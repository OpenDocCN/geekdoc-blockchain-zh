# DeFi 智能合同的数据质量

> 原文：<https://blog.chain.link/the-importance-of-data-quality-for-defi/>

分散金融( [DeFi](https://chain.link/education/defi) )应用程序的生态系统和由[区块链先知](https://chain.link/education/blockchain-oracles)保护的价值正在协同扩展，相互支持彼此的成功和发展。随着 DeFi 所担保的价值持续快速增长，确保这一革命性的新型去中心化金融生态系统为其用户提供更高级别的安全性和可靠性保证也变得越来越重要。

区块链的"[甲骨文问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)"是众所周知的，因为许多文章已经详细研究了这个主题。然而，oracles 提供的“数据质量”主题仍然很大程度上不为人知和误解。这种误解的根源在于通常持有的假设，即 oracles 既用于传输链上的外部数据，也用于生成高质量的数据。根据我们研究和构建安全 oracle 解决方案的经验，区块链 Oracle 旨在传输链上的数据并加强数据的可操作性，而不是创建数据本身。

这些问题(数据交付与数据质量)的分离已应用于支持 [Chainlink 数据馈送](https://data.chain.link/)的分散式 oracle 网络架构，这些数据馈送是 DeFi 中使用最多的 Oracle。基于这些 oracle 网络在为实时应用提供高质量数据方面的成功，我们确定了解决数据质量问题的五个基本要素。

1.  使 oracle 节点能够连接到高级数据提供商,以确保用户合同能够访问最高质量的数据。这要求 oracle 协议具有密码和凭证管理功能，以便所有节点可以安全地存储 API 密钥并管理付费订阅的帐户登录。
2.  让节点从专门生成准确价格数据的高质量链外数据提供商获取价格数据；特别是在所有交易环境中维护经交易量调整的市场覆盖面的数据聚合器。使用 oracle 机制从原始数据馈送的集合中生成全球市场价格是极其困难的，并且它使 oracle 暴露于许多攻击面，例如快速交易量变化和数据异常值，这两种情况在加密货币市场中并不罕见。
3.  将分散化作为 oracle 提供的安全性和可靠性保证的一个积极部分。从多个独立节点进行聚合，以确保 oracle 机制在向合同交付数据时具有抗篡改性和高可用性。在不牺牲质量的情况下，从多个高质量的数据提供商处获取数据，从而进一步分散数据源级别。
4.  更倾向于让用户和开发人员在设计 oracle 机制时能够做出明智决策的系统，为他们提供对每个节点和分散式 oracle 网络作为一个整体的当前和历史性能的实时洞察。通过模糊的方法避免任何安全问题，以最大限度地减少隐藏的风险，并确保尽可能多的人能够在任何潜在问题成为实质性问题之前及早发现它们。
5.  规避较大的风险，例如使用单一 exchange 数据源和/或用不太安全的 oracle 解决方案中的低质量数据稀释安全的 oracle 解决方案中的高质量数据。没有质量控制标准的分散化使合同暴露在更大的攻击面上，具有更大的复杂性，经常导致削弱高质量 oracle 解决方案的意外后果。

为了进一步阐述这些对确保数据质量至关重要的特性，我们研究了安全的分散式 oracle 网络的理想组成，如何正确利用 Chainlink 的广泛灵活性来生成高质量的数据，以及在设计 price oracle 网络时要避免的大量数据来源风险。

## 安全分散的 Oracle 网络的组成

oracle 是一种中间件，充当区块链和外部世界之间的桥梁。它允许[智能合约](https://chain.link/education/smart-contracts)消费不存储在区块链上的信息，以便从外部了解真实世界中的日常事件。这种外部连接成倍地增加了智能合同可以撰写的事件数量，使开发者能够在更广泛的市场中获取更多价值。随着连接性的增加，出现了新的攻击面，必须保护这些攻击面，以保持智能合同的核心租户的防篡改性、不变性和可用性。

去中心化的 oracle networks 是**安全中间件**，用于连接链上和链下环境，提供一个框架来构建用户信任外部连接的智能合同所需的安全性和可靠性保证，这些合同拥有数十亿美元或更多的用户资金。如果没有像区块链那样的安全性和可靠性标准，即使合同代码本身没有缺陷，整个智能合同也会面临风险。

[Chainlink Data Feeds](https://data.chain.link/) 是一组分散的 oracle 网络，提供以太坊生态系统中最大的链上定价数据集，越来越多的领先 DeFi 应用程序依赖这些数据。这些 price oracle networks 的设计模式遵循通过可验证的分散化方法实现安全性，并遵循最佳数据质量实践，为其用户带来最大的安全性。以下是在整个 Chainlink 数据馈送中实施的四个关键特性，它们应该应用于所有希望确保数据质量的分散式 oracle 网络。

![A diagram showing various node operators and data sources.](img/7ffaec42d0bcd18113675c66b9556c92.png)

### 来自优质数据提供商的高质量数据

虽然挖掘区块链散列是一种相当统一的操作，但生成质量足够高的行业特定数据以确保数亿美元的价值却不是任何人都可以信赖的任务。与其尝试使用 oracle 机制从原始数据集合中生成高质量的数据，不如让 nodes 直接从知名的数据聚合公司获取数据，这些公司拥有大型团队、全栈基础架构，并且只专注于为特定行业生成高质量的数据。

生成高质量的专有数据是资本密集型的；它不是免费的，需要一份具有法律约束力的合同和凭证才能访问。节点必须向数据提供者(API)付费订阅，或者由数据提供者特别授权(例如，内部企业数据)。这两种许可模型都需要密码和凭证管理功能来桥接节点和 API 之间的交互。因此，节点操作员需要能够存储 API 密钥和管理帐户登录，以便与这些高级数据提供者进行交互。

由于缺乏凭证管理功能而无法连接到高级 API 的 Oracle 解决方案仅限于提供开放、免费或盗版的 API。这些 API 通常具有低质量的数据、速率限制、不可靠的响应时间以及没有法律约束的可用性或服务质量保证，所有这些都使得这样的数据源不适合任何高、中甚至许多小价值的用例。获得低质量数据的智能合约无法保证所消费数据的可靠性或准确性，从而在这一过程中形成了更大的攻击面。正如任何其他由数据驱动的技术一样，“垃圾进，垃圾出。”

参与价格参考数据契约的 Chainlink 节点利用[外部适配器](https://docs.chain.link/docs/external-adapters)，使它们能够连接到任何高级 API。这些 API 提供了更高质量的数据、更快的响应时间，并保证了可用性和服务质量。外部适配器是模块化的，可以用任何编程语言编写，并且可以由不同于 Chainlink 节点的服务器托管。它们可用于从数据提供商、web APIs、企业系统、物联网设备、支付系统、其他区块链等获取数据。

### 高质量节点运营商的分散化

如果没有安全可靠的 oracle 机制将数据交付给智能合同，数据质量就无从谈起。高质量[节点操作员](https://blog.chain.link/what-is-a-chainlink-node-operator/)的分散化是一个关键的设计模式，可以防止不可预测的停机时间，并消除信任单个实体不会篡改数据交付过程的需要。分散的共识大大增加了攻击的成本，因为即使少数节点经历停机或变得恶意，对最终的聚合响应也几乎没有影响。

Chainlink 的价格参考合同由分散的 oracle 网络提供支持，这些网络聚合了来自众多独立的、经过安全审查的、抗 Sybil 的 oracle 节点的响应。参与的 Chainlink 节点由分布在世界各地的领先区块链开发团队和安全团队运营，包括异地云中服务器和现场裸机服务器，以避免 oracle 机制中的任何单点故障。还有许多社区运营的备用节点可以随时添加到网络中，以实现进一步的分散化。

### 高质量数据源的分散化

只要不牺牲任何单个数据源的质量，Oracle 解决方案可以通过合并多个数据源变得更加健壮。高质量数据源的分散化防止单个数据提供者成为唯一的真实来源，并防止唯一的数据提供者离线的情况。然而，可能存在只有一个高质量数据源可用的情况，这是更高级的用于保护数据质量的加密技术变得更重要的情况，例如桩支持的服务协议(下面将讨论)、TLS 验证( [Town Crier](https://blog.chain.link/town-crier-and-chainlink/) 、 [DECO](https://www.deco.works/) 和[零知识证明](https://blog.chain.link/what-is-a-zero-knowledge-proof-zkp/))。

Chainlink 的价格参考合同在数据源级别是分散的。每个价格参考网络从多个独立且高度可靠的数据提供商处收集市场数据。这些数据提供商完全由优质数据聚合商组成，这些数据聚合商在所有交易环境中拥有全面的市场覆盖，包括 [Brave New Coin](https://bravenewcoin.com/) 、 [Kaiko](https://www.kaiko.com/) 、 [Amberdata](https://amberdata.io/) 以及许多其他知名的数据 API。然后，将每个数据点聚合起来，形成一个单一的参考价格，存储在链上，供合同使用，只需使用一个简单的读取功能。

### 开源可视化和监控

如果 DeFi 应用程序的智能合约是开源的，供公众实时监控，那么 oracle 提供数据的价格机制也应该是透明的。如果没有 oracle 解决方案的透明性，dApp 用户就无法验证数据的来源、哪些节点提供数据、响应延迟、oracle 网络的历史性能及其数据的准确性等等。

Chainlink 的每份价格参考数据合同都附有从链上数据中获得的[透明可视化数据](https://feeds.chain.link/)，这些数据展示了一组非常详细的信息，例如:

*   每个参考数据馈送的最新价格
*   哪些 DeFi 项目赞助和支持每个价格馈送
*   哪些经过安全审查的节点运营商正在保护价格馈送
*   何时应该进行更新
*   开始聚合所需的最小节点响应量
*   关于 oracle 网络整体和每个节点运营商的大量其他相关关键信息



![Chainlink Data Feeds](img/1cd446e88a028ab84ae8a6da6b9ae6a2.png)

<figcaption id="caption-attachment-2802" class="wp-caption-text">Chainlink 数据馈送使用 oracle 节点的分散网络为智能合约提供高质量的价格数据。</figcaption>





此外，可以在每个数据请求的基础上分析单个节点的性能，以查看节点是否能够成功完成数据请求。 [Chainlink Explorer](https://explorer.chain.link/) 允许节点运营商、数据提供商和用户研究网络中每个节点的性能，并准确了解采取了哪些步骤来确定沿途是否有任何错误。

## 使用 Chainlink 灵活获取数据

灵活性是通用 oracle 网络的重要组成部分，能够成为整个 DeFi 的标准。它使开发人员能够创建他们认为能够提供他们所需的安全性和可靠性保证的任何 oracle 设计模式。尽管 Chainlink 价格参考数据馈送利用众多数据聚合器的组合来生成全球市场价格，但 Chainlink 协议并不强制实施任何一种关于 oracle 网络如何构建或数据来自何处的设计模式。相反，它提供了市场上最开放的模块化框架来满足任何特定需求。

### 合并任何数据、节点集合和聚合模型

开发人员使用这些外部适配器将他们的智能合约快速连接到执行所需的任何数据源。他们还可以定制他们所需的精确分散量、他们想要从中提取数据的确切数据源、用于聚合数据的算法以及更新的频率。这为契约如何使用外部数据提供了最大的灵活性。



![Chainlink Market](img/13376fc19b8c56324b02b21b20e56f51.png)

<figcaption id="caption-attachment-2803" class="wp-caption-text">Market.link 是一个第三方网站，开发者可以在这里探索预建的外部适配器，这些适配器提供了广泛的数据源。</figcaption>





这种可定制的框架允许开发人员根据他们希望购买的安全性，轻松扩展或缩减其 oracle 网络。Chainlink 拥有最大的安全节点操作员池，以及许多竞争职位的社区节点，这些职位可以快速添加到任何 oracle 网络中，以获得额外的安全保证。此外，开发人员可以访问越来越多的预格式化数据源，这些数据源无需任何前期开发工作就可以包含在数据聚合中。

Chainlink 还提供了定制聚合的能力，通过使用平均、中值甚至更复杂的加权来源模型和异常值删除模型。这包括更新频率的灵活性，无论是使用基于时间的更新、价格偏差更新(例如，每 0.5%的价格变化)，还是具有多个参数的某种类型的混合方法。

### 数据提供者可以作为传统的 API 运行，也可以运行 Chainlink 节点

Chainlink 的灵活框架允许数据提供商定制他们如何向新兴的智能契约经济提供数据，要么作为传统的 API 业务运营，要么直接运行 Chainlink 节点。

传统应用编程接口
数据提供商可以选择与现在完全一样的运营方式，通过以法定货币提供的订阅模式向付费用户提供数据。Chainlink 节点可以订阅这些 API，并通过在其节点设置中利用 Chainlink 的外部适配器在链上中继其数据。这可以应用于任何当前现有的数据提供商，并且已经由 chain link Data Feed Oracle networks 用于生产，节点订阅高级数据提供商，如 [Amberdata](https://medium.com/amberdata/announcing-chainlink-amberdata-partnership-the-most-advanced-data-sets-accessible-on-ethereum-56c3b3359619) 和 [CoinGecko](https://blog.coingecko.com/coingecko-to-provide-cryptocurrency-market-data-for-chainlink/) 。Chainlink 也有已经为交换 API 制作的外部适配器，可用于像[币安](https://market.link/adapters/75425757-aa1c-407f-a057-86b3dd07cda1)和[比特币基地](https://market.link/adapters/7b6c35bb-1879-4530-929e-12429695e315)的节点。

这种模式非常强大，因为数据提供商不需要改变他们当前的业务模式或基础设施。即使数据提供商自己不愿意直接为智能合约市场服务，Chainlink nodes 仍然可以通过模块化外部适配器为开发人员提供他们所需的任何数据资源。这也允许节点订阅运行它们自己的 Chainlink 节点(如下所述)的数据提供者，以向它们的数据提供额外的分散。

**数据提供商作为 Chainlink 节点**
另一种模式是数据提供商运营 Chainlink 节点，将其数据直接出售给智能合约。这为他们提供了一种将数据货币化的新方法，并且已经被几家领先的数据提供商所利用，如市场数据聚合商 [Kaiko](https://medium.com/@kaikodata/kaiko-partners-with-chainlink-to-bring-cryptocurrency-market-data-to-smart-contracts-1a2f9f428465) 和 [Alpha Vantage](https://medium.com/alpha-vantage/alpha-vantage-chainlink-integration-blockchain-hitting-a-massive-milestone-954778e6c2a1) ，以及加密货币交易所 [Huobi](https://support.huobiwallet.io/hc/en-us/articles/900001616523-Huobi-to-Make-Exchange-Data-Available-to-Smart-Contracts-and-Huobi-Wallet-to-Run-a-Chainlink-Node) 。

数据提供者通过运行他们自己的 Chainlink 节点而获得的独特优势之一是对他们自己的数据进行加密签名的能力。用户和智能合约可以放心，直接来自数据提供商或交易所的 Chainlink 节点的价格数据在通往智能合约的途中没有被篡改，因为数据在链上广播之前使用其节点的唯一私钥进行了加密签名。然后，可以通过节点的公钥地址在链上验证已签名的数据，确保它具有直接来自源的高完整性。

通过这一框架，数据提供商可以直接向区块链广播数据，不再需要依赖外部行为者在链上为他们传送数据。这使数据提供商能够控制他们在链上广播数据的频率，并允许他们维护其数据的安全性——从数据生成到最终交付，再到消费智能合同。因此，数据提供商可以灵活地以独特的方式同时向多个不同的应用程序提供数据，例如，每分钟向一组应用程序提供更新，同时使用价格每变化 0.5%的价格偏差阈值机制来服务其他应用程序。



![Data Providers can sell their data to Chainlink node operators and/or run a Chainlink node directly](img/ba5de0c449746380e66a4c10a0939e67.png)

<figcaption id="caption-attachment-824" class="wp-caption-text">数据提供商可以将其数据出售给 Chainlink node 运营商和/或直接运营 chain link node</figcaption>





### 从一个网关向所有区块链环境销售

不能指望数据提供商了解每个区块链环境，并在每个环境上独立设置安全操作，尤其是考虑到区块链市场的新颖性以及缺乏了解每个环境的文档和开发人员。

所有区块链环境都可以访问 Chainlink 的 oracle 网络，既可以利用现有的外部适配器/启动器，也可以创建新的适配器/启动器来快速提供新的区块链。Chainlink 是开源的，因此核心开发人员可以集成 Chainlink，而无需任何外部许可，从而实现水平可伸缩性，而不会出现开发瓶颈。大多数领先的区块链，包括以太坊、[波尔卡多特](https://polkadot.network/chainlink-reaches-milestone-with-polkadot/)、[泰佐斯](https://www.prnewswire.com/news-releases/leading-tezos-developers-collaborate-to-bring-chainlink-oracles-to-the-tezos-ecosystem-301049831.html)、[宇宙](https://medium.com/kava-labs/kava-integrates-chainlink-as-its-official-oracle-network-to-bring-defi-to-cosmos-e31c2c2e929)等等，都已经将 Chainlink 原生集成到他们的网络中

这种设置为数据提供商和智能合约开发商提供了一个单一的网关，他们可以通过该网关销售和访问任何链上的数据，最终为 dApps 带来更多的链上数据，并允许数据提供商获得更多的收入。重要的是，这种方法的灵活性避免了数据提供者选择在哪里部署资源的需要。

### 建立数据和服务质量的加密经济保证

Chainlink oracle networks 将纳入由节点运营商和请求智能合同双方签署的具有约束力的[服务协议](https://github.com/smartcontractkit/chainlink/wiki/Service-Agreements-and-the-Coordinator-Contract)，该协议预先定义了节点在整个协议期间需要遵守的参数。这些参数设置了数据交付的条款(响应延迟)、数据质量(响应准确性)、链接数量(加密经济保证)、删减条件(惩罚)以及请求者定义的任何其他预定义条款和条件。节点运营商的报酬取决于能否成功满足这些参数，并最终及时在链上交付高质量的数据。这确保了运行自己的 Chainlink 节点的数据提供者在他们提供的数据保证方面具有最大的灵活性，为其数据的质量、可靠性和准确性带来了额外的信任和完整性。



![Binding Service Agreements create crypto-economic guarantees of data quality and delivery.](img/d04fd0efabb98667a765a86a900bc3a5.png)

<figcaption id="caption-attachment-825" class="wp-caption-text">绑定服务协议创造了数据质量和交付的加密经济保证。</figcaption>





### 使用信誉框架和节点市场做出明智的决策

管理灵活性的一个重要组成部分是为用户提供工具，使他们能够就整合到 oracle 网络中的部件做出明智的决策。它包括两个部分:信誉系统和节点市场。

**信誉框架**
信誉系统向用户提供展示节点运营商和/或数据提供商的历史业绩的链上数据的不可变记录。未来的请求者然后具有历史密码证明，用于确定哪些节点是可靠的，哪些是不可靠的。

通过第三方服务，Chainlink 节点可以直接相互比较，以了解哪些 oracle 节点比其他节点更可靠。这些站点显示了关于 Chainlink 网络的原始数据和精确统计数据，以及关于每个 oracle 节点的具体数据，包括事务计数、响应时间、获得的付款、成功率等。



![Reputation.link allows developers and users alike to get deep insight into the performance of Chainlink oracle networks, including each individual node and data source.](img/4feb659a9bb8623505dcf44fbff0fe1b.png)

<figcaption id="caption-attachment-826" class="wp-caption-text">Reputation.link 允许开发者和用户分析 Chainlink oracle networks 的性能，包括每个单独的节点和数据源。</figcaption>





**节点市场**
另一个重要的组成部分是有一个位置来发现 oracle 节点，过滤它们，比较它们，并最终选择它们在 oracle 网络中使用。Chainlink 节点有多个第三方节点列表站点，比如 LinkPool 的 [Chainlink Market。](http://market.link/)这使得开发人员可以完全控制他们的 oracle 网络将如何构建，因为他们可以准确选择他们信任哪些节点以及他们愿意为多少节点付费。

此外，每个节点操作员能够列出他们的认证、安全审查、身份证明、外部适配器、数据源和作业运行规范，这些规范详细说明了他们向智能合同提供的链外服务。运营商可以为他们提供的每项工作设定自己的价格和参数，创造一个自由市场经济，其中节点在众多不同的因素上竞争。



![LinkPool Chainlink node details](img/7c787b4d251a038b380d9a16d251c009.png)

<figcaption id="caption-attachment-2804" class="wp-caption-text">market . link 上的节点能够在链上建立它们的声誉，并将其显示给寻找可靠节点的开发者。</figcaption>





## 如何利用灵活性来构建价格预测，以避免大量数据来源风险

为了提供高质量的数据，在设计 oracle 机制时，有几个关键的攻击媒介需要考虑并预先防范。由于没有考虑到这些情况，开发者正在用用户资金冒巨大的风险，并最终将他们整个 dApp 的成功置于风险之中。

**交易量转移/交易所锁定**
加密货币市场不同于传统金融市场，因为没有交易所拥有资产的独家发行权，因此无法锁定用户并覆盖资产的整个交易市场。区块链技术是无许可的，因此任何人都可以在交易所列出加密货币硬币/代币，供交易者随时访问。由于这种动态，加密货币的数量分布在许多不同的交易所，并且可以在不同的交易所之间快速转移。如果要避免市场操纵攻击，将大部分交易量转移到不包括在数据汇总流程中的交易所，oracle 机制需要考虑这一点。

**闪电崩盘**
加密货币交易所通常缺乏足够的断路器，容易受到闪电崩盘的影响，其市场价格远远超出所有其他交易所的市场价格。即使是最大的交易所也会面临这种风险，而且多年来已经多次经历过这些问题。北海巨妖经历了一场[闪电崩盘](https://blockonomi.com/bitcoin-flash-crash-kraken/)，BTC/加元价格对从 11200 美元暴跌至 100 美元，跌幅近 99%。比特币基地经历了一次极端的闪电暴跌，ETH 一度从 322 美元跌至 0.1 美元。此外，在 2020 年初，加密货币衍生品交易所 Bitmex 经历了一次[闪电崩盘](https://www.coindesk.com/xrp-sees-flash-crash-and-quick-rebound-on-bitmex)，XRP 价格在一分钟内暴跌 60%，从 0.33 美元跌至 0.13 美元。

**质量稀释**
避免在没有质量控制标准的情况下实施分散化，以避免任何质量较低的数据源稀释汇总流程，这一点很重要。任何 oracle 机制都应禁止业绩不佳、声誉不明、安全基础设施未经验证的数据提供商和节点运营商加入。确保节点运营商和数据提供商拥有资源和知识，能够解决可能出现的任何问题，并设置警报和确保故障安全。

**请注意**，恶意攻击者不一定要成为有经验的开发人员才能利用这些攻击媒介。注意到这种机会的任何零售交易者或交易者小组都可以使用交易所的 UI 来操纵特定市场，并扭曲由有限市场覆盖范围的 oracle 生成的参考价格点。这极大地增加了攻击面，因为它向任何具有 internet 连接和 exchange 帐户的人开放了操纵设计不当的 oracle 的能力。

Chainlink 的价格参考数据合约是专门为减轻这些风险而设计的，它利用数据聚合器，而不是单一的交换 API 或交换 API 的集合。

### 高质量的数据聚合器提供所有价格发现环境的市场覆盖

Chainlink Data Feeds 专门使用数据聚合器，因为它们提供最强大的市场覆盖面，这一功能对于向与传统金融市场相比交易量仍然相对较低的市场提供准确数据尤为重要。当从数据聚合商处采购时，维护市场覆盖面的角色从 oracle 网络的创建者转变为专业的数据聚合商，因为 Oracle 网络的创建者可能不具备持续跟踪交易量的经验或资源。

这些数据整合者拥有遍布全球的全职团队，他们在维护准确的价格数据方面经验丰富，能够全面覆盖所有交易环境。它们考虑了流动性、交易量、时间等重要指标，以及这些指标在交易所之间的差异；它们还会消除任何异常值。这些特点使 Chainlink 的价格参考合同高度抵制量的变化，闪电崩溃和质量稀释。

Chainlink 的价格参考合同还利用多个数据聚合器强化价格数据，防止任何单一来源操纵结果数据点。这为 dApp 开发人员和最终用户提供了更好的安全性和可靠性保证，此外还使用了经过安全审查的节点运营商和一流的监控团队。



![The end-to-end process of Chainlink’s Price Reference Data contracts](img/6513addedd19bd9aac35a54cddb10433.png)

<figcaption id="caption-attachment-828" class="wp-caption-text">链家价格参考数据合约的端到端流程</figcaption>





## 在获取数据时不恰当地利用 Oracle 灵活性的主要风险

要全面了解部署 oracle 网络所涉及的风险，无论是不考虑容量变化还是仅从单个 API 获取资源，最好看一些现实世界中的例子，看看会出现什么问题以及这是如何发生的。

### 注意:避免基于单一交换的 Oracle 设计

从单个交易所获取价格数据的 Oracle 网络不仅没有针对交易所宕机、闪存崩溃和价格操纵的保护措施；它们的市场覆盖面也极其有限。虽然这种设置在波动性较低的时候看起来似乎是可行的，但当市场波动性增加时，价格发现就会出现，交易量会在不同交易所之间频繁转移。即使 oracle 更新以跟踪不同的交易所，新的价格点也可能非常不准确，因为市场变化并不总是以相同的形式出现。这就产生了一种情况，即尽管数据源已经改变，但它不能可靠地维持市场覆盖。

在这个视频中，Chainlink 的联合创始人 Sergey Nazarov 解释了使用单一交易所作为数据源的危险:

[https://www.youtube.com/embed/4qRz9_PC3iE?feature=oembed](https://www.youtube.com/embed/4qRz9_PC3iE?feature=oembed)

以下是从单一交易所撤出所带来的危险的逐步概述:

*   开发人员 Joe 编写了一个智能合同应用程序，它需要加密资产的外部价格数据。他决定构建一个 oracle 网络，从他首选的交易所——交易所 C 中提取价格数据。在他构建 oracle 的同一天，交易所 C 拥有该资产 80%的交易量；他认为这是一个“足够好”的解决方案。
*   一周过去了，用户存款在增长。虽然交易所 C 现在仅覆盖该资产 50%的交易量，但该资产的市场波动性很低，oracle 机制似乎正在发挥作用。Joe 认为他可以继续专注于为他的 dApp 开发更多的功能，而不是因为“它仍然在工作”而再三考虑 oracle 不断下降的市场覆盖率。
*   又一个月过去了，在半夜，乔醒来，接到电话通知他，他的 dApp 刚刚有数百万用户存款被取走。他很快发现大部分市场交易量从交易所 C 转移，这是他的甲骨文唯一的来源，现在只占资产交易量的 5%。这个交易所被一个鲸鱼交易者操纵，导致甲骨文报告了一个异常价格点，这为不公平地从无辜用户那里吸走大量价值提供了机会。

![A diagram showing how centralized oracles introduce a single point of failure](img/adde97397fbc3d6df20321c6400cfd48.png)

*   由于失去了用户的信任，Joe 的 dApp 现在已经死了，他作为一个有能力的开发者的声誉也受到了损害。如果他的甲骨文解决方案有适当的市场覆盖面，这种情况本来是可以避免的。

上面的例子显示了当 oracle 网络构建为仅从单个交换中提取数据时所产生的极端危险。市场覆盖率可以决定一款应用的成败，在闪电崩盘的情况下，情况可能会更糟。

## 固定交换聚合 Oracles 不考虑数量变化

直接从预先选择的交换中提取数据的 Oracles 很容易出现这样的情况，即数据量转移到未包括在原始聚合过程中的新交换中。虽然最初选择作为 oracle 网络数据源的交换在最初创建时可能是流动的，但不能保证将来这些交换中的数据量会保持不变。这降低了恶意行为者的攻击成本，因为只需要操纵资产总量的一小部分。

在该视频中，Chainlink 联合创始人 Sergey Nazarov 讨论了为什么通过安全的 oracle 机制适应交易所之间的交易量变化对于 DeFi 产品的安全性和可靠性至关重要:

[https://www.youtube.com/embed/Bkv4RRJ00cc?feature=oembed](https://www.youtube.com/embed/Bkv4RRJ00cc?feature=oembed)

虽然这看起来像是最小的攻击媒介，但请考虑以下情况:

*   另一位智能合约开发人员 Bob 目睹了 Joe 只使用一个交易所的错误，他决定构建一个 oracle，而不是从一系列预先选择的交易所(A、B 和 c)中提取加密资产的数据。他的想法是，通过取多个交易所的中间值，可以减轻市场操纵。

![A diagram showing how aggregated data equals better oracle reporting. ](img/17889cfcf1579a8dec7fba1a328ec869.png)

*   几周过去了，Bob 似乎确信他做出了正确的决定，因为他的 oracle 从多个交易所提取数据，即使在单个交易所被操纵的情况下，它也能继续提供准确的响应。因此，他将注意力转移到改进应用程序的核心业务逻辑上。当 Bob 在开发新功能时，他没有注意到已经出现了两个新的交易所，并捕获了 85%的加密资产量。

![A diagram showing how aggregated data leads to better oracle reporting. ](img/871b0500fc26b73149241659800b6123.png)

*   又过了几天，Bob 醒来后发现，就像 Joe 一样，他的合同被利用来窃取数百万用户存款。事实证明，虽然 Bob 为其 oracle 网络选择的交易所在最初构建时是流动的，但随着时间的推移，交易量转移到了初始聚合过程中未包括的新交易所。因此，他的甲骨文网络最终只有 15%的市场覆盖率，然后被利用 Bob 的智能合约应用程序的交易员操纵。

![A diagram showing how aggregated data leads to better oracle reporting. ](img/30fd50a69622f9029668c68365d116ac.png)

*   虽然 Bob 分散 oracle 数据源的想法是正确的，但他没有考虑交易所之间的交易量变化，也没有考虑新的未跟踪交易所可能捕获资产的大量市场交易量这一事实。即使新的交易所没有出现，交易量仍然可以集中到一两家交易所，这将使交易员能够操纵低交易量的交易所，并扭曲中值计算，对他们有利。

Joe 和 Bob 都缺乏足够的市场覆盖，因为他们试图使用 oracle 机制构建一个数据生成产品。他们本可以完全避免这种情况，让甲骨文从拥有数十年防止市场操纵和市场覆盖问题经验的数据聚合器中提取数据。

### 将低质量的 Oracle 解决方案与高质量的 Oracle 解决方案混合使用

这种防止异常情况的愿望导致一些人考虑使用多个不同的 oracles 来创建价格更新。虽然分散到许多 oracle 解决方案在理论上听起来是个好主意，但由于其他 oracle 机制在可靠性方面的缺点以及它们提供的数据质量差，它实际上会带来更大的风险。

我们认为，将 Chainlink 来自其价格参考数据网络的高度安全可靠的价格数据与来自未经验证且不太透明的 oracle 解决方案的质量较低的数据相混合存在巨大风险，这些解决方案也不支持高级 API 和/或直接来自 exchange APIs 的源市场数据。随着 DeFi 保护的价值增加，这种担心变得尤其重要，因为通过 oracle 机制中的弱点攻击 DeFi dApps 的动机也会增加。

想象一下三个 oracle 解决方案聚合在一起的情况:一个是 Chainlink 的价格参考数据，它使用高质量的节点从优质数据聚合器获取数据；另一个是 oracle，它从预先选择的一系列交易所 API 中获取价格数据；最后一种是 oracle 解决方案，它不支持凭据管理，因此只能连接到单一的低质量数据源或 exchange API。



![Combining Chainlink's high-quality data with low-quality data from insecure oracle solutions lowers the quality of the resulting aggregated data point.](img/a7290ef896ec1a04e07641f72994c1b8.png)

<figcaption id="caption-attachment-834" class="wp-caption-text">将 Chainlink 的高质量数据与来自不安全 oracles 的低质量数据相结合会降低最终聚合数据点的质量。</figcaption>



<figcaption></figcaption>



在这个例子中，

*   在右边， **Chainlink Data Feeds** 从多个高质量的数据聚合器中提取数据，产生一个涵盖所有交易环境的交易量和流动性加权的全市场价格，价格为 100 美元。
*   左上角的 oracle 解决方案从预先选择的一系列 exchange API(A、B、C)中获取数据，这些 API 当时仅占市场总量的 15%(不包括占市场总量 85%的 D 和 E)。这扭曲了结果数据点，导致 oracle 报告了错误的价格点 70 美元。
*   左下角的 oracle 解决方案只连接到**一个低质量的数据源，**由于市场波动性大，该数据源出现了中断。这个单点故障导致 oracle 报告价格为 0 美元。

当智能合约采用收到的三个值的中间值(0 美元、70 美元、100 美元)时，最终的合计价格是不准确的 70 美元，而不是正确的市场价格 100 美元。更糟糕的是，三者的平均值将导致价格在 57 美元左右。在这两种情况下，其他两个 oracle 解决方案提供的低质量数据稀释了 Chainlink 价格参考数据提供的高质量数据。

这种情况导致低质量的数据点更容易受到操纵，并稀释了 Chainlink 经容量调整的数据所提供的高质量数据。oracle 解决方案中的去中心化是关键，但它不应以牺牲数据或节点质量为代价。任何类型的数据混合都会威胁到 Chainlink 价格参考数据网络提供的价值质量。我们强烈建议不要使用未知来源的价格数据，不要使用考虑不周的计算方法，不要依赖没有额外数据的预测，不要依赖加密经济保证低于标准的预测。

## 为下一代应用程序提供高质量的数据

Oracles 和数据源是两个不同的组件，当它们组合起来提供全方位的端到端安全性时，必须具有同等的弹性。为了让可靠的 oracle 网络能够支持数十亿乃至数万亿美元的 DeFi 生态系统，所提供的数据质量必须安全可靠。Chainlink 始终将 oracle 机制的安全性和数据的可靠性放在首位，以创建一个安全的端到端设备，让 DeFi 在未来几年发展壮大并成为主流。

[![A clickable banner to a report detailing the Ultimate Guide to Blockchain Oracle Security](img/9ede9173a1fba83a6a8ec756c6b9e3a8.png)](https://chain.link/resources/blockchain-oracle-security)

<figcaption id="caption-attachment-3518" class="wp-caption-text">This guide gives a comprehensive breakdown on how to evaluate blockchain oracle security.</figcaption>



如果您是一个 DeFi 项目，并且希望构建自己的价格参考 oracle 网络或[使用现有的网络](https://feeds.chain.link/)，请访问我们的[开发者文档](https://docs.chain.link/)，参加 [Discord](https://discordapp.com/invite/aSK4zew) 的技术讨论，或[安排电话讨论集成](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog)。如今，您可以在 mainnet 和 testnet 上轻松集成一个或多个 Chainlink oracle networks，为您的智能合同增加更多安全性和功能。