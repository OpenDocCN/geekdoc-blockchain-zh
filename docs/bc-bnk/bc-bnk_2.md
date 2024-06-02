© 作者 即独家许可 Springer Nature Switzerland AG 2021P. Martino 区块链与银行[`doi.org/10.1007/978-3-030-70970-9_2`](https://doi.org/10.1007/978-3-030-70970-9_2)

# 2. 区块链技术：关键特征和主要应用

Pierluigi Martino^(1  )(1)皮萨大学经济与管理系 意大利皮尔鲁奇·马蒂诺电子邮件：pierluigi.martino@unipi.it

## 摘要

本章提供了区块链技术基础的一般概述以及其工作原理。目标是让人清楚地了解为什么这项技术被认为具有颠覆性。特别是，本章讨论了区块链技术的关键特征以及其各种类型和类别；还突出了它们的不同特点、优势和风险。此外，它探讨了区块链的两个主要应用，即加密货币和智能合约。

关键词 区块链 分布式账本技术 加密货币 智能合约

## 2.1 介绍

许多学者和金融从业者一致认为，区块链是一项颠覆性技术，是未来金融市场创新的关键来源，并且可能颠覆我们的社会和新世界经济。自从它作为比特币底层技术并用于记录加密货币交易以来，区块链已成为一项可以方便记录任何交易类型并跟踪任何资产流动的技术。它的应用广泛且涉及不同领域。

本章提供了区块链技术基础的一般概述以及其工作原理。目标是让人清楚地了解为什么这项技术被认为具有颠覆性。特别是，本章讨论了区块链技术的关键特征以及其各种类型和类别；还突出了它们的不同特点、优势和风险。此外，它探讨了区块链的两个主要应用，即加密货币和智能合约。

## 2.2 区块链技术的基础

区块链是一个不断更新的数字、去中心化和分布式分类账。这项技术使得在给定网络中记录交易和跟踪资产成为可能（Swan 2015; Crosby 等 2016; Walport 2016）。“区块链”这个词源于交易被分组成“区块”（作为数据包），这些区块与前面的区块相连，形成一个按时间顺序排列的“链”。“区块链”提供了交易的底层路径，因此代表了交易历史的完整分类账（Holotiuk 等 2017; Nofer 等 2017）。然而，与传统分类账不同，区块链结合了多种计算机技术，包括数字分类账、分布式数据存储、点对点传输、共识机制和加密算法（Guo 和 Liang 2016; Holotiuk 等 2017; Lewis 等 2017），在成本、速度和数据完整性方面提供了潜在的优势。特别是，可以确定一些潜在的基础特征，这些特征构成了区块链并使其成为一项颠覆性技术（Bohme 等 2015; Iansiti 和 Lakhani 2017; Tapscott 和 Tapscott 2017; Zheng 等 2017; Martino 等 2019）。

首先，区块链是网络参与者的“分布式分类账”，所有参与者都有权访问它。“分布式”意味着每个参与者都可以共享分类账，在每次交易发生时更新，并同时访问查看信息^(1)（Natarajan 等 2017）。因此，在区块链中透明度得到保证，因为所有参与者在网络上存储了完整的交易历史，并对任何有权访问系统的人可见（Fanning 和 Centers 2016; Iansiti 和 Lakhani 2017）。同时，它也是“去中心化”的，因为没有个体节点能够完全控制整个网络（Iansiti 和 Lakhani 2017; Tapscott 和 Tapscott 2017）。因此，不需要中央机构，因为分类账的控制权归所有网络参与者。区块链中的去中心化存储也通过消除单点故障确保了高强度，这在中心化系统中很典型（Fanning 和 Centers 2016）。实际上，如果任何一个节点出现故障，其他节点将继续运行，从而保持系统的可用性。

其次，区块链采用“点对点技术”，允许用户在没有中央权威或控制点的情况下连接（Iansiti 和 Lakhani 2017; Tapscott 和 Tapscott 2017）。这使得分散式交易处理成为可能，也就是说，每个人都可以直接向给定网络中的任何其他人发送东西，从而消除了需要中央权威来验证信任和转移价值的需求。

第三，如上所述，在区块链中，交易被分组到链接到其前身的区块中，这种区块的时间链提供了底层交易的迹象。这些区块通过哈希函数在链中被“加密密封”，哈希函数是一种将字母和数字输入转换为固定长度的加密输出（即 “哈希”）的密码系统，无法反转以恢复原始输入（Narayanan et al. 2016; Yermack 2017）。具体来说，如图 2.1 所示，除了交易信息之外，每个区块还包含前一区块（父区块）的 *哈希值*^(2)（即唯一标识数据的固定长度的数字值），记录了特定区块链分类帐项目在特定时间段内的时间存在，以及 *nonce* ，这是一个用于验证哈希的随机数字（Nomura Research Institute [NRI] 2016; Nofer et al. 2017; Zheng et al. 2018).![../images/490216_1_En_2_Chapter/490216_1_En_2_Fig1_HTML.png](img/490216_1_En_2_Fig1_HTML.png)

图 2.1

区块链示例

因此，区块被“链接”在一起：每个区块的头部包括反映前一个区块内容的哈希函数，而前一个区块本身包括源自其前身的哈希函数，如此循环——一直回溯到链中的第一个区块（Yermack 2017）。此外，区块的交易会通过 *Merkle 树根* 进行哈希计算，即区块链网络中包含的所有交易的哈希的哈希的哈希……这意味着区块链上信息的完整性和安全性是通过加密功能来确保的；这保证了记录的不可逆转性，因此具有高鲁棒性和高信任度，因为不可能删除或编辑这些区块（Iansiti and Lakhani 2017; Tapscott and Tapscott 2017; Adhami et al. 2018）。

区块链还利用“非对称加密”机制（即公钥加密）来验证交易的身份验证。这有助于用户保护其数字资产，并通过使用加密和解密的不同密钥来增强用户安全性：一个用于私人使用—即*私钥*—而另一个对任何人可用—即*公钥*（NRI 2016; Zheng et al. 2018）。公钥代表个人的账户地址，可被任何人看到，而私钥限制对账户所有权的访问权限提供私钥/账户持有者。^(3) 私钥—和公钥对允许人们加密将要发送的信息，因此使接收者能够确定消息是否源自正确的人，并且是否有任何篡改（Peters and Panayi 2016）。因此，信息的发送和接收可以安全进行，因为仅仅凭公钥就几乎不可能推导出私钥。此外，当账户持有人授权交易时，通过数学算法创建了一个“数字签名”。此签名将用户的私钥与他们想要转移的数据结合起来，并用于证明正在发送的数据的真实性。通过使用发送者的私钥加密要发送的数据的哈希值，将其与发送者的公钥解密发送者的数字签名获得的哈希值进行交叉检查，从而确认数字签名的真实性（NRI 2016; Drescher 2017）。

最后，区块链的另一个关键特征是它是“基于共识”的，也就是说，只有在网络中所有参与者同意的情况下才能记录一笔交易（Lewis 等人 2017）。 Swanson（2015）将共识机制定义为网络验证者大多数（或在某些情况下全部）同意账本状态的过程。根据他的说法，“这是一组规则和程序，它允许在多个参与节点之间保持一致的事实集”。这意味着当网络中的大多数节点通过共识机制就一个块中的交易的有效性以及块本身的有效性达成一致意见时，新的块才能被添加到链上^(4)（Nofer 等人 2017）。一旦验证，新的块就被添加到区块链中，实质上更新了分布在网络中的交易账本。因此，在这个系统中，每笔交易都只在经过验证确保交易有效性后记录在账本上，因此，区块链是一种确保透明度和信任的机制（Buitenhek 2016；Crosby 等人 2016）。

区块链中有几种达成共识的方法，每种方法都有不同的优势和劣势。第一种最流行的区块链共识机制是工作量证明（PoW），它被用于比特币网络。在 PoW 系统中，网络参与者必须在允许将新的“区块”添加到区块链之前解决一个复杂的数学问题。他们必须使用随机数（一次性号码）计算变化的块头的哈希值，直到他们获得一个等于或小于特定目标的值^(5)（Zheng 等 2018）。当相关值被实现时，网络参与者应相互确认该值的正确性；如果大多数参与者同意，新的块被认为是有效的并被添加到现有链中。制作有效 PoW 的矿工可能会获得加密货币作为奖励（例如以交易费的形式），这作为维护系统完整性的经济激励（Natarajan 等人 2017）。应当指出，由于随着解决了更多的区块，挖矿难度不断增加，因此 PoW 机制需要大量的计算资源，这带来高昂的电力成本，因而对矿工来说成本也很高（Houben 和 Snyers 2018）。

第二种最广为人知且最常用的共识机制是权益证明（PoS），它是工作量证明（PoW）的节能替代品，其中矿工必须证明拥有一定数量的货币所有权（在加密货币的情况下）才能参与交易验证（6）（Houben 和 Snyers 2018；Zheng 等人 2018）。而 PoW 依赖于“计算能力”来挖掘区块，PoS 则依赖于节点在系统中的“股份”——通常是用户持有的货币数量。这意味着交易验证者必须证明他们的“股份”（即他们所拥有的所有货币的份额）之后才能被允许验证一笔交易。因此，用户的股份越高，他们对验证的权威性就越大，因为他们在网络中的地位更高，这赢得了他们更受信任的地位（Natarajan 等人 2017；Houben 和 Snyers2018）。权益证明的演进是委托权益证明（DPoS），在 DPoS 中，矿工验证区块的能力依赖于他们的股份，但与 PoS 不同的是，利益相关者（根据他们的持股）选举一组被委托的见证人来生成和验证区块（Li 等人 2017；Zheng 等人 2018）。

### 2.2.1 区块链技术：优势和劣势

区块链技术被认为是传统的基于经典复式记账法的金融分类帐的替代品（Yermack 2017）。特别是，区块链背后的分布式分类帐技术代表了对历来由公司用于支持交易处理的中心化数据存储库的一种突破。

传统上，用于记录交易的数据库是中心化系统。这种系统昂贵、重复努力、需要长时间，并且存在许多问题，特别是关于信任——即需要第三方验证（MacDonald 等人 2016）。共享数据库的参与者必须相信一个控制主要副本的中央权威，以保持记录的准确性并维护防止设备故障或网络攻击导致数据丢失的技术基础设施。因此，中心化系统也容易受攻击，因为中央权威代表一个单点故障（Lewis 等人 2017）；这意味着如果中央权威的技术基础设施受到损害，数据库将丢失，这将影响整个商业网络。

通过结合数种计算机技术，如数字分类账、分布式数据存储、点对点传输、共识机制和加密算法，区块链可以解决传统数据库（即集中式系统）的问题，无需第三方即可快速、低成本和安全地进行交易（Buitenhek 2016；Yermack 2017）。特别是，文献已指出区块链技术的以下优势（Iansiti and Lakhani 2017；Natarajan et al. 2017；Tapscott and Tapscott 2017；Zheng et al. 2018；Martino et al. 2019）：

+   *去中心化*和*非居间化*。区块链实现了去中心化的交易处理和记录保存，从而使任何人都能直接进行交易和达成协议，无需中央机构或中间人来验证信任并转移价值。这可能导致较低的交易成本。

+   *更大的透明度*。由于区块链上的完整交易历史由网络上所有参与者存储，并且任何拥有系统访问权限的人都可以查看（所有网络参与者都拥有分布式分类账的完整副本，从而完全访问查看信息），区块链确保更大的透明度，因此可以减少欺诈行为。

+   *自动化*。通过自动化组织的业务流程的部分，例如通过执行智能合约（见第 2.4.2 节）中的内容，区块链可以显着提高许多组织领域的效率，例如通过减少组织在这些流程上花费的时间和精力（因此降低成本），以及提高其质量、准确性和速度。

+   *不可变性*。由于区块链上的信息受到密码证明的保护（Yermack 2017），意味着一旦交易输入到数据库中并更新账户，记录就无法更改，因为它们与之前的每个交易记录相关联，区块链可以提供不可变和可验证的任何资产类型的交易审计路径。

+   *更好的网络安全弹性*。由于其分布式性质消除了单一攻击或故障点（Nofer et al. 2017），区块链可能提供比传统集中式数据库更具弹性的系统，并且更好地防范各种类型的网络攻击。

尽管技术仍在不断发展，许多技术和监管问题尚未解决。特别是，区块链面临以下风险和挑战（Barber et al. 2012；Natarajan et al. 2017；Zheng et al. 2018；Martino et al. 2019)^(7)：

+   *可扩展性*。与传统系统相比，区块链（尤其是公共区块链）在交易数量和验证速度方面面临可扩展性问题。例如，比特币运行的公共区块链仅能每秒处理四至七次交易，因为区块大小受限于 1 兆字节，而传统银行系统今天每秒执行数千次操作。

+   *安全问题*。虽然人们普遍认为区块链是安全的，但由于技术的缺陷（或者例如智能合约的脆弱性）可能存在潜在风险，这可能导致盗窃和网络攻击，就像过去几年发生的几起事件所展示的那样^(8)（例如，攻击去中心化自治组织 The DAO，黑客窃取了 DAO 资产的三分之一，价值约 5000 万美元）（Niranjanamurthy 等人，2018）。

+   *隐私*。在公共区块链中，所有网络参与者都可以访问交易信息，这带来了隐私问题。例如，正如 De Filippi（2016）所指出的那样，区块链的透明性“使得任何人都可以检索在区块链上执行的所有交易历史，并依靠大数据分析来检索潜在的敏感信息”。

+   *环境问题*。当使用 PoW 作为共识机制时，由于挖矿需要大量的计算处理能力以及频繁的硬件更新需求，区块链可能会产生潜在的环境问题，并导致高昂的电力成本。

## 2.3 区块链的类型和分类

根据账本的性质，区块链可分为三类，即*公共*、*私有*和*混合*区块链，每种区块链在共识确定、读取权限和去中心化程度等方面都具有自己的特点（Peters 和 Panayi，2016）；Natarajan 等人，2017；Zheng 等人，2018；Martino 等人，2019）。

公共（也称为*无许可*）区块链是完全分散的，没有单一所有者。此外，无需中央实体的批准即可加入网络。因此，任何网络参与者都可以访问区块链中的信息，并进行交易，以及参与共识过程。比特币和以太坊是公共区块链的最著名示例。

在两个极端（公共和私有区块链）之间，结合了两种模型的第三种分类是混合（或*联合*）区块链，其中共识过程由预选节点集控制（Peters and Panayi 2016）。具体而言，网络的一部分具有公共特性（即对任何参与者可访问），但只有特权群体负责共识过程。因此，它们在一定程度上是分散的，因为区块链仅在合格参与者之间分布。

区块链技术的进一步分类取决于其发展和应用的发展。区块链的第一个应用是作为验证虚拟货币比特币所有权的方法。然而，虽然区块链技术通常与数字或虚拟货币方案和支付相关联，但其范围要广得多：今天，区块链的分布式分类账技术可以促进任何交易类型的记录，并可以跟踪任何资产的动向，无论是有形、无形还是数字的，并且可以应用于多个领域（Tapscott 和 Tapscott 2017）。根据其进化和应用的发展，可以确定区块链技术的不同类别：*区块链 1.0*、*区块链 2.0* 和 *区块链 3.0*（Swan 2015；Gatteschi 等人 2018；Martino 等人 2019）。

区块链 1.0 是货币。它代表了这项技术的第一个应用，即加密货币的开发（例如比特币），与现金和数字支付系统有关。具体来说，它是比特币运行的技术，允许记录比特币和其他加密货币的交易。相反，区块链 2.0 涉及货币和简单支付以外的广泛经济和金融应用（Efanov 和 Roschin 2018）。根据 Swann（2015）的说法，虽然区块链 1.0 是为了货币和支付的去中心化，区块链 2.0 则是为了更普遍的市场去中心化，并考虑使用区块链转移除货币以外的其他各种资产。这些领域的应用包括传统银行工具，如贷款和抵押贷款，以及股票、债券、期货和衍生品等复杂金融市场工具，以及像所有权证书、合同和其他可货币化的资产和财产等法律工具。

区块链 2.0 特别与智能合约的发展相关联（Gatteschi 等人 2018），即在区块链上编写并在满足特定条件时自动执行的程序。它们使得不同类型的应用程序得以运行，特别是在金融领域。最著名的区块链 2.0 示例是以太坊，这是一个开源的区块链平台，允许开发者编写智能合约和去中心化应用程序（Dapps）。这些 Dapps 以分布式方式在网络上运行，参与者的信息得到安全保护，操作执行在网络节点上的分散化^(9)（Swan 2015）。

最后，区块链 3.0 指的是超越货币、金融和市场的广泛应用，但有潜力涵盖政府、医疗保健、艺术和教育等各个领域（Swan 2015; Crosby 等人 2016; Natarajan 等人 2017; Gatteschi 等人 2018）。随着区块链生态系统的成熟，其应用案例继续远远超出金融应用范围。在过去几年里，许多不同行业和原因的区块链解决方案已经涌现，从防范欺诈和增加透明度，到降低交易成本/费用和对手方风险。

## 2.4 区块链应用

正如上一节所示，区块链可以应用于各个领域。本节将重点介绍区块链技术的两个主要应用，即*加密货币*和*智能合约*，并将突出它们的特点和应用案例。

### 2.4.1 ***加密货币***

货币在历史上发生了很大的变化——从物物交换到使用硬币和纸币，最近又发展到数字支付——这些改变得益于科技的进步，其中一些科技现在使无现金交易比以往任何时候都更加容易（OECD 2002; UBS 2018）。随着电子支付的出现，全球许多行业都已经摆脱了现金交易，使得无现金交易（即数字货币交换方式，如新的移动支付、信用/借记卡）在全球经济中变得更加普遍，尤其是在新兴经济体中（Capgemini 2019）。根据 Capgemini 最新的《世界支付报告》（2019），全球非现金交易量在 2016 年至 2017 年间增长了 12%，达到了 5390 亿次，而新兴市场则引领了这一增长潮流。

这种转变可能会在全球经济方面带来多方面的益处，如提高效率、减少逃税等。然而，新技术的出现同时也带来了与欺诈、洗钱、恐怖主义融资和网络犯罪相关的新问题，这些问题必须得到解决。比特币和其他加密货币的出现加剧了这一讨论，因为它们有潜力颠覆现有的支付和货币系统（Bohme 等人 2015）。

加密货币是区块链技术的先驱应用，是设计成以密码学而非银行或其他可信的第三方（政府或其他中央权威）来保障金融交易、控制额外单位的创造和验证资产转移的数字金融资产（数字货币）（Yermack 2013; European Payment Council 2019; Giudici et al. 2020)。^(10) 它们使用去中心化控制而非中央化的数字货币和央行系统（Bohme et al. 2015; Richter et al. 2015; Jacobs 2018）。特别是，与需要中央信任方（例如中央银行）来保证国家货币和交易价值的传统法定货币相反，加密货币依赖区块链技术在互联网上创建分布式的支付系统以确保支付交易的认证和完整性，因此无需中央权威（Adhami et al. 2018）。

比特币是第一个也是最著名的加密货币。2008 年，一个名为 Satoshi Nakamoto 的个人或开发者团队起草了一份白皮书，提出了创建一个点对点的电子现金系统（即比特币）的构想，目的是允许在线支付直接从一方发送到另一方，无需通过金融机构（Nakamoto 2008）。其思想是基于加密证明而非信任来建立电子支付系统，使任何人能够直接向另一方交易和转移价值，无需像银行这样的可信第三方，从而解决了在进行支付时需要第三方的问题。^(11)

随后产生了众多数字货币，并且多年来建立了专用的（交易）平台，用于兑换法定货币和加密货币，反之亦然。目前，有超过 2,000 种加密货币（也称为替代币）^(12)，总市值超过 3000 亿欧元^(13)。其中最受欢迎的是以太坊、^(14)瑞波、莱特币、比特币现金、达世币和门罗币等。值得注意的是，其中一些新的加密货币解决了比特币固有的许多问题，因此在改进中有所突破，从而推动了加密货币的发展（Martino et al. 2019）。

加密货币市场自 2008 年以来在新货币数量、消费者基础和交易频率方面大幅增长（Dyhrberg 2016）。

然而，目前存在一些因素（如交易效率低（技术/可扩展性问题）和高波动性（Ciaian 等人 2016）），限制了加密货币在日常支付中广泛采用的潜力（瑞士银行 2018）。因此，加密货币必须在成本、速度和可扩展性方面与其他系统竞争。例如，新的交易技术（如 SEPA 即时信用转账）和资金转移系统（如 Transferwise）可以降低资金转移的成本和时间（即时方案允许进行泛欧洲信用转账，资金在不到 10 秒内即可使用）。加密货币的安全性和隐私性也一直是讨论的话题。在安全问题方面，加密货币可能会遭受盗窃和黑客攻击（例如，如果有人窃取用户的私钥，然后篡改用户的账户）。就隐私问题而言，Bohme 等人（2015）指出，比特币交易并非真正匿名，而是伪匿名，因为每笔交易都指定账户信息（即用户的公钥），尽管没有个人姓名，而区块链会发布带有该用户标识符的交易。据他们称，借助这些信息可以获得比特币用户的身份（另见 De Filippi 2016）。

此外，加密货币必须克服几个监管障碍（Jacobs 2018）。与加密货币相关的匿名性（或化名）和缺乏监管引发了严重关切，特别是关于加密货币被用于欺诈、黑客攻击、洗钱、资助恐怖主义和逃税等问题（Bohme 等人 2015; Richter 等人 2015; Houben 和 Snyers 2018，等等）。全球各地的监管机构担心犯罪分子越来越多地利用加密货币进行非法活动。由于上述问题，加密货币交换规则未来可能会改变，这是因为当局对此类问题进行干预（Martino 等人 2019）。

#### 初始代币发行机制

与加密货币相关联，区块链技术的另一个应用是首次代币发行（ICOs）机制，这代表了向新创企业融资的一种工具，特别是针对基于区块链的组织（Frame 等人 2018; Martino 等人 2019）。具体来说，ICO 机制代表了一种基于区块链技术和相关加密货币的新筹资模式。它的工作方式类似于众筹，但售卖不同性质的工具（代币），并且使用区块链技术进行验证，而不是众筹平台^(15) (Arnold 等人 2019; Fisch 2019)。

许多学者和金融机构认为 ICO 是企业融资领域的一项重要创新（Howell 等人 2018; Martino 等人 2019），并将其视为传统融资（如风险投资、天使投资者和众筹）的一种替代方式，因为它为新创企业和投资者提供了几项优势。越来越多的公司和个人正在使用 ICO 作为筹集资金或参与投资机会的一种方式^(16) (SEC 2017)。正如文献（如 Tapscott 和 Tapscott 2017; Howell 等人 2018; Fisch 2019; Huang 等人 2019; Martino 等人 2019, 2020）强调的，由于区块链技术的关键特点，ICO 可能使新创企业能够以更快、更灵活且成本更低的方式从全球各地的大量投资者那里筹集大量的资金，这比其他传统的融资机制（如众筹）更有优势。此外，它们为潜在投资者提供了便利，降低了参与成功初创公司的金融门槛，意味着任何人（包括小投资者）都可以投资任意金额进入一家公司。然而，ICO 确实存在一些潜在的风险缺陷。区块链技术的缺陷可能会受到网络攻击，缺乏监管可能会使投资者易受欺诈或增加非法活动（Martino 等人 2020)。^(17)

### 智能合约

区块链技术的另一个关键应用是*智能合约*，也就是“根据计算机科学家和密码学家 Nick Szabo 的说法，它是“执行合同条款的计算机化交易协议”，他在 1994 年首次提出了这个概念。他提出的想法是将合同条款转化为代码，并将其嵌入硬件或软件中，以便自动执行它们（即满足通用的合同条件），以尽量减少交易双方之间信任的中介和恶意或意外异常的发生（Szabo 1994, 1997). 因此，它们从根本上代表了以计算机代码编写的合同，一旦满足合同中规定的某些条件，就会自动执行^(18) (Lewis et al. 2017). 目前还没有为智能合约建立明确定义，它们的官方法律地位仍然有些不清楚（Lauslahti et al. 2017）。例如，Lauslahti 等人（2017, p. 11）将智能合约定义为“基于区块链共识架构的数字程序，在达成协议条款时将自我执行，并由于其分散式结构也是自动执行且防篡改的”。同样，Cong 和 He（2019, p. 1761）将智能合约定义为“允许基于去中心化共识的条款的数字合同，是防篡改的，通常通过自动执行来自我执行”。

尽管智能合约的概念是在 1990 年代发展起来的，但直到区块链技术的出现才变得更加流行。这是因为区块链能够更好地促进智能合约的执行，优于其发明时期的技术，因为区块链的分布式账本技术使得可以使用密码学托管和自动执行合约，而无需第三方（例如公证人、律师等）的参与^(19) (Fairfield 2014; Nofer et al. 2017; Gatteschi et al. 2018; Giudici and Adhami 2019). 具体来说，区块链允许将代码嵌入分布式账本中，从而使合同具有防篡改性，一旦满足特定的预定义条件，合同将自动执行，而不需要第三方来执行协议，因为双方都无法篡改代码 (Wang et al. 2019).

通过智能合约的实施，许多人（例如，Nowinski 和 Kozma 2017; Cong 和 He 2019）认为区块链可能会颠覆整个交易过程，并可能会对传统业务产生影响，因为智能合约可以实现当前需要手动干预的流程自动化：具体来说，它们可以以成本高效、透明和安全的方式实时自动执行商业交易和协议，而无需第三方参与。正如 Yermack 2017 年（#CR61）; Cong 和 He 2019 年（#CR11）的研究所指出的那样，智能合约的潜在应用非常广泛，特别是对于金融服务行业。例如，Cong 和 He（2019 年）声称智能合同可以提高合同可操作性，并以算法自动化的方式促进货币、财产、股份、服务或任何有价值的东西的交换。其他研究（例如，Capgemini 2016; Lewis 等人 2017）表明，智能合约可能允许自动化当前需要手动干预并依赖于实体文档的流程；这些流程表现出延迟、低效和更多的错误和欺诈风险。根据 Capgemini（2016 年）的一份报告，智能合约的采用可以降低风险，降低行政和服务成本，并提供更高效的业务流程，覆盖金融服务行业的所有主要领域。例如，其估计表明，美国和欧洲市场的抵押贷款借款人每笔贷款可能节省 480 至 960 美元，而银行通过降低抵押贷款原始流程的处理成本，每年可节省 30 至 110 亿美元。金融机构的其他相关领域，智能合约的使用可以减少支持经济交易执行所需的手动工作，并加快业务流程，包括全球支付、银团信贷、跨境结算和贸易金融，以及监管和合规活动（Swanson 2015; Capgemini 2016; Cong 和 He 2019）。

尽管上面提到了智能合约的诸多潜力，但在它们能够被广泛采用之前，还有一些挑战需要解决（Peters 和 Panayi 2016）。除了技术漏洞之外，使用智能合约还引发了许多法律和监管问题（Yermack 2017；Natarajan 等人 2017）。首先，智能合约是容易受到网络攻击的，因为它们无法被修改（智能合约攻击的最相关案例是 The DAO）（Gatteschi 等人 2018）。假设一个智能合约中存在漏洞，一旦合约存储在区块链上，由于区块链的不可变性，它将无法再次修改，这意味着没有直接的方式来修复这个漏洞（Atzei 等人 2017）。正如 Gatteschi 等人（2018）所建议的，开发人员应该创建一个新的合约，并将旧合约中的所有数据和指针转移到新合约中，以消除代码漏洞。其次，缺乏标准和规定引发了许多法律和监管问题，特别是关于责任、司法管辖权、修正案和合同的无效性的问题，以及与此相关的对于智能合约能否合法替代书面协议的担忧（Natarajan 等人 2017；Giudici 和 Adhami 2019）。例如，智能合约的不可变性（即它们部署后无法更改）可能会在外部条件改变时产生问题，比如法律的变动、适用法规的改变等，这将需要修改智能合约，或者如果某些事件对智能合约的当事方的权利和义务产生法律影响。在某些情况下，法院不承认智能合约的结果在现行法律下是合法的，也可能引发问题（Gatteschi 等人 2018）。因此，必须解决许多技术和法律问题，以使智能合约能够与现有的法律体系相互操作（Lauslahti 等人 2017）。