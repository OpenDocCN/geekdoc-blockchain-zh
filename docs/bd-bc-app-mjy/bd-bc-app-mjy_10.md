## 一. 开始使用 CyberMiles

CyberMiles 是一个支持委托权益证明（DPoS）共识的以太坊兼容公共区块链。虽然它为以太坊生态系统带来了许多功能增强，但它也可以作为一个更快、更便宜、更可靠的以太坊区块链替代品。所有以太坊智能合约都可以在 CyberMiles 区块链上无需修改地运行。此外，CyberMiles 生态系统拥有易于使用的开发者工具，这些工具是其以太坊对应工具的改进版本。因此，CyberMiles 是你学习以太坊协议和开始应用开发的不错选择。

虽然有许多工具可以帮助您快速开始在 CyberMiles 公共区块链上使用 Lity 智能合约和 dapp 开发，但为了真正了解区块链如何工作，您应该启动一个节点并将其与区块链网络同步。节点可以在服务器上运行，甚至可以在需要时在您自己的笔记本电脑上运行。在本附录中，我将描述如何使用 Docker 运行 CyberMiles 节点以及如何使用命令行工具与节点交互。

### 部署 Node

部署 CyberMiles 节点的最快方法是使用 Docker 获取最新的节点软件并使用快照获取最新的区块链数据。以下说明将指导你如何构建一个 CyberMiles 测试网节点。首先，你必须安装 Docker 软件：[`docs.docker.com/install/`](https://docs.docker.com/install/)。

在 Docker Hub 上存储了用于 Travis 的 Docker 镜像。测试网环境使用 `vTestnet` 版本，可以从 Travis 自动拉取。

请点击此处查看代码图片

```
docker pull cybermiles/travis:vTestnet
```

接下来，让我们将区块链配置和数据下载到本地目录 `$HOME/.travis` 中，这样我们就可以将其对 Docker 容器可见。配置文件在这里：

请点击此处查看代码图片

```
$ rm -rf $HOME/.travis && mkdir -p $HOME/.travis/config
$ curl https://raw.githubusercontent.com/CyberMiles/testnet/
master/travis/init/config/config.toml > $HOME/.travis/config/config.toml
$ curl https://raw.githubusercontent.com/CyberMiles/testnet/
master/travis/init/config/genesis.json > $HOME/.travis/config/genesis.json
```

你应该编辑 `config.toml` 文件，将节点名称更改为你自己的。

请点击此处查看代码图片

```
$ vim ~/.travis/config/config.toml
# here you can change your name
moniker = "<your_custom_name>"
```

然后，从这里下载最新的区块数据快照：

请点击此处查看代码图片

```
$ wget $(curl -s http://s3-us-west-2.amazonaws.com/travis-ss-testnet/
latest.html)
```

解压 tar 文件，并将 `data` 和 `vm` 子目录从解压缩的目录复制到 `$HOME/.travis`。最后，通过将本地计算机的 `$HOME/.travis` 目录映射到 Docker 容器的 `/travis` 目录来启动 Docker 容器。

请点击此处查看代码图片

```
$ docker run --name travis -v $HOME/.travis:/
travis -t -p 26657:26657 cybermiles/travis:vTestnet node start --home
/travis
```

你可以使用类似的过程启动 CyberMiles 主网节点。唯一不同的是配置和区块链数据下载 URL。你可以在 [`travis.readthedocs.io/en/latest/connect-mainnet.html`](https://travis.readthedocs.io/en/latest/connect-mainnet.html) 了解更多。

### 在 Node 上进行交互式控制台

一旦 CyberMiles 节点与区块链同步，你可以使用 Travis 程序连接到它，并向网络发送命令和交互。你只需要将`travis`命令附加到节点。以下命令应该在运行 Docker 的同一台计算机上运行：

点击此处查看代码图片

```
$ docker exec -it travis bash
> ./travis attach http://localhost:8545
```

**注意**

当你启用`personal`模块时，永远不要将端口 8545 暴露在防火墙外。如果你这样做，黑客将能够窃取存储在节点上的所有加密货币。

Travis 在新终端中打开一个交互式控制台，你可以使用`web3-cmt` JavaScript API 来访问区块链。例如，以下命令将在这个网络上创建一个新的账户来持有虚拟货币。只需重复几次`newAccount()`命令，你将在`cmt.accounts`列表中看到几个账户。如早前所述，每个账户都包含一对私钥和公钥。在涉及此账户的每笔交易中，只记录公钥在区块链上。

点击此处查看代码图片

```
> personal.newAccount()
Passphrase:
Repeat passphrase:
"0x7631a9f5b7af9705eb7ce0679022d8174ae51ce0"
> cmt.accounts
["0x7631a9f5b7af9705eb7ce0679022d8174ae51ce0", ...]
```

当你从 Travis 控制台创建或解锁账户时，账户的私钥存储在与附加节点文件系统上的 keystore 文件中。然后，你可以将一些 CMT 从一个账户发送到另一个账户。或者，如果你的节点在测试网 上，你还可以从[`travis-faucet.cybermiles.io/`](https://travis-faucet.cybermiles.io/)获取一些测试网 CMT。

点击此处查看代码图片

```
> personal.unlockAccount("0x7631a9f5b7af9705eb7ce0679022d8174ae51ce0")
Unlock account 0x7631a9f5b7af9705eb7ce0679022d8174ae51ce0
Passphrase:
true
> cmt.sendTransaction({from:"0x7631a9f5b7af9705eb7ce0679022d8174ae51ce0",
to:"0xfa9ee3557ba7572eb9ee2b96b12baa65f4d2ed8b", value: web3.toWei(0.05,
"cmt")})
"0xf63cae7598583491f0c9074c8e1415673f6a7382b1c57cc9b06cc77032f80ed3"
```

最后一行是向两个账户之间发送 0.05 CMT 的交易 ID。在下一个例子中，让我们看看如何构建并部署智能合约，然后调用其函数。

要从源代码构建智能合约，你可以使用 Europa 集成开发环境（IDE）。或者，你可以使用命令行`lityc`编译器，它比 Europa 提供更多高级功能，如安全和合规性检查（参见第十五章）。目标是一样的：从 Lity/Solidity 源代码生成应用程序二进制接口（ABI）和字节码，以便它们可以部署在区块链上。让我们看看如何为此目的使用`lityc`。你可以按照[`lity.readthedocs.io/`](https://lity.readthedocs.io/)的说明安装`lityc`。以下命令从`HelloWorld.lity`源代码生成字节码和 ABI 定义：

点击此处查看代码图片

```
$ lityc --bin HelloWorld.lity
======= ./HelloWorld.lity:HelloWorld =======
Binary:
608060405234...
$ lityc --abi HelloWorld.lity
======= ./HelloWorld.lity:HelloWorld =======
Contract JSON ABI
[ { "constant": false, "inputs": [], "name": "kill",
"outputs": [], "payable": false, "stateMutability": "nonpayable",
"type": "function" }, { "constant": false, "inputs": [ {
"name": "_new_msg", "type": "string" } ], "name": "updateMessage",
"outputs": [], "payable": false, "stateMutability": "nonpayable",
"type": "function" }, { "inputs": [], "payable": false, "stateMutability":
"nonpayable", "type": "constructor" }, { "constant": true, "inputs": [],
"name": "owner", "outputs": [ { "name": "", "type": "address" } ],
"payable": false, "stateMutability": "view", "type": "function" }, {
"constant": true, "inputs": [], "name": "sayHello", "outputs": [ {
"name": "", "type": "string" } ], "payable": false, "stateMutability":
"view", "type": "function" } ]
```

在 Travis 控制台上，你现在可以部署 CyberMiles 区块链上的合约字节码和 ABI。

点击此处查看代码图片

```
> personal.unlockAccount(cmt.accounts[0],'1234');
> bytecode="0x608060..."
> abi = ... the ABI output ...
> contract = web3.cmt.contract(abi);
> contractInstance = contract.new(
   {
     from: web3.cmt.accounts[0],
     data: bytecode,
     gas: "4700000"
   },
   function(e, contract) {
     console.log("contract address: " + contract.address);
     console.log("transactionHash: " + contract.transactionHash);
   }
 );
```

一旦合约在区块链上部署并获得确认，你将在控制台上看到其合约地址。你现在可以调用其函数。

点击此处查看代码图片

```
> contractInstance.sayHello.call({from: cmt.accounts[0]})
Hello World
> contractInstance.updateMessage.call("Hi", {from: cmt.accounts[0]})
```

另外，您还可以从其部署地址获取合约实例，然后调用其函数。

点击此处查看代码图片

```
> contractInstance = web3.cmt.contract(abi).at("0x1234ABCD...");
```

Travis 控制台为用户提供可靠且互动的 CyberMiles 区块链访问方式。我们强烈建议您熟悉并使用它来探索区块链。

### 结论

CyberMiles 区块链针对电子商务应用进行了优化。它与以太坊区块链完全兼容，但速度更快、成本更低、更安全。它拥有完整的一套开发和部署工具，以促进智能合约和 dapp 的开发。因此，CyberMiles 区块链是开始以太坊应用开发和更广泛应用的绝佳选择。
