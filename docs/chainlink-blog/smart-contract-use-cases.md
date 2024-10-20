# Chainlink 支持 77 个以上智能合同使用案例

> 原文：<https://blog.chain.link/smart-contract-use-cases/>

*这篇文章是“使用 Chainlink 增强智能合同的 44 种方法”的更新，最初发表于 2019 年 5 月 17 日。*

*   [分权财政](#decentralized-finance)
*   [对外支付](#external-payments)
*   [NFTs、游戏和随机性](#gaming-and-randomness)
*   [保险](#insurance)
*   [企业系统](#enterprise-systems)
*   [供应链](#supply-chain)
*   [实用程序](#utilities)
*   [授权和身份](#authorization-and-identity)
*   [政府](#government)
*   [可持续性](#sustainability)
*   [链外计算](#other)

从根本上说，合同定义了两个或多个独立方之间价值交换的条款和义务。历史上，通常需要一个集中仲裁器来验证这些条款和条件是否得到满足。然而，由于[区块链技术](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/)和[智能合同应用](https://chain.link/education/smart-contracts)的出现，我们现在可以用分散的基础设施取代集中的仲裁员，降低交易对手风险，提高运营效率。

然而，由于区块链的共识机制，智能合约没有与外部资源(如[数据提供商和 API 服务](https://blog.chain.link/understanding-how-data-and-apis-power-next-generation-economies/))进行交互的内置功能，无法验证区块链之外发生的真实事件的结果。这就产生了所谓的[区块链甲骨文问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)，并且代表了在区块链上表示日常合约的最大限制之一。

为了克服这种连通性的缺乏， [混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/) 使用 oracles 作为中间件来检索外部数据输入，将数据输出推送到外部系统，并执行可扩展的链外计算。oracles 不仅充当智能合约和外部世界之间的双向桥梁，而且还提供了一个安全框架来防止任何单点故障，如数据操作和停机。



![The Chainlink Network connects smart contracts to off-chain data and events](img/9b26e20d587b285f86e1127844d58293.png)

<figcaption id="caption-attachment-717" class="wp-caption-text">chain link 网络将智能合约连接到链外数据和事件</figcaption>





[Chainlink](https://chain.link) 是使用最广泛的分布式 oracle 网络，目前为众多区块链和用例中的实时应用提供了数百亿美元的价值。Chainlink 不是一个单一的 oracle 网络，而是一个由众多并行运行的分散式 oracle 网络组成的生态系统。每个 [oracle](https://chain.link/education/blockchain-oracles) 网络都可以提供大量的 oracle 服务，而无需交叉依赖其他 oracle 网络，其中包括:

*   [**分散式价格馈送**](https://data.chain.link/) 可以集成到任何 [DeFi](https://chain.link/education/defi) 应用程序中，以获得高质量、防篡改、全新的金融市场数据源，涵盖广泛的资产和完整的市场。
*   [**一个可验证的随机函数**](https://blog.chain.link/chainlink-vrf-on-chain-verifiable-randomness/)**【VRF】**为 NFTs 和链上游戏应用程序提供一个可证明公平安全的随机数生成器(RNG)专门为智能合约应用程序构建。
*   [**准备金证明**](https://blog.chain.link/chainlink-proof-of-reserve-bringing-transparency-to-defi-collateral/)**【PoR】**启用智能合约来审核由链外准备金支持的任何链上资产的真实抵押，如菲亚特支持的 stablecoins、跨链代币、代币化资产等。
*   [**自动化**](https://blog.chain.link/chainlink-automation-is-now-live-on-mainnet/) 为 dApp 开发者提供可靠的、去中心化的、具有成本效益的事务执行服务，用于触发智能合约功能，并通过利用链外计算来执行合约维护。
*   [**跨链互操作协议**](https://blog.chain.link/introducing-the-cross-chain-interoperability-protocol-ccip/)**【CCIP】**是针对多链生态系统的开源标准，使跨链应用能够跨多个区块链发送消息和传输令牌。
*   [**模块化外部适配器**](https://blog.chain.link/build-and-use-external-adapters/) 用于连接任何链外资源，包括高级数据提供商、经过认证的 web APIs、物联网传感器、银行支付、企业后端、其他区块链网络等。
*   [](https://blog.chain.link/how-chainlink-supports-any-off-chain-data-resource-and-computation/)**如 [公平排序服务](https://blog.chain.link/chainlink-fair-sequencing-services-enabling-a-provably-fair-defi-ecosystem/) 用于事务排序，[DECO](https://www.forbes.com/sites/benjessel/2020/08/29/chainlinks-new-acquisition-from-cornell-university-could-transform-blockchain-for-good/#6f58570c162b)用于 TLS web 会话数据的隐私保护证明，[Arbitrum roll up](https://medium.com/offchainlabs/scalable-low-cost-computation-of-ethereum-smart-contracts-using-arbitrum-on-the-chainlink-8985c6542d4e)用于可扩展的链外可靠性计算，等等。**

 **

![Chainlink's heterogeneous network model](img/6b2b7b96a3e4d7680a84461aec3d17e1.png)

<figcaption id="caption-attachment-2096" class="wp-caption-text">Chainlink 是由多个 oracle 网络模型组成的异构 oracle 网络</figcaption>



<figcaption></figcaption>



最终，Chainlink 提供了构建任何类型的 oracle 网络所需的必要的[开发人员工具](https://docs.chain.link/)，例如使用多个数据源、多个 oracle 节点、各种聚合方法、支付惩罚、信誉服务和可视化工具。这允许广泛的用例被开发、测试，并推向生产。

对外部数据的访问为智能合同开启了全新的功能浪潮。为了激发您对普遍连接的智能合约的无限潜力，我们列出了 77 种以上使用 Chainlink 网络的方式。如果你对这些想法有任何共鸣，或者如果你想了解更多，请在 [Discord](https://discord.gg/eJXg88) 或[Github](https://github.com/smartcontractkit/chainlink)上找到我们，并查看我们的 [文档](https://docs.chain.link/) ，立即开始构建普遍连接的智能合约。

## 分散金融

货币是今天用来估价和交换资产的普通媒介。金融产品提供了不同的工具，在这些工具中，人们可以通过不同的策略，如对冲、投机、赚取利息、抵押贷款等，最大限度地提高他们的货币价值。然而，传统金融往往是封闭的，资本充足的实体对货币发行和金融产品的创造/提供和结算拥有不成比例的控制权。结果是缺乏对某些金融产品的普遍可获得性，并引入了交易对手风险，其中较大的实体对金融产品是否根据预先商定的条款公平兑现具有更大的影响。

区块链和智能合约为金融产品带来了确定性的执行，消除了围绕金融产品创造的护城河，并为链上资产提供了防篡改的货币政策。Chainlink oracles 在创建代表金融产品和货币工具的高级智能合约方面发挥着至关重要的作用，特别是那些基于外汇利率、利率、资产价格、指数等市场数据执行的合约。

### 货币市场

基于区块链的[货币市场](https://blog.chain.link/decentralized-money-markets/)是至关重要的金融基础设施，它使用智能合约将希望从其资产中获得收益的贷款人与希望获得营运资本的借款人联系起来。它们允许用户增加他们的密码资产的效用，并参与供应方和需求方。然而，为了确保平台的偿付能力，需要价格反馈来跟踪平台上使用的资产的估值，以此确保贷款以公平的市场价格发放，并且对抵押不足的贷款自动进行清算。

[Aave](https://medium.com/aave/the-aave-oracle-network-powered-by-chainlink-is-now-live-45bb8a5a8c4e) ，[Compound](https://compound.finance/governance/proposals/47)和[Liquity](https://chain.link/case-studies/liquity)是链上货币市场协议的示例，该协议使用 Chainlink 价格馈送来获取数十种不同链上加密货币的市场数据。有了这些实时定价数据，这些借出/借入协议可以计算每个用户的抵押品和债务的估价，以便确定何时应该启动清算。这确保了货币市场协议总是有足够的担保，保护了用户存款中数百亿美元的价值。

![Aave Money Markets](img/e550c83a7ae4005f4582af3eb3ecbe99.png)

<figcaption id="caption-attachment-2366" class="wp-caption-text">Aave uses Chainlink Price Feeds to ensure proper collateralization</figcaption>



### 分散的稳定细胞

[稳定币](https://blog.chain.link/what-are-stablecoins/)是与法定货币(通常是美元)1:1 挂钩的链上代币。它们为用户提供了持有非易失性加密货币的能力。虽然集中式 stablecoins 由非连锁银行账户中的 fiat 支持，但分散式 stablecoins 通常被连锁加密货币过度抵押，并需要价格数据来维持完全抵押(例如，用户的抵押品价值超过其贷款价值的 150%)。

[DeFiDollar](https://medium.com/defidollar/defidollar-using-chainlink-price-oracles-live-on-mainnet-3cdc6c3047af) 是分散化元稳定币(由多个稳定币支持的稳定币)的一个例子，它使用[链式价格馈送](https://feeds.chain.link/)来跟踪基础资产的价格，包括 sUSD、、戴和。如果一个或多个此类货币偏离其 1:1 美元的挂钩汇率，从而导致 DUSD 也失去其挂钩汇率，则在四个储备货币之间启动再平衡，以保持 DUSD 的美元平价。



![DeFiDollar uses Chainlink Price Feeds for valuation data on the stablecoins backing DUSD](img/01b252b7d7b3dfe2cf9a0c85653f25bf.png)

<figcaption id="caption-attachment-719" class="wp-caption-text">DeFiDollar 在支持 DUSD</figcaption>



的 stablecoins 上使用 Chainlink 价格馈送作为估价数据

### 算法稳定积分

与银行账户中以美元为抵押的集中式稳定货币或链上加密货币超额抵押的分散式稳定货币类似，算法稳定货币旨在保持与另一种货币(如美元)的挂钩。然而，与其他实施方式不同，算法稳定币使用自动奖励和惩罚来维持其盯住汇率，以将价格推向盯住汇率，通常是在低于盯住汇率(通缩)时烧掉稳定币，在高于盯住汇率(通胀)时铸造更多稳定币。

[Fei 协议](https://medium.com/@bpmontgomery28/fei-protocol-upgrades-its-oracle-mechanism-to-chainlink-price-feeds-4368760b4991) 是一个算法稳定币的示例，它使用 Chainlink 价格馈送作为参考，为 Uniswap 上的 FEI/ETH 流动性池设置协议控制的价值绑定曲线，以稳定 Fei 令牌的挂钩。通过由 ETH/USD 价格馈送提供的市场范围的定价，Fei 协议可以确保由结合曲线提供适当的汇率。

![Fei Chainlink Integration](img/38379ebe439e9956c5c3cab8081fa78f.png)

<figcaption id="caption-attachment-2097" class="wp-caption-text">How the Fei Protocol uses Chainlink Price Feeds to stabilize the peg of its algorithmic stablecoin FEI</figcaption>



### 期货

期货是金融工具，它“责成”交易者在未来特定时间以预定价格购买或出售资产。通常用于对冲和杠杆风险的期货智能合同要求用户抵押他们的多头或空头头寸。价格反馈用于确定是否应该进行清算，以确保每份合同在任何时候都有充分的抵押。

[莱拉](https://blog.lyra.finance/lyra-integrates-chainlink-price-feeds/) 和 [MCDEX](https://mcdex.medium.com/mcdexs-perpetual-contracts-to-leverage-chainlink-oracles-for-index-prices-7af84eb319d9) 是链上金融应用的例子，其利用链价格馈送以便为永久合同提供动力，永久合同是没有到期的期货合同。通过使用 Chainlink oracles，这些协议能够通过访问实时价格数据来确保其平台的偿付能力，以确定何时应该进行清算，并动态设置融资利率以保持净中性风险。



![Diagram showing how Lyra uses Chainlink Price Feeds](img/d203387c406f3b6e21420b3d0b848565.png)

<figcaption id="caption-attachment-4970" class="wp-caption-text">Lyra 使用 LINK/USD 价格馈送为链上 LINK-USD 永久合约提供动力</figcaption>





### 选择

与期货合约类似，期权是一种金融衍生品，它赋予交易者在未来某个日期购买或出售一定数量特定资产的“期权”,如果他们愿意的话。在链外世界，中央集权的实体最经常签署合同，但是在区块链，分散的点对点的选择是可能的。

[Opyn](https://medium.com/opyn/opyn-v2-gamma-protocol-launches-using-chainlink-oracles-to-settle-options-95c110ceb766) 和 [Thales](https://thalesmarket.medium.com/thales-will-integrate-chainlink-price-feeds-to-secure-binary-options-outcomes-d7137f3199e1) 是期权协议的例子，它们使用 Chainlink 价格馈送来计算加密资产的估价，使用户能够铸造、交易和结算期权合同。此外，像[dx feed](https://www.dxfeed.com/dxfeed-will-make-btc-and-eth-implied-volatility-data-available-on-chain-through-chainlink/)这样的 Chainlink oracle 节点提供各种加密资产的隐含波动率(IV)数据，使合约创建者能够以可靠和防篡改的方式计算期权的合约溢价。

![Smart Contract Options](img/ab1b932d8745b052e56421798257cf6c.png)

<figcaption id="caption-attachment-2248" class="wp-caption-text">Opyn uses Chainlink Price Feeds to settle options contracts</figcaption>



### 合成资产

合成资产是一类金融工具，为交易者提供特定资产的价格风险，如指数或商品，而不需要拥有实物资产本身。[基于智能合约的合成资产](https://blog.chain.link/unlocking-synthetic-derivatives-with-chainlink-oracles/)允许交易员创建先进的非托管交易策略，并获得区块链上不存在的传统资产的敞口。

Synthetix 是一个协议的例子，该协议使用 Chainlink 价格馈送来实现各种“合成器”的铸造，使交易者能够获得加密货币、法定货币、商品、指数、股票等资产的链上敞口。通过点对点交易模式，用户可以使用 Chainlink 价格源在这些零滑动的合成代币之间进行互换，以获取基础资产的当前价值。



![Synthetix uses Chainlink Price Feeds as the target peg for numerous synthetic assets](img/b3e1fd7055e50d9953acf0defcff2d68.png)

<figcaption id="caption-attachment-721" class="wp-caption-text">Synthetix 使用 Chainlink 价格馈送作为众多合成资产的目标钉住值</figcaption>





### 信用违约互换

信用违约互换(CDS)是一种金融协议，允许贷款人对冲借款人违约(不付款)的可能性。如果借款人违约，发行和出售信用违约互换的一方将偿还贷款人借款人未支付的未偿资金。

[鸦片。Exchange](https://medium.com/opium-network/opium-exchange-is-live-consuming-chainlinks-price-reference-data-a83226b592cf) 是一个链上协议的例子，它使用 Chainlink 价格馈送来结算各种金融工具产品。其中一个产品包括在集中的 stablecoin USDT 系绳上的[信用违约互换](https://www.coindesk.com/credit-default-swaps-tether-opium)，允许交易者对冲系绳偏离和跌破 1 美元的情况。

### 结合

债券是一种金融协议，通过发行日后偿还的债务来筹集短期资本。通过使用 Chainlink oracles，可以将传统债券合同复制为自动化智能合同，该合同提供了结算所需的数据，如利率、债务评分、法定付款等。

Chainlink 已经通过 SWIFT 的 [POC 展示了这种能力，oracles 用于汇总五大银行的利率，从 S & P 获取债务评分数据，并以 ISO20022 SWIFT 支付报文的形式生成利息支付。作为一个价值数万亿美元的行业，将债券引入区块链可以大大降低交易对手风险和整体运营成本。](https://create.smartcontract.com/sibos17)



![A smart contract bond using Chainlink oracles and SWIFT’s ISO20022 standard](img/ca4d3ec35ca04774760db0581f1e1007.png)

<figcaption id="caption-attachment-722" class="wp-caption-text">采用 Chainlink oracles 和 SWIFT 的 ISO20022 标准的智能合约债券</figcaption>





### 令牌化的投资组合管理

智能合约的一个独特用例是非托管的“智能投资组合”，它通过根据预设条件代表用户执行交易来自动重新平衡用户投资组合。这为用户提供了先进的金融产品，这些产品基于特定资产和代币的当前市场价格以编程方式管理投资。这些交易策略可以进行令牌化，允许用户在其他智能合约应用程序中转移和使用这些令牌。

[Tokensets](https://medium.com/set-protocol/introducing-the-link-rsi-set-on-tokensets-fe3b4fcacf94) 就是这样一个协议的例子，它使用 Chainlink 价格馈送来生成各种“集合”，即代表用户执行交易的标记化头寸。这些集合基于技术分析(TA)指标，如 RSI 或移动平均线，旨在捕捉关键的价格走势。此外，用户可以在其他协议中使用他们的 Set 令牌作为抵押品，如 Aave 货币市场，以获得额外的资本效率。

### 链上储备证明

包装的跨链资产——一个区块链本地的加密货币/代币被锁定在一个合同中，然后在另一个区块链上“解锁”——正变得越来越受欢迎，因为它们能够增加 DeFi 生态系统中可用的抵押品类型。但是，为了确保支持打包资产存款的 DeFi 应用程序的完整性，准备金证明参考合同可用于提供有关这些链上资产的真实抵押的数据。

使用 Chainlink 为储备证明参考源供电的两个协议包括 [BitGo 的 WBTC](https://blog.bitgo.com/chainlink-brings-onchain-proof-of-reserve-to-wbtc-fcda00f2815c) 和 [Ren Protocol 的 renBTC](https://medium.com/renproject/chainlink-brings-onchain-proof-of-reserve-to-renvm-d5e66839850a) ，代表以太坊上包装的比特币的大部分，代表数十亿美元的价值。这些储备证明参考源为 DeFi 协议提供了他们需要的数据，以自动验证抵押品储备，并在抵押不足事件期间迅速保护用户资金。储备证明参考源还可用于跟踪跨链代币之外的资产抵押，包括稳定的货币和真实世界的商品，进一步增加 DeFi 中可用的抵押品。



![Chainlink Proof of Reserve provides smart contracts proof of the Bitcoin collateral backing BitGo’s Wrapped BTC (WBTC)](img/b15ac7125a6c7763f345827e2bc989cd.png)

<figcaption id="caption-attachment-724" class="wp-caption-text">chain link Proof of Reserve 提供智能合约证明的比特币抵押品 backing BitGo 的裹 BTC (WBTC)</figcaption>





### 外链储备证明

将真实世界的资产引入区块链为扩大 DeFi 的经济活动提供了巨大的潜力，正如菲亚特支持的 stablecoins 的采用所表明的那样。然而，这要求基础担保品由中央托管人持有，将链上令牌化表示与实际的链外资产本身断开。通过 Chainlink Proof of Reserve，智能联系人能够自主审计真实世界资产支持令牌的抵押，在黑天鹅事件期间保护用户。

这方面的例子有用于 PAX 和 PAXG 的 [Paxos 储备证明](https://www.paxos.com/paxos-adopts-chainlink-oracles-to-further-adoption-of-pax-and-paxg-in-defi/) 以及用于 TUSD 的 [TrustToken 储备证明](https://blog.trusttoken.com/trusttoken-introduces-proof-of-reserve-for-tusd-stablecoin-in-collaboration-with-chainlink-and-584b3674b89f) 。后者向 DeFi 应用程序提供有关支持 TrustToken 的非链托管银行账户持有的稳定 TUSD 币的真实美元金额的数据，这些数据由美国排名前 25 位的独立审计公司 Armanino 审查。可以根据补充的 TUSD 供应凭证所报告的各种区块链上流通的 TUSD 代币总量来检查该抵押数据，以确定 TrustToken 的代币美元的抵押。



![TrustToken uses Chainlink Proof of Reserve to provide smart contracts proof of the off-chain fiat reserves backing the TUSD stablecoin](img/3ca96e3159ecd887fb5af30b4358f637.png)

<figcaption id="caption-attachment-725" class="wp-caption-text">TrustToken 使用储备链证明来提供支持 TUSD 稳定币</figcaption>



的非链菲亚特储备的智能合约证明

### 自动化资产管理

智能合约可用于在预定的时间间隔自动执行交易策略。然而，一系列变量会影响这些策略的盈利能力，特别是网络天然气成本。因此，使用自动化系统的交易者需要来自先知的可靠数据，以确保他们的交易持续盈利。

[Pickle Finance](https://picklefinance.medium.com/pickle-finance-univ3-jars-powered-by-chainlink-keepers-8ce1756a2497)在其 Pickle Jars 产品中使用 Chainlink Automation 来帮助自动管理 Uniswap v3 中的资本高效型 lp 头寸。通过自动重新平衡用户的 LP 头寸，Chainlink Automation 有助于确保头寸保持在范围内，并收取最高的 LP 费用，从而帮助用户获得最大回报。

### 分享收入

随着越来越多的 DeFi 产品采用 DAO(分散自治组织)治理，开发者和社区成员越来越需要以分散和实时的方式分配 DeFi 协议产生的收入。通过使用 Chainlink oracles，DAOs 可以根据各种指标按比例分配加密收入，如赌注、治理参与、开发人员活动或任何定制的需求集。

Synthetix 是 DeFi 协议的一个例子，它将使用 Chainlink Automation 来触发每周向用户分配交换费和赌注奖励。Chainlink Automation 将监控智能合约的离线状态，并在费用周期结束后自动调用协议的 feePools 智能合约中的费用分配功能。

![Synthetix Chainlink Keepers](img/2e2461f9b04cee0f0ae0c7a645827e91.png)

<figcaption id="caption-attachment-2275" class="wp-caption-text">Synthetix will use Chainlink Automation to trigger the distribution of exchange fees and staking rewards to users</figcaption>



### 高产农业

[收益农业](https://chain.link/education/defi/yield-farming) 是 DeFi 生态系统中一种新的金融原语，用于引导流动性和促进协议治理令牌的公平分配。在大多数 yield farming 应用程序中，为协议提供流动性的用户会以其本机治理令牌的形式获得奖励，作为增长补贴。

在它们的产量耕作机制中使用链式预言的两个协议是 [血浆](https://medium.com/stake-technologies/plasm-integrates-chainlink-price-feeds-live-on-mainnet-to-provide-asset-valuations-to-its-lockdrop-25d17f52ca42) 和[strong block](https://medium.com/@strongblockio/strongblock-integrates-chainlink-oracles-live-on-mainnet-to-help-power-its-defi-mining-rewards-93bf8f1b76ae)。Plasm 使用 Chainlink price oracles 来帮助确定用户锁定到协议中的价值金额，然后相应地分配奖励，而 StrongBlock 每 24 小时计算一次锁定在社区池中的美元价值。



![StrongBlock uses Chainlink oracles to calculate staking rewards based on miner reliability](img/fad2e15c4ea1b7bea4263b2173f34f5a.png)

<figcaption id="caption-attachment-728" class="wp-caption-text">StrongBlock uses Chainlink oracles to calculate staking rewards based on miner reliability</figcaption>



产量优化协议可为用户自动收割和复利。用户将代币存入金库，金库会在临界点自动收获收益，以实现复利回报最大化。然而，由于智能合约无法执行自己的功能，因此收益率优化器需要一个外部实体来触发链上交易。许多收益率优化器使用信任最小化解决方案，而不是依赖不可靠的公共奖金或具有单点故障的集中式机器人来自动化交易。

[chain link Automation](https://chain.link/automation)使开发人员能够以高度可靠、经济高效和分散的方式触发智能合同，并且已经为 Web3 上成千上万的自动化交易提供了动力。开发人员可以将它们设置为定期自动复利，或者建立高级优化策略，只在有利可图时才执行。

例如，yield optimizer[Pickle Finance](https://picklefinance.medium.com/pickle-finance-integrates-chainlink-keepers-to-automate-new-uniswap-v3-jars-92473db14f2a)正在使用 Chainlink Automation 来帮助 yield aggregators 构建更高级的全自动保险库策略。通过 Chainlink Automation，Pickle Finance 能够增加对储户的回报，而无需依赖人工干预或引入单点故障，单点故障会使其平台容易受到操纵和技术故障的影响。查看如何使用 chain link Automation或 [浏览文档](https://docs.chain.link/docs/chainlink-automation/introduction/) 。



### 杠杆产量农业

用户可以通过使用杠杆化收益耕作协议来提高他们的收益和资本效率，杠杆化收益耕作协议通过协议控制的低抵押贷款向储户提供资本。有了这些头寸，借款人可以通过各种产量农业策略最大化其资产价值，而贷款人则从希望扩大其农业头寸的借款人那里获得被动收入。这就产生了一个专门针对具体应用的货币市场，专门关注农业生产活动。

[羊驼金融](https://medium.com/alpaca-finance/alpaca-finance-integrates-chainlink-price-feeds-to-maximize-security-of-leveraged-yield-farming-on-8f60f7589fa0) 是一个协议的例子，该协议使用 Chainlink 价格馈送使用户能够通过借贷资本来增加他们在 PancakeSwap 和 WaultSwap 上的头寸。来自价格馈送的金融市场数据用于在贷款发放和清算头寸期间计算适当的抵押比率，以确保协议的长期偿付能力，即使在借款人存放的抵押品估值的市场波动期间也是如此。

![Leveraged Yield Farming](img/bb844853cc36a790a1440a842cf90c79.png)

<figcaption id="caption-attachment-2249" class="wp-caption-text">Alpaca Finance uses Chainlink Price Feeds during the loan issuance and liquidation processes</figcaption>



### 跨链产量农业

随着 DeFi 生态系统继续在多个区块链网络中扩展，从 Aave 等现有协议中产生收益的机会将在断开的环境中细分。为了克服这个问题，需要一个跨链令牌桥来促进用户资金跨网络转移。然而，现有的跨链解决方案很容易被利用，已经有数亿美元被从这些协议中抽走。[跨链互操作性协议](https://blog.chain.link/introducing-the-cross-chain-interoperability-protocol-ccip/) (CCIP)，一种用于跨区块链网络传输消息和令牌的安全开源标准，克服了这些问题，并将为开发人员提供创建多链收益平台所需的防篡改基础设施。

### 自付贷款

作为一种新的支持 DeFi 的金融原语，自付贷款协议使用户能够将资产作为抵押品进行存款，并借入/铸造合成资产以提供营运资金。存入的抵押品被发送到一个产生收益的协议，该协议中的收益被用来随着时间的推移自动偿还债务，从而创建一个资本效率很高的借款头寸。

这种新金融原语的一种实现是 [Alchemix](https://alchemixfi.medium.com/advancing-alchemix-with-chainlink-277b48e27ec8) ，这是一种自付贷款协议，它使用 Chainlink 自动化为用户提供 DAI 和 ETH 存款的未来收益率。自动化用于触发每天的保险库获取和保险库刷新，自动偿还债务，并将新存款重新分配到渴望金融以产生收益。

### 断路器

在某些异常高波动性的情况下，加密货币交易所的资产价格可能不再反映更广泛市场上的价格。这可能会导致套利者的资金损失，或者导致用户因其持有的杠杆头寸而被错误平仓。这种情况会降低用户对交易的信任。交易所可以从使用断路器中受益，如果出现某些偏差，断路器就会跳闸。

Digitex 是传统交易所的一个例子，它通过监控用户的内部价格馈送和 Chainlink 价格馈送之间的偏差来保护用户免受市场操纵，作为用户在平台上交易的附加安全层。如果交易所的价格偏离 Chainlink oracles 报告的更广泛的市场价格超过一定的百分比，就会触发“熔断机制”，暂时停止交易和清算。

### 分散交换

[分散交易所(dex)](https://blog.chain.link/dex-decentralized-exchange/)是链上交易场所，允许用户交易加密货币，而无需保管这些资产或向中央机构提供个人信息。随着 dex 越来越受欢迎，对传统的交易策略和目前在传统的集中交易中可用的高级功能的需求变得越来越重要。

0x Relayer [Bamboo Relay](https://medium.com/bamboo-relay/bamboo-relay-integrates-chainlink-oracles-for-stop-loss-order-functionalities-32a5fd35a037) 是一个分散式交易所的例子，它使用 Chainlink 价格馈送来支持止损订单功能——基于资产价格行为的条件交易功能。通过 Chainlink 的汇总市场数据，每个交易者的止损单将仅在资产的市场价格超过某个预定义的阈值时执行，从而防止市场操纵攻击错误地执行交易。



![Bamboo Relay uses Chainlink Price Feeds to power stop-loss orders on top of the 0x protocol](img/089daab7d0eabec13e1037306f9a5fca.png)

<figcaption id="caption-attachment-726" class="wp-caption-text">竹中继使用 Chainlink 价馈给电力止损单在 0x 协议之上</figcaption>





### 自动做市商

自动做市商是一种越来越受欢迎的分散交易类别。与传统的订单簿不同，资产管理工具是链上的流动性池，便于根据预先确定的价格公式进行资产互换。通过汇集资本，流动性提供者能够获得被动收益，交易者获得按需流动性。

DODO 是 AMM 协议的一个例子，该协议使用 Chainlink 价格反馈为一种新的 AMM 设计提供动力，这种设计被称为主动做市商。多多的 PMM 模仿人类的做市行为，在 Chainlink 报告的市场价格附近聚集更多的资本，以促进更高效、更频繁的交易。

### 红星

许多协议依赖于某种形式的赌注——将加密货币抵押品锁定到智能合同中——以保护其加密经济网络。赌注抵押品可能有助于表明奖励应该按比例分配，或者可以“削减”——在特定条件下有计划地采取，作为抑制恶意行为的一种手段。

例如， [AdEx](https://www.adex.network/blog/adex-integrates-chainlink-oracles/) 要求它的验证器节点使用抵押品并保持高可用性。AdEx 使用 Chainlink oracles 监控节点的正常运行时间，并在任何节点低于正常运行时间要求时触发抵押品削减。这就保证了只有优质的节点运营商参与网络，进而增强了整个平台的安全性。

### 重置基础

重定基准是 DeFi 中的一种新的金融工具，涉及调整代币的供应量，以维持其与特定参考资产(如美元)的挂钩。如果在换基期间代币的价格高于其挂钩，则铸造更多代币并按比例给予所有代币持有者，目的是降低每个代币的价格。相反，如果代币的价格低于挂钩，那么每个持有者的一定百分比的代币被烧掉，以提高每个代币的价格。

Ampleforth 是一个协议的例子，它使用 Chainlink 价格馈送来支持其本地的重新基础功能。AMPL 的总供应量每天进行重新调整，以跟踪当前的消费者价格指数(CPI)率，CPI 是经济分析局(Bureau of Economic Analysis)关于经通胀调整的 2019 年美元现值的指数。AMPL 的数量加权平均价格和 CPI 指数都由 Chainlink oracles 提供给 Ampleforth 协议。



![Ampleforth Chainlink](img/d2695efdae92ca7046517e24a0c9c534.png)

<figcaption id="caption-attachment-2277" class="wp-caption-text">Ampleforth 使用 Chainlink oracles 每 24 小时重置一次 AMPL 令牌供应</figcaption>





### 真实世界的资产

正如我们在最近的教育文章中所讨论的，[标记化的真实世界资产](https://blog.chain.link/asset-tokenization-bringing-real-world-value-to-the-blockchain/)是区块链和智能合约技术最有前途的用例之一。他们将现实世界的资产作为一种象征，在区块链上展示出来。与传统资产相比，令牌化资产受益于全球可访问性、无许可流动性、链上透明性和减少的交易摩擦。

### 清算

区块链货币市场通常被过度抵押，以确保当抵押品价值下降和/或债务价值上升时，用户贷款可以被适当清算，从而确保用户资金在市场上的安全。然而，由于智能合约在默认情况下处于“休眠”状态，因此清算需要由外部方执行，以通过偿还债务来“唤醒”合约以结清头寸。该流程需要高度可靠，以确保没有已创建和未结的有毒贷款头寸。

Aave 是拥有数百亿美元用户存款的货币市场协议的一个例子，它将使用 Chainlink 自动化来帮助触发用户头寸的清算。Chainlink Automation 将监控用户头寸的抵押比率，如果任何头寸低于抵押品的预定义阈值(例如 150%)，分散式 Chainlink Automation 网络将调用清算功能并平仓，即使在市场剧烈波动和区块链网络拥塞期间也是如此。

![Aave Chainlink Keepers Liquidation](img/9aa426c43e21082bf9cb80ad20fb81ed.png)

<figcaption id="caption-attachment-2276" class="wp-caption-text">Aave will use Chainlink Automation to help trigger the liquidation of undercollateralized loans.</figcaption>



## 对外支付

智能合约很容易以其本地区块链的加密货币发行支付，例如以太坊智能合约以 ETH 发行支付。然而，许多企业无法承担在其资产负债表上持有不稳定的加密货币资产的风险。他们也不希望在用加密货币兑换他们喜欢的法定货币时产生额外的摩擦。鉴于世界各地的支付偏好多种多样，智能合同需要访问多种类型的支付选项，以充分满足全球需求。由于 Chainlink 能够将智能合约的输出推送到外部 API，因此它可以促进各种各样的支付服务。

![Chainlink Payments](img/306a3162e3ff647f0c4fc9e5f88d9446.png)

<figcaption id="caption-attachment-2385" class="wp-caption-text">Chainlink connects blockchains to external payment solutions</figcaption>



### 银行付款

Chainlink 使智能合约能够连接到现有的银行系统，允许智能合约开发商无缝集成信息和服务，如消费者银行账户、直接存款和来自领先全球银行的其他流程。

### 零售支付

许多消费者应用程序，如优步和 AirBnB，向用户提供流行的零售支付。Chainlink 可以为智能合约带来同样的易用性，让它们能够访问领先的信用卡提供商和成熟的支付网络，如 PayPal 和 Stripe。开发人员可以开始构建应用程序，利用零售经济中日常使用的国内和国际最受欢迎的支付产品。Chainlink 已经为流行的零售支付轨道，如 [PayPal](https://github.com/smartcontractkit/paypal-adapter) 和 [Mistertango](https://github.com/smartcontractkit/mistertango-adapter) 预建了模块化外部适配器。

### 加密货币支付

加密货币越来越受欢迎，但一些受欢迎的选择往往与领先的智能合约平台脱节。Chainlink 弥合了这一差距，它允许任何智能合约平台在任何其他分布式账本上进行支付，如以太坊区块链触发的比特币支付。此外，Chainlink 价格馈送可用于提供转让时或销售点的汇率，确保用户以防篡改的方式获得公平的市场汇率。

[Alchemy](https://medium.com/@alchemyGPS/alchemy-pay-to-integrate-chainlink-price-feeds-to-power-defi-products-and-fair-crypto-payments-c5282135a77a) 和 [Paycoin](https://medium.com/payprotocol/paycoin-to-integrate-chainlink-price-feeds-into-its-global-retail-payments-solution-9506d2c5e95) 是混合加密/法定支付平台的例子，它们将使用 Chainlink 价格馈送来确定汇率，允许用户使用各种加密货币支付，同时商家仍然收到他们喜欢的支付形式。

### 员工工资

在传统世界中，几乎所有行业效率低下的一个重要原因是延迟向员工和承包商支付服务费用。Chainlink 支持的智能合同可用于以编程方式实时向工人发放款项，这将减少雇主的会计管理费用，并为工人提供更直接的工资获取途径。

fiat on/off-ramp aggregator[Transak](https://medium.com/@transak/transak-integrates-with-chainlink-to-connect-smart-contracts-with-fiat-crypto-payment-gateways-4cd7c54ab3c4)展示了如何通过使用 WakaTime 这样的工作跟踪 API 来定期触发对开发人员的支付。此外，Chainlink 价格馈送可用于计算要分配的加密收入的确切金额，从而保持每次支付的特定美元值。

### 汇款

在一个日益全球化的世界里，汇款非常普遍。然而，尽管技术进步，这是一个缓慢而昂贵的行业。许多 DLT 项目旨在扰乱汇款行业，Chainlink oracles 可以向智能合约提供可靠的外汇汇率数据，并在转账时实现直接存款。

## NFTs、游戏和随机性

虽然 DeFi 是目前最大的智能合约市场，但开发人员正在越来越多地构建防欺诈、加密经济激励的游戏应用程序。区块链游戏的一个独一无二的特点是他们能够产生稀有的游戏内物品(大多数是 NFT)，因为区块链提供了物品稀有性的明确证据。以一种外部实体或游戏开发者可以操纵的方式铸造这些稀有物品对确保它们的价值至关重要，这就是为什么 Chainlink 开发了一个[可验证的随机性函数(VRF)](https://chain.link/solutions/chainlink-vrf) 。VRF 链是一个安全的和可证明公平的随机数生成源(RNG)，它生成链上加密证明，向用户证明随机性没有被篡改。

他们被证明是公平的随机性形式为物品的稀有性带来了可靠性，开辟了像虚拟[元对](https://blog.chain.link/the-economic-impact-of-random-rewards-in-blockchain-video-games/)这样的东西，其中标记化的物品可以在不同的游戏中可靠地使用。可验证的随机性对于创建监管赌博应用程序的无可置疑的公平性也是至关重要的，消除了信任赌场对他们的赔率说真话的需要。此外，VRF 链家可以订购按需赠品和活动的参与者，或者以公正的方式公平选择低需求活动的参与者，如陪审团职责。除了随机性，游戏还可以受益于众多数据集，如增加游戏内功能/评级的真实世界事件数据、促进 NFT 市场的汇率、连接物理世界的物联网数据等等。

### 随机奖励和 NFT

游戏中的物品是大多数游戏的重要组成部分，因为它们为用户提供了特殊的力量或独特的属性。很多游戏内物品都是作为 [不可互换代币](https://chain.link/education/nfts) (NFTs)发放的，代币是唯一的，不可互换的。Chainlink VRF 已经在生成可证明的随机 NFT 和创建 NFT 属性作为对不同预定义的游戏内成就的奖励方面发挥了重要作用，例如获得前 10 名的稀有皮肤。

[Aavegotchi](https://aavegotchi.medium.com/chainlink-vrf-launches-on-polygon-enabling-provably-rare-aavegotchis-d03e36698795) 是一个在多边形 sidechain 上的链上游戏项目的例子，当玩家打开门户时，该项目使用 Chainlink VRF 快速有效地制造出具有随机选择属性的可证明罕见的 Aavegotchi NFTs。另一个例子是 [以太传奇](https://medium.com/ether-legends/ether-legends-launching-randomized-end-of-season-nft-rewards-powered-by-chainlink-vrf-7346450a8c12) ，这是一种数字收藏交易卡游戏，它使用 Chainlink VRF 在一个赛季结束时向顶级玩家随机分发罕见的加密支持的 NFT 奖。热门游戏 dApp Axie Infinity 也于 [最近宣布](https://blog.chain.link/what-is-play-to-earn/) 它正在使用 Chainlink VRF 在游戏的数字宠物世界中为起源轴生成可证明的随机特征。



![Ether Legends uses Chainlink VRF to mint and randomly distribute rare crypto-backed NFTs](img/bb9df998595abccf89ba5a4c14a05fa4.png)

<figcaption id="caption-attachment-730" class="wp-caption-text">以太传奇使用 Chainlink VRF 铸造并随机分发稀有的加密支持的 NFTs</figcaption>





### 动态 NFTs

[动态 NFTs](https://blog.chain.link/create-dynamic-nfts-using-chainlink-oracles/) 扩展了 NFTs 的概念，使这种令牌能够随着时间的推移而发展和变化，这是由现实世界的事件或链状神谕所传递的可验证的随机性所确定的。与铸造后不会改变的静态 NFT 相比，动态 NFT 的稀有性和实用性会随着时间的推移而改变，这为收集 NFT 提供了一种游戏化的体验。

MLB 球星 [特雷·曼奇尼](https://medium.com/ureeqa-inc/mlbs-trey-mancini-using-ureeqa-and-chainlink-to-launch-nfts-for-cancer-research-6450d2d0e5c4) 和 NBA 年度最佳新秀 [【拉梅洛·鲍尔】](https://blog.ether.cards/lamelo-ball-nft/) 就是在区块链以太坊上用链状神谕创造动态 NFT 的两个例子。对于前者，NFT 被表示为限量版的数字棒球卡，使用 Chainlink VRF 以可验证的公平和公正的方式为 NFT 分配特殊效用，所有 NFT 销售收入都将用于癌症研究。对于后者，NFTs 随着时间的推移根据球员在现实世界中的表现进行升级，在现实世界中，当拉梅洛·鲍尔被选为 NBA 年度最佳新秀时，EVOLVE 令牌被激活。

![Trey Mancini NFT](img/debd2769d97b2810692fe24e82b94d7d.png)

<figcaption id="caption-attachment-2252" class="wp-caption-text">Trey Mancini’s NFTs use Chainlink VRF to randomly assign additional utility.</figcaption>



### 随机游戏

不可预测性是有趣游戏的特征之一。不知道下一个阶段或即将发生什么的兴奋感创造了悬念、阴谋和挑战。开发者可以利用 Chainlink VRF 来确保不可预测事件的完整性。其中一些游戏场景可能包括地图生成、关键命中(战斗游戏)、配对(多人游戏)、抽牌顺序和随机遭遇/事件。



![Chainlink VRF enables smart contracts to use randomness for both inputs and outputs](img/88bf8c6c13da9ca9024f6debe3a0afeb.png)

<figcaption id="caption-attachment-729" class="wp-caption-text">Chainlink VRF 使智能合约能够对输入和输出都使用随机性</figcaption>





### 预测市场

区块链预测市场使个人能够对特定现实世界事件的结果下注。由于其本质，总部位于区块链的预测市场依赖外部数据来确定结果。 [Chainlink 数据馈送](https://chain.link/solutions/defi) 提供一个分散的、防篡改的外部数据源，可用于触发预测市场的结算以及对赢家的支付。预测市场已经围绕体育赛事结果、政治选举结果以及加密货币路线图完成和价格预测而创建，但最终预测市场可以包含任何类型的赌注，只要另一方有接受者。

随着 Chainlink 数据馈送， [Chainlink 自动化](https://chain.link/automation) 在增强预测市场的安全性和分散性方面日益发挥关键作用。[chain link Automation](https://automation.chain.link/)通过以高度可靠、经济高效和分散的方式触发智能合同，可以自动化智能合同功能，而不是依赖 DevOps 团队、cron jobs 等集中式自动化机器人或激励奖金来启动和停止每一轮预测并选择获胜者。在 chain link Automation[开发者文档](https://docs.chain.link/docs/chainlink-automation/introduction/) 中了解更多信息。

Chainlink Automation 不仅为开发人员节省了数百个小时，还显著增强了预测市场的安全性。通过将 Chainlink 自动化集成到他们的预测游戏中，以帮助开始和停止预测回合并向获胜者分发奖励，[Entropyfi](https://medium.com/entropyfi/entropyfi-saves-engineering-hours-with-chainlink-keepers-6ec172a76249)消除了单点故障，并能够每周节省 20 个工程小时。

总部位于区块链的百科全书[](https://chainlinkecosystem.com/ecosystem/everipedia/)Everipedia 最近使用 Chainlink 在线传递选举结果，以帮助稳定预测市场。Everipedia 运营一个 Chainlink oracle 节点，并将美联社关于 2020 年美国总统选举结果的加密签名数据传送到以太坊区块链，然后 Chainlink 数据馈送被链上预测市场使用，如[yield wars](https://yieldwars.com/)。



![Everipedia’s Chainlink node recently delivered the results of the 2020 US Presidential Election on-chain using data cryptographically signed by The Associated Press](img/ad70345cdf404d9cb0e0f6ff53e6f244.png)

<figcaption id="caption-attachment-731" class="wp-caption-text">Everipedia 的 Chainlink node 最近使用美联社</figcaption>



加密签名的数据在网上发布了 2020 年美国总统大选的结果

### 游戏化

GameFi 是区块链博彩公司的一个分支。GameFi 游戏使玩家能够获得游戏内奖励。顾名思义，GameFi 位于区块链游戏和分散金融的交汇处。通过提供经济激励，开发者可以创造一种吸引人的游戏体验，鼓励玩家参与到游戏生态系统中来。

在 GameFi 平台上，玩家可以通过在游戏中前进、与其他玩家战斗以及完成特殊任务来获得奖励。奖励包括代表武器、皮肤、头像和虚拟土地的游戏内代币和 NFT，然后可以在二级市场上交易或出售，如分散交易所或 NFT 市场。非托管所有权使玩家能够完全控制他们的游戏内资产，潜在地使用户能够在未来将他们的 NFTs 带到其他游戏和 metaverses。

自动化对于开发高级 GameFi 体验至关重要。开发人员需要自动化智能合约功能，以按时开始和结束游戏回合，根据特定的游戏结果向玩家分配奖励，等等。虽然开发人员可以使用集中服务器上的脚本来自动化这些过程，但这将消耗宝贵的时间，并产生可能导致漏洞和可靠性问题的单点故障。相比之下，通过使用chain link Automation，开发人员可以以一种高度可靠、经济高效且分散的方式触发智能合约功能。

例如，游戏化的 NFT 平台[Nifty Royale](https://niftyroyale.medium.com/nifty-royale-will-integrate-chainlink-keepers-to-automate-nft-based-battle-royale-games-d3c73c43525d)正在使用 Chainlink Automation 来帮助触发其位于 NFT 的皇家之战游戏。具体来说，Nifty Royale 正在使用自动化来触发智能合同功能，以开始和结束其每一轮皇家之战。通过使用自动化，Nifty Royale 正在增加其游戏的安全性和可靠性保证，这一点尤其重要，因为玩家可以赢得具有现实世界价值的游戏内资产。如果你想在你自己的 GameFi 项目中利用 Chainlink Automation，现在 [浏览文档](https://docs.chain.link/docs/chainlink-automation/introduction/) 。

### 无损失储蓄游戏

DeFi 可组合性的进步导致了一些创新应用，如无损失储蓄游戏——dapp，它汇集用户存款，并在分散的货币市场上贷出，以产生利息。在一个特定的时间框架后，一个赢家被选中，从资金池中赚取所有累积的利息。获胜者被选中后，所有用户都可以提取他们的原始存款，而不会有任何损失。

这方面的一个例子是 [PoolTogether](https://medium.com/pooltogether/improving-pooltogether-with-chainlink-vrf-dcf1a3d6ea) ，这是一种在线无损失储蓄游戏，它使用 Chainlink VRF 来选择每个奖项的获胜者。通过利用链上随机性的透明且可验证的来源，向用户提供了对无损失奖金池平台的整体可靠性和公平性的更高程度的信任。



![PoolTogether uses Chainlink VRF to randomly choose winners in their no-loss savings game](img/7b6911152dfa254642e6801d29f62860.png)

<figcaption id="caption-attachment-732" class="wp-caption-text">PoolTogether 使用 Chainlink VRF 在他们的无损失储蓄游戏</figcaption>



中随机选择赢家

### 体育和电子竞技

智能合约为在线体育博彩的执行提供了完整性，而 Chainlink 分散式 oracle networks 可以通过从可靠的 web APIs 聚合数据来验证体育比赛结果。这些智能合约(通常以预测市场的形式)可以基于一场比赛的结果、个人表现，甚至是一些看似无关紧要的事情，比如一场游戏的开场掷硬币。最重要的是，电子竞技预测市场有可能检索游戏数据，并在链上传播，以确定赢家。

以区块链为基地的体育博彩市场的一个例子是 [占卜](https://augur.net/blog/launching-augur-turbo-chainlink-polygon/) ，它使用高吞吐量多边形侧链上的 Chainlink oracles 来为其 Turbo 预测市场提供动力。用户可以推测各种主题的结果，包括 NBA、MLB、MMA 和奥运会的不同体育赛事，这些赛事在市场关闭后使用提供优质真实世界数据的分散式 oracle 网络快速解决。

![Augur Chainlink Diagram](img/be25634e16ddc07b3469412fa710ffb5.png)

<figcaption id="caption-attachment-2253" class="wp-caption-text">Augur uses Chainlink Data Feeds to power their Turbo prediction markets.</figcaption>



# **保险**

如今，保险业在低信任度的商业环境中运营。投保人有动机在保险申请中虚假报告积极的指标，以减少他们的每月免赔额，而保险公司有动机延迟付款并提高费率，以说明错误的风险状况。由于保险公司负责处理索赔，并且比保单持有人更有资本，因此在理赔时间和方式方面，它们拥有更大的权力。由 Chainlink 驱动的智能合同将保险合同转变为更加客观、平等的模式，在这种模式下，数据直接决定结果，执行是确定的，任何一方都不会篡改。

### 参数保险

传统保险公司可以通过创建基于智能合同的高级 [参数保险协议](https://blog.chain.link/parametric-insurance-smart-contract/) 来利用区块链技术的优势，这些协议可以根据分散式 oracle networks 提供的真实数据自动触发赔付。通过减少对人工仲裁的依赖并因此减少延迟付款，保险范围可以扩大到更广泛的企业，以对冲现实世界中存在的各种风险。

### 作物保险

农作物保险长期以来一直被认为是智能合同的一个特别有前途的用例，因为它为发展中国家的农民提供了保险，否则他们将无法获得或不信任这些保险，因为当地保险市场不发达。通过为任何人提供互联网连接，使他们能够抵御不可预见的天气条件，全世界的农民都能够维持生计，而不必担心一个恶劣的天气季节可能导致经济崩溃。

这方面的一个例子是 [Arbol](https://www.arbolmarket.com/businesses-and-farmers-can-now-hedge-weather-risk-through-the-arbol-platform-and-chainlink-data/) ，这是一个智能的基于合同的天气覆盖解决方案，它使用 Chainlink oracles 从国家海洋和大气管理局(NOAA)获取降雨数据集。该数据用于结算参数作物保险合同，该合同根据该地区的降雨量提供保险范围。



![Arbol uses Chainlink oracles to fetch weather data used to execute parametric crop insurance contracts](img/4dbba9488b240a9dcaf75a2e45219d22.png)

<figcaption id="caption-attachment-734" class="wp-caption-text">Arbol 使用 Chainlink oracles 获取用于执行参数作物保险合同的天气数据</figcaption>





### 飞行保险

智能合同保险最早进入生产的形式之一是飞行保险。由于天气和维护等一系列不可控制的变量，航班经常延误，给商务旅客带来不便。航班保险单允许旅行者减少这些机会成本，因为他们在航班延误时支付赔偿。

一个例子是 [Etherisc](https://blog.etherisc.com/etherisc-to-leverage-chainlink-oracles-for-decentralized-flight-insurance-product-9559b64d79c7?gi=c7260a60fbc1) ，这是一个分散的保险协议，它利用 Chainlink oracles 来检索航班数据，以确认它是否被延误。通过消除对争议期的需求，被保险人可以保证，如果他们的航班延误，他们将立即收到付款，并且保险公司能够通过消除人工索赔处理来降低成本。

### 汽车保险

现代车辆配备了广泛的内部传感器、互联网连接，甚至本地 API。chain Link 2020 年虚拟黑客马拉松的获胜者 [Link My Ride](https://blog.chain.link/create-tesla-smart-contract-rental/) 利用了其中的一些数据点，允许智能合同指定租赁期，为租赁者解锁车门，记录租赁时间，计算行驶里程，确定剩余电池电量，并自动支付租金。这些功能结合在一起，使用定制的[外部适配器](https://market.link/adapters/1c70368e-c2df-4e05-adde-27b257092cbe)为特斯拉汽车创建了一个复杂的租车合同。随着基于车辆的 API 变得越来越复杂，新的保险形式将变得可用，包括基于车辆中大量碰撞传感器触发的参数汽车保险，或基于每年行驶里程等指标的保险折扣。

### 家庭保险

日益增长的“智能家居”现象导致传感器和先进的安全系统自动通知房主和紧急服务机构不寻常的事件。这些传感器可以通过 Chainlink oracles 连接到智能合同，以创建新的参数化家庭保险产品。对于度假屋和其他全年不使用的住宅来说，保险产品特别有用，可以通过连线来检测破裂的管道、故障的太阳能电池板，甚至是家庭入侵，作为一种更直接的保护公司的游戏中的皮肤报警系统的手段。

### 人寿保险

拥有可靠数据的智能合同是降低成本、减少纠纷、加快解决时间的理想选择。许多 web APIs 和外部数据库拥有足够的数据来确定死亡是否发生以及何时发生，例如死亡证明、讣告、火化记录和警方报告。Chainlink 可以使用这些数据自主支付款项，并在人寿保险单上列出的几方之间分配资产，从而消除不必要的管理费用，加快对投保人的支付。

### 健康保险

由于生物技术和物联网可穿戴设备(如智能手表)的无数进步，保险公司可以创建智能合同，根据患者的健康数据提供健康保险折扣或触发处罚。有用的数据点可以包括行进的距离(锻炼)、体重、心率，以及未来可能提供的更先进的生物识别技术。Chainlink oracles 还可以发现可以触发强制咨询的数据异常，以便保持有利的政策利率。

ETHDenver 2019 黑客马拉松参赛作品 Gran Fondo 使用 Chainlink oracles 将物联网可穿戴设备上的 GPS 时间戳数据带到链上，以创建在 ETH 中支付的链上体育比赛。同样的精确数据也可以用于创建健康保险合同，根据 Chainlink 连接的物联网可穿戴设备记录的特定时间范围内的身体活动量来确定保险费率。

### 海上保险

与气候相关的不确定性正在导致越来越不可预测的航道条件，如低水位或高水位。由于主要海运航道的临时关闭，这可能导致数亿美元的损失。智能合约可以使用 Chainlink oracles 连接到一系列现实世界的传感器，为各种保护范围签发参数保险，如运输过程中冷冻货物的解冻，运输船只的损坏，或由于不可预见的天气条件导致的延迟运输。

这方面的一个例子是[一个黑客马拉松项目](https://devpost.com/software/parametric-water-level-insurance),目的是在气候变化导致主要航线关闭的情况下为货运公司提供保险。连接到水位传感器的链节神谕，在水位下降或上升到当前水平以上导致水道关闭时触发保险赔付。

### 再保险

由于承保大量保单的风险，潜在企业家很难进入保险业。在灾难性事件中，保险公司可能无法承担所有责任，导致违约。因此，许多公司“再保险”他们承保的投资组合——在他们不能覆盖所有索赔的情况下卸载一部分风险。

一个可能的解决方案是将再保险政策标记为智能合同。这将允许个人投资者通过购买保单的一部分来支持保单。在这个过程中，可以使用 Chainlink oracles 来命名保险单的当前价值，将保险支付路由到令牌持有者，并自动触发保险支付。

## 企业系统

由于减少了交易对手风险、中介费用和外部纠纷，智能合同为企业在多方业务流程中削减成本和提高效率提供了充足的机会。但是，为了利用智能合同，企业需要围绕隐私、可伸缩性和连接性进行额外的考虑，以满足某些业务和法律要求。Chainlink 为企业提供了一个向区块链环境销售其数据和 API 服务的网关，并满足某些技术要求，如私有数据的链上访问、契约逻辑的链外计算、交易的链上隐私等等。

### 区块链抽象层

就像互联网作为连接计算机的单一网关一样，Chainlink 为 [企业](https://chain.link/solutions/enterprise) 提供单一中间件，用于将它们的 API 连接到每个区块链环境。Chainlink 是区块链不可知的，可以集成到任何当前和未来的区块链上，许多领先的连锁店已经支持 Chainlink，如以太坊、波尔卡多特、雪崩、币安智能链、Polygon、乐观、Arbitrum 等。通过让 Chainlink 跨所有主要连锁店运营，企业可以将它作为一个“区块链抽象层”,用于让其现有系统跨任何/所有连锁店高效地“支持区块链”。

这将集成工作减少到最低限度，因此企业不必重建现有的基础设施，而是可以专注于其核心的区块链战略。通过消除企业选择哪种区块链最有可能成为行业标准的负担，供应商锁定得到了限制。此外，Chainlink 节点提供了一些关键优势，如安全的私钥管理、安全的链外计算、信任最小化的硬件、权限控制等等。

![Chainlink Enterprise Diagram](img/29f1d53e6ee93c36aeea2b134888283f.png)

<figcaption id="caption-attachment-3191" class="wp-caption-text">Enterprises can use Chainlink oracles as a blockchain abstraction layer to connect their backend systems to smart contracts across any DLT networks</figcaption>





### 数据和 API 的货币化

Chainlink 内置的灵活性确保了它与现有的遗留数据和 API 基础设施完全兼容。因此，[数据提供商](https://blog.chain.link/easily-sell-your-apis-and-data-to-any-blockchain-via-chainlink/)也可以使用 Chainlink 的区块链抽象层向任何区块链上的智能合约出售他们的数据。有两种方法可以做到这一点:向 Chainlink 网络出售数据，或者由运行自己的 Chainlink oracle 节点的数据提供商直接向区块链出售数据。

通过向 Chainlink 网络出售数据，数据提供商不需要改变他们当前的商业模式，这意味着后端修改是不必要的，他们可以接受法定货币支付。或者，看到智能合约经济价值的数据提供商可以运行一个 Chainlink 节点，直接向智能合约提供签名数据(使用数字签名)，从而获得更多收入，并建立作为可靠数据提供商的声誉。



![Data providers can sell their data to the Chainlink Network using their existing API interfaces without modifications and/or can operate a Chainlink node to provide smart contracts with origin-signed data](img/c9e8f668eeeb3e48616385f7ba6310e3.png)

<figcaption id="caption-attachment-737" class="wp-caption-text">数据提供商可以使用其现有的 API 接口将其数据出售给 Chainlink 网络，无需修改和/或可以操作 Chainlink 节点以提供带有原始签名数据的智能合同</figcaption>





### 节点即服务(NaaS)

运行 Chainlink 节点使数据提供商能够开始向智能合同应用程序销售他们的 API 连接。为了简化启动 Chainlink oracle 节点的体验，基础设施提供商可以提供节点即服务(NaaS)解决方案，以便快速启动新的 Chainlink 节点，并以向后兼容的方式将数据提供商的现有 API 连接到区块链网络。

Amazon Web Services (AWS)是领先的云提供商的一个例子，它与 Chainlink Labs 合作推出了 AWS Chainlink Quickstart，这是一个一键式工作流，数据提供商和 DevOps 团队可以轻松地在 AWS 云上推出 Chainlink oracle 节点，并通过多个区块链网络向智能合约销售真实数据。面向未来的框架使数据提供商能够在 AWS 上无缝地推出 Chainlink 节点，允许他们对数据进行加密签名，并将其广播到区块链，在那里可以出售给智能合约应用程序。

![AWS Chainlink Quickstart](img/49d8bb76004e7c8937bc4943529db958.png)

<figcaption id="caption-attachment-2836" class="wp-caption-text">The AWS Chainlink Quickstart gives data providers a single gateway to all blockchains</figcaption>



### 混合云/区块链应用

随着智能合同的发展，对更高级的分散式应用程序的需求越来越大，这些应用程序需要昂贵或复杂的计算，而这些计算在链上是不可行的。一种解决方案是使用 oracles 来证明在更可扩展的云计算环境中处理的离线计算。利用 Chainlink 的双向通信能力，可以创建 [混合云/区块链应用](https://cloud.google.com/blog/products/data-analytics/building-hybrid-blockchain-cloud-applications-with-ethereum-and-google-cloud) 以离线方式发送计算指令和/或数据进行处理，并将结果桥接回链上以供智能合同使用。

一个例子是 Google Cloud 上的 NOAA 天气预报，Google Cloud 使用 Chainlink oracles 将它带到了区块链以太网上。通过这种集成，智能合同可以访问高质量的天气数据(温度、降水、冰雹等)，为 Arbol 提供的参数作物保险协议提供动力。

![Google Cloud Chainlink Diagram](img/fa12a3cbc2f60f1a823aab9f6634a46d.png)

<figcaption id="caption-attachment-2255" class="wp-caption-text">NOAA weather data hosted on Google Cloud being brought on-chain using Chainlink oracles</figcaption>



### 隐私保护数据查询和凭证管理

对于许多企业和机构来说，数据隐私不是一个可有可无的奖励，而是一项严格的要求，是满足 GDPR 等法规要求的必要条件。Chainlink 正在通过最近收购 [DECO](https://arxiv.org/abs/1909.00938) 来开发应对这一挑战的尖端解决方案，DECO 是由康奈尔大学 Ari Juels 领导的团队创建的一项保护隐私的 oracle 技术。

DECO 允许通过 HTTPS/TLS 传输的所有数据(占世界数据的大部分)由 oracles 保密地证实，而不会泄露链上数据(它不会离开链外数据库)，也不会对托管链外数据的服务器进行任何修改。例如，Alice 能够使用 DECO 来证明她的银行帐户余额高于某个阈值，而不会向链上的 oracle 本身透露她的确切帐户余额或她的身份。这使得几乎所有的数据都可以在链上利用，同时仍然保留机密性和数据许可协议。



![Chainlink’s DECO uses zero knowledge proofs to enable the use of confidential data within smart contracts without revealing the data on-chain or to the oracles](img/7f387e301be68fb56d2b20b3df8de51d.png)

<figcaption id="caption-attachment-739" class="wp-caption-text">Chainlink 的 DECO 使用零知识证明来支持在智能合同中使用机密数据，而不会泄露链上数据或向 Oracle</figcaption>





### 链上交易隐私

除了数据输入的私密性，许多企业还希望契约逻辑和输出的私密性。Chainlink 开发了一种使用 oracles 的方法，通过一个名为 [Mixicles](https://blog.chain.link/breaking-down-mixicles-and-its-potential-to-unlock-enterprise-demand-for-defi-applications-on-public-blockchains/) 的解决方案为 DeFi 智能合同提供链上交易隐私。Mixicles 将链上数据输入和链上支付输出分开，使用 oracle 作为两个组件和交易混合器之间的桥梁。Chainlink oracles 不是在链上传递原始数据输入，而是发布一个只对契约参与者有意义的整数表示(例如，如下例所示的 1 或 2)。然后，mixer 可以接受该整数输入来执行对隐藏的一方的支付，但仍然为用户生成链上审计报告，作为满足监管要求的一种方式。Mixicles 协议能够实现多层隐私，例如隐藏合同条款、使用的数据源、合同中资金的真实价值以及谁收到了付款(根据与输入的相关性)。

![A diagram showing examples of binary options.](img/1c31730c6b665e85fb2491fe94a08626.png)

### 私有离链计算

Chainlink 实践了一种深度防御的安全方法，用户利用多层安全来获得各种保证。Chainlink 正在开发的另一个解决方案是 [Town Crier](https://blog.chain.link/town-crier-and-chainlink/) ，这是一个 oracle 协议，它使用可信执行环境(TEE)形式的附加硬件来实现私有、通用的链外计算。

Town Crier 使用基于 TEE 的 oracle(特别是英特尔 SGX)来支持 Chainlink oracle 节点在黑盒环境中对数据执行高级计算，在黑盒环境中，数据不会泄露，甚至不会泄露给节点运营商。Town Crier 提供了数据机密性和计算完整性，开辟了新的 oracle 用例，如处理用于加密货币支付的私钥或用于身份验证的用户登录凭据。



![Chainlink’s Town Crier uses Intel SGX to enable off-chain data confidentiality and computational integrity](img/da5534d36d9b1b921622e500e22b7cbb.png)

<figcaption id="caption-attachment-741" class="wp-caption-text">Chainlink 的 Town Crier 使用英特尔 SGX 实现链外数据的机密性和计算完整性</figcaption>





### 稠度计算

随着智能合约的采用不断加快，对实用的扩展解决方案的需求也在不断增加，这些解决方案可以提高吞吐量，降低分散应用的延迟，同时保持用户资金的基础层安全性。通常，这些第 2 层可伸缩性解决方案需要存在一个或多个链外验证器节点，这些节点负责批处理事务，并根据需要将简洁的响应传递到基础层链上。

Chainlink oracle 节点支持计算，可以作为第 2 层解决方案的验证器，例如 Offchain Labs 的[Arbitrum roll up](https://medium.com/offchainlabs/scalable-low-cost-computation-of-ethereum-smart-contracts-using-arbitrum-on-the-chainlink-8985c6542d4e)。链式链接节点可以执行可靠性函数的任意计算，生成欺诈证据，并在不做任何修改的情况下支持它们的服务。最终的结果是 oracles 不仅用于数据输入，还用于执行可伸缩的链外可靠性计算。



![Layer 2 Arbitrum Rollup chains can be operated and validated by Chainlink oracles, creating highly scalable smart contract applications secured by fraud proofs and cryptoeconomics.](img/13cb1b69bc718da012369e1401efb2ef.png)

<figcaption id="caption-attachment-742" class="wp-caption-text">第 2 层 Arbitrum Rollup 链可以通过 Chainlink oracles 进行操作和验证，从而创建高度可扩展的智能合同应用程序，这些应用程序受到欺诈证据和密码经济学的保护。</figcaption>





### 基础架构提供商 Oracle 节点

区块链需要一个基础设施提供者的分散网络，例如验证器、序列发生器、代码转换器和 oracles。电信公司或互联网服务提供商等传统基础设施提供商可以支持 Chainlink 网络，并通过直接运营 Chainlink oracle 节点获得额外收入。通过利用其现有的内部基础架构，此类提供商可以提供高度可靠的 oracle 服务，并从混合智能合同生态系统的增长中获利。

[T-Systems MMS](https://www.t-systems-mms.com/en/expertise/archive/smart-contracts-made-reliable-and-useful-with-the-real-world-data.html) 是德国电信(欧洲最大的电信提供商)的子公司，运营着一个 Chainlink oracle node，为众多领先的 DeFi 应用提供金融市场数据。随着对普遍连接智能合同的需求持续增长，收入机会可能会增加，导致更多基础设施提供商推出 Chainlink 节点。

> “通过运营 Chainlink 节点，T-Systems MMS 将为 Chainlink 网络用户和以太坊上的分散式应用(dApps)提供可靠的真实世界数据，进一步支持公共区块链作为分散式金融(DeFi)等众多用例基础的愿景。”–[T 系统彩信](https://www.t-systems-mms.com/en/expertise/archive/smart-contracts-made-reliable-and-useful-with-the-real-world-data.html)



![Deutsche Telekom subsidiary T-Systems MMS operates Chainlink oracle infrastructure and provides smart contracts with real-world data and events](img/47097268fa825b1f06563006165a1ff7.png)

<figcaption id="caption-attachment-2256" class="wp-caption-text">德国电信子公司 T-Systems MMS 运营 Chainlink oracle 基础设施，并为智能合同提供真实世界的数据和事件</figcaption>





### 通过发票提取加密货币支付

鉴于加密货币/代币的新颖性、波动性和监管不确定性，一些企业目前对个人持有和处理加密货币犹豫不决。由于大多数区块链基础设施需要加密货币来运行，企业的采用仍然有限，甚至完全被阻止。与其等待通常缓慢的法律系统来解决问题或让企业接受这个想法，Chainlink oracles 可以作为一个解决问题的方法，使用目前广泛使用的通用发票技术，允许他们向菲亚特的第三方服务提供商支付，然后在后台处理加密货币支付。

黑客马拉松项目 [LINK Gas Station](https://github.com/pappas999/Link-Gas-Station) 采用了[元交易](https://defirate.com/meta-transactions/)的概念——区块链交易费用被提取出来，由一个中继站支付——并将其应用于 Chainlink。它使用第三方中继来管理实用令牌 LINK 和 ETH 的所有权，这两者都是支付以太坊计算和获得 Chainlink oracle 数据服务所必需的。通过这样做，加密货币所有权的责任和复杂性从企业转移到了所选择的继电器上，导致企业可以简单地用菲亚特支付发票，并获得整个分散生态系统的访问权。重要的是，企业仍然完全控制签署交易所需的加密私钥。

### 基线协议的外部数据

Baseline Protocol 是一个使用以太坊 mainnet 作为通用参考框架来同步企业记录系统的框架。Baseline 使用零知识证明来确保不同的企业数据库与其交易对手保持一致(同一组记录),而不会泄露链上的任何机密数据。

Chainlink oracles 是确保基线事件使用相同外部数据输入的关键基础设施。例如，[动态采购订单](https://medium.com/baselineprotocol/how-the-baseline-protocol-integrates-chainlink-oracles-fc66be703c6e)可以利用 Chainlink oracles 来获取(来自多个来源的)关于运输货物温度的聚合天气数据。采购订单中每件商品的价格可以根据温度自动更新，例如香蕉可以根据天气情况动态定价。Chainlink 围绕外部数据输入创建一致性的能力在业务合作伙伴之间创建了一致性，减少了分歧和协调。



![Multi-party agreements using the Baseline Protocol can use Chainlink oracles to fetch redundantly validated real-world data and events](img/db687eb7c6b787569dbd54a7748dda35.png)

<figcaption id="caption-attachment-744" class="wp-caption-text">使用基线协议的多方协议可以使用 Chainlink oracles 获取冗余验证的真实世界数据和事件</figcaption>





### 引导传统系统安全性

如白皮书中的[所述，Chainlink 将使用服务级别协议(SLA)和堆栈为 oracle 服务创建额外的安全性和加密经济保证。SLA 存在于链上并由双方签署，它定义了 oracle 服务的条款以及根据 oracle 的表现发布的惩罚/奖励。SLA 的结果可以输入到信誉系统中，在那里未来的用户可以评估节点的可靠性。运行自己的 Chainlink 节点的企业可以使用 staking-backed SLA 来提升其数据和链外服务的可靠性和安全性，迫使他们因未能满足其声明的要求而面临真正的经济风险和声誉。这使得企业和数据提供商能够为智能合同等自动化流程提供确定性保证，而无需重建整个后端系统。](https://link.smartcontract.com/whitepaper)

## 供应链

供应链始于原材料的采购，止于将货物交付给最终客户。沿着这条路线有支付转移，所有权的变化，海关清关，监管监督，以及各方之间共享的文件。智能合约提供了一种自动化这些过程的方式，作为减少全球贸易中摩擦和对手风险的一种手段。Chainlink oracles 可以将供应链智能合约连接到 web APIs、云网络和各种现实世界的传感器，如 GPS、温度、速度、加速度、湿度、光度等。这些数据可以用来触发支付和各方之间的数据传输，而这种方式是供应链中任何一方都无法操纵的。这样一个框架为所有相关方生成了一个黄金的事实来源，而开销却少得多。

### RFID 跟踪

供应链越来越多地利用 RFID(射频识别)技术来跟踪商品。RFID 系统将库存物品与标签连接起来，这些标签可以通过无线电频率在远处被检测到。这允许简化和高效地跟踪商店商品、货运托盘和许多其他常见的库存方法。有了 Chainlink oracles，来自现实世界的 RFID 数据可以用来触发各种各样的链上合同，包括在仓库收到库存时启动付款，或延迟发货的自主保险赔付。

[开放图书馆项目](https://devpost.com/software/the-open-library-project)，一个在 [Chainlink 虚拟黑客马拉松 2020 期间创建的项目，](https://blog.chain.link/congratulations-to-the-winners-of-the-chainlink-virtual-hackathon-2020/)使用 Chainlink oracles 构建了一个 [RFID 区块链集成](https://blog.chain.link/rfid-blockchain-integration-with-chainlink-external-adapters/)，使用户能够检查进出的带有 RFID 标签的书籍，并在链上记录这一活动，创建了一个分散和无边界的图书租赁平台。

![Chainlink RFID Diagram](img/ef7a88ea2a5500fa701ae3b08f28c69b.png)

<figcaption id="caption-attachment-2257" class="wp-caption-text">RFID devices can be connected to smart contracts using Chainlink oracles.</figcaption>



### 物联网传感器

物联网传感器可用于确保运输中的产品在整个供应链旅程中得到妥善维护。例子包括在特定温度下保存食物和密封容器以防篡改。Chainlink 可用于创建 [【区块链】物联网集成](https://blog.chain.link/how-chainlink-enables-blockchain-iot-integrations/) ，通过 将物联网传感器连接到智能合同，智能合同根据物联网数据是否确认遵守了预定义采购订单中定义的质量控制标准来触发支出和发放罚款。

这方面的一个例子是 [PingNET](https://medium.com/@pingnet/ping-to-integrate-chainlink-oracles-to-provide-iot-data-to-smart-contracts-2fd9d5a1abe2) ，这是一个面向物联网设备的分散式传输网络，它使用 Chainlink 基于 PingNET 上支持物联网的托盘中的数据实现利益相关方之间的自动支付。PingNet 还旨在提供其他物联网事件数据，如湿度、海拔、紫外线指数、辐射等。

### 结关

当货物跨境运输到监管不同的国家时，通常需要接收国海关机构的许可，以防止非法或危险货物的运输。许多贸易融资合同需要访问这些数据，以实时确定货物的状态。随着智能合同开始将此类协议自动化，它们仍将需要有关清关的信息。Chainlink oracles 可以以保护隐私的方式直接提供这些数据，从而实现跨境贸易融资合同的端到端自动化。

### 提单、发票和保险单

国际贸易文书工作主要包括三个主要文件:提单，由承运人签发，用以确认收到待运货物；由卖方开具给买方的关于销售交易细节的发票；保险单——保险公司和投保人之间的合同，说明保险公司依法需要支付的索赔。这些文档中的每一个都可以受益于 oracles 可以使用 oracles 直接从数据生成提单，向支付发票提供外汇汇率，并向保险合同的连锁保单提供物联网质量控制数据以触发结算。

## 公用事业

水、能源和互联网等公用事业是现代社会的基础支柱。这些公用事业的有效运作和管理对社会和身体健康至关重要，但它们往往依赖于缺乏激励的商业动力和过时的基础设施。智能合同通过将公用事业基础设施推向更公平、自动化、实时的系统，利用去中心化的网络、数据和加密经济激励来实施这些条件，从而实现了公用事业基础设施的现代化。这确保了公用事业提供商达到更高的标准，并且用户能够更好地访问展示关键公用事业服务质量和状态的客观数据。

![Chainlink Utilities ](img/1ade988de12a9372015f7929c9ccaecc.png)

<figcaption id="caption-attachment-2396" class="wp-caption-text">Chainlink oracles can connect blockchain networks to utilities</figcaption>



### 互联网、电信和云托管

许多公用事业公司，如互联网、有线电视和云托管，都是根据既定的定价结构向客户收费的。但是，当他们的服务出现故障时，有时会因机会成本而造成巨大的财务损失(例如，由于云中断，交易所经历停机)，没有人对此负责。物联网传感器可以监控公共设施的正常运行时间，Chainlink 可以将它们的性能数据输入智能合同，以计算每月付款或根据停机时间发放补偿。

ETHNewYork 2019 黑客马拉松参赛作品 [Blocksolid](https://blog.chain.link/showcasing-the-winning-projects-from-the-ethnewyork-hackathon/) 探索了一个用例，其中非政府组织可以让互联网服务提供商(ISP)为发展中地区的错误互联网服务负责。他们通过跟踪互联网服务提供商(ISP)的正常运行时间，并使用 Chainlink oracles 在链上中继这些数据。如果检测到停机，保存捐赠资金的链上智能合同将被更新，以防止从 ISP 提款。

### 活力

能源供应商有责任确保世界上所有的基础设施都能获得推动全球经济发展所需的能源。为了提高能源交付的效率，可以使用 Chainlink oracles 将消耗率输入智能合同，以触发过度消耗罚款，征收二氧化碳税，并提供当前能源价格，以公平生成电费，并允许以不同货币支付。智能合约可以从智能电表中读取读数，将某人的产出货币化，跟踪消费，并促进两者之间的支付。

总部位于区块链的分布式能源交易市场 Dipole 计划使用 Chainlink 价格反馈来实现能源资产的在线交易和估值。然后，用户可以使用法定货币或加密货币购买能源，汇率由 Chainlink 供电的分散价格馈送决定。

### 水

虽然经常被认为是理所当然的，但确保您家中的水龙头能够为您提供水的基础设施受到了严格的质量控制和可靠性监控。物联网传感器可以监控地下水位，跟踪企业消耗，并识别公共机构的非法虹吸。Chainlink 可以将这些物联网数据输入智能合同，以便发出监管罚款，生成消费发票，触发自动支付，更新供应跟踪数据库，甚至触发对面临洪水风险的城市的紧急资助。

### 排放和废物管理

排放和废物处理行业可以通过支持物联网的智能合同进行变革，这些智能合同可以准确衡量产出和效率。通过 Chainlink oracles，这些数据可用于自动触发向适当的监管机构支付过度消费，将回收或废物转化为燃料技术中使用的垃圾货币化，或生成激励性支付结构，当某人消费较少或使用更多可生物降解的物品时，降低垃圾账单。

## 授权和身份

虽然支持智能合同的区块链网络本质上是假名的，但用户强烈要求能够证明他们的真实身份，以此作为确保抗 Sybil 和/或授予许可的手段。通过 Chainlink oracles，包含用户身份的传统数据基础设施(如政府数据库、社交媒体等。)[可以连接到智能合约应用程序](https://blog.chain.link/digital-identity-on-the-blockchain/)，或者通过将用户的身份绑定到他们的链上地址，或者证明链外服务器中的数据。这确保了机构能够保持完全的法规遵从性，并通过处理已知身份提供了额外的安全层。

### 电子签名

电子签名已经成为越来越流行的获取文档签名的方式。他们实现了签名流程的现代化，并帮助公司避免了获取手写签名的高昂开销。由于签名是授权合同最常见的方式，Chainlink oracles 有必要让智能合同访问像 DocuSign 这样的领先电子签名公司。

Chainlink 可以通过两种方式使电子签名行业受益:证明电子签名并在链上转发，或者为现有的电子签名解决方案提供外部数据访问，作为使其合同解决方案更加动态的一种手段。[FirmaChain](https://medium.com/firmachain/notice-firmachain-chainlink-integration-fcacdb2b145d)，一家总部位于区块链的数字签名和签约解决方案，正在使用 Chainlink oracles 允许其数字合同根据现实世界的数据和事件执行，就像在批准租车之前检查驾照的真实性一样。再比如[eth sign](https://medium.com/ethsign/ethsign-will-use-chainlink-keepers-and-oracles-to-power-new-smart-agreement-framework-1c864ed0c5d8)，这是一个自动化的合同结算框架，用户可以通过 Chainlink oracles 定义链外数据源以及各自的触发条件。

### 生物测定学

授权智能合同的另一种可验证方式是通过生物特征数据，如指纹或视网膜眼睛扫描。由于生物识别技术对特定的人来说是唯一可识别的，只要有可靠的数据库或来源可以相互参照，它们就可以成为验证某人身份的有效方法。Chainlink oracles 既可以将生物数据传递给智能合约，也可以将其连接到不同的链外数据库以验证真实性。

![Chainlink oracles can connect smart contracts to biometric data.](img/e14d2c344f5d4aaec2dba4b9bdfc4fa2.png)

<figcaption id="caption-attachment-2285" class="wp-caption-text">Chainlink oracles can connect smart contracts to biometric data.</figcaption>



### 资格证书

使用可信硬件和/或高级加密技术，Chainlink oracles 安全地处理外部系统和应用程序的私有帐户信息。这使得智能合约能够直接验证凭证，例如某人是否有适当的资金量或拥有特定的安全密钥。一旦 Chainlink oracles 在链上中继确认，智能合约就可以触发资金的执行和结算。在交换有价值的资产之前，将凭证带上链对于验证输入也是特别有效的。

### KYC/反洗钱

利用区块链和智能合约技术的机构通常需要额外的基础设施，以确保在了解客户(KYC)和反洗钱(AML)法律方面完全符合法规要求。这需要使用外部 oracle 来提供有关被转移资金的身份和完整历史的数据。

[Coinfirm](https://www.coinfirm.com/blog/coinfirm-chainlink-anti-money-laundering-blockchain/) 是一家区块链分析公司使用 Chainlink oracles 从其反洗钱(AML)解决方案中获取数据的一个例子。这为希望通过 oracle 网络的实时验证为任何链上应用程序添加合规性的用户提供了一个即插即用的解决方案。此外，[cipher trace](https://ciphertrace.com/ciphertrace-launches-defi-compli-a-compliance-oracle-solution-on-chainlink-to-enable-dexs-and-defi-protocols-to-abide-by-ofac-sanctions/)在 Chainlink 上推出了 [DeFi 合规 oracle 服务](https://market.link/data-providers/57a9cf23-fc11-45e7-ba5b-18975e4562cf/integrations?network=1) ，通过在链上提供源代码签名的合规数据，使 dex 和其他 DeFi 应用程序遵守外国资产控制办公室(OFAC)的制裁要求。

![CipherTrace launched a Chainlink oracle node to bring AML data on-chain.](img/b1c538428e1dbb51a27098c7b61b2d3d.png)

<figcaption id="caption-attachment-2258" class="wp-caption-text">CipherTrace launched a Chainlink oracle node to bring AML data on-chain.</figcaption>



### 社交媒体身份和域名

对于许多人来说，区块链仍然有一个陡峭的学习曲线，特别是在处理长的十六进制地址方面。为了改善用户体验，oracles 被用来帮助将十六进制地址转换成人类可读的名称，如“chad.crypto”。

一个例子是[unstopped Domains](https://hackernoon.com/making-crypto-payments-less-scary-pjv3z2f)，这是一个链上域名存储库，使用 Chainlink oracles 以可验证和透明的方式将用户的 Twitter 社交媒体帐户与他们的人类可读链上地址联系起来。这使得任何人都可以在向用户发送资金之前，验证一个[区块链域名](https://blog.chain.link/how-to-create-nft-domain-names/)与用户的社交媒体账户相关联。



![Unstoppable Domains uses Chainlink oracles to enable users to tie their off-chain Twitter identity to their on-chain Ethereum domain name](img/3fc8ab4f290ea923397d4c7a4e002502.png)

<figcaption id="caption-attachment-745" class="wp-caption-text">unstopped Domains 使用 Chainlink oracles 使用户能够将他们的离线 Twitter 身份与他们的在线以太坊域名</figcaption>





### 智能合同审计结果

为了确保智能合约应用程序的完整性和正常运行，开发人员可能希望在向其发送资金之前验证协议是否经过了一次或多次安全审核。使用 oracle，用户可以直接在链上获得对审计结果的按需验证，从而在某些交易(如高价值交易)之前，或者在充当其他用户资金的可信托管人时，打开自动检查等使用案例。

网络安全公司 [Hacken](https://hackenclub.medium.com/hacken-integrates-chainlink-to-bring-its-security-audit-data-on-chain-for-defi-b175bfa8df8b) 将使用 Chainlink oracles 将他们的安全数据带上链，这些数据涉及智能合同审计、集中交易所的渗透测试、漏洞奖金等。然后，智能合约可以利用这些数据来防止与危险的和/或未经审核的智能合约进行交互。



![Hacken uses Chainlink oracles to bring security audit reports on-chain to be used by smart contract applications](img/5ce7ce1833dd3155169380f1726d8c60.png)

<figcaption id="caption-attachment-746" class="wp-caption-text">Hacken 使用 Chainlink oracles 提供安全审计报告，供智能合同应用程序使用</figcaption>





### 账户安全

双因素身份验证(2FA)是用户可以用来保护其在线帐户的另一种方法，除了用户名和密码之外，还需要一层额外的验证。这种安全性的提高防止了对机密信息的未经授权的访问，并且防止了在没有多重验证的情况下转移资金。通过 Chainlink oracles，智能合约能够增强 2FA 功能，直接保护用户的加密货币资产。

[Digital Bridge](https://digitalbridge-io.medium.com/digital-bridge-using-chainlink-to-launch-a-2fa-oracle-for-smart-contracts-abf06ca1cd7a) 是一个使用 Chainlink oracles 为 Matic 网络上的智能合同带来 2FA 安全性的项目示例。通过连接到高可用性 2FA API 认证服务，Chainlink 使用户能够为其链上资金创建深度防御策略，即使在私钥被盗的情况下也能防止未经授权的转移。



![Digital Bridge uses Chainlink oracles to enable smart contracts secured by 2 Factor Authentication services](img/5075d0e6acf8540bc4675c4f5729a136.png)

<figcaption id="caption-attachment-2259" class="wp-caption-text">Digital Bridge 使用 Chainlink oracles 启用由双因素认证服务保护的智能合同</figcaption>





### 知识产权

所有类型的知识产权，从版权和商标等版税到专利许可费，都可以转化为智能合同。Chainlink 可用于检查 ip 数据库的所有权验证，在 IP 访问之前验证链外凭证，并方便用户向 IP 所有者付款。智能合同甚至可以将知识产权的部分所有权令牌化，并根据个人的股份比例来分配报酬。像微软和 EY 这样的大型企业已经证明这是一个[实用的解决方案](https://internetofbusiness.com/microsoft-ey-launch-blockchain-solution-for-royalties-management/),可以显著降低版权和版税管理流程中的运营效率低下问题。

### 捐款奖金

开源技术越来越受欢迎，并可以从更广泛的奖励计划中受益，以激励贡献。然而，验证贡献者的工作并向他们付款通常是手动过程，增加了成本并延迟了支付时间表。Chainlink oracles 可用于跟踪 GitHub 等公共代码库上的贡献，并在奖金的预定义测试案例无误通过后解锁支付托管。

## 政府

虽然社会可能不会在各种问题上达成一致，但大多数人可以支持的一项倡议是在政府机构中建立更多的透明度、问责制和效率。区块链为社会提供了跟踪和执行政府流程的新基础设施，智能合同为政府如何采取行动提供了防篡改的防护栏，oracles 允许使用客观数据来触发这些行动的执行，而不是总是留给集中解释。Oracles 是在政府流程中实现智能合同价值的最重要因素之一，因为它们既提供了将遗留基础设施连接到区块链的桥梁，又充当了执行合同的最终触发器。

### 规章制度

企业使用智能合同将需要新形式的自动化法规遵从性。虽然一些限制可以硬编码到智能合约的编程代码中，但政府也可以利用 oracle 作为从智能合约中提取元数据的方式，或者在广播交易之前需要政府运营的 Oracle 的外部批准。

托管和信托清算公司(DTCC)发起的 [Project Whitney 案例研究](https://www.dtcc.com/news/2020/may/18/dtcc-unveils-proposals-to-explore-further-digitalization)中概述了合规 Oracle 的一个示例，该公司是一家交易后金融服务公司，负责结算美国绝大多数证券交易。如案例研究中所述，法规遵从性 oracle 是一个“动态规则引擎，使发行者和投资者能够通过批准/拒绝交易，在整个证券生命周期中保持法规遵从性。交易获得批准后，库存记录会更新，代币会在链上移动。”

### 投票

考虑到最近围绕选举结果的两极分化，人们越来越需要安全、防篡改的投票解决方案来确保选举过程的完整性。虽然彻底检查政府投票系统可能需要时间，但人们可以想象一个简化的场景，其中可以使用私钥在链上进行投票，oracle 可以通过 DECO 以保护隐私的方式从多个批准的来源验证该人的 ID，如果匹配，则在链上发布确认，将其存储为不可变的记录，任何人都可以通过加密验证。这导致通过防篡改投票创造更可持续的民主，符合联合国的可持续发展目标[](https://sdgs.un.org/goals)。

### 契约/许可证/证书

智能合同可用于提高政府证书、许可证和契约的发放效率和完整性。Oracles 可以用来更自主地生成证书，比如在向用户发送令牌化的文档(比如许可证)之前，使用 DECO 来验证用户的凭证。使用 DECO 这样的系统允许智能合同以保护隐私的方式查询一组权威来源。这样的自动化过程可以节省数十亿美元的政府开支。

 **### 再生农业

结合物联网传感器和卫星数据的链上代码和真实世界数据的混合智能合同可以用来创建完全可追溯、透明和自动化的激励系统，直接奖励参与[可持续实践](https://www.weforum.org/agenda/2021/06/blockchain-can-help-us-beat-climate-change-heres-how/)和应对气候变化并减轻其有害影响的个人、公司和政府。这可以包括创造象征性的碳抵消、可再生农业，甚至监控消费以奖励那些量入为出的人。

[绿色世界运动](http://greenworld.org/) 是一个项目的例子，该项目旨在使用混合智能合同来激励与 IC3 合作创建的再造林项目中的再生农业，并由 [Chainlink 社区赠款](https://blog.chain.link/reversing-climate-change-how-hybrid-smart-contracts-incentivize-regenerative-agriculture/) 资助。这个项目使用卫星遥感数据，这些数据由 Chainlink oracles 提供，以奖励帮助退化土地重新造林的再生农业管理者。通过激励碳减排，他们的计划是最终种植数十亿棵树，并帮助提高发展中地区人民的生活和健康水平。

![Blockchain-based hybrid smart contracts reversing climate change](img/e5ebd8e66438ecde16b4d4616f704ae2.png)

<figcaption id="caption-attachment-1841" class="wp-caption-text">How AIRS incentivizes regenerative agriculture using satellite data, Chainlink oracles, and hybrid smart contracts.</figcaption>



### 卫星图像和无人机

虽然稍微先进一些，但不难想象未来卫星图像将与物联网网络和无人机结合使用，以收集建筑项目等外部活动的数据。通过人工智能，可以对数据进行分析，并与过去的项目进行交叉参考，以确定项目的完成百分比。Chainlink oracles 可以将这些数据转发给一个链上智能合同，向建筑公司发放基于完工的支出，为执行大型耗时项目的公司解决现金流延迟的主要问题。

在 Chainlink Labs 首席科学家 Ari Juels 和 Chainlink 联合创始人 Sergey Nazarov 的一次炉边聊天中，Ari 讨论了他和博士生 Sishan Long 在一个名为 AIRS:造林管理自动化激励的项目中的早期工作。AIRS 旨在通过持续获取卫星数据(碳捕获能力、碳封存能力、碳同步能力等)来激励环境管理。)并使用可信执行环境监控其状态。这个想法是，政府和非政府组织等实体向智能合同投入资金，然后分配给负责维护和扩大这一非常重要的碳汇的人，激励可持续的做法。

## 离链计算

### 可证实的随机性(VRF)

由于区块链网络的确定性，链上应用程序无法访问安全随机数生成器(RNG)。使用链上块哈希可能导致区块链矿工/验证者的操纵，他们丢弃具有不利哈希的块，并可以“重新掷骰子”，最终改变 RNG 值。幼稚的外链解决方案是不透明的，无法证明产生的 RNG 值是合法的，并且没有被数据源或 oracle 节点操纵。 [Chainlink 可验证随机函数](https://blog.chain.link/chainlink-vrf-on-chain-verifiable-randomness/) (VRF)通过为智能合约提供安全的随机来源来克服这些问题，该来源由加密证明支持，不能被 oracle 节点、用户或开发团队操纵。

Chainlink VRF 的工作原理是将发出请求时未知的块数据与 oracle 节点预先提交的私钥相结合，以生成一个随机数和一个加密证明。消费智能合约将只接受随机数输入，如果它有一个有效的加密证明。这为用户提供了直接在链上的自动化和公开可验证的保证，即每个使用 VRF 链的智能合约应用程序都是可证明公平的。可验证的随机性可以在广泛的用例中使用，包括动态 NFTs、链上游戏应用程序、链外系统等等。

![Chainlink VRF](img/3f8cb27719fbdfee5c718c29c46bb31e.png)

<figcaption id="caption-attachment-2278" class="wp-caption-text">Chainlink VRF provides smart contracts a secure source of randomness</figcaption>



### 自动化

智能合约是在区块链上确定性运行的代码片段。然而，默认情况下，它们是“休眠”的，必须被一些外部实体“唤醒”来执行链上功能和改变契约状态。[chain link Automation](https://blog.chain.link/chainlink-automation-open-beta-is-live/)通过一个高度可靠、分散且具有成本效益的分散式节点网络，为智能合同开发者、分散式应用程序(dApps)和分散式自治组织(DAOs)提供了解决这一问题的方案，该网络可以自动化任何智能合同功能并执行定期合同维护。

Chainlink Automation 可用于广泛的智能合约功能，包括在 DEX 上执行限价单，在储备价值增加时铸造新代币，从金库中获取收益，对弹性供应代币进行再基准化，触发自动化交易策略，清算抵押不足的贷款，释放归属代币，补足低于阈值的代币余额，等等。

![How Chainlink Keepers automates smart contract functions](img/3bd9bddcfbd7e178d3d471987f4f8f09.png)

### 跨链互操作协议(CCIP)

一个区块链不太可能主宰整个智能合约市场，尤其是考虑到吞吐量限制、管辖权差异和连锁专业化。这样一个多区块链世界意味着区块链必须相互交流。然而，由于其固有的安全属性，区块链无法本地访问其他区块链网络上的数据，这与甲骨文的问题非常相似。通过在一个区块链上读取数据，在另一个上写入结果，作为触发某种类型的跨链交互和/或只是请求信息的链上的链上事务的一种方式，Chainlink oracles 可用于弥合这一差距。

[跨链互操作性协议](https://blog.chain.link/introducing-the-cross-chain-interoperability-protocol-ccip/) (CCIP)是一个开源标准，它将提供一个安全、分散和可扩展的跨链消息传递解决方案，使任何区块链网络上的智能合约能够跨任何其他区块链网络发送消息、传输令牌和启动操作。除了链之间的通用消息传递，CCIP 还支持创建跨链桥，如可编程令牌桥参考实现，允许将令牌和命令一起传输到任何其他区块链网络。

![Cross-Chain Interoperability Protocol (CCIP)](img/064aa60ac16cd744ce5e5a18cc15b90f.png)

<figcaption id="caption-attachment-2272" class="wp-caption-text">The Cross-Chain Interoperability Protocol (CCIP) enables the creation of cross-chain bridges.</figcaption>



### 公平测序服务公司(FSS)

虽然链式 oracles 通常被认为能够以可靠和安全的方式从链上的真实世界获取和传递数据，但是它们也可以执行各种链外计算，包括事务的排序。Chainlink 开发的[公平排序服务](https://blog.chain.link/chainlink-fair-sequencing-services-enabling-a-provably-fair-defi-ecosystem/) (FSS)将允许分散式应用程序通过确保交易排序不会被矿工操纵为从用户那里榨取价值的手段来降低矿工可提取价值(MEV)。此外，通过防止抢先攻击，天然气成本可以大幅降低，dex 可以变得更加值得信赖(例如，交易根据更公平的规则兑现，如交易到达 mempool)。

![Chainlink Fair Sequencing Services enables the fair ordering of transactions to mitigate issues caused by miner extractable value (MEV)](img/21b82e9b23772a8d3a749cb5a1ecd6df.png)

<figcaption id="caption-attachment-749" class="wp-caption-text">Chainlink Fair Sequencing Services enables the fair ordering of transactions to mitigate issues caused by miner extractable value (MEV)</figcaption>



### 区块链气价

为了防止垃圾邮件攻击，支持智能合约的区块链上的交易需要本地令牌中的汽油费来支付矿工验证交易所花费的成本。然而，决定天然气价格的市场发生在供应链之外，因此智能合同需要一个 oracle 来获取每单位天然气的当前成本。

这方面的一个例子是[【ETHA】Lend](https://medium.com/etha/etha-lend-integrates-chainlinks-gas-price-feed-into-their-discovery-api-to-provide-algorithmic-564110fb66ae)，这是一个链上产量优化器，它使用 Chainlink gas price oracle 来帮助构建和执行 LPs 的算法优化产量策略。智能合约还可以使用这种天然气价格 oracle 来创建天然气价格金融产品和其他金融产品，这些产品旨在对冲区块链网络拥塞和高交易成本。

### 公平的参与者选择

随着基于区块链的公共销售的出现，许多项目正在寻找超越常见的“先到先服务”模式的公平选择销售参与者顺序的方法，这种模式很容易操纵。最初由集中交易所推广，现在越来越倾向于在智能合约中随机选择销售参与者。

一个例子是 [Centaur](https://medium.com/centaur/chainlink-vrf-used-by-centaur-to-deploy-new-standard-for-enhanced-transparency-in-public-sale-3cc0fa5b10e6) ，一个 DeFi 平台，使用 Chainlink VRF 来确定在线公开销售的参与者。基于销售前积累的地址列表，链家 VRF 以可验证和公平的方式确定该列表中的哪些地址被允许参与链上公开销售。



![Centaur uses Chainlink VRF to select participants in an on-chain public sale, ensuring equal opportunity of access](img/fd6b3ba04df953e8f1b748fb73586815.png)

<figcaption id="caption-attachment-748" class="wp-caption-text">Centaur 使用 Chainlink VRF 来选择网上公开销售的参与者，确保平等的机会进入</figcaption>





另一个例子是 [Get Protocol](https://medium.com/get-protocol/get-protocol-integrates-chainlink-vrf-to-further-improve-blockchain-ticketing-solution-864c7056e73d) ，这是一个位于区块链的活动票务解决方案，它使用 Chainlink VRF 随机确定点播音乐会和活动的数字排队。这为用户提供了获得门票的平等机会，以这种方式，他们可以独立地验证链上的公正。

### 随机节点选择

一些协议使用不可预测性作为一种安全形式，例如通过随机选择块生产的验证器。不安全的随机性来源将允许恶意行为者过度地将自己插入到过程中，并操纵块的产生，甚至可能使网络停止。Chainlink VRF 可以用作随机的防篡改源，在每次需要产生一组交易时公平地选择验证器，保护区块链网络免受一大类关键攻击媒介的攻击。

## 结论

作为构建分散式 oracle 网络的通用框架，Chainlink 为开发人员提供了将智能合约应用程序连接到其用例所需的任何真实数据或事件所需的工具。虽然上面列出的用例并不是一个详尽的列表，但由于 Chainlink 使无数的智能合约用例成为可能，我们相信它们为有兴趣构建新的创新型分散式应用程序的开发人员提供了一个起点。

如果您是一名开发人员，并且希望快速将您的智能合同应用程序连接到 Chainlink oracles，请访问[开发人员文档](https://docs.chain.link/)，并参加 [Discord](https://discordapp.com/invite/aSK4zew) 中的技术讨论。如果您想安排一次电话会议，更深入地讨论整合事宜，请点击此处的。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink) | [Reddit](https://www.reddit.com/r/Chainlink/) | [时事通讯](https://chn.lk/newsletter) | [YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA) | [电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://www.chain.link/solutions/defi)** **