# Chainlink 赏金赢家:ETHGlobal 2021 MarketMake 黑客马拉松

> 原文：<https://blog.chain.link/chainlink-bounty-winners-ethglobal-2021-marketmake-hackathon/>

*下一届 Chainlink 虚拟黑客马拉松将于 3 月 15 日开始！[立即报名参加](https://chain.link/hackathon)竞赛，赢取 125，000+美元奖金。*

eth global 2021 market make Hackathon 是一次令人印象深刻的外出活动，智能合约开发人员在 DeFi 中拥抱创新热情，并使用 Chainlink oracles 构建先进的新 dApps。我们继续看到智能合约生态系统的爆炸性增长，因为开发人员既在分散的基础设施上构建传统的金融工具，又解锁全新的 [DeFi 原语](https://blog.chain.link/analyzing-the-defi-ecosystem-and-the-many-ways-chainlink-can-accelerate-adoption/)和市场。Chainlink 广泛采用的 oracle 网络正在帮助 dApp 开发人员安全地访问各种链外数据资源，确保随着智能合同继续锁定更多价值，他们可以依赖超可靠的外部输入和计算。

我们很高兴颁发总额为 5，000 美元的奖金，每个使用 Chainlink oracles 展示独特的外部连接[智能合同](https://chain.link/education/smart-contracts)应用的获奖项目将获得 1，000 美元。这些奖项鼓励开发人员探索 DeFi 应用的创造性方法，同时使用 Chainlink Network 安全可靠的数据基础设施将他们的智能合同连接到大量的链外数据、API 服务和计算。

感谢 eth global market make 2021 的所有参与者、赞助商和评委为开发者创造了一个提升智能合约技能的环境，以及#BuildwithChainlink。

## Chainlink MarketMake 黑客马拉松获胜者

下面的获奖者按字母顺序突出显示。

### 审计死了:精简 DeFi 保险

[Audits R Dead](https://hack.ethglobal.co/showcase/audits-r-dead-%E2%98%A0%EF%B8%8F-recOGX63mU1zXmaEI) 是一种基于以太坊的保险协议，由 Evert Kors 和 Jack Sanford 提交，通过激励安全分析师研究和评估 DeFi 协议的保险风险，为智能合同漏洞或黑客攻击提供保险。分析师通过协议费和保险池的收益获得报酬。他们对协议风险的详细评估为保险费用、保险政策和利益相关者的风险/回报权衡提供了信息。

此外，Audits R Dead 允许保单持有人和保险公司使用内部互换功能将托管资金作为治理令牌。Audits R Dead 团队使用 chain link[AAVE/美元价格数据馈送](https://data.chain.link/aave-usd)安全地对进入 AAVE 的货币掉期进行价格稳定，实现平台的监管功能，同时保持以美元为基础的保险覆盖的准确水平。这些治理策略对于审计覆盖的每个协议都是可配置的。

Audits R Dead 旨在通过风险调整协议审查来降低审计成本并提高安全性。该项目还将积极的治理参与作为 DeFi 保险的核心元素。使用 Chainlink 的防篡改甲骨文[确保治理的自动交换是安全的，而不是潜在攻击者的蜜罐。](https://chain.link/education/blockchain-oracles)

[https://www.youtube.com/embed/e06MmL6IpLQ?feature=oembed](https://www.youtube.com/embed/e06MmL6IpLQ?feature=oembed)

### 迪久。实验:以太坊-BSC 定义交换

开发者亚历山大、鲍里斯·波瓦尔、谢尔盖·皮里皮夫和波格丹一世·西沃奇金创建了 [DigiU。实验室](https://hack.ethglobal.co/showcase/digiu-lab-team-recFaz0b2bXIgun6T)通过以太坊和币安智能链(BSC)上的流动性池进行分散式交换。这使得用户可以在 DEX 界面中将令牌从以太坊钱包交换到 BCS 钱包(反之亦然)，从而简化跨链体验。

数码相机。Lab DEX 使用 Chainlink oracles 作为 EVM 链之间的桥梁。他们开发了一个 [Chainlink 外部适配器](https://blog.chain.link/build-and-use-external-adapters/)脚本，从一个链调用数据，并在另一个链上触发智能合约。数码相机。Lab DEX 可以在任何与 EVM 兼容的区块链上工作，该本机集成了 Chainlink。在这个黑客马拉松项目中，以太坊上的 Chainlink oracle 检测到一个令牌交换请求，然后激活 BSC 上的 Chainlink oracle，这将启动从流动性池到用户 BSC 钱包的转移。一个类似的过程允许用户在池的任何一边添加流动性。

信任度最小化的跨链 DEX 为用户提供了更多移动资产的选择，而无需依赖于集中的财务轨道。通过实现基于安全智能合约的跨链交换，DeFi 协议和用户可以开始开发自动化方法，以利用不断增长的多链生态系统的收益。

[https://www.youtube.com/embed/0hdak66MBQI?feature=oembed](https://www.youtube.com/embed/0hdak66MBQI?feature=oembed)

### 变速箱协议:保证金交易不足

Mikhail Lazarev 开发的 Gearbox Protocol 允许用户利用 4 倍于其保证金的保证金进行交易。在 Gearbox，有限合伙人持有经批准的资产，用户可以借入这些资产进行杠杆交易。然后，用户可以通过 Gearbox 进行各种白名单 dex 交易，交易头寸在链上受到持续监控，以发现可能导致清算的风险因素。

![A diagram of the Gearbox Protocol’s undercollateralized margin trading system flow.](img/4506b749ce470e894e13a740c59ccf77.png)

<figcaption id="caption-attachment-1823" class="wp-caption-text">Gearbox Protocol function flow.</figcaption>



Gearbox 使用由 Chainlink oracles 保护的防篡改价格数据来确定用户投资组合的风险得分。用户必须保持有效的风险水平，否则他们的抵押品将被清算，提供 LP 赌注收入。Chainlink 提供安全可靠的价格数据，确保根据公平准确的投资组合评估进行清算。



[https://www.youtube.com/embed/p_lVROj0t58?feature=oembed](https://www.youtube.com/embed/p_lVROj0t58?feature=oembed)

### 二次国库(Q2T):公共产品的分散资金

[Q2T 扩展了二次融资模式](https://hack.ethglobal.co/showcase/quadratictreasury-q2t-rec1qb30pq4pgwXsV)，为基于成功里程碑的项目提供融资。队友亚历克斯·p、叶夫根尼·沙夫库诺夫、马库斯·瓦塞姆吉、米莲娜·莫诺瓦和卡洛斯·诺弗隆构建了 Q2T，以便捐助者可以提交根据成功的项目开发版本、时间锁或各种其他里程碑标记从智能合同解锁和分配的资金。

当一个项目成功地达到一个里程碑时，就会释放预定数量的资金。这减少了项目需要花费的资源来促进资助，这样他们就可以专注于运输代码。Quadratic Treasury 的融资模式还允许使用更大的资金池来累计和重新分配从财资管理中获得的回报。Q2T 通过利用 Aave 的本地信用委托来防止少数大型捐助者用许多钱包资助项目，从而实现了 Sybil 抗性。

Q2T 使用定制的 [Chainlink 外部适配器](https://blog.chain.link/build-and-use-external-adapters/)来确定何时达到里程碑。首先，里程碑在 Q2T 系统中被有效地点对点和离线验证。当在 Q2T 中创建一个里程碑时，它会生成一个惟一的散列，并将其发送给验证器智能契约。智能合约使用 Chainlink 外部适配器在后端验证里程碑哈希。一旦散列通过验证，Chainlink oracle 就会触发一个“请求已实现”事件，该事件又会触发实现功能，将分配的资金分配到正确的地址。

Q2T 提供了一个很好的例子，使用 Chainlink 外部适配器将有用的链外数据带到链上，以自动化和分散财务流，确保这些过程是公平和透明的。

[https://www.youtube.com/embed/Ww6GojVJeSI?feature=oembed](https://www.youtube.com/embed/Ww6GojVJeSI?feature=oembed)

### 威士忌做市商:DeFi 暴露于小批量威士忌

威士忌做市商 Jasper 和 Tillman Degens 的团队创建了一个 DeFi 平台，小批量威士忌酒厂可以将即将到期的威士忌酒列为连锁令牌。投资者可以为代表小批量威士忌酒瓶的 ERC1155 代币存款，等待威士忌成熟，随着时间的推移跟踪威士忌的价值，并在到期时赎回或出售酒瓶的权利。存放的 ETH 用于 Aave 计息池，直至赎回。

威士忌做市商使用 [Chainlink ETH/USD 价格数据 Feed](https://data.chain.link/eth-usd) 来计算每瓶酒在 ETH 中存放和赎回的成本。在这种方法中，酒厂收到早期订单，以预测长期的预算和资源需求，用户在等待赎回时从存款中赚取利息，同时提前获得升值的“流动”资产。

[https://www.youtube.com/embed/bqn3MsZWqCI?feature=oembed](https://www.youtube.com/embed/bqn3MsZWqCI?feature=oembed)

## 加入 2021 年春季 Chainlink 虚拟黑客马拉松

再次祝贺获奖者，感谢所有在 ETHGlobal MarketMake 2021 黑客马拉松中使用 Chainlink 的开发人员。我们期待看到这些独特的黑客马拉松构建如何发展成成熟的项目，吸引 DeFi 空间内外的用户。

2021 年春季 Chainlink 虚拟黑客马拉松将于 3 月 15 日正式开始，所以请务必报名。这是我们迄今为止最大的一次黑客马拉松，也是一次利用 Chainlink 提升您的智能合同开发水平、向业内顶尖团队学习以及争夺超过 125，000 美元奖金的绝佳机会。注册将一直开放到黑客马拉松中途。[现在就报名吧。](https://chain.link/hackathon)

如果您想快速将您的智能合同应用程序连接到 Chainlink，请访问[开发者文档](https://docs.chain.link/)并加入 [Discord](https://discordapp.com/invite/aSK4zew) 的技术讨论。

