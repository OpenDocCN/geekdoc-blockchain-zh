# 宣布 Chainlink-Filecoin 联合资助结合分散存储和 Oracles 的 dApps

> 原文：<https://blog.chain.link/announcing-the-chainlink-and-filecoin-joint-grant-program/>

我们很高兴地宣布[Chainlink](https://chain.link)和[Filecoin](https://filecoin.io/)正在启动一项联合资助计划，以加速开发将 chain link 分散式 oracles 和 Filecoin 分散式存储结合在一个应用程序中的 [混合智能契约](https://blog.chain.link/hybrid-smart-contracts-explained/) 。

混合智能合约利用运行在区块链(链上)的代码和来自区块链之外(链下)的数据和计算。这种双重架构实现了高级形式的经济和社会协调，保留了区块链的防篡改和不可变属性，同时通过安全的离线 oracle 服务获得了额外的功能，如可扩展性、保密性和与真实世界数据源或系统的连接。通过将 Filecoin 和 Chainlink 结合在一起，开发人员可以构建端到端的分散式应用程序，这些应用程序具有经济高效且不可变的存储能力，以及与外部资源的通用安全连接。

在此之前，Filecoin 和 Chainlink 社区还联合开展了其他几项活动。首先，Chainlink 和 Filecoin 已经在 Chainlink 外部适配器 上 [工作，以促进两个项目之间的双向通信。此外，Chainlink Labs 团队作为第二批项目的顾问加入了](https://filecoin.io/blog/posts/filecoin-and-chainlink-integration/)[Filecoin launch pad Accelerator](https://www.filecoinlaunchpad.co/)，帮助他们使用 oracles 扩展应用程序的功能。Filecoin 还赞助了广泛参与的 2021 年春季 Chainlink Hackathon的奖项，有几个双重启用 Filecoin 和 chain link 的项目被纳入 Filecoin Launchpad 加速器，如[Tamago](https://tamago.finance/)、[Nifty Royale](https://niftyroyale.com/)和 [隐睾](https://cryptorchids.io/)

新的联合资助计划旨在支持和鼓励 Chainlink 和 Filecoin 之间更深入的整合，鼓励开发者创建直接结合两个网络的工作流。这可以通过几个关键的方式来实现，都有可能通过定制的 [Chainlink 外置适配器](https://docs.chain.link/docs/external-adapters/) :

*   **智能合约输入** —使用 Chainlink oracles 将 Filecoin 上存储的经过加密验证的数据连接到区块链。这些数据可以作为输入，在以太坊这样的网络上触发智能合约应用程序的执行。
*   **智能合约输出** —允许智能合约将输出发送到 Filecoin 作为数据存储的命令，使用 Chainlink oracles 桥接两种环境。
*   **智能合同自动化** —利用 [Chainlink Automation](https://chain.link/automation) 根据预定义的条件(如定期时间间隔或市场活动)触发输入或输出的 oracle 作业。

鉴于混合智能合约应用的快速增长，它们将继续生成和消耗大量数据是合乎逻辑的，这就需要更大的存储需求 同时保持区块链的防篡改性和可用性保证。Chainlink 中间件的双向通信功能使 Filecoin 和外部区块链之间的通信成为可能，这扩展了智能合约的不可变数据存储功能。

## 向 Chainlink 和 Filecoin 申请联合资助

chain link 和 Filecoin 联合资助计划正在支持多达五个团队构建由防篡改文件存储和通用连接支持的卓越混合智能合同应用。本质上，共同赞助的资助是给那些将 Web3.0 栈从链上计算扩展到分散的链外计算、数据和存储的开发人员的。

下面是一些可能的混合智能合约应用的例子，但是鼓励所有结合 Chainlink 和 Filecoin 的提议:

*   Filecoin miner 保险 —当 Filecoin Miner 不可靠时，Chainlink oracles 可以通知外部智能合同。如果先知无法从存储器中检索数据或确定矿工离线，保险赔付可以自动发放给另一个区块链上的投保人。
*   **数据奖励** —智能合同可以汇集资金用于存储特定的数据，这通过其唯一的内容标识符(CID)来表征。一旦证明它已经存储在 Filecoin 网络上的证据从 Chainlink oracles 转发，支付就被触发。
*   **永久存储**——由于 Chainlink 的双向连接，其他区块链上的智能合约可以为 Filecoin 上的存储提供资金和验证。合同可以建立在以太坊这样的网络上，任何人都可以在 Filecoin 上以特定的时间间隔存放和资助数据存储。
*   **DeFi Data** —智能合约可以使用 Chainlink 的 oracles 以防篡改的方式在 Filecoin 上存储大量金融数据，这些数据可以按需交付给各种区块链上的智能合约，以创建更多的互操作性。

如果您想参加 Chainlink-Filecoin 资助计划，请在 2021 年 9 月 17 日之前在此 处 [申请。最多有五个团队将被选为共同赞助的资助对象，用于他们项目的进一步发展。](https://github.com/filecoin-project/devgrants/blob/master/rfps/chainlink-and-filecoin.md)