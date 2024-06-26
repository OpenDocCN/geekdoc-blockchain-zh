# 第二章  区块链构建模块

维塔利克·布特林在 19 岁时改变了世界。

维塔利克出生在俄罗斯，六岁时他的父母移民到了加拿大。很明显，维塔利克是一个神童：教育者很快 recognize his remarkable talents and moved him into a class for gifted children, where he excelled in math, programming, and economics.

在青少年时期，年轻的维塔利克由他的父亲，一位计算机程序员，介绍给了比特币。虽然维塔利克对这项技术着迷，但他认为比特币本身并不是最终目标，而是一种达到目的的手段。如果你能在比特币之上开发应用程序，本质上把比特币本身变成一个平台，那会怎样？

维塔利克提出了一种新型的脚本语言，可以建立在比特币之上。（作为一个类比，想想这种语言就像安卓脚本语言，它使开发者更容易创建安卓应用程序。）他当时年轻且缺乏经验，所以他的想法并没有在比特币的核心开发者中获得太多关注，这些开发者现在成了“老派”。所以维塔利克自己建立了这个项目。

像中本聪一样，这位年轻的开发者也在一份白皮书中描述了他的想法。^(1) 他描述了他于 2013 年宣布的项目，这是一个具有简单脚本语言的一般区块链平台，将允许开发者快速创建新的区块链应用程序。该平台将自带其自身的价值单位，即其自身的*数字货币*。

像中本聪一样，维塔利克围绕他的想法吸引了一小群开发者，他们帮助他原型设计和推出平台。该项目很快吸引了一群志愿者，他们愿意建立网络，因为他们 (就像比特币一样) 因为托管节点而获得小单位的价值奖励。

维塔利克将该项目命名为*以太坊*，这个名字来源于以太，一种假想的、充盈宇宙的隐形物质。^(2) 该价值单位被称为*以太*。 (这些术语很快就会变得混淆，今天*以太坊*通常被用来指代网络和价值单位。)

以太坊对区块链来说是一个巨大的进步，因为它允许一套共同的开发标准，这意味着更快的上市时间。它几乎*太*成功了，因为它让任何人都可以轻松创建可以被数字交易者购买和销售的基于区块链的价值单位。

就像互联网让任何人都能轻松发布信息（无论真实与否）一样，这项新发明让任何人都能轻松创建新的价值单位（无论是否有价值）。在某种意义上，它允许人们“印钞票”。正如您将看到的，这既是祝福也是诅咒。

历史将记住 Vitalik，与 Satoshi 一起，作为区块链的创始人之一。如今，以太坊是仅次于比特币的第二大区块链项目，它作为成功区块链项目的构建模块的一个极好的案例研究。

但就像之前的 Satoshi 一样，Vitalik 也无法预见到他的区块链项目将如何改变世界。 (你总是无法预测一个区块链项目将走向何方。)为了理解我们故事的下一部分，让我们看看区块链是如何给身体泵血的。

# 分布式账本技术：区块链的心脏

让我们回到我们的会计账本，在这个账本中，Alice 已经将一个以太坊单位转给了 Bob，Bob 又转给了 Carol，Carol 又转给了 Devansh(图 2-1)。

![Alice、Bob、Carol 和 Devansh，我们在会计账本中代表他们](img/bcss_0201.jpg)

###### 图 2-1。Alice、Bob、Carol 和 Devansh，我们在会计账本中代表他们

首先想象我们把这条信息记录到本地的 Excel 表格中。现在它存储在一个副本，一台计算机上，如图图 2-2 所示。

![一系列 ETH 交易，记录在 Excel 表格中](img/bcss_0202.jpg)

###### 图 2-2。一系列 ETH 交易，记录在 Excel 表格中

接下来，想象我们把信息从 Excel 中复制出来，放入一个 Google 表格中：现在它被共享在数百个网络节点上，跨越一个云计算集群，如图图 2-3 所示。比较 Excel 文件（一个副本，一台计算机）和 Google 表格（一个副本，许多计算机）。

![Alice 将一个 ETH 转给 Bob，记录在 Google 表格中](img/bcss_0203.jpg)

###### 图 2-3。Alice 将一个 ETH 转给 Bob，记录在 Google 表格中

区块链更进一步：许多副本，许多计算机，如图图 2-4 所示。

![Alice 将一个 ETH 转给 Bob，记录在区块链上](img/bcss_0204.jpg)

###### 图 2-4。Alice 将一个 ETH 转给 Bob，记录在区块链上

再次查看图 2-3 和 2-4，以深刻理解**分布式账本技术**（DLT）与云计算的不同。即使 Google 表格跨越多个服务器，它仍然是中心化的，因为 Google 拥有这些服务器。区块链是去中心化的，意味着用户运行服务器。

###### 注意

**分布式账本技术**：区块链的心脏。它允许我们将所有交易同步，在一个分布式的计算机网络中。

明确地说：只有一个账本，但这个账本并不存储在任何单一的中央位置。相反，在每个节点上都有完全相同的副本——每一台计算机上都有一个副本。

再次比较图 2-3 和 2-4，以将此模型深植于你的脑海中。这是一件大事。分布式账本技术（DLT）是区块链的跳动心脏。

###### 注意

DLT 通常被定义为*分布式*账本技术，有时与区块链本身混淆。然而*分布式*仅指将相同的账本存储在不同的计算机上（如云计算）。

我们将 DLT 定义为*分布式*账本技术，以表明账本不仅分布式，而且不受任何中央权威的约束。维护账本的力量分散在各个节点之间。这种 DLT 的定义更准确地描述了“区块链的跳动心脏”。

分布式账本技术的显著之处在于，我们可以在世界任何地方保持所有这些分布式副本*同步*，同时每秒进行多次交易。（想想和朋友们安排午餐有多困难。）

而且，我们以一种可信、带时间戳和可审计的方式同步所有这些副本。让我们逐一解析这些术语：

+   分布式账本之所以*可信*，是因为它通过共识达成的（关于此点稍后会详细讨论），没有任何中央实体能够篡改数据。中心化的谷歌表格可能会被谷歌修改，但分布式账本不能被中央公司或机构修改。（就像互联网一样，没有单一组织“拥有”它。）

+   分布式账本通过创建*区块*进行*时间戳*——单一的数据记录，类似于我们会计账本上的条目——确保交易的适当顺序。记录交易时间 keeping the system safe and secure: when we pay someone in Ethereum at 12:02, we know when that Ethereum landed in the recipient’s wallet.

+   分布式账本之所以*可审计*，是因为它是透明的：就像谷歌表格一样，我们可以回顾过去，看到交易的全部序列。与真正匿名的现金不同，数字账本在我们每次交易时都会留下痕迹。各方仍然可以匿名，但他们的交易是在光天化日之下广播的。^(3)

话虽如此，DLT 对你合适吗？对于大多数企业技术管理者来说，共享中心化数据库是更好的解决方案：它更快、更便宜、更容易部署。当您需要在全球网络参与者之间共享“货币”（或价值单位）时，区块链技术才是更好的选择：换句话说，当您需要*分享财富*时。

DLT 是我们将价值流入价值互联网的方式，就像心脏将血液泵入身体一样。它是区块链背后的技术，是保持生态系统充满活力和健康的器官。

在以太坊推出后的接下来四年里，这颗心脏开始越来越快地跳动。然后一切爆发了。

# 节点和矿工

以太坊——和整个区块链市场一样——正在疯狂扩张。

因为人们可以在以太坊（平台）之上创建自己的代币，以太坊（资产）的价格开始飙升。2017 年初，一个 ETH 的价格是 10 美元；一年后，同一个 ETH 的价格是 1000 美元。

随着价格飞入以太空间，*矿工*（向网络贡献计算机的人）的数量也随之激增。这反过来又增加了网络容量，因此甚至更多的项目可以在以太坊上启动，为以太坊生态系统带来更多的收益。更多的人意味着更多的去中心化，这意味着更多的安全性（失败点更少），这使得网络价值更高。这是推动比特币早期增长的同一良性循环。

随着价格的飙升，节点数量也急剧增加，因为越来越多的人将他们的计算机连接到网络。这些节点发挥了几个关键作用：

维护账本副本

就像青少年在 Napster 上分享 NSYNC 专辑一样，许多节点托管账本，不断保持同步。因为账本随时间可能会变得相当大，所以有些节点只托管账本的一部分。

验证交易

通过共识过程（接下来介绍），节点不断就哪些交易区块是有效的达成“协议”，然后将有效的区块记录在区块链上（即向分布式账本写入带时间戳的区块数据）。

挖矿

广而言之，矿工是运行区块链网络的专用计算机，它们使用特殊硬件和软件获得新交易区块的比特币或其他数字资产作为奖励。用户搭建一个*挖矿机*（定制计算机）并向网络中托管节点获得奖励。^(4)

节点和*矿工*这个概念至关重要。在起步阶段，所有区块链都面临一个“鸡-蛋问题”：没有用户，你就不可能有区块链，但没有区块链，你也不能吸引用户。区块链不是中心化的：你不能仅仅启动一个服务器群。它是去中心化的：你必须说服用户构建网络。

那么你如何启动一个区块链？你需要挖矿。

###### 注

**挖矿**：让我们把定义从第一章扩展到包括通过向网络贡献计算能力来获得奖励（通常以硬币或代币的形式）的过程。

用户希望为参与你的区块链获得奖励：再次，这是对价值的认知。术语**挖矿**现在泛指任何为在网络中托管节点而获得的奖励。

这也是我们认为区块链是价值互联网的另一个原因：你的价值（你的数字资产，通常被称为*硬币*或*代币*）通常用来奖励参与网络的矿工。

这就是我们解决鸡-蛋问题的方法：我们付给鸡钱。

# 共识算法

> 我们拒绝：国王、总统和选举。我们信仰：粗略共识和运行代码。^(5)
> 
> —Dave Clark，互联网工程任务组

现在你理解到区块链使用的是分布式账本（一个巨大的共享数据库），它通过节点和矿工（一个全球网络）来维护，他们通过代币（你的自定义货币，或价值单位）来获得奖励。这就是区块链在现实生活中是如何构建的。

但是，当交易同时在全世界各地发生时，我们如何保持这一切同步呢？我们称之为*共识*。

共识（也称为**共识算法**，或**共识协议**）是所有节点就交易达成一致的过程。*我们并不是指人类手动就每笔交易达成一致*。恰恰相反：正如 Dave Clark 指出的，共识不是投票。共识是在幕后发生的，在代码中：机器与机器达成一致。

目前，共识有几种不同的形式，我们接下来会进行介绍。（如果这一节对你来说太过技术性，你可以略读斜体字句子，直接跳到第三章。）

###### 注意

**共识协议**：计算机用来自动“同意”彼此的算法。

## 工作量证明

*工作量证明*(*PoW*) 是比特币最初使用的共识协议。在这种方法中，计算机节点为验证交易（即，批准它们作为新数据块）解决日益复杂的数学问题。随着复杂性的增加，解决这些问题的计算能力也在增加。

提供计算能力的计算机不仅建造成本日益昂贵，运行成本也在日益增加：计算能力需要电力。这个想法是，这种具有挑战性的数学“工作”进一步证明了比特币的价值，因为它使用了真实的计算能力和真实的电力。

实际上，一个常见的批评是比特币使用了*太多*的电力。根据《经济学人》的报道，仅比特币网络使用的总能源消耗足以供电爱尔兰！^(6)这种巨大的能源消耗是区块链开发者正在尝试替代共识机制的原因。

在早期，任何拥有家用电脑的人都可以挖掘比特币。然后它发展成专门的挖掘机，然后是装满挖掘机的仓库，然后是位于便宜能源源附近的巨大服务器农场。随着个人矿工赚钱的竞争变得更加激烈，他们开始加入巨大的利润共享集体，或*挖掘池*。这些集体中的许多进一步合并成公司，现在控制着比特币网络的大部分。

共识是一件有趣的事情。随着竞争性挖掘公司之间的权力集中，我们最终得到了类似寡头垄断的局面，少数几个庞大的玩家控制着大部分挖掘力量：这正是去中心化网络试图解决的问题。

我们将这个问题称为**共识悖论**：一个去中心化的共识算法在变得更加广泛采用时，往往趋向于变得更加集中化。

###### 注

**共识悖论**：作为一种去中心化的共识机制，随着更广泛的应用，它趋向于变得更加集中化。

## 权益证明

工作量证明（Proof of Work，PoW）的最常见替代方案是*权益证明*（*Proof of Stake，PoS*），其中节点的挖矿能力与它们拥有的代币数量成比例。例如，在以太坊 2.0 中，^(7)，这是一个基于 PoS 构建的系统，如果有人拥有所有以太坊的 1%，那么这个人最多可以验证（或批准）所有交易的 1%。

###### 注

**权益证明**（**PoS**）：一种共识机制，用户必须证明他们在网络中的权益，才能验证（或挖矿）新代币。

权益证明的巨大优势在于它使用更少的电力：与其让每个人都为奖励而“竞争”，不如按代币所有权比例分配奖励。

然而，在这里我们再次遇到了共识悖论：在这种方案下，富者愈富，贫者愈贫。就像在《大富翁》游戏中开发了最值钱地产的玩家一样，最富有的代币持有者获得相对更多的收益。

权益证明（PoS）确实为参与者创造了一个巨大的激励机制，以确保系统的完整性：在 PoS 系统中，你拥有的区块链代币越多，你就越希望该区块链能够成功。没有人希望在赢得游戏的时候，《大富翁》游戏就提前结束。

## 实验性共识算法

共识悖论是区块链中最有趣的问题之一，因此有一系列新的共识算法正在开发中，例如委托权益证明、纠缠和哈希图。这是一个难题：如何让成千上万的独立节点持续保持一致？每个解决方案都有其自身的优点和缺点。

正如你所看到的，区块链提出了既技术性又金融性的挑战。以太坊在这两个方面都做得很好：一个好的共识协议（技术方面），以及对节点和矿工的内置激励（金融方面）。

我们看到，区块链——价值互联网——有很多组成部分。当我们构建区块链时，我们不仅仅是在构建一个技术系统；我们正在构建一个经济系统（见图 2-5）。

![区块链位于技术和经济交汇点。我们称它为“技经学”。](img/bcss_0207.jpg)

###### 图 2-5\. 区块链位于技术和经济交汇点。我们称它为“技经学”。

实际上，将区块链视为一个位于货币和技术交汇点的新学科是有帮助的。这需要新技能。传统的网络管理员不会理解如何创建经济激励，正如传统经济学家无法理解共识协议一样。

相反，我们鼓励企业区块链领导者开始学习“代币经济学”：设计代币化数字资产的艺术/科学。这将导致一个新的职位，即**Tokenomist**，他既了解经济原理，也了解区块链技术。在未来的就业市场上，Tokenomists—字面上和比喻上—都将印钞票。

###### 注意

**Tokenomist**：部分是经济学家，部分是区块链专家——起薪为每年 20 万美元（但你可以用代币支付）。

^(1) Vitalik Buterin，“以太坊白皮书：下一代智能合约和去中心化应用平台，”[Ethereum.org](http://Ethereum.org)，2013 年，*[*http://blockchainlab.com/pdf/Ethereum_white_paper-a_next_generation_smart_contract_and_decentralized_application_platform-vitalik-buterin.pdf*](http://blockchainlab.com/pdf/Ethereum_white_paper-a_next_generation_smart_contract_and_decentralized_application_platform-vitalik-buterin.pdf)*。

^(2) Rugbyowl，“那么以太坊这个名字是从哪里来的？”以太坊社区论坛，2014 年 3 月 20 日，*[*https://forum.ethereum.org/discussion/655/so-where-did-the-name-ethereum-come-from*](https://forum.ethereum.org/discussion/655/so-where-did-the-name-ethereum-come-from)*。

^(3) “加密货币洗钱是一个真正的威胁吗？”AML RightSource，2019 年 1 月 15 日，[*https://www.amlrightsource.com/news/posts/cryptocurrency-money-laundering-red-flags*](https://www.amlrightsource.com/news/posts/cryptocurrency-money-laundering-red-flags)。

^(4) 这进一步说明了我们为什么定义 DLT 为分布式账本技术。*分布式*仅指维护相同账本副本的节点。*去中心化*指的是也执行挖矿和验证交易的节点。

^(5) A. L. Russell，“‘Rough Consensus and Running Code’ and the Internet-OSI Standards War，”《IEEE 计算机历史期刊》28，第 3 期（2006 年）：48-61，[*https://doi.org/10.1109/mahc.2006.42*](https://doi.org/10.1109/mahc.2006.42)。

^(6) “为什么比特币消耗这么多能源，”《经济学人》，2018 年 7 月 9 日，*[*https://www.economist.com/the-economist-explains/2018/07/09/why-bitcoin-uses-so-much-energy*](https://www.economist.com/the-economist-explains/2018/07/09/why-bitcoin-uses-so-much-energy)*。

^(7) “Ethereum 2.0 规格，”GitHub，2019 年 9 月 3 日，*[*https://github.com/ethereum/eth2.0-specs*](https://github.com/ethereum/eth2.0-specs)*。
