# 用链式甲骨文解锁合成衍生品

> 原文：<https://blog.chain.link/unlocking-synthetic-derivatives-with-chainlink-oracles/>

**我们与 Synthetix 一起开发了一种新的定价机制，为一种新的合成衍生产品提供动力，为用户提供石油的连锁风险敞口。这项创新是越来越多的例子之一，表明 Chainlink 如何通过提供能够访问高质量数据的安全[神谕](https://chain.link/education/blockchain-oracles)将传统市场的合成资产引入 DeFi。**

自直接易货时代以来，金融体系已经发生了巨大的变化。如今，从贷款和 401k 计划到保险和信用违约互换，存在一整套金融产品。现在唯一的限制是一个人自己的想象力，因为投资者可以以合适的价格获得几乎任何东西的金融敞口。

纵观历史，金融产品的创造大多局限于大型金融机构。这主要是因为提供奇异的金融产品所涉及的风险和资本以及围绕它的金融法规。

分散金融(DeFi) 可以说是有史以来第一次创建了一个新的无许可金融框架，允许世界上任何人建立标准和独特的金融产品，并提供给公众。现在，任何有互联网连接的人都可以在 Aave 上获得稳定利率的贷款，在 Synthetix 上获得长期黄金敞口，在 DODO 上用即时获得的 AMM 流动性交换资产，等等。

支持这种新金融基础设施的一个关键部分是访问[数据](https://blog.chain.link/understanding-how-data-and-apis-power-next-generation-economies/)。Chainlink 正在提供一个标准的开源框架，任何人都可以[构建任何价格的 oracle design](https://docs.chain.link/docs/request-and-receive-data) 或通过 [Chainlink 价格参考数据合同](https://feeds.chain.link/)访问现有的 oracle design。许多这些初始价格先知都专注于加密货币，因为这是大多数 DeFi 产品的核心。然而，Chainlink 的价格参考数据已经扩展到包括商品、外汇汇率和指数。这只是一切可能的开始。

## 使用 Synthetix 构建独特的石油/美元价格馈送

我们很高兴地宣布，我们与 Synthetix 一起为土壤提供了一种新的价格馈送，这是一种与永不过期的原油价格指数挂钩的合成数字资产。这是通过结合使用 [SIP-62](https://sips.synthetix.io/sips/sip-62) 期货参考定价算法和一个链式供电的[分散 oracle 网络](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)实现的。

为土壤创建参考价格馈送需要一种新颖的方法来创建典型设计模式之外的准确可靠的价格馈送。这种复杂性是由于石油等大宗商品通常只作为月度期货合约进行交易。这意味着同一资产可能有多个不同的价格点，因为有几个期货合同并行存在，到期日不同。

只利用最近期货合约的价格数据会带来很大的风险。最好的例子是最近的闪电崩盘，2020 年 5 月西德克萨斯中质油(WTI)原油期货合约在到期前一天下跌了 300%，最终以每桶负 37 美元的价格结算。尽管这种情况并不常见，但这种市场动态确实存在，需要加以缓解。

为了抵消这些价格异常，我们努力与 Synthetix 合作创建了一个石油/美元价格参考源，它采用了两个最接近到期的期货合约的动态加权方案。最近的合约最初权重最大，但随着到期日的临近，权重逐渐从最近的合约转移到下个月的期货合约。一旦前一个月完全到期，最近的两个有效合约成为第一个月和第二个月，动态加权过程重复进行。

这确保了期货合约到期前后的任何波动对由 Chainlink 价格馈送在链上生成和发布的最终参考价格点的影响最小。类似上述 WTI 石油闪电崩盘的事件对产生的参考价格点几乎没有影响。

## 开发定制金融产品的广阔市场

sOIL 是一个很好的案例研究，它展示了 DeFi 开发者即将超越加密货币价格馈送，开始创建金融产品，提供对食品、能源、稀土金属、现实世界资产、股票、 [NFTs](https://chain.link/education/nfts) 、加权资产篮子等的投资。

虽然 DeFi 最近经历了爆炸性的增长，实现了超过[130 亿美元的总价值锁定](http://defipulse.com/)，但仅全球原油市场就超过 1.7 万亿美元，衍生品市场的名义价值估计在[500 万亿美元到 1.2 万亿美元之间](https://www.investopedia.com/ask/answers/052715/how-big-derivatives-market.asp)。传统金融市场比加密货币市场大几个数量级；DeFi 才刚刚开始涉足 it 领域。

![A diagram showing how DeFi has room to grow into a trillion dollar market. ](img/db3da4352277db111fe83b93cb35bde2.png)

<figcaption>DeFi is still a very small fraction of the value of traditional markets, opening up massive opportunities for smart contract developers.</figcaption>



Chainlink 是提供传统资产或全新金融产品链上风险的基础设施。在土壤整合之前，Chainlink 已经在以太坊主网上提供黄金、外汇汇率、汽车、以太坊快速燃气等的实时价格。现在，有了这个新的价格 oracle 模型，我们可以轻松地应用于许多其他行业，在这些行业中，价格发现主要发生在月度期货合约中，如玉米、咖啡、糖、小麦和铂等。

创建基于期货市场的价格馈送为传统数据提供商开辟了新的利润丰厚的收入来源，这些数据提供商可能已经有几十年跟踪现实世界资产市场的经验。高质量数据提供商利用 [Chainlink 网络](https://blog.chain.link/what-is-a-chainlink-node-operator/)向 Synthetix 等应用程序出售期货石油数据就是一个例子。

通过实现对任何可以想象的真实资产的链上暴露，用例呈指数级增长。只要有互联网连接，苏丹的农民就可以对冲棉花价格下跌的风险。在注意到对自然资源的需求增加后，东南亚的一名工厂工人可以增加她对铜的接触。委内瑞拉的一个家庭可以通过投资贵金属来对抗恶性通货膨胀。

重要的是，这些用例都不要求参与者等待当地政府或银行提供对这些产品的访问。DeFi 的无许可基础设施可供世界任何地方的开发人员构建可定制的应用程序和价格源，服务于全球和本地市场。

也不限于猜测；合成资产可以用作贷款的抵押品，代表对意外事件的保险，或作为道投资策略的一部分。事实上,[智能合同](https://chain.link/education/smart-contracts)足够灵活，整个村庄的农民可以集中资金，集体保护他们的作物免受雨季的影响。

传统金融市场的连锁风险将变得越来越容易获得，而无需离开你的数字钱包。此外，新的金融产品也将出现，以前从来没有可能创造。我们并不完全知道未来将带领我们走向何方，但我们知道这里的潜力是无限的。

## 今天就开始用 Chainlink 建造吧

通过访问[开发者文档](https://docs.chain.link/)并加入 [Discord](https://discordapp.com/invite/aSK4zew) 的技术讨论，立即开始使用 Chainlink 价格参考数据。如果您想安排一次电话会议来更深入地讨论整合事宜，请点击此处的。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/)|[GitHub](https://github.com/smartcontractkit/chainlink)|[DeFi](https://defi.chain.link/)