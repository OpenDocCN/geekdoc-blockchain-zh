# 什么是区块链互通？

> 原文：<https://blog.chain.link/interoperability-and-connectivity-unlocking-smart-contracts-3-0-2/>

[](https://blog.chain.link/what-is-blockchain/)是去中心化的计算机网络，在数字账本中跟踪用户的账户余额和数据。区块链不依赖于集中的权威，而是使用分散的共识，在接受之前集体同意对分类帐的更新提议。其结果是一个新的 [信任最小化计算范例](https://blog.chain.link/what-is-trust-minimization/) 用于多方记录保存和流程自动化，比传统计算环境更加可信、中立、防篡改和透明。

然而，区块链类似于没有互联网连接的计算机——它们没有与其他区块链或 [外部 API](https://blog.chain.link/understanding-how-data-and-apis-power-next-generation-economies/)的内置通信能力。这种限制通常被称为[Oracle 问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/) ，它不仅禁止区块链与传统系统交互，还阻止了区块链之间的互操作性。随着多区块链世界的日益现实，区块链互操作性协议成为在不同区块链之间交换数据和令牌(即跨链)的关键基础设施。

以下文章是关于区块链互操作性的定义和重要性的教育入门，同时概述了不同类型的区块链互操作性解决方案，以及由[Chain link](https://chain.link/)支持的 [跨链互操作性协议(CCIP)](https://chain.link/cross-chain) ，如何扩展[Oracle](https://chain.link/education/blockchain-oracles)的功能，以支持跨链的任意数据消息传递。

# 什么是区块链互通？

区块链互操作性是指区块链与其他区块链进行通信的能力。区块链互操作性的基础是跨链消息协议，它使区块链能够从其他区块链读取数据和/或向其他写入数据。

跨链消息传递协议支持创建[](https://blog.chain.link/cross-chain-smart-contracts/)跨链分散式应用(dApp)，其中单个统一 dApp 可以跨多个不同的 [智能契约](https://chain.link/education/smart-contracts) 运行，部署在多个不同的区块链上。跨链 dApp 与多链 dApp 的不同之处在于，多链 dApp 通常在多个区块链上部署相同的应用程序，但是每个实例都是一组独立的智能合约，与其他区块链没有任何联系。

![Cross-chain smart contracts](img/bd5a2aec9bba1f0ec1efeefd6a8218c7.png)

<figcaption id="caption-attachment-3277" class="wp-caption-text">Cross-chain dApps have unified logic across smart contracts deployed on different blockchains.</figcaption>



利用跨链消息传递协议的跨链 dApps 的范围有限；例如，令牌桥的存在只是为了将源区块链上的令牌传输到目的地区块链。然而，任意数据消息协议提供了更一般化的跨链功能，其可以支持更复杂的 dApps，例如跨链[【DEXs】](https://blog.chain.link/dex-decentralized-exchange/)、跨链 [分散货币市场](https://blog.chain.link/decentralized-money-markets/) 、跨链[NFTs](https://chain.link/education/nfts)、跨链 [分散自治组织(DAOs)](https://blog.chain.link/daos/)

# 区块链互通的重要性

当前的 [Web3](https://chain.link/education/web3) 景观日趋多链条、多层次。已经有超过 100 个第 1 层区块链(即基础层)和越来越多的 [第 2 层](https://blog.chain.link/what-is-a-layer-2/) 以及最终的第 3 层网络存在于基础层区块链之上。第二层和第三层网络本质上是独立的区块链，它们将其安全性的一部分锚定到基础层(例如 [汇总](https://blog.chain.link/arbitrum-and-chainlink-fair-sequencing-services/#what-are-rollups-and-their-core-benefits:~:text=What%20Are%20Rollups%20and%20Their%20Core%20Benefits%3F) )。

基础层和第二层网络的激增是区块链技术和区块链生态系统富有表现力的设计空间的结果。区块链通过优化其协议以支持某些功能集来争夺开发人员和应用程序，通常是通过与其他功能进行权衡。例如，一些区块链更关注分散化和审查阻力，而不是基础层的吞吐量和可组合性，而其他区块链选择以牺牲可信硬件中的新安全假设为代价来构建本地隐私功能。

区块链通过试验不同的共识协议、执行环境和数据存储解决方案进行优化，这些解决方案为开发人员提供了关于成本、活跃度、性能、数据可用性、安全性、密码经济学和环境影响的各种假设。此外，区块链可能会通过提供对特定编程语言的支持，专注于捕捉特定的用例及地理位置，以及开发独特的品牌和价值来吸引观众，从而使自己与众不同。

优化选择的一个主要差异围绕着区块链关于如何扩展其生态系统的一个特定论题。缩放论文的例子包括:

*   拥有单一的高性能基础层区块链，支持所有垂直行业的所有应用。
*   拥有一个高度分散的基础层区块链，通过第二层和第三层可扩展网络支持大量模块化应用。
*   使每个应用程序和/或智能合同部门或用例在其自己的基础层区块链或独立的第二层网络上运行。

要深入了解区块链可扩展性解决方案，请查看博客 [区块链可扩展性:执行、存储和共识](https://blog.chain.link/blockchain-scalability-approaches/) 。

鉴于区块链生态系统的多样性，所有这些不同的链上环境能够互操作至关重要。这对于希望构建跨链/模块化应用程序的开发人员来说尤其重要，这些应用程序在众多链上环境中保持单一的全局状态和统一的流动性。对于希望利用每个区块链的独特资产和功能的应用程序开发人员来说，这也很重要。

区块链互操作性协议对于需要从现有后端与许多不同区块链交互的传统系统同样重要。互操作性协议是构建区块链抽象层的基础，它允许传统的后端和 dApps 通过单一的区块链中间件解决方案与任何链上环境进行交互。如果没有区块链抽象层，Web2 系统和 dApps 将需要为他们想要利用的每个跨链交互构建单独的内部实现——这是一个非常耗时、资源密集型和复杂的过程。

# 区块链互操作解决方案的类型

尝试对区块链互操作性解决方案进行分类的最佳起点是查看最流行的跨链交互。

**代币互换** 涉及在源链上交易代币，在目的链上接收不同的代币。跨链代币互换通常通过原子互换协议和/或跨链 [自动做市商(AMMs)](https://blog.chain.link/automated-market-maker-amm/) 来实现，它们在每个区块链上都有单独的流动性池来促进互换。

**令牌桥** 涉及通过源链上的智能合约锁定或烧毁令牌，以及通过目的链上的单独智能合约解锁或铸造令牌。令牌桥允许资产在区块链转移，通过使跨链流动性成为可能来增加令牌的效用。有三种类型的令牌处理机制支持令牌桥:

*   **锁定和铸造令牌桥(即 IOU)** 在源链上的智能合约中锁定令牌，然后在目标链上铸造令牌的包装版本，通常称为桥接资产。反方向，目的链上包裹好的代币被烧掉，解锁源链上的原币。
*   **刻录和铸造令牌桥(即本机)** 在源链上刻录令牌，然后通过在目的链上铸造令牌来重新发布相同的令牌。
*   **锁定和解锁令牌桥** 锁定源链上的令牌，然后从目标链上的流动性池中解锁相同的令牌。这些类型的代币桥通常通过收入共享等激励计划吸引桥两边的流动性。

**本地支付** 涉及源链上的应用程序在其本地资产中触发目的链上的支付。跨链支付也可以基于来自单独的区块链的数据在其本地资产中的源链上进行。这些支付中的大多数通常代表某种形式的结算，并且可以基于区块链数据或者甚至外部事件。

**契约调用** 涉及源链上的智能契约，调用目的链上部署的智能契约函数，潜在地基于源自源链的数据。几个契约调用可以组合起来形成一个更复杂的跨链应用程序，其中可能涉及令牌交换和桥接。

**可编程令牌桥** 涉及令牌桥和任意消息传递的组合，其中一旦令牌从源链被递送到目的链，就可以执行契约调用。这发生在单个交易中，实现了更丰富的跨链功能，例如作为完成桥接功能的一部分，在目标链上的智能合约中下注、交换或存放令牌。

为了支持这些跨链交互，有四种通用的互操作性解决方案来验证源区块链的状态，并将后续事务转发到目的地区块链。这两个功能——状态验证和中继——是完成大多数跨链交互的关键。

## Web2 验证

Web2 验证 是指某人使用 Web2 服务执行跨链交易。实践中最常见的例子是用户利用集中式交换来交换或桥接他们自己的令牌。用户只需将他们的资产存入交易所控制下的源链上的一个地址，然后将相同的令牌或不同的令牌(通过交易所上的互换)提取到用户控制的目的链上的一个地址。

Web2 验证对于个人交易来说非常方便，并且不需要太多的专业技术知识。然而，它对于支持跨链应用程序并不那么有用，并且需要信任一个集中的保管者。此外，它主要限于在交易所支持的区块链之间交换和桥接令牌。

## 外部验证

外部验证是指使用一组与跨链交互中涉及的任一区块链的验证器节点不同的验证器节点来验证源区块链的状态，并在满足一组特定标准时触发目标链上的后续事务。虽然有许多基于委员会的共识的方法，即多方计算、分散 oracle 网络、门限多签名契约，但它们都涉及验证器节点进行信任最小化的 [链外计算](https://blog.chain.link/what-is-oracle-computation/) 链上认证的计算(即 [混合智能契约](https://blog.chain.link/hybrid-smart-contracts-explained/) )。

外部验证通常需要诚实多数假设，其中大多数外部验证器节点必须诚实行为，以便维护跨链交互的完整性。然而，可以利用其他技术来增加信任最小化，例如乐观桥验证、反欺诈网络和加密经济赌注。 尽管有额外的信任假设，外部验证是当前在某些类型的区块链之间执行跨链契约调用同时仍然提供信任最小化保证的唯一可行的方式。它也是高度通用和可扩展的跨链计算形式，能够支持更复杂的跨链应用程序。

## 本地验证

本地验证是指跨链交易中的交易对手验证彼此的状态。如果双方都认为对方有效，则执行跨链事务，从而产生对等跨链事务。使用本地验证的跨链交换通常被称为原子交换。

给定合理的区块链假设，通过原子互换的本地验证具有高度的信任最小化，因为互换或者发生或者两个交易都失败。然而，它并不能很好地推广到各种跨链合约看涨期权，并且伴随着像 [无意看涨期权问题](https://blog.bitmex.com/atomic-swaps-and-distributed-exchanges-the-inadvertent-call-option/) 这样的权衡——原子互换中的第二方可以对互换采取行动或不采取行动，在一定时期内给予他们无意看涨期权。因此，本地验证主要用于跨链流动性协议，涉及每个链上独立存在的流动性池。

## 原生验证

本地验证是指跨链交互中的目的区块链验证源区块链的状态以确认交易，然后在自己的链上执行后续交易。这通常是通过在目标链的虚拟机中运行源链的轻型客户端或者并行运行它们来实现的。

本地验证依赖于诚实少数或同步假设，其中至少一个诚实中继者必须存在于委员会中(即诚实少数)，或者如果委员会失败，用户必须中继他们自己的事务(即同步假设)。本机验证是最信任最小化的跨链通信形式，但它更昂贵，提供的开发灵活性更低，并且更适合于具有类似状态机的区块链，例如以太坊和基于 EVM 的第二层网络之间，或者仅在基于 Cosmos SDK 的区块链之间。

# 跨链互操作协议(CCIP)

为了满足生态系统对区块链互操作性解决方案不断增长的需求，Chainlink 目前正在开发 [【跨链互操作性协议】(CCIP)](https://chain.link/solutions/cross-chain)—一种新的跨链通信开源标准，包括任意消息传递和令牌传输。CCIP 的目标是通过一个简单而优雅的界面在区块链网络之间建立一个通用的连接。此外，它的目标是在一个可编程令牌桥框架内集成各种其他 oracle 服务，以支持高度复杂的跨链交互。

考虑到越来越多的跨链攻击——去年大约损失了[](https://www.theblock.co/data/decentralized-finance/exploits)12 亿美元——一种安全第一的思维模式正在应用于 CCIP。它的开发得到了一些世界上最好的密码学和计算机安全专家的支持，包括 Ari Juels、Dan Boneh、Lorenz Breidenbach 和 Dahlia Malkhi。应用于 CCIP 的一些安全增强措施包括监控恶意活动的反欺诈网络、由一系列具有可验证的链上性能历史的高质量节点运营商进行的分散 oracle 计算，以及链外报告(OCR)协议，该协议已经在区块链主网上保护了数千亿美元。

要了解更多关于 Chainlink CCIP 的信息，请查看此博客[【https://blog . chain . link/introducing-the-cross-chain-inter operability-protocol-ccip/](https://blog.chain.link/introducing-the-cross-chain-interoperability-protocol-ccip/)。

![Chainlink CCIP](img/d772497be6b67e5ba023b26e26654c21.png)

<figcaption id="caption-attachment-3874" class="wp-caption-text">CCIP is a cross-chain messaging protocol powered by Chainlink decentralized oracle networks that plans to support a variety of cross-chain dApps, token bridges, and programmable tokens bridges.</figcaption>



# 通过区块链互操作性发展 Web3】

区块链互操作性是不断发展的 Web3 领域下一个前沿的重要组成部分。像 CCIP 这样的互操作性协议不仅可以帮助解锁在许多区块链中作为统一实体运行的复杂应用程序，还可以帮助企业、机构和政府从单一界面安全地访问任何链上环境。这两个功能将是开发下一代 dApps 的关键，这些 dApps 可以通过更传统的用户界面访问，从而加快 Web3 的采用率。

要了解更多关于 Chainlink 的信息，请访问 [Chainlink 网站](https://chain.link/) 并关注官方[Chainlink Twitter](https://twitter.com/chainlink)以了解最新的 chain link 新闻和公告。