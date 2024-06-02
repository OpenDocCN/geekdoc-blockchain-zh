© Springer Nature Switzerland AG 2020S. Stein Smith 区块链、人工智能和金融服务业商业和金融的未来[`doi.org/10.1007/978-3-030-29761-9_4`](https://doi.org/10.1007/978-3-030-29761-9_4)

# 4. 共识方法论

Sean Stein Smith^(1 )(1)Lehman College, CUNY, Bronx, NY, USA

### 关键词

共识审计工作证明工作股权证明经过时间的证明公共区块链私有区块链联盟区块链 ICOSTOSSmart 合同支付通道

在此时值得注意的是，在深入讨论不同类型的区块链之前，似乎很自然地先讨论信息是如何被批准、验证并添加到现有的区块以形成区块链本身的（Andolfatto 2018）。

在这里稍微停顿一下，来欣赏一下基于共识的方法论与传统金融服务流程是多么的不同吧。让我们简单浏览一个快速简单的例子。

审计失败，其中一些失败非常惨重，比如发生在金融危机期间的那些失败，以及发生在不经常但令人不安地频繁发生的失败，都是一个很好的例子。转向市场交易和流动性讨论，摩根大通的伦敦鲸事件突显出即使在最大最复杂的组织中，交易、交易限制和对这些活动的监督的内部控制有多么薄弱。无数其他的失败，无论是与以适当文件或支持出售的抵押贷款有关，还是与发布然后撤回的报告有关，又或者是与缺乏可靠数据影响决策有关，都显示出一个中心化的批准和文档过程实际上有多脆弱。现在，话虽如此，也很重要要认识到，对于绝大多数情况来说，集中式的数据管理解决方案可能完全可以正常工作。然而，随着信息和业务变得越来越数字化、全球化和去中心化，维护一个核心操作的集中平台的可能性将不足以前进。

让我们来看看当前市场个人和组织目前使用的三种最高知名度的基于共识的批准选项之一。

+   工作证明（PoW）：仅需要单个节点提交解决方案来解决一个算法问题，这很难实现，但一旦完成就很容易验证。这是比特币和以太坊区块链中使用的方法，但消耗的电力比其他选项多，降低了大规模实施的适用性。对于中型甚至大型注册会计师事务所和客户来说，这种审批协议和共识可能不太有效或适用于日常使用。

+   权益证明（PoS）：与 PoW 相反，PoS 协议使用抽签系统来决定哪个节点（成员）将批准所讨论的交易和信息。被选中批准交易和信息的概率取决于问题组织或个人持有的权益。

    +   在这个讨论中，权益指的是个人或组织持有的比特币或其他另类币的数量。

    +   虽然这可能导致一些较大的另类币持有者对条目和区块有着超出比例的批准控制权，但这些大股东也同样对网络的成功和真实性感兴趣。

+   时间流逝的证明（PoET）：PoET 与 PoS 协议背后的方法论不同，PoET 分配了一个随机模型来决定谁将批准待处理信息的区块。等待时间最短的节点（成员）赢得了彩票，但必须等待一段时间才能批准其他区块。需要记住的一点是，为了使用 PoET，涉及的节点必须运行英特尔软件保护扩展，这可能会给一些组织和客户带来问题。

## 公共区块链与私有区块链

尽管书籍、文章、播客、视频以及无数的演示对区块链进行了广泛的讨论和分析，但往往将其视为一个整体或协议来讨论和分析，这是对技术的不完整和错误的视角。虽然市场上有更细致的定义和类型的区块链，但在本次对话中，这个话题可以归结为两个大的类别：公共和私有区块链（Bussmann 2017）。尽管有数百甚至数千种可行的区块链模型可供组织采用，但一般来说，有两个值得进一步研究的可行类别。对这两个大的和不同的类别进行一番审视，现在似乎是一个好时机，可以制定一些既有解释性又有区分性的定义。

## 公共区块链

公共区块链可能是大多数专业人士在谈论区块链时所想到的，以广泛分布的数据库形式存在，任何个人或组织都可以加入并成为其成员。完全的去中心化性质，提供大量的匿名度，公共区块链可以像网络成员希望的那样大。除了允许任何人加入并成为网络的一部分之外，公共区块链的概念也是比特币所依赖的区块链类型。即使从高层次上看，这种开放访问也在链接诉讼、治理和冲突解决机制等问题上产生了相当多的开放问题和议题，这对于金融专业人士来说都是非常重要的（Webster and Charfoos 2018）。本书并不专门讨论加密货币，但在接下来的页面中，我们将讨论并分析什么是比特币，揭开炒作，将比特币与金融服务联系起来。然而，就目前而言，公共区块链的概念可以被视为一些最直言不讳的支持者认为的区块链技术的“理想”版本和类型。

利用公共区块链模型的一些优点和优势在于，由于技术本身的特性，无需中央清算机构或监管机构来验证、清算或确认交易。这可能会吸引一些自由主义倾向的区块链支持者，或者对当前银行和监管系统现状不满的个人，但对金融专业人士来说会带来一些关键问题。例如，吸引了各行业子部门的金融专业人士注意的一点是，如果这个完全去中心化的金融系统从概念到现实的发展，对中介的需求和要求将会减少。想想这个具体的例子；如果个人或组织可以在不需要中介来验证或确认数据的情况下进行交易和发送信息，银行和其他金融机构真的有必要吗？

公共区块链实施和方法的一些劣势是，随着公共区块链的扩展和增长，单个交易的实际验证和确认可能变得越来越繁琐。2018 年，支撑加密货币比特币的区块链网络是最受欢迎和广泛使用的公共区块链之一，会员数量超过 1000 万。然而，网络的规模本身并不一定是一个问题或复杂的问题；是网络规模和数据验证方法的组合可能使利用过程复杂化。再深入一点，并回到之前介绍的工作证明思想，与比特币和其他公共网络相关联的这种批准和共识验证方法通常是工作量证明协议。虽然对一些人来说，这可能是数据在加入区块链环境时应该得到批准的最真实的形式，但这可能会在许多交易和互动方面形成瓶颈，因为实际上有多少交易和互动能够得到网络成员的验证。

例如，在 2018 年中期，比特币区块链（最大和最成熟的区块链网络）可以处理的交易数量介于每秒 10-15 笔之间。这在数据批准的速度上并非缓慢或繁琐，但与信用卡和其他金融中介机构可以处理或批准的数据量相比，比特币作为购买工具的显著缺点就显而易见了。除了不如现有的批准方法那样高效或快速外，比特币区块链采用的工作证明方法还有其他两个值得注意的问题。首先，处理和确认不同交易和信息所需的大量计算能力和服务器意味着，随着区块链规模的扩大，参与网络的积极作用需要更大规模和更复杂的计算能力。其次，除了需要大量的计算能力和基础设施外，所有这些计算设备都会消耗大量电力。电力需求增长如此之大，以至于一些公用事业公司寻求转租或出租部分场地来促进区块链批准流程。

## 私有区块链

相反地，由于私有区块链网络的构建和操作方式有点混合的特性，私有区块链并不被区块链纯粹主义者认为是真正的区块链模型。然而，需要记住的是，即使私有区块链是一个混合模型和区块链类型，数据添加和批准的基本原则并没有实质性的不同。私有区块链和公共区块链之间的核心区别在于，公共区块链不存在集中的中心或权威，而私有区块链将会有一个组织机构。组织机构可以是任何类型的组织，比如银行、其他金融机构或之前介绍的沃尔玛等其他类型的组织。

组织机构是为了缺乏更好的描述性词语而使用的，它编写并制定了区块链运行规则和准则。具体来说，通过嵌入在区块链功能中的编码和编程语言，组织机构将决定并授权什么样的组织可以成为网络的一部分，也授权这些不同成员能做什么。更深入地了解这到底意味着什么最好的方法是，一个类比可以帮助将这个有些抽象的思想连接到每个金融服务行业中大家更熟悉的概念。将私有区块链看作是类似于可共享文件的方式之一，就像谷歌文档一样。创建文件夹或文件的个人可以决定（1）谁有权访问所讨论的文件或文件夹，以及（2）这些不同个体一旦成为网络的一部分后实际上可以做什么，就像不同用户可以具有编辑、评论或仅查看权限一样。

由于私有区块链的访问比纯公共区块链的访问更受限制，这意味着批准、数据验证和向其他网络成员传达这些信息可以以更简化的方式进行。客观地看，这些好处是合理的；与任何人都可以加入并成为其中一部分的公共区块链不同，私有区块链的批准过程可以被限制只包括直接参与其中的个人。这种限制会员资格和不同分配的责任级别的组合意味着，除了对商业用途更有效和实用之外，私有区块链可能实际上是更注重环保的选择。因为，由于组织机构的监督，任何批准和验证过程可以被网络成员使用，这也意味着信息的确认和批准可以比纯粹的公共区块链模型更为时间有效地进行。

私有区块链的一些不利之处源于区块链技术本身，以及它是如何从纯粹的公共模型被适应为私有区块链设置的，这可以在所有意图和目的上被视为一种混合模型。具体来说，对于寻求实施和利用区块链技术的金融服务专业人士来说，一个组织公司能够以各种方式制定政策、指南和要求至关重要。例如，在私有区块链网络中，如果组织公司和协议以某种方式编写，使得一组组织、特定的几家公司或少数几家组织可以在没有其他网络成员监督的情况下上传、验证和验证数据块，那么这对于金融服务技术的适用性构成了威胁。除了私有区块链模型中的这个根本缺陷外，还有一个要求，就是对于组织公司来说，要真正领导私有区块链，该组织必须具备足够的技术专业知识。除了将责任放在组织公司身上外，这也创造了一个机会，即如果客户和其他组织加入由不道德行为者领导的私有网络，那么所有其他网络成员都可能面临潜在风险。

## 联合或联邦区块链模型

公共区块链可能不是针对个人组织最适合的区块链技术模型，特别是考虑到存储在平台上的信息的分布性和开放性质。特别是考虑到 2018 年和 2019 年与加密货币市场相关的价格波动（即价格下跌），一些投资者和机构已经越来越不愿投资于公共或完全分布式的区块链模型。尽管底层的区块链技术和加密货币本身并不完全相同，但它们在同一个加密区块链生态系统中运作，并且自然而然地受到彼此的影响。与此形成鲜明对比的是，完全私有的区块链模型，尽管有这样模型所产生的好处和效率特征，也并不总是适用于每一种情况。为了建立和运作一个私有区块链模型，实质上必须由一个公司或组织负责驱动网络本身的操作协议和算法。

在某些情况下，例如 IBM 和沃尔玛之间公开的私人区块链合资建设，负责机构可能有技术和财政能力来建立和维护私人区块链。更重要的是，组织机构可能具有影响力和谈判地位，以帮助推动并要求供应链或网络的不同成员采用组织机构开发的私人区块链模型。也就是说，特别是在市场权力相对集中的领域或行业，如会计或投资银行，可能有一些机构希望承担组织公司的角色。即使有适当的保障措施和控制措施，将信息存储和保护外包给第三方公司始终存在风险，特别是在半合作半竞争模式下。这种愿望以及市场现实的反映已经引导一些行业和在其中运营的组织努力开发一个满足市场需求的模型和理念，同时仍允许个体公司对信息和数据拥有控制权和所有权。

归纳为核心理念，联盟区块链模型最好被总结为团体努力开发和维护区块链。特定行业的区块链平台已经在房地产、医疗保健、会计、金融以及版税支付和分配领域得到发展，并且区块链作为服务的提供已开始进入市场（Roberts 2019）。与这种战术和理念相关的好处相对容易分析和记录，并且大多数时候与降低成本和降低其他实施障碍有关。例如，在技术复杂领域，一组组织共享资源和信息要比一个组织试图单独承担重担容易得多。此外，在金融服务领域，客户之间的合作和信息分类可能出现潜在利益冲突，建立联盟模型可能更合适，尤其是客户希望获得增加的透明度和信息获取途径时。

一个创建和分发的模型，缺乏更好的词汇，共同所有权和操作的区块链模型在信息透明度方面带来了几方面好处，但也引起与数据治理以及责任关切相关的问题。特别是涉及到个人可识别信息，责任正在逐渐转移到收集和利用这些信息的组织，以建立和保持对该信息访问的保障。尽管与信息连接和共享的共同平台存在的运营和潜在的隐私驱动挑战，贸易财团模型似乎正在成为一个可行的模式。无论是与低成本相关的组织联系在一起，这些成本可以通过在不同公司之间分散成本实现，还是与在特定领域的最大玩家之间的共同平台或模型相伴随的监管便利，或者对于大型标准报告和分析程序的渴望，贸易财团模型似乎为涉及的组织产生了好处。有关不同区块链模型和其他网络安全问题的治理和责任问题在本文中更深入地讨论，但至少在此处初步提及似乎是合适的。图 4.1，对于每种区块链模型，从公共到私有再到混合，都有需要考虑的利弊，其中一些包含在这里的图中：![../images/467992_1_En_4_Chapter/467992_1_En_4_Fig1_HTML.png](img/467992_1_En_4_Fig1_HTML.png)

图 4.1

区块链选项的亮点和区别

## 区块链投资

在金融服务领域和跨不同行业线上，大多数对区块链空间的投资都集中在私人区块链领域，原因很简单，即区块链本身可以定制和修改以满足特定组织的需要。在私人区块链领域，已经进行了大量工作和投资的一个鲜明例子是由 IBM、四大会计师事务所及其他大型跨国公司合作开展的工作。作为对 IBM、亚马逊和其他许多组织投资的回应，微软最近推出并公开了一个旨在建立市场框架和标准的区块链财团工具（Hernandez 2016）。除了利用和拓展加密货币的功能和用例外，供应链和文件似乎是区块链开发正在发生的领域。

即使目前已经进行了这些投资和活动，承认这些投资结果在商业模式方面的商业化数量仍相对较少是恰当的（Moynihan and Syracuse 2018）。商业规模是区块链采用的一种实现目标 - 证明这项技术可以规模化、被采用并在传统系统中实施。话虽如此，在四大会计事务所和投资组织中，已将成千上万的员工和数十亿美元投资到这些平台上，但很少有区块链被用于大规模利用的例子。特定的用例，包括审计某些类型的信息以及应用区块链进行资产验证和税收目的，可能目前已经存在，但这些解决方案更广泛的采用和推广仍然是一个正在进行中的工作。

现在，看起来文件或供应链对会计和金融服务专业人士似乎并没有太多前景，但这只代表了区块链潜力的不完整观点。抵押贷款文件、解决不同交易、确认付款已全额支付并支付给合适的方，以及几乎所有与追踪和分析财务信息相关的事情都涉及确认、追踪和传达大量定量信息。与其仅仅专注于区块链功能的技术编程方面，更合适的讨论应该聚焦于将区块链的潜力框定在数据验证和通信的背景下，将该技术与不同的商业用途联系起来。加密货币可能是区块链经济和格局的领先端，但区块链的核心功能直接连接到了加密货币和建立在该区块链基础之上的其他应用。

在深入研究两个具体的前瞻应用之前，首先有必要重新审视市场已经进行的一些合作进展，这表现在信息技术组织和其他行业参与者之间的合作。除了某些最大会计和金融服务组织的几乎通常的投资和参与，关于这一话题的底层层面可能起初被忽视了。迄今为止，区块链领域的许多最大投资发生在与金融服务有关但最终将不可避免地影响到职业子集目前所执行的工作和功能的领域。无论是房地产文件、供应链实施、改善环境计划的合规性，还是有效利用物联网，事实是区块链的实施和投资是一个数十亿美元的大项目。

仅看一看运行在区块链技术上的三个倡议和应用程序必然会导致某些领域和主题未被讨论；对新兴技术的任何分析也可以说是一样。 话虽如此，让我们看看在市场上引发一些关注和激动的三个最知名的区块链应用程序。

### 前瞻性应用程序

#### 初始代币发行（Initial Coin Offerings，ICOs）

在加密货币市场之外，也许与金融服务和区块链技术最引人关注的组合是市场中 ICO 的普及。 尽管存在许多金融市场创新的例子，但似乎增加的区块链采用和整合不断推动创新和产品开发，无论是在美国境内还是海外（Lewis，McPartland 和 Ranjan 2017）。 尽管 ICO 听起来可能像是一个过于技术化或抽象的概念，但在基本层面上，与首次公开发行（IPO）并没有实质性的不同。 金融服务专业人员几乎普遍熟悉并熟悉 IPO 的概念，这种概念中，一个组织以交换现金来筹集持续运营的所有权份额。 ICO 就组织的影响而言以类似方式运作，现金与组织发行的东西进行交换，但相似之处止步于此。 发行组织与投资者直接交换所有权份额以换取现金不同，发行组织交易的是一种不同类型的资产。

尽管在讨论之前，意识到一个现实是，为了使 ICO 能够顺利进行，发行组织（寻求资金的公司）必须使用区块链平台。 这一要求导致市场上可用的区块链选项数量大幅增加，但也导致监管不确定性增加。 就此书的写作和编辑而言，有关作为 ICO 一部分发行的项目和资产应如何在市场上计算的指导有限。 让我们看看通常与 ICO 过程相关的一些规格，这种过程似乎仅在增加：

1.  1.

    ICO 需要区块链才能发生 - ICO 与区块链技术之间的联系与加密货币和区块链技术之间的关系非常相似。 就像加密货币需要区块链才能正常运作一样， ICO 要求所有代币，无论其基本目的如何，都必须使用区块链技术发行。

1.  2.

    所有权可能会或可能不会交换 - 不像传统的 IPO 流程，其相对简单易懂（现金换取所有权），投资者为组织贡献的现金可能会也可能不会交换为组织的所有权。根据筹资的整体目标和管理团队的想法，投资者可能只是收到一枚代币，它是一种与直接所有权不同的资产类型。

1.  3.

    Tokens 是用于交换现金的东西 - 而不是在业务本身内部交换现金以换取股权所有权，ICO 在 2017 年至 2018 年之间是这样运作的，该组织筹集的现金被交换为代币。代币的具体技术细节不是本书的目的，但对代币代表的基本工作定义可以如下。代币只是对某种权利、产品、服务或最终所有权的一种选择，是一家通过 ICO 筹集资金的公司在将来某个时刻的一种选择。换句话说，代币可以被视为期权，这可能比简单深入技术细节更容易理解。在本文中进行了更彻底的分析，但现在让我们继续对话。

1.  4.

    监管仍在发展中 - 这可能看起来不像是一个惊人的惊喜，或者不应该是，考虑到区块链技术的萌芽性质。虽然区块链技术的概念自 2008 年左右开始在市场中得到分析和讨论，但当比特币（第一个真正规模应用）开始日益流行时，它真正引起公众的关注。ICO 只是区块链技术的最新迭代和演变，通过代表下一步 - 使用区块链筹集资本 - 由于市场变化而受到变化的监管的影响。

1.  5.

    ICO 并不一定更好 - 客户和潜在客户可能提出的最大问题和关注之一是，ICO 流程是否实质上比通过 IPO 流程简单筹集资金更好。虽然答案是独特的，并且会因组织而异，但事实是，由于监管的不确定性，看起来 ICO 并不是固有地比传统 IPO 更好或更适当。这可能是与某些客户进行的困难对话，特别是如果他们对整个加密货币市场感到非常兴奋，但这是必须进行的对话。

## Security Token Offerings

在撰写本书同时，也始终面临一个挑战，即尝试撰写关于新兴领域（如区块链或人工智能）新兴趋势的综合性文本时，技术不断演变和发展。随着 2018 年结束，迈入 2019 年，并且各种 ICO 市场的不断成熟和发展，两股不同的力量开始交汇。首先，随着 ICO 的数量和财务影响持续增加，监管关注和重点也持续增加并发展。这种增加的审查在 S.E.C.的 2018 年年度报告中也是明显的，报告中特别提到了 ICO 以及委员会计划在 2019 年及以后对市场采取的加强执法行动。这种增加的监管关注当然是这些 ICO 的受欢迎程度的逻辑副产品；加密货币和区块链公司寻求筹集资金的同时也想要避免一些 IPO 相关的合规成本和文件工作。

间歇性解决方案，也在本书中讨论，是利用空投来帮助寻求筹集资本并增加市场知名度的组织。虽然这一步骤与证券交易委员会（S.E.C.）和其他监管机构的监管和监督职权更加分隔，但很明显，与这一过程相关的会计、财务和合规问题仍在继续探讨。就目前而言，这些事件所涉及的税收、报告通过空投初始筹集的收益以及相关影响仍然是未决事项，但毫无疑问是各种监管和监督机构正在研究和审查的话题。一些人似乎认为，有担保的代币发行似乎提供了一种初期的加密货币领域的目标和使命与传统金融市场的混合。再次强调，金融服务专业人士不必成为加密货币和区块链领域所有方面的技术专家，但必须了解建立在这些平台上的应用程序以及它们与传统金融基础设施的交互方式。

在这个理念的核心，一个安全令牌发行实际上可以被分类为传统 IPO 流程和许多基于区块链的组织选择利用的首次代币发行之间的中间点。从合规和报告的角度来看，加密货币市场中 STOs 的实施和采用可能有助于解决当前可能使加密货币空间麻烦，令人困惑或高风险的一些当前未解决的问题。ICO 和 STO 之间的一个核心区别是，作为 STO 流程结果发行的代币由基础资产支持，组织的股份或组织利润的权利。然而，无论给该工具分配了什么标签，当分析 STO 空间时，有几个关键点需要考虑。然而，在检验其中一些关键点之前，必须谈论 STO 的一个显著点是这些活动得到了证券交易委员会的批准。此外，虽然许多 ICO 实际上不给投资者提供任何保护或分享管理组织的机会，但 STO 的概念包含了这两个方面。这可能看起来是一个相对简单的区分，但在市场确定性和这些投资选项将对金融谈话带来的影响方面，这是一个强大的区别。

在 2018 年末，证券交易委员会（S.E.C.）开始对参与 2017 年和 2018 年市场上各种 ICO 和其他代币发行的个人和机构采取并执行执法行动。这些执法行动中包括对相关组织和管理这些组织的个人处以有罪判决和数百万美元的罚款，表明监管机构和监管机构正在认真评估这个新兴领域。一项安全令牌发行似乎提供了 ICO 或其他潜在无监管区域与更传统的资本筹集模式之间的混合或桥梁解决方案。虽然仍在发展中，但从金融服务和会计和市场制造的角度来看，这绝对值得考虑。

## 智能合约

如果 ICO 的概念和想法是加密货币、区块链和金融服务之间最直接的联系，那么智能合约的概念可以说是区块链经济最引人注目和常被讨论的下一个应用步骤。不同的区块链网络和协议显然将有不同的批准和编码过程，但区块链与合同法之间的联系并不像它们最初看起来的那样抽象或不相关。合同法，以及对合同法细微之处的理解，本身构成了一个完整的专业领域，区块链并不能自动使金融专业人士成为合同法专家。尽管如此，自动化、商业进行方式的相互联系以及日益复杂的商业和融资安排意味着金融服务专业人士确实花了相当多的时间处理与合同相关的问题。

## 背景

然而，在深入分析和讨论金融服务确实与合同、协议以及对这些协议的解释如何紧密相连之前，让我们退一步。首先，会计信息几乎默认情况下是由对合同、协议和标准的解释和分析驱动的。无论这些协议和合同是基于与供应商、客户和合作伙伴的协议，还是受到新的 FASB 法规和标准的驱动，其潜在趋势是相同的。注册会计师和其他会计专业人士经常（无论是在公共实践中还是在私营行业内）花费大部分时间试图理解协议，并将这些协议转化为财务报告。其次，在原始人、贷款人和第三方之间的复杂协议越来越驱动着金融市场和从事全面市场活动的金融服务专业人员（商业贷款、投资银行业、交易业、信用交易业）。

不管个人对金融服务增加复杂性是否具有价值的意见或观点如何，事实仍然是，这种复杂性继续发生，并且这种复杂性可能会被加剧，特别是通过加密货币与当前未决会计问题的交集（Bruno and Gift 2019）。解释协议，向第三方解释协议，确保财务影响清晰是任何负责的受托人的基本职责。这也将这场讨论与智能合约对金融服务环境的影响联系在一起；加强合规性和审查。毫无疑问，全球各地，金融监管已经成为 2007-2008 年金融危机之后一个日益引起关注的问题。责任归咎于众多方，也一直这样，但毫无异议的是，事后看来，对某些金融工具中到底包含了什么产生了误解和错误解释。金融服务、风险和合规性之间的联系构成了智能合约市场演变可能有多么强大的基础。

显然，智能合约并不会在每种情况或每家公司都发挥作用，但金融服务专业人士有必要了解这对未来职业发展可能意味着什么。例如，审计本身可能会因不同组织之间信息的记录和自动记录而发生改变。对于涉及多方交易、大量文件工作和多家组织批准才能完成交易的行业和情况，智能合约的实施可能会是一个变革者。数据最终推动决策过程，不同公司处理、分析和持续行动不同数据片段的能力很可能决定成功或失败。深入了解智能合约的应用和可能性后，看一看这些项目到底代表着什么，似乎就很合适了。

## 深入研究智能合约

合同可能看起来是一个复杂的问题，有些合同确实可能非常复杂和详细，但合同的核心概念可以总结如下。无论行业关联，甚至合同中包含的具体细节，合同都可以被认为是推动业务协议的一系列（如果，那么）陈述。这些（如果，那么）陈述的组合反过来产生义务，确保权利，并确保不同组织明白交易的预期和回报。这显然是一个简化的观点，但为区块链技术、合同法和金融服务之间的相互连接提供了坚实的基础。

如果我们能接受合同是一系列陈述和条款的组合和融合，这些陈述和条款又会创建与涉及方相关的权利和义务，那么对智能合同本身进行更深入的分析就变得更简单了。进一步审视合同所包括和代表的内容还突显了为什么这个领域对区块链的颠覆和演进如此成熟。关于合同法、执行和审查的常见痛点包括但不限于以下内容：

1.  1.

    对合同条款的误解

1.  2.

    与合同细节相关的意识缺乏

1.  3.

    提供服务后付款的延迟

1.  4.

    工作要么未完成要么完成延迟

1.  5.

    与谁理解合同相关的透明度问题

1.  6.

    在公司内部丢失或错误标记文件形式的流动

1.  7.

    由于缺乏透明度而产生的争论和诉讼

1.  8.

    外部法律专家的高成本

1.  9.

    书写和批准合同的时间延迟

1.  10.

    效率的损失和管理时间的有效利用

任何曾经在组织内工作过，或者处理过合同，包括但不限于供应商协议、抵押贷款或其他复杂文件的人都意识到改进的潜力很大。回到合同作为（如果，那么）语句的组合的想法，区块链的核心功能似乎创造了一种情况，合同应用变得显而易见。区块链技术几乎通过技术平台的功能性质，提供了一个用于网络成员之间的信息传播和分发的实时平台。在目前阶段，区块链已经被开发为主要跟踪和监控不一定相信彼此的各方之间信息的流动。区块链经常被称为“信任的互联网”或其他变体，这回到了这个平台核心的基于共识的验证模型。即使在友好情况下，不管是组织之间还是个人之间曾经有过业务往来的情况下，合同的产生都有两个明显的原因。

首先，通过记录涉及方的条款、条件、义务和权利，与如果协议只是口头的相比，风险低，未来发生争议的可能性更小。区块链智能合约也可以帮助解决这个信任问题，要求合同中所有涉及方验证和批准已上传到平台上的条款和条件。除了这种默认增加了对最终文件的信任级别的必要验证之外，在私有区块链环境中还可以限制对不同类型信息的访问。在之前，这可能看起来是一个相对小的细节，但在潜在敏感的合同信息的背景下，这是一个巨大的问题。由于许多合同有条款、修正案，涉及不同层次的组织，对某些用户仅披露某些数据的能力至关重要。保持对专有流程和知识财产的保密性在不仅关乎业务如何进行，而且关乎组织如何未来相互作用方面变得越来越重要。

其次，智能合约执行条款、协议，并分配相关方的角色的实时性质，也代表了对当前合同管理和执行方式的显著改进。在处理常规合同和协议的处理延迟以及应对诉讼问题方面的时间延迟问题，已经是法律公司和法律专家正寻求改进的问题，并通过各种技术选项来解决。虽然技术工具的焦点和实施目前已集中在人工智能选项上（稍后详述），但区块链技术也开始成为一种可行的选择。信息传输，无论是改善律师事务所和法律专家的效率，还是改善客户体验，都是两个明显的量化权益，个人律师和律师事务所都可以实现，也应该实现。减少甚至消除与文件和文件分析相关的内部流动是区块链可以帮助解决的痛点，这些痛点常常是客户和律师投诉的原因。

第三，在前两条数据的基础上，加密在通信过程中的重要性和整合性。数据传输，无论其自然上的高效性如何，如果通信和数据被黑客入侵、窃取、违反或者暴露在市场中，将不会给商业流程增加任何价值。这不仅仅是一条关于确保更改密码的常规警告；数据入侵、违反和对组织和个人的影响是一个大生意。无论是国家赞助的黑客和行为者、公司间谍活动，还是为了个人利益而发动勒索软件攻击的个人，其基本现实情况仍然存在。一旦数据被侵犯和/或暴露给更广泛的市场，那些被黑客入侵的机构和其信息暴露给不法行为者的个人就会遭受负面后果。由于区块链本身，在其各种迭代版中，迄今尚未被黑客攻击，这种额外的安全和加密必然会为法律交易增加安全和保护。然而，在这一点上，需要划清一条细线，并承认与区块链相关的交易所和组织已经被入侵、黑客攻击和受到其他威胁的现实。

说了这么多，实时通信、加密以及要求所有合同条款都必须以基于共识的验证为支持，仍需看待为它们本质上就是原型和实验性程序。区块链本身虽然尚未被破解，但许多区块链技术与互联网其他部分交叉的应用和门户已经遭受了入侵。加密货币交易所、持有加密货币的钱包以及其他建立在区块链技术上的应用都经历了入侵事件，其中一些导致了这些程序和组织的崩溃。智能合约只是建立在基础区块链上的下一个更全面的应用程序，因此重要的是要认识到任何信息存储都将始终成为黑客和数据泄露的目标。

## 侧链和离链交易

目前，在区块链领域最有趣的工作之一可能就是侧链、离链交易和闪电网络的开发和实施。值得指出的是，在开发过程中，很多工作仍处于试点阶段，或者仍在各种组织的测试阶段。尽管如此，在区块链领域，对这些不同类型的进展的投资、兴趣和报道持续增加，全球一些大型金融机构都参与了这一讨论和研究。在讨论这些工具可能对会计专业未来意味着什么之前，确立工作定义来推动这一讨论显得十分恰当。

比特币区块链，作为闪电网络本身的基础，存在着一些问题和限制，这些问题和限制限制了加密货币和更广泛的区块链市场的采用程度。处理时间的延迟，记录、传输比特币区块链和交易所需的大量计算能力和电力，以及实际执行这些操作的技术要求，限制了这项技术实际上可能有多大的用处。现在，本分析关注闪电网络的原因如下：比特币区块链是全球范围内最大、最成熟、使用最广泛的区块链网络。开发这个闪电网络可能起源于简化比特币和相关比特币信息的传输方式，但对其他基于区块链的交易必然会产生影响。让我们来看看闪电网络究竟代表着什么，以及这对金融服务行业专业人士意味着什么。

闪电网络就好比是一种进行业务和交易的方式，使用加密货币，而不必承受目前与传统比特币交易相关的时间滞后和大量电能消耗。在业务交易的背景下，闪电网络似乎最适用，并对于两家机构或个人之间进行大量业务的情形最合理。例如，两个供应商、银行或供应链环境的其他任何组成部分，这些每天进行业务的情况在这种情况下是合理的，并且似乎很适合闪电网络。由于这些机构或个人已经彼此了解，基于先前交易历史建立了一定程度的信任，并且持续进行业务，因此认为并非每笔数据或交易都必须直接涉及到区块链。在确定是否适合开发和实施闪电网络的情况后，讨论的下一步应该集中在如何让这个想法启动和运行。

这在理论上看起来是一个相对简单的概念，但代表了比特币、其他区块链金融交易以及如何识别这些交易的方式的一个地质性变革。与完全依赖去中心化和半匿名基础进行来回交易和通信信息不同，闪电网络（目前的构成方式），闪电网络确实要求交易双方相互识别。虽然这确实减少了初始区块链对话的一些好处和优势，但这实际上使区块链更适用于金融服务交易。识别交易中涉及的各方，无论是个人还是机构，还允许区块链更符合反洗钱和了解客户法规等法规。适应并遵守这些金融法规对于更广泛地采用区块链进行金融服务至关重要。

将这个概念浓缩到基本术语，下一步将是打开一个称为付款渠道的东西（稍后再详谈），并在区块链上记录这个渠道的开启。现在，交易可以通过这个渠道在机构或个人之间进行，而无需触及区块链，直到付款渠道关闭。这样的渠道可以保持开启几个小时、几天、几周，甚至几年；分配的特定时间不重要。只有在该渠道的关闭时，无论何时发生，最终的交易总数才会被记录到区块链上。现在，这确实削弱了一些使区块链使用具有吸引力并成为分析和投资的焦点的安全性和隐私选项，但它似乎也解决了一些阻碍区块链扩展并在市场中占据领导地位的问题。引入付款渠道的概念在整个区块链领域引起了轰动，因为这似乎解决了与比特币区块链相关的一个根本问题。简而言之，比特币和比特币区块链相关的时间滞后和延迟将会保留。现在，还引入了一个新术语，即付款渠道的概念，所以让我们深入研究一下，看看这到底意味着什么。

## 付款渠道

付款渠道的核心理念与区块链技术的技术方面的名称并非毫无关联。简而言之，付款渠道是一个与区块链并行运行的离链网络。换句话说，这些交易及与这些交易相关的信息并非在每一时刻直接存储在区块链上。这样的安排解决了目前与这项技术相关的一些不足之处，包括处理速度的滞后和处理某些交易所花费的时间。通过使用智能合约（记住那些被嵌入到区块链的自动协议），它允许两个或多个相连的当事方在无需向网络广播每笔交易的情况下执行交易。相反，在付款渠道的生存期内（可以是从几天到几年），单个交易被存储在离链上。当渠道关闭时，最终余额会被挖掘/确认，然后加入到区块链中。

将这个概念付诸实践代表了支付通道对话中的下一个逻辑步骤。也就是说，一个公司或个人如何实际着手实践这个概念呢？如果两个个人或机构想要安排并使用支付通道，那么这个过程的第一步就是将资金存入通道中。以比特币为例，支持闪电网络，个人或机构将比特币存入通道。使用“多签”地址，允许多个参与方之间发送和接收比特币或其他信息，并在交易结束之前等待，然后才将这些变化广播到网络本身，以完成通道的建立。对于金融和交易行业来说，另一个可能更深远的影响是，个人或机构不需要直接之间进行通道交易才能使支付通道正常运作。只要有一条路径，利用已存在的通道，个人或机构就可以与他人进行交易，支付通道协议就可以派上用场。已被多个组织或个人构建并使用的任何支付通道的关闭过程都可以由该通道的任何单个参与方完成。与使用完整的区块链来验证和发布交易块相比，利用基于闪电的网络有几个明显的好处。

1.  1.

    更便宜的交易处理。与不得不支付矿工来验证并发布每个交易块，而且不要忘记，每个块（至少在比特币区块链上）的大小只能是 1 MB，支付通道的成员只需在通道开启或关闭时支付费用。对于通过支付通道进行数百甚至数千次交易的实体来说，这可能代表了一个重大的节省机会。

1.  2.

    提高速度。在比特币区块链上，作为闪电网络的基础和支持，每个交易块的处理速度最多可能需要 10 分钟（或更长时间）才能验证并发布到区块链上。然而，通过支付通道协议，交易处理的速度的唯一限制就是参与方所使用的互联网连接速度。

1.  3.

    可扩展性。在利用传统区块链时，无论是比特币区块链还是以太坊区块链，最难解决的问题之一是它们都不太具有可扩展性。慢慢的交易处理速度，以及建立和维护这些网络的成本意味着，除了市场上最大的一些组织外，扩展区块链并不是一个可行的目标。然而，通过支付通道的实施和利用，这样的扩展不仅有可能，而且非常实用。

1.  4.

    安全性。由于支付渠道使用数字签名，特别是多重签名协议需要所有参与方在交易得到验证前签署，并使用哈希时间锁合约（HTLCs）来确保只有预期收件人获得预期的币种，支付渠道在市场上代表着一个安全选项。HTLCs 的特性是有时间限制的，因此涉及到您的交易的各方必须声明收到节点或其他信息，以便交易实际发生并记录。

1.  5.

    隐私性。由于在支付渠道中发生的个体交易之间，没有向整个网络广播，直到该渠道本身关闭。一旦这些最终余额在区块链上发布，它们几乎不可能被追踪到参与其中的个人。

## 空投活动

尽管向市场引入新加密货币或代币的主要方式是通过首次代币发行（ICO）过程，但是对这一领域的增加监管审查导致个人和组织寻求该过程的替代方案。具体而言，仍在依赖 1946 年的豪伊测试来确定和指导代币发行的分类和交易过程的美国证监会（S.E.C.）试图遏制该领域周围的热情。虽然围绕改进和更新该领域法规的许多讨论和辩论已经进行，但它仍然是一个模糊的领域，吸引了众多监管机构的关注。除了监管对话外，2018 年还就区块链、加密货币的现状以及这些对整个金融服务领域的影响进行了许多圆桌会议、辩论和听证会。而现在，尽管空投活动特指发行新兴加密货币，但整个过程 - 如同整个加密资产经济一样 - 都依赖于基础的区块链技术。

不需要翻译。

不需要翻译。

### 章节 4 总结

第四章直接深入讨论与区块链、加密货币相关的最重要的主题和特征，它将其与更广泛的技术趋势以及这些技术对会计和其他金融服务的影响联系在一起。区块链可以说是进入金融和会计术语库的最热门和最引人注目的话题之一。但即使有了如此多的关注，似乎客户和从业者双方对这方面仍然存在理解和领悟上的差距。这一章旨在区分市场上可用的不同类型的区块链选项，以及网络本身通过哪些方法对数据进行验证和验证。建立这些差异是重要的，因为这构成了平台的核心，并使其以客观和可量化的方式脱颖而出。与世界上几乎所有其他数据输入或存储系统不同，在区块链平台上上传和存储数据需要至少部分网络成员在上传数据时批准和验证数据。具体情况会因不同的区块链而异，但团体数据验证这一整体主题在区块链平台上是保持一致的。这一章详细分析了市场上存在的特定共识批准方法，并分析了这些不同方法对商业交易的意义。

### 反思问题 – 第四章

1.  1.

    安全代币发行、首次代币发行和空投之间有何异同？

1.  2.

    支付通道是否可能成为更广泛的区块链和加密货币采用的关键和潜在承诺？

1.  3.

    智能合约有很多潜在的用例，包括一些金融服务领域；有哪些最有前途的痛点可以通过智能合约来解决？

## 补充阅读

Blockgeeks – 区块链共识协议的基础入门：[`​blockgeeks.​com/​guides/​blockchain-consensus/​`](https://blockgeeks.com/guides/blockchain-consensus/)

Medium – 区块链共识算法及不同类型共识模型是什么：[`​medium.​com/​@BangyTech/​what-is-consensus-algorithm-in-blockchain-different-types-of-consensus-models-12cce443fc77`](https://medium.com/@BangBitTech/what-is-consensus-algorithm-in-blockchain-different-types-of-consensus-models-12cce443fc77)

Coindesk – 一份关于共识协议的简短指南：[`​www.​coindesk.​com/​short-guide-blockchain-consensus-protocols`](https://www.coindesk.com/short-guide-blockchain-consensus-protocols)

Blockgeeks – 工作证明与股权证明的比较：[`​blockgeeks.​com/​guides/​proof-of-work-vs-proof-of-stake/​`](https://blockgeeks.com/guides/proof-of-work-vs-proof-of-stake/)