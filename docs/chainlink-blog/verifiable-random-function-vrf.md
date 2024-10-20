# 可验证随机函数(VRF)

> 原文：<https://blog.chain.link/verifiable-random-function-vrf/>

在密码学中，一个可验证的随机函数(VRF)是一个随机数生成器(RNG ),它生成一个可以被密码验证为随机的输出。可验证的随机性对于许多区块链应用程序来说是必不可少的，因为它的防篡改不可预测性使得令人兴奋的游戏、罕见的[](https://chain.link/education/nfts)、以及无偏见的结果成为可能。

在本文中，我们研究什么是可验证随机函数，探索随机性在区块链中是如何使用的，并看看聪明的合同开发者如何使用 [Chainlink 可验证随机函数(VRF)](https://chain.link/solutions/chainlink-vrf) 在他们自己的 dApps 中利用安全的随机性来源。

## 什么是可验证的随机函数(VRF)？

可验证的随机函数是一种加密函数，它接受一系列输入，对它们进行计算，并产生伪随机输出，以及任何人都可以验证的真实性证明。

VRF 的输入通常包括公钥/私钥对(也称为验证密钥和秘密密钥)和种子。创建公钥/私钥对并选择种子。这些值被传递到 VRF，在那里私钥和种子被用来生成一个随机数。然后 VRF 输出一个随机数和一个证明。重要的是，证明的生成使得函数可验证，而隐藏私钥确保了数字不可预测。

顾名思义，可验证随机函数由其核心特征定义:

*   **可验证**—任何人都可以验证 VRF 生成的随机数是有效的。他们所需要做的就是检查证据并验证散列输出的正确性。虽然只有 VRF 秘钥的持有者才能计算散列，但任何有公钥的人都可以验证散列的正确性。
*   **随机**—对于任何不知道种子或私钥并且不遵循任何模式的人来说，VRF 的输出是完全不可预测的(均匀分布的)。在 VRF 中，每一种可能的产出都是同样可能的。通过以独特的方式组合种子和私钥来产生随机性。
*   **函数**—vrf 依靠数学算法来产生随机数和验证其真实性的证据。对于被认为是 VRF 的函数，RNG 必须保持种子隐藏(隐式)以保持其不可预测性，而证明必须是显式的并且每个人都可以计算(显式)以确保其可验证性。

### VRF 历史

可验证随机函数的概念是由著名的计算机科学家和数学家希尔维奥·米卡利、迈克尔·拉宾和萨里尔·瓦德汉在 1999 年发表的一篇论文[](https://dash.harvard.edu/bitstream/handle/1/5028196/Vadhan_VerifRandomFunction.pdf)中引入的。值得注意的是，希尔维奥·米卡利接着推出了阿尔格兰德区块链，在其共识机制中使用了 VRF。

从那以后，vrf 的发展取得了许多重大突破。2005 年，Yevgeniy Dodis 和 Aleksandr Yampolskiy 对这项技术进行了改进，他们利用了一种防冲突散列函数，缩短了证明和密钥，从而提高了效率。然后在 2015 年，Dennis Hofheinz 和 Tibor Jager 使用椭圆曲线加密技术创建了一个可证明安全的 VRF。并且在 2019 年，Nir Bitansky 表明，vrf 可以用一般的基元来构造，而不是简单的代数构造。如今，许多 VRF 实施都依赖于这些创新。

有趣的是，在 2020 年，研究人员提出了一种使用基于晶格的加密技术的 VRF，它足够安全，可以抵御来自量子计算机的攻击，这表明 VRF 在未来很长一段时间内仍然是一项重要的技术。

### VRF 用例

大多数 RNG 不产生可以用密码验证的随机数，这使得它们容易被操纵，从而限制了它们的使用情况。通过保证随机数的安全性，VRFs 开启了许多重要的用例，例如:

*   **互联网安全** —VRF 用于帮助保护域名系统(DNS)信息的安全。
*   **零知识技术**——VRF 用于零知识证明和零知识数据库的协议设计。
*   **非交互式彩票系统**——VRF 为彩票提供了可证明的公平和高效的结果。
*   **可验证的交易托管方案** —VRF 可以帮助支持自动托管服务，保护用户匿名。
*   **区块链和智能合约**——VRF 已经成为去中心化协议和应用的重要组成部分。

## 区块链中的 VRF

许多一级区块链，包括 Algorand、Cardano、Internet Computer 和 Polkadot，在他们的共识机制中使用 VRF 来随机选择区块生产商。

在区块链技术生态系统的其他地方，智能合约开发者也需要他们的应用程序有一个随机性来源。然而，由于区块链网络的确定性，链上应用程序无法访问安全 RNG。使用链上块哈希作为随机性的来源可能会导致区块链矿工/验证者的操纵，他们丢弃具有不利哈希的块，并可以“重新掷骰子”，改变 RNG 值。幼稚的外链解决方案是不透明的，无法证明产生的 RNG 值是合法的，并且没有被数据源或 oracle 节点操纵。

![Image showing how miners and validators can exploit RNGs.](img/0cd414c1edc8fa23ff9416529c250df0.png)

<figcaption id="caption-attachment-3901" class="wp-caption-text">Blockchain miners/validators can exploit blockchain-based RNG solutions.</figcaption>



依赖于随机性的设计良好的系统在理想情况下会希望它对所有合同参与者都是可证明的公平和同样不确定的，并且还会降低对手通过预测其结果来利用合同的风险。

### 链型 VRF

[Chainlink VRF](https://chain.link/solutions/chainlink-vrf) 是一个满足这些要求的可证明公平且可验证的 RNG，它为智能合约提供了一个安全的随机性来源，该来源由加密证明支持，不能被 oracle 节点、用户或开发团队操纵。

[https://www.youtube.com/embed/eRzLNfn4LGc?feature=oembed](https://www.youtube.com/embed/eRzLNfn4LGc?feature=oembed)

VRF 链家为开发商提供了一系列优惠，包括:

*   **不可预测性** —Chainlink VRF 是不可预测的:没有人能够预测随机性以增加他们成功的几率，因为在发出请求时块数据是未知的。
*   **公平** —Chainlink VRF 是公平和公正的，因为随机数基于均匀分布，这意味着该范围内的所有数字都有平等的机会被选中。
*   **随机性**—VRF 链可证明是随机的，因为它依赖于事先未知的块散列作为内置于 VRF 节点中的 RNG 的种子。
*   **防篡改**—VRF 链家是防篡改的，因为没有人——无论是甲骨文、外部实体还是开发团队——能够篡改 RNG 流程。

Chainlink VRF 作为用户和区块链之间的抽象层，使智能合约开发者能够访问安全的随机性来源，并在他们的应用程序中使用。

![Image showing how Chainlink VRF reduces risks to users.](img/32fb99190ca9fd2a10929711e187dbfa.png)

<figcaption id="caption-attachment-3900" class="wp-caption-text">Chainlink VRF uses open-source code and cryptography to create a tamper-proof source of randomness that users can verify as fair and unbiased.</figcaption>



Chainlink VRF 是本文[](https://eprint.iacr.org/2017/099.pdf)中描述的戈德堡可验证随机函数(VRF)的实现。对于每个随机性请求，Chainlink VRF 会生成一个或多个随机值，以及这些值是如何确定的加密证明。在任何消费应用程序可以使用它之前，证据在链上被发布和验证。

### Chainlink VRF 用例

在整个 Web3 生态系统中，包括在领先的 GameFi、DeFi 和 NFT 项目中，Chainlink VRF 被用作链上随机性的安全来源。

链环[T3】VRF 用例 T5包括:](https://blog.chain.link/blockchain-rng-use-cases-enabled-by-chainlink-vrf/)

*   **将随机属性分配给 NFT**—VRF 链环可以在铸造过程中帮助创建独特的 NFT。[Axie Infinity](https://axieinfinity.com/)使用 VRF 链为每个原点 Axie 提供一组随机的特征。
*   **公平分配稀有的非森林交易**——VRF 链家提供了可审计的证据，证明非森林交易是公平分配的。 [【百无聊赖】猿游艇俱乐部(BAYC)](https://boredapeyachtclub.com/#/) 利用 VRF chain link 向目前 BAYC NFT 持有者随机发放其新的突变血清 NFTs。
*   **不可预测的游戏结果**——开发者可以通过利用随机结果来构建更有趣的区块链游戏。例如，[block mine](http://chainlinkecosystem.com/ecosystem/blockmine/)在其下一个卡牌游戏中使用 Chainlink VRF 支持随机抽奖。
*   **公平选择参与者**—分发独家活动门票等令人垂涎的物品，选择奢侈品预售获奖者，并选择受欢迎的公开销售的参与者。例如， [Centaur](https://medium.com/centaur/chainlink-vrf-used-by-centaur-to-deploy-new-standard-for-enhanced-transparency-in-public-sale-3cc0fa5b10e6) 使用 Chainlink VRF 来选择其在线公开销售的参与者。
*   **随机选择获奖者**——通过 VRF 链家，用户将能够验证每个获奖者都是通过公正的随机来源选出的。例如，[【pool together】](https://pooltogether.us/)是一款无损失储蓄游戏，它将用户存款汇集在一起，并在每日和每周的抽奖中将赢得的利息分配给随机选择的赢家。

![Image showing how PoolTogether uses Chainlink VRF.](img/7a9f9873b78b25c5afff670b6004dd48.png)

<figcaption id="caption-attachment-3899" class="wp-caption-text">PoolTogether uses Chainlink VRF to help randomly choose winners in its no-loss savings game.</figcaption>



## 结论

在区块链领域，Chainlink VRF 是行业领先的安全随机数生成器(RNG)，使智能合约和非链系统能够访问可验证的防篡改随机源。

提供一个既安全又可验证的随机性来源，使开发人员能够构建比当前替代方案更加开放、可访问和防篡改的系统。最终，Chainlink VRF 和智能合约有助于实现区块链的愿景，即让社会远离基于信任的薄弱系统，转向建立在 [【加密真理】](https://blog.chain.link/what-is-cryptographic-truth/) 基础上的更强大的基于数学的系统。

如果你是一名开发人员，想要快速将你的应用程序连接到 [【链接 VRF](https://chain.link/solutions/chainlink-vrf) ，请访问 [开发人员文档](https://docs.chain.link/docs/chainlink-vrf/) ，并加入关于 [不和谐](https://discordapp.com/invite/aSK4zew) 的技术讨论。如果您想安排一次电话会议来更深入地讨论整合事宜，请点击 [这里的](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=announcement) 。

## 附加资源

*   [什么是智能合约？T3】](https://chain.link/education/smart-contracts)
*   [什么是区块链甲骨文？T3】](https://chain.link/education/blockchain-oracles)
*   [【随机数生成(RNG)】中](https://blog.chain.link/random-number-generation-solidity/)
*   [如何在一个 NFT 中得到随机数(ERC721)](https://blog.chain.link/random-numbers-nft-erc721/)