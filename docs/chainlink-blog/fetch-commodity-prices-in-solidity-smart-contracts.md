# 获取 Solidity 智能合约中的商品价格

> 原文：<https://blog.chain.link/fetch-commodity-prices-in-solidity-smart-contracts/>

安全、最新的价格数据是许多金融应用的核心，通常用于触发交易和衍生其他工具和产品，尤其是在分散金融(DeFi)协议中。[基于商品价格数据的合成代币](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/#synthetics)在创建分散期权、期货和其他复杂衍生品的 DeFi 空间中具有重要意义。除了获取[安全的加密货币价格数据](https://blog.chain.link/fetch-current-crypto-price-data-solidity/)，Chainlink 数据馈送还可用于在您的智能合约中获取高质量的商品价格数据，以便您可以推出这些更复杂的金融产品。

在本技术教程中，我们将介绍如何在 Solidity 智能合约中使用 Chainlink 商品数据馈送。首先，让我们快速回顾一下什么是商品提要，以及使用它们可以创建什么类型的衍生品。

## 什么是商品数据馈送？

商品交易市场是黄金和石油等原材料交易的全球市场。由于这一市场的高容量和受欢迎程度，许多 DeFi 应用程序使用 Chainlink 商品数据馈送来确保商品价格数据以安全和分散的方式传递给其衍生品合约，而没有任何单点故障。

例如， [Synthetix Exchange](https://synthetix.exchange/) ，一家领先的 DeFi 衍生产品交易所，使用 Chainlink oracles 提供的几种商品价格反馈，以确保根据其基础资产的真实市场价格进行防篡改和准确的估值，即使在波动性很高的时候也是如此。

![Synthetix Exchange synths powered by the Chainlink Network.](img/b6339de3b67faa07c14d65963aaefc9f.png)

<figcaption id="caption-attachment-1627" class="wp-caption-text">How Synthetix Exchange uses Chainlink oracles to obtain real-time market data of various commodities.</figcaption>



## 如何使用 Chainlink 商品数据馈送

[Chainlink 数据馈送](https://data.chain.link/)使用数百个高质量的数据源，并通过一个分散的 Chainlink oracles 网络将它们聚合起来，这些 oracles 将价格数据馈送到参考合同中，结果在聚合器智能合同中再次聚合，作为最新的可信答案。通过在分散的节点网络中使用众多数据源和[多级聚合](https://blog.chain.link/levels-of-data-aggregation-in-chainlink-price-feeds/)，Chainlink oracles 确保价格数据具有最高质量并反映广泛的市场覆盖面，保护数据免受突然的数量变化和[价格 oracle 攻击](https://blog.chain.link/flash-loans-and-the-importance-of-tamper-proof-oracles/)。

### 创建智能合同

要开始在您的智能合约中使用 Chainlink 商品数据馈送，首先[让 testnet ETH](https://app.mycrypto.com/faucet) 在您的智能合约中用作 gas。一旦您有了一些 ETH，开始构建使用 Chainlink 商品数据馈送的智能契约的最简单方法是部署[价格消费者契约](https://remix.ethereum.org/#version=soljson-v0.6.7+commit.b8d736ae.js&optimize=false&evmVersion=null&gist=0c5928a00094810d2ba01fd8d1083581)。这是一个基本的模板合同，用于启动链接数据馈送请求。首先，我们需要导入[聚合器 v3 接口](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/interfaces/AggregatorV3Interface.sol)契约接口，它允许我们的智能契约引用 Kovan testnet 上的链上数据。然后在局部变量中创建它的一个实例。

**注意:**本教程是重新编写的，但确实提到了 Node.js 语法，例如在下面的 import 语句中:

```
import "https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/interfaces/AggregatorV3Interface.sol";
```

```
AggregatorV3Interface internal priceFeed;
```

在[价格提要引用契约](https://docs.chain.link/docs/ethereum-addresses)的构造函数中，我们可以初始化我们感兴趣的价格提要的地址。通过探索 Chainlink 文档中的[以太坊价格馈送页面](https://docs.chain.link/docs/ethereum-addresses)，我们可以找到 Chainlink 当前提供的所有价格馈送合同地址。导航到页面的 Kovan 部分并选择商品价格提要。出于本例的目的，我们将选择[XAU/美元](https://data.chain.link/xau-usd)价格提要，费城黄金和白银指数，其地址为[0x c 8 FB 5684 f 2707 c 82 f 28595 deac 017 bfdf 44 ee 9 c 5](https://kovan.etherscan.io/address/0xc8fb5684f2707C82f28595dEaC017Bfdf44EE9c5)。

```
priceFeed = AggregatorV3Interface(0xc8fb5684f2707C82f28595dEaC017Bfdf44EE9c5);
```

定义了一个名为 getLatestPrice 的函数，用于从价格提要聚合器契约中获取最新价格，该契约在上面的构造函数中进行了实例化。为此，定义了一个新函数，它从聚合器契约中调用 [latestRoundData](https://docs.chain.link/docs/price-feeds-api-reference#latestrounddata) 函数。这个函数返回聚合器契约的当前状态，在本例中，我们获取当前价格并将其返回到消费函数中。

```
function getLatestPrice() public view returns (int) {
    (
        uint80 roundID, 
        int price,
        uint startedAt,
        uint timeStamp,
        uint80 answeredInRound
    ) = priceFeed.latestRoundData();
    return price;
}
```

### 部署和测试智能合约

现在我们已经准备好部署和测试我们的契约了。在 Remix 中编译合同，然后在 deployment 选项卡上，将环境更改为“Injected Web3”，并确保下面的 wallet 地址是您的 MetaMask wallet 中包含一些之前获得的 ETH 的地址，按 deploy 按钮，然后按照步骤操作。最终结果是您将智能合约部署到了 Kovan testnet。您应该通过 Remix 控制台中的事务输出注意到部署的契约地址。

部署完成后，我们只需执行“getLatestPrice”函数。结果应该是该函数从 XAU/美元集合合约返回最新价格，然后可以在我们的[智能合约](https://chain.link/education/smart-contracts)中使用。请注意，我们不需要为该请求发送任何链接，我们甚至也没有使用任何 ETH，因为该事务是对链上 XAU-美元聚合器合同中的数据的纯读取。

![XAU/USD Price Feed result](img/377638b0798243e1d790dd2a2fdab515.png)

<figcaption id="caption-attachment-1628" class="wp-caption-text">XAU/USD Price Feed result</figcaption>



## 摘要

Chainlink 数据馈送为将高质量的商品价格数据纳入 Solidity smart 合约提供了一种超可靠的机制，因此您可以围绕现实世界的资产数据构建新的 [DeFi](https://chain.link/education/defi) 衍生品。此外，Chainlink 的 oracle 框架提供了快速轻松地获取股票、加密货币、稳定货币、指数和许多其他资产类型的安全数据的灵活性，为智能合约开发商提供了强大的数据基础设施，以推动下一波 DeFi 创新。

如果你是一名开发人员，并且想要快速将你的应用程序连接到 Chainlink 数据馈送，请访问[开发人员文档](https://docs.chain.link/)，并参加 [Discord](https://discordapp.com/invite/aSK4zew) 中的技术讨论。

### 关于这个话题的更多信息

*   [如何获取以太坊、比特币和其他加密货币的当前价格](https://blog.chain.link/fetch-current-crypto-price-data-solidity/)
*   [获取 Solidity 智能合约中的外汇汇率](https://blog.chain.link/fetch-foreign-exchange-rates-in-solidity-smart-contracts/)
*   [智能合同开发者使用 Chainlink 的主要方式](https://blog.chain.link/smart-contract-api-price-random/)