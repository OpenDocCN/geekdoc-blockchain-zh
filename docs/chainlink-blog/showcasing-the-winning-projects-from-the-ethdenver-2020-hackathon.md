# 展示 ETHDenver 2020 黑客马拉松的获奖项目

> 原文：<https://blog.chain.link/showcasing-the-winning-projects-from-the-ethdenver-2020-hackathon/>

Chainlink 团队连续第二年参加 ETHDenver 黑客马拉松。该团队夜以继日地工作，支持那些希望使用 Chainlink powered [分散式 oracle networks](https://chain.link/education/blockchain-oracles) 将他们的[智能合同](https://chain.link/education/smart-contracts)与现实世界的数据和系统对接的热情开发人员。互联智能合约的信息正在引起共鸣；在这次顶级以太坊黑客马拉松上，我们看到了一些迄今为止最高质量的黑客马拉松项目提交。

在活动中，我们宣布了我们正在与链外实验室进行的[工作，使用 Chainlink 节点计算可扩展的 solidity 智能合同链外，以及我们与 0x 的](https://medium.com/offchainlabs/scalable-low-cost-computation-of-ethereum-smart-contracts-using-arbitrum-on-the-chainlink-8985c6542d4e)[合作开发新的 DEX 功能](https://twitter.com/chainlink/status/1227999845182558210?s=20)。Sergey 发表了一个强有力的演讲，讲述了 [Chainlink 如何通过超越代币来帮助重新定义智能合约行业](https://www.youtube.com/watch?v=B6SQy5zPoZQ&feature=youtu.be&t=38557)。产品经理 Johann Eid 发表了关于“[安全地将智能合同连接到链外数据源](https://youtu.be/B6SQy5zPoZQ?t=19946)的演讲，高级合作伙伴经理 Andrew Thurman 参加了关于[第二层技术](https://youtu.be/gRBCD5nzBdQ?t=20348)的小组讨论。

黑客马拉松参与者有 36 个小时的时间来构建最好的区块链应用程序。我们向使用 Chainlink 的最佳智能合同应用程序颁发了三份价值 5000 美元的奖金。与会者展示了如何在分散的基础设施上构建数据驱动的商业模式，包括参数保险产品、多平台自动化杠杆交易和实时在线出勤跟踪。

## 第一名:InsuraLink

InsuraLink 赢得了 2，500 美元的大奖，这是一个由来自 [Secure Data Links](https://www.securedatalinks.com/) 的 Aidan Tetther、Owen Evans、Raymond Mogg 和 Patrick McNab 组成的四人团队。正如最近与 [Etherisc](https://blog.etherisc.com/etherisc-to-leverage-chainlink-oracles-for-decentralized-flight-insurance-product-9559b64d79c7) 、[parameter insurance](https://blog.chain.link/blockchain-insurance/)通过 Chainlink oracle 支持的智能合同所展示的那样，这种模式在降低索赔处理成本和开放保险供应方的公众参与方面具有巨大的潜力。

[InsuraLink](https://github.com/securedatalinks/InsuraLink-Frontend/blob/master/InsuraLink.pdf) 是一个模块化框架，用于设计数据驱动的保险协议，使用 Chainlink oracles 来桥接物联网和智能合同。这使得物联网设备收集的真实世界数据能够被转发到并触发[基于保险的智能合同](https://blog.chain.link/blockchain-insurance/)。结果是链上事件的自动执行，例如基于真实世界的可保事件对投保人的索赔支付。链环神谕扮演两个关键角色:

1.  **启动**–物联网传感器用于监控环境中超出规定阈值的偏差，例如温度低于某一点。当出现偏差时，物联网设备充当触发链式作业的外部启动器。启动器可能依赖于多个事件，例如所有三个类别的异常:温度、湿度和重力。
2.  **运输**–chain link 节点监控日志事件，使用来自指定物联网设备的数据响应作业。多个链接节点用于防止单点故障。用户还可以通过对同一数据发起多次回调来增加安全性。



![A basic overview of the architecture design of InsuraLink](img/6861d7e6f5d8a63f8c1f611d6d64059e.png)

<figcaption id="caption-attachment-390" class="wp-caption-text">insural ink 架构设计的基本概述 ‌‌</figcaption>





Secure Data Links 的团队表示,“使用 InsuraLink Marketplace 时，签订保险合同的协调成本会降低。这允许本地和跨辖区网络中的用户为他们的对等用户投保。因此，风险是本地化的、透明的，并分布在受激励的网络利益相关者之间。”该团队计划在未来添加更多功能，如支持支付的定制选项、争议功能、数据的多因素认证等。

## 第二名:1x.ag

排名第二，赢得 1，500 美元奖金的是 1x.ag，这是一个由瑟奇·昆兹、克里尔·库兹涅茨科夫、尼基塔·科兹洛夫和阿尔特姆·沃罗贝夫组成的四人团队。有各种各样的 Dapps 进入市场进行借贷、杠杆交易和分散交易。 [1x.ag](https://1x.ag/) 是一个 Dapp，使用户能够从一个用户界面建立跨不同借贷平台的杠杆交易头寸。用户可以采用自动化交易策略来管理他们跨平台的头寸，以减少汽油费，降低滑点成本，并简化用户体验。

1x.ag 旨在允许用户通过 Aave flash loans 同时从 Compound、Fulcrum、Aave 和 MakerDAO CDP 获得贷款。用户可以设置止损以防止清算，并在达到某些定义的价格点时获利，这些价格点将根据来自[chain link DeFi Oracle](https://feeds.chain.link/)的市场数据进行验证并自动执行。当清算有效时，任何人都可以调用清算或利润函数。

1x.ag 利用由 1inch.exchange 创建的开源链上聚合器 1split.eth，通过在几个不同的分散交易所(如 Kyber、Bancor、MakerDAO/Oasis 和 Uniswap)之间拆分令牌互换来交换基础抵押品。该团队承认，“在交易时定义参数对于准确对冲价格波动非常重要。Chainlink oracles 支持将更强大的对冲逻辑内置到智能合约中，使我们的机器人能够在头寸偏离止盈和止损限制时跨平台准确平仓。”



![The 1x.ag user interface for creating trade positions and automated trading strategies](img/dd1a4732edc8673624bce34d064a63f4.png)

<figcaption id="caption-attachment-391" class="wp-caption-text">用于创建交易头寸和自动交易策略的 1x.ag 用户界面</figcaption>





## **评委选择奖:我们在公共场所观看**

Iain Nash 和 Evan Trumbull 的两人团队“我们在公共空间观看”赢得了 1000 美元的评委选择奖。大型活动对企业来说是营销和联系潜在客户的重要机会。参加这些活动需要投入大量的资源，因此选择合适的活动尤为重要。问题是潜在的参与者如何知道活动组织者的承诺——预计出席人数、展位流量、潜在奖励等——实际上值得他们的宝贵资源？

[我们在公共场所观看](https://github.com/iainnash/ethdenver-we-watch-in-public)通过创建一个区块链跟踪系统来解决活动透明度的问题，该系统通过监控高流量的场馆位置来计算活动出席率。激光束和物联网传感器根据光束交叉的次数跟踪入口处的参与者，而低功耗蓝牙连接则监控整个空间的参与者。来自传感器的出勤信息通过多个链式 oracles 实时安全地传递到区块链。该团队指出，“Chainlink 简化了每隔 *N* 分钟更新数据并为实现这一目标的过程提供资金的困境。”

最终结果是提高了活动绩效指标的透明度，所有参与方都可以轻松验证。该团队表示，“通过这一监控系统，我们可以建立问责制，以更好地告知广告定价、赞助商安排和参与以及活动门票定价。”这导致了基于可验证的链上数据的动态计费的新合同结构，并且可以作为协商未来合同的不可改变的过去性能基础。

所有这三个应用程序都展示了智能合同如何通过与外链数据和系统安全交互而变得更加强大。我们特别感兴趣的是，它们如何增强用户与 [DeFi](https://chain.link/education/defi) 交互的能力，以及智能合同与不断扩大的物联网世界之间的无缝集成。

如果您是一名开发人员，并希望将您的智能合约连接到底层区块链之外的现有数据和基础设施，请联系我们[此处](https://chainlink.typeform.com/to/gEwrPO)！我们可以帮助您快速、安全地在 mainnet 上推出您的数据应用程序或 [Chainlink 价格参考数据合同](https://feeds.chain.link/)。

你也可以访问[开发者文档](https://docs.chain.link/)或者加入关于[不和](https://discordapp.com/invite/aSK4zew)的技术讨论。通过访问 [Chainlink 网站](https://chain.link/)了解更多信息，或者在 [Twitter](https://twitter.com/chainlink) 或 [Reddit](https://www.reddit.com/r/Chainlink/) 上关注我们。