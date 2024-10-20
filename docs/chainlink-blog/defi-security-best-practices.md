# 十大 DeFi 安全最佳实践

> 原文：<https://blog.chain.link/defi-security-best-practices/>

无论你是在构建 [DeFi 协议](https://chain.link/education/defi)还是任何其他智能合约应用程序，在进入区块链主网之前，都需要考虑许多安全因素。许多团队在审查他们的代码时只关注可靠性缺陷，但通常有更多的事情要做，以确保 dApp 的安全性足够坚固，使其可以维护。了解最常见的 DeFi 安全漏洞，如 oracle 攻击、暴力攻击和许多其他威胁，可能会为您和您的用户节省数十亿美元，并让您头疼几个月。无论您是派生一个工作代码库还是从头构建一切，在启动代码之前做好尽职调查都是必不可少的。

![](img/ce847be6c0fe450a612edbedd734cba8.png)

考虑到这一点，让我们来看看 DeFi 安全性的 10 个最佳实践，它们将有助于防止您的应用成为攻击的受害者，减少与用户的不愉快对话，并保护和巩固您作为超安全开发人员的声誉。

## 1.注意重入攻击

DeFi 安全攻击的一种常见类型是 [重入攻击](https://docs.soliditylang.org/en/latest/security-considerations.html#re-entrancy)——这种形式就是臭名昭著的[DAO hack](https://www.gemini.com/cryptopedia/the-dao-hack-makerdao)。这是指协定在更新自身状态之前调用外部协定。

引用可靠性文件:

> “一个合同(A)与另一个合同(B)之间的任何互动，以及任何将控制权移交给该合同(B)的行为。这使得 B 有可能在这个交互完成之前回调到 A。”

让我们看一个例子:

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

// THIS CONTRACT CONTAINS A BUG - DO NOT USE
contract Fund {
 /// @dev Mapping of ether shares of the contract.
 mapping(address => uint) shares;
 /// Withdraw your share.
function withdraw() public {
        (bool success,) = msg.sender.call{value: shares[msg.sender]}("");
 if (success)
 shares[msg.sender] = 0;
 }
}
```

在这个函数中，我们用“msg.sender.call”调用另一个帐户。我们必须记住的是，这可能是另一个智能合约！

被调用的外部契约可以编码为在`( bool success，)= msg . sender . call { value:shares[msg . sender]}(" ")之前再次调用撤回函数**；`** 回报。这将允许用户在状态更新之前提取合同中的所有资金。

合同可以有几个 [特殊功能](https://docs.soliditylang.org/en/v0.8.9/contracts.html?highlight=receive#special-functions) ，即‘接收’和‘回退’。如果您将 ETH 发送给另一个合同，它将自动发送到“接收”功能。如果“接收”功能然后将 *点回到* 原始合同，则在您有机会将余额更新为 0 之前，您可能会继续撤销。

让我们看看这个合同可能是什么样子:

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

// THIS CONTRACT IS EVIL - DO NOT USE
contract Steal {
 receive() external payable {
        IFundContract(addressOfFundContract).withdraw();
    }
}
```

在该函数中，当你将 ETH 发送到“窃取”合约后，它将调用“接收”函数，该函数将 *返回* 到“基金”合约。此时，我们还没有运行“shares[msg.sender] = 0 ”,因此合同仍然认为用户拥有可以退出的份额。

### **解决方案:** 在转移 ETH/tokens 或调用不受信任的外部契约之前更新契约的内部状态

有几种方法可以做到这一点，从使用互斥锁到简单地对函数调用排序，只在状态更新后才调用外部契约或函数。 一个简单的修复方法是在调用任何外部未知契约之前更新状态:

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract Fund {
 /// @dev Mapping of ether shares of the contract.
    mapping(address => uint) shares;

 /// Withdraw your share.
 function withdraw() public {
 uint share = shares[msg.sender];
 shares[msg.sender] = 0;
 (bool success,)=msg.sender.call{<wbr>value: share}("");
 }
}
```

### 转移、呼叫和发送

一直以来，Solidity 安全专家都推荐 **而不是** 使用上面的方法。他们建议不要使用“呼叫”功能，而是使用“转移”，就像这样:

```
payable(msg.sender).transfer(shares[msg.sender]);
```

我们之所以提到这一点，是因为你可能会看到一些相互冲突的资源在暗示着一些与我们的建议不同的东西。此外，您还会听到“发送”功能。这些中的每一个都可以用来发送 ETH，但都有细微的差别。

*   `transfer `:最多有 2300 气，失败时抛出错误
*   `send `:最大 2300 gas，失败时返回` false'
*   `call `:将所有天然气转发给下一个合同，失败时返回` false'

转移和发送在很长一段时间内被认为是“更好”的做法，因为 2300 气体确实只够发射一次事件或其他无害的操作；接收契约不能回调或者做任何恶意的事情，除了发出卑鄙的事件，因为如果他们尝试的话会耗尽能量。

然而，这只是当前的设置， [天然气成本会随着不断变化的基础设施生态系统而变化](https://consensys.net/diligence/blog/2019/09/stop-using-soliditys-transfer-now/) 。我们已经看到 EIP 中的 [改变不同操作码](https://eips.ethereum.org/EIPS/eip-1884#motivation) 的气体成本。这意味着将来可能会有一天，调用一个函数的开销少于 2300 gas，或者事件的开销会超过 2300 gas，这意味着任何要发出事件的接收函数在将来都会失败。

这意味着在调用项目之外的任何合同之前更新状态是最佳实践。 另一种可能的缓解是对关键函数施加互斥，例如[*ReentrancyGuard*](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/ReentrancyGuard.sol)中的 *不可重入* 修饰符。采用这样的互斥体将防止交换契约被重新输入。这实际上是添加了一个“锁”,这样在契约执行时，调用契约就不能“重新进入”它。

可重入攻击的另一个版本是跨函数可重入。这里有一个跨函数重入攻击的例子，为了可读性，使用了“transfer”函数:

```
mapping (address => uint) private userBalances;

function transfer(address _recipient, uint _amount) {
 require(userBalances[msg.sender] >= _amount);
 userBalances[_recipient] += _amount;
 userBalances[msg.sender] -= _amount;
}

function withdrawBalance() public {
 uint amountToWithdraw = userBalances[msg.sender];
 msg.sender.transfer(amountToWithdraw);
 userBalances[msg.sender] = 0;
}
```

在一个函数完成之前，可以调用另一个函数。这应该是一个明确的提醒，要在发送 ETH 之前更新状态。有些协议甚至在它们的函数上添加了 [互斥锁](https://stackoverflow.com/questions/34524/what-is-a-mutex) ，这样如果另一个函数还没有返回，这些函数就不能被调用。

除了常见的可重入漏洞，还有一些可重入攻击可以由特定的 EIP 机制触发，如 ERC777。ERC-777([T5)【EIP-777](https://eips.ethereum.org/EIPS/eip-777))是建立在 ERC-20 ( [)之上的以太币令牌标准。它向后兼容 ERC-20，增加了一个功能，使“运营商”能够代表令牌所有者发送令牌。关键的是，该协议还允许为令牌所有者添加“发送/接收挂钩”，以便在发送/接收交易时自动采取进一步的行动。](https://eips.ethereum.org/EIPS/eip-20)

从 Uniswap imBTC 黑客攻击中可以看出，该漏洞实际上是由 uni WAP 交换机在余额更改之前发送 ETH 造成的。在那次攻击中，Uniswap 函数的实现没有遵循广为采用的 [检查-效果-交互](https://fravoll.github.io/solidity-patterns/checks_effects_interactions.html) 模式，该模式是为了保护智能合约免受可重入攻击而发明的，在此之后，令牌传输应该在任何值传输之前进行。

## 2.使用德克斯或 AMM 储备作为价格甲骨文将导致一个漏洞

这是攻击协议最常用的方法之一，也是最容易防范的 DeFi 安全攻击手段之一。如果你使用 **`getReserves()`** 作为一种量化价格的方式，这应该是一个危险信号。当用户操纵订单簿或基于自动做市商的[分散交易(DEX)](https://blog.chain.link/dex-decentralized-exchange/) 的现货价格时，通常通过使用 [快速贷款](https://blog.chain.link/flash-loans-and-the-importance-of-tamper-proof-oracles/) ，就会出现这种集中价格 oracle 漏洞。该协议然后使用 DEX 报告的价格作为他们的价格预测，以触发虚假清算、发放过大贷款或触发不公平交易的形式导致智能合约执行中的扭曲。由于这个漏洞，即使是像[uni swap](https://app.uniswap.org/)这样的热门 dex 也不建议单独使用其储备作为定价神谕。

An[Oracle](https://chain.link/education/blockchain-oracles)是获取外部数据并将其传递到区块链或进行某种外部计算并将结果传递到智能合约的任何外部实体。在基于 DEX 或 AMM 的 oracle 机制的情况下，oracle 提取的数据源是由 DEX 上一次成功交易调整的储备价格，该价格可能与资产的更广泛市场价格不同步，例如在流动性不足的情况下进行的大宗交易。与所有交易所的成交量加权平均价格相比，这将导致价格要么涨得很高(大买单)，要么跌得很低(大卖单)。

快速贷款加剧了这一问题，因为它允许任何用户在没有任何抵押品的情况下获得大量临时资金，以进行大宗交易。用户经常将问题归咎于闪贷，称之为“闪贷攻击”然而，根本问题在于，dex 本身是不安全的价格先知，因为现货价格很容易被操纵，导致依赖先知的协议引用不准确的价格。这些被更准确地描述为“甲骨文操纵攻击”，并在 DeFi 生态系统中占据了大量的[](https://www.coindesk.com/flash-loans-centralized-price-oracles)。所有开发人员都应该在其智能合同中删除 oracle 操纵攻击媒介。

让我们看看最近一次攻击的代码，这次攻击造成了 3000 万美元的损失，随后使协议的奖励令牌价格暴跌:

为了便于理解，对该函数进行了细微的修改，但实际上是一样的。

```
function valueOfAsset(address asset, uint amount) public view override returns (uint valueInBNB, uint valueInDAI) {
 if (keccak256(abi.encodePacked(IProtocolPair(asset).symbol())) == keccak256("Protocol-LP")) {
 (uint reserve0, uint reserve1, ) = IPancakePair(asset).getReserves();
 valueInWETH = amount.mul(reserve0).mul(2).div(IProtocolPair(asset).totalSupply());
 valueInDAI = valueInWETH.mul(priceOfETH()).div(1e18);
 }
}
```

这个协议有一个 oracle 设置，它从一个 DEX 获取现货价格。在 DEX 中，用户可以将一对代币存入流动性池合约(例如代币 A +代币 B)，允许用户根据汇率在这些代币之间进行互换，该汇率是根据池中每一侧的流动性数量计算的。假设该协议是安全的，因为它的大部分代码是 Uniswap 的流行协议 [的分支。然而，在顶部添加了奖励令牌计划，以便当用户将流动性存入特定池时，他们不仅可以获得收据令牌(LP 令牌),代表对自己的流动性和池费用百分比的要求，还可以获得流动性挖掘奖励。一名黑客能够通过获得一笔快速贷款并将额外的资本存入流动性池来操纵这种奖励铸造功能。这让他们能够以错误的转换率 印刷 奖励代币。](https://github.com/Uniswap/uniswap-v2-core/tree/4dd59067c76dea4a0e8e4bfdda41877a6b16dedc)

在这个函数中，我们可以看到攻击者首先做的事情之一是根据资产池中两种资产的储备金额来获取流动性池中资产之间的汇率。调用下面一行来获取流动性池中的准备金:

```
(uint reserve0, uint reserve1, ) = IProtocolPair(asset).getReserves();
```

你可以想象一个有 5 个 wet 和 10 个 DAI 的流动性池会使‘reserve 0’变成‘5’，而‘reserve 1’变成‘10’。WETH 代表“包裹以太坊”，是以太坊的 ERC20 版本，ETH 和 WETH 之间的转换率为 1 比 1。

一旦你有了协议中的储备数量，找到任一资产价格的简单方法是将两个储备相除得到一个汇率。例如，如果我们的流动性池中有 5 WETH 和 10 DAI，则转换率为 1 WETH 到 2 DAI，因为我们只是将 10 除以 5。

虽然使用分散的交易所可以很好地交换具有即时流动性的资产，但它们并不能产生良好的现货价格预测，因为它们的价格很容易被操纵，特别是通过快速贷款，并且只代表任何给定资产总交易量的一小部分。当用于铸造奖励代币时，智能合同执行很容易变得不准确(为了便于理解，稍作修改):

```
// ProtocolMinterV2.sol 0x819eea71d3f93bb604816f1797d4828c90219b5d
function mintReward(address asset /* LP token */, uint _withdrawalFee /* 0 */, uint _performanceFee /* 0.00015... */, address to /* attacker */, uint) external payable override onlyMinter {
 uint feeSum = _performanceFee.add(_withdrawalFee);
 _transferAsset(asset, feeSum); // transfers LP tokens from VaultFlipToFlip to this
    uint protocolETHAmount = _zapAssetsToProtoclETH(asset, feeSum, true);

 if (protocolETHAmount == 0) return;

 IEIP20(PROTOCOL_ETH).safeTransfer(PROTOCOL_POOL, protocolETHAmount);
    IStakingRewards(PROTOCOL_POOL).notifyRewardAmount(protocolETHAmount);

 (uint valueInETH,) = priceCalculator.valueOfAsset(PROTOCOL_ETH, protocolETHAmount); // returns inflated value
 uint contribution = valueInETH.mul(_performanceFee).div(feeSum);
 uint mintReward = amountRewardToMint(contribution);
    _mint(mintReward, to); // mints the reward to the liquidity providers and attacks
}
```

在这个例子中，支付用户的主要函数是 **`_mint(mintReward，to)；`** 行。我们可以看到，该功能是基于用户在流动性池中锁定的价值来创造的。因此，如果用户突然在流动性池中拥有一笔 *lot* 的资产(由于快速贷款攻击)，那么用户可以轻松地为自己铸造大量的奖励代币，从代币的用户处窃取。

然而，这仍然没有给他们带来他们想要的利润水平。所以当他们被给予额外的代币时，他们被给予的代币数量由于被操纵的神谕而大大增加。假设这个协议认为它会给用户 5 美元的奖励——相反，它会发出 5000 美元的奖励。这正是这个特定漏洞所发生的情况。

通过这种设置，用户可以轻松获得快速贷款，将临时资本存入流动性池的一方，赚取大量回报，然后偿还快速贷款，以其他流动性提供者为代价获利。

为避免快速贷款资助的市场操纵问题，通常提出的解决方案是从 DEX 市场中获取时间加权平均价格(TWAP )(例如，一小时内资产的平均价格)。虽然这可以防止快速贷款扭曲 oracle 价格，但由于快速贷款只存在于单个交易/区块中，而 TWAP 是多个区块的平均值，因此这不是一个完整的解决方案，因为 TWAP 有自己的权衡。在波动时期，TWAP 预言变得不准确，这可能导致下游事件，如无法及时清偿抵押不足的贷款。此外，TWAP oracle 没有提供足够的市场覆盖范围，因为只跟踪一个指数，这使它们容易受到交易所之间流动性/交易量变化的影响，从而扭曲了 TWAP Oracle 给出的价格。

### **解决方案:** 使用一个分散的 Oracle 网络

DeFi 安全最佳实践不是使用集中式 oracle(在本例中为单个连锁交易所)来确定汇率，而是使用分散式 oracle 网络来发现反映广泛市场覆盖范围的汇率的真实值。DEX 作为一个交易所是分散的，但它是定价信息的集中参考点。

相反，您会希望收集所有流动性集中和分散交易所的价格，按交易量对价格进行加权，并删除异常值/清洗交易，以获得基础资产全球汇率的分散和准确视图，从而确保全面的市场覆盖。如果你的资产价格代表了所有交易环境下的成交量加权全球平均值，那么一笔快速贷款是否拉低了一家交易所的资产价格就无关紧要了。

此外，由于快速贷款只存在于单个交易中(同步)，因此它们对分散式价格馈送没有影响，分散式价格馈送在单独的交易中生成具有市场范围定价的 oracle 更新(异步更新)。Chainlink oracle networks 的分散式架构及其实现的广泛市场覆盖保护了 DeFi 协议免受闪贷资助的市场操纵，这就是为什么越来越多的 DeFi 项目正在集成[chain link Price Feeds](https://chain.link/data-feeds)以防止价格 oracle 漏洞，并确保在突然的交易量变化期间准确定价。

您可以从 [Chainlink 数据馈送](https://docs.chain.link/docs/using-chainlink-reference-contracts/) 获得您的转换率，而不是使用**【get reserves`**来计算价格，这些数据馈送是 oracle 节点的分散网络，提供反映所有相关 cex 和 dex 的交易量加权平均价格(VWAP)。

```
pragma solidity ^0.6.7;

import "@chainlink/contracts/src/v0.6/interfaces/AggregatorV3Interface.sol";

contract PriceConsumerV3 {

    AggregatorV3Interface internal priceFeed;

 /**
 * Network: Kovan
 * Aggregator: ETH/USD
 * Address: 0x9326BFA02ADD2366b30bacB125260Af641031331
     */

 constructor() public {
 priceFeed = AggregatorV3Interface(0x9326BFA02ADD2366b30bacB125260Af641031331);
 }

 /**
 * Returns the latest price
     */

 function getThePrice() public view returns (int) {
 (
 uint80 roundID,
 int price,
 uint startedAt,
 uint timeStamp,
 uint80 answeredInRound
 ) = priceFeed.latestRoundData();
 return price;
 }
}
```

上面的代码是实现访问 Chainlink price oracles 所需的全部内容，您可以阅读 [文档](https://docs.chain.link/docs/get-the-latest-price/) 开始在您的应用程序中实现它们。如果您是智能合约或 oracle 的新手，我们有一个 [初学者演练](https://docs.chain.link/docs/beginners-tutorial/) 来帮助您入门，并保护您的协议及其用户免受 flash loan 和 Oracle 操纵攻击。

如果你想了解更多，并看到所有这些在行动中，玩 [OpenZeppelin 的 DEX Ethernaut 级别，](https://ethernaut.openzeppelin.com/level/0x0b0276F85EF92432fBd6529E169D9dE4aD337b1F) 这表明操纵 DEX 的现货价格是多么容易。

## 3.不要使用 Keccak256 或 Blockhash 作为随机性的来源

使用**` block . difference`**，**` block . timestamp `**， **`blockhash`** ， 或任何与块相关的东西将一个随机数放入您的应用程序，会使您的代码被利用。智能合约中的随机性可以用于许多用例，例如无偏见地确定奖品赠品的获胜者，或者 [公平地向用户分发稀有的 NFT](https://forum.openzeppelin.com/t/understanding-the-meebits-exploit/8281/3?u=patrickalphac)。然而，区块链是确定性系统，并且不提供随机数的防篡改源，因此试图在不查看区块链之外的情况下获取随机数将总是存在问题，并且可能导致漏洞。RNG 漏洞不像 oracle 操纵攻击或重入攻击那样普遍，但它们在 Solidity 教育材料中以惊人的频率出现。很多教育内容教区块链开发者用这样的代码得到一个随机数:

```
uint randomNumber = uint(keccak256(abi.encodePacked(nonce, msg.sender, block.difficulty, block.timestamp))) % totalSize;
```

这里的想法是使用随机数、阻塞难度和时间戳的某种组合来创建一个“随机”数。然而，这有一些明显的缺点。

1.  实际上，你可以继续“重新滚动”已取消的交易，直到你得到一个你喜欢的随机数。这对任何人来说都很容易做到。
2.  使用 block . difference(或者链上的任何东西)这样的散列对象作为 RNG，可以让矿工对数字产生巨大的影响。与“重新滚动”策略类似，如果结果对矿工不利，矿工可以使用他们的能力来对交易进行排序，以将某些交易从区块中排除。矿工也可以选择保留对他们不利的块哈希，如果这是随机使用的链上数据的来源。
3.  使用 block.timestamp 这样的东西提供了零随机性，因为时间戳是任何人都可以预测的。

以这种方式使用链上随机数发生器给予用户和/或矿工对“随机”数的影响和控制。如果你希望有一个公平的系统，以这种方式使用随机性将非常有利于恶意的行为者。随着被随机性函数保护的价值数量的增加，随着利用它的动机的增加，这个问题只会变得更糟。

### **解:** 用链环 VRF 作为可验证随机性的神谕

为了防止被利用，开发人员需要一种方法来创建可验证的随机性，并防止矿工和重新滚动用户篡改。我们需要的是从先知那里获得的随机信息。然而，许多提供来源随机性能力的神谕没有办法实际证明他们交付的数字确实是随机生成的(操纵的随机性只是看起来像正常的随机性，你无法区分)。开发人员需要能够从链外获得随机性，同时也有一种方法来明确地和加密地证明随机性没有被操纵。

[【VRF】](https://docs.chain.link/docs/get-a-random-number/)【链环可验证随机函数】恰恰做到了这一点。它使用 oracle 节点生成一个链外随机数，以及该数字完整性的加密证明。然后，VRF 协调器在链上检查密码证明，以验证 VRF 的确定性和防篡改的完整性。工作原理是这样的:

1.  用户从链接节点请求随机数并提供种子值。这将发出一个链上事件日志。
2.  离线 Chainlink oracle 读取此日志，并根据节点的 keyhash、用户给定的种子和请求期间未知的块数据，使用可验证随机函数(VRF)创建一个随机数和加密证明。然后，它在第二个事务中将随机数返回到链上，并使用加密证明通过 VRF 协调器契约在链上进行验证。

VRF 链家是如何解决上述问题的？

#### 你不能重投攻击

由于此过程需要两次交易，第二次交易是创建随机数的地方，所以您看不到随机数或取消您的交易。

#### 矿工没有影响力

由于 Chainlink VRF 不使用矿工可以控制的值，如 block . difference 或 block.timestamp 等可预测的值，他们无法控制随机数。

用户、oracle nodes 或 dApp 开发人员无法操纵 VRF 链家提供的随机性数据，这使得它成为智能合约应用程序使用的链上随机性的一个极其安全的来源。

您可以按照 [文档](https://docs.chain.link/docs/get-a-random-number/) 或者按照我们的[Chainlink VRF](https://docs.chain.link/docs/intermediates-tutorial/)初学者指南开始在您的代码中实现 chain link VRF，其中包括一个视频演练。

## 4.避免常见故障

这一点对于可靠性来说是一种总括，但是为了有一个安全的契约，你需要在建立它的时候牢记所有这些 DeFi 安全原则。要写出真正坚实可靠的文章，你必须知道它是如何工作的。否则，您可能容易受到:

### 溢出/下溢

在 Solidity 中，uint256 和 int256 是“包装”的。这意味着，如果您在 uint256 中有一个最大 uint256 大小的数字，然后添加到它，它将“包装”到它可能是最小的数字。一定要检查这个。在 0.8 之前的 Solidity 版本中，您会希望使用类似于 [安全数学](https://docs.openzeppelin.com/contracts/2.x/api/math#SafeMath) 的东西。

在 Solidity 0.8.x 中，默认检查算术运算。这意味着 x + y 会在溢出时抛出异常。所以一定要知道你用的是什么版本！

### 回路气体极限

当编写动态大小的循环时，你需要非常小心它们能有多大。一个循环很容易超过最大块大小，当它恢复时，会使你的契约无效。

### 避免使用 tx.origin

`tx.origin '不应用于智能合约中的授权，因为它可能导致 [类似网络钓鱼的攻击](https://blog.sigmaprime.io/solidity-security.html#tx-origin-vuln) 。

### 代理存储冲突

对于代理实现模式的项目，可以通过改变代理合同中实现合同的地址来更新实现。

通常，在代理合同中有一个特定的变量存储实现合同地址。如果这个变量的存储位置是固定的，而恰好有另一个变量与实现契约中的存储位置具有相同的索引/偏移量，那么就会出现存储冲突。

```
pragma solidity 0.8.1;

contract Implementation {
  address public myAddress;
    uint public myUint;

    function setAddress(address _address) public {
        myAddress = _address;
    }
}

contract Proxy {
  address public otherContractAddress;

    constructor(address _otherContract) {
        otherContractAddress = _otherContract;
    }

    function setOtherAddress(address _otherContract) public {
        otherContractAddress = _otherContract;
    }

    fallback() external {
  address _impl = otherContractAddress;
        assembly {
          let ptr := mload(0x40)
          calldatacopy(ptr, 0, calldatasize())
          let result := delegatecall(gas(), _impl, ptr, calldatasize(), 0, 0)
          let size := returndatasize()
          returndatacopy(ptr, 0, size)

          switch result
          case 0 { revert(ptr, size) }
  default { return(ptr, size) }
        }
    }
}
```

要触发存储冲突，您可以在 Remix 中执行以下步骤:

1.  部署实施合同；
2.  部署代理契约，将实现契约的部署地址作为其构造函数参数；
3.  在代理合同的部署地址上运行实现合同；
4.  调用 myAddress()函数。它将返回一个非零地址，该地址是存储在代理契约中的 otherContractAddress 变量中的部署地址。

那么，以上四个步骤发生了什么？

1.  部署实施合同并生成其部署地址；
2.  用实现契约的部署地址部署代理契约，其中调用代理契约的构造函数，用实现契约的部署地址赋给 otherContractAddress 变量；
3.  In step 3, the implementation contract interacts with the proxy storage, i.e., the variable that in the deployed implementation contract can read the value of the corresponding hash-collided variable in the deployed proxy contract.

    |  | 实施合同 | 代理合同 |
    | 存储槽 0 | 公开我的地址 | address public other contract address |
    | 存储插槽 1 | uint public myUint |  |
    | 存储插槽 2 |  |  |
    | … |  |  |

    *myAddress 可以通过碰撞读取 otherContractAddress 的值*

4.  myAddress()函数的返回值正好是部署的实现契约中 myAddress 变量的值，与部署的代理契约中的 othercontractdaddress 变量发生冲突，可以在那里得到 othercontractdaddress 变量的值。

为了避免代理存储冲突，我们建议开发人员通过为存储变量选择伪随机槽来实现非结构化存储代理。

一种常见的做法是为项目采用可靠的代理模式。最广泛采用的代理模式有 [通用可升级代理标准](https://eips.ethereum.org/EIPS/eip-1822) (UUPS)和 [透明代理模式](https://blog.openzeppelin.com/the-transparent-proxy-pattern/) 。它们都提供了具体的存储“偏移”,以避免在代理契约和实现契约中使用相同的存储槽。

下面是一个使用透明代理模式实现随机存储的例子。

```
bytes32 private constant implementationPosition = bytes32(uint256(
  keccak256('eip1967.proxy.implementation')) - 1
));
```

### 令牌转移计算准确性

正常情况下，对于一个普通的 ERC20 token，收到的 token 金额应该等于调用函数 with 的原始金额；例如，请参见下面的函数“retrieveTokens()”。

```
function retrieveTokens(address sender, uint256 amount) public {
token.transferFrom(sender, address(this), amount);
    totalTokenTransferred += amount;
}
```

然而，如果代币是通货紧缩的，即每次转账都要收费，那么实际收到的代币金额将少于最初请求转账的代币金额。

在下面显示的修改后的函数 retrieveTokens(地址发送者，uint256 金额)中，根据转账操作前后的余额重新计算“金额”。这将准确地计算已传送到“地址(This)”的令牌量，而不管令牌传送机制如何。

```
function retrieveTokens(address sender, uint256 amount) public {
uint256 balanceBefore = deflationaryToken.balanceOf(address(this));
deflationaryToken.transferFrom(sender, address(this), amount);
uint256 balanceAfter = deflationaryToken.balanceOf(address(this));
amount = balanceAfter.sub(balanceBefore);
    totalTokenTransferred += amount;
}
```

### 正确的数据删除

有许多场景需要删除合同不再需要的某个对象或值。在像 Java 这样的 stature 语言中，有一种垃圾收集机制可以自动安全地处理这个问题。然而，在 Solidity 中，开发者必须手动处理 **【垃圾】** 。因此，不正确地处理垃圾可能会给智能合约带来安全问题。

例如，当使用 delete 从数组中删除单个成员时，即“删除数组[成员]”,则 **【数组[成员]`** 仍然存在，但会根据 **`数组[成员]`** 的类型重置为默认值。开发人员应该记住要么跳过这个成员，要么重组数组并减少其长度。比如:

```
array[member] = array[array.length - 1];
array.pop()
```

这些只是需要注意的一些漏洞，但是深入理解可靠性将有助于你避免这些“陷阱”可以查看审计员 [【适马总理】关于常见可靠性漏洞](https://blog.sigmaprime.io/solidity-security.html) 的文章。

## 5.功能可见性和限制

在 Solidity 语言的设计中，有四种类型的函数可见性:

*   私有:该功能仅在当前合同中可见；
*   内部:该功能在当前合同和派生合同中可见；
*   外部:该功能仅对外部调用可见；
*   public:函数对内部和外部调用都可见。

功能可见性是指特定功能的上述四种可见性之一，用于限制某一组用户的访问。至于限制，它指的是专门为限制访问而编写的自定义代码片段。

可见性和限制可以结合起来，为特定的功能设置适当的访问权限。例如，在 ERC20 实现的函数` _mint()'中:

```
function _mint(address account, uint256 amount) internal virtual {
require(account != address(0), "ERC20: mint to the zero address");
    _beforeTokenTransfer(address(0), account, amount);
    _totalSupply += amount;
    _balances[account] += amount;
    emit Transfer(address(0), account, amount);
    _afterTokenTransfer(address(0), account, amount);
}
```

函数` _mint()`的可见性被设置为 internal，这正确地保护了它不被外部调用。为了为 mint 功能设置适当的访问授权，可以使用下面的代码片段:

```
function mint(address account, uint256 amount) public onlyOwner {
    _mint(account, amount);
 require(MaxTotalSupply >= _totalSupply, "over mint");
}
```

函数' mint()'只允许合同的所有者铸造，而' require()'语句防止所有者铸造太多的代币。

正确使用可见性和约束有利于合同管理。也就是说，一方面，缺乏这样的设置可能会允许恶意攻击者调用管理配置函数来操纵项目，另一方面，过度限制性的设置可能会给合同带来集中化问题，这可能会引起您的社区的怀疑。

## 6.在部署到 Mainnet 之前，一定要进行外部审计

把对你的代码的审核想象成一个关注安全性的同行评审。审计员将逐行检查您的整个代码库，并使用正式的验证技术来检查您的智能合同中的任何漏洞。在没有审计的情况下部署代码，或者在审计后更改代码并重新部署，是一种容易暴露潜在漏洞的方法。

有许多方法可以帮助你和你的审计员确保你的审计尽可能全面:

1.  记录一切，这样他们就可以更轻松地跟踪正在发生的事情
2.  保持与他们的沟通渠道畅通，以防他们有问题
3.  在你的代码中加入注释，让你的团队和他们的团队更容易理解

然而，不要依赖审计员来捕捉一切。你应该首先有一个安全的心态，因为，在一天结束的时候，如果你的协议被黑了，你仍然是一个团队。安全审计不一定能解决所有问题，但它们确实提供了一轮额外的审查，有助于捕捉您尚未发现的 bug。

Tincho 有一个 [很棒的 tweet 线程](https://twitter.com/tinchoabbate/status/1400170232904400897) 关于如何最好地与审计员合作。

如果您正在寻找审计师推荐，请随时联系我们的技术专家[](http://security@chain.link)。

## 7.进行测试并使用静态分析工具

你需要对你的应用程序进行测试。人类是伟大的，但是他们永远不会给你自动化测试套件所提供的代码覆盖率。如果您正在寻找一个起点，那么[chain link starter kit repos](https://github.com/smartcontractkit)有一些示例测试套件供您查看。像 [Aave](https://github.com/aave/protocol-v2) 和[Synthetix](https://github.com/Synthetixio/synthetix)这样的协议也有很棒的测试套件，查看它们的代码来了解一些测试(以及更一般的编码)的最佳实践可能是个好主意。

静态分析工具也会帮助你更早地发现 bug。它们被设计成自动检查你的合同并寻找潜在的漏洞。目前最流行的静态分析工具是[](https://github.com/crytic/slither)。CertiK 目前还在基于其在审计、验证和监控智能合同方面的丰富经验构建下一代静态分析、语法分析、漏洞分析和形式验证工具。

## 8.将安全性视为整个生命周期的努力

毫无疑问，您应该在生产部署前尽最大努力创建安全可靠的智能合同，但区块链和 DeFi 协议的快速发展以及新攻击的不断发明意味着您不能止步于此。相反，您应该获取并跟踪最新的监控和警报情报，如果可能的话，尝试在智能合同本身中引入面向未来的功能，以访问数量快速增长的动态安全情报并从中受益。

[![A clickable banner to a report detailing the Ultimate Guide to Blockchain Oracle Security](img/9ede9173a1fba83a6a8ec756c6b9e3a8.png)](https://chain.link/resources/blockchain-oracle-security)

<figcaption id="caption-attachment-3518" class="wp-caption-text">This guide gives a comprehensive breakdown on how to evaluate blockchain oracle security.</figcaption>



也有可能带来一些额外的帮助。 [CertiK 天网](https://www.certik.org/technology#skynet) 作为 24/7 安全智能引擎，为智能合约上线部署提供多维度、实时透明的安全监控。它包括社会情绪、治理、市场波动、安全评估等，为区块链客户、社区和代币投资者提供一般的安全理解。 [CertiK 安全排行榜](https://www.certik.org/) 提供透明、易于理解的安全见解和最新的项目状态，提供激励改进的社区问责制。

## 9.制定灾难恢复计划

根据你的协议，最好有一个应急计划以防你被黑。一些流行的方法有:

*   投保
*   安装紧急“暂停”功能
*   有升级计划

保险协议越来越受欢迎，是从灾难中恢复的最分散的方法之一。它们在不影响权力下放的情况下增加了一定程度的财务安全。你应该有保险，即使你也有其他灾难恢复计划。一种解决方案是 CertiK 的[ShentuShield](https://shield.certik.org/)，这是一种增加了去中心化和透明度的保险产品。

实施紧急“暂停”功能是一种有利有弊的策略。如果发现漏洞，此功能会停止与您的智能合约的所有交互。如果您准备好了这个特性，您需要确保您的用户知道谁能够操作它。如果只有一个用户，你就不是在运行一个分散的协议，一个精明的用户可以通过你的代码找到答案。小心你如何实现它，因为你可能最终在一个分散的平台上得到一个集中的协议。

升级计划也有同样的问题。转移到一个没有错误的智能合同是很好的，但是你需要以一种深思熟虑的方式升级你的合同，以便不牺牲去中心化。一些安全公司甚至走到了 [强烈建议 *对抗* 可升级智能合约模式](https://blog.trailofbits.com/2018/09/05/contract-upgrade-anti-patterns/) 。您可以在智能合约升级地址 的 [状态或在](https://blog.openzeppelin.com/the-state-of-smart-contract-upgrades) [Patrick Collins 的 YouTube 视频](https://www.youtube.com/watch?v=bdXJmWajZRY) 主题中了解更多关于升级您的智能合约的信息。

[链环不和谐](https://discord.gg/2YHSAey) 如果你正在寻找一些保险建议，请随时垂询。

## 10.防止抢跑

在区块链，所有交易在 [mempool](https://academy.binance.com/en/glossary/mempool) 中可见，这意味着每个人都有机会看到你的交易，并有可能在你的交易通过之前进行交易，以便从你的交易中获利。

举个例子，假设你用一只 DEX 以当前市场价格换了 5 只 ETH 给戴。一旦您将交易发送到 mempool 进行处理，领先者可能会在您之前进行大量购买 ETH 的交易，从而导致价格上涨。然后，他们可以以更高的价格向你出售他们购买的 ETH，并以你为代价获利。[front running bot 目前在区块链世界横行](https://www.coindesk.com/miners-front-running-service-theft) ，以牺牲一般用户为代价获利。这个术语来自于传统的金融世界 ，交易者试图做完全相同的概念，但是使用股票、商品、衍生品和其他金融资产和工具。

作为另一个例子，下面列出的函数具有被抢先运行的高风险。根据修饰符 **`初始化器`** ，该函数只能被调用一次。如果调用 **`initialize()`** 函数的事务在 mempool 中被攻击者监听到，那么攻击者就可以 **`replicate`** 使用一组定制的 token、distributor 和 factory 值的事务，并最终控制整个契约。由于函数**` initialize()`**只能被调用一次，合同所有者没有办法防御或减轻这种攻击。

```
function initialize(IERC20 _token, IDistributor _distributor, IFactory _factory) public initializer {
    Ownable.initialize();
token = _token;
distributor = _distributor;
factory = _factory;
}
```

这往往也与所谓的 [矿工可提取值，或 MEV](https://blog.chain.link/what-is-miner-extractable-value-mev/) 有关。MEV 是指矿工或机器人对交易进行重新排序，以便以某种方式从排序中获利。就像领先者支付更多的汽油来让他们的交易排在你的前面一样，一个矿商可以重新安排交易，让他们的交易排在你的前面。在整个区块链生态系统中，MEV 每天从普通用户那里窃取数百万美元。

幸运的是，包括 Chainlink Labs 首席科学家 Ari Juels 在内的一群世界级智能合约和密码研究人员正致力于用一种叫做“公平测序服务”的解决方案来解决这个问题

### **开发中的解决方案:**【chain link Fair 测序服务(FSS)

[Chainlink 2.0 白皮书](https://chain.link/whitepaper) 概述了公平排序服务的关键特性，这是一种由 chain link 分散式 Oracle Networks (DONs)支持的安全链外服务，将用于根据 dApp 概述的公平临时概念(如 mempool 中首次出现的概念)对交易进行排序。FSS 旨在大大减轻前置运行和 MEV 的影响，并降低整个区块链生态系统用户的费用。你可以在这篇介绍性的博客文章 中了解更多关于 FSS 的信息，并在 [Chainlink 2.0 白皮书](https://research.chain.link/whitepaper-v2.pdf) 的第五节中了解更多信息。

除了 FSS，减轻抢先运行问题的最好方法之一是尽可能降低事务排序的重要性，从而抑制协议中的事务重新排序和 MEV。

## 总结和后续步骤

在保护您的智能合同时，有许多重要的 DeFi 安全考虑因素，我们已经看到了太多的漏洞利用和攻击，让用户损失了数千万美元。掌握以上技巧将有助于您在构建智能合约时避免这些漏洞。然而，永远不会有一个涵盖每个独特漏洞的详尽列表。我们继续看到围绕集中机制的新的和复杂的经济利用形式，以及围绕脆弱抵押品的快速贷款资助的市场操纵。对于 DeFi 社区来说，共同努力来发现和缓解整个生态系统中这些新出现的风险至关重要。

通过参考来自 [CertiK Security 排行榜](https://leaderboard.certik.io/) 等地的顶级项目，学习围绕安全智能合约开发的最佳实践，是提高项目安全性的有益方法。智能合同世界是开放和协作的，开发人员希望尽最大努力互相帮助。

你可能会在 [中找到价值，回顾一些以前的利用](https://www.rekt.news/leaderboard/) 作为了解过去攻击是如何进行的手段。您还可以通过全天候安全情报服务(如[CertiK Skynet](https://www.certik.org/technology#skynet))实时接收最新的链上安全漏洞更新并从中学习。

对于那些想要深入安全和游戏化整个过程的人，一定要看看 [以太游戏](https://ethernaut.openzeppelin.com/level/0x4E73b858fD5D7A5fc1c3455061dE52a53F35d966) 。它包含了 DeFi 安全示例，教你许多关于可靠性的细节，这是一个快速了解 DeFi 安全的好方法。另一个学习安全的游戏化项目是 [该死的脆弱 DeFi](https://www.damnvulnerabledefi.xyz/) 。您也可以在 [防范闪贷攻击网站](https://preventflashloanattacks.com/) 了解更多关于闪贷攻击的信息。

作为一个社区，让我们从错误中吸取教训，确保智能合约构建安全，并得到尽可能广泛的采用。到 了解更多关于如何实现这里提到的一些解决方案，到 [Chainlink 文档](https://docs.chain.link/) 和 [CertiK 文档](https://www.certik.io/blog) 。