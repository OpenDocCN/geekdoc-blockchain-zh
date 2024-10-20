# 如何成为一名聪明的合同开发者

> 原文：<https://blog.chain.link/how-to-become-a-smart-contract-developer/>

目前有许多因素使智能合同开发人员成为一个有吸引力的职业前景，从与对世界产生变革性影响的技术合作的机会到人才市场对智能合同开发人员的巨大需求。

此外，智能合同开发技能正变得越来越重要。20 世纪 90 年代，工程师们从大型机的封闭世界转移到互联网的开放数据库，随着 [智能合约](https://chain.link/education/smart-contracts) 的引入，类似的转变正在发生。正如那时开发人员过渡到与未来更相关的技术堆栈一样，现在开发人员正在向 Web 3.0 堆栈转移。

有抱负的智能合约开发人员必然会对如何实现这种转变有许多疑问:什么是 Web 3.0 开发人员堆栈？应该学习哪些编码语言？需要什么样的技术技能，你如何学习这些技能？下面，您将找到这些问题以及更多问题的答案，引导您进入智能合同开发的世界。

## 区块链语言

区块链智能合约的主要语言是[](https://docs.soliditylang.org/en/latest/index.html#getting-started)，以 [Vyper](https://vyper.readthedocs.io/en/stable/) 为主要竞争对手。与 Python 等解释型语言不同，Solidity 是静态类型化的(变量类型是声明的)并且是编译的，这意味着你需要在运行之前生成一个二进制文件。Solidity 是 Gavin Wood 为解决 2014 年面临的独特问题 [以太坊](https://ethereum.github.io/yellowpaper/paper.pdf) 而开发的语言，它现在是所有以太坊虚拟机(EVM)兼容链的默认语言。这意味着，无论你是在以太坊、雪崩、多边形、币安智能链(BSC)还是任何其他 EVM 链上开发，你都需要了解坚固性的来龙去脉。但是，有些链不使用 EVM，而是用不同的语言编程。Solana 是一个不使用 Solidity，而是使用 Rust 和 C/C++的区块链的例子。

那么，你如何选择一个区块链来发展呢？考虑因素很多，没有一刀切的答案。以太坊是目前大多数 dApps 存在的地方，它通常具有最大的流动性。此外，以太坊悠久的历史赋予了它可靠的声誉。如果速度和低成本不是你的主要考虑因素，并且你有生态系统需求(例如，你想与之交互的 dApp 只在以太坊上)，以太坊是一个强有力的选择。

您还可以部署在一个扩展层(L2)上，如 Arbitrum，它具有完全的 EVM 兼容性，但将事务“汇总”到压缩包中，因此事务吞吐量更高，这意味着成本更低，速度更快。至于其他的 EVM 链，每一个都提供了某种形式的超越以太坊的可伸缩性改进；BSC 使用更大的事务块，Polygon 是一个侧链，它为了扩展而牺牲了一些去中心化，而 Avalanche 使用新的一致算法来提高其事务速度/成本。

由于这篇文章的缘故，我们将集中讨论通过坚固性的 EVM 链，因为这是最常见的选择。

## 技术技能

编译的、相对低级的后端语言，如 C/C++为进入 Solidity 编程提供了一个强有力的入口。那些具有 web 开发背景或 JavaScript 和 Python 等语言经验的人将需要适应较低层次的可靠性思维模式，在这种思维模式下，您可能会发现自己直接对变量的位进行操作。然而，一个全栈区块链程序员会希望拥有这两种技能，因为大多数与 Solidity smart contracts 的接口都是通过 web3.js、ethers.js 和 web3.py 库完成的。一个好的开发人员可以处理 JS/Python 中的后端可靠性契约或前端——但是一个优秀的开发人员可以处理整个堆栈。 [OpenZeppelin 契约库](https://openzeppelin.com/contracts/) 也是一个很好的来源，因为它节省了开发人员编写一些常见契约的麻烦，比如令牌契约。

或许最需要培养的技能是安全。你的智能合同有一天可能会处理数十亿美元的价值，所以它没有缺陷是最重要的。像 [重入](https://solidity-by-example.org/hacks/re-entrancy/) 这样的漏洞在智能合约中是需要重点考虑的。由于智能合约经常调用其他智能合约函数，因此其他函数可能会中断您的智能合约流。这就是著名的 7000 万美元 ETH DAO 黑客事件的起因。安全思维对于智能合约开发人员来说至关重要。

那么这些合同的开发流程是什么样的呢？有没有工具和 ide 可以帮助我们？当然啦！一个流行的 IDE 是 [Remix](https://remix.ethereum.org/) ，这是一个基于 web 的 IDE，可以处理您的合同的编译及其在您选择的链上的部署。此外， [松露](https://www.trufflesuite.com/) 和 [布朗尼](https://github.com/eth-brownie/brownie) 是两个也是为了辅助你而构建的开发框架。为了从头到尾了解更多的过程，包括如何使用这些框架，我们强烈建议查看 Chainlink Labs 的首席开发人员 Patrick Collins 通过 freeCodeCamp 提供的极其全面的智能合同课程: [可靠性、区块链和智能合同课程——初学者到专家 Python 教程](https://www.youtube.com/watch?v=M576WGiDBdQ) 。

[https://www.youtube.com/embed/M576WGiDBdQ?feature=oembed](https://www.youtube.com/embed/M576WGiDBdQ?feature=oembed)

*   坚固度
*   JavaScript
*   Python
*   web3.js/web3.py
*   ethers.js
*   松露
*   布朗尼
*   混音

## 社区

社区在智能合同领域极其重要。如此多的创新发生得如此之快，你自己很难跟上。这就是为什么最优秀的开发人员积极地在 Twitter 上建立联系，参加黑客马拉松来会见其他开发人员和潜在的投资者或雇主，拿起 [Gitcoin](https://gitcoin.co/) 奖金来帮助开源开发，参加诸如 [智能合同研究论坛](https://www.smartcontractresearch.org/) 之类的深思熟虑的论坛，并就不一致之处进行聊天来学习和帮助他人学习。    黑客马拉松是培养你聪明的合同技巧的一个特别好的地方。在黑客马拉松上，您可以边做边学，并在构建过程中实时磨砺您的才能，同时业内受人尊敬的成员会帮助指导您——甚至可能成为您项目的合作者！[chain link 2021 年秋季黑客马拉松](https://chain.link/hackathon) 是一个开始建设的好地方。总奖金为 55 万美元，有领先的专家和风投出席，还有成千上万的开发人员会面，这对智能合约开发人员的职业生涯来说是一个巨大的推动。另一个很棒的资源是[chain link Discord](https://discord.gg/2YHSAey)，开发者拥护者和热情的社区成员可以帮助你开始。T34
T36】

## 去哪里学

有大量的资源可以支持你的学习，从黑客马拉松到博客到 Discord 服务器到 YouTube 频道等等。我们选择了八种资源，为那些希望成为智能合同开发人员的人提供了一个极好的组合，下面是每个资源领域的顶级资源。

1.  [可靠性、区块链、智能合约课程——初级到专家 Python 教程](https://www.youtube.com/watch?v=M576WGiDBdQ)
2.  [](https://cryptozombies.io/)
3.  [](https://www.chainshot.com/)
4.  [链接 YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)
5.  [链结博客](https://blog.chain.link/)
6.  [链环不和](https://discord.gg/2YHSAey)
7.  [Ethereum.org](https://ethereum.org/en/)
8.  [康森斯训练营](https://consensys.net/academy/bootcamp/)

### YouTube

如果你是一名视觉学习者，喜欢有人带你看教程，而不是自己一个人看，YouTube 是一个很好的资源。这些 YouTubers 都为学习智能合同开发的人提供了优秀的材料，提供了详细的教程供您遵循，以支持您的学习。

1.  [Dapp 大学](https://www.youtube.com/channel/UCY0xL8V6NzzFcwzHCgB8orQ)
2.  [伊万上理工T3】](https://academy.ivanontech.com/)
3.  [吃积木](https://www.youtube.com/channel/UCZM8XQjNOyG2ElPpEUtNasA)
4.  [](https://www.youtube.com/channel/UCn-3f8tw_E1jZvhuHatROwA)
5.  [奥斯格里菲斯](https://www.youtube.com/channel/UC_HI2i2peo1A-STdG22GFsA)
6.  [纳德达比特T3】](https://www.youtube.com/user/boyindasouth)

### 社区

在智能合同领域，加入社区至关重要。向更有经验的人学习，交朋友，帮助那些会反过来帮助你的人。Discord 和 Reddit 社区是获得实时帮助和扩大与其他志同道合的开发人员的社交圈的强大资源。这里有一些空间，将有助于您的智能合同开发之旅。

1.  [链环不和](https://discord.gg/2YHSAey)
2.  [安全帽不和](https://discord.com/invite/TETZs2KK4k)
3.  [](https://consensys.net/blog/news/say-hello-to-the-consensys-discord/)
4.  [布朗尼不和](https://discord.gg/9zk7snTfWe)
5.  [以太坊不和](https://ethereum.org/en/)
6.  [Reddit ethdev](https://www.reddit.com/r/ethdev/)

### 黑客马拉松

黑客马拉松是加速开发者之旅的一种令人兴奋的方式。在新技术的前沿发展的同时挑战你的极限，同时著名的社区领袖在那里提供建议，投资者正在寻找下一个大项目——这可能就是你的。Chainlink Hackathon 是一个很好的起点，提供了大量的资源、研讨会、奖品和社交机会。

1.  [链式黑客特逊T3](https://chain.link/hackathon)
2.  [ETH Global](https://ethglobal.co/)
3.  [ETH IndiaT3】](https://twitter.com/ETHIndiaco)

## 迈出智能合同之旅的第一步

成为一名聪明的合同开发者有很多途径。我们列出了一些选项，但您可以选择最适合自己的选项。最重要的是你开始做，做一些有趣的东西，开始探索，开始问问题——剩下的事情会随之而来。无论您是后端开发人员、web 开发人员，还是开发工作的新手，都有一条通往成功的道路，并且有很多人乐于提供帮助。所以，迈出第一步:加入讨论，阅读教程，加入黑客马拉松，开始构建令人兴奋的 Web 3.0 未来。

在构建安全、功能丰富的 dApps 时，Chainlink 成熟的 oracle 基础设施为开发人员开启了无数可能性。 了解更多关于 Chainlink 的信息，请访问[chain . link](https://chain.link/)，订阅 [Chainlink 简讯](https://chn.lk/newsletter) ，并在 Twitter 上关注[@ chain link](http://www.twitter.com/chainlink)。要了解 Chainlink 网络的完整愿景，请阅读 [the Chainlink 2.0 白皮书](https://chain.link/whitepaper) 。