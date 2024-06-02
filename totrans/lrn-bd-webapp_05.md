© Santiago Palladino 2019S. Palladino《面向 Web 开发者的以太坊》[`doi.org/10.1007/978-1-4842-5278-9_5`](https://doi.org/10.1007/978-1-4842-5278-9_5)

# 5. 发送交易

圣地亚哥·帕拉迪诺^(1 )(1)阿根廷布宜诺斯艾利斯自治市

在上一章中我们回顾了如何读取数据并监视网络变化，现在我们将深入探讨通过发送交易来写入数据的方法。我们将首先建立一个开发环境，方便地与智能合约进行交互，然后进入一个启用 web3 的环境，并最终深入讨论发出交易并监控其生命周期的细节。再一次，我们将以一个示例应用程序总结本章的所有学习内容。

## 环境设置

在深入了解交易的细节之前，我们将首先建立一个开发环境，用于构建和测试我们的应用程序。

### 开发节点

与在应用程序中使用远程公共节点不同，这次我们将使用本地私有节点。回想一下上一章中提到的，当一个节点持有一组帐户及其私钥时，它被称为*私有*节点，因此可以用于签署交易。这使得它们更适合脚本编写和测试，因为我们不需要在我们的代码中担心帐户管理，可以将该责任委托给节点本身。

运行本地节点还有另一个好处，就是我们可以创建自己的网络而不是连接到现有的网络。这对于开发特别是自动化测试非常有用，因为我们不需要等待漫长的网络或挖矿时间——我们可以设置自己的网络，几乎立即进行挖矿。这样的网络通常称为*开发网络*。

构建应用程序时的通常工作流程是依赖于本地开发节点进行编码和单元测试，然后转移到测试网络进行更真实的环境测试，并最终进入主网以进行生产部署。

#### 使用 Ganache

最广泛使用的开发客户端之一是*ganache*（原名*testrpc*）。Ganache 是专为开发而建的工具：它不连接到任何以太坊网络 - 它只是启动并运行一个新的开发链。它还创建了一组随机测试账户，每个账户都有一定数量的以太币，并显示它们的私钥和助记词（见 5-1）。$ npm install -g ganache-cli@6.4$ ganache-cli -dGanache CLI v6.4.3 (ganache-core: 2.5.5)可用账户==================(0) 0x90f8bf6a479f320ead074411a4b0e7944ea8c9c1（〜100 ETH）(1) 0xffcf8fdee72ac11b5c542428b35eef5769c409f0（〜100 ETH）......私钥==================(0) 0x4f3edf983ac636a65a......(1) 0x6cbed15c793ce57650......HD 钱包==================助记词：我的神话般的奖金吓唬问题客户蜥蜴开创者提交女性收集基础 HD 路径：m/44'/60'/0'/0/{account_index}......监听 127.0.0.1:8545 列表 5-1

全局安装并运行使用 Ganache 的本地开发网络。请注意-d 标志，代表确定性：使用此标志，ganache 将始终生成相同的账户集合。否则，账户和助记词会在每次运行时发生变化。

### 注意

你可能已经注意到 ganache 输出中的 HD 钱包部分，其中包括一个助记词和一个 HD 路径。HD 代表分层确定性，是从比特币借用的一个概念，用于根据*扩展*私钥/公钥对创建任意数量的账户。不深入技术细节，通过提供不同的*派生路径*（如 ganache 输出中显示的 m/44’/60’/0’/0/0、m/44’/60’/0’/0/1 等），可以从扩展对创建新的私钥/公钥对。扩展对本身可以从*助记词*派生出来：一组随机生成的单词，更容易记忆或记下。总的来说，这允许从一组单词中安全地派生出无限数量的账户。我们将在第七章中深入讨论这个问题。

Ganache 默认采用即时封存，意味着每当收到新交易时，新区块会立即被挖掘并添加到链中^(1)。为了测试这一点，通过 ganache-cli 启动一个新的 ganache 实例（清单 5-3）。在另一个终端上，使用 web3@1.2.0 创建一个新项目，并启动一个新的控制台^(2)（清单 5-2），在那里我们将执行一个交易。 .$ npm init -y$ npm install web3@1.2.0$ node --experimental-repl-await> // 加载 web3 并连接到节点> let Web3 = require('web3')> let web3 = new Web3('http://localhost:8545')> // 将前两个账户加载为 alice 和 bob> let [alice, bob] = await web3.eth.getAccounts()> // 检查 bob 的初始余额（记住 1ETH = 1e18 Wei）> await web3.eth.getBalance(bob) / 1e18100> // 从 Alice 发送 1ETH 到 Bob> // 注意，交易立即被挖掘> web3.eth.sendTransaction({from: alice,to: bob,value: 1e18})> // 再次检查 bob 的余额，并查看额外的 1ETH> await web3.eth.getBalance(bob) / 1e18101Listing 5-2

在 ganache 生成的两个帐户之间测试发送 1ETH。当你发送交易时，密切关注 ganache 日志：你会注意到它被立即处理和挖掘。

> ganache-cli -d 在 127.0.0.1:8545 上监听 eth_gasPriceeth_getBalanceeth_sendTransaction  交易：0x6c79e178...  Gas 使用：21000  块号：1eth_getTransactionReceipteth_getBalanceListing 5-3

之前列出的 ganache 日志的输出结果

你可以指定一个 blockTime（以秒为单位）来替代 ganache 在每笔交易上挖掘一个新块，该参数表示生成新块的时间间隔。虽然比即时封存慢，但这更好地展示了实际链的运作方式。

你也可以通过发送特殊的 evm_mine 指令来随时强制 ganache 进行新块挖掘，该指令通过其 JSON-RPC 接口发送（见 5-4）。该指令是特定于 ganache 的，不是标准的 JSON-RPC API 的一部分。

通过直接通过提供者发送 evm_mine 调用来向 ganache 开发区块链添加新块。Ganache 还支持 evm_increaseTime 调用来模拟时间流逝，这对自动化测试特别有用。

默认情况下，ganache 生成的所有链都是临时的：当 ganache 进程停止时，它们将丢失。这可以通过使用 db 选项启动 ganache 并将其状态存储在本地文件夹中来更改，如下所示。

确保运行 --help 命令以检查所有可用选项：ganache 是一个非常灵活的测试工具，允许您设置任意账户和任意余额。它甚至可以从现有的链上分叉，以在实际网络上运行操作的干跑。

#### Geth 或 Parity 的开发模式

在开发中使用 ganache 的替代方法是与常见的以太坊客户端一起工作，例如 Geth 或 Parity，并设置为开发模式。这种模式会创建一个由节点完全管理的新的私有区块链，可以选择立即封存。虽然它们在测试方面比 ganache 提供的灵活性较少，但它们更具代表性，因为您连接的应用程序与您在生产中连接的客户端相同。

### 注意

虽然我们将把本节的其余部分重点放在 Geth 上，但请确保也查阅 Parity 的文档，以查看其开发模式的可用选项。^(3)

要以开发模式启动 geth，请将其安装在您的工作站上^(4)，然后运行以下命令。确保首先停止我们之前启动的 ganache 实例（如果它仍在运行），因为两者都会尝试使用相同的端口。$ geth --datadir=geth-data --rpc --ws --dev --dev.period=1

这将在默认的 8545 端口上打开 HTTP 接口，并在 8546 端口上打开 websocket 接口。dev.period 选项指定了应该在其中挖掘新块的间隔（以秒为单位）– 省略此选项会切换为与 ganache 中的立即封存相同。还请注意 datadir 选项，它将所有区块链数据存储在本地 geth-data 目录中；如果您不设置此标志，geth 将在家目录的默认位置存储所有数据。

在启动时，Geth 将创建一个包含大量以太币的单一帐户用于开发。但是，如果您想生成额外的帐户，可以使用帐户子命令，并设置与原始 geth 命令相同的 datadir。$ geth --datadir=geth-data account newYour new account is locked with a password. Please give a password. Do not forget this password.Passphrase:Repeat passphrase:Address: {3975c2...}Geth 将要求您输入密码来加密帐户，您可以在开发网络中留空（但绝对不能在真实网络中这样做！）。所有以太坊客户端都会加密用户帐户，直到所有者要求使用它们为止。因此，要实际使用帐户，所有者必须首先通过提供密码来解锁它。让我们来测试一下：我们将再次启动一个节点控制台并连接到节点。$ node --experimental-repl-await> // Load web3 and open a connection to the node> let Web3 = require('web3')> let web3 = new Web3('http://localhost:8545')> // List accounts on the node> let accounts = await web3.eth.getAccounts()[ '0xC5A4bA36f7C0B4eD17455C1A578a6ab3Fb738245', ...]> // Send a transaction from the always-unlocked dev account> await web3.eth.sendTransaction({ from: accounts[0], to: accounts[1], value: 5e18 }){ transactionHash: '0x18737033...', ... }> // Try sending a transaction from the newly created account> await web3.eth.sendTransaction({ from: accounts[1], to: accounts[0], value: 1e18 })Returned error: authentication needed: password or unlockUnlocking an account requires access to the *personal* API, which is disabled by default on the HTTP interface. To avoid going into detail on how to configure API accesses for a node, we will simply restart the geth process supplying an unlock option with the comma-separated list of addresses we want to freely use. Geth 将在启动时提示输入帐户密码。$ geth --datadir=geth-data --rpc --ws --dev --dev.period=1--unlock=3975c2...

### 注意

到目前为止，我们只与节点的 eth API 进行交互，该 API 用于与以太坊网络进行常规交互。但是，节点还提供其他 API，用于管理账户、管理节点、挖矿，甚至调试。启动选项控制哪些 API 通过哪些接口提供：默认情况下，诸如个人或管理的敏感 API 仅通过 IPC 接口本地公开。

请记住，geth 节点可以在开发模式下使用，在连接到测试网时使用，或者直接连接到主网。当在实际网络上工作时，您只需将 dev 启动选项替换为指定要连接的以太坊网络的 networkid。

请记住，与比特币不同，以太坊账户对于任何网络都是有效的，因此要特别小心不要混淆您的开发账户和主网账户。在不同网络使用不同地址是一个好习惯。您可不想在开发中从默认账户中转走 10ETH，最后才意识到您实际上是在主网上运行。

### 创建合约

现在我们有了一个本地节点并设置了开发网络，我们将介绍编译和部署智能合约的过程。请记住，由于我们正在使用全新的开发网络，因此没有已部署的合约供我们进行交互，所以我们需要创建所有合约。

#### 编译

首先，在新的项目文件夹中，创建一个名为 contracts/Greeter.sol 的新文件，其中包含一个我们将用于测试的 Greeter 合约。// contracts/Greeter.sol

然而，Solidity 编译器的命令行界面相当有限。更复杂的应用程序的推荐用法是标准的 JSON 接口，该接口接受一个用于配置编译任务的 JSON 文件，并为每个合约输出一个文件。但需要注意的是，手动使用该接口相当复杂。

尽管如此，还有一些包装器为编译器提供了更友好的界面。在这里，我们将使用来自 0x 团队的 sol-compiler，它是标准 JSON 格式的一个薄包装器。使用以下命令安装并运行它，它将为每个合约生成一个 JSON 文件，保存在 artifacts 文件夹中。  .$ npm install -g @0x/sol-compiler@3.1$ sol-compiler sol-compiler 生成的输出文件具有以下结构。请注意，可以设置 compiler.json 配置文件^(6)来控制生成哪些字段，以及一些编译器选项，例如优化器。{  "contractName": "Greeter",  "compilerOutput": {    "abi": [ {"constant": true, ... } ],    "evm": {      "bytecode": {        "object": "0x6080..."      }    }  }}

*sol-compiler 的简化样本输出*。

### 注意

虽然内容与之前通过 solc 的 JSON 选项生成的内容相同，但组织形式不同。从现在开始，我们将在所有示例中使用 sol-compiler 的输出。

#### 部署

现在我们已经编译了我们的 Solidity 文件，我们可以将它们部署到我们的开发网络上。虽然有许多工具可以为我们管理这个过程，但我们将尽可能保持我们的工具链简单，并仅依赖 web3 来完成这个过程。

使用 web3 部署合约，首先需要创建一个 web3 合约对象，确保我们提供了合约的二进制代码（可以从编译后的构件中提取）。我们将忽略构造函数的第二个参数，即合约地址，因为它目前还不存在。Greeter = new web3.eth.Contract(abi, null, { data: binary })获得合约对象后，我们可以通过提供一个解锁的发送者账户和一定的 gas 金额来调用 deploy 方法。返回的对象是一个完整的可与之交互的 web3 合约。greeter = await Greeter.deploy().send({ from, gas: 1e6 })让我们把所有这些放在一个新的 scripts/deploy.js 文件中（见 5-5）。我们将从 artifacts 文件夹中检索 ABI 和字节码，并连接到一个本地节点来运行部署。// scripts/deploy.jsconst Web3 = require('web3')const GreeterJSON = require('../artifacts/Greeter.json')async function deploy() {  const web3 = new Web3('http://localhost:8545')  const [from] = await web3.eth.getAccounts()  const gas = 1e6  const arguments = ["Hello world!"]  const data = GreeterJSON.compilerOutput.evm.bytecode.object  const abi = GreeterJSON.compilerOutput.abi  const Greeter = new web3.eth.Contract(abi, null, { data })  const greeter = await Greeter.deploy({ arguments })                               .send({ from, gas })  console.log(greeter.options.address);}deploy();清单 5-5

Greeter 合约的部署脚本。请注意，data 和 abi 是从 sol-compile 生成的 JSON 文件中提取的，发送者账户设置为节点中的第一个账户。

要测试这一点，请确保首先启动一个 ganache 实例（或一个开发模式下的 geth），监听默认端口 8545。然后通过 node scripts/deploy.js 运行上述脚本，其应该输出部署地址。然后我们可以启动一个 javascript 控制台连接到节点，并运行合约的 greet 函数(Listing 5-6)来验证一切是否按预期工作。$ node --experimental-repl-await> Web3 = require('web3')> GreeterJSON = require('../artifacts/Greeter.json')> let web3 = new Web3('http://localhost:8545')> let abi = GreeterJSON.compilerOutput.abi> let greeter = new web3.eth.Contract(abi, '0xa42d93...')> await greeter.methods.greet().call()'Hello world!'Listing 5-6

用于在部署地址初始化 greeter 合约对象并测试调用 greet 函数的脚本。确保用实际部署地址替换示例地址

部署脚本虽然简单，但可以推广到应用程序中的任何合约，并修改以接受命令行选项或环境变量以配置连接到节点、发送帐户或构造函数参数。将部署地址保存到本地文件而不仅仅是在控制台中输出也是一个好主意。当我们构建一个完整的应用程序时，我们将在本章末再次讨论这个问题。

### 管理账户

我们下一步将是账户管理，包括在开发环境中创建和种子账户，以及从我们的 Web 应用中访问它们。

#### 重温 Metamask

与以往章节一样，我们将依靠 Metamask 从我们的 Web 应用连接到网络。不过，我们现在将在一个本地开发网络上工作，而不是在实际的以太坊网络上。我们将在稍后阶段切换到测试网络和主网络。

### 注意

正如我们之前指出的，以太坊中的地址在所有网络中都是有效的。这意味着你可以在测试网、主网，甚至本地开发网络中使用相同的私钥和地址对。当然，能够并不意味着应该。最好使用完全不同的账户，因为你会希望对*真实*网络中的账户密钥进行特殊的关注。不幸的是，Metamask 将在所有网络中使用相同的账户集，这些账户都是从相同的助记词派生的。为了避免将开发账户和真实账户搞混，一些开发者选择在开发时运行不同的浏览器配置文件，这样他们就可以拥有完全独立的账户集。

你的第一步将是将 Metamask 连接到你的开发网络（图 5-1）。点击扩展中的网络下拉菜单，并选择连接到 *本地主机 8545*，这是你的开发节点正在运行的地方。

或者，如果你已经在不同的端口上设置了开发节点，你需要将其注册为一个新的网络。要做到这一点，转到 *设置*，选择连接到 *新网络*，并输入到你启动 ganache、geth 或 parity 的端口的 localhost 的 HTTP 连接（默认为 8545）。

图 5-1

在 Metamask 中创建新的网络连接

现在，我们需要为 Metamask 帐户提供资金，以便通过它发送交易。请记住，由于这是一个新的网络上的新帐户，它没有余额。复制您的 Metamask 地址，并像之前一样打开控制台，从您的初始帐户将资金转移到 Metamask 帐户。$ node --experimental-repl-await> // 加载 web3 并连接到节点> let Web3 = require('web3')> let web3 = new Web3('http://localhost:8545')> // 获取节点上的第一个帐户> let [from] = await web3.eth.getAccounts() '0xC5A4bA36f7C0B4eD17455C1A578a6ab3Fb738245', ...> // 在此处复制您的 Metamask 地址> let metamask = '0x43a93b...';> // 从您的开发者帐户种子化您的 Metamask 地址> await web3.eth.sendTransaction({ from, to: metamask, value: 5e18 })

除了手动填写地址种子的方法，还可以在 Metamask 上使用自动生成的开发帐户，如果您正在使用 ganache，这很容易实现。由于 ganache 和 Metamask 都依赖于助记词来生成新的地址，您可以在它们两者上使用相同的助记词，以确保使用相同的帐户。

为了完成这一步，您需要在 Metamask 初始化向导（图[5-2）中选择*使用助记词导入*选项，并输入 ganache 启动时显示的 12 个单词。

### 提示

如果您使用--deterministic 标志启动 ganache，则该助记词应为：myth like bonus scare over problem client lizard pioneer submit female collect。请确保不要在开发环境之外使用此助记词！

![../images/476252_1_En_5_Chapter/476252_1_En_5_Fig2_HTML.jpg](img/476252_1_En_5_Fig2_HTML.jpg)

图 5-2

将 ganache 助记词输入 Metamask

相反的方式也是可行的。你可以获取你在 Metamask 中生成的助记词，并在 ganache 中输入它。这样，ganache 创建的所有开发帐户，并在新网络中以资金种子方式创建的帐户将与 Metamask 创建的帐户相同。如果你不记得你的 Metamask 助记词，有一个在*设置*下的选项*显示助记词*。

不管你使用的是三个选项中的哪一个，你现在应该在 Metamask 上有一个或多个帐户，其中有足够的资金来与你的开发网络中的应用进行交互。

#### 在我们的应用程序中检索用户帐户

从上一章记得我们在 Web 应用程序中连接到网络所使用的脚本。我们在这里只重现现代 web3 浏览器对应的代码片段。if (window.ethereum) {  web3 = new Web3(window.ethereum);  try {    accounts = await window.ethereum.enable();  } catch (error) {    console.error("无法访问用户帐户");  }}

全局 Ethereum 对象，由 web3 浏览器注入（或者在我们的情况下是 Metamask 扩展），允许我们与以太坊网络和用户的帐户进行交互。这里最重要的方法是 enable，它将触发一个提示，询问用户是否允许我们的应用程序列出他们的帐户。

需要牢记的是，从 ethereum.enable() 或 web3.eth.getAccounts() 返回的帐户列表是有序的，用户打算使用的帐户始终是第一个。因此，在发送任何交易之前，我们应该先重新获取用户帐户列表，并在那一刻使用第一个，这可能已经在我们初始化 web3 实例后发生了变化。

或者，如果您想保持用户当前账户状态的显示，您可以订阅 ethereum 对象上的 accountsChanged 事件（见 5-7）列表，每当用户切换到新账户时触发该事件，从而允许您相应地更新界面。ethereum.on('accountsChanged', async function (accounts) { currentAccount = accounts[0]; currentBalance = await web3.eth.getBalance(currentAccount); // Show currentBalance in the UI})Listing 5-7

Metamask 上观察用户账户变化并相应更新 UI 的示例代码

现在我们已经设置好了本地开发环境，我们可以终于深入了解在该网络中发送交易的详细信息了。

## 发出交易

尽管发送交易的要点很简单，但您应该考虑到一些细节。我们将在本节中逐一讨论它们，然后在一个样本 dapp 中进行说明。

### 交易参数

我们将从审查发送交易时可用的参数开始：数据、价值、燃气和燃气价格，以及发送者和目标地址。

#### 发送价值或数据

首先要考虑的一件事是您的交易是否将发送价值、数据或两者兼而有之。这里所说的价值是指以太币（ETH），即网络的货币，而数据通常指执行合约中的函数。在某些情况下，可能两者都包括：运行合约中需要随之转移 ETH 的函数。

简单地向地址发送 ETH 是直接的，正如我们在本章中已经看到的那样，使用 web3.eth.sendTransaction 方法。请记住，向合约发送普通交易仍然可能执行代码，因为合约可以通过其回退函数对传入交易做出反应。

另一方面，在合约中调用改变状态的函数类似于进行静态调用：可以通过发送一个带有手工制作的数据参数的交易来以低级别执行，该参数指示必须在目标合约上调用哪个函数以及使用哪些参数，或者通过与 web3 合约对象进行交互。

为了说明这一点，让我们在“*创建合约*”部分的 Greeter 合约基础上扩展一个额外的 setGreeting 方法（见列表 5-8）。这个方法将允许任何用户更改当前的问候语，只要他们支付至少 1 kWei。// contracts/Greeter.sol

示例的 Greeter 合约带有一个 setGreeting 函数。注意，我们正在发出一个与我们从函数返回的相同数据的事件。我们将在本章后面看到原因。

使用 sol-compile 将该合约编译并部署到您的本地网络上，同时使用我们之前编写的部署脚本。我们现在可以像下面展示的那样从节点控制台与合约进行交互。$ node --experimental-repl-await> Web3 = require('web3')> GreeterJSON = require('./artifacts/Greeter.json')> let web3 = new Web3('http://localhost:8545')> let abi = GreeterJSON.compilerOutput.abi> let greeter = new web3.eth.Contract(abi, ADDRESS)我们可以通过在 greeter 实例中调用方法来测试 setGreeting 函数（见 5-9）。请注意，与上一章不同，我们使用的是 send 而不是 call – 这将触发一个新的交易而不是静态调用。我们还需要指定一个发送方帐户，其燃气费将从其余额中扣除。由于 setGreeting 方法要求我们在交易中发送一些 ETH，因此我们还包括一个 value 选项。> let [from] = await web3.eth.getAccounts()> let value = 1000> greeter.methods.setGreeting('Hi there!').send({from, value})> await greeter.methods.greet().call()*'Hi there!'*[5-9]

发送交易以更改我们合约的问候语

### 注意

在 web3.js 中，作为合约函数一部分的参数设置在相应的合约方法上，而交易选项则通过发送或调用方法传递。

如前所述，我们也可以手动构造要发送的数据，以调用合约中的函数，然后使用低级别的 sendTransaction（见 5-10）。您可能实际上不会使用此模式，但知道在从 web3 合约对象发送交易时发生了什么是有用的。> let to = ADDRESS> let data = greeter.methods.setGreeting('Hi!').encodeABI()> web3.eth.sendTransaction({ from, value, data, to })[5-10]

使用低级别的 sendTransaction 调用 setGreeting。请注意，我们需要将目标地址指定为另一个选项

### 注意

如果你对数据的内容感到好奇，你可以查看它包含以下十六进制序列：

0xa4136862000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000034869210000000000000000000000000000000000000000000000000000000000

尽管有些吓人，但这个序列对应于我们提供的以 RLP 编码的数据的 ABI 调用。RLP，即递归长度前缀，是一种编码任意嵌套数据的方法，长度也是任意的。^(7) 在这种情况下，前 8 个字节（a4136862）是函数选择器，告诉合约必须调用 setGreeting。其余的有效载荷对应于“Hi!”的 RLP 编码。

#### 估算燃气

让我们再次尝试 setGreeting 方法，但这次使用一个更长的字符串作为函数的参数。> const longGreeting = 'Hi there! This is a very long and costly greeting to set which will require more gas.'> await greeter.methods.setGreeting(longGreeting)    .send({ from, value})*Error: Returned error: VM Exception while processing transaction: out of gas*

请记住，从第三章可以知道，在以太坊中执行交易需要燃气。交易的总燃气成本与执行的所有操作的累积成本成比例，不同的操作有不同的燃气成本。写入存储是一项特别昂贵的操作，因为它意味着在区块链中持久化新状态。而且数据越大，涉及的存储操作就越多。

在上面的例子中，试图将一个非常大的字符串保存到此合约的状态中，我们超出了交易的燃气津贴（在 web3@1.2.0 中默认为 90,000），因此交易失败了。

我们可以通过为其执行分配更多的燃气来使此事务工作（清单 5-11）。例如，让我们尝试使用 100 万燃气单位。请记住，这并不意味着事务实际上将使用 100 万燃气，只是我们愿意在其执行中花费这么多。

运行上一个事务时分配更多的燃气。注意，返回的事务收据包含事务实际使用的燃气，这远远低于 100 万。

这引发了一个问题，即我们如何知道要为事务分配多少燃气。一个选择可能是简单地指定一个非常高的燃气津贴：大多数网络的块燃气限制在 400 万到 800 万燃气之间，所以我们可以简单地使用一个在这个范围内的值。

然而，如果我们这样做，我们的用户将被要求接受可能比他们愿意放弃的资金更多的事务（图 5-3）。任何查看燃气费用数字的用户很可能会拒绝在这些条件下运行事务。

图 5-3

相同事务的 Metamask 确认对话框使用不同的燃气津贴：左边使用默认燃气量；右边使用 500 万。请注意 USD 的费用差异：用户被要求投资高达 9 美分对比 10 美元。

要解决这种情况，我们可以在实际发送交易之前*估算*交易将耗费的气体（见 5-12）。以太坊节点实现了一个 estimateGas 方法，接受一个交易并在本地运行它，以确定运行它所需的气体量。> gas = await greeter.methods.setGreeting(longGreeting)    .estimateGas({ from, value })> await greeter.methods.setGreeting(longGreeting)    .send({ from, value, gas })5-12 节

使用 estimateGas 来计算交易所需的气体数量。在这种情况下，estimateGas 的返回值约为 98K

在某些情况下，estimateGas 返回的值可能不完全等于实际使用的气体量。这是因为估算依赖于调用时网络的状态，而实际的气体量仅在交易实际被挖掘时确定。在这两个事件之间，合同的状态可能已经发生了变化，这可能会改变所需的气体量。^(8)

因此，最好是在估算气体调用返回的值上分配稍高一点的气体量（见 5-13）。增加 20%通常就足够了，尽管你的情况可能会因你所使用的合同而有所不同。另外，请确保不要将气体津贴设置为超过区块气体限制，否则交易将被简单地拒绝。> let lastBlock = await web3.eth.getBlock('latest')> let limit = lastBlock.gasLimit> gas = Math.min(limit - 1, Math.ceil(gas * 1.2))5-13 节

计算交易中实际使用的气体数量

值得注意的是，如果在估算气体时交易失败，则估算调用将失败，并显示“总是失败的交易”错误。这可以防止你发送一笔最终会失败的交易到网络中去。

#### 选择气体价格

交易不仅需要一个 gas 限制，还需要一个 gas 价格。从第三章记得 gas 价格表示每个交易执行过程中使用的每单位 gas 所支付的数量（以 Wei 计）。尽管在开发或测试网络中这个值不重要，但在主网络或任何其本地货币具有实际货币价值的网络中，它们对于准确性至关重要。

毋庸置疑，使用更高的 gas 价格将导致更昂贵的操作。另一方面，高于平均 gas 价格意味着交易将更早地被矿工拾取；这减少了用户必须等待其交易包含在区块链中的时间。

Gas 价格会根据总网络负载的情况而波动。在以太坊网络被密集使用时，有更多竞争来使得交易被包含在下一个区块中，这会推高 gas 价格。

估算 gas 价格比估算 gas 允许额困难得多，因为不能仅通过对交易进行干扰运行并检查总使用量来获得估算值。相反，估算价格需要对过去和待处理的交易进行分析。

获得 gas 价格估算的最直接方式是依赖以太坊节点的 gasPrice API 方法（见清单 5-14）。节点保留一个 gas 价格值，该值会以预先配置的频率进行更新，并根据最近几个区块中交易的 gas 价格的百分位数进行计算。> await web3.eth.getGasPrice()*'20000000000'*清单 5-14

查询以太坊节点的 gas 价格。请注意，ganache 返回 gas 价格的常量值，可以在启动时进行配置。

### 注意

当通过 Metamask 运行 getGasPrice 时，一个子提供程序会拦截调用并手动计算 gas 价格，作为最后 N 个区块的中值。

然而，该方法只考虑已经挖掘的交易数据，而忽略了在 mempool 中等待包含在区块链中的未决交易的任何信息。

作为替代方案，有一些集中式服务为以太坊主网络提供实时燃气估算（参见 5-15）。这些服务基于更复杂的计算，通常返回更好的结果，但以引入对应用程序的集中式依赖为代价。此类服务由 Etherchain 或 EthGasStation 等提供，并为低、标准、快速或最快的交易处理提供燃气价格。$ npm install axios@0.18.0$ node --experimental-repl-await// 设置 web3 提供程序和合同> Web3 = require('web3')> GreeterJSON = require('./artifacts/Greeter.json')> let web3 = new Web3('http://localhost:8545')> let abi = GreeterJSON.compilerOutput.abi> let greeter = new web3.eth.Contract(abi, ADDRESS)// 检索燃气价格并发送交易> axios = require('axios')> let URL = 'https://www.etherchain.org/api/gasPriceOracle'> let { data: gasData } = await axios.get(URL)> let gasPrice = gasData.fast * 1e9> await greeter.methods.setGreeting('Hello!')    .send({ from, value, gas, gasPrice })列表 5-15

从 Etherchain API 获取燃气价格并在交易中使用。此代码片段使用 axios 包执行标准的 HTTP GET 请求到 API。

### 交易的生命周期

现在我们知道如何配置交易的主要组件，是时候审查一下一旦交易发送后会发生什么以及我们如何与其交互了。

#### 交易已发送

当交易发送到节点时，节点会执行一些基本检查，以确保交易有效并可以广播。例如，节点会检查发送者账户是否有足够的资金，并且燃气允许量和价格值是否合理。

如果节点接受了交易，则返回交易的哈希。 此交易哈希充当区块链上交易的全局唯一标识符，并且可以用来稍后检索交易的信息。> let txHash = null> greeter.methods.setGreeting('Hello!')    .send({ from, value })    .on('transactionHash', (hash) => txHash = hash)

### 注意

如果需要，交易哈希可以由客户端离线计算，只要客户端有发送者的私钥，因为它完全依赖于其参数和签名。

当交易哈希返回时，无论交易是否已经被挖掘，任何看到过这个交易的节点（见列表 5-16）都可以从中检索交易信息。 这些信息包括发送者、接收者、gas 津贴、价格、nonce、输入数据以及发送交易时可能指定的所有内容。> await web3.eth.getTransaction(txHash){ blockHash: '0x0000...0',  blockNumber: null,  from: '0x...',  gas: 90000,  gasPrice: '1000000000',  hash: '...',  input: '0xa41368620...',  nonce: 470,  to: '0x...',  transactionIndex: 0,  value: '1000'}列表 5-16

交易发送后立即返回的信息。 请注意，所有与区块相关的信息都为空，因为交易尚未被挖掘

此时，交易尚未被挖掘，被称为 *待处理* 状态。 任何试图检索交易收据的尝试都将简单地返回 null。

#### 交易已被挖掘

一段时间后，根据使用的 gas 价格和网络负载的不同，交易应该会被挖掘。 请注意，交易无论成功与否都会被挖掘：已撤销的交易也会被包含在区块链中，并且会从发送方那里消耗 gas 费用。

一旦交易被打包，其 getTransaction 信息将包括所包含的区块号和哈希，以及其在区块中的索引。此时，交易收据也变得可用。> await web3.eth.getTransactionReceipt(txHash){ transactionHash: '0x...',  transactionIndex: 0,  blockHash: '0x...',  blockNumber: 29,  gasUsed: 23235,  cumulativeGasUsed: 23235,  logs: [ ... ],  status: true}

收据包含在挖矿期间执行交易时生成的信息，如实际使用的 gas，交易是否成功（如果交易没有回滚，则状态标志为 true），以及它发出的日志。

### 注意

如果您检查通过 getTransactionReceipt 调用获取的交易收据中的日志，您只能获取事件的原始数据。这是因为客户端库没有足够的上下文来理解如何*解码*这些日志。它需要一个 ABI 来指示事件名称和参数类型。

我们可以通过检查新块（通过轮询或订阅新区块头）并在看到新挖掘的块时尝试检索事务收据来等待事务被挖掘（见 5-17）。如果事务成功在新块中挖掘，那么它的收据将可用。// 将事务发送到网络并返回其哈希函数 sendTransactionReturnHash(opts) {  return new Promise((resolve, reject) => {    web3.eth.sendTransaction(opts)      .on('transactionHash', hash => resolve(hash))      .on('error', err => reject(err));  })}// 发送事务并等待其被挖掘 function sendTransactionAwaitReceipt(opts) {  const BLOCKS = 'newBlockHeaders';  return new Promise((resolve, reject) => {    sendTransactionReturnHash(opts).then(hash => {      const sub = web3.eth.subscribe(BLOCKS, (err) => {        if (err) reject(err);        // 每个新块上检查收据        // 如果可用，则表示 tx 已经被挖掘        web3.eth.getTransactionReceipt(hash).then(receipt => {          if (receipt) {            sub.unsubscribe();            **resolve(receipt);**          }        });      });    }).catch(reject);  });}第 5-17 节

订阅新的区块头以检查事务是否成功被挖掘。请注意，如果您有多个正在进行的事务，将新区块头的订阅共享给它们中的所有可能是值得的

如果使用 web3，只需等待 sendTransaction 方法（无论是发送普通交易还是触发合约函数交易）即可获得交易收据。这还可以轻松访问事件，根据发出交易的合约对象的 ABI 进行解码。> let receipt = await greeter.methods.setGreeting('Hey!')    .send({ from, value: 10000 })> let { events } = receipt> let { greeting, balance } = events.GreetingSet.returnValues> greeting*'Hey!'*> balance*'30000'*

能够处理事务事件特别重要，因为*无法检索在事务中调用的函数的返回值*。如果回到我们合约的代码，你会看到我们的函数实际上返回了问候语字符串和合约余额。但是，按设计，这些值不是交易收据的一部分，无法从客户端获取。

### 注意

从事务中的函数获取返回值的唯一方法是从另一个合约调用它们：调用 setGreeting 的合约将可以访问它们，但是发送交易到 Greeter 的链下客户端将无法访问它们。

因此，智能合约设计中的常见模式是，公共状态更改函数通过事件发出其返回值（见 5-18）。这允许外部账户调用此类函数并从事件参数中检索返回值。function setGreeting(string memory _greeting)  public payable returns (string memory, uint256){  greeting = _greeting;  // This can only be accessed by a client off-chain  emit GreetingSet(_greeting, address(this).balance);  // This can only be accessed by another contract calling  return (_greeting, address(this).balance);}Listing 5-18

发出带有模拟返回值数据的事件，以便客户端可以访问它们

#### 事务已确认

尽管立即对挖掘出的交易进行操作可能很诱人，但由于重新组织的原因，交易可能会移出区块链。这意味着挖掘出的交易可能会重新回到待处理状态，然后再次被挖掘或被丢弃 - 甚至在不同的上下文中挖掘时可能会产生不同的状态更改。

因此，在实际对交易进行操作之前等待一定数量的确认可能是明智的。*对交易进行操作*的意思取决于您的用例，以及等待的确认数量。请记住，确认是指包含交易的区块之后已挖掘的区块数：每挖掘一个新区块都是您的交易的新确认。随着链上添加更多的区块，重新组织变得越来越不可能。

可以通过订阅网络上的新区块（见第四章）并计算自交易收据以来的区块数来衡量交易确认。我们可以修改前一节中的代码，使其在发生一定数量的确认后才返回（见代码清单 5-19），而不是在收据立即可用时返回。function sendTransactionAwaitConfirmations(opts, confs) {  const BLOCKS = 'newBlockHeaders';  return new Promise((resolve, reject) => {    sendTransactionReturnHash(opts).then(hash => {      const sub = web3.eth.subscribe(BLOCKS, (err, block) => {        if (err) reject(err);        // Instead of just checking that the receipt exists,        // now we also check its age in blocks        web3.eth.getTransactionReceipt(hash).then(receipt => {          if (receipt &&          **block.number > receipt.blockNumber + confs**) {            sub.unsubscribe();            **resolve(receipt);**          }        });      });    }).catch(reject);  });}代码清单 5-19

修改 sendTransactionAwaitReceipt 函数以在返回收据之前等待特定数量的确认。请注意，重要的是在每个块上重新获取交易收据，因为它可能由于链重组而更改

或者，web3 还提供了一个事件来跟踪交易发送后的确认（见列表 5-20），它在底层执行类似的逻辑。> greeter.methods.setGreeting('Hello!')    .send({ from, value })    .on('confirmation', (number, receipt) => {      if (number === 12) {        console.log(receipt.events.GreetingSet.returnValues)      }    })列表 5-20

在使用来自 web3 的确认事件处理程序之前，等待 12 个确认

### 替换交易

未被挖掘的交易可以通过其发送者进行*替换*，方法是黑客入侵 nonce 和 gas 价格参数。请记住，要使交易有效，其 nonce 不能由发送者先前使用过。因此，如果发送者在第一个交易仍在挂起状态时广播具有相同 nonce 的第二个交易，则两个交易都有资格被挖掘，尽管只会有一个。为了强制选择第二个交易，发送者只需以比第一个交易更高的 gas 价格发出它即可。

测试此功能的一种简单方法是发出具有非常低的矿工费的第一笔交易，以确保需要多个区块才能被挖掘，这样我们就有足够的时间发送第二笔交易来替换它。请确保在没有即时封印的网络中测试此功能；否则，第一笔交易将立即被挖掘。// 发送价值为 0.02 ETH 的第一笔交易> let to = accounts[1]> let value = 2e16> let gasPrice = 100> let txOpts = { from, to, value, gasPrice };> let txHash = await sendTransactionReturnHash(txOpts)// 检索 nonce> let { nonce } = await web3.eth.getTransaction(txHash)// 以不同价值和更高矿工费发送替换交易> value = 1e16> gasPrice = 20e9> txOpts = { from, to, value, gasPrice, **nonce**}> let txHashReplace = await sendTransactionReturnHash(txOpts)// 验证只有替换交易被挖掘> await web3.eth.getTransactionReceipt(txHash)*null*> await web3.eth.getTransactionReceipt(txHashReplace)*{ status: true, ... }*替换交易有多种用途，因为第二笔交易与原始交易除了 nonce 和发送方账户外无需有任何相同之处。

+   替换交易最常见的用法是加速原始交易。如果您发现某个交易的挖掘时间太长，您可以简单地重新提交该交易，参数完全相同，但矿工费更高，以使其对矿工更具吸引力。在用户体验方面，这也是一种简单的模式实现：如果您在处理交易时向用户显示加载指示器，您可以在长时间没有消息后显示重新提交选项。Metamask 已经在其 UI 中默认包含了此功能。

+   另一个用途是简单地取消交易。如果用户想要撤销已发送的交易，一个可行的选择是发送一个无操作的替代交易，以移除先前的交易。无操作交易可以简单地是一笔价值为`0 ETH`且没有数据的交易，接收地址与发送者相同。

+   或者，可以发送一个替代交易来更改先前交易的参数，作为修正先前交易的手段。这将严重依赖于你的使用情况，并且需要用户能够快速执行，因为如果原始燃气价格已经很高，那么获取交易替换的窗口可能很短。

### 错误处理

当向网络发送交易时，有许多潜在的问题可能发生。你的应用程序应该准备好处理它们，并相应地通知用户：

+   在任何时候，你都可能失去与节点的连接。不用说，这不仅会影响发送交易，还会影响与网络的任何读写操作。在这些情况下，你通常会收到一个*Invalid JSON-RPC response*错误，因为你的库将会从无法访问的节点获得一个空响应。

+   被发送的交易可能无效。这可能是由于其参数之一不是良好形式，比如一个非十六进制字符串的地址，或者一个明显无效的值。作为后者的例子，如果你试图发送一个燃气配额为`1`的交易，你将会收到一个*intrinsic gas too low*的错误。这些错误通常在构建要发送的交易时被你的库捕获。

+   发送方账户可能没有足够的资金用于交易的指定值、燃气配额和燃气价格。这些错误通常在交易甚至广播之前由节点报告。

+   当替换交易时，尝试替换已挖掘的交易将在将交易发送到网络之前即产生*nonce too low*错误。同样，大多数客户端将阻止您尝试替换交易而不增加燃气价格。

+   执行合约代码的交易可能会因合约引发的 REVERT 或 ABORT 而失败。Solidity 0.4.22 及以上版本编写的合约可以包含一个回滚原因，该原因可用于确定错误的原因。这仅在交易实际被挖掘并且发送方的资金已被用于支付执行的燃气费用后才会检测到。

+   在估算交易所需的燃气量时，*始终失败的交易*错误意味着估算失败，因为交易引发了错误。这可用于在实际发送交易到网络并花费燃气之前检测到失败的交易。

+   即使你估计了交易所需的燃气量，交易被挖掘时的条件可能与估算燃气时的条件不同。在这些情况下将引发燃尽错误，但只有在交易已经被挖掘后才会出现。

+   在发送交易后，如果燃气价格过低或网络繁忙，可能无法成功挖掘。大多数库最终会超时，并在一定数量的区块后通知你找不到交易。请注意，如果你的用户连接到的节点不同步，那么交易实际上可能已被挖掘，但节点永远不会看到它，从而引发此错误。

### 注意

请记住，实际的错误消息可能取决于你使用的库，以及在某些情况下，你连接的客户端（Geth、Parity 或 Ganache）。

在 web3 中，大多数前面的错误都可以通过错误事件处理程序捕获，类似于发送的事务、收据或确认事件。另一方面，输入格式错误会立即引发异常。> let [from, to] = await web3.eth.getAccounts()> web3.eth.sendTransaction({ from, to, gas: 1 })  .on('error', err => console.error(err.message))*Returned error: intrinsic gas too low*

## 示例应用程序

与上一章相同，我们现在将设置一个示例应用程序，涵盖了本章中我们已经复习过的许多概念。在这种情况下，我们将建立一个简单的界面，允许用户使用修改后的 ERC721 合同创建（铸造）新的数字收藏品。

### 设置

我们的设置将类似于前几章的设置，依赖于 create-react-app 作为客户端样板，^(9) 因为我们将构建一个仅客户端的应用程序。npm init react-app erc721-app

#### 依赖关系

与我们的 ERC20 应用程序相同的一组依赖项一起，我们还将安装 solidity 编译器和用于执行 HTTP 请求的 axios 库。$ npm install web3@1.2.0 openzeppelin-solidity@2.1 bignumber.js@8.0 axios@0.18.0$ npm install --save-dev @0x/sol-compiler@2.0.2

确保您已经安装了 ganache-cli、Geth 或 Parity，如本章前述，在本地开发网络上运行。

#### 合同部署

对于这个应用程序，我们将编写、编译并部署我们自己的合约 contracts/ERC721PayPerMint.sol（见列表 5-21）。这将是一个基于默认 ERC721 实现的合约，我们将从 OpenZeppelin 合约库中获取，其中还包括一个额外的方法，以 ETH 费用交换创建新实例。ETH 将保留在合约中，直到其所有者决定提取它。

修改后的 ERC721 代币将支持我们的应用程序。它提供了一个公共铸币功能，用户可以支付费用创建新代币，以及一个查看功能来检查代币是否存在。

现在我们可以尝试使用 sol-compiler 编译我们的合约。$ npx sol-compiler*ERC721PayPerMint 的构件不存在**使用 Solidity v0.5.2 编译 1 个合约（ERC721PayPerMint.sol）...**ERC721PayPerMint 构件已保存！*现在应该在构件文件夹中有一个 ERC721PayPerMint.json 文件。让我们添加一个简短的脚本 scripts/deploy.js，用于检索编译后的字节码并将合约部署到本地网络，使用我们在本章前面编写的部署代码的修改版本（见清单 5-22）。我们还将部署地址存储在 Deploys.json 文件中，然后从应用程序中检索出来。// scripts/deploy.jsconst Web3 = require('web3');const fs = require('fs');const path = require('path');// 从默认帐户部署任何构件 async function deploy(artifact, arguments, opts) {  const providerUrl = process.env.PROVIDER_URL                      || 'http://localhost:8545';  const web3 = new Web3(providerUrl);  const from = (await web3.eth.getAccounts())[0];  const data = artifact.compilerOutput.evm.bytecode.object;  const abi = artifact.compilerOutput.abi;  const Contract = new web3.eth.Contract(abi, null, { data });  const gasPrice = 1e9;  const instance = await Contract.deploy({ arguments })                         .send({ from, gasPrice, ...opts });  const address = instance.options.address;  const network = await web3.eth.net.getId();  save(network, address);  console.log(address);}// 将部署地址保存到 Deploys.json 文件中 function save(network, address) {  const file = path.join(    __dirname, '..', 'artifacts', 'Deploys.json'  );  const deployments = fs.existsSync(file)    ? JSON.parse(fs.readFileSync(file)) : {};  deployments[network] = address;  const content = JSON.stringify(deployments, null, 2);  fs.writeFileSync(file, content);}// 部署我们的 ERC721PayPerMint 合约 function main() {  const artifactPath = '../artifacts/ERC721PayPerMint.json';  const artifact = require(artifactPath);  return deploy(artifact, [], { gas: 5e6, gasPrice: 1e9 });}main();清单 5-22

脚本用于将 ERC721PayPerMint 合约部署到 PROVIDER_URL 环境变量指定的网络，并将部署地址索引化为网络 ID。注意，主函数可以修改以轻松部署其他合约

现在，使用 ganache-cli 进程（或 Geth 或 Parity 开发节点）监听 8545 端口，尝试运行部署脚本。node scripts/deploy.js 然后，您应该在 artifacts 文件夹中看到一个 Deploys.json 文件，其中包含网络 ID 和部署地址。请注意，您获得的 ID 和部署地址可能会有所不同。$  cat artifacts/Deploys.json{  "155164184873": "0x0E696947A06550DEf604e82C26fd9E493e576337"}

现在我们已经在本地网络上设置好了我们的合约，我们可以开始处理 Web 应用程序本身了。

### 应用程序

我们的应用程序将遵循与之前相似的结构。我们将有单独的文件夹用于与以太坊网络交互，用于管理合约构件，以及用于 React 组件的文件夹。

#### 初始化 Web3 实例

我们将设置一个 src/eth/network.js 文件（见列表 5-23），其中包含从注入的提供程序实例化新的 web3 对象所需的代码，以及一些稍后在整个应用程序中将要使用的方法。// src/eth/network.jsimport Web3 from 'web3';let web3;export function getWeb3() {  if (!web3) {    web3 = new Web3(Web3.givenProvider);  }  return web3;}export function hasProvider() {  return !!Web3.givenProvider;}export async function getAccount() {  const accounts = await window.ethereum.enable();  return accounts[0];}export async function getBlockNumber() {  return web3.eth.getBlockNumber();}export async function getNetwork() {  return web3.eth.net.getId();}列表 5-23

通过注入的提供程序初始化一个新的 web3 对象的网络文件

请注意，getAccount 方法特别重要，因为它包含调用 *enable* 提供程序的调用。这是允许我们访问用户帐户列表的关键。

#### 创建合约对象

现在我们将创建一个名为 src/contracts/ERC721.js 的文件，该文件将初始化 web3 合约对象，并从 Deploys.json 文件中加载部署地址。

但是，该文件位于我们项目根目录下的 artifacts 文件夹中，而不是 src 文件夹内。不幸的是，create-react-app 模板阻止我们从 src 文件夹外导入任何内容。如果我们试图从我们的 react 应用程序中导入它，我们将收到以下错误消息。您尝试导入 ../../artifacts/Deploys.json，它位于项目 src/ 目录之外。不支持 src/ 之外的相对导入。最简单的解决方法是在 src 文件夹内创建到 artifacts 文件夹的符号链接。我们可以使用以下命令来执行此操作。

返回表示当前网络中 ERC721PayPerMint 已部署实例的 web3 合约

#### 根应用组件

我们的根应用组件（见 5-25）将类似于上一章节的内容。该组件将负责加载默认账户和合约实例，并将其注入到将在 src/components/ERC721.js 中定义的主要 ERC721 组件中。// src/App.jsimport React, { Component } from 'react';import { getDeployed } from './contracts/ERC721';import { hasProvider, getAccount } from './eth/network';import ERC721 from './components/ERC721';class App extends Component {  async componentDidMount() {    if (hasProvider()) {      const contract = await getDeployed();      const sender = await getAccount();      this.setState({ contract, sender });    }  }  render() {    const { contract, sender } = this.state;    return (      <div className="App">        { (hasProvider() && contract && sender)          ? <ERC721 contract={contract} owner={sender} />          : <div>请启用 Metamask 并重新加载</div>        }      </div>    );  }}Listing 5-25

根应用组件的主要方法

请记住，如果用户在 Metamask 中更改了当前账户，我们需要刷新显示的信息，因为我们将列出用户的代币。我们可以通过在以太坊对象上安装监听器来检测帐户更改，并通过将发送者作为 React 键^(11)（见 5-26）来强制重新加载 ERC721 组件。// src/App.jsclass App extends Component {  async componentDidMount() {    // ...    window.ethereum.on('accountsChanged', async (accounts)=>{      this.setState({ sender: accounts[0] });    });  }  render() {    // ...    <ERC721 contract={contract} owner={sender} **key={sender}** />    // ...  }}Listing 5-26

自 5-25 列表中的更新方法，用于监视帐户更改。当帐户更改时，整个 ERC721 组件将自动重新加载。

### 主要 ERC721 组件

该组件将包含我们应用程序中的大部分逻辑：它将列出用户的代币，并允许用户通过一个简单的*Create*按钮铸造新的代币。让我们从页面加载时开始列出现有的代币。

#### 列出现有的代币

枚举用户的非同质代币可能有些棘手。ERC721 标准公开了两个函数来实现这一点：balanceOf 和 tokenOfOwnerByIndex。前者返回用户的代币数量，后者返回给定索引（在零和用户余额之间）的代币 ID。为了避免这两种方法不同步，重要的是在运行所有查询时指定单个块编号。// src/components/ERC721.jsclass ERC721 extends Component {  async getTokensAtBlock(blockNumber) {    const { contract, owner } = this.props;    // 加载用户的代币数量    const strBalance = await contract.methods.balanceOf(owner)                         .call({}, blockNumber);    const balance = parseInt(strBalance);    // 检索每个代币的 ID    const queries = Array.from({length: balance}, (_,index)=>(      contract.methods.tokenOfOwnerByIndex(owner,index)        .call({}, blockNumber)    ));    return await Promise.all(queries);  }}给定上述函数，我们现在可以在组件的*didMount*生命周期事件中将代币加载到组件的状态中（见 5-27 列表）。async componentDidMount() {  const currentBlock = await getBlockNumber();  const tokenIds = await this.getTokensAtBlock(currentBlock);  const tokens = tokenIds.map(id => ({id, confirmed: true}));  this.setState({ tokens, loading: false });}列表 5-27

将用户代币加载到状态中。请注意，我们正在为这些代币添加一个 confirmed 标志，以区分它们和稍后我们将添加的新铸造的代币

我们还将在构造函数中将组件的状态初始化为以下默认值，以便组件在用户的令牌加载完成之前处于加载状态。构造函数(props) {  super(props);  this.state = {    tokens: [],    loading: true  };}让我们用一个简单的渲染方法来测试这个，这个方法只会通过展示它们的 ID 来渲染令牌列表，并且同时将它们作为 React keys 进行复用。render() {  const { tokens, loading } = this.state;  if (loading) return "加载中";  return (    <div>      <h1>收藏品编号</h1>      <div>        { tokens.map(token => (          <div key={token.id.toString()}>            { token.id.toString() }          </div>        ))}      </div>    </div>  );}

如果你在浏览器中检查你的 React 应用程序，你现在应该看到属于当前用户的令牌列表，假设有的话。我们现在可以转向这个应用程序的主要功能：发送交易以铸造新的令牌。

#### 铸造新令牌

我们将首先在我们的 ERC721 组件中创建两个方法：一个用于检查用户是否可以铸造特定的代币，另一个用于实际铸造。用户是否可以铸造代币取决于该 ID 的代币是否已经存在。// src/components/ERC721.jsclass ERC721 extends Component {  // ...  async canMint(id) {    const { contract } = this.props;    const exists = await contract.methods.exists(id).call();    return !exists;  }}铸造将需要实际向合约发送交易，包括要铸造的 ID。正如我们在本章中所看到的，这需要估算气体，并选择要使用的气体价格。对于后者，我们将定义一个 getGasPrice 辅助函数，它将从 Etherchain 申诉处获取当前价格。// src/eth/gasPrice.jsimport axios from 'axios';import BN from 'bignumber.js';const URL = 'https://www.etherchain.org/api/gasPriceOracle';async function getGasPrice() {  const { data: gasData } = await axios.get(URL);  const bn = new BN(gasData.fast);  return bn.shiftedBy(9).toString(10);}利用这个辅助函数，我们现在可以在 ERC721 组件中定义我们的铸造函数。记住，我们需要发送的值与我们正在尝试创建的 ID 成正比，因此较高的数字实际上会花费更多 ETH 来铸造。// src/components/ERC721.jsimport { getGasPrice } from '../eth/gasPrice';import BN from 'bignumber.js';class ERC721 extends Component {  // ...  async mint(id) {    const { contract, owner } = this.props;    const from = owner;    const value = new BN(id).shiftedBy(12).toString(10);    const gasPrice = await getGasPrice();    const gas = await contract.methods.mint(owner, id)                  .estimateGas({ value, from });    contract.methods.mint(owner, id)      .send({ value, gas, gasPrice, from });  }}我们现在将定义一个带有受控组件表单的新的小型 Mint 组件，使用 canMint 检查创建操作是否可用，并在用户选择创建代币时触发铸造。我们将作为 props 传递 mint 和 canMint 方法。// src/components/Mint.jsimport React, { Component } from 'react';export default class Mint extends Component {  constructor(props) {    super(props);    this.state = { value: "" };    this.handleChange = this.handleChange.bind(this);    this.handleMint = this.handleMint.bind(this);  }  async handleChange(event) {    const value = event.target.value;    this.setState({ value, mintable: false });    if (value && value.length > 0) {      const mintable = await this.props.canMint(value);      if (value === this.state.value) {        this.setState({ mintable });      }    }  }  async handleMint(event) {    event.preventDefault();    this.props.mint(this.state.value);    this.setState({ value: "", mintable: false });  }  render() {    const { value, mintable } = this.state;    return (      <form onSubmit={this.handleMint}>        <input type="numeric" value={value}               onChange={this.handleChange} />        <button disabled={!mintable}>Create</button>      </form>    );  }}我们可以通过在其 render 函数中添加以下标记来将此组件连接到我们的主 ERC721。请注意，这要求在 ERC721 构造函数中绑定两个函数到 this。// src/components/ERC721.jsclass ERC721 extends Component {  constructor(props) {    // ...    this.mint = this.mint.bind(this);    this.canMint = this.canMint.bind(this);  }  render() {    // ...    <Mint canMint={this.canMint} mint={this.mint} />    // ...  }}

试试这个新版本，当你点击铸造组件中的“创建”按钮时，应该会看到 Metamask 对话框。如果你接受，将铸造一个新的代币，但在你重新加载页面之前，它不会被添加到你的列表中。现在让我们来解决这个问题。

#### 对交易事件做出反应

最后一块拼图是让我们的应用程序对发出的交易的生命周期做出反应。每当发送新交易以铸造新代币时，我们将向列表中添加一个新的临时代币，并随着新区块的挖掘增加其确认数。为此，我们将在 ERC721 组件的 mint 方法中为每种情况附加处理程序以侦听交易事件。// src/components/ERC721.jsclass ERC721 extends Component {  async mint(id) {  // ...    contract.methods.mint(owner, id)      .send({ value, gas, gasPrice, from })      .on('transactionHash', () => this.addToken(id))      .on('receipt', () => this.confirmToken(id, 0))      .on('confirmation', (n) => this.confirmToken(id, n))      .on('error', (error) => this.failToken(id, error));  }}其中的每个处理程序将分别向列表中添加一个代币，将其标记为已确认或将其标记为出错。我们假设六次确认对于我们当前的使用情况已经足够了。// src/components/ERC721.jsclass ERC721 extends Component {  addToken(id) {    this.setState(state => ({      ...state,      tokens: [ ...state.tokens, { id }]    }));  }  confirmToken(id, confirmations) {    const confirmed = confirmations >= 6;    this.setState(state => ({      ...state,      tokens: state.tokens.map(token => (        token.id === id ? { id, confirmed } : token      ))    }));  }  failToken(id, error) {    this.setState(state => ({      ...state,      tokens: state.tokens.filter(token => (        token.id !== id      ))    }));  }}现在，我们有了一个 Token 对象列表，其中每个代币由其 ID 和其是否处于挂起、已挖掘或已确认状态来定义。让我们使用这些信息通过一个简单的 Token 可视组件在 src/components/Token.js 中显示每个代币，我们可以使用它来代替仅显示代币 ID。// src/components/Token.jsexport default function({ token }) {  const { id, confirmed } = token;  const pending = typeof(confirmed) === "undefined";  let status;  if (pending) {    status = "Pending";  } else if (!confirmed) {    status = "Awaiting confirmation";  } else {    status = "Confirmed";  }  return (    <div>      <h3>{id.toString()}</h3>      <div>{status}</div>    </div>  );}

在您自己的应用程序中，您可能希望使用其他视觉提示来报告每个令牌的状态，例如颜色代码 – 辅以工具提示来向用户解释确认概念。

#### 现有令牌的确认

在此组件中加载初始令牌列表时，我们假设所有这些令牌都已经 *确认*，也就是说，它们已经在几个区块之前被挖出。然而，情况可能并非如此。您可以通过在发送交易后立即重新加载页面，然后查看等待确认的令牌如何错误地进入确认状态来轻松测试此问题。

处理这些情况的技术有很多种，其中一些我们将在下一章中看到。在这种情况下，我们将采用简单的方法，并且偏向简单而不是效率。

首先，我们不再在页面加载时从当前区块加载所有令牌，而是加载两组令牌：一组来自当前区块，另一组来自六个区块之前。我们将六个区块之前的所有令牌视为已确认，而当前区块的所有新令牌将标记为未确认。让我们更新 ERC721 主组件的 didMount 处理程序（代码清单 5-28）以实现此更改。// src/components/ERC721.jsconst CONFIRMATIONS = 6;class ERC721 extends Component {  async componentDidMount() {    const currentBlock = await getBlockNumber();    const confirmedBlock = currentBlock – CONFIRMATIONS;    const confirmedTokenIds = await this      .getTokensAtBlock(confirmedBlock)      .catch(() => []);    const latestTokenIds = await this      .getTokensAtBlock(currentBlock);    const unconfirmedTokenIds = latestTokenIds      .filter(id => !confirmedTokenIds.includes(id));    const tokens = confirmedTokenIds      .map(id => ({ id, confirmed: true }))      .concat(unconfirmedTokenIds        .map(id => ({ id, confirmed: false })      ));    this.setState({ tokens, loading: false });  }}代码清单 5-28

获取确认和未确认的代币列表，并据此在代币集合上相应地设置确认标志。在查询 confirmedTokenIds 时注意 catch 块，因为如果合同在 confirmedBlock 之前尚未创建，调用将会抛出异常，在这种情况下所有代币应该是未确认的。

这将允许我们在页面加载时正确显示每个代币的状态。但是，任何被列为未确认的代币将保持在该状态，直到进行完整页面重新加载。我们需要在它们达到所需的确认数目后更新它们的状态。

我们将通过订阅新区块并重新检查每个未确认代币*六个区块之前*的所有权来做到这一点。一旦有足够的新区块被挖出，我们将能够将这些新代币转移到确认状态。让我们添加一个新方法（列表 5-29）来在 didMount 处理程序中调用。// src/components/ERC721.jsclass ERC721 extends Component {  subscribeUnconfirmedTokens(unconfirmedIds) {    if (unconfirmedIds.length === 0) return;    const { contract, owner } = this.props;    this.newBlocksSub = getWeb3().eth      .subscribe('newBlockHeaders', (err, { number }) => {      unconfirmedIds.forEach(async (id) => {        const confirmedOwner = await contract.methods          .ownerOf(id).call({}, (number – CONFIRMATIONS))          .catch(() => null);        if (areAddressesEqual(confirmedOwner, owner)) {          this.confirmToken(id, CONFIRMATIONS);          unconfirmedIds = unconfirmedIds.filter(i => id!==i);          if (unconfirmedIds.length === 0) {            this.newBlocksSub.unsubscribe();          }        }      });    });  }}Listing 5-29

订阅新区块，并在当前区块之前的六个区块内重新检查每个代币的所有权。如果一个代币在六个区块之前属于当前用户，我们认为它是确认的。一旦所有待处理的代币都被处理完，我们关闭订阅。

请记住，在本示例中，我们仅跟踪通过铸造创建的新代币，并且用户转移的任何新代币 *转移* 到用户将不会显示，直到重新加载页面。我们还假设用户不转移他们自己的代币。如果您的应用程序需要处理这些情况，则监视 Transfer 事件比仅监视用户从应用程序发送的交易更安全。我们将在下一章中围绕这个概念构建。

### 下一步

应用程序的下一步是转移到更有趣的网络，首先从类似 Rinkeby 的测试网络开始，最终转移到 Mainnet。您可以启动一个连接到这种网络的本地 Geth 或 Parity 节点（使用轻量级同步模式以加快同步过程），并依靠 deploy.js 脚本或使用在线工具如 MyCrypto^(12) 或 Remix 来部署合约。一旦部署完成，所有交互将由 Metamask 管理 - 只需记得切换到正确的网络。

## 摘要

在本章中，我们回顾了如何通过依赖 ganache 或完整的以太坊客户端来建立本地开发环境的过程。然后，我们通过使用原生 solc 编译器或 sol-compiler 包装器来编译和部署合约到网络的过程。我们还回顾了在使用 Metamask 时它的工作原理，用于发送交易和解锁用户帐户。

一旦我们解决了设置环境的细节，我们就深入研究了发送交易的过程，特别关注了 gas 估算和定义 gas 价格。然后，我们回顾了交易的生命周期以及如何访问特定事件，比如它何时被挖掘或确认。我们还简要介绍了发送交易时最常见的一些错误以及替换过程的工作方式。

为了阐述所有这些概念，我们构建了一个小型应用程序，类似于上一章的应用程序，但这次是关于非同质化代币。从用户现有代币列表开始，我们允许用户铸造新代币，并监控此类交易的生命周期。在下一章中，我们将涵盖诸如索引和存储等概念，我们还将学习一些关于处理重新组织和测试的额外技巧，这些技巧也可以应用于这种类型的应用程序。
