<hgroup>

# 第三部分

# 概率数据结构概述

</hgroup>

<hgroup>

# 9

# 概率数据结构简介

</hgroup>

## 9.1 概率数据结构的需求

近年来数据生成呈指数增长。这种庞大的数据增长给工业和学术界的存储和查询处理带来了挑战。在分析大型数据集的日志时，需要执行不同的查询操作，例如计算唯一项的数量，计算数据项的频率，搜索集合中的任何项等。此外，我们还需要探究更复杂的数据集，例如图像、视频、网页等。显然，为了在数据上执行这些查询操作，必须将数据存储在计算机内存中。磁带、硬盘、固态硬盘是计算系统可用的不同类型的内存。然而，这些不同类型的内存具有不同的特性，如图 9.1 所示。例如，硬盘是机械设备，与集成在半导体芯片上的主存储器相比，它们的访问速度较慢，这使得从硬盘中的数据库查询耗时。因此，对于一个查询，处理器每次都必须访问硬盘以获取所需的数据，这显然是一个缓慢的操作。而且，与主存储器相比，磁盘访问的成本较高（这就是为什么 1GB 的主存储器比 1GB 的硬盘要贵得多）。

![图 9.1](img/fig9_1.jpg)

**图 9.1**

计算机内存层次结构。

此外，为了执行一个进程，它需要在主存中，因此必须从辅助存储器交换到主存中，如图 9.2 所示。同时，对于开发人员来说，主存易于使用，因为在主存中创建数组、链表或集合比使用 Hadoop 数据库或 Apache Solr 在辅助存储器中读取或写入文件要容易得多。这些即将到来的大数据技术通常用于提供准确的分析和决策。这些技术提供了分布式数据存储和并行处理。虽然分布式数据库 Hadoop 与重型处理引擎（Spark、MapReduce）在批处理框架方面表现良好，其目标是提高作业吞吐量而不是处理速度问题。值得注意的是，数据的批处理不会施加任何时间约束，因此可以存储在磁盘上，并且可以以批量方式处理查询。此外，在辅助存储器中使用 SQL 处理查询的流行方法会导致高空间复杂性。例如，Powerdrill 是一种列向数据存储方法，面临着对大型数据集的高内存和计算开销的挑战。然而，流数据需要实时处理，最小延迟是可能的，这是通过提高访问速度实现的。此外，流数据需要在单次通过中处理。因此，最好更多地在主存中工作，以实时处理流数据以及在单次通过中处理数据。随着数据库和应用程序数据集的不断增长，需要一种紧凑的数据结构来正确管理和处理数据。

![图 9.2](img/fig9_2.jpg)

**图 9.2**

通过交换进行内存管理。

当前数据生成的情景导致了需要处理大量数据的新应用程序的发布。传统算法假设将数据适应主存储器，但在处理如此大量的数据时会失败。在这种情况下，流式算法（在消耗有限的存储和时间的同时以一次或几次传递处理数据）在研究人员中变得流行起来。

不幸的是，为了解决上述问题，确定性数据结构，如哈希表、数组、二叉搜索树无法处理大型数据集，因为一次性将大量流式数据放入内存中是困难的。传统数据结构无法超越线性处理的进一步方面。此外，对于大型数据集，确定性数据结构提供的多项式运行时间复杂性并不有利。此外，数据的 3V 特性（容量、多样性和速度）要求实时分析和处理。此外，数据的复杂性和数据中的噪声没有定义。由于事先不知道数据的大小，因此无法预测存储数据所需的内存需求。因此，需要一种能够支持快速响应时间和有效存储空间的有效数据结构来解决这些挑战。为了解决这些挑战，最近许多研究人员和程序员开始使用概率数据结构（PDS）。

PDS 允许在主内存中对数据执行基本查询操作。PDS 的用例是处理不适合主内存的大数据。PDS 用于查询操作，如成员检查、频率检查、相似性检查和基数检查。低内存需求和良好的处理速度是 PDS 的两个独特属性。然而，PDS 的工作高度依赖于密码哈希函数，这些函数能够在插入数据时提供随机性和灵活性。当哈希函数应用于大数据集时，它以紧凑的形式总结数据，极大地减少了存储需求，并且其行为难以预测。在这里，密码哈希函数还必须满足三个主要要求：

+   工作因子：为了抵御暴力破解，哈希函数应该具有计算上的昂贵性。

+   粘性状态：无法创建具有合理输入模式的状态。

+   扩散：哈希函数的相关输出位应该是每个输入位的复杂函数。

密码哈希函数进一步分为有密钥哈希函数和无密钥哈希函数两类。有密钥哈希函数涉及一个秘密密钥，而对于无密钥哈希函数，密钥为所有人所知。有密钥哈希函数用于消息认证码（MAC）。

特别需要注意的是，PDS（概率数据结构）基于无键哈希函数。有了这一认识，这种数据结构的性质因随机选择的哈希函数而随机化。而且，在大多数情况下，并不重要知道集合中的哪个项已经匹配，有时只需要知道是否已经进行了匹配。因此，只需存储项的签名而不是值。此外，PDS 不会在相同的操作序列下每次都产生相同的结构。因此，PDS 也被称为草图数据结构。值得注意的是，PDS 会出现与特定结构不一致的情况是预期的。然而，它们具有恒定的查询处理时间，并且可以轻松并行化（因为哈希具有独立属性），用于实时数据处理以获得快速响应。接下来的章节将详细讨论成员查询、基数估计、相似度搜索和频率估计 PDS，以及它们的 Python 实现。有关 PDS 分类，请参阅图 9.3。

![图 9.3](img/fig9_3.jpg)

**图 9.3**

PDS 的分类。

由于内存需求的最小化，PDS 对大数据和流数据应用非常有用。

## 9.2 确定性数据结构与概率性数据结构

IT 专业人员遇到不同的确定性数据结构，例如数组、哈希表等。然而，使用这些内存中的传统数据结构，如插入、搜索、删除等操作是以特定键值执行的。这些数据结构产生确定性（准确）的结果。与此相反，在 PDS 的情况下，操作的结果可能是概率性的，这意味着结果是近似的，而不总是确定的。值得注意的是，传统数据结构可以执行 PDS 可以执行的所有操作，但仅适用于小数据集。然而，如果数据集太大而无法放入内存，传统数据结构在该情况下失败。此外，对于需要一次处理数据的流式应用，使用传统数据结构很难处理。表 9.1 显示了确定性数据结构和概率性数据结构之间的区别。

**表格 9.1**

确定性数据结构和概率性数据结构的区别。

| 确定性数据结构 | 概率性数据结构 |
| --- | --- |
| 不会产生误报 | 在查询处理时会产生误报 |
| 提供最优路径 | 提供良好路径而不是最优路径 |
| 不一定使用哈希函数 | 这些数据结构严格使用哈希函数来处理查询 |
| 将数据存储为实际格式 | 仅存储数据的签名而非实际数据 |
| 在 PDS 上使用更多内存 | 在传统数据结构上使用较少内存 |
| 在线性、次线性、二次、阶乘等时间内处理查询 | 仅在常数时间内处理查询 |
| 生成无误差结果 | 处理查询时会产生错误。然而，错误率具有特定的结构 |
| 当需要完全准确性时使用 | 当需要速度和低内存而不是完全准确性时使用 |
| 将数据存储为非活跃形式 | 将非均匀分布的数据转换为均匀分布的数据 |
| 示例：数组、链表 | 示例：Bloom 过滤器、HLL |

## 9.3 概率数据结构应用

要构建有效的应用程序，一个做法是高效地使用数据结构。事实上，选择一个好的数据结构是一个优秀程序员的标志。任何涉及大规模业务的应用程序都可以利用 PDS。分析大数据集、统计分析、挖掘庞大数据集是 PDS 的一些用例。例如，检查亚马逊上的特定商品是否可以订购。然而，PDS 的应用不仅局限于计算机科学领域，还用于各个领域。例如，在将 DNA 序列分类为新的或已知的基因组方面。

+   当多个文件共享相同数据或相同数据在给定文件中出现在多个位置时，定义为数据块的重复。将每个文件与所有其他文件进行比较涉及重量级处理。PDS 通过存储数据块的指纹而不是存储原始数据，并匹配哈希来找到重复文件来解决此问题[71]。

+   当攻击者向特定机器发动洪水攻击，使其在用户需要时无法访问时，就定义了 DDoS（分布式拒绝服务）攻击。这需要对网络流量进行监控。一种解决方案是分析 IP 数据包的目标 IP 地址，如果任何 IP 地址的计数器值超过预定义的阈值，则该地址被视为可疑。PDS 可以帮助以较少的内存和恒定的时间分析这些数据包。

+   同样，使用 PDS（概率数据结构）可以简化个人电子邮件的过滤，因为垃圾邮件检测系统涉及一个包含电子邮件签名的大型数据库[216]。

+   网络流量的增长需要网络监控和流量工程的需求。为了有效运行，数据中心和 PDS 草图用于任务，如重型打击者检测、流量矩阵估计、流量模式检测等。PDS 草图已被证明可以最小化网络中信息收集的计算成本[137]。

+   基数估计 PDS 用于检查在任何特定网站上查看文章的唯一 IP 地址有多少。

+   PDS 还用于涉及将序列分类为新颖或已存在基因组的 DNA 序列。测序意味着计算 DNA 片段中碱基对的正确顺序。此外，PDS 还用于分析 DNA 测序中的相关性[109]。

+   PDS 值得一提的应用是查找数据集中频率大于预定义数字的所有元素。PDS 的这种特性用于检测网站的重型打击者。

+   同样，PDS 可以用于具有 350000 个词典单词的拼写检查应用程序。

## 9.4 概率数据结构挑战

PDS 通过使用固定或亚线性内存以及提供恒定执行时间来优化算法性能。然而，PDS 面临的最大挑战是它们无法提供精确答案并显示一定的错误概率。但是，可以通过与 PDS 资源的权衡来控制此错误。因此，对于精度降低不可接受的情况（如银行账户、军事应用），不建议使用 PDS。然而，对于小错误成本的情况（如推荐电影、计算独立访问者、防止 DDoS 攻击），可以推荐使用 PDS。

## 活动

### 多项选择题

1.  以下哪种存储器的访问速度最慢？

    1.  寄存器

    1.  主存储器

    1.  硬盘

    1.  磁带存储

1.  密码哈希函数的要求是什么？

    1.  单向

    1.  工作因子

    1.  扩散

    1.  所有上述内容

1.  在键控哈希函数中，密钥为所有人所知。

    1.  真

    1.  错误

1.  哪种内存具有最大的易用性？

    1.  寄存器

    1.  主存储器

    1.  硬盘

    1.  磁带存储

1.  以下关于 PDS 的陈述哪个是错误的？

    +   PDS 也被称为草图数据结构

    +   PDS 也被称为确定性数据结构

    +   PDS 操作的结果会有一定的误差

    +   布隆过滤器是 PDS 的一个例子

1.  以下哪个是基数估计 PDS 的一个例子？

    1.  HyperLogLog

    1.  BF

    1.  跳表

    1.  最小哈希

1.  以下哪个是成员查询 PDS 的一个例子？

    1.  布谷鸟过滤器

    1.  最小哈希

    1.  Simhashing

    1.  LogLog

1.  以下哪个是频率查询 PDS 的一个例子？

    1.  布谷鸟过滤器

    1.  CMS

    1.  Simhashing

    1.  LogLog

1.  PDS 对大数据和流数据应用非常有用

    1.  真

    1.  错误

1.  以下哪个是 PDS 的一个例子？

    1.  检测 DDoS 攻击

    1.  拼写检查器

    1.  监控 IP 流量

    1.  所有上述内容

1\. d  2\. d  3\. b  4\. a  5\. b  6\. a  7\. a  8\. b  9\. a  10\. d

<hgroup>

# 10

# 成员查询概率数据结构

</hgroup>

## 10.1 成员查询概率数据结构

在处理流式物联网数据时，经常需要以最小的延迟和空间搜索特定项。成员查询概率数据结构（MSQ PDS）的目的是检查大型集合<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>S</mi><mo stretchy="false">)</mo></mrow></math>中元素*x*的存在。使用链表、数组或平衡二叉树的成员查询操作需要与集合*S*大小线性的内存空间。哈希表也有更大的大小，因此它所占用的内存也更大。另一方面，MSQ PDS 在处理大数据和流式应用程序的查询方面越来越受欢迎，因为这些数据结构消耗的内存较少。此外，MSQ PDS 提供恒定的查询时间。为了提供优化的空间效率，与存储整个数据集相反，MSQ PDS 使用哈希存储数据的摘要形式。表 10.1 表示了不同数据结构中成员查询操作的空间和时间复杂度的比较。插入和删除（对于某些特定的 MSQ PDS）是 MSQ PDS 支持的操作。

**表 10.1**

不同数据结构中搜索的空间和时间复杂度

|  | 线性数据结构 | 非线性数据结构 | 哈希数据结构 | 概率数据结构 |
| --- | --- | --- | --- | --- |
| 示例： | 数组、链表 | 图、二叉搜索树 | 哈希表 | 布隆过滤器、快速过滤器、跳表 |
| 空间复杂度 | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math> | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math> | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math> | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>m</mi><mo stretchy="false">)</mo></mrow></math> |
| 搜索时间 | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math> | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><mi>g</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math> | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math> | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>k</mi><mo stretchy="false">)</mo></mrow></math> |

*n*：数据大小，*m*：PDS 大小（*m* ¡ ¡ *n*），*k*：哈希函数的数量，DS：数据结构，BST：二叉搜索树

尽管在使用 MSQ PDS 时预期会出现可预测的错误。但是，在此处，错误被管理在预定义的边际阈值下，以权衡准确性和存储需求。布隆过滤器、商过滤器和跳表是在此类别下广泛使用的 PDS，本章将进一步讨论它们。此外，布隆过滤器的流行导致了其各种变体，具有一些标准布隆过滤器不支持的额外功能。然而，作为容错方法的一部分，布隆过滤器和商过滤器在成员查询中返回带有误报的结果，而跳表不会返回任何错误。

False positive 表示即使元素不在集合中，查询结果可能会输出 true，而 false negative 意味着对于元素的存在，查询结果为否定。 图 10.1 中已经表示了 false positive 和 false negative 的区别。此外，模型的精确度和召回率值可以从 Eqs. 10.1 和 10.2 分别计算出来，其中精确度描述了计算结果在总正预测中的准确性，而召回率描述了正确识别的实际正值的比例。下一个主题将讨论布隆过滤器的概念。

![图 10.1](img/fig10_1.jpg)

**图 10.1.**

False positive vs. false negative.

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>P</mi><mi>r</mi><mi>e</mi><mi>c</mi><mi>i</mi><mi>s</mi><mi>i</mi><mi>o</mi><mi>n</mi><mo>=</mo><mfrac><mrow><mi>T</mi><mi>r</mi><mi>u</mi><mi>e</mi><mi>p</mi><mi>o</mi><mi>s</mi><mi>i</mi><mi>t</mi><mi>i</mi><mi>v</mi><mi>e</mi></mrow><mrow><mi>T</mi><mi>r</mi><mi>u</mi><mi>e</mi><mi>p</mi><mi>o</mi><mi>s</mi><mi>i</mi><mi>t</mi><mi>i</mi><mi>v</mi><mi>e</mi><mo>+</mo><mi>F</mi><mi>a</mi><mi>l</mi><mi>s</mi><mi>e</mi><mi>p</mi><mi>o</mi><mi>s</mi><mi>i</mi><mi>t</mi><mi>i</mi><mi>v</mi><mi>e</mi></mrow></mfrac></mrow></mtd></mtr></mtable></mrow></math>(10.1)

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>R</mi><mi>e</mi><mi>c</mi><mi>a</mi><mi>l</mi><mi>l</mi><mo>=</mo><mfrac><mrow><mi>T</mi><mi>r</mi><mi>u</mi><mi>e</mi><mi>p</mi><mi>o</mi><mi>s</mi><mi>i</mi><mi>t</mi><mi>i</mi><mi>v</mi><mi>e</mi></mrow><mrow><mi>T</mi><mi>r</mi><mi>u</mi><mi>e</mi><mi>p</mi><mi>o</mi><mi>s</mi><mi>i</mi><mi>t</mi><mi>i</mi><mi>v</mi><mi>e</mi><mo>+</mo><mi>F</mi><mi>a</mi><mi>l</mi><mi>s</mi><mi>e</mi><mi>n</mi><mi>s</mi><mi>e</mi><mi>g</mi><mi>a</mi><mi>t</mi><mi>i</mi><mi>v</mi><mi>e</mi></mrow></mfrac></mrow></mtd></mtr></mtable></mrow></math>(10.2)

## 10.2 Bloom Filter 及其变体

BF 的概念是由 Burton H. Bloom 在 1970 年提出的 [46]。BF 位于主存储器内，使用 BF 可以快速检查 MSQ。标准 BF 支持插入和查找两种操作。然而，标准 BF 的查找操作偶尔会出现误判，但永远不会出现漏判。显然，BF 应该在可以接受一定误判的情况下使用。

### 10.2.1 Bloom 过滤器的结构

BF 是一个包含*m*个比特的数组，索引从 0 到 m-1，如图 10.2 所示。每个条目在过滤器中用一个比特来表示，即 0 或 1。除此之外，BF 使用*k*个不同的独立和均匀的哈希函数。BF 不存储数据本身，而是利用哈希来以紧凑的形式存储数据的哈希值。然而，所使用的哈希函数应具有快速速度。哈希函数的数量可以从 1 到*m*。BF 的比特都初始化为零。它首先对每个数据项执行多次哈希运算，然后将其哈希值存储在大小为*m*的数组中。显然，随着哈希函数数量的增加，BF 的速度会变慢。值得注意的是，BF 的搜索时间复杂度与数组大小和存储元素数量无关。对于固定的错误率，插入和查找操作的时间复杂度都是与所使用的哈希函数数量成比例的常数时间复杂度。因此，通过在位向量中编码信息，BF 可以紧凑地表示数据，并且可以以低带宽要求进行传输。尽管证明了相当有益，但 BF 也有一些缺点，列举如下：

+   尽管如此，BF 不支持删除，因为将比特重置为 0 可能会引入错误的否定（重置的比特可能代表 BF 中的其他元素条目）。然而，可以通过重置函数偶尔删除整个 BF。虽然，有各种 BF 的实例支持删除，例如，通过在内存中记录可变计数的计数 BF[79]，可删除的 BF[165]等。

+   在主存储器外扩展性差，因为在使用多个哈希函数的次级存储器上需要许多随机访问磁盘。

+   BF 无法动态调整大小。

+   无法计算每个元素的频率计数。它只能检查任何元素的存在。

![图 10.2](img/fig10_2.jpg)

**图 10.2.**

Bloom 过滤器的表示。

BF 的插入和成员查询操作描述如下：

+   要插入一个元素*x*，首先对元素*x*和对应于<math alttext="" display="inline"><mrow><mi>h</mi><mi>i</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo stretchy="false">(</mo><mi>i</mi><mo>=</mo><mn>1</mn><mo>,</mo><mn>2</mn><mo>,</mo><mn>...</mn><mo>,</mo><mi>k</mi><mo stretchy="false">)</mo></mrow></math>位置应用*k*个哈希函数，如果尚未设置，则将对应的位置设置为 1。

+   要检查元素*x*的成员资格，将元素*x*通过*k*个哈希函数传递以获得*k*个数组位置。如果这些位置对应的位中有任何一个位为零，则元素肯定不在集合中，否则，它可能存在。此外，即使所有*k*个相应的位置都为 1，元素可能也不在集合中（假阳性）。在设计 BF 时，开发者的一个目标是设计具有非常低的假阳性率的过滤器。然而，BF 永远不会出现假阴性。

例如，考虑一个情况，其中 BF 长度为 10 位，有三个哈希函数（<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo>,</mo><msub><mi>h</mi><mn>2</mn></msub><mo>,</mo><msub><mi>h</mi><mn>3</mn></msub></mrow></math>），其中 <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo>=</mo><mi>x</mi><mi>m</mi><mi>o</mi><mi>d</mi><mn>6</mn></mrow></math>，<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo>=</mo><mo stretchy="false">(</mo><mi>x</mi><mi>m</mi><mi>o</mi><mi>d</mi><mn>4</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>6</mn></mrow></math> 和 <math alttext="" display="inline"><mrow><mi>h</mi><mn>3</mn><mo>=</mo><mo stretchy="false">(</mo><mn>2</mn><mo>*</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>6</mn></mrow></math>。要插入元素 11，将键（*11*）通过所有哈希函数，得到 3 个索引，即，<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo>=</mo><mn>5</mn><mo>,</mo><msub><mi>h</mi><mn>2</mn></msub><mo>=</mo><mn>3</mn><mo>,</mo><msub><mi>h</mi><mn>3</mn></msub><mo>=</mo><mn>4</mn></mrow></math>，并将这三个结果位置设置为 1。类似地，要插入元素 3，位置 0、3 将被设置为 1，如 图 10.3 所示。然而，对于键 *5* 的成员查询结果肯定不在集合中，因为对应哈希函数 <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub></mrow></math> 的位置为零（见 图 10.4）。元素 12 的查找操作将产生误报，因为 12 不在集合中，但与所有三个哈希函数对应的位置（即 0、0、0）都被设置为 1，而对于元素 5，则表示真正的命中。同时，图 10.5 表示删除，可以观察到，从集合中删除元素 3 会导致元素 11 的误删。

**标准 BF 的并集和交集**

BF 也支持并集和交集的代数运算。假设 *BF(X)* 和 *BF(Y)* 是两个使用相同大小的过滤器和哈希函数的 BF。那么 *BF(X)* 和 *BF(Y)* 之间的交集和并集操作如下：

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>B</mi><mi>F</mi><mo stretchy="false">(</mo><mi>A</mi><mo>∩</mo><mi>B</mi><mo stretchy="false">)</mo><mo>=</mo><mi>B</mi><mi>F</mi><mo stretchy="false">(</mo><mi>A</mi><mo stretchy="false">)</mo><mo>∩</mo><mi>B</mi><mi>F</mi><mo stretchy="false">(</mo><mi>B</mi><mo stretchy="false">)</mo></mrow></mtd></mtr></mtable></mrow></math>(10.3)

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>B</mi><mi>F</mi><mo stretchy="false">(</mo><mi>A</mi><mo>∪</mo><mi>B</mi><mo stretchy="false">)</mo><mo>=</mo><mi>B</mi><mi>F</mi><mo stretchy="false">(</mo><mi>A</mi><mo stretchy="false">)</mo><mo>∪</mo><mi>B</mi><mi>F</mi><mo stretchy="false">(</mo><mi>B</mi><mo stretchy="false">)</mo></mrow></mtd></mtr></mtable></mrow></math>(10.4)

![图 10.3](img/fig10_3.jpg)

**图 10.3.**

在 BF 中进行插入。

![图 10.4](img/fig10_4.jpg)

**图 10.4.**

在 BF 中进行查找。

![图 10.5](img/fig10_5.jpg)

**图 10.5.**

在 BF 中进行删除。

**BF 的应用**

+   Yahoo 邮件使用 BF 来紧凑地表示用户的联系人列表，以便轻松地适配浏览器缓存内存。BF 的使用避免了回到后端服务器检查发件人的电子邮件地址是否已经存在于联系人列表中。

+   YouTube 使用 BF 来确保向用户推荐的视频不与用户的观看历史匹配。

+   URL 缩短器使用 BF 来确保生成唯一的 URL。

+   Tinder 使用 BF 来过滤右滑重复的情况。

+   Apache HBase，Postgress 数据库正在使用 BF 来检查特定记录是否存在，如果结果为正，则会从内存中获取记录。

+   Facebook 使用 BF 进行一次性奇观检查。一次性奇观用于那些流量很大的站点。它基本上检查仅发生一次且不再发生的事件。因此，BF 可以用于探测特定网页是否已经被访问过。如果有人只访问该站点一次，则不会提供太多内容和复杂的计算。另一种情况是，如果有人经常访问网站，则会提供更多个性化的内容。为了实现这个过程，采用 BF 并对访问者进行检查。如果结果为正，站点将提供昂贵的内容；如果结果为负，则提供缓存版本。

+   Quora，一个著名的提问平台，使用 BF 来过滤用户之前看过的故事。

+   BF 支持拼写检查器。

+   BF 被广泛用于在不同节点之间转发和路由数据包。

+   生物信息学[108]。

+   通过插入具有恶意 IP 地址条目的 BF 来预防 DDoS 攻击。[161]

**BF 中的假阳性概率：**

显然，假阳性率取决于过滤器中的 1 的数量和哈希函数的计数。

通过哈希函数传递给元素并设置一个位的概率由<math alttext="" display="inline"><mrow><mfrac><mn>1</mn><mi>m</mi></mfrac></mrow></math>给出，而不设置位（获取假阳性的概率）的概率由 Eq. 10.5 给出。

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>P</mi><mo>=</mo><mn>1</mn><mo>−</mo><mfrac><mn>1</mn><mi>m</mi></mfrac></mrow></mtd></mtr></mtable></mrow></math>(10.5)

当元素经过*k*个哈希函数时。因此，将元素映射到*k*个对应位置后，任意位未设置的概率由方程 10.6 给出。

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>P</mi><mo>=</mo><msup><mrow><mfenced close=")" open="("><mrow><mn>1</mn><mo>−</mo><mfrac><mn>1</mn><mi>m</mi></mfrac></mrow></mfenced></mrow><mi>k</mi></msup></mrow></mtd></mtr></mtable></mrow></math>(10.6)

现在，对于*n*次插入，将元素通过*k*个哈希函数传递后，任意位未设置的概率由方程 10.7 给出。

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>P</mi><mo>=</mo><msup><mrow><mfenced close=")" open="("><mrow><mn>1</mn><mo>−</mo><mfrac><mn>1</mn><mi>m</mi></mfrac></mrow></mfenced></mrow><mrow><mi>k</mi><mi>n</mi></mrow></msup></mrow></mtd></mtr></mtable></mrow></math>(10.7)

尽管如此，当一个位被错误地设置为高时，会发生误判率（FPR）。因此，任意位被设置为高的概率由方程 10.8 给出。

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>P</mi><mo>=</mo><mn>1</mn><mo>−</mo><msup><mrow><mfenced close=")" open="("><mrow><mn>1</mn><mo>−</mo><mfrac><mn>1</mn><mi>m</mi></mfrac></mrow></mfenced></mrow><mrow><mi>k</mi><mi>n</mi></mrow></msup></mrow></mtd></mtr></mtable></mrow></math>(10.8)

新元素经过*k*个哈希函数。因此，对于*k*个哈希函数，方程 10.8 可以改写为方程 10.9

-   <math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>P</mi><mo>=</mo><msup><mrow><mfenced close=")" open="("><mrow><mn>1</mn><mo>−</mo><msup><mi>e</mi><mrow><mfrac><mrow><mo>−</mo><mi>k</mi><mi>n</mi></mrow><mi>m</mi></mfrac></mrow></msup></mrow></mfenced></mrow><mi>k</mi></msup></mrow></mtd></mtr></mtable></mrow></math>(10.9)

-   从方程式 10.9 中可以清楚地看出，FPR 是 *k, m* 和 *n* 的函数。增加元素的总数并减少过滤器大小会导致 FPR 的增加。然而，通过增加 *k*，可以减少 FPR。不幸的是，通过增加 *k* 的值，系统的计算复杂度也会增加。另外，如果 *m* 的值设置为 <math alttext="" display="inline"><mi>∞</mi></math>，错误率趋于 0，而如果 *m* 的值为 1，则错误率趋于 0，这意味着出错的几率为 100%。为了实现最小的 FPR，在给定 *m* 和 *n* 的情况下，通过计算方程 10.10 中描述的最优 *k* 的值来使 *k* 的值保持不变。

-   <math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><msub><mi>k</mi><mrow><mi>o</mi><mi>p</mi><mi>t</mi></mrow></msub><mo>=</mo><mi>l</mi><mi>n</mi><mo stretchy="false">(</mo><mn>2</mn><mo stretchy="false">)</mo><mfrac><mi>m</mi><mi>n</mi></mfrac><mo>=</mo><mn>0.7</mn><mfrac><mi>m</mi><mi>n</mi></mfrac></mrow></mtd></mtr></mtable></mrow></math>(10.10)

-   此外，通过设定接受的目标 FPR *(p)* 并利用 *k* 的最优值，可以计算出过滤器 *m* 的大小：

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>P</mi><mo>=</mo><msup><mrow><mfenced close=")" open="("><mrow><mn>1</mn><mo>−</mo><msup><mi>e</mi><mrow><mfrac><mrow><mo stretchy="false">(</mo><mo>−</mo><mi>l</mi><mi>n</mi><mo stretchy="false">(</mo><mn>2</mn><mo stretchy="false">)</mo><mfrac><mi>m</mi><mi>n</mi></mfrac><mo stretchy="false">)</mo><mi>n</mi></mrow><mi>m</mi></mfrac></mrow></msup></mrow></mfenced></mrow><mrow><mi>l</mi><mi>n</mi><mo stretchy="false">(</mo><mn>2</mn><mo stretchy="false">)</mo><mfrac><mi>m</mi><mi>n</mi></mfrac></mrow></msup></mrow></mtd></mtr></mtable></mrow></math>（10.11）

进一步得到

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>m</mi><mo>=</mo><mo>−</mo><mfrac><mrow><mi>n</mi><mi>l</mi><mi>n</mi><mo stretchy="false">(</mo><mi>p</mi><mo stretchy="false">)</mo></mrow><mrow><msup><mrow><mo stretchy="false">(</mo><mi>l</mi><mi>n</mi><mo stretchy="false">(</mo><mn>2</mn><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow><mn>2</mn></msup></mrow></mfrac></mrow></mtd></mtr></mtable></mrow></math>（10.12）

因此，根据方程 10.12，可以计算出每个元素所需的最佳比特数为：

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mfrac><mi>m</mi><mi>n</mi></mfrac><mo>=</mo><mo>−</mo><mfrac><mrow><mi>n</mi><mi>l</mi><mi>n</mi><mo stretchy="false">(</mo><mi>p</mi><mo stretchy="false">)</mo></mrow><mrow><mi>l</mi><mi>n</mi><mn>2</mn></mrow></mfrac><mo>≈</mo><mo>−</mo><mn>1.44</mn><msub><mrow><mi>log</mi><mo>⁡</mo></mrow><mn>2</mn></msub><mi>p</mi></mrow></mtd></mtr></mtable></mrow></math>（10.13）

图 10.6 中呈现的图表显示了 FPR 随过滤器大小变化的变化情况，对于 1000 万个元素[41]。 可以观察到，随着过滤器大小的增加，误报率下降。 要使 *p* 小于 0.01 的单个哈希函数的情况下，过滤器的大小需要是总元素大小的 100 倍，而选择 *k = 5* 则可以在 100M 中提供相同的结果。

![图 10.6](img/fig10_6.jpg)

**图 10.6**

误报率 vs. 数组大小 [41]。

### 10.2.2 BF 在 Python 中的实现

![](img/list10_1.jpg)![](img/list10_2.jpg)![](img/list10_3.jpg)![](img/list10_4a.jpg)![](img/list10_4b.jpg)

### 10.2.3 BF 的变种

一些流行的 BF 变种如下所述，并且它们的比较显示在表 10.3 中。

**表 10.2**

当每个元素使用 8 位进行压缩时的情况。

| 每个元素的数组位 | <math alttext="" display="inline"><mrow><mfrac><mi>m</mi><mi>n</mi></mfrac></mrow></math> | 8 | 14 | 92 |
| --- | --- | --- | --- | --- |
| 每个元素的传输位 | <math alttext="" display="inline"><mrow><mfrac><mi>z</mi><mi>n</mi></mfrac></mrow></math> | 8 | 7.293 | 7.293 |
| 哈希函数 | k | 6 | 2 | 1 |
| 误报率 | P | 0.0216 | 0.0177 | 0.0108 |

*n*: 数据大小, *m*: BF 大小 *k*: 哈希函数数量, *z*: 期望压缩大小

**表 10.3**

不同 BF 变种的比较。

![表 10.3](img/tab10_3.jpg)

#### 10.2.3.1 计数 BF

如前所述，标准 BF 中的删除需要将一个位从 1 重置为 0，这可能导致出现假阴性，因为单个任意位可能表示多个元素。 作为这个问题的解决方案，作者们在[79]中设计了计数 BF，以在互联网上各种代理之间交换与 Web 缓存相关的信息。

值得注意的是，网络使用量的增加影响了网络的获取延迟。在这种情况下，分布式代理服务器通过维护每个其他代理服务器信息的 Web 缓存内存来改善延迟，这允许从邻近客户端的缓存中访问所需页面，而不是从原始 Web 源访问。Web 缓存共享可以从 BF 中获益，因为总的消息交换与代理服务器的总数成二次关系。Web 缓存的优点在于降低了因增加的 Internet 请求而导致的不必要的带宽消耗。在这个过程中，每个代理服务器都使用其他代理服务器缓存文档的紧凑和总结信息。Web 代理服务器定期使用它们当前的缓存条目构建 BF，并将其广播到网络中。对于缓存未命中，代理服务器会在其他代理服务器的 BF 中探测缓存命中。然后将查询发送到具有正面结果的代理服务器。误报概率通过减少带宽消耗来补偿，因为 BF 抑制了 URL 缓存摘要的完整列表的传输。分布式 Web 缓存的概念在 图 10.7 中表示。

![图 10.7](img/fig10_7.jpg)

**图 10.7.**

分布式 Web 缓存。

在计数 BF 中，与使用单个位来表示过滤器中的每个条目不同，而是使用固定大小的计数器值来跟踪哈希到该位置的元素的计数。 为了避免计数器溢出，毒素近似建议每个计数器使用 4 位，适用于大多数应用程序。 计数 BF 不仅仅检查元素的存在，还用于检查元素出现*θ*次或更多次的情况，其中*θ*表示计数阈值。 例如，如果*θ*=2，对于一次命中奇迹的情况，这意味着特定事件的一次命中或两次命中。 与标准 BF 类似，计数 BF 也会产生误报。 但是，与标准 BF 不同，如果尝试从过滤器中删除从未插入的元素，则计数 BF 可能导致假阴性。 参数*m*、*n*、*k*的定义与标准 BF 相同。 然而，据报道，计数 BF 导致空间浪费[51]。

最初，该过滤器中的所有位都是零。 计数 BF 支持的操作描述如下：

+   插入：要插入一个元素，需要经过*k*个哈希函数，然后递增对应于这些哈希函数的*k*个计数器。为了解释这个概念，考虑一个具有 3 个哈希函数的 BF，即，<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo>,</mo><msub><mi>h</mi><mn>2</mn></msub><mo>,</mo><msub><mi>h</mi><mn>3</mn></msub></mrow></math>) 其中 <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo>=</mo><mi>x</mi><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn></mrow></math>, <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo>=</mo><mo stretchy="false">(</mo><mn>2</mn><mi>x</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn></mrow></math>, <math alttext="" display="inline"><mrow><mi>h</mi><mn>3</mn><mo>=</mo><mo stretchy="false">(</mo><mn>2</mn><mo>*</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn></mrow></math>，而*x*代表要插入的数字。元素 9、15、8 的插入操作见图 10.8。每个元素对应的哈希索引为：

    <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mn>9</mn><mo stretchy="false">)</mo><mo>=</mo><mn>9</mn><mo>,</mo><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mn>9</mn><mo stretchy="false">)</mo><mo>=</mo><mn>1</mn><mo>,</mo><msub><mi>h</mi><mn>3</mn></msub><mo stretchy="false">(</mo><mn>9</mn><mo stretchy="false">)</mo><mo>=</mo><mn>8</mn></mrow></math>

    <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mn>15</mn><mo stretchy="false">)</mo><mo>=</mo><mn>5</mn><mo>,</mo><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mn>15</mn><mo stretchy="false">)</mo><mo>=</mo><mn>3</mn><mo>,</mo><msub><mi>h</mi><mn>3</mn></msub><mo stretchy="false">(</mo><mn>15</mn><mo stretchy="false">)</mo><mo>=</mo><mn>0</mn></mrow></math>

    <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mn>8</mn><mo stretchy="false">)</mo><mo>=</mo><mn>8</mn><mo>,</mo><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mn>8</mn><mo stretchy="false">)</mo><mo>=</mo><mn>9</mn><mo>,</mo><msub><mi>h</mi><mn>3</mn></msub><mo stretchy="false">(</mo><mn>9</mn><mo stretchy="false">)</mo><mo>=</mo><mn>6</mn></mrow></math>

    ![图 10.8](img/fig10_8.jpg)

    **图 10.8.**

    在计数 BF 中的插入操作。

+   查询：对于一个元素的成员查询，将该元素输入到 *k* 个哈希函数中。如果任何一个位映射到这些对应的位置为零，则意味着该元素绝对不在集合中，否则，可能存在。对于元素 9 和 15 的成员查询结果为真正，而对于元素 13 的成员查询报告为假正，如 图 10.9 所示（<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mn>13</mn><mo stretchy="false">)</mo><mo>=</mo><mn>5</mn><mo>,</mo><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mn>13</mn><mo stretchy="false">)</mo><mo>=</mo><mn>3</mn><mo>,</mo><msub><mi>h</mi><mn>3</mn></msub><mo stretchy="false">(</mo><mn>13</mn><mo stretchy="false">)</mo><mo>=</mo><mn>4</mn></mrow></math>）。

    ![图 10.9](img/fig10_9.jpg)

    **图 10.9.**

    计数 BF 中的查询。

+   删除：要删除一个元素，只需将相应位置的计数器值减一，如 图 10.10 中表示的元素 8\. 此外，图 10.11 表示了一个情况，即从过滤器中从未添加过的元素 13 被删除，随后对元素 8 的成员查询结果为假负。尽管计数 BF 支持删除，但其空间不能按需扩展 [92]。

    ![图 10.10](img/fig10_10.jpg)

    **图 10.10.**

    计数 BF 中的删除。

    ![图 10.11](img/fig10_11.jpg)

    **图 10.11.**

    理解计数 BF 的假负。

计数溢出是计数 BF 的一个缺点。如果计数器值达到 <math alttext="" display="inline"><mrow><msup><mn>2</mn><mi>w</mi></msup><mo>−</mo><mn>1</mn></mrow></math>（其中 w 表示计数器的宽度），则在此点之后无法递增。计数 BF 也支持与标准 BF 描述的相同应用程序。不同之处在于，计数 BF 可以替换 BF 并允许从 Web 缓存中删除最近未使用的 Web 信息。计数 BF 的一个值得注意的应用是在短时间内对给定网页的访问设置近似计数以检测 DDoS 攻击。

#### 10.2.3.2 压缩 BF

引入压缩 BF [146] 的目的是使 BF 可以在不同的网络节点之间作为消息传递。压缩是一种有效的技术，可以减小传输大小，而压缩 BF 可以提高网络性能。作者建议使用算术编码进行快速压缩过程。显然，开发人员在关注网络流量大的网络中优化传输大小。除了减少广播比特位数之外，假阳性率和查找成本也会降低。不幸的是，压缩和解压缩会增加处理成本。在这里，哈希函数不是针对 *m* 和 *n* 进行优化，而是针对传输大小（不一定是 *m*，而是一个压缩数组）。然而，压缩后的假阳性概率被目标最小化。

在标准 BF 中，开发者的主要关注点是通过调整 *k*（对于固定的 *m* 和 *n* 值）来尽量减少误报的概率。标准 BF 在 <math alttext="" display="inline"><mrow><msub><mi>k</mi><mrow><mi>o</mi><mi>p</mi><mi>t</mi></mrow></msub><mo>=</mo><mi>l</mi><mi>n</mi><mo stretchy="false">(</mo><mn>2</mn><mo stretchy="false">)</mo><mfrac><mi>m</mi><mi>n</mi></mfrac><mo>=</mo><mn>0.7</mn><mfrac><mi>m</mi><mi>n</mi></mfrac></mrow></math> 时进行了优化，此时每个位位置的设置为 0 或 1 的概率为 <math alttext="" display="inline"><mrow><mfrac><mn>1</mn><mn>2</mn></mfrac></mrow></math>。尽管在压缩 BF 中，选择 *k* 以使每个数组条目为 1 的概率为 <math alttext="" display="inline"><mrow><mfrac><mn>1</mn><mn>3</mn></mfrac></mrow></math>，从而产生不平衡的过滤器，包含 <math alttext="" display="inline"><mrow><mfrac><mn>1</mn><mn>3</mn></mfrac></mrow></math> 个 1 和 <math alttext="" display="inline"><mrow><mfrac><mn>2</mn><mn>3</mn></mfrac></mrow></math> 个 0，易于压缩。这一特性用于压缩 *m* 位数组并减少其传输大小。为了实现这一目标，对于较大的过滤器大小使用了较少的哈希函数，因此网络传输的比特数比标准 BF 少，同时具有较低的误报率。具体来说，在相同的比特数传输的情况下，压缩 BF 实现了比标准 BF 更低的误报率。值得注意的是，误报率降低到 <math alttext="" display="inline"><mrow><msup><mrow><mn>0.5</mn></mrow><mrow><mo stretchy="false">(</mo><mi>z</mi><mo>/</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></msup></mrow></math>，其中 *z* 是压缩后的数组大小。在此，作者们得出结论，随着过滤器大小的增加，可以最小化哈希函数的使用。表 10.2 显示了在传输中每个元素使用 8 比特时的结果，即 <math alttext="" display="inline"><mrow><mfrac><mi>z</mi><mi>n</mi></mfrac><mo>=</mo><mn>8</mn></mrow></math>。与标准 BF 类似，完全随机的哈希函数被使用，且元素的删除是不可能的。此外，较大的 *w* 值可能导致由于未使用的零的数量而产生空间浪费。因此，决定正确的 *w* 值是一个复杂的权衡，取决于应用程序的类型和数据的分布。此外，BF 的其他变体，如计数 BF，可以从这种压缩中受益。在接收节点，BF 被解压缩。显然，这种过滤器在端点处仍然需要更大的内存空间。具体而言，压缩 BF 被用于分布式节点之间的 P2P 共享。然而，具有少量计算能力和内存资源的轻量级节点可能无法处理这种复杂的算法。

### 10.2.3.3 光谱 BF

不幸的是，标准 BF 不支持多重集合，即，如果一个元素在集合中重复多次，则不允许查询该元素的重复次数。2003 年，谱 BF[65]专门设计用于支持多重集合，并且更适用于流数据。事实上，谱 BF 是计数 BF 的优化扩展。术语“谱”表示支持元素的重复次数在一个请求的频谱内。改进的查找、增强的准确性和支持删除是选择谱 BF 而不是标准 BF 的原因。与计数 BF 类似，使用的是一个*m*计数器数组而不是位向量。所有计数器都初始化为零。然而，使用计数器而不是单个位会增加空间需求。除了插入和查找操作外，谱 BF 还支持删除操作。所有这些操作的时间复杂度都是常数，即，<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math>。处理临时冰山查询、谱 Bloom 连接、提供快速的积极索引是谱 BF 的一些用例。临时冰山查询在查询时执行具有指定阈值的查询，并返回少量数据。谱 Bloom 连接的功能减少了远程数据库站点的常见轮次，同时执行连接以最小化复杂性和网络使用。此外，谱 BF 用于需要关系上频率计数查询的场景，例如，双焦采样。谱 BF 采用两种方案进行操作，即，最小增量和重复最小值。前者适用于插入和查找，而后者也支持删除。对于只需要插入和查找的序列，最小增量显示出比重复最小值更好的性能。<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>N</mi><mo stretchy="false">)</mo><mo>+</mo><mi>O</mi><mo stretchy="false">(</mo><mi>m</mi><mo stretchy="false">)</mo><mo>+</mo><mi>N</mi></mrow></math>是此数据结构的总空间需求，其中*N*是数组的总长度，*m*是插入到数组中的唯一元素的数量。现在，我们将依次讨论两种谱 BF 方案。

**最小增加**：这种方案基于一个关键的见解，即最小计数器对应于*k*个哈希函数的*k*个计数器位置具有最合适的结果，因为其他项在大型数据集中也可能被散列到相同的位置。有了这个见解，对于增量操作，只有最小值的计数器会增加，而其余的保持不变。对于一个多重集合*S*，假设<math alttext="" display="inline"><mrow><msub><mi>f</mi><mi>x</mi></msub></mrow></math>是集合中元素*x*的频率。

+   插入：在插入元素时，会计算与*k*个哈希函数对应的位置，并且只有最小值的计数器会加 1。考虑一个具有*10*个计数器值和*3*个哈希函数的谱 Bloom 过滤器，即，<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo>=</mo><mi>x</mi><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn></mrow></math>, <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo>=</mo><mo stretchy="false">(</mo><mn>2</mn><mi>x</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn></mrow></math>, <math alttext="" display="inline"><mrow><mi>h</mi><mn>3</mn><mo>=</mo><mo stretchy="false">(</mo><mn>2</mn><mo>*</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn></mrow></math>。Fig. 10.12 表示使用最小增加方案进行插入。在这里，元素 9、15、8、9、8、9 按顺序插入，插入时只有最小计数器值加 1。例如，第一次插入元素 8 时，哈希函数返回了数组位置 8、9、6，其数据分别为 1、1、0。因此，在插入 8 时，只有位置 6 的值，即 0，会加 1。但是，对于第二次插入元素 9，哈希函数返回了位置 9、1、8，其值为 1、1、1。由于所有三个位置具有相同的计数器值，因此所有位置都会加 1。

+   频率查询：对元素*x*的频率计数查询返回<math alttext="" display="inline"><mrow><msub><mi>f</mi><mi>x</mi></msub></mrow></math>。经过*k*个哈希函数处理后，返回*k*个位置中的最小值。图 10.13 表示了采用最小增量方案的查找操作。这里，查询元素 8 返回 2 作为对应于哈希函数的位置，即，8、9、6 的值分别为 3、3、2，它们的最小值为 2，因此返回频率查询结果为 2。此外，查询元素 13 返回 1，尽管它不在集合中，这显然是一个错误的阳性。

+   删除：在使用最小增量时，不推荐删除。因为在插入元素时并不是所有计数器值都会增加（只有最小计数器值会增加），所以删除操作可能会导致错误的负值。图 10.14 表示在谱布隆过滤器中执行删除时发生错误的负值。删除元素 9 将会将位置 9、1、8 的计数器值减 1，因此查询元素 8 的频率将返回 1，但实际上应该是 2，因为元素出现了 2 次。

![图 10.12](img/fig10_12.jpg)

**图 10.12。**

在谱布隆过滤器中采用最小增量方案进行插入。

![图 10.13](img/fig10_13.jpg)

**图 10.13。**

在谱布隆过滤器中采用最小增量方案的查找操作。

![图 10.14](img/fig10_14.jpg)

**图 10.14。**

在谱布隆过滤器中采用最小增量方案的删除操作。

**重复最小值：** 重复最小值使用两个不同的频谱 BF，主要（F1），次要（F2）。重复最小值的关键逻辑是，查询时遇到错误的元素具有较少的重复最小计数器值的机会。在这里，具有 *k* 个哈希函数对应的重复最小计数器值的项目在主频谱 BF 中维护，而具有唯一最小计数器值的元素在次要频谱 BF 中维护。因此，次要 BF 存储面临更高错误率的元素。尽管如此，在唯一最小情况下进行两次哈希到 BF 使得重复最小值成为一个复杂的方法。重复最小值方案支持的操作如下所述。

+   插入：要插入一个项 *x*，在主 BF 中递增相应的 *k* 计数器。接下来，检查元素 *x* 是否具有重复的最小计数器值，如果是，则继续计数器值的过程。否则，如果 *x* 具有单个最小计数器值，请在次要 BF 中检查 *x* 并递增计数器。如果在那里找不到，则将 *x* 插入到次要频谱 BF 中，其值等于从主 BF 检索到的最小计数器值。

+   频率查询：查询一个元素时，首先探测主要的 BF 并检查一个元素是否有重复的最小值，然后返回最小计数器值。否则，在次要 BF 中搜索，如果值大于零，则返回次要 BF 中的最小计数器值，如果没有，则返回主 BF 中的最小计数器值。

+   删除：要删除一个元素，首先在主 SBF 中将计数器值减 1。此外，如果它有单个最小值，则在次要 BF 中也递减其计数器值。由于一个元素同时插入了主 BF 和次要 BF，所以假阴性永远不会发生。

### 10.2.3.4 可删除的布隆过滤器（DBF）

可删除布隆过滤器（DBF）[165]被引入来解决在计数布隆过滤器中删除元素时出现的假负问题。然而，与计数布隆过滤器使用计数器数组不同，它使用了一个包含*m*位的位数组。DBF 背后的关键见解是，它试图定位在插入元素时可能发生冲突的位区域，而删除只能在无冲突的区域进行。这里，一个*m*位的位数组被分为*r*个区域，每个区域应该包含<math alttext="" display="inline"><mrow><mfrac><mrow><msup><mi>m</mi><mo>′</mo></msup></mrow><mi>r</mi></mfrac></mrow></math>位，其中<math alttext="" display="inline"><mrow><msup><mi>m</mi><mo>′</mo></msup><mo>=</mo><mi>m</mi><mo>−</mo><mi>r</mi></mrow></math>。在*m*位数组的开头，保留了一个大小为*r*的冲突位图来编码，这些*r*位被初始化为 0。冲突位图中的 1 表示冲突易发生区域，而零表示无冲突区域。在设计 BF 时的一个关键问题是选择*r*的值，因为这个值决定了 BF 删除元素和 FPR 的能力。DBF 的假阳性概率计算如下：

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>P</mi><mo>=</mo><msup><mrow><mfenced close="]" open=""><mrow><mn>1</mn><mo>−</mo><msup><mrow><mfenced close=")" open="("><mrow><mn>1</mn><mo>−</mo><mfrac><mn>1</mn><mrow><mi>m</mi><mo>−</mo><mi>r</mi></mrow></mfrac></mrow></mfenced></mrow><mrow><mi>k</mi><mo>*</mo><mi>n</mi></mrow></msup></mrow></mfenced></mrow><mi>k</mi></msup></mrow></mtd></mtr></mtable></mrow></math>(10.14)

其中，*n*是要插入的元素总数。DBF 支持的操作描述如下：

+   插入：要插入一个元素，对应于*k*个哈希函数的*k*个位置被设置为 1。如果*k*个位置中的任何一个单元格已经是 1，则表示发生了冲突，在响应此冲突时，碰撞位图中发生冲突的区域的位被设置为 1。[图 10.15 代表 DBF 中的插入。在这里，元素 15、9、8、4 被按序插入，使用 3 个哈希函数：<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo>=</mo><mi>x</mi><mi>m</mi><mi>o</mi><mi>d</mi><mn>11</mn></mrow></math>, <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo>=</mo><mo stretchy="false">(</mo><mn>2</mn><mi>x</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>11</mn></mrow></math>, <math alttext="" display="inline"><mrow><mi>h</mi><mn>3</mn><mo>=</mo><mo stretchy="false">(</mo><mn>2</mn><mo>*</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>11</mn></mrow></math>。对于元素 9，未检测到冲突，而对于元素 8，在区域 3 的第 8 个位置检测到冲突。因此，碰撞位图中的相应位被设置为 1。类似地，对于元素 4，在区域 1、2 和 3 中发生冲突，因此这些碰撞位图中的相同位置被设置为 1。

    ![图 10.15](img/fig10_15.jpg)

    **图 10.15。**

    在可删除的 BF 中的插入操作。

+   查找查询：要查询一个元素，将要查询的元素通过*k*个哈希函数，如果*k*个位置中有任何一个位置为 0，则该元素不在集合中，否则可能存在。

+   删除：要删除，在*k*个计算的哈希位置中，只重置位于无碰撞区域的位。如果所有对应哈希函数的*k*位位于碰撞区域，则该元素不可删除。因此，只有当*k*中的至少一个位可以重置为 0 时，才能删除元素。这样可以避免假负，但假正可能仍然存在。图 10.16 展示了 DBF 的删除操作。如图所示，元素 15 无法删除，因为对应的哈希位置，即 4、0、8 都位于碰撞区域，而元素 9 成功被删除，因为对应的哈希位置中第 9 和第 10 位置位于无碰撞区域。

    ![图 10.16](img/fig10_16.jpg)

    **图 10.16.**

    DBF 中的删除操作。

### 10.2.3.5 稳定 BF

不幸的是，BF 中零的计数随时间减少，到达一定时点时，所有查询都被回答为可能存在于集合中。SBF 的引入是为了消除流数据中的重复项，并在错误达到预定义阈值之前驱逐过时数据。稳定 BF 为更新的数据创建了空间，因为这些数据比旧数据更重要。与计数 BF 类似，这里使用*d*位计数器数组，所有计数器初始化为 0。因此，最大计数器值可以达到<math alttext="" display="inline"><mrow><msup><mn>2</mn><mi>d</mi></msup><mo>−</mo><mn>1</mn></mrow></math>。为了处理过时数据，稳定 BF 清除过时数据以为新数据创建空间。查询处理、URL 抓取、监视不同 IP 地址、图处理是稳定 BF 的一些应用。

+   插入：要插入一个项，需要通过*k*个哈希函数。在某个点上，当零的数量变得恒定时，更新稳定 BF。要更新，随机减少*p*计数器值 1。在这一步之后，所有*k*个计算出的哈希位置被设置为最大值。

+   检查重复性：要检查重复值，查询并检查*k*个哈希单元是否哈希为 0 或 1。对于任何一个单元返回 0 的情况，集合中不存在重复项，否则存在重复性。然而，随机将位设置为 0 可能导致错误负值。这里，错误负值定义为当查询重复项时被回答为不同的情况。另外，错误负值取决于输入数据分布。对于没有前任的元素，错误负值的机会为零。

此外，稳定 BF 保证了 FPR 的严格上限，同时由于随机逐出过时信息而引入了错误负值。设置*p=0*和*d=1*，稳定 BF 的行为类似于 SBF。图 10.17 表示*p=2*和*d=3*的情况。

![图 10.17](img/fig10_17.jpg)

**图 10.17.**

理解稳定 BF。

### 10.2.3.6 修正的 Bloom 过滤器（RBF）

减少假阳性的一种方法是增加位向量的大小。然而，这种方法可能会增加内存使用量。Donnet 等人引入了另一种从过滤器中减少 FPR 的 BF 变种，并命名为 RBF。该过滤器还增强了系统的灵活性。在这里，试图从过滤器中删除更为麻烦的假阳性。然而，这种方法引入了随机假阴性。在构建 BF 之后但在其被使用之前，试图识别出假阳性。经过调整的 BF 通过与引入一些假阴性的权衡来随机移除一些假阳性。值得注意的是，在标准 BF 中不会发生假阴性。

RBF 通过将位向量中的一些选定位重置为 0 来降低 FPR。这个 RBF 的过程被称为位清除过程。显然，对于一个元素，如果位清除过程中任何位置对应于 *k* 个哈希函数的位置都被重置为 0，则会导致假阴性。位清除过程可以是随机的或有选择性的。RBF 的结果被总结在一个度量 *χ* 上。如果这个度量的值大于 1，则意味着删除的假阳性比例高于生成的假阴性比例，而小于 1 的值表示删除的假阳性比例低于生成的假阴性。

+   随机位清除 RBF：在随机位清除过程中，随机地将一些位重置为 0，尽管这些位是否重置为 0 的逻辑是不确定的。对于随机位清除过程，观察到 *χ* 的值计算为 1，这意味着系统的整体错误率得以维持。

+   选择性位清除 RBF：与随机位清除不同，只有那些导致假阳性的位被重置为零。选择性清除过程有 4 种算法可以进行，如下所讨论：

    +   随机选择：第一个是随机选择，对选择性清除过程不需要任何智能。在这里，与随机位清除过程不同，位向量中不是随机重置位，而是只有一个位可以被重置，该位与麻烦键的假阳性有关。

    +   最小误负选择：在这里，目标是减少选择性清除过程中产生的假负的概率。这通过在本地设置一个计数向量来处理，该向量存储记录元素的数量。此算法考虑了在位向量中哈希键和属于集合的元素的哈希键之间的哈希碰撞的可能性。这种算法的缺点是估计过高。

    +   最大假阳性选择：此算法旨在删除最大假阳性。对于以前未删除的每个令人困扰的键，从*k*个哈希键中选择要重置的位置，以减少假阳性的数量。

    +   比例选择：最后一个算法是比例选择，它是最小误负选择和最大假阳性选择算法的组合。这也旨在最小化生成的假阴性并最大化假阳性的移除。

选择性清除过程使假阳性率大大降低，而生成的假阳性数量增加的程度小。显然，RBF 会增加键移除的额外处理成本，这个成本是 RBF 参数的倍数，比如哈希函数的数量。有关更多细节和涉及的数学内容，用户可以参考[73]。

### 10.2.3.7 动态布隆过滤器

正如之前提到的，Bloom Filter（BF）不适用于动态集合，即其大小随时间变化的集合。静态集合无法通过标准 BF 执行添加和删除操作。BF 只对事先已知大小的集合有效。此外，在 BF 中，目标 FPR 阈值是在了解总元素大小之后计算的。对于那些没有关于集合基数上限的任何信息的应用程序而言，很难决定 BF 的大小。如果元素数量超过集合大小的阈值，SBF 会变得非常不成功，因为会出现太多的误报。此外，在分布式应用场景中，网络上的所有节点必须采用相似的配置，以实现节点之间标准 BF 的互操作性。为了处理这种情况，如果即使一个节点的基数大小超过了阈值，所有节点都会重建它们的 BF。对于大多数独立应用程序，对于动态集合，这些应用程序具有关于总元素数量的上限的先验信息，将分配比已知上限更大的空间，以便可以表示所有项目。然而，这种方法会降低标准 BF 的空间效率。

解决标准 BF 问题的一个解决方案是引入了动态 BF。对于独立应用，动态 BF 可以按需插入项目。对于分布式应用程序，动态 BF 处理节点之间的互操作性问题，因为它消耗适当的内存以减少不必要的浪费和传输开销。此外，它控制错误匹配概率的速率，即使元素数量增加也能保持在可接受的水平。在动态 BF 中，误报概率称为错误匹配概率。值得注意的是，动态 BF 也可以支持静态集合。在这里，如果错误概率低于预定义的上限，则 BF 称为“活动”，否则称为满。动态 BF 由*s*个同质标准 BF 组成。*s*的初始值为 1，并且处于活动状态。元素的插入只能在活动 BF 中进行，当前一个活动 BF 满时，会在其后附加一个新的 BF。图 10.18 代表了动态 BF 的数据结构。设*NR*为添加到 BF 的元素计数。然而，动态 BF 的初始化值为动态 BF 的错误匹配概率上限，*s*的最大值，标准 BF 的错误概率上限，每个标准 BF 的过滤器大小*m*，即最多可存储的项目数。要创建动态 BF，请使用上述参数初始化一个标准 BF。动态 BF 支持的操作如下所述：

+   插入：要插入一个元素，首先从给定的动态布隆过滤器中找到活动布隆过滤器。如果当前的布隆过滤器不活跃，则使用下一个布隆过滤器作为新的活动布隆过滤器，并将 *s* 的值增加一。通过 *k* 个哈希函数传递元素，并将元素插入当前活动的布隆过滤器中。然后增加当前布隆过滤器的 *NR* 值。在多次插入后，当元素数量超过容量阈值 *c*，即 *NR <math alttext="" display="inline"><mo>></mo></math>* c 时，将附加一个新的布隆过滤器，并将这个新创建的布隆过滤器称为活动布隆过滤器。一次只有一个布隆过滤器是活动的，其余的是不活跃的。插入操作的时间复杂度为 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>k</mi><mo stretchy="false">)</mo></mrow></math>。

+   查找查询：通过 *k* 个哈希函数传递项目来搜索项目。如果动态布隆过滤器中存储的任何一个返回 true，则元素可能存在于集合中；否则，如果所有的布隆过滤器返回 false，则元素绝对不存在于集合中。查找查询的时间复杂度为 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>k</mi><mo>*</mo><mi>s</mi><mo stretchy="false">)</mo></mrow></math>。

+   删除：动态布隆过滤器中的删除有些困难。要删除，首先使用上述查找查询操作在动态布隆过滤器中检查元素是否存在。如果元素不存在，则拒绝删除元素。如果查找查询的结果对单个布隆过滤器为正，则将相应的 *k* 位重置为 0，否则如果多个布隆过滤器返回 1，则动态布隆过滤器不会删除元素，以防止出现误删除。删除操作的时间复杂度为 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>k</mi><mo>*</mo><mi>s</mi><mo stretchy="false">)</mo></mrow></math>。

![图 10.18](img/fig10_18.jpg)

**图 10.18.**

动态布隆过滤器的数据结构。

### 10.2.3.8 布谷过滤器

类似于 BF，布谷过滤器[78]提供了快速的成员查询和出色的空间效率。此外，布谷过滤器支持删除、有限计数，并具有相同的空间复杂度。布谷过滤器基于布谷哈希的概念。布谷哈希以其处理基于哈希的数据结构碰撞的卓越性而闻名。在布谷哈希中，使用一个布谷哈希表，其中包括一个桶数组，假定要插入一个项。这里，每个表分别使用两个哈希函数。每个项都使用两个不同的哈希函数进行哈希处理，并且每个哈希函数都索引到一个桶。该项存储在两个桶中的任意一个中。首先尝试将项存储在第一个桶中，如果那里没有存储任何内容，则如果第二个桶中对应的位置为空，则将项存储在第二个桶中。如果第二个桶不为空，则在替代哈希索引中逐出并重新插入第二个桶中的项。接下来，元素放置在空位置中。显然，此过程面临将旧键位置替换的问题。如果旧键的备用哈希位置为空，那么重新定位就相当容易，否则，旧键必须替换另一个键。重复此过程直到找到一个空的桶为止。如果此情况导致循环，则会选择全新的哈希函数，并且整个数据结构会被重新构造。因此，插入的摊销复杂度为*O(1)*。查询过程会探测两个桶以检查项的存在。图 10.19 代表了依次插入元素 20、50、53、75、100、67、105、3、36、39 的过程。

![图 10.19](img/fig10_19.jpg)

**图 10.19.**

布谷哈希中的插入。

由其指纹和桶大小确定的布谷鸟过滤器。例如，*(3,5)* 过滤器表示 3 位长度的过滤器，每个桶可以存储 5 个指纹。总结认为，如果目标假阳率小于 3%，则布谷鸟过滤器消耗的空间比标准 BF 少。即使过滤器的空间使用了 95%，布谷鸟过滤器的成员查询性能也优于标准 BF。然而，仅存储指纹而不是实际项会阻止使用标准布谷鸟哈希进行插入。在这里，现有的指纹必须重新定位到替代位置，而不是实际项。布谷鸟过滤器的操作如下所述：

+   插入：在这里，问题是如何恢复和重新散列原始项以定位到替代位置？为了解决这个问题，布谷鸟过滤器采用了”部分键布谷鸟哈希”来从指纹中找到项目的替代位置。在这里，对于一个项目*x*，两个哈希桶的索引计算如下：<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> 和 <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo>=</mo><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mi>f</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow></math>。通过使用 XOR 操作，确保了可以使用<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math>和*x*的指纹来计算<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math>。因此，要将键从计算得到的<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math>或<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math>的位置之一重新定位到替代位置，通过公式<math alttext="" display="inline"><mrow><mi>j</mi><mo>=</mo><mi>i</mi><mo>⊕</mo><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mi>f</mi><mo stretchy="false">[</mo><mi>i</mi><mo stretchy="false">]</mo><mo stretchy="false">)</mo></mrow></math>计算替代位置，其中*i*是项目最初存储的桶的索引位置，*j*是替代桶的索引。通过这个过程，不需要项目*x*的原始值。考虑一个布谷鸟过滤器，每 10 个桶有两个条目，如图 10.20 所示。要计算项目*x*的索引位置，请使用<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo>=</mo><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math>和<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo>=</mo><msub><mi>i</mi><mn>1</mn></msub><mo>⊕</mo><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mi>f</mi><mo stretchy="false">)</mo></mrow></math>。假设<math alttext="" display="inline"><mrow><msub><mi>i</mi><mn>1</mn></msub></mrow></math>和<math alttext="" display="inline"><mrow><msub><mi>i</mi><mn>2</mn></msub></mrow></math>是从这些哈希函数计算得到的索引。此示例使用移位折叠方法计算项目*x*的指纹<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>f</mi><mo stretchy="false">)</mo></mrow></math>，并且*x*的哈希值通过*xmod*10 计算。要处理碰撞，随机选择<math alttext="" display="inline"><mrow><msub><mi>i</mi><mn>1</mn></msub></mrow></math>或<math alttext="" display="inline"><mrow><msub><mi>i</mi><mn>2</mn></msub></mrow></math>（假设*i*），并使用公式<math alttext="" display="inline"><mrow><mi>j</mi><mo>=</mo><mi>i</mi><mo>⊕</mo><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mi>f</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow></math>将桶*i*处的指纹移到替代桶*j*。在插入时可能存在以下情况：

    *Case1: 插入(131)*

    +   (a)使用移位折叠方法计算指纹*f*，*f*= 13+1 = 14。

    +   (b)<math alttext="" display="inline"><mrow><msub><mi>i</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> = <math alttext="" display="inline"><mrow><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> = <math alttext="" display="inline"><mrow><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mn>131</mn><mo stretchy="false">)</mo></mrow></math> = 131*mod*10 =1

    +   (c)<math alttext="" display="inline"><mrow><msub><mi>i</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mn>1</mn><mo>⊕</mo><mo stretchy="false">(</mo><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mn>14</mn><mo stretchy="false">)</mo><mo stretchy="false">)</mo><mo>=</mo><mn>1</mn><mo>⊕</mo><mo stretchy="false">(</mo><mn>14</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo stretchy="false">)</mo><mo>=</mo><mn>1</mn><mo>⊕</mo><mn>4</mn><mo>=</mo><mn>5</mn></mrow></math>

    +   (d)由于索引 1 可用，在相同位置插入*f*。

    *Case 2: 插入(1111)*

    +   (a)<math alttext="" display="inline"><mrow><mi>f</mi><mo stretchy="false">(</mo><mn>1111</mn><mo stretchy="false">)</mo><mo>=</mo><mn>11</mn><mo>+</mo><mn>11</mn><mo>=</mo><mn>22</mn></mrow></math>

    +   (b)<math alttext="" display="inline"><mrow><msub><mi>i</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mn>1111</mn><mo stretchy="false">)</mo><mo>=</mo><mn>1111</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>1</mn></mrow></math>

    +   (c)<math alttext="" display="inline"><mrow><msub><mi>i</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mn>3333</mn><mo stretchy="false">)</mo><mo>=</mo><mn>1</mn><mo>⊕</mo><mo stretchy="false">(</mo><mn>22</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo stretchy="false">)</mo><mo>=</mo><mn>1</mn><mo>⊕</mo><mn>2</mn><mo>=</mo><mn>3</mn></mrow></math>

    +   (d)由于索引 1 和 5 均被占用，这表示发生了碰撞情况。

    +   (e)随机选择 <math alttext="" display="inline"><mrow><msub><mi>i</mi><mn>1</mn></msub></mrow></math> 或 <math alttext="" display="inline"><mrow><msub><mi>i</mi><mn>2</mn></msub></mrow></math> 并将指纹从所选位置移动到其他桶中。假设选择了 <math alttext="" display="inline"><mrow><msub><mi>i</mi><mn>1</mn></msub></mrow></math>，那么 <math alttext="" display="inline"><mrow><mi>j</mi><mo>=</mo><msub><mi>i</mi><mn>1</mn></msub><mo>⊕</mo><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mi>f</mi><mo stretchy="false">[</mo><msub><mi>i</mi><mn>2</mn></msub><mo stretchy="false">]</mo><mo stretchy="false">)</mo><mo>=</mo><mn>1</mn><mo>⊕</mo><mo stretchy="false">(</mo><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mi>f</mi><mo stretchy="false">[</mo><mn>1</mn><mo stretchy="false">]</mo><mo stretchy="false">)</mo><mo stretchy="false">)</mo><mo>=</mo><mn>1</mn><mo>⊕</mo><mo stretchy="false">(</mo><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo stretchy="false">(</mo><mn>14</mn><mo stretchy="false">)</mo><mo stretchy="false">)</mo><mo>=</mo><mn>1</mn><mo>⊕</mo><mn>4</mn><mo>=</mo><mn>5</mn></mrow></math>。

        ![图 10.20](img/fig10_20.jpg)

    **图 10.20.**

    在杜鹃过滤器中插入。

+   查找：对于项目*x*，首先计算*x*的指纹和桶的两个索引。接下来，读取这两个位置的内容。如果匹配，则过滤器返回 true，否则返回 false。这样可以避免假阴性，因为没有溢出。如果两个元素具有相同的指纹并且哈希索引也相同，则可能发生假阳性。显然，这个过程的时间复杂度为<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math>。然而，当过滤器填满时，FPR 会变高。

+   删除：要删除一个项目，首先按照查找查询的相同过程查找要删除的元素。如果没有匹配，删除不可能进行，否则如果有匹配，只需从桶中删除该指纹的副本。为了避免“错误删除”，元素的条目不会被清除。有了这个洞察力，删除后过滤器的假阳性性质保持不变。这个过程的时间复杂度为<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math>。

然而，与布谷鸟哈希不同的是，过滤器中仅存储指纹而不是原始值。每个元素都存储在一个*f*位的指纹中。布谷鸟过滤器消耗的空间由等式 10.15 给出，其中，*ϵ*指定了 FPR，*α*是过滤器的最大容量，*B*是每个桶的条目数。

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mfrac><mrow><mi>l</mi><mi>o</mi><msub><mi>g</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mfrac><mn>1</mn><mi mathvariant="normal">ϵ</mi></mfrac><mo stretchy="false">)</mo><mo>+</mo><mi>l</mi><mi>o</mi><msub><mi>g</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mn>2</mn><mi>B</mi><mo stretchy="false">)</mo></mrow><mi>α</mi></mfrac></mrow></mtd></mtr></mtable></mrow></math>（10.15）

### 10.2.3.9 分层 BF

在网络术语中，归因被定义为查找某些流量的源和目的地的过程。然而，有时这个过程很困难，因为缺乏日志记录机制，例如，攻击者可能使用僵尸机器欺骗地址。分层 BF 促进了有效负载归因过程，其中给定有效负载，目标是识别给定有效负载的发送者或接收者。这对于检测某些安全攻击，如 DDoS、欺骗，可能是有益的。Shanmugasundarm 等人[168]基本上扩展了 BF 以支持子字符串匹配。作为一个优势，这个算法甚至不需要完整的数据包来进行归因，只需要一个重要的部分就足够了。除此之外，该算法需要较低的存储要求，并且通过仅存储有效负载的哈希而不是实际有效负载来确保数据的隐私。

这里，长度为*p*的每个数据包的有效负载首先被分成大小为*s*的*q*个多个块的集合。每个块都附带其偏移值。接下来，对每个带有其偏移值的块进行哈希处理，并插入标准 BF。这种数据结构被称为带偏移的基于块的 BF，如图 10.21 所示。

![图 10.21](img/fig10_21.jpg)

**图 10.21.**

分层 BF。

### 10.2.3.10 随机公平蓝色

尽管作者并未将此数据结构定义为 BF 的变体，但它与 BF 的工作方式非常相似。随机公平蓝（SFB）[81]是一种利用计数 BF 以及蓝色算法的技术。作者提出了这个方案，以解决 TCP 的拥塞控制问题。它检测重要流量以提高组播数据包的转发速度。SFB 使用*N*k*个存储桶，其中*k*是级别数量，每个级别都有*N*个存储桶，以及*k*个哈希函数。此外，每个存储桶都关联一个丢弃/标记概率<math alttext="" display="inline"><mrow><msub><mi>p</mi><mi>m</mi></msub></mrow></math>。对于每个传入的数据包，将其连接 ID（源-目的地地址对、源-目的地端口对和协议）应用*k*个哈希函数，并增加相应的桶位置。如果哈希到一个桶的数据包计数超过了桶的最大大小，那么增加<math alttext="" display="inline"><mrow><msub><mi>p</mi><mi>m</mi></msub></mrow></math>的值，其值为<math alttext="" display="inline"><mrow><msub><mi>δ</mi><mn>1</mn></msub></mrow></math>；否则，在链接空闲时，将其值减小<math alttext="" display="inline"><mrow><msub><mi>δ</mi><mn>2</mn></msub></mrow></math>。如果<math alttext="" display="inline"><mrow><msub><mi>p</mi><mi>m</mi></msub></mrow></math>的值达到 1，则将数据包放入重要流量列表中。为了降低 FPR，作者使用了保守更新的思想。对于一个数据包，在对应的*k*个哈希位置中提取<math alttext="" display="inline"><mrow><msub><mi>p</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi></mrow></msub></mrow></math>。现在，如果<math alttext="" display="inline"><mrow><msub><mi>p</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi></mrow></msub></mrow></math>的值等于 1，则将数据包标记为重要流量，然后将其丢弃。因此，使用 BF 可以轻松检测到重要流量，而且每个数据包的空间和操作次数都较少。

图 10.22 展示了随机公平蓝色的一个示例。如图所示，数据包<math alttext="" display="inline"><mrow><msub><mi>p</mi><mi>x</mi></msub></mrow></math>被映射到了所有箱子中的较高位置。<math alttext="" display="inline"><mrow><msub><mi>p</mi><mi>m</mi></msub></mrow></math>。然而，数据包<math alttext="" display="inline"><mrow><msub><mi>p</mi><mi>y</mi></msub></mrow></math>可能在同一级别的同一个箱子中与重要的流相同，但在其他级别中，它将映射到普通箱子中。由于数据包<math alttext="" display="inline"><mrow><msub><mi>p</mi><mi>y</mi></msub></mrow></math>的<math alttext="" display="inline"><mrow><msub><mi>p</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi></mrow></msub></mrow></math>为<math alttext="" display="inline"><mrow><mn>0.2</mn><mtext>\textless</mtext><mn>1</mn></mrow></math>，因此被识别为普通流，而<math alttext="" display="inline"><mrow><msub><mi>p</mi><mi>x</mi></msub></mrow></math>被标记为重要流。

![图 10.22](img/fig10_22.jpg)

**图 10.22.**

随机公平蓝色的示例。

## 10.3 商数过滤器

BF 后，商数过滤器（QF）[40]在程序员中流行，用于检查近似成员查询（AMQ），即它还检查元素是否属于集合。 QF 是一种基于商数技术的缓存友好型方案[120]，甚至在主存储器之外提供可扩展性。与 BF 类似，成员查询结果回答“可能在集合中”或“绝对不在集合中”，因为 QF 也会产生误报错误。增加过滤器大小可以显著降低查询的错误概率，而将更多元素插入集合中则可能增加误报率。但是，对于任何查询结果都不会生成假阴性。AMQ QF 的典型用例是存储在磁盘上的数据库表。对存储在磁盘上的数据库的任何访问都将首先检查 QF 以获取特定键。如果过滤器返回积极结果，则访问磁盘，否则不访问。

仅当 BF 存储在主内存中时，才提供有益。当 BF 大小过大时，其性能显著降低。另一个选择是将 BF 存储在磁盘上，但是由于使用了多个哈希函数，此方法需要太多随机访问磁盘。此外，此方法将执行多个输入输出操作。此外，如果 BF 大小远大于内存缓冲区大小，则内存缓冲技术无法提供可扩展性。另一方面，QF 将元素数据存储得非常接近，以避免多个随机访问。借此洞察力，QF 使用单个哈希函数并提供了解决高碰撞概率的方法。然而，QF 占用的空间比 BF 大 20%。

QF 对哈希表的概念非常着迷，其中不仅存储实际元素，而且存储元素的哈希值以及一些元数据位。额外的元数据位用于处理碰撞。QF 支持插入、查找、删除、合并、调整大小等操作。要执行 QF 操作，首先将元素*x*通过单个哈希函数传递，该函数将生成*p*位指纹。指纹进一步分为两部分：余数部分，其中包含*r*个最低有效位，以及商部分，其中包含*q*个最高有效位。采用的哈希表总共有 2^q 个槽，而任何元素的余数部分都存储在由商索引的位置。如果不同值的元素散列出相似的指纹，则会发生硬碰撞，而如果两个不同值的指纹具有相同的商但不同的余数，则会发生软碰撞。

假设元素*k*生成指纹*kf*，并在分区后让其余数为*KR*，商为*KQ*。如果*KR*正好存储在槽*KQ*中，那么该槽被称为规范槽。对于软碰撞，*KR*存储在排序顺序中*KQ*右侧的下一个可用槽。插入算法确保所有具有相同商位的指纹都以连续方式存储，并形成一组运行。还可能出现一种情况，即运行的第一个指纹可能不会存储在其规范槽中，因为它可能会与已存储的某个不同商的余数位相移。具有其第一个指纹存储在规范槽中的运行指的是簇的开始。一个簇可能包含多个结束于空槽或其他簇的开始的运行。除了元素的指纹外，槽中还存储了三个额外位，如图 10.23 所示。这些位的功能如下所述：

+   *is_occupied*：如果设置了此位，则意味着此槽位是过滤器中某个插入元素的规范槽位。可能的情况是，键不存储在其规范槽位中，而是存储在过滤器的其他位置。

+   *is_continuation*：如果设置了此位，则意味着槽位被某个余数占用，但绝对不是运行的第一个余数。

+   *is_shifted*：如果设置了此位，则意味着槽位保存的是不在其规范槽位中的余数。

但是，带有元数据位的 QF 比 BF（但少于计数 BF）消耗的空间多 20%，用于相同数据大小。此外，查找操作的吞吐量减慢 3 倍。唯一可能发生误报的情况是发生硬碰撞时，其概率如下所示：<math alttext="" display="inline"><mrow><mn>1</mn><mo>−</mo><msup><mi>e</mi><mrow><mfrac><mrow><mo>−</mo><mi>α</mi></mrow><mrow><msup><mn>2</mn><mi>r</mi></msup></mrow></mfrac></mrow></msup></mrow></math>，其中 *α* 被定义为总元素和槽位数的比例。插入新元素时，其槽位被标记为占用，并相应地更新其他位。不同附加位组合的重要性在 Table 10.4 中指定。QF 的操作如下所述：

![Figure 10.23](img/fig10_23.jpg)

**图 10.23.**

QF 的结构。

**表 10.4**

可能的元数据位组合的重要性。

| 1 | 2 | 3 | 解释 |
| --- | --- | --- | --- |
| 0 | 0 | 0 | 此槽位为空 |
| 0 | 0 | 1 | 这是一次运行的开始，并且余数已经从其规范槽位中移出。 |
| 0 | 1 | 0 | 此组合未被使用。 |
| 0 | 1 | 1 | 此余数不是运行中的第一个余数，并且它已经从其规范槽位中移出。 |
| 1 | 0 | 0 | 这是运行中的第一个余数，也在规范槽位中。 |
| 1 | 0 | 1 | 这是持有已从其规范槽位移出的第一个余数的连续序列。此外，意为此槽位的连续序列已向右移动。 |
| 1 | 1 | 0 | 此组合未被使用 |
| 1 | 1 | 1 | 此余数不是已从其规范槽位移出的连续序列中的第一个余数。此外，意为此槽位的连续序列已向右移动。 |

1：is_occupied，2：is_continuation，3：is_shifted

**查找**：要查询任何元素*k*，请按照以下步骤进行。

+   对键进行哈希处理以生成其指纹*kH*。

+   接下来，将*kH*分为商*kQ*和余数*kR*。很明显，元素*k*的规范槽位是*kQ*。如果规范槽位的所有元数据位都为 false，则意味着槽位未被占用。因此，元素明确不存在于集合中。

+   如果*kQ*被占用，则定位*k*的连续序列。正如前面提到的，具有相同商的余数被连续存储，它形成一个连续序列。连续序列中的第一个元素可能不在规范槽位上，如果整个连续序列已被左侧的另一个连续序列向右移动。因此，要定位商序列，首先要定位集群的起始位置，然后找到在集群中跳过的连续序列的数量以达到*kR*的连续序列。为此：

    +   向左扫描以定位集群的起始位置。如果*kQ*左侧的槽位的*is_shifted*为 false，则意味着集群的起始位置。

    +   向右扫描以跟踪一个计数器，该计数器计算要跳过的连续序列的数量以达到商序列。设置为 1 的*kQ*左侧的槽位意味着另一个要跳过的连续序列。对于*is_occupied*的每个值为 1 的情况，增加计数器的值，并在*is_continuation*清除时减去 1（意味着另一个连续序列的开始），直到计数器的值达到零。当计数器的值变为零时，意味着商序列已经达到。

+   接下来，将与 *kR* 运行对应的余数进行比较。如果匹配，则元素 *k* 可能存在于集合中，否则肯定不在过滤器中。

    **插入：**

+   将要插入的元素 *k* 通过哈希函数传递以计算其指纹。首先，通过上述描述的查找过程确保密钥尚未插入到过滤器中。如果尚未插入，则按照下一步操作。

+   当元素按运行顺序插入时，始终以排序顺序进行。即使它们属于同一运行，元素余数可能必须在任何槽中向右移动，并相应地更新元数据位。但是，此移位不会更改 *is_occupied* 位的值。

+   如果在已存在的运行的开头插入了余数，则会导致任何先前的余数向右移动到下一个可用的槽，并响应地设置其 *is_continuation* 位。如果移动了余数，则还必须重置 *is_shifted*。

要理解 QF，请考虑一个商大小为 4 且余数大小为 28 的示例。让雇用的哈希函数生成 32 位哈希。首先，将元素 *144, 133, 4033* 加入到 QF 中，如 图 10.24 (a) 所示。所有 3 个元素的插入都在规范槽中进行，因为这些槽未被占用。

![图 10.24](img/fig10_24.jpg)

**图 10.24.**

在 QF 中插入元素。

接下来，添加元素 9999。该元素的规范槽已被占用。观察到 *is_shift* 和 *is_continuation* 位未设置，这意味着它是集群的开头并且运行已开始。元素 999 的余数大于元素 144 的余数，因此应将其存储在元素 144 的右侧，即槽 2，并设置其 *is_shifted* 和 *is_continuation* 位。在插入元素 9999 后，QF 的变化反映在 图 10.24 (b) 中。

接下来，要添加元素 14023。由于槽 2 已在使用中，但其*is_occupied*位为 0。因此，元素 14023 必须存储到右侧的下一个可用槽，即槽 3，并为槽 3 设置*is_shifted*位。同时，为元素 14023 的规范槽 2 设置*is_occupied*位。插入元素 14023 后 QF 的状态如图 10.24（c）所示。

最后，将元素 55 添加到 QF 中，经过哈希函数生成 0*x*10000001。由于规范槽 1 不空闲。槽 1 的*is_shifted*和*is_continuation*位值为 0，这意味着它是集群的起始，也是运行的开始。元素 55 的余数比元素 144 的余数小。因此，槽 1 中的现有余数应向右移动到槽 2，并相应地设置*is_continuation*和*is_shifted*位。插入元素 55 后 QF 的状态如图 10.24（d）所示。

现在，考虑查找元素 4045 的查询。假设*f(4045)* = 733433CD。由于规范槽 7 已被占用。*is_occupied*、*is_continuation*和*is_shifted*的值表明它既是集群的开始，也是运行的开始。参见图 10.24（d）。右侧的下一个槽，即 8 是空的，这表明槽 7 本身是运行的起始和结束。接下来，将元素 4045 的余数与槽 7 中的现有余数进行比较。由于两个值不匹配，因此该元素肯定不在其中。

接下来，考虑查询 133 的情况，其指纹值为 48921258\. 可以观察到槽 4 已经被占用。同时，其 *is_shifted* 位的值为 1，这意味着对应当前余数的元素已存储在其规范槽中并且已被移动。*is_canonical* 位的值为 1 表示存在此槽的规范槽但已被向右移动的运行。为了找到簇的起始位置，从槽 4 开始向左扫描，并寻找 *is_shifted* 为 false 的槽，发现是槽 1\. 因此，槽 1 表示簇的起始位置。接下来，定位商的运行，从槽 4 开始向左扫描并检查 *is_occupied*。如果 *is_occupied* 位的值为 1，则意味着还有另一个运行需要跳过。有 3 个这样的槽，即 1、2 和 4，这表示元素 4033 的第三个运行在簇中。通过 *is_continuation* 位的值为 false 检测当前运行的起始和前一个运行的结束。第一个运行位于索引 1，第二个位于索引 4，第三个位于索引 5\. 因此，索引 5 是元素 4033 的商运行起始位置。现在，将索引 5 处商运行中存储的余数与问题中的元素的余数进行比较。然而，在该运行中只有一个槽。因此，将元素 4033 的余数与槽 5 处的现有余数进行比较。由于匹配，因此得出结论，元素 4033 可能在集合中。

**算法 1** 商技术

**输入：** 指纹 f

**输出：** 商 f[q] 和余数 f[r]

1: f[r]←f mod 2^r

2: **2:** 返回 f[q]，f[r]

**算法 2** 查找运行

**输入：** 规范桶索引 f[q]

1: i ← f[q]

2: **当** QF[i].is_shifted=1 **时**

3:i←i−1

4: **结束当**

5: run[start]← i

6: **当** i≠f[q] **时**

7:**重复**

8:run[start]← runstart+1

9:**直到** QF[run[start]].is_continuation ≠1

10:**重复**

11:i←i+1

12:**直到** QF[i].is_occupied=1

13: **结束当**

14: run[end]←run[start]

15: **重复**

16:run[end]← run[end]+1

17: **直到** QF[runend].is_continuation ≠1

18: **返回** run[start], run[end]

**算法 3** 测试 QF 中的元素

**输入**: 元素 *x*, 哈希函数 *h*

**输出**: 正面为真，负面为假

1: f←h(x) f[q], f[r]←f

2: **如果** QF[fq.is_occupied≠1 ] **那么**

3:返回 假

4: **否则**

5:run[start], run[end]← **查找(f[q])** 

6:**对于** i← run[start] 到 runend **执行**

7:**如果** QF[i] =f[r] **那么**

8:返回 真

9:**结束如果**

10:**结束循环**

11:返回 假

12: **结束如果**

## 10.4 跳跃表

Skip list 采用类似链表的结构。然而，链表中搜索操作的最坏时间复杂度为 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>，因为在搜索时列表是线性遍历的，而在 skip list 中，时间复杂度为 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><mi>g</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math>。对于一组唯一元素 *S*，skip list 被定义为链表序列 *S0*、*S1*、*S2*，……，*Sh*。较低的列表（基本列表）高度为 0，假定该列表按非递减顺序包含集合 *S* 的所有元素。此外，每个列表 *Sl <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>l</mi><mo>=</mo><mn>0</mn><mo>,</mo><mn>1</mn><mo>,</mo><mn>2</mn><mo>,</mo><mn>......</mn><mo>,</mo><mi>h</mi><mo stretchy="false">)</mo></mrow></math>* 包含特殊项目 <math alttext="" display="inline"><mrow><mo>−</mo><mi>∞</mi></mrow></math> 和 <math alttext="" display="inline"><mrow><mo>+</mo><mi>∞</mi></mrow></math>。系列中的每个连续链表容纳来自上一个列表的子集，选择子集的方式定义了链表的类型，即确定性或概率性。任何元素都以概率 *p* 插入到新层中，其中 *p* 是 <math alttext="" display="inline"><mrow><mfrac><mn>1</mn><mn>2</mn></mfrac></mrow></math>。对于概率性（或随机）skip list，使用随机硬币翻转来构造每个更高级别的元素，而在确定性（或完美）skip list 中，每个更高级别由来自即时下一个列表的 <math alttext="" display="inline"><mrow><mfrac><mn>1</mn><mn>2</mn></mfrac></mrow></math> 元素组成。在概率性跳表中，每个元素被添加到下一个级别的概率为 <math alttext="" display="inline"><mrow><mfrac><mn>1</mn><mn>2</mn></mfrac></mrow></math>。由于本章主要讨论 PDS，为简洁起见，重点放在概率性跳表上。与其他数据结构不同，跳表不使用哈希，但仍被视为概率性数据结构，因为它基于概率概念构建了跳表原始层上面的后续层。跳表数据结构的名称之所以被称为跳表，是因为更高级别跳过了较低列表中的一些元素。跳表的操作定义如下：

+   搜索：要开始搜索项目*i*，从左侧最顶部列表的最左边项目开始，即在任何情况下都是<math alttext="" display="inline"><mrow><mo>−</mo><mi>∞</mi></mrow></math>。在任何当前位置（称为*p*），将要搜索的项目*i*与*p*的右侧紧邻项目进行比较，并将该元素存储在一个新变量中，称为*v*，即<math alttext="" display="inline"><mrow><mi>v</mi><mo>←</mo><mo stretchy="false">(</mo><mi>E</mi><mo stretchy="false">(</mo><mi>r</mi><mo stretchy="false">(</mo><mi>p</mi><mo stretchy="false">)</mo><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow></math>，然后执行以下操作：

    +   如果<math alttext="" display="inline"><mrow><mi>i</mi><mo>=</mo><mi>v</mi></mrow></math>，则返回*v*。

    +   否则，如果（<math alttext="" display="inline"><mrow><mi>i</mi><mtext>\textgreater</mtext><mi>v</mi></mrow></math>），则向右移动一步，如果<math alttext="" display="inline"><mrow><mi>i</mi><mtext>\textless</mtext><mi>v</mi></mrow></math>，则向下移动一步，并将其与其右侧最右边的项目进行比较。重复相同的过程，直到没有向下的选项，这表明项目不在列表中。

    表示元素 80 的搜索过程在图 10.25 中。对于*n*个元素，跳表的搜索时间复杂度为<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><mi>g</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math>，因为在每个级别，项目数量都减半。

    ![图 10.25](img/fig10_25.jpg)

    **图 10.25。**

    在跳表中进行搜索。

+   插入：要插入一个项目，请按照以下步骤操作：

    +   首先按照搜索算法找到底层元素的位置。

    +   接下来，抛出一个偏向正面的硬币多次，直到遇到尾部。观察在遇到尾部之前出现正面的硬币的次数。将此数字存储在一个变量中，称为*x*。

    +   如果*x=0*的值，则仅在底层添加项目，即<math alttext="" display="inline"><mrow><msub><mi>S</mi><mn>0</mn></msub></mrow></math>。 否则，如果<math alttext="" display="inline"><mrow><mi>x</mi><mo>≥</mo><mi>h</mi></mrow></math>，则在顶层*Sh*的顶部添加额外的新级别<math alttext="" display="inline"><mrow><msub><mi>S</mi><mrow><mi>h</mi><mo>+</mo><mn>1</mn></mrow></msub><mo>,</mo><msub><mi>S</mi><mrow><mi>h</mi><mo>+</mo><mn>2</mn></mrow></msub><mo>,</mo><mn>...</mn><mo>,</mo><msub><mi>S</mi><mrow><mi>x</mi><mo>+</mo><mn>1</mn></mrow></msub></mrow></math>，其中只包含两个特殊键，即，- <math alttext="" display="inline"><mi>∞</mi></math>，+ <math alttext="" display="inline"><mi>∞</mi></math> 和元素*i*。

    对于*n*个元素，插入元素的时间复杂度为<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><mi>g</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math>。 具有*x=1*值的元素 85 的插入在图 10.26 中表示。

    ![图 10.26](img/fig10_26.jpg)

    **图 10.26.**

    在跳跃列表中插入。

+   删除：要删除项目*i*，请按照以下步骤进行：

    +   首先使用上述搜索算法搜索*i*，并找到元素*i*的位置*p0，p1，………，ph*。

    +   从级别*S0，S1，………，Sh*中的位置*p0，p1，………，ph*处的列表中移除元素。

    删除操作的时间复杂度为*n*个元素的<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><mi>g</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math>。 元素 87 的删除在图 10.27 中表示。

    ![图 10.27](img/fig10_27.jpg)

    **图 10.27.**

    跳跃列表中的删除。

在数据结构需要同时访问的情况下，跳表提供了很多好处。例如，跳表用于设计高度可伸缩的并发优先级队列，用于大规模微处理器 [171]。同样，跳表用于在大规模多处理器的抢占式和并发环境中实现无锁字典，用于共享对象 [181]。跳表实现了一种非阻塞（无锁）算法，用于共享对象，确保无论有多少争用，至少都会有一个操作处于活动状态。

### 10.4.1 Python 中的 Skiplist 实现

首先，我们将定义一个跳表节点，其中每个节点都由指向直接下一个节点的指针列表链接。

![](img/list10_5.jpg)

接下来，我们将定义一个跳表

![](img/list10_6.jpg)

要执行搜索、插入和删除操作，重要的是定义一个更新函数，该函数将从最顶层开始搜索，并将列表传递到任何级别，直到找到一个大于问题中的元素的元素。然后，探索下一个级别，重复上述过程。

![](img/list10_7.jpg)![](img/list10_8.jpg)![](img/list10_9.jpg)![](img/list10_10.jpg)

## 活动

### 多项选择题

1.  以下哪项不属于成员查询 PDS 的范畴？

    1.  BF

    1.  最小哈希

    1.  QF

    1.  跳表

1.  在标准布隆过滤器中，对于 *k* 个哈希函数、*m* 过滤器大小和 *n* 总插入元素，搜索复杂度是多少？

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>k</mi><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo>+</mo><mi>k</mi><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>m</mi><mo stretchy="false">)</mo></mrow></math>

1.  以下哪种布隆过滤器不支持假阴性？

    1.  计数 BF

    1.  光谱 BF

    1.  可删除的 BF

    1.  以上都不是

1.  计数 BF 相对于标准 BF 的优势是什么？

    1.  空间需求更少

    1.  计数 BF 从不支持假阳性

    1.  计数 BF 从不支持假阴性

    1.  计数布隆过滤器支持删除

1.  以下提到的哪种布隆过滤器不支持删除？

    1.  计数 BF

    1.  可删除的 BF

    1.  可扩展的 BF

    1.  动态 BF

1.  在一个包含 *n* 个元素的跳表中，删除操作的时间复杂度是多少？

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><mi>g</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><msup><mi>n</mi><mn>2</mn></msup></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo>+</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

1.  以下哪项不是 QF 的元数据位？

    1.  <math alttext="" display="inline"><mrow><mi>i</mi><mi>s</mi><mo>_</mo><mi>o</mi><mi>c</mi><mi>c</mi><mi>u</mi><mi>p</mi><mi>i</mi><mi>e</mi><mi>d</mi></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>i</mi><mi>s</mi><mo>_</mo><mi>c</mi><mi>o</mi><mi>n</mi><mi>t</mi><mi>i</mi><mi>n</mi><mi>u</mi><mi>a</mi><mi>t</mi><mi>i</mi><mi>o</mi><mi>n</mi></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>i</mi><mi>s</mi><mo>_</mo><mi>s</mi><mi>e</mi><mi>t</mi></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>i</mi><mi>s</mi><mo>_</mo><mi>s</mi><mi>h</mi><mi>i</mi><mi>f</mi><mi>t</mi><mi>e</mi><mi>d</mi></mrow></math>

1.  QF 优于 BF，因为：

    1.  QF 比 BF 占用更少的空间

    1.  QF 是缓存友好的，而 BF 不是

    1.  BF 在主内存之外提供可扩展性，而 QF 不提供

    1.  以上都不是

1\. b  2\. a  3\. c  4\. d  5\. c  6\. a  7\. c  8\. c

<hgroup>

# 11

# 基数估计概率数据结构

</hgroup>

## 11.1 简介

PDS 的下一个类别是用于在查询处理和数据库设计中广泛使用的基数估计。数据库模型使用基数估计算法来计算谓词的选择性。线性计数、LogLog、HyperLogLog 是此类别下的一些算法。这样的 PDS 的目标是计算集合中存在重复项的唯一元素的数量。例如，对于集合 <math alttext="" display="inline"><mrow><mi>S</mi><mo>=</mo><mo stretchy="false">[</mo><mn>1</mn><mo>,</mo><mn>2</mn><mo>,</mo><mn>3</mn><mo>,</mo><mn>1</mn><mo>,</mo><mn>2</mn><mo>,</mo><mn>3</mn><mo>,</mo><mn>4</mn><mo stretchy="false">]</mo></mrow></math>，集合的基数是 4。这种 PDS 的一个重要用例是计算特定网站的独立访问者数量。根据提供的数据，从 2019 年 5 月到 2019 年 9 月，Amazon 网页的总访问量为 22 亿。如果我们认为每 10 个访问者中有一个是独立的，则这种情况下的基数为 2.22 亿。值得注意的是，使用线性空间要求，基数估计对于任何确定性数据结构都很难实现。计算基数估计的一个简单方法是首先将集合元素按升序排列。接下来，在集合 S 上应用线性扫描以消除重复项。如果我们使用归并排序，集合 S 的基数，其中 *n* 个元素，可以在 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mi>l</mi><mi>o</mi><mi>g</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math> 的磁盘访问中计算出来，需要 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math> 的额外空间，因此这种方法效率低下。另一种计算基数的方法是使用哈希表数据结构，其中元素的哈希存储在哈希表中，并且通过哈希表中的键的总数来计算基数。显然，哈希具有删除重复项而无需排序的优点，因此只需要一次扫描。然而，对于大数据集，哈希法表现不佳，因为很难将大的哈希表适应主内存。这种方法的时间复杂度是 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>，需要 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math> 的额外空间。因此，对于传统的确定性方法，随着数据量的增加，查询处理只能在线性内存空间中进行。

使用概率技术的 PDS 可以估计出低空间要求和线性时间的基数。基数估计的 PDS 也是基于哈希的。然而，与简单的哈希不同，这些数据结构不会将元素的值存储在哈希表中。使用 PDS 进行基数估计可以不考虑数据类型，并且还可以在并行机器上分布，减少通信开销。

## 11.2 线性计数

作为概率方法计算基数的首次尝试，作者们在[213]中介绍了线性计数算法。线性计数不是存储实际元素，而是简单地在哈希表中设置对应元素的位。由于可能存在两个记录碰撞到相同位置的情况，因此计算的计数可能不准确。因此，基数是通过哈希表的占用率来近似计算的。对于一个包含 1.2 亿个元素的集合，使用线性计数方法计算基数需要 1.25 MB 的主存，1000 次磁盘访问和 1%的错误率。线性计数提供了计算基数的两个步骤，具体如下所述：

+   线性计数使用主存中大小为*m*的哈希表以及哈希函数。哈希表的每个条目都初始化为 0。对于每个传入的项，都会应用一个哈希函数，并将哈希表中相应的索引设置为 1。

+   接下来，记录空条目的数量（即，0）。我们将这个数字称为*x*。然后通过取*x*和*m*的比例来分析空位的分数（<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><msub><mi>V</mi><mi>n</mi></msub><mo stretchy="false">)</mo></mrow></math>)。通过将值放入以下方程式中来计算最终估计的基数：

    <math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mover accent="true"><mi>n</mi><mo>^</mo></mover><mo>≈</mo><mo>−</mo><mi>m</mi><mi>l</mi><mi>n</mi><msub><mi>V</mi><mi>N</mi></msub></mrow></mtd></mtr></mtable></mrow></math>(11.1)

    其中，*n* 是计算出的估计基数。

线性计数算法的时间复杂度为*O(n)*，其中，*n* 是集合 *S* 中元素的总计数。线性计数算法的结果准确性取决于负载因子。在这里，负载因子定义为唯一元素和哈希表大小的分数。负载因子的值越高，结果的准确性越低，而负载因子的值越低，结果的准确性越高。因此，如果哈希表大小与元素总数相比非常小，可能会导致碰撞的风险增加。否则，如果哈希表大小足够大，则碰撞的风险减小，但会消耗更多空间。作者得出结论，对于负载因子大于 1 的情况，线性计数产生 1%的误差。给定具有*N*个唯一元素的给定多重集合的估计基数 <math alttext="" display="inline"><mover accent="true"><mi>n</mi><mo>^</mo></mover></math> 的预期相对误差由方程 11.3 给出。变量 *t* 表示负载因子 ( <math alttext="" display="inline"><mrow><mfrac><mi>N</mi><mi>m</mi></mfrac></mrow></math>)。相对误差表示平均估计基数 <math alttext="" display="inline"><mover accent="true"><mi>n</mi><mo>^</mo></mover></math> 的百分比被错误计算，给出如下。

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mfrac><mrow><mo stretchy="false">(</mo><msup><mi>e</mi><mi>t</mi></msup><mo>−</mo><mi>t</mi><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo></mrow><mrow><mn>2</mn><mi>N</mi></mrow></mfrac></mrow></mtd></mtr></mtable></mrow></math>(11.2)

哈希表大小也受标准错误的影响。 标准错误被描述为<mrow><mfrac><mrow><mover accent="true"><mo stretchy="false">(</mo><mo>^</mo></mover><mi>n</mi><mo stretchy="false">)</mo></mrow><mi>N</mi></mfrac></mrow>的标准偏差，并由以下方程式计算。

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><msqrt><mi>m</mi></msqrt><mfrac><mrow><msup><mrow><mo stretchy="false">(</mo><msup><mi>e</mi><mi>t</mi></msup><mo>−</mo><mi>t</mi><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo></mrow><mrow><mn>1</mn><mo>/</mo><mn>2</mn></mrow></msup></mrow><mi>N</mi></mfrac></mrow></mtd></mtr></mtable></mrow></math>(11.3)

使用这种方法时，必须事先知道唯一项的数量，以便分配适当大小的哈希表。 显然，线性计数方法比传统方法更快，但不能产生准确的结果。 因此，这种数据结构的用例是对不需要 100％准确性的应用程序。 尽管如此，作者在[38]中建议不要对基数大于 2000 万的数据库关系使用线性计数算法，因为表格非常大，这将导致更准确的结果，存储要求较小。 作为更好的解决方案，还提供了 LogLog 和 HyperLogLog 算法。

让我们通过一个例子来理解线性计数。假设 <math alttext="" display="inline"><mrow><mi>m</mi><mo>=</mo><mn>16</mn></mrow></math> 并且哈希函数基于模哈希，即，<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>k</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>k</mi><mo>+</mo><mn>2</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>16</mn></mrow></math> 其中 *k* 是要插入的键。让集合 *S* 包含总共 10 个元素，即，<math alttext="" display="inline"><mrow><mi>S</mi><mo>=</mo><mn>4</mn><mo>,</mo><mn>34</mn><mo>,</mo><mn>6</mn><mo>,</mo><mn>4</mn><mo>,</mo><mn>14</mn><mo>,</mo><mn>36</mn><mo>,</mo><mn>6</mn><mo>,</mo><mn>7</mn><mo>,</mo><mn>0</mn><mo>,</mo><mn>7</mn></mrow></math>。值得注意的是，该集合的基数为 7。将这些元素通过哈希函数并将相应的位设置为 1。通过这些元素后，哈希表的结果状态表示为 <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mn>4</mn><mo stretchy="false">)</mo><mo>=</mo><mn>6</mn><mo>,</mo><mi>h</mi><mo stretchy="false">(</mo><mn>34</mn><mo stretchy="false">)</mo><mo>=</mo><mn>0</mn><mo>,</mo><mi>h</mi><mo stretchy="false">(</mo><mn>6</mn><mo stretchy="false">)</mo><mo>=</mo><mn>8</mn><mo>,</mo><mi>h</mi><mo stretchy="false">(</mo><mn>4</mn><mo stretchy="false">)</mo><mo>=</mo><mn>6</mn><mo>,</mo><mi>h</mi><mo stretchy="false">(</mo><mn>14</mn><mo stretchy="false">)</mo><mo>=</mo><mn>0</mn><mo>,</mo><mi>h</mi><mo stretchy="false">(</mo><mn>36</mn><mo stretchy="false">)</mo><mo>=</mo><mn>2</mn><mo>,</mo><mi>h</mi><mo stretchy="false">(</mo><mn>6</mn><mo stretchy="false">)</mo><mo>=</mo><mn>8</mn><mo>,</mo><mi>h</mi><mo stretchy="false">(</mo><mn>7</mn><mo stretchy="false">)</mo><mo>=</mo><mn>9</mn><mo>,</mo><mi>h</mi><mo stretchy="false">(</mo><mn>0</mn><mo stretchy="false">)</mo><mo>=</mo><mn>2</mn><mi>a</mi><mi>n</mi><mi>d</mi><mi>h</mi><mo stretchy="false">(</mo><mn>7</mn><mo stretchy="false">)</mo><mo>=</mo><mn>9</mn></mrow></math>。在这种情况下，*x* 的值为 11，负载因子为 <math alttext="" display="inline"><mrow><mfrac><mn>7</mn><mrow><mn>16</mn></mrow></mfrac></mrow></math>，因此（<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><msub><mi>V</mi><mi>n</mi></msub><mo stretchy="false">)</mo></mrow></math>）的值为 <math alttext="" display="inline"><mrow><mfrac><mrow><mn>11</mn></mrow><mrow><mn>16</mn></mrow></mfrac></mrow></math>，即等于 0.6875。要获得最终估计的基数，请将（<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><msub><mi>V</mi><mi>n</mi></msub><mo stretchy="false">)</mo></mrow></math>）的值放入方程式 11.1 中，结果为 <math alttext="" display="inline"><mrow><mover accent="true"><mi>n</mi><mo>^</mo></mover><mo>≈</mo><mo>−</mo><mn>16</mn><mo>*</mo><mi>l</mi><mi>n</mi><mo stretchy="false">(</mo><mn>0.6875</mn><mo stretchy="false">)</mo></mrow></math>，求解得 5.99 ≈ 6。由于碰撞，估计计数为 6，而实际基数为 7。整个例子在 图 11.1 中表示。

![图 11.1](img/fig11_1.jpg)

**图 11.1.**

线性计数算法示例。

![](img/list11_1a.jpg)

### 11.2.1 线性计数的实现代码

Python 实现的线性计数代码如下所示。这里，首先定义一个数据集，其中包含 300 个介于 0 和 20 之间的数字。接下来，我们使用 len() 函数检查数据集中唯一值的数量。结果表明，随着映射大小的增加，负载因子减小，基数估计生成更准确的结果。

![](img/list11_1b.jpg)![](img/list11_1c.jpg)

## 11.3 对数对数

线性计数仍然消耗 O(n)的空间，即线性空间消耗。在这种情况下，LogLog 在[74]中被引入，为大型数据集的基数估计提供了解决方案。该算法的内存使用量为<math alttext="" display="inline"><mrow><mi>l</mi><mi>o</mi><msub><mi>g</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><msub><mi>g</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>N</mi><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow></math>，其中，*N* 是唯一项的上限。为了计数<math alttext="" display="inline"><mrow><msup><mn>2</mn><mrow><mn>32</mn></mrow></msup></mrow></math>（40 亿）个不同的项，这个算法只需要<math alttext="" display="inline"><mrow><mi>l</mi><mi>o</mi><msub><mi>g</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><msub><mi>g</mi><mn>2</mn></msub><mo stretchy="false">(</mo><msup><mn>2</mn><mrow><mn>32</mn></mrow></msup><mo stretchy="false">)</mo><mo stretchy="false">)</mo><mo>=</mo><mn>5</mn></mrow></math>位的空间。要理解 LogLog 的概念，可以举个类比：假设两个朋友汤姆和杰瑞去了一个会议，并在那里决定打赌谁与最多陌生人互动。于是，他们开始计数他们互动的人数。然而，这样的计数可能是一项乏味的任务。所以下次会议，他们不再只是计数，而是开始在纸上写下他们的名字。这样做，更好地计算了独特的人数，而不是被总的对话次数所困扰。然而，随身携带一支笔和一张纸并不容易。所以，汤姆想出了一个替代方案，而不是记录人的名字，他们决定询问对方联系电话号码的最后 6 位数字，最后 6 位数字中前导零的序列最长的人将被宣布为赢家。例如，一个人的联系电话号码是 988866336，所以这里最长的序列是 0，因为没有前导零，如果联系电话号码是 00639，那么最长的序列就变成了 2。显然，如果汤姆或杰瑞只与少数人互动，获得最长前导零的概率要么是 0 要么是 1。随着他们互动的人数增多，获得前导零序列的概率增加到 3 或 4。要获得最长的零序列值 6，他们中的任何一个都必须与成千上万的人互动，以获得联系电话号码的最后 6 位数字为 00000 的人。

相同的概念也适用于 LogLog 算法。在这里，通过对每个元素进行哈希处理，然后记录每个元素的最长零序列来计算大型集合中的唯一元素数量。LogLog 使用一个具有*m*个条目或桶以及一个单一哈希函数的哈希表。值得注意的是，随着*m*值的增加，平均误差率会降低。由于哈希函数的输出是固定长度的，因此元素的插入具有 O(1)的时间复杂度。下面逐步解释使用 LogLog 估计基数的过程：

+   对于每个传入的项，计算每个项的固定长度哈希值。

+   将从上一步获得的哈希值分成两部分。前*k*位表示一个桶的索引，从剩余序列中记录最长的零序列，并将最长的零序列的值存储在该特定桶中。例如，对于一个包含 16 个桶的哈希表，获得的固定长度（10 位）哈希值为 1010 001001，总共有 16 个桶。因此，前 4 位表示桶的索引，从剩余的位中记录最长的零序列，即，在第 10 个位置存储了 2。

+   对于每个获得的哈希值，只有到目前为止最长的前导零字符串的值被存储在每个桶中。

+   假设 R1、R2、………、Rm 表示哈希表中的条目。集合的最终基数可以通过计算哈希表中条目的算术平均值来计算。为了减少异常值的影响并减小方差，不是取平均值，而是计算平均值。因此，LogLog 通过存储多个估计值然后对结果进行平均来提高准确性。因此，集合的最终基数可以计算为：

    <math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>估</mi><mi>计</mi><mi>精</mi><mi>确</mi><mi>度</mi><mo>=</mo><mn>0.79402</mn><mo>*</mo><mi>m</mi><mo>*</mo><msup><mn>2</mn><mrow><mfrac><mrow><mstyle displaystyle="true"><msubsup><mo>∑</mo><mrow><mi>j</mi><mo>=</mo><mn>1</mn></mrow><mi>m</mi></msubsup><mrow><msub><mi>R</mi><mi>j</mi></msub></mrow></mstyle></mrow><mi>m</mi></mfrac></mrow></msup></mrow></mtd></mtr></mtable></mrow></math>(11.4)

采用 *m* 个桶基本上相当于采用了不同的 *m* 个哈希函数。LogLog 算法的标准误差为 <math alttext="" display="inline"><mrow><mfrac><mrow><mn>1.30</mn></mrow><mrow><mi>s</mi><mi>q</mi><mi>r</mi><mi>t</mi><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></mfrac></mrow></math>，其中 *m* 表示总桶条目。因此，对于一个具有 2048 个条目且每个条目具有 S 位的桶，预期误差为 2.5%。哈希表可以估计基数直到 227\. LogLog 的明显见解是，一个数字以长字符串的零开始的可能性较小（一个数字具有 10 个前导零的概率较小，但不是很罕见）。虽然 LogLog 算法不适用于小基数，并且它只能处理具有大基数的集合。此外，需要对要插入的总项数进行先前的上限解码，以便选择哈希表。让我们以 LogLog 为例，其中 <math alttext="" display="inline"><mrow><mi>m</mi><mo>=</mo><mn>16</mn></mrow></math>，任何桶的索引占用 4 位。该示例计算网站的独立访客。请参阅 图 11.2 在插入 4 个元素后，估计的基数为 <math alttext="" display="inline"><mrow><mn>0.79402</mn><mo>*</mo><mn>16</mn><mo>*</mo><msup><mn>2</mn><mrow><mfrac><mn>6</mn><mrow><mn>16</mn></mrow></mfrac></mrow></msup><mo>≈</mo><mn>16.47</mn></mrow></math>。显然，由于插入了少量元素，此算法的结果计算错误。然而，对于大基数，该算法将生成更准确的结果。

![图 11.2](img/fig11_2.jpg)

**图 11.2.**

LogLog 示例。

### 11.3.1 Python 中 LogLog 的实现

![](img/list11_2a.jpg)![](img/list11_2b.jpg)

## 11.4 HyperLogLog

HyperLogLog（HLL）是最流行的概率算法，用于计算多重集合中的不同项。与精确计算不同，HLL 在低存储要求下计算近似值。HLL[82]在两个方面是 LogLog 的改进版本。

+   在 HLL 中插入任何元素的过程几乎与 LogLog 中讨论的过程相同。与 LogLog 不同的是，在第四步中组合桶时，不是使用算术平均值，而是取桶中值的调和平均值。HLL 的顺序实现在图 11.3 中表示。这是为了减少同一桶中不常见的高最大前导零计数的影响。调和平均值有助于忽略接近无穷大的值。因此，它减少了干扰的指数化嘈杂数字的影响，并提高了基数估计的准确性。HLL 进一步减少了离群值的影响，通过在平均之前移除最大值来提高估计的准确性。从 HLL 估算的基数如下所示：

    <math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>E</mi><mo>=</mo><msub><mi>α</mi><mi>m</mi></msub><mo>.</mo><mi>m</mi><mfrac><mi>m</mi><mrow><mfenced close=")" open="("><mrow><mstyle displaystyle="true"><msubsup><mo>∑</mo><mrow><mi>j</mi><mo>=</mo><mn>1</mn></mrow><mi>m</mi></msubsup><mrow><msup><mn>2</mn><mrow><mo>−</mo><msup><mi>R</mi><mi>j</mi></msup></mrow></msup></mrow></mstyle></mrow></mfenced></mrow></mfrac></mrow></mtd></mtr></mtable></mrow></math>(11.5)

    ![图 11.3](img/fig11_3.jpg)

    **图 11.3.**

    HLL 的顺序实现。

    其中，*α* 是一个常数，其值根据桶的数量选择。

+   HLL 对极端情况进行校正，即当所有桶都未被占用或者桶几乎全满且哈希冲突导致低估时。如果计算得到的估计值 *E* 小于 <math alttext="" display="inline"><mrow><mn>2.5</mn><mo>*</mo><mi>m</mi></mrow></math>，并且有一些桶的最大前导零值为零，则在这种情况下，最终基数被替换为

    <math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><msub><mi>E</mi><mrow><mi>n</mi><mi>e</mi><mi>w</mi></mrow></msub><mo>=</mo><mo>−</mo><mi>m</mi><mo>*</mo><mi>l</mi><mi>o</mi><mi>g</mi><mo stretchy="false">(</mo><mfrac><mi>V</mi><mi>m</mi></mfrac><mo stretchy="false">)</mo></mrow></mtd></mtr></mtable></mrow></math>(11.6)

    其中，*V* 表示最大前导零值为零的桶的计数。对于接近哈希表总大小的大基数，即 <math alttext="" display="inline"><mrow><mi>E</mi><mo>></mo><mfrac><mrow><msup><mn>2</mn><mi>m</mi></msup></mrow><mrow><mn>30</mn></mrow></mfrac></mrow></math>，最终基数计算如下：

    <math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><msub><mi>E</mi><mrow><mi>n</mi><mi>e</mi><mi>w</mi></mrow></msub><mo>=</mo><mo>−</mo><msup><mn>2</mn><mi>m</mi></msup><mi>l</mi><mi>o</mi><mi>g</mi><mo stretchy="false">(</mo><mn>1</mn><mo>−</mo><mfrac><mi>E</mi><mrow><msup><mn>2</mn><mi>m</mi></msup></mrow></mfrac><mo stretchy="false">)</mo></mrow></mtd></mtr></mtable></mrow></math>(11.7)

除此之外，HLL 还支持合并操作，简单地应用两个 HLL 的并集，该函数返回每对桶中的最大值，即，

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>H</mi><mi>L</mi><msub><mi>L</mi><mrow><mi>u</mi><mi>n</mi><mi>i</mi><mi>o</mi><mi>n</mi></mrow></msub><mo stretchy="false">[</mo><mi>j</mi><mo stretchy="false">]</mo><mo>=</mo><mi>m</mi><mi>a</mi><mi>x</mi><mo stretchy="false">(</mo><mi>H</mi><mi>L</mi><msub><mi>L</mi><mn>1</mn></msub><mo stretchy="false">[</mo><mi>j</mi><mo stretchy="false">]</mo><mo>,</mo><mi>H</mi><mi>L</mi><msub><mi>L</mi><mn>2</mn></msub><mo stretchy="false">[</mo><mi>j</mi><mo stretchy="false">]</mo><mo stretchy="false">)</mo></mrow></mtd></mtr></mtable></mrow></math>(11.8)

其中，*j* 的取值范围是从 1 到 *m*。相比于 LogLog，HLL 更受欢迎的一个原因是，对于相同数量的项目，HLL 的准确性比 LogLog 更高。HLL 的标准误差率被描述为 <math alttext="" display="inline"><mrow><mfrac><mrow><mn>1.04</mn></mrow><mrow><mi>s</mi><mi>q</mi><mi>r</mi><mi>t</mi><mo stretchy="false">(</mo><mi>m</mi><mo stretchy="false">)</mo></mrow></mfrac></mrow></math>，其中 *m* 是使用的桶的数量。例如，Redis 软件默认使用 16348 个寄存器，因此为了实现 HLL，它返回标准误差为 0.81%。原始的 HLL 对于小基数仍然返回较大的误差，但稍加改进后，它可以处理非常小范围的基数到大范围的基数。

举个例子，统计迄今为止访问网站的唯一用户数量。假设有 16 个桶，这意味着寻址一个桶需要 4 位。如 图 11.4 所示，对于每个 IP 地址，首先将其通过 HLL 哈希函数传递，返回 16 位固定数字。前四位确定桶号，从剩余位中提取前导零的计数，但只保留最大前导零的记录，其余的被忽略。类似地，对其他 IP 地址也是如此。为了得到最终的基数，取计数列的调和平均数。在插入 4 个不同的 IP 地址后，估计的基数可以计算为 <math alttext="" display="inline"><mrow><mfrac><mrow><mn>0.673</mn><mo>*</mo><mn>16</mn><mo>*</mo><mn>16</mn></mrow><mrow><msup><mn>2</mn><mrow><mo>−</mo><mn>2</mn></mrow></msup><mo>+</mo><msup><mn>2</mn><mrow><mo>−</mo><mn>4</mn></mrow></msup></mrow></mfrac><mo>≈</mo><mn>551</mn></mrow></math>，显然不等于 4，因为对于小基数，HLL 结果显示出强烈的偏见。然而，对于大基数，该算法运行良好。

![图 11.4](img/fig11_4.jpg)

**图 11.4.**

HLL 示例。

### 11.4.1 Python 中的 HLL 实现

![](img/list11_3a.jpg)![](img/list11_3b.jpg)![](img/list11_4.jpg)![](img/list11_5a.jpg)![](img/list11_5b.jpg)

## 活动

### 多项选择题

1.  对于 *n* 个总元素的线性计数算法的时间复杂度是多少？

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><msup><mi>n</mi><mn>2</mn></msup><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><mi>g</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mi>l</mi><mi>o</mi><mi>g</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

1.  对于大小为 *m* 的哈希表的 LogLog 算法的插入操作的时间复杂度是多少？

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>m</mi><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><msup><mi>m</mi><mn>2</mn></msup><mo stretchy="false">)</mo></mrow></math>

    1.  以上都不是

1.  对于大小为 32 的哈希表。为索引字段和最长零序列字段保留了多少位？

    1.  6,25

    1.  5,27

    1.  16,16

    1.  10,22

1.  HLL 代表？

    1.  水日志

    1.  超对数日志

    1.  超对数线性

    1.  超线性线性

1.  LogLog 数据结构的空间需求是多少，其中 *N* 是唯一元素数量的上限？

    1.  <math alttext="" display="inline"><mrow><mi>l</mi><mi>o</mi><msub><mi>g</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><msub><mi>g</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>N</mi><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>l</mi><mi>o</mi><msup><mi>g</mi><mn>2</mn></msup><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><msub><mi>g</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>N</mi><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>l</mi><mi>o</mi><msub><mi>g</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><msup><mi>g</mi><mn>2</mn></msup><mo stretchy="false">(</mo><mi>N</mi><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>l</mi><mi>o</mi><msup><mi>g</mi><mn>2</mn></msup><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><msup><mi>g</mi><mn>2</mn></msup><mo stretchy="false">(</mo><mi>N</mi><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow></math>

1.  要计数，<math alttext="" display="inline"><mrow><msup><mn>2</mn><mrow><mn>32</mn></mrow></msup></mrow></math>（40 亿）个不同项，LogLog 算法只需要？

    1.  5 位

    1.  10 位

    1.  32 位

    1.  以上都不是

1\. a  2\. b  3\. c  4\. b  5\. a  6\. a

<hgroup>

# 12

# 频率计数查询概率数据结构

</hgroup>

## 12.1 简介

此类别涉及对集合中特定项目的数量进行估计。例如，搜索引擎使用频率估计器来提取频繁搜索的查询，网络路由器使用它们来定位常见的源和目标地址。对此的一个提出的解决方案是从显示完整集合特性的集合中随机提取样本。然而，实现真正的随机性是一项相当不利的任务。因此，抽样也不是我们问题的一个有用的解决方案。另外，使用哈希表时，随着更多项目的添加，内存需求变得很高（线性空间需求）。Majority algorithm [52] 和 Misra-Gries [144] 算法是解决频率计数问题的两种流行的确定性算法。一个有效的方法之一是采用基于近似的查询来处理流数据。在这个背景下，一种流行的数据结构是“Sketch”，它基于摘要的方法执行近似查询。基于近似和随机化的 Sketch 算法是这个背景下空间和时间有效的解决方案。Sketches 指的是一类通过比实际数据大小小得多的紧凑摘要来描绘大量数据的算法 [89]。机器学习、自然语言处理、安全性是一些重要领域，其中 Sketch 的变体正在被使用 [203]。Sketches 还解决了抽样技术面临的问题，并在实践中支持并行化。Sketches 中的并行化意味着它可以独立地在数据的不同部分上实现，并进一步组合这些部分，从而产生一致的聚合结果。简而言之，并行化对面临可伸缩性挑战的问题施加了一种直观的分而治之的方法。此外，Sketches 具有次线性渐近计算复杂性，这导致低计算功率和存储。该类别下的算法由两个参数 *ϵ* 和 *δ* 特征化，其中 *ϵ*（精度参数）描述了在最大概率下频率估计结果中的最大可承受误差，最大概率为 *δ*（置信度参数）。这两个参数可以根据可用空间进行调整。另外，对于 Sketches，估计频率时的误差可能是过估计、低估计或两者的组合。

## 12.2 计数最小化草图

计数最小化草图（CMS）[66] 是用于执行频率计数查询的最流行的可用草图数据结构。具体来说，这种数据结构能够对流数据进行高效的查询处理。CMS 使用压缩的数据表示来保证低存储需求。类似于哈希表，CMS 使用宽度 *w* 和深度 *d* 的表。在设计草图时，参数 *w* 和 *d* 是固定的。表中的所有内容都初始化为零。与哈希表不同的是，CMS 不是使用单个哈希函数，而是对于表的每一行使用不同的哈希函数，即使用了 *d* 个成对独立的哈希函数，如 图 12.1 所示。成对独立构建了一个通用哈希族，导致最小碰撞 [113]。来自通用族的哈希函数是那些具有较低碰撞概率的类。哈希函数应该被选择为使得它们将传入的项分散开来以达到高精度。每个哈希函数将传入的元素映射到范围为 1, 2, 3, ……, *w* 的相应列。CMS 只消耗次线性空间，但由于哈希碰撞而导致过度计数。线性空间复杂度意味着随着数据量的增加，内存消耗也会直接增加。而次线性空间复杂度不会消耗与数据相等的内存。但是它消耗的内存少于数据的一半，如 图 12.2 所示。CMS 支持的操作描述如下：

![图 12.1](img/fig12_1.jpg)

**图 12.1.**

CMS 的结构。

![图 12.2](img/fig12_2.jpg)

**图 12.2.**

理解次线性空间要求。

+   更新（i，c）：此函数通过计数*c*更新任何传入元素*i*的频率。对于每个传入的元素，都会应用所有*d*个哈希函数，并且在每个哈希函数中的相应位置之间的<math alttext="" display="inline"><mrow><mn>1</mn><mo>−</mo><mi>w</mi></mrow></math>更新现有值的值。

+   估算（i）：此函数计算集合中元素*i*的频率。首先定位对应于*d*个哈希函数的位置。最后，元素*i*的频率计数是*d*个获得的位置中的最小值。由于使用了哈希函数，不同元素可能会在同一个单元上发生碰撞。因此，通过选择最小值，可以为频率查询获取最接近准确的结果。显然，来自 CMS 的结果可能会高估但永远不会低估。值得注意的是，CMS 首先进行计数，然后计算最小值，因此被称为计数-最小值草图。

+   删除（i，c）：要从集合中删除元素*i*，只需在每一行中相应的位置递减计数*c*。

需要注意的是，CMS 的频率估计与计数 BF 有些相似。与其他 PDS 一样，CMS 的使用情况对于不关心元素的确切频率计数的应用是有益的。数据库查询规划、流量监控中查找重要数据、自然语言处理、压缩感知、联合大小估计是频率查询估计 PDS 的一些有前途的使用情况。CMS 也支持并行化，因为这里的子草图可以通过取表的和来合并。但是，只有在使用相同的 *w* 和 *d* 值以及相同的哈希函数构建的两个草图才能合并。此外，CMS 允许对支持幺半群的任何可加值进行近似添加。CMS 的一个缺点是它显示了对数字真实频率计数的行为偏向估计。Count-min-log 草图、count-min-mean 草图是 CMS 的一些最近的改进。显然，对于任何项目 *i*，实际频率（<math alttext="" display="inline"><mrow><msub><mi>f</mi><mi>i</mi></msub></mrow></math>）总是小于或等于估计频率（<math alttext="" display="inline"><mrow><msub><mover accent="true"><mi>f</mi><mo>^</mo></mover><mi>i</mi></msub></mrow></math>）。对于大小为 *w*d* 的草图，设置 <math alttext="" display="inline"><mrow><mi>w</mi><mo>=</mo><mfrac><mn>2</mn><mi>ϵ</mi></mfrac></mrow></math> 和 <math alttext="" display="inline"><mrow><mi>d</mi><mo>=</mo><mi>l</mi><mi>o</mi><mi>g</mi><mo stretchy="true">(</mo><mfrac><mn>1</mn><mi>δ</mi></mfrac><mo stretchy="true">)</mo></mrow></math> 确保估计操作最多可以超过实际频率 <math alttext="" display="inline"><mrow><mi>ϵ</mi><mi>N</mi></mrow></math>（<math alttext="" display="inline"><mrow><msub><mover accent="true"><mi>f</mi><mo>^</mo></mover><mi>i</mi></msub><mo>≤</mo><msub><mi>f</mi><mi>i</mi></msub><mo>+</mo><mi>ϵ</mi><mi>N</mi></mrow></math>）的概率至少为 <math alttext="" display="inline"><mrow><mn>1</mn><mo>−</mo><mi>δ</mi></mrow></math>。改变 *w* 和 *d* 值的影响在 表 12.1 中表示。因此，对于大小为 *N* 的基数估计，最多有 <math alttext="" display="inline"><mrow><mfrac><mrow><mn>2</mn><mi>N</mi></mrow><mi>w</mi></mfrac></mrow></math> 的错误概率至少为 <math alttext="" display="inline"><mrow><mn>1</mn><mo>−</mo><msup><mrow><mo stretchy="true">(</mo><mfrac><mn>1</mn><mn>2</mn></mfrac><mo stretchy="true">)</mo></mrow><mi>d</mi></msup></mrow></math>。CMS 消耗的空间是 O（<math alttext="" display="inline"><mrow><mfrac><mn>1</mn><mi>ϵ</mi></mfrac><mi>l</mi><mi>o</mi><mi>g</mi><mfrac><mn>1</mn><mi>δ</mi></mfrac></mrow></math>），更新和估计所需的时间由 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="true">(</mo><mi>l</mi><mi>o</mi><mi>g</mi><mfrac><mn>1</mn><mi>δ</mi></mfrac><mo stretchy="true">)</mo><mo>=</mo><mi>O</mi><mo stretchy="true">(</mo><mi>d</mi><mo stretchy="true">)</mo></mrow></math> 给出。CMS 还支持通过减少相应的哈希位置进行删除。

**表格 12.1**

CMS 参数变化的影响。

| 参数 | 增加 | 减少 |
| --- | --- | --- |
| w |

+   高准确率

+   较高的内存需求

| • 相对更高的错误率 |
| --- |
| d |

+   更新将以较低的速度处理

+   较低的误报率

+   较高的内存需求

|

+   更新数据所需的时间较短

+   较低的内存需求

|

CMS 的主要应用之一是监测重要访问者。根据阈值 *ϕ* 定义了重要访问者，如果任何项目的频率计数等于或大于 *ϕ*，那么该项目可能被视为重要访问者。 Schechter 等人 [167] 提出了一种方法，用于识别最流行的密码，以防止统计猜测攻击。在这里，作者的主要贡献是通过不让任何密码变得普遍来剥夺攻击者猜测最流行的密码。 CMS 与 BF 结合使用时效果更好。Gupta 等人 [94] 提出了一种基于 PDS 的入侵检测系统模型。为了检查一个节点是否可疑，从一组可疑节点中，所有进入的节点都通过 BF，然后通过 CMS 计算特定节点的命中频率，如果 BF 返回 true，则该节点被认为可疑。

让我们通过一个例子来理解 CMS。考虑一个 2-D 表格，其中 <math alttext="" display="inline"><mrow><mi>w</mi><mo>=</mo><mn>6</mn></mrow></math> 且 <math alttext="" display="inline"><mrow><mi>d</mi><mo>=</mo><mn>4</mn></mrow></math>，即将使用 4 个哈希函数，每行将有 6 个桶。考虑 <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo>=</mo><mi>i</mi><mi>m</mi><mi>o</mi><mi>d</mi><mn>6</mn></mrow></math>，<math alttext="" display="inline"><mrow><mi>h</mi><mn>2</mn><mo>=</mo><mo stretchy="true">(</mo><mn>2</mn><mo>*</mo><mi>i</mi><mo stretchy="true">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>6</mn></mrow></math>，<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>3</mn></msub><mo>=</mo><mo stretchy="true">(</mo><mi>i</mi><mi>m</mi><mi>o</mi><mi>d</mi><mn>3</mn><mo stretchy="true">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>6</mn></mrow></math> 和 <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>4</mn></msub><mo>=</mo><mo stretchy="true">(</mo><mn>2</mn><mi>i</mi><mo>+</mo><mn>3</mn><mo stretchy="true">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>6</mn></mrow></math>。所有 24 个位置都初始化为零。每个传入的元素都经过这 4 个哈希函数，并且相应位置根据给定的计数递增。操作序列 update(12,1), update(5,2), update (16,1), update(6,1) 显示在 图 12.3 中。通过给定哈希函数传递元素 12, 5, 16, 6 的结果显示在 表格 12.2 中。查询操作 Estimate(6) 在 图 12.4 中展示，查询操作 Estimate(12) 在 图 12.5 中表示。对于元素 6，估计查询返回真实结果，而对于元素 12，它显示了一个过估计的情况。最后，通过计数 1 删除元素 6 的操作显示在 图 12.6 中。

![图 12.3](img/fig12_3.jpg)

**图 12.3**

CMS 中的更新操作。

**表格 12.2**

经过哈希函数处理后的元素结果。

| 元素 | *h*[1] | *h*[2] | *h*[3] | *h*[4] |
| --- | --- | --- | --- | --- |
| 12 | 0 | 0 | 0 | 5 |
| 5 | 5 | 4 | 2 | 1 |
| 16 | 4 | 2 | 1 | 5 |
| 6 | 0 | 0 | 0 | 3 |

![图 12.4](img/fig12_4.jpg)

**图 12.4.**

CMS 中的估算操作。

![图 12.5](img/fig12_5.jpg)

**图 12.5.**

CMS 中的估算操作代表了过估计。

![图 12.6](img/fig12_6.jpg)

**图 12.6.**

CMS 中的估算操作代表了过估计。

### 12.2.1 使用 Python 实现 CMS

![](img/list12_1a.jpg)![](img/list12_1b.jpg)![](img/list12_2a.jpg)![](img/list12_2b.jpg)![](img/list12_3.jpg)![](img/list12_4.jpg)

### 12.2.2 计数均值最小素描

为了处理 CMS 产生的偏差，[70]的作者引入了 CMS 的变体称为计数均值最小（CMM）。作者指出，由于 CMS 的计数器被许多元素触摸，因此会出现误差。在这里，作者将这种误差称为噪声。值得注意的是，CMS 输出最小噪声计数器。在 CMM 中，作者的目标是估计每个计数器产生的噪声。为了估计计数器的噪声，注意观察一行中未被问题元素触摸的其他计数器的值。在这里，假设每个元素在表的所有行中均匀且随机映射。未被元素触摸的每个计数器的值是一个独立的随机变量，并且遵循与噪声相同的分布模式。CMM 的结构和更新过程与 CMS 类似。这里还使用了一个 2-D 表（w*d），它使用相同的哈希函数（h0、h1、…、hd-1）。但是，CMM 的估计过程与 CMS 不同。不是从*d*个计数器中返回最小值，而是从这些*d*个计数器中估计的噪声中扣除并返回残差的中位数。要计算一行中*d*个计数器的噪声，请计算除该行中任何计数器之外的所有其他计数器的平均值。因此，计数器的估计噪声由以下方程给出：

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mfrac><mrow><mi>N</mi><mo>−</mo><mi>C</mi><mi>M</mi><mo stretchy="false">[</mo><mi>i</mi><mo>,</mo><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>q</mi><mo stretchy="false">)</mo><mo stretchy="false">]</mo></mrow><mrow><mi>w</mi><mo>−</mo><mn>1</mn></mrow></mfrac></mrow></mtd></mtr></mtable></mrow></math>(12.1)

其中，*N* 是数据流大小，

*CM[i, hi(q)]* 是第*i*行中元素*q*的计数器，*i= o,1,…., d-1*，

*w* = 笔记宽度

*q* = 问题中的元素

该算法也可能会过度估计，其估计次数由中位数给出：

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>C</mi><mi>M</mi><mo stretchy="false">[</mo><mi>i</mi><mo>,</mo><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>q</mi><mo stretchy="false">)</mo><mo stretchy="false">]</mo><mo>−</mo><mfrac><mrow><mi>N</mi><mo>−</mo><mi>C</mi><mi>M</mi><mo stretchy="false">[</mo><mi>i</mi><mo>,</mo><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>q</mi><mo stretchy="false">)</mo><mo stretchy="false">]</mo></mrow><mrow><mi>w</mi><mo>−</mo><mn>1</mn></mrow></mfrac></mrow></mtd></mtr></mtable></mrow></math>(12.2)

对所有*i*行。

## 12.3 计数草图

Count-sketch 几乎与 CMS 类似，并为任何单个项目提供频率估计。实际上，count-sketch 的作者[62]设计它来在流中保持最高频率项目的近似计数。CMS 和 count-sketch 的区别在于估计过程和频率估计的准确性保证的性质。作者已经证明所提出的算法比抽样算法更好。Count sketch 还使用大小为 *w*d* 的二维表格，这被解释为具有 *w* 个桶的 *d* 个哈希表的数组。与 CMS 不同的是，count-sketch 每行不是使用单个哈希函数，而是使用两个哈希函数（*h* 和 *g*）。每个哈希函数 <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo>,</mo><msub><mi>h</mi><mn>2</mn></msub><mo>,</mo><mn>......</mn><mo>,</mo><msub><mi>h</mi><mi>d</mi></msub></mrow></math> 映射自 *1,2,….,w*，而 <math alttext="" display="inline"><mrow><msub><mi>s</mi><mn>1</mn></msub><mo>,</mo><msub><mi>s</mi><mn>2</mn></msub><mo>,</mo><mn>..........</mn><mo>,</mo><msub><mi>s</mi><mi>d</mi></msub></mrow></math> 映射到 -1 或 +1，即 +1 或 -1。Count-sketch 支持的操作如下讨论：

+   Update(q, c): 此操作将项目 *q* 的计数 *c* 更新到 count-sketch 中。对于数组的每个哈希表，计算更新后的 sketch 状态如下：

    <math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>s</mi><mi>k</mi><mi>e</mi><mi>t</mi><mi>c</mi><mi>h</mi><mo stretchy="false">[</mo><mi>k</mi><mo>,</mo><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">[</mo><mi>q</mi><mo stretchy="false">]</mo><mo stretchy="false">]</mo><mo>=</mo><mi>s</mi><mi>k</mi><mi>e</mi><mi>t</mi><mi>c</mi><mi>h</mi><mo stretchy="false">[</mo><mi>k</mi><mo>,</mo><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">[</mo><mi>q</mi><mo stretchy="false">]</mo><mo stretchy="false">]</mo><mo>+</mo><mi>c</mi><mo>*</mo><msub><mi>s</mi><mi>i</mi></msub><mo stretchy="false">[</mo><mi>q</mi><mo stretchy="false">]</mo><mi>w</mi><mi>h</mi><mi>e</mi><mi>r</mi><mi>e</mi><mo>></mo><mi>i</mi><mo>∈</mo><mo stretchy="false">[</mo><mn>1</mn><mo>,</mo><mi>d</mi><mo stretchy="false">]</mo><mo>></mo><mi>a</mi><mi>n</mi><mi>d</mi><mo>></mo><mn>1</mn><mo><</mo><mi>k</mi><mo><</mo><mi>d</mi><mo>.</mo></mrow></mtd></mtr></mtable></mrow></math>（12.3）

    引入<math alttext="" display="inline"><mrow><mo>±</mo><mn>1</mn></mrow></math>对元素*q*的更好估计可能会有所帮助，因为它可以更好地处理元素之间的碰撞。然而，如果元素*q*与多个频繁元素发生碰撞，则对元素*q*的估计不会很好，但在与不频繁元素发生碰撞的情况下，<math alttext="" display="inline"><mrow><mo>±</mo><mn>1</mn></mrow></math>的影响是积极的。

+   估计（q）：该操作找到了草图中元素*q*的近似计数。要执行此操作，请取<math alttext="" display="inline"><mrow><mi>s</mi><mi>k</mi><mi>e</mi><mi>t</mi><mi>c</mi><mi>h</mi><mo stretchy="true">[</mo><mi>k</mi><mo>,</mo><msub><mi>h</mi><mi>k</mi></msub><mo stretchy="true">[</mo><mi>q</mi><mo stretchy="true">]</mo><mo>.</mo><msub><mi>s</mi><mi>k</mi></msub><mo stretchy="true">[</mo><mi>q</mi><mo stretchy="true">]</mo><mo stretchy="true">]</mo></mrow></math>的中位数，其中，<math alttext="" display="inline"><mrow><mi>i</mi><mo>∈</mo><mo>[</mo><mn>1</mn><mo>,</mo><mi>d</mi><mo>]</mo></mrow></math>，而且<math alttext="" display="inline"><mrow><mn>1</mn><mo>≤</mo><mi>k</mi><mo>≤</mo><mi>d</mi></mrow></math>。作者在结果中证明了中位数相对于均值具有较强的鲁棒性。此外，均值对异常值很敏感。

然而，在 count-sketch 的基础论文中，作者并未提及删除操作。Count-Sketch 所消耗的空间为<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="true">(</mo><mfrac><mn>1</mn><mrow><msup><mi>ϵ</mi><mn>2</mn></msup></mrow></mfrac><mi>l</mi><mi>o</mi><mi>g</mi><mfrac><mn>1</mn><mi>δ</mi></mfrac><mo stretchy="true">)</mo></mrow></math>。然而，作者忽略了流中元素的实际存储空间要求。此外，设置 <math alttext="" display="inline"><mrow><mi>w</mi><mo>=</mo><mfrac><mn>2</mn><mrow><msup><mi>ϵ</mi><mn>2</mn></msup></mrow></mfrac></mrow></math> 和 <math alttext="" display="inline"><mrow><mi>d</mi><mo>=</mo><mi>l</mi><mi>o</mi><mi>g</mi><mo stretchy="true">(</mo><mfrac><mn>4</mn><mi>δ</mi></mfrac><mo stretchy="true">)</mo></mrow></math> 可以实现至多<math alttext="" display="inline"><mrow><mi>ϵ</mi><mi>N</mi></mrow></math>的误差，至少有<math alttext="" display="inline"><mrow><mn>1</mn><mo>−</mo><mi>δ</mi></mrow></math>的概率，其中*N*为流大小。值得注意的是，该算法对查询产生了高估和低估。

让我们举个例子来更清楚地理解计数蓝图。考虑一个表，其中<math alttext="" display="inline"><mrow><mi>w</mi><mo>=</mo><mn>6</mn></mrow></math>，<math alttext="" display="inline"><mrow><mi>d</mi><mo>=</mo><mn>4</mn></mrow></math>。每个哈希表的哈希函数值分别为<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo>=</mo><mi>i</mi><mi>m</mi><mi>o</mi><mi>d</mi><mn>6</mn></mrow></math>，<math alttext="" display="inline"><mrow><mi>h</mi><mn>2</mn><mo>=</mo><mo stretchy="true">(</mo><mn>2</mn><mo>*</mo><mi>i</mi><mo stretchy="true">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>6</mn></mrow></math>，<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>3</mn></msub><mo>=</mo><mo stretchy="true">(</mo><mi>i</mi><mi>m</mi><mi>o</mi><mi>d</mi><mn>3</mn><mo stretchy="true">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>6</mn></mrow></math>以及<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>4</mn></msub><mo>=</mo><mo stretchy="true">(</mo><mn>2</mn><mi>i</mi><mo>+</mo><mn>3</mn><mo stretchy="true">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>6</mn></mrow></math>，*g*1,*g*2 对于任何输入项都会随机生成<math alttext="" display="inline"><mrow><mo>−</mo><mn>1</mn></mrow></math>或<math alttext="" display="inline"><mrow><mo>+</mo><mn>1</mn></mrow></math>。通过哈希函数*h*和*g*传递后的元素的结果在表 12.3 中表示出来。连续执行<math alttext="" display="inline"><mrow><mi>u</mi><mi>p</mi><mi>d</mi><mi>a</mi><mi>t</mi><mi>e</mi><mo stretchy="true">(</mo><mn>12</mn><mo>,</mo><mn>1</mn><mo stretchy="true">)</mo></mrow></math>，<math alttext="" display="inline"><mrow><mi>u</mi><mi>p</mi><mi>d</mi><mi>a</mi><mi>t</mi><mi>e</mi><mo stretchy="true">(</mo><mn>5</mn><mo>,</mo><mn>2</mn><mo stretchy="true">)</mo></mrow></math>，<math alttext="" display="inline"><mrow><mi>u</mi><mi>p</mi><mi>d</mi><mi>a</mi><mi>t</mi><mi>e</mi><mo stretchy="true">(</mo><mn>16</mn><mo>,</mo><mn>1</mn><mo stretchy="true">)</mo></mrow></math>以及<math alttext="" display="inline"><mrow><mi>u</mi><mi>p</mi><mi>d</mi><mi>a</mi><mi>t</mi><mi>e</mi><mo stretchy="true">(</mo><mn>6</mn><mo>,</mo><mn>1</mn><mo stretchy="true">)</mo></mrow></math>在图 12.7 中表示出来。类似地，操作<math alttext="" display="inline"><mrow><mi>e</mi><mi>s</mi><mi>t</mi><mi>i</mi><mi>m</mi><mi>a</mi><mi>t</mi><mi>e</mi><mo stretchy="true">(</mo><mn>5</mn><mo stretchy="true">)</mo></mrow></math>和<math alttext="" display="inline"><mrow><mi>e</mi><mi>s</mi><mi>t</mi><mi>i</mi><mi>m</mi><mi>a</mi><mi>t</mi><mi>e</mi><mo stretchy="true">(</mo><mn>12</mn><mo stretchy="true">)</mo></mrow></math>分别在图 12.8 和 12.9 中表示出来。从图 12.9 可以清楚地看出，对元素 12 的查询结果是过估计的。值得注意的是，对计数蓝图的估计查询也可能导致欠估计。

**表 12.3**

经过两个哈希函数 *h* 和 *g* 后元素的结果。

![表 12.3](img/tab12_3.jpg)![图 12.7](img/fig12_7.jpg)

**图 12.7.**

在 Count-sketch 中进行更新操作。

![图 12.8](img/fig12_8.jpg)

**图 12.8.**

在 Count-sketch 中进行估算操作。

![图 12.9](img/fig12_9.jpg)

**图 12.9.**

在表示过估算的 Count-sketch 中进行估算操作。

## 12.4 采用保守更新的 Count-Min Sketch

保守更新背后的主要逻辑是“最小增量”，只有在确保估算的准确性的最小增量的情况下才会增加计数。保守更新（CU）可应用于 Count-Min-sketch，也可应用于频谱 BF。 CMS 的保守更新（CM-CU）被作者在[76] 中引入，目的是减少结果中的误报正错误。特别地，[88] 的作者得出结论，CMS 与保守更新最小化了超估计误差约 1.5 倍。与 CMS 类似，CM-CU 也使用大小为 <math alttext="" display="inline"><mrow><mi>w</mi><mo>*</mo><mi>d</mi></mrow></math> 的二维表，其中，*w* 是表的宽度，*d* 是表的深度。还使用 *k* 个哈希函数，等于表的深度。对于任何传入的项，只会增加最小量的计数。然而，CM-CU Sketch 不支持删除。 CM-CU Sketch 支持的操作如下所述：

+   更新(*q, c*): 该操作将元素*q*与计数*c*添加到草图中。要执行此操作，首先从草图的现有状态中使用 CMS 中解释的<math alttext="" display="inline"><mrow><mi>E</mi><mi>s</mi><mi>t</mi><mi>i</mi><mi>m</mi><mi>a</mi><mi>t</mi><mi>e</mi><mo stretchy="true">(</mo><mi>q</mi><mo stretchy="true">)</mo></mrow></math>过程计算元素*q*的近似频率（即通过取由*d*个哈希函数索引的值的最小值来完成此操作）。让我们将这个值称为<math alttext="" display="inline"><mrow><msub><mi>f</mi><mi>q</mi></msub></mrow></math>。接下来，比较对应于*k*个哈希函数的*k*个位置的值。在这里，在 CMS 中，仅当草图中的现有值小于<math alttext="" display="inline"><mrow><msub><mi>f</mi><mi>q</mi></msub><mo>+</mo><mn>1</mn></mrow></math>时，才会递增*k*个位置的值，否则值不会改变。这种条件更新类型确保了不必要的更新并减少了过度估计错误。为了使用以下方式更新*q*和计数*c*，首先计算<math alttext="" display="inline"><mrow><msub><mi>f</mi><mi>q</mi></msub></mrow></math>：

    <math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><msub><mi>f</mi><mi>q</mi></msub><mo>=</mo><mi>m</mi><mi>i</mi><msub><mi>n</mi><mi>k</mi></msub><mo>></mo><mi>s</mi><mi>k</mi><mi>e</mi><mi>t</mi><mi>c</mi><mi>h</mi><mo stretchy="false">[</mo><mi>k</mi><mo>,</mo><msub><mi>h</mi><mi>k</mi></msub><mo stretchy="false">(</mo><mi>q</mi><mo stretchy="false">)</mo><mo stretchy="false">]</mo><mo>></mo><mo>∀</mo><mo>></mo><mn>1</mn><mo>≤</mo><mi>k</mi><mo>≤</mo><mi>d</mi></mrow></mtd></mtr></mtable></mrow></math>(12.4)

    并根据以下方程式更新计数：

    <math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>s</mi><mi>k</mi><mi>e</mi><mi>t</mi><mi>c</mi><mi>h</mi><mo stretchy="false">[</mo><mi>k</mi><mo>,</mo><msub><mi>h</mi><mi>k</mi></msub><mo stretchy="false">(</mo><mi>q</mi><mo stretchy="false">)</mo><mo stretchy="false">]</mo><mo>←</mo><mi>m</mi><mi>a</mi><mi>x</mi><mo>{</mo><mi>s</mi><mi>k</mi><mi>e</mi><mi>t</mi><mi>c</mi><mi>h</mi><mo stretchy="false">[</mo><mi>k</mi><mo>,</mo><msub><mi>h</mi><mi>k</mi></msub><mo stretchy="false">(</mo><mi>q</mi><mo stretchy="false">)</mo><mo stretchy="false">]</mo><mo>,</mo><msub><mi>f</mi><mi>q</mi></msub><mo>+</mo><mi>c</mi><mo>}</mo></mrow></mtd></mtr></mtable></mrow></math>(12.5)

+   *估计(q)*: 它遵循与第 12.2 节中为 CMS 解释的相同程序 *Estimate(q)*。

更新操作示例已在 图 12.10 中表示。这里，操作 <math alttext="" display="inline"><mrow><mi>u</mi><mi>p</mi><mi>d</mi><mi>a</mi><mi>t</mi><mi>e</mi><mo stretchy="true">(</mo><mn>12</mn><mo>,</mo><mn>1</mn><mo stretchy="true">)</mo></mrow></math>, <math alttext="" display="inline"><mrow><mi>u</mi><mi>p</mi><mi>d</mi><mi>a</mi><mi>t</mi><mi>e</mi><mo stretchy="true">(</mo><mn>5</mn><mo>,</mo><mn>2</mn><mo stretchy="true">)</mo></mrow></math>, <math alttext="" display="inline"><mrow><mi>u</mi><mi>p</mi><mi>d</mi><mi>a</mi><mi>t</mi><mi>e</mi><mo stretchy="true">(</mo><mn>16</mn><mo>,</mo><mn>1</mn><mo stretchy="true">)</mo></mrow></math>, <math alttext="" display="inline"><mrow><mi>u</mi><mi>p</mi><mi>d</mi><mi>a</mi><mi>t</mi><mi>e</mi><mo stretchy="true">(</mo><mn>6</mn><mo>,</mo><mn>1</mn><mo stretchy="true">)</mo></mrow></math> 依次显示。所有这些元素的哈希输出在 表 12.2 中显示。类似地，操作 Estimate(6) 已在 图 12.11 中显示。实验得出的结论是误差率与 <math alttext="" display="inline"><mrow><mfrac><mn>1</mn><mi>M</mi></mfrac></mrow></math> 成正比，其中 *M* 是可用内存。

![图 12.10](img/fig12_10.jpg)

**图 12.10.**

在 CM-CU 轮廓中的更新操作。

![图 12.11](img/fig12_11.jpg)

**图 12.11.**

在 CM-CU 轮廓中估计操作。

## 活动

### 多项选择题

1.  保守更新的 count-min 背后的主要思想是什么？

    1.  最小增加

    1.  最小减少

    1.  最大增加

    1.  最大减少

1.  如果一个草图使用大小为 <math alttext="" display="inline"><mrow><mi>t</mi><mo>*</mo><mi>b</mi></mrow></math> 的表，其中 *t* 是行数，*b* 是列数，那么为了实现 CMS 需要多少个哈希函数？

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="true">(</mo><mi>t</mi><mo>+</mo><mi>b</mi><mo stretchy="true">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="true">(</mo><mi>b</mi><mo stretchy="true">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="true">(</mo><mi>t</mi><mo stretchy="true">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="true">(</mo><mi>t</mi><mo>*</mo><mi>b</mi><mo stretchy="true">)</mo></mrow></math>

1.  为了执行计数草图查询，使用了哪种集中趋势度量？

    1.  众数

    1.  中位数

    1.  平均值

    1.  范围

1.  2-D CMS 数组宽度增加时的错误率影响是什么？

    1.  错误率会变高

    1.  错误率会降低

    1.  错误可能是高的或低的

    1.  错误率与表的宽度之间没有关系

1.  以下提到的 BF 中哪个不支持删除？

    1.  计数 BF

    1.  DBF

    1.  稳定 BF

    1.  压缩 BF

1.  以下哪个是用于频率估计的确定性算法？

    1.  CMS

    1.  HLL

    1.  多数算法

    1.  以上全部

1.  CMS 中更新操作的时间复杂度是多少？

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="true">(</mo><mi>d</mi><mo stretchy="true">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="true">(</mo><mi>w</mi><mo stretchy="true">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="true">(</mo><mi>l</mi><mi>o</mi><mi>g</mi><mi>d</mi><mo stretchy="true">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>i</mi><mi>s</mi><mo>_</mo><mi>s</mi><mi>h</mi><mi>i</mi><mi>f</mi><mi>t</mi><mi>e</mi><mi>d</mi></mrow></math>

1.  CMS 的空间需求是多少？

    1.  线性

    1.  亚线性

    1.  超线性

    1.  对数

1\. a  2\. b  3\. b  4\. b  5\. c  6\. c  7\. a  8\. b

<hgroup>

# 13

# 近似相似性搜索查询概率数据结构

</hgroup>

## 13.1 简介

从系统生成的大型数据集可能包含重复或接近重复的数据。应用暴力技术来探索所有可能的组合可以得到精确的最近邻匹配，但这种方式是不可扩展的。此外，传统的聚类分析技术（例如，k-最近邻）需要二次或三次时间，对于大型数据集来说似乎不实用。而且，树结构方法，如 kd 树、BDD 树等，需要足够的空间和时间，因为这些方法在搜索时将给定的查询与每个记录进行比较以识别相似的记录。因此，需要一种能以低成本解决所需查询的高效相似性搜索方法。为了解决这个问题，研究人员提出使用高维相似性搜索的近似技术。

这一类别下的数据结构近似于高维数据的相似性搜索。有时，相似性搜索也称为近似最近邻搜索或接近搜索。在这种类型的问题中，感兴趣的不同特征，如文本文档、图像被视为点，距离度量用于识别两个对象之间的相似性。相似性搜索度量将一对集合映射到范围为[0,1]的相似性分数。具体而言，这里的目标是在高维属性空间中找到重复项或相似点簇。近似相似性搜索的用例包括在互联网上查找网页之间的相似性，定位相似的图像或音频/视频文件，数据去重，识别抄袭案例，识别恶意软件家族的变体等。从数学上讲，该问题被定义为：对于查询*q*，目标是找到项目*x*，使得<math alttext="" display="inline"><mrow><mtext>dis</mtext><mo>(</mo><mi>q</mi><mo>,</mo><mi>x</mi><mo>)</mo><mo>≤</mo><mo>(</mo><mn>1</mn><mo>+</mo><mi>ϵ</mi><mo>)</mo><mi>d</mi><mi>i</mi><mi>s</mi><msup><mrow><mo stretchy="false">(</mo><mi>q</mi><mo>,</mo><mi>x</mi><mo stretchy="false">)</mo></mrow><mo>∗</mo></msup></mrow></math>，其中，*ϵ*是最多估计的预期误差[212]。

近似相似性的基本原理也依赖于哈希，因为哈希将数据点转换为低维表示。哈希表查找和快速距离近似是哈希的两种技术，用于执行近似最近邻搜索。前者方法使用哈希表作为数据结构，由桶组成。每个项目*x*都被哈希到一个桶<mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow>中。然而，不同于传统的哈希算法，这里的哈希表旨在最大化相邻项碰撞的概率。相反，后者计算给定查询和参考项的哈希码之间的距离。随后，具有最小距离的参考项是最近邻的候选项。接下来，我们将介绍近似相似性搜索 PDS 的不同类型。

## 13.2 最小哈希

Andrie Border 引入了 minhashing 来检测 AltaVista 搜索引擎网页中的重复性[53], [54]。Minhash 基于 Jaccard 相似性概念来识别两个集合之间的相似性。两个集合的 Jaccard 相似性是两个集合的交集与并集的比值，表示为:

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>J</mi><mi>S</mi><mo stretchy="false">(</mo><msub><mi>S</mi><mn>1</mn></msub><mo>,</mo><msub><mi>S</mi><mn>2</mn></msub><mo stretchy="false">)</mo><mo>=</mo><mo>|</mo><msub><mi>S</mi><mn>1</mn></msub><mo>∩</mo><msub><mi>S</mi><mn>2</mn></msub><mo>|</mo><mo>/</mo><mo>|</mo><msub><mi>S</mi><mn>1</mn></msub><mo>∪</mo><msub><mi>S</mi><mn>2</mn></msub><mo>|</mo><mo>.</mo></mrow></mtd></mtr></mtable></mrow></math>(13.1)

例如，取两个小集合，<math alttext="" display="inline"><mrow><mi>s</mi><mi>e</mi><mi>t</mi><mi>A</mi><mo>=</mo><mn>10</mn><mo>,</mo><mn>113</mn><mo>,</mo><mn>2</mn><mo>,</mo><mn>55</mn><mo>,</mo><mn>12</mn></mrow></math> 和 <math alttext="" display="inline"><mrow><mi>s</mi><mi>e</mi><mi>t</mi><mi>B</mi><mo>=</mo><mn>10</mn><mo>,</mo><mn>3</mn><mo>,</mo><mn>56</mn><mo>,</mo><mn>7</mn><mo>,</mo><mn>9</mn></mrow></math>。可以注意到这两个集合之间有 2 个共同项，两个集合中总共有 10 个唯一项。因此，集合 A 和 B 的 Jaccard 相似度为 <math alttext="" display="inline"><mrow><mfrac><mn>2</mn><mn>9</mn></mfrac></mrow></math>。尽管计算两个集合之间的交集和并集是一项昂贵的操作。然而，为了计算文档之间的相似性，文档也可以表示为集合。Shingling 是将文档转换为集合的一种流行方式之一。*k*-shingles 被定义为给定文档的所有可能的 *k* 大小的不可重复子字符串的集合。一个由 *n* 个单词组成的文档，具有 *k*-shingles 的集合占用 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>k</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math> 的空间。假设一个文档由一个小句组成：“对大量的二进制程序进行聚类是一个困难的任务”。因此，5 个词长的 shingles 为:

+   对大量的二进制进行聚类

+   大量的二进制程序

+   二进制程序的数量是

+   二进制程序的数量是一个

+   二进制程序是一个困难的

+   编程是一个困难的任务

因此，文档作为一个集合是：（“聚类大量的二进制”，“大量的二进制程序”，“二进制程序的数量”，“二进制程序是一个”，“二进制程序是一个困难的”，“程序是一个困难的任务”）。 计算 Jaccard 相似性的时间复杂度为<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><msub><mi>n</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></math> ，因为总共有<math alttext="" display="inline"><mrow><mfrac><mrow><mi>n</mi><mo stretchy="false">(</mo><mi>n</mi><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo></mrow><mn>2</mn></mfrac></mrow></math> 次比较。

此外，一组大集合也可以用一个布尔矩阵表示。为了将集合表示为布尔矩阵，矩阵的行包含通用集合的元素，而矩阵的列包含所有集合。矩阵的第*r*行和第*c*列的条目仅当行*r*的集合是列*c*的成员时为 1，否则为零。在这种情况下，列相似性是具有列值为 1 的行的 Jaccard 相似性。为了理解这一点，考虑具有值的三列 C1、C2、C3：从 Table 13.1 <math alttext="" display="inline"><mrow><mi>S</mi><mi>i</mi><mi>m</mi><mo stretchy="false">(</mo><msub><mi>C</mi><mn>1</mn></msub><mo>,</mo><msub><mi>C</mi><mn>2</mn></msub><mo stretchy="false">)</mo><mo>=</mo><mfrac><mn>2</mn><mn>5</mn></mfrac></mrow></math>，因为列 C1 和 C2 都有两行条目为 1。因此，列 C1 和 C2 代表的集合的交集为 2。此外，有行至少有一列为 1。因此，表示的集合的并集为 5。因此，Jaccard 相似性为<math alttext="" display="inline"><mrow><mfrac><mn>2</mn><mn>5</mn></mfrac></mrow></math>，即 40%。同样，<math alttext="" display="inline"><mrow><mi>S</mi><mi>i</mi><mi>m</mi><mo stretchy="false">(</mo><msub><mi>C</mi><mn>1</mn></msub><mo>,</mo><msub><mi>C</mi><mn>3</mn></msub><mo stretchy="false">)</mo><mo>=</mo><mfrac><mn>1</mn><mn>5</mn></mfrac></mrow></math>。值得注意的是，这个矩阵不是稀疏的，计算这种情况的 Jaccard 相似性是相当简单的。然而，用这种表示的结果矩阵是稀疏的，即它的零元素比 1 多，这对内存来说是一种负担。从 Table 13.1 <math alttext="" display="inline"><mrow><mi>S</mi><mi>i</mi><mi>m</mi><mo stretchy="false">(</mo><msub><mi>C</mi><mn>1</mn></msub><mo>,</mo><msub><mi>C</mi><mn>2</mn></msub><mo stretchy="false">)</mo><mo>=</mo><mfrac><mn>2</mn><mn>5</mn></mfrac></mrow></math>，因为列 C1 和 C2 都有两行条目为 1。因此，列 C1 和 C2 代表的集合的交集为 2。此外，有行至少有一列为 1。因此，表示的集合的并集为 5。因此，Jaccard 相似性为<math alttext="" display="inline"><mrow><mfrac><mn>2</mn><mn>5</mn></mfrac></mrow></math>，即 40%。同样，<math alttext="" display="inline"><mrow><mi>S</mi><mi>i</mi><mi>m</mi><mo stretchy="false">(</mo><msub><mi>C</mi><mn>1</mn></msub><mo>,</mo><msub><mi>C</mn>

**表 13.1**

理解最小哈希。

| C1 | C2 | C3 |
| --- | --- | --- |
| 0 | 1 | 1 |
| 1 | 1 | 0 |
| 1 | 0 | 1 |
| 0 | 0 | 0 |
| 1 | 1 | 0 |
| 0 | 1 | 1 |

+   随机排列行。

+   计算最小哈希值，<math alttext="" display="inline"><mrow><mi>M</mi><mi>H</mi><mo stretchy="false">(</mo><mi>C</mi><mo stretchy="false">)</mo></mrow></math> =在列 *C* 中第一个含 1 的行的索引（在排列后）。

+   同样，使用多个独立的哈希函数，并为每个列创建一个签名，使得签名矩阵有 *h* 行。这些最小哈希函数只选取一次，并且相同的最小哈希函数集应用于每个列。值得注意的是，大矩阵产生较少的错误。

+   Sim(C1, C2)= Sim(Sig(C1), Sig(C2)，即，两个集合之间的相似性是最小哈希值相符的排列分数。

让我们通过一个例子来理解这个概念。考虑一个有 5 列 7 行的输入矩阵，如图 13.1 所示。这些列按顺序 P1、P2、P3 进行了三次排列。因此，结果签名矩阵有 3 行（每行对应一个排列）和 5 列。排列 1 的最小哈希值分别为<math alttext="" display="inline"><mrow><mn>2</mn><mo>−</mo><mn>1</mn><mo>−</mo><mn>2</mn><mo>−</mo><mn>3</mn><mo>−</mo><mn>4</mn></mrow></math>，原因如下所述：第 5 行是第一个顺序，第 4 行是第二个，依此类推。显然，第 5 行在第二列中有 1，因此第二列在签名矩阵中得到了其第一个最小哈希值，接下来分析第 4 行。由于第 4 行的列 1 和 3 都为 1，并且这两列尚未被分配值。因此，这两列在签名矩阵中都得到了值 2。接下来，扫描第 2 行，它在第 2 和第 4 列中有 1。由于第 2 列已经有一个最小哈希值，因此只有第 4 列在签名矩阵中得到了值 3。类似地，第 5 列得到值 4。值得注意的是，我们已经发现了每列的最小哈希值，因此没有继续移动的必要。

![图 13.1](img/fig13_1.jpg)

**图 13.1.**

理解最小哈希。

**令人惊讶的特性**

如果考虑所有可能的行排列，则观察到：

<math alttext="" display="inline"><mrow><mi>P</mi><mo stretchy="false">[</mo><mi>M</mi><mi>H</mi><mo stretchy="false">(</mo><msub><mi>C</mi><mn>1</mn></msub><mo stretchy="false">)</mo><mi>M</mi><mi>H</mi><mo stretchy="false">(</mo><msub><mi>C</mi><mn>2</mn></msub><mo stretchy="false">)</mo><mo stretchy="false">]</mo><mo>=</mo><mi>J</mi><mi>S</mi><mo stretchy="false">(</mo><msub><mi>C</mi><mn>1</mn></msub><mo>,</mo><msub><mi>C</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></math>

不幸的是，对于大型数据集，随机排列很难选择。此外，为大量条目表示随机排列需要大量空间。此外，按照任何这些排列之一的顺序访问行需要许多磁盘访问以获取每行，这显然是耗时的。

让我们来看一下更好的最小哈希实现。其思想是模拟排列而不实际对行进行排列。在这个实现中，为每个最小哈希函数选择了一个普通的哈希函数<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">)</mo></mrow></math>，将整数哈希到某个桶中。我们假设排列中行*r*的位置为<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>r</mi><mo stretchy="false">)</mo></mrow></math>。下面是获取签名矩阵的步骤。

+   而不是对行进行排列，选择一些普通的哈希函数，每个哈希函数对应我们想模拟的每个最小哈希函数。

+   对于每个列*C*和每个哈希函数<math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub></mrow></math>，保持一个插槽<math alttext="" display="inline"><mrow><mi>M</mi><mo stretchy="false">(</mo><mi>i</mi><mo>,</mo><mi>c</mi><mo stretchy="false">)</mo></mrow></math>。例如，插槽的数量是<math alttext="" display="inline"><mrow><mn>100</mn><mo>*</mo><mi>n</mi><mi>u</mi><mi>m</mi><mi>b</mi><mi>e</mi><mi>r</mi><mi>o</mi><mi>f</mi><mi>c</mi><mi>o</mi><mi>l</mi><mi>u</mi><mi>m</mi><mi>n</mi><mi>s</mi></mrow></math>。

+   将所有插槽<math alttext="" display="inline"><mrow><mi>M</mi><mo stretchy="false">(</mo><mi>i</mi><mo>,</mo><mi>c</mi><mo stretchy="false">)</mo></mrow></math>初始化为无穷大。

+   为了计算最小哈希签名，<math alttext="" display="inline"><mrow><mi>M</mi><mo stretchy="false">(</mo><mi>i</mi><mo>,</mo><mi>c</mi><mo stretchy="false">)</mo></mrow></math> 应始终包含对于那些列 *C* 在行 *r* 中有 1 的最小值 <math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>r</mi><mo stretchy="false">)</mo></mrow></math>。

**算法 4** 最小哈希算法

上述方法的算法已在算法 4 中显示。

1: **对于** 每一行 r **执行**

2:**对于** 每一个哈希函数 **执行**

3:计算 <math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>r</mi><mo stretchy="false">)</mo></mrow></math>;

4:**对于** 每一列 c **执行**

5:**如果** 列 c 在行 r 中有 1 **那么**

6:**对于** 每一个哈希函数 <math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub></mrow></math> **执行**

7:**如果** hi(r) ¡ M(i,c) **那么** M(i,c) ← hi(r);

8:**结束 如果**

9:**结束 for**

10:**结束 如果**

11:**结束 for**

12:**结束 for**

13: **结束 for**

此实现既快速又使用固定的内存占用。尽管签名矩阵相对较少地占用空间来表示文档签名，但仍需要 <math alttext="" display="inline"><mrow><mfenced close=")" open="("><mtable><mtr><mtd><mi>n</mi></mtd></mtr><mtr><mtd><mn>2</mn></mtd></mtr></mtable></mfenced><mo stretchy="false">(</mo><mi>O</mi><mo stretchy="false">(</mo><msup><mi>n</mi><mn>2</mn></msup><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow></math> 的近似时间来找到相似的比较对。要通过示例理解这个概念，请考虑一个具有 2 列和 5 行的矩阵，如 图 13.2 中所示。这里使用了两个哈希函数，即 <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mi>x</mi><mi>m</mi><mi>o</mi><mi>d</mi><mn>5</mn></mrow></math> 和 <math alttext="" display="inline"><mrow><mi>g</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>2</mn><mi>x</mi><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>5</mn></mrow></math>。因此，最终的签名矩阵将长度为 2。

![图 13.2](img/fig13_2.jpg)

**图 13.2.**

理解最小哈希（minhashing）。

最初，所有槽都是无穷大。第一行在第一列为 1，在第二列为 0。因此，第二列的组件都没有改变，仍然是无穷大，但是第一列的值会被改变为<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math>和<math alttext="" display="inline"><mrow><mi>g</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math>的值，即 1 和 3。现在，考虑第二行，两列的值都为 1，<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mn>2</mn><mo stretchy="false">)</mo><mo>=</mo><mn>2</mn></mrow></math>，<math alttext="" display="inline"><mrow><mi>g</mi><mo stretchy="false">(</mo><mn>2</mn><mo stretchy="false">)</mo><mo>=</mo><mn>0</mn></mrow></math>。简单来说，对于第二列，无穷大的值被哈希值取代，而对于第一列<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mn>2</mn><mo stretchy="false">)</mo><mo>></mo><mi>h</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math>，所以这个值不会改变，<math alttext="" display="inline"><mrow><mi>g</mi><mo stretchy="false">(</mo><mn>2</mn><mo stretchy="false">)</mo><mo><</mo><mi>g</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math>，所以第二个组件的值将被改变为 0。由于 minhash 函数使用每个哈希函数遇到的最小值，因此 minhash 这个名字是有道理的。同样，观察其他行，最终的列签名矩阵分别显示在图 13.2 中。代码 13.4 展示了使用内置哈希函数和 *h* 按位异或掩码进行哈希的 Python 实现。

![](img/list13_1.jpg)![](img/list13_2a.jpg)![](img/list13_2b.jpg)![](img/list13_2c.jpg)![](img/list13_3a.jpg)![](img/list13_3b.jpg)

## 13.3 局部敏感哈希

局部敏感哈希（LSH）旨在找到与给定查询最近的数据点。在这里，也利用了哈希表来找到足够接近的匹配项。检测抄袭、按主题分类、推荐系统、实体解析、全基因组关联研究、音视频指纹等是 LSH 被使用的一些关键领域。LSH 使用的思想是“重用碰撞”，即与其避免碰撞，不如使几乎相邻的数据点发生碰撞。因此，在 LSH 中，附近或足够接近的数据点被放在同一个桶中，而远离的数据点被放在不同的桶中。更正式地说，算法选择了一个哈希族*H*，如果这个哈希族是局部敏感的，则：

当*A*足够接近*B*时，<math alttext="" display="inline"><mrow><mi>P</mi><mi>r</mi><mo stretchy="false">[</mo><mi>h</mi><mo stretchy="false">(</mo><mi>A</mi><mo stretchy="false">)</mo><mo>=</mo><mi>h</mi><mo stretchy="false">(</mo><mi>B</mi><mo stretchy="false">)</mo><mo stretchy="false">]</mo></mrow></math>较高。

当*A*远离*B*时，<math alttext="" display="inline"><mrow><mi>P</mi><mi>r</mi><mo stretchy="false">[</mo><mi>h</mi><mo stretchy="false">(</mo><mi>A</mi><mo stretchy="false">)</mo><mo>=</mo><mi>h</mi><mo stretchy="false">(</mo><mi>B</mi><mo stretchy="false">)</mo><mo stretchy="false">]</mo></mrow></math>较低。

LSH 是一个多次对项目进行哈希处理并仅比较至少一次落入同一桶中的项目的想法。然而，LSH 不能保证提供精确的答案，但它们给出了一个很好的近似值。为了实现 LSH，

+   第一步是对给定文档集进行 shingling 处理。

+   第二步是执行 minhashing，以签名形式输出集合的短整数表示。

    值得注意的是，minhash 将大型集合转换为使用哈希的短签名，同时保留相似性，而 LSH 进一步找到可能相似的签名对。

+   第三步是执行局部敏感哈希，旨在找到一小部分仅用于相似性检查的签名候选对列表。而不是针对一组所有对进行相似性检查，只对一小部分候选对进行评估。对于 minhash 签名矩阵，使用多个哈希函数将列哈希到不同的桶中，并且即使一次也将哈希到相同桶的文档被称为候选对。

    LSH 不是检测完全相似的文档，而是找到文档之间大于*t*的相似度。因此，如果 min-hash 签名矩阵的两列 C1 和 C2 在至少*t*的行签名中的签名一致，则两列是候选对。要对单个列执行哈希，

    +   首先将签名矩阵分成*b*个带，每个带有*r*行。

    +   在任何*k*个桶中的每个列的每个带中哈希。为了更高效，尽可能取大的*k*。

    +   识别哈希到至少 1 个带的相同桶的候选对。

    +   应选择*b*和*r*以实现最相似的对和少数不相似的对，同时消除误报和漏报。下面讨论了选择*b*和*r*的更多见解。

    每个带的带分区和哈希函数计算的概念在图 13.3 和 13.4 中表示。

+   最后，访问主内存以测试候选对是否真的具有相似的签名。

![图 13.3](img/fig13_3.jpg)

**图 13.3.**

LSH 中的带分区。

![图 13.4](img/fig13_4.jpg)

**图 13.4.**

一个带的哈希函数。

观察

对于一个包含 100 行的签名矩阵，如果我们选择 25 个 4 个签名的组，则两个给定文档落入相同哈希桶的概率较高，因为这两个文档将被哈希 20 次（每个组一次），并且每个组中只有少数签名进行比较，即仅有 5 个，与每个组有 10 个签名的 10 个组相比。因此，如果选择更多的组，误报的可能性就更高。相反，如果选择的组数较低，则误报的可能性会增加。

假设签名矩阵中有 100,000 列和 100 行，这意味着签名矩阵的大小为 100*100000。假设选择的组数为 20，每组有 5 个签名。为了理解误报和漏报的存在，考虑两种情况：

**案例 1**

假设相似度阈值为 80%，即我们希望检索出所有 80% 相似的文档对。

两列 C1、C2 在特定组中相同的概率: <math alttext="" display="inline"><mrow><msup><mrow><mo stretchy="false">(</mo><mn>0.8</mn><mo stretchy="false">)</mo></mrow><mn>5</mn></msup><mo>=</mo><mn>0.32768</mn></mrow></math>。

两列 C1、C2 在任何 20 个组中都不相同的概率: <math alttext="" display="inline"><mrow><msup><mrow><mo stretchy="false">(</mo><mn>1</mn><mo>−</mo><mn>0.328</mn><mo stretchy="false">)</mo></mrow><mrow><mn>20</mn></mrow></msup><mo>=</mo><mn>0.00035</mn></mrow></math>，这意味着大约 <math alttext="" display="inline"><mrow><mfrac><mn>1</mn><mrow><mn>3000</mn></mrow></mfrac></mrow></math> 的真正 80% 相似集合是误报的否定。

**案例 2**

再举一个两个文档相似度为 40% 的情况。

两列 C1、C2 在特定组中相同的概率: <math alttext="" display="inline"><mrow><msup><mrow><mo stretchy="false">(</mo><mn>0.4</mn><mo stretchy="false">)</mo></mrow><mn>5</mn></msup><mo>=</mo><mn>0.01</mn></mrow></math>。

因此，两列 C1、C2 至少在 20 个带中的一个中相同的概率为：<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mn>1</mn><mo>−</mo><mo stretchy="false">(</mo><mn>1</mn><mo>−</mo><mn>0.01</mn><mo stretchy="false">)</mo><mo stretchy="false">)</mo><mo>=</mo><mn>0.19</mn></mrow></math>。这意味着假阳性的概率约为 20%。

因此，应选择 *b* 和 *r* 以达到最低的假阳性和假阴性率。

![](img/list13_4a.jpg)![](img/list13_4b.jpg)

### 13.3.1 Simhash

Simhash 是 LSH 的一种变体，与典型的加密算法不同，Simhash 还试图使几乎相似的项目发生碰撞的概率最大化 [62]。它由摩西·尚卡尔提出，用于检测近似重复的文档。Simhash 基于符号随机投影的概念 [34]。它基本上降低了数据的维度，并将高维数据映射到 *f* 位指纹 (*f* 是从哈希生成的非常小的值)。

Simhash 指纹通常是从文档的任何特征生成的。文档特征通常是 *k* -word shingles 或单词频率。要计算 simhash 指纹，请按照以下步骤进行：

+   生成文档的特征。

+   选择一个哈希大小 *f*（8,16,32 等），并维护一个 *f* 维向量 *V*，并将向量的所有维度初始化为 0。

+   将每个特征哈希到 *f* 位哈希值（每个特征的这些唯一的 f 位增加/减少向量的最终 *f* 值）。

+   对于每个唯一的 *f* 位哈希值：

    <math alttext="" display="inline"><mrow><mi>i</mi><mi>f</mi><mi>b</mi><mi>i</mi><msub><mi>t</mi><mi>i</mi></msub><mi>o</mi><mi>f</mi><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mi>i</mi><mi>s</mi><mi>s</mi><mi>e</mi><mi>t</mi><mi>t</mi><mi>h</mi><mi>e</mi><mi>n</mi><mo>,</mo><mi>a</mi><mi>d</mi><mi>d</mi><mn>1</mn><mi>t</mi><mi>o</mi><mi>f</mi><mi>i</mi><mi>n</mi><mi>a</mi><mi>l</mi><mi>f</mi><mo>−</mo><mi>b</mi><mi>i</mi><mi>t</mi><mi>v</mi><mi>e</mi><mi>c</mi><mi>t</mi><mi>o</mi><mi>r</mi><mo stretchy="false">(</mo><mi>V</mi><mo stretchy="false">[</mo><mi>i</mi><mo stretchy="false">]</mo><mo stretchy="false">)</mo></mrow></math>

    *如果哈希的位 iof 未设置*，*则从 V[i]中减去 1*。

+   最终的 simhash 位向量为

    当 <math alttext="" display="inline"><mrow><mi>V</mi><mo>[</mo><mi>i</mi><mo>]</mo><mo>></mo><mn>0</mn></mrow></math> 时，<math alttext="" display="inline"><mrow><mi>b</mi><mi>i</mi><msub><mi>t</mi><mi>i</mi></msub></mrow></math> 设为 1，否则设为 0。

例如，取一句话“数据结构”。

+   首先，将所有大写单词转换为小写单词，并分成 3 个单词的 shingles，即“dat”，“ata”，“tas”，“ast”，“str”，“tru”，“ruc”，“uct”，“ctu”，“tur”，“ure”，“res”。

+   对每个 shingle 进行哈希

    <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>d</mi><mi>a</mi><mi>t</mi><mo stretchy="false">)</mo><mo>=</mo><mn>10110000</mn></mrow></math>

    <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>a</mi><mi>t</mi><mi>a</mi><mo stretchy="false">)</mo><mo>=</mo><mn>10100001</mn></mrow></math>

    <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>t</mi><mi>a</mi><mi>s</mi><mo stretchy="false">)</mo><mo>=</mo><mn>10110010</mn></mrow></math>

    <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>a</mi><mi>s</mi><mi>t</mi><mo stretchy="false">)</mo><mo>=</mo><mn>01100011</mn></mrow></math>

    <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>s</mi><mi>t</mi><mi>r</mi><mo stretchy="false">)</mo><mo>=</mo><mn>10110100</mn></mrow></math>

    <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>t</mi><mi>r</mi><mi>u</mi><mo stretchy="false">)</mo><mo>=</mo><mn>00100101</mn></mrow></math>

    <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>r</mi><mi>u</mi><mi>c</mi><mo stretchy="false">)</mo><mo>=</mo><mn>10110110</mn></mrow></math>

    <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>u</mi><mi>c</mi><mi>t</mi><mo stretchy="false">)</mo><mo>=</mo><mn>10111000</mn></mrow></math>

    <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>t</mi><mi>u</mi><mi>r</mi><mo stretchy="false">)</mo><mo>=</mo><mn>01101001</mn></mrow></math>

    <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>u</mi><mi>r</mi><mi>e</mi><mo stretchy="false">)</mo><mo>=</mo><mn>10111010</mn></mrow></math>

    <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>r</mi><mi>e</mi><mi>s</mi><mo stretchy="false">)</mo><mo>=</mo><mn>01101011</mn></mrow></math>

+   *如果<math alttext="" display="inline"><mrow><mi>s</mi><mi>h</mi><mi>i</mi><mi>n</mi><mi>g</mi><mi>l</mi><mi>e</mi><mo>.</mo><mi>h</mi><mo stretchy="false">[</mo><mi>i</mi><mo stretchy="false">]</mo><mo>=</mo><mo>=</mo><mn>1</mn></mrow></math>*，则*V[i]*增加 1

    *如果<math alttext="" display="inline"><mrow><mi>s</mi><mi>h</mi><mi>i</mi><mi>n</mi><mi>g</mi><mi>l</mi><mi>e</mi><mo>.</mo><mi>h</mi><mo stretchy="false">[</mo><mi>i</mi><mo stretchy="false">]</mo><mo>=</mo><mo>=</mo><mn>0</mn></mrow></math>*，则*V[i]*减少 1

    *V*向量由图 13.5 表示。

    ![图 13.5](img/fig13_5.jpg)

    **图 13.5.**

    Simhash 示例。

+   计算最终的 simhash 指纹：

    如果<math alttext="" display="inline"><mrow><mi>V</mi><mo>[</mo><mi>i</mi><mo>]</mo><mo>></mo><mn>0</mn></mrow></math>，则*simhash[i]* = 1

    否则*simhash[i]*= 0

    因此，simhash 指纹为<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mn>10110000</mn><mo stretchy="false">)</mo></mrow></math>。

    要检测文档*d*与给定一组文档的相似性。一个解决方案是计算*d*的 simhash 指纹与所有其他文档 simhash 指纹值的汉明距离。然而，随着问题规模的增长，这种方法并不高效。在另一种方法中，与其将文档*d*的所有 simhash 位与文档集合中的所有位进行比较，不如只比较一些特定的位位置。如果它们匹配，则计算两个 simhash 指纹的汉明距离。

## 活动

### 多项选择题

1.  以下哪一个不是 PDS 相似性搜索的一种类型？

    1.  最小哈希

    1.  Maxhash

    1.  LSH

    1.  Simhash

1.  一个文档中包含 n 个单词的 k-shingles 集合所占用的空间是？

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><msup><mi>k</mi><mn>2</mn></msup><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>k</mi><mo>+</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><msup><mi>n</mi><mn>3</mn></msup><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>k</mi><mo>*</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

1.  用于比较相似对的签名矩阵所消耗的时间是多少？

    1.  <math alttext="" display="inline"><mrow><mfenced close=")" open="("><mtable><mtr><mtd><mi>n</mi></mtd></mtr><mtr><mtd><mn>2</mn></mtd></mtr></mtable></mfenced><mo stretchy="false">(</mo><mi>O</mi><mo stretchy="false">(</mo><msup><mi>n</mi><mn>2</mn></msup><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><msup><mi>n</mi><mn>4</mn></msup><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><mi>g</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

1.  一般来说，对于两列 C1 和 C2，签名不在任何频段上达成一致的概率是多少？

    1.  <math alttext="" display="inline"><mrow><msup><mrow><mo stretchy="false">(</mo><mn>1</mn><mo>−</mo><msup><mi>s</mi><mi>b</mi></msup><mo stretchy="false">)</mo></mrow><mi>r</mi></msup></mrow></math>

    1.  <math alttext="" display="inline"><mrow><msup><mrow><mo stretchy="false">(</mo><mn>1</mn><mo>−</mo><msup><mi>s</mi><mi>b</mi></msup><mo stretchy="false">)</mo></mrow><mi>r</mi></msup></mrow></math>

    1.  <math alttext="" display="inline"><mrow><msup><mrow><mo stretchy="false">(</mo><mn>1</mn><mo>−</mo><msup><mi>r</mi><mi>s</mi></msup><mo stretchy="false">)</mo></mrow><mi>b</mi></msup></mrow></math>

    1.  <math alttext="" display="inline"><mrow><msup><mrow><mo stretchy="false">(</mo><mn>1</mn><mo>−</mo><msup><mi>b</mi><mi>r</mi></msup><mo stretchy="false">)</mo></mrow><mi>s</mi></msup></mrow></math>

1.  以下哪项不是距离度量？

    1.  欧几里得距离

    1.  汉明距离

    1.  余弦距离

    1.  签名距离

1.  计算给定文档 *n* 的 Jaccard 相似度的时间复杂度是多少？

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><msup><mi>n</mi><mn>2</mn></msup><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><mi>g</mi><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><msup><mi>n</mi><mn>3</mn></msup><mo stretchy="false">)</mo></mrow></math>

    1.  <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>

1.  LSH 中更多的频段意味着：

    1.  较低的假阳性

    1.  较高的假阴性

    1.  较高的假阳性

    1.  较低的假阴性

1.  局部敏感哈希生成：

    1.  仅假阳性

    1.  仅假阴性

    1.  假阳性和假阴性都较高

    1.  假阳性和假阴性都不是
