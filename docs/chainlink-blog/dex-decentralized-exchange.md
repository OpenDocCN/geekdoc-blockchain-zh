# 什么是 DEX(分散交换)？

> 原文：<https://blog.chain.link/dex-decentralized-exchange/>

*最后更新:2022 年 11 月 1 日*

**DEX(去中心化交易所)是一个点对点的市场，用户可以以非托管的方式交易加密货币，而不需要中介来促进资金的转移和托管。**dex 用总部位于区块链的 [智能合约](https://chain.link/education/smart-contracts) 替代传统意义上的中介——银行、经纪商、支付处理商或其他机构，促进资产交换。

传统的金融交易是不透明的，通过中间人进行，而中间人对交易行为的了解极其有限，相比之下，dex 对资金的流动和促进交易的机制提供了完全的透明度。此外，由于用户资金在交易期间不会通过第三方的加密货币钱包，dex 可以降低交易对手风险，并可以降低加密货币生态系统中的系统性集中化风险。

dex 是 [去中心化金融(DeFi)](https://chain.link/education/defi) 的基石，并作为一个关键的“金钱乐高”，由于 [的无权限可组合性](https://blog.chain.link/defis-permissionless-composability-is-supercharging-innovation/) ，可以在此基础上构建更复杂的金融产品。    

[https://embed.theblockcrypto.com/data/decentralized-finance/dex-non-custodial/dex-volume-monthly/embed](https://embed.theblockcrypto.com/data/decentralized-finance/dex-non-custodial/dex-volume-monthly/embed)

*DEX 现货成交量的迅猛增长。( [来源](https://www.theblockcrypto.com/data/decentralized-finance/dex-non-custodial/dex-volume-monthly) )*

本文概述了分散交易所的工作方式、不同类型的 DEX，以及它们给加密货币生态系统带来的好处和风险。

## DEX 是如何工作的？

有几种 DEX 设计，每一种都在功能集、可伸缩性和分散性方面提供了不同的优势和权衡。最常见的两种是订单簿 dex 和[【AMMs】](https://blog.chain.link/challenges-in-defi-how-to-bring-more-capital-and-less-risk-to-automated-market-maker-dexs/)。DEX 聚合器也是一个广泛使用的类别，它解析链上的多个 DEX，以找到用户所需交易的最佳价格或最低汽油成本。

DEXs 的一个主要好处就是通过使用 [【区块链】技术](https://blog.chain.link/what-is-blockchain/) 和不可变的智能合约实现了高度的确定性。在比特币基地或币安等中央交易所(CEXs)，该平台使用交易所的内部匹配引擎来促进交易，而 dex 则通过智能合约和链上交易来执行交易。此外，dex 允许用户在交易期间通过自己托管的钱包保持对资金的完全托管。

DEX 用户通常需要支付两种费用——网络费和交易费。网络费用指的是链上交易的气体成本，而交易费用由底层协议、其流动性提供者、令牌持有者或协议设计所指定的这些实体的组合来收取。

许多 dex 背后的愿景是拥有无需许可即可访问的、端到端的链上基础设施，没有中心故障点，所有权分散到分布的利益相关者社区。这通常意味着协议管理权限由一个分散的自治组织(DAO)管理，该组织由一个利益相关者团体组成，该团体对关键的协议决策进行投票。

然而，在拥挤的 DEX 环境中保持协议竞争力的同时，最大限度地分散协议并不是一件容易的事情，因为 DEX 背后的核心开发团队通常能够比分散的利益相关者更明智地决定关键任务协议的功能。即便如此，许多 dex 还是选择了 [分布式治理](https://blog.chain.link/how-chainlink-powers-decentralized-governance/) 结构，试图增加审查阻力和长期弹性。

### 订单簿指数

订单簿——市场中未平仓买卖订单的实时集合——是电子交易的基础支柱。订单簿允许交易所的内部系统匹配买卖订单。

历史上，全链订单簿索引在 DeFi 中并不常见，因为它们要求将订单簿中的每一项交易都发布在区块链上。这要么需要比当前大多数区块链所能处理的更高的吞吐量，要么需要在网络安全性和分散性方面做出重大妥协。因此，以太坊上订单簿 dex 的早期例子具有低流动性和次优的用户体验。即便如此，这些交易所也是 DEX 如何利用智能合约促进交易的一个令人信服的概念证明。

随着可扩展性创新，如乐观汇总和 ZK 汇总等二层网络，以及更高吞吐量和特定于应用程序的区块链的推出，链上订单簿交换变得更加可行，现在吸引了大量的交易活动。此外，混合订单簿设计变得更加流行，其中订单簿管理和匹配过程在链外进行，而交易结算在链上进行。

一些流行的订单指数包括 0x、dYdX、Loopring 指数和 Serum。

### 自动做市商

自动做市商是使用最广泛的 DEX 类型，因为它们实现了即时流动性、流动性供应的民主化，并且在许多情况下，实现了任何令牌的无许可市场创建。AMM 本质上是一个货币机器人，总是愿意在两个(或更多)资产之间报价。AMM 不使用订单簿，而是利用一个流动性池，用户可以用代币交换代币，价格由基于代币在池中所占比例的算法决定。

由于资产管理系统总是能够为用户报价，因此可以在流动性较低的市场中即时获得流动性。在订单簿 DEX 的情况下，有意愿的买家必须等待他们的订单与卖家的订单匹配——即使买家将他们的订单张贴到接近当前价格的订单簿的“顶部”,订单也可能永远不会执行。

在 AMM 的情况下，汇率由智能合约决定。用户可以立即获得流动性，而流动性提供者(AMM 流动性池的储户)可以通过交易费获得被动收入。这种即时流动性和民主化流动性供应的结合使得通过 AMMs 推出的新代币激增，并解锁了专注于不同用例的新设计，如 [稳定币](https://blog.chain.link/what-are-stablecoins/) 互换。如果你想更详细地探索 AMMs，请阅读这篇文章，内容涉及 AMMs 如何工作。

虽然目前大多数 AMM 设计都处理加密货币，但 AMMs 也可以用于促进[【NFT】](https://chain.link/education/nfts)、令牌化现实世界资产、碳信用等的互换。

一些流行的 AMM 指数包括 Bancor、Balancer、Curve、PancakeSwap、Sushiswap、Trader Joe 和 Uniswap。

## 分散交流有什么好处？

由于确定性智能合约促进了 DEX 交易，因此它们具有强大的保证，即它们将完全按照用户预期的方式执行，而无需集中各方的干预。与传统金融市场中不透明的执行方法和潜在的审查相比，dex 提供了强有力的执行保证，并增加了基本交易机制的透明度。

在这段视频中，Chainlink 的联合创始人 Sergey Nazarov 讨论了对加密强制保证的需求如何增加了对分散式基础设施的需求:  

[https://www.youtube.com/embed/D30NUjn_3Es?feature=oembed](https://www.youtube.com/embed/D30NUjn_3Es?feature=oembed)

由于不涉及托管人，用户可以使用自己托管的钱包参与，dex 降低了交易对手风险。通过减少集中在少数集中交易所钱包中的资本数量，dex 还可以降低区块链行业的一些系统性风险。2014 年，Mt. Gox 集中交易所处理了所有比特币交易量的很大一部分，后来由于数十万比特币的损失而突然停止运营。

dex 还有助于提高金融包容性。虽然存在特定用户界面基于地理位置或其他因素限制访问的情况，但访问 DEX 的智能合约只需要互联网连接和兼容的自托管钱包。由于用户可以使用他们的钱包地址以直接的方式登录，因此与集中式交换相比，DEX 的入职流程是无缝的，并且几乎是即时的。

## DEX 风险和考虑事项

通过强有力的执行保证、更高的透明度和无许可访问，dex 已经实现了交易和流动性供应的民主化。然而，dex 也带有一系列风险，包括但不限于:

 ***   **智能合约风险**—区块链被认为是执行金融交易的高度安全的地方。然而，智能合约的代码质量仍然依赖于开发团队的技能水平和经验。智能合约错误、黑客攻击、漏洞和利用可能会发生，使 DEX 用户容易遭受资金损失。开发人员可以通过安全审计、同行评审的代码和可靠的测试实践来减轻这种风险，但是始终需要勤奋。
*   **流动性风险**—尽管 DEX 越来越受欢迎，但一些 DEX 市场的流动性状况不佳，导致大量滑点和次优的用户体验。由于流动性的网络效应(高流动性吸引更多的流动性，低流动性吸引更少的流动性)，交易活动的很大一部分仍在集中交易所进行，这往往导致 DEX 交易对的流动性减少。
*   **抢先风险**—由于区块链交易的公开性质，DEX 交易可能会被套利者或 [最大可提取价值(MEV)](https://blog.chain.link/what-is-miner-extractable-value-mev/) 机器人抢先，试图从不知情的用户那里攫取价值。与传统市场的高频交易者类似，这些机器人试图通过支付更高的交易费用和优化网络延迟来利用普通用户的 DEX 交易，从而利用市场的低效率。
*   **集权风险**——虽然许多 dex 的目标是最大化他们的分权和审查阻力，但集权点仍然存在。其中包括托管在集中式服务器上的 DEX 匹配引擎、对 DEX 智能合同拥有管理权限的开发团队，以及使用低质量令牌桥接基础设施等。
*   **网络风险**
*   **代币风险**—由于许多 dex 的特点是无许可的市场创建——任何人都可以为任何代币创建市场——购买低质量或恶意代币的风险可能高于集中交易。DEX 用户需要考虑参与早期项目的相关风险。

除此之外，一些用户可能会发现完全保管他们的私钥是一个令人望而生畏的前景。虽然完全控制自己的资产是 [Web3](https://chain.link/education/web3) 愿景提供的主要好处之一，但许多用户可能更喜欢让第三方受托保管他们的资产。然而，遵循良好的 [安全性](https://blog.chain.link/defi-security-best-practices/) 和密钥管理实践可以让更多用户享受到保持对其资产的完全控制的好处，同时访问开放源代码金融服务的复杂生态系统。

## dex 如何使用 Chainlink 帮助提高安全性和解锁高级功能

dex 可以使用 chain link[Oracle](https://chain.link/education/blockchain-oracles)服务来提高其协议的弹性，并从集中式基础设施中引入用户可能熟悉的高级功能。

[chain link Price Feeds](https://data.chain.link/)提供关于加密货币、商品、外汇、指数等的准确、安全、可靠的金融市场数据，并帮助保护整个多链生态系统中数百亿美元的 DeFi 应用。使用 Chainlink 分散式 oracle networks，dApps 能够以简单、安全和分散的方式检索链外价格数据，并根据该数据执行操作。

DEX 协议可以使用 Chainlink 价格馈送进行可靠的价格转换，在前端准确显示价格，或者安全计算[](https://blog.chain.link/what-is-staking/)对利益相关者的奖励和费用分配。对于涉及保证金或期货合约的 dex，价格反馈有助于确保抵押资产的正确定价和清算的准确处理。

dex 还可以将 Chainlink 价格馈送用作额外的支持，以提高其协议对异常市场事件的弹性，这是一种经过战斗考验的价格数据源，有助于防范异常市场事件。安全的价格基础设施还可以帮助确保价格监控和金融分析基础设施的安全性和准确性，并帮助创建和管理不同分散交易所之间的套利策略。

[chain link Automation](https://chain.link/automation)，一种分散化的自动化解决方案，也在 DeFi 生态系统中广泛使用，以支持通过端到端 [智能合约自动化](https://blog.chain.link/smart-contract-automation/) 引入复杂功能。Chainlink Automation 使用分散且可靠的链外计算来监控用户定义的条件，然后在满足这些条件时调用链上函数。

当资产价格越过预定义的价格点时，Chainlink Automation 可以触发限价单，使交易者能够对其投资组合进行更精细的控制，并节省开发团队的时间和资源，然后他们可以将这些时间和资源用于改进其协议的核心业务逻辑。Chainlink Automation 也可用于可靠地执行交易费用和赌注奖励的定期分配。

## 结论

dex 是加密货币生态系统的基础支柱，让用户以点对点的方式交换数字资产，而无需中介。在过去几年中，由于 dex 可以为新推出的代币提供即时流动性，无缝的入职体验，以及它们提供的交易和流动性供应的民主化途径，dex 的采用率越来越高。

大部分交易活动是否会转移到 DEX，以及当前的 DEX 设计是否会支持长期增长和[](https://blog.chain.link/chainlink-enterprise-blockchain-middleware/)【机构采用】还有待观察。然而，dex 预计仍将是加密货币生态系统的重要基础设施，并将继续在交易可扩展性、智能合约安全性、治理基础设施和用户体验方面得到改善。

如果你是一名 DeFi 开发者，想要集成 Chainlink，请查看我们的 [文档](https://docs.chain.link/) ，在[Discord](https://discord.com/invite/aSK4zew)中提问，或者 [与专家建立通话](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=homepage&typeform-source=blog.chain.link) 。

## 附加资源

*   [什么是 DeFi(去中心化财政)？T3】](https://chain.link/education/defi)
*   [什么是智能合约？T3】](https://chain.link/education/smart-contracts)
*   [什么是稳定点？T3】](https://blog.chain.link/what-are-stablecoins/)
*   [什么是产量耕作？T3】](https://chain.link/education/defi/yield-farming)**