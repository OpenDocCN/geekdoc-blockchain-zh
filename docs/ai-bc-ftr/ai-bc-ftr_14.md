© 作者，独家许可给 Springer Nature Switzerland AG 2021Y. Maleh 等人（编辑）人工智能和区块链用于未来网络安全应用大数据研究 90[`doi.org/10.1007/978-3-030-74575-2_12`](https://doi.org/10.1007/978-3-030-74575-2_12)

# 基于区块链技术的无线传感器网络中检测恶意攻击的新方案

Mohammed Amin Almaiah^(1  )(1)沙特阿拉伯阿尔阿赫萨阿尔法德国王大学计算机网络与通信系 Mohammed Amin AlmaiahEmail: malmaiah@kfu.edu.sa

## 摘要

无线传感器网络（WSNs）在智慧城市、医疗领域、智能建筑和交通等各个领域工作。这些网络在多个传感器节点、智能设备和收发器之间共享敏感数据。WSNs 环境中的这些敏感数据容易受到各种网络攻击和威胁。因此，需要一种高效的安全机制来处理 WSNs 中的威胁、攻击和安全挑战。本文提出了一种使用启发式、签名和投票检测方法的新方案，利用区块链技术识别出用于检测恶意和安全威胁的最佳对策。在我们的方案中，集群头节点（CN）使用三个检测系统与区块链一起检测恶意传感器节点。此外，CN 使用传感器节点哈希值、节点签名和恶意节点检测的投票度等重要参数来检测 WSNs 中的恶意节点。总的统计结果表明，在我们方案的模拟过程中成功检测和识别了 94.9％的恶意消息。

关键词无线传感器网络区块链技术恶意传感器攻击

## 1 引言

无线传感器网络（WSNs）已经成为敏感数据共享和其他人类生活活动（如智能家居、银行交易等）的一个众所周知和流行的来源。WSNs 的广泛使用大大增加了网络安全攻击的数量。WSNs 中的安全问题仍然是许多研究人员的严重关注点，原因是基础设施的异构性质及其在操作环境中的弱点。这使得网络攻击者可以利用这些漏洞非法访问系统[1]。WSNs 在电源、计算处理和资源有限方面存在几个限制[2]。WSNs 包含数百万个无线传感器节点，这些节点根据其分配的任务收集数据并与其他传感器节点共享。这些设备在异构环境中的互连使其更容易受到网络安全问题和威胁的影响。因此，网络攻击已经成为一个严重的问题，导致了许多研究界的安全解决方案。

网络安全被定义为一种组合，包括安全程序、技术、工具和指南，用于保护互联网上的网络和设备[3]。网络安全是世界各国的一个最为关键的问题之一，通过检测和缓解各种网络威胁和攻击来保护其资产并保障其信息的安全[4]。许多研究人员提出了许多技术来解决无线传感器网络中的多种安全问题和问题。然而，它们仍然不足以保护无线网络免受不断增加的安全漏洞和攻击的影响。因此，保护无线传感器网络免受网络攻击和威胁的影响已成为必不可少的，并促使许多研究人员近年来进行更多的研究。

文献中提出了几种机制和方法，用于检测和缓解无线传感器网络环境下的网络安全攻击和威胁[2]。这些方法中的每一种都具有不同的工具和特性，以应对各种安全攻击和违规行为[5]。在这项工作中，我们对与无线传感器网络相关的主要安全问题进行了概述分析，以确定重大网络威胁，并根据区块链技术提供了解决方案。区块链技术包括硬件和软件解决方案，用于解决无线传感器网络的安全挑战，这是一种新颖的方法。为填补这一研究空白，本文旨在提出一种新的方案，利用启发式、签名和投票检测方法来识别使用区块链技术检测恶意和安全威胁的最佳对策。

区块链网络使用对等网络来记录数据。在对等策略中，所有无线传感器节点都可以同时作为客户端和服务器，因此它们之间进行通信。基于对等方法，在我们的方案中，所有节点都作为对等体进行通信。这意味着每个节点都可以充当发送方和接收方。所有节点与其直接观察者节点共享信息（其邻居节点）的网络中的每个活动。所有消息都应使用非对称加密技术进行签名，以验证成员节点的信息。集群头节点具有网络中所有传感器节点的公钥，以验证成员传感器节点的身份。基于非对称加密原理，网络中的每个节点都有其私钥，只有此节点才能使用其 ID（标识符）对其发送消息进行签名。通过非对称加密，没有一个节点可以以假身份发送信息（块）的报告，这是区块链原则之一。因此，当一个节点观察到另一个节点的异常活动时，它直接报告观察到的情况。该节点使用其签名将此消息作为已签名块记录到区块链系统中，并使用对等网络与其他节点共享。一旦此消息记录在区块链系统中，通过永久的对等存储共享，修改就变得非常困难。如果其中一个节点被劫持，该节点将开始发送伪造信息，但由其正确标识符签名，然后投票技术将检测到其异常活动，如本研究中我们方案的当前实验所示。

在本文中，我们着重介绍了区块链技术的使用机制和解决方案，以解决无线传感器网络的安全挑战，这是一种新颖的方法。这篇论文是最早专注于在区块链技术的光环下分析无线传感器网络安全问题的研究之一，仍然是许多研究人员未来进行更多研究的热门话题。具体来说，我们的研究旨在解决以下研究问题：

区块链技术如何提供更多的安全选项来增强对无线传感器网络的安全性？

论文的其余部分组织如下：2 节包含研究背景。同样，3 节概述了提出的模型。我们方案的实验实施和结果统计在 4 节中讨论。第五部分总结和结束了论文。

### 1.1 研究动机和意义

尽管无线传感器网络（WSNs）具有许多好处，但传感器设备中的安全问题和漏洞仍然是 WSNs 面临的主要挑战 [5]。这个问题可能会让入侵者突破传感器设备的安全性并访问网络。这可能导致窃取敏感信息或损害网络 [6, 7]。因此，为了防止这些安全问题，需要提出有效的安全方案和机制来处理 WSNs 中的安全漏洞。当前的 WSNs 安全方案在能源消耗成本高昂方面仍然存在复杂性 [8]。由于 WSNs 资源有限，在预防和避免恶意攻击方面加入安全特性是一个复杂的挑战 [9, 10]。如果我们利用区块链技术及其解决方案，就可以为 WSNs 提供高级安全性，并同时防止恶意攻击。区块链还可以通过检测恶意传感器节点、路由攻击和入侵检测为 WSNs 提供更好的安全性。如果在 WSNs 中采用区块链技术，那么安全优势将是巨大的。  

## **2 研究背景**

### **2.1 WSNs 中的安全问题**

无线传感器节点单独处理各种网络安全威胁的智能程度不够。因此，需要一个强大的安全机制来帮助无线设备应对网络威胁和漏洞。无线设备在存储安全应用程序方面资源有限，例如小内存。此外，由于其资源有限，如板载电源、内存和处理能力，无线设备容易受到各种威胁的影响。此外，这些设备的结构简单，由小型处理芯片、传感器和收发器组成。由于无线设备的脆弱和简单结构，各种网络攻击（如 DDOS）可能会传播，导致网络问题和设备停止工作。WSNs 还存在其他安全问题，如检测恶意节点、入侵检测和身份验证应予考虑。[11] 将安全问题分为三个级别：数据安全级别（匿名性和新鲜度）、访问安全级别（可访问性、授权和身份验证）和网络安全级别。同一研究[11] 还提到，WSNs 中的攻击可能发生在从应用层到物理层的所有层。例如，在应用层，可以沿通信链路添加恶意节点以生成虚假消息和数据以攻击正在进行的通信并增加数据碰撞。传输层攻击通过发送无限连接请求来最小化节点的能量并耗尽其资源，从而导致服务拒绝。另一种攻击可能在网络层以几种形式发生，如欺骗、虚假目标、洪泛和重放攻击，以创建和发送虚假消息或导致网络拥塞。在数据链路层的干扰攻击可能导致信号和数据丢失，破坏信道并增加干扰。在物理层，攻击者可以允许未经授权的节点访问网络并损害它。其他研究人员还关注了物联网环境中的安全问题以及如何检测安全威胁和漏洞[12–14]。[15] 首次尝试基于区块链技术为 WSNs 设计信任和身份验证方案，并调查区块链在 WSNs 中解决安全问题的适用性。本文旨在提出一种使用启发式、签名和投票检测方法的新方案，以识别使用区块链技术检测恶意和安全威胁的最佳对策。

### 2.2 区块链技术概述

区块链是一种强大的技术，可以通过使用区块链原则，在网络中部署的不同传感器节点之间共享和检查数据，从而提高 WSNs 的安全性[16–18]。在这种情况下，区块链可以被定义为一种分布式和协作的安全机制，用于保证信息的完整性、安全性和安全性。在区块链系统中，数据存储在多个记录中，称为区块。这些信息通过链接分布在网络中的所有区块之间。这些区块之间的链接通过使用密码学机制进行保护，其中每个区块都有前一个区块内容的哈希。基于此，任何记录都无法修改，而不修改所有下一个区块。一个重要的注意事项是，如果链中的任何区块被修改，下一个区块的哈希也将需要被修改，而这种修改还将需要更改即将到来的区块，依此类推。所有这些区块以分布式和去中心化的方式保存在不同的节点中。通过这种方式，除非大多数节点接受并执行更改，否则这些区块中的任何一个都无法更改。因此，数据安全地永久存储在无线传感器网络中。通过这种方式，网络攻击非常难以传播和实施。

区块链可以帮助改善无线传感器网络（WSNs）的安全性，防止恶意攻击，通过共识机制防止恶意活动，并基于其包括数据加密、透明度、不可变性、可审计性和运行韧性在内的底层特性检测数据篡改[19]。此外，区块链特征提供了一个无法渗透的平台，用于包括典型网络网络安全控制、实践和程序。

### 2.3 区块链在 WSNs 中的适用性

区块链原理激发了当前无线网络安全问题的解决方案。每个无线传感器节点都有一个记录传感器节点标识符（ID）的记录列表，这些标识符是根据直接观察节点报告其存在而生成的。这些信息与无线网络一起分布，因此大多数传感器节点必须永久且安全地拥有这些信息。如果恶意节点试图通过插入伪造信息（如虚假哈希键）来修改区块，其他传感器节点将丢弃该信息，因为它们使用了区块链的点对点原理，除非大多数传感器节点都是恶意的。但根据区块链的健壮原理，这种情况不会发生。另一种可能发生的情况是，当一个传感器节点报告其观察到的节点存在异常活动时。在使用区块链系统的无线网络中，这些信息不能被忽略，因为这可能是后来发生的。因此，这些虚假信息可以被引入到传感器节点中分布的区块中。为了解决这个问题，信任策略被用来应对这些情况，通过识别节点的行为、动作和活动，这些行为、动作和活动只被一个直接观察者节点反复报告，基于这个假设，其他几个传感器节点通常会观察到每个活动。还可能发生的另一种情况是，一个恶意节点将忽略对任何其他受损恶意节点的检测等等；但是，通常这些恶意节点也可能被使用信任表的其他节点观察到。

在我们的方案中，检测系统启动之前，所有传感器节点（SN）和集群头节点（CN）都应在区块链系统中注册。每个集群头节点在网络中都有所有邻居节点的公钥列表。每个节点都应对收到的每个消息进行签名，并将其安全地发送给所有邻居节点，以避免被入侵的恶意节点发动恶意攻击。因此，所有节点都可以通过非对称加密[20]对网络上的所有消息进行签名和转发。通过这种方式，无线网络中的每个传感器节点都可以知道其他节点观察到的恶意节点列表。

如果其中一个节点被劫持，该节点将开始发送虚假信息，但由其正确的标识符签名，然后投票方法将检测其异常活动。通过这种方式，每个集群节点都可以通过其他节点的投票结果（恶意或良性）知道已检测到的恶意节点列表，并将结果发送到区块链系统。最后，根据区块链上的投票结果和 CN 上的检测系统，检测系统决定是否消除网络中的可疑节点。

### 2.4 研究贡献

在我们的方案中，为了利用区块链的好处，我们设计了一个私有区块链。在我们的模型中，每个簇首节点（CN）负责对其位置下的参与传感器节点进行身份验证并存储传感器节点的 ID。CN 节点还使用启发式检测系统来计算哈希值并检查它是否在区块链系统上，以便在 WSN 中检测到恶意传感器节点。其次，CN 节点负责通过使用基于签名的系统验证传感器节点的签名。区块链系统中有网络中所有节点签名的列表，并与所有 CN 共享。假设每个传感器节点应对接收到的每条消息进行签名，并将其安全地发送给所有邻居节点，以避免通过簇首节点进行网络攻击。因此，所有节点都可以使用非对称加密签署并转发网络上的所有消息。通过这种方式，每个簇首节点都可以调查签名是否已经存在于区块链系统上。因此，基于区块链上的结果，簇首节点中的签名检测系统可以决定是否删除可疑节点。最后，簇节点可以知道通过其他节点的投票结果（恶意或良性）检测到的恶意节点列表，并将结果发送给区块链系统。根据区块链上的投票结果和 CN 上的检测系统，检测系统决定是否消除网络的可疑节点。

## 3 提出的系统

在本节中，我们介绍了提议方案的概述和方案中的一些假设。然后，我们描述了提议系统中使用的检测系统。接下来，我们通过应用淘汰决策公式计算了恶意程度。最后，我们提出了针对恶意节点大规模投票的对策。

### 3.1 提议方案的概述

在这项工作中，我们提出了一种新的方案，为簇首节点（CNs）分配与区块链系统通信的三个功能。这三个基于三个检测系统的功能分别是（1）基于启发式的系统，（2）基于签名的系统和（3）基于投票的系统，用于检测恶意传感器节点。图 1 展示了我们工作中提出的方案的概述。在这个提出的模型中有三个主要组成部分：![../images/507793_1_En_12_Chapter/507793_1_En_12_Fig1_HTML.png](img/507793_1_En_12_Fig1_HTML.png)

图. 1

提议系统的概述

![../images/507793_1_En_12_Chapter/507793_1_En_12_Fig2_HTML.png](img/507793_1_En_12_Fig2_HTML.png)

图. 2

由簇首节点使用启发式检测系统和基于签名的系统执行的恶意传感器节点检测的流程图

![../images/507793_1_En_12_Chapter/507793_1_En_12_Fig3_HTML.png](img/507793_1_En_12_Fig3_HTML.png)

图. 3

使用启发式检测对 CN 节点的分析结果来检测 WSNs 中的恶意传感器节点

1.  （1）

    传感器节点（SNs）：每个传感器节点由于由电池供电，具有较低的计算能力和内存空间。

1.  （2）

    簇头节点（CNs）：簇头节点具有更多的计算能力，更多的存储空间和更长的通信距离。此外，区块链系统通过预设所有节点的公钥和签名在 CN 中，以在布置网络之前对传感器节点进行认证。它还具有轻量级认证（LAC）以验证区块链系统和簇头节点（CN）之间的认证并交换秘密密钥。

1.  （3）

    区块链：这个可信系统用于初始化传感器节点，并与 CN 共享秘密密钥（SK）。此外，区块链用于以分布方式存储 CN 中传感器节点的认证结果。

对于这个提出的方案，由于网络中分布了大量的传感器节点，我们根据簇头节点的位置将它们划分为不同的组。在我们的方案中，由于传感器节点数量众多且资源有限，所有传感器节点的认证都分布到了每个簇头节点上。然后，每个簇头节点都与区块链系统一起应用轻量级认证（LAC）。区块链系统包括想要消除虚假信息并检测入侵者和恶意节点的传感器节点和簇头节点。假设每个簇头节点都有一个启发式入侵者检测系统和一个基于签名的系统。区块链系统记录了所有良性节点的签名（哈希值）以及所有可疑入侵者和恶意节点的签名和信息。在我们的方案中，在检测过程开始之前，我们有以下假设：

1.  （1）

    所有传感器节点（SNs）都应该在区块链系统中注册。

1.  （2）

    所有簇头节点（CNs）都应该在区块链系统中注册。

1.  （3）

    每个簇头节点都拥有属于簇节点确切位置的所有传感器节点的公钥和签名。

1.  （4）

    每个簇头节点都与区块链共享一个秘密密钥。

1.  （5）

    区块链系统在网络中拥有所有传感器节点的公钥和签名列表。

1.  （6）

    区块链系统有两个列表：（a）良性身份列表和（b）可疑的恶意身份列表。

1.  （7）

    存储在区块链上的敏感数据和信息可以表示为一条记录，以下五个元素代表了该记录：

    +   可疑传感器节点的哈希值。

    +   投票“恶意”的次数。

    +   投票“良性”的次数。

    +   投票“恶意”的传感器节点的地址。

    +   投票“恶意”的传感器节点的地址。

    +   投票“良性”的传感器节点的地址。

“恶意”和“良性”的投票数将用于计算淘汰决策公式（第 4.4 节）中的恶意程度，以决定是否淘汰该节点。 传感器节点地址的记录防止同一传感器节点非法投票超过一次。 在这里，传感器节点地址不是 IP 地址，而是在区块链上使用的地址，例如“0yac46tu874458ef540ade6068dfe2f44e8fc6543”。

在当前方案中，我们假设每个属于区块链系统的集群首节点（CN）安装以下两种入侵检测方法：

**(1) 使用基于启发式方法的恶意节点检测：** 当集群首节点（CN）收到来自传感器节点（SN）的消息时，该系统正在运行。 在当前提案中，假定每个 CN 通过检查消息的哈希值是否已在区块链系统上注册为良性节点标识或疑似恶意节点标识来检测恶意或良性节点。

**(2) 使用基于签名的恶意节点检测方法：** 该技术通过调查区块链系统上是否已存在签名来确保对所有节点的签名进行身份验证。

流程图显示了由 CN 使用启发式检测系统和基于签名的系统执行的恶意传感器节点检测过程（图 2）。

### 3.2 在具有区块链的 CN 上使用启发式检测系统检测疑似恶意节点

当 CN 收到来自传感器节点的消息时，CN 计算哈希值并检查它是否存在于区块链系统中。 如果哈希值不存在于区块链上，则执行启发式恶意检测系统来验证传感器节点的哈希值。 假设启发式或行为检测系统确定接收到的消息是恶意的。 在这种情况下，CN 将节点哈希值发送到区块链系统以共享它，然后淘汰节点并将其存储为疑似恶意节点标识。 当其他节点接收相同的消息时，首先由 CN 验证消息的哈希值是否已在区块链系统上注册为良性节点标识或疑似恶意节点标识。 如果消息的相同哈希值已经存在于区块链系统上的疑似恶意标识列表中，则 CN 上的启发式检测系统判断其为恶意节点并将其移除。

### 3.3 在具有区块链的 CN 上使用基于签名的系统检测疑似恶意节点

相反，如果相同的哈希值存在于良性身份列表中，则通过非对称加密的基于签名的系统执行。这种技术确保了所有节点签名的身份验证。区块链系统具有网络中所有节点签名的列表，并与所有 CN 共享。假设每个传感器节点都应对接收到的每条消息进行签名，并将其安全地发送到所有邻居节点的节点，以避免通过簇头节点进行网络攻击。因此，所有节点都可以使用非对称加密在网络上签署并转发所有消息。通过这种方式，每个簇头节点都可以调查区块链系统上是否已存在签名。因此，基于区块链的结果，簇头节点中的签名检测系统可以决定是否删除可疑节点。此外，区块链系统在所有簇节点之间共享此信息，其中包括所有被怀疑的恶意节点。通过这种方式，每个簇节点都可以知道已通过其他节点的投票结果（恶意或良性）检测到的恶意节点列表，并将结果发送给区块链系统。最后，根据区块链上的投票结果和 CN 上的检测系统，检测系统决定是否消除网络中的可疑节点。

### 3.4 应用消除决策公式

在本节中，我们应用消除决策公式来计算恶意程度。表 1 显示了消除决策公式中使用的一些符号的定义。表 1

在消除决策公式中使用的一些符号的定义

| 符号 | 定义 |
| --- | --- |
| *D*[*m*] | 恶意程度 |
| *T*[*m*] | 恶意程度阈值 |
| *M*[*v*] | 恶意总投票数 |
| *b*[*v*] | 良性总投票数 |
| *T*[*v*] | 总投票阈值 |
| *V*[*r*] | 投票信心率 |
| *S*[*r*] | 自信率 |
| *R*[*d*] | 恶意检测系统的结果 |

正如我们上面提到的，当 CN 的检测系统验证传感器节点的哈希值并发现哈希值存在于区块链记录中时。然后，CN 检测系统可以根据恶意程度的结果，通过使用下面的方程式计算的消除决策公式来决定是否移除可疑节点。

在方程（1）中，当恶意节点的度数*D*[*m*]小于或等于恶意度阈值*T*[*m*]时，结果得到满足；因此，传感器节点不会从区块链网络中移除。![$${\varvec{D}}_{\varvec{m}} \, \le \,{\varvec{T}}_{\varvec{m}}$$](img/507793_1_En_12_Chapter_TeX_Equ1.png)(1)在方程（2）中，当恶意节点的度数*D*[*m*]大于恶意度阈值*T*[*m*]时，结果得不到满足；因此，传感器节点从区块链网络中移除。![$${\varvec{D}}_{\varvec{m}} \, &gt; \,{\varvec{T}}_{\varvec{m}}$$](img/507793_1_En_12_Chapter_TeX_Equ2.png)(2)当***M***[***v***]** + *****b***[***v***]** ≥ *****T***[***v***]**时：检测系统仅使用区块链上的投票结果，并使用方程（3）计算恶意度。![$${\varvec{D}}{\varvec{m}}=\frac{{{\varvec{M}}}_{{\varvec{v}}}}{{{\varvec{M}}}_{{\varvec{v}}}+{{\varvec{b}}}_{{\varvec{v}}}}$$](img/507793_1_En_12_Chapter_TeX_Equ3.png)(3)CN 检测系统使用方程（4）计算恶意度，区块链上的投票结果以及其通过启发式或基于签名的方法得到的恶意检测结果。在此，假设当传感器节点恶意时，恶意检测系统输出 1，当传感器节点良性时，输出 0。即，*R*[*d*]* ∈ {*0*,* 1*}*。![$${\varvec{D}}{\varvec{m}}=\frac{{\varvec{M}}{\varvec{v}}}{{{\varvec{M}}}_{{\varvec{v}}}+{{\varvec{b}}}_{{\varvec{v}}}}\times {{\varvec{V}}}_{{\varvec{r}}}+{{\varvec{R}}}_{{\varvec{d}}}\times {{\varvec{S}}}_{{\varvec{r}}}$$](img/507793_1_En_12_Chapter_TeX_Equ4.png)(4)其中*V*[*r*]和*S*[*r*]由以下方程计算：![$${\mathbf{V}}_{\mathbf{r}}=\frac{{\mathbf{M}}_{\mathbf{v}+{{\varvec{b}}}_{{\varvec{v}}}}}{{\mathbf{T}}_{{\varvec{\upnu}}}}$$](img/507793_1_En_12_Chapter_TeX_Equ5.png)(5)![$${\textbf{S}}_{\textbf{r}} = {\textbf{1}} - {\textbf{V}}_{\textbf{r}}$$](img/507793_1_En_12_Chapter_TeX_Equ6.png)(6)例如：假设传感器节点向集群头节点发送消息，并在区块链上为传感器节点的哈希值投票为 10 个“恶意”票（*M*[*v*] = 20）和 5 个“良性”票（*b*[*v*] = 5）。此外，CN 中的恶意检测系统判断传感器节点为恶意（*R*[*d*] = 1），总票数的阈值设为 20（*T*[*v*] = 20），恶意度的阈值设为 0.5（*T*[*m*] = 0.5）。此示例中的恶意度*D*[*m*]计算如下：![$${\varvec{D}}{\varvec{m}}=\frac{10}{10+5}\times\frac{10}{10+5}+{1}\,{\times }\,\left(1-\frac{10+5}{20}\right)=\frac{3}{4}$$](img/507793_1_En_12_Chapter_TeX_Equa.png)

根据 *D*[*m*] 的结果，由于 Dm 的值大于恶意程度的阈值 (![$$\frac{3}{4}&gt;0.5$$](img/507793_1_En_12_Chapter_TeX_IEq1.png))，传感器节点将从区块链网络中删除。

## 4 实验分析与结果

所提出的方案是使用 OMNeT++  软件在仿真环境中实现的。OMNeT++ 被认为是在仿真环境中开发无线传感器网络的常用工具，这一观点在无线网络文献中有所体现。所提出的方案通过指定具有网络拓扑顺序的簇头节点 (CNs) 的传感器节点 (SNs) 的分布来执行。此外，我们创建了一个与簇头节点 (CNs) 通信连接的私人虚拟区块链。为此，我们安装了 Geth，一个以太坊客户端，并通过 Python 脚本与 Geth 进行交互。在具有与传感器节点连接的簇头节点 (CNs) 中设置了仿真参数。此外，分配给 CN 节点的功能是检测网络中的恶意传感器节点，例如通过对每个传感器节点的哈希值、传感器节点的签名、恶意程度 (*D*[*m*]) 和对恶意的总投票数 (*Mv*) 进行评估来检测劫持节点。所提出的方案中使用的仿真参数如表 2 所示。表 2

无线传感器网络仿真设置

| 仿真参数 | 值 |
| --- | --- |
| 仿真工具 | OMNeT++  |
| 仿真环境 | 800 × 800 |
| 传感器节点数 *SNi* | 50, 100, 200, 400, 600,800 |
| 簇头节点数量 | 6 |
| 恶意节点数量 | 100, 200, 300, 400, 500 |
| 良性节点数量 | 100, 200, 300 |
| 传输范围 | 150 M |
| 数据包大小 | 256 Kbps |
| CN 的传输间隔 | 30 s |
| 良性节点传输时间间隔 | 10 s |

### 4.1 基于启发式检测系统的 CN 功能结果分析

对于 CN 节点功能的仿真结果观察到，通过计算哈希值并通过区块链系统验证以检测恶意传感器节点的提出方案的性能可靠性。通过使用启发式检测系统进行 CN 和区块链检测和识别恶意传感器节点的结果统计发现相当一致和引人注目。CN 节点被确定用于检测和识别，在这里，恶意节点向网络中的 CN 节点发送了一条假消息。同样，这条消息也被 CN 节点接收到。CN 节点执行必要的安全验证流程，将节点哈希值与区块链系统中的哈希值进行匹配。结果表明，此传感器节点未通过匹配其值来验证哈希值的安全条件。之后，CN 节点将节点哈希值发送到区块链系统以共享它，然后将其消除并存储为疑似的恶意节点身份。此外，区块链生成警报消息以确认网络中存在恶意节点。模拟结果验证了具有区块链的 CN 节点成功识别了网络中的恶意节点。这验证了基于哈希值评估的 CN 节点检测恶意节点的准确率在无线传感器网络中针对假消息完全准确。随后，在部署的 WSN 基础设施中增加了恶意传感器节点的数量，以验证具有许多假消息的性能可靠性，这对于 CN 节点也被发现相当特殊。CN 节点检测到其位置的最大数量的假消息，其统计数据显示在图 5 中。

### 4.2 基于签名的系统的 CN 功能的结果分析

我们提出的模型的结果还基于基于签名的系统对 CN 功能进行了评估，该方法通过区块链系统确保所有节点的签名被 CN 正确验证。在模拟中，我们使用恶意节点发送具有假签名的消息。在这种情况下，假消息中的哈希值和传感器节点 ID 与良性节点保持相似，但对所有引入的恶意节点的签名不同。在模拟过程中，CN 节点已检查了对所有恶意节点签名的伪造进行评估，通过使用区块链系统评估网络中传感器节点的签名，发现这一点相当引人注目。此外，在基于签名的系统的 CN 节点的模拟期间观察到的统计分析如图 4 所示，其中以图形形式呈现了在模拟过程中捕获的恶意节点签名检测。![../images/507793_1_En_12_Chapter/507793_1_En_12_Fig4_HTML.png](img/507793_1_En_12_Fig4_HTML.png)

图 4

使用基于签名的系统分析 CN 节点结果，以检测 WSN 中的恶意传感器节点

![../images/507793_1_En_12_Chapter/507793_1_En_12_Fig5_HTML.png](img/507793_1_En_12_Fig5_HTML.png)

图 5

使用投票系统分析 CN 节点结果，以检测 WSN 中的恶意和良性传感器节点

### 4.3 基于投票系统的 CN 功能对恶意或良性传感器节点的结果分析

CN 结果还被用于检测操作网络中的恶意或良性传感器节点。如果其中一个节点被劫持，该节点将开始发送假信息，但由其正确标识符签名，然后投票方法将检测到其异常活动，如本研究中的当前实验所示。这样，每个集群节点都可以通过其他节点的投票结果（恶意或良性）知道已检测到的恶意节点列表，并将结果发送到区块链系统。最后，根据区块链上的投票结果和 CN 上的检测系统，检测系统决定是否消除网络中的可疑节点。从模拟工具提取的统计分析显示在图 5 中，其中恶意和良性节点都在网络中广播消息。然而，CN 直接从传感器节点接收到的正确消息也通过基于恶意程度（*D*[*m*]）的投票系统进行评估。使用投票系统捕获的恶意节点的伪造消息的统计结果分析显示在图 5 中（图 3）。

### 4.4 基于启发式检测系统、基于签名的系统和投票系统的 CN 功能结果分析

在模拟中，将三个检测系统组合后评估了提出的方案的整体检测率，以评估恶意节点的整体检测率。整体结果统计表明，在我们的方案模拟期间，94.9%的恶意消息被成功检测和识别，如图 6 所示。![../images/507793_1_En_12_Chapter/507793_1_En_12_Fig6_HTML.png](img/507793_1_En_12_Fig6_HTML.png)

图 6

WSN 中恶意消息的整体检测率

## 5 结论

在这项研究中，提出了一种基于区块链的启发式、签名和投票方法的新方法，用于检测无线传感器网络的恶意攻击。所提出的方案将通过最小化网络资源利用来对抗已部署的 WSN 中的恶意传感器攻击。所提出的方案使用三个基于区块链技术的功能来确保网络的安全，并为 WSN 维护安全的通信基础设施。所提出的方案的三个功能相互支持，以更精确地识别网络中的恶意攻击。类似地，这些功能在网络中独立工作，但是认证机制相互支持，以高速识别恶意攻击。在第一个功能中，CN 节点执行启发式恶意检测系统来验证传感器节点的哈希值。假设启发式检测系统确定接收到的消息是恶意的。那么，CN 将节点哈希值发送到区块链系统以共享它，然后消除节点并将其存储为可疑的恶意节点标识。第二个功能是基于签名的方法。如果相同的哈希值存在于良性身份列表中，则执行基于签名的系统，通过非对称加密。这种技术确保了所有节点签名的认证。区块链系统具有网络中所有节点签名的列表，并与所有 CN 共享。假设每个传感器节点应该对接收到的每条消息进行签名，并安全地发送到所有邻居节点，以避免通过簇头节点进行网络攻击。因此，所有节点都可以使用非对称加密对网络上的所有消息进行签名和转发。通过这种方式，每个簇头节点可以调查区块链系统上是否已存在签名。因此，基于区块链的结果，簇头节点中的签名检测系统可以决定是否删除可疑节点。投票方法是第三个功能，在其中一个节点被劫持时，节点将开始发送虚假信息，但由其正确标识符签名，然后投票方法将检测其不正常的活动。通过投票结果（恶意或良性）由其他节点检测到的恶意节点的列表，每个簇节点都可以知道，并将结果发送给区块链系统。根据区块链上的投票结果和 CN 上的检测系统，检测系统决定是否消除网络的可疑节点。最后，我们进行了模拟实验；总体实验结果表明我们的方案可以有效抑制传感器节点的恶意攻击。