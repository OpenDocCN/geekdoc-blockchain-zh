© Santiago Palladino 2019S. Palladino《面向 Web 开发者的以太坊》[`doi.org/10.1007/978-1-4842-5278-9_4`](https://doi.org/10.1007/978-1-4842-5278-9_4)

# 查询网络

Santiago Palladino^(1 )(1)阿根廷布宜诺斯艾利斯自治市

在对编写智能合约进行了不那么简要的插曲之后，我们将审查连接到以太坊网络以检索数据的不同方法。我们将涵盖不同的连接方法，以及监听更改的模式，并在一个用于监视 ERC20 代币转账的示例应用程序中将它们整合起来。

## 连接到网络

从网络中检索数据的第一步是实际连接到以太坊节点。由于 Web 应用程序不能直接连接到网络，它们依赖于节点来回答对区块链状态的任何查询。我们将从审查节点类型、连接方法和提供者对象开始。

### 关于完整节点和轻节点

典型的以太坊节点是 Geth 或 Parity 实例^(1)，它拥有自己的区块链副本（部分或全部），可以回答客户端（如 DApp）的查询，并转发交易（更多内容请参阅下一章）。具有区块链完整副本的节点称为*完整节点*。这些节点可以获取或重新计算区块链历史中的任何数据。大多数客户端默认以此模式运行。

完整节点也可能存储所有历史数据。这些节点被称为*归档节点*，由于需要支持它们的大量磁盘空间，它们相对较少见——在撰写本文时约为 2TB。它们是必需的，以防您想要查询旧区块的特定信息，例如一年前合约的状态或帐户的余额。

作为完整节点的替代方案，一些节点可能以*轻客户端*模式运行。这些节点仅保留区块头，并根据需要从网络请求信息。它们比完整节点轻得多，适合于移动设备，但不适合于 DApp 的后端，因为查询需要更长时间解决。

#### Infura 和公共节点

关于节点的下一个问题是哪些节点适用于我们的应用程序。在理想的去中心化场景中，每个用户都应该运行自己的完整以太坊节点，以便自己验证所有交易，并避免信任第三方。移动设备或物联网设备上的用户可以选择运行轻节点，这些节点会信任其他节点来中继信息，但仍然会进行验证。

在当前格局中，我们的用户中只有很小一部分实际上会运行以太坊节点。他们中的大部分人只是在了解以太坊是什么，并想知道如何购买他们的第一个 ETH 以支付其初始交易的手续费。让他们自己运行节点仍然不可能。

因此，为了让以太坊的采用过程更加容易，有许多*公共节点*可用。当以太坊节点不持有私钥、对公众开放，并用于回答区块链查询和中继预签名交易时，称其为公共节点。

特别地，**Infura**（日语意为“基础设施”）是一项服务，为以太坊主网以及 Kovan、Ropsten 和 Rinkeby 测试网络提供 HTTP 和 WebSocket 终端节点。由于其可靠性以及免费使用的事实，它被许多去中心化应用程序和钱包广泛使用。

### JSON-RPC 接口

所有以太坊节点，无论特定的实现如何，都暴露了一组众所周知的方法，这些方法组成了*JSON-RPC 接口*。顾名思义，这是一个基于 JSON 的 API，用于执行远程过程调用，并构成了客户端与节点交互的低级接口。常见方法包括 call、sendTransaction、getBlockByNumber、accounts 或 getBalance。甚至还有一些查询节点本身状态的方法，比如它是否在同步或连接了多少对等体。

### 注意

鉴于它是一个低级接口，你会发现自己手动构建 JSON-RPC 调用有些奇怪。大多数库（如 web3.js 或 ethers.js）将为你生成调用并提供响应。然而，了解底层发生了什么总是有用的，以防你遇到可怕的抽象泄漏。

值得一提的是，某些节点可能不实现所有方法。例如，Infura HTTP 端点不提供诸如 newFilter（本章后面将更多介绍过滤器）等昂贵的操作。在讨论如何将我们的应用连接到以太坊网络时，这一点将非常重要。

#### 连接协议

有三种不同的协议可以用作交换 JSON-RPC 消息的传输。节点可以配置为处理其中任何一种。

**HTTP** 协议是最简单的协议之一。它提供了一个简单的基于 HTTP 的接口来 POST JSON 消息。某些节点可能设置在 HTTPS 加密连接之后，并且可能需要基本身份验证来访问它们。一个简单的 HTTPS 连接字符串如下所示："https://user:password@example.com:8545/"一个更有趣的选择是 **websocket** 协议。Websocket 连接是客户端和服务器之间的持久双向连接。这使得客户端不仅可以执行所有可用的 JSON-RPC 调用，还可以订阅从节点推送到客户端的更改（稍后会详细介绍）。像 HTTP 连接一样，websocket 也可以在 SSL 上建立，并且可能包括基本身份验证："wss://user:password@example.com:8545/ws"最后，**IPC**（进程间通信）协议基于节点创建的本地 UNIX 域套接字。具有对套接字访问权限的客户端可以通过其文件名连接到它。这些连接旨在由具有对节点相同文件系统访问权限的进程使用，因此不会在 Web 应用程序上使用。"ipc://home/ubuntu/.ethereum/geth.ipc"

#### 备选 API

作为与节点的 JSON-RPC 接口建立连接的替代方案，您可以选择从不同的源查询区块链数据。

**Etherscan**（etherscan.io）是一个集中式服务，不仅提供了一个基于 Web 的区块链浏览器，在这里您可以直观地检查发送到和从帐户发送的所有交易，还提供了一个普通的 HTTP API（见 4-1）实现了 JSON-RPC 接口中的许多方法。# Etherscan APIcurl "https://api.etherscan.io/api?module=proxy&action=eth_getTransactionCount&address=$ADDRESS&tag=latest&apikey=YourApiKeyToken"# 普通的 JSON-RPC 调用{"jsonrpc":"2.0","method":"eth_getTransactionCount","params":["$ADDRESS","latest"],"id":1}列表 4-1

执行 getTransactionCount 调用到 etherscan API 的示例（前文）与标准 JSON-RPC 调用（后文）的区别。两者都返回相同的 JSON 对象作为响应

某些 JavaScript 库，如 ethers.js，甚至包括抽象连接到 Etherscan API 的 *provider* 对象，因此它可以像任何其他标准 JSON-RPC 连接一样无缝使用。现在让我们深入了解提供程序的角色。

### 注意

我们暂时不深入讨论特定领域的 API。项目可能决定提供一个 API 来查询其领域的相关数据。您还可以选择设置一个集中式服务器，从您的协议中聚合区块链数据，并将其中继到客户端应用程序。

### 提供程序对象

正如我们在第二章中简要介绍的，构建我们的第一个示例 DApp 时，与节点的连接由 *provider* JavaScript 对象管理。提供程序负责抽象正在使用的连接协议，并提供一个用于发送 JSON-RPC 消息和订阅通知的最小接口。

### 注意

在撰写本文时，不同库的提供程序具有略有不同的 API。正在努力将最小提供程序标准化为 EIP 1193，但仍然是草案。

例如，web3 JavaScript 库^(2) 提供了以下提供程序用于连接 HTTP、websocket 或 IPC 接口（见列表 4-2）。然后使用提供程序来初始化完整的 web3 对象。const Web3 = require('web3');const httpProvider = newWeb3.providers.HttpProvider("https://example.com");const wsProvider = newWeb3.providers.WebsocketProvider("wss://example.com");const ipcProvider = newWeb3.providers.IpcProvider("/home/ubuntu/.ethereum/geth.ipc");const web3 = new Web3(provider);列表 4-2

创建提供程序和初始化 web3 实例的示例 web3@1.2.0 代码

只有在需要手动设置与节点的连接时，您才需要创建提供者实例。在大多数情况下，您实际上会将这个责任委托给用户的 Web3 可用浏览器。

#### Metamask 和 Web3 可用浏览器

在第二章之后，您现在应该对 Metamask 有所了解，这是一个作为 Web 应用程序与以太坊网络之间桥梁的浏览器扩展。还有其他选择，比如 Cipher 或 Opera 浏览器用于 Android，不过我们将在本书中专注于 Metamask，因为它目前是最广泛使用的工具。

Web3 可用浏览器通过在全局范围内注入 *提供者* 实例来工作。这个提供者的工作方式或者它的后台支持方式对于您的 DApp 来说并不重要。DApp 应该能够查询它需要的任何信息，并让提供者解决它。

请注意，为了访问用户的帐户或请求签署交易（见 4-3），可能需要 *启用* 这个提供者，这将提示用户接受 DApp 请求访问他的帐户信息。// Metamask 将 web3 提供者注入为 window.ethereumconst Web3 = require('web3');const provider = window.ethereum;if (provider) {  try {    // 请求访问用户的帐户    await provider.enable();  } catch (error) {    // 用户拒绝了帐户访问，但我们仍然可以    // 运行查询到网络  }  const web3 = new Web3(provider);}Listing 4-3

使用 Metamask 注入的提供者实例实例化 web3 对象的片段

默认情况下，Metamask 通过 HTTPS 连接到 Infura 公共服务器。这允许任何已下载扩展的用户立即连接到以太坊网络，而无需维护和同步自己的节点。尽管如此，Metamask 还允许高级用户设置自己的连接到其他节点的自定义连接，例如他们自己的（见图 4-1 和 4-2）。![../images/476252_1_En_4_Chapter/476252_1_En_4_Fig1_HTML.jpg](img/476252_1_En_4_Fig1_HTML.jpg)

图 4-1

Metamask 设置选项卡允许用户配置自己与节点的连接

![../images/476252_1_En_4_Chapter/476252_1_En_4_Fig2_HTML.jpg](img/476252_1_En_4_Fig2_HTML.jpg)

图 4-2

Metamask 控制选择连接节点的方式，在扩展对话框顶部点击网络下拉时显示。前四个是由 Infura 托管的公共节点连接。

#### 子提供程序

某些 web3 提供程序也可能由 *子提供程序* 组成。子提供程序是拦截通过提供程序发出的调用的非标准对象。除了其他用途外，子提供程序还通过填补所使用的以太坊节点功能集中的任何空白来提供一个常见的接口。在这个意义上，子提供程序就像隐藏在提供程序中的填充物。

举个例子，连接到不提供 *filters* API（用于轮询特定更改）的节点的提供程序可能包含一个 *filter 子提供程序*，它在客户端模拟该功能。这是 Metamask 注入的 web3 提供程序的情况：由于 Infura 不提供 filters API，Metamask 通过自定义子提供程序在提供程序级别添加了该功能。这样，作为开发者，你不需要担心支持哪些 API，并且无论哪个节点回答你的查询，都会得到一致的接口。

在下一章节中，我们将重新讨论子提供者，其中我们将讨论提供者和签名者，因为 Metamask 将其签名者实现为另一个子提供者。

### 选择正确的连接

到目前为止，我们已经审查了不同类型的节点（完整和轻量级，公共和私有），以及不同的连接协议（ipc、http 和 websockets）。我们还学习了如何设置提供者对象以及如何启用 web3 启用的浏览器注入的提供者。在考虑了所有这些选项后，我们需要考虑的一个问题是从 DApp 中查询信息应选择哪种连接方式。

#### 尊重用户的选择

首先，如果我们的用户正在使用支持 web3 的浏览器，我们的 DApp 应依赖于其注入的提供者。支持 web3 的浏览器意味着用户已经是以太坊生态系统的一部分，并且可能正在运行自己的节点。因此，我们需要为他们提供选择要在浏览我们的 DApp 时使用哪个节点的手段。

虽然我们可以重新实现 Metamask 的网络连接界面，但这样做没有多大意义。希望连接到另一个节点的用户已经在运行 Metamask 或其他支持 web3 的浏览器，并且已经预先配置了自己的节点。因此，注入的 web3 提供者应始终是我们连接到网络的首选。

请记住，需要启用提供者才能访问用户的账户列表。尽管如此，如果应用程序不需要这些信息，这一步可以省略。

#### 使用公共节点

下一个选项很简单：连接到公共节点。你可以为你的 DApp 设置自己的节点，或者使用 Infura 的节点。选择使用自己的节点具有自己的基础设施的所有利与弊：你不依赖于第三方，但需要注意节点的健康情况。请记住，没有什么可以阻止任意数量的用户连接到您的节点，因此您应该为流量激增做好准备。因此，仅依赖外部的基础设施提供者可能更容易些。

作为 Infura 的替代方案，你也可以依赖于像 Etherscan 这样的公共 API。Ethers.js，作为 web3.js 的一种替代方案，默认连接到 Infura，并在连接失败时退而使用 Etherscan。

请注意，在您的 DApp 依赖第三方的所有情况下，它都依赖于外部的集中式服务来从区块链获取数据。由于 DApp 的一个强大之处恰恰在于去中心化，添加一个需要信任的组件可能是朝相反方向迈出的一步。决定在便利性和用户的 DApp 的去中心化之间权衡的问题取决于您。因此，一个很好的经验法则是如果找到了注入式提供者，则使用注入式提供者，否则回退到一个集中式服务。

#### 将其整合起来

在 4-4 中的代码尝试从 web3 浏览器中加载注入的提供程序，无论是现代的还是旧版的。 如果失败，它将回退到使用 Infura 安全 websocket 端点。 提供程序用于创建 web3.js 实例，但相同的代码可以被重新用于其他库。async function getWeb3() {  // 现代 web3 浏览器  if (window.ethereum) {    const web3 = new Web3(window.ethereum);    // 仅当我们需要访问用户账户时    try {      await window.ethereum.enable();    } catch (error) {      console.error("No access to user accounts");    }    return web3;  }  // 旧版 web3 浏览器  else if (window.web3) {    return new Web3(window.web3.currentProvider);  }  // 标准浏览器  else {    return new Web3("wss://mainnet.infura.io/ws/v3/TOKEN");  }}Listing 4-4

基于 metamask.io 提供的代码，用于初始化 DApp 的 web3 连接的代码片段。

## 检索数据

现在我们知道如何连接到网络，我们可以开始实际检索数据。 我们将查看如何访问网络信息、账户余额、执行静态调用和订阅事件。 与之前一样，我们将使用 web3@1.2.0 作为与以太坊网络交互的库，但其他库应该提供类似的功能。

### 网络信息

我们可以通过查询一般的网络信息开始。 首先，总是检查您是否连接到预期的网络是一个好习惯。 如果您的应用程序意在在 Rinkeby 测试网络上使用，您不希望用户意外地使用与主网的连接。 为此，您可以获取您连接的网络的标识符，并将其与预期网络的标识符进行比较。> await web3.eth.net.getId()1

网络通过数字标识符进行识别。 主网为 1，Ropsten 为 3，Rinkeby 为 4，Kovan 为 42。 临时开发网络通常使用较高的 ID 设置。

### 注

像大多数 JavaScript 中对外部数据源的请求一样，对以太坊网络的调用都是异步操作。不同的库可能有不同的处理方式，可以使用回调函数或返回 promises。特别是，web3.js 支持传统的错误优先回调以及 Promi-events。Promi-events 是同时充当事件发射器的 promise 对象，允许你监听异步操作的不同阶段。它们将在下一章变得更加相关。目前，我们将简单地使用 async-await 语法来处理 promises。

我们还可以从网络中获取另一种信息，即当前区块编号。轮询此值可以让我们知道何时向链中添加了新的区块，可能包括已修改我们正在处理的合约状态的交易，从而触发我们应用程序中的重新读取。> await web3.eth.getBlockNumber()7059809^(3)我们还可以从一个区块中获取详细信息，例如其哈希值、总用气量、矿工和其中包含的所有交易列表。请注意，我们可以通过数字、哈希值或字符串“latest”来引用一个区块，以示我们要获取链上最新的区块。> await web3.eth.getBlock('latest'){ author: '0xea674fdde...',  gasLimit: 8000029,  gasUsed: 1808896,  hash: '0xcdb2699b240ece675611aa...',  number: 7059810,  transactions:   [ '0xca7d315abc76988ddcfa49...',     '0x9b72090bbabe017d4bcf5b...',     '0xa50150e448a0cc40a29986...',     ... ],  ... }我们还可以获取不在网络上而是在节点本身的信息。例如，我们可以查询节点正在运行的软件版本，甚至在该版本存在已知问题时通知我们的用户。> await web3.eth.getNodeInfo()'Parity-Ethereum//v2.1.11-stable-e9194b0-20190107/x86_64-linux-gnu/rustc1.31.1'另一个可能有用的检查是节点是否与链的其余部分保持同步。刚刚设置的节点可能尚未同步，因此它们将无法从网络中返回最新的信息。如果一个节点不再同步，你可以放心地依赖它。> await web3.eth.isSyncing()false

从节点中可以查询到更多的信息。务必查看 web3.js 参考文档^(4)以获取额外的方法。

### 账户余额和代码

给定一个地址，你可以查询该账户存储的 ETH，无论它是外部拥有账户还是合约。此外，由于区块链历史是不可更改的，你甚至可以查询账户在以前某个时间点的余额（见清单 4-5）。你可以回溯的区块数量取决于你是否使用归档或常规节点。> const addr = '0xcafE1A77e84698c83CA8931F54A755176eF75f2C';> const block = await web3.eth.getBlockNumber() - 10;> await web3.eth.getBalance(addr, block);'180300794957635301822239'清单 4-5

查询十个区块之前的地址余额

请注意，ETH 余额**总是**以 Wei 表示，这是 ETH 可以细分的最小单位。1 ETH 相当于 1e18 Wei（即，后面跟着 18 个零）。你可以使用 web3 utils 模块（见清单 4-6）在它们之间进行转换。> const balance = await web3.eth.getBalance(addr, block)> web3.utils.fromWei(balance)'180300.794957635301822239'清单 4-6

使用 `web3.utils.fromWei` 将 Wei 转换为 ETH。反向方法是 `toWei`。

你可能已经注意到前面的片段中，ETH 余额返回的不是一个数字，而是一个**字符串**。这是为了在处理非常大的数字时避免丢失精度，因为 JavaScript 数字无法处理非常大的数量级。举例来说，在下面的代码中，将 1822239 wei 转换为整数时会丢失精度。> parseInt(balance).toLocaleString();'180,300,794,957,635,300,000,000'

这个决定是针对 web3.js 库的。其他库依赖于 JavaScript 的大数实现，比如 bignumber.js^(5) 或 bn.js^(6)。一旦语言中对本机大数的支持稳定下来，很可能这些库会切换到它。无论哪种方式，重要的是要记住，以太坊中的大多数数字不能使用常规 JavaScript 数字来处理，否则可能会失去精度。

除了余额之外，您还可以获取地址上的代码，并使用它来检查地址是合约还是外部拥有的帐户。您还可以检查代码本身，以查看它是否与已知合约的二进制代码匹配。> await web3.eth.getCode(addr);'0x6060604052361561011...'

请记住，用于检查帐户是否为合约的方法远非健壮。如果从地址中获取不到代码，则不一定意味着它是外部拥有的：可能稍后会将合约部署到该地址，或者合约可能已在该处部署，但最终已自毁。总而言之，您应避免依赖任意地址是否为外部拥有的帐户来进行特别敏感的操作。

### 调用合约

正如我们在第二章中看到的，您可以通过向其地址发出 JSON-RPC 调用来从合约中查询信息。大多数合约都公开了返回其当前状态或执行纯计算的 getter 函数；这些函数可以通过 Solidity 中的 view 或 pure 修饰符进行标记。与本章中列出的所有函数一样，调用它们不会花费任何 gas，因为任何网络中的节点都可以回答该调用，并且不需要在区块链上引入更改。

这些调用可以使用`web3.js`中的`call`函数在低级别执行，该函数需要手动提供目标地址和要发送到目标合约的原始数据。例如，`0x18160ddd`是访问 ERC20 代币合约的`totalSupply`的函数选择器[⁸]，因此我们可以对主网上的现有合约进行测试，例如主网上的 BAT 代币，它返回 1.5e27 的十六进制表示。> `const addr = '0x0d8775f648430679a709e98d2b0cb6250d2887ef';`> `await web3.eth.call({ to: addr, data: '0x18160ddd' });``0x00000000...0004d8c55aefb8c05b5c000000`但是，我们通常会依赖于`web3`合约抽象来与合约进行交互（见清单 4-7）。如前所述，创建其中一个需要合约的 ABI 和其地址。我们将使用 ERC20 的 ABI 复制前面的示例。[⁹]> `const abi = [  {    "constant": true,    "inputs": [],    "name": "totalSupply",    "outputs": [{"name": "", "type": "uint256"}],    "payable": false,    "stateMutability": "view",    "type": "function"  }, ...];`> `const erc20 = new web3.eth.Contract(abi, addr);`> `await erc20.methods.totalSupply().call()`'1500000000000000000000000000'清单 4-7

通过`web3`合约对象访问相同代币的总供应量。请注意，输出的格式是基于其类型而不是作为原始十六进制值返回的。

### 注意

像`getBalance`一样，对合约的所有调用也可以包括一个可选的区块参数，以便在以前的某个时间点查询合约的状态。请记住，请求链中太久之前的块的更改需要连接到归档节点，而这并不总是可用的。另外，请记住，根据您的用例，仅显示一段时间之前的信息可能是明智的，以防止可能的链重组。这种最近的数据通常始终可用，无论节点是否保留了归档。

Contract 对象还可以用于获取可以插入低级调用或原始交易的函数选择器。在下一行中，encodeABI 方法返回了我们在本节开头使用的数据选择器。> await erc20.methods.totalSupply().encodeABI()'0x18160ddd'合约还公开了对 ABI 上声明的所有事件的便捷接口（见列表 4-8），从而可以轻松查询区块范围内的所有事件。> const block = await web3.eth.getBlockNumber();> const opts = { fromBlock: block - 100, toBlock: block };> await erc20.getPastEvents('Transfer', opts);[{address: '0x0D8775F648430679A709E98d2b0Cb6250d2887EF',  blockNumber: 7060651,  logIndex: 91,  removed: false,  transactionHash: '0x3bd37...',  transactionIndex: 96,  transactionLogIndex: '0x0',  type: 'mined',  returnValues:    Result {      '0': '0xAAAAA6...',      '1': '0x664753...',      '2': '1905510325611397921584',      from: '0xAAAAA6...',      to: '0x664753...',      value: '1905510325611397921584' },  event: 'Transfer'}, ... ]列表 4-8

获取在过去 100 个区块中发生的主网上 BAT 代币的转账事件。在此示例中，以 0xAAAAA6 开头的地址将 1.9e21 代币转账给地址 0x664753

每个日志对象都会提供发生事件的区块和交易信息，以及事件的名称（在本例中为 Transfer），并包括其发出时的参数。

## 检测变化

我们现在将深入探讨事件。即使我们现在知道如何查询过去的事件，但监听新事件是实时检测合约在我们应用程序中的变化的一种有用方法。我们将看到三种不同的监视变化的方法。

### 轮询新区块

轮询是一种简单但有效的方法来对变化做出反应（见 4-9）。鉴于以太坊网络中的任何变化都需要通过链中的新块引入，一个完全有效的方法是只轮询新块，并在挖掘新块时重新读取您感兴趣的合约状态。由于以太坊块每隔几秒钟生成一次，1 秒的间隔可能就足够了。let block = null,    totalSupply = null;const interval = setInterval(async function() {  const newBlock = await web3.eth.getBlockNumber();  if (newBlock !== block) {    // 更新块编号    block = newBlock;    // 从合约中重新读取相关数据    totalSupply = await erc20.methods.totalSupply().call();  }}, 1000);[4-9]清单

轮询新块以更新 ERC20 合约的 totalSupply。虽然我们可以直接轮询总供应量，但如果有更多需要在每个块上更新的数据，则此方法更有效率

每当发现新块时，您可以查询您的应用正在交互的合约以检索其最新状态，并根据需要更新您的应用程序，如果有任何更改。另一种方法是在新块上运行 getPastEvents，并且只有在有任何影响您的合约的事件时才做出反应。

### 安装事件过滤器

*事件过滤器*是以太坊节点提供的一种机制，用于检索与指定条件匹配的新事件。它通过允许你在**节点上**安装事件过滤器，然后轮询与该过滤器匹配的任何新事件来工作。在 JSON-RPC 层面上，该模式主要由以下方法支持：

+   newFilter 在节点上安装新事件过滤器，返回一个过滤器 ID

+   获取过滤器更改，返回自上次调用此方法以来给定过滤器 ID 的所有新日志

+   uninstallFilter 通过其 ID 删除过滤器

事件过滤器仍然依赖于轮询节点以获取新更改，但它们更方便使用，因为现在节点会准确跟踪需要发送到客户端的新事件。这使得客户端无需定期发出 getPastLogs 调用以检查新事件，并允许节点在需要时预先计算要发送的数据。还可以为发送到节点的新区块和待处理事务安装过滤器。

### 警告

一些公共节点，如 Infura 提供的节点，可能不支持安装事件过滤器。为了解决这个问题，Metamask 配备了一个 web3 子提供程序，完全在客户端上模拟过滤器的行为。这使您可以使用事件过滤器编写应用程序，而无需担心连接的节点实际上是否支持它们。但是，请记住，在这种情况下，通过使用过滤器获得的性能增益完全丧失。

此时，值得讨论一下可用于检索和轮询事件的选项。这些选项既可在创建新过滤器时使用，也可在获取过去日志时使用：

+   **区块范围**可用于指定要监视事件的区块。默认情况下，会创建过滤器以监视最新挖掘的区块。

+   一个或多个日志来源的**地址**。从 web3 合约对象检索事件将自动将日志限制为合约实例的地址。

+   用于过滤事件的**主题**。请记住，从第三章中可以得知 EVM 日志最多可以有四个索引主题，这些主题在查询期间用于过滤它们。第一个主题始终是事件选择器，而其余的主题是来自 Solidity 的索引参数。过滤器可以对任何主题施加限制，要求主题可选择匹配一组值。

例如，以下过滤器对象可用于检索发送到三个代币持有者组的 ERC20 代币的所有转账，在最后的 1000 个区块中。> const block = await web3.eth.getBlockNumber();> const filter = { to: [holder1, holder2, holder3] };> const opts = { fromBlock: block - 1000, filter: filter };> await erc20.getPastEvents('Transfer', opts);

web3 库不支持事件过滤器。相反，监听事件是通过第三种也是最后一种监听更改的机制实现的：订阅。

### 创建订阅

监听事件的更高级选项是创建订阅。事件订阅的工作方式类似于事件过滤器，即它们在节点中从一组过滤器（区块范围、地址和主题）创建，以指示哪些事件对客户端感兴趣。但是，订阅不需要客户端轮询更改，而是依靠双向连接直接将新事件推送到客户端。因此，订阅仅在 websocket 或 IPC 连接上可用，而不在 HTTP 连接上可用。

### 注意

与事件过滤器不同，Infura 支持 websocket 连接，通过 URL wss://mainnet.infura.io/ws/v3/PROJECTID。然而，如果用户选择通过常规 HTTP 连接使用自定义节点，Metamask 也配备了一个子提供程序来模拟客户端订阅，依靠轮询实现。同样，这使您能够在应用程序中透明地使用事件订阅，在连接或节点不支持时，子提供程序会填充该功能。

在底层，当你监听事件时，web3 使用订阅（见 4-10）。这意味着只有在 websocket 或 IPC 连接上运行，或者你有一个子提供程序来填充订阅时，你才能依赖事件。web3 事件发射器将在匹配过滤器的新事件可用时报告，发生错误时以及由于重新组织而从区块链中删除事件时报告。

设置一个订阅以监视 ERC20 代币合约上的转账事件。`data` 处理程序在每个新事件上触发，而 `error` 在订阅出错时触发。由于重组而从链上移除的事件会在 `changed` 中触发。

当与服务器的连接关闭时，订阅会自动清除。或者，可以通过取消订阅对象上的 unsubscribe() 方法或使用 web3.eth.clearSubscriptions() 来删除所有活动订阅。

与事件过滤器一样，可以为来自多个地址的事件以及新挂起的交易或新区块设置订阅。使用后者，可以实现类似轮询的模式，其中安装一个订阅以监视新块，然后在每个块上重新读取合约的状态。然而，如果合约为所有状态更改发出事件，则监视它们会更加高效。

## 例子应用

我们现在将整合本章学到的所有内容，并构建一个用于监视 ERC20 代币转账的 Web 应用程序。此应用程序将仅从代币中检索数据，而不提供实际发送交易的界面。

### 设置

我们将再次使用 create-react-app 包来引导我们的应用程序。毫无疑问，使用这个包并不是必须的，但会简化我们的设置，并让我们专注于构建应用本身。npm init react-app erc20-app

#### 依赖项

除了 web3，我们还将 openzeppelin-solidity 包安装为依赖项。OpenZeppelin 是一个开源的安全可重用智能合约库，包含了一些标准的审核实现。我们将使用它来获取我们需要创建 web3 Contract 实例的 ERC20 合约的 ABI。我们还将添加 bignumber.js 来在整个应用程序中操纵一些数值。npm install web3@1.2.0 openzeppelin-solidity@2.1 bignumber.js@8.0

像以前一样，尝试运行 npm start 确保示例 react-app 成功运行。现在我们可以开始编码了。

#### 初始化 Web3

我们将像以前一样创建一个 network.js 文件来管理连接到网络的 web3 对象。我们将依赖于注入的 web3 提供者，如果需要，会回退到 Infura 的 WebSocket 连接。请注意，由于我们不会请求用户账户访问权限，我们可以跳过 ethereum.enable() 调用。

// src/eth/network.jsimport Web3 from 'web3';let web3;export function getWeb3() {  if (!web3) {    web3 = new Web3(window.ethereum              || (window.web3 && window.web3.currentProvider)              || "wss://mainnet.infura.io/ws/v3/PROJECT_ID");  } return web3;}

### 注意

确保在回退提供者的有效 URL 中填入你的 Infura 令牌，以防用户浏览站点时没有 Metamask 或兼容 web3 的浏览器。请注意，这是基于 WebSocket 的，因为我们将在应用程序后期使用事件订阅。

#### ERC20 合约

我们将创建一个小函数，用于为 ERC20 初始化新的 web3 合约对象。请记住，为了做到这一点，我们需要访问 web3 对象（我们已经设置好了），合约 ABI 和地址。// src/contracts/ERC20.jsimport ERC20Artifact from 'openzeppelin-solidity/build/contracts/ERC20Detailed.json';export default function ERC20(web3, address = null) {  const { abi } = ERC20Artifact;  return new web3.eth.Contract(abi, address);}

我们从 OpenZeppelin 检索合约 ABI，而将地址留作参数。现在我们已经设置好了所有基本组件，我们可以开始使用应用程序视图了。

### 构建应用程序

我们将从一个主要的应用程序组件开始，该组件将初始化连接并设置我们将要监视的 ERC20 合约实例。一旦我们准备好了合约实例，我们将开始从中检索一些信息。

#### 根组件

应用程序组件将成为我们组件树的根（见 4-11）列表。该组件将管理与网络和 ERC20 合约实例的连接，这两者都将在 componentDidMount 生命周期方法中设置。

请记住，此方法会在组件挂载后由 React 自动触发，并且是检索异步数据的建议事件。当然，如果您使用特定的状态管理库（如 Redux），您加载异步数据的策略可能会有所不同。// src/App.jsimport React, { Component } from 'react';import ERC20Contract from './contracts/ERC20';import { getWeb3 } from './eth/network';const ERC20_ADDRESS = "0x1985365e9f78359a9B6AD760e32412f4a445E862";class App extends Component {  state = { loading: true };  async componentDidMount() {    const web3 = getWeb3();    **const erc20 = await ERC20Contract(web3, ERC20_ADDRESS);**    this.setState({ erc20, loading: false });  }  render() {    return (      <div className="App">        { this.getAppContent() }      </div>    );  }  getAppContent() {    const { erc20 } = this.state;    if (!erc20) {      return (<div>连接到网络中...</div>);    } else {      return (<div>ERC20 在 {erc20.options.address}</div>);    }  }}Listing 4-11

我们应用程序的根组件的初始版本。请注意`componentDidMount`中突出显示的行，该行正在设置我们之前构建的工厂方法

由于上例中的地址指的是主网上的一个合约，所以只有当我们连接到以太坊主网络时，应用程序才能正常工作。如果我们连接到另一个网络，该地址上的合约可能不存在，导致应用程序失败。

### 注意

如果您对所选的 ERC20 地址感兴趣，它是 Augur REP 代币。 Augur 是一个去中心化的预言机和预测市场，其主要代币用于报告和争议事件的结果。如果您想尝试其他 ERC20 代币，Etherscan 在 etherscan.io/tokens 提供了一个方便的代币列表。

要处理这种情况，我们将添加几行代码来检测当前网络，并验证我们确实在主网络上（见 4-12）。您可以在应用程序上使用 Metamask 更改当前网络来测试此功能。  async componentDidMount() {    const web3 = getWeb3();    **const networkId = await web3.eth.net.getId();**    **const isMainnet = (networkId === 1);**    **this.setState({ isMainnet });**    if (isMainnet) {      const erc20 = await ERC20Contract(web3, ERC20_ADDRESS);      this.setState({ erc20 });    }    this.setState({ loading: false });  }列表 4-12

检查我们当前是否连接到主网络。请注意，只有在我们连接到正确的网络时才会实例化合约。

渲染方法需要相应更改，以处理不仅是加载和已加载状态，还包括我们不在主网的状态。`getAppContent() {`    `const { loading, isMainnet, erc20 } = this.state;`    `if (loading) {`      `return (<div>连接到网络中...</div>);`    `} else if (!isMainnet) {`      `return (<div>请连接到主网</div>);`    `} else {`      `return (<div>ERC20 在 {erc20.options.address}</div>);`    `}`  `}我们还有另一个问题要解决：如果连接失败怎么办？我们连接的节点可能已离线，或者合约地址可能不正确。当我们检索区块链数据时，我们需要添加适当的错误处理（见 4-13）。`async componentDidMount() {`    `const web3 = getWeb3();`    `await this.checkNetwork(web3);`    `await this.retrieveContract(web3);`    `this.setState({ loading: false });`  `}`  `async checkNetwork(web3) {`    `try {`      `const networkId = await web3.eth.net.getId();`      `const isMainnet = (networkId === 1);`      `this.setState({ isMainnet });`    `} catch (error) {`      `console.error(error);`      **`this.setState({ error: '连接网络时出错' })`**    `}`  `}`  `async retrieveContract(web3) {`    `if (!this.state.isMainnet) return;`    `try {`      `const erc20 = await ERC20Contract(web3, ERC20_ADDRESS);`      `this.setState({ erc20 });`    `} catch (error) {`      `console.error(error);`      **`this.setState({ error: '检索合约时出错' })`**    `}`  `}`4-13

更新了`componentDidMount`方法以添加错误处理。请注意，渲染方法也需要相应更新，以便根据组件状态显示错误消息（如果存在）。

现在我们可以专注于代币本身。让我们创建一个名为 ERC20 的新组件，显示它而不是合约地址（见列表 4-14），并开始处理它。 getAppContent() { const { loading, error, isMainnet, erc20 } = this.state; if (error) { return (<div>{error}</div>); } else if (loading) { return (<div>Connecting to network...</div>); } else if (!isMainnet) { return (<div>Please connect to Mainnet</div>); } else { **return (<ERC20 contract={erc20} />);** } }Listing 4-14

更新渲染辅助方法以显示 ERC20 组件，该方法期望 erc20 合约实例作为属性

#### ERC20 组件

此组件应接收合约实例，知道所有连接细节已由父组件解决，并将其显示出来。我们将从检索一些静态信息开始，例如名称、符号和小数位数（见列表 4-15）。根据 ERC20 标准，这些是可选属性，因为它们从不作为合约逻辑的一部分使用；然而，大多数代币确实会实现它们。

我们还将检索代币的总供应量。这是为该合约创建的代币总数。与名称、符号和小数点不同，不能保证此值会保持不变：一些代币具有连续发行模型，导致总供应量在每个区块上增加，而其他代币可能采用通缩模型，在某些事件实际上会销毁代币。

为了这个应用程序，我们将仅使用固定供应量的代币，因此我们不需要刷新总供应量。尽管如此，您可以轻松地添加一个轮询机制，在每次调用时更新总供应量，就像我们在本章前面看到的那样。class ERC20 extends Component {  async componentDidMount() {    const { contract } = this.props;    **const [name, symbol, decimals, totalSupply] =**      **await Promise.all([**        **contract.methods.name().call(),**        **contract.methods.symbol().call(),**        **contract.methods.decimals().call(),**        **contract.methods.totalSupply().call(),**      **]);**    this.setState({ name, symbol, decimals, totalSupply });  }}列表 4-15

用于显示 ERC20 代币信息的 React 组件。再次，我们依赖 componentDidMount 方法来加载异步信息以填充状态。通过使用 Promise.all()，我们同时触发所有四个请求，并仅在获取到所有请求的返回值后设置它们。

现在我们可以通过向用户显示代币名称和符号以及总供应量来呈现此信息（列表 4-16）。我们将依赖代币的小数位数来格式化我们显示的所有值。render() {  if (!this.state.totalSupply) return "Loading...";  const { name, totalSupply, decimals, symbol } = this.state;  const formattedSupply = formatValue(totalSupply, decimals);  return (<div>    <h1>{name} 代币</h1>    <div>{formattedSupply} {symbol} 的总供应量</div>  </div>);}列表 4-16

渲染方法用于显示 ERC20 代币的静态信息。请注意，totalSupply 受代币的小数位数调整影响。

对于辅助的 formatValue 函数（见 4-17），我们将依赖于 bignumber.js，这是一个用于操作和格式化 JavaScript 中大数的库。我们将把总供应量值转换为一个大数实例，按小数点的数量（以 10 为基数）进行右移，然后将结果格式化为字符串。// src/utils/format.jsimport BigNumber from 'bignumber.js';BigNumber.config({ DECIMAL_PLACES: 4 });export function formatValue(value, decimals) {  const bn = new BigNumber(value);  return bn.shiftedBy(-decimals).toString(10);}列表 4-17

根据合约的小数属性格式化代币金额的辅助函数

到目前为止的输出应该看起来像图 4-3，假设你没有改变示例中的代币地址。![../images/476252_1_En_4_Chapter/476252_1_En_4_Fig3_HTML.jpg](img/476252_1_En_4_Fig3_HTML.jpg)

图 4-3

我们的示例应用程序显示 Augur REP 代币的静态信息：名称（声誉）、符号（REP）和总供应量（1.1e25），并根据代币小数（18）进行格式化

### 显示转账事件

我们现在将添加我们应用程序的最后一个组件，它将显示代币的最新转账，并实时监听任何新的转账。

#### 加载过往转账

让我们从给已有的 ERC20 组件添加一个 Transfers 组件开始（见 4-18）,它将首先加载过去的转账。该组件将从其父组件接收合约、小数点和符号作为 props：第一个用于监视事件，另外两个用于格式化数值。render() {  if (!this.state.totalSupply) return "Loading...";  const { name, totalSupply, decimals, symbol } = this.state;  const { contract } = this.props;  const formattedSupply = formatValue(totalSupply, decimals);  return (    <div className="ERC20">      <h1>{name} Token</h1>      <div>Total supply of {formattedSupply} {symbol}</div>      <div>        **<h2>转账</h2>**        **<Transfers contract={contract}**           **decimals={decimals} symbol={symbol} />**      </div>    </div>  );}Listing 4-18

更新了 ERC20 组件的 render 方法以包含新的 Transfers 组件

我们将加载过去 1000 个区块的所有转账事件来初始化该组件。尝试加载所有历史转账可能会失败，因为 REP 在撰写本文时已有超过 75,000 次转账，这是一个太大的数量，在单个请求中查询节点可能会失败。还有其他代币，比如 OMG，在撰写本文时已有超过 200 万次转账。// src/components/Transfers.jsimport React, { Component } from 'react';import { getWeb3 } from '../eth/network';export default class Transfers extends Component {  async componentDidMount() {    const { contract } = this.props;    const blockNumber = await getWeb3().eth.getBlockNumber();    const EVENT = 'Transfer';    **const pastEvents = await contract.getPastEvents(EVENT, {**      **fromBlock: blockNumber - 1000,**      **toBlock: blockNumber**    **});**    this.setState({      loading: false,      transfers: pastEvents.reverse()    });  }}

### 注意

出于本应用程序的目的，我们只是从任意数量的块中加载事件，以便在加载时为组件提供初始数据。根据您的用例，您可能希望通过连续调用 getPastEvents 来添加加载更多事件的选项（例如，当用户滚动到列表末尾时）。

该组件的渲染方法很简单：我们将展示一个纯组件以在列表中显示每个转账（见 4-19）。我们将传递符号和小数点以格式化每个事件中转移的代币数量。 render() {    const { loading, transfers } = this.state;    const { decimals, symbol } = this.props;    if (loading) return "Loading...";    return (<div className="Transfers">      { transfers.map(transfer => (        <Transfer          key={getLogId(transfer)}          transfer={transfer}          decimals={decimals}          symbol={symbol} />      )) }    </div>)  }Listing 4-19

使用纯组件显示集合中的每个转账，该组件仅显示接收到的数据。

请记住，React 要求我们为集合中的每个元素分配一个唯一的键。为了生成此键，我们使用一个名为 getLogId 的帮助函数（见 4-20），该函数组合了事件发生的事务哈希和日志索引（即，数组中发出的所有日志的特定事件的索引）。此组合保证是唯一的。 function getLogId(log) {  return `${log.transactionHash}.${log.logIndex}`;}Listing 4-20

为日志生成唯一标识符的简单函数。请注意，web3.js 已经为日志条目分配了一个 ID，计算方式是对相同参数的哈希。然而，该哈希然后被截断为 4 个字节，如果我们处理大量事件，可能会导致碰撞。

对于 Transfer 纯组件（见 4-21） ，我们只需依赖之前使用的 formatValue 辅助函数，并从转移对象中获取 from、to 和 value 参数。作为额外内容，我们将包含一个到 etherscan 上交易的链接，这样我们的用户可以在那里查看交易，以便他们可以对我们在应用程序上显示的数据进行额外的检查。^(10)常量 ETHERSCAN_URL = 'https://etherscan.io/tx/';export default function Transfer (props) {  const { decimals, symbol, transfer } = props;  const { from, to, value } = transfer.returnValues;  const roundedValue = formatValue(value, decimals);  const url = ETHERSCAN_URL + transfer.transactionHash;  return (    <div>      <a href={url}>        {from} 到 {to} 为 {roundedValue} {symbol}      </a>    </div>  );}4-21 列表

显示从 ERC20 代币合约加载的单个 Transfer 事件的转移组件

使用这段代码，每次重新加载页面时，我们都会看到该令牌最近 1000 个区块的转移。现在，我们可以添加支持以在发生时监听新的转移。

#### 监控新的转移

为了监视新的转移，我们将安装一个 *subscription*，监听此合约的 Transfer 事件（见 4-22），正如我们在本章中之前已经看到的那样。我们将监听从我们用于获取过去事件的区块之后的所有转移，并在组件取消挂载时取消订阅（见 4-23）。  subscribe(contract, fromBlock) {    const eventSub = contract.events.Transfer({ fromBlock })      .on('data', (event) => {        this.setState(state => ({          ...state,          transfers: [event, ...state.transfers]        }));      });    this.setState({ eventSub });  }4-22 列表

用于监听新的转账事件的订阅函数，应该从 componentDidMount 中调用，使用 erc20 和 blockNumber+1 作为参数。注意，我们将订阅对象存储在状态中以便以后取消订阅

componentWillUnmount() {    const { eventSub } = this.state;    if (eventSub) eventSub.unsubscribe();  }示例 4-23

当组件从树上卸载时停止监听事件的代码。即使在这个特定的应用程序中我们永远不会卸载组件，但始终在不再使用时移除订阅是一个好的做法

您的应用程序现在应该在发生新交易时立即显示，无需刷新页面。但是，为了确保我们正确处理所有情况，我们将为从区块链中删除转账事件以进行重新组织和当订阅失败时添加处理程序（示例 4-24）  subscribe(contract, fromBlock) {    const eventSub = contract.events.Transfer({ fromBlock })      .on('data', (event) => {        this.setState(state => ({          ...state,          transfers: [event, ...state.transfers]        }));      })      **.on('changed', (event) => {**        **this.setState(state => ({**          **...state,**          **transfers: state.transfers.filter(t =>**            **t.transactionHash !== event.transactionHash**            **|| t.logIndex !== event.logIndex**        **)}))**      **})**      **.on('error', (error) => {**        **this.setState({ error })**      **});**    this.setState({ eventSub });  }示例 4-24

为订阅的更改事件和错误事件添加处理程序。前者在从区块链中删除事件时触发，因此我们将其从状态中删除，而后者在出现错误时触发，我们将其添加到状态中以显示给用户

#### 等待确认

作为应用程序的最后一步，我们将避免向用户显示未确认的转账。我们不会在收到转账事件后立即显示它，而是在链上添加一定数量的区块后再在列表中呈现它。

为了做到这一点，我们首先需要监视当前的区块编号。我们将专门为此添加一个订阅（见 4-25），虽然我们也可以每秒轮询 getBlockNumber 方法以实现类似的结果。  async componentDidMount() {    const blockNumber = await getWeb3().eth.getBlockNumber();    this.setState({ blockNumber });    const HEADERS = 'newBlockHeaders';    **const blockSub = getWeb3().eth.subscribe(HEADERS)**      **.on('data', ({ number }) => {**        **if (number) this.setState({ blockNumber: number});**      **});**    this.setState({ blockSub });    // 订阅新的转账并加载之前的转账    // ...  }Listing 4-25

更新 componentDidMount 部分以在组件状态中设置初始区块编号，并添加订阅以在接收到新区块时更新它

现在我们可以将我们的组件限制为只渲染发生在一定数量区块之前的转账事件（见 4-26）。通过检查交易发生的区块编号与当前区块编号，我们可以很容易地实现此过滤器。  render() {    const { transfers, blockNumber } = this.state;    **const confirmed = transfers.filter((transfer) => (**      **blockNumber - transfer.blockNumber > 12**    **));**    // 仅渲染已确认的转账    // ...  }Listing 4-26

更新 render 方法以仅显示至少有 12 个确认的转账

### 注意

不同的应用程序对于确认数会有不同的要求，有些甚至需要数百个区块。这将严格依赖于你的用例。

## 概要

在本章中，我们深入探讨了如何从以太坊网络中提取数据并将其馈送到我们的应用程序中。我们首先回顾了与节点的连接方式，列出了 JSON-RPC 接口可用的协议，并研究了由 web3 和其他库用于管理底层连接的 Provider 对象。我们还了解到有不同类型的节点可用，以及 Provider（例如由 web3 启用的浏览器注入的 Provider）如何通过使用子提供者来抽象出其中一些差异。

使用 web3.js 作为示例库，我们研究了向区块链发出的查询类型：一般网络信息，地址特定的数据如余额和代码，以及对现有合约的调用。连接到存档节点时，这些查询可以发出到过去的任何一个区块，而不仅仅是最近的几个。

我们还研究了在我们的应用程序中实时监视合约变化的不同方法。虽然轮询是一种始终可用的经典方法，但由于性能更好或通知时间更快，事件过滤器或订阅可能是更有趣的选择。

为了总结本章，我们构建了一个应用程序，用于从 ERC20 代币合约中检索信息，并使用订阅监视其所有转账事件。在下一章中，我们将学习如何对区块链进行更改，详细介绍向网络发送新交易涉及的所有细节。
