# 可靠性中的随机数生成(RNG)

> 原文：<https://blog.chain.link/random-number-generation-solidity/>

*chain link 2021 秋季黑客马拉松于 10 月 22 日拉开帷幕。* [*今天报名。*](https://chain.link/hackathon?utm_medium=referral&utm_source=chainlink-blog&utm_campaign=fall-2021-hackathon&utm_content=random-number-generation-rng-in-solidity)

solidity 中的随机数生成(RNG)必须通过向 oracle 等链外资源发送种子来完成，然后 Oracle 必须将生成的随机数和可验证的证据返回给[智能契约](https://chain.link/education/smart-contracts)。由于区块链的决定论，随机数不可能在实体中自然产生。

随着 Chainlink VRF 现已在众多区块链上线，开发人员可以安全、可靠、可验证地轻松生成随机数。在这篇技术文章中，我们将向你展示如何使用 VRF 链生成一个随机数。

在您的智能合约中生成安全随机数的示例可以在 [Chainlink 文档](https://docs.chain.link/docs/chainlink-vrf)中找到。这里有一个在 Kovan testnet 上的[区块链随机数生成](https://remix.ethereum.org/#version=soljson-v0.6.6+commit.6c089d02.js&optimize=false&evmVersion=null&gist=536123b71478ad4442cfc4278e8de577)的混合例子，供那些现在想测试它的人使用。请记住遵循[请求和接收方法](https://docs.chain.link/docs/architecture-request-model)和[通过 LINK](https://docs.chain.link/docs/fund-your-contract) 为您的智能合同提供资金。

## VRF 链环项目概述

Chainlink VRF(可验证随机函数)是一个为智能合同设计的可证明公平和可验证的随机性来源。Solidity 开发人员可以将其用作防篡改随机数生成器，为依赖不可预测结果的以太坊应用程序构建安全可靠的智能合约。

使用 VRF 链生成随机数的第一步是确定一个[种子](https://en.wikipedia.org/wiki/Random_seed)。选择一颗[难以影响或预测](https://docs.chain.link/docs/chainlink-vrf-api-reference#choosing-a-seed)的种子极其重要。如果有人可以影响或预测种子，理论上他们可以尝试与执行随机性请求的[先知](https://chain.link/education/blockchain-oracles)勾结，给自己一个有利的结果。因此，建议不要使用来自区块链状态的值，如块高度或块时间戳。

然后，该种子在请求中被发送到链接 oracle。然后，oracle 使用给定的种子生成一个伪随机数，并将结果返回给 smart contract，同时返回使用种子生成随机数的加密证明。这种加密证明是通过[公钥加密](https://en.wikipedia.org/wiki/Public-key_cryptography)创建的，这是一种被广泛接受的区块链技术特性。结果可以被验证是很重要的，因为像矿工或先知这样的参与者可以为了他们自己的利益而试图影响一个随机数的结果。

这是一个高层次的概述如何链接 VRF 工程。底层技术实现的更多细节可以在我们对 Chainlink VRF 的[介绍中找到。然而，作为一名开发人员，除了获取种子然后创建对 Chainlink oracle 的请求之外，您不需要担心任何事情。](https://blog.chain.link/chainlink-vrf-on-chain-verifiable-randomness/)

## 创建消费者契约

为了在您的 Solidity 智能契约中获得一个随机数，我们应该首先从 chain link[VRFConsumerBase](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/VRFConsumerBase.sol)契约中继承。我们的契约还应该包含随机数结果的变量、用于生成随机性的公钥散列，以及为完成请求而支付给 oracle 的费用。

```
import "https://raw.githubusercontent.com/smartcontractkit/chainlink/master/evm-contracts/src/v0.6/VRFConsumerBase.sol";

contract RandomNumberConsumer is VRFConsumerBase {
    bytes32 internal keyHash;
    uint256 internal fee;
    uint256 public randomResult;
}
```

接下来，在构造函数中，我们应该初始化链接 VRF 协调器。为此，我们调用 VRFConsumerBase 函数，为给定环境传入 VRF 协调器的地址和 Chainlink 令牌的地址。我们还需要设置 keyHash 变量，它是生成随机性的公钥。这些环境的具体值可在链节 VRF 文档的[合同地址](https://docs.chain.link/docs/vrf-contracts)部分获得。最后，我们需要设置链接令牌支付金额。对于 Kovan 测试环境，它是 0.1 LINK。

```
constructor() 
    VRFConsumerBase(
        0xdD3782915140c8f3b190B5D67eAc6dc5760C46E9, // VRF Coordinator
        0xa36085F69e2889c224210F603D836748e7dC0088  // LINK Token
    ) public
{
    keyHash = 0x6c3699283bda56ad74f6b855546325b68d482e983852a7a82979cc4807b641f4;
    fee = 0.1 * 10 ** 18; // 0.1 LINK
}
```

接下来，我们在契约中覆盖两个函数“getRandomNumber”和“fulfillRandomness”。“getRandomNumber”函数应该将种子作为输入参数，并且应该简单地调用 VRFConsumerBase“request randomness”函数，传入 keyHash、费用金额和给定的种子。

```
/** 
  * Requests randomness from a user-provided seed
  */
function getRandomNumber(uint256 userProvidedSeed) public returns (bytes32 requestId) {
    require(LINK.balanceOf(address(this)) > fee, "Not enough LINK - fill contract with faucet");
    return requestRandomness(keyHash, fee, userProvidedSeed);
}
```

在执行时，该函数将请求发送给给定的 VRF 协调器契约，该契约然后构建最终种子，并将其发送给该 VRF 协调器的 Chainlink oracle。最终种子由以下值的散列构成:

*   用户提供种子
*   完成请求的链接 oracle 的公钥散列
*   用户在请求时的随机数
*   提出请求的合同的地址
*   当前块号

使用这些额外值的原因是为了防止契约多次使用相同的种子获得相同的结果。nonce 有助于防止契约在同一个块中执行多个请求，因此从理论上讲，契约可以在同一个块中对每个请求使用相同的种子来执行多个请求，并且它们仍然会为每个请求返回唯一的可验证随机数。

“fulfillRandomness”函数应该只接受作为无符号整数的随机数响应，以及请求的 ID，然后在契约中存储给定的随机数。当 VRFCoordinator 协定接收并验证一个随机数时，它将调用此函数。关于这两种功能的更多信息，可在 [Chainlink VRF 文档中找到。](https://docs.chain.link/docs/chainlink-vrf-api-reference)

```
/**
  * Callback function used by VRF Coordinator
  */
function fulfillRandomness(bytes32 requestId, uint256 randomness) internal override {
    randomResult = randomness;
}
```

我们现在在 Solidity 中有了一个完整的随机数生成(RNG)的工作示例，现在可以部署和测试契约了。

## 测试随机数生成消费者契约

上面的[完整合同](https://remix.ethereum.org/#version=soljson-v0.6.6+commit.6c089d02.js&optimize=false&evmVersion=null&gist=536123b71478ad4442cfc4278e8de577)可以很容易地在 Kovan 网络上的 Remix 中打开、编译和部署。一旦部署完毕，一定要通过一些链接[为合同](https://docs.chain.link/docs/fund-your-contract)提供资金。

一旦合同获得了至少 0.1 个链接的资金，我们就可以调用“getRandomNumber”函数，传入一个数字作为种子。这将把请求和种子一起发送到在 Chainlink oracle 上运行的 VRF 协调器。



![Random Number Solidity ](img/a49fd70d02ae528515671e4c0fae725d.png)

<figcaption id="caption-attachment-605" class="wp-caption-text">随机数实度</figcaption>





处理完该事务后，我们等待几秒钟，让 Chainlink oracle 完成对随机数的请求，然后调用我们之前创建的“fulfillnommandations”函数将随机数返回给我们的消费者契约。

然后，我们可以调用“randomResult”getter 函数来查看 Chainlink oracle 使用给定种子生成的可验证随机数的结果。我们现在有了一个可验证的随机数，可以在我们的消费者契约和任何其他使用它的应用程序中使用。



![Random Result Solidity (Remix)](img/b35caa48e7a61f6c95f2d0357ce88d4a.png)

<figcaption id="caption-attachment-606" class="wp-caption-text">【随机结果实度(混音)</figcaption>





## 验证随机性

现在我们有一个随机数返回到我们的契约，您可能想知道我们如何确定它是用执行请求的 Chainlink oracle 的给定种子和公钥散列生成的。使用 Chainlink VRF 的答案是，你不需要。验证作为满足请求的 [VRFCoordinator](https://github.com/smartcontractkit/chainlink/blob/develop/evm-contracts/src/v0.6/VRFCoordinator.sol) 契约的一部分自动发生。

如果验证失败，则随机数不会返回给消费契约，并且事务被恢复。因此，使用 Chainlink VRF 的区块链开发者可以确信，他们通过 Chainlink VRF 获得的随机数是可验证的随机。验证的基本技术细节可以在我们的 VRF 链节的[技术演练中找到。](https://blog.chain.link/verifiable-random-functions-vrf-random-number-generation-rng-feature/#technical-walkthrough)

## 摘要

Chainlink VRF 允许 Solidity 开发者在他们的智能合约中以一种安全、可靠且经过验证的方式快速、轻松地生成随机数。

如果你是一个聪明的合同开发者，想要利用 Chainlink VRF 特性，请访问 [Chainlink 开发者文档](https://docs.chain.link/docs/chainlink-vrf)并加入关于[不和谐](https://discordapp.com/invite/aSK4zew)的技术讨论。您可以通过访问 [Chainlink 网站](https://chain.link/)并在 [Twitter](https://twitter.com/chainlink) 和 [Reddit](https://www.reddit.com/r/Chainlink/) 上关注 Chainlink 来了解更多关于 Chainlink 的信息。

*[chain link 2021 秋季黑客马拉松](https://chain.link/hackathon) 于 2021 年 10 月 22 日开赛。无论您是开发人员、创作人员、艺术家、区块链专家，还是该领域的新手，这个黑客马拉松都是启动您的智能合同开发之旅并向行业领先的导师学习的最佳场所。立即锁定您的席位，争夺超过$ 300，000 的奖金。T9】*

[Sign up today](https://chain.link/hackathon?utm_medium=referral&utm_source=chainlink-blog&utm_campaign=fall-2021-hackathon&utm_content=random-number-generation-rng-in-solidity)