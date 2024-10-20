# Chainlink 2.0 超线性定位:概述

> 原文：<https://blog.chain.link/explicit-staking-in-chainlink-2-0/>

最近发布的 [Chainlink 2.0 白皮书](https://blog.chain.link/chainlink-2-0-lays-foundation-for-adoption-of-hybrid-smart-contracts/) 引入了多种创新，旨在显著提高 [分散式 Oracle 网络](https://blog.chain.link/what-is-chainlink/) (DONs)的能力，最显著的是使 DONs 能够执行安全的链外计算。随着 DONs 为智能合约提供对数据交付之外的更广泛的分散服务的访问，开发人员可以使用更广泛的混合基础设施，使他们能够将链上代码与链下资源结合起来，以构建越来越先进的智能合约。

供应这些下一代 [混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/) 的一个方面是为 don 创建一个强大的加密经济安全模型，最大化攻击成本。这对于扩展 don 的安全性至关重要，因为他们越来越多地参与保护影响用户资金的高价值智能合同中的关键功能。为了实现更高水平的防篡改性，该论文提出了 *显式桩*——一种正在开发中的高级密码经济系统，其中 Chainlink 节点锁定链接令牌作为抵押品，可以针对恶意和不良行为进行削减。

chain link staking 模型是独一无二的，因为它旨在防范极其广泛的资金雄厚的对手，并实现 *超线性赌注影响*——一种要求恶意参与者的预算远远大于 DON 内所有节点存款总和的机制，以经济高效的方式为高价值[智能合同](https://chain.link/education/smart-contracts)应用程序创建越来越大的安全保证。

![Chainlink’s super-linear explicit staking](img/50be8f5bc5144fd50644c0449e1c7c6a.png)

<figcaption id="caption-attachment-2146" class="wp-caption-text">Chainlink’s explicit staking mechanism is super-linear as the number of nodes increase</figcaption>



在本文中，我们概述了 Chainlink 2.0 网络中的显式赌注，以及它将如何为用户带来更高级别的加密经济安全性。有关 Chainlink 的显式定位模型及其所有技术细节的更多信息，请参考 Chainlink 2.0 白皮书[](https://research.chain.link/whitepaper-v2.pdf)的第九节。

## **在分散式 Oracle 网络中显式定位的作用**

Chainlink 的显式锁定机制旨在实现与 [【区块链网络](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/) 内的锁定完全不同的目标。虽然区块链的利益相关证明使用了一种利益相关机制来生成对一组连续创建的块进行排序的全球共识，但 Chainlink 2.0 中的显式利益相关旨在创建可靠且防篡改的 oracle 报告，准确反映区块链(链外)之外的特定真实事件的状态。

最终，Chainlink 2.0 中显式赌注的目标是增加 DONs 的加密经济安全性，为用户提供围绕其高价值混合智能合约所依赖的 [外部数据](https://blog.chain.link/understanding-how-data-and-apis-power-next-generation-economies/) 和 [链外计算](https://blog.chain.link/off-chain-computation-statistical-analysis-with-chainlink/) 的有效性和及时性的更大保证。迄今为止，Oracle staking 机制仅设计用于防范有限的攻击，而不具备现实对手的能力。相比之下，Chainlink 的显式赌注机制可以抵御各种攻击，包括预期贿赂等高级策略，其中节点根据其在网络中的角色而成为目标，例如那些被选中进行报告裁决的节点。

## **链环明确标桩的基础**

chain link 2.0 白皮书描述了显式堆栈将如何保护负责在链上提供金融市场数据的 don，这是许多 [DeFi](https://chain.link/education/defi) 应用程序所需的常见外部数据资源。所提出的显式赌注机制由多个独立的组件组成，这些组件组合起来产生大量的密码经济安全性。

### **服务协议**

在每个 DON 的背后是一个服务协议，它将定义每个 [oracle 节点](https://blog.chain.link/what-is-a-chainlink-node-operator/) 所需要的链路令牌的数量和关键性能要求，例如单个节点的响应可以偏离聚合值多远，以及 oracle 报告中的聚合值可以偏离它应该表示的正确值多远。服务协议还可以定义其他参数，比如使用的数据源、更新的频率、每个节点的费用等等。

由 DON 产生的输出被构造成报告轮次，其中每轮次涉及创建新的 oracle 报告，该报告包含每个节点对特定数据(例如，ETH/USD 的价格)的个体响应，所有个体响应被聚合成单个值(例如，取中值)。DON 网络的服务协议定义了每个报告应该如何生成，以及可以削减节点股份的条件。

可以选择任何节点参与 DON 的服务协议，包括现有的高度可靠和声誉良好的节点运营商，这些运营商已经在 DeFi 生态系统中获得了数百亿美元的收益。可以使用现有的 Chainlink 信誉框架来过滤和选择节点，如[chain link Market](http://market.link)，它提供了一个无许可的市场，该市场突出了历史节点运营商性能，如正常运行时间、等待时间、响应偏差、支持的网络、数据源等。

![market.link](img/16eef9df74a92326b93587939c575f3a.png)

<figcaption id="caption-attachment-2144" class="wp-caption-text">Example of node operator performance as shown on market.link</figcaption>



### **双层 Oracle 网络**

为了确保充分履行服务协议的条款，将使用双层[甲骨文](https://chain.link/education/blockchain-oracles)网络设计。这就涉及到一个高效低成本的 *第一层* DON，由明确标注链接令牌的节点组成，负责定期持续生成新的聚合 oracle 报告。此外，安全性最高且成本较高的 *第二层* DON 将用于解决第一层生成的有关 oracle 报告有效性的任何争议。双层 oracle 网络设计优化了正常使用期间的效率，同时在第二层仲裁期间优先考虑防篡改和精确度，以确保第一层网络中的节点对恶意行为和糟糕的性能负责。

当前实施的 Chainlink 网络已经运行了两年多，产生了数百万的链上交易，并在 DeFi 经济中获得了数百亿美元的收益。从来就不需要仲裁层，因为现有的加密经济激励机制已经确保了声誉良好的 Chainlink 节点运营商即使在区块链网络拥塞期间也能继续可靠地发布准确的 oracle 报告，而不会出现问题，从而不会危及他们的声誉或收入。然而，作为一种过度的谨慎，在极不可能发生争议的情况下，Chainlink 2.0 模型支持内置的第二层仲裁层，提供了更大的安全保证。

### **通过用户投票实现二级网络的加密经济安全性**

在极少数情况下，由第一层 oracle 网络生成的 oracle 报告会引发争议，由下面进一步描述的看门狗/警报器机制触发，争议将由较慢的第二层委员会解决，该委员会由数百乃至数千个独立的 Chainlink 用户组成，如 Aave、Synthetix、Compound 等。如果产生了争议，这些用户将使用由 [DECO](https://arxiv.org/pdf/1909.00938.pdf) 生成的加密 TLS 证明，对有问题的原始 oracle 报告的准确性进行投票，该证明提供了来自一个或多个数据提供商的权威的 [零知识证明](https://blog.chain.link/what-is-a-zero-knowledge-proof-zkp/) 。DECO 提供了高效、低成本和防篡改的仲裁，允许第二层参与者在不访问原始数据源的情况下解决争议。

**由于每个 Chainlink 用户的智能合约应用程序及其包含的用户资金的安全性取决于来自 Chainlink 网络的准确 oracle 报告，因此每个二级投票人都有很高的经济激励来正确解决争议，而不会危及其应用程序的安全性、声誉和可用性，也不会潜在地损害其应用程序的本机令牌的价值。** 即使在极少数用户恶意投票的情况下，绝大多数二级参与者在游戏中也有很大程度的利益，因为他们的应用程序从根本上依赖于准确的 oracle 报告。随着每一个额外付费用户的增加，Chainlink oracle network 的安全预算不仅会增加，而且经济合理的二级参与者的数量也会增加。

这些第二层参与者可以包括管理链式应用程序的核心开发团队，以及由管理此类应用程序的令牌持有者组成的分散自治组织(Dao)。在 Dao 使用其本地监管令牌对二级争议进行投票的情况下，二级的加密经济安全性会随着流程中使用的所有监管令牌的总经济价值成比例增加。任何投票反对 DECO proof 的第二层参与者将被鼓励投票支持准确的 oracle 报告的用户集合投票否决，并将建立错误投票的链上记录，这可能会损害其应用程序的声誉。

### **优先看门狗报告**

为了确保第二层 oracle 网络在发生争议时被正确调用，第一层网络中的任何节点都可以充当 *看门狗* ，如果它认为来自 oracle 报告的合计值不正确，则发出警报。在每个报告周期中，第一层网络中的每个节点被随机分配一个公共优先级数，该公共优先级数确定第二层网络处理它们的警报(如果有的话)的顺序。例如，在具有 100 个节点的第一层网络中，每个节点将被分配一个范围从 1 到 100 的唯一编号。

如果看门狗节点发出警报，并且第二层网络确定第一层的原始集合报告不正确，则由恶意的大多数第一层节点存放的所有标记链接被切断(取走)并给予具有最高优先级编号的发出警报的看门狗节点。这为第一层节点以经济合理的方式作为监督者产生了强大的财务激励，特别是因为如果聚集的 oracle 报告被确定为不正确，监督者有机会获得大量削减的股份。

![Chainlink’s two-tier oracle network](img/aeb412f5932f9eaf7f27ea0c569076a6.png)

<figcaption id="caption-attachment-2141" class="wp-caption-text">In the highly unlikely case that a majority of nodes in the first tier are corrupted/bribed and emit an incorrect value, rather than the correct report value, the watchdog node(s) sends an alert to the second-tier network, which determines and emits the correct report value, resulting in corrupted nodes forfeiting their deposits to the highest priority watchdog node.</figcaption>



### **集中奖励**

这种按优先顺序排列的看门狗报告系统推动了回报的集中，产生了超线性的赌注影响——恶意行为者成功腐蚀 DON 所需的预算随着节点数量的增加呈二次方增加，即使是资金雄厚的对手也能获得最大的防篡改能力。虽然集中削减的股份奖励被给予最高优先级的节点，但是第一层网络中的任何节点都有机会充当看门狗。因此，如果总报告是错误的，较低优先级的节点仍然有动机发出警报，因为如果较高优先级的节点没有发出警报(例如，那些节点被贿赂或离线)，它们可以赢得被削减的股份。

为了让恶意参与者防止任何警报被提升到第二层，他们将被要求向每个第一层 DON 节点行贿全部集中的奖励金额，这大大增加了贿赂 DON 的可行贿赂的最低总成本。通过向单个节点提供集中的警报奖励，与在所有警报节点之间平均分享削减的股份相比，总体上为 DON 创建了更多的加密经济安全性。

![Chainlink explicit staking concentrated alerting rewards ](img/16f886c5fde83a59f153088d9884e98b.png)

<figcaption id="caption-attachment-2145" class="wp-caption-text">A malicious actor must bribe each node with more than the reward it stands to gain by alerting (shown as a red bar). The total payout by the adversary for a viable bribe (gray regions) is much larger with concentrated than shared alerting rewards.</figcaption>



### **量化链环显式打桩的安全性**

为了量化这种超线性的打桩影响动态，白皮书提供了以下解释:

假设存在一个第一层唐，有*【n】*个节点，其中每个节点存放 *d* 笔股份，从而导致网络中的股份总额为*【dn】*。创建不正确的合计 oracle 报告需要破坏大多数节点，确保恶意节点下注资金的合计价值至少为*dn/2*。如果第二层发出警报并认为其有效，那么最高优先级的看门狗将因此从所有被削减的恶意节点中至少获得*dn/2*。然而，因为任何节点都可以成为看门狗，所以每个节点都需要接受至少相同金额的贿赂才能不发出警报。因此，对手破坏第一层 DON 所需的总预算至少是 dn /2 ，这是节点数量的二次值。

下图摘自 Chainlink 2.0 白皮书的第 9.4.2 节，提供了一个具体的例子，说明一级网络分散性的增加如何成倍地增加了敌对行动者腐败堂所需的预算。

![Showing the decentralization of the first tier of nodes](img/36c4270525e9f69c528cdfa230e30371.png)

### **引发警报的潜在后果**

通过这种显式的赌注机制，在一级 DON 发布汇总的 oracle 报告后，可能会出现三种结果:

 **1.  **完全一致** :所有第一层节点运行正常，并且一致认为 oracle 报告中的聚合值是正确的。每个节点为其 oracle 服务支付固定的每轮费用。
2.  **部分一致** :一些节点脱机或少数节点报告数据损坏，但大多数节点产生正确的值，并且创建了聚合报告，没有发出警报。所有诚实的/可操作的节点因其服务而被支付费用，而所有有故障的/离线的节点的股份被削减适量(例如 10 倍的费用支付)。
3.  **警报** :如果一级网络中的一个或多个节点认为聚合报告不正确，它们公开触发警报，将验证升级到二级网络，导致两种可能的结果:

*   **正确警报** :第二层网络确认第一层的聚合报告不正确，导致所有恶意节点的全部股份被削减并授予最高优先级的警报看门狗。
*   **故障警报** :第二层网络与第一层网络产生的总价值一致，认为升级有故障，并导致所有警报节点的股份被适度削减。

作为显式赌注机制的结果，第一层网络中的每个节点不仅有强烈的动机为每个报告提供准确和可靠的数据，而且有强烈的动机在最终聚集的 oracle 报告被破坏的情况下报告恶意节点的不当行为。

### **误报保险**

尽管来自恶意节点的所有被削减的股份都被判给了最高优先级的警报看门狗，但如果生成了不正确的 oracle 报告，用户可能仍然希望得到补偿。这是因为在多轮警报机制实施中，用户可以选择乐观地接受来自第一层的新 oracle 报告(由可信的仲裁威胁保护),或者可以等待查看第二层是否发出并解决了任何警报。

向乐观地接受来自第一层 oracle 网络的 oracle 报告的用户销售保险的保险商可以提供误报保险。该保险协议可以采用链上智能合同的形式，该合同基于从第一层和第二层 oracle 网络生成的已签名 oracle 报告来执行。如果这些报告不同，可以自动向投保人支付一笔款项。因为链式网络生成关于每个节点和 DON 的历史性能的大量数据，所以保险成本可以保持较低，同时对于承保人来说仍然是可持续的。

## **结论**

通过超线性显式赌注创建额外的加密经济安全性，Chainlink 网络可以扩展以支持下一代混合智能合同，从而确保不断增加的价值。如果智能合同将成为数字协议的主导形式，那么这种加密经济安全性的提升对于为用户提供准确、及时和防篡改地执行直接依赖 oracle 报告和计算的分散式应用程序的最大保证将是至关重要的。

[Chainlink 2.0 白皮书](https://research.chain.link/whitepaper-v2.pdf) 对 chain link 提出的显式锁定机制进行了更深入的分析，如附加的细微差别、设计注意事项以及每个组件背后的解释。如果您有兴趣了解更多信息，请参考白皮书的第 9 部分。

## **关于这个话题的更多信息**

*   [Chainlink 2.0 为采用混合智能合约奠定基础](https://blog.chain.link/chainlink-2-0-lays-foundation-for-adoption-of-hybrid-smart-contracts/)
*   [去中心化甲骨文网络的下一步发展](https://research.chain.link/whitepaper-v2.pdf)
*   [SCRF Chainlink 2.0 白皮书摘要](https://www.smartcontractresearch.org/t/research-summary-chainlink-2-0-next-steps-in-the-evolution-of-decentralized-oracle-networks/300)

如果您是一名开发人员，并且希望使用 Chainlink 网络将您的智能合约安全地连接到链外数据和计算， 请访问 [Chainlink 开发人员文档](https://docs.chain.link/) 或[联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog)。T11】**