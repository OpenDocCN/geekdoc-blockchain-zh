© 作者，独家许可给 Springer Nature Switzerland AG 2021

# 基于 Spark 的入侵检测系统使用实用粒子群优化聚类

Mohamed Aymen Ben HajKacem^(1), Mariem Moslah^(1) 和 Nadia Essoussi^(1) 

## 摘要

鉴于大型网络中数据的可用性增长，入侵检测系统成为一个重要挑战，因为它们需要有效的方法从这样的网络中发现攻击。本文提出了一种基于 Spark 的入侵检测系统，使用粒子群优化聚类，称为 IDS-SPSO，用于大规模数据，能够在可扩展性和准确性之间提供良好的权衡。据称，使用粒子群优化聚类可以避免初始聚类中心的敏感性问题以及过早收敛的问题。此外，我们在这项工作中提出利用基于 Spark 框架的并行处理。对几个大型真实入侵数据集进行的实验表明，所提出的入侵检测系统在可扩展性和聚类准确性方面的有效性。

关键词：入侵检测、大数据、聚类、PSO、Spark

## 1 引言

鉴于互联网的不断增长和普及，网络入侵检测成为提供信息保护和安全的重要挑战。这是因为用户数量和数据交换量巨大，难以区分正常连接和攻击。为此，入侵检测系统（IDSs）被设计用于处理大量数据，以保护系统免受网络攻击。

文献中对 IDSs 应用了几种机器学习技术 [1, 6, 11, 23, 26, 33]。聚类是用于将数据组织成相似数据点组的一种机器学习技术，也称为聚类 [18]。聚类方法主要可以分为五类，即层次、密度、网格、模型和分区方法 [39]。作为分区聚类方法之一的 K-means [24] 由于其简单性和线性时间复杂度而仍然是最有效的。然而，由于初始聚类中心的选择敏感，当未正确选择初始聚类中心时，它可能产生局部最优解 [10]。

为了解决这个问题，引入了几种优化算法来解决数据聚类问题[8, 14, 17, 20, 27, 31, 34]。基于变异算子的遗传优化算法被设计用来处理聚类任务[20]。模拟退火优化也被用于数据聚类[8]。粒子群优化（PSO）被提出来解决聚类问题，通过使用具有社会行为的多个搜索方向来增强聚类结果的质量[34]。在这些算法中，粒子群优化（PSO）因其效率而广受欢迎[29]。

另一方面，基于聚类的传统入侵检测方法难以应对网络流量规模较大的情况，并且在内存方面计算开销巨大。为了处理大规模数据，文献中设计了几种分布式聚类方法[2–5, 12, 15, 30, 40, 41]。其中大多数方法使用了 MapReduce 框架[13] 进行数据处理。然而，MapReduce 不适合迭代算法，因为它需要多次读写磁盘。Spark[9, 32] 被引入来克服 MapReduce 的局限性，特别适用于处理迭代算法。它是一个用于使用一组机器的内存并行处理大数据的框架。与 MapReduce 框架相比，Spark 在数据处理任务上更有效率，大约快 10 到 100 倍[7]。

本文提出了一种基于 Spark 的新型入侵检测系统（IDS-SPSO）。所提出的系统利用 PSO 聚类构建入侵检测模型。据我们所知，这是第一项使用 PSO 和 Spark 框架实现并行入侵检测系统的工作。旨在展示所提出的系统如何利用 Spark 和 PSO 处理真实的大规模入侵数据，以达到高准确性和可扩展性。

本文的剩余部分安排如下：第一部分介绍与粒子群优化（PSO）和并行框架相关的背景定义。第二部分讨论基于聚类的入侵检测方法领域的相关工作。然后，第三部分描述了所提出的并行入侵检测系统，而第四部分展示了在大规模真实入侵数据上进行的实验结果。最后，第五部分给出了结论性的评论和一些未来的工作。

## 2 初步

本节首先介绍与粒子群优化（PSO）相关的背景定义，然后介绍本文中使用的并行框架。

### 2.1 粒子群优化

粒子群优化（PSO）是由电气工程师埃伯哈特和社会心理学家肯迪引入的[29]。该算法旨在模拟鸟类寻找食物时的社会行为。当一只鸟发现一个食物区域时，它会向整个群体广播信息。因此，所有鸟都跟随它，这样它们提高了找到食物的概率，因为这是一项协作工作。因此，群体内鸟类的行为被转化为一种智能算法，能够解决多个优化问题。

PSO 是一种基于群体的优化算法。它由一群粒子组成，每个粒子代表优化问题的一个潜在解决方案。每个粒子 ![$$P_i$$](img/507793_1_En_11_Chapter_TeX_IEq1.png) 在时间 *t* 被其在搜索空间中的当前位置 ![$$x_{i}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq2.png)、速度 ![$$v_{i}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq3.png)、个人最佳位置 ![$$pbestP_{i}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq4.png) 和适应度值 ![$$pbestF_{i}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq5.png) 表征。个人最佳位置表示粒子曾经见过的最佳适应度值，其计算方式为：![$$\begin{aligned} pbestP_{i}(t+1)={\left\{ \begin{array}{ll} pbestP_{i}(t)\, if \, f( pbestP_{i}(t))&lt;= f(x_ {i}(t+1))\\ x_{i}(t+1) \, if \, f(pbestP_{i}(t)) &gt; f(x_{i}(t+1))\\ \end{array}\right. } \end{aligned}$$](img/507793_1_En_11_Chapter_TeX_Equ1.png)(1)个人最佳位置表示任何粒子曾经经历过的最佳适应度值，其计算方式为：![$$\begin{aligned} gbestP(t+1)= min \, (f(y) , f(gbestP(t))) \end{aligned}$$](img/507793_1_En_11_Chapter_TeX_Equ2.png)(2)其中 ![$$\, y \in \lbrace { pbestP_{0}(t),...,pbestP_{S}(t)\rbrace }$$](img/507793_1_En_11_Chapter_TeX_IEq6.png)。下列方程用于更新问题搜索空间内的粒子位置：![$$\begin{aligned} x_{i}(t+1) \leftarrow x_{i}(t)+v_{i}(t) \end{aligned}$$](img/507793_1_En_11_Chapter_TeX_Equ3.png)(3)而下列方程用于更新粒子速度：![$$\begin{aligned} v_{i}(t+1) \leftarrow w v_{i}(t)+c_{1}r_{1}(pbestP_{i}(t)-x_{i} (t))+c_{2}r_{2}(gbestP(t)-x_{i}(t)) \end{aligned}$$](img/507793_1_En_11_Chapter_TeX_Equ4.png)(4)其中 *w* 是惯性权重，![$$x_{i}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq7.png) 是粒子 ![$$P_i$$](img/507793_1_En_11_Chapter_TeX_IEq8.png) 在时间 *t* 的位置，![$$v_{i}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq9.png) 是粒子 ![$$P_i$$](img/507793_1_En_11_Chapter_TeX_IEq10.png) 在时间 *t* 的速度，![$$c_{1}$$](img/507793_1_En_11_Chapter_TeX_IEq11.png) 和 ![$$c_{2}$$](img/507793_1_En_11_Chapter_TeX_IEq12.png) 是两个加速系数，![$$r_{1}$$](img/507793_1_En_11_Chapter_TeX_IEq13.png) 和 ![$$r_{2}$$](img/507793_1_En_11_Chapter_TeX_IEq14.png) 是两个在区间 [0, 1] 中的随机值。PSO 的主要算法概述如算法 1\.![../images/507793_1_En_11_Chapter/507793_1_En_11_Figa_HTML.png](img/507793_1_En_11_Figa_HTML.png)

### 2.2 MapReduce 框架

MapReduce [13] 是用于数据处理的并行编程框架。如图 1 所示，MapReduce 由三个阶段组成，即 *map*、*shuffle* 和 *reduce*。每个阶段通过 ![$${&lt;}key/value{&gt;}$$](img/507793_1_En_11_Chapter_TeX_IEq15.png) 对来处理数据。映射阶段通过并行处理每个 ![$${&lt;}key^{}/value^{}{&gt;}$$](img/507793_1_En_11_Chapter_TeX_IEq16.png) 并生成一组中间 ![$${&lt;}key^{'}/value^{'}{&gt;}$$](img/507793_1_En_11_Chapter_TeX_IEq17.png) 对应用映射函数。然后，shuffle 阶段将所有共享相同中间键的中间值合并为列表。reduce 阶段应用 reduce 函数以组合与同一中间键关联的所有中间值。请注意，MapReduce 框架的实现可在 Hadoop [35] 中使用。MapReduce 的输入和输出存储在分布式文件系统中，称为 Hadoop 分布式文件系统（HDFS）。尽管 MapReduce 框架在处理大数据方面表现出色，但在执行迭代算法时不适用 [22]。因为它要求在每次迭代中从磁盘读取和写入数据，这可能会增加运行时间。![../images/507793_1_En_11_Chapter/507793_1_En_11_Fig1_HTML.png](img/507793_1_En_11_Fig1_HTML.png)

图 1

MapReduce 框架的流程图

### 2.3 Spark 框架

Spark 框架支持迭代计算，并且与 MapReduce 相比具有改进的处理速度，因为它利用了内存计算，使用弹性分布式数据集（RDD）进行计算。这些 RDD 可以缓存在内存中，以在多个连续操作中使用。Spark [42] 被引入以与 Hadoop [35] 一起运行，特别是通过从 HDFS 读取数据。此外，它提供了一组内存操作符，超出了标准的 MapReduce，旨在在分布式环境中比 MapReduce 更快地处理数据 [32]。Spark 框架提出了两种可以处理 RDD 的操作符，称为转换和动作。转换被设计为对所有记录执行函数并生成新的 RDD。Map、ReduceByKey 和 MapPartition 是转换的示例。动作被设计为向程序返回一个值，并将计算的最终结果存储在文件系统中。Filter 和 Count 是动作的示例。Spark 框架的数据流程如图 2 所示。![../images/507793_1_En_11_Chapter/507793_1_En_11_Fig2_HTML.png](img/507793_1_En_11_Fig2_HTML.png)

图 2

Spark 框架的数据流程

## 3 相关工作

文献中提出了基于机器学习技术的多个入侵检测方法[1, 6, 11, 23, 26, 33]。这些方法可以根据处理过程中所使用的数据类型是否标记来划分为监督或无监督。已设计出多种用于入侵检测系统的无监督方法，如基于聚类的方法[16, 19, 21, 28]。

Peng 等人[28]提出了用于入侵检测的小批量 k 均值聚类方法。他们采用主成分分析技术来减少所用数据集的维数，以增强聚类效率。然而，该方法仅考虑了入侵数据集的小样本量，可能导致质量损失。

Leung 等人[21]设计了一种基于密度的聚类方法，该方法采用频繁模式树来解决所用数据集的高维度问题。该方法在一百万条记录上进行了测试，并取得了良好的检测结果。

Jiang 等人[19]提出了一种模糊 c 均值聚类入侵检测方法，在其中采用了一种加权策略进行记录成员计算。该方法在五个数据样本上进行了测试，每个样本有一万条记录。结果显示，虽然存在高假阳性率，但检测率令人满意。

Harish 等人[16]提出了模糊 c 均值聚类方法的修改版本用于异常检测。他们采用主成分分析（PCA）作为特征选择技术来处理维度诅咒。此外，该方法基于使用高斯核作为距离度量来计算聚类中心和样本之间的距离。使用高斯核的优点是可以减少噪声的影响。

Wankhade 等人[36]提出了集成聚类方法来解决入侵检测问题。该方法基于 k 均值和分割与合并策略，用于选择准确的聚类中心数。实验结果表明，该策略可以提高检测率并降低误报率。

尽管现有入侵检测方法的表现已经得到验证，但它们无法对大规模网络流量进行组织。为了解决大规模入侵数据，提出了并行方法来执行分布式计算[2–5, 12, 15, 30, 40, 41]。其中大多数方法使用 MapReduce 作为并行编程框架。

Aljarah 等人 [2] 提出了一种通过 MapReduce 框架实现的并行入侵检测系统，称为 IDS-MRPSO。此外，他们通过解决入侵检测问题来构建聚类模型，采用 PSO 优化算法。最后，该系统使用真实的大规模入侵数据进行了测试，以评估可伸缩性和检测质量的不同训练子集大小。然而，MapReduce 框架不适合处理迭代算法，因为它在每次迭代时需要从磁盘读取和写入数据。

Wang 和 Han [37] 提出了基于并行 DPC 聚类的网络入侵检测方法。该方法基于截断距离策略，减少了数据点和聚类之间的比较次数。此外，他们提出使用 Spark 框架拟合 DPC 聚类以处理可伸缩性问题。然而，该方法仍对初始聚类中心的随机选择敏感 [10]。

我们提出的系统是第一个基于 Spark 框架拟合并行入侵检测系统的工作，这一点很重要。与 MapReduce 相比，Spark 是一个很好的内存并行框架，用于数据处理。

## 4 提出的入侵检测系统（IDS-SPSO）

大型网络流量数据需要高效的入侵检测系统来防御攻击。所提出的入侵检测系统结合了基于 PSO 算法的数据聚类过程。此外，PSO 聚类使用 Spark 框架进行分布，以便与大型网络流量一起扩展。如图 3 所示，所提出的入侵检测系统包括三个主要阶段：*预处理阶段*、*数据检测建模阶段* 和 *验证阶段*。第一阶段致力于应用一系列数据预处理技术，例如删除缺失值、消除分类特征和数据归一化。一旦完成预处理阶段，我们建议在第二阶段对训练数据应用基于 Spark 的 PSO 聚类方法（S-PSO） [25]，以生成全局最佳质心向量。在第三阶段，我们通过计算测试数据与最终全局最佳质心向量之间的距离来评估检测模型的质量。![../images/507793_1_En_11_Chapter/507793_1_En_11_Fig3_HTML.png](img/507793_1_En_11_Fig3_HTML.png)

图 3

IDS-SPSO 系统的流程图

### 4.1 预处理阶段

首先，我们移除包含缺失值的记录，因为在构建聚类时我们使用这些记录进行距离计算。因此，在距离计算中，我们不能使用包含缺失值的记录。然后，我们消除分类特征。在这项工作中，我们建议仅考虑数值特征进行距离计算，因为对于分类特征，我们需要一种特殊的距离度量。之后，我们对得到的数据集进行归一化处理，以避免某些特征在最小值和最大值之间具有较大的变化性而导致的偏差问题。归一化过程使用以下方程进行：![$$\begin{aligned} x_{ij_{new}}=\frac{x_{ij}-x_{j_{min}}}{x_{j_{max}}-x_{j_{min}}} \end{aligned}$$](img/507793_1_En_11_Chapter_TeX_Equ5.png)(5)其中 ![$$x_{ij}$$](img/507793_1_En_11_Chapter_TeX_IEq18.png) 是特征 *j* 的记录 *i* 的值，![$$x_{ij_{new}}$$](img/507793_1_En_11_Chapter_TeX_IEq19.png) 是特征 *j* 的记录 *i* 的归一化值，![$$x_{j_{min}}$$](img/507793_1_En_11_Chapter_TeX_IEq20.png) 是特征 *j* 的最小值，![$$x_{j_{max}}$$](img/507793_1_En_11_Chapter_TeX_IEq21.png) 是特征 *j* 的最大值。

### 4.2 数据检测建模阶段

数据检测建模阶段包括将 S-PSO 方法应用于预处理阶段产生的数据。作者提出了一种利用 Spark 的高效 PSO 聚类方法。对大规模数据的实验结果显示，随着数据的增加，S-PSO 的扩展性非常好，并且达到了良好的聚类准确性。与现有的 PSO 聚类的 MapReduce 实现相比，该方法仅需一次读取数据集。因此，它利用了 Spark 框架提供的灵活性，通过使用内存操作来减轻现有 MapReduce 解决方案的消耗时间 [2]。

S-PSO 方法由三个 MapReduce 作业组成，分别是*数据分配和适应度计算*、*个人和全局最佳更新*以及*位置和速度更新*。S-PSO 方法的主要流程如图 4 所示。![../images/507793_1_En_11_Chapter/507793_1_En_11_Fig4_HTML.png](img/507793_1_En_11_Fig4_HTML.png)

图 4

S-PSO 方法的流程图

#### 4.2.1 数据分配和适应度计算

在第一个 MapReduce 作业中，S-PSO 首先创建一个初始种群，该种群由粒子的位置、速度、个人最佳位置和个人最佳适应度组成。为此，粒子的位置从输入数据集中随机初始化，并且它们代表了初始聚类的中心。

然后，数据集被分成块，并且每个块被分配给一个映射函数。粒子的信息被广播到所有块中。映射函数首先通过计算距离将每个数据点分配给每个粒子中最近的聚类质心。然后，映射函数生成一个键值对作为输出，其中键表示粒子 ID 和质心 ID 的组合，值表示在粒子 ID 中数据点与质心 ID 之间的最小距离。

一旦所有数据点被分配给最近的聚类中心，就会应用一个 reduce 函数来计算适应度值，通过合并来自不同映射函数的数据来计算。 适应度值是使用总平方误差来计算的：![$$\begin{aligned} 适应度=\frac{\sum _{j=1}^{k}\sum _{i=1}^{|C_{j}|}d(r_{i},C_{j})}{k} \end{aligned}$$](img/507793_1_En_11_Chapter_TeX_Equ6.png)(6)其中![$$d(r_{i},C_{j})$$](img/507793_1_En_11_Chapter_TeX_IEq22.png)表示记录![$$r_{i}$$](img/507793_1_En_11_Chapter_TeX_IEq23.png)与聚类的质心![$$C_{j}$$](img/507793_1_En_11_Chapter_TeX_IEq24.png)之间的距离，![$$|C_{j}|$$](img/507793_1_En_11_Chapter_TeX_IEq25.png)表示分配给质心![$$C_{j}$$](img/507793_1_En_11_Chapter_TeX_IEq26.png)的记录数，*k*表示聚类数。 然后，减少函数生成键值对作为输出，其中键表示粒子 ID，值表示适应度值。假设![$$R=\lbrace {r_{1}...r_{n} \rbrace }$$](img/507793_1_En_11_Chapter_TeX_IEq27.png)是输入数据集。 假设![$$P(t)=\lbrace {P_{1}(t) ... P_{S}(t)\rbrace }$$](img/507793_1_En_11_Chapter_TeX_IEq28.png)是粒子信息集，其中![$$P_{c}(t)=\lbrace {x_{c}(t),v_{c}(t), pbestP_{c}(t),pbestF_{c}(t)\rbrace }$$](img/507793_1_En_11_Chapter_TeX_IEq29.png)表示迭代*t*中粒子*c*的信息，其中![$$x_{c}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq30.png)是位置，![$$v_{c}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq31.png)是速度，![$$pbestP_{c}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq32.png)是最佳位置，![$$pbestF_{c}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq33.png)是最佳适应度。 假设![$$F=\lbrace {F_{1}...F_{S} \rbrace }$$](img/507793_1_En_11_Chapter_TeX_IEq34.png)是适应度值集，其中![$$F_{c}$$](img/507793_1_En_11_Chapter_TeX_IEq35.png)是粒子*c*的适应度值。 数据分配和适应度计算 MapReduce 作业的主要步骤描述在算法 2 中。![../images/507793_1_En_11_Chapter/507793_1_En_11_Figb_HTML.png](img/507793_1_En_11_Figb_HTML.png)

#### 4.2.2 Pbest 和 Gbest 更新

一旦计算出新粒子的适应度，它们将自动分配到 RDDs 集合中。然而，个体最佳和全局最佳的计算并不是一个昂贵的操作。因此，它不需要以并行方式执行。然后，每个粒子更新其个体最佳位置和全局最佳位置。

让 ![$$pbestF(t)=\lbrace {pbestF_{1}(t) ... pbestF_{S}(t) \rbrace }$$](img/507793_1_En_11_Chapter_TeX_IEq36.png) 为个体最佳适应度值集合，其中 ![$$pbestF_{i}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq37.png) 是粒子 *i* 在迭代 *t* 时的个体最佳适应度。 

让 ![$$pbestP(t)=\lbrace { pbestP_{1}(t) ... pbestP_{S}(t) \rbrace }$$](img/507793_1_En_11_Chapter_TeX_IEq38.png) 为个体最佳位置集合，其中 ![$$pbestP_{1}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq39.png) 是粒子 *i* 在迭代 *t* 时的个体最佳位置。让 *gbestP* 为最佳粒子的位置。个体最佳和全局最佳更新 MapReduce 作业的主要步骤见算法 3\.![../images/507793_1_En_11_Chapter/507793_1_En_11_Figc_HTML.png](img/507793_1_En_11_Figc_HTML.png)

#### 4.2.3 位置和速度更新

在这个 MapReduce 作业中，S-PSO 首先将粒子信息分配给不同的映射函数。然后，映射函数使用公式 3 和 4 执行速度和位置更新。而减少函数将来自不同映射函数计算的所有中间键值对分组。一旦减少阶段完成，数据集和粒子信息将分布在存储在内存中的 RDDs 集合中，以供下一次迭代使用。有关 S-PSO 方法的更多详细信息，读者可以参考 [25]。

让 ![$$x(t)=\lbrace { x_{1}(t) ... x_{S}(t)\rbrace }$$](img/507793_1_En_11_Chapter_TeX_IEq40.png) 为位置值集合，其中 ![$$x_{i}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq41.png) 是粒子 *i* 在迭代 *t* 时的位置。让 ![$$v(t)=\lbrace {v_{1}(t) ... v_{S}(t) \rbrace }$$](img/507793_1_En_11_Chapter_TeX_IEq42.png) 为速度值集合，其中 ![$$v_{i}(t)$$](img/507793_1_En_11_Chapter_TeX_IEq43.png) 是粒子 *i* 在迭代 *t* 时的速度。位置和速度更新 MapReduce 作业的主要步骤见算法 4\.![../images/507793_1_En_11_Chapter/507793_1_En_11_Figd_HTML.png](img/507793_1_En_11_Figd_HTML.png)

### 4.3 评估阶段

一旦数据探测建模阶段完成，我们从最终粒子信息中提取全局最佳质心向量。在此阶段，我们通过计算测试记录与全局最佳质心向量之间的距离来评估检测模型。之后，我们通过计算距离将测试记录分配给它们最近的簇。评估阶段的主要步骤在算法 5 中描述。![../images/507793_1_En_11_Chapter/507793_1_En_11_Fige_HTML.png](img/507793_1_En_11_Fige_HTML.png)

最后，簇标记过程被应用于预测在测试数据分配步骤中生成的簇的正确标签。通过检索测试数据的真实标签与应用测试数据分配步骤生成的分配的簇之间的最大交集百分比来执行簇标签的分配。

图 5 说明了一个示例，更好地理解了簇标记过程。对于簇 ![$$C_1$$](img/507793_1_En_11_Chapter_TeX_IEq44.png)，正常记录的百分比是 ![$$\frac{3}{4}$$](img/507793_1_En_11_Chapter_TeX_IEq45.png)，而攻击记录的百分比是 ![$$\frac{1}{4}$$](img/507793_1_En_11_Chapter_TeX_IEq46.png)。因此，簇 ![$$C_1$$](img/507793_1_En_11_Chapter_TeX_IEq47.png) 是一个正常簇。对于簇 ![$$C_2$$](img/507793_1_En_11_Chapter_TeX_IEq48.png)，正常记录的百分比是 ![$$\frac{1}{3}$$](img/507793_1_En_11_Chapter_TeX_IEq49.png)，而攻击记录的百分比是 ![$$\frac{2}{3}$$](img/507793_1_En_11_Chapter_TeX_IEq50.png)。因此，簇 ![$$C_2$$](img/507793_1_En_11_Chapter_TeX_IEq51.png) 是一个攻击簇。类似地，对于簇 ![$$C_3$$](img/507793_1_En_11_Chapter_TeX_IEq52.png)，正常记录的百分比是 ![$$\frac{1}{3}$$](img/507793_1_En_11_Chapter_TeX_IEq53.png)，而攻击记录的百分比是 ![$$\frac{2}{3}$$](img/507793_1_En_11_Chapter_TeX_IEq54.png)。因此，簇 ![$$C_3$$](img/507793_1_En_11_Chapter_TeX_IEq55.png) 是一个攻击簇。![../images/507793_1_En_11_Chapter/507793_1_En_11_Fig5_HTML.png](img/507793_1_En_11_Fig5_HTML.png)

图 5

簇标记过程的说明性示例

### 4.4 时间复杂度分析

为了展示所提出系统的有效性，我们以下面的方式描述了对 S-PSO 方法时间复杂度的评估。给定*n*为数据集大小，*k*为聚类数，*c*为数据块数，*l*为迭代次数，*s*为粒子群大小。

PSO 算法中数据分配步骤是最昂贵的操作，因为它需要计算每个记录到粒子群中所有聚类的距离。然后，这个步骤必须重复多次直到收敛。因此，PSO 的时间复杂度为*O*(*n*.*k*.*s*.*l*)。S-PSO 首先将输入数据划分为可以以并行方式执行的*c*个块。因此，S-PSO 需要每次迭代处理*n*/*c*条记录。因此，S-PSO 的时间复杂度为*O*(*n*/*c*.*k*.*s*)。

## 5 实验和结果

### 5.1 环境

实验是在一组 4 台机器的集群上进行的，每个节点都有 2 核 2.30GHz 的 CPU E5400 和 1GB 内存。实验使用 Apache Spark 版本 2.1.1、scala 版本 2.1.1、Apache Hadoop 2.7.0 和 Ubuntu 16.04 进行。

### 5.2 数据集描述

为了评估所提出系统的性能，我们使用了一个大型入侵检测数据集^(1)，该数据集被用作 1999 年知识发现与数据挖掘中的基准。这个数据集包含了一组标准数据，其中包括了军事网络环境中各种正常和攻击连接。

收集的数据集中每个记录表示两个 IP 地址之间的连接。数据包含 4,898,431 个连接记录，这些记录被分类为正常流量和四种攻击，即拒绝服务（DoS）、探测（PRB）、远程到本地（R2L）和用户到根（U2R）。每个连接由 3 个分类特征和 38 个数值特征描述，共 41 个特征。

一组预处理技术被应用在训练和测试数据集上。我们首先删除具有缺失值的记录。然后，我们通过消除 3 个分类特征将特征数量减少到 38。最后，我们对训练和测试数据集应用归一化处理。表 1

数据样本摘要

| 数据集 | 连接数 | 正常 | 攻击 |
| --- | --- | --- | --- |
| Train20 | 979,686 | 194,556 | 785,130 |
| Train40 | 1,959,372 | 389,112 | 1,570,260 |
| Train80 | 3,918,745 | 778,225 | 3,140,520 |
| Train100 | 4,898,431 | 972,781 | 3,925,650 |

为了评估数据大小对检测器模型性能的影响，我们从整个训练数据集中提取了 4 个不同的数据样本。为了简化数据样本的命名，我们将使用以下符号 Train20、Train40、Train80 和 Train100 来表示存储整个训练数据集的 20%、40%、80%和 100%的提取数据集。这些数据集的统计信息总结在表 1 中。

### 5.3 评估措施

为了评估所提出系统的可扩展性，我们使用了速度提升（Speedup）度量[38]，该度量是通过固定数据集大小并改变机器数量来定义的。速度提升的定义如下：![$$\begin{aligned} Speedup=\frac{T_{1}}{T_{m}}, \end{aligned}$$](img/507793_1_En_11_Chapter_TeX_Equ7.png)(7)其中![$$T_{1}$$](img/507793_1_En_11_Chapter_TeX_IEq56.png)是在一台机器上处理数据的运行时间，![$$T_{m}$$](img/507793_1_En_11_Chapter_TeX_IEq57.png)是在*m*台机器上处理数据的运行时间。为了评估所提出系统的聚类质量，我们使用了真正例、真负例、假正例和假负例。真正例（TP）表示入侵检测系统精确地检测到发生了特定的攻击。真负例（TN）表示入侵检测系统在检测正常连接时没有出错。假正例（FP）表示入侵检测系统检测到了特定的攻击，但实际上并没有发生这样的攻击。假负例（FN）表示入侵检测系统无法在特定攻击发生后检测到入侵。本文使用了真正率（TPR）和假正率（FPR），它们分别在方程 8 和 10 中定义。![$$\begin{aligned} TPR=\frac{TP}{TP+FN} \end{aligned}$$](img/507793_1_En_11_Chapter_TeX_Equ8.png)(8)![$$\begin{aligned} FPR=\frac{FP}{FP+TN} \end{aligned}$$](img/507793_1_En_11_Chapter_TeX_Equ9.png)(9)此外，我们使用曲线下面积（AUC）度量[43] 来结合 TPR 和 FPR，这被认为是这些率的良好指标。AUC 可以定义如下：![$$\begin{aligned} AUC=\frac{(1-FPR)\times (1+TPR)}{2}+\frac{FPR\times TPR}{2} \end{aligned}$$](img/507793_1_En_11_Chapter_TeX_Equ10.png)(10)这些度量的值越大，表示结果质量越好。表 2

IDS-SPSO 与 IDS-MRPSO 准确性的比较

| 数据集 | 方法 | TPR | FPR | AUC |
| --- | --- | --- | --- | --- |
| Train20 | IDS-MRPSO | 0.903 | 0.038 | 0.933 |
| IDS-SPSO | 0.848 | 0.096 | 0.875 |
| Train40 | IDS-MRPSO | 0.911 | 0.021 | 0.945 |
| IDS-SPSO | 0.856 | 0.085 | 0.888 |
| Train80 | IDS-MRPSO | 0.935 | 0.013 | 0.961 |
| IDS-SPSO | 0.879 | 0.068 | 0.904 |
| Train100 | IDS-MRPSO | 0.939 | 0.013 | 0.963 |
| IDS-SPSO | 0.883 | 0.059 | 0.905 |

![../images/507793_1_En_11_Chapter/507793_1_En_11_Fig6_HTML.png](img/507793_1_En_11_Fig6_HTML.png)

图 6

IDS-SPSO 与 IDS-MRPSO 运行时间的比较

### 5.4 结果

在实验中，我们使用以下参数：粒子数量为 10，迭代次数为 50，惯性权重为 0.72，加速系数为 1.49。我们首先评估了所提出的 IDS-SPSO 相对于 IDS-MRPSO 系统的准确性。表 2 报告了所提出的系统使用不同的训练数据样本大小与 IDS-MRPSO 系统相比获得的 TPR、FPR 和 AUC 值。得到的结果显示，所提出的 IDS-SPSO 给出了与现有 IDS-MRPSO 系统几乎相同的结果。此外，我们从这张表中观察到，IDS-SPSO 使用整个训练数据（即 Train100）的 TPR 值达到了最佳值，相比较较小的训练数据集。此外，表 2 显示 IDS-SPSO 对于 Train100 数据集获得了最低的 FPR。例如，IDS-MRCPSO 系统在 Train100 上的 TPR 高达 0.883，而在 Train20 上为 0.848。此外，IDS-MRCPSO 在 Train100 上的 FPR 为 0.059，而在 Train20 上为 0.096。因此，我们观察到所提出的系统能够有效区分正常和攻击数据记录。最后，我们得出结论，当使用较大的训练数据集时，准确性有所提高。![../images/507793_1_En_11_Chapter/507793_1_En_11_Fig7_HTML.png](img/507793_1_En_11_Fig7_HTML.png)

图 7

对 KDD 数据集样本从 20% 到 100% 大小的加速结果评估

然后，我们评估了所提出系统的运行时间与 IDS-MRPSO 系统的运行时间。图 6 显示了使用不同数量的机器对 4 个训练数据样本的运行时间结果。得到的结果显示，所提出的系统比现有的 IDS-MRPSO 系统更快。例如，IDS-SPO 对于 Train20 和 Train100 数据集分别比 IDS-MRPSO 快了 1.52 倍和 2.66 倍。从这张图中，我们还可以观察到当机器数量增加时运行时间的改善。例如，对于相同的样本，1 台机器的运行时间分别为 870、1740、3480 和 4350 秒，而 4 台机器的运行时间分别为 245、477、901 和 1092 秒。

我们随后通过在不同数量的机器上运行多个实验来评估所提出系统的可伸缩性。图 7 显示了使用不同数量的机器以及不同训练数据大小时的加速比结果。从这个图表中，我们观察到当数据量增加时，加速比结果变得尤其重要。例如，使用 4 台机器运行 IDS-SPSO 在 Train20 数据时的加速比值为 3.57，而在 Train100 数据时为 3.90。此外，所提出的系统在机器数量增加时显示出近似线性的加速比。这可以通过 Spark 框架的内存处理的优势来解释，当我们增加机器数量时，可以显著降低网络成本。

## 6 结论

在本文中，我们提出了一种用于大规模网络流量的入侵检测系统 IDS-SPSO。所提出的系统通过使用粒子群优化聚类算法解决入侵检测问题来将聚类分析纳入构建检测模型。我们还在这项工作中展示了入侵检测系统可以通过 Spark 框架有效地分布。实验是在真实入侵数据集上实现的，以评估所提出系统的可伸缩性。实验结果显示，当我们增加机器数量和训练数据大小时，IDS-SPSO 的效率得到了提高。此外，实验结果表明，使用更大的训练数据可以通过保持假警报非常低来获得更好的检测率。

我们未来的工作是将能够自动提供聚类数量的算法纳入。此外，我们将通过采用特征选择技术来扩展所提出的系统，在构建聚类时提取最重要的特征。
