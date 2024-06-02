© Santiago Palladino 2019S. PalladinoWeb 开发者的以太坊[`doi.org/10.1007/978-1-4842-5278-9_2`](https://doi.org/10.1007/978-1-4842-5278-9_2)

# 2. 一个示例 DApp

Santiago Palladino^(1 )(1)阿根廷布宜诺斯艾利斯自治城

在这一章中，我们将从头开始构建一个完整的 DApp。虽然我们不会深入探讨所涉及的步骤，但这一章将帮助您识别构建分布式应用程序所涉及的所有组件。在接下来的章节中，我们将重点关注每个不同部分，但您始终可以参考这些页面，了解每个部分如何在整体中起作用。

## 关于我们的 DApp

我们将创建一个全局**计数器**，它作为一个 DApp 实现。用户应该能够查看计数器的值，并通过向其发送交易来增加它。尽管这个应用没有实际用途，但逐个组件地了解 DApp 的每个部分将会有所帮助。

### 我们的需求

我们的应用将以一个计数器作为其状态，并允许任何以太坊用户通过交易增加它。同时，任何访问 DApp 的用户都应该能够实时看到计数器值的更新。

应用程序不会管理任何 ETH，并且不会有任何形式的访问控制。只要用户能够访问 DApp，他们就应该能够自由地与之交互。

### 智能合约

以太坊智能合约是部署在以太坊区块链上的小程序。每个合约都有自己的代码和内部状态。在这个应用程序中，我们将计数器的值存储在合约的状态中。合约还将为任何客户端提供一个 getter 来轻松查询其值，以及一个通过向合约发送交易来增加它的方法（见列表 2-1）。pragma solidity ⁰.5.0;contract Counter {    uint256 public value;    function increase() public {        value = value + 1;    }}列表 2-1

我们示例 DApp 支持的智能合约的初始实现

智能合约还应为客户端提供一个*事件*，以便实时监听其状态的更新（见 2-2）。以太坊中的每个交易都可以选择性地触发一个或多个事件，并且客户端可以订阅其中特定的一组事件，作为一种通知合约任何更改的手段。pragma solidity ⁰.5.0;contract Counter {    uint256 public value;    event Increased(uint256 newValue);    function increase() public {        value = value + 1;        emit Increased(value);    }}Listing 2-2

更新的实现以在调用 increase 方法时发出一个事件

现在，这个实现展示了智能合约提供接口供客户端与之交互的基本方式：

+   一个 getter 用于查询合约的内部状态，即 value。在声明字段时使用 public 关键字时会自动生成它。查询合约很快，不涉及发送交易，因此不需要燃气，甚至不需要以太坊账户。

+   一个用于修改合约状态的函数，即 increase。这些函数需要发送交易，需要 ETH 执行。因此，它们需要有资金的账户。

+   增加的事件，用于监听合约状态的更新。任何客户端都可以请求订阅合约的一组事件，以获取对其任何更改的通知。

我们将在下一章节详细介绍智能合约。现在，这些概念足以构建我们的 DApp。

### 架构

我们将为这个示例构建一个传统的 DApp。该应用程序将由以太坊网络中的智能合约支持，该合约将充当 Dapp 的用户的分布式数据库。前端将设置为常规的客户端 JavaScript 应用程序。

对于连接 JavaScript 前端和以太坊网络之间的胶水，我们将依赖于支持 web3 的 Web 浏览器。这是一种允许用户连接到互联网和以太坊网络的浏览器，通过用户自己选择的节点。它还管理用户的私钥和交易签名。

最受欢迎的支持 web3 的浏览器是 MetaMask[¹]，它本身不是一个浏览器，而是一个插件，提供所有必需的功能。MetaMask 跟踪用户的私钥，允许连接到一系列预定义节点或自定义节点，并提示用户接受当前页面试图代表其发送的任何交易。

从开发者的角度来看，MetaMask 向 Ethereum 节点注入一个全局连接提供程序，并拦截所有交易，用自己的密钥对其进行签名。

### 环境设置

在我们开始构建 DApp 之前，我们将设置我们的开发环境，以及与我们的 DApp 交互和测试所需的工具。

#### 开发工具链

我们的开发环境的基本设置将是构建简单的仅客户端 JavaScript 应用程序所需的设置。确保在您的开发机器上安装了 nodejs 和 npm[²]，以便开始。

我们将依赖于 create-react-app 包来启动我们的应用程序。这是 Facebook 开发团队提供的一个包，它初始化一个新的预配置的 React web 应用程序。这将允许我们节省大部分设置时间，专注于构建 DApp。npm init react-app counter-app 至于以太坊特定的库，虽然有许多开发框架可用，但我们将在此示例中坚持使用最少量的内容。我们将使用的唯一与以太坊相关的 JavaScript 库是 web3.js。^(3) 这是一个由以太坊基金会支持开发的库，被许多人视为事实上的标准库。npm install web3@1.2.0 至于以太坊构建工具链，我们将再次专注于所需的最小工具集。首先，我们将安装 Solidity 编译器，以便编译智能合约。^(4) 确保您安装的版本是 0.5.0 或更高版本。$ solc --versionsolc，Solidity 编译器命令行界面版本：...然后，为了为我们的应用程序设置自动化测试，我们将安装 ganache。Ganache 是一个模拟以太坊节点并独立模拟整个以太坊区块链的进程。它在开发环境中或用于运行单元测试时特别有用。npm install -g ganache-cli

默认情况下，ganache 会在每次发送的交易后立即挖掘一个新块，消除了等待交易确认的时间。这使得在编码时使用它作为后端变得容易，但请记住，ganache 环境将会与真实环境大不相同，尤其是在用户体验方面。

#### Web3 浏览器

现在我们将使用 MetaMask 设置一个支持 web3 的浏览器。请记住，虽然现在有其他支持 web3 的浏览器，但在撰写本文时，MetaMask 是与 DApps 交互最流行的方式。

首先安装 MetaMask 插件^(5)到您的浏览器上 – 它支持 Chrome、Firefox、Opera 和 Brave。安装完成后，MetaMask 会提示您创建一个密码来加密您的账户，并提供给您秘密备份短语。确保记下这个短语：如果您丢失了 MetaMask 钱包，您可以使用这个短语重新生成它。否则，其中包含的所有资金将无法挽回地丢失。

### 警告

在安装 MetaMask 时要特别小心。大多数与管理用户密钥或交易相关的软件都容易受到网络钓鱼攻击的影响。下载时请确保您正在访问官方 MetaMask 网站。

下一步是实际资助您的账户以便与智能合约进行交互。在本书的示例中，我们将使用 Rinkeby 测试网络（或测试网）。以太坊有几个测试网（Ropsten、Rinkeby、Kovan 和 Goerli），每个测试网都有自己的特点，并由唯一的数字 ID 标识：

+   Ropsten（id 3）是唯一基于工作证明的测试网，这使得它最类似于主网，但也非常不可靠。由于网络上没有太多实际的*工作*，区块时间是不可预测的，网络容易受到攻击。

+   Rinkeby（id 4）是基于权威证明的测试网，这意味着有一组受信任的节点有*权威*来向区块链添加新区块。这使得它比 Ropsten 稳定可靠得多。然而，由于所使用的共识算法的限制，只有 Geth 客户端可以连接到 Rinkeby。

+   Kovan（id 42）与 Rinkeby 类似，它也是基于权威证明的测试网，但其共识算法与 Geth 不同，而是与 Parity 客户端兼容。

+   Goerli（id 6）是最新设置的测试网。它也使用权威证明，但与之相比，它的优势在于与 Geth 和 Parity 客户端都兼容。

有几个在线水龙头^(6)可以获取测试网络 ETH 进行试验。使用其中一个来为你在 MetaMask 中刚刚创建的账户之一请求资金。

### 注意

你觉得 MetaMask 的入门过程如何？如果你觉得复杂或有点冗长，现在想想你的用户。所有第一次使用以太坊的用户都需要经历类似的流程，另外还需要注册交易所购买真实的主网 ETH 与你的应用程序进行交互，这通常需要完整的 KYC 过程。这就是为什么用户入门在以太坊上是如此具有挑战性的原因。有一些技术可以缓解这个问题，比如在绝对需要之前不要求用户拥有以太坊账户，或者基于元交易构建的备用入门流程。关于这一点，后面在第七章会有更多介绍！

## 构建我们的应用程序

我们将从 create-react-app 模板开始构建。确保已经运行了“*设置环境”* 部分中的所有步骤，你应该在 src 文件夹下有一个简单的 JavaScript 应用程序，并围绕着 index.js 构建了一些文件。为了验证一切是否正常运行，请运行 npm run start 并在 localhost:3000 中打开你的浏览器。你应该会看到 create-react-app 包的默认初始屏幕，包括一个旋转的 React 标志。

### 编译智能合约

我们的 DApp 将由一个名为 Counter 的单一智能合约支持。在项目的根目录下创建一个名为 contracts 的文件夹，并添加一个 Counter.sol 文件（见 2-3）。// contracts/Counter.sol

Solidity 中的智能合约实现，我们将在我们的应用程序中使用。

我们将在下一章节更深入地讨论智能合约，但现在你可以开始识别合约的重要部分：

+   合约的状态，值，定义为 256 位无符号整数，在 Solidity 中是默认大小

+   通过在字段声明中使用 public 关键字生成的用于访问值的 getter

+   通过事务增加值的增加函数

+   用于信号化值修改发生时的 Increased 事件

你可以通过运行 solidity 编译器来测试合约是否正常：$ solc contracts/Counter.sol 编译器运行成功，未请求输出。我们需要指定编译的输出格式。我们特别关注合约的公共接口规范，或者说 ABI（应用二进制接口），这是我们的 JavaScript 应用程序将与合约通信的方式。我们还想要二进制代码，这样如果需要的话就可以部署合约到网络上。我们可以请求 Solidity 编译器将这两者输出到一个单独的 JSON 文件中，然后我们可以使用：solc --pretty-json --combined-json=abi,bin --overwrite \-o ./build/contracts contracts/Counter.sol

### 注意

从编译器输出此信息所需的标志可能会根据您使用的版本而变化。上述代码适用于 Solidity 0.5.1。

上述命令将生成一个名为 build/contracts/combined.json 的文件，其中包含所有编译输出。看一下它，我们很快将使用它与我们的合约交互。

### 通过 Web3 连接到网络

如前所述，我们将使用 web3.js 连接到以太坊网络。这需要一个 web3 *提供者*，它是一个小对象，知道连接哪个节点以便调用智能合约并向网络发送事务。换句话说，正如其名称所示，提供者 *提供* 了与以太坊节点的连接，并通过它连接整个网络。

根据你使用的库的不同，提供者有时会与*签名者*混淆。签名者是另一个组件，负责使用用户的密钥对交易进行签名，如果这些密钥不是由本地节点管理的话。这在大多数 Dapp 中都是如此，因为普通用户通常不会运行节点，而是依赖公共节点。因此，MetaMask 注入的 web3 提供者既充当提供者又充当签名者。我们将在本书后面深入讨论这些差异。

通过 Web3.givenProvider 可以方便地访问 MetaMask 注入的 web3 提供程序。您可以检查此属性以确定用户浏览器中是否启用了 MetaMask，并在可用时创建新的 web3 对象。我们可以将此逻辑保存在我们应用程序的 network.js 文件中（见 2-4）。// src/eth/network.jsimport Web3 from 'web3';let web3;export function getWeb3() {  if (!web3) {    web3 = new Web3(Web3.givenProvider);  }  return web3;}列表 2-4

使用 MetaMask 提供程序创建 web3 对象的片段。请注意，如果用户未安装 MetaMask，则此代码将无法工作。

创建的 web3 对象具有大量可用的方法，其中大多数在 web3.eth 命名空间下。例如，我们可以查询用户账户列表（见 2-5）并检索正在使用的默认账户 – 即列表中的第一个账户。// src/eth/network.jsexport async function getAccount() {  const web3 = getWeb3();  const accounts = await web3.eth.getAccounts();  return accounts[0];}列表 2-5

检索用户当前默认账户的函数

然而，这种方法在运行在 *隐私模式* 的浏览器上无法工作。隐私模式限制了对用户账户的访问，直到用户批准应用程序检索在 MetaMask 中持有的账户。要解锁此功能，我们必须使用全局 ethereum 对象并启用它（清单 2-6）。导出异步函数获取帐户() {  const accounts = await window.ethereum.enable();  return accounts[0];}清单 2-6

更新以处理以太坊浏览器隐私模式的函数

对 ethereum.enable 的异步调用将在用户在 MetaMask 上授予其批准后返回。请注意，MetaMask 将记住用户的批准，因此他们只会在第一次提示时回答（图 2-1）。![../images/476252_1_En_2_Chapter/476252_1_En_2_Fig1_HTML.jpg](img/476252_1_En_2_Fig1_HTML.jpg)

图 2-1

用户必须在 MetaMask 中接受 Dapp 的连接请求

现在我们已经设置好了一个 web3 对象，并且可以访问用户的账户，我们将使用它们来构建我们的界面，以便与部署在以太坊网络上的 Counter 智能合约交互。

### 合约接口

为了从应用程序中与我们的合约交互，我们需要三件事：

+   与部署了我们的合约的以太坊网络的连接

+   合约在网络中的地址

+   合约公共函数的规范，也称为 ABI（应用二进制接口）

第一项在前一节中已涵盖，并由我们提供的 web3 对象封装。至于第二项，我们将使用在 Rinkeby 网络上已部署的实例，其地址如下：0x1D2561D18dD2fc204CcC8831026d28375065ed53

请记住，区块链上的所有内容都是公开且不可抹去的，因此一旦部署合约，它就会成为所有用户可以与之交互且无法删除的公开可用的内容。这意味着我们可以自由地使用此实例来测试 DApp。

### 注意

如果您不想使用该特定合约实例或更喜欢在不同的网络上工作，则代码仓库中有一个部署脚本，您可以使用它来设置您自己的实例。

至于 ABI，我们将利用编译器之前生成的输出。将输出的 json 文件复制到应用程序 src 中的新 contracts 文件夹中的 Artifacts.json 文件中。现在我们可以解析它以获取 ABI，并创建一个新的 web3 合约实例（见清单 2-7）。// src/contracts/Counter.js

创建 Counter web3 合约对象的函数。请注意，该函数不会部署新的合约，它只是创建一个 JavaScript 对象，作为在指定地址上先前部署的合约的包装器。

web3 合约抽象是一个充当实际以太坊合约外观的对象。它为其所有公共函数暴露了 JavaScript 方法，这些方法在底层被转换为对网络的调用和交易。我们将在下一节中使用它来实际与合约交互。

现在我们有了一个像工厂一样的函数，可以根据地址创建新的 Counter 合约抽象（见清单 2-8）。// src/contracts/Counter.js

获取部署在 Rinkeby 网络上的 Counter 合约的 web3 合约实例的代码。请注意，为了避免硬编码地址，您也可以将地址存储为环境变量，并从 process.env 中检索^(7)。

现在我们有了与部署的合约交互的手段，我们可以为我们的用户界面构建 React 可视化组件。

## 与我们的智能合约交互

现在，我们将逐步构建我们的计数器可视化组件，以便我们的 DApp 用户与之交互。我们将从检索计数器的当前值开始，然后提供一种发送交易以修改其状态的方式，然后订阅实时更新。

### 连接我们的组件

让我们从创建文件 components/Counter.js 开始（见 2-9）。目前这将是一个空的 React 组件^(8)。// src/components/Counter.jsimport React, { Component } from 'react';class Counter extends Component {  render() {    return (      <div>计数器在此处</div>    );  }}Listing 2-9

用于渲染计数器合约并与之交互的空 React 组件。我们将逐步向其添加功能

此组件将从 App.js 根组件接收 Counter 合约实例。一旦准备就绪，将由 App 负责检索此类实例并注入 Counter 视觉组件。让我们修改由 create-react-app 自动生成的 src/App.js 文件以加载合约实例（见列表 2-10）。

App 根组件的代码。我们使用根 App 状态来存储合约实例，并将其作为属性传递给子组件。

我们依赖于 componentDidMount React 事件来加载 Counter 合约实例^(9) 并将其存储在组件的状态中。只有当此实例可用时，我们才渲染 Counter 视觉组件。

### 注意

到目前为止，您可能已经意识到我们在此 DApp 中缺少错误管理。例如，我们没有处理用户没有安装 MetaMask 的情况，或者合约地址不正确的情况，或者网络连接丢失的情况。这是一个故意的决定，因为目标是专注于快乐的路径，并提供关于什么构成 DApp 的快速概述。在即将到来的章节中，随着我们更深入地研究每个主题，我们还将涵盖可能出现的所有问题。

在此时，您应该能够通过 npm start 运行您的应用程序并检查一切是否正确渲染。确保已安装 MetaMask，解锁并连接到 Rinkeby 网络。

现在我们已经把所有的应用程序都连通了，是时候专注于计数器视觉组件本身了。

### 查询合约的状态

我们将从在我们的组件上显示计数器合约的值开始（见列表 2-11）。由于我们在组件的生命周期内不会更改计数器实例，因此我们可以在 React 组件挂载时简单地检索该值。^(10)// src/components/Counter.jsasync componentDidMount() {  const counter = this.props.contract;  const initialValue = await counter.methods.value().call();  this.setState({ value: initialValue });}列表 2-11

在组件挂载时检索计数器的初始值

注意对计数器合约实例的调用以检索初始值。call 的 Web3js API 可能看起来有些奇怪，但它有其背后的理由：

+   methods 属性授予对合约 ABI 中定义的所有公共方法的访问权限。它们并不在合约实例本身设置，以防止与 Web3 合约对象的其他特定方法发生冲突。

+   value() 调用实际上并不查询网络，而只是构建一个方法调用。如果函数需要任何参数，它们必须在这里提供。

+   调用 call() 最终向区块链发出查询。我们将在下一章中审查查询方法和发出事务之间的区别，但现在我们只需要知道的是，当我们想要 *检索* 合约数据时使用 call()。

一旦我们在组件状态中设置了初始值，我们就可以最终将其呈现给我们的用户（见列表 2-12）。render() {  const { value } = this.state;  if (!value) return "Loading";  return (    <div>      <div>计数器值：{ value.toString() }</div>    </div>  );}列表 2-12

渲染方法以显示计数器的值。请注意，该值仅在对合约的初始查询返回后才可用，因此我们需要处理还没有准备好的情况。

到此为止，您应该能够重新加载浏览器中的应用程序，并在 Rinkeby 网络上查看 Counter 实例的值。

### 提示

您可以通过区块链浏览器（例如 Etherscan）来双重检查显示的值。^(11) Etherscan 是一个区块链浏览器，是一个提供地址和交易可视化界面的网站，可用于主网和大多数测试网络。在合约地址下找到并点击“读取合约”选项卡，您将能够检查计数器的值。

我们的下一步将是允许用户通过发出交易来增加计数器的值。

### 发送交易

让我们首先编写一个函数来发送一个交易，调用 Counter 合约上的增加函数。increaseCounter() {  const counter = this.props.contract;  return counter.methods.increase().send();}

在上一节之后，发送交易的调用应该更加熟悉。请注意，在这种情况下，我们使用的是 send() 而不是 call()。这是因为我们需要实际发送一个交易来影响合约的状态，而不仅仅是从网络中查询数据。

现在我们可以将这个方法与我们界面中的一个按钮连接起来（见列表 2-13），并进行测试。render() {  const { value } = this.state;  if (!value) return "加载中";  return (    <div>      <div>计数器值：{ value.toString() }</div>      <button onClick={() => this.increaseCounter()}>        增加计数器      </button>    </div>  );}列表 2-13

更新渲染方法以显示一个增加计数器的按钮

如果你尝试这样做，你将会看到 Metamask 的对话框来确认一笔交易，大致会像图 2-2 所示。

图 2-2

Metamask 确认对话框用于接受应用程序发出的交易。每当您尝试代表用户发送交易时，用户将看到此对话框。

如果在确认交易后几秒钟内刷新页面，您应该会看到计数器的新值。但是，为了避免需要重新加载页面来更新值，我们将在交易确认后再次查询该值（见列表 2-14）。increaseCounter() {  const counter = this.props.contract;  return counter.methods.increase().send()    .on('receipt', async () => {      const value = await counter.methods.value().call();      this.setState({ value });    });}列表 2-14

在交易被确认后查询计数器的值

send() 方法返回一个事件发射器，允许我们监听交易生命周期中的不同事件。目前，我们只对交易被确认时的事件感兴趣，也就是被包含在链中的块中。这个事件被称为收据，因为它对应于交易收据对象可用时。如果我们愿意，我们也可以检查交易实际发送到节点时，或者达到合理数量的确认时的情况。

现在，即使更新后的代码确实刷新了计数器的值，我们仍然需要让用户知道正在发生什么。交易的确认需要几秒钟，这绝对比常规的 Web 2.0 应用程序通常需要的时间长。

我们将跟踪交易状态（见 2-15）以显示简单的“等待交易”消息，让用户知道发生了什么，并在此期间禁用按钮（见 2-16）。我们还将处理交易失败的情况，以便我们不会永久禁用按钮。当然，在一个真实的 DApp 中，你可能希望提供更好的视觉提示。increaseCounter() {  const counter  = this.props.contract;  this.setState({ increasing: true, error: null });  return counter.methods.increase().send()    .on('receipt', async () => {      const value = await counter.methods.value().call();      this.setState({ value, increasing: false });    })    .on('error', (error) => {      this.setState({ error, increasing: false })    });}Listing 2-15

更新 increaseCounter 函数以跟踪标识挂起交易和任何返回的错误的标志

render() {  const { value, **increasing**, **error** } = this.state;  if (!value) return "Loading";  return (    <div className="Counter">      <div>Counter value: { value.toString() }</div>      <button        **disabled={!!increasing}**        onClick={() => this.increaseCounter()}>          Increase counter      </button>      **<div>{ increasing && "等待交易" }</div>**      **<div>{ error && error.message }</div>**    </div>  );}Listing 2-16

更新渲染方法以在交易挂起或失败时显示通知，并在交易完成前禁用按钮

### 注意

作为等待交易被挖掘的替代方案，我们也可以*乐观地更新*值。乐观更新是一种技术，在超出 DApps 的许多异步应用程序中使用，它假设用户执行的交易将成功，并立即在客户端更新值。这样，用户感知到应用程序几乎立即做出反应，并且可以继续与其进行交互，并对其行动的结果有即时反馈。

当单个用户与合同交互时，这种解决方案已经足够好了，但当涉及到多个用户时就不够了。你可以尝试在两个不同的浏览器窗口打开网站：在一个窗口中进行的任何更改都不会影响另一个窗口，除非重新加载页面查询合同。为了解决这个问题，我们将依赖于合同界面中介绍的最后一个概念：事件。

### 通过事件监视更新

合同的公共界面不仅由公共函数组成。合同还可能在某些交易发生时发出自定义*事件*。我们的 Counter 合同在每次调用增加函数时都会发出一个名为 Increased 的事件，并将计数器的新值作为参数包含在内。

要监视此事件的所有实例，我们将在组件挂载时订阅它，并相应地更新组件状态（见 2-17）。async componentDidMount() {  const counter = this.props.contract;  const initialValue = await counter.methods.value().call();  this.setState({ value: initialValue });  **counter.events.Increased()**    **.on('data', (event) => {**      **const value = event.returnValues.newValue;**      **this.setState({ value });**    **});**}Listing 2-17

订阅 Increased 事件，每当事件的新实例被发出时更新组件的状态

请注意，这里我们引用的是 `counter.events` 属性，而不是之前所做的 `counter.methods`。在这里，事件发射器每次发现新事件时都会触发一个数据事件，并包含事件的参数。

此外，通过在每次事件上更新组件的状态，我们不再需要在确认交易时查询合约状态。`increaseCounter` 函数上的收据事件处理程序可以简化为以下形式。    `.on('receipt', async () => {      this.setState({ increasing: false });    })`

有了这个新的设置，您现在可以接收到合约的实时更新，无论状态变化的来源是什么。再次尝试打开两个浏览器窗口并从其中一个增加计数器，然后查看一旦交易确认后两者如何反映变化。如果你幸运的话，你甚至可能会碰巧遇到另一位读者在同一个合约实例上发出的更改。

### 部署应用程序

您可能已经注意到，我们的示例应用程序仅在客户端运行。所有逻辑都在浏览器中进行，区块链被用作后端来执行简单的计算并保持所有用户之间的共享状态，充当计数器状态的共识层。这使得部署变得简单，因为 DApp 只需作为静态站点托管即可。

## 摘要

在本章中，我们已经经历了开发一个简单 DApp 的过程，为我们的用户提供了一个基本的基于 Web 的界面，用于单个智能合约。我们已经探讨了如何从合约中读取状态并向其发送交易，以及如何监视事件以进行实时更新。

我们构建整个应用程序仅依赖于两个库：用于与以太坊网络交互的 web3js 和作为演示框架的 React。考虑到 JavaScript 和以太坊生态系统中库和框架的变化速度，本书的目标是（并将始终如此）尽可能少地依赖外部依赖，并专注于构建 DApp 背后的概念，而不是专注于当前工具的特定 API。当然，这并不意味着在构建您自己的 DApp 时不应该依赖这些工具，因为它们可能会提供很大帮助。确保在拿到本书时检查 OpenZeppelin、Truffle、Buidler、Etherlime、Embark、Clevis 以及当前可用的其他工具。

总之，本章应该作为整个 DApp 开发过程和组件的概述帮助了您。我们略过了合约本身的部署，以及账户和 ETH 管理的一般情况。我们也没有涵盖与基于区块链的后端处理时出现的许多边缘情况或错误情况。然而，在整本书中，我们将深入研究所有这些主题，包括新的和更高级的内容，并通过更有趣的示例重新审视每一个构建 DApp 的步骤。
