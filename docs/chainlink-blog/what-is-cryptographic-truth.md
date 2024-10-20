# 加密真相:信任最小化计算和记录保存的未来

> 原文：<https://blog.chain.link/what-is-cryptographic-truth/>

这是关于信任的未来的两部分系列的第二部分。阅读第 1 部分， [什么是真正的加密](https://blog.chain.link/what-crypto-is-really-about/) ，深入探究区块链、智能契约和甲骨文构建来解决的社会问题。T9】

虽然基于区块链的技术有许多不同于其他计算模式的特质，但它们的主要价值主张是生成加密真理。从最简单的意义上来说， **加密真相是一种后端计算和记录保存的形式，它比当前的替代方案更加准确、可访问、可审计和防篡改。**

密码真理源自 *信任最小化* 基础设施— 代码，它完全按照预期工作，因为它的执行和验证不依赖于对陌生人或不可控变量的信任 。 [区块链](https://blog.chain.link/what-is-blockchain/) 使用加密技术生成信任最小化，以认证数据和保护记录的时间顺序，并分散共识以验证新条目并保持其不变。通过这种机制，多方流程可以在共享的、可信的中立后端上被跟踪和执行，该后端被激励诚实地管理。

![Cryptographic Truth](img/42a401c9790ca67f50f94ca8eccc3ad9.png)

<figcaption id="caption-attachment-3474" class="wp-caption-text">Cryptographic truth combines cryptography and decentralized consensus to generate a golden record amongst a distributed set of entities and deterministically compute applications.</figcaption>



在讨论 oracles 如何将加密真理扩展到区块链上不可用的任何类型的事件或计算的验证之前，下面的文章将考察加密和分散共识如何在区块链结合产生加密真理。

### 目录

*   *[在区块链了解密码学及其使用](#understanding_cryptography_and_its_use_in_blockchains)* 
    *   [*密码学介绍*](#introduction_to_cryptography)
    *   *[现代密码学](#modern_cryptography)* 
        *   [*哈希函数*](#hash_functions)
        *   [*对称加密*](#symmetric_encryption)
        *   [*不对称加密*](#asymmetric_encryption)
*   *[区块链密码术](#cryptography_in_blockchains)* 
    *   [*交易认证和验证*](#transaction_authentication_and_verification)
    *   [*阻滞生产，西比尔抵抗，以及终结*](#block_production_sybil_resistance_and_finality)
    *   [*数据存储*](#data_storage)
    *   [*区块链使用的其他密码技术*](#other_cryptographic_techniques_used_in_blockchains)
*   *[真理从分散的共识中产生](#truth_generated_from_decentralized_consensus)* 
    *   [*游戏结构*](#game_structure)
    *   [*游戏激励*](#game_incentives)
    *   [*游戏结果*](#game_outcome)
*   [*chain link 如何利用密码真理构建全球真理机器*](#how_chainlink_leverages_cryptographic_truth_to_build_a_global_truth_machine)
*   [*一个由密码真相驱动的世界*](#a_world_powered_by_cryptographic_truth)

## 了解加密技术及其在区块链的应用

为了全面理解加密真理及其在区块链的作用，首先熟悉现代密码学的术语和一般工作方式是很重要的。 **注:** 如果你已经了解密码学，可以随意跳到下一小节 [*区块链的密码学*](https://blog.chain.link/what-is-cryptographic-truth/#cryptography-in-blockchains) 。

### 密码学简介

[密码学](https://www.kaspersky.com/resource-center/definitions/what-is-cryptography) 是在敌对行为存在的情况下安全通信的科学。虽然大多数人理解加密在保持通信机密性方面的作用(例如加密的消息应用程序)，但它也用于验证来源、验证完整性和建立通信的不可否认性；即用于确定消息来自特定的人并且没有被篡改，并且这些属性不能被发送者否认。

密码术用于将原始信息转换成只有知道内情的人才能解读的难以理解的信息。 [*加密*](https://usa.kaspersky.com/resource-center/definitions/encryption) 是一种 *双向功能* 即 *加密* 原始消息(即 *明文* )成一条不知所云的消息(即 *密文) 【T31)其他加密函数是单向的，只寻求证明一些关于数据的知识或属性，而不是使原始数据可知。*

一种加密算法被称为 *密码* 而 *密钥* 是一个秘密——通常是一串字符——允许某人理解密码。密码中使用的技术有两种基本类型:替换和置换(也称为传输)。 *替换密码* 用其他字母、数字或符号替换明文字母、数字和符号。 *排列密码* 使用明文消息字母但重新排列它们的顺序。这些技术经常被组合、分层，受外部数据的影响，并随着时间的推移而改变，从而产生复杂性。

![Substitution and permutation ciphers](img/4bf70f5ab31cfc9372853decf56d1026.png)

<figcaption id="caption-attachment-3475" class="wp-caption-text">The two basic encryption techniques utilized by ciphers are substitution and permutation (also called transportation).</figcaption>



第一批加密算法是基于硬件的，这意味着它们是记忆的、手写的或者通过非数字机器实现的。然而，随着计算机的出现，基于软件的加密算法成为主要的加密形式。

### 现代密码学

现代密码学在很大程度上基于 *计算难度假设*——特定问题无法有效解决的观念。因此，尽管理论上大多数加密函数都有可能被破解，但鉴于当前的计算限制，在实践中破解它们是不切实际的。因此，现代密码算法寻求在计算效率和计算安全之间取得正确的平衡，依靠数学和计算机科学来做出关于密钥长度等因素的决定。这就是为什么许多密码函数是基于现代计算系统寻找难以解决的数学问题的解决方案所花费的时间和预算，例如 [离散对数问题](https://www.mccurley.org/papers/dlog.pdf)[整数因式分解问题](https://crypto.stanford.edu/cs359c/17sp/projects/JacquelineSpeiser.pdf) ，以及 [椭圆曲线](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.400.7990&rep=rep1&type=pdf) 中的理论问题。

现代的、基于软件的密码学有三大类: *哈希函数* ， *对称加密* ，以及 *非对称加密* 。

#### 哈希函数

[哈希函数](https://www.tutorialspoint.com/cryptography/cryptography_hash_functions.htm) 将任意长度的数据转换成固定位长称为 *哈希* 。哈希是数据的唯一标识符，类似于指纹，本质上是验证原始数据集。散列数据通常用于索引数据，并以高效的方式从数据库中检索数据。它还用于安全地存储数据，例如在网站中只存储用户密码的 *加盐* 散列，以防止在数据库被破坏时密码泄露。

哈希函数不使用密钥，并且基于 *单向函数* 以确保它们是 *抗预镜像的*——对于不知道原始消息的人来说，仅从哈希中就能猜出它几乎是不可能的。获得原始消息的唯一现实方法是通过 *蛮力*；即猜测每一个可能的输入，在散列的情况下，这是可能的字符组合的无限集合。哈希算法通常也被设计成抗——两个不同的输入几乎不可能生成相同的哈希。这些属性使得更改输入中的任何内容，比如字母的大写或添加标点符号，都会导致完全不同且看似随机的散列输出。

当今最流行的安全哈希算法是[](https://www.movable-type.co.uk/scripts/sha256.html)，它生成长度为 256 位的字符串(即 256 个连续的 1 和 0)。256 位哈希通常以十六进制字符串格式表示，因此它们的长度可能是 32 或 64 个字符。SHA-256 存在于 SHA-2 散列函数集内，取代了现在被密码破解的 SHA-1。SHA-3 也是在 2015 年基于加密原语 Keccak 推出的。

![Hashing in blockchains](img/8ba1139c2fc1d0e70b4fee888a71de1f.png)

<figcaption id="caption-attachment-3477" class="wp-caption-text">Changing one character in the hash, such as adding the comma in the second input, will completely change the output and appear totally random to observers.</figcaption>



#### 对称加密

[对称加密](https://www.thesslstore.com/blog/symmetric-encryption-101-definition-how-it-works-when-its-used/) (又名秘钥加密) 涉及一个发送方和接收方都用来加密和解密消息的通用 *秘钥* 。对称加密快速而高效，但也带来了在互联网上以安全的方式共享密钥的挑战。虽然共享可以亲自完成，但这不是一种全球可扩展的方法，因为它需要与每个交易对手建立正式关系。另一个问题是，一旦秘密密钥被泄露，任何使用它的人都有被解密的危险。这就是为什么许多使用对称加密的互联网协议，如 TLS，也利用 *密钥交换协议* 来安全地建立共享密钥，而无需通过互联网发送它。

最流行的对称加密密码是 [高级加密系统](https://cybernews.com/resources/what-is-aes-encryption/) (AES)。AES 提供长度为 128、192 和 256 位的密钥，这是对以前和现在不安全的 [数据加密标准](https://www.tutorialspoint.com/cryptography/data_encryption_standard.htm)【DES】标准中使用的 56 位密钥的重大升级。就上下文而言，一个 56 位密钥有 2 个 56 个 、 或 72 万亿个可能的密钥，可以在 [下 24 小时](https://www.cnet.com/personal-finance/crypto/record-set-in-cracking-56-bit-crypto/) 被蛮力破解。或者，AES 中最短的密钥长度将花费 [万亿万亿年](https://www.eetimes.com/how-secure-is-aes-against-brute-force-attacks/#) 来尝试所有 2 个 <sup>128 个</sup> 可能的密钥，甚至当组合世界上所有的计算机时。

![Symmetric Encryption](img/cc2a7a06e6f601af8e17fe182210da10.png)

<figcaption id="caption-attachment-3470" class="wp-caption-text">Symmetric encryption uses the same secret key to encrypt and decrypt messages.</figcaption>



#### 不对称加密

[非对称加密](https://cheapsslsecurity.com/blog/what-is-asymmetric-encryption-understand-with-simple-examples/) (又名公钥密码) 给每个用户一个公钥和私钥对。 *公钥* 对所有人可见，而 *私钥* 只有所有者知道。用户可以用他们的私钥加密消息，任何人用公钥都可以解密。这就是所谓的 [*数字签名*](https://www.docusign.com/how-it-works/electronic-signature/digital-signature/digital-signature-faq) ，因为它证明知道一个秘密而不泄露该秘密(即用户拥有公钥地址的私钥)。用户也可以用别人的公钥加密消息，只有拥有私钥的人才能解密(即发送机密信息)。

最流行的非对称加密算法是 RSA(以其发明者 Ramis、Shamir 和 Adleman 命名)、ECC(椭圆曲线加密)、Diffie Hellman(流行密钥交换协议)和 DSS(数字签名标准)。一些非对称加密算法是抗量子的，而另一些则不是，将来可能不得不升级或放弃。

![Asymmetric encryption](img/753fcd18a20974b3027b86bbfc685a3d.png)

<figcaption id="caption-attachment-3471" class="wp-caption-text">Asymmetric encryption requires each user to have a public/private key pair.</figcaption>



### 区块链的密码学

区块链利用了两种主要的加密形式:公钥加密和散列函数。然而，其他加密技术正越来越多地被用于为区块链带来扩展、隐私和外部连接解决方案。以下是区块链使用加密函数的一些方式。

#### 交易认证和验证

区块链上的每个用户必须有一个 *公/私钥对* 和 *区块链地址* ，以便在网络上提交交易。私钥用于生成公钥，公钥用于生成 [*区块链地址*](https://blockgeeks.com/guides/blockchain-address-101/)——一般是公钥的散列，最后 20 个字节添加到前缀，如 *0x* 。注意，许多 *区块链钱包* 和传统交易所抽象掉了公钥/私钥对的生成和用户与之的交互。

[https://www.youtube.com/embed/u6yzP4wF0so?feature=oembed](https://www.youtube.com/embed/u6yzP4wF0so?feature=oembed)

区块链地址类似于与用户银行账户相关的真实姓名(例如，按订单付款……)，只是在区块链，它是一串伪匿名的数字和字母。区块链地址是用户存储资金和部署 [智能合约](https://chain.link/education/smart-contracts) 的地方。私钥类似于 pin 码，用户必须输入它才能对其帐户采取行动，如转移资金和更改智能合同。公钥类似于用户的银行账号，用于验证他们的私钥签名。

当提交交易时，用户从他们的区块链地址向网络发送包含交易数据和数字签名的消息。交易数据描述了用户想要在网络上采取的动作，而数字签名验证了该动作。数字签名由两个输入生成:用户交易数据的散列和他们的私钥。然后将数字签名附在交易数据上，形成数字签名交易。

*挖掘者/验证者* 和 *全节点—* 谁管理区块链—运行数字签名验证协议来验证交易的有效性。验证协议将获取原始交易数据并对其进行哈希处理。它还将使用用户的公钥解密数字签名，以获得散列值。如果两个哈希值相同，则交易被视为有效。通过结合散列法和公钥加密来支持数字签名， **区块链确保只有私钥持有者才能访问存储在相应区块链地址的资金。**

![Blockchain transaction authentication and verification](img/6144084e23458f5327e273382ada96d3.png)

<figcaption id="caption-attachment-3476" class="wp-caption-text">Blockchains use digital signatures to authenticate and verify user transactions.</figcaption>



#### 区块生产，西比尔阻力，和终结

*分块生产* 是挖掘者/验证者将待处理事务捆绑成称为 *分块* 的数据结构并在网络上提出的过程。块通常由包含在块中的所有事务的列表和包含来自块的元数据的块头组成。为了产生一个块，挖掘器/验证器需要生成一个有效的 *块散列* ，否则该块将被拒绝。

[*工作证明*](https://en.bitcoin.it/wiki/Proof_of_work)*(PoW)*区块链(例如比特币)主持矿工之间的公开比赛，其中首先通过蛮力生成有效散列(即以至少一定数量的零开始的散列)的人被选中，以向分类帐提议他们的块。PoW 区块链在块生产中使用散列函数来确保 *抗 Sybil*——防止单个实体通过欺骗替代身份来控制块生产过程。由于散列能力是 PoW miner 增加其成为块作者的机会的唯一方式，获得对更多网络散列能力的控制伴随着以执行更多计算的形式的成比例的财务成本。这不仅可以防止拒绝服务攻击，还要求矿工付出“努力”才能获得获得奖励的机会。

[*股权证明*](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/)*(PoS)*类似以太坊(后合并)的区块链也在块生产中生成散列，但是该过程被故意设计为容易，因为在验证器之间没有竞争。相反，PoS 验证者通常通过随机选择作为块作者，通常基于他们的利害关系。PoS 区块链通过要求验证者存放加密货币(即股份)来参与批量生产，从而产生 Sybil 阻力。因此，PoS 验证者必须投入财政资源来增加他们被选为批量作者的机会。通常，如果他们违反某些协议规则，如在其区块中包括无效交易或在相同高度签署两个区块，他们的股份会受到 *削减* (即没收)。

通常，有效的块散列必须具有以下输入:

*   **Merkle root**—Merkle 树数据结构中包含的块中所有包含的事务的散列。
*   **Nonce**—任意数字/字母组合，产生满足当前难度目标的有效散列。PoW 区块链周期性地调整猜测随机数的难度，以针对特定频率的块(例如，每十分钟)，而 PoS 网络使得随机数相对容易生成。
*   **附加区块元数据**—这在区块链各不相同，但可能包括以下一些:区块链的当前软件版本、时间戳、开采难度目标、整个链的州根或当前区块号。
*   **先前块散列**—来自先前验证的块的有效块散列。

![Blockchain blocks](img/6ea1142bed3ed6d69ad2c41067b189d6.png)

<figcaption id="caption-attachment-3472" class="wp-caption-text">Blocks consist of transaction data, the Merkle root, other block metadata, a valid nonce, and a hash of the previous block.</figcaption>



块包括前一个块的块哈希值到 **用密码将它们链接在一起形成一个链** ，保持分类账的时间顺序。这就是为什么区块链被称为是不可变的，因为它需要大量的计算能力和/或财务风险来撤销先前验证的块，称为 [块重组](https://learnmeabitcoin.com/technical/chain-reorganisation) 或简称为 *重组* 。即使一个数据块中只有一个事务被更改，该数据块的整个哈希也会发生变化，从而很容易被其他节点发现。注意，并不是所有的重组都是恶意的；即，由于异步网络条件，链末端的 1-block 重组更常见。然而，深度重组可能更具争议性，而且发生的时间越往后，成功重组的难度就越大。

在 PoW 区块链中，挖掘者必须为所有被替换的块重新生成有效散列以执行重组攻击，在此期间，其他挖掘者花费计算资源将新块附加到最近的块。这就是[Nakamoto consensus](https://bitcoinmagazine.com/guides/what-is-nakamoto-consensus-bitcoin)逻辑“工作量最大的最长链是有效链”发挥作用的地方，因为它为矿工提供了一种直接的方式来确定总帐的有效版本。

这个逻辑就是为什么说战俘区块链有 *概率性终局性* 的原因，越往后企图更改，攻击就越不可能成功。从概率终结性而来的是 *51%攻击* 的概念——矿工需要 51%或更多的散列能力来完成更深层次的重组攻击或审查其他矿工的区块。概率终结性也是为什么集中式加密货币交易所通常只批准用户在包括他们的交易的块之上已经挖掘出一定数量的后续块时花费他们的存款(例如，通常比特币中 6 个块，以太坊中 32 个块)。这有助于防止 *重复消费攻击—* 当同一货币单位被多次欺诈性消费 。

在 PoS 网络中，当前不产生块的所有或一部分验证器通常被赋予通过投票机制证明新块的有效性的任务。试图执行重组的验证者将不得不将他们的经济利益置于风险之中，随着攻击越深，违背分散共识(通常是验证者的 2/3)的惩罚将增加。PoS 的这种广义模型为共识算法带来了密码经济属性，如 [【实用拜占庭容错】](https://www.geeksforgeeks.org/practical-byzantine-fault-tolerancepbft/)[Tendermint](https://tendermint.com/)[Casper](https://arxiv.org/pdf/1710.09437.pdf)，以及[hotstuf](https://arxiv.org/abs/1803.05069)。

一些 PoS 区块链还对区块链分类账可以更改多远有限制，本质上是建立一个 *检查点* ，在此之前的每笔交易都有 *显式终结* 。例如，PoS [信标链](https://ethereum.org/en/upgrades/beacon-chain/) 的*合并* 到当前以太坊网络中会将块生产和验证分割成 *时期* ，每个时期具有 32 个槽，每个槽的长度为 12 秒。在每个时期，所有验证器被随机分成至少 128 人的委员会规模，验证器围绕每个时期混合。在每个时间段，验证者提出一个区块，来自一个或多个委员会的验证者证明该区块。这样设计是为了让验证器证明每个时期有一个建议的块。

![Ethereum epoch](img/1f251e4e65c056cb4d7d383ecc409fef.png)

<figcaption id="caption-attachment-3469" class="wp-caption-text">Ethereum block production and verification post Merge will be split into epochs with 32 slots, where a block can be proposed and attested to every slot. [Source](https://ethos.dev/beacon-chain/).</figcaption>



在每个时期结束时，如果至少三分之二的所有验证者证明其有效性(即绝对多数)，则前一时期内的块被认为是合理的。如果两个先前的历元在一行中对齐，则前一个历元成为最终的。给定理想的网络条件和验证程序的参与，事务的终结平均需要 14 分钟左右。一旦一个时代最终确定，协议的规则防止它在没有外部社会共识的情况下被恢复。

#### 数据存储

区块链是一个分类账，按时间顺序包含了区块链网络上曾经发生过的每一笔交易(虽然有些区块链在探索 [修剪历史数据](https://eips.ethereum.org/EIPS/eip-4444) 经过某个检查点)。区块链运行的时间越长，分类账就越大，节点存储和同步的成本就越高。过多的存储和带宽要求增加了运行一个完整节点的硬件要求，从而使区块链网络的分散化面临风险，有可能允许一小组实体破坏网络。

为了以高效安全的方式对分类账数据进行编码，区块链使用了名为*Merkle trees*的数据结构。在 Merkle 树中，每个用户事务被散列，然后与另一个散列事务配对并再次散列。散列被不断地配对并在树上散列，直到所有散列只有一个散列，称为 *Merkle 根。*T9】

比特币使用 Merkle 树进行基于 *未用交易输出(UTXO)模型* 的交易，而以太坊使用 Merkle 树进行交易、状态和收据(例如日志和事件)，在所谓的 *账户模型* 中具有通用智能合约支持。

![Blockchain hashing in Merkle trees](img/5e4cc1ede45003fabb9fdd777abed984.png)

<figcaption id="caption-attachment-3478" class="wp-caption-text">Merkle trees are an efficient way to store transaction data in blockchains.</figcaption>



Merkle 树非常有用，因为与其他数据结构相比，Merkle 树占用的磁盘空间更少，并且有助于有效验证分类帐中的数据完整性和数据包含性。此外，因为 Merkle 根包含在块头中，所以它们允许连接到可信完整节点的 *轻型客户端* 快速且安全地验证特定事务包含在块中，而无需下载整个区块链。

#### 区块链使用的其他加密技术

区块链中使用的其他一些密码原语包括:

*   [**零知识证明**](https://blog.chain.link/what-is-a-zero-knowledge-proof-zkp/)**(ZKPs)**—用户( *【证明者】* )向另一方( *验证者* )证明他们拥有关于某条特定信息的知识而不暴露实际底层信息的方法。例如，在 Zcash 区块链上，完全节点可以在不知道 发送方、接收方或者交易金额 的情况下证明交易有效。
*   **可信执行环境(TEEs)**—使用可信硬件，如英特尔 SGX，来执行机密计算，其中计算的完整性可以通过 [密码证明](https://www.intel.com/content/www/us/en/developer/tools/software-guard-extensions/attestation-services.html) 来证明。这方面的一个例子是 Oasis，这是一个区块链，其中所有验证器节点都利用可信执行环境来提供智能契约的机密和可验证的执行。
*   **门限签名方案(TSS)**—一种分布式密钥生成和签名的形式，用于通过单个加密签名来认证由分散式网络执行的计算，该签名只需要一组门限参与者签名。例如，15 个节点中只有 10 个需要签名的事务被认为是有效的。

## 分散共识产生的真理

*博弈论* 是一种基于数学的策略方法，关注于预测特定竞争中理性行动者的行动。在博弈论中， *机制设计* 是在战略互动中利用激励手段达到预期结果的艺术。

区块链利用机制设计来激励理性、自利节点的分散网络，以维护准确、不变、始终可用、抗审查的账本。这种期望的结果有时被总结为实现——区块链网络中的大多数节点诚实地参与，使得用户能够始终如一地信任网络共识。

让我们看看区块链是如何通过诚实的多数结果来实现真理的。

### 游戏结构

区块链是由开源软件驱动的透明分类账，这意味着所有参与者都可以查看分类账的整个历史，并验证代码是如何运行的。区块链网络参与者被分成五个一般组:

**用户** 在网络上进行交易，或者是出于个人原因，或者是为了托管应用程序。在无许可的区块链，任何人都可以在任何时候向网络提交交易。

挖掘者/验证者 通过从用户交易中产生新的块来扩展分类账。一些区块链允许任何人成为挖掘者/验证者，而其他区块链限制了有限数量或允许的参与者集合。一些人通过允许用户投票或将股份委托给验证者来抵消这种限制。

**全节点** 在区块链网络上有几种功能。首先，完整节点提供 RPC 端点，使用户能够读取和写入区块链。RPC 端点可以通过自托管节点实现，也可以通过第三方提供商(例如 Infura)实现。当向区块链写入数据(即提交事务)时，完整节点要么将它们中继到公共内存池，要么将它们保存在私有事务池中。这是因为在对等分散网络中没有单一的事务池，而是每个完整的节点都有自己的事务池。

在将用户事务转发到网络之前，或者在网络上传播其他节点的事务之前，完整节点还检查用户事务的有效性。此外，完整节点验证由挖掘器/验证器提出的新块，作为自我验证区块链分类账的一种方式。如果他们认为该块是有效的，他们将把它附加到他们的分类账的副本。如果他们不认为这是有效的，他们将拒绝阻止，不更新他们的分类帐。全节点的分散网络中的共识代表分类帐的当前 *状态*——所有区块链地址、它们的余额、部署的智能合同和相关存储的顶点。任何人都可以运行一个完整的节点，尽管不同网络的硬件要求不同。挖掘器/验证器通常作为完整节点参与。

![Blockchain full nodes, miners, and validators](img/d5d9c54a75cac9493edf50f00b0d5d85.png)

<figcaption id="caption-attachment-3473" class="wp-caption-text">Blockchains separate the roles of miners/validators and full nodes for increased security on the network.</figcaption>



**服务提供商** 是向区块链提供服务或基于区块链的内容创建服务的外部实体。这包括[Oracle](https://chain.link/education/blockchain-oracles)、索引协议、集中式交换、轻客户端、归档节点、块浏览器等等。这些实体通常具有需要与区块链交互的业务模型。例如，集中式交换提供加密货币和传统金融系统之间的上/下斜坡，轻型客户端允许用户验证从完整节点发送的信息，而不需要完整的分类账副本，oracles 为智能合约应用程序提供关键的外部资源。

MEV 机器人 是寻求在区块生产期间影响交易顺序的实体，尤其是矿工和 MEV 开发商。 [*矿工可提取价值(MEV*](https://blog.chain.link/what-is-miner-extractable-value-mev/)*)*，也称为 *最大可提取价值* ，是基于矿工/验证者选择块中包含哪些交易以及这些交易如何排序的能力。然后他们就可以利用这种特权来榨取自己的利益，比如通过或者 *的夹层攻击* 的用户，并利用清算和套利机会获利。MEV 机器人通常通过私有事务池和链外块空间拍卖来运行，尽管它们可能独立运行。

### 游戏激励

激励分为两大类:隐性激励和显性激励。 *显性激励* 是对在游戏中采取的行动的直接奖励或惩罚，例如对访问服务的强制支付或对违反协议规则的硬编码罚款。 *隐性激励* 是源于游戏的间接奖励和惩罚，比如参与者失去了未来的收入机会或者在没有保证报酬的情况下花费了劳动力。

区块链最明显的激励措施是支付给生产批准区块的采矿者/验证者的 *区块奖励* 和 *交易费* 。块奖励通常在数量上是标准化的，而交易费可以根据当前对有限块空间的需求而上下浮动。在批量生产过程中，也存在以特定方式订购交易的动机，MEV 机器人试图利用这种动机来获取财务收益。

区块链还通过 PoW 和 PoS 等抗 Sybil 机制利用经济处罚；即，挖掘者/验证者需要提交计算或财务股份，以获得赚取奖励的机会，如果他们违背网络共识，则可能会浪费或削减奖励。要求区块生产商承诺计算或财务股份的另一个好处是，它激励了去中心化。特别是因为挖掘器/验证器获得对网络散列能力或赌注的更多控制变得越来越昂贵。

区块链也用本国的加密货币向矿工/验钞机付款。这为挖掘者/验证者诚实地参与网络创造了隐含的激励，因为安全可靠的网络可能会吸引更多的用户。更多的用户导致更多的交易费用，以及他们赚取的加密货币的潜在更高价格。更高的加密价格意味着更高的单位收入和个人持有量的增加。

![Implicit staking Bitcoin](img/c34eaa0731bc620809d6378a48e1251f.png)

<figcaption id="caption-attachment-3479" class="wp-caption-text">Bitcoin has a form of implicit staking where miners are rewarded in an asset (BTC) that only remains valuable and covers their expenses if they uphold the security of the network.</figcaption>



虽然协议中通常没有直接内置运行完整节点的明确激励，但有许多隐含的激励来这样做。首先，网络运行需要完整的节点，因此矿工至少需要运行它们。用户、应用程序和服务提供商也需要运行或访问完整的节点，以便提交和验证未决事务的状态。因此，有几种免费的节点即服务模式来支持生态系统。

除了财务激励之外，完整的节点对分类账的完整性至关重要，因为缺乏分散化将使较小的参与者群体控制网络。受损的分类帐将会影响服务提供商和分散式应用程序，这些应用程序的业务模式完全依赖于区块链的诚实多数假设。

分散的全节点网络也有助于将块生成与块验证分开，通过降低挖掘者/验证者任意改变协议规则的能力来保持他们的责任。此外，运行自己的完整节点的实体经历最大程度的审查阻力和安全保证，因为它们不需要信任任何第三方来读取或写入区块链。这些隐性激励结合起来，鼓励用户和关键经济行为体运行全节点。

### 游戏结果

在既定的游戏结构中引入这些激励措施，导致了区块链的预期结果:

*   **准确性—** 区块链的去中心化，隐含/显性成本的风险，以及检测无效交易的容易性，激励了挖掘者/验证者和完整节点就有效性交易达成诚实的共识。
*   **不变性—** 试图改变先前批准的区块的财务成本和风险使得这样做在很大程度上是不可取的，尤其是当更多的区块在目标区块之上被生产时。
*   **可用性—** 充足的奖励有助于确保挖掘者/验证者不断地生成块，同时大量的价值受到威胁，这激励了扩展到挖掘者/验证者之外的全节点网络。
*   **抵制审查—** 抵制西比尔的机制、经济奖励和未经许可参与的能力，使得任何中央集权实体试图审查交易的成本都高得令人难以置信，尤其是在很长一段时间内。

有了这些期望的属性，用户与区块链网络互动的动机就更强了。不仅使用率会上升，而且用户会乐于在区块链上存储更高的价值，并在智能合约应用程序中使用他们的链上资产。

然而，应该注意的是，虽然区块链通常是抗审查和准确的，但由于 MEV 的原因，不能保证交易在发送时间或支付费用方面的排序。这就是 Chainlink 开发[【FSS】](https://blog.chain.link/chainlink-fair-sequencing-services-enabling-a-provably-fair-defi-ecosystem/)公平排序服务的原因——这是一种 oracle 服务，用于根据收到交易的时间对区块链、第二层网络和应用进行分散排序。

还应该说，区块链最终都是由人类运行的系统，为人类服务，所以如果每个人都达成一个(即参与者之间的链外协议) 的社会共识，认为区块链需要改变，那么就可以做到。推动变革的社会共识最明显的例子是以太坊 *硬分叉*——一种向后不兼容的软件更新——恢复了 2016 年 DAO 黑客窃取的资金。社会共识也可能反过来发生，社区参与者阻止部署提议的更改，如拒绝比特币网络的 Segwit2x 和以太坊网络的 ProgPoW。

也就是说，区块链可以说是最有效的网络，可以防止不受欢迎的攻击和违背绝大多数社会共识的改变，特别是通过加密和经济机制。

## Chainlink 如何利用加密真相构建全球真相机器

到目前为止，本文的重点是区块链如何将密码学和博弈论结合起来，在内部交易的有效性方面始终如一地形成诚实的共识——事实。然而，如何能可靠地证实发生在区块链之外的事件呢？输入[](https://chain.link)。

Chainlink 是一个 *的分散式 oracle 网络* 旨在生成关于外部数据和链外计算的真相。从这个意义上说，Chainlink 从很大程度上的非确定性环境中产生真理。 *确定性* 是计算的一个特性，其中特定的输入将总是导致特定的输出，即代码将完全按照编写的那样执行。分散式区块链之所以被称为确定性的，是因为它们采用了信任最小化技术，这种技术消除了任何可能抑制内部事务提交、执行和验证的变量，或者将这些变量降低到几乎统计上不可能的程度。

非确定性环境的挑战在于，真相可能是主观的、难以获得的，或者验证起来非常昂贵。比如比特币的价格是多少？答案是，比特币没有统一的价格，因为它在不同的交易所有所不同，而每个交易所都处于不断变化的状态。此外，是否所有用户都同意他们愿意为真相支付的价格，以及特定方法在获取真相时提供的确定性程度？例如，由众多高性能物联网设备组成的网络将获得比单个低质量传感器更准确的天气读数，但安装和运行成本也将更高。这些情况凸显了一个现实，即产生外部真相的方法以及人们愿意为此支付的成本将因人而异，因公司而异。

由于区块链只在所有用户和应用程序之间保留一个单一的真相来源，Chainlink 是关键的基础设施，因为它让用户能够创建自己的 ***最终真相***——一种预定义的生成真相的方法，参与各方都同意这种方法对于解决他们的协议是权威的。此外，使用区块链的加密保证和确定性计算，可以验证用于生成确定性真理的 oracle 机制，并强制其条款。

![Cryptographic truth for digital agreements](img/82ffc43044f0b9376d2062c4dc37571d.png)

<figcaption id="caption-attachment-3468" class="wp-caption-text">By combining definitive truth with cryptographic guarantees, decentralized oracle networks can securely, reliably, and accurately perform off-chain services and prove they are in alignment with user-defined parameters.</figcaption>



从这个意义上来说，最终真相是一种用户定义的共识机制，用于将自己锚定在区块链上的分散式 oracle 网络，以一种更加信任最小化的方式运行。用户可以定义的一些共识参数包括 oracle 网络的基础设施、使用的特定数据源、执行的精确计算、获得的奖励/惩罚，以及 oracle 网络如何向区块链证明其工作的完整性。和 w 虽然这些参数可以定制以满足各种预算、性能要求和信任假设，但行业标准也将扎根，整个市场或大部分市场都同意将这些标准作为共享的真理来源。

在信任最小化方面，Chainlink 使用了许多与区块链相同的方法，例如:

*   **密码术**—每个 Chainlink oracle 节点在每个支持的区块链上都有一个公钥/私钥地址。节点使用这些密钥为它们执行的所有计算生成数字签名，签名经过验证并存储在区块链上。加密签名不仅证明了谁提供了数据以及他们的计算是什么，而且有助于支持跟踪节点链上性能的信誉系统，例如它们的历史正常运行时间和准确性。oracle nodes 和 oracle networks 的签名数据也可用于触发奖惩的发布。
*   **去中心化共识** —Chainlink 在数据源、oracle 节点和 oracle 网络级别利用去中心化来减少数据来源、交付和计算中的任何故障点和控制。这使得用户能够从他们需要并愿意付费的任意数量的特定源和节点聚集数据，以便高度确定地证明外部事件或链外计算的有效性。
*   **财务激励** —Chainlink 节点因提供甲骨文服务而以用户付费的形式获得报酬。此外，作为未来[加密经济赌注模式](https://blog.chain.link/explicit-staking-in-chainlink-2-0/)的一部分，链接令牌可以作为抵押品来进一步激励诚实的甲骨文服务。在节点表现不佳或恶意行为的情况下，例如扣压数据/计算、不按时交付数据或提供偏离 DON 总体中值一定百分比的数据，被标桩的链接抵押品可能会受到削减。

最终结果是一个信任度最小化的框架，用于根据任何用户定义的参数执行链外计算，并将结果和签名一起传送到区块链进行验证。这些新的 [混合“链上/链下”应用](https://blog.chain.link/hybrid-smart-contracts-explained/) 极大地扩展了区块链的价值主张，因为它们允许链上智能合约代码对来自外部环境的数据和计算做出反应并直接产生影响，例如数据提供商、web APIs、物联网网络、其他区块链、遗留后端、支付系统或任何类型的外部资源。

![Chainlink Network](img/5f4b2c9554ef2397f1ca6191a4ea274c.png)

<figcaption id="caption-attachment-3480" class="wp-caption-text">Chainlink can provide an end-to-end framework for hybrid smart contracts powered by cryptographic truth.</figcaption>



例如， [Chainlink 价格馈送](https://data.chain.link/) 是分散的 oracle 网络，其使用 [多层聚合](https://blog.chain.link/levels-of-data-aggregation-in-chainlink-price-feeds/) 架构来生成关于实时资产价格和金融市场信息的加密真相的行业标准。

使用 Chainlink 价格馈送，数据由专业数据聚合公司进行聚合，这些公司从数百家交易所的原始数据中生成数量加权平均价格(VWAPs)。然后，每个 Chainlink 节点从多个数据聚合器获取一个 VWAP，并取一个中值。最后，每个 Chainlink 节点的中值进一步聚合成一个中值，以创建一个存储在区块链上的可信值。任何人都可以通过链上数据验证每个节点和整个 oracle 网络提交的值。

传统和 [分散金融](https://chain.link/education/defi) 应用程序使用这些价格来执行关键操作，例如发放和清算贷款、结算衍生品合约以及设定汇率。

![Chainlink Price Feeds are cryptographic truth for asset prices](img/b8d013f6d891e5a78dad3aece993c00d.png)

<figcaption id="caption-attachment-3467" class="wp-caption-text">Chainlink Price Feeds generate cryptographic truth for the real-time prices of financial assets.</figcaption>



## 一个由密码真理驱动的世界

最终，加密真理为计算和记录保存带来了确定性、准确性和透明性。通过了解应用程序代码将按预期执行，并且历史记录已经过冗余验证并将保持防篡改，社会和经济关系可以建立在比以往更深层次的事实基础上。有了坚实的真理基础，就会增加经济活动，加强社会和谐——一个每个人都希望看到实现的世界。这就是为什么我们所有人都有责任构建和采用区块链和甲骨文技术，在我们集体社会的核心支柱之间建立加密真理。

如果你喜欢这篇文章，我们鼓励你阅读 [关于](https://blog.chain.link/what-crypto-is-really-about/) 什么是真正的加密，这是一篇研究我们现有的经济和社会系统对加密真相的需求的博客文章。

如果您想更多地了解区块链和甲骨文技术，我们鼓励您查看 [Chainlink 博客](https://blog.chain.link/) 上不断增长的教育材料列表。

要了解更多关于 Chainlink 的信息，请访问[chain . link](https://chain.link/)，订阅 [Chainlink 简讯](https://chn.lk/newsletter) ，并关注 Chainlink 上的[Twitter](https://twitter.com/chainlink)，[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)，以及[Reddit](https://www.reddit.com/r/Chainlink/)