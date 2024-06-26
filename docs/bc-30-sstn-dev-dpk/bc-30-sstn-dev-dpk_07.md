# 第七章 可持续医疗保健的区块链 3.0

Ashok Bhansali O.P. Jindal University，印度，ashok.bhansali@opju.ac.inJolly Masih Prestige Institute of Engineering Management and Research，印度，jolly.iabm@gmail.comMeenakshi Sharma Global Group of Institutions，印度，sharma.minaxi@gmail.com

#### 摘要

随着数字化的增加，与患者健康信息、电子健康记录、基于物联网（IoT）的健康监测系统、保险数据等相关的大量数据正在产生。区块链 3.0 提供了巨大的分布式存储空间，不需要太多的资源，提供了可扩展性而不牺牲安全性，帮助整合来自不同来源的数据而不损害隐私，提供了透明性而不透露所有权，确保了互操作性而不引入太多的复杂性，并建立了带有真实性的出处。区块链技术的灵活性和多维能力为医疗保健领域的创新、整合和可持续性提供了很多潜力。人工智能、分析和智能合约的融合有助于利用核心区块链技术为医疗保健领域的整个价值链的所有利益相关者创造更好的价值主张。这对医疗保健审计、临床研究、打击假药、医疗合规、政府监管、药品供应链管理、索赔结算等方面都有所帮助。

这一章旨在解释区块链 3.0 在整个医疗体系价值链中的不同应用、方法和模型的实施，并讨论了可能导致转型并增加整个医疗行业可持续性的最重要的用例。这一章从技术角度、挑战的视角、实施策略和未来发展方向讨论了区块链采用的旅程。本章介绍了区块链技术如何影响和影响医疗领域的广泛细分，以及如何提高可持续性。第一个最重要的用例解释了区块链如何帮助创建、交换和维护完整、准确、安全和可转让的患者医疗记录，并且所有的合规性都齐备。智能合约提供了受监管和透明的数据访问，可以帮助无需中间人的冲突自由快速理赔解决。第二个用例解释了区块链如何帮助简化医疗保险公司的流程，并为患者以及医疗业务增加价值。区块链与人工智能、机器学习和数据分析一起，通过从大量数据中得出推论，固定责任，并以更有效和更便宜的方式分发研究报告，从而帮助研究和临床试验管理，以实现更快速和更好的科学研究结果。第三个案例研究说明了区块链 3.0 如何更好地管理临床试验。第四个用例解释了区块链如何改进制药供应链管理，并减轻假冒、伪造和未批准药品和设备的风险。当然，医疗领域对区块链 3.0 的采用速度很慢，但该技术为医疗系统的可持续性提供的附加值已引起了研究人员、政府和医疗公司的注意，他们在这一领域进行投资，以实现更美好的未来。

关键词：区块链、分布式账本技术、可持续医疗、互操作性、制药供应链、临床试验、健康保险、医疗管理。

## 7.1 介绍

整个世界正在快速迈向工业 4.0。新兴和颠覆性技术可以帮助提高生产力和收入，并为更好的经济增长和整个医疗领域的可持续性提供了大量机会。人们相信，通过采用新兴技术，医疗保健每年将能够节省约 1000 亿美元，而区块链技术将在其中发挥最大作用。

随着数字化程度的提高，医疗行业产生了大量数据，但由于与数据共享相关的各种问题，不同的利益相关者无法利用这些好处，例如完整性、隐私、安全性、真实性和责任制。区块链通过其设计本身以有效和高效的方式解决了这些挑战，并在金融部门证明了其实施。区块链 3.0 通过其扩展功能和丰富的 API 可以通过启用有效的协作、数据交换、减轻数据威胁、自动化后勤工作和改善收入周期管理来改变卫生部门。区块链有潜力增加几乎所有医疗部门的可持续性，如患者健康记录（PHR）、供应链、临床试验、健康保险、制药研发等等。事实上，爱沙尼亚已成为第一个采用基于区块链的医疗保健系统的国家，以确保其所有公民的电子健康记录（EHRs）的安全性和完整性[1]。

## 7.2 区块链技术

区块链是由一位匿名的个人引入世界的，作为创造世界上第一个虚拟货币比特币的技术[2]。它是一个协议，用于创建一系列通过加密哈希函数链接的交易块，并使用数字签名实现无信任的分布式账本技术[3, 4]。技术的详细支撑超出了本章的范围，但我们将介绍技术的概念和工作原理，以了解其在医疗领域的用途。

简而言之，区块链是一个共享的区块记账本，其中包含了交易的记录，可以是加密货币、智能合约、健康信息、保险政策或任何信息。每个区块以及其中的交易都使用密码哈希嵌入了前一个区块的消息摘要，以确保不可变性。每个区块都通过分布式点对点（P2P）网络上的密码协议连接到前一个区块上，通过互联网广播。发生的任何交易都由私钥签名以确保隐私和不可否认，并广播到网络中。挖矿节点验证此交易，将其添加到区块中并广播到网络中。网络节点使用共识协议和已知算法（例如工作量证明）验证区块的有效性。一旦交易块得到验证，它就会使用密码哈希函数附加到现有的区块链顶部。每个区块都使用时间戳排序，并由区块链上的所有节点更新。区块链不归任何人所有，它使用经过验证的密码技术嵌入隐私和信任；并允许每个用户存储、分享和查看区块数据。不同的共识机制和密码函数可用于解决各种隐私、透明度和访问使用问题。

### 7.2.1 智能合约

智能合约是通过在区块链网络上嵌入编程代码，代替传统手工合约的一种方法，从而实现协议条款的自动执行。它是一种基于区块链的创新方法，实现了分散式自动化，如图 7.1 所示。

![](img/b_9783110702507-007_fig_001.jpg)

图 7.1：智能合约的流程和优势。

当预定义的合约条件得到满足时，智能合约会自动执行，从而提高了效率、信任度、透明度和实时结算，无需任何争议。存在着不同性质的智能合约 - 确定性和非确定性。确定性合约在区块链上具有所有所需信息，而非确定性合约需要来自外部数据源的信息。第一代区块链，即比特币的合约编写功能非常有限，而下一代区块链，例如超级账本和以太坊支持完全定制的智能合约。基于区块链的智能合约在消除第三方验证、执行条款和自动化数据管理的复杂过程方面发挥着核心作用。

### 7.2.2 区块链的分类和演化

区块链实现根据它可以被如何使用和谁可以使用而分为以下任何一类[10]，通常，决策者根据预期用途选择适当的区块链。表 7.1 描述了区块链分类及其特点和用途。 

表 7.1：区块链分类。

| 区块链类型 | 特点 |
| --- | --- |
| 公共区块链 |

+   完全去中心化的公共网络

+   无许可分布式账本

+   任何人都可以添加和验证交易

+   为公众提供加入和支持网络的激励。

+   比特币、以太坊、莱特币等。

|

| 私有区块链 |
| --- |

+   属于个人或组织所有。

+   限制性或许可区块链

+   允许选定用户验证和添加交易

+   通常，任何人都可以查看交易。

+   Multichain、Corda、Hyperledger 等。

|

| 联盟区块链 |
| --- |

+   半去中心化网络

+   共享给一组组织

+   许可账本，可供所有人或少数人使用

+   由授权节点控制，信息只能由授权帐户添加。

+   R3、能源网络基金会等。

|

| 混合区块链 |
| --- |

+   提供私有和公共区块链的优势

+   使用公共区块链来访问账本

+   后端使用私有区块链进行访问控制和更新账本

+   免疫 51% 攻击

+   VeChain、瑞波网络、IBM FoodTrust 等。

|

区块链技术随着时间不断发展，并被划分为三个阶段[11]。所提出的技术的第一个实现仅用于加密货币，称为区块链 1.0\. 随后，区块链引入了智能合约的概念，智能合约是嵌入在分布式账本中的编程代码，在预定义条件满足时执行[7]。Eris 和 Ethereum 属于 2.0\. 第三代，区块链 3.0，扩展了 API 和功能，用于政府和不同领域（如能源、健康、土地等）的非金融应用。区块链 2.0 和 3.0 还引入了新的共识协议，以服务于目的，如股权证明、委托权益证明、实用拜占庭容错等[12]，如图 7.2 所示。

![](img/b_9783110702507-007_fig_002.jpg)

图 7.2：区块链技术的发展。

### 7.2.3 区块链在医疗领域的应用

区块链可以通过改善任何被描述如下的业务流程或操作的效率和效果来增强可持续性：

+   发生大量交易（信息），需要与多方共享。

+   不同的未知方需要协作和信任交易。

+   中介不可信且效率低下。

+   强大的安全性和多样化的数据控制是确保系统完整性的期望。

图 7.3 显示了基于区块链的医疗保健系统的高级概述。健康领域通常涉及多个利益相关者，包括患者、制药公司、保险提供商、医院和研发公司。每个方生成大量数据，所有这些的可持续性都取决于及时的信息流、保持透明度和信任、确保数据的隐私和正确性，并共同做出数据驱动的决策。区块链有巨大潜力改变古老的医疗保健系统，并在数据安全、隐私、共享和存储方面真正发挥了很大的帮助[13, 14]。考虑到当前情况，区块链似乎最适合用于医疗保健系统，以增加价值并使其更可持续。

![](img/b_9783110702507-007_fig_003.jpg)

图 7.3：基于区块链的医疗保健系统的高级概述。

## 7.3 互操作性

互操作性是确保正确信息传达给正确人员/方并导致每年数百万人丧生和数十亿美元损失的最大瓶颈。互操作性使得不同的医疗信息系统和软件应用能够在组织内部或外部进行通信、交换和使用共享信息。此外，全球范围内的医疗生态系统正在演变为依赖数据驱动决策和协作工作的价值驱动护理模式。互操作性可以通过减少手工录入数据等行政问题的时间和成本来节省成本，并提高系统的运行效率[15]。它通过及时顺畅地访问患者信息来提高临床决策能力和响应时间。

### 7.3.1 互操作性的级别和挑战

存在四种不同级别的互操作性。基础或第 1 级处理互连性需求。它展示了一个信息系统与其他系统交换患者或临床数据的能力。结构或第 2 级建议数据的结构。它定义了需要交换的格式和语法，以及在数据级别的解释。语义或第 3 级是互操作性最复杂的级别。它包括数据集的模型、值、编码、标准词汇和对用户的意义的规则。最高级别是组织或第 4 级，旨在解决法律方面、治理和政策以确保数据安全和无缝交换。此级别还有助于定义工作流程和最终用户之间的值得信赖的合作。

EHR 采用是启用互操作性的主要阶段，已经被许多利益相关者实施。下一阶段是健康相关数据在所有利益相关者之间的无缝流动，但存在三个主要挑战，即技术、市场营销和系统性。不同的 EHR 软件采用不同的格式存储记录，使它们彼此兼容是一个巨大的技术挑战。数据的完整性和隐私是最关键的，互操作性可能提供单一的妥协点。此外，医院和病理学已经在传统系统上投入了大量资金，他们不愿意为了互操作性而进一步投资。不同的 EHR 解决方案提供商销售具有各种功能和服务的专有系统，而互操作性削弱了它们的竞争优势。中间人在整个医疗空间起着非常重要的作用，去中介化并不容易。此外，由于缺乏指南和框架，政府无法强制执行单一的互操作性标准。

### 7.3.2 区块链 3.0 实现互操作性

表 7.2 说明了典型的互操作性痛点以及区块链如何帮助解决这些问题。基于区块链的智能合约驱动的应用可以帮助摆脱中间商。实施集成医疗企业协议在实现互操作性方面发挥着非常重要的作用。它有助于方便地交换个人健康记录（PHRs）、EHRs 和医疗健康记录（MHRs）。一个区块链上的交易通常可以存储 EHRs 的引用，并且智能合约可以嵌入不同利益相关者访问 EHRs 的规则。这有助于微调谁可以访问什么以及多长时间。此外，区块链本质上包含了所有与数据相关的活动的不可改变记录。区块链可以真正帮助改善流程和合规性，避免冲突，节省成本和高效数据管理[16]。它还可以帮助克服单点故障，并通过更快速、可靠的数据访问帮助医学研究[17]。

表 7.2：互操作性挑战和区块链解决方案。

| 痛点和挑战 | 区块链解决方案 |
| --- | --- |
| 建立一个维护所有数据交易完整记录的可信代理是困难的。 | 信任是使用共识协议和加密功能的网络的隐含部分。 |
| 对于较少数量的交易，每笔交易的成本更高。 | 去除中间商和分布式网络使基于区块链的系统更加高效，降低成本。 |
| 大量的专有标准使互操作性困难且低效。 | 参与节点上的实时数据更新使操作高效且互操作性可行。 |
| 数据的隐私和安全性是更大的挑战。 | 加密哈希函数使数据安全，而公钥私钥确保隐私。 |
| 互操作性可能会产生单一故障点或网络攻击。 | 分散和分布式网络以及加密时间戳确保不可变性和更好的安全性。 |
| 整合专有数据格式的更改是困难且耗时的。 | 智能合约可以用于实时基础上的变更。 |

所有医疗记录或其引用都可以直接存储到区块链上，以确保安全性并使其对他人可见。然而，大型数据，例如 MRI 图像，会降低处理速度，因此较小的数据直接存储在链上，而大型数据则保留在链下，并且可以在区块链上保存指向它的指针。可以编写一个 API，通过智能合约方便地获取数据。这些 API 可以分发给所有参与节点，以便与现有数字系统实现无摩擦的集成。类似地，另一组 API 可以用于从区块链中查询信息。这种基于 API 的架构允许组织加强其内部系统，并且可以自动从区块链上获取所需数据，以确保互操作性。

### 7.3.3 示例用例

最重要的用例是爱沙尼亚，它是世界上第一个采用区块链系统安全存储其公民医疗记录的国家 [1]。爱沙尼亚政府与荷兰公司 Gaurdtime 合作实施了一项电子健康记录，将来自不同医疗保健提供商的所有 PHR 和 EHR 统一整合起来。它采用 KSI 区块链技术来维护检索到的 HERs、MHRs、PHRs 和访问日志的完整性。所有公民都有一张智能卡，用于将他们的 EHR 数据与其私人身份关联起来。一旦 EHR 得到更新，就会创建一个新的哈希，并将记录添加到区块链中。

MedRec 是由麻省理工学院媒体实验室和以色列医疗中心开发的试点原型。它使用分散系统提供互操作性，以共享数据和管理授权、权限等。患者可以上传他们的数据，并授权或取消使用权限。为了保密，数据存储在数据库中，仅在区块链上存储引用和权限。它使用以太坊平台使人们了解有关数据使用的信息 [18]。

MedBlock 是一种基于区块链的用于搜索医疗记录的应用程序 [19]。患者的记录由医疗部门维护和分组，并且 MedBlock 包含对区块链上每个记录的引用。数据的操作和权限存储在区块链上，并且使用智能合约进行执行目的。

BlocHIE 充分利用了链下和链上数据存储的便利性和功能[20]。健康记录存储在提供者的数据库中，而区块链存储链下记录的引用，用于验证目的。为了提高性能和公平性，作者提出了两种事务打包算法：FAIR-FIRST 和 TP&FAIR。

快速医疗互操作性资源（FHIR）链是一个基于区块链的网络，实现了方便分享临床数据记录的 FHIR 标准[21]。它使用以太坊来分享和管理医疗记录数据，针对遵守 ONC 的患者。ONC 与埃森哲的白皮书还建议，区块链具有隐含的功能，可以帮助实现医疗记录的互操作性[22]。

BlockCloud 是一个部署在云环境上的区块链应用，用于保持数据分布，安全，并提供巨大的云存储空间[23]。Gem Health Network 是使用以太坊建立的，旨在改善患者护理，并节省常规数据交换的成本[24]。

## 7.4 健康保险

随着全球化、自由化和人们意识的增强，健康保险的范围不断扩大。在许多国家，健康保险由政府和私营企业提供。利用技术的巨大机会，作者认为区块链的特性可以为整个保险行业增加很多价值，并通过降低成本、管理风险、提高客户满意度水平、增加业务，最终为所有利益相关者提供价值主张。

### 7.4.1 健康保险面临的挑战

任何保险公司的运营流程都是多方面且复杂的，而医疗保险由于直接涉及人们的生命而变得更加复杂。在当今情况下，医疗保险生态系统是一个多层次系统，由保险提供者、承保人、患者、医院和病理学、第三方管理员（TPA）和政府组成。所有不同的参与方都维护着自己的电子健康记录（EHRs/EMRs/PHRs），并且因为许多不同的原因而不愿意与他人共享这些记录。这种由权威主导的纸张繁琐的手工系统容易受到操纵和错误的影响。所有人的积极互动和合作都希望能够及时进行索赔结算，但整个网络却高度混乱且效率低下。根据美国国家医疗保健反欺诈协会的说法，仅在 2018 年，美国就因医疗欺诈和错误而损失了约 3000 亿美元。这些损失最终由保险公司承担，并对整个系统的可持续性提出了质疑。在当今激烈的竞争环境中，医疗保险领域的所有利益相关者都比以往任何时候都更加关注信任、透明度、隐私、安全性、纠纷和不满的问题。

### 7.4.2 区块链 3.0 用于医疗保险系统

表 7.3 提及了医疗保险系统的典型痛点。区块链具有所有技术扩展，可以为整个保险流程链添加大量价值。它可以帮助消除由于非标准化和非互操作性而引起的瓶颈，实现跨行业无缝数据集成。基于区块链的解决方案可以帮助自动化不同利益相关者之间复杂的信息流动。去中心化的分布式区块链网络和密码哈希有助于促进完整性和安全性，而数字签名和共识确保了隐私、信任和透明度。智能合约可以通过从所有保险公司收集证据来维护一个最新的虚假和伪造方的数据库，每个人都可以访问。这将有助于通过向许多方重新提交索赔，使用虚假身份、假账单和报告等手段减少欺诈和无效的保险索赔。

表 7.3：区块链对现有医疗保险系统的增值。

| 痛点和挑战 | 区块链解决方案 |
| --- | --- |
| 区块链的分布式账本技术（DLT）和密码哈希确保了数据的完整性和安全性。 |
| 索赔验证涉及大量手工操作，导致延迟和客户不满。 | 智能合约可以自动化整个端到端流程，索赔可以实时结算，无需人工干预 |
| 总是存在中央服务器上存储的政策数据被盗或泄漏的威胁。 |
| 当前系统需要大量的文书工作，容易被操纵和意外错误。 | 所有节点共享相同的数据副本。如果数据意外或故意更改，则每个节点立即知道。 |
| 理赔结算需要中介和大量数据的复杂交换。 | 互操作性和智能合约自动化整个流程，并将中介从系统中移除。 |
| 患者数据的隐私是一个重大挑战。 | 区块链使用数字签名来维护隐私，同时共享数据。 |

区块链智能合约从系统中移除中介，并帮助实时自动化理赔结算流程。它从区块链总账中获取所有信息，如保单条款、费率和协议，并确保所有利益相关者访问相同的数据，从而消除错误或虚假信息。一旦达到设定条件，预先同意的理赔结算逻辑将以程序形式嵌入其中，并在满足条件时立即执行。这些内置的业务规则确保及时适当地进行理赔结算，同时保持监管合规性和审计报告[25]。TPA 和核保人员的手动工作、信息访问和验证的延迟以及不必要的争议可以以一种可追溯的方式自动解决，如图 7.4 所示。

![](img/b_9783110702507-007_fig_004.jpg)

图 7.4：基于区块链的医疗保险流程。

### 7.4.3  使用智能合约进行保单核保和理赔处理

医疗保险领域正在迅速发展，并采用数字化来提高客户满意度和收入管理。许多业务规则可以嵌入智能合约中，以更好地管理和记录交易到区块链网络[26]。整个核保流程可以更透明、防伪和高效。

现在让我们逐步了解这个过程：

+   智能合约可以帮助电子提交保单文件以及医疗史。特定的保单条款和限额/限制可以根据各方达成的协议自动设置。

+   一旦提交的文件被自动验证，就会为保费支付发出发票。

+   保费可以在特定的到期日自动扣除。一旦完成，保单文件、网络医院列表和特定条款/条件将变为不可变，并提供给所有利益相关者。

+   理赔提交可以自动化以提出理赔请求。一旦提交了所有文件，如理赔表、账单、报告等，就可以由授权医生建议。智能合约通过无缝集成来自所有利益相关者的所有记录来确保提交数据的真实性。

+   一旦索赔被审批者批准，并且合同中的所有条件都得到满足，它就会自动执行，并且金额将转账至受益人账户。

+   所有相关信息，包括扣除等，都由被保人接收，并且如果需要，可以提交重新考虑的请求。

### 7.4.4 使用智能合约进行欺诈检测

由于虚假索赔和欺诈行为，保险公司损失了主要收入的很大一部分，约为 8.5%。当前的运营机制和数据管理系统不允许轻易识别欺诈索赔。主要原因是每家公司都维护自己的数据，并因不同原因而避免共享。有许多不同类型的欺诈，例如虚假政策，夸大和索赔未覆盖的疾病。基于智能合约的区块链系统确实可以有效地管理欺诈[27]。以下系统可能有用：

+   保险公司联盟为每个服务提供商分配一个智能合约。智能合约地址成为一个标识，并且用于唯一标识特定的服务提供商。

+   不同的保险公司对不同的服务提供商进行评级，智能合约在区块链分类账中管理所有这些，这是无法篡改的。此外，这对于所有贡献方成员都是可见的。

+   如果某提供者的聚合评分点数低于某一值，则将其列入黑名单，并且不允许进一步经营业务。这一事实连同统计数据向所有参与的贡献方成员提供。

+   智能合约具有内置功能，可以修改评级并在所有贡献方成员达成一致意见的情况下恢复黑名单提供者。

通过对代理商进行认证并跟踪其历史，也可以限制欺诈行为。目前，我们没有一个整合系统来跟踪涉及不端行为和欺诈的代理商。区块链与智能合约可以帮助实现代理商的透明度和信任，如下所示：

+   在联盟区块链上注册代理商可以被强制执行。每当代理商在网络上注册时，都会创建一个帐户，并且哈希成为该代理商的唯一标识符。

+   客户以及保险公司都可以通过各自的账户使用智能合约为代理商分配评级。

+   如果有人想要查看代理商的评级，将执行智能合约并获取评级。

### 7.4.5 示例用例

医疗保险领域是一个非常关键的领域，可以为整个医疗生态系统的可持续性增加很多价值，而智能合约具有真正改变这一领域的潜力[28]。然而，迄今为止，非常有限的原型或概念验证（PoC）已经部署，甚至用于实验目的。

MIStore 是一个基于区块链的医疗保险应用程序[29]。它旨在帮助行业使用以加密方式存储在网络上的真实不可变数据。MIStore 协议由记录节点和轻节点组成。记录节点维护和存储整个区块链，并使用 PBFT 共识协议将正确的区块添加到链中。每个轻节点只存储区块头。它在以太坊上实现，并使用其嵌入式签名方案 ECDSA 与 secp256k1 椭圆曲线来签署消息。

Culver 提出了一个基于智能合约的区块链解决方案，实现了 FHIR 标准[30]。它提出使用 API 进行实时理赔，并建议组建一个负责促进基于智能合约的操作和推动部署的联盟。服务提供商、受益人和政府，每个人都应该成为这个过程的一部分，以就标准化、政策和监管问题做出决策。

Nukala 等人开发了一个工作模型，利用基于区块链的分散环境提供透明度和数据完整性来处理大数据。他们使用了 IPFS 在同一框架中跨不同应用程序的互操作性概念[31]。

## 7.5 临床试验

临床试验涵盖了广泛的研究范围，涉及众多利益相关者来测试新治疗方法的功效和安全性。该过程涉及试验方案设计和注册，患者招募和参与，数据收集和分析，数据共享和管理，以及结果的报告生成和发布[32]。区块链可以通过直接授权各种参与者以更好和更大的方式控制数据，并将信任嵌入整个试验链，显著加快试验过程并提高可持续性。

### 7.5.1 可持续临床试验的挑战

在临床试验过程中，许多利益相关者参与其中，拥有不同类型的投资、利益和承诺。这产生了复杂而庞大的数据轨迹，有效地管理这些数据是试验可持续性面临的最大挑战。临床试验容易受到有意和无意的错误以及数据篡改的影响[33]，并且往往不遵循定义的步骤和/或可能记录与案例相关的不正确的数据[34]。大量资金和努力因数据分析不足、试验设计不良、出版偏见和结果操纵而白白浪费。患者招募和保留是临床研究成功的最重要但也最具挑战性的因素[35, 36]。约有 86%的临床试验难以按时实现其招募目标，19%的试验由于招募不足而被迫关闭或终止。患者招募在预算中占约 30–35%，特别是在第 II 和第 III 阶段，而招募失败则反映在研究结果不足、试验过早终止、资金浪费，并且可能使计划的招募期加倍[37]。

### 7.5.2 临床试验的区块链 3.0

表格 7.4 阐述了现有临床试验流程的典型挑战以及区块链如何在其中发挥作用。在保护数据、确保隐私、完整性、出处、不可变性、可追溯性的同时，以透明、可信赖和自动化的方式与所有利益相关者分享数据，最好的方法是将整个临床试验流程部署到区块链上，并使整个流程可持续化 [38]。Benchaufi 等人解释了如何在试验的每个步骤中使用区块链使其更具可持续性，从试验设置、患者招募、数据收集、试验监控、数据分析到结果发布 [32]。在设计试验和同意协议之后，在试验开始之前，监管和业务规则被编程到智能合约中，并部署到区块链上 [39]。关于数据如何收集、不同事件发生的时间表以及许多其他重要数据的信息可以存储在区块链的元数据中。基于区块链的设置可以保证数据的完整性和保密性。它帮助将数据的完全控制委托给患者，患者可以以精细调整的方式分享数据，甚至可以撤销分享。它有助于建立信任，并鼓励患者分享用于临床试验的数据 [40]。它使研究人员以及患者能够安全地共享数据，确保隐私并控制不同试验的同意 [41]。

表格 7.4：区块链对现有临床试验系统的增值。

| 痛点和挑战 | 区块链解决方案 |
| --- | --- |
| 试验设计和同意协议在实地实施过程中偏离了。 | 基于智能合约的 DApps 可以帮助验证协议在整个周期内是否符合监管代码。 |
| 患者招募和匹配困难且存在操纵空间。 | 区块链为患者的招募提供匿名性和隐私，智能合约可以用于纳入/排除标准。 |
| 试验志愿者对数据收集程序及其安全性和使用方式感到担忧。 | 区块链交易数据是不可变的并始终保持更新。患者可以通过私钥控制数据共享和安全性。 |
| 数据解释错误和研究不端可能会带来灾难。 | 区块链共识算法确保数据完整性，DLT 可以帮助追溯数据的来源。 |
| 选择性报告和协作研究的困难。 | 区块链试验数据具有时间戳，透明和可信赖。DApps 可以帮助带有问责制的协作研究。 |

许多人对同意书的使用持有顾虑。区块链可以很好地解决这个问题，其中确认的同意书可以作为交易存储在网络上。不同版本的同意书按顺序链接，链中的最新版本被视为试验的版本。只有像 FDA 这样的权威机构才能将包含/排除协议插入智能合约。符合条件的方，如赞助商，可以向智能合约发送请求，根据基因、人口统计、治疗和地理分布等进行适当的主题匹配。一旦确定了符合条件的受试者，试验过程可以在不知道患者姓名的情况下进行随机化。智能合约还可以确保试验是合法的，赞助商是可靠的，以及试验是否被相关机构批准。区块链还可以用于开发公开登记处，用于快速披露临床试验结果。所有参与方可以实时访问这个中央存储库，有助于减少试验时间线。它还可以帮助进行没有中央试验中心的虚拟试验。

### 7.5.3 示例用例

BlockTrial 是一个基于以太坊区块链的智能合约试验 PoC（Proof of Concept）。它包含一个患者智能合约（Patient SC）用于患者注册和权限记录，以及一个研究人员智能合约（Researcher SC）用于自动查询临床试验数据库。所有的查询都是根据设定的权限自动过滤和触发的，使用智能合约进行注册用户。庄等人提出了一个私有的基于以太坊的模型，该模型具有多个基于试验的合约，用于患者参与和试验监控。它还有一个主智能合约，用于主题匹配，患者注册和基于试验的合约管理。

为了改进试验性能，开发了四个新的并行和分布式组件来补充核心区块链[45]。这些模型旨在进行多样化的协作研究，并包括大数据分析、数据集成、物联网设备的身份管理、隐私保护以及数据共享工具。Choudhury 等人共享了一个具有基于智能合约的数据管理框架的权限区块链，以自动化多地点临床试验的行政任务，并维护数据的完整性和隐私性[46]。在临床试验流程之上提出了一个非常有趣的同意管理流程[32]。他们建议同意书加上时间戳以管理顺序，并且智能合约可以用于注册。他们阐述了一个主记录可以包含完整同意收集周期存在证明的流程，可以从互联网网站验证。

Wong 等人开发了一个治理和管理试验数据的区块链原型。通过模拟，他们解释了附加在交易中的密码哈希如何确保数据的安全性。此外，模拟显示即使不检查每个文件的内容，也可以验证完整性[47]。Nugent 等人采用了类似的方法，并展示了区块链如何提供试验历史的不可变记录以及如何消除数据操纵[48]。

## 7.6 医药供应链管理

对于任何行业来说，管理供应链都是一个复杂的过程，但有效管理医疗保健供应链会使情况变得更加复杂，因为它直接影响到人们的生活。这是一个多层次系统，数据、收入和药物的流动来自于多个实体，从制造商、分销商、物流公司、医院、零售商、患者等等。例如，仅美国就从国外进口了大约 40% 的药物和 80% 的药物制造成分，仅在 2018 年就记录了 1750 起假药案件。

### 7.6.1 医药供应链的区块链 3.0

表格 7.5 解释了现有制药供应链存在的问题，以及区块链如何为其提供解决方案。区块链的核心特性确保了原产地，并帮助完全端到端地跟踪制造、分销和消费。它简化了操作，降低了成本，提高了可追溯性，并增加了所有利益相关者的可持续性。

表格 7.5:区块链为医药供应链系统增加的价值。

| 痛点与挑战 | 区块链解决方案 |
| --- | --- |
| 行业正在与假药、盗窃和囤积问题作斗争。 | 区块链可以帮助为药物分配加密身份，这个身份是可以被所有人验证的，并且确定了责任。 |
| 弄清药品的安全性、起源和制造过程是一项非常困难的任务。 | 区块链在每个阶段都固有地增加了溯源性、不可变性和可见性。 |
| 许多不同监管机构在许多阶段提出了太多和非常严格的合规要求。 | 基于区块链 3.0 DApps 的智能合约有助于自动化任务并引起警示。 |
| 许多畅销药物需要冷链运输，这容易被操纵。 | 区块链结合物联网、机器学习和分析，使整个冷链数据实时可用并自动分析。 |
| 制药业是全球性业务，但跨境发送货物和付款是复杂的。 | 区块链已被证明是一个金融工具，智能合约可以帮助解决冲突并建立信任和透明度。 |

基本概念非常简单且保持不变。每个产品都与一个新的哈希相关联，可以是 QR 码的形式，并在区块链网络上注册。这个产品在网络上成为一个数字资产，借助物联网和其他技术，其完整移动记录为交易；并根据设定的规则是可追溯和可访问的。与产品相关的其他信息可以根据需求和性能问题存储为离线或在线数据。

### 7.6.2 示例用例

为了提高医药产品的安全性和交付效率，谢等人提出了一种区块链机制[49]。基于智能合约的系统使用权威证明，并在区块链网络上实时显示供应链数据。Molina 等人还提出了一个框架，以实时追踪药品并有效管理供应链[50]。每个节点都可以跟踪药品并检查交付状态。

Kumar 和 Tripathi 使用了一种有趣的基于 QR 码的区块链解决方案来应对药品伪造问题。它有助于确保药物送达最终用户[51]。Drugledger 是一个旨在提高药品供应链可追溯性的区块链网络[36]。它采用了被认为比 P2P 网络更好的面向服务的架构。它还建议了数据存储方法，并使整个药品供应链更加高效。

CounterChain 设计用于应对行业中药品的伪造[52]。它连接生产商、运输商、供应商、零售商等，并帮助增加它们之间的信任。它增强了任何时间点的药品可见性。

药品供应链管理和推荐系统是一个非常有趣的框架[53]。不同的用户已经被提供了前端客户端，用于与区块链网络交互和记录交易。客户端应用程序使用超级账本 REST 服务器 composer 与区块链网络通信。通过访问控制规则和智能合约提供了差异化的访问。框架使用数据存储池来离线存储所有交易。这个池子使用人工智能技术进行挖掘，为用户提供关于最合适药品的建议。

## 7.7 结论

区块链是一种基础技术，因为它有潜力彻底改变整个医疗生态系统朝着更好的可持续性发展。虽然它承诺以不同的方式做事情，但它也提供了许多新的事情可以做。它以最有效的方式解决了最痛苦的问题，并提供了信任、透明度和可追溯性。虽然在加密货币和金融领域的使用已被证明是变革性的，但医疗领域尚未见证全面的解决方案。尽管存在许多框架和实验性 PoC，但预计采用将是逐渐的。

在技术前沿存在许多挑战。随着海量数据的增加，存储和速度方面存在问题。最大的优势，即不可变性，也是最大的劣势。在获准或私有区块链中，安全性和操纵性都无法避免。预计新兴和创新的计算技术将改善速度和安全性。然而，仅仅部署基于区块链的技术解决方案还不够，我们需要确保每个利益相关者在网络中的积极参与。这是一个数据驱动的不可变系统，因此数据的正确性和真实性在系统进一步发展和建立可信度方面至关重要。除了解决方案提供者外，监管机构和普通人的角色也非常关键。IEEE SA 积极参与教育和推动医药价值链的新兴技术的采用，IEEE P2418.6 特别涉及医疗保健领域的区块链。

## 参考文献

[1]Taavi, E., 2018, 区块链与医疗保健：爱沙尼亚的经验, 2018, [`e-estonia.com/blockchain-healthcare-estonian-experience/`](https://e-estonia.com/blockchain-healthcare-estonian-experience/) a, b

[2]Satoshi, N., 比特币：一种点对点的电子现金系统, 2008, [`bitcoin.org/bitcoin.pdf`](https://bitcoin.org/bitcoin.pdf) →

[3]Kuo, T.-T., Kim, H.-E., Ohno-Machado, L. (2017). 区块链分布式分类账技术在生物医学和医疗保健应用中的应用。美国医学信息协会杂志, 24(6), 1211–1220. →

[4]Zheng, Z., Xie, S., Dai, H., Chen, X., Wang, H. “区块链技术概述：架构，共识和未来趋势。” 在 2017 年 IEEE 大数据国际大会(BigData Congress), 557–564\. IEEE, 2017. →

[5]Iansiti, M., Lakhani, K.R. (2017). 区块链的真相。哈佛商业评论, 95(1), 118–127。 →

[6]Banerjee, M., Lee, J., Raymond Choo, K.-K. (2018). 互联网安全的区块链未来：立场文件。数字通信与网络, 4(3), 149–160。 →

[7]Dwivedi, A.D., Srivastava, G., Dhar, S., Singh, R. (2019). 一种去中心化的隐私保护医疗物联网区块链。传感器, 19(2), 326。a, b

[8]Morabito, V. (2017). 智能合约和许可。在：通过区块链创新业务，101–124\. Springer。 →

[9]Toshendra, K.S. (2019), 基于区块链的最佳 5 个智能合约平台, [`www.blockchain-council.org/blockchain/best-5-blockchain-based-smart-contract-platforms/`](https://www.blockchain-council.org/blockchain/best-5-blockchain-based-smart-contract-platforms/) →

[10]Ray, P.P., Dash, D., Salah, K., Kumar, N. (2020). 用于基于物联网的医疗保健的区块链：背景，共识，平台和用例。IEEE 系统期刊, 15(1), 85–94, doi: 10.1109/JSYST.2020.2963840。 →

[11]Swan, M. 区块链：新经济的蓝图。” O’Reilly Media, Inc.”, 2015. →

[12]张，李，(2020)。区块链的主要共识协议分析。ICT Express, 6(2), 2020 年 6 月 93–97\. [`reader.elsevier.com/reader/sd/pii/S240595951930164X?token=DB758040A0B8119E1E6EA32C8842746373A104BBCED467E215070674896F893EC1C1AB8224B27F09734E599B10D5594B`](https://reader.elsevier.com/reader/sd/pii/S240595951930164X?token%3DDB758040A0B8119E1E6EA32C8842746373A104BBCED467E215070674896F893EC1C1AB8224B27F09734E599B10D5594B). →

[13]Engelhardt, M.A. (2017). 将医疗挂钩在链上：区块链技术在医疗领域的介绍。Technology Innovation Management Review, 7, 22–34. →

[14]Rawal, V., Mascarenhas, P., Shah, M., Kondaka, S.S. (2017). 白皮书：区块链为医疗业解决许多复杂挑战的机会，普林斯顿，新泽西，美国：CitiusTech。 →

[15]周，安克，Upadhye，麦格格尔，Guarrera，Hegde，等(2013)。电子健康记录互操作性对门诊医师实践的影响：离散事件模拟研究。初级护理信息学, 21, 21–29。 →

[16]Mackey, T.K., 郭, T.T., Gummadi, B., Clauson, K.A., Church, G., Grishin, D., Obbad, K., Barkovich, R., Palombini, M. (2019). ‘适用于什么目的?’ – 区块链技术在未来医疗保健中的应用的挑战和机遇. BMC 医学, 17, 68. →

[17]郭, T.-T., Ohno-Machado., L. "Modelchain: 在私有区块链网络上的分散式隐私保护医疗预测建模框架." arXiv 预印本 arXiv:1802.01746 (2018). →

[18]Azaria, A., Ekblaw, A., Vieira, T., Lippman, A. "Medrec: 使用区块链进行医疗数据访问和权限管理." 在 2016 年第二届国际开放和大数据会议 (OBD), 25–30\. IEEE, 2016. →

[19]范, K., 王, S., 任, Y., 李, H., 杨, Y. (2018). Medblock: 通过区块链实现高效安全的医疗数据共享. 医疗系统杂志, 42(8), 136\. Doi: 10.1007/s10916-018-0993-7. →

[20]江, S., 曹, J., 吴, H., 杨, Y., 马, M., 何, J.: BlocHIE: 一种基于区块链的医疗信息交换平台. 在: IEEE 国际智能计算大会 (SMARTCOMP), 49–56\. IEEE (2018) →

[21]张, P., White, J., Schmidt, D.C., Lenz, G., Rosenbloom, S.T. (2018). FHIRChain: 将区块链应用于安全可扩展地共享临床数据. 计算结构生物技术期刊, 16, 267–278\. Doi: 10.1016/j.csbj.2018.07.004. →

[22]Brodersen, C., Kalis, B., Leong, C., Mitchell, E., Pupo, E., Truscott, A., 区块链: 保护新的健康互操作体验,(2016),[`www.truevaluemetrics.org/DBpdfs/Technology/Blockchain/2-49-accenture_onc_blockchain_challenge_response_august8_final.pdf`](http://www.truevaluemetrics.org/DBpdfs/Technology/Blockchain/2-49-accenture_onc_blockchain_challenge_response_august8_final.pdf) →

[23]Kaur, H., Alam, M.A., Jameel, R., Mourya, A.K., Chang, V. (2018). 云环境中基于区块链的异构医疗数据的提议解决方案和未来方向. 医疗系统杂志, 42, 156. →

[24]Park, J., Park, J. (2017). 区块链安全在云计算中的应用: 应用案例、挑战和解决方案. 对称性, 9(8), 164. →

[25]Miliard, M. (2017 年). 区块链在医疗保健中的潜在用例：炒作还是现实？ 检索自 [`www.healthcareitnews.com/news/blockchains-potential-use-cases-healthcare-hype-or-reality?mkttok=eyJpIjoiTnpBM05XVXlPR0kzWXpZMyIsInQiOiJMYU1TWHZdUVYUCs3SjdKQU9sQURhT3kzY3ZFSFl0Z1dmdmJ6TWMrREdwSXhkZUcrZmRLeWFjNmNtUTAwZGdzT0pYa21KNmcyenVJdlA1VXd1YlB4MGU2RFVzM2F2bzJ5K1BRUjNTRVwvbkVqSVpTYVJpc3ZaVXRoVlwvcjhCNW96In0%3D`](http://www.healthcareitnews.com/news/blockchains-potential-use-cases-healthcare-hype-or-reality?mkttok%3DeyJpIjoiTnpBM05XVXlPR0kzWXpZMyIsInQiOiJMYU1TWHZdUVYUCs3SjdKQU9sQURhT3kzY3ZFSFl0Z1dmdmJ6TWMrREdwSXhkZUcrZmRLeWFjNmNtUTAwZGdzT0pYa21KNmcyenVJdlA1VXd1YlB4MGU2RFVzM2F2bzJ5K1BRUjNTRVwvbkVqSVpTYVJpc3ZaVXRoVlwvcjhCNW96In0%3D) →

[26]Christidis, K., Devetsikiotis, M. (2016 年). 用于物联网的区块链和智能合约。 IEEE Access, 4, 2292-2303. →

[27]Saldamli, G., Reddy, V., Bojja, K.S., Gururaja, M.K., Doddaveerappa, Y., Tawalbeh, L., “利用区块链进行医疗保险欺诈检测”，2020 年第七届软件定义系统国际会议（SDS），法国巴黎，2020 年，145-152，doi: 10.1109/SDS49854.2020.9143900。 →

[28]Gatteschi, V., Lamberti, F., Claudio, D., Víctor, S.: 区块链和智能合约用于保险：技术是否足够成熟？, 2018 年 2 月。 →

[29]Zhou, L., Wang, L., Sun, Y. (2018 年). MIStore: 一种基于区块链的医疗保险存储系统。 Journal of Medical Systems, 42(8), 149. →

[30]Culver, K. (2016 年). 区块链技术：讨论理赔流程如何改进的白皮书。 [`www.healthit.gov/sites/default/files/3-47-whitepaperblockchainforclaims_v10.pdf`](https://www.healthit.gov/sites/default/files/3-47-whitepaperblockchainforclaims_v10.pdf), 2020-08-05. →

[31]Nukala, P.V.S., Pallav, K.B., Sathya, S.M., Phani, K.K. (2018 年 10 月). 区块链技术在整合医疗保险公司和医院方面的应用。 International Journal of Scientific & Engineering Research, 9(10). →

[32]Benchoufi, M., Ravaud, P. (2017 年 12 月 19 日). 区块链技术改善临床研究质量。 Trials, 18(1), 335\. Doi: 10.1186/s13063-017-2035z. [`trialsjournal.biomedcentral.com/articles/10.1186/s13063-017-2035–z`](https://trialsjournal.biomedcentral.com/articles/10.1186/s13063-017-2035%E2%80%93z). a, b, c

[33]George, S.L., Buyse, M. (2015 年). 临床试验中的数据欺诈。 Clinical investigation, 5, 161–173\. Doi: 10.4155/cli.14.116 25729561. →

[34]Romano, C.A., Nair, S., Delphin, E.S. (2018)。 对 2010 年至 2014 年 FDA 发布的警告信和临床调查员检查名单进行临床研究不端行为的回顾性分析。《麻醉与镇痛》，126，976–982。 DOI：10.1213/ANE.0000000000002694 29239950。→

[35]Furlong, E.M.J.R.P., Bull, G.U.J. (2016)。 临床试验招募的障碍及可能的解决方案：一项利益相关者调查，25(2/3)，20–25。→

[36]Huang, G.D., Bull, J., McKee, K.J., Mahon, E., Harper, B., Roberts, J.N. (2018)。 临床试验招募规划：来自临床试验转型倡议的一个提议框架，66，74–79。a，b

[37]Mahon, E., Roberts, J., Furlong, P., Uhlenbrauck, G., Bull, J. (2015)。 临床试验招募的障碍及可能的解决方案：一项利益相关者调查。《应用临床试验》，24。→

[38]Leeza, O. (2019)。 区块链改善临床试验的潜力——Leeza Osipenko 的一篇文章。《英国医学杂志》，367。l5561。 DOI：10.1136/bmj.l5561。（2019 年 10 月 3 日出版）。→

[39]Chan, A.W., Tetzlaff, J.M., Altman, D.G., Dickersin, K., Moher, D. (2013)。 Spirit 2013：临床试验方案内容的新指南。《柳叶刀》，381(9861)，91–92。→

[40]Sandve, G.K., Nekrutenko, A., Taylor, J., Hovig, E. (2013)。 可复现计算研究的十个简单规则。《PLoS 计算生物学》，9(10)，e1003285。→

[41]Irving, G., Holden, J. (2016)。 如何利用区块链时间戳协议改善医学科学的可信度[版本 1；审稿人：2 名批准]。《F1000 Research》，5，222。→

[42]Myles, P.S., Williamson, E., Oakley, J. 等人 (2014)。 对同时进行临床试验的患者招募的伦理和科学考虑。《Trials》，15，470。 DOI：10.1186/1745-6215-15-470。a，b

[43]Zhuang, Y., Sheets, L.R., Shae, Z., Chen, Y.W., Tsai, J.J.P., Shyu, C.R. (2020)。 应用区块链技术增强临床试验招募。《AMIA 年会论文集》，2019，1276–1285。 发表于 2020 年 3 月 4 日。→

[44]Maslove, D.M., Klein, J., Brohman, K., Martin, P. (2018)。 使用区块链技术管理临床试验数据：一项概念验证研究。《JMIR Medical Informatics》，6(4)，e11949。 发表于 2018 年 12 月 21 日 DOI：10.2196/11949。→

[45]Shae, Tsai, J.J.P.，“关于设计用于临床试验和精准医学的区块链平台的研究”，2017 年 IEEE 第 37 届分布式计算系统国际会议（ICDCS），亚特兰大，乔治亚州，2017 年，1972–1980。 DOI：10.1109/ICDCS.2017.61。→

[46]Choudhury, O., Fairoza, N., Sylla, I., Das, A. (2019)。 用于管理和监测多中心临床试验数据的区块链框架。→

[47]Wong, D.R., Bhattacharya, S., Butte, A.J.（2019）。使用区块链在不受信任的环境中运行临床试验的原型。自然通讯，10，917\. Doi：10.1038/s41467-019-08874-y 30796226。 →

[48]Nugent, T., Upton, D., Cimpoesu, M.（2016）。使用区块链智能合约提高临床试验数据透明度。F1000Res，5，2541\. Doi：10.12688/f1000research.9756.1 28357041。 →

[49]Xie, W., Wang, B., Ye, Z., Wu, W., You, J., Zhou, Q. 基于仿真的区块链设计用于保护生物制药供应链。在 2019 年冬季仿真大会（WSC）论文集中，美国马里兰州国家港，2019 年 12 月 8-11 日；797–808 →

[50]Molina, J.C., Delgado, D.T., Tarazona, G. 在药品供应链中使用区块链进行溯源。在 2019 年知识管理组织国际会议论文集中，西班牙萨莫拉，2019 年 7 月 15-18 日；Springer：德国柏林，2019；536–548 →

[51]Kumar, R., Tripathi, R. 通过区块链追踪假药供应链。在 2019 年通信系统与网络国际会议（COMSNETS）论文集中，印度班加罗尔，2019 年 1 月 7-11 日；568–570 →

[52]Chitre, M., Sapkal, S., Adhikari, A., Mulla, S. 使用 Counterchain 监测假药。在 2019 年国际计算、通信和控制（ICAC3）会议论文集中，印度孟买，2019 年 12 月 20-21 日；1–6 →

[53]Abbas, K., Muhammad, A., Ahmed Khan, T., Song, W.-C.（2020）。基于区块链和机器学习的药品供应链管理和推荐系统，智能制药行业。电子学，9，852\. Doi：10.3390/electronics9050852。 →
