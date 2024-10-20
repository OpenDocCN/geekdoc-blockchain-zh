# ApeWorX:即将推出的新 Python 框架

> 原文：<https://blog.chain.link/apeworx-python-vyper/>

Python 开发人员喜欢使用智能契约框架 Brownie。Brownie 的继任者正在酝酿中——创造 Python Web3 开发人员体验的新形象。

在这一块，我要说的是 [ApeWorX](https://www.apeworx.io/) ，也叫“猿”。

ApeWorX 是一个基于 Python 的智能合约开发和部署框架，以其可定制性和安全的私钥管理而闻名。

你们很多人都知道我喜欢 Python，一进入 Web3 空间我就爱上了 [布朗尼](https://github.com/eth-brownie/brownie) 框架。自从我进入这个领域以来，似乎所有最初的 Web3 框架要么已经成功，要么另一个竞争者已经进入:

*   [DappTools 官方认可](https://github.com/dapphub/dapptools/pull/927/files) [代工厂](https://github.com/foundry-rs/foundry) 为其继任者。
*   [安全帽](https://hardhat.org/) 继 [松露](https://trufflesuite.com/) 之后，在 DeFi 中占据了最常用框架的位置。
*   [ApeWorX](https://www.apeworx.io/) 似乎被定位为有朝一日成为布朗尼框架的继承者。

众所周知，以太坊 Python 社区是最具协作性和紧密联系的团体之一。许多的 [威伯族](https://vyper.readthedocs.io/en/stable/index.html) 和 [布朗尼贡献者](https://github.com/eth-brownie/brownie/graphs/contributors) 在 [猿类贡献者](https://github.com/ApeWorX/ape/graphs/contributors) 的名单上可以看到，包括 [小狗 B](https://github.com/fubuloubu)[Banteg](https://twitter.com/bantg)和 [)](https://github.com/skellet0r)

另外，Python 爱好者和 DeFi 协议[曲线](https://curve.fi/) 都开始使用 Ape 作为他们合同的框架。

今天，我们将从一个布朗尼用户的角度，对 ApeWorX 进行一个高层次的“web 3 licity-split”审视。

### web 3 licity-拆分外观

*你可以在我们的*[*ape worx-starter-kit*](https://github.com/smartcontractkit/apeworx-starter-kit)*中找到一个最小的 ApeWorX & Vyper 模板，用代码示例让你入门。T13】*

在 [安装 ape](https://docs.apeworx.io/ape/stable/userguides/quickstart.html#installation) 和类似`pipx install eth-ape`或者`pip`的东西之后，你就可以进入 ape 命令行界面了。

启动一个新项目的最快方法是使用 ape init，它会给你一个空白的设置，如下所示:

```
.

├── ape-config.yaml

├── contracts

├── scripts

└── tests
```

以下是每个文件夹包含的内容:

*   合同: 你所有的抵押、担保或其他合同都将存放在那里。
*   **脚本:** 你所有的 Python 代码都将放在哪里。
*   **测试:** 你的 Python 测试。
*   **ape-config.yaml:** 项目的配置文件。这是与 brownie-config.yaml 或 hardhat.config.js 相对应的 ape

在您的脚本文件夹中，您可以创建如下脚本:

```
def main():

 print("Hello!")
```

要在 ape 中运行任何 Python 脚本，请运行:

```
ape run scripts/my_script.py
```

#### **插件**

Ape 没有默认的 Vyper、Solidity 或其他任何东西，而是使用一个 [系统的插件](https://docs.apeworx.io/ape/stable/userguides/installing_plugins.html) 来使 ApeWorX 完全可定制为您特定的智能合约需求。最流行的两个插件是[Solidity](https://github.com/ApeWorX/ape-solidity)和[Alchemy](https://github.com/ApeWorX/ape-alchemy)的插件，它们允许你编译 Solidity 契约并轻松部署到 Alchemy。

```
ape plugins install solidity alchemy
```

一旦你设置好了，你就可以在合同文件夹中写下你的 Solidity 合同并进行编译。

```
ape compile
```

#### **网络**

Ape 采用了一种特殊的方法来处理网络。大多数框架，包括 Hardhat、Brownie 和 Foundry，都以类似的方式对待 EVM 链。ApeWorX 不一样。

ApeWorX 将网络分成 **生态系统** 和 **链条** 。比如以太坊生态系统被分成 **mainnet、ropsten、kovan、goerli、** 等。如果你想使用类似 fantom 的东西，你可以安装 Fantom 网络插件:

```
ape plugins install fantom
```

然后你会在 ape 网络列表中看到你的新网络列表:

```
fantom                                                                                                      

├── opera                                                                                                   

│   └── geth  (default)                                                                                     

├── testnet                                                                                                 

│   └── geth  (default)                                                                                     

└── local  (default)                                                                                        

   └── test  (default)
```

如果您不想为您的网络安装插件，您可以使用 [临时方法](https://docs.apeworx.io/ape/stable/userguides/networks.html#ad-hoc-network-connection) ，只需将 RPC URL 放入您喜欢的网络即可。ape 将尽可能多地假设发送事务。

```
ape run scripts/my_script.py --network https://my_rpc_url.com
```

#### **账户**

各种框架之间最大的区别之一是它们处理账户的方式。大多数框架都设置了一个. env 文件来存储您的私钥。但是，把你的私钥放在 a .env 中已经被 [永远绊倒了开发者](https://twitter.com/heyOnuoha/status/1522542744954191872) 。你 *可以* 在 ape 中做到这一点，但是默认要安全得多。

Ape 允许您导入私钥，然后它会加密并存储在您的计算机上。无论何时你想使用这个帐号或私钥，你都需要密码来解密它。这意味着再也不会不小心把你的按键推到 GitHub 上了！

```
ape accounts import my_key
```

然后它会提示您输入密钥和密码。在 Python 脚本中，您可以使用 load 函数获得您的私钥。

```
from ape import accounts

accounts.load("local-default")
```

运行该脚本时，系统会提示您输入密码。

#### **其余的……**

框架的其余部分如你所料。您可以使用最流行的 Python 测试框架之一的 [pytest](https://docs.pytest.org/en/7.1.x/) 来编写您的测试。您可以进入 [ape 控制台](https://docs.apeworx.io/ape/stable/commands/console.html) 在您选择的网络的 Python 环境中使用交互式 shell。

这是你想从框架中得到的一切。

猿是框架空间中的新玩家，这是一个 [的精彩回购促成的。](https://github.com/ApeWorX/ape/issues) 如果你热爱 Python 并且对如何改进 ape 有想法，一定要留下一个问题，一个拉请求，或者干脆给他们掉一颗星！

祝你模仿愉快！

*本文中表达的观点仅是作者个人的观点，并不代表链家基金会或链家实验室的观点和信念。T3】*