# Chainlink Automation 开放测试版上线:智能合约开发的完全分散式服务

> 原文：<https://blog.chain.link/chainlink-automation-open-beta-is-live/>

我们很高兴地宣布 [Chainlink Automation 公开测试版](https://automation.chain.link/)现在面向初始用户、社区评论和反馈开放。

Chainlink Automation 为[智能合同](https://chain.link/education/smart-contracts)开发人员、分散式应用程序(dApps)和分散式自治组织(Dao)提供了一种高度可靠、分散且经济高效的方法来触发智能合同功能和定期合同维护，从而创建了前所未有的完全分散式 DevOps 功能。智能合约应用程序可以使用 Chainlink Automation 来加强关键链上功能的正常运行时间保证，并实现端到端的分散自动化，而无需依赖额外的信任层。结果是 [DeFi](https://chain.link/education/defi) 和更广泛的智能合约经济拥有更强大的基础设施来扩展和保障更高的用户价值。

Chainlink Automation 目前正在与初始用户进行公开测试，因此我们可以收集最终反馈，并根据用户需求继续改善分散服务的体验。要尝试 Chainlink Automation 开放测试版，请访问[https://Automation . chain . link](https://automation.chain.link/)。开发团队也可以选择直接在新的 OpenZeppelin Defender 平台中注册和管理 Chainlink Automation 作业，该平台是一个针对以太坊和 EVM 项目的安全运营套件，通过以下链接:【https://openzeppelin.com/defender/】T2

[Try Chainlink Automation Open Beta](https://automation.chain.link/)

如有任何反馈，请联系我们的团队[。如果你想从技术层面了解更多关于 Chainlink 自动化的知识，请访问 Chainlink 文档:](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=announcement)[https://docs . chain . link/docs/chain link-Automation/introduction/](https://docs.chain.link/docs/chainlink-automation/introduction/)。

Chainlink Automation 可以为智能合约执行各种计算操作、监控以及基于时间和事件的任务，例如:

*   在分散的交易所执行限价单
*   当储备增加时铸造代币
*   从金库中收获收益
*   重置弹性供应代币
*   触发自动交易策略
*   清算抵押不足的贷款
*   闲置一段时间后释放锁定的资产
*   低于最低阈值的充值代币余额

![Diagram showing how smart contracts use Chainlink Automation](img/b9a35f7767f92f42e0bc83f74fbd3ebd.png)

作为一种通过 Chainlink 网络提供的新的分散服务，DeFi 和其他混合智能合约可以使用 Chainlink Automation 作为各种智能合约操作的超可靠交易管理器，最初在以太坊上使用。由于 Chainlink 自动化网络利用的是经过时间考验和久经沙场的专业节点运营商，这些运营商目前为 [Chainlink 数据馈送](https://data.chain.link/)提供支持，目前已在 DeFi 范围内获得数十亿智能合同价值，因此用户可以获得强有力的活跃度保证，确保关键合同功能按预期运行。开发人员还可以消除手动或通过集中式系统执行维护操作所涉及的时间、资源和风险。

## Chainlink 自动化如何增强智能合同应用

智能合约是在区块链上确定性运行的代码片段。然而，智能合约有两个基本限制:1)它们与外部资源断开连接，限制了它们使用真实世界数据或利用链外计算作为增加链上功能的手段的能力，2)它们默认处于休眠状态，需要一些外部实体在执行链上功能和改变合约状态时唤醒它们。Chainlink 正在积极消除智能合约开发人员的第一个限制，通常称为 [oracle 问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)，方法是提供越来越多的高质量外部数据馈送和信任最小化的链外计算。Chainlink Automation 现在提供了一种方法来克服可靠地触发常规契约功能的第二个限制。

Chainlink Automation 通过发出触发智能合约逻辑在区块链上执行的链上事务来扮演唤醒智能合约的角色。Chainlink Automation 不同于 chain link[Oracle](https://chain.link/education/blockchain-oracles)。Chainlink oracles 获取外部数据或执行链外计算，然后将结果存储在区块链上，而 Chainlink Automation 让智能合约知道何时执行某个功能。在被维护唤醒后，智能合同经常会引用 oracle 报告作为其执行的一部分。Chainlink Automation 允许您定义触发函数执行的确切条件集。这可以基于时间(例如，美国东部时间每天下午 4 点)、事件(例如，体育赛事的结束)、计算(例如，贷款被确定为抵押不足)或任何组合。

在 DeFi 的早期，开发团队开始分散他们的 oracle 机制，以提高他们的智能联系人的端到端安全性和可靠性。Chainlink 自动化实现了类似的现象，使开发团队能够分散他们的自动化机制，以增强他们的智能契约触发器的安全性和可靠性。由于 Chainlink Automation 管理着关键的智能合约功能，这些功能通常对时间敏感并对用户资金负责，因此 Chainlink Automation 在保证及时执行这些功能以及消除手动运行自动化服务等中心故障点方面发挥着至关重要的作用。

![Screen shot of the Chainlink Automation app](img/678eae5a9b77c766f77efc32f24e79bc.png)

<figcaption id="caption-attachment-4630" class="wp-caption-text">The Chainlink Automation interface enables developers to easily add new upkeep jobs for triggering various smart contract functions.</figcaption>



为了更好地理解 Chainlink Automation 的作用，我们来看两个涉及 Aave 和 Synthetix 的不同用例示例:

### Aave

Aave 是一个分散的货币市场，用户提供抵押品来获得连锁贷款。由于 Aave 贷款被过度抵押(抵押价值/未偿贷款价值大于 100%)，使用 Chainlink Automation 清算抵押不足的贷款对于保持 Aave 贷款池的偿付能力和保护贷方的资本至关重要。

1.  Aave 会注册一个 Chainlink 自动化作业，以便在用户的贷款低于特定池的清算阈值(例如 150%)时触发其清算功能。
2.  Chainlink Automation 监控用户的离线贷款抵押情况，并在检测到抵押不足的贷款时调用 Aave 的清算功能。
3.  Aave 的智能合约参考 Chainlink 价格馈送来计算用户的抵押率，并验证他们是否抵押不足。
4.  Aave 的智能合约在用户的抵押率低于指定的清算阈值时清算用户，确保贷款池的持续偿付能力。

![Aave Chainlink Automation Liquidation](img/32618128fd5f1fcc4e3a15bb8d33a892.png)

### 合成的

Synthetix 是一个分散化的衍生品协议，用户可以在链上接触过度抵押的合成资产，并根据流动性池合约零滑动地交易它们。维护 Synthetix 需要多种维护功能，包括当价格达到预定义的上限和下限时，自动冻结 iSynths(通过 Chainlink 价格馈送反向跟踪资产价格)，为最终用户提供更有效的杠杆。

1.  Synthetix 会注册一个 Chainlink 自动化作业，以便在价格达到上限和下限时冻结 iSynths。
2.  Chainlink Automation 监控 iSynths 的离线价格，并在发现价格达到预定义的上限和下限时调用 Synthetix 的 freezerate 函数。
3.  Synthetix 智能合约引用 Chainlink 价格馈送来计算 iSynths 的值，并验证是否达到上限或下限。
4.  Synthetix 智能合约在达到价格上限和下限时冻结 iSynths，防止协议变得过度杠杆化，并保护流动性池合约中的利益相关者。

![Chainlink Automation Synthetix freezing iSynths example](img/0326ab2bdeae86ef68cb900cc4c80ef3.png)

## 为什么 Chainlink Automation 为开发团队提供了卓越的任务管理解决方案

Chainlink Automation 利用一个经过安全审查和历史验证的节点运营商分散网络，已经在 DeFi 中保护了数百亿的安全，并在 Chainlink 网络的现有高度可靠的加密经济学中利用 link。基于具有基于时间的自动故障转移的轮换作业框架来选择节点，以避免作业竞争导致的用户成本上升。Chainlink 自动化网络的架构为用户提供了几个独特的优势:

*   **高正常运行时间** — Chainlink Automation 由相同的高质量 Chainlink 节点运行，这些节点已经在 DeFi 的各种网络条件下保护了数百亿次 TVL。Chainlink 节点由专业的 DevOps 团队运营，这些团队在为现有的分散式 oracle 网络(如 price feeds)提供高可靠性方面拥有良好的声誉。
*   **低成本**—chain link 自动化网络具有多项气体优化功能，有助于降低运行维护任务的成本，以及一个旋转节点选择流程，以进一步降低和稳定智能合同开发运营的成本。
*   **分散执行** — Chainlink 利用分散的节点池实现更安全的合同自动化，节省团队时间并降低人工干预或集中式服务器带来的风险。
*   **透明信誉** — Chainlink 为用户提供了一个强大的信誉框架和一套链上监控工具，以独立验证节点的历史性能。
*   **信任最小化验证**–Chainlink Automation 网络允许合同在采取任何重大行动之前执行维护作业时验证呼叫数据，使 chain link Automation 适用于信任最小化 dApps。
*   **可扩展计算–**chain link Automation Network 可以为智能合约执行链外计算，允许开发人员以更低的成本构建更高级的 dApps。

通过将智能合同维护外包给 Chainlink Automation，开发团队可以扩展其分散应用程序的安全性和可靠性，以匹配他们代表用户负责保护的不断增长的 TVL。

## 我们需要您的反馈

我们正在将 Chainlink Automation 发布到公开测试版，以便社区可以参与验证关键功能、收集反馈以及根据您的需求改善开发人员体验的最后步骤。我们希望听到您对我们如何改进 Chainlink 自动化的意见，因此请[分享任何反馈](https://discordapp.com/invite/aSK4zew)。我们期待着支持整个生态系统的开发团队，并将 Chainlink Automation 转变为一个强大的链外服务，这将有助于推动新一代高效、安全的混合智能合同。

通过访问[https://Automation . chain . link](https://automation.chain.link/)或位于[https://docs . chain . link/docs/Chainlink-Automation/introduction/](https://docs.chain.link/docs/chainlink-automation/introduction/)的 chain link 文档，立即开始在公测版中使用 Chainlink Automation。您还可以直接在 OpenZeppelin Defender 平台中注册和管理 Chainlink 自动化作业。更多详情，请参考他们[最近的整合公告](https://blog.openzeppelin.com/developers-can-now-register-and-manage-chainlink-keeper-jobs-with-openzeppelin-defender/)。

[Try Chainlink Automation Open Beta](https://automation.chain.link/)

要了解更多关于 Chainlink 的信息，请访问 [chain.link](https://chain.link/) ，订阅 [Chainlink 简讯](https://chn.lk/newsletter)，并在 Twitter 上关注 [@chainlink](http://www.twitter.com/chainlink) 。