# 区块链上的数字身份:用 Chainlink 保护用户数据

> 原文：<https://blog.chain.link/digital-identity-on-the-blockchain/>

在链外世界中，“**数字身份**”(D-ID)是指当用户在线花费时间和进行活动时，由各方和平台收集的聚合信息。用户的搜索历史、社交媒体活动、交易历史、用户名和密码、通话记录、SSN、出生日期、信用记录、病史和其他重要信息等数据通常会找到它的方式并存储在网上，最终建立一个跨多个数据库的独特档案 **—** 每个用户的数字身份。

用户拥有一系列身份认证和安全工具来保护他们的数据，但即使是最安全的在线平台也可能被黑客攻击，导致用户 D-ID 的敏感方面暴露，并使他们和平台面临身份盗窃和欺诈的风险。事实上，多项研究表明，被黑客攻击或泄露的个人信息是暗网上交易最频繁的产品之一。

相比之下，D-ID 在区块链上的运行方式既公开又私密。[区块链](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/)是分散的、不可变的分类账(或数据库)，允许个人进行点对点交易，同时保持关于分类账/数据的共识，最终创建共享真相的来源。区块链是公开的，任何参与者甚至是局外人都可以审计每一笔交易和地址；它们是私有的，除非得到明确许可，区块链不需要 KYC(了解你的客户),用户可以匿名参与，他们的区块链地址与他们的外链身份没有什么联系。

区块链技术的一个特别有前途的用例是通过将区块链技术的最佳特征应用于传统的 D-ID 系统来改善 D-ID 体验。尽管架构细节各不相同，但基于区块链的 D-ID 解决方案将理想地允许用户选择性地选择与谁以及何时共享他们的信息，使用户信息远离易受攻击的数据库，允许用户更好地将他们的数据货币化，并更好地保护用户隐私。虽然这个用例乍一看似乎微不足道，但它提供的不仅仅是便利和数据安全 **—** 据估计，到 2030 年，数字身份和相关产业可能会达到 GDP 的 3%。

本文将研究与传统 D-ID 实现相关的风险和挑战，分解区块链 D-ID 可能如何解决它们，并分析四个依赖 chain link[Oracle](https://chain.link/education/blockchain-oracles)将个人信息与区块链连接起来的具体实现。

## D-ID 中的当前缺陷

虽然传统 D-ID 系统的缺陷对于已经接受它们的用户来说可能经常不被注意到，但是这些缺陷是系统性的和有害的。D-ID 是让人们日常生活所依赖的许多在线系统正常工作的一个关键因素，但几乎在数据收集、存储和出售的每一步**—****—**D-ID 都充满了安全、隐私甚至道德问题。最终，这些问题可以大致分为三类:数据货币化、数据访问和数据存储。

### 数据货币化

D-ID 的一个重要部分是主要互联网平台秘密收集的关于用户行为、习惯和传记信息的数据。例如，搜索引擎可能会收集用户的兴趣数据，为他们量身定制广告，或者社交媒体网站可能会将用户自己创建的信息出售给感兴趣的团体，如政治活动。因为这些活动的细节通常隐藏在使用协议中，这些平台的用户无处不在，不知不觉地用表面上休闲的时间丰富了平台。

这个过程中，用户通过正常的习惯，在不知不觉中为平台提供信息，然后这些信息被货币化，这个过程通常被称为“免费劳动”。自由劳动力的支持者认为，这种数据货币化是访问通常免费的服务/平台的自然交换，最终通过允许平台更快地发展和提供更好的用户体验而使用户受益。

然而，免费劳动力带来了一系列道德和隐私问题，通常围绕着用户不清楚收集的是什么数据，卖给谁，或者存储在哪里。尽管一些国家试图对主要平台可以收集的数据进行监管，但免费劳动力仍然是一个猖獗的问题，互联网上的用户都不确定哪些数据正在被收集，以及这些数据将被用来做什么。

### 数据存取

某些互联网平台和服务需要比其他平台和服务更完整的 D-ID 档案才能访问。社交媒体网站可能只需要一个电子邮件地址(尽管他们随后会建立一个用户档案)，而贷款服务或政府机构可能需要完整的财务或个人历史，然后才能通过其门户网站提供访问和服务。因此，用户经常被迫在不同的平台上反复提供相同的个人信息。虽然数据库的分离可以通过隔离攻击来防止更灾难性的破坏，但是存储重要用户信息的每个数据库最终会增加用户数据的攻击面。

这使用户处于一个困难的境地，不得不在耗时的过程和官僚主义之间做出选择，或者将他们的信息存储在可能容易受到攻击的数据库中以供重复使用。此外，这种系统也给平台带来了头痛的问题:政府机构可能会在多个服务器上存储冗余信息，这导致成本效率低下，并且由于用户数据泄露，其他平台可能更容易受到诈骗或盗窃。在许多情况下，平台是与身份盗窃相关的任何财务损失的最终责任方。

### 数据安全

如上所述，用户经常在线传播关于他们自己的信息，包括财务信息，以便进行购买或获得对服务的访问。访问和安全很少是相辅相成的，D-ID 也是如此 **—** 每个存储用户信息的网站都是一个新的攻击媒介，用户的信息可能会通过这个媒介被窃取。

鉴于威胁的级别，人们会期望平台会投资于高级安全和隐私基础设施。然而，尽管采取了安全措施，统计数据表明数据保护问题正在恶化，而不是改善:每年有超过 10%的人口受到身份盗窃的影响，在疫情期间，这一数字还在上升。

## 基于区块链的 D-ID 解决方案

由于这些缺陷，D-ID 是一个被区块链技术颠覆的成熟空间。通过使用区块链来设计高级 D-ID 系统，许多最突出的 D-ID 问题可以得到解决，全新的用例可以实现。

以区块链为基地的 D-ID 系统的主要特点包括:用户能够将他们自己创造的信息货币化，并跟踪他们的信息是如何被使用的；能够方便快捷地共享 D-ID 信息；以及保护数据安全的能力。有一系列独特的方法来实现这些目标 **—** ，包括完全消除外链身份的潜力 **—** ，每种方法都以不同的方式利用区块链。

### 德科

一个基于区块链的 D-ID 系统是 Chainlink 的隐私保护甲骨文技术 [DECO](https://arxiv.org/pdf/1909.00938.pdf) **—** 由 Chainlink 实验室首席科学家阿里·朱尔斯、研究员张帆和其他人开发。虽然新的 D-ID 存储解决方案可能会改变数据的存储方式，但现实是许多数据仍然存储在可信的数据库中。许多用户/机构，尤其是政府和大型企业，可能更喜欢委托高安全性的托管机构来保护这些数据。

DECO 允许 oracle 证明可信数据库/系统中的信息的有效性，而不会将其暴露给公众，甚至 Oracle 本身，使用一种称为零知识证明的加密技术。本质上，oracle 可以加入一个用户发起的 web 会话来证明一些请求的信息 **—** 可能是为了验证某人的身份、批准他们的财务信息或检查关键的政府记录。重要的是，这些数据永远不会离开用户选择的安全数据库，从而允许用户将他们的 D-ID 信息存储在他们信任的某些位置，并设置选择性访问，而不是将其传播到访问控制保证较弱的各种系统。这提供了一个保护隐私的即插即用选项，将传统系统的可用性与区块链的安全性结合起来。

![An image showing a three-party handshake.](img/03fef67e6372d7a2fd40e52caaaa1253.png)

<figcaption>One of DECO’s main techniques involves a three-party handshake – a method in which the Prover (user) and Verifier (oracle) can combine their public TLS keys and form a combined request for data, without the Verifier ever receiving said data.</figcaption>



DECO 的隐私保护技术还允许原本不可能的用例，如大数据医学研究。多年来，研究人员一直对将机器学习和计算分析应用于大型医疗数据集的潜力感到兴奋，希望使用这些工具来实现人类分析无法发现的发现和突破。然而，患者数据的隐私和安全问题长期以来一直是一个障碍。DECO 将允许研究人员选择性地访问他们需要的数据，同时遵守 HIPA 法规，并且不会将数据置于风险之中，这可能会开创医学研究的新时代。

### 花

另一个使用区块链技术增强 D-ID 的项目示例是 Bloom，这是一个分散的身份协议，允许用户声明、控制和选择性地共享他们的财务数据，同时通过分散的架构保留全部所有权。

Bloom 的工作原理是获取用户提供的数据并验证每个用户的身份，然后将这些数据以加密哈希的形式写入区块链。这允许将用户信息存储在公共分类账/真实来源上，同时维护其隐私。这对金融信息尤其有用，这是布鲁姆关注的核心领域之一 **—** 布鲁姆最近在[发表的博客文章](https://bloom.co/blog/bloom-integrates-with-chainlink-decentralized-finance/)展示了 Chainlink oracles 如何帮助将信用评分与 [DeFi](https://chain.link/education/defi) 协议联系起来。



![How Chainlink decentralized oracles connect credit scores to DeFi protocols. ](img/e3070bb20c788d75c7981403af6c4c7a.png)

<figcaption id="caption-attachment-771" class="wp-caption-text">chain link 分散式 oracles 如何将信用评分连接到 DeFi 协议。</figcaption>





Bloom 的首席技术官 Isaac Patka 说:“Bloom 最初是一个协议，它使用[智能合同](https://chain.link/education/smart-contracts)和以太坊地址来唯一地识别个人，并使他们能够声明、存储和共享经过验证的身份属性，其目标是分散信用局模型。“随着技术的发展，我们与更大的分散/自主身份社区联手，开发用于识别用户、颁发证书和交换信息的开放和互操作标准。身份标准现在已经成熟，我们可以将这项技术推向市场，并推动全球影响。我们很高兴实现我们最初的扩展金融包容性的愿景，并使用 Chainlink 等平台来弥合传统和分散世界之间的差距。”

### 不可阻挡的域名

Unstoppable Domains 是一个基于区块链的分散式协议，用于在区块链以太坊上将互联网[域名注册和托管为不可替换的 ERC721 令牌](https://blog.chain.link/how-to-create-nft-domain-names/)。不可阻挡的域名[最近宣布了](https://hackernoon.com/making-crypto-payments-less-scary-pjv3z2f)一项新功能，使用 Chainlink oracles 将 Twitter 用户链接到特定的域名，从而可以根据用户的社交媒体账户轻松识别和确认用户的公共地址。此外，用户可以直接向域名付款，绕过经常混淆的以太坊地址，获得更好的用户界面/UX 体验。

这个解决方案的独特之处在于，它有可能完全绕过真实世界的信息。Twitter 用户可以保持匿名，但仍有一个与他们关联的域名，可以发送和接收基于区块链的支付。这允许在身份可能完全数字化且不必存储在任何中央数据库中的各方之间进行安全、高度直观的价值转移。

### 相当好的

Decentr 是一个项目，旨在提供一个 Web3 版本的信用评分 **—** 他们称之为“个人数据价值”(PDV)。每个用户的 PDV 将来源于社交媒体活动、连锁活动(如他们的总资产和还贷历史)以及真实世界数据(如 KYC/反洗钱信息)的潜在组合。正如 Decentr 的[博客文章](https://medium.com/@DecentrNet/decentr-integrates-chainlink-to-provide-user-centric-social-reputation-scores-to-defi-311d12ed4b68)所讨论的，Chainlink oracles 可以向任何区块链的 DeFi 协议提供这些数据，并且具有高 PDV 值的用户可能会获得较少抵押甚至无抵押贷款。



![Decentr integrates with Chainlink to provide user-centric social reputation scores to DeFi. ](img/66530f868163f72524676514cae2cadb.png)

<figcaption id="caption-attachment-772" class="wp-caption-text">Decentr 与 Chainlink 整合，为 DeFi 提供以用户为中心的社交信誉评分。</figcaption>





像不可阻挡的域一样，这种方法不仅找到了一种使用区块链安全地将链外数据连接到 D-ID 的方法，而且还通过获取有价值的链上数据并使用它来创建用户的 D-ID 配置文件来支持区块链身份体验。注重隐私的用户可能会绕过使用真实世界的信息，转而只从他们的链上指标建立他们的 PDV 价值。

## 结论

D-ID 系统当前的缺陷持续且普遍地将用户的隐私和安全置于风险之中。然而，这些风险目前被视为访问关键日常服务和平台的必要权衡。通过使用区块链技术和 Chainlink oracle，这些风险可以通过安全地允许平台按需访问链外数据，或者通过完全取消链外身份来代替由 Chainlink oracle networks 验证的链上数据来减轻。

这些发展不仅有助于保护用户的隐私和数据安全，而且有可能为私人数据提供新的使用案例，否则由于安全和隐私问题，这是不可能的。通过使用 Chainlink oracles 将链上和链下数据连接到协议和 Web3 平台，数字身份的新时代可能刚刚开始。

### 了解更多信息

如果你想了解更多关于区块链空间的信息，请浏览 Chainlink 博客获取更多内容，包括关于 DeFi 的[数据质量、](https://blog.chain.link/the-importance-of-data-quality-for-defi/)[动态 NFTs](https://blog.chain.link/create-dynamic-nfts-using-chainlink-oracles/) 、[甲骨文问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)、[游戏中的经济回报](https://blog.chain.link/the-economic-impact-of-random-rewards-in-blockchain-video-games/)、 [DeFi 可组合性](https://blog.chain.link/defis-permissionless-composability-is-supercharging-innovation/)等更多内容。

如果您是一名开发人员，并希望将您基于智能合约的应用程序连接到区块链以外的链外数据和基础设施，请联系我们[此处](https://chainlink.typeform.com/to/gEwrPO)或访问[开发人员文档](https://docs.chain.link/)。

[网站](https://chain.link/) | [简讯](https://chn.lk/newsletter) | [推特](https://twitter.com/chainlink)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://defi.chain.link/)