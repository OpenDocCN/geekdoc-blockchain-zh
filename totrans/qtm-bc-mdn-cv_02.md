© 作者（们），独家许可给 Springer Nature Switzerland AG 2022A. Kumar 等人（编辑）：《量子和区块链用于现代计算系统：愿景和进展》数据工程与通信技术讲义 133[`doi.org/10.1007/978-3-031-04613-1_2`](https://doi.org/10.1007/978-3-031-04613-1_2)

# 量子技术 II：密码学、区块链和传感

Anant Sharma^(1  )，Achintya Paradkar^(2  ) 和 Vinod N. Rao^(3)（1）印度普纳费格森学院，印度普纳（2）瑞典哥德堡查尔莫斯科技大学（3）印度班加罗尔波恩普拉吉纳科学研究所 Anant Sharma（通讯作者）Email: anantsharma2410@gmail.comAchintya ParadkarEmail: achintya@chalmers.se

## 摘要

本章进一步强调了量子技术的方面，基于前一章中处理的量子信息的基础。简要回顾了两个主要的量子信息处理任务，即量子通信和量子传感。量子通信又分为量子密码学和量子区块链。在量子密码学中，对量子加密系统中安全性的特征进行了评论。量子区块链包括了见证量子领域中的去中心化、分布式和公共数字分类帐的框架的性质和网络。最后，介绍了从由量子力学描述的粒子/系统（如光子）中产生的量子传感的出现。

## 1 量子通信

量子通信时代始于 20 世纪 80 年代初，当时科学家开始考虑使用量子态作为信息载体。直到那时，量子力学的基础方面才是社区的主要关注点。尽管早期的一些工作表明了这样一个前景的可能性，但量子通信领域直到 1984 年贝内特和布拉萨德提出了密钥分发和硬币抛掷协议后（因此得名“BB84”）才引起了极大的关注。BB84 协议基于共轭编码的想法，这个想法几年前由韦斯纳首次观察到。本章的主要单元主要关注量子通信的两个方面，即量子密码学和量子区块链。前者处理系统（量子位）中的信息以及与之相关的保密性。量子密码学仍然是一个巨大的探索领域，涉及到众多的两方或多方方案的研究和调查。在本书中，我们将限制讨论量子密钥分发协议，特别是基于反事实的协议。但是将简要总结一些其他密码学任务。本单元的后半部分将涵盖使用量子位的区块链技术的阐述。这一部分主要解决与量子系统相关的网络和共享问题以及相关的概念性问题。尽管经典区块链技术提供了各种功能，并且其近年来的发展非常有前景，但量子对应技术值得追求它自身的优势。首先，对量子区块链技术的研究将影响其他网络是至关重要的领域（例如：量子互联网）。

现有工作安排如下。 第一部分 包含了量子通信的介绍，接着是第二部分 的量子传感。特别是，第一部分 包括两个主要部分——量子密码学和量子区块链。在 第 1.2.1 节 简要介绍了量子密码学，随后的子节包括量子反事实性（第 1.2.2 节），反事实安全性的最新进展（第 1.2.3 节 和 第 1.2.4 节），最后以量子反事实 QKD 协议的实验版本简要描述（第 1.2.5 节 和 第 1.2.6 节）。 第 1.3 节 包括区块链技术的介绍，并对比了经典和量子区块链的差异（第 1.3.6 节 和 第 1.4 节），同时提供了在 IBM Q Experience 中演示的示例（第 1.5.1 节 和 第 1.6 节）。最后，第二部分 讨论了量子传感的需求和优势，考虑了某些系统作为量子性源的情况。对其限制、挑战（第 2.3 节）和应用（第 2.4 节）做出了简要观察。

### 1.1 引言

无论任何类型的信息，自古以来对社会都有巨大价值。信息的价值通常取决于三个因素：相关性、可重复性（或准确性）和进展范围 [1]。这里的“信息”一词指的是了解某事物的结果；或者说是知识。因此，验证信息的重要性与信息本身一样大。

影响信息的第四个因素是保密性。许多信息只要是秘密的就是相关的。保密性的需求并不新鲜。我们有过使用信鸽传输秘密信息的日子，一些标准的加密方法，甚至经常涉及人类的参与。大约三个世纪前，数学家们找到了一种有组织的加密和解密方法——由一些数学定理保证的保密性。在信息时代的出现之后（大约一个半世纪前），传统的编码-解码方法被更好的协议所取代，这些协议潜在地使用了一些非线性数学模型来保证安全性。

名称‘密码学’来自两个希腊单词，‘kryptos’表示秘密或隐藏，‘graphein’表示写作或研究。它可以被定义为对秘密通信技术/方法的实践和系统研究。从一个参与方发送到另一个参与方的信息必须受到保护，以防泄露给至少与通信参与方一样强大和高效的对手。因此，信息的保密性至关重要，因此需要寻求更好的技术，以抵御更强大的对手。

典型的密码学方案包括两个参与方，‘Alice’（编码状态的发送方）和‘Bob’（解码状态的接收方），他们希望在‘Eve’（窃听者）或不受信任的参与方存在的情况下执行密码任务。经典密码学涉及一个基于某些数学问题的计算复杂性的密码任务。一个典型的例子是使用大数的因子化困难。

在加密方案中，明文（例如：一条消息）被转换为编码格式，即密文，通过不安全的经典通信渠道从艾丽丝传输到鲍勃。鲍勃解码密文并获取原始明文。一串称为“密钥”的比特在编码和解码明文时都被使用，根据密钥的性质，可以有两种广泛的分类：

1.  1.

    对称（或秘密密钥）密码学：编码和解码密钥是相同的。

1.  2.

    非对称（或公钥）密码学：编码密钥不同于解码密钥。

这里的一个固有假设是，艾丽丝和鲍勃在执行任务之前至少会见一次，并因此分享各自的密钥。这是一个合理的假设，因为艾丽丝和鲍勃需要沟通，他们至少应该曾经见过一次以建立身份。因此，最初的密钥共享足以在以后的任何时间点执行任意数量的加密任务（因为他们都可以使用上一次运行的部分秘密消息作为下一次运行的密钥）。

一些经典的加密技术包括：

+   凯撒密码：一种简单的替换密码，其中特定字母被其后第三个字母替换。其他移位和替换密码都可以归类为这一类。

+   杰斐逊密码：一组圆盘（每个圆盘上有 26 个字母），依次放置，并且密文对应于前一个或后一个圆盘中的字母。

+   普莱菲尔密码：所有字母都被表示为矩阵的元素，并且明文中的字母被矩阵的对角线或反对角线元素替换。

+   RSA 算法：两个质数相乘，乘积是公钥的一部分。私钥由唯一的模运算操作生成，并且使用私钥和公钥的一部分进行解密。

还有许多其他的加密技术，如一次性密码本和哈希函数，在许多其他作品中都有讨论。古典密码学的局限性在于其安全性是通过解决数学问题的困难性（因此只有'计算安全性'）来保证的。量子密码学的优势在于其安全性是由量子力学原理保证的，因此可能具有“无条件安全性”的可能性。

### 1.2 量子密码学

#### 1.2.1 介绍

量子密码学（QC）涉及与古典密码学中完全相同的情况，但是爱丽丝和鲍勃是量子启用的，夏娃也是。具体来说，爱丽丝、鲍勃和夏娃可以访问量子系统，可以执行量子操作并通过量子信道进行通信。每个人的详细情况在前一章中介绍过。因此，爱丽丝和鲍勃（以及夏娃）有两个信道；经过身份验证的经典信道和不安全的量子信道。特别是，从爱丽丝发送到鲍勃（反之亦然）的消息在前者可以被任何人监听，但不能被更改，在后者，任何人都可以攻击和更改消息。有关 QC 的概述，请参阅此处 - [4]。

QC 领域起步于 1984 年，当时贝内特和布拉萨德提出了一个基于共轭编码的密钥分发协议[5]（因此得名‘BB84’），其基于想法生成对称密钥的爱丽丝和鲍勃，这个密钥可能在未来用于发送秘密消息。这种在两个或多个方之间生成秘密密钥的协议通常称为量子密钥分配（QKD）协议。下面列出的步骤是 BB84 协议（图 1），以及随后的示例（表 1）。

1.  (1)

    Alice 生成一串光子（量子比特），分别在直线基础（{![$$\boldsymbol{\uparrow }$$](img/516210_1_En_2_Chapter_TeX_IEq1.png), ![$$\boldsymbol{\downarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq2.png)}，用 ‘**+**’ 表示）或对角基础（{![$$\boldsymbol{\leftarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq3.png), ![$$\boldsymbol{\rightarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq4.png)}，用 ‘![$$\boldsymbol{\times }$$](img/516210_1_En_2_Chapter_TeX_IEq5.png)’ 表示）。她将它们依次发送给 Bob。

1.  (2)

    Bob 选择用其中一种基础测量每个光子。如果他的选择与 Alice 的基础相匹配，就生成一个秘密密钥位。

1.  (3)

    Alice 和 Bob 通过一个经典通道宣布各自的基础，并形成一个匹配基础的实例密钥。这称为筛选。

1.  (4)

    在筛选密钥位子的子集上，他们通过宣布各自光子的极化来估计信道中的错误。

1.  (5)

    如果观察到的错误率超过阈值限制，Alice 和 Bob 中止协议。否则，他们继续进行首先进行错误校正的后处理，然后进行隐私放大，这两者都是经典技术，以获得更小、更安全的密钥。

![](img/516210_1_En_2_Fig1_HTML.png)

图 1

代表 BB84 协议的一个块图。这里的 ‘S’ 是带有 Alice 的源，‘D’ 是带有 Bob 的检测仪器。

表 1

上表是从 BB84 协议生成秘密密钥的示例

| Alice 的比特 | 1 | 0 | 0 | 1 | 1 | 1 | 0 | 0 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 爱丽丝的基 | **+** | **+** | ![$$\boldsymbol{\times }$$](img/516210_1_En_2_Chapter_TeX_IEq6.png) | **+** | ![$$\boldsymbol{\times }$$](img/516210_1_En_2_Chapter_TeX_IEq7.png) | ![$$\boldsymbol{\times }$$](img/516210_1_En_2_Chapter_TeX_IEq8.png) | ![$$\boldsymbol{\times }$$](img/516210_1_En_2_Chapter_TeX_IEq9.png) | **+** |
| 爱丽丝的极化 | ![$$\boldsymbol{\uparrow }$$](img/516210_1_En_2_Chapter_TeX_IEq10.png) | ![$$\boldsymbol{\downarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq11.png) | ![$$\boldsymbol{\leftarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq12.png) | ![$$\boldsymbol{\uparrow }$$](img/516210_1_En_2_Chapter_TeX_IEq13.png) | ![$$\boldsymbol{\rightarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq14.png) | ![$$\boldsymbol{\rightarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq15.png) | ![$$\boldsymbol{\leftarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq16.png) | ![$$\boldsymbol{\downarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq17.png) |
| 鲍勃的基 | **+** | ![$$\boldsymbol{\times }$$](img/516210_1_En_2_Chapter_TeX_IEq18.png) | ![$$\boldsymbol{\times }$$](img/516210_1_En_2_Chapter_TeX_IEq19.png) | ![$$\boldsymbol{\times }$$](img/516210_1_En_2_Chapter_TeX_IEq20.png) | **+** | ![$$\boldsymbol{\times }$$](img/516210_1_En_2_Chapter_TeX_IEq21.png) | **+** | **+** |
| Bob 的测量 | ![$$\boldsymbol{\uparrow }$$](img/516210_1_En_2_Chapter_TeX_IEq22.png) | ![$$\boldsymbol{\rightarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq23.png) | ![$$\boldsymbol{\leftarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq24.png) | ![$$\boldsymbol{\leftarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq25.png) | ![$$\boldsymbol{\downarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq26.png) | ![$$\boldsymbol{\rightarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq27.png) | ![$$\boldsymbol{\uparrow }$$](img/516210_1_En_2_Chapter_TeX_IEq28.png) | ![$$\boldsymbol{\downarrow }$$](img/516210_1_En_2_Chapter_TeX_IEq29.png) |
| 公开讨论 |   |   |   |   |   |   |   |   |
| 秘钥 | 1 |   | 0 |   |   | 1 |   | 0 |

如果窃听者 Eve 尝试测量 Alice 发送的光子，她必然会选择其中的一个或两个基础来进行测量。但正如我们在上表中看到的那样，如果她选择了错误的基础，她将会发送具有随机极化的光子。换句话说，Eve 可用的状态是非正交的，她无法完全区分它们。此外，她也无法简单地‘复制’一个状态然后稍后测量，因为无复制原理限制了她这样做。因此，当 Alice 和 Bob 在通道中测试错误时，她将会被发现。

QKD 是一种特定的加密任务，其中秘密密钥在两个或多个参与方之间共享，并通过测试量子力学的特定定律来验证安全性。还有许多其他涉及两个或多个参与方的量子加密方案。显然，特定方案中的保密性将基于方案的社会结构。除了 QKD 外，还列出了一些其他量子加密方案，详见表 2。然而，量子加密的应用范围并不仅限于这些协议。Table 2

这里的 A 和 B 是 Alice 和 Bob。给出的示例都是基于量子的方案。Eve 角色的相关性对于特定协议是独特的。她要么是相关的（如直接通信和 QRNGs），要么一个或多个参与方可能不信任（其他列出的协议）

| 协议 | 目标 | 示例 |
| --- | --- | --- |
| 直接通信 | A 和 B 直接通过编码极化来进行通信 | 乒乓协议 |
| 随机数生成器 | 随机性在 A 和 B 之间共享 | 光学 QRNG 和纠缠 QRNG |
| 位承诺 | A 向 B 承诺一个位，她以后无法更改 | Lo 和 Chau 的 QBC |
| 秘密分享 | A 在两个或多个方之间分享一个秘密，以便没有单个个体可以知道它 | Buzek 的协议 |
| 数字签名 | A 用她的签名签署数字文档，可由其他方验证 | Gottesman & Chuang 的协议 |
| 多方计算 | 多个方希望计算一个函数，每个输入都是私密的 | 量子投票 |

**窃听**：Eve 的角色和主观安全威胁是许多量子计算方案中的主要关注点。因此，这些量子计算协议的目标是使 Alice 和 Bob 能够在假定 Eve 攻击量子通道的情况下进行通信。Eve 被假定攻击的标准方法包括但不限于：

+   拦截并转发—IRUD（拦截-重发非歧义识别）是一种通用但重要的攻击，Eve 用自己的量子比特替换原始量子比特。她必须在通道中引入错误（无法克隆定理），但获取部分信息。

+   光子数分裂—如果协议涉及单个时间点的多个光子，那么 PNS 是一种强大的攻击。Eve 移除一个光子并获取信息，而其余光子到达 Bob。

+   探测攻击—Eve 将她的粒子与量子比特纠缠起来，然后稍后测量她的粒子以获取信息。产生的误差取决于纠缠的强度。

+   拒绝服务 — Eve 试图通过过载系统或截取传输线来干扰通信。

+   木马 — Eve 使量子比特经历一种使 Bob 站点上的测量变得难以理解的功能。这方面的一个例子是中间人攻击。

Eve 可能通过许多其他攻击潜在地窃听量子比特的信息。广义上，她的攻击可以分为：(a) 相干攻击 和 (b) 非相干攻击。在前一种情况下，Eve 对多个量子比特进行攻击，并获得平均信息。在后一种攻击（也称为个体攻击）中，Eve 攻击每个量子比特并获取信息。前者可以进一步划分为：(![$$\cdot $$](img/516210_1_En_2_Chapter_TeX_IEq30.png)) 联合攻击 — Eve 按顺序攻击一组量子比特并获取信息; 和 (![$$\cdot $$](img/516210_1_En_2_Chapter_TeX_IEq31.png)) 集体攻击 — Eve 使用更高维度的探针攻击所有量子比特并获取信息。

如表 2 所示，不同类型的通信方案都属于 QC 的范畴。本章将限制进一步讨论到量子密钥分发协议。具体来说，将讨论反事实量子密钥分发协议的各种版本以及该领域的最新进展。

#### 1.2.2 反事实性

尽管 BB84 是首个提出的量子密钥分发协议，但在短时间内提出了许多其他协议[7–10]。每个协议都基于非正交状态或纠缠量子比特。一般来说，到目前为止提出的 QKD 方案可以大致分为两类：

1.  (1)

    准备和测量协议。

1.  (2)

    基于纠缠的协议。

基于正交和非正交状态的量子密钥分发（QKD）协议形成准备和测量方案的两个子部分。本章的主要目的将集中在基于正交状态的协议上。特别地，本章将概述其基本工作原理是无交互量子测量（IFM）的 QKD 协议。IFM 的概念是在 EV 协议[11]中提出的，其中使用马赫-泽德干涉仪（如图 2 所示）来检测窃听者（或对象'O'）的存在而不警告她。IFM 涉及到量子叠加可以用来实现远离被阻挡位置的粒子的检测这一反直觉的想法。

探测器上的检测结果由以下给出![$$\begin{aligned} \mathinner {|{a}\rangle } = \frac{\mathinner {|{D1}\rangle } + \mathinner {|{D2}\rangle }}{\sqrt{2}} \nonumber \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ44.png)![$$\begin{aligned} \mathinner {|{b}\rangle } = \frac{\mathinner {|{D1}\rangle } - \mathinner {|{D2}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ1.png)(1)其中![$$\mathinner {|{a}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq32.png)和![$$\mathinner {|{b}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq33.png)分别是干涉仪的上路径和下路径。因此，如果没有物体存在，则只在 D1 处发生探测:![$$\begin{aligned} \mathinner {|{a}\rangle } + \mathinner {|{b}\rangle } = \mathinner {|{D1}\rangle }, \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ2.png)(2)而在![$$\mathinner {|{D2}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq34.png)处的检测表示路径'a'上存在物体。![](img/516210_1_En_2_Fig2_HTML.png)

图 2

IFM 原理的图示表示。通过在检测器 D1 或 D2 上检测到可以找到物体‘O’的存在。‘S’是发射单光子的光源，光子入射到光束分束器 BS 上。‘M’是光学镜子。

原型反事实量子密钥分发（CQKD）协议是 2009 年诺氏提出的协议[12]（称为‘Noh09’）。这也是基于 IFM 原理，但使得爱丽丝和鲍勃能够共享相同的比特串集合—秘密密钥。在 CQKD 中，光束分束器的一臂保留在爱丽丝的站点，另一臂延伸至鲍勃的站点。相关意义上的‘反事实性’意味着粒子在阻挡动作发生的地方之外被检测到。‘反事实’这个术语是罗杰·彭罗斯创造的，用来解释这一现象[13]。

IFM 原理的应用不仅限于密钥分发，还包括其他一些量子信息处理方案，比如直接通信[14]、纠缠产生[15]、量子计算[16, 17]，以及反事实量子密钥分发的设备独立场景[18]。要了解量子计算的其他方面以及对其的简要评论，请参见参考文献[19]。

Noh09 协议的工作原理如下：

1.  (1) 爱丽丝发送的单光子极化状态为 ![$$\uparrow $$](img/516210_1_En_2_Chapter_TeX_IEq35.png)（水平）或 ![$$\downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq36.png)（垂直），通过米歇尔森干涉仪（M）的光束分束器（BS）发送。她保留 M 的一个臂（臂 *a*）在她的站点，而另一个臂（外部的臂 *b*）到达鲍勃的站点（图 3）。经过 BS 后，输入光子的状态变换为:![$$\begin{aligned} \mathinner {|{\varPsi }\rangle }_{ab} = \frac{1}{\sqrt{2}}(\mathinner {|{0,s}\rangle }_{ab}+ \mathinner {|{s,0}\rangle }_{ab}), \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ3.png)(3)，其中 ![$$s \in \{\uparrow , \downarrow \},\mathinner {|{0}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq37.png) 代表真空态（即从另一个臂输入），“ab” 下标表示各自输出臂的状态。

1.  (2)

    在协议的每次运行中，鲍勃以相等的概率选择两个选项之一：(a) 在测量光子的极化状态 ![$$\mathinner {|{\uparrow }\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq38.png) 的同时将其反射（表示为 ![$$R_\uparrow $$](img/516210_1_En_2_Chapter_TeX_IEq40.png))；或者(b) 相反地（表示为 ![$$R_\downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq41.png))。

1.  (3)

    如果 Bob 的操作 ![$$R_t$$](img/516210_1_En_2_Chapter_TeX_IEq42.png)（其中 ![$$t \in \{\uparrow ,\downarrow \}$$](img/516210_1_En_2_Chapter_TeX_IEq43.png)），与 Alice 的输入光子态匹配（即，![$$t=s$$](img/516210_1_En_2_Chapter_TeX_IEq44.png)），则光子被反射并导致在 Alice 的 ![$$D_2$$](img/516210_1_En_2_Chapter_TeX_IEq45.png) 探测器上确定性地检测到。

1.  （4）

    当输入状态与 Bob 的动作不匹配时（即，![$$t \ne s$$](img/516210_1_En_2_Chapter_TeX_IEq46.png)），光子将以概率为 0.5/0.25/0.25 被检测到在检测器 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq47.png)/![$$D_2$$](img/516210_1_En_2_Chapter_TeX_IEq48.png)/![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq49.png)。请注意，第一个发生在 Bob 的站点，其他两个发生在 Alice 的站点。

1.  （5）

    挑选过程涉及 Alice 公开宣布的 ![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq50.png) 检测实例。秘密比特串由相应的 ![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq51.png) 检测的极化态形成。

1.  （6）

    Alice 和 Bob 分别在被挑选的比特的子集上宣布输入状态和操作选择，以便他们可以用它来确定信道中的（近似）错误率 *e*。如果观察到的错误超过阈值限制，他们终止协议。

![](img/516210_1_En_2_Fig3_HTML.png)

图 3

S ![$$\rightarrow $$](img/516210_1_En_2_Chapter_TeX_IEq52.png) 源；C ![$$\rightarrow $$](img/516210_1_En_2_Chapter_TeX_IEq53.png) 循环器；(P)BS ![$$\rightarrow $$](img/516210_1_En_2_Chapter_TeX_IEq54.png) （极化）分束器；OD ![$$\rightarrow $$](img/516210_1_En_2_Chapter_TeX_IEq55.png) 光延迟；FM ![$$\rightarrow $$](img/516210_1_En_2_Chapter_TeX_IEq56.png) 法拉第镜；OL ![$$\rightarrow $$](img/516210_1_En_2_Chapter_TeX_IEq57.png) 光环路；SW ![$$\rightarrow $$](img/516210_1_En_2_Chapter_TeX_IEq58.png) 开关；![$$D_{1/2/3}$$](img/516210_1_En_2_Chapter_TeX_IEq59.png) ![$$\rightarrow $$](img/516210_1_En_2_Chapter_TeX_IEq60.png) 探测器。协议：艾丽斯将在基础 {![$$\uparrow , \downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq61.png)} 中准备的单光子态发送到一个迈克尔逊干涉仪，鲍勃位于其中一个臂的末端。他在每个时刻应用“反射”或“测量/阻挡”（这取决于极化）的操作。在 ![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq62.png) 检测到的是无相互作用的测量，而在 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq63.png) 检测到的是穿过外部臂的光子。检测到的光子极化构成了一组秘密比特。

在量子通道中误差率的估计是由爱丽丝和鲍勃完成的，其中，![$$\begin{aligned} e \equiv P(\uparrow , R_\uparrow |D_1) + P(\downarrow , R_\downarrow |D_1), \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ4.png)(4)其中 ![$$P(\cdot |\cdot )$$](img/516210_1_En_2_Chapter_TeX_IEq64.png) 代表条件概率。尽管爱丽丝的输入态（Eq. 3）彼此正交（即，![$$\langle \uparrow | \downarrow \rangle = 0$$](img/516210_1_En_2_Chapter_TeX_IEq65.png)），但外部通道中伊娃可获得的相应态 ![$$\rho _s$$](img/516210_1_En_2_Chapter_TeX_IEq66.png) 确实不是。具体来说，![$$\rho _s = \left( \mathinner {|{0}\rangle }_b\mathinner {\langle {0}|} + \mathinner {|{s}\rangle }_b\mathinner {\langle {s}|}\right) $$](img/516210_1_En_2_Chapter_TeX_IEq67.png) 不能完全区分，因为两个编码态之间的迹距离为 ![$$D = |\rho _\uparrow - \rho _\downarrow | = \frac{1}{2}$$](img/516210_1_En_2_Chapter_TeX_IEq68.png)。因此，伊娃能找到真正偏振的最佳可能概率是 ![$$p_\mathrm{guess} = (1+D) = \frac{3}{4}$$](img/516210_1_En_2_Chapter_TeX_IEq69.png)。因此，她找到真正偏振的最小误差为![$$\begin{aligned} e^\prime \equiv 1-p_\mathrm{guess}=\frac{1}{4}. \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ5.png)(5)Table 3

下表给出了在鲍勃操作和爱丽丝发送具有特定极化的光子的情况下，检测到的概率，假设设备完美（无损耗情况下）。这里 *R*（反射率）（分别是 *T*（透射率））是分光镜的反射率（分别是透射率），满足方程式为 ![$$R + T = 1$$](img/516210_1_En_2_Chapter_TeX_IEq70.png)

| (爱丽丝, 鲍勃) | D1 | D2 | DB |
| --- | --- | --- | --- |
| (![$$\uparrow $$](img/516210_1_En_2_Chapter_TeX_IEq71.png),![$$R_{\uparrow }$$](img/516210_1_En_2_Chapter_TeX_IEq72.png)) 或者 (![$$\downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq73.png),![$$R_\downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq74.png)) | 0 | 1 | 0 |
| (![$$\uparrow $$](img/516210_1_En_2_Chapter_TeX_IEq75.png),![$$R_\downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq76.png)) 或者 (![$$\downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq77.png),![$$R_{\uparrow }$$](img/516210_1_En_2_Chapter_TeX_IEq78.png)) | *RT* | ![$$R²$$](img/516210_1_En_2_Chapter_TeX_IEq79.png) | *T* |

结果表明，如果鲍勃以等概率应用![$$R_\uparrow $$](img/516210_1_En_2_Chapter_TeX_IEq80.png)或![$$R_\downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq81.png)(见表 3)，则反事实检测的概率为![$$\eta _\mathrm{Noh} \equiv \sum _{s = \uparrow ,\downarrow } P_{D_1|s} P_s = \frac{RT}{2},$$](img/516210_1_En_2_Chapter_TeX_Equ6.png)(6)。在无偏振分束器的情况下，![$$\eta _\mathrm{Noh} = \frac{1}{8}$$](img/516210_1_En_2_Chapter_TeX_IEq82.png)。量![$$\eta _\mathrm{Noh}$$](img/516210_1_En_2_Chapter_TeX_IEq83.png)代表每个发送的光子产生的平均比特数，可以视为该协议的效率。多年来，对 Noh 的协议进行了详细研究，用于错误分析和克服窃听问题的有效方法[21]。Noh09 被研究并修改为一种基于纠缠的协议，其安全性由贝尔不等式违反给出[22]。

在直接通信中关于反事实性的定义[14]已经在过去几年中进行了讨论[23–26]。主要论点是当光子在爱丽丝站点的一个探测器处被探测时留下的微弱痕迹。因此，根据这个定义，只有在一个情况下探测才真正是反事实的。然而，这仅限于直接通信协议，因为 QKD 协议使用的是正交状态，而不是与前者相同的状态。因此，编码并不是基于鲍勃是否阻挡或反射，而是基于鲍勃是否应用 ![$$R_\uparrow $$](img/516210_1_En_2_Chapter_TeX_IEq84.png) 或 ![$$R_\downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq85.png)，使协议完全是反事实的。

#### 1.2.3 最新进展

在 Noh09 协议的筛选过程中，非反事实部分（在 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq86.png) 和 ![$$D_2$$](img/516210_1_En_2_Chapter_TeX_IEq87.png) 探测器处）被丢弃。它们既不用于错误检查，也不用于密钥生成。对于 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq88.png) 探测，由于量子比特在外部臂到达鲍勃并在他的站点被探测，因此在很大程度上似乎不可行考虑将它们用于密钥生成。但最近却证明了相反。

对 Noh09 协议进行了独特而独特的修改后，证明了在 Bob 的站点检测到的 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq89.png) 也可以用作秘密密钥位[27]。在修改版本中，实验部分保持不变，并使 Alice 和 Bob 能够进行 *翻转* 操作。这本质上是执行操作 ![$$\uparrow \leftrightarrow \downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq90.png)。首先让我们看看使用 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq91.png) 位作为密钥的后果。考虑仅使用 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq92.png) 检测作为密钥位的协议，而使用 ![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq93.png) 检测进行误差估计。通过所提出的修改，Alice 和 Bob 可能可以将效率提高一倍（与 Noh09 相比），因为（来自表 3）![$$\begin{aligned} \eta = P_{D_B} = \frac{1}{4}. \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ7.png)(7)然而，这引发了一个安全问题。Eve 可能会发起一种攻击，其中她将她的探针与外部臂中的粒子纠缠（并解缠），并获取有限信息。但扭曲的是，通过这种攻击，Eve 在 Alice 和 Bob 估计错误时不会引入错误。要了解这是如何工作的，请考虑这个：

+   Eve 在光子在外部路径上进行攻击时，设为 ![$$\begin{aligned} \mathinner {|{x, \epsilon _0}\rangle }_{be}&amp;\longrightarrow \mathinner {|{x,\epsilon _x}\rangle }_{be} ~~~ (x \in \{0, \uparrow , \downarrow \}), \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ8.png)(8a)![$$\begin{aligned} \mathinner {|{0,\epsilon _s}\rangle }_{be}&amp;\longrightarrow \mathinner {|{0,\epsilon _s}\rangle }_{be} ~~~(s \in \{\uparrow , \downarrow \}). \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ9.png)(8b)

+   让这个攻击成为酉算符 ![$$\mathcal {U}$$](img/516210_1_En_2_Chapter_TeX_IEq94.png)，她的探针最初准备在状态 ![$$\mathinner {|{\epsilon _0}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq95.png)。特别是，如果 Alice 将光子 ![$$\mathinner {|{s}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq96.png) 通过分光器发送（如方程 3），Eve 的攻击后光子的状态 ![$$\mathcal {U}$$](img/516210_1_En_2_Chapter_TeX_IEq97.png) 将会是 ![$$\begin{aligned} \mathinner {|{\varPsi ^\prime }\rangle }_{abe} = \frac{1}{\sqrt{2}}(\mathinner {|{s,0,\epsilon _0}\rangle } + \mathinner {|{0,s, \epsilon _s}\rangle })_{abe}. \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ10.png)(9)

+   Bob 应用了![$$R_t$$](img/516210_1_En_2_Chapter_TeX_IEq98.png)，接着 Eve 对其进行了不可逆攻击![$$\mathcal {U}^{-1}$$](img/516210_1_En_2_Chapter_TeX_IEq99.png)，光子的状态变为![$$\begin{aligned} \mathinner {|{\varPsi ^{\prime \prime }}\rangle }_{abe}&amp;{\mathop {\longrightarrow }\limits ^{R_t}} \left\{ \begin{array}{ll} \mathinner {|{\varPsi ^\prime }\rangle }_{abe} &amp;{} (t = s) \\ (\mathinner {|{s,0,\epsilon _0}\rangle })_{abe}  \mathrm{or}  (\mathinner {|{0,s, \epsilon _s}\rangle })_{abe} &amp;{} (t \ne s) \end{array}, \right. \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ11.png)(10a)![$$\begin{aligned}&amp;{\mathop {\longrightarrow }\limits ^{\mathcal {U}^{-1}}} \left\{ \begin{array}{ll} \mathinner {|{\varPsi }\rangle }_{ab}\otimes \mathinner {|{\epsilon _0}\rangle }_e &amp;{} (t = s) \\ (\mathinner {|{s,0,\epsilon _0}\rangle })_{abe}  \mathrm{or}  (\mathinner {|{0,0, \epsilon _s}\rangle })_{abe} &amp;{} (t \ne s) \end{array}. \right. \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ12.png)(10b)

在上述方程中，本质上第一种情况![$$(t = s)$$](img/516210_1_En_2_Chapter_TeX_IEq100.png)对应于 Bob 对粒子![$$\mathinner {|{s}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq102.png)应用了![$$R_s$$](img/516210_1_En_2_Chapter_TeX_IEq101.png)，它确定地到达了 Alice 站的检测器![$$D_2$$](img/516210_1_En_2_Chapter_TeX_IEq103.png)，即使 Eve 也在场。因此根据方程(4)，不会产生错误。第二种情况中的变化反映不出错误。Eve 基本上利用了这种情况并获取了信息，而引入的错误量为零。

+   如果发现粒子在 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq106.png) 探测器上，伊娃不产生任何错误，她的探测器处于状态 ![$$\mathinner {|{\epsilon _s}\rangle }\mathinner {\langle {\epsilon _s}|}$$](img/516210_1_En_2_Chapter_TeX_IEq105.png)。

+   如果粒子崩溃到艾丽斯的臂上，探测器处于状态 ![$$\mathinner {|{\epsilon _0}\rangle }\mathinner {\langle {\epsilon _0}|}$$](img/516210_1_En_2_Chapter_TeX_IEq107.png)。由于在这种情况下没有生成密钥，伊娃不会失去任何东西。

+   因此，伊娃获得了完整的关于艾丽斯发送的偏振信息，在鲍勃的站点检测到，并且在通道中没有引入错误。

+   因此，伊娃的这种策略将是无误差的，或者是一个‘无噪声攻击’。

在此需要注意的重要一点是，修改后的协议中的密钥速率正好是 ![$$\frac{1}{4}$$](img/516210_1_En_2_Chapter_TeX_IEq108.png)，与方程式 (5) 的结果没有矛盾。换句话说，由于粒子的相干性不参与在 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq109.png) 探测器上的检测，非反事实位并没有利用与伊娃的非正交条件的优势。因此，回顾起来，包括 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq110.png) 探测用于密钥不是一个理想的建议。然而，存在一个简单而优雅的解决方案，本质上保持效率相同。这实质上将解决将非正交条件的相关性恢复到 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq111.png) 探测中的问题。

#### 1.2.4 反事实安全

让 Alice 和 Bob 能够执行一个操作 ![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq112.png)，将光子的极化从 ![$$\uparrow $$](img/516210_1_En_2_Chapter_TeX_IEq113.png) 翻转为 ![$$\downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq114.png) 或反之，如前所述。这个翻转操作由 Alice 在内部臂的镜子 *M* 之后在分数 *f* 的情况下执行。独立地，Bob 也在分数 *f* 的情况下翻转了反射的极化。准确地说，如果他应用了 ![$$R_\uparrow $$](img/516210_1_En_2_Chapter_TeX_IEq115.png) 然后应用 ![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq116.png)，那么他实际上测量了光子的 ![$$\downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq117.png) 极化，同时反射了 ![$$\uparrow $$](img/516210_1_En_2_Chapter_TeX_IEq118.png) 极化，该极化被翻转为 ![$$\downarrow $$](img/516210_1_En_2_Chapter_TeX_IEq119.png)。这个第二修改的协议被称为 ![$$\mathcal {P}$$](img/516210_1_En_2_Chapter_TeX_IEq120.png)，它保持了两个状态之间的正交性 ![$$\mathinner {|{\uparrow }\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq121.png) 和 ![$$\mathinner {|{\downarrow }\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq122.png)，因为操作 ![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq123.png) 只在它们之间切换。

通过这个简单的修改，Alice 和 Bob 有可能限制 Eve 进行无噪声的攻击。这是可能的，因为 Eve 在不知道他们何时应用或不应用操作![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq124.png)的情况下受限于知识，为了消除她的痕迹，两种情况需要不同的无攻击策略。下面的示例演示了这一点。

1.  (1)让![$$\mathinner {|{s}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq125.png)表示由 Alice 发送的光子。经过 Eve 的攻击![$$\mathcal {U}$$](img/516210_1_En_2_Chapter_TeX_IEq126.png)后，光子的状态变为![$$\begin{aligned} \mathinner {|{\varPsi ^\prime }\rangle }_{abe} = \frac{1}{\sqrt{2}}(\mathinner {|{s,0,\epsilon _0}\rangle } + \mathinner {|{0,s, \epsilon _s}\rangle })_{abe}. \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ13.png)(11)

1.  (2)如果 Bob 应用![$$R_s$$](img/516210_1_En_2_Chapter_TeX_IEq127.png)，并且两者执行操作![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq128.png)，那么光子的状态将是![$$\begin{aligned} \mathinner {|{\varPsi ^{\prime \prime }}\rangle }_{abe} = \frac{1}{\sqrt{2}}(\mathinner {|{\overline{s},0,\epsilon _0}\rangle } + \mathinner {|{0,\overline{s}, \epsilon _s}\rangle })_{abe}. \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ14.png)(12)

1.  (3)夏娃必须失败于将她的探针与光子完全分离开来，因为![$$\begin{aligned} \mathinner {|{\overline{s}, \epsilon _s}\rangle }_{be} \xrightarrow {\mathcal {U}^{-1}}\mathinner {|{s, \epsilon _0}\rangle }_{be}  \mathrm{and}  \mathinner {|{s, \epsilon _{s}}\rangle }_{be} \xrightarrow {\mathcal {U}^{-1}} \mathinner {|{s, \epsilon _0}\rangle }_{be}, \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ15.png)(13) 在一个酉操作中是不可能的。

因此，**夏娃** 无法进行无噪声的攻击！$$\mathcal {P}$$ 协议。夏娃可能考虑其他形式的（有噪声的）攻击，但其核心思想仍然相同——夏娃通过探针与外部臂中的粒子的相互作用所做的任何尝试必然会使探针与光子纠缠在一起，导致相干性降低，并且会在干涉仪中观察到。

由于现在必须重新定义误差估计（考虑翻转动作），所以让协议中的扩展公式![$$\mathcal {P}$$](img/516210_1_En_2_Chapter_TeX_IEq130.png) 定义为![$$\begin{aligned} e_{(1)}&amp;\equiv P(\downarrow ,R_\downarrow |D_1,\tau _{ab}) + P(\uparrow ,R_\uparrow |D_1, \tau _{ab}), \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ16.png)(14a)![$$\begin{aligned} e_{(2)}&amp;\equiv P(\downarrow ,R_\downarrow |D_1,\tau _{ab}) + P(\uparrow ,R_\uparrow |D_1, \tau _{ab}), \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ17.png)(14b)，其中![$$e_{(1)}$$](img/516210_1_En_2_Chapter_TeX_IEq131.png)（响应地，![$$e_{(2)}$$](img/516210_1_En_2_Chapter_TeX_IEq132.png)）对应于它们都未（响应地，都）在给定的![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq134.png) 检测中应用操作![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq133.png) 的实例。类似地，![$$\tau _{ab}$$](img/516210_1_En_2_Chapter_TeX_IEq135.png)（响应地，![$$\tau _{ab}$$](img/516210_1_En_2_Chapter_TeX_IEq136.png)）代表当艾丽斯和鲍勃都（响应地，都不）应用操作![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq137.png) 的情况。通道中的总误差率被认为是上述两个误差率的平均值。因此如果![$$f=0.5$$](img/516210_1_En_2_Chapter_TeX_IEq138.png)，那么![$$e = \frac{e_{(1)} + e_{(2)}}{2}$$](img/516210_1_En_2_Chapter_TeX_IEq139.png)。

该协议 ![$$\mathcal {P}$$](img/516210_1_En_2_Chapter_TeX_IEq140.png) 的一个新颖之处在于，用于安全分析的比特（拟实验比特）与形成秘密密钥的比特（非拟实验比特）不同。该协议的这一有趣特征导致了一个令人惊讶和好奇的情况，即形成秘密密钥的探测发生在一个特定位置（探测器 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq141.png)），而安全性是通过发生在其他地方的探测（探测器 ![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq142.png)）来验证的。因此得名 *拟实验安全性*。

#### 1.2.5 其他拟实验量子密钥分发协议

**(a) 半对拟实验协议**：半对拟实验量子密钥分发（SC-QKD）协议[28]简要介绍如下；

(![$$*$$](img/516210_1_En_2_Chapter_TeX_IEq143.png))

艾丽斯向鲍勃发送固定偏振状态的光子，如图 4 所示。

(![$$*$$](img/516210_1_En_2_Chapter_TeX_IEq144.png))

在这里，艾丽斯和鲍勃都能够反射/测量光子。

(![$$*$$](img/516210_1_En_2_Chapter_TeX_IEq145.png))

在该协议中，拟实验探测发生在一方进行反射操作，而另一方选择测量操作的情况下。

(![$$*$$](img/516210_1_En_2_Chapter_TeX_IEq146.png))

因此，在该协议中的两种编码状态要么是 ![$$\{M_A,R_B\}$$](img/516210_1_En_2_Chapter_TeX_IEq147.png)（艾丽斯测量 & 鲍勃反射），要么是 ![$$\{R_A,M_B\}$$](img/516210_1_En_2_Chapter_TeX_IEq148.png)（反之亦然）。

![](img/516210_1_En_2_Fig4_HTML.png)

图 4

表示半对拟实验量子密钥分发协议装置的图示

符号与图 3 中的符号相同。 变化在于，Alice 还有一个开关 (SW) 来阻挡或反射粒子，而 Bob 站点上的偏振分束器不再必要。 在 SC-QKD 中，在检测器 ![$$D_A$$](img/516210_1_En_2_Chapter_TeX_IEq149.png)（Alice 站点，除了 ![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq150.png) 和 ![$$D_2$$](img/516210_1_En_2_Chapter_TeX_IEq151.png)）或 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq152.png)（Bob 站点）上生成的非计数位既不用于密钥生成，也不用于错误估计。 类似于 Noh09 中的情况，在修改后的 SC-QKD 协议中，检测器 ![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq153.png) 的计数位可用于错误分析，并且检测器 ![$$D_A$$](img/516210_1_En_2_Chapter_TeX_IEq154.png) 和 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq155.png) 的非计数位可用于生成密钥。 检测实例的公开公告仅由 Alice 进行，仅适用于发生在检测器 ![$$D_2$$](img/516210_1_En_2_Chapter_TeX_IEq156.png) 或 ![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq157.png) 上的检测。 这可能会将修改后的 SC-QKD 协议的效率从 ![$$\frac{1}{8}$$](img/516210_1_En_2_Chapter_TeX_IEq158.png) 增加到 ![$$\frac{1}{2}$$](img/516210_1_En_2_Chapter_TeX_IEq159.png)，但为 Eve 启动无噪声攻击提供了可能，原因与之前的情况类似。

对于 Noh09 案例，解决此问题的一个方法是允许 Alice 和 Bob 都执行翻转操作！$$\theta $$。为了看到提议的修改如何帮助 Alice 和 Bob，假设在协议运行的每个实例中，Alice 将极化为![$$\mathinner {|{\uparrow }\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq161.png)的光子发送给 Bob。对于特定实例中发送的给定光子，当他们两个都对反射极化执行操作![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq162.png)时，光子的状态变为![$$\begin{aligned} \mathinner {|{\varPsi ^\prime }\rangle }_{abe}&amp;{\mathop {\longrightarrow }\limits ^{R_A,R_B}} \left\{ \begin{array}{ll} \frac{1}{\sqrt{2}}(\mathinner {|{\uparrow ,0,\epsilon _0}\rangle } + \mathinner {|{0,\uparrow , \epsilon _\uparrow }\rangle })_{abe} &amp;{} (\tau _{ab}) \\ \frac{1}{\sqrt{2}}(\mathinner {|{\downarrow ,0,\epsilon _0}\rangle } + \mathinner {|{0,\downarrow , \epsilon _\uparrow }\rangle })_{abe} &amp;{} (\tau _{ab}), \end{array} \right. \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ18.png)(15)，假设 Bob 应用*reflect*操作。方程(15)中的第一种情况（第二种情况）表示两者都（分别）未执行操作![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq163.png)。与 Noh09 的情形类似，Eve 无法完全解缠探针。这是因为，单次未攻击中既不可能执行操作![$$\mathinner {|{\downarrow , \epsilon _\uparrow }\rangle }_{be} \rightarrow \mathinner {|{\uparrow , \epsilon _0}\rangle }_{be}$$](img/516210_1_En_2_Chapter_TeX_IEq164.png)(*reflect*和*flip*)，也不可能执行操作![$$\mathinner {|{\uparrow , \epsilon _{\uparrow }}\rangle }_{be} \rightarrow \mathinner {|{\uparrow , \epsilon _0}\rangle }_{be}$$](img/516210_1_En_2_Chapter_TeX_IEq165.png)(仅*reflect*)。指出操作![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq166.png)只降低了反事实检查位的总数，但并不改变非反事实密钥位的比例，如协议![$$\mathcal {P}$$](img/516210_1_En_2_Chapter_TeX_IEq167.png)中所示。因此，该协议的总效率为![$$\begin{aligned} \eta _\mathrm{sc} = P_{D_A} + P_{D_B} = \frac{1}{2} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ19.png)(16)，如![$$P_{D_A} = P_{D_B} = \frac{1}{4}$$](img/516210_1_En_2_Chapter_TeX_IEq171.png) 操作，它们的缺席意味着 ![$$R_A/R_B$$](img/516210_1_En_2_Chapter_TeX_IEq172.png)。

**(c) 级联 Noh09**：为了提高 Noh09 的效率，提出了同样的级联版本[30]，在第一个后引入了一系列分束器。到达 Bob 的光子的结果振幅呈指数下降（![$$2^{-b_n/2}$$](img/516210_1_En_2_Chapter_TeX_IEq173.png)，其中 ![$$b_n$$](img/516210_1_En_2_Chapter_TeX_IEq174.png) 是设置中分束器的总数），因此 ![$$D_B$$](img/516210_1_En_2_Chapter_TeX_IEq175.png) 检测减少。因此，为秘钥加入非计数位将在效率方面几乎没有增加。但是，级联 Noh09 协议的效率也可以通过修改后的 SC-QKD 协议实现，但实验设置要简单得多。

**使用计数位进行密钥**：原则上，Noh09（以及其他计数协议）中的计数探测（在 ![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq176.png) 探测器处）也可以用于密钥位。下表表示考虑翻转操作 ![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq178.png) 时 ![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq177.png) 检测的概率（表 4）。表 4

第二列代表了检测到![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq179.png)的概率![$$P_{D_1}$$](img/516210_1_En_2_Chapter_TeX_IEq179.png)，第三列代表了贡献秘钥的分数![$$P_{D_1}^*$$](img/516210_1_En_2_Chapter_TeX_IEq181.png)，考虑到它们的![$$\theta$$](img/516210_1_En_2_Chapter_TeX_IEq182.png)的翻转操作情况。

| ![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq183.png) 的翻转动作 | ![$${P_{D_1}}$$](img/516210_1_En_2_Chapter_TeX_IEq183.png) | ![$${\frac{P_{D_1}^*}{P_{D_1}}}$$](img/516210_1_En_2_Chapter_TeX_IEq184.png) |
| --- | --- | --- |
| 两者都不 | ![$$\frac{1}{8}(1-f)²$$](img/516210_1_En_2_Chapter_TeX_IEq185.png) | 1 |
| 爱丽丝或鲍勃 | ![$$\frac{3}{8}f(1-f)$$](img/516210_1_En_2_Chapter_TeX_IEq186.png) | ![$$\frac{1}{3}$$](img/516210_1_En_2_Chapter_TeX_IEq187.png) |
| 其中 | ![$$\frac{1}{8}f²$$](img/516210_1_En_2_Chapter_TeX_IEq188.png) | 1 |

原文：发现 ![$$P_{D_1} = \frac{1}{8} + \frac{1}{2}f(1-f)$$](img/516210_1_En_2_Chapter_TeX_IEq189.png)，即探测器![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq190.png)的总探测次数。有趣的是，反事实密钥率 ![$$P_{D_1}^*=\frac{1}{8}$$](img/516210_1_En_2_Chapter_TeX_IEq191.png)，与 Noh09 协议中探测器![$$D_1$$](img/516210_1_En_2_Chapter_TeX_IEq192.png)的探测概率相同。因此，协议的总效率 ![$$\mathcal {P}$$](img/516210_1_En_2_Chapter_TeX_IEq193.png)可以写成![$$\begin{aligned} \eta _\mathrm{total} = P_{D_B} + P_{D_1}^*= \frac{3}{8}. \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ20.png)(17)

#### 原文：1.2.6 实验部分

原文：Noh09 协议已经被作为基于光纤的通信方案实验实施[31]，其设置如图 6 所示。![](img/516210_1_En_2_Fig6_HTML.png)

原文：图 6

原文：图是 Noh09 协议基于光纤的实验设置的框图，下方是图中的组件。

原文：经过（Liu et al.）的许可，©2012 年，美国物理学会重现

原文：以下是对实验输出的简要描述。

+   原文：两个版本的实验是桌面设置和带有 1km 光纤的设置。这两个版本都显示了干涉仪的可见度大于 98%。

+   原文：实验是在 C 波段的通信波长（1550 纳米）进行的。

+   原文：在桌面设置模式下，当平均光子数为 0.5（0.05）光子/脉冲时，实验观察的误比特率为 6.8%（4.2%）时，原始密钥率为 51.3 比特/秒（2.2 比特/秒）。

+   在光纤模式下，通道损耗约为 1dB，当通道误码率为 5.8%（5.5%）时，达到了 126 比特/秒（94 比特/秒）的关键速率，平均光子数为 1（0.5）光子/脉冲。

#### 1.2.7 结论和展望

基于正交状态的量子密码学通常有三种类型：Goldenberg-Vaidman，反事实和贝尔型状态。引入了一种不同类型的基于 IFM 的 QKD 协议，该协议提高了效率，同时不会在安全性上妥协。采用反事实协议进行 QKD 的好处是：（a）由于它是基于正交状态的协议，所以设置包括更简单的状态准备和测量设备；（b）潜在的密钥位不用于错误估计，这导致了反事实安全性的产生；（c）通过对 SC-QKD 协议的建议修改也可以实现 BB84 的效率。因此，基于反事实的量子通信方案具有某些优点，以及在实现商业目的上的方便性。

### 1.3 量子区块链

区块链技术自人工智能（AI）和机器学习（ML）爆发后又一伟大创举，指的是一种去中心化的数字分类账。但同样的缺点是系统极为巧妙，效率低下。这是一个无中间人处理交换的公共分类账，用户可以匿名地转移资金和信息，而不必担心交易被泄露、删除或从公共分类账中编辑。区块链的概念采用了哈希算法、工作证明等想法。然后可以将这些术语与几种量子协议相关联，并用于量子区块链的量子模拟，即*量子区块链*[32]。构建量子区块链使用 GHZ-States、![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq194.png)-protocol[33]和时间纠缠的概念。我们将详细讨论提到的每件事情，首先让我们来谈谈经典区块链。

#### 1.3.1 经典区块链

区块链是由一组计算机管理的不可变数据记录的时间戳编译，不属于单个组织所有。交易是区块链的基本要素，许多交易形成一个区块，许多区块使用数字数据连接形成一个区块链。去中心化基础设施、去中介化和分布式分类账是区块链的主要特征，正因为这些特性，高效的区块链具有巨大的应用。区块链的目标是验证和验证参与者发起的交易，并在其他参与者的同意下记录这些行动的证据。首先，我们建立必要的术语，然后了解量子区块链的整个工作流程。

在深入了解复杂性之前，让我们澄清一下关于区块链分类账的几个关键点

1.  1.

    所有新区块都必须经过共识过程，经过验证后才能添加到账本中。

1.  2.

    每个区块都包含自己的哈希值和前一个区块的哈希值，形成链式结构。

1.  3.

    没有***中央***机构来管理像普通数据库一样的信息交换。

#### 1.3.2 关键术语

+   **挖矿**：简而言之，挖矿是向账本中添加和验证新区块，或者向已有交易账本中添加交易的过程，这些交易账本分布在所有用户之间。由于每个节点都有一个特定的哈希值，只有下一个区块知道，所以挖矿（创建和验证新区块）的过程应该是这样的，即新区块不应该破坏整个账本的完整性，也就是说新区块的哈希值不应该容易被伪造。挖矿由称为*矿工*的特殊对等节点进行，他们必须解决一个复杂的问题，并在解决难题（复杂问题）后将其广播，以便由对等块进行验证并添加到账本中。挖矿的过程是区块链设置中非常重要但需要资源的过程。

+   **哈希算法**：我们上面提到的作为区块之间数字链接的哈希值是使用哈希算法创建的。哈希算法基本上将任意长度的输入值转换为固定长度的十六进制值。这个过程通常被称为*xyz*的哈希。固定长度的十六进制值称为哈希值。在哈希过程中，为特定输入获取哈希值很简单，但反向工程哈希算法并获取输入值实际上是不可能的。因此，哈希函数被称为单向函数。让我们看一下 SHA256（注：SHA256 哈希算法最近被攻破了，但在这里仅作为示例说明，现在没有区块链账本使用 SHA256 了。）

    ![$$\begin{aligned}&amp;\qquad \qquad \qquad {\text {sha256sum(``这是 SHA256 示例'')}} = \\&amp;{\text {c6a96c2ae5414c8e009db2bb8913ceafcd860f8be92d526b7b57288e5d4e4c50}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ45.png)

+   **共识算法**：共识一词意味着一般意见，共识算法是区块链网络中所有节点就分布式分类帐的当前状态达成共识（共同协议）的技术。分布式一词指出数据库的副本由所有节点存储。正如前面所述，没有中央机构来处理交易，这使得这些节点之间的一般协议成为确保所有节点就区块链达成一致的唯一方式。Proof of work 算法 (POW) 是这样一种共识算法。POW 是哈希算法的应用，它允许证明已经执行了一定量的工作。在挖矿过程中，矿工需要解决工作量证明难题（在前面部分提到的复杂问题）以便将新区块添加到数据库中。POW 难题是一个非确定性多项式硬（NP-hard）问题。这里使用的概念是 POW 难题是一个数学问题且难以解决，因此解决并提供 POW 难题的解决方案可以确保整个数据库的完整性。此外，解决难题需要大量的计算资源（非常耗时）并且还有一些限制。这些限制和缺点已经得到加强，并且使用了一种新的共识算法，称为 Proof of Stake 算法。

+   **时间戳**：*信任*是与交易一般关联的非常重要的组成部分，在物理交易中显而易见，但在数字交易中谈论信任在开始时是违反直觉的。共识算法与时间戳的概念一起被用来克服这个问题，时间戳是每个区块上的唯一序列号，它被认为确定了该特定区块被挖掘并由同行通过解决 POW 难题验证的确切时刻。不仅如此，时间戳还用于保持区块链中的交易，以确认交易发生且没有重复的交易。

+   **智能合约**：智能合约基本上是预先编写的“如果/当-那么程序”或“模块”，当事先确定的条件得到满足和验证时执行，涉及两个或多个方之间的交易。它们被认为是数据库中的合约治理，然后在交易结束时更新区块链。但智能合约在区块链中并非强制性，它们被视为一项附加功能。

#### 1.3.3 古典区块链的框架

现在我们对区块链的基本概念有了一个了解，我们可以从图示化开始并理解数据库的链式结构（图 7）。![](img/516210_1_En_2_Fig7_HTML.png)

图 7

区块链的设计

#### 1.3.4 古典区块链的设计

每个区块被挖掘后库中被挖掘后，每个区块由一个头部和一个主体组成，其中头部包含：

+   前一个区块的哈希值。

+   区块的时间戳。

而身体包括：

+   区   区块的哈希值。

因此，通过链接区块的哈希值形成链式结构，并按时间顺序将新挖掘的区块添加到数据库中。区块头还包括随机数和默克尔根，但这些更与账本的深层概念有关。这只是为了让读者知道区块头部还有更多内容。

#### 1.3.5 经典区块链网络

我们看一下区块链的示意图，以更好地理解在网络中执行交易的方式。

区块链中的工作流程：

1.  1.

    新交易将被检查其合法性，并丢弃无效的交易。

1.  2.

    一段时间后，生成一个包含多个交易的区块。新创建的交易是一组未确认交易的一部分。

1.  3.

    区块被发送给网络中的每个节点(参与者)。将新区块的哈希值与现有账本中前一个区块的哈希值相结合。

1.  4.

    一个节点通过满足网络对新提议区块的额外审定需求来验证交易（比特币中的工作证明难题是一个例子）

1.  5.

    节点解决 POW 难题后会收到奖励，通常是加密货币，所有其他节点也会收到新区块的通知。

1.  6.

    然后，每个节点验证区块的合法性，并将其添加到区块链的本地副本中。

1.  7.

    交易完成，账本更新（图 8）。

![](img/516210_1_En_2_Fig8_HTML.png)

图 8

区块链工作流程

#### 1.3.6 量子区块链

在上述部分谈到区块链时，我们了解了区块链的工作原理，但在许多实际应用中，区块链使用大整数因子分解（RSA）问题作为加密算法。这种加密仅依赖于发现大整数因子是一个困难的计算问题（NP-难问题）。最近量子算法（Shor 算法）的发展可以在多项式时间内解决整数因子分解问题，并对 RSA 加密算法的安全性构成威胁。不仅是 Shor 算法，还有 Grover 算法，它对无结构搜索问题提供了二次加速，可以在挖矿过程中使用量子计算机更快地找到满足条件的哈希值 [34]。这意味着拥有量子计算机的一方在竞争中具有不公平的优势。为了应对这一情况，引入了一种基于量子性质构建的区块链建设方案，这种方案对量子计算机具有抵抗性。

首先，我们看看量子区块链的构建，然后再看看多年来已经研究和开发的量子区块链框架。最后，我们将简要概述量子算法如何应用于量子区块链的某些领域，并查看使用电路的量子区块链。

#### 1.3.7 量子区块链的构建

2018 年，提出了一种量子区块链的构建方案 [87]，它利用了时间上的纠缠概念，即像光子这样的两个微观粒子的纠缠，这些粒子从未共存过。量子区块链的构建可以分为两部分，

#### 1.3.8 建立量子链

简而言之，整个区块链账本是一个链式结构，使用哈希值链接并允许点对点连接。量子链的类似概念是利用量子系统的固有属性——纠缠，并编码到 GHZ 状态（格林伯格-霍恩-齐林格）。GHZ 状态是至少具有 3 个子系统的多部分纠缠态。

这里的纠缠指的是时间上的纠缠，而不是空间上的纠缠。可以用这个简单的例子来解释时间上的纠缠，它是在不同时间 t1 和 t2 中对 2 个系统 S1 和 S2 进行的纠缠。

在量子区块链的概念设计中，经典区块中的数据被转换为空间纠缠的贝尔态（2 位的比特串）；*xy* 其中

*xy* = 00,01,10,11 并且被编码为状态:![$$\begin{aligned} |\beta _{xy}\rangle = \frac{1}{\sqrt{2}}(|0\rangle |y\rangle + (-1)^x|1\rangle |\bar{y} \rangle ) \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ21.png)(18)上述方程中 ![$$\bar{y}$$](img/516210_1_En_2_Chapter_TeX_IEq195.png) 代表 *y* 位的取反。为了简化起见，我们也暂时用两个比特串 ![$$r_1r_2$$](img/516210_1_En_2_Chapter_TeX_IEq196.png) 代表我们的经典数据，并将其编码为临时贝尔态:![$$\begin{aligned} |\beta _{r_1 r_2}\rangle ^{0, \tau } = \frac{1}{\sqrt{2}}(|0⁰\rangle |r_2^\tau \rangle + (-1)^{r_1}|1⁰\rangle |\bar{r_2}^\tau \rangle ) \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ22.png)(19)上标表示我们的光子被吸收的时间，注意到每个块的第一个光子会立即被吸收，这为我们提供了执行类似时间戳的操作的可能性。因此，在区块链中，每当记录生成时，它们都被编码在临时贝尔态中，然后这些光子在各自的时间被创建和吸收。例如:![$$\begin{aligned} |\beta _{00}\rangle ^{0, \tau }, \qquad |\beta _{10}\rangle ^{\tau , 2\tau }, \qquad |\beta _{11}\rangle ^{2\tau , 3\tau } \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ23.png)(20)我们仍然需要使用 GHZ 状态和时间上的纠缠概念构建量子链。我们需要将贝尔态的比特串按时间顺序链接成链状结构，为此，我们使用融合过程，其中我们递归地将临时贝尔态投影到一个增长的临时 GHZ 状态中。执行融合过程在物理上需要一个纠缠的光子对源，一个延迟线和一个偏振分束器（PBS）。之后，我们得到以下状态:![$$\begin{aligned} |\text {GHZ}_{r_1r_2 \dots r_{2n}}\rangle ^{0, \tau , \tau , 2\tau , 2\tau \dots , (n-1)\tau , (n-1)\tau , n\tau }=\frac{1}{\sqrt{2}}(|0⁰ r_2^\tau r_3^\tau \dots r_{2n}^{n\tau }\rangle + (-1)^{r_1}|1⁰ \bar{r}_2^\tau \bar{r}_3^\tau \dots \bar{r}_{2n}^{n\tau }) \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ24.png)(21)这里下标表示每个块的比特串的连接字符串，上标表示时间戳。仅使用前两个块 ![$$|\beta _{00}\rangle ^{0, \tau }, |\beta _{10}\rangle ^{\tau , 2\tau } $$](img/516210_1_En_2_Chapter_TeX_IEq197.png) 我们得到一个小的区块链 ![$$|\text {GHZ}_{0010}\rangle ^{0, \tau , \tau , 2\tau }$$](img/516210_1_En_2_Chapter_TeX_IEq198.png)。连接第三个块然后产生 ![$$|\text {GHZ}_{001011}\rangle ^{0, \tau , \tau , 2\tau , 2\tau , 3\tau }$$](img/516210_1_En_2_Chapter_TeX_IEq199.png)。讨论临时纠缠态的可扩展性是一个活跃的研究领域，几篇论文已经对此进行了讨论。解码过程可以用于从方程 (4) 中提取经典数据，而无需测量全部光子统计数据，甚至无需检测它们。上述所有操作已在简单系统中进行了实验验证。

#### 1.3.9 量子区块链网络

我们已经有了构建量子链的想法，创建量子网络面临着与来自不诚实来源的不诚实节点（拜占庭节点）的任何网络相似的问题。最初，简单地假设了不同方之间的通信的安全私密量子信道。最近的发展提出了一种新的 ![$${\theta }$$](img/516210_1_En_2_Chapter_TeX_IEq200.png)-协议[33]，用于验证来自不诚实来源的节点，而且这个过程是通过对等节点以去中心化的方式完成的。

任何验证协议的目标都是利用诚实的参与方来确定他们共享的状态与理想的 GHZ 状态有多接近，并验证其是否包含真正的多体纠缠（GME）。以这种方式验证多体 GHZ 状态中的 GME 对于分布式量子计算和量子通信中的各种协议都是相关的。此外，量子网络中的每个节点都将托管量子区块链的副本，因此，如果节点篡改其自己的本地副本，它不会影响其他节点上的副本，类似于经典情况。

![$${\theta }$$](img/516210_1_En_2_Chapter_TeX_IEq201.png)-协议建立在*XY*-协议的基础上，该协议也是在这里建议的一种验证协议[88]。然而，*XY*-协议无法容忍任意损失，对于更高的损失率是无法使用的。![$${\theta }$$](img/516210_1_En_2_Chapter_TeX_IEq202.png)-协议首先通过使用量子随机数发生器选择一个随机节点作为验证节点。然后，不受信任的源共享一个可能的有效块，一个 n 比特状态。不受信任的源将每个比特分配给每个节点 j 进行验证。现在，验证节点生成随机角度![$$\theta \in 0, \pi )$$，其中![$$\sum _j \theta _j$$](img/516210_1_En_2_Chapter_TeX_IEq204.png)是![$$\pi $$](img/516210_1_En_2_Chapter_TeX_IEq205.png)的倍数。然后将角度分配给每个节点，包括验证节点。最后，分别在![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq206.png)基础上测量比特。![$$\begin{aligned} |+_{\theta _j}\rangle&amp;=\frac{1}{\sqrt{2}}\left( |0\rangle +e^{i\theta _j}|1\rangle \right) \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ25.png)(22)![$$\begin{aligned} |-_{\theta _j}\rangle&amp;= \frac{1}{\sqrt{2}}\left( |0\rangle -e^{i\theta _j}|1\rangle \right) \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ26.png)(23)每个节点的结果![$$\{0,1\} \in Y_j$$](img/516210_1_En_2_Chapter_TeX_IEq207.png)被发送给验证者。必要条件![$$\begin{aligned} \bigoplus _j Y_j = \frac{1}{\pi } \sum _j \theta _j \quad (\text {mod} \; 2) \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ27.png)(24)在 n 比特状态为有效块，即 GHZ 空间状态时，满足概率为 1。因此，![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq208.png)-协议有效地检查新生成的块是诚实还是不诚实。

上述建议的 ![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq209.png)-协议对空间 GHZ 态效果良好，对于时间 GHZ 态需要更多的研究。

### 1.4 量子区块链的量子算法

量子算法是讨论量子技术应用的最有效方法之一。量子算法是指在执行特定任务时，旨在优于在传统计算机上执行同一任务的算法。在类似的情况下，量子算法已经为传统区块链的某些特定任务提出了建议，这可以帮助我们实现高效率。这样一个量子算法利用修改后的 Grover 算法来进行挖矿过程。

#### 1.4.1 Grover’s 算法用于区块链挖矿

简单回顾 Grover’s 算法，Grover’s 算法[35]用于在数据大小为 N 的无序搜索问题中获得二次速度。经典最坏情况的时间复杂度是 ![$$\mathcal {O}$$](img/516210_1_En_2_Chapter_TeX_IEq210.png)(N)，但 Grover’s 算法为我们带来了 ![$$\mathcal {O} \sqrt{N}$$](img/516210_1_En_2_Chapter_TeX_IEq211.png) 的二次加速。以下是算法中涉及的步骤：

+   将系统初始化为均匀叠加态 ![$$|s \rangle $$](img/516210_1_En_2_Chapter_TeX_IEq212.png)，以包括整个样本空间，并且每个状态具有相等的概率振幅 ![$$\frac{1}{\sqrt{2^n}}$$](img/516210_1_En_2_Chapter_TeX_IEq213.png) 。可以使用 Hadamard 门（H-gate）轻松实现这一点。 ![$$|s \rangle = H^{\otimes n}|0 \rangle ^ {n}$$](img/516210_1_En_2_Chapter_TeX_IEq214.png)

+   创建一个反射 Oracle ![$$U_f$$](img/516210_1_En_2_Chapter_TeX_IEq215.png)，基本上对解态添加一个负相位。该 Oracle 是一个对角矩阵。然后将该 Oracle 应用于初始化状态 ![$$U_f|s \rangle $$](img/516210_1_En_2_Chapter_TeX_IEq216.png)，在这里它对解态添加一个负相位。![$$U_f|s \rangle = (-1) ^ {f(x)} |s \rangle $$](img/516210_1_En_2_Chapter_TeX_IEq217.png)，![$$f(x) \in {0,1}$$](img/516210_1_En_2_Chapter_TeX_IEq218.png)

+   创建并应用一个额外的反射 Oracle ![$$U_s$$](img/516210_1_En_2_Chapter_TeX_IEq219.png)，它对应于初始状态接近最终状态 ![$$|s ^ {'} \rangle $$](img/516210_1_En_2_Chapter_TeX_IEq220.png)。![$$U_s$$](img/516210_1_En_2_Chapter_TeX_IEq221.png) 被认为是 Grover 的扩散算子，它围绕平均振幅给出一个反射。在第一个反射过程中由 ![$$U_f$$](img/516210_1_En_2_Chapter_TeX_IEq222.png) 降低了。在这个反射过程中，解态 ![$$|s ^ {'} \rangle $$](img/516210_1_En_2_Chapter_TeX_IEq223.png) 的振幅（带有负相位）增加到大约原来值的三倍，而空间中的其他状态的振幅降低。

可以多次重复这个过程以增加解态的概率，同时将其余状态的振幅减少到零。

如上所述，使用 Grover 算法可以在搜索未排序的数据库时获得二次加速。在摘要中挖矿的过程是找到并替换随机数值，这些随机数值由可用的与交易相关的数据、上一个区块的哈希值、时间戳的组合组成，并通过哈希算法运行以获得当前区块的哈希值 [34]。因此，通过应用 Grover 算法，如果我们可以一次考虑所有的随机数值，那么我们就可以加速搜索正确的随机数值。以下步骤考虑了使用修改后的 Grover 算法：初始设置需要将量子寄存器分成几部分，因为每个传入的数据首先与哈希状态组合，有一个寄存器用于存储所有的随机数值。每个随机数值的哈希值一个寄存器，用于存储中间计算结果的服务量子位和用于算法的功能量子位。

+   将量子寄存器分成几个部分；随机数、哈希、服务量子位和一个功能量子位。

+   使用哈达玛门操作将随机数寄存器的状态转换为一个状态的叠加。这样可以访问整个状态空间（所有随机数值）。

+   计算所有的随机数值的哈希值，并将它们存储在一个寄存器中。

+   应用 Oracle 函数到哈希寄存器，找出哪些哈希值低于某个阈值。

+   应用反向哈希计算过程，排除随机数位和功能量子位。

+   应用 Grover 的扩散操作到随机数寄存器。

与 Grover 算法一样，这也可以重复多次以获得更好的结果。

### 1.5 量子优势

对修改后的格罗弗算法的建议带来了直接的提议的量子优势。在比特币中，随机数寄存器的长度为 32 位，哈希具有 256 位哈希寄存器。与哈希值集合相比，随机数值的幂集要小得多，即使在遍历所有随机数值后，我们也可能找不到满足条件的哈希值。因此，我们将随机数寄存器扩展到 48 位。因此，经典地处理 48 位随机数需要 40 百万秒 11,000 小时或 465 天。而对于量子计算机，这个过程只需要 2 秒。因此，在理论上证明了量子优势。

#### 1.5.1 在 IBM QX 上使用量子区块链

在这里，我们将使用 IBM 量子体验构建一个量子区块链[36]。我们使用 GHZ 状态和![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq224.png)-协议来构建我们的区块链，并且在电路上执行 CNOT 攻击，模拟窃听场景（图 9 和 10）。![](img/516210_1_En_2_Fig9_HTML.png)

图 9

量子区块链的通用电路

![](img/516210_1_En_2_Fig10_HTML.png)

图 10

量子区块链在 IBM QE 上

#### 1.5.2 量子区块链构建

1.  1.

    准备 GHZ 状态。

    GHZ 状态是一种特殊的量子态，至少有三个子系统纠缠，使用一个 H 门和两个 CNOTs 制作。如下图所示。

1.  2.

    在 IBM 量子体验中实现![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq225.png)-协议

    让我们考虑 3 个参与方 A、B、C 共享 GHZ 状态，其中 B 是验证节点。作为验证者的 B 将使用 Hadamard 门生成随机角度，以及当 ![$$\theta \in 0, \pi )$$ 且 ![$$\sum _ j\theta _j = n\pi $$](img/516210_1_En_2_Chapter_TeX_IEq228.png) 时提供的 ![$$U_1$$](img/516210_1_En_2_Chapter_TeX_IEq226.png) 门。现在我们考虑 ![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq229.png) 为 ![$$\theta _1 = 0$$](img/516210_1_En_2_Chapter_TeX_IEq230.png)， ![$$\theta _2$$](img/516210_1_En_2_Chapter_TeX_IEq231.png) = ![$$\frac{\pi }{2}$$](img/516210_1_En_2_Chapter_TeX_IEq232.png)， ![$$\theta _3$$](img/516210_1_En_2_Chapter_TeX_IEq233.png) = ![$$\frac{\pi }{3}$$](img/516210_1_En_2_Chapter_TeX_IEq234.png)。因此，验证者 B 使用 H 门生成一个角度 ![$$\theta _1 = 0$$](img/516210_1_En_2_Chapter_TeX_IEq235.png)，以及 U(![$$\theta _1$$](img/516210_1_En_2_Chapter_TeX_IEq236.png))。类似地，B 使用 H 门生成一个角度 ![$$\theta _2 = 0$$](img/516210_1_En_2_Chapter_TeX_IEq237.png)，以及 U(![$$\theta _2$$](img/516210_1_En_2_Chapter_TeX_IEq238.png))。再次，B 使用 H 门生成一个角度 ![$$\theta _3 = 0$$](img/516210_1_En_2_Chapter_TeX_IEq239.png)，以及 U(![$$\theta _3$$](img/516210_1_En_2_Chapter_TeX_IEq240.png))。这就是 Theta-Protocol 在区块链中的使用方式，因为它形成一个相互连接的链条。下面是泛化电路和我们特定情况的电路。

1.  3.

    在![$$\theta $$](img/516210_1_En_2_Chapter_TeX_IEq241.png)基础上测量电路。

量子区块链的电路准备好了，我们可以使用 CNOT 攻击创建一个窃听的情况。

#### 1.5.3 CNOT 攻击

CNOT 攻击是量子密码领域的基本攻击之一，它使用 CNOT 门。在我们的案例中，我们展示了攻击者如何通过保持其量子位上的控制以及攻击者想要攻击的量子位上的目标来攻击共享的量子位。通过在 Z 基础上测量量子位，攻击者将得到结果（图见 11 和 12）。![](img/516210_1_En_2_Fig11_HTML.png)

图 11

CNOT 攻击的一般电路

![](img/516210_1_En_2_Fig12_HTML.png)

图 12

IBM QE 上的 CNOT 攻击

1.  1.

    **电路实现**：

    在上图中，明显地显示了一个 GHZ 态与 A、B 和 C 共享。其中第一、第二和第三量子位分别表示 A、B 和 C。让第![$$5{\mathrm{th}}$$](img/516210_1_En_2_Chapter_TeX_IEq242.png)量子位属于攻击者。在这里，我们使用两个辅助量子位![$$3{\mathrm{rd}}$$](img/516210_1_En_2_Chapter_TeX_IEq243.png)和![$$4{\mathrm{th}}$$](img/516210_1_En_2_Chapter_TeX_IEq244.png)来检测攻击。一种特定模式下的 4 个 CNOT 门的组合被用作检测电路。要知道电路是否受到攻击，我们必须测量辅助量子位![$$3{\mathrm{rd}}$$](img/516210_1_En_2_Chapter_TeX_IEq245.png)和![$$4{\mathrm{th}}$$](img/516210_1_En_2_Chapter_TeX_IEq246.png)。

1.  2.

    **A 的量子位被攻击**：

    GHZ 态在三个子系统之间共享，使用三个量子比特，这些量子比特分别属于 A、B 和 C，没有在额外的量子比特上进行任何操作。![$$\begin{aligned} \frac{\mathinner {|{000}\rangle } + \mathinner {|{111}\rangle }}{\sqrt{2}} \otimes \mathinner {|{00}\rangle } = \frac{\mathinner {|{00000}\rangle } + \mathinner {|{11100}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ28.png)(25)攻击者在第一个量子比特上执行了 NOT 操作。![$$\begin{aligned} \frac{\mathinner {|{10000}\rangle } + \mathinner {|{01100}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ29.png)(26)应用四个 CNOT 门，分别在第 1 和第 4、第 2 和第 4、第 2 和第 5 以及最后第 3 和第 5 个量子比特之间。前者是控制位，后者是目标位。因此状态变为;![$$\begin{aligned} \frac{\mathinner {|{10010}\rangle } + \mathinner {|{01110}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ30.png)(27)

1.  3.

    **B 的量子比特受到攻击**：

    GHZ 状态通过三个量子比特在 A、B 和 C 之间共享，而不涉及额外量子比特的任何操作。![$$\begin{aligned} \frac{\mathinner {|{000}\rangle } + \mathinner {|{111}\rangle }}{\sqrt{2}} \otimes \mathinner {|{00}\rangle } = \frac{\mathinner {|{00000}\rangle } + \mathinner {|{11100}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ31.png)(28)在这种情况下，攻击者对第二个量子比特执行 NOT 操作。![$$\begin{aligned} \frac{\mathinner {|{01000}\rangle } + \mathinner {|{10100}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ32.png)(29)应用四个 CNOT 门，分别在第 1 和第 4 个量子比特之间，第 2 和第 4 个量子比特之间，第 2 和第 5 个量子比特之间，最后第 3 和第 5 个量子比特之间。前者是控制位，后者是目标位。因此，状态变为:![$$\begin{aligned} \frac{\mathinner {|{01011}\rangle } + \mathinner {|{10111}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ33.png)(30)

1.  4.

    **C 的量子比特受到攻击**:

    GHZ 状态在三个子系统之间共享，这三个子系统使用 A、B 和 C 三个量子位，而不需要在额外的量子位上进行任何操作。![$$\begin{aligned} \frac{\mathinner {|{000}\rangle } + \mathinner {|{111}\rangle }}{\sqrt{2}} \otimes \mathinner {|{00}\rangle } = \frac{\mathinner {|{00000}\rangle } + \mathinner {|{11100}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ34.png)(31)在这里，攻击者对第三个量子位执行 NOT 操作。![$$\begin{aligned} \frac{\mathinner {|{00100}\rangle } + \mathinner {|{11000}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ35.png)(32)在第 1 个和第 4 个量子位之间，第 2 个和第 4 个量子位之间，第 2 个和第 5 个量子位之间以及最后一个第 3 个和第 5 个量子位之间应用四个 CNOT 门。前者是控制位，后者是目标位。因此，状态变为;![$$\begin{aligned} \frac{\mathinner {|{00101}\rangle } + \mathinner {|{11001}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ36.png)(33)

1.  5.

    **任何量子位上都没有攻击**:

    类似于上述情况，GHZ 状态在三个子系统之间共享，这三个子系统使用 A、B 和 C 三个量子位，而不需要在额外的量子位上进行任何操作。![$$\begin{aligned} \frac{\mathinner {|{000}\rangle } + \mathinner {|{111}\rangle }}{\sqrt{2}} \otimes \mathinner {|{00}\rangle } = \frac{\mathinner {|{00000}\rangle } + \mathinner {|{11100}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ37.png)(34)由于任何量子位都没有受到攻击，状态将保持不变。在第 1 个和第 4 个量子位之间，第 2 个和第 4 个量子位之间，第 2 个和第 5 个量子位之间以及最后一个第 3 个和第 5 个量子位之间应用四个 CNOT 门。前者是控制位，后者是目标位。因此，状态变为;![$$\begin{aligned} \frac{\mathinner {|{00000}\rangle } + \mathinner {|{11100}\rangle }}{\sqrt{2}} \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ38.png)(35)

#### 1.5.4 结果

我们在测量两个辅助量子比特以检测攻击时得到的理论结果如下：

+   ![$$\mathinner {|{1}\rangle } \otimes \mathinner {|{0}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq247.png) 当攻击者对 A 的量子比特执行 CNOT 攻击时，在电路中测量辅助量子比特时，我们得到的结果。

+   ![$$\mathinner {|{1}\rangle } \otimes \mathinner {|{1}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq248.png) 当攻击者对 B 的量子比特执行 CNOT 攻击时，在电路中测量辅助量子比特时，我们得到的结果。

+   ![$$\mathinner {|{0}\rangle } \otimes \mathinner {|{1}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq249.png) 当攻击者对 C 的量子比特执行 CNOT 攻击时，在电路中测量辅助量子比特时，我们得到的结果。

+   ![$$\mathinner {|{0}\rangle } \otimes \mathinner {|{0}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq250.png) 电路中没有攻击时的结果。

### 1.6 结论

老实说，量子区块链及相关算法离现实还很远，但这是一个开端。量子区块链领域的发展和研究可以被视为类似于量子计算领域中的原始阶段发展，如 Detuch-Jozsa 和 Shor 的因子分解算法（图 13）。

## 2 量子传感

### 2.1 介绍

随着单位的标准化，人们致力于使测量更加精确和准确。这最终引出了一个问题：我们究竟能够测量到多小的尺度？从那时起，科学家和工程师一直在探讨检测物理量（如距离、时间、质量、力等）的极限。由于观察到这些量会随环境条件的变化而变化，这导致了基于自然常数重新定义这些物理量。直到 19 世纪末，人们仍然认为只要能够设计出足够灵敏的测量设备或技术，测量可以任意精确。例如，对粒子位置的测量在经典上受限于由于平衡浴温度而产生的热噪声，这些热噪声会激发粒子运动，从而导致位置测量误差。因此，有人假设在基态时，粒子运动将完全冻结，从而消除位置测量中的任何波动。然而，随着量子力学的发展，这个假设被证明是错误的。根据量子力学的假设，每次测量都是基本不准确的。这意味着，即使在基态时，每个量子系统都有一个固有的波动，称为系统的零点运动。这个零点能量是著名的海森堡不确定性原理（方程式 36）的结果。![$$\begin{aligned} \varDelta x \varDelta p \ge \frac{\hbar }{4\pi } \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ39.png)(36)![](img/516210_1_En_2_Fig13_HTML.png)

图 13

分子动能的概念表示，作为温度的函数绘制。实线是理想值 ![$$(3/2)k_BT$$](img/516210_1_En_2_Chapter_TeX_IEq251.png)，在零温度时达到非零能量，这表示气体分子的平均零点能量 [37]

根据不确定性原理，对一个参数的准确测量会引入另一个参数的测量不准确性。这种行为是变量测量中的统计误差的结果。这种误差可以直观地看作是在测量一个变量时对另一个变量的干扰。这样两个相互影响的变量的测量被称为共轭对。这样一个共轭对的著名例子是位置和线性动量。因此，当粒子的位置被测量时，测量过程本身对粒子施加了一个反作用力，这在测量其线性动量时产生了不确定性。这意味着，测量的采样频率越高，施加在粒子上的反作用力就越大。另一方面，如果降低测量采样频率，那么测量误差与预期值的比值就会变大。因此，测量中的不确定性开始占主导地位，信噪比再次增加。因此，在任何给定的测量中存在一个最佳点，其中反作用噪声和测量噪声的总和达到最低。这种最小的额外噪声被称为系统的基态的标准量子极限（方程 37）。![$$\begin{aligned} \sqrt{S_fS_x} \approx \hbar \end{aligned}$$](img/516210_1_En_2_Chapter_TeX_Equ40.png)(37)对量子力学及其所强加的限制的理解也为在一定程度上克服这些限制铺平了道路。例如，上述的位置测量中的不确定性可以通过故意增加相干态的动量的不确定性而降低到其基态值以下。通过这种方式，量子系统的测量误差可以降低到标准量子极限所设定的值以下。这种非经典量子态被称为“压缩相干态”，现今在干涉仪实验和甚至原子钟中被普遍用于提高精度[38]。利用量子现象来提高测量灵敏度的另一个例子是量子波干涉。在这种情况下，创建两个量子态的叠加，并观察要测量的物理参数作为叠加态的概率分布的变化，以布洛赫矢量相位的变化形式呈现。因此，量子感知可以被定义为“利用受控的量子相干态来测量超出其经典极限的物理量”[39]。

### 2.2 需要量子感知

量子区域的感测可以用来测量包括但不限于距离、力、磁通量、电荷、能量、时间、相位和加速度等大范围的物理量。这些物理量的噪声功率谱密度远低于经典极限，在某些情况下甚至低几个数量级。例如，基于 SQUID 的磁力计具有高达 3 ![$$fT/\sqrt{Hz}$$](img/516210_1_En_2_Chapter_TeX_IEq252.png)的磁场灵敏度[40]，足以测量大脑产生的磁场，而自旋交换弛豫无关（SERF）原子磁力计的磁场灵敏度已经达到了 200 ![$$aT/\sqrt{Hz}$$](img/516210_1_En_2_Chapter_TeX_IEq253.png) [41]。因此，这些量子传感器在医学诊断和地理空间成像中非常有用。与此相比，经典磁力计的灵敏度仅限于几个纳米[42]。同样，原子钟极大地增强了基于卫星的导航，并且可以以不到一米的精度定位 GPS 设备。为了在地球同步轨道上提供这种位置精度，卫星中的原子钟必须具有几十阿秒数量级的艾伦偏差。这是可能的，因为使用磁光陷阱对原子进行基态冷却以减少声子诱导噪声。这为国防导航和空间任务中的定位和成像开辟了机会。除了量子传感器在工程和技术应用方面的应用之外，它们在高能粒子物理学、物理假设检验和实验天体物理学中变得越来越关键。例如，悬浮系统被提议作为测试量子引力相互作用和波函数坍缩机制的有希望平台[43, 44]。量子传感器的另一个有趣应用是通过尝试探测一些提出的暗物质粒子如轴子[45]和弱相互作用的大质量粒子（WIMPs）[46]来研究暗物质。

### 2.3 实现

量子传感器可以在任何满足 DiVincenzo-Degen 标准 [39, 47, 48] 的量子系统中实现，其标准如下：

1.  1.

    量子系统最好是具有离散和可解析能量的二能级系统，由一个恒定且有限的跃迁频率定义。![$$\mathinner {|{0}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq254.png) 和 ![$$\mathinner {|{1}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq255.png)。

1.  2.

    量子系统可以初始化为已知状态，即 ![$$\mathinner {|{0}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq256.png) 或 ![$$\mathinner {|{1}\rangle }$$](img/516210_1_En_2_Chapter_TeX_IEq257.png)，并且可以在不太影响量子系统的情况下读取其状态。

1.  3.

    应该可以以相干方式控制量子系统，最好使用时间依赖的电磁场。

1.  4.

    量子系统应能够与外部世界相互作用，以使其量子状态能够转换为可以实际测量的物理量，例如电场或磁场。

上述标准不需要完全符合，并且仅表明实际量子传感平台所需特性的指示性特征。到目前为止，有五种这样的量子系统已经显示出具有这些关键特征，以便作为量子传感基础的基础，即：

1.  1.

    光子

1.  2.

    固态自旋

1.  3.

    中性原子和离子

1.  4.

    超导器件和电路

1.  5.

    悬浮的宏观粒子

#### 2.3.1 光子

光子是具有特定能量的自然能量量子。这使得具有给定频率的光子集合彼此相同。因此，通过计数单光子源发射的光子数，可以实现高精度的传感，间接将待测信号转换为电磁波包。单光子检测和光子时间相关计数已被广泛应用于诸如成像和通信之类的技术应用中。例如，LiDAR、QKD、DNA 测序、荧光寿命成像和光子相关光谱学都基于单光子检测和/或相关技术。尽管这种方法已被广泛研究和实施，但检测信号受到射击噪声或测量噪声的限制，这降低了信噪比（SNR）。射击噪声源于光子击中探测器的数量的统计量子波动。由于这是一个随着样本大小降低而增加的统计误差，为了提高信噪比，必须对信号进行更多的平均处理。这反过来会增加测量时间，并根据实施的检测技术，可能会增加测量噪声。因此，为了进行更敏感的测量，必须使用光子的非经典态[49]。

如前述第二部分所讨论的，组合测量（shot）噪声和反作用噪声的最小值由 SQL 给出，其中位置和动量的标准差乘积等于![$$\hbar /2$$](img/516210_1_En_2_Chapter_TeX_IEq258.png)。虽然由海森堡不确定性原理给出的这一极限是测量中总误差可以达到的物理障碍，但可以通过牺牲一个变量的误差来减少另一个变量的误差，同时保持产品使海森堡不确定性原理得到遵守。这样的量子态被称为压缩相干态，其中光子位置的测量误差减少，同时使动量更加不确定[50，51]。这是通过使用非线性光学器件如光参量放大器[52]来实现的。压缩光已经在利用激光干涉测量技术的 LIGO 实验中用于探测宇宙引力波[53]。

进一步说，马赫-曾德型干涉仪可以实现超越瑞利判据的成像，因此优于经典光学成像[52, 54]。使用纠缠态和压缩光的量子干涉仪可用于创建长达数公里的干涉，因此可用于量子通信以进行加密信息传输。类似地，带有单光子源的干涉仪可以在两个纠缠单光子之间生成 EPR 相关性。这可用于量子读取光学记忆体，如 CD 和 DVD，实现无误差和更快的读取速率，并允许更密集地打包信息。这类单光子应用的主要挑战在于单光子源的效率和探测器的灵敏度。此外，必须采取措施防止光子因光吸收或退相干而丢失信息。最近，光子的明确定义属性，如频率和极化，已被用来存储量子信息。信息以非经典态的形式编码，如相干态或纠缠态。这可用于将原子的量子状态的量子信息映射到光子的量子信息上。这种光-物质相互作用在量子计算应用中得到了很好的利用，但也可用于量子传感。研究还预测了使用类似原理的量子微波光谱学和量子雷达的发展[55]（图 14 和 15）。![](img/516210_1_En_2_Fig14_HTML.png)

图 14

在位置-动量轴上显示的光的各种类型的挤压态： **a** 坐标挤压，其中标准偏差低于动量（p 轴）或位置（x 轴）的相干态![$$\hbar /2$$](img/516210_1_En_2_Chapter_TeX_IEq259.png)，以及 **b** 光子数挤压，其中光子数量的标准偏差低于相干态的标准偏差，可以是振幅挤压或相位挤压 [51]

![](img/516210_1_En_2_Fig15_HTML.png)

图 15

**a** 钻石晶体的晶格表示，显示氮注入和形成一个缺陷位点形成的彩色中心。 **b** 单个 NV 中心在零磁场下的基态和激发态之间的光学跃迁，具有两个简并的激发态，由于塞曼效应而分裂。 **c** 利用纳米金刚石中的 NV 中心的量子传感器。 微波发生器初始化 NV 中心，光学激光将电子激发到一个较高的状态，并且光致发光被光子探测器检测到 [56, 57]

#### 2.3.2 固态自旋

量子力学上，自旋磁矩仅具有两个特征值，使其成为真正的两能级系统。基于量子自旋的系统可以利用半导体衬底中的单个自旋，如捐赠者原子 [58] 或捕获电子的量子点 [59] 来发展。基于核磁共振（NMR）的自旋传感器已经实现了 20-30 fT/![$$\sqrt{Hz}$$](img/516210_1_En_2_Chapter_TeX_IEq260.png) 的灵敏度 [60]。与经典磁场传感器相比，自旋量子系统具有高灵敏度和低信噪比的优势。然而，主要挑战仍然在于将系统与背景场和杂散辐射隔离开来，这些可以在测量中添加噪声并导致量子态失相。同样，自旋系统也可以是钻石晶格中阴离子 NV 中心的集合形式 [61]。NV 中心是钻石晶格中的晶格缺陷。这些缺陷是通过将碳原子替换为氮原子来创建的，要么通过离子注入，要么通过中子或质子轰击，并且通过辐照或粒子碰撞创建的一个相邻的空位。选择在钻石晶格中的氮空位材料是为了使缺陷位点成为一种光致发光的颜色中心，并对磁场和电磁辐射作出响应。NV 中心本质上是中性的，但可以通过施加外部电压来使其带负电荷，以移动晶体的费米能级。这导致中心中的两个未配对电子形成了单态和三重态态。这些未配对电子的电子结构形成了混合态，然后可以用来响应外部磁场，其灵敏度为 1 pT/![$$\sqrt{Hz}$$](img/516210_1_En_2_Chapter_TeX_IEq261.png)。因此，纳米磁性 NV 中心可以与 AFM 探针结合用于成像和计量应用。由于其更长的相干时间，NV 中心中的自旋具有作为量子位的额外应用。

#### 2.3.3 中性原子和离子

原子具有电子构型，其中价电子可以通过吸收适当频率的光子而被激发到更高能级。因此，原子的基态和激发态可以近似为一个二能级系统，特别是如果这两个能级之间的能量间隔在原子结构中是唯一的，以至于没有其他不必要的激发可能性。类似的概念也可以应用于带电离子的情况，其具有被困在电离子阱中的可能性，从而减少离子量子态的阻尼机制。这些阱可以是光学阱，如光镊，由交替电场组成的保罗阱，或带有静电和磁场的彭宁阱（见图 16）。这些传感器可以在一秒钟内测量高达 240 nV/m 的电场，这是先前演示的其他原子传感器灵敏度的大约十倍[62]。被困离子也正在用于暗物质探测。由于困扰的性质，这些离子阱理论上可以扩展到 10 万个离子，从而使其灵敏度提高 30 倍[62]。

图 16

一组被困在彭宁阱中的铍原子（红色），使用静电和磁场进行约束。磁场导致离子在局部回旋运动中移动。这会产生离子质心运动的模式，导致整体表现得像一个弹簧质量系统[62]。

过去几十年来，中性原子和离子已被广泛用于光谱学和成像应用。例如，原子钟是一种广为人知的基于中性原子的量子传感器类型。在这里，特定原子的跃迁频率，例如铯的工作频率约为 9.19 GHz，被用于维持精确的时间。精度直接取决于原子光谱的线宽：基于锶-87 的典型光学钟（工作频率约为 429.2 THz）的 Allan 偏差约为![$$10^{-17}$$](img/516210_1_En_2_Chapter_TeX_IEq262.png)，导致每天的时间误差为 1 阿秒。大多数基于中性原子的传感器，包括原子钟，在受激拉曼跃迁的基础上工作。在这里，利用了不同捕获离子[63]和 Rydberg 原子的原子态来生成双能级系统。利用塞曼分裂，这些系统已经展示了 100 aT/![$$\sqrt{Hz}$$](img/516210_1_En_2_Chapter_TeX_IEq263.png)的磁场灵敏度[64]。甚至对于通过塞曼分裂对磁场的敏感性进行了广泛的研究。最近，光脉冲原子干涉术已被用于惯性力和时间测量[65]。这种干涉术依赖于物质的波动性，并用相干激光脉冲操纵它[66]。在这里，原子被制备成量子态，利用干涉然后自由落体。与外部力的相互作用导致干涉图案的偏差，这被两个 CCD 相机捕获并解释以记录测量。这种技术已经展示了高达![$$4 \times 10^{-8} m/s²/\sqrt{Hz}$$](img/516210_1_En_2_Chapter_TeX_IEq264.png)的加速度灵敏度[67]。

另一方面，里德堡原子是其电子被激发到非常大的主量子数 n 以实现更长的相干时间的任何原子 [68, 69]。这增加了它们对电磁场的响应，从而增加了它们对弱电磁辐射的敏感度 [70]。最近，里德堡原子还被建议在天体物理观测中扮演重要角色。在远处的恒星和星云中检测和谱测量里德堡原子可以帮助理解那里的恒星化学和气体大气。此外，测量相对论性里德堡原子亚稳态衰变的发射可以用于测试标准模型的预测（图 17）。![](img/516210_1_En_2_Fig17_HTML.png)

图 17

**a** 一种典型的里德堡原子图像，其中核心电子处于基态（灰色云）并且一个价电子处于更高的激发态（红色点状圆圈）。激发电子绕核子（黑色实心圆圈）以开普勒轨道运动，位于轨道椭圆焦点之一。 **b** 原子干涉仪的基本原理，在这里，一个真空室中的超冷原子云通过激光脉冲进行分裂。原子云然后自由下落，与外部力相互作用，再次使用另一个激光脉冲将两个云结合起来，形成干涉效应。这两个云的干涉效果如 [71] 所示。

#### 2.3.4 超导设备和电路

超导现象是物理学中著名的现象，为总共六项诺贝尔奖的获得做出了贡献。1960 年代初约瑟夫森效应的发现导致了超导量子干涉仪（SQUID）的开发，该仪器被广泛用作高灵敏度磁力计。SQUID 的噪声底线为 3 fT/![$$\sqrt{Hz}$$](img/516210_1_En_2_Chapter_TeX_IEq265.png)，在 100 Hz 时可以探测到 50 fT/![$$\sqrt{Hz}$$](img/516210_1_En_2_Chapter_TeX_IEq266.png)的磁场，并且有 50 nm 的环直径[72]。此外，中村和帕什金的开创性工作于 1999 年展示了在超导电路中的宏观量子态的相干控制[73]，其后在 2001 年展示了拉比振荡[74]。此后，通过利用库珀对隧穿的宏观量子态来实现电路量子电动力学。这些超导电路通常在硅芯片上制造，通常使用铝或铌沉积，其中可以制作 SQUID、非线性二维电磁谐振器、单库珀对盒（SCB）、超导纳米线单光子探测器（SNSPD）等器件。超导（SC）量子比特基本上是一个非谐振的 LC 振荡器，由于库珀对通过约瑟夫森结的第二量子化而展示了宏观量子行为。这些 SC 量子比特可以用作 GHz 范围内的微波信号分析仪，因此可以作为 VNA[75]。另一项研究将 SC 量子比特与铁磁晶体纠缠，并检测到了孤立的磁波包（磁子）[76]。最近的一项新提议声称，SC 量子比特可以通过与电磁场的弱相互作用来检测低质量玻色子暗物质粒子，如轴子或隐藏光子[77]（见图 18）。![](img/516210_1_En_2_Fig18_HTML.png)

图 18

**a** 超导物质之间隧道的约瑟夫逊结构，显示了两个电子（蓝色）的库珀对，这两个超导物质之间由几个纳米宽的绝缘障碍物分隔开。**b** 用作磁强计的超导量子干涉仪（SQUID）的示意图，通过一个捕获线圈将磁通转换为电压以进行通量传递。**c** SQUID 的 V versus I 图，用于零通量和一半通量量子。**d** 一个 SQUID 的 ![$$\phi $$](img/516210_1_En_2_Chapter_TeX_IEq267.png) versus V 图，显示出由于通量量子化而产生的典型正弦行为 [78]

#### 2.3.5 悬浮的宏观粒子

磁悬浮超导(SC)微粒有望实现超低机械耗散 [44]，这是由于缺乏夹持和内部材料损耗，这在夹持纳米机械谐振器中是限制因素，以及缺乏光子反冲加热，这是光悬浮实验的限制因素。这些微粒与环境的极端隔离导致长达数百毫秒的相干时间，这是产生量子态的要求。此外，磁悬浮微粒可以通过磁通与超导电路耦合，从而允许对其质心(COM)运动进行量子操作。因此，磁悬浮微粒是开发超灵敏力和加速度传感器的有前途的新平台，无论是在经典 [79] 还是量子体制下。通过在低温下使用磁场陷阱悬浮 SC 微粒，可以实现这种超灵敏平台。这些陷阱已经在芯片上实现，以更好地促进 SC 微粒与超导电路的耦合，以在量子体制下控制它们 [80]。为了将微粒的质心运动带到其运动的基态，可以实施反馈冷却或边带冷却。可以通过使用芯片上的 SQUID 磁强计来实施反馈冷却，该磁强计将检测悬浮微粒的质心运动位置。然后，可以放大 SQUID 的信号并相移，以将其反馈到磁陷阱中，以使悬浮微粒的参量冷却。一旦微粒处于基态，就可以将其耦合到超导电路，例如可调非线性 LC 谐振器或通过磁通的流量比特。最终，这种耦合允许产生 COM 运动的量子态，例如叠加态或挤压态，这可以用于感测超低力，例如重力。这个平台可以用来准备质量为 ![$$10^{13}$$](img/516210_1_En_2_Chapter_TeX_IEq268.png) a.m.u.的宏观量子态，这可以用于研究量子力学的坍缩模型。此外，这个平台在技术和基础物理学中都有应用。这种量子态的增强灵敏度可以用于建立用于导航、国防和地理空间成像的超灵敏力和加速度传感器。由于预测这种高质量谐振器的力敏感度在 zN 数量级，因此这种悬浮微粒可以用于研究重力对量子系统的影响，并可能用于探测暗物质候选体 [44, 79, 81] (图 19)。![](img/516210_1_En_2_Fig19_HTML.png)

图 19

在类似反亥姆霍兹陷阱几何结构中悬浮的超导微粒，通过迈斯纳场排斥。陷阱线圈带有电流，产生具有在陷阱中心处的场最小值的四极场[80]

### 2.4 挑战和限制

由于这些传感器的量子特性，发展商业量子传感器必须克服许多挑战。一个主要且明显的挑战是将量子系统与外部环境隔离，以获得更长的相干时间和更低的测量噪声。然而，这必须在不妨碍检测测试信号或待测物理量的情况下完成。这对噪声隔离和最终量子传感器的灵敏度构成了限制。例如，NV 中心被封装在像冷却金属或超导铌这样的磁屏蔽体中，因为它们对任何微弱的磁噪声都很敏感。然而，作为中心的宿主的金刚石晶格本身会由于碳核的随机自旋切换而引入磁场波动。这种杂散场无法屏蔽，因此限制了量子状态的相干时间。此外，量子传感平台严重依赖于量子材料研究。来自德克萨斯州 A&M 大学的 Philip Hemmer 解释了量子材料研究资金的减少如何影响了美国基于 NV 中心的量子传感器的进展[82]。

开发实用量子传感器的另一个主要挑战是可扩展性。许多量子传感器的实现可以通过增加参与检测的量子系统的数量来使其更加敏感。例如，NV 中心和被困离子在多个自旋系统的集合中使用时被认为具有出色的灵敏度。然而，扩展性可能会因各种原因而面临挑战，包括但不限于捕捉性质、随尺寸增加而增加的材料缺陷、信号强度随距离减弱（在与距离成反比的电磁信号中非常明显）、多个量子态的纠缠、随探测器数量增加而增加的测量噪声、涉及到的低温器件的尺寸等。最后一个是一个主要的关注点，不仅对于量子传感器，对于量子计算机也是如此，因为它们大多依赖某种形式的低温技术以确保有效运行。甚至像 NV 中心和被困离子这样在室温下运行良好的系统也被证明在接近 4K 的低温下表现更佳，此时的线宽足以分辨零声子线（ZPL）[83, 84]。

最后，基础设施本身对许多量子传感器构成了重大限制。例如，基于约瑟夫森结的设备需要稀释冰箱，这在实施超导量子传感器用于暗物质探测的空间应用中构成了障碍。另一个类似的限制出现在重力计传感器中。尽管这些设备非常敏感，但它们是相对重力计，因此需要定期用绝对重力计进行校准。在空间应用中，这意味着需要来回往返于太空和地球之间，这既耗时又费钱。同样，对于参与国防和导航应用的加速度传感器，迷你化和便携性是一个常见的限制。

### 2.5 应用

量子传感器被广泛用于时间测量、计量学和成像、重力和电磁力检测以及探索物理前沿。SQUIDs 和 NV-中心通常用于磁场检测，Rydberg 原子用于电场检测，中性原子用于测量时间，原子干涉仪和悬浮系统用于探测重力力、惯性加速度和旋转。然而，最近，量子传感器的更多多样化应用正在涌现，例如，可再生能源、暗物质检测、导航和测距、地球物理学和天体物理学、生物医学和医疗保健、化学和光谱学等。为了实现这些应用，已经提出了不同的实现技术。例如，在零声子线 (ZPL) 上的传感导致某些材料产生单一窄的发射带，然后可以在 NV-中心和类似六硼氮化硼的 2D 材料中用于高精度的温度和电场传感。通过光学检测磁共振，类似于 NV-中心，硅碳化物和各种稀土金属等材料可用于温度、压力、应变以及电场和磁场传感[48]。在金刚石中心的自旋弛豫可以用于化工和生物技术中检测磁离子和 pH 值。

一个全新的能源领域正在研究实施量子传感器。目的是拥有更高效、更安全和更快的能源系统。这些提议包括使用原子干涉量子传感器来检测核电厂中的辐射泄漏，进行能源监测以实现资源管理的高效性，为最佳能源消耗而设计的智能建筑和电网，用于油气和矿产储量的高精度地下扫描的重力仪，监测煤炭和天然气电厂中的 ![$$CO_2$$](img/516210_1_En_2_Chapter_TeX_IEq269.png) 排放，电网中的场传感器用于提前检测天气引起的干扰等[48]。量子传感器也正在探索在暗物质探测方面的应用。据推测，85![$$\%$$](img/516210_1_En_2_Chapter_TeX_IEq270.png) 的宇宙由暗物质组成，并有许多理论试图解释其性质和特性。然而，目前还没有检测到任何预测的暗物质粒子，研究人员希望量子传感器能够通过弱电磁相互作用来检测它们。

### 2.6 Outlook

量子传感器自 20 世纪末以来一直受到研究，但直到过去几十年才开始引起关注。它已经显示出从基础物理到先进工程和计量学的广泛应用。与它们的经典对应物相比，每种量子传感器的实施都具有独特的优势。基于光子的系统具有高灵敏度和低噪音，而最大限度压缩的光线提供了超出标准量子极限的精度。量子传感器的一个主要优势是在其实施上的灵活性：研究人员可以设计他们的传感器来检测特定的物理量，以及选择大范围的材料和物理平台来设计传感器，例如天然原子、量子点、半导体和超导电路，甚至宏观系统。这种设计的灵活性可用于开发对某种特定类型的力或能量尺度具有免疫性的量子传感器，这种力或能量尺度在测量所需的物理量时可能会起到干扰作用。例如，使用超导性可以使系统免受微弱杂散磁场的影响。同样，悬浮系统可以使量子传感器远离夹持损耗和原子间力。超导电路可以用于开发像宏观尺寸那样坚韧的类原子两能级系统。

探索量子传感的另一个优势是它在其他量子技术中的并行应用，如量子计算、量子通信和量子材料。已经在量子计算和通信方面投入了大量努力并取得了成功，这项研究也可以造福于开发更好、更多样化的量子传感器。例如，量子点技术和超导电路技术近期被提出用于传感应用。同样，量子传感的进展也可以用于解决其他量子技术领域的问题。例如，以往，钻石晶格中的被困离子和 NV 中心仅以其光谱学应用和测量磁场的超高灵敏度而闻名。然而，作为具有长相干时间的良好双能级系统，被困离子和 NV 中心都被应用于量子计算。最近，NV 中心被提议用于不仅仅是计算应用的量子比特，还用于量子信息的存储。同样，悬浮的宏观粒子也可以用于存储量子信息，尽管它们在量子计算中的应用尚待探索。此外，一个领域的研究资金也可以惠及多个领域。例如，对更好的制造工艺、低温技术和材料开发的投资将极大地推动所有量子技术领域的发展，从而可以成为合作项目或寻求研究资助的强大动力（图 20）。

图 20

从初步的学术研究到成熟的消费产品的量子传感器发展路线图[85]

最后，量子传感器现已离开学术校园，开始受到政府、企业和国际财团的关注。许多主要国家，如美国、英国、中国和印度，正在规划长期的量子技术路线图，包括量子传感，以提升其技术实力。有许多初创公司以及学术和工业衍生企业，专门致力于开发旨在研究和商业用途的量子传感器。这将同时导致供应链和增强型产业，如射频组件、低温技术、传感器和数据采集系统的增加。此外，根据 Inside Quantum Technology 2019 年的市场报告，全球量子传感器市场预计在未来十年内将增长到十亿美元[86]。因此，可以说量子传感器仍然是一个新兴领域，面临着机遇和挑战，但在研究和应用方面似乎增长迅速。因此，未来几年量子传感器的进展将使其成为量子技术的重要和关键支柱。

致谢

V. N. R. 感谢 R. Srikanth 进行讨论。作者还感谢 Admar Mutt 教育基金会的鼓励。
