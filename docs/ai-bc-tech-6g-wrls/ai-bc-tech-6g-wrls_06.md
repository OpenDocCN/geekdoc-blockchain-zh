© 作者（们），在 Springer Nature Singapore Pte Ltd 的独家许可下。 2022 年。M. Dutta Borah 等人（编）AI 与区块链技术在 6G 无线网络中的应用[`doi.org/10.1007/978-981-19-2868-0_6`](https://doi.org/10.1007/978-981-19-2868-0_6)

# 区块链分布式账本在无线通信网络中的各种应用中的安全性、隐私挑战和解决方案

Vivekanandan Manojkumar^(1  )，V. N. Sastry^(2  )和 U. Srinivasulu Reddy^(3  )(1)印度安得拉邦阿马拉瓦提，SRM 大学应用科学工程学院计算机科学与工程系(2)移动银行中心（CMB），银行技术发展与研究所（IDRBT），印度泰拉干纳，海德拉巴(3)印度泰米尔纳德邦特里钦拉普利，国立理工学院人工智能卓越中心机器学习与数据分析实验室，计算机应用系 Vivekanandan Manojkumar 邮箱：vmanojk88@gmail.comV. N. Sastry 邮箱：vnsastry@idrbt.ac.inU. Srinivasulu Reddy（通讯作者）邮箱：usreddy@nitt.edu

## 摘要

区块链是一种安全的计算技术，可以应用于各种领域，如金融、供应链管理、土地登记、医疗保健和教育。为了从各种服务提供商那里获得服务，用户或消费者通过无线通信网络向注册中心管理局（RAC）注册。然而，RAC 存在内部威胁和单点故障（SPoF）等缺陷。为了规避这些问题，如果用户对任何服务的基于区块链的注册需要通过无线通信网络进行，而且区块链网络具有用于存储用户或消费者身份信息的分布式账本（DL）。在本章中，我们将讨论上述每个应用所带来的安全和隐私问题，以及每个应用中的一些关键挑战，如数据保密性、完整性、认证、访问控制和隐私。公钥基础设施（PKI）为数据保密性、完整性和认证提供了解决方案。访问控制通过访问控制策略（限制用户权限）进行处理，隐私通过安全认证实现。

关键词隐私安全分布式账本（DL）认证访问控制医疗银行供应链管理 6G5G

## 1 引言

### 1.1 区块链

**中本聪**（Satoshi Nakamoto）[1]引入了区块链技术用于比特币加密货币，交易基于点对点模式执行，没有中央权威机构。区块链是一个安全的 DL，其中包含了一系列交易，交易记录保持在不断增长的区块链中。每个区块都通过密码学技术进行保护，以确保交易记录的完整性。新的交易记录根据共识机制添加到全局区块链中，共识机制由矿工（具有更高计算能力的矿工）执行。此外，每个区块都有整个区块的哈希值，每个区块都有前一个区块的哈希值。共识机制包括“工作量证明（PoW）”，“状态证明（PoS）”，“拜占庭容错（BFT）-基础”，“瞌睡”，“经过时间的证明（PoET）”，“权威证明（PoA）”，“声誉证明（PoR）”等。有三种类型的区块链，即“私有区块链”，“公共区块链”，“联盟区块链”。私有区块链：读取权限对所有人开放，或者读取权限仅限于特定节点网络，并且写入权限由单个组织执行。公共区块链：任何人都可以写入、发送和接收。公共区块链网络允许根据成功完成的共识机制将区块添加到区块链中。联盟区块链：仅选定的节点集合在区块链网络中具有写入权限，读取操作对所有人开放[41]。

### 1.2 区块链架构

区块链有五个层次，即物理、网络、共识、传播和应用。物理层包含区块链节点。这些节点相互连接以形成一个区块链。在区块链网络中，有两种类型的节点：全节点和轻节点。全节点包含 DL 的完整副本。全节点参与挖矿过程。如果全节点完成了成功的挖矿过程，矿工将获得奖励。轻节点不需要更高的硬件。它们只维护区块链网络的最后一个区块。信息从全节点传递到轻节点。网络层：该层提供数据传递服务。所有节点相互通信以处理共识机制。没有中央机构来批准交易。在区块链网络中，去中心化程序用于批准交易。共识层：该层负责向完成成功挖矿过程的小型节点提供激励。传播层：它具有遵循通信协议中的块和消息如何传播的规则[2]。

### 1.3 分布式账本（DL）技术

区块链网络具有 DL。DL 是一种更强大的技术，如今许多用例用于身份管理和机器对机器交易。 “去中心化”，“不可变性”和“分布式”是 DL 的属性。在去中心化中，没有单个实体来维护数据，因此它基于区块链类型在网络节点上可用。因此，它可以防止单点故障以及内部威胁。不可变性：数据记录在 DL 中，并且可以在审计过程中的任何时刻验证。分布式：所有参与的网络节点都可以访问 DL，并且基于区块链类型对所有网络节点可见。一致性，可用性和分区容忍性（CAP）是分布式系统的属性，这些特性适用于 DL。一致性属性表示所有计算节点具有 DL 的最新版本。可用性是指在网络中任何时候可以通过 DL 访问的数据总量。分区容忍性意味着如果一个或多个计算节点失败，其他节点将继续运行，确保没有单点故障。因此，基于区块链的服务适用于各种应用 [3]。

### 1.4 无线通信网络

在 1980 年代，第一代（1G）移动通信网络被引入，并且也被用于语音通信。他们使用模拟技术进行移动通信。在基于模拟到数字转换的第二代（2G）移动通信中，支持了诸如语音通信和短消息服务（SMS）等附加功能。在第三代（3G）移动通信中，引入了视频通话功能、移动电视、宽带服务和多媒体消息服务（MMS）。第四代（4G）引入了改进的宽带服务、高清视频流、IP 语音和在线游戏。5G 支持增强功能的移动宽带，数据速率可达 10 Gbps，延迟可达 1 ms，并且网络可用性达到 99.99% [43]。

### 1.5 5G 的限制和 6G 中区块链的机遇

5G 技术存在可靠性、数据速率、延迟、处理、可用性、全球覆盖、连接密度和地面覆盖等限制。这些限制在 6G 通信网络中得到了克服[43]。6G 技术具有 1Tbps 的数据速率、10ms 以下的延迟、99.99%的网络可用性、每平方公里 10⁷个设备连接的一切互联网（IoE）环境。如今，区块链是一种新兴技术，被广泛应用于诸多行业，如商业和学术等。区块链包含一个共享账本，并提供诸如非复制交易、基于保密性的身份验证和去中心化等属性。区块链在 6G 网络的分布式环境中维护着许多用户。智能合约用于在区块链中执行（用户之间同时进行）交易[44]。6G 应用于各种应用，如一切互联网（IoE）、智能电网、无人机、自动驾驶车辆、工业 5.0 和医疗保健[43]。在每个应用中，DL 技术被用于各种目的，如第四部分所述。

现在，我们在本章讨论与基于 6G 的应用相关的隐私和安全挑战，以及解决这些挑战的解决方案。每个应用程序中的一些安全和隐私关键挑战包括“数据保密性”、“完整性”、“身份验证”、“访问控制”和“隐私”。公钥基础设施（PKI）为数据保密性、完整性和身份验证提供了解决方案。访问控制由访问控制[17]策略（限制用户对资源的访问权限）处理，隐私则通过安全身份验证实现。我们在本章讨论以下主要方面：

+   基于区块链分布式账本的 6G 应用，如银行、金融、COVID-19、供应链、土地登记、医疗保健、媒体与娱乐以及教育领域；

+   每个应用程序的安全和隐私挑战；

+   解决基于区块链应用的安全挑战的解决方案。

### 1.6 章节组织

以下是本章各节组织的摘要。数学准备在第二部分中呈现，系统模型在第三部分中呈现。基于区块链分布式账本（BLT）的 6G 应用显示在第四部分中。安全分析在第五部分中呈现。基于区块链的安全协议的比较研究在第六部分中呈现。DL 隐私和安全的未来挑战在第七部分中讨论。第八部分总结了本章。

## 2 数学准备

用于解决区块链中安全和隐私问题的密码学技术[19]在基于 DL 的 6G 应用中至关重要。

### 2.1 哈希函数

定义 1

哈希函数 (H) 接受任意长度的输入，如 a ![$$\in$$] {0,1}^*，并产生固定大小的输出，如 b ![$$\in$$] {0, 1}^n，使得 b = H (a)。H 具有以下属性：

1.  1.

    单向属性：对于给定的 b，很难找到输入消息使得 b = H(a)。

1.  2.

    弱碰撞抵抗性：对于给定的输入 x，很难找到输入 y，即 y ≠ x，使得 H(y) = H(x)。

1.  3.

    强碰撞抵抗性：找到消息 1 和消息 2 对，使得 H(message1) = H(message2) 很困难。

不同哈希函数的详细信息见 Stallings [4]。

### 2.2 椭圆曲线加密 (ECC)

ECC 是公钥密码学方法之一。它基于有限域 (![$${Z}_{P}$$]) 使用椭圆曲线。椭圆曲线定义如下：

定义 2

椭圆曲线方程是 ![$${y}^{2}={x}^{3}+ax+b \: \:over \: {Z}_{P}$$]，其中 p 是素数且 p > 3，x 和 y 是方程的解 (x, y) ![$$\in$$] ![$${Z}_{P}$$] ![$$\times$$] ![$${Z}_{P}$$] 满足同余式 ![$${y}^{2}\equiv {x}^{3}+ax+b \: (mod \: p)$$]，其中 a 和 b 是常数 a, b ![$$\in$$] ![$${Z}_{P}$$]，使得 4a² + 27b² ![$$\not\equiv$$] 0 (mod p)，同时含有无穷远点。对椭圆曲线的详细解释见 Kobliz [5]。椭圆曲线可用于密钥交换、加密/解密和数字签名算法。

### 2.3 双线性配对

定义 3

设 G[1] 和 G[2] 是 E[p]（a, b）上的加法循环群和大素数 q 的乘法循环群，双线性映射 e: G[1] ![$$\times$$] G[1] ![$$\to$$] G[2] 具有以下性质：

双线性性：设 a, b ![$$\in$$](img/517376_1_En_6_Chapter_TeX_IEq16.png) Z^*[p]，A, B, C ![$$\in$$](img/517376_1_En_6_Chapter_TeX_IEq17.png) G[1]。 双线性配对 (见公式 1)：![$${{e (\alpha }}\,{ + }\,{\beta ,}\,{{\gamma ) = e (\alpha ,}}\,{\gamma )} \cdot {{ e (\beta ,}}\,{\gamma )}$$](img/517376_1_En_6_Chapter_TeX_Equ1.png)(1)![$${{e (\alpha ,}}\,{\upbeta }\,{ + }\,{{\gamma ) = e (\alpha ,}}\,{\beta )} \cdot {{e (\alpha ,}}\,{\gamma )}$$](img/517376_1_En_6_Chapter_TeX_Equa.png)![$${{e }}({{a\alpha }},{{ b\beta }}) \, = {{ e }}({{a\alpha }},{{ b\beta }})$$](img/517376_1_En_6_Chapter_TeX_Equb.png)![$$= {{ e }}({\upalpha },{\upbeta })^{{{{a}},{{b}}}} .$$](img/517376_1_En_6_Chapter_TeX_Equc.png)

非退化性：e (α, α) ![$$\ne$$](img/517376_1_En_6_Chapter_TeX_IEq18.png) 1。

可计算性：e 需要有效地计算。 Menezes 给出了详细解释[6]。

### 2.4 模糊提取器

定义 4

模糊提取器是使用用户生物特征进行用户认证的技术之一[7]。 它分别具有生成函数 Gen(.) 和再现函数 Rep(.)。 Gen(.) 获取用户的生物特征 (BIO)，并生成生物特征密钥，即，![$${\sigma }_{i}$$](img/517376_1_En_6_Chapter_TeX_IEq19.png) ![$$\in$$](img/517376_1_En_6_Chapter_TeX_IEq20.png){0,1}^a 和公开再现，即，![$${\tau }_{i.}.$$](img/517376_1_En_6_Chapter_TeX_IEq21.png) Rep(.) 接受用户生物特征 (BIO') 和公开再现字符串 ![$${\tau }_{i.}$$](img/517376_1_En_6_Chapter_TeX_IEq22.png) 作为输入，并输出生物特征密钥 ![$${\sigma }_{i}$$](img/517376_1_En_6_Chapter_TeX_IEq23.png)，使得汉明距离为计算距离 (BIO, BIO') < t，其中 t 是阈值。 模糊提取器函数的详细解释见 Dodis 等人[8]。

### 2.5 生物哈希函数

定义 5

生物哈希是使用用户生物特征进行用户认证的技术之一[9]。 它从用户获取生物特征输入，并生成称为生物码的特定代码。 生物码是根据具有随机盐值的用户输入生物特征数据生成的。 首先，从指纹或面部图像中提取特征。 然后将生物特征与随机盐值相加，最后生成生物码。 生物哈希函数的详细解释见 Lumini 和 Nanni[10]。

### 2.6 切比雪夫混沌映射

切比雪夫多项式（CP）定义为 CP[n] (x)：[–1, 1]![$$\to$$](img/517376_1_En_6_Chapter_TeX_IEq24.png)[–1,1]，基于阶数 n，并表示如下（见方程 2, 3, 4)：![$$CP_n (x) = \left\{\begin{array}{c}\mathrm{cos}\left(n.\mathit{arccos}\left(x\right)\right)if\: x \in [-1, 1]\\ \mathrm{cos}\left(n\theta \right) if \: x=\mathrm{cos}\theta , \theta \: \epsilon \left[0,\pi \right]\end{array}\right.$$](../images/517376_1_En_6_Chapter/517376_1_En_6_Chapter_TeX_Equ2.png)(2)CP 可以递归地定义如下：![$$C{P_n}\left( x \right){\text{ }} = \left\{ {\begin{array}{*{20}{l}} 1&amp;{if\,n = 1} \\ x&amp;{if\,n = 1} \\ {2x{P_{n - 1\left( x \right)}} - {P_{n - 2\left( x \right)}}}&amp;{if\,n \geqslant 2} \end{array}} \right.$$](img/517376_1_En_6_Chapter_TeX_Equ3.png)(3)

增强型 CP 的区间为 –![$$\infty , +\infty$$]，并且表现如下 [39, 40]：

![$$\mathrm{CPa }(\mathrm{CPb }(\mathrm{x})) \equiv \mathrm{CPab }(\mathrm{x}) \equiv \mathrm{ CPa }(\mathrm{x}) (\mathrm{CPn }(\mathrm{x})) (\mathrm{mod \: p})$$](img/517376_1_En_6_Chapter_TeX_Equ4.png)(4)

p 是一个素数（大），n ![$$\ge 2$$](img/517376_1_En_6_Chapter_TeX_IEq26.png)，x ![$$\in$$](img/517376_1_En_6_Chapter_TeX_IEq27.png) [–![$$\infty , +\infty ].$$](../images/517376_1_En_6_Chapter/517376_1_En_6_Chapter_TeX_IEq28.png)

## 具有 6G 应用的系统模型

图 1 显示了系统模型。在系统模型中，区块链分布式分类帐适用于基于 6G 的不同应用，如金融（银行业）、电子投票、供应链、医疗保健、媒体和娱乐、土地登记、教育、能源管理和房地产。在每个应用中，安全性和隐私性是主要挑战。在第四部分中，我们讨论了每个应用的隐私和安全挑战，并提出了解决方案！[](../images/517376_1_En_6_Chapter/517376_1_En_6_Fig1_HTML.png)

在一个以区块链分布式分类帐为核心的系统模型中，适用于基于 6G 的不同应用，如金融（银行业）、电子投票、供应链、医疗保健、媒体和娱乐、土地登记、教育、能源管理和房地产。

图 1

系统模型

## 4 区块链 DL 基于 6G 的应用

### 4.1 区块链 DL 在银行业中

在银行业中，区块链分布式账本将发挥重要作用。一般来说，所有银行交易数据都存储在中央服务器中，所有客户数据也存储在中央服务器中。因此，存在一定可能性的单点故障和内部威胁。为了避免这些问题并保持所有客户数据和客户交易数据，需要分布式服务器，即区块链。与传统银行业和金融科技 1.0 相比，金融科技 2.0（区块链+银行）提供了良好的客户体验、高效率、低成本和分布式账本安全性 [33]。

### 4.2 金融中的区块链分布式账本

在金融 [32] 行业中，区块链发挥着至关重要的作用。区块链分布式账本用于许多用途，如身份管理、完整性检查、机器对机器通信和多方计算。在身份管理中，将用户数据存储到区块链分布式账本中存在安全和隐私挑战。为了解决隐私和安全的挑战，用户数据以加密格式存储在区块链分布式账本中。在完整性检查中，用户数据的一部分存储在区块链中，在验证时，服务器将验证用户数据的完整性。在机器对机器通信中，设备在物联网环境中与区块链注册。在认证时，设备在没有 GWN/RAC 的情况下彼此认证 [35]。在多方计算中，多个节点参与计算过程，而不信任任何权威机构。在小节点成功计算后，该节点将获得工作激励 [34]。

### 4.3 COVID-19 中的区块链分布式账本

当今世界受到“冠状病毒（COVID-19）”的严重影响。根据世界卫生组织（WHO）2021 年 10 月 14 日的报告，全球约有 239,007,759 例确诊病例感染了 COVID-19 [38]，约有 4,871,841 人因冠状病毒死亡。在这种情况下，区块链分布式账本将发挥重要作用。如果有人感染 COVID-19，那么他们的数据（用户位置、用户信息等）存储在区块链分布式账本中将有助于确定他们的位置、接触追踪、家庭隔离详情等。为了保护用户隐私，用户数据是基于加密技术加密的，健康管理机构拥有加密数据的密钥。每当健康管理机构需要用户数据时，数据可以从区块链 DL 中检索，并使用私钥解密数据。

### 4.4 供应链中的区块链分布式账本

区块链分布式账本在供应链管理中用于跟踪产品信息，例如产品的创建和交付地点以及产品信息的整个历史。每当需要产品验证时，产品信息验证就从区块链分布式账本中检索出来。在食品供应链管理中[36]，区块链分布式账本维护着参与食品供应链的所有实体。这些实体包括零售商、农民、食品制造商和消费者。这些实体具有访问账本完整副本的权限。对于其他人来说，则基于访问写入权限[42]。

### 4.5 土地登记中的区块链分布式账本

为了避免欺诈和可疑登记，区块链分布式账本为土地登记的购买细节（买方和卖方信息）保留记录。

### 4.6 医疗保健中的区块链分布式账本

在医疗保健领域，患者的敏感数据存储在分布式账本中；随后，这些数据可以用于患者健康分析，DL 跟踪患者数据历史，使临床医生能够跟踪患者病况的确切情况。通过使用私有区块链，不同的组织将共享相同的患者信息分布式账本。这涉及到一些安全挑战，例如数据隐私和完整性。患者的数据根据患者的许可存储在区块链中。患者的数据是加密的，可以存储在私有区块链中以解决隐私和安全问题。

### 4.7 娱乐和媒体中的区块链分布式账本

如果娱乐媒体数据在区块链分布式账本中可用，则用户从区块链分布式账本访问媒体数据的延迟较小，并且媒体数据的质量得到提高。区块链分布式账本在所有次要节点中进行维护，因此与中心化系统相比，媒体到达用户的延迟较小。

### 4.8 教育部门中的区块链分布式账本

在教育领域，每个学生的记录都存储在分布式账本中，如果学生遗失任何信息，可以从分布式账本中恢复。DL 链接也可以提供给任何有权机构，用于基于学生访问权限的学生信息验证。

## 5 安全分析

对于安全分析协议，需要以下正式安全验证工具和正式安全分析方法[28, 29]。

### 5.1 Avispa

AVISPA 工具是一种形式化安全验证工具。在此工具中，安全协议是用 HLPSL 格式编写的。AVISPA 工具验证安全协议是否免受中间人攻击（MITM）和重放攻击。AVISPA 工具的架构由四个后端组成，如 TA4SP、CLAtSe、SATMC 和 OFMC。安全协议 [20] 是通过 HLPSL 语言编写的，并且由每个参与者角色表示。在每个参与者角色之后，还表示了会话和环境角色。AVISPA 工具支持加密、签名、哈希函数和异或操作等密码原语。在环境角色中，入侵者（i）也根据 Dolev–Yao 模型作为合法用户参与。HLPSL 通过 HLPSL2IF 翻译器转换为中间格式。中间格式（IF）通过后端（任意后端）生成输出。通过后端测试后，显示结果。从结果中，我们知道安全协议是否抵抗重放攻击和 MITM 攻击。AVISPA 工具的详细说明在指南中给出 [21]。

### 5.2 Scyther

Scyther 工具用于对安全协议进行形式化安全验证。在此工具中，假定所有的密码原语都是完美的。它基于类似于 C/java 语法。在 Scyther 工具中，安全协议是用安全协议描述语言（SPDL）来指定的。在此工具中，参与者的安全协议角色被表示出来。每个参与者角色都有一组事件，如接收、发送、声明和声明。Scyther 工具支持密码原语，如对称加密/解密、公钥基础设施、哈希函数等。输出显示了安全协议中事件的声明。详细的 Scythe 工具文档由 Cremers [22] 给出。

### 5.3 Proverif

Proverif 工具用于对安全协议进行形式化安全验证。它支持密码原语，如对称加密/解密、非对称加密/解密、数字签名、哈希函数、非交互式零知识证明和位提交。在 Proverif 工具中，安全协议是通过 pi-演算来编写的。它有三个部分，如声明、过程宏和主过程。Proverif 工具用于验证可达性、真实性和保密性。Proverif 工具具有 Dolev–Yao 威胁模型。在 Proverif 工具的输出中，它显示了三种结果，如查询为真、为假和不能证明。Blanchet 等人给出了 Proverif 工具的详细解释 [23]。

### 5.4 Tamarin Prover

Tamarin prover[24, 25]是用于验证安全协议[26]的形式安全验证工具。Tamarin prover 工具的输入是安全协议模型。安全协议模型是基于参与安全协议的实体的不同角色构建的，并且涉及对手。Tamarin prover 支持额外的加密技术，例如双线性配对和 Diffie–Hellman 指数运算。Tamarin prover 工具提供两种方法构造证明，完全自动化模式和交互模式。详细解释见 Li 等人[18]。

### 5.5 BAN 逻辑

BAN 逻辑是由伯罗斯等人提出的[27]。BAN 逻辑用于分析安全协议的形式安全证明[22, 23]。在 BAN 逻辑中，包括假设、规则和证明。假设（假设）是为了分析安全协议而进行的，并且这种假设是基于新鲜度构建的。假设用于证明安全协议以避免重放攻击。在 BAN 逻辑中，根据证明的规则，如消息含义、随机数验证、权限、新鲜度和信任，实现安全协议的目标。BAN 逻辑的详细解释由伯罗斯等人[27]给出。

### 5.6 RoM 模型

随机预言模型（Random oracle Model，RoM）是由贝拉雷和罗加威提出的[27]。RoM 模型[30] 用于安全协议的形式安全分析。它是一个黑匣子。黑匣子根据个别查询从其输出域中给出随机响应输出。如果查询多次重复，同样的方法会响应请求的查询。RoM 模型的详细解释在贝拉雷和罗加威[27]中给出。

## 6 比较分析

### 6.1 DL-Based 安全协议的比较研究

Jangirala 等人[11]设计了基于区块链的 RFID 启用的供应链身份验证协议，使用 5G 技术进行移动边缘计算。在他们的协议中，他们设计了基于哈希函数、异或运算和位移运算的协议。会话密钥是在供应链节点和标签（T）之间与读取器（T）的帮助下生成的。他们使用 AVISPA 工具进行了非正式和形式安全验证的安全分析。Jangirala 等人[11]的协议不使用正式分析进行验证，通信成本较高。

Guo 等人[12]提出了一种基于区块链的边缘计算认证协议。他们的协议是基于椭圆曲线密码学（ECC）、双线性配对设计的，并采用了联合区块链进行身份验证。在他们的协议中，共识算法用于存储认证日志并基于区块链网络验证身份。他们使用 MATLAB 和 Hyperledger Fabric 进行了模拟。他们的协议的安全分析使用了较少的参数，并且他们的协议没有使用“正式安全分析”和“正式安全验证”。

Lin 等人[13]设计了一种基于区块链的智能家居“相互认证”协议。他们的协议是基于公钥加密和群签名设计的。他们使用了基于 PBFT 共识机制的许可区块链来支持他们的协议。该“相互认证”是在家庭网关和用户之间执行的。他们协议的缺点是：没有进行正式的安全验证。

Odelu[14]设计了基于生物特征的用户认证协议，使用联合区块链进行身份管理。他们的协议是基于双线性配对和椭圆曲线密码学开发的。在他们的协议中，在初始化阶段，注册中心（RC）和认证服务器（AS）生成公/私钥对，并使用其公钥加入到区块链网络中。在用户注册阶段，RC 为用户生成一些秘钥，并将用户信息放入区块链网络中。在认证阶段，用户向认证服务器发出带有其身份的登录请求，认证服务器将利用区块链验证身份。在验证身份后，用户和认证服务器之间生成会话密钥（SK）用于安全通信。在他们的协议中，他们使用联合区块链对用户的身份进行验证。他们通过非正式安全分析进行了安全分析。该协议的缺点是他们没有进行“正式安全分析”，“正式安全验证”，而且他们的协议需要高通信和计算成本。

Kumar 等人[15]建议使用基于可加 Elgamal 同态加密的区块链进行虹膜认证。在他们的协议中，他们使用同态加密，哈希函数和区块链。 在他们的协议中，他们使用区块链进行身份验证。 在注册阶段时，加密的用户虹膜模板与用户身份信息一起存储在区块链中。 在身份验证时，客户端设备将用户身份和加密的用户虹膜模板发送到区块链，区块链从服务器获取加密的用户虹膜模板。 区块链计算加密用户虹膜模板的哈希值，最后，区块链比较用户虹膜模板值和检索到的服务器值。 如果两个值相同，则区块链计算距离，并可将其发送到客户端设备进行身份验证测试。 他们方案的缺点是在身份验证阶段不提供用户匿名性和不可追踪性属性，不提供正式的安全性分析和不具有正式的安全性验证。

沈[16]设计了基于区块链的智能城市环境中物联网（IoT）数据的支持向量机（SVM）训练。在他们的方法中，他们使用同态加密系统来保护物联网数据，并使用区块链存储加密的物联网数据。 SVM 用于数据分类及其应用有疾病诊断和异常检测。 训练和测试阶段是基于存储在区块链中的加密数据进行的。

张等人[18]设计了通过区块链对抗拖延审计员的云存储中存储的数据的完整性检查。在他们的协议中，他们使用哈希函数，双线性配对和区块链。 他们有五个阶段，例如设置，存储，审计，日志生成和检查日志。 在设置阶段，初始参数由密钥生成中心（KGC）确定。 在存储阶段，用户（U）将其数据与一些安全参数（SP）（即数据（D[i]），即 I = 1 到 n，SP）一起外包到云中。 在审计阶段，第三方审计员借助区块链检查云中外包用户数据的完整性。 在生成日志阶段，第三方审计员生成日志文件，并将日志文件上传到区块链中。 在检查日志阶段，用户审计存储在区块链中的日志文件。 他们方案的缺点是他们只对一些攻击进行了安全性分析，并没有进行详细的安全性分析，“没有进行正式的安全性验证”，并且外包的数据块是明文格式。

### 6.2 量化分析

表 1 显示了基于 DL 的协议的量化分析。表 1

量化分析

| 作者和年份 | 使用的加密技术和技术 | 安全性分析 | 缺点 |
| --- | --- | --- | --- |
| Jangirala et al. [11] | 哈希，异或，位旋转操作和区块链 | 非正式，使用 AVISPA 进行形式化安全验证 | 没有通过正式分析进行验证，通信成本高 |
| Guo et al. [12] | ECC，双线性配对和联盟区块链 | 非正式 | 安全分析是在较少的参数下进行的，没有使用正式安全分析和正式安全验证进行验证 |
| Lin et al. [13] | 公钥加密，群签名，权限区块链 | 随机预言模型，非正式安全分析 | 没有通过正式安全验证进行验证 |
| Odelu [14] | 双线性配对，ECC，联盟区块链 | 非正式 | 没有通过非正式安全分析和正式安全验证进行验证，通信和计算成本高 |
| Kumar et al. [14] | Elgamal 同态加密，区块链，哈希函数 | 非正式 | 在认证时不提供用户匿名性和不可追踪性，没有提供正式的安全分析，并且没有正式的安全验证 |
| Shen [16] | 同态加密系统，区块链，支持向量机 | 安全证明 | 没有正式的安全验证和正式的安全分析 |
| Zhang et al. [18] | 哈希，双线性配对和区块链 | 非正式 | 没有进行详细的安全分析，没有正式的安全验证，并且外包的数据块是明文格式 |

## 7 未来挑战

+   在区块链中，使用分布式账本来解决中心化系统的问题，但网络中的每个节点都需要大量的存储空间来存储区块链。

+   在区块链网络中，攻击的可能性为 51%。为解决这些问题，需要采用密码学技术来进行安全数据存储。我们在第 2 和 5 节中分别列出了一些密码学技术和一些安全分析方法。

+   挑战在第 6.4 节中进行了讨论。在文献调研中，我们还讨论了基于区块链的安全协议，并列出了现有工作的安全挑战。

+   量子攻击可能对 PKI 方案造成影响，因此需要采用基于格的密码学技术来解决安全和隐私挑战。

## 8 结论

在本章中，我们分析了基于区块链分布式账本的应用程序的各种安全和隐私挑战，并提出了一些基于区块链分布式账本的最新安全协议。解决基于区块链分布式账本应用程序的安全和隐私挑战的解决方案得到了解决。基于“区块链分布式账本”的应用程序的安全和隐私挑战在未来将发挥重要作用。

致谢

作者们感谢 SRM 大学 - 安得拉邦分校，印度安得拉邦，印度国家理工学院，特里琴拉帕利，以及印度德里银行科技研究所，还有匿名审稿人、编辑和副编辑们的宝贵建议。
