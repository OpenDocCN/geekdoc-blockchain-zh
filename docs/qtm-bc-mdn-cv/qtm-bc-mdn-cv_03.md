© 作者（们），独家许可给 Springer Nature Switzerland AG 2022A. Kumar et al.（编）量子与区块链对现代计算系统的影响与进展数据工程与通信技术讲义 133[`doi.org/10.1007/978-3-031-04613-1_3`](https://doi.org/10.1007/978-3-031-04613-1_3)

# 在云环境中启用安全量子计算的经验分析

Shahnawaz Ahmad^(1  ), Shabana Mehfuz^(1  ) 和 Javed Beg^(2  ) （1）印度新德里，贾米亚米利亚伊斯兰教大学，电气工程系，110025（2）甲骨文，印度诺伊达 Shahnawaz Ahmad （通讯作者）Email: shahnawaz98976@gmail.comShabana MehfuzEmail: smehfuz@jmi.ac.inJaved BegEmail: javed.beg@oracle.com

## 摘要

尽管量子云计算（CC）基于理论概念，但仍需要实验验证。CC 已经成为一个按需可访问的工具，在数字产业、学术界、制造业、医疗领域等不同实际应用中出现。备份、安全、处理和定位都是云正在处理的问题。因此，量子计算在几个领域都取得了巨大的增长。在文献中，大多数从事量子研究的研究人员都相信它将解决云服务问题。量子云计算（QCC）涉及在云环境中部署量子计算源，以克服现有简单云计算模型所面临的挑战和问题。然而，并非每个人都对将基于物理的原子计算与基于软件的 CC 相结合感兴趣。本研究将展示量子计算（QC）与云系统结合使用时所具有的所有可能的好处和缺点。本文还涵盖了一些最新的更新，以及量子作为云服务的一些不确定前景。本工作展示了量子服务领域的当前状态。此外，还进行了与类似领域的比较分析。

关键词云计算量子计算量子云量子信息处理密码学和量子云

## 1 Introduction

云计算的概念最早是由谷歌的首席执行官在 2006 年 8 月的搜索引擎大会（Sessane Jose 2006）上首次提出的。"云"一词指的是云计算中的云服务。由于过去三十年来计算和信息技术的巨大进步，计算机世界现在可以设想过渡到云计算时代[1]。近年来，云计算（CC）在学术实践、工业活动和政府运作的各个方面都有了显著增长。CC 加速了安全技术的进步，并且互联网服务的使用显著增加。在银行业的情况下，CC 是跨银行网络传输机密数据的有效工具[2]。这种数据传输在数据保护和维护其完整性、服务质量、流动性、互操作性和可移植性方面面临严重的云安全问题。在这个领域，量子云计算（QCC）理论着眼于发展基于计算机技术的概念，这被称为量子计算（QC）。在量子水平上，主要目标是系统地定义能量的性质和特征。QC 总是需要从上百万领域的最后一个发展，以增加量子计算机的能力，就像从简单的 CPU 发展到今天的超级计算机一样。通过了解量子物理定律的思想，QC 可以轻松理解，通过这些定律，高处理能力被创建，并且能力被发展到各种状态，每种状态都有助于在并行组合中执行任务。一般来说，QC 基于量子物理定律，因为量子物理学提供了各种各样的优点和核心属性，这些被定义为量子物理定律，QC 通过这些属性被启用为量子位或简称为量子位，成为计算机的处理器或内存。本研究将展示 CC 在我们的日常生活中的使用，无论是直接还是间接。简而言之，将数据和过程存储、检索和处理在网络上而不是在计算机上的实践称为 CC。CC 涵盖了各种概念和术语。由于系统存在一些缺陷，CC 也是如此，这些缺陷会产生一些后果。因此，新服务被称为量子云服务（QCaaS）。我们的主要目标是对云环境中启用安全的 QC 进行经验分析的摘要。

这项研究将展示基于量子的计算如何从根本上改变我们传统的云系统处理和通信方式。这项研究还通过一个简单的例子展示了所有主要的好处和一些最新的量子计算进展中存在的主要困难。这项研究将概述最近的发展以及量子云计算最令人关注的未来方面。此外，这项研究将从实践的角度展示量子计算和互联网系统的现实情况直至目前。

论文的其余部分格式如下：第二部分简要定义了 QC，QC 的架构，QC 的属性以及不同的可用 QC 算法及其优缺点。CC 架构及其安全问题，不同的 CC 服务模型，CC 系统中不同类型的攻击，CC 中的最新进展和趋势，以及计算范式的技术演进都在第三部分中描述。第四部分涉及 QC 中的最新进展和趋势。QC 在云基础架构中的表示在第五部分中。在第六部分中，以基于 QC 的云基础架构的研究挑战和方向为代表。在第七部分中，代表了研究的前景。最后，在第八部分中提出了结论和未来方向。

## 2 量子计算和量子力学简介

量子计算是一种基于量子理论及其惊人现象的尖端计算机技术。它精美地融合了“物理学”、“数学”、“计算机科学”和“信息论”。通过操纵小物体的行为，它具有强大的计算能力、低能耗和比传统计算机更高的指数速度。量子计算是一个引人入胜的新领域，它结合了数学、计算机科学和物理学。它关注于利用量子物理学来提高计算性能。这里简要介绍了一些量子计算的概念。Table 1

具有不同比较关键的量子计算机

| 比较关键 | 量子计算机 |
| --- | --- |
| --- | --- |
| 计算基础 | “基于量子力学的高速并行计算机” |
| 信息存储 | “基于电子自旋的量子位（qubit）信息存储” |
| 位值 | “量子位（Qubits）的值为 0、1 或有时是负数，同时可以同时具有两个值” |
| 可能状态数 | “可能状态数是无限的，因为它可以容纳 0 或 1 的组合以及一些复杂信息” |
| 结果 | “概率性-（对叠加状态上的计算重复，给出概率性答案）” |
| 处理方面，使用门进行处理 | “量子逻辑门并行处理信息” |
| 潜在解决方案范围 | “由于叠加和纠缠特性，考虑到概率性和多个答案” |
| 操作 | “操作使用线性代数，并用幺正矩阵表示” |
| 电路实现 | “微观技术中实现的电路（例如，核磁共振），速度慢且精密” |

表 1 通过不同比较关键定义了量子计算机（比如“计算的基础”、“信息存储”、“比特值”、“可能状态数量”、“结果”、“所需门用于处理”、“潜在解决方案范围”、“操作和电路实现”）。

量子计算机的架构由标准和量子部件组成，共有五层，每一层代表计算机的一个功能组件（如图 1 所示）。应用层位于堆栈的顶部，它既不是量子计算机的一部分，却又对整个系统至关重要。它包括组装相关算法所需的一切，比如“一个编程环境”、“一个量子计算机操作系统”和“一个用户界面”。该层可用于创建完全的量子算法，也可以用于创建包含经典和量子组件混合的算法。传统处理层位于应用层的直接下方，并按照所提供的职责扮演主要角色。它首先优化和编译当前正在使用的量子算法。这类似于传统计算机的 CPU，处理必须执行的每个机器码指令的众多微指令。该层还处理下方各层硬件提供的量子态测量结果，然后可将其馈回传统算法以生成最终结果。数字处理、模拟处理和量子处理层位于经典层的下方，构成量子处理单元（QPU）。QPU 的三个层紧密相连，并且一个的设计严重受到另外两个设计的影响。![](img/516210_1_En_3_Fig1_HTML.png)

图 1

量子计算机架构 [3]

QC 的性质如图 2 所示。叠加是量子物理中的一个概念，它声称任何两个量子状态都可以组合起来生成一个新的有效量子状态。在量子物理中，这是一个基本的思想。另一方面，我们可以断言任何量子状态都是由两个或更多不同状态组成的。在量子物理中，叠加指的是量子系统存在于两个不同地点或同时状态的能力。它使得惊人的并行处理以高速进行，与其传统的表兄弟不同，后者受限于二进制操作。![](img/516210_1_En_3_Fig2_HTML.png)

图 2

量子计算的性质

量子计算中最重要的一个方面之一是纠缠。两个量子粒子之间的高相关性，也称为量子位或量子比特，被称为这样（系统的物理特性）。在自然界中，远离电子云中的彼此分离的电子是极端纠缠的。在量子计算中，经典物理学中的干涉类似于波干涉。利用干涉的概念，本研究将有意地扭曲量子位的内容，以有利于正确的状态[4]。

### 2.1 量子计算的分类

量子计算可分为三类，即模拟量子计算（“量子退火”、“量子仿真”和“绝热量子计算”）、NISQ 门控计算和带有错误校正的门控量子计算（如图 3 所示）[5–8]。图 4 展示了像“傅里叶变换量子算法（QA）”、“幅度放大量子算法”、“量子行走算法”、“BQP 完全问题”和“混合量子/经典算法”这样的量子计算算法。量子开源基金会在 GitHub 上维护了一个精选列表（如表 2 所示）的开源量子工具。它根据工具的类型和工具构建的语言进行分组，并提供到工具位置的链接。Python 是量子计算中最常用的编程语言！[](../images/516210_1_En_3_Chapter/516210_1_En_3_Fig3_HTML.png)

图 3

量子计算的分类

![](img/516210_1_En_3_Fig4_HTML.png)

图 4

不同类型的量子计算算法

表 2

量子计算的各种开源工具

[9]

| 开源资源 | 使用的语言 | 起源（公司、大学、个人） |
| --- | --- | --- |
| Qubiter | C++ | 艺术家-qb，加拿大 |
| PyQu | Python | 谷歌，美国 |
| Q++ | C++ | Cybernet Systems Corp |
| QuanSuite | Java | 艺术家-qb，加拿大 |
| 量子计算游乐场 | qScript | 谷歌，美国 |
| Liqui&#124;> | F# | 微软研究院，美国 |
| 量子迷雾 | Python | 艺术家-qb，加拿大 |
| Qubiter | Python | 艺术家-qb，加拿大 |
| QISKIT | Python | IBM |
| pyQuil | Python | Rigetti forest |
| ProjectQ | Python | Ryan Babbush 和 Jarrod McClean |
| Cirq | Python | 谷歌 |
| CirqProjectQ | Python | 谷歌 |
| PennyLane 和 strawberry fields | Python | Xanadu |
| Q-CTRL | Python | 迈克尔·J·比尔楚克 |
| qHiPSTER | – | 英特尔 |
| Mitiq | Python | IBM |
| QCircuits | Python | 克罗内克积 |
| Yao | Julia 语言 | Norman Yao |
| Silq | – | 苏黎世联邦理工学院 |
| Qulacs | C++/Python | 京都大学 |
| staq | C++ | – |
| Bayesforge | Python | IBM |
| Blueqat | Python | Nvidia CUDA |
| 量子用户界面（QUI） | – | 墨尔本大学 |
| 旗博 | Python | 基利曼贾罗 |
| QuEST | C | – |
| Quantum++ | C++ | – |
| Quantum inspire | QASM | IBM |
| QUCAT | Python | – |
| QuTiP | Python | Matplotlib |
| TensorFlow 量子 | Python | 谷歌 |
| Quipper | Haskell | – |
| QX 量子计算模拟器 | – | QuTech |
| 量子算法动物园 | – | 来自 NIST 的 Stephen Jordan |

### 2.2 量子计算的优势

+   科学家们认为，量子计算机（QCs）将能够在一定时间内回答普通计算机无法回答的复杂数学问题。

+   它提供了可以处理海量数据（每天 2.5 涵字节）并从全球提取信息的计算能力。

+   由于称为“量子隧道”的传输现象，它可以并行操作，需要更少的电力，从而将功耗减少了“100 到 1000”倍。

+   一台通用的量子计算机可以比任何传统计算机快上千倍。例如，谷歌已经构建了一台量子计算机 [10]，其速度比公司实验室中的任何其他计算机慢 1 亿倍。

+   由于量子系统保持在 0.2 K 的低温以保持稳定，它可以解决挑战性问题而无需过热。

+   它可以轻松解决类似确定最佳路线、安排火车和飞机等困难。它还能够每秒处理 一万亿个国际象棋步数。即使是最安全、最难破解的加密方案也将被量子计算机破解。不过，这将导致无法被黑客攻击的替代方案。

+   它有潜力彻底改变从制药到石油等各个行业。它将能够开发新药。金融机构的营销算法可以得到加强。人工智能也可以很快得到改进。

### 2.3 量子计算的劣势

这个小节介绍了量子计算的劣势。

+   如果量子计算技术取得突破，现有的物联网安全将面临威胁。加密技术可以被用来入侵政府和商业重大企业、银行和国防系统的数据库。考虑到这些因素，量子计算有可能对人类的未来造成可怕的影响。

+   量子计算机将作为一个独立设备运行，并且无法完全取代传统计算机。因为经典计算机在某些任务上比量子计算机更优越，比如电子邮件、Excel 等等。

+   它非常精细而容易出错。

+   量子处理器因其不安全和难以测试而声誉不佳。量子计算机的工作温度保持在接近宇宙温度的 0.2 K [11]。

## 3 云基础设施简介

云计算服务模型主要分为三类（如图 5 所示），如 IaaS、SaaS 和 PaaS [12]。IaaS 用于通过已经过时的虚拟机提供基础设施。这是由于云安全和虚拟机安全之间的不一致性引起的。此外，还包括由于客户使用过时软件而导致的兼容性问题。因此，虚拟机的物理资源被分割以维护虚拟机监控器的安全性。PaaS 系统作为编程活动中的服务器。与 PaaS 相关的安全问题出现在容错、历史系统的脆弱性、隐私认证问题、互操作性等方面。![](img/516210_1_En_3_Fig5_HTML.png)

图 5

云计算服务模型

发现云计算网络包含复杂设计，并且此架构中存在多个易受攻击的区域。这些组件涉及云消费者、提供商、审计员、经纪人和云承载者。云消费者：与云提供商保持业务关系并使用其服务的个人/组织是谁？云提供商：承诺向感兴趣的人提供服务的个人/组织/实体。云审计员是对云组织进行安全问题的自主审查的主要组成部分。云经纪人是作为云计算服务买方和服务卖方之间的中间人的第三方个人或公司。云承载者充当将云管理系统从提供商传递给云用户的管道（如图 6 所示）。![](img/516210_1_En_3_Fig6_HTML.png)

图 6

云计算架构

### 3.1 云安全问题

CC 被视为具有大量潜在增长要素的新兴模式。另一方面，就其应用而言，它具有广泛的价值[17]。尽管具有独特的特点，但该系统存在多种安全威胁，这给保护工作带来了挑战。主要的三个因素包括完整性、机密性和数据的可用性[18]。关于机密性因素的安全问题来自内部人员，使得客户信息容易受到外部攻击的风险。这可能是由于内部与云服务提供商关联的成员非法获取客户信息所致。外部攻击也会产生这样的风险，包括远程软件或硬件对云客户的攻击。由于手动干扰、不足的工具、安全访问失败等原因导致的信息泄漏也会在基于云的系统中产生与机密性相关的风险。完整性威胁与客户访问控制不力有关，并围绕信息质量产生风险。在基于云的网络中，虚拟机的不恰当设计和安全参数的缺乏会产生完整性威胁[19]。与可用性相关的另一个威胁是由于信息不可访问性、恢复策略不足和物理中断引起的。发现恢复技术不足还会导致恢复失败不足，从而对恢复时间及其有效性产生不利影响。除了上述威胁外，还有四种主要攻击也以不利的方式影响云计算框架。这些攻击基于网络、虚拟机、相关存储单元和应用程序[20]。基于网络的攻击是由于黑客在端口检查期间入侵网络造成的。基于虚拟机的攻击会导致多种安全问题变得脆弱，而基于应用程序的攻击包括恶意软件注入、隐写术攻击、协议攻击等，如图 7 所示。![](img/516210_1_En_3_Fig7_HTML.png)

图 7

云计算系统中的不同类型攻击

客户无法控制 CC。因此，存在多种威胁模型，如“数据泄露”、“配置错误和不足的变更控制”、“缺乏云安全架构和策略”、“身份不足”、“凭据、访问和密钥管理”、“账户劫持”、“内部威胁”、“不安全的接口和 API”、“弱控制平面”、“元结构和应用结构”、“有限的云使用可见性”、“云服务滥用和恶意使用”（如表 3 所示）。我们最担心的是内部攻击，其中云服务提供商（如“AWS”、“微软 Azure”、“谷歌云”和“阿里巴巴”）可能欺骗或窃听客户的机密信息。 图 8 描绘了云计算中数据安全的基本特征，以及潜在的风险和防御技术[21]。表 3

云安全：问题、等级、责任和云服务模型

| 安全问题和等级 | 安全责任 | 云服务模型 |
| --- | --- | --- |
| “数据泄露” | 客户和 CSP | SaaS、PaaS、IaaS |
| “配置错误和不足的变更控制” | 客户 | SaaS、PaaS、IaaS |
| “缺乏云安全架构和策略” | 客户 | PaaS、IaaS |
| “身份、凭据、访问和密钥管理不足” | 客户 | SaaS、PaaS、IaaS |
| “账户劫持” | 客户和 CSP | SaaS、PaaS、IaaS |
| “内部威胁” | 客户 | SaaS、PaaS、IaaS |
| “不安全的接口和 API” | 客户和 CSP | SaaS、PaaS、IaaS |
| “弱控制平面” | 客户 | SaaS、PaaS、IaaS |
| “元结构和应用结构故障” | 客户和 CSP | SaaS、PaaS、IaaS |
| “有限的云使用可见性” | 客户和 CSP | SaaS、PaaS、IaaS |
| “云服务滥用和恶意使用” | 客户和 CSP | SaaS、PaaS、IaaS |

![](img/516210_1_En_3_Fig8_HTML.png)

图 8

云计算中数据安全的最重要组成部分

### 3.2 云基础设施的最新进展和趋势

云计算目前与一系列研究范式相关联，这些范式以显著的方式利用现有技术来解决相关问题[22]。 实施基于人工智能的工具可以用来解决向客户提供服务质量（QoS）方面的问题。人工神经网络（ANN）是一种有效的算法，可用于检测云计算框架在实际应用中的安全相关问题。例如，ANN 适用于确定银行系统中数据的安全传输。Levenberg-Marquardt（LMBP）算法在确定云计算系统安全级别方面也非常重要。

云计算目前与一系列研究范式相关联，这些范式以显著的方式利用现有技术来解决相关问题[22]。 实施基于人工智能的工具可以解决向客户提供服务质量（QoS）方面的挑战。人工神经网络是一种有效的算法，可用于检测云计算框架在实际应用中的安全相关问题。例如，ANN 适用于确定银行系统中数据的安全传输。Levenberg-Marquardt（LMBP）算法在确定云计算系统安全级别方面也非常重要。利用在云端加入点处可访问的系统流量信息构建的 ANN 模型，可衡量分布式计算的挑战。

### 3.3 云计算范式时间表

CC 的时间线如图所示 9。需要在不同的计算系统之间建立一个安全的通信网络来进行数据交换。在计算领域发现了一种系统化的演变，促进了不同客户端之间的通信。客户端-服务器是基于 1960 年的模型，通过该模型，客户端可以通过计算机网络相互通信[23]。之后的超级计算机、专有主机、集群计算和其他模型都为计算系统的性能提升做出了贡献。CC 是一种技术先进的计算工具，促进了数据和服务在相关社区之间的共享，同时确保了安全性、可靠性和能源效率[24]。CC 拥有有效的风险管理系统，其中包括在减轻任何类型的风险失败中所需的重要计算过程。ANN 是在这方面使用的一种技术先进的工具，用于解决计算框架中的安全问题。基于与网络安全相关联的受限、不完善和非线性数据源，采用了神经网络思想来识别和分类网络活动。![](img/516210_1_En_3_Fig9_HTML.png)

图 9

云计算范式的时间线

基于人工智能（AI）的模型对解决与信息安全相关的问题很有效。在动态计算环境中缓解恶意使用 CC 网络的最脆弱安全威胁至关重要[25]。入侵检测和防御服务（IDPS）在检测安全问题并防止其发生方面提供了巨大支持。另一方面，该系统也会生成某些不必要的警报，这会在检测实际危险时产生问题[26]。另一方面，该系统对于检测存在安全问题的系统、记录现有危险以及使参与信息交流的参与者遵守安全政策方面是有效的。通过防止分布式计算安全风险的发生来实现并行处理活动是该系统的优点。而其缺点包括增加了保护数据的计算成本，并改善了云计算系统中的安全问题。

## 量子计算、力学和信息处理的 4 个最新进展和趋势

无论是传统计算还是 QCC 出现问题时，改进工作仍在进行。我们需要的只是强大的量子计算机，能够同时生成多个量子位、量子协议和适当的通讯介质。谷歌已经发现，d-wave 使用的方法将用于他们的第一台量子计算机。通过改进 d-wave 的硬件，他们计划以一种新的方式设计量子位。最近的 d-wave 主机芯片具有 512 个量子位。他们开发了基于测量的量子计算理论框架；它提供了一种用户向量子服务器发送计算的方法。2013 年 9 月 27 日，英国布里斯托尔大学的科学家小组展示了一个量子云设备。Qcloud 是这一努力的名称。Qcloud 量子计算机安置在布里斯托尔大学的量子光子学设施中。目标是以可行的方式建立 QC 为服务（QCaaS）[27]。全球任何人都可以远程访问和管理这个量子处理器。它将允许用户进行实验，并将结果与其模型进行比较。然而，他们只使用了 2 个量子位。这是如何在现实世界中使用 QC 和 CC 的最新案例。远距离量子密钥传输需要使用量子中继器。我们可以利用光子在“幽灵般的行为”具有的距离上的优势。由于两个纠缠对之间的关系[28]。Zeilinger 和他的同事利用纠缠通过第三个光子在多瑙河上跨越 600 m “传送”信 息。如果这种技术可以扩展到许多中继器，密钥中的量子位可以横跨大陆或海洋进行传输[29]。简言之，量子计算研究的机遇如图所示。![](img/516210_1_En_3_Fig10_HTML.png)

图 10

量子计算研究的机遇简介

### 4.1 处理和用于安全问题的量子密码学

加密是将消息或数据加密的过程，以便只有授权方才能阅读它[30]。在公钥加密技术中，加密密钥可供所有人使用以加密消息。只有接收方拥有解密密钥，才能读取消息。各种加密算法包括“Triple DES”、“Twofish 加密算法”、“Blowfish 加密算法”、“高级加密标准(AES)”、“IDEA 加密算法”、“MD5 加密算法”、“HMAC 加密算法”、“RSA 安全”、“RC4—也称为 ARC4”、“ECC 非对称加密算法”、“W7”、“MARS”、“RC 2”、“RC 5”、“RC 6”、“Threefish”、“Serpent”、“Diffie-Hellman”、“椭圆曲线”、“SHA 1”等（如图 11 所示）。它的重要性在于，如果数据的安全传输被忽视，安全漏洞会给组织造成巨大损失！[](../images/516210_1_En_3_Chapter/516210_1_En_3_Fig11_HTML.png)

图 11

不同的轻量级加密算法

在加密之前，数据被称为明文，而在加密之后，数据被称为密文。数据加密是在存储或从一个节点移动到另一个节点时有意执行的，以保护敏感信息。现代加密工具具有诸如“数据完整性”、“数据认证”以及“不可取消”等机密性属性。数据发送方通过认证进行检测和检查；诚实功能显示数据内容没有偏差，而不可取消属性则保证发送数据的人不会拒绝它。因此，应建立一个适当的密钥管理系统，将加密密钥分布在传感器节点之间。在密码学中，加密是将消息或信息加密的过程，以便只有授权方才能阅读，其他人则不能。非对称加密和对称加密是两种加密方法。在公钥加密系统中，加密密钥对所有人开放以加密消息。只有接收方才能访问解密密钥，这允许消息被阅读。公钥加密首次在 1973 年的一份机密文件中进行了解释。在此之前的所有加密系统都是对称密钥（也称为私钥）。在对称密钥方案中，加密和解密密钥是相同的。通信各方必须具有相同的密钥才能实现安全通信。这些技术也可以用于保护量子互联网系统中的终端用户的云通信。量子互联网完全依赖于光子传输；当我们将加密数据传输到云时，如果有人拦截，数据可以很快被修改。最后，终端用户将能够确定数据传输过程中是否被拦截。因此，如果我们希望构建量子互联网，安全机制将得到显着改进。一支来自麻省理工学院（MIT）和西北大学（NU）的研究团队[31]创造了一种用于高保真、长距离通信量子比特传输的方法[18]。首先，大多数量子问题仍然是理论性的。有些已被证明，而其他一些仍在测试中。除了量子计算的这个主要问题之外，还有一些其他困难需要考虑：

+   在同一时间生成量子比特并将多个量子比特同步是非常困难的。

+   由于干扰，量子密码传输能力太短。最近，“鲍里斯·科尔日，查尔斯·刺温·林” 等人建立了一种“在 307 公里光纤上可行且安全的量子密钥分发（QKD）” [32]。

+   量子分散网络中，根据我们所使用的物质，我们必须将各种“量子比特”转换为光子，这是量子通信最困难的事实。

+   当光子与其他粒子碰撞时，其自旋可能会改变，并且有可能在接收时其极化不会按照预期的方式。

+   大多数量子计算是基于物理定律的；然而，要创建量子代码编译非常困难。

+   整个过程昂贵、精细，并且尚未取得成果。

+   最后，请记住，对云系统的不道德内部攻击是无法阻止的 [29]。

考虑以下情景：云上的两个用户（Alice 和 Bob）正在通过量子密码加密交换和接收量子密钥，而黑客正在试图窃听对话。

***阶段 1***: *Alice 在通过光纤向 Bob 发送消息之前生成一个“量子比特”。*

***阶段 2***: *Alice 利用极化计算密钥的值。*

***阶段 3***: *Bob 等待光子到达，然后随机使用任何直线或对角极化滤波器，记录极化、自旋和值。*

***阶段 4***: *在完全传输后，Alice 和 Ezekiel 通过一个未加密的公共通道交流，而 Bob 只是提供给 Alice 他所使用的极化滤波器序列。*

表 4 显示了结果。密钥由 Alice 以以下格式发送：(01,101,101)。Alice 和 Bob 只需比较极化滤波器序列，而不是直接接收密钥。表 4

Alice 发送一个密钥，即极化的。

| Alice 的极化 | X | X |  +  |  +  | X |  +  |  +  |  +  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 自旋 | **\** | **/** | **−** | **│** | **/** | **−** | **−** | **│** |
| 数值 | **0** | **1** | **1** | **0** | **1** | **1** | **0** | **1** |

***第五阶段***：*现在，如果 Bob 收到了一个错误的信息序列，如* 表 5 *(10,011,001)，Alice 将确定该序列是否有效。在完全传输和修正不正确的极化后，可以提供和解密最终加密的数据。*表 5

Bob 收到了一个有误的密钥比特

| Alice 的回答 | Y | N | Y | Y | Y | N | N | N |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Bob 的极化 | **X** | ** + ** | ** + ** | ** + ** | **X** | ** + ** | ** + ** | **X** |
| Bob 的自旋 | **\** | **−** | **−** | **│** | **│** | **−** | **−** | **/** |
| Bob 的数值 | **1** | **0** | **0** | **1** | **1** | **0** | **0** | **1** |

在这个系统中，中间没有窃听者可以准确地推导出所有的极化。如果 Alice 和 Bob 都检查了极化，但 Bob 无法解码数据，那么黑客的通信干扰将会很快被检测出来。

### 4.2 量子密码学的研究方向

最近对量子原理的测试揭示了保护云系统的两种不同方法。一种方法被称为盲计算，其中量子处理的计算机对所有输入和数据处理都不知情。根据盲计算，云用户构建了量子比特，并且只知道早期状态。在将这些量子比特交付给量子计算机后，计算机使用正常机制来组装量子比特。计算本身基于测量。用户将这些规则应用于每个量子比特的个体条件。处理成功后几秒钟，用户会收到自己的结果，并可以得到最终的结果。整个过程是“盲”的，因为如果量子计算机试图解码量子比特，则不会收到相关信息。这是因为他们对原始条件一无所知。使用量子互联网系统的量子密码学是另一种选择，其中使用光子偏振滤波器来加密和解密数据[33]。

## 云基础设施中的量子计算

与其他发展中的技术（如人工智能和机器学习）一样，云上的量子计算具有颠覆业务的潜力。根据[34] IBM 量子生态系统发展副总裁 Bob Sutor 的说法，量子计算仍然通过大学课程和工作路径在发展。同样，大型云服务提供商在这个早期阶段仅专注于教育。量子计算编排平台 Quantum Machines 与联合创始人兼首席执行官 Itamar Sivan 表示，“今天的云服务旨在为行业做准备，迎接量子计算机即将到来的时刻”[34]。

2016 年，IBM 成为首家将小型量子计算机连接到云计算的企业，使用户能够通过互联网编写和运行量子计算机上的短程序。自 IBM 首次提出基于云的量子计算概念以来，其他计算机巨头也急于尝试。因此，“Google”、“Amazon”和“Microsoft”等科技巨头决定跟随 IBM 的步伐。2019 年，微软推出了“Azure Quantum”，这是一个服务，让用户可以访问量子算法、硬件和软件[35]。图 12 显示了量子云的整合，增强了 QCC 的安全性，提供了高速度、大存储，并为 QCC 环境提供了 QCC 作为服务的功能。![](img/516210_1_En_3_Fig12_HTML.png)

图 12

云量子计算的整合

## 量子计算基础云基础设施中的 6 个研究挑战和方向

由于量子技术仍处于早期发展阶段，在它能够在机器上大规模使用之前，必须解决许多问题。量子测量暴露了状态的一个类似成分，这是与归一化振幅的概率不同的可能状态的完全叠加[31]。因此，无法确定系统的精确状态。这个约束条件使得使用量子复杂性理论来评估量子计算的成本变得困难[31]。随着某些多项式时间量子算法所需的测量设备数量的增加，其重要性可能会增加。即使它是一个研究困难，它也可以用来克服另一个量子云的限制，即退相干。量子测量被用于纠缠保护策略，这可以有效地避免甚至是纠缠突然死亡（ESD）。理解多部分纠缠和操纵多部分纠缠态对于分布式量子计算和网络至关重要，因此在量子纠错码中发挥关键作用[31]。因为，根据[6]，纠缠不能在不同的粒子之间交换，确定多部分纠缠的边界和可能性是一个迷人的科学话题。在计算理论领域，确定量子细胞自动机与量子图灵机的计算能力仍然是一个挑战。对于云环境中量子基础设施的 10 个有效应用，量子云必须解决这些问题。能够在更大规模和更可靠的环境中进行量子计算的云量子处理器一直是广泛技术发展的主题。困扰离子、液态 NMR 和电子自旋晶体管是一些被提出和用于这些量子比特处理器开发的技术，但与之相关的挑战是建立“初始状态”、“稳定量子存储器”、“执行测量读数”和“与退相干作斗争”。对于在量子云中的实际应用，量子比特处理器的范围需要扩展，以便它们能够处理要处理的信息的负担。开发量子-经典界面协议的挑战仍然相对较新，因为一旦我们实现了基本的量子计算机并设计了必要的量子算法，下一步就是开发经典和量子基础设施之间的接口，因为量子云将使用经典基础设施。有必要构建能够结合量子和经典水平的网络协议，以及应用像盲 QC 和量子密码学等思想。

## 7 未来前景：确定与不确定

云计算一直备受质疑，如果对终端用户的安全性和可靠性没有保证的话。正如我们所展示的，量子计算原理可以解决与云计算相关的所有问题，但前提是量子云计算在未来得到充分发展。IBM 在人口普查时宣布了一款新的云计算超级处理器。然而，量子计算仍然受到《连线》杂志的质疑。根据几家企业的说法，量子计算存在许多缺点。以下是主要关注的问题：D-Wave 的巨型黑匣子是否为量子计算机？在亚原子水平上是否可能施加影响？制造操作量子比特的新门的最有效方法是什么？我们将如何避免光子噪声效应？如果适量的噪声解开量子比特，量子计算机将像经典计算机一样运行。还有“如何将大量量子比特（1000）进行并行化？”。“它有多少可移植性？”仍有许多问题有待解答。因此，量子云计算是可能的。我们希望我们在量子计算方面持续取得的进展将引发一场革命，并为未来的更好的量子云系统铺平道路。

## 8 结论

这项研究将展示量子计算（QC）如何比传统计算更高效。在安全性、处理和运行方面，量子云计算表现优于传统云计算。在这项工作中，我们将尽一切可能的方式，连同适当的例子，来展示量子云计算的演进。量子云作为服务（Qcaas）是一种未来将会推出的新技术。随着量子的接近，我们必须继续学习和发展，创造出提供最优质服务的适应性企业和公司。我们希望它将在未来继续发展，带来新的革命，开启最美好的未来。如果没有端到端用户的安全性和可靠性保证，云计算（CC）总是备受质疑。正如我们所展示的，量子计算原理可以解决与云计算相关的所有问题，但前提是量子云计算（QCC）必须完全为未来发展做好准备。