第八章

# 基于区块链的 IoT 安全和隐私访问控制框架，具有强大的匿名性、不可链接性和难以推测性保证。

Aafaf Ouaddah    ^(Mchain, Admirals Way, Canary Wharf E14 9UH, London, United Kingdom)

## 摘要

受到区块链近期爆炸性增长的兴趣的启发，我们检查它们是否适合构建一个轻量级且健壮的访问控制框架，以解决物联网（IoT）领域的安全和隐私问题。在这个方向上，本章讨论了中心化模型保护物联网的局限性，并提出区块链方法作为成功的分布式系统的例子，以为物联网设备带来安全和隐私。在这个方向上，我们介绍了 FairAccess 和 PPDAC，作为一个基于新兴区块链技术的轻量级和隐私保护访问控制框架，主要是无许可和公共类型，以确保对物联网设备的细粒度访问控制功能，为 IoT 最终用户提供强大的匿名保证。所提出的框架保留了区块链的优势，以满足 IoT 安全和隐私的需求，同时克服了将区块链整合到物联网中所面临的挑战。

### 关键词

区块链；物联网；隐私；智能合约；访问控制；CP-ABE

## 1 引言

二十年前，科幻小说中描述的日常物品可以感知、分析、存储或交换信息的世界只存在于科幻小说中[[1]](S0065245818300676.xhtml#bb0010)。如今，随着硬件技术的快速发展，这样的场景越来越成为现实。事实上，Gartner 将物联网（IoT）确定为十大战略技术趋势之一^(a)，思科预测到 2020 年将有 500 亿台连接设备^(b)，市场潜力超过 14 万亿美元^(c)。物联网已经在这里。物品通过启用全新范围的应用程序来扩展我们所处的世界。能够在我们周围随处放置一堆强大、微小和廉价的计算机，使得我们能够以比以往任何时候都更精细的空间和时间分辨率监控和与物理世界进行交互。然而，由物体主动和自主地进行通信所提供的应用场景和市场机遇远远超出可预见的地平线[[2]](S0065245818300676.xhtml#bb0015)。

物联网（IoT）既是一个全球物理基础设施，也是一个涵盖许多现有和不断发展的互操作信息和通信技术（ICT）的大伞术语，这些技术相互连接，设备、物体和服务 [[3]](S0065245818300676.xhtml#bb0020)，越来越多地部署在工业控制、医疗保健、航空、家庭自动化、零售、交通、可穿戴设备等各个领域 [4,[5]](S0065245818300676.xhtml#bb0030)。这场革命，也被称为物联网 [[6]](S0065245818300676.xhtml#bb0035)，万物互联或雾计算网络 [[7]](S0065245818300676.xhtml#bb0040)，在这里智能物体相互通信，并与互联网中的计算机以智能 [[8]](S0065245818300676.xhtml#bb0045)和机器对机器的方式进行通信 [[9]](S0065245818300676.xhtml#bb0050)，旨在重新定义人类、工作和技术的整个关系 [[10]](S0065245818300676.xhtml#bb0055)。

然而，正如法国理论家和城市规划师保罗·维里奥所引用的：“当你发明了船，你也发明了沉船……每一项技术都伴随着自己的负面，这在技术进步的同时也被发明出来”[[11]](S0065245818300676.xhtml#bb0060)。这句智慧的格言给了我们一个雄辩的理解，即如果我们能够克服其主要的安全和隐私问题，物联网将成为一项革命性的技术。实际上，在某种程度上，由于大多数物联网设备使用的简单处理器和操作系统不支持复杂的安全方法，物联网正在带来新的安全挑战。此外，物联网边缘设备缺乏身份验证和授权标准，导致了对机密性和身份验证的恶意攻击，对服务完整性的悄无声息的攻击，或对网络可用性的攻击，如耗尽电池的睡眠拒绝服务攻击，或服务拒绝（DoS）攻击[12,[13]](S0065245818300676.xhtml#bb0070)。

另一方面，隐私问题同样严重。实际上，物联网设备本质上是“信息的收集者和分发者”[[8]](S0065245818300676.xhtml#bb0045)，因此它们对个人隐私构成了巨大挑战[14，[15]](S0065245818300676.xhtml#bb0080)，特别是物联网设备无处不在地存在于用户的日常生活中，并且用户与智能物体的无所不在的互动。除了第三方无序、自动和隐蔽地收集细粒度数据外，缺乏透明度还可能不断地让用户面临诸多威胁，例如：身份识别、定位和跟踪、监视、监控、操纵、个人资料、数据关联、侵犯隐私的互动和呈现，甚至社会工程学[16，[17]](S0065245818300676.xhtml#bb0090)。隐私策略和隐私设计是两种新兴方法，由学术文献引发[18–20]，用于增强物联网中的隐私。隐私策略旨在保护数据免受意外披露或滥用，并促进知情的消费者选择[21，[22]](S0065245818300676.xhtml#bb0115)，而隐私设计则促使在整个工程过程中实施隐私，采用积极主动和预防性的方法，而不是事后[23，[24]](S0065245818300676.xhtml#bb0125)。结合这两种方法已被证明对于概念化和缓解与物联网相关的潜在风险至关重要，尽管这仍然是一个高度争议的问题。

不幸的是，目前的解决方案几乎无法跟上这些新出现的挑战。因此，迫切需要新的安全和隐私工程实践和分布式架构，以便妥善解决物联网的主要挑战。因此，我们的研究关注的是如何通过区块链技术的去中心化，主要是无许可和公共类型，来提供隐私保护的物联网对象访问控制解决方案，以及在这样做时的优势和劣势。为此，我们在物联网场景中引入了 FairAccess [25,[26]](S0065245818300676.xhtml#bb0135)作为一种新颖的分布式隐私保护访问控制框架，其结合了访问控制模型和加密货币区块链机制。在 FairAccess 中，我们提出使用智能合约来表达细粒度的访问控制策略，以做出授权决策。我们选择授权令牌作为访问控制机制，通过新兴的加密货币解决方案进行交付。我们首先使用公共区块链来确保在无中央权威/管理员的分布式环境中评估访问策略，并确保所有互动实体将正确执行策略，其次是确保令牌重用检测。然而，区块链账本的公共性可能初看起来似乎与某些访问控制策略的私密性相抵触。为了解决这个问题，本立场章节提出了一个隐私保护的分布式访问控制（PPDAC）方案，以与 FairAccess 集成。PPDAC 使用分布式密文策略属性基加密(DCP-ABE)技术的白盒版本，以在公共区块链中增加一个隐藏敏感属性和私密访问控制策略的隐私层，同时保持验证过程透明和公开。此外，利用密码学中最近的零知识证明协议“zk-SNARK”等协议，使我们的框架能够保证物联网最终用户的高匿名性和难以追踪性。

本章的剩余部分组织如下：第二部分 从定义物联网在安全和隐私方面的具体要求开始。它讨论了集中式方法的缺点和在物联网环境中分布式方法的优势。第三部分 提出了区块链方法作为一种有望实现物联网安全的分布式技术。接下来将简要概述区块链技术。第四部分 通过名为 FairAccess 的基于区块链的分散式和用户驱动的访问控制框架来调查我们提出的确保智能对象安全的方法，并讨论了我们在使用公共区块链时所面临的限制，主要是隐私和可追溯性问题。第五部分 通过 PPDAC 方案在区块链上添加隐私层来解决定义的问题。最后，第六部分 总结了本章。  

<hgroup>

## 2 问题陈述和研究问题

### 2.1 物联网安全和隐私需求

</hgroup>

由于物联网具有异构设备、动态性、多领域应用和未定义的边界，因此其面临重大的隐私和安全风险。因此，安全研究人员更难以找到当前安全挑战的综合解决方案。因此，理解、定义和分析这些要求的重要性变得至关重要。事实上，每个领域应用都有其特殊性，这些特殊性通常取决于该领域中的上下文和设备之间的交互，当处理安全和隐私要求时必须考虑到这一点。为了实现这一目标，我们进行了深入分析，支持以结构化形式规范安全和隐私要求的说明。在我们的研究中，我们首先将这些要求定义为六个组：隐私、机密性和完整性、可靠性和可用性、社会和经济方面、技术约束和可用性。主要的六个安全和隐私要求以及它们的子组件显示在图 1 中。

![图 1](img/f08-01-9780128171899.jpg)

图 1 物联网的安全和隐私要求 [[27]](S0065245818300676.xhtml#bb0140)。

随后，我们列出了物联网的不同应用领域，并详细说明了每个领域的特点和安全要求。事实上，我们将这些应用程序分为三个领域：（1）个人和家庭：个人、家庭和医疗保健的规模。(2)政府和公用事业：社区、国家和地区的规模。(3)企业和产业：产业和大公司的规模。此外，我们概述了物联网中受限设备的不同分类和分类。

该研究得出以下结果：一目了然，就个人和家庭类别而言，针对该类别的访问控制解决方案需要以专有、原始但用户友好的方式保护终端用户的隐私。此外，安全解决方案针对企业和工业类别的可用性和可靠性需求是突出的目标，而针对政府和公用事业应用程序来说，机密性和完整性需求占主导地位。然而，观察到整个类别通常在合作与协作原则、开放性/互操作性、高可扩展性、灵活性和分布方面有共同需求。图 2 描绘了各种物联网领域应用与安全需求之间的关系。

![图 2](img/f08-02-9780128171899.jpg)

图 2 物联网领域应用分类及其安全需求[[27]](S0065245818300676.xhtml#bb0140)。

### 2.2 当前物联网访问控制架构的状态及相关挑战

将物理对象集成到互联网基础设施中需要应用轻量级安全机制，即使在受限环境中也要使用。然而，当前的安全标准和访问控制解决方案并未考虑到这些方面。它们无法满足这些新生态系统在可扩展性、互操作性、轻量级和端到端安全方面的需求[[27]](S0065245818300676.xhtml#bb0140)。这些挑战引起了研究界越来越多的关注，最近一些努力开始朝着这个方向出现。然而，这些解决方案可以分为以下三种方法（见图 3）：

+   • 集中式架构

    这种方法是将物联网设备的访问控制相关操作外包给可信的第三方实体。这个实体，也称为策略决策点（PDP），可以由后端服务器或直接连接到它管理的设备的网关实例化。它负责根据存储的访问控制策略分析访问请求。因此，希望访问由终端设备提供的数据的请求者被要求经过这些受信任的第三方。这种架构的好处在于解除了受限设备（即传感器、执行器）处理繁重访问控制功能的负担，从而使得可以使用标准访问控制技术，如 SAML 和 HTTPS（以安全方式传输身份验证信息），XACML（定义复杂的访问控制策略）等。然而，在物联网环境中，这种架构存在一些主要缺点，列举如下：首先，引入可信的第三方导致端到端安全性受损。其次，在这种架构中，物联网设备的角色在决策过程中受到严格限制。因此，制定智能授权策略，其中访问控制决策基于即时从物联网终端设备环境收集的上下文信息，是非常具有挑战性的。第三，资源所有者（RO）访问控制策略以及用户的授权请求都被透露给了可信方。因此，资源所有者或请求者的隐私被破坏。第四，PDP 仍然是一个可能破坏整个网络的瓶颈和故障点。当它直接与关键的物联网服务挂钩时，这一点尤为重要。

+   • 分布式架构与可信实体

    在这种方法中，设备部分参与访问控制决策的制定。其主要作用是收集其周围环境的上下文信息（位置、温度、湿度、电力水平等），并将其发送给受信任的第三方。这个受信任的第三方接收访问控制请求，并根据预定义的策略和从智能对象收到的上下文信息做出决策。与集中式方法一样，这种架构使得可以利用已有的授权技术，而无需在受信任的第三方和连接设备之间制定连接来传输上下文信息。然而，在这种情况下，必须采取额外的安全措施来保护受信任的第三方和终端设备之间的通信渠道，以保护传输的信息。此外，终端设备必须配置为提供或不提供其收集的数据。此外，将上下文信息传输给受信任方可能无法以即时方式完成，这意味着不推荐在需要实时决策访问的用例中使用此架构，例如医疗保健场景或 SCADA 系统。最后，不考虑资源所有者和请求者的隐私。

+   • 分布式架构

    分布式方法包括在设备端定位和嵌入处理访问控制决策的智能。这种方法与物联网的真正本质完美匹配，物联网的智能位于网络边缘。就资源所有者和请求者的隐私而言，它提供了许多令人印象深刻和有前景的优势，因为没有信任的第三方参与。通过边缘智能原则，最终用户更能够通过定义自己的策略来控制对自己设备的访问。此外，实时进行智能访问控制决策的可能性得到了提供。此外，与前两种方法相比，由物联网设备生成的数据的成本管理更为廉价，因为前两种方法需要为每个连接的智能对象提供云后端。在分布式方法中，设备只有在必要时才被授权发送信息。最终，端到端的安全性可以得到实现。

![图 3](img/f08-03-9780128171899.jpg)

图 3 物联网中的现有访问控制架构。

然而，该方法中最具挑战性的障碍源自现有访问控制技术的固有特性，如 RBAC [[28]](S0065245818300676.xhtml#bb0145)和 ABAC [[29]](S0065245818300676.xhtml#bb0150)以及 OAUTH [[30]](S0065245818300676.xhtml#bb0155)，这使得它们在资源受限设备上的实现不可行[[31]](S0065245818300676.xhtml#bb0160)。

因此，必须付出大量努力来深入分析调整现有访问控制模型的可行性，或者定义满足分布式访问控制方法要求的新提议。

### 2.3 总结

集中式和去中心化的信任实体方法是通过云服务器支持巨大的处理和存储容量来识别、验证和连接所有设备的方法。尽管这种模式几十年来一直用于连接标准计算设备，并且将继续适用于小规模的物联网网络[[32]](S0065245818300676.xhtml#bb0165)，但由于以下原因，它严重难以满足明天庞大物联网生态系统的增长需求[33–35]。

+   • 成本：现有的物联网解决方案很昂贵，主要有两个原因：（1）高维护成本：从制造商的角度来看，集中式云、大型服务器农场和网络设备由于在设备停产多年后仍需要分发软件更新而具有高昂的维护成本[[36]](S0065245818300676.xhtml#bb0185)。（2）高基础设施成本：当存在数十亿物联网设备时，需要处理的通信量庞大，需要处理非常大量的消息（通信成本）、设备生成的数据（存储成本）和分析过程（服务器成本）。

+   • 瓶颈和单点故障：云服务器和农场将继续是可能导致整个网络中断的瓶颈和故障点。这在它直接与关键物联网服务（如医疗保健服务）紧密联系时尤为重要。

+   • 可扩展性：在集中式范式中，基于云的物联网应用平台从位于数据采集网络中的实体获取信息，并向其他实体提供原始数据和服务。这些应用平台控制着整个信息流的接收。这种执行创建了一个瓶颈，无法将物联网解决方案扩展到呈指数增长的设备数量以及这些设备生成和处理的数据量（即“大数据”概念）。

+   • 安全性不足：从数百万设备收集的大量数据引发了个人、企业或政府的信息安全和隐私担忧。正如最近对物联网设备进行的拒绝服务攻击所证明的那样[[37]](S0065245818300676.xhtml#bb0190)，连接到互联网的大量低成本和不安全的设备正在成为确保物联网安全的主要挑战。

+   • 隐私泄露和缺乏透明度：在集中式模式中，从消费者的角度来看，服务提供商获取数十亿实体收集的数据的行为缺乏可辩驳的信任。在这个超级连接的世界中，需要一种“透明度安全”的方法，允许用户保持匿名。

## 3 解决方案：通过区块链以无需信任的方式去中心化物联网网络

分布式的物联网网络化方法将解决上述许多与中心化相关的问题。分布式物联网的概念并不新颖。事实上，许多学术和工业文件将其视为将物联网梦想推向现实世界的最有前途的方法之一。Panikkar 等人[[36]](S0065245818300676.xhtml#bb0185)指出，对于不断扩大的物联网设备生态系统而言，向去中心化架构转变是可持续的需求。已经明确提到，发展去中心化的自主架构和将智能定位在网络的边缘是需要解决的问题。我们认为，区块链为上述问题提供了一种优雅的解决方案。

### 3.1 区块链现象：去中心化的新浪潮

最初由 Satoshi Nakamoto 在 2008 年[[38]](S0065245818300676.xhtml#bb0195)引入，用于支撑比特币加密货币网络，区块链已经吸引了科技行业和金融界的大部分关注。作为一个安全和去中心化的计算基础设施，它被广泛认为是解决中心化、隐私和安全问题的颠覆性和高效的解决方案，用于记录、跟踪、监视、管理和共享不仅仅是金融交易，还包括出生和死亡证明、结婚证书、产权证书、教育学位、金融账户、医疗程序、保险索赔、投票、食品溯源以及任何可以用代码表示的价值[39–41]。

在本章中，我们将重点研究区块链的公共和无需许可类型。然后，我们将后文定义为用于交易处理的分布式数据库。区块链中的所有交易都存储在单个分类帐中。区块链技术是建立在四个基本构件之上的，每个构件都具有关键属性，并且每个属性都通过特定的机制实现。

我们认为区块链技术依赖于以下构件，如下所述：

1.  (1) 识别交易的来源和目的地：在基于区块链的生态系统中，用户使用称为“地址”的数字身份来发送和接收交易。这些地址应具备以下关键特征：

    +   • 自我发行和独立：用户应能够自动生成匿名的（例如使用软件）交易身份（例如，在比特币系统中使用公钥的加密哈希）与任何给定的权威（例如政府、企业等）无关。

    +   • 匿名性：交易身份应该是匿名的，即不透露其所有者的真实身份，以满足用户隐私的需求，因此数字身份的真正匿名性需要具备自我发布功能以外的特征。它还需要具备不可链接性和不可追踪性的特征。

    +   • 保护隐私的可验证性：系统中的任何实体都应能够验证数字身份的安全性。在保护所有者身份隐私的同时，需要一种公开验证算法来验证任何给定（匿名）交易身份的信任来源。

1.  (2) 交易：交易记录了价值（代币）从某个源地址到目标地址的转移。交易由发送方生成并广播给对等网络。除非交易已记录在交易的公共历史记录中，即区块链中，否则交易无效。最终，使用区块链技术进行交易处理应满足以下属性：

    +   • 专有：只有授权执行交易的所有者可以使用自己的身份地址。

    +   • 不可逆：一旦交易进入账本，就应无法修改其信息或删除它，否则将有效地撤销交易。

    +   • 公开可验证：交易的验证算法应使网络中的任何节点能够验证交易的有效性。

    +   • 免疫性：一旦交易记录在区块链中，就不能在未被其他节点检测到并拒绝的情况下进行更改。此外，如果交易符合账本协议，它应最终被添加到账本中。

1.  (3) 自动处理交易的条件：通过区块链传输任何价值（例如，代币）或通过区块链执行任何函数都应受到逻辑条件（例如，合约）的限制，这些条件必须编写为代码并由网络中的节点自动执行。此条件应自动执行。

1.  (4) 共识：网络中的每个用户或节点都依赖于算法强制执行的规则来处理交易，无需人为干预即可验证协议的正确执行，并获得相同的结果。每个节点的账本与网络中的所有其他用户或节点完全相同。这确保了所有用户或节点在相应货币的区块链中达成完全共识。

区块链机制：为了满足上述特性，一套密码学机制已经被引入，如下所述并在图 4 中描述：

![图 4](img/f08-04-9780128171899.jpg)

图 4 区块链的构建模块和机制。

公钥密码学：实现了自行颁发的、匿名的、且保护隐私的身份识别。数字签名：用于满足交易的专有性和公开可验证属性：系统中的每个用户至少拥有一对私钥和公钥；公钥公开发布用于确定数字身份，而私钥用于由其所有者（或代表其的值得信赖的方）签署相应的交易。

+   • 签名的有效性与发送者私钥的掌握有关（专有）

+   • 任何知道发送者公钥的人都可以验证签名（公开可验证）

+   • 如果交易的任何参数发生改变，签名将无效。

哈希函数[[42]](S0065245818300676.xhtml#bb0215)和默克尔树[[43]](S0065245818300676.xhtml#bb0220)：用于解决区块链系统中交易的不可变性、不可逆转性和公开验证的问题。将交易分布到时间顺序块中，并通过其密码哈希对每个块进行时间戳，从而实现了这些特性。

交易使用默克尔树（Merkle tree），也称为二进制哈希树，在每个块中进行总结。它是一种有效的数据结构，用于总结和验证大量数据的完整性。将块组织成有序链（区块链），其中每个块都指向前一个块，是中本聪引入的一种巧妙技术，使得删除或替换整个块变得不可行。为了简化区块链的验证，关键块参数（如默克尔根）被收集在块头中。因此，提供交易的不可变性等同于提供区块头的不可变性。

交易的不可变性特性是通过哈希函数的属性实现的。实际上，交易中的任何更改都会导致块的默克尔根发生变化，而默克尔根是其头部的一部分。因此，要更改单个块，攻击者还必须更改分类帐中的所有后续块，这是不可行的。

在（工作/堆栈/空间等）共识协议中证明 X 的方法：一旦交易被创建，就会在网络中广播，并且每个节点都会独立验证收到的交易并将其包含在一个区块中。然而，每个节点可能对区块链有不同的视图，导致区块链的分支发散。为了缓解这个问题，在网络中需要一种分布式机制来在不信任的参与者之间达成共识。这个问题在历史上被称为“拜占庭将军”（BG）问题，这在文献中提出过[44]。在分布式环境中达成共识是一项具有挑战性的任务。实际上，网络的共识可以通过多种方式实现，包括工作证明（例如比特币中使用的方式）、权益证明（例如 Nxt）、委托权益证明（例如 BitShares）和实用拜占庭容错（超级账本项目）。有关更多详细信息，我们建议读者参考这四种方法的全面调查文献[45, 46]。

智能合约/脚本语言：用于满足自动处理属性。脚本语言描述了在堆栈机器上执行某个程序的过程。每个交易包含一个脚本，该脚本锁定或附加了该交易转移的价值。脚本是每个交易的输入和输出的一部分。当我们将这种脚本语言计算推广到任意图灵完备逻辑时，我们就得到了一个富有表现力的智能合约系统。自 2014 年以来，对智能合约应用的兴趣稳步增长，这是因为出现了类似比特币的技术，如以太坊[[47]](S0065245818300676.xhtml#bb0240)和许多其他专门设计用于分散式智能合约系统的工作。智能合约是存储在区块链中的自执行的加密“盒子”，只有在满足某些条件时才能解锁其中的价值。

### 3.2 为什么选择区块链作为解决方案

区块链技术和物联网提供了一个充满希望和迷人可能性的新世界。实际上，区块链的去中心化、自治和无需信任的固有能力使其成为物联网解决方案的基础组成部分的理想选择。它有可能改善物联网行业[[48]](S0065245818300676.xhtml#bb0245)，并显著有助于实现去中心化[[49]](S0065245818300676.xhtml#bb0250)和私有设计的物联网[[50]](S0065245818300676.xhtml#bb0255)的愿景。

区块链的以下显著特点，如图 5 所示，使其成为解决物联网中上述安全性和隐私挑战的理想技术：

+   • 去中心化和无需信任：缺乏中央控制确保了通过使用所有参与节点的资源并消除多对一的流量流向来实现可伸缩性和健壮性，从而减少了延迟并克服了单点故障的问题。

+   • 追加方式。区块链的主要设计目标是使得从区块链中删除信息（即，撤销交易）是不可能的，或者至少成本过高。

+   • 伪匿名性：所提供的固有匿名性非常适合大多数物联网用例，其中用户的身份必须保密。

+   • 透明性：网络中的每个节点都可以独立验证分类帐的当前状态，并得出与网络其余部分相同的结论。

+   • 密码学模型：对区块链的信任不是来自维护分类帐的权威，而是来自系统中使用的密码协议的数学合理性和攻击的经济成本的限制。

![图 5](img/f08-05-9780128171899.jpg)

图 5 结合区块链与物联网的好处。

然而，采用区块链处理物联网中的授权功能并不直接，需要解决以下关键挑战：

+   • 区块链的公共性与访问控制策略的私密性

+   • 可解性问题

+   • 共识过程特别是在计算上密集，耗时，而大多数物联网设备资源受限，大多数物联网应用程序需要低延迟。

先前定义的问题陈述导致以下研究问题：

1.  1 如何通过利用公共且无许可的区块链技术解决物联网中的访问控制挑战？

1.  2 如何为受限制的物联网设备提供轻量级访问控制框架，尽管公共区块链中采用的共识协议需要大量计算资源？

1.  3 如何实现隐私保护的访问控制解决方案，隐藏用户的访问控制策略，并解决公共区块链中常见的可追踪性和个人资料问题？

## 4 FairAccess：使用区块链技术作为访问控制基础设施

为了回答上述问题，我们提出了一个由两个主要模块组成的框架，即 FairAccess 和 PPDAC，如 图 6 所示。在下一节中，我们将概述并简要描述这两个协议。

![图 6](img/f08-06-9780128171899.jpg)

图 6 我们提出的解决方案。

### 4.1 FairAccess：使用区块链技术作为访问控制基础设施

FairAccess [25, 51] 是基于区块链技术的新型分布式访问控制框架，首次将访问控制模型和加密货币区块链机制结合起来。在 FairAccess 中，我们提议使用 SmartContract [[47]](S0065245818300676.xhtml#bb0240) 来表达细粒度和上下文访问控制策略，以做出授权决策。我们选择授权令牌作为访问控制机制，通过新兴的加密货币解决方案进行交付。我们使用区块链来确保在没有中央权威/管理员的分布式环境中执行访问策略，并保证所有交互实体都能正确实施策略（图 7）。

![图 7](img/f08-07-9780128171899.jpg)

图 7 FairAccess 的构建模块。

授权令牌：在我们的 FairAccess 框架中，我们将授权令牌定义为一种数据结构，表示由智能合约的创建者定义的访问权限或权利，生成授权令牌，以便与此智能合约进行交互的实体访问由其地址标识的特定资源。如果设备呈现的授权令牌是由与管理该设备的其他设备或服务关联的智能合约提供的，则访问将被授予。实际上，区块链技术强制执行的基于令牌的访问控制在物联网环境中提供了许多优势。实际上，在区块链上安全保存令牌意味着智能设备可以轻松验证访问令牌的有效性，从而减轻了物联网受限设备处理大量与访问控制相关信息的负担，同时减少了将这些功能外包给可信强大实体的需要，从而阻止了端到端安全性的实现。此外，它减少了通信成本，因为获取令牌只需要签名而不需要进一步的身份验证机制。同样，资源所有者可以通过在区块链上放置所请求数据的资源哈希来管理和更新他的众多和异构设备的访问权限。然后，设备可以读取哈希并检查更新的访问控制配置。该哈希可以随着与区块链的每次新连接而更新。如果访问控制逻辑位于设备端，特别是对于放置在难以到达或几乎无人关注的位置的设备，例如智能停车系统中直接嵌入沥青中的设备，这可能会使访问控制策略的管理和更新变得更加容易。此外，令牌可以用于许多访问控制操作，例如更轻松灵活地获取、委托、撤销甚至更新访问。

区块链：FairAccess 使用区块链提供了几种有用的机制。实际上，在 FairAccess 中，区块链被视为数据库或策略检索点，所有访问控制策略都以交易形式存储；它还充当日志数据库，确保审计功能。此外，它通过交易完整性检查防止令牌伪造，并通过双重支付检测机制检测令牌重复使用。

智能合约：智能合约在区块链上有自己的账户，而区块链支持基于账户的模型[[47]](S0065245818300676.xhtml#bb0240)。它允许我们在代码中表达逻辑功能。它作为自主的参与者运行，其行为完全可预测。因此，它们可以被信任驱动任何可以表达为对链上数据输入函数的链上逻辑向前推进，只要它们需要管理的数据在它们自己的范围内（在上面的示例中，合同将无法交易它不拥有的资产）。此外，由于所有与合同的交互都通过区块链上的签名消息进行，所有网络参与者都可以检查其代码，所有与合同的交互都可以得到加密可验证的合同操作的痕迹。

这使得我们的框架能够表达细粒度的访问控制策略。实际上，策略是一组规则和条件（基于特定上下文或属性等），请求者实体必须满足才能获得访问令牌并访问特定资源。这些规则可以由任何访问控制模型表示，但必须转换为被视为锁定脚本的脚本语言，放置在交易输出上。幸运的是，正在开发新的区块链协议，包括完全的图灵完备性能力，允许任何人编写智能合约和具有自己任意规则的分散应用程序，用于所有权、交易格式和状态转换功能[[47]](S0065245818300676.xhtml#bb0240)。使用这些高级语言，如以太坊，肯定会使我们的 FairAccess 框架能够表达细粒度的上下文感知访问控制策略。我们相信智能合约是一个有前途的新兴领域，可以用来表达一般和特别是在物联网中的细粒度、上下文和合同访问控制模型。

### 4.2 FairAccess 的架构

我们分散式访问控制框架的愿景是一个围绕一个或多个资源所有者的自治组织系统，其拥有一个或多个资源，这些资源被识别为具有地址，并通过交易（请求、授予、委派和撤销访问）在彼此之间进行交互，在其 RO 的控制下。区块链是一个记录和确保交互组织之间访问交易有效性的分类帐。每个组织都管理自己的访问策略，只受其资源所有者的控制，从而产生了一个“分散自治组织的互联网”，因此我们的访问控制框架的公平性（图 8）。

![图 8](img/f08-08-9780128171899.jpg)

图 8 FairAccess 的架构概述。

考虑以下情景，请参见图 9，一个主体（例如，标识为 rq 的设备 A）想要对受保护的资源（例如，标识为 rs 的设备 B 温度）执行某个操作（例如，修改）。我们假设请求者已经了解了调节对设备 B 访问权限的访问控制策略。FairAccess 工作流程如下：Rq 满足了访问控制策略中指定的条件，并通过他的钱包以 RequestAccess 事务的形式提交了请求。随后，钱包将该事务广播到网络节点，直到它抵达矿工的手中。后者充当分布式策略决策点（dPDP），评估该事务并通过执行先前通过名为 GrantAccess 的事务在区块链上已部署的策略合同来检查请求与定义的策略。策略合同的执行确定了请求是否应该被允许或被拒绝。最后，如果成功执行，策略合同生成并分配一个授权令牌给请求者的地址，通过 AllowAccess 事务。然后，授权令牌被记录在区块链上，并出现在请求者的授权令牌列表中。最后，请求者通过 GetAccess 事务向最终设备展示授权令牌。设备 B 通过参考区块链检查授权令牌的有效性；如果这个授权令牌是由对应于设备 B 的智能合同发放的，则允许访问，否则拒绝。

![图 9](img/f08-09-9780128171899.jpg)

图 9 FairAccess 工作流程。

### 4.3 面对的挑战

FairAccess 已成功实现了本章开头所述的以下物联网安全和隐私保护要求，即：（1）分布式性质和缺乏中央权威。用户驱动和透明度。 （2）轻量级。 （3）细粒度。 （4）使物联网设备之间的交互成为可能。 （5）假名和不可追溯性。然而，采用区块链技术处理访问控制功能并不简单，会出现额外的关键问题：

1.  (1) 区块链的公开和透明方面与公开记录在区块链上的访问控制策略的私密性相冲突：通常，确定谁可以访问资源的策略也是敏感的，需要保护。

1.  (2) 追溯问题，例如交易图的结构[52，[53]](S0065245818300676.xhtml#bb0270)，以及交易的价值和日期，可能会导致学习设备授权功能模式，以及某个特定设备是否试图与其他设备通信。

## 5 通过透明度实现隐私：一种隐私保护的分布式访问控制（PPDAC）方案，以增强 FairAccess 中的隐私和匿名性。

本节将介绍如何通过引入 PPDAC 作为完全匿名的隐私保护分布式访问控制方案（PPDAC）来克服这两个确定的挑战，并将其集成到 FairAccess 中。 PPDAC 提供了一种强大的隐私保证访问控制方案，保留了资源所有者的访问控制策略和请求者的敏感属性，然后以强大的方式保护了请求者和资源所有者的匿名性，参见图 10。该方案旨在保持区块链的透明特性，同时确保用户的强大隐私保证。我们开发了一个政策隐藏的访问控制方案，既保护了敏感属性，又保护了敏感策略。也就是说，在公共区块链中的节点可以决定 Alice 的认证属性值是否满足 Bob 的策略，而不了解 Alice 的属性值或 Bob 的策略的任何其他信息。为了实现政策隐藏的访问控制和授权令牌的不可追踪性，我们构建 PPDAC 的方法使用了一种新颖的技术，结合了白盒分布式多权威 CP-ABE [54,[55]](S0065245818300676.xhtml#bb0280), zk-SNARKs [[56]](S0065245818300676.xhtml#bb9000) 协议和智能合约（图 11）。  

![图 10](img/f08-11-9780128171899.jpg)

图 10 PPDAC 构建模块。

![图 11](img/f08-10-9780128171899.jpg)

图 11 基于 PPDAC 的技术。

### 5.1 PPDAC 构建模块

在传统的 CP-ABE 方案中，加密器可以使用隐藏的访问结构加密数据。解密器预先从认证机构获取与其属性相关联的秘密密钥，如果解密器的秘密密钥相关联的属性不满足与加密数据相关联的访问结构，则解密器无法解密数据，甚至无法猜测加密器指定的访问结构是什么。在我们的设置中，由于我们的框架建立在公共区块链上，使用 CP-ABE 技术的目的不是像文献中介绍的那样解密数据，而是确保两个属性：

1.  1. 在区块链网络中隐藏 RO 访问控制策略

1.  2. 启用请求者以公开方式向网络（矿工）证明其隐藏属性符合隐藏策略。为此，我们引入了两个新概念：

挑战：是由资源所有者随机选择的任意字符串，并加密以获得密文 CT。它被视为请求者以公开方式向区块链网络证明其满足访问控制策略的证据，而不暴露其属性或访问控制策略，因为访问控制策略的评估被简化为请求者解密密文 CT 并获取公开已知的挑战的能力。实际上，仅当请求者的属性与隐藏的访问结构匹配时，请求者才能解密密文 CT。

身份密钥（IDkey）：在我们的设置中，我们引入了 IDkey 的概念，它扮演着私钥的同等角色，但是它是公开的。这个 IDkey 拥有加密货币币的特征。IDkey 应该满足三个重要属性：

+   • 匿名性：指不透露所有者的真实身份信息。不可追踪性：我们无法猜测将令牌发送到区块链的原始来源。我们通过使用零知识的 Succinct Non-interactive ARguments of Knowledge（zk-SNARKs）来隐藏花费 IDkey 的交易的起源，从而实现 IDkey 的匿名性和不可追踪性。

+   • 使用由所有者控制：我们认为，由区块链作为硬币加密保护的身份令牌 IDkey 不可能是秘密的，因为此身份令牌的使用仅限于其所有者或在其同意下被让渡。为了实现这一属性，我们将 IDkey 的使用“绑定”到消耗相关的 IDcoin 上，而该 IDcoin 又是由所有者私钥控制的。

我们的协议在以下实体之间运行：一个拥有物联网设备（D）的资源所有者（RO），一个或多个请求者，他们可能是 RO 想要与之合作以获得其设备上智能服务的服务提供商。负责认证一组属性的一组权威机构。

+   • 认证机构：认证机构是受信任的，并以独立的方式管理其属性集。

+   • FairAccess 节点：FairAccess 节点相当于矿工的角色。我们假设这些节点是诚实但好奇的。因此，不仅交互实体的身份应匿名，而且智能合约中保存的访问控制策略也应该是隐藏的。

+   • 资源所有者（Ro）负责定义他的设备上的访问控制策略，并使用具有隐藏策略的分散式多权威 CP-ABE（基于属性的加密）将此访问控制策略模糊化在智能合约中。然后他将智能合约部署到网络上。

+   • 请求者：认证机构为每个请求者生成相关的 IDkeys。此外，只有符合访问控制策略的请求者才会获得授权令牌。

### 5.2 PPDAC 阶段和功能

提议的协议将参与方的交互分为五个阶段：设置阶段、授予权限阶段、请求权限阶段、获取权限阶段、评估访问控制策略阶段和允许访问阶段（图 12–14）。

![图 12](img/f08-12-9780128171899.jpg)

图 12 PPDAC 的阶段。

![图 13](img/f08-13-9780128171899.jpg)

图 13 将私有访问控制策略隐藏在公共区块链中。

![图 14](img/f08-16-9780128171899.jpg)

图 14 授权令牌的不可链接性和不可解性。

### 5.3 背景和定义

要构建 PPDAC 方案，采用以下基本组成部分和定义。

#### 5.3.1 伪随机函数

定义 1\. 抗碰撞哈希

我们使用抗碰撞哈希函数

<math><mi>CRH</mi><mo>:</mo><msup><mfenced close="}" open="{" separators=","><mn>0</mn><mn>1</mn></mfenced><mo>∗</mo></msup><mo>→</mo><msup><mfenced close="}" open="{" separators=","><mn>0</mn><mn>1</mn></mfenced><msup><mi mathvariant="normal">Ο</mi><mi mathvariant="normal">Υ</mi></msup></msup></math>

![si1_e](img/si1_e.png)  (1)

定义 2\. 伪随机函数

我们使用伪随机函数系列 PRF

<math><mi>PRF</mi><mo>=</mo><msub><mfenced close="}" open="{"><mrow><msub><mi>PRF</mi><mi mathvariant="normal">λ</mi></msub><mo>:</mo><msup><mfenced close="}" open="{" separators=","><mn>0</mn><mn>1</mn></mfenced><mo>∗</mo></msup><mo>→</mo><msup><mfenced close="}" open="{" separators=","><mn>0</mn><mn>1</mn></mfenced><msup><mi mathvariant="normal">Ο</mi><mi mathvariant="normal">Υ</mi></msup></msup></mrow></mfenced><mi mathvariant="normal">λ</mi></msub></math>

![si2_e](img/si2_e_u1.png)  (2)

其中λ表示种子。我们以任意方式推导出三个伪随机函数：

<math><msubsup><mi mathvariant="italic">PRF</mi><mi>λ</mi><mi mathvariant="italic">地址</mi></msubsup><mfenced close=")" open="("><mi>x</mi></mfenced><mo>∶</mo><mo>=</mo><msub><mi mathvariant="italic">PRF</mi><mi>λ</mi></msub><mfenced close=")" open="("><mrow><mn>00</mn><mo>∥</mo><mi>x</mi></mrow></mfenced></math>

![si3_e](img/si3_e.png)  (3)

<math><msubsup><mi mathvariant="italic">PRF</mi><mi>λ</mi><mi mathvariant="italic">apk</mi></msubsup><mfenced close=")" open="("><mi>x</mi></mfenced><mo>∶</mo><mo>=</mo><msub><mi mathvariant="italic">PRF</mi><mi>λ</mi></msub><mfenced close=")" open="("><mrow><mn>01</mn><mo>∥</mo><mi>x</mi></mrow></mfenced></math>

![si4_e](img/si4_e.png)  (4)

我们假设 PRF[λ]^(Tsn) 在某种意义上也是抗碰撞的，即找到以下是不可行的

(λ, x) ≠ (λ′, x′) 使得 PRF[λ]^(Tsn)(x) = PRF[λ′]^(Tsn)(x′)。

#### 5.3.2 一次性强不可伪造数字签名

我们使用数字签名方案 Sign = <math><mfenced close=")" open="(" separators=",,,"><mrow><mi mathvariant="script">G</mi><mi mathvariant="italic">en</mi></mrow><mrow><mi mathvariant="script">KS</mi><mi>i</mi><mi mathvariant="script">G</mi></mrow><mrow><mi mathvariant="italic">sig</mi></mrow><mrow><mi mathvariant="italic">check</mi></mrow></mfenced></math>![si5_e](img/si5_e.png) ，其工作原理如下：

<math><mi mathvariant="bold-script">G</mi><mi mathvariant="bold-italic">en</mi><mfenced close=")" open="("><msup><mn mathvariant="bold">1</mn><mi mathvariant="bold-italic">k</mi></msup></mfenced><mo mathvariant="bold-italic">→</mo><msub><mi mathvariant="bold-italic">param</mi><mi mathvariant="bold-italic">sig</mi></msub></math>![si6_e](img/si6_e.png)。给定安全参数 1^k，<math><mi mathvariant="script">G</mi><mi mathvariant="italic">en</mi></math>![si7_e](img/si7_e.png) 为签名方案的公共参数 param[sig] 生成样本

<math><mi mathvariant="bold-script">KS</mi><mi mathvariant="bold-italic">i</mi><mi mathvariant="bold-script">G</mi><mfenced close=")" open="("><msub><mi mathvariant="bold-italic">param</mi><mi mathvariant="bold-italic">sig</mi></msub></mfenced><mo mathvariant="bold-italic">→</mo><mfenced close=")" open="(" separators=","><msub><mi mathvariant="bold-italic">pk</mi><mi mathvariant="bold-italic">sig</mi></msub><msub><mi mathvariant="bold-italic">sk</mi><mi mathvariant="bold-italic">sig</mi></msub></mfenced></math>![si8_e](img/si8_e.png)。给定公共参数 <math><msub><mi mathvariant="bold-italic">param</mi><mi mathvariant="bold-italic">sig</mi></msub><mo>,</mo><mi mathvariant="script">KS</mi><mi>i</mi><mi mathvariant="script">G</mi></math>![si9_e](img/si9_e.png)，对于单个用户，样本生成一个公钥和一个密钥。

sig[sk[sig]](m) → σ。给定私钥 sk[sig] 和消息 m，sig[sk[sig]] 签署 m 以获得签名 σ。

check[pk[sig]](m, σ) → b。给定公钥 pk[sig]、消息 m 和签名 σ，check[pk[sig]] 输出 b。

如果签名 σ 对消息 m 有效，则 b = 1；否则输出 b = 0。

签名方案 Sign 满足针对选择消息攻击的一次强不可伪造性安全性属性（SUF-1CMA 安全）。

#### 5.3.3 访问结构

定义 3\.（访问结构[57]）

设{P[1]，P[2]，…，P[n]}为一组参与方，集合<math><mi mathvariant="script">A</mi></math>![si10_e](img/si10_e.png) ⊆ 2^({P[1]，P[2]，…，P[n]})是单调的，如果<math><mo>∀</mo><mi>B</mi><mo>,</mo><mi>C</mi><mo>:</mo><mi mathvariant="italic">if</mi><mi>B</mi><mo>∈</mo><mi mathvariant="script">A</mi></math>![si11_e](img/si11_e.png)，且 B ⊆ C，则<math><mi>C</mi><mo>∈</mo><mi mathvariant="script">A</mi></math>![si12_e](img/si12_e.png)。访问结构（分别为单调访问结构）是一组（分别为单调组）<math><mi mathvariant="script">A</mi></math>![si10_e](img/si10_e.png)的非空子集合{P[1]，P[2]，…，P[n]}，即<math><mi mathvariant="script">A</mi></math>![si10_e](img/si10_e.png) ⊆ 2^({P[1]，P[2]，…，P[n]}) ∖ {ϕ}，<math><mi mathvariant="script">A</mi></math>![si10_e](img/si10_e.png)中的集合称为授权集合，而不在<math><mi mathvariant="script">A</mi></math>![si10_e](img/si10_e.png)中的集合称为未授权集合。

#### 5.3.4 线性秘密共享方案（LSSS）

在我们的构造中，我们将使用线性秘密共享方案（LSSS）。 因此，我们使用从参考文献[[57]](S0065245818300676.xhtml#bb9005)中改编的定义。

定义 4。 （线性秘密共享方案（LSSS））

如果秘密共享方案∏涉及参与方 P 的一个集合，并且满足以下属性，则称为线性（在ℤ[p]上）。

1.  （1）每个参与方的份额形成一个ℤ[p]上的向量。

1.  （2）对于∏，存在一个具有ℓ行和 n 列的矩阵 M，称为共享生成矩阵。对于 i = 1, 2,…，ℓ，第 i 行带有一个标有方 ρ(i)的 party，其中ρ：{1, 2,…，ℓ}→ℤ[p]。为了共享一个秘密 s∈ℤ[p]，选择一个向量<math><mover accent="true"><mi>v</mi><mo stretchy="true">→</mo></mover></math>![si17_e](img/si17_e.png) = (s, v2,…，vn)，其中 v2,…，vn 是从ℤ[p]随机选择的。 <math><mi>M</mi><mover accent="true"><mi>v</mi><mo stretchy="true">→</mo></mover></math>![si18_e](img/si18_e.png)是根据∏的ℓ个分享的向量。份额<math><msub><mi>M</mi><mi>i</mi></msub><mover accent="true"><mi>v</mi><mo stretchy="true">→</mo></mover></math>![si19_e](img/si19_e.png) 属于 party ρ(i)，其中 M[i]是 M 的第 i 行。

#### 5.3.5 分布式多权威 CP-ABE 方案

在我们的设置中，我们使用了基于[[58]](S0065245818300676.xhtml#bb9010)中介绍的分布式多权威 CP-ABE 方案。

定义 5

DCP-ABE 方案包括以下四个基本算法：系统设置，权威设置，加密，密钥生成和解密。

系统设置（1^k）→（PP）：设置算法接受一个安全参数 1^k 作为输入。它输出公共参数 PP。

假设存在 N 个认证机构{CÅ[1]，CÅ[2]，…，CÅ[N]}，每个机构 CÅ[i]监控一组属性Ã[i]。每个用户 U 都有一个唯一的全局标识符 GID[U]，并持有一组属性Û。

权威设置（1^k）→（SK[i]，PK[i]）。接受安全参数 1^k 作为输入，并为每个权威Ã输出密钥对（SK[i]；PK[i]），其中 KeyGen（1^k）→（SK[i]，PK[i]）。

<math><mi mathvariant="bold-italic">Encrypt</mi><mfenced close=")" open="(" separators=",,"><mi mathvariant="italic">PP</mi><mi mathvariant="script">M</mi><msub><mfenced close=")" open="(" separators=",,"><msub><mi>M</mi><mi>i</mi></msub><msub><mi>ρ</mi><mi>j</mi></msub><msub><mi mathvariant="italic">PK</mi><mi>i</mi></msub></mfenced><mi mathvariant="italic">iϵI</mi></msub></mfenced><mo>→</mo><mi mathvariant="italic">CT</mi></math>![si20_e](img/si20_e.png)。它将公共参数 PP、明文消息<math><mi mathvariant="script">M</mi></math>![si21_e](img/si21_e.png)、一组访问结构（Mi, ρi）i ∈ I 和一组公钥（PKi） ∈ I 作为输入，并输出密文 CT。

keyGen（GID；PP；Û∩ Ã；SK[i]） → idKey[GID,i] 将公共参数 PP、密钥 SK[i]、请求者的全局标识符 GID[U] 和一组属性 Û∩ Ã 作为输入，IDkeyGen 生成算法输出 idKey[GID,i]。

Decrypt(PP, (idKey[GID,i])[i ∈ I], CT) → M。解密算法以公共参数 PP、密文 CT 和秘密密钥 idKey[GID,i] 作为输入。如果属性集满足访问结构 A，则算法将解密密文并返回消息 m；否则返回 ⊥。

定义 6

分布式密文策略属性加密（DCP-ABE）如果正确的话

<math><mi mathvariant="italic">Pr</mi><mfenced close="|" open="|"><mtable><mtr><mtd><mi mathvariant="italic">解密</mi><mfenced close=")" open="(" separators=",,"><mi mathvariant="italic">PP</mi><msub><mfenced close=")" open="("><msub><mi mathvariant="italic">idKey</mi><mrow><mi mathvariant="italic">GID</mi><mo>,</mo><mi>i</mi></mrow></msub></mfenced><mrow><mi>i</mi><mo>∈</mo><mi>I</mi></mrow></msub><mi mathvariant="italic">CT</mi></mfenced></mtd></mtr><mtr><mtd><mo>→</mo><mi>M</mi></mtd></mtr></mtable></mfenced><mfenced close="|" open=""><mtable><mtr><mtd><mi mathvariant="italic">系统</mi><mi mathvariant="italic">设置</mi><mfenced close=")" open="("><msup><mn>1</mn><mi>k</mi></msup></mfenced><mo>→</mo><mfenced close=")" open="("><mi mathvariant="italic">PP</mi></mfenced></mtd></mtr><mtr><mtd><mi mathvariant="italic">权威</mi><mi mathvariant="italic">设置</mi><mfenced close=")" open="("><msup><mn>1</mn><mi>k</mi></msup></mfenced><mo>→</mo><mfenced close=")" open="(" separators=","><msub><mi mathvariant="italic">SK</mi><mi>i</mi></msub><msub><mi mathvariant="italic">PK</mi><mi>i</mi></msub></mfenced></mtd></mtr><mtr><mtd><mi mathvariant="italic">加密</mi><mfenced close=")" open="(" separators=",,"><mi mathvariant="italic">PP</mi><mi mathvariant="script">M</mi><msub><mfenced close=")" open="(" separators=",,"><msub><mi>M</mi><mi>i</mi></msub><msub><mi>ρ</mi><mi>j</mi></msub><msub><mi mathvariant="italic">PK</mi><mi>i</mi></msub></mfenced><mi mathvariant="italic">iϵI</mi></msub></mfenced><mo>→</mo><mi mathvariant="italic">CT</mi></mtd></mtr></mtable></mfenced><mo>=</mo><mn>1</mn></math>

![si22_e](img/si22_e.png)

其中概率是对方案中所有算法使用的随机比特的令牌。

定义 7\. (选择性访问结构安全的 DCPABE (IND-sAS-CPA))

在选择性访问结构模型中，如果没有可能的多项式时间对手 A 能够以概率多项式时间赢得上述游戏，则分布式密文策略属性加密（DCP-ABE）方案在（T，q，ϵ(k)）上是安全的，其中 q 为秘密密钥查询次数。

<math><msubsup><mi mathvariant="italic">Adv</mi><mi>A</mi><mrow><mi mathvariant="italic">ACP</mi><mo>−</mo><mi mathvariant="italic">ABE</mi></mrow></msubsup><mo>=</mo><mfenced close="|" open="|"><mrow><mi mathvariant="italic">Pr</mi><mfenced close="]" open=""><mrow><msup><mi>b</mi><mo>′</mo></msup><mo>=</mo><mi>b</mi></mrow></mfenced><mo>−</mo><mfrac><mn>1</mn><mn>2</mn></mfrac></mrow></mfenced><mo>></mo><mi>ϵ</mi><mfenced close=")" open="("><mi>k</mi></mfenced></math>

![si23_e

其中概率是在挑战者和对手消耗的所有比特上进行的。

#### 5.3.6 zk-SNARKs 协议

定义 8

我们非正式地定义了算术电路可满足性的 zk-SNARKs。我们建议读者参考，例如，引用[56]以获取正式定义。

对于一个域<math><mi mathvariant="double-struck">F</mi></math>![si24_e](img/si24_e.png)，一个<math><mi mathvariant="double-struck">F</mi></math>![si24_e](img/si24_e.png)算术电路接受作为输入的元素，这些元素属于<math><mi mathvariant="double-struck">F</mi></math>![si24_e](img/si24_e.png)，其门输出<math><mi mathvariant="double-struck">F</mi></math>![si24_e](img/si24_e.png)中的元素。我们自然地将电路与其计算的函数相关联。为了模拟非确定性，我们考虑具有输入<math>x ∈ F^n</math>和辅助输入<math>a <mo>∈</mo><msup><mi mathvariant="double-struck">F</mi><mi>p</mi></msup></math>![si28_e](img/si28_e.png)的电路，称为证明。我们考虑的电路只有双线性门。算术电路可满足性类似于布尔情况，定义如下：

定义 9

一个<math><mi mathvariant="double-struck">F</mi></math>![si24_e](img/si24_e.png)算术电路的可满足性问题：

C: <math><msup><mi mathvariant="double-struck">F</mi><mi>n</mi></msup><mo>×</mo></math>![si30_e](img/si30_e.png) <math><msup><mi mathvariant="double-struck">F</mi><mi>p</mi></msup><mo>→</mo><msup><mi mathvariant="double-struck">F</mi><mi>l</mi></msup></math>![si31_e](img/si31_e.png) 被关系 <math><msub><mi mathvariant="normal">ℝ</mi><mi>C</mi></msub><mo>=</mo><mfenced close="}" open="{"><mrow><mfenced close=")" open="(" separators=","><mi>x</mi><mi>a</mi></mfenced><mo>∈</mo><msup><mi mathvariant="double-struck">F</mi><mi>n</mi></msup><mo>×</mo><msup><mi mathvariant="double-struck">F</mi><mi>p</mi></msup><mi>C</mi><mfenced close=")" open="(" separators=","><mi>x</mi><mi>a</mi></mfenced><mo>=</mo><msup><mn>0</mn><mi>l</mi></msup></mrow></mfenced><mo>;</mo><mi mathvariant="italic">其</mi><mi mathvariant="italic">语言</mi><mi mathvariant="italic">为</mi><msub><mi mathvariant="script">L</mi><mi>C</mi></msub><mo>=</mo><mfenced close="}" open="{"><mrow><mi>x</mi><mo>∈</mo><msup><mi mathvariant="double-struck">F</mi><mi>n</mi></msup><mo>:</mo><mo>∃</mo><mi>a</mi><mo>∈</mo><msup><mi mathvariant="double-struck">F</mi><mi>p</mi></msup><mi mathvariant="italic">，</mi><mi mathvariant="italic">使</mi><mi mathvariant="italic">得</mi><mi>C</mi><mfenced close=")" open="(" separators=","><mi>x</mi><mi>a</mi></mfenced><mo>=</mo><msup><mn>0</mn><mi>l</mi></msup></mrow></mfenced></math>![si32_e](img/si32_e.png)![si999_e](img/si999_e.png)

给定一个域 <math><mi mathvariant="double-struck">F</mi></math>![si24_e](img/si24_e.png)，一个（公开可验证的预处理）

对于 <math><mi mathvariant="double-struck">F</mi></math>![si24_e](img/si24_e.png)-算术电路可满足性的 zk-SNARK 是一组多项式时间算法（KeyGen；Prove；Verify）：

keyGen(1^k, C) → (pk, vk) 接受安全参数 k 和一个 <math><mi mathvariant="double-struck">F</mi></math>![si24_e](img/si24_e.png)-算术电路 C，密钥生成器 keyGen 概率性地采样一个证明密钥 pk 和一个验证密钥 vk。这两个密钥被发布为公共参数，并且可以被使用任意次数，来证明/验证属于 <math><msub><mi mathvariant="script">L</mi><mi>C</mi></msub></math>![si36_e](img/si36_e.png) 的成员资格。

证明（pk，x，a）→ π 接受证明密钥 pk 和任何 (x, a) ∈ ℝ[C]，证明者 Prove 输出关于命题 x ∈ <math><msub><mi mathvariant="script">L</mi><mi>C</mi></msub></math>![si36_e](img/si36_e.png) 的非交互式证明 π。

验证（vk，x，π）→ b 接受验证密钥 vk、输入 x 和证明 π，验证器 Verify 输出 b = 1 如果他确信 x ∈ <math><msub><mi mathvariant="script">L</mi><mi>C</mi></msub></math>![si36_e](img/si36_e.png)。

一个 zk-SNARK 满足以下属性：

完备性。对于每个安全参数 k，任何 <math><mi mathvariant="double-struck">F</mi></math>![si24_e](img/si24_e.png)-算术电路 C 和任何 (x, a) ∈ ℝ[C]，诚实的证明者可以说服验证者。也就是说，在以下实验中，b = 1 的概率为 1 − negl (k)：(pk, vk) ← keyGen(1^k, C)，π ← Prove(pk, x, a)，b ← Verify( vk, x, π)。

简洁性。一个诚实生成的证明π具有<math><msub><mi mathvariant="script">O</mi><mi>k</mi></msub><mfenced close=")" open="("><mn>1</mn></mfenced></math>![si40_e](img/si40_e.png)比特，而 Verify(vk, x, π)在时间<math><msub><mi mathvariant="script">O</mi><mi>k</mi></msub><mfenced close=")" open="(" separators="||"><mi>x</mi></mfenced></math>![si41_e](img/si41_e.png)内运行。（这里，<math><msub><mi mathvariant="script">O</mi><mi>k</mi></msub></math>![si42_e](img/si42_e.png)隐藏了 k 的固定多项式因子。）

知识证明（以及声音性）。如果验证器接受有界证明者生成的证明，则证明者“知道”给定实例的见证人。（特别是，声音性针对有界证明者保持。）即，对于每个 poly(k)-size 对手<math><mi mathvariant="script">A</mi></math>![si10_e](img/si10_e.png)，存在一个 poly(k)-size 提取器<math><mi mathvariant="script">E</mi></math>![si44_e](img/si44_e.png)，使得在以下实验中 Verify(vk, x, π) = 1 且(x, a) ∈ ℝ[C]的概率为 negl(k)：(pk, vk) ← keyGen(1^k, C); <math><mfenced close=")" open="(" separators=","><mi>x</mi><mi>π</mi></mfenced><mo>←</mo><mi mathvariant="script">A</mi><mfenced close=")" open="(" separators=","><mi mathvariant="italic">pk</mi><mi mathvariant="italic">vk</mi></mfenced></math>![si45_e](img/si45_e.png); <math><mi>a</mi><mo>←</mo><mi mathvariant="script">E</mi><mfenced close=")" open="(" separators=","><mi mathvariant="italic">pk</mi><mi mathvariant="italic">vk</mi></mfenced></math>![si46_e](img/si46_e.png)

完美的零知识。一个诚实生成的证明是完美的零知识。也就是说，存在一个多项式大小的模拟器 <math><mi mathvariant="script">S</mi><mi mathvariant="italic">im</mi></math>![si47_e](img/si47_e.png)，对于所有有状态的多项式大小的区分器 <math><mi mathvariant="script">D</mi></math>![si48_e](img/si48_e.png)，以下两个概率相等：

1.  1. 在诚实证明中，<math><mi mathvariant="script">D</mi><mfenced close=")" open="("><mi>π</mi></mfenced></math>![si49_e](img/si49_e.png)= 1 的概率。

<math><mi mathvariant="italic">Pr</mi><mfenced close="]" open=""><mrow><mfenced close=")" open="(" separators=","><mi>x</mi><mi>a</mi></mfenced><mo>∈</mo><msub><mi mathvariant="normal">ℝ</mi><mi>C</mi></msub><mi mathvariant="script">D</mi><mfenced close=")" open="("><mi>π</mi></mfenced><mo>=</mo><mn>1</mn><mfenced close="" open="|"><mtable><mtr><mtd><mfenced close=")" open="(" separators=","><mi mathvariant="italic">pk</mi><mi mathvariant="italic">vk</mi></mfenced><mo mathvariant="bold">←</mo><mi mathvariant="bold-italic">keyGen</mi><mfenced close=")" open="("><mrow><mi>C</mi></mrow></mfenced></mtd></mtr><mtr><mtd><mfenced close=")" open="(" separators=","><mi>x</mi><mi>a</mi></mfenced><mo>←</mo><mi mathvariant="script">D</mi><mfenced close=")" open="(" separators=","><mi mathvariant="italic">pk</mi><mi mathvariant="italic">vk</mi></mfenced></mtd></mtr><mtr><mtd><mi>π</mi><mo>←</mo><mi mathvariant="bold-italic">Prove</mi><mfenced close=")" open="(" separators=",,"><mi mathvariant="italic">pk</mi><mi>x</mi><mi>a</mi></mfenced></mtd></mtr></mtable></mfenced></mrow></mfenced></math>

![si50_e1.  2. 在模拟证明中，<math><mi mathvariant="script">D</mi><mfenced close=")" open="("><mi>π</mi></mfenced></math>![si49_e](img/si49_e.png) = 1 的概率。

<math><mi mathvariant="italic">Pr</mi><mfenced close="]" open=""><mrow><mfenced close=")" open="(" separators=","><mi>x</mi><mi>a</mi></mfenced><mo>∈</mo><msub><mi mathvariant="normal">ℝ</mi><mi>C</mi></msub><mi mathvariant="script">D</mi><mfenced close=")" open="("><mi>π</mi></mfenced><mo>=</mo><mn>1</mn><mfenced close="" open="|"><mtable><mtr><mtd><mfenced close=")" open="(" separators=",,"><mi mathvariant="italic">pk</mi><mi mathvariant="italic">vk</mi><mi mathvariant="italic">trap</mi></mfenced><mo mathvariant="bold">←</mo><mi mathvariant="bold-italic">Sim</mi><mfenced close=")" open="("><mrow><mi>C</mi></mrow></mfenced></mtd></mtr><mtr><mtd><mfenced close=")" open="(" separators=","><mi>x</mi><mi>a</mi></mfenced><mo>←</mo><mi mathvariant="script">D</mi><mfenced close=")" open="(" separators=","><mi mathvariant="italic">pk</mi><mi mathvariant="italic">vk</mi></mfenced></mtd></mtr><mtr><mtd><mi>π</mi><mo>←</mo><mi mathvariant="bold-italic">Sim</mi><mfenced close=")" open="(" separators=",,"><mi mathvariant="italic">pk</mi><mi>x</mi><mi mathvariant="italic">trap</mi></mfenced></mtd></mtr></mtable></mfenced></mrow></mfenced></math>

![si52_e

### 5.4 隐私保护分布式访问控制方案（PPDAC）的正式定义

我们首先描述并直观地解释了 PPDAC 方案中使用的数据结构，这些算法使用并在第 5.5 节详细介绍了每一个构造细节。

#### 5.4.1 数据结构

公共参数（PP）：系统中所有用户都可以访问的公共参数 PP 列表。这些参数由系统的“启动时间”上的受信方生成，并由系统的算法使用。

地址：与 FairAccess 中一样，系统中的每个用户都可以生成任意多个地址。每个地址对应于一对密钥（a[pk]; a[sk]）。公钥 a[pk] 被发布，使其他人能够与用户交互。密钥 a[sk] 用于花费由拥有 a[pk] 的用户拥有的授权令牌。

IDkey：是 idKey[GID,i] 的向量，如 IDkey = (idKey[GID,i])[i ∈ N]

其中 idKey[GID,i] 是由监控一组属性 Û ∩ Ã[i] 和 GID 的认证机构 CÅ[i] 颁发的私钥。其中 GID 对应于 chaise 在 [[59]](S0065245818300676.xhtml#bb9015) 中引入的全局标识符概念，用于将由不同机构颁发给同一用户的私钥链接在一起。

请求者通过与认证机构运行 IDkeygen 算法来获得一个 IDkey。然后在铸造 IDcoin 时由其所有者记录在区块链中作为一个公共值。

IDcoin：对于每个 IDkey，我们关联一个 IDcoin。IDcoin 是一个数据对象 idc，我们将其与以下内容关联：

+   • IDcoin 承诺，表示为 cm (idc)：一串字符串，一旦 idc 被请求者铸造，就会出现在总账上。

+   • IDcoin 序列号，表示为 sn (idc)：与 idc 关联的唯一字符串，用于防止双重支付。

+   • IDcoin 地址，表示为 a[pk] (idc)：公钥地址，表示谁拥有 idc。

授权令牌 TKN：是按照以下方式构造的数据结构：

<math><mi mathvariant="italic">TKN</mi><mo>≔</mo><mfenced close=")" open="("><mrow><mtext>智能合约地址</mtext><mo stretchy="true">‖</mo><mi>cm</mi></mrow></mfenced><mo>.</mo></math>

![si53_e](img/si53_e.png)

当 IDcoin 被请求者铸造时，它以与 IDCMlist 中 IDcoin 的承诺同时出现的方式被智能合约添加到 TKNList 中。

铸造的 IDcoin 和花费的 IDcoin 的承诺。对于任何给定时间 T，

IDCMList[T] 表示在时间 T 区块链中记录的 Request Access RqTx 和 GetAccess GtATx 中出现的所有 IDcoin 承诺的列表。

TKNList[T] 表示记录在时间 T 区块链中的 GetAccess GtATx 交易中出现的所有授权令牌的列表。

SNListT[T] 表示在时间 T 的分类账中出现的所有序列号的列表。

IDcoin 承诺的 Merkle 树：对于任何给定的时间 T，IDCTree[T] 表示 IDCMList[T] 上的 Merkle 树，rt[T] 表示其根。此外，函数 Path[T] (idcm) 给出了出现在 IDCMList[T] 中的 IDcoin 承诺 idcm 到 Tree[T] 根的身份验证路径。为方便起见，我们假设时间 T 的分类账 L[T] 也存储了所有 T* < T（即，它存储了所有过去的 Merkle 树根）。

授权令牌的 Merkle 树：对于任何给定的时间 T，AUTree[T] 表示 TKNList[T] 上的 Merkle 树，rt ∗[T] 表示其根。此外，函数 Path ∗[T] (idcm) 给出了出现在 TKNList[T] 中的授权令牌 TKN 到 TKNTree[T] 根的身份验证路径。为方便起见，我们假设时间 T 的分类账 L[T] 也存储了所有 T* < T（即，它存储了所有过去的 Merkle 树根）。

智能合约：是在区块链中运行的程序，存储着两个值：（1）密文 CT。 （2）其对应的挑战 CH，它是与 CT 相关联的随机数，如下所示：CT ≔ Encrypt(PP, CH, (M[i], ρ[j], PK[i])[iϵI])。智能合约嵌入了三个函数：

1.  （i）Decrypt(PP,IDkey,CT) → M

1.  （ii）一个布尔函数 IsEqual(M, CH)

1.  （iii）AddToTKNList(TKN)

新交易：我们在我们的框架中使用了三种新类型的交易，分别是：

1.  （1）授权访问交易：它用于在区块链中部署智能合约：

<math><mi mathvariant="italic">GrATx</mi><mo>≔</mo><mfenced close=")" open="("><mrow><mi mathvariant="italic">智能合约</mi><mi mathvariant="italic">SC</mi></mrow></mfenced></math>

![si54_e](img/si54_e.png)

1.  (2) 请求访问权限交易：触发 SmartContract 并铸造 IDcoin：

<math><mi mathvariant="italic">RqTx</mi><mo>≔</mo><mfenced close=")" open="(" separators=";;;"><mi mathvariant="italic">IDkey</mi><mi>k</mi><mi>s</mi><mi mathvariant="italic">cm</mi></mfenced></math>

![si55_e](img/si55_e.png)

1.  (3) 获取访问权限交易：倾倒 RequestAccess IDcoin 并持有授权令牌：

<math><mi mathvariant="italic">GtATx</mi><mo>≔</mo><mfenced close=")" open="(" separators=";;;"><mi mathvariant="italic">rt</mi><mi mathvariant="italic">sn</mi><mi mathvariant="italic">cm</mi><mi>π</mi></mfenced></math>

![si56_e](img/si56_e.png)

区块链：我们的协议应用于像以太坊这样的公共无许可账本之上。在任何给定时间 T，所有用户都可以访问时间 T 的账本，它是一系列交易。账本只能追加。

#### 5.4.2 算法

我们将接下来描述我们系统中需要的函数。实现这些函数的协议将在后面的部分中描述。这些函数中的大多数，如果不是全部，都将根据给定的区块链 B 进行，或者需要调用我们系统中的公共参数。这些是协议的隐含输入。

(PPDAC) 方案 Π 是多项式时间算法的元组：(SystemSetup，Authority Setup，IDkeyGen，encrypt，decrypt，CreateAddress，GrantAccess，RequestAccess，GetAccess，ValidateTransaction，executeSmartContract，AllowAccess)

系统设置：(1^k) → PP。将安全参数 1^k 作为输入，全局设置算法输出公共参数 PP。

算法设置由可信方执行。生成的公共参数 PP 被发布并提供给所有参与方（例如，通过将它们嵌入到协议的实现中）。设置仅执行一次。之后，不再需要可信方，也不保留全局秘密或陷阱门。

Authority Setup: KG(1^k) → (SK[i], PK[i])。系统中的每个权威都运行具有安全参数 1^k 的权威设置算法，作为输入产生自己的秘密密钥和公钥对(SK[i]; PK[i])。

Encrypt(PP, CH, (M[i], ρ[j], PK[i])[iϵI]) → CT。它以公共参数 PP、随机明文字符串 CH、一组访问结构(Mi, ρi)[i ∈ I]和一组公钥(PKi)[i ∈ I]作为输入。它输出与此访问结构相关联的密文 CT。

ExecuteSmartContract(RqT[x], SmartContract SC) → True or ⊥. 它以 RequestAccess 交易作为输入。它返回 true 或 false。该算法调用了三个子算法，分别是：(Decrypt, IsEqual, AddtoTKNList)，定义如下：

Decrypt(PP, IDkey, CT) → M. 以公共参数 PP、密文 CT 和来自触发智能合约的 RequestAccess 交易的 IDkey 作为输入。其中 Request Access 交易 RqTx 如下所示：RqTx ≔ (IDkey, k, s, cm)

IsEqual(M, CH)。一个布尔函数，用于比较生成的消息 M 和记录的挑战 CH，如下所示：如果请求者的属性，与 IDkey 关联的属性，满足访问结构集合(Mi, ρi)i ∈ I，则 M 将等于 CH，并且函数返回 true，否则函数返回 false ⊥。

AddtoTKNList(idcm) → (rt, path(idcm))。它以 IDcoin 承诺作为输入，并返回其在根为 rt 的默克尔树中的身份验证路径。

CreateAddress(PP) ⟶ (a[pk]; a[sk])。该算法生成一个新的假名地址密钥对：(a[pk]; a[sk])。每个用户至少生成一个地址密钥对，以接收授权令牌。公钥 a[pk]被公开，而秘密密钥 a[sk]用于赎回发送到 a[pk]的令牌。用户可以生成任意数量的地址密钥对；这样做不需要任何交互。

<math><mi mathvariant="bold-italic">GrantAccess</mi><mfenced close=")" open="("><mi mathvariant="bold-italic">CH</mi><mi>,</mi><mrow><mfenced close=")" open="("><mi mathvariant="bold-italic">PKi</mi></mfenced><mo mathvariant="bold-italic">∈</mo><mi mathvariant="bold-italic">I</mi></mrow><mrow><mfenced close=")" open="(" separators=","><mi mathvariant="bold-italic">Mi</mi><mi mathvariant="bold-italic">ρi</mi></mfenced><mi mathvariant="bold-italic">i</mi><mo mathvariant="bold-italic">∈</mo><mi mathvariant="bold-italic">I</mi></mrow></mfenced><mo mathvariant="bold-italic">→</mo><mi mathvariant="bold-italic">GrATx</mi><mo mathvariant="bold-italic">≔</mo><mfenced close=")" open="("><mrow><mi mathvariant="bold-italic">智能合约</mi><mi mathvariant="bold-italic">SC</mi></mrow></mfenced></math>

![si57_e](img/si57_e.png)

算法 GrantAccess 的输出是一个 GrantAccess 事务，其中包含隐藏的 RO 访问控制策略，以智能合约的形式，并管理每个设备的访问控制。

输入参数包括：隐含的公共参数 PP，明文 CH，一组访问结构（Mi， ρi）i ∈ I，以及相关机构的公钥集合（PKi） ∈ I。

<math><mi mathvariant="bold-italic">IDkeyGen</mi><mfenced close=")" open="(" separators=";;;"><mi mathvariant="bold-italic">GID</mi><mi mathvariant="bold-italic">PP</mi><mrow><mi mathvariant="bold">Û</mi><mo mathvariant="bold-italic">∩</mo><mi mathvariant="bold">Ã</mi></mrow><msub><mi mathvariant="bold-italic">SK</mi><mi mathvariant="bold-italic">i</mi></msub></mfenced><mo mathvariant="bold-italic">→</mo><msub><mi mathvariant="bold-italic">idKey</mi><mrow><mi mathvariant="bold-italic">GID</mi><mo mathvariant="bold-italic">,</mo><mi mathvariant="bold-italic">i</mi></mrow></msub><mi mathvariant="bold-italic">和 IDkey</mi><mo mathvariant="bold-italic">=</mo><msub><mfenced close=")" open="("><msub><mi mathvariant="bold-italic">idKey</mi><mrow><mi mathvariant="bold-italic">GID</mi><mo mathvariant="bold-italic">,</mo><mi mathvariant="bold-italic">i</mi></mrow></msub></mfenced><mrow><mi mathvariant="bold-italic">i</mi><mo mathvariant="bold-italic">∈</mo><mi mathvariant="bold-italic">N</mi></mrow></msub></math>

![si58_e](img/si58_e.png)

请求者和权威参与 IDkeyGen 算法，该算法的输入包括公共参数 PP、秘密密钥 SK[i]、请求者的全局标识符 GID[U] 以及一组属性 Û ∩ Ã。它为请求者生成一个 IDkey。

<math><mi mathvariant="bold-italic">RequestAccess</mi><mfenced close=")" open="(" separators=",,"><mi mathvariant="bold-italic">PP</mi><msub><mi mathvariant="bold-italic">GID</mi><mi mathvariant="bold-italic">U</mi></msub><mrow><msub><mi mathvariant="bold-italic">a</mi><mi mathvariant="bold-italic">pk</mi></msub></mrow></mfenced><mo mathvariant="bold-italic">→</mo><mfenced close=")" open="(" separators=","><mi mathvariant="bold-italic">IDcoin</mi><mrow><mi mathvariant="bold-italic">RqTx</mi><mo mathvariant="bold-italic">≔</mo><mfenced close=")" open="(" separators=";;;"><mi mathvariant="bold-italic">IDkey</mi><mi mathvariant="bold-italic">k</mi><mi mathvariant="bold-italic">s</mi><mi mathvariant="bold-italic">cm</mi></mfenced></mrow></mfenced><mo mathvariant="bold-italic">.</mo></math>

![si59_e](img/si59_e.png)

算法**GetAccess**的输入包括公共参数**PP**，请求者的全局标识符**GID[U]**，以及请求者想要接收授权令牌的公共地址**a[pk]**。该算法输出一个**IDcoin**和一个**RequestAccess**交易**RqTx**。

<math><mi mathvariant="bold-italic">GetAccess</mi><mfenced close=")" open="(" separators=",,,,"><mi mathvariant="italic">PP</mi><mi mathvariant="italic">rt</mi><mi mathvariant="italic">idcoin</mi><mrow><mi mathvariant="italic">path</mi><mfenced close=")" open="("><mi mathvariant="italic">idcm</mi></mfenced></mrow><msub><mi>a</mi><mi mathvariant="italic">sk</mi></msub></mfenced><mo>→</mo><mi mathvariant="italic">GtATx</mi><mo>≔</mo><mfenced close=")" open="(" separators=";;;"><mi mathvariant="italic">rt</mi><mi mathvariant="italic">sn</mi><mi mathvariant="italic">cm</mi><mi>π</mi></mfenced></math>

![si60_e](img/si60_e.png)

算法 GetAccess 的输入是带有相应秘钥 a[sk]（用于赎回 idcoin）的 IDcoin。为了确保 IDcoin 未曾被铸造过，GetAccess 算法还将从 Idcm 的认证路径路径形式中获取的 Merkle 根 rt 作为输入。它输出一个 GetAccess 事务 GtATx。

<math><mi mathvariant="bold">ValidateTransaction</mi><mfenced close=")" open="(" separators=",,"><mrow><mi mathvariant="bold">GrantAccess</mi><mi mathvariant="bold-italic">GrATx</mi></mrow><mrow><mi mathvariant="bold">RequestAccess</mi><mi mathvariant="bold-italic">RqTx</mi></mrow><mrow><mi mathvariant="bold">GetAccess</mi><mi mathvariant="bold">transaction</mi><mi mathvariant="bold-italic">GtATx</mi></mrow></mfenced><mo mathvariant="bold-italic">→</mo><mfenced close=")" open="(" separators=","><mi mathvariant="bold-italic">true</mi><mi mathvariant="bold-italic">false</mi></mfenced></math>

![si61_e](img/si61_e.png)

算法 ValidateTransaction 检查交易的有效性：所有交易在被视为格式良好之前都必须经过验证。在实践中，交易可以由维护账本的分布式系统中的节点验证，也可以由依赖这些交易的用户验证。

<math><mi mathvariant="bold">AllowAccess</mi><mfenced close=")" open="(" separators=","><mrow><mi mathvariant="bold">GrantAccess</mi><mi mathvariant="bold">Transaction</mi><mi mathvariant="bold-italic">GrATx</mi></mrow><mi mathvariant="bold-italic">SNlist</mi></mfenced><mo mathvariant="bold">→</mo><mfenced close=")" open="(" separators=","><mi mathvariant="bold-italic">true</mi><mi mathvariant="bold-italic">false</mi></mfenced></math>

![si62_e](img/si62_e.png)

算法 AllowAccess 的输入是来自当前账本的 GrantAccess 事务和 SNList，如果由该 GrantAccess 事务所花费的 IDCoin 出现在 SNlist 中，则允许访问，否则不允许。

### 5.5 PPDAC 构造

+   第 1 阶段：设置

系统设置：(1^k) → PP。输入安全参数 1^k，全局设置算法输出公共参数 PP。

权威设置：假设存在 N 个认证机构 {CÅ[1], CÅ[2], …, CÅ[N]}，每个机构 CÅ[i] 监控一组属性 Ã[i]。每个用户 U 具有唯一的全局标识符 GID[U]，并持有一组属性 Û。系统中的每个机构运行权限设置算法，以安全参数 1^k 为输入生成其自身的秘密密钥和公钥对 (SK[i]; PK[i])，如下所示：KG(1^k) → (SK[i], PK[i])。

注：值得注意的是，此阶段在区块链之外进行。

+   第二阶段：GrantAccess 阶段包括在设备上定义访问控制策略并将其隐藏在智能合约中：

资源所有者负责定义访问策略和混淆策略。

对于每个设备，RO 的操作如下：

1.  1. 他生成一个我们称之为挑战的随机数：CH

1.  2. 他定义一个访问结构 (Mi, ρi)i ∈ I。

1.  3. 他使用分布式 DCP-ABE 方案，根据相应的访问结构 Mi，ρi 加密挑战 CH，并通过以下函数获得密文 CT：Encrypt(PP, CH, (M[i], ρ[j], PK[i])[iϵI]) → CT。

    输入公共参数 PP、明文消息 CH、一组访问结构 (Mi, ρi)i ∈ I 和一组公钥 (PKi) ∈ I。输出与这组访问结构相关联的密文 CT。

1.  4. 他定义一个智能合约：

    1.  a. 存储两个值：(1) 密文 CT，(2) 及其对应的 CH。

    1.  b. 嵌入三个函数：

        1.  (1) Decrypt(PP, IDkey, CT) → M。

            输入公共参数 PP、来自触发智能合约的 RequestAccess 交易的密文和 IDkey。其中一个 Request Access 交易 RqTx 如下：RqTx ≔ (IDkey, k, s, cm)，这个交易的详细信息将在下一阶段详述。

        1.  (2) 一个布尔函数，用于比较结果消息 M 和记录的挑战 CH，如下所示：IsEqual(M, CH)

            如果与 IDkey 关联的请求者属性满足访问结构集(Mi, ρi)i ∈ I，则 M 将等于 CH，否则该函数返回 false ⊥。

        1.  (3) 如果比较函数的输出为真，则智能合约将 IDkey 关联到 RqTx 交易中的 idcm，并将其添加到授权令牌列表 TKNList 中。

1.  5. 然后 RO 通过 GrantAccess 交易在区块链中部署定义的智能合约：GrATx:= (SmartContract SC)

最后，为了防止智能合约和交易可塑性，我们使用数字签名。这个数字签名起到了将智能合约与 RO 及其设备绑定的“MACS”的作用。RO 随机抽取一个密钥对(pk[sig], sk[sig])，并计算σ = sig[sk[sig]](SC)。然后，设置

<math><mi mathvariant="italic">GrATx</mi><mo>≔</mo><mfenced close=")" open="(" separators=",,"><mrow><mi mathvariant="italic">SmartContract</mi><mi mathvariant="italic">SC</mi></mrow><msub><mi mathvariant="italic">pk</mi><mi mathvariant="italic">sig</mi></msub><mi>σ</mi></mfenced></math>

![si63_e](img/si63_e.png)

+   第三阶段：请求访问阶段的任务是成功执行智能合约以获得访问令牌

这个阶段分为两个子阶段，如下所示：

请求者（RQ）-权限交互。在这个子阶段中，Rq 与认证机构（CÅ[i]）[i ∈ I] 进行交互，并运行 IDkey 提取算法，如下所示：

<math><mi mathvariant="italic">IDkey</mi><mi>Gen</mi><mfenced close=")" open="(" separators=";;;"><mi mathvariant="italic">GID</mi><mi mathvariant="italic">PP</mi><mrow><mi>Û</mi><mo>∩</mo><mi mathvariant="normal">Ã</mi></mrow><msub><mi mathvariant="italic">SK</mi><mi>i</mi></msub></mfenced><mo>→</mo><msub><mi mathvariant="italic">idKey</mi><mrow><mi mathvariant="italic">GID</mi><mo>,</mo><mi>i</mi></mrow></msub><mtext>和</mtext><mi mathvariant="italic">IDkey</mi><mo>=</mo><msub><mfenced close=")" open="("><msub><mi mathvariant="italic">idKey</mi><mrow><mi mathvariant="italic">GID</mi><mo>,</mo><mi>i</mi></mrow></msub></mfenced><mrow><mi>i</mi><mo>∈</mo><mi>N</mi></mrow></msub></math>

![si64_e](img/si64_e.png)

将公共参数 PP、秘密密钥 SK[i]、请求者的全局标识符 GID[U] 和一组属性 Û∩ Ã 作为输入，IDkeyGen 生成算法输出 Rq 的 IDkey。我们假设 RQ 与机构之间的通信是安全和私密的。该阶段在区块链网络之外运行。

请求者-智能合约交互。在获取管理目标设备访问权限的智能合约地址之后，请求者通过发送请求访问事务 RqTx 来触发智能合约，以正确解密挑战并获取授权令牌。正如本节开头所述，在我们的设置中，我们不像传统的 CP-ABE 方案那样使用私钥，而是使用身份密钥：嵌入在 IDcoin 中的 IDKey。为了释放 IDKey 的不可互操作性属性，我们利用了 zk-SNARKs（如上所述）和以下承诺方案：

让 COMM 表示一个统计隐藏的非交互式承诺方案（即，给定随机数 r 和消息 m，承诺为 c ∶= COMMr，随后，通过揭示 r 和 m 来打开 c，并且可以验证 COMMr 等于 c）。

请求者通过请求访问 RqTx 事务将持有 IDKey 的 ID 币铸造到总账上。与传统的 CP-ABE 方案不同，其中私钥用于解密密文并且保密给其所有者以便仅由其使用，我们在我们的设置中提供了 IDKey 限制使用的相同属性，即使它是公共的。为此，我们以下面的方式派生与 IDkey 相关联的 ID 币：

我们使用三个伪随机函数（从一个函数派生）。对于一个种子 x，这些被标记为 PRF[x]^(address)。我们假设 PRF[x]^(address)此外是抗碰撞的。

为了为 ID 币提供目标，我们使用地址：每个用户 u 生成一个地址密钥对(a[pk];a[sk])。绑定到 ID 密钥的 ID 币包含值 a[pk]，只有知道 a[sk]的情况下才能使用。通过这种方式，ID 密钥的使用由拥有 a[sk]的所有者控制。通过选择随机种子 a[sk]并设置 a[pk]: = PRF[ask]^(address)(0)来采样密钥对(a[pk]; a[sk])。用户可以生成并使用任意数量的地址密钥对。

将 ID 币“绑定”到指定的 ID 密钥，请求者 Rq 首先对ρ进行抽样，这是一个秘密值，并计算ρ′ = PRF[ask]^(IDkey)(ρ)，然后确定 ID 币的序列号 sn 为 sn:= PRF[ask]^(sn)( ρ′)。

然后，请求者以两个阶段承诺元组(a[pk]:IDkey;ρ′)：(a) u 计算 k ∶ = COMMr 为一个随机 r; 然后(b) 请求者计算 cm ∶ = COMMs 为一个随机 s。铸造产生一个 ID 币 idc:= (a[pk]; IDkey; ρ; r; s; cm)和一个请求访问事务 RqTx:= (IDkey; k; s; cm)。

具体来说，由于互连的承诺，任何人都可以验证请求访问事务中的 cm 是否是 IDkey 的 ID 币的硬币承诺（通过检查 COMMS 是否等于 cm），但不能辨别所有者（通过学习地址密钥 a[pk]）或序列号（从 ρ′ 派生），因为这些都隐藏在 k 中。通过这种方式，实现了 IDkey 的匿名性和不可追踪性。

请求访问事务仅在请求者呈现与隐藏访问控制策略匹配的正确 ID 密钥（通过解密密码文本 Decrypt(PP, IDkey, CT) → M）且在一手持有的情况下才被账本接受，另一方面，如果承诺是正确的。

在此阶段，ID 币承诺和相应由智能合约签名的授权令牌分别记录在区块链上的两个列表中：ID 币承诺列表 IDcList 和授权令牌列表 TKNList。

授权令牌是一个用智能合约地址签名的 ID 币承诺，该承诺已添加到账本上。随后，令 IDcoinList 表示账本上所有 ID 币承诺的列表，而 TKNList 分别表示账本上所有授权令牌。请求者可以通过发布包含以下内容的 GetAccess 事务来使用授权令牌：

1.  （i）一个 ID 币的序列号 sn，智能合约的地址。

1.  （ii）一个 NP 陈述的 zk-SNARK 证明 π：“我知道 r，使得 COMMr 出现在 IDcoin 承诺的列表 IDcoinList 中。”

1.  （iii）带有智能合约地址的 ID 币承诺 idcm。

TKN: =（智能合约地址 || idcm）出现在 TKNList 中

假设 sn 尚未出现在账本上（作为过去的花费交易的一部分），请求者可以兑换授权令牌。（如果 sn 已经出现在账本上，则被视为双重支出，并且该交易被丢弃。）此外，终端设备将能够验证此授权令牌是否由其相应的智能合约提供，通过检查智能合约地址。请求者的匿名性得到保证，因为证明π是零知识的，而 sn 被揭示，r 的信息不被透露，找出 TKNList 中的众多承诺中的哪一个对应于特定的 GetAccess 交易等同于求逆 f(x)：= COMMx，这被假设为不可行。因此，交易的起源是匿名的（图 15）。

+   第 4 阶段：获得权限并花费授权令牌

![图 15](img/f08-14-9780128171899.jpg)

图 15 生成 IDcoin 和授权令牌。

为了访问受保护的设备，请求者使用 GetAccess 交易来花费授权令牌，如下所示：

假设一个请求者，带有地址密钥对(a[pk]; a[sk])，希望消费他的 IDcoin:= (a[pk]; IDkey; ρ; ρ′, r; s; cm)，请求者为以下 NP 语句生成 zk-SNARK 证明π，我们称之为 GetAccess：

“鉴于 Merkle 树根 rt、序列号 sn 和 IDcoin 承诺 cm，我知道 IDcoin 和地址秘钥 a[sk]，使得：i）IDcoin 格式正确，对于 IDcoin，它成立：k ∶ = COMMr 和 cm ∶ = COMMs。ii）地址秘钥与公钥匹配：a[pk] = PRF[ask]^(address)(0)。 iii）IDcoin 正确绑定到 Ideky：ρ′ = PRF[ask]^(IDkey)(ρ)。 iv）序列号正确计算：sn:= PRF[ask]^(sn)( ρ′)。v）硬币承诺 cm 显示为具有根 rt 的 Merkle-树的叶子。”

最终的 GetAccess 交易得到形式 GtATx:= (rt; sn; cm; π)被附加到账本上，如果序列号 sn 出现在先前的交易中，则被拒绝。

这样，如果请求者不知道与公钥 a[pk]关联的地址秘钥 a[sk]，那么请求者既不能花费授权令牌，也不能使用 IDkey，因为他无法提供作为后续 GetAccess 交易见证的新 a[sk]。

此外，为了防止交易篡改并将每个 IDkey 与其所有者绑定，我们使用数字签名。请求者对密钥对(pk[sig], sk[sig])进行抽样，设置<math><mi>m</mi><mo>=</mo><mfenced close=")" open="(" separators=","><mover accent="true"><mi>u</mi><mo stretchy="true">→</mo></mover><msub><mi>π</mi><mi mathvariant="italic">grant</mi></msub></mfenced><mo>,</mo></math>![si65_e](img/si65_e.png)，计算σ = sig[sk[sig]](m)。然后，设置 GtATx ≔ (rt; sn; cm; IDkey, π, pk[sig], σ)。

+   第 5 阶段：AllowAccess 阶段的作用是通过终端设备检查令牌的有效性，并决定是允许还是拒绝访问。

当请求者向终端设备呈现授权令牌时，后者验证 TKNList 中存在的授权令牌是否由终端设备的智能合约添加。如果是，则允许访问，否则不允许。

为了轻量级验证而压缩授权令牌列表：在上述 NP 陈述中，IDCMList 被明确指定为 IDcoin 承诺的列表。这种直接的表示方式严重限制了可扩展性，因为大多数协议算法（例如，证明验证算法）的时间和空间复杂度都随着 IDCMList 的增长而线性增加。此外，对于已经花费的 IDcoins 对应的授权令牌无法从 IDCMList 中删除以减少成本，因为它们无法被识别（由于提供匿名性的相同零知识属性）。正如在[[60]](S0065245818300676.xhtml#bb9020)中所述，我们依赖于碰撞抗性哈希函数 CRH 来避免对 IDCMList 进行显式表示。我们在（增长中的）列表 IDCMList 上维护一个基于 CRH 的 Merkle 树 Tree(IDCMList)，它可以高效地更新并追加。设 rt 表示 Tree(IDCMList) 的根，众所周知，更新 rt 来考虑新叶子的插入可以在时间和空间上与树深度成正比。因此，时间和空间复杂度从 IDCMList 的大小线性减少到对数。考虑到这一点，我们将 NP 陈述修改为以下内容：“我知道 r，使得 COMMr 出现在根为 rt 的基于 CRH 的 Merkle 树中的一个叶子节点。”与对 IDCMList 的朴素数据结构相比，这种修改使给定 zk-SNARK 实现可以支持的 IDCMList 大小呈指数增长。我们对授权令牌列表 TKNList 也采取同样的操作（参见图 16）。

![图 16](img/f08-15-9780128171899.jpg)

图 16 基于 CRH 的授权令牌（tkn）树。

这结束了构建大纲的说明。我们指出，由于 zk-SNARK，我们的构建需要一次性的公共参数信任设置。尽管信任影响了证明的可靠性，但即使设置被恶意方损坏，匿名性仍然保持不变。

算法构建：我们描述了 PPDAP 方案的构建（SystemSetup; AuthoritySetup, CreateAddress, GrantAccess, RequestAccess, GetAccess, VerifyTransaction; AllowAccess）在 图 17 和 图 18 中。

![图 17](img/f08-17-9780128171899.jpg)

图 17 PPDAC 隐私保护分布式访问控制（第 1/2 部分）。

![图 18](img/f08-18-9780128171899.jpg)

图 18 PPDAC 隐私保护分布式访问控制（第 2/2 部分）。

## 6 结论

本章中，我们提出了我们解决物联网隐私和安全问题的方法。具体而言，这种方法包括提供一个遵守以下原则的分布式访问控制框架：边缘智能、透明安全、设计隐私和用户驱动策略。然后，我们介绍了 FairAccess 作为一种新颖、更强大和透明的访问控制解决方案，符合这四个定义的原则。FairAccess 利用基于区块链的加密货币提供的一致性来解决所有与物联网相关的访问控制挑战。虽然 FairAccess 利用了基于区块链的加密货币提供的一致性来解决物联网中的集中式和分散式访问控制问题，并提供了一种有前景的用户驱动和透明的访问控制工具，但由于区块链的公开性及其固有的可追溯性问题，它无法为用户提供强大的匿名性。为了解决这个问题，本章介绍了一个完全匿名的、保护隐私的分布式访问控制方案（PPDAC）。PPDAC 被整合到 FairAccess 中，以保持区块链的透明特性，同时为用户提供强大的隐私保证。在这个方向上，采用了基于属性的访问控制系统，其中访问控制决策基于属性（而不是身份）。使用分布式多权威密文策略属性基础加密 DMCP-ABE 的白盒版本开发了一个保护敏感属性和敏感策略的策略隐藏访问控制方案。此外，为了解决授权令牌的可追溯性问题，引入了一个充分的非交互式零知识证明（zk-SNARK）协议。最后，提供了所提议方案的正式定义和构造。

总之，我们总结了在第三部分中制定的研究问题的答案。

1.  1. 如何通过利用区块链技术解决物联网中的访问控制挑战？

+   我们去中心化访问控制框架的愿景是一个围绕一个或多个资源所有者的自治组织系统，这些资源所有者拥有一个或多个通过交易进行交互的资源，并通过交易（请求、授权、委托和撤销访问）在它们的 RO 控制下进行交互。区块链是一本账簿，用于跟踪和确保交互组织之间访问事务的有效性。每个组织都管理着自己的访问策略，仅受其资源所有者的控制。实际上，在 FairAccess 中，我们使用类似比特币的地址来标识所有交互实体，并使用智能合约（又名链代码）来表达封装在交易中的细粒度和上下文访问控制策略。我们选择由区块链分发的授权令牌。FairAccess 利用区块链提供了几种有用的机制。事实上，在 FairAccess 中，区块链被视为一个数据库或策略检索点，所有访问控制策略都以交易形式存储在其中；它还充当了确保审计功能的日志数据库。此外，它通过交易完整性检查防止令牌伪造，并通过双重花费检测机制检测令牌重用。

1.  2. 如何在受限的物联网设备上提供轻量级访问控制框架，尽管公共区块链采用的共识协议需要大量的计算资源？

+   我们通过提出一个分层架构来回答这个问题，在这个架构中，物联网中的设备支持不同程度的 FairAccess 功能，这取决于它们的性能和存储能力。

1.  3. 如何实现隐私保护的访问控制，隐藏用户的访问控制策略，并克服公共区块链中常见的可追踪性和用户画像问题？

+   我们通过引入 PPDAC 来解决这个问题，这是一个完全匿名的隐私保护分布式访问控制方案，用于集成到 FairAccess 中，以获得强大的隐私保证访问控制方案，保留资源所有者的访问控制策略和请求者的敏感属性，并以强大的方式保护请求者和 Ro 的匿名性。所提出的方案旨在保持区块链的透明特性，同时为用户提供强大的隐私保证。我们使用基于属性的访问控制系统，其中访问控制决策基于请求者的属性（而不是身份）：如果 Alice 在她的证书中的属性满足 Bob 的访问策略，则授予访问权限。我们开发了一个隐藏策略的访问控制方案，既保护了敏感属性又保护了敏感策略。也就是说，在公共区块链中的节点可以确定 Alice 的已认证属性值是否满足 Bob 的策略，而不了解 Alice 的其他属性值或 Bob 的策略。我们为 PPDAC 的构建使用了一种将 CP-ABE、szNARK 协议和智能合约相结合的新技术。

## 参考文献

[1] Benessia A., Pereira Â.G. 互联网物联网的梦想。在：*科学、哲学和可持续发展：笛卡尔梦想的终结 5，第 78 卷。* 2015。检索自[`books.google.com/books?hl=fr&lr=&id=_K7ABgAAQBAJ&oi=fnd&pg=PA78&dq=decentralizing++internet+of+things+ibm+watson+&ots=O98rKriJQ1&sig=Kz5bB4EJ80hSktroqnbo_ScvSZM`](https://books.google.com/books?hl=fr&lr=&id=_K7ABgAAQBAJ&oi=fnd&pg=PA78&dq=decentralizing++internet+of+things+ibm+watson+&ots=O98rKriJQ1&sig=Kz5bB4EJ80hSktroqnbo_ScvSZM)。

[2] Gubbi J., Buyya R., Marusic S., Palaniswami M. 物联网（IoT）：愿景、架构要素和未来方向。*未来计算系统* 2013;29(7):1645–1660。[`doi.org/10.1016/j.future.2013.01.010`](https://doi.org/10.1016/j.future.2013.01.010)。

[3] Miorandi D., Sicari S., De Pellegrini F., 等. 物联网: 视觉, 应用和研究挑战. *Ad Hoc Netw.* 2012;10(7):1497–1516\. 检索自 [`www.sciencedirect.com/science/article/pii/S1570870512000674`](http://www.sciencedirect.com/science/article/pii/S1570870512000674).

[4] Borgia E. 物联网愿景: 关键特征, 应用和未解之谜. *Comput. Commun.* 2014;54:1–31\. [`doi.org/10.1016/j.comcom.2014.09.008`](https://doi.org/10.1016/j.comcom.2014.09.008).

[5] Mattern F., Floerkemeier C. *从计算机互联网到物联网.* Springer 柏林海德堡; 2010.242–259\. [`doi.org/10.1007/978-3-642-17226-7_15`](https://doi.org/10.1007/978-3-642-17226-7_15).

[6] Guinard D. *物联网应用架构—将现实世界整合到网络中.* 博士论文, 苏黎世联邦理工学院 (19891), 220 [`doi.org/10.3929/ethz-a-006713673`](https://doi.org/10.3929/ethz-a-006713673). 2011.

[7] Bonomi F., Milito R., Zhu J., Addepalli S. *雾计算及其在物联网中的作用.* In: 第一届移动云计算 MCC 研讨会论文集—MCC’12; 纽约: ACM 出版社; 2012:13\. [`doi.org/10.1145/2342509.2342513`](https://doi.org/10.1145/2342509.2342513).

[8] Jardak C., Walewski J.W. *使物联网能够交流.* [`doi.org/10.1007/978-3-642-40403-0`](https://doi.org/10.1007/978-3-642-40403-0). 2013.

[9] Holler J., Tsiatsis V., Mulligan C., Avesand S. *从机器到机器到物联网：迈向智能新时代的介绍.* Academic Press; 2014\. Retrieved from [`books.google.com/books?hl=fr&lr=&id=wtfEAgAAQBAJ&oi=fnd&pg=PP1&dq=From+Machine-To-Machine+to+the+Internet+of+Things:+Introduction+to+a+New+Age+of+Intelligence+&ots=mICCLT9hgD&sig=UNQUKzbr7Co6cDF9jn8P9FL_01Q`](https://books.google.com/books?hl=fr&lr=&id=wtfEAgAAQBAJ&oi=fnd&pg=PP1&dq=From+Machine-To-Machine+to+the+Internet+of+Things:+Introduction+to+a+New+Age+of+Intelligence+&ots=mICCLT9hgD&sig=UNQUKzbr7Co6cDF9jn8P9FL_01Q).

[10] Vermesan O., Friess P., eds. *物联网：智能环境和集成生态系统的融合技术.* River Publishers; 2013.

[11] Armitage J. *保罗·维里利奥：从现代主义到超现代主义及其以后.* Retrieved from [`books.google.com/books?hl=fr&lr=&id=-WL75BiQBRYC&oi=fnd&pg=PP1&dq=PAUL++virilio+Politics+of+the+Very+Worst+&ots=0AmM0dctMV&sig=QpI5pdafuGVLP4hr88N3kSb9i_A`](https://books.google.com/books?hl=fr&lr=&id=-WL75BiQBRYC&oi=fnd&pg=PP1&dq=PAUL++virilio+Politics+of+the+Very+Worst+&ots=0AmM0dctMV&sig=QpI5pdafuGVLP4hr88N3kSb9i_A). 2000.

[12] Kumar J.S., Patel D.R. *物联网安全与隐私问题调查.* *Int. J. Comput. Appl.* 2014;90(11) MLA.

[13] Decker C., Seidel J., Wattenhofer R. *比特币遇到强一致性.* *Proceedings of the 17th International Conference on Distributed Computing and Networking.* 2016;13: ACM.

[14] Vasilomanolakis E., Daubert J., Luthra M., Gazis V., Wiesmaier A., Kikiras P. *关于物联网架构和系统安全与隐私.* In: *Secure Internet of Things (SIoT).* International Workshop on IEEE.ISO; 49–57\. 2015;690.

[15] Ziegeldorf J.H., Morchon O.G., Wehrle K. *物联网中的隐私：威胁与挑战.* *Secur. Commun. Netw.* 2014;7(12):2728–2742\. [`doi.org/10.1002/sec.795`](https://doi.org/10.1002/sec.795).

[16] Langheinrich M. *隐私设计——隐私感知智能系统原则.* Springer Berlin Heidelberg; 2001.273–291\. [`doi.org/10.1007/3-540-45427-6_23`](https://doi.org/10.1007/3-540-45427-6_23).

[17] Ziegeldorf J.H., Morchon O.G., Wehrle K. 物联网中的隐私：威胁与挑战。*Secur. Commun. Netw.* 2014;7(12):2728–2742\. [`doi.org/10.1002/sec.795`](https://doi.org/10.1002/sec.795).

[18] Berman F., Cerf V.G. 互联网物联网中的社会和道德行为。*Commun. ACM.* 2017;60(2):6–7\. [`doi.org/10.1145/3036698`](https://doi.org/10.1145/3036698).

[19] E.P. Goodman，数据的原子时代：物联网政策，“智能城市”用例背景下的一些政策问题的报告，ISO 690，2015。

[20] Diaz C., Gürses S., Troncoso C. 隐私设计工程。*Comput. Priv. Data Prot.* 2011\. 检索自 [`software.imdea.org/~carmela.troncoso/papers/Gurses-CPDP11.pdf`](https://software.imdea.org/~carmela.troncoso/papers/Gurses-CPDP11.pdf).

[21] Gurses S., del Alamo J.M. 隐私工程：塑造一门新兴的研究与实践领域。*IEEE Secur. Priv.* 2016;14(2):40–46\. [`doi.org/10.1109/MSP.2016.37`](https://doi.org/10.1109/MSP.2016.37).

[22] Spiekermann S., Cranor L.F. 隐私工程。*IEEE Trans. Softw. Eng.* 2009;35(1):67–82\. 检索自 [`ieeexplore.ieee.org/abstract/document/4657365/`](http://ieeexplore.ieee.org/abstract/document/4657365/).

[23] Sánchez Alcón J.A., López L., Martínez J.F., et al. 基于整体服务需求的信任和隐私解决方案。*Sensors (Basel).* 2015;16(1):16\. 检索自 [`www.mdpi.com/1424-8220/16/1/16/htm`](http://www.mdpi.com/1424-8220/16/1/16/htm).

[24] Cavoukian A. 法律、政策和实践中的隐私设计。*面向监管机构、决策者和政策制定者的白皮书.* 2011.

[25] Ouaddah A., Abou Elkalam A., Ait Ouahman A. FairAccess：一种新的基于区块链的物联网访问控制框架. *Secur. Commun. Netw.* 2016;9(18):5943–5964\. [`doi.org/10.1002/sec.1748`](https://doi.org/10.1002/sec.1748).

[26] Ouaddah A., Elkalam A.A., Ouahman A.A. *基于区块链技术的 IoT 隐私保护访问控制模型.* Cham: Springer; 2017.523–533\. [`doi.org/10.1007/978-3-319-46568-5_53`](https://doi.org/10.1007/978-3-319-46568-5_53).

[27] Ouaddah A., Mousannif H., Abou Elkalam A., Ait Ouahman A. 物联网中的访问控制：巨大挑战与新机遇. *Comput. Netw.* 2017;112:237–262\. [`doi.org/10.1016/j.comnet.2016.11.007`](https://doi.org/10.1016/j.comnet.2016.11.007).

[28] Sandhu R.S. 基于角色的访问控制. *Adv. Comput.* 1998;46:237–286\. [`doi.org/10.1016/S0065-2458(08)60206-5`](https://doi.org/10.1016/S0065-2458(08)60206-5).

[29] Yuan E., Tong J. *基于属性的访问控制（ABAC）用于 Web 服务.* In: IEEE International Conference on Web Services (ICWS’05); IEEE; 2005\. [`doi.org/10.1109/ICWS.2005.25`](https://doi.org/10.1109/ICWS.2005.25).

[30] Seitz L., Selander G., Wahlstroem E., Erdtman S., Tschofenig H. *Internet of Things 使用 OAuth 2.0 的授权.* 检索自[`tools.ietf.org/html/draft-ietf-ace-oauth-authz-01`](https://tools.ietf.org/html/draft-ietf-ace-oauth-authz-01). 2016.

[31] Cirani S., Picone M., Gonizzi P., Veltri L., Ferrari G. IoT-OAS：基于 OAuth 的物联网场景下的安全服务架构. *IEEE Sensors J.* 2015;15(2):1224–1234\. [`doi.org/10.1109/JSEN.2014.2361406`](https://doi.org/10.1109/JSEN.2014.2361406).

[32] Roman R., Zhou J., Lopez J. 关于分布式物联网安全与隐私的特征和挑战。 *计算机网络.* 2013;57(10):2266–2279。[`doi.org/10.1016/j.comnet.2012.12.018`](https://doi.org/10.1016/j.comnet.2012.12.018)。

[33] Cirani S., Davoli L., Ferrari G., Léone R. 一种可扩展且自配置的物联网服务发现架构。 *IEEE 物联网期刊.* 2014;1:508–521。检索自[`ieeexplore.ieee.org/abstract/document/6899579/`](http://ieeexplore.ieee.org/abstract/document/6899579/)。

[34] Said O., Masud M. 走向物联网：调查与未来愿景。 *计算机网络国际期刊.* 2013;5(1):1–17。检索自[`citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.741.3655&rep=rep1&type=pdf`](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.741.3655&rep=rep1&type=pdf)。

[35] Tsai C.-W., Lai C.-F., Vasilakos A.V. 未来物联网：开放问题和挑战。 *无线网络.* 2014;20(8):2201–2217。[`doi.org/10.1007/s11276-014-0731-0`](https://doi.org/10.1007/s11276-014-0731-0)。

[36] Panikkar S., Nair S., Brody P., Pureswaran V. *ADEPT：物联网从业者的视角.* 检索自[`ibm.biz/devicedemocracy`](http://ibm.biz/devicedemocracy)。2015 年。

[37] Antonakakis M., April T., Bailey M., 等。理解**Mirai 僵尸网络**。在：*USENIX 安全研讨会.* 2017 1092–1110。

[38] Nakamoto S. *比特币：一种点对点的电子现金系统.* 2008 年。1–9。

[39] Underwood S. 区块链超越比特币。 *ACM 通信.* 2016;59(11):15–17。

[40] Swan M. *区块链：新经济的蓝图.* 检索自[`books.google.com/books?hl=fr&lr=&id=RHJmBgAAQBAJ&oi=fnd&pg=PR3&dq=BLOCKCHAIN+APPLICATION+BEYOND+FINANCE&ots=XPyHHY-Rg4&sig=xZ1yJTxrIgXGqd22L30op9po8-s`](https://books.google.com/books?hl=fr&lr=&id=RHJmBgAAQBAJ&oi=fnd&pg=PR3&dq=BLOCKCHAIN+APPLICATION+BEYOND+FINANCE&ots=XPyHHY-Rg4&sig=xZ1yJTxrIgXGqd22L30op9po8-s)。2015 年。

[41] 乌列鲁 M. 区块链 2.0 及其以后：自组织网络。在：*超越银行和货币的银行.* 2016\. 检索自 [`link.springer.com/chapter/10.1007/978-3-319-42448-4_15`](http://link.springer.com/chapter/10.1007/978-3-319-42448-4_15).

[42] 卡特尔 J.L., 韦格曼 M.N. 哈希函数的通用类。*J. 计算机系统科学.* 1979;18(2):143–154\. 检索自 [`www.sciencedirect.com/science/article/pii/0022000079900448`](http://www.sciencedirect.com/science/article/pii/0022000079900448).

[43] 默克尔 R.C. *基于常规加密函数的数字签名。* 在：密码学理论与应用会议; 柏林，海德堡：施普林格; 1987\. 369–378, 检索自 [`link.springer.com/chapter/10.1007/3-540-48184-2_32`](http://link.springer.com/chapter/10.1007/3-540-48184-2_32)。

[44] 兰波特 L., 肖斯塔克 R., 皮斯 M. 拜占庭将军问题。*ACM Trans. 程序设计语言系统.* 1982;4(3):382–401\. 检索自 [`dl.acm.org/citation.cfm?id=357176`](http://dl.acm.org/citation.cfm?id=357176).

[45] 特雄尔斯 F., 舒尔曼 B. 比特币及其以后：关于去中心化数字货币的技术调查。*IEEE 通讯. 调查. 导师.* 2016;18(3):2084–2123\. 检索自 [`ieeexplore.ieee.org/abstract/document/7423672/`](http://ieeexplore.ieee.org/abstract/document/7423672/).

[46] 王 W., 郭浩阳 D.T., 熊泽., 等. *区块链网络中共识机制和挖矿管理的调查.* 2018 arXiv 预印本 arXiv:1805.02707.

[47] 布特林 V. 一个下一代智能合约和去中心化应用平台。在：*以太坊.* 2014:1–36\. 检索自 [`buyxpr.com/build/pdfs/EthereumWhitePaper.pdf`](http://buyxpr.com/build/pdfs/EthereumWhitePaper.pdf).

[48] Christidis K., Devetsikiotis M. 物联网的区块链和智能合约. *IEEE Access.* 2016;4:2292–2303\. 检索自 [`ieeexplore.ieee.org/abstract/document/7467408/`](http://ieeexplore.ieee.org/abstract/document/7467408/).

[49] Caldwell J. *IBM 物联网观点与策略.* 2015.

[50] Conoscenti M., Vetrò A., Martin J.D. *物联网区块链: 一项系统文献综述.* 检索自 [`porto.polito.it/id/eprint/2650266`](http://porto.polito.it/id/eprint/2650266). 2016.

[51] Ouaddah A., Bellaj B. FairAccess 2.0: 基于智能合约的授权框架, 用于在物联网中实现细粒度访问控制. *国际信息与计算安全期刊(IJICS).* 2018.

[52] Reid F., Harrigan M. *比特币系统匿名性分析*, 收录于:《社交网络中的安全与隐私》. 纽约: Springer New York; 2013.197–223\. [`doi.org/10.1007/978-1-4614-4139-7_10`](https://doi.org/10.1007/978-1-4614-4139-7_10).

[53] Ron D., Shamir A. *比特币交易图的定量分析.* 柏林海德堡: Springer; 2013.6–24\. [`doi.org/10.1007/978-3-642-39884-1_2`](https://doi.org/10.1007/978-3-642-39884-1_2).

[54] Bethencourt J., Sahai A., Waters B. 密文策略属性基础加密. [IEEE]. 收录于: *2007 年 IEEE 安全与隐私研讨会(SP’07).* 2007:321–334\. [`doi.org/10.1109/SP.2007.11`](https://doi.org/10.1109/SP.2007.11).

[55] Cheung L., Newport C. 可证安全的密文策略属性基础加密. 收录于: *第 14 届 ACM 计算机与通信安全会议论文集, ACM.* 2007:456–465\. 检索自 [`dl.acm.org/citation.cfm?id=1315302`](http://dl.acm.org/citation.cfm?id=1315302).

[56] Bitansky N., Chiesa A., Ishai Y., Paneth O., Ostrovsky R. *线性交互证明的简洁非交互论证.* 柏林, 海德堡: Springer; 2013.315–333\. [`doi.org/10.1007/978-3-642-36594-2_18`](https://doi.org/10.1007/978-3-642-36594-2_18).

[57] Beimel A.，סומע למיב。 *秘密分享和密钥分配的安全方案。*以色列理工学院计算机科学系；1996。

[58] 韩杰，Susilo W.，穆宇，周靖，何炎城。改进去中心化密文策略属性加密中的隐私和安全性。《IEEE 信息检索与安全性杂志》2015;10(3):665–678。

[59] Chase M. 多机构属性基加密。在：《密码理论》。柏林，海德堡：斯普林格柏林海德堡；2007:515–534。

[60] 桑德尔 T.，塔夏马 A。可审计、匿名的电子现金。在：《密码学进展—CRYPTO’ 99》。柏林，海德堡：斯普林格；1999:555–572。[`link.springer.com/10.1007/3-540-48405-1_35`](http://link.springer.com/10.1007/3-540-48405-1_35) (参见第 122 页)。

![u08-01-9780128171899](img/u08-01-9780128171899.jpg)

**Aafaf Ouaddah 博士**于 2017 年从卡迪·艾亚德大学获得博士学位，她的研究方向是利用区块链技术提升物联网安全和隐私。2013 年，她从国家邮电与电信学院（INPT）获得网络和信息技术工程师学位。自 2017 年起，她担任 Mchain 企业的首席科学家。她的研究兴趣包括区块链和新型分布式分类账，以及分布式系统、物联网和雾计算中的安全性和隐私。她在包括 IEEE、斯普林格和爱思唯尔在内的各种会议、研讨会和国际知名期刊上发表了 10 多篇研究论文。

* * *

^(a) [`www.gartner.com/newsroom/id/2209615`](http://www.gartner.com/newsroom/id/2209615)。

^(b) [`share.cisco.com/internet-of-things.html`](http://share.cisco.com/internet-of-things.html)。

^(c) [`iotevent.eu/cisco-sees-14-trillion-opportunity-in-iot/`](http://iotevent.eu/cisco-sees-14-trillion-opportunity-in-iot/)。
