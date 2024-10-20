© 作者，独家许可给 Springer Nature Switzerland AG  2021Y. Maleh et al. (eds.)人工智能和区块链未来网络安全应用 Studies in Big Data90[`doi.org/10.1007/978-3-030-74575-2_10`](https://doi.org/10.1007/978-3-030-74575-2_10)

# 通过用户定义的套接字和随机森林分类器改进的安全入侵检测系统

Garima Sardana^(1  ) 和 Abhishek Kajal^(1  )(1)计算机科学与工程系，古鲁·詹贝什瓦尔科学技术大学，印度希萨尔

## 摘要

研究已考虑入侵检测系统（IDS）来检测和分类入侵、攻击以及不同类型的窃取数据活动。已经考虑了 IDS 系统领域的现有研究。该模型已开发用于发送和接收数据。IDS 系统被提议用于检测、分类带有随机森林算法集成的入侵。套接字编程已用于将数据从发送者传输到接收者。为了保护传输，使用了定义的端口号。此外，通过网络传输的数据将以加密形式进行，以避免数据被篡改或被非法用户访问的可能性。IDS 系统能够追踪不同类别的攻击，因为随机分类器已对攻击进行了分类。

关键词 IDSRandom forest 算法 Socket 编程分类

## 1 引言

随着基于网络的服务和应用的使用日益增加，网络攻击的可能性也在增加。当敏感和重要的用户数据在网络上传输时，内部和外部入侵者可能会尝试攻击或黑客这些数据。攻击者可以使用手动和基于机器的方法来实现这一目的。这些攻击者变得越来越强大和有效。阻止和避免这些攻击者或黑客已成为一个挑战。数据攻击或这些类型的窃取数据被称为网络犯罪，执行这些活动的恶意人员被称为网络攻击者。研究人员或专业团队时常在这一领域工作，并提出创新的、灵活的、更可信赖的 IDS 系统 [1]。

### 1.1 入侵检测系统

入侵捕获模型系统用于检测和分类入侵、攻击以及不同类型的窃取数据活动。此系统用于网络和主机级系统，并在时间上自动运行。根据入侵行为，入侵检测系统在网络和主机级系统之间有所区别。

该系统被视为犯罪警告的形式。让我们举个例子来理解这一点。为了保护家庭免受盗窃，家庭中使用了锁系统。一旦它识别到这种类型的活动，它就会通过响起警报来提醒业主。然而，来自互联网的输入拥塞在防火墙的出口方向上被防火墙过滤掉了。

IDS 硬件库存已经可用。它使用从单个基于主机的 IDS（HIDS）生成的信息。除此之外，它还使用那些利用从整个正常系统段收集的信息的 IDS。

例如，外部用户可以通过调制解调器拨号连接到内部网络。调制解调器在企业个人系统中投入使用。防火墙无法识别这种类型的入口。入侵防止系统成为一种保护和威胁阻止技术系统。它控制系统流量流动以识别并阻止利用弱点。

### 1.2 入侵检测系统的类型

1.  1

    基于主机的入侵检测系统（Host-based IDS）

1.  2

    基于网络的入侵检测系统（Network-based IDS）

1.  3

    混合型入侵检测系统（Hybrid IDS）

**基于主机的入侵检测系统**在本地系统中查看入侵迹象。为了分析检查目的，它们使用与主机系统日志相关的信息。主机管理器被视为传感器。基于主机信息的传感器包括网络和控制器处理产生的其他日志以及未在正常控制器检查和日志记录方法中反映的对象数据。

**基于网络的入侵检测系统**用于检测网络流量。它需要在整个系统中实施传感元件。这种类型的系统需要用于网络的特定部分。它用于分析网络和协议活动。

**混合型入侵检测系统**试图整合所有入侵检测系统的优点，同时消除其漏洞。在这个系统中，传感元件和主机与核心管理或指导阶段进行通信。来自基于网络的传感元件和基于主机的计算机程序收集的数据的引入成为混合型入侵检测系统供应商的最大问题。

### 1.3 随机森林分类器

随机森林（RF）[16]被称为集成分类器（见图 1）。它已经发展成为提高 IDS 系统准确性和性能的方法。这种分类器包括多个决策树。在审查了几种分类器之后，可以清楚地看出，使用 RF 分类入侵的错误较少，这显示了其效率和适用性。这种分类比其他分类器更好。该分类器考虑了多棵树，最小节点大小以及每个节点分割的特征数量。这种分类器有许多优点，例如它保存了生成的森林，可以供将来参考。它还解决了与拟合相关的问题。准确性和变量重要性都可以在不进行任何手动努力的情况下生成。当在随机森林中构建个别树时，使用随机化来选择最佳的节点进行分割。此值等于√A，其中 A 是数据集中的属性数。因此，RF 制定了几个嘈杂的树，这些树会影响准确性和错误决策。![../images/507793_1_En_10_Chapter/507793_1_En_10_Fig1_HTML.png](img/507793_1_En_10_Fig1_HTML.png)

图 1

随机森林分类

在这篇研究论文中，第 1 节介绍了入侵检测系统及其类型。此外，已经介绍了随机森林分类在 IDS 检测中的作用。第 2 节介绍了入侵检测领域的现有研究，而第 3 节专注于问题陈述。第 4 节专注于研究方法论，其中考虑了套接字编程以及客户端服务器传输机制。本节考虑了用户定义端口和预定义端口的概念。入侵第 5 节介绍了用于 IDS 检测的工具，第 6 节讨论了拟议的工作。第 7 节探讨了模拟过程中获得的结果，最后第 8 节呈现了结论。

## 2 文献综述

在 2020 年，Y. Zhou 等人[1] 开发了一个高效的入侵检测系统。在他们的工作中，他们考虑了特征选择和集成分类器。在 2020 年，Y. J. Chew 等人[2] 在系统中应用了决策树，并与系统中的响应大小相配合—依赖入侵检测。他们提出的设计已经在六个比例的 Gure KDDCup，NIDS 记录中得到检验。在 2020 年，宋亚杰和布冰等人[3] 提出了一个新的入侵检测设计。为了实现这个目的，他们结合了网络和硬件。该工作在 CBTC 系统的上等再现基础设备上得到了确认。模拟结果表明该方法实现了 97.64% 的真实正确率。它可以显著提高 CBTC 结构的安全保护水平。在 2019 年，A. Arul Anitha 等人[4] 开发了 ANNIDS: 用于物联网的基于人工神经网络的入侵检测系统。他们讨论了关于物联网的几项研究，这些研究表明人工神经网络（ANN）相对于其他方法具有更高的准确检测率。在 2019 年，A. Khraisat 等人[5] 对入侵检测系统、各种方法、记录和相关问题进行了调查。他们的调查工作提出了当代入侵检测系统的分类法。除此之外，还对值得注意的最近的工作进行了全面回顾。在 2019 年，R. Vinayakumar 等人[6] 开发了一种用于智能入侵检测系统的深度学习原则。他们的研究工作引入了一种新形式的深度学习，即深度神经网络（DNN）。在 2018 年，Meira，Jorge 等人[7] 在网络攻击新颖性检测中提出了相对结果非监督技术。入侵检测在当前时代被认为是一个重要的需求。计算机系统不断成为恶意攻击的受害者。在 2018 年，Kolli，Satish 和 Lilly 等人[8] 考虑了 CSA 在 PTC 中对 DIDS 的支持。铁路公司计划在 2020 年完成 PTC 系统的实施，主要的安全目标是避免列车之间的碰撞、列车事故，并确保铁路工作者的安全。在 2018 年，Clotet 等人[9] 讨论了关键基础设施的工业过程中基于异常的 IDS 的最新不一致性。该工作提出了一个专门用于关键基础设施（CI）工业过程中的实时异常检测系统。在 2018 年，T. Tian 等人[10] 改进了蚂蚁狮子的最大化方法。它的应用也得到了改进。这是在水力涡轮主导的系统中进行的，以识别其参数。在 2017 年，Aleroud[11] 利用附加数据进行互联网攻击的检测。当前的趋势是朝着基于信息的入侵检测系统（IDSs）发展。IDSs 中使用的数据以基地保存信息的形式保存了关于数字攻击和可能的弱点，并利用了这些信息。在 2017 年，Al-Dabbagh 等人[12] 编写了一个给定互联网攻击的入侵检测系统。在这篇文章中，对远程组织控制系统的一种拓扑结构进行了研究，并考察了几种数字攻击情景。在 2017 年，S. M. Alqahtani 等人[13] 在云 IDS 警报和模糊文件夹方面比较了各种组织的方法。在他们的研究工作中，他们使用了通用的分类算法。在 2017 年，S. Mouassa 等人[14] 讨论了蚂蚁狮子优化器来解决电网中理想和敏感能量传输的问题。在 2017 年，B. B. Rao 等人[15] 解释了快速 KNN 分类器用于开发高效的 IDS 系统。他们的工作考虑了一些非常快速的 KNN 分类方法。

## 3 问题陈述

基于机器学习建立的分类器已经存在。当实施此分类器时，将使入侵检测系统的效率更高。但是，与此同时，它也包含一些漏洞。现有系统的执行期需要改进。为此，额外的节点被添加到可用组的方向。除此之外，现有系统无法提供与恶意软件模式和质量相关的完整细节。简而言之，为了提高效率，需要使用最新设备上的复杂模式的 DNN，并借助分布式方法进行训练。

在这项工作中，不使用入侵检测系统记录的标准来训练复杂模式的 DNN。这是因为与复杂模式的 DNN 相关的计算费用是全面的。使用入侵检测系统记录的标准，基于机器学习设计的解决方案引发了许多具有挑战性的问题，如下所述：

1.  1

    设计在入侵大范围的公司中生成了极不准确的鼓舞人心的速度。

1.  2

    设计无法概括，因为在当前的评估中，为了表示设计效率，仅实现了一个单独的记录。

1.  3

    目前的设计检查并不考虑当前的网络连接。

1.  4

    为了维持当前快速增长的网络规模和活动，需要一种不同类型的解决方案。

所有上述具有挑战性的问题成为此研究的主要鼓舞人心之处，其中现有的机器学习分类器的有效性成为主要焦点。然而，现有方法通过捕获网络供应的使用情况生成了极不准确的鼓舞人心的速度。在攻击的标准连接安排中，存在高度低描述和长时间存在的问题。

## 4 研究方法

所提出的工作利用了套接字编程的客户端服务器模型。传输过程中需要 IP 地址和端口号。接收方在接收数据之前需要初始化连接。然后将数据从发送方传输到接收方。入侵检测模型在传输过程中检测和分类入侵者。

客户端-服务器模型

一个系统可以同时启动两个与之相关的请求，但实际上这并不需要。因此，有必要按照一定顺序形成传输网络的应用，以执行指定顺序的强制网络功能，而不是并行功能。主要是服务器执行并保持在此位置，直到获得网络数据包，当客户端执行时，此时任何一方完成主要联系，消费者或服务器都能够交付和接收信息。

IP4 地址

这些地址延伸到三十二位。通常它们以数字的标准形式存在于市场上。所有四个字节，因此存在着三十二位地址的形式，都以整数（零到二百五十五）的形式存在，并通过一个点进行划分。

端口

用于在异常方式下标识套接字的地址，与端口相关的网络服务，相邻规则和数字被使用。由于这个原因，每当一个套接字被形成时，它都与互联网协议地址和端口号进行比较。端口成为计算机程序的对象之一，位于不同需求之间。当主机接收到一个数据包时，它移动到协议堆栈，并最终到达应用层。在数据传输期间，数据包由端口号和 IP 地址组成，数据将在其中传递。端口号 1 到 1023 保留供现有服务使用，但 1024 到 65,535 可供我们的程序使用。

套接字编程

编程已用于两个应用程序之间的通信。此应用程序在两个 Java 运行时环境的设置中运行。Java 套接字相关的编程可能是面向连接的。也可能是在没有连接的情况下进行此编程。套接字和服务器套接字类已被使用。这些用于面向连接套接字的编程。Datagram 套接字与 Datagram 数据包类一起使用。这些用于无连接套接字的编程。在套接字编程中，用户必须知道以下两点：

服务器 IP 地址

1.  1.

    端口号

1.  2.

    套接字类

套接字用于设备之间的通信。套接字类可用于创建套接字。套接字类的几种方法用于创建连接、关闭连接，以及从一个套接字向另一个套接字读取和写入数据。

服务器套接字类

它可以用于制定服务器套接字。它用于与客户端进行通信。以下表格解释了服务器套接字内可用的方法。

重要方法运行此代码需要打开两个命令提示符。每个命令提示符上都会执行每个程序（见图 2）。在客户端代码执行期间，服务器端会显示信息（见表 1）。![../images/507793_1_En_10_Chapter/507793_1_En_10_Fig2_HTML.png](img/507793_1_En_10_Fig2_HTML.png)

图 2

程序输出

表 1

服务器套接字类方法

| 方法 | 描述 |
| --- | --- |
| 公共套接字接受() | 除了在服务器和客户端之间建立连接外，继续套接字 |
| 公共同步 void 关闭() | 停止服务器套接字 |

## 入侵检测中的 5 种工具

公开提供给公众的产品在入侵检测后管理与其安全相关的各种管理目标[2]。此处考虑用于提供安全性的硬件。

SNORT

这是一种可以免费访问的计算机程序。它使用基于规则的语言来定义拥塞。这种语言是可调整的[6]。它以一种可视化检查人类能够检查的格式文件数据包的 Internet 协议地址。它识别许多蠕虫、弱点探测尝试、扫描端口以及其他非法活动。通过不同的预处理器、内容发现和各种规则和法规的检查，所有这些都被识别。

OSSEC-HIDS

它以开源安全的形式而闻名。这是一个可以免费评估的计算机程序。它关注于关键的计算机程序。它使用基于客户端/服务器模型建立的结构。它非常强大，可以轻松地将操作系统日志传送到服务器以进行检查和保存。它已经在执行日志分析、互联网服务提供商、教育机构和信息中心的机器上实施。入侵检测系统用于观察和评估认证日志和防火墙。

FRAGROUTE

它以用于分割的转发设备的形式而闻名。攻击者向碎片路由器发送 Internet 协议的包。然后这些数据包被分解并处理给各方。

HONEYD

它变成了将基本调节器开发成网络的硬件[6]。当这些设施通过主机利用时，允许个体主机在网络计算的支持下要求各种位置。它可以批评基本引擎或跟踪它们的路径[6]。

KISMET

支持移动的入侵检测系统，成为基准。该系统安排在 WIDS 数据包和事件的有用负载内。它将识别入侵者网关。

## 提出的工作

这里介绍的工作包含两个阶段：（1）质量收集（2）组织。在这项工作中，我们采用了一种支持组织所有攻击的一对所有方法。为了识别常规数据集，我们将它们建立为类别一，并将其余攻击建立为类别二。然后，通过射频方法进行质量收集和组织。系统的完整布置显示在图中（见图 3）。

图 3

所提出工作的流程图

## 7 结果与讨论

模拟过程展示了发送方和接收方之间的客户端服务器传输，其中使用用户定义的端口在两个节点之间传输信息。已应用随机森林分类器来对入侵进行分类。

### 7.1 发送方和接收方的客户端服务器设置

这里提出了网络的使用。基于 NetBeans 的集成开发环境。在图中已经突出显示（见图 4）。

图 4

在服务器端，我们已经设计并编写了代码，以启用下载选项并禁用下载选项。

文件接收器模块的设计视图（见图 5）。这里指定了端口号、文件路径和内容解码令牌。

图 5

接收器应用程序的设计视图

### 7.2 发送方实施

文件发送器模块的设计视图（见图 6）。这里指定了端口号、文件路径、接收器的 IP 地址和内容编码令牌。

图 6

在发送方实现上传的代码

运行的应用程序。需要将文本文件从发送方上传到接收方。在下图中显示了 nn.txt 文件（见图 7）。

图 7

运行的应用程序

在执行文件发送方代码（见图 8）时，有必要澄清端口号是否大于 1023。还指定了文件路径和批准令牌。

图 8

运行的应用程序

在执行文件发送模块时，需要用户定义的端口号 6666、文件路径和令牌授权。指定 IP 地址以将文件放置在广播的目标位置（见图 9）。![../images/507793_1_En_10_Chapter/507793_1_En_10_Fig9_HTML.png](img/507793_1_En_10_Fig9_HTML.png)

图 9

文件发送应用

### 7.3 随机森林实现

使用 MATLAB 进行随机森林分类器的模拟，并显示分类结果如图 10 和 11。

图 10

根据生长树的分类误差

![../images/507793_1_En_10_Chapter/507793_1_En_10_Fig11_HTML.png](img/507793_1_En_10_Fig11_HTML.png)

图 11

分类树查看器

≫call_generic_random_forests

混淆矩阵训练数据集测试模块运行后，考虑到各种属性生成混淆矩阵。真实类别显示在 y 轴上，预测类别显示在 x 轴上（图 12）。![../images/507793_1_En_10_Chapter/507793_1_En_10_Fig12_HTML.png](img/507793_1_En_10_Fig12_HTML.png)

图 12

提出模型的混淆矩阵

考虑到上述混淆矩阵图，生成了准确度、精度、召回率值和 f-score 的图表。现有工作的准确度图如下（图 13, 14, 15, 16 和 17）。![../images/507793_1_En_10_Chapter/507793_1_En_10_Fig13_HTML.png](img/507793_1_En_10_Fig13_HTML.png)

图 13

在准确度方面提出的方法和之前方法的比较

![../images/507793_1_En_10_Chapter/507793_1_En_10_Fig14_HTML.png](img/507793_1_En_10_Fig14_HTML.png)

图 14

在准确度方面提出的方法和之前方法的比较

![../images/507793_1_En_10_Chapter/507793_1_En_10_Fig15_HTML.png](img/507793_1_En_10_Fig15_HTML.png)

图 15

在召回率方面提出的方法和之前方法的比较

![../images/507793_1_En_10_Chapter/507793_1_En_10_Fig16_HTML.png](img/507793_1_En_10_Fig16_HTML.png)

图 16

在 f-score 方面提出的方法和之前方法的比较

![../images/507793_1_En_10_Chapter/507793_1_En_10_Fig17_HTML.png](img/507793_1_En_10_Fig17_HTML.png)

图 17

提出模型和之前 IDS 模型的比较

## 8 结论

研究得出结论，随机森林已被证明是一种集成分类器。它能够提高 IDS 系统的准确性和性能。结果表明，这种分类器包含许多决策树。模拟之后，得出结论，使用 RF 对入侵进行分类的错误较少，效率高且适用。所提出的系统更加安全，因为在数据传输过程中使用了用户定义套接字。由于加密和用户定义套接字传输的存在，IDS 攻击的可能性已经降低。在所提出的 IDS 系统情况下，准确性、精度值、召回率和 f-score 都得到了改善。

## 9 未来展望

研究已经集中在提供安全防御，以抵御不同的攻击，如 DOS 攻击和探测攻击。为了提高现有入侵检测系统的效率，新增了一个模型来监控网络中的 DNS 和 BGP 事件。未来的相关研究工作正在分析各种机器学习分类器，以提高 IDS 性能。这项研究工作还介绍了一种基于入侵检测的系统效率增强方法。为此，采用了随机森林分类器。未来的研究人员应该通过计算服务质量参数来评估新技术。
