# 展示 2020 年 HackMoney 虚拟黑客马拉松的获胜者

> 原文：<https://blog.chain.link/showcasing-the-winners-of-the-2020-hackmoney-virtual-hackathon/>

我们有幸参加了由 ETHGlobal 赞助的 2020 [HackMoney 虚拟黑客马拉松](https://hack.ethglobal.co/online/showcase)。黑客马拉松的参与者有整个 4 月的时间来创建最好的工作[智能合同](https://chain.link/education/smart-contracts)应用程序，整合 Chainlink 的前三名项目可获得 5000 美元的链接奖金。

总共有 18 个项目将 chain link[Oracle](https://chain.link/education/blockchain-oracles)集成到他们的应用程序中，代表了整个黑客马拉松中使用最多的协议之一。获胜者是根据他们的创造力、可用性和链环集成的技术复杂性选出的。顶级应用包括游戏竞赛的无损失奖励平台、stablecoins 的自我维持标记化指数和 dex 聚合器驱动的游戏。

## 第一名:精灵

在 LINK 中赢得 2500 美元冠军的是来自以色列、泰国和美国的四人开发团队 [Genie](https://hack.ethglobal.co/showcase/genie-recIFwzUZH3BopAjG) 。Genie 是一个游戏和比赛的无损失奖励平台，支持社区驱动的电子竞技比赛和挑战。通过与流行的在线游戏(如《流放之路》)的整合，任何玩家都可以参加无风险的竞技比赛，现金奖励以稳定积分的形式支付。

任何人都可以通过选择游戏和创建预定义配置的池智能合同来发起比赛。玩家通过将资产加入池合同来加入，池合同代表他们进入竞争的门票。当玩家竞争时，这个资金池被投资到位于区块链的借贷协议中心以产生利息，最终成为获胜玩家的奖励。一旦比赛结束，所有参与者都可以提取他们的原始股份，而获胜者可以收回他们的股份以及池中产生的所有利息。

Genie 使用 Chainlink oracles 的分散网络将池智能合同与验证获胜者所需的离线游戏数据连接起来。Chainlink 的外部适配器用于从链外游戏 API 读取比赛结果，然后将响应写入池合同，以执行对获胜者的支付。



[https://player.vimeo.com/video/422234684?app_id=122963](https://player.vimeo.com/video/422234684?app_id=122963)



Genie 的后端开发人员 Brahma 阐述了 Chainlink 去中心化的重要性，他说“重要的是它是无信任的，所以玩家不必信任 Genie 团队来验证和奖励获胜者。”Brahma 还讨论了 Chainlink 如何使 Genie 上可用的游戏数量更容易扩展，他说“任何时候有人想集成一个新游戏，他们只需构建一个新的 Chainlink 外部适配器。”

有兴趣了解更多关于 Genie 及其使用 [Chainlink Adapters](https://github.com/genie-platform/genie-chainlink-adapters) 的信息吗？在 [GitHub](https://github.com/genie-platform) 上探索他们的代码库。

## 第二名:DefiDollar

在 LINK 中获得 1500 美元奖金的第二名是由 Arpit Agarwal、Deep Joshi 和 Manthan Satani 组成的三人小组 [DefiDollar](https://hack.ethglobal.co/showcase/defidollar-reclDekIJG0kSaW95) 。DefiDollar 是一个稳定货币的符号化指数，使用 [DeFi](https://chain.link/education/defi) 原语构建，以维持其美元挂钩。

[根据 DefiDollar 团队](https://medium.com/@atvanguard/introducing-defidollar-742e30be9780)的说法，当前的 stablecoins 经常遭受波动，存在广泛的治理问题，并存在与地址黑名单或资金损失相关的集中保管风险。DefiDollar 通过创建一种指数代币(defi dollar)来解决这些问题，这种代币由基于美元的顶级稳定货币担保。

DefiDollar 的核心智能合约允许用户存入最多 8 个现有的 stablecoins，然后重定向到 Aave 的分散货币市场协议。这些稳定债券抵押了附息债券，然后存入流动性池(平衡器)以赚取交易费用。来自 Aave 的利息和来自 Balancer 的交易费用都在收益池合同中累积，可用于支付协议费用。

为了保持稳定债券之间 1:1 的比率，套利者受到激励重新平衡流动性池。然而，也有这样的情况，所有稳定的货币都在 1 美元以下交易，这使得与 1 美元挂钩的赤字美元面临风险。为了应对这些情况，Chainlink oracles 定期将 [Chainlink 的价格参考数据馈送](https://data.chain.link/)给 DefiDollar 核心合约，以告知其基础稳定合约的当前价格。当合约注意到所有稳定的硬币价格都低于 1 美元时，它会从收益池中提取硬币，对流动性池进行再抵押，并重新建立 1 美元的挂钩。

[https://www.youtube.com/embed/m3iAvOw8ezw?feature=oembed](https://www.youtube.com/embed/m3iAvOw8ezw?feature=oembed)

当被问及 Chainlink 的价值时，Arprit 解释说:“我们在 oracle 解决方案中使用 Chainlink，是因为 Chainlink 网络已经为大多数稳定的公司提供了安全、分散的链上价格参考数据。此外，所有以太坊测试网都提供 Chainlink 价格参考源，从而最大限度地减少集成工作，实现无缝测试。”

DefiDollar 在 Kovan testnet 上直播，你可以在这里尝试他们的解决方案[，或者在](https://www.defidollar.xyz/) [GitHub](https://github.com/defidollar) 上探索他们的代码库。

## 第三名:糖果商店

在 LINK 中赢得 1000 美元奖金的第三名是 [CandyShop](https://hack.ethglobal.co/showcase/candyshop-recaC7q4YjNVRj4tq) ，这是一个由 Vaibhav Chellani、Arth Patel 和 Thrilok Kumar 等区块链开发人员组成的印度团队。CandyShop 是一个 DEX 聚合器，它通过对用户互换进行套利并通过抽奖与最终用户分享套利利润来优化效率。

CandyShop 旨在通过在 Uniswap V2 使用快速掉期对 Uniswap V1 的大宗交易进行套利，来减少大宗交易的滑点。用户将他们的令牌交换请求发送到 CandyShop，后者在 uni WAP V1 上执行交换。然后，CandyShop 利用 Uniswap V2 的快速掉期(在同一笔交易中偿还的临时贷款)对同一笔交易进行套利。从快速互换中节省的资金被视为利润。利润的 20%作为让用户参与抽奖的“糖果费”，剩下的 80%返还给用户。

坎迪费存入彩票池，投资于一种资产或复合资产，赚取为期一周的利息。用户还可以通过存款代币来赞助彩票池，以帮助积累更多的利息。使用 [Chainlink 的可验证随机函数](https://docs.chain.link/docs/chainlink-vrf) (VRF)来选择随机赢家，这是一种可证明公平的产生真实随机性的方法，可在链上验证。一旦中奖者被选中，赞助商的本金将被返还。

CandyShop 的 Vaibhav Chellani 分享了 [Chainlink VRF](https://blog.chain.link/chainlink-vrf-on-chain-verifiable-randomness/) 对他们彩票应用的重要性，声称“Chainlink 提供了一个快速插入系统来获取随机数，这使得在区块链上获取随机数的复杂任务变得非常简单。”

你可以在 Ropsten testnet [这里](https://musing-poincare-635b61.netlify.app/swap)试用一下 CandyShop 的演示，或者在这里查看一下 GitHub repo [。](https://github.com/itsthecandyshop/)

[https://www.youtube.com/embed/Ig9JcofRrOM?feature=oembed](https://www.youtube.com/embed/Ig9JcofRrOM?feature=oembed)

使用真实世界数据的广泛应用激发了我们的活力，并增强了它们的链上功能。虽然只有三个获胜者，但有大量创造性、创新性和技术性的项目是使用 Chainlink powered 分散式 oracle networks 构建的。我们期待继续参与未来的黑客马拉松，推进我们的使命，使智能合同成为全球数字协议的主导形式。

## 今天就开始用 Chainlink 建造吧

如果您想立即开始使用 Chainlink 进行构建，请访问[开发者文档](https://docs.chain.link/docs/getting-started)，加入关于[不和谐](https://discordapp.com/invite/aSK4zew)的技术讨论，和/或[联系我们](/cdn-cgi/l/email-protection#3e5d4b4d4a51537e5d565f57501052575055)关于安全启动您的数据支持应用程序、 [Chainlink 价格参考数据合同](https://feeds.chain.link/)或 mainnet 上的 [Chainlink VRF](https://blog.chain.link/chainlink-vrf-on-chain-verifiable-randomness/) 产品。

如需了解更多信息，请查看 [Chainlink 网站](https://chain.link/)或关注我们的 [Twitter](https://twitter.com/chainlink) 或 [Reddit](https://www.reddit.com/r/Chainlink/) 。