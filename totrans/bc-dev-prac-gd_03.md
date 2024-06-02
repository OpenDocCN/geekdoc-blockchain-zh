© Elad Elrom 2019 Elad Elrom The Blockchain Developer [`doi.org/10.1007/978-1-4842-4847-8_3`](https://doi.org/10.1007/978-1-4842-4847-8_3)

# 3. 创建您自己的区块链

Elad Elrom¹(1)New York, NY, USA 在本章中，我将介绍如何构建您自己的区块链 P2P 网络。这是一个七个步骤的过程，因此在每个部分，我都会先简要介绍，然后进行一个练习。您可以从 GitHub 下载以下每个练习的代码并跟随进行：

+   创建基本 P2P 网络

+   发送和接收块

+   注册矿工和创建新块

+   设置名称-值数据库，LevelDB

+   创建私钥-公钥钱包

+   使用 API 服务

+   创建命令行界面

本章将深入代码，本章中的示例性质简单，旨在用于学习目的。它们将帮助您更好地理解区块链以及实现区块链的完全工作原型的所需元素。

### 注意

在这个简短的教程章节中创建一个完整的生产级区块链是不切实际的；然而，我将为您提供创建基本工作区块链的基础知识。

## 创建基本 P2P 网络

创建区块链的第一个步骤是创建一个 P2P 网络。正如您在之前的章节中看到的那样，P2P 网络是使区块链工作的关键。在加密货币中，P2P 网络可以帮助防止 PoW 的双重支付问题，也是 PoS 背后的核心架构。在区块链中，它允许您在网络上同步所需的数据。

### 注意

点对点（P2P）是一种计算机网络类型，使用分布式架构。每个节点或同伴共享工作负载，与其他同伴平等，意味着不应有任何特权节点。

> “我们提出了一种无需信任的电子交易系统。我们以由数字签名组成的硬币的通常框架开始，这提供了对所有权的强大控制，但如果没有防止双重支付的方法则是不完整的。为此，我们提出了一种使用工作量证明的点对点网络，以记录交易的公共历史，如果诚实的节点控制了大多数 CPU 证明-of-worker，则攻击者很快就会变得计算上不可行。”
> 
> —《比特币：一种点对点电子现金系统》

在本章中，我将向您展示如何使用 Node.js 创建您的区块链，但您可以使用任何其他编程语言来实现，因为原理是相同的。您将使用 WebStorm 集成开发环境（IDE）设置您的机器，该 IDE 将在本书中使用。要下载 WebStorm，请访问 [`www.jetbrains.com/webstorm/`](https://www.jetbrains.com/webstorm/) 。WebStorm 提供 30 天的试用版；然而，这不是必要的，您可以选择喜欢的任何 IDE，并取得相同的结果。在撰写本文时，WebStorm 版本是 2018.2。

### 第一步：基本 P2P 网络练习

**设置你的项目**

在这个练习中，你将设置你的项目并创建一个基础的对等（P2P）网络以发送和接收消息。在你能够发送和接收消息之后，你将能够创建一个区块类和一个链式库，并将几个区块结合起来创建一个区块链。你的机器上需要安装 Node.js；安装方式有很多。一种简单的方式是通过预构建的安装程序管理器；在这里找到适合你平台的安装程序：[`nodejs.org/en/download/`](https://nodejs.org/en/download/)。

下载 WebStorm 后，你可以创建一个新项目。选择文件➤创建新项目➤Node.js Express App➤创建。在位置处，将项目命名为**区块链**，然后点击创建（见图 3-1）。![../images/475651_1_En_3_Chapter/475651_1_En_3_Fig1_HTML.jpg](img/475651_1_En_3_Fig1_HTML.jpg)

图 3-1

WebStorm，创建新项目向导

**创建 P2P 网络**

创建一个名为**区块链**的文件夹。然后创建一个名为 p2p.js 的文件，并写入以下代码。或者，你也可以直接从 GitHub 克隆代码。<https://github.com/Apress/the-blockchain-developer/blob/master/chapter2/step1/p2p.js>git clone <https://github.com/Apress/the-blockchain-developer/chapter3/step1/>const crypto = require('crypto'),    Swarm = require('discovery-swarm'),    defaults = require('dat-swarm-defaults'),    getPort = require('get-port');const peers = {};let connSeq = 0;let channel = 'myBlockchain';const myPeerId = crypto.randomBytes(32);console.log('myPeerId: ' + myPeerId.toString('hex'));const config = defaults({        id: myPeerId,});const swarm = Swarm(config);(async () => {    const port = await getPort();    swarm.listen(port);    console.log('Listening port: ' + port);    swarm.join(channel);    swarm.on('connection', (conn, info) => {        const seq = connSeq;        const peerId = info.id.toString('hex');        console.log(`Connected #${seq} to peer: ${peerId}`);        if (info.initiator) {            try {                conn.setKeepAlive(true, 600);            } catch (exception) {                console.log('exception', exception);            }        }        conn.on('data', data => {            let message = JSON.parse(data);            console.log('----------- Received Message start -------------');            console.log(                'from: ' + peerId.toString('hex'),                'to: ' + peerId.toString(message.to),                'my: ' + myPeerId.toString('hex'),                'type: ' + JSON.stringify(message.type)            );            console.log('----------- Received Message end -------------');        });        conn.on('close', () => {            console.log(`Connection ${seq} closed, peerId: ${peerId}`);            if (peers[peerId].seq === seq) {                delete peers[peerId]            }        });        if (!peers[peerId]) {            peers[peerId] = {}        }        peers[peerId].conn = conn;        peers[peerId].seq = seq;        connSeq++    })})();setTimeout(function(){    writeMessageToPeers('hello', null);}, 10000);writeMessageToPeers = (type, data) => {    for (let id in peers) {        console.log('-------- writeMessageToPeers start -------- ');        console.log('type: ' + type + ', to: ' + id);        console.log('-------- writeMessageToPeers end ----------- ');        sendMessage(id, type, data);    }};writeMessageToPeerToId = (toId, type, data) => {    for (let id in peers) {        if (id === toId) {            console.log('-------- writeMessageToPeerToId start -------- ');            console.log('type: ' + type + ', to: ' + toId);            console.log('-------- writeMessageToPeerToId end ----------- ');            sendMessage(id, type, data);        }    }};sendMessage = (id, type, data) => {    peers[id].conn.write(JSON.stringify(        {            to: id,            from: myPeerId,            type: type,            data: data        }));};Listing 3-1

展示了 Node.js P2P 网络初始代码以发送和接收消息

为了使这个例子运行，你需要运行这个代码的两个实例。你可以从两台不同的机器上运行，就像现实生活中那样，或者你可以在同一台机器上通过终端运行两个实例。

你的代码需要找到并连接对等体，部署用于发现其他对等体的服务器，并获取一个可用的 TCP 端口。这是通过使用这三个库来完成的：

+   **discovery-swarm**：用于创建一个网络蜂群，该蜂群使用发现通道来找到并连接对等体

+   **dat-swarm-defaults**：部署用于发现其他对等体的服务器

+   **get-port**：获取可用的 TCP 端口

要安装这些库，运行这个命令：> npm install crypto discovery-swarm dat-swarm-defaults get-port --save 现在这些库已经安装好了，打开两个终端实例，导航到库的位置。运行以下命令：> node p2p.js 要从 GitHub 上的克隆库运行代码，导航到代码，按照这些终端命令来安装库，并运行一个 node.js 实例，附上我们的 p2p.js 代码：> cd [位置]/chapter2/step2> npm install> node p2p.js 图 3-2 显示了运行 Node.js 代码的输出。![../images/475651_1_En_3_Chapter/475651_1_En_3_Fig2_HTML.jpg](img/475651_1_En_3_Fig2_HTML.jpg)

图 3-2

在终端中运行两个对等体

正如你在图 3-2 中所看到的，网络为你的机器生成了一个随机的对等体 ID，并利用你安装的发现库随机选择了一个端口。然后代码能够发现网络上的其他对等体，并与其他对等体发送和接收消息。你现在与其他用户连接在 P2P 网络上。

让我们通过代码来更好地理解它是如何工作的。代码的第一行是导入你将在代码中使用的开源库的声明。const crypto = require('crypto'), Swarm = require('discovery-swarm'), defaults = require('dat-swarm-defaults'), getPort = require('get-port');

注意你使用 const 来设置你的变量，而不是 let。你希望确保没有重新绑定，并且总是引用同一个对象，所以根据最佳实践建议选择 const。

接下来，你需要设置变量以保存包含对等节点和连接序列的对象，并选择一个所有节点都将连接到的通道名称。你还利用加密库为你的对等节点生成一个随机生成的对等 ID。const peers = {};let connSeq = 0;let channel = 'myBlockchain';const myPeerId = crypto.randomBytes(32);console.log('myPeerId: ' + myPeerId.toString('hex'));接下来，你需要生成一个包含你的对等 ID 的配置对象。然后你使用这个配置对象来初始化蜂群库。蜂群库可以在这里找到：[`github.com/mafintosh/discovery-swarm`](https://github.com/mafintosh/discovery-swarm) 。它的作用是创建一个网络蜂群，使用发现通道库在 UCP/TCP 网络上查找并连接对等节点。const config = defaults({    id: myPeerId,});const swarm = Swarm(config);现在一切设置就绪，你将创建一个 Node.js 异步函数，以持续监控蜂群.on 事件消息。(async () => {你监听随机选定的端口，一旦与对等节点建立连接，你使用 setKeepAlive 确保网络连接与其他对等节点保持在一起。    const port = await getPort();    swarm.listen(port);    console.log('Listening port: ' + port);    swarm.join(channel);    swarm.on('connection', (conn, info) => {        const seq = connSeq;        const peerId = info.id.toString('hex');        console.log(`Connected #${seq} to peer: ${peerId}`);        if (info.initiator) {            try {                conn.setKeepAlive(true, 600);            } catch (exception) {                console.log('exception', exception);            }        }一旦你在 P2P 网络上接收到数据消息，你使用 JSON.parse 解析数据，这是一个 Node.js 本地命令，所以你不需要包含任何导入声明。这个命令将你的消息解码回一个对象，而 toString 命令将字节转换为可读的字符串数据类型。        conn.on('data', data => {            let message = JSON.parse(data);            console.log('----------- Received Message start -------------');            console.log(                'from: ' + peerId.toString('hex'),                'to: ' + peerId.toString(message.to),                'my: ' + myPeerId.toString('hex'),                'type: ' + JSON.stringify(message.type)            );            console.log('----------- Received Message end -------------');

+   **发送/接收方**：你发送消息的和对端点 ID

+   **类型**：消息类型

+   **数据**：您希望在 P2P 网络上分享的任何数据

这些参数在你分享你的区块链区块时会很有用。请注意，你传递的信息需要是一个字符串，不能是一个对象，所以你在通过 P2P 网络分享之前，使用 JSON.stringify 本地函数来编码你的消息。

在这个练习中，你下载并安装了 WebStorm IDE，并创建了你的项目，其中包括一个基础的 P2P 网络。你能够保持对 TCP 网络随机端口的连接，并发送和接收消息，包括对这些消息的编码和解码。你现在可以进入下一个练习，并在你的网络上的每个节点之间发送一个实际的区块。

## 创建创世区块和分享区块

在下一个练习中，你将创建可以在你节点之间分享的区块对象。但在你这样做之前，让我们更仔细地看看区块对象。不同的区块链使用不同类型的区块对象；你将使用与比特币相似的区块对象；我在第二章中详细介绍了它。为了更好地理解架构，请查看下一练习中将使用的区块和区块头对象的统一建模语言（UML）图，如图 3-3 所示！../images/475651_1_En_3_Chapter/475651_1_En_3_Fig3_HTML.jpg

图 3-3

区块和区块头 UML 图

作为提醒，从第二章起，区块对象包含以下属性：

+   **索引**：创世区块是我们的第一个区块，我们将区块索引值设定为 0。

+   ***交易***：区块中的原始交易。在本章中，我不想只关注加密货币，所以将其视为您想要存储的任何类型的数据。

区块对象中包含区块头对象，该对象包含以下属性：

+   **版本**：在撰写本文时，共有四个区块版本。版本 1 是创世区块（2009 年），版本 2 是比特币核心 0.7.0 的软分叉（2012 年）。版本 3 区块是比特币核心 0.10.0 的软分叉（2015 年）。版本 4 区块是比特币核心 0.11.2 中的 BIP65。

+   ***前一个区块头哈希**：这是前一个区块头的 SHA-256（安全哈希算法）哈希函数。它确保前一个区块无法更改，因为此区块需要更改。

+   ***Merkle 根哈希**：Merkle 树是一个二叉树，包含树中所有哈希对的哈希值。

+   ***时间**：矿工开始哈希头部时的 Unix 纪元时间。

正如你所回忆的，比特币还包含一个矿工的难度属性，每 2016 个块重新计算一次。在这里，你不会使用 nBits 和 nounce 参数，因为你没有做 PoW。

+   ***nounce***：比特币块中的 nonce 是一个 32 位（4 字节）的字段，其值由矿工调整，以便块的哈希值小于或等于网络当前的目标。

+   ***nBits***：这指的是目标。目标是一个 256 位的数字，与难度成反比。每 2016 个块重新计算一次。

就 P2P 通信而言，P2P 网络中每个对等体之间的块流动包括从网络上的一个对等体请求最新的块，然后接收一个块请求。图 3-4 显示了流程图。![../images/475651_1_En_3_Chapter/475651_1_En_3_Fig4_HTML.jpg](img/475651_1_En_3_Fig4_HTML.jpg)

图 3-4

P2P 通信请求最新块和接收最新块的流程图

现在你已经理解了架构以及 P2P 网络中块的流动，在接下来的练习中，你将发送和请求块。

### 第二步：P2P 网络发送块练习

**设置** **块类和链库**

在这个练习中，你将创建你自己的区块链。区块链由两个文件组成：block.js 和 chain.js。文件 Block.js 将包含块类对象，而 chain.js 将是处理与块交互的方法的粘合剂。就块对象而言，你将创建与比特币核心类似的属性。查看列表 3-2，block.js 文件包括 Block 和 BlockHeader 对象。

列表 3-2。 block.js*exports.BlockHeader = class BlockHeader {    constructor(version, previousBlockHeader, merkleRoot, time) {        this.version = version;        this.previousBlockHeader = previousBlockHeader;        this.merkleRoot = merkleRoot;        this.time = time;    }};exports.Block = class Block {    constructor(blockHeader, index, txns) {        this.blockHeader = blockHeader;        this.index = index;        this.txns = txns;    }}如你所见，chain.js 包含第一个块，称为*创世块*，以及接收整个区块链对象、添加块和检索块的方法。注意你将在 chain.js 库中添加一个名为 moment 的库，以保存时间以 Unix 时间格式。为此，使用 npm 安装 moment。> npm install moment --save

现在你已经创建了 block.js 文件，你可以创建 chain.js 类；参见列表 3-3。

以下是*Listing 3-3. chain.js*的翻译：let Block = require("./block.js").Block, BlockHeader = require("./block.js").BlockHeader, moment = require("moment");let getGenesisBlock = () => {    let blockHeader = new BlockHeader(1, null, "0x1bc3300000000000000000000000000000000000000000000", moment().unix());    return new Block(blockHeader, 0, null);};let getLatestBlock = () => blockchain[blockchain.length-1];let addBlock = (newBlock) => {    let prevBlock = getLatestBlock();    if (prevBlock.index < newBlock.index && newBlock.blockHeader.previousBlockHeader === prevBlock.blockHeader.merkleRoot) {        blockchain.push(newBlock);    }}let getBlock = (index) => {    if (blockchain.length-1 >= index)        return blockchain[index];    else        return null;}const blockchain = [getGenesisBlock()];if (typeof exports != 'undefined' ) {    exports.addBlock = addBlock;    exports.getBlock = getBlock;    exports.blockchain = blockchain;    exports.getLatestBlock = getLatestBlock;}

现在您有一个包含在 chain.js 中的区块对象。您的库可以创建创世区块并将区块添加到区块链对象中。您还将能够发送和请求区块。

在您的 P2P 网络课程中，您可以使用您创建的 chain.js 文件。首先，您需要导入 chain.js 类。const chain = require("./chain");然后，您可以定义一种消息类型来请求和接收最新的区块。当您在 P2P 网络中发送消息时，您需要能够弄清楚消息的目的。通过使用 MessageType 属性，您可以定义一个切换机制，以便不同的消息类型用于不同的功能。let MessageType = {    REQUEST_LATEST_BLOCK: 'requestLatestBlock',    LATEST_BLOCK: 'latestBlock'};一旦收到连接数据事件消息，您就可以创建一个 switch 代码来处理不同类型的请求，如列表 3-4 所示。switch (message.type) {    case MessageType.REQUEST_BLOCK:        console.log('-----------REQUEST_BLOCK-------------');        let requestedIndex = (JSON.parse(JSON.stringify(message.data))).index;        let requestedBlock = chain.getBlock(requestedIndex);        if (requestedBlock)        writeMessageToPeerToId(peerId.toString('hex'), MessageType.RECEIVE_NEXT_BLOCK, requestedBlock);        else        console.log('No block found @ index: ' + requestedIndex);        console.log('-----------REQUEST_BLOCK-------------');        break;    case MessageType.RECEIVE_NEXT_BLOCK:        console.log('-----------RECEIVE_NEXT_BLOCK-------------');        chain.addBlock(JSON.parse(JSON.stringify(message.data)));        console.log(JSON.stringify(chain.blockchain));        let nextBlockIndex = chain.getLatestBlock().index+1;        console.log('-- request next block @ index: ' + nextBlockIndex);        writeMessageToPeers(MessageType.REQUEST_BLOCK, {index: nextBlockIndex});        console.log('-----------RECEIVE_NEXT_BLOCK-------------');        break;}Listing 3-4

消息切换和处理

最后，你将设置一个超时请求，每 5000 毫秒（5 秒）发送一个请求以获取最新块。setTimeout(function(){writeMessageToPeers(MessageType.REQUEST_BLOCK, {index: chain.getLatestBlock().index+1});}, 5000);

你可以从这里下载完整的练习：[`github.com/Apress/the-blockchain-developer/tree/master/chapter3/step2/`](https://github.com/Apress/the-blockchain-developer/tree/master/chapter3/step2/) 。

在此练习中，你能够生成你的创世块并创建一个通过发送消息请求来请求和接收块的机制。请求和接收块的能力使你能够同步进入 P2P 网络的新同伴。你在创世块创建后还需要一个同步，以同步你生成的任何额外块。

## 注册矿工和创建新块

至此，你已经有一个基本的 P2P 网络，你能够连接网络中的同伴，创建创世块，发送和接收块。下一步是能够生成新块。正如你在第二章所见，工作量证明是基于创建一个数学问题，并奖励首先找到问题解决方案的矿工。然而，在这个例子中，你将采取一种权益证明（PoS）的方法，你信任每个矿工来生成你的块。每个同伴将注册为矿工，并将轮流挖出块。你可以在图 3-5 中看到每个矿工生成块的概述。![../images/475651_1_En_3_Chapter/475651_1_En_3_Fig5_HTML.jpg](img/475651_1_En_3_Fig5_HTML.jpg)

图 3-5

你的区块链使用简单的权益证明（PoS）机制来处理挖矿

最后，在你开始下一个练习之前，回顾图 3-4，以更好地理解你的流程。流程显示了你的 P2P 网络如何处理 peer 通信，请求最新块并接收最新块。在下一个练习中，你将注册你的同伴作为矿工并创建新块。

### 步骤 3：注册矿工和创建新块练习

**注册矿工**

在此练习中，你将注册矿工并创建新块。你可以从这里下载完整的练习：[`github.com/Apress/the-blockchain-developer/tree/master/chapter3/step3`](https://github.com/Apress/the-blockchain-developer/tree/master/chapter3/step3) 。

为了自动化每 x 分钟生成一个块的过程，你可以使用一个名为 cron 的 Node.js 库，它类似于 Linux 库，用于自动化任务。

要安装 cron 开源库，请运行以下命令：> npm install cron --save 接下来，在你的 p2p.js 文件中，你将创建两个变量来跟踪注册的矿工以及谁挖出了最后一个块，以便你可以将下一个块分配给下一个矿工。let registeredMiners = [];let lastBlockMinedBy = null;你还将添加两种消息类型。

+   REQUEST_ALL_REGISTER_MINERS

+   REGISTER_MINER

定义 MessageType 对象，包含以下键值对：REQUEST_BLOCK: 'requestBlock'，RECEIVE_NEXT_BLOCK: 'receiveNextBlock'，RECEIVE_NEW_BLOCK: 'receiveNewBlock'，REQUEST_ALL_REGISTER_MINERS: 'requestAllRegisterMiners'，REGISTER_MINER: 'registerMiner'；在注册自己的矿工之前，你需要请求获取网络中所有已注册的矿工信息，然后将在注册的矿工对象中添加自己的矿工信息。你可以通过运行一个定时器，每五秒更新一次你的矿工信息。setTimeout(function(){writeMessageToPeers(MessageType.REQUEST_ALL_REGISTER_MINERS, null);}, 5000);现在，你有一个自动超时的命令，可以指向一个处理器来更新注册矿工的列表，你也可以自动化一个命令将你的矿工信息注册到系统中；setTimeout(function(){registeredMiners.push(myPeerId.toString('hex'));console.log('----------Register my miner --------------');console.log(registeredMiners);writeMessageToPeers(MessageType.REGISTER_MINER, registeredMiners);console.log('---------- Register my miner --------------');}, 7000);在你的 switch 命令中，你希望修改代码，以便能够为矿工注册的消息设置处理器。你希望跟踪已注册的矿工，以及处理新区块挖出后的消息。参见列表 3-5 中的矿工处理器。case MessageType.REQUEST_ALL_REGISTER_MINERS:console.log('-----------REQUEST_ALL_REGISTER_MINERS------------- ' + message.to);writeMessageToPeers(MessageType.REGISTER_MINER, registeredMiners);registeredMiners = JSON.parse(JSON.stringify(message.data));console.log('-----------REQUEST_ALL_REGISTER_MINERS------------- ' + message.to);break;case MessageType.REGISTER_MINER:console.log('-----------REGISTER_MINER------------- ' + message.to);let miners = JSON.stringify(message.data);registeredMiners = JSON.parse(miners);console.log(registeredMiners);console.log('-----------REGISTER_MINER------------- ' + message.to);break;Listing 3-5

矿工处理器

**注销矿工**

当与矿工的连接关闭或丢失时，你还需要注销矿工。console.log(`Connection ${seq} closed, peerId: ${peerId}`);if (peers[peerId].seq === seq) {delete peers[peerId];console.log('--- registeredMiners before: ' + JSON.stringify(registeredMiners));let index = registeredMiners.indexOf(peerId);if (index > -1)registeredMiners.splice(index, 1);console.log('--- registeredMiners end: ' + JSON.stringify(registeredMiners));}

**挖出一个新块**

与比特币不同，比特币每 10 分钟产生一个区块，而你的区块链将会更高效，每 30 秒产生一个区块。为了实现这一点，你已经安装了适用于 Node.js 的开源 cron 库。这个 cron 库的工作方式与 Linux 的 cron 相同。你可以使用 cron 库来设置如何频繁地再次调用相同的代码，这将会用于每 30 秒调用一次你的矿工。

为了实现这一点，首先需要在 p2p.js 文件的顶部在你的代码的导入声明中包含这个库。let CronJob = require('cron').CronJob;

接下来，你可以将你的计划任务（cronjob）设置为每 30 秒运行一次，`job.start()`将会启动任务，正如列表 3-6 所展示的。

*清单 3-6. 挖矿新区块的 crobjob*

图 3-6

注册矿工和生成新区块的代码

在这个练习中，你能够注册你的 peers 作为矿工，生成新区块，并将区块与其他 peers 分享；你使用了一个简单的 PoS 作为共识机制，并通过创建三个 peers 测试了功能。这个共识机制很简单，并没有考虑到可能发生的一切用例或安全性。在下一步，你将在 LevelDB 数据库中保存你的区块。

## 在 LevelDB 中存储区块

如果你运行你的区块链几小时，你会注意到创建的区块数量增长，这可能成为一个问题，因为目前这些区块存储在你的计算机内存缓存中。随着你添加越来越多的区块，内存使用将会增长，最终你的代码将会崩溃。此外，不将你的区块存储在数据库中，你将无法启动和停止你的 P2P 网络，因为区块没有被保存。

为了适应这些用例及其他用例，你将使用一个 LevelDB 数据库。

### 注意

**LevelDB** 数据库以所谓的 *层级提升* 和 *层级降低* 的方式存储键值对。它是区块链网络的理想选择。实际上，比特币使用 LevelDB 不仅存储区块信息，还存储交易信息。参见 [`github.com/bitcoin-core/leveldb`](https://github.com/bitcoin-core/leveldb) 。

### 步骤 4：使用 Leveldb 存储区块练习

**LevelDB**

在这个练习中，你将实现一个数据库来存储你的区块。你可以从这里下载完整的练习：[`github.com/Apress/the-blockchain-developer/tree/master/chapter3/step4/blockchain`](https://github.com/Apress/the-blockchain-developer/tree/master/chapter3/step4/blockchain) 。记得运行安装命令以获取所有的 npm 模块。> npm install

在 LevelDB 中存储区块

正如你所见，你使用 __dirname Node.js 原生类来提供目录路径位置，因为你需要完整的路径来保存你的数据库。

因为你正在同一台机器上运行你 P2P 网络的多个实例，你不能为每个对等实体使用相同的路径，因为数据库需要是分开的。你可以为每个数据库的路径设置一个单独的位置，使用文件夹名作为你的对等 ID 名称；然后每个数据库可以存储在 db 文件夹中。同时注意你保存了第一个区块，getGenesisBlock()。

接下来，您创建一个 storeBlock 方法来存储新块。let storeBlock = (newBlock) => {    db.put(newBlock.index, JSON.stringify(newBlock), function (err) {        if (err) return console.log('Ooops!', err) // 某种 I/O 错误        console.log('--- Inserting block index: ' + newBlock.index);    })}当您使用 generateNextBlock 方法生成新块时，您现在可以将块存储在 LevelDB 数据库中。storeBlock(newBlock);您还将添加一个方法，以便能够从 LevelDB 数据库检索区块。let getDbBlock = (index, res) => {    db.get(index, function (err, value) {        if (err) return res.send(JSON.stringify(err));        return(res.send(value));    });}确保您公开 createDb 和 getDbBlock 方法。if (typeof exports != 'undefined' ) {    exports.createDb = createDb;    exports.getDbBlock = getDbBlock;}最后，在您的 P2P 网络代码中，您需要做的是在启动代码时创建一个数据库。chain.createDb(myPeerId.toString('hex'));要看到代码的实际运行，运行 P2P 网络的一个实例。> node p2p.js 您可以使用带有 -f 标志的 tail 命令监控 db 文件夹中的数据库数据。终端将保持打开状态，并可以显示新块在生成时的输出（参见图 3-7 的输出）。> cd step4/db/[我们的 peer Id]> tail –f 000003.log![../images/475651_1_En_3_Chapter/475651_1_En_3_Fig7_HTML.jpg](img/475651_1_En_3_Fig7_HTML.jpg)

图 3-7

使用 LevelDB 数据库的 tail 命令显示新块正在生成

在这个练习中，您创建了一个 LevelDB 数据库。您正在存储您的区块，这样您就可以检索它们，而不是依赖您的缓存内存。我让事情变得简单；如果这是一个真实运行的区块链，您将实现以下步骤：

1.  1.

    减轻所有可能的安全风险。

1.  2.

    从 LevelDB 数据库存储和检索您的区块。

1.  3.

    创建一个方法来恢复 LevelDB 的条目。

1.  4.

    因为每次初始化都会创建新的数据库，所以清理旧的数据库。

## 创建区块链钱包

在加密货币中，一个钱包是必要的，以便奖励矿工生成区块，同时也能创建交易和发送交易。在本节中，您将创建一个钱包。您需要创建公钥和私钥的组合，不仅是为了验证用户，而且是为了能够存储和检索用户拥有的数据。您将创建带有公钥和私钥的钱包。

在比特币中，钱包的原始软件是你在第二章 2 下载的比特币核心协议；它需要自 2009 年以来所有交易的完整账本，截至撰写本文时，超过 150 GB。因此，大多数正在使用中的钱包是“轻量级”钱包或所谓的*简化支付验证*（SPV）钱包，它们与比特币核心同步。在区块链中，有多种不同的钱包可供选择，从在线钱包到将私钥写在纸上的纸钱包。

在继续之前，让我们快速了解一下如何与比特币钱包进行通信。正如你所回忆的，在第二章 2 中，你能够获取某个比特币钱包的余额。为了更好地了解钱包，你可以使用比特币核心创建一个比特币钱包。

首先，你需要运行比特币守护进程。> bitcoind –printtoconsole 接下来，你可以请求一个地址。> bitcoin-cli help getnewaddress 然后，你可以将你的私钥导出到一个文本文件中。> bitcoin-cli dumpwallet ~/mywallet.txt 你可以获取私钥的位置并查看密钥。> vim /Users/[location]/mywallet.txt 仅供参考，请查看 C++比特币核心钱包代码：> vim /[Bitcoin Core Location]/bitcoin/src/wallet/init.cpp

### 第五步：钱包练习

**创建区块链钱包**

在这个练习中，你将生成用于你的钱包的公私钥。你可以从[`github.com/Apress/the-blockchain-developer/tree/master/chapter3/step5/blockchain`](https://github.com/Apress/the-blockchain-developer/tree/master/chapter3/step5/blockchain)下载完整的练习并运行 npm install 命令。另外，创建一个名为 wallet 的文件夹。> npm install> mkdir wallet

你将使用椭圆曲线密码学库实现来生成公私钥组合。请注意，椭圆曲线库使用 secp256k1 作为 ECDSA 曲线算法。

**注意** *椭圆曲线密码学*（ECC）是比特币使用的公钥加密技术。它基于椭圆曲线理论生成密码学密钥。Secp256k1 是图形椭圆曲线 ECDSA 算法。

为了安装库，运行以下命令：> npm install elliptic --save

接下来，添加一个名为 wallet.js 的文件。查看列表 3-8 中的完整代码。

列表 3-8. wallet.js*let EC = require('elliptic').ec,    fs = require('fs');const ec = new EC('secp256k1'),    privateKeyLocation = __dirname + '/wallet/private_key';exports.initWallet = () => {        let privateKey;        if (fs.existsSync(privateKeyLocation)) {            const buffer = fs.readFileSync(privateKeyLocation, 'utf8');            privateKey = buffer.toString();        } else {            privateKey = generatePrivateKey();            fs.writeFileSync(privateKeyLocation, privateKey);        }        const key = ec.keyFromPrivate(privateKey, 'hex');        const publicKey = key.getPublic().encode('hex');        return({'privateKeyLocation': privateKeyLocation, 'publicKey': publicKey});};const generatePrivateKey = () => {        const keyPair = ec.genKeyPair();        const privateKey = keyPair.getPrivate();        return privateKey.toString(16);};在钱包文件中，您创建并初始化 EC 上下文。const ec = new EC('secp256k1'),然后存储您的钱包私钥的位置，privateKeyLocation。privateKeyLocation = __dirname + '/wallet/private_key';接下来，您可以创建一个方法 exports.initWallet 来生成实际的公钥-私钥，generatePrivateKey。    const keyPair = ec.genKeyPair();    const privateKey = keyPair.getPrivate();注意，只有在没有钱包的情况下，您才会生成一个新的钱包。if (fs.existsSync(privateKeyLocation))

在这个练习中，您利用椭圆曲线加密库创建一个 wallet.js 文件，以生成您的私钥-公钥组合。

为了看到代码运行，暂时在 wallet.js 文件的末尾添加以下代码。脚本将创建公钥和私钥。let wallet = this;let retVal = wallet.initWallet();console.log(JSON.stringify(retVal));接下来，创建一个钱包目录以存储私钥并运行脚本。代码将初始化脚本并创建您的公钥。> mkdir wallet> node wallet.js> cat wallet/private_key 当你运行 node wallet.js 命令时，你可以看到公钥。见图 3-8 的输出。![../images/475651_1_En_3_Chapter/475651_1_En_3_Fig8_HTML.jpg](img/475651_1_En_3_Fig8_HTML.jpg)

图 3-8

生成钱包的私钥-公钥

记得注释掉这些行，因为在下一个练习中，您将创建一个 API，以便通过浏览器创建您的密钥。

## 创建 API

下一步是创建一个应用程序接口（API），以便能够访问您编写的代码。这是区块链的一个重要部分，因为您希望使用 HTTP 服务来访问您的区块、钱包或任何其他 P2P 网络操作。在本节中，您将使用 express 库，因为它易于运行，您可以轻松创建您的 API。

### 步骤 6：API P2P 区块链练习

**创建 API**

在这个练习中，你将创建一个 API 来与你对等式区块链网络进行交互。你可以从这里下载完整的练习：[`github.com/Apress/the-blockchain-developer/tree/master/chapter3/step6/blockchain`](https://github.com/Apress/the-blockchain-developer/tree/master/chapter3/step6/blockchain) 。

你将创建以下服务：

+   ***blocks***: 获取区块链中的所有区块

+   ***getBlock***: 通过索引获取特定区块

+   ***getDBBlock***: 从数据库中获取区块

+   ***getWallet***: 通过生成公私钥创建新钱包

你会安装 express 和 body-parser。这些库将允许你创建一个服务器并在浏览器中显示页面。> npm install express body-parser --save 你还需要导入你创建的 wallet.js 文件。let express = require("express"), bodyParser = require('body-parser'), wallet = require('./wallet');接下来，你创建一个名为 initHttpServer 的方法，该方法将初始化服务器并创建服务。当你在同一台计算机上运行不同实例的 P2P 网络时，你希望使用不同的端口号。通常用于 HTTP 服务的端口是 80 或 8081，但这不是强制的。你要做的是传递你正在使用的随机端口号，并使用切片方法获取端口号的最后两位数字。let initHttpServer = (port) => { let http_port = '80' + port.toString().slice(-2); let app = express(); app.use(bodyParser.json()); 区块服务将获取你的所有区块。app.get('/blocks', (req, res) => res.send(JSON.stringify( chain.blockchain )));获取区块服务将根据索引获取一个区块。app.get('/getBlock', (req, res) => { let blockIndex = req.query.index; res.send(chain.blockchain[blockIndex]); });获取数据库区块服务将根据索引获取 LevelDB 数据库条目。app.get('/getDBBlock', (req, res) => { let blockIndex = req.query.index; chain.getDbBlock(blockIndex, res); });获取钱包服务将使用你在上一步创建的 wallet.js 文件生成你的公私钥对。app.get('/getWallet', (req, res) => { res.send(wallet.initWallet()); });最后，你将使用 Express 监听方法。app.listen(http_port, () => console.log('Listening http on port: ' + http_port)); };你将在启动 P2P 网络并选择随机端口号后调用你创建的 initHttpServer 方法。(async () => { const port = await getPort(); initHttpServer(port);}要调用你的服务，启动 P2P 网络，然后你可以打开浏览器并调用 API。http://localhost:80[port]/getWallethttp://localhost:80[port]/blockshttp://localhost:80[port]/getBlock?index=0http://localhost:80[port]/getDBBlock?index=0 例如，查看图 3-9，你会获取你的区块链中的所有区块。![../images/475651_1_En_3_Chapter/475651_1_En_3_Fig9_HTML.jpg](img/475651_1_En_3_Fig9_HTML.jpg)

图 3-9

获取区块链中的所有区块

在这个练习中，你将创建 API 服务，现在你可以与你的 P2P 网络进行交互。你创建了自己的服务，这样你就可以在同一台机器上创建 P2P 网络的多个实例；然而，实际上，每台机器只会持有一个对等体。在下一个练习中，你将创建一个命令行界面（CLI）来轻松调用这些服务。

## 创建命令行界面

在本章的最后一步，你将创建一个命令行界面（CLI）。CLI 是用来轻松访问你创建的服务所必需的。我不会深入讲解 CLI 脚本的整个内部过程，因为它超出了本章节的范围；然而，你可以下载整个示例并查看。

### 第 7 步：CLI 练习

**区块命令**

在这个练习中，你将创建一个 CLI 来与你的 P2P 区块链网络进行交互和访问。你可以从这里下载完整的练习：[`github.com/Apress/the-blockchain-developer/tree/master/chapter3/step7/blockchain`](https://github.com/Apress/the-blockchain-developer/tree/master/chapter3/step7/blockchain)。

接下来，安装你将用于运行承诺、运行异步函数、为控制台添加颜色以及存储 cookies 的库。`npm babel-polyfill async update-notifier handlebars colors nopt --save`在 block.js 命令中，你将设置两个命令：get 和 all。查看整个代码，如列表 3-9 中所示。

区块命令代码

如你所见，wallet.js 命令将包括 get 和 all 方法，指向一个 curl 命令来运行 HTTP 服务调用。

**钱包命令**

同样，block.js 命令将包括一个 create 方法和一个 curl 命令来运行 HTTP 服务调用。参见列表 3-10。

钱包命令代码

现在你已经设置了你的命令，你可以在 bash_profile 中为你的 CLI 添加别名，以便能够从任何路径位置运行 CLI。

图 3-10

在端口 8057 上运行 P2P 区块链网络。

![图 3-10](img/475651_1_En_3_Fig10_HTML.jpg)

图 3-11

在端口 8057 上检索区块。

在这个练习中，你为获取区块和创建你的钱包创建了两个命令。这是你的 CLI 的起点，你可以根据需要继续添加命令。

## 从这里出发去哪里。

我已经提到，本章中的代码没有考虑很多用例，也没有安全性措施以保持简单。你可以做很多事情来改进代码。

+   **确认（Confirmations）**：每个矿工都会发送一个带有区块的消息。你可以创建一个确认系统来确保数据的完整性。

+   **交易/数据**：你可以实现交易或数据对象来解决双重支付、交易验证和 coinbase 交易问题。

+   **levelDB**：一旦 P2P 初始化，你可以创建一个脚本来检索并写入所有区块到 LevelDB 数据库，验证它们，并在需要时清理数据库。

## 总结

本章介绍了如何创建你自己的基础对等区块链网络；你能够发送和接收消息并在这些消息中包含区块。你能够注册和注销矿工并实现一个简单的权益证明（PoS）共识机制。你创建了新的区块并将它们在 peer 之间发送。你还设置了一个名称-值 LevelDB 数据库来存储区块。你继续并创建了一个包含私钥-公钥对的钱包。最后，你创建了通过 API 服务和命令行界面（CLI）与你的 P2P 网络通信的方法。在下一章中，将通过与比特币核心 API 交互来深入理解比特币钱包和交易。
