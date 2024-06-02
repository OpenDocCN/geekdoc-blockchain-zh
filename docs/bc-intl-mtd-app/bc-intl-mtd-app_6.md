© 作者（们），在独家授权下 Springer Nature 新加坡私人有限公司 2021Z. 郑等人（编辑）区块链智能[`doi.org/10.1007/978-981-16-0127-9_6`](https://doi.org/10.1007/978-981-16-0127-9_6)

# 6. 基于区块链的加密货币市场分析

卿汉^(1, 2  ), 贾静^(1, 2  ), 韦丽^(1, 2  ), 许岳金^(1, 2  ) 和 郑子宾^(2, 3  )(1)中山大学数据科学与计算机学院, 广州, 中国(2)中山大学国家数字生活工程研究中心, 广州, 中国(3)中山大学, 广州, 中国卿汉 Email: hanq25@mail2.sysu.edu.cn 贾静（通讯作者）Email: wujiajing@mail.sysu.edu.cn 韦丽 Email: chenwli28@mail.sysu.edu.cn 许岳金 Email: xuyj25@mail2.sysu.edu.cn 郑子宾 Email: zhzibin@mail.sysu.edu.cn

## 摘要

在本章中，我们从两个角度呈现基于区块链的加密货币市场分析。一个角度是基于加密货币市场的特点我们可以考虑哪些特征，以及通过分析它们我们能发现什么。我们将通过分析以太坊市场上的一些有趣特征并将其与同一时期比特币进行比较来阐述这一点。另一个角度是关于检测加密货币市场的异常行为。我们将介绍如何使用改进的 Apriori 算法来检测加密货币市场上的“拉高出货”计划。

## 6.1 概述

随着加密货币的快速发展，加密货币市场涌现出来并吸引了众多投资者。由于加密货币的急剧流行和作为一种新货币的独特性，加密货币市场分析引起了大量研究兴趣。加密货币市场分析可以分为两部分。首先，许多投资者希望全面了解某个加密货币市场，以便我们能从中获利。因此，许多研究人员致力于分析和揭示特定加密货币市场的特征。其次，由于监管不足，加密货币市场上各种诈骗行为泛滥。因此，也有大量研究旨在检测市场上的异常计划。从上述情况来看，本章分为两部分。第一部分是关于加密货币市场的特征分析，第二部分是检测加密货币市场上的异常计划。

## 6.2 加密货币市场特征分析

在本节中，我们将使用我们的一篇作品，分析以太坊市场的长距离依赖、多分形和交易量与回报的因果关系，来说明加密货币市场的特征分析。这项工作可以作为一个很好的例子，展示挖掘特征的重要性以及通过分析它们我们能发现什么。

这项工作致力于填补以太坊市场分析的研究空白，目的是提供有价值的以太坊投资见解。特别是，我们首先使用去趋势波动分析和非对称多分形去趋势波动分析来研究长距离依赖、多分形及其不对称性。然后，我们利用非参数分位数因果性检验研究回报与以太坊交易量之间的因果关系，以找出投资者的活动如何影响回报。此外，通过与比特币市场的比较，我们进一步揭示了以太坊市场的独特属性。

### 6.2.1 引言

最近，比特币市场分析已成为一个热门的研究课题，许多研究已经揭示了比特币市场的各种特征，包括风格化事实（Bariviera 等人 2017）、非线性统计（混沌、多分形）(Lahmiri 和 Bekiros2018)、交易量与回报的关系（Balcilar 等人 2017）、市场操纵（Chen 等人 2019）等 Kondor 等人(2014), Drożdż等人(2018)。

然而，对于以太坊市场的分析，尽管最近以太坊的普及程度迅速提高，但相关研究却很少。因此，本章试图通过分析以太坊市场的几个重要的统计和非线性特征来填补这一研究空白。通过研究以太坊市场的价格、回报和交易量的性质，我们旨在揭示以太坊市场的潜在结构和动态，帮助投资者更好地理解以太坊市场。通过与比特币市场的比较，我们试图发现以太坊市场的独特之处。由于比特币的出现早于以太坊，我们也可以通过这种比较来评估以太坊市场的发展情况。

以前的研究表明，货币市场可以被建模为非线性系统，其各种影响因素都是非线性的。因此，我们假设以太坊市场符合分数市场假说，而不是经典的有效市场假说。为了证明这一点，我们首先评估以太坊回报率的长距离依赖特性以表征价格的可预测性。在这里，我们从多分数的角度探索以太坊回报率在不同时间尺度上的波动及其不对称性质。这种分析可以帮助投资者理解这种分数市场的无效率和波动性（Cajueiro 等人 2009; Wang 等人 2010）。因果关系是市场信息传播以及投资者活动如何影响回报的指标。对因果关系的分析是预测回报以及理解市场繁荣和崩溃的有效工具。与传统货币市场相比，加密货币市场通常具有相对较高价格波动，因此对于以太坊投资者来说，深入理解上述特性非常重要。因此，在本研究中，我们将重点分析上述特性，以揭示这个新市场的潜在动态和特性。据我们所知，这是对以太坊市场进行的第一个全面分析。

### 6.2.2 相关研究

在本章中，我们将重点从分数市场角度分析以太坊市场，并探索其成交量和回报之间的关系。

首先，之前的研究（Bariviera 等人 2017）已证明比特币市场与有效市场假说不一致，原因在于其具有长期记忆特性。因此，我们假设以太坊市场符合更广泛的分数市场假说，这表明以太坊价格之间存在内在的相关性。Hurst 指数*H*是衡量时间序列自相关性的广泛采用的度量标准。如果 Hurst 指数的值为*H*=0.5，那么时间序列可以被描述为随机游走，序列中的各项之间不存在相关性。如果 0.5<*H*<1，时间序列中存在长期记忆特性，序列中的一个高值后面很可能跟着另一个高值。相反，0<*H*<0.5 表明时间序列中存在反持续相关性。

在过去的几十年里，已经开发出许多计算 Hurst 指数的方法。经典的 R/S 方法（Mandelbrot 和 Taqqu1979）是最早的之一，但它不够健壮，可能会将短期记忆误认为是长距离记忆。后来，去趋势波动分析（DFA）（Peng 等人 1995）被提出，这个方法可以避免伪检测，并且更适合处理非平稳数据。因此，在本章中，我们选择 DFA 作为评估长距离依赖性的方法。

上述方法能够从单分形的角度分析市场的长距离依赖性，并假设在高波动或低波动下所有行为保持不变。这种假设对于许多现实市场的有效性是有问题的，因此传统的 DFA 被扩展为多分形 DFA (MF-DFA)（Kantelhardt 等人 2002）以估计不同尺度下的 Hurst 指数。此外，由于在缩放行为中存在非对称性，因此提出了非对称 DFA (A-DFA)（Alvarezramirez 等人 2009）来分析时间序列在缩放行为中的非对称相关性。这些方法最终被综合为非对称多分形去趋势波动分析（A-MFDFA）（Cao 等人 2013），不仅可以评估不同相关性中的多分形性，还可以探索具有上升和下降趋势的时间序列中的多分形性的非对称性。因此在我们的工作中，我们选择 A-MFDFA 来检测以太坊市场的相关性质。

关于成交量与回报的关系，我们致力于发现以太坊市场中每日成交量和每日回报之间的内在因果关系。作为一个分形市场，以太坊的成交量和回报之间的关系是非线性的，因此传统的线性 Granger 因果测试不能直接用来分析成交量的回报因果关系。最近，提出了一种更适合具有非线性关系的 time series 的非参数因果性-分位数测试（Balcilar 等人 2016）。在本章中，我们将使用这种方法来探讨投资者的活动（可以通过成交量反映）如何影响以太坊的回报和价格波动。

### 6.2.3 方法

#### 6.2.3.1 去趋势波动分析

作为一种计算非平稳数据 Hurst 指数的有效方法，去趋势波动分析（DFA）已经被现有工作（Bariviera 等人 2017）用来估计比特币收益的长距离相关性。为了研究以太坊市场的信息市场效率，在这里我们采用 DFA 方法来计算以太坊价格收益的 Hurst 指数。DFA 方法的详细描述可以在先前的研究中找到（Peng 等人 1995），在这里我们介绍了使用 DFA 方法研究以太坊价格收益的主要步骤。

对于价格时间序列*P* [*t*]，*t* = 1, …, *N*，我们首先计算相应的对数回报序列*R* [*t*] = *ln*(*P* [*t*]) − *ln*(*P* [*t*−1]), 其中*ln*(⋅)表示自然对数。然后，通过从*k*th 元素减去均值并相加得到整合的时间序列*y*(*k*)，*k* = 1, …, *N*，即![

$${y}(k)=\sum _{i=1}^{k}[R_{i}-\bar {R}]$$

](../images/506524_1_En_6_Chapter/506524_1_En_6_Chapter_TeX_IEq1.png)，其中![$$\bar {R}$$](img/506524_1_En_6_Chapter_TeX_IEq2.png)是*R* [*t*]的平均值。接下来，我们将*y*(*k*)分为*N* [*n*] = ⌊*N*∕*n*⌋个不重叠的部分，其中*n*是一个称为时间尺度的整数。由于*y*(*k*)不能被每个可能的*n*完全除尽，*y*(*k*)的末尾可能留下一小段时间周期。为此，我们从*y*(*k*)的末尾开始重复同样的过程，从而总共得到 2*N* [*n*]个部分。

对于每个部分，我们计算一个多项式拟合*y* *n*来确定该部分的局部趋势，然后得到波动函数，其表达式为![

$$\displaystyle \begin{aligned} F(n)=\sqrt{\frac{1}{N} \sum_{k=1}^{N}\left[{y}(k)-{y}_{n}(k)\right]^{2}}. \end{aligned} $$

](../images/506524_1_En_6_Chapter/506524_1_En_6_Chapter_TeX_Equ1.png)(6.1)

我们选择很多不同的*n*值来重复上述过程，已经被证明（Peng 等人 1994）*n*的最佳范围是![

$$[5, \frac {N}{4}]$$

](../images/506524_1_En_6_Chapter/506524_1_En_6_Chapter_TeX_IEq3.png)。波动函数*F*(*n*)以*n*的幂律函数的方式缩放，即*F*(*n*) ∼ *n* ^(*H*)，缩放指数*H*是 Hurst 指数的估计值。

此外，我们可以使用重叠滑动窗口（Cajueiro 和 Tabak 2004）每次向前移动一个数据点来观察 Hurst 指数如何随时间演变。

#### 6.2.3.2 A-MFDFA 方法

为了探索以太坊回报的多重分形及其不对称性，我们考虑了非对称多重分形去趋势波动分析（A-MFDFA）方法。

与 DFA 方法类似，我们从对数回报序列*R* [*t*]及其积分序列*y*(*t*)开始，然后分别将它们分成 2*N* [*n*]段。设！

$$S_{j}=\left \{s_{j, k}, k=1, \ldots , n\right \}$$

 是*R* [*t*]的第*j*段和！

$$Y_{j}=\left \{y_{j, k}, k=1, \ldots , n\right \}$$

 是*y* [*t*]的第*j*段。对于每个*S* [*j*]，我们计算最小二乘法直线拟合！

$$L_{{S}_{j}}(k)=b_{S_{j}} k+a_{S_{j}}$$

 并记录其斜率！

$$b_{S_{j}}$$

 以表示该段的局部趋势。而对于每个*Y* [*j*]，我们计算最小二乘法直线拟合！

$$L_{Y_{j}}(k)=b_{Y_{j}} k+a_{Y_{j}}$$

，然后记录！

$$L_{Y_{j}}$$

 作为去趋势*Y* [*j*]的估计值。然后我们得到每个段的波动函数，即！

$$\displaystyle \begin{aligned} F_{j}(n)=\frac{1}{n} \sum_{k=1}^{n}\left(y_{j, k}-L_{Y_{j}}(k)\right)^{2}. \end{aligned} $$

(6.2)

接下来，我们考虑当*R* [*t*]具有分段正负趋势时的平均波动函数。在这里，记录的斜率值符号！

$$b_{S_{j}}$$

 用作趋势指示器；即，如果！

$$b_{S_{j}} &gt; 0$$

 （分别为！

公式$$b_{S_{j}} &lt; 0$$

), 这一段的 *R* [*t*] 具有正向 (分别为负向) 趋势。

然后 *q* 阶平均波动函数为：![

公式$$\displaystyle \begin{aligned} F_{q}^{+}(n)=\left(\frac{1}{M^{+}} \sum_{j=1}^{2 N_{n}} \frac{1+\operatorname{sign}\left(b_{S_{j}}\right)}{2}\left[F_{j}(n)\right]^{q / 2}\right)^{1 / q}, \end{aligned} $$

](../images/506524_1_En_6_Chapter/506524_1_En_6_Chapter_TeX_Equ3.png)(6.3)![

公式$$\displaystyle \begin{aligned} F_{q}^{-}(n)=\left(\frac{1}{M^{-}} \sum_{j=1}^{2 N_{n}} \frac{1-\operatorname{sign}\left(b_{S_{j}}\right)}{2}\left[F_{j}(n)\right]^{q / 2}\right)^{1 / q}. \end{aligned} $$

](../images/506524_1_En_6_Chapter/506524_1_En_6_Chapter_TeX_Equ4.png)(6.4)其中 ![公式$$M^{+}=\sum _{j=1}^{2 N_{n}} \frac {1+\operatorname {sign}\left (b_{S_{j}}\right )}{2}$$](img/506524_1_En_6_Chapter_TeX_IEq13.png) 和 ![公式$$M^{-}=\sum _{j=1}^{2 N_{n}} \frac {1-\operatorname {sign}\left (b_{S_{j}}\right )}{2}$$](img/506524_1_En_6_Chapter_TeX_IEq14.png) 表示趋势为正和负的段落数量分别。假设 ![公式$$b_{S_{j}} \neq 0$$](img/506524_1_En_6_Chapter_TeX_IEq15.png) 对于每个 *j*, 我们有 *M* ^+ + *M* ^− = 2*N* [*n*]。与 DFA 方法类似，在这里我们通过观察 *F* *q* 对 *n* 的对数对数图来分析波动的缩放行为，即![公式$$\displaystyle \begin{aligned} F_{q}(n) \sim n^{H(q)} ; \quad  F_{q}^{+}(n) \sim n^{H^{+}(q)} ; \quad  F_{q}^{-}(n) \sim n^{H^{-}(q)}, \end{aligned} $$](img/506524_1_En_6_Chapter_TeX_Equ5.png)(6.5)其中 *H*(*q*)、*H* ^+(*q*) 和 *H* ^−(*q*) 分别表示整体、向上和向下的缩放指数。当 *q*=2 时，*H*(*q*) 是通过上述 DFA 方法计算得到的 Hurst 指数，整体缩放指数 *H*(*q*) 也被称为广义 Hurst 指数。

](../images/5

此外，对于 *q* > 0，*H*(*q*) 描述了大波动的缩放行为，对于 *q* < 0，它描述了小波动。如果 *H*(*q*) （分别为 *H* ^+(*q*) 或 *H* ^−(*q*)）显著地依赖于 *q*，我们可以认为时间序列的整体（分别为上升和下降趋势）相关性是多分形的，否则为单分形。

](../images/506524_1_En_6_Chapter/506524_1_En_6_Chapter_TeX_Equ7.png)(6.7)其中 ![$$\displaystyle \begin{aligned} \tau(q)=q H(q)-1\. \end{aligned} $$](img/506524_1_En_6_Chapter_TeX_Equ6.png)(6.6)在应用勒让德变换后，时间序列的多分形性可以通过奇异性谱 *f*(*α*):![$$\displaystyle \begin{aligned} f(\alpha)=q \alpha-\tau(q), \end{aligned} $$为了对标准化时间序列的多分形分析，我们可以考虑一个尺度指数，它表示为![$$\alpha =\dfrac {\mathrm {d} \tau }{\mathrm {d} q} = H(q)+q H^{\prime }(q)$$](img/506524_1_En_6_Chapter_TeX_IEq16.png) 是奇异性强度，*H* ^(*′*)(*q*) 表示 *H*(*q*) 对 *q* 的导数。我们常用 Δ*α* = *α* [*max*] − *α* [*min*] 来描述市场的多分形程度。(Kantelhardt 等人 2002).

#### 6.2.3.3 量子位数因果性测试

为了分析以太坊回报和交易量之间的关系，我们采用了由 Balcilar 等人 (2016) 提出的非参数量子位数因果性测试。

令 *y* [*t*] 表示以太坊的回报，*x* [*t*] 表示其交易量。就量子位数因果性而言，如果![$$\displaystyle \begin{aligned} Q_{\theta}\left(y_{t} | y_{t-1}, \ldots, y_{t-p}, x_{t-1}, \ldots, x_{t-p}\right)\!=\! Q_{\theta}\left(y_{t} | y_{t-1}, \ldots, y_{t-p}\right), \end{aligned} $$](img/506524_1_En_6_Chapter_TeX_Equ8.png)(6.8)其中 *p* 是滞后阶数，![$$Q_{\theta }\left ( y_{t} | \cdot \right )$$](img/506524_1_En_6_Chapter_TeX_IEq17.png) 表示依赖于 *t* 的 *y* [*t*] 的 *θ*th 分位数。令 *Y* [*t*−1] = (*y* [*t*−1], …, *y* [*t*−*p*]), *X* [*t*−1] = (*x* [*t*−1], …, *x* [*t*−*p*]), ![$$ Z_{t}=\left (X_{t}, Y_{t}\right )$$](img/506524_1_En_6_Chapter_TeX_IEq18.png), 和 ![$$F_{y_{t} | Z_{t-1}}\left (y_{t}, Z_{t-1}\right )$$](img/506524_1_En_6_Chapter_TeX_IEq19.png) 表示给定 *Z* [*t*−1] 下 *y* [*t*] 的条件分布函数。记![$$Q_{\theta }\left (Z_{t-1}\right ) \equiv Q_{\theta }\left (y_{t} | Z_{t-1}\right )$$](img/506524_1_En_6_Chapter_TeX_IEq20.png) 和![$$Q_{\theta }\left (Y_{t-1}\right ) \equiv Q_{\theta }\left (y_{t} | Y_{t-1}\right )$$](img/506524_1_En_6_Chapter_TeX_IEq21.png)，我们才有![$$ P\left \{F_{y_{t} | Z_{t-1}}\left \{Q_{\theta }\left (Y_{t-1}\right ) | Z_{t-1}\right \}=\theta \right \}=1 $$](img/506524_1_En_6_Chapter_TeX_IEq22.png)。因此，根据 (6.8) 的零假设和备择假设可以分别表示为![$$\displaystyle \begin{aligned} H_{0} : \quad  P\left\{F_{y_{t} | Z_{t-1}}\left\{Q_{\theta}\left(Y_{t-1}\right) | Z_{t-1}\right\}=\theta\right\}=1, \end{aligned} $$](img/506524_1_En_6_Chapter_TeX_Equ9.png)(6.9)并且![$$\displaystyle \begin{aligned} H_{1} : \quad  P\left\{F_{y_{t} | z_{t-1}}\left\{Q_{\theta}\left(Y_{t-1}\right) | Z_{t-1}\right\}=\theta\right\}&lt;1\. \end{aligned} $$](img/506524_1_En_6_Chapter_TeX_Equ10.png)(6.10)基于零假设的回归误差表示为 *ε* [*t*] (Balcilar 等 2016; Jeong 等 2012)，且 *H* [0] 只有在![$$1\left \{y_{t} \leq Q_{\theta }\left (Y_{t-1}\right )\right \}=\theta +\varepsilon _{t}$$](img/506524_1_En_6_Chapter_TeX_IEq23.png)，其中 1{⋅} 是一个指示函数。此外，距离度量 ![$$J=\left \{\varepsilon _{t} E\left (\varepsilon _{t} | Z_{t-1}\right ) f_{z}\left (Z_{t-1}\right )\right \}$$](img/506524_1_En_6_Chapter_TeX_IEq24.png)，其中 ![$$f_{z}\left (Z_{t-1}\right )$$](img/506524_1_En_6_Chapter_TeX_IEq25.png) 是 *Z* [*t*−1] 的边际密度函数。*J* 的可行核函数样本模拟形式由 Jeong 等人在 2012 中给出！

$$\displaystyle \begin{aligned} \hat{J}_{T}=\frac{1}{T(T-1) h^{2 p}} \sum_{t=p+1}^{T} \sum_{s=p+1, s \neq t}^{T} K\left(\frac{Z_{t-1}-Z_{s-1}}{h}\right) \hat{\varepsilon}_{t} \hat{\varepsilon}_{s}, \end{aligned} $$

(6.11)其中 *K*(⋅) 是带宽为 *h* 的核函数，*p* 是滞后阶数，*T* 是样本大小。在这里，估计的回归误差 ![$$\hat {\varepsilon }_{t}$$](img/506524_1_En_6_Chapter_TeX_IEq26.png) 可以这样给出![$$\displaystyle \begin{aligned} \hat{\varepsilon}_{t}=1\left\{y_{t} \leq \hat{Q}_{\theta}\left(Y_{t-1}\right)-\theta\right\}. \end{aligned} $$](img/506524_1_En_6_Chapter_TeX_Equ12.png)(6.12)![$$\hat {Q}_{\theta }\left (Y_{t-1}\right )$$](img/506524_1_En_6_Chapter_TeX_IEq27.png)是*θ*th 条件*y* [*t*]给定*Y* [*t*−1]的估计，![$$\hat {Q}_{\theta }\left (Y_{t-1}\right )$$](img/506524_1_En_6_Chapter_TeX_IEq28.png)可以使用非参数核方法估计为![$$\hat {Q}_{\theta }\left (Y_{t-1}\right )=\hat {F}_{y_{t} | Y_{t-1}}^{-1}\left (\theta | Y_{t-1}\right )$$](img/506524_1_En_6_Chapter_TeX_IEq29.png)，其中！

$$\hat {F}_{y_{t} | Y_{t-1}}\left (y_{t} | Y_{t-1}\right )$$

表示 Nadarya-Watson 核估计器，即![$$\displaystyle \begin{aligned} \hat{F}_{y_{t} | Y_{t-1}}\left(y_{t} | Y_{t-1}\right)=\frac{\sum_{s=p+1, s \neq t}^{T} L\left(\frac{Y_{t-1}-Y_{s-1}}{h}\right) 1\left(y_{s} \leq y_{t}\right)}{\sum_{s=p+1, s \neq t}^{T} L\left(\frac{Y_{t-1}-Y_{s-1}}{h}\right)}, \end{aligned} $$](img/506524_1_En_6_Chapter_TeX_Equ13.png)(6.13)其中*h*是带宽，*L*(⋅)表示核函数。

这样，我们可以估计每个分位数返回和成交量之间的因果关系。由于波动率通常计算为返回值的平方，我们可以进一步使用上述方法分析波动率与成交量之间的因果关系，将方程(6.9)和(6.10)中的*y* [*t*]替换为![公式$$y_{t}²$$](img/506524_1_En_6_Chapter_TeX_IEq31.png)（Balcilar 等人 2017）。

### 6.2.4 数据与实证发现

#### 6.2.4.1 数据

在本章中，我们将从分形市场的角度全面审视以太坊。此外，我们还考虑了比特币市场的数据进行比较。为此，我们选择了 2015 年 8 月至 2019 年 3 月以太坊和比特币的市场价格和数量数据。采样间隔为 4 小时，即每 4 小时收盘价和交易量作为原始数据。在这里，我们使用上述数据进行分形分析，使用 DFA 和 A-MFDFA。我们还获得了因果关系测试的每日收盘价和成交量信息。以太坊和比特币的原始市场数据来自 Poloniex（加密货币交易所 2019），是活跃的加密货币交易所之一。

由于价格序列的非平稳性，我们选择对数回报\( R \) [\( t \) ] = \( \ln \)(\( P \) [\( t \)]) - \( \ln \)(\( P \) [\( t \)−1])作为回报的度量，其中\( P \) [\( t \) ]是时间\( t \)的收盘价，\( \ln \)()表示自然对数。表 6.1 展示了以太坊和比特币每日对数回报的描述性统计。正如我们所看到的，以太坊回报的平均值高于比特币回报，但波动性更大。此外，根据它们的结果进行 Jarqie-Bera 检验（Jarque 和 Bera 1987），这两种加密货币的回报都不符合有效市场假说。以太坊和比特币回报的峰度值表明存在厚尾现象。表 6.1

以太坊和比特币每日对数回报的描述性统计

| ETH_Return | BTC_Return |
| --- | --- |
| 标准差 | 0.076976 | 0.041977 |
| 观测值 | 1315 | 1315 |
| 平均值 | 0.003503 | 0.002055 |
| 中位数 | 0.000003 | 0.002906 |
| --- | --- | --- |
| Jarque-Bera | 1467.93^a | 4550.07^a |
| 偏度 | 0.193640 | −0.659642 |
| 峰度 | 5.164818 | 8.998307 |
| ADF | −6.140743^a | −25.74626^a |

^a 表示在 1%的显著性水平下拒绝

为了应用第 6.2.3 节中描述的方法，我们需要保持回报和成交量系列平稳。至于回报，对数回报系列已经是平稳的，并通过了增广 Dickey-Fuller（ADF）测试。然而，当涉及到成交量时，一项先前的研究（Gallant 等人 1992）已经表明，成交量数据中存在线性和非线性的时间趋势。遵循先前工作（Gebka 和 Wohar 2013）中提出的去趋势方法，我们尝试通过取成交量的对数并减去回归值![\(\frac {t}{T}\)](img/506524_1_En_6_Chapter_TeX_IEq32.png)和![\((\frac {t}{T})^{2}\)](img/506524_1_En_6_Chapter_TeX_IEq33.png)，其中\( T \)是总大小。通过这样做，去趋势的成交量系列通过了 ADF 测试，这意味着它已经变得平稳。

### 6.2.5 结果

#### 6.2.5.1 长程依赖

为了验证以太坊市场是否符合分形市场假设，我们使用 DFA 方法计算了市场 3 个月滑动时间窗口的 Hurst 指数。图 6.1 显示了日期和回报对数价格的变化以及 Hurst 指数。![../images/506524_1_En_6_Chapter/506524_1_En_6_Fig1_HTML.png](img/506524_1_En_6_Fig1_HTML.png)

图 6.1

Hurst 指数和两种 ETH 与 BTC 的对数价格，使用 3 个月滑动窗口和 4 小时采样时间间隔。（**a**）ETH 价格和 Hurst 指数。（**b**）BTC 价格和 Hurst 指数

当我们考虑从 2015 年 8 月至 2019 年 3 月的整个时间段，而不是使用滑动窗口，以太坊回报的 Hurst 指数值为 0.57503，这表明以太坊市场表现出长距离依赖的特性。由于内部相关性的存在，以太坊回报系列是分形的，效率低下，并且有内部趋势。内部趋势的存在表明，可以根据历史信息预测短期回报趋势，这对投资是有利的。图 6.1 展示了在 3 个月滑动窗口下的 Hurst 指数和对数价格曲线，我们可以发现 Hurst 指数和同一时期的价格之间有很强的一致性。例如，ETCWin，基于以太坊的第一家数字货币交易所，于 2016 年 12 月成立，从而导致了以太坊应用的爆炸式增长。我们还可以从图 6.1a 看出，2016 年 12 月，Hurst 指数达到峰值，远高于 0.5，暗示以太坊回报将继续当前的上升趋势。图 6.1a 中的价格曲线在 2016 年 12 月之后相对较长时间持续上升，这一结果与我们的先前的说法非常一致。

当比较图 6.1 中以太坊和比特币回报的 Hurst 指数曲线时，我们观察到以太坊回报曲线的波动性更大。相反，比特币回报的 Hurst 指数相对稳定。这个 Hurst 指数曲线逐渐从下方接近 0.5，然后围绕这个值波动，表明比特币市场正在变得更加成熟（Di Matteo 等人 2003）。这一现象表明，与比特币市场相比，以太坊市场不够成熟，因为它是一种较新的加密货币。然而，我们也可以观察到，以太坊 Hurst 指数的波动随着时间逐渐减小，表明这个新兴市场现在正在成熟。

#### 6.2.5.2 多分形性

关于长距离依赖的讨论揭示了以太坊市场的可预测模式，并显示了市场分形分布的特性。同时考虑到回报的厚尾分布，根据先前工作（Lahmiri 等人 2018）的结论，我们假设以太坊市场存在多分形结构。因此，接下来我们将探索多分形性质，以检测不同时间尺度上价格的波动特性。

图 6.2 绘制了 *H*(*q*) 值与 *q* 之间的关系，其中 *q* 从 -6 到 6 变化（间隔为 0.5）。为了评估多分形不对称性，我们还绘制了 *H* ^+(*q*) 和 *H* ^−(*q*) 的曲线。总的来说，当 *q* > 0 时，*H*(*q*) 描述大波动的缩放行为，而当 *q* < 0 时，它描述小波动的缩放。从图 6.2 可以看出，对于所有序列，*H*(*q*) 随着 *q* 的增加而减小，这表明与小波动相比，大波动的内部相关性较弱。这个结果支持了以太坊和比特币都存在多分形，因为 *H*(*q*) 取决于 *q*，并且表明当面临小波动时，市场更有可能维持当前趋势。![../images/506524_1_En_6_Chapter/506524_1_En_6_Fig2_HTML.png](img/506524_1_En_6_Fig2_HTML.png)

图 6.2

整体、上升和下降的广义 Hurst 指数曲线对于（**a**）ETH 和（**b**）BTC 回报序列

此外，从图 6.2 中，我们可以观察到以太坊回报的趋势曲线始终高于其他两个，这意味着上升趋势的记忆明显比下降趋势的记忆长。换句话说，对于以太坊市场，当回报上升时，趋势会持续得更久，而且前者为投资者提供的投资风险会更小。此外，随着波动的增加，多分形不对称性也变得更弱。

然而，对于比特币，回报序列的多分形不对称性在较大波动时更为明显，比特币的三条曲线比以太坊的更为复杂。此外，通过比较，比特币回报上升和下降的长期依赖性对于较小波动相对更强，对于较大波动则较弱，这表明比特币市场的持续性更可能受到波动的影响。

图 6.3 说明了多分形谱*f*(*α*)如何随*α*变化，表 6.2 显示了不同情况下的奇点谱宽度（Δ*α*）。表 6.2 中的结果显示，对于以太坊收益，上升趋势显示出比下降趋势更强的多分形程度，特别是对于大波动(*q*>0)的情况。与以太坊的结果不同，比特币在小波动时具有更明显的多分形性，因为上升趋势的Δ*α*大于下降趋势的Δ*α*。此外，我们可以发现，比特币的Δ*α*平均大于以太坊的，这表明比特币的多分形性更强，比特币价格更容易受到波动的影响。总的来说，多分形程度较弱和Δ*α*较窄表明投资风险较低，因此这一分析可以帮助投资者调整他们的投资策略，使投资更加合理。![../images/506524_1_En_6_Chapter/506524_1_En_6_Fig3_HTML.png](img/506524_1_En_6_Fig3_HTML.png)

图 6.3

奇点谱*f*(*α*)与*α*的关系对于（**a**）ETH 和（**b**）BTC 收益系列

表 6.2

不同情况下的奇点谱宽度（Δ*α*）

|  | ETH | BTC |
| --- | --- | --- |
|  | Δ*α* | Δ*α*(*q*>0) | Δ*α*(*q*<0) | Δ*α* | Δ*α*(*q*>0) | Δ*α*(*q*<0) |
| --- | --- | --- | --- | --- | --- | --- |
| 总体 | 0.571970 | 0.298052 | 0.234831 | 0.589466 | 0.086779 | 0.401271 |
| 上升 | 0.613629 | 0.320023 | 0.249938 | 0.627751 | 0.150247 | 0.386848 |
| 下降 | 0.545993 | 0.232761 | 0.264445 | 0.695628 | 0.178399 | 0.399475 |

#### 6.2.5.3 因果关系

如上所述，我们已经从分形市场的角度探索了以太坊收益的特性。接下来，我们将关注投资者扮演的角色，或者投资者如何影响收益的变化。由于投资者的行为可以用成交量来表示，我们可以尝试检测以太坊交易量与收益之间的因果关系来说明这一点。

在进行第 6.2.3.3 节介绍的因果关系在分位数中的方法之前，我们首先应用了基于 VAR(*p*)模型的经典线性 Granger 因果关系，其中*p*是滞后阶数，根据 Hannan-Quinn 标准（HQ）设为 6（Liew 2004）。在线性 Granger 检验中，我们发现以太坊的交易量 Granger 原因收益，因为 P 值是 0.0025\。然而，当我们在 VAR(6)模型上应用 BDS（Broock 等人 1995）检验时，结果显示统计量值足够大，可以在 5%的显著性水平上拒绝序列线性依赖的零假设，即时间序列是非线性依赖的。因此，线性 Granger 因果关系的结果可能是不准确的，因此我们需要因果关系在分位数中测试来进一步衡量交易量和收益之间的因果关系。

在图 6.4 中给出的分位数因果关系检验结果表明，成交量是否对以太坊和比特币的收益或波动性产生 Granger 因果关系。注意这里我们选择收益的平方值来衡量收益的波动性。图 6.4 显示，成交量不能 Granger 引起两种加密货币的收益，因此成交量不能用来预测收益。至于波动性，图 6.4a 的结果显示，当分位数低于 0.38 或高于 0.83 时，因果关系相对较弱。也就是说，当波动性足够低或高时，它不能受到成交量的变化影响。但当波动性适中时，成交量可以用来预测收益波动的变化。在我们模拟的实验中，我们还测试了波动性是否可以用类似的方法预测成交量，计算出的检验统计量几乎全部低于显著性水平，表明波动性与成交量之间没有明显的因果关系。从图 6.4b 给出的检验统计量中，我们可以得出关于成交量与波动性因果关系对比特币市场的类似结论，尽管分位数范围更广，从 0.10 到 0.89。![../images/506524_1_En_6_Chapter/506524_1_En_6_Fig4_HTML.png](img/506524_1_En_6_Fig4_HTML.png)

Fig. 6.4

因果关系在分位数上的检验统计量（**a**）ETH 和（**b**）BTC，5% 显著性水平的值为 1.96

因此，我们可以得出结论，成交量是导致收益波动变化的原因，而不是直接影响收益，这种因果关系仅在以太坊和比特币的波动性适中时才得以建立。

## 6.3 检测加密货币市场的异常 schem

在本节中，我们将介绍我们的一项工作，旨在使用改进的 Apriori 算法检测加密货币市场的“泵 & 倾倒 schem”。这个例子可以帮助我们了解如何检测加密货币市场的异常 schem。

由于监管不足，加密货币市场吸引了骗局，例如，泵 & 倾倒（P&D）schem，股市中一种著名的欺诈行为，在市场上已经发现泛滥。为了帮助处理这个问题，作为一项初步研究，这项工作提出了使用改进的 Apriori 算法来检测可能涉及 P&D schem 的用户群体。算法的有效性通过使用 Mt. Gox 比特币交易所泄露的交易记录来验证。此外，通过探索一些被检测到的用户群体，发现了交易所中的许多异常交易行为。这些发现为加密货币市场中用户的行为提供了新的见解，从而对政策制定者、投资者和管理加密货币市场的管理者产生了有意义的启示。

### 6.3.1 引言

如今，著名的“泵”和“抛”骗局（Williams-Grut 2017），与交易所和价格操纵直接相关，被 INSIDER 揭露。^(1) “泵”和“抛”（P&D）是一种证券欺诈形式，涉及通过虚假和具有误导性的正面声明人为地推高所持股票的价格，以高价出售以低价购买的股票（Wikipedia contributors 2018）。随着加密货币市场的出现，P&D 骗局也出现在这个市场中（Williams-Grut 2017）。图 6.5 显示了在 Telegram（一款俄罗斯即时通讯软件）上发布的 P&D 广告，该软件加密程度很高，允许人们使用别名并隐藏自己的身份，以宣传“PumpKing Community”这一群组。该群组在通讯应用上有 17,000 名追随者，似乎致力于 P&D。如图所示，广告以财富承诺吸引人们。提到的 UBQ 和 GNO 是两种典型的加密货币。更详细的信息可以在 INSIDER 报告中找到（Williams-Grut 2017）。![../images/506524_1_En_6_Chapter/506524_1_En_6_Fig5_HTML.png](img/506524_1_En_6_Fig5_HTML.png)

图 6.5

Telegram 上宣传“PumpKing Community”的 P&D 广告截图。（来源：[www.cointelegraph.com](http://www.cointelegraph.com)）

P&D 骗局是非法的，因为我们在股票和债券等传统金融市场上受到严格的监管。然而，加密货币市场很大程度上是不受监管的，因此这些骗局泛滥成灾。毫无疑问，这些骗局伤害了投资者，阻碍了区块链技术的发展。幸运的是，政府和监管机构已经认识到这些骗局，并开始解决这些问题。例如，美国联邦贸易委员会于 6 月 25 日在芝加哥举办了一个关于加密货币骗局的研讨会（Federal Trade Commission 2018）。

正如这些例子所显示的，检测交易所的欺诈行为是一项紧迫且具有意义的任务。特别是，为公平交易环境测试 P&D 骗局不仅是投资者的愿望，也是交易所的责任。因此，本章重点关注 P&D 骗局的检测。虽然解决这个问题有意义且紧迫，但它对几个原因来说是一个巨大的挑战。首先，揭露 P&D 程序需要交换交易数据；然而，这些数据对用户来说非常机密，很难获取这些交易数据。其次，即使我们可以获取一些数据，由于交易所和加密货币的数量众多，很难决定应该调查哪个。第三，仅基于交易数据声明，用户无法参与 P&D 场景。

由于 P&D 计划的核心是在短时间内协调买卖目标加密货币，因此本章基于这一认识提出了一个改进的 Apriori 算法来帮助解决这个问题。据我们所知，这是文献中首次解决加密货币市场的这种骗局。这项研究可行的一个重要原因是，我们拥有 2.5 年的完整交易记录，并且是破产的 Mt.Gox 交易所的一部分。这些数据是在 2014 年初 Mt. Gox 申请破产不久后泄露的。基于这个数据集，在加密货币市场中发现了许多异常行为，例如价格操纵（Gandal 等人[2018]（#CR15））和 DDoS 攻击（Feder 等人[2018]（#CR12））。本章重点验证基于数据集提出的 P&D 计划发现算法。尽管，如前所述，不可能断言一个 P&D 计划，但这项初步研究加上实验结果，对以下方面做出了贡献：

+   我们提出了一种改进的 Apriori 算法，用于检测加密货币市场中的 P&D（买涨卖跌）骗局，据我们所知，这在文献中是首次提出。

+   基于提出的算法，在曾经主导的比特币交易平台上发现了许多新的异常行为，这补充了之前对加密货币市场的研究。

+   该算法为加密货币交易所提供了一个工具，以处理隐藏的 P&D 计划和其他市场操纵行为。此外，本章讨论的结果为加密货币市场中的用户行为提供了新的见解，这对决策者、投资者和从业者产生了重要的影响。

### 6.3.2 数据集与算法

#### 6.3.2.1 数据集

数据格式在 2014 年初，Mt. Gox 的 2011 年 4 月至 2013 年 11 月的交易历史以 CSV 文件的形式被泄露。表 6.3 报告了 2011/04/01 记录的泄露数据的一部分。在表中，每一行代表用户的记录（由*User_Id*标识）在*日期*那一刻购买或出售一定数量的比特币（即*Bitcoins*）的总金额为*Money*美元。因此，那一刻比特币的真实价格为*Money*∕*Bitcoins*。具有相同*Trade_Id*的两条记录表示交易的双方。泄露的数据有超过 1400 万条记录和 12 万用户。表 6.3

泄露数据的一部分

| 交易 ID | 日期 | 用户 ID | 类型 | 比特币 | 金额 |
| --- | --- | --- | --- | --- | --- |
| 35372 | 2011/04/01 00:28:00 | 3931 | 购买 | 23.02 | 18.061 |
| 35372 | 2011/04/01 00:28:00 | 895 | 出售 | 23.02 | 18.061 |
| 35373 | 2011/04/01 00:28:00 | 722 | 购买 | 10 | 7.8 |
| 35373 | 2011/04/01 00:28:00 | 895 | 出售 | 10 | 7.8 |

数据清洗

由于数据集中存在一些冗余记录，我们采用了类似于 Gandal 等人 (2018) 方法来清洗数据。具体来说，我们将每个（日期，用户 ID，类型，比特币）元组视为唯一，并删除所有冗余记录。此外，由于一个买入或卖出订单可能与多个合适的参与者匹配，并在数据集中产生多个记录，我们尝试合并这些交易。换句话说，我们将这些多次交易视为单一的买入和卖出交易。具体来说，我们将具有相同买方（卖方）的相邻交易记录视为买家的单一购买交易（卖方）。

通过检查交易记录，我们发现用户的交易次数是异质的。由于 P&D 计划可能不会太频繁地发生，我们删除了所有交易次数是平均用户交易次数 10 倍的用户的记录（共 1383 名用户）。此外，根据 Gandal 等人 (2018) 确定的用于价格操纵的 Markus 和 Willy 账户的记录也被删除。

#### 6.3.2.2 改进的 Apriori 算法

构建交易矩阵

由于 P&D 计划的关键特征是参与用户在同一时间周期内买入或卖出数字资产，因此我们可以通过寻找经常在同一时间周期内买入或卖出资产的用户群体来检测 P&D 计划。为此，我们引入了一个交易矩阵 *B* 以记录所有用户的购买交易。 （在以下内容中，我们基于购买交易呈现算法；对于销售交易，思路是相似的。）矩阵的每一行代表一个用户，每一列代表一个时间戳。当用户 *i* 在时间戳 *t* [*j*] 进行购买交易时，元素 *B*(*i*, *j*) = 1，否则 *B*(*i*, *j*) = 0。

算法的基本思路

在本节中，提出了一个基于连续时间属性的改进 Apriori 算法。简单来说，该算法通过给出购买矩阵 *B* 和两个参数，返回用户组及其“购买行为”的数量。在一个时间段内，如果一个用户组中的所有用户至少进行了一次购买交易，我们称该用户组在该时间段内具有“购买行为”。

具体来说，令*U*= {*u* [1], *u* [2], …, *u* [*n*]} 为所有用户的集合，*T*= {*t* [1], *t* [2], …, *t* [*T*]} 为所有购买交易时间戳的集合，而*T* [*i*] = {*t* [*i*1], *t* [*i*2], …} 是用户 *u* [*i*] 的购买交易时间戳集合。与关联分析类似，包含 *k* 个用户（即组的大小）的用户组被称为 *k*-组。对于给定的时间间隔 *span*，如果 *group* 中的每个用户在时间区间 [*t* − *span* + 1, *t* + *span*] 内至少进行了一次购买交易，则称该用户组具有同时购买交易。用户组 *support* 计数是在用户组具有同时购买交易的不重叠时间区间数。所提出的算法旨在找到所有支持大于给定阈值 *mincnt* 的组（及其相应的支持）。

所提出方法的伪代码在算法 6.1 中显示（#FPar1）。算法的两部分。第一部分（第 1 行至第 9 行）返回所有的 *k*-组（表示为 *F* [*k*]）及其相应的支持（表示为 *supports* [*k*]）。第一行引入了一个用户集 *C* [1]，其中包括了所有的用户。然后通过计算用户支持并过滤掉支持小于 *mincnt* 的用户，构建 1-组 *F* [1]；相应的支持记录在 *supports* [1] 中（第 3 行）。接下来，如果 *F* [(*k*−1)] 不是一个空集，那么使用 *Apriori* 原理（第 5 行）构建候选 *k*-组 *C* [*k*]，并通过定义的函数 *COUNT* 计算 *k*-组 *F* [*k*]及其支持 *supports* [*k*]。*COUNT* 函数（第 10 行至第 33 行）是算法的另一部分。它计算给定的 *n*-组（*n* ≥ 2）的支持。 （计算 1-组的支持只需要计算用户购买频率，因此算法中没有呈现。）假设 *T* [*i*] (*i* = 1, 2, …, *n*) 是组中用户的全部购买交易时间戳集合（第 12 行至第 15 行），为了计算 *n*-组的支持，算法中选择组中的一个枢轴用户（在算法中，第一个用户被选为枢轴）。计数过程遍历枢轴用户的每个购买交易时间戳，并在需要时增加计数器（即 *common times*）。例如，如果其他所有用户在 *i*th 时间戳区间内都进行了一次购买交易（即 ！[

$$[t_{i_{begin}}, t_{i_{end}}]$$

](../images/506524_1_En_6_Chapter/506524_1_En_6_Chapter_TeX_IEq34.png)), 计数器增加一（第 17 行至第 32 行）。如果相邻的时间区间相交，则将后者的左端点设置为前者的右端点的下一秒，以避免重叠（第 25 行至第 26 行）。

算法 6.1 改进的 Apriori 算法![../images/506524_1_En_6_Chapter/506524_1_En_6_Figa_HTML.png](img/506524_1_En_6_Figa_HTML.png)

## 6.4 实验结果

为了验证所提出的算法，我们用它来探索 2013 年 5 月的交易记录。我们选择这个月的数据，因为它包含足够的记录，而且这个月的比特币价格波动很大。我们将*跨度*分别设置为 1、5 和 10 分钟，以查看不同时间间隔下用户群体的分布。此外，两种交易类型（即购买和出售）都被考虑在内。图 6.6 显示了结果。从图中可以看出，购买和出售交易记录中识别出的群体数量和大小是不同的。在购买交易记录中，发现了更多的群体。结果显示，更多的用户一起购买，但出售时间是不同的。总的来说，随着群体规模的增大，群体数量减少。但在购买交易记录中，当跨度为 10 分钟时，有五个群体数量最多。很难说被检测到的组织涉及 P&D 计划。但奇怪的是，一些用户更倾向于一起购买。为了检查异常行为，我们手动探索了一些群体。这样做后，我们发现了许多异常现象。因此，在以下章节中，我们将总结数据集中发现的所有的异常现象，并讨论可能的成因。具体来说，可以发现两种异常行为：异常交易行为和异常交易价格。![../images/506524_1_En_6_Chapter/506524_1_En_6_Fig6_HTML.png](img/506524_1_En_6_Fig6_HTML.png)

图 6.6

改进的 Apriori 算法的结果

### 6.4.1 异常交易行为

在分析 1 组用户时，我们发现有些用户在购买和出售比特币的行为上存在极大的差异。例如，有些用户的比特币购买量远远超过我们的出售量，而其他人则相反。为了量化这种差异，我们引入了以下用户符号：

+   **计数** [**购买**]: 购买交易的次数

+   **计数** [**出售**]: 出售交易的次数

+   **比特币** [**购买**]: 用户购买的总比特币数量

+   **比特币** [**出售**]: 用户出售的总比特币数量

基于上述符号，我们可以定义两个比率：![

$$\displaystyle \begin{aligned}rate_{count} = \frac{count_{buy}}{count_{sell}},rate_{amount}= \frac{bitcoins_{buy}}{bitcoins_{sell}}.\end{aligned}$$

图片对于普通投资者来说，上面定义的两种频率可能很长一段时间都接近 1。因此，我们定义了三种异常用户，并在表 6.4 中显示了相应的用户数量。正如所看到的，奇怪的是，有相当多的用户在系统中从未买过或卖过比特币。一个可能的原因是一些记录缺失。然而，通过与多个 Mt. Gox 用户沟通验证了数据集（Feder 等人 2018）。因此，更合理的解释是这些账户（即用户）可能被交易所用于某些特殊目的，例如平衡交易和提供流动性。到目前为止，我们至少可以说 Mt. Gox 交易所上有一些假交易。表 6.4

异常交易行为统计

| 类型 | 描述 | 用户数量 |
| --- | --- | --- |
|  |  |  |
| I | *计数* [*买*] = 0 | 9367 |
|  | *计数* [*卖*] = 0 | 2026 |
| II | *频率* [*计数*] ∈ (5, *∞*) | 4586 |
|  | *频率* [*计数*] ∈ (0, 0.2) | 3809 |
| III | *频率* [*比特币*] ∈ (5, *∞*) | 4697 |
|  | *频率* [*比特币*] ∈ (0, 0.2) | 3695 |

### 6.4.2 异常交易价格

通过进一步比较数据集中比特币的实时价格与 investing.com 上公布的比特币价格，我们发现有些用户总是以异常价格交易，即实时价格远高于当天的最高价格或远低于当天的最低价格。表 6.5 显示了两个异常交易价格交易。因为 2013 年比特币的价格在(13 美元, 1100 美元)之间，所显示记录的价格明显异常。表 6.5

异常价格交易记录

| 交易 ID | 日期 | 用户 ID | 类型 | 比特币 | 货币 | 价格 |
| --- | --- | --- | --- | --- | --- | --- |
| 1362098659903894 | 2013-03-01 00:44:19 | 231 | 买 | 0.01 | 0.01 | 1 |
| 1362098659903894 | 2013-03-01 00:44:19 | 231 | 卖 | 0.01 | 0.01 | 1 |
| 1367359249580015 | 2013-04-30 22:00:49 | 310991 | 买 | 1.0000 | 13,839.17 | 13,839.17 |
| 1367359249580015 | 2013-04-30 22:00:49 | THK | 卖 | 1.0000 | 13,839.17 | 13,839.17 |

由于 Mt.Gox 交易所已经关闭，从交易所收集历史数据变得困难，因此我们可以从*investing.com*查询历史数据。由于交易平台之间可能存在一定价格差异，我们在 investing.com 上考虑实时价格为*异常*，如果它高于当天的最高价格的 150%或低于最低价格的 50%。我们从整个数据集中提取了 471,899 个异常价格交易记录，占所有交易记录的 3.04%。这些异常价格交易涉及 16,660 个用户，占数据集中用户的 13.09%。

在以下内容中，我们关注最活跃的用户及其对手方。通过统计所有用户的异常定价交易次数，我们发现用户 ID“THK”、“231”、“TIBANNE_LIMITED_HK”和“698630”是最为活跃的四位用户。异常用户“698630”在 Gandal 等人（2018）中被命名为*Markus*，因为它从不支付交易费，且交易价格几乎随机。用户“231”有 53 个对手方进行了异常定价的交易。在所有对手方中，“231”最为频繁，达到了 55,380 次（即用户“231”与自己交易）。此外，用户“231”总是以非常低的价格与自己交易，且价格总是 1 美元/比特币。此外，在用户“TIBANNE_LIMITED_HK”和“THK”的记录中也发现了“与自己交易”的情况。这些特征表明这些账户是“真实”的异常账户。当探索用户“THK”的对手方时，我们发现了一个由另外三名用户组成的交易群体，分别是用户“300696”、“428513”和“444956”。这三名用户在 2013 年 5 月同时进行了 16 次交易。提取这三名用户的全部交易记录，几乎所有他们的交易价格都是异常的。用户“300696”和用户“444956”总是以绝对低价交易，比当天最低价低得多，而用户“428513”总是以绝对高价交易，比当天最高价高出许多。由于用户“THK”与这三名用户同时进行交易，因此推测这四名用户可能组成一个交易群体来制造虚假交易。

## 6.5 总结

在本章中，我们介绍了关于基于区块链的加密货币市场分析的两个主要研究方面，包括加密货币市场特征分析和检测加密货币市场异常方案。我们还将使用我们的工作作为例子来说明这两种研究视角。在本节的剩余部分，我们将总结这些工作并介绍它们未来的研究方向。

至于前者，我们从分形市场的角度分析以太坊回报的特性，并讨论投资者行为如何影响回报的变化。首先，通过计算 Hurst 指数，我们展示了以太坊回报中存在长程依赖，这表明回报序列具有持久性行为，并否定经典的效率市场假说。其次，我们验证了存在厚尾分布，并进一步探索了以太坊市场的多分形特性和多重分形的不对称性。最后，我们发现以太坊的交易量（在一定程度上反映投资者的活跃度）对回报没有明显的因果关系，但在波动性适中时会导致市场波动。与比特币市场的比较显示，以太坊市场的 Hurst 指数波动更大，多重分形性更弱，这表明以太坊市场不如比特币市场成熟，投资风险较低。我们的分析和结果可以为以太坊投资者和关注以太坊市场的研究人员提供有益的见解。未来，可以投入更多研究力量，从金融角度揭示这些特性的原因。

当涉及到后者时，我们提出了一种改进的 Apriori 算法来检测可能涉及“泵 & dump”计划的用户群体。通过著名比特币交易所 Mt.Gox 泄露的交易历史，我们发现许多用户同时买入和卖出。为了进一步分析检测出的群体，我们找到了许多异常交易记录，即异常交易行为和交易价格。其中一些异常行为可能是由交易所控制的账户引起的。未来，我们计划进一步研究系统中的异常行为和用户，评估这些行为对比特币价格的影响。