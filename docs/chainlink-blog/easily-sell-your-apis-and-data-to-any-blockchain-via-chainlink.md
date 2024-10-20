# 通过 Chainlink 向任何区块链轻松销售您的 API 和数据

> 原文：<https://blog.chain.link/easily-sell-your-apis-and-data-to-any-blockchain-via-chainlink/>

[智能合同](https://chain.link/education/smart-contracts)是[数据/API 经济](https://blog.chain.link/understanding-how-data-and-apis-power-next-generation-economies/)和自动化的交叉产物，使用[区块链](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/)网络作为高度安全的基础设施，托管和自动执行直接基于数据输入的多方流程。一些例子包括:在收到市场数据后自动结算的金融衍生品合同，由天气数据直接触发的农作物保险支付，或者在物联网数据确认货物完好无损后自动进行的贸易融资银行支付。虽然数据驱动的智能合约经济的可能性是无限的，但有一个固有的问题，区块链没有内置的与外部系统对话和进行 API 调用的能力，这通常被称为[Oracle 问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)。

[**Chainlink**](https://chain.link/) **克服了 oracle 的问题，使数据提供商能够轻松地将他们的数据直接出售给所有区块链人，而无需投入任何额外的资源或运营任何新的基础设施。**在本帖中，我们将介绍数据提供商利用 Chainlink 软件及其 oracle 网络快速实现数据货币化的两种方法，以便在所有区块链网络中使用。

1.  **使用现有 API 销售**–在不到一小时的时间内将您的数据销售到 Chainlink 网络，无需对您现有的业务模式或后端基础设施进行任何修改
2.  **提供更可靠的数据**–通过在几个小时内在 Chainlink 网络上启动一个节点，销售更多数据，为您提供新的数据签名功能，在基于区块链的自动化解决方案中提高您数据的可靠性

在深入讨论每种方法之前，让我们简要地检查一下为什么[Oracle](https://chain.link/education/blockchain-oracles)对于将数据供应商和 API 提供者连接到智能合约是必不可少的。

## **为什么 Oracles 对于数据提供者是必要的**

智能合约是运行在区块链上的编码业务逻辑(如果 x 事件发生，则执行 y 动作)，使其执行具有内在确定性，其结果绝对正确。因此，智能合同比传统合同有更大的优势，因为它们保证合同将按书面形式执行，并且结果是不可改变的，从而减少了交易对手风险、对账纠纷和流程低效。然而，区块链以牺牲连通性为代价提供了这些强大的安全性和可靠性保证。与没有互联网的计算机类似，没有甲骨文的智能合同是孤立的业务逻辑，不知道现实世界中存储的数据或发生的事件。

Oracles 是连接区块链(链上)和现实世界(链下)的安全中间件，允许智能合约与 API 服务交互，既可以使用外部数据来触发合约的执行，也可以将输出发送到外部系统。简单地说，oracles 是数据供应商和应用编程接口提供商将他们现有的基础设施用于区块链网络的门户。Oracle 从 API 检索数据并将其发布到区块链网络，从智能合约向外部系统发送消息/指令，并执行各种验证技术以确保数据准确且不易被篡改。

![A diagram showing different inputs and outputs connecting to Chainlink oracle networks.](img/09b218059844593bc186c2fe4551e2b3.png)

Chainlink 已经确立了其作为 oracle 市场领导者的地位，提供高度审计的开源软件，为分散式 Oracle 网络提供支持，例如 Chainlink 的[价格参考源](https://feeds.chain.link/)。Chainlink 是高度通用的，区块链不可知论者；它可以在任何区块链上提供与任何外部 API 资源连接的任何智能合约，这意味着来自每个市场的数据提供商都可以通过 Chainlink 实现区块链。

## **通过 Chainlink 向全区块链同时出售数据**

有数百种不同的区块链支持金融、保险、游戏、全球贸易等领域的各种智能合约应用和用例。作为数据提供商，集成所有这些不同的链既耗时又耗费宝贵的资源，这些资源原本可以用于核心服务，而不是配置和维护基础架构。随着区块链技术的采用越来越多，区块链的数量只会继续增加，进一步消耗宝贵的资源和开发人员的带宽。

数据提供商可以将开发工作外包给 Chainlink 的区块链中间件，而不是与每个区块链单独集成，使用其 oracles 作为单一集成网关向任何连锁店出售数据。 Chainlink 已经在大多数领先的区块链建立，包括以太坊、比特币、Hyperledger、Polkadot、Cosmos、艾娃等等。此外，Chainlink 已经建立了一个简单的框架和奖金计划，以便在新区块链出现和用户采用增长时快速加入。这不仅允许现有的数据基础设施立即连接到当今所有领先的区块链，而且它为数据提供商提供了一个面向未来的解决方案，可以支持任何即将到来的可能变得流行的区块链。

![A diagram showing how Chainlink connects any blockchain to different inputs and outputs. ](img/cd9c7208e841edbf61b82ab46b6a4dbc.png)

## **以简单或高级的方式与 Chainlink 集成**

了解到将新基础设施引入已经建立和扩展的数据/API 经济所面临的挑战， **Chainlink 从第一天起就被设计为与现有的遗留数据和 API 基础设施完全兼容，无需任何后端修改或业务模式检修。**除了这种方法，我们还使现有数据供应商和 API 提供商能够非常轻松地运营他们自己的 Chainlink Node (Oracle ),以此作为扩展其产品供应和直接向 smart contracts 销售数据的一种方式。通过成为 Chainlink Node 运营商，他们拥有了向用户提供一套先进的数据来源保证并直接接受链上支付的内在能力，从而增加了收入并提高了数据的安全性。

使用 Chainlink 的这两种高度互补的方式为现有的数据供应商和 API 提供商提供了最大的灵活性，这些供应商和 API 提供商希望实现区块链，并进一步从他们的数据基础设施中获利。

### **利用现有的链式网络快速开始销售数据**

数据提供商可以在不到一个小时的时间内通过他们现有的 API 向 Chainlink 网络出售数据。节点的链式网络能够聚集对数据提供者的链上需求，发出对关键数据集有巨大市场需求的信号，同时允许数据提供者最大限度地减少他们在链上销售数据的初始投资。这也不需要改变您现有的业务模型，因为节点用传统的法定货币(如美元)支付您的 API 调用，与您的 API 的其他用户没有什么不同。已经有许多高质量的 API 提供者可以通过 Chainlink 访问，例如 Google BigQuery 数据集、CoinGecko、美国国家海洋和大气管理局(NOAA)天气数据等等。

**Chainlink 将运行节点和处理加密货币支付的所有复杂性抽象化，使数据提供商能够专注于提供高质量的数据。**这是整个智能合约经济的一大优势，因为它提供了一条清晰的路径，使全球所有数据都可以在链上获得，而无需让数据提供商承担彻底改造其后端系统或业务模式的责任，以使其与区块链兼容。这种模式加快了数据周期，导致更多智能合同的开发，从而产生更多用户对数据驱动型应用程序的需求。



![Data providers can monetize their data for the smart contract economy by selling to the Chainlink Network or running a Chainlink Node to sell directly to blockchains.](img/fc3376e428f98c74bb20cd96227ff8e3.png)

<figcaption id="caption-attachment-658" class="wp-caption-text">数据提供商可以通过向 Chainlink 网络销售或运行 Chainlink 节点直接向区块链销售来为智能合约经济货币化他们的数据。</figcaption>





### **加入 Chainlink 网络出售更可靠的数据**

对于相信智能合约的未来并希望在这个新的数据驱动型市场中赚取更多收入和建立良好声誉的数据供应商和 API 提供商，他们可以自己运行 Chainlink 节点，作为直接向智能合约提供原始签名数据(使用数字签名)的一种方式。Chainlink 从第一天开始就支持这一功能，并且已经被多家领先的数据提供商用于生产，包括 [Tiingo](https://blog.tiingo.com/tiingo-launches-live-chainlink-equity-price-node/) 、[美联社](https://www.ap.org/press-releases/2021/ap-chainlink-to-bring-trusted-data-onto-leading-blockchains)和 [AccuWeather](https://www.accuweather.com/en/press/accuweather-announces-live-node-on-chainlink-making-weather-based-blockchain-applications-possible/1062306) 。

我们的审计软件非常易于操作，我们可以帮助您快速设置，开始向每个区块链的智能合同销售原始签名数据。**通过使用 Chainlink Core node 软件签署您自己的数据，用户对数据的来源有了强有力的保证，允许系统依靠它来自动执行大额合同**。没有这样的能力，就很难开发大规模或高价值用例的自动化业务流程。

除了内置的数据签名功能，使用 Chainlink 的数据供应商和 API 提供商将获得仅在 Chainlink 网络上提供的各种专门的 oracle 技术，包括保护隐私的 oracle 技术，如 [DECO](https://www.prnewswire.com/news-releases/chainlink-acquires-deco-from-cornell-university-301120614.html) 、 [Town Crier](https://blog.chain.link/town-crier-and-chainlink/) 、 [Mixicles](https://blog.chain.link/breaking-down-mixicles-and-its-potential-to-unlock-enterprise-demand-for-defi-applications-on-public-blockchains/) 等。这些先进的 oracle 技术允许将机密数据直接出售给智能合同，而不会公开泄露这些数据，甚至不会泄露给 oracle 节点本身。因此，敏感和/或专有数据变得可货币化，而没有通常的隐私或盗版问题。

最好的部分是，数据提供商可以在不到 10 分钟的时间内快速启动 Chainlink 节点，并准备好向智能合约出售数据。Chainlink 是一种开源技术，就像 Linux 和 Python 一样，所以你不需要我们或任何人的许可来设置任何东西，你就可以走了。然而，如果你在这个过程中需要帮助，请不要犹豫，通过我们的[不和谐](https://discordapp.com/invite/aSK4zew)或通过[建立呼叫](https://chainlink.typeform.com/to/gEwrPO)来联系我们。

## **10 分钟后启动数据源的 Chainlink 节点**

既然你知道了为什么你作为一个数据提供商应该成为 Chainlink 网络的一部分，那就让我们向你展示一下如何去做。这将是在以太坊区块链上运行 Chainlink 节点的设置指南，但 Chainlink 是区块链不可知的，可以在任何链上工作，每天都有越来越多的集成发生。

运行 Chainlink 节点只需要几个简单的 DevOps 步骤。你只需要:

1.  虚拟机或机器
2.  postgres 数据库(10 GB 也可以)
3.  码头工人
4.  以太坊钱包
5.  以太坊客户端(如果你不知道，不要担心这是什么)

本文中的所有内容都在 [Chainlink 文档](https://docs.chain.link/docs/running-a-chainlink-node)中。对于更详细的分步说明，我们鼓励您前往那里，但本文可以向您展示如何使用快速入门模型进行设置。

### 第一步:[安装 Docker](https://docs.chain.link/docs/running-a-chainlink-node#requirements)

您可以检查您的具体机器类型，以了解如何做到这一点。例如，如果你使用的是 Ubuntu，你可以运行:

```
curl -sSL https://get.docker.com/ | sh
sudo usermod -aG docker $USER
exit
# log in again
```

### 步骤 2:创建一个`. env '文件

```
mkdir ~/.chainlink
echo"ROOT=/chainlink
LOG_LEVEL=debug
ETH_CHAIN_ID=1
CHAINLINK_TLS_PORT=0
SECURE_COOKIES=false
GAS_UPDATER_ENABLED=true
ALLOW_ORIGINS=*" > ~/.chainlink/.env
```

这将是运行链节节点所需的所有变量。

### 步骤 3:设置您的 ETH 客户端

为了与以太坊区块链互动，你需要一个节点来读写网络上的事件。我们可以运行以太坊节点，或者利用第三方以太网客户端服务。现在，我们将只使用 [Fiews.io](https://fiews.io/) 。它们可以自由启动，并且是专门为 Chainlink 节点定制的。只需注册一个密钥并获取与 mainnet 相关的 URL 然后运行:

```
echo "ETH_URL=URL_HERE" >> ~/.chainlink/.env
```

### 步骤 4:连接数据库

要运行 Chainlink 节点，您需要使用 postgres 数据库。最简单的连接方法之一是将数据库 URL 添加到。环境文件。这个外部数据库允许无缝的 oracle 客户端冗余(确保可靠性)，并且可以托管在任何云服务、自托管机器或其他设备上。

```
echo
"DATABASE_URL=postgresql://$USERNAME:[email protected]$SERVER:$PORT
/$DATABASE" >> ~/.chainlink/.env
```

### 第五步:启动它！

现在你可以开始你的链接节点了！

```
cd ~/.chainlink && docker run -p 6688:6688 -v ~/.chainlink:/chainlink -it --env-file=.env smartcontract/chainlink local n
```

第一次会提示你输入邮箱和密码，然后你就可以进入[http://localhost:6688](http://localhost:6688/)**登录 GUI 了。**

你被录取了。现在，您已经运行了一个 Chainlink 节点。

一种流行的运行 Chainlink 节点的方式是在云中，我们已经提供了一个[一步一步的视频](https://www.youtube.com/watch?v=t9Uknfw27IU)记录如何这样做。虽然我们不会在这里讨论运行链节节点的一些[最佳实践，但是要知道所有适用于数据库的最佳实践也适用于运行链节节点。您需要多重冗余、高可用性/正常运行时间和自动化灾难恢复，以便您的节点始终保持在线和高性能。](https://docs.chain.link/docs/best-security-practices)

## **结论**

很明显，对外部 API 的访问是加速区块链和智能合约采用的关键，这是一种已经在发展的趋势。链上可用的数据越多，构建的创新智能合约应用就越多，从而培养出越来越多的用户群来出售数据和构建智能合约。这一数据周期的规模和需求将继续增长，渗透到众多价值数万亿美元的行业，并使数据提供商受益，这些数据提供商在智能合约经济中作为外部数据的可靠来源，很早就建立了良好的声誉。

![A diagram showing a positive feedback loop of security and data in Chainlink oracle networks.](img/6263b6671e9afcd209dfc728b9127d50.png)

随着 Chainlink 已经拥有智能合约经济中最大的用户网络，数据提供商将获得潜在客户的巨大市场，以及使他们的任何数据/API 在任何区块链可用的工具，无论要求的保密级别如何。标准化的智能合同模板将会出现，当涉及到合同逻辑和 oracle 设计时，开发人员通常只是复制经过时间考验和行业认可的标准。**因此，作为最广泛采用的 oracle 网络的首选数据提供商，默认情况下将提供大量机会来快速扩大您的用户群，因为其他人也想在自己的设计中使用相同的模式。**

我们看到了数据供应商和 API 提供商利用 Chainlink 扩展其业务模式的巨大机会，并在未来支持分散经济和社会系统的基础设施中发挥重要作用。我们今天想帮助您快速连接，所以请随时安排[电话](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog)讨论您的集成，联系[不和谐](https://discordapp.com/invite/aSK4zew)的技术问题，或者关注我们的[文档](https://docs.chain.link/docs/running-a-chainlink-node)了解如何测试和运行 Chainlink 基础设施。

通过在 [Twitter](https://twitter.com/chainlink) 、 [YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA) 和 [Reddit](https://www.reddit.com/r/Chainlink/) 上关注我们，了解最新的 Chainlink 活动。