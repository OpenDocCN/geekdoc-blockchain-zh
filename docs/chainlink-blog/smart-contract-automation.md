# 智能合同自动化解释

> 原文：<https://blog.chain.link/smart-contract-automation/>

[智能合约](https://chain.link/education/smart-contracts) 的效用会随着时间的推移不断演变。智能合约的第一波浪潮被用于向区块链的代币发行和分配权利。后来，开发人员开始利用[Oracle networks](https://chain.link/education/blockchain-oracles)来创建 [混合智能契约](https://blog.chain.link/hybrid-smart-contracts-explained/) ，这些契约在链上应用程序中使用外部数据和链外计算来实现新的市场，如[【DeFi】](https://chain.link/education/defi)、动态[NFTs](https://chain.link/education/nfts)和 GameFi。现在，又一项基础设施脱颖而出——智能合同自动化。

本文将探讨智能合同自动化及其开启的可能性。我们首先定义智能合同自动化，并检查围绕自动化智能合同执行的关键安全性和成本考虑因素，然后强调智能合同自动化工具[chain link Automation](https://chain.link/automation)的优势，并展示 Web3 automation 解锁的各种用例。

如果你是一名开发人员，并且想要立即进入代码和技术组件，请跳到下面的初学者指南教程，或者访问 [Chainlink 自动化文档](https://docs.chain.link/docs/chainlink-automation/introduction/) 。

## 什么是智能合同自动化？

智能合同自动化允许开发人员以自动化的方式触发智能合同功能。这些可以包括收获产量，铸造 NFT，开始和停止游戏回合，触发清算抵押不足的贷款，等等。为了更好地理解智能合约自动化的广泛好处，让我们从它帮助开发人员克服的问题的角度来建立对智能合约自动化的工作理解。

### 问题:智能合约无法自动执行

智能合约是运行在[](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/)上的确定性程序。它们包含这样的代码:“如果 x 事件发生，那么触发 y 动作。”然而，智能合约不是自动执行的，这意味着它们的代码不会在区块链上运行和进行状态更改，直到被链上的事务触发。外部事务充当唤醒智能契约并启动其逻辑的“戳”,类似于单击鼠标可以启动计算机程序。

例如，一个基于区块链的贷款协议不能清算抵押不足的贷款，直到发生调用其清算功能的连锁交易。一旦调用，该协议的清算智能合同将通过参考链上的价格馈送来验证贷款是否抵押不足。如果抵押不足，用户的抵押品将被清算以偿还债务，否则，交易将恢复。

在某些用例中，最终用户通过他们自己的智能合约交互直接调用链上功能。例如，当用户想要在 [分散货币市场](https://blog.chain.link/decentralized-money-markets/) 中获得贷款时，他们以自己的抵押品借入代币的交易直接触发贷款发放功能的执行。该功能将确定用户的最大贷款规模，然后将借来的令牌转移到他们的地址。然而，在许多情况下，智能合约必须执行链上功能来维护协议的健康和效用，而没有直接的用户交互来触发它们。

### 解决方案:Chainlink 自动化即交易执行服务

“保管者”是 [外部拥有的账户](https://ethereum.org/en/developers/docs/accounts/) (EOAs)，其被激励以基于预定义的条件触发智能合同的执行。条件在作业中定义，并由开发团队、DAO 或协议用户提交给一个分散的网络，同时根据绩效给予奖励。智能合约自动化的条件通常基于时间(例如，美国东部时间每天下午 5:00 触发 x 函数)或事件(例如，仅当资产价格越过特定阈值时触发 y 函数)。

分散的自动化节点检查条件，并在那些预定义的条件得到满足时进行交易。该过程通常涉及节点使用离线计算来执行最终可能在链上调用的相同智能契约功能。一旦函数返回 true，那么节点通过发出链上事务调用链上函数。当调用该函数时，在状态发生变化之前，协议的智能契约可以在链上验证条件，这有助于确保节点是正确的。最终结果是，智能合约只在需要时，根据明确定义的条件，在区块链运行。

虽然自动化的目的相对简单，但为了理解诸如 Chainlink Automation 等工具的优势，了解一些关键的技术考虑因素是很重要的。

## 自动化智能合同执行的安全性和成本考虑

下面是在您的 dApp 中使用智能合同自动化工具时需要考虑的一些关键安全风险和成本因素。

### 手动开发和集中式服务器

一种类型的智能合同自动化实现包括在中央服务器上运行 Solidity cron 作业，或者让开发团队手动监控条件并进行链上交易。在这种设置中，自动化节点会成为一个集中的故障点，从而带来智能合同功能执行不及时的风险(例如停机或延迟)。在需要时不执行的智能合同可能导致不对称的利用和错失机会，如贸易下滑、协议破产和用户资金损失。

手动开发人员操作(DevOps)也对项目有限的时间和资源提出了要求，否则这些资源可以用于核心产品开发和生态系统扩展。随着时间的推移，手动开发操作也可能变得更加繁重，因为项目寻求通过智能合同自动化来简化用户体验并为其 dApps 添加高级实用程序。最终，智能契约需要端到端地去中心化，包括负责触发它们的执行的链外自动化基础设施。

### 昂贵且不可预测的奖金

设计智能合同自动化系统的另一种方法是提供奖金，当满足某些条件时，第一个调用链上函数的节点将获得经济奖励。虽然这种方法改进了集中式自动化模型，但它带来了成本效益、集中化和不可预测性方面的挑战。例如，在第一个分散自动化解决方案之一中使用的激励系统[以太坊闹钟](https://ethereum-alarm-clock.readthedocs.io/en/latest/index.html)，意味着交易有可能[根本不会被执行](https://ethereum-alarm-clock.readthedocs.io/en/latest/introduction.html#execution-guarantees)。

奖金的主要问题是，节点最终会直接参与争夺赢家通吃的奖励，从而引发优先天然气拍卖(PGA)竞标战。竞争节点将不断提高他们愿意支付的天然气价格，以激励矿工首先处理他们的交易。因为智能合约函数在其条件满足后只能被调用一次，所以只有第一个节点成功并获得工作报酬。每个其他节点都不成功，并且当其事务失败时会招致损失，因为没有发出对气体消耗的补偿。由于大多数自动化工作成本包括基础成本加上汽油费，PGA 导致最终用户的成本增加，他们必须支付更高的汽油费。

围绕公共奖金设计的智能合同自动化实施还会引发其他一些意想不到的后果。首先，PGA 会加剧区块链的网络拥堵，推高节点和网络中其他所有人的油价。此外，随着时间的推移，竞争可能导致节点数量自然减少，只剩下少数资金雄厚、提交激进天然气价格的参与者。集中式自动化网络通过减少监控和提交事务的节点数量来降低可靠性。

公共奖金的另一个风险是智能合同没有来自节点的提供及时服务的直接承诺。这带来了一定程度的不确定性，尤其是在市场极度波动和网络拥塞的时期，此时最需要自动化。例如，如果一小群竞争节点因为油价过高、天然气资金耗尽或忙于其他活动而没有及时采取行动，不清算有毒头寸的贷款协议可能会破产。

从这些设计中得出的结论是，自动化网络需要以经济高效、防篡改和高度可用的方式执行智能合同自动化。

## Chainlink 自动化:分散、低成本、可靠的智能合同自动化

项目可以将智能合同的执行外包给[](https://chain.link/automation)【chain link Automation】，这是一种分散的智能合同自动化工具，具有高度可靠性和激励一致性的良好记录，而不是依赖于集中式设置或在竞争性公共奖金上冒险。Chainlink Automation 已经在 Avalanche、BNB 链、以太坊和 Polygon 上运行，并支持未来添加更多链。

chain link 自动化服务的一些优势包括:

*   **激励性工作** —Chainlink Automation 提供了一个简单的框架，用户可以在其中清楚地概述分散的 Chainlink 节点网络所承诺的工作和奖励，消除竞争并创造可预测的财务激励。
*   **高正常运行时间** —Chainlink Automation 由相同的专业 DevOps 团队和企业运行，这些团队和企业在极端网络拥塞和市场波动期间拥有可验证的可靠性历史。Chainlink 自动化节点已经帮助其他 Chainlink 服务获得了 800 多亿美元的智能合同价值(例如， [价格反馈](https://data.chain.link/) )。
*   **低成本**
*   **分散执行** —Chainlink 利用分散且透明的节点池，为安全、及时的智能合同执行提供有力保障，节省团队时间，并减少人工干预或集中式服务器风险。
*   **增加效用** —Chainlink Automation 可以执行高级链外计算，并生成可通过智能合约验证的调用数据，允许开发人员构建高级功能，这在没有任何额外信任假设的情况下是不可能的。
*   **无缝集成** —Chainlink Automation 可以在几个小时内集成，以触发智能合同，为开发人员提供简单的文档和逐步安装指南。

## 智能合同自动化用例

以下是 Chainlink Automation 支持的众多 [智能合约用例](https://blog.chain.link/smart-contract-automation-use-cases-powered-by-chainlink-keepers/) 中的几个，包括流动性管理、DEX 限价单、动态 NFTs 等。还有许多其他的用例还没有被创建出来，等待着创新和有创造力的开发人员去开拓。

### 自动化产量收获和债务偿还

[Alchemix](https://alchemixfi.medium.com/alchemix-integrates-chainlink-keepers-for-vault-harvesting-and-launches-new-price-feeds-for-defi-34ff62a07b43) 是一种自我偿还的借贷协议，它集成了 Chainlink 自动化，以每天收获用户抵押品产生的收益。然后，收益用于偿还贷款产生的部分债务，无需任何人工输入或开发人员开销。

### 弹性供给代币的分散再基准

[【COTI】](https://u.today/chainlink-link-keepers-now-integrated-by-coti-networks-coti-cvi-design-details)正在使用 Chainlink Automation 对一个波动率令牌的供应进行基数调整，该令牌盯住了 UTC 时间每天午夜的[【CVI】](https://cvi.finance/)。这建立了更强的保证，即代币以完全分散的方式保持与基础 CVI 指数挂钩。

### 流动性准备金的最佳再平衡

[Visor Finance](https://medium.com/visorfinance/visor-finance-integrates-chainlink-keepers-to-automate-liquidity-provisioning-strategies-on-uniswap-2fd46a2bbcc7) 是 Uniswap v3 流动性提供商(LPs)的管理协议，旨在优化收益率回报。当超过某些预定义的阈值时，Visor Finance 使用 Chainlink Automation 将赚取的费用和新的资本存款再投资到活跃流动性头寸和单一资产限价单中 。最终结果是有限合伙人能够通过高效、及时的资本配置保持高资产利用率。

### 在特定事件发生时铸造限量版 NFTs】

[The Curse NFT](https://accursedshare.art/the-curse-nft/) 是一个动态的 NFT 艺术项目，根据 ETH 的价格运动，展示模特郑秀晶·肖特的正面或负面 3D 效果图。诅咒 NFT 正在使用 Chainlink Automation 来触发 NFT 展示其最终的“祝福”形式，如果 ETH 的价格曾经达到 20，000 美元。

### 基于时间的智能合同自动化

NFT 战略游戏 [行星九](https://blog.planetix.com/planet-ix-integrates-chainlink-keepers-to-help-automate-weekly-drawings-225154d5587a) 正在多边形上使用 Chainlink Automation 对其每周图纸进行基于时间的智能合约自动化。这有助于为用户提供更强的保证，即抽奖将准时开始和停止，不会中断。现在，开发人员可以使用 Chainlink Automation 创建雪崩、BNB 链、Fantom 或以太坊基于时间的智能合约。访问 [文档](https://docs.chain.link/docs/chainlink-automation/introduction/) 了解如何使用智能合同自动化触发交易。

### 开始、停止或结算游戏或回合

Chainlink Automation 可用于定期触发智能合约开始和结算功能，以帮助在预定义的时间间隔执行游戏或回合。如果没有智能合约自动化工具，开发人员将需要手动触发负责开始和停止回合的智能合约功能。

### 触发 DEX 限价单

分散的交易所需要智能合约自动化工具，使用户能够在平台上设置限价单，并解锁更无缝的用户体验。Chainlink Automation 可以监控链上条件，在达到某个价格时自动触发限价单。

### 自动化在线支付

chain link 自动化网络可以监控预定义的条件，并在满足这些条件时触发网上支付，从而帮助实现自动化的网上支付工作流程。

### 触发自动奖励分配

Chainlink 自动化节点可以根据预定义的时间表定期触发锁定或授权资产的释放，帮助项目利用透明的令牌授权机制。

### 分散货币市场的及时清算

Chainlink Automation 可以通过持续检查未结贷款的抵押率是否低于预定义的清算阈值，来监控分散货币市场上用户贷款的健康状况。如果用户的借款交易被发现抵押不足，Chainlink Automation 可以调用货币市场的清算功能，帮助确保协议保持偿付能力。

### 自动动态 NFT 更新

动态 NFT 响应于由神谕传达的外部数据而进化。当某些条件发生变化时，Chainlink 自动化网络可以触发动态 NFT 更新，并帮助解锁日益复杂的艺术项目、粉丝体验、游戏资产等。

### 自动化 DAO 治理流程

分散的治理流程通常需要手动执行，这给组织的管理带来了集中化风险。Chainlink Automation 可以通过自动触发库更新和贡献者支付、在链上传递链外治理投票等等，来帮助分散治理过程。

![Infographic showing the wide range of smart contract automation use cases enabled by Chainlink Keepers.](img/8e93399d4796e11cc53e2333cbbca166.png)

<figcaption id="caption-attachment-3971" class="wp-caption-text">Chainlink Automation enables a wide array of use cases including harvesting and auto-compounding yield, starting and stopping prediction rounds, setting limit orders, and more.</figcaption>



## 如何开始使用 Chainlink Automation 创建自动化 dApp】

[https://www.youtube.com/embed/-Wkw5JVQGUo?feature=oembed](https://www.youtube.com/embed/-Wkw5JVQGUo?feature=oembed)

跟随本 [技术指南](https://blog.chain.link/how-to-automate-smart-contract-execution-using-chainlink-keepers/) 学习如何使用 Chainlink Automation 实现智能合同的自动化。您将学习如何部署自动化兼容的合同，如何注册维护，等等。

如果您想立即开始构建混合智能合约应用程序，并且需要某种类型的外部数据或计算，请参考 [文档](https://docs.chain.link/docs/getting-started) 以了解如何触发智能合约功能，在[Discord](https://discordapp.com/invite/aSK4zew)中询问技术问题，或者 [与专家建立通话](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=homepage) 。

要了解更多，请访问[chain . link](https://chain.link/)，订阅 [Chainlink 简讯](https://chn.lk/newsletter) ，并关注 Chainlink 上的[Twitter](https://twitter.com/chainlink)，[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)，以及[Reddit](https://www.reddit.com/r/Chainlink/)。