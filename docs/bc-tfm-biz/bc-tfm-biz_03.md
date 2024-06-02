第二章

什么是区块链？

区块链 /ˈblɒktʃeɪn/：一种按时间顺序和公开记录比特币或其他加密货币交易的数字账本

2.1 引言

2008 年，当全世界面临几十年来最大的金融危机时[29]，一份论文在一小群密码学爱好者中流传[30]。在这篇论文中，中本聪（Satoshi Nakamoto）[31]解释了名为比特币（Bitcoin）的一种加密货币的概念，以及解决长期存在的双重支付问题（即代表唯一价值的数字代币可以被多次使用）[32]的方案。多年来，双重支付一直是数字货币广泛采用的主要障碍之一。2008 年，域名[Bitcoin.org](http://Bitcoin.org)被注册，2009 年初，比特币的创世区块——即区块链的第一个区块——被创建[30]。在那个时候，没有人预见到 Nakamoto’s [31]的基础技术对世界上最大组织、受信任的中介机构以及整个社会[33]的影响。

自中本聪的论文发表以来，分布式账本技术，也被称为区块链技术，^(2)已经迅速流行起来。尽管账本已经存在了数千年，但历史上第一次，通过使用区块链技术，账本可以在多个组织和计算机网络之间同时更新。这种功能显著降低了“系统操纵”的可能性，即区块链账本的分布式和去中心化性质，防止任何单一方控制和操纵账本。区块链背后的密码学确保了一个“无需信任”的系统，从而消除了管理风险的中介需求。这是一个真正的范式转变，这也是为什么这么多组织正在探索区块链的潜在用途，以改善他们的追踪和审计系统。^(3)尽管区块链技术还不到十年，但企业和政府组织，以及财团都对此现代现象进行了大量投资，希望利用它获得金融或政治利益 [31]。知名风险投资公司安德森·霍洛维茨（Andreessen Horowitz）的马克·安德烈森（Marc Andreessen）称其为与互联网一样重要的发明。法国巴黎银行（BNP Paribas）的研究分析师帕利查塔（Palychata）[34]将区块链的创建比作蒸汽机或内燃机的发明，而《经济学人》预测，它将像有限责任公司（Limited Liability Corporations）的发明一样重要的一项创新[35]。

区块链对我们世界的影响程度从 R3 合伙企业的调查中可以看出，该企业研究了分布式账本技术如何影响金融行业的参与者。R3 合伙企业是由 80 家最大的金融机构组成的联盟。R3 合伙企业将其 2015 年 12 月的启动描述为银行和其他金融机构对多代不同遗留系统难以实现互操作性的挫败感的产物。此外，由瑞士银行 UBS 领导的六家最大的全球银行开发了一种“公用结算币”（USC）[36]，这是由中央银行支持的主要货币的数字对应物。他们的目标是开发一个处理交易（接近）实时的结算系统，而不是需要数天。该项目的目的是使全球银行能够使用抵押资产在定制的区块链上相互进行各种交易，并使金融市场更加高效[37]。第三个例子是澳大利亚邮政，该机构发布了开发基于区块链的维多利亚州电子投票系统的计划[38]。区块链的可能性巨大，几乎任何涉及某种交易或跟踪机制的行业都可能且将被区块链颠覆。然而，为了了解我们应该如何利用区块链为社会带来好处，首先让我们深入了解一下这项技术。

区块链是一种共享的、去中心化的公共或私人账本，它描述了所有权的一个单一版本的真实情况[39-41]。它是一个分布式账本，利用数据库技术来记录并无限期地维护一个不断增长的数据记录列表[42]，这些数据记录是不可篡改的、不可撤销的、可验证的和可追溯的[33, 42, 43]。最初，这些数据记录是比特币交易，但现在应用已经扩展到任何类型的在线交易，涵盖任何行业。区块链可以作为社会的记录者，包括注册任何类型的文件或财产[44]。数据记录按时间顺序存储在通过加密方式链接在一起的区块中。网络中的每个节点都拥有区块的副本，为了使交易能够添加到链中，网络中的节点必须达成共识。

结果是，点对点交易成为可能，无需中央认证机构，如银行，通常需要收取少量手续费来完成工作。去除第三方，以及组织者和消费者能够几乎瞬间执行点对点交易的能力，是一个真正的范式转变。本质上，这就是使区块链如此重要的原因。

区块链有不同类型，所选的区块链类型决定了网络中的参与者如何相互交互[33]。有授权和无授权的区块链，各有不同的特征、规则和参与者。无授权的区块链是公共区块链。最著名的例子是比特币区块链。系统内的信任是通过博弈论激励和密码学[33]创造的。这意味着任何有兴趣加入特定无授权区块链的人都可以通过将他的电脑连接到去中心化网络、下载应用程序并开始处理交易来实现。没有必要与账本之前有关系，也不需要批准加入。如果你想开始挖掘比特币并支持比特币网络，只需访问[`bitcoin.org/en/full-node`](https://bitcoin.org/en/full-node)即可开始。一个公开的无授权区块链不属于任何人，每个人都可以参与。

另一方面，授权或私有的区块链不需要这些人工激励，因为网络中的所有参与者彼此都知道[33]。新参与者必须得到网络中现有参与者的批准，这使得在验证交易时更加灵活和高效[33]。私有的区块链通常被那些喜欢保持共享账本以结算交易的组织使用[45]，如金融服务行业内部。它们由一组组织拥有和运营，并且交易只对网络成员可见[45]。一个私有区块链的好例子是瑞士银行 ubs 和其他五家主要银行在 2016 年开发的区块链结算系统[36]。这个区块链使得四家参与银行明显缩短了彼此之间的结算时间，其他任何一方都无法访问区块链或对其做出贡献。

私有和公有区块链是两种存在的风味，对于这两种选项，主要特点是，一旦交易被批准并记录在区块链上，它就不能被更改或编辑。一些较大的金融科技机构（包括中国第一家私人和全数字银行，微众银行）正在考虑将它们的在线银行建立在公有和私有区块链网络的组合之上 [46]。然而，自 2016 年以来，已经开发出了第三种选择。安永会计师事务所已经申请了一项“可编辑区块链”的专利，其历史可以通过中央权威机构进行调整。这有点自相矛盾，因为区块链的力量在于，一旦验证，数据就无法更改。然而，安永声称这种区块链将仅适用于私有权限的区块链——例如，被银行使用，其中中央权威机构可以在商定的治理规则下管理网络 [47]。这种区块链将提供一种“安全按钮”，实际上可以使得区块链更安全地使用。

一个组织可能会选择的区块链类型取决于该组织的目标以及需要存储在区块链上的交易类型。一些交易，如金融交易，不应该对公众可见，而其他交易，如（数字）商品的所有权和土地登记，从公有区块链中获益更多 [48]。无论区块链的类型如何，由于区块链的四个关键组成部分：加密原语，共识机制，交易和智能合约，存储的数据都变得不可篡改，可验证和可追溯。我们分别讨论这些组件。

2.2 加密原语

加密学是任何区块链系统的关键组成部分。除了其他内容外，它包括两个重要特征：数字签名和哈希算法。

2.2.1 数字签名

数字签名基于公钥加密，也称为非对称加密。非对称加密意味着两个数学上相互关联的密钥：公钥和私钥。这种关系意味着任何由一个密钥（公钥）加密的数据只能由另一个（私钥）解密，反之亦然。使用公钥加密数据并用另一个公钥解密数据是不可能的 [49]。因此，您可以使用密钥对来标识某个数字资产的所有者。由于公钥是公开可用的，任何用相关私钥加密的数据只能由对应的公钥解密。它像一个邮箱，每个人都有一个钥匙可以向那个邮箱投递信件，但只有一个人有权利钥匙打开邮箱并取出信件。

公钥基础设施现在已经广泛部署。几乎在线的任何事物都使用公钥基础设施，从发送电子邮件到访问网站（如果一个网站有 SSL 证书并且网站显示 https，那么它就是使用公钥基础设施进行加密的）。这意味着我们可以确信，在您和服务器之间传输的数据没有被中断。公私钥基础设施也用于确保特定文档的真实性，这是使用哈希算法完成的。

2.2.2 哈希算法

区块链上的每一个数据块都会收到一个由安全哈希算法计算得到的哈希 ID，作为数据库的键。一个块的哈希是固定的。换句话说，分配给块的哈希 ID 永远不会改变。哈希算法在区块链技术的各种组件中都有应用，其中之一就是哈希 ID，这是一个独特的 64 位数字和字母字符串，与每个块中的数据相关联。美国国家安全局（NSA）设计了一种称为安全哈希算法 2 的第二代密码哈希函数。它包括 SHA-256，这是一种高效的安全哈希算法，为每块数据创建唯一的哈希 ID。如果数据完全相同，哈希算法会产生完全相同的哈希值[50]。数据中只要改变一个比特位，就会导致全新的哈希 ID。添加到区块链上的块的哈希 ID 是下一个块的开始数据，因此这些块是相互链接的。这意味着如果块中的数据被更改，它将改变该块的哈希，进而改变后续块的哈希等。要篡改数据，区块必须通过共识重新验证。这不会发生，因为网络中的其他节点没有动力去处理链中的“旧”区块。此外，区块链不断增长，因此需要相当大的计算能力来重新验证旧区块，这使得这种做法根本不划算[51]。哈希使区块链上的数据不可变，并且可以验证数据随时间没有发生变化。

2.3 共识机制

人类已经使用了共识决策机制很多年[52]。虽然它最初是应用于政治和社会的概念，但它已经成为计算机科学的一个重要组成部分[53]。共识算法确保连接的机器能够独立协作，无需相互信任，并且即使网络中的一些成员失败，它们也能够继续工作[53, 54]。有许多共识算法采用不同的方法来验证区块链上的值和交易。共识机制对于任何区块链都至关重要；由于共识算法的存在，不再需要信任对方，因此可以创建、实施和评估决策，而无需中心权威[44, 54, 55]。其结果是无中间人的交易，无论是人与人之间、人与机器之间还是机器与机器之间的交易[44]。

共识对于区块链至关重要，因为区块链没有可信任的中心权威机构。网络中的参与者必须就控制区块链的规则以及这些规则的应用方式达成一致，然后才能部署区块链。网络中的节点执行一个达成共识的算法，并且必须有一个预定义的多数节点同意结果。共识算法使用密码学来验证交易（从而决策）），目前，(4)最常用的两种共识算法是工作量证明（PoW）和实践拜占庭容错（PBFT），尽管新的共识算法正在不断开发中[56]。PoW 通常用于无需许可的区块链，而 PBFT 用于需要许可的区块链。此外，权益证明（PoS）是另一种目前正在开发的共识机制。它高度实验性，只在少数山寨币中使用，并且尚未成熟。尽管以太坊正在考虑切换到 PoS，EOS 区块链将使用委托权益证明共识机制。

共识算法解决了与数字货币相关的双重支付问题。双重支付是指想要通过多次使用同一数字货币来欺骗系统的参与者。在法定货币中，这个问题是通过使用中央权威机构（即银行）来解决的。在一个去中心化系统中，没有中央权威机构，可以通过共识来解决。为了理解这个问题，Lamport 和 Shostak[57]提出了拜占庭将军问题，这是一个关于一组指挥不同拜占庭军队部分的将军需要就攻击和征服敌方城市计划达成一致的思想实验。这些将军只能通过信使进行通信，但问题在于至少有一个将军是叛徒。问题是军队中可以有多少叛徒，但仍能作为一个整体行动？每一个共识算法都是拜占庭将军问题的解决方案，第一个提出解决方案的是 PBFT 算法[58]。自那时以来，在比特币被引入之前，已经开发了许多 PBFT 算法。PBFT 算法可以应用于去中心化、受许可的网络，这意味着 PBFT 算法的核心方面是需要一个成员资格，这必须得到中央权威机构的批准。工作量证明算法解决了这个问题[31, 54]。这个共识算法在去中心化网络中运行，没有中央权威机构，但它假定大多数参与者都是“诚实”的参与者，并减少了不诚实参与者的风险。

2.3.1 工作量证明

工作量证明算法解决了需要中央权威机构的问题。工作量证明的技术创新在于它不需要会员资格。因此，不再需要中央权威机构。工作量证明算法因此用于公共或无许可的区块链中，其中参与者无需了解或信任彼此。因此，它被用于比特币区块链中，这是一个公共区块链。这个共识算法要求参与演员解决一个困难的计算问题来验证区块。验证使用密码学完成，这意味着演员必须找到一个不等式的解决方案，这需要大量的计算能力（和能源）。当一个解决方案被提出时，立即就很清楚它是正确的。这可以与填字游戏相比较，这个游戏可能很难解决，但一旦完成，你立即知道它是正确的。当一个演员解决了方程时，解决方案被提交给整个网络，演员会因此获得比特币作为奖励（在比特币区块链的情况下）。

2.3.2 权益证明

权益证明（PoS）是另一种常见的共识算法，它采取了不同的方法。在 PoS 中，正如在 PoW 中一样，验证者是随机选择的，但是，与 PoW 中的验证者相比，如果他们拥有更多的计算能力，他们被选中的机会更大，而在 PoS 中，一个成员持有的货币量（即代币数量或加密货币的量）决定了被选中的可能性[59]。一旦产生了区块，就会支付交易费给那个验证者，签署者将区块提交到区块链上。这些签署者可以是网络中的所有节点，或者是一组随机选择的节点，为整个网络进行签署。为了“激励”节点持有更大的权益，一个节点在网络中的权益越大，节点需要解决的谜题就越简单。因此，已经在网络中拥有大量权益的节点可以很容易地变得更大。PoS 仍然需要对网络的当前状态达成共识，但是一个参与者拥有的加密货币越多，他们对区块链成功的权益就越大。因此，PoS 需要的计算单元计算量要少得多，因此更加节能[60]。PoS 背后的假设很简单：如果一个参与者对系统的权益更高，他们就有更大的动力确保网络是安全和正确的，因为他们会因为加密货币的价格和声誉受损而感到痛苦。预计以太坊网络将在 2018 年实现 PoS 共识机制。

2.3.3 时间戳

共识机制实现了一个时间戳服务[31]，该服务确保添加到区块链中的每个区块都有时间戳，以证明不同事件之间的时序关系[31, 61]。时间戳基本上确认了在区块链上某一时间点发生了某项交易。如果一个参与者试图欺骗系统并再次提供相同的交易，节点将检查交易与时间戳的一致性，如果发现交易在之前的区块中，网络中的节点将达成共识，认为该交易是无效的。此外，时间戳功能与散列值结合使用，使用户能够证明在任意时刻，某一文档是由特定用户在特定时间点所拥有，并且自那时以来该文档没有被更改过[44]（也就是说，它使数据完全可追溯）。

2.4 交易

去中介化交易[44]对区块链技术至关重要，因为它消除了需要信任的集中式第三方，这些第三方通常会收取验证交易的佣金。去除中介（即中介机构）将彻底改变行动者之间的互动方式以及决策的制定、执行和评估[60]。比特币交易仍然是记录在区块链上的最常见交易。然而，任何其他货币、金融合约或硬软资产相关的金融交易也可以记录在区块链上[44]。实际上，任何类型的交易，无论涉及数字还是实体商品，都可以记录在区块链上。这包括土地注册[62]、供应链中商品的追踪[48]、物联网设备交换交易[63]、身份、声誉、自然资源[64]，以及诸如出租车或房屋共享[65]之类的点对点交易所。这个列表无穷无尽，一个完整的概述可以在 Ledra Capital 的网站上查看，该网站正在持续收集区块链的广泛潜在用途[66]。2016 年，首次有两家组织跨越全球进行了用区块链和智能合约支付的交易[67]。澳大利亚联邦银行和美国富国银行利用区块链在所谓的全球首笔独立银行之间的全球贸易交易中，为从德克萨斯州到中国青岛的棉花运输付款。此外，2017 年 12 月，荷兰农业贸易公司路易斯·德雷弗斯公司（Louis Dreyfus Co.）与荷兰银行 ING 和 ABN Amro 以及法国银行 Société Générale SA 合作，利用区块链平台向中国出售了一船美国大豆。他们数字化了文件，能够实时匹配数据，防止了重复，并将整个交易时间缩短了一半[68]。

当所有者（例如艺术家）通过转移与该资产关联的私钥来出售其资产时，物理产品的所有权也可以记录在区块链上[44]。当使用智能合约自动完成此操作时，它被称为智能财产[44]。智能合约是存储在区块链上的交易的一个特殊分支，例如使用以太坊区块链[69]。提议智能合约将对组织设计和决策产生重大影响[44, 65, 69]。

【2.5 智能合约](toc.xlink.xhtml#r2s1-2.5)

术语“智能合约”最初由 Szabo[70]提出，作为“一种计算机化的协议，执行合同的条款”。它可以被看作是一种传统协议，由代码自动定义和执行，没有留下任何自由裁量的余地[44]。智能合约与处理交易和/或决策的脚本类似。它们在区块链上运行，被认为是“加密货币世界的杀手级应用”[71]。随着在区块链上部署的智能合约的出现，定义组织的概念以及组织如何实现竞争优势将发生巨大变化。

智能合约可以被看作是“如果这样，那么那样”的声明，它们被编译成了位代码（尽管要复杂得多）。它们是软件程序，将执行两个或更多参与者达成的某些交易或决策[72]。它们是通过选择事件或前提条件，并提供当这些前提条件得到满足时需要发生的事情来创建的。协议随后记录在区块链上，一旦部署在区块链上，这些脚本就无法再更改，并且一旦前提条件得到满足，它们将始终执行[73]。

智能合约具有三个显著特征：它们是自主的（在部署到区块链后，它们无法再被更改）；它们是自给自足的（它们可以随着时间的推移积累和花费价值）；并且它们是去中心化的（它们分布在网络中的多个节点上）[39, 44]。一旦智能合约上了区块链，它就是最终的，无法更改（也就是说，它们变得不可变、可验证和可追溯）。然而，只有当原始代码允许时，某些参数才能被更改。因此，对于组织来说，确保在智能合约记录在区块链上时代码是 100%正确，且没有留下任何错误至关重要。如我们通过 The DAO Hack 所看到的，错误可能极其昂贵，因为智能合约中的一个错误导致了 5000 万美元的损失[74]。修复已部署智能合约中的错误唯一的方法是通过区块链上的“硬分叉”，这正是 The DAO 所发生的事情。尽管如此，不要期望每次组织部署有缺陷的智能合约时，区块链都会产生硬分叉。

智能合同不仅对合同法有潜在影响，而且更广泛地对社会和组织内的社会合同也有影响。这是因为智能合同是自动和自主执行的，从而消除了对人判定的需要并最小化了信任需求[44]。此外，智能合同消除了开发、实施或评估管理层或员工决策的需要——当多个智能合同结合人工智能和大数据分析时，可以自动化决策能力[44, 69]。这将导致“组织活动的新范式”[44]，自动化（战略）决策、企业数据治理，并创造全新的组织设计[33]，这些完全由计算机代码运行，所谓的去中心化自治组织（DAOs）[69]。

智能合同可能看起来具有革命性，但它们并非新事物，已经存在很长时间了。正如以太坊创始人 Vitalik Buterin 所解释的，智能合同已经在大多数现代办公楼中得到应用。例如，决定你是否被允许进入某个区域的门禁卡由一段代码预定义，并与数据库相连[75]。门禁卡的例子说明智能合同已经存在很长时间了。现在唯一不同的是，当它们部署在区块链上时，它们将无限期地保持可访问性，并在满足某些条件时执行它们预定义的任务。智能合同为组织提供了巨大的机遇，但它们只有在正确的时候部署在区块链上才是至关重要的。在未来的几年里，我们可能会看到大量使用智能合同的应用程序，这些将改变我们的工作方式、商业运作方式以及日常生活。这将很有趣，因为这将逐渐消除中介、管理者和员工。

当管理者或员工不再被需要去运营一个组织时，它将显著改变组织设计以及组织网络内各行动者之间的互动方式[44]。即使一个组织没有完全转向 DAO 设计，区块链和智能合同的使用也会影响行动者之间的互动方式[76]并改变决策能力。区块链通过基于密码学的无需信任的系统减少了网络内的机会主义[55]，并自动化了决策过程。此外，组织之间的联系变得更加紧密，因为它们跨越时间和空间共享同一个数据库，从而增加了网络内的行动者和互动。

采用区块链技术的组织可以被视为人机网络（HMNs），在这种网络中，人类和机器的组合相互作用，以产生协同效应 [77]。根据组织内部区块链整合的程度，它可能会影响战略决策能力。一个组织越是向去中心化自治组织（DAO）设计靠拢，它就会变得越高效和自治。最终，组织可以使用区块链、智能合约和大数据分析完全独立地运营，而 DAO 将不再有任何管理或员工 [69]。参与者之间的互动将完全由自主软件算法指导 [39, 44, 62]，这增加了 DAO 股东在区块链上谨慎部署智能合约的需求。区块链的不变性、可验证性和可追溯性特性意味着需要采取措施，以避免如果智能合约带有漏洞将会造成的巨大损害 [73]。然而，错误的智能合约并不是组织想要迁移到区块链时面临的唯一挑战。区块链仍然是一项新兴技术，许多（技术）挑战仍然需要解决，才能实现大规模采用。

2.6 改变组织设计

尽管区块链是比特币的基础技术，但加密货币并不是区块链的唯一可能应用。任何交易都可以记录在区块链上 [39]。智能合约可以启用各种应用，不仅限于金融市场和/或“自我执行的自治治理应用” [73]。因此，对于组织来说，区块链的可能性几乎是无限的，以创建新的、分布式的产品和服务，这将导致现有组织结构中的效率提升 [33]。这种区块链启用的产品和服务通常被称为去中心化应用程序，或 DApps。一个 DApp 至少具有两个显著特征 [44]：（1）对 DApp 协议的任何更改必须得到共识的批准；（2）应用程序必须使用一种加密代币或加密货币，该代币或加密货币根据一组算法生成。目前已经有一些 DApps 的例子，其中比特币当然是知名度最高的。目前所有已知 DApps 的详尽列表可以在 dapps.ethercasts.com 找到。

此类去中心化产品和服务的发展将改变组织设计。区块链不需要中心化权威来进行维护，因为数据库存储在数百万台去中心化计算机上，其去中心化基础设施确保了单一案例的误管理，导致故障点，不会影响整个网络[45]。此外，由于基于密码学的无需信任的系统，区块链和智能合同的使用将使一个组织能够控制和减少机会主义，同时自动化决策。这将，反过来，对组织设计[55]以及任何法律，监管，IT 和会计框架[72]产生直接影响。区块链消除了在缺乏中心化管理机构时的信任需求。因此，任何开发 DApps 的组织仍然应该对数据治理有强烈的关注。毕竟，只有数据的真实性可以得到保证；可靠性和准确性则不能。借助区块链，可以直接在网络中嵌入数据治理，将代码带到数据[45]中。法律法规可以编程到区块链本身，使其自动执行，从而使治理变得更容易[78]。因此，账本可以作为数据的法定证据，增加数据所有权、数据透明度和可审计性的重要性。这种组织设计的结果最终可能导致 DAO 的建立。

DAO 是一种由智能合约组成的组合，可能与物联网设备、大数据分析和人工智能相连。它由不可篡改的代码在一套不可逆转的业务规则**独占控制**下运行[39]。DAO 将拥有来自今天组织中的不同参与者；它将需要广泛的数据治理流程，以确保数据的可靠性和准确性，并将导致一种根本新的组织结构[44, 79-81]。DAO 是一个自我组织的框架，它使用基于共识的自动化决策，其中参与者无需相互信任即可相互交互。在 DAO 内部没有传统的组织层次结构，因为层次结构是由所有权（即参与者被信任的程度以及由于行为而获得的该参与者的功绩）决定的。这种组织结构的变化影响了权力平衡。在传统组织中，权力要么通过层次结构，要么通过知识来分配，而且这些往往是有关系的；层次结构越高，你拥有的信息越多，你在组织内的权力也越大[82]。在 DAO 中，这种方式有所不同。权力由参与者拥有的代币数量、参与者的信任级别和他们实现的功绩来决定。这将使组织内的权力平衡从层次结构转变为分布式结构，从而影响治理结构[83]。

在它的最简单形式中，DAO 就是不可更改的计算机代码：一系列智能合约的集合，部署在区块链上，促使参与者自我组织。代码定义了 DAO 内的治理结构，因为治理就是实现在智能合约中的规则。借助区块链技术的功能，DAO 可以被看作是一个使用共识机制来自动做出决策的自我组织结构，无需信任。因此，在 DAO 内部，没有传统层级（因为没有员工或管理者），没有传统治理（因为代码就是治理，规则已嵌入智能合约中），也无法通过电子邮件或电话联系 DAO，只能与聊天机器人互动（因为整个组织是自动运作的，无需人员参与）。然而，DAO 仍然可以作为传统组织运作，尽管它们是自主运作；它们可以订购产品和服务，有客户和供应商，也可以盈利或亏损。它与传统组织有相同的活动；需要赚钱，有成本，有客户、股东，甚至员工（尽管这些是独立承包商），提供产品或服务，并受到监管要求（尽管作为分布式公司，这变得更加困难，因为监管要求在不同司法管辖区可能相互矛盾）。因此，在开发 DAO 时，治理结构非常重要，应该将治理结构纳入 DAO（代码中）。此外，还应确保 DAO 的代码长期有效并正确运行，因为一旦部署在区块链上，它就不可逆转。缺乏治理或质量保证可能会产生重大后果，正如 2016 年的 The DAO 攻击所显示的那样[84]。因此，总结来说，希望建立 DAO 的参与者必须确保在代码中实施正确的治理结构，并确保代码正确运行，以保证 DAO 一旦部署就能正常运作。

到目前为止，我们还没有看到任何真正的、成功的 DAO。第一个 DAO，“The DAO”，在智能合约中出现漏洞，让黑客可以将 5000 万美元转移到自己名下后，就被停止了。然而，已经有一些尝试创建 DAO，其中 DAX 和 Digix 是最为人所知的。Digix 是一个建立在以太坊上的资产代币化平台。他们通过将区块链的不变性、透明性和可审计性应用于贵重实物资产（另请注意，Digix 在 2016 年的首次代币发行—或 ICO—中在短短 12 小时内筹集了 550 万美元[85]）。Dash 是一种开源的对等加密货币，提供即时和私密的交易。有些人还将比特币归类为 DAO，尽管这种分类是有争议的。

为了更好地理解未来社会中真正的 DAO 会是怎样的，让我们来看一个几年后 DAO 在现实世界中运作的科幻例子：

想象一下在不太遥远的未来，一家自动驾驶出租车公司。消费者可以通过一个类似 Uber 应用的 App 调用出租车。一旦出租车被订购，它会自动接上乘客并把他或她送往请求的目的地。车辆会自动选择最佳路线，避开交通和绕行。一旦乘客离开出租车，钱就会通过智能合约自动转账。收到的服务费会用来如果需要的话自动维护车辆。一旦车辆注意到需要维护，它就会自动与汽车服务中心预约。维修人员会自动立即收到需要做什么以及是否需要订购任何零件的报告。经过多年的优质服务，车辆会注意到它的寿命已经结束，并自动将自己驶向汽车回收公司。在那之前，智能合约已经根据市场需求的看到订购了一辆新的自动驾驶汽车。一旦旧车被回收，新车离开工厂并接上第一名乘客。整个过程中不会有经理或员工参与。大数据分析用于自动改进服务，了解客户并监控车辆。^(5)

虽然要等到这样的 DAO 出现可能还需要一段时间，大概十年左右，但这是时间问题。利用智能合约、大数据分析、人工智能、机器学习和物联网完全自动化一家公司的过程不仅可以在出租车行业完成，也可能在零售、银行、制造甚至餐饮业实现[86]。显然，治理始终很重要，还有不少挑战需要解决。毕竟，在 DAO 中，多个行动者，无论人类还是非人类，必须相互依赖地合作。在这种系统中，冲突和协作的数学模型可以激励行动者为了整个系统的最佳利益而行动。DAO 为我们重新设计社会和商业方式，以及创建更高效的组织提供了令人兴奋的机会，这些组织能够以更低的成本提供更好的产品和服务的。

2.7 代币发行融资——每家公司自己的中央银行

对于 DApp 或 DAO 来说，加密货币（有时被称为密码货币或代币）是一个重要的方面。多年来，初创公司一直在寻找投资者投资他们的项目，以建立下一个 Facebook 或 Google。然而，资金昂贵，任何筹集资金的初创公司都必须向投资者提供公司股份。投资者加入得越早，风险越高，对创业者的成本也越高。这是过去几十年的范式。现在不再是这样。自从区块链兴起以来，时代正在改变。新兴创业公司筹集资金的最新方法已成为代币发行融资，或称 ICO（也称为代币生成事件）。

代币发行融资（ICO）越来越多地被区块链初创公司使用，通过分发初始代币供应量的百分比来筹集资金[87]。基本上，通过 ICO，初创公司扮演了银行的角色；它从无中数字化创造货币，并将其出售给“投资者”。在众筹销售中出售的代币或加密货币将用于平台支付交易并在利益相关者之间分配价值。在 ICO 期间购买这些货币的“投资者”并不会获得初创公司的股份，但他们希望货币价格上涨，从而能够获得（可观的）投资回报。

一些初始币发行（ICO）可能非常成功。例如，去中心化数据存储网络 Filecoin 的 ICO 在 2017 年 9 月筹集了约 2.57 亿美元。Filecoin 在不到一个月的时间里就筹集了创纪录的金额。然而，早期的 ICO 之一是以太坊的。2014 年，以太坊通过其加密货币以太币（ETH）的 ICO 筹集了约 1840 万美元。在 ICO 时，1 个以太币的价值约等于 0.31 美元（2000 个以太币兑换 1 个比特币），而在此书的撰写之际，1 个以太币的价值已从 11.27 美元上涨至 1228 美元，随后又跌至 600 美元。^(6) 另外两个非常成功的 ICO 是 Bancor，在五小时内筹集了 1.53 亿美元，以及 Block，在五天内筹集了 1.85 亿美元。2017 年底，安全的通讯应用 Telegram 宣布进行 ICO，以帮助他们发展去中心化生态系统。2018 年 3 月，他们通过私人代币销售已经筹集了约 17 亿美元，到您读到这里时，最终筹集的金额将会明了。当然，这些筹资活动也引发了关于目的、信任和治理的问题。臭名昭著的是，一些 ICO 和交易所运作着庞氏骗局和其他诈骗。只要有钱可赚，欺诈和欺骗就可能随之而来。本书后面会讨论这些例子。

在 ICO 期间出售的货币通常用于资助构建平台的开发。在许多情况下，一个平台甚至尚未建成，而初创企业的创始人只有一个想法或解释平台目标的白皮书。因此，ICO 的风险极高，并且因为它们通常发生在政府监管机构的范围之外，对于投资者来说没有任何保障或保证[88]。

想要进行 ICO 的初创企业应该对此非常重视，并确保 ICO 符合所有相关法规。通常，初创企业会天真地认为，因为它们是在美国之外注册的，所以不需要考虑美国证券交易委员会（SEC）的要求[89]。然而，不遵守 SEC 的规定是非法的，可能会影响初创企业的创始人。

尽管如此，当前 ICO 是一种非常流行的筹集资金的方式。在过去的几个月里，有些 ICO 在几天、几小时甚至几分钟内就筹集了数百万美元。一些最成功的 ICO 包括：DAO（在三周内筹集了 1.6 亿美元，随后在 DAO 黑客攻击中损失了 5000 万美元）[90]，Bancor（在三小时内筹集了 1.53 亿美元），Block.one（筹集了 1.85 亿美元），Sirin Labs（在 2017 年 12 月筹集了 1.57 亿美元以开发基于区块链的智能手机），Polkadot（在 2017 年 10 月筹集了 1.45 亿美元，以允许人们同时使用多个区块链），以及 Status（在 2017 年 6 月筹集了 1.07 亿美元，以提供一个使使用以太坊变得更加便捷的界面）。这些大规模的 ICO 与早期的 ICO 相去甚远，早期的 ICO 在当时被认为是极为成功的。例如，在 2016 年，Lisk 在四周内筹集了 570 万美元，而 Synereo 在四周内筹集了 470 万美元，SingularDTV 在仅 17 分钟内筹集了 750 万美元。回到 2015 年，Augur 筹集了 520 万美元，其中前 2000 个 BTC 在仅 12 小时内售罄。截至您阅读这篇文章时，这些数字在与最近趋势和记录相比将显得微不足道。正在进行中的 ICO 列表可以在[www.smithandcrown.com/icos/](http://www.smithandcrown.com/icos/)或[`tokenmarket.net/ico-calendar`](https://tokenmarket.net/ico-calendar)找到。

然而，并非全是好消息。ICO 中存在一些骗局。许多 ICO 更像是对冲基金，试图通过承诺高回报来吸引人们。OneCoin 是最近被曝光为庞氏骗局的最大的数字货币骗局之一[91]。另一个骗局是 GAWMiners，他们基于谎言在 ICO 中筹集了 1900 万美元[92]。如果没有可用的测试版，或者更糟糕的是只有有限的文档，以及/或者不清楚开发者是谁以及他们的背景是什么，参与 ICO 风险极高，消费者可能会被骗走他们的钱。即使一切看起来都很好，就像 Tezos 的巨大 ICO 一样，在 2017 年 7 月筹集了 2.32 亿美元，事情也可能很快变坏。2017 年 12 月，根据 Tezos 涉嫌违反美国证券法并犯有投资者欺诈行为，提起了一项集体诉讼。

在 SEC 对 DAO 黑客攻击进行调查之后，SEC 裁定一些出售的代币实际上是证券，投资者在决定是否投资时应该小心。证券交易委员会可能会在未来宣布更多指南[93]。中国走得更远，在 2017 年完全禁止了 ICO；这是中国社区提出一些 ICO 是金融诈骗和金字塔计划的结果[94]。

由邪恶“企业家”组织的诈骗是投资者参与 ICO 时可能失去资金的一种方式。不幸的是，加密货币诈骗还有很多种。最常见的是所谓的“泵与 dump”计划，例如在即时通讯应用 Telegram 上的私人团体成员决定推广他们所拥有的货币，以便以更高的价格出售。在股票市场，这种做法是非法的，但许多司法管区的加密货币市场仍然未受监管。这种行为可能导致波动性增大，普通投资者遭受巨大损失。犯罪分子还试图通过复制热门 ICO 的网站并试图引导人们到错误的网站来窃取资金。当人们将资金转到给定地址时，他们从未收到任何代币作为回报。此外，还出现了假冒交易所、庞氏骗局、假冒钱包和网络钓鱼尝试的例子。

这些诈骗事件导致了包括中国和大韩民国在内的各国在 2017 年和 2018 年对加密货币进行了打击。当然，这也使得加密货币市场一片混乱，一些货币的价值在几小时内几乎下跌了 50%，比特币跌幅达到了 25%。许多政府机构和监管机构都在努力了解加密货币，并为它们制定法规。然而，彻底禁止加密货币、加密货币交易所和首次币发行（ICO）并不是解决问题的办法。相反，我们需要的是关注交易所遵守了解你的客户-反洗钱（KYC-AML）法规和 ICO 遵守类似于首次公开募股（IPO）的法规的全球法规。只有这样，我们才能获得一个更加成熟和规范的市场，不会限制创新，造福所有人。

正如任何新技术创新，特别是在信息技术领域一样，监管机构总是落后于新兴市场和对旧系统的破坏。等到法律和规定实施时，它们往往不再适用于数字空间。一旦新的规定公布，社区就会向前迈进，开发新的解决方案。此外，无论政府能否防止黑客攻击、垃圾邮件或网络钓鱼，它们都无法防止加密货币市场的黑客攻击和抢劫。此外，由于加密货币本质上是去中心化、虚拟和无国界的，试图在网络的一部分对这种现象进行监管是不起作用的。正如德国联邦银行的大卫·吴尔迈林在 2018 年初所说的，唯一规范去中心化现象的方法是通过全球协议：

因此，对虚拟货币的有效监管只能通过尽可能的国际合作来实现，因为国家监管权力显然是有限的。^(7)

全球法规的问题是，它们需要时间，而且许多国家对禁止或监管加密货币有不同的动机。尽管如此，监管机构在尝试全球法规时可以关注的两个领域是：加密货币交易所和 ICO。

法规可以迫使加密货币交易所遵守 KYC-AML 义务，以防止不允许进行交易的人进行加密货币交易（尽管由于其固有的去中心化特性，它们永远无法防止用户在交易所外进行交易）。法规还可以强制交易所采取正确的安全措施。不幸的是，完全防止黑客攻击或数字抢劫是不可能的。

此外，监管机构应该关注 ICO。围绕 ICO 的更简洁的过程肯定可以防止诈骗和庞氏骗局。与现有的 IPO 法规类似，ICO 应该遵守某些法规，以保护投资者并使推广者负责。然而，法规不应完全禁止 ICO，因为它们确实具有巨大的潜力。因此，类似于欧盟开发的《通用数据保护条例》（GDPR）合规性，应该为 ICO 制定全球标准。这些法规可能包括诸如以下要求：

•   在 ICO 之前披露财务、会计、税务和其他业务信息；

•   通过智能合约实现托管功能，确保只有在达到某些里程碑时才释放资金。如果未能达到这些里程碑，资金将自动退还；

•   拥有一个与公司有实质性参与的顾问团队，而不是使用顾问的股票照片，甚至盗用别人的身份。

•   拥有一个说明书，告知潜在投资者 ICO 涉及的风险。

除了法规，政府和管理机构还应该关注的另一个领域是教育公民了解涉及加密货币交易的风险，并帮助消费者了解他们应该如何处理这些风险。到 2017 年，俄罗斯已经宣布了一个计划，旨在教育其公民关于加密货币以及投资于它们所涉及的风险。更多的国家应该效仿，帮助公民了解这一新现象是什么以及涉及的风险有哪些。

然而，似乎 ICO 是势不可挡的。初创公司已经发现了这种筹集资金的盈利方式，并充当自己的中央银行，尽管监管机构很可能会试图监管 ICO，并对进行 ICO 施加限制或规则。加密货币将从根本上改变我们在线进行交易的方式，以及我们使用和构建新产品和服务的方式。它们将对区块链为社会带来好处产生重大影响，并可能持有解决一些邪恶问题的关键，但关于这一点将在接下来的章节中详细介绍。

2.8 区块链平台

本节考虑了一些正在为区块链开发新技术的组织。当然，这并不是已经可用的技术的详尽列表。开发新工具和解决方案的公司数量不断增加，在这里我们提供了三种不同类型的区块链初创公司的例子。下面提到的公司只是为了说明已经存在的东西。

2.8.1 以太坊

以太坊旨在重新发明互联网，现在已经存在几年了。它是一个去中心化平台，用于开发通过智能合约运行的 DApps。这些智能合约是执行任务的小型软件程序，是一种“如果这个，那么那个”的声明（但复杂得多）。它们运行在定制的区块链上，因此不存在欺诈、审查或第三方干预的机会。以太坊开发了一个极其强大、共享的全球基础设施——以太坊虚拟机，它可以执行任意算法的复杂度的代码。他们正在不断扩展基础设施，并为分布式网络构建新的解决方案。

2.8.2 Ripple

Ripple 是一家专注于金融服务行业的区块链初创公司。他们声称自己不是在用区块链，而是在用分布式账本技术。他们开发了一种分布式账本技术，使世界各地的银行能够发送实时国际支付，而不需要中央权威机构。实际上，它是一个全球范围内的任何类型的货币即时转账的支付网络。他们开发了一个分布式的全球网络，托管支付节点，以便在全球范围内转移价值。银行可以监控和协调分布式账本上的资金转移，风险和延迟最小，与今天解决国际交易所需的时间（可能长达一周）相比。

2.8.3 IOTA

IOTA 是一种与上述完全不同的加密货币，因为它不使用区块链，而是使用一个称为 Tangle 的有向无环图。它专门为工业 4.0 而开发，在工业 4.0 中，连接的设备必须能够相互执行微交易或纳秒交易。因此，它具有以下特点：

• 无限可扩展性，因为它不使用区块或矿工。相反，每个想要执行交易的一方都必须验证两笔交易；

• 没有交易费用，从而使连接的设备能够进行纳秒交易；

• 工作量证明（Proof of Work）共识机制，需要的计算能力最小，可以由连接的设备执行；

• 完全去中心化，与比特币等半去中心化网络形成对比。

2.8.4 其他初创公司

2016 年，对区块链初创公司的投资金额首次超过 10 亿美元，2018 年第一季度，ICO 融资额达到 60 多亿美元，因此要提供一个完整的区块链初创公司概述是不可能的【95】。然而，我们下面列出的是一些在去中心化和分布式领域工作的更有趣的初创公司，按字母顺序排列。当你读到这本书的时候，这些初创公司中的一些可能已经不再存在：

埃弗雷德：钻石认证和相关交易历史的永久账本。

卡尔达诺：一个旨在提供比此前任何协议都更为先进功能的智能合约平台。

恒星：一个连接银行、支付系统和个人的平台。能够快速、可靠地转移资金，几乎不产生成本。

NEO：以太坊的竞争对手，NEO 正在开发一个智能经济的开放网络。

硬币基地：一个购买和出售比特币和以太坊的平台。

利斯：一个使您能够开发和发布具有您自己的侧链的区块链应用程序的平台。

区块链流：提供使用区块链的软件和硬件解决方案。

tØ：一个基于区块链的交易平台。

开放市场：一个去中心化市场。

比特沸石：最大的比特币挖矿基础设施提供商之一。

奥古普：建立在以太坊区块链上的去中心化预测市场。

神经元：开源的、去中心化的人工智能。

玛伊德：一个分布式平台，能够实现快速、安全的应用创建。

IPFS：一个点对点的分布式文件系统，旨在取代 http。

想象：开发一个声誉协议，以实现个人、组织和事物的协作。

EOS：一个为 DApps 提供智能合约平台的区块链项目，其代币销售中筹集了超过 40 亿美元。

当然，还有许多其他的区块链初创公司每天都在这个市场上扎根。

【2.9 需要克服的区块链挑战】（toc.xlink.xhtml#r2s1-2.9）

区块链走的是一条与许多可能对世界产生重大影响的破坏性技术相同的路径。因此，它仍然面临一些挑战，这些挑战需要时间才能克服。

随着关注点从比特币转向区块链的巨大潜力，似乎区块链将解决世界上许多问题，但它仍然是一个非常年轻的技术。下面是一个概览。

【2.9.1 可扩展性问题】（toc.xlink.xhtml#r2s2-2.9.1）

可扩展性是区块链的一个主要问题，至少对于公共区块链来说是这样。最受欢迎的区块链，比特币区块链，现在已经达到 170 吉字节【8】（#note8），并且每十分钟每个区块以 1 兆字节的速度稳步增长。区块链的设想是，分布式网络中的每个节点都有一个完整的区块链副本。所以，如果你想开始在比特币区块链上验证交易，你首先必须下载整个区块链。

解决可扩展性问题的潜在方案之一可能是“区块链修剪”。这基本上意味着网络中的节点只使用包含最后几百个块的区块链的验证表示。整个区块链仍然可用，但只在几个节点上。在撰写本文时，比特币社区就区块大小是否应增加至 2 或 4MB 的问题进行了大量讨论。随着比特币的普及，可扩展性问题可能会持续存在。2017 年，这一可扩展性挑战导致比特币矿工之间出现分歧。结果，一些矿工决定进行硬分叉，创建了一种新的加密货币，比特币现金，它支持高达 8MB 的区块。比特币现金区块链的大小自那时以来已增长到 159GB。^(9)

私有区块链，如 Hyperledger，扩展性问题的压力较小，因为它们只包含对处理交易有直接利益的节点。尽管私有区块链比单个集中式数据库更昂贵，但如果你加上所有那些被区块链替代的集中式数据库的成本，它仍然要便宜得多。

2.9.2 交易速度和成本

交易速度和成本也是某些区块链的主要问题（尽管并非全部如此）。IOTA 的分布式账本（Tangle）以零成本实现无限扩展。然而，比特币区块链确实面临着交易和成本的重大挑战，并且由于它是最发达的区块链，我们重点关注比特币区块链。当比特币推出时，每个人都对几乎可以忽略的交易成本感到兴奋。几乎免费地即时将资金发送到全球各地，这创造了一个完全新的世界，它绕过了在跨国转账时需要银行的需求。然而，事情已经发生了变化。2017 年 12 月 21 日，平均交易费达到了每笔交易最高水平，为 54.90 美元。

显然，如果你想进行一笔小额交易，比如说用比特币买咖啡，这变得不可能了。如果你用比特币向全球转移大量资金，数百万甚至数千万美元，这样的费用与你必须支付给银行的费用相比相对便宜。然而，对于一种加密货币来说，要想被广泛接受，并有可能取代法定货币，它应该适用于每个人进行每种类型的交易。

交易费用高昂的原因在于，目前每个区块的大小限制为 1 MB，几乎每个区块都完全装满了交易。例如，2018 年 5 月 4 日，平均区块大小为 974 kB，这意味着每个区块都充满了交易。比特币的设计方式是这样的：验证交易的矿工必须使用大量的计算能力（即能量）。如果对验证交易的需求不断增加，矿工会优先处理支付更高费用的交易。经济学原理 101 告诉我们，如果需求增加，但供应保持不变（每个区块可以验证的交易数量），价格就会上升。

增加交易费用的另一个原因是新诞生的加密货币比特币现金（Bitcoin Cash），它在 2017 年 8 月 1 日从比特币中分裂出来。比特币和比特币现金是非常相似的加密货币，这意味着矿工可以很容易地从比特币转向比特币现金，如果挖矿比特币现金更有利可图（背后的逻辑与比特币和比特币现金协议的发展有关；矿工越少，挖矿难度越低，赚取更多金钱的可能性就越大）。比特币网络上矿工的减少意味着供应减少，从而导致交易费用增加。

当然，比特币社区已经意识到这个问题，并且正在尝试实施解决方案来增加区块的大小，从而增加供应并降低交易费用。比特币社区关于区块大小的问题正在进行一场辩论，有多个赞成和反对增加大小的论据。现实情况是，如果不解决这个问题，每秒的交易次数仍然有限，交易费用将继续增加。或者，如以太坊创始人维塔利克·布特林（Vitalik Buterin）所说：[数字黄金这一利基市场]如果是比特币用户想要的，那么他们应该保持限制，甚至可以减少。但如果比特币用户想要成为一个支付系统，那么区块大小就必须增加。

2.9.3 因安全问题导致的负面形象

显然，区块链提供的去中心化方法具有一些优势。黑客攻击和/或审查数据变得困难得多，Hashcash 算法的使用确保了无法恢复哈希内容。尽管比特币区块链已经存在了近十年，但它还没有被黑客攻击过。然而，围绕它的许多服务已经被攻破。DAO 被黑客攻击，随后几乎失去了 5000 万美元 [90]。这仅是因为一个“硬分叉”才得以预防。Mt Gox（当时世界上最大的比特币交易所）被黑客攻击，结果 4.6 亿美元不翼而飞 [97]。此外，基于香港的比特币交易平台 Bitfinex 失去了 7000 万美元 [98]。更近一些，2018 年 1 月，日本交易所 Coincheck 被黑客攻击，导致 6600 万美元的 NEM 代币损失。这些黑客攻击并没有帮助比特币和其他加密货币的形象。尽管比特币只是区块链的一个应用，但这些攻击使公众偏离了区块链的真正价值。人们可能对这些围绕区块链的安全问题感到不安。

2.9.4 能源消耗与成本

验证交易需要计算机解决复杂的谜题。这反过来又需要大量的计算能力和费用。在能源消耗方面，比特币是一种特别不可持续的货币。工作量证明（Proof of Work）共识机制需要大量的计算能力。据 VICE 报道，2015 年，单个比特币交易大约使用了足够电力来支持一个美国家庭一天的用电 [99]。这导致了估计的年能源消耗大约为 16 太瓦时。

CERN（欧洲核子研究组织）每年大约使用 1.3 太瓦时电力来驱动大型强子对撞机[100]，这一数字与冰岛全年的能源消耗相当。这几乎是 VISA[101]能源消耗的 30,000 倍（VISA 在 2016 年处理了 823 亿笔交易[102]，而 2017 年的比特币交易大约有 1 亿笔）。随着区块大小的潜在增加，解决谜题所需的能量将继续增加。此外，考虑到大多数矿池都设在中国，大部分能源消耗都是由不可持续的煤电能源厂驱动的。尽管矿工可能会转向清洁能源，但比特币挖掘实际上是在浪费能源[103]，因为作为工作量证明共识协议一部分的复杂计算机计算毫无价值。计算过程并没有解决任何世界性问题，只是证明了计算已经完成。在一个理想的世界里，我们会看到真正有助于公共利益的共识算法的开发，就像 reCAPTCHA 所做的那样，用于训练神经网络。

在气候变化的时代，比特币的能源消耗是一个严重的问题。当然，像权益证明这样的不同共识机制确实解决了这些问题，但包括比特币区块链在内的许多区块链继续使用工作量证明。除非比特币切换到不同的共识协议，否则比特币的能源消耗将迅速变得不可持续。

2.9.5 人才短缺

区块链技术仍然处于初级阶段，因此并没有多少开发者掌握与区块链相关的技术。目前已经有了数百个区块链初创公司，它们都希望从同一个人才池塘中捕鱼。因此，对于想要迁移到分布式网络的组织来说，吸引合适的人才变得越来越困难。就像几年前的大数据一样，它需要时间才能让大学跟上步伐，并开始为分布式网络开发正确的课程。这种培训合适毕业生的延迟可能会减缓新应用的发展。

2.10 关于区块链采纳过程中的怀疑和批评

2017 年，澳大利亚政府的数据研究和工程中心——Data61——产生了两份报告，详细说明了区块链技术的长期情景和即时技术应用^(11)。Data61 报告描述了区块链在澳大利亚可能使用的某些机会，包括监测害虫或动物和植物疾病的爆发、进行边境监控、追踪知识产权，以及建立提供对权利、福利和税收义务更大确定性的身份系统。报告还提供了一些经过良好研究的洞察，解释了为什么一些在 2015 年和 2016 年启动的主要区块链项目停滞不前。在这里考虑区块链解决方案面临的问题是有用的，因为这些问题引起了媒体关注，并导致了一些关于区块链作为我们全球化世界中一些基本问题解决方案的负面情绪。

自 2015 年以来，世界各地的银行、监管机构、科技巨头和初创公司已经筹集了数十亿美元来探索区块链的潜力。但迄今为止，唯一真正成功、可“规模化”的区块链应用仍然是加密货币。阻碍尝试将区块链的能力应用于其他应用程序的问题都是基于风险的，并分为三大类：隐私和欺诈。

当谈论区块链与隐私时，首先需要区分私有账本和公有账本是很重要的。公有账本无法提供隐私保障。比特币系统内的隐私已经被证明是高度漏洞百出且启发式的，几乎没有任何接近高保障的东西。这是因为交易是全局公开的，而且在大多数应用中并没有进行加密。如果这些数据是个人数据，例如“医疗或财务数据”，这将把监管和法律问题带到台前，特别是在德国，该国拥有 some of the strictest privacy regulations。即使尝试加密和隐藏个人信息，仍然可能统计或元数据。一种解决方案是将加密后的数据存储在区块链上，但这会导致另一个问题：如果特定信息的解密密钥丢失，数据可能无法准确恢复。此外，如果密钥被窃取并公开，所有数据都因为数据无法被更改而在区块链上永远解密。有关公钥基础设施的更多信息，请参阅第三章。

在 2017 年 3 月向非洲区块链会议发表的讲话中，Andreas Antonopoulos 警告说，许多最近的“区块链”项目都是打着创新和颠覆性技术的幌子筹集资金的欺诈企图。在金融交易中使用区块链也使遵守反洗钱立法面临问题，该立法要求任何提供金融服务的人（例如）都必须确信他们的客户或客户的身份。此时，智能合约和加密货币的一个问题是它们容易受到操纵。这是美国证券交易委员会在 2017 年 3 月拒绝批准 Winklevoss 比特币资产信托注册的关键原因。

这些缺点可能解释了为什么许多高调的区块链项目在 2015 年、2016 年甚至 2017 年停滞不前。例如，2017 年年中，加拿大银行宣布其区块链项目 Jasper 尚未准备好处理结算业务。该银行以透明度和隐私问题为由，认为使用区块链的好处不足以抵消风险[104]。

风险并不是区块链项目停滞不前的唯一原因。2017 年 2 月，银行和技术专家组成的 R3CEV 联盟在投资、创新和测试了 18 个月后宣布，他们不会为其项目使用区块链，因为他们不需要它。这个决定并不构成对区块链承诺或声誉的攻击。这只是一个基于应用是否适用的实际决策。

找到解决区块链面临的实际风险和挑战的解决方案对于开发者、投资者和推广者来说是一个优先事项，他们希望吸引足够多的用户，使运行网络变得可靠和有利可图。

在 2017 年 9 月在上海举行的第三届全球区块链峰会上，Vitalik Buterin 承认了这些问题，并为以太坊项目提出的解决方案提供了一份路线图。在与 1200 名政府、行业和学术专家的观众面前，他提出，通过创建用户账户（用于由中央当局管理的网络），或者通过被称为 SNARKS 和 STARKS 的零知识证明，可以轻松解决安全和隐私问题，这可能解决公共网络的问题。

SNARK 是一种简洁的非交互式知识论证，它使提取验证成为可能，以便将其发布到网络上作为一个额外的证明。与此同时，STARKs 是可扩展的透明知识论证。这种零知识证明通过提供一种统计（概率）可检查的证明来改进验证过程。这些措施将改善链中每个块的数学防御性验证。

为了解决安全性和可扩展性需求产生的问题，以太坊开发者将分片技术视为可能的解决方案。区块链无法处理比单个节点更多的交易。这在很大程度上是比特币限于每秒三到七笔交易，以太坊也只能处理每秒七到十五笔交易的原因。以太坊的承诺是，分片技术将改变区块链的验证方式。被称为分片的网络节点的小 subset 将验证每一笔交易。这意味着以太坊区块链将保持安全，同时允许更好的可扩展性。还有一些全新的解决方案正在生产中，如物联网区块链初创公司 IOTA，它提供了一种新版本的区块链，称为“纠缠”，提供无限的可扩展性。

仍有一些问题悬而未决，还有一些疑问尚未得到解答。例如，这些创新实施的时机尚不明确，它们的性能也尚未得到测试。重要的是，技术专家与用户一样关心未来的发展方向。这一刻让人联想到 1989 年互联网发展过程中困扰路由安全的问题，当时互联网鲜为人知，难以解释，人们用冲浪和超级高速公路的比喻来形容它，令人捧腹。

最终，区块链技术可以帮助改善防御性的网络安全策略，特别是在身份和访问方面。人们正在探索解决方案，它们承诺提供的网络安全和隐私保护超过互联网上以往的任何体验。网络安全威胁每天都在出现，而旧的威胁仍然存在，等待再次被利用。区块链技术不会成为网络安全的神器，但它是一个强大的工具，可以帮助加强系统。

2.11 去中心化和分布式社会

近年来，技术极大地改变了我们做生意和生活的许多方面。不幸的是，我们的经济、法律和政治体系并没有跟上这些变化[105]。因此，我们的行政控制也没有跟上，我们的经济、法律和政治体系仍然以官僚方式运作。所以，这些体系往往效率低下，缺乏透明度，并容易遭受欺诈行为。区块链技术可以改变这一点，去中心化和分布式社会的机遇是巨大的。哈佛商学院的 Marco Lansiti 和 Karim Lakhani 两位教授认为，区块链不仅仅是一种“革命性技术，而是一种基础性技术，具有为我们的经济和社会体系创造新基础的潜力”[105]。为我们的经济、法律和政治体系建立新基础需要时间（可能几十年），并将带来许多不同的挑战。然而，一旦我们完成这个过渡，它将导致更好的、更透明、更公平的经济、法律和政治体系。

一个去中心化和分布式的点对点世界将带来许多好处，这是我们的经济和社会系统目前所缺乏的。去除中介机构将降低做生意的成本，（智能）合同将根据预设条件自动执行，社会将被重塑，我们将需要更少地依赖中介机构，无论是政府还是盈利组织。当然，想要转向区块链的组织也将享受这项技术所有的益处；它将帮助他们降低成本，减少欺诈，提供更好的服务，变得更加透明，总的来说，成为一家更好的公司。然而，这本书并不是关于公司如何使用区块链的。如果您想了解您的公司如何通过使用区块链变得更加盈利，我们建议您放下这本书，阅读一本关于商业区块链的众多书籍之一，这些书通常写得非常好。在第十章中，我们确实为组织提供了一个路线图，介绍如何在其业务中实施区块链技术。这本书全部关于解决我们社会面临的许多“棘手问题”，这些问题是由经济、法律和政治体系的滞后造成的。我们的目标是解释区块链如何帮助这些体系迎头赶上，我们真诚地相信，如果政府和组织关注区块链的社会价值，我们可以为所有人创造一个更好的世界。因此，我们关注那些对社会产生负面影响的問題，并对每个这些问题讨论其身份和性质。问题的范围和影响是什么，我们为什么应该关心？迄今为止已经做出了哪些尝试来解决问题，区块链如何解决问题？去中心化和分布式方法如何为解决“棘手问题”提供新的见解？我们深入探讨了一些已经存在的最佳实践，以及这些障碍及其可能的解决方案。本书讨论的七个“棘手问题”是：

•    身份；

•    贫困；

•    气候变化；

•    腐败、逃税和洗钱；

•    公平贸易；

•    选举舞弊和剥夺选权；

•    审查制度。

如果我们能够使用去中心化和分布式解决方案解决上述“棘手问题”，我们将创造一个对我们的现有系统提供许多优势的点对点世界。尽管技术发展将需要至少十年或更长时间，但一旦我们创建了一个基于点对点协作的去中心化和分布式社会，我们就创造了一个更好的世界。

2.12 结论和启示

区块链是一种分布式账本技术，确保数据和合同存储在透明和共享的数据库中，并通过共识机制和密码学保护数据免受删除、篡改或修改。哈希算法确保我们总能控制一个文档、所有权或交易是否已被修改。区块链上记录的不变性确保我们总能追溯到交易的起源，控制或监控跨越时间和空间参与交易的人员。除了交易，区块链还可以存储智能合约，所谓的“如果这个，那么那个”的声明，尽管要复杂得多。这些合同用代码编写，跨司法管辖区可理解，并确保一旦满足了某些预设条件，某个特定动作将自动发生。当你开始将一个或多个智能合约与大数据分析、人工智能等技术结合时，创建 DApps 或甚至 DAOs 成为可能。DAO 是一个没有管理或员工的组织，完全由代码运行，其中（数据）治理在代码中执行。这种方式，我们应该如何运行一个组织的现有范式被彻底改变。

区块链及其已经开发的数百个 DApps，为我们展示了未来可能的样子。区块链仍处于早期发展阶段，还有很多开发工作要做。然而，由智能合约运行的去中心化应用程序，无需中心化的 governing power 通常抽取大量佣金，具有巨大的优势。它们运行成本更低、更高效，更难以被政府或中心化组织控制，比现有应用程序更安全、更透明。正是这些技术和应用程序（区块链、智能合约、DApps，甚至 DAOs）可能有助于解决 Wicked Problems。

注解

1    本书在撰写“比特币 vs. 比特币”时遵循了行业惯例。当写作 Bitcoin 时，它指的是这项技术，而当写作 bitcoin 时，它指的是加密货币。

2    区块链只是分布式账本技术的一种形式。还有更多版本的分布式账本技术，例如 IOTA 开发的 Tangle。然而，在本书中，我们关注的是称为区块链的分布式账本技术，为了论述的需要，将其他分布式账本技术的变体也归入区块链（尽管从技术上讲，这些变体当然有所不同，有时甚至差异显著）。

3    本书在撰写“区块链 vs. 区块链”时遵循了行业惯例。区块链指的是作为一种整体的技术/趋势，而区块链则意味着一个或多个区块链——一个分布式账本数据库。

4   需要注意的是，围绕区块链的技术发展非常迅速，以至于在你阅读这本书的时候，这些内容可能已经过时了。

5   这个例子最初是由以太坊创始人 Vitalik Buterin 创作的，并为此书进行了改编。

6   2018 年 2 月初的价格—[`blockchain.info/charts/blocks-size`](https://blockchain.info/charts/blocks-size)。

7   德国中央银行表示，比特币的规定必须是全球性的—[www.reuters.com/article/us-bitcoin-regulations-germany/any-rule-on-bitcoin-must-be-global-germanys-central-bank-says-idUSKBN1F420E](http://www.reuters.com/article/us-bitcoin-regulations-germany/any-rule-on-bitcoin-must-be-global-germanys-central-bank-says-idUSKBN1F420E)。

8     根据 2018 年 3 月的数据—[`blockchain.info/charts/blocks-size/`](https://blockchain.info/charts/blocks-size/)。

9   2018 年 3 月的数据显示—[`bitinfocharts.com/bitcoin%20cash/—as`](https://bitinfocharts.com/bitcoin%20cash/—as)。

10   [`blockchain.info/charts/avg-block-size`](https://blockchain.info/charts/avg-block-size)。

11  参见‘分布式账本’（2017 年）和‘使用区块链和智能合约的系统风险与机遇’（2017 年），这两篇文章都可以在这里找到—[www.data61.csiro.au/en/our-work/safety-and-security/secure-systems-and-platforms/blockchain](http://www.data61.csiro.au/en/our-work/safety-and-security/secure-systems-and-platforms/blockchain)。