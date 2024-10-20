# 链环 VRF:链上可验证的随机性

> 原文：<https://blog.chain.link/chainlink-vrf-on-chain-verifiable-randomness/>

我们很高兴地宣布 Chainlink VRF，它利用可验证的随机函数来产生可在链上验证的随机性。我们看到许多优秀的智能合约受益于 Chainlink VRF，特别是那些愿意提供证据证明他们确实在使用他们无法控制的防篡改随机来源的合约。

我们要感谢我们的学术合作者、为我们提供关于 VRF 链家的反馈的广大开发者社区，以及为实现这一初步实施付出努力的许多团队成员，谢谢你们。

Chainlink VRF 帮助支持和加速开发 [智能合约](https://chain.link/education/smart-contracts) 专注于区块链游戏、安全、二层协议和各种其他用例。开发人员可以通过我们最近发布的开发人员文档 ，轻松集成 Chainlink VRF，以在他们的智能合同中利用可验证的随机性。

## **对可验证随机性的需求**

创建智能合同并成功防御试图窃取该合同资金的对手，需要安全敏感的心态。使用随机性作为关键输入的智能合同开发人员也应该将对随机性的操纵视为一个关键风险。依赖于随机性的制作良好的系统理想地希望它对所有契约参与者都是可证明公平的/同样不确定的，同时还成功地降低了对手通过预测其结果来利用其契约的风险。

Chainlink VRF 试图通过提供其随机性以及可在线验证的加密证明来满足这两个要求，这表明随机性确实是不可预测的。由于 Chainlink VRF 随机性的链上可验证性质，参与节点只能拒绝请求，为此它们将使用 Chainlink 即将推出的打桩功能受到经济处罚，并可能从未来为其随机性付费的查询中删除。

使用 Chainlink VRF，您可以为任何需要不可预测结果的应用构建可靠的智能合同:

*   通过使用链上可验证的随机来源，使游戏更值得信赖，允许开发者向安全敏感的用户提供额外的证明。
*   通过生成具有挑战性和不可预测的场景和环境，以及分配不可预测的玩家奖励(如掉落战利品),让游戏更有趣。
*   产生可证明的职责和资源的随机分配，例如，将法官随机分配给案件，或者将审计员随机分配给被审查的公司。
*   选择一个有代表性的观察员样本，该样本有资格对合同需要建立共识的提案进行投票(调查是提供额外 sybil 阻力的有效方式)。

## **现有方法的安全限制**

为智能合约提供随机性的现有解决方案具有局限性，而 Chainlink VRF 的可验证随机性克服了这些局限性。使用现有的链上数据(如块哈希)和/或各种链外随机性(需要放在链上)都带来了独特的挑战。

希望依靠区块链实现随机性的智能合约开发人员应该设法避免的一个利用示例是过度依赖基于块散列的随机性保证。例如，假设一个契约基于某个高度的块的散列中最后一位的奇偶性来做出决策。这看起来像是 50/50 的结果，但是考虑到平均生产三分之一块的矿工(或矿工联盟)可能决定放弃块散列的最后一位为 1 的获胜块，放弃大约 2-3 ETH 的块奖励。在这种情况下，矿工可能将零结果从可靠的 50%可能性偏向 2/3 可能性，导致任何依赖这种随机生成方法的智能合同的用户资金损失。如果合同的零比特行为将使采矿者受益超过 12-18 ETH，这种行为将是经济上合理的，为使用这种方法的合同应该获得的价值创造了上限。

为了避免这样的问题，智能合约开发者已经转向了链外解决方案，即在链外生成一个随机数，然后在链上生成。然而，如果没有密码验证外链值是无偏的，结果就有可能被外链提供者和/或把随机值放在外链上的数据传输层操纵。类似地，应用程序的用户被迫假设随机性是公平产生的，并且已经被带到链上而没有在应用程序的途中被改变。

我们认为，考虑智能合约随机性来源的智能合约开发人员应设法避免的其他关键权衡和安全风险包括:

*   智能合同不可访问或不兼容
*   由随机数生成器的集中操作员操纵
*   一名区块链矿工作为该应用程序的用户之一进行剥削
*   应用程序最终用户不合理的高信任要求

为了帮助应对这些和其他不良的安全风险，VRF 链家提供了透明度和加密证明，证明每个结果都是公平生成的。

## **VRF 链环的工作原理**

![](img/9d67bdb413979fa9ad2e6b53153171ae.png)

<figcaption id="caption-attachment-425" class="wp-caption-text">How Chainlink VRF works</figcaption>



Chainlink VRF 的工作原理是将发出请求时仍未知的块数据与 [oracle](https://chain.link/education/blockchain-oracles) 节点预先提交的私钥相结合，生成一个随机数和一个加密证明。每个先知在产生随机性时都使用自己的密钥。当结果与证明一起在链上发布时，它在被发送到用户的合同之前在链上被验证。依赖于广泛接受的区块链的签名和证据验证能力，使得契约仅消耗随机性，这也已经被运行契约本身的相同链上环境所验证。

使用 Chainlink VRF 的最大好处是其可验证的随机性。即使节点受到危害，它也不能操纵和/或提供有偏见的答案——链上加密证明将失败。最糟糕的情况是，受损节点没有对请求做出响应，这将立即并永远在区块链上可见。用户将不再依赖停止响应和/或不提供具有有效证明的随机性的节点。即使在一个节点被破坏的不太可能的情况下，其产生的随机性也不能被操纵。受损害的节点只能拒绝请求，不作出响应，为此，它们将使用 Chainlink 即将推出的打桩功能受到经济处罚，并被从未来的查询中删除，这些查询将为它们的随机性付费，从而为低质量和/或行为不端的节点运营商造成巨大的即时和长期经济损失。简而言之，链环 VRF 不能操纵一个正确使用它的应用程序；在作为任何未来随机性的来源被移除之前，它只能离线或保留单个结果。这为智能合约开发人员及其用户创造了卓越的安全性。

Chainlink VRF 的另一个好处是，随着越来越多的用户使用它，支付给节点运营商的用户费用也会增加，从而促使节点运营商提供尽可能多的安全保障。随着时间的推移，用户可能会要求增加通过赌注实现的加密经济安全性，并通过支付越来越多的费用来证明其合理性。这导致了由用户付费支持的共享全球资源，并允许额外的用户花费资金来制作他们自己的 RNG 解决方案，以将这些相同的资金用于增加整个区块链生态系统的共享资源的集体安全性。Chainlink 支持各种链的能力，如 [波尔卡多](https://polkadot.network/chainlink-reaches-milestone-with-polkadot/) ， [Tezos](https://www.coindesk.com/tezos-blockchain-chainlink-oracle-services?utm_source=newsletters&utm_medium=blockchainbites&utm_campaign=&clid=00Q1I00000LxD77UAF) 和许多其他链，这意味着为该社区资源付费的用户群将在用户身份和逐渐增加的加密经济安全保证之间的网络效应中继续增长。

## **集成示例:PoolTogether**

以太坊上的无损储蓄游戏 [PoolTogether](https://pooltogether.us/) 是我们发现真正令人兴奋的东西，我们很高兴在他们的团队进行了广泛的技术研究后，他们将 [使用 Chainlink VRF 向他们的用户提供保证](https://medium.com/@lay2000lbs/dcf1a3d6ea) 关于他们的应用程序的可证明的公平随机性。

![](img/e2e369f24a28a83fe386ff54ea94b860.png)

<figcaption id="caption-attachment-482" class="wp-caption-text">How PoolTogther uses Chainlink Verifiable Random Function</figcaption>



PoolTogether 是一款不赔钱的储蓄游戏，它汇集用户的存款，并将赢得的利息分配给每天和每周抽奖中随机选出的赢家。

通过实施 Chainlink VRF 的可验证随机性，PoolTogether 用户将能够验证每个获奖者都是通过无偏见的随机性来源选出的。除了更加确定自身的安全性之外，PoolTogether 还将能够向其用户证明，其架构的一个关键部分正在以可证明的安全和可验证的随机方式运行，从而让用户有更大的理由相信，如果他们成为智能合同的参与者，PoolTogether 将实际上向他们提供支付。

# **技术演练**

Chainlink VRF 是本文 [中描述的戈德堡可验证随机函数(VRF)的实现。](https://eprint.iacr.org/2017/099.pdf) “可验证随机函数”中的“随机”是指“对任何不知道种子或密钥的人来说完全不可预测(均匀分布)”

VRF 密钥是甲骨文 [从{0，…，#secp256k1-1}上均匀分布的](https://github.com/smartcontractkit/chainlink/blob/master/core/store/models/vrfkey/private_key.go#L92) 中选择的一个数，以密码安全的方式。([secp 256k 1](https://en.bitcoin.it/wiki/Secp256k1)是以太坊的密码学使用的椭圆曲线。)与这个秘密密钥相关联的是一个公共密钥，它用于识别神谕。oracle [向链上机器注册公钥](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/VRFCoordinator.sol#L65) ，以及它将响应的 chainlink 作业 ID。

当一个消费契约使 [成为一个随机的](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/VRFConsumerBase.sol#L103) 请求时，它 [广播一个以太坊日志](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/VRFCoordinator.sol#L132) 从消费者请求中指定的 oracle 请求相应的 VRF 输出。在 [上看到这个日志](https://github.com/smartcontractkit/chainlink/blob/master/core/store/models/parse_randomness_request.go#L28) ，oracle 构造输出如下:

首先，它“ [将输入散列到曲线](https://github.com/smartcontractkit/chainlink/blob/master/core/services/vrf/vrf.go#L288) ，“从 secp256k1 获得一个密码安全的随机样本，使用不可预知的块数据和 oracle 的公钥作为输入。它通过使用 keccak256 对输入进行 [递归散列](https://github.com/smartcontractkit/chainlink/blob/c514d0b266f5021b732609958f350dfd14f1dffd/core/services/vrf/vrf.go#L162) ，直到输出小于 secp256k1 的基址字段的顺序(在那个 [secp256k1 描述](https://en.bitcoin.it/wiki/Secp256k1) 中为 *p* )，并且是 secp256k1 上某个点(x，y)的 x 坐标(即(x，y)则是曲线输入的散列。

然后它将 [乘以(x，y)，作为 secp256k1 曲线上的点](https://github.com/smartcontractkit/chainlink/blob/master/core/services/vrf/vrf.go#L292) 通过它的密钥获得一个点ɣ.作为 uint256，ɣ的 keccak256 散列是 VRF 输出。它证明了ɣ是(x，y)的倍数，就像甲骨文的公钥是 secp256k1 生成器的一样。这个证明与一个 [Schnorr 签名](https://en.wikipedia.org/wiki/Schnorr_signature) 非常相似:首先，它 [从{0，…，#secp256k1-1}中安全地采样一个 nonce](https://github.com/smartcontractkit/chainlink/blob/master/core/services/vrf/vrf.go#L328)，就像它对其密钥所做的一样，然后它计算=【T33 然后它计算出*v*=*n×*(x，y)。接下来，它 [将(x，y)、它的 VRF 公钥、ɣ、u 的地址和 v](https://github.com/smartcontractkit/chainlink/blob/master/core/services/vrf/vrf.go#L297) 一起散列，取该散列的余数模#secp256k1，并调用那个 *c.* 最后，它 [计算](https://github.com/smartcontractkit/chainlink/blob/master/core/services/vrf/vrf.go#L299) *[](https://github.com/smartcontractkit/chainlink/blob/master/core/services/vrf/vrf.go#L305)则是它的公钥，*c*，*s*，以及它的输入种子。它 [将此](https://github.com/smartcontractkit/chainlink/blob/master/core/adapters/random.go#L71) 发送回链上的 VRF 机器，后者 [验证凭证](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/VRFCoordinator.sol#L163) ， [将输出发送回消费契约](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/VRFCoordinator.sol#L172) ，假设凭证验证。*

为了检查证据，合同最好是

*   检查公钥和ɣ是有效的 secp256k1 点，
*   验证 [点的地址*c×PK*+*s×g*与*u*](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/VRF.sol#L464)(其中 *pk* 是
*   从公钥和种子中计算出“hash to curve”(x，y)，并 [检查出](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/VRF.sol#L474) 的 hash 为 *h，* 其公钥，的地址，[c×ɣ+](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/VRF.sol#L471)

要直观地了解为什么这是密码安全的，请参见 Jimmy Song 的著作 [*编程比特币*](https://programmingbitcoin.com/) 第 3 章“签名和验证”一节中的“箭头”类比。在我们的例子中，我们试图攻击的特殊“目标”是 *c.* 关于该方案安全性的完整证明，请参见附录 B[“使 NSEC5 在 DNSSEC 实用化”T19】](https://eprint.iacr.org/2017/099.pdf)

不幸的是，secp256k1 上的标量乘法像*c×*ɣ在 EVM 上直接计算是极其昂贵的，所以为了效率，我们使用 [Vitalik 的诡计](https://ethresear.ch/t/you-can-kinda-abuse-ecrecover-to-do-ecmul-in-secp256k1-today/2384) 到 [验证一个 *见证* 作为 c×ɣ传递到证明中，实际上与乘积 c×ɣ](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/VRF.sol#L245)相匹配这样，我们就把实际计算*c×*ɣ的负担推离了链，而只需要验证我们已经传递的值为*c×*ɣ实际上是*c×*ɣ，这样就便宜多了。

因此，除了上述输入/步骤，证据的链上验证涉及 c×ɣ和 s×(x，y)， 的 [见证，并且验证包括使用 Vitalik 的技巧检查这些见证是有效的 secp256k1 曲线点，并且与它们声称的产品相匹配。另外，我们使用以太坊地址为 *u* ，并使用 Vitalik 的诀窍检查其是否与点*c×PK+s×g*匹配。](https://github.com/smartcontractkit/chainlink/blob/master/core/services/vrf/solidity_proof.go#L22)

# **VRF 链环项目的发展计划**

Chainlink 即将采用 [阈值签名](https://blog.chain.link/threshold-signatures-in-chainlink/) 来实现 oracle 网络的高度可扩展和经济高效的去中心化，这也将为 Chainlink VRF 提供极致的去中心化和可用性。通过结合这两种方法，我们获得了 Chainlink VRF 提供链上可验证随机性的独特能力的所有优势，以及经济高效地拥有数千个节点以提供 Chainlink VRF 的正常运行时间/可用性的能力。

![](img/66107df31fa9d209ee1507d3d80b3de6.png)

<figcaption id="caption-attachment-485" class="wp-caption-text">A diagram showing the planned evolution of Chainlink VRF.</figcaption>



通过允许更广泛的 Chainlink 节点生态系统参与 Chainlink VRF 随机数生成，我们实现了一个节点运营商的全球分布式网络，这些运营商在经济上有动力在链上生成和广播可验证的随机数据。结合高度分散的节点运营商网络使用链式阈值签名将有助于防止对手窃取用户资金。不仅来自 VRF 链家的回复可以在网上验证；它们还将具有极端的正常运行时间/可用性，结合加密经济保证和 Chainlink 在各种区块链上的可用性，其中可验证的随机性将是有用的，可能会使 Chainlink VRF 成为智能合同如何消耗随机性的标准。

除了上面提到的好处，我们目前正在改进 Chainlink VRF，并继续进行关于产生分散随机性的前沿研究以及与其他 RNG 系统的合作。从我们最初的研究中，我们相信 VRF 链可以与 VDF 和其他方法相结合，产生随机，无论是链上还是链下。我们很高兴能与更大的区块链产业和更大的学术界合作，研究如何为智能合同提供尽可能最好的可证明公平的随机性来源。

# **试用 VRF 链环并给出反馈**

如果您是一名智能合约开发人员，并且想知道如何使用我们的 Chainlink VRF 的初始实现，请访问 testnet 上的 [开发人员文档](https://docs.chain.link/docs/chainlink-vrf) 以与它集成，并加入关于 [不和谐](https://discordapp.com/invite/aSK4zew) 的技术讨论。

我们对 Chainlink VRF 公司的安全审查已进入最后阶段，我们希望与开发者社区和学术界的用户合作。

如果制定和支持解决现实世界问题的安全可靠的智能合同听起来很有趣，我们目前正在增加额外的核心团队成员！更多信息请访问我们的 [招聘页面](https://careers.chain.link/) 。

如果您想了解更多关于 Chainlink 的信息，请访问 [Chainlink 网站](https://chain.link/) 或关注我们的[Twitter](https://twitter.com/chainlink)或[Reddit](https://www.reddit.com/r/Chainlink/)。