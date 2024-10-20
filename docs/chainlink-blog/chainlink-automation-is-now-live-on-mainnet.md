# Chainlink Automation 现在在 Mainnet 上运行，为 dApps 带来了安全、低成本的链外计算

> 原文：<https://blog.chain.link/chainlink-automation-is-now-live-on-mainnet/>

一旦项目可以将他们的神谕外包给像[chain link Price Feeds](https://chain.link/solutions/defi)这样的分散解决方案，创新就开始了。开发人员不再需要构建核心后端基础设施，将他们的注意力完全转移到创造新颖的 DeFi 产品上。与 oracles 类似， [Chainlink Automation](https://chain.link/automation) 通过为开发人员提供安全可靠的链外计算服务，加速了 [混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/) 的创新。当预定义的条件发生时，开发人员无需执行手动流程、依赖集中式服务或实施深度协议更改来自动化链上功能，他们只需将作业外包给 Chainlink 自动化节点。

[https://www.youtube.com/embed/xL96sTwQ5Ho?feature=oembed](https://www.youtube.com/embed/xL96sTwQ5Ho?feature=oembed)

在成功推出 [测试版](https://blog.chain.link/chainlink-keepers-open-beta-is-live/) 后，其中包括由一组初始用户进行的现场测试，我们很兴奋地宣布[chain link Automation](https://chain.link/automation)现已在以太坊主网上直播，并向公众完全开放。任何个人开发人员、分散式应用程序和 DAO 现在都可以利用 Chainlink Automation 作为分散式链外计算层来可靠地触发关键智能合约功能，并使用自定义参数将高级实用程序引入其 dApp。

Chainlink Automation 可代表混合智能合约执行各种开发运维服务和链外计算，包括:

*   在分散交易所执行限价单
*   储备增加时铸造代币
*   从金库收获产量
*   重置弹性供应代币
*   重新平衡链上交易和产量养殖策略
*   清算抵押不足的贷款
*   闲置一段时间后释放锁定的资产
*   充值低于最小阈值的代币余额
*   还有更多的可能性有待发现

如果你今天想在你的应用中使用 Chainlink Automation，请使用以下链接注册:[【https://automation.chain.link/】](https://automation.chain.link/)。如果您想与专家讨论集成， [请点击这里](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog) 。

开发团队还可以直接在 OpenZeppelin Defender 平台中注册和管理 Chainlink 自动化作业，该平台是一个针对以太坊和 EVM 项目的安全运营套件:[【https://docs.openzeppelin.com/defender/guide-chainlink】](https://docs.openzeppelin.com/defender/guide-chainlink)。

## Chainlink Automation:智能合同的成熟基础设施

[Chainlink 2.0 白皮书](https://research.chain.link/whitepaper-v2.pdf) 概述了 chain link 网络的宏伟愿景，其中分散式 Oracle 网络(don)除了在链上和链外环境之间进行数据传输之外，还执行分散式链外计算。除了 chain link[【VRF】](https://chain.link/solutions/chainlink-vrf)和[OCR](https://blog.chain.link/off-chain-reporting-live-on-mainnet/)， [Chainlink Automation](https://chain.link/automation) 标志着混合智能合约开发者可以通过 Chainlink DONs 获得的一系列链外计算服务的重大升级，特别是基于预定义条件的自动化智能合约功能。

智能合约是在区块链上运行的确定性程序，它使用链上交易形式的输入来触发其嵌入式逻辑并生成输出。开发人员使用自动化作业来创建可验证的基于事件的输入，其中只有在满足特定条件的情况下，输入才会在链上广播以触发智能合约。一些自动化作业很简单，比如在每周的特定时间调用一次收益率采集函数，而其他自动化作业则更高级，比如在用户的贷款抵押不足时调用清算函数。这些自动化作业中的每一个都涉及运行链外计算，以在触发链上功能之前验证条件是否得到满足。

Chainlink Automation 使开发人员能够根据可验证的条件输入，为智能合同管理打开广阔且尚未开发的设计空间。Chainlink Automation 提供了一个高度可编程的框架，用于使用链外计算来设计高级自动化作业，还提供了一个分散的可靠节点网络，用于外包自动化作业的执行。

Chainlink Automation 为开发人员提供了分散的链外计算，这些计算经过了优化，提供了重要的功能，最值得注意的是:

*   **最大可靠性** —Chainlink Automation 由相同的专业开发人员运行，他们已经为chain Link Price Feeds获得了数百亿美元的价值，并在由自动故障转移支持的分散架构内运行，以确保无单点故障的高可靠性。
*   **链上验证** —Chainlink Automation 由一套强大的链上监控工具支持，并根据其链下计算生成 EVM 调用数据，使用户能够在执行关键的链上工作之前评估自动化节点的输入并验证条件。
*   **低成本** —Chainlink Automation 在链外执行复杂的计算，并利用旋转节点选择框架来防止天然气价格拍卖战，从而降低和稳定成本。

## 为不断发展的 Chainlink 生态系统带来自动化

目前有数百名用户依赖或积极集成 Chainlink 分散式服务，如[Price Feeds](https://docs.chain.link/docs/using-chainlink-reference-contracts/)[VRF](https://docs.chain.link/docs/chainlink-vrf/)和[Proof Reserve](https://blog.chain.link/chainlink-proof-of-reserve-bringing-transparency-to-defi-collateral/)，Chainlink Automation 为 Chainlink 生态系统带来了全新的功能，使每个项目能够构建更高级的混合智能合同应用程序，为其用户创造附加值。

下面是 Chainlink 项目已经使用或正在使用的几个用例，展示了自动化为 chain link 生态系统带来的许多独特功能。

### Aave

Aave 是一个 DeFi 流动性协议，它使用户能够提供和借用加密资产，并从提供给协议的资产中获得收益。Chainlink Automation 将通过持续计算抵押并检查抵押率是否低于池的预定义清算阈值(如 150%)来监控用户的离线借款交易的健康状况。如果发现抵押不足，Chainlink Automation 将调用 Aave 协议的清算功能，确保借款人的头寸保持偿付能力，即使在市场剧烈波动和网络拥塞的时候。当清算人清算经济上不可行的头寸时，这变得尤其重要，否则可能会导致抵押不足。每个自动化节点在经济上被激励来执行所有注册的维护，确保所有位置被迅速清算，即使它们不盈利。

![Aave Chainlink Automation Liquidation](img/32618128fd5f1fcc4e3a15bb8d33a892.png)

<figcaption id="caption-attachment-4658" class="wp-caption-text">Aave will use Chainlink Automation to trigger the liquidation of undercollateralized loans.</figcaption>



### 共池

PoolTogether 是一个用于无损失有奖游戏的开源和去中心化协议。用户将计息代币存入奖池，在预定义的时间段结束时，奖池赚取的所有利息将奖励给随机赢家。Chainlink Automation 用于持续监控池，并调用 PoolTogether 的智能合同来通知他们游戏何时开始和结束，从而实现全自动无损失奖金游戏和支付。

![Chainlink Automation for PoolTogether's no-loss prize game](img/28f172d0821ffa871231cf41fe08d12a.png)

### 合成酶

Synthetix 是一个分散化的衍生品协议，用户可以获得过度抵押的合成资产的链上风险敞口，并根据流动性池合同以零滑动率进行交易。Synthetix 将使用 Chainlink Automation 为他们的[](https://docs.synthetix.io/contracts/source/contracts/FeePool/)收费期关闭服务。Chainlink Automation 将在费用周期结束后调用此函数，以自动分配 synthetix.exchange 费用和赌注奖励。

![Diagram showing how Synthetix uses Chainlink Automation](img/24a8fd2a93b1e91f5360df56224f9d44.png)

### Chainlink 不断增长的自动化生态系统

*   **Bancor:** 基于自动做市商的分散式交易所，支持单边流动性池和非永久性损失保护。Bancor 计划将自动化集成为即将到来的 V3 更新的一部分，以进一步简化最终用户的 DeFi 体验，并为其 AMM 协议添加高级实用程序。
*   **Alchemix:** 一种自我偿还的借贷协议，将用户抵押品存入 Yearn 的收益率汇总金库，产生的利息用于支付用户贷款。Alchemix 计划使用自动化来触发每天的保险库收集和保险库刷新，从而实现无缝用户债务偿还和新存款的注入。
*   **巴恩布里奇** :一种 DeFi 风险标记化协议，为对冲收益率敏感性和市场价格波动创造衍生品。BarnBridge 在其智能敞口产品中利用 Chainlink Automation 来监控链外标记化头寸的敞口比率，并在需要重新平衡保险库时调用 BarnBridge 的链上合约。
*   **更多:** 各种 DeFi 应用计划或已经使用 chain link Automation in-production 来安全地触发智能合约功能，包括 Visor Finance、ParaSwap、yAxis、Base Protocol、EthSign、Nifty Royal、B Protocol、improval ax、Flurry Finance、DeFi Network、Finance.vote 以及更多即将推出的功能。

## 如何在应用程序中使用 Chainlink Automation

![Gif showing how to use the Chainlink Automation Job Scheduler](img/e73fbb19098c85be1a87ce8439430a03.png)

Chainlink Automation 支持关于如何在链上执行和验证链外计算的各种配置。开发人员的一些设计考虑包括:

### 触发条件验证

当满足触发条件时，尽管 Chainlink Automation 节点负责调用链上函数，但开发人员可以定制他们的智能合约如何在执行合约逻辑之前处理 Chainlink Automation 事务的验证。

*   **满足条件时触发，无需验证**—当满足预定义的条件时，必须执行状态更改，但是当不满足条件时执行状态更改不会出现任何问题，例如在一天结束前从金库中收获收益，或者在达到阈值最小值之前充满状态通道令牌余额。在这种情况下，智能合约中的条件验证不是必需的，但仍可能有助于最小化为用户提供很少价值的维护呼叫费用。
*   **仅当条件满足时触发**—当条件满足时必须执行状态更改，但当条件不满足时执行此类操作是不合适的，例如清算抵押不足的贷款或从锁定合同中授予令牌。在这种情况下，当调用 performUpkeep 函数时，必须在智能合约中进行条件验证，例如检查链上的价格参考合约或块号，以确保状态更改在执行前有效。

### 离线执行昂贵的计算以限制在线成本

开发人员可以定制的另一个参数是通过 Chainlink Automation 最大化链外计算，作为最小化链上成本的一种手段，特别是为了减少链上函数调用的必要输入。

一种设计模式涉及对大量地址和状态执行链外条件检查，例如，查看哪些地址有资格空投，然后对满足契约条件的子集执行链上状态更改。开发人员可以在调用基于 check maintenance 调用结果的链上函数时传递适当的输入。理想情况下，条件验证仍然由智能合同在链上执行，但消耗的气体被最小化，因为维护仅传递相关输入的子集进行验证。

### 在同一个智能合约上设置多个维持费

还有一些架构模式使用智能合约来处理多种维护，帮助开发人员管理链上成本，并为更高级的 dApps 构建定制触发器，如在执行前进行多种不同的条件验证。比如:

*   **管理无界保养**—通过为 Chainlink 自动化检查和执行创建一个范围界限，限制合同链上执行的计算复杂性，最大限度地减少不必要的链上计算。这允许开发人员将链上执行保持在一组预定义的活动中，从而产生一个可预测的事务执行成本上限。
*   **配置 check maintenance 函数**——设计智能契约逻辑，可以基于 Chainlink 自动化调用数据执行不同的代码路径，在单个契约函数中实现多种不同的执行。这可以基于开发人员独特的用例需求以创造性的方式使用，例如，如果条件满足，则触发特定农场的产量收获，或者如果条件不满足，则触发特定位置的再投资。

对于想要了解如何使用 Chainlink Automation 开始构建的详细信息的开发人员，请阅读以下文档:[https://docs . chain . link/docs/chain link-Automation/introduction/](https://docs.chain.link/docs/chainlink-automation/introduction/)。

## 由安全离链计算驱动的高级混合智能合约的未来

Chainlink Automation 是一套更先进的分散服务的下一部分，可供希望构建下一代混合智能合同的开发人员使用，为用户释放更多价值。开发人员不仅可以利用 Chainlink [oracle](https://chain.link/education/blockchain-oracles) 基础设施安全连接到外部数据源，还可以利用 Chainlink Automation 基于预定义的事件触发链上功能，所有这些都以高度安全、可靠、低成本和链上可验证的方式实现。

最终，这是使 Web 3.0 开发像 Web 2.0 开发一样复杂和敏捷的又一步，将可证明可靠的数据和安全的链外计算服务带到开发人员的指尖。访问经过时间考验且易于集成的 don 使开发人员能够专注于核心协议和产品开发，从而在智能合约经济中带来更多创新，并在更广阔的世界中产生更大的社会影响。Chainlink Automation 只是更大的 Chainlink 2.0 愿景的开始，该愿景旨在提供一整套离线计算服务，以扩大和增强开发人员使用区块链构建的内容。

![Chainlink Automation and Decentralized Oracle Networks (DONs)](img/b425f4964ce7e46fd15d82a2f0f1eba2.png)

<figcaption id="caption-attachment-4662" class="wp-caption-text">Chainlink Automation is only the beginning of how Decentralized Oracle Networks (DONs) will evolve to provide a wide range of off-chain computations and external services to smart contracts.</figcaption>



访问[【https://chain.link/automation】](https://chain.link/automation)了解更多关于 Chainlink 自动化的信息，或阅读 Chainlink 文档，网址为[【https://docs . chain . link/docs/chain link-Automation/introduction/](https://docs.chain.link/docs/chainlink-automation/introduction/)。 我们鼓励开发者 分享任何关于[不和谐](https://discordapp.com/invite/aSK4zew) 的反馈，这样我们就可以扩展 的 Chainlink 自动化，使它更加可靠、可用、功能更加丰富。

[Integrate Chainlink Automation](https://automation.chain.link)[Talk to an expert](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog)