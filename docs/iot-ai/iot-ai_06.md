© 作者（们），独家授权给 Springer Nature Switzerland AG 2021R. Kumar 等人（主编）《物联网、人工智能和区块链技术》[`doi.org/10.1007/978-3-030-74150-1_6`](https://doi.org/10.1007/978-3-030-74150-1_6)

# 6. 基于物联网的生物医学传感器用于普及和个性化医疗

R. Indrakumari^(1  ), T. Poongodi^(1), D. Sumathi^(2), S. Suganthi^(3) 和 P. Suresh^(4)(1)Galgotias 大学计算科学与工程学院，印度尼泊尔大德里，NCR 大德里，印度(2)VIT-AP 大学计算机科学与工程学院，阿马拉瓦蒂，安得拉邦，印度(3)卡韦里女子学院计算机科学研究生部，泰米尔纳德邦，印度(4)Galgotias 大学机械工程学院，印度尼泊尔大德里，NCR 大德里，印度关键词智能物联网区块链商业模式伦理网络安全法融合技术颠覆性技术新兴技术伦理规范 GDPRMs. R. Indrakumari

担任印度尼泊尔大德里 Galgotias 大学计算科学与工程学院助理教授。她毕业于马诺曼尼亚姆·苏丹纳拉大学计算机与信息技术专业，主要研究领域包括大数据、物联网、数据挖掘、数据仓库及其可视化工具如 Tableau、Qlikview。她在各种国内外会议上发表了 25 多篇论文，并在 Elsevier、Springer、Wiley 和 CRC Press 出版了多篇书籍章节。![../images/504166_1_En_6_Chapter/504166_1_En_6_Figa_HTML.jpg](img/504166_1_En_6_Figa_HTML.jpg)

Dr. T. Poongodi

目前担任印度德里-全国首都区加尔各答大学计算机科学与工程学院副教授。她在印度泰米尔纳德邦安娜大学完成了信息技术（信息与通信工程）的博士学位。她是大数据、无线自组网、物联网、网络安全和区块链技术领域的先驱研究者。她在各种国际期刊、国际/国家会议上发表了 50 多篇论文，以及在斯普林格、爱思维尔、约翰威立、德格鲁伊特、CRC 出版社、IGI global 等书籍中撰写了书籍章节，并在 CRC、IET、约翰威立、斯普林格和 Apple Academic Press 的编辑书籍中做了贡献。![../images/504166_1_En_6_Chapter/504166_1_En_6_Figb_HTML.jpg](img/504166_1_En_6_Figb_HTML.jpg)

D. Sumathi 博士

目前在印度安得拉邦 VIT-AP 大学担任 SCOPE 副教授一级。她于 1994 年获得印度巴拉蒂亚尔大学计算机科学与工程学士学位，2006 年在印度查谟邦 Sathyabama 大学获得计算机科学与工程硕士学位。她在印度安娜大学获得博士学位。她总共有 21 年的工作经验，其中工业界工作 6 年，教学领域工作 15 年。她的研究兴趣包括云计算、网络安全、数据挖掘、自然语言处理和计算机科学的理论基础。她在国际期刊和会议上发表了论文。她组织了许多国际会议，并担任技术主席和教程主讲人。她是 ISTE 的终身会员，在 CRC Press、IGI global、斯普林格、IET、德格鲁伊特、爱思维尔等出版了书籍章节，并在 CRC 泰勒弗朗西斯集团的编辑书籍中做出了贡献。![../images/504166_1_En_6_Chapter/504166_1_En_6_Figc_HTML.jpg](img/504166_1_En_6_Figc_HTML.jpg)

S. Suganthi 女士

是印度泰米尔纳德邦 Tiruchirappalli 的 Cauvery 女子学院（自主）计算机科学的研究学者。她感兴趣的研究领域包括数据挖掘、大数据、区块链技术和物联网。她在 Springer、IET 和 CRC Press 等知名出版社上撰写了许多书籍章节。

Dr. P. Suresh

2000 年在印度马德拉斯大学获得机械工程学士学位。随后，他分别于 2001 年和 2014 年在印度巴拉蒂亚大学和安娜大学获得了硕士和博士学位。他在国际会议、期刊和书籍章节上发表了大约 45 篇论文。他是 IAENG 国际工程师协会的一员。他目前在印度北方邦的 Galgotias 大学担任教授。

## 6.1 简介

医疗健康数字化促进了医疗数据的公开，成为医疗行业革命的原因。政府、私人和公共利益相关者现在通过从不同来源收集数据、预处理数据并存储在一个可搜索和可操作的隔离仓库中，以实现数据透明化。可穿戴设备、医疗应用、无线监测设备、平板电脑和智能手机使医疗服务无处不在。预计连接医疗设备的采用量将在未来几年内急剧增长（Zhang et al.，2014）。这种不断增加的连接设备数量，以及软件和编程语言的支持，正在使医疗行业成为普遍医疗的高效平台。

医疗系统的目标应该通过提供医疗设施，无论用户的位置如何，都能保证对患者的生活质量进行支持，从而为健康的普遍状态的概念铺平道路。传统上，人们遵循基于医院的医疗保健系统（Porter & Heppelmann，2014），但由于患者健康状况恶化，为了节省时间，大多数人更喜欢在家中接受医疗服务。

可穿戴设备（Castillejo 等，2013），物联网（IoT）（Atzori 等，2010），以及智能传感器（Dey 等，2017）通过提供远程监控改善了医疗服务。例如，如果患者患有糖尿病，则葡萄糖监测系统可能会提醒患者按时服药。对于老年人和小儿科患者，它会将警报发送给他们的照料者。在具有智能传感器的物联网中，用户或照料者可以远程获取患者的详细信息，包括他们的饮食、健康问题和与生活方式相关的详细信息。在某些情况下，收集临床数据是不够的，为了真正了解健康详情，数据必须定期进行分析（Wang 等，2018）。通过这种先进的选项，医生可以在没有任何物理出现的情况下持续监控患者。普遍医疗应用的重要作用极大地增强了与健康相关的数据流动性，从而使医疗保健部门前所未有地增加了。

在无处不在的医疗保健系统（JE，2008）中，患者可以自行跟踪他们的医疗记录，并进行基本分析以决定他们需要咨询的医生的专业领域。与数据库结合的先进应用程序与医疗设备相结合，使用户能够通过手持便携设备在任何地方访问数据。本章的主要目标是解释个性化无处不在的医疗传感器和设备的目标，其在医学诊断中的应用以及后续治疗以提高生活质量。本章介绍了无处不在的医疗保健设备的关键组成部分，构想了个性化监测技术、传统医疗保健的挑战、基于物联网的智能医疗保健设备和各种健康传感器。本章的监测路线图如下。第 6.2 节概述了物联网（IoT）和无处不在计算的一般概念。第 6.3 节强调了传统医疗程序面临的挑战。第 6.4 节重点介绍了连接医疗与远程医疗相比的概念。第 6.5 节涵盖了物联网在医疗保健行业中的作用。

## 6.2 移动与无处不在的医疗保健

将医疗部门与物联网相结合，明智地实现了普及系统。普及系统的特性，如适应性、移动性和上下文意识，在正确的时间为相关人员提供正确的数据。普及医疗将医疗系统从治病转变为健康。此外，普及应用程序，如移动性、无线链接和手持设备，允许医疗记录在患者入院之前送达医生。也就是说，当患者前往医院时，他们的机密健康相关信息，如血糖水平、血压、过敏反应和保险详情，可以在患者到达之前发送给医生，医生可以在开始治疗之前进行预防性评估。此外，医生可以在正式场合或家中查看患者记录。

可穿戴设备和基于物联网的健康监测传感器收集患者的健康相关信息，如血氧水平、心率、血糖、体温和血压。RFID 和 GPS 被用来提供基于位置的服务，以便追踪患有精神疾病、残疾以及老年人的人，并定位他们的位置。与健康相关的移动应用程序，如个性化监测、远程医疗、紧急响应和基于上下文的服务，会根据患者目前的健康情况提醒他们按时服药（Doukas & Maglogiannis，2008）。

普遍医疗系统的主要特点是**适应性**。患者的诊断决策源自其背景、位置、社交关系和习惯等上下文信息，这导致了准确的治疗。普遍技术遵循预防胜于治疗的口号，它不仅治疗疾病，还关注未来的健康。普遍技术允许传感器收集的数据融合以研究过去、现在和未来的医疗并发症（Arnrich 等人，2010）。

## 6.3 连接医疗

人类面临着巨大的社会和医疗挑战。人口增加和生活成本是直接相关的，其中包括与健康相关的费用。人们认为应该有新技术来管理他们一生的社会和医疗。Poon 和 Zhang 建议应以普遍、参与和个性化的方式做出预防性、预防性和预测性的医疗决策（Poon 和 Zhang，2008）。有些人尚未接受这个概念，但现在是一个技术革命的世界，创新正在以指数速度发生。现代技术重新构想了医疗部门，以利用技术创新成本效益高、有效的医疗模式（Wilson 和 Cram，2012）。

“连接的健康”一词近年来频繁被使用来协助医疗系统。连接的医疗保健与诸如远程医疗、移动、无线、电子和数字等术语相关联，以服务使用其健康相关数据的人们。与此过程相关的利益相关者通过共享或限制访问与设备连接。这种方法将传统的医疗保健系统转变为一个将利益相关者从他们的住所连接到急性护理环境的积极模式，如图 6.1 所示。![../images/504166_1_En_6_Chapter/504166_1_En_6_Fig1_HTML.png](img/504166_1_En_6_Fig1_HTML.png)

图 6.1

普适医疗保健应用

连接的医疗保健是一种基于物联网传感器的应用，监测远程居住但通过互联网连接的患者。连接的健康方法赋予患者、医疗保健规划者和临床医生在关键接触点访问和获取服务和健康相关信息的能力。连接的健康循环的主要功能是从患者收集与健康相关的数据，因为这些数据被认为是过程的燃料，如图 6.2 所示。获取的数据经过处理并进行标准生物医学调查，以发现或观察症状或行为。连接健康的关键特征是患者可以自行管理其健康详情。![../images/504166_1_En_6_Chapter/504166_1_En_6_Fig2_HTML.png](img/504166_1_En_6_Fig2_HTML.png)

图 6.2

连接健康管理模型

## 6.4 普适医疗保健与远程医疗

普适医疗和远程医疗听起来相似，都涉及远程操作，常常会被混淆，但它们采用不同的方法。远程医疗提供诸如疾病识别和推荐远程地点的后续行动等医疗服务，使用远程通信作为交互介质。在这里，会诊医生远离患者的居住地（Telehealth，Wiki，2020）。普适医疗系统收集健康相关数据，进行分析，并预测疾病。

### 6.4.1 远程医疗

远程医疗是通过远程通信远程实践临床服务的方法。其主要目标是克服偏远地区的距离困难和医生短缺问题。远程医疗方法分为三类（Blanchet，2008）。

存储和转发（Cush，2014）：在这种方法中，患者的医疗数据被发送给医生进行分析。医生和患者不需要同时出现，因此被视为异步处理过程。

远程监测：医生通过预约的远程通信链路实时远程监控患者，在这里，医生可以诊断患者的健康状况，做出决策，并推荐后续程序（ATA，2020）。

实时交互：诸如互联网、视频会议、扫描仪、传真和移动通信等技术是实时交换健康相关文档的主要通信来源。医生会基于 X 光、视频、照片、超声波、病理报告、处方和心电图报告对患者进行分析。远程医疗是一个低成本的过程，填补了医生和患者之间的差距（Merrell，2010）。

### 6.4.2 普适医疗

普适医疗是一种基于物联网的自动监测健康状况的方法。传感器用于感知临床数据，分析准确；因此，普适医疗系统的流行度随着新的应用，如远程老年人护理、健康监测和残疾人护理而增加。物联网医疗系统的组成部分包括互联网、传感器、泛在计算、嵌入式设备和 Wi-Fi 网络（Poongodi 等人，2020a）。生物传感器用于在物联网中收集生理数据，这些传感器通过互联网与数据处理单元连接。生物传感器分为主动或被动类型。主动传感器被注入到患者体内以收集生理数据，而被动传感器则不插入到体内，而是放置在体表上以收集数据（Indrakumari 等人，2020）。

收集的数据经过处理、分析和存储以发现任何异常。物联网传感器不断收集数据，因此，以往的数据可用于预测未来的健康状况。生物传感器和可穿戴医疗设备的流行使得大量医疗应用的开发成为可能（Poongodi 等人，2020b）。用于监测患者的一些常见传感器包括温度传感器、生物电传感器（脑电图、肌电图和心电图）、惯性运动传感器（体态捕捉传感器）和电化学传感器。联网医疗的好处患者参与和护理管理是实时数据、提高治疗结果、对紧急情况做出快速和有意义的反应、更好地照顾远程患者、残疾人的物联网、物联网作为错误减少器、智能药物和降低成本。

## 6.5 传统医疗的挑战

传统医疗面临着诸多挑战，如人口增长、老龄化、不断演变的医疗需求、诊断程序、检测报告分析、临床指南和实践。医疗系统的重大转型对于克服困难、预防错误、提高质量和增强消费者信心至关重要。

+   人口增长：人口过剩会造成不利的健康危害。人口从 1800 年的 10 亿增加到 2020 年的 78 亿。目前，平均人口增长率为每年 8100 万。当人口密集时，疾病很容易以较高的速率传播。由于人与人之间更密切，流行病或大流行病会对密集人口产生不利影响。此外，在发生任何意外事件，如自然灾害或疾病传播时，管理庞大的人口需要适当的医疗保健资金和规划。扩大医疗设施和系统以满足不利情况下人口的惊人增长是各国政府面临的重大挑战。

+   人口老龄化：根据世界卫生组织的报告，人口老龄化的速度正在以非常快的速度增加，60 岁以上的人口预计从 2015 年的 9 亿增加到 2050 年的 20 亿。这意味着世界 60 岁以上人口的比例将从 2015 年的 12%增加到 2050 年的 22%。此外，低收入和中等收入国家将有 80%的老年人口。老年人的生活质量和贡献高度依赖于他们的健康状况。医疗保健行业应该准备满足老年人口的需求，如患者护理、组建人员队伍、推动技术进步以使健康系统与老年人的需求相适应、保险、改变实践和常规，并提供以人为中心和综合的服务。

+   健康需求的演变：随着人们对新技术的认识和现有技术的了解，他们希望参与与医生的讨论，选择他们喜欢的可行治疗方法，并做出与健康相关的决定，因此，满足客户需求的医疗系统至关重要，而具有合格和经过培训的专业人员的医院和诊所是满足这些需求的先决条件。

+   医疗进步所产生的成本：医疗支出的增加主要是由于医疗技术的进步。这包括药物、医疗设备、医疗程序以及对患者进行治疗的支持系统。进步也可以是渐进的，其中改进被附加到已经存在的系统中。这些进步通过降低死亡率有效地提供增值服务，但也产生更多成本。确定投资新技术的水平，以获得有益结果非常繁琐。

+   供应链管理：供应链管理在医疗保健领域是指从制造商获取产品并将其有效、经济地交付给医疗中心的战略规划，这些中心可以是医院、诊所、实验室或医生办公室。这必须在最短的交货时间和更低的成本下完成，以造福患者。医疗产品可以进行库存，并不取决于供求关系。但患者的期望不断变化和医疗保健的监管性质是一个巨大的挑战，需要改变传统系统。此外，必须考虑患者护理的可负担性和质量，以及医疗机构的成本结构。供应链是医疗保健系统或医院面临的巨大支出之一，应该进行良好规划。它不仅涵盖产品成本，还包括诸如税费、关税、保险和物流成本等隐藏成本。因此，数据收集和分析将在供应链管理中产生良好的结果。但不幸的是，在传统系统中，大多数活动都是手工完成的。因此，实施一个能够实时跟踪产品和库存的自动化技术系统将能够提供降低成本的高质量患者护理。

+   数字化转型：与其他行业不同，医疗行业对新技术的适应速度较慢。不断变化的客户期望和个性化的医疗需求需要医疗行业进行数字化转型。此外，医疗数据以指数增长的速度增长，具有不同的数据类型和新技术，必须结合新技术和分析来从数据中获得有意义的见解，从而获得利润并改善对患者的增值服务。接受新变革的恐惧以及在此过程中产生的成本是数字化转型受阻的原因。投资者将寻求对实施任何新系统的投资回报率（ROI）。数据维护、互操作性、不断变化的业务需求、过时的遗留系统、成本以及新技术的复杂性、医疗数据的安全性和隐私性是数字化转型面临的其他主要挑战。

+   透明度：可以定义为向公众提供医疗信息的过程，使其易于理解和可靠，以获取服务质量、成本、患者体验、医疗错误、治理、个人医疗数据以及所有这些数据和信息的沟通。透明度可以改善降低成本、改善医疗护理和提高生产率，确保医疗过程中的所有利益相关者都以平衡的方式受益。医疗价格的透明度可以使客户了解成本，并促使提供者在竞争中降低价格。然而，实现透明度是一个复杂的过程，只有通过在所有涉及患者、提供者和参与过程的利益相关者之间建立合作关系才能实现。此外，应利用标准和政策来促进所有渠道之间的透明度水平。

+   互操作性：在医疗领域，不同设备、信息系统和软件应用之间通过使用数据标准和数据交换模型进行通信和数据交换的能力，有助于为患者提供增值服务。医疗信息交换（HIE）缺乏跨电子健康记录（EHR）的通信标准、集成成本高、HIE 跨患者识别不足以及数据共享不足是互操作性的主要挑战。

+   隐私与安全：医疗数据正在慢慢数字化，因此确保数据安全至关重要。它们经常受到侵犯，必须采取适当的安全措施来确保患者数据的安全和隐私。此外，从这些网络攻击中恢复会产生巨大成本。因此，需要具有适当的集中化数据管理和医疗保健网络安全的标准化协议。

+   支付模式：在传统方法中，通常有三种形式的报销方法，分别如下：在按项目收费（FFS）或基于量的付款中，患者按医生提供的每项服务的相应费用收费。治疗慢性疾病时，患者每次都要单独支付服务费，最终可能会产生巨额费用。这种方法的缺点是，提供者可以不必要地增加服务数量以增加收入。在按人头付费中，提供者在特定时期为一组人提供所有服务。提供者的收入取决于正在接受治疗的人数。在捆绑或基于事件的付款中，提供者估计了在特定问题（例如，心脏手术）上提供的所有服务的预期总成本，并且支付是针对治疗事件进行的。它是 FFS 和按人头支付模式的组合。在 FFS 模式中，患者可能会负担不需要的服务，导致更多的费用支出，而在按人头付费模式中，服务可能会受到影响。因此，患者期望一种增值的报销模式，该模式侧重于以最低费用提供有效的患者护理。医疗保健体系非常复杂，设计正确的支付机制是一项巨大的挑战。

+   医疗保健政策：任何个人采取的医疗保健政策在意外或不利情况下都非常有用，以覆盖即将发生的主要费用。医疗保健政策由政策制定者制定，涉及医疗保障以及与医疗保健相关的成本。政策应该这样制定，以免客户支付过多的金额，并确保他们得到合理的医疗保健服务。挑战在于制定能够平衡所有限制的医疗保健政策。

+   用户接受度：与医疗保健相关的患者、医生和中心对于接受新技术都表现出一定的犹豫。这是因为他们对于使用新系统不太熟悉，对于接受新技术会产生焦虑或不安。因此，说服这一群体的人对医疗行业来说是一个巨大的挑战，而这可能需要根据相关人员的不同而需要不同的时间。

## 6.6 物联网医疗服务

预计物联网将为众多医疗服务提供最有前途的解决方案。通用的物联网协议需要进行微小的修改，以确保不同医疗场景的正常运行。一般来说，这些服务可能包括互联网服务、协议连接、异构设备之间的互操作性、资源共享等。此外，用于提供医疗服务的设备应更加安全、快速、耗能更少，且易于访问。下面将讨论一些医疗服务及其应用的潜在解决方案：

环境辅助生活

对于老年人来说，需要更多专门的物联网服务。利用人工智能和物联网为失能和年迈的人提供医疗解决方案的平台被称为环境辅助生活（AAL）。此外，它帮助老年人更方便、更安全地独立生活。AAL 的主要解决方案在遇到任何严重问题时都使老年人的生活充满信心。所提出的架构旨在通过物联网系统实现适当的通信、安全和自动化（Shahamabadi 等人，2013）。该框架特别介绍了为老年人提供医疗保健服务。利用无线射频识别（RFID）、6LoWPAN 和近场通信（NFC）等各种技术进行主动和被动通信。所设计的框架也可以通过引入针对医疗需求的不同算法来扩展，以诊断老年人面临的问题。

一个通用的 AAL 范式以及物联网智能对象使得各利益相关者之间的闭环服务成为可能，这些利益相关者包括医生、照顾者、家庭成员和老年人。Zhang 和 Zhang（2011）提出了一个面向云计算和物联网的开放、灵活和安全的平台，解决了一些限制，如数据存储、网关安装的可行性、安全性、互操作性和流媒体服务质量（QoS）。此外，还详细调查了基于 AAL 的物联网服务，用于药物控制（Goncalves 等人，2013）。

医疗物联网（M-IoT）

M-健康是关于医疗传感器、移动计算和通信技术用于提供医疗保健服务（Istepanian 等，2004）。在 m-IoT 中，一种新颖的连接模型的特征是连接 6LoWPAN，它演变成提供 m-健康保健服务的 4G 网络。此外，m-IoT 通过其固有特性代表了医疗保健服务与物联网设备之间的连接，这使得实体能够在全球范围内参与。已经研究了利用 m-IoT 服务来感知（非侵入式）葡萄糖水平以及挑战、实施问题和体系结构也得到了解决（Istepanian 等，2011）。M-IoT 生态系统和上下文感知问题是 m-IoT 服务中的重大挑战（Istepanian，2011）。

不良药物反应

不良药物反应（ADR）是指通过摄入药物而发生的一种伤害（ICH 专家工作组，1996）。这种伤害可能是由单一药物的一剂量或多种药物的组合引起的。特别是，它本质上是通用的，意味着它不特定于任何特定的疾病。因此，对于可以处理常见技术问题并提供解决方案（ADR 服务）的设计存在普遍要求。提出了一种基于物联网的 ADR 系统（Jara 等，2010）；在这个系统中，患者的节点可以通过 NFC 或条形码启用的设备检测使用药物。该系统可以与制药智能系统协调工作，以识别药物是否与存储在库中的历史记录兼容（电子健康记录）。iMedPack 采用 RFID 和受控剥离材料（CDM）设计，以解决 ADR 服务（Yang 等，2014）。

社区卫生保健

基于物联网的社区医疗监测关注于像居民区、市立医院、农村社区等本地社区范围内。一种称为社区医疗服务的专门服务是不可避免的，以满足一系列技术要求。提出了一种基于物联网的节能型农村医疗监测系统（Rohokale 等人，2011），并且需要在这个合作网络中加入明确的授权和认证机制。提出了一种社区医疗监测网络（You 等人，2011），它整合了几个无线体域网（WBANs）以提供医疗服务。社区网络的拓扑结构被视为一个“虚拟医院”，它使得远程医疗服务能够被访问。

可穿戴设备

几种无创传感器被开发出来，以向广泛的应用提供不同的健康服务（Chung 等人，2008）。可穿戴设备和医疗设备的异构性与 IoT 框架相适配的适当功能提出了开发者之间的重大挑战。可穿戴设备融入不同 IoT 场景的 WSN 应用的融合被检验了（Castillejo 等人，2013）。提出了一个原型来通过智能手表和智能手机等移动计算设备运行多样化的医疗应用。演示了利用 IoT 框架进行远程监测的可穿戴设备，以及 WBAN 如何通过蓝牙低功耗（BLE）用于可穿戴设备。

## 6.7 基于物联网的智能医疗系统

物联网应用以用户为中心，可以直接被患者和用户使用。如今，诸如可穿戴设备和小工具等医疗设备已经普遍存在，并提供了众多医疗解决方案。世界人口的指数增长对当前可用的医疗服务构成了决定性挑战。

尽管尖端技术和医疗基础设施每天都在改善，但医疗系统仍然面临着几个问题。随着人口老龄化的加剧，对医疗支持的需求巨大，这反过来导致了对医院的不计划的访问。最后，传统方法的有效性丧失了。传统医院系统中总是存在着物理限制；高住院率导致了服务不满意。长期护理需要大量资源来应对人口结构变化的挑战。

[电子健康](https://wiki.example.org/e_health)通过信息和通信技术（ICT）彻底改善了医疗保健服务。存储在存储库中的健康数据可以传输、共享，并应用于任何临床目的。物联网和大数据技术被利用来促进医疗保健利益相关者之间的有效联系。电子健康数据使得能够检查患者的状况，并可以预测其健康状况。在这种“预防性和预测性”医疗模式下，在改善人类健康状况之前采取了重要的措施。

M-健康是指利用多媒体技术和电信技术来传递与健康相关的信息和医疗服务。患者可以通过智能手机获取与治疗依从性和健康意识相关的信息。此外，患者还可以与医务人员进行互动。医务人员可以利用远程智能资源查阅临床指南，获取诊断支持和与客户进行互动。物联网在智能医疗系统中协助远程监测患者，并且能够降低治疗成本和地理障碍。在智能医疗系统中，物联网传感器生成的数据通过物联网网络传输到服务器进行智能分析。通信技术可以根据应用需求进行应用。

智能医疗系统可以根据用户的身体状况为个性化用户提供适当的治疗方案。该系统通过说服技术对患者产生显著影响，其主要目标是改变用户的态度以改善其健康状况。它还促进了预测性维护。例如，传感器可以通过感知患者的心电图信号来识别患者即将发生心脏病发作。智能医疗范式改变了接近方式，患者如何连接和交流，识别和访问新的医疗选择，并分享与健康相关的信息。它警示人们远离各种慢性疾病，而不是接受治疗。持续监控和无处不在的感知是重要特征，对于关键和安全应用程序（如公共安全，医疗保健和辅助生活）至关重要。它编程得如此之好，能够处理许多复杂的医疗案例。智能物联网健康应用机会在表 6.1 中提及。

智能物联网健康应用机会

| 在医院中 | 个人和社区 |
| --- | --- |
| 智能警报系统 | 压力监测 |
| 设备跟踪 | 远程治疗 |
| 行为修改 | 检测与诊断 |
| 预防用药错误 | 远程监测 |
| 实时监测 | 慢性病的自我管理 |
| 检测与诊断 | 行为修改 |
| 适当治疗 | 饮食管理 |

## 6.8 不同的医疗传感器

如今，物联网应用的发展日益增长。由于缺乏诸如意识和基础设施等特定设施，农村地区的人们无法获得适当的健康服务（Ayón，2018）。由于这个原因，与城市地区相比，死亡率较高。此外，随着世界人口的迅速增长，对老年人生命支持的需求增加了（Chaudhary 等人，2018）。为了监测一个人的健康，可穿戴系统可能包含多种类型的传感器，这些传感器可能是微型的、可穿戴的或可植入的。由于诸如人口迅速增长和老龄化等因素，各种医疗设备、部署在这些设备内的传感器以及患者体内的传感器的进展加速，如图 6.3 所示。![../images/504166_1_En_6_Chapter/504166_1_En_6_Fig3_HTML.png](img/504166_1_En_6_Fig3_HTML.png)

图 6.3

部署在医疗应用中的传感器

+   加速度计：该传感器的目标是监测血压和其他用于监测健康的设备。此外，它被用于除颤器、心脏起搏器和监测病人健康状况。

+   温度传感器：可以使用此传感器进行温度监测。它还部署在肾透析机、氧浓缩器、胰岛素泵、麻醉输送机、血压监测仪器和呼吸机中。除了这些仪器，它还植入到数字温度计和器官移植系统中。

+   编码器：安装在医学成像系统、外科机器人、计算机辅助断层扫描仪器和磁共振成像（MRI）机器中。

+   压力传感器：它被植入到各种设备中，如肾透析、呼吸监测、手术液体管理系统和压力驱动的牙科仪器中。

+   流量传感器：电切术、呼吸监测、气体混合和睡眠呼吸暂停机器使用此传感器。通过高频电流，组织被切割，破坏如肿瘤等组织，并导致脱水。

+   图像传感器：眼科手术、人工视网膜、心脏病学、牙科成像、放射学和微创手术是图像传感器的各种应用。

+   SQUID：它用于推断大脑中发生的神经活动。此外，它也作为探测器执行磁图（MEG）和磁心电图（MCG）。

测量参数必须通过有线链接或无线链接传输到集中模式，该模式在用户界面上显示所呈现的信息或将其传输到医疗中心（Pantelopoulos 和 Bourbakis，2010）。

### 6.8.1 医疗护理单位中使用的其他传感器

以小型硬件形式的可穿戴设备涉及一个应用程序，用于跟踪和观察健身指标，如计步、卡路里消耗、睡眠跟踪和心率（Poongodi 等，2020c）。这些设备现今被设计为与计算机或智能手机配合良好，以跟踪长期数据。以下是一些讨论的设备：

+   光电容积描记（PPG）传感器：该传感器背后的原理是光学传感。透过皮肤反射的光被收集以观察静脉内血液的节律。监测血流的目的是分析人体循环和呼吸系统的功能状态。通过从该传感器发出的信号，可以监测某些疾病，如心律失常、自主神经病变、偏头痛、微循环障碍、直立性低血压和周围动脉疾病（Buchs 等，2005; Nasimi 等，1991; Allen 和 Murray，2000; Avnon 等，2003）。

+   脉搏血氧传感器：用于监测患者在心力衰竭、哮喘、肺癌、慢性阻塞性肺疾病（COPD）、贫血和心脏病等多种情况下血液中的氧气含量。手术期间需要测量血液中的氧气含量，以检查肺部药物的作用，验证患者是否需要呼吸机，以及在睡眠期间监测个人的状态。

+   胃肠道传感器：传感器的尺寸微小，用于监测胃肠道的运动。从传感器收集的数据会传输给远程位置的医生，以确定胃肠疾病。此传感器的另一个用途是观察食物摄入量。根据医生提供的建议，肥胖者有必要监测食物摄入量。测量摄入量是一项复杂的任务。因此，借助传感器的帮助，监测食物摄入量变得更加容易。

+   电子皮肤传感器：由于具有可塑性、自愈合和皮肤模拟等特点而受到欢迎，可实现化学、生物生理和机械传感特性。这些传感器被植入以观察脚踝、手指、脉冲信号和喉部感染的运动（Ling et al.，2020；Gong et al.，2015；Jason et al.，2015）。除了监测微小运动外，还可以检测轻微应变和皮肤扭曲。此外，它还用于感知人体运动，如腰盆运动。然而，无法估计人体的微小运动。 （Gong et al.，2015；Jason et al.，2016，Ho et al.，2017）。为了发现和检查脚的压力和手指的运动等身体运动，使用基于纳米材料的电子皮肤（E-Skin）可穿戴传感器。通过在身体中部署此传感器，可以监测腰盆运动（LPM）。这有助于医学专家理解个体的腰背疼痛经历（Zhang et al.，2020）。

+   生物化学传感器：利用基于氧化铪（HfO2）的新型生物传感器，可以早期检测人类白细胞介素（IL）；此外，它还通过电化学阻抗谱技术检测人类抗原来研究抗体沉积。植入电测量的生物传感器利用生化分子识别进行特定识别。

+   荧光生物传感器：该传感器旨在发现药物和癌症。它还感知酶在多个层面上的职责和监测，如基于 GFP 和基于细胞的监测。借助该传感器，及时发现生物标志物可以跟踪疾病的增长和对治疗的反应，进行图像引导手术和体内成像。还确定了关节炎、心血管疾病、转移、炎症性疾病和病毒感染的症状。通过基因编码的 FRET 生物传感器发现了 Bcr-Abl 激酶活性。对癌症患者的细胞进行了活性检查，并与疾病状态进行了关联。生物传感器的几种应用包括微流体阻抗测试，用于调节内皮素诱导的心肌肥大，氧杂烷对固定的果糖转移酶在口腔疾病中的影响，生物芯片，用于快速和准确地发现多种癌症标志物，通过金刚石微针电极进行神经化学研究，以及组蛋白去乙酰化酶（HDAC）抑制剂的共振能量转移测定（Mehrotra，2016）。

+   可摄入传感器：了解的某些信息包括医疗补充剂，现象性变化，食物在胃肠道中的影响，即时健康和疾病。该传感器的独特特点是侵入本能的管状结构，以接触所有胃肠道器官。通过此方法，收集图像并监测管腔液。每个肠段的填充物包括酶、代谢产物、激素、电解质和微生物群落。

### 6.8.2 不同的健身设备

以小型硬件的形式出现的可穿戴设备涉及一种应用程序，用于跟踪和观察健身指标，如计步、消耗卡路里、睡眠跟踪和心率。这些设备如今通常与计算机或智能手机配合使用，以跟踪长期数据。以下讨论了一些设备（Chen 等人，2014）：

1.  (a)

    Fitbit Flex：

    借助加速度计的帮助，跟踪一个人的运动。它记录了人们采取的每一步，以评估其他属性，如燃烧的卡路里、行进距离和运动的极限水平。如果一个人走得精力充沛，那么它将确定这个人是在以‘积极的方式’行走。计步是按分钟计算的。它还确定一个人是在跑步还是在步行。

1.  (b)

    Withings pulse：它用于监测一个人的心率和睡眠时间。此外，它还确定了人的行进距离、计步数和活跃卡路里。

1.  (c)

    Misfit：这是一种用于监测用户活动和活动水平的设备。此设备执行的各种操作包括计步、行进距离、深度睡眠和燃烧的卡路里。

## 6.9 结论

物联网在智能医疗行业中进行了革命性转变。技术的最新进展支持了普及的医疗系统的发展。就这一章而言，讨论了各种生物传感器及其应用。医疗设备相互连接，提供更好的疾病诊断和预测，改善病人体验，及时响应等。物联网在医疗行业发挥着重要作用，是卫生保健行业的助手。使用传感器收集医疗数据，并观察模式以预测疾病。专家和医疗专家利用佩戴式和其他远程设备以最小成本开发了许多基于物联网的应用程序。e 健康监控系统的目标是根据其健康状况为需要的人员提供指导或处方。在没有任何实际互动的情况下，医生可以与患者交流。从临床角度来看，普及医疗系统的进展容纳了许多提供综合护理并填补健康和疾病管理之间差距的先进技术。本章旨在探讨健康和可穿戴传感器在普及和个性化医疗中的应用。本章还讨论了物联网在医疗行业中的作用。本章的最终目标是解释个性化普及医疗传感器和设备的目标，其在医学诊断和后续治疗中的应用，以提高生活质量。考虑到挑战，来自异构来源的数据集成发挥着重要作用。在未来，数据流学习模型、高性能计算和语义网络将发挥关键作用。