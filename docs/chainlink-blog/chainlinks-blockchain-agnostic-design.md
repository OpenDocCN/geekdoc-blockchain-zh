# Chainlink 的区块链不可知设计:对任何网络的原生 Oracle 支持

> 原文：<https://blog.chain.link/chainlinks-blockchain-agnostic-design/>

[智能合约](https://chain.link/education/smart-contracts) 生态系统日益向多链未来转移。 [区块链](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/) 的采用并非孤立于任何一个网络，而是发生在一个由各种分散分类账组成的生态系统中，每个分类账都有自己独特的价值主张和技术能力。不同的区块链和第 2 层解决方案针对不同的共识算法、安全模型、编程语言、硬件要求等进行了优化。这为开发人员和用户提供了灵活性，他们可以选择哪个网络最适合他们希望构建和交互的 [智能契约用例](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/) 。

然而，所有区块链和第二层网络的共同点是它们与现实世界隔绝，也就是所谓的“ [甲骨文问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/) ”克服这一障碍需要一个称为[Oracle](https://blog.chain.link/what-is-chainlink/)的额外基础设施，它为区块链及其支持的智能合约应用程序提供对安全可靠的外部数据源和链外计算的访问。

作为一个区块链不可知和 [异构框架](https://blog.chain.link/how-chainlink-supports-any-off-chain-data-resource-and-computation/) 用于构建分散式 oracle 网络，Chainlink 通过为开发人员提供在他们选择的区块链网络上构建 [混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/) 所需的安全 oracle 基础设施，积极支持多链生态系统。Chainlink oracle networks 已经在许多领先的区块链网络中获得了数百亿美元的资金，包括以太坊、BNB 链、多边形、灵知链、Heco、Avalanche、Fantom、Arbitrum、Harmony、乐观、Moonriver、Moonbeam、Solana 等。可以在 [Chainlink 文档](https://docs.chain.link/docs/reference-contracts/) 中了解在每个区块链网络上本地运行的 oracle 网络。

Chainlink 能够在 oracle 的本地支持下为如此广泛的区块链网络提供服务，这得益于由 [Chainlink 社区资助计划](https://blog.chain.link/introducing-the-chainlink-community-grant-program/) 支持的优秀开发团队，他们成功地集成、测试并监控了 Chainlink oracles 在各种区块链网络上的部署。通过该计划，其他区块链网络目前正在整合过程中，包括 Klaytn、RSK、Cosmos、Celo、Stacks、Plasm、Edgeware、OKExChain 等。随着对额外区块链网络支持的集成，这些环境中的开发人员可以构建更高级的 dApps 来利用链外资源，进一步推动该生态系统的发展。

然而，并非所有设计区块链不可知的 oracle 网络的方法都是一样的。在本文中，我们将探讨与区块链无关的 oracle 设计、Chainlink 针对原生区块链不可知论的独特方法，以及该方法如何支持跨链互操作性协议(CCIP)的开发。

## 与区块链无关的分散式 Oracle 网络

分散式 oracle networks 通过提供生成预期输出所需的数据输入和计算，直接保护智能合同应用程序的执行。如果交付的信息被破坏或不可用，用户的合同将不会按设计执行，并可能导致用户资金的损失。因此，必须谨慎对待 oracle networks 中的区块链不可知论，以免损害用户对混合智能合约应用程序的安全性、速度或可用性的期望。

### Oracle 区块链不可知论的次优方法的风险

区块链不可知论的一种方法是在一个区块链网络上运行 oracle 网络，然后使用中继器设计将报告的数据桥接到其他链。虽然这种设计在理论上确实提供了一种使用 oracle reports 在各种区块链上提供智能合约的方法，但它也引入了重要的权衡。

![Sub-optimal blockchain agnostic oracle design](img/3bbe74a6378beab4c55a4cbff5003ca6.png)

<figcaption id="caption-attachment-2435" class="wp-caption-text">The sub-optimal approach to a blockchain agnostic oracle network</figcaption>



首先，由于该设计中的 oracle 节点只能将数据直接交付给一个区块链，这意味着所有其他区块链的 oracle 更新频率和成本都受到主区块链的速度和吞吐量的限制。这就造成了一个瓶颈，即使部署和采用了更高吞吐量和更低成本的区块链和第 2 层网络，oracle 更新仍然受到桥接数据的主区块链的限制。这可能会增加用户的成本，并导致 oracle 更新的频率低于在区块链上本地运行的 Oracle。

其次，中继器设计增加了延迟，因为用户不仅必须等待数据首先在主区块链上交付，还必须等待数据被桥接到辅助区块链或第 2 层网络，智能合约就在该网络上运行。在市场波动和区块链网络拥塞期间，这可能会导致过时数据被交付给智能合约，最终会使协议面临抵押不足的风险。

第三，中继模式需要一组高度可用且受激励的第三方中继器，它们随时准备将 oracle 报告数据从一个链连接到另一个链。通常，这采用单个集中式中继器的形式，如果它出现宕机，会使其他区块链上的用户无法获得他们需要的数据。此外，这会增加成本，因为用户不仅需要支付足够支付将数据传送到第一区块链网络上的交易费用，还需要支付将数据传送到第二区块链上的交易费用。

最后，将 oracle 数据从一个区块链桥接到另一个会带来一系列严重的依赖性。用户必须相信，oracle 节点直接向其传送数据的区块链和使用的中继机制都按照设计正常运行。这扩大了必须信任的基础设施的范围，结果增加了用户智能合同的攻击面。

### Chainlink 的原生区块链不可知论方法

Chainlink 对区块链不可知论的研究遵循了与 relayer 设计完全不同的模型。Chainlink oracle networks 不仅可以将数据传送到一个区块链网络，还可以将数据桥接到其他链路，它可以将数据直接传送到任何区块链或第 2 层网络，而无需交叉依赖任何其他区块链网络或中继器。最终，这意味着 Chainlink oracle networks 可以直接在每个区块链上运行，为外部资源和链外计算提供原生 oracle 支持。

![Chainlink’s natively blockchain agnostic oracle networks](img/e7b92dedc44562db4d212003e5daa00f.png)

<figcaption id="caption-attachment-2436" class="wp-caption-text">Chainlink’s approach to native blockchain agnosticism in oracle networks</figcaption>



因此，Chainlink oracle networks 可以以任何区块链或第 2 层网络的本地速度和成本运行，从而使吞吐量更高、成本更低的区块链上的智能合同受益于更高频率和更低成本的 oracle 更新。例如，Polygon mainnet 上的 Chainlink oracle 网络已经在快速更新数据馈送，如果从较低吞吐量和/或较高成本的区块链桥接数据，这是无法实现的。

此外，由于一个区块链上的 oracle networks 不依赖于任何其他区块链，因此即使其他区块链遇到停机问题，用户也能更好地保证及时收到 oracle 更新。这种程度的分离降低了攻击面，减少了 oracle 更新延迟，并允许智能合约受益于他们选择部署的区块链的独特功能集。例如，以太坊等网络上的 Chainlink oracle 网络不依赖于更高吞吐量区块链的安全性或活性，这有助于确保提供准确的 oracle 报告不需要额外的信任假设。

最后，由于 Chainlink oracle 节点可以直接将数据传送到消费智能合约所运行的区块链网络，因此无需第三方中继。这增加了可靠性保证，并减轻了用户补偿跨多个区块链网络支付的交易费用的需要。因此，总体而言，用户可以获得更新鲜、更具成本效益的 oracle 更新。

我们与各种区块链和第二层网络的开发团队密切合作，以确保 Chainlink oracles 的深度本地集成满足其开发人员生态系统的长期可靠性和确切需求。在不牺牲安全性、速度或可靠性的情况下，Chainlink 网络为多链生态系统提供了一个与区块链无关的分散式 oracle 网络集合，这些网络通过本机集成为任何环境中的混合智能合同应用程序提供支持。此外，Chainlink 将继续扩大其对更多区块链网络的支持，为更大的智能合约生态系统中的开发者提供支持。

## 与 CCIP 建立可互操作的多链生态系统

chain link 网络本身支持广泛的区块链和第 2 层网络，非常适合为多链生态系统提供最安全可靠的跨链消息传递解决方案，支持智能合约在不同链上环境之间桥接命令和令牌。重要的是，在其多链设计中避免使用第三方中继器有助于确保在跨链桥接数据时没有集中的故障点。随着 Chainlink 对更多区块链网络的支持不断增加，正在创建一个标准来促进多链生态系统的发展。

通过 [跨链互操作性协议](https://blog.chain.link/introducing-the-cross-chain-interoperability-protocol-ccip/)【CCIP】，一个跨链消息传递的全球开源标准，开发者将拥有创建真正安全的跨链应用和令牌桥所需的安全的链外基础设施。CCIP 将利用现有的超可靠、抗 Sybil 和区块链不可知的 Chainlink oracle 节点，这些节点已经在各种区块链网络的 DeFi 应用中保护了数百亿美元。通过创建跨越不同链的各种安全桥，所有这些桥都由通用 CCIP 标准提供支持，用户可以获得无缝的互操作性解决方案，而没有集中化的风险。

观看 Chainlink 联合创始人 Sergey Nazarov 在[智能合约峰会#1](https://www.smartcontractsummit.io/) 上宣布 CCIP:

[https://www.youtube.com/embed/btbIgwJy29s?feature=oembed](https://www.youtube.com/embed/btbIgwJy29s?feature=oembed)

新发明的风险管理系统“反欺诈网络”将进一步确保 CCIP 标准的安全。反欺诈网络将由分散的甲骨文网络和独立的节点委员会组成，其唯一目的是监测 CCIP 服务的恶意活动和区块链网络的活性。通过这一额外的验证层，可以自动触发紧急关机，保护用户免受潜在黑天鹅事件的影响。

![CCIP tech stack](img/9225a6c68a9c4905a9318a226cd6c4c9.png)

<figcaption id="caption-attachment-2437" class="wp-caption-text">CCIP is enabled through a layered tech stack including natively blockchain agnostic Chainlink oracle nodes</figcaption>



超过 100 个区块链网络与 Chainlink(T2)合作，许多已经在 mainnet 上得到支持，chain link 是一个理想的基础设施，作为所有区块链和第 2 层网络之间跨链通信的可靠中立协议。随着 Chainlink oracles 支持的区块链的不断扩展，开发人员可以访问他们需要的各种分散服务，以构建越来越先进的混合智能合约应用程序。

—

如果你是一名开发人员，想要将你的智能合同连接到 Chainlink 的安全离线服务，请阅读位于[docs . chain . link](https://docs.chain.link/)的文档 。讨论一个整合， [联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=announcement) 。