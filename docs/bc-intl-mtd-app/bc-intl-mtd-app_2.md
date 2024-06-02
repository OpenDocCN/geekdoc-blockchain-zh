© 作者（们），在 Springer Nature 新加坡私人有限公司独家授权下 2021 郑培林等人（编辑）区块链智能[`doi.org/10.1007/978-981-16-0127-9_2`](https://doi.org/10.1007/978-981-16-0127-9_2)

# 2.链上和链下区块链数据收集

郑培林^(1  )，郑子宾^(2  )，吴嘉静^(2, 3  ) 和戴红宁^(4  )（1）中山大学，广州，中国（2）中山大学数字生活国家工程研究中心，广州，中国（3）中山大学数据科学与计算机学院，广州，中国（4）澳门科技大学，澳门特别行政区，中国郑培林电子邮件： zhengpl3@mail2.sysu.edu.cn 郑子宾（通讯作者）电子邮件： zhzibin@mail.sysu.edu.cn 吴嘉静电子邮件： wujiajing@mail.sysu.edu.cn 戴红宁电子邮件： hndai@ieee.org

## 摘要

在第一章引入区块链智能之后，在本章中，我们概述了区块链数据收集。我们首先回顾了近年来区块链快速发展带来的数据增长，然后分析了这种现象引起的数据处理和探索挑战，并最终提出了我们的解决方案 XBlock-ETH，这是经过精心处理的最新链上数据集。

## 2.1 概述

学术界和工业界正密切关注具有巨大价值的区块链。在不同的区块链系统中，他们在未经许可的区块链（或公有区块链）上做出了许多努力，以解决区块链（或公有区块链）的去中心化布局引起的问题（郑平等人 2018b）。无许可的区块链是对比特币的一项创新（中本聪 2008）。区块链系统中的每个节点相当于一个账本。考虑到账本的特点，它通常被用作一项公开的总计。以太坊（但斌 2013）是比特币背后的创新，是一个能够实现图灵完备智能合约的无许可区块链系统。区块链的不可思议的发展使得区块链数据迅速增长。根据 Statista（[`​www.​statista.​com/`](https://www.statista.com/)）的报告，2019 年第三季度的比特币数据轻松达到了 242 GB。在本章中，考虑到以太坊有图灵完备的智能合约，我们更关注以太坊。同样，有超过 1600 万份智能合约部署在以太坊上。以太坊社区率先推出的两个代币协议简化了初始代币发行（所谓的 ICO）（但斌和法比安 2015），因此在以太坊上可以转移超过 100,000 个 ERC20 代币和 1600 个 ERC721 代币。

大量区块链数据的开放性、去中心化和高温耐受性让研究人员看到了巨大的商业机会和研究机会（Dai 等 2019）。研究人员很难突破隐私保护和所有权保护来获取真实的商业交易数据。相比之下，区块链系统中的所有数据都存储在链上并完全公开。其去中心化特性也意味着无需许可的区块链可以轻松访问任何数据。此外，区块链的分布式共识也确保了区块链数据的抗疲劳性。区块链交易非常重要，但以太坊（或其替代品）提供的智能合约和加密货币也是主要研究方向。对相关数据的大数据分析有利于交易欺诈检测、智能合约漏洞检测和智能合约软件开发。在区块链系统的快速发展中，挑战悄然而至：**（1）区块链对等节点数据同步遇到的困难。** 区块链的去中心化意味着区块链数据需要一个长期的节点同步过程。在区块链白皮书节点选择部分，强调了完全同步整个以太坊需要超过一周时间，并且需要超过 500 GB 的存储空间。对存储空间和网络带宽的巨大需求阻碍了区块链数据分析。**（2）区块链数据提取和处理面临的挑战。** 区块链数据的存储方式也影响着大数据分析的效果。所有数据都是加密或二进制的，这进一步阻碍了相关研究的发展。显然，传统数据分析方法可能不适用于这类数据，针对区块链的新分析方法仍在研究中，因此处理异构区块链数据并不容易。**（3）缺乏针对区块链的通用数据提取工具。** 有很多工具可以提取区块链数据，但大量完整数据意味着这些工具只能获取部分数据来完成相关论文中的特定研究任务。**（4）区块链基本数据探索的缺乏。** 现有研究只关注区块链数据的特定数据分析，例如，交易图（Chen 等 2018a）和合约安全（Luu 等 2016）。基本数据探索，如统计分析、文本分析和数据可视化，是目前区块链大数据分析的不足之处。我们提出的区块链数据分析框架可能解决这些挑战，即 e underline X plore underline Block chain underline ETH (XBlock-ETH)来分析以太坊数据。特别是，我们从以太坊中提取了包含 8,100,000 个区块的原始数据。原始数据包括三种以太坊数据：*区块*、*交易轨迹*和*收据*。由于难以分析原始以太坊数据，我们将获得的以太坊区块链数据分为六个数据集：*（1）区块和交易*、*（2）内部以太交易*、*（3）合约信息*、*（4）合约调用*、*（5）ERC20 代币交易*、*（6）ERC721 代币交易*。我们提供的以太坊数据新分类可以帮助其他研究人员更好地从总体角度推进大多数研究任务。然而，分割和处理原始数据并不容易，因为从原始数据中提取元数据信息并将其与六个数据集关联需要付出很大努力。然后，我们对六个精炼的数据集进行统计分析。我们还将讨论 XBlock-ETH 的潜在应用，如区块链系统分析、智能合约分析和加密货币分析。

总结来说，我们突出本章的主要贡献如下：

+   链上的数据由 XBlock-ETH 更全面地包含（只覆盖了以太坊数据的一部分）。它特别包括了区块链数据、智能合约数据和加密货币数据。因此，这些精心处理的数据集使得处理人员能够轻松进行数据探索。此外，XBlock-ETH 在线正式发布的数据^(1) 已经定期更新。

+   XBlock-ETH 框架还提供了基本的统计和探索功能来分析区块链数据集。本章也概述了 XBlock-ETH 带来的研究机遇。特别是，我们讨论了 XBlock-ETH 在区块链系统分析、智能合约分析和加密货币分析方面的应用。

本章的其余部分如下组织。第 2.3 节和第 2.4 节接着介绍从以太坊获取原始数据和六个数据集的数据探索。第 2.5 节讨论了 XBlock-ETH 数据的应用。最后，第 2.6 节作结。

## 2.2 以太坊与智能合约

图 2.1 展示了以太坊区块链的概览，从底层到顶层包括以下几个层次：节点、区块链、智能合约和代币。接下来，我们将回顾以太坊每个层次的基本概念。![../images/506524_1_En_2_Chapter/506524_1_En_2_Fig1_HTML.png](img/506524_1_En_2_Fig1_HTML.png)

Fig. 2.1

以太坊区块链概览

### 2.2.1 节点与区块链

总之，我们通常所说的区块链是由多个特殊区块组成的一种链式数据结构。在 P2P 区块链网络中的所有节点共同维护这条链。在一定时间，共识协议在整个区块链网络中只能确认一个区块。矿工扮演着重要角色。它可以生成包含已确认交易和前一个区块的区块的哈希值，并且该块的验证将由其他节点独立完成。等待区块链网络中大多数节点的验证和确认，这个区块中的交易将被视为*完成*。这样，账本的概念就被扩展了，即由于所有节点都验证了交易，每个节点都可以信任整个区块链。换句话说，区块链分布式系统中的交易数据的可信度需要通过在每个节点上复制计算和存储来维护。

无权限的区块链节点的区块必须是完整的，因此，研究人员可以通过已经连接到区块链网络的区块链节点获取整个区块链数据。用户和矿工在区块链上完成的大量业务操作构成了区块链数据，考虑到交易记录本质上是由不同的业务方完成的操作。区块链数据中代表的各种行为可以映射到现实经济系统中的用户行为（如汇款）。同时，随着比特币和以太坊中用户和交易的激增，区块链数据的大小迅速增长。分析区块链数据也可能有助于预测经济趋势。

### 2.2.2 智能合约

重塑现代行业的关键可能是智能合约，而不是区块链（Szabo 1997）。智能合约实际上是一些计算机程序。它们基于区块链，并在区块链之上存储执行状态。与比特币不同，区块链交易代表智能合约的部署或调用。因此，区块链本身的存在意味着智能合约的可靠性。

智能合约已经是现有区块链系统的一个常见功能。例如，比特币允许用户在交易过程中运行简单的脚本。尽管这个脚本是图灵不完整的，但它可以被视为基于区块链的智能合约的原型，因此它不能使合同中实现复杂的逻辑表达。而以太坊对图灵完备的智能合约的支持真正体现了区块链系统的价值。在以太坊中，智能合约是在一种名为以太坊虚拟机（EVM）的环境中执行的。EVM 读取和写入状态（以键值对的形式存储），这些操作在智能合约中有定义。在合约执行过程中，矿工使用“*Gas*”作为单位来评估智能合约的消耗。在合约执行过程中，合约用户将按“GasUsed”和“GasPrice”付费。“GasPrice”用户承诺支付给矿工越多，合约执行的速度就越快。在完成交易（即操作）后，EVM 将生成状态的哈希值并记录在区块链上。因此，从图 2.1（2.1）我们可以理解到，以太坊上的智能合约并不是直接存储在区块链上的。它们基本上是存储在由区块链操作的状态中。

### 2.2.3 代币与客户端

Ethereum 拥有两种智能合约标准代币协议（又名模板）。这些代币协议定义了智能合约中的标准变量、函数和接口。有了这些协议，用户可以在以太坊之上基于智能合约发行代币（或所谓的加密货币）。如图 2.1（即最上层）所示，有四种典型的代币 USDT、^(2) Cryptokitties (Kharif 2017)，Kyber (Luu 2017)和 MarkerDAO^(3)。例如，用户可以在以太坊上发布一个 ERC20 合约，向其他人发行代币。此后，其他任何用户（甚至合约）都可以在没有集中权威（例如，证券交易所）的情况下接收或发送代币。标准代币协议极大地丰富了以太坊生态系统，使以太坊成为了一个灵活的金融系统。在 2.4.5 和 2.4.6 节中，我们将探讨以太坊中的代币数据。

Ethereum 允许任何满足协议要求的计算机程序加入网络，就像 P2P 协议（例如 BitTorrent）一样。因此，有许多不同的 Ethereum 客户端可以验证区块和交易。在大多数 Ethereum 客户端中，Go-Ethereum（Geth）和 Parity 根据 Ether nodes 的统计数据，一直是使用最广泛的。它们都为用户提供 JSON-RPC 接口以与 Ethereum 区块链交互。通过 JSON-RPC 接口，用户可以从以太坊获取区块链数据。Geth 在许多先前的研究中通常被使用，而 Geth 中设计的接口不适合数据采集。即使许多研究者试图修改 Geth 的源代码以获取详细的运行时数据，整个代码修改过程既耗时又复杂。此外，在某些情况下获取的数据并不完全准确。与 Geth 不同，Parity 更好地设计了接口，使其能够获取与我们需要的每块数据相对应的每个块的索引。关于区块链数据的数据采集的详细信息将在 2.3 节中描述。

## 2.3 从 Ethereum 中提取原始数据

本节描述了从 Ethereum 区块链获取原始数据的过程。图 2.2 展示了从区块*N*通过区块链对等体到 EVM 的典型 Ethereum 交易执行流程。在这个过程中，我们收集了三种类型的区块链原始数据：区块、收据和跟踪。我们接下来描述每种原始数据的组成和获取细节。![../images/506524_1_En_2_Chapter/506524_1_En_2_Fig2_HTML.png](img/506524_1_En_2_Fig2_HTML.png)

图 2.2

Ethereum 交易流程中的原始数据收集

### 2.3.1 区块

区块数据直接存储在 Ethereum 区块链中。每个区块由两个组件组成：

+   **区块头**：区块头是区块的基本信息，包括矿工地址、时间戳、燃料限制等。

+   **区块交易**：区块交易构成区块的主体。每笔交易包括如下字段：*From*、*To*、*Value*、*Input*等。如果交易用于部署合约，区块交易中的*To*字段为“null”。

几乎所有的以太坊客户端，包括 Geth 和 Parity，都提供了查询区块的接口。例如，“eth_getBlock”在 Geth 和 Parity 中都可以使用，且效率相似。然而，区块交易的输入只代表了在合约部署阶段 EVM 的操作，合约代码将在交易执行结束时存储，与交易输入不同。这意味着对区块数据的分析只能让我们获取到关于区块链用户非常有限的信息。在大额交易中，我们无法获取确切的合约代码。我们不知道交易是否成功执行，以及交易执行过程中会抛出什么样的错误。是合约向其他合约发送消息或加密货币引起的问题。

### 2.3.2 跟踪

跟踪数据本质上是在 EVM 中生成的一系列详细的运行时数据（例如，智能合约内的内部调用，从合约向个人转账）。跟踪数据不能直接从区块数据中获取或观察，但可以在合约执行期间记录。在本章中，跟踪数据指的是在交易执行前后无法获取，仅在执行过程中出现的数据。跟踪数据包括以下类型：

+   **创建**是在部署智能合同时记录的跟踪数据，包括创建者、代码和初始余额。合约的创建者可以是个人或另一个智能合约。

+   **调用**当通过不同的以太坊地址转移资金或消息时发生。合约调用或以太币转账显示为“调用”跟踪数据。

+   **自杀**是智能合约“自杀”删除其代码，并将价值退回到特定账户的跟踪数据。

+   **奖励**是矿工挖出一个区块时获得的以太币奖励。奖励的值取决于矿工的贡献。

在 Geth 中，交易跟踪的接口是“debug_traceTransaction”。然而，这个接口返回了交易期间的全部操作，导致资源消耗大且效率低下。因此，许多先前的研究尝试修改 Geth 的源代码以获取详细的运行时数据，但这一过程极为耗时。在本章中，我们采用 Parity 中的“parity_trace”来获取跟踪数据。这个接口由官方开发者提供和维护，因此与 Geth 相比，正确性得到保证。同时，它还提供了我们需要的足够信息，例如基本跟踪类型和错误。此外，Parity 的另一个优点是数据的更新方便，因为数据按区块进行索引。

### 2.3.3 收据

交易执行后，以太坊状态中的一些已经被改变（例如，代币合约中的账户余额）。然后客户端需要知道发生了什么变化。为了减少客户端的查询开销，许多合约在执行过程中留下了一种称为“事件”的输出。例如，一个标准代币合约将输出一个“Transfer(from,to,value)”事件，让客户端知道执行过程中发生了什么。这种输出是一种单向输出，因为它只是写入交易的收据中，可以被外部客户端或个人读取，但不能被内部 EVM 读取。

第 2.4 节将给出以太坊数据的统计信息。特别是，有超过 100,000 种加密货币在以太坊上使用智能合约。至于这些代币合约，收据数据是了解持有者、所有者和用户行为的重要来源。因此，获取收据数据是必要的。Geth 和 Parity 都提供了获取交易收据的接口。Geth 和 Parity 接口的主要区别在于收据的查询索引。特别是，Geth 接口的收据是“eth_getTransactionReceipt”，按交易哈希索引，而 Parity 的接口是“parity_getBlockReceipts”，按区块号索引。这样，由于 Parity 可以在一次查询中返回一批收据，因此比 Geth 效率更高。

总结起来，在以太坊中可以获得三种原始数据集：区块数据、交易跟踪数据和收据数据。更具体地说，使用 Shell、NodeJS 和 Python 实现几乎需要花费两周时间来同步整个以太坊区块链并获取原始数据。压缩后，数据大小约为 313 GB。由于原始数据的海量体积和冗余信息，数据处理是必要的，以简化数据表示并加快数据分析，以便进一步研究。

## 2.4 以太坊数据探索

在本节中，我们对从以太坊获取的原始数据进行处理，并将其划分为六个数据集：(1) 区块与交易，(2) 内部以太坊交易，(3) 合约信息，(4) 合约调用，(5) ERC20 代币交易，(6) ERC721 代币交易。原始数据与处理后的数据集之间的关系如图 2.3 所示。划分这六个数据集的原因是我们希望为特定研究领域的研究人员找到数据的最小必要子集。例如，如果研究人员想要研究以太坊转账网络，他只能研究数据集 2（内部以太坊交易），而不是处理原始数据或其他子数据集，从而节省了他的工作量。![../images/506524_1_En_2_Chapter/506524_1_En_2_Fig3_HTML.png](img/506524_1_En_2_Fig3_HTML.png)

图 2.3

原始数据到数据集的映射

本节将介绍数据集是如何生成的，以及统计观察结果。

### 2.4.1 数据集 1：区块与交易

为了研究以太坊的基本统计数据，我们从区块和区块内的交易中提取相关信息。特别是，从区块数据中产生了 8,100,000 个区块和 491,562,222 个交易。对于每个区块，我们还获得了“gasPrice”的统计值：最小值、平均值和最大值。同时，与每个交易的哈希相对应，从收据和跟踪中提取了“minerReward”、“gasUsed”和“error”字段。关于以太坊区块链的矿工，表 2.1 显示了有 5122 个独特的矿工地址。这意味着既然一个 peer 可能拥有多个地址，最多只有 5122 个 peer 充当矿工。同时，每个矿工都有权在区块中写入额外的文本。因此，我们也使用词云来分析矿工的文本。图 2.4a 显示了词云文本的可视化。结果显示，由于大多数矿工都在矿池中，他们在区块中留下了他们的名字以推广他们的挖矿能力。![../images/506524_1_En_2_Chapter/506524_1_En_2_Fig4_HTML.png](img/506524_1_En_2_Fig4_HTML.png)

图 2.4

数据集 1 可视化（彩色显示更佳）。(**a**) 矿工文本的词云。 (**b**) 交易次数。 (**c**) GasPrice 的宏观视图。 (**d**) GasPrice 的微观视图。

表 2.1

数据集 1 统计

| 统计 | 值 |
| --- | --- |
| 区块数量 | 8,100,000 |
| 交易数量 | 491,562,222 |
| 矿工地址数量 | 5122 |
| 每区块交易次数平均值 | 60.68 |
| 区块时间平均值 | 15.33 秒 |
| 区块大小平均值 | 11,457 字节 |

如表 2.1 所示，每个区块的交易次数平均为 60.68，区块时间为 15.33 秒。换句话说，以太坊的平均吞吐量大约为每秒 4 笔交易。即使当网络大部分活跃时，如图 2.4b 中 4,900,000 区块所示，吞吐量也大约为每秒 16.7 笔交易。这一结果暗示以太坊仍有很长的路要走，以支持实时互联网应用。在以太坊中，矿工有更高的优先级将“gasPrice”较高的交易打包进区块。 “gasPrice”的可视化如图 2.4c 和 d 所示。从宏观角度看，“gasPrice”随着以太坊社区的不断发展而逐渐下降，除了由于网络拥堵而造成交易异常频繁引起的一些峰值。从微观角度看，我们从 8,000,000 到 8,020,000 区块中提取时间，并发现“gasPrice”的此类波动可以遵循潮汐法则观察到。这一观察暗示“gasPrice”的波动 potentially 可以预测。

### 2.4.2 数据集 2：内部以太坊交易

以太坊是以太坊的原生加密货币。以太坊的交易不仅发生在区块记录的交易中，还发生在智能合约执行过程中。例如，如果有人要求智能合约向他人发送 10 以太坊，合约内的以太坊交易不会在区块中被观察到。在某些区块链浏览器（如 Etherscan），^(5)这种交易也称为“*内部交易*”。为了调查所有的以太坊交易，我们处理区块和跟踪数据以进行内部以太坊交易数据集。如表 2.2 所示，收集了在 54,688,782 个地址之间发生的 330,239,865 笔以太坊交易。以太坊的价值波动很大，最高值为 11,901,464.24 以太坊（目前约两亿美元），但平均值仅为 22.26 以太坊。图 2.5a 展示了每 10,000 个区块的总交易金额的统计信息。可以看出，以太坊交易最活跃的时间是 4,000,000 到 4,300,000 区块之间，这与初始币发行（ICO）最活跃的时间相匹配。关于如图 2.5b 所示的以太坊分布，我们发现大多数以太坊交易落在 0.1 以太坊到 1 以太坊的范围内，这表明大多数交易只转移少量的以太坊。![../images/506524_1_En_2_Chapter/506524_1_En_2_Fig5_HTML.png](img/506524_1_En_2_Fig5_HTML.png)

图 2.5

数据集 2 的可视化。（**a**）转移的以太坊金额。（**b**）以太坊交易分布

表 2.2

数据集 2 的统计信息

| 统计信息 | 值 |
| --- | --- |
| 以太坊交易数量 | 330,239,865 |
| 地址数量 | 54,688,782 |
| 以太坊平均金额 | 22.26 |
| 以太坊最大金额 | 11,901,464.24 |

### 2.4.3 数据集 3：合同信息

对于智能合约来说，更重要的平台是以太坊。创作者、创建时间、初始值、合约代码、创建代码，这些都是我们在处理跟踪数据后得到的基本智能合约信息，我们一步一步地实现了调查以太坊上所有智能合约的目的。"SUICIDE"操作码可以在函数中删除具有该操作码的智能合约并将其返回给他人。根据数据集 3 中的统计信息，从 133,039 个地址创建了 16,557,477 个智能合约。这意味着应该有很大比例的用户创建了多个合约。当主异常可以在表 2.3 中找到，有 5,704,054 个合约被删除，并将以太币余额返回给 19,133,738 个地址。通常，在删除过程中，智能合约不会将以太币退回到多个地址。这来自于服务拒绝(DoS)攻击。以太坊遭受了这种攻击。攻击者利用了"SUICIDE"价格的漏洞在以太坊上创建了一个账户。在修复漏洞之前，大量合约被删除并指向空地址，导致许多以太坊节点关闭，如前所述的工作(Chen 等 2017)。表 2.3

数据集 3 的统计

| 统计学 | 值 |
| --- | --- |
| 创建的合约数量 | 16,557,477 |
| 创作者地址数量 | 133,039 |
| 删除的合约数量 | 5,704,054 |
| 退款地址数量 | 19,133,738 |
| 合约十六进制代码大小的平均值 | 962.00 |

关于合约代码，我们将字节码翻译成十六进制代码。图 2.6a 给出了合约大小的统计。特别是，合约大小的平均值为 962.00，这表明智能合约占用的存储空间很小。合约大小分布也暗示了大多数合约的大小集中在一些簇上。这表明许多智能合约可能看起来很相似。这种相似性将在数据集 4 中进一步研究。图 2.6b 展示了创建的合约数量。图 2.6b 显示新智能合约的数量在增加，特别是在"ICO"概念（Howell 等 2018）提出后的时间。![../images/506524_1_En_2_Chapter/506524_1_En_2_Fig6_HTML.png](img/506524_1_En_2_Fig6_HTML.png)

图 2.6

数据集 3 的视觉化。(**a**)合同大小分布。(**b**)创建的合同数量。

### 2.4.4 数据集 4：合约调用

在 EVM 中，一个智能合约可以调用另一个来执行一些代码或函数。为了调查以太坊合约之间的调用（以地址表示），我们从跟踪数据集中提取执行中的合约调用。合约调用数据集包括调用者、被调用地址、调用函数。如表 2.4 所示，它由 11,485,720,090 个合约调用组成，其中 6,393,367,220 个包含输入代码和 169,463,261 个包含错误。图 2.7 给出了合约调用的可视化。特别是图 2.7a 和 c 显示，在从 2,300,000 到 2,460,000 块的时间段内，合约调用和错误非常频繁地发生。这是由于上一个小节提到的 DoS 攻击造成的，因为攻击者批量调用了大量合约，其中一些抛出了错误。图 2.7b 给出了调用类型的分布。特别是图 2.7b 显示，大多数开发者更倾向于使用“call”和“delegatecall”而不是“staticcall”和“callcode”，因为“call”和“delegatecall”的逻辑更清晰、更实用。图 2.7d 显示了调用合约时的错误类型，表明大多数错误是由“Out of gas”引起的，这主要是由于消息发送者的设置不当造成的。第二常见的错误是“Reverted”，这是开发者手动抛出的异常。此外，如“Bad instruction”和“Bad jump destination”等其他错误通常是由合约代码本身引起的。![../images/506524_1_En_2_Chapter/506524_1_En_2_Fig7_HTML.png](img/506524_1_En_2_Fig7_HTML.png)

图 2.7

数据集 4 的可视化。(**a**) 合约调用的计数。 (**b**) 调用类型分布。 (**c**) 合约错误的计数。 (**d**) 错误类型分布。 (**e**) 调用次数最多的前 10 个合约函数。

表 2.4

数据集 4 的统计数据

| 统计学 | 值 |
| --- | --- |
| 合约调用次数 | 11,485,720,090 |
| 带有输入的调用次数 | 6,393,367,220 |
| 带有错误的调用次数 | 169,463,261 |

通常，智能合约的编译器会使用函数名和参数的哈希值作为函数的入口。换句话说，在以太坊智能合约中，源代码中相同的函数在编译后的合约代码中将有相同的入口。然后我们统计调用合约函数来看哪些函数是最常用的。最常调用的前 10 个函数的分布如图 2.7e 所示。结果显示，大多数调用函数集中在一些类型上。例如，前 10 个函数占据了合约调用的 46.32%。此外，在验证了开源合约中函数的哈希值后，我们获得了源代码中的函数。然后我们得到了前 3 个函数：“transfer( address,uint256) ”，“balanceOf( add-ress) ”和“transferFrom( address, address, uint256) ”。这一结果暗示最常用的合约调用是关于代币的，由于类似的调用，合约之间可能存在很大的相似性。

### 2.4.5 数据集 5：ERC20 代币交易

从上面的分析中，我们观察到目前以太坊上最活跃的智能合约是代币合约。接下来我们进一步研究代币合约。为了收集代币的信息，我们处理收据数据集以提取标准事件，这些事件是在以太坊社区的标准 ERC20 协议中定义的。^(6)另外，每个 ERC20 代币都包含诸如名称、符号、总供应量等基本信息。然后我们将调用发送到本地以太坊对等节点以收集 ERC20 代币的此类基本信息。如表 2.5 所示，106,683 个智能合约被认为是 ERC20 合约，因为它们输出了定义为标准 ERC20 代币交易的事件。有 227,698,645 个 ERC20 交易涉及 42,146,575 个持有者地址。通常，持有者地址的数量可能远大于确切的人类持有者数量，因为一个用户可能拥有多个地址。同时，一些代币发行者会在未经用户许可的情况下向其他用户发送代币（也称为*代币空投*（van Valkenburgh 2017)）。图 2.8a 展示了每个 ERC20 代币的交易计数分布。从图 2.8a 中我们可以很容易地观察到马太效应（Merton 1968），因为大多数代币交易发生在少数代币合约中。图 2.8b 呈现了 ERC20 代币名称的词云。如图 2.8b 所示，最常见的词汇是“Chain”、“Coin”和“Share”，大多数 ERC20 代币都关注这些词汇。此外，另一个常见的词汇是“Test”，暗示许多部署在以太坊上的 ERC20 合约只是为了测试目的。![../images/506524_1_En_2_Chapter/506524_1_En_2_Fig8_HTML.png](img/506524_1_En_2_Fig8_HTML.png)

图 2.8

数据集 5 的可视化（彩色显示更佳）。（**a**）ERC20 流行度分布。（**b**）ERC20 代币的词云

表 2.5

数据集 5 的统计

| 统计 | 值 |
| --- | --- |
| ERC20 合约数量 | 106,683 |
| ERC20 交易数量 | 227,698,645 |
| 持有者地址数量 | 42,146,575 |

### 2.4.6 数据集 6：ERC721 代币交易

ERC721 代币是以太坊社区提出的另一种合约协议。^(7) 与 ERC20 代币不同，ERC721 代币是不可分割的。在合约函数中，参数不是代币的值而是代币 ID。例如，智能合约中的虚拟宠物可以是一个 ERC721 代币，它是不可分离但可以转让的。表 2.6 展示了 ERC721 合约的统计数据。我们发现，1954 个 ERC721 合约包含 7,524,827 个代币交易和 414,829 个持有者地址。值得注意的是，一些收集的合约并不完全遵循标准的 ERC721 协议。这些合约也包含在数据集中，因为它们在收据中输出了代币转让事件。图 2.9a 展示了 ERC721 代币的流行度分布。与 ERC20 代币相比，ERC721 代币的总量要少得多。主要原因是 ERC721 应用在每个代币上需要做更多的工作量，在视觉上进行展示，从而提高了开发难度。我们还研究了一个流行的 ERC721 代币合约，名为 CryptoKitties。它是最著名的 ERC721 代币合约之一，出售虚拟猫作为代币。每只猫在 ERC721 合约中代表为一个代币。我们计算了猫的出生区块分布的转手次数，如图 2.9b 所示。图 2.9b 还显示，在 4,500,000 到 5,000,000 区块出生的猫具有比其他猫更高的转手次数。那时，CryptoKitties 的种类达到了顶峰。图 2.9b 达到顶峰的时间与图 2.4b 和 c 几乎相同，暗示 CryptoKitties 的流行导致了以太坊的拥堵。![../images/506524_1_En_2_Chapter/506524_1_En_2_Fig9_HTML.png](img/506524_1_En_2_Fig9_HTML.png)

图 2.9

数据集 6 的可视化。（**a**）ERC721 流行度分布。（**b**）CryptoKitties 转手次数

表 2.6

数据集 6 的统计

| 统计 | 值 |
| --- | --- |
| ERC721 合约数量 | 1954 |
| ERC721 交易数量 | 7,524,827 |
| 持有者地址数量 | 414,829 |

## 2.5 XBlock-ETH 的应用

本节展示了 XBlock-ETH 框架的应用。如图 2.1 所示，以太坊架构包括节点、区块链、智能合约和代币。因此，我们也根据该架构的前三层对这些应用进行了分类。同时，我们还讨论了每一层的研究机会。

### 2.5.1 区块链系统分析

由于 XBlock-ETH 处理来自现实区块链系统的数据，因此它可以用来支持以下应用。

#### 2.5.1.1 去中心化分析

去中心化是区块链系统的重要特征之一。然而，关于区块链系统去中心化评估的研究很少。特别是，Wang et al. (2019)提出了比特币挖矿池的测量方法。尽管 Gencer et al. (2018)对比特币和以太坊的去中心化水平进行了测量研究，但他们的研究只考虑了网络带宽、挖矿能力和公平性等几项指标。相比之下，我们的 XBlock-ETH 数据为以太坊提供了更全面的测量。此外，我们的工作可以用来分析用户、合约所有者和矿工的去中心化。另外，我们的 XBlock-ETH 也可以用来与其他区块链系统进行比较，如比特币、EOS 或其他区块链系统。

#### 2.5.1.2 气体价格预测

由于交易费用等于“gasPrice”乘以“gasUsed”，用户可以在合理低的范围内控制“gasUsed”，以最小化矿工收取的交易费用。与此同时，我们可以从第 2.4.1 节了解到，每个区块中的最低“gasPrice”和平均“gasPrice”之间总是存在差距，这提供了节省费用的机会。近期如 Other-tech（Jin 2018）和 Majuri (2018)等研究分析了以太坊的“gasPrice”，而一些以太坊网站（例如，Etherscan（见脚注 5），Etherchain^(8))提供了预测短期“gasPrice”的工具。然而，这些工具本质上都是*黑箱*，它们的准确性和正确性无法得到保证。总之，对“gasPrice”的预测具有很大的经济价值，使得以太坊用户可以通过“gasPrice”预测来节省资金或缩短等待时间，而未来进行深入研究是值得的。

#### 2.5.1.3 性能基准

性能对区块链系统至关重要。有很多关于区块链性能优化的研究，如 Omniledger (Kokoris-Kogias et al. 2018)，Algorand (Gilad et al. 2017)和 RapidChain (Zamani et al. 2018)。同时，一些优化的区块链系统（例如，Monoxide (Wang and Wang 2019))采用了现实世界的区块链交易数据来对区块链系统进行性能评估。为了比较不同优化方法的表现，需要一个针对区块链系统的现实世界用例的通用基准。Zheng et al. (2018a)和 BlockBench (Dinh et al. 2017)提出了针对区块链系统的性能评估工具。性能基准需要模拟用户行为并获取与现实世界区块链系统类似的数据。在这种情况下，XBlock-ETH 框架可以被视为一个基准，因为源数据正是由现实世界用户生成的。

### 2.5.2 智能合约分析

作为最受欢迎的智能合约平台之一，以太坊吸引了许多软件开发者以及大量的智能合约。因此，与 EOS 和 Tron 等其他声称比以太坊具有更高的吞吐量和更低的延迟的智能合约平台相比，以太坊有一个更加活跃的开发者社区。因此，我们的 XBlock-ETH 框架（基于以太坊）可以用于智能合约的研究。我们总结了 XBlock-ETH 的潜在应用如下。

#### 2.5.2.1 合约相似性与推荐

正如 2.4 节所指出的，智能合约代码与智能合约的调用之间存在很大的相似性。代码相似性评估是软件工程中的一个传统研究课题，因为许多研究集中于代码相似性检测（Chilowicz 等人 2009; Luo 等人 2014）。一些近期研究关注智能合约的相似性分析。特别是，Etherscan（见脚注 5）提供了基于相似合约的查询系统。寻找相似合约对开发者开发新合约是有益的。例如，开发者可以在发布合约之前预测用户行为。同时，黄等人(2019)提出了根据智能合约现有代码推荐不同代码以更新智能合约的方法。此外，从用户角度来看，推荐相似的智能合约将帮助用户找到适合自己的合约。合约相似性与推荐的具体内容将在第四章讨论。

#### 2.5.2.2 合约开发者分析

开发者分析是软件工程中的另一个传统研究课题，包括开发者网络分析（Meneely 等人 2008）、行为分析（Layman 等人 2007）、故障预测（Weyuker 等人 2007）等。关于开发者分析，XBlock-ETH 也包括了大量的智能合约开发者网络。例如，有一些由不同开发者部署和提供的链上库；其他人可以调用这些库。每个开发者都可以通过他/她自己的以太坊地址来识别。因此，合约调用网络也可以被视为合约开发者的协作网络。开发者协作的网络和结构可能会告诉我们关于合约代码的可靠性。例如，开发具有漏洞的智能合约的开发者比其他人更有可能开发带有漏洞的新合约。从这个意义上说，我们的 XBlock-ETH 在分析开发者的智能合约之后，可以对开发者分析有益。

#### 2.5.2.3 合约漏洞检测

区块链安全和隐私近期引起了广泛关注（Su 等人 2020；Xu 等人 2019，2020a，b）。智能合约的安全性一直是区块链研究社区中的热门研究课题。特别是，智能合约的漏洞引起了额外的关注。许多针对以太坊的恶意攻击（例如，TheDAO 攻击）已经导致了巨大的损失（高达数百万美元）（Mehar 等人 2019）。为了防止智能合约受到恶意攻击，对合约进行漏洞检测是一个关键步骤。在漏洞检测方面有一些最新的尝试。例如，Oyente（Luu 等人 2016）、Zeus（Kalra 等人 2018）、teEther（Krupp 和 Rossow2018）、S-gram（Liu 等人 2018）和 ContractFuzzer（Jiang 等人 2018）提出了智能合约漏洞检测工具。在某些情况下，智能合约的漏洞检测方法可以借鉴和启发传统软件漏洞检测方法，因为它们本质上等同于代码的验证。在这方面，一些研究专注于验证区块链上的合约代码；这些合约代码也被称为“字节码”或“操作码”。我们的 XBlock-ETH 本质上包括了合约代码的数据，可以应用于合约漏洞检测。

#### 2.5.2.4 欺诈检测

由于巨大的经济价值和智能合约的普及，智能合约可能会被恶意用户用作骗局。例如，承诺高回报以吸引受害者投资的众筹合约。据 Chen 等人 2018b 报道，庞氏骗局合约可以诈骗他人的加密货币。已经提出了几种方法（Bartoletti 等人 2020；Chen 等人 2018b，2019；Torres 等人 2019）来检测以太坊上的欺诈合约。大多数方法主要基于智能合约的代码和交易记录，而这些都包含在 XBlock-ETH 数据中。因此，XBlock-ETH 数据可以在欺诈检测中进一步利用。

### 2.5.3 加密货币分析

基于区块链的加密货币近年来由于其去中心化和成本降低而成为一个热门话题。在以太坊中有大量的加密货币，包括以太币、ERC20 代币和 ERC721 代币。据 CoinMarketCap^(9)显示，超过 2000 种代币可以在第三方交易所使用。因此，基于区块链数据的加密货币分析可以带来巨大的经济价值。我们将加密货币分析大致分为加密货币转移分析、加密货币价格分析和虚假用户检测，如下所述。

#### 2.5.3.1 加密货币转移分析

加密货币交易的分析是进行加密货币转账分析的初步步骤。关于以太币转账，Chen 等人(2018a)对以太币交易进行了图分析，并从图分析中得出了一些洞见。关于 ERC20/ERC721 代币，Victor 和 Lüders(2019)以及 Somin 等人(2018)提出了代币交易网络的分析。在加密货币交易分析之后，可以进一步分析用户行为。例如，代币用户可能形成不同的社区。可以通过分析加密货币交易来开展社区发现。此外，基于区块链的加密货币的匿名性可能导致洗钱行为，这可以通过加密货币交易分析本质上进行识别和检测。我们的 XBlock-ETH 数据为解决这些问题提供了潜在解决方案。

#### 2.5.3.2 加密货币价格分析

区块链加密货币的价格受到多种不同因素的影响，比如政府政策、技术革新、社会情绪和商业活动。最近的一些研究聚焦于加密货币价格分析和预测（Abraham 等人 2018；Lamon 等人 2017；Mensi 等人 2019）。典型的加密货币价格分析包括三个步骤：（1）从加密货币交易所收集价格数据，（2）确定加密货币价格与其他因素的相关性，（3）预测未来价格和潜在利润。然而，有时加密货币的价格可能被某些方面恶意控制。因此，进行数据清洗以获得准确和正常的加密货币价格数据是必要的。一些加密货币价格数据存储在去中心化交易所合约中，可用于加密货币价格分析，而原始数据可能需要进一步预处理以便于未来的分析。

#### 2.5.3.3 虚假用户检测

假用户检测（Cao 等人的研究 2012；Ferrara 等人的研究 2016；Varol 等人的研究 2017）是社交网络中的一个传统研究课题。在区块链系统中，加密货币用户也形成了类似社交网络的社区，在这些社区中，开发者控制的一些假用户为了提高 DApps 的活动排名。由于 DApp（或加密货币）的排名是基于与用户活动相关的某些指标，比如日活跃用户（DAU）。因此，许多开发者利用这个漏洞制造一些假用户来提高活动水平，以获得更高的排名。尽管一些 DApp 网站，如 DAppReview（参阅文献 10）会标记有假用户的加密货币，但这种假用户检测几乎是在黑盒中或手动完成的。此外，关于加密货币的假用户检测的研究很少。通常免费使用的无需授权的区块链系统可能会倡导比需要授权的区块链系统更频繁的假用户活动。我们的 XBlock-ETH 将来会进一步改进以支持假用户检测。

## 2.6 总结

本章介绍了经过精心处理的最新以太坊链上数据集，即 XBlock-ETH，它包括以太坊区块链、智能合约和加密货币的数据。此外，还展示了数据集的全面统计和探索。XBlock-ETH 数据集已在 XBlock.pro 网站上发布。此外，还概述了 XBlock-ETH 数据集的研究机会。我们的 XBlock-ETH 有望促进以太坊的研究。未来的改进如下：**(1) 更多特性：** 本章给出了数据集基本特性的探索。以太坊是一个复杂的生态系统，包括去中心化金融、稳定币等。将来会探索更多以太坊数据的特性和**(2) 从以太坊获取额外的链下数据：** 由于链下数据提供了关于开发者和用户链下行为的宝贵信息，因此它也很重要。将来，将收集链下数据。**(3) 与其他区块链系统联合数据分析：** 还有一些其他吸引了大量用户和开发者的区块链系统。将来会进行以太坊和其他无需授权的区块链系统的联合数据分析。