# 展示埃思柏林吾妻玲二黑客马拉松的获胜者

> 原文：<https://blog.chain.link/showcasing-the-winners-of-the-etherlin-zwei-hackathon/>

在刚刚结束的鼓舞人心的 Web3 会议上，我们举办了自己的 [OracleNode 活动](https://www.youtube.com/playlist?list=PLVP9aGDn-X0T-FUrlKsdOJRF6HJYsB6eJ)，Chainlink 团队将这种兴奋带到了 2019 年 8 月的[埃思柏林吾妻玲二](https://ethberlinzwei.com/)黑客马拉松。除了向使用 Chainlink 的顶级项目颁发 4000 欧元的奖金之外，Sergey 还发表了题为“[安全地将智能合同连接到链外数据和事件](https://youtu.be/FDoLr7myvxo)”的演讲，该团队还举办了一次开发人员研讨会。

黑客马拉松参与者有 36 个小时的时间来构建最好的区块链应用程序。考虑到通过将[智能合约](https://chain.link/education/smart-contracts)连接到外部链外资源的无限可能性，令人鼓舞的是看到出现了一系列广泛的产品，如预测市场的争议解决方案、对冲 ETH 气体波动的 DAO 和 white hacker bounty 计划。

## 第一名:Chainlink \ u2661 Augur

在 LINK 中获得令人垂涎的 2500 欧元第一名的是 Chainlink \ u2661 Augur(昵称为“Chaugur”)，这是一个由来自 Flux Market 的 Peter Mitchell 和 Jasperdg de Gooijer 组成的两人团队，这是一个用户可以根据初创公司的估值创建衍生品的平台。Chainlink 的声誉系统、赌注和阈值签名功能尚未在 Mainnet 上运行，Mainnet 使用货币奖励/惩罚和分散化来激励诚实的节点行为。虽然有一个广泛的白名单过程来装载高度可信的节点，但一些用户可能想要一个完全不可信的过程来获取立即可用的外部数据。

Chaugur 是 chain link——一个去中心化的 [oracle](https://chain.link/education/blockchain-oracles) 网络和 auger——一个去中心化的预测市场的结合。在 Chaugur 中，Chainlink oracles 的任务是检索数据并将其报告给查询智能契约。如果对 oracle 数据有异议，在 Chainlink 的信誉系统仍在开发中时，可以将 Augur 作为安全的备份层来实施。Augur 的预测市场允许用户就数据的准确性进行投票，例如就衍生品合约中基础资产的市场价格在执行时是否正确进行一致投票。虽然它延长了执行和结算之间的时间，但通过利用货币激励，利用“群众的智慧”，Augur 为仲裁数据提供了一种可选的方法。

Chaugur 团队表示，“通过 Augur 的争议机制，我们整合了第二层安全性，从而消除了恶意操作 Chainlink Oracle 节点的财务动机。”Chaugur 是增强 oracle 安全性的一个有用的选项，但是 Chainlink 团队完全期望一旦我们的信誉、赌注和阈值签名在 Mainnet 上上线，就能获得大规模的卓越安全性。

## 第二名:沃尔加斯道

在 LINK 获得 1000 欧元奖金的第二名是 VollgasDAO，这是一个由 Max Fritz、Luis Schliesske 和 Hilmar Orth 组成的三人小组。VollgasDAO 是一个去中心化的自治组织(DAO ),它使用智能合约和资本集合基金来铸造、销售和促进 gasFuture tokens 的赎回。这些代币是以固定费用购买的(由 DAO 代币持有者支付),代表对特定数量的汽油的所有权，这些汽油可在未来某个日期兑现。因此，VollgasDAO 允许用户对冲未来的天然气波动，而 DAO 持有人在促进市场流动性方面略有盈利。

VollgasDAO 使用 Chainlink oracles 从 EthGasStation API 获取当前的 Eth gas 价格——这是一个获取 ETH gas 消费者数据指标的流行网站。然后，由 Chainlink oracles 获取的当前天然气价格乘以兑现的天然气期货令牌的数量，以确定用户收到的天然气总量。

该团队表示，“安排交易在以太坊上越来越受欢迎。然而，用户这样做的最大障碍之一是估计继电器的未来执行成本。”Chainlink 通过提供可靠的价格反馈来促进天然气价格的令牌化期货，从而缓解了这一问题。

## 第三名:以太耀斑

由 Bohdan Melnychuk、Bohdan Malkevych 和 Kirill Kirikov 组成的三人小组 Etherflare 在 LINK 中获得了 500 欧元的第三名奖励。Etherflare 是一个激励系统，它使用智能合同来奖励从事高效渗透测试(pen 测试)的白帽黑客。Pen 测试是基于道德的黑客行为，旨在测试网络系统的漏洞和弱点，然后通过补丁和升级成为网络改进的基础。

EthFlare 允许网络托管公司(如 Cloudflare)发行黑客可以购买的令牌，这些令牌代表特定公司的正常运行时间。然后，他们可以向托管公司偿还这些代币，如果他们成功渗透到系统中，就可以获利，如果不能，就要赔钱。在 Etherflare 的案例中，黑客必须成功执行 DDOS 攻击——淹没网站导致停机。Chainlink oracles 用于监控公司网站最近 30 天的正常运行时间，并将其报告给查询智能合同。该数据随后用于计算兑换时的代币价值。

Etherflare 利用一种游戏中的皮肤方法来实现互联网安全，而虚拟主机公司如果防止 DDOS 攻击就能获利，但如果黑客成功发起攻击，他们就会获胜。该团队表示,“Chainlink 使得在链上使用互联网数据和发明全新的金融/保险服务成为可能。在我们的案例中，Chainlink 允许我们与互联网安全提供商实施新的服务协议模式。”

三位黑客马拉松获胜者都展示了 Chainlink oracles 如何将链外数据带到区块链，以触发具有现实影响的智能合约。数据驱动的智能合同为基于无信任自动化和分散安全性的合同协议带来了范式转变。这不是一个未来的概念，而是为企业和开发人员今天实现做好了准备！