# Chainlink，概述和我们的关注点

> 原文：<https://blog.chain.link/chainlink-an-overview-and-our-focus/>

首先，我们要感谢所有为 Chainlink 的成功付出个人时间、努力和加密货币的人。我和我们的整个团队对我们和我们的社区在解决 smart contract 连接问题方面所获得的支持深表感谢。

## 定义智能合约连接问题

[智能合同](https://chain.link/education/smart-contracts)是一种数字协议，通过在以太坊等分散节点网络上运行，该协议已被防篡改；创造一种更值得信赖的，因此也是更高级的数字协议。

**智能合约连接问题，**智能合约无法与任何外部数据馈送或在执行智能合约本身的节点网络之外运行的另一资源进行交互。

![Smart contracts are currently unable to connect with relevant external events, APIs, and/or payment methods.](img/20b1038955f4f0b50427e9891822b540.png)

<figcaption id="caption-attachment-399" class="wp-caption-text">Smart contracts are currently unable to connect with relevant external events, APIs, and/or payment methods.</figcaption>



由于围绕区块链交易达成共识的方法，这种外部连接的缺乏是所有智能合约网络所固有的，因此将是所有智能合约网络的持续问题。

缺乏与外部资源的连接对智能合约开发人员今天所能构建的内容造成了很大的限制。没有关键输入，如证明性能的数据馈送(保险的物联网、证券的市场价格、装运的 GPS 等..)，或者关键输出(被广泛接受的银行支付)，构建智能合约变得很困难，智能合约具有我们期望从一个制作良好的 web/移动应用程序中获得的功能。如果我们研究像优步这样成功的应用程序的构建方式，我们会看到应用程序的核心代码使用了关键输入(GPS 数据)和关键输出(SMS 和支付)的组合。如果我们试图构建一个像优步一样的应用程序，而不能访问这些关键的构建模块，除了高度复杂的应用程序本身，我们还必须自己构建输入/输出。制作一个好的应用程序所依赖的所有构件是许多公司的工作；提供精确的 GPS 数据(谷歌)、与电信对接短信(Twilio)以及提供可用的银行间支付(Stripe)，这些都是关键的组成部分，而不是依赖它们来开发工作应用的公司所构建的。我们认为，智能合约开发人员能够轻松访问他们的分散式应用程序的类似有用构件，这是创建越来越有用的智能合约所必需的。

## 解决方案是一个安全的区块链中间件

幸运的是，智能契约所需的许多输入和输出已经以 web/移动应用程序使用的数据馈送和 API 的形式存在。我们需要解决的问题是智能合约与这些外部资源连接的能力，以便为最终用户保留智能合约的价值；值得信赖的防篡改数字协议。现在应该有一种安全、分散和防篡改的方式来触发与外部事件/数据的智能合同，同时还发送关键的支付输出。

![Chainlink will provide the building blocks needed to build complex & high-value smart contracts.](img/3fe0c1f1af341969b964d5f27a2fbd4e.png)

<figcaption id="caption-attachment-400" class="wp-caption-text">Chainlink will provide the building blocks needed to build complex & high-value smart contracts.</figcaption>



Chainlink 提供了一个安全、分散的防篡改“区块链中间件”，同时也是一种访问复杂智能合约所需的多个输入和输出的简单方法。通过大大简化智能合约安全访问关键链外资源的方式，Chainlink 加速了日益有用的智能合约的开发。

有关我们方法的详细信息，请查看我们的[白皮书](https://link.smartcontract.com/whitepaper)，以及我们来自[敌无双 3](https://www.youtube.com/watch?v=kW27zYIxZhY&feature=youtu.be&t=28s) 、[SF 以太坊会议](https://www.youtube.com/watch?v=nMlpTgxKtAY)和 [SIBOS](https://create.smartcontract.com/sibos17) 的演讲。

## 支持 Chainlink 网络的重点领域

#### **在 Go 中构建 Chainlink 的改进参考实现**

我们目前专注于构建 Chainlink 的改进参考实现，这是我们在[白皮书](https://link.smartcontract.com/whitepaper)中描述的广泛功能的基础。我们已经决定在 Go 中编写这个改进的主要实现，因为它的安全性、可伸缩性，以及不断增长的开发者社区将 Go 应用于加密用例，例如以太坊流行的 Geth 客户端。我们的计划是 2018 年在 Q1 发布 Go Chainlink 的初步简化实现，届时我们计划与更大的开源社区积极合作，改进和保护它，使其为 mainnet 上的活跃用户做好准备。

我们已经聘用并将继续聘用 Go 开发人员和活跃的面向细节的开发人员，他们希望解决智能合约领域的复杂问题，愿意学习像 Go 或 know solidity 这样的新语言，并对 Chainlink Core 的开源代码(MIT 许可证)感兴趣。如果你对我们正在解决的问题感兴趣，我们正在积极地通过我们的 [Gitter](https://gitter.im/smartcontractkit-chainlink/Lobby) 与熟悉我们 [Github](https://github.com/smartcontractkit) 的开发者会面。

## 创造了一个巨大的网络直接有用的链环

我们目前有超过 19，000 人告诉我们，他们想成为[链节运营商](https://blog.chain.link/what-is-a-chainlink-node-operator/)；即使这个庞大的初始群体的转换率很低，我们预计我们将能够拥有足够多的独立节点运营商，以提供一个完全分散的[甲骨文](https://chain.link/education/blockchain-oracles)网络。我们很高兴地说，拥有一个由活跃的 Chainlink 节点运营商组成的大型生态系统似乎是我们目前正在努力实现的目标。

除了运行每个独立节点的 Chainlink 节点操作符之外，在我们的社区中还有多个开发人员编写代码，将一个 Chainlink 连接到一个特定的链外资源/API。通过最少的代码，任何 API 的特定请求/响应都可以成为一个链接，安全地与各种网络上的请求契约进行接口。我们已经使用任何语言编写 Chainlink 适配器变得很容易，并且知道核心/适配器模型对于围绕 web APIs 和 SWIFT 支付报文等企业标准制作 chain link 非常有效。如果您是一名开发人员，希望在领先的网络(如以太坊)上让智能合约访问您熟悉的 API，我们可以让您轻松地同时访问多个合约。如果你需要帮助建立一个链接，请发送电子邮件[【电子邮件保护】](/cdn-cgi/l/email-protection)，或者与我们和其他已经在我们的 [Gitter](https://gitter.im/smartcontractkit-chainlink/Lobby) 上建立链接的开发者聊天。

## Chainlink 在智能合约生态系统中的角色

#### 使智能合约开发人员能够构建更好的应用程序

我们目前正与多个智能合同开发团队合作，将 ChainLink 用作[一种向他们自己的合同添加外部数据的方式，和/或供他们自己的平台上生成的合同使用](https://blog.zeppelinos.org/chainlink-partnership/)。我们很高兴与这些优秀的团队合作，并且很高兴看到他们使用 Chainlink 作为智能合同连接问题的解决方案。我们还积极会见智能合同开发商、fintechs、insurtechs 和其他各种初创公司，尽最大努力帮助他们开发下一代令人兴奋的新型分散式应用。我们还与更大的技术团队合作，将智能合同应用到现有公司的后端，以及在私有网络中构建智能合同的团队。这些较大的团队通常受益于 Chainlink 的能力，该能力使用链外计算来帮助保持关键交易数据的私密性，将他们的合同连接到他们已经依赖的数据馈送，使用他们现有的支付方法实现支付，并允许他们当前的后台办公系统更容易地与智能合同连接。我们将继续努力寻找最佳方式[将大型现有系统及其底层标准连接到智能合同](https://create.smartcontract.com/sibos17)，并渴望帮助更大的技术团队将其现有系统连接到各种合同，使用他们依赖的标准进行关键操作，如支付，如 SWIFT 报文。

由于我们与敏捷智能合同开发团队、支付网络、银行和金融机构的持续合作，我们正在使 Chainlink 对各种规模的技术团队都有用。如果您正在处理一个需要外部输入/输出的智能合同，我们随时可以提供帮助，请随时发送电子邮件至 [【电子邮件保护】](/cdn-cgi/l/email-protection#c3b0b6b3b3acb1b783b0aea2b1b7a0acadb7b1a2a0b7eda0acae) ，或[注册联系](https://chainlink.typeform.com/to/CTSrCg)，了解我们如何帮助您快速将智能合同连接到关键的链外资源。

#### 提供对数据、支付和许多其他 API 服务的访问

我们相信，智能合约和基于区块链的网络有望超越通过现有互联网交易的总价值。如果以智能合约形式出现的基于区块链的逻辑真的成为交易大量价值的方法，这种新形式的数字协议将需要数据输入、支付输出和各种其他 API 服务，就像今天集中运行的 web 应用程序一样。随着这种新基础设施的出现，使广泛使用的智能合同取得成功的数据、支付和各种其他基于 API 的服务将处于优越的竞争地位。看看历史上的一个例子，如 PayPal，由于它在 Ebay 的 P2P 电子商务 web 应用程序(一组集中运行的数字协议)中的使用，它成为一种广泛使用的互联网支付服务；我们认为，作为一项由广泛使用的合同使用的服务，它建立在这个新形成的基础设施上，可能会成为其他合同在这个新出现的基础设施上更广泛采用的转折点。

一个成功的应用程序的关键构建模块被广泛复制的动态，实际上在智能合约中比传统的软件、web 或移动开发更加普遍。智能合同代码的公共性质，以及合同的“复制粘贴”性质，使得成功使用的智能合同被广泛复制的情况屡见不鲜。今天流行的令牌合约就是一个很好的例子，许多令牌合约来自于[Open zeplin](https://openzeppelin.org/)的代码，然后由于其他人最初的成功实现而被广泛复制。这种动态意味着，如果数据、支付或任何其他服务被用作高度成功的智能合同的关键组成部分，则该关键输入/输出很可能会与合同的其余部分一起被复制。这种动态为实现高度成功的合同的服务提供了巨大的机会；成功合同的大规模复制会导致对该合同至关重要的任何 API 服务在所有复制的合同以及这些合同的后续副本中迅速获得市场领先的使用量。

现在有很大的机会成为非常成功的智能合约/分散式应用程序正常运行所依赖的关键在线服务，为 API 的提供商带来大量数据和更广泛的使用。我们目前正在与多家数据提供商、支付网络和各种 API 服务合作，我们正在积极推动这些服务成为下一个高度成功的智能合同的关键构建模块。如果你有想要卖给智能合约的数据馈送、支付和/或 API，我们会让这个过程容易实现；请随时发送电子邮件至[【电子邮件保护】](/cdn-cgi/l/email-protection)，或[注册联系](https://chainlink.typeform.com/to/CTSrCg)关于您的 API。

## 推动智能合同的发展

我们的整个团队，以及我们有幸吸引到的更大的社区，都致力于将智能合同推进到他们发展的下一步。我们坚信，智能合同能够与关键的链外事件/数据进行交互，并能够使用广泛接受的支付方法，这是该技术发展的下一个关键步骤。我们的整个团队对我们所得到的所有支持深表感谢，这些支持帮助我们扩展了智能合同的能力，并感谢每个人给予的道义、技术和非技术支持；我们非常感谢这一切。

如果你最近才听说我们正在解决的问题，并有兴趣看到它为你自己或他人解决，我们鼓励你加入我们；我们是一个包容、开放和尊重的社区，致力于解决这个问题。对于一般问题，请发送电子邮件至[【电子邮件保护】](/cdn-cgi/l/email-protection)，和/或请求邀请参加我们的 [Slack](https://chainlinknetwork.slack.com/) ，对于关于 Chainlink 的技术讨论，请查看我们的 [Github](https://github.com/smartcontractkit) ，和/或加入我们的 [Gitter 频道](https://gitter.im/smartcontractkit-chainlink/Lobby)。