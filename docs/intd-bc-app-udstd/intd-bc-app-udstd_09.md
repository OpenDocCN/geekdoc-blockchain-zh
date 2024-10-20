© 作者，独家许可给 APress Media, LLC，隶属于 Springer Nature 2022J. T. George 介绍区块链应用[`doi.org/10.1007/978-1-4842-7480-4_9`](https://doi.org/10.1007/978-1-4842-7480-4_9)

# 9. 实时系统

Joseph Thachil George^(1  )(1)罗马，意大利

分布式实时系统（DRTS）由通过实时网络连接在一起的自包含计算节点组成。这些节点共同努力在预定的时间限制内实现共同的目标。由于各种原因，需要分布式实时系统。

任何实时计算机控制系统必须能够实时测量事件之间的时间，并在预定的实时间隔内对刺激做出反应。本章讨论了将这个实时度量包含在实时分布式系统中的一些影响。

“实时系统”一词指的是受实时约束的系统，即响应必须在一定时间限制内得到保证，或者系统必须满足特定的截止日期。例子包括飞行控制系统、实时监控系统等。

## 9.1 理解实时系统

具有时间约束的实时系统分为硬实时系统和软实时系统两种。*硬实时系统*不能错过截止日期。错过截止日期的后果可能是灾难性的。如果延迟增加，硬实时系统结果的效用会急剧下降，甚至可能变为负值。延迟是指实时系统完成任务相对于截止日期的迟延时间。飞行控制系统就是硬实时系统的一个例子。

*软实时系统*，另一方面，偶尔可能会错过截止时间，但错过的概率足够低以至于是可以接受的。错过截止时间没有负面后果。随着延迟增加，软实时系统结果的效用会迅速降低。电话交换机是软实时系统的一个例子。

## 9.2 实时系统参考模型

这个参考模型由三个组成部分特征化：

+   **一个工作量模型：** 识别系统支持的应用程序。

+   **资源模型：** 描述程序可以访问的资源。

+   **算法：** 描述软件应用程序如何使用资源。

实时系统术语包括：

+   **任务：** 一个可以分配给处理器的小任务，可能需要使用资源，也可能不需要。

+   **任务：** 一组相关的任务，共同工作以提供系统功能。

+   **一个工作的发布时间任务：** 任务准备执行的时间点。

+   **任务执行时间：** 任务完成执行所需的时间。

+   **任务截止时间：** 这是任务必须完成的最后期限。有两种类型的截止时间：绝对截止时间和相对截止时间。（任务的**相对截止时间**是允许的最长响应时间。任务的**绝对截止时间**是其相对截止时间和发布时间的总和。）

+   **任务响应时间：** 这是从任务发布到任务完成的时间。

+   **活动资源：** 处理器的另一个名称，这些资源对于任务成功完成是必需的。为了执行并向完成进展，一个任务需要一个或多个处理器。计算机和传输链路是两个例子。

+   **被动资源** **:** 在作业执行期间，可能需要或不需要资源。内存和互斥量是两个例子。也称为资源。如果两个资源可以互换使用，则它们是相同的；否则，它们是异构的。

图 9-1 描述了硬实时系统与软实时系统之间的关键区别。硬实时系统具有毫秒或更短的响应时间要求，如果未达到这些要求，可能会导致灾难。另一方面，软实时系统具有更高且不太严格的反应时间。在严格实时系统中，必须预期峰值负载性能，并且不能违反指定的截止时间。在软实时系统中，可以接受在罕见的峰值负载时出现降级功能。在所有情况下，硬实时系统必须与环境状态保持同步。![../images/520777_1_En_9_Chapter/520777_1_En_9_Fig1_HTML.jpg](img/520777_1_En_9_Fig1_HTML.jpg)

图 9-1

硬实时与软实时系统

### 9.2.1 故障安全 vs. 故障操作系统

如果在系统故障时可以达到良好状态，则系统被认为是故障安全的。一个例子是火车信号系统。

在故障安全应用程序中需要高错误检测覆盖率。应用程序的故障安全性是一个特征。如果应用程序没有提供安全状态的识别，则系统必须是故障操作的，并且在发生故障时，这些系统（例如飞机上的飞行控制系统）必须保持运行。

### 9.2.2 保证及时性 vs. 最佳尽力系统

即使存在故障，计算机系统也必须提供最低水平的服务。

## 9.3 实时系统分类

根据外部需求，考虑以下类别：

+   实时软件与硬实时软件

+   故障安全 vs. 故障操作

+   保证及时性 vs. 最佳尽力

+   资源的充足性

+   基于时间的触发与基于事件的触发

如果可以通过分析推理（在规定的负载和故障假设范围内）证明时间精确性，则系统实施将保证及时性。如果无法提出时间正确性的知识性论据，则系统实施将尽力而为。

即使在定义的负载和故障假设范围内，对于最佳努力系统的时间验证也依赖于概率考虑。保证及时性应该是硬实时系统的基础。

### 9.3.1 资源充足

一个系统的处理资源必须能够处理所述的最大负载和故障场景，才能保证及时性。过去有几种应用程序认为资源充足是不可承受的昂贵开支。

由于硬件成本在下降，实施资源适当的设计变得更加具有成本效益。在具有挑战性的实时应用中，资源充足的设计是唯一的选择。

### 9.3.2 罕见事件情况下的可预测性

罕见事件是系统寿命中极少发生的重要事件，比如核反应堆中的爆管。罕见事件可能会导致一系列相关的服务请求（例如，报警器激活）。

在许多应用程序中，系统的价值取决于在罕见事件场景下的可预测性能，例如飞行控制系统。大多数情况下，工作负载测试不会解决罕见事件场景。

### 9.3.3 状态和事件

![../images/520777_1_En_9_Chapter/520777_1_En_9_Fig2_HTML.jpg](img/520777_1_En_9_Fig2_HTML.jpg)

图 9-2

状态事件

*状态* 是实时中持续一定时间的条件，例如时间轴的一部分。瞬时发生称为 *事件*。见图 9-2。

状态信息描述了观察站点（本身是一个事件）的状态特征。提供了事件信息，即事件发生前后状态特性的变化，以及事件发生的时间估计。

### 9.3.4 时间触发与事件触发系统

实时系统中的控制信号如果纯粹是从事件发生（例如任务完成、消息接收或外部中断发生）中获取的，则称为事件触发（ET）的。

如果控制指示器（例如消息发送和接收）纯粹是从时间（全局时间）的发展中生成的，则实时系统是时间触发（TT）的。

## 9.4 时间要求

对于实时系统，操作员看到的数据片段在时间上必须准确。必须确定和限制刺激和反应之间的最大实时间隙。尽管这是一种罕见的情况，但时间行为也应该是可预测的。请参见图 9-3。![../images/520777_1_En_9_Chapter/520777_1_En_9_Fig3_HTML.jpg](img/520777_1_En_9_Fig3_HTML.jpg)

图 9-3

与实时数据相关的时间参数

## 9.5 调度算法的分类

### 9.5.1 硬实时和软实时调度

在硬实时系统中，必须通过各种可能的方式提前保证关键任务的截止日期，并考虑可预见的情况。这需要仔细设计系统资源。如果您正在设计软实时系统，您可以接受低成本的调度器设计。

### 9.5.2 动态和静态调度程序

如果调度器根据当前请求进行运行决策，则称其为动态（在线）调度器。因此，动态调度器具有灵活性，并随着系统的演变而适应。如果在调度器运行之前就做出决定并且不能更改，则称调度器为静态（预运行）。这需要对要执行的任务有深入完整的了解（最大执行时间、优先级、互斥约束、截止时间等）。这样的调度器在执行阶段的成本低，因为不需要进行决策计算。

### 9.5.3 具有/不具有抢占的调度器

在具有抢占的调度器中，任务可以在更高优先级任务的请求下被中断。然而，只有在不违反某些断言的情况下（见互斥）才会授权抢占。在非抢占调度器中，任务直到完成才不会被中断。

### 9.5.4 静态调度

在静态调度中，任务的执行顺序是离线计算的。静态调度在时间触发应用程序和周期性任务中很典型。

### 9.5.5 动态调度

动态调度器根据系统当前状态确定事件到达时要执行的任务。不同的动态调度算法根据所做的假设而不同。

### 9.5.6 独立任务调度

这一类别假设任务没有任何依赖关系（例如互斥）。

## 9.6 复习问题

1.  1.

    “分布式实时系统（DRTS）由实时网络连接的独立计算节点组成。”这个说法正确吗？

1.  2.以下哪项描述了硬实时系统？

    1.  a.

        可能会定期错过截止时间，但概率很低。

    1.  b.

        偶尔会错过截止时间，但有合理的机会这样做。

    1.  c.

        由于某些不可接受的低概率，偶尔会错过其截止时间，

    1.  d.

        有时会错过截止日期，但概率很低。

1.  3.关于*状态*的以下哪种说法是正确的？

    1.  a.

        状态是在实时中持续一段时间的状态。

    1.  b.

        状态是持续一段非实时时间的条件。

    1.  c.

        状态是不持续一段时间的状态。

    1.  d.

        状态是不可预测地变化的条件，持续一段时间。

1.  4.关于*事件*的以下哪种说法是正确的？

    1.  a.

        事件是发生在特定状态下的事件。

    1.  b.

        事件是一次性的非发生。

    1.  c.

        事件是一次发生。

    1.  d.

        所有这些。

1.  5.三个部分定义了一个参考模型：

    1.  a.

        工作负载模型

    1.  b.

        资源模型

    1.  c.

        算法

这个说法正确吗？

## 9.7 复习答案

1.  1.

    答案：正确。分布式实时系统（DRTS）由通过实时网络链接的自包含计算节点组成，并由实时网络连接的自主计算节点组成。这样的系统中的节点合作以在指定的截止日期内实现共同目标。

1.  2.

    答案：D，有时会错过截止日期，但概率很低。

1.  3.

    答案：A，*状态*是在实时中持续一段时间的条件。

1.  4.

    答案：C，*事件*是一次发生。

1.  5.

    答案：正确。RT 系统模型的主要部分是工作负载模型、资源模型和算法。

## 9.8 总结

本章解释了分布式系统的时间管理。此外，还讨论了软实时和硬实时系统，这些系统说明了参考模型。为了实现分布式系统，有必要了解这个时间管理系统。调度算法也是分布式系统的重要概念，因此下一章将解释分布式系统中的动态和静态调度算法。
