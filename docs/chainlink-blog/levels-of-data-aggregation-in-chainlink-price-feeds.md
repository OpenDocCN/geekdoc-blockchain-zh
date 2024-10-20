# Chainlink 价格馈送中的 3 个数据聚合级别

> 原文：<https://blog.chain.link/levels-of-data-aggregation-in-chainlink-price-feeds/>

[智能合约](https://chain.link/education/smart-contracts) 定义了链上协议可以处理用户资金的方式，而甲骨文是 [链外信息](https://blog.chain.link/understanding-how-data-and-apis-power-next-generation-economies/) 的来源，这些信息最终决定了这些资金最终将如何转移。外部事件和链上契约逻辑一起形成一个完整的契约流程，这使得 [oracle 机制](https://chain.link/education/blockchain-oracles) 对于智能契约的正确执行与其底层代码一样重要。

[![A clickable banner to a report detailing the Ultimate Guide to Blockchain Oracle Security](img/9ede9173a1fba83a6a8ec756c6b9e3a8.png)](https://chain.link/resources/blockchain-oracle-security)

<figcaption id="caption-attachment-3518" class="wp-caption-text">This guide gives a comprehensive breakdown on how to evaluate blockchain oracle security</figcaption>



[DeFi 协议](https://blog.chain.link/analyzing-the-defi-ecosystem-and-the-many-ways-chainlink-can-accelerate-adoption/)通常依赖市场数据来触发连锁事件，尤其是资产价格，以及其他类型的信息，如总加密市值、汇率和资产支持代币的储备余额。智能合约使用这些价格馈送来执行涉及用户资金的重要链上操作，如是否清算抵押贷款、合成资产互换的公平市场汇率，或者何时重新平衡使用自动化交易策略的投资组合。

[Chainlink Price Feeds](https://chain.link/solutions/defi) 已经成为 DeFi 市场中使用最广泛的价格先知，已经为 Aave、Synthetix 和向往等领先和新兴协议获得了数十亿美元的价值。Chainlink 价格馈送专门为 DeFi 应用程序提供最大的 oracle 安全性、可靠性和数据质量。这些属性是通过各种设计选择产生的，如 oracle 节点和数据源级别的分散化、安全节点操作符和优质数据源的选择、可证明的链上性能和可靠性以及安全性的加密经济激励。要更深入地了解 Chainlink 价格源，请阅读我们关于[数据质量对 DeFi 智能合约的重要性](https://blog.chain.link/the-importance-of-data-quality-for-defi/)的深度报道。

在本文中，我们通过关注每次价格更新时发生的三种类型的聚合来研究 Chainlink 价格提要的数据质量和 oracle 安全性:在数据源、节点操作符和 oracle 网络级别。通过了解每一个链价格馈送中特意构建的多层冗余，就可以清楚地了解为什么他们目前获得了大部分的 [DeFi](https://chain.link/education/defi) 市场份额。

![The basic flow of how crypto price data gets on-chain for DeFi](img/f64e8865ba428858680d2368af0f9a1e.png)

<figcaption id="caption-attachment-4939" class="wp-caption-text">The basic flow of how crypto price data gets on-chain for DeFi</figcaption>



## 数据源聚合

Chainlink 价格提要的第一个组成部分是 Chainlink oracles 用来获取价格数据的实际数据源。原始价格数据通常来自链外集中交易所(如比特币基地、币安)和链上[分散交易所](https://blog.chain.link/dex-decentralized-exchange/)协议(如 Uniswap、Kyber)。数据聚合器(如 BraveNewCoin、CoinGecko)从这些交易所收集原始交易所数据，以生成精确的数据集，如按交易量、流动性和时差对其进行加权，以及删除异常值、过滤虚假交易量、监控交易所停机时间等。拥有可靠的价格数据来源的关键是全面的市场覆盖，其中价格点代表所有交易环境的精细集合，而不是单个交易所或甚至一小组交易所，以防止数据操纵漏洞和/或交易量变化不准确。

为了确保高度的防篡改性和可靠性，Chainlink Price Feeds 专门从优质数据聚合器中提取数据。这意味着每个数据源都代表了一个从所有集中和分散的交易所聚集的经过调整的价格点，使其在本质上能够抵御众多攻击媒介，如[闪贷](https://blog.chain.link/flash-loans-and-the-importance-of-tamper-proof-oracles/)或异常偏差。

## 节点运算符聚合

链式价格反馈的第二个组成部分是每个 oracle 节点运营商的链上响应。这些[节点运营商](https://blog.chain.link/what-is-a-chainlink-node-operator/)由专业的 DevOps 团队组成，他们拥有运营关键任务区块链基础设施的经验，已经获得了数十亿美元的链上价值。他们负责运行 Chainlink 核心软件，该软件用于在[区块链](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/)上获取和传播外部市场数据。

Chainlink Price 中的节点操作符从多个独立的数据聚合器获取源价格数据，并获取它们之间的中间值，从而减少异常值和 API 停机时间。这意味着，不仅每个单独的数据源反映了来自所有交易环境的聚合价格点，而且每个单独的节点的响应代表了来自多个数据源的聚合，进一步防止了任何单个源成为故障点。



![Chainlink node operators take a median value from multiple data aggregators](img/4f64f68e44c6df45da53d029b85981df.png)

<figcaption id="caption-attachment-703" class="wp-caption-text">Chainlink 节点运算符从多个数据聚合器中取中值</figcaption>





## Oracle 网络聚合

链式价格反馈的第三个组成部分是整个 oracle 网络。oracle 网络定义了节点集合如何协同工作来创建链上的单个参考数据点，这通常涉及到聚合所有单个节点的响应。最常见的汇总形式是，一旦预定义数量的节点做出响应，就取报告值的中间值。最终，聚合可以采取多种形式，并且可以在链上或链外执行，具体取决于底层区块链网络的吞吐量和成本。

Chainlink 价格馈送汇总了许多经过安全审查的节点运营商的响应，并取中间值，需要一个预定义的阈值来响应，以便触发链上价格更新(例如，在下面的示例中，21 个中至少有 14 个)。这种类型的 oracle 网络聚合可确保 oracle 网络作为一个整体保持较高的正常运行时间，并防止链上数据交付中的操纵，即使在少数节点或数据源离线或试图执行恶意活动的情况下也是如此。



![The ETH/USD Chainlink Price Feed oracle network](img/38723e527ccf39a8a65d06ab815aaca6.png)

<figcaption id="caption-attachment-2241" class="wp-caption-text">ETH/USD 链价馈甲骨文网</figcaption>





通过在 Chainlink 价格馈送的数据源、节点运营商和 oracle 网络层中整合多层聚合，DeFi 应用程序在决定如何管理用户资金时，可获得其参考价格数据的行业级安全性和可靠性。正是因为这个原因，链接价格源已经成为 DeFi 经济中最广泛使用的安全链上价格数据来源，确保了数十亿的链上价值。

由于 Chainlink 网络的所有层都设计了安全性和可靠性，使用 Chainlink 价格反馈的 dApps 可以确保他们的合同将始终按预期执行，从而为扩展奠定坚实的基础，以确保为用户提供更多价值。

### 今天就开始用 Chainlink 建造吧

如果您是一名开发人员，并且希望快速将您的应用程序连接到 [Chainlink 价格参考数据](https://data.chain.link/)，请访问[开发人员文档](https://docs.chain.link/)，并参加 [Discord](https://discordapp.com/invite/aSK4zew) 中的技术讨论。如果您想安排一次电话会议来更深入地讨论集成，请联系此处的。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/)|[GitHub](https://github.com/smartcontractkit/chainlink)|[DeFi](https://www.chain.link/solutions/defi)