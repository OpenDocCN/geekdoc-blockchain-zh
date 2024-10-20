# Chainlink 2.0 为采用混合智能合约奠定了基础

> 原文：<https://blog.chain.link/chainlink-2-0-lays-foundation-for-adoption-of-hybrid-smart-contracts/>

自三年前发布[原始 Chainlink 白皮书](https://research.chain.link/whitepaper-v1.pdf)以来，Chainlink 已经发展成为每个新兴智能合同垂直领域中使用最广泛的分散式 [oracle](https://chain.link/education/blockchain-oracles) 解决方案，包括 [DeFi](https://chain.link/education/defi) ，保险，游戏， [NFTs](https://chain.link/education/nfts) 等等。Chainlink 网络上不断扩展的分散服务套件正在推动众多领先区块链的创新，为开发人员提供了一系列关键的 oracle 功能:

*   [**chain link Price Feeds**](https://chain.link/solutions/defi)为各种资产提供广泛的链上金融市场数据，用于为领先的 DeFi 应用程序(如 Aave、Synthetix 和 dYdX)获取数十亿美元的资金。
*   [**Chainlink VRF**](https://chain.link/solutions/chainlink-vrf) 生成由链上加密证明支持的可验证的随机性，使像 Aavegotchi 这样的项目能够铸造具有可证明罕见属性的 NFT，并将其汇集在一起，以公平地选择无损失彩票中的赢家。
*   [**chain link Proof of Reserve**](https://chain.link/solutions/proof-of-reserve)提供链上数据馈送，使 smart contracts 能够对令牌化资产储备执行按需审计，如 TUSD 和帕克斯等稳定资产和跨链令牌。
*   [**Chainlink 外部适配器**](https://blog.chain.link/build-and-use-external-adapters/) 为开发人员提供工具来创建与任何链外资源或 API 的连接，由 Arbol 的参数作物保险市场利用来获取天气数据，Everpedia 的预测市场用户来获取美国选举结果。

Chainlink 网络通过在分散的 oracle 市场中的广泛采用实现了广泛的网络效应，并且已经获得了数十亿的链上价值。虽然走到这一步并非易事，但我们只触及了分散式 oracle 网络及其支持的[智能合同](https://chain.link/education/smart-contracts)的皮毛。

为了展示 oracle 支持的智能合同的未来愿景，我们推出了 [*Chainlink 2.0:分散式 Oracle 网络*](https://research.chain.link/whitepaper-v2.pdf) 发展的下一步——这是一份新的白皮书，概述了 **Chainlink 分散式 Oracle 网络如何继续创建分散式元层，以高度可扩展、保密和安全的链外计算形式增强智能合同，以及 Chainlink 目前已经提供的外部数据。**

该白皮书介绍了一种用于构建[混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/)的新架构，其中分散式 Oracle 网络提供了区块链无法提供的关键功能，作为一个安全的链外计算层，该计算层在一定程度上依赖于区块链的安全性，但仍能以链外系统的连通性、功能丰富性和可扩展性运行。这种新抽象层的结果是一套不断增长的 Chainlink 分散式服务，这些服务支持大量安全、功能丰富的智能合约应用程序，能够支持更广泛的用户和用例集。

![Hybrid smart contracts for enterprises](img/35cc68471b917ebe08415f70c814d240.png)

<figcaption id="caption-attachment-4663" class="wp-caption-text">Chainlink Decentralized Oracle Networks provide access to any off-chain data source or computation for smart contract applications.</figcaption>



要阅读 Chainlink 2.0 白皮书，请点击下面的按钮或访问[https://chain.link/whitepaper/](https://chain.link/whitepaper/)，其中也提供了该白皮书的设计目标和 Chainlink 网络未来的概述。

[Download the Chainlink 2.0 Whitepaper](https://research.chain.link/whitepaper-v2.pdf)

Chainlink 2.0 白皮书由世界一流的学术研究人员团队撰写，他们专门研究安全、密码学、分布式系统、博弈论、数学和各种其他计算机科学相关学科。该小组由前 RSA 首席科学家、现 Chainlink Labs 首席科学家 Ari Juels 领导，成员包括 Lorenz Breidenbach、Christian Cachin、Benedict Chan、Alex Coventry、Steve Ellis、Farinaz Koushanfar、Andrew Miller、Brendan Magauran、Daniel Moroz、Sergey Nazarov、Alexandru Topliceanu、Florian Tramèr 和张帆。

[https://www.youtube.com/embed/7Ow8uN1TmxA?feature=oembed](https://www.youtube.com/embed/7Ow8uN1TmxA?feature=oembed)

在这个研究小组中，白皮书的共同作者 Ari Juels、Lorenz Breidenbach、Andrew Miller 和 Sergey Nazarov 介绍了 Chainlink 2.0 的主要技术进步。

## 重新定义分散式 Oracle 网络的功能

最初的 Chainlink 白皮书开创了分散式 oracle 网络，通常被视为一种以安全可靠的方式将外部数据输入区块链的方式。Chainlink 2.0 白皮书为多个互操作的分散式 Oracle 网络(don)创建了一个框架，每个网络都由一组节点组成，这些节点可以双向传输数据，并使用各种共识协议执行分散式链外计算。与第 2 层技术类似，Chainlink DONs 锚定到现有的区块链，以便定期同步数据输出和离线计算的状态变化，并建立护栏，强制执行正确的 oracle 报告和仲裁离线 oracle 争议。

![Chainlink Decentralized Services](img/e2d1d22be0135fc7558884c7ebb875d7.png)

<figcaption id="caption-attachment-4668" class="wp-caption-text">Chainlink Decentralized Services enhance the capabilities of smart contracts across the broader blockchain ecosystem.</figcaption>



白皮书中描述的更高级的链外计算允许 d on 为智能合约提供通用的、区块链不可知的网关，不仅可以访问任何链外资源，还可以访问用于代码执行的链外计算环境，这些代码执行要么不能在区块链上执行，要么由于各种约束(如成本、速度、隐私和技术限制)而无法在链上执行。因此，Chainlink 网络中的 don 作为一种安全、灵活的全栈解决方案，用于创建混合智能契约，该契约依赖于现有的链上代码，并将其与关键的链外计算相结合。这些混合智能合约使分散的应用程序能够在可伸缩性和保密性方面实现重大升级，这两者是大规模采用区块链的关键。

*   **扩展** : DONs 将离线计算 oracle 结果和部分合同执行，同时定期与现有的区块链网络或第 2 层同步。这使得 Chainlink 分散式 Oracle 网络能够实现服务区块链、第 2 层网络甚至传统 Web 2.0 系统所需的低延迟和高吞吐量性能。
*   **机密性** : DONs 允许多种形式的机密性，例如链上和链下系统之间的机密性保持连接器，以及智能合同和 oracle 数据的机密计算。

## Chainlink DONs 将如何为 DeFi 和更广泛的智能契约经济提供动力

通过 DONs 带来的增强将使 Chainlink 支持各种支持下一代智能合同用例的分散式服务。此外，Chainlink 网络今天提供的 oracle 服务将通过 don 提供的优势得到进一步增强。这些高级分散式服务的简要初始列表包括:

*   **混合智能合同**无缝连接到所有必要的链外资源，同时保持更高的隐私级别，并受到您首选的区块链或第 2 层的保护。
*   **增强型 Chainlink 数据馈送**提供更高频率的更新、隐私保护查询和多区块链交付，所有这些都降低了成本，并为衍生协议和企业解决方案等 DeFi 应用提供了更加安全可靠的外部数据源。通过 OCR，Chainlink 数据馈送已经变得更加可扩展。
*   **增强型 Chainlink VRF** 具有增强的安全性、加密经济安全性和成本效益，可支持更安全的游戏、NFT 造币和任何其他需要端到端安全性的安全随机来源的应用。
*   **Chainlink Automation** 提供关键智能合同功能的分散和高度可靠的执行，如收获产量和触发清算，目前正在为生产做准备，并由顶级项目进行测试。
*   **chain link Fair Sequencing Services(FSS)**使用 DONs 在区块链上订购用户交易，以此作为一种手段来减轻前置、后置和其他相关攻击，以及其他类型的交易，如由矿工可提取价值(MEV)引起的 oracle 报告传输。
*   **Chainlink 分散身份认证**保护隐私的 oracle 协议以向后兼容的方式与现有系统进行互操作，以开辟新的用例，如基于链上信用的贷款。

以及由各种附加的 don 创建的更多附加的分散服务。

## 链式加密经济安全

![An image showing how super-linear staking in Chainlink 2.0 requires a successful attacker to have a budget quadratically greater in n than the combined deposits of all oracle nodes in a network.](img/c61de13e2b6f8ec6e78c50ef87c9ca3a.png)

<figcaption id="caption-attachment-1743" class="wp-caption-text">Super-linear staking in Chainlink 2.0 requires a successful attacker to have a budget quadratically greater in n than the combined deposits of all oracle nodes in a network.</figcaption>



Chainlink 2.0 白皮书介绍了超线性锁紧的概念，这是锁紧机制设计中的一项重要进步。超线性赌注要求攻击者拥有比所有 DON 节点的安全保证金总和更大的资源(特别是 Chainlink，二次方),才能成功。通过独特的集中警报系统和双层裁决系统，don 提供了更强的加密经济安全保证，可以战胜其他系统无法抵御的强大对手。

随着 Chainlink 生态系统的不断扩大，我们相信其对用户的吸引力以及作为区块链经济基础设施的重要性将加速各种良性循环，推动更多的链上数据，并使 don 能够为智能合同提供新的服务。这种价值增长源于规模经济(随着服务量的增加，每个用户的成本效率更高)和网络效应(随着用户更广泛地采用 don，网络效用增加)。如白皮书中所述，我们认为，由链式链桩机制的良性循环所推动的网络安全的增长是链式链网络在分散服务的链上经济中帮助实现更大增长模式的例证。

![An image showing how the Chainlink Network aims for a virtuous cycle of cryptoeconomic security in which additional user fees incentivize increased node security, which drives more data on-chain.](img/e1ab18c83ce1de975029a19558c88cd8.png)

<figcaption id="caption-attachment-1744" class="wp-caption-text">The Chainlink Network aims for a virtuous cycle of cryptoeconomic security in which additional user fees incentivize increased node security, which drives more data on-chain.</figcaption>



有关超线性赌注和其他正在开发的加密经济安全形式的更多信息，请参考白皮书的第 9 节。

## 下一步是什么

本白皮书是对 Chainlink 未来发展的长期、多年展望。Chainlink 网络的这一宏伟愿景将随着新的分散式服务的并行发布而逐步实施，因此我们可以正式分析这一系列 oracle 新功能的安全影响。我们相信，Chainlink 将使智能合约在其发展过程中实现下一次重大飞跃，由混合链上/链下架构提供动力。正如 Chainlink 的安全数据 Oracle 在整个 DeFi 生态系统中开启了创新一样，Chainlink 2.0 的扩展分散式 Oracle Networks 将使混合智能合约开发人员能够构建主流用户一直在等待的可扩展和隐私保护的分散式应用。

要加入关于 Chainlink 2.0 及其对整个社区的其他研究人员和工程师的影响的讨论，请访问智能合同研究论坛上的白皮书研究摘要。

[网站](https://chain.link/) | [文档](https://docs.chain.link/docs/getting-started) | [不和](https://discordapp.com/invite/aSK4zew) | [时事通讯](https://chn.lk/newsletter) | [推特](https://twitter.com/chainlink)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial)