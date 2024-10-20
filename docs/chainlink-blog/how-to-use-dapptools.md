# 如何使用 DappTools

> 原文：<https://blog.chain.link/how-to-use-dapptools/>

说到写智能合约，开发者只需要知道一种语言，比如 [Solidity](https://docs.soliditylang.org/en/v0.8.11/) ， [Vyper](https://vyper.readthedocs.io/en/stable/) ，或者[Rust](https://www.rust-lang.org/learn)。然而，选择一个框架并学习围绕该框架的所有语言可能会很棘手。  

学习像[DappTools](https://dapp.tools/)这样的极简命令行框架可以消除这些问题，让 Web3 开发者的生活变得更加轻松。

在本 daptools 教程中，您将学习如何通过 daptools 框架创建、测试和部署您的智能合约。

查看本教程的视频:

[https://www.youtube.com/embed/csTWByu481I?feature=oembed](https://www.youtube.com/embed/csTWByu481I?feature=oembed)

## 什么是 DappTools？

DappTools 是一个类似于 Hardhat 和 Brownie 的框架，帮助智能联系人开发人员测试、部署和维护他们的代码。如果部署一个契约，那么编译后的字节码存储在哪里？你怎么知道它去了哪里？重新部署新代码有多容易？所有这些都是通过使用智能契约开发框架解决的问题。

DappTools 最初是用 Haskell 编写的。然而最近，Paradigm 团队采用了 DappTools，并在 Rust 中重写了它，将他们的新创作称为 [铸造](https://www.paradigm.xyz/2021/12/introducing-the-foundry-ethereum-development-toolbox/) 。两者的工作方式相似，都是以命令行为中心的，快速的，并且经常涉及到编写大量模糊的可靠性测试。

DappTools 是许多领先协议的流行选择。

## 为什么要使用 DappTools？

如果你是一个热爱 Linux、bash shells 和快速、以命令行为中心的编码的开发人员，那么这绝对是一个你应该尝试的智能契约框架。此外，如果您不熟悉 JavaScript 或 Python，这也非常适合您！

## 我们在学习什么？

在本教程中，我们将学习如何:

1.  使用 DappTools
2.  部署 Chainlink-powered [混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/) 使用[daptools-starter-kit](https://github.com/smartcontractkit/dapptools-starter-kit)

下面是几个在这个初学者工具包中使用 Chainlink 服务的例子:

*   [链环价格提要](https://docs.chain.link/docs/get-the-latest-price/)
*   [链型 VRF](https://docs.chain.link/docs/chainlink-vrf/) 链型 VRF
*   [](https://docs.chain.link/docs/chainlink-automation/introduction/)

## 安装

### 要求

首先，我们需要安装一些东西。

*   [去](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) 去
*   [DappTools](https://github.com/dapphub/dapptools#installation)

您可能已经安装了它，但如果没有，您将需要`make`。按照 [这些步骤](https://askubuntu.com/questions/161104/how-do-i-install-make) 检查你是否安装了。

### 入门

一旦我们安装了这些工具，我们就可以克隆 starter kit repo 并开始工作。

```
sh
git clone https://github.com/smartcontractkit/dapptools-starter-kit
cd dapptools-starter-kit
make # This installs the project's dependencies.
make test
```

现在你有了文件，让我们来看看每件事都做了什么:

*   `Makefile`:放置脚本的地方。DappTools 是基于命令行的，我们的 makefile 帮助我们用几个字符运行大型命令。
*   `lib`:这个文件夹是用于外部依赖的，比如 OpenZeppelin 或者 ds-test。
*   `out`:你编译的代码去哪了。类似于 Brownie 中的构建文件夹或 Hardhat 中的工件文件夹。
*   `src`:这就是你的智能合约所在。类似于 Brownie 和 Hardhat 中的合同文件夹。

### 测试

让我们做些测试吧！为了测试我们可以运行 `make test` 或者 `dapp test`。

【DappTools 中的所有命令都与这个 repo 一起工作，包括`dapp build`、`ethsign`和`dapp test`。

### 导入外部依赖关系

假设我们想要使用 [OpenZeppelin 标准](https://docs.openzeppelin.com/contracts/2.x/api/token/erc721) 创建一个 NFT。要安装外部契约或包，我们可以使用`dapp install`命令。我们需要命名 GitHub 回购组织和要安装的回购名称。

首先，我们需要提交到目前为止所做的更改。DappTools 将外部包作为 git 子模块引入，所以我们需要首先提交。

运行:

```
git add .
git commit -m ‘initial commit’
```

然后，我们可以安装我们的外部软件包。例如，对于 OpenZeppelin，我们将使用:

```
dapp install OpenZeppelin/openzeppelin-contracts
```

现在你应该会在你的 lib 文件夹中看到一个名为 openzeppelin-contracts 的新文件夹，因为它是从 GitHub 下载的。这个回购已经从 OpenZeppelin 合同开始，所以有一些重复，但我们仍然要看看它是如何工作的。

## 展开

要进行部署，您首先需要设置您的`ethsign`和`.env`文件。

### 设置您的帐户/ethsign

要将您的私钥放入 DappTools，您可以使用 keystore 或`ethsign`。`ethsign`随`dapptools`的安装一起提供。对于`ethsign`，运行以下:

```
bash
ethsign import 
```

现在会提示您输入私钥和密码。可以从类似 [MetaMask](https://metamask.io/) 的钱包中获得私钥。一旦成功，将私钥的地址添加到您的`.env`文件中的一个`ETH_FROM`变量下。参见`.env.example`文件中的例子。

请参见`Makefile`了解更多关于这种工作方式的背景信息。

如果你要部署到一个测试网，确保你的钱包里有测试网 ETH 和 LINK。你可以从 [链接龙头](https://faucets.chain.link/) 获得 testnet 链接。

### 建立你的`.env`档案

你可以在`.env.example`中看到你的`.env`应该是什么样子的一个例子(部署到一个真实的网络)。

1.  `ALCHEMY_API_KEY`:获取一个 [炼金术](https://www.alchemy.com/) 账号即可找到。
2.  `ETH_FROM`:你要发送交易的钱包地址。您必须将您想要使用的地址的私钥加载到您的`ethsign`中，请参见上文。
3.  `ETHERSCAN_API_KEY`:用于在 Etherscan 上验证合同(可选)。
4.  `ETH_RPC_URL`:使用`make deploy`时有默认部署网络(可选)。

## 测试网和维护网部署

在你的`.env`文件中设置你的`ETH_RPC_URL`或`ALCHEMY_API_KEY`，然后运行以下命令之一:

柜台(自动化兼容合同):

```
bash
make deploy CONTRACT=Counter
```

价格馈送:

```
bash
make deploy CONTRACT=PriceFeedConsumer
```

链家 VRF 消费者:

```
bash
make deploy CONTRACT=VRFConsumer
```

您可以在`scripts`文件夹中各自的`deploy`文件中更改它们的部署参数。所有的构造函数参数都创建在`./src/helper-config.sh`文件夹中。在这里，您可以跨网络分配不同的构造函数参数。

#### 本地测试网

#在一个端子上

dapp 测试网

把你的`ETH_RPC_URL`改成`http://127.0.0.1:8545`

然后运行您的部署脚本。

#### 在以太扫描上验证

部署合同后，您可以使用在 Etherscan 上验证合同

```
ETHERSCAN_API_KEY=<api-key> dapp verify-contract <contract_directory>/<contract>:<contract_name> <contract_address>
```

例如:

```
ETHERSCAN_API_KEY=123456765 dapp verify-contract ./src/Counter.sol:Counter 0x23456534212536435424
```

查看 [dapp 文档](https://github.com/dapphub/dapptools/tree/master/src/dapp#dapp-verify-contract) 看看如何使用 DappTools 验证合同。

## 与您的合同互动

为了与我们的合同进行交互，我们使用`seth`命令。假设我们已经将我们的`PriceFeedConsumer.sol`部署到了 Kovan，现在我们想要调用`getLatestPrice`函数。我们如何做到这一点？

```
ETH_RPC_URL=<YOUR_RPC_URL> seth call <YOUR_CONTRACT_ADDRESS> "getLatestPrice()"
```

例如:

```
ETH_RPC_URL=https://alchemy.io/adsfasdf seth call 0xd39F749195Ab1B4772fBB496EDAF56729ee36E55 "getLatestPrice()"
```

这将给我们一个类似于`0x0000000000000000000000000000000000000000000000000000004c17b125c0`的输出，它是`326815000000` 的十六进制数

这是打电话交易(不是花煤气)。要改变区块链的状态，我们可以使用`seth send`。假设我们部署了一个`VRFConsumer`合同，我们想调用`getRandomNumber` :

首先，我们需要将我们的合同发送到 Kovan 链上的某个环节:

```
ETH_RPC_URL=<YOUR_RPC_URL> ETH_FROM=<YOUR_FROM_ADDRESS> seth send <LINK_TOKEN_ADDRESS> "transfer(address,uint256)" <VRF_CONSUMER_ADDRESS> 1000000000000000000
```

喜欢:

```
ETH_RPC_URL=https://alchemy.io/adfasdf ETH_FROM=0x12345 seth send 0xa36085F69e2889c224210F603D836748e7dC0088 "transfer(address,uint256)" 0xa74576956E24a8Fa768723Bd5284BcBE1Ea03adA 100000000000000000
```

其中`100000000000000000` = 1 环节

然后，我们可以调用`getRandomNumber`函数:

```
ETH_RPC_URL=<YOUR_RPC_URL> ETH_FROM=<YOUR_FROM_ADDRESS> seth send <VRF_CONSUMER_ADDRESS>  "getRandomNumber()"
```

稍微延迟后，读取结果:

```
ETH_RPC_URL=<YOUR_RPC_URL> seth call <VRF_CONSUMER_ADDRESS> "randomResult()"
```

如您所见，将这些脚本保存在我们的`scripts`文件夹中会很棒。如果你想投稿，请制作一个 PR！

## 资源

本教程的一些有用资源:

*   [DappTools](https://dapp.tools)
    *   [Hevm 文档](https://github.com/dapphub/dapptools/blob/master/src/hevm/README.md)
    *   [Dapp 文档](https://github.com/dapphub/dapptools/tree/master/src/dapp/README.md)
    *   [塞斯文件](https://github.com/dapphub/dapptools/tree/master/src/seth/README.md)
*   [链环](https://docs.chain.link)
*   [牛逼-dapptools](https://github.com/rajivpo/awesome-dapptools)

## 总结

DappTools 是一个非常强大的应用程序，可以帮助您构建一个改变游戏规则的 dApp。我们建议检查一下，试一试，看看通过利用 Chainlink 分散式服务可以构建什么。

访问[chain . link](https://chain.link)或阅读[docs . chain . link](https://docs.chain.link)上的文档，了解更多关于 Chainlink 的信息。要讨论整合，[联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF)。