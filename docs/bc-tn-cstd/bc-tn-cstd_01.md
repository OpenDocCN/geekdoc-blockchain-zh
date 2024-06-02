© 作者（们），在独家授权下由 APress Media, LLC 出版， Springer Nature 集团的一部分 2023B. Wu, B. Wu 青少年区块链[`doi.org/10.1007/978-1-4842-8808-5_1`](https://doi.org/10.1007/978-1-4842-8808-5_1)

# 1. 区块链：一项突破性技术

Brian Wu^(1  ) 和 Bridget Wu^(1)(1)Livingston, NJ, USA

近年来，拥有加密货币的美国人数量不断增加。即使那些没有加密货币的人，大多数美国人也已经听说过加密货币——比特币这个名字听起来是否熟悉？如果你听说过区块链，但不确定它如何工作，那么不用担心；你并不孤单！尽管区块链乍一看可能是一个令人畏惧的话题，但我们将帮助你熟悉区块链的重要概念。

本章将从区块链的基础知识开始。然后，我们将讨论区块链是如何工作的，并深入了解共识算法。接下来，我们将学习货币系统的演变以及区块链技术如何影响货币、商业和现代世界。最后，在本章末尾，我们将提供一个加密货币的概览。

在本章中，我们将讨论区块链的以下具体主题：

+   什么是区块链？

+   区块链是如何工作的

+   共识算法

+   货币系统的演变

+   理解加密货币

## 什么是区块链？

在所有加密货币的核心，我们可以找到一种革命性的去中心化技术，即区块链。明确我们所指的去中心化很重要，因为这一概念在区块链中经常被使用。让我们先看看去中心化的反面：集中化是指权力由特定的个人、组织或地点持有。

图 1-1 显示了一个集中式组织的示例。![](img/535492_1_En_1_Fig1_HTML.png)

两个集中式组织的流程图。第一个图从上到下的标签部分是 C E O、工程经理、市场营销经理、工程师和市场营销员。第二个图被标记为集中式，箭头从中央结构向外指。

图 1-1

集中化示例

想象一下公司内典型的层级结构——高管做出所有关键决策。然后，高管将决策传达给经理，他们负责较低层次。他们需要完成高管分配给他们的任何任务。再进一步，员工被期望听从他们的经理，并完成分配的工作。虽然集中式公司可以相对快速和容易地实现目标，但员工通常无法与其他部门和更高层次进行沟通。缺乏这种沟通可能会导致问题，并导致失败，使所有层次都受到影响。通常，公司任何部分的一个缺陷都可能危及目标，这被称为单点故障。

中心化的另一个例子是在线服务提供商，如 Meta（Facebook）、亚马逊、苹果和谷歌。这些互联网服务遵循客户端-服务器架构。用户使用客户端机器（也称为远程处理器——想想网页浏览器或手机）向中心化服务器机器（也称为主机系统）发送远程请求。用户从这个单一的复杂服务提供者那里接收服务请求的结果。从好的方面来说，数十亿人使用这些出色的数字服务进行日常任务，如在线购物、发布照片和给家人朋友打电话，而且都是免费的。但这些“免费”服务的被忽视的成本是：这些公司在其中心化服务器上收集和存储了大量有价值的用户行为数据。利用大数据分析和机器学习算法，这些用户数据被转化为产品并出售给第三方。有了这些数据，公司可以在广告和服务中针对用户，增加暴露于安全风险的机会——这一切都超出了用户的控制范围。

既然我们已经了解了中心化，我们可以探讨去中心化，它指的是将权力从顶部权威或位置分配给每个单元。与之前我们看过的例子不同，在去中心化组织中，决策制定不是集中在中心权威或权力。每个成员都是独立的，可以决定组织活动。与去中心化相比，所有成员都参与其中，共同努力实现目标。根据组织的规则，每个人都可对决策进行投票。![](img/535492_1_En_1_Fig2_HTML.png)

两个区块链图表展示了在市场营销和工程中的去中心化组织结构。标记的流程位置包括 C E O、经理、工程师和市场营销员。

图 1-2

去中心化示例

与中心化的在线服务提供商相比，去中心化的世界为用户提供了对其交易和数据的完全控制权。在做出决策时，每个成员拥有平等的权力。系统将接收来自个别参与者的决策，并利用[加密学](https://101blockchains.com/what-is-consensus-algorithm/)共识方法（我们稍后会查看这个）做出决策。没有单一的权威来接收和响应请求；即使某些个体不参与决策制定，系统仍然可以运行。

表 1-1 提供了中心化和去中心化的比较。表 1-1

比较中心化和去中心化

|  | 中心化 | 去中心化 |  |
| --- | --- | --- | --- |
| 单点故障 | 是 | 否 | 区块链网络是点对点的，每个节点都拥有区块链数据的完整副本。因此，当发生故障时，数据永远不会丢失。 |
| 谁掌控着一切？ | 集中式权威 | 用户 | 区块链网络中没有集中的权威机构来控制。 |

现在我们理解了集中化和去中心化的区别。那么，区块链到底是什么呢？

在一片古老的被称为 Shell 岛的地方，人们经常彼此交易，以获取他们需要或想要的资源。起初，岛民相互信任，只交易贝壳和食物；这短时间内运作得很好。过了一段时间，岛民交易更加复杂的商品，如珠宝、衣服和工具。随着交易变得更加频繁和复杂，追踪它们变得越来越困难。例如，某人与 20 人每天交易，但与每个人交易的商品都不同。为了解决这个问题，岛上的领导者雇佣了一个值得信赖的“中间人”来记录所有交易，以保持交易的公平和可审核；这也在一段时间内运作得很好。然而，“中间人”开始对他的工作收取额外的费用，甚至开始接受贿赂。随着不公平的交易越来越多，腐败在岛上蔓延，没有人再信任这个“中间人”了。由于交易减少，商业活动也随之放缓。为了帮助人们再次公平交易，岛上的领导者解雇了“中间人”，并同意用一个更高效的解决方案来替代他。岛中心有一块巨大的石头，每个人都能清楚地看到。领导者提出，岛民可以在交易者完成并证明交易后，将每笔交易信息永久性地依次刻在石头上，这样可以使系统可验证。这块石头对每个人开放，所以岛上的任何人都可以查看和验证这些交易，这意味着系统是透明的。如果任何记录不匹配，岛民可以投票验证记录，这赋予了每个人平等的参与权力。岛民也不需要相互信任这个系统才能运作；他们只需要去石头上看记录，而不是依赖“中间人”，这使得系统无需信任。岛民同意遵循领导者提出的这些规则，从那时起，对所有人来说都有一个幸福的结局，公平交易对所有人都是可能的。

类似于 Shell 岛交易系统，区块链是一个去中心化的点对点网络。在区块链网络中，参与者可以无需中央权威机构即可提交和确认交易。一旦交易数据保存在网络中，它将不可变，或者说是无法被更改的。网络成员或节点可以直接在网络上相互交互，而无需中央权威机构或中间商来干涉交易过程。

区块链也被称为分布式账本技术（DLT）。DLT 允许所有数据在跨越多个实体或位置的计算机网络中共享，这些被称为节点。每个节点保留区块链账本相同的副本。

区块链具有以下关键特性：

1.  1.

    去中心化

    正如我们所学的，区块链的去中心化意味着将中心权力分布到区块链网络中的所有参与用户，这消除了单一故障点。它通常存在于对等网络中。

1.  2.

    共识协议

    分布式共识是任何区块链网络的一个重要组成部分。所有网络参与者必须达成共识，以将交易记录添加到区块链。这将使区块链能够呈现交易的一个版本。有许多共识协议，包括：

    +   工作证明（PoW）

    +   股份证明（PoS）

    +   实用拜占庭容错（PBFT）

    +   委托证明股份（DPoS）

    +   证明时间流逝（PoET）

    +   权威证明（PoA）

    +   还有更多…

我们将在后面的章节讨论一些这些共识协议。

1.  3.

    不可变性

    区块链的不变性意味着一旦数据被记录在区块链上，就无法操纵、更改或删除数据。区块链数据将永远存在。

1.  4.

    透明度

    所有区块链交易都可供任何方或个人公开查看，这实现了透明度。

1.  5.

    安全性

    由于区块链的不变性和去中心化特性消除了单一故障点，区块链中的记录无法被篡改。这使得区块链数据极其安全。当用户从区块链钱包中转移资金时，它们由钱包的私钥加密签名。我们将在第二章解释这一点。

图 1-3 展示了区块链的关键特性。![](img/535492_1_En_1_Fig3_HTML.png)

一个带有标记特性的区块链流程图。标记的链流是去中心化、不可变性、安全性、透明度和共识。

图 1-3

区块链关键特性

既然我们已经对区块链的概念有了相当的了解，接下来我们将看看区块链是如何工作的。

## 区块链是如何工作的

区块链由一系列有序的区块组成。当生成新的区块时，它通过散列机制连接到前一个区块。这样，最新的数据总是可以添加到链的顶部。

想象一下有一个涵盖一整年的每日墙历。这个日历最初从 1 月 1 日开始。一天结束后，日历的主人会翻到下一页，将是 1 月 2 日。因为日期的数字遵循线性序列，所以很容易看出是否缺少或修改了任何页面。![](img/535492_1_En_1_Fig4_HTML.png)

从区块 1 到区块 n 的区块链图考虑为 T 1 到 T n，包括第 3、4、5 天和今天。

图 1-4

区块的区块链图

还需要知道，位是一个二进制数字（要么是 0 要么是 1），它是存储在计算机上的最小数据单位。8 位等于 1 字节。

散列是一个独特的标识符，它使用数学函数从输入文本或数据记录生成固定长度的字符串。（我们将在第二章更详细地解释散列和加密函数。）加密散列函数旨在保护数据免受任何更改。

区块链的散列算法 SHA-256，或安全散列算法 256，生成一个 256 位或 32 字节的散列码。SHA-256 是一种单向散列函数，意味着它很容易计算，但逆转散列以找出原始输入是什么几乎是不切实际的。即使输入消息有最小的变化，通常也会使输出散列完全不同。要破解散列结果，最好的方法是通过暴力破解策略，这意味着逐一测试每一种可能的组合。方法是猜测被散列的原始值，通过应用相同的散列函数来看结果是否匹配。我们需要处理 2²⁵⁶个 256 位字符串的变体，这将产生总共 3.2 * 10⁷⁹种可能的组合。总计算时间将超过十亿年。

SHA-256 散列也是确定性的，意味着给定相同的输入（或文件），输出将始终生成相同的散列值。

表 1-2 显示了 SHA-256 散列的示例。表 1-2

SHA-256 散列示例

| SHA-256（输入） | 输出 |
| --- | --- |
| Hellohello | 185f8db32271fe25f561a6fc938b2e264306ec304eda518007d17648263819692cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824 |
| 针对青少年的区块链 | ae398c6f1d78e76d472c26e091869b9913f7624abea82901c00893a0015ccd50 |
| 区块链散列 | f067428fdeb5984a6eeff5dbbe39a60cdb9dbffecdb80f18830eeb1e91d3dde5 |

您可以看到，输入数据的长度不影响输出长度——输出总是 64 个字符的文本。正因为如此，从输出中猜测输入几乎是不可能的。区块链使用这个 SHA-256 散列函数来散列交易数据，确保交易不能轻易被篡改。如果有人想要篡改一个交易，他们需要重新散列它，这将完全改变输出。所以，当我们提到散列时，我们指的是散列算法的 64 个字符文本输出。

每个区块的结构分为区块标题和正文，如图 1-5 所示。![](img/535492_1_En_1_Fig5_HTML.png)

区块的图包括一个标题和一个正文。标题的标签部分包括版本、前一个区块散列、时间戳、n 位、nonce、merkle 根。正文有部分标签为交易，还有一个标签为交易计数器的盒子。

图 1-5

区块链区块结构

### 区块头部

区块头部由块版本、前一个块哈希、时间戳、nBits、nonce 和 Merkle 根等几个组件组成：

**区块版本 –** 区块链的版本号。

**前一个块哈希** – 当前块必须引用前一个块的哈希，称为父块，以确保新块按正确顺序添加到链中。它允许用户从当前块中了解之前的交易。通过追踪连接每个块到其父块的哈希，我们可以回溯到第一个块，即*创世块*。

**时间戳 –** 块添加的时间和日期。

**nBits –** 当前用于创建此块的共识算法的难度。（我们将在下一节中介绍。）

**Nonce –** 称为**一次使用的数字**，区块创建者被允许改变的一个随机值，以产生一个小于目标哈希的块哈希。

**Merkle 根** – Merkle 树是一种基于哈希的数据结构，也称为二叉哈希树。Merkle 根是 Merkle 树的根节点。

在计算机科学中，树是一种数据结构，包含一系列节点。

树具有以下属性：

+   每个节点只有一个父节点。

+   每个节点最多可以有两个子节点。

+   树有一个没有父节点的节点，称为根节点（或根）。树从根节点开始。

+   节点通过边连接。

+   每个节点内部都有一个数据元素。

图 1-6 是二叉树的示例。A、B、C、D、E、F、G 和 H 都是节点。A 是根节点，B 和 C 是 A 的子节点；它们通过边连接。E 和 F 是 B 的子节点。G 和 H 是 C 的子节点。![](img/535492_1_En_1_Fig6_HTML.jpg)

二进制数据结构的树形图。A、B、C、E、F、G 和 H 是节点。A 是根节点，B 和 C 通过边连接。

图 1-6

树数据结构

由于 Merkle 树被归类为二叉哈希树，所以它会共享相同的树结构。每个叶节点都是一个数据的哈希。每个节点包含区块链交易数据，这意味着子节点的哈希包含在父节点中。

在我们之前的树形结构示例中，由于这些节点没有子节点，叶节点将是 E、F、G 和 H。B、C 和 A 是父节点，A 是根节点。

如果我们假设节点 E 有一个交易值，那么将使用哈希函数 HASH(E)对块数据进行哈希，其他叶节点也会有类似的哈希：HASH(E)，HASH(F)，HASH(G)，HASH(H)。当我们到达父节点时，每对子节点都会递归地（根据规则反复）重新哈希，直到我们到达根节点。

父节点 B 是它们的子节点 E、F 的哈希 – HASH(HASH(E) + HASH(F))。

父节点 C 是它们的子节点 G、H 的哈希 – HASH(HASH(G) + HASH(H))。

根节点 A 是 Merkle 根；它包含跟随它的树节点的哈希：HASH(HASH(B) + HASH(C))。

图 1-7 展示了从叶子节点哈希到根节点的 Merkle 根哈希值是如何计算的。![](img/535492_1_En_1_Fig7_HTML.png)

从叶子节点哈希到根节点的 Merkle 哈希计算树形图。哈希 A 的根是哈希 B 加 C，哈希 B 的根是哈希 E 加 F，哈希 C 的根是哈希 G 加 H。

图 1-7

Merkle 树哈希计算

我们为什么需要 Merkle 根哈希？

在之前的例子中，H(B) = H(E) + H(F)。

假设 E 是 1，F 是 2。我们将使用 SHA-256 哈希函数。

SHA-256(1) = 6b86b273ff34fce19d6b804eff5a3f5747ada4eaa22f1d49c01e52ddb7875b4b

SHA-256(2) = d4735e3a265e16eee03f59718b9b5d03019c07d8b6c51f90da3a666eec13ab35

为了简化，让我们将两个哈希值连接（组合）在一起成为一个长字符串（H(1) + H(2)），所以我们得到以下值：

33b675636da5dcc86ec847b38c08fa49ff1cace9749931e0a5d4dfdbdedd808a

但是如果我们通过改变顺序来连接（H(2) + H(1)），我们得到 9704a05c9afffc927899ad21907866ec72b166fd58250b57bca6a184e462d554。

你可以看到，即使是微小的变化也会导致完全不同的结果。考虑到每个区块数据需要包括交易数据、时间戳以及许多其他类型的数据，更改这些值中的任何一个都会导致 Merkle 根哈希完全不同。在之前的例子中，我们可以按以下方式计算 Merkle 根哈希：

Merkle 根哈希 = H(B) + H(C) = H(E) + H(F) + H(G) + H(H)。

根节点哈希代表了整个节点数据的指纹。为了验证节点数据的完整性，你不需要下载整个块的数据并遍历整个 Merkle 树；你只需要检查数据是否与 Merkle 根哈希一致。如果区块链网络中的区块副本具有与另一个相同的 Merkle 根哈希值，那么该区块中的交易是相同的。通过这种方式，交易数据可以被迅速证明。

在区块链中，每个区块都在区块头部存储了 Merkle 根。Merkle 树允许网络上的每个节点验证单独的交易，而不需要下载并验证整个区块。如果区块链网络中的区块副本具有与另一个相同的 Merkle 根，那么该区块中的交易是相同的。由于哈希的特性，即使是一点错误的数据也会导致截然不同的 Merkle 根。因此，没有必要验证所需信息的数量。

所有区块都通过其前一个区块哈希作为指针连接在区块链中，形成一个区块列表。由于区块头部包含了 Merkle 根哈希，我们可以通过执行哈希操作来验证区块头部和交易数据是否被篡改。交易数据的任何微小修改都会导致整个链中所有区块哈希指针的整体变化。

现在区块链通过一系列连续的区块链接在一起。它看起来像图 1-8 所示。![](img/535492_1_En_1_Fig8_HTML.png)

一个水平区块链的示意图，有 2 个小立方体和一个大的立方体形状的中间块。标签部分包括前一个区块散列、头部、体、交易计数器和 Merkle 根，

图 1-8

区块的顺序以及 Merkle 树和前一个区块散列

### 区块体

区块体由交易计数器和交易组成。

#### 交易计数器

交易编号代表存储在区块中的交易数量。交易计数器是 1 到 9 字节。它通常用于衡量区块链每日交易次数或“TPS”——每秒交易次数。以下图表（来自[`studio.glassnode.com/`](https://studio.glassnode.com/)）显示了比特币的每日交易次数：

![](img/535492_1_En_1_Figa_HTML.png)

比特币每日交易量的信号图。交易量的值为 24.82，价格为 723.31。最高的波数超过 350 K。

#### 交易

交易指的是需要作为一个单独动作来处理的一组逻辑行动。交易请求可以成功执行或失败。该过程将确保系统中的数据完整性。在区块链中，交易是构建区块的基本元素。交易数据可以包括资产、价格、时间戳和用户账户地址。

既然我们已经了解了区块结构中的组件，那就让我们来看看区块链如何处理用户提交的交易请求。Alice 想要将五个比特币（BTC）发送到区块链网络；为了加入这个网络，Alice 和 Bob 都需要有一个账户地址。当 Alice 向 Bob 发送五个 BTC 时，交易请求将在区块链上进行处理：

1.  1.

    Alice 从她的地址向 Bob 的比特币地址发送了五个比特币。创建了一个交易请求并得到验证（由 Alice 钱包的私钥签名）。

1.  2.

    创建了一个包括这个新交易的新区块。

1.  3.

    新的区块广播到网络中的每个节点。

1.  4.

    每个节点都验证并批准新的区块交易数据。收到交易的节点将使用区块链共识验证交易数据。

1.  5.

    新的区块被永久性地添加到现有区块链的末尾。

1.  6.

    所有节点更新并包含这个新区块。

1.  7.

    交易现在已经完成。图 1-9 描述了交易过程中的每个步骤。![](img/535492_1_En_1_Fig9_HTML.png)

区块交易过程的链路图。标签部分包括 Alice 向 Bob 发送交易请求、新的区块广播到网络中的每个节点，以及所有节点更新并包含这个新区块。

图 1-9

区块交易过程

## 共识算法

共识算法通过帮助网络中的所有节点就链中的全局状态达成必要的一致意见，成为区块链的基石。共识验证交易或数据，然后将其广播到网络中。所有其他节点将接收到数据的副本，并通过使用相同的规则验证将其添加到新区块中。

分布式共识协议的一些重要特性包括：

+   **容错性**——共识协议将确保网络在出现任何故障的情况下继续顺畅运行。

+   **统一协议**——由于区块链本质上是去中心化的，网络中的每一笔交易数据都需要通过共识规则进行验证和验证。共识协议要求网络参与者之间达成统一协议，确保处理的所有数据都是有效的，并且分布式账本是最新的。这样，网络才能可靠，用户才能以去中心化方式操作。

+   **确保公平和公正**——该协议不会在去中心化网络中延续偏见或歧视。任何人将能够访问并加入网络，并参加共识协议，每一票都将是平等的。

+   **防止双重支付**——只有经过公开验证和验证的交易才能添加到区块链账本中。所有节点将同意单一的真实来源。这保证了网络中不同的节点具有相同的最终结果。

每种共识算法都具有不同的特性和属性，以实现期望的结果。在我们刚刚介绍的区块链共识属性基础知识上，让我们更深入地了解当前市场上流行的区块链共识算法。

### 工作量证明（PoW）

工作量证明，也称为 PoW，是区块链和加密货币（如比特币、以太坊、比特币现金、ZCash、Litecoin 等）最常用的共识算法之一。

这个概念最早是由 Cynthia Dwork 和 Moni Naor 在 1993 年发表的。术语“工作量证明”或 POW 是由 Markus Jakobsson 和 Ari Juels 在 1999 年的论文中使用的。第一个加密货币，比特币，是由 Satoshi Nakamoto 在 2008 年创造的。这是首次在区块链中使用工作量证明协议作为共识。

工作量证明描述了一种机制，在该机制中，网络中的计算机（称为矿工）相互竞争，争相第一个解决复杂的数学难题。当矿工解决这个“难题”时，他们被允许将新区块添加到区块链上并获得奖励。

在“区块链如何工作”一节中，我们讨论了所有区块通过前一个区块哈希连接起来形成一个区块列表。矿工需要解决异常困难的数学问题才能添加一个新的区块。为了找到一个解决方案，矿工必须使用暴力破解方法猜测一个随机数（即 nonce），直到他们找到解决方案。nonce 是一个 32 位（4 字节）的字段。每个区块的哈希值是通过 SHA-256（前一个区块哈希）、梅克尔根、时间戳、nonce 以及难度目标的预定义值生成的。难度目标由哈希前的零位表示。哈希前的零位越多，整个过程需要的时间和资源就越多。随着计算机能力的增强，矿工可以更快地解决这些难题，因此区块链的难度目标也会相应增加。图 1-10 描述了如何计算工作量证明中的区块哈希。![](img/535492_1_En_1_Fig10_HTML.jpg)

一种算法展示了工作量证明中的哈希。标签部分包括随机数（nonce）、时间戳、前一个区块哈希、梅克尔根、哈希以及带有难度目标的哈希，

图 1-10

工作量证明中的哈希

以下是一个最近比特币难度的例子（有 19 个前导零）：

0000000000000000000469f80aeb7bac1b440652a9ef729658c1010d23962a1cdi

强大的挖矿机器大约需要十分钟来挖出一个比特币区块。单人矿工在成功挖矿后可以获得大约 1 个比特币的奖励。

如我们之前所学的，SHA-256 哈希函数是一种单向函数，这意味着没有办法恢复原始值。我们所知的最快解决方案是暴力破解。矿工需要尝试不同的 nonce 值，尽可能快地计算哈希，直到找到匹配的哈希。

工作量证明的过程如下：

1.  1.

    新交易广播到所有节点。

1.  2.

    每个节点收集交易，形成一个候选区块。

1.  3.

    矿工验证交易，并提出一个新的区块。

1.  4.

    矿工竞争解决难题，为其区块找到工作量证明的解决方案。

1.  5.

    当矿工找到一个解决方案时，工作量证明被解决，并广播到所有节点。

1.  6.

    节点验证新区块中的交易是否有效，并接受添加新区块。

1.  7.

    矿工获得奖励。

图 1-11 形象地展示了工作量证明的过程：![](img/535492_1_En_1_Fig11_HTML.png)

一个流程图展示了工作共识的过程。标签包括新交易广播到所有节点、矿工验证交易及新区块的目的，以及矿工获得奖励。

图 1-11

工作量证明的过程

#### 能量消耗

在 2008 年，你可以轻松地用个人计算机挖出一个比特币。如今，你需要大约 149.2PH/s 的计算能力来挖出一个比特币。PH 是千万亿次哈希：

1 PH/s = 1,000,000,000,000,000（一万亿）每秒哈希次数

这个过程通常需要一个装满挖矿机器的房间，这些机器通常需要数千美元，专门设计以提高哈希率评分和优化电力消耗。需要大量的电力来持续运行这些挖矿节点。2022 年，全球比特币挖矿占世界能源生产的 0.12%（188 TW/h，太瓦时）——这超过了挪威的能源消耗。

#### 51%问题

为了将区块添加到网络，工作量证明（Proof of Work，PoW）需要足够的计算能力来解决一个谜题。要想篡改一个交易的哈希值，攻击者需要控制至少网络 51%的挖矿能力（算力）。这代价昂贵，所以一个人不可能攻击一个网络。

表 1-3 1-3 显示了比特币和以太坊的 PoW 51%攻击成本：表 1-3

PoW 51%攻击的成本

| 名称 | 哈希率 | 1 小时攻击成本 |
| --- | --- | --- |
| --- | --- | --- |
| 比特币 | 33,511 PH/s | 5.83 万美元 |
| 以太坊 | 216 PH/s | 3.64 万美元 |

然而，如果一群有影响力的矿工相互合作并控制这个多数，他们最终可以控制整个网络并决定哪些交易可以添加到网络。这被称为 51%攻击。

由于这些缺点，这些年提出了许多其他新的共识机制，其中最受欢迎的是权益证明（PoS）。

### 权益证明（Proof of Stake，PoS）

工作量证明是一种*验证竞赛*的方法，矿工通过解决加密谜题来验证交易并获得奖励。在这个过程中，工作量证明计算消耗了大量的能量。矿工用能量换取利润。可以把它看作是“一 CPU，一票”。

权益证明（PoS）机制试图通过用质押代替计算能力来减少可扩展性和环境可持续性的问题。可扩展性指的是能够处理更多用户和应用程序增加请求的区块链网络。权益证明与工作量证明的挖矿功能相似。矿工为他们想要验证区块的加密货币作为抵押。这些矿工变成了“验证者”。PoS 算法选择验证者验证新交易并将它们添加到区块链，验证者以加密货币作为回报。矿工质押的加密货币越多，节点被选中参与网络验证的机会就越大。

为解决区块交易验证，计算只依赖于节点拥有的加密货币的质押量。我们可以简化为“一币一票”。

网络将随机选择一些验证者并要求他们提供“正确”的交易。

在验证节点中作为输入的未经验证交易满足以下条件：

哈希(s, c) ≤ N 币* T 币

N 币是节点中的当前质押币金额

T 币是币的时间积累

Ncoin* Tcoin 表示节点的币龄，币龄越大，在同一难度级别下满足条件的几率就越大。

PoS 最早是在 2011 年 7 月 11 日提出的，当时 QuantumMechanic 在 BitcoinTalk 在线论坛上提出了这个概念。Sunny King 和 Scott Nadal 在 2012 年首次发表了这篇论文。

以下是权益证明的过程：

1.  1.

    矿工作为“验证者”，锁定一定数量的加密货币或代币。

1.  2.

    网络运行协议公式 f(x)以选择验证者。

1.  3.

    选定的矿工验证交易并提出新块。

1.  4.

    矿工将新块广播给所有节点。

1.  5.节点证明新块：

    1.  a.

        如果块有效，则将新块添加到网络。矿工获得奖励。

    1.  b.

        如果块无效，节点再次投票新块。矿工失去抵押的硬币。

图 1-12 可视化了权益证明的过程。![](img/535492_1_En_1_Fig12_HTML.png)

权益证明的工作流程图。标签包括矿工抵押他们的硬币，声明为验证者，矿工获得奖励，矿工失去抵押的硬币，以及至少新的块节点。

图 1-12

权益证明的过程

作为最常用的共识机制之一，PoS 被许多加密货币采用。以下是支持权益证明币的流行加密货币列表。

1.  1.

    ETH 2.0

    Ethereum 2.0 将当前基于 PoW 的 Ethereum 区块链 1.0 切换到 PoS。此外，Beacon Chain 将 PoS 带到 Ethereum 2.0。

1.  2.

    Cardano

    2017 年创建的 Cardano，基于权益证明 Ouroboros 共识协议运行。Cardano 中的加密货币代币称为 ADA。

1.  3.

    雪崩

    雪崩是基于 PoS 最快的智能合约平台之一。

    雪崩是一个基于 PoS 的区块链平台，其原生代币为 AVAX。

1.  4.

    Polygon

    Polygon，前身为 Matic Network，是一个“层二”或“侧链”扩展解决方案的区块链网络。Polygon 中的加密货币代币称为 Matic。

## 货币系统的演变

货币是生活的中心部分之一，许多日常生活活动都依赖于它。你可以给出货币，作为回报，你可以获得食物、玩具、衣服、电脑、汽车、医疗保健和其他服务。货币通常用于市场上的商品和服务购买，但有时，人们可能会不使用货币直接以物易物。例如，1984 年 8 月，沙特阿拉伯用 10 亿美元的石油换取了 10 架波音 747 客机给其国家航空公司。这种贸易称为直接交换或物物交换。

### 物物交换系统

物物交换是一种古老的交换方式，该系统可以追溯到公元前 6000 年，甚至早于货币的发明。美索不达米亚人引入了这一系统，腓尼基人采用了它。后来，巴比伦人通过用罗马士兵的盐作为工资来改善他们的物物交换系统，因为盐非常珍贵。许多东西都可以用于交易，包括食物、茶叶、武器、香料和工具。

物物交换系统曾支持早期经济数千年，但它可能效率低下，并不总是运作良好。

+   时间

-   例如，如果一个人手里有小麦，想要用它来换取布料，那么这个人不仅得找到拥有布料的人，还得让双方都同意小麦换布料是一项公平的交易。如果做不到这一点，这个人可能得等待，或者找到其他人，直到有人接受这些条件。这些安排需要时间。

+   不可分割的商品

许多商品无法在不失去价值的情况下进行分割。假设布料的价格等于五个鸡蛋，如果一个人只有四个鸡蛋，布料需要分成或剪成几块才能完成交易。但布料会失去部分价值。

+   缺乏标准单位

-   在物物交换系统中，缺乏一个共同的度量单位，所以每一次交易都需要讨价还价。这既耗时又低效。比如，需要多少个鸡蛋才能换得一块布料？鸡蛋的大小又如何？布料是新的吗？所有这些因素两边可能都不会平等看待。

+   延期支付的难度（未来支付）

有些商品是时间敏感的。例如，一个渔民想用新鲜海鲜换取小麦，但农民几周后才能提供小麦。随着时间的推移，鱼的价值会降低，所以未来不可能进行这种交换。

+   价值的运输难度

运输大量精致或贵重物品和动物到远距离市场进行交换是有风险的。

+   大宗或非常昂贵商品的储存难度

-   在物物交换系统中，有些商品需要额外的购买来储存，比如牛、猪、羊等。

### 商品货币

盐逐渐成为一种流行的支付方式，并被社会接受。由于多年来对盐支付的信任建立起来，所有者可以随时用盐交换许多其他有用的商品。单词“salary”（薪水）来自拉丁语单词“salarium”，意为“盐钱”。

当一种商品成为买卖商品和服务的流行媒介时，它受到信任并具有内在价值。这种商品成为一种称为“商品货币”的货币形式。历史上，许多物品曾被用作商品货币，如盐、烟草、牲畜、贝壳、珍贵宝石和谷物。

位于太平洋中部群岛的雅普岛有一种非常奇特的巨石货币，称为“Rai”。雅普人将石头制成带有中间孔洞的圆盘形状，以帮助运输。石头的价值由其稀有性和将新石头运到岛屿的成本决定。有时在交易结束后石头不需要移动；人们只需要转移石头的所有权。直到 20 世纪 60 年代，它一直被用作日常交易的货币。

以下是商品货币的其他几个例子：

烟草叶：

在整个 17 世纪，弗吉尼亚、马里兰和北卡罗来纳州将烟草作为官方的货币，用于税收和贸易以及其他所有交易。

牲畜：

从公元前 9000 年到公元前 6000 年，最古老的货币形式包括牛、骆驼、羊和其他牲畜。在古代，牲畜可以相对容易地作为商品货币运输。

尽管商品货币在古代极大地促进了商品和服务的流动，但人们很快在这种货币形式上遇到了困难：

+   无法分割的商品：

有些商品货币难以根据个人需求进行分割或分成更小的单位。例如，牲畜和海贝壳不能分成小块用于日常购买。

+   易腐性：

在易腐商品的情况下，保持商品的价值是困难的。

当人们使用牲畜作为商品货币时，这些动物在运输过程中可能会生病、受伤，甚至死亡。长期储存后，商品食品会失去其价值。

+   便携性不足：

有些商品，如雅普石头，从一地转移到另一地是困难的。

+   没有普遍接受性：

商品在各地区之间没有标准化。这使得不同商品交易时定价变得困难。

但是，与物物交换一样，为了克服这些困难，人们转向了金属货币作为另一种货币。

#### 金属货币

Lydia 王国（现今土耳其的一部分）在公元前 700 年左右铸造了第一批金币和银币。这些硬币的重量接近美国的五美分。一个士兵的薪水大约是每月三枚硬币。 Lydia 币是第一次由中央政府发行的货币概念。 Lydian 币通常由金、银或 electrum（黄金和银的混合物）制成，并刻有神和皇帝的图案。

由于硬币有标准的质量和大小，它们变得更容易携带和交换。此外，与商品货币相比，金属硬币要耐用得多。如果你记得并将其熔化来制造工具、武器和新硬币，金属是可分和可替代的。一枚硬币可以保持很长时间的价值，并且难以伪造。

金属货币已成为人类有记录的货币历史中的主要货币形式。每枚硬币都有自己的设计价值和大小。当处理少量交易时，它很容易使用。然而，一旦人们需要长途旅行或进行大量交易，兑换就变得复杂了。携带大量硬币既不安全也不方便。

由于金属的稀缺性，硬币的供应是有限的。需要大量的工作来周期性地获取更多的金属，以满足快速增长的经济发展。

在古希腊和罗马帝国时期，大部分的硬币是由金、银和 electrum 制成，但也有少量的硬币是由铜、青铜和合金制成。这些小硬币通常用于小额交易，其中硬币的价值低于其面值。这引发了代币货币的原则。

穆罕默德·宾·图格勒克（Mohammad Bin Tughlaq）在 1324 年至 1351 年 AD 期间统治着印度次大陆和德干地区的北部。在此期间，黄金和银币出现短缺。但穆罕默德·宾·图格勒克很好地理解了代币货币的性质，发行了一种名为坦卡（Tanka）的铜币，这是世界上第一种代币货币。坦卡的价值等于一枚银币。

几个世纪以来，大多数国家使用金、银和其他更便宜的铜、锌和镍铸造硬币。硬币的价值逐渐与其金属独立，更多地由其标记价值表示。这种演变导致了纸币的发明，标志着货币发展的重要阶段。

### 纸币

金属货币的主要问题在于，在进行与商家的大额交易或长途旅行时，它极其不便。为了克服这个问题，中国人开始在公元前 118 年使用第一张纸币——"飞钱"来换取商品和服务。人们可以用纸币作为信用证，并将其远距离转让。纸币的成功导致了纸币货币的开始。

宋朝在 1023 年发行了第一张真正的纸币，当时宋真宗建立了兑换局。该局印刷并发行了通用的纸币，与商人流通。

纸币可以用作商品、服务或劳动的收据，服务完成后可以兑换。

纸币是由政府发行和背书的法定货币，而不是传统的商品，如金或银。这是世界上第一种法定货币（拉丁语：fiat，“使其成为现实”）。

作为欧洲第一个采用纸币的国家，瑞典的第一家银行斯德哥尔摩银行在 1661 年发行了瑞典纸币。这些银行券作为银行存款证明。由于纸币比金属货币更容易制造，更轻，携带更方便，银行券很快变得流行起来。到 1600 年，全世界的政府和银行都开始向其社会发行纸币。

制造金属硬币需要原材料、精炼、熔化、铸造等多个工序，直到它们可以被压制和分发。与金属货币相比，纸币可以通过 Bureau 更快地印刷，总供应量不会受到金属数量的限制。

在当今世界，纸币在我们日常生活中无处不在。它有不可否认的好处；但是，与其他货币一样，现金也有一些缺点。

使用现金的一个缺点是，你总是需要携带现金。当你购买昂贵商品时，你需要从一地携带大量纸币到另一地。

第二个缺点是，当你丢失钱包时，你可能会丢失现金——或者它被偷了。没有办法保证现金可以归还。交易完成后，你才会交出现金，所以如果交换的商品有问题时，没有办法保证钱可以退还。

纸币的这些缺点导致了银行发明了像信用卡这样的塑料货币，这在今天的支付中越来越受欢迎。

### 塑料货币

随着互联网和计算机技术的发展，交易不仅可以在线下发生，也可以在线上进行，且速度更快、更便捷。如今，万事达卡、维萨卡、美国运通卡和发现卡等信用卡公司在全球范围内是最为广泛接受的支付方式。

约翰·比格斯，一位在布鲁克林为弗拉特布什国民银行工作的银行家，在 1946 年发明了第一张信用卡。这张银行卡被称为“Charg-It”卡。

Charge-It 卡只在离他银行两街范围内的当地商家有效。持卡人在弗拉特布什国民银行有账户。银行在审查持卡人购物的账单后，而不是让持卡人直接支付商家。目标是吸引更多忠实客户到银行。这种概念使客户可以在未来支付的基础上先购买产品。

1950 年，Diners Club 创建了第一张多功能信用卡，允许消费者在各种商家使用。

1958 年，美国运通在美国和加拿大推出了其第一张信用卡——美国运通紫卡。这是我们所知的第一张塑料信用卡。

同年，美国银行推出了其第一个全国性授权的信用卡计划，并将其命名为 BankAmericard。美国银行通过邮件发送信用卡，并将其“投递”到邮箱中，这种做法至今仍在进行。

1960 年，IBM 发明了信用卡背面的磁条。磁条包含了嵌入的持卡人信息，包括持卡人姓名、卡到期日期和账户号码。

1966 年，加利福尼亚州的几家银行决定联合起来成立一个新的银行协会——银行卡协会（ICA），并推出万事达卡。

1976 年，BankAmericard 在全球范围内扩展，最终被称为维萨。

在 1986 年，西尔斯推出了其首次信用卡计划，提供“现金返还”奖励计划，同时销售店内更多产品。这种信用卡被称为发现卡。

图 1-13 展示了塑料货币历史。![](img/535492_1_En_1_Fig13_HTML.png)

一个流程图展示了塑料货币历史。标记的流程是第一张信用卡，第一张多功能计费卡，美国运通，银行美国卡，IBM 磁条，万事达卡，维萨卡，和发现卡。

图 1-13

塑料货币历史

信用卡逐渐但肯定地改变了我们对“信贷”和货币的使用和思考方式。

人们将现金存入银行账户，并使用信用卡（信贷资金或银行资金）进行日常购物。它执行与纸币相同的职能。塑料货币大幅减少了携带现金的需求，并带来了越来越多复杂的现代支付系统。

### 移动支付

1991 年 8 月 6 日，伯纳斯-李从瑞士阿尔卑斯山的一个实验室推出了世界上第一个网站。今天，在其创建二十多年后，存在的网站数量接近 19 亿。自那时以来，电子商务在过去几十年中迅速发展。

1994 年 8 月 11 日，世界上第一次在线购买发生，通过必胜客订购了辣味香肠和蘑菇披萨。维萨处理了有史以来的第一笔在线支付。

在 1995 年，亚马逊推出了其在线书店，成为首批电子商务网站之一。

1998 年，Paypal 推出了第一个金钱转账工具，被认为是第一个数字钱包，允许客户进行安全的在线支付。

1999 年，爱立信和 Telenor Mobil 推出了第一个用于通过手机购买电影票的移动钱包。

2003 年，全球 9500 万移动用户通过手机进行了购买。

在 2007 年，iPhone 和安卓移动操作系统发布。

到 2022 年，大约有 72.6 亿人拥有智能手机，占世界人口的 91.54%。79%的智能手机用户在过去六个月内进行了移动支付。

图 1-14 描述了移动支付历史。![](img/535492_1_En_1_Fig14_HTML.png)

移动支付历史的流程图。标签流程是第一个移动，在线移动，亚马逊推出，PayPal 推出，第一个移动钱包，9500 万移动购买，iPhone &安卓操作系统，以及 72.6 亿移动用户。

图 1-14

移动支付历史

一些值得注意的移动钱包包括苹果支付、亚马逊支付、谷歌支付、Venmo、PayPal、微信支付、Zelle 和 Square。

#### 移动支付类型

市场上可用的移动支付类型有很多，包括以下几种。

近场通信（NFC）是允许移动设备通过私有频道安全连接的技术。它通常要求设备彼此之间的距离很短（4 厘米或更短）以启动连接。

移动设备通过 NFC 标签连接到使用 NFC 的商家。客户需要激活 NFC 以开始一对一的互动。

**二维码支付**

快速响应码，或二维码，是一种二维条形码。它编码信息，以便产品可以现场购买。信息可以被数字设备，如手机读取。

许多移动钱包支持二维码支付，如 PayPal、Zelle、Square 和 Venmo。

**基于云的移动支付**

Google、Amazon、GlobalPay 和 GoPago 采用基于云的方法处理店内移动支付。它允许消费者使用近场通信（NFC）购买产品的同时，将移动支付提供商置于交易中间。

移动支付仍然存在许多问题，以下是一些例子：

**数据隐私**

当我们使用移动支付应用购买东西时，商家和用户并不是交易中唯一的参与者。还有其他隐藏的供应商或中间商成为交易的一部分。每个参与方都会在其数据库中记录交易以用于业务。供应商可以使用收集到的数据来研究用户行为并针对他们投放广告。

**隐藏费用**

大多数移动支付选项都与信用卡和借记卡绑定。Visa 的数字钱包对信用卡支付收取相同的费用。但 PayPal、Venmo 和其他许多支付供应商收取的费用比大型银行的平均费用还要高。以下是一些常见的隐藏费用：平衡转账费、跨境交易费、不活动费、滞纳金等。

**钱包控制**

即使你有自己的支付账户，你也没有完全控制权。在某些情况下，支付发行商可能会暂时冻结用户账户并限制借款能力。

使用移动支付有很多优点，但货币仍在不断进化。图 1-15 展示了货币系统的演变。![](img/535492_1_En_1_Fig15_HTML.png)

货币系统演化的流程图。标签流是实物交易系统、商品货币、金属币、纸币、塑料币、移动支付和加密货币。

图 1-15

货币系统演变

在移动支付中，所有的钱都是电子存储在电子系统或数字数据库中。因此，我们通常广泛地称其为电子货币，电子货币。电子货币可以用于有或没有银行账户的电子支付交易。

电子货币有两种系统：集中式系统和去中心化系统。这两种系统之间的主要区别是去中心化数字货币，也称为加密货币，是去中心化系统中的原生货币。没有集中的当局发行这种货币，加密货币是由区块链网络中的计算机协议定义和生成的。我们将在下一节中讨论更多内容。

## 理解加密货币

在集中货币系统中，数字货币由某些中央银行支持。人们认为他们的货币有价值，是因为他们信任政府发行这种货币。加密货币（或“加密”）是去中心化的数字货币，旨在作为区块链交易的媒介，对公众透明，并且抗审查。与集中货币不同，加密不依赖于发行货币的中央货币当局，如政府或银行。加密货币依赖于现代密码学来验证区块链上的交易，发行货币单位，保护用户账户和确保账本数据安全。

第一种去中心化加密货币是比特币。它是在 2008 年由中本聪发明的，并于 2009 年推出。比特币是所有加密货币的母币，至今仍是最有价值和最受欢迎的加密货币。在 2022 年的加密货币市值中，比特币占据了所有加密货币的 47%市场份额。

### 加密货币市场

自 2008 年比特币推出以来，加密货币已经彻底改变了整个金融世界。加密货币的总数迅速 proliferation。截至目前，大约有 20,000 种加密货币，总市值接近 1.2 万亿美元。每 24 小时，有价值约 680 亿美元的加密货币被交易。全球有 500 多个加密货币交易所。

根据区块链.com，在撰写本文时，比特币的日交易量约为 270K/天。!

分析报告描绘了 2021 年 11 月 23 日至 2022 年 11 月 22 日区块链点 com 上确认的比特币交易数量。每天的确认交易量为 2,53,235，日交易量约为 270k。

图 1-16

比特币每天的确认交易数量（blockchain.com）

根据 statista.com，2009 年 1 月到 2021 年 11 月 7 日，比特币、以太坊和其他 13 种加密货币的区块链上的每日交易量如图 1-17 所示。!

从 2009 年到 2021 年的每年交易量与颜色编码曲线的图表代表了 16 个过程。最高的波浪水平在 7500.000 以上。

图 1-17

加密货币的每日交易量（statista.com）

比特币每天的交易量为 260,000 次。

以太坊每天处理超过 110 万次。

Ripple 每天处理 140 万笔。

Stella 每天处理 880 万笔。

信用卡公司每天处理大约 1 亿笔交易。加密货币要想达到这样的日交易量还有很长的路要走。但大约五分之一的美国人已经使用过、投资过或交易过加密货币，这是加密货币尽管相对最近才出现，但仍然快速增长并越来越受欢迎的另一个迹象。

2014 年，一家大型在线零售商 Overstock 开始接受比特币作为其网站购物的支付方式。同年，微软成为首批采用加密货币作为游戏、应用程序和其他产品支付方式的大型科技公司之一。

主要移动运营商 AT&T 通过 BitPay 接受在线加密货币支付，为客户服务。特斯拉在其网站上接受比特币和狗狗币支付一些商品。

即使在美国就有超过三分之一的的小企业和许多大型公司接受加密货币作为支付方式，其受欢迎程度仍在增长。现在，你可以用比特币购买许多东西，其中一些包括：

汽车、移动通信和电视服务、家具、电影和活动的门票、食品、艺术和收藏品、房地产、旅行和慈善。

随着加密货币采用率的提高，区块链交易量将继续增长。

### 什么是加密货币波动性？

金融市场的波动性是资产价格在特定期间内增加或减少的速度。它是理解、管理和量化投资风险的重要指标。通常，高波动性指的是价格快速波动，低波动性指的是价格在小范围内缓慢变化，意味着价格相对稳定。

高波动性通常意味着更高的风险但也可能带来更高的回报。而低波动性通常意味着较低的风险和回报，但并非总是如此。低波动性的一个例子是政府债券，它们由政府的信用完全支持，市场通常认为其风险较低。黄金是另一个例子，因为它在很长时间内价格稳定。图 1-18 展示了高波动性和低波动性。![](img/535492_1_En_1_Fig18_HTML.jpg)

高波动性时间和价格的高波动性用较粗的锯齿线表示，低波动性时间和价格的低波动性用较细的锯齿线表示。

图 1-18

高波动性和低波动性

许多人听说过加密货币市场的高波动性。一些加密货币的价格在很短的时间内可能会损失 90%的价值。让我们看几个例子。

市场调整通常指的是从近期高点值下跌 10%到 20%。表 1-4 列出了 2013 年 11 月至 2020 年 3 月比特币调整的历史。对于加密市场的新手来说，加密市场崩盘可能相当可怕。然而，对于了解比特币历史的人来说，这种市场调整并不新鲜。尽管这些跌幅使人们对比特币不稳定价格感到相当沮丧，但价格从 2010 年的 0.0008 美元开始，到 2022 年 6 月增加到 2.5 万美元。表 1-4

比特币调整历史

| 日期 | 价格 | 跌幅 |
| --- | --- | --- |
| - | - | - |
| 2013 年 11 月 30 日至 2016 年 1 月 14 日 | 1163 - 152 | -86.9% |
| 2017 年 3 月 10 日至 25 日 | 1350–$891 | -34.0% |
| 2017 年 5 月 25 日至 27 日 |
| 2017 年 6 月 12 日至 7 月 17 日 | 2980–1830 | -38.6% |
| 2017 年 9 月 2 日至 15 日 | 4980–$2972 | -40.3% |
| 2017 年 11 月 8 日至 12 日 | 7888– $5555 | -29.6% |
| 2017 年 12 月 17 日至 2018 年 12 月 15 日 | 19666–$3220 | -83.6% |
| 2019 年 6 月 26 日至 2020 年 3 月 12 日 | 12867– $5040 | -60.8% |

Luna（也称为 Terra）是原始 Terra 区块链的本地代币，于 2018 年推出。当时，代币的名字是 LUNA。Luna 是由韩国公司 Terraform Labs 在 2018 年开发的区块链。该区块链旨在改变现代金融体系。

2020 年，Luna 开始销售名为 TerraUSD 的稳定币。Luna 是市值前十的主要加密货币之一。但是，根据 CoinMarketCap 的数据，2022 年 5 月 11 日，LUNA 在 24 小时内下跌到原价的 2%，LUNA 价格从 32.71 美元跌至 0.08384 美元。![](img/535492_1_En_1_Fig19_HTML.jpg)

以下是 Luna 市场价格波动的说明，从 190.52719716，119.2518039，46.12450969，0.80000000 和 0.00007500 的价值下跌。

图 1-19

加密货币市场的波动性——Luna

StepN 是一个基于步数的健身应用，引入了一种新的 Web3 生活方式应用。用户必须购买 NFT 运动鞋才能玩游戏。STEPN 使用 GST（绿色比特币代币），这是一种基于 Solana 区块链的代币。用户可以通过户外步行或跑步使用移动 GPS 服务追踪用户动作，或者通过“出租”他们的 NFT 运动鞋给其他用户来赚取 GST。一些运动鞋在 NFT 市场上的价值高达数千美元。StepN 是由 FindSatoshi Lab 于 2021 年 12 月推出的。这个创新解决方案使 STEPN 能够迅速颠覆健身行业，并吸引市场的广泛关注。

加密市场于 2022 年 3 月 9 日开始列出 GMT(STEPN)。起初的价格是 0.01 美元。到了 4 月 28 日，价格飙升到 4.03 美元——仅 51 天就增长了 40200%（数据来自 coinmarketcap）。但是整个加密市场下跌后，6 月份的价格下跌至 0.6317 美元。图 1-20 显示了加密货币市场的波动性——STEPN。该图表来自 CoinGecko。![](img/535492_1_En_1_Fig20_HTML.png)

来自 CoinGecko 的加密货币市场波动性示意图。5 月 2 日最高波浪水平超过 5400。

图 1-20

加密货币市场的波动性——Stepn（来自 CoinGecko）

#### 什么可能导致加密货币市场的高波动性？

有多个因素可能导致高度波动和不稳定的环境。让我们探索这些因素。

#### 新兴市场

与互联网的历史相比，加密货币仍处于非常早期的阶段——自加密货币出现以来，至今只有十年。在这段时间内，加密货币市场呈指数级增长。

全球加密货币市值达到约 1.25 万亿美元，而 2021 年全球股市市值为 121 万亿美元。与全球股市相比，加密货币市场仍然相对较小，任何新兴市场都会伴随波动。即使在互联网股票的早期阶段，也存在高波动性，如同今天的加密货币市场。

加密货币仍然需要很长时间才能大规模采用。与股票、法定货币和其他传统金融产品不同，该行业仍在研究、理解和开发一个可靠的模型，以确定加密货币的基本价值。这意味着在当前市场中没有可靠的预测加密货币价格的产品。

#### 新技术

在之前的 LUNA 示例中，LUNA 发明了 TerraUSD（UST）的概念。一种稳定币由 Terra 算法控制，作为法定货币发挥作用，类似于美元。它的目标是将美元与***1:1***的比例挂钩，但与其它主要稳定币不同的是，UST 没有完全抵押。LUNA 还允许持有者对协议进行投票。该协议如预期般运作，直到出现可扩展性问题。如果用户在市场下跌时返回 UST，LUNA 协议需要通过向用户发行更多的 UST 代币来将 UST 带回到 1 美元。这使得 LUNA 的总代币供应量从 5 月 5 日的约 7.25 亿激增至 5 月 13 日的约 7 万亿美元。稳定币的 1:1 比例已无法维持。它从 1 美元跌至 0.009 美元。

#### 去中心化

加密货币，如比特币，是区块链网络的原生资产。与黄金这种真实物理世界的有形资产相比，加密货币更像是一种“价值储存手段”。它没有任何实体商品或中央货币的支持，只存在于虚拟世界中，因此没有内在价值。价格由市场需求决定，但许多因素可能导致价格波动。

#### 情绪

市场情绪，也称为投资者关注度，是指投资者对特定资产价格预测的整体感觉。许多因素都可能影响加密货币的投资者关注度，可能引发一段显著的波动期。以下是其中几个因素：

治理、法规、供需、安全漏洞、竞争等。

加密价格的波动和难以预测可能会让人感到沮丧，因此管理风险、在各种不同的加密资产中分散投资、进行研究和技术分析、投资你能够承受的金额，并长期持有等方面尤为重要。

### 硬币与代币的区别

有一个常见的误解是代币和硬币是同一事物。

在货币系统的演变部分，我们知道金属硬币是由黄金或银制成，以代表其内在价值。莫卧儿·本·图格勒克发明了代币货币——坦卡，它使用铜币代表与银币相等的价值。

在区块链中，代币和硬币都代表了一种价值储存，并可用于处理支付。但它们之间有一些区别：加密硬币是区块链的本地资产，由区块链共识协议生成。例如，比特币网络中的比特币和以太坊网络中的以太币都是硬币。

加密代币建立在区块链网络之上，由智能合约（在网络上运行的自我执行程序）创建。在创建代币时，代币的创建数量可以由智能合约定义。

表 1-5 展示了硬币和代币之间的区别。表 1-5

比较硬币和代币

| 硬币 | 代币 |
| --- | --- |
| 硬币是一种独立的数字货币，是其自身区块链的本地代币，由网络共识验证。硬币与法定货币相似。 | 代币的创建需要智能合约来定义代币的基本属性，然后进行构建和运营。 |
| 硬币的数量由区块链共识定义。 | 代币的数量由智能合约定义。智能合约可以定义更多的自定义代币属性，如代币名称、总供应量、某些代币转移规则等。 |
| 硬币的主要用途是执行共识协议来建立区块链网络。硬币可以通过挖矿或转移硬币所有权来分发 | 代币的用途可能更加多样，因为它们的功能是根据每个业务需求定义的 Dapps（去中心化应用）。 |
| 示例：比特币、以太坊、索拉纳、卡尔达诺、狗狗币、莱特币、币安、瑞波币等。 | 示例：安全代币、实用代币、股权代币、ERC-20 代币、NFT 代币等。 |

## 总结

在本章中，我们学习了区块链的主要特征并探讨了去中心化。然后我们详细了解了区块链的工作原理，包括交易过程中的每个步骤。共识算法，如 PoW、PoS，构成了区块链的核心。我们接着继续探讨货币系统的演变，从物物交换到加密货币。最后，我们简要介绍了加密货币，并理解了加密市场的一些基本概念。

在下一章中，我们将继续学习之旅，开始学习密码学——区块链安全的基石。