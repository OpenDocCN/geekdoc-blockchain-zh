# 使用链节储备证明使稳定圈更加稳定

> 原文：<https://blog.chain.link/stablecoins-and-proof-of-reserve/>

虽然[stablecoins](https://blog.chain.link/what-are-stablecoins/)在概念上不难掌握，但在实际操作中却很难实现，算法上的 stable coins 表现得更加复杂。借助 PoR(chain link Proof of Reserve ), stable coin 协议能够增强其稳定性和透明度，提供对其储量的实时了解，并增强用户和市场的信心。

### 是什么让 Stablecoins 变得稳定？

让我们后退一步，仔细考虑一下 [稳定器](https://blog.chain.link/what-are-stablecoins/) 到底是什么。稳定货币是价格与加密货币、法定货币或交易所交易商品(如黄金或工业金属)挂钩的加密货币。

当市场上各种其他资产价格波动时，投资者希望在波动性较小的资产中保持头寸，他们可以使用稳定债券。这就是为什么他们经常被描述为一种对冲(即保护/保险)的价值损失。稳定资产是指相对于参考资产保持稳定的价值。这就是“ [钉住](https://en.wikipedia.org/wiki/Fixed_exchange_rate_system) ”的意思——稳定的货币必须保持“钉住”另一种资产。最常见的情况是，钉住美元，一个单位的稳定硬币总是等于一美元。

也就是说，稳定货币的支持资产可以是任何稳定的法定货币或另一种稳定的价值储存手段(多年来，美元本身由真金“支持”，但那是另一回事)，包括其他类型的加密货币。

但是一枚稳定的硬币是如何保持其钉住汇率的呢？一种方法是稳定币发行者持有与稳定币等值或更高价值的资产作为“支持”或“储备”。这被称为抵押——支持资产(储备资产)充当抵押品。钉住不同于抵押——钉住是一种衡量稳定货币相对于储备货币的价值的方法，抵押使用资产来保护这一价值。

考虑抵押品的一种方式是这样的:如果一个你不太了解的人问你要 100 美元，你可能想知道如何拿回你的钱。你的资本损失是你想要防范的风险，所以你很可能会要求这个人给你一些有价值的东西来“担保”你给他们的贷款。他们可能会把车和车钥匙留给你。如果你需要，你可以卖掉汽车，收回你的钱。如果汽车的价值高于 100 美元，那么你就是“超额抵押”如果少于 100 美元，你就是“抵押不足”——对你这个贷款人来说，这是一个风险更大的位置。

如果发行者的资产储备价值等于或大于已发行的稳定币，则稳定币保持其钉住汇率。这样，价值 1 美元的稳定币持有者可以兑换(即赎回)这些稳定币，并获得价值 1 美元的资产或法定货币。这是一个 1:1 的挂钩。

### 稳定币的种类

大致上有三种类型的稳定硬币，根据它们用来保持稳定价值的机制来分类。它们可以是法定抵押、加密抵押或算法抵押。

前两种类型很容易理解，因为我们已经介绍了抵押品的含义，并补充说明了加密抵押的稳定债券完全是链上的，也就是说它们的抵押品本身也是链上的。

算法 stablecoins 略有不同。虽然稳定币由资产储备支持，但算法稳定币主要由数学和激励机制(编码在智能合约中)支持，保持与法定货币挂钩。它们可能没有潜在的储备资产——它们被设计成通过使用算法来控制稳定货币的供给(或者相反，需求),从而调节和稳定它们的挂钩汇率。事实上，算法稳定债券通常是——抵押担保，因为它们(理论上)不需要抵押品来保持它们的“稳定”价值。一些算法稳定币有一对硬币——一个是稳定币，另一个是支持稳定币的加密货币——算法操纵这对硬币来保持盯住，从某种意义上说，这使它们成为加密抵押稳定币的一个子类。

在这种情况下，有充分的理由采用不同的术语对担保稳定债券进行分类。像“常规”、“抵押的”和“算法的”这样的术语开始重叠，就失去了精确性。一些稳定的货币，如制造商 DAO 的戴和 Terra 的，被加密抵押 *和* 对抗另一种加密货币。一个比较好的分类可能是vs .*内源性*vs .*隐性* 抵押。外生的意思是“外于”，内生的意思是“从内”。“外源性”担保品是指在 stablecoin 项目之外有主要用例的担保品。“内源性”是指担保物是专门为担保物的目的而产生的。“隐含”是指设计缺乏明确的担保。你可以在这里 阅读更多关于这个 [。因此，Terra UST 和 Synthetix 的 sUSD 是与 *内源性* 担保物的稳定连接，因为它们的担保物标记被创建来支持稳定连接。区别于(例如)由 ETH 和等抵押的制造商 DAO。其中是因为它们有主用例以外的背衬戴。T44
T46】](https://arxiv.org/pdf/2006.12388.pdf#.)

更深入地探究这种区别，值得注意的是稳定的内容也可能在不同程度上分散。Vitalik Buterin 将分散式 stablecoins 称为“ [”自动化 stablecoins](https://vitalik.eth.limo/general/2022/05/25/stable.html#analysis) ”。分散算法 stablecoin 的一个显著例子是由 [MakerDAO 协议](https://awesome.makerdao.com/#faqs) 管理的[DAI stable coin](https://makerdao.world/en/faqs/dai/)。它由 DAO 管理，与美元挂钩，并由一篮子加密货币作为抵押品支持——这与大多数算法稳定货币的设计不同，后者没有抵押品支持。DAI 抵押品通常由其用户提供，用户可以在此之后铸造 DAI。DAI 硬币被视为向用户发行的债务，其发行利率实际上超过了发行的 DAI 的抵押品价值(即用户存放的抵押品价值通常高于他们作为回报获得的 DAI)。抵押品与 DAI 的比率是通过算法计算的，以保持 1 DAI = 1 美元的稳定挂钩价格。

你可以将这种稳定币设计与[【USDT】](https://tether.to/en/how-it-works)进行对比，这是一种由 [基于菲亚特的资产](https://tether.to/en/transparency/#reports) 支持(几乎完全支持)并集中控制(而非算法)的稳定币。另一个与美元挂钩并由等价资产支持的中央稳定货币的例子是 USDC。

所有这些都提出了一些非常重要的问题，这些问题围绕着关于稳定的权力下放和稳定性:

1.  我们如何知道支持稳定抵押品的准备金存在(特别是外源抵押品)？
2.  我们如何相信这些储备等于或大于它们所支持的稳定货币的当前市场价值？
3.  我们如何获得准确、实时的价格数据来支持算法稳定的货币挂钩？

### 高质量的链上数据是一个问题

解决这三个问题的传统的、集中的、离线的方法是由审计员人工核实和验证储备，由集中的交易所提供价格数据。然而，手动验证储量有一些缺点——它是手动的，很昂贵，是根据别人的计划完成的，不是自动完成的。

传统的第三方审计也缺乏透明度，因为他们仍然需要信任审计师和他们的诚信，相信他们的话没有篡改。我们指望审计师的自身利益会保护他们的声誉，这是一种“隐性激励”。

从历史上看，当涉及到实物资产，如黄金，甚至是由政府国库管理的中央控制的法定货币时，这种机制就其目的和环境而言可以很好地发挥作用。但是，这种技术的更高级版本，通过现代技术实现并消除了对中介的信任，将依赖于由分散的 oracle 网络保护的[](https://blog.chain.link/what-is-cryptographic-truth/)。

区块链的一个问题是他们无法连接到外部数据，这个问题被称为 [区块链 oracle 问题。](https://blog.chain.link/what-is-the-blockchain-oracle-problem/) 为了以分散的、安全的、加密真实的方式验证储量，区块链需要一种可靠的方式与链外数据进行交互。行业领先的分散式 oracle 网络 Chainlink 解决了这一问题，它在链上提供链外数据，并帮助整个 DeFi 领域获得数十亿美元的价值。

[Oracle](https://chain.link/education/blockchain-oracles)可以在跨多链生态系统向协议交付数据方面发挥强大的作用，Chainlink 能够验证储备的存在，根据市场条件准确评估储备，以低廉的价格向区块链交付数据，执行储备的自动审计，以及许多其他有助于提高稳定的资本的安全性和稳定性的功能。

### Chainlink 储备证明和价格反馈拯救世界

如果任何人、任何地方能够证实稳定币协议确实受到其声称拥有的储备的支持，并且储备的价值(市场价格)足以担保稳定币的供应，即使稳定币及其储备位于不同的区块链，那又会怎样？对稳定的硬币及其挂钩的信心会急剧增加。

想象一下，如果任何智能合约都可以对价格馈送进行两次简单的 API 调用——`getLatestSupply()`和`getLatestReserves()`——从而为稳定的硬币及其储备资产提供分散的、聚合的、密码保护的链上数量和市场价值。只要储备货币的供应量超过稳定货币的供应量，并且储备货币的价值至少和流通中的稳定货币数量的价值一样多，我们就知道稳定货币是完全抵押的，并且处于健康状态。

[【链环预留证明】【PoR】](https://blog.chain.link/verify-stablecoin-collateral-with-chainlink-proof-of-reserve/)异能正是这种功能。PoR 为 stablecoin 的用户提供了透明度，使他们能够直接并随时确认他们正在使用的 stable coin 资产是端到端安全的，并且不包含单点故障。这正是[true USD(TUSD)](https://www.trusttoken.com/trueusd)所做的，你可以 [在这里](https://blog.chain.link/what-are-stablecoins/) 了解更多。

![On-Chain Proof of Reserve Diagram](img/d79a016de03e684d9963e19bebc97d4a.png)

<figcaption id="caption-attachment-4069" class="wp-caption-text">On-chain Proof of Reserve</figcaption>



PoR 参考源为智能合约提供计算任何由链外储备支持的链上资产的真实抵押所需的数据。这些参考源由 Chainlink 网络上的分散式 oracles 网络操作，允许对协议中使用的抵押品进行实时自主审计，有助于确保用户资金免受不可预见的“部分”准备金做法和链外托管人的其他欺诈活动的影响。PoR 链环公司甚至可以横跨区块链做到这一点。

对于利用链外储备的稳定币协议，PoR 链结支持的重复审计有助于提高透明度并确保支持稳定币的储备的状态。使用 PoR 的稳定帐户可以向用户提供更高的透明度，因为他们可以证明他们的令牌是受支持的。PoR 还可以提供有关任何类型的挂钩资产的抵押数据，包括替代法定货币或黄金等商品，从而增加了利用这一机制的任何令牌协议的透明度。

![Off-Chain Proof of Reserve Diagram](img/ede90d4d3f9364ae236af38e5bfac68d.png)

<figcaption id="caption-attachment-4070" class="wp-caption-text">Off-Chain Proof of Reserve</figcaption>



例如，金融市场基础设施和加密经纪平台 Paxos 使用 Chainlink 提供智能合约所需的高可用性、防篡改和准确的定价数据，以验证支持稳定货币 Pax Dollar (USDP)的美元储备和支持 PAX Gold token (PAXG)的黄金储备。这是通过 Paxos 代币的 [Chainlink PoR 数据馈送](https://data.chain.link/ethereum/mainnet/reserves/paxg-reserves) 完成的，它授权 DeFi dApps 验证 Paxos 代币确实由 Paxos 保管的链外储备中持有的美元和金条 1:1 支持。

随着 [【中央银行数字货币】](https://www.investopedia.com/terms/c/central-bank-digital-currency-cbdc.asp) 开始出现，它们可能需要链上和链外资产的支持。这将需要关于其储备资产的准确和安全的价格数据。这些 [政府发行的 stablecoins 将由 Chainlink PoR、](https://chainlinktoday.com/how-chainlink-unlocks-the-value-of-cbdcs/) 很好地服务，它们可以提供帮助保护其挂钩所需的定价数据以及验证抵押所需的储备数据，所有这一切都通过分散的 oracle 网络来保证加密的真实性。

Chainlink 准备金证明不仅有助于验证基础资产，还有助于防范系统性冲击。例如，利用 Chainlink Proof of Reserve 数据，DeFi smart contracts 可以在抵押贷款下降到正常健康范围之外的情况下实施“断路器”作为故障保险，有助于减轻潜在的灾难性市场波动和价值破坏。

### 总结

Stablecoins 是 DeFi 生态系统的重要支柱，使用户能够存储和转移稳定的价值。stablecoins 有多种实现方式，但所有 stablecoins 的稳定性和透明度都可以通过更高质量的数据和探明储量的能力来增强。有了 Chainlink 价格馈送和 Chainlink PoR，stablecoin 协议有了两个增强其安全性和稳定性的强大工具。

如果您是一名开发人员，并且想要将 Chainlink 集成到您的智能合同应用程序中，请查看 [【区块链教育中心】](https://blockchain.education) ， [开发人员文档](https://docs.chain.link/docs) 或 [联系专家](https://chainlink.typeform.com/to/gEwrPO) 。您还可以在此处查看 [live Chainlink 预留数据证明](https://data.chain.link/ethereum/mainnet/reserves) 和 [在您的智能合约](https://blog.chain.link/verify-stablecoin-collateral-with-chainlink-proof-of-reserve/) 中实现它们。