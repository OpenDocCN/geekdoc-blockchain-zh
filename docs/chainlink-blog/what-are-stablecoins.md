# 什么是 Stablecoins？

> 原文：<https://blog.chain.link/what-are-stablecoins/>

*更新于 2022 年 4 月 18 日。T3】*

稳定货币是一种加密货币，试图将其市场价值与另一种资产挂钩，如法定货币。

虽然加密货币通常以其波动性而闻名，但 stablecoins 通过允许美元等法定货币作为数字代币在区块链上出现，为加密货币市场带来了相对的稳定性。这些稳定币允许世界各地的任何人持有一种代币，这种代币是为了保持其相对于其声称代表的法定货币的价值而特意设计的(例如，1 美元稳定币试图保持 1 美元的价值)。对区块链稳定资产的渴望，导致区块链行业内广泛采用稳定资本和 [【去中心化金融】](https://chain.link/education/defi) 。

[https://embed.theblockcrypto.com/data/decentralized-finance/stablecoins/total-stablecoin-supply-daily/embed](https://embed.theblockcrypto.com/data/decentralized-finance/stablecoins/total-stablecoin-supply-daily/embed)

  *稳定的货币供给总量的爆发式增长。( [来源](https://www.theblockcrypto.com/data/decentralized-finance/stablecoins) )*

在本文中，我们将围绕 stablecoin 探讨一些基本问题——它们是什么，如何工作，以及 Chainlink [神谕](https://chain.link/education/blockchain-oracles) 如何为各种 stable coin 设计提供动力。

## 什么是稳定币？

从本质上来说，稳定货币是试图保持“挂钩”的加密货币——与它们所代表的外部资产具有相同的市场价值。稳定货币可以采取几种方法来匹配它们所盯住的货币的价格，比如用外部资产抵押或算法机制，比如根据需求动态调整供给。

稳定的公司主要有两种类型:集中的和分散的。传统上，中央稳定币由非连锁银行账户中的法定货币支持，该账户作为支持连锁代币的储备。或者，他们可能会跟踪另一种资产，如商品、指数或其他。虽然 [链式储备证明](https://chain.link/proof-of-reserve) 可以通过自动审计提供强大的透明度保证，但这些稳定币设计通常需要对保管人的信任。

分散的稳定信贷通常被链上加密货币超额抵押，并需要价格数据来维持完全抵押(例如，用户的抵押品价值大于其贷款总价值的某个百分比)。分散的 stablecoins 被设计成更有弹性和更透明，因为它们不是由单一方控制的，并且协议的抵押可以由链上的任何人审计。  算法稳定银行通常不持有储备，而是使用智能合约来编纂一种机制——类似于央行的机制——通过动态供应调整或其他方法来保持其与目标指数的挂钩。

另一种类似于稳定货币的数字资产是中央银行数字货币(CBDCs)。中央银行跟单信用证类似于中央银行发行的稳定货币，但它们不一定要有非连锁银行账户中的法定货币支持。中央银行跟单信用证被发行它们的政府视为法定货币，用于简化个人和机构之间的支付。

## Stablecoins 是如何工作的？

稳定的货币利用各种经济机制通过保持其盯住汇率来保持相对稳定。最常见的例子包括将代币兑换为法定货币的能力、抵押债务头寸、套利、弹性供给等等。

### 稳定点的类型

[](https://www.circle.com/en/usdc)是一个中央集权的稳定币发行圈。每一个 USDC 都由一美元或等值的资产支持，由受监管的金融机构的非连锁账户持有。拥有美元银行账户的客户可以用 1 USDC 兑换 1 美元，确保代币与美元保持 1:1 的挂钩。其他类似的中央集权国家包括 USDT、BUSD、TUSD、USDP 等。一些集中式 stablecoins 使发行者能够冻结属于某个地址的令牌，有效地使冻结的令牌不可用。稳定硬币发行者可以使用这种方法来冻结通过协议破解或利用获得的大量稳定硬币。

[MakerDAO](https://makerdao.com/) ，一个去中心化的 stablecoin 协议，通过让用户将抵押品锁定在一个智能合约中来维持其钉住机制。然后，智能合约将稳定的硬币 DAI 铸造为可调整利率的超额抵押债务。为了维持 1 美元= 1 戴的 1:1 挂钩，MakerDAO 的智能合同通过链上管理调整 MKR 代币持有者设定的利率，以鼓励借款人偿还债务或获得更稳定的外币贷款。通过利率变化鼓励总供给的增加或减少，DAI 的价格将发生变化，当供给和利率低时其价值上升，当供给和利率高时其价值下降。

分散稳定币的另一种设计涉及在稳定币指数中使用套利，其中稳定币由多个不同的稳定币支持，以实现挂钩的稳定性。例如，如果一种储备稳定币的价格超过 1 美元，而整个指数价格低于 1 美元，那么智能合约将在市场上出售超过 1 美元的稳定币作为指数稳定币的令牌，以推动指数价格回升到 1 美元。Chainlink oracles 可以提供可靠和高质量的价格信息，stablecoin 指数智能合约可以在计算如何重新平衡指数时参考这些信息。

[安普尔福思](https://www.ampleforth.org/)【AMPL】是一种分散的、算法稳定的货币，它使用弹性供应机制来维持其与当前消费者价格指数(CPI)的挂钩，CPI 是经济分析局关于经通胀调整的 2019 年美元现值的指数。这实际上意味着 AMPL 的价格目标被设定为 CPI 所代表的 2019 年 1 美元的购买力。当 AMPL 的价格高于指数时，协议增加钱包余额，而当 AMPL 的价格低于指数时，协议减少钱包余额。这种供应的自动变化被称为重定基数，通过调整未偿还代币供应来影响市场价格。AMPL 的总供应量按日重定基数，以跟踪消费物价指数——AMPL 的量加权平均价格(VWAP)和消费物价指数均由 Chainlink oracles 提供给 Ampleforth 协议。

## 稳定的硬币是用来做什么的？

Stablecoins 是加密货币和 [Web3](https://chain.link/education/web3) 生态系统不可或缺的一部分，占其交易量和基础经济活动的重要部分。

由于[](https://blog.chain.link/what-is-blockchain/)是促进价值转移的潜在机制，而不是不透明、过时的手动流程，Stablecoins 提供了一些优于传统同行的独特优势。集中的稳定货币有效地允许与法定货币挂钩的价值在全球钱包之间转移，而不需要中间人来促进转移。    【stable coins】也常用作非保管性储蓄账户，存放个人储蓄或作为抵押品在 DeFi 中产生收益，从事[](https://chain.link/education/defi/yield-farming)策略。

## 稳定资本风险

不同的 stablecoin 设计具有不同的相关风险。这些可能包括:

*   **脱钩风险**—通过流动性事件、“银行挤兑”情景、次优储备实践等表现出的潜在经济或算法机制的失败，以及更为明显的稳定货币脱钩于其目标的风险。
*   **监管风险**—在特定的地理位置，当地金融机构可能会以不同的方式监管稳定的信贷。
*   **中央集权风险**—一些中央集权的稳定硬币发行者有能力在特定的钱包地址冻结代币。
*   **密钥管理风险**—如果 stablecoins 存放在非保管钱包中，用户必须全权负责安全存储其私钥。

## 使用 Chainlink 的 Stablecoin 应用程序

尽管 stablecoin 的架构和设计有所不同，但所有 stable coin 都需要准确的价格数据，以支持其潜在的挂钩机制，并在分散应用中使用。由于汇率不断波动，实时价格数据需要输入到稳定的货币中，以维持其盯住汇率。此外，由于 stablecoins 通常由其他加密资产或链外银行储备支持，因此需要获取这些储备细节的防篡改方法来确保这些系统的安全性和可靠性。

[Chainlink](https://chain.link/) 是一个去中心化的 oracle 网络，它为智能合同提供对安全可靠的真实数据源的访问。由于 stablecoins 在 DeFi 应用中具有重要价值，因此它们需要与区块链相同的保证和安全保障。实际上，这意味着向 stablecoins 提供数据的 oracles 需要健壮、分散，并具有 [多层安全](https://blog.chain.link/levels-of-data-aggregation-in-chainlink-price-feeds/) 来帮助确保 stable coins 保持 1:1 的比率。这为这些 stablecoin 的用户提供了透明度和信任，因为他们可以确认他们正在使用的 stable coin 资产是端到端安全的，并且不包含单点故障。

这方面的一个例子是[true USD](https://www.trusttoken.com/trueusd)【TUSD】，它使用 Chainlink 来提供链上担保级别的详细信息，并让用户清楚地了解他们的资产是否得到充分支持。凭借这种新发现的透明度，DeFi 用户可以实时验证所有铸造 TUSD 代币的真实抵押情况，协议本身可以自动保护用户资金免受任何部分准备金做法或潜在黑天鹅事件的影响。

![A diagram showing how TrustToken uses Chainlink to provide smart contracts proof of its off-chain fiat reserves.](img/efe07a592ea9bdbad4ef45d2a14e71b1.png)

<figcaption id="caption-attachment-1394" class="wp-caption-text">TrustToken uses Chainlink Proof of Reserve to provide smart contracts proof of the off-chain fiat reserves backing the TUSD stablecoin.</figcaption>



这种验证资产储量的机制利用了 Chainlink [【储量证明】【PoR】](https://chain.link/proof-of-reserve)。PoR 参考源为智能合约提供所需的数据，以计算任何由链外储备支持的链上资产的真实抵押。这些参考源由 Chainlink 网络上的分散式 oracles 网络操作，允许对协议中使用的抵押品进行实时自主审计，有助于确保用户资金免受不可预见的部分准备金做法和链外托管人的其他欺诈活动的影响。

对于利用链外储备的稳定币协议，PoR 链家支持的重复审计有助于提高透明度，并确保支持稳定币的储备状态。使用 PoR 的稳定帐户可以向用户提供更高的透明度，因为他们可以证明他们的令牌是受支持的。PoR 还可以提供有关任何类型的挂钩资产的抵押数据，包括替代法定货币或黄金等商品，从而增加了利用这一机制的任何令牌协议的透明度。

[金融市场基础设施和加密经纪平台 Paxos](https://www.paxos.com/paxos-adopts-chainlink-oracles-to-further-adoption-of-pax-and-paxg-in-defi/) 使用 Chainlink 为美元支持的 stablecoin Pax Dolar (USDP)和黄金支持的 token PAX Gold (PAXG)提供高可用性、防篡改和准确的链上定价数据源。此外，Chainlink [为 Paxos 代币](https://data.chain.link/ethereum/mainnet/reserves/paxg-reserves)提供的储备数据证明允许 DeFi 应用程序快速验证代币是否以 1:1 的比例得到美元的完全支持，金条是否由 Paxos 在链外托管。 

![A diagram showing how Paxos uses Chainlink to verify collateralization.](img/c8492bf226e793d823a8c27599c7d3d5.png)

<figcaption id="caption-attachment-1395" class="wp-caption-text">How Paxos uses Chainlink Proof of Reserve to verify the collateralization of off-chain assets.</figcaption>



链式稳定币体系的另一个例子是 [费协议](https://fei.money/) ，它实际上起到了算法中央银行的作用，旨在通过所谓的重新加权过程，在公开市场上维持其稳定币的挂钩。用户可以用等价的 ETH 存款值铸造稳定币 FEI，该值将添加到方案储备中，用作方案控制值(PCV)。PCV 代表用户不可赎回的所有资产。如果 FEI 在钉住汇率之下交易，PCV 用于在公开市场上购买 FEI 以推高价格，如果 FEI 在钉住汇率之上交易，则铸造更多的 FEI 并在公开市场上出售以推低价格。Fei 协议使用 Chainlink 价格反馈来帮助确保在所有市场或网络条件下参考准确的数据。

央行数字货币(CBDCs)也可能与外部资产挂钩，这意味着它们需要能够接收关于该资产的价格数据。Chainlink 可以支持这些政府发行的稳定货币，为它们提供维持挂钩所需的价格数据，以及有关系统当前抵押的重要信息。

## 结论

尽管很简单，stablecoins 可以被认为是加密货币行业最重要的创新之一，它允许稳定价值的无缝转移。虽然有许多不同的 stablecoin 设计，但任何 stablecoin 协议的共同基础都是它接收到的关于它所跟踪的资产的数据。Chainlink 提供久经考验的数据基础设施，有助于确保 stablecoins 的可靠性、安全性和透明度，以及更大的 DeFi 生态系统的稳定性。

如果您是一名开发人员，并且想要将 Chainlink 集成到您的智能合同应用程序中，请查看 [开发人员文档](https://docs.chain.link/docs) 或 [联系专家](https://chainlink.typeform.com/to/gEwrPO) 。

## 附加资源

*   [什么是 DeFi(去中心化财政)？T3】](https://chain.link/education/defi)
*   [什么是智能合约？T3】](https://chain.link/education/smart-contracts)
*   [数据质量对于 DeFi 的重要性](https://blog.chain.link/the-importance-of-data-quality-for-defi/)
*   [链环准备金证明:为 DeFi 抵押品带来透明度](https://blog.chain.link/chainlink-proof-of-reserve-bringing-transparency-to-defi-collateral/)
*   【Ampleforth 如何使用 Chainlink 分散其重置基础机制