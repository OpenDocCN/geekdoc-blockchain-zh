© 作者，由 Springer Nature Switzerland AG 2021 独家授权。R. Kumar 等（编）物联网、人工智能与区块链技术[`doi.org/10.1007/978-3-030-74150-1_13`](https://doi.org/10.1007/978-3-030-74150-1_13)

# 13. 利用大数据分析进行心脏病预测的系统框架

T. Poongodi^(1  ), R. Indrakumari^(1), S. Janarthanan^(1) 和 P. Suresh^(2)(1)加尔各答大学计算科学与工程学院，印度德里-首都圈大学大学，大哥打，印度(2)加尔各答大学机械工程学院，印度德里-首都圈大学，大哥打，印度关键词大数据心脏病预测分析可视化健康医疗数据驱动的 T. Poongodi 博士

现任印度德里-首都圈加尔各答大学计算科学与工程学院的副教授。她获得了来自印度泰米尔纳德邦安纳大学的信息技术（信息与通信工程）博士学位。她是大数据、无线自组网、物联网、网络安全和区块链技术领域的先驱研究者。她在 Springer、Elsevier、Wiley、De-Gruyter、CRC Press 和 IGI Global 等国际期刊、国内外会议以及书籍章节中发表了 50 多篇论文，并在 CRC、IET、Wiley、Springer 和 Apple Academic Press 等出版的书籍中担任了编辑工作。![../images/504166_1_En_13_Chapter/504166_1_En_13_Figa_HTML.jpg](img/504166_1_En_13_Figa_HTML.jpg)

R. Indrakumari 女士

目前在印度德里 NCR 的 Galgotias 大学计算机科学与工程学院担任助理教授。她在曼努曼尼亚姆·苏达拉纳尔大学获得了计算机与信息技术的硕士学位。她的主要研究方向包括大数据、物联网、数据挖掘、数据仓库以及 Tableau 和 QlikView 等可视化工具。她在国内外各种学术会议上发表了 25 多篇论文，并在 Elsevier、Springer、Wiley 和 CRC Press 等出版社贡献了许多书籍章节。![../images/504166_1_En_13_Chapter/504166_1_En_13_Figb_HTML.jpg](img/504166_1_En_13_Figb_HTML.jpg)

S. Janarthanan 先生

目前在印度 Noida 的 Galgotias 大学计算机科学与工程学院担任助理教授。他的专业领域是图像处理和物联网；他正在 Galgotias 大学攻读计算机科学与工程的博士学位，并已完成了计算机科学与工程流的 BE 和 ME 学位。他在工业和学术机构有超过 8 年的经验。他在国际和国内会议、期刊和专利上发表了论文。他成功完成了关于图像分类和对象检测的“人工智能和深度学习”研讨会培训。他还曾在 Smart India Hackathon AICTE 担任导师，并指导学生进行与图像处理相关的各种项目。他曾受邀担任多个组织的网络研讨会资源人、分会主席和主题演讲嘉宾。![../images/504166_1_En_13_Chapter/504166_1_En_13_Figc_HTML.jpg](img/504166_1_En_13_Figc_HTML.jpg)

P. Suresh 博士

2000 年，他在印度马德拉斯大学获得了机械工程学士学位。随后，他分别于 2001 年在印度巴拉蒂亚尔大学和 2014 年在印度安娜大学获得了硕士和博士学位。他在国际会议、期刊和书籍章节上发表了约 45 篇论文。他是 IAENG 国际工程师协会的成员。目前，他在印度德里-全印度工商联合会大学担任教授。![../images/504166_1_En_13_Chapter/504166_1_En_13_Figd_HTML.jpg](img/504166_1_En_13_Figd_HTML.jpg)

## 13.1 介绍

### 13.1.1 大数据

大数据是一个非常庞大的数据集，需要高效的软件进行分析，由于数字存储成本可行且廉价，因此变得非常普遍。美国大约估算出健康数据的数据集数量为 150 艾字节（10¹⁸），在未来几年可能会估算到约 1 千亿亿字节（10²⁴）。大数据包含大量高度复杂、多变的数据，需要先进的技术来捕获、存储、分发、管理和分析信息（术语表，2012）。大数据的主要目标是分析可用的原始数据，以便为决策提供意义并利用其价值。一些大数据的特征如下：体积、多样性、速度、真实性、可变性和价值（Gani 等人，2016），并在图 13.1 中描述：![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig1_HTML.png](img/504166_1_En_13_Fig1_HTML.png)

图 13.1

大数据的特征

+   Volume 指的是社交媒体和应用程序的指数增长，从而导致从各种无限异构源头收集大量的大数据，如 Google、Facebook 内容、Netflix 等。处理这种类型的数据对于进一步的存储和分析来说是非常具有挑战性的。事实上，它指的是数据的大小，例如，千兆字节、拍字节和泽字节（大约是 10¹²、10¹⁵ 和 10²¹ 字节）。

+   Variety 指的是来自不同来源的跨学科数据，例如传感器、企业文档、移动设备、社交网络或卫星图像。这种类型的数据通常以结构化、非结构化和半结构化数据的形式普遍存在。因此，需要适当的工具和技术来分析数据，这也是极具挑战性的，因为存在某些约束条件。

+   Velocity 在分析和流式传输实时数据方面起着重要作用，同时还要考虑速率。来自不同来源的数据，如视频音频、在线交易、地图可视化或社交网络，都被视为分析对象。应该及时利用高效的学习算法提取信息，进行实时数据分析。

+   Veracity 与收集到的大数据的可信度、确定性或准确性有关。因此，它涉及到清理、转换、规范化或过滤等不同阶段的过程，以删除任何噪音信息。如果数据集太大，那么数据清理过程就会变得复杂。

+   Variability 意味着由于数据负载的突然增加而导致数据流中发生的变化的不确定性。

+   Value 是一个重要的方面，它决定了发现的数据是否有意义和适合分析。由于数据集丰富，数据验证也是一项复杂的任务。

医疗大数据分析的整体好处包括改善临床试验、预测疾病、提供适当疗法、检查人口健康、预防疾病、增强护理流程，并通过在正确时间为正确患者提供个性化护理来降低成本（Alexander 和 Wang，2017）。一些大数据分析的用例如图 13.2 所示。![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig2_HTML.png](img/504166_1_En_13_Fig2_HTML.png)

图 13.2

医疗大数据分析的用例

### 13.1.2 心脏疾病

心血管疾病的主要原因是冠状动脉血流在前往心肌的过程中被阻塞或减少，导致血流受阻或减少。人体内的红细胞携带着人类生存所必需的氧气。没有氧气，会导致心肌停止运动，最终导致死亡。智能设备获取并发送关于慢性疾病的数据，提供有关人体心脏、血压或血糖以及呼吸过程的信息，并增加做出适当决定的能力（Bui 等人，2011）。心脏病专家定期收到关于患者的数据，并且有时会提前警告有关心脏问题，以预防心脏疾病。心电图（ECG）是预测心脏疾病的可靠技术，并指导患者进行快速治疗，以减轻任何严重病情的影响。电化学生物传感器可以手术植入人体皮肤下，以便直接接触血流。植入的传感器通过蓝牙传输与肌钙蛋白相关的信息，以实时分析（Poongodi 等人，2020，b，c）。

心血管疾病是全球影响人口众多的健康威胁。通过预测分析，有潜力丰富早期检测、风险评估、症状追踪和准确性。根据麦肯锡报告，美国有 50%的人患有慢性疾病，80%的医疗费用用于治疗。平均每年有 2.7 万亿美元用于慢性疾病治疗，占年度 GDP 的 18%。根据 2015 年中国营养与慢性病报告，86.6%的死亡是由慢性疾病引起的。因此，需要对慢性疾病进行风险评估分析。此外，由于资源和医生短缺，诊断过程非常复杂，这对正确诊断和治疗产生了影响。根据欧洲心脏病学会的报告，2600 万患者被诊断患有慢性心脏病，其中每年有 360 万人。特别是，在最初的 1 到 2 年期间，50%的心脏病患者的病情也会以死亡结束，心脏病管理所产生的费用约占卫生预算的 3%。

心力衰竭是一种疾病，当心脏无法有效地将血液泵送到全身各部分时发生。影响左心室的两种心力衰竭的分类是收缩期和舒张期心力衰竭。收缩期心力衰竭也称为左心室射血分数减少性心力衰竭（HFrEF），是指左心室由于收缩不完全而无法将血液有力地泵送到全身各部分。射血分数（EF）是心室在每次泵血过程中排出的血液量。正常情况下，EF 在 50%到 70%之间，但低于 40%被视为射血分数较低或收缩期心力衰竭。舒张期心力衰竭也称为保留射血分数性心力衰竭（HFpEF），是指左心室在心跳之间不再放松。这种衰竭使心脏组织变得更加僵硬，并且心脏在下一次跳动之前不会充满血液（Bui 等人，2011）。舒张期心力衰竭经常与其他类型的心脏疾病或非心脏疾病（如癌症和肺部疾病）同时发生（Lopez-Sendon，2011）。心力衰竭的情景如图 13.3 所示。![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig3_HTML.png](img/504166_1_En_13_Fig3_HTML.png)

Fig. 13.3

收缩期和舒张期功能障碍

### 13.1.3 心脏疾病的预测分析

医疗大数据在实现各利益相关方的高度利益方面发挥着重要的转型作用。数据分析处理涉及数据获取、预处理、集成、分析、解释和应用算法以生成输出。精确的分析和及时的诊断对于预防心力衰竭并为心脏疾病提供适当的治疗至关重要（Ebenezer & Durga, 2015）。使用传统系统诊断慢性疾病不可靠，无法获得足够的信息来有效诊断。一些心脏病症状是身体虚弱、呼吸急促、脚部肿胀和伴有头晕疲劳，由心脏或非心脏异常引起。医疗数据集中可用的数据极其复杂，因为存在结构不完整的数据（Suguna 等，2017）。结构化数据可以是生活习惯、实验室结果、患者人口统计数据，而非结构化数据包括患者的疾病、病史和问诊记录。识别高风险患者并将其引导至适当的药物治疗是必要的，以减少药物费用，因为他们通常需要昂贵的医疗保健。生物传感器如 EMG、EEG 和 ECG 可用于收集和传输健康参数至服务器进行处理。应确定人体传感器的感知和部署策略，以收集有关心脏患者的数据（Poongodi 等，2020，b，c）。应考虑慢性疾病的生理参数以及隐藏症状进行疾病预测。

电子健康数据的构建使得医疗行业在维护大量信息方面非常强大。各种临床信息来源包括医师录入、临床笔记、影像设备等（Manikantan & Latha，2013）。医疗行业可用的数据集特别庞大且复杂，这些数据也是为了满足监管和政府合规要求而维护的。大量医疗数据固有地难以分割，这导致了对各种与健康相关的问题进行复杂的调查（Fang 等人，2016）。如果患者能够得到精确的医疗治疗，就可以避免医疗服务的不规则性，提高治疗质量，减少副作用。可穿戴设备等医疗设备持续采集数据，高速生成的数据在紧急情况下需要快速处理（Indrakumari 等人，2020）。通过医疗应用程序，用户可以通过服务器向医疗服务提供者发送症状查询。患者可以立即获得关于治疗过程的紧急援助，或者被引导到相关部门进行进一步处理（Panda 等人，2017）。代谢综合征的一些风险因素包括高血压、高血压、低胆固醇、高甘油三酯和胰岛素抵抗，在图 13.4 中有所描述。大数据分析的主要目标是预测代谢综合征的个体和群体水平上的风险因素。![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig4_HTML.png](img/504166_1_En_13_Fig4_HTML.png)

图 13.4

代谢综合征的疾病预测

生物医学信号如心电图和血压是通过移动云计算（MCC）在医疗系统中收集和分析的。健康数据自动与云计算同步进行数据存储和分析（Lo’ai 等，2016）。数字数据在医疗领域呈现出了巨大增长，收集到的数据被有效地探索，以获取来自不同用户的宝贵信息。来自多个来源的大量数据已经被收集，包括传感器网络、流式机器、仪器吞吐量、移动应用等。由于技术不足，存储、处理、可视化和从庞大数据中提取知识变得极为复杂。医疗历史被认为是特别重要的数字副本，尤其是在医疗分析中（Senthil Kumar，2015）。

## 13.2 通过大数据使用数据驱动方法的药物数据

数据驱动方法高度依赖于合成和计算药物化学家来处理不断增加的数据。可以利用潜在资源来在数据驱动过程中获得更高程度的决策（Lusher 等，2013）。以下步骤用于将原始数据转换为更好的决策：

+   确保从内部创建的数据中可以获得的潜在好处。

+   可以整合可用的外部数据资源以进行更好的决策。

### 13.2.1 新科学

数据一旦生成，就会迅速共享，促进知识和当代合作共享（Indrakumari 等人，2019）。 数据驱动方法被启用来管理不断增长的数据，以增强统计分析。 例如，复杂的生物和分析数据集可以与化学实体和公开存在的信息（例如，患者文献）在设计过程中集成。 药物化学家能够识别相关信息，准备原始数据，利用统计工具，获取有意义的信息，解释结果，识别潜在问题，并可视化研究结果以进行有效沟通（Scneiderman 等人，2013）。 通过从数据集中提取数据并将其应用于分类算法以识别结果，可以预测心脏病，如图所示。13.5。![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig5_HTML.png](img/504166_1_En_13_Fig5_HTML.png)

Fig. 13.5

数据集的工作流程

### 13.2.2 药物数据中的大数据挑战

高度可用的内容、组合合成和多样化参数大幅增加了医药化学家相关数据量的大小。即使在当前的计算架构中，处理能力、网络容量或数据存储都不足以管理庞大的医疗数据量。密集型研究或数据驱动的重要目标是在质量或速度方面丰富决策过程。在药物发现中重复的不良实践容易导致糟糕的决策。对半结构化数据进行深入分析需要分析专业知识和更深层次的可视化。在医药化学中，决策依赖于时间和药物设计与评价阶段的适当框架。实验数据被传播给研究人员，以在设计阶段整合新数据，以便提供直观的概览并产生更好的结果。需要直观的知识库和决策支持工具，以便在发现任何新信息时迅速修改计划。关键方面是在不同资源的数据点之间搜索隐藏的模式和相互关联。此外，如果链接暴露出来，那么可以构建复杂的网络来管理它们。可以将公共数据库和相关的生物活动与从不同实验室检索的不同数据源相互关联，这在数据规范化方面带来了挑战（Murdoch & Detsky，2013）。

### 13.2.3 数据驱动方法中的有效决策-making

化学直觉是药物化学家在制定药物设计决策时的关键因素。其他一些因素包括药物化学家的过往经验、对生物靶点（基于配体/基于结构）的了解以及响应反应。配体效率方法，包括亲脂性、焓值和大小依赖性，被认为是支持决策的重要驱动因素，它们平衡了生理化参数以及其功效（Hopkins 等人，2004）。

### 13.2.4 数据简化、可视化和分析

随着数据集的容量和复杂性增加，数据可视化和分析方法引起了人们的极大关注。然而，需要发现一种减少复杂性并以可解释的方式提供交互的方法。一些数据简化方法包括线性回归、贝叶斯方法、层次聚类、K 均值聚类和主成分分析（PCA），这些方法与几种数据分析方法相关，例如聚类分析、预测建模、数据挖掘和决策树。这些直观的方法可以被数据科学家用来在制药公司中可视化结果。计算化学家审查模式和趋势而不是专注于个别化合物。为了在更大的数据集上产生道德感，还可以花费额外的时间来检查信息图表、基于时间的图表以及各种形式的数据表示（Stopler 等人，2014）。

在药物发现过程中，药物化学的巨大能力，特别是内部和外部生成的数据，提高了决策过程。在这个大数据时代的快速增长需要连接所有可用资源，并被视为未来成功的先决条件。此外，数据仓库在维护多样化数据资源方面非常困难。

## 13.3 数据驱动医疗的挑战

医疗学科引入了一些特定领域的问题，以下是所解决的挑战：

+   广泛范围：从个体到大规模，涵盖了各种健康应用。

+   数据复杂性：涵盖了不完整或缺失的数据，大量患者，异构变量以及从多个来源检索的数据。

+   统计严谨性：指的是医疗领域生死攸关的决策。

交互式数据可视化是在医疗生态系统中解决机会和领域特定实践的有效工具（Gotz & Borland，2016）。

### 13.3.1 数据复杂性

可视化在从类似患者仓库检索的数据中支持大量数据以获得洞察力时，本质上是适当的。像柱状图这样的可视化表现良好，无论可用的实体集合如何。可以实施像 Hadoop、BlinkDB 或 Spark 这样的工具来管理在医疗领域快速增长的数据。

### 13.3.2 数据多样性

包括药物、非结构化临床数据、人口统计数据、放射学结果、基因组数据、图像、诊断等医学数据可以考虑用于图 13.6 中显示的诊断。也许，使用各种数据表示形式来可视化数据是极具挑战性的。可视化应使用户能够利用数据集的各种可视化维度来探索变量空间。可视化有效处理各种不同的数据类型，例如分类、数值和分层。![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig6_HTML.png](img/504166_1_En_13_Fig6_HTML.png)

图 13.6

疾病诊断

### 13.3.3 数据质量

医学数据的不确定性，例如医学影像或临床笔记，是一个关键后果。在可视化之前，可以使用图像分析算法和自然语言处理（NLP）分析医学资源，以获得结构化的注释。无效或缺失的数据往往是由于数据的不正确输入或缺乏互操作性。很难区分遗漏或未发生事件之间的差异。大部分医学数据是非结构化的；这些资源需要有效地分析，以便以结构化形式呈现。可视化应突出显示缺陷，并设计成能够有效处理与数据质量相关的问题。

### 13.3.4 统计严谨性

在医疗领域需要专业的可视化工具来确定统计严密性。因此，可视化可帮助用户深入了解或发现在某些角度可能有用的有趣趋势。统计方法存在限制，如缺乏情境化和可解释性。可将来自可视化和统计学学科的最佳实践融合，以满足医疗领域主要需要的高标准验证。获取大规模详细数据可以带来可靠的决策制定。

### 13.3.5 选择偏差

在处理大量医疗数据时，选择偏差起着一定作用。考虑到两种不同的问题，并且将样本与总体之间的差异视为可视化系统的输入，最终导致不具有一般化直觉。例如，在私立医院和公立医院接受治疗的患者可能不同。在选择偏差的背景下，侧重于特定数据集的可视化可能无法获得一般化的结果。因此，必须通过考虑基准样本构建数据集，以确定结果的一般化情况。

## 13.4 大数据分析工具

### 13.4.1 Zoho Analytics

Zoho，一家面向独立业务智能的基于云的业务应用服务提供商，通过仪表板解决方案。它提供本地部署和自动数据融合设施。Zoho 分析支持增强型分析，以生成用户友好的分析报告。网络管理专家 AdvenNet 于 1996 年创立了 Zoho，并将其命名为 Zoho 套件。

### 13.4.2 Cloudera

Cloudera 是一家基于 Apache Hadoop 的解决方案提供商，支持分布式计算和可伸缩存储以及企业能力和基于 Web 的用户界面。Cloudera-Apache Hadoop 的生态系统如图 13.7 所示。Cloudera 的特点包括：

+   可扩展性 – 提供一系列应用程序，并根据需求扩展应用程序。

+   灵活性 – 可以使用各种计算框架处理各种数据，如统计计算、自由文本搜索、机器学习、批处理和交互式 SQL。

+   安全性 – 对敏感数据有良好的控制。

+   集成 – 与所有处理软件和硬件解决方案的 Hadoop 平台兼容。

+   兼容性 – 利用投资和基础设施。

+   高可用性 – 可执行关键信心业务任务。

![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig7_HTML.png](img/504166_1_En_13_Fig7_HTML.png)

图 13.7

Apache Hadoop 开源生态系统 – Cloudera

### Power BI 13.4.3

微软在 2010 年推出了自助商业智能 Power Pivot，该服务的延伸是 Power BI。它是一种用于分析数据并使用与兼容设备功能相对应的 360 度视图可视化见解的工具，具有实时更新功能。Power BI 的一些特点包括：

不受存储位置限制：使用 Power BI，用户可以将数据存储在任何地方，如 Excel 表格、任何数据库管理系统和在线。Power BI 将为用户提供业务关键指标的全面视图。

易于设置：用户可以立即开始工作，因为注册是免费的，用户可以利用简单易用的仪表板（如 Salesforce、Google Analytics 和 Dynamics）立即开始从数据中获取见解。

实时报告：提供交互式仪表板，可以在数据实时更改时自动采用；因此，使用 Power BI 不会有不必要的阻碍。

数据驱动决策：Power BI 为 iOS、Android 和 Windows 提供了触摸启用的本机应用程序。

所有用户可以同时访问：组织的所有成员都可以获得单一视图，这意味着每个利益相关者都可以了解业务进展的当前状态，以便快速决策。

### 13.4.4 Tableau

Tableau 是用于分析数据并以图表和图形形式可视化洞察力的商业智能软件之一。用户可以开发和共享交互式仪表板，显示数据的隐藏模式、趋势、密度和变化。无需编码；用户可以拖放来在一分钟内创建输出的交互式可视化效果。有许多可视化选项可提高用户体验。Tableau 可以轻松处理多行和多列，并创建不同的可视化。医疗大数据分析的其他一些平台列在表 13.1 中。表 13.1

医疗行业的大数据平台

| 序号 | 平台 | 描述 |
| --- | --- | --- |
| 1 | MapReduce | 在集群上的并行分布式算法提供了界面，以分发子任务和收集输出。MapReduce 在执行时跟踪每个节点的过程 |
| 2 | Hadoop 分布式文件系统（HDFS） | 具有容错性和廉价硬件的巨大数据量。它将数据分割成块并将其分发到多个节点 |
| 3 | Hive | 它是使用 SQL 的运行时 Hadoop 架构。这里使用 Hive 查询语言（HQL） |
| 4 | PIG 和 PIG 拉丁 | 处理各种数据结构，如结构化、非结构化和半结构化。这里使用的语言是 Pig Latin |
| 5 | Mahout | 基于 Hadoop 的应用程序为机器学习和支持大数据分析的分布式算法提供解决方案 |
| 6 | Avro | 提供数据序列化过程 |
| 7 | Lucene | 用于文本分析和 JAVA 应用程序内的库搜索 |

## 13.5 案例研究：使用大数据分析进行心脏病预测

### 13.5.1 大数据与人口健康的承诺

保健行业通过记录、患者护理和规律性活动生成大量数据（Raghupathi，2010）。大数据不仅因其规模而受到保健行业的青睐，而且还因其必须以其管理速度和多样性而受到保健行业的青睐（Frost & Sullivan）。与患者福祉和健康相关的整个信息组成了大数据。数据包括临床决策支持决策，其中包括医生的处方、实验室结果、医学影像、医疗索赔政策、药房、某些管理记录和患者的电子记录、传感器数据等。从这些数据中，数据科学家可以找到关联、相关性、潜在模式和异常值。保健领域中的大数据应用探索数据以找到洞察力，从而做出更好和更精确的决策。大数据在以下领域减少了低效和浪费：

+   在临床操作中，分析成本效益方法以检测和治疗患者。

+   基于证据的医学方案分析结构化和非结构化数据，如财务数据、电子医疗记录、基因组数据和临床数据，以预测患者的风险。

+   使用统计算法和工具增强临床设计，以提供更好的治疗，从而减少试验并加快新型治疗的速度。

+   预测建模用于生成更快的药物分发。

+   分析患者记录以增强后续行动。

### 13.5.2 使用可视化方法从患者数据中预测心脏病

心脏病预测分析利用了 Kaggle 数据集。该数据集包括 209 条记录，具有最重要的属性，如年龄、胸痛、血糖、休息血压、心率、休息心电图和胸痛类型。在机器语言中有许多机器学习算法，如 ID3 算法、朴素贝叶斯分类、K 均值和决策树分类算法。心脏病的预测和监测过程在图 13.8 中清晰显示。

图 13.8

心脏病的预测和监测

本研究使用 K 均值算法来预测心脏病。K 均值聚类算法通过将聚类内的平方距离之和最小化来提供低类间相似性和高类内相似性。给定的数据集按照与质心的距离被划分为 K 个簇。质心是通过迭代计算以减小聚类中心与个别点之间的距离而得出的。在本章中，K 均值聚类与数据分析和可视化工具 Tableau 一起使用。K 均值算法属于无监督机器学习算法，它在不参考任何预定义值的情况下给出输出。图 13.9 中的流程图展示了 K 均值聚类算法的工作原理。

图 13.9

K 均值算法的一般工作流程

### 13.5.3 数据集描述

用于定义所提出算法的数据集是 Kaggle 心脏病原始数据集，其中包含 303 名患者记录的 76 个特征。

为了消除数据不一致性带来的误差，数据进行了标准化处理。此分析是基于 209 个样本进行的，独立特征包括年龄、胸痛类型、静息血压、心电图、最大心率和体育锻炼习惯。Kaggle 心脏病数据集的描述在 13.2 表中简要介绍。冠状动脉脂肪条纹是导致心脏病的主要原因，与年龄密切相关。许多研究者指出男性比女性更容易受心脏病影响；这里考虑的数据集是成年男性。表 13.2

Kaggle 心脏病数据集及其特征描述

| 序号 | 特征名称 | 特征代码 | 描述 | 值的范围 |
| --- | --- | --- | --- | --- |
| 1 | 年龄 | 年龄 | 人的年龄 | 28 < 年龄 < 66 |
| 2 | 胸痛类型 | chest_pain | 1\. 非典型心绞痛 | 1 |
| 2\. 典型性心绞痛 | 2 |
| 3\. 无症状 | 3 |
| 4\. 非心绞痛 | 4 |
| 3 | 静息血压 | rest_bpress | Mm Hg | 92 到 200 |
| 4 | 空腹血糖 | blood_sugar | 空腹血糖 >120 mg/dl | t = true |
| f = false |
| 5 | 静息心电图结果 | rest_electro | 1\. 左心室肥厚 |   |
| 2\. 普通 |
| 3\. ST-T 波异常 |
| 6\. 达到的最大心率 | max_heart_rate |   | 82 到 188 |
| 7\. 运动诱发性心绞痛 | exercise_angina | 1\. 是 |   |
| 2\. 否 |

使用 Tableau 可视化工具进行心脏病的预测，并制作仪表板来展示输出。考虑的参数包括年龄、胸痛类型、血糖、静息血压、最大心率、静息心电图和运动性心绞痛。数据集已标准化和预处理。使用 K 均值算法来预测疾病。在这里，讨论了四种类型的心脏疾病，分别是无症状疼痛、非典型性心绞痛、典型性疼痛和非心绞痛。结果是使用所有四种类型的胸痛与其他决定性变量计算出来的。

### 13.5.4 表现指标分析

直方图是一种用于表示一组连续数据出现频率的图表。图 13.10 中的直方图描述了年龄和目标类别心脏疾病风险的分布。![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig10_HTML.png](img/504166_1_En_13_Fig10_HTML.png)

图 13.10

每个目标类别年龄变化的直方图

观察到年龄在 50 至 55 岁范围内的目标类别患心脏病的风险较高，因为冠状动脉脂肪条纹的形成始于这个年龄范围。用于预测心脏疾病的变量是年龄、最大心率、胸痛类型和疾病。这里考虑了四种胸痛类型，并对结果进行了单独讨论。图 13.10 显示了每个目标类别年龄变化的直方图。

图 13.11 显示了患有糖尿病和最大心率的人群的图表。颜色代码代表了结果。从颜色代码可以观察到，患有糖尿病人群被蓝色表示，而红色表示无糖尿病人群。患有糖尿病和可接受心率的目标类别显示出负面症状。![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig11_HTML.png](img/504166_1_En_13_Fig11_HTML.png)

图 13.11

具有最高心率和糖尿病的目标类别

在图 13.12 中，以下图表显示了血压和糖尿病对心脏疾病的影响。可以推断出，糖尿病患者和高血压人群预期会患上心脏疾病。![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig12_HTML.png](img/504166_1_En_13_Fig12_HTML.png)

图 13.12

血压和糖尿病对心脏疾病的影响

图 13.13 展示了用于预测心脏病的用户定义过滤器，它应用在胸痛类型、血压范围和最大心率上。应用在维度类别上的过滤器称为分类过滤器，应用在度量上的过滤器称为定量过滤器。这里胸痛类型是一个分类过滤器，血压和心率属于定量过滤器。用户可以通过滑块来改变测量和类型以预测心脏病。![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig13_HTML.png](img/504166_1_En_13_Fig13_HTML.png)

图 13.13

用户定义的过滤器用于预测心脏病的探索性数据

### 13.5.5 用于临床应用的机器学习训练

人工智能（AI）和机器学习（ML）算法被利用来预测和监测全球范围内的事物，特别是在医疗保健行业。医疗数据由 AI 和 ML 算法整理，从疟疾爆发到心脏疾病都可以进行预测。这种预测对一些缺乏重要医疗基础设施和教育系统的发展中国家有所帮助。这里考虑了 K-means 算法以及数据分析工具 Tableau。图 13.14 展示了机器学习在医疗保健中的应用领域。![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig14_HTML.png](img/504166_1_En_13_Fig14_HTML.png)

图 13.14

医疗保健中的机器学习应用领域

K 均值聚类算法被选择是因为其效率高、简单、能够产生均匀大小的群集，以及在处理 Web 数据集时具有可伸缩性，从而产生准确的输出。K 均值算法有最小的平方和来对数据点的群集进行分类。这里数据集有 7 个变量的 209 个观测值。群集的初始中心通过以下步骤计算得出。

1.  (i)

    确定随机 K 簇。

1.  (ii)

    迭代地找到显著的簇。

1.  (iii)

    如果观察值与其最近簇中心的距离大于其他最近簇中心之间的距离，则通过计算簇和观察值之间的欧几里德距离将该观察值替换为最近中心。

1.  (iv)在簇内，平方和计算为![$$ \sum \limits_K^{k=1}\sum \limits_{i\in {S}_k}\sum \limits_p^{j=1}{\left({x}_{ij}-{\overline{x}}_{kj}\right)}² $$](img/504166_1_En_13_Chapter_TeX_Equ1.png)(13.1)

其中 S[k] 指的是第 *k* 个簇中的观察集合，![$$ {\underset{\_}{x}}_{kj} $$](img/504166_1_En_13_Chapter_TeX_IEq1.png) 指的是第 *k* 个簇的中心的第 *j* 个变量。如果两个连续迭代之间平方和的差异最小，则迭代将停止，并被称为“最终簇中心”。Tableau 中 K 均值聚类的摘要如下详细说明：

+   簇的数量。

+   点数定义了视图的数量。

+   簇间平方和 - 这是一种通过考虑每个簇中心之间的平方距离的和来测量簇之间距离的度量。该值越高，簇之间的分离程度越高。

+   簇内平方和 - 此指标将数据点在簇内的距离表示为每个簇的中心与簇中各个数据之间的平方距离的总和。

+   总平方和 - 它是簇间平方和与簇内平方和的总和。这两个变量之间的比率提供了方差的比例。

方差分析是一种用于查找组平均值差异的统计方法，其中必须有一个因变量和一个或多个自变量。换句话说，ANOVA 可以找出定义的组的平均值是否不同。

F 统计量

F 检验用于确定均值的平等性。F 检验是两个方差的比率，是离散度的一种度量。最大的 F 统计值表示在聚类之间更好地区分。

P 值

当落在特定阈值以下时的概率，然后可以忽略原假设。

模型平方和和自由度（DF）-它是组间平方和与模型自由度的比率。自由度是 k-1 和 N-k，其中 k 是聚类的数量，N 指的是聚类的项数。

误差平方和和自由度

它是组内平方和与误差自由度的比率。误差具有 N-k 个自由度，其中 N 是聚类的总观测数（行数），k 是聚类的数量。

在 Tableau 平台中实现的 K 均值聚类

考虑了四种类型的胸痛，即无症状、非典型性心绞痛、非心绞痛和典型心绞痛，对于每种类型的疼痛，都形成了聚类。根据聚类信息，探索数据集预测心脏病的机会。计算组间和组内平方和。计算 F 统计量和 p 值以准确预测疾病。以下是每种胸痛类型的解释。

1.  （a）

    胸痛类型：无症状

年龄 vs. 最大心率的图表，按疾病分类，显示了无症状胸痛类型的情况，见图 13.15。颜色显示了有关疾病的细节，下面描述了聚类的截图。无症状胸痛类型的聚类细节见表 13.3，无症状胸痛类型的方差分析计算并显示在表 13.4 中。

| 诊断摘要 |
| --- |
| 聚类数 | 2 |
| 点数 | 102 |
| 组间平方和 | 4.7366 |
| 组内平方和 | 5.2604 |
| 总平方和 | 9.997 |

![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig15_HTML.png](img/504166_1_En_13_Fig15_HTML.png)

图 13.15

按疾病分类的年龄 vs. 最大心率图，显示无症状的胸痛类型

表 13.3

胸痛类型：无症状的聚类细节

| 聚类 | 项目数 | 年龄总和 | 最大心率总和 | 疾病 |
| --- | --- | --- | --- | --- |
| 聚类 1 | 49 | 45 | 143.49 | 阳性 |
| 聚类 2 | 53 | 53.679 | 112.43 | 阴性 |

表 13.4

无症状的胸痛类型的方差分析

| 变量 | f-统计量 | P 值 | 模型平方和 | 自由度误差平方和 DF |
| --- | --- | --- | --- | --- |
| 聚类 1 | 55.68 | 3.204 | 3.171 | 1 5.695100 |
| 聚类 2 | 36.4 | 2.732 | 1.566 | 1 4.302100 |

1.  (b)

    胸痛类型：非典型性心绞痛

年龄 vs. 最大心率的图表，按非典型性心绞痛胸痛类型分类显示在图 13.16 中。颜色显示了有关疾病的细节，下面描述了聚类的截图。非典型性心绞痛胸痛类型的聚类细节见表 13.5，非典型性心绞痛胸痛类型的方差分析计算并显示在表 13.6 中。

| 诊断摘要 |
| --- |
| 聚类数 | 2 |
| 点数 | 65 |
| 组间平方和 | 3.6632 |
| 组内平方和 | 4.7261 |
| 总平方和 | 8.3893 |

![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig16_HTML.png](img/504166_1_En_13_Fig16_HTML.png)

图 13.16

按疾病分类的非典型心绞痛胸痛类型的年龄与最大心率

表 13.5

胸痛类型的聚类细节：非典型心绞痛

| 聚类 | 项目数 | 年龄总和 | 最大心率总和 | 疾病 |
| --- | --- | --- | --- | --- |
| 聚类 1 | 36 | 39.139 | 154.72 | 阳性 |
| 聚类 2 | 29 | 53.793 | 136.83 | 阴性 |

表 13.6

胸痛类型的方差分析：非典型心绞痛

| 变量 | F 统计量 | P 值 | 模型平方和 | 自由度误差平方自由度 |
| --- | --- | --- | --- | --- |
| 聚类 1 | 44.22 | 8.121 | 2.984 | 1 4.251100 |
| 聚类 2 | 10.34 | 0.002 | 0.6795 | 1 4.138100 |

1.  (c)

    胸痛类型：非心绞痛

对于非心绞痛胸痛类型按年龄与最大心率的图解如图 13.17 所示。颜色显示有关疾病的细节，聚类的截图如下所述。非心绞痛胸痛类型的聚类细节见表 13.7，非心绞痛胸痛类型的方差分析计算并显示在表 13.8 中。

| 诊断总结 |   |
| --- | --- |
| 聚类数目： | 2 |
| 点数 | 6 |
| 组间平方和 | 1.0374 |
| 组内平方和 | 0.53259 |
| 总平方和 | 1.57 |

![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig17_HTML.png](img/504166_1_En_13_Fig17_HTML.png)

图 13.17

按疾病分类的非心绞痛胸痛类型的年龄与最大心率

表 13.7

胸痛类型的聚类细节：非心绞痛

| 聚类 | 项目数 | 年龄总和 | 最大心率总和 | 疾病 |
| --- | --- | --- | --- | --- |
| 聚类 1 | 16 | 40.12 | 163.56 | 阳性 |
| 聚类 2 | 20 | 54.25 | 133.75 | 负面 |

表 13.8

对非心绞痛胸痛类型方差分析

| 变量 | f-统计量 | P 值 | 模型平方和 | 自由度误差平方 DF |
| --- | --- | --- | --- | --- |
| 聚类 1 | 24.79 | 1.734 | 2.433 | 1 3.313 34 |
| 聚类 2 | 13.31 | 0.0008 | 0.8572 | 1 2.189 34 |

1.  (d)

    胸痛类型：典型心绞痛

以年龄与最大心率为变量，按照典型心绞痛胸痛类型的疾病情况绘制的图示在图 13.18 中描述。颜色显示了有关疾病的详细信息，聚类的屏幕截图如下所述。典型心绞痛胸痛类型的聚类细节在表 13.9 中给出，并且对典型心绞痛胸痛类型的方差分析进行计算并显示在表 13.10 中。

| 诊断总结 |
| --- |
| 聚类数 | 2 |
| 数据点数 | 6 |
| 组间平方和 | 1.0374 |
| 组内平方和 | 0.53259 |
| 总平方和 | 1.57 |

![../images/504166_1_En_13_Chapter/504166_1_En_13_Fig18_HTML.png](img/504166_1_En_13_Fig18_HTML.png)

图 13.18

年龄与最大心率按典型心绞痛胸痛类型分析

表 13.9

胸痛类型：典型心绞痛的聚类细节

| 聚类 | 项目数 | 年龄总和 | 最大心率总和 | 疾病 |
| --- | --- | --- | --- | --- |
| 聚类 1 | 2 | 40.0 | 177.5 | 负面 |
| 聚类 2 | 4 | 49.75 | 145.5 | 正面 |

表 13.10

对典型心绞痛的胸痛类型方差分析

| 变量 | f-统计量 | P 值 | 模型平方和 | 自由度误差平方 DF |
| --- | --- | --- | --- | --- |
| 聚类 1 | 3.35 | 0.1412 | 0.75 | 1 0.8954 4 |
| 聚类 2 | 1.704 | 0.2618 | 0.2874 | 1 0.6746 4 |

从以上聚类中可以推断，年龄、最大心率和胸痛类型在预测心脏疾病方面起着至关重要的作用。

## 13.6 结论和未来展望

该章介绍了在医疗保健背景下的大数据，通过提供信息来说明从大数据的基础到使用探索性数据分析的大数据用例的清晰愿景。对结构化、非结构化和庞大数据的分析已经取得了重大发现。大数据建议使用大量承诺来识别变量之间的非线性和关系。讨论了大数据在医疗保健分析中使用的主要技术和工具。大数据工具可以通过探索来自异构源的数据来预测、预防并推荐最佳的循证治疗方法给患者。在医疗保健领域，使用交互式数据可视化可以获得许多令人兴奋的机会。这将与医疗保健研究人员和从业者形成密切的合作关系，以提供成本低廉的更好诊断和治疗，从而增强患者的预后。一个精心设计的决策支持系统利用机器学习算法将更适合于心脏病的诊断和预测。通过识别最相关的特征，可以提高心脏病诊断系统的性能，并减少计算时间。使用特征选择算法，可以选择最佳特征，从而自动提高准确性并减少执行时间。未来将进行更多的实验，以使用不同的优化技术来提高预测系统的性能。