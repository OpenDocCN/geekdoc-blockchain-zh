# 介绍链接提要注册表:链接价格提要的通用网关

> 原文：<https://blog.chain.link/introducing-the-chainlink-feed-registry/>

作为将任何区块链上的[智能合同](https://chain.link/education/smart-contracts)连接到外部数据资源的框架，Chainlink Network 通过增加新的特性和功能不断改善开发人员的体验。作为这一目标的延续，我们自豪地推出了 [链链接提要注册中心](https://docs.chain.link/docs/feed-registry/) ，这是一个将现有令牌合同地址映射到链链接价格提要的链上注册中心。因此，智能合约可以通过单个通用注册中心合约从任何 Chainlink 价格馈送中获取数据，从而大大减少了创建混合智能合约应用程序的集成工作。

作为智能合同开发人员高度要求的功能，Chainlink Feed Registry 使开发人员能够通过仅提供一对资产和面额地址来查询价格 Feed 的最新值，而无需知道每个 Feed 的单独合同地址。通过消除手动发现和单独连接到每个所需资产的价格馈送合同的需要，开发人员可以创建智能合同应用程序，该应用程序通过按需调用单个注册中心合同来检索任何受支持资产的最新价格。

这个新的注册中心提供了一个更直观、更简单的连接到 Chainlink 价格订阅源的体验，而以前的方法需要直接查询每个订阅源合同，包括在 [Chainlink 开发者文档](https://docs.chain.link/docs/ethereum-addresses/) 上过滤价格订阅源地址，或者通过提供字符串值使用 [以太坊名称服务](https://docs.chain.link/docs/ens/) 。重要的是，作为一个与区块链无关的 oracle 网络，Chainlink Feed Registry 合同将首先部署到以太坊区块链上，然后扩展到未来支持其他链上环境。

除了简化链式应用程序的开发之外，开发人员只需向单个智能合同提供一个令牌合同地址，就可以无缝跟踪价格源支持的任何和所有资产。这个过程可以在智能合约内部的链上完成，或者由开发人员通过调用区块链完整节点(包括自营节点)、区块链节点即服务提供商或可信块浏览器(如 Etherscan)来直接完成。此外，开发人员可以使用链上事件跟踪价格馈送合同的更新时间，从而提高透明度并简化跨前端 ui 常见的不同聚合器合同索引 Chainlink 事件的过程。

![Chainlink Feed Registry](img/2fe847851e9635b8b1012c2e5e8351b0.png)

<figcaption id="caption-attachment-2167" class="wp-caption-text">The Chainlink Feed Registry provides a universal gateway to Chainlink Price Feeds</figcaption>



## 支持链式智能合约的快速开发和部署

Chainlink Feed Registry 旨在为开发人员提供最顺畅、最直观的方式，通过一个通用网关将他们的智能合同应用程序连接到 Chainlink Price Feeds。因此，越来越先进的混合智能合约应用程序的创建速度可以显著提高。特别是，链接提要注册表为开发人员提供了许多关键特性。

### 减少集成工作

智能合同开发者不再需要创建他们自己的注册管理机构映射合同，因为他们现在可以利用 Chainlink Feed 注册管理机构来发现和验证正确的价格馈送地址。这减少了想要获取价格数据的开发人员的工作量，因为他们不需要单独发现和连接每个价格馈送契约，而是可以简单地将一对资产和面额地址馈送到单个链上注册中心契约。

```
latestRoundData(address base, address quote)
```

例如，要从以太坊 mainnet 上的 LINK/USD 价格提要中查询最新值，开发人员需要的唯一信息是 LINK token 契约地址和 USD 常量地址值。

```
// Defining the token contract addresses used
address LINK = 0x514910771af9ca656af840dff83e8264ecf986ca;

// Fetch the latest value from the LINK/USD Price Feed
(
 uint80 roundID,
 int price,
 uint startedAt,
 uint timeStamp,
 uint80 answeredInRound
) = FeedRegistry.latestRoundData(LINK, Denominations.USD);
```

这使得开发人员能够查询 Chainlink 价格提要，而不需要预先了解确切的提要合同地址。执行的唯一交互是对具有少量数据的单个智能契约的单个方法调用，当从任何 Chainlink 价格提要获取数据时，可以复制该方法调用。除了减少集成摩擦之外，对开发人员来说还有许多其他重要的好处。

### 跟踪支持的资产

作为价格馈送地址的全局索引，开发人员可以使用链式馈送注册表来发现他们的应用程序所运行的特定区块链网络上的特定资产对的价格馈送。当执行查询时，要么返回 Chainlink Price Feed 合同地址，要么返回零值，从而为特定区块链网络上可用的 Feed 的选择提供即时透明性。此外，注册中心简化了用链接数据创建子图的过程，因为注册中心事件可以被动态地索引到 HTTP API 中，以在前端用户界面中可视化所支持的资产。

由于链链接 Feed 注册完全存在于链上，这是一个抗审查的解决方案，开发者可以利用它来验证特定价格 Feed 及其相应的官方链上地址的存在。这提供了更大的安全保障，因为储存在区块链网络上的数据(如登记册)不能被任何外部方篡改或不经通知而更改。

### 跟踪价格源更新

因为每次更新底层聚合器契约时，链链接提要注册中心契约都会发出一个 FeedChanged() 事件，所以可以提醒用户注意任何价格提要升级，包括底层聚合契约到最新版本的变化，例如 [OCR](https://blog.chain.link/off-chain-reporting-live-on-mainnet/) 。 与 Feed Registry 提供的新一轮检查助手一起，这简化了跨不同聚合器契约版本索引 Chainlink 事件的过程。

通过为开发人员社区提供持续改善开发人员体验的功能，Chainlink 网络变得比以往任何时候都更容易集成，提供了多种方法，开发人员可以通过这些方法创建 chain link 智能合约应用。从减少从 Chainlink 价格源消费数据所需的集成工作到帮助协议通过令牌地址找到资产的正确源，Chainlink Feed Registry 旨在使 Chainlink 生态系统对所有参与者更加灵活和用户友好。

*通过访问 [开发者文档](https://docs.chain.link/docs/getting-started) ，加入关于 [不和谐](https://discordapp.com/invite/aSK4zew) 的技术讨论，或[联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog) ，立即开始使用 Chainlink 进行构建。获取现成可靠的解决方案 [价格供稿](https://feeds.chain.link/) 和 [可证明的随机性](https://blog.chain.link/chainlink-vrf-on-chain-verifiable-randomness/) 。*