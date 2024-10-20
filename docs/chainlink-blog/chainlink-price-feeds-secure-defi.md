# Chainlink 价格馈送如何保护 DeFi 生态系统

> 原文：<https://blog.chain.link/chainlink-price-feeds-secure-defi/>

[chain link Price Feeds](https://data.chain.link)于 2019 年初上线，以满足智能合约开发商不断增长的需求，构建 [DeFi 应用](https://chain.link/use-cases/defi) 要求在区块链网络上访问安全、准确、实时的金融市场数据。此后，Chainlink Price Feeds 已经发展成为价格预测的行业标准解决方案，超过 900 个分散的 oracle 网络正在生产中运行，这些网络共同帮助众多区块链和第 2 层网络中的数百个 DeFi 应用获得了数百亿美元的资金。链式 DeFi 应用包括 Aave、本齐、Compound、dYdX、Frax、Liquity、Sushi、Synthetix 等等。

本帖将深入探讨 chain link Price feed 如何保护 DeFi 生态系统，首先探讨 DeFi 为什么需要 oracles，然后概述 chain link Price feed 的七个主要优势，这些优势导致其采用率呈指数增长。

## **DeFi 神谕简介**

在短短几年内， [【去中心化金融(DeFi)](https://chain.link/education/defi)——一个基于区块链的金融应用生态系统——已经从 [区块链技术](https://blog.chain.link/what-is-blockchain/) 的小众用例转变为全球增长最快的行业之一。目前，DeFi 的总价值已经超过了 2000 亿美元，这是一个跟踪存放在 DeFi 应用程序中的所有加密资产总和的指标。

大多数 DeFi 应用程序中存储的加密资产的安全性的先决条件是访问金融市场数据。例如， [货币市场](https://blog.chain.link/decentralized-money-markets/) 需要实时资产价格来准确地发行和清算抵押贷款，而 [算法稳定器](https://blog.chain.link/what-are-stablecoins/) 需要当前资产价格来可靠地自动管理其货币政策。然而，对于 DeFi 应用程序来说，获取金融市场数据是很困难的，因为区块链本质上是与外部世界断开的，并且大多数高质量的金融市场数据是在区块链环境之外生成的(即，离线)。区块链和链外系统之间缺乏连接通常被称为“ [oracle 问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/) ”

克服 oracle 问题需要使用被称为“[【Oracle](https://chain.link/education/blockchain-oracles)”的安全中间件，它为区块链提供对离线数据和服务的访问。Oracles 对于 DeFi 来说是必不可少的，最显著的原因是它们支持链上的 **价格馈送** ，使得 DeFi 应用程序在执行关键功能时能够立即获取各种加密或真实资产的当前或历史价格。因为来自价格源的数据决定了 DeFi 应用程序采取的操作，所以它们是被利用的目标，不安全的价格预言已经造成了价值数千万美元的损失。因此，为了保护 DeFi 生态系统中的数十亿美元，需要安全的价格先知。

## 【DeFi 的链节价格馈送

[https://www.youtube.com/embed/-pJqlI61ZKc?feature=oembed](https://www.youtube.com/embed/-pJqlI61ZKc?feature=oembed)

Chainlink 价格馈送是链上 [参考合同](https://docs.chain.link/docs/reference-contracts/) ，由包含 Chainlink 节点的分散 oracle 网络(don)自动更新。每个参考合约以汇率(例如 BTC/美元)的形式存储资产的最新和历史价格，然后智能合约可以按需查询这些价格。每个 Chainlink 价格馈送都在特定的区块链网络上运行，并根据预定义的参数定期更新新数据。

为了全面了解 Chainlink 价格源是如何保护和操作的，让我们来探索一下它们的七个有助于保护 DeFi 生态系统的独特属性。

### 1。多层分散和高质量数据

Chainlink 价格馈送保持高水平正常运行时间和数据质量的主要方法之一是使用多层分散聚合系统。这种架构减少了单点故障，有助于确保每份 oracle 报告反映真实的市场资产价格。价格源的聚合架构有几个步骤。

![Chainlink Price Feed Aggregation](img/dde984517434dd5d85358cd271fcb545.png)

<figcaption id="caption-attachment-3690" class="wp-caption-text">Multiple layers of decentralized aggregation in Chainlink Price Feeds.</figcaption>



#### 数据源聚合

首先，在数据源级别聚合数据。原始市场数据由集中交易所(如比特币基地、币安、北海巨妖)和分散交易所(如 Uniswap、Curve、PancakeSwap)的各种集合作为交易活动的结果产生。

专业数据整合公司(如 CoinMarketCap、CoinGecko、Tiingo)从各交易所收集原始市场数据，并计算精确的定价数据集。更具体地说，细化过程包括生成一个交易量加权平均价格(VWAP)，将每个交易所的数据平均在一起，但根据交易量按比例加权。数据聚合器通常还会考虑交易所之间的各种差异，如市场深度、延迟和价差，并过滤掉市场异常，如闪电崩盘、洗盘交易和其他异常值，以便它们不会影响最终的聚合数据点。

结果是每个数据聚合器提供一个覆盖整个市场的数据点——一个反映所有交易环境的精确聚合的价格，而不是一小部分市场，后者可能是不准确的。数据聚合器还使用类似的方法为其他资产类型(如法定货币、大宗商品和股票)生成精确的价格数据。然后通过 [应用编程接口(API)](https://blog.chain.link/understanding-how-data-and-apis-power-next-generation-economies/) 提供该价格数据，通常通过付费订阅计划，这意味着数据聚合者有明确的财务动机以 [服务级别协议(SLA)](https://www.bearer.com/resources/what-is-sla-service-level-agreements-and-how-to-find-them)的形式维护准确的数据和高 API 正常运行时间。

#### 节点运算符聚合

接下来是节点操作符级别的聚合。支持价格馈送的每个 Chainlink 节点被配置为与多个高级数据聚合器的 API 连接，包括通过对凭证管理的本地支持的密码保护的 API。然后，当需要新的价格更新时，每个 Chainlink 节点从多个数据聚合器获取数据，并以中值作为响应。因此，每个单独的 Chainlink 节点通过自动删除数据异常值和防止数据聚合器的意外 API 停机来提供增强的弹性。

#### 甲骨文网络聚合

最后是 oracle 网络聚合。多个独立的 Chainlink 节点组合在一起，形成一个分散的 oracle 网络(DON ),该网络定期生成包含每个节点的单独观察值(中间化价格点)和签名(加密证明)的聚合 oracle 报告。由 DON 生成的 oracle 报告随后被链存储在特定数据集的相应参考智能合约中(例如以太坊上的[【BTC/美元参考合约】](https://data.chain.link/ethereum/mainnet/crypto-usd/btc-usd) )。每次在链上发布 oracle 报告时，在将所有响应的中间值不变地存储在引用契约中之前，都会验证每个节点签名的完整性。

为了保持高水平的防篡改性，DON 中至少三分之二的节点必须贡献他们的观察结果和签名，以使新的 oracle 报告在链上被接受。这可以防止任何单个节点或一小组节点破坏最终存储值或在链上发布不完整的报告。此外，由于最终中值是在 oracle 报告发布后获取的，因此至少有一半的响应节点必须被破坏，才能影响链上存储的最终值并使其对合同可用。

![The data aggregation pipeline of Chainlink Price Feeds](img/6a8d0f83f06a0ad12eda0f4a216851b5.png)

<figcaption id="caption-attachment-4937" class="wp-caption-text">The data aggregation pipeline of Chainlink Price Feeds.</figcaption>



Chainlink 在数据源、节点运营商和 oracle 网络级别的多层聚合策略有助于确保 Chainlink 价格反馈的每次更新都反映了一个经过彻底提炼的数据点，并高度准确地反映了资产的市场价格。

有关 Chainlink Price Feeds 如何保持持续高水平的数据质量的更多信息，请参考这篇深入的文章:[DeFi 智能合约的数据质量](https://blog.chain.link/the-importance-of-data-quality-for-defi/) 。

### 2。高质量、超可靠的 Oracle 节点运营商

每个 DON 由地理上分散的一群具有抗 Sybil 能力、经过安全审查的 [节点运营商](https://blog.chain.link/what-is-a-chainlink-node-operator/) 运营，他们在运营关键任务基础设施方面经验丰富。节点运营商跨云服务和自托管裸机基础设施运行 [Chainlink 节点软件](https://github.com/smartcontractkit/chainlink) 。Chainlink node 软件是开源的，麻省理工学院许可的，安全审计的，并且在 mainnet 运行时经过了多年的考验。

![Chainlink Node Operators](img/e9690755693371a53925334243dbb8fe.png)

<figcaption id="caption-attachment-3692" class="wp-caption-text">Node Operators run Chainlink nodes which are grouped into Oracle Networks.</figcaption>



为 Chainlink 价格反馈提供动力的节点运营商来自不同的背景和行业，他们拥有丰富的经验和专业知识，能够安全可靠地将市场数据汇总并传送至区块链。一些主要类型的链环节点操作符包括:

 ***   **DevOps nodes:** 专门运营区块链基础设施的组织，如证据验证器、工作证据挖掘池和全节点 RPC 提供商。这些运营商在运行重要的 Web3 基础设施、管理加密私钥以及收取加密货币作为服务报酬方面拥有丰富的经验。DevOps 节点包括 Stake 等领先的 PoS 赌注池提供商。Fish、P2P 验证器、Staked 等等。
*   **企业节点:** 世界各地目前为传统 Web2 经济运营后端基础设施的机构。其中包括全球电信提供商，如德国电信的 T-Systems 和瑞士电信，以及其他全球性机构，如 LexisNexis。
*   **社区节点:** 来自 Chainlink 社区的组织，专注于支持生态系统的发展，并已证明具有高度的可靠性。这包括 [Chainlink 甲骨文奥林匹克](https://chain.link/oracle-olympics) 、CryptoManufaktur、LinkRiver、西北节点的获胜者。

Chainlink node 运营商还包括 Huobi 等加密货币交易所、Tiingo 等数据提供商、Kyber 等 DeFi 应用程序，以及各种各样的其他参与者。通过汇集经验丰富、动机一致的基础设施提供商，Chainlink Price Feeds 为智能合同开发商提供了高水平的保证，即数据将以特定的时间间隔或更新频率一致地在链上交付。

### 3。经济高效且分散的数据交付

为了平衡对准确市场数据的需求与将此类数据引入供应链的相关成本，Chainlink 价格馈送在 oracle 报告何时以及如何在供应链上交付方面具有高度的可配置性。特别是，有两个触发参数用于确定新的 oracle 报表何时在链上发布:

*   **偏离阈值** :资产价格与上次更新相比的百分比变化。例如，如果某项资产的全球价格自上次链上更新以来上涨或下跌 0.05%，0.05%的偏差阈值将触发 oracle 更新。
*   **心跳** :自上次更新后经过的时间。例如，如果自上一次链上更新以来至少过去了一分钟，则一分钟的心跳将触发更新。

这些触发参数通常是分层的，因此，在市场波动期间，价格馈送的更新频率较高，以获得更好的准确性，但在市场波动较低时，价格馈送的更新频率较低，以降低成本。每个触发参数都是基于许多因素设置的，包括市场需求、担保价值、接收区块链的天然气成本、特定用例要求、资产的预期市场波动性等。

高吞吐量链通常可以支持更快的更新频率，因为 Chainlink 可以以每个区块链的本地速度和成本运行。在成本较高的区块链，优化成本降低对长期经济可行性至关重要，并确保即使在网络极度拥挤的情况下，oracle 报告也能在链上发布。这是 2021 年初更新 Chainlink 价格馈送以支持 [离链报告](https://blog.chain.link/off-chain-reporting-live-on-mainnet/) (OCR)协议的主要原因。Chainlink OCR 利用链外计算和点对点网络将运营成本降低高达 90%，与 OCR 推出之前相比，链上交付的数据量增加了 10 倍。

Chainlink OCR 允许节点在链外将它们的响应汇总到一个 oracle 报告中，而不是每个 chain link 节点在链内将它们对每次更新的响应作为一个单独的交易，并支付相关的汽油费用。然后，该 oracle 报告将在单个事务中进行链内交付，在该事务中，每个节点的签名将被单独验证，所有观察值的中值将被存储。这不仅降低了运营成本，还支持更大程度的节点分散、更快的更新频率、更短的更新延迟以及进一步的 oracle 计算定制。

更多关于 OCR 的技术信息可以在 [Chainlink 离链报告协议白皮书](https://research.chain.link/ocr.pdf) 中找到。

![Chainlink Off-Chain Reporting (OCR)](img/3c2371e96dac5220b02d160754290ccc.png)

<figcaption id="caption-attachment-3693" class="wp-caption-text">The Chainlink Off-Chain Reporting (OCR) Protocol delivers significant cost improvements.</figcaption>



通过结合可配置的触发参数和经济高效的链上数据交付，Chainlink Price Feeds 可高度抵御不利条件，如市场极度波动和区块链网络拥塞时期，在此期间，准确和及时的 oracle 更新最受欢迎，也是保护用户资金安全最必要的。

### 4。多层纵深防御方法

Chainlink 价格馈送还采用额外的安全和监控层来主动缓解潜在问题，包括黑天鹅事件。

#### 链上透明度

由 Chainlink Price Feeds 生成的每份 oracle 报告都作为不可更改的公共记录存储在接收方区块链网络上。这使得世界上的任何人都可以分析自开始以来每个 Chainlink 价格馈送更新的历史性能和准确性。此外，因为每个 oracle 报告都包含每个响应节点的单独签名和响应，所以每个单独节点操作员的历史准确性和正常运行时间都是可审计的。

由 don 和单个节点提供的数据的透明的链上性质导致了各种公共仪表板和可视化工具的创建。例如，[dATA . chain . link](https://data.chain.link)提供了对各种 Chainlink 数据馈送的当前状态的整体概述，提供了最新可信答案、触发参数、最新更新时间、节点组成和契约地址等指标。

![Chainlink Data Feeds](img/bf411b4ccab885d79f59842398636ee6.png)

<figcaption id="caption-attachment-3694" class="wp-caption-text">Visualization tools like [data.chain.link](https://data.chain.link) bring transparency to Chainlink Price Feeds.</figcaption>



其他仪表板和透明度工具包括[Chainlink Market](https://market.link)和[chain link Oracle Explorer](https://oracle.reputation.link/)，它们可以更深入地了解 chain link 价格馈送和节点运营商详细信息的性能。这两个网站都由 Chainlink 生态系统中的独立项目管理。

#### 主动监控

支持 Chainlink 价格馈送的节点运营商在其基础设施设置中采用主动监控策略，在问题发生前或发生时主动检测问题。这包括使用内部分析工具来跟踪实时和历史节点性能，以及设置通知警报来通知潜在问题，而不管日期或时间。

主动监控包括跟踪许多关键数据点和领域，如燃气费所需硬币的余额、价格偏差、意外错误、无响应、硬件资源消耗等。除了节点性能和可靠性之外，还监控数据提供商的准确性和正常运行时间，使节点运营商能够根据需要切换到不同的提供商，以获得持续的数据质量和可靠性。

#### 故障转移能力和灾难恢复

作为维持任务关键型基础设施高正常运行时间的最佳实践，Chainlink 价格馈送中的节点运营商整合了故障转移系统以提高弹性。这通常采取按需自动启动新的 Chainlink 节点实例或同时并行运行至少两个 Chainlink 节点的形式，其中一个作为主节点，其余作为备份。如果主节点出现故障或变得无响应，则会发生故障转移过程，辅助节点会立即接管，以最大限度地减少停机时间。

![AWS Chainlink Quickstart](img/959970fb276a2d9ef30ce1f788675b44.png)

<figcaption id="caption-attachment-3695" class="wp-caption-text">Example of infrastructure redundancy, with a primary and backup oracle node, provided by the [AWS Chainlink Quickstart](https://blog.chain.link/announcing-the-aws-chainlink-quickstart/).</figcaption>



故障切换功能超越了 Chainlink 节点部署，还包括用于从区块链读取数据和向其写入数据的区块链完整节点。这可以采取以下形式:多个自托管完整节点之间的负载平衡器、以高级完整节点 RPC 提供程序作为辅助节点的故障转移模式，以及其他各种实现高可用性的方法。节点运营商还部署了灾难恢复系统，使他们能够从黑天鹅事件中快速恢复。方法包括定期拍摄快照、执行云迁移，以及在数据意外损坏时进行恢复的其他方法。

要了解更多关于 Chainlink 节点操作员采用的一些一般安全实践，请参考 Chainlink 文档中关于 [安全和操作最佳实践](https://docs.chain.link/docs/best-security-practices/) 和 [在 AWS 上部署节点的最佳实践](https://docs.chain.link/docs/best-practices-aws/) 。

#### 备份 Oracle 网络和客户端多样性

某些区块链上的 Chainlink Price Feeds 以备份 oracle networks 的形式利用额外的冗余，feed 由一个主要 DON 和一个辅助 DON 组成。don 更新两个独立的参考智能合约，代理智能合约指向两个版本中的一个。在正常情况下，主 DON 作为 feed 的默认 DON。然而，如果主要 DON 有问题，那么代理合同可以切换到次要 DON。

![Chainlink Price Feed backups](img/8291cbbd6abf20eefb7c04af1abc27ea.png)

<figcaption id="caption-attachment-3696" class="wp-caption-text">An ETH/USD Chainlink Price Feed with primary and secondary networks.</figcaption>



二级 DON 由按延迟时间表更新到新节点软件版本的节点组成，创建了一种软件形式 [客户端多样性](https://blog.chain.link/circuit-breakers-and-client-diversity-within-the-chainlink-network/) ，并为 Chainlink 价格馈送添加了另一层保护，以防止意外的软件错误。虽然 Chainlink 价格馈送从来不需要切换到第二 DON，但该功能是存在的，并且是减轻黑天鹅事件的有力工具。

### 5。稳健的区块链无关架构

Chainlink 是一种与区块链无关的 oracle 协议，原生集成到十几个领先的区块链、侧链和第 2 层汇总中。通过在本地部署，Chainlink 价格馈送可以直接向区块链传送数据，而无需交叉依赖其他区块链。这使得数据能够以受支持链的本地速度和成本交付，因此高吞吐量链上的 DeFi 应用程序可以受益于更高频率和更低成本的 oracle 更新。此外，如果另一个区块链网络出现停机或拥塞问题，一个区块链上的 Chainlink 价格馈送将不会受到影响。

![Chainlink blockchain-agnostic price feeds](img/9c582faf4954cf09b05bc1cc534b637f.png)

<figcaption id="caption-attachment-3697" class="wp-caption-text">​​Chainlink Price Feeds run natively on each supported blockchain network.</figcaption>



相比之下，如果一级链遇到可靠性问题，依赖第三方中继器将 oracle 价格报告从一级区块链传递到二级区块链的替代价格馈送设计可能无法提供数据。这些非本地价格先知还受到速度、延迟、成本和集中化问题的影响，这些问题将 DeFi 协议置于风险之中。

欲了解更多关于 Chainlink 的区块链不可知 oracle 网络的方法，请查看 [Chainlink 的区块链不可知设计:任何网络的原生 Oracle 支持](https://blog.chain.link/chainlinks-blockchain-agnostic-design/) 。

### 6。通过聚集用户费用实现规模经济

Chainlink Price Feeds 以一种共享成本模式运行，随着时间的推移，feed 由不同的付费用户社区(称为赞助商)共同支持。这使得需要相同区块链(例如 Arbitrum 上的 AAVE/美元汇率)上的相同数据的多个赞助商可以合计其费用，以支持向节点运营商提供的奖励，从而抵消其生成 oracle 报告的成本。这种共享成本模式产生了强大的规模经济效应，链价格提要的每个新赞助商都进一步增加了该提要的安全预算。

![Chainlink DeFi snapshot](img/57f0aa6130c3446a10f7d14859c618b9.png)

<figcaption id="caption-attachment-3698" class="wp-caption-text">A snapshot of leading DeFi protocols powered by Chainlink (January 2022).</figcaption>



增加的安全预算可用于提升提要的保证和性能，例如增加更多 oracle 节点和数据源以实现更大的分散化，增加更新频率以提高数据精度，等等。类似的网络改进可以在以太坊 上的 [Chainlink ETH/USD 价格反馈中看到，它从最初的三个节点扩展到现在由 31 个独立节点运营商支持。此外，用户费用的聚集意味着用户不需要支付价格馈送的全部操作成本，而只需要支付总成本的一部分。](https://data.chain.link/ethereum/mainnet/crypto-usd/eth-usd)

### 7。采用支持长期可持续性

如今，除了提供高水平的安全性和可靠性，Chainlink 价格馈送还针对长期可持续性进行了优化。随着采用的增加，可以产生更大的用户费用池来支持价格馈送的持续操作和扩展。随着时间的推移，随着越来越多的赞助商整合并提供资金，feed 可以完全通过用户付费来支持。

这种优化为现有和未来用户提供了更大的保证，即 Chainlink 价格源将继续存在，并在未来很长一段时间内得到财务支持，从而支持 DeFi 经济的持续增长和采用。

## **价格反馈只是冰山一角**

对数据质量和 oracle 基础设施安全性的高度关注推动 Chainlink Price Feeds 成为 DeFi 经济中最久经考验、使用最广泛的 Oracle Price 解决方案。此外，Chainlink 价格馈送经过专门设计，可随着 DeFi 的增长而扩展，帮助生态系统成长为价值数十亿至数万亿美元的主要全球金融市场的首选后端。

价格数据只是冰山一角，Chainlink 已经支持广泛的 [数据馈送](https://chain.link/data-feeds) ，具有类似的安全性和质量标准，例如 [储备证明](https://chain.link/proof-of-reserve) 、天气数据、体育比赛结果、区块链元数据等等。除了数据交付，Chainlink 还越来越多地支持新形式的 [信任最小化的链外计算](https://blog.chain.link/what-is-oracle-computation/) 使用 DONs，以及为 Web3 生态系统开发安全的 [跨链通信协议](https://blog.chain.link/introducing-the-cross-chain-interoperability-protocol-ccip/) 。

外部数据、链外计算和跨链通信的这种结合使 Chainlink 成为一种全栈解决方案，能够提供智能合约所需的任何链外服务。 如果你是一名 DeFi 开发者，想要整合 Chainlink Price Feeds，请查看我们的 [文档](https://docs.chain.link) ，在[Discord](https://discord.com/invite/aSK4zew)中提问，或者 [与专家建立通话](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=homepage&typeform-source=blog.chain.link) 。**