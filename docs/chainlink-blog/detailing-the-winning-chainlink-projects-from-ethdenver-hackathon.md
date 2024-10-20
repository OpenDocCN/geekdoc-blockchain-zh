# ETHDenver 黑客马拉松的获奖项目

> 原文：<https://blog.chain.link/detailing-the-winning-chainlink-projects-from-ethdenver-hackathon/>

Chainlink 团队很高兴参加 2019 年 2 月 [ETHDenver Hackathon](https://www.ethdenver.com/) 。除了在区块链博物馆向使用 Chainlink 的顶级项目颁奖之外，Sergey Nazarov 还参加了一个关于“Dapps 的神谕和数据”的小组讨论，集成工程师 Thomas Hodges 为开发人员举办了一个关于如何“构建连接到现实世界数据的智能合同，事件&API”的研讨会。

黑客马拉松参与者有 36 个小时的时间来构建最好的区块链应用程序。 [Chainlink](https://chain.link/) 颁发了三个奖项:2500 美元的 Chainlink 最引人注目和现成的原型，1500 美元的 Chainlink 最具创意的应用，以及 1000 美元的评委选择奖励。鉴于连接链上智能合同和链下资源的可能应用过多，与会者展示了各种分散化的概念，从金融衍生品到体育比赛，再到公共活动规划。

## 法官的选择:聪明的小猪

由迈克尔·阿里夫、托比·阿尔加和李东旻组成的三人小组“聪明小猪”获得了评委选择奖。SmartPiggies 提出了一个点对点全球期权市场的开源标准。期权合约是买卖双方之间的一种简单的金融协议，它给予买方以溢价在约定的到期日之前以特定价格购买资产的选择权。

由于交易对手的信任问题，期权合约通常只由投资银行提供，进入壁垒很高。SmartPiggies 使用分散的基础设施为世界各地的任何人买卖期权合约打开市场。根据该团队的说法，“聪明猪为买家提供保护，防止任何资产、产品或服务的价格发生不良变化。”它还允许愿意承担风险的卖家有机会通过向市场出售期权合约(聪明猪)来赚取溢价。

所有者可以在任何时候行使期权，但是一旦这只聪明的小猪到期，那么任何一方都可以解决它。SmartPiggies 使用 chain link[Oracle](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)在结算时参考基础资产的价格数据。该数据用于触发资金所有权的状态变化。“这些聪明的小猪很少接触真实世界(外链)，唯一重要的是你可以通过 Chainlink 获得外链价格。拥有一家致力于以最安全的方式做好一件事的公司，让人们开发智能合同变得极其容易。”

## 第二名:格兰方多

获得第二名的是 Gran Fondo，这是一个由 Ron Gierlach，Aaron Biser，Greg Prouty 和克里斯·沃克组成的四人小组。Gran Fondo 是一个 Dapp，旨在通过分散的体育竞赛来促进优秀的运动。它使运动参与者能够根据绩效目标创建智能合同。希望参加的运动员在 ETH 上下注，然后根据所述目标的完成情况相互竞争 ETH 奖金。

它利用跑步和骑行的社交健身跟踪平台 Strava，结合 GPS 时间戳数据和可选的物联网可穿戴设备来跟踪用户的表现。Gran Fondo Dapp“使创建或参加健身挑战、查看竞争对手和申领奖励变得简单，前提是 Strava API 证明您已经赢得了这些奖励。”



![Gran Fondo User Interface](img/18492281f9edc3087dfdfe48c67bef53.png)

<figcaption id="caption-attachment-468" class="wp-caption-text">格兰方多用户界面</figcaption>





据该团队称，“我们将从 Strava API 获得的运动员数据与满足约定挑战所需的条件进行比较。“虽然链上智能合同具有挑战的条件，”大部分处理是在链外完成，以减少链上的带宽和成本。“Chainlink oracles 将链外数据提供给链内合同，以触发向获胜者发放资金。作为狂热的跑步者和自行车运动员，该团队认为 Gran Fondo 是目前促进分散式体育比赛的最佳方法之一，其基础是值得信赖的表现和可靠的支出。

## 第一名:EventLINK

最后，获得令人垂涎的第一名荣誉的是 EventLINK，这是一个由 Max Seesing，Henry Nguyen，Connor Maloney 和 Sharon 曼里克-希门尼斯组成的四人小组。他们发现，规划公共活动的挑战之一是组织者很难确定最佳地点。目前，收集人群兴趣的指标被简化为“粗略的假设”EventLINK 通过使用 Twitter APIs、智能合约和赌注机制来解决这个问题，以“利用大众的力量”。

利用两步流程，EventLINK 通过使用 Twitter API 指标(如带有 GPS 位置数据的转发)将字段过滤到某个阈值，找到最有可能资助众包活动的城市。一旦对可用城市进行了精细的选择，众筹[智能合同](https://chain.link/education/smart-contracts)就可以以一种近乎竞争的结构提供给每个城市，看谁能筹集到最多的资金，或者谁能最快地筹集到预定金额的资金。最终，活动组织者可以定义智能合同的条款。

使用 chain link[Oracle](https://chain.link/education/blockchain-oracles)，活动组织者可以通过在 Keybase 上验证他们的身份来要求他们的股份，key base 是一种广泛使用的身份服务，允许你通过利用加密签名来证明你的身份。群众现在可以相信，智能合同中的资金将只在从 Chainlink oracles 交付密钥库数据后发放给活动组织者。该团队表示，“一个分散的 oracle 网络非常适合于确保信任分散在众多节点运营商之间，而不是由一个中央运营商来证实签名。”

该团队看到了这种应用的巨大潜力，称“这种众筹解决方案减少了将活动带到一个城市的大量管理费用/中间人参与。售出一张票可能是有保证的，而营销部门可能要为他们付出很多努力，因为资金已经有了保障。”

三名黑客马拉松获胜者都展示了 Chainlink 神谕如何触发区块链的状态变化。我们相信，使用 Chainlink oracles 的自动化智能合同执行将使基于现实世界事件的复杂操作得以执行。这不是一个未来派的概念，但是开发者现在就可以实现。