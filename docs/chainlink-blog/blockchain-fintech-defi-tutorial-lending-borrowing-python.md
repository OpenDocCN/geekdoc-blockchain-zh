# 区块链 Fintech 教程:用 Python 借贷

> 原文：<https://blog.chain.link/blockchain-fintech-defi-tutorial-lending-borrowing-python/>

先决条件:

*本教程面向稍微熟悉 Python，并且很少或没有 Solidity/smart contract 经验的任何人。*

* * *

## 介绍

经典的金融科技世界充满了工具，让用户能够建立复杂的算法交易模型和系统。[去中心化金融(DeFi)](https://chain.link/education/defi) 世界为用户和开发者提供了完全相同的工具，围绕基础金融协议和工具的透明度和灵活性显著提高，催生了 DeFi 量化和研究工程师。DeFi 开发者和 DeFi quants 甚至可以利用这些工具的衍生品，将它们组合成新的服务，以建立传统金融科技领域没有的创新金融头寸。DeFi 开发人员的一个基本工具是以非托管方式借出和借入加密货币资产的能力。使用 DeFi 借贷协议的一些巨大优势是:

*   无摩擦卖空
*   在不平仓的情况下获得流动性
*   获得存款抵押品的收益
*   在传统金融科技世界里不可能的事情，比如[闪贷](https://aave.com/flash-loans/)。

金融科技领域的很大一部分都在使用 Python，这是因为其出色的开发者体验。通过智能合约，您可以使用您所熟悉的完全相同的 Python 工具。你不需要知道可靠性或如何编写智能合约，就可以参与量化 DeFi 或建立自己的加密货币对冲基金或商店。然而，如果你决定学习稳健，你的 DeFi 能力将会增加十倍，因为你将能够从事分散量化金融，更有效地集中你的资源。

在本教程中，我们将学习如何:

1.  将抵押品存入 Aave 贷款池
2.  获取我们的抵押品和另一项资产之间的对话率
3.  使用抵押品来借入不同的资产(取得贷款)
4.  偿还贷款

学习如何做到这一点将使我们能够利用 DeFi 生态系统中的交易，这些交易在传统的金融科技世界中远不容易实现，有时甚至不可能实现。

## Web3.py 和 Brownie 简介

像大多数系统一样，区块链世界目前有两个 Pythonic 接口: [web3.py](https://web3py.readthedocs.io/en/stable/) 和 [brownie](https://eth-brownie.readthedocs.io/en/stable/) 。Web3.py 是最原始和最细粒度的(除了自己编写自己的 web3.py 包！)与区块链互动的方式。Brownie 是建立在 web3.py 之上的一个框架，它抽象出了区块链交易的许多困难。在本教程中，我们将向您展示如何编写这些脚本和互动链使用布朗尼。布朗尼让生活变得简单多了，并且是一种很好的方式来抽象一些与区块链一起工作的更令人困惑的部分。如果你已经熟悉 web3.py，你也可以将 web3.py 与 Brownie 一起使用。如果你更喜欢原始的 web3.py，我们也在 [web3.py 存储库中做了所有的例子。](https://github.com/PatrickAlphaC/aave_web3_py)

让我们开始解释这是怎么回事。

## **设置**

首先，让我们克隆回购。

```
git clone https://github.com/PatrickAlphaC/aave_brownie_py
cd aave_brownie_py

```

你会看到一个这样的目录。

![Github for Borrowing, Lending, Shorting, and More](img/455d3239f1b17674ab8c71244a38497d.png)

<figcaption id="caption-attachment-2081" class="wp-caption-text">Github for Borrowing, Lending, Shorting, and More.</figcaption>





<figcaption></figcaption>



如果你迷路了，你也可以通过阅读自述文件获得一些有用的提示。

1.  安装需求

你需要在这里安装 [Python](https://www.python.org/downloads/) 。您还希望安装 [Nodejs](https://nodejs.org/en/download/) 来更快地运行我们的测试和开发，但是我们现在可以跳过这一步。

一旦 Python 安装完毕，让我们运行:

```
pip install -r requirements.txt

```

这将安装`eth-brownie`和`python-dotenv`。`eth-brownie`是布朗尼包，附带 web3.py

如果遇到问题，可以用 pipx 安装 eth-brownie:

```
pip install --user pipx
pipx ensurepath
# restart your terminal
pipx install eth-brownie

```

如果您可以运行`brownie --version`并得到如下结果，您就会知道您做对了:

```
Brownie v1.14.6 - Python development framework for Ethereum

```

2.  获取 ETH wallet 并设置环境变量

你需要一个以太坊钱包，你可以在这里下载[元面具](https://metamask.io/)或者[观看此视频](https://youtu.be/P7FX_1PePX0?t=40)开始。一旦有了元掩码，就需要两个环境变量，`WEB3_INFURA_PROJECT_ID`和`PRIVATE_KEY`。

您的 WEB3_INFURA_PROJECT_ID 将是您从 [Infura](https://infura.io/) 开始的项目 ID。Infura 是一个节点基础设施解决方案，用于连接以太坊区块链并与之交互。

```
# DO NOT SEND THESE TO GIT/GITHUB
export WEB3_INFURA_PROJECT_ID=<PROJECT_ID>
export PRIVATE_KEY=<PRIVATE_KEY>

```

您可以将它们添加到标签为`.env`的文件中，然后运行`source .env`将环境变量添加到您的 shell/终端中。请注意，如果您关闭了您的 shell/终端，您将不得不在下次打开 shell/终端备份时运行您的`.env`文件所在的`source .env`。你也可以从 Twilio 博客中了解更多关于[设置环境变量的信息。](https://www.twilio.com/blog/2017/01/how-to-set-environment-variables.html)

注意:不要把你的私人钥匙和任何真钱一起发给 GITHUB。请始终使用不同的帐户进行测试，然后你有真正的资金。

3.  获取一些 testnet ETH

对于准备经营本地连锁的，可以跳过这一步。如果你不明白我说的“本地连锁”是什么意思，那就继续阅读并遵循这些步骤。

使用这个[水龙头连接](https://faucet.kovan.network/)到达科万水龙头。如果以下步骤不起作用，您可以随时访问 [Chainlink 文档链接令牌合同](https://docs.chain.link/docs/link-token-contracts/)页面，找到最新的水龙头。输入您的新钱包地址，并获得一些测试网络。您应该会在 MetaMask 中看到您的余额更新。

![Get Kovan Testnet ETH](img/99939d63da9c278df7cdb8f9eca28b2e.png)

<figcaption id="caption-attachment-2082" class="wp-caption-text">Get Kovan Testnet ETH.</figcaption>





<figcaption></figcaption>



我们将在科万测试网上运行。测试网是对与真实区块链互动的模拟。

4.  用你的衣服换我们的

如果你从 2 个 ETH 开始，在完成这一步后，你将有大约 0.99 个 ETH 和 1 个 WETH 的余额。我们继续吧。

为了与 Aave 协议进行交互，我们将把我们的 ETH 换成一个 ERC20 版本的 ETH，称为 WETH(也称为 wrapped ETH)。这使得我们更容易与《AAVE 议定书》互动。对于不熟悉的人来说， [ERC20](https://support.blockchain.com/hc/en-us/articles/360027491872-What-is-an-ERC20-token-#) 是以太坊上常见的令牌标准。

```
brownie run scripts/get_weth.py --network kovan

```

* *对于那些想在 mainnet 分支上运行这些命令的人来说，只需删除命令的`--network kovan`部分。如果这让你困惑，忽略这个。**

您应该会看到元掩码余额减少。这是因为我们用 ETH 替换 wet。为了看到我们的新平衡，进入 MetaMask，点击`add token`。然后，在`custom tokens`下输入地址`0xd0a1e359811322d97991e03f863a0c30c2cf029c`。这是 Kovan testnet 上包装以太令牌的合同地址。

您会注意到现在总共有不到 2 个 ETH (1 + 0.99！= 2).这是因为每次你在区块链上交易，你都要付一点点汽油费。天然气是一种支付矿工和验证者少量费用来完成交易的方式。随着学习的深入(本教程中没有涉及)，您将发现有两种 gas:事务 Gas 和 Oracle Gas。

在本教程中，我们只需要关注事务气体。

如果你是新来的，这是你在 testnet 上的第一笔交易！恭喜你！

5.  放下抵押品，借链接，然后偿还借款金额，都在一个脚本！

```
brownie run scripts/aave_borrow.py --network kovan

```

或者，分叉 mainnet:

```
brownie run scripts/aave_borrow.py --network mainnet-fork

```

您应该得到这样的输出:

```
Brownie v1.14.6 - Python development framework for Ethereum
AaveBrowniePyProject is the active project.
Running 'scripts/aave_borrow.py::main'...
Approving ERC20...
Transaction sent: 0x04b86b3c11d8b45ad410ecb580becb8f1ef57fb1f72d3ac3944365317b99ca21
  Gas price: 2.0 gwei   Gas limit: 50695   Nonce: 3
  IERC20.approve confirmed - Block: 25241881   Gas used: 46087 (90.91%)
  IERC20.approve confirmed - Block: 25241881   Gas used: 46087 (90.91%)
Approved!
Depositing...
Transaction sent: 0xade4ab7c979e96dcb8ca6ebfda4206f8927d12fc078b32c59a723c3ae4883bca
  Gas price: 2.0 gwei   Gas limit: 253974   Nonce: 4
  ILendingPool.deposit confirmed - Block: 25241883   Gas used: 212742 (83.77%)
Deposited!
You have 0.100000012276459112 worth of ETH deposited.
You have 0 worth of ETH borrowed.
You can borrow 0.08000000982116729 worth of ETH.
LETS BORROW IT ALL
The DAI/ETH price is 0.0003642722357682
We are going to borrow 208.6351960638322 DAI
Transaction sent: 0x07b07852de7ac7cf492b34e0c929c65f38f1f83bf5953c14011ba9f659475247
  Gas price: 2.0 gwei   Gas limit: 392549   Nonce: 5
  ILendingPool.borrow confirmed - Block: 25241886   Gas used: 351754 (89.61%)
  ILendingPool.borrow confirmed - Block: 25241886   Gas used: 351754 (89.61%)
Congratulations! We have just borrowed 208.6351960638322
You have 0.100000036829377336 worth of ETH deposited.
You have 0.076000009330108915 worth of ETH borrowed.
You can borrow 0.004000020133392954 worth of ETH.
Approving ERC20...
Transaction sent: 0xede77fa7f91db8cda493a9aad092b4771c3dcf16718b086da64fe1b3b20dda9f
  Gas price: 2.0 gwei   Gas limit: 50798   Nonce: 6
  IERC20.approve confirmed - Block: 25241888   Gas used: 46180 (90.91%)
  IERC20.approve confirmed - Block: 25241888   Gas used: 46180 (90.91%)
Approved!
Transaction sent: 0xfda598cede32c2af0b8309b330bb93d08a8ccb2787adedef0de485220ee7d88a
  Gas price: 2.0 gwei   Gas limit: 242655   Nonce: 7
  ILendingPool.repay confirmed - Block: 25241889   Gas used: 187617 (77.32%)
  ILendingPool.repay confirmed - Block: 25241889   Gas used: 187617 (77.32%)
Repaid!

```

哇这里发生了很多事！我们来分解一下刚刚发生的事情…

# 打破它

## 与...相处

所以我们在这里做的第一件事是用一些 ETH 替换 wet。我们用我们的`./scripts/get_weth.py`脚本中的`get_weth`函数做到了这一点。

```
def get_weth(account=None):
   """
   Mints WETH by depositing ETH.
   """
   account = (
       account if account else accounts.add(config["wallets"]["from_key"])
   )  # add your keystore ID as an argument to this call
   weth = interface.WethInterface(
       config["networks"][network.show_active()]["weth_token"]
   )
   tx = weth.deposit({"from": account, "value": 1000000000000000000})
   print("Received 1 WETH")
   return tx

```

为了在以太坊上进行交易或通话，如果你想[修改区块链的状态](https://docs.soliditylang.org/en/v0.8.4/contracts.html#view-functions)，你必须始终使用`from`账户。我们正在修改区块链的状态，因为我们将要修改我们的 ETH 和 WETH 平衡。

我们使用从配置中得到的位于`brownie-config.yaml`的`account`。我们在底部附近看到它使用了我们的`PRIVATE_KEY`环境变量。

```
wallets:
 from_key: ${PRIVATE_KEY}
 from_mnemonic: ${MNEMONIC}

```

现在不要担心`MNEMONIC`。

我们将该帐户添加到我们的核仁巧克力饼帐户列表中:

```
accounts.add(config["wallets"]["from_key"])

```

现在，我们在脚本中有了一个帐户。

接下来，我们需要获取 WETH 契约对象，以便能够与它进行交互。我们想在合同中存入我们的钱，这样我们就能得到同样多的钱。我们可以随时用这份合同把我们的 wet 转换回 ETH。所有 ERC20 令牌(如 LINK、WETH、AAVE 等)本身都是链上的合约。为了与契约进行交互，我们总是需要两样东西。

1.  合同 ABI/接口
2.  合同地址

我们的`interfaces`文件夹中有这个界面。我们也有 ABI。编译后的项目将合同放入`build`文件夹。如果我们查看`build`下的`interfaces`文件夹，我们可以看到一个名为`WethInterface.json`的文件。在那个文件夹里，有一把钥匙叫`abi`。我们可以使用这个接口，因为它可以编译成 ABI。

ABI 代表[应用二进制接口](https://docs.soliditylang.org/en/v0.5.3/abi-spec.html)，是程序知道如何与契约交互的标准方式，包括 Python。

我们可以通过创建如下的`weth`变量，将地址和 ABI 添加到一个对象中，以便我们进行交互:

```
weth = interface.WethInterface(
       config["networks"][network.show_active()]["weth_token"]
   )

```

我们再次从配置文件中获得了`weth_token`地址。您会注意到不同的令牌有不同的地址，这取决于您正在处理的链。如果我们去`print(type(weth))`我们会得到:

```
<class 'brownie.network.contract.Contract'>

```

一个`Contract`对象就像一个类，它代表链上的契约。然后我们可以在链上调用该契约的函数。

然后，我们调用合同上的存款函数:

```
tx = weth.deposit({"from": account, "value": 1000000000000000000})

```

可靠性合同`weth`具有`deposit`功能。事实上，我们可以看到链上的[代码](https://kovan.etherscan.io/address/0xd0a1e359811322d97991e03f863a0c30c2cf029c#code)。此链接指向以太扫描，一个块浏览器。这是一种想象区块链上发生的所有事情的方式。

![Etherscan for WETH](img/2fd8a3fa08c9f40b216334ed600fa94d.png)

<figcaption id="caption-attachment-2083" class="wp-caption-text">Etherscan for WETH</figcaption>



我们可以看到下面的`Code`部分，其中有来自合同的所有代码。你有时会遇到没有代码部分的合同。这是因为他们还没有验证块浏览器。如果我们转到`Write Contract`部分，我们可以看到同样的`deposit`函数。

![Showing the deposit function on Etherscan.](img/76656286035c1b8d06b9da6ae91a9e86.png)

<figcaption id="caption-attachment-2084" class="wp-caption-text">Showing the deposit function on Etherscan.</figcaption>



所以我们也可能以这种方式收到 WETH！

每当我们进行函数调用并修改区块链的状态时，我们就进行了一次事务处理。在上面的输出中，我们看到类似这样的内容:

```
Transaction sent: 0x888bb9d6657b1de2e5eec465bf9641b401647a61a2bd428b51d8a95d5a3e329a

```

然后，您可以将此事务哈希复制到块资源管理器中，以查看该事务的详细信息。

咻！那里进行了大量的工作。让我们回顾一下。

*   我们用 Python 写了我们的账户
*   我们学习了如何通过地址和 ABI 与合同互动
*   我们学习了如何通过函数调用发送事务
*   我们学习了街区探险者

太棒了，现在让我们进入借贷方面。

## 存放抵押品

接下来，我们运行了`aave_borrow.py`脚本，它做了 4 件事:

1.  将抵押品存入 Aave 贷款池
2.  获得我们的担保品和另一项资产之间的对话率
3.  使用抵押品来借入不同的资产(取得贷款)
4.  偿还贷款

让我们看看`main`函数的开始:

```
def main():
   account = get_account()
   erc20_address = config["networks"][network.show_active()]["weth_token"]
   if network.show_active() in ["mainnet-fork"]:
       get_weth(account=account)
   lending_pool = get_lending_pool()

```

我们首先从我们的配置文件中获得我们的地址(如果我们在一个 testnet 上，它同样来自我们的配置)。如果您在本地链上测试，我们只使用它生成的第一个帐户。这在`get_account`功能中定义。然后，我们也从配置文件中获取 WETH 令牌的地址，如果我们在本地链上，我们调用之前调用的那个相同的`get_weth`函数。这是为了确保如果我们使用本地连锁店，我们的钱包里有 wet。

最后，我们得到了`lending_pool.`的地址 [`lending_pool`](https://docs.aave.com/developers/the-core-protocol/lendingpool) 是管理借贷和销售功能的智能合同链，因此得名。你可以在[的 Aave 文档](https://docs.aave.com/developers/the-core-protocol/lendingpool)中看到这些函数，或者你可以直接在链上看到合同。这是以太坊主网上的合同。

我们在这份合同中看到了许多有用的功能:

*   借
*   存款
*   getuseracaccountdata
*   偿还

这些是我们将要使用的功能。请记住，链上的智能契约与传统软件工程中的对象或类是相同的，并且每个都有与之相关联的功能。如果你去`print(type(lending_pool))`我们会得到这种类型:

```
<class 'brownie.network.contract.Contract'>

```

这意味着借贷池是一个合同，就像 WETH 一样！我们的`get_lending_pool()`函数实际上做了一些额外的步骤来获得 lending_pool 契约。让我们看看这个函数:

```
def get_lending_pool():
   lending_pool_addresses_provider = interface.ILendingPoolAddressesProvider(
       config["networks"][network.show_active(
       )]["lending_poll_addresses_provider"]
   )
   lending_pool_address = lending_pool_addresses_provider.getLendingPool()
   lending_pool = interface.ILendingPool(lending_pool_address)
   return lending_pool

```

请记住，我们需要两样东西来与智能合约交互:

1.  ABI/界面
2.  地址

我们有位于`interfaces`文件夹中的借出池的接口。你会注意到一个流行的接口惯例是以字母“I”开头。在这个例子中，我们有一个混合，以表明它不必以“I”开头。

为了让我们获得贷款池的地址，我们实际上必须通过`LendingPoolAddressesProvider`的地址。这是一个包含所有 Aave 贷款池地址的合同链。有时，贷款池的地址会改变，但贷款池提供者的地址永远不会改变，所以我们总是可以使用该合同的地址来获取贷款池的地址。你会看到我们在`lending_pool_addresses_provider`变量上调用函数`getLendingPool`。

让我们回到主函数。在我们获得 lending_pool 契约的地址之后，我们希望存放抵押品。这是我们需要做的第一步，因为只有我们提供了抵押品，我们才能获得贷款。我们也可以假设只是存放抵押品，然后收工！存放抵押品将让我们:

1.  获得收益——该协议向将抵押品存入平台的用户支付费用。他们从在平台上贷款的人产生的费用中给他们一部分。
2.  办理贷款——如果我们有足够的抵押品，我们只能办理贷款/借款。Aave 有一个名为 [liquidationcall](https://docs.aave.com/developers/the-core-protocol/lendingpool#liquidationcall) 的功能，如果你没有足够的抵押品，任何人都可以拨打这个电话并获得奖励。抵押品的价值必须保持高于贷款的价值，这就是为什么这被称为超额抵押贷款。
3.  [流动性挖掘](https://docs.aave.com/developers/guides/liquidity-mining)—也称为[、【产出农业】](https://chain.link/education/defi/yield-farming)，流动性挖掘是一种 DeFi 机制，它使用户能够以治理或某种其他类型的令牌的形式获得奖励，为协议提供流动性。

然而，为了让我们存放一些代币，我们必须`approve`智能合约来从我们的钱包中取出代币。记住，我们要把我们的 WETH 作为抵押品。

```
approve_erc20(amount, lending_pool.address, erc20_address, account)

```

让我们看看我们的`approve_erc20`函数。

```
def approve_erc20(amount, lending_pool_address, erc20_address, account):
   print("Approving ERC20...")
   erc20 = interface.IERC20(erc20_address)
   tx_hash = erc20.approve(lending_pool_address, amount, {"from": account})
   tx_hash.wait(1)
   print("Approved!")
   return True

```

*   `amount`:er C20 的多少，以 wei 为单位，允许协议使用。
    *   `wei`是区块链世界最小的计量单位。
    *   [1 ETH = = 100000000000000000 Wei](https://eth-converter.com/)
*   `lending_pool_address`:借贷池的地址。
*   `erc20_address`:ERC 20 令牌的地址。
*   我们想要交易的账户。

在使用 ERC20 令牌时，如果我们希望从我们的钱包中“拿出”另一份合同，我们必须首先批准该合同。我们调用 ERC20 契约上的`approve`函数(我们的 wet)，然后我们“等待”该事务继续进行。

```
tx_hash.wait(1)

```

既然我们已经批准了合同，我们可以将`lending_pool`合同中的抵押品放回我们的主函数中。

```
print("Depositing...")
   lending_pool.deposit(erc20_address, amount, account.address, 0, {"from": account})
   print("Deposited!")

```

我们可以在这里看到，我们调用契约上的`deposit`函数，我们给它:

*   要存放的令牌(在我们的例子中是 wet)
*   `amount`:存入的金额，单位为魏。
*   我们想贷款给谁，在这个例子中是我们。
*   `0`:这是推荐代码(折旧，总是用 0)

我们可以从 [Aave 文档中了解更多关于智能合约中的`deposit`功能。](https://docs.aave.com/developers/the-core-protocol/lendingpool#deposit)

现在事情变得非常酷了:如果你正确地完成了这一部分，你将得到一个事务散列，它将向你展示正在发生的事情。让我们看看 Etherscan 上的 [Kovan Testnet 上的一个例子。](https://kovan.etherscan.io/tx/0x05f8d009652f52fcc1d519f074cd78fcf179bd48316b2a2a6691edc5d3dec224)



![Getting aTokens from Aave.](img/e962379e7d151bf9f4c2344b3ced1e0f.png)

<figcaption id="caption-attachment-2085" class="wp-caption-text">从 Aave</figcaption>



到 T5】

让我们仔细想想发生了什么事。如果我们查看`Tokens Transferred`部分，我们可以看到 1 笔存款交易发生了 3 笔交易。依次是:

*   一些 [aToken](https://aave.com/aTokens/) 是为我们创造的存款(aWETH)
*   我们向`lending_pool`合同发送了 1 WETH(这是我们的存款)
*   我们被送来一些 aToken

因此，中间的令牌转移是有意义的——我们向贷款池发出了一些信号。这是有道理的。但是其他的代币是什么呢？

阿托肯是一种计息代币，在存款时铸造，赎回时燃烧。所以，当你把存款取出来时，你就烧掉了你的阿托肯，换来了等值的基础资产。aTokens 最酷的地方在于它们每一秒钟都在升值！余额上升是因为人们在使用 Aave 协议并借用你的资产，所以你得到了回报！

您可以[查看某人的余额](https://kovan.etherscan.io/token/0x87b1f4cf9bd63f7bbd3ee1ad04e8f52540349347?a=0x643315c9be056cdea171f4e7b2222a4ddab9f88d)并每隔几秒钟刷新一次，以实时查看余额上升情况。

每当我们想要赎回我们的财富时，无论我们拥有多少财富，我们都会把它烧掉。

与 WETH 令牌相同，您现在可以在元掩码钱包中看到 WETH。只要进入你的元掩码，做我们上面做的添加令牌部分，但是使用 Kovan WETH 地址`0x87b1f4cf9bd63f7bbd3ee1ad04e8f52540349347`。

## 抵押借款/获得贷款

既然我们有一些抵押存款，我们可以申请贷款。我们为什么要贷款呢？

*   无摩擦卖空
*   在不平仓的情况下获得流动性

你可以借入一项资产，以保持对基础抵押品的敞口，同时也可以用另一项资产进行交易或支付。只要确保你的健康系数在 1 以上。



![DeFi health factor equation.](img/37324c28c068e3fb0503e39a64c794fe.png)

<figcaption id="caption-attachment-2086" class="wp-caption-text">DeFi 健康因子方程。</figcaption>



<figcaption></figcaption>



你的健康系数是你贷款的抵押品数量。假设我存了 1 ETH，借了 0.5 ETH。如果清算阈值是 1，那么我的健康系数就是 2。

[来自 Aave:](https://docs.aave.com/risk/asset-risk/risk-parameters#liquidation-threshold)

> 清算阈值是贷款被定义为抵押不足的百分比。例如，80%的清算阈值意味着，如果抵押品的价值超过 80%,则贷款是抵押不足的，可以被清算。

但假设我有 2 个 ETH 借，1 个 ETH 做抵押，1 个作为清算门槛。我的健康系数会是 0.5，我会被要求平仓。在这种情况下，清算人代表借款人偿还部分或全部未偿借款金额，同时**收到抵押品**的折扣金额作为回报(也称为清算“奖金”)。清算人可以决定他们是否希望获得同等数量的抵押品，或者直接获得基础资产。当清算成功完成时，头寸的健康系数增加，使健康系数高于 1。

这样，方案保持[溶剂](https://www.investopedia.com/terms/s/solvency.asp)。所以保持贷款健康！

为了用我们的抵押品借款，我们首先要衡量我们有多少抵押品。我们可以调用`lending_pool`上的`getUserAccountData`函数来找出答案。

我们把它包装成一个名为`get_borrowable_data`的函数

```
borrowable_eth, total_debt_eth = get_borrowable_data(lending_pool, account)

```

。

。

。

```
def get_borrowable_data(lending_pool, account):
   (
       total_collateral_eth,
       total_debt_eth,
       available_borrow_eth,
       current_liquidation_threshold,
       tlv,
       health_factor,
   ) = lending_pool.getUserAccountData(account.address)
   available_borrow_eth = Web3.fromWei(available_borrow_eth, "ether")
   total_collateral_eth = Web3.fromWei(total_collateral_eth, "ether")
   total_debt_eth = Web3.fromWei(total_debt_eth, "ether")
   print(f"You have {total_collateral_eth} worth of ETH deposited.")
   print(f"You have {total_debt_eth} worth of ETH borrowed.")
   print(f"You can borrow {available_borrow_eth} worth of ETH.")
   return (float(available_borrow_eth), float(total_debt_eth))

```

`getUserAccountData`退货:

*   总抵押贷款
*   totalDebtETH
*   可用 BorrowsETH
*   currentLiquidationThreshold
*   Ltv
*   健康因素

你可以在[的 Aave 文档](https://docs.aave.com/developers/the-core-protocol/lendingpool#getuseraccountdata)中了解这些技术的作用。我们将只关注`available_borrow_eth`和`total_debt_eth`，这样我们就会知道:

*   我们能借多少
*   我们目前有多少债务

## 等等……为什么我没有成交？

您可能已经注意到，这是对智能合约进行函数调用，我们刚刚在上面说过，为了调用函数，我们必须进行事务处理，这是什么原因呢？嗯，有两种类型的智能合约功能，您不需要进行交易就可以调用。

1.  查看功能
2.  纯函数

这些函数不会修改区块链的状态，所以我们可以调用它们，因为我们只是在读取智能合约的状态。记住，只有当你修改区块链的州名时，才需要花费汽油。

回到贷款。

每项资产都有不同的[贷款对借款](https://docs.aave.com/risk/asset-risk/risk-parameters)比率，它告诉你的清算阈值，以便你借入一项资产。

一旦我们得到我们可以借多少，我们就可以借！

```
borrowable_eth, total_debt_eth = get_borrowable_data(lending_pool, account)
print(f"LETS BORROW IT ALL")
erc20_eth_price = get_asset_price()
amount_erc20_to_borrow = (1 / erc20_eth_price) * (borrowable_eth * 0.95)
print(f"We are going to borrow {amount_erc20_to_borrow} DAI")
borrow_erc20(lending_pool, amount_erc20_to_borrow, account)

```

## 获得可借款资产价值

现在，当我们借款时，我们被告知我们拥有的资产数量。然而，也许我们要借用一个不同的令牌，像戴。如果要用 ETH 做抵押借 DAI，首先要得到 ETH 的转化率-> DAI。

[Chainlink](https://docs.chain.link/docs/get-the-latest-price/) 是在 DeFi 和智能合约生态系统中获取数据和执行外部计算的标准，也是 Aave 用来获取费率的标准！他们有一个 [Price Oracle](https://docs.aave.com/developers/the-core-protocol/price-oracle) 部分，描述了如何通过他们的智能合约 API 获取 Chainlink 数据。如果你学会了使用 Chainlink 数据，你可以跨协议使用它，即使他们没有使用 Chainlink，或者没有价格 oracle 机制！

Chainlink 通过一个分散的 [oracle](https://chain.link/education/blockchain-oracles) 网络获取数据，在该网络中，多个节点通过许多 API 和服务聚集数据，以获得一个分散的真实来源，该来源在链上被验证和记录以供我们使用。我们可以在 [data.chain.link](https://data.chain.link/) 页面或[文档](https://docs.chain.link/docs/ethereum-addresses/)上看到当前可用数据的列表。如你所知，数据是大多数量化系统、算法交易者和整个 DeFi 生态系统的支柱，所以你要始终确保你是从一个分散的系统中提取的，这样你就可以得到最准确、最可靠、最安全的数据。

此外，如果没有你想要的数据，你可以[从任何 API](https://docs.chain.link/docs/make-a-http-get-request/) 调用你的智能合约，[获得可证明的随机数](https://docs.chain.link/docs/get-a-random-number/)，以及许多其他不同的服务。这些使得智能合同数据馈送安全、可靠且分散。

但是让我们回到蟒蛇身上！

我们有一个名为`get_asset_price`的函数，它从`dai_eth_price_feed`中读取数据，就像这样:

```
def get_asset_price():
   # For mainnet we can just do:
   # return Contract(f"{pair}.data.eth").latestAnswer() / 1e8
   dai_eth_price_feed = interface.AggregatorV3Interface(
       config["networks"][network.show_active()]["dai_eth_price_feed"]
   )
   latest_price = Web3.fromWei(dai_eth_price_feed.latestRoundData()[1], "ether")
   print(f"The DAI/ETH price is {latest_price}")
   return float(latest_price)

```

我们从接口中获取的链接契约`AggregatorV3Interface`,已经存储在我们的配置文件中。在那个契约上，我们调用了`latestRoundData`函数。

您会注意到，我们也不需要为此进行交易，这也是一个视图功能！

另一种方式，你会看到人们用布朗尼链接数据饲料价格是:

```
from brownie import Contract

print(Contract(f"{pair}.data.eth").latestAnswer() / 1e8)

```

这使用 [ENS](https://ens.domains/) 来获得价格对的地址。ENS 是一种获取智能合同地址并使其可读的方法。例如，您可以这样做:

```
print(Contract(f"eth-usd.data.eth").latestAnswer() / 1e8)

```

获取以太坊的最新美元价格。请注意，ENS 只在 mainnet 网络上工作，所以当您运行 brownie 时，您必须使用`--network mainnet`或`--network mainnet-fork`。

## 将值转换为借款

既然我们已经有了抵押品和我们想借的资产之间的转换率，我们可以设置一个变量来确定我们想借多少。

```
amount_erc20_to_borrow = (1 / erc20_eth_price) * (borrowable_eth * 0.95)

```

我们得到 ETH/DAI 价格的倒数，并乘以我们可以借多少(单位为 ETH)。安全起见，我们还将其乘以 0.95。然后，我们调用 borrow 函数！

```
borrow_erc20(lending_pool, amount_erc20_to_borrow, account)

```

。

。

。

```
def borrow_erc20(lending_pool, amount, account, erc20_address=None):
   erc20_address = (
       erc20_address
       if erc20_address
       else config["networks"][network.show_active()]["aave_dai_token"]
   )
   # 1 is stable interest rate
   # 0 is the referral code
   transaction = lending_pool.borrow(
       erc20_address,
       Web3.toWei(amount, "ether"),
       1,
       0,
       account.address,
       {"from": account},
   )
   transaction.wait(1)
   print(f"Congratulations! We have just borrowed {amount}")

```

希望现在你已经掌握了窍门。borrow 函数有几个参数:

*   资产的地址(在我们的例子中，是 DAI 令牌)
*   我们要借的金额，以魏为单位
*   `interestRateMode`，(0，1，2: 1 是稳定的，2 是可变的…现在不用担心 0)
*   推荐代码(忽略)
*   `onBehalfOf`价值，也就是谁将承担债务

让我们来看看 Etherscan 上的这个[事务的示例，以理解刚刚发生了什么。](https://kovan.etherscan.io/tx/0x07b07852de7ac7cf492b34e0c929c65f38f1f83bf5953c14011ba9f659475247)



![Borrowing DAI on Aave](img/6405aa6d29c300ddb6f4e7bfc27d885b.png)

<figcaption id="caption-attachment-2087" class="wp-caption-text">借戴上 Aave</figcaption>



T5】

按顺序，`Tokens Transferred`动作是:

*   Aave 协议是在某一天制定的
*   我们的钱包被铸造了一些
*   我们的钱包变得有些戴

重要提示:Aave 有时会改变它的 testnet 令牌。通过检查[部署的合同地址，确保您有正确的 testnet DAI 地址。](https://docs.aave.com/developers/deployed-contracts/deployed-contracts)并查看[官方 JSON 列表。](https://aave.github.io/aave-addresses/kovan.json)

这一次，我们得到了一种不同类型的有息代币，一种债务代币。这就是我们将要偿还的金额，和阿托肯一样，它也在升值。如果你欠了更多的债务(由这个债务代币象征)，有人可以清算你，拿走你所有的抵押品！所以要警惕你有多少债务。

通过添加新的令牌地址，我们可以在元掩码中再次看到借用的资产。我们还可以通过添加债务令牌地址来查看我们的债务。

这才是真正有趣的地方。卖空最简单的方法之一就是现在就卖掉我们的资产。如果资产价格下跌，我们必须偿还的比我们借的少。在这里，你的创造力没有限制！

然而，我越来越担心我会被清算。让我们偿还我们的债务。

## 偿还我们的债务

到目前为止，您已经掌握了窍门。我们想算出我们欠了多少钱，然后再还！我们可以通过这些函数来实现:

```
borrowable_eth, total_debt_eth = get_borrowable_data(lending_pool, account)
amount_erc20_to_repay = (1 / erc20_eth_price) * (total_debt_eth * 0.95)
repay_all(amount_erc20_to_repay, lending_pool, account)

```

。
。
。

```
def repay_all(amount, lending_pool, account):
   approve_erc20(
       Web3.toWei(amount, "ether"),
       lending_pool,
       config["networks"][network.show_active()]["aave_dai_token"],
       account,
   )
   tx = lending_pool.repay(
       config["networks"][network.show_active()]["aave_dai_token"],
       Web3.toWei(amount, "ether"),
       1,
       account.address,
       {"from": account},
   )
   tx.wait(1)
   print("Repaid!")

```

有点啰嗦，但如果做得正确，你应该大部分付清！

## 摘要

我们已经经历了使用 Aave 的所有步骤。

1.  存款抵押品
2.  申请贷款
3.  偿还它

呜！你将成为区块链金融科技专家！您接下来需要做的一些步骤是:

1.  通过 [Synthetix](https://synthetix.exchange/) 或 [Bancor](https://bancor.network/) 等协议进行资产交易
2.  拿出一笔[闪贷](https://github.com/brownie-mix/aave-flashloan-mix)
3.  学习如何[入股](https://app.aave.com/staking)并参与[治理](https://governance.aave.com/)

还有更多！您还可以学习如何成为一名智能合约开发人员，[在 Solidity 中构建分散式协议](https://docs.chain.link/docs/beginners-tutorial/)，并发现智能合约的广泛功能。你的旅程才刚刚开始！

事情是这样的:我们在本教程中所做的一切——存放抵押品、贷款、还款——您也可以通过 Aave UI 来完成！ui 很棒，但是它们不能像编程那样给我们灵活的创造力和复杂的量化方法。

**关于这个话题的更多信息**

*   [如何获取以太坊、比特币和其他加密货币的当前价格](https://blog.chain.link/fetch-current-crypto-price-data-solidity/)
*   [获取 Solidity 智能合约中的外汇汇率](https://blog.chain.link/fetch-foreign-exchange-rates-in-solidity-smart-contracts/)
*   [获取 Solidity 智能合约中的商品价格](https://blog.chain.link/fetch-commodity-prices-in-solidity-smart-contracts/)
*   [获取可靠智能合约的指数价格](https://blog.chain.link/get-index-prices-in-solidity-smart-contracts/)
*   [智能合同开发者使用 Chainlink 的主要方式](https://blog.chain.link/smart-contract-api-price-random/)

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink) | [不和](https://www.reddit.com/r/Chainlink/)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://defi.chain.link/)