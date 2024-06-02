© Elad Elrom 2019Elad Elrom 区块链开发者[`doi.org/10.1007/978-1-4842-4847-8_5`](https://doi.org/10.1007/978-1-4842-4847-8_5)

# 5. 以太坊钱包和智能合约

Elad Elrom^(1 )(1)纽约，纽约，美国

在第一章中，当我介绍比特币、替代币和不同的共识机制时，我介绍了以太坊。具体来说，我涵盖了以太坊的 PoW 共识以及利用以太坊使开发者能够创建自己的智能合约和代币。我提到以太坊代币可以作为以太坊请求评论（ERCs）生成，如 ERC-20、ERC-223 或 ERC-777。在第三章中，你创建了自己的区块链，我介绍了比特币钱包和交易。

在本章中，我将详细扩展讲解以太坊。以太坊允许你编写代码（智能合约）来处理资金，利用区块链技术来克服停机和第三方干预的问题。以太坊平台主要归功于维塔利克·布特林和加文·伍德。根据以太坊网站的定义，以太坊的定义如下：

> “以太坊是一个去中心化的平台，它运行智能合约：应用程序严格按照编程运行，没有任何停机、审查、欺诈或第三方干预的可能性。”
> 
> —Ethereum.org

在前几章中，你能够传递和存储数据，如比特币彩色硬币使用案例中的 OP_RETURN 参数。这很有用，因为你能够生成一个文件的 MD5 散列值并将其存储在比特币网络上。你所存储的 MD5 可以是文件、合同或任何你想要的东西。然而，正如你所看到的，比特币只能存储信息，你无法与数据互动。具体来说，你能够在网络上传递和存储数据，但你无法针对你的文件运行代码，如对你的数据执行操作。以太坊通过允许你利用区块链的力量创建智能合约来解决这一功能缺失。

### 注意

智能合约是用于处理资金的可编程代码。该代码独立运行，无需第三方参与。Solidity 是一种流行的以太坊合约编程语言，可以用来编写智能合约并将代码部署在多个区块链上。

以太坊的核心是以太坊虚拟机（EVM）。EVM 是以太坊中智能合约运行的地方。帮助你理解 EVM 的一个好方法是想成一个分布式全球计算机，智能合约可以在其中执行。

### 注意

以太坊虚拟机（EVM）是一个分布式全球计算机，用于运行任意的、算法的、复杂的代码。简单地说，EVM 由以太坊网络中所有节点组成，这些节点通过单一共识连接，能够接收智能合约的代码，处理它并执行它。EVM 使用 256 位作为基本共识机制；它可以处理 1 TB 的区块，标准区块时间为 15 秒。

去中心化应用开发者编写智能合约，然后借助前端代码在 EVM 上运行代码。见图 5-1。EVM 在所有连接的以太坊节点上并行连接中执行代码。这确保了节点的共识。以太坊区块链的大小可以高达 1 TB，而比特币的区块高度限制在每块 4 MB。此外，比特币创建新区块大约需要 10 分钟，而 EVM 上只需要 15 秒。

尽管让去中心化代码作为单一共识运行是有优势的，但也存在缺点。例如，智能合约的代码在所有节点上运行时比传统计算机更慢、更昂贵。![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig1_HTML.jpg](img/475651_1_En_5_Fig1_HTML.jpg)

图 5-1

以太坊 10,000 英尺视角。图片来源：xbt.net。

要运行一个以太坊矿工，你需要运行一个完整的 EVM 节点。矿工们正在运行一种类似于比特币的工作量证明（PoW）共识机制来验证交易。在挖矿过程中，每个区块会挖出五枚硬币。正如你在第一章中看到的，以太坊矿工通过运行智能合约并获得以太币来获得报酬，这些以太币会转化为所谓的*燃料*。

### 注意

以太坊燃料是以太坊代币的一个部分。以太坊燃料被合同使用，以支付矿工的努力。想象一辆车。它需要汽油来运行，以太坊也是。没有以太坊燃料，你不能执行智能合约。

由于以太坊能够提供构建有趣应用的能力，该平台因其潜力而得到了认可，并被微软、英特尔、亚马逊、摩根大通，甚至政府以一种或另一种方式使用。这使得以太坊变成了一个广泛的选择众多的生态系统，帮助你轻松创建智能合约。你可以从大量的开发工具、与其他工具通信的应用程序、最佳实践、基础设施、测试、安全、监控工具等中进行选择。

选择使用工具可能会让人感到不知所措和困惑，尤其是当许多工具仍处于 alpha、beta 阶段或未完全测试时。然而，请记住，到现在为止，你已经具备了关于区块链技术，包括交易、钱包以及它们是如何工作的良好基础理解。此外，你在第三章中开发的区块链是用 JavaScript 和 Node.js 实现的，这是许多以太坊工具的基础。我建议你收藏以下两个列表：

+   [`github.com/ConsenSys/ethereum-developer-tools-list`](https://github.com/ConsenSys/ethereum-developer-tools-list)

+   [`github.com/ConsenSys/ethereum-developer-tools-list/blob/master/EcosystemResources.md`](https://github.com/ConsenSys/ethereum-developer-tools-list/blob/master/EcosystemResources.md)

这些资源提供了所有与以太坊相关的开发工具和资源的一份详尽列表。鉴于本书的范围，不可能涵盖所有这些不同的工具，但我建议如果你专注于以太坊开发，在一定程度上要回顾这些工具，这样你就可以自行判断哪个工具最适合你的项目。

在本章中，我将重点介绍以太坊智能合约，并在测试网上运行它们，正如你在前一章中为比特币所做的那样。我将展示如何设置你的开发工具和 IDE，并为你提供基本的 dapp 主网部署信息，我将在本书的后续章节中进一步扩展这些内容。

## Ganache 模拟全节点客户端

Ganache（之前称为 ethereumjs-testrpc）允许你在本地机器上运行一个模拟的以太坊全节点客户端，并通过 CLI 与你的合约进行交互。这个工具很有用，因为你将设置一个开发网络和一个私有的测试网网络，以测试你的智能合约代码。

正如你在前一章所看到的那样，设置测试网网络允许你在将代码提交到主网之前，使用虚拟货币测试你的代码。我决定在本章使用 Ganache，因为它属于 Truffle 开发套件的一部分，并且与 Truffle 集成得很好。

### 安装 Ganache

开始使用时，你可以使用 npm 将 Ganache 全局安装，并通过调用帮助命令确认它是否正常工作。> npm install -g ganache-cli> ganache-cli help 如果你遇到安装问题或想了解更多关于该工具的信息，请访问 Ganache 的 GitHub 页面：[`github.com/trufflesuite/ganache-cli`](https://github.com/trufflesuite/ganache-cli)。你还可以通过运行以下命令来检查 CLI 的版本：> ganache-cli -v

这个命令会输出版本信息。在撰写本文时，Ganache CLI 的版本为 v6.4.3（ganache-core: 2.5.5）。

### Ganache CLI：监听端口

您可以在开发和调试合同时在您的机器上运行 Ganache。为此，您需要在终端中设置 Ganache CLI 以监听稍后在本书中设置的 truffle.js 中的端口。> ganache-cli -p 8584 请注意，此时 8584 端口上没有任何运行的东西，所以假设您将设置 8584 端口。命令应输出以下内容：监听 127.0.0.1:8584

## IntelliJ IDEA 的 Solidity 插件

在第三章中，您下载并使用 WebStorm 作为您的 IDE 来开发您的区块链。WebStorm 是 IntelliJ IDEA 的一个子集，并且有一个 Solidity 语言插件，它提供了一种轻松编写您合约的方法。此外，它还提供高亮和代码补全，使开发更加容易。您可以使用之前安装的 WebStorm 版本，只需添加 Solidity 插件。为此，首先在此处下载插件：[`plugins.jetbrains.com/plugin/9475-intellij-solidity`](https://plugins.jetbrains.com/plugin/9475-intellij-solidity) 。

为了安装插件，请按照以下步骤操作：

1.  1.

    选择 WebStorm➤首选项（或按命令+ ,）。

1.  2.

    选择“插件”。

1.  3.

    在“插件”中搜索“*Solidity*”。它会显示“没有找到插件”。有一个链接到“在仓库中搜索”。点击“在仓库中搜索”链接。“Intellij-Solidity”插件将显示。请参阅图 5-2。

1.  4.

    安装“Intellij-Solidity”插件：语言和检查。请参阅图 5-2。

1.  5.点击 IntelliJ-Solidity➤安装。请参阅图 5-2。![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig2_HTML.jpg](img/475651_1_En_5_Fig2_HTML.jpg)

    图 5-2

    在 WebStorm 中安装 IntelliJ-Solidity 和 Solidity Solhint

1.  6.

    在插件中搜索 Solidity Solhint。它会显示“没有找到插件”。有一个链接到“在仓库中搜索”。点击“在仓库中搜索”链接。点击 Solidity Solhint 检查➤然后点击安装。

1.  7.

    重启 WebStorm。

请注意，如果您是 Visual Studio 的粉丝，还有一个 Solidity 扩展适用于 Visual Studio；请参阅[`marketplace.visualstudio.com/items?itemName=ConsenSys.Solidity`](https://marketplace.visualstudio.com/items%253FitemName%253DConsenSys.Solidity)。在撰写本文时，该插件仅适用于 Visual Studio 2015 或更早版本。

请记住，像往常一样，您可以使用您喜欢的 IDE，文本编辑器，甚至 vim 来编写您的代码；没有必要购买 IDE。

## Truffle 套件

您将使用 Truffle，因为它是最受欢迎的工具之一，并且具有集成的库，可以帮助加快开发周期。Truffle 套件包括 Truffle、Ganache 和 Drizzle；请参阅图 5-3。

> “Truffle 是一个开发环境，测试框架和资产管道，用于 Ethereum，旨在使 Ethereum 开发者的生活更加轻松。”
> 
> *—* [`github.com/trufflesuite/truffle`](https://github.com/trufflesuite/truffle)

Truffle 文档包括安装说明，可以在[`truffleframework.com/docs`](https://truffleframework.com/docs)找到！../images/475651_1_En_5_Chapter/475651_1_En_5_Fig3_HTML.jpg

图 5-3

Truffle 套件文档

开始之前，打开一个新的终端窗口并在你的机器上全局安装 Truffle（在撰写本文时，当前的 Truffle 版本是 5.0.14）。然后确保它正确安装，通过运行帮助命令来查看所有可用的命令列表。> npm install -g truffle+ truffle@5.0.14> truffle helpTruffle v5.0.14 - 以太坊开发框架使用：truffle <命令> [选项]

### 创建你的智能合约

开始之前，让我们创建你的文件夹并初始化 Truffle 向导以生成所有开始所需的所有代码。在终端中，输入以下命令：> mkdir MySmartContract && cd $_> truffle init 这些命令创建一个名为 MySmartContract 的文件夹并更改目录位置到新项目；然后 truffle init 命令初始化项目。你可以在图 5-4 中看到输出！../images/475651_1_En_5_Chapter/475651_1_En_5_Fig4_HTML.jpg

图 5-4

创建 MySmartContract 项目和用 truffle init 命令初始化

接下来，打开 WebStorm，通过选择“文件”➤“打开”来打开你创建的项目。导航到 MySmartContract 项目目录，并点击“打开”。WebStorm 将打开该项目，如图 5-5 所示！../images/475651_1_En_5_Chapter/475651_1_En_5_Fig5_HTML.jpg

图 5-5

MySmartContract 在 WebStorm 中打开

EVM 支持许多编程语言，如 Solidity、JavaScript、GO、C++、Python、Java、Ruby、Web Assembly、Rust 和 Haskell。在本节中，你将使用 Solidity，因为它是编写智能合约最流行的以太坊编程语言。Solidity 基于 ECMAScript，并受到 JavaScript、C++和 Python 的影响。Solidity 的一个优势在于你能够将你的智能合约交易部署在除了以太坊之外的其它各种区块链平台上，如以太坊经典、Tendermint、ErisDB 和 Counterparty。

Solidity 使用.sol 文件扩展名；事实上，如果你检查你项目中的合约文件夹，你会找到一个名为 Migrations.sol 的文件，如图 5-5 所示。这个文件是在你初始化 Truffle 向导时自动为你生成的。迁移文件帮助你将合约部署到以太坊网络。随着你的项目进展，你会创建新的迁移文件。

### 将 Truffle 连接到 Ganache 网络

接下来，您将通过调用您的网络开发并设置 URL 和端口来自定义您的环境。如您所回忆，您已经运行了 Ganache，并且已经编程您的网络以监听 127.0.0.1，端口 8584。您将使用这些设置在您的以太坊区块链网络上部署您的合约。

要开始，打开 MySmartContract/truffle-config.js，在 network 对象中添加一个开发对象，并设置这些配置：

+   gas：此参数用于部署时的石墨烯限制。默认值为 4712388。

+   gasPrice：此参数用于部署时的石墨烯价格。默认值为 100000000000（100 Shannon）。

您正在设置默认值，您也可以通过省略 gas 和 gasPrice 标签来实现；然而，对于 live 主网络，在撰写本文时，我建议设置一个 21,000 的石墨烯价格，这是一个合理的值。查看 ETH Gas Station（[`ethgasstation.info/`](https://ethgasstation.info/)）以确定石墨烯价格值应该是多少，如图 5-6 所示。

图 5-6

Ethgasstation.info 计算推荐的石墨烯价格

正如你所见，在撰写本文时，支付 1 美元的法定货币可以提供标准的 5.6 次交易时间。

你只设置了一个开发环境；然而，当你将你的代码从开发转移到公共测试网络，然后是生产环境时，你可以在 truffle-config.js 文件中添加更多环境。

### “你好，世界”智能合约

如前所述，智能合约是 Ethereum 区块链上的账户对象；你可以编写函数与其他合约互动、发送代币、做出决策和存储数据。总的来说，合约是为了去中心化而构建的；然而，要记住它们可以被编程为具有受监管的选项，使它们变得中心化。例如，以太坊 Gemini 美元有一个冻结交易或甚至撤销交易的选项，其他代币可以由所有者构建具有自毁功能的。

你将从一个简单的“你好，世界”合约开始。这是最少的代码，这里的目的是不是创建任何有用的东西，而是帮助你理解如何创建一个智能合约。

在终端中，在项目位置，使用 truffle 命令创建一个新的合约，并将其命名为 HelloWorldContract。

如果 CLI 正确无误地工作，则不输出任何内容。

然后，打开您创建的合约；它将出现在 contracts/HelloWorldContract.sol 下。正如您所看到的，Truffle 向导已经为您创建了您的合约。

这个第一个智能合约是一个最小化的工作示例；它只是保存一个消息，并通过调用您的 main 函数允许您检索消息。用下面的代码替换 contracts/HelloWorldContract.sol 中的现有代码；pragma solidity ⁰.5.0;contract HelloWorldContract {  string greeting;  constructor() public {    greeting = 'Hello World';  }  function greet() public view returns (string memory) {    return greeting;  }}

正如您所看到的，Solidity 脚本与 JavaScript 或 C++相似，且易于阅读。代码的第一行是 Solidity 编译器版本；您将使用 0.5.0。在 HelloWorldContract 构造函数中，您将 greeting 变量设置为'Hello World'。主要函数是 greet()。一旦您调用主要函数，您就可以检索 greeting 变量的值。

### “MD5 智能合约”智能合约

接下来，您将创建一个更实用的第二个合约。这个合约将允许您存储前一章中存储的 MD5 散列值，但这次您将能够与之交互，而不仅仅是将 MD5 数据存储在区块链上。

在终端中，在项目级别，使用命令 truffle 创建一个名为 MD5SmartContract 的新合约。truffle create contract MD5SmartContract 接下来，打开您创建的名为 contracts/RegisterContract.sol 的合约。您将运行以下合约：pragma solidity ⁰.5.0;contract MD5SmartContract {  bytes32 public signature;  event signEvent(bytes32 signature);  constructor() public {  }  function sign(string memory document) public {    signature = sha256(bytes(document));    emit signEvent(signature);  }}

代码创建了一个名为 signature 的变量。然后您的 main 函数签署您的文档。您传递文档的 MD5，并使用 SHA256 签署文档。您创建了一个事件，一旦签署文档就会被调度。

### 注意

安全散列算法（SHA）是众多加密散列函数中的一个。加密散列函数作为文本或数据的签名；它是单向的，无法被解密。生成的 SHA256 散列值是一个固定大小的，256 位（32 字节），几乎唯一。

### 为您的智能合约部署创建 Truffle 迁移文件

如前所述，Truffle 迁移文件帮助您在以太坊网络上部署您的合约。您将为您部署创建一个迁移文件。为此，创建一个新的部署文件，命名为 2_deploy_contracts.js，并将文件放在这里：migrations/2_deploy_contracts.js。您可以像这样指向您创建的智能合约代码：const HelloWorldContract = artifacts.require("HelloWorldContract.sol");module.exports = function(deployer) {    deployer.deploy(HelloWorldContract);};创建另一个名为 3_deploy_contracts.js 的部署文件，并将文件放在这里：migrations/3_deploy_contracts.js。const MD5SmartContract = artifacts.require("MD5SmartContract.sol");module.exports = function(deployer) {    deployer.deploy(MD5SmartContract);};至此，您的项目包括了两个智能合约和迁移文件。您可以比较您的项目目录和文件与我的一致；如图 5-7 所示。![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig7_HTML.jpg](img/475651_1_En_5_Fig7_HTML.jpg)

图 5-7

包含两个智能合约和迁移文件的 MySmartContract

对于更懒惰的开发人员，另一种技巧是使用 Truffle 创建向导来生成迁移文件。> truffle create migration deploy_my_contract

这个命令会自动为你生成迁移文件。

### 使用 Truffle 编译智能合约

在另一个终端窗口中，您将运行 Truffle 来编译您的智能合约。编译命令将您的 Solidity 代码转换为字节码，该字节码可以被 EVM 解释。现在，Ganache 模拟 EVM。> truffle compile 您可以在以下 JSON 文件中看到您合约的字节码：build/contracts/HelloWorldContract.json 和 build/contracts/MD5SmartContract.json。请在此查找所示的字节码标签："bytecode": "0x608060405234801561001057600080fd5b5061031..."

### 注意

请记住，理想情况下你应该在再次编译之前手动删除合约的 contracts/*.json 文件。这将确保最新的代码被编译，因为 CLI 不总是立即识别更改。

### 将智能合约部署到您的开发网络

现在你已经从你的智能合约中编译出了字节码，你可以将字节码迁移到你的开发环境中，这样你就可以运行迁移命令来切换到 truffle.js 文件中设置的网络。> truffle migrate --network development 运行这个命令将返回如图 5-8 所示的响应。这表明三个迁移文件已成功在网络上部署。每个合约都有一个成功的部署。![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig8_HTML.jpg](img/475651_1_En_5_Fig8_HTML.jpg)

图 5-8

Truffle migrate 命令响应

请记住，--reset 标志在您更改代码时很有用，因为您需要重新编译和部署。> truffle migrate --reset

### Truffle 控制台

既然你的合约已经部署到了你的开发网络，你就可以通过 Truffle CLI 与你的智能合约互动了。为此，你可以打开一个控制台并连接到你的开发网络。> truffle console --network development 一旦你运行了控制台命令，你的终端显示你处于

要退出 CLI 模式，点击 Control+C 两次或者在控制台里输入.exit。

### 通过 Truffle CLI 与你的智能合约互动

为你的智能合约设置了两个变量 hello 和 sign，这样你就可以与它们互动了。truffle(development)> HelloWorldContract.deployed().then(_app => { hello = _app })undefinedtruffle(development)> MD5SmartContract.deployed().then(_app => { doc = _app })undefined 要与你的 HelloWorldContract 合约互动，你可以调用你创建的主要公共函数，因为你暴露了函数 greet。truffle(development)> hello.greet()'Hello World'同样，你可以与 MD5SmartContract.sol 合约互动。你将传递在第三章中生成的相同的 MD5 散列值（634ef85e038cea45bd20900fc97e09dc），并调用你的主函数 sign。那个函数将生成一个 SHA256 散列值，如图 5-9 所示。truffle(development)> doc.sign('634ef85e038cea45bd20900fc97e09dc')![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig9_HTML.jpg](img/475651_1_En_5_Fig9_HTML.jpg)

图 5-9

创建 doc.sign 交易

现在你可以通过调用签名函数来确认你有一个 SHA256 散列值；查看输出在图 5-10。truffle(development)> doc.signature()'0x7869cd540ff8c3b2635ec87251f361e21ad3c72fbc2f79897b9816bec54b0a48'![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig10_HTML.jpg](img/475651_1_En_5_Fig10_HTML.jpg)

图 5-10

与 MD5SmartContract 智能合约互动以生成签名

你可以从这里下载整个智能合约项目：[`github.com/Apress/the-blockchain-developer/chapter5/step1/`](https://github.com/Apress/the-blockchain-developer/chapter5/step1/)。

## 使用 Remix 编译

到目前为止，你已经使用了 Truffle 工具、Ganache 网络和 WebStorm IDE 来创建、编译、部署和与你的合约互动；然而，还有一种更简单的方法。Remix 提供了一个在线 IDE，可以做到和 WebStorm 和 Truffle 一样的事情。

要查看这个工作原理，请访问 Remix 网站：[`remix.ethereum.org`](https://remix.ethereum.org)。

粘贴你的示例中的“你好，世界”智能合约代码。确保右侧面板设置为正确的编译器；你将使用“当前版本：0.4.22。”然后点击“开始编译（Ctrl-S）。”见图 5-11。![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig11_HTML.jpg](img/475651_1_En_5_Fig11_HTML.jpg)

图 5-11

“你好，世界”智能合约

在你的项目中创建一个新文件夹，命名为 remix；然后在该文件夹中创建一个名为 HelloWorldContract.js 的文件。在 Remix Online IDE 中点击“详情”按钮，将 WEB3DEPLOY 内容复制并粘贴到你创建的 HelloWorldRemix.js 文件中，如图 5-12 所示！../images/475651_1_En_5_Chapter/475651_1_En_5_Fig12_HTML.jpg

图 5-12

智能合约“Hello, World”的 WEB3DEPLOY 代码

### 注意

web3.js 是一个以太坊 JavaScript API；其库允许你通过 HTTP 或 IPC 连接与以太坊节点进行交互。WEB3DEPLOY 代码可以部署在本地或远程节点上。

## 私有以太坊区块链的 Geth 搭建

你已经在你本地机器上与你的智能合约进行了交互。接下来，建议运行一个完整的节点，并在测试网区块链上测试你的智能合约；这可以在一个更真实的环境中测试它。Geth 提供了一个用 Go 实现的完整的以太坊节点，你可以在本地运行。这个私有测试网将允许你在与真实以太坊区块链隔离的环境中开发和测试你当前的智能合约。

首先，使用 Brew 安装 Geth。> brew tap ethereum/ethereum> brew install ethereum 为确保安装成功，运行当前 Geth 版本（我写这篇文章时使用的是 1.8.27 版本）的--version 命令。> geth versionVersion: 1.8.27-stable

### 初始化 Geth 私有区块链

现在你已经安装了 Geth，接下来将创建你的第一个区块，即区块 0，也称为*创世区块*。在项目根目录下创建一个名为 genesis_block.json 的文件。现在只需粘贴提供的 JSON 即可，但请注意，你可以使用此处提供的 Python 脚本生成自定义的创世区块：[`blog.ethereum.org/2015/07/27/final-steps/`](https://blog.ethereum.org/2015/07/27/final-steps/)。

在本书的范围内，您将使用此脚本并将难度设置为 1000，将燃料限制设置为 1000000，以便轻松挖矿和低燃料费用；然而，在您自己的实验中，可以根据需要进行调整。请参阅 genesis_block.json。{  "config": {  "chainId": 1,  "homesteadBlock": 0,  "eip155Block": 0,  "eip158Block": 0},  "difficulty": "0x1000",  "gasLimit": "0x1000000",    "alloc": {      "0x44dc998cbc1c7504bec0a96af4a9aef6606a768a":      {"balance": "0x1337000000000000000000"}    }}接下来，您将创建您的私有测试网。在终端中，运行此命令：> geth --identity "MyTestNet" --nodiscover --networkid 1999 --datadir testnet-blockchain init genesis_block.json 您需要为您的测试网区块链创建一个账户；使用账户命令。选择一个简单的密码，因为您正在运行一个本地测试网络，但在主网上，您需要关注安全性；在这里，我选择密码 123。> geth account new --datadir testnet-blockchain 密码：123 重复密码：123 地址：{ a8eceb3e2dd7af9c6fdb12edd8a7e84290932c2d}正如您所看到的，在选择密码后，您收到了一个钱包地址。您可以将自己的输出与我显示的进行比较，如图 5-13 所示。![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig13_HTML.jpg](img/475651_1_En_5_Fig13_HTML.jpg)

图 5-13

使用 Geth 创建私有测试网和钱包

### Geth 控制台

现在您已经设置了账户和测试网区块链，您可以打开一个 Geth 控制台与区块链互动。> geth --identity "MyTestNet" --datadir testnet-blockchain --nodiscover --networkid 1999 console 2>> geth.log

请注意，我使用了 2>> geth.log 参数将日志输出到自定义文件位置。一旦 Geth 控制台启动，您可以运行 eth.syncing 命令来检查当前正在同步的区块。在这种情况下，它将返回 false，因为没有要同步的内容；您正在本地网络上从区块 0 开始。

您将收到一个弹出警告，询问以下内容：

> “您想要应用程序“geth”接受传入的网络连接吗？点击拒绝可能会限制应用程序的行为。此设置可以在“安全与隐私”首选项的防火墙面板中更改。”请选择“允许”。

接下来，在 Geth 终端中运行同步命令。geth> eth.syncingfalse 如果您运行 eth.blockNumber 命令，它将返回 0，因为您还没有挖出任何区块。geth> eth.blockNumber0

### 为您的私有测试网挖以太坊

然后，你可以使用 getBalance 命令确认你的账户里是否有余额。`geth> eth.getBalance(eth.accounts[0])` `0` 使用`eth.accounts`命令，你将得到你创建的新账户。`geth> eth.accounts["0xa2a6d8fe7e39645613e74fe19c79071ee52009ba"]` 你可以在你创建的私有以太坊链上生成或挖出以太币。无论如何，你需要知道如何挖矿，因为你测试代码时需要交易被包含在挖出的区块中。要开始挖矿，只需运行`miner.start`命令。`geth> miner.start()` `null` 同样地，要停止挖矿，只需运行`miner.stop`命令。`> miner.stop()` `null` 如果你让挖矿运行，你将挖出一些区块，所以当你检查区块号码时，你将现在也看到结果以及资金。`geth> eth.blockNumber` `1672` `geth> eth.getBalance(eth.accounts[0])` `8.36e+21`

### 将 Remix 部署到 Geth

既然你的节点已经同步，你也知道如何挖矿，接下来你可以将你的智能合约部署到测试网上了。首先，你需要解锁你的主 Geth 账户以便使用。确保你的账户里有一定的余额，否则你将无法在网络上部署你的合约。在 Geth 上，使用你的密码解锁你的账户以便 Geth 可以调用它。`geth> personal.unlockAccount(eth.accounts[0], "123", 24∗3600)` `true` 我使用了密码 123，但如果你使用了不同的密码，你需要将其改为你的密码。接下来，加载你在 Remix 上生成的 web3.js 脚本。`> loadScript("remix/HelloWorldContract.js")` `null [object Object]` `true` 挖出下一个区块并包含这个合约需要几秒钟；一旦挖出，你将收到以下消息：`Contract mined! address: 0x9905f1663f1b808d52dca42ce26e0d2648f8be07 transactionHash: 0x66b80787eb3eae16c9535a1bd86ff1a623c1914ac9ffc2addde74655aed09157` 如果你没有看到这条消息，确保你在挖矿。`geth> miner.start()` 合约一旦挖出，你将在终端中收到以下消息，其中包括地址和交易哈希：`Contract mined! address: 0xe49da16551c5c5735de46e07e8ab9e713310a13b transactionHash: 0x36d3ec593f63280ca6aae1b079bfb6f00eea719468e04960643c23f39cbef5b3`

### 将 Truffle 部署到 Geth

同样地，通过 Truffle 部署 web3.js 合约的脚本，你需要运行 migrate --reset 命令。`--reset`标志告诉 Truffle 从头开始运行所有迁移。确保在运行 migrate 命令之前使用`.exit`退出 Truffle 控制台。Truffle 将自动编译你的合约。`truffle(development)> .exit` `> truffle migrate --reset` `Using network 'development'.Network up to date.` `Now you can open a development console again.` `> truffle console --network development` `truffle(development)> HelloWorldContract.deployed().then(_app => { hello = _app })` `undefined` `truffle(development)> hello.greet()` `'Hello World'`

合约已重新部署，你可以再次与你的合约互动。你可以从这里下载这一步：[`github.com/Apress/the-blockchain-developer/chapter5/step2/`](https://github.com/Apress/the-blockchain-developer/chapter5/step2/)。

### Geth 中实用的命令

你可以通过按下 Command+C 来停止 Geth 进程，然后退出，或者你可以通过 aux 来检查是否有任何进程打开。或者你可以使用 killall 命令来停止进程。> ps aux | grep geth> killall -HUP geth 在任何时候，你可以运行帮助标志来获取命令列表。> geth –help 要获取待处理的交易列表，请运行以下命令：> geth --identity "MyTestNet" --datadir testnet-blockchain --nodiscover --networkid 1999 console 2>> geth.loggeth> eth.pendingTransactions 要删除公共测试网上的本地同步区块链数据，使用这个命令：geth> geth removedb 要删除你的私有区块链测试网数据，使用这个命令：geth> geth removedb --datadir test-net-blockchain 为了更快地同步区块链，使用  --fast 标志来执行快速以太坊同步。请注意，使用这个命令你将无法保留过去的交易数据。缓存标志设置了缓存限制。geth> geth --fast --cache=1024

## 将 Mist Ethereum 钱包连接到你的私有网络

拥有一个可以连接到你的私有网络的钱包会很有用。那就是 Mist 的作用所在。你可以将你的私有区块链连接到 Mist 并进行交易，就像人们正在使用你的合约一样进行真实的交易。

开始使用，从这里下载 Mist：[`github.com/ethereum/mist/releases`](https://github.com/ethereum/mist/releases)。

对于 Mac，在撰写本文时，要下载的文件名为 Mist-macosx-0-11-1.dmg。请注意，你也可以通过从同一个网址下载以太坊钱包来实现相同的结果。

接下来，你将启动 Mist 并将其连接到你的测试网区块链。在命令行中，指向 Mist 的位置和 geth.ipc 数据库。> /Applications/Mist.app/Contents/MacOS/Mist --rpc /[项目位置]/MySmartContract/testnet-blockchain/geth.ipcMist 打开并显示你的活动账户和余额，如图 5-14 所示。![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig14_HTML.jpg](img/475651_1_En_5_Fig14_HTML.jpg)

图 5-14

Mist 活动账户和余额

### 与你的智能合约互动的其他人

一旦合约发布，任何人都可以使用地址和应用程序二进制接口（ABI）来连接和与合约互动。你可以在将合约发布到主网之前，像一个实际的人一样启动并与你合约互动。

Mist 是一个可以用于测试的桌面应用。要关注一个合约，在 Mist 中，点击右上角的“合约”链接，然后点击“关注合约”，如图 5-15 所示。![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig15_HTML.jpg](img/475651_1_En_5_Fig15_HTML.jpg)

图 5-15

Mist 的“关注合约”按钮

要让其他人运行你的合约，他们需要两样东西。

+   合约地址

+   应用二进制接口

### 注意

ABI 描述了合约的函数。这个描述是知道如何调用函数所必需的。把它想象成一本用户手册。

你可以像这样检索合约地址：truffle(development)>var hello = HelloWorldContract.deployed().then(_app => { hello = _app })truffle(development)>hello.address'0x0b4f69f88390bc8cec93e730128a5e5c5dffd56c'同样，你可以用这个命令检索合约的 ABI：truffle(development)>JSON.stringify(hello.abi)'[{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor","signature" '[{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor","signature":"constructor"},{"constant":true,"inputs":[],"name":"greet","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"view","type":"function","signature":"0xcfae3217"}]'然后在 Mist 中传递合约地址和 ABI，如图 5-16 所示。![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig16_HTML.jpg](img/475651_1_En_5_Fig16_HTML.jpg)

图 5-16

在 Mist 中传递信息

请注意，你在将 ABI 和地址粘贴到 Mist 中时省略了单引号。

现在点击确定，你就可以在你的关注合约列表中看到你的合约了。见图 5-17。![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig17_HTML.jpg](img/475651_1_En_5_Fig17_HTML.jpg)

图 5-17

Mist 的关注合约

你在 Mist 中有了你的合约，并且可以与之互动，发送资金，监听事件，以及调用函数，就像用户将会在主网上与你合约互动一样。

## MetaMask

类似于 Mist，另一种无需下载桌面应用就能与你的合约互动的方式是通过一个名为 MetaMask 的浏览器插件。就像 Mist 一样，你可以使用 MetaMask 将你的合约连接到主网、公共测试网和本地区块链（例如你用 Ganache 创建的那个），或者你甚至可以连接到 Truffle Develop。开始之前，为 Chrome 或 Firefox 下载 MetaMask 插件。

+   [Chrome 网上应用店](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn) 。点击“添加到 Chrome”按钮。见图 5-18。

+   [Firefox 附加组件页面](https://addons.mozilla.org/en-US/firefox/addon/ether-metamask) 。点击“添加到 Firefox”按钮。

![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig18_HTML.jpg](img/475651_1_En_5_Fig18_HTML.jpg)

图 5-18

MetaMask beta Chrome 插件

点击 MetaMask 图标，然后点击继续按钮。接下来，选择一个密码，接受条款，保存你的秘密备份短语，并创建你的账户。

现在账户已经创建，你在顶部的下拉菜单中有选项选择连接到哪个网络，如图 5-19 所示。![../images/475651_1_En_5_Chapter/475651_1_En_5_Fig19_HTML.jpg](img/475651_1_En_5_Fig19_HTML.jpg)

图 5-19

MetaMask beta Chrome 网络下拉菜单

正如你可能回忆的，你编程了 truffle.js 的值来在 localhost 端口 8584 上设置一个网络，这与默认网络匹配；然而，你可以设置一个自定义 RPC 或连接到测试网络或主网络。

有关将 Truffle 与 MetaMask 连接的更多信息，请访问 Truffle 框架文档；

[`truffleframework.com/docs/truffle/getting-started/truffle-with-metamask`](https://truffleframework.com/docs/truffle/getting-started/truffle-with-metamask)

## 公共测试网络

现在你能够在开发网络上运行你的智能合约，你可以在主网上线之前再迈出一小步。你可以将你的合约在公共测试网络上运行。

### 区块同步

有三个著名的测试网络：Ropsten、Kovan 和 Rinkeby。你可以让 Geth 通过--testnet 标志连接到测试网络，这将连接到公共测试网络（Ropsten）。> geth --testnet --syncmode "fast" --cache=512 console

和之前一样，需要 rpc 标志来接受 Geth RPC 连接，让 Truffle 能够连接到 Geth。你还把它设置为快速同步并将缓存大小限制为 512\. 这个命令包括启动 Geth 控制台。

要检查同步命令的状态，使用这个：geth> eth.syncing{    currentBlock: 1011878,    highestBlock: 3569550,    knownStates: 2058862,    pulledStates: 2056745,    startingBlock: 968873}

完成后，同步命令将返回 false。记住，在撰写本文时，有数百万个状态条目和 3,569,550 个区块，这可能需要数小时，具体取决于你的连接速度。currentBlock 值是正在检索的当前区块，总区块数（最高区块）。这可以让你知道下载需要多长时间。

正如你所回忆的，你可以在 Geth 控制台中运行 eth.blockNumber 命令来查看当前正在同步的区块号码，以及检查你的账户余额是否已经更新。> eth.blockNumber> eth.getBalance(eth.accounts[0])

### 公共测试网络水龙头

除了测试网货币外，你还可以通过水龙头获得额外的测试网货币，正如你用比特币所做的那样。访问[`faucet.ropsten.be/`](https://faucet.ropsten.be/)，如图 5-20 所示，请求将硬币发送到你设置在 Mist 中的钱包地址！../images/475651_1_En_5_Chapter/475651_1_En_5_Fig20_HTML.jpg

图 5-20

Ropsten 以太坊水龙头

## 以太坊主网

从 Ganache 控制台，你能够发布到一个公共测试网网络（Ropsten）。下一步是发布到以太坊主网。为此，你需要重新启动 Geth，这次连接到主网。> geth --fast --cache=512 就像公共测试网一样，你得等待 Geth 同步完成。一旦同步完成，你可以调用 Truffle migrate 命令来部署，和之前一样，你需要你的账户有以太币硬币。> truffle migrate --reset

## 推荐用于智能合约的工具

在本章中，我介绍了 Ganache、Solidity、IntelliJ、Truffle、Geth、Remix 和 MetaMask；然而，还有其他值得提及的工具。

+   *Solium*：Solidity 代码清理解决方案

+   *conteract.io*：与智能合约互动

+   *Populus*：适用于以太坊智能合约的开发框架

+   *Parity*：轻量级以太坊节点

+   *Drizzle*：前端 dapp 解决方案

## 总结

在本章中，我介绍了如何使用 Ganache 来模拟一个完整的以太坊客户端。你安装了 Ganache，一旦你能够连接到 Ganache CLI，你就可以创建一个网络并监听一个端口。你学会了如何使用 IntelliJ IDEA 插件 for Solidity 以轻松地开发带有自动补全和高亮功能的智能合约。你还了解了 Truffle 套件以及如何使用命令行向导创建自己的智能合约。你把 Truffle 连接到 Ganache 网络，然后创建了一个“Hello, World”智能合约以及一个“MD5SmartContract”智能合约。

一旦你创建了你的合约，你就可以使用 Truffle 部署过程将你的智能合约迁移。你使用 Truffle 编译并部署你的智能合约代码到你的开发网络。然后，你使用 Truffle 控制台通过 Truffle CLI 与你的智能合约互动。接下来，你使用 Geth 创建了一个私有的以太坊区块链并初始化了这个区块链。你使用 Geth 控制台并在你的 Geth 私有测试网上挖出了假以太坊。

接下来，你把你用 Remix web3.js 部署到你自己创建的 Geth 私有测试网，以及部署你的 Truffle 合约。此外，你看了一些在开发智能合约时会有帮助的 Geth 命令。你把你用的 Mist 以太坊钱包连接到你创建的私有 Geth 网络，并能够与你的智能合约互动。你能够在你浏览器的 MetaMask 中使用 MetaMask 作为桌面客户端的替代品。

一旦你能够看到你的合约在运行，你就设置了一个公共测试网络，并同步区块以及通过水龙头获取硬币。最后，你学会了如何将你的代码迁移到以太坊主网。

在接下来的章节中，你将学习如何为智能合约构建前端代码并发布一个完整的去中心化应用（dapp）。
