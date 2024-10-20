# 区块链和神谕:相似、不同和协同

> 原文：<https://blog.chain.link/blockchains-oracles-similarities-differences-synergies/>

区块链和甲骨文都是开发分散应用(dApps)的关键网络基础设施，并使用类似的安全方法，如加密、分散共识和加密经济激励。然而，它们在网络体系结构、服务提供、节点组成和总体目的方面也有所不同。这些差异是协同的，并结合起来形成混合智能合约——保留区块链的安全假设，同时通过 oracles 实现广泛的功能丰富性的智能合约。T3】

[区块链](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/) 引入新的后端基础设施，用于运行防篡改计算并将数据存储在不可变的分类账上。虽然最初用于创造和管理分散形式的货币，区块链已经发展到现在的权力[](https://chain.link/education/smart-contracts)—具有条件逻辑的确定性程序(如果/当 *x* 事件发生时，触发 *y* 动作)。

就像互联网对于计算机的价值一样， [甲骨文](https://chain.link/education/blockchain-oracles) 通过允许它们使用来自区块链外部(链外)的数据和计算来执行智能合约，从而开启了智能合约的全部潜力。这些 [混合智能契约](https://blog.chain.link/hybrid-smart-contracts-explained/) 提供了一个支持分散化应用程序(dApps)的高级框架，其中区块链和 oracles 之间的相似性确保了端到端的分散化，而它们的组合差异使得在不牺牲底层安全模型的情况下增强连接性、可伸缩性、隐私性和公平性成为可能。

![Hybrid smart contracts](img/67caae9d2315e2bdb90d7e2f2627c7b7.png)

<figcaption id="caption-attachment-2310" class="wp-caption-text">Hybrid smart contracts combine on-chain and off-chain infrastructure for advanced decentralized applications.</figcaption>



下面的文章将对区块链和神谕的目的和架构，以及它们之间的相似性、差异和协同作用进行更深入、更细致的研究。

## 比较区块链和神谕的目的和架构

在深入研究相似性和差异之前，让我们根据区块链和甲骨文在 dApps 中的作用来定义它们的目的和通用架构。

### 区块链

区块链的核心目的是维护一个持久的分布式数据分类帐，通常由数字资产组成。区块链分类帐存储用户的帐户余额和智能合同状态，并在确认新的有效交易时更新它们。区块链使用分散的挖掘者/验证者网络来更新他们的分类账，这些挖掘者/验证者批量验证新交易，称为块，以获得财务奖励。验证规则被硬编码到由挖掘器/验证器运行的软件客户端中，并且在没有大多数网络参与 [硬分叉](https://www.investopedia.com/terms/h/hard-fork.asp) 的情况下不能改变。

挖掘者/验证者致力于涉及二元(是/否)确认的交易验证的共同目标，其中必须满足几个基本条件:1) [私钥签名](https://www.gemini.com/cryptopedia/public-private-keys-cryptography) 匹配相应的公钥地址，2)用户的账户余额足以支付交易付款和 [汽油费](https://www.investopedia.com/terms/g/gas-ethereum.asp) ，以及 3)接下来是用户的 [随机数](https://kb.myetherwallet.com/en/transactions/what-is-nonce/) 挖掘器/验证器需要参与的唯一资源是当前的软件客户端、足够高性能的硬件和当前分类帐的副本——它们都不需要任何特殊的访问权限。

这个总体架构展示了区块链的四个主要特征:

 ***   [**密码真实性**](https://blog.chain.link/sergey-nazarov-smartcon-keynote-the-future-of-hybrid-smart-contracts/)—新交易的验证基于对分类账中已被认为真实并公开的历史信息的验证。
*   **网络是单片的**—所有节点作为一个整体一起工作，为区块链上的所有帐户和应用程序提供一个单一的 全球真相来源。
*   **服务是标准化的**—网络上的用户可以使用一组标准的计算，所有节点都执行相同的事务验证服务。
*   **节点要求是通用的**—运行一个节点涉及所有作业的相同资源(例如计算能力)，没有外部依赖性。

![Paper Promises vs. Cryptographic truth](img/b37f6150eb6b1164600050ae44a24d15.png)

<figcaption id="caption-attachment-2311" class="wp-caption-text">Cryptographic truth provides a superior form of truth compared to today’s “just trust us” paper promises.</figcaption>



### 神谕

oracles 的核心目的是获得关于链外数据、事件或计算有效性的真相，然后将结果传递到链上。生成真实世界的外部真相是复杂的，因为它涉及非确定性数据集，这些数据集本身无法单独使用加密技术进行验证。非确定性是一个具有不可控外部变量的过程，对于 oracles 来说，它依赖于数据，而数据的值可能会根据查询的源和查询的时间而改变。这种数据不能被区块链网络验证，因为数据的有效性不依赖于历史的链上状态。

相反，从一个非确定性的环境中产生真理包括在给定预算、时间表和资源列表的情况下，在某种事物的外部状态中创建一个统计上的高度置信度。这就是区块链与甲骨文分离的原因，因为关于现实世界外部状态的分歧会导致区块链的一致失败，扰乱其上运行的所有 dapp，即使大多数 dapp 与特定的甲骨文报告没有关联。分歧还需要大量的治理开销，限制了潜在的 oracle 创新并增加了成本。

关于用户认为外部世界的真实情况，以及他们对真实情况的信任度和验证方法，有很多观点。例如，加密货币价格或外汇汇率具有非二进制、范围限制的真实性，因为金融市场是连续的(与离散值相比)，导致不同交易所、地理位置和计算方法的正确价格的不同概念。

生成真相的能力也可能受到某人可用资源的限制——一个免费的数据 API 可能不如人们付费访问的认证数据 API 准确可靠，而几个认证 API 的集合可能比一个更可靠。资源可用性还扩展到用户是否可以访问信息，例如仅限于认证用户的私有物联网网络和允许访问的企业后端系统。此外，还需要考虑时间和货币价值如何影响外部状态验证的可靠性，例如，是否需要实时验证，或者在发起后几天就足够了，以及外部数据的智能合同价值是 1 万美元还是 100 亿美元？不同的答案可能会导致不同的 oracle 设计。

因为在非确定性环境中没有单一的生成真理的方法，所以 oracles 是用于获得 [确定性真理](https://blog.chain.link/how-chainlink-is-helping-blockchain-cross-the-chasm/) 的特定于应用的服务——一种生成真理的预定义方法，所有相关方都同意这种方法对于解决他们的协议是权威的。设计良好的 oracles 的真正强大之处在于，它们能够以防篡改和自动化的方式生成关于外部状态的明确真相，并根据用户自己的信任假设、性能需求和预算进行定制。因此，Chainlink 支持多种 [oracle 网络定制技术](https://blog.chain.link/how-chainlink-supports-any-off-chain-data-resource-and-computation/) 来获取确定的真相，包括不同程度的去中心化、特定数据源和节点操作符的选择、不同级别的加密经济安全性以及各种其他可调整的安全参数。

与区块链相比，像 Chainlink 这样的通用 oracle 网络的架构在几个方面有所不同:

 ***   **确定的真相**—每个智能合约应用程序都精确地定义了它们将如何从外部世界获取真相，以及超出这些界限的内容。
*   **网络是异构的**—Oracle 为应用程序执行特定的工作，但并不作为一个具有交叉依赖性的统一整体网络运行。
*   **服务多种多样**—用户可以获得无限数量的 oracle 服务，节点执行的工作和获得的收入的数量和质量各不相同。
*   **节点要求各不相同**—每项工作都有不同的要求，节点通过不同的基础设施、数据访问、声誉等来竞争这些要求。

## 区块链和甲骨文设计的相似之处

虽然存在各种差异，但区块链和神谕都可以生成关于事物状态的真相，并利用许多相同的安全技术。

### 开源代码

安全区块链和甲骨文都是用开源代码编写的(通常在许可许可下，如 [麻省理工](https://opensource.org/licenses/MIT) )，提供了节点后端过程的透明性，并促进了其网络的创新、迭代和正确性。

### 分散网络

分散式 oracle 网络(DONs)采用了与区块链相同的概念，通过一组不同的实体进行冗余计算，以实现服务的防篡改性、可用性和正确性。

### 加密签名

区块链和东斯的节点都使用公/私加密技术对它们广播的所有交易进行签名，以便验证身份、证明所有权、建立不可否认性和创建透明性。

### 密码经济安全

两种网络都使用经济激励来培养诚实的多数共识，并抑制单个节点和整个网络的恶意活动。节点因诚实工作而获得奖励，因直接或间接的恶意活动而受到惩罚。

![Blockchains and oracle similarities](img/384cf3daf0ada68dc8b772bc6b8b3c79.png)

<figcaption id="caption-attachment-2305" class="wp-caption-text">Blockchains and oracles share similar properties like open-source code, decentralized networks, cryptographic signatures, and cryptoeconomic security.</figcaption>



## 区块链和甲骨文设计的差异

很少有人了解区块链和甲骨文之间的区别，这是理解为什么在混合智能合约中结合两者时协同作用成为可能的关键。

### 密码与确定真相

区块链是故意隔离的网络，具有基于完全已知的、可验证的和可访问的变量的内部真理源。因为来自 genesis 块的每个事务都是加密签名的，所以每个公共地址都有一个可公开审计的事务历史。因此，每一笔需要验证的新交易只需查看一个公共地址的交易历史，以验证他们已经积累了足够的资金来支付交易。在这个意义上，真理是基于在特定区块链内具有密码验证来源的信息，称为密码真理。

先知的任务是从具有未知变量的非确定性环境中创造真理。神谕被用来创建应用程序定义为足够的孤立的真理集，而不是将区块链共识置于危险之中。确定性事实并不是为了保持所有应用程序的全局状态，而是为了证明 oracles 完全按照其创建者的意图执行。建立在加密真理的基础上，最终真理使用区块链的公钥/私钥加密来确保离线 oracle 计算的不可否认性和透明性。最终真相还依靠区块链根据甲骨文网络的表现建立奖励和惩罚制度，创造确定性的结果。最终结果是一种高度可配置的方式来生成关于世界的真相，并具有强有力的加密保证，它将按预期执行。

![Definitive truth from oracle networks](img/7de134d6637b5d3bbbbfd40457c82095.png)

<figcaption id="caption-attachment-2308" class="wp-caption-text">Definitive truth uses the cryptographic truth of blockchains as a foundation to enable highly configurable truth with strong security guarantees.</figcaption>



拥有一种生成关于外部世界的确定真相的方法，使得 dApps 能够克服 [甲骨文问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/) 因为他们可以根据自己的信任假设配置甲骨文网络。虽然用户可能会对他们认为值得信赖的 oracle 网络有所不同，这取决于使用案例、价值和生成方法等变量，但许多标准框架已经出现。例如，[chain link Price Feeds](https://chain.link/solutions/defi)是已经成为价格数据绝对真实性的行业标准的 don，在整个 DeFi 行业中已经得到广泛信任，可以确保大量的链上价值。

### 整体网络架构与异构网络架构

由于加密和确定性真实具有不同的角色，区块链和广义 oracle 网络具有不同的底层架构。区块链管理着一个需要全球访问的内部真相的单一来源，因此它使用一个单一的网络来维护。网络中的所有区块链节点聚集在一起执行一组标准化的作业，以获得一个特定的报酬——在大致标准化的时间间隔内创建有效的块，以获得块报酬和用户费用。不存在不同作业的并行处理；即，分片是相同作业类型的并行处理，而不是不同的。正是这种有目的的专业化使区块链在交易验证的特定计算中非常安全可靠，但也是这种特性使它们非常受限。

Oracles 可以接收一组无限的不同请求，以生成关于任何现实世界事件、数据点或计算的确定事实。每个 oracle 请求都有不同的服务成本和回报，这取决于验证的难度和用户想要的确定程度。Oracle 请求还可以跨越许多不同的区块链，并且可能涉及私人付费墙或法律障碍背后的数据和服务，只有某些获得许可的节点才能访问这些数据和服务。

从技术、法律和财务的角度来看，工作成本、质量和要求的多样化使得单个节点网络几乎不可能访问所有外部资源来满足网络上的所有 oracle 请求，并维护所有用户所需的独特安全保证。单个网络不仅会消除满足涉及许可资源的某些 oracle 作业的可能性，而且考虑到服务所有作业所需的巨大资源，每个作业可以获得的分散化的上限会非常低。因此，采用整体式设计的 oracle 网络必须以最少的灵活性和数据访问来优化节点的最小公分母，从而显著降低用户可获得的服务和质量。

正是因为这个原因，Chainlink 采用了异构网络设计，在这种设计中，无限数量的节点和 don 可以并行执行各种各样的任务，而不会相互依赖。这是为所有 oracle 用例提供服务的唯一方式，因为不同的作业按照各自的时间表同时得到服务。Chainlink 的异构架构为混合智能合约开辟了多种服务，如数据交付、数据聚合、数据签名、链外计算、隐私生成、交易自动化、可验证的随机性、L2 验证、跨链通信、链外支付等。此外，Chainlink oracles 可以由原始数据/服务提供商直接运行，也可以外包给专业的 oracle 节点运营商，如传统企业，从而为混合智能合同开发者创造了广泛的灵活性。

![Monolithic blockchain vs Heterogeneous oracle network](img/80d5128530a550d62e01a471592f6b45.png)

<figcaption id="caption-attachment-2306" class="wp-caption-text">Monolithic blockchains act as a single network keeping a single source of shared truth. Heterogeneous oracle networks are a network of networks, simultaneously delivering many sources of user-defined definitive truth to support various use cases and trust assumptions.</figcaption>



### 标准与变化的服务质量和节点要求

网络架构的差异导致区块链和甲骨文网络在服务质量和运行服务的节点要求方面存在差异。区块链在二进制验证框架内提供标准化服务，导致节点质量几乎没有偏差(注:风险证明区块链倾向于节点正常运行时间差异非常小，且通常具有预设的风险金额)。作业规范的标准化也意味着每个区块链节点可以通过一个硬件设置执行网络上的所有作业。由于节点质量之间几乎没有差异，区块链主要通过简单地添加更多独立节点来提高 Sybil 抵抗力和分散性，从而在网络级别进行扩展。

Oracle networks 的不同之处在于，它们不提供标准的服务列表，从而导致单个 Oracle 节点和整体上的性能质量存在差异。节点的差异意味着，增加更多的节点或允许任何人运行一个节点并不能保证 DON 的质量会提高。DONs 中未经许可的去中心化实际上会降低数据质量和安全性，并导致用户的服务保证不确定，节点运营商的收入保证不稳定。尝试这种模式的 oracle 通常具有较弱的数据质量保证、有限的 oracle 服务选择、更新之间的大时间延迟和/或 Sybil 攻击漏洞，这使得它们对于大多数 Oracle 用例来说不切实际。

要克服 oracle 网络中的质量差异，有必要建立 [信誉框架](http://reputation.link) 和 [市场](http://market.link) ，用户可以根据他们认为重要的指标来评估单个节点和 d on 的质量。节点运营商可以通过提供有关其链上作业历史、数据资源连接、支持的 oracle 服务、真实身份、地理位置和基础架构设置详细信息的信息，在市场上脱颖而出。信誉系统还可以通过跟踪节点的链上性能，如它们的平均响应等待时间、平均响应偏差和服务的作业，以及跟踪整个 don 的性能，来帮助过滤节点质量。

![Chainlink Market](img/b323b1e05a11f6282dbefe13f710142b.png)

<figcaption id="caption-attachment-2314" class="wp-caption-text">The permissionless Chainlink Market provides a community resource for node operators to highlight their reputation, infrastructure, and performance history to users.</figcaption>



声誉系统和市场使用户能够做出明智的决定，如何为他们自己确定的真理创建一个用户定义的谢林点。他们可以通过购买更高质量的数据源、更有信誉的节点、更快的更新频率、更分散的节点和数据源、更高效的聚合方法、更分布式的基础设施设置、合并信任最小化的硬件、可选的断路器、软件客户端多样性、零知识证明等来提高安全性。它们的架构也不一定是静态的，它们可以随时放大或缩小，以增加鲁棒性或降低成本。当在一组独立付费用户之间共享和集体资助时，DON 也可以变得更强大，其中每个额外的用户增加 DON 的安全预算，降低所有现有和未来用户的成本。这种共享使用和融资模式已经在今天的 Chainlink 价格源中出现。

## 区块链+甲骨文=高级混合智能合约

区块链和甲骨文的重叠相似之处，结合它们的不同优势，使得混合智能合约的全部潜力得以实现。区块链作为隔离和标准化的计算网络是有价值的，具有有限的攻击面和极端水平的防篡改、防审查、可用性、不变性和正确性。这些特征使区块链成为伟大的数字资产分类账、不可变的数据存储网络和最终结算层。

或者，oracles 作为一种高度灵活、可伸缩和低成本的计算基础，对于执行智能合约由于技术、财务或隐私限制而无法在其底层区块链上获得的所有服务来说是有价值的。oracle 安全性可以通过对多种安全技术进行分层并对每种技术进行微调来进行扩展，以便 Oracle 服务达到符合用户信任假设的可靠性水平。

![Chainlink Network decentralized services](img/1b7c77616494e7ed253b6c0323f43d54.png)

<figcaption id="caption-attachment-2307" class="wp-caption-text">The Chainlink Network offers a broad diversity of decentralized services to power hybrid smart contracts operating on numerous blockchain networks.</figcaption>



将这两种技术相结合打开了分散化应用程序开发的圣杯——混合智能合约基础设施，它将信任最小化的资产托管和最终结算与高吞吐量计算和补充附加功能(如外部连接、隐私、公平订购、交易自动化、可验证的随机性等)相结合。混合智能合约是区块链应用程序开发下一个飞跃的基础，在这个飞跃中，真理可以扩展到更广泛的外部环境，并进行定制，以满足更广泛的用户和用例的需求。只有通过一个建立在真理而不是信任之上的世界，社会才能走向更加公平的社会和经济体系。

如果您想现在就开始构建混合智能合约应用程序，并且需要某种类型的外部数据或计算，请参考我们的 [文档](https://docs.chain.link/docs/getting-started) ，在[Discord](https://discordapp.com/invite/aSK4zew)中询问一个技术问题，或者 [与我们的一位专家建立一次通话](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=homepage) 。

要了解更多信息，请访问[chain . link](https://chain.link/)，订阅 [Chainlink 简讯](https://chn.lk/newsletter) ，并关注[chain link 上的](https://twitter.com/chainlink) 、[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)和 [Reddit](https://www.reddit.com/r/Chainlink/)****