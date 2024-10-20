# Oracle 计算:将 Oracle 的用途扩展到数据交付和离线计算

> 原文：<https://blog.chain.link/what-is-oracle-computation/>

*重点提示:*

*   oracles 的目的不仅仅是向区块链传递外部数据。oracle 还可以代表智能合约执行一种新型的信任最小化的链外计算，称为“Oracle 计算”。
*   Oracle 计算介于集中式 Web 2.0 计算和分散式区块链计算之间，实现了比区块链更高的性能和功能丰富性，同时比 Web 2.0 系统更防篡改和透明。
*   Oracle computing 通过提高可扩展性、成本效益和隐私性，以及授权访问订单公平性、可验证随机性、链外聚合和交易自动化等新功能，扩展了智能合同执行的能力。
*   Chainlink 为应用程序提供了由 oracle computation 支持的大量服务，包括 Chainlink Automation、Chainlink 可验证随机函数(VRF)、链外报告(OCR)和跨链互操作性协议(CCIP)。

—

[区块链神谕](https://blog.chain.link/what-is-chainlink/) 通常被认为具有数据传输能力，即从现实世界获取信息并将其传递到[](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/)上，以便智能合同应用程序引用。正如最初的 [Chainlink 1.0 白皮书](https://research.chain.link/whitepaper-v1.pdf) 中所述，分散式 oracle 网络(don)对于以高度可靠和防篡改的方式克服“ [oracle 问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)”——区块链无法本地连接外部数据资源——至关重要。

don 的数据交付能力已经实现了数百种不同的 [Chainlink 价格馈送](https://data.chain.link) 的创建，其提供了对金融市场数据的访问的智能合约。链式价格馈送是 [分散金融(DeFi)](https://chain.link/education/defi) 作为[【1000 亿美元+美元市场](https://defipulse.com) 快速增长的主要催化剂。DeFi 的一些领先应用程序依赖 Chainlink 价格馈送来执行链上功能，包括 Aave、Compound、Synthetix、Liquity 和 Sushi。

除了为 DeFi 应用程序提供市场数据，Chainlink oracles 还支持许多其他 [智能合约用例](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/) ，例如提供天气数据以自动化参数保险索赔，提供体育数据以结算预测市场，以及提供 [储备证明](https://chain.link/proof-of-reserve) 数据以审计支持令牌化资产的储备(例如，验证稳定的货币以 1 比 1 的美元支持)。然而，Chainlink DONs 不仅限于传输数据，还可以以一种独特的信任最小化方式为智能合约执行链外计算任务。

在下面的文章中，我们定义了 oracle 计算，提供了 Chainlink oracle 计算的真实示例，并展示了混合智能合同如何利用 chain link Oracle 的数据和计算来为自己配备比单独使用区块链或传统 Web 2.0 计算更先进的功能。

## 定义 Oracle 计算及其独特属性

计算是由一组指令逻辑定义的任何类型的计算，例如方程式或算法。计算会根据其输入产生一个确定性的输出，即如果满足 *x* 条件，则产生输出 *y* 。一个非常基本的计算的例子是取五个数字(输入)的中间值(指令)来得到一个结果(输出)。虽然计算可以手动执行，但今天的大多数计算都是数字化的——编写为由计算机执行的代码。数字计算存在于所有规模，从你手腕上的数字手表到训练高级机器学习算法的大型超级计算机。

区块链是一种新型的分散计算，它管理包含数字资产和数据的分布式账本。区块链还可以存储和处理关于智能合约应用程序当前“状态”的更新。可以将 State 视为应用程序在更广泛的区块链分类帐中自己的内部分类帐，对于资产如何在帐户之间移动有自己的规则(指令)。智能合约的每个状态改变都需要区块链执行某种类型的计算，例如:

*   验证私钥(即密码)生成的签名与发起交易的相应公钥(即地址)匹配
*   确认公钥地址有足够的账户余额来支付发送的金额和网络费用
*   使用用户输入执行智能合同，然后使用生成的输出更新合同状态
*   在区块生产期间生成工作证明哈希或利益证明证明，以使用包含用户交易的新区块扩展分类账
*   通过重新执行存储在块内的所有事务来检查网络内其他节点产生的块

虽然区块链为智能合约进行了防篡改计算，但每一种都有自己的局限性。例如，高度分散的区块链提供了为抵制审查而优化的计算，但也带来了更高的交易成本和更低的速度。更高速度的区块链针对更高吞吐量的事务进行了优化，但无法支持更高级的计算，如端到端隐私或事务自动化。

代替区块链执行所有 dApp 计算，许多计算可以离线执行，结果在链上中继。然而，集中式 Web 2.0 系统的传统链外计算与用户期望的区块链智能合约的保证不兼容。如果没有防篡改、透明和分散的计算来支持整个智能合约，那么使用区块链首先就没有什么意义。因此，如果智能合约将关键计算路由到链外以扩展其能力，这些链外网络必须提供与区块链类似的安全性、可靠性和透明度。进入信任最小化的链外计算，也称为 oracle 计算。

**Oracle computing 使用分散的 oracle networks (DONs)代表智能合约执行链外计算，同时保持与区块链的联系，以创建信任最小化保证。** 通过这种方式，管理员可以以高度可扩展、隐私保护和功能丰富的方式执行任何计算，与集中式 Web 2.0 系统不相上下，同时还可以利用各种区块链技术和依赖性来保持 oracle 计算的正确性、防篡改性、正常运行时间和透明度的更高标准。

![Spectrum of Computation](img/efa5c689268f9a3f270aaf8ff6c0ecf7.png)

<figcaption id="caption-attachment-2813" class="wp-caption-text">The trust-minimization and feature richness spectrum of computation</figcaption>



通过与区块链的协同关系，唐创造了信任最小化——一种计算将完全按照预期执行的信心。Oracle computation 使用与区块链类似的分散式架构来生成信任最小化，以避免单点故障，同时还受链上实施的用户定义的服务协议的约束。此外，DON 可以通过多方计算、密码证明、欺诈证明、链上重新执行等验证技术向区块链证明其链外计算的正确性和完整性。这些验证技术为进一步激励透明度和问责制提供了机会，如智能合同中概述的各种加密经济处罚或奖励的触发。

除了信任最小化，oracle 计算的另一个主要优势是相对于区块链计算的极大灵活性。虽然区块链计算非常标准化，但 oracle 计算可以包含任何设计模式，包括不同级别的分散、特定节点选择、定制计划、预定义的加密经济安全级别、组合安全技术等等。通过这种方式，用户可以根据自己的需求、信任假设和预算，优化 oracle 计算，在安全性和性能之间取得适当的平衡。

为了更好地理解 oracle 计算，让我们看看它是如何在整个 Chainlink 中实现的，以支持更高级的 [混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/) 。

## 链式网络中的 Oracle 计算示例

如 [Chainlink 2.0 白皮书](https://chain.link/whitepaper) 所述，Chainlink 网络演进的长期愿景包括通过提供外部数据和信任最小化的链外计算的 don 来增强新的和现有的区块链应用。通过由 Chainlink oracle 计算支持的一系列服务，包括自动化、可验证的随机性、链外报告、外部适配器和跨链互操作性协议，Chainlink 网络已经在努力实现这一愿景。

[https://www.youtube.com/embed/khhN54VKIbk?feature=oembed](https://www.youtube.com/embed/khhN54VKIbk?feature=oembed)

### 链环自动化

[chain link Automation](https://chain.link/automation)是一个事务自动化解决方案，在预定义的条件发生时触发区块链计算运行。Chainlink Automation 使用 oracle computation 来监控链上或链下条件的状态，例如时间的流逝(例如，24 小时过去了吗？)或事件的发生(例如，资产是否达到了某个价格？).一旦满足条件，Chainlink Automation 会提交一个链上事务，该事务会唤醒智能合约并触发它运行预定义的代码。Chainlink 自动化的一些常见用例包括在贷款协议中触发贷款清算，在[分散交易所](https://blog.chain.link/dex-decentralized-exchange/)中执行限价单，以及在预测市场中结算结果。

Chainlink Automation 通过使用分散的节点网络来执行合同逻辑的链外计算，然后在链上进行完全验证，从而实现信任最小化。Chainlink Automation 节点还会在链上对其响应进行加密签名，以便用户可以跟踪其可靠性，使用自动化故障转移流程来应对一个节点未能响应的情况，并生成呼叫数据来确定需要执行智能合约逻辑的哪一部分，以最大限度地降低燃气成本。此外，Chainlink Automation 消除了开发团队手动或通过集中式服务器执行这些任务的需要，从而减少了创建自动化 dApps 的摩擦。

![Chainlink Keepers](img/ec3b60e57f77bd71b1b4e58465b6dbb5.png)

<figcaption id="caption-attachment-2814" class="wp-caption-text">Chainlink Automation enables development teams to automate their smart contracts</figcaption>



### 链环可验证的随机性

[【chain link 可验证随机函数(VRF)](https://chain.link/solutions/chainlink-vrf) 是专为智能合约应用打造的安全可验证随机数生成器(RNG)解决方案。Chainlink VRF 的工作原理是离线计算一个随机值和一个相应的密码证明，然后在发送到用户的合同之前在链上进行验证。在不使加密证明无效的情况下，无法操纵产生的随机性，这有助于防止用户、oracles 或智能合约开发团队的操纵。因此，智能合约可以在应用之前充分验证随机性的完整性。

Chainlink VRF 的一些常见 dApp 用例包括:在铸造过程中公平地分配不同稀有性的特征给 NFTs 将无偏熵引入游戏机制，如匹配玩家和打开战利品盒；以及在幸运抽奖和无损失有奖游戏中随机选择获胜者。

![Chainlink VRF](img/f0b180566fe291cb7cfbb98619f94382.png)

<figcaption id="caption-attachment-2815" class="wp-caption-text">Chainlink VRF provides smart contracts a verifiable source of randomness</figcaption>



### Chainlink 离链报告和外部适配器

[【Chain link Off-Chain Reporting(OCR)](https://blog.chain.link/off-chain-reporting-live-on-mainnet/)是一种 oracle 网络协议，可提高链式分散 oracle 网络离线计算数据的效率。OCR 允许 Chainlink 节点使用对等网络将其数据聚合到链外的单个报告中，然后使用具有自动故障转移的旋转节点选择过程在单个事务中提交到链上。与以前的模型相比，通过利用 oracle 计算，OCR 将每次 oracle 更新的链上气体成本降低了高达 90%,同时还确保了完全的可问责性，因为每个 oracle 报告都包含每个节点的观察和签名。在下面的示例图中，OCR oracle 报表仅涉及一个链上事务，而如果聚合是在链上完成的，则涉及 15 个链上事务。

![Chainlink OCR](img/681c47b0daf133220ffa1b9ccb635a50.png)

<figcaption id="caption-attachment-2818" class="wp-caption-text">Chainlink OCR increases the efficiency of publishing oracle reports on-chain</figcaption>



通过引入 [Chainlink 外置适配器](https://blog.chain.link/build-and-use-external-adapters/) 可以增强 Chainlink OCR。Chainlink 外部适配器扩展了 oracle 节点可以访问的数据 Chainlink 的类型，以及它们可以执行的超出内置功能的计算类型。通常用于连接到受密码保护的 API，Chainlink 外部适配器还可以定义 oracle 如何执行计算，选择是否针对隐私、低延迟和/或高吞吐量进行优化。例如，外部适配器使 Chainlink 节点能够执行高级计算，如 [统计分析](https://blog.chain.link/off-chain-computation-statistical-analysis-with-chainlink/) ，价格指数的计算或机器学习处理。外部适配器也可以用于简单地将智能合同连接到来自外部网络(如云或大数据系统)的计算。

外部适配器的模块化特性为开发人员提供了一个框架，使他们能够利用区块链或 Web 2.0 系统无法提供的任何类型的智能合约计算，从而使 Chainlink 网络经得起未来考验。

![Chainlink External Adapters](img/a533f0acf09094cf2defc805744445b1.png)

<figcaption id="caption-attachment-2819" class="wp-caption-text">Chainlink External Adapters extend the types of data and computation Chainlink nodes can support</figcaption>



### 跨链互操作协议(CCIP)

[跨链互操作协议(CCIP)](https://blog.chain.link/introducing-the-cross-chain-interoperability-protocol-ccip/) 是一个正在开发中的开源标准，它在不同的区块链网络之间建立了一个通用的连接。CCIP 是支持创建安全令牌桥和跨链应用程序的主干，这些应用程序在区块链之间移动数据、资产和命令。Chainlink 节点使用 OCR 2.0 形式的 oracle 计算从一个区块链读取交易，生成关于其合法性的链外共识，然后将结果传输到另一个区块链。

在 CCIP 实施的许多形式的信任最小化之一是反欺诈网络——由独立于跨网络桥接资产和命令的节点组成的 DON。反欺诈网络使用 oracle computation 来分析 CCIP 网络，如果检测到协议或连接的区块链网络中的问题(如重组事件)，会立即暂停。重要的是，反欺诈网络不直接参与资金转移，而是作为一个制衡层。反欺诈网络和桥之间的权力分离通过减少任何单个组对其服务的控制来进一步降低 CCIP 的信任度。

![Cross-Chain Interoperability Protocol (CCIP)](img/85eb3df99d5d51eddf49763f724a5d62.png)

<figcaption id="caption-attachment-2820" class="wp-caption-text">CCIP connects blockchain networks and enables the creation of secure token bridges and cross-chain smart contracts</figcaption>



## Oracle 计算支持的混合智能合同

这些 Chainlink 服务展示了信任最小化的 oracle 计算如何通过与区块链的协作关系进一步扩展智能合同应用程序的功能。Oracle computation 不仅增强了智能合同应用，还可以通过支持计算的服务直接改善区块链网络的架构，例如用于交易排序的 [公平排序服务](https://blog.chain.link/chainlink-fair-sequencing-services-enabling-a-provably-fair-defi-ecosystem/) 和用于离线执行合同代码的第 2 层验证。鉴于其灵活性，oracle 计算在如何补充链上智能契约逻辑方面确实是无限的。

最终结果是 [混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/)——将区块链(链上)上运行的防篡改代码与 oracle networks(链下)提供的分散服务相结合的分散应用程序的激增，以实现更高级的效用。事实上，DeFi、游戏、NFTs 等领域最成功的智能合约应用都是混合智能合约。例如，DeFi 货币市场使用 Chainlink 价格馈送来访问外部金融市场数据，这些数据是确定用户的借贷能力和检查未偿贷款是否需要清算所必需的。当发现贷款抵押不足时，DeFi 货币市场还使用 Chainlink Automation 触发清算功能。链外数据和计算的结合也超越了货币市场，支持算法稳定积分、衍生品平台、预测市场、NFT 平台、无损失储蓄游戏等用例。

随着 Chainlink 2.0 白皮书中提出的愿景不断具体化，oracle 计算将在增强智能合约方面发挥类似的作用，就像 API 目前在支持 Web 2.0 系统方面发挥的作用一样。开发人员可以在他们的应用程序中利用不同类型的 oracle 数据和计算，因为他们知道这些服务通过各种信任最小化技术是安全可靠的。这将大大加快开发时间，因为团队可以专注于他们的应用程序的核心业务逻辑，而不是担心构建和维护链外基础设施。最终，这需要将 oracles 的定义扩展到提供智能合约的实体，这些智能合约提供所有数据和计算，而这些数据和计算在他们的本地区块链上无法以符合他们自己的信任假设、性能需求和预算的方式获得。

如果您想现在就开始构建混合智能合约应用程序，并且需要某种类型的外部数据或计算，请参考我们的 [文档](https://docs.chain.link/docs/getting-started) ，在[Discord](https://discordapp.com/invite/aSK4zew)中询问一个技术问题，或者 [与我们的一位专家建立一次通话](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=homepage) 。

要了解更多，请访问[chain . link](https://chain.link/)，订阅 [Chainlink 简讯](https://chn.lk/newsletter) ，并关注 Chainlink 上的[Twitter](https://twitter.com/chainlink)，[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)，以及[Reddit](https://www.reddit.com/r/Chainlink/)。