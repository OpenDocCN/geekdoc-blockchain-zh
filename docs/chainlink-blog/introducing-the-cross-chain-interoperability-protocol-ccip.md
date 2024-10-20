# 为分散的链间消息传递和令牌移动引入跨链互操作性协议(CCIP)

> 原文：<https://blog.chain.link/introducing-the-cross-chain-interoperability-protocol-ccip/>

众多独立的 [【区块链】](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/) 生态系统不断发展，优化程度和地理位置各不相同，这导致了一个越来越多链的世界。能够在单个应用程序中无缝利用这些区块链中每一个的优势及其独特的资产将推动新的跨链智能合同开发的巨大浪潮——与 [DeFi](https://chain.link/education/defi) 、[【NFT】](https://chain.link/education/nfts)和 [链上游戏](https://blog.chain.link/what-is-play-to-earn/) 经济在 [分散 oracle 服务时的激增没有什么不同](https://blog.chain.link/what-is-chainlink/)

然而，鉴于现有跨链基础设施的问题，构建跨链应用程序是众所周知的困难。首先，令牌桥和消息传递协议中存在大量碎片，大多数是两个不同链之间的特定于应用程序的服务。此外，许多网桥相当集中，安全保障薄弱，缺乏透明或可靠的节点运营商，增加了最终用户的成本和处理时间。这些限制和漏洞已经导致了高达数千万美元的资金损失，阻碍了跨链创新。

为了满足生态系统对链间解决方案日益增长的需求，我们很高兴地宣布即将推出[【CCIP】](https://chain.link/solutions/cross-chain)【跨链互操作协议】——一种全新的跨链通信开源标准。CCIP 旨在建立数百个区块链网络之间的通用连接，包括私有和公共网络，解锁孤立的令牌，并为所有链上生态系统提供跨链应用。

![Using CCIP to send messages between blockchains](img/cde27b93da5ca3655cde28039c96e0ce.png)

CCIP 为[智能合约](https://chain.link/education/smart-contracts)开发商提供通用的、支持计算的基础设施，用于在区块链网络间传输数据和智能合约命令。CCIP 将支持各种跨链服务，如 Chainlink 可编程令牌桥，这将使用户能够以高度安全、可扩展和经济高效的方式在任何区块链网络中移动令牌。

观看 Chainlink 联合创始人 Sergey Nazarov 在[智能合约峰会#1](https://smartcontractsummit.io/) 上宣布 CCIP:

[https://www.youtube.com/embed/btbIgwJy29s?feature=oembed](https://www.youtube.com/embed/btbIgwJy29s?feature=oembed)

跨链互操作性协议是安全跨链技术多年研发的结晶，可追溯到 [Chainlink 1.0 白皮书](https://research.chain.link/whitepaper-v1.pdf) 的初衷。CCIP 由 Chainlink Labs 首席科学家 Ari Juels、Chainlink Labs 工程副总裁 Ben Chan(在以太坊(WBTC)广泛使用的交叉链包装的比特币令牌背后的建筑师)以及与 Chainlink Labs 团队合作的众多世界级研究人员领导。

在下面的文章中，我们将概述为什么 Chainlink 经过优化，为区块链行业提供通用的跨链通信协议，CCIP 如何融入多层技术堆栈，以及 CCIP 将如何为各种服务提供动力，以支持跨链的发展[混合智能合同](https://blog.chain.link/hybrid-smart-contracts-explained/)。

## 为什么 Chainlink 针对通用跨链基础设施进行了优化

为跨所有区块链网络的令牌移动和通用消息传递构建安全高效的跨链技术并非易事。然而，Chainlink 现有基础设施的历史可靠性，以及不断增长的 Chainlink 生态系统和特定的跨链技术创新，使 Chainlink 成为最适合作为跨链通信开源标准的协议。

### 经验证的节点运营商分散网络

最基本的跨链桥是一个由节点组成的委员会，这些节点共同证明一条链上的信息，并通过以门限方式对交易进行加密签名，将信息转发给另一条链。Chainlink 网络已经得到了业内最大的独立、抗 Sybil、可靠的节点运营商的支持，这些运营商由世界上一些顶级的 DevOps 和基础设施提供商组成。Chainlink 不断增长的节点运营商网络通过众多 oracle 服务为智能合同生态系统提供了超过 300 亿美元的资金，并将通过即将到来的对 Chainlink 的 [非链报告协议](https://blog.chain.link/off-chain-reporting-live-on-mainnet/) (OCR)的升级进一步扩大规模。

Chainlink OCR 1.0 是一种用于数据聚合的安全、高效的链外计算协议，该协议已经成功大规模运行了一段时间，成功地将 oracle 报表的链上气体成本降低了 90%。OCR 2.0 将在这一成功的基础上更进一步，支持更高效、更有表现力的链外计算，从而带来高级的跨链功能。CCIP 将在其协议栈中利用 OCR 2.0，将签署基于委员会的报告的节点数量扩展到数百个，从而提高锁定资金的安全性，同时为用户保持高度的成本效益。结合世界上最大的安全节点运营商与升级的链外计算能力，CCIP 将实现高度的防篡改和性能。

![Chainlink OCR 2.0](img/d8095f9940771ebb014f6248741e5bf6.png)

<figcaption id="caption-attachment-2206" class="wp-caption-text">Chainlink OCR 2.0 aggregates node responses off-chain and commits the oracle report on-chain as a single transaction.</figcaption>



### 反欺诈网络

安全性和欺诈防范是跨链服务的基本要素，旨在直接保护高价值合同。为此，CCIP 将包括一个新发明的风险管理系统，这是区块链业界前所未见的，被称为反欺诈网络。反欺诈网络将由分散的 oracle networks 组成，其唯一目的是监控 CCIP 服务中可能导致财务损失的恶意活动。重要的是，反欺诈网络将包含完全独立的节点委员会，而不是他们在 CCIP 上负责监控的节点委员会，将反欺诈检测和跨链服务完全分离。

反欺诈网络充当验证层，将在系统正常运行时定期提交心跳检查。如果反欺诈网络的心跳消息停止或其节点注意到任何恶意活动，就会自动触发紧急关闭，以停止特定的跨链服务。暂停可以保护用户资金免受影响服务的潜在黑天鹅事件的影响。虽然反欺诈网络最初将由独立于其保护的 CCIP 服务的高质量 Chainlink 节点组成，但通过 CCIP 服务获得大量价值的 dApps 可以加入反欺诈网络，以向其用户提供更大的保证，即任何欺诈活动都将被发现并减轻。

反欺诈网络是风险管理和反欺诈检测的分散实施，通常用于保护高价值合同。反欺诈网络通过建立制衡系统来分离责任，并最大限度地减少任何单个团体对 CCIP 服务运营的控制，从而彻底改变了跨链基础设施中的风险管理方式。重要的是，该网络还可以通过增加人工智能等增强的检测技术来扩展和发展到未来。

![Anti-Fraud Network](img/929f223ef226be67b922b7424c854b95.png)

<figcaption id="caption-attachment-2208" class="wp-caption-text">The Anti-Fraud Network monitors CCIP services in order to identify and mitigate any potential issues.</figcaption>



### 整个区块链的大型生态系统支持

当交叉链系统具有大的网络效应时，它们是最有用的。网络效应提高了用户资金的安全性，增加了令牌访问并简化了用户体验，为开发人员提供了更好的文档和工具，并且无论资产在哪个区块链上本地启动，令牌供应都有更大的收入机会。超过 100 个区块链与 Chainlink 一起工作，许多区块链和第 2 层解决方案已经与 mainnet 上的 Chainlink 集成，Chainlink 是一个理想的基础设施，可作为所有区块链之间跨链通信的可靠中立协议。

chain link 是托普区块链公司最广泛集成的[甲骨文](https://chain.link/education/blockchain-oracles)解决方案，为区块链上运行的大量 dApps 提供动力。Chainlink 已经与顶级贷款、保险和其他 DeFi 协议合作，并正在通过开源开发和 [Chainlink 社区资助计划](https://blog.chain.link/introducing-the-chainlink-community-grant-program/) 加速在受支持的链内的采用。许多区块链合作伙伴和应用程序已经表达了使用 Chainlink oracles 进行跨链活动的愿望，这使得为整个智能合约行业带来一套高度安全、可靠和高性能的通用跨链解决方案成为当务之急。

## 定义跨链技术堆栈

跨链互操作性协议(CCIP)位于一个分层的开源技术堆栈中，该堆栈将用于为用户提供新的跨链服务，如 Chainlink 可编程令牌桥、各种其他桥实现，以及创建跨任何区块链网络的强大跨链应用的能力。技术堆栈的每一层都在最终支持不断扩大的多链生态系统方面发挥着关键作用。

![Cross-Chain Tech Stack](img/f429e1fdcadb68f00403a44ea7f3394f.png)

<figcaption id="caption-attachment-2227" class="wp-caption-text">The Cross-Chain Interoperability Protocol (CCIP) is part of a layered open-source tech stack for supporting data and asset movements across blockchains.</figcaption>



### 用户界面

在技术栈的顶端是使用户能够连接到 Chainlink 可编程令牌桥或其他桥实现并开始在区块链环境中移动他们的令牌的接口。重要的是，新的和现有的生态系统项目可以以无许可的方式部署它们自己的接口。这可能包括已建立的钱包、聚合器、应用程序、交易所，以及希望为多链生态系统提供门户的各种面向用户的服务。通过对接口层采取社区驱动的方法，在用户如何与基于 CCIP 构建的解决方案交互方面，跨链基础设施可以变得易于访问、抗审查和创新。

### 可编程令牌桥

可编程令牌桥是建立在 CCIP 基础上的参考桥实现，允许开发人员构建跨链应用，在任何区块链上无缝、安全地移动其现有令牌。这是一个统一的桥系统，链之间的各种桥连接由独特的节点委员会保护，以便在使用路由契约维护通用互操作性的同时分配安全性。可编程令牌桥将支持现有的令牌标准，这意味着已经流动的资产可以立即在不同的智能合约生态系统中使用。除了采用高质量的节点运营商和分散架构之外，还将实施额外的安全预防措施，例如基于时间的流量限制，以最大限度地降低黑天鹅事件期间的下行风险——其参数可以由大得多的 don 管理。

可编程令牌桥支持计算，使用户和智能合约不仅可以向桥发送令牌，还可以向桥发送命令，并让桥围绕其与其他区块链的交互方式运行定制逻辑。用户不需要知道如何使用其他区块链，他们只需要向桥发送关于他们希望如何与其他链交互的指令，桥将自动跨链移动令牌，并在原子交易内的目标链上的智能合约中部署它们。因此，用户可以留在他们选择的区块链，同时仍然受益于其他区块链网络上的智能合同生态系统。可编程令牌桥开辟了高级混合智能合约用例，如跨链收益聚合器、抵押贷款等等。重要的是，可编程令牌桥只是 Chainlink 实验室构建的一个参考实现，但任何第三方桥应用程序都可以由希望利用 CCIP 的安全性和功能的独立开发团队轻松构建。

### 跨链互操作协议(CCIP)

CCIP 是一种开源标准，它使任何区块链上的智能合约能够向任何其他区块链网络上的智能合约发送数据包，并从其接收数据包。该协议在本质上是通用的，支持智能合约可能希望跨链交付的任何类型的数据的交付。通用的跨链互操作性将为开发人员提供一个简单的框架来构建跨链应用程序，而无需处理底层协议的复杂性。

基于 CCIP 构建的所有应用程序，如可编程令牌桥、其他跨链桥和跨链 dApps，都可以利用反欺诈网络的安全性，以便自动检测和缓解恶意活动。我们还在探索可在未来部署的深度防御方法，如可信执行环境、用于密钥管理的硬件安全模块、通过赌注实现的加密经济安全性等。

### 网络基础设施

Chainlink 的跨链技术体系将由独立、声誉卓著的 oracle 节点运营商的分散网络提供支持。Chainlink 节点将运行 OCR 2.0 客户端，以安全和经济高效的方式就跨链交易达成链外共识。OCR 2.0 消除了任何单点故障，并支持扩展到数百个独立节点运营商的能力，而不会显著增加链上天然气成本。重要的是，该报告将包含每个响应的 oracle 节点的签名，从而创建责任并提供可用于实现信任最小化技术的线索。

## **跨链应用无缝连接到所有区块链**

CCIP 的引入旨在快速扩展开发者可以在每个区块链上构建的东西。全新的跨链应用成为可能，它们同时利用所有链上的令牌，并利用特定链或这些链上的应用和资产的独特属性。

这开启了全新的跨链应用，如跨链协议，它们利用一个区块链的可扩展计算、另一个的令牌多样性、第三个的存储和第四个的结算安全性来创建一个具有卓越功能的混合智能合约应用。确实有无限的可能性，我们很高兴在不久的将来为区块链行业带来初步的实施。

无论您是用户、界面、应用还是现有的跨链桥，我们都希望听到您对 CCIP 的反馈，以便继续改进。请在 [【电子邮件保护】](/cdn-cgi/l/email-protection#8ae9e9e3facaf9e7ebf8fee9e5e4fef8ebe9fea4e9e5e7) 分享任何反馈。通过社区反馈，CCIP 可以适应所有区块链生态系统和使用案例的跨链需求，最终推动巨大的开发和创新浪潮，将所有生态系统的混合智能合同行业推向采用和成熟的新水平。

如果您对使用 CCIP 构建跨链功能感兴趣并想了解更多，请访问[【https://chain.link/solutions/cross-chain】](https://chain.link/solutions/cross-chain)了解更多，并访问 [联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog) 。

要了解更多关于 Chainlink 的信息，请访问[chain . link](https://chain.link/)，订阅 [Chainlink 简讯](https://chn.lk/newsletter) ，并在 Twitter 上关注[@ chain link](https://www.twitter.com/chainlink)。