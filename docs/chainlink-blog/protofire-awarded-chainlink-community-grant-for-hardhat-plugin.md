# Protofire 收到了 Chainlink 社区的资助，来建造一个可以旋转本地 Chainlink 节点的安全帽插件

> 原文：<https://blog.chain.link/protofire-awarded-chainlink-community-grant-for-hardhat-plugin/>

[chain link 社区资助计划](https://chain.link/community/grants) 的主要目标之一是通过使用 [混合智能契约](https://blog.chain.link/hybrid-smart-contracts-explained/) 和 [Chainlink 甲骨文](https://blog.chain.link/what-is-chainlink/) 让构建影响世界的应用变得更加容易，从而为全球开发者社区提供支持。为了推进这一目标，该计划从财务上支持开发人员工具的创建，以无缝创建、测试混合智能合同并将其投入生产，并为其持续维护提供资金，确保其保持功能性和安全性。

为了在以太坊上集成 Chainlink 信任最小化服务，开发人员需要与 Chainlink 节点交互以创建作业，托管一个 [外部适配器](https://docs.chain.link/docs/external-adapters/) ，或者解决一个问题。虽然开发人员可以将 Chainlink 节点托管给第三方，但是难度和所需的时间会减缓开发过程。需要一种解决方案，通过使开发者能够在单个步骤中旋转本地 Chainlink 节点来简化该过程。

为了支持这一目标，我们很高兴地宣布[Protofire](https://protofire.io/)[【区块链】](https://blog.chain.link/what-is-blockchain/) 开发服务的提供商已经获得了 Chainlink 社区的资助，用于开发一个 Hardhat 插件，该插件将允许开发人员通过一个命令来启动本地 Chainlink 节点。该插件将使以太坊开发者能够使用 Chainlink Any API 更轻松地开发和测试智能合约，帮助他们将外部数据无缝集成到他们的分散应用程序中。

该插件将使用 Hardhat 插件安装和使用模式，被添加到 Hardhat 配置中，并通过 NPM 分发。通过合并 Chainlink 节点的所有主要功能——在启动时打印出必要的集成信息并使节点易于更新——开发人员将能够更轻松地编写和测试一系列不同 [用例](https://chain.link/use-cases) 的智能合约。

作为资助的一部分，Protofire 将在插件开发过程中完成几个步骤，包括:

*   使用 Docker 创建一个包含现有的 Chainlink docker、Postgres 数据库容器和键配置的组合。
*   创建一个 Hardhat 插件结构，开发主要功能，以便开发者可以通过命令行与 Chainlink 节点进行交互。
*   完成端到端测试，帮助确保插件的可靠性和性能。
*   在 GitHub 上制作书面文档，向用户展示如何设置环境、编写智能合同以在本地使用 [Chainlink 数据馈送](https://data.chain.link/) 、创建工作、为帐户提供资金等等。

通过简化启动本地 Chainlink 节点的过程，该插件将鼓励更多开发人员使用 Chainlink 服务构建解决方案，并加快测试和迭代智能合约应用程序的开发周期。此外，它还将消除依赖第三方提供商和基础设施构建节点的需要，从而节省开发人员的宝贵时间。最终，该插件将使开发人员能够启动新项目，试验新用例，并在 [Web3](https://chain.link/education/web3) 领域推动创新。

[Hardhat](https://hardhat.org/) 是一个本地以太坊开发环境，帮助开发者运行测试、调试 Solidity 代码、与智能合约交互。有了 Hardhat，开发人员可以使用一个简单的命令来启动本地 EVM 环境。现在，有了这个插件，开发者可以轻松地启动一个本地链接节点。

Protofire 是区块链技术、构建分散式协议、[](https://chain.link/education/smart-contracts)、应用程序和开发工具(SDK/API)的公认开发服务和咨询提供商。久经考验的区块链专家团队为众多领先的 Web3 项目贡献了他们的开发资源，包括 Armanino、Filecoin、Gnosis、The Graph、Maker、Tezos、0x、Kyber Network 和 Synthetix。Protofire 还收到并成功完成了多个 Chainlink 社区资助项目，如[【xDai】](https://blog.chain.link/protofire-receives-a-chainlink-community-grant-for-an-integration-with-xdai/)[雪崩](https://blog.chain.link/protofire-receives-a-grant-for-native-integration-of-chainlink-on-avalanche/)[Celo](https://blog.chain.link/celo-chainlink-grant-protofire/)[io tex](https://blog.chain.link/iotex-protofire-chainlink-grant/)和[Plasm](https://blog.chain.link/protofire-receives-a-grant-to-natively-integrate-chainlink-on-plasm-and-shiden/)鉴于他们在 Chainlink 和 EVM 环境中丰富的经验和被证明的成功，Protofire 是构建无缝旋转 Chainlink 节点的 Hardhat 插件的合适人选。

Protofire 的工程总监 Christian Malfesi 说:“我们很高兴能够获得社区拨款来开发一个 Hardhat 插件，使以太坊开发者能够在他们的本地机器上快速启动 Chainlink 节点。“通过让智能合约开发人员更容易在本地测试他们的 Chainlink Any API 集成，我们可以帮助开发人员使用来自网络的任何数据更快地开发和测试应用程序。最终，该插件使开发人员能够更无缝地利用外部数据来实现高级用例，推动 Web3 空间向前发展。”

通过社区资助计划，Chainlink 继续支持研发关键工具和基础设施的创新团队、学者和社会影响项目，以加快混合智能合同、安全 oracle 网络和尖端技术的采用，从而创造一个更加经济公平的世界。

## 关于 Chainlink 赠款计划

如果您想了解更多关于 Chainlink 社区资助计划的信息，请查看我们的 [博客帖子](https://blog.chain.link/introducing-the-chainlink-community-grant-program/) ，该帖子进一步阐述了该计划的目标和提交标准。我们鼓励有才华的个人开发者和开发团队 [在这里](https://chainlinkgrants.typeform.com/to/efEbsq) 申请资助计划，或者如果你是一名研究人员并且想要合作， [联系我们](/cdn-cgi/l/email-protection#61130412040013020921020900080f0d080f0a0d0003124f020e0c) 。