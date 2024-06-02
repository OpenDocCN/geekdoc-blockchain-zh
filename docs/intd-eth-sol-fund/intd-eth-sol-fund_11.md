© Chris Dannen 2017Chris DannenIntroducing Ethereum and Solidity10.1007/978-1-4842-2535-6_11

# 11. 高级概念

Where the Ethereum Protocol is going, and where it came fromChris Dannen^(1 )(1)Brooklyn, New York, USAA book introducing Ethereum and Solidity would not be complete without mention of the nascent cult of personality forming around Vitalik Buterin, the inventor of Ethereum and a collaborator on a handful of other high-profile blockchain projects.

## 谁在引领软件开发者走向去中心化？

或许对于 Buterin 最好的描述来自于 2014 年春季由作家 Morgan Peck 在在线杂志 Backchannel 上发表的一篇文章。¹ 这篇文章描述了作者与以太坊联合创始人的第一次相遇：

> Buterin 是唯一清醒的人。他坐在外面的一把摇椅上，专注地工作着。我没有打扰他，他也没有打招呼。但是，我记得当时他给我的印象。这个瘦削的 19 岁男孩，四肢和关节都很突出，像一只螳螂一样悬浮在他的笔记本电脑上，以难以置信的速度交付着灵活、致命的打击。事实证明，Buterin 才是大家聚在一起的原因。两个月前，他发表了一篇白皮书，描述了一项不可能实现的雄心勃勃的技术，这项技术超越了比特币只能实现无法阻止、无中介数字支付的使命，设想了一个用于各种自主软件的平台。

在这个自由开源网络协议运动的中心，Buterin 的智力领导力是独一无二的。除了项目取代 HTTP Web 的雄心壮志之外，可能最令人震惊的是其速度。以太坊项目于 2014 年启动，2015 年投入运营，并在 2016 年成为继比特币之后的第二大加密货币网络。有关所有以太坊基金会成员的当前列表，请访问 [www.ethereum.org/foundation](http://www.ethereum.org/foundation) 。在 2017 年，核心开发团队计划推出其他组件，这些组件将使以太坊达到与我们今天所熟悉和喜爱的 Web 应用程序相当的水平，但具有像前几章描述的惊人的新功能集。本章的其余部分涉及以太坊路线图以及一些尚未解决和未构建的组件。如果您想在这里停下来深入研究以太坊网络的数学、经济和商业基础，那么您将找不到比以太坊博客更好的长篇、深度文章，Buterin 在其中阐述了有关协议核心概念的思想。 

### Vitalik 的最佳技术博客文章

以下是一些有趣的博客供参考：

+   [`blog.ethereum.org/2015/06/06/the-problem-of-censorship/`](https://blog.ethereum.org/2015/06/06/the-problem-of-censorship/)

+   [`blog.ethereum.org/2015/04/13/visions-part-1-the-value-of-blockchain-technology/`](https://blog.ethereum.org/2015/04/13/visions-part-1-the-value-of-blockchain-technology/)

+   [`blog.ethereum.org/2015/04/27/visions-part-2-the-problem-of-trust/`](https://blog.ethereum.org/2015/04/27/visions-part-2-the-problem-of-trust/)

+   [`blog.ethereum.org/2015/01/10/light-clients-proof-stake/`](https://blog.ethereum.org/2015/01/10/light-clients-proof-stake/)

+   [`blog.ethereum.org/2015/01/23/superrationality-daos/`](https://blog.ethereum.org/2015/01/23/superrationality-daos/)

要查看更多为以太坊生态系统做出贡献的人员和公司名单，请访问[`ecosystem.eth.guide`](http://ecosystem.eth.guide)。

## 以太坊发布时间表

现代服务器应用程序擅长三件事：计算和运行程序，记住我们的数据，并促进人类互动。今天，以太坊虚拟机可以进行计算，但无法存储大量数据，也无法作为人与人之间消息传递的中介。恰巧的是，正如我们所说，后两个组件正在进行中。近期以太坊路线图包括三个主要组件：

+   EVM：去中心化状态（已完成！）

+   Swarm：去中心化存储

+   Whisper：去中心化消息传递

### Whisper（消息传递）

Whisper 是以太坊协议的一部分的分布式消息传递系统，将可供使用以太坊虚拟机作为其后端的 Web 应用程序。与本书的前几章不同，在这些章节中，“消息”指的是从一个智能合约传递到另一个智能合约的数据对象，在这种情况下，我们是以传统方式使用它：一个人通过网络协议与一个或多个其他人进行通信。

### Swarm（内容寻址）

Swarm 是一个基于内容寻址的会计协议。它使用不可变数据，对其进行分片，并将其存储在分布式网络中，以便在应用程序需要时轻松检索。Swarm 的目标是能够在同一内存地址下找到文件的不同版本，模仿今天 URL 中的域路径及其文件夹结构。需要注意的是，该寻址协议与硬件无关。它仅仅是一个索引，用于存储数据块的位置。这种 Blob 存储方案是分散式系统的一个热门应用，并且由于一些由 BitTorrent 领先的创新，Swarm 使其变得更加容易。如果你不想等待 Swarm，可以查看一个现有的分布式文件存储协议，叫做星际文件系统（Interplanetary File System，或 IPFS），它也可以与以太坊 dapps 兼容。假设现在是 2020 年，你在 Mist 浏览器中访问一个以太坊应用程序。到那时，我们可以想象已经有一个可读的命名空间系统存在；以太坊已经完全与 Web 平行，并具备了自己的域名查找系统。以下是使用 Swarm 协议的 dapp 的数据检索过程：

1.  1.在 Mist 中导航至应用程序。输入以太坊域名。

1.  2.域名被转换为 Swarm 哈希。

1.  4.请求与此哈希链接的新文件会在数据到来时加载最新数据。

1.  3.Swarm 检索与此哈希相关联的 HTML/CSS/JS 文件。

对于用户来说，体验与使用现有网络应用程序的体验没有太大的区别。然而，这里的目标是实现分布式拒绝服务 (DDoS) 抗性的 P2P 存储，提供 100％的正常运行时间，并且可以被各种客户端轻松地以编程方式访问，访问各种不同存储网络上的文件。您可以通过阅读[`swarm-gateways.net/bzz:/swarm/#the-thsph-orange-paper-series`](http://swarm-gateways.net/bzz:/swarm/#the-thsph-orange-paper-series)上的白皮书了解更多关于 Swarm 的信息。

## 未来的发展方向

2016 年春季，比特林发布了一篇名为“Mauve Paper”的新白皮书。在这篇论文中，他列出了以太坊路线图的七个主要焦点：

+   从工作证明向权益证明共识算法的过渡。作为一个共识系统，工作证明在能源消耗的角度来看是有效的但昂贵的。在不挖矿的情况下确保共识将减少电力浪费以及对通货膨胀性发行方案的需求。

+   权益证明应该能够产生更快的区块时间，从而实现数据更精细化、效率更高，而不会丧失安全性或中心化风险。

+   经济最终性。正如第三章所述，以太坊对企业的承诺是建立一个分散式的交易结算最终性系统。权益证明系统可能包括验证节点的角色，这些节点完全承诺一个区块，这意味着如果它们串通传播一个错误的区块，它们将失去他们的 ETH 余额（可能达到数百万美元）。

+   当前全节点需要的计算资源是一个问题，尤其是在可扩展性方面。庞大的区块链、1 GB DAG 以及繁重的 CPU 或 GPU 要求使智能手机和其他低功耗设备无法运行以太坊节点守护程序。要阅读团队关于可扩展性的白皮书，请访问 [`github.com/vbuterin/scalability_paper/blob/master/scalability.pdf`](https://github.com/vbuterin/scalability_paper/blob/master/scalability.pdf) 。另一个关于可扩展性的重要阅读是所谓的链纤维的使用，在 www.reddit.com/r/ethereum/comments/31jm6e/new_ethereum_blog_post_by_dr_gavin_wood/。

+   分片区块链数据并实现跨片通信是扩展的另一个关键要素。分片是将单个数据块分解到数据库中的过程，以便在需要时重新组装。区块链不会进行分片。然而，让 EVM 状态的不同部分由不同节点存储，并构建可以在那里访问它们的应用程序应该是可行的。

+   抵抗审查的重要性体现在验证节点试图共谋跨所有 shard 封锁某些交易以阻止最终确认。这在以太坊 1.0 中已经存在，但将在随后的版本中加强。

紫红色论文位于 [`vitalik.ca/files/mauve_paper.html`](http://vitalik.ca/files/mauve_paper.html) 。

## 其他有趣的创新

随着以太坊团队努力实现他们对 EVM 的愿景，以太坊开发者社区继续尝试他们自己的解决方案。一些吸引关注的有希望的技术创新包括：

+   状态通道：像微支付通道一样，状态通道是两个基于区块链的数据库之间的链接，通过该链接可以在不等待主链处理交易的情况下同步和更新分类帐。要了解更多关于这些可能如何工作的信息，请查看 [www.jeffcoleman.ca/state-channels/](http://www.jeffcoleman.ca/state-channels/) 。

+   轻量级客户端：轻量级客户端将允许智能手机和其他低功耗计算机使用 Merkle-Patricia 树的一部分来构造证明，证明某个交易确实在一个区块中。这将省去下载和同步整个区块链的必要性，但仍然可以验证、发送和接收交易。要了解有关轻量级客户端可能如何工作的更多信息，请参阅这个网络存档：[`web.archive.org/web/20140623061815/http://sourceforge.net/p/bitcoin/mailman/message/31709140/`](https://web.archive.org/web/20140623061815/http://sourceforge.net/p/bitcoin/mailman/message/31709140/) 。

+   以太坊计算市场：计算市场将是一种允许某些交易在链外发生，并稍后与公共链协调的方式之一。一个正在尝试这种方法的项目可以在 [`github.com/pipermerriam/ethereum-computation-market`](https://github.com/pipermerriam/ethereum-computation-market) 找到。

## 完整的以太坊路线图

尽管软件开发可能是一个不可预测的过程，但以太坊开发人员在达到时间里程碑方面表现出了非凡的能力。在撰写本文时，以下是他们已完成的工作以及尚未完成的工作。

### 初始发布（2015 年）

初始阶段的几个主要目标都按时完成了。在以太坊的这个阶段，所有工作都是通过命令行完成的。当时的优先事项包括以下内容：

+   启动挖矿操作（以降低的奖励率）

+   将以太币列入加密货币交易所

+   建立用于测试 dapps 的实时环境

+   创建用于获得以太的沙盒和水龙头

+   允许人们上传和执行合同

### Homestead Release (2016)

Homestead 发布将更多的主流加密货币爱好者带入了 Mist 浏览器的使用者行列。它的特点如下：

+   以太挖矿奖励率提高到 100%

+   没有网络中断

+   稍微不那么 beta 状态（更少的警告）

+   对命令行和 Mist 的更多文档

### Metropolis (2017)

就目前而言，以太坊协议开发的第二阶段 Metropolis 正在进行中。这个发布将是 Mist 的真正登场派对，完全功能后，它将看起来有点像 Chrome 和 iOS App Store 的混合体。它将包括几款重量级的第三方应用程序。到这个阶段，Swarm 和 Whisper 将运作起来。

### Serenity (2018)

这个阶段之所以被命名为 Metropolis，是因为计划从工作量证明转向不那么繁忙的东西：理想情况下，是某种形式的股权证明算法。目前，以太坊基于 POS 的共识引擎的临时代码名为 Casper。²虽然还没有人完善该共识系统，但进展每周都在发生，而在这一领域工作的数学家和计算机科学家似乎对即将到来的突破充满信心。有关以太坊研究这方面背景材料的两篇文章可以在以下网址找到：

+   [`blog.ethereum.org/2015/12/24/understanding-serenity-part-i-abstraction/`](https://blog.ethereum.org/2015/12/24/understanding-serenity-part-i-abstraction/)

+   [`blog.ethereum.org/2015/12/28/understanding-serenity-part-2-casper/`](https://blog.ethereum.org/2015/12/28/understanding-serenity-part-2-casper/)

## 摘要

当 Serenity 发布并且工作量证明挖矿结束时，世界会变成什么样子？很难说。但是以太坊、比特币和其他加密网络将对商业信息技术产生几个相当可预测的影响。二十世纪伟大的经济学家之一，罗纳德·科斯，因其洞察力而闻名，即公司存在的初衷是为了避免每天都要去市场寻找工人的“交易成本”。公司建立长期雇佣协议以增加效率。但是，这些在少数几十名工人中增加效率的官僚流程在规模上会成为障碍，使大公司变得缓慢和不具竞争力。因此，它们试图找到一个平衡点，即最少的官僚制度创造最大的效率。在过去的二十年里，技术已经加速了商业的发展，因为企业已经在大规模软件系统方面积累了专业知识。最近，大量的努力已经投入到使这些系统更擅长处理承包商、顾问和自由职业者。这些临时工使公司能够在需求出现时迅速组建团队，并且无需解雇全职员工就可以将其解散。现代公司的边界变得更加渗透。根据软件公司 Intuit 的一项研究，到 2020 年，美国约 40％的劳动力将是“临时工”。以太坊承诺加强这种趋势。当整个世界都可以在一个可以执行无需信任应用程序的全球交易单体中运作时，办公楼（或虚拟专用网络，或公司本身）的限制变得越来越不必要。当补偿方案可以轻松地由智能合约中的一系列 if-then 语句组成时，工资和奖金之间的区别变得模糊。公司的大小、年龄或位置可能不再具有关于其信誉或重要性的文化内涵。终身雇员、公司男人或公司女人的时代可能正在结束。这种转变已经在政府和银行的最高层得到认可。 2017 年 1 月 18 日，联邦储备委员会主席珍妮特·耶伦在加利福尼亚联邦俱乐部举行的炉边聊天中被问及区块链技术的前景时，她的回答：

> 我们正在审视其在我们自己使用的一些技术方面的承诺，许多金融机构也在关注。它可能会在全球经济中交易结算的方式上产生重大影响。 ⁴

或许一个范式转变即将到来：首先，个人和企业将逐渐适应他们自由参与商业协议的自由，甚至有些可能是长期的，几乎不需要对手方，并且几乎不关心公司甚至国家的边界。数百万美元的交易也许（一段时间内）仍然会用笔墨签署，但有多少价值 1 到 100,000 美元的合同可以由运行标准条款的以太坊机器处理？能节省多少美元和工作时间？多少分歧变得不重要了？多少商业协议可能变得更公平且可执行？毫无疑问，有很多。这就是以太坊的承诺。脚注 1 后台，"The Uncanny Mind That Built Ethereum," [`backchannel.com/the-uncanny-mind-that-built-ethereum-9b448dc9d14f#.ct4n4b561`](https://backchannel.com/the-uncanny-mind-that-built-ethereum-9b448dc9d14f#.ct4n4b561)，2016 年。2 以太坊博客，"Introducing Casper, the Friendly Ghost," [`blog.ethereum.org/2015/08/01/introducing-casper-friendly-ghost/`](https://blog.ethereum.org/2015/08/01/introducing-casper-friendly-ghost/)，2015 年。3Intuit，"The Intuit 2020 Report," [`about.intuit.com/futureofsmallbusiness/`](http://about.intuit.com/futureofsmallbusiness/)，2010 年。4YouTube，Janet Yellen interview，[www.youtube.com/watch?v=ktBgb4xHKGY](https://www.youtube.com/watch?v=ktBgb4xHKGY)，2016 年。
