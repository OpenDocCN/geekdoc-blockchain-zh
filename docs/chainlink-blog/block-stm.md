# Block-STM:加速智能合约处理

> 原文：<https://blog.chain.link/block-stm/>

## 剧情简介

[Block-STM](https://arxiv.org/pdf/2203.06871.pdf) 是最近宣布的用于加速智能合同执行的技术，源自 [Diem 项目](https://github.com/diem) 。加速方法与现有的区块链兼容，而不需要由挖掘器/验证器节点修改或采用，并且当它验证(块)事务时，可以独立地使任何节点受益。

这篇文章用简单的英语解释了 Block-STM，并附有一个运行场景。

## 背景

在分布式数据库背景下的[Calvin 2012](http://cs.yale.edu/homes/thomson/publications/calvin-sigmod12.pdf)和[Bohm 2014](https://arxiv.org/pdf/1412.2324.pdf)项目中开创的一种方法是后面许多内容的基础。这些项目中有见地的想法是通过传播预先排序的批量(类似于块)事务以及对它们的读写集的预先估计来简化并发管理。然后，每个数据库分区都可以根据块预排序自主执行事务，每个事务只等待对块中较早事务的读取依赖。[first die VMM 并行执行器](https://github.com/diem/diem/issues/8829) 实现了这种方法，但是它依赖于静态事务分析器来预先估计读/写集，这非常耗时并且可能不精确。

另一部作品 [Dickerson 等人 2017](https://arxiv.org/abs/1702.04467) 提供了从传统数据库并发到 smart-contract 并行的链接。在该工作中，共识领导者(或挖掘者)通过利用乐观软件事务内存(STM)预先计算并行执行串行化，并将预执行调度准则传播给所有验证器节点。后期作品，包括[par block chain](https://arxiv.org/pdf/1902.01457.pdf)和[OptSmart 2021](https://arxiv.org/abs/2102.04875)在预执行期间添加读/写-集依赖跟踪，并传播这些信息以增加并行性。这些方法消除了对静态事务分析的依赖，但需要领导者预先执行块。

Block-STM 并行执行器将预先排序的块思想与乐观 STM 相结合，在运行中强制执行事务的块预先排序，完全消除了预先传播执行计划或预先计算事务依赖性的需要，同时保证了可重复性。

## 技术概述

Block-STM 是智能合约的并行执行引擎，围绕软件事务内存的原则构建。事务按块分组，每个块包含一个预先排序的事务序列 TX <sub>1</sub> ，TX <sub>2</sub> ，…，TX <sub>n</sub> 。事务由读写共享内存的智能合约代码组成，它们的执行产生一个读集和一个写集:读集由成对的内存位置和写它的事务组成；写集由一个内存位置和一个值组成，事务在提交时会记录这些值。

### 区块预购

块的并行执行必须产生相同的确定性结果，保持块的前序，也就是说，它产生与顺序执行完全相同的读/写集。如果在顺序执行中，TX <sub>k</sub> 读取 TX <sub>j</sub> 写入的值，即 TX <sub>j</sub> 是写入该特定存储器位置的 TX <sub>k</sub> 之前的最高事务，我们将其表示为:

TX<sub>j</sub>T3→TX<sub>k</sub>T7T9】

### 运行实例

在本文中，我们将使用以下场景来说明并行执行策略及其效果。

```
   A block B consisting of ten transactions, TX<sub>1</sub>, TX<sub>2</sub>, ..., TX<sub>10</sub>, 
 with the following read/write dependencies:
    TX<sub>1</sub> → TX<sub>2</sub> → TX<sub>3</sub> → TX4 
    TX<sub>3</sub> → TX<sub>6</sub> 
    TX<sub>3</sub> → TX<sub>9</sub>
```

为了说明执行时间表，我们将假设一个系统有四个并行线程，为了简单起见，每个事务正好用一个时间单位来处理。

如果我们事先知道上述块的依赖性，我们可以按照以下时间步骤安排块 B 的理想执行:

1.  并行执行 TX <sub>1</sub> ，TX <sub>5</sub> ，TX <sub>7</sub> ，TX <sub>8</sub>
2.  并行执行 TX <sub>2</sub> ，TX<sub>10</sub>
3.  并行执行 TX<sub>3</sub>T3】
4.  并行执行 TX <sub>4</sub> ，TX <sub>6</sub> ，TX <sub>9</sub>

### 乐观调度

如果事先不知道依赖关系怎么办？一个正确的并行执行必须保证所有的事务确实按照块依赖关系读取值。即当 TX <sub>k</sub> 从内存中读取时，必须获取 TX <sub>j</sub> ，TX<sub>j</sub>→TX<sub>k</sub>写入的值，如果存在依赖关系；或者是块执行开始时该内存位置的初始值(如果没有的话)。

Block-STM 通过采用乐观的“推测-验证-重做”方法来确保这一点，它贪婪地、乐观地并行执行事务，然后进行验证，如果验证失败，则重复执行。TX <sub>k</sub> 的验证重新读取 TX <sub>k</sub> 的读取集，并与 TX <sub>k</sub> 在其最近一次执行中获得的原始读取集进行比较。如果比较失败，TX <sub>k</sub> 中止并重新执行。

关键的一点是，预订大大简化了乐观情绪！

*   如果验证失败，只有更高的交易需要重新验证(VALIDAFTER)
*   读取获取最高的先前事务写入的值，而不是最后写入的值(READHIGH)

有了这种认识，我们首先考虑一种直截了当的稻草人方法。strawman 算法使用集中式调度程序来协调并行线程的工作。

### 稻草人(S-1)算法

```
 // Phase 1:      
    dispatch all TX’s for execution in parallel ; wait for completion 

   // Phase 2:
 repeat {
dispatch all TX's higher than the last failed for read-set validation in parallel ; wait for completion
} until all read-set validations pass 
 read-set validation of TX<sub>j</sub> {
 re-read TX<sub>j</sub> read-set 
 if read-set differs from original read-set of the latest TX<sub>j</sub> execution 
 re-execute TX<sub>j</sub>
 } 
 execution of TX<sub>j</sub> {
 (re-)process TX<sub>j</sub>, generating a read-set and write-set
    }
```

S-1 在两个主协调阶段运行。阶段 1 乐观地并行执行所有事务。阶段 2 乐观地并行重复验证高于上一次失败的 的所有事务 ，重新执行那些失败的事务，直到不再有读取集验证失败。

回想一下我们的运行示例，一个具有依赖关系的块 B TX<sub>1</sub>→TX<sub>2</sub>→TX<sub>3</sub>→{ TX<sub>4</sub>，TX <sub>6</sub> ，TX <sub>9</sub> })，运行四个线程，每个事务占用一个时间单元(忽略所有其他计算)块 B 上 S-1 的可能执行将沿着以下时间步骤进行:

1.  第一阶段开始。并行执行 TX <sub>1</sub> ，TX <sub>2</sub> ，TX <sub>3</sub> ，TX <sub>4</sub>
2.  并行执行 TX <sub>5</sub> ，TX <sub>6</sub> ，TX <sub>7</sub> ，TX <sub>8</sub>
3.  并行执行 TX <sub>9</sub> ，TX <sub>10</sub>
4.  第二阶段开始。在第一次循环迭代中， 对 TX <sub>2</sub> ，TX <sub>3</sub> ，TX <sub>4</sub> ，TX <sub>6</sub> 失败的所有事务进行并行读集验证并重新执行
5.  TX <sub>9</sub> 失败并重新执行的所有事务的持续并行读集验证
6.  在下一阶段-2 循环迭代中， 并行对 TX <sub>3</sub> ，TX <sub>4</sub> ，TX <sub>6</sub> 失败的所有事务进行读-集验证并重新执行
7.  在下一阶段-2 循环迭代中， 并行对 TX <sub>4</sub> ，TX <sub>6</sub> ，TX <sub>9</sub> 失败的所有事务进行读-集验证并重新执行
8.  在最后一次阶段 2 循环迭代中， 所有事务的并行读集验证成功

### Block-STM 算法

在完整的 Block-STM 解决方案中，对上述 strawman 进行了两项基本改进。

**偷任务。** 第一个改进是用线程并行偷任务来代替两个阶段。它遵循来自 S-1 的 洞察，区分初步执行(对应于阶段 1)和重新执行(在确认中止之后)。窃取通过两个同步计数器来协调，每个任务类型一个， `nextPrelimExecution` (最初为 1)和 `nextValidation` (最初为 n+1)。

窃用使得较高事务的验证能够在完成时或较低事务验证失败时立即开始。TX <sub>j</sub>

**原始依赖追踪。** 第二个改进是一个非常简单的依赖跟踪(没有图或偏序),大大减少了中止。当 TX <sub>j</sub> 中止时，其最近一次调用的写集被标记为中止。更高的事务简单地在读取中止标记时暂停，等待直到 TX <sub>j</sub> 的重新执行覆盖它。这是交易预购大大简化事务的另一个例子。

具有任务窃取的高级线程循环如下:

*   如果可用，窃取下一个验证任务 TX<sub>j</sub>T3】
*   否则，窃取下一个预执行任务 TX<sub>j</sub>T3】

通过中止标记和中止任务的早期重新验证来支持依赖性管理，如下所述:

*   如果验证失败，标记写设置中止并立即减少下一个验证
*   如果重新执行的写入集不同于原始写入集，再次减少 nextValidation】

下面的伪代码(不到 20 行)给出了更精确的描述。有关完整的详细信息，请参见白皮书。

### Block-STM 算法

```
 // per thread main loop:
    repeat {
 task := "NA"
        // if available, steal next read-set validation task
 atomic {
 if nextValidation < nextPrelimExecution
 (task, j) := ("validate", nextValidation)
 nextValidation.increment();
 } 
        if task = "validate"
 validate TX<sub>j</sub> 

        // if available, steal next execution task
 else atomic { 
            if nextPrelimExecution <= n         
 (task, j) := ("execute", nextPrelimExecution)
 nextPrelimExecution.increment();
 }
        if task = "execute"
 execute TX<sub>j</sub> 
 validate TX<sub>j</sub> 
    } until nextPrelimExecution > n, nextValidation > n, and no task is still running

 read-set validation of TX<sub>j</sub> {
        re-read TX<sub>j</sub> read-set 

        if read-set differs from original read-set of the latest TX<sub>j</sub> execution 
 mark the TX<sub>j</sub> write-set ABORTED
 atomic { nextValidation := min(nextValidation, j+1) }
 re-execute TX<sub>j</sub>
    }

 execution of TX<sub>j</sub> {
        (re-)process TX<sub>j</sub>, generating a read-set and write-set
 resume any TX waiting for TX<sub>j</sub>'s ABORTED write-set
 if the new TX<sub>j</sub> write-set contains locations not marked ABORTED
 atomic { nextValidation := min(nextValidation, j+1) }
    }
```

Block-STM 通过使用中止标签进行简单、即时的依赖性管理来提高效率。对于我们正在运行的块 B 的例子，一个四线程的执行可以通过等待一个中止标记来避免在 稻草人场景 中发生的几次重新执行。尽管存在高争用 B 场景，但 Block-STM 的可能执行可以实现非常接近最优的调度，如下所示。对块 B 的一个可能的执行(回忆，TX<sub>1</sub>→TX<sub>2</sub>→TX<sub>3</sub>→{ TX<sub>4</sub>，TX <sub>6</sub> ，TX <sub>9</sub> })将沿着以下时间步骤进行(如图所示):【T29

1.  并行执行 TX <sub>1</sub> ，TX <sub>2</sub> ，TX <sub>3</sub> ，TX<sub>4</sub>；TX <sub>2</sub> 、TX <sub>3</sub> 、TX <sub>4</sub> 的读-设置验证失败；nextValidation 设置为 3
2.  并行执行 TX <sub>2</sub> ，TX <sub>5</sub> ，TX <sub>7</sub> ，TX<sub>8</sub>；TX <sub>3</sub> 、TX <sub>4</sub> 、TX <sub>6</sub> 的执行被中止中止；nextValidation 设置为 6
3.  并行执行 TX <sub>3</sub> ，TX<sub>10</sub>；TX <sub>4</sub> 、TX <sub>6</sub> 、TX <sub>9</sub> 的执行在中止时暂停；所有读集验证成功(暂时)
4.  并行执行 TX <sub>4</sub> ，TX <sub>6</sub> ，TX<sub>9</sub>；所有读集验证成功

### ![Block-STM](img/2193efa41455ac2b6c338d8346ed4751.png)

### 正确性

正确的乐观主义围绕着两个原则:

*   READHIGH(k):每当 TX <sub>k</sub> 执行(推测性地)时，TX <sub>k</sub> 的一个 read 就获得它之前的最高事务 TX <sub>j</sub> 迄今记录的值，即，其中 j < k .更高的事务 TX <sub>l</sub> ，其中 l > k 不干扰 TX <sub>k</sub>
*   VALIDAFTER(j，k):对于每个 j，k，使得 j < k，每次 TX <sub>j</sub> 执行(或重新执行)时，执行 TX <sub>k</sub> 的读集合的验证。

总之，无论如何调度事务，这两个原则足以保证安全性和活性。简而言之，由于在所有 TX <sub>j</sub> 、j < k 被最终确定之后，TX <sub>k</sub> 得到验证，因此安全性得以保证。活跃度随归纳而来。最初，保证事务 1 成功通过读集验证，并且不需要重新执行。从 TX <sub>1</sub> 到 TX <sub>j</sub> 的所有事务成功验证后，事务 j+1 的(重新)执行将成功通过读集验证，不需要重新执行。

READHIGH(k)通过一个简单的多版本内存数据结构在 Block-STM 中实现，该结构保存版本化的写集。TX <sub>j</sub> 写的 A 用版本 j 记录，TX <sub>k</sub> 读的 A 用最高 j<k获得 TX <sub>j</sub> 最后一次调用记录的值

当 TX <sub>j</sub> 的最近一次调用中止时，中止的特殊值可能存储在版本 j 中。如果 TX <sub>k</sub> 读取该值，它将暂停，并在该值被设置时恢复。

VALIDAFTER(j，k)通过调度为每个 TX <sub>j</sub> 执行一个 TX <sub>k</sub> 的读集验证，对于每个 k > j，在 TX <sub>j</sub> 完成(重新)执行之后。与早期重新验证的交互有点微妙。假设 TX<sub>j</sub>→TX<sub>k</sub>。回想一下，当 TX <sub>j</sub> 失败时，Block-STM 会在 TX <sub>j</sub> 完成重新执行之前，立即调度(重新)TX <sub>k</sub> 、k > j 的验证。有两种可能的情况。如果 TX<sub>k</sub>-validation 读取 TX <sub>j</sub> 的中止值，它将等待 TX <sub>j</sub> 完成；并且如果它读取的值没有被标记为中止，并且 TX <sub>j</sub> 重新执行具有新的写设置，则 TX <sub>k</sub> 将被强制再次重新生效。

## 结论

简单是 Block-STM 的一个优点，而不是一个缺点，可以实现健壮和稳定的实现。通过仔细组合简单的已知技术，并将其应用于批量提交的预先排序的事务块，Block-STM:

*   有效加速智能合同并行处理
*   启用可重复执行(必需)
*   由于线性依赖/验证，STM 变得实用
*   批量提交每个块(而不是每个事务)
*   独立惠及客户
*   可以与现有的区块链一起工作，而不需要被所有/其他验证器节点采用

Block-STM 已经集成到 Diem 区块链内核([](https://github.com/diem/))中，并在合成事务工作负载上进行评估，在低/中度争用的情况下，在 32 个内核上实现了超过 17 倍的加速。

*关于区块链、智能合约和神谕的最新研究，[订阅 Chainlink 时事通讯](https://pages.chain.link/subscribe)，[关注官方 Chainlink Twitter。](https://twitter.com/chainlink)*

___

免责声明:以上描述或多或少忠实地反映了 Block-STM 方法；详见 [论文](https://arxiv.org/pdf/2203.06871.pdf) 。此外，请注意这里的描述使用了与论文不同的名称，例如，ABORTED 替换了“估计”，nextPrelimExecution 替换了“执行 _idx”，nextValidation 替换了“验证 _idx”。T9】

*鸣谢:非常感谢 [卓伦(大牛)向](https://www.linkedin.com/in/zhuolun-xiang-b6898ab5/) 指出了帮助改进这篇文章的微妙细节。T9】*

*这篇文章的一个版本于 2022 年 4 月 13 日在 https://dahliamalkhi.github.io/posts/2022/04/block-stm/.首次发表*