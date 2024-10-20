# 为智能合约生态系统构建面向服务的架构

> 原文：<https://blog.chain.link/service-oriented-architecture-for-smart-contracts/>

面向服务的架构(SOA)是一种软件设计方法，它使不同的、独立维护的组件或“微服务”能够在单个应用程序中协同工作。这种服务分离加速了创新，减少了开发时间，并解释了 [DeFi](https://chain.link/education/defi) 生态系统中持续增长的原因，在该生态系统中，多个无许可的开源协议被组合利用来组成全新的金融应用程序。当人们谈论 DeFi composability 时，在许多方面，他们都在谈论智能合约[的面向服务的架构。](https://chain.link/education/smart-contracts)

Chainlink 的联合创始人 Sergey Nazarov 最近解释了 Chainlink 网络如何适应更大的区块链生态系统的新兴面向服务的架构，为智能合同应用程序提供高度可靠的微服务，如安全数据馈送、可证明随机数生成、[储备证明](https://chain.link/proof-of-reserve)和其他链外计算。作为智能合约的安全数据基础设施，Chainlink 也是许多传统公司将其后端系统连接到快速增长的智能合约经济的门户，并将分散的微服务集成为市场买卖双方商业模式的一部分。

这篇文章摘自 Sergey 最近在 2020 年 Coindesk Invest: Ethereum 会议上的演讲[DeFi 智能合约中可组合性的力量](https://www.youtube.com/watch?v=rJIH8uISyNA&feature=youtu.be)。

[https://www.youtube.com/embed/rJIH8uISyNA?feature=oembed](https://www.youtube.com/embed/rJIH8uISyNA?feature=oembed)

* * *

## 面向服务的架构的好处

我们的生态系统的一个关键转变已经开始，将是向更加面向服务的架构(SOA)的转变，在 SOA 中，协议可以非常高效和安全地组合服务。这也是标准计算架构的发展方向。整体架构是封闭的系统，人们不能与另一个系统组合在一起，因此进入该系统的所有工作只是为了它自己的利益，而不是可以被其他人重用的东西。然后，你有一个微服务，或面向服务的架构，方法，它允许人们制作多个独立的服务，然后以安全和非常有用的方式进行交互。



![Microservices architecture enables composable application components for web applications.](img/c894ba0ee504e004843d3ca77c2b4dc1.png)

<figcaption id="caption-attachment-1461" class="wp-caption-text">微服务架构为 web 应用提供可组合的应用组件。</figcaption>





当我们寻求在[去中心化金融(DeFi)](https://blog.chain.link/analyzing-the-defi-ecosystem-and-the-many-ways-chainlink-can-accelerate-adoption/) 中创建可组合性时，这确实是我们的生态系统试图实现的目标。这是一种非常常见的动态，更大的计算环境已经趋向于这种动态。在面向服务的体系结构出现之前，您有这些大型应用程序，它们存在于这些数据库大型机中，并且它们都以某种有限的方式交互。让他们一起工作真的很难。有一种向面向服务架构的转变，最初只是通过提供不同的服务，然后是微服务，然后是无服务器方法。

这确实是智能合约生态系统的逻辑发展方向。面向服务的架构通过分离不同的关注点，改善了您对安全性的假设。您还可以获得服务的可重用性，因此任何人在这些服务上投入的努力都会使它们对其他人有用，这些服务的组合允许快速迭代，这种方式在更单一的应用程序类型的结构中是无法实现的。



![SOA increases security and reusability, while enabling faster, more iterative product development.](img/3c82aa9f5992ad6240c64bda12a4972b.png)

<figcaption id="caption-attachment-1460" class="wp-caption-text">SOA 增加了安全性和可重用性，同时支持更快、更迭代的产品开发。</figcaption>





## 定义可组合性:智能契约的有效 SOA

我们空间中的相似之处正慢慢开始出现。当我回顾智能合约的历史时，在计算世界中这并不是很长的历史，我们已经有了像 DAO 这样更完整的智能合约的例子，它们是以这些大块的形式编写的，最终并不安全，因为它们是以这种僵硬的、不可组合的格式编写的。这些早期的智能合同系统中有许多并不是真正可用的，或者被其他人制造成可用的。

现在，我们正从围绕单一资源的体系结构转变为一种封闭的体系结构，这种体系结构可能以一种非常堆叠、非常复杂的方式构建，其中隐藏着许多问题，我们正转向一种动态的体系结构，在这种结构中，我们有多个较小的服务在一个协议内交互。并且该协议中的那些独立服务实际上可以被其他协议使用。



![Recent developments in composable services-oriented smart contracts have led to a boom in DeFi products — Chainlink provides composable secure data to power this ecosystem.](img/50349b5eb6b76a992b950ca44999c975.png)

<figcaption id="caption-attachment-1459" class="wp-caption-text">可组合的面向服务的智能合同的最新发展带来了 DeFi 产品的繁荣——chain link 提供可组合的安全数据来推动这一生态系统。</figcaption>





Chainlink 通过为这些不同的协议和服务提供安全数据，适合这个更大的体系结构。现在，你可以看到由 Aave 和 Synthetix 等优秀团队开发的各种高级 DeFi 协议正在被整合到越来越多的高级产品中，共享价值和功能。

这就是我真正认为 DeFi composability 将为我们所有人实现的目标:DeFi 现在发展如此之快的部分原因是因为我们的生态系统已经采用了在软件行业中被证明有效的 SOA 思想。这就是我们如何组合一堆服务并构建一些伟大的东西。

## Chainlink 如何加速智能合约的可组合性

面向服务的架构在我们的领域变得越来越流行，这使得开发团队可以更容易地以 DeFi 协议契约的形式添加新的组件，其他人也可以更容易地将价值注入这些契约中。像 [Chainlink Price Feeds](https://chain.link/solutions/defi) 、 [VRF](https://blog.chain.link/chainlink-vrf-now-live-on-ethereum-mainnet/) 、 [Proof of Reserve](https://blog.chain.link/chainlink-proof-of-reserve-bringing-transparency-to-defi-collateral/) 和[Oracle](https://chain.link/education/blockchain-oracles)这样针对[天气数据](https://arbolmarket.medium.com/businesses-and-farmers-can-now-hedge-weather-risk-through-the-arbol-platform-and-chainlink-data-d6f36506146c)等独特数据集的服务有助于确保这些合同，提供附加值，并提供新形式的真实世界抵押品。

我认为，未来 DeFi 项目的可组合性将以智能合约的形式开启新的服务，并产生新的金融产品，如可能作为 DeFi 抵押品的游戏产品。Chainlink 为人们提供了一个基础设施，通过运行他们自己的 Chainlink 节点或使用 Chainlink 作为中间件，将他们现有的数据和 API 出售给 DeFi、分散保险和区块链博彩业，从而轻松地将服务放到链上。

我们越快支持更多的链上微服务，越快实现不同的、可组合的构建块的生态系统，我们的行业就越像 web 行业，并开始以 web 速度构建。



![Chainlink provides SOA for secure price feeds, RNG, and any other type of external data.](img/17685d2b74e0a58ae104c6c78f89b922.png)

<figcaption id="caption-attachment-1458" class="wp-caption-text">Chainlink 为安全的价格馈送、RNG 和任何其他类型的外部数据提供 SOA。</figcaption>





## 围绕数据使用和安全性创造良性循环

我认为真正的挑战是，如何以一种安全的方式构建这些可组合的构建块，将安全问题从需要构建的人那里抽象出来？

从正在构建的开发人员的角度来看，您需要速度，并且您还希望为他们提供一个系统，在他们快速地将这些不同的构建块组合在一起时，该系统能够保证一定级别的安全性。

我们实际上看到了一个循环动态，随着更多智能合同的出现，这些服务、数据和 DeFi 协议的使用越来越多，这鼓励了更多数据和更多服务被放在链上。这是 Chainlink 密切参与和推动的一种动态。我们看到了一个循环模式，其中有一个将更多数据放在链上的市场，因此这将支持更多的 DeFi 市场，以及随后更多的 DeFi 智能合同，可以组合成更多的产品和服务。



![Virtuous cycles around Chainlink providing more on-chain data and oracle security, which drives increasingly more smart contracts that secure more value.](img/43c8e16b218cdb2449e25ac6043fbc6e.png)

<figcaption id="caption-attachment-1457" class="wp-caption-text">围绕 Chainlink 的良性循环提供了更多的链上数据和 oracle 安全性，这推动了越来越多的智能合同，从而确保了更多的价值。</figcaption>





我们看到的另一种模式是，人们倾向于为安全付费，因此随着这些智能合同的用户费用开始增长，并进入像 Chainlink 这样的系统，这些用户费用为更多的数据和更多的安全付费，你将到达一个出现循环模式的地方。更智能的合同会产生更多的数据使用和更多的数据需求，然后像 Chainlink 这样的系统通过直接从高质量数据源购买数据，以签名格式安全地提供数据。

Chainlink 加速了这些围绕数据消费和安全性的循环，在加速这种良性循环的过程中，智能合约生态系统获得了更多服务，以组合到 DeFi 智能合约中，包括数据的多样性、数据的质量以及数据交付的安全保证。

* * *

开发人员，查看 Chainlink 的[技术文档](https://docs.chain.link/)，快速开始使用 Chainlink oracles 和一系列用于智能合同的分散式微服务。为了更深入的整合，[联系我们的专家](https://chainlink.typeform.com/to/gEwrPO)。

### 关于这个话题的更多信息

*   [DeFi 的无权限组合是增压创新](https://blog.chain.link/defis-permissionless-composability-is-supercharging-innovation/)
*   [77 个由 Chainlink 支持的智能合约用例](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/)
*   [智能合同如何减少保险行业的信息不对称](https://blog.chain.link/blockchain-insurance/)