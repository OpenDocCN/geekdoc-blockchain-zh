# 什么是赌注？区块链，神谕，和 DeFi

> 原文：<https://blog.chain.link/what-is-staking/>

*Chainlink Staking v0.1 现已[在 mainnet](https://staking.chain.link/) 上线。*

Staking 是一个经常用来描述锁定加密货币作为抵押品以帮助保护特定区块链网络或智能合约协议的术语。赌注通常也用于加密货币存款，指定用于提供 DeFi 流动性、获取收益回报和获得治理权。加密货币赌注涉及锁定网络或协议中的令牌以获得奖励，这些令牌用于帮助为用户提供关键服务。

在本帖中，我们将探索加密货币的基础知识，它是如何工作的，以及为什么它在区块链和 DeFi 生态系统中被广泛使用。我们还研究了 [甲骨文网络](https://chain.link/education/blockchain-oracles) 的利益相关动态与区块链网络内现有实施中的利益相关相比有何不同。

## 在区块链，赌博是如何进行的？

为了让区块链保持安全并保持高度的 [拜占庭容错](https://en.wikipedia.org/wiki/Byzantine_fault) ，他们需要一种 Sybil-resistant 机制——一种防止一小部分节点破坏网络的方法。如果区块链的 Sybil 抵抗力较弱，区块链更容易受到 51%的攻击，其中一小部分或串通的行为者可以从事恶意活动，如重写链的历史和审查用户。

一个块只是作为区块链分类帐更新的一部分一起验证的一批用户交易。每个块不仅包含这个新的事务信息，而且还包含一个对以前块的引用，它以散列的形式将块按时间顺序加密地连接在一起；即块+链。验证器/挖掘器的任务是产生块并将它们推荐给网络。如果被其他验证者/挖掘者和完整节点的多数共识认为是有效的，则它们提议的块然后被附加到分类帐。

[https://www.youtube.com/embed/LRiA2OWGwtw?feature=oembed](https://www.youtube.com/embed/LRiA2OWGwtw?feature=oembed)

利益证明(PoS)是区块链的一种 Sybil-resistance 机制，要求验证者在网络中持有财务“利益”,以获得在区块链中添加新区块的机会。在 PoS 区块链，任何下注最低要求的本地硬币余额的人都可以加入网络并成为验证者(下注者)来生成区块。验证者赌注余额的大小或用户操作的验证者数量通常与他们被批量生产选中的机会成正比——赌注余额越高或他们控制的验证者越多，被选中的机会就越大。

当一个验证者节点成功创建一个有效块时，他们通常会收到来自协议的赌注奖励和一部分用户费用。为了抑制恶意行为，PoS 区块链还经常实现一种称为削减的机制，其中验证器节点通过丢失其部分或全部标记令牌来受到惩罚，因为它们被确定违反了协议的规则。一些 PoS 区块链还会没收一部分验证者的股份，如果他们离线时没有生成块，当他们被选择这样做时。

## 区块链标桩的类型:工作证明(PoW)、利益证明(PoS)和委托利益证明(DPoS)

工作证明(PoW) Sybil-resistance 机制，如比特币区块链中使用的机制，涉及矿工竞争解决计算难题(即基于块内的信息产生有效的哈希)。第一个解决它并提交网络批准的有效块的人赢得奖励。比特币网络会自动调整每 2016 个块(大约每 2 周)生成一个有效哈希的难度，以实现 10 分钟的平均块时间目标。难度调整一般基于参与的矿工数量(总 hashrate)，矿工越多，保持网络分散的难度越大。

在 PoW 中，向区块链添加新块的机会与计算工作量成正比。因此，虽然 PoW 区块链没有传统的显式赌注机制，用户可以在智能合同中锁定加密货币，而智能合同可能会被削减，但他们有隐性赌注，即购买昂贵的硬件(通常是特定于应用程序的)，并花费计算能力，只是为了获得奖励的机会，此外还有对正在开采的硬币的金融敞口。如果矿工没有通过采矿奖励获得收入，那么他们在设备和电力消耗上的资本支出就是亏损的。如果网络的安全性得不到维护，那么用于采矿的设备和采矿产生的资产的市场价值可能会下降，从而造成隐性的经济损失。

![Implicit staking Bitcoin](img/dc0f3440b5f912a6ecfb3e054f7d6e7c.png)

<figcaption id="caption-attachment-3356" class="wp-caption-text">Though Bitcoin does not have conventional staking, it does have a form of implicit staking where miners are rewarded in an asset (BTC) that only remains valuable and covers their expenses if they uphold the security of the network.</figcaption>



staked-of-stake Sybil-resistance 机制用 staked 加密货币的要求取代了这种计算工作量要求。换句话说，PoW 系统中的挖掘器与计算能力竞争，而 PoS 系统中的验证器与货币价值竞争。另一个值得注意的区别是，对于每个区块，区块链电力公司在所有矿工之间举行公开竞争，以获得生产区块的机会，而区块链邮政公司通常在验证者之间轮换，以生产区块，通常基于股权加权的随机性。以太坊是一个区块链的例子，它作为被称为[](https://ethereum.org/en/upgrades/merge/)的过程的一部分，从 PoW 转移到 PoS。

![Explicit staking PoS blockchains](img/7eba82565588ad3810c137daff5348dc.png)

<figcaption id="caption-attachment-3357" class="wp-caption-text">PoS blockchains utilize explicit staking, where validators put down a staking deposit that can be confiscated if they deviate from the protocol rules.</figcaption>



PoS 的一个变体是委托利益证明(DPoS ),它旨在通过允许令牌持有者将他们的利益委托给现有的验证者来分离利益相关者和验证者的角色。分离这些角色使代币持有者能够参与批量生产，从而被动地获得奖励，而不仅仅是验证者。然而，与传统的利害关系证明系统(其中每个赌注者运行他们自己的验证软件客户端)相比，这种权衡有时会导致网络验证器数量的减少。

## 赌注奖励

区块链网络中的赌注者通过每笔交易附带的用户费用和区块奖励(新发行的加密货币，分配给成功创建和/或证明区块的验证者)来激励产生有效区块。

协议以不同的方式计算赌注奖励，这取决于许多因素，例如每个验证者下注的硬币数量、验证者已经下注的时间量、网络中下注的代币总量、流通中的代币量与总供应量的比较以及各种其他参数。PoS 区块链对一段时间内发行的报酬率采取不同的方法，但通常根据网络中存放的总股份来确定发行和收益率。

在一些利益证明系统中，令牌持有者群体可以通过集体赌注池来组合他们的资源(赌注权力),以增加他们被选中进行区块验证并获得赌注奖励的机会。如果网络有最低赌注要求，赌注池允许用户在 PoS 区块链中下注他们的代币，即使他们没有达到最低要求。然后，储蓄池获得的回报在储蓄者和储蓄池的经营者之间分享。

## 定义中的定位

Staking 也是 [分散式金融(DeFi)](https://chain.link/education/defi) 协议中常用的术语。DeFi staking 通常指的是在协议中锁定令牌以实现特定的目标或结果，而不是保护块生产。虽然在这种情况下“标记”对于某些用例来说可能被认为是用词不当，但它是整个行业中使用的一个常见短语。

定义定位的一些用途包括:

*   **协议保险** —分散式借贷协议，如 [Aave](https://aave.com/) 使用押记代币作为流动性后盾，持有人可以在协议的安全模块内锁定他们的 Aave 代币，以便在发生黑天鹅事件时为储户提供额外的安全和保险。然后赌注者从协议中获得奖励。
*   **治理** — [曲线](https://curve.fi) ，一种去中心化的交易所(DEX)，利用赌注作为一种方式来协调流动性提供者和治理参与者之间的长期激励。CRV 持有者可以“投票锁定”他们的 CRV，以接收投票托管 CRV (veCRV)，他们锁定的时间越长，他们收到的 veCRV 就越多。投票锁定使持有人能够对治理提案进行投票，影响特定流动性池中获得的 CRV 收益率，并获得协议交易费的一部分。
*   **流动性准备**——分散流动性协议[Synthetix](https://synthetix.io/)将抵押作为一种为创建合成资产提供担保的方式，这些资产跟踪外部资产的价格，并由被抵押的 SNX 进行抵押。SNX 的利益相关者受到激励，通过通货膨胀的赌注奖励和通过使用 Synthetix 协议的 Kwenta 等 dApps 赚取的交易费的分配，为协议提供流动性。
*   **令牌分发** —诸如 [Alchemix](https://alchemix.fi/) 之类的 DeFi 协议采用赌注的方式向社区分发令牌，并在分散的生态系统中引导流动性。ALCX 令牌可以通过在赌注池合同中下注某些令牌来获得。

## 区块链 vs 甲骨文网络跑马圈地动态

与在区块链进行投资相比，在分散的甲骨文网络中进行投资旨在实现一个完全不同的目标。如 [Chainlink 2.0 白皮书](https://chain.link/whitepaper) 中所述，“区块链中的交易验证是内部一致性的属性，而区块链上的 oracle 报告的正确性是外部的属性，即链外数据。”要进一步了解区块链和甲骨文之间更深层次的细微差别，请查看这篇博文: [区块链和甲骨文:相似、不同和协同](https://blog.chain.link/blockchains-oracles-similarities-differences-synergies/) 。

本质上，区块链提供一种服务(即验证块),该服务遵循一组集体同意的预定义规则。因此，区块链使用一种桩设计来保护整个网络。或者，Chainlink 分散式 oracle networks 提供了广泛的不同服务(即提供外部数据、执行链外计算、实现跨链互操作性、向传统系统提供输出)，这些服务都可以通过多种方式进行定制，以满足用户自己的性能要求、预算和信任假设。因此，oracles 需要高度灵活的 staking 实现来适应用户验证外部数据和事件的多种方式。

在利益相关证明区块链中，利益相关机制用于激励对一组未决网络交易的有效性和批准达成诚实的共识。验证器的斜线条件可以包括但不限于:

*   **密码术** —一个验证器通过在相同的块高度生成并签名两个不同的块而自相矛盾(例如，双重签名块)。
*   **内部状态** —创建一个包含无效交易的块，这些交易花费了用户没有的资金(例如，重复花费交易)。
*   **网络内部规则** —验证器生成的块不符合协议规则(例如，铸造的硬币超过块奖励允许的数量)。

在分散式 oracle 网络(don)中，目标不是确保有效数据块的生产，而是确保创建可靠且防篡改的 oracle 报告，准确反映外部世界的状态。由于生成关于区块链之外的环境的真实情况的动态和不确定性的性质，对于所有用户，oracle 节点的删减条件可能不相同，并且可能无法仅通过加密或内部状态/规则来验证。相反，oracle 服务利用用户和 oracle 网络之间的链上服务级别协议(SLA ),该协议概述了削减条件、奖励/惩罚以及用于确定削减事件是否发生的验证技术。

![Similarities in blockchain and oracle networks](img/3a8b9e91c7bd382ec8dde49e6533e88c.png)

<figcaption id="caption-attachment-3358" class="wp-caption-text">Blockchains achieve consensus around validated blocks of transactions, while oracle networks achieve consensus on external data and off-chain computation.</figcaption>



由于 Chainlink 已经支持超过 800 个不同类型服务和区块链的 oracle 网络，正在积极开发中的 Chainlink explicit staking 模型必须涵盖非常广泛的可定制的苛刻条件、惩罚/奖励系统和验证技术，这些技术可以在各种区块链中自然运行。这就是为什么 Chainlink explicit staking 系统被设计为在考虑不同 Chainlink oracle 网络和服务之间的差异的同时，适当地激励正确的 oracle 节点操作员行为。

![Chainlink staking](img/71bbcf8de6f088c7f2137518352acd24.png)

<figcaption id="caption-attachment-3359" class="wp-caption-text">Chainlink staking combines implicit staking in the form of oracle node reputation systems and future fee opportunities, and explicit staking in the form of node deposits subject to slashing by the terms and conditions laid out in SLA smart contracts.</figcaption>



值得注意的是，区块链、DeFi applications 和 oracle networks 等公司的赌注机制都有一个共同的属性，即与帮助保护和促进所提供服务的赌注者分享用户费用。随着采用协议服务的增加，可以产生更大的费用池，并与利益相关者共享。

## 赌注的未来

赌注是智能合约生态系统中越来越受欢迎的加密经济模式，也与甲骨文网络直接相关。虽然最初的系统设计旨在为区块链带来安全性和经济可持续性，但 staking 已成为管理流动性和治理的 DeFi 协议中的一种宝贵机制，并将帮助 Chainlink oracle networks 获得额外的安全层。

要全面了解 staking 将如何帮助提升 Chainlink oracle networks 的安全性，请阅读[【Chainlink Staking:概述](https://blog.chain.link/explicit-staking-in-chainlink-2-0/) ，或观看 Chainlink 联合创始人 Sergey Nazarov 的演讲[chain link 的未来](https://www.youtube.com/watch?v=YShbzR7mlog) ，他在演讲中介绍了 chain link 的网络经济学基础知识。

[https://www.youtube.com/embed/YShbzR7mlog?feature=oembed](https://www.youtube.com/embed/YShbzR7mlog?feature=oembed)

*[今天检查您的资格](https://staking.chain.link/)为 Chainlink Staking v0.1 早期访问。*

*了解更多关于 Chainlink 的信息，请访问**[chain . link](https://chain.link/)，订阅 [Chainlink 简讯](https://chn.lk/newsletter) ，并在 Twitter 上关注[@ chain link](https://www.twitter.com/chainlink)。*

### 关于这个话题的更多信息

*   [chain link 2.0 中的显式定位:概述](https://blog.chain.link/explicit-staking-in-chainlink-2-0/)
*   [Chainlink 2.0:分布式 Oracle 网络发展的下一步](https://research.chain.link/whitepaper-v2.pdf)
*   [Chainlink 2.0 为采用混合智能合约奠定基础](https://blog.chain.link/chainlink-2-0-lays-foundation-for-adoption-of-hybrid-smart-contracts/)