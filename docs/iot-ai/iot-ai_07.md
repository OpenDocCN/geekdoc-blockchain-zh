© 作者(们)，独家许可给施普林格自然瑞士公司 2021R. Kumar 等人 Internet of Things, Artificial Intelligence and Blockchain Technology[`doi.org/10.1007/978-3-030-74150-1_7`](https://doi.org/10.1007/978-3-030-74150-1_7)

# 7. 巨大的融合 AIoT - 一种一致性还是融合？

G. Ignisha Rajathi^(1  ), R. Johny Elton^(2), R. Vedhapriyavadhana^(3), N. Pooranam^(1) 和 L. R. Priya^(4)(1)印度泰米尔纳德邦科英格拉斯工程技术学院计算机科学与工程系(2)印度泰米尔纳德邦蒂鲁内尔维利 Indsoft Technologies(3)印度泰米尔纳德邦钦奈维特大学计算机科学与工程学院(4)印度泰米尔纳德邦蒂鲁内尔弗朗西斯·泽维尔工程学院电子与通信工程系关键词人工智能物联网融合威胁云计算工业 4.0 预测性维护数据隐私标准化框架治理 G. Ignisha Rajathi

G. Ignisha Rajathi 博士以排名第一的身份在 Chennai 的 Anna University 获得了工程学学士学位和工程硕士学位，专业是计算机科学与工程。她在 Chennai 的 Anna University 信息与通信工程学院完成了博士学位。拥有超过 14 年的教学经验，她目前担任印度科英布雷的斯里克里希纳工程技术学院计算机科学与商业系统系的副教授。她的研究领域包括医学成像、图像处理、软计算。她在期刊上发表了超过 35 篇研究文章，包括高影响力版本和各种会议。她发表了国际和国内专利，书籍和书籍章节。她是她领域的 TCS 认证培训师，并发表了许多邀请演讲和客座讲座，同时参与咨询项目。![../images/504166_1_En_7_Chapter/504166_1_En_7_Figa_HTML.jpg](img/504166_1_En_7_Figa_HTML.jpg)

R. Johny Elton 博士

是一个研究狂热者，对当前技术的详细描述进行科学探索，充满热情。他在 Noorul Islam College of Engineering 获得了工程学学士学位，于 Manonmaniam Sundaranar University 获得了工程硕士学位，并在 Chennai 的 Anna University 获得了博士学位。他的研究兴趣包括自然语言处理、计算机视觉，他在同行评议的期刊上发表了许多研究论文。目前，他正在 Tirunelveli 的 Indsoft Technologies 从事各种创新研究工作。![../images/504166_1_En_7_Chapter/504166_1_En_7_Figb_HTML.jpg](img/504166_1_En_7_Figb_HTML.jpg)

R. Vedhapriyavadhana 博士

2005 年获得阿维纳什林格姆大学生物医学仪器工程学士学位。2009 年获得马诺曼尼亚姆·苏达拉纳尔大学计算机与信息技术硕士学位，2019 年 7 月在安娜大学信息与通信专业完成博士学位。目前，她担任印度泰米尔纳德邦金奈维洛尔工业技术学院计算机科学与工程学院的高级助理教授。她在图像/视频信号处理、无线网络、物联网、深度学习和生物医学仪器领域发表了 30 多篇研究文章。![../images/504166_1_En_7_Chapter/504166_1_En_7_Figc_HTML.jpg](img/504166_1_En_7_Figc_HTML.jpg)

Ms. N. Pooranam

是斯里克里希纳工程技术学院计算机科学与工程系的助理教授，于 2016 年加入。她的主要研究兴趣是人工智能和机器学习。她已发表多项专利、Scopus 文章和期刊论文。![../images/504166_1_En_7_Chapter/504166_1_En_7_Figd_HTML.jpg](img/504166_1_En_7_Figd_HTML.jpg)

Dr. L. R. Priya

2005 年，她从安娜大学获得电气与电子工程学士学位。2007 年，她在卡鲁尼亚大学获得了 VLSI 设计硕士学位，2020 年在安娜大学获得了信息与通信博士学位。目前，她在印度泰米尔纳德邦蒂鲁内利的弗朗西斯·泽维尔工程学院担任电子与通信工程教授。她在网络芯片、4G LTE 和 5G 技术、视频处理和 MEMS 材料等领域的各种期刊上发表/合著了超过 20 篇研究文章和 21 个会议论文。![../images/504166_1_En_7_Chapter/504166_1_En_7_Fige_HTML.jpg](img/504166_1_En_7_Fige_HTML.jpg)

## 7.1 引言

物联网（IoT）和人工智能（AI）在充分利用其卓越实用性方面仍有很长的路要走，这两者的协作听起来像是硬件连接、收集和处理与物联网以及软件连接、收集、处理和行动与人工智能的组合卓越。类似于 20 世纪 90 年代末发生的移动通信和互联网碰撞的伟大融合，物联网和人工智能的结合更加宏伟。

### 7.1.1 人工智能框架

人工智能的重要性在于开发必要的软件和系统，使机器学习和提高以产生更好的结果。它要求在逻辑推理、问题解决和学习或培训方面具有组合能力，并且最重要的是，适应能力是人工智能的一个异常特征（Millet 等，2018）。

随着演变迈向包含人工智能的探索，考虑到适当的人工智能框架和人工智能战略至关重要。首先要从多维概念出发，我们必须专注于人工智能框架，比如基于需求实施的流程、能力的增强、整合我们所需的要求的平台、在所选平台上工作的工具、组织结构以及涉及的利益相关者或参与者。所有这些因素的集合构成了人工智能的框架。在这些最具量化维度下最佳选项的适当选择提供了人工智能的框架。所有这些维度都随着所做的决定向前推进，几乎在所有方面都是如此。例如，正在开发的应用程序的数据存储可以通过校园内或云存储来实现。如果是云服务提供商的情况下，选择哪一个作为备份或主要的，所有这些决定都受到成本效益、时间消耗拥有足够技能的影响，以及能力的增强。此外，第二提供方的选择也必须在所有方面保持开放。进一步的决定涉及使用的工具，比如云供应商提供的工具集或开源工具，以及人工智能团队是来自内部人员组织还是任何外部咨询机构以增加人力资源。可能的流程可以以组织层次人员批准的增强方式实施，与生产过程中涉及的合作伙伴的互动和授予一致，并依靠他们将其作为其端上的页面或利用处于同一领域前沿的新合作伙伴。人工智能各个维度的简单描述如图 7.1 所示。![../images/504166_1_En_7_Chapter/504166_1_En_7_Fig1_HTML.png](img/504166_1_En_7_Fig1_HTML.png)

图 7.1

简单人工智能框架

完整的适当决策集形成了人工智能战略，其主要目标是使用人工智能实现目标结果。这一战略可能是单个结构团队或一组团队的结果决策，但总体上，从框架中建立人工智能战略必须保持整体性。人工智能框架的条款包括 Tensorflow、Microsoft Cognitive Toolkit、Caffe2、Theano torch、Amazon Machine Learning、Accord .Net、Spark MLlib 等。这些框架适用于被分类为反应式机器、有限记忆、心灵理论和自我意识人工智能的任何类型。用于融入人工智能概念的编程语言包括 Python、Java、C++、JavaScript 和 R 编程。对人工智能的远期积极情绪仍然存在黑匣子执行，这导致了为什么会这样的创伤问题，这些问题变得非常具有挑战性，难以解决。

### 7.1.2 物联网框架

物联网的意义正在重新定义工业自动化，将其作为网络的网络（Gubbi 等人，2013）。其精髓在于在所有层面上朝着创新的一致性地平线，无论是在对象功能和行为、应用程序交互性、相应的技术方法还是现实世界和虚拟世界方面。机器对机器（M2M）、人对人（P2P）和人对机器（P2M）阐述了各种类型和规模的连接，包括车辆、智能城市、家用电器、玩具、医疗设备、工业系统等等。

由于物联网是一个全球性的概念，因此它在很多方面都有定义。 IERC 积极参与 ITU-T 13 研究组的工作，该组负责国际电信联盟（ITU）关于下一代网络（NGN）和未来网络的标准制定，并已制定了以下定义：“物联网（IoT）：作为信息社会的全球基础设施，通过连接（物理和虚拟）基于现有和不断发展的可互操作的信息和通信技术的物品，实现先进服务”。

上述展示的几项技术结合了物联网技术以提高其整体效率，如图 7.2 所示。无线射频识别（RFID）是一种主动标签，有 4 种不同类型，例如类 1 标签用于读取或写入存储器，类 2 标签用于使用形式保护数据，类 3 半被动标签与传感器和电池交织在一起，并且类 4 标签用于阐述标签激活并与后端网络建立连接，在定位和传输任何区域存在的数据方面起作用。这些 RFID、条形码、智能手机、传感器、执行器等作为中间件，与异构设备开发交互环境。无线传感器网络（WSN）与传感器设备和 RFID 标签合作、跟踪和通信，控制参数的状态，如温度、噪音、位置、空气污染、湿度、位移、压力、速度、接近度等。为了为传感器设备获得的海量数据建立适当的存储区，焦点转向使用云计算的云存储，这需要本地和现场存储，需要计算和传输能力，以有效地响应对延迟敏感的应用。然而，使用雾计算的本地和云计算服务的结合是另一个巨大的探索性领域。![../images/504166_1_En_7_Chapter/504166_1_En_7_Fig2_HTML.png](img/504166_1_En_7_Fig2_HTML.png)

图 7.2

利用物联网框架的技术

在物联网在宝贵领域的荣耀生存中，物联网面临的挑战依然存在。其中一些挑战包括数据管理挑战，包括存储、传感器分析的数据挖掘，隐私和安全挑战，针对服务提供商的逆向黑客攻击，以及复杂通信中的混乱混乱。此外，数据要素必须能够以直观的方式表示数据，并根据问题解决的分析操作提供推荐的解决方案，这将证明是有效的。

### 7.1.3 章节组织

本章重点讨论了 AIoT 技术面临的挑战。第 7.1 节介绍了物联网和人工智能的概述。第 7.2 节讨论了 AIoT 的演变和不同的代。在第 7.3 节中，讨论了智慧城市、零售业、制药业、石油和天然气行业、隐私和治理以及雅思和 PTE 考试等案例。第 7.4 节汇总了 AIoT 融合中的挑战。在第 7.5 节，列出了未来的趋势和结论。

## 7.2 AIoT 的演变

AIoT 的演变是人工智能（AI）和物联网（IoT）的融合。在洞察了 AI 和 IoT 框架这两项技术之后，AI 和 IoT 的融合不断发展。它已经经历了一代又一代的发展，即使我们称之为初期阶段，还有很多待探索的地方。

### 7.2.1 AIoT 的代

#### 7.2.1.1 第一代

在第一代中，云计算将设备与全天候连接起来。物联网通信建立了具有成本效益的存储，这似乎是遥测数据和处理遥测数据的目的地。它支持设备连接，丰富的存储和非常实惠的计算，使用计算机和存储的驱动程序处理数据。

#### 7.2.1.2 第二代

在第二代中，开始将所有数据流式传输到云中，这降低了延迟并导致数据分流。从隐私方面来看，这是非常危险的。因此，物联网网关被发明用于在本地处理数据，它解决了协议转换（传统掠食），即并非所有数据都会被发送到云端，并且它让客户对数据进行了匿名化。它似乎是云和用户之间的设备。

#### 第三代

在第三代中，通过网关需要更多的计算能力来制定业务逻辑。因此，虚拟机开始支持容器和无服务器函数，因此，云提供商获得了计算能力，例如，亚马逊的 Green grass、微软的容器等等，具有相同的流分析和有效查询逻辑。因此，具有智能计算设备的物联网网关反映了公共云存储、计算和网络。它进一步被积极发展为具有更有效的业务逻辑的雾计算和边缘计算层。

#### 第四代

第四代强化了大数据的价值。手段是大数据，目的是涉及到人工智能。物联网（罗等人，2019）是解决大数据和人工智能问题的用例解决方案。在公共云中有如此多的数据可用，机器学习、深度学习等技术浮出水面，以展示云中数据的价值。它执行了大量的计算、存储、查询答案、群体因果分析、预测等。人工智能非常适合于工业自动化和预测性维护与机器学习。因此，亚马逊的 SageMaker、Azure 机器学习、IBM Watson、Salesforce 推出了 Einstein、Google TensorFlow 等等…应运而生，解决了当时的挑战。

虽然规则引擎在所有通用的物联网网关或云中都起作用，但 AI 部署了一个模型，用于学习和训练以在公共云中运行。它与实时传感器的使用叠加，或者实时收集数据并学习。物联网通过大数据和数据湖利用了人工智能。通过预测性维护，它获得了更多的价值。它不再使用静态规则引擎进行静态编程，而是变得动态起来。在公共云中训练模型，在边缘运行，它将在运行时进行推断；当检测到预测不准确时，它会回到使用前一个数据湖的数据流进行再次训练，并且部署到边缘，并自动运行循环以抑制实际值与预测值之间的漂移。这种 AI 和物联网的封装反映为 AIoT 完全是动态的，用静态规则引擎嵌入到物联网中，反应建模转换为预测性（预测）建模以及分析和维护。简单的 CPU 处理需要加速器。它附加到边缘计算层。作为新一代，英特尔正在运输 Myriad X VPU，NVDI – Jedson，Quadcom 和 Google – 边缘 TPU，并补充 CPU，戴尔正在运输网关和边缘设备，亚马逊等。

### 7.2.2 强力存在中 AIoT 的少数应用

所有下文提到的应用程序都将与其目的、过程、优势以及由 AIoT 嵌入到生产和管理中所面临的挑战进行详细讨论（Katare 等人，2018）：

1.  1.

    智能城市

1.  2.

    零售行业

1.  3.

    制药行业

1.  4.

    石油和天然气行业

1.  5.

    隐私和治理

1.  6.

    雅思和 PTE 考试。

## 7.3 各种应用的案例讨论

### 7.3.1 智能城市

为了建设智慧城市（Parra-Domínguez 等人 2021），这一理念是在城市运作的各个方面，如公共交通、IT 连接、水电供应、卫生、废物管理、电子治理等，注入技术，当需要时，在合适的地方和时间应用人工智能和数据分析。智慧城市（Vermesan & Friess，2013）应该学习、适应、创新，并因此迅速而准确地应对变化的环境。它需要具备灵活性以适应变化。

为此，首要要求是从城市不同部分收集数据。重要的是要确定哪些设施需要改进。为了做到这一点，与市民的关系和与客户的互动起着重要作用。

重要的是了解用户、现实和人们的日常生活，他们面临的挑战以及需要解决的问题，以改善市民的生活条件。标记目标人口的痛点、常见风险和挑战。

建设智慧城市对环境、自然资源、财务上的后果以及其他社会相关性的影响需要进行讨论。

智慧城市不应产生负面影响，而应该在安全、时间、健康、互联性、就业和生活成本等方面带来图 7.3 所示的好处，特别是在环境领域可以实现巨大的改善。![../images/504166_1_En_7_Chapter/504166_1_En_7_Fig3_HTML.png](img/504166_1_En_7_Fig3_HTML.png)

图 7.3

智慧城市的好处

智慧城市不仅是一个技术先进的城市，而且其根本目标是建立一个宜居、愉悦和安全的城市。统计数据显示，到 2050 年，大都市居民数量将轻易突破 65 亿。智慧城市提供了平衡大都市（Thakker 等人，2020）设施数量增加的解决方案，因此它的最佳用途。

大数据、物联网、人工智能以及其他各种即将出现的技术领域需要被探索，以便成功发展智慧城市。物联网是一个关键技术，没有它，智慧城市计划就无法存在，而传感器是物联网系统中每个设备的核心。除了现有的技术方面，还需要评估未来的场景，以获得关于几种可能的、潜在的智慧城市概念的知识。

然而，有一个风险，那就是支持全球标准化的智慧城市发展系统必须分析增加城市腐败的利弊。用于建设智慧城市的资金应该被有效和最优地利用。人们也担心富人和穷人之间的差距可能会增加。智慧城市的建设成本高昂，而提供的设施可能无法为生活在贫困线以下的人们所访问。这与建立智慧城市的目标完全相悖，其目标是创建一个轻松和宜居的环境。

在新加坡，智慧国计划于 2014 年宣布。该计划激励数字创新以支持可持续发展。例如，在公共场所已安装的摄像头的帮助下，可以从监控摄像头拍摄的照片/视频中推断出禁止吸烟区域内的吸烟情况、人群密度、清洁程度、注册车辆的移动情况等。当灾难发生时造成的混乱和困惑，以及人们对威胁的反应也可以预测到。

智慧城市倡议的目标得到了数字经济、数字政府和数字社会的支持。建立智慧城市面临的挑战是收集数据成本高昂。虚拟新加坡是一个在线平台，它使政府能够访问城市的功能。但是，目前投资建设智慧城市可以在未来节省金钱和能源。

在巴塞罗那，智能路灯只有在检测到移动时才会亮起，从而节省了数十亿美元的能源开支。到 2021 年，可以节省 190 亿美元，但首先需要投资 150 亿美元。

智慧城市解决了大都市的问题（Trindade，2017）并创建了更好、更可持续的城市。

通过构建一个生产性的巧妙模型（SmartCities Council, 2018）来创造一个充满活力的环境，通过最新技术来帮助开创新的思维方式。这样做会以积极的方式迅速产生变化，从而导致明确的关联连接。

在印度，智慧城市的理念是将人们从农村地区搬迁到城市地区。印度政府关于智慧城市的倡议主要是关于改造和定期维护，其中 50%的智慧城市将是新建城市，另外 50%将是旧的、现有的城市。问题在于将现有城市转变为智慧城市，因为每个城市都希望尝试奢华和智能化的生活方式。这里存在竞争；每个州都需要提出建议，只有最好的想法才会获得批准。

在规划智慧城市时需要考虑的事项包括人们每天面临的问题和挑战。这包括免费提供的水、节约能源、清洁能源、空气质量等许多基本事项。需要提供一个切实可行的解决方案，不一定要复杂。从简单的事情开始，然后不断改进和建设。

如图 7.4 所示的第一步是构思，涉及头脑风暴，分析可能的替代解决方案，克服挑战，以提供最小可行产品。![../images/504166_1_En_7_Chapter/504166_1_En_7_Fig4_HTML.png](img/504166_1_En_7_Fig4_HTML.png)

图 7.4

智慧城市实施所面临挑战的切实解决方案

产品原型建立后，应进行测试。可以通过征求客户的反馈来进行测试，以检查产品对客户的实用性以及它能够改善客户生活方式的程度。了解人们想要什么使得规划变得更容易，并且他们的批准有助于达到相同的目标。反馈需要返回给构思委员会，以进一步审查结果。

接下来的挑战是资金和支出。城市领导者最关注的是他们如何负担得起智能技术。可能无法重新分配资金用于新项目，并且在市政当局获得新资金批准可能需要数月，甚至数年的时间。

尽管存在这些挑战和障碍，智慧城市议程要求通过采用智能解决方案来提高公民的生活质量，增强和多样化经济，并优先考虑环境可持续性。

### 7.3.2 零售行业

在制造和加工工厂的分销市场中（Mordor Intelligence, 2021; Kimberly Amadeo, 2018），它见证了在金融部门全球范围内的迅速增长，并且始终友好地适应着不断变化的环境。生产者和消费者的投资已经在这家工厂创造了历史，这导致了巨大的向上转变，这在这个充满挑战的环境中被认为是一个积极的迹象。

印度的游客为零售行业做出了很大贡献。在印度，人工智能与物联网在从最高生产，然后通过主要的节点中心分发，再到本地店铺的整个过程中发挥着至关重要的作用，以方便公众使用。

#### 7.3.2.1 印度零售业

随着谷歌、高通、亚马逊和 Facebook 等各种外国公司在印度各个领域增加投资，预计零售市场在对国内生产总值做出公平贡献的过程中将有所增长。从全球范围来看，印度有望在扩大的零售市场中攀升并站稳脚跟。竞争对手在全球范围内提出的需求必须得到满足，因为数字化在无数的营销策略中发挥作用，而在经济中占据顶级巨头之间的立足点又是一种威胁。事实上，这似乎是良性的，因为面对的挑战越多，增长空间的速度就越快。

印度政府正在做出更大的努力，通过最近的各项修改和政策，不仅为生存提供条件，还为所有公民提供清晰和最佳的服务，以在很短时间内使印度成为一个重要的先锋国家。

#### 7.3.2.2 网络零售和疫情期间的零售业

在这场 Covid-19 大流行中，线上零售变得越来越重要。线上零售是增长最快的领域，每年增长 9%。预计到 2030 年，它将达到 1.3 万亿美元。线上零售销售预计将以每年 31% 的速度增长，达到 327 亿美元。预计线上零售产生的收入将在 2020 年达到 600 亿美元。由于关闭了所有的实体店以减少传播，即使一些零售店开业了，但由于社交距离的减少，线下商店的产品消费也减少了。此外，由于今年旅游业的崩溃，一些热门旅游目的地已关闭，这对零售业产生了巨大影响。

#### 7.3.2.3 零售业的未来

这次 Covid-19 改变了消费者行为。由于健康和安全问题，人们开始意识到他们不需要过度购买，更注重只在必需品上花费。这些因素导致其他商品和产品的大量减少。即使在这场大流行危机之外，线上零售（Business World, 2020）也将在未来发挥重要作用。

#### 7.3.2.4 零售业面临的问题

零售销售受到许多因素的影响。其中一些列举如下：

1.  (i)

    *无知*。

创建公司的一个基本要求是拥有富有想象力和创新性的企业家。然而，一旦初始阶段完成，发起人们决定通过以自己独特的步调大步前进来连续成功。但是，缺乏发起人的正确指导和参与会导致大规模销售的失败。为了公司的正常运作，对日常运营的细心维护非常重要。

1.  (ii)

    *灾难*。

灾害，无论是自然的还是人为的，如洪水或火灾，都会给公司带来巨大损失，有时甚至成为公司倒闭的原因。由于避免此类灾难很困难，公司必须至少制定适当的应急计划。此外，公司管理层必须确保公司拥有适当的灾难保险。

1.  (iii)

    *支出*。

高额关税和频繁忽视支出导致了所发现的企业企业的痛苦和崩溃。以下是一些费用：

1.  (a)

    雇佣和服务费

1.  (b)

    进货费

1.  (c)

    服务发票

1.  (d)

    指定损失补偿

1.  (e)

    支付费

1.  (f)

    处理和运输费用

1.  (g)

    维修和保养

1.  (h)

    宣布和进展费用

1.  (i)

    困境处置。

任何企业没有销售就会失败。因此，销售是任何企业的生命线。导致销售不佳的一个不可避免的原因是灾难，但它们不在公司领导层的控制范围内。然而，管理层可以因为许多原因而对销售不佳负责。例如，任何客户喜好的波动都可能导致失败。老板应该始终保持对当前趋势的活跃和接受。

1.  (iv)

    *提前构思*。

许多批发零售店店主在面对公司成熟后再次遭遇灾难时，由于无能或缺乏管理经验而无法胜任。

对于持有者而言，提前非常谨慎地遇到，在创建额外的隔间和扩展解决方案时的构思是责任所在。

另一方面，过度和快速扩张往往会导致企业破产。企业扩张的潜在障碍包括物流挑战、供应问题、融资问题和人员配备问题。尽管没有充分的准备和策略，这些挑战就无法应对。

1.  (v)

    *周期性财务摆动*。

根据市场上关于金融波动的情景转变，大量商业持有者应该提前做好准备，因为这种摇摆以周期性的方式发生。

为了给持有者提供解决方案，应该时刻关注意外的下跌，并在慢速间隔中注意缺陷。

1.  （六）

    *客户复杂性*。

整个过程的关键部分，即客户复杂性，必须在突然撤销购买和赔偿协议时进行监控。这经常发生是因为公司对他们没有完全的控制权。

对上述说法的另一种选择是始终与客户保持良好的联系，提供不间断的反馈，并持续补贴，如果有任何问题从小问题到最重大的争议都由他们提出的话。

1.  （七）

    *个人/财务欺骗*。

关键和有趣的部分是财务欺骗，它可能随时从商业的各个方面出现。它可能会从客户端的底层迅速弹出，也可能是在中途的工人和合作者，或者是从高层管理人员。应该确保在各个点上不发生冲突，以应对遇到的欺骗。

1.  （八）

    *在零售业工作的好处*。

零售营销正在将无法触及的客户带到他们的地方以便容易接纳。零售营销有许多优点，比如电视广告、直邮给消费者、在线广告或优惠券。零售营销对零售商和消费者有不同的好处。商业市场已经发展到零售不再是消费世界中的垄断。过去，顾客只能依靠零售店购买他们所需的产品，但今天，顾客可以从在线商店、拍卖网站、批发店和清仓中心购物，有时甚至可以直接去制造商那里。利用传统零售渠道销售产品仍然有好处。因此，零售仍然有很多优势。

### 7.3.3 制药行业

世界上一个庞大的王朝之一是制药行业中的制药业务，它在当前市场上取得了知名度。

在制药业中，物联网的沉迷真正革命了那些在建立与网络、设备和校外系统之间连接时挣扎的过程，等等。除了解决所有这些因素外，物联网还获得了对实时数据的访问，并消除了操作过程的不透明性。人工智能和区块链的至高无上的力量已经大大改善了供应链及其物流。物联网的潜力肯定非常强大，可以将传感器嵌入智能设备中，这显着提升了制造供应链。

在药品库存中，生产和交付的阶段性干预对于节省大量资金的供应链具有积极的作用。影响制药领域供应链优化的因素（Sharma 等，2020）如图 7.5 所示：![../images/504166_1_En_7_Chapter/504166_1_En_7_Fig5_HTML.png](img/504166_1_En_7_Fig5_HTML.png)

图 7.5

供应链物联网优化

#### 7.3.3.1 制造和运营

产品高品质的保证和生产资产的利用处理了优化的第一个因素。制造一个简单的产品可能是一个复杂的调查过程，往往会削弱活力。因此，人工智能物联网与相关数据合作，揭示引起进程延迟或低效的趋势，可以提前发现并纠正。预防性维护可用于克服这一挑战。

#### 7.3.3.2 库存管理

需要细心的警惕来保持适当的库存和超库存因素之间的稳定。仓库材料必须根据其使用和可见性进行断言，即，人必须知道库存中有哪些材料可用等。因此，人工智能物联网管理智能仓库中材料或产品的效用率和可见性率，以相应地优化运营成本和管理成本。

#### 7.3.3.3 订单管理

将特定的制药公司置于制高点的最重要因素是订单管理。主要的模式依赖于对发布的订单进行透明和可靠的适当管理。配备人工智能物联网的智能制药公司追踪整个交付过程，从下订单到产品到达最终目的地。客户可以舒适地跟踪货物的运输进展，例如实时的当前位置，并且也可以支持性地向客户提供意外延误的信息。与药品运输有关的另一个值得注意的问题是是否存在与保存温度有关的任何约束，例如重要药物。使用这项技术跟踪当前的温度条件。尽管看起来有挑战性，但传感器可能会对监测温度状态产生积极的帮助。

制药业中的 IoT 感知设备不一定是用于扫描条形码的；相反，它们能够准确地将实时数据从一个 IoT 设备传输到另一个同质环境的 IoT 设备，或者传播到网络中。AI 和 IoT 在制药业支持一系列应用，如材料追踪、设备连接以及对温度敏感药物的冷温度监控，从而保证温度稳定。

#### 7.3.3.4 AIoT 的主要优势

1.  1.

    供应链系统效率提高

1.  2.

    制造流程得到了优化。

1.  3.

    操作维护得到简化

1.  4.

    具有仓储的可管理库存

1.  5.

    生产效率总体改善。

#### 7.3.3.5 制药行业的挑战

在**制药行业**人类探险的壮丽技术边缘上，借助 AIoT，整个过程流程的内部和互操作性都在控制之下，以道德步伐继续证明自己具有竞争力，克服了单一包裹的延迟发货，并在各个方面减少了浪费。最重要的是，在市场上及时推出合适的产品，以满足部门人道社会的需求，这意味着区域特定的挑战标准。温度敏感产品的管理，稳定供应药物而不缺货，以及在运输过程中防止贵重药品的盗窃，这是制药行业的可持续发展挑战。

### 7.3.4 石油和天然气行业

全球天然气和石油的需求将从 2017 年的 3736 亿立方米每年增长 1%，预计将于 2035 年达到 4503 亿立方米。统计数据（Ayn de Jesus，2019）预测亚洲是这些资源的最大消费者，占 47%，中东占 16%，美国占 14%。

AI 和 IoT 的结合在这个油气行业中在许多方面极大地改变了整体生产和维护。油气世界中的 IoT 促进了与设备和其他机械的通信，管理、存储数据，并进一步制定安全协议等。此外，AI 与 IoT 在油气行业的结合还对何时进行了适当的回答？这个问题。

图 7.6 描述了涉及 AI 和 IoT 的品牌优势结合的油气行业中涉及的各种利益、应用和技术（Qualetics，2020）。![../images/504166_1_En_7_Chapter/504166_1_En_7_Fig6_HTML.png](img/504166_1_En_7_Fig6_HTML.png)

图 7.6

石油和天然气行业的 AIoT

#### 7.3.4.1 预防性维护

在列出的利益清单中，预防性维护被认为是保持石油和天然气行业最有效运行的重要因素。IoT 启用的 AI 作为 AIoT 以其在实时完美规划中解决主要约束的方式，以清晰的方式解决了主要约束。

能够执行以下两项工作可以极大地提高石油和天然气生产王朝的可持续性：

1.  (i)

    在机器、管道和罐内或外运输的即时发生中识别不正常运行，监控因故障而导致受伤的人员的法定支付和赔偿。

1.  (ii)

    预测或预测该行业所涉及设备的故障或即将磨损。这样可以通过及时修复它们来防止机械的破损，从而节省了数百万的修复成本。

#### 7.3.4.2 AI-IoT 解决方案

有几家供应商公司提供类似以下的 AI 解决方案。

##### SparkCognition 使用以下四个不同的模块

1.  (i)

    DeepNLP、Spark predict、Darwin 和 DeepArmor。

1.  (ii)

    它使用预测性机器学习模型分析实时流传感器捕获的数据，并在任何机器故障时及时发出警报。

1.  (iii)

    一旦警报被激发，人员就会审查并决定何时执行修理过程，无论是按需还是立即更换，或者在完全磨损之前仍然延长。

1.  (iv)

    在这种情况下，如果警报原因似乎已记录，那么此软件会分析、预测并指导采取适当的决策。另一方面，如果它是一个新的原因，系统会根据引起的新特征条件进行培训，并给出原因和影响。

1.  (v)

    它帮助客户提高生产力并降低成本。

1.  (vi)

    它重新构想了工业维护，全面优化资产运营。

##### Softweb Solutions 使用物联网连接系统。

1.  (i)

    它将大量数据转换为实际值，这使得最小干扰具有意义。

1.  (ii)

    它注册批量传感器和设备以加速流程。

1.  (iii)

    它与软件智能和分析（SIA）一起工作。

1.  (iv)

    它通过实时交互报告更新公司人员的当前统计数据，并根据定制训练规则提供适当的建议，这也允许做出实时决策。

1.  (v)

    移动 API 也可用于追踪嵌入到日常石油和天然气生产区域中的 AIoT。

1.  (vi)

    它大大降低了复杂性、相关成本和上市时间。

1.  (vii)

    它支持 AIoT 在智能工厂、资产监控、联网工人、智能建筑、车队管理和零售等不同领域的高效工作能力。

##### Telit 使用物联网解决方案。

1.  (i)

    它嵌入了自然语言处理（NLP）和智能感知无处不在的方法，利用人工智能。

1.  (ii)

    它更多地是一个监控设备特定服务器，它使相关人员对操作服务器中的当前情况保持警惕。

1.  (iii)

    所有数据以单击方式提供，以列表视图和地图视图的形式呈现。

1.  (iv)

    它利用散装液化石油气罐中的传感器收集必要的跟踪信息。

1.  (v)

    所有已安排维护、所有升级、所有故障停机的历史或已解决的问题的清单。

##### 雾号使用闪电边缘智能

1.  (i)

    这是一种基于物联网的石油和天然气行业的前沿解决方案。

1.  (ii)

    延迟导致数据传输到云端进行离线分析，这一挑战被雾号克服了。

1.  (iii)

    它使用机器学习驱动的分析引擎，在实际中心云环境用于存储之前在边缘执行分析。

1.  (iv)

    它协助预测性维护，并向相关人员发出警报，尽管它是一种需培训以理解设备常规运行的指导性分析软件。

1.  (v)

    它降低了故障率、停机时间和成本，增加了客户满意度。

#### 7.3.4.3 石油和天然气行业的挑战

尽管许多技术优势正在进行中，但故障区域仍然是不可避免的，而进一步研究在石油和天然气行业实施无缺区域的动机已有数年历史，并且仍然具有挑战性（V-Soft，2020）。在石油和天然气行业中 AIoT 实施的重要模式的影响如下：

1.  (i)

    对地球层中的碳氢化合物的实际预测

1.  (ii)

    产品的质量保证

1.  (iii)

    主动解决方案的缺陷检测

1.  (iv)

    安全和安全标准

1.  (v)

    成本效益的生产

1.  (vi)

    维护成本的降低

1.  (vii)

    基于分析的适当无缺决策的选择

1.  (viii)

    用于必要辅助的语音或文本聊天机器人。

### 7.3.5 隐私和治理

非人类智能（即 AI）和非侵入式数据收集（即 IoT 设备）对最重要的世俗组织、政府或社会的渗透是同样收敛的，以及一致的（Chelvachandran 等，2020；Atluri 等 2020）。

所有数据内容均通过传感器或任何其他 IoT 设备捕获，以实现其特殊目的。它应该在数据使用和数据保护之间保持适当的平衡，从而隐私、信任和网络安全的问题受到最大程度的重视。数据完整性引发了许多信任问题，引发了社交媒体技术进步的网络空间中的不公正现象。根据政府政策制定者的指导方针，利用积累的数据内容显示出具有生产力的特点，适当的标准化。

#### 7.3.5.1 标准化

标准化（Vermesan & Friess，2013）遵循全球理解的目标，并与权威问题的指导方针以及对因素的治理（例如安全和隐私、技术、社会、法律和政策、全球合作、幸存者的市场竞争、互补产品的互操作性、公共利益等）合作，如图 7.7 所示。![../images/504166_1_En_7_Chapter/504166_1_En_7_Fig7_HTML.png](img/504166_1_En_7_Fig7_HTML.png)

图 7.7

参与标准化的因素

随着 AI 的发展，治理从自动化劳动力的最佳状态转变为技术繁荣。然而，必须针对以下问题验证一个强有力的目的性问题。

1.  （i）

    你能预测分析进展的边界吗？

1.  （ii）

    AI 技术在适当的指导下接受这些限制吗？

1.  （iii）

    建议参与此过程的人员名单，包括持有人、官方当局、公司或工业业务磁铁、供应商等。

1.  （iv）

    在适用的地方必须设置适当的防护栏，以确保完整性。

1.  (v)

    如何平衡数据的使用和保护范围？

数据保护政策、规则和法规必须根据法律法规、成功行业中实践的商业模式、实施隐私政策标准所涉及的风险管理，以及 AI 和物联网在治理中的推论制定。

#### 7.3.5.2 隐私与治理中的挑战

针对重要数据的攻击是恶意黑客的主要打击目标。他们非常容易将企业数据覆盖在公共网络中，并捕获具有战略优势的物联网设备。总的来说，除非采用了可调解或欺骗性的策略，否则黑客或攻击者无法从其目标物联网设备中分散注意力。

在这些社交距离的日子里，头部人员、决策权威通过各种设备进行交流；此外，在泄密高度敏感事项方面遭受了极大威胁。黑客和技术专家攻击者不道德地轻松地突破隐私防火墙，掌握治理策略。对此的恢复是一个持续进行的过程，就像找到一种疾病，发现一种疫苗，然后下一个疾病出现，循环往复。

### 7.3.6 雅思和 PTE 考试

雅思（国际英语语言测试系统）和 PTE（Pearson 语言测试）考试是着名的合格考试，测试一个国家的可用移民的各种技能。考试可以作为人工评估（纸质）（[www.ielts.org](http://www.ielts.org)）或系统评估（计算机评估）（[www.pearsonpte.com](http://www.pearsonpte.com)）进行。

评估考生的标准如下所示，如图 7.8 所示：

1.  (i)

    口语。

1.  (ii)

    阅读。

1.  (iii)

    听力。

1.  (iv)

    写作。

![../images/504166_1_En_7_Chapter/504166_1_En_7_Fig8_HTML.png](img/504166_1_En_7_Fig8_HTML.png)

图 7.8

IELTS 和 PTE 的评估标准

当评估手动进行时，非常透明且顺畅。然而，由计算机系统完成的评估真是一个谜。在内置软件中，它完全抽象为一个黑盒子，嵌入了高级技术强大的人工智能，连接了全槽数据记录的物联网。

在雅思和 PTE 应用软件中使用的基本可预测的软件技术（Nikhil，2017）包括语音识别，它在阅读和口语组合的主要类别中执行语音到文本的转换，根据口语发音、流利度和与文本内容相关的必要关键词。这是考试的关键部分，人工智能发挥着重要的预测作用，这几乎决定了候选人的未来命运。然而，其他部分则直接评估答案，完美地以二进制模式进行评估。

特别是，在 PTE 考试中，有许多任务完全依赖于连接设置的硬件和软件，在这里，听力遵循着与其自己的发音相似的数据复制，这在全球各地各地方都有所不同。同样，阅读、写作和口语部分都与每项任务相互关联，关键性是通过实时人工智能算法精确计算的，最终将候选人的最终得分公布出来。

#### 7.3.6.1 面临的 IELTS 和 PTE 挑战

许多雅思和 PTE 的培训师都指出，与计算机评估的讽刺挑战是无法探索的。 主要的约束在于 PTE，评估的四个主要区域被分成近 20 个任务，这些任务对这 4 个评估区域的贡献是不可预测的，这是基于说话流畅与听力在重述讲座中的相互关联，听讲座并记下要点，以及任务朗读与阅读和说话相互关联等等。 尽管软件的假设是可预测的，但它仍然是许多技术的组合，在具有 AI 核心的情况下，用于评估系统驱动的考试。

这个设置不仅适用于雅思和 PTE，还适用于 COVID-19 大流行引起的当前社交距离，泰米尔纳德邦的教育管理系统，但印度也采用了类似的考试方法论，结合了 AI 和 IoT 的提取效用。

## 7.4 汇总 AIoT 收敛中面临的挑战

总的来说，数据湖和数据流与技术相结合的挑战正在前进，每次解决新问题时，循环就会继续进行。 对于综合 IoT 的未来成功，M2M 服务层标准化，语义互操作性和未来网络标准化有很好的推动力。

AI（Stahl & Wright，2018）几乎已成为我们日常决策的影响因素，根据用户的谱系提出了所有明智的建议。 当信任 AI 预测进行决策时，必须用适当的理由来衡量。 AI 和 IoT 必须是公正的，正如一个公正的人所期望的那样； 然而，人类无法预测他在类似情况下的行为，其中 AI 预测和 IoT 传感器假定了偏见的决策，这导致保守决策的缺陷，未来变得模糊的概念，而 AIoT（Dassault Systemes，2019）也反对人类本性。

这种技术属性在智慧城市、零售行业、石油和天然气行业以及在线考试中的共存，在维护全球的可扩展性方面极具挑战性，涉及到预测性维护、安全性和有效的可操作性。

数据隐私和数据治理（Misuraca & Viscusi，2020）必须非常谨慎处理，因为人工智能和物联网技术的快速扩张，有时会无意中产生错误的概念。这是大规模智能互联网连接对象的组合结果，这些对象被称为云存储、边缘网关或任何其他先进技术的服务和应用。

如今，整个地球都被迫在家办公（WFH），从小学教学一直延伸到讨论任何国家的重要安全秘密。因此，由于 COVID-19（Vaishya 等人，2020），在意想不到的不可避免的领域造成了可怕的风险，涉及到具有人工智能和物联网的技术，包括健康恶化。通信变得简单，而隐私对所有人类都面临着巨大风险。

## 7.5 未来趋势与结论

AIoT 在技术时代中占据着不可动摇的地位，即使个体超级力量 IoT 和 AI 继续在其领域中不断开拓，就其能力而言。IoT 在释放全部潜力和联合系统设备方面起到必要的推动作用。硬件和软件协作的封装引领了 AIoT 的融合。挑战正在成为在这一新兴技术领域中卓越发展的机遇。连接车辆是边缘计算的轮子，具有数以千计的代码，车辆通过 AI 运行，工业设备在边缘计算层中复杂纠缠等等已经通过 AI 和加速器产生了计算方式的显著转变，朝着工业 4.0 的进步前进。IoT 作为数据收集器在巨大蹲位中提供了毫不妥协的足迹，而 AI 则提取有希望的分析洞察力来预测未来。在所有情感智能和逻辑推理方面接受培训后，统计分析预测必须是可以解释的，除非处于安全区域。因此，AI 和 IoT 的日益技术融合成为单一大规模利用的极端平衡和融合。

作为制定有效利用 AIoT 的适当策略的一次尝试，完整的可操作性挑战涉及规格、验证、编程、注释、集成、分析和推理，以及与安全性、兼容性和复杂性、人工愚蠢、缺乏信心、云攻击、技术转移等相关的问题，必须更加慎重地计划和编程，以期在未来的努力中实现人工智能和物联网的卓越融合。
