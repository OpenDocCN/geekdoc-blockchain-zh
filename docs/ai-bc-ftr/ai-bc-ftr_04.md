© 作者，独家许可给 Springer Nature Switzerland AG 2021Y。Maleh 等人（编辑）未来网络安全应用的人工智能和区块链大数据研究 90[`doi.org/10.1007/978-3-030-74575-2_3`](https://doi.org/10.1007/978-3-030-74575-2_3)

# 基于区块链加密 IoMT 数据的隐私保护多变量回归分析

Rakib Ul Haque^(1, 2  )和 A. S. M. Touhidul Hasan^(2, 3  )(1)中国科学院大学计算机科学与技术学院，北京市石景山区，100049，中国(2)孟加拉国达卡自动化研究与工程学院，达卡，1205，孟加拉国(3)亚太大学计算机科学与工程系，达卡，1205，孟加拉国 Rakib Ul Haque 邮箱：rakibulhaqueraj@mails.ucas.ac.cnA. S. M. Touhidul Hasan（通讯作者）邮箱：touhid@uap-bd.edu

## 摘要

大多数与保护医疗物联网（IoMT）数据的隐私保护线性回归训练相关的研究并不能满足数据所有者的所有隐私问题。本文提出了一种安全设计，以在训练线性回归模型时保护 IoMT 数据的隐私问题。区块链与称为 Paillier 的部分同态加密系统一起使用，以保护所有参与者的数据隐私。为了消除第三方的领土，所提出的研究将安全构建块集成到安全线性回归中。首先，在各种数据提供者之间开发了一个受保护的数据共享平台，其中加密的 IoMT 数据被注册到一个共享账本上。其次，利用 Paillier 的同态属性概述了安全多项式操作（SPO）和安全比较（SC）。安全线性回归不需要任何可信的第三方。每次迭代只需要三次交互。严格的安全性调查证明了安全线性回归保留了每个数据提供者和分析员的敏感数据隐私。安全线性回归分别在 BCWD、HDD 和 DD 数据集上实现了 0.78、0.066 和 0.196 的调整![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq1.png)。安全线性回归的性能几乎与一般线性回归相似。

## 1 引言

由于医疗物联网（IoMT）的广泛利用，个人和许多医疗机构已经收集了大量的数据[1]。这导致各个数据所有者之间信息的协作提取的扩展。大多数数据所有者缺乏进行数据挖掘所需的资源和专业技能。通常，数据所有者将这些任务外包给服务提供商。然而，在许多情况下，数据所有者出于与数据所有权、完整性和隐私相关的隐私问题的考虑而不愿共享他们的数据，例如，任何制药公司希望估计针对重病患者的各种处方策略的影响。个人的处方策略可能是特定对称的各种药物的混合物。制药公司准备共享他们的数据以便在假设所有参与者的隐私得到很好保护的情况下对合并数据集进行分析。

差分隐私[2]、密码学[3]和隐私保护数据发布[4–7]等研究考虑了数据保密性的问题，每种方法都在效率、时间复杂度和数据分析方面存在局限。另一方面，参与者信息的记录并未存储在这些方法中。SecureSVM[8]和安全![$$k-$$](img/507793_1_En_3_Chapter_TeX_IEq2.png) nn[9]等是一些最近的解决方案，其中区块链被整合以在模型训练时保留参与者的信息，并建立与标准方法相似的最接近可能的精度。再次，一些工作直接关注隐私保护线性回归[10–14]，但它们都没有涵盖现实生活中所有的隐私需求，并且没有利用区块链技术进行工作。

在这项工作中，我们介绍了基于加密系统的隐私保护安全线性回归，以缓解前述的担忧。一个名为 Paillier 的部分同态公钥加密系统[15]与区块链和加密的 IoMT 数据集成，以采用安全的线性回归来保护数据所有者的隐私。所提出的方法应用了使用 Paillier 的同态特性作为线性回归的安全构建块，其中线性回归具有基本的算术运算和比较，如下所讨论：

+   安全多项式运算（SPO）：用于在 Paillier 上进行加法和减法的计算。

+   安全比较（SC）：用于在 Paillier 上比较任何数字。

安全的线性回归每次迭代只需要三次交互，并且不需要可信任的第三方。其主要贡献如下。

+   区块链技术建立了数据所有者和数据分析师之间的安全可靠的数据共享。一个唯一的交易被开发用于在区块链上记录加密数据。

+   使用 Paillier 采用 SPO 和 SC 等安全构建模块组装安全线性回归算法，每次迭代中有三次交互，并且不需要信任第三方。

+   细致的调查表明，安全的线性回归可以保护数据隐私，并且能够达到与标准线性回归相似的性能。

接下来的研究结果如下。2 和 3 部分分别阐述了初步和系统概述。4 和 5 部分分别展示了模型构建和性能评估。本文总结于第六部分。

## 2 初步

本节讨论了所有符号和背景技术。

### 2.1 符号说明

![$$x_{i}$$](img/507793_1_En_3_Chapter_TeX_IEq3.png) 和 ![$$y_{i}$$](img/507793_1_En_3_Chapter_TeX_IEq4.png) 是数据集 *D* 中的第$$i^{th}$$个属性，共有 *m* 条记录。在分类属性之后，属性 ![$$x_{i}$$](img/507793_1_En_3_Chapter_TeX_IEq6.png) 和 ![$$y_{i}$$](img/507793_1_En_3_Chapter_TeX_IEq7.png) 获得标签 ![$$l_{i}$$](img/507793_1_En_3_Chapter_TeX_IEq8.png)。*P* 和 *A* 分别表示数据所有者和数据分析师。[[*m*]] 表示在 Paillier 下的消息加密。所有符号均在表 1 中描述。表 1

符号说明

| 符号 | 解释 | 符号 | 解释 |
| --- | --- | --- | --- |
| *P* | 数据所有者 | *A* | 数据分析师 |
| *D* | 数据集 | *x* | *D* 中的自变量 |
| *y* | *D* 中的因变量 | *m* | *D* 中的记录数 |
| *n* | *D* 中的自变量数量 | ![$$\alpha $$](img/507793_1_En_3_Chapter_TeX_IEq9.png) | 学习率 |
| ![$$\sum _{i=1}^{m} \theta _{i}$$](img/507793_1_En_3_Chapter_TeX_IEq10.png) | 回归系数 | ![$$\sum _{i=1}^{m} h_{\theta }^{i}$$](img/507793_1_En_3_Chapter_TeX_IEq11.png) | 假设函数 |
| ![$$J_{\theta }$$](img/507793_1_En_3_Chapter_TeX_IEq12.png) | 代价函数 | ![$$\sum _{i=0}^{n} \theta _{i}$$](img/507793_1_En_3_Chapter_TeX_IEq13.png) | 梯度下降函数 |
| *PK* | 公钥 | *SK* | 私钥 |
| ![$$\pi $$](img/507793_1_En_3_Chapter_TeX_IEq14.png) | 协议 | ![$$\delta $$](img/507793_1_En_3_Chapter_TeX_IEq15.png) | 偏差 |
| ![$$x_{i},y_{i}$$](img/507793_1_En_3_Chapter_TeX_IEq16.png) | 数据集中的第$$i^{th}$$个记录 | ![$$\phi (N)$$](img/507793_1_En_3_Chapter_TeX_IEq18.png) | 欧拉费函数 |
| ![$$l_{i}$$](img/507793_1_En_3_Chapter_TeX_IEq19.png) | 类标签 | [[*message*]] | 使用 Paillier 加密的加密消息 |

### 2.2 同态加密系统

公钥密码系统中使用一对密钥（*PK*； *SK*）。例如，私钥 *SK* 和公钥 *PK* 用于加密和解密。如果在不知道解密密钥的情况下，加密系统的特征能够将密文的计算映射到相应的明文，那么它被称为同态。在提议的方案中，使用了部分同态密码系统（Paillier [15]），它允许多项式运算，如安全加法和减法。设 *n* 位素数为 *p* 和 *q*，则 ![$$N = pq$$](img/507793_1_En_3_Chapter_TeX_IEq20.png)。*N* 是公钥，而 ![$$(N,\phi (N))$$](img/507793_1_En_3_Chapter_TeX_IEq21.png) 是私钥。Paillier 的加密函数为 ![$$c:=[[(1+N)^{m} r^{N} \;mod\; N^{2}]]$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq22.png)，其中解密函数为 ![$$m \in \mathbb {Z}_{N}$$](img/507793_1_En_3_Chapter_TeX_IEq23.png)，且 ![$$m:=[[\frac{[c^{\phi (N)} \; mod \; N^{2}-1]}{N} \times \phi (N)^{-1}mod \; N]]$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq24.png)。

### 2.3 区块链

使用加密系统连接和保护的交易的连接递增记录称为区块链 [16]。区块链采用点对点（P2P）协议来处理单点故障。共识机制确保交易和区块的普遍、明确的规范。

### 2.4 线性回归

线性回归 [17] 是一种简单的估计分析方法。这些近似通常被用来描述一个因变量和一个或多个自变量之间的关系。回归分析的三种主要技术是：

+   预测器准确性的测量

+   效果预测

+   趋势预测

回归分析所需的公式如下列所示。

假设函数的方程 1:![$$\begin{aligned} h_{\theta }=\theta _{0}+(\theta _{1} * x_{1})+...+(\theta _{n}+x_{n}) \end{aligned}$$](img/507793_1_En_3_Chapter_TeX_Equ1.png)(1)成本函数的方程 2:![$$\begin{aligned} J_{\theta }= \frac{1}{2m} * \sum _{i=1}^{m} (h_{\theta }^{i} - y^{i})^{2} \end{aligned}$$](img/507793_1_En_3_Chapter_TeX_Equ2.png)(2)梯度下降函数，当![$$j=0$$](img/507793_1_En_3_Chapter_TeX_IEq25.png)遵循方程 3，当![$$j&gt;0$$](img/507793_1_En_3_Chapter_TeX_IEq26.png)遵循方程 4:![$$\begin{aligned} \theta _{j=0} = \theta _{j=0} - \alpha * \frac{1}{m} \sum _{i=1}^{m} (h_{\theta }^{i} - y^{i}) \end{aligned}$$](img/507793_1_En_3_Chapter_TeX_Equ3.png)(3)![$$\begin{aligned} \sum _{j=1}^{n} \theta _{j} = \sum _{j=1}^{n} \theta _{j} - \alpha * \frac{1}{m} \sum _{i=1}^{m} (h_{\theta }^{i} - y^{i}) x_{j}^{i} \end{aligned}$$](img/507793_1_En_3_Chapter_TeX_Equ4.png)(4)

## 3 系统概述

本节演示了使用的系统模型、线程模型和安全定义。

### 3.1 系统模型

该模型的主要焦点是确保*P*和*A*之间的安全数据共享。各自的*P*将其加密数据分享给*A*并将其注册在基于区块链的分布式记录中，形成交易。*A*可以通过累积记录在公共账本中的加密数据来训练其线性回归算法。*A*可以基于安全构建块（如 SPO 和 SC）组装安全方法。在训练过程中，*A*和*P*之间的相互作用至关重要，用于共享中间结果。*P*在分享中间数据时将添加少量偏差(![$$\delta $$](img/507793_1_En_3_Chapter_TeX_IEq27.png))。这种偏差将保护数据隐私并减少算法的时间和空间复杂度。这种偏差对分类结果没有负面影响。该偏差主要用于安全比较加密数字。图 1 说明了整个过程。

+   **IoMT 设备:** 通过无线网络传输 IoMT 数据的设备。

+   **数据所有者** *P***:** 收集来自 IoMT 设备的所有数据的实体或个人。

+   **数据分析员** *A***:** 能够进行数据分析的实体或个人。

![../images/507793_1_En_3_Chapter/507793_1_En_3_Fig1_HTML.png](img/507793_1_En_3_Fig1_HTML.png)

图 1

数据驱动的 IoMT 生态系统

通常，提出的系统由一个不受信任的数据分析员*A*和*n*个数据所有者$$P_{i} (i \in {1, ..., n})$$ 组成。每个个体![$$P_{i}$$](img/507793_1_En_3_Chapter_TeX_IEq29.png) 拥有包含重要信息的数据集![$$D_{i}$$](img/507793_1_En_3_Chapter_TeX_IEq30.png)。考虑了水平数据共享[18]，其中*n*个数据集![$$\{D_{i}\}_{i=i}^{n}$$](img/507793_1_En_3_Chapter_TeX_IEq31.png) 具有相似的特征空间但样本不同。*A* 顺序收集*n*个加密数据，并在样本集![$$D := (D_{1} \,\cup \, ....\, \cup \, D_{n})$$](img/507793_1_En_3_Chapter_TeX_IEq32.png) 上训练线性回归模型。运行隐私保护训练协议 ![$$\pi $$](img/507793_1_En_3_Chapter_TeX_IEq33.png) 后，*A* 可以实现期望的模型。

**安全目标：** 隐私保护的训练协议 ![$$\pi $$](img/507793_1_En_3_Chapter_TeX_IEq34.png) 满足以下要求。

+   *A* 无法从数据集*D*中学到任何重要信息。

+   每个*P*都无法区分模型参数。

+   每个*P*都无法了解其他*P*的敏感信息。

### 3.2 威胁模型

提出的模型中的所有参与者都不信任彼此。本研究将所有参与者视为诚实但好奇的对手。本节将讨论线程模型。

*A* 在遵循预先设计的 ML 训练协议时是诚实的！$$\pi $$。*A* 还对数据的详细信息感兴趣，并尝试通过分析计算的中间数据获得额外的知识。同样，*P* 可能会尝试从中间数据中识别*A*的设计参数。

+   已识别的密文模型。*A* 只能获取记录在区块链平台上的加密信息。在训练安全方法时，*A* 可以记录中间输出，例如迭代步骤。

+   已识别的后端模型。*A*预期对已公开的密文模型中能区分的细节更加了解。*A*可以与不同的*P*共谋，以获取另一个*P*的重要数据。

### 3.3 通过区块链共享加密数据

本研究认为所有相似的数据实例都分配了各自的特征向量，并在本地预处理。交易被定义为在区块链中累积加密的*D*。预期的交易形成主要基于两个领域：输入和输出。输入字段包括：

+   发件人地址

+   数据的加密版本

+   源 IoMT 设备名称

相应的输出终端包括：

+   收件人地址

+   数据的加密版本

+   源 IoMT 设备名称

发件人和收件人的地址将是哈希值。加密数据来自部分同态加密系统（Paillier）。私钥和每个加密数据实例的长度为 128 字节，并记录在区块链中。IoMT 设备类型的段长度为 4 字节。组装新事务后，发送节点将其广播到区块链网络的 P2P 系统中。矿工节点正在验证操作的正确性。特定矿工节点将交易打包到新块中。使用传统共识协议，即 PoW 机制，将块添加到当前链中。单个块可能注册多个交易。

### 3.4 安全定义

该研究采用了安全两方计算框架[19]。模块化顺序组合[20]被应用于以模块化方式将安全构建块组合成 PPML 训练协议。

**安全两方计算。** 对于两方协议，为了确保安全，我们必须展示无论*A*（*B*）从与*B*（*A*）的交互中计算出什么，都可以从其输入和输出中计算出来，这导致了一种常用的定义，即安全两方计算[19]。令![$$F=(f_{A}, f_{B})$$](img/507793_1_En_3_Chapter_TeX_IEq36.png)为（概率性的）多项式函数。![$$\pi $$](img/507793_1_En_3_Chapter_TeX_IEq37.png) 是计算*F*的协议。A 和 B 希望计算*F*（*a*, *b*），其中*a*是 A 的输入，*b*是 B 的输入。在执行![$$\pi $$](img/507793_1_En_3_Chapter_TeX_IEq38.png) 过程中，A 的视图是元组![$$view^{\pi }_{A} (a,b) = (a, r, m_{1}, m_{2}, ..., m_{n})$$](img/507793_1_En_3_Chapter_TeX_IEq39.png)，其中![$$m_{1}, m_{2}, ..., m_{n}$$](img/507793_1_En_3_Chapter_TeX_IEq40.png)是从 B 接收到的消息，*r*是 A 的随机带。B 的视图定义类似。安全两方计算的形式化陈述如下：

定义 1（安全两方计算[19]）。如果对于所有可能的输入（*a*, *b*）和模拟器![$$S_{A}$$](img/507793_1_En_3_Chapter_TeX_IEq42.png)和![$$S_{B}$$](img/507793_1_En_3_Chapter_TeX_IEq43.png) 都满足以下属性，则两方协议![$$\pi $$](img/507793_1_En_3_Chapter_TeX_IEq41.png) 私下计算*f*：![$$\begin{aligned}&amp;S_{A}(a,f_{A}(a,b)) \equiv _{c} view_{A}^{\pi } (a,b)\\&amp;S_{B}(b,f_{B}(a,b)) \equiv _{c} view_{B}^{\pi } (a,b) \end{aligned}$$](img/507793_1_En_3_Chapter_TeX_Equ6.png)

其中![$$\equiv _{c}$$](img/507793_1_En_3_Chapter_TeX_IEq44.png)表示对于在安全参数![$$\lambda $$](img/507793_1_En_3_Chapter_TeX_IEq45.png)下具有可忽略优势的概率多项式时间(*PPT*)对手的计算不可区分性[15]。

**模块化顺序组合。**由于我们所有的协议都是以模块化方式设计和构建的，我们采用模块化顺序组合[20]来证明我们协议的安全性。

定义 2

(模块化顺序组合[20])。设![$$f_{1}, . . . , f_{n}$$](img/507793_1_En_3_Chapter_TeX_IEq46.png)是双方概率多项式时间功能，![$$\rho _{1}, . . . , \rho _{n}$$](img/507793_1_En_3_Chapter_TeX_IEq47.png)是在半诚实对手存在的情况下分别安全地计算![$$f_{1}, . . . , f_{n}$$](img/507793_1_En_3_Chapter_TeX_IEq48.png)的协议。让*F*是一个概率多项式时间功能，![$$\pi $$](img/507793_1_En_3_Chapter_TeX_IEq49.png)是一个在半诚实对手存在的情况下安全地计算*F*与![$$f_{1}, . . . , f_{n}$$](img/507793_1_En_3_Chapter_TeX_IEq50.png)的协议。那么![$$\pi ^{\rho _{1}, . . . , \rho _{n}}$$](img/507793_1_En_3_Chapter_TeX_IEq51.png)在半诚实对手存在的情况下安全地计算*F*。

## 4 模型构建

本节介绍了提议模型的构建细节。目标是在训练多个来自不同*P*的私有数据集上训练线性回归模型时保护不同*P*和*A*的隐私。

### 4.1 安全多项式运算（SPO）

开发了安全多项式加法和安全多项式减法来训练使用 Paillier 的提议安全线性回归方法。在加法、减法和乘法时可以实现可靠性。Paillier 的加法同态属性推导如下: ![$$[[m_{1}+m_{2}]] = [[m_{1}]] \times [[m_{2}]]$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq52.png) (*mod* ![$$N^{2})$$](img/507793_1_En_3_Chapter_TeX_IEq53.png)，减法推导为: ![$$[[m_{1}-m_{2}]] = [[m_{1}]] \times [[m_{2}]]^{-1} (mod N^{2}) [[[m]]^{-1}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq54.png) 表示模取余的乘法逆。在 Paillier 中可以计算 ![$$[[m]] \times [[m]]^{-1} (mod N^{2}) = 1$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq55.png)。![$$[[m]]^{-1}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq56.png) 可以由 ![$$\phi (N)$$](img/507793_1_En_3_Chapter_TeX_IEq57.png) 函数计算，![$$[[m]]^{-1} = [[m]]^{\phi (N)-1}]$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq58.png)。同样，密文操作可以实现表示在方程 (5) 中的安全多项式乘法。![$$\begin{aligned}{}[[am_{1}+bm_{2}]]=[[m_{1}^{a}]] \times [[m_{2}^{b}]] (mod \quad N^{2}) \end{aligned}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_Equ5.png)(5)然而，本研究需要安全多项式减法和加法。Paillier 是统计不可区分的，因此安全多项式减法和加法也是类似的 [15]。

### 4.2 安全比较（SC）

它指的是加密数字之间的安全比较。假设，*A* 和 *B* 参与了安全比较算法，以便比较遵循协议 ![$$\pi $$](img/507793_1_En_3_Chapter_TeX_IEq61.png) 的 ![$$[[m_{1}]]$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq59.png) 和 ![$$[[m_{2}]]$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq60.png)，并且任何一方都无法获得原始的 ![$$m_{1}$$](img/507793_1_En_3_Chapter_TeX_IEq62.png) 和 ![$$m_{2}$$](img/507793_1_En_3_Chapter_TeX_IEq63.png)。算法 1 表示安全比较算法。![../images/507793_1_En_3_Chapter/507793_1_En_3_Figa_HTML.png](img/507793_1_En_3_Figa_HTML.png)命题 1

(安全比较算法)**。** 算法 1 在好奇但诚实的模型中是安全的。

***证明（命题的证明*** 1***）。*** 在算法 1 中涉及两个实体（*P* 和 *A*）。函数 *F* : ![$$\begin{aligned} F([[m_{1}']]_{A}, [[m_{2}']]_{A}, PK_{A}, SK_{A})= (\phi , (m_{1} \ge m_{2})) \end{aligned}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_Equ7.png)*P* 的视角是![$$\begin{aligned} view_{P}^{\pi }=([[m_{1}']]_{A}, [[m_{2}']]_{A}, PK_{A}) \end{aligned}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_Equ8.png)因此，模拟器： ![$${S_{P}^{\pi }}((m_{1},m_{2});$$](img/507793_1_En_3_Chapter_TeX_IEq64.png)![$$\begin{aligned} F(m_{1},m_{2}))= view_{P}^{\pi }([[m_{1}]]_{A}, [[m_{2}]]_{A}, [[\delta ]]_{A}, PK_{A}) \end{aligned}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_Equ9.png)其中 ![$$[[m_{1}]]_{A}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq65.png) 和 ![$$[[m_{2}]]_{A}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq66.png) 被 ![$$PK_{A}$$](img/507793_1_En_3_Chapter_TeX_IEq67.png) 加密，而 ![$$[[m_{1}]]_{A}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq68.png) 和 ![$$[[m_{2}]]_{A}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq69.png) 的保密性类似于 Paillier。因此，*P* 没有机会推断出原始值。*A* 的视角是![$$\begin{aligned} view_{A}^{\pi }= (([[m_{1}']]),([[m_{2}']]), PK_{A}, SK_{A}) \end{aligned}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_Equ10.png)接下来， ![$${S_{A}^{\pi }}$$](img/507793_1_En_3_Chapter_TeX_IEq70.png) 运行如下：![$$\begin{aligned} F(m_{1}',m_{2}') = view_{A}^{\pi } (m_{1}', m_{2}', PK_{A}, SK_{A}) \end{aligned}$$](img/507793_1_En_3_Chapter_TeX_Equ11.png)*A* 永远无法从 ![$$(m_{1}')$$](img/507793_1_En_3_Chapter_TeX_IEq73.png) 和 ![$$(m_{2}')$$](img/507793_1_En_3_Chapter_TeX_IEq74.png) 恢复原始值，因为 *A* 不知道偏置 ![$$\delta $$](img/507793_1_En_3_Chapter_TeX_IEq75.png)。*A* 将根据条件 ![$$(m_{1}')$$](img/507793_1_En_3_Chapter_TeX_IEq78.png) ![$$\ge $$](img/507793_1_En_3_Chapter_TeX_IEq79.png) ![$$(m_{2}')$$](img/507793_1_En_3_Chapter_TeX_IEq80.png) 或 ![$$(m_{1}')$$](img/507793_1_En_3_Chapter_TeX_IEq81.png) < ![$$(m_{2}')$$](img/507793_1_En_3_Chapter_TeX_IEq82.png) 返回 0 或 1，因为 *A* 忠实于遵守协议。   ![$$\square $$](img/507793_1_En_3_Chapter_TeX_IEq83.png)

### 4.3 安全线性回归的训练算法

本研究采用轻量级受保护的线性回归训练协议来保护所有参与方的模型参数。假设有一个单一的*A*和*n*个*P*。算法 2 详细说明了提议的训练协议。在算法 2 中，*A*的模型参数和*P*的敏感数据是保密的。每个参与者永远不会从算法的中间结果中推断出其他参与者的任何敏感数据，即使面对任何好奇但诚实的对手或勾结。![../images/507793_1_En_3_Chapter/507793_1_En_3_Figb_HTML.png](img/507793_1_En_3_Figb_HTML.png)命题 2

(安全性![$$Protocol_{\pi }$$](img/507793_1_En_3_Chapter_TeX_IEq84.png))**.** 在算法 2 中，![$$Protocol_{\pi }$$](img/507793_1_En_3_Chapter_TeX_IEq85.png) 在好奇但诚实的模型下是安全的。

***证明（命题证明*** 2***）。*** *P* 和 *A* 是参与算法 2 的 ![$$Protocol_{\pi }$$](img/507793_1_En_3_Chapter_TeX_IEq86.png) 中的角色。每个 *P* 的功能都是相似的。如果其中一个 *P* 满足安全规范，那么所有 *P* 都将满足安全要求。函数 F：![$$\begin{aligned} F(D, (PK,SK)_{A}, \alpha , \sum _{i=0}^{n} \theta _{i})= (\phi ,(\sum _{i=0}^{n} \theta _{i}^{'}) \end{aligned}$$](img/507793_1_En_3_Chapter_TeX_Equ12.png)各个 IoMT 数据所有者 *P* 的视图是 ![$$\begin{aligned} view_{P}^{Protocol_{\pi }}=(D, [[\alpha ]]_{PK_{A}},[[\sum _{i=0}^{n} \theta _{i}]]_{PK_{A}},PK_{A}) \end{aligned}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_Equ13.png)，其中 ![$$[[\alpha ]]_{PK_{A}}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq87.png) 和 ![$$[[\sum _{i=0}^{n} \theta _{i}]]_{PK_{A}}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq88.png) 都由 ![$$PK_{A}$$](img/507793_1_En_3_Chapter_TeX_IEq89.png) 加密，![$$[[\alpha ]]_{PK_{A}}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq90.png) 和 ![$$[[\sum _{i=0}^{n} \theta _{i}]]_{PK_{A}}$$](../images/507793_1_En_3_Chapter/507793_1_En_3_Chapter_TeX_IEq91.png) 的机密性等同于密码系统 Paillier。因此，没有一个 *P* 可以直接推断出值。*A* 的视图是 ![$$\begin{aligned} view_{A}^{Protocol_{\pi }}= (PK_{A}, SK_{A}, \sum _{i=1}^{m} (h_{\theta }^{i} - y^{i}), (\alpha \times (\sum _{i=1}^{m} (h_{\theta }^{i}-y^{i}) \times x_{j}^{i}))) \end{aligned}$$](img/507793_1_En_3_Chapter_TeX_Equ14.png)现在，需要讨论 ![$$\sum _{i=1}^{m} (h_{\theta }^{i} - y^{i})$$](img/507793_1_En_3_Chapter_TeX_IEq92.png) 和 ![$$(\alpha \times (\sum _{i=1}^{m} (h_{\theta }^{i}-y^{i}) \times x_{j}^{i}))$$](img/507793_1_En_3_Chapter_TeX_IEq93.png) 的机密性，即 *A* 是否可以从这些值中预测个人 *P* 的私有 *D*。显然，![$$\sum _{i=1}^{m} (h_{\theta }^{i} - y^{i})$$](img/507793_1_En_3_Chapter_TeX_IEq94.png) 和 ![$$(\alpha \times (\sum _{i=1}^{m} (h_{\theta }^{i}-y^{i}) \times x_{j}^{i}))$$](img/507793_1_En_3_Chapter_TeX_IEq95.png) 对于未知的 *D* 没有解。*A* 可能尝试使用已知的值 ![$$\alpha $$](img/507793_1_En_3_Chapter_TeX_IEq96.png) 和 ![$$\sum _{i=0}^{n} \theta _{i}$$](img/507793_1_En_3_Chapter_TeX_IEq97.png) 计算未知的 *D*。在除法时，*A* 有一些中间值，还知道 *m*。但是，*A* 永远也无法猜到 *P* 的确切 *D*。除了蛮力破解外，没有更可靠的方法来感知 *D* 的真实值。假设，每个 *P* 都有一个由 100 个实例组成的二维有限数据集。每个维度都是 32 位 [通常，单精度浮点数占用 4 字节（32 位）内存空间]。基于这个条件，*A* 成功猜测的概率是 ![$$\frac{1}{2^{(n\times 6400)}}$$](img/507793_1_En_3_Chapter_TeX_IEq98.png)。这是一个微小的可能性 [15]。因此，![$$\pi $$](img/507793_1_En_3_Chapter_TeX_IEq99.png) 在诚实但好奇的模型中是安全的。 ![$$\square $$](img/507793_1_En_3_Chapter_TeX_IEq101.png)的安全性，该方法在算法 2 中使用，因此在诚实但好奇的情况下，它是安全的。

## 5 性能评估

此部分代表了提议系统的性能分析。

### 5.1 测试床

每个*P*从 IoMT 设备收集所有数据，并在建议的系统中对其进行加密。所有操作都在装有内存（4 GB 1600 MHz DDR3）、Intel Core i5 处理器（2.5 GHz）的 MacBook Pro 上同时进行。 SC、SPO 和安全线性回归在浏览器中实现：Google Chrome；语言：Python 3；平台：Google 的 Collaboratory。

### 5.2 数据集

三个真实世界的数据集，即糖尿病数据集（DD）、心脏病数据集（HDD）和威斯康星乳腺癌数据集（BCWD）[21, 22]。 BCWD 的特征代表了图像中细胞核和乳腺肿块的描述。 HDD 和 DD 分别包含 13 个离散属性和 9 个数值属性。 根据实例分类的心脏疾病和糖尿病症状是类型。 表 2 表示数据集的统计信息。 数据集的 80% 和 20% 分别用于模型的训练和测试。表 2

数据集的统计信息

| 数据集 | 实例数量 | 属性数量 | 离散属性 | 数值属性 |
| --- | --- | --- | --- | --- |
| DD | 768 | 9 | 0 | 9 |
| HDD | 303 | 13 | 13 | 0 |
| BCWD | 699 | 9 | 0 | 9 |

### 5.3 浮点格式转换

标准线性回归可以在浮点数和整数上进行训练，但密码系统执行它们的操作时必须是整数。因此，必须执行格式转换并将所有数字转换为整数。根据全球标准 IEEE 754 对浮点二进制数的表示为*D*为![$$D=(-1)^{s} \times M \times 2^{E}$$](img/507793_1_En_3_Chapter_TeX_IEq102.png)[其中符号位为*s*，有效数字为*M*，指数位为*E*]。

### 5.4 密钥长度设置

公钥密码系统的安全性与长度严格相关。一些问题包括：

+   如果密钥过于紧凑，可能会导致易受攻击的加密。

+   如果密钥太长，同态操作的效率可能会降低。

+   如果密钥太短，可能会导致明文空间的溢出。

因此，估算密钥的大小以避免拥塞的概率是至关重要的。在安全线性回归中，Paillier 密码系统的密钥大小*N*被固定为 1024 位。

### 5.5 评估参数

对于评估回归算法的四种最流行的方法如下：

+   R-squared (![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq103.png))是由预测变量解释的结果变化的关系。R-squared 值越高，模型越好。调整后的 R-squared 是![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq104.png)的一种版本，它调节了设计中生成多个变量的![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq105.png)。

+   均方根误差（RMSE）衡量了模型在预测观测结果时的平均误差。![$$MSE = mean((observeds - predicteds)²)$$](img/507793_1_En_3_Chapter_TeX_IEq106.png)和![$$RMSE = \sqrt{MSE}$$](img/507793_1_En_3_Chapter_TeX_IEq107.png)。RMSE 值越低，模型越好。

+   AIC 代表（赤池信息准则）。AIC 惩罚将额外变量纳入模型。它结合了一个增强添加额外项时的失败的学科。AIC 值越低，模型越好。AICc 是对小单位大小进行了调整的 AIC 的版本。

+   BIC（或贝叶斯信息准则）是 AIC 的一种替代方法，对模型中持有额外变量的惩罚更大。

结果显示在表 3 中。在 BCWD 数据集上，安全线性回归分别在![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq108.png)、调整![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq109.png)、RMSE、AIC 和 BIC 上获得了 0.79、0.78、0.031、−424.03 和−2169.72 的分数，与标准线性回归几乎相似。表 3

性能分析

| 数据集 | 测量 | 标准线性回归 | 安全线性回归 |
| --- | --- | --- | --- |
| BCWD | ![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq110.png) | 0.83 | 0.79 |
| 调整后的![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq111.png) | 0.814 | 0.78 |
| RMSE | 0.038 | 0.031 |
| AIC | −438.66 | −424.03 |
| BIC | −2224.51 | −2169.72 |
| HDD | ![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq112.png) | 0.54 | 0.43 |
| 调整后的![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq113.png) | 0.08 | 0.066 |
| RMSE | 0.115 | 0.136 |
| AIC | −69.84 | −123.83 |
| BIC | −477.75 | −655.13 |
| DD | ![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq114.png) | 0.26 | 0.37 |
| 调整后的![$$R^{2}$$](img/507793_1_En_3_Chapter_TeX_IEq115.png) | 0.214 | 0.196 |
| RMSE | 0.171 | 0.193 |
| AIC | −253.94 | −537 |
| BIC | −1296.36 | −1468.43 |

### 5.6 效率

表 4 显示了在加密数据集上使用 SPO 的执行时间。它还说明了 *P* 和 *A* 的总时间消耗。表 4

时间消耗

| 数据集 | SC | SPO | 安全线性回归 |
| --- | --- | --- | --- |
| BCWD | 1245 秒 | 3842 秒 | 4131 秒 |
| DD | 985 秒 | 2988 秒 | 3766 秒 |
| HDD | 542 秒 | 1679 秒 | 2133 秒 |

表 4 展示了安全线性回归的结果。对于 DD、HDD 和 BCWD 数据集，以加密形式进行训练消耗不到一小时。在时间消耗方面表现良好。在 Python 中，多线程被用于实现，以限制较大数据集的执行时间。我们以多种 *P* 进行了线性模拟。因此，表 4 显示了不同 *P* 的总耗时。*P* 可以并行运行他们的方法，以减少 SPO 和 SC 的执行时间。

## 6 结论

本研究介绍了一种新颖的隐私保护框架，用于对加密 IoMT 数据进行线性回归训练。在数据提供者和数据分析师之间进行安全数据共享，以训练线性回归算法是本研究的主要关注点。所提出的安全线性回归方法确保了 IoMT 数据的隐私和完整性。许多 IoMT 数据提供者发送他们的数据，并在多方场景下应用区块链技术来训练 ML 算法。为了建立更好的模型，采用了部分同态加密系统。区块链用于记录所有交易。本研究展示了安全线性回归的性能和安全性。这种推荐方法在准确度上大致与标准线性回归相当。

致谢

作者感谢中国科学院大学计算机科学与技术学院，中国北京，以及亚洲太平洋大学计算机科学与工程系，孟加拉国达卡，对本研究的支持。