# 用储备链证明验证稳定币抵押品

> 原文：<https://blog.chain.link/verify-stablecoin-collateral-with-chainlink-proof-of-reserve/>

[分散金融(DeFi)](https://chain.link/education/defi) 是关于经济透明度和改变金融交易方式的基本信任哲学。通过 [智能合约](https://chain.link/education/smart-contracts) ，在基础协议层实现了透明和不信任，但随着新奇的新金融工具不断出现在 DeFi 领域，我们的生态系统需要越来越强大的基础设施来保护这些协议和进出协议的数据。这就是 Chainlink 的用武之地，它是一个区块链不可知的、安全的、去中心化的智能合约离线服务层。

一种已经从 Chainlink 的高质量数据馈送中受益的 DeFi 工具是 [stablecoins](https://blog.chain.link/what-are-stablecoins/) ，这是由链外或跨链抵押品支持的数字资产。Stablecoins 为用户提供了以非易失性货币进行交易的能力，同时还提供了基于区块链的智能合约的无许可性质以及持续吸引新用户进行定义的高收益。有了 Chainlink [储备证明](https://chain.link/solutions/proof-of-reserve)，开发者和用户现在可以放心地验证包装代币和稳定币等担保资产是否完全由他们声称的抵押品支持。准备金证明还为抵押贷款、信用违约互换、跨链代币互换等提供了更高水平的可靠性和透明度。

与所有的 [Chainlink 数据馈送](https://chain.link/data-feeds)一样，易于访问是优先考虑的问题，这使得开发人员可以轻松地将预聚合的、可靠的链外数据集成到他们的 dApp 中。在本指南中，我们将介绍如何快速利用 Chainlink Proof of Reserve 来证明稳定币的抵押，特别是 [TrustToken 的 TUSD](https://blog.trusttoken.com/trusttoken-introduces-proof-of-reserve-for-tusd-stablecoin-in-collaboration-with-chainlink-and-584b3674b89f) 。

[Integrate Chainlink Proof of Reserve](https://chain.link/proof-of-reserve)

## 初始化订阅源

任何 Chainlink 数据提要的第一步都是导入聚合器接口，然后用构造函数中的正确地址初始化提要。

```
import "https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/interfaces/AggregatorV3Interface.sol";

contract ProofOfReserve {

    AggregatorV3Interface internal supplyTUSD;
    AggregatorV3Interface internal reservesTUSD;

    /**
     * Aggregator: TUSD reserve and TUSD supply
     * Reserves Address: 0x478f4c42b877c697C4b19E396865D4D533EcB6ea
     * Supply Address: 0x807b029DD462D5d9B9DB45dff90D3414013B969e
     */
    constructor() public {
        supplyTUSD = AggregatorV3Interface(0x807b029DD462D5d9B9DB45dff90D3414013B969e);
        reservesTUSD = AggregatorV3Interface(0x478f4c42b877c697C4b19E396865D4D533EcB6ea);
    }
```

在这种情况下，我们有两个提要，一个显示支持 TUSD 的当前储备，另一个提供 TUSD 的当前供应。我们都需要能够确定储备是否足以满足已经发放的供应。

## 检索值

一旦提要被初始化，我们需要两个函数来从中检索值。

```
   //Returns the latest Supply info
    function getLatestSupply() public view returns (int) {
        (
            uint80 roundID, 
            int answer,
            uint startedAt,
            uint updatedAt,
            uint80 answeredInRound
        ) = supplyTUSD.latestRoundData();
        return answer;
    }

    //Returns the latest Reserves info
    function getLatestReserves() public view returns (int) {
        (
            uint80 roundID, 
            int answer,
            uint startedAt,
            uint updatedAt,
            uint80 answeredInRound
        ) = reservesTUSD.latestRoundData();
        return answer;
    }
```

由于数据已经由 Chainlink 节点的网络聚合并提交到链上，因此我们只需要一个简单的查看函数来访问数据，因此没有汽油成本。还有一些其他字段，如检索数据的聚合轮的 ID 和时间，但在这种情况下，我们只关心答案:供应和储备的值。

## 对照供应检查储备

最后，一旦我们有了这些数据，我们只需要检查储备是否超过了供给，这意味着稳定的硬币是完全抵押的，并且处于健康的状态。

```
//Determines if supply has exceeded reserves
    function isTUSDHealthOK() public view returns (bool) {
        return getLatestReserves() >= getLatestSupply();
    }
```

如果这个函数返回 false，这将意味着供给大于储备，TUSD 没有足够的支持。在这种情况下，您可能希望触发 dApp 中的断路器，调用此功能来关闭任何相关贷款或暂时停止交易，以防止任何连锁市场风险。如果该函数为真，则 TUSD 是健康的，超额抵押，并且您的 dApp 可以继续正常运行。

## 结论

DeFi 和 smart 合约建立在透明和可验证的原则之上。这是设计上的一个巨大转变，与现有系统相比，现有系统往往不够完善和不透明。为了满足 DeFi 在透明度方面的标准，并降低用户和更大市场的风险，协议端到端遵守这些原则至关重要。Chainlink Proof of Reserve 是为任何利用备份或打包资产的平台维护端到端透明性的解决方案，现在在 mainnet 上利用 dApp 比以往任何时候都更容易。

如果你是一名开发人员，并希望将 chain link Proof Reserve 集成到你的智能合同应用程序中，请查阅 [Chainlink 开发人员文档](https://docs.chain.link/docs)或[联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog)。

### 关于这个话题的更多信息

*   [储备证明链:为 DeFi 抵押品带来透明度](https://blog.chain.link/chainlink-proof-of-reserve-bringing-transparency-to-defi-collateral/)
*   什么是 Stablecoins？
*   [链式断路器](https://blog.chain.link/circuit-breakers-and-client-diversity-within-the-chainlink-network/)