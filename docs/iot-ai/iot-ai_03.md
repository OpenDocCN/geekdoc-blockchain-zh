© 作者(们)，独家许可给 Springer Nature Switzerland AG 2021R. Kumar 等(编著)物联网，人工智能和区块链技术[`doi.org/10.1007/978-3-030-74150-1_3`](https://doi.org/10.1007/978-3-030-74150-1_3)

# 3.网络韧性能源基础设施和物联网

Divya M. Menon^(1  )，S. Sindhu^(2)，M. R. Manu^(1)和 Soumya Varma(1)教育部，阿联酋，阿布扎比(2)乔迪工程学院，印度，特里苏尔关键词智能电网智能家居实用中心智能家电信任传播网络韧性机器学习物联网消息队列遥测传输电力生态系统的演变 Divya M. Menon

目前在阿联酋教育部担任计算机科学教师。她曾在印度喀拉拉邦乔迪工程学院计算机科学与工程系任副教授，目前正在阿玛里塔维什瓦维达佩塔姆科伊马托尔计算机科学与工程系攻读智能电网安全的博士学位。她获得了信息技术硕士学位。她的研究兴趣包括智能电网、数据挖掘和计算机网络。她在吉隆坡举办的国际会议上凭借她关于使用深度学习技术进行智能电网安全研究的论文获得了最佳论文奖。她曾在不同的资助研究项目下工作，并在不同的 Scopus 和 SCI 索引期刊上发表论文。![../images/504166_1_En_3_Chapter/504166_1_En_3_Figa_HTML.jpg](img/504166_1_En_3_Figa_HTML.jpg)

Sindhu S.

目前在印度喀拉拉邦的 Jyothi 工程学院电子与通信工程系担任副教授。她毕业于印度科英布扎里大学，考邦拔拉塔米，获得了博士学位。她的研究兴趣包括电力质量、定制电力设备、电力电子和智能电网。她在不同的 Scopus 和 SCI 索引期刊上发表了论文。![../images/504166_1_En_3_Chapter/504166_1_En_3_Figb_HTML.jpg](img/504166_1_En_3_Figb_HTML.jpg)

Manu M. R.目前在阿联酋阿布扎比的教育部担任计算机科学教师。他曾在印度德里的加尔各特亚斯大学计算机科学与工程学院担任助理教授。他在印度泰米尔纳德邦的安娜大学塔拉马尼校区获得了计算机科学与工程的硕士学位，并目前正在加尔各特亚斯大学攻读计算机科学与工程的博士学位。他的兴趣领域包括大数据、网络和网络安全。他参与了不同的网络专业研究项目，并在各种国际和国内期刊上发表了 16 篇论文。他目前正在为 CRC 出版社、斯普林格出版社和爱思唯尔出版社撰写专著和书章节。![../images/504166_1_En_3_Chapter/504166_1_En_3_Figc_HTML.jpg](img/504166_1_En_3_Figc_HTML.jpg)

Soumya Varma

目前在阿拉伯联合酋长国教育部担任计算机科学教师。她曾在印度喀拉拉邦特里苏尔的 Sahrdaya 工程技术学院计算机科学与工程系担任助理教授。目前，她正在印度科伊马托尔的 Karunya 理工学院计算机科学与工程系攻读博士学位，研究领域为“用于自动视频字幕生成的深度学习技术”。她在印度马哈特玛·甘地大学获得了计算机科学与工程的学士和硕士学位，并在硕士学位中获得了大学排名。她的研究兴趣包括视频处理、医学图像处理、机器学习、计算机网络和深度学习。她在许多国际会议上展示过她的作品，并在各种期刊上发表过研究论文。![../images/504166_1_En_3_Chapter/504166_1_En_3_Figd_HTML.jpg](img/504166_1_En_3_Figd_HTML.jpg)

电力生态系统一直以来都是复杂的，并且与各种电气和网络组件密切相关。电力网络由发电站、输电线路和配电线路组成。传统电网中执行的主要任务包括三个主要部分：发电厂发电、将电力传输和分配给工业和家庭消费者。发电包括利用可再生能源和非可再生能源发电。发电的电力被送往变电站，然后从变电站传输到不同的客户（Liu 等人，2018）。电力的供应和需求在传统电网中显著增加，因此需要优先考虑电网的现代化。能源系统继续在发电、输电和配电领域部署创新技术，以改善性能并保持电网的环境可持续性。我们日常生活对电力的依赖程度不断增加，对电力质量的需求也在增长，这促使行业开发更好的电力网络（P. Ganguly 等人，2019）。将电网现代化以使其成为智能电网，是指通过整合尖端技术对传统电网进行电脑化。智能电网中的先进技术包括被称为相量测量单元（PMUs）的先进传感器、智能电表、继电器和自动馈线开关。智能电网是一种网格自动化技术，允许消费者参与到系统中。从传统电网向可靠的智能电网的渐进过渡承诺将改变整个电力基础设施及其与电力系统中所有利益相关者的关系。然而，引入这些数字技术引入了额外的网络风险维度。网络弹性是整个电力行业面临的挑战。物联网（IoT）设备的增加以及整个电力网络的数字化为网络攻击面的增加铺平了道路（Elmrabet 等人，2012）。图 3.1 表示智能电网的层次结构。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig1_HTML.png](img/504166_1_En_3_Fig1_HTML.png)

图 3.1

智能电网层

## 3.1 网络弹性原则

网络弹性是所有组织面临的挑战；电力生态系统对发生的网络攻击产生了重大影响（R. Marah 等人，2020）。在电力行业中，网络风险是一个具有挑战性的问题，因为电网部署在一个大型互联网络上。

### 3.1.1 什么是网络弹性？

网络弹性是组织在不引起重大灾害的情况下，适应、管理或准备其企业的能力，以应对任何网络攻击。这是从网络攻击中恢复并管理企业，并持续有效地运营业务的能力（Nazir 等人，2015）。完全消除网络攻击在实践上是不可能的，因为黑客将始终寻找入侵系统的方法，通过识别任何网络中的缺陷和漏洞。然而，系统弹性是通过提供的可持续性来分析的。在电网的任何一层发生攻击都可能导致整个电力系统瘫痪，并可能导致全面停电。智能电网中的网络弹性需要分析智能电网架构中每一层的所有安全约束。在智能电网中实现弹性是一项挑战，因为电网是一个由复杂的电力系统、高端网络组件、复杂的数据库和云架构构成的复杂体系。智能电网的弹性是在网络攻击后迅速恢复电力网格运行的能力（Hossain 等人，2019）。

### 3.1.2 网络弹性挑战

智能电网系统中的网络安全组件需要解决智能电网中所有可能的攻击（AlMajali 等，2012）。智能电网的部署需要考虑主要的安全目标，包括保密性、完整性、可用性、真实性、授权和不可否认性（Liu 等，2012）。主要挑战是识别智能电网系统中所有可能的漏洞，并开发一个能够及时从攻击中恢复的系统（Ghiasi 等，2020）（Khan 等，2020）。需要在每个智能电网层设计工具，以实现更快速的恢复，从而实现电网的自愈（Ghiasi 等，2020）。图 3.2 描述了智能电网中网络弹性的三个主要阶段。电力基础设施中攻击的早期检测和诊断是实现网络弹性所必需的。网络弹性网格只能在网络智能电网架构的顶部实施。网络基础设施应纳入到物理层基础设施之上。弹性应验证整个系统，包括网格中的物理和网络组件。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig2_HTML.png](img/504166_1_En_3_Fig2_HTML.png)

图 3.2

网络弹性的阶段

网络韧性的一般设计原则包括物理安全、风险管理和系统建模。主要阶段是设计核心原则以实现网络韧性。设计原则需要考虑电网的物理基础设施安全和数据安全。风险管理应涵盖与电网相关的所有漏洞（Nazir 等，2015）。在解决方案实施之前，需要监测和分析风险。在实施安全性时应考虑风险的实时优先级。智能电网系统预计将通过全面的架构框架提供韧性。

电网中的系统建模涉及考虑电网的每个安全目标。使用 IT 安全工具如防火墙、入侵检测工具、异常检测工具和第三方监控工具来提供基于网络和基于主机的安全性（Le Blanc 等，2017）。利用相关的网络安全工具来增强电网性能是实现网络韧性的重要步骤。企业和组织应在智能电网中实施网络韧性治理以实现有效实施。

### 3.1.3 网络韧性生命周期

网络韧性战略可以捍卫电网系统免受潜在风险的影响。该策略应保护关键的应用程序和数据。需要识别通信网络架构中的漏洞，并尽早从任何安全漏洞或系统故障中恢复，以确保电网的可持续性。智能电网需要系统集成方法来确保电力转换的无缝性（Hossain 等，2019）。网络韧性生命周期考虑了所有智能电网组件，并帮助确保电网的整体性能。

网络韧性生命周期的阶段包括：

1.  3.2.1.1

    识别潜在风险

1.  3.2.1.2

    数据保护

1.  3.2.1.3

    异常检测

1.  3.2.1.4

    快速响应

#### 3.1.3.1 识别潜在风险

智能电网应识别可能对其性能产生显著影响的网络安全风险。电网中的网络基础设施应考虑影响电网电力流的机密性、完整性和可用性的威胁。对电网的威胁分析应包括所有可能发生的网络安全威胁，甚至还应包括看似不太可能发生的威胁。

#### 3.1.3.2 数据保护

网络安全的主要目标是提供数据保护。智能电网中从普遍数据源生成的数据以格式和大小不一致。在实现网络弹性时，考虑到这一点是一个主要挑战。生成的数据包括来自发电站的不同传感器源、智能电表的成本相关数据、公用事业的定价信息，以及不同电子组件的状态信息。将来自不同智能传感器源的大量数据集成到智能电网中又是另一个挑战。

#### 3.1.3.3 异常检测

异常是意外事件或偏离正常行为的事件。智能电网中的异常检测需要进行，以便早期检测网络攻击。监督和无监督的机器学习用于智能电网中的异常检测。由于存在未标记的数据，无监督机器学习被广泛使用（Breiman，2001）。

#### 3.1.3.4 快速响应

智能电网应该对配置中的所有变化做出快速响应。智能电网应该有一个指数响应的系统。智能电网部署中不可避免地需要一个快速响应的系统。为了提高电网的安全性，发电、配电和传输基础设施需要能够快速响应电网中发生的异常。

## 3.2 物联网使能的智能电网

智能电网是下一代物联网使能的电网，包括通信和网络技术。物联网使能的智能电网的主要范围是通过启用传感器，提供给电力公用事业管理机构一个高效的容错系统，以便早期检测攻击。图 3.3 代表了智能电网中的物联网范式。在电力系统停电事件发生时，快速恢复是自愈智能电网的需求。远程监控和管理电力系统设备是物联网使能的智能电网的优势，它可以为电网网络中现有问题提供长期解决方案。公用事业站必须将所有电力设备、电网、充电站和储存空间与智能传感器整合在一起。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig3_HTML.png](img/504166_1_En_3_Fig3_HTML.png)

图 3.3

智能电网中的物联网范式

这将有助于检测停电，并实现有效的电力分配和负载管理，从而帮助公用事业公司保持经济节省（Al-Turjman＆Abujubbeh，2019）。 IoT 的整合可以为客户提供有关其日常能源使用情况的详细信息，以帮助明智决策并保持成本效益。 这将有助于长期节能和成本节约。 IoT 启用的电网技术进步可以为住宅客户提供独立性和可靠性。 这可以帮助住宅客户成为智能电网基础设施的积极参与者。 随着这些进步（图 3.4），消费者将自动成为电力部门的决策者。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig4_HTML.png](img/504166_1_En_3_Fig4_HTML.png)

图 3.4

IoT 在智能电网中的作用

智能计量技术有助于改善使用统计数据的可见性和经济管理（Aranha 等人，2019）。 IoT 启用的智能家居可以通过自动使它们脱网，帮助在发生电力事故时维护家庭的安全。 IoT 利用智能电网中的传感器架构，有助于检测不可预测的情况和停电。 智能电网的自愈性质通过 IoT 的整合得以实现，这有助于在任何组件故障或停电事件发生时将电网切换到孤立模式。 借助 IoT 的实时监控智能电网主要涵盖从发电厂到住宅智能家居的电网所有领域。 在 IoT 的干预下，智能电网正在逐步向自愈的更智能环境发展。

与智能电网之前相比，电力系统发电级别已经受到了更多关注。随着 IoT 的发明，电力发电框架的复杂性增加，带来了自主性和更高的性能。利用 IoT-enabled 传感器可以监控来自煤炭、风能、生物质等不同能源的电力发电情况。考虑到可再生能源的间歇性，将其整合到电力发电中是一项巨大的任务。从公用事业运营商的角度来看，IoT 的概念已经帮助了这一情景。利用基于 IoT 的传感器网络，可以有效监测电力消耗，无论是从公用事业还是客户的角度来看。物联网帮助测量智能电网网络中涉及的不同类型参数，从而有助于智能电力消费和管理能效和需求侧管理。智能电网有效实施的主要要求是在智能电网的所有关键点部署 IoT。

### 3.2.1 IoT-启用智能电网中的层

将物联网与智能电网的集成将以可靠性和可扩展性方面成倍增加电网的能力。IoT 启用的智能电网最基本的架构主要有三层：

+   应用层

+   网络层

+   对象层/物理层

物理层或对象层包含用于数据感知和数据收集的所有设备。安装在智能电网的不同层中，从发电和传输到家庭区域网络的分配，有助于使电网高效。对象层包括智能电表、执行器和其他传感器，这些传感器从周围环境中收集数据，并用于控制不同的电网组件。它还包括微控制器和模块，用于传感器之间的有效通信。网络层包括网格架构中使用的所有通信技术。家庭区域网络使用 Wi-Fi 和 ZigBee 进行智能家居内部的通信。WiMAX 在家庭区域网络和分配侧用于通信。通过网络层中使用的网络技术，从物理层收集的数据被传输到顶层。应用层是最顶层，包括智能家居、电动车和其他服务（见图 3.5）。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig5_HTML.png](img/504166_1_En_3_Fig5_HTML.png)

图 3.5

物联网的层次结构

## 智能家居与智能电网的融合

万物互联与智能家居组成的家庭区域网络的协作是一种有前途的方法，将有助于充分释放智能电网的能力。智能家居由一系列连接到互联网的家用设备组成。智能家居与智能电网的整合有助于实现下一代电网的能源效率、成本效益和可持续性。在未来的日子里，智能电网技术有助于与公用事业中心和帮助管理客户能源消耗的智能电表进行日常通信。智能电表仍然是客户与公用事业中心互动的基本单位。家庭区域网络中的智能电表连接到聚合器，而聚合器又连接到电网的公用事业中心。先进的信息和通信技术以及物联网的帮助帮助客户实时管理电力使用，从而帮助他们调整月度预算。客户可以根据其日常例行事务管理智能家电，从而有助于管理家庭能源消耗（图 3.6）。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig6_HTML.png](img/504166_1_En_3_Fig6_HTML.png)  

图 3.6

智能家居在智能电网架构中的应用

### 3.3.1 智能电网组件及其漏洞

智能电网具有两个主要组成部分：系统组件和通信组件（Aloul 等人，2012）。电网中的系统组件包括智能家电、智能电表、公用事业中心和服务提供商，通信组件包括家庭区域网络和广域网络。智能家电是构成智能电网家庭区域网络的基本系统组件。智能电表是智能家庭的一个组成部分，有助于有效管理客户的用电情况。公用事业中心管理从所有智能电表收集的详细信息，这些信息有助于用电统计和容错系统的工作。服务提供商是注册的电力供应商，与公用事业的许可一起为住宅和工业客户提供电力。服务提供商必须使用数字证书进行身份验证，以建立智能电表和其他智能家电之间的安全信任通信。

智能电网的**漏洞**是不同组件受攻击者攻击的可能性（Clements & Kirkham，2010）。最容易受攻击的关键组件是智能电表。连接在智能电表上的各种设备的多样性也使智能电表易受攻击。智能电表收集来自个别家用电器的所有信息，并将这些客户数据发送给公用事业公司。从设备收集的数据对电网的正常运行至关重要。从设备收集的数据包含具有高度关键的生活方式信息的客户。然而，如果这些数据没有得到安全保护，或者被窃取或泄露，可能会导致严重的安全漏洞。每个智能电表都配备有相同的安全机制，因此如果攻击者能够破坏一个智能电表的安全性，那么所有智能电表的安全性都可能会受到影响（图 3.7）。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig7_HTML.png](img/504166_1_En_3_Fig7_HTML.png)

图 3.7

智能电网组件

## 智能电网的安全漏洞

智能电网是现有电力系统中先进通信和计算技术的结合体。智能电网是一个与物联网网络集成的巨大复杂网络，因此与电网相关的漏洞是众多的。智能电表、智能充电器和分布式能源资源都是智能电网的组成部分，易受网络攻击。对这些组件的攻击严重程度可以从低到高，具体取决于它造成的破坏影响。智能电网中的安全架构需要考虑人类和他们生活社区的安全，同时满足主要的安全目标。在智能电网中，攻击者在针对攻击时遵循攻击循环（Knapp & Samani，2013）。电网中的攻击循环主要分为四个步骤，即侦察、扫描、利用和保持访问（Elmrabet 等，2012）。

Reconnaissance

侦察是攻击循环中的第一步，也称为收集攻击，因为它收集目标的信息。侦察主要有两种类型的攻击，称为社会工程和流量分析（Elmrabet 等，2012）。数据包嗅探、钓鱼和端口扫描是侦察攻击的例子。所有这些攻击都针对智能电网系统的机密性。

Scanning

在发动攻击之前，攻击者会扫描智能电网网络中连接的所有设备。扫描的目的是了解网络的强度，并制定攻击计划以针对网络中存在的弱实体。端口扫描、网络扫描和漏洞扫描是扫描中最常见的类型。

Exploitation

利用  是攻击者在智能电网网络中首次建立入口的步骤。在攻击周期的前两个步骤之后，攻击者就有可能渗入网络。攻击者试图通过这一步骤控制网络。中间人攻击、拒绝服务攻击、重放攻击、病毒和蠕虫的攻击、缓冲区溢出和 teardrop 攻击都是利用的示例（Elmrabet et al., 2012）。这些攻击会危及所有的安全目标，包括数据和资源的可用性、信息的保密性以及完整性的违规（Elmrabet et al., 2012）。

维持访问

在攻击生命周期中的最终步骤是维持访问。这一步骤是为了使攻击者永久地访问电网网络。攻击者然后清除所有的数字足迹和痕迹，使系统不会有关于攻击的任何信息。目标只有在攻击启动后才会得知攻击。

## 3.5 用于基于物联网的智能家居的网络安全框架

智能电网基础设施整合了一些基本的安全任务，这些任务旨在提高智能电网对安全攻击的性能（Rehman & Manickam, 2016）。安全技术包括：

+   保密性  : 数据的披露仅向授权人员或系统进行。

+   完整性  : 完整性保证数据的准确性和一致性。

+   可用性  : 可用性确保网络资源（包括数据、带宽、设备等）始终可用。这些资源也受到任何可能威胁的保护，确保其可用性。

+   真实性  : 确保通信双方是它们声称的身份。真实性检查它们发送的消息是否来自经过认证的系统。

+   授权：它指定网络中每个实体的控制权和特权。当用户试图访问系统时，它会检查权限值。

+   不可否认：它确保一个行为无法被否认。非否认提供了不可否认的证据，以验证实体的任何主张的真实性（见图 3.8）。

![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig8_HTML.png](img/504166_1_En_3_Fig8_HTML.png)

图 3.8

智能家居网络安全框架组件

### 3.5.1 智能家居环境的威胁

智能家居由几个连接的物联网设备组成。随着物联网多年来的发展，智能家居现在也变得非常重要。智能家居实现了家庭中所有数字设备的无缝集成，从个人电脑到烹饪炉都包括在内。智能家居将所有这些设备融合在一起，并提供日常监控，有助于高效能源管理。就像物联网一样，智能家居也容易受到来自数字入侵者的多种网络攻击（见图 3.9）。智能家居面临的一些主要威胁包括（Rehman & Manickam，2016）：

+   窃听

+   中间人攻击

+   数据和身份盗窃

+   恶意代码

+   设备劫持

+   分布式拒绝服务（DDoS）

![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig9_HTML.png](img/504166_1_En_3_Fig9_HTML.png)

图 3.9

智能电网威胁

### 3.5.2 智能家居的基于信任的智能安全系统

智能家居是物联网框架中数字设备的组合。当物联网在智能家居中实施时，需要与附属于社交网络的用户进行基于信任的通信。社交物联网（SIoT）帮助智能家居建立社交关系，并为所有参与实体提供基于信任的通信（Chen 等人，2016）。自适应信任管理使用过去的信息计算涉及通信的所有实体的信任，以计算每个节点的当前信任（Chen 等人，2016）。Karmore 等人讨论了基于物联网的人形软件用于识别和诊断 Covid-19 嫌疑人（2020）。信任计算主要集中在信任组成、信任传播和信任聚合（Guo & Chen，2015）。基于信任的安全智能家居通信可以通过在 MQTT 协议顶部加入这三个元素来实现（图 3.10）。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig10_HTML.png](img/504166_1_En_3_Fig10_HTML.png)

图 3.10

基于信任的 MQTT

在 SIoT 网络中，每个节点之间的安全通信可以通过 DTrustInfer 算法（Meena Kowshalya & Valarmathi，2018）建立。智能家居网络可以用图 G（V，E）来表示，其中 V 代表顶点，可以是智能家居中的设备或设备。E 代表图的边缘。在 DTrustInfer 算法中，每个节点在与其他节点通信之前计算可信度评分（Meena Kowshalya & Valarmathi，2018）。在传输之前，每个节点的信任和认证都经过验证。基于信任的 MQTT 协议计算信任，然后遵循提供数据传输双层安全性的 MQTT 协议。在这里，我们集成了机器学习分类器，它有助于对数据的特征进行分类并生成数据的分类模型。我们在这里使用支持向量机（SVM）分类器进行机器学习分类。SVM 分类器在高维数据中工作良好，并且内存效率高（图 3.11）。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig11_HTML.png](img/504166_1_En_3_Fig11_HTML.png)

图 3.11

三层安全的基于信任的架构

### 3.5.3 性能分析

通过对吞吐量、端到端延迟、传输延迟、数据包传递比率、通信能量成本和计算能量成本的比较研究来进行性能评估。所提出的技术与 RF4CE（Han 等，2013）、WAKE（Y W Law 等，2013）和 RLMA（GABA 等，2020）的相关方法进行了比较。图 3.12 显示了所提出方案的通信开销。值得注意的是，与相关技术相比，在传输数据时，所提出的技术实现了最小量的通信开销。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig12_HTML.png](img/504166_1_En_3_Fig12_HTML.png)

图 3.12

通信开销

包交付比率是网络中正确交付的数据包的比率与总交付数据包数量的比率（Chen 等人，2020）。在网络流量拥塞时，数据包交付比率会被最小化。拥塞发生在从发送方到接收方传递数据包时。如果发生拥塞，则数据包始终在发送队列中，并且不会进入活动网络传输过程。高效的流量管理程序将始终具有更高的数据包交付比率。图 3.13 显示，与相关技术相比，提出的技术在模拟时间内改善了数据包交付比率。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig13_HTML.png](img/504166_1_En_3_Fig13_HTML.png)

图 3.13

数据包交付比率

数据包传输的端到端延迟对于提供网络的高效优化至关重要（Chen 等人，2020）。在算法中需要高效的优化以增强网络中的流量控制。网络延迟是通过将数据包传输到目的地时每个中间节点的延迟相结合计算得出的。巨大的延迟将导致网络流量拥塞并产生数据包丢失。图 3.14 展示了提出的技术的端到端延迟。结果显示，与其他相关方法相比，提出的系统的端到端延迟较小。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig14_HTML.png](img/504166_1_En_3_Fig14_HTML.png)

图 3.14

端到端延迟

吞吐量是指在指定的时间段内传递到目的地的数据包的总量。图 3.15 展示了所提出的技术增加了吞吐量的结果。数据传输速度是指在单位时间内通过通信信道传递的数据包数量。它还被测量为在特定时间段内在家庭区域网络中传递的数据位数。图 3.16 描述了所提出的技术与其他相关技术相比具有增加的数据传输速度的实验结果。![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig15_HTML.png](img/504166_1_En_3_Fig15_HTML.png)

图 3.15

吞吐量

![../images/504166_1_En_3_Chapter/504166_1_En_3_Fig16_HTML.png](img/504166_1_En_3_Fig16_HTML.png)

图 3.16

数据传输速度

## 3.6 未来的抗干扰电网

过去几十年来，智能电网的恢复力一直是研究的重点（Das 等，2020）。电网的恢复力是指电网从攻击中快速恢复的能力。今天的电网需要成为一个经济和我们智慧城市的智能电网基础设施。我们大部分的关键基础设施，从医院到通信技术，都在日常生活中依赖于电网。电网的效能以电网的灵活性和健壮性来衡量。一个具有弹性的电力系统应该具有：

+   更好的可靠性，即更少的停电和用户的更少中断。

+   经济实惠，即总建设成本和从故障中恢复的成本应该是可管理的。

+   在停电和故障情况下减少中断时间。

+   对关键能源消费者（医疗和紧急服务）的可管理的电力中断。

+   最小的电力恢复时间。

电网向智能电网的过渡存在几个挑战，其中安全性和可靠性是关键概念领域（Othman & Gabbar，2018）。智能电网中的弹性可以确保电力基础设施安全可持续。电力基础设施可以被完善，有助于经济发展和建设世界一流的首都。

## 3.7 结论

通过整合物联网技术和机器学习算法，传统电网可以变得更智能和灵活。机器学习帮助物联网获得实时洞见，从而帮助智能电网充分发挥作用。利用机器学习技术可以有效消除人为错误并处理大数据。机器学习的真正优势在于识别攻击模式，从而有助于未来对电网攻击的预测。将机器学习与物联网相结合有助于部署容错系统。在基本 MQTT 协议中结合机器学习，并配备信任架构，对每个节点进行认证，通过计算家庭区域网络中每个通信节点的信任分数来完成。信任参数有助于为 MQTT 增加额外的安全层。MQTT 协议提供高效的安全通信，并使用 SVM 分类器创建分类模型。SVM 分类器可以对攻击进行分类，从而识别攻击实体。性能分析表明，所提议的协议在通信开销、数据包传递比、吞吐量、端到端延迟和数据传输速度方面效果更好。未来的工作可以通过实施深度学习策略来使体系结构更加健壮。
