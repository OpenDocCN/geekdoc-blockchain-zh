© 2018 Bikramaditya Singhal、Gautam Dhameja、Priyansu Sekhar PandaBikramaditya Singhal、Gautam Dhameja 和 Priyansu Sekhar Panda《区块链入门》`doi.org/10.1007/978-1-4842-3444-0_5`

# 5. 区块链应用程序开发

Bikramaditya Singhal¹、Gautam Dhameja² 和 Priyansu Sekhar Panda¹(1)印度卡纳塔克邦班加罗尔(2)德国柏林在之前的章节中，我们详细介绍了区块链的理论细节以及比特币和以太坊区块链的工作原理。我们还研究了构建区块链技术所需的不同密码学和数学算法、定理和证明。在本章中，我们将从区块链应用程序与传统应用程序的不同之处开始，然后深入探讨如何在区块链上构建应用程序。我们还将看看如何设置所需的基础设施来开始开发去中心化应用程序。

## 去中心化应用程序

区块链技术的普及主要是因为它有潜力解决各种现实问题，因为它提供的透明度和安全性（防篡改）比传统技术更高。有很多区块链用例被几家初创公司和社区成员确定，旨在解决这些问题。为了实现这些用例，我们创建在区块链上运行的应用程序。一般来说，与区块链交互的应用程序被称为“去中心化应用程序”，简称为 DApps 或 dApps。为了更好地理解 DApps，让我们首先重新审视一下什么是区块链。区块链或分布式账本基本上是一种特殊类型的数据库，其中数据不存储在集中式服务器上，而是复制到网络中的所有参与节点。此外，区块链上的数据是经过加密签名的，这证明了写入区块链的数据的实体的身份。为了利用这个数据库来存储和检索数据，我们创建了被称为 DApps 的应用程序，因为这些应用程序不依赖于集中式数据库，而是依赖于基于区块链的去中心化数据存储。对于这些应用程序，没有单一的故障点或控制点。让我们以一个 DApp 的例子来说明。让我们以供应链的场景为例，在这个场景中，有几个供应商和物流合作伙伴参与到制造商品的供应链过程中。为了将区块链技术用于这个供应链用例，我们将做以下操作：

+   我们需要在每个供应商处设置区块链节点，以便它们可以参与共识过程并共享数据。

+   我们需要一个接口，以便所有参与者和用户都能在区块链上存储、检索、验证和评估数据。这个接口将供制造商使用，以输入生产的商品信息；供物流合作伙伴使用，以输入关于货物转移的信息；供仓储供应商使用，以验证生产的商品和转移的商品是否同步等等。这个接口将是我们的供应链 DApp。

另一个 DApp 的例子是基于区块链的投票系统。使用区块链进行投票，我们能够使整个过程更加透明和安全，因为每一票都会被加密签名。我们需要创建一个应用程序，可以获取一份候选人名单，选民可以为这些候选人投票，这个应用程序还将提供一个简单的界面来提交和记录投票。

## 区块链应用开发

在我们深入代码之前，首先需要理解围绕区块链应用开发的一些基本概念。通常，当我们开发传统的软件应用时，我们会用到像对象、类、函数等概念。然而，当涉及到区块链应用时，我们需要了解一些更多的概念，比如交易、账户和地址、代币和钱包、输入和输出以及余额。去中心化应用与区块链之间的握手和请求/响应机制正是由这些概念驱动的。首先，当基于区块链开发应用时，我们需要确定应用数据如何映射到区块链数据模型。例如，在基于以太坊区块链开发 DApp 时，我们需要了解应用状态如何以 Solidity 数据结构表示，以及应用行为如何以以太坊智能合约为表达。我们知道，区块链上的所有数据都由用户的私钥以加密方式签署，因此我们需要确定我们应用中的哪些实体将在区块链上具有身份或地址表示。在传统应用中，通常并非如此，因为数据不总是被签署。对于区块链应用，我们需要定义谁将是签署者以及他们会签署哪些数据。例如，在一个每个选民都通过加密方式签署他们选票的投票 DApp 中，这是容易确定的。然而，想象一个场景，我们需要将一个现有的传统分布式系统应用迁移到一个基于以太坊区块链的 DApp。在这种情况下，我们需要确定哪个表中的哪个实体将具有其身份，以及哪些实体将附属于其他身份。在接下来的几节中，我们将通过一些简单的代码片段来探索比特币和以太坊的应用编程，发送一些交易。这个练习的目的是熟悉区块链 API 和常见的编程实践。为了简单起见，我们将使用这些区块链的公共测试网络，并且我们将用 JavaScript 编写代码。选择 JavaScript 的原因是，在撰写本文时，我们已经为这两个区块链提供了稳定的 JavaScript 库，而且通过编写代码来理解我们所采取的方法的相似之处和不同之处会更容易。每个逻辑步骤之后都有详细的代码片段解释，即使读者不熟悉 JavaScript 编程，也能理解。

### 库和工具

回想第二章的内容，区块链技术中使用了大量的加密算法和数学。在我们从应用程序中将交易发送到区块链之前，我们需要准备好这些交易。交易准备包括定义账户和地址，向交易对象添加所需的参数和值，以及使用私钥进行签名等几个其他步骤。在开发应用程序时，最好使用经过验证和测试的交易准备库，而不是从头编写代码。一些适用于比特币和以太坊的稳定库是开源的，可以用来准备和签名交易，并将它们发送到区块链节点/网络。为了我们的代码练习，我们将使用 bitcoinjs JavaScript 库与比特币区块链互动，以及 web3.js JavaScript 库与以太坊区块链互动。这两个库都可以作为 node.js 包使用，并可以使用 npm 命令下载和集成。重要提示本章的代码练习基于 node.js 应用程序。这是为了确保我们作为本练习编写的代码有一个可以运行和与其他预包装库（node 模块）互动的容器。了解一些关于 node.js 应用程序开发的知识是很好的，读者被鼓励跟随一个关于 node.js 和 npm 的入门教程。图 5-1 展示了 DApp 如何与区块链互动。![A440588_1_En_5_Fig1_HTML.jpg](img/A440588_1_En_5_Fig1_HTML.jpg)图 5-1 区块链应用程序互动

## 与比特币区块链互动

在本节中，我们将从一台机器的一个地址向另一台机器的地址发送一个比特币交易到比特币公共测试网络。这可以看作是针对比特币区块链的“Hello World”应用程序。如前所述，我们将使用 bitcoinjs JavaScript 库来准备和签名交易。为了简化，我们不会运行本地的比特币节点，而是使用第三方提供商 block-explorer 提供的公共比特币测试网络节点。请注意，您可以使用任何提供商为您应用程序提供服务，也可以托管本地节点。您需要做的就是让您的应用程序代码连接到您选择的节点。回想一下，比特币区块链主要用于实现点对点支付。比特币交易主要是将比特币从一台机器的一个地址转移到另一台机器的地址。以下是我们如何以编程方式实现这一点。

### 在 node.js 应用程序中设置并初始化 bitcoinjs 库

在调用针对比特币交易的库特定代码之前，我们将安装并初始化 bitcoinjs 库。在使用 npm init 命令初始化 node.js 应用程序后，让我们创建一个应用程序的入口点，即 index.js，以及自定义 JavaScript 模块来调用 bitcoinjs 库函数 btc.js。在 index.js 中导入 btc.js。现在，我们准备好了下一步。首先，让我们安装 bitcoinjs 的 node 模块：npm install --save bitcoinjs-lib 然后，在我们的比特币模块 btc.js 中，我们使用 require 关键字初始化 bitcoinjs 库：var btc = require('bitcoinjs-lib');现在我们可以使用这个 btc 变量来调用比特币 js 库的库函数。此外，作为初始化过程的一部分，我们初始化了一些其他变量：

+   目标网络：我们使用比特币测试网络。var network = btc.networks.testnet;

+   获取和发送交易的公共节点 API 端点：我们使用 Block Explorer API 进行比特币测试网络。请注意，您可以将此 API 端点替换为您喜欢的端点。var blockExplorerTestnetApiEndpoint = 'https://testnet.blockexplorer.com/api/';

此时，我们已经准备好使用 node.js 应用程序创建一个比特币交易。

### 为发送者和接收者创建密钥对

我们首先需要的是发送者和接收者的密钥对。这些就像用户账户，它们在区块链上标识用户。所以，让我们首先为爱丽丝和鲍勃创建两个密钥对。var getKeys = function () {    var aliceKeys = btc.ECPair.makeRandom({        network: network    });    var bobKeys = btc.ECPair.makeRandom({        network: network    });    var alicePublic = aliceKeys.getAddress();    var alicePrivate = aliceKeys.toWIF();    var bobPublic = bobKeys.getAddress();    var bobPrivate = bobKeys.toWIF();    console.log(alicePublic, alicePrivate, bobPublic, bobPrivate);};在上一个代码片段中，我们使用了比特币 js 库的 ECPair 类，并调用其 makeRandom 方法来为测试网络创建随机的密钥对；请注意传递给网络类型的参数。现在我们已经创建了一对密钥对，让我们用它们将比特币从一个人发送到另一个人。在几乎所有的密码学示例中，爱丽丝和鲍勃都是最受欢迎的角色，正如前面密钥对变量所看到的。然而，每次我们看到一个密码学示例时，通常爱丽丝是加密/签名某物并发送给鲍勃的那个人。因此，我们觉得鲍勃欠爱丽丝很多债务，所以在我们这个案例中，我们将帮助鲍勃偿还其中一部分债务。我们将通过鲍勃到爱丽丝的这个示例比特币交易来实现这一点。

### 在发送者的钱包中获取测试比特币

我们已经确定在这个示例比特币交易中，Bob 将扮演发送者的角色。在他向 Alice 发送任何比特币之前，他需要拥有这些比特币。由于我们知道这个示例交易针对的是比特币测试网络，其中并没有涉及真实货币，但我们仍然需要一些测试比特币在 Bob 的钱包里。获取测试网络比特币的一个简单方法就是在互联网上寻求帮助。互联网上有许多网站提供了一个简单的网络表单，用于接收比特币测试网络地址，然后向这些地址发送测试网络比特币。这些服务被称为比特币测试网络水龙头，如果你在网上搜索这个术语，你会在搜索结果中找到很多这样的服务。我们没有列出或推荐任何特定的测试网络水龙头，因为它们通常不是永久的。一旦水龙头服务提供商耗尽了他们的测试硬币，或者他们不再想提供服务，他们就会关闭它。但然后新的服务会不断出现。关于这些水龙头服务的列表也存在于比特币维基测试网络页面中。获取测试网络比特币的另一种方法是运行一个本地比特币节点，指向测试网络，并挖矿一些。比特币测试网络的区块挖掘难度不如主网络。当构建一个生产比特币应用程序并需要频繁测试时，这种方法可能是下一个级别的解决方案。而不是每次想要测试应用程序时都请求测试硬币，你可以自己挖矿。对于这个简单的示例，我们只需从测试网络水龙头获取一些比特币。在前面的代码片段中，bobPublic 变量中的值是 Bob 的比特币测试网络地址。当我们运行这个片段时，它生成了“msDkUzzd69idLLGCkDFDjVRz44jHcV3pW2”作为 Bob 的地址。这也是 Bob 的 base 58 编码的公钥。我们将在其中一个测试网络水龙头网络表单中提交这个值，作为回报，我们将收到一个交易 ID。如果我们在任何比特币测试网络浏览器中查找这个交易 ID，我们会看到另一个地址向我们在表单中提交的 Bob 的地址发送了一些测试比特币。

### 获取发送者的未花费输出

既然我们知道 Bob 的钱包里有一些测试比特币，我们就可以通过比特币交易将它们花掉并转给 Alice。让我们回顾一下第三章中比特币交易是如何由输入和输出组成的。你可以通过将未花费的输出作为输入添加到你想花费的交易中来花费你的未花费输出。为此，首先你需要查询网络关于发送者未花费输出的信息。下面是我们将通过 block explorer API 为 Bob 的比特币测试网络地址这样做的方式。为了获取未花费输出，我们将向 UTXO 端点发送一个 HTTP 请求，带有 Bob 的地址 "msDkUzzd69idLLGCkDFDjVRz44jHcV3pW2"。var getOutputs = function () {    var url = blockExplorerTestnetApiEndpoint + 'addr/' + msDkUzzd69idLLGCkDFDjVRz44jHcV3pW2 + '/utxo';    return new Promise(function (resolve, reject) {        request.get(url, function (err, res, body) {            if (err) {                reject(err);            }            resolve(body);        });    });};在前面的代码片段中，我们使用了 node.js request 模块来发送使用 node.js 应用程序的 HTTP 请求。请随意使用你喜欢的 HTTP 库/模块。这个代码片段是一个 JavaScript 函数，它返回一个解析为 API 方法响应体的承诺。响应看起来是这样的：[    {        address: 'msDkUzzd69idLLGCkDFDjVRz44jHcV3pW2',        txid: 'db2e5966c5139c6e937203d567403867643482bbd9a6624752bbc583ca259958',        vout: 0,        scriptPubKey: '76a914806094191cbd4fcd8b4169a70588adc51dc02d6888ac',        amount: 0.99992,        satoshis: 99992000,        height: 1258815,        confirmations: 1011    },    {        address: 'msDkUzzd69idLLGCkDFDjVRz44jHcV3pW2',        txid: '5b88d5fc4675bb86b0a3a7fc5a36df9c425c3880a7453e3afeb4934e6d1d928e',        vout: 1,        scriptPubKey: '76a914806094191cbd4fcd8b4169a70588adc51dc02d6888ac',        amount: 0.99998,        satoshis: 99998000,        height: 1258814,        confirmations: 1012    }]调用返回的响应体是一个 JSON 数组，里面有两个对象。每个这些对象代表 Bob 的一个未花费输出。每个输出都有一个 txid，即这个输出列出的交易 ID，与输出关联的金额，以及 vout，即在这个交易中的输出的序列或索引号。JSON 对象中还有一些其他信息，但在交易准备过程中不会使用。如果我们取数组中的第一个对象，它基本上说明比特币测试网络地址 "msDkUzzd69idLLGCkDFDjVRz44jHcV3pW2" 来自交易 "db2e5966c5139c6e937203d567403867643482bbd9a6624752bbc583ca259958" 的索引 "0" 有 `99992000` 个未花费的 Satoshis。同样，第二个对象表示来自交易 "5b88d5fc4675bb86b0a3a7fc5a36df9c425c3880a74

### 准备比特币交易

下一步是准备一笔比特币交易，以便鲍勃可以将测试币发送给爱丽丝。准备交易基本上就是定义它的输入、输出和金额。正如我们在上一步所知道的那样，鲍勃在他的比特币测试网络地址下有两个未花费的输出，让我们花费输出数组的第一个元素。把这个作为输入添加到我们的交易中。var utxo = JSON.parse(body.toString());var transaction = new btc.TransactionBuilder(network);transaction.addInput(utxo[0].txid, utxo[0].vout);在前面的代码片段中，首先我们解析了从前一个 API 调用中收到的响应，以获取鲍勃的未花费输出。然后我们使用 bitcoinjs 库为比特币测试网络创建了一个交易构建器对象。在最后一行，我们定义了一个交易输入。注意这个输入指的是 utxo 数组中 0 索引的元素，这是我们在上一步的 API 调用中收到的。我们将交易 ID（txid）和未花费的 vout 从交易中作为输入参数传递给 addInput 方法。基本上，我们在定义我们要花费什么以及我们从哪里得到它。接下来，我们添加交易输出。这是我们说明我们想要如何花费添加到输入中的内容的地方。在下面的一行中，我们通过在交易构建器对象上调用 addOutput 方法并传入目标地址和金额，添加了一个交易输出。鲍勃想要将 99990000 萨索斯发送给爱丽丝。注意我们使用了爱丽丝的比特币测试网络地址作为函数的第一个参数。transaction.addOutput(alicePublic, 99990000);虽然在这个例子交易中我们只使用了一个输入和一个输出，但一个交易可以有多个输入和输出。需要记住的重要一点是，输入中的总金额不应少于输出中的总金额。大多数时候，输入的金额略多于输出的金额，差异是提供给矿工的费用，以便他们在挖下一个区块时包含这个交易。在这个交易中，我们交易费用为 2000 萨索斯，这是输入金额（99992000）和输出金额（99990000）之间的差异。注意我们不必为交易费用创建任何输出；输入和输出总金额之间的差异自动作为交易费用。另外，请注意我们不能花费部分未花费的输出。如果一个未花费的输出与 x 金额的比特币相关联，那么在将这个未花费的输出作为交易输入时，我们必须花费所有的 x 比特币。所以，如果鲍勃不想将与他未花费输出关联的 99,990,000 萨索斯全部送给爱丽丝，那么我们需要通过在交易中添加另一个金额等于总未花费金额和鲍勃想给爱丽丝的金额之间的差异的输出，将它们还给鲍勃。

### 签署交易输入

现在，既然我们已经定义了交易中的输入和输出，接下来我们需要使用鲍勃的密钥来签名输入。下面的代码行调用了交易构建对象上的签名函数，使用鲍勃的私钥对交易进行加密签名，但它将整个密钥对对象作为输入参数。`transaction.sign(0, bobKeys);`请注意，`transaction.sign`函数接受输入的索引和完整的密钥对作为输入参数。在这个交易中，因为我们只有一个输入，所以我们传递的索引是 0。在这个阶段，我们的交易已经准备就绪并签名为止。

### 创建交易十六进制字符串

现在我们将从交易对象创建一个十六进制字符串。`var transactionHex = transaction.build().toHex();`此代码行的输出如下面的字符串，它表示我们准备好的交易；这一步是必需的，因为发送交易 API 接受原始交易作为一个字符串。

### 将交易广播到网络

最后，我们使用在上一步生成的十六进制字符串值，并通过 API 将其发送到区块链浏览器公共测试网节点，`txPushUrl = blockExplorerTestnetApiEndpoint + 'tx/send';`。请求.post({    url: txPushUrl,        json: {            rawtx: transactionHex        }    }, 函数 (err, res, body) {        如果 (err) 控制台.log(err);        控制台.log(res);        控制台.log(body);    });如果区块链浏览器公共节点接受了交易，我们将收到作为此 API 调用响应的交易 ID，{        txid: "db2e5966c5139c6e937203d567403867643482bbd9a6624752bbc583ca259958"}既然我们有了交易的交易 ID，我们可以在任何在线测试网浏览器中查找它，以查看它何时被挖掘以及它有多少确认。综上所述，这是使用 JavaScript 发送比特币测试网交易的完整代码。输入参数是我们在第 1 步创建的比特币测试网密钥对。var createTransaction = 函数 (aliceKeys, bobKeys) {    获取输出(bobKeys.getAddress()).then(函数 (res) {        var utxo = JSON.parse(res.toString());        var transaction = new btc.TransactionBuilder(网络);        交易.添加输入(utxo[0].txid, utxo[0].vout);        交易.添加输出(alicekeys.getAddress(), 99990000);        交易.签名(0, bobKeys);        var transactionHex = 交易.建立().toHex();        var txPushUrl = blockExplorerTestnetApiEndpoint + 'tx/send';        请求.post({            url: txPushUrl,            json: {                rawtx: transactionHex            }        }, 函数 (err, res, body) {            如果 (err) 控制台.log(err);            控制台.log(res);            控制台.log(body);        });    });};在这一节中，我们学习了如何程序化地将交易发送到比特币测试网络。同样，我们可以通过在库函数和 API 端点中使用主网络作为目标来发送交易到比特币主网络。我们还使用了查询 API 来获取比特币地址的未花费输出。这些功能可以用来创建一个简单的比特币钱包应用程序，以查询和管理比特币地址和交易。

## 以太坊的程序化交互—发送交易

以太坊区块链在区块链应用开发方面比比特币区块链提供更多功能。使用智能合约在区块链上执行逻辑是以太坊区块链的关键特性，这使得开发者能够创建去中心化应用。在本节中，我们将学习如何使用 JavaScript 程序化地与以太坊区块链交互。我们将从简单的交易到创建和调用智能合约，了解以太坊应用编程的主要方面。正如在上一节中为与比特币区块链交互所做的那样，我们也将使用一个 JavaScript 库和一个测试网络来交互 with Ethereum. 我们将使用 web3 JavaScript 库来 interact with Ethereum. 这个库封装了很多以太坊 JSON RPC API，并提供了使用 JavaScript 创建以太坊 DApps 的易于使用的函数。在撰写本文时，我们使用的是 web3 JavaScript 库的版本，该版本大于并兼容 web3 JavaScript 库的 1.0.0-beta.28 版本。对于测试网络，我们将使用以太坊区块链的 Ropsten 测试网络。为了简化，我们再次使用一个公共托管的测试网络节点来 interact with Ethereum，这样在运行这些代码片段时我们就不必托管一个本地节点。然而，所有片段也应与本地托管节点一起工作。我们使用 Infura 服务提供的以太坊 API。Infura 是一个提供公共托管以太坊节点的服务，以便开发者可以轻松测试他们的以太坊应用。在使用 Infura API 之前，我们需要完成一个简单且免费的注册步骤，因此我们将前往[`infura.io`](https://infura.io/)进行注册。注册后，我们将获得一个 API 密钥。使用这个 API 密钥，我们现在可以调用 Infura API。以下（图 5-3）显示了这段代码如何与以太坊区块链交互。注意：该图仅为草图，并未详细显示 Infura 服务架构。![A440588_1_En_5_Fig3_HTML.jpg](img/A440588_1_En_5_Fig3_HTML.jpg)图 5-3 使用 Infura API 服务与以太坊区块链交互本节的以下小节是按顺序执行的步骤，以使用 JavaScript 将交易发送到以太坊 Ropsten 测试网络。

### 设置库和连接

首先，我们在 node.js 应用程序中安装 web3 库。注意安装命令中提到的库的具体版本。这是因为库的 1.0.0 版本有一些更多的 API 和功能可用，它们减少了对其他外部包的依赖。`npm install web3@1.0.0-beta.28`然后，我们使用 require 关键字在我们的 nodejs 以太坊模块中初始化该库，`var Web3 = require('web3');`现在，我们有了 web3 库的引用，但在使用它之前需要实例化它。以下代码创建了 Web3 对象的实例，并将其设置为 Infura 托管的以太坊 Ropsten 测试网络节点，为这个 Web3 实例提供支持。`var web3 = new Web3(new Web3.providers.HttpProvider('https://ropsten.infura.io/<your Infura API key>'));`

### 设置以太坊账户

现在我们已经设置好了，让我们将交易发送到以太坊区块链。在这个交易中，我们将从一个账户发送一些以太币到另一个账户。回想一下第四章，以太坊不使用 UTXO 模型，而是使用账户和余额模型。基本上，以太坊区块链以账户和余额的形式管理状态和资产，就像银行一样。这里没有输入和输出。您可以简单地将以太币从 one account 发送到 another account，以太坊将确保在所有节点上更新这些账户的状态。要向以太坊发送将以太币从 one account 转移到 others 的交易，我们首先需要几个以太坊账户。让我们从为 Alice 和 Bob 创建两个账户开始。以下代码片段调用 web3 库的账户创建函数并创建两个账户。`var createAccounts = function () {    var aliceKeys = web3.eth.accounts.create();    console.log(aliceKeys);    var bobKeys = web3.eth.accounts.create();

### 在发送方账户中获取测试以太币

现在，要创建一个将以太币从一方账户转移到另一方账户的以太坊交易，我们首先需要在其中一个账户中有一些以太币。回想一下，在比特币编程部分，我们使用了测试网络水龙头来获取我们在生成地址时的一些测试比特币。我们也将对以太坊做同样的事情。记住，我们的目标是针对以太坊的 Ropsten 测试网络，因此我们将在互联网上搜索一个 Ropsten 水龙头。作为一个例子，我们把在之前的代码片段中生成的是 Alice 的地址提交给了一个以太坊 Ropsten 测试网络水龙头，我们在那个地址上收到了三个以太币。在 Alice 的地址上收到以太币后，让我们检查这个地址的余额，以确认我们是否真的有以太币。虽然我们可以使用任何在线的以太坊浏览器来检查这个地址的余额，但让我们通过代码来完成。以下代码片段调用了 getBalance 函数，将 Alice 的地址作为输入参数。

### 准备以太坊交易

既然我们现在已经在 Alice 这里有一些测试以太币，那么让我们创建一个以太坊交易，将其中一些以太币发送给 Bob。回想一下，在以太坊中没有输入和输出以及 UTXO 查询，因为以太坊使用基于账户和余额的系统。所以，在交易中我们只需要做的是指定发送方的地址（即发送者的地址）、接收方地址以及要发送的以太币数量，还有一些其他的事情。另外，回想一下，在比特币交易中我们不需要指定交易费用；然而，在以太坊交易中，我们需要指定两个相关字段。一个是 gas 限制，另一个是 gas 价格。回想一下，从第四章我们知道，gas 是我们需要支付给以太坊网络以使我们的交易得到确认并添加到区块的交易费用的单位。gas 价格是我们希望每单位 gas 支付的以太币（以 gwei 为单位）的数量。我们允许用于交易的最多费用是 gas 和 gas 价格的乘积。所以，对于这个示例交易，我们定义了一个具有以下字段的 JSON 对象。在这里，“from”有 Alice 的地址，“to”有 Bob 的地址，value 是 1 个以太币，单位是 wei。我们选择的 gas 价格是 20 gwei，我们想要为这个交易支付的最大 gas 数量是 42,000。另外，请注意，我们留下了数据字段为空。我们稍后会在智能合约部分回到这个问题。{    from: "0xAff9d328E8181aE831Bc426347949EB7946A88DA",    gasPrice: "20000000000",    gas: "42000",    to: '0x22013fff98c2909bbFCcdABb411D3715fDB341eA',    value: "1000000000000000000",    data: ""}

### 签署交易

现在我们已经创建了一个带有所需字段和值的交易对象，接下来我们需要使用发送以太币的账户的私钥来签名它。在此例中，发送者是爱丽丝，因此我们将使用爱丽丝的私钥来签名交易。这样做是为了通过加密技术证明，确实是她本人正在使用她账户中的以太币。

### 将交易发送至以太坊网络

最后一步就是将这个已签名的原始交易发送到公共托管的以太坊测试网络节点，我们将其设置为 web3 对象的提供者。以下代码调用 sendSignedTransaction 函数将原始交易发送到以太坊测试网络。输入参数是我们在前一步作为签署交易的一部分获取的原始交易字符串的值。web3.eth.sendSignedTransaction(signedTx.rawTransaction).then(console.log);注意 preceding code snippet 中使用了“then”。这很有趣，因为 web3 库在处理以太坊交易时提供了不同级别的最终性，因为一个以太坊交易在提交后要经历几个状态。在这个函数中，调用发送交易到网络，然后，当交易收据创建时，交易完成。几秒钟后，当 JavaScript 承诺解决时，我们得到以下输出。{   blockHash: '0x26f1e1374d11d4524f692cdf1ce3aa6e085dcc181084642293429eda3954d30e',   blockNumber: 2514764,   contractAddress: null,   cumulativeGasUsed: 125030,   from: '0xaff9d328e8181ae831bc426347949eb7946a88da',   gasUsed: 21000,   logs: [],   logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',   status: '0x1',   to: '0x22013fff98c2909bbfccdabb411d3715fdb341ea',   transactionHash: '0xd3f45394ac038c44c4fe6e0cdb7021fdbd672eb1abaa93eb6a1828df5edb6253',   transactionIndex: 3}如我们所见，输出有很多信息。最重要的部分是 transactionHash，这是网络上交易的 ID。它还给出了 blockHash，这是包含此交易的区块的 ID。此外，我们还获得了关于此交易

## 程序化与以太坊交互—创建智能合约

在本节中，我们将继续我们的以太坊编程练习，并使用相同的 web3 JavaScript 库和 Infura 服务 API 在以太坊区块链上创建一个简单的智能合约。因为，没有计算机编程初学者教程会没有“Hello World”程序，我们将要创建的智能合约将是一个简单的智能合约，当调用时返回字符串“Hello World”。合约创建过程将是一种特殊类型的交易发送到以太坊区块链，这种类型的交易称为“合约创建交易”。这些交易不提及“to”地址，智能合约的所有者是交易中提到的“from”地址。

### 先决条件

在这个创建智能合约的代码练习中，我们将继续假设 web3 JavaScript 库已经在 node.js 应用程序中安装并实例化，并且我们已经为 Infura 服务注册，就像我们在上一节中做的那样。以下是使用 JavaScript 在以太坊上创建智能合约的步骤。

### 编程智能合约

在第四章 4 中提到，以太坊智能合约是用 Solidity 编程语言编写的。尽管 web3 JavaScript 库将帮助我们将合约部署到以太坊区块链上，但我们仍然需要在 Solidity 中编写并编译我们的智能合约，然后使用 web3 将其发送到以太坊网络。所以，我们首先使用 Solidity 创建一个示例合约。有许多工具可用于在 Solidity 中编码。大多数主流 IDE 和代码编辑器都有 Solidity 插件，用于编辑和编译智能合约。还有一个基于网页的 Solidity 编辑器，名为 Remix。它可以在[`remix.ethereum.org/`](https://remix.ethereum.org/)免费使用。Remix 提供了一个非常简单的界面，用于在浏览器中编写和编译智能合约。在这个练习中，我们将使用 Remix 来编写和测试我们的智能合约，然后我们将会使用 web3 JavaScript 库和 Infura API 服务，将同样的合约发送到以太坊网络。

### 编译合约并获取详情

首先，让我们从 Remix 获取我们的智能合约的一些细节，这些细节将需要使用 web3 库将合约部署到以太坊网络上。点击右侧菜单中的“Compile”选项卡，然后点击“Details”按钮。这将弹出一个新的子窗口，显示智能合约的详细信息。对我们而言重要的是详情弹出窗口中的 ABI 和 BYTECODE 部分。让我们使用 ABI 部分的“复制到剪贴板”按钮复制细节。以下是我们智能合约的 ABI 数据的值。[    {        "constant": true,        "inputs": [],        "name": "Hello",        "outputs": [            {                "name": "",                "type": "string"            }        ],        "payable": false,        "stateMutability": "view",        "type": "function"    },    {        "inputs": [],        "payable": false,        "stateMutability": "nonpayable",        "type": "constructor"    }] 这是一个 JSON 数组，如果我们仔细观察，我们会发现它对应我们合约中的每个函数，包括它的构造函数。这些 JSON 对象包含了关于函数及其输入和输出的详细信息。该数组描述了智能合约的接口。当我们在合约部署到网络后调用该智能合约时，我们将需要这些信息来了解合约公开了哪些函数以及我们需要将什么作为输入传递给我们希望调用的函数。现在让我们获取详情弹出窗口中 BYTECODE 部分的数据。以下是我们合约的数据。{    "linkReferences": {},    "object": "6060604052341561000f57600080fd5b6040805190810160405280600c81526020017f48656c6c6f20576f726c642100000000000000000000000000000000000000008152506000908051906020019061005a929190610060565b50610105565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106100a157805160ff19168380011785556100cf565b828001600101855582156100cf579182015b828111156100ce5782518255916020019190600101906100b3565b5b5090506100dc91906100e0565b5090565b61010291905b808211156100fe5760008160009055506001016100e6565b5090565b90565b6101bc806101146000396000f300606060405260043610610041576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff168063bcdfe0d514610046575b600080fd5b341561005157600080fd5b6100596100d4565b6040518080602001828103825283818151815260200191508051906020019080838360005b8381101561009957808201518184015260208101905061007e565b50505050905090810190601f1680156100c65780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b6100dc61017c565b60008054600181600116156101000203166002900480601f0160208091040260200160405190810160405280929190818152602001828054600181600116156101000203166002900480156101725780601f1061014757610100808354040283529160200191610172565b820191906000526020600020905b81548152906001019060200180831161015557829003601f168201915b5050505050905090565b6020604051908101604052806000815250905600a165627a7a72305820877a5da4f7e05c4ad9b45dd10fb6c133a523541ed06db6dd31d59b35d51768a30029","opcodes": "PUSH1 0x60 PUSH1 0x40 MSTORE CALLVALUE ISZERO PUSH2 0xF JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST PUSH1 0x40 DUP1 MLOAD SWAP1 DUP2 ADD PUSH1 0x40 MSTORE DUP1 PUSH1 0xC DUP2 MSTORE PUSH1 0x20 ADD PUSH32 0x48656C6C6F20576F726C64210000000000000000000000000000000000000000 DUP2 MSTORE POP PUSH1 0x0 SWAP1 DUP1 MLOAD SWAP1 PUSH1 0x20 ADD SWAP1 PUSH2 0x5A SWAP3 SWAP2 SWAP1 PUSH2 0x60 JUMP JUMPDEST POP PUSH2 0x105 JUMP JUMPDEST DUP3 DUP1 SLOAD PUSH1 0x1 DUP2 PUSH1 0x1 AND ISZERO PUSH2 0x100 MUL SUB AND PUSH1 0x2 SWAP1 DIV SWAP1 PUSH1 0x0 MSTORE PUSH1 0x20 PUSH1 0x0 KECCAK256 SWAP1 PUSH1 0x1F ADD PUSH1 0x20 SWAP1 DIV DUP2 ADD SWAP3 DUP3 PUSH1 0x1F LT PUSH2 0xA1 JUMPI DUP1 MLOAD PUSH1 0xFF NOT AND DUP4 DUP1 ADD OR DUP6 SSTORE PUSH2 0xCF JUMP JUMPDEST DUP3 DUP1 ADD PUSH1 0x1 ADD DUP6 SSTORE DUP3 ISZERO PUSH2 0xCF JUMPI SWAP2 DUP3 ADD JUMPDEST DUP3 DUP2 GT ISZERO PUSH2 0xCE JUMPI DUP3 MLOAD DUP3 SSTORE SWAP2 PUSH1 0x20 ADD SWAP2 SWAP1 PUSH1 0x1 ADD SWAP1 PUSH2 0xB3 JUMP JUMPDEST JUMPDEST POP SWAP1 POP PUSH2 0xDC SWAP2 SWAP1 PUSH2 0xE0 JUMP JUMPDEST POP SWAP1 JUMP JUMPDEST PUSH2 0x102 SWAP2 SWAP1 JUMPDEST DUP1

### 将合约部署至以太坊网络

现在我们已经有了智能合约及其详细信息，我们需要准备一个交易，该交易可以将此合约部署到以太坊区块链上。这个交易准备将非常类似于我们在上一节中准备的交易，但它将具有创建合约所需的一些额外属性。首先，我们需要创建一个 web3.eth.Contract 类的实例，该实例可以表示我们的合约。以下代码片段创建了一个带有 JSON 数组作为输入参数的实例，这个 JSON 数组就是我们从 Remix 弹出窗口的 ABI 部分复制的，展示了我们智能合约的详细信息。var helloworldContract = new web3.eth.Contract([{                "constant": true,                "inputs": [],                "name": "Hello",                "outputs": [{                    "name": "",                    "type": "string"                }],                "payable": false,                "stateMutability": "view",                "type": "function"            }, {                "inputs": [],                "payable": false,                "stateMutability": "nonpayable",                "type": "constructor"            }]);现在我们需要使用 web3 库的 Contract.deploy 方法将这个合约发送到以太坊网络。以下代码片段展示了如何做到这一点。helloworldContract.deploy({                data: '0x6060604052341561000f57600080fd5b6040805190810160405280600c81526020017f48656c6c6f20576f726c642100000000000000000000000000000000000000008152506000908051906020019061005a929190610060565b50610105565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106100a157805160ff19168380011785556100cf565b828001600101855582156100cf579182015b828111156100ce5782518255916020019190600101906100b3565b5b5090506100dc91906100e0565b5090565b61010291905b808211156100fe5760008160009055506001016100e6565b5090565b90565b6101bc806101146000396000f300606060405260043610610041576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff168063bcdfe0d514610046575b600080fd5b341561005157600080fd5b6100596100d4565b6040518080602001828103825283

## 以编程方式与以太坊交互——执行智能合约函数

现在我们已经将我们的智能合约部署到了以太坊网络，我们可以调用它的成员函数。以下是以编程方式调用以太坊智能合约的步骤。

### 获取智能合约的引用

要执行智能合约的一个函数，我们首先需要创建一个 web3.eth.Contract 类的实例，这个实例需要用到我们部署的合约的 ABI 和地址。下面的代码片段展示了如何做到这一点。

### 执行智能合约函数

回忆一下，在我们的合约中只有一个公共函数。这个方法名为 Hello，当它被执行时返回字符串"Hello World!"。要执行这个方法，我们将使用 web3 库中的 contract.methods 类来调用它。下面的代码片段展示了这一点。helloworldContract.methods.Hello().send({

## 重新审视区块链概念

在前几节中，我们用 JavaScript 程序化地向比特币和以太坊区块链发送交易。现在我们可以重新回顾一些常见概念，通过代码手写交易的过程。

+   交易：通过我们编写并发送交易到以太坊和比特币时得到的输出，我们现在可以说，区块链交易是由账户所有者发起的操作，如果成功完成，将更新区块链的状态。例如，在我们的 Alice 和 Bob 之间的交易中，我们看到一定数量的比特币和以太币的所有权从 Alice 转移到 Bob，反之亦然，这种所有权的变更记录在区块链上，因此使其进入新的状态。在以太坊的情况下，交易进一步涉及智能合约的创建和执行，这些交易也更新了区块链的状态。我们创建了一个交易，该交易进而部署了以太坊区块链上的智能合约。区块链的状态得到更新，因为现在我们在区块链上创建了一个新的合约账户。

+   输入、输出、账户和余额：我们还看到了比特币和以太坊在管理状态方面的不同。虽然比特币使用 UTXO 模型，以太坊使用账户和余额模型。然而，背后的想法是两个区块链都记录资产的所有权，而交易用来改变这些资产的所有权。

+   交易费用：在公共区块链网络上进行的每笔交易，我们必须为我们的交易支付交易费用，以便矿工确认。在比特币中这是自动计算的，而在以太坊中我们应该提到我们愿意支付的最大费用，以每单位气体价格和气体限制来表示。

+   签名：在两种情况下，我们也都看到了，在创建带有所需值的交易对象后，我们使用发送者的公钥对其进行签名。加密签名是一种证明资产所有权的方法。如果签名不正确，那么交易就变得无效。

+   交易广播：在创建并签名交易后，我们将它们发送到区块链节点。虽然我们例子中的交易是发送到公开托管的比特币和以太坊测试网络节点，但如果我们不信任所有节点来处理我们的交易，我们可以自由地将交易发送到多个节点。这被称为交易广播。

总结一下，当我们与区块链交互时，如果我们想要更新区块链的状态，我们需要提交已签名的交易；为了使这些交易得到确认，我们需要向网络支付一定的费用。

## 公共区块链与私有区块链

基于访问控制，区块链可以分为公共和私有。公共区块链也被称为无需许可的区块链，而私有区块链也被称为需要许可的区块链。两者的主要区别是访问控制。公共或无需许可的区块链不限制新节点加入网络，任何人都可以加入网络。私有区块链中的节点数量有限，并非任何人都可以加入网络。公共区块链的例子有比特币和以太坊主网。一个私有区块链的例子可能是一个由几个以太坊节点组成的网络，这些节点彼此相连，但未连接到主网。这些节点统称为私有区块链。私有区块链通常被企业用于在彼此及其合作伙伴以及子组织之间交换数据。当我们为区块链开发应用时，区块链的类型，公共还是私有，是有区别的，因为与区块链的交互规则可能相同也可能不同。这称为区块链治理。公共区块链有一套预定义的规则，而私有区块链可能有不同的规则。例如，供应链的私有区块链可能有不同的治理规则，而协议治理的私有区块链可能有不同的规则。上述私有以太坊账本和以太坊主网中的代币、燃料价格、交易费、端点等可能相同也可能不同。这也会影响我们的应用。在我们的代码示例中，我们主要关注比特币和以太坊的公共测试网络。尽管与这些区块链的私有部署交互的基本概念仍然相同，但在配置代码以指向私有网络方面将存在差异。

## 去中心化应用架构

一般来说，去中心化应用旨在无需任何中心化组件即可直接与区块链节点进行交互。然而，在实际场景中，由于需要与遗留系统集成以及当前区块链网络的功能有限和可扩展性不足，在设计我们的 DApps 时，我们有时必须在完全去中心化和可扩展性之间做出选择。

### 公共节点与自托管节点的对比

区块链是由节点组成的去中心化网络。所有节点都拥有数据的一致副本，并且始终同意数据的状态。当我们为区块链开发应用时，我们可以让我们的应用与目标网络中的任何一个节点进行通信。这主要有两种设置方式：

+   应用和节点都运行在本地：应用和节点都运行在本地计算机上。这意味着我们将需要我们的应用用户运行一个本地区块链节点，并让应用指向与之连接。这种模型将是一个纯粹的去中心化应用运行模型。这个模型的一个例子是基于以太坊的 Mist 浏览器，它使用一个本地的 geth 节点。图 5-6 展示了这个设置。![A440588_1_En_5_Fig6_HTML.jpg](img/A440588_1_En_5_Fig6_HTML.jpg)图 5-6DApp 连接到本地节点

+   公共节点：应用与第三方提供的公共节点通信。这样我们的用户就不必运行本地节点。这种方法有几个优点和缺点。虽然用户不必为运行本地节点支付电源和存储费用，但他们需要信任第三方将他们的交易广播到区块链。以太坊浏览器插件 MetaMask 使用这种模型，并与公共托管的以太坊节点连接。 图 5-7 展示了这个设置。![A440588_1_En_5_Fig7_HTML.jpg](img/A440588_1_En_5_Fig7_HTML.jpg)图 5-7DApp 连接到公共节点

### 去中心化应用与服务器

除了前面提到的场景外，根据特定的用例和需求，还可能有其他的设置。有很多场景需要在应用和区块链之间运行一个服务器。例如：当你需要维护一个区块链状态的缓存以加快查询速度时；当应用需要根据区块链上的状态更新向用户发送通知（电子邮件、推送、短信等）时；以及当涉及多个账本时，你需要运行后端逻辑以在账本之间转换数据。想象一下，一些大型加密货币交易所使用的基础设施，我们从这些服务中得到两因素认证、通知和支付网关等服务，而这些服务在任何一个区块链中都不直接可用。从更广泛的角度来看，区块链只是确保数据层不易受篡改且可审计。

## 总结

在这一章中，我们学习了去中心化应用开发，并通过一些代码练习了解了如何与比特币和以太坊区块链程序化交互。我们还查看了一些 DApp 架构模型，以及它们如何根据用例而有所不同。在下一章中，我们将搭建一个私有的以太坊网络，然后我们将开发一个完整的 DApp，与这个私有网络交互，并使用智能合约处理业务逻辑。

## 参考文献

web3.js 官方文档[`web3js.readthedocs.io/en/1.0/index.html`](http://web3js.readthedocs.io/en/1.0/index.html) 。Solidity 官方文档[`solidity.readthedocs.org/`](https://solidity.readthedocs.org/) 。bitcoinjs 源代码仓库[`github.com/bitcoinjs/bitcoinjs-lib`](https://github.com/bitcoinjs/bitcoinjs-lib) 。Infura 官方文档[`infura.io/docs`](https://infura.io/docs) 。区块浏览器 API 文档[`blockexplorer.com/api-ref`](https://blockexplorer.com/api-ref) 。为您的以太坊应用设计架构[`blog.zeppelin.solutions/designing-the-architecture-for-your-ethereum-application-9cec086f8317`](https://blog.zeppelin.solutions/designing-the-architecture-for-your-ethereum-application-9cec086f8317) 。