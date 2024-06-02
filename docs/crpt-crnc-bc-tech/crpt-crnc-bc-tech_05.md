# 加密货币的市场结构

Jiri SvecSean FoleyAngelo Aspris

加密货币是一种可以通过数字货币交易所由不同交易团体交易的电子媒介。随着世界上许多国家在理解适当的投资者保护规则方面进行的监管斗争，过去十年中看到了加密货币交易所的激增，越来越多的山寨币列表出现。尽管没有中央机构来注册这些交易所，但据估计，目前流通中有多达五百个交易所，它们具有不同的平台、地理覆盖范围和遵守监管框架的特点。加密货币市场与外汇市场和股票市场有许多相似的特征，如限价订单簿和匹配算法，以及可以 centralised 或 decentralised 的交易所。由于这些市场仍处于起步阶段，它们将来会采取什么形状或形式将取决于消费者、投资界以及全球监管机构的接受程度。

## 1 用加密货币进行交易

比特币（以及其他）区块链上的所有交易都是公开记录的。这使得所有用户都能确定现有所有钱包的余额。然而，区块链只适用于在用户之间转移加密货币的单位。当用户想要用他的/她的加密货币换取一种资产——比如一个披萨时，比特币从消费者到比萨店的运动将是可见的，然而披萨的交付将不会被记录。同样，在用比特币换取现金的销售中，比特币的转移将被记录，但不会有法定货币价格支付的记录，也不会有法定货币的实际交付。

Yermack (2015) 和 Baur et al. (2018) 以及 Foley et al. (2019) 表明，目前大多数加密货币交易都是投机投资者之间进行的，只有很小一部分用于商品和服务的购买。因此，它们更像是一种投机投资，而不是货币。即使从法律和税收的角度来看，在许多司法管辖区，加密货币被视为代币、虚拟资产或商品，而不是货币（无论是数字的、网络的还是电子的）。¹

## 2 建立交易所

随着加密货币成为可交易资产，出现了许多市场，最早的是现在臭名昭著（且已倒闭）的“Mt Gox”。加密货币的去中心化性质要求交易所扮演“保管人”的角色。要在交易所出售比特币，需要将比特币存入由交易所控制的私钥地址。这个地址通常被称为“热钱包”，并直接连接到互联网。这类似于银行柜员持有的现金量：余额不是无限的，但对于日常存取款是有用的。一旦热钱包中的余额变得过大，大多数交易所会将他们的加密货币供应转移到“冷钱包”中——这通常是一个离线持有的账户，需要多个人访问（多签）——类似于需要三个不同钥匙才能打开的银行金库。

交易所控制着系统内所有的加密货币。加密货币的存取款将出现在公共区块链上。然而，一旦加密货币被交易所持有，交易所就需要负责跟踪哪些比特币属于哪个用户。

## 3 交易和费用

加密货币的市场结构与现代股票市场相似，都通过限价订单簿进行连续交易，且没有中介。交易者可以选择立即执行的市场订单，或者等待更好执行价格的限价订单。限价订单存储在限价订单簿中，并根据价格时间优先原则执行。没有指定市场制造商的订单驱动市场主要依赖内生流动性提供者（ELPs）来提供流动性，因为这是有利可图的。由于 ELPs 无需维持市场的义务，当流动性提供变得有风险或无利可图时，它们可以撤出，这会对市场质量产生不利影响（Anand 和 Venkataraman，2016）。为了增加 ELPs 在市场中的参与度，大多数加密货币交易所使用制造商-消费者模型来区分提供流动性的订单和移除流动性的订单。制造商-消费者模型通过向要求立即执行的交易者收取更高的费用，并向为市场提供流动性的 ELPs 收取较低的费用（或无费用）来减少不理想的交易行为。对于中等规模交易的典型费用，消耗流动性的交易者在 10 到 30 个基点（bps）之间，而市场制造商在 0 到 15 个基点之间，具体取决于交易的加密货币。费用通常按过去 30 天内执行的价值（美元等值）计算。

### 3.1 交易是如何报告的？

由于只有在用户将加密货币存入或从交易所提取时才会记录在区块链上，因此那些存入法定货币、购买比特币、在交易所内持有并在稍后以盈利为目的的同一交易所出售的用户不会在区块链上产生任何记录。实际上，交易所内发生的交易本身在区块链上根本不会被记录，除了由交易所记录外。许多交易所将这种交易级别的数据公开，然而这完全是与区块链本身分开的。就像彭博社对股票市场一样，组织机构如[cryptocompare.com](http://cryptocompare.com)和[tardis.dev](http://tardis.dev)提供了交易所级别交易的历史和实时数据访问。

### 3.2 如果交易所被黑了会发生什么？

将加密货币资产存入交易所使个人面临重大的交易对手方违约风险。简单来说，如果一个交易所破产或被黑，投资者可采取的补救措施很少。加密货币的“信任更少”的特性意味着没有办法取消或恢复丢失的加密货币资产。随着加密货币的普及和价格上涨，它们也日益成为网络犯罪分子的攻击目标。在过去的几年中，许多交易所遭到黑客攻击——下面列出的一些较为知名的攻击事件，代表了全球加密货币交易市场上的一些最大名称：

+   2011 年 – Mt. Gox – 一名审计员通过审计盗窃了 2,643 个比特币。

+   2012 年 – Bitfloor – 备份服务器上的 24,000 个比特币通过未加密的私钥被盗。

+   2013 年 – Vicurex – 攻击者盗窃了 1,454 个比特币，导致交易所破产。

+   2014 年 – Mt. Gox – 攻击者盗窃了 850,000 个比特币，导致交易所破产。

+   2015 年 – Bitstamp – 通过针对员工的钓鱼攻击盗窃了 19,000 个比特币。

+   2016 年 – Bitfinex – 通过他们的支付处理器 BitGo 被盗走了 120,000 个比特币。

+   2018 年 – QuadrigaCX – 在 CEO 可疑死亡期间，19 亿美元的加密货币资产丢失。

+   2019 年 – Binance – 通过钓鱼诈骗盗窃了 7,000 个比特币。

随着用户对黑客攻击的担忧日益增加，交易所本身也采取了一系列回应措施。例如，2016 年 Bitfinex 黑客攻击的受影响客户获得了“BFX”代币，以代替被盗窃的比特币。这些代币代表了 Bitfinex 对其用户所欠的比特币的“我欠你”。在 244 天内，所有被盗的比特币都得到了偿还。通常，交易所会破产，使它们的用户成为无担保债权人。2017 年，一种名为“去中心化交易所”的创新在以太坊平台上推出，将加密货币资产的保管从交易所移交给用户。

对市场基础设施的健壮性、账户安全、高波动性和低流动性的担忧与有限的监管相结合，降低了加密货币对受严格监管的机构投资者的吸引力，因此到目前为止，这些投资者在很大程度上已经远离了加密货币市场。

## 4 交易所的类型

全球范围内有数百个加密货币交易所。截至 2019 年，[Coinmarketcap.com](http://Coinmarketcap.com)列出了超过 285 个交易所的交易量。这些交易所中的大多数被称为“中心化”的，因为有一个单一的、值得信赖的对手方负责运营限价单簿，接受法定货币和加密货币的存款/提款，遵守“了解你的客户”（KYC）规定，并为市场内存款的资产担任保管人。相比之下，“去中心化交易所”（DEXs）本身不保管任何资产，通常不由任何个人运营，不会破产也不会被黑客攻击。

### 4.1 中心化与去中心化交易所

典型的交易所（例如，Binance, Bitfinex, Poloniex, Kraken, Bitstamp）是中心化的，其运营方式对参与纽约证券交易所（NYSE）和纳斯达克（NASDAQ）等传统股票交易所的参与者来说很熟悉。每个交易所选择交易哪种加密货币（例如比特币、以太坊、莱特币）以及创建哪些货币对的市场（例如欧元/比特币、美元/比特币、以太坊/比特币）。用户可以存入加密货币和/或法定货币，并在中心化限价单簿中交易这些资产。尽管这些市场在技术上都是独立运行的，但套利通常会保持这些市场同步，类似于全球外汇市场（参见，Makarov and Schoar, 2019）。

这些市场通常遵循价格-时间优先原则，价格粒度有不同层次，通常达到 8 位小数（Dyhrberg et al., 2018）。这使得定价可以非常精确，确保愿意以更好价格交易的交易者的订单先执行。

以太坊网络上的智能合约（以及使用 ERC20 代币在以太坊平台上进行的大量首次代币发行）使得限价单（限价单市场的基本需求）可以编入自我包含的合约中。智能合约可以编码为提供 N 个 ERC20 货币单位，以换取 E 个以太坊单位。用户可以发送一个“市价”订单，交付 E 个以太坊单位，并自动接收 N 个 ERC20 单位。这样的合约与限价单完全相似。

此类订单的聚合可能形成一个虚拟的“限价单簿”。例如，提供 10 个 XYZ 以换取 1 个以太坊的报价将优于提供 9 个 XYZ 的报价，但不如提供 11 个 XYZ 的报价。

为了作为一个市场有效运作，去中心化交易所（DEX）的用户需要观察所有可用的订单，按价格优先级排序它们，然后选择与哪些订单进行交互。最早的 DEX（即 OasisDex 和 EtherDelta）采用了*完全基于链上*的执行方式。这意味着所有的订单录入、执行和取消都是由以太坊区块链本身处理的。因此，订单匹配的速度受到了以太坊区块时间的限制（目前为 14 秒）。下面的图 1 展示了完全基于链上的 DEX 的运作情况。

![](img/b_9783110660807-006_fig_001.jpg)

图 1 完全基于链上的去中心化交易所的运作情况。

很快就很明显，依赖以太坊网络（并支付费用）来录入、修改或取消订单将严重限制 DEX 的增长。这导致了*混合交易所*的创建，如 IDEX 和 0×，其中一个中心化组织在链下（类似于中心化交易所）汇总所有的订单录入、修改和取消，但保管和结算（在匹配得到确认后）是在以太坊区块链上进行的。集中化限价订单簿使得交易确认速度大大加快，并减少了需要支付矿工更新过时限价订单的成本约束。然而，这也引入了一个单一的、中心的故障点和中止点。下面的图 2 展示了使用链下订单簿并利用链上结算的去中心化交易所的运作情况。

![](img/b_9783110660807-006_fig_002.jpg)

图 2 链下去中心化交易所的运作情况。

### 4.2 去中心化交易所的优点

去中心化交易所为用户提供了许多优于传统交易所的潜在优势。这包括：因为没有对手方的违约风险，因为交易所从未保管过您的代币；因为没有实行 KYC 规定，因为（与种子文件类似）没有中心化的实体可以强制任何规定；能够立即列出几乎任何代币；以及在真正去中心化的环境中能够免受任何政府基于的审查。正因为这些原因，DEX 吸引了越来越多的用户和交易量，如图 3 所示。尽管 DEX 中的交易活动正在增长，但这些场所执行的交易数量与中心化交易所相比相形见绌。

![](img/b_9783110660807-006_fig_003.jpg)

图 3 去中心化交易所的交易量。

### 4.3 去中心化交易所的缺点

尽管去中心化交易所（DEX）的性质正在迅速变化，但目前 DEX 存在许多限制，这些限制阻碍了它们的广泛采用。这包括：一个允许所有用户查看与所有交易相关联的地址的公共交易账本；无法在（目前基于以太坊的）智能合约环境之外交易代币（例如，法定货币和比特币无法交易）；由于依赖底层区块链，交易速度较慢；以及由于依赖智能合约，流动性较低和基本的订单类型功能。DEX 的另一个缺点是，它们不会严格实施价格时间优先原则。结合加密货币交易的复杂性和高精度（许多小数点），这意味着错误可能非常昂贵——错过一个小数位可能会导致 10 倍或更多的套利机会。这导致了所有 DEX 上出现各种定价错误，使参与者损失了 significant profits。

### 4.4 加密货币的可投资性

近年来，加密货币的价值迅速上升。2017 年 12 月，比特币价格短暂触及 20,000 美元，仅比特币市值就超过 3000 亿美元。但加密货币的投资吸引力有多大呢？Dyhrberg 等人（2018）通过估计 Gdax、Gemini 和 Kraken 等加密货币交易所之间比特币/美元汇率的有效交易成本和日内交易模式来探讨这一问题。与报价驱动市场不同，在这些市场中，由于一些交易发生在买卖价差内，有效价差通常小于报价价差，而完全电子订单驱动的加密货币市场中的交易者无法在报价内交易。此外，由于报价深度非常小，订单量经常超过最佳挂单深度，交易经常不能以最佳价格执行。因此，交易者被迫向上调整限价订单簿，有效价差通常大于报价价差。Dyhrberg 等人（2018）发现，这三个加密货币交易所之间的报价价差从 0.54 到 7.80 不等，而有效价差从 5.60 到 22.51 个基点。这比 NYSE 股票的平均报价（有效）价差 37.2（23.9）个基点、澳大利亚证券交易所的 32（27）个基点、Euronext 集中电子订单簿的 25.9（25.0）个基点以及 LSE 混合订单驱动段的 70.5（40.2）个基点要窄得多。Boehmer 等人（2005）的研究表明，比特币价差与 NYSE 上最流动的 100 只股票相当，这些股票的平均报价（有效）价差为 10.9（7.3）个基点。Dyhrberg 等人（2019）在 Gemini、Gdax 和 Kraken 等加密货币交易所之间比特币/美元汇率的有效交易成本和日内交易模式进行了平均。所有变量均为每小时平均值，按变量平均值进行缩放。Dyhrberg 等人（2019）。

图 4 展示了 2017 年 9 月 7 日至 2018 年 5 月 10 日，在美国交易所比特币市场中的流动性、买卖价差和波动性的日内变化。由于加密货币市场是连续交易的，图表更符合外汇市场通常发现的日内走势，并未描绘出股票市场中交易者行为所特有的 U 型买卖价差和波动性。

![](img/b_9783110660807-006_fig_004.jpg)

图 4 2017 年 9 月 7 日至 2018 年 5 月 10 日，Gemini、Gdax 和 Kraken 等加密货币交易所之间比特币/美元汇率 volume、报价价差和波动性的日内变化。所有变量均为每小时平均值，按变量平均值进行缩放。Dyhrberg 等人（2019）。

图 4（Figure 4）显示，在美国东部时间早上，随着欧洲市场的开盘，交易活动有所下降，随后随着美国市场的开盘而上升至高峰。交易随后在美国市场收盘时下降，并在亚洲市场收盘时进一步下跌。波动性遵循相同的模式，但高峰和低谷并不那么明显，而报价和有效价差与流动性和波动性显示出反比关系。这种独特的日内模式表明，美国加密货币交易所的交易主要在白天产生，这与零售投资者执行订单的情况相一致。有趣的是，周末也会产生类似的模式，这与外汇市场上通常观察到的沉闷交易活动形成对比。

![](img/b_9783110660807-006_fig_005.jpg)

图 5 投资者在不同交易规模下能够在订单簿的前十级别交易加密货币的比例（从 2017 年 8 月 1 日至 10 月 5 日）。所有货币对均换算为美元。

为了更好地衡量加密货币的可投资性，图 5 显示了在不同货币对（比特币（XBT）、以太坊（ETH）、以太坊经典（ETC）、莱特币（LTC）和美元）之间，买入或卖出方能够吸收不同规模的流动性冲击的比例。该图显示，投资者通常可以在订单簿的前十级别内交易 500 美元至 1000 美元。然而，对于更大的机构交易通常深度不足。XBT/USD 货币对为执行较大订单提供了最好的前景。

### 4.5 加密货币衍生品

2017 年 12 月，芝加哥商业交易所（CME）和芝加哥期权交易所（CBOE）为新兴的加密货币金融期货交易铺平了道路，推出了各自的现金结算比特币期货交易合约。推出金融期货合约旨在为机构投资者、投资基金会、矿工和零售投资者提供一个受监管和集中的市场，对 Bitcoin 的价格和波动性进行投机。² 用户还将从金融衍生品提供的风险管理机会中受益，这些机会来自于即期货币价格变动。CME 上比特币期货的推出被许多观察者视为数字货币合法化的重要一步，可能会将加密货币提升为公认的新兴资产类别。

CME 的比特币期货基于伦敦时间下午 4:00 的 CME CF 比特币参考利率（BRR）。参考价格在发表前汇总了全球加密货币现货交易所执行的订单流，包括 Bitfinex、Bitstamp、Coinbase、Genesis Global Trading、itBit 和 Kraken，在一个特定的计算窗口内。³ 每个相关交易的价格和大小被记录并添加到一个列表中，该列表在下午 3:00 至 4:00 之间被划分为 12 个 5 分钟的等权重时间间隔。在每个分区中，对这些组成部分交易所的成交量加权中位数交易价格进行计算，BRR 随后通过取所有分区的成交量加权中位数的等权重平均值来确定。⁴ BRR 是由 CME 集团和 Crypto Facilities Ltd（CF）⑤设计的，基于 IOSCO 金融基准原则⑥，是每天以美元计价的一个比特币的参考利率。这个基准的选择旨在提高基础现货市场的弹性和可复制性。

比特币期货交易在 CME 的 Globex 平台上进行（通过 Clearport 进行场外交易），从周日到周五，从下午 5:00 持续到次日凌晨 4:00，每天有 60 分钟的休息时间。市场由市场制造商计划支持，以确保其参与者有足够的流动性。比特币交易的费用比股指期货（大约高 3 倍）定价显著溢价。⁷ 比特币期货的保证金要求也显著高于其他工具。比特币期货的维持保证金目前约为 37%（相比之下，E-mini S&P 500 期货为 4%），其中对冲者（投机者）的初始保证金为维持保证金的 100%（110%）。这些要求可能会发生变化，CME 保留实施头寸限制或额外资本要求的权利。这种交易和清算由商品期货交易委员会（CFTC）监管。

自 2017 年推出以来，CME 已经见证了超过 20 次期货到期结算，有超过 3,300 个个人账户每天交易大约 7,000 个 CME 比特币期货合约。合约单位为 5 个比特币，每个合约的最小价格波动为 25 美元。截至 2019 年 9 月，单个 BTC 合约的价值约为 50,000 美元。

科伯特等人（2018）研究了比特币期货和现货价格之间的关系，发现基础资产在价格发现方面领先于期货合约。他们认为，金融工具和市场结构可能在这种令人惊讶的关系中发挥作用，并评论称，缺乏大量机构投资者的参与可能会阻碍其在价格发现方面的贡献。对商品期货交易委员会（CFTC）交易者承诺报告（COT）的分析显示，“杠杆基金”和“其他应报告者”在 BTC 期货的持仓兴趣中占据主导地位，而机构投资者（资产管理师）只持有少量的兴趣。截至 2019 年 9 月，资产管理师（机构）对于多头和空头头寸的持仓兴趣分别仅为 6.3%和 4.8%。在《金融期货交易者》（TFF）中，杠杆基金被定义为可能参与管理和进行自有期货交易以及代表投机性客户交易的交易者。⁸ 与此同时，其他应报告者是指未被归类为交易商、资产管理师或杠杆基金类别的交易者，主要由持有不到 25 个比特币合约的零售交易者组成。CFTC 应报告数据中持仓较小的交易者的相对较高比例，使其与其他更显著的金融市场合约区别开来，这表明它可能是该市场价格发现不足的一个因素。

鉴于比特币期货的成功，2019 年 9 月，CME 集团宣布，将在 2020 年第一季度等待监管审查后，提供其比特币期货合约的期权。这些期权旨在为客户 提供更多用于精确对冲和交易的工具。

## 5 加密货币特定的交易问题

### 5.1 套利

尽管加密货币交易所的实物交易与其他股票交易所的交易相当，但相对价位大小，即最小允许的交易价格增量为价格的百分比，远小于股票交易所。价位大小的选择是交易所为影响整体市场质量所做的最重要的决策之一。价位大小决定了超越挂单优先权的价格成本，并决定了最小的买卖价差，这是交易成本的主要组成部分。随着加密货币价格的上涨，尤其是比特币，相对价差变得越来越小，不受约束。在大多数加密货币交易所中，要么是 1 美分（例如，Bitstamp 和 Coinbase），要么是 10 美分（Bitfinex），当一个比特币交易价格约为 10,000 美元时，导致相对价位大小低至 0.01 个基点。

由于交易增量为如此之小，对于交易者来说，通过微不足道的量提高限价订单来获得优先权相对便宜，如图 6 所示。这种“做空”行为消除了交易者提供流动性的动机，并鼓励他们穿过价差以被执行，导致最佳报价的深度降低，并恶化报价价差。

![](img/b_9783110660807-006_fig_006.jpg)

图 6 2017 年 8 月 2 日 BTC-USD 的买入和卖出报价以及交易价格(Dyhrberg 等人, 2019).

Buti 等人 (2019) 开发了一个公开限价订单簿的理论模型，以分析价格变动幅度对市场质量的影响，并显示了在不受约束的价差证券市场中，随着价格变动幅度的增加，市场质量可以得到改善。 several exchanges have recognised that small tick sizes can lead to excessive undercutting behaviour and have begun to increase tick sizes for many of the currency pairs to improve market quality.⁹ The following excerpt from a Kraken press release in 2017 highlights the impact of rising cryptocurrency prices on the prevalence of undercutting.

> 减少价格精度将有助于减少订单簿中的额外活动，因为交易者通过一个非常小的分数不断跳到对方前面。我们收到了许多客户对此减少的请求，它将通过更有效的订单簿减少交易引擎的负载。
> 
> （Kraken 新闻稿，2017 年 8 月 26 日）

Dyhrberg 等人 (2019) 确认，Kraken 上的较宽价格变动幅度改变了交易者的行为，显著减少了做空，并导致市场质量的整体改善。图 7 显示了 2017 年 8/9 月 tick size increases 前后，S&P 500 指数的成分股和 Kraken 上的货币对的相对报价价差和相对价格变动幅度（bps，对数刻度）。

![](img/b_9783110660807-006_fig_007.jpg)

图 7  Kraken 与 S&P500 股票的相对价格变动幅度和相对报价价差比较(Dyhrberg 等人, 2019).

### 5.2 做空限制

在金融理论中，允许理性套利者无限制地借入以进行做空是一种必要条件，这对于有效的资本市场至关重要。它与价格发现和市场流动性的提高相关，然而这并不是区块链的固有特征。用户不能花费他们没有的加密货币；然而，这并不排除用户采取与这种货币价值相关的金融头寸。

> *如果有一个简单的方法做空，我会这么做*¹⁰
> 
> 比尔·盖茨，微软联合创始人

在 Cboe 和 CME 上市比特币期货之前，想要做空比特币（或其他山寨币）或进行某种形式的风险管理的使用者仅限于少数几个平台。最受欢迎的做空平台是 Bitfinex 和 Poloniex。在做空交易中，卖方进行常规的现货销售，不同的是交易通过交付借来的加密货币来结算。在这方面，做空加密货币与做空上市证券相似——做空者必须找到可借的货币。加密货币可以在交易所上借出（例如 Bitfinex 或 Poloniex），通过点对点功能，这意味着借款人是从其他参与者那里借的，他们将收到以利息形式支付的回扣。回扣将取决于贷款期限，利率将随时间变化。加密货币借款人可能会寻找借款数字货币的出价或做出投标，并且不允许超过某些杠杆阈值。例如，Bitfinex 上的比特币借款人不被允许借入超过短售比特币的 70%。任何短售的法定货币收益都用作借入比特币的抵押品，直到这些比特币被偿还。

考虑到零售交易者做空比特币（以及其他山寨币）的门槛过高，一些经纪商，例如 Plus500 和 eToro，已经建立了替代性的做空选项，例如差价合约（CFDs）。CFD 的操作方式与期货合约相似，投资者可以对标的资产进行投注，而不必实际拥有它，从而允许建立空头头寸。

北美衍生品交易所（Nadex）是一家位于美国的受监管交易所，向投资者提供二元期权和价差。¹¹ 价差可以用来限制风险，同时获得比特币多头和空头曝光。这些合约以美元结算，因此不需要实际拥有物理资产。

为了克服点对点加密货币交易平台流动性问题（特别是某些山寨币），最近已经探讨了使用加密货币资产的回购市场。回购可以被看作是一种以抵押品为担保的贷款，不同之处在于抵押品不是抵押，而是出售并在到期时回购。通过在这个环境中为加密货币资产持有者提供贷款能力，专业市场参与者可以为采取或覆盖空头头寸的目的借款。提供这一服务的当前平台示例是 Oxygen。¹²

最后，预测市场也为做空加密货币提供了可能的方法。这些市场允许投资者创建一个事件来进行基于结果的赌注。例如，预测比特币会下降一定的百分比，设定其他方可以参与的赌注。这些赌注在不受监管的市场中进行，因此存在重大风险。

### 5.3 抢先交易

与股票市场不同，区块链上的所有交易都是公开的，包括用户的钱包地址。这初看起来可能无害，然而它将大订单暴露在前置运行的风险之中。想象一个交易者持有 1 亿美金的比特币，并决定出售。为了这样做，交易者首先需要将大量比特币转移到一个交易所。此类交易将显示在区块链上，并且像 WhaleAlert.io 这样的监控网站可能会将此交易向全世界广播。如果交易者能够立即执行大订单，这可能不是一个问题。然而，由于加密货币的不信任性质，交易所通常会“锁定”存款 30-60 分钟，以保护自己免受双重支付攻击。这意味着敏锐的观察者，注意到大量比特币的流入，可能会推断出存款者打算出售。如果这次出售足够大以至于对价格产生重大影响，观察者可能会自己出售存入的资产，以便“前置运行”存款者，从大订单最终的定价影响中获利。这些分析使研究人员能够识别出美元泰达币与关联的 Bitfinex 交易所比特币价格的“泵送”之间可能存在联系（参见 Griffin and Shams，2018）。

### 5.4 抢先交易

股票市场的中央撮合引擎按照纯价格时间优先处理订单。这些引擎现在被校准以将订单分离到极其精细的时间测量 - 通常到皮秒（一万亿分之一秒）。然而，许多去中心化交易所（DEX）利用以太坊网络的“时钟时间”（14 秒），这可能会造成问题。

![](img/b_9783110660807-006_fig_008.jpg)

图 8 两个套利者之间的竞购战，试图向以太坊区块链提交市场订单（Daian et al.，2019）。

具体来说，想象一个用户在 DEX 上发布了一个定价错误的订单，从而产生了潜在的套利机会。为了利用这个机会，用户需要向 DEX 提交一个“市场”订单，耗尽有吸引力的流动性。问题是，这个订单将不会被确认，直到下一个以太坊区块被开采。由于矿工按费用优先处理交易，一个套利者可以提供高额费用，以利用有盈利的套利机会。Daian 等人 (2019) 识别出数千个这样的机会，并在其论文中记录了与矿工之间的“竞拍战”，以利用这些情况。

当一个用户在去中心化交易所（DEX）中看到套利机会时，他们会提交一个带有费用的市场订单——比如说 1 美元。这个订单只有在被矿工合并进一个交易时才会被执行。在市场订单被执行之前，第二个套利者也可能发现这个机会，并向矿工提供 2 美元的费用。当矿工最终解决加密难题时，他们会从两个用户那里收取费用，但只有费用最高的用户的订单会被执行。失败的出价者将支付费用，试图与已经耗尽流动性的智能合约交互。

这种行为被称为“Griefing”，Daian 等人 (2019) 在其论文中有记录。图 8 如下摘自他们的论文，展示了两个试图向以太坊区块链提交市场订单的套利者之间的“竞拍战”，他们出价愿意支付给矿工的费用以优先处理他们的订单。

## 参考文献

Aitken, M., H. Chen, 和 S. Foley (2017)。碎片化、交易所费用和流动性提供对市场质量的影响。《经验金融期刊》41，140-160。a, b

Anand, A., 和 K. Venkataraman (2016)。市场条件、脆弱性以及市场造市的经济学。《金融经济学家》121，327-349。a, b

Baur, D. G., K. Hong, 和 A. D. Lee (2018)。比特币：交易媒介还是投机资产？《国际金融市场、机构和货币杂志》54，177-189。a, b

Boehmer, E., G. Saar, 和 L. Yu (2005)。揭开面纱：对纽约证券交易所交易前透明度的分析。《金融杂志》60，783-815。a, b, c, d

Buti, S., B. Rindi, Y. Wen, 和 I. M. Werner (2019)。价格最小变动单位、交易策略和市场质量。可在以下网址找到：https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3330807。a, b

Corbet, S., B. Lucey, M. Peat, and S. Vigne (2018). 比特币期货 - 它们有什么用？*《经济学简报》172*，23–27。 a, b

Daian, P., S. Goldfeder, T. Kell, Y. Li, X. Zhao, I. Bentov, L. Breidenbach, and A. Juels (2019). 闪电男孩 2.0：去中心化交易所中的抢先交易、交易重新排序和共识不稳定性。可在：https://arxiv.org/pdf/1904.05234.pdf。 a, b, c, d, e, f

Dyhrberg, A., S. Foley, and J. Svec (2018). 比特币的可投资性如何？分析比特币市场的流动性和交易成本。*《经济学简报》17*，140–143。 a, b, c, d, e, f

Dyhrberg, A., S. Foley, and J. Svec (2019). 交易者行为对滴定规模的影响：来自加密货币交易所的证据。可在：https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3194932。 a, b, c, d, e, f, g, h

Foley, S., J. R. Karlsen, and T. J. Putniņš (2019). 性、毒品和比特币：多少非法活动是通过加密货币融资的？*《金融研究评论》32*，1798–1853。 a, b

Gajewski, J-F., and C. Gresse (2007). 集中式订单簿与混合式订单簿：NSC（欧洲泛欧交易所）和 SETS（伦敦证券交易所）交易成本的配对比较。*《银行与金融杂志》31*，2906–2924。 a, b

Griffin, J. M.，和 A. Shams (2018). 比特币真的是不受束缚的吗？ 可在 SSRN 找到：https://ssrn.com/abstract=3195066 或 http://dx.doi.org/10.2139/ssrn.3195066。 a, b

Makarov, I.，和 A. Schoar (2019). 加密货币市场的交易和套利。*金融经济学杂志 135*，293–319。 a, b

Yermack, D. (2015). 比特币、创新、金融工具和大数据。在*数字货币手册*中。 31–43。 a, b

## Notes