© 作者（通过 Springer Nature Singapore Pte Ltd. 排他许可） 2022M. Dutta Borah 等人（编著）AI 和区块链技术在 6G 无线网络中区块链技术[`doi.org/10.1007/978-981-19-2868-0_1`](https://doi.org/10.1007/978-981-19-2868-0_1)

# 从 5G 到 6G 的范式转变中协助的技术

Murari Kumar Singh^(1  )、Rajnesh Singh^(2  )、Narendra Singh^(3  ) 和 Chandra Shekhar Yadav^(4  )（1）印度北方邦大学沙达校区计算机科学与工程系（2）印度北方邦大学 GL Bajaj 技术与管理学院信息技术系（3）印度北方邦大学 GL Bajaj 技术与管理学院管理研究系（4）印度北方邦大学大纽约邦达工程技术学院计算机科学与工程系 Murari Kumar Singh（通讯作者）电子邮件：mksinghjamia@gmail.comRajnesh Singh 电子邮件：rajneshcdac.mtech@gmail.comNarendra Singh 电子邮件：narendra.naman09@gmail.comChandra Shekhar Yadav 电子邮件：csyadavrp@gmail.com

## 摘要

人工智能（A.I.）、区块链和物联网（IoT）应用需要大量资源、极高的数据传输速率和 1 Tbps 的增加吞吐量。为了满足这些需求，现有的 5G 网络可能不够高效。5G 可能无法完全满足基于自主驾驶车辆、无人机技术、虚拟现实（V.R.）、增强现实（A.R.）、混合现实（M.R.）和扩展现实（E.R.）等新应用的需求。6G 网络将是数据高速公路，使智能的网络物理世界完全连接。6G 技术对整合人员、设备、车辆、传感器、信息、云资源和机器人专家大有裨益。6G 网络实现了巨大的数据传输速率、超低延迟、高带宽速度、高质量的服务、能源效率和智能频谱利用。本章重点介绍了从 1G 到 6G 的演变和技术进步，使范式从 5G 转向 6G。比较了 6G 的性能指标与 5G，并在提出的章节中重点介绍了 6G 的关键特性。太赫兹通信、MIMO 和快速全包含访问将带来 6G 网络的密集化。此外，本章还介绍了具有新兴技术的 6G 应用。

关键词 6G5G 网络架构太赫兹（THz）通信区块链安全 IoE

## 1 引言

[5G 网络系统](https://zh.wikipedia.org/wiki/5G)的设计是为了满足[一切互联网（IoE）](https://zh.wikipedia.org/wiki/%E4%BA%92%E8%81%94%E7%BD%91%E4%BA%8B%E4%BB%B6)的需求。5G 系统在高频毫米波频段运行。5G 系统可以处理基本的 IoE 和超可靠低延迟通信，但对于要求端到端通信、控制和计算本地化以及 Akyildiz 传感器的新兴 IoE 技术仍然是一个具有挑战性的领域，可能无法满足。人工智能、区块链和基于 IoE 的应用需要大量资源、极快的数据速率、超低延迟和 1 Tbps 的吞吐量。此外，还需要最佳连接的异构网络环境，以满足用户和系统的异构应用需求。

为了应对这些挑战，设计了能够满足 IoE 应用需求的 [6G 网络](https://zh.wikipedia.org/wiki/6G)。5G 系统无法捕获扩展现实（X.R.）的感官输入，因为它们无法为高容量数据速率提供低延迟。无人机、水下通信和自动驾驶汽车的出现是 5G 无法满足速率-可靠性-延迟比例的领域。5G 使用的加密技术可能无法保护 IoE 设备。过去的系统使用蜂窝基站，但智能城市现在需要像道路和建筑物这样的电磁表面来满足无线网络的需求。

6G 将在将物联网转变为相关的智能 IoE、[人体互联网](https://zh.wikipedia.org/wiki/%E4%BA%BA%E4%BD%93%E4%BA%92%E8%81%94%E7%BD%91)和[纳米物联网](https://zh.wikipedia.org/wiki/%E7%BA%B3%E7%B1%B3%E7%89%A9%E8%81%94%E7%BD%91)方面发挥关键作用。为了实现增加的网络密度，它将支持高达 1Tbps 的异常高信息速率，高达太赫兹（1 到 3 THz）的非常高频率，并且提供更多的能源产品，以在没有电池的情况下使物联网设备正常运行。6G 将需要创建超过 5G 提供的管理类型。它将支持三种新服务：面向计算的通信（COC）、情境敏捷 eMBB 通信（CAeC）和事件定义的 uRLLC（EDuRLLC）。它还将与新技术的部署一起运作，例如巨大的引人注目的表面、极大范围的接收天线、可见光通信等。

在本章中，作者提出了对比 5G 和 6G 的性能指标，并使用 6G 的性能指标进行了比较。作者介绍了 6G 无线网络的主要趋势、架构、特征、异构方面以及 6G 与新兴技术的应用。本文分为五个部分。第二节 2 提供了有关 1G 到 6G 通信系统性能分析的背景和相关工作的发展。第三节 3 描述了 6G 网络的性能测量，并与常规的 5G 进行了对比。第四节 4 描述了 6G 无线网络的技术特性和 6G 移动通信的优势。第五节 5 描述了 6G 无线网络的异构网络方面。第六节 6 提供了 6G 与新兴技术的应用，第七节 7 总结了本文。

## 2 移动通信系统的背景和演进

移动通信和网络技术始于 20 世纪 70 年代末，并随着从 1G 到 6G 的连续几代的显著演变而逐渐发展，如图 1 所示。无线和移动技术的演进和革命已经发展到了 6G，提供了高速网络、低延迟和新兴技术的整合。

**1G**：语音通话是最基本的服务，语音质量可接受，网络覆盖通常较全面。传真服务可用，但仅部分地区提供，声学调制解调器允许一些数据传输。然而，无线标准由大量的专有、相互矛盾的原则组成。在 1G（图 1）中，基于模拟平衡的 AMPS（先进移动电话系统）在美国建立起来，但一些欧洲国家采用了北欧移动无线电（NMR）系统。在德国，无线网络被称为 C 网络。当时，AMPS 的传输速率为 2.4 kbps，信道容量为 30 kHz，并且使用频分多址（FDMA）协议进行语音服务。它存在诸如低频段利用率、支持类型有限和数据服务速度慢等问题。漫游是不现实的，可用性非常有限。因此，仅约有全球总人口的 10% 使用此类服务。

条形图显示了印度生产的市政固体废物成分的最低到最高比较。生物可降解物 45-55，纸张 8-13，塑料/橡胶 9-10，金属、玻璃和破布 1-1.5，惰性物质 20-25

图 1

不同世代的技术规格

**2G**: 第二代移动通信依赖于数字技术；像诺基亚这样的公司根据 GSM（全球移动通信系统）标准推出了这项技术。芬兰在 1991 年商业化推出了它；它利用了诸如时分多址（TDMA）和码分多址（CDMA）之类的数字调制技术，64 kbps 的数据速率和最高 200 kHz 的带宽，如图 1 所示。2G 支持全球漫游，具有更好的质量和信息服务。

**3G**: 3G 移动系统的特征是由一个名为第三代合作伙伴计划（3GPP）的协会所确定的。WCDMA、CDMA2000 和 TD-SCDMA 无线技术仍在争夺成为 ITU（国际电信联盟）认可的 3G 标准。第一款通用移动通信系统（UMTS）PDA 问世。它于 2000 年推出，旨在提供高达 2 Mbps 的数据速率，适用于快速速度的互联网，15 到 20 MHz 的数据传输。它可以提供声音、视频、图片、信息和网页浏览等视听服务。它使用 WCDMA（无线码分多址）技术进行 UMTS。由于 UMTS 中各种标准（如 WCDMA、CDMA2000 和 Wi-Max）的兼容性问题，CDMA 中的自阻抗问题，WCDMA 的复杂设计以及发送成本较高，很难解决用户以最低价格浏览数据和**高速**的问题[7]。

**4G**: 第四代移动网络在 2010 年代后期推出，4G 的目标是提供高速、高容量、更好的安全性和成本更低的数据和语音服务。在这项技术中，所有移动设备都通过基于 IP 的网络系统连接。4G 利用了 OFDM 技术，克服了 3G 中使用的 CDMA 技术的基本缺陷。此外，它还结合了一些其他无线技术，如 LAS-CDMA、MC-CDMA 和网络 LMDS，以实现从一种技术到另一种技术的平滑漫游。然而，长期演进（LTE）和 Wi-Max 也被认为是 4G 技术。从理论上讲，它可以提供高达 1 Gbps 的数据速率和 20 MHz 的数据容量。此外，这项技术的数据速率已满足了用户的基本需求，但由于新兴技术应用的出现，如增强现实/虚拟现实、物联网、无人机等，需要更多的带宽和数据速率。

**5G**：5G 的标准档案已于 2018 年 6 月的 3GPP 全体会议上正式通过。它包括超可靠低延迟通信（uRLLC）、大规模机器型通信（mMTC）和增强移动宽带（eMBB）服务。URLLC 支持可靠高质量和低延迟（以毫秒计），eMBB 支持超高吞吐量，以满足用户访问原始应用、AR/VR、视频实时等的需求。5G 的目标是实现机器对机器（M2M）之间的通信，人与机器之间的互联，并提供高速、全覆盖、无限数据访问、随时随地共享信息和智能联网。

5G 的核心技术包括在物理层支持更高带宽的大规模 MIMO 天线。尽管第五代支持超可靠低延迟通信，但它存在短数据包、基于识别的 uRLLC 限制，这些限制限制了低延迟服务的活动，如 AR/VR、混合现实、新兴物联网等的高数据速率。

### 2.1 5G 的局限性：推动向 6G 迈进的驱动力

尽管 5G 通信网络可以支持 URLLC，但基于短数据包、基于识别的 URLLC 组件意味着 5G 在保证高数据速率的同时，提供需要低延迟和高可靠性质量的服务方面存在限制。未来，工业 4.0 和工业 5.0 将拥有高度密集的 M2M（机器对机器通信），智能车辆和无人驾驶车辆将需要超宽带和实时服务，如 AR/VR 云游戏、8K/4K 视频和 3D 全息视频。智能移动机器人将需要通过远程访问获得高性能的计算资源。

2030 年，无人机（UAV）、自动引导车辆（AGV）和群体网络（S.N.）将成为与计算和运输、紧急响应等相关的常态。它们将要求具有强大连通性的连续服务[8]。对于低延迟和高数据速率、通信和识别聚合、开放接口的要求需要 6G 的原始架构设计[9]。因此，例如，需要这种特殊需求的多感官 X.R. 应用程序（VR/ AR/MR）无法在 5G 蜂窝网络中发挥其最大潜力。此外，像通信、控制、处理和感知等功能的融合是万物互联（IoE）即将到来的应用的先决条件。这一方面在 5G 中被广泛忽视。为了成功运行像自主系统之类的 IoE 服务，网络需要为异构设备提供高数据速率和可靠性，以及上下行传输的低延迟[10]。为了克服这些缺点，需要一个具有革命性的 6G 无线网络，该网络已经在设计中考虑到了这些应用的要求和可能从这些新兴 IoE 设施中产生的所有相关技术趋势。

**6G**：6G 网络将确保一切都能深度、智能和无缝地连接。基于陆地、空间、空中和海洋，6G 网络将利用高吞吐量卫星建立卫星间通信、飞机通信、声学通信等[11]。6G 将能够将卫星升空并在任何两颗卫星之间进行切换。它将整合基于海洋的海洋互联网通信和基于陆地的地面移动通信等多个平台，形成覆盖全球的高精度、高可靠性网络。许多与 6G 相关的技术正在从不同的角度进行开发[8]。

解决了基本和大规模机器类型通信（MTC）向 6G[12，12]的发展。然而，对于 2030 年机器类型通信的文化转变和用例的讨论，区分了关键执行指标（KPI）和前提条件；并研究了未来 6G 网络中 MTC 的各种预期专业化影响。M. Katz 等人提出了什么是 6G 的基本愿景，创作者介绍了最近提出的概念 6GFP（6 Genesis Flagship Program）的研究计划。 6GFP 是由领先的芬兰学术和工业合作伙伴组成的财团的 8 年研究计划，旨在开发、实施和测试 6G 的关键启用技术[13]。David 和 Berndt[14]提出了 6G 系统及其需求的愿景，例如能源收集策略、电池寿命的远程充电以及利用人工智能与创新服务进行合作。他们指出了 1G 到 5G 都无法满足的一些关键需求。其中包括超长（最好是无限）电池寿命和对高数据速率（如 5G 中）的集中关注，这两者只在单一岛屿上才可用。在论文[15–17]中，作者进一步阐述了 6G 的主要度量标准、设计驱动因素。P. E. Mogensen 定义了设计 6G 的六个关键度量标准，创作者确定了以下关键技术变革，这些变革有最高潜力定义 6G 网络：（i）人工智能/机器学习驱动的空中接口设计和优化；（ii）进入新型选择群体和新的认知频谱共享方法；（iii）将约束和感知能力整合到系统定义中；（iv）实现延迟和可靠性方面的极限性能要求；（v）包括子网络和 RAN-Core 融合在内的新网络设计最佳模型；以及（vi）新的安全和隐私计划[17，18]。6G 网络比较了智能无线电（I.R.）、软件定义无线电（SDR）和认知无线电（C.R.）的关键条款。他们试图为 6G 提供一个前瞻性的研究路线图[15]。在[16]中，作者研究了 6G 的驱动因素（即全息、大规模可用性和时态/时序应用程序）、6G 网络设计原则以及 6G 组织的传播特性。

## 与传统 5G 网络相比的 6G 网络的 3 个性能指标

与 5G 和 5G 不同，6G 将具有高峰值速率、高客户体验速率、低延迟、高关联密度、强大的移动性、高流量密度、高可靠性、高网络能效、高到达效率、强大的定位能力、强大的覆盖支持能力等。如下图所示[2]。![](img/517376_1_En_1_Fig2_HTML.png)

显示了 5G 和 6G 之间的相对性能比较。5G 和 6G 根据数据速率、延迟、流量密度、连接密度、移动性和频谱效率进行区分。

图 2

5G 和 6G 之间的相对性能比较

最可能的使用场景包括 eMBB-Plus、大型通信（BigCom）、安全超超可靠低延迟通信（SURLLC）、三维集成通信（3D-InteCom）、非常规数据通信（UCDC）、全息通信、触觉通信、人类安全通信等，这些应用将由 6G 通信支持[19, 20]。这些应用导致了识别此类通信所需的关键条款。Yastrebova 等人预测了 2030 年代的各种现代、尚不存在的无线通信条件，包括全息通话和物质互联网[21]。

图 3 显示了未来 6G 的关键特征（高安全性、多频段超快传输和高能效通信）。![](img/517376_1_En_1_Fig3_HTML.png)

条形图显示了印度一些产生最多固体废物的州（马哈拉施特拉邦、北方邦、西孟加拉邦、泰米尔纳德邦、卡纳塔克邦、特伦甘纳邦、中央邦、拉贾斯坦邦、旁遮普邦、喀拉拉邦）在固体废物的产生、收集、处理和填埋量方面的比较。

图 3

E.M.（电磁）频谱和 THz 和 mm 波长

### 3.1 高安全性、隐私和保密

依赖于 RSA（Rivest Shamir–Adleman）公钥算法等密码系统的传统加密方法仍然在 5G 网络中使用，以提供传输安全性和隐私[21]。在大数据和人工智能技术的需求下，RSA 密码系统已变得不稳定，但原始的安全保障策略在 5G 未来仍然遥遥无期。在 6G 系统中，应该利用物理安全和通过可见光通信（VLC）的量子密钥分发来解决数据安全挑战。对抗网络攻击的全面防御策略可能通过复杂的量子计算和量子技术方法证明是有用的[22–24]。通过区块链技术可以实现绝对匿名化、去中心化安全、非分散性和不可追踪性[25]。

### 3.2 多频段超快传输

诸如 M2M、智能车辆、云游戏、无人驾驶车辆、AR/VR、3D 全息视频 8K/4K 视频、无人机、AGV 和群体网络等信息饥饿型应用需要极高范围的数据传输，目前在毫米波（mm 波）范围内无法实现。目前的情况对区域或光谱空间效率以及频率范围组合的连接都有严重影响。因此，需要更广泛的无线电频率范围数据传输，这只能在亚太和太赫兹频段（图 4 中显示）中找到，通常被称为微波和光谱之间的间隙带[26]。![](img/517376_1_En_1_Fig4_HTML.png)

电磁波谱描述了频率和波长，频率范围从 106 赫兹到 1016 赫兹，电子范围从 106 到 1012。无线电波低于 106 赫兹，微波介于 1010 和 1011 赫兹之间，红外线介于 1012 和 1013 赫兹之间，紫外线介于 1015 和 1016 赫兹之间，X 射线高于 1016 赫兹。

图 4

THz 和 mm 波的电磁（Electromagnetic）谱和波长

对于高速通信，文本已对 0.1–10 THz 范围内的 THz 波段进行了简要而全面的调查[27]。由于近期微波通信的发展，THz 电气和光子技术现在是可能的。6G 混合手持设备无疑将使用 THz/自由空间光学混合。THz 信号可以由光学激光产生，或者可以发送光学信号[28]。

## 4 6G 无线网络技术特征和 6G 移动通信的优势

6G 移动通信技术具有像普遍包容性、安全性和 AI 插入的自主智能等机械进步[18, 29]。

**无处不在的覆盖**：6G 具备整合空中、太空、海洋和陆地的能力，消除信号易受损的一面，并与客户合作，实现平稳和广泛的网络覆盖。例如，为了解决现有地面通信系统覆盖不足的问题，6G 将引入空-空间通信网络（例如，卫星通信网络）以进一步提高覆盖范围。然而，卫星通信网络存在容量不足的问题。将地面通信系统的巨大容量与卫星通信网络的高覆盖范围结合起来形成混合网络将是必要的。此外，6G 将使个人和物品能够随时随地访问网络。此外，分析无线移动技术的性能以提高基础设施网络的性能方面的丢包率、端到端延迟、丢包率、节点密度、路由开销、确认数量和节点能量[30–32]。它们可以快速参与信息交换，而不受持续的网络异构困扰。系统发展和网络速度可以与精益开发相匹配。

**安全性**：6G 对数据安全进行端到端的预判和分类。它支持用户定义的方法以确保终端节点、空中接口、数据传输和用户感知的安全。同时，6G 不需要满足基本通信安全要求，而是为不同场景提供差异化的安全服务。因此，6G 可以适应各种传统或新的接入网络方法，保护用户隐私，并支持公开和可调度的安全功能。与之前的几代不同，6G 同时包含实现和虚拟化资源。与实体和虚拟环境相关的安全需求也不同。这促使对安全规划、策略制定和算法设计提出了更高的要求。随着它实现和虚拟化网络资源（应当指出的是，实体和虚拟资源都将增加网络异构性），6G 将应对物理和虚拟安全需求。

**AI 嵌入式自主智能**：6G 将与人工智能结合，实现意识、自主学习、自我增强和自我发展。例如，基于人工智能的 6G 网络的架构、运作和优化，可以发现以下情景中的好处：以用户体验为驱动的网络设置、灵活且自我增强的网络、主动网络监视和故障分析、以及主动网络安全保护[33]。根据技术的飞跃，6G 移动通信的一些更多的技术优势显示在图 5 中。![](img/517376_1_En_1_Fig5_HTML.png)

介绍了第六代移动通信的技术优势。天线、太赫兹、功率、覆盖范围和密集度是重点。

图 5

第六代移动通信的技术优势

### 4.1 太赫兹通信的概念

根据[34, 35]，第六代通信技术将于 2030 年左右出现。6G 需要更大的传输带宽来支持高数据传输速率和超快速通信。这些规格导致了培育太赫兹频段系统的出现，该系统包括 0.1 到 10THz 的频段[36–38]。总的来说，太赫兹（THz）是远红外光谱范围内的一个频率范围，即在电子学和光子学的界面处。下限直接在微波区域之上，该区域由卫星天线和手机使用，并且上限接近红外频率，该频率由电视遥控器和其他设备使用。因此，THz 间隙结合了微波和红外电磁频谱。电磁频谱的这个区域在感测、成像和通信方面具有丰富的可能性，以及在武器、爆炸物和生物危害评估中的独特应用，以及水含量和人体皮肤评估。

太赫兹天线的主要好处是获得异常巨大的传输带宽，以及最简单的调整方案。这可以用于诸如安全、研究、灵活的电子设备、远程探测、感应和图像应用、节能设备和技术设备等各种应用。它具有非常高的数据传输速率的潜力，例如每秒 1 太比特[40]，这是第六代通信网络的重要要求。

起初，它主要用于太空和天文学应用。最近发现了医学、环境和生物科学以及安全和质量控制等新的应用领域[41，42]。由于波的自由空间衍射较少，太赫兹通信比微波或毫米波链路更具方向性[43]。它可以支持超高带宽扩展频谱网络，这可以实现安全通信的大容量网络，并防范通道干扰攻击。与某些气候条件下的红外相比，太赫兹辐射的衰减较低，例如雾。在某些气候条件下和特定的电缆长度要求下，太赫兹可以实现可靠的通信，而红外网络则会在某些气候条件下失败。

有趣的是，与 5G 相比，6G 预计将支持更高的数据速率或容量（每秒 1 太字节）、更高的融合、更低的延迟、更高的可靠性（10^(–9)）、更低的能量和成本、更高的密度[44]、整体网络、自由电池 IoT 设备、与人工智能的联合智能[12]，以及这些要求的新组合以满足即将到来的用例。

由于它们的频率接近太赫兹波段，气候中的原子和微粒，如水汽和氧气，吸收或分散了太赫兹频带。由于 6G 的路损非常高，这对通信的覆盖范围和范围造成了真正的限制，这一范围高达 10 米。因此，根本需求是培育在太赫兹区域共振并支持高带宽的无线电天线，正如非常重要的那样。基于石墨烯片的天线是需要进一步探索的领域之一。通道和噪声建模、物理层、链路层、网络层和传输层都是太赫兹波段通信网络中的问题。物理层的挑战包括均衡设计、通道编码方案、多输入和多输出（MIMO）网络、中继、媒体访问控制（MAC）[45]和同步。然而，6G 通信系统所需的天线不仅应支持高数据速率，而且应该是多频带共振天线。根据应用的不同，有时需要全向天线，而有时也可能需要高度定向天线以满足特定目的。其尺寸应该非常小，制造成本应该非常低，并且最好是圆偏振天线。

多输入多输出（MIMO）天线簇技术可能被用于 6G 的原因，因为它可能提供高增益，并相互增强网络的通信范围和容量。 许多研究仍在进行中，以开发一些海上天线 [46]，46 开发了一种在 0.270–0.330 THz 下工作的漏斗形角天线，该天线采用线切割 EDM 技术制造，如图 6 所示。![](img/517376_1_En_1_Fig6_HTML.png)

描述了锥形角天线的三维分解图。 描述了一个锥形角、交叉槽、波导馈源、圆偏振盘和尾巴。

图 6

锥形角天线的三维分解图

由 47 使用多面高频 PCB 技术开发的 16 组件平面阵列天线，在 0.135 和 0.115 THz 之间共振，如图 3 所示。

### 4.2 密度

快速全包容访问将导致 6G 网络的密集化。 连接设备的密度将超过每立方米 100 个。 6G 基站将解决同时访问数以万计的无线设备的问题； 因此，新的访问元件将需要以高效和可伸缩的方式处理大量用户数据。 由于 6G 系统的密集化，每立方米超过 100 个设备的接入容量为智能家居、智能城市、灾难预防、公共健康和隐私、医疗保健和教育带来了新的应用。 6G 将为人与物之间或物与物之间提供通信 [48]。

### 4.3 功率

拉长的功耗请求将促使 6G 开发新的电池和远程能量传输技术。 6G 的到来将推动对新电池技术的研究，如固态电池和石墨烯电池。 6G 电池将具有更高的能量、更低的成本、更大的安培小时存储容量和更便利的功能。 使用远程能量传输充电 6G 电池预计将延长电池寿命并使充电更加方便 [49]。

## 6G 无线网络的异构网络方面

6G 网络将严重依赖于网络智能，网络将根据环境条件的变化执行动态活动。 据专家称，人工智能将在物联网（IoT）和生物网络（IoBNTs）驱动的未来发挥关键作用。 传输数据的最有效技术将是从 5G 过渡到 6G 的关键。 一个不需要人为干预的系统将是完美的 [46，50]。

图 7a 显示了 5G 和 6G 网络架构的比较。高处理能力、智能性和高性能已经将 6G 核心网络更新为 5G 核心网络。整合基站（B.S.）、卫星和无人机（UAVs）也将改善接入网络。在 6G 中，除了 5G 中的水平传输方式外，还有一种垂直传输方式。此外，雾计算和多接入边缘计算（MEC）是 6G 网络设计中的基本要素，通过延迟和带宽减少了用户计划中大量设备对广泛使用服务的需求。云、边缘和雾（CEF）计算用于提供快速服务访问。虚拟化、软件化和切片将用于实现自组织、自优化和自重构的特性。![](img/517376_1_En_1_Fig7_HTML.png)

第一幅图描述了 5G 和 6G 网络架构在用户计划、接入计划和核心计划方面的比较，而第二幅图描述了空间、陆地、海洋和水下的 6G 异构网络架构。

图 7

**a** 5G 和 6G 网络架构的比较分析 **b** 6G 的异构网络架构

### 5.1 云化/雾/边缘

公司中有成千上万的传感器，在家中也安装了数百个传感器，提供大量数据，将所有这些传感器连接在一起是极其困难的。此外，这些设备是复杂和智能的，能够明智地评估和利用最少的计算资源。因此，数据必须从云端下载到设备的末端。为了减少来自云的处理延迟，我们需要将处理移动到终端设备附近。为了提高服务质量，我们需要将负担转移到边缘。

### 5.2 软件化

配置性、可编程性、自组织性、灵活性和异构使用情况是创建 6G 网络的主要驱动力。实现所有上述功能的物理设备安装起来很困难。虚拟化和软件化是 6G 网络面临的两个最具挑战性的假设，因为它们使底层网络能够实现功能。软件化建立了边界和约定，允许控制平面和用户平面分离，并在软件中建立网络。用户计划通常由一组分布式路由表和无状态表组成，这些表为数据包交换提供了高速执行。中心化的控制平面提供了有关不同服务的端到端路由的信息，并更新这些表。服务提供商和 SDN 提供商负责数据交换和管理。所需服务将由 SDN 提供商发送到服务客户端。服务客户端可以使用这些虚拟资源来控制这些服务。

### 5.3 虚拟化

网络功能的虚拟化允许在虚拟机上实现软件功能，同时仍然可以访问常见的物理资源，如存储、网络和计算。在同一个虚拟机中，可以使用容器创建多个功能。连续的虚拟机可以处理不断变化的网络需求，如网络流量和服务。虚拟化服务包括(i) 服务基带处理、(ii) 负载管理、(iii) 移动管理和(iv) 演进数据核心 (EPC)。

### 5.4 切片

其中一个核心网络是允许我们在实际的共享基础设施上构建一个可适应的网络的网络切片。此外，5G 的推出将使其成为赋予各种应用广泛应用的核心技术。利用单个网络设备在共享的物理基础设施上提供多个逻辑网络，成本更低。切片可以提供给特定用例，如物联网、服务类、消费者类和无线网络运营商。它还可以归因于其他类型的网络，如有线与无线或消费者与商业。在网络切片中配置新切片是最具挑战性的工作，因为它影响整个网络组件。我们还可以为医疗保健、汽车、公用事业等构建切片。

6G 网络包括海底、海洋和所有空中通信，在图 7b 中描述。正如图 7b 所示，6G 将允许设备以极低的数据速率连接，例如物联网和生物传感器设备，同时也实现了高数据速率的通信，例如在智能城市中的高清（H.D.）视频传输。在 6G 网络中，快速移动的车辆或喷气式飞机将实现通信。它还表明所有网络将被整合。此外，智能城市中的桥梁、建筑物和表面可能安装 IRS，以改善每个通信设备的覆盖范围和服务质量（QoS）。可靠的水下数据连接将允许在海洋通信情况下在潜艇、船只和传感器之间进行连接。此外，增强现实（AR/VR）、触觉反馈和机器学习（ML）等尖端技术将进一步减小世界各地物理距离的影响。

## 6 区块链与新兴技术的应用

本章探讨了结合人工智能和区块链技术的几个 6G 无线网络方面的最新结果，并评估了未来技术的性能。人工智能和区块链在 6G 网络中具有动态资源管理和移动性管理的潜力。在 6G 中，人工智能和区块链的整合将使无线网络能够高效监控和管理资源利用和共享。由于资源有限，区块链用户可能需要通过媒体访问控制（MAC）机制竞争无线频道来广播交易。人工智能技术实现了高效智能的资源共享机制。人工智能和区块链有效优化了网络性能，在 6G 的各个部分实现了 AI-enabled wireless edge processing，执行者的出色移动性，移交板，和执行者的智能频谱以及去中心化网络管理。

### 6.1 区块链与 6G 的应用

区块链和分布式账本技术 (DLT) 应用可能被视为分布式感知服务的新一代，需要将 URLLC 和大规模机器类型通信 (mMTC) 相结合，以提供低延迟、灵活性和可靠性。这些是最具挑战性的 IoE 技术。张等人 [66] 对最近在使用区块链为远程组织提供保护、安全访问控制、资源共享、管理和认证等方面进行了全面考虑。作者还提出了一种利用区块链技术提高效率和安全性的 6G 网络可靠和安全的统一架构，称为区块链无线接入网络 (B-RAN) [51]。区块链与 6G 可以彻底改变医疗保健和农业领域 [52]**。**Sekaran 等人已经为 6G 启用的 IoT 引入了最常见的区块链应用，如车联网 (IoV)、无人机 (UAV)、供应链管理 (SCM)、食品行业、农业、智能电网、智能制造、医疗保健等，如图所示 [53]。![](img/517376_1_En_1_Fig8_HTML.png)

描述了适用于 6G 网络的区块链应用。主要应用包括车联网、无人机、供应链管理、食品行业、农业、智能电网、智能制造和医疗保健。 

图 8

[利用区块链的 6G 网络应用](https://wiki.example.org/blockchain_for_6g_network) 

作者们 [54] 强调了 6G 的需求，正如最新的 6G 研究努力、应用和为 6G 网络提供基本的支持性进步所表明的。智能资源管理、建立信任、快速、安全和透明的通信、成本降低和去中心化是区块链在 6G 中的好处 [55]。 

### 6.2 与人工智能结合的 6G 应用 

6G 网络可以提供像优化医疗规划、金融市场监测和先进预测等 AI 应用，通过增强的无线通信为各种移动设备提供服务。在某些情况下，它可能能够与人脑媲美地进行人工智能计算并实时控制。本节将从 6G 无线网络的角度探讨两个重要的人工智能应用：自动车辆调度和室内定位 [56]。 

#### 6.2.1 自动车辆调度 

热衷于城市的独立车辆调度的困难预计将通过 6G 与人工智能技术得到解决。在 6G 未来时代安全可靠地驾驶在道路上，自主车辆可以利用嵌入式传感器获取关于周围环境的数据，并根据关于车辆位置、障碍物等数据控制方向和速度。自主车辆可以与其他道路用户进行通信，如行人、骑车者和其他自主车辆，并了解它们的位置、环境因素和道路状况。例如，当自主车辆接近十字路口时，它可以快速构建与十字路口相连的实时动态网络，并在通过后将其暂停，如图 9 所示。

上传到云服务器的数据随后可以进行分析，以确定行车路线并计算行车时间。其他应用领域可能包括医疗优化规划、金融市场监控和高级预测等。

#### 6.2.2 室内定位

室内定位对紧急救援、安全监控、消防等至关重要。地震、火灾等灾难中的关键救援阶段是迅速定位被困人员，如图 10 所示。![](img/517376_1_En_1_Fig9_HTML.png)

6G 网络中描绘了基于人工智能的自主车辆、有人驾驶车辆、停放车辆、网络链接和动态网络。

图 9

使用人工智能的 6G 网络中的自主车辆

![](img/517376_1_En_1_Fig10_HTML.png)

图像展示了 6G 网络中室内定位人工智能应用。它描述了一个中央市场的地图，其中一个人被困在一个着火的电影院大厅以及其他区域，如美食广场、杂货店、电子区、服装和儿童区。

图 10

6G 网络中室内定位的人工智能应用

在紧急救援过程中，它可以提供重要的技术帮助，并保证被困人员的安全。通过数据分析，室内定位可以捕捉客户的活动，跟踪并追踪客户的情况和行为偏好。它被用于通过科学方法找到个人的持续发展或位置轨迹。如今，室内定位广泛应用于移动支付、室内导航、店内购物指导、人员活动分析、物品监控等与人类相关的任务中。因此，它具有巨大的商业价值。

**1G 到 6G 技术的摘要和比较**

表 1 提供了 1G、2G、3G、4G、5G 和 6G 架构主要元素之间的详细比较。它展示了关于网络特性、技术发展、带宽、多路复用、延迟、调制、网络标准、应用等特征的描述。表 1

各代移动通信技术 1G、2G、3G、4G、5G 和 6G 的各种特性比较

| 代 | 1G | 2G | 3G | 4G | 5G | 6G |
| --- | --- | --- | --- | --- | --- | --- |
| 网络特性 | 语音 | 数据包交换，电路交换 | 数据包交换，宽带 | 全 IP，数据包交换，超宽带 | 数据包交换，云化，软件化，虚拟化，切片，互联网 | 智能化，云化，软件化，虚拟化，切片，互联网 |
| 技术发展 | AMPS | GSM，GPRS，TDMA，EDGE | CDMA，WCDMA，CDMA-2000，UMTS | 多输入多输出，正交频分复用，载波聚合，设备对设备通信 | 云，雾，EDGE，毫米波，低密度奇偶校验码，大规模多输入多输出，非正交多址 | 太赫兹通信，量子通信，机器学习，人工智能，区块链 |
| 峰值数据速率 | 2.4 Kbps | 64 Kbps | 30 Mbps | 1 Gbps | 20 Gbps | 1 Tbps |
| 移动性 | – | – | – | 350 km/h | 500 km/h |  >  = 1000 km/h |
| 延迟 | – | 300 ms | 100 ms | 10 ms | 1 ms | 10–100 微秒 |
| 多路复用 | FDMA | TDMA/CDMA | CDMA | CDMA | CDMA | OFDM |
| 调制 | 调频，频移键控 | 高斯最小移动键控 | 正交相移键控 | 单用户多输入多输出，多用户多输入多输出时分时分频，频分时分时分频 | 频率复用振幅调制，滤波器组合多个载波，大规模多用户多输入多输出，高级多输入多输出 | 频率复用振幅调制，滤波器组合多个载波，大规模多用户多输入多输出，高级多输入多输出 |
| Web 标准 | – | 万维网 | 万维网(IPv4) | 万维网(IPv4) | 万维网(IPv6) | 万维网(IPv6) |
| 首次商业化地点 | 美国 | 芬兰 | 日本 | 韩国 | 圣马力诺 | 尚未实现 |
| 应用 | 语音 | 语音，文本 | 语音，多媒体 | 语音，移动互联网，移动电视，移动支付，高清视频 | 虚拟现实，增强现实，360⁰视频，超高清视频，可穿戴设备，物联网，智慧城市，远程医疗 | 全自动驾驶车辆，无人驾驶汽车，全息垂直，数字感知，深海视觉 |

## 7 结论

在本章中，我们探讨了移动通信技术从 1G 到 6G 的发展过程。我们首先介绍了 1G–6G 系统，并比较了 6G 和 5G 的性能指标。我们还重点介绍了 6G 的所有技术特点和重要的关键技术。高安全性、隐私、保密性和超高速传输是 6G 的一些主要优势，明确了 6G 在区块链技术中的应用。还强调了太赫兹频率通信的使用，这使得极高的带宽和超高速传输成为 6G 的主要需求。提供了天线的规格、需求和设计，随后讨论了 6G 网络通信系统中太赫兹波段的一般困难。介绍了 6G 网络的异构架构，即四层一体化的空间-空中-地面-水下网络。然后，我们探讨了人工智能和区块链如何在 6G 网络中使用。
