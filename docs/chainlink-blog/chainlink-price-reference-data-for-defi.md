# DeFi 的 Chainlink 价格参考数据

> 原文：<https://blog.chain.link/chainlink-price-reference-data-for-defi/>

*所有价格参考 Oracle 网络由一个位置的 Chainlink 提供支持*

在以太坊上构建开放金融产品的整个过程中， [DeFi](https://defi.chain.link/) 生态系统现在可以访问最大的链上市场数据集合！现在以太坊主网上有 30 多个分散式 Oracle 网络，并被领先的 DeFi 应用程序使用，如 [Synthetix](https://blog.synthetix.io/chainlink-decentralizes-first-wave-of-synthetix-price-feeds/) ，我们现在可以说，在高质量链上数据的帮助下，DeFi 空间正在缓慢增长。

使用 DeFi 的新 [Chainlink 价格参考数据，探索并获得加密货币、法定货币和商品价格的不断增长的列表，这些价格在链上可用，并由 Chainlink 的分散 oracle 网络保护。](https://feeds.chain.link/)

总体而言，这些分散的甲骨文网络为众多金融市场的各种领先 DeFi 产品提供了超过 1 亿美元的价值，例如 [ETH/USD](https://feeds.chain.link/eth-usd) 、 [BTC/USD](https://feeds.chain.link/btc-usd) 、 [XAG/USD](https://feeds.chain.link/xag-usd) 、 [MKR/ETH](https://feeds.chain.link/mkr-eth) 等等。

Chainlink 的价格参考数据 oracle networks 极大地扩展了以太坊 Dapps 可访问的安全可靠的数据量，大大加快了新 DeFi 产品成功上市的速度。Chainlink 分散式 oracle networks for Price Reference Data 是一种受用户支持的共享社区资源，用户使用这些 Oracle Networks 的费用低于单独广播相同数据的费用，同时受益于 Oracle Networks 分散式带来的安全性显著提高。

## 需要链环参考数据

DeFi 需要持续访问实时市场数据，尤其是价格，以可靠地执行支撑应用的逻辑。例如，货币( [Ampleforth](https://medium.com/ampleforth/the-ampleforth-chainlink-oracle-integration-is-going-live-16053ccdebd5) )、衍生产品( [Synthetix](https://www.youtube.com/watch?v=YWR3qENDebg) )、借贷( [Aave](https://medium.com/aave/the-aave-oracle-network-powered-by-chainlink-is-now-live-45bb8a5a8c4e) )和分散交换( [Loopring](https://medium.com/loopring-protocol/chainlink-and-loopring-collaborate-on-oracles-for-zkrollup-dex-protocol-c1c8094afc27) )协议都是需要在执行核心链上功能之前快速了解特定资产价格的应用程序的例子。

即使协定逻辑由高质量的代码组成，智能协定的输出也完全依赖于接收到的输入的质量。这意味着，获得准确的市场数据对于分散金融的安全性来说，就像基础智能合约本身一样至关重要。

虽然一些 Dapps 可以单独使用链上数据运行，但保守地说，90%以上的 DeFi 应用需要稳定地连接到链外数据，才能以可信、健壮和经济上可持续的方式运行。大多数价格发现发生在区块链网络之外(链外)，如在主要交易所，这些平台的价格各不相同。因此，获得最可靠的资产价格需要从多个链外数据源进行汇总。

区块链人获得这些链外信息的唯一途径是通过神谕。然而，聚合链上数据是昂贵的，特别是因为大多数项目需要一个持续的链上价格更新流来跟上市场波动。链式分布式 oracle 网络满足了这一需求。

## Oracle 参考数据网络的底层设计

![ETH/USD Price Feed](img/290c11db07af7f85987a832c31f2ac9f.png)

<figcaption id="caption-attachment-508" class="wp-caption-text">The dashboard for the current ETH/USD reference price oracle network with all 21 nodes</figcaption>



Chainlink 的分散式 oracle 网络由经过安全审查、抗 Sybil 和完全独立的节点组成。这些节点由领先的区块链开发团队和安全团队运营，他们中的许多人在运营 POS 节点方面拥有丰富的经验，这些节点在多个区块链网络中保护了数百万美元的价值。

每当有链上价格更新的请求时，网络中的每个节点都被赋予检索和提交当前价格的任务。然后，响应被聚合在一起，作为一个单独的价格更新。在节点层引入去中心化可确保所有基于 Chainlink 的价格参考数据 oracle networks 的高可用性。

他们还通过冗余来维护数据质量，让每个节点从 API 中检索价格，如 [CoinMarketCap](https://docs.chain.link/docs/coinmarketcap-chainlink-ethereum-mainnet) 、 [CoinGecko](https://blog.coingecko.com/coingecko-to-provide-cryptocurrency-market-data-for-chainlink/) 等。，它聚合了来自许多来源的数据。目前，大多数网络上使用七种数据聚合器。因此，链上价格更新是从可信数据聚合器检索价格的各个节点的累积聚合。这确保了 DeFi 应用程序不断与高质量的市场数据进行交互。

支持项目可以调用这些参考合同来访问触发核心产品功能执行的最新价格。可以根据时间(每小时、每天等)对链上更新进行编程。)、价格偏差(例如价格每 1%的变化)或适应特定用户需求的定制组合。

## 更深入地了解 Chainlink 参考数据

DeFi 资源的新 [Chainlink 价格参考数据可让您从一个用户界面轻松访问 Chainlink oracle networks 提供的所有价格参考数据。这是查找最近发布的参考数据的绝佳资源，并允许用户轻松访问有关基础架构、功能和分散式 oracle 网络的当前/历史数据的大量信息，从而确保这些价格。](https://feeds.chain.link/)

![Chainlink Price Reference Data](img/aaf12f8ada8bd5886c635851237f3b6d.png)

<figcaption id="caption-attachment-510" class="wp-caption-text">Some of the price pairs available for navigation on the Chainlink Price Reference Data for DeFi page</figcaption>



每个 Chainlink 价格参考 Oracle Network 的一些运营细节包括:

*   **涉及的 oracle 和 dapp:**探索保护特定价格馈送的单个 Oracle，以及支持和使用特定价格参考 oracle networks 的 dapp。用户可以确切地知道谁在保护他们的数据，以及有多少实时应用程序利用了某些参考数据。
*   **Oracle 网络功能:**了解当前在链价格、下一次价格更新，以及每个分散的 Oracle 网络在链上记录的频率和实际价格更新的历史数据。用户可以了解参考数据契约的编程方式，并对其历史功能进行分析。
*   **节点的链上指标**:检查构成分散网络的单个节点的性能的实时数据，例如使用的天然气量、单个价格提交以及它们提交数据的确切区块。

我们鼓励您更深入地探索不同的网络可视化和操作细节，并通过我们的 [Discord](https://discordapp.com/invite/aSK4zew) 提供任何额外的反馈来改善用户体验。

## 构建您自己的价格参考 Oracle 网络

如果您是一个 DeFi 项目，并且希望构建自己定制的由 Chainlink 支持的 oracle 参考数据网络，如支持项目所示，请联系我们[此处](https://chainlinkcommunity.typeform.com/to/XcgLVP)。

您可以轻松使用这些 oracle networks 快速安全地启动、添加更多功能和/或大大提高您的智能合同的安全性。