# 什么是储量证明？

> 原文：<https://blog.chain.link/proof-of-reserves/>

全球金融体系通常以抵押不足和高度不透明的方式运行，从而产生系统性风险，可能导致繁荣和萧条周期以及市场范围内的失败。[【DeFi】](https://chain.link/education/defi)通过提供高度透明、信任最小化的金融产品提供了一种替代方案，这些产品由确定性智能合约和 [密码真实性](https://blog.chain.link/what-is-cryptographic-truth/) 提供支持。随着 DeFi 的增长，对新抵押品类型的需求不断增加，这些新抵押品类型超出了本地链上资产的范围，包括跨链令牌、菲亚特支持的 stablecoins、令牌化的真实资产等。

在本文中，我们将分解什么是储备证明链(PoR ),以及它如何帮助在加密货币生态系统中提供更强的安全保证和更大的透明度。此外，我们还将探索顶级 DeFi 团队已经实施的 PoR 参考源，并为未来的使用案例和实施提供背景。

## 什么是储备证明？

准备金证明传统上是指持有加密货币的企业创建关于其准备金的公开证明，以通过独立审计向其储户证明其偿付能力。由于这些审核通常由集中的第三方完成，因此可能会耗时且需要手动流程。

随着开发人员继续在数字资产生态系统中构建越来越复杂的金融产品，需要一种可靠、透明和分散的标准，以便利用区块链、 [【智能合约】](https://chain.link/education/smart-contracts) 和甲骨文—进入 PoR chain link 的卓越透明度，使用自动化流程对储备进行审计。

## 链环储备证明(PoR)

[Chainlink 准备金证明](https://chain.link/solutions/proof-of-reserve) 为智能合约提供计算任何由链外或跨链准备金支持的链上资产的真实抵押所需的数据。通过由[Oracle](https://chain.link/education/blockchain-oracles)组成的分散式网络运营，chain link Proof Reserve 支持对抵押品进行实时的自主审计，有助于确保用户资金免受不可预见的部分准备金做法和来自链外托管人的其他欺诈活动的影响。无需强迫用户相信托管人提供的书面担保，Chainlink PoR 可以部署用于自动在线审计，为用户提供资产基础抵押的高级担保，并为资产抵押相关的加密资产生态系统带来更高的透明度。

此外，Chainlink PoR 还越来越多地被用于保护包装资产的铸造、赎回和焚烧。一旦 Chainlink PoR 确定包装的代币不足，可以使用[chain link Automation](https://chain.link/automation)停止包装代币的铸造、兑换和燃烧。

## 跨链资产准备证明

作为一个高度灵活和透明的 oracle 网络模型，Proof of Reserve 通过提供各种资产的抵押数据和释放 [跨链](https://chain.link/cross-chain) 流动性，帮助加速 DeFi 的增长。由于 Chainlink 是区块链不可知的，Chainlink PoR 饲料可以构建为提供任何智能合约支持的区块链上结算的任何跨链资产的抵押数据。

### 比特币的储备证明

以太坊上的令牌化比特币代表了 DeFi 中使用的抵押品的重要部分。Chainlink PoR 参考源向 DeFi 应用程序提供审计 [BitGo 的 WBTC](https://blog.bitgo.com/chainlink-brings-onchain-proof-of-reserve-to-wbtc-fcda00f2815c) 和 [Ren Protocol 的 renBTC](https://medium.com/renproject/chainlink-brings-onchain-proof-of-reserve-to-renvm-d5e66839850a) 的储备所需的数据，这些储备共同代表区块链以太坊上所有包装比特币的大部分。

这些储备证明由 Chainlink oracles 网络提供支持，该网络每十分钟检查一次比特币区块链上托管人地址的 BTC 余额。每当检测到与存储在链上的先前余额的偏差超过预定义的阈值时，链上的储量证明参考馈送就会用新的余额数据进行更新。

通过使这种储备数据在链上可用，基于智能合约的 DeFi 应用能够采用定制的逻辑，在抵押不足事件期间，即当支持跨链代币的比特币少于预期数量时，自动保护用户资金。这一功能对于使用令牌化比特币作为抵押品来确保借用其他数字资产的应用程序尤其有益。  



![A diagram showing a Chainlink Proof of Reserve data feed for WBTC.](img/9a8dd1698013b3936894ba8fbe9f22b6.png)

<figcaption id="caption-attachment-712" class="wp-caption-text">Chainlink Proof of Reserve provides smart contracts proof regarding the amount of Bitcoin backing BitGo’s tokenized WBTC.</figcaption>



令牌化比特币的储备证明参考源还解锁了新的金融产品，如 [信用违约掉期](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/#credit-default-swaps) ，使用户能够对冲部分储备活动，并推测特定令牌化比特币实施的抵押健康状况。由于提供了额外的安全性和透明度，在 DeFi 内对冲令牌化比特币的风险敞口可以增加经济活动。

## 菲亚特支持的稳定信贷储备证明

[Stablecoins](https://blog.chain.link/what-are-stablecoins/) 是 DeFi 生态系统中的一个关键组成部分，为用户提供了以波动性相对较低的货币进行交易并赚取收益的能力，同时还能受益于智能合约的确定性。因此，stablecoins 是一种受欢迎的附属选择，也是扩大 DeFi 产品采用范围的基础。

随着 stablecoin 生态系统的价值超过 1000 亿美元，为智能合约提供证据证明每种担保 stablecoin 都由链外银行账户中等量的价值完全支持变得越来越重要。

通过利用专业审计员生成的数据，Chainlink PoR 公司为智能合约应用程序提供有关菲亚特支持的稳定信贷的链外储备的抵押数据。作为一个主要的例子，TUSD [储备证明和供应证明](https://blog.trusttoken.com/trusttoken-introduces-proof-of-reserve-for-tusd-stablecoin-in-collaboration-with-chainlink-and-584b3674b89f?gi=889128a78984) 参考源为 DeFi 申请提供了关于 TrustToken 托管银行账户中持有的支持 TUSD 代币的美元金额以及在多个区块链铸造的 TUSD 代币供应量的明确证明。

为了支持 TUSD 储备证明参考源，Chainlink oracles 从美国排名前 25 位的独立会计公司 Armanino 获取数据，该公司定期审查 TrustToken 托管的银行账户。当 TrustToken 储备中持有的美元数量超出预定义的阈值时，会通过链向储备证明参考源推送更新。然后，DeFi 应用程序可以利用这些数据按需审计 TUSD 代币的储备。



![A diagram showing a Chainlink Proof of Reserve data feed for TUSD.](img/e9edd8a9d9ce71d55cee783cbf817f30.png)

<figcaption>Chainlink Proof of Reserve provides smart contracts proof regarding the amount of US dollars backing TrustToken’s stablecoin TUSD.</figcaption>



根据这一模型，储备证明参考源可用于跟踪由非链法定储备支持的任何稳定货币的抵押。通过这些数据，stablecoins 的经济活动可以在 DeFi 内加速，不仅来自零售用户，也来自寻求在分散金融生态系统中安全产生收益的传统机构。

除了美元支持的稳定资产——这是 DeFi 生态系统中最受欢迎的挂钩资产——还可以构建储备源的 Chainlink Proof，以提供任何类型的挂钩资产的抵押数据。这可以包括英镑等法定货币或黄金等大宗商品，从而增加 DeFi 内部整个类别的透明度。例如，Paxos 正在使用[chain link PoR feeds](https://data.chain.link/ethereum/mainnet/reserves/paxg-reserves)使 DeFi 应用程序能够快速验证其 PAX Gold (PAXG)令牌是否完全由 Paxos 保管的链外金条支持。

## 传统市场的储备证明

虽然当前的实施方式提供了加密货币生态系统中当前使用的令牌抵押的透明度，但链连接储备证明模型的范围更广，可用于为任何已令牌化和链上的资产带来透明度。以前需要对发行者不切实际的信任级别的令牌化资产现在能够利用储备证明来提供用户采用所需的透明度。

![A diagram showing how Chainlink PoR helps secure wrapped tokens backed by off-chain reserves.](img/3cef118d8a39c154535fb50096ab76ab.png)

<figcaption id="caption-attachment-3349" class="wp-caption-text">How Chainlink PoR helps secure wrapped tokens backed by off-chain reserves.</figcaption>



chain link PoR feed 可用于各种各样的令牌化现实资产，如产生可核实现金流的房地产。财产的所有权和持有所产生的美元现金流的托管银行账户都能够被审计和链上，使智能合同能够创造房地产财产及其现金流的信任最小化的符号化表示，并由 Chainlink oracles 的分散网络验证抵押。

此外，Proof of Reserve feeds 还可用于 DeFi 和智能合约应用之外的领域。例如，他们可以为传统金融机构提供一种方法，通过使用 Chainlink oracles 将他们的审计报告作为不可改变和防篡改的记录发布到链上，来增加客户和交易对手的信任。

通过利用区块链技术，而无需对其业务模式或 [后端企业系统](https://blog.chain.link/chainlink-enterprise-blockchain-middleware/) 进行任何修改，机构可以提供有关其资产的确定且不变的真实来源，从而创造出前所未有的透明度。此外，DeFi 产品可以围绕这些数据构建，允许用户对冲传统链外机构的部分准备金活动。

## 结论

Chainlink Proof of Reserve 为不断增长的 DeFi 生态系统和传统金融系统提供了一种方法，通过对任何资产的真实抵押进行明确的链上证明来提高其运营的透明度。随着智能合约生态系统的发展，确保不透明的运营流程和有毒抵押品导致的市场失灵成为历史至关重要。有了 Chainlink Proof of Reserve，DeFi 生态系统就能很好地扩展并帮助保护下一代信任最小化的金融产品。

如果您想了解更多关于 Chainlink 预留证明的信息，请访问[PoR 产品页面](https://chain.link/proof-of-reserve)。如果您是一名开发人员，并且想要将 chain link Proof Reserve 集成到您的智能合同应用程序中，请查看 [开发人员文档](https://docs.chain.link/) 或 [联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog) 。