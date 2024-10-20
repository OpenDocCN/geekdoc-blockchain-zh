© 作者，独家授权给 Springer Nature Switzerland AG 2021Y. Maleh 等人（编）未来网络安全应用的人工智能和区块链大数据研究 90[`doi.org/10.1007/978-3-030-74575-2_6`](https://doi.org/10.1007/978-3-030-74575-2_6)

# 移动设备和应用程序的网络安全威胁分类

Mohammed Amin Almaiah^(1  ), Ali Al-Zahrani^(2), Omar Almomani^(3) 和 Ahmad K. Alhwaitat^(4) (1)沙特阿拉伯艾哈萨阿尔法萨利哈大学计算机网络与通信系，邮编 31982(2)沙特阿拉伯艾哈萨阿尔法萨利哈大学计算机工程系，邮编 31982(3)约旦世界伊斯兰科学与教育大学计算机网络与信息系统系，邮编 11947(4)约旦大学计算机科学系，阿曼，约旦 Mohammed Amin AlmaiahEmail: malmaiah@kfu.edu.sa

## 摘要

移动设备和应用程序容易受到各种网络威胁和攻击的影响，从而影响到用户的隐私。因此，有必要深入了解所有网络威胁的特征，以防范其风险。然而，大多数网络威胁分类通常受限于在威胁分类过程中的一两个标准。此外，目前的框架没有提供移动设备和应用程序上网络威胁的详尽列表。基于上述原因，本研究提出了一个详尽的移动设备和应用程序网络安全威胁分类框架，其中包括大多数网络威胁分类和原则。我们框架的主要目的是系统地识别网络安全威胁，展示它们的潜在影响，引起移动用户对这些威胁的关注，并使他们能够采取适当的保护行动。

关键词移动设备移动应用程序网络威胁恶意攻击

## 1 简介

[移动应用程序](https://wiki.example.org/mobile_applications)已经成为进行人类生活活动的一种众所周知和流行的工具，比如在线购物、银行交易等。这种移动应用程序的使用大幅增加导致了网络安全攻击的大幅上升[7, 8, 10]。移动应用程序中的安全问题仍然是许多研究人员关注的严重问题，这是由于移动设备的安全性不足[12, 34, 45]。这使得网络攻击者利用这些漏洞非法访问系统[26]。移动设备在功耗、计算处理和资源方面存在许多限制[36]。移动设备存在许多安全漏洞，可能会给用户和组织带来高风险[59]。移动用户面临着多种安全风险，例如数据丢失、隐私侵犯和财务损失。当恶意攻击利用移动设备操作系统中的漏洞时，这些风险就会发生。移动设备包括许多应用程序，这些应用程序根据其分配的任务收集数据并与其他应用程序共享数据。这些设备在异构环境中的相互连接使它们更容易受到网络安全问题和威胁的影响。因此，网络攻击已经成为一个严重的问题，这促使研究界提出了许多安全解决方案[60]。

网络安全被定义为一种组合，包括用于保护互联网上的应用程序和设备的安全程序、技术、工具和指南[18]。网络安全现在已经成为用户和组织最重要的问题之一，通过保护其资产并通过检测和缓解各种网络威胁和攻击来保护其信息[19]。尽管许多研究人员已经提出了许多对策来解决移动应用程序平台中各种类型的安全问题和问题，但仍然不足以保护移动应用程序免受不断增加的安全漏洞和攻击的影响。因此，保护移动应用程序免受网络攻击和威胁已经成为近年来激励许多研究人员开展更多研究的重要角色[3, 4, 6, 9, 20]。

尽管文献中已经进行了几项研究，用于识别和分类诸如物联网（IOT）[24]、云计算[45]和无线网络[3, 4, 6, 9]等多种技术的网络安全攻击和威胁。这些研究中的每一项都有不同的工具和对策来应对各种安全攻击和侵犯。此外，目前对移动应用程序平台的网络安全威胁的识别和分类的研究有限。威胁分类有助于了解网络攻击的风险和性质，这是有效威胁缓解的重要步骤[11]。因此，本研究旨在：  

1.  (1)

    复习常见的网络安全威胁。

1.  (2)

    复习网络安全攻击。

1.  (3)

    对移动设备和应用程序的网络安全威胁进行分类。

在这项工作中，首先，我们对与移动应用程序以及其他技术（如物联网和云计算）相关的网络安全威胁进行了系统性的审查分析。其次，我们对移动应用程序平台的主要网络威胁进行了分类和识别，第三，我们针对移动技术提出了一些应对措施。在这里，移动技术提供了硬件和软件解决方案来应对移动应用程序的安全挑战，这是一种新颖的方法。为了填补这一研究空白，本文旨在全面呈现网络安全攻击、移动应用程序平台中的威胁以及建议的解决方案。

## 2 移动设备和应用程序的安全

保护移动设备和应用程序免受网络攻击是确保移动用户安全和隐私的关键挑战之一。安全对策应在所有阶段保护数据、信息、硬件和应用程序。拉·波拉等人[31]确定了移动平台领域的三个主要安全问题，包括数据保密性、隐私和信任。

数据机密性被认为是移动设备和应用程序中的基本问题之一 [51]。在移动平台的背景下，如果用户需要访问数据，应首先进行授权，以防止攻击者访问存储在移动设备上的敏感数据。为了实现这一点，需要关注两个重要方面：（1）授权和访问控制以及（2）身份验证。移动设备和应用程序需要能够验证用户或设备身份是否被授权访问数据。授权机制帮助移动设备和应用程序识别移动用户或设备是否被允许访问数据或服务。访问控制机制还确保阻止攻击者访问系统资源。这将在移动设备之间建立安全连接，从而安全地传输用户之间的数据。另一个应该考虑的重要问题是移动设备和应用程序中的身份验证。实际上，这个问题在移动环境中非常关键，因为大量用户和设备需要通过可信赖的方式以安全的方式相互认证。

隐私对于用户、组织和政府而言是移动设备和应用程序中的一个重要问题。在移动平台的背景下，移动设备是相互连接的，敏感数据在互联网上被共享和交换，这使得用户隐私成为移动领域的一个敏感话题。保护移动设备中用户数据的隐私免受网络攻击仍然是许多研究人员的热门话题，并且需要解决 [2, 29, 63]。

## 3 研究方法论

在这项研究中，采取了不同的步骤来对与网络安全威胁和攻击相关的文献进行严格的系统性审查。审查过程是基于 Kitchenham 和 Charters 建立的现有指南 [30] 进行的，其中包括 (1) 确定纳入和排除标准 (2) 确定数据源和搜索策略以及 (3) 数据分析和编码。这项审查被认为是在进行任何研究论文之前的一个重要步骤，它有助于建立知识积累的基础。它还有助于识别之前的研究所错过的领域。以下各小节详细描述了本研究中用于进行系统性审查的步骤。

### 3.1 确定纳入和排除标准

在审查的第一步中，确定了一组纳入和排除标准，这些标准在选择文章时使用。表 1 展示了网络安全威胁研究的纳入和排除标准。表 1

纳入和排除网络安全威胁研究的标准

| 纳入标准 | 排除标准 |
| --- | --- |
| 1\. 包含网络安全威胁的选定研究 | 1\. 排除未关注网络安全威胁的每项研究 |
| 2\. 包含网络攻击方法和技术的选定研究 | 2\. 排除未关注网络安全威胁影响的每项研究 |
| 3\. 包含网络威胁影响的选定研究 | 3\. 排除未关注网络安全攻击技术的每项研究。 |
| 4\. 包含网络威胁类别的选定研究 |   |

### 3.2 确定数据源和搜索策略

在系统文献综述的第二步中，我们通过在以下热门数据库进行搜索收集了大量研究：Google 学术、Wiley、IEEE、ScienceDirect 和 Springer。搜索过程中使用的主要关键词是：（“网络安全” AND “网络安全威胁” AND “网络安全攻击” AND “网络安全技术和方法” AND “网络安全威胁影响” AND “网络安全类别”）。我们通过搜索过程找到了 1522 篇以上的文章，并根据识别的数据库进行了分类，如表 2 所示。然后，我们排除了所有发现的重复项，共计 200 篇文章；因此，收集的项目总数减少到 833。之后，根据表 1 中的标准筛选了剩余的文章。最后，有 91 项研究符合纳入标准，并在分析过程中使用。图 1 描述了本研究的系统综述过程。表 2

来自排名前列数据库的论文分布

| 数据库 | 研究数量 |
| --- | --- |
| IEEE | 33 |
| Springer | 6 |
| Elsevier | 22 |
| Google 学术 | 30 |
| 总计 | 91 |

![../images/507793_1_En_6_Chapter/507793_1_En_6_Fig1a_HTML.png](img/507793_1_En_6_Fig1a_HTML.png)![../images/507793_1_En_6_Chapter/507793_1_En_6_Fig1b_HTML.png](img/507793_1_En_6_Fig1b_HTML.png)

图 1

移动设备和应用程序威胁分类

### 3.3 数据分析与编码

#### 3.3.1 网络安全威胁分类

网络安全威胁被定义为利用系统安全漏洞并对其造成负面影响的任何行为[16]。随着移动设备和应用程序成为现实，大量普及的移动设备增加了网络安全威胁的数量。不幸的是，移动设备带来了一系列新的网络安全威胁。人们越来越意识到新一代移动设备可能会受到恶意软件攻击，并且容易受到攻击。文献中有几项研究根据攻击者利用漏洞的攻击技术对网络安全威胁进行了分类[42, 43, 50]。例如，Tomić和 McCann [54] 将安全威胁分为三个级别：数据安全级别（匿名性和新鲜度）、访问安全级别（可访问性、授权和身份验证）和网络安全级别。同一研究中的研究人员还提到，攻击可以发生在从应用程序层到物理层的所有层次。例如，在应用程序层级别，可以沿通信链路添加恶意攻击以生成假消息和数据，以便攻击正在进行的通信并增加数据碰撞。传输层中的攻击通过发送无限连接请求以最小化节点能量并耗尽其资源，从而导致拒绝服务。在网络层中，其他攻击可以采取几种形式，如欺骗、漏斗、洪水和重放攻击，以创建和发送假消息或在网络中造成拥塞。数据链路层的干扰攻击可以导致信号和数据丢失，破坏通道并增加干扰。在物理层级别，攻击者可以允许未经授权的节点访问网络并破坏网络。Jouini 等人 [42] 进行了信息系统安全威胁分类的文献综述。他们建立了一个用于信息系统安全威胁分类的混合模型。他们将安全威胁分类为三种类型：人为威胁、技术威胁和环境威胁。Otuoze 等人 [43] 提出了基于威胁来源的智能电网安全威胁框架。在该框架中，研究人员将安全威胁分类为技术和非技术资源威胁。技术威胁被分类为基础设施威胁、技术运营威胁和系统数据管理威胁三种类型。而非技术威胁被分类为环境威胁和政府威胁。Singh 和 Shrivastava [52] 将云计算中的安全攻击和威胁分类为四个级别：认证攻击、侧信道攻击、云恶意软件注入攻击和拒绝服务（DoS）攻击。Roman、Lopez 和 Mambo [47] 将移动边缘计算的安全威胁分类为五个资产：（1）网络基础设施威胁，如中间人和拒绝服务攻击，（2）边缘数据中心威胁，如物理损坏、隐私泄露、特权升级和服务操纵，（3）虚拟化基础设施威胁，如拒绝服务、资源滥用、隐私泄露和特权升级，（4）核心基础设施威胁，如隐私泄露、服务操纵、流氓基础设施和（5）用户设备，如信息注入和服务操纵。Abraham 和 Chengalur Smith [1] 通过各种渗透渠道（如电子邮件、社交软件、网站和便携式媒体）确认了社会工程恶意软件的传播。Mosakheil [40] 在他的研究中将区块链技术的安全威胁划分为五类：（1）双重支付威胁、（2）挖矿/矿池威胁、（3）钱包威胁、（4）网络威胁，如 DDoS 攻击，以及（5）智能合约威胁。同样，Homayun 等人 [26] 使用映射研究对常见的网络安全威胁进行了分类，包括网络钓鱼、拒绝服务（DoS）、注入攻击、中间人攻击、会话劫持、SQL 注入攻击和恶意软件（表 3）。

云安全威胁分类

| 文献 | 目标应用 | 方法论 | 研究发现和贡献 |
| --- | --- | --- | --- |
| Tomić 和 McCann [54] | 无线传感器网络 | 文献调查和分析 | 将云计算的安全攻击和威胁分为四个层次：认证攻击、侧信道攻击、云恶意软件注入攻击和拒绝服务（DoS）攻击 |
| Jouini et al. [42] | 信息系统 | 文献综述 | 建立了一个混合模型，用于对信息系统的安全威胁进行分类。他们将安全威胁分为三类：人为威胁、技术威胁和环境威胁 |
| Otuoze 等人 [43] | 智能电网 | 文献综述 | 将智能电网的安全威胁分类为技术和非技术资源威胁。技术威胁分为基础设施威胁、技术操作威胁和系统数据管理威胁三种类型。而非技术威胁则分为环境威胁和政府威胁 |
| Tomić 和 McCann [54] | 无线传感器网络 | 文献调查 | 对可能发生在从应用层到物理层的所有层次的攻击进行了分类。例如，在应用层级别，恶意攻击者可以沿通信链路添加恶意攻击以生成虚假消息和数据，以便攻击正在进行的通信并增加数据碰撞。传输层中的攻击通过发送无限连接请求来最小化节点的能量，并耗尽其资源，从而导致服务拒绝。网络层中的其他攻击可以以多种形式发生，例如欺骗、漏洞、洪水和重放攻击，以创建和发送虚假消息或在网络中造成拥塞。数据链路层的干扰攻击可能会导致信号和数据丢失，并破坏信道并增加干扰。在物理层级别，攻击者可以允许未经授权的节点访问网络并损坏它 |
| Singh 和 Shrivastava [52] | 云计算 | 文献综述 | 将云计算中的安全攻击和威胁分类为四个层次：认证攻击、侧信道攻击、云恶意软件注入攻击和拒绝服务（DoS）攻击 |
| Roman，Lopez 和 Mambo [47] | 移动边缘计算 | 发展 | 将移动边缘计算的安全威胁分类为五种资产：(1) 网络基础设施威胁，如中间人和拒绝服务攻击，(2) 边缘数据中心威胁，如物理损坏、隐私泄露、特权提升和服务操纵，(3) 虚拟化基础设施威胁，如拒绝服务、资源滥用、隐私泄露和特权提升，(4) 核心基础设施威胁，如隐私泄露、服务操纵、流氓基础设施和(5) 用户设备，如信息注入和服务操纵 |
| Mosakheil [40] | 区块链技术威胁 | 发展 | 将区块链技术的安全威胁分为五类：(1) 双重支付威胁，(2) 挖矿/矿池威胁，(3) 钱包威胁，(4) 网络威胁，如 DDoS 攻击，以及(5) 智能合约威胁 |
| Humayun 等人 [38] | 网络安全威胁 | 映射研究 | 使用映射研究对常见的网络安全威胁进行分类，包括钓鱼、拒绝服务（DoS）、注入攻击、中间人攻击、会话劫持、SQL 注入攻击和恶意软件 |
| Mitrokotsa 等人 [37] | RFID 攻击分类 | 文献综述与合成 | 对与射频识别系统相关的威胁进行分类。他们区分了物理层、网络传输层、应用层、战略层和多层的攻击 |
| Abraham 和 Chengalur Smith [1] | 社会工程恶意软件 | 文献综述与合成 | 社会工程恶意软件无处不在且持久存在。强调了组织发展共同社会责任来打击社会工程恶意软件的重要性，而不仅仅依赖技术解决方案。社会工程恶意软件通过各种渗透渠道传播，如电子邮件，社交软件，网站和便携式媒体。 |
| Heartfield 和 Loukas [27] | 社会工程语义攻击 | 调查 | 提出了一个结构化的基线，用于将语义攻击分类为组件，并确定相应的对策 |

### 3.4 网络安全攻击分类

网络安全攻击被定义为通过利用各种技术和工具来利用漏洞从而损害系统或破坏正常运行的任何行为。攻击者发动攻击是为了实现个人满足或获得补偿等目标。网络攻击有多种形式，包括（1）被动攻击，用于监视未受保护的网络通信，以便解密弱加密流量并获取身份验证信息；近距离攻击；内部人员利用漏洞等，以及（2）主动攻击旨在监视未加密的流量以捕获敏感信息。在本节中，我们尝试根据攻击者使用的行为类型来审查网络安全攻击的分类。根据文献，常见的网络安全攻击分类包括：（1）访问攻击，允许未经授权的用户访问网络或设备，例如没有权限访问的智能手机[2，15，23，46]。表 4 总结了网络安全攻击的分类，（2）侦察攻击允许攻击者捕获、发现和映射系统漏洞，例如扫描流量网络、网络端口和 IP 地址信息[2，5，17，49]。 （3）物理攻击，这种攻击旨在篡改硬件设备，例如一些在室外环境中运行的技术，如 IOT 设备可能极易受到物理攻击[23，25，32，55]。 （4）拒绝服务（DoS）攻击允许攻击者使网络或设备服务对其预期用户不可用，原因有很多，如计算资源有限和内存容量低下。这使得移动平台容易受到 DOS 攻击[22，41，44，48]。 （6）基于密码的攻击可以由攻击者以两种方式进行：（1）暴力破解攻击，利用破解工具猜测正确的密码以访问有效密码，（2）字典攻击依赖于尝试多个字母和数字来猜测用户密码[53，62]。 （7）监控与数据采集攻击使用恶意软件如木马来控制系统。移动应用程序容易受到诸如木马病毒等许多网络攻击的影响[2]。 （8）欺骗攻击是基于获取设备的 IP 地址，以便攻击者通过启用攻击者访问用户的机密数据并将其用于恶意目的[28，33，38，39，58]。 （9）僵尸网络攻击是基于一组被入侵并被转让给恶意设备的互联网连接设备的集合，这个恶意设备被称为僵尸网络控制器。僵尸网络控制器能够指导恶意活动以损坏网络或利用用户和数据以获取物质利益[13，14，39]。 （10）Sybil 攻击是一种威胁，攻击者试图获取诚实用户的身份并假装成一个不同的用户，然后尝试与诚实用户建立关系。如果攻击者成功地妥协了诚实用户中的一个，他将获得未经授权的权限，有助于攻击过程[21，57]。表 4

在不同领域的常见网络安全攻击分类

| 网络安全攻击 | 描述 | 上下文 | 文献 |
| --- | --- | --- | --- |
| 访问攻击 | 允许未经授权的用户访问网络或设备，例如没有权利访问的智能手机 | IOT，无线传感器网络，移动设备 | Abomhara 和 Køien [2]; Ashokkumar, Giri 和 Menezes [15]; Damghani 等人 [23]; Rahman 和 Tomar [46] |
| 侦察攻击 | 侦察攻击允许攻击者捕获、发现和映射系统漏洞，例如扫描流量网络、网络端口和 IP 地址信息 | 无人机（UAV），IOT，网络取证和移动应用 | Abomhara 和 Køien [2]; Changsheng [17]; Alabady 等人 [5]; Rizal, Mendoza 和 Gu, [49] |
| 物理攻击 | 这种类型的攻击旨在篡改硬件设备，例如一些技术，如运行在户外环境的 IOT 设备可能极易受到物理攻击 | 智能电网，IOT，移动网络，移动平台 | He 和 Yan [25]; Damghani [23]; Mavoungou 等人 [32]; Van Der Veen [55] |
| 拒绝服务（DoS）攻击 | 拒绝服务（DoS）攻击允许攻击者由于诸多原因（如计算资源有限和内存能力不足）使网络或设备服务不可用于其预期用户。这使得移动平台易受 DOS 攻击影响 | 移动设备，移动自组网，IOT | Farina 等人 [22]; Paul, Chitodiya 和 Vishwakarma [44]; Roland, Langer 和 Scharinger [48]; Nawir 等人 [41]: |
| 针对隐私的攻击 | 通过使用远程访问方法和恶意软件来窥探或窃取用户或组织的敏感信息进行隐私攻击。由于移动设备之间共享大量信息，移动设备的隐私保护变得日益具有挑战性 | 云存储，IOT，移动设备和应用 | Abomhara 和 Køien, [2]; Kang, Wang 和 Shao [29]; Yu, Chen 和 Cai [63] |
| 基于密码的攻击 | 攻击者可以通过两种方式进行基于密码的攻击：（1）使用破解工具进行暴力攻击，以猜测正确的密码以便访问有效密码，（2）字典攻击依靠尝试多个字母和数字来猜测用户密码 | IOT，移动设备 | Shah 和 Venkatesan [53]; Zhang 等人 [62] |
| 监控控制和数据采集攻击 | 监控控制和数据采集攻击使用木马等恶意软件控制系统。移动应用程序易受许多类似木马病毒的网络攻击影响 | IoT | Abomhara 和 Køien [2] |
| 欺骗攻击 | 欺骗攻击是基于获取设备的 IP 地址来攻击用户的，使攻击者能够访问用户的机密数据并将其用于恶意目的 | 移动设备，无人机（UAV），移动云，移动自组网，IOT | Malisa，Kostiainen 和 Capkun[33]；黄等人[28]；莫尔蒂，文卡塔拉曼和拉奥[39]；Mohammadnia 和 Slimane[38]；Visalakshi 和 Prabakaran[58] |
| 僵尸网络攻击 | 僵尸网络攻击基于一组已被入侵并让位给恶意设备（称为僵尸网络控制器）的互联网连接设备。僵尸网络控制器能够指导恶意活动，以损害网络或利用用户和数据获得物质利益（Ali 等人[13，14]；莫尔蒂，文卡塔拉曼和拉奥[39] | IOT，移动云 | Ali 等人[13，14]；莫尔蒂，文卡塔拉曼和拉奥[39] |
| 虚拟身份攻击 | 虚拟身份攻击是一种威胁，攻击者试图获取诚实用户的身份并假扮成不同的用户，然后试图与诚实用户建立关系。如果攻击者成功地 compromise 了其中一个诚实用户，他将获得未经授权的特权，有助于攻击过程中的行动 | 移动 IOT，无线自组网，无线传感器网络（WSN） | 吴和马 61；董等人[21]；瓦苏德瓦和苏德[57] |

## 4 提出的框架

实际上，移动设备和应用程序容易受到各种网络威胁和攻击的影响，这些影响会影响到用户的隐私，因此有必要了解所有网络威胁的特征以防范其风险。然而，大多数网络威胁分类通常受到限制，并且在威胁分类过程中仅基于一两个标准。此外，当前的框架没有提供移动设备和应用程序上所有网络威胁的详尽列表。这些框架可能适用于稳定的技术，但在不断变化的技术领域，如移动技术和 IOT 中，情况就完全不同了，需要持续不断地保护免受网络威胁[64]。

网络威胁分类过程是一个重要的步骤，允许用户、组织和政府了解影响其敏感信息的威胁，并因此提前保护其设备和系统。此外，这一步骤还帮助公司以更少的漏洞开发其移动应用程序[35]。这些威胁可以通过理解现有威胁的行为来识别。不幸的是，现有的分类并未提供关于移动设备和应用程序的网络威胁的详尽列表，并且不支持分类原则[35，56，61]。在这一点上，最佳解决方案是提出一个混合模型，将所有不同的威胁分类组合起来。

鉴于上述原因，我们提出了一个详尽的框架，用于移动设备和应用程序的网络安全威胁分类，包括大多数网络威胁分类和原则。我们框架的主要目的是系统地识别网络安全威胁，展示它们的潜在影响，引起移动用户对这些威胁的注意，并使他们可以适当地采取保护措施。提出的框架中的网络威胁分类是通过文献回顾在上述部分中制定的，如下所示：

+   网络安全威胁源：导致网络威胁的来源，我们确定了两个主要来源：人类和技术。

+   网络安全威胁形式：网络威胁源的起源可以是物理威胁或技术威胁。

+   网络安全威胁动机：攻击者对移动设备和应用程序的目的可以是恶意的或非恶意的。

+   网络安全威胁意图：此标准旨在确定导致威胁的攻击者的意图，这可以分为两类：意外或故意。此外，这个因素有助于理解攻击者的行为，以便理解其意图，从而减轻风险。

+   网络安全威胁类型：在我们的框架中，我们将移动设备和应用程序的网络安全威胁分类为九类：物理访问威胁，操作系统威胁，社会工程威胁，应用程序威胁，身份验证威胁，网络威胁，GPS 威胁和移动设备威胁。

+   网络威胁影响：威胁影响是攻击者在违反移动设备和系统安全之后采取的恶意行为。在我们的框架中，我们确定了最重要的网络威胁影响，如破坏存储在移动设备中的信息，破坏信息，信息盗窃，未经授权披露敏感数据，应用程序的恶意版本，信用卡信息窃取等。

## 5 结论

移动应用程序中的安全问题仍然是许多研究人员关注的严重问题，因为移动设备的安全性不足。这使得网络攻击者利用这些漏洞非法访问系统。本研究旨在更好地了解网络威胁的性质，以建立适当的对策来预防或减轻其影响。我们提出了一个全面的框架，用于移动设备和应用程序的网络安全威胁分类，其中包括大多数网络威胁的分类和原则。我们的框架灵活、动态且多维的，涵盖了移动设备和应用程序上的大多数网络威胁。
