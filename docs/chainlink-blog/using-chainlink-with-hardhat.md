# 如何在安全帽上使用 Chainlink

> 原文：<https://blog.chain.link/using-chainlink-with-hardhat/>

由于其对自动化和重复[任务](https://hardhat.org/guides/create-task.html)的关注，以及其内置的[本地以太坊网络](https://hardhat.org/hardhat-network/)，Hardhat 正迅速成为许多以太坊开发者的首选开发环境。在这篇技术文章中，我们将向您展示如何使用 Hardhat 来构建、部署三种不同类型的智能合约并与之交互，这三种智能合约利用了 Chainlink 网络:

1.  获取外部数据的 API 使用者协定
2.  从[链价格馈送](https://docs.chain.link/docs/using-chainlink-reference-contracts)中读取最新价格的消费者契约
3.  使用 [Chainlink VRF](https://docs.chain.link/docs/chainlink-vrf) 请求随机数的 VRF 消费者契约

## 概述和前提条件

Hardhat 是一个面向以太坊开发者的开发环境，帮助管理和自动化重复性任务。任务是简单的可重复函数，包含某些元数据，例如任务需要什么参数。任务的一个例子是用一些 ETH 或其他令牌为部署的合同提供资金。

Hardhat 还配备了自己的本地开发网络，名为 [Hardhat Network](https://hardhat.org/hardhat-network/) ，专注于可靠性调试和额外的日志记录，并为开发人员提供了一个非常适合开发和精炼代码的本地开发环境。

Hardhat 的许多功能来自插件，这些插件本质上是注入到项目中的任务或外部代码。两个流行的安全帽插件是 [web3](https://hardhat.org/plugins/nomiclabs-hardhat-web3.html) 和 [ethers.js](https://hardhat.org/plugins/nomiclabs-hardhat-ethers.html) 插件，这两个插件都允许开发者与以太坊网络进行交互。

在我们的[源代码](https://github.com/pappas999/chainlink-hardhat-box)中，我们已经创建了一个‘Chainlink Hardhat Box’，这基本上是一个 hard hat 项目，包含在您的 Solidity [智能合约](https://chain.link/education/smart-contracts)中实施和部署 chain link 网络今天提供的主要功能所需的所有任务和智能合约。

第一步是下载 Chainlink Hardhat box 的[源代码](https://github.com/pappas999/chainlink-hardhat-box)并安装所需的依赖项:

```
git clone https://github.com/smartcontractkit/hardhat-starter-kit/
cd hardhat-starter-kit
npm install
```

一旦完成，您需要按照项目的[自述文件](https://github.com/smartcontractkit/hardhat-starter-kit/)中的说明来设置所需的环境变量。在本教程中，我们将使用科万测试网。现在，您已经准备好部署智能合约了。

## 部署智能合同

Chainlink Hardhat Box 附带了三个智能合约，如本文顶部所述。您可以部署所有这三个组件，或者只是其中的一个子集。要选择部署哪些契约并设置所需的特定于环境的参数，可以对 [deploy](https://github.com/pappas999/chainlink-hardhat-box/tree/main/deploy) 脚本进行适当的修改。如果一切保持原样，它将使用默认值将所有三个合同部署到 Kovan 网络。在下面的例子中，我们将在项目中使用默认值。

为了将我们的智能合约部署到 Kovan 网络，我们将利用 [hardhat-deploy](https://hardhat.org/plugins/hardhat-deploy.html) 插件，这是一个用于可复制部署和测试的 hardhat 插件。为了部署合同，我们运行以下命令:

```
npx hardhat deploy
```



![Deploying the Chainlink Hardhat Box](img/0dcb8636e2a61fd22b343746911285a8.png)

<figcaption id="caption-attachment-1427" class="wp-caption-text">展开链环安全帽盒</figcaption>





## 运行安全帽任务

既然我们的智能合约已经部署，我们将利用 Hardhat [任务](https://hardhat.org/guides/create-task.html)与我们部署的合约进行交互。

### 使用链接价格源

价格提要消费者契约有一个 **read-price-feed** 任务，用于读取指定价格提要的最新价格。如果使用部署中的默认值，它将在 Kovan 上查找 [ETH/USD](https://feeds.chain.link/eth-usd) 价格。

```
npx hardhat read-price-feed --contract 0x0ef1181768A99E522FB5535fA2e0D172B36d3479

```



![Reading data from the Price Feed contract](img/b0a359b7587cfc9e4d636c814c50fca2.png)

<figcaption id="caption-attachment-1426" class="wp-caption-text">从价格饲料合同中读取数据</figcaption>





### 请求外部数据

API 消费者契约有两个任务，一个是基于一组参数请求外部数据，另一个是检查数据请求的结果。此合同需要首先通过 LINK 获得资金:

```
npx hardhat fund-link --contract  0xc719F4B720cB7cBcabB09dF0040b47f3F9CE6a58

```



![Funding the contract](img/9b0aabed2ba22315541c8b0dde3a8453.png)

<figcaption id="caption-attachment-1425" class="wp-caption-text">资助合同</figcaption>





一旦获得资金，您就可以通过向**请求数据**任务传递[个参数](https://github.com/pappas999/chainlink-hardhat-box#request--receive-data)来请求外部数据。合同参数是必需的，其余是可选的

```
npx hardhat request-data --contract  0xc719F4B720cB7cBcabB09dF0040b47f3F9CE6a58

```



![Requesting external data](img/7f108ca6173147cb89c921b3969eecb7.png)

<figcaption id="caption-attachment-1424" class="wp-caption-text">请求外部数据</figcaption>





一旦您成功地请求了外部数据，您就可以使用 **read-data** 任务来读取从 Chainlink [oracle](https://chain.link/education/blockchain-oracles) 返回的结果。

```
npx hardhat read-data --contract  0xc719F4B720cB7cBcabB09dF0040b47f3F9CE6a58

```



![Reading the returned data](img/826332c29cbb4a95ef719d7877de43b6.png)

<figcaption id="caption-attachment-1423" class="wp-caption-text">读取返回的数据</figcaption>





### 使用链环 VRF

VRFConsumer 契约有两个任务，一个是请求随机数，另一个是读取随机数请求的结果。此合同需要首先通过 LINK 获得资金:

```
npx hardhat fund-link --contract  0x524Bf15C1d63581Fcf27bC34105542F53AA378Bb

```



![Funding the contract](img/7f115584fa05cc30b708140ecb95a1e2.png)

<figcaption id="caption-attachment-1422" class="wp-caption-text">资助合同</figcaption>





一旦资金到位，您就可以使用**请求随机数**任务执行 VRF 请求，并传入所需的种子号:

```
npx hardhat request-random-number --contract  0x524Bf15C1d63581Fcf27bC34105542F53AA378Bb  --seed '777'

```



![Requesting a random number using Chainlink VRF](img/b966627acbeda20ceb94a2a16c224fc0.png)

<figcaption id="caption-attachment-1421" class="wp-caption-text">使用链环请求随机数</figcaption>





一旦您成功地请求了一个随机数，您就可以使用 **read-random-number** 任务来读取由 Chainlink oracle 返回的经过验证的随机数。

```
npx hardhat read-random-number --contract  0x524Bf15C1d63581Fcf27bC34105542F53AA378Bb
```



![Reading the returned random number](img/b091128f77337098965c3e3b5d824639.png)

<figcaption id="caption-attachment-1420" class="wp-caption-text">读取返回的随机数</figcaption>





## 摘要

Hardhat 是一个开发环境，允许以太坊开发人员快速将 Chainlink oracles 实现到他们的智能合约中，使他们能够通过使用可重复的预定义任务轻松部署和测试它们。

如果你是一名开发人员，并希望将你的智能合同连接到链外数据和系统，请访问[开发人员文档](https://docs.chain.link/)，并加入关于[不和谐](https://discordapp.com/invite/aSK4zew)的技术讨论。如果您想安排一次电话会议来更深入地讨论整合事宜，请点击此处的。

### 关于这个话题的更多信息

*   [如何获取实体加密货币的当前价格](https://blog.chain.link/fetch-current-crypto-price-data-solidity/)
*   [实态随机数生成](https://blog.chain.link/random-number-generation-solidity/)
*   [API、智能合约以及如何连接它们](https://blog.chain.link/apis-smart-contracts-and-how-to-connect-them/)

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://www.chain.link/solutions/defi)