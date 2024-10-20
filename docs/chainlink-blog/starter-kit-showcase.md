# Chainlink 开发者入门套件展示

> 原文：<https://blog.chain.link/starter-kit-showcase/>

我们很高兴地宣布 Chainlink 开发人员入门套件展示，这是一项以开发人员为中心的计划，将在整个五月进行。在接下来的一个月中，我们鼓励您尝试我们的[初学者工具包](https://docs.chain.link/docs/create-a-chainlinked-project)，或者通过构建使用 Chainlink [价格馈送](https://docs.chain.link/docs/using-chainlink-reference-contracts)、 [VRF](https://docs.chain.link/docs/chainlink-vrf) 或 [Any-API](https://docs.chain.link/docs/request-and-receive-data) 功能的智能合约，或者通过以某种方式或形式改进初学者工具包，并与社区共享您的项目。

## Chainlink 入门套件

[Chainlink 文档](https://docs.chain.link/)是学习如何构建利用 Chainlink 的工具和功能的[智能合约](https://chain.link/education/smart-contracts)的好地方，为开发人员提供了一种快速简单的方法，既可以将样板代码复制到他们的项目中，也可以使用在线 Solidity IDE[Remix](http://remix.ethereum.org/)部署示例代码片段。这些例子是简单的，独立的合同，演示了如何使用链接工具。然而，当创建一个需要其他东西的新项目时，它们并不总是理想的起点，比如测试、部署脚本，或者与项目的其他外链部分集成。开发人员希望有健壮的、文档完善的、最新的模板，他们可以轻松地在这些模板上进行构建。

Chainlink 初学者工具包是基于现有以太坊虚拟机(EVM)开发框架的开源项目，允许开发人员轻松地将 Chainlink 功能和工具集成到他们的项目中。每个初学者工具包都为开发人员提供了一个工作代码库，其中包含三个广泛使用的 Chainlink oracle 函数的简单而完整的版本:

*   [价格馈送](https://docs.chain.link/docs/using-chainlink-reference-contracts)
*   [任意 API](https://docs.chain.link/docs/request-and-receive-data)
*   [VRF](https://docs.chain.link/docs/chainlink-vrf) 的应用

除此之外，存储库包含部署和测试所有智能合同的脚本，为开发人员提供了一个合理的起点，让他们了解如何构建利用 Chainlink 产品的智能合同。每个存储库都基于现有的流行 Solidity 开发环境，如 [Truffle Suite](https://www.trufflesuite.com/truffle) 、 [Hardhat](https://hardhat.org/) 或 [Brownie](https://eth-brownie.readthedocs.io/en/stable/) ，其中 Truffle 和 Hardhat 专注于 JavaScript 和 TypeScript 编程语言，Brownie 专注于 Python。这三个开发环境都基于 Solidity/Ethereum 虚拟机开发，并通过使用本地网络为开发人员提供测试环境。Chainlink 初学者工具包可以在 [SmartContract GitHub 帐户](https://github.com/smartcontractkit)的顶部找到:

*   [Chainlink 安全帽入门套件](https://github.com/smartcontractkit/hardhat-starter-kit)
*   [Chainlink 布朗尼入门套件](https://github.com/smartcontractkit/chainlink-mix)
*   [Chainlink 松露启动套件](https://github.com/smartcontractkit/truffle-starter-kit)

![Chainlink Starter Kits](img/e10ee78df889a29e65014b639e4a588d.png)

<figcaption id="caption-attachment-1731" class="wp-caption-text">Chainlink Starter Kits pinned at the top of the SmartContract GitHub repository</figcaption>



## Chainlink 安全帽入门套件

[Hardhat](https://hardhat.org/) 是一个基于 JavaScript 和 TypeScript 的开发环境，供开发人员编译、部署、测试和调试与 [EVM 兼容的](https://ethereum.org/en/developers/docs/evm/)智能合约。它帮助开发人员管理和自动化重复任务，这些任务是简单的可重复功能，旨在提高生产率，减少开发、测试和部署生命周期中重复任务所花费的时间。

Hardhat 还配备了自己的本地开发网络，称为 [Hardhat Network](https://hardhat.org/hardhat-network/) ，专注于可靠性调试和额外的日志记录，并为开发人员提供了一个非常适合开发和精炼代码的本地开发环境。

我们的[Chainlink Hardhat Starter Kit](https://github.com/smartcontractkit/hardhat-starter-kit)是一个预打包的 hard hat 项目，它包含了在您的 Solidity 智能合约中实施、部署和测试 chain link 网络提供的主要功能所需的所有任务和智能合约。

查看关于[如何将 Chainlink 与 Hardhat 一起使用的博客文章](https://blog.chain.link/using-chainlink-with-hardhat/)，了解更多关于在 Hardhat 开发环境中使用 Chainlink 的不同 oracle 函数的详细信息和说明。

## Chainlink 布朗尼入门套件

Brownie 是一个基于 Python 的以太坊智能合约开发和测试框架。它为 Python 开发人员提供了一种在单个集成开发环境中维护智能合约、部署、脚本和测试的方法。

我们的[Chainlink Brownie Starter Kit](https://github.com/smartcontractkit/chainlink-mix)是一个预烘焙的 Brownie 组合，包含在 Python 环境中处理和使用 chain link 智能合约所需的所有合约和脚本。它还支持本地开发环境，以及网络分叉。

查看我们关于使用 Python 开发 DeFi 项目的博文[,了解更多信息和使用 Chainlink Brownie 初学者工具包构建利用 Chainlink oracles 的 dApp 的真实示例。](https://blog.chain.link/develop-python-defi-project/)

## Chainlink 松露初学者工具包

Truffle Suite 是一个以太坊的开发环境、测试框架和资产管道，旨在让以太坊开发者的生活更加轻松。它通过为开发人员提供内置的智能合同编译和部署、使用[摩卡](https://mochajs.org/)和[柴](http://chaijs.com/)的自动化合同测试，以及可脚本化的部署和迁移框架来实现这一点。Truffle 还提供可配置的网络管理，用于部署到各种公共和私有网络。

我们的[Chainlink Truffle Starter Kit](https://github.com/smartcontractkit/truffle-starter-kit)允许您在公共以太坊网络以及集成本地网络(如 [Ganache](https://github.com/trufflesuite/ganache) )上轻松开发、部署和测试 chain link 驱动的智能合约。

查看我们关于[如何使用 Chainlink with Truffle](https://blog.chain.link/how-to-use-chainlink-with-truffle-2/) 的博客文章，获得更深入的使用 Chainlink Truffle 初学者工具包的指南。

## 初学者工具包展示

初学者工具包展示是一项将在未来几周内进行的活动，旨在为开发人员提供一个试验我们的初学者工具包的机会。

我们鼓励开发人员从三个初学者工具包中选择一个，然后通过执行下列操作之一进行试验:

*   克隆存储库，然后实现您在 Solidity smart 契约中的想法或概念，该契约利用了 Chainlink 工具或功能
*   派生存储库，然后在一个新的代码分支中改进或扩展初学者工具包，然后创建一个 [pull 请求](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests#:~:text=Pull%20requests%20let%20you%20tell,merged%20into%20the%20base%20branch.)来评审您的改进，并可能合并回主代码库

使用初学者工具包实现想法或概念的一些示例:

*   组合多个链链接价格馈送，以基于两个馈送创建新的价格对
*   将智能合约连接到您使用 Any-API 功能构建的外部适配器
*   使用 Chainlink VRF 在奖池智能合约中随机选择获奖者
*   [创造一个具有可验证随机特征的 NFT](https://blog.chain.link/random-numbers-nft-erc721/)
*   扩展或改进初学者工具包中的测试
*   将[持续集成(CI)](https://en.wikipedia.org/wiki/Continuous_integration) 实施到其中一个入门套件中
*   实现要使用的类型脚本，而不是现有的 JavaScript 版本

使用初学者工具包的现有项目的一些示例:

*   [NFT 混合](https://github.com/PatrickAlphaC/nft-mix)，使用布朗尼初学者工具包
*   [永远不要使用安全帽入门套件打两次](https://github.com/tina1998612/Never.Fight.Twice)
*   [参数作物保险，](https://github.com/pappas999/Parametric-Crop-Insurance)使用块菌入门套件

在接下来的几周里，我们将展示每个初学者工具包，并介绍每个工具包提供的特性和功能。

## 炫耀你的作品

一旦你用一套工具实现了你的想法或者改进了一套工具，向全世界展示你的工作！为了展示你的例子，确保你已经将它登记到一个公共存储库中，并在 Twitter 上用标签`#StarterKitShowcase`分享它的链接，或者在 [Chainlink Discord](https://discord.com/invite/aSK4zew) 的`#starter-kit-showcase`频道中分享你的存储库。

大约一个月后，我们将举办一个直播，在那里我们将看一些分享的示例，我们还将邀请一些贡献者加入直播，谈论他们的项目和他们使用初学者工具包的体验。

因此，请务必查看固定在 [Chainlink 公共存储库](https://github.com/smartcontractkit)上的初学者工具包，并开始试验。一如既往，我们迫不及待地想看看你的建设！