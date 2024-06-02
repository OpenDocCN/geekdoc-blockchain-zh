# 区块链与经济交易

Daisuke AdachiJun Aoyagi

## 1 引言

加密货币市场价值飙升，以比特币为例。与此同时，基于加密货币的交易在过去十年中也显著增加。与此同时，区块链的概念自加密货币的兴起以来也得到了普及，作为加密货币的背景技术。在本章中，我们将概述加密货币和区块链的技术和经济方面。我们试图回答的第一组问题包括但不限于：什么是区块链？比特币挖矿过程是什么？什么是加密交易？

此外，区块链不仅仅是关于比特币。我们一直在观察这些新技术在实体经济交易以及金融市场中的作用范围扩大。商品、商品和资产市场的交易曾经与基于区块链的操作无关，而如今，几种重要的产品是借助区块链进行交易的。例如，咨询公司 EY 顾问进行了一项关于商品市场区块链的实证实验，例如葡萄酒交易。区块链采用对葡萄酒市场的影响是什么？为什么我们需要在葡萄酒交易中使用区块链？它如何改变葡萄酒市场的属性，如葡萄酒的质量、交易价格？

在我们简要讨论了区块链的技术方面之后，我们将详细解释加密货币和区块链在实体经济交易中的作用。特别是，我们将关注（i）区块链如何影响交易中的信息摩擦以及（ii）它如何改变市场的格局，同时考虑到对所有参与者的溢出效应。

为了使我们的讨论更加流畅，我们不会详细讨论区块链中的加密技术。

感兴趣的读者可以参考，例如哈维（2016）关于基于加密的金融的概述，以及安东诺普洛斯（2014）关于比特币中使用的加密技术的更详细解释。

## 2 区块链的技术方面

我们的主要讨论从区块链及其相关技术的概述开始，这些技术包括加密货币和比特币，这些都是最近金融和经济研究的结果。

### 2.1 双重支付

讨论区块链在比特币交易中的角色是一个很好的起点：比特币如何以及为何与现有货币和数字货币不同。这方面的一个显著问题是双重支付问题。假设鲍勃通过移动支付系统在线购买了一本书。在收到书后，他可以入侵在线账本，重写他的账户信息，假装交易从未发生，以取回他的钱。实物货币通过发展复杂的印刷技术来解决这一问题，从而使伪造钞票变得困难。此外，具有物理实体的现金（硬币和纸币）不能被重复使用，因为如果爱丽丝手里拿着它，鲍勃就无法将它放在口袋里。

虽然伪造实物钞票变得越来越困难，但我们的大部分日常交易已经变得数字化，例如，借记卡交易，通过 PayPal、Venmo、Google Pay 等支付。传统的数字货币受到双重支付问题的困扰，因为它们容易受到信息操纵的攻击。如果账本系统存在缺陷，鲍勃可能会操纵账本信息，取回他支付的钱。这个问题通常通过设立一些具有反操纵安全性的集中机构来处理。虽然这样做可能很安全，但成本相当高，用户也担心信誉问题。

区块链和比特币提供的是一个全新的解决方案。具有难以回滚机制的去中心化缓解了这个问题。它将交易信息分发到大量参与计算机的节点。数据被时间戳标记且不可撤销。一组交易记录被嵌入到一个块中，进行加密，并附加到预先存在的信息链上。这个过程反复进行，以生成一系列链块，即区块链。由于所有节点都拥有关于世界状态的信息，必须有一个共识机制来确定什么是正确的状态以及应该在块中记录什么。

接下来，我们将依次详细介绍关键概念、去中心化、共识机制和智能合约。

### 2.2 去中心化

第一个构建模块是信息的去中心化管理。信息被分发到大量（潜在的无限）数量的计算机上，它们各自跟踪信息。首先，这防止了单点故障，意味着即使网络中的一个节点失败，整个系统仍然可以跟踪正确的信息。

另一个好处包括减少市场力量和增加竞争。如果一个中心化的玩家行使她的垄断权力，她可能会有动机操纵和扭曲信息以利于自己。正如我们在下面的节中讨论的，区块链上的信息必须是网络的共识。因此，即使一个单一的记录者试图操纵信息，几乎不可能实现。¹

总之，在传统记录系统中，中心化的记录者被大量的竞争性记录者（在比特币网络中称为“矿工”）所取代。他们通过一定的共识机制竞争性地决定将哪些信息记录到区块链系统中，而不是由一个单一的中心实体做出决定。

### 2.3 共识机制

第二个构建块是如何达到共识。该机制必须使共识难以被操纵，而一个关键的技术进步，即密码学，在这里发挥作用。² 达成共识的关键要素是选择合法信息的节点。由于区块链网络中没有中心化的玩家，一些终端节点必须做出决定。选择节点的过程对每个应用程序都是独特的，但在比特币和其他大型区块链（例如，以太坊）中，采用了名为工作量证明（PoW）的共识机制。我们接下来关注 PoW，尽管还有许多其他可能的共识算法，例如权益证明(Saleh, 2019)。

PoW 是一种过程，该过程（i）要求网络中的每个节点解决计算密集型的加密难题，并且（ii）奖励第一个成功解决问题的节点，通过赋予其授权信息并将其记录在区块链上。

加密难题依赖于哈希函数。哈希函数应满足几个属性（例如，均匀性、普遍性、确定性函数、定义域），这对于下面解释的挖矿协议的工作是可取的。具体来说，节点被要求找到一个数学问题的正确值。找到解决方案的预期时间由难度目标决定。同时，随着每个节点投入到问题中的计算能力（称为哈希能力）变得强大，它会减少。解决问题需要高计算能力，这触发了节点之间的竞争，即如果其他节点采用更高的哈希能力，你赢得比赛的概率就会降低。寻找这个值的这个过程被称为挖矿，因为它让人联想到从矿中找到金属矿石。当一个节点赢得比赛时，挖矿奖励以比特币支付，她有权在区块链上记录信息。

这有助于解释为什么区块链上的信息几乎是不可篡改的。首先，试图重写链上信息的有害实体必须积累超过网络其他参与者的巨大计算能力。其次，潜在的攻击者必须找到攻击的重大利益，即挖矿比特币的回报必须超过计算能力的成本。

通过去中心化记录者之间的竞争，总哈希率影响共识的质量。正如我们稍后将要讨论的，较高的哈希率可能会提高共识的质量，因为对于每个矿工来说，赢得比赛的成本变得更高，她通过投入大量电力来操纵信息的激励就会减弱。这种激励问题将转化为我们后文讨论的经济交易中的信息摩擦程度。

从 2016 年到 2018 年秋季，比特币的哈希率逐年增加，但随着虚拟货币市场的崩溃，哈希率继续下降。在这些时期，公司可能被迫退出挖矿业务。这一观察结果将是我们在第三部分中的经济分析的关键因素。

### 2.4 智能合约

智能合约本身就是一个独立于区块链的抽象概念。Szabo（1997 年[1]）将其描述为一种基于特定条件自动执行的合约，无需任何集中授权。虽然加密安全机制只是实现智能合约的众多可能选择之一，但区块链逐渐成为保证智能合约中安全交易的主要机制。

作为底层技术的区块链非常适合智能合约的目标。首先，具有共识机制的去中心化信息存储系统使得交易可验证，因此在不依赖集中权威的情况下也可执行（即智能合约的第一个条件）。此外，以太坊发明了一种区块链系统，该系统记录一些预先设定条件的信息（即智能合约的第二个条件）。也就是说，当且仅当满足特定条件时，交易才会被验证——即支付和交付的信息被记录为“正确”并且变得不可更改。

智能合约不仅使双重支付变得极其困难，它还作为一种新型的“保证书”来确保商品的质量。其创新之处在于，合约所依据的信息是由去中心化的记录者管理，而不是由集中的权威机构管理。在第三部分中，我们将详细研究智能合约的概念、它所包含的内容以及背后的区块链角色。

### 2.5 现有问题

到目前为止，我们已经概述了区块链的一些有利属性。虽然区块链显著减轻了这些问题，但在区块链和智能合约的实际实施中仍然可能存在问题。其中，我们概述了一些技术问题。一般来说，深入考虑可以给出区块链的“不可能三角”Abadi 和 Brunnermeier (2018)。他们比较了工作量证明（PoW）、权益证明（Proof-of-Stake）和中心化账本的特点特征。他们的分析确立了自给自足、无租约和资源效率之间的基本问题。

#### 2.5.1 可扩展性

在区块链的技术问题中，我们概述了可扩展性和 Oracle 问题。可扩展性问题，一般来说，是在区块链参与者数量增加时出现的。这里所说的参与者包括加密货币的矿工和用户。一方面，当矿工池的大小增加时，记账变得缓慢。特别是，区块链最新状态的传输速度取决于网络中最慢的节点。因为任何人都可以参与区块链网络，一个低性能的节点通常会减慢整个系统。

另一方面，如果许多用户涌入加密货币，区块链网络的负载会爆炸性增长，在许多情况下会导致显著的转账等待时间和增加交易费用。此类问题的一种表现包括拥堵效应；交易批准的长时间队列可能会激励用户支付高额交易费用，因为矿工会优先处理产生高额佣金的交易。拥堵效应增加了使用区块链的整体成本(Easley 等人, 2019; Huberman 等人, 2019)。

#### 2.5.2 Oracle 问题

区块链中的 Oracle 指的是将数据从区块链外部发送到区块链内部。区块链能够对在区块链系统中积累的信息生成共识并使其不可更改。然而，原始信息必须从外部来源引入到区块链中。这些外部信息也必须可信，以保证整个区块链系统的安全。如何保证可信度被称为 Oracle 问题。

例如，在葡萄酒区块链中，我们希望建立这样一个事实：存储在区块链中的葡萄品种没有被操纵，但是区块链内部并没有暗示最初注入系统的信息不是谎言。这也对智能合约提出了怀疑。假设你进行了一笔葡萄酒交易，取决于某些条件，比如“只有当葡萄酒是 100%来自加州纳帕的卡本内苏维翁时才付款”。你（几乎）确信在信息被锁定到区块链记录系统之后没有进行任何信息操纵，即一旦区块链保证瓶中是 100%的卡本内苏维翁，就很难将其与品诺黑混合并仍声称它是 100%的卡本内苏维翁。然而，你并不确定最初的信息是否正确。区块链节点无法区分最初的葡萄。当我们分析对实际经济交易的含义时，我们将回到这个问题。

#### 2.5.3 分叉

回想一下，区块链向之前的链添加区块。偶尔，节点不同意应该向哪个现有链添加区块。在这种情况下，区块链在链中的某个点分裂。这种分裂称为分叉。分叉对整个区块链系统可能是有害的，因为它可能破坏存储在链中的信息的共识。一些现有研究解决了分叉发生的原因。例如，拜 ais 等（2019 年）2019 以重复博弈的形式研究了在什么条件下矿工遵循最长链规则（LCR）的简单规则。

### 2.6 一些应用

尽管上述有一些问题需要解决，但我们有很多区块链应用的例子，我们现在将进行概述。这样做时，我们涉及到几个区块链成功解决问题的案例，并开辟了新的领域。

第一个值得提及的成就是加密货币消除了部分证券市场中固有的结算风险。在此背景下，结算风险指的是卖方在收到支付的同时未能交付证券，或反之亦然。智能合约可以通过自动化的区块链基础设施实现交收对支付（DvP）机制，而无需任何中央权威。特别是，赵和科佩尔（2019 年）2019 认为，区块链在这种情况下主要的优势是“它可以加快结算，一方面通过摆脱分割的后交易基础设施，另一方面通过实施更灵活的结算周期。”

区块链还显著改变了动态环境下的金融合约设计。

传统上，金融合同只取决于事件，使得合同是静态的。然而，区块链以时间戳的顺序存储信息。因此，出现了新的金融合同，这些合同不仅取决于已经发生的事件，还取决于事件的时机。蒂恩（2017）2017 表明，各方之间的最优合同是动态调整利润分享规则的合同。

此外，区块链在去中心化共识与信息分布之间开辟了新的紧张关系，这两者是密不可分的。具体来说，为了实现去中心化共识，区块链需要让参与节点验证信息。为此目的，它需要分布（有时是敏感）数据。丛和何（2018）2018 从这种可能性中获得了启示，并将其应用于隐性共谋的问题。他们发现，尽管区块链可能通过缓解不完全合同的问题而实现更高的竞争，但它可能会潜在地导致卖家之间的共谋。

我们已经概述了区块链技术的最前沿理解、问题和应用。在本节中，我们将自己限制在金融交易的领域。从现在开始，我们将拓宽视野，包括实际经济交易。为了从下一节研究的技术的新的视角，以一种新的方式考虑哈希率。特别是，人们可以认为哈希率是比特币市场的供应产品，因为它传递到输出，即比特币代币。例如，帕诺塔塔和布拉斯基（2018）2018 将这一想法应用于分析比特币价格和哈希率的行为。通过进一步推动这一想法到实际经济交易，我们将在下一节考虑区块链更广泛潜在影响。

## 3 对实际经济交易的启示

当我们仔细考虑市场和参与者如何对区块链在经济学家经常称之为一般均衡的环境中的采用做出反应时，另一个问题出现了。通过回顾青柳和增田（2018）的研究，我们将探讨区块链和加密货币对金融领域之外实际经济的潜在影响。

### 3.1 背景

考虑下的真实经济交易例子可能很多且不断扩展。已经推出了许多基于区块链的交易平台，包括葡萄酒（安永咨询和顾问公司）、新鲜食品（沃尔玛）、珠宝（超级账本）、艺术品和摄影（柯达）、安全（tZero）和加密货币（Waves、IDEX、Steller、Oasis、OKEx、Cashaa 等）。在下面的分析中，我们将这些商品、商品和资产统称为“商品”或“产品”。

为了让大家了解真实经济交易的情况，可以考虑安永咨询和顾问公司的葡萄酒区块链案例。该区块链作为跟踪葡萄酒产地和质量的解决方案，涉及葡萄酒分销的所有生态系统：生产商、分销商、物流和保险公司。区块链提供交易代币。使用代币可以跟踪葡萄酒运输、仓库存储和交付，以及运输过程中的保险赔偿和瓶子的买卖。换句话说，分销商和消费者可以直接从平台上订购葡萄酒，并实时跟踪运输状态，包括清关和储存。

从这个例子中可以看出，区块链在商品交易中的应用可以概括如下。首先，区块链包括加密货币，这是一种作为交易手段的数字代币。其次，矿工持续监控涉及加密货币和区块链的交易。最后，包括卖家在内的用户可以使用代币来交易商品。

在下面的讨论中，我们将提供一个涉及区块链的完整经济交易系统。加密货币代币在挖矿市场中进行交换。矿工加入市场，代币作为记录保存努力的奖励给予他们。代币的用户有两类——商品（咖啡）的买家（鲍勃）和卖家（爱丽丝）。用户可以使用或不使用加密货币进行交易。如果他们不使用，他们需要求助于传统的支付方法。值得我们再次强调的是，我们将矿工和用户这两种类型的代理商区分开来。鉴于这种二分法，下面提出了以下问题。

### 3.2 问题

由于我们的兴趣在于区块链采用对实际经济交易产生的广泛影响，因此我们需要谨慎地提出一个正确的问题。我们首先提出一个相对抽象的动机，然后逐步细化为一个更具体和精确的问题。这个过程始于询问：区块链采用对经济交易的一般均衡（GE）有何影响？在我们关注的背景下，GE 意味着我们感兴趣的是经济变量的联合决定，包括商品的价格、交易量、市场质量，以及与区块链相关的变量，如加密货币的价值和矿工池的大小。迄今为止的讨论已经探讨了每个参与者的机制和激励（例如，矿工）。在现实经济中，它们相互作用，形成整体经济系统。我们关注的经济发展成果是什么样的，比如交易的加密货币的价格和数量、使用加密货币的用户分类、交易的商品质量？当加密货币挖矿的成本增加时会发生什么？去中心化的交易空间是否比由单一集中记录者运营的空间更好？

这些动机使我们提出一个自然的问题——用户为何使用区块链交易商品，除了防止双重支付之外？对这个问题的简短回答是不对称信息。为了更好地理解这一点，让我们进一步询问自己：区块链的经济含义是什么？正如我们所看到的，区块链在技术上是一系列使能去中心化信息保存系统的技术和概念。这一定义特征与近年来商品市场应用的激增密不可分。特别是，在现实经济中，对商品来源知识的日益增长的需求。部分原因是国际法规的变化和运输与通信成本的降低，供应链变得复杂。例如，iPad 和波音 787 的全球供应链庞大得令人难以置信。理解这些产品链的整体结构几乎是 impossible 的（Antras，2015）。

甚至在跳到这样的极端例子之前，葡萄酒生产已经足够复杂，以至于区块链发现它有助于我们下面讨论的问题。葡萄酒生产至少包括以下步骤：种植和收获葡萄及其他原料，酿造，运输，陈年，以及交付。所有这些步骤对于让最终消费者享受到高质量的酒瓶都是不可或缺的。如果这些步骤在一个家庭生产和销售的个人玩家内部完成，那么质量造假的问题就会最小化。然而，这种生产的一体化方法是不具备可扩展性的，而一个典型的市场结构涉及供应链中的多个各方。此外，在生产的任何给定阶段，通常很难验证产品的质量直至该阶段。

在这种情况下，经济学家通常所说的柠檬问题出现了。即，买家可能无法验证他们购买的输入质量。此外，生产低质量商品的成本通常更低（想象一下通过重写低质量的葡萄品种来伪造高质量品种的 counterfeiting）。因此，交易被低质量商品污染。柠檬直接转化为葡萄酒的低质量瓶装，可能导致高质量葡萄酒市场的崩溃（阿克洛夫，1970 年）。因此，正确了解其他各方生产的上游商品质量的需求非常大。

### 3.3 区块链在经济交易中的作用

柠檬问题中的关键概念是信息不对称，只有卖家知道质量，而买家不知道。这个问题的一种潜在（且历史上）的解决方案是引入一个中心化的记录保持者。然而，通常这种解决方案是昂贵的，如我们上面所讨论的。区块链有潜力解决这一问题。如我们之前所讨论的，区块链的技术方面允许智能合约。参与方可能使用合同协议中预先指定的条件，在这些条件下交易完成。如果声明只有高质量商品可以交易的要求不满足，任一方都可以终止交易，而商品和货币的所有权实际上不发生变化。通过这样做，我们可能实现，在区块链支持下的智能合约下交易的商品可能是可靠的高质量商品。

上述配置可能是正确的。然而，区块链存储的信息的可靠性仍然存在一定的误差。正如我们上面章节讨论的，考虑到预言机问题，无法保证任何协议中传达的信息一定是真实的。区块链能做的是减轻信息的不确定性。我们将这种不确定性水平称为区块链的“安全性”。当安全性高时，存储的信息的不确定性低，反之亦然。

安全级别是如何确定的？当然，当底层技术，比如用于操作区块链的程序代码，强大且复杂时，安全级别就会很高。然而，这并不是故事的结束。认识到并强调矿工的角色和矿工池的大小至关重要。池的大小之所以重要，是因为区块链的去中心化特性——参与的矿工越多，作弊的好处就越小。我们将在下面详细说明具体的机制。至此，我们只声称两点。首先，区块链有一个安全级别的概念。其次，必须在分析的最后确定它。

### 3.4 矿工侧分析

然后我们详细分析市场参与者——矿工、通过购买和销售商品分离的代币用户。之后我们回来结合所有考虑因素来确定经济预测。

关于矿工方面的关键首要问题是：区块链矿工是如何进入矿工池的？正如我们在技术部分讨论的，矿工只有当这样做有利可图时才会加入池并参与挖矿过程（在 PoW 协议的情况下，很可能会配备 ASIC）。何时进入有利可图？为了简化，我们关注区块链附带的加密货币的价格角色。换句话说，矿工在加密货币价格高时进入。我们承认，在确定盈利性时，实际上有很多方面需要考虑。此外，青柳和 stadhi (2018) 表明，我们的分析可能可以扩展到没有加密货币的区块链案例。

尽管上述对矿工方面的考虑在区块链和加密货币的研究中相对常见，但相对而言，研究区块链的用户端如何与矿工互动的却较少。实际上，用户也应积极地对区块链的特点、安全级别以及加密货币的价格做出反应——显然，区块链越安全，对用户的价值就越大。加密货币的价格越低，对于交易商品的买家来说价值就越大，对于卖家来说则越小。考虑到上述讨论，我们将在双重市场中详细考虑这些问题，其中产品可能在一个使用现金或传统数字货币的传统市场中出售和购买，在一个基于区块链的市场中，交易是以基于区块链的加密货币进行的。特别是，用户需要通过区块链积极参与市场，并通过区块链系统提前购买加密货币。因此，我们需要考虑用户和矿工在区块链上的互动。

### 在这种双重市场中，用户对加密货币的需求增加，从而提高了加密货币的安全性。而加密货币价格的降低，对于购买商品的买家来说，增加了其价值，而对于卖家来说则减少了其价值。在这种情况下，我们需要考虑的是，如何通过区块链系统提高用户的安全性和满意度，同时降低交易成本，提高交易效率。

尽管上述对矿工方面的考虑在区块链和加密货币的研究中相对常见，但相对而言，研究区块链的用户端如何与矿工互动的却较少。实际上，用户也应积极地对区块链的特点、安全级别以及加密货币的价格做出反应——显然，区块链越安全，对用户的价值就越大。加密货币的价格越低，对于交易商品的买家来说价值就越大，对于卖家来说则越小。考虑到上述讨论，我们将在双重市场中详细考虑这些问题，其中产品可能在一个使用现金或传统数字货币的传统市场中出售和购买，在一个基于区块链的市场中，交易是以基于区块链的加密货币进行的。特别是，用户需要通过区块链积极参与市场，并通过区块链系统提前购买加密货币。因此，我们需要考虑用户和矿工在区块链上的互动。

在这种双重市场中，用户对加密货币的需求增加，从而提高了加密货币的安全性。而加密货币价格的降低，对于购买商品的买家来说，增加了其价值，而对于卖家来说则减少了其价值。在这种情况下，我们需要考虑的是，如何通过区块链系统提高用户的安全性和满意度，同时降低交易成本，提高交易效率。

直观地说，随着安全等级的提高，基于区块链的商品的需求会增加，因为获得高质量商品的机会更高。这种安全效应增加了其中所需的加密货币的需求。然而，与此同时，随着更多买家涌入基于区块链的市场，加密货币的价格会上升。价格上涨将一些原本会留下的买家驱逐出去。这种拥堵效应可能会减少加密货币的需求，因为区块链市场的规模在缩小。因此，存在两个相互冲突的力量，积极的安全效应和消极的拥堵效应，使得预测是非单调的。特别是，青柳和繁（2018）讨论了这一发现的背后条件以及更多具体的非单调性预测。

读者还应注意，此处加密货币的价值是真实价值而非泡沫。加密货币及其底层区块链有助于减轻信息摩擦问题，从而带来真实经济收益。由于减少了柠檬问题，实际经济价值也是这一分析的特征之一。

### 3.6 变化分析

通过深入思考关于矿工和用户的两方面思想实验，我们可以考虑外部经济条件变化对我们感兴趣的研究特征（如加密货币价格和区块链的安全等级）产生的丰富影响分析。这种分析在测试我们上述考虑时通常很有用。尽管详细信息见青柳和繁（2018），我们给出了他们研究的两个示例。

何时区块链比中心化系统更有效？我们可以将上述分析视为在有中心权威的情况下嵌套案例。通过考虑只有一个概念性的“矿工”被允许进入代币生成系统的情况，可以看到这一点。这个矿工，我们称之为中心化权威，不再挖矿，因为它不再需要以去中心的方式保持记录。相反，它只是给系统中的所有交易提供凭据。中心化权威会做什么？由于现在它可以选择安全级别，而无需分布式共识机制，它会这样做以优化其利益，即在授权时他们将收到的代币的价格。在这里，非单调的加密货币价格结构很重要——中心化权威会利用它，为自己选择最佳的安全级别，而不考虑其他方的适当安全级别。青柳和繁（2018）详细说明了在分布式账本系统（区块链）下的安全级别高于中心化账本系统的情况。从这个意义上说，我们的考虑在强调去中心化好处的同时已经完成了。

第二种分析是关于以下预测：ASIC（例如 ASIC 机器价格、电力价格）的运营成本将发生变化。当成本增加时，会有更少的矿工加入矿池。实际上，这会提高加密货币的价格，因为矿工的进入必须更有利可图，以覆盖增加的挖矿成本。我们已经概述了区块链的安全级别可能会增加或减少对加密货币的需求。如果它下降了，那么我们预计加密货币的价格会上升。这一预测证实了之前研究中讨论的直觉。如果它增加了，那么令人惊讶的是，挖矿成本的增加可能会潜在地降低加密货币的价格。这个预测最初是由青柳和繁（2018）提出的，但尚未在真实世界数据中得到正式测试。

尽管不全面，我们已经见证了一些支持我们故事的支持证据。一个例子来自上面提到的葡萄酒区块链项目。例如，几家葡萄酒销售公司在接受 EY 咨询和咨询进行实证实验时引入了葡萄酒区块链。结果包括瓶装酒的单位价格提高。这一结果与我们的故事一致，因为葡萄酒区块链旨在改善供应链中无篡改存储的信息，使瓶装酒对最终消费者的平均质量得到改善。更高的质量转化为更高的价格。预计更彻底的实证研究将挑战本节概述的故事。

## 4 结论

在本章中，我们概述了技术方面以及实际经济交易的可能影响。在整个分析过程中，我们强调了去中心化和智能合同在我们的目的中的作用，而未解释区块链的许多有趣方面。我们只是开始见证深刻真实经济后果的经济交易子集。然而，如我们技术部分所暗示的，这些影响即将到来。我们希望当前的专著有助于读者框架区块链及其经济影响。

## 参考文献

阿巴迪，约瑟夫，和马克斯·布鲁内默尔（2018）。《区块链经济学》，技术报告，米莫，普林斯顿大学。 a，b

阿克洛夫，乔治（1970）。柠檬市场。 《经济学季刊》第 84 卷（3），488-500。 a，b

安东诺普洛斯， Andreas M. 2014\. 《精通比特币：解锁数字加密货币》。奥莱利媒体公司。 a，b，c，d

安特拉斯，波尔（2015）。《全球生产：企业、合同和贸易结构》。普林斯顿大学出版社。 a，b

青柳，纯，和大道寺达哉（2018）。区块链平台的经济含义。可在 SSRN 上获取，3132235。 a，b，c，d，e，f，g，h，i，j，k，l

比哀斯，布鲁诺，克里斯托夫·比谢雷，马修·布瓦 vard，和凯瑟琳·卡萨马塔（2019）。《区块链民俗定理》。《金融研究评论》第 32 卷（5），1662-1715。 a，b

陈，龙，林威廉，和小肖（2019）。区块链经济学简介。可在 SSRN 上获取。 a，b

蔡，乔纳森，和 Thorsten V. Koeppl（2019 年）。基于区块链的资产交易结算。*金融研究评论* 32(5)，1716-1753。 a，b

丛，林威廉，和 Zhiguo He （2018 年）。*区块链 disruption and smart contracts.* a，b

Easley，大卫，Maureen O’Hara，和 Soumya Basu（2019 年）。从挖矿到市场：比特币交易费用的演变。*金融经济学杂志*。 a，b

哈维，坎贝尔（2016 年）。*加密金融*。 a，b

胡伯曼，古尔，雅各布·莱什诺，Ciamac C. Moallemi（2019 年）。比特币支付系统的经济分析。*哥伦比亚商学院研究论文*，17-92。 a，b

帕诺塔，埃米利亚诺，和安德烈亚·布拉斯基（2018 年）。比特币和去中心化网络资产的均衡估值。可在 SSRN 3142022 处获得。 a，b，c，d

萨利赫，法哈德（2019 年）。无浪费的区块链：权益证明。可在 SSRN 3183935 处获得。 a，b

萨博，尼克（1997 年）。在公共网络上正式化和保障关系。*第一星期一* 2(9)。 a，b

蒂恩，卡特琳（2017 年）。*区块链与最优融资合同的未来*。 a，b

## 注释