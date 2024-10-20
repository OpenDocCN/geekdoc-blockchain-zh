# 什么是链环节点操作符？

> 原文：<https://blog.chain.link/what-is-a-chainlink-node-operator/>

*2022 年 7 月 27 日更新。* 
链环节点运营商是链环网络的骨干。Chainlink 节点运营商参与到[分散式甲骨文网络](https://docs.chain.link/docs/architecture-decentralized-model)中，允许工程师以安全可靠的方式[获取外部数据](https://blog.chain.link/apis-smart-contracts-and-how-to-connect-them/)。他们运营着至关重要的 oracle 基础设施，该基础设施负责确保每个区块链都能够访问他们需要正确执行的真实数据。例如，Chainlink 使用大量的节点运营商来共同推动各种分散的[价格反馈](https://chain.link/solutions/defi)Oracle networks live in-production，目前为 Synthetix、Aave、Compound、dYdX、Liquity 等领先的 DeFi 应用提供了超过 220 亿美元的价值。

正如我们之前在教育系列中提到的，由于支撑区块链的安全属性，所有智能合约(链上)都有一个固有的 [oracle 问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)，即无法从外部系统(链下)获取数据。这就需要使用 oracle 作为中间件，在链上和链下环境之间双向传输数据。在本文中，我们旨在概述节点运营商如何为 Chainlink 网络做出贡献，包括:

*   节点算子在链式网络中的作用
*   运行链节节点的要求是什么
*   Chainlink 节点运营商如何向智能合约出售数据
*   何处查找和评估链节节点运算符

## **节点操作符如何适应链式网络**

Chainlink 节点运营商是运行 [oracle](https://chain.link/education/blockchain-oracles) 基础设施(硬件和软件)的实体，该基础设施为 Chainlink 网络上运行的每个 oracle 网络提供动力和安全保障。这些 oracle 节点操作符负责监视来自智能合约的新的传入数据请求的区块链，从指定的 API 获取请求的链外数据，并在链上交付数据，智能合约可以使用这些数据来触发其执行。类似于互联网如何将计算机连接到外部世界，oracles 是区块链和任何外部数据或系统之间的桥梁。

虽然合同可以选择将其数据请求直接发送到单个 Chainlink 节点并接收单个响应，但 Chainlink 节点在组合成 oracle 网络时最为强大。分散式 oracle networks 聚合来自任意数量的 Chainlink 节点的数据，以消除在向区块链系统发送数据的过程中出现的任何单点故障。

链式网络是由独立的 oracle 和 Oracle 网络组成的无限可扩展的网络。尽管每个 oracle 都运行核心 Chainlink 软件，但它们最终的运行不依赖于任何其他 oracle，能够自由地同时成为不同 oracle 网络的一部分和/或独立运行。链式网络不允许在其上运行 oracle，但是每个 oracle 网络可以限制允许贡献的单个 Oracle，以及定制如何在其中获取和聚集数据。与区块链不同，它没有统一的共识机制或节点网络。



![The various components of Chainlink's oracle network](img/c38f28bad03f1071294e8738c6c6a578.png)

<figcaption id="caption-attachment-793" class="wp-caption-text">甲骨文网络</figcaption>



的各种组件

## **一个链环节点需要操作什么**

要成为 Chainlink 网络中的节点运营商并开始向 smart contracts 传送外部数据，Chainlink 节点设置中有一些技术要求，以确保平稳可靠的操作。核心组件包括:

*   **Chainlink 节点客户端软件**–由节点运营商运行的开源基础设施，连接链上和链下环境。
*   **链上 oracle 契约**–chain link 节点的智能契约，用于监控数据查询并将响应转发回请求用户的智能契约。
*   **数据源订阅**–chain link 节点代表请求智能合约连接并从中获取数据的链外数据源 API。
*   **外部监控系统**–实时监控链节点性能和可靠性的外围链外基础设施。

每个 Chainlink 节点操作符定期与这些组件进行交互。它们共同构成了一个链节节点，能够将数据安全地传送到任何区块链。

## 链接节点如何连接到链外资源

Chainlink 节点从一开始就被设计为在可以获取何种数据以及如何传递数据方面提供最高级别的灵活性。默认情况下，每个 Chainlink 节点都有一组预建的[核心适配器](https://docs.chain.link/docs/adapters)，允许它们连接到任何开放的 API 并在链上传递数据。虽然这些核心适配器为 Chainlink 节点提供了初始特性集，但真正开放对任何链外资源的访问的是外部适配器。

[外部适配器](https://docs.chain.link/docs/external-adapters)是模块化组件，可以添加到 Chainlink 节点，以极大地扩展其本机功能，特别是它可以访问的数据范围和它可以执行的计算类型。例如，外部适配器可用于对数据执行链外计算(生成节点响应的平均值)或访问需要凭证的经过身份验证的 API。

外部适配器是 Chainlink nodes 能够向智能合约销售任何类型数据的主要原因之一，也是它能够扩展到数据交付之外，包括双向通信、链外银行支付、与其他区块链的互操作性等等。最终，它们确保 Chainlink 网络可以不断扩展以支持新功能，因为新的外部适配器可以轻松创建，而不会危及网络的任何核心功能。

## 节点如何向智能合约出售数据

Chainlink 网络的灵活框架支持[两个 Chainlink 节点模型，](https://blog.chain.link/easily-sell-your-apis-and-data-to-any-blockchain-via-chainlink/)既支持快速加入链外数据提供商的现有需求，只需很少或不需要集成工作，也支持数据/API 基础设施的长期转型，直接向智能合同交付其自己的签名数据。



![The two ways to sell data using Chainlink](img/c3c34a8f9fdc6fe920d2dd39552edbb7.png)

<figcaption id="caption-attachment-794" class="wp-caption-text">两种方式出售数据使用</figcaption>



<figcaption></figcaption>



**标准 API 模型**中，节点操作符是一个独立于数据源的实体。通过将数据直接出售给 Chainlink 网络，Chainlink 节点可以为该数据付费，并使其在任何区块链可用，而无需数据提供商运营任何新的基础设施或修改其现有的商业模式。这使得世界上所有的数据和 API 服务都可以无缝地加入进来，因为数据提供商不需要承担将他们的数据集成到区块链的任何成本或责任。

**原始签名数据模型**是指数据提供者运行他们自己的 Chainlink 节点。这样做允许数据提供者使用唯一的私钥对他们的数据进行加密签名，并将其直接交付给智能合约本身。这增加了数据的 Sybil 抗性，因为最终用户可以明确地证明它来自特定的来源。它还消除了向智能合同出售数据的任何中间人，增加了数据提供商的收入，并帮助他们在不断增长的 Chainlink 生态系统中建立了作为可靠的事实来源的声誉。

这两种 Chainlink 节点模型都可以在一个分散的 oracle 网络中混合搭配使用。这种灵活性降低了加入 Chainlink 网络的门槛，并导致智能合同可获得更多数据集，而现有数据提供商没有任何负担。

## **如何查找和评估链节节点运算符**

![Chainlink Node Operator Infographic](img/275c1df0939cc9ee2150f9300a5b0802.png)

<figcaption id="caption-attachment-4186" class="wp-caption-text">The node operators that power the Chainlink Network leverage significant experience and expertise to facilitate the secure and reliable operation of Chainlink services.</figcaption>



链式网络使用“透明安全”方法，其中每个链式节点具有唯一的公共地址，它们从该地址提交数据，并随后使用它们相应的私钥对数据进行签名。作为具有不可变链上性能历史的可公开识别的地址，Chainlink 节点因其提供的所有 oracle 服务而享有声誉。

为了确保用户和智能合约开发人员可以轻松访问 Chainlink 节点的声誉，我们提供了多个独立的网站和 API，它们可以提供关于 Chainlink 网络整体性能以及每个分散的 oracle 网络、节点运营商和数据提供商的详细和精确的数据。

## 分散式 Oracle 网络可视化

Chainlink Labs 团队以简单、易于浏览的方式向公众提供了关于每个分散式 oracle 网络状态的链上性能数据，并深入了解了每个价格反馈的关键参数。 [Data.chain.link](https://data.chain.link/) 是一种资源，它提供了 chain link[DeFi](https://chain.link/education/defi)生态系统中所有价格反馈、项目和节点运营商的总集合，以及在 DeFi 经济中确保数十亿美元价值的许多价格反馈的实时状态。向用户提供以下信息:

*   mainnet 上所有实时价格信息的汇总视图
*   每个价格源的当前链上价格
*   更新频率和上次更新的时间戳
*   发布更新所需的最少节点数以及每个节点的状态
*   赞助和使用每个价格源的 DeFi 项目列表
*   为价格馈送提供动力的经过安全审查的链接节点的列表



![ETH/USD Chainlink Price Feed](img/b0230a15df9e4b1e2909de772c756e4c.png)

<figcaption id="caption-attachment-4187" class="wp-caption-text">可视化的链节 ETH/USD 价格馈送。</figcaption>





## Chainlink 节点运算符列表

Chainlink node 运营商能够在市场上向潜在用户展示自己，如 [market.link](http://market.link/) 。节点运营商可以列出他们的 oracle 服务、外部数据连接、认证等。这为 Chainlink 节点提供了一个向智能合同开发人员提供服务的平台，以及一个供用户分析每个 Chainlink 节点的重要特性以确定它们是否适合满足 oracle 需求的中心。



![Chainlink Node dashboard](img/2aec5706a88b63e403206a7324ea3ff9.png)

<figcaption id="caption-attachment-4188" class="wp-caption-text">用于查看单个链节节点的仪表板，如本例中的 LinkPool。</figcaption>





## Chainlink 网络统计和节点运营商信誉

链式链接节点的所有请求和响应都以不变的方式记录在链上，这可用于进一步分析整个链式链接网络的可靠性和准确性。 [Reputation.link](https://www.reputation.link/) 就是这样一个前端，它提取链上数据，为用户和节点运营商等提供关于 Chainlink 网络实时性能的全面概述。这为数据提供商和未来的节点运营商提供了关于链式网络的客观统计数据，并提供了关于各个节点运营商的更多细节。

所有这些资源的结合创造了前所未有的透明度，用户、开发者和节点运营商等可以在粒度级别上了解 Chainlink 网络的实时功能。通过这些数据，Chainlink 网络已经发展成为节点运营商质量和可靠性的黄金标准，确保现在和未来的高价值智能联系人拥有高质量 oracle 性能的明确证据。



![Reputation.link oracle explorer](img/d6bcef9c729197121015cc87a9afff9d.png)

<figcaption id="caption-attachment-4189" class="wp-caption-text">reputation.link 为用户提供了一个 oracle explorer 来分析 oracle 事务、提要和集成合同。</figcaption>





## 结论

节点运营商是 Chainlink 网络提供的每一个数据馈送的命脉，并在不断增长的智能合约经济中直接确保数十亿美元的价值。随着这一数据驱动的分散应用生态系统的不断扩大和发展，Chainlink 节点运营商的作用只会越来越重要，数量也会越来越多。Chainlink nodes 以安全性和灵活性为出发点，现在证明了分散式 oracle networks 的优势，它是一种创造真实世界的可靠手段，极大地扩展了智能合约的潜在市场。

如果您想阅读更多内容，请查看我们关于 DeFi 智能合同的[数据质量的文章，其中我们探讨了 oracles 采购高质量数据的极端重要性，以便扩展 DeFi 保护的价值数量。
在](https://blog.chain.link/the-importance-of-data-quality-for-defi/) [Twitter](https://twitter.com/Smart_Contract) 上关注我们，以获得即将发布的文章的通知，加入我们的 [Telegram](https://t.me/chainlinkofficial) 或 [Reddit](https://www.reddit.com/r/Chainlink/) 了解关于 [Chainlink](https://chain.link/) 的一般新闻，或参加关于我们[不和](https://discordapp.com/invite/aSK4zew)的技术讨论。