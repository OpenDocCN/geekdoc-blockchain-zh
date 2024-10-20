# 戴着匕首的 BFT

> 原文：<https://blog.chain.link/bft-on-a-dag/>

## **剧情简介**

新兴的利益相关证明区块链通过以网络能够承载的速度可靠地传播事务并将其累积在 DAG 中来实现高事务吞吐量。然后，参与者在不交换更多消息的情况下在本地解释他们的 DAG，并确定累积事务的总排序。

这篇文章探索了一种简单有效的基于 DAG 的 BFT 共识排序方法——这可能是将 BFT 嵌入 DAG 的最简单的方法。它以逐个视图的方式运行，保证当网络稳定时，只需要两次广播延迟就可以对 DAG 中累积的所有事务达成一致决策。重要的是，DAG 永远不必等待共识协议步骤/定时器来添加事务。

## **简介**

最近的基于 DAG 的系统(见下面的[建议阅读](#suggested-reading))通过将可靠地传播消息的责任和因果排序从共识排序逻辑中分离出来，展示了卓越的性能:

*   DAG 传输负责可靠地传播尚未确认的交易。它调节通信并优化吞吐量，但它仅跟踪 DAG(直接非循环图)形式的因果排序。
*   BFT(拜占庭容错)共识协议负责形成关于事务的串行提交排序的协议。每一方利用其 DAG 的本地副本从 DAG 结构中独立地提取事务的共同排序。

在 DAG 传输上建立共识的出现是 DAG 中的每个消息传播有用的有效载荷(事务或事务引用)。每当一方发送包含事务的消息时，它也无偿地对提交的事务进行总排序。各方可以继续发送消息，并且 DAG 保持增长，即使当共识协议停止时，例如当共识领导者出错时，并且稍后提交 DAG 中累积的消息。此外，DAG 消息的明确属性和它们携带的因果关系信息可以消除一致性协议设计中的许多复杂性。

这篇文章探索了一种简单的方法，在可靠的、因果有序的通信传输上建立共识。这种方法借鉴并建立在许多以前的作品之上(见[建议阅读下面的](#suggested-reading))。然而，它独特地提供了一种极简主义和纯粹主义的方法，强调以下主要原则:

*   **零 DAG 延迟。** 我们的方法提供了一致性排序逻辑与 DAG 传输的清晰分离。Consensus 仅将 DAG 用作“智能内存池”来传播事务和元信息。相比之下，从这里描述的共识方法到像[Bullshark](https://sonnino.com/papers/bullshark.pdf)这样的共识协议的仅仅 [的一个(小)部分](https://arxiv.org/pdf/2209.05633.pdf) ，需要规定一个分层 DAG 结构，在每个 DAG 消息上添加必要数量的前趋，并根据共识步骤/定时器来调节每个 DAG 传输。
*   **简单。** 对于部分同步模型，我们的方法很可能是最简单的基于 DAG 的协议。简而言之，它是一个视图到视图的协议:一个视图的领导者向 DAG 广播一个提议，当这个提议在 DAG 中被足够多的投票通过时，它就被提交。通过提交或广播到 DAG 中的投诉，可以前进到下一个视图。这就是整个协议！
*   ****部分同步。** 该解决方案保证当网络稳定时，只需要两次广播延迟就能达成一致决策。排序决策成批提交 DAG 中累积的所有事务。**

 **![](img/1bebb0d1c0537c0eb4b660a68a95e07f.png)

<figcaption id="caption-attachment-4488" class="wp-caption-text">DAG-based BFT consensus</figcaption>



这篇文章是为了教学目的，而不是作为一个成熟的 BFT 系统设计:我们想要一个简单的，极简主义的方法作为算法的基础，像 [Fino](https://arxiv.org/abs/2208.00940) (未来文章的主题)这样的结构可以建立并证明是正确的。像大多数进步一样，这里描述的方法是站在一个历史悠久的作品的肩膀上的(见下面的[建议阅读](#suggested-reading))。该领域的主要收获是，DAG 上的共识可以同时是简单的和高性能的。 

## 什么是基于 DAG 的 BFT？

在基于 DAG 的 BFT 协议中，各方将通过可靠且因果有序的广播传递的消息存储在本地图中。当消息被插入本地 DAG 时，它具有以下保证:

*   **可靠性:** 消息的副本存储在足够多的参与者身上，这样最终所有诚实的一方都可以下载它
*   **毫不含糊:** 每一方发出的信息都是有编号的。如果一方从特定的发送方发送第 k 条消息，则该消息由其发送方验证，其他方发送与发送方第 k 条消息相同的消息。
*   **因果排序:** 该消息携带对发送者先前传递的消息(包括其自己的)的显式引用。前置任务在消息传递之前在本地传递。

请注意，不同方的 Dag 在任何时刻都可能略有不同。由于消息调度，这在分布式系统中是不可避免的。然而，基于 DAG 的共识协议允许每个参与者解释其本地 DAG，从而得出形成总排序的自主结论。可靠性、明确性和因果性使得这种协议的设计极其简单，正如我们将在下面看到的。

**一条 DAG 消息的生存期。**DAG 传输公开了两个基本的 API， `broadcast()` 和 `deliver()`。

*   **播出。** `broadcast()` 是一个异步 API，用于一方呈现要传输给所有其他方的 DAG 传输的有效载荷。在基于 DAG 的一致性协议中，DAG 消息的主要用途是将关于事务的元信息打包到一个块中，并呈现该块以供广播。DAG 传输将引用添加到先前传递的消息中，并将携带块和因果引用的消息广播给所有各方。
*   **发货。** 当另一方接收到携带该信息块的消息时，它检查是否需要检索该信息块中的任何交易的副本以及之前的消息。一旦它获得块中所有事务的可用性证明及其因果过去，它就可以确认它。当收集到足够多的对一方的确认时，触发该方的向上调用 `deliver(m)` ，保证消息本身、它所涉及的事务以及它的整个因果过去保持可靠性、不含糊和因果排序。

**实现 DAG。** 在 n=3F+1 方之间实现可靠且因果有序的广播有多种方式，其中最多 F 方被假定为拜占庭错误，其余为诚实。

*   **附和。** 可靠性和明确性的关键机制是让各方用特定的索引回显他们从发送方收到的第一条消息的摘要。有两种常见的回声方式，一种是通过认证的点对点信道进行全对全广播，如 [布拉查广播](https://core.ac.uk/download/pdf/82523202.pdf)；另一种是带有加密签名的汇聚-广播，如 [壁垒](https://dl.acm.org/doi/10.1145/191177.191194) 。在这两种情况下，回显都可以简化，因此分摊的每条消息的通信是线性的，这是传播消息所必需的最低要求。
*   **压条。**运输机通常是一层一层地建造的。在这种体制下，每个发送者每层允许一条消息，并且一条消息只能引用它之前的层中的消息。分层是为了调节传输和饱和网络容量，并已被各种项目证明非常有效，包括 [Blockmania](https://arxiv.org/abs/1809.01620) 、 [Aleph](https://arxiv.org/pdf/1908.05156.pdf) 和 [Narwhal](https://arxiv.org/abs/2105.11827) 。我们重申，这里描述的共识协议不需要分层结构。

## **Fino 基于 DAG 的 BFT 共识**

我们通过 [Fino](https://arxiv.org/abs/2208.00940) 的核心，一个为部分同步模型设计的 BFT 共识排序协议嵌入，展示了 DAG 的效用，解决 n=3F+1 方之间的共识，其中 F 可以是拜占庭的。

给定 DAG 传输的强保证，嵌入非常简单，很可能是部分同步模型的最简单的基于 DAG 的一致解决方案。它在一个阶段中操作，并且完全脱离 DAG 事务传播的关键路径。

简而言之，该方法工作如下:

*   **观点。** 协议以一个视图接一个视图的方式运行。每个视图都有编号，如 `view(r)` ，并且有一个大家都知道的指定领导。每个视图由嵌入 DAG 内部的 **【提案】****【投票】** 和 **投诉** 组成。
*   **提议。** 当领导者进入 `view(r)` 时，它广播 `proposal(r)` 。提议就像 DAG 中的任何消息一样，它包含事务元信息和因果前导。每个建议被解释为包括一个 **批次:** 其因果过去的所有事务，包括那些直接包括在建议消息中的、尚未包括在前面的建议中的事务。
*   **投票。**`view(r)`，送完 `proposal(r)` 后，播出一个 `vote(r)`。投票就像 DAG 中的任何消息一样。它被解释为由`proposal(r)``view(r)`中的因果关系进行表决。
*   **投诉。** 来表示 `view(r)` 没有进展，当事人播报 `complaint(r)` 。抱怨过后，一方不能在 `view(r)` 投票。请注意，为了保证稳定状态下的进展，只有在给领导者足够的时间来提议和投票后，才会发出抱怨。
*   **提交。** A **提交** 发生在 `view(r)` 如果有 F+1 票支持领导提案，
*   **下一个视图。** 进入 `view(r+1)` 由提交或 2F+1 投诉使能。

重要的是，提案、投票和投诉随时都会被注入 DAG，独立于各层。同样，协议视图的 **不对应于 DAG 层的** 。该属性是 DAG/共识分离的关键原则，允许 DAG 完全在关键路径之外继续传播具有共识的消息。

由于 DAG 的特性，解决方案非常简单:共识逻辑不需要考虑领导者的模棱两可，因为 DAG 阻止了它。领导者不需要证明其提议是合理的，因为通过该提议在 DAG 中的因果历史，它是内在合理的。在 F+1 次投票或 2F+1 次投诉后，通过前进到下一个视图来控制视图中提交的安全性，保证与 F+1 次提交投票相交。

完整的协议在下面的 [伪代码](#pseudo-code) 中用伪代码描述。接下来提供了一步一步的场景演练。

## **逐场景演练**

**幸福之路场景。**

每一方进入 `view(r)` 都是通过因果跟随一个由 2F+1 的 `view(r-1)` 或 `complaint(r-1)` 消息中的提交。每个 `view(r)` 都有一个预先指定的首领，分别标注为 `leader(r)` ，这是大家都知道的。

第一条 `view(r)` 消息被领导者解释为 `proposal(r)` 。该建议隐式包含一个 **批:** 该建议之前的所有交易(包括其本身)，这些交易尚未包含在之前的批中。

在 [**图 1**](#figure-1) 下面， `leader(r)` 是甲方 1，其第一条消息在 `view(r)` 中用全绿色椭圆形表示，表示是 `proposal(r)` 。

一方发出 `proposal(r)` 后，其建议后的第一条消息解释为 `vote(r)` 。法定人数为 F+1 票的提案被视为 **通过** 。

在 [**图 1**](#figure-1) 下面，党 3 票为 `proposal(r)` ，用一个带条纹的绿色椭圆形表示。 `proposal(r)` 现在已经有了 F+1 票所需的法定人数(包括领袖的隐式投票)，就变成了 committed。 `proposal(r)` 的因果过去的批量交易被追加到已提交交易的共识序列中。

当一方在 `view(r)` 看到 F+1 票就进入 `view(r+1)` 。

![Diagram showing proposals, votes, complaints, and commits.](img/cdee11074338b2766793aa04c8f022f2.png)

<figcaption id="caption-attachment-4489" class="wp-caption-text">**Figure 1:** Proposals, votes, complaints and commits.</figcaption>



![Diagram highlighting complaints.](img/7979b03deda9796a87e6914b89471c2f.png)

<figcaption id="caption-attachment-4490" class="wp-caption-text">**Figure 1b:** The same scenario as above at the DAG level. Messages have Reliability, Non-equivocation and Causality. There is no Consensus context at the transport level (Complaints are marked red indicating they carry extra information in addition to transaction references).</figcaption>



有一个错误领导者的场景。

如果视图的领导者出现故障或断开连接，各方最终会暂停并广播投诉消息。当一方看到 2F+1 对一个视图的抱怨时，它进入下一个视图。

在 [**图 1**](#figure-1) 上面，第一个视图 `view(r)` 正常进行。然而，没有由第二方 `leader(r+1)` 标记为 `view(r+1)` 的消息到达，显示为丢失的椭圆。别担心！如图所示，DAG 传输继续进行，不受领导者故障的影响。因此，错误的观点在传播交易中是有用的。最终，当事人 1、3、4 抱怨 `view(r+1)` ，显示为带条纹的红色椭圆形。收集到 2F+1 投诉后， `view(r+2)` 的首领发布一条消息，该消息被记为 `proposal(r+2)` 。该建议的批处理包含其因果历史中累积的所有消息，所有这些消息都会影响吞吐量。

**慢热领导的场景。** 下面的 [**图 2**](#figure-2) 描述了一个稍微复杂一点的场景。这个场景与上面的相同，但是实际上发出 `proposal(r+1)` 的是 `leader(r+1)` ，表示为全红色椭圆，这对于到达第 1、3 和 4 方来说太慢了。这些当事人抱怨一个视图失败，启用 `view(r+2)` 开始而没有提交 `proposal(r+1)` 。然而， `proposal(r+2)` 因果跟随 `proposal(r+1)` 而当 `proposal(r+2)` 犯时，它间接犯。首先将 `proposal(r+1)` 的因果历史中的批次追加到已提交事务的共识序列中，其次将 `proposal(r+2)`的剩余因果历史追加。

![Diagram showing belated proposal.](img/159374279c912ff0501faa9e95162b33.png)

<figcaption id="caption-attachment-4491" class="wp-caption-text">**Figure 2:** A belated proposal in `view(r+1)` being indirectly committed in `view(r+2)`.</figcaption>



## **在伪代码中**

消息在 deliver(m)中传递，携带发送者的有效载荷和附加元信息，这些信息可以在接收时被检查:

```
 - m.sender, the sender identity 
 - m.index, a delivery index from the sender
 - m.payload, contents such as transaction(s) and BFT protocol meta-information piggybacked on transmissions
  - m.predecessors, references to messages sender has delivered from other parties, including itself
```

p 方对视图(r)进行如下操作:

```
1\. Entering a view. 
 A party enters view(r) if the DAG satisfies one of the following two conditions:
 (i) A commit of proposal(r-1) happens
 (ii) 2F+1 complaint(r-1) messages are delivered
 Initially, view 1 is entered.

2\. Proposing. 
 A message in the DAG is proposal(r) if it is the first broadcast of leader(r) in view(r).

3\. Voting.
 A message in the DAG is vote(r) for the leader’s proposal(r) if:
 (i) It is the first broadcast of party p in view(r) that causally follows proposal(r) or it is proposal(r) itself
 (ii) It does not follow a complaint(r) message by p

4\. Committing. 
 A proposal(r) becomes committed if there are F+1 vote(r) messages in the DAG.
 Upon a commit of proposal(r), a party disarms the view(r) timer. 

4.1\. Ordering commits. 
 If proposal(r) commits, messages are appended to the committed sequence as follows.
 First, among proposal(r)'s causal predecessors, the highest proposal(s) is (recursively) ordered.
 After it, remaining causal predecessors of proposal(r) including the proposal itself, 
     which have not yet been ordered, are appended to the Consensus sequence of committed transactions.
     (Within this batch, ordering can be done using any deterministic rule to linearize the partial ordering into a total ordering.)

5\. Expiring the view timer.
     If the view(r) timer expires, a party broadcasts complaint(r).
```

## **分析**

上面提出的方法最低限度地集成到 DAG 中，简单地解释携带事务引用块的广播，并根据需要呈现广播的视图投诉。重要的是，DAG 广播在任何时候都不会因为共识协议而变慢，也不会等待共识协议。

DAG 的可靠性和因果性使得争论正确性变得非常容易，尽管正确性的正式证明超出了本文的范围。

**安全(草图)。** 如果曾经 `proposal(r)` `成为承诺，那么就是在 F+1 方的因果过去中投票赞成。任何更高视图的建议都必须引用(直接或间接)F+1 `vote(r)` 消息，或 2F+1 `complaint(r)` 消息，其中一个消息跟随一个 `proposal(r)` 。在任一情况下，在这样的未来视图中的提交因果地跟随对 `proposal(r)` 的投票，因此，它(重新)提交它。`

 `反过来说，当 `proposal(r)` 提交时，就可能引起一个建议在下级看来， `proposal(s)` ，其中 `s < r` ，成为第一次提交。安全持有是因为未来提交将以同样的方式递归顺序 `proposal(r)` 及其因果过去。

**同步期间的活性(草图)** 。在 GST(全局稳定时间)之后，即，在通信变得同步之后，视图通过可靠的 DAG 广播固有地同步。因为设δ是 GST 之后 DAG 广播的上界。一旦具有诚实领导者的 `view(r)` 由第一诚实方进入，在δ内，由第一诚实方 p 看到的所有消息都由领导者和所有其他诚实方传递。因此，在δ内，所有诚实的当事人也进入 `view(r)` 。    内加 2δ，把 `view(r)` 的提案和选票从所有诚实的党派中分摊到每个人身上。只要视图计时器设置为至少 3δ，未来视图就不会抢占当前视图的提交。对于为了开始一个未来视图，其领导者必须收集 F+1 `vote(r)` 消息，于是提交`proposal(r)`；或者 2F+1 `complaint(r)` 过期消息，这是不可能如上面所论证的。

我们现在讨论稳定状态下的沟通复杂性，此时领导者是诚实的，与它的沟通是同步的:

*   **DAG 消息开销** :为了使 DAG 消息可靠传递，必须实现可靠广播。这导致每次广播在认证的信道上携带二倍数量的消息，或者二倍数量的签名验证。在这两种情况下，二次成本可以通过流水线来分摊，在实践中使每个消息的二次成本(几乎)成线性。
*   **提交消息开销** :协议发送 O(n)个广播消息，一个提议和每个决定的投票。决策提交提议的因果历史，由(至少)线性数量的消息组成。此外，每个消息可以在其有效负载中携带多个事务。因此，在实践中，提交成本被分摊到许多事务中。
*   **提交延迟**:DAG 消息的提交延迟是 2，一个提议后面跟着投票。

## **基于 DAG 的相关解决方案**

早期基于 DAG 的一致性系统专注于数据中心复制，例如[【Isis】](https://dl.acm.org/doi/10.1145/37499.37515)[Psync](https://dl.acm.org/doi/10.1145/65000.65001)[Trans](https://ieeexplore.ieee.org/document/80121?tp=&signout=success)[Total](https://dl.acm.org/doi/10.1145/327164.327298)和[Transis](https://ieeexplore.ieee.org/document/243613)。[](https://www.sciencedirect.com/science/article/pii/S0890540198927705)和[ToTo](https://dahliamalkhi.github.io/files/Multicast-FTCS1993.pdf)都是前区块链时代的，纯 DAG 总订购协议为异步模式。这些纯 DAG 协议的设计没有调整 DAG 层，也没有注入外部常见的硬币来处理异步。因此，它们都相当复杂，而且收敛缓慢。

Cheriton 和 Skeen[【CATOCS，1993】](https://dl.acm.org/doi/10.1145/173668.168623)【随后是 Birman 的 [【对 CATOCS 的回应 1，1994】](https://dl.acm.org/doi/10.1145/164853.164858)和 Van Renesse 的 [【对 CATOCS 的回应 2，1994】](https://dl.acm.org/doi/10.1145/164853.164859)

最近对缩放区块链的兴趣重新点燃了对基于 DAG 的协议的兴趣。几个区块链项目正在使用基于 DAG 的一致协议高吞吐量地构建，包括 [漩涡散列图](https://www.swirlds.com/downloads/SWIRLDS-TR-2016-01.pdf)[block mania](https://arxiv.org/abs/1809.01620)[Aleph](https://arxiv.org/pdf/1908.05156.pdf)[Narwhal&Tusk](https://arxiv.org/abs/2105.11827)[DAG-rider](https://arxiv.org/abs/2102.08325)

[漩涡状哈希图](https://www.swirlds.com/downloads/SWIRLDS-TR-2016-01.pdf) 是区块链时代唯一的、纯粹的——DAG 解我们的知识。它利用消息中的比特作为伪随机掷硬币，以推动随机共识。

[Narwhal](https://arxiv.org/abs/2105.11827) 是一种具有逐层结构的 DAG 传输，每层对于每个发送者最多有一条消息，并且引用前一层中的 2F+1 条消息。类似的分层 DAG 结构出现在前面的 [Aleph](https://arxiv.org/pdf/1908.05156.pdf) 。

[Narwhal-HS](https://arxiv.org/abs/2105.11827) 是基于[hot stuff](https://dahliamalkhi.github.io/posts/2022/06/dag-bft/)为部分同步模型的 BFT 共识协议，其中 Narwhal 被用作“mempool”。为了推动一致决策，Narwhal-HS 在 Narwhal 之外添加消息，仅使用 DAG 来传播事务。

[DAG-Rider](https://arxiv.org/abs/2102.08325) 和 [Tusk](https://arxiv.org/abs/2105.11827) 为“骑”在 Narwhal 上的异步模型建立随机化的 BFT 共识，这些协议在 DAG 上是“零消息开销”，不交换 Narwhal 协议之外的任何消息。DAG-Rider (Tusk)由专门构建的 DAG 层构成，这些层被分组为每个 4 (2)层的“波浪”。

[牛鲨](https://arxiv.org/abs/2201.05677) 为部分同步模型建立骑在独角鲸身上的拜占庭共识。它设计有 8 层 waves 驱动提交，每一层都是专门为协议中的不同步骤而构建的。Bullshark 是 DAG 上的一种“零消息开销”协议，但是推进层可能会被一致计时器延迟。

***鸣谢:**非常感谢*[*left Eris Koko ris-kogi as*](https://twitter.com/LefKok)*指出了关于独角鲸和牛鲨的实际细节，帮助改进了这篇文章。T15】*

## **建议阅读**

前区块链时代:

*   *【利用分布式系统中的虚拟同步】* ，伯尔曼和约瑟夫，1987。[【Isis】](https://dl.acm.org/doi/10.1145/37499.37515)
*   *《异步拜占庭协议协议》* ，布拉查，1987 年。 [【布拉查广播】](https://core.ac.uk/download/pdf/82523202.pdf)
*   *《在进程间通信中保存和使用上下文信息》* ，彼得森、布赫霍尔茨和施利奇廷，1989。[【Psync】](https://dl.acm.org/doi/10.1145/65000.65001)
*   *《分布式系统的广播协议》* ，梅利亚-史密斯，莫泽和阿格拉瓦拉，1990。 [【交易和合计】](https://ieeexplore.ieee.org/document/80121?tp=&signout=success)
*   *【总排序算法】* ，莫泽、梅利亚尔-史密斯和阿格拉瓦拉，1991。 [【总计(简写)】](https://dl.acm.org/doi/10.1145/327164.327298)
*   *【拜占庭-弹性总排序算法】* ，Moser 和 Melliar Smith，1999。[](https://www.sciencedirect.com/science/article/pii/S0890540198927705)
*   *《Transis:一个高可用性的通信系统》* ，阿米尔、多列夫、克雷默、马尔基，1992。 [【瞬态】](https://ieeexplore.ieee.org/document/243613)
*   *“异步环境下的提前交付全有序多播”* ，多列夫，克雷默和马尔基，1993。[【ToTo】](https://dahliamalkhi.github.io/files/Multicast-FTCS1993.pdf)
*   *《理解因果和完全有序传播的局限性》* ，切里顿和斯基恩，1993。[【CATOCS】](https://dl.acm.org/doi/10.1145/173668.168623)
*   *“何苦用 CATOCS？”* ，范·雷内塞，1994。 [【响应 1 到 CATOCS】](https://dl.acm.org/doi/10.1145/164853.164859)
*   *《回应切里顿和斯基恩对因果和完全有序传播的批评》* ，伯尔曼，1994。 [【响应 2 到 CATOCS】](https://dl.acm.org/doi/10.1145/164853.164858)
*   *【安全协商协议:Rampart 中可靠的原子组组播】* ，Reiter，1994。 [【壁垒】](https://dl.acm.org/doi/10.1145/191177.191194) 。

区块链时代:

*   *《漩涡散列图共识算法:公平、快速、拜占庭容错》* ，贝尔德，2016。 [【漩涡散列】](https://www.swirlds.com/downloads/SWIRLDS-TR-2016-01.pdf)
*   *《区块狂热:从区块 DAGs 到共识》* ，Danezis and Hrycyszyn，2018。[【block mania】](https://arxiv.org/abs/1809.01620)。
*   *《aleph:具有拜占庭节点的异步网络中的高效原子广播》* ，Gągol、莱尼亚克、斯特拉扎克、威特克，2019。[【Aleph】](https://arxiv.org/pdf/1908.05156.pdf)
*   *《独角鲸和长牙:一个基于 DAG 的 Mempool 和高效的 BFT 共识》* ，Danezis，Kokoris-Kogias，Sonnino，和 Spiegelman，2021。 [【独角鲸与长牙】](https://arxiv.org/abs/2105.11827)
*   *“你所需要的只是达格”* ，凯达，科科里斯-科吉亚斯，纳奥尔，和斯皮格曼，2021。[【DAG-rider】](https://arxiv.org/abs/2102.08325)
*   *《牛鲨:达格·BFT 协议实用化》* ，斯皮格曼，吉里达兰，索尼诺，和科科里斯-科吉亚斯，2022。 [【牛鲨】](https://arxiv.org/abs/2201.05677%22)T10】
*   *《DAG 上的 MEV 保护》* ，Malkhi 和 Szalachowski，2022。[【MEV 保护上 DAG】](https://arxiv.org/abs/2208.00940)`**