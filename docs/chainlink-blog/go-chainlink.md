# 加油链环！

> 原文：<https://blog.chain.link/go-chainlink/>

我们相信区块链技术是许多应用程序的基础。Oracles 是上述区块链的中间件，是连接现有软件和支持未来用例的关键组件。Chainlink 将成为中间件，作为区块链分散式 oracle 网络。

这是一个快速的帖子，看看我们在构建 Chainlink 节点时所做的一些技术设计决策，以及对我们将如何继续开发的一点见解。如果你对 Chainlink 的技术方面感兴趣，我鼓励你[查看 Github 项目](http://github.com/smartcontractkit/chainlink)或[在 Gitter](http://gitter.im/smartcontractkit-chainlink/Lobby) 上联系我们。

规划时的一个重要考虑是让人们能够在尽可能多的地方运行 Chainlink。Chainlink 的一个重要原则是输入的多样性。我们想让 Chainlink 节点运行起来负担得起，并且易于安装，这样全世界的人都可以在他们选择的任何计算平台上运行。因此，让它可访问，并且在不损害安全性或开发人员生产力的情况下这样做。

进入 Golang。在比特币的 genesis block 开启“区块链”不到一年后，Go 编程语言被介绍给了世界。从那以后，它经历了飞速的发展，为今天开发人员所依赖的许多工具提供了动力。Go 通过在可用性和安全性之间找到平衡点来实现这个目标:[简单性](https://talks.golang.org/2015/simplicity-is-complicated.slide#1)。

Golang 专注于几个关键特性，优化它们的长期稳定性，然后在它们的基础上构建令人惊叹的工具。例如，并发性是现成的，非常适合分布式系统。最重要的是，Go 的工具提供了交叉编译，允许应用程序在任何设备上本地运行。这有助于我们保持较低的内存占用，当您考虑运行一个节点的成本，以及这对世界上许多人运行 Chainlink 的能力有何影响时，这一点非常重要。

此外，Go 还有一个蓬勃发展的开发者社区。不是一般的开发商，是区块链的开发商。[以太坊](https://github.com/ethereum/go-ethereum)、[比特币](https://github.com/btcsuite/btcd)、[IPFS](https://github.com/ipfs/go-ipfs)……你最喜欢的不可信分布式系统，可能已经有一个欣欣向荣的围棋社区了。

因此，我们在 Golang 中使用嵌入式数据库和无依赖关系从头开始构建节点，使节点的安装像下载和运行二进制文件一样简单。Chainlink 节点提供了一个[可组合管道](https://github.com/smartcontractkit/chainlink/wiki/Job-Pipeline)，这是一个[易于扩展的](https://github.com/smartcontractkit/chainlink/wiki/External-Adapters)，因此任何应用程序开发人员都可以轻松地连接到 Chainlink 并与区块链可靠地交互。例如，一旦一个应用程序被连接，Chainlink 通过监控和修改交易费用来确保该应用程序发出的交易得到确认。

此外，Chainlink 已经从 Golang 区块链社区中受益匪浅。通过使用 Geth，我们能够利用部署最广泛的以太坊版本，并依靠已经确保数百亿美元安全的相同标准。

Chainlink 的社区对其未来至关重要。同样，一个稳定的安全节点将是链式网络的基石。除了开放与社区协作的代码，我们还决定向更大的社区开放我们的内部开发流程，向公众开放我们团队的 [Pivotal Tracker](https://www.pivotaltracker.com/n/projects/2129823) 。自 2014 年以来，我们一直将[敏捷流程](http://agilemanifesto.org/)应用于复杂智能合同的开发，并认为这是快速改善分散基础设施以满足用户不断变化的需求的正确方法。

如果你对 Chainlink 的未来发展感兴趣，你可以关注 Github 的进展，看看我们目前正在开发的的[功能。我们重视各种规模的贡献，包括问题、拉动请求和新问题，其中一些我们已经开始标记为适合首次使用 ChainLink 的](https://www.pivotaltracker.com/n/projects/2129823)的[。如果您有兴趣在这方面帮助我们，请随意开始处理](https://github.com/smartcontractkit/chainlink/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)[问题](https://github.com/smartcontractkit/chainlink/issues)、[打开拉动请求](https://github.com/smartcontractkit/chainlink/pulls)，或者[联系 Gitter](http://gitter.im/smartcontractkit-chainlink/Lobby) 。