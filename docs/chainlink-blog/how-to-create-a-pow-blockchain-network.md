# 如何创建一个电力区块链网络

> 原文：<https://blog.chain.link/how-to-create-a-pow-blockchain-network/>

有没有想过如何创建自己的区块链网络？

虽然以太坊和比特币之类的网络是大型公共网络，但你可以使用以太坊客户端为自己的目的建立一个新的私人区块链网络(在这种情况下，私人并不意味着受保护或安全，而是保留或隔离)。

在本教程中，你将学习如何开始使用以太坊的 Go 语言实现 [Geth](https://geth.ethereum.org/) 创建自己的区块链网络。

## 安装 Geth

安装 Geth 有几种方法:

*   使用包管理器
*   下载独立的预构建包
*   在 docker 容器中运行它
*   自己动手建造

您的电脑、操作系统和先前的知识会影响您的选择。查看 [官方文档](https://geth.ethereum.org/docs/install-and-build/installing-geth) 了解如何安装 Geth。

### 检查是否安装了 Geth

您可以通过检查版本来检查您是否安装了 Geth 客户端。

在终端中，运行这个命令。如果它运行并返回您正在使用的版本的详细信息，则 Geth 已经成功安装:

```
geth version
```

### 获取帮助

Geth 附带了一个有用的`help`命令，可以这样运行:

```
geth --help
```

![A screenshot showing the result of running geth --help](img/7a5cc3324fdc8a6bb9bbb253bd0946d0.png)

### 运行 Geth

默认情况下，Geth 运行一个 mainnet 节点，它将开始为以太坊 mainnet 下载整个数据库。

如果你的目标是使用 Geth 创建你自己的区块链，不要在没有指定参数的情况下运行`geth`。

## 共识算法

以太坊主网使用工作证明(PoW) `ethash`来保护区块链。可以使用相同的一致算法创建私有区块链。

Geth 还支持“小团体”授权证明(PoA)共识算法，作为专用网络的替代方案，在专用网络中，新块只能由授权的“签名者”创建。授权签名者的初始列表在 genesis 块中配置。在[【EIP】-225](https://eips.ethereum.org/EIPS/eip-225)中指定了小团体共识协议。

在本教程中，我们将使用 PoW consensus 算法来演示挖掘过程。

## 区块链网络文件夹

让我们在文件夹`C:\ETH\LocalNode`中创建区块链网络。以下示例适用于 Windows 操作系统。

在命令提示符下，运行以下命令:

```
cd C:\ETH
mkdir LocalNode
cd LocalNode
```

## 用 Geth 创建一个本地节点

安装完 Geth 客户端后，下一步是创建一个本地节点。

为了创建您的区块链网络，网络中所有参与的计算机都必须完成此步骤。

### 创世纪文件

每个区块链都是从创世纪开始的。这是一个特殊的 genesis.json 文件，为创建您的区块链网络而定制。

在您选择的文本编辑器中，创建一个名为 genesis.json 的文件。

复制并粘贴此配置:

```
{
    "config": {
        "chainId": 9183,
        "homesteadBlock": 0,
        "eip150Block": 0,
        "eip155Block": 0,
        "eip158Block": 0,
        "byzantiumBlock": 0,
        "constantinopleBlock": 0,
        "petersburgBlock": 0
 },
    "difficulty": "0x1",
    "gasLimit": "8000000",
    "alloc": {}
}
```

### 了解参数

当您创建自己的区块链网络时，需要了解一些与参数相关的重要注释。

#### 链锯

在我们的区块链网络中，`chainID`将与网络 ID 相同，这是一个隔离以太坊对等网络的整数。

只有当两个对等体使用相同的 genesis 块和`chainID`时，区块链节点之间的连接才会发生。为了创建一个专用区块链网络，您必须使用一个尚未使用过的号码。你可以在[https://chainid . network](https://chainid.network/)找到以太网的社区运行注册表。

主网络的 ID 为“1”。如果您提供不同于主网络或其他已知网络的自定义网络 ID，您的节点将不会连接到其他节点，而会加入专用的区块链网络。

注意:创世纪文件中的`chainId`对于这个区块链网络中的所有参与者必须是相同的。在我们的网络中，`chainId`是 9183。

关于这个你可以在 [文档](https://geth.ethereum.org/docs/interface/private-network) 中找到更多。

#### 难度

注意`difficulty`是如何被设置得非常低，只有 1。

#### 气体极限

这是初始阻塞气体限值(`gasLimit`)。它影响单个块中可以进行多少 EVM 计算。

### 初始化你的区块链

在终端中进入创建 genesis.json 文件的文件夹，然后 运行这个命令初始化一个新的区块链:

```
geth init --datadir data genesis.json
```

区块链的数据库将位于`data` : 文件夹中

![Screenshot of the result of running geth init](img/de4104e5461f27f3eefd85f2334cc590.png)

## 运行 Geth

下面的命令将启动客户端节点:

```
geth --datadir ".\data" --networkid 9183 --identity "Node1"
```

您应该会看到类似如下的输出:

![Screenshot showing the output of a command to start the client node](img/ecd503ac2a2fdde9ffee4bcb24a95f3a.png)

如果您收到错误消息“快照扩展注册失败”,则错误在另一个对等端，并且现在您在网络中是单独一人——该对等端将被丢弃。你的节点工作正常，你不用担心。

### IPC 路径

稍后将使用 IPC 路径连接到您的节点，因此请记下它。

![Screenshot of IPC path](img/720af2a358c12f631a0acf46714a69d3.png)

在本例中，IPC 路径为:

```
\\.\pipe\geth.ipc
```

## Geth JavaScript 控制台

Geth 有一个 [JavaScript 控制台](https://geth.ethereum.org/docs/interface/javascript-console) ，可以在 Geth 节点中使用，向其发送命令。下面是如何使用`geth attach`命令连接到一个已经在运行的 Geth 本地节点，并在其中运行一些命令。

### 使用 IPC 进行连接

打开第二个终端窗口。

执行节点时可以获得 IPC 路径(你在上一步收到了)。

运行该命令:

```
geth attach ipc:\\.\pipe\geth.ipc
```

这是结果:

![Screenshot of the output of geth attach ipc:\\.\pipe\geth.ipc](img/da9dfd830cd12f139d0d0c5c4c47b54f.png)

#### 警告

该程序仅适用于在您的机器或您有权访问的网络上运行的节点。让您完全控制远程实例，所以不要指望其他人会让您这样访问他们的机器。

### 创建账户

每个节点必须至少有一个账户，尤其是如果要获得矿工奖励的话。在连接的 Geth 终端中，运行下面的命令:

```
personal.newAccount("yourpassword")
```

“您的密码”文本是用于加密您的私钥的密码。如果您忘记了，您将无法再使用您的帐户。

![Screenshot showing the output of personal.newAccount("yourpassword")](img/8240e9b7c83df77bc713560ea0e6aae8.png)

在 Node1 上创建的账户是`0xe3badc04240a4fa99e758e030024560bde46ea11`。

## 创建第二个节点

本教程的目的是创建一个网络，在同一台计算机内运行两个 Geth 节点，连接到不同的端口。

让我们创建第二个节点，Node2。

以下是我们将在节点 2 中使用的信息:

*   数据目录:数据 2
*   监听端口:30305
*   ipc 路径:geth2
*   身份:节点 2

现在让我们在文件夹`C:\ETH\LocalNode2`中创建第二个节点。

重要的是要记住这个例子使用的是 Windows 操作系统——如果你使用的是另一个操作系统，你需要做相应的调整。

在命令提示符下，运行:

```
cd C:\ETH
mkdir LocalNode2
cd LocalNode2
```

最终路径为`C:\ETH\LocalNode2`。

### Geth Init Node2

将 genesis.json 文件从 LocalNode1 复制到 LocalNode2。

运行此命令初始化节点 2:

```
geth init --datadir data2 genesis.json
```

区块链的数据库将位于文件夹`data2`中。

## `geth attach`使用节点 2 的 IPC

我们已经定义了节点 2 将拥有`geth2` IPC。

IPC 路径也可以在节点执行时获得。像对 Node1 一样，在 IPC path 中检查它。

打开第二个终端窗口，运行以下命令:

```
geth attach ipc:\\.\pipe\geth2.ipc
```

## 为节点 2 创建帐户

Node2 还必须至少有一个帐户。在连接的 Geth 终端中，运行下面的命令:

```
personal.newAccount("yourpassword")
```

“您的密码”文本是用于加密您的私钥的密码，如果您忘记了，您将无法再使用您的帐户。

![Screenshot of the output of personal.newAccount("yourpassword")](img/57a6655157cfe60e1eb1fe38c08d3310.png)

node 2 上的账户是`0x4d11a54211f8a5a83ea2275aa0065f3eef4f623c`。

# 配置区块链网络

为了创建您的区块链网络，您需要知道您的一个节点的`enode`，以便您的节点可以相互通信。

## 来自节点 2 的 Enode】

在运行`geth attach`的终端中，连接到 Node2，运行该命令发现`enode` :

```
admin.nodeInfo.enode
```

这是节点 2 的`enode`:

```
"enode://b9b9200ee68b324f0b4486cd9719f876763a3b9c8c9fe9cfe20a13221055472b6[[email protected]](/cdn-cgi/l/email-protection)89.20.185.250:30305"
```

我们的目标是在同一台计算机上设置运行 Geth 节点的区块链网络，因此我们将 IP 更新为本地 IP:

```
127.0.0.1
```

更新 IP 后，node2 的`enode`应该是:

```
"enode://b9b9200ee68b324f0b4486cd9719f876763a3b9c8c9fe9cfe20a13221055472b6[[email protected]](/cdn-cgi/l/email-protection)127.0.0.1:30305"
```

### 使用不同的电脑

在本教程中，我们创建了一个在同一台计算机内通过不同端口运行两个 Geth 节点的网络，如果您想使用不同的计算机创建您的区块链网络，您需要知道每台计算机的 IP。

建立点对点网络取决于您的需求。如果您通过互联网连接节点，您需要确保您的 bootnode 和所有其他节点都分配了公共 IP 地址，并且 TCP 和 UDP 流量都可以通过防火墙。

## 连接节点

让我们运行我们的区块链网络吧！

到 Node1 中运行`geth attach`的终端，为 Node2 添加`enode`。

更新命令`admin.addPeer`中的`enode2`。

```
admin.addPeer("enode")
```

像这样:

```
admin.addPeer("enode://b9b9200ee68b324f0b4486cd9719f876763a3b9c8c9fe9cfe20a13221055472b6[[email protected]](/cdn-cgi/l/email-protection)127.0.0.1:30305")
```

这是结果:

![Screenshot of the output of admin.addPeer](img/b6241893037d051c3460058e4d570eaf.png)

搞定！现在一个节点知道另一个节点的存在。

## 验证网络

### net.peerCount

这个命令告诉你有多少节点连接到你的。

在任何 Geth 连接的终端中，您可以运行:

```
net.peerCount
```

结果应该是`1`，因为我们有一个节点连接在另一个节点上，如下图所示:

节点 1

![Node1](img/af5d68ec2c4c5497eb663ec2f753128e.png)

节点 2

![Node2](img/9c65fa78a777c5b36e2c55b0fa7118f3.png)

### 管理员同行

该命令显示了连接到您的节点的其他节点的详细信息。在 Geth 连接的终端中运行:

```
admin.peers
```

您可以看到节点 2 连接到节点 1:

![Screenshot showing Node2 connected to Node1](img/60c3dd3948f75b6bf113ec1a7f47c617.png)

并且节点 1 连接到节点 2:

![Screenshot showing Node1 connected to Node2](img/9f154134bc7294142e0e7a47ecf466cf.png)

## 账户

让我们来了解更多与账户相关的命令。

### 个人

该命令列出一个节点中所有账户的详细信息。

```
personal
```

这是节点 1 的结果:

![Screenshot of the result of running personal](img/996f8c8bf71fc500c5e29521d002c18a.png)

### 平衡

这个命令获取一个账户的余额:

```
eth.getBalance(eth.accounts[0])
```

如果我们运行这个命令，我们将得到一个很大的结果，因为这个结果是以 wei 命名的。让我们转换成以太:

```
web3.fromWei(eth.getBalance(eth.accounts[0]),"ether")
```

![Screenshot of the result of running web3.fromWei(eth.getBalance(eth.accounts[0]),ether)](img/33f4f4c4c61734648cb67e6a6ea57d58.png)

### 特定账户余额

让我们使用这个地址: `0x942b17d335321128225d23bd7e8451fe78ce9547`来查看一个账户的余额。

```
web3.fromWei(eth.getBalance("0x942b17d335321128225d23bd7e8451fe78ce9547"),"ether")
```

结果:

![web3.fromWei(eth.getBalance("0x942b17d335321128225d23bd7e8451fe78ce9547"),"ether")](img/da0ad80b5063346a17132f3003e12047.png)

## 采矿

如果我们想在我们的区块链上创建新的区块，就需要对它们进行开采，因为我们使用的是 PoW consensus 算法。

我们已经在网络中配置了两个节点，让我们挖掘并获得一些以太网吧！请记住，这些令牌没有任何价值，它们只存在于我们的私有网络中。

### 开始采矿

在两个节点的 Geth-attached 终端中，运行:

```
miner.start(1)
```

参数`1`是计算机中使用的线程数量。在我们的例子中，我们没有启用并行挖掘线程。默认值是处理器核心的总数。

您可以在这里 了解更多矿业 [。](https://geth.ethereum.org/docs/interface/mining)

### 开采后的余额

在每个 Geth 连接的节点中，几分钟后检查余额。

```
web3.fromWei(eth.getBalance(eth.accounts[0]),"ether")
```

请看下图:节点 2 比节点 1 拥有更多的以太。

![Screenshot showing Node2 has more ether than Node1](img/2fe81868fb6160899a1ebb4d7adba64b.png)

你在两个节点上使用相同的计算能力进行挖掘，所以当第二个开始时，第一个将不再能够通过挖掘获得奖励。

使用不同的计算机安装网络以避免这个问题。

### Geth 出口

要退出任何 geth 控制台，运行:

```
exit
```

## 接下来的步骤

现在你已经创建了自己的 PoW 区块链网络，有许多可能性可供你使用:你可以将以太网从一个节点传输到另一个节点，发布智能合同，或者与其他已发布的智能合同进行交互——尽管考虑到它是私有的，你的网络的效用会受到一定的限制。

访问[chain . link](https://chain.link)或阅读[docs . chain . link](https://docs.chain.link)上的文档，了解更多关于 Chainlink 的信息。 [要讨论一个集成，就去找专家。](https://chainlinkcommunity.typeform.com/to/OYQO67EF?typeform-source=blog.chain.link)