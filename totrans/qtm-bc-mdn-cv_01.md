© 作者，Springer Nature Switzerland AG 2022 独家许可。A. Kumar 等人（编辑）。《现代计算系统的量子和区块链：愿景与进展》数据工程与通信技术讲义 133[`doi.org/10.1007/978-3-031-04613-1_1`](https://doi.org/10.1007/978-3-031-04613-1_1)

# 量子技术 I：信息、通信与计算

Emilio Peláez^(1    ), Minh Pham^(1    ) 和 U. Shrikant^(2    ) (1)芝加哥大学，芝加哥，IL，美国(2)数学科学研究所，金奈，印度 Emilio Peláez（通讯作者）电子邮件：epelaez@uchicago.eduMinh Pham 电子邮件：mpham26@uchicago.eduU. Shrikant 电子邮件：shrikantu@imsc.res.in

## 摘要

在本章中，我们介绍了一些量子信息科学的概念，包括信息、信息安全、纠缠态、量子门、量子隐形传态、直接安全通信、量子秘密共享、量子噪声、量子操作、量子纠错、量子电路和量子 Toffoli 门。其中大部分概念在量子增强技术中至关重要，包括量子区块链。本章的目标是介绍量子信息科学方面的基本概念，以及其实时需求和用途，包括一些关于上述概念和工具如何在量子区块链技术中发挥作用的注释。本章分为三个主要部分，如下所述。首先，从量子力学的假设开始，该假设规定了与经典力学明显不同的基本规则。然后我们在第一部分中介绍了量子信息（QI）科学的基本概念，如摘要所述。第二部分专门介绍了多控制 Toffoli 门，该门可能在量子计算的多个领域以及量子区块链中找到应用。第三部分专门讨论了量子纠错的某些方面，这是一种保护量子比特（量子信息的单位）免受环境噪声干扰的方案，有助于发展容错的量子技术。在结论部分，我们指出本章内容如何与量子区块链技术相关。附录中给出了符号表。  

## 1 量子信息

量子信息（QI）科学现在吸引着来自不同学科的科学家。过去的十年对于量子信息科学来说是密集的，无论是在理论上还是在实验上。各个公司和学术界已经宣布了所谓的“量子霸权”的实现，这个术语是由约翰·普雷斯基尔创造的。一方面，量子计算机据说能够胜过任何现有的经典（数字）计算机，这在今天仍然是一个有争议的话题。然而，真正的量子霸权实例挑战了任何经典算法，即使在理论上也是如此。另一方面，量子密码学提供的无条件安全性为未来的量子技术和安全通信带来了巨大的希望。更不用说，已经实现了非常长距离和基于卫星的量子密钥分发。目前，我们生活在嘈杂中等规模量子（NISQ）时代，在这个时代，NISQ 设备已经被用于学术和工业目的。

提出量子信息在物理学基础中的实用性是相关的，比如凝聚态理论、统计力学、热力学、黑洞信息悖论、量子理论基础，以及通过 AdS/CFT 对应求解量子引力理论长期难题包括弦理论等等。它提供了一个无需担心使用什么物理系统来研究理论的普遍语言。例如，在离散变量设置中，一个量子态是一个密度算子，无论我们是在非相对论还是相对论量子理论中讨论。量子理论的奇妙之处在于它在量子信息科学中找到了巨大的应用，但在基础层面仍然神秘莫测。

然而，本章节的目的和范围仅限于介绍量子信息科学的基本概念。读者应该具备量子力学和线性代数的基本知识，以及一些概率论的基础。我们不希望在本节中涵盖所有的话题，而只涵盖在量子区块链技术中应用的量子信息的基础。我们将提及快速应用于量子密码学和通信的示例。

### 1.1 量子力学的假设

这里我们将采用密度矩阵方法来处理量子力学，因为它为量子信息理论提供了最通用的语言。

**态和算符**。一个量子态由希尔伯特空间中的一个向量给出。一个状态更一般地用一个密度矩阵表示，具有以下属性：它是厄米的： ![$$\rho = \rho ^\dagger $$](img/516210_1_En_1_Chapter_TeX_IEq1.png)，具有单位迹： Tr![$$(\rho ) =1$$](img/516210_1_En_1_Chapter_TeX_IEq2.png)，且是半正定的： ![$$\rho \ge 0$$](img/516210_1_En_1_Chapter_TeX_IEq3.png)。由于每个厄米算符都有一个谱分解，因此状态可以写成 ![$$\rho = \sum _i \lambda _i \left| {e_i} \right\rangle \left\langle {e_i} \right| $$](img/516210_1_En_1_Chapter_TeX_IEq4.png)。这里， ![$$ \left| {e_i} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq5.png) 是 ![$$\rho $$](img/516210_1_En_1_Chapter_TeX_IEq6.png) 的特征向量，具有相应的特征值 ![$$\lambda _i$$](img/516210_1_En_1_Chapter_TeX_IEq7.png)，要求 ![$$\sum _i \lambda _i = 1$$](img/516210_1_En_1_Chapter_TeX_IEq8.png) 和 ![$$0 \le \lambda _i \le 1$$](img/516210_1_En_1_Chapter_TeX_IEq9.png)。所有的*可观察量*必然是厄米算符，因此具有实特征值。这符合实验中观察到的情况。一个可观察量的平均值由 ![$$\langle O \rangle = \text {Tr}(O \rho )$$](img/516210_1_En_1_Chapter_TeX_IEq10.png) 给出。

*混合态*是那些满足![$$\text {Tr}(\rho ²) &lt; 1$$](img/516210_1_En_1_Chapter_TeX_IEq11.png)的态，*纯态*是那些满足![$$\text {Tr}(\rho ²) = 1$$](img/516210_1_En_1_Chapter_TeX_IEq12.png)的态。我们稍后将看到，在噪声演化下，一个纯态将被转化为混合态，因此密度矩阵形式主义上提供了量子信息和统计性质理论的最通用语言。

**动力学**。量子动力学由一个酉矩阵给出，该矩阵将一个量子态映射到另一个量子态：![$$\rho ^\prime = U \rho U^\dagger $$](img/516210_1_En_1_Chapter_TeX_IEq13.png)，其中![$$U = \text {exp}\{- i H t / \hbar \}$$](img/516210_1_En_1_Chapter_TeX_IEq14.png)是酉矩阵，*H*是时间平移的生成器。动力学仅适用于闭合系统且是可逆的，酉算符将正交态映射到正交态。我们稍后将看到，对于更一般的（例如有噪声的）演化，动力学可能不是酉的和可逆的。

**测量和概率**。在量子力学中，一个测量由满足条件的一组测量算符![$$\{M_i\}$$](img/516210_1_En_1_Chapter_TeX_IEq15.png)给出，满足条件![$$\sum _i M^\dagger M \le \mathbbm {1}$$](img/516210_1_En_1_Chapter_TeX_IEq16.png)。得到结果*i*的概率以及测量后的更新状态分别为![$$\begin{aligned} p(i) = \text {Tr}[M_i \rho M_i^\dagger ] \quad ; \quad \rho \rightarrow \rho ^\prime = \frac{M_i \rho M_i^\dagger }{p(i)}. \end{aligned}$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_Equ1.png)(1)量子力学中的测量理论涉及两种类型：投影算符测量（PVM）和正算符值测量（POVM）。事实上，测量是一个*不可逆*的过程，通过它可以了解系统的状态。一旦测量过，状态就不可逆地*坍缩*到其中一种基态中，其中测量的状态被展开。量子理论预测的是在测量后才能揭示的获得特定基态的概率。量子测量确实作为量子和经典世界之间的桥梁。一旦测量过，量子状态坍缩，量子信息就减少到经典信息！

**复合系统**。一个多部分状态由各个部分的张量积给出。例如，一个通用的双量子比特状态可以表示为 ![$$ \left| {\psi } \right\rangle ^{AB} = \sum _{i,j} p_{ij} \left| {\phi _i} \right\rangle \otimes \left| {\phi _j} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq17.png)，其中 ![$$\otimes $$](img/516210_1_En_1_Chapter_TeX_IEq18.png) 表示张量积。如果一个多部分状态能够被写成各个部分的张量积，则称其为*可分离*的。然而，量子力学允许存在不能被写成边缘状态张量积的状态，具有这种非可分离联合状态的粒子被称为量子相关。在接下来的章节中将介绍例子。

### 1.2 经典和量子信息

古典信息和量子信息在*本质上*是不同的[1, 3]。古典信息的基本单位是*比特*，如逻辑/物理上的 0 或 1。量子信息则以“量子比特”*qubit*的形式讨论信息，它是两种状态的量子*叠加*： ![$$ \left| {\text {qubit}} \right\rangle = \frac{1}{\sqrt{2}}( \left| {0} \right\rangle + \left| {1} \right\rangle )$$](img/516210_1_En_1_Chapter_TeX_IEq19.png)，其中 ![$$ \left| {0} \right\rangle = \begin{bmatrix} 1 \\ 0 \end{bmatrix} $$](img/516210_1_En_1_Chapter_TeX_IEq20.png) 和 ![$$ \left| {1} \right\rangle = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$](img/516210_1_En_1_Chapter_TeX_IEq21.png)。这些矩阵可以被看作是对应于两级量子系统的正交状态，比如光子的极化度或电子的自旋度。实际上，这些自由度定义了我们正在谈论的量子系统的类型，更确切地说，维度确定了系统的类型。在本小节中，我们将定义一些主要的信息度量，包括古典和量子。并进一步提及这些定义在量子信息科学中的一些用途。

1948 年，香农[4]提出了信息的抽象理论，彻底改变了信息科学领域。给定一个二进制位序列，其以某种概率出现为 ![$$p_i$$](img/516210_1_En_1_Chapter_TeX_IEq22.png)，那么信号中包含的信息简单地表示为 ![$$I = - \sum _i \log p_i$$](img/516210_1_En_1_Chapter_TeX_IEq23.png)。这告诉我们，事件越不可能发生，其包含的信息就越多！一般来说，这样的抽象理论能够提供一种信息处理语言，不依赖于使用了什么物理系统。现在众所周知，*信息是物理的*，正如兰道尔[5]所说，“信息不是抽象的实体，而是仅通过物理表示存在”，因此受到物理定律的限制。

正如早些时候所指出的，经典信息通常由二进制位 0 和 1 表示。经典计算遵循布尔代数。我们在这里不会过多地讨论经典计算，而是将重点放在对量子通信和密码学有用的要素上。经典通信是通过将这些位编码到物理系统中并发送到通信信道中来完成的。最常用的通信形式是使用电磁波，而通信信道是自由空气或光纤电缆。

在经典信息理论[4, 6]中，信号中的信息被编码为对应于以某种概率发生的事件的经典比特。考虑一个随机变量 ![$$A \in \{a_1,a_2...\}$$](img/516210_1_En_1_Chapter_TeX_IEq24.png)，称为源，其符号为 ![$$a_1,a_2... $$](img/516210_1_En_1_Chapter_TeX_IEq25.png)，等等，分别以概率 ![$$p_1,p_2...$$](img/516210_1_En_1_Chapter_TeX_IEq26.png) 发生。然后，*香农熵*（SE），用于量化 *A* 中的信息，定义为概率的负对数的平均值：![$$\begin{aligned} H(A) = - \sum _a p(A=a) \log (p(A=a)). \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ2.png)(2)这里，*H*(*A*) 是 SE，![$$p(A=a)$$](img/516210_1_En_1_Chapter_TeX_IEq27.png) 是随机变量 *A* 取随机值 *a* 的概率。除非另有说明，否则始终取对数为 2。基于上述定义，可以继续定义源自多个源的信息的各种测量，比如随机变量 *A* 和 *B*。*条件熵*（CE）量化了已知 *Y* 时通过测量 *A* 获得的信息量：![$$\begin{aligned} H(A \vert B) = - \sum _{a,b} p(a \vert b) \log [p(a \vert b)]. \end{aligned}$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_Equ3.png)(3)*A* 和 *B* 的*联合熵*（JE）是通过测量 *A* 和 *B* 获得的信息：![$$\begin{aligned} H(A,B) = - \sum _{a,b} p(a,b) \log [p(a,b)] \end{aligned}$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_Equ4.png)(4)其中 *p*(*a*, *b*) 是 *A* 和 *B* 的联合概率分布。JE 实际上衡量了关于 *A*、*B* 的总不确定性。事实上，CE 和 JE 由表达式 ![$$H(A,B) = H(A) + H(A \vert B)$$](img/516210_1_En_1_Chapter_TeX_IEq28.png) 相关联。而香农熵具有由不等式 ![$$H(A,B) \le H(A)+ H(B)$$](img/516210_1_En_1_Chapter_TeX_IEq29.png) 给出的子可加性性质，在 *A* 和 *B* 依赖时成立不等式，当它们独立时成立等式。

由于量子态可以被视为概率的综合，通过简单地用密度矩阵替换概率分布，可以写出*冯诺伊曼熵*：![$$S = - \text {Tr}(\rho \log \rho )$$](img/516210_1_En_1_Chapter_TeX_IEq30.png)。由于每个自伴算符都是正常算符，可以给出谱分解(![$$\rho = \sum _i p_i \left| {i} \right\rangle \left\langle {i} \right| $$](img/516210_1_En_1_Chapter_TeX_IEq31.png))，因此冯诺伊曼熵在基础上化简为香农熵(2)，基是![$$\{ \left| {i} \right\rangle \}$$](img/516210_1_En_1_Chapter_TeX_IEq32.png)，这些是![$$\rho $$](img/516210_1_En_1_Chapter_TeX_IEq33.png)的本征向量，![$$p_i$$](img/516210_1_En_1_Chapter_TeX_IEq34.png)是算符![$$\rho $$](img/516210_1_En_1_Chapter_TeX_IEq35.png)的本征值。

用量子版本替换经典熵测量的每个定义，可以通过用密度矩阵(![$$\rho $$](img/516210_1_En_1_Chapter_TeX_IEq37.png))替换经典概率分布(![$$p_i$$](img/516210_1_En_1_Chapter_TeX_IEq36.png))和用迹操作替换求和(![$$\sum _i$$](img/516210_1_En_1_Chapter_TeX_IEq38.png))来获得。例如，条件熵是![$$S(\rho _A\vert \rho _B) = S(\rho _{AB}) - S(\rho _A)$$](img/516210_1_En_1_Chapter_TeX_IEq39.png)，其中![$$S(\rho _A) = - \text {Tr}(\rho _A \log \rho _A)$$](img/516210_1_En_1_Chapter_TeX_IEq40.png)和![$$S(\rho _{AB}) = - \text {Tr}\rho _{AB} \log \rho _{AB}$$](img/516210_1_En_1_Chapter_TeX_IEq41.png)，是*A*和*B*的联合熵。

#### 1.2.1 距离度量和保真度

在经典信息理论中，一个常见的问题是询问任意两个概率分布有多接近，以及一个人能够多好地区分它们。一个距离度量告诉我们两个概率分布的差异有多大。在经典信息理论中，人们学习到了柯尔莫哥洛夫距离[1]：给定两个概率分布*p*和*q*，它们之间的距离由以下公式给出：![$$d(p,q) = \frac{1}{2}\sum _i \vert p_i-q_i \vert $$](img/516210_1_En_1_Chapter_TeX_IEq42.png)。然而，在量子信息理论中，定义了许多等价的距离度量。例如，任意两个量子态![$$\rho _1$$](img/516210_1_En_1_Chapter_TeX_IEq43.png)和![$$\rho _2$$](img/516210_1_En_1_Chapter_TeX_IEq44.png)之间的迹距离被定义为：![$$\begin{aligned} D(\rho _1, \rho _2 ) = \frac{1}{2}\Vert (\rho _1-\rho _2) \Vert _1 \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ5.png)（5），其中![$$\Vert A \Vert _1 = \sqrt{A^\dagger A}$$](img/516210_1_En_1_Chapter_TeX_IEq45.png)是操作符 A 的![$$L_1$$](img/516210_1_En_1_Chapter_TeX_IEq46.png)范数或迹范数。实际上，迹距离给出了一个上限，表明在量子通道上可以可靠传输多少信息，同时距离是在状态![$$\Phi [\rho ]$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq47.png)和![$$\rho $$](img/516210_1_En_1_Chapter_TeX_IEq48.png)之间计算的，其中![$$\Phi $$](img/516210_1_En_1_Chapter_TeX_IEq49.png)是量子通道^[1]。人们还可以定义一个量度来量化两个状态有多接近，这就是保真度：![$$F = \text {Tr}(\rho _1 \rho _2) $$](img/516210_1_En_1_Chapter_TeX_IEq50.png)。保真度还有其他有用的形式，比如由 R Josza 提出的形式：![$$\begin{aligned} F = (\text {Tr}\sqrt{\sqrt{\rho _2} \rho _1 \sqrt{\rho _2}})²\. \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ6.png)（6）。乌尔曼定理指出，鉴于一个状态![$$\rho _1$$](img/516210_1_En_1_Chapter_TeX_IEq52.png)的“净化”![$$ \left| {\phi _{\rho _1}} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq51.png)，其中![$$\{ \left| {i} \right\rangle \}$$](img/516210_1_En_1_Chapter_TeX_IEq53.png)是![$$\mathcal {H}^k$$](img/516210_1_En_1_Chapter_TeX_IEq54.png)中的正交基，则保真度![$$\begin{aligned} F(\rho _1,\rho _2) = \underset{{ \left| {\phi _{\rho _1}} \right\rangle }}{\text {max}}\; | \langle \phi _{\rho _1} \vert \phi _{\rho _2} \rangle |² \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ8.png)（8）量化了纯化之间的最大重叠。有趣的是，迹距离（5）是保真度的上限：![$$\begin{aligned} F(\rho _1,\rho _2) \le 1 - \frac{1}{4}\Vert \rho _1 - \rho _2 \Vert ²\. \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ9.png)（9）。另一个众所周知的距离度量是布尔斯距离：![$$\mathcal {B} = \sqrt{2-2\sqrt{F(\rho _1,\rho _2)}}$$](img/516210_1_En_1_Chapter_TeX_IEq55.png)，其中![$$F(\rho _1,\rho _2)$$](img/516210_1_En_1_Chapter_TeX_IEq56.png)是等式(6)中给出的保真度。

#### 1.2.2 纠缠态

量子纠缠[7]是量子系统之间的一种空间相关性，无法用经典资源创建。它在量子信息科学的许多领域中找到应用，特别是量子通信和密码学。

一个空间量子相关状态的例子是纠缠（贝尔）态：![`$$\begin{aligned} \left| {\phi } \right\rangle _{ij} = \frac{1}{\sqrt{2}}( \left| {0j} \right\rangle + (-1)^i) \left| {1\bar{j}} \right\rangle \end{aligned}$$`](img/516210_1_En_1_Chapter_TeX_Equ10.png)(10)在这里，当 ![$$ \left| {j} \right\rangle = \left| {0} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq57.png)时，![$$ \left| {\bar{j}} \right\rangle = \left| {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq58.png)。以上四个贝尔态 ![$$ \left| {\phi } \right\rangle _{ij}$$](img/516210_1_En_1_Chapter_TeX_IEq59.png) 是正交的，并形成所谓的贝尔基 ![`$$\{ \left| {\phi } \right\rangle _{00}, \left| {\phi } \right\rangle _{01}, \left| {\phi } \right\rangle _{10}, \left| {\phi } \right\rangle _{11}\}$$`](img/516210_1_En_1_Chapter_TeX_IEq60.png)。然而，还有其他特殊类别的*混合*纠缠态，比如 Werner 态：在 (10) 给出的四个贝尔态的凸混合！`$$\begin{aligned} \left| {\Psi } \right\rangle ^\mathrm{\small Werner} = f \left| {\phi } \right\rangle _{00} + \frac{1}{3}(1 - f) ( \left| {\phi } \right\rangle _{01} + \left| {\phi } \right\rangle _{10} + \left| {\phi } \right\rangle _{11} ) \end{aligned}$$`(11)它仅在 ![`$$ \frac{2}{3} \le f \le 1$$`](img/516210_1_En_1_Chapter_TeX_IEq61.png) 时纠缠。这表明最大纠缠态的叠加不一定是最大纠缠的。即使在今天，多粒子纠缠理论也没有完全发展。然而，有一类状态，称为 GHZ^(2)态，在量子信息科学中找到应用。由[8]给出的多量子比特 GHZ 态![`$$\begin{aligned} \left| {GHZ} \right\rangle = \frac{1}{\sqrt{2}}( \left| {000 \cdots 0} \right\rangle + \left| {111 \cdots 1} \right\rangle ). \end{aligned}$$`](img/516210_1_En_1_Chapter_TeX_Equ12.png)(12)在这里，记号 ![`$$ \left| {000 \cdots 0} \right\rangle \equiv \left| {0} \right\rangle \otimes \left| {0} \right\rangle \otimes \left| {0} \right\rangle \otimes \cdots \otimes \left| {0} \right\rangle $$`](img/516210_1_En_1_Chapter_TeX_IEq62.png)。另一类多粒子纠缠态，在许多应用中找到，是 W

不一定只有离散变量之间存在纠缠。人们甚至可以创建粒子的*混合*态，这些粒子在它们的连续和离散自由度之间纠缠在一起。纠缠态，曾经只是理论上的兴趣点，现在被用作量子计算的资源[10]。另一类状态是*超*-纠缠态[11, 12]，其中两个粒子在多个离散自由度上纠缠在一起。

#### 1.2.3 互信息，霍勒沃界限和信息安全

让 *A* 和 *B* 是具有相应量子态 ![$$\rho _A$$](img/516210_1_En_1_Chapter_TeX_IEq63.png) 和 ![$$\rho _B$$](img/516210_1_En_1_Chapter_TeX_IEq64.png) 的两个系统。量子互信息量化了两个系统共有的信息量。此外，它也是两个系统状态之间相关性的度量。它由[1]给出![$$\begin{aligned} I(A:B) = S(A) + S(B) - S(A,B) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ14.png)(14)，其中 *S*(*A* : *B*) 是联合熵。现在假设 Alice 想通过概率为 ![$$p_i$$](img/516210_1_En_1_Chapter_TeX_IEq66.png) 的一般混合态 ![$$\rho _i$$](img/516210_1_En_1_Chapter_TeX_IEq65.png) 向 Bob 发送信息。当 Alice 通过 *嘈杂的* 量子信道发送纯态 ![$$ \left| {\psi } \right\rangle _i$$](img/516210_1_En_1_Chapter_TeX_IEq67.png) 时，这种情况可能会发生，由于这个纯态变为混合态。总消息由 ![$$\rho = \sum _i p_i \rho _i$$](img/516210_1_En_1_Chapter_TeX_IEq68.png) 给出。鉴于此，Bob 可以在他这一边解码多少信息？他可以提取的 *经典* 信息量由![$$\begin{aligned} I(A:B) \le S(\rho ) - \sum _i p_i S(\rho _i). \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ15.png)(15)右侧被称为 Holevo 信息或 ![$$\chi $$](img/516210_1_En_1_Chapter_TeX_IEq69.png) 量。可以编码在量子系统中的，因此可以从中提取的经典信息量上界由 ![$$\chi $$](img/516210_1_En_1_Chapter_TeX_IEq70.png) 量给出。

在量子密码学和通信中，如果合法各方之间的相互信息 *I*(*A* : *B*) 大于 Alice 和窃听者 Eve 之间的相互信息，即 ![$$I(A:B) &gt; I(A:E)$$](img/516210_1_En_1_Chapter_TeX_IEq71.png)，这将导致积极安全密钥速率： ![$$\kappa = I(A:B) - I(A:E) &gt; 0$$](img/516210_1_En_1_Chapter_TeX_IEq72.png)。然而，这种安全性通常仅适用于个体攻击，其中 Eve 在每一轮通信中攻击粒子。更一般地，Eve 可以采用一种策略，选择在最后攻击所有粒子，这被称为集体攻击。在这种情况下，安全密钥速率由 ![$$\kappa = I(A:B) - \chi (E)$$](img/516210_1_En_1_Chapter_TeX_IEq73.png) 给出，其中 ![$$\chi (E)$$](img/516210_1_En_1_Chapter_TeX_IEq74.png) 是 Eve 学到的霍利沃信息。

基于相互信息的量子密钥分发的信息安全定义不是“可组合的”。这是因为它仅在限于一个密码系统时有效。当使用多个密码系统时，需要一个可组合的定义。然而，对于许多一般目的，使用上述定义就足够了。

#### 1.2.4 无克隆定理

克隆定理指出，给定一个量子态 ![$$ \left| {\psi } \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq75.png)，不存在单位算符使得 ![$$U \left| {\phi } \right\rangle \rightarrow \left| {\phi } \right\rangle \left| {\phi } \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq76.png)。该定理的证明最终源自量子力学的线性性质。假设存在一个单位算符 *U*，它将态 ![$$ \left| {\phi } \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq77.png) 克隆为 ![$$U \left| {\psi } \right\rangle = \left| {\phi } \right\rangle \otimes \left| {\phi } \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq78.png)。若 ![$$ \left| {\phi _1} \right\rangle = \left| {0} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq79.png)，则 ![$$U \left| {0} \right\rangle = \left| {0} \right\rangle \left| {0} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq80.png)。然而，如果态是*未知*的，即任意叠加态 ![$$ \left| {\phi } \right\rangle =\alpha \left| {\phi _1} \right\rangle + \beta \left| {\phi _2} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq81.png)，那么由于线性性，复制机应输出 ![$$ U \left| {\phi } \right\rangle = |\alpha |² \left| {\phi _1\phi _1} \right\rangle + |\beta |² \left| {\phi _2\phi _2} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq82.png)，这与![$$\begin{aligned} \left| {\psi } \right\rangle \otimes \left| {\psi } \right\rangle&amp;=(\alpha \left| {\phi _1} \right\rangle + \beta \left| {\phi _2} \right\rangle ) \otimes (\alpha \left| {\phi _1} \right\rangle + \beta \left| {\phi _2} \right\rangle ) \nonumber \\&amp;= |\alpha |² \left| {\phi _1\phi _1} \right\rangle + |\beta |² \left| {\phi _2\phi _2} \right\rangle + \alpha ^* \beta \left| {\phi _1\phi _2} \right\rangle + \beta ^* \alpha \left| {\phi _2\phi _1} \right\rangle . \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ16.png)(16)不同。换句话说，克隆定理表明，*未知*量子态不能被完美复制。一旦被测量，它就会坍缩成一个经典态，然后显然可以被复制。克隆定理还指出，一对非正交态不能以完美的保真度进行复制，因为它们在测量中无法可靠地区分。设 ![$$\psi _1$$](img/516210_1_En_1_Chapter_TeX_IEq83.png) 和 ![$$\psi _2$$](img/516210_1_En_1_Chapter_TeX_IEq84.png) 为两个正交态。那么 ![$$U \left| {\psi _1} \right\rangle = \left| {\psi _1} \right\rangle \otimes \left| {\psi _1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq85.png) 和 ![$$U \left| {\psi _2} \right\rangle = \left| {\psi _2} \right\rangle \otimes \left| {\psi _2} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq86.png)。现在，在克隆前后两个态之间的重叠应该相等，即 ![$$\langle \psi _1 \vert \psi _2 \rangle = (\langle \psi _1 \vert \psi _2 \rangle )²$$](img/516210_1_En_1_Chapter_TeX_IEq87.png)，这仅在两个态都相同时或者两个都是正交时才可能。例如，当 ![$$ \left| {\psi _1} \right\rangle = \left| {+} \right\rangle = \frac{1}{\sqrt{2}}( \left| {0} \right\rangle + \left| {1} \right\rangle )$$](img/516210_1_En_1_Chapter_TeX_IEq88.png) 和 ![$$ \left| {\psi _2} \right\rangle = \left| {0} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq89.png) 时，这两个态不能以完美的保真度进行复制，因

量子密码学中，**无法克隆**对于其基本重要性有着重要且基本的含义 [13]。窃听者将无法在不产生可检测干扰的情况下复制量子状态，而这种干扰会被希望秘密通信的合法方检测到。在测量过程中产生的干扰越大，就越能够收集有关被干扰的量子系统的信息。这是加密安全的核心。窃听者通过她的测量获得的信息越多，她就会干扰系统越多，因此在过程中被捕获。但是，沟通双方需要确保这种情况的必要条件。例如，他们需要随机切换用于在系统中编码信息的基础，并且通过经典公共信道（假定为真实的）共享他们的基础信息，而不是测量结果。

#### 1.2.5 量子门和操作

在量子计算中，电路形式主义最常被采用。可以通过对量子比特执行量子门来实现任务。比较经典计算与量子计算的一个重要方面是通用门集的概念 [1]。在计算理论中，一组 AND 和 NOT 门就足以形成一个通用集。有趣的是，只需一个 Toffoli 门就足以实现通用性，Fredkin 门也是如此。一般来说，逻辑门是一个函数 ![$$f: \{0,1\}^i \rightarrow \{0,1\}^j$$](img/516210_1_En_1_Chapter_TeX_IEq90.png)，具有 *i* 个输入和 *j* 个输出。例如，一个异或门由 2 输入 1 输出映射给出： ![$$XOR: \{x,y\} \rightarrow x \oplus y$$](img/516210_1_En_1_Chapter_TeX_IEq91.png)，其中 ![$$\oplus $$](img/516210_1_En_1_Chapter_TeX_IEq92.png) 表示模 2 加法。

量子电路由门构成，这些门将输入状态转换为输出状态，并通过量子态携带量子信息的导线组成。导线在空间和时间中传输比特。一组最简单的量子门是量子比特门。事实上，所有单比特门和一个双比特门的集合就足以形成一个通用集合。这意味着任何量子比特门以及量子比特电路都可以通过这些门的组合来实现。假设一个量子比特门有*k*个输入和输出，那么表示门的矩阵将是![$$2^k$$](img/516210_1_En_1_Chapter_TeX_IEq93.png)度的。一个双比特门将是![$$2^k = 4$$](img/516210_1_En_1_Chapter_TeX_IEq94.png)，即一个![$$4 \times 4$$](img/516210_1_En_1_Chapter_TeX_IEq95.png)矩阵。

单量子比特门 量子信息中的一个重要转换组是由算符构成的 Pauli 群！$$\begin{aligned} \sigma _1 = X = \begin{pmatrix} 0 &amp;{} 1 \\ 1 &amp;{} 0 \end{pmatrix},\sigma _2 = Y = \begin{pmatrix} 0 &amp;{} -i \\ i &amp;{} 0 \end{pmatrix},\sigma _3 = Z = \begin{pmatrix} 1 &amp;{} 0 \\ 0 &amp;{} -1 \end{pmatrix} \; \text {and} \;\sigma _0 = \mathbbm {1} = \begin{pmatrix} 1 &amp;{} 0 \\ 0 &amp;{} 1 \end{pmatrix}, \end{aligned}$$(17)，它们产生了两能级系统的动力学，这可以在 Bloch 球面上实现。Pauli 算符是 2D 希尔伯特空间中旋转的生成器。例如，关于任意方向![$$\hat{n}$$](img/516210_1_En_1_Chapter_TeX_IEq96.png)的旋转，酉矩阵由![$$R_{\hat{n}}(\theta ) = \exp \big (-i \theta \frac{\hbar }{2} (\mathbf {\sigma } \cdot \hat{n}) \big )$$](img/516210_1_En_1_Chapter_TeX_IEq97.png)给出，其中![$$\mathbf {\sigma } = a_1 \sigma _1 + a_2 \sigma _2 + a_3 \sigma _3$$](img/516210_1_En_1_Chapter_TeX_IEq98.png)是 Pauli 算符向量。*X*和*Y*的等叠加给出了一个重要的转换，称为 Hadamard 门！$$\begin{aligned} H = \frac{1}{\sqrt{2}}(X+Z) = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 &amp;{} 1 \\ 1 &amp;{} -1 \end{pmatrix}. \end{aligned}$$(18)在量子动力学中，复杂相位起着核心作用。介绍相位门是相关的！$$\begin{aligned} P = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 &amp;{} 0 \\ 0 &amp;{} e^{i \theta } \end{pmatrix}, \end{aligned}$$(19)，其中![$$\theta \in \{0, 2\pi \}$$](img/516210_1_En_1_Chapter_TeX_IEq99.png)的值决定了量子比特的特定操作。例如，一个著名的门是所谓的![$$\frac{\pi }{8}$$](img/516210_1_En_1_Chapter_TeX_IEq100.png)门：![$$T = \begin{pmatrix} 1 &amp;{} 0 \\ 0 &amp;{} e^{\frac{i \pi }{4}} \end{pmatrix} = e^{\frac{i \pi }{8}} \begin{pmatrix} e^{-\frac{i \pi }{8}} &amp;{} 0 \\ 0 &amp;{} e^{\frac{i \pi }{8}} \end{pmatrix}.$$](img/516210_1_En_1_Chapter_TeX_IEq110.png)

#### 1.2.6 量子操作

量子系统是脆弱的，因为它们不可避免地受到无处不在的环境相互作用的影响。在现实中，不存在完全封闭的量子系统，系统始终是*开放的*[14]。当量子系统与环境相互作用时，它失去了相干性，因此经历了*退相干*。也就是说，当一个系统完全退相干时，密度矩阵中的非对角项（也称为相干项）消失。此外，它还可能失去能量，经历*耗散*。开放系统量子力学现在遵循不同的公理：（1）状态是密度矩阵，（2）测量是 POVMs，（3）动力学由完全正（CP）的保持迹（TP）映射固定。密度矩阵同时捕捉纯态和混合态表示，POVMs 是 PVMs 的凸组合，动力学不再是酉的，而是线性的和 CP 的，因此代表着一个物理上有效的演变。也就是说，非 CP 演变在对应的动力学映射输出负态方面是不物理的。

量子技术面临的挑战是减少由噪声引起的误差，量子纠错码的目标和目的是促进容错量子计算机的运行，该计算机对环境危害和设备故障引起的错误具有鲁棒性。研究退相干是量子信息的一个重要方面，因为任何量子计算机必须满足所谓的 DiVincenzo 标准之一：*长退相干时间*。

假设一个量子比特正在与环境相互作用。 它的演化由著名的 Gorini-Kossakowski-Lindblad-Sudarshan（GKSL）方程[15, 16]统治着，这是在所谓的玻恩-马尔可夫近似下获得的。 在量子信息科学中有用的等效表示是 CPTP 映射（量子通道）的算子和求和（KSMR）表示[17, 18]: 

#### 1.2.7 崔-雅米奥尔科夫同构

量子信息理论的中心工具之一是 Choi-Jamiolkowski（CJ）同构[19]。它主要用于利用通道-态对偶性。也就是说，任何 CPTP 映射（通道）都可以用于转换与该映射同构的状态。而 CJ 矩阵[19]或 B 矩阵^(4)[18]是由下式给出的：

### 1.3 量子信息科学—应用

在这里，我们将讨论量子信息科学的一些主要应用，即传输、超密编码和纠缠交换，这在经典情况下是不可能的。这意味着在经典世界中不存在资源，可以用来复制应用于传输和操纵信息的相当反直觉的效果，而这些效果是使用量子系统实现的。在本小节中，我们的主要动机是解释量子纠缠在量子通信和量子技术中的作用。我们还将提及量子力学与狭义相对论的和平共存，即在执行量子信息处理任务时不涉及超光速通信。

#### 1.3.1 超密编码

如何利用量子粒子发送信息？量子粒子具有可编码信息的自由度。事实上，特定的自由度，比如光子的极化，可以用作量子比特。这就是我们在实验室中操纵的量子系统。现在，信息的比特可以被编码在光子的极化中并通过量子通道发送。Alice 能用一粒单独的粒子向 Bob 发送多少比特？对于一粒孤立的不相关光子，她可以发送一比特的经典信息。假设 Alice 和 Bob 共享一对最大纠缠的粒子，那么 Alice 可以在一粒量子比特上发送两比特的信息。这就是超密编码。假设有一个初始的贝尔态！$$\begin{aligned} \left| {\phi } \right\rangle _{00} = \frac{1}{\sqrt{2}}( \left| {00} \right\rangle + \left| {11} \right\rangle ), \end{aligned}$$(26)如果 Alice 想发送比特 00，她对粒子不做任何操作并将其发送给 Bob。如果 Alice 在本地应用一个![$$\sigma _x$$](img/516210_1_En_1_Chapter_TeX_IEq125.png)门，那么态会转变为![$$\begin{aligned} (\sigma _x \otimes \mathbbm {1}) \left| {\phi } \right\rangle _{00} = \frac{1}{\sqrt{2}}( \left| {10} \right\rangle + \left| {01} \right\rangle ) = \left| {\phi } \right\rangle _{01}. \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ27.png)(27)同样，如果她本地应用![$$i\sigma _y$$](img/516210_1_En_1_Chapter_TeX_IEq126.png)和![$$\sigma _z$$](img/516210_1_En_1_Chapter_TeX_IEq127.png)门，她会分别转变态为![$$\begin{aligned} (i\sigma _y \otimes \mathbbm {1}) \left| {\phi } \right\rangle _{00}= \frac{1}{\sqrt{2}}( \left| {01} \right\rangle - \left| {10} \right\rangle ) = \left| {\phi } \right\rangle _{11}, \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ28.png)(28)![$$\begin{aligned} (\sigma _z \otimes \mathbbm {1}) \left| {\phi } \right\rangle _{00}= \frac{1}{\sqrt{2}}( \left| {00} \right\rangle - \left| {11} \right\rangle ) = \left| {\phi } \right\rangle _{10}. \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ29.png)(29)当 Bob 接收到量子比特时，他进行贝尔测量以找出 Alice 想发送给他的比特![$$\{ \left| {\phi } \right\rangle _{00}, \left| {\phi } \right\rangle _{01}, \left| {\phi } \right\rangle _{10}, \left| {\phi } \right\rangle _{11}\}$$](img/516210_1_En_1_Chapter_TeX_IEq128.png)，对应于比特![$$\{00, 01,10,11\}$$](img/516210_1_En_1_Chapter_TeX_IEq129.png)。

#### 1.3.2 量子传送

量子传送是量子力学的一项引人注目的特性，它允许使用纠缠来通信一个未知的量子比特。该协议的步骤如下。假设 Alice 想要发送一个未知的量子态 ![$$ \left| {\psi } \right\rangle = \alpha \left| {0} \right\rangle + \beta \left| {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq130.png) 到 Bob，他与她空间分隔，即，光或信息需要有限的时间到达。Alice 和 Bob 预先共享了一对纠缠的量子比特，即 EPR-Bell 态，假设为 ![$$ \left| {\phi } \right\rangle _{00} = \frac{1}{\sqrt{2}}( \left| {00} \right\rangle + \left| {11} \right\rangle )$$](img/516210_1_En_1_Chapter_TeX_IEq131.png)。现在所有比特的初始总态为：![$$\begin{aligned} \left| {\Psi } \right\rangle _\mathrm{\small initial}&amp;= \left| {\psi } \right\rangle \otimes \left| {\phi } \right\rangle _{00} \nonumber \\&amp;= (\alpha \left| {0} \right\rangle + \beta \left| {1} \right\rangle )\frac{1}{\sqrt{2}}( \left| {00} \right\rangle + \left| {11} \right\rangle ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ30.png)(30)Alice 将她的 EPR-Bell 对的一部分与要传送的未知态 ![$$ \left| {\psi } \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq132.png) 纠缠起来，即，她在她的对上执行一个 CNOT 门 ![$$C_N = \left| {0} \right\rangle \left\langle {0} \right| \otimes \mathbbm {1}_2 + \left| {1} \right\rangle \left\langle {1} \right| \otimes \sigma _x$$](img/516210_1_En_1_Chapter_TeX_IEq133.png)。随后，她在*第一个*量子比特上执行一个 Hadamard 门 ![$$ H = \frac{1}{\sqrt{2}} \bigg ( \begin{array}{cc} 1 &{} 1 \\ 1 &{} -1 \end{array}\bigg )$$](img/516210_1_En_1_Chapter_TeX_IEq134.png)。这里， ![$$\mathbbm {1}_2$$](img/516210_1_En_1_Chapter_TeX_IEq135.png) 和 ![$$\sigma _x$$](img/516210_1_En_1_Chapter_TeX_IEq136.png) 是量子比特的恒等和 Pauli-X 操作符。所有这些之后，简单的代数给出了结果的总态：![$$\begin{aligned} \left| {\tilde{\Psi }} \right\rangle&= \frac{\alpha }{2}( \left| {0} \right\rangle + \left| {1} \right\rangle )( \left| {00} \right\rangle + \left| {11} \right\rangle ) + \frac{\beta }{2} ( \left| {0} \right\rangle - \left| {1} \right\rangle )( \left| {10} \right\rangle + \left| {01} \right\rangle ) \nonumber \\&= \frac{1}{2}[ \left| {00} \right\rangle (\alpha \left| {0} \right\rangle +\beta \left| {1} \right\rangle ) + \left| {01} \right\rangle (\alpha \left| {1} \right\rangle +\beta \left| {0} \right\rangle ) + \left| {10} \right\rangle (\alpha \left| {0} \right\rangle -\beta \left| {1} \right\rangle ) + \left| {11} \right\rangle (\alpha \left| {1} \right\rangle -\beta \left| {0} \right\rangle )]. \end{aligned}$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_Equ31.png)(31)像之前一样，Alice 拥有态 ![$$ \left| {\tilde{\Psi }} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq137.png) 的前两个量子比特，Bob 拥有第三个。现在量子传送的神奇部分来了。Alice 现在以计算基础 ![$$\{ \left| {0} \right\rangle , \left| {1} \right\rangle \}$$](img/516210_1_En_1_Chapter_TeX_IEq138.png) 测量她的量子比特对，^(5) 这将 *瞬间* 将未知态 ![$$ \left| {\psi } \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq139.png) 传送给 Bob！如果 Bob 现在对他的量子比特进行测量，那么他有 ![$$\frac{1}{4}^\mathrm{\small th}$$](img/516210_1_En_1_Chapter_TeX_IEq140.png)

有趣的是，无克隆定理和信息不可超越光速的传输是相关的。如果 Bob 能够制作大量他的粒子的副本，那么他可以对每个粒子进行测量，返回相同结果的基是 Alice 将会编码的基。但是，再次强调，对未知状态的复制是被无克隆定理禁止的！因此，Bob 永远无法在没有 Alice 的经典信息的情况下恢复他的状态。

量子隐形传态在量子技术中具有巨大的应用。其中一个直接的应用是在量子互联网中——一个用于在节点之间交换量子状态的量子网络，其中节点之间存在分布式纠缠。另一个应用是基于隐形传态的量子计算。事实上，隐形传态已经实现了非常长的距离，约 143 公里长[20]，并且还使用了基于卫星的量子纠缠粒子实现了 1400 公里的距离[21]。这种实用的长距离隐形传态将是全球量子互联网的关键。

#### 1.3.3 纠缠交换

还有另一种没有经典模拟的过程是纠缠交换，它在基于量子网络的通信中找到了用武之地。在这里，我们简要解释一下它的原理。

一般来说，要使两个量子粒子纠缠在一起，它们必须在过去的某个时刻通过某种物理过程发生过相互作用。量子纠缠交换是一种利用量子测量和纠缠本身来纠缠从未相互作用过的两个粒子的技术！假设，![$$\{a,b\}$$](img/516210_1_En_1_Chapter_TeX_IEq148.png) 和 ![$$\{c,d\}$$](img/516210_1_En_1_Chapter_TeX_IEq149.png) 分别是具有 Alice 和 Bob 的粒子对。 *a* 与 *b* 纠缠在一起；*c* 与 *d* 纠缠在一起。现在，*a* 和 *c* 在过去从未相互作用过。问题是：![$$\{a,c\}$$](img/516210_1_En_1_Chapter_TeX_IEq150.png) 能够纠缠吗？答案是肯定的，这是量子力学允许的一种神秘现象之一！其过程如下。

假设爱丽丝有一个纠缠对 ![$$ \left| {\phi } \right\rangle _{ab} = \frac{1}{\sqrt{2}}( \left| {00} \right\rangle _{ab}+ \left| {11} \right\rangle _{ab})$$](img/516210_1_En_1_Chapter_TeX_IEq151.png)。同样，鲍勃有一个 ![$$ \left| {\phi } \right\rangle _{cd} = \frac{1}{\sqrt{2}}( \left| {00} \right\rangle _{cd}+ \left| {11} \right\rangle _{cd})$$](img/516210_1_En_1_Chapter_TeX_IEq152.png)。所以初始状态为:![$$\begin{aligned} \left| {\psi } \right\rangle _\mathrm{\small initial} = \left| {\phi } \right\rangle _{ab} \otimes \left| {\phi } \right\rangle _{cd}. \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ32.png)(32)现在，这个初始状态被发送到第三方查理，他对 ![$$\{b,d\}$$](img/516210_1_En_1_Chapter_TeX_IEq153.png) 进行贝尔态测量，正如之前解释的那样，结果是 ![$$\{a,c\}$$](img/516210_1_En_1_Chapter_TeX_IEq154.png) 纠缠！ 这展示了量子物理中测量和纠缠的一些神奇特性。请注意，纠缠交换已经在实验中实现[22, 23]。

#### 1.3.4 量子密码学与通信

自从 1984 年 Bennett 和 Brassard 提出了著名的 BB84 量子密钥分发协议以来，已经有超过 30 年的时间致力于开发更安全的通信协议。在理论和实验前沿已经取得了显著的进展。但在建立一个*可扩展*的量子安全通信系统和量子计算机的挑战上还有很多要做的工作，这将超越现有的经典信息处理系统。尽管如此，也有人在努力开发提供后量子密码安全性的经典加密算法，意味着它们将提供对抗来自量子计算机攻击的安全性。

纠缠的一个引人注目的应用是在安全的*直接*量子通信协议中。在这里，有必要简要解释一个这样的协议，2002 年由 Bostrom 和 Felbinger[24]首次提出：

+   Bob 有一对偏振度纠缠的光子，比如说，![$$ \left| {\phi ^+_{ht}} \right\rangle = \frac{1}{\sqrt{2}} ( \left| {01} \right\rangle + \left| {10} \right\rangle )$$](img/516210_1_En_1_Chapter_TeX_IEq155.png)，其中一只由他保留（家中光子处于状态 ![$$\rho _h$$](img/516210_1_En_1_Chapter_TeX_IEq156.png)），另一只（旅行光子处于状态 ![$$\rho _t$$](img/516210_1_En_1_Chapter_TeX_IEq157.png)）他发送给了远离他的爱丽丝。

+   一旦爱丽丝接收到量子比特，她以概率![$$\frac{1}{2}$$](img/516210_1_En_1_Chapter_TeX_IEq158.png)对其进行恒等或 Pauli-Z 操作，然后将其发送回给 Bob。

+   在收到旅行量子位后，Bob 对它们进行贝尔态测量，并发现他的粒子对处于 ![$$ \left| {\phi ^+} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq159.png) 或 ![$$ \left| {\phi ^-} \right\rangle = (\mathbbm {1} \otimes \sigma _z)[ \left| {\phi ^+} \right\rangle ]$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq160.png) 中的一个，取决于 Alice 是否想发送给他 0 或 1。

+   如果 Bob 发现这对粒子是反相关的，那么他们会中止协议。如果他发现自己的粒子处于 Bell 状态 ![$$ \left| {\phi ^\pm } \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq161.png) 中的任何一个，那么协议将会重复。

现在，如果窃听者试图测量飞行量子位，她会发现的只是完全随机的结果，因为*极大*纠缠态 ![$$\rho ^{AB}$$](img/516210_1_En_1_Chapter_TeX_IEq163.png) 的约化密度矩阵 ![$$\rho _t = \text {Tr}_h( \left| {\phi ^+_{ht}} \right\rangle \left\langle {\phi ^+_{ht}} \right| )$$](img/516210_1_En_1_Chapter_TeX_IEq162.png) 是最大混合，即，![$$\rho _t=\frac{I}{2}$$](img/516210_1_En_1_Chapter_TeX_IEq164.png)。请注意，Alice 和 Bob 从未使用经典通道传输基础信息，而且传输的信息是直接且确定的。在这里，我们立即看到使用纠缠来确保量子密钥分发的安全性以及直接的量子通信的优势。然而，Wojcik [25] 对这个协议提出了一个巧妙的攻击，通过这个攻击，窃听者可以获得与 Alice 和 Bob 最终拥有的信息量相同。因此，安全检查被扩展到分析由窃听引起的信道损失。读者可参考 Refs. [25, 26] 进一步学习。

该协议的缺点是，当用于直接通信时，它几乎是安全的，但当用于密钥分发时，它具有完全安全的优势。此外，所有双向协议都因额外发送粒子通过量子通道所需的资源而遭受损失。一些单向量子密钥分发协议，无论是否反事实，都将在后面的章节中介绍。令人惊讶的是，在反事实密钥分发协议中，Alice 和 Bob 可以选择生成一个密钥，其粒子实际上并不通过量子通道传输（在这种情况下是干涉臂）的概率为特定概率！这个对于安全的量子密钥分发协议的有趣特性将在后面的章节中讨论。

#### 1.3.5 量子秘密分享

将秘密分享给不信任的个体的想法是一个非常相关的问题。简要介绍如下见参考文献[[27]及其中引用的参考文献]下方 见图[2]：

1.  1.

    个体（Alice）必须在两个或更多不信任的方（Bob，Charlie，Dave，...）之间分享秘密，以便没有单一方能解码它，但至少一半方必须联合才能这样做。

1.  2.

    例如，密钥![等于$K \equiv 11010 \Longleftrightarrow b (= 10001) + c (= 01001)$](img/516210_1_En_1_Chapter_TeX_IEq165.png) 分享给 Bob 和 Charlie。因此*b*和*c*是密钥的分享。仅知道其中一个，无法获得*K*的任何信息。

1.  3.秘密*S*需要分割给*n*个参与方，使得：

    1.  1.

        # ![当且仅当有$\ge k$](img/516210_1_En_1_Chapter_TeX_IEq166.png) 个参与方才足够重建*S*。

    1.  2.

        # ![当有$k-1$](img/516210_1_En_1_Chapter_TeX_IEq167.png) 个参与方获取零信息。

1.  3.

    对于一次多项式（在一个素数域上的），至少需要*k*个点。每个分享是三元组（*x*， *f*(*x*)， *P*）。

1.  4.

    示例：二次多项式 ![$$f(x) = a_0 + a_1x + a_2x²$$](img/516210_1_En_1_Chapter_TeX_IEq169.png)，其中 ![$$a_0$$](img/516210_1_En_1_Chapter_TeX_IEq170.png) 是秘密（一个质数）。我们为 *n* 个方分享 (*x*, *f*(*x*))，然后至少需要三方一起才能得到 ![$$a_0$$](img/516210_1_En_1_Chapter_TeX_IEq171.png)。

![](img/516210_1_En_1_Fig2_HTML.png)

图 2

一个秘密共享协议的示意图，针对与三个不受信任的方进行密钥共享的情况

量子秘密共享方案提供了基于量子力学的不可能定理的安全性，与经典对应物中的问题的计算难度不同。下面给出了一个简单的协议。

1.  1.

    四方 ![$$\{A,B,C,D,E\}$$](img/516210_1_En_1_Chapter_TeX_IEq172.png)：可以重建秘密的集合的集合： ![$$\mathcal {G} = \{\{A,B,C\} , \{C,D\}, \{A,B,E\}\}$$](img/516210_1_En_1_Chapter_TeX_IEq173.png)。这里 ![$$\mathcal {G}$$](img/516210_1_En_1_Chapter_TeX_IEq174.png) 是访问结构[27]。

1.  2.

    量子情况：无克隆定理 ![$$\Rightarrow $$](img/516210_1_En_1_Chapter_TeX_IEq175.png) ![$$\mathcal {G}$$](img/516210_1_En_1_Chapter_TeX_IEq176.png) 中没有两个不相交的元素。

1.  3.

    经典密钥 + 量子密钥分发解决了窃听问题；因此，量子秘密共享最适合于**量子**密钥。

假设一个 GHZ 三重态被三个方的当事人，爱丽丝，鲍勃和查理共享，其状态为[28]![$$\begin{aligned} \left| {\psi } \right\rangle = \frac{1}{\sqrt{2}} ( \left| {000} \right\rangle + \left| {111} \right\rangle ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ33.png)(33)。爱丽丝和鲍勃随机选择在 X 或 Y 方向测量他们的粒子，这可以给出![$$\pm 1$$](img/516210_1_En_1_Chapter_TeX_IEq177.png)的特征值，用![$$\pm \mathrm{X}$$](img/516210_1_En_1_Chapter_TeX_IEq178.png)或![$$\pm \mathrm{Y}$$](img/516210_1_En_1_Chapter_TeX_IEq179.png)表示。将 GHZ 状态写成 XY 基，我们构造了表格 1 [29]。表 1

代表测量粒子所在的泡利基的表格

|   | + X | – X | + Y | – Y |
| --- | --- | --- | --- | --- |
| + X | ![$$ \left&#124; {0} \right\rangle + \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq180.png) | ![$$ \left&#124; {0} \right\rangle - \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq181.png) | ![$$ \left&#124; {0} \right\rangle - i \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq182.png) | ![$$ \left&#124; {0} \right\rangle + i \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq183.png) |
| – Y | ![$$ \left&#124; {0} \right\rangle - \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq184.png) | ![$$ \left&#124; {0} \right\rangle + \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq185.png) | ![$$ \left&#124; {0} \right\rangle + i \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq186.png) | ![$$ \left&#124; {0} \right\rangle - i \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq187.png) |
| + Y | ![$$ \left&#124; {0} \right\rangle - i \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq188.png) | ![$$ \left&#124; {0} \right\rangle + i \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq189.png) | ![$$ \left&#124; {0} \right\rangle - \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq190.png) | ![$$ \left&#124; {0} \right\rangle + \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq191.png) |
| – Y | ![$$ \left&#124; {0} \right\rangle + i \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq192.png) | ![$$ \left&#124; {0} \right\rangle - i \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq193.png) | ![$$ \left&#124; {0} \right\rangle + \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq194.png) | ![$$ \left&#124; {0} \right\rangle - \left&#124; {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq195.png) |

#### -   1.3.6 开放量子系统动力学

量子操作提供了一种清晰的方法来表示和研究开放量子系统动态——马尔可夫和非马尔可夫[30, 31]。在现实情况下，大多数开放系统动态都是非马尔可夫（NM），因为波恩-马尔可夫近似可能不成立。最近，人们已经付出了巨大的努力来从信息论的角度研究非马尔可夫动态。例如，Breuer-Laine-Piilo（BLP）提出了第一个简单的检测和量化非马尔可夫性（NM-ity）的方法[32]，该方法利用了迹距离（TD）(5)在马尔可夫 CPTP 映射下的单调性！$$\Phi (t)$$： ![$$D(\Phi (t)[\rho _1],\Phi (t)[\rho _2]) \le D(\rho _1, \rho _2)$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq197.png)，其中*D*是 TD，![$$\rho _1$$](img/516210_1_En_1_Chapter_TeX_IEq198.png)和![$$\rho _2$$](img/516210_1_En_1_Chapter_TeX_IEq199.png)是两个正交的初始状态。这意味着随着初始正交状态在时间演化过程中变得越来越难以区分，这被解释为对环境的量子信息损失。关键观察是，在非马尔可夫通道下，这种单调性将被打破，即丢失给环境的信息会回流到系统。因此，非单调区域可以用来量化非马尔可夫性。BLP 度量由![$$N_\mathrm{\small BLP} = \int _{\sigma &gt; 0} \sigma (\Phi , \rho _1,\rho _2)$$](img/516210_1_En_1_Chapter_TeX_IEq200.png)给出，其中![$$\sigma = \frac{dD}{dt}$$](img/516210_1_En_1_Chapter_TeX_IEq201.png)。另一种检测和量化非马尔可夫性的方法是 Rivas-Huelga-Plenio（RHP）提出的，该方法基于通道的可分性。给定一个 CPTP 映射![$$\Phi $$](img/516210_1_En_1_Chapter_TeX_IEq202.png)，它可以分解为简单的 3 个实例的中间映射的连接：![$$\Phi (t_2,t_0) = \Phi (t_2,t_1)\Phi (t_1,t_0)$$](img/516210_1_En_1_Chapter_TeX_IEq203.png)。如果中间映射![$$\Phi (t_2,t_1)$$](img/516210_1_En_1_Chapter_TeX_IEq204.png)的 CJ 矩阵(25)为负（即如果中间映射不是通道），那么 CPTP 映射![$$\Phi (t_2,t_0)$$](img/516210_1_En_1_Chapter_TeX_IEq205.png)是 CP-不可分的，并且根据 RHP 被称为 NM。NM-ity 可以量化为![$$N_\mathrm{\small RHP} = \int _{0}^{\infty } g(t)$$](img/516210_1_En_1_Chapter_TeX_IEq206.png)，其中![$$g(t) = \lim _{\epsilon \rightarrow 0^+} \frac{\Vert \xi (\Phi , \epsilon ) \Vert _1 - 1}{\epsilon }$$](img/516210_1_En_1_Chapter_TeX_IEq207.png)，其中![$$\epsilon $$](img/516210_1_En_1_Chapter_TeX_IEq208.png)是无穷小时间，![$$\xi (\Phi , \epsilon )$$](img/516210_1_En_1_Chapter_TeX_IEq209.png)表示在无穷小时间极限下的映射的 CJ 矩阵。注意，BLP 和 RHP 度量都不需要归一化，可以使用适当的归一化将它们拟合到 0 到 1 的范围内。

除了上述两种方法之外，还有许多方法来量化 NM-ity——基于保真度[34]、信道容量[35]、因果性测量[36]、干涉功率、可访问信息等等。然而，它们之间存在着不等价关系。当一个过程涉及多个退相干通道时，那么 BLP 和 RHP 未必等价。但对于涉及单个退相干通道的量子比特动力学，它们被认为是等价的。NM-ity 可能通过马尔可夫通道的凸组合方式产生另一种有趣且引人入胜的方式。在单位通道的情况下^(6)，已知 Pauli 马尔可夫（CP 可分）通道空间不是凸的[37–39]。如果将两个 Pauli 半群进行凸组合，则得到的通道在某种意义上是非马尔可夫的，因为它是 CP 不可分的。此外，根据 RHP 测量的意义，它可以永远地是非马尔可夫的，因为它从时间 ![$$t=0$$](img/516210_1_En_1_Chapter_TeX_IEq212.png) 开始就是 CP 不可分的，并且永远保持不变。然而，根据 BLP 测量，这样的通道仍然是马尔可夫的[40]。这是一个显著的例子，证明了非马尔可夫性的证据和测量是不等价的。

量子 NM-性在某些特殊情况下被声称在量子信息处理任务中发挥了有用的作用。例如，在阻尼 Jaynes-Cummings 模型中由于失谐而增加 NM-性可以改善量子信道容量 [35]。类似地，热机的效率被认为会增加，NM-性还有助于提高量子电池效率 [41]。接下来我们将提及如何故意添加的 NM 噪声可以提供针对基于纠缠的 QKD 协议攻击的安全性。所有这些优势可能归因于量子噪声的某些特殊性质和由于非马尔可夫性质开放系统演化导致的信息回流 [42]。

#### 1.3.7 量子噪声的反直觉性质

量子噪音对量子信息处理任务有害是被普遍接受的观点。但这并不总是正确的。信息处理任务受到环境噪声的影响，因此假定各方之间的通信是通过嘈杂的量子通信渠道进行的。正如之前所指出的，窃听者可以被认为是在 Alice 和 Bob 运行密钥交换协议后收集的最终数据中的噪声。有趣的是，*故意*向测量数据中添加一些*经典*噪声实际上可以提高安全密钥速率[43]。后续的研究表明，通过 Bob 在最终测量之前故意添加*量子*噪声，可以增加合法各方对窃听者的优势[44, 45]。这是指 Alice 和 Bob 之间的互信息与 Eve 收集到的信息相比更多。这种通过故意添加量子噪声产生的优势可能特定于协议和窃听攻击策略[42]。在这里，我们看到量子噪声在量子密码学中起着违反直觉的作用。人们可能将这种噪声称为“受信任的”。在连续变量 QKD 的情况下也提出了类似的结果[46]。然而，受信任噪声的定义方式与离散变量 QKD 中的定义方式有所不同。

另一个量子噪声发挥作用的有趣领域是光合复合物中的量子传输 [47]。这些复合物可以被视为传输激子的量子网络。有论据和实验证据表明，在绿硫细菌中存在长寿命的相干性 [48]。因此，自然而然地问，自然是否正在利用量子效应，如长寿命的相干性，来实现激子能量的高效传输 [49, 50]。事实证明，量子噪声，如退相干，可能有助于实现高达 99%的高效传输! [51]。自然利用噪声而不是量子本性，如相干性，来实现高效能量传输，这相当反直觉。然而，这种高效的量子传输的整个原因仍然是一个活跃的研究领域，引发了量子物理学家和化学家之间的激烈争论 [49, 50]。

### 1.4 量子区块链

区块链是一个去中心化的账本，没有中央机构监督账本中发生的所有交易和信息交换。在这样一个交换系统中存在信任缺乏，但这些问题通过哈希、时间戳和共识算法来解决。这些是使区块链可靠的一些方面。然而，量子计算机可能对区块链技术构成威胁，因为其安全性取决于基于单向哈希的加密。典型例子包括以太币、比特币、瑞波币等加密货币。因此，开发量子模拟区块链是有必要的。

量子区块链技术是一个活跃的研究领域，对于更快、更新的方法是开放的。建立在量子属性上的区块链的需求源于量子技术的最新发展，如量子计算和少数算法。简言之，量子区块链利用贝尔态和 GHZ 态的时间纠缠属性来形成量子区块链的链和网络。也就是说，时间 GHZ 态的单个单位充当时间戳，其信息安全性提供了经典区块链中单向哈希提供的安全性的类似物。

这里的技术细节已经简化了很多，但在区块链和量子区块链方面，远不止眼前所见，这将在结论中予以指出，并在后续章节中详细讨论。

## 2 多控制托菲利

量子计算范式最初是由本尼奥夫（Benioff）在上世纪 80 年代提出的，其提出了量子图灵机[52]。在过去的 40 年中，量子算法取得了许多重大突破，有助于巩固量子计算模型。一些最值得注意的创新包括肖尔的因子分解算法、格罗弗的搜索算法，以及最近的变分量子本征求解器。这些算法利用了量子系统的独特性质，如叠加、干涉和纠缠，为经典问题提供了非平凡的加速。

“黑匣子”预言机是量子算法共享的一个相似之处。这种类型的预言机编码了与所关注系统有关的信息，并在量子电路中的不同量子位之间使用控制操作。

多控制 Toffoli 门是量子计算科学家感兴趣的一种受控操作。当作用于两个量子比特时，它是经典 XOR 门的可逆模拟。而在三个量子比特上，它是 AND 门的量子模拟。本章总结了多控制 Toffoli 门的不同构造。我们还将介绍其中一种构造的一个小而新颖的改进。最后，我们将提供一份最有效的实现的简短列表，以最小化 CNOT 计数。

### 2.1 背景

本节简要回顾了一些电路身份，这些身份将有助于理解后面的构造。

#### 2.1.1 旋转门

三个单量子比特旋转门 ![$$R_x, R_y, R_z$$](img/516210_1_En_1_Chapter_TeX_IEq213.png) 将状态向量分别绕*x*、*y* 和 *z* 轴旋转 $\theta$ 弧度。当 $\theta = \pi$ 时，这些旋转门采用称为 Pauli 矩阵的特殊形式，表示为 *X*、*Y*、*Z*。

![$$R_z$$](img/516210_1_En_1_Chapter_TeX_IEq216.png) 门具有一种称为相位门的特殊形式，用*P*表示，它与![$$R_z$$](img/516210_1_En_1_Chapter_TeX_IEq217.png) 不同，差别在于全局相位。这两个门之间的关系由![$$\begin{aligned} P(\theta ) = e^{i\frac{\theta }{2}} R_z(\theta ) = \begin{pmatrix} 1 &amp;{} 0 \\ 0 &amp;{} e^{i\theta }\end{pmatrix} \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ34.png)(34) 给出。

#### 2.1.2 Hadamard 身份

Hadamard 门将 *z* 基础上的旋转转换为 *x* 基础上的旋转，反之亦然。![$$\begin{aligned} HR_z(\theta )H&amp;= R_x(\theta ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ35.png)(35)![$$\begin{aligned} HR_x(\theta )H&amp;= R_z(\theta ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ36.png)(36)当 ![$$\theta = \pi $$](img/516210_1_En_1_Chapter_TeX_IEq218.png) 时，我们有特殊情况![$$\begin{aligned} HZH = X \quad \text {和} \quad HXH = Z \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ37.png)(37)

#### 2.1.3 受控门

最简单的控制门是 CNOT 门，也被称为费曼门。该门作用于控制比特**![$$ \left| {q_0} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq219.png)**和目标比特**![$$ \left| {q_1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq220.png)**。当两个输入都处于*z*基态时，CNOT 门会对目标比特进行位翻转，如果控制比特为**![$$ \left| {1} \right\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq221.png)**。换句话说，![$$\begin{aligned} \mathrm {CNOT} \left| {q_0 q_1} \right\rangle = {\left\{ \begin{array}{ll} \left| {q_0 q_1} \right\rangle \text {如果} q_0 = 0 \\ \left| {q_0 \overline{q_1} } \right\rangle \text {如果} q_0 = 1\end{array}\right. } \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ38.png)(38)我们用一个点表示电路上的 CNOT 门的控制比特。我们画一条线连接它与目标比特上的 XOR 圆圈，如图 3 所示。上面显示的 CNOT 门具有单位矩阵![$$\begin{aligned} \text {CNOT} = \begin{pmatrix} 1&amp;{}0&amp;{}0&amp;{}0 \\ 0&amp;{}1&amp;{}0&amp;{}0 \\ 0&amp;{}0&amp;{}0&amp;{}1 \\ 0&amp;{}0&amp;{}1&amp;{}0 \end{pmatrix} = \begin{pmatrix} \begin{array}{c | c} I &amp;{} 0 \\ \hline 0 &amp;{} X \end{array} \end{pmatrix}\end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ39.png)(39)![](img/516210_1_En_1_Fig3_HTML.png)

图 3

CNOT 门的作用

现在我们将这个结果推广到任意两比特受控幺正操作。当控制位是 ![$$|1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq222.png) 时，作用到目标比特的算子是一个一比特幺正 ![$$U= \begin{pmatrix} a&amp;{}b \\ c&amp;{}d \end{pmatrix}$$](img/516210_1_En_1_Chapter_TeX_IEq223.png)。![$$\begin{aligned} CU \left| {q_0 q_1} \right\rangle = {\left\{ \begin{array}{ll} \left| {q_0} \right\rangle \left| {q_1} \right\rangle &amp;{}\text { if } q_0 = 0 \\ \left| {q_0} \right\rangle U \left| { q_1} \right\rangle &amp;{}\text { if } q_0 = 1 \end{array}\right. } \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ40.png)(40)同样，当两个输入比特都是在基态时，我们可以用一种简写的符号来表示幺正操作的矩阵幂 ![$$I\otimes U^{k}$$](img/516210_1_En_1_Chapter_TeX_IEq224.png)，其中 *k* 是控制位的计算基值。我们用这样的符号来代表控制门，用 ![$$I\otimes U^{k}$$](img/516210_1_En_1_Chapter_TeX_IEq224.png) 替换异或操作，如图 4 所示。幺正矩阵类似于等式 39 的矩阵；现在 *U* 是底部右侧四分之一的 ![$$(2 \times 2)$$](img/516210_1_En_1_Chapter_TeX_IEq225.png) 矩阵。![](img/516210_1_En_1_Fig4_HTML.png)

第 4 图

CU 门的作用

![$$\begin{aligned} CU = \begin{pmatrix} 1&amp;{}0&amp;{}0&amp;{}0 \\ 0&amp;{}1&amp;{}0&amp;{}0 \\ 0&amp;{}0&amp;{}a&amp;{}b \\ 0&amp;{}0&amp;{}c&amp;{}d \end{pmatrix} = \begin{pmatrix} \begin{array}{c | c} I &amp;{} 0 \\ \hline 0 &amp;{} U \end{array} \end{pmatrix}\end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ41.png)(41)引理 1

受控幺正门可以分解为两个 CNOT 门和单量子比特门。

单量子比特幺正矩阵，也称为*U*(2)矩阵，可以表示为布洛赫球上的正交旋转对。首先，我们定义沿两个不同轴的三个旋转角。根据[53]中的引理 4.1，![$$\begin{aligned} U = e^{i\delta } \cdot R_z(\alpha ) \cdot R_y(\theta ) \cdot R_z(\beta ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ42.png)。此外，一般的![$$2 \times 2$$](img/516210_1_En_1_Chapter_TeX_IEq226.png)幺正矩阵也可以写成形式![$$U = e^{i\delta }A \cdot X \cdot B \cdot X \cdot C $$](img/516210_1_En_1_Chapter_TeX_IEq227.png)，其中![$$A\cdot B \cdot C = I$$](img/516210_1_En_1_Chapter_TeX_IEq228.png)。为了证明这一点，设置

+   ![$$A = R_z(\alpha ) \cdot R_y(\frac{\theta }{2})$$](img/516210_1_En_1_Chapter_TeX_IEq229.png)

+   ![$$B = R_y(-\frac{\theta }{2})\cdot R_z(-\frac{\alpha + \beta }{2})$$](img/516210_1_En_1_Chapter_TeX_IEq230.png)

+   ![$$C = R_z(\frac{\beta - \alpha }{2})$$](img/516210_1_En_1_Chapter_TeX_IEq231.png).

现在，要将此转化为一个受控幺正操作，我们将 *A*、*B*、*C* 置于两个 CNOT 门的目标之间。如果控制输入为 ![$$|0\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq232.png)，那么目标上的结果为 ![$$A\cdot B \cdot C = I$$](img/516210_1_En_1_Chapter_TeX_IEq233.png)，对输入没有影响。如果控制输入为 1，那么目标上的结果为 ![$$A \cdot X \cdot B \cdot X \cdot C $$](img/516210_1_En_1_Chapter_TeX_IEq234.png)。这个行为相当于 CNOT 门的行为。请注意，我们仍然缺少一个受控全局相位操作 ![$$e^{i\delta }$$](img/516210_1_En_1_Chapter_TeX_IEq235.png)。我们通过在控制比特的任意位置添加相位门 ![$$P(\delta )$$](img/516210_1_En_1_Chapter_TeX_IEq236.png) 来解决这个问题。我们现在有了一个将 CU 门分解为 CNOT 和单比特门的分解方案（图 5）。   ![$$\square $$](img/516210_1_En_1_Chapter_TeX_IEq237.png)

![](img/516210_1_En_1_Fig5_HTML.png)

图 5

任意受控幺正门的分解

现在我们将注意力转移到具有更多控制比特的控制操作上。

### 2.2 符号表示

控制操作 CU(*n*) 对量子电路的 *n* 量子比特子集执行一个非平凡的变换，并使用 ![$$n-1$$](img/516210_1_En_1_Chapter_TeX_IEq238.png) 个控制比特和 1 个目标比特。为方便起见，我们将所有目标比特的排列都称为图 6 中所示的 CU(4)。

图 6

这 4 个门都称为 CU(4)

为了讨论不同分解技术的复杂性，我们将门的一个实例表示为一个标量，表示其 CNOT 计数。然后，我们根据它们的构造将这些门分类到不同的集合中。方便地，我们还可以将这些集合定义为以 *n* 为参数的序列，其中 *n* 是门作用的量子比特数。我们还研究了其他电路资源，例如使用辅助比特或引入非平凡的相对相位。最后，我们概述了对于任何给定的电路大小和约束条件的最有效构造。

在本章的其余部分，我们将重点讨论 CX(n) 的构造，但请注意，所提出的方法可以用来构造任何单位 CU(*n*) 门。

### 2.3 定义

我们概述了 CX(*n*) 和其相对相位的表征矩阵的一些定义，即 RCX(*n*)。我们还定义了一些有助于我们操纵这些门的恒等式。

Definition 1The permutation of the CX(*n*) gate whose target is the lowest bit has the unitary matrix representation.![$$\begin{aligned} \text {CX}(n) = \text {diag} \bigg \{ 1, 1, 1, ..., \begin{pmatrix} 0&amp;{}1 \\ 1&amp;{}0\end{pmatrix} \bigg \} \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ43.png)(43)When acting on an *n*-bit system, the action of ![$$\text {CX}(n)$$](img/516210_1_En_1_Chapter_TeX_IEq239.png) is given by![$$\begin{aligned} \text {CX}(n) \left| {x_1, x_2, ..., x_n} \right\rangle = \left| {x_1, x_2, ... x_{n-1}} \right\rangle X^{\prod ^{n-1}_{i = 1} x_i} \left| {x_n} \right\rangle \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ44.png)(44)Definition 2Given a unitary matrix *U*, its relative phase version is a unitary matrix *V* such that ![$$|u_{i,j}|=|v_{i,j}|$$](img/516210_1_En_1_Chapter_TeX_IEq240.png) for all *i*, *j*, which implies that the magnitude of all elements of *U* and *V* is equal. Using this definition we can define the RCX(*n*) gate, the relative phase version of the ![$$\text {CX}(n)$$](img/516210_1_En_1_Chapter_TeX_IEq241.png) gate, as![$$\begin{aligned} \text {RCX}(n) = \text {diag} \bigg \{ z_0, z_1, ..., z_{2^{n}-3}, \begin{pmatrix} 0&amp;{}z_{2^{n}-2} \\ z_{2^{n}-1}&amp;{}0\end{pmatrix} \bigg \} \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ45.png)(45)where ![$$z_j = e^{i\theta _j}$$](img/516210_1_En_1_Chapter_TeX_IEq242.png). By [54], we can express the RCX(*n*) as the matrix product of ![$$\text {CX}(n)$$](img/516210_1_En_1_Chapter_TeX_IEq243.png) and a diagonal phased matrix *D*(*n*).![$$\begin{aligned} \text {RCX}(n) = D(n) \cdot \text {CX}(n) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ46.png)(46)where ![$$D(n) = \text {diag} \bigg \{ z_0, z_1, ..., z_{2^n - 1} \bigg \}, \text { with } z_j = e^{i\theta _j}$$](img/516210_1_En_1_Chapter_TeX_IEq244.png).Definition 3The inverse of a ![$$\text {RCX}(n)$$](img/516210_1_En_1_Chapter_TeX_IEq245.png) gate is also a ![$$\text {RCX}(n)$$](img/516210_1_En_1_Chapter_TeX_IEq246.png) gate. This identity is very powerful because it allows us to reverse the presence of any relative phase when using ![$$\text {RCX}(n)$$](img/516210_1_En_1_Chapter_TeX_IEq247.png) in our constructions. We are also using, without proof, the identity ![$$\text {CX}(n) = \text {CX}^{-1}(n)$$](img/516210_1_En_1_Chapter_TeX_IEq248.png).![$$\begin{aligned} \text {RCX}^{-1}(n)&amp;= \big [ D(n) \cdot \text {CX}(n) \big ] ^{-1} \nonumber \\&amp;= \text {CX}^{-1}(n) \cdot D(n)^{-1} \nonumber \\&amp;= \text {CX}(n) \cdot D^{-1}(n) \end{aligned}$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_Equ47.png)(47)where ![$$D^{-1}(n) = \text {diag} \bigg \{ \overline{z}_0, \overline{z}_1, ..., \overline{z}_{2^n - 1} \bigg \}, \text { with } \overline{z}_j = e^{-i\theta _j}$$](img/516210_1_En_1_Chapter_TeX_IEq249.png).Definition 4An arbitrary ![$$m+n+p$$](img/516210_1_En_1_Chapter_TeX_IEq250.png) qubit oracle ![$$U_f$$](img/516210_1_En_1_Chapter_TeX_IEq251.png) nested between RCX(*n*) and its inverse RCX![$$^{-1}(n)$$](img/516210_1_En_1_Chapter_TeX_IEq252.png) satisfies the identity![$$\begin{aligned}{}[I^m \otimes \text {RCX}(n) \otimes I^p] \cdot U_f \cdot [I^m \otimes \text {RCX}^{-1}(n) \otimes I^p] = [I^m \otimes \text {CX}(n) \otimes I^p] \cdot U_f \cdot [I^m \otimes \text {CX}(n) \otimes I^p] \end{aligned}$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_Equ48.png)(48)![](img/516210_1_En_1_Equ85_HTML.png)![$$\begin{aligned}{}[I^m \otimes D(n) \otimes I^p] \cdot U_f \cdot [I^m \otimes D^{-1}(n) \otimes I^p] = U_f \end{aligned}$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_Equ49.png)(49)We define the oracle ![$$U_f$$](img/516210_1_En_1_Chapter_TeX_IEq253.png) such that it transforms the *p*-qubits based on the values of the *n*-qubits above it.ProofVisually, we have the following circuit. Expand RCX(*n*) and RCX![$$^{-1}(n)$$](img/516210_1_En_1_Chapter_TeX_IEq254.png) into its phased and non-phased components, and cancel the two exterior CX(*n*) gates from both sides, we get (see Figs. 7, 8 and 9).![](img/516210_1_En_1_Fig7_HTML.png)

图 7

等式 4 中的标识

![](img/516210_1_En_1_Fig8_HTML.png)

图 8

调用定义 3

![](img/516210_1_En_1_Fig9_HTML.png)

图 9

由于![$$U_f$$](img/516210_1_En_1_Chapter_TeX_IEq255.png)不影响顶部的![$$m+n$$](img/516210_1_En_1_Chapter_TeX_IEq256.png)个量子位，两个对角矩阵与其交换并相互抵消。

![$$\square $$](img/516210_1_En_1_Chapter_TeX_IEq257.png)

### 2.4 Sleator-Weinfurter 构造

![$$\text {CX}(n)$$](img/516210_1_En_1_Chapter_TeX_IEq258.png) 门的最简单情况是 Toffoli 门。我们首先展示 Sleator-Weinfurter 构造[55]（见图 10）。其中 ![$$V² = X$$](img/516210_1_En_1_Chapter_TeX_IEq259.png)。由于 ![$$X = e^{i\frac{\pi }{2}} R_x(\pi )$$](img/516210_1_En_1_Chapter_TeX_IEq260.png)，我们可以推导出 ![$$V = \sqrt{X} = e^{i\frac{\pi }{4}} R_x(\frac{\pi }{2})$$](img/516210_1_En_1_Chapter_TeX_IEq261.png)。使用等式 35 中的身份，我们得到！$$\begin{aligned} e^{i\frac{\pi }{4}} R_x\bigg (\frac{\pi }{2}\bigg )&amp;= e^{i\frac{\pi }{4}} H \cdot R_z\bigg (\frac{\pi }{2}\bigg ) \cdot H \end{aligned}$$(50)![$$\begin{aligned}&amp;= H \cdot S \cdot H \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ51.png)(51)![](img/516210_1_En_1_Fig10_HTML.png)

图 10

Sleator-Weinfurter 构造

现在，我们用*H*和*P*门代替*V*和![$$V^\dagger $$](img/516210_1_En_1_Chapter_TeX_IEq262.png)。严格看目标线，我们看到所有内部*H*门相互抵消，只留下两个外部的*H*门。这是构建 CX(*n*) 门的常见方法，我们首先构建 CZ(*n*) 门，然后在目标位的两侧围绕*H*门以形成 CX(*n*)。为了分析这个电路的作用，我们根据输入![$$x_1$$](img/516210_1_En_1_Chapter_TeX_IEq263.png) 和 ![$$x_2$$](img/516210_1_En_1_Chapter_TeX_IEq264.png)（见图 11）来观察作用在目标位上的操作。![](img/516210_1_En_1_Fig11_HTML.png)

图 11

采用可控相位门的 Sleator-Weinfurter 构造方法

![$$\begin{aligned} HSH \text { 如果 } x_1 = 1 \quad&amp;(10) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ52.png)(52)![$$\begin{aligned} HS^\dagger H \text { 如果 } x_1 \oplus x_2 = 1 \quad&amp;(11) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ53.png)(53)![$$\begin{aligned} HSH \text { 如果 } x_2 = 1 \quad&amp;(01) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ54.png)(54)总体上，作用在目标位上的门是 ![$$X^k$$](img/516210_1_En_1_Chapter_TeX_IEq265.png)，其中 ![$$\begin{aligned} k = x_1 + x_2 - (x_1 \oplus x_2) = 2\cdot (x_1 \wedge x_2) = 2 \cdot (x_1 \cdot x_2) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ55.png)(55)。这与等式 43 中 CX(*n*) 门的定义一致。根据图 4，每个可控相位门 CP 分解为 2 个 CNOT 门。总之，这个构造方法使用了 ![$$3\cdot 2 + 2 = 8$$](img/516210_1_En_1_Chapter_TeX_IEq266.png) 个 CNOT 门。

### 2.5 最佳 CNOT Toffoli 电路

Toffoli 门的最佳构造使用 6 个 CNOT 门。要推导出这个构造，我们首先概述一些有用的引理。

Lemma 2

相位门，比如![$$R_z$$](img/516210_1_En_1_Chapter_TeX_IEq267.png)，与 CNOT 的控制相交换。

Proof

观察到相位门和 CNOT 的控制都不影响输入的比特值。这也适用于*P*门，因为它们相当于![$$R_z$$](img/516210_1_En_1_Chapter_TeX_IEq268.png)加上一个全局相位。 ![$$\square $$](img/516210_1_En_1_Chapter_TeX_IEq269.png)

Lemma 3

X 轴旋转门，比如![$$R_x$$](img/516210_1_En_1_Chapter_TeX_IEq270.png)，与 CNOT 的目标相交换。

证明根据控制位的输入值，目标位有两种可能的动作，*I*或*X*。第一种情况是显而易见的，![$$\begin{aligned} I R_x(\theta ) = R_x(\theta ) I = R_x\end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ56.png)(56)第二种情况依赖于![$$R_x(\pi )= iX$$](img/516210_1_En_1_Chapter_TeX_IEq271.png)的事实。![$$\begin{aligned} X R_x(\theta )&amp;= -i R_x(\pi ) R_x(\theta ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ57.png)(57)![$$\begin{aligned}&amp;=R_x(\theta ) \big ( -iR_x(\pi ) \big ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ58.png)(58)![$$\begin{aligned}&amp;=R_x(\theta ) X \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ59.png)(59)因此，我们证明了*I*和*X*都是![$$R_x$$](img/516210_1_En_1_Chapter_TeX_IEq272.png)旋转。 ![$$\square $$](img/516210_1_En_1_Chapter_TeX_IEq273.png)Lemma 4

相位门与 Ising 耦合门可交换![$$R_{zz}$$](img/516210_1_En_1_Chapter_TeX_IEq274.png)。

证明 Ising 耦合门![$$R_{zz}$$](img/516210_1_En_1_Chapter_TeX_IEq275.png)具有参数化![$$\begin{aligned} R_{zz}(\theta )= \exp \big ( -i\frac{\theta }{2} Z\otimes Z\big ) = \begin{pmatrix} R_z(\theta ) &{} 0 \\ 0 &{} R_z(-\theta ) \end{pmatrix} \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ60.png)(60)注意它是对角矩阵。我们有两个选择来放置我们的相位门，![$$I \otimes R_z$$](img/516210_1_En_1_Chapter_TeX_IEq276.png)和![$$R_z \otimes I$$](img/516210_1_En_1_Chapter_TeX_IEq277.png)。作为练习，证明这两个都是对角矩阵。由于对角矩阵可交换，我们得到![$$R_{zz}$$](img/516210_1_En_1_Chapter_TeX_IEq278.png)和![$$I \otimes R_z$$](img/516210_1_En_1_Chapter_TeX_IEq279.png)（同样![$$R_z \otimes I$$](img/516210_1_En_1_Chapter_TeX_IEq280.png)）可交换。    ![$$\square $$](img/516210_1_En_1_Chapter_TeX_IEq281.png)我们将引理 4 重新表达为量子电路形式。首先，我们展示 Ising ![$$R_{zz}$$](img/516210_1_En_1_Chapter_TeX_IEq282.png) 门的分解为 CNOT 门和![$$R_z$$](img/516210_1_En_1_Chapter_TeX_IEq283.png) 门。注意，这种分解强调了![$$R_{zz}$$](img/516210_1_En_1_Chapter_TeX_IEq284.png) 门的对称性质。如果我们的相位门在顶部量子位上，它只需通过引理 2 移到另一侧。现在我们将引理 4 重新表述为电路等式（见图 12）。![](img/516210_1_En_1_Fig12_HTML.png)

图 12

Ising ![$$R_{zz}$$](img/516210_1_En_1_Chapter_TeX_IEq285.png) 作为量子门

引理 5

（引理 4 作为电路恒等式）相位门与另外两个 CNOT 门以及它们之间的另一个相位门可以交换位置（见图 13）。

![](img/516210_1_En_1_Fig13_HTML.png)

图 13

Ising ![$$R_{zz}$$](img/516210_1_En_1_Chapter_TeX_IEq286.png) 作为量子门

引理 6

这两个电路等价性是正确的（见图 14 和 15）。

![](img/516210_1_En_1_Fig14_HTML.png)

图 14

简化 CNOT 级联

![](img/516210_1_En_1_Fig15_HTML.png)

图 15

CNOT 镜像恒等式

证明

通过验证每个等价关系的八个基础输入/输出对。    ![$$\square $$](img/516210_1_En_1_Chapter_TeX_IEq287.png)

定理 7

Toffoli 门的最佳构建使用了 6 个 CNOT 门

在这里，我们只会证明这种构建是可能的。要证明其在 CNOT 门方面的最佳性，请参见[56]。

证明

我们首先将图 11 中的所有控制相位门展开为 CNOT 和相位门，使用引理 1。然后，我们使用引理 2、3、4（更具体地说是图 12 中的分解）来调整门的位置，并使用引理 6 来取消多余的 CNOT 门。作为练习，我们把细节留给读者。最后，我们得到了图 16 所示的最佳构建。    ![$$\square $$](img/516210_1_En_1_Chapter_TeX_IEq288.png)

### 2.6 递归相对相位 Toffoli

我们偏离了正常的 CX(*n*) 构建，讨论了 RCX(*n*) 构建。回顾一下，这与 CX(*n*) 等效，只是当其矩阵元素非零时可能有相对相位的可能性（45）。我们将看看 Minh Pham 和 Emilio Peláez 提出的递归构建。

#### 2.6.1 构造

我们概述了一种递归方案来构建 RCX(*n*)门。我们从三个基本情况开始：CNOT，RCX(3)和 RCX(4)。

注意![$$\cong $$](img/516210_1_En_1_Chapter_TeX_IEq289.png)表示右侧电路是左侧电路的相对相位版本。在最终分解和门计数中，我们考虑右侧的电路（参见图 17）。![](img/516210_1_En_1_Fig16_HTML.png)

图 16

Toffoli 门的最佳构造

注意 RCX(4)（图 18）有 3 个 CNOT 对。一个控制位在量子比特*a*上，另一个在量子比特*b*上，还有一个在量子比特*c*上。我们可以通过首先将量子比特*a*的 CNOT 扩展为 CX(3)来构建 RCX(5)。然后，我们可以用图 17 中显示的 RCX(3)基本情况替换普通的 CX(3)。类似地，对于 RCX(6)和 RCX(7)，我们可以将 CNOT 对扩展为 CX(3)，并用 RCX(3)替换这些。对于 RCX(8)，RCX(9)和 RCX(10)，我们重复上述过程，但这次将 CNOT 对扩展为 CX(4)，并用 RCX(4)替换这些。一般来说，对于任意 RCX(*n*)其中![$$n&gt;4$$](img/516210_1_En_1_Chapter_TeX_IEq290.png)，构造如下（图 19 和 20）。

1.  1.

    从 RCX(4)的结构开始

1.  2.

    将*a*量子比特的 CNOT 对扩展成 CX(![$${\lceil \frac{n-1}{3} \rceil }$$](img/516210_1_En_1_Chapter_TeX_IEq291.png)),

1.  3.

    将*b*量子比特的 CNOT 对扩展到 CX(![$${\lfloor \frac{n-1}{3} \rfloor }$$](img/516210_1_En_1_Chapter_TeX_IEq292.png))

1.  4.

    将*c*量子比特的 CNOT 对扩展到 CX(![$${n-1- \lceil \frac{n-1}{3} \rceil - \lfloor \frac{n-1}{3} \rfloor }$$](img/516210_1_En_1_Chapter_TeX_IEq293.png)).

1.  5.

    然后，使用与步骤 1-3 中概述的相同过程分解最后三个门。我们重复步骤 1-5，直到所有门都分解为基本情况中的门。最后，我们用相应的相位门替换这些门。

![](img/516210_1_En_1_Fig17_HTML.png)

图 17

RCX(3) 使用 3 个 CNOT 门和 4 个相位门

![](img/516210_1_En_1_Fig18_HTML.png)

图 18

RCX(4) 使用 6 个 CNOT 门和 8 个相位门

![](img/516210_1_En_1_Fig19_HTML.png)

图 19

从 RCX(4) 到 RCX(5)

![](img/516210_1_En_1_Fig20_HTML.png)

图 20

用 RCX(3) 替换普通的 CX(3)

#### 2.6.2 CNOT 计数和应用

当我们从 RCX![$$(n-1)$$](img/516210_1_En_1_Chapter_TeX_IEq294.png)转向 RCX(*n*)时，我们将两个 RCX![$$(\lceil \frac{n-1}{3}\rceil -1)$$](img/516210_1_En_1_Chapter_TeX_IEq295.png)替换为两个 RCX![$$(\lceil \frac{n-1}{3} \rceil )$$](img/516210_1_En_1_Chapter_TeX_IEq296.png)门。因此，任何 RCX(*n*)门的成本，其中![$$n \ge 5 $$](img/516210_1_En_1_Chapter_TeX_IEq297.png)，由以下关系给出：![$$\begin{aligned} \text {RCX}(n) = \text {RCX}(n-1) + 2\cdot \text {RCX}\bigg (\lceil \frac{n-1}{3}\rceil \bigg ) - 2\cdot \text {RCX}\big (\lceil \frac{n-1}{3}\rceil -1 \big ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ61.png)(61)在渐进情况下，这个关系按照![$$\Theta (n^{\log _6{3}})$$](img/516210_1_En_1_Chapter_TeX_IEq298.png)的速度增长。RCX 门的应用由方程 4 给出，每当 RCX 和 RCX![$${}^{-1}$$](img/516210_1_En_1_Chapter_TeX_IEq299.png)同时使用时。例如，当我们讨论 Barenco 等人提出的二次构造时，我们将会遇到以下配置[53]（图 27）。在这里，通过 RCX 门替换 CX 门将显著减少所使用的 CNOT 数量（参见图 21）。![](img/516210_1_En_1_Fig21_HTML.png)

图 21

应用 RCX(*n*)门

### 2.7 V-链分解

如果允许使用辅助位，我们可以使用线性数量的 CNOT 构造 CX(*n*) 门。每当必要时，我们在门旁边的上标中标明使用/允许的辅助位数。我们将讨论 Maslov [54] 的 V-Chain 分解，这是 Barenco 等人第 7.2 引理的改进 [53]。我们可以通过引入前一节讨论的 RCX 门进一步改进这一技术。这种技术使用 ![$${\lceil {\frac{n-6}{2}}\rceil }$$](img/516210_1_En_1_Chapter_TeX_IEq300.png) 借用位来构建 CX(*n*) 门。这些位要求在计算后将辅助量子位返回到原始状态。

#### 2.7.1 构造

从现在开始，我们用方括号表示门作用的量子比特集合，最后一个元素是目标位。最顶部的量子比特索引为 1，其余依次升序排列。对于 ![$$n \ge 8$$](img/516210_1_En_1_Chapter_TeX_IEq301.png)，构造定义如下：

1.  1.

    从大小为 ![$$m = n + \lceil \frac{n-6}{2}\rceil $$](img/516210_1_En_1_Chapter_TeX_IEq302.png) 的电路开始。顶部 ![$$n-1$$](img/516210_1_En_1_Chapter_TeX_IEq303.png) 位是控制位。接下来的 ![$$\lceil \frac{n-6}{2}\rceil $$](img/516210_1_En_1_Chapter_TeX_IEq304.png) 位是辅助位。底部位是目标位。

1.  2.

    第一个门是 CX(![$$3) [n-1, m-1, m]$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq305.png)。

1.  3.

    如果 *n* 是奇数，放置 CX(![$$3)[n-2, m-2, m-1]$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq306.png)。否则，跳过此步骤。

1.  4.

    当 ![$$n > 8$$](img/516210_1_En_1_Chapter_TeX_IEq307.png) 时，对于每个 *k* 在 ![$$\lfloor \frac{n-8}{2} \rfloor , ..., 1$$](img/516210_1_En_1_Chapter_TeX_IEq308.png)，放置 CX(![$$4) [2k+5, 2k+6, n+k-1, n+k] $$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq309.png)。

1.  5.

    接下来是 CX(7) [1, 2, 3, 4, 5, 6, *n*]。

1.  6.

    当 ![$$n > 8$$](img/516210_1_En_1_Chapter_TeX_IEq310.png) 时，对于每个 *k* 在 ![$$1,..., \lfloor \frac{n-8}{2} \rfloor $$](img/516210_1_En_1_Chapter_TeX_IEq311.png)，放置 CX(![$$4) [2k+5, 2k+6, n+k-1, n+k]$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq312.png)（步骤 4 的顺序相反）。

1.  7.

    如果 *n* 是奇数，放置 CX(![$$3)[n-2, m-2, m-1]$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq313.png)。否则，跳过此步骤。

1.  8.

    下一个门是 CX(![$$3) [n-1, m-1, m]$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq314.png)。

1.  9.

    实现步骤 3。

1.  10.

    实现步骤 4。

1.  11.

    接下来是 CX(7) [1, 2, 3, 4, 5, 6, *n*]。

1.  12.

    实现步骤 6。

1.  13.

    实现步骤 7。

我们将通过示例解释这种构造背后的动机，示例为图 22 中显示的![$$n = 11$$](img/516210_1_En_1_Chapter_TeX_IEq315.png)。在这个示例中，有 10 个控制位，标记为 *A* 到 *J*，以及 3 个辅助位，标记为![$$a_1$$](img/516210_1_En_1_Chapter_TeX_IEq316.png)到![$$a_3$$](img/516210_1_En_1_Chapter_TeX_IEq317.png)。左侧山脉（步骤 2–8）将控制位的乘积累积到目标中。这是通过将乘积的一部分存储在辅助位中来迭代完成的。首先，![$$a_1$$](img/516210_1_En_1_Chapter_TeX_IEq318.png)存储![$$a_1 \oplus ABCDEF$$](img/516210_1_En_1_Chapter_TeX_IEq319.png)。然后，![$$a_2$$](img/516210_1_En_1_Chapter_TeX_IEq320.png)存储![$$a_2 \oplus ABCDEFGH$$](img/516210_1_En_1_Chapter_TeX_IEq321.png)。之后，![$$a_3$$](img/516210_1_En_1_Chapter_TeX_IEq322.png)存储![$$a_3 \oplus ABCDEFGHI$$](img/516210_1_En_1_Chapter_TeX_IEq323.png)。最后，目标 *t* 变为![$$t \oplus ABCDEFGHIJ$$](img/516210_1_En_1_Chapter_TeX_IEq324.png)。然而，需要注意我们必须将辅助位恢复到原始状态。右侧山脉（步骤 9–13）通过向每个辅助位添加（模 2）与第一座山脉相同的乘积来实现这一点。由于![$$(x \oplus y) \oplus y = x$$](img/516210_1_En_1_Chapter_TeX_IEq325.png)，我们成功地恢复了辅助位的原始值。在 V 链的高效构造中的关键是用 RCX 门替换所有 CX 门。我们引入了四个门，在这种构造的背景下更容易实现，其中三个来自 Maslov[54]。![](img/516210_1_En_1_Fig22_HTML.png)

图 22

CX(11)的 V 链构造

1.  1.

    ![$${\textbf {SRTS}}$$](img/516210_1_En_1_Chapter_TeX_IEq326.png). 这是图 16 中的部分 Toffoli。 当与其逆 SRTS![$${}^{-1}$$](img/516210_1_En_1_Chapter_TeX_IEq327.png)一起使用时，我们可以消去 2 个 CNOT 门。 总共包含 4 个 CNOT 门。 我们在第 2 步中用 SRTS 替换，在第 8 步中用 SRTS![$${}^{-1}$$](img/516210_1_En_1_Chapter_TeX_IEq328.png)替换。

1.  2.

    ![$${\textbf {RTS}}$$](img/516210_1_En_1_Chapter_TeX_IEq329.png). 当 RCX(3)与 RCX![$${}^{-1}(3)$$](img/516210_1_En_1_Chapter_TeX_IEq330.png)一起使用时，我们可以消去一个完整的 CNOT 门。 结果是 RTS。 电路包含 2 个 CNOT 门。 我们在第 3 步中用 RTS 替换，第 7 步中用 RTS![$${}^{-1}$$](img/516210_1_En_1_Chapter_TeX_IEq331.png)替换。

1.  3.

    ![$${\textbf {RT4S}}$$](img/516210_1_En_1_Chapter_TeX_IEq332.png). 这是 RCX(4)电路与其逆消除后的剩余部分。 实现使用 4 个 CNOT。 我们在第 4 步中用 RT4S 替换，在第 6 步中用 RT4S![$${}^{-1}$$](img/516210_1_En_1_Chapter_TeX_IEq333.png)替换。

1.  4.

    ![$${\textbf {RT7L}}$$](img/516210_1_En_1_Chapter_TeX_IEq334.png). 这个电路等价于 RCX(7)。 但是，为了与原始文献保持一致，我们将其称为 RT7L。 RT7L 由 18 个 CNOT 组成。 我们在第 5 步中用 RT7L 替换，在第 11 步中用 RT7L![$${}^{-1}$$](img/516210_1_En_1_Chapter_TeX_IEq335.png)替换（参见图 23、24、25、26 和 27）。

![](img/516210_1_En_1_Fig23_HTML.png)

图 23

SRTS 电路：4 个 CNOT 门

![](img/516210_1_En_1_Fig24_HTML.png)

图 24

RTS 电路：2 个 CNOT 门

![](img/516210_1_En_1_Fig25_HTML.png)

图 25

RT4S 电路：4 CNOTs

![](img/516210_1_En_1_Fig26_HTML.png)

图 26

RT7L 电路：18 CNOTs

要创建上述任何门的逆门，我们翻转门操作的顺序并反转它们的相位。将上述门替换到电路中会导致 CX(*n*) 的构造，使用了 ![$$\lceil \frac{n-6}{2} \rceil $$](img/516210_1_En_1_Chapter_TeX_IEq336.png) 个辅助比特，这比原文[54]中使用的 ![$$\lceil \frac{n-3}{2} \rceil $$](img/516210_1_En_1_Chapter_TeX_IEq337.png) 有所改善。![](img/516210_1_En_1_Fig27_HTML.png)

图 27

CX(11) 的替代示例

#### 2.7.2 CNOT 数量

我们从 ![$$n = 8$$](img/516210_1_En_1_Chapter_TeX_IEq338.png) 开始，这需要 2 个 RT7L 和 2 个 SRTS 门，总共需要 44 个 CNOTs。对于更大的 *n* 值，我们要么添加 4 个 RTS 门来构建 ![$$n+1$$](img/516210_1_En_1_Chapter_TeX_IEq339.png)，要么添加 4 个 RT4S 门来构建 ![$$n+2$$](img/516210_1_En_1_Chapter_TeX_IEq340.png)。两者都会使每个量子比特的 CNOT 计数增加 8。因此，我们构造 CX(*n*) 使用了 ![$$8n-20$$](img/516210_1_En_1_Chapter_TeX_IEq341.png) 个 CNOT 门。

### 2.8 二次分解

这个分解方案来自 Barenco 等人[53]。在某种程度上，它是图 11 结构的延伸，其中 CX(1) 和 CS(1) 门变成了 CX![$$(n-1)$$](img/516210_1_En_1_Chapter_TeX_IEq342.png) 和 CS![$$(n-1)$$](img/516210_1_En_1_Chapter_TeX_IEq343.png) 门。

#### 2.8.1 构造

在这里，我们将描述 CX(*n*) 门的构造。对于任意的 CX(*n*) 门，我们可以将其分解为 2 个 CX![$$(n-1)$$](img/516210_1_En_1_Chapter_TeX_IEq344.png)、CS、CS![$${}^\dagger $$](img/516210_1_En_1_Chapter_TeX_IEq345.png) 和 CS![$$(n-1)$$](img/516210_1_En_1_Chapter_TeX_IEq346.png)。请注意，我们不计算两个 Hadamards，因为它们是单量子比特门，许多指标认为它们是微不足道的。![](img/516210_1_En_1_Fig28_HTML.png)

第 28 图

例子：CX(5)

然后，我们可以将 CS![$$(n-1)$$](img/516210_1_En_1_Chapter_TeX_IEq347.png) 进一步分解为 2 个 CX![$$(n-2)$$](img/516210_1_En_1_Chapter_TeX_IEq348.png)、CT、CT![$${}^\dagger $$](img/516210_1_En_1_Chapter_TeX_IEq349.png) 和 CT![$$(n-2)$$](img/516210_1_En_1_Chapter_TeX_IEq350.png)（见图 28 和 29）。![](img/516210_1_En_1_Fig29_HTML.png)

第 29 图

例子：CS(4)

从现在开始，括号中的数字指的是每当控制相位门中有参数 ![$$\theta $$](img/516210_1_En_1_Chapter_TeX_IEq351.png) 时的角度。如果没有，括号内的值将指的是所讨论门作用于的量子比特数。一般来说，对于任意的 CP![$${}_\theta (n)$$](img/516210_1_En_1_Chapter_TeX_IEq352.png) 门，我们可以将其分解为 2 个 CX![$$(n-1)$$](img/516210_1_En_1_Chapter_TeX_IEq353.png)、CP![$$({\frac{\theta }{2}})$$](img/516210_1_En_1_Chapter_TeX_IEq354.png)、CP![$${}^\dagger ({\frac{\theta }{2}})$$](img/516210_1_En_1_Chapter_TeX_IEq355.png) 和 CP![$${}_{\frac{\theta }{2}}(n-1)$$](img/516210_1_En_1_Chapter_TeX_IEq356.png)。我们对 CP![$${}_{\frac{\theta }{2}}(n-1)$$](img/516210_1_En_1_Chapter_TeX_IEq357.png) 重复此过程，直到达到基本情况 CP![$$({\frac{\theta }{2^{n-2}}})$$](img/516210_1_En_1_Chapter_TeX_IEq358.png)。我们在下面展示了 CX(5) 的分解示例（参见图 30）。![](img/516210_1_En_1_Fig30_HTML.png)

图 30

示例：CX(5) 的完全分解

方框中的角度 ![$$\theta $$](img/516210_1_En_1_Chapter_TeX_IEq359.png) 表示相位门 ![$$P(\theta )$$](img/516210_1_En_1_Chapter_TeX_IEq360.png)。

我们需要做的是分解电路中所有的 CP 和 CX(*m*) 门。我们在引理 1 中概述了 CP 分解。至于 CX(*m*) 门，有几种方法可以做到这一点。最简单的方法是用第 2.5 节描述的 RCX (*m*) 门替换所有的 CX(*m*) 门。在![$$n \le 21$$](img/516210_1_En_1_Chapter_TeX_IEq361.png)的情况下，这种替换是最优的。在此之后，如果我们有足够的辅助比特，我们可以使用 Maslov 的技术 [54]。更具体地说，对于任意的 CX(*n*)，只要![$$m + \lceil \frac{m-6}{2} \rceil \le n$$](img/516210_1_En_1_Chapter_TeX_IEq362.png)，我们就可以像在第 2.7 节中描述的那样实现 RCX(*m*)。如果不是这种情况，我们可以使用 [57] 的构造。这种方法也会随着量子比特数量的线性增长而建立 RCX 的 CNOT 数。这种构造的技术细节超出了本章的范围。

#### 2.8.2 CNOT 计数

由于构造是递归的，我们可以为 CNOT 计数定义一个简单的递归关系。![$$\begin{aligned} \text {CX}(n) = 2 \text {CX}(n-1) + \text {CP}(n-1) + 2\text {CP}(2) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ62.png)(62)这个方程式来自于对图 28 的观察。该表达式的渐近行为取决于我们对 CX![$$(n-1)$$](img/516210_1_En_1_Chapter_TeX_IEq363.png)的选择。如果我们使用线性构造，那么我们有![$$\begin{aligned} \text {CX}(n) = \text {CP}(n-1) + \Theta (n) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ63.png)(63)这意味着 CX![$$(n) \in \Theta (n²)$$](img/516210_1_En_1_Chapter_TeX_IEq364.png)。另一方面，如果我们使用方程 61 中的![$$\Theta (n^{\log _3{6}})$$](img/516210_1_En_1_Chapter_TeX_IEq365.png)构造，那么我们的复杂度是超二次的。

### 2.9 总结

我们在下表中总结了我们提出的各种构造。对于每种技术，我们给出了构造是否导致相对相位矩阵，以及是否需要辅助位的详细信息。我们还描述了随着量子比特数量增加，每种构造所使用的 CNOT 门数量的增长（见表 2）。表 2

所述构造的摘要

| 构造 | 相对相位 | # 辅助位 | # CNOT |
| --- | --- | --- | --- |
| 递归相对相位 | 是 | 不适用 | ![$$\Theta (n^{log_3{6}})$$](img/516210_1_En_1_Chapter_TeX_IEq366.png) |
| V 链 | 否 | ![$$\lceil \frac{n-6}{2} \rceil $$](img/516210_1_En_1_Chapter_TeX_IEq367.png) | ![$$8n-20$$](img/516210_1_En_1_Chapter_TeX_IEq368.png) |
| 二次 | 否 | 不适用 | ![$$\ge \Theta (n²)$$](img/516210_1_En_1_Chapter_TeX_IEq369.png) |

## 3 量子错误校正

量子错误校正（QEC）是量子计算的一个必不可少且非常活跃的部分。它用于减轻由于噪声和退相干导致的量子信息中存在的错误。量子错误校正在量子信息科学的发展中起着重要作用，因为一旦我们处于适当的技术时代，它将帮助我们开发抵抗噪声、退相干和故障操作（如门、态准备和测量）的量子软件。这意味着即使量子硬件对噪声敏感，将来我们仍然可以在电路的特定部分添加错误检测和纠正代码以获得可靠的结果，尽管设备具有故障性。

基于电路表示的任何量子计算模型（例如超导量子比特和离子阱）都将需要错误校正[58]。这是由量子比特的特性决定的：它们很难与环境隔离，因此外部噪声很容易干扰它们的量子状态。我们将在第 3.1 节讨论一些可能引入噪声的因素。如果这种干扰不被纠正，将导致错误的计算，从而得到错误的输出。

从我们对经典计算的先前了解来看，我们可能的第一反应是假设经典的错误校正理论可以很容易地适应量子计算。然而，这是不可能的，因为量子比特可能经历比简单的位翻转更多类型的错误（我们将在第 3.2 节中探讨这一点）。因此，我们不能仅仅使用简要描述的经典计算中的技术（在第 3.3 节中），而是需要提出适用于量子计算领域的新技术。这是从第 3.4 节开始的话题。最后，我们将所有内容整合在一起，讨论更有用（也更复杂）的纠错码，见第 3.8 节。

关于该领域的最新发展，请参阅[59]。在这篇论文中，作者使用了一个十量子比特的离子阱量子计算机来编码一个单一逻辑量子比特，使用了[[7, 1, 3]]码（这种括号表示法在本节后面解释）。他们还能够准备一个具有足够低的错误率用于魔术状态蒸馏的逻辑![$$T|+\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq370.png)魔术状态，并实现非克利福德门。这些成就是迈向面向大规模用途的容错通用量子计算的关键步骤，远远超出了 NISQ 时代[61]。

### 3.1 噪声来源

量子计算中的错误可以由不良操作引入。其中一些是门、初始状态准备和最终测量。量子计算中另一个非常常见的错误来源是量子比特与环境的相互作用。由于没有技术能够完全隔离单个量子系统（在本例中即量子比特），量子比特与外界存在一定程度的相互作用。这种相互作用可以在计算过程中改变量子比特的状态，从而破坏其余部分的计算。

量子比特的本质也导致了我们所称之为弛豫和退相干现象。量子比特的弛豫与其从![$$|1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq371.png)到![$$|0\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq372.png)因“自然”原因而衰减的时间有关，即电路不经意地导致的。量子比特的退相干非常类似，但是针对的是相位。它与量子比特获取一些不经意的相位信息所需的时间有关。2000 年，DiVincenzo 提出了实现量子计算的三个标准[62]。第三个标准指出退相干时间应远远长于门操作时间，意味着量子比特必须在退相干和弛豫发生之前通过电路中的所有门。

探讨这个概念可能会使我们进入与本节意图不同的完全不同的讨论。因此，我们将不是专注于通过改进现有硬件来实现具有更长退相干时间的量子比特，而是关注这些（和其他因素）可能引入我们计算中的什么类型的错误，以及如何从软件方面检测和纠正它们。

### 3.2 错误类型

在经典计算中，唯一存在的错误类型是比特翻转： ![$$0 \xrightarrow {} 1$$](img/516210_1_En_1_Chapter_TeX_IEq373.png) 和其反向操作 ![$$1 \xrightarrow {} 0$$](img/516210_1_En_1_Chapter_TeX_IEq374.png)。这是一个相当简单的错误，因为在经典硬件中发生的机会很少，这要归功于几十年的硬件发展，而且由于当今的软件，检测和纠正也很容易。然而，在量子计算中，比特翻转并不罕见。正如之前讨论的，这种错误的一个原因是弛豫时间。截至 2019 年[63]，IBM 计算机的弛豫时间约为 50 微秒，这意味着比特翻转错误经常发生。尽管弛豫时间是指从激发态（![$$|1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq375.png)）到基态（![$$|0\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq376.png)）的时间，但反向比特翻转也可能发生。从 ![$$|0\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq377.png) 到 ![$$|1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq378.png) 的比特翻转确实更不常见，但由于故障门或其他噪声，它仍然可能发生；因此，在开发错误纠正代码时，我们需要考虑这一点。

此外，当涉及到量子计算时，比特翻转并不是唯一类型的错误。请记住，量子态引入了一种称为相位的东西，它是形式为 ![$$e^{i \theta }$$](img/516210_1_En_1_Chapter_TeX_IEq379.png) 的数字，它乘以状态向量的某些部分。例如，考虑状态 ![$$|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle )$$](img/516210_1_En_1_Chapter_TeX_IEq380.png)。可以向第二因子引入一个相位误差 ![$$e^{i \pi }$$](img/516210_1_En_1_Chapter_TeX_IEq381.png)，留下 ![$$\frac{1}{\sqrt{2}}(|0\rangle + e^{i \pi }|1\rangle ) = \frac{1}{\sqrt{2}}(|0\rangle -|1\rangle )=|-\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq382.png)。因此，一个相位错误已经将我们的状态从 ![$$|+\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq383.png) 改变为了 ![$$|-\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq384.png)，这可能对其余的计算产生重要影响。因此，我们还需要考虑这种类型的错误，这种错误事实证明是困难的，因为在经典计算中，我们习惯于只遇到简单的比特翻转。

引入比特翻转和相位错误后，我们可以将它们合并并将其视为一种单一类型的错误：旋转错误。这种错误可以被视为使状态从布洛赫球中的一点移动到另一点。像这样描述错误会使我们之前没有讨论过的一个困难变得明显。量子比特受到无限多个错误的影响，就像布洛赫球表面有无限多个点一样。幸运的是，多亏了 Knill 和 Laflamme [64]，我们知道纠正有限一组错误是充分条件，可以使我们纠正无限集合的任何错误。回到正轨，为了更数学地描述旋转错误，首先考虑量子比特的一般状态:![$$\begin{aligned} |\psi \rangle = \cos \frac{\theta }{2}|0\rangle + e^{i \phi } \sin \frac{\theta }{2}|1\rangle \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ64.png)(64)现在考虑代表旋转错误的操作符*E*。正如讨论的那样，这个错误是比特翻转和相位错误的组合。这里需要注意的一点是，虽然我们刚刚讨论了![$$|0\rangle \xrightarrow []{} |1\rangle $$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq385.png)和![$$|1\rangle \xrightarrow []{} |0\rangle $$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq386.png)的转换，但比特翻转可以推广到方程式 (64) 中参数![$$\theta $$](img/516210_1_En_1_Chapter_TeX_IEq387.png)的任何变化。换句话说，比特错误（我们现在省略“翻转”，因为它并不总是完全翻转）改变了状态中![$$|0\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq388.png)和![$$|1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq389.png)的数量。相位错误可以类似地描述为同一方程式中![$$\phi $$](img/516210_1_En_1_Chapter_TeX_IEq390.png)的变化。考虑到这一点，*E* 依赖于参数![$$\delta \theta $$](img/516210_1_En_1_Chapter_TeX_IEq391.png)和![$$\delta \phi $$](img/516210_1_En_1_Chapter_TeX_IEq392.png)，其效果描述为:![$$\begin{aligned} E(\delta \theta , \delta \phi ): \cos \frac{\theta }{2}|0\rangle + e^{i \phi } \sin \frac{\theta }{2}|1\rangle \xrightarrow {} \cos \frac{\theta + \delta \theta }{2}|0\rangle + e^{i (\phi + \delta \phi )} \sin \frac{\theta + \delta \theta }{2}|1\rangle . \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ65.png)(65)乍一看，要纠正这种错误并不太明显。我们现在不会深入讨论，但我们将简化方程式 (65)，这将在以后帮助我们。由于我们知道 *E* 是相位和翻转错误的组合，将其写成 *X* 和 *Z* 门的某种线性组合是有意义的，因为前者执行比特翻转，后者为![$$|1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq394.png)添加![$$-1$$](img/516210_1_En_1_Chapter_TeX_IEq393.png)相位。我们还需要考虑不引入错误的情况，即恒等门，以及 *XZ* 的情况（为了完整起见，以每个可能的方式到达布洛赫球上的每个点）。因此，我们可以将 *E* 写成:![$$\begin{aligned} E = \alpha _1I + \alpha _2 X + \alpha _3 Z + \alpha _4 XZ . \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ66.png)(66)回到一些段落，关于纠正有限一组错误就足以纠正任何可能错误的观点，我们可以使用方程式 (66) 来看到这个集合由 Pauli 集合 ![$$\{I, X, Z, XZ\}$$](img/516210_1_En_1_Chapter_TeX_IEq395.png) 构成。正如你所看到的，我们最终得到了我们开始的东西：我们有一个由 *X* 描述的错误和一个由 *Z* 描述的错误，并且纠正这些错误以及它们的任何线性组合将使我们能够纠正任何错误。那么，为什么

### 3.3 经典纠错

我们已经描述了我们在量子计算中会遇到的一般错误，现在我们想看看如何纠正它。首先，让我们退一步，回顾一下经典计算中使用的技术，并尝试将它们引入量子计算。我们将看到这些技术在量子情况下既不高效也不适用，更糟糕的是，它们没有考虑到整个错误谱。让我们从后者开始。很容易看出为什么经典纠错码没有考虑到*E*描述的错误：相位的概念在经典计算中根本不存在。因此，不深入探讨，我们已经知道经典码不起作用。然而，还有其他有趣的特性使经典码不适用于量子情况。

首先，我们需要简要描述经典纠错码的工作原理。有许多比我们将要描述的更复杂的编码，但它们都遇到同样的困难，因此一个简单的例子就足以说明问题。这个例子是重复码。它依赖于使用重复来编码信息。换句话说，它使用多于一个比特来表示一个比特的信息。我们将要探讨的具体例子使用 3 位来通过称为三位编码的方式编码一个比特的信息。简单地说，这种编码是通过将相同的比特重复 3 次来实现的。更数学化地说，这种编码将原始比特集合 ![$$\{0, 1\}$$](img/516210_1_En_1_Chapter_TeX_IEq396.png) 映射到逻辑码字集合 ![$$\mathcal {C} = \{000, 111\}$$](img/516210_1_En_1_Chapter_TeX_IEq397.png)。

因此，重复码的第一步是将原始二进制信息编码为逻辑码字。这也意味着使用这种纠错码的 *n* 位比特串将占用 3*n* 位。我们不会在这里担心这一点，因为我们正在考虑经典计算，其中设备中的晶体管数量足以使用这种昂贵的表示。从这一步得出的另一个含义是，我们可以随意复制信息位。你可能已经想象到，当涉及到量子计算时，这是一个很大的限制；我们稍后将进一步讨论这一点。

一旦我们编码了信息，我们就可以继续处理我们需要处理的事情。将它发送给世界另一端的某人，用我们的数据作为输入运行一个非常复杂的算法等等。重要的是，在某一点上，我们将需要解码数据。这样做非常简单，我们遍历每个 3 位长的比特串，并执行与编码相反的映射。然而，在编码和解码过程中可能会出现一些错误，并且一些比特串可能已经发生了一些位翻转。由于错误而导致的可能的比特串是什么？好吧，简单来说，任何不在 ![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq398.png) 中的东西，其中 ![$$\mathcal {E} = \{001, 010, 011, 100, 101, 110\}$$](img/516210_1_En_1_Chapter_TeX_IEq399.png) 是集合 ![$$\mathcal {E}$$](img/516210_1_En_1_Chapter_TeX_IEq400.png)。如果我们读到一个比特串在 ![$$\mathcal {E}$$](img/516210_1_En_1_Chapter_TeX_IEq401.png) 中，我们将知道发生了错误。由于我们也知道这些错误非常罕见，我们将假设最好的情况是只发生了一次位翻转。这导致我们将 ![$$\mathcal {E}$$](img/516210_1_En_1_Chapter_TeX_IEq401.png) 中的比特串解码为 ![$$\{ 0, 1\}$$](img/516210_1_En_1_Chapter_TeX_IEq402.png)，取决于字符串中出现最多的哪个（两次）。

我们刚刚描述的正确解码依赖于有关位翻转错误低频率的假设。这并不保证这种方法总是有效。具体来说，有两种情况（你可能已经想到了）会导致位翻转错误使我们解码错误的原始位：（1）两个位翻转导致我们假设错误的原始位和（2）三个位翻转使错误不被注意。情况（1）非常罕见，但可能发生，并且会导致我们对数据的错误解释。情况（2）甚至更糟，尽管也更罕见，因为它不仅会导致我们解码错误，而且还不会留下任何错误的证据，因为它是从![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq403.png)到自身的映射。

如你所见，重复码并不完美。有些情况下会有错误通过它。因此，我们需要一种表达纠错码特性的方式，这样我们就能比较不同的码，并决定在每种情况下哪一个是最佳的。为此，让我们首先定义码的距离概念。我们定义一个码的距离（表示为*d*）为将集合![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq404.png)的一个元素映射到另一个元素所需的错误数量。换句话说，使任何错误的证据消失所需的错误数量。正如我们在上一段讨论的那样，在我们的情况下![$$d=3$$](img/516210_1_En_1_Chapter_TeX_IEq405.png)。更数学化且在一般情况下，我们将距离定义为![$$\begin{aligned} d = 2t+1, \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ67.png)(67)其中*t*是方案可以纠正的错误数量。在我们的情况下，![$$t=1$$](img/516210_1_En_1_Chapter_TeX_IEq406.png)，因为我们只能纠正位翻转。

使用距离的概念，我们可以引入[*n*, *k*, *d*]符号。最后一个数字是我们刚刚引入的距离，*n*是码字的长度（集合![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq407.png)的元素），*k*是每个码字中编码的信息位数（在编码步骤之前的原始位串的长度）。使用这个符号，我们刚刚描述的 3 位经典重复码是一个[3, 1, 3]码。

### 3.4 从经典到量子

对于经典纠错码的工作原理有一个很好的理解之后，我们可以将注意力转回到量子计算上。假设我们想要使用刚刚描述的[3, 1, 3]码来纠正量子计算中的*X*错误。一个问题立即出现，上一节简要提到过：我们如何执行原始量子位的映射到码字的集合？我们想要进行的映射如下所示：![$$\begin{aligned} |\psi \rangle \xrightarrow []{encoding} |\psi \rangle \otimes |\psi \rangle \otimes |\psi \rangle \end{aligned}$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_Equ68.png)。对于无叠加的情况，编码可以简化为![$$\{|0\rangle , |1\rangle \}\xrightarrow []{}\{|000\rangle , |111\rangle \}$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq408.png)。这非常容易执行：我们只需使用两个*CNOT*门。因此，对于状态![$$|a\rangle \in \{|0\rangle , |1\rangle \}$$](img/516210_1_En_1_Chapter_TeX_IEq409.png)，编码如下所示：![](img/516210_1_En_1_Fig31_HTML.png)

图 31

假设在状态![$$|a\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq410.png)中没有叠加的情况下对三量子位进行编码

然而，当我们想要编码任意单比特态时，会出现问题！$$|\psi \rangle = \alpha |0\rangle + \beta |1\rangle $$。由于无克隆定理，我们知道没有幺正操作能够创建与态 ![$$|\psi \rangle $$](img/516210_1_En_1_Chapter_TeX_IEq412.png) 相同的完全副本 [65]。将态 ![$$|\psi \rangle $$](img/516210_1_En_1_Chapter_TeX_IEq413.png) 送入图 31 中的电路会输出态 ![$$\alpha |000\rangle + \beta |111\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq414.png)。尽管这可能看起来是等式 (68) 中映射的正确输出，但这并不是我们想要的。正确的映射应该输出态![$$\begin{aligned} |\psi \rangle \otimes |\psi \rangle \otimes |\psi \rangle&amp;= (\alpha |0\rangle + \beta |1\rangle ) \otimes (\alpha |0\rangle + \beta |1\rangle ) \otimes (\alpha |0\rangle + \beta |1\rangle ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ69.png)(69)![$$\begin{aligned}&amp;= (\alpha ²|00\rangle + \alpha \beta |01\rangle + \beta \alpha |10\rangle + \beta ²|11\rangle ) \otimes (\alpha |0\rangle + \beta |1\rangle ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ70.png)(70)![$$\begin{aligned}&amp;= \alpha ³|000\rangle + \alpha ²\beta (|010\rangle + |100\rangle + |001\rangle ) + \beta ²\alpha (|110\rangle + |011\rangle + |101\rangle ) + \beta ³|111\rangle \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ71.png)(71)显然，这与我们在图 31 中得到的结果相去甚远。并且，我们由无克隆定理保证，没有电路可以让我们对任意状态执行正确的编码。因此，我们可以立即排除我们在第 3.3 节中描述的重复码在量子情况下的使用可能性。

### 3.5 检测比特翻转错误

尽管我们无法像经典重复代码那样添加冗余（![$$|\psi \rangle \xrightarrow []{} |\psi \psi \psi \rangle $$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq415.png)）, 但我们可以使用*CNOT*门来添加一种不同类型的冗余，这种冗余我们在方程（71）中已经见过。 *CNOT*门引入的冗余不同之处在于它使量子位纠缠在一起。更具体地，带有![$$|\psi \rangle $$](img/516210_1_En_1_Chapter_TeX_IEq416.png)作为控制位，![$$|0\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq417.png)作为目标位的*CNOT*门执行以下转换：![$$\begin{aligned} |\psi \rangle |0\rangle = (\alpha |0\rangle + \beta |1\rangle ) |0\rangle = \alpha |00\rangle + \beta |10\rangle \xrightarrow []{CNOT} \alpha |00\rangle + \beta |11\rangle \end{aligned}$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_Equ72.png)(72)显然，这个方程并不等于![$$|\psi \rangle $$](img/516210_1_En_1_Chapter_TeX_IEq418.png)与自身的张量积，但它仍然是一种添加有用冗余的方法。这个编码器的扩展遵循了图 31 中的*CNOT*模式，可以扩展到任意数量*n*的冗余量子位。现在，我们将只看一个冗余量子位。

就像我们对经典纠错码所做的那样，我们可以定义一组逻辑码字（称为码空间）![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq419.png)，其由![$$\{|0\rangle _L=|00\rangle , |1\rangle _L=|11\rangle \}$$](img/516210_1_En_1_Chapter_TeX_IEq420.png)所张成，其中下标 *L* 代表逻辑。由于我们现在考虑的是两个量子比特，它们所在的空间是一个由计算基态![$$\{|00\rangle , |01\rangle , |10\rangle , |11\rangle \}$$](img/516210_1_En_1_Chapter_TeX_IEq422.png)张成的四维希尔伯特空间![$$\mathcal {H}⁴$$](img/516210_1_En_1_Chapter_TeX_IEq421.png)。这意味着![$$\mathcal {C} \subset \mathcal {H}⁴$$](img/516210_1_En_1_Chapter_TeX_IEq423.png)，这留下了另一个子空间![$$\mathcal {F}$$](img/516210_1_En_1_Chapter_TeX_IEq424.png)，我们将其称为错误子空间，其由![$$\{|01\rangle , |10\rangle \}$$](img/516210_1_En_1_Chapter_TeX_IEq425.png)所张成。因此，我们可以看到![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq426.png)和![$$\mathcal {F}$$](img/516210_1_En_1_Chapter_TeX_IEq427.png)是正交的，这使我们能够在不破坏编码信息的情况下区分它们。这是通过以下电路实现的：

让我们逐步了解电路。请注意，前两个量子比特已经从逻辑上起始于![$$|\psi \rangle _L = \alpha |00\rangle + \beta |11\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq428.png)，这是事先准备好的。在第一步中，有一个作用于两个代码比特的酉变换*E*。这些酉变换可以对应于以下操作之一:![$$X_1$$](img/516210_1_En_1_Chapter_TeX_IEq429.png)，![$$X_2$$](img/516210_1_En_1_Chapter_TeX_IEq430.png)，![$$X_2X_1$$](img/516210_1_En_1_Chapter_TeX_IEq431.png)，或*I*。这意味着在第一个量子比特上发生了一个比特翻转，第二个量子比特上发生了一个比特翻转，两者都发生了，或者根本没有错误。正如你所看到的，我们现在只关心比特翻转错误。

第 2 步可能一开始有点难以理解。但是让我们看看将运算符应用于 ![$$|\psi \rangle _L$$](img/516210_1_En_1_Chapter_TeX_IEq433.png) 的效果是什么。![$$\begin{aligned} Z_1Z_2(\alpha |00\rangle + \beta |11\rangle ) = Z_1(\alpha |00\rangle - \beta |11\rangle ) = \alpha |00\rangle + \beta |11\rangle = (+1)|\psi \rangle _L \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ73.png)(73)这意味着 ![$$|\psi \rangle _L$$](img/516210_1_En_1_Chapter_TeX_IEq434.png) 是 ![$$Z_1Z_2$$](img/516210_1_En_1_Chapter_TeX_IEq435.png) 的特征向量，其特征值为 ![$$+1$$](img/516210_1_En_1_Chapter_TeX_IEq436.png)。当将该运算符应用于两量子比特逻辑状态时，该状态保持不变，因此称 ![$$Z_1Z_2$$](img/516210_1_En_1_Chapter_TeX_IEq437.png) 为稳定化运算符。当将相同运算符应用于具有单比特翻转的状态时，即不在 ![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq438.png) 中时会发生什么？让我们考虑状态 ![$$X_1|\psi \rangle _L = \alpha |01\rangle + \beta |10\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq439.png)。![$$\begin{aligned} Z_1Z_2(\alpha |01\rangle + \beta |10\rangle ) = Z_1( - \alpha |01\rangle + \beta |10\rangle ) = -\alpha |01\rangle - \beta |10\rangle = (-1)X_1|\psi \rangle _L \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ74.png)(74)正如您所看到的，![$$X_1|\psi \rangle _L$$](img/516210_1_En_1_Chapter_TeX_IEq440.png) 是 ![$$Z_1Z_2$$](img/516210_1_En_1_Chapter_TeX_IEq441.png) 的特征向量，其特征值为 ![$$-1$$](img/516210_1_En_1_Chapter_TeX_IEq442.png)。您可以轻松验证对于 ![$$X_2$$](img/516210_1_En_1_Chapter_TeX_IEq443.png) 也是如此。但是，正如在经典编码情况下一样，当 ![$$E=X_1X_2$$](img/516210_1_En_1_Chapter_TeX_IEq444.png) 时，我们面临一个问题。该运算符将原始逻辑状态转换为仍在码空间 ![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq445.png) 中的另一状态，因此对于 ![$$Z_1Z_2$$](img/516210_1_En_1_Chapter_TeX_IEq447.png) 其具有特征值 ![$$+1$$](img/516210_1_En_1_Chapter_TeX_IEq446.png)。总结一下，在 ![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq448.png) 中的状态具有特征值 ![$$+1$$](img/516210_1_En_1_Chapter_TeX_IEq449.png)，而在 ![$$\mathcal {F}$$](img/516210_1_En_1_Chapter_TeX_IEq450.png) 中的状态具有特征值 ![$$-1$$](img/516210_1_En_1_Chapter_TeX_IEq451.png)。我们如何提取这些信息？

这正是第二步的作用。第三个量子比特被用作辅助量子比特来测量应用![$$Z_1Z_2$$](img/516210_1_En_1_Chapter_TeX_IEq452.png)稳定器的结果。首先将辅助量子比特设置为![$$H|0\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle )$$](img/516210_1_En_1_Chapter_TeX_IEq453.png)，之后应用一个受控![$$Z_1Z_2$$](img/516210_1_En_1_Chapter_TeX_IEq454.png)门。由于我们知道前两个量子比特的状态是![$$Z_1Z_2$$](img/516210_1_En_1_Chapter_TeX_IEq455.png)的本征态，因此对这些量子比特的唯一影响将是本征值的加成，此门的显著效果将通过相位回馈作用在辅助量子比特上。如果本征值为![$$-1$$](img/516210_1_En_1_Chapter_TeX_IEq456.png)，辅助量子比特将变为![$$\frac{1}{\sqrt{2}}(|0\rangle - |1\rangle )$$](img/516210_1_En_1_Chapter_TeX_IEq457.png)。如果为![$$+1$$](img/516210_1_En_1_Chapter_TeX_IEq458.png)，辅助量子比特将保持不变。

第二个哈达玛门作用在辅助量子比特上，如果逻辑状态处于 ![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq460.png)，则将其变为 ![$$|0\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq459.png)，如果逻辑状态处于 ![$$\mathcal {F}$$](img/516210_1_En_1_Chapter_TeX_IEq462.png)，则变为 ![$$|1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq461.png)。这是最终测量到的结果。这个过程称为综合提取，正如你所看到的，它告诉我们逻辑量子比特是否存在错误。然而，它无法区分 ![$$X_1$$](img/516210_1_En_1_Chapter_TeX_IEq463.png) 和 ![$$X_2$$](img/516210_1_En_1_Chapter_TeX_IEq464.png)，并且将 ![$$X_1X_2$$](img/516210_1_En_1_Chapter_TeX_IEq465.png) 视为无错误（该代码在位翻转错误方面具有距离 2）。因此，此代码仅检测错误，但无法对其进行纠正。

### 3.6 修正位翻转错误

纠正需要更多的努力。首先，我们将添加另一个冗余量子比特。因此，编码器将变成图 31 所示的电路，正如我们已经看到的，该电路执行编码 ![$$(\alpha |0\rangle + \beta |1\rangle )|00\rangle \xrightarrow []{} \alpha |000\rangle + \beta |111\rangle $$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq466.png)。与两比特代码不同，我们现在正在使用一个八维希尔伯特空间。我们可以将此空间划分为四个子空间，每个子空间由两个基态张成。我们要定义的第一个是码空间，即 ![$$\mathcal {C} = \text {span}\{|000\rangle , |111\rangle \}$$](img/516210_1_En_1_Chapter_TeX_IEq467.png)。现在，我们定义另外三个子空间，它们对应于可能的错误。![](img/516210_1_En_1_Fig32_HTML.png)

第 32 图

两比特翻转检测电路

我们将考虑错误门为 ![$$E=\{X_1, X_2, X_3\}$$](img/516210_1_En_1_Chapter_TeX_IEq468.png)，每种可能性都会产生一个错误子空间。 对于 ![$$X_1$$](img/516210_1_En_1_Chapter_TeX_IEq469.png)，我们有 ![$$\mathcal {F}_1=\text {span}\{|100\rangle , |011\rangle \}$$](img/516210_1_En_1_Chapter_TeX_IEq470.png)，对于 ![$$X_2$$](img/516210_1_En_1_Chapter_TeX_IEq471.png)，我们有 ![$$\mathcal {F}_2=\text {span}\{|010\rangle , |101\rangle \}$$](img/516210_1_En_1_Chapter_TeX_IEq472.png)，对于 ![$$X_3$$](img/516210_1_En_1_Chapter_TeX_IEq473.png)，我们有 ![$$\mathcal {F}_3=\text {span}\{|001\rangle , |110\rangle \}$$](img/516210_1_En_1_Chapter_TeX_IEq474.png)。 这给我们提供了一般方程 ![$$E_i|\psi \rangle _L \in \mathcal {F}_i$$](img/516210_1_En_1_Chapter_TeX_IEq475.png)。 有了这个想法，我们可以制定出三比特纠错码的电路。![](img/516210_1_En_1_Fig33_HTML.png)

图 33

三比特错误检测码

正如你所见，图 33 中的电路与图 32 中的双量子位版本非常相似。第一步应用门 *E*，其中可能包含一个错误。之后，在第 2 步中，执行两个综合测量。为了查看综合测量的结果，让我们分析一下它们的工作原理。正如我们在前一节中所看到的，如果存在单量子位错误，则辅助量子位的测量结果为 ![$$|1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq476.png)，否则为 ![$$|0\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq477.png)。将这种想法普遍化，对于双量子位综合测量，输出将在量子位不同比特时为 ![$$|1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq478.png)，否则为 ![$$|0\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq479.png)。因此，设 ![$$|\psi \rangle _L$$](img/516210_1_En_1_Chapter_TeX_IEq480.png) 为 ![$$\alpha |abc\rangle + \beta |\bar{a} \bar{b} \bar{c}\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq481.png)。第一综合测量结果为 ![$$|0\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq482.png)，如果 ![$$a=b$$](img/516210_1_En_1_Chapter_TeX_IEq483.png)，而为 ![$$|1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq484.png)，如果 ![$$a \not =b$$](img/516210_1_En_1_Chapter_TeX_IEq485.png)。同样，第二综合测量结果为 ![$$|0\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq486.png)，如果 ![$$b=c$$](img/516210_1_En_1_Chapter_TeX_IEq487.png)，而为 ![$$|1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq488.png)，如果 ![$$b \not = c$$](img/516210_1_En_1_Chapter_TeX_IEq489.png)。

使用上述最后一条陈述，我们可以计算以下错误门的综合测量：![$$\begin{aligned} E = I_1I_2I_3: 00 \qquad E = I_1I_2X_3: 01&amp;\qquad E = X_1I_2I_3: 10 \qquad E = I_1X_2I_3: 11 \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ75.png)(75)![$$\begin{aligned} E = X_1X_2X_3: 00 \qquad E = X_1X_2I_3: 01&amp;\qquad E = I_1X_2X_3: 10 \qquad E = X_1I_2X_3: 11 \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ76.png)(76)你可以看到这些测量值与我们之前定义的三个错误子空间![$$\mathcal {F}_i$$](img/516210_1_En_1_Chapter_TeX_IEq490.png)之间的直接关系。在![$$\mathcal {F}_1$$](img/516210_1_En_1_Chapter_TeX_IEq491.png)中的状态导致测量值为 10，![$$\mathcal {F}_2$$](img/516210_1_En_1_Chapter_TeX_IEq492.png)的测量值为 11，而![$$\mathcal {F}_3$$](img/516210_1_En_1_Chapter_TeX_IEq493.png)的测量值为 01。在辅助量子比特测量之后，我们只需应用与检测到的错误对应的![$$X_i$$](img/516210_1_En_1_Chapter_TeX_IEq494.png)算子即可纠正。

因此，此代码使我们能够确定发生了哪个错误，并带有将相同综合症分配给两个不同错误的警告。这种情况类似于经典纠错代码中的情况。例如，假设错误是 ![$$X_1X_2I_3$$](img/516210_1_En_1_Chapter_TeX_IEq496.png)。综合症测量将告诉我们状态处于 ![$$\mathcal {F}_3$$](img/516210_1_En_1_Chapter_TeX_IEq497.png)，因此我们将应用 ![$$X_3$$](img/516210_1_En_1_Chapter_TeX_IEq498.png) 进行纠正。但这是错误的，因为真正的错误是前两个量子比特中的两个*X*门。然而，我们暂且只能接受这一点。

此外，两个比特翻转到相同的逻辑状态要比单个比特翻转要少得多，所以，我们大多数时候会准确地纠正错误。而且，错误检测代码不仅在计算过程中仅应用一次，而是多次，以便在错误变得太大和难以检测之前检测和纠正错误。因此，根据我们正在使用的硬件，我们可以足够频繁地应用代码，使得两个比特翻转在单个逻辑状态中出现变得困难。

尽管这段代码能够高精度地检测和纠正比特翻转错误，但并不完美。为了看清楚这一点，让我们看一下它的代码距离。就像经典的三比特重复码一样，它需要三次比特翻转才能将状态从 ![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq499.png) 中的一个状态转移到同一子空间中的另一个状态。基于此，我们会说上面概述的代码具有 3 的量子距离。然而，这假设了只有*X*错误是可能的。但是，正如我们在 3.2 节中讨论过的，还存在相位错误，其特征由*Z*操作符描述。通过将*Z*应用于状态 ![$$|\psi \rangle _L = \alpha |0\rangle _L + \beta |1\rangle _L$$](img/516210_1_En_1_Chapter_TeX_IEq500.png) 中的单比特，并将其发送通过图 33 中的电路，您可以看到该代码无法检测到此错误。

您还可以通过观察到 ![$$\alpha |0\rangle _L + \beta |1\rangle _L$$](img/516210_1_En_1_Chapter_TeX_IEq501.png) 和 ![$$\alpha |0\rangle _L - \beta |1\rangle _L$$](img/516210_1_En_1_Chapter_TeX_IEq502.png) 都在 ![$$\mathcal {C}$$](img/516210_1_En_1_Chapter_TeX_IEq503.png) 中来注意到这一点。因此，三比特码无法检测单比特*Z*错误。这导致我们说本节描述的代码的量子距离为 1，因为只需一个错误就可以将代码空间中的状态转移到同一空间中的另一个状态。因此，我们仍然需要找出如何纠正相位错误。

### 3.7 用于相位错误的三比特码

从纠正比特翻转到纠正相位错误并不是一个非常困难的任务。我们只需拿出前一节设计的代码，做出一些修改即可。我们现在只关注代码的数学方面，而不是实际的电路实现，但请放心，它与比特翻转校正一样简单。首先，编码器。我们将定义码空间为 ![$$\mathcal {C} = \text {span}\{|0\rangle _L=|+++\rangle , |1\rangle _L = |---\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq504.png)。因此，对于单比特的一般状态 ![$$|\psi \rangle = \alpha |0\rangle + \beta |1\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq505.png)，这种编码会给出状态 ![$$|\psi \rangle _L = \alpha |+++\rangle + \beta |---\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq506.png)。有了这个想法，我们可以继续定义稳定器测量。

由于我们使用了 ![$$Z_1Z_2$$](img/516210_1_En_1_Chapter_TeX_IEq507.png) 和 ![$$Z_2Z_3$$](img/516210_1_En_1_Chapter_TeX_IEq508.png) 来纠正比特翻转错误，直觉告诉我们必须使用 ![$$X_1X_2$$](img/516210_1_En_1_Chapter_TeX_IEq509.png) 和 ![$$X_2X_3$$](img/516210_1_En_1_Chapter_TeX_IEq510.png) 来纠正相位错误。要看到这两个算符稳定了逻辑态 ![$$|\psi \rangle _L$$](img/516210_1_En_1_Chapter_TeX_IEq511.png)，你可以首先展开 ![$$|+++\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq512.png) 如下所示：![$$\begin{aligned} \frac{1}{\sqrt{8}}(|000\rangle + |001\rangle + |010\rangle + |011\rangle + |100\rangle + |101\rangle + |110\rangle + |111\rangle ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ77.png)(77)同样，对于 ![$$|---\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq513.png) 也是一样的：![$$\begin{aligned} \frac{1}{\sqrt{8}}(|000\rangle - |001\rangle - |010\rangle + |011\rangle - |100\rangle + |101\rangle + |110\rangle - |111\rangle ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ78.png)(78)将这两个方程式放在一起，你会得到逻辑量子位 ![$$|\psi \rangle _L$$](img/516210_1_En_1_Chapter_TeX_IEq514.png) 的一般状态，你可能已经猜到，这个写法有点冗长。尽管如此，你可以这样做，并应用两个稳定器门来验证它们在没有错误时以 ![$$+1$$](img/516210_1_En_1_Chapter_TeX_IEq515.png) 的特征值时保持状态不变，而在存在相位错误时以 ![$$-1$$](img/516210_1_En_1_Chapter_TeX_IEq516.png)。为了完整起见，我们将在哈达玛基础上展示这一点。要理解推导过程，请记住 ![$$Z|+\rangle = |-\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq517.png) 以及反之，以及 ![$$X|+\rangle = |+\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq518.png) 以及 ![$$X|-\rangle = (-1)|-\rangle $$](img/516210_1_En_1_Chapter_TeX_IEq519.png)。因此，对于没有引入错误的逻辑态，我们得到以下方程式：![$$\begin{aligned} X_1X_2(\alpha |+++\rangle

### 3.8 通用纠错码

我们已经了解了如何单独纠正位翻转和相位错误，但我们仍需要将这两个电路组合在一起来纠正任何给定的错误（布洛赫球上的旋转）。这超出了本节的范围，但并不太难。这种纠正码的一个例子是 Shor 的[[9，1，3]]（双括号通常用于区分使用单括号的经典编码）编码[66]。该编码使用我们在最后两节中定义的编码来创建一个具有距离为 3 的单个 9 比特错误纠正编码。为此，它将其编码空间定义为以下两个逻辑状态的张成！$$\begin{aligned} |0\rangle _L&amp;= \frac{1}{\sqrt{8}}(|000\rangle + |111\rangle )(|000\rangle + |111\rangle )(|000\rangle + |111\rangle ) \end{aligned}$$(83)![$$\begin{aligned} |1\rangle _L&amp;= \frac{1}{\sqrt{8}}(|000\rangle - |111\rangle )(|000\rangle - |111\rangle )(|000\rangle - |111\rangle ) \end{aligned}$$](img/516210_1_En_1_Chapter_TeX_Equ84.png)(84)然后，稳定器被定义为![$$Z_1Z_2, Z_2Z_3, \dots , Z_8Z_9$$](img/516210_1_En_1_Chapter_TeX_IEq523.png)和![$$X_1X_2, X_2X_3, \dots , X_8X_9$$](img/516210_1_En_1_Chapter_TeX_IEq524.png)。这为我们每个单比特*X*错误提供了一个独特的综合测量，从而使我们可以轻松纠正它们。对于每个单比特*Z*错误，我们不会得到一个唯一的综合测量，但这不是问题，因为我们得到相同测量的错误可以使用相同的算子进行纠正。这就是 Shor 编码具有理想距离为 3 的原因。

为什么这个距离是理想的？具有距离$$d\ge 3$$的码允许检测和准确纠正错误，而具有$$d&lt;3$$的码只允许错误检测（它们不指定错误是在哪个量子比特引入的）。Shor 的码并不是唯一一个能够纠正任何错误的纠错码的实现。关于![$$[[n, k, d\ge 3]$$](../images/516210_1_En_1_Chapter/516210_1_En_1_Chapter_TeX_IEq527.png)码的严格描述和构造可以在第 4.1–4.2 节和第 4.4–4.5 节中找到[58]。此外，量子纠错是一个非常活跃的研究领域，正在积极追求设计纠错码的不同方法。一个例子是表面码，你可以在[67]和[68]中了解更多关于它的信息。

## 4 结论和关于区块链的注释

在本章中，我们介绍了量子信息、纠缠、量子门、超密编码、量子隐形传态、纠缠交换、基于纠缠的量子密钥分发和量子秘密共享的概念。在量子区块链中，当需要防止双重支付时，隐形传态是至关重要的。也就是说，一旦量子状态被发送，一个人就不能保留已经花费的硬币。事实上，区块链可以被转化为量子电路形式，因此读者被介绍了简单的量子比特门以及如何从它们构建通用量子电路。例如，可以构建拜占庭协议的量子类比，取代其经典对应物。

任何量子通信或交易都将通过网络进行。量子系统对环境噪声非常脆弱。我们介绍了量子噪声的概念，这导致系统与噪声相互作用时出现马尔可夫或非马尔可夫演化。在量子网络中，包括区块链技术可以利用非马尔可夫动态中的信息反馈。有趣的是，噪声并不总是坏事。在实验室中充分控制下，合法方可以向系统添加额外的量子噪声，以在安全性上获得反直觉的优势来对抗黑客攻击。

多重受控 Toffoli 门是一类多功能的门，在密码学和区块链的许多应用中得到了应用。未来，很可能量子计算机将通过 Shor 算法来破解使用椭圆曲线签名方案计算离散对数[69]。此外，量子计算机在进行区块链工作量证明（PoW）时使用 Grover 算法可以提供二次加速[70]。然而，目前用于 PoW 的硬件的优化时钟速度，以及目前量子架构的门速度要慢得多，基本上抵消了上述所有的优势。在这两个示例中，Toffoli 门（以预言的形式）占用了大部分资源[71]。因此，人们确实希望尽可能地优化这些昂贵的组件，使量子计算机能够提供任何有形的优势。

对于遥远的未来，许多提出的量子区块链协议[72, 73]都建立在容错计算的中心假设之上。因此，基于可逆计算的性质，多个受控操作无疑将在任何实施在此类设备上的错误校正方案中起着至关重要的作用。

实用量子区块链将需要大量的量子比特和门才能发挥作用。为了使其在经典对应物上具有优势，量子区块链需要既快速又准确。量子纠错是提高后者因素的关键部分。需要具有小码字长度和足够大的码距的编码，以准确检测和纠正量子区块链中使用的电路中的错误。这必须同时考虑效率，因为我们不希望纠错码的电路复杂度变得与原始电路一样大甚至更大。如果满足这些标准，那么量子区块链（以及量子信息的所有其他应用）将受益匪浅，我们可能会看到它们在现实世界的使用上迅速取得进展。

基于经典信息原则的当前区块链技术正面临量子计算的崛起带来的威胁。正在努力开发（经典）后量子加密安全协议，以便在受到量子计算机攻击时保持安全。然而，开发抵御量子攻击的量子区块链技术是一个好主意。量子密码学已经得到了很大发展，并已经在学术界和工业界初步应用。类似地，量子区块链将成为一种新的基于量子力学原理的去中心化、加密的账本技术。可能会成为一种未来技术，整合经典和量子原则和技术，以开发更安全的区块链技术。

致谢

US 感谢 R. Srikanth 审阅草稿，Vinod N. Rao 就量子秘密共享进行了有益的讨论。US 还感谢 C. M. Chandrashekar 的鼓励。

作者贡献

美国贡献了第一部分有关量子信息的部分。MP 贡献了第二部分关于多重受控托菲利门的部分，EP 贡献了第三部分关于量子纠错的部分。
