# 如何构建和部署雪崩智能合同

> 原文：<https://blog.chain.link/how-to-build-and-deploy-an-avalanche-smart-contract/>

在本技术教程中，我们将介绍如何构建智能合同并将其部署到 Avalanche 合同链(C-Chain ),以及如何利用 [Chainlink 数据馈送](https://chain.link/solutions/defi)在 Avalanche 上创建使用链外市场数据的混合智能合同。

随着 [Chainlink Price Feeds 现已在 Avalanche mainnet](https://medium.com/avalancheavax/chainlink-price-feeds-are-live-on-avalanche-mainnet-paving-wave-for-advanced-defi-apps-6c4f0dfac565) 上上线，开发人员能够轻松利用 Chainlink Network 久经考验的可靠价格数据，以 Avalanche 平台的全原生速度和低成本运行。Chainlink 价格馈送通过一个由 Chainlink 节点运营商组成的分散网络，将来自多个流动性来源和预汇总的数据结合起来，以得出一个覆盖整个市场的高度准确的单一价格。

获取这些数据对新连锁店的发展至关重要，因为没有价格或其他外部数据，许多 dApps 根本无法生存。雪崩是区块链生态系统在 Chainlink feeds 部署后爆炸式增长的最新例子，随着[【TVL】](https://defillama.com/chain/Avalanche)交易和地址的增加，自从 Chainlink 集成以来，越来越多的开发人员希望了解如何构建和部署雪崩智能合同。

![Avalanche TVL Growth](img/b78c93c8d5372dcdb7920b4b0207602c.png)

<figcaption id="caption-attachment-3003" class="wp-caption-text">The explosive growth of Avalanche’s TVL following its integration of Chainlink.</figcaption>



chain link Price Feeds 的整合和最近推出的[Avalanche Rush](https://medium.com/avalancheavax/avalanche-foundation-announces-180m-defi-incentive-program-d320fdfafff7)，这是世界上最大的 DeFi 激励计划之一，现在正是学习如何在 Avalanche 上部署 dApp 的最佳时机。在本教程中，我们将介绍如何构建和部署一个检索 Chainlink 价格数据的 Solidity 智能合约，这些数据可用于确定所需的贷款抵押品、令牌之间的汇率、dApps 参与者的奖励率等。由于其新颖的一致性算法，Avalanche 提供了高水平的吞吐量、低延迟的事务终结性以及可伸缩的、高度分散的验证器架构。此外，由于 Avalanche 是 EVM 兼容的，我们可以使用所有标准的以太坊工具。在这种情况下，我们在基于浏览器的 Solidity IDE Remix 中进行构建。  

你可以使用这个 [混合要点](https://remix.ethereum.org/?#gist=8c19940a9c1b96bc453cbd43378df63c) 跟随并部署代码。

```
// SPDX-License-Identifier: MIT
pragma solidity 0.8;

import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract AvaxLinkFeeds {

    AggregatorV3Interface internal priceFeed;

 /**
 * Network: Fuji
 * Aggregator: AVAX/USD
 * Address: 0x5498BB86BC934c8D34FDA08E81D444153d0D06aD
 * URL: https://docs.chain.link/docs/avalanche-price-feeds/
 */
    constructor() {
        priceFeed = AggregatorV3Interface(0x5498BB86BC934c8D34FDA08E81D444153d0D06aD);
    }

 /**
 * Returns the latest price
 */
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
}
```

## 写合同

我们将首先为价格提要导入必要的 Chainlink 契约，即“AggregatorV3Interface.sol ”,它包含从现有的预聚合分散价格提要中检索数据的接口。要使用这个接口，我们需要知道价格提要位于哪里。这可以在[链节雪崩进给](https://docs.chain.link/docs/avalanche-price-feeds/)文档中找到。我们使用的是 AVAX/USD 提要的地址，所以我们可以简单地初始化价格提要接口，在构造契约时将该地址作为惟一的参数，如下所示:` price feed = aggregator v3 interface(0x 5498 bb 86 BC 934 c8 d 34 FDA 08 e 81d 444153 d0 d 06 ad)；`

初始化后，我们可以通过调用函数“latestRoundData()”从聚合器接口获取最新的价格数据，如“getLatestPriceData()”所示。这返回了关于提要的多点信息，但是我们只关心价格，所以我们只返回价格。因为这个函数不修改任何东西，只是从聚合器接口读取数据，所以它被定义为一个视图函数，幸好它不使用 gas。

## **编制和部署合同**

部署这段代码很简单，由于 Avalanche 的 EVM 兼容性，对标准以太坊部署路径的改动很小。从编译器标签下的 Remix 中编译开始；只需点击“编译 AvaxLinkFeeds.sol”。然后，进入 Deploy 选项卡，将环境设置为 Injected Web3(元掩码)，并为 Avalanche 的 Fuji testnet 配置元掩码。为此，只需将这些设置作为“自定义 RPC”添加到元掩码网络中。

![MetaMask Network Illustration - Custom RPC](img/3e83a781eec063f6016799023707fdb4.png)

<figcaption id="caption-attachment-2629" class="wp-caption-text">Select Custom RPC on MetaMask</figcaption>



网络名称:雪崩富士 C 链

新建 RPC URL:https://API . avax-test . network/ext/BC/C/RPC

chained:43113

符号:AVAX

Explorer:https://cchain . Explorer . avax-test . network

然后进入[https://水龙头. avax-test.network/](https://faucet.avax-test.network/) 获取一些免费的 testnet AVAX 用于部署您的合同。有关此设置过程的更多信息，您可以查看雪崩文档 上的 [部署智能合同。](https://docs.avax.network/build/tutorials/smart-contracts/deploy-a-smart-contract-on-avalanche-using-remix-and-metamask)

现在合同已经完成，您的网络设置为 Fuji，您的地址由 testnet AVAX 提供资金，您只需选择“AvaxLinkFeeds”合同并点击“部署”即可部署到网络。您的合同现已在 Avalanche 上生效，并准备好使用 Chainlink 对现实世界的数据做出反应。  

![Deploying to Avalanche ](img/f9d14548739c49ce555ec369dd6dc087.png)

<figcaption id="caption-attachment-2630" class="wp-caption-text">Deploying to Avalanche</figcaption>



只需调用 getLatestPrice，您将看到返回的 AVAX/USD 的精度为 8 位小数，此处的值为$51.54。

就是这样:一个导入，一个初始化提要的构造函数，一个读取价格数据的函数(不带 gas！)都需要使用 Chainlink 的行业标准价格数据来增强您的智能合同。

## 摘要

Avalanche 为构建智能合约应用程序提供了一个强大的选择，网络的高速度和低成本使其成为对开发者有吸引力的前景。当与 Chainlink 分散式 oracle networks 结合使用时，Avalanche 变得更加强大，能够访问链外数据和事件。Chainlink 价格馈送提供高质量的聚合价格数据，可用于各种有用的[](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/#decentralized-finance)【应用，如分散交易所(dex)、流动性池、借贷协议、分散保险解决方案和自动做市商(AMMs)。

如果您想了解更多关于在 Avalanche 上构建的信息，请观看本次研讨会，来自艾娃实验室的 Connor Daly 将为您演示在 Avalanche 上构建第一个 dApp 的过程。

[https://www.youtube.com/embed/UdzHxdfMKkE?feature=oembed](https://www.youtube.com/embed/UdzHxdfMKkE?feature=oembed)

Chainlink 是构建、访问和销售 oracle 服务的行业标准，可在任何区块链上支持混合智能合约。Chainlink oracle networks 为智能合约提供了一种可靠地连接到任何外部 API 的方式，并利用安全的链外计算来实现功能丰富的应用。Chainlink 目前在 DeFi、保险、游戏和其他主要行业获得了数百亿美元的资金，并为全球企业和领先的数据提供商提供了通往整个区块链的通用网关。

访问[chain . link](https://chain.link/)或阅读[docs . chain . link](https://docs.chain.link/)了解更多关于 Chainlink 的信息。 讨论一个整合， [联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=announcement) 。