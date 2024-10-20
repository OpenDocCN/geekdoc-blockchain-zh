# 使用 Chainlink 自动化作业调度程序触发基于时间的智能合同功能

> 原文：<https://blog.chain.link/chainlink-automation-job-scheduler/>

[智能合约](https://chain.link/education/smart-contracts) 是在区块链上运行的确定性程序，当满足某些预定义的条件时执行。智能合约的最初用例主要涉及发行基于区块链的令牌，开发人员后来利用[Oracle networks](https://chain.link/education/blockchain-oracles)创建了 [混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/) ，它们使用外部数据和计算来创建更复杂的应用程序。

对于希望构建高级智能合约应用的开发人员来说，外部计算基础设施的一个关键部分是“维护”，当各种预定义的条件发生时，它会触发链上交易，使开发人员能够自动执行关键的智能合约功能。

在本帖中，我们将探索 [Chainlink 自动化作业调度器](https://docs.chain.link/docs/chainlink-automation/job-scheduler/)——一种新的用户界面，使智能合同开发人员能够快速、安全、可靠地在几秒钟内调度基于时间的维护作业。如果您想立即开始使用自动化作业调度程序，请访问 [Chainlink 自动化应用](https://automation.chain.link)，并注册一个新的基于时间的维护 。

## 智能合约不能自主执行

智能合约的一个经常被忽视的特点是它们不能自己执行——它们需要一个外部实体来触发其内部逻辑。

为了克服这个问题，开发人员可以手动触发他们的合同，或者构建集中的脚本来代表他们触发合同。然而，这些方法存在集中化风险和效率瓶颈，引入了智能合约安全漏洞，并且占用了宝贵的开发时间和资源，这些时间和资源原本可以用于推进协议。

![A diagram showing how unreliable keeper systems can compromise smart contract security](img/35abedaf6218a3dfd0f853386caff320.png)

<figcaption id="caption-attachment-4015" class="wp-caption-text">Creating and maintaining centralized infrastructure such as cron jobs for smart contract automation introduces significant security risks.</figcaption>



此外，希望自动执行基于时间的智能合约功能的开发人员通常必须使他们的合约与自动化服务兼容，重新部署合约和迁移用户，执行耗费大量时间的检查，并单独注册每个自动化作业。

## 使用 Chainlink 自动化作业调度程序触发基于时间的智能合同任务

[chain link Automation](https://chain.link/automation)使开发人员能够以一种分散的、经济高效的、高度安全的方式自动化他们的智能合约功能。

开发人员可以为 Chainlink Automation 指定预定义的条件，以持续检查，当这些条件得到满足时，节点会发出一个链上事务，触发智能合约自动执行。

Chainlink Automation Job Scheduler 是一款全新的无代码用户界面，允许开发人员在几秒钟内 **在 chain link Automation 网络上安排所有基于时间的智能合同维护作业。** 使用自动化作业调度程序，开发人员可以使用支持[chain link Automation](https://automation.chain.link/)和[chain link Data Feeds](https://chain.link/data-feeds)的相同分散式 oracle 网络，轻松可靠地执行基于时间或调度的智能合同自动化作业。

通过使用 chain link Automation Job Scheduler 以分散的方式轻松触发基于时间的可靠性功能，开发人员可以节省关键的开发时间，分散他们的协议或 dApp，并增加安全性和正常运行时间。开发人员可以使用自动化作业调度程序作为现成的解决方案，根据时间间隔执行分散的智能合同，而不是花费宝贵的资源来构建内部基础设施。

chain link 自动化作业调度程序的主要优势包括:

*   **易于使用的**—使用易于使用的无代码用户界面，在几秒钟内自动执行您的智能合同。
*   **分散化**—通过利用分散的节点网络来执行维护作业，自动化作业调度程序为其自动化的合同提供了更高的安全性、可靠性和正常运行时间保证。
*   **安全性** —Chainlink 自动化节点自己签署链上交易，从而实现智能合同执行，而无需在 Cron 脚本中暴露私钥。
*   **气体效率**—自动化固体调度程序消除了对气体密集型时间检查的需要。

## 如何入门

![Gif showing how to use the Chainlink Automation Job Sch](img/e73fbb19098c85be1a87ce8439430a03.png)

首先导航到 [Chainlink 自动化应用](https://automation.chain.link) 并选择“注册新保养”。

输入包含您想要自动化的功能的目标合同地址。

![Screenshot showing UI to register a new Upkeep](img/0c129bd514bf7f18b443399c1dcd5744.png)

选择您希望调用的功能，并根据需要指定任何功能输入。

![Contract call](img/de438cee9e82f814b342aa055c307cb0.png)

指定您的首选时间表

![Specify time schedule](img/deb37981e43e6646d24f001b26f6d01c.png)

在指定保养名称、[气体极限](https://docs.chain.link/docs/chainlink-keepers/faqs/#how-do-i-determine-the-gas-limit-for-my-upkeep)和开始链路平衡后，在 Chainlink Automation 网络上注册您的保养。

![Screenshot showing Upkeep details](img/067ea3e388c6b0daada748b4fb3157aa.png)

最后，确认交易以部署 CRON 工作合同，并将您的基于时间的维护注册到 Chainlink Automation 网络。在自动化注册表中将您的合同注册为维护费后，自动化网络会监控维护费并执行您的功能。

![Deploy CRON job contract](img/d0ad0626292c120782b05910a150acb2.png)

从仪表板查看和管理您的保养。

![Screenshot showing Upkeep test UI](img/7ad521ddb076d5406c00ea71d65f058e.png)

你就大功告成了！使用 Chainlink Automation，开始执行任何智能合同功能都是如此简单。

## Chainlink 自动化作业调度器示例用例

Chainlink Automation 已经在授权 Solidity 开发者在 [【雪崩】](https://medium.com/avalancheavax/chainlink-keepers-and-chainlink-vrf-go-live-on-avalanche-3ebee050ebef)[【BNB 链】](https://www.binance.org/en/blog/chainlink-keepers-now-live-on-binance-smart-chain-for-securely-automating-smart-contract-devops/)[以太坊](https://blog.chain.link/chainlink-keepers-is-now-live-on-mainnet/)[Fantom](https://fantom.foundation/blog/chainlink-keepers-and-vrf-now-live-on-fantom/)和[Polygon](https://blog.polygon.technology/chainlink-keepers-now-live-on-polygon-mainnet-to-automate-smart-contract-devops/)上构建全功能的 dApps，这些 dApps 都是去中心化的、完全自动化的端到端应用。如果你正在寻找由 Chainlink Automation 支持的大量智能合同自动化用例的深度挖掘，请阅读 [这篇文章](https://blog.chain.link/smart-contract-automation-use-cases-powered-by-chainlink-keepers/) 。

以下是 chain link Automation Job Scheduler 解锁的许多基于时间的智能合同自动化用例的几个例子。

### 开始和停止游戏回合

预测市场和无损失储蓄游戏等智能合约应用程序具有需要在特定时间间隔触发的功能，例如开始、停止或暂停游戏或回合。

这些 dApps 需要一个自动化网络来监控时间的流逝，并在特定的时间间隔触发特定的事件。自动化作业调度程序可以可靠地自动调用应用程序智能合约，以触发不同回合或游戏阶段的开始或结束。

### 奖励支出

许多 DeFi 和[](https://chain.link/education/nfts)平台旨在通过财务激励吸引流动性并鼓励用户参与。定期向一组特定用户分发奖励的协议可以使用 chain link Automation Job Scheduler 以可靠和分散的方式自动执行奖励分发过程。

作业调度程序有助于确保奖励以预定义的时间间隔分发给用户，无需任何手动输入，从而为开发人员团队创造顺畅的用户体验并简化智能合同管理。

### 重置令牌

弹性供给令牌通过一种称为重定基础的机制定期调整其未偿供给，以实现预期功能——通常是维持一个有目标指数的挂钩。

将弹性供应令牌的重置机制自动化是一项智能的合同维护任务，必须定期执行以实现所需的 peg。在这里，Chainlink Automation 作业调度程序可以定期调用智能合约，并以高度可靠和分散的方式启动弹性供应令牌的重置机制。

### 动态 NFTs

动态 NFT 是[](https://chain.link/education/nfts)基于外部数据进化并获得新属性的不可替代令牌(NFT)。NFT 项目可以通过使用 [Chainlink 数据馈送](https://data.chain.link/) 或使用定制的 [外部适配器](https://blog.chain.link/build-and-use-external-adapters/) 连接到任何外部 API，用真实世界的数据更新它们的 NFT。

作为基于时间的智能合同管理任务的可靠分散调度程序，自动化作业调度程序是根据预定义的基于时间的条件升级 NFTs 的完美工具。在此了解更多 [链环工程教程](https://www.youtube.com/watch?v=E7Rm1LUKhj4) 。

## 总结

chain link Automation Job Scheduler 使开发人员能够以分散的方式安全、轻松地触发基于时间的智能合约功能。开发人员可以使用 Solidity Scheduler 来取代集中式 Cron 作业，增强他们的协议的安全性和正常运行时间，并在他们的操作中释放开发能力。

如果您是一名开发人员，并且希望快速将您的应用程序与[chain link Automation](https://automation.chain.link)集成，请访问 [开发人员文档](https://docs.chain.link/docs/chainlink-automation/introduction/) 并加入[Discord](https://discordapp.com/invite/aSK4zew)中的技术讨论。如果您想安排一次电话会议来更深入地讨论整合事宜，请点击 [这里的](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=announcement) 。

要了解更多，请访问[chain . link](https://chain.link/)，订阅 [Chainlink 简讯](https://chn.lk/newsletter) ，并关注 Chainlink 上的[Twitter](https://twitter.com/chainlink)，[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)，以及[Reddit](https://www.reddit.com/r/Chainlink/)。

## 关于这个话题的更多信息

*   [如何入门 Chainlink 自动化](https://blog.chain.link/smart-contract-automation/)
*   [由 Chainlink 自动化解锁的用例](https://blog.chain.link/smart-contract-automation-use-cases-powered-by-chainlink-keepers/)
*   [Chainlink 自动化现已上线以太坊 Mainnet](https://blog.chain.link/chainlink-keepers-is-now-live-on-mainnet/)
*   [Oracle 计算:将 Oracle 的用途扩展到数据交付和链外计算](https://blog.chain.link/what-is-oracle-computation/)