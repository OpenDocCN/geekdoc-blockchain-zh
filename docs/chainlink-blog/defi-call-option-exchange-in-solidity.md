# 用 Chainlink 价格源建立 DeFi 看涨期权交易所

> 原文：<https://blog.chain.link/defi-call-option-exchange-in-solidity/>

仅 DeFi 一项就涵盖了大量智能合约用例，从[区块链投票](https://blog.chain.link/blockchain-voting-using-a-chainlink-alarm-clock-oracle/)和[分散彩票](https://blog.chain.link/how-to-build-a-blockchain-lottery-2/)到[产量农业](https://chain.link/education/defi/yield-farming)，当然还有分散交易所。本指南涵盖了如何使用[chain link Price Feed](https://chain.link/solutions/defi)Oracle 在以太坊主网上实现简单的买入期权 DeFi 交换。对于看跌期权，也可以很容易地修改这个实现。这种期权交易所的一个强大的特点是，所有的价值都是通过合约转移的，没有任何可信方，直接在双方之间转移。在实现 [DeFi](https://chain.link/education/defi) 的理想中，没有中间人，只有合同和分散的链接价格。

在开发 DeFi 期权交易所的过程中，我们将涉及:

*   比较字符串的可靠性
*   整数形式的定点小数
*   创建和初始化令牌接口，如 LINK
*   在用户/合同之间转移令牌
*   令牌转移批准
*   萨吉马思
*   [智能合约](https://chain.link/education/smart-contracts) ABI 接口
*   用 require()强制事务状态
*   Ethereum msg.value 及其与代币价值交易的不同之处
*   int 和 uint 之间的转换
*   应付地址
*   当然，使用 Chainlink 的聚合器接口来检索 DeFi 价格数据

本指南的代码可以在 [GitHub](https://github.com/gmondok/ChainlinkCallOptions/blob/main/chainlinkOptions.sol) 和 [Remix](https://remix.ethereum.org/#version=soljson-v0.6.12+commit.27d51765.js&optimize=false&gist=19152b9f6938c97052bb93361ca26457) 上找到。在我们开始之前，先简单介绍一下什么是期权合约:期权合约给你一个“选择权”,让你在某个特定的时间内以约定的价格执行交易。具体来说，如果合约是购买股票/代币等的期权，这就是所谓的看涨期权。此外，其中显示的代码可以很容易地重新用于看跌期权。看跌期权类似于看涨期权的逆期权，而不是能够购买资产的合同，看跌期权是一种便于以预先约定的价格出售的合同。一些术语:

*   成交价格:可以购买/出售资产的商定价格
*   溢价:购买合约时支付给期权发行人(卖方)的费用
*   到期日:合同不再有效的时间
*   行使:当合约购买者选择使用他们的期权以执行价格买入/卖出

无论是在 Solidity 中实现一个 put 还是 call 选项，我们首先需要我们常用的基础知识，比如导入、构造函数和全局变量。

```
pragma solidity ^0.6.7;

import "https://github.com/smartcontractkit/chainlink/blob/develop/evm-contracts/src/v0.6/interfaces/LinkTokenInterface.sol";
import "https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/interfaces/AggregatorV3Interface.sol";
import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/math/SafeMath.sol";

contract chainlinkOptions {
    //Overflow safe operators
    using SafeMath for uint;

    //Pricefeed interfaces
    AggregatorV3Interface internal ethFeed;
    AggregatorV3Interface internal linkFeed;

    //Interface for LINK token functions
    LinkTokenInterface internal LINK;
    uint ethPrice;
    uint linkPrice;

    //Precomputing hash of strings
    bytes32 ethHash = keccak256(abi.encodePacked("ETH"));
    bytes32 linkHash = keccak256(abi.encodePacked("LINK"));
    address payable contractAddr;

    //Options stored in arrays of structs
    struct option {
        uint strike; //Price in USD (18 decimal places) option allows buyer to purchase tokens at
        uint premium; //Fee in contract token that option writer charges
        uint expiry; //Unix timestamp of expiration time
        uint amount; //Amount of tokens the option contract is for
        bool exercised; //Has option been exercised
        bool canceled; //Has option been canceled
        uint id; //Unique ID of option, also array index
        uint latestCost; //Helper to show last updated cost to exercise
        address payable writer; //Issuer of option
        address payable buyer; //Buyer of option
    }
    option[] public ethOpts;
    option[] public linkOpts;

    //Kovan feeds: https://docs.chain.link/docs/reference-contracts
    constructor() public {
        //ETH/USD Kovan feed
        ethFeed = AggregatorV3Interface(0x9326BFA02ADD2366b30bacB125260Af641031331);
        //LINK/USD Kovan feed
        linkFeed = AggregatorV3Interface(0x396c5E36DD0a0F5a5D33dae44368D4193f69a1F0);
        //LINK token address on Kovan
        LINK = LinkTokenInterface(0xa36085F69e2889c224210F603D836748e7dC0088);
        contractAddr = payable(address(this));
    }
}
```

对于我们的导入，我们需要 Chainlink 的聚合器接口来公开价格馈送功能，还需要 LINK token 接口，因为我们将执行 LINK token 传输，并且需要令牌合同提供的 ERC20 功能。最后，我们导入了 OpenZeppelin 的 SafeMath 契约，它已经成为一个标准库，用于执行内置溢出检查的算法，这是 Solidity 的默认操作符所没有的。

接下来，我们重新定义我们的算术类型 uint，以使用导入的 SafeMath，定义我们的价格提要、链接接口、价格变量，计算 ETH 和链接字符串的“keccak256”散列以供以后使用，以及一个地址变量以存储我们的合同地址。值得注意的是，该地址被定义为“应付”，因为我们的合同需要在其地址接收资金。然后，在构造时，将接口初始化为它们的 Kovan 契约地址，这样就可以调用这些契约的函数，并使用“address(this)”设置我们的契约地址。我们再次将其转换为 payable，因为 address()将返回一个非 payable 地址类型。

至于选项本身的数据结构，在这种情况下，结构数组是一种有效的数据结构，但是结构的链表也是有效的。标准数组的缺点是我们可以直接访问我们想要的选项，不像链表，但是删除数组中的条目代价很高。为了避免这种情况，我们只是从不删除选项，而是将它们标记为过期/取消，从而以空间换取速度和低复杂性。通过 O(1)操作，写、买和行使期权都变得更有效率。

## 链接价格源

```
//Returns the latest LINK price
function getLinkPrice() public view returns (uint) {
    (
        uint80 roundID, 
        int price,
        uint startedAt,
        uint timeStamp,
        uint80 answeredInRound
    ) = linkFeed.latestRoundData();

    // If the round is not complete yet, timestamp is 0
    require(timeStamp > 0, "Round not complete");
    //Price should never be negative thus cast int to unit is ok
    //Price is 8 decimal places and will require 1e10 correction later to 18 places
    return uint(price);
}
```

我们实现的第一个函数是 ETH 和 LINK price feeds 的两个 getters，ETH 与上面看到的 LINK 函数相同，但带有 ethFeed。这些方法简单地调用我们初始化的提要的 latestRoundData()函数，并自动返回最新的分散式广域市场聚合价格数据。既然是查看功能，这个连气都不需要！对默认 price feed getters 的一个更改是，我们将 price 从 int 转换为 uint，以便该类型与我们后面使用 uint 的函数相匹配。值得注意的是，这种转换是可以的，因为这些价格永远不会是负数，因此不会使用 int 提供的符号位。在类型之间进行转换时，应该仔细考虑这样的问题。

## 买入期权

```
//Allows user to write a covered call option
//Takes which token, a strike price(USD per token w/18 decimal places), premium(same unit as token), expiration time(unix) and how many tokens the contract is for
function writeOption(string memory token, uint strike, uint premium, uint expiry, uint tknAmt) public payable {
    bytes32 tokenHash = keccak256(abi.encodePacked(token));
    require(tokenHash == ethHash || tokenHash == linkHash, "Only ETH and LINK tokens are supported");
    updatePrices();

    if (tokenHash == ethHash) {
        require(msg.value == tknAmt, "Incorrect amount of ETH supplied"); 
        uint latestCost = strike.mul(tknAmt).div(ethPrice.mul(10**10)); //current cost to exercise in ETH, decimal places corrected
        ethOpts.push(option(strike, premium, expiry, tknAmt, false, false, ethOpts.length, latestCost, msg.sender, address(0)));
    } else {
        require(LINK.transferFrom(msg.sender, contractAddr, tknAmt), "Incorrect amount of LINK supplied");
        uint latestCost = strike.mul(tknAmt).div(linkPrice.mul(10**10));
        linkOpts.push(option(strike, premium, expiry, tknAmt, false, false, linkOpts.length, latestCost, msg.sender, address(0)));
    }
}
```

有了初始设置和价格供给，我们现在可以开始期权的功能，从期权合约的写作开始。编写器调用 writeOption 并提供选项的所有属性，使用 18 位数字作为“小数”。定义我们使用的小数点标准以保持合同中使用的所有数字的一致性非常重要。例如，整数 777 没有小数，但是如果我们在逻辑上决定我们在一个二进制定点空间中操作，我们知道它实际上代表 7.77。我们决定使用 18 位十进制标准，因为 ETH 和 LINK 都有 18 位小数，较小的十进制数可以简单地通过添加零扩展到 18 位。

接下来是我们第一次使用之前散列的 ETH 和 LINK 字符串。为了确定作者试图为哪个令牌编写选项，我们需要能够比较字符串，但是 Solidity 不支持字符串之间的==运算符，因为它们的长度是动态的。我们可以简单地用 keccak256 散列函数将每个字符串散列为一组 32 字节的散列，然后直接比较这些散列，而不是编写一个函数来检查和比较字符串的每个字节。同样的哈希，同样的字符串。

现在，我们知道了作者正在为哪个令牌编写选项，并需要做出相应的反应。如果是 ETH，我们可以使用 msg.value 来确认 ETH 的正确金额是否与函数调用事务一起发送，以便为期权提供资金。我们使用 require()函数严格执行这一要求。如果 require 的第一个字段的值不为 true，交易将被拒绝，并且不会发生任何事情。通过这种方式，我们保证所有选项都有合同规定的正确金额。当检查通过时，我们就可以创建选项，为它提供所有必要的字段来填充结构。LatestCost，根据当前 ETH 价格，使用 SafeMath 函数而不是默认运算符计算行使期权的当前成本。当前价格由我们的 updatePrices() helper 函数检索，该函数更新全局 ETH 和链接价格。请注意，ethPrice 乘以 10 的 10 次方。这样做是因为链接价格反馈返回的美元价格是 8 进制的，但正如前面提到的，我们正在使用 18 进制的标准。添加 10 个零数字纠正了这一点，因此价格现在总共有 18 个数字表示小数，与 ETH 和 LINK 令牌相匹配。最后，我们将 option struct 推入 ethOpts 数组，正式编写了 option 并提供了资金。



![LINK option](img/8c318b36afeb3e41de1a7314265b9f44.png)

<figcaption id="caption-attachment-634" class="wp-caption-text">写一个链接期权，行权价 10 美元，链接溢价 0.1，Unix 到期时间，换 1 个链接令牌。</figcaption>





如果选项是针对 LINK，情况就有点不同了。Msg.value 仅提供交易中的 ETH 数量，为了强制执行一定数量的链接资金，我们直接与链接令牌合同进行交互。因为我们导入并初始化了 LINK token 接口，所以我们可以访问所有的 [LINK token 函数](https://github.com/smartcontractkit/chainlink/blob/develop/evm-contracts/src/v0.6/interfaces/LinkTokenInterface.sol)，其中之一是 transferFrom()，顾名思义，它将 LINK 从一个地址传输到另一个地址。当然，我们不希望任何合约能够移动你的链接，所以期权作者必须首先调用链接的 approve()函数，并指定他们允许移动多少链接，以及他们允许哪个合约移动它。

## 合同 ABI 接口

当您在 Etherscan 上查看合同时，有两个选项卡，阅读合同和编写合同，这两个选项卡允许您与合同的功能进行交互。例如:[链接令牌 mainnet 契约](https://etherscan.io/token/0x514910771af9ca656af840dff83e8264ecf986ca#writeContract)。Etherscan 知道这些函数是什么，以及如何基于契约的 ABI 调用它们，该契约是一个概述函数调用的 JSON 规范。这是为 mainnet 合同提供的，但对于 Kovan LINK，我们需要导入它。ABI 可以在[链接令牌](https://github.com/smartcontractkit/LinkToken/tree/master/contracts/v0.6) Github 中找到。值得庆幸的是，在生产系统中，这将通过 web3js 调用在 UI 中处理，导致用户获得一个简单的元掩码请求来批准，但现在在我们的开发示例中，我们是手动完成的。



![Kovan LINK Contract](img/4a03f071bcc772fdc83e7a9d9a5c58e0.png)

<figcaption id="caption-attachment-635" class="wp-caption-text">通过水电部与科万联系合同使用进口 ABI。</figcaption>



<figcaption></figcaption>





![Approving LINK Contract](img/ed0453139ce4bf6aed0e5c39dfbdc4f6.png)

<figcaption id="caption-attachment-636" class="wp-caption-text">批准 Kovan LINK 向/从我们的地址和期权合同地址转移 100 LINK。</figcaption>





## 购买看涨期权

```
//Purchase a call option, needs desired token, ID of option and payment
function buyOption(string memory token, uint ID) public payable {
    bytes32 tokenHash = keccak256(abi.encodePacked(token));
    require(tokenHash == ethHash || tokenHash == linkHash, "Only ETH and LINK tokens are supported");
    updatePrices();

    if (tokenHash == ethHash) {
        require(!ethOpts[ID].canceled && ethOpts[ID].expiry > now, "Option is canceled/expired and cannot be bought");
        //Transfer premium payment from buyer
        require(msg.value == ethOpts[ID].premium, "Incorrect amount of ETH sent for premium");

        //Transfer premium payment to writer
        ethOpts[ID].writer.transfer(ethOpts[ID].premium);
        ethOpts[ID].buyer = msg.sender;
    } else {
        require(!linkOpts[ID].canceled && linkOpts[ID].expiry > now, "Option is canceled/expired and cannot be bought");
        //Transfer premium payment from buyer to writer
        require(LINK.transferFrom(msg.sender, linkOpts[ID].writer, linkOpts[ID].premium), "Incorrect amount of LINK sent for premium");
        linkOpts[ID].buyer = msg.sender;
    }
}
```

现在期权写好了，也有了资金，希望有人想买！买方只需说明他们是想购买 ETH 期权还是 LINK 期权以及该期权的 ID。由于选项阵列被定义为公共的，它们自动可见，无气体，因此买方可以查看所有可用的选项及其 ID 字段。选择一个选项后，我们再次使用 require()函数来验证是否发送了正确的金额来支付保险费。这一次，对于 ETH 来说，我们要确认的不仅仅是 msg.value，我们还需要将那笔溢价费用转给作者。Solidity 中的所有 ETH 地址都有一个 address.transfer()函数，我们利用这个函数，将保险费金额从合同中转移到作者。然后，我们设置选项的买方地址字段，购买就完成了。在链接的情况下，事情稍微简单一些。我们可以使用转账功能(批准后)将溢价从买方直接转账给卖方，而使用 ETH，溢价从买方流向合同再流向卖方。

## 行使期权

```
//Exercise your call option, needs desired token, ID of option and payment
function exercise(string memory token, uint ID) public payable {
    //If not expired and not already exercised, allow option owner to exercise
    //To exercise, the strike value*amount equivalent paid to writer (from buyer) and amount of tokens in the contract paid to buyer
    bytes32 tokenHash = keccak256(abi.encodePacked(token));
    require(tokenHash == ethHash || tokenHash == linkHash, "Only ETH and LINK tokens are supported");

    if (tokenHash == ethHash) {
        require(ethOpts[ID].buyer == msg.sender, "You do not own this option");
        require(!ethOpts[ID].exercised, "Option has already been exercised");
        require(ethOpts[ID].expiry > now, "Option is expired");

        //Conditions are met, proceed to payouts
        updatePrices();
        //Cost to exercise
        uint exerciseVal = ethOpts[ID].strike*ethOpts[ID].amount;
        //Equivalent ETH value using Chainlink feed
        uint equivEth = exerciseVal.div(ethPrice.mul(10**10)); //move decimal 10 places right to account for 8 places of pricefeed

        //Buyer exercises option by paying strike*amount equivalent ETH value
        require(msg.value == equivEth, "Incorrect LINK amount sent to exercise");
        //Pay writer the exercise cost
        ethOpts[ID].writer.transfer(equivEth);
        //Pay buyer contract amount of ETH
        msg.sender.transfer(ethOpts[ID].amount);
        ethOpts[ID].exercised = true;  
    } else {
        require(linkOpts[ID].buyer == msg.sender, "You do not own this option");
        require(!linkOpts[ID].exercised, "Option has already been exercised");
        require(linkOpts[ID].expiry > now, "Option is expired");
        updatePrices();
        uint exerciseVal = linkOpts[ID].strike*linkOpts[ID].amount;
        uint equivLink = exerciseVal.div(linkPrice.mul(10**10));

        //Buyer exercises option, exercise cost paid to writer
        require(LINK.transferFrom(msg.sender, linkOpts[ID].writer, equivLink), "Incorrect LINK amount sent to exercise");
        //Pay buyer contract amount of LINK
        require(LINK.transfer(msg.sender, linkOpts[ID].amount), "Error: buyer was not paid");
        linkOpts[ID].exercised = true;
    }
}
```

对于期权的所有者来说，希望 ETH 或 LINK 的价格上升到执行价格以上，足以使他们的期权变得有利可图。在这种情况下，他们会希望“行使”他们的期权，以履约价格购买代币。这一次，我们必须首先确认几个条件，即合同由消息发送者拥有，合同还没有被执行，以及到期时间大于我们的当前时间“现在”。如果这些要求的检查中的任何一个失败，则事务被恢复。



![Remix output](img/7153be3db8f39e21b1045ab14b3696f7.png)

<figcaption id="caption-attachment-637" class="wp-caption-text">未通过一个或多个 require 语句的事务的示例重新混合输出。</figcaption>





如果检查通过，我们继续将行权成本转移给卖方，将合约金额转移给买方。当行使时，买方为每一个代币支付执行价。然而，执行价格以美元为单位，但合约金额以 ETH 或 link 为单位，这意味着我们需要使用 Chainlink 价格源来计算相当于行权成本的 ETH 或 LINK 金额。一旦转换成等价的 ETH 或 LINK 值，我们就可以进行适当的转账。为此，我们对 ETH 使用前面介绍过的 msg.value/address.transfer 方法，对 LINK 使用 transferFrom()。

![Etherscan transaction](img/f653d1d80524f5967aacf88724905d86.png)

以上是成功执行期权的交易。在每条链接 11.56 美元的价格下，1 条链接执行 10 美元的执行合同，这意味着买方只需为该链接支付 10 美元，而不是 11.56 美元。10/11.56 = 0.86，导致买方仅支付 0.86 链接来接收 1 个链接。算上 0.1 LINK 的溢价费用，这个交易员一共赚了 0.04 LINK。

## 取消/移除资金

```
//Allows option writer to cancel and get their funds back from an unpurchased option
function cancelOption(string memory token, uint ID) public payable {
    bytes32 tokenHash = keccak256(abi.encodePacked(token));
    require(tokenHash == ethHash || tokenHash == linkHash, "Only ETH and LINK tokens are supported");

    if (tokenHash == ethHash) {
        require(msg.sender == ethOpts[ID].writer, "You did not write this option");
        //Must not have already been canceled or bought
        require(!ethOpts[ID].canceled && ethOpts[ID].buyer == address(0), "This option cannot be canceled");
        ethOpts[ID].writer.transfer(ethOpts[ID].amount);
        ethOpts[ID].canceled = true;
    } else {
        require(msg.sender == linkOpts[ID].writer, "You did not write this option");
        require(!linkOpts[ID].canceled && linkOpts[ID].buyer == address(0), "This option cannot be canceled");
        require(LINK.transferFrom(address(this), linkOpts[ID].writer, linkOpts[ID].amount), "Incorrect amount of LINK sent");
        linkOpts[ID].canceled = true;
    }
}

//Allows writer to retrieve funds from an expired, non-exercised, non-canceled option
function retrieveExpiredFunds(string memory token, uint ID) public payable {
    bytes32 tokenHash = keccak256(abi.encodePacked(token));
    require(tokenHash == ethHash || tokenHash == linkHash, "Only ETH and LINK tokens are supported");

    if (tokenHash == ethHash) {
        require(msg.sender == ethOpts[ID].writer, "You did not write this option");
        //Must be expired, not exercised and not canceled
        require(ethOpts[ID].expiry <= now && !ethOpts[ID].exercised && !ethOpts[ID].canceled, "This option is not eligible for withdraw");
        ethOpts[ID].writer.transfer(ethOpts[ID].amount);
        //Repurposing canceled flag to prevent more than one withdraw
        ethOpts[ID].canceled = true;
    } else {
        require(msg.sender == linkOpts[ID].writer, "You did not write this option");
        require(linkOpts[ID].expiry <= now && !linkOpts[ID].exercised && !linkOpts[ID].canceled, "This option is not eligible for withdraw");
        require(LINK.transferFrom(address(this), linkOpts[ID].writer, linkOpts[ID].amount), "Incorrect amount of LINK sent");
        linkOpts[ID].canceled = true;
    }
}
```

随着市场条件的变化，合约作者可能希望取消他们的期权，并在尚未买入的情况下收回资金。类似地，期权可能在没有被行使的情况下到期，在这种情况下，卖方的资金仍然存在于合同中，他们肯定希望收回这些资金。为此，我们添加了 cancelOption()和 retrieveExpiredFunds()函数。

这两个函数最重要的是满足正确的取款条件。在非常特殊的情况下，应该允许作者转移他们的资金，而且他们显然只能这样做一次。在取消的情况下，作者应该不能取消已经购买的合同，所以我们确认买方地址仍然是其初始零值。此外，我们确认期权尚未被取消，然后退还资金。在检索过期资金的情况下，条件略有不同。在这种情况下，有可能期权被购买但从未行使，这意味着资金仍应返还给作者。我们确认合同已到期，且尚未执行。在这种情况下，我们还重新调整了期权的取消标志，如果条件满足，再次返回资金。

希望本指南已经阐明了 [Chainlink 的众多用途之一](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/)，你今天可以在 mainnet 上开发这些用途，并且展示了一些 Solidity 独有的功能。如果你想了解更多的 Chainlink 功能，请查看 [VRF](https://blog.chain.link/chainlink-vrf-on-chain-verifiable-randomness/) 的可证明随机数生成，或者了解 Chainlink 如何通过[公平排序服务](https://blog.chain.link/chainlink-fair-sequencing-services-enabling-a-provably-fair-defi-ecosystem/)来打击 miner 抢注。

如果你是一名开发人员，并希望将你的智能合同连接到链外数据和系统，请访问[开发人员文档](https://docs.chain.link/)，并加入关于[不和谐](https://discordapp.com/invite/aSK4zew)的技术讨论。如果您想安排一次电话会议来更深入地讨论整合事宜，请点击此处的。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://defi.chain.link/)