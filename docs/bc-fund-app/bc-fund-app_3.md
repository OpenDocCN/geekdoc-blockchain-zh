© 作者（们），在瑞士 Springer Nature AG 独家授权下 2022X. Yi 等。《区块链基础与应用》Springer 应用科学与技术简报[`doi.org/10.1007/978-3-031-09670-9_3`](https://doi.org/10.1007/978-3-031-09670-9_3)

# 3. 分布式共识

Xun Yi^(1  )，Xuechao Yang^(1  )，Andrei Kelarev^(1  )，Kwok Yan Lam^(2  ) 和 Zahir Tari^(1  )（1）澳大利亚皇家墨尔本理工大学计算技术学院，维多利亚州，墨尔本（2）新加坡南洋理工大学计算机科学与工程学院，新加坡，新加坡 Xun Yi（通讯作者）电子邮件： xun.yi@rmit.edu.auXuechao Yang 电子邮件： xuechao.yang@rmit.edu.auAndrei Kelarev 电子邮件： andrei.kelarev@gmail.comKwok Yan Lam 电子邮件： kwokyan.lam@ntu.edu.sgZahir Tari 电子邮件： zahir.tari@rmit.edu.au

## 3.1 引言

区块链技术依赖于几个技术组成部分。分布式共识协议是实现区块链去中心化的关键构建块。它允许所有参与者对共同账本当前状态达成一致，记录系统所有交易，而无需任何可信任的中心权威机构的帮助。分布式共识协议确定节点之间消息通信的条件和区块链社区中的决策过程。所采用共识协议的性能对整个区块链系统的有效性至关重要，因为它影响通信能力、可靠性和可扩展性。

比特币网络采用原始中本聪共识过程，该过程依赖于其*工作量证明*（PoW）挖矿算法。这一协议帮助比特币有效地建立起一种可靠数字货币，在点对点去中心化网络中有效抵抗所谓的双重支付攻击。比特币网络的指数级增长导致了几个瓶颈的出现，阻碍了比特币共识的性能，并造成了重大的可持续性问题。在大规模加密货币网络中，中本聪共识及其对 PoW 挖矿的依赖不可避免地导致了以下问题：

（1）不可持续的能源消耗，

（2）可扩展性差和低吞吐量，

（3）可能随挖矿奖励减少而增长的安全弱点。

例如，比特币的交易能力大约是每秒 7 笔交易（TPS），通过调整参数而无需危及安全，最多可以增加到 25 TPS [13]。目前比特币网络由大约 10,000 个节点组成 [7]。如果我们把这些数据与其他金融网络进行比较，我们会发现，例如，VISA 网络由超过 5000 万参与者组成，处理速度可以达到 65,000 TPS [36]。2019 年，有人指出，一个比特币交易消耗的电能相当于 21 个美国家庭一天的电力消耗 [15]。

为了解决 PoW 挖矿中固有的这些问题，研究人员一直在研究应用多种替代分布式共识技术，如权益证明（PoS）、权威证明（PoA）和流逝时间证明（PoET）等，以减少能源消耗，这只是举几个例子。密码学方法可以应用于实现参与者之间的信任，使处理新块的方案更加健壮，例如循环和基于委员会的块生成。

适当的激励措施，鼓励诚实在区块链网络中的参与，是共识协议的另一个关键组成部分。新的区块处理方案通常包含新的激励机制，促进所有参与者的公平性，并提高整个系统的可持续性。流行的区块链共识协议的例子包括 Peercoin [20]、Bitcoin-NG [17]、Ouroboros (Cardano) [19]、Snow White [14]、EOSIO [16]、POA Network [30] 等。

## 3.2 共识机制的历史

容错（FT）分布式共识算法已经得到了积极的研究很长时间。在分布式系统中，共识对应于所有参与者对一组变量的相同当前值达成一致的情况。

### 3.2.1 容错共识机制

拜占庭容错的概念是区块链技术的中心，因为每个区块链都必须保护节点最广泛的恶意行为和故障。回想一下，网络节点的*崩溃*是指节点停止运行，无法响应网络消息。拜占庭错误是一个广泛的术语，描述了一个试图隐藏其恶意行为的节点，它可能正确执行一些所需的步骤，但同时根据自己的判断，它也可以展示任何可以想象的不正确响应或恶意行为。对于共识协议中的诚实的参与者来说，识别拜占庭节点并从结果中排除他们的输入可能相当困难，因为这些有故障的节点正在尽其所能地保持不被发现，同时颠覆协议的结果。

如果一个共识协议可以容忍一定数量的崩溃故障并在这些故障下取得正确的结果，则该协议被称为*崩溃容错*（CFT）。同样，如果一个共识协议可以抵抗一定数量的拜占庭故障并继续正常运行取得正确的共识结果，则该协议被称为*拜占庭容错*（BFT）。每个 BFT 共识协议也是 CFT 的，因为拜占庭节点也可以模仿这些节点的崩溃。

为了使共识协议成为一个 BFT 共识，相应的网络中必须满足不等式 ![$$N \ge 3f + 1$$](img/516136_1_En_3_Chapter_TeX_IEq1.png)，其中 *N* 是网络中的节点数，*f* 是拜占庭节点的数量。这个基本定理最早是由 Pease 等人于 1980 年证明的[29]，后来被适应到 BFT 共识框架中。证明使用了归纳法，从归纳基础 ![$$N = 3$$](img/516136_1_En_3_Chapter_TeX_IEq2.png) 开始。在证明中，留下一个或两个节点使得 *N* 可以被 3 整除，然后将所有剩余的节点划分为三个大小相等的小组，使得所有故障节点都属于这三个小组中的一个。读者可以参考[4, 29]获取完整的证明。

### 3.2.2 实用拜占庭容错协议（PBFT）

实用拜占庭容错协议（PBFT）是由 Castro 和 Liskov 在一般分布式系统的背景下提出的[9]。之前的 BFT 共识算法扩展性不佳。PBFT 是第一个被认为具有实用性的 BFT 共识协议，并得到了广泛采用。它采用了状态机复制。消息处理算法被表示为一个有限状态机，所有节点都保持状态机的相同副本或复制品。选择一个节点作为主节点，其他节点称为客户端。PBFT 包括三个子协议：

（1）正常运行，

（2）检查点，

（3）视图变更。

正常运行协议如算法 3.1 所示。如果没有故障节点，那么节点收到的消息响应中的所有值都相等。否则，节点选择在响应中出现大多数的值，因为该值对应于诚实节点的回复。

检查点协议作为一种日志工具，保持一个滑动窗口以跟踪活动操作请求。最新的稳定检查点用于安全地丢弃操作日志中的旧请求，并促进视图变更协议。

视图变更消息用于确定主节点是否拜占庭式，如果是，则激活视图变更协议。在主节点失败的情况下，每个检测到主节点消息超时的副本都会触发视图变更协议。它们驱逐当前的主节点，并向彼此广播视图变更消息并进行接收计数。在接收到来自 2*f*个同伴的视图变更消息后，下一个副本成为新的主节点并通知其余副本恢复正常操作。![](img/516136_1_En_3_Figa_HTML.png)

一个算法描述了操作协议，包括请求阶段、预准备阶段、准备阶段、承诺阶段和回复阶段。

PBFT 正常操作的消息复杂度是![$$O(N²)$$](img/516136_1_En_3_Chapter_TeX_IEq3.png)，这是由于准备和承诺阶段的消息。每个节点都需要在准备或承诺阶段接收超过![$$2f + 1$$](img/516136_1_En_3_Chapter_TeX_IEq4.png)个准备或承诺消息，以便处理下一个请求的操作。这依赖于至少![$$2f + 1$$](img/516136_1_En_3_Chapter_TeX_IEq5.png)个诚实的节点在相同的状态下，考虑到假设![$$N \ge 3f + 1$$](img/516136_1_En_3_Chapter_TeX_IEq6.png)。因此，剩余的*f*个拜占庭式节点不能改变大多数共识接受的价值。因此，当不等式![$$N \ge 3f + 1$$](img/516136_1_En_3_Chapter_TeX_IEq7.png)成立时，PBFT 可以容忍*f*个拜占庭式错误。根据基本 1/3 BFT 阈值，这是可以达到的最佳 BFT 性能。读者可以参考 [9, 37] 获取更多详细信息和严格的证明。

PBFT 激发了各种其他共识协议的发展，这些协议增强了性能和安全。这些协议中知名的例子包括 Quorum/Update (QU) [1]，混合 Quorum (HQ) [12]，使用投机执行的 Zyzzyva (Zyzzyva) [21]，FaB [25]，Spinning [35]，健壮的 BFT SMR [10]，和 Aliph [5]。读者可以参考教程 [6] 了解这些协议的概览。

## 3.3 区块链共识概览

区块链网络允许每个参与者既可以是发出交易的客户端，也可以是验证和最终确定交易的服务器。区块链账本的数据结构由按时间顺序排列且通过哈希链链接的区块组成，每个区块都需要共识才能包含在账本中。每个区块包含一组有效的交易。区块链上的交易应与其他交易保持一致，以防止双重花费、过度花费和挪用。

区块链系统通常与负责交易处理和验证的金融应用相关联。因此，区块链共识协议的目标和责任可能比传统分布式共识协议的目标和责任更为增强。

### 3.3.1 区块链共识的目标

区块链共识协议的目标是确保所有参与节点对一个共同的网络交易历史达成一致，该历史以账本形式序列化。根据之前对 BFT 共识的讨论和[37]中提供的共识目标抽象，我们为区块链共识定义了以下要求。

+   **终止**。在每一个诚实节点，一个新的交易要么被丢弃，要么被纳入区块接受进入区块链。

+   **协议**。每一个新交易及其持有区块应该被所有诚实节点接受或丢弃。被接受的区块应该被每一个诚实节点分配相同的序列号。

+   **有效性**。如果每个节点都接收到相同的有效交易/区块，它应该被纳入区块链。

+   **完整性**。在每一个诚实节点，所有接受的交易应该彼此一致，并应防止双重花费。所有接受的区块应该正确生成并以时间顺序进行哈希链结。

### 3.3.2 区块链共识协议的组件

区块链共识协议的五个关键组件如下对应于前一小节的主要要求。

+   **块提议**。生成区块并附上生成证明。

+   **信息传播**。在网络中传播区块和交易。

+   **区块验证**。检查区块生成证明和交易的有效性。

+   **块最终化**。对验证过的区块达成接受协议。

+   **激励机制**。促进诚实参与并创建网络代币。

这五个要素为区块链共识提供了基本功能。然而，一些新的区块链共识算法并不包括所有这些组件。例如，激励机制对于无权限区块链是绝对必要的。然而，对于所有参与者都被识别并正式授权参与的授权区块链，激励机制是不必要的，因为管理员可能简单地要求所有参与者正确操作，而不需要额外的激励。许多新的公有区块链提案只涵盖块提议的过程，并从 Nakamoto 共识算法中包含了其余组件。这是因为 PoW 块提议计算强度如此之大，以至于改进它是可持续性的首要任务。

## 3.4 工作量证明共识协议

Nakamoto 工作量证明（PoW）[28]共识协议是使比特币成为可能的的关键创新。它可以总结如下。

+   **工作量证明（PoW）**。区块生成需要找到一个哈希函数的预图像，使得哈希结果满足一个难度目标，该目标动态调整以保持平均区块生成间隔。

+   **八卦规则**。每个新接收或生成的交易或区块应立即广告并向所有对等节点广播。

+   **验证规则**。在向对等节点广播或添加到区块链之前，区块或交易需要进行验证。验证包括检查交易中没有双重花费，并验证区块头中工作量证明的有效性条件。

+   **最长链规则**。最长的链代表网络共识，任何看到它的节点都应接受它。挖矿应始终扩展最长的链。

+   **区块奖励和交易费**。区块的生成者可以声称一定数量的新代币以及从所有包含的交易中收集的费用，以硬币交易的形式。

计算密集型 PoW 过程旨在缓解 Sybil 攻击。比特币网络是无需许可的，所有参与者都可以以伪匿名方式加入。Sybil 攻击发生在一个成员创建多个身份和几个账户的情况下。PoW 过程要求使用真实硬件解决困难任务，并且无法伪造。

最长链规则确保账本的最长链在可能允许对最后几项进行修改的情况下保持稳定。因此，最长链可以作为系统历史的普遍接受的记录。比特币社区不预见任何权威实体，并且是去中心化的。区块奖励和交易费用于激励矿工参与并创建新的比特币。

Nakamoto 协议的高级版本在算法 3.2 中给出。在区块生成期间，更高的挖矿难度要求进行更多的暴力试验，以找到满足要求的 nonce。为确保每个区块在新区块产生之前都得到充分传播，每 2016 个区块调整一次挖矿难度，使预期区块间隔保持恒定值（比特币中为 10 分钟），无论矿工的总计算能力如何波动。![](img/516136_1_En_3_Figb_HTML.png)

Nakamoto 共识协议的算法流程包括网络加入阶段、主循环阶段、八卦规则阶段、最长链验证阶段、基于 POW 的区块生成阶段、POW 散列谜题阶段以及最终条件。

## 3.5 股份证明共识协议

权益证明（PoS）是 PoW 挖矿的能量高效的替代方案。参与者的质押是其节点拥有的硬币或网络代币的集合，可以投入以支持区块链共识过程。因此，在 PoS 中应用代币所有权以防止 Sybil 攻击。因此，PoS 矿工提议账本块的概率与矿工拥有的质押价值成比例，而 PoW 矿工提议账本块的概率与矿工设备拥有的暴力计算能力成比例。从可持续性的角度来看，PoS 消除了计算能力和电能的浪费，并要求矿工投入或质押他们的代币[31]。由于 PoW 共识不要求真正的挖矿工作，而更类似于投资资本市场，因此 PoS 矿工也常被称为*验证者*、*发行者*或*代币持有者*。

我们确定了四种权益证明（PoS）协议的类别：基于链的 PoS、基于委员会的 PoS、基于 BFT 的 PoS 和委托 PoS（DPoS）。基于链的 PoS 继承了 Nakamoto 共识协议的许多组件，如信息传播、区块验证和区块最终确定（即最长链规则）。区别在于，区块生成机制被 PoS 所替代。基于委员会的 PoS 利用多方计算（MPC）方案，使委员会能够协同生成区块。基于 BFT 的 PoS 将质押与 BFT 共识结合，确保块的确定性最终性。DPoS 采用一种社会投票机制，选举一定数量的代币持有者代表投票者进行交易验证和区块链共识。

### 3.5.1 基于链的 PoS

基于链的 PoS 是一种早期的 PoS 方案，作为块生成机制的替代方案。消息传递的八卦规则、区块验证规则、最长链规则和概率性最终性与其他 Nakamoto 共识框架保持一致。早期的基于链的 PoS 区块链系统包括 Peercoin 和 Nxt。

基于链的 PoS 发行者的通用流程总结在算法 3.3 中。一个 PoS 发行者只能在时钟滴答一次的情况下解决哈希谜题。由于发行者的角色随着发行者质押值的增长而增加，因此可以减少发行者解决哈希谜题的预期次数，以防止一个发行者主导系统。这样，PoS 避免了矿工的暴力竞争，减少了能源消耗。![](img/516136_1_En_3_Figc_HTML.png)

关于基于链的通用流程算法，包括加入网络阶段、主循环段、基于 PoS 的块生成、PoS 哈希谜题阶段和最终条件。

### 3.5.2 基于委员会的 PoS

基于委员会的 PoS 根据他们的股份确定一个利益相关者委员会，并允许委员会成员轮流产生区块。在分布式网络中，通常使用安全多方计算（MPC）技术来导出这样的委员会。MPC 是一种分布式计算类型，其中多个拥有各自输入的各方安全地计算出结果，而不揭示他们各自条目的值 [32]。基于委员会的 PoS 中的 MPC 过程实际上实现了这样一种功能：输入当前区块链状态以及所有利益相关者的股份值，输出一个称为*领导者序列*的伪随机利益相关者序列。然后根据序列中的顺序填充委员会。所有节点都知道相同的领导者序列。股份较高的参与者被允许占据更早的位置，在序列中可以更频繁地出现。基于委员会 PoS 的节点的一般程序在算法 3.4 中显示。在这个算法中，CommitteeElect()函数也可以通过可验证的随机函数（VRF）[26]以隐私保护的方式实现，这样只有节点本身知道它们是否被选入委员会。![](img/516136_1_En_3_Figd_HTML.png)

基于委员会 PoS 的通用程序上的算法，包括加入网络和跟踪阶段，主循环阶段，委员会选举阶段，区块提议和广播阶段，最长链和验证规则阶段，基于 PoS 的委员会选择阶段，以及最终条件阶段。

### 3.5.3 基于 BFT 的 PoS

基于链的 PoS 和基于委员会的 PoS 在很大程度上遵循 Nakamoto 共识框架，即仍然使用最长链规则来提供块的概率性最终性。相比之下，基于 BFT 的 PoS（或混合 PoS-BFT）包含了一个额外的 BFT 共识层，提供了快速和确定性的块最终性。算法 3.5 显示了每个参与者的基于 BFT 的 PoS 的一般程序。提出块的过程可以使用任何 PoS 机制组织：循环，基于委员会或其他方法。唯一的要求是该过程保证新的块稳定流入账本。

一种验证机制可以用来确认区块链账本的最终性。这个选项不包括在算法 3.5 中。然后，最长链规则可以被最新的验证规则所取代，以确定稳定的主链。流行的基于 BFT 的 PoS 区块链协议包括 Tendermint、Algorand 和 Casper FFG。像 EOSIO 这样的 DPoS 协议也使用 BFT 共识来进行委托之间的区块最终确定。![](img/516136_1_En_3_Fige_HTML.png)

基于 B F T 的 PoS 通用流程的算法，包括加入网络和追踪，主循环段，区块提议和广播，区块验证阶段，B F T 的共识层，基于 PoS 的区块生成，基于 B F T 的区块最终确定，以及最终的条件。

### 3.5.4 委托 PoS（DPoS）

委托 PoS（DPoS）采用一种民主形式的 PoS 委员会创建方式。共识委员会是通过公开的股份委托方式选出的。DPoS 被 BitShares 2.0 [8]、Lisk [24]、EOSIO [16] 和 Cosmos [33] 使用。DPoS 旨在控制共识组的大小，以便共识协议的消息开销保持可管理。共识组的成员也被称为*代表*。代表的选举也称为委托过程。

为了当选为代表，每个候选人必须从代币持有者那里获得足够的票数。这通常是通过提供一个受欢迎的应用程序并通过宣传运动建立声誉来实现的。通过区块链交易向代表投票，代币持有者将自己的股份委托给代表。因此，代表合并了来自投票者的股份投票权，在共识过程中作为他们的代理人。代币持有者可以通过新的委托交易将投票切换给另一个代表。例如，EOSIO 协议规定任何人都可以成为代表并寻求票数，但只有排名前 21 的加入共识组，其中块提议权平等共享。EOSIO 采用了一种流水线式的 PBFT 风格的共识方案，以便在 21 名代表之间最终确定提出的区块 [22]。特别是，物理时间被划分为槽，21 名代表轮流以循环方式提出区块。在每个代表提议块的槽中，共识方案经历预提交和提交阶段，并在提出的块上宣布决定。由于共识组规模较小，以及井然有序的 PBFT 风格过程，每个新的有效交易都可以迅速推广到共识组并在区块链上最终确定。

为了执行交易验证和共识安全，DPoS 的激励机制旨在鼓励诚实的委托和共识参与。每位代表每天获得的奖励与代表获得的投票成比例。成为共识小组成员后，代表还会因为验证每个区块而获得奖励。

## 3.6 其他区块链共识协议

现代大多数区块链共识机制都采用了 PoW、PoS 和 BFT 等成熟的技术，并进行了一些小的修改和改进。然而，在学术文献中也有许多其他有前景的新颖区块链共识算法提案，这些提案针对的是各种应用领域。这些新颖方案中的许多仍然是概念性的，只描述了区块链共识协议的五大部分中的一个或两个。接下来，我们将回顾权威证明（PoA）、时间消耗证明（PoET）、安全区股份证明（PoTS）和可检索性证明（PoR）。

### 3.6.1 权威证明（PoA）

权威证明（PoA）这一术语是由以太坊联合创始人 Gavin Wood 提出的，作为一种替代 PoW 和 PoS 的机制。它目前部署在以太坊的 Rinkeby（2017）和 Kovan（2017）测试网上，以及 POA 网络（2018）[30]。PoA 协议是对 PoS 的一种改进。验证者使用他们的授权身份作为股份，而不是具有货币价值的代币。为了被接受为 PoA 验证者参与共识团队，每个候选人必须通过一个强制性的认证程序，该程序为候选人分配一个批准的身份值。在这个过程中，候选人的身份可能会被验证，并且可以考虑之前的操作历史，因为这证明了他们为共识团队做出贡献的能力。官方认证文件随后可以公开提供。共识团队应该是稳定且相对较小的，它通过公开审查，确保用户可以信任团队进行可靠的交易处理和区块链管理。在执行这些任务时表现出无能或不正当行为的验证者应该被用户和同行验证者审查并排除。

### 3.6.2 时间消耗证明（PoET）

时间消耗证明（PoET）是由英特尔在 2016 年提出的一种替代挖矿机制，随后被应用于 Hyperledger Sawtooth 区块链平台[34]。PoET 不是通过耗费算力的挖矿，而是模拟了消耗工作量证明（PoW）挖矿的时间。也就是说，每个节点在宣布其区块之前，都会随机等待一个指数分布的时间周期。为了确保本地时间真正流逝，PoET 要求退避机制在可信执行环境（TEE）中执行，TEE 是一个提供对运行其中的程序保密性和完整性的内存隔离区域，以防止被恶意的主机平台侵害。在 TEE 中包含的程序称为*安全区*。英特尔 SGX [11] 和 Arm TrustZone [3] 是两种主要的 TEE 解决方案。TEE 通过远程证明提供 enclave 程序的完整性证明，帮助网络建立对共识节点的信任，这其中包括了许多其他设施。

### 3.6.3 安全区股份证明（PoTS）

证明 TEE-Stake（PoTS）是另一个基于 TEE 的区块链共识协议。它由 Li 等人 [23] 提出，并由 Andreina 等人 [2]. 每个 PoTS 节点*i*遵循与 PoET 相同的设置过程来设置一个 TEE enclave，生成签名密钥对![$$\langle SK_i, PK_i \rangle $$](img/516136_1_En_3_Chapter_TeX_IEq8.png)，并将设置通知网络。而不是模拟 PoW 挖掘的流逝时间，PoTS 的 enclave 程序类似于 Algorand 的加密方案，根据股份分布随机选择一个委员会。委员会中的每个节点都有资格为即将到来的区块周期提出一个新的区块。为了证明区块提案是合格的，区块包括资格证明签名![$$\sigma ^{ep}_{SK_i}$$](img/516136_1_En_3_Chapter_TeX_IEq9.png)，该签名由区块生成节点的 enclave 程序产生。一旦其他节点收到这个区块，他们会验证区块内容以及其签名![$$\sigma ^{ep}_{SK_i}$$](img/516136_1_En_3_Chapter_TeX_IEq10.png)是否使用节点的公钥![$$PK_i$$](img/516136_1_En_3_Chapter_TeX_IEq11.png)。然后使用最长链规则来确定是否接受这个区块进入账本。

### 3.6.4 证明可检索性（PoR）

证明可检索性（PoR）最初由 Juels 和 Kaliski [18] 提出，作为半可信分布式归档的一个加密基础。PoR 的关键功能允许文件所有者验证他们的在线文件或文件片段是否被安全地存储并且可以通过应用一个特殊的挑战-响应协议来检索。文件*F*在远程节点![$$n_i$$](img/516136_1_En_3_Chapter_TeX_IEq12.png)的可检索性可以证明![$$n_i$$](img/516136_1_En_3_Chapter_TeX_IEq13.png)确实为*F*分配了所需的存储资源。由于可检索性内在的空间要求，PoR 也被称作*空间证明*。

作为一种分布式共识协议，PoR 首先被 Miller 等人 [27] 提出的加密货币 Permacoin 使用。它被发明作为另一种消除挖矿工作的 PoW 替代方案。在算法中，一个中心管理员发布一个目标数据集*F*并计算*F*的摘要（所有段落的 Merkle 哈希树根）。然后每个参与者根据其存储能力存储*F*的一些随机段并计算这些段的摘要。对于每一个区块周期，经销商发起一个带有随机谜题的彩票游戏。然后每个参与者从其本地存储的段、公钥和谜题导出一个包含固定数量 PoR 挑战的彩票。

存储了更多数据的参与者赢得彩票的概率更高，因此有资格生成一个区块。所有 PoR 挑战都存储在新区块中，并整个网络进行验证。Permacoin 还实现了一个签名方案，以阻止参与者将存储任务外包。除了采用 PoR，Permacoin 还继承了比特币在共识机制的其他组件方面的方法。

与 PoW 相比，PoR 更经济且具有优势。首先，PoR 的文件存储比 PoW 的暴力挖矿消耗的能源更少。其次，作为资源的存储空间可以被回收。第三，PoR 可以被重新编程执行有用且有意义的存储任务，这并非浪费而是能带来其他好处。例如，在过程中使用的数据集可以是一些大但实用的公共数据集，为了许多用户的利益必须进行存储。
