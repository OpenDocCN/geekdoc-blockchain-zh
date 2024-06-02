编辑苏迪普·坦沃尔

# 区块链技术用于 5G 启用的物联网

## 工业自动化的新浪潮

第一版 2021![../images/501059_1_En_BookFrontmatter_Figa_HTML.png](img/501059_1_En_BookFrontmatter_Figa_HTML.png)出版商徽标编辑苏迪普·坦沃尔计算机科学与工程系，印度古吉拉特邦艾哈迈达巴德理工学院 ISBN 978-3-030-67489-2 电子 ISBN 978-3-030-67490-8[`doi.org/10.1007/978-3-030-67490-8`](https://doi.org/10.1007/978-3-030-67490-8)©编辑（如适用）和作者，独家许可给 Springer Nature Switzerland AG 2021 版权所有。本出版物受版权保护。出版物的全部或部分内容，特别是翻译、再版、插图的重复使用、朗读、广播、胶片复制或以任何其他物理方式、以及信息存储和检索、电子适应、计算机软件的使用或类似或不同的已知或今后开发的方法，出版商的版权独家授权。本出版物中使用的一般描述性名称、注册名称、商标、服务标志等，并不意味着，即使在没有特别声明的情况下，这些名称在相关保护法律和法规中免于限制，因此可以自由使用。出版商、作者和编辑可以安全地假设本书中的建议和信息在出版日期被认为是真实和准确的。出版商、作者或编辑不就本文中包含的材料或可能存在的任何错误或遗漏给出保证，无论是明示的还是暗示的。出版商在出版的地图和机构隶属方面保持中立。 

本 Springer 印记由注册公司 Springer Nature Switzerland AG 出版

注册公司地址为：瑞士 6330 Cham, Gewerbestrasse 11

序言

物联网通过在全球范围内部署的各种应用中扩展互联网连接，使泛在计算成为现实。 物联网连接数十亿个物体进行高速数据传输，尤其是在 5G-enabled 工业环境中进行信息收集和处理。 大多数问题，如访问控制机制、从不同设备获取数据的时间以及使用的协议，在未来可能不适用，因为这些协议基于集中式机制。 此集中式机制可能存在单点故障以及计算开销。 因此，在各种工业部门需要一种高效的去中心化访问控制机制用于 D2D 通信，例如，不同地区的传感器可以收集和处理数据以做出智能决策。 在这种环境中，安全性和隐私是主要问题，因为大多数解决方案都是基于集中式控制机制的。

为了缓解上述问题，这本编辑过的书包括以下内容：

+   对以 5G 为支撑的物联网作为区块链基础的工业自动化在智慧城市、智能家居、医疗 4.0、智能农业、自动驾驶车辆和供应链管理等应用中的最新提议进行了深入分析。

+   从现有提议中可以看出，区块链可以通过提供细粒度访问控制，彻底改变不同部门当前和未来的大部分工业应用。

+   分析了基于区块链的工业自动化的 5G-enabled IoT 的未解决问题和挑战。 最后，提出了关于各种参数的现有提议的比较，这使最终用户可以根据其在其他方面的优点选择提议。

+   通过案例研究展示了区块链在 5G-enabled IoT 中的采用，使读者了解与此采用相关的未来挑战，特别是智能工业应用。

+   用于基于区块链的工业自动化的 5G-enabled IoT 的分层架构。

该书分为五个部分。 第一部分专注于区块链和 5G-enabled IoT 的背景和基础知识，包括五章。 第二部分讨论了 5G-enabled IoT 的使能技术和架构，包括五章。 第三部分阐述了具有良好结构的 AI 辅助安全的 5G-enabled IoT，包括五章。 第四部分突出了 5G-enabled IoT 的模型、解决方案和标准，包括四章。 最后，最后一部分专注于下一代 5G-enabled IoT 用于工业自动化，包括四章。

第一部分：背景与基础知识

第一章介绍了区块链和 5G 启用的物联网。本章旨在以工业自动化的视角系统地介绍区块链和 5G 启用的物联网。本章还对应用基于区块链的解决方案的不同障碍进行了比较研究。此外，本章旨在阐述和强调区块链在 5G 和物联网中的利用的关键部分。本章还对所选领域的最佳提案进行了内外审查。

第二章旨在指导研究人员和利益相关者改善区块链和 5G 物联网在工业自动化中的整体功能。在章节结束时，作者总结了发现，描述了现有机制的优势和局限性，并提供了可能的研究方向的见解。

第三章介绍了 5G 和区块链技术的基本理念以及它们在各种应用领域中的互补优势和劣势。这些观点得到支持，并且紧接着展示了应用领域的明显吸引力，以便 5G 与区块链的适应性能够开辟新的研究方向，以及为即将到来的通信网络系统带来未来的服务型应用。

第四章介绍了区块链的基本架构和主要特征，以及如何将区块链与 5G 启用的物联网集成。随后，在本章中展示了管理 5G 启用的物联网设备的安全要求。此外，探讨了基于区块链的 5G 启用的物联网的机会、应用、问题与挑战、限制和研究方向，这将有助于研究人员深入了解物联网和区块链领域。

第五章简要介绍了这些新兴技术，它们对工业自动化的影响以及它们在不同行业中的应用。本章分为六个主要部分，即介绍、工业自动化的兴起、物联网、5G 无线网络的出现、区块链技术；下一个大事、以及金融领域中区块链和 5G 启用的物联网用例。

第 II 部分：为 5G 启用的物联网提供支持的技术和架构

第六章概述了关键的启用技术，如云计算、异构网络（HetNet）、设备对设备（D2D）通信和软件定义网络（SDN），这些技术已成为实现任何工业自动化应用更高效的关键技术。此外，在本章中，还审视了物联网应用需求及相关蜂窝通信技术的现状。然后，与新兴物联网应用一起呈现了各种通信技术的比较分析。在本章末尾，讨论了基于 5G 的物联网的案例研究，以及部署各种物联网服务和应用的挑战和未来研究趋势。

第七章通过将基于 5G 的物联网系统与云生态系统集成，阐明了 5G 使能物联网系统的好处。然后，提供了一个案例研究，反映了利用云生态系统为 5G 基础的物联网基础设施实现有效决策过程和处理物联网框架中的安全性的好处。

第八章分析了用于工业自动化的基于 5G 的物联网网络的前景，并探讨了它们在现代应用和技术中所需的技术软件能力。此外，本章还检验了将基于 5G 的物联网网络集成到工业自动化领域中的架构、其中使用的现有技术以及区块链技术在确保这些技术的安全性和可靠性方面发挥的关键作用。此外，还讨论了用于解决资源分配问题的解决方案的优化方法，并突出了区块链技术的重要性。

第九章讨论了两种技术标准化将出现的问题。在众多可能的替代方案中，本章讨论了在 5G IoT 领域解决所有这些问题的区块链的使用。从本章开始，最终用户将从 5G 的功能中受益，随后是区块链与物联网应用的融合。最后，本章讨论了基于 5G 的物联网应用架构及其特点。

第十章提出了智能数据分析和移动计算辅助医疗系统开发的详细设计。提出的先进的股权证明（PoS）共识算法比其他现有算法具有更好的性能。此外，在本章中，作者设计了一个 eHealth 程序，部署了三层患者代理软件的多个实例：感知、近距离处理和远程处理层。还定义了如何在 5G 单位上实现患者代理。

第三部分：AI 辅助安全的基于 5G 的物联网

第十一章讨论了有关云计算和边缘标准、5G 网络的安全基础知识以及其他安全措施的重要事实。然后，讨论了 5G 可启用的物联网架构、5G 可启用的物联网中的安全威胁、安全分析、5G 可启用的物联网中的隐私威胁、特定领域中的安全和隐私威胁以及挑战和机遇。此外，本章还讨论了包含五个层次的 5G 可启用的物联网：识别层、连接/边缘计算层、支持层、应用层和业务层。审查了涉及边缘范式领域的 5G 可启用的物联网的安全和隐私策略的挑战。

第十二章提供了一种详细的数据加密和方案方法，使得黑客难以解密数据。随后，本章讨论了一些案例研究，以更好地理解 5G 可启用的物联网网络中的数据安全和隐私。本章帮助读者了解数据如何被盗用，并在相应的研究领域提供解决方案。

第十三章概述了用于 IoT 可启用的 5G 网络的对抗性 AI 技术，用于自动检测和分类威胁，并使用区块链实现安全交易。然后，本章讨论了有助于理解交通方向和道路信号识别的实时攻击的案例研究。最后，本章讨论了如何检查工业部署的自动化系统以及它们如何防止系统受到攻击并保护数据。

第十四章着重介绍了物联网平台、机器学习与物联网平台的融合、数据挖掘与物联网平台的融合以及大数据分析与物联网平台的融合。这个概念包括机器学习如何提高 5G 网络的效率，数据挖掘如何为 5G 网络提供数据，以及大数据分析如何减少 5G 网络的时间消耗。本章介绍了两个案例研究，将通过这些革命性技术更深入地了解 5G 网络的机制。第一个案例研究是关于智能城市的，在其中强调了 5G 网络的作用，第二个案例研究是关于移动网络的，其中详细阐述了移动社交网络 (MSN) 的概念。本章是一套完整的信息，让用户探索新事物以及技术如何每秒都在进步，以及人类如何适应变化以在世界上生存。

第十五章利用基于区块链的智能合约开发了一个受保护的健康信息（PHI）系统，以协助安全数据分析、数据共享、数据传输和管理，以处理智能远程康复应用程序的安全健康信息。这个名为自闭症远程康复应用程序（ATA）的应用程序使用基于以太坊协议的私有区块链来记录所有患者的电子健康记录（EHRs）的历史和记录。此外，这个 ATA 将通过向患者和医疗专家发送警报来提供医疗干预和实时患者观察。此外，它可以安全地记录谁发起了这些活动。这个提议的带有 ATA 的区块链为所有利益相关者提供了高数据安全性。

第四部分：5G 启用的物联网模型、解决方案和标准

第十六章提出了一种基于区块链辅助的应用系统，由云环境支持，用于为老年人医疗保健系统提供方便、适应性强和高效的平台，以解决老年人的医疗保健问题。此外，提出了一个旨在为用户提供必要医疗服务的架构，具有处方、饮食计划和来自医生端的药物摄入详情等功能。本章展示了如何通过扫描患者的 Aadhar 上的 QR 码将患者的记录添加到数据库中，患者之前拜访不同医生的医疗历史以及在这些拜访中观察到的症状。给定的处方将被良好地维护，并且通过简单地扫描 Aadhaar 上的 QR 码，任何医生或患者都可以轻松地查阅以供将来参考。

第十七章简要介绍了技术（区块链、物联网、边缘计算）的背景，并探讨了深度学习技术在即将到来的技术（未来一代蜂窝网络、物联网和边缘计算）中的资源管理。然后，本章讨论了当前深度学习技术在将深度学习与区块链高效部署到即将出现的新兴技术中的潜力。本章对深度学习技术进行了百科全书式的回顾，并通过指出当前的研究挑战和未来研究方向来总结分析。

第十八章简要介绍了 5G 启用的物联网对行业和工业自动化的影响。在过去的几年里，工业增长势头迅猛，但本章仅包括那些预计在 5G 的出现及其与物联网的整合后将经历重大革命的类别。预计 5G 启用的物联网将使医疗保健更加先进，使可用的自动驾驶车辆更接近现实，并将许多典型的工业产品和系统演变为智能版本，如智能家居、智能城市、智能农业、智能供应链管理等。本章对所有提及的变化进行了简要讨论。

第十九章提出了一个去中心化应用，利用智能合约借助区块链技术促进文档的认证和验证。与传统的存储整个输入数字文档的方式相比，所提出的方法通过使用加密哈希函数为每个输入文档创建一个唯一的指纹。这个指纹被存储在区块链网络上，以便将来验证文档。这种基于区块链的解决方案可以被组织用来验证他们生成的文件，并允许其他实体对其进行验证。

第五部分：面向工业自动化的下一代 5G 启用物联网

第二十章涵盖了基于 5G 技术的医疗保健应用。它提出了医疗领域的新挑战和技术。本章还提出了一个基于 5G 网络的可穿戴生物技术平台，以展示生物信息方法和生物感知平台。本章还讨论了医疗系统环境的相对比较，如用户环境、生物信息收集类型和方法等。

第二十一章对策划的调查论文进行了比较分析，具体参数用于理解主题覆盖范围并发现研究间隙。然后，重点突出研究问题、实施挑战和未来趋势。本章提供了一个世界一流的工具制造公司的案例研究，并以物联网应用的整体视角结尾。

第二十二章讨论了临床医生通过实时监测患者状况以及患者通过高速 5G 网络和使用区块链和物联网提供的增强服务分享医疗记录的情况。该技术被接受的主要问题是在与第三方分享数据或通过匿名标识符间接识别用户时的数据滥用。这项研究着重于为现有患者和普通用户使用技术，并改进医疗行业的服务。

第二十三章讨论了最新移动和卫星通信的重大发展；具有高隔离度和低互耦合的多频率天线尤其引人关注。此外，低交叉极化、高增益和最大前后比的天线被获取，并且讨论了它们在 5G 启用的物联网应用中的使用。

编辑非常感谢斯普林格的所有成员，特别是玛丽·詹姆斯女士和阿尼达·博斯先生，给予编辑本书的机会。

苏迪普·坦瓦尔，印度古吉拉特邦艾哈迈达巴德内容第 I 部分背景和准备 11 区块链和 5G 启用的物联网：背景和准备 3 施韦塔·考希克 2 区块链驱动的 5G 物联网启用工业自动化的背景和研究挑战 33U. 哈里哈兰和 K. 拉吉库玛 3 区块链技术与 5G 的融合：一个对称的开始 61 苏尼塔·萨特帕西、萨特亚松德拉·马哈帕特拉和阿努帕姆·辛格 4 区块链和 5G 启用的物联网设备介绍 83 希万吉·苏拉蒂、贝拉·希米和希伦·帕特尔 5 5G、物联网和区块链技术在工业自动化中的影响 107 埃曼·谢赫和纳齐鲁丁·穆罕默德第 II 部分 5G 启用的物联网的使能技术和架构 1316 新兴通信技术用于 5G 启用的物联网应用 133 马拉拉姆·库姆哈尔和吉滕德拉·巴蒂亚 7 5G 启用的物联网的先进云数据分析 161 维韦克·库马尔·普拉萨德、苏迪普·坦瓦尔和马杜里·D. 巴夫萨尔 8 工业自动化中 5G 启用的物联网的现有技术和解决方案 183 哈利姆贾·库贾马托夫、杜斯顿·卡萨诺夫、埃尔纳扎尔·雷普纳扎罗夫和努尔肖德·阿赫迈多夫 9 5G 启用的物联网的使能技术和架构 225 帕尔文·莫尔和沙琳·巴斯卡尔·巴贾 10 5G 启用的物联网医疗保健的大数据分析 263A. 西瓦桑加里、L. 拉克什马南、P. 阿吉萨、D. 迪帕和 J. 贾贝兹第 III 部分 AI 辅助安全的 5G 启用的物联网 27911 5G 启用的物联网中的数据安全和隐私 281 达潘·阿南德和维尼塔·凯姆钦达尼 12 5G 启用的物联网的安全与隐私：数据分析视角 305S. R. 马尼·塞卡尔、G. 尼迪·巴特、S. 瓦什纳维和 G. M. 西德 13 安全的 5G 启用的物联网的对抗性人工智能协助 325 莫罕默德·侯赛因·博哈拉、库西·帕特尔、阿图法利·赛耶德和阿米特·甘纳特拉 14 用于 5G 启用的物联网的机器学习、数据挖掘和大数据分析 353 普内特·库马尔·阿加尔瓦尔、帕丽塔·贾因、贾雅·梅赫塔、丽娅·加尔格、Kshirja·马卡尔和普尔维·乔德哈里 15 使用区块链系统的个性化自闭症家庭干预的智能安全远程康复应用 379Nurnadiah·Zamri、Zarina·Mohamad、Wan·Nor·Shuhadah·Nik 和 Aznida·Hayati·Zakaria·Mohamad 第 IV 部分 5G 启用的物联网模型、解决方案和标准 40116 混合区块链安全的老年医疗保健环境 403 艾什瓦里亚·古普塔、普杰·卡纳和萨钦·库马尔 17 区块链和深度学习增强未来蜂窝网络、边缘计算和物联网中的资源优化：挑战和当前解决方案 443Upinder·考尔和沙鲁 18 5G 启用的物联网对工业自动化的重要性 477

是印度古吉拉特邦艾哈迈达巴德尼尔马大学计算机科学与工程系的副教授。他是波兰波尔科维采的扬·韦兹科夫斯基大学和罗马尼亚皮特什蒂大学的访问教授。他于 2002 年获得印度库鲁克什特拉大学的 B.Tech 学位，2009 年获得印度古鲁·戈宾德·辛格·因德拉普拉斯特大学的 M.Tech（荣誉）学位，2016 年获得无线传感器网络专业的博士学位。他是 IEEE、Elsevier、Springer、Wiley 等领先期刊和会议上发表的 200 多篇技术研究论文的作者或合作者。他的一些研究成果发表在*IEEE TNSE*、*IEEE TVT*、*IEEE TII*、*Transactions on Emerging*、*Telecommunications Technologies*、*IEEE WCM*、*IEEE Networks*、*IEEE Systems Journal*、*IEEE Access*、*IET Software*、*IET Networks*、*JISA*、*Computer Communication*、*Applied Soft Computing*、*JPDC*、*JNCA*、*PMC*、*SUSCOM*、*CEE*、*IJCS*、*Software: Practice and Experience*、*MTAP*和*Telecommunication System*等高被引用期刊上。他还与 IET 和 Springer 等国家/国际出版商合作编辑/撰写了 13 本书。他编辑的一本教材，《面向物联网应用的多媒体大数据计算：概念、范式和解决方案》，2019 年由 Springer 出版，截至 2021 年 3 月 13 日已下载了 370 万次。这本教材吸引了全球研究人员的关注。([`​link.​springer.​com/​book/​10.​1007/​978-981-13-8759-3`](https://link.springer.com/book/10.1007/978-981-13-8759-3))。他指导了许多学生完成 M.E./M.Tech 和博士学位。他目前是《物理通信》、《计算机通信》、《国际通信系统杂志》和《安全与隐私》的编辑委员会成员。他目前的兴趣包括无线传感器网络、雾计算、智能电网、物联网和区块链技术。他于 2017 年发起了区块链技术在各个垂直领域的研究领域。他被邀请担任许多国际期刊的客座编辑/编辑委员会成员，在亚洲举办的许多国际会议上担任主题发言人，在北美、欧洲、亚洲和非洲举办的许多国际会议上担任程序主席、出版主席、宣传主席和分会主席。他曾获得 IEEE GLOBECOM 2018、IEEE ICC 2019 和 Springer ICRIC-2019 的最佳研究论文奖。他是 IEEE、CSI、IAENG、ISTE、CSTA 的高级会员，是 IEEE 通信学会触觉互联网技术委员会的成员。

贡献者