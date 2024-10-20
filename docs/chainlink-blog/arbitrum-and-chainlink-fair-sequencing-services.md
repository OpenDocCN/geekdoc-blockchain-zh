# 使用 Arbitrum 和 Fair 测序服务创建高度可扩展和抗 MEV 的 DeFi 生态系统

> 原文：<https://blog.chain.link/arbitrum-and-chainlink-fair-sequencing-services/>

[【智能合约】](https://chain.link/education/smart-contracts) 经济在短短几年时间内创造了一个庞大的分散式应用生态系统，支持独特的市场，如 [分散式金融](https://blog.chain.link/analyzing-the-defi-ecosystem-and-the-many-ways-chainlink-can-accelerate-adoption/)(DeFi)[不可替换代币](https://chain.link/education/nfts)(NFTs)[即玩即赚游戏](https://blog.chain.link/what-is-play-to-earn/) 等等。然而，如果智能合同经济要搭载下一个十亿用户并成为合同协议的主导系统，它将需要通过最大限度地减少 [矿工可提取价值](https://blog.chain.link/what-is-miner-extractable-value-mev/) (MEV)的有害影响，来扩展其交易处理能力并保持高度信任。在本帖中，我们将探讨 Chainlink 推荐的在以太坊、Arbitrum 上扩展智能合约的解决方案，以及 Arbitrum 和 Chainlink 如何共同探索通过消除 Arbitrum 上的 MEV 来创建更公平的智能合约的解决方案。

可扩展性有许多不同的方法，第 2 层解决方案使用一种称为“rollups”的技术，成为扩展以太坊等现有生态系统的主要方法。这在很大程度上是由于 rollups 能够实现现有智能合约代码的可扩展交易处理，同时保持与其他也用 Solidity 等语言编写的 dApps 的可组合性，并提供第 1 层以太网的底层安全保证。

不幸的是，汇总仍然受制于困扰第一层区块链的某种形式的 MEV，同样限制了它们的可信度。MEV 是挖掘者/排序者的副产品，他们能够选择他们产生的块内的事务顺序，使他们能够通过 [【前置】和](https://arxiv.org/abs/1904.05234) 等技术操纵事务排序，以他人为代价为自己谋利。MEV 使得任何基于时间顺序的流程都变得容易被破坏，极大地限制了智能合约的可信度，也限制了我们的行业被更广泛地采用。

为了最大程度地解决 MEV 问题，Chainlink 团队一直在开发一种解决方案: [公平排序服务](https://blog.chain.link/chainlink-fair-sequencing-services-enabling-a-provably-fair-defi-ecosystem/)【FSS】——一种分散的交易排序服务，使交易的时间排序对所有用户都是公平和可预测的。通过使用 FSS 作为订购交易的方法，智能合约经济可以通过使用领先的第 2 层汇总(如 Arbitrum)同时实现可伸缩性，并减轻 MEV 的信任侵蚀效应(如果将 FSS 应用于相同的第 2 层)。

在下面的博文中，我们将简要介绍 rollup 技术及其核心优势，探索最广泛使用的乐观 rollup 以及 Chainlink 推荐的在以太坊、Arbitrum 上公平扩展您的智能合约的解决方案，并讨论 Arbitrum 如何探索 FSS 的集成以最小化 MEV，恢复交易订单的公平性。

## 什么是汇总及其核心优势？

一般来说，汇总将执行用户事务所需的计算从第 1 层区块链转移到以较低成本执行的离线第 2 层网络。然后，汇总通过在第一层区块链上张贴交易数据及其离线计算的精简证明来保留它们所支持的第一层区块链的安全性，在第一层上，交易数据及其离线计算可以被争议/无效。

从稍微更专业的角度来说，可能涉及数百个独立交易的用户交易数据被捆绑成一个汇总交易，发布在第一层区块链上。操作该汇总的节点然后生成新的状态根——网络当前状态的加密散列——该状态根也被发布到第一层区块链上，作为支持其工作的声明。然后通过有效性证明(生成一个 [零知识证明](https://blog.chain.link/what-is-a-zero-knowledge-proof-zkp/) )或欺诈证明(追溯性地证明一个状态根是不正确的)来验证该声明是合法的。有效性证明与 ZK 汇总相关联，而欺诈证明与乐观汇总相关联。

在乐观汇总的情况下，在提出索赔后，有一个争议期(通常为一周),在此期间，任何人都可以发布欺诈证明，如果他们认为某个州根是不正确的。如果在此期间没有发布欺诈证据，则交易被视为有效，因此有“乐观”一词然而，如果创建了防欺诈，那么所讨论的事务要么全部要么部分地在第 1 层网络上执行，以查看结果是否与声明相冲突。如果链上执行的结果与该声明不匹配，则该声明(状态根)和任何后续声明将被还原，并且提出该声明的实体的股份将被削减。如果最初的声明被证明是真实的，那么提出错误警报的实体将被砍掉。

由于乐观汇总的所有交易数据直接存储在第 1 层网络上，任何运行汇总节点的人都可以生成汇总链的最新状态，并根据需要发布欺诈证明。通过这种设计，只需要一个诚实的实体来检查乐观汇总网络的状态，以确保用户资金的安全。如果用户选择自己执行这项工作，他们不需要为了资金的安全而信任任何外部实体。此外，这种设计允许用户在任何时候强制撤回到第一层区块链，这意味着用户的资金永远不会卡在第二层网络上。

将大部分执行工作移出链外，仅在第 1 层区块链上存储少量数据，这意味着第 2 层汇总只需很小一部分成本就能提供类似的安全性。正是由于这些优势，汇总已成为以太坊等区块链的可伸缩性选择，最终实现了更广泛的采用，因为更多的用户可以负担得起与应用程序的交互，应用程序可以以接近实时的速度运行，以迎合快速变化的市场。

## Arbitrum 的乐观汇总协议

根据运营跟踪记录、社区规模和安全价值，领先的第 2 层汇总是 Arbitrum。Arbitrum 已经引起了更广泛的加密货币社区的极大兴趣，因为它是 rollup 技术的先驱之一，并得到了行业领导者团队的支持。Arbitrum 背后的开发公司 Offchain Labs 团队由密码学和区块链技术领域的领先计算机科学家组成，包括前白宫首席技术官 Ed Felten 和普林斯顿大学博士 Steven Goldfeder 和 Harry Kalodner。

对于部署在 Arbitrum 上的开发团队来说，一些好处包括完全的 EVM 兼容性，这意味着 Arbitrum 可以使用现有的工具和基础设施 运行未经修改的 Solidity smart 契约并执行以太坊式的交易。Arbitrum 还具有很高的可伸缩性，事务成本极低，因为它使用了将契约计算和状态存储移出链的乐观汇总模型。

Arbitrum rollups 使用创新的 [交互式防欺诈](https://medium.com/offchainlabs/interactive-fraud-proofs-arbitrums-secret-sauce-debc3b019418) 机制作为一种高效、低成本的方式来证明第一层区块链上的欺诈。Arbitrum 的交互式防欺诈设计涉及一个由第 1 层合同审核的来回协议，该协议将争议分解为在以太网上执行的一步计算，而不是像重新执行整个交易这样成本更高的替代方案。Arbitrum 的方法带来了一些强大的特性，例如与以太坊相比，允许更高的每次交易 gas 限制，以及取消 Arbitrum 上智能合约的大小限制。

重要的是，这些可扩展性功能是在与以太坊 L1 的关系中以高度信任最小化的方式实现的——这是因为 Arbitrum 的安全性植根于以太坊，允许任何一方确保正确的第 2 层结果。通过不牺牲安全性来实现以太坊智能合约的规模，智能合约生态系统作为一个整体可以轻松扩展，并支持更高级的应用程序。阅读 [Arbitrum 协议深度潜](https://developer.offchainlabs.com/docs/inside_arbitrum) 可以了解更多。除了 [集成对 chain link Price Feeds](https://www.prnewswire.com/news-releases/chainlink-oracles-now-running-live-on-arbitrum-one-301354380.html)的支持，众多领先的 DeFi 项目已经在 Arbitrum One 网络上启动。Arbitrum One 上不断发展的 dApps 生态系统现在可以使用 Arbitrum 门户网站[](https://portal.arbitrum.one/)进行探索。

## 通过公平测序服务降低 MEV

作为 Offchain Labs 和 Chainlink Labs 合作的延续，两个团队都致力于通过探索应用 [公平测序服务](https://blog.chain.link/chainlink-fair-sequencing-services-enabling-a-provably-fair-defi-ecosystem/)【FSS】——一种分散的交易订购解决方案来减轻 MEV 的不利影响，从而最大限度地降低 MEV。FSS 使用包括 Chainlink 节点的分散式 oracle 网络来收集链外的用户交易，为交易排序生成分散式共识，并使用 Arbitrum 协议以分散方式提交排序的交易。我们非常高兴能与 Offchain 实验室合作，探索 FSS 如何帮助分散 Arbitrum 测序仪并将 MEV 降至最低。

正如 Chainlink Labs 首席科学家 Ari Juels 在其最近在 SmartCon 2021 上的演示中所探讨的那样，FSS 正计划分两个阶段进行部署。第一阶段涉及安全因果排序(原子广播)，其中用户事务首先由用户加密以隐藏事务细节，由分散的 oracle 网络排序，然后由 Arbitrum 协议解密以供执行。因此，在订购流程开始之前，事务有效负载将对节点不可见，从而无法根据早期可见性提前运行事务。

在第二阶段，这是 Arbitrum 合作的重点，[【Aequitas ordering(consensus)](https://eprint.iacr.org/2021/139.pdf)(共同作者包括 Chainlink Labs 的 Ari Juels 和 Arbitrum 的 Steven Goldfeder)将在 FSS 实施，用于基于绝对多数接收时间的交易订购。这有助于实施先进先出(FIFO)排序策略，当与第一阶段的交易加密相结合时，为用户交易的公平排序提供了深度防御解决方案。使 FSS 成为可能的技术在 [Chainlink 2.0 白皮书](https://research.chain.link/whitepaper-v2.pdf) 的第 5 节中有进一步的深入探讨。

最终，FSS 与 Arbitrum 协议的结合将有助于为用户提供更大程度的保证，即他们的交易顺序不会被操纵。随着更多 dApps 部署在 Arbitrum One 上以及网络的总锁定价值上升，这种保证变得越来越重要。此外，FSS 将通过创建一个分散的定序器来增加 Arbitrum 协议的可靠性，从而最大限度地降低停机风险。Arbitrum 领先的第 2 层汇总功能和 FSS 提供的交易公平性的完美结合，使 Arbitrum Chainlink 成为将以太坊扩展到全球所有 dApps 数十亿用户的推荐解决方案。

![The Arbitrum protocol with FSS](img/8e06aabec5dc5ddea8574e48d109eb99.png)

<figcaption id="caption-attachment-3055" class="wp-caption-text">The Arbitrum protocol with FSS</figcaption>



“分散 Arbitrum 协议的定序器一直是我们的长期目标，以增加信任最小化，并为用户提供最大限度降低 MEV 的有力保证。Offchain Labs 的联合创始人 Steven Goldfeder 表示:“我们很高兴能够通过与 Chainlink Labs 的长期合作，探索将 FSS 应用到 Arbitrum 中，chain link Labs 拥有一支经验丰富的团队，专注于学术研究的方法，并在为高价值智能合同提供安全可靠的 oracle 解决方案方面取得了成功。

“Arbitrum One 的推出给我们留下了深刻的印象，它为现有的以太坊生态系统提供了急需的扩展解决方案，该解决方案易于集成，同时保持了以太坊 L1 的安全属性。由于团队的技术专长和基于学术研究的方法，Chainlink Labs 一直与 Offchain Labs 进行长期合作，探索将 FSS 集成到 Arbitrum 中。Chainlink 的联合创始人 Sergey Nazarov 表示:“我们很高兴能够在公平和分散的交易排序方面建立一个新的行业标准，并让开发人员能够构建高度可扩展、抗 MEV 的智能合约应用。