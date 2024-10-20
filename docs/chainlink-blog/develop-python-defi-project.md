# 使用 Python 开发 DeFi 项目

> 原文：<https://blog.chain.link/develop-python-defi-project/>

***2021 年 11 月 5 日更新***

在本教程中，我们将介绍如何用 Python 开发一个 DeFi 项目。分散金融(DeFi) 是区块链和智能合约领域最重大的进步之一，通常被称为“新金融科技”目前，智能合约开发由 JavaScript 主导，部分原因是 JavaScript 是[这个星球上最常用的语言](https://insights.stackoverflow.com/survey/2020#technology-programming-scripting-and-markup-languages)，利用 Node.js 自带的“JavaScript 无处不在”的思想更容易构建全栈应用程序。然而，量化分析师、股票交易员和对冲基金的金融科技世界并非如此。这些金融科技公司大多出于各种原因使用 Python:

*   出色的开发人员体验
*   强大的人工智能和机器学习
*   捆绑的金融科技产品包
*   全面的分析工具
*   生产环境中的可靠性



![A diagram showing current job openings by coding language. Python has the most jobs available. ](img/fba8715ee26b192e36583a9c031c5089.png)

<figcaption id="caption-attachment-1410" class="wp-caption-text">来源:电子金融职业</figcaption>





这么多数据科学家、学者和金融科技机构使用 Python 是有原因的。DeFi 领域的一些项目也有这种想法，并且已经用 Python 和 Solidity 构建了他们的整个 DeFi 平台。正是因为有了像 [web3.py](https://web3py.readthedocs.io/en/stable/) 和 [Brownie](https://github.com/eth-brownie/brownie) 这样的库和框架，我们才能看到这些项目变成现实。Brownie 是一个类似松露的框架(它们都很“可爱”)，它维护您的部署、脚本、测试，并允许您创建一个端到端的后端。

Web3.py 和 Brownie 还提供了“mixes ”,你可以用一些样板代码预先打开一个项目。这就是我们今天要做的,[链环布朗尼混合物](https://github.com/smartcontractkit/chainlink-mix)。

现在我们为什么要用 Chainlink + Python？正如 Python 是金融科技事实上的编程语言一样，Chainlink 是为 DeFi [智能合约](https://chain.link/education/smart-contracts)提供离线数据和计算的事实上的 [oracle](https://chain.link/education/blockchain-oracles) 解决方案，目前为顶级 DeFi 协议确保了超过 750 亿美元的价值。这两种技术的结合为安全地分散金融科技领域提供了一个强大的框架。

要开始用 Brownie 和 Python 构建你的 DeFi 应用，你首先需要[安装 Python。](https://www.python.org/downloads/)此时不建议 Python 低于 3.6 版本，如果你有比 3.6 更老的版本请升级。您可以通过运行以下命令来查看您的 Python 版本并验证其安装是否正确:



```
python --version

```

或者，如果使用 python3:

```
python3 --version

```

你还需要安装 [Ganache](https://www.trufflesuite.com/ganache) 。Ganache 是一个用 Python 编写的一键区块链，允许您轻松地旋转本地区块链。尽管您必须用 npm 和 node.js 下载它，但这将是您必须与之交互的唯一一段 JavaScript。

首先，您需要安装 [node.js 和 NPM](https://nodejs.org/en/download/)。Node.js 随 npm 一起安装。下载后，您可以通过运行以下命令来检查它是否正确完成:

```
npm --version 
node --version
```

然后，您可以通过命令行安装 Ganache。

```
npm install -g ganache-cli

```

一旦你安装了这些，我们将安装 eth-brownie。我们推荐使用`pipx`而不是`pip`，这样我们可以将`eth-brownie`安装在它自己的环境中。

首先，安装`pipx:`

```
python3 -m pip install --user pipx
python3 -m pipx ensurepath

```

然后，关闭并重新启动终端。如果你使用的是 [VSCode](https://code.visualstudio.com/) ，它看起来会像一个小小的垃圾桶图标。`pipx`

应该可以成功安装。可以用`pipx --version`查一下。然后，安装`eth-brownie`。

```
pipx install eth-brownie
```

有时，在这一步您可能会遇到问题。如果你在谷歌上搜索这个问题，你可能会找到这个问题的线索。否则，做一个 [StackOverflow](https://stackoverflow.com/) 问题，用`brownie`标记。

如果您想在没有虚拟环境的情况下安装，您可以使用`pip`或`pip3`:

```
pip3 install eth-brownie

```

如果您在终端中运行`brownie`,您将知道您已经做对了，并且您会得到类似如下的输出:

```
Brownie v1.17.0 - Python development framework for Ethereum
Usage: brownie <command> [<args>...] [options <args>]
Commands:
 init  Initialize a new brownie project
 bake  Initialize from a brownie-mix template
 pm  Install and manage external packages
 compile Compile the contract source files
 console Load the console
 test  Run test cases in the tests/ folder
 run Run a script in the scripts/ folder
 accounts  Manage local accounts
 networks  Manage network settings
 gui Load the GUI to view opcodes and test coverage
 analyze Find security vulnerabilities using the MythX API
Options:
 --help -h Display this message
 --version Show version and exit
Type 'brownie <command> --help' for specific options and more information about
each command.

```

此外，你还需要一个超能面具或其他以太坊钱包。如果你以前从未使用过 ETH 钱包，你可以观看这个视频来帮助你进行设置。**请注意，这也显示了为 Ropsten 获取 testnet ETH，而 Chainlink 不再支持它。**如果跟随，请使用 Kovan。

[https://www.youtube.com/embed/4ZgFijd02Jo?feature=oembed](https://www.youtube.com/embed/4ZgFijd02Jo?feature=oembed)

最后，确保你的 ETH 钱包里有一些 testnet 链接和 Kovan ETH。你可以在[链节龙头](https://faucets.chain.link/)找到 ETH 和 LINK。

## 启动 Chainlink 项目

为了开始使用核仁巧克力饼，我们可以使用所谓的核仁巧克力饼混合给我们样板代码。在这个例子中，我们将部署一个简单的 [Chainlink Price Feed](https://data.chain.link/) 来了解 Brownie 框架。让我们烘烤链环混合物。

```
brownie bake chainlink-mix
cd chainlink

```

这将使我们进入一个新的项目，其中一些默认代码已经为我们建立。如果我们运行 *ls* ，我们可以看到文件的布局:

*   构建:这是项目跟踪您部署的智能契约和编译的契约的地方
*   合同:合同的源代码，通常用 Solidity 或 Vyper 编写
*   接口:您将需要使用部署的契约的接口布局。每次与合同的交互都需要一个 [ABI](https://ethereum.stackexchange.com/questions/234/what-is-an-abi-and-why-is-it-needed-to-interact-with-contracts) 和一个地址。接口是获得合同 ABI 的好方法
*   脚本:我们创建的脚本，用于自动化处理我们的合同
*   测试:测试
*   brownie-config.yaml:这是 brownie 了解如何使用智能合约的所有信息。我们想部署到什么样的区块链？有什么我们想设置的特殊参数吗？所有这些都在配置文件中设置。

`requirements.txt`、`README.md`、`LICENSE`、`.gitignore`暂时可以忽略。当你练习的时候，你会发现它们是干什么用的。

## 设置环境变量

尽管我们刚刚安装了 Ganache 来进行本地测试，但我们也希望能够连接到 ETH mainnet 和 test net，这样我们就可以在真正的 test net 上部署它们。为此，我们需要设置我们的`WEB3_INFURA_PROJECT_ID`。您可以从 [Infura 网站免费获得一个 Infura ID。](https://infura.io/)你可以使用其他的 web3 提供商或者你自己的节点，但是你需要为此做更多的配置。

现在您已经有了 web3 ID，我们需要将我们的私钥作为一个环境变量，这样我们就可以用我们的钱包来使用我们的帐户。如果你正在使用元掩码，寻找*导出键*。使用元掩码，您可能需要在私钥的开头添加`0x`。建议在测试和导出密钥时使用不同于主帐户的帐户，以防万一。

>重要提示:请不要将您的私钥发送到 GitHub 或任何公共场所！如果有人得到了你的私人钥匙，他们就可以使用你账户中的所有资金！我们强烈建议您使用与您持有资金的账户不同的账户进行测试。

现在我们需要让它们成为环境变量。我们将使用一种简单的方法来设置环境变量，创建一个`.env`文件，并添加以下内容:

```
export PRIVATE_KEY=0x96789…..
export WEB3_INFURA_PROJECT_ID=’dog cat mouse….’

```

其中,`PRIVATE_KEY`是 MetaMask 中的键,`WEB3_INFURA_PROJECT_ID`是 Infura 中的项目 ID。然后，创建一个`brownie-config.yaml`文件(或者只是添加到其中，如果它在那里的话)并添加下面一行:

```
dotenv: .env
```

您已经准备好部署到测试网络和本地网络了！

## 部署您的智能合同

现在我们已经设置好了一切，我们甚至可以继续将智能合约部署到 Kovan testnet！

在我们的`scripts`文件夹中，我们有一个名为`deploy_price_consumer_v3.py`的脚本。这将部署我们的智能合约，读取以太坊的美元价格。

如果您想更容易地了解这个契约的功能以及如何部署它，请随意查看关于[部署 price feed 契约](https://docs.chain.link/docs/beginners-tutorial)的 Chainlink 教程。

只需使用“brownie run”来使用部署脚本:

```
brownie run scripts/price_feed_scripts/deploy_price_consumer_v3.py --network kovan

```

您会看到类似这样的内容:

```
Running 'scripts/price_feed_scripts/deploy_price_consumer_v3.py::main'...
Transaction sent: 0x23d1dfa3937e0cfbab58f8d5ecabe2bfffc28bbe2349527dabe9289e747bac56
Gas price: 20.0 gwei   Gas limit: 145600   Nonce: 1339
PriceFeed.constructor confirmed - Block: 22721813   Gas used: 132364 (90.91%)
PriceFeed deployed at: 0x6B2305935DbC77662811ff817cF3Aa54fc585816

```

如果这个工作正常，我们可以去科万以太扫描，找到我们部署的合同。上面的链接显示了本例中部署的契约。

## 阅读你的智能合同

现在我们已经部署了一个智能合约，我们可以从刚刚部署的合约中读取 ETH 的价格。我们将使用现有的另一个脚本:

```
brownie run scripts/price_feed_scripts/read_price_feed.py --network kovan

```

我们将得到如下输出:

```
Brownie v1.12.2 - Python development framework for Ethereum
ChainlinkProject is the active project.
Running 'scripts/price_feed_scripts/read_price_feed.py::main'...
Reading data from 0x5A….
122322000000

```

其中 122322000000 是 ETH 当前的美元价格！Solidity 不懂小数，我们知道 Chainlink 价格 Feeds 有 8 位小数，所以价格是 1223.22 美元。

您刚刚使用 Python 和 Brownie 部署了您的第一个智能合同！

## 测试您的智能合同

这也是如何测试智能合约的一个很好的例子。我们使用[模仿对象](https://en.wikipedia.org/wiki/Mock_object)来测试甚至是本地的！

只需运行:

```
brownie test

```

您的测试将在本地 Ganache 实例上运行！

您还可以在 testnets 上使用类似以下的内容进行测试:

```
brownie test --network kovan

```

测试有一些功能，知道你是否在测试网上工作。如果您在本地工作，它会部署 oracle 代码的虚拟代码或“模拟代码”,以便我们可以从中进行测试。

## 更进一步

既然您已经知道如何使用 Python 部署智能合约，那么您可以开始在这个框架的基础上进行构建，以做更多有趣的事情。Python 有强大的包，如 Numpy、Scikit、Pandas 和 TensorFlow，可以进行定量工作、机器学习等。能够最终将这些技术结合在一起，是金融科技新时代的成功秘诀:去中心化金融。

Chainlink 是一个灵活的框架，用于将外部财务数据和系统引入链上，并与 Numpy 和 Pandas 等以数据为中心的包无缝集成。如果你是一名开发人员，想要快速将你的应用程序连接到 Chainlink，请访问[开发人员文档](https://docs.chain.link/)并加入 [Discord](https://discordapp.com/invite/aSK4zew) 的技术讨论。如果你用 Python、Chainlink 和 Brownie 做了一些很棒的东西，一定要用@chainlink 给我们加标签，这样我们就可以检查你做的所有很酷的工作了！

