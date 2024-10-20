# 什么是闪贷？

> 原文：<https://blog.chain.link/flash-loans/>

*更新于 2022 年 5 月 2 日。T3】*

快速贷款是一种无抵押贷款，允许用户在没有前期抵押的情况下借入资产，只要借入的资产在同一笔区块链交易中得到偿还。

[分散金融(DeFi)](https://chain.link/education/defi) 生态系统是通过为区块链重建传统金融服务，如借贷、交易所、期货和期权市场而开始的。随着生态系统的发展，全新的服务应运而生，这要归功于区块链技术的固有属性以及智能合约应用程序支持的 [无权限可组合性](https://blog.chain.link/defis-permissionless-composability-is-supercharging-innovation/) 。

就像概念中的[](https://chain.link/education/defi/yield-farming)一样，闪贷是一种令人兴奋的新型金融工具。闪贷使用户能够从链上流动性池中借入资产，无需前期担保，只要借入的流动性加上少量费用在同一笔交易中返回到池中。如果借款人没有在同一交易中偿还贷款，则整个交易被恢复，包括最初的借款和之后采取的任何行动。这一创新机制增加了用户在各种用例中获得资本的机会，同时确保基础链上流动性池的持续偿付能力。

在本文中，我们概述了快速贷款的工作原理、用途，以及 DeFi 协议可以做些什么来减轻这种新的金融工具带来的潜在攻击媒介。

## 闪贷如何运作？

在抵押贷款的情况下，借款人需要提供资本(抵押品)来借入资金。如果借款人未能满足贷款条件，贷款人仍然可以使用借款人的抵押品来支付贷款。闪贷没有这个要求；贷款只有在借款人在同一笔交易中偿还的情况下才能存在。因此，拖欠快速贷款是不可能的，因为整个交易将简单地恢复。

在很短的时间内——单笔交易的时间——快速贷款可以把任何人变成资金雄厚的演员。闪电贷款提供的数亿美元的流动性为套利、清算、抵押品互换和杠杆头寸创造了独特的机会。这也带来了一定的风险，尤其是对于一个新生的金融协议生态系统而言，这种生态系统具有不同程度的分散性和安全性。智能合约开发人员应该了解这些风险，以便为用户构建更健壮的应用程序。

## 闪贷是用来做什么的？

闪贷最常见的用途是套利。通过利用大量资本来填补市场中的低效率，一种资产在不同市场上有不同的汇率，套利者可以通过使市场达到平衡并改善 DeFi 市场中每个人的流动性来创造利润。

快速贷款的另一个使用案例是清算。许多贷款协议激励第三方清算人，他们可以通过清算未能满足特定抵押比率要求的贷款获得奖励。通过快速贷款获得大量资本有助于确保抵押不足的贷款按时清算，基础协议保持偿付能力。

快速贷款也可用于抵押品互换——一种用户用借来的资金结束贷款，然后立即用不同的资产作为抵押品开立新贷款的技术。快速贷款还可以简化创建杠杆头寸的过程，或者允许贷款跨协议无缝转移。

## 闪电贷款和价格甲骨文攻击

Flash loans 的声誉颇具争议，因为除了上述使用案例之外，它们还可用于资助对 DeFi 协议的各种类型的攻击。一旦漏洞被恶意行为者发现，攻击者就可以使用通过快速贷款获得的资本来操纵协议的某些功能，并在可能从其智能合同中耗尽资金的同时获利。此外，由于快速贷款交易会在失败时恢复，黑客不必将大量自己的资本置于风险之中来资助攻击。

这里需要注意一个重要的区别——快速贷款本身并不是问题，因为它们只是提供了一个资金来源。眼前的真正问题是协议中存在的漏洞，这些漏洞可能会通过闪贷资助的攻击暴露出来。从长远来看，快速贷款甚至可能有利于 DeFi 生态系统的安全，因为协议工程师必须考虑快速贷款通过提供大量流动性的即时访问可能发现的潜在攻击媒介。

虽然攻击的方法和范围经常不同，但通常被归因于快速贷款的攻击涉及操纵协议，该协议使用来自[分散交易所(DEX)](https://blog.chain.link/dex-decentralized-exchange/) 的现货价格作为其唯一价格 oracle。如[DeFi 智能合约数据质量的重要性](https://blog.chain.link/the-importance-of-data-quality-for-defi/) 中所述，从单一集中来源获取价格的协议很容易被资金充足的恶意行为者利用，他们可以通过一笔大额交易操纵市场。DeFi 协议通常寻求最大化其去中心化和审查阻力——集中式价格先知通过充当单点故障来破坏这一目标。

这是一个闪贷资助的攻击 DeFi 贷款协议的例子，使用基于 DEX 的现货价格作为其唯一价格 oracle:

1.  攻击者从一个支持闪贷的协议中借用了大量令牌 A。
2.  攻击者在一个 DEX 上用令牌 A 交换令牌 B(降低令牌 A 的现货价格，提高 DEX 上令牌 B 的现货价格)。
3.  攻击者将购买的令牌 B 作为抵押品存放在 DeFi 协议上，该协议使用来自上述 DEX 的现货价格作为其唯一的价格馈送，并使用操纵的现货价格来借入比正常情况下可能借入的更大量的令牌 A。
4.  攻击者使用借用令牌 A 的一部分来完全偿还原始快速贷款并保留剩余令牌，使用协议的操纵价格馈送来产生利润。
5.  由于 DEX 上代币 A 和 B 的现货价格被套利回真实的市场范围价格，DeFi 协议留下了不足抵押的头寸。



![Steps taken by a malicious actor during a flash loan price oracle attack](img/a7fcac4b9ced1ccd4460c059991086c8.png)

<figcaption id="caption-attachment-763" class="wp-caption-text">一次闪贷期间恶意行为人所采取的步骤价格甲骨文攻击</figcaption>





由于攻击者能够开立快速贷款并操纵 DeFi 协议用作其唯一现货价格 oracle 的交易所，攻击者能够提高用作抵押品的代币的报告价值，并降低用作债务的代币的报告价值。这使得攻击者能够借入比他们应该能够借入的更多的资金，从而形成了一个无法完全清算的头寸，因为抵押品的价值变得低于债务。这种攻击可能发生在单个事务中，但也可能在多个事务中重复多次，从而进一步造成损害。

此外，当用作价格馈送时，单个链上交易所也提供极其有限的市场覆盖，因为它们仅代表一个交易所的交易活动。这使得依赖于该指数现货价格的协议容易受到操纵价格点的影响，如果交易量转移到不同的交易所或资金充足的行为者临时操纵该交易所的价格。对于流动性较低的资产来说，风险尤其大，这些资产越来越多地被用作 DeFi 贷款协议中的抵押品。

考虑到这一点，这种类型的攻击完全可以通过分散的 [【甲骨文】](https://chain.link/education/blockchain-oracles) 解决方案以及适当的市场覆盖率来避免。

## 【Chainlink Oracles 如何防止闪贷攻击

[https://www.youtube.com/embed/ZiRCrSz1brc?feature=oembed](https://www.youtube.com/embed/ZiRCrSz1brc?feature=oembed)

为了产生全面的市场覆盖， [链式价格反馈](https://chain.link/data-feeds) 由分散的节点网络提供动力，这些节点网络不是从单一来源而是从多个独立的数据汇总公司汇总价格数据。这些数据聚合器跟踪所有流动性交易环境，包括集中和分散的交易所，以生成反映整个市场资产价格的交易量加权平均价格。这种数据聚合器通常还会考虑交易所之间的各种差异，并积极过滤市场异常值，如闪电崩盘和洗盘交易。

如果你想深入了解在 DeFi 协议中使用 Chainlink Price Feeds 的优势，请阅读[chain link Price Feeds 如何保护 DeFi 生态系统](https://blog.chain.link/chainlink-price-feeds-secure-defi/) 。

由于快速贷款只存在于单个链上交易的时间范围内，因此发生的任何操纵在交易结束时都会被还原。由于 Chainlink Price 从广泛的来源收集离线聚合价格数据，并在链上异步发布数据，因此 flash loans 对 oracle reports 中的聚合值没有影响。

为了防止与闪贷相关的价格 oracle 攻击，强烈建议智能合约开发商避免可操纵的 DEX 现货价格，而是利用 Chainlink 价格馈送作为其经验证的市场数据来源。这有助于确保 DeFi 协议始终获得一个反映市场范围内交易活动且闪贷无法触及的聚合价格点，从而缓解整个类别的 oracle 价格攻击媒介。



![Flash loans are ineffective against Chainlink Price Feeds](img/0c323153f83046aaeda9f6d8ce9a9b61.png)

<figcaption id="caption-attachment-764" class="wp-caption-text">闪贷对 Chainlink 价馈无效。</figcaption>





## 结论

快速贷款是 DeFi 中一种复杂的金融工具，它开启了复杂的金融应用，降低了新一波市场参与者的准入门槛。虽然 flash loans 已被用于资助对 DeFi 协议的攻击，但它们只是开发人员和用户可用的金融工具，它们不会产生漏洞，但会暴露协议中可能已经存在的漏洞，最常见的是 oracle 设计的错误价格。

Chainlink 是一个分散的 oracle 网络，有助于 DeFi 协议变得更加防篡改，特别是在获取实时市场数据的关键功能方面，这将触发其他 [Web3](https://chain.link/education/web3) 应用程序之间的其他交易级联。只有通过 [安全第一的方法](https://blog.chain.link/defi-security-best-practices/)DeFi 协议才能适应新的风险，保持信任，并可持续地扩展以吸引数十亿用户和数万亿美元的价值。

[![A clickable banner to a report detailing the Ultimate Guide to Blockchain Oracle Security](img/9ede9173a1fba83a6a8ec756c6b9e3a8.png)](https://chain.link/resources/blockchain-oracle-security)

<figcaption id="caption-attachment-3518" class="wp-caption-text">This guide gives a comprehensive breakdown on how to evaluate blockchain oracle security.</figcaption>



如果你是一名开发人员，想要快速将你的应用连接到 [Chainlink Price Feeds](https://data.chain.link/) ，请访问[开发人员文档](https://docs.chain.link/)并加入 [Discord](https://discordapp.com/invite/aSK4zew) 的技术讨论。如果想更深入的讨论整合，伸出 [这里](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog) 。