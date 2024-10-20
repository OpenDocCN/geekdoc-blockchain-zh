# 什么是 Chainlink？初学者指南

> 原文：<https://blog.chain.link/what-is-chainlink/>

Chainlink 是一个分散的 oracles 网络，它使智能合约能够安全地与区块链网络之外的真实世界数据和服务进行交互。通过 Chainlink，目前为现代经济提供动力的传统系统可以连接到新兴的区块链行业，从而在业务和社会流程中实现更高的安全性、效率和透明度。

[https://www.youtube.com/embed/tIUHQ7sDoaU?feature=oembed](https://www.youtube.com/embed/tIUHQ7sDoaU?feature=oembed)

随着加密货币和区块链技术获得主流关注，以及 Chainlink 成为许多区块链应用程序的关键组件，越来越多的人开始进入该行业，并提出一个基本问题:Chainlink 是什么？

为了帮助那些刚刚接触区块链、[智能合同](https://chain.link/education/smart-contracts)和[甲骨文](https://chain.link/education/blockchain-oracles)的人，我们创建了一个简单的概述来展示 Chainlink 甲骨文网络的价值，以及它如何使区块链技术发挥其全部潜力。本指南通过回答三个关键问题提供了关于 Chainlink 的背景信息:

*   区块链和智能合约的潜在价值主张是什么？
*   为什么 Chainlink 必须帮助解决智能合约的固有限制？
*   Chainlink 的解决方案如何释放智能合约的全部潜力？

## 区块链如何消除交易对手风险

为了充分理解 Chainlink 的重要性，首先理解区块链和智能合约的潜在价值至关重要。一般来说，[区块链](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/)是一个分散的计算机网络，它执行计算并将数据存储在一个共享的账本中。区块链与传统的集中式计算机系统的不同之处在于:

*   没有一个人或团体能控制它。
*   世界上的每个人都有平等的权利向它发送命令。
*   运行在其上的应用程序和存储在其中的数据不能被篡改或删除。
*   一段时间内处理的所有交易都记录在一个不断增长的分类账中。
*   交易通过本地加密货币支付。

区块链通过让成千上万的计算机运行相同的软件，处理相同的交易，存储相同的数据，并一致地相互交叉检查，以达成关于什么是有效的网络的共识，来实现这些属性。所有这些网络运作都有金钱激励作为后盾，强化诚实的行为和共识。通过在一个由金融激励的参与者组成的大型分散网络中冗余地验证和存储交易，区块链使得操纵共享账本变得极其昂贵和不切实际。

因此，区块链是非常安全和可靠的系统，用于为涉及两个或多个独立方的进程执行计算和存储数据。区块链的根本好处在于，它们降低了交易对手风险——合约中的另一方不遵守合约条款的风险。比如有人要和一个陌生人做数字交易，如何决定谁先送钱，是否有足够的资金，资金不能花两次(俗称双花问题)？传统上，用户会雇用第三方，如支付处理器或票据交换所，以促进交易或仲裁纠纷。然而，区块链是一个更可靠、防篡改、公正的交易结算系统。用户知道，当他们向区块链发送交易时，交易将完全按照指示执行。



![Centralized transaction vs. decentralized transaction](img/129a16766e10ead1df7e4add72a8da2c.png)

<figcaption id="caption-attachment-3030" class="wp-caption-text">与银行不同，区块链在双方之间转移资金，而不需要保管。</figcaption>





区块链的去中心化架构是比特币和其他加密货币成为如此强大的货币形式的原因:用户可以相信没有中央管理者会夸大供应量(上限为 2100 万 BTC)，显示谁拥有比特币的基础比特币区块链已经得到了全球数千台电脑的验证。此外，区块链的分散设计允许用户直接交换价值，“点对点”，消除了可以抽取费用和审查交易的监管中间人，最终允许用户保留对其资产和数据的所有权。

然而，区块链可以支持许多用例，而不仅仅是简单地移动和在账本上记录资金。一些高度可编程的区块链允许更具表现力的命令集，特别是通过在网络上运行应用程序，这些应用程序基于特定的预定义事件触发动作(如果 x 事件发生，则执行 y 动作)。例如，如果明天 777 航班取消，支付 77 美元的保险金；如果没有，那就不要付款。这些区块链应用程序可以处理更广泛的逻辑，被称为“[智能合约](https://chain.link/education/smart-contracts)”，自以太坊在 2015 年首次大规模推出以来，一直是区块链周围许多开发的主题。

![](img/0061c8dc47c8cdb6b0609975ef746bd5.png)

## 问题:智能合约可能会再次引入交易对手风险

问题在于，智能合同需要数据(如航班起飞信息)来执行命令，但它需要数字化和自动化现实世界[协议](https://blog.chain.link/brand-based-vs-math-based-agreements/)的大部分数据并不存储在区块链上。智能合同也不能获取[外部数据](https://blog.chain.link/understanding-how-data-and-apis-power-next-generation-economies/)，因为区块链就像黑匣子，没有与外部世界连接的内置能力。这意味着资产价格、[体育比分、](https://blog.chain.link/bringing-sports-markets-to-blockchains-using-chainlink/)、[物联网(IoT)](https://blog.chain.link/how-chainlink-enables-blockchain-iot-integrations/) 传感器、网络数据、企业系统和众多其他真实世界数据集在区块链上根本不可用，这严重限制了开发人员可以创建的智能合同的类型。一个人如何在没有飞行数据的情况下制定飞行保险协议？

将数据有效输入区块链的唯一方法是通过一个名为“oracle”的软件组件将数据输入区块链。接下来的挑战是，如何设计一种具有与基础区块链相同的安全性和可靠性属性的 oracle 机制，以便保留智能合约的基础价值主张，例如没有交易对手风险的极端可靠性。如果单个集中式 oracle 负责输入用于触发智能合约的数据，则该 oracle 完全控制智能合约的结果。这引入了一个被称为[甲骨文问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)的严重故障点，将整个智能合同置于风险之中。



![A centralized oracle introduces a single point of failure in the delivery of data to the blockchain.](img/7430dc21a3d66a2c5f70e132695078f7.png)

<figcaption id="caption-attachment-814" class="wp-caption-text">集中式 oracle 在向区块链传送数据时引入了单点故障。</figcaption>





## 解决方案:链式分散 Oracle 网络

Chainlink 是一个分散式 oracle 网络，开发该网络是为了让 smart contracts 以高度安全和可靠的方式在区块链系统和外部系统之间自动传输数据。它使用类似于区块链的模型，其中有一个由独立实体(oracles)组成的分散式网络，这些实体共同从多个来源检索数据、聚合数据，并将经过验证的单一数据点交付给智能合约以触发其执行，从而消除任何集中的故障点。

例如，Chainlink 通过 [ETH/USD 价格馈送](https://feeds.chain.link/eth-usd)向区块链提供以太坊的本地加密货币 ETH 的美元价格，该价格馈送使用大量独立的 oracle 节点和数据源来获取和提供价格数据(如下图所示)。然后，区块链应用程序可以使用 ETH/USD 价格 oracle 来获取 ETH 的当前价格，作为获得贷款或解决对未来 ETH 价格的预测的抵押品。



![Screenshot of ETH-USD Price Feed page](img/6997932fafa47061b59634ea0e84718a.png)

<figcaption id="caption-attachment-2134" class="wp-caption-text">ETH/USD chain link Price Feed 汇总了来自众多独立 oracle 节点运营商的价格数据。</figcaption>





Chainlink 还提供了超越分散的多层安全性，以确保用户可以信任 oracle 网络:

*   **通用架构**–chain link 是一个用于构建和运行 oracle 网络的灵活框架，这意味着用户可以构建和/或连接到定制的 oracle 网络，而无需依赖其他 oracle 网络。



![Chainlink Network diagram](img/86a439e4817a10983b6bc168fb560ef0.png)

<figcaption id="caption-attachment-2093" class="wp-caption-text">链式网络、oracle 网络、链式节点和节点操作符的基本区别。</figcaption>



<figcaption></figcaption>



*   **数据签名**–chain link oracle 使用唯一的加密签名对他们在链上输入的数据进行签名，允许用户证明数据来自特定的 Oracle 节点。
*   **高质量数据**–**chain link 为智能合约提供来自任何外部系统(包括高级数据提供商)的数据，并允许智能合约向其他系统发送命令，例如在传统支付轨道上进行支付。**
***   **区块链不可知**–chain link 可以在任何区块链上本地运行，不依赖于其他区块链，这意味着它可以支持公共区块链、企业区块链等。**

 **

![Chainlink connects any blockchain to any input and output](img/9b26e20d587b285f86e1127844d58293.png)

<figcaption id="caption-attachment-717" class="wp-caption-text">Chainlink 将任何区块链上的智能合约连接到任何输入和输出。</figcaption>





*   **服务水平协议**–chain link 最终将允许用户定义链上智能合同中请求的 oracle 作业的条款，这可能需要 oracle 节点支付保证金，只有当它们按照预先商定的条款执行时(例如，数据按时交付)，保证金才会返还给节点。
*   **信誉系统**–chain link Oracle 的历史性能通过链上签名数据公开，允许用户根据历史性能指标选择 Oracle，如平均响应时间、完成率、平均保证金等。节点运营商还可以选择提供其他数据，如他们的身份、地理位置和第三方认证。



![A diagram showing Chainlayer's node statistics on market.link](img/2488d083b5b9a66a9c7997acb055e87b.png)

<figcaption id="caption-attachment-1480" class="wp-caption-text">Chainlink Market 允许节点列出有关其运营的关键功能，并使用户能够通过这些功能以及链上数据指标进行过滤。</figcaption>





*   **可选功能**–chain link 还在为 oracle 和数据隐私、高级 oracle 计算等功能开发额外的安全方法。

## 链环的使用案例

通过提供与区块链相当的强大的安全性和可靠性保证，使用 Chainlink oracles 创建了更高级的智能合同。虽然我们已经概述了由 Chainlink 支持的 [77 个智能合约用例，其中一些主要用例包括:](https://blog.chain.link/smart-contract-use-cases/)

### 分散融资

许多传统金融产品，如贷款、支付、衍生品、资产净值等，正在区块链上构建，使用智能合约来提高安全性和透明度，并降低准入门槛。这些 [DeFi](https://chain.link/education/defi) 应用程序使用 Chainlink 为资产定价、获取利率、验证抵押等，使这些产品能够执行以公平市价发放贷款、自动发放股息以及结算期权合同等功能。

### 保险

智能合同也被用来在区块链创建参数保险合同。Chainlink 目前在生产中用于向 Arbol 作物保险市场提供天气数据，使世界各地的农民只需通过互联网连接即可获得参数作物保险，该保险根据降雨量、温度或政策设定的其他评估者以公平和及时的方式结算(例如，如果今年降雨量超过 x 量，支付 y 结算)。

### 赌博

开发商也开始在区块链推出基于合同的智能游戏应用程序，这些应用程序通常包含不可替代的代币(NFT)作为稀缺的数字收藏品。许多区块链游戏的一个关键组成部分是随机性的来源，以产生随机的游戏场景或确定幸运的获奖者。Chainlink 提供了一个名为 VRF 的随机性解决方案，它可以生成随机性，并以一种用户可以证明它是公平和公正的方式将其交付给智能合约，因为无论是玩家，游戏创作者还是外部实体都无法篡改或操纵随机性以对自己有利。



![Chainlink VRF enables input and output randomness for in-game scenarios for blockchain games.](img/697ce9d3bc68b82feed50c6a56a9dce4.png)

<figcaption id="caption-attachment-1481" class="wp-caption-text">Chainlink VRF 为区块链游戏的游戏内场景启用输入和输出随机性。</figcaption>





### 传统系统

Chainlink 的另一个关键用例是为数据提供商、物联网网络、网站和企业等传统系统提供一种方式，使其数据和服务可用于任何区块链网络。由于 Chainlink 网络是区块链不可知的，Chainlink oracles 充当连接当前数字和数据基础设施到任何/所有区块链网络的集成网关。在最近由 Chainlink 联合创始人 Sergey Nazarov 共同撰写的题为[弥合治理差距:区块链和遗留系统的互操作性](http://www3.weforum.org/docs/WEF_Interoperability_C4IR_Smart_Contracts_Project_2020.pdf)的世界经济论坛报告中，概述了使用 Chainlink 等 oracle 网络将传统系统与区块链连接起来的行业标准互操作性框架。

这些只是 Chainlink 提供的许多功能中的一部分，这些功能允许智能合约以高度的安全性和可靠性与外部数据和系统进行交互。最终结果是，基于区块链的智能合约应用程序能够在更加多样化的市场中实现更多的使用案例。

如果区块链是分散的计算机，智能合同是分散的应用程序，那么 Chainlink 可以被认为是一个分散的互联网，最终允许智能合同与外部世界进行交互，同时保持区块链技术在安全性、透明度和信任方面的基本保证。

## 额外资源

如果您是区块链技术的新手，并且想要深入了解，我们建议您按顺序阅读以下教育系列:

*   [什么是区块链](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/)？
*   [什么是智能合约](https://chain.link/education/smart-contracts)？
*   [什么是数据和 API](https://blog.chain.link/understanding-how-data-and-apis-power-next-generation-economies/)？
*   [什么是甲骨文问题](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)？
*   [什么是 Chainlink 节点运算符](https://blog.chain.link/what-is-a-chainlink-node-operator/)？
*   [混合智能合约解释](https://blog.chain.link/hybrid-smart-contracts-explained/)

如果你想要更技术性的东西，我们鼓励你阅读[原始 Chainlink 白皮书](https://link.smartcontract.com/whitepaper)、 [Chainlink 2.0 白皮书](https://research.chain.link/whitepaper-v2.pdf)、[开发者文档](https://docs.chain.link/)，并浏览 [Chainlink 博客](https://blog.chain.link/)以获得各种资源。

要了解最新的新闻和事件，请关注各种官方 Chainlink 社交媒体账户，并订阅 [Chainlink 简讯](https://chn.lk/newsletter)。

[网站](https://chain.link/) | [不和](https://discordapp.com/invite/aSK4zew)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [价格供稿](https://feeds.chain.link/)|[DeFi](https://www.chain.link/solutions/defi)|[VRF](https://chain.link/solutions/chainlink-vrf)|[文档](https://docs.chain.link/docs/getting-started)**