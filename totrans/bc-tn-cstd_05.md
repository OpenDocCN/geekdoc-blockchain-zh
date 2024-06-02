©作者，受独家授权于 APress Media, LLC，是 Springer Nature 的一部分 2023B. Wu，B. Wu 青少年区块链[`doi.org/10.1007/978-1-4842-8808-5_5`](https://doi.org/10.1007/978-1-4842-8808-5_5)

# 5. 智能合约与 Dapps：从理论到实践

布莱恩·吴（Brian Wu）和布里吉特·吴（Bridget Wu）(1)美国新泽西州 Livingston

计算机科学家布莱恩·卡恩（Brian Kernighan）在 1972 年为贝尔实验室内部使用的 B 语言编写了第一个“Hello, World!”程序。布莱恩编写了一本名为《B 语言入门教程》的手册，以展示如何使用 B 语言。从那时起，这本受欢迎的文本迅速传播开来。1974 年，它在贝尔实验室的一份备忘录中使用，1978 年出现在《C 编程语言》一书中。“Hello, World!”至今仍然很受欢迎。它成为了新手程序员的第一程序的标准。这段特定的代码证明了你的代码语法、编译和执行能够一致地产生期望的输出。“Hello, World!”提供了超过 60 种编程语言的版本。

在上一章中，我们从理论上解释了以太坊网络，包括以太坊的关键组成部分、EVM、架构等。更好地理解我们已经学到的内容的最佳方式是开始实践，并为以太坊区块链编写智能合约和 Dapps。

通过使用在线 Remix 工具，你将学会如何在 Solidity 中编写 HelloWorld 代码，并掌握所有所需的语法。你会从最基础的部分开始，一步一步地进行。你还将学习如何在本地以及全球分布式的测试网上编译和部署你的智能合约。然后，我们将安装并连接我们的 MetaMask 钱包到测试网。在设置好你本地的 Dapp 开发环境后，你将可以轻松地开发出自己的 Dapp，并在测试网上连接合约。在本章结束时，当你控制好自己的以太坊钱包时，你应该能够运行完整的 HelloWorld Dapp。

本章将帮助你实现以下实际目标：

+   介绍 Remix

+   编写你的第一个智能合约

+   控制你的第一个以太坊钱包

+   去中心化应用（Dapps）

+   代币标准

在上一节中，我们讨论了两种最重要的代币标准——ERC-20 和 ERC-721。ERC-721 是我们将在下一章讨论的 NFT 代币标准。

这将帮助你更加熟悉智能合约和 Dapps。

## 介绍 Remix

加文·伍德在 2014 年 8 月提出了 Solidity 编程语言。亚历克斯·贝雷加萨兹（Alex Beregszaszi）、克里斯蒂安·雷特魏瑟纳（Christian Reitwiessner）以及其他以太坊核心贡献者创造了 Solidity。它是一种高级的面向对象编程语言，灵感来源于 JavaScript、C++和 Python。Solidity 的目的是在基于 EVM 的区块链网络上执行智能合约。

有很多工具可用于创建和开发 Solidity 智能合约。Remix、HardHat、Truffle 等是 Solidity 开发者常用的流行工具。Remix 是一个功能强大的在线集成开发环境（IDE），用于在 Solidity 中编码、编译、测试和调试智能合约。我们不需要安装任何其他特殊软件，只需安装一个网络浏览器即可。

您可以在浏览器 URL 框中输入以下 URL 来打开 Remix IDE：

[`remix.ethereum.org`](https://remix.ethereum.org)。然后您将被引导到如图 5-1 所示的 Remix 主页。![](img/535492_1_En_5_Fig1_HTML.png)

显示一个带有工具栏的文件资源管理器界面。右侧显示主页，带有“remix I D E”标题，下方显示扫描警告信息。

图 5-1

Remix 主页

您会注意到 Remix 屏幕上有一个左侧工具栏菜单。当你点击每个菜单图标时，你会看到提供的不同模块。

### 文件资源管理器

在文件资源管理器模块中，您可以管理您的工作区并在工作区下创建合约文件。当你处理多个项目时，工作区可以帮助你在不同的项目工作区中组织文件。您可以创建智能合约文件、创建文件夹和将本地文件上传到当前工作区。它与其他基于浏览器的云工具非常相似，例如 Google Drive、Dropbox 等。在合约文件夹下，Remix 为您创建了三个默认合约。如果您不使用，可以删除它们。![](img/535492_1_En_5_Fig2_HTML.jpg)

显示一个带有三个图标标记的默认工作区界面。标记包括创建新合约、创建新文件夹和将本地文件加载到当前工作区。

图 5-2

Remix 文件资源管理器页面

### Solidity 编译器

在 Solidity 编译器模块中，您可以选择不同的 Solidity 编译器版本，目前版本为 0.8.7。由于 Solidity 频繁更新，您需要密切关注选择您需要的配置。创建 Solidity 文件后，可以通过点击编译按钮来编译文件。Remix 合约部分将显示文件编译信息，例如错误和警告。Remix 会每 5 秒自动保存一次当前文件更改。![](img/535492_1_En_5_Fig3_HTML.jpg)

显示一个带有文件选择和运行选项的高级配置的 Solidity 编译器界面。

图 5-3

Remix Solidity 编译器页面

### 部署和运行交易

编译智能合约后，你可以使用部署和运行交易模块来部署合约。如果你编译了多个合约，需要在合约编辑器中选择一个合约来部署。![](img/535492_1_En_5_Fig4_HTML.png)

一张标记为“部署和运行交易页面”的截图，其中包括环境、账户、燃料限制、值和合约详细信息填写表单。下半部分说明了地址添加、记录的交易和部署的合约部分。

图 5-4

Remix 部署和运行交易模块

此模块提供多个 EVM 环境：

**JavaScript 虚拟机** – JS VM 在浏览器中运行自己的沙盒区块链模拟环境。它能够非常快速地执行交易（无需挖矿）。当你执行交易时，数据只在浏览器中临时保存。一旦你关闭或重新加载页面，所有交易数据都将丢失。你必须从头开始。这对于快速尝试和测试简单合约非常有用。![](img/535492_1_En_5_Fig5_HTML.jpg)

这是一张来自标记为“环境”界面的截图。该环境包含一个用于选择 JavaScript、网络提供商和连接列表的盒子。

图 5-5

Remix EVM 环境

**注入式提供商** – Remix 将连接到浏览器中注入的 web3 提供商（通常被称为您的钱包的浏览器扩展）。目前，MetaMask 是最受欢迎的注入式提供商。您还可以使用其他流行的钱包，如 Coinbase 钱包、Trust Wallet 和 Ledger。通过提供商，您可以连接到以太坊主网络或各种测试网络。这使得 Remix 能够与真实网络互动。

**Web3 提供商** – Remix 将连接到远程节点。您需要为所选提供商提供 URL。Infura、Alchemy 和 QuikNode 是一些流行的 Web3 提供商。

### 其他模块

我们已经介绍了我们通常经常使用的 Remix 重要模块。其他如插件模块允许您安装所需的插件，如调试插件、Solidity 静态分析模块、Solidity 单元测试模块和设置模块。如果您有兴趣，可以参考 Remix 文档以获取详细信息([`remix-ide.readthedocs.io`](https://remix-ide.readthedocs.io))。

在这个阶段，我们应该已经掌握了 Remix 的基本知识。

让我们通过编写“Hello, World!”智能合约来开始学习 Solidity。

## 编写您的第一个智能合约

根据 dune.com 的数据，2022 年第二季度创建的智能合约总数为 0.93 百万。2021 年 Q2，近 6 百万智能合约被创建，如图 5-6 所示。在当前的以太坊区块链中，大多数智能合约使用 Solidity 编程语言。![](img/535492_1_En_5_Fig6_HTML.png)

2021 年第二季度创建的智能合约数量创下了最高纪录。[费曼学习法](https://wiki.example.org/feynmans_learning_method)的灵感源于诺贝尔物理奖获得者**理查德·费曼**。

图 5-6

2021 年第一季度至 2022 年第二季度智能合约创建数量

### 编写合约

在 Remix 文件浏览器模块中，在合约文件夹下，点击创建新合约图标（页面图标）或使用右键菜单添加我们的第一个合约。我们将我们的第一个智能合约命名为 HelloWorld.sol。Solidity 智能合约总是有一个`.sol`作为文件类型扩展名。

#### 软件许可

在一个智能合约的第一行，你会写你的智能合约许可。SPDX 许可标识符指示相关的许可信息。MIT 许可授予使用此软件的任何权利，如复制、修改、合并、分发等：

这里`//`是一个出现在 Solidity 程序中的一行文本，但不被程序执行。

#### `pragma`

第二行是如下所示的`pragma`：

`pragma`关键字与 C 语言相似，提供了当前的 Solidity 编译器。在这里，0.8.15 是 Solidity 编译器的版本。`^`符号意味着这个文件将只支持从 0.8.7 开始的编译器版本，直到未来的重大更改，这将导致这个文件无法编译。例如，像`pragma solidity >=0.4.0 <0.6.0`这样的合约在 0.6.0 中无法编译，因为有一个主要的变化。在这种情况下，您需要修改文件中的相关语法以使用新版本。

#### 定义合约

为了使代码更整洁，你通常会在`pragma`条目后留一个空行。然后，在下一行代码中，你开始声明合约。在 Solidity 中，我们使用`contract`关键字，后跟合约的名称。在我们这个案例中，将是 HelloWorld。合约名称应与您创建的文件名匹配。合约的内容将被大括号`{}`所包含：

solidity 编译器配置和编译 hello world 的截图。

图 5-7

HelloWorld 空合约

#### 声明合约变量

在下一行，我们输入**字符串公共信息**。

在这里，`string`关键字是一个状态变量类型。状态变量是永久存储在合约存储中的值，用于维护合约的状态。

状态变量的可见性可以被定义为公共、私有或内部。在我们这个案例中，因为我们将可见性设置为公共，所以消息字段可以在智能合约之外公开访问。

#### 定义合约构造函数

下一步是创建一个构造函数函数：

带有消息的 hello world 合约截图。

图 5-8

HelloWorld 合约构造函数

构造函数是一个可以与工厂机器相比较的函数。一旦给出一个输入，它们可以运行一个特定的任务以返回一个结果。

要声明一个构造函数，我们使用 constructor 关键字。一旦我们创建了我们的构造函数，我们可以使用相同的构造函数创建许多不同的合约。每当创建一个新的合约时，系统会自动调用构造函数；他们只需要使用一次构造函数来创建合约。如果没有显式定义构造函数，Solidity 编译器将创建一个默认构造函数，它不需要任何输入。

通常，您可能需要一个传递一个或多个参数的构造函数。在{}内部，我们添加初始化逻辑。在我们的示例中，我们传递“string memory initMessage”输入。我们在这里使用的 memory 关键字表示我们想要 initMessage 参数是可变的，或可更改的，并且 initMessage 值在合约创建时分配给 message 变量并初始化。

#### 定义函数

HelloWorld 合约将有两个函数。一个用于更新消息，另一个用于获取消息：

1.  1.

    更新合约消息函数

    更新函数将如下所示：function update(string memory newMessage) public {  message = newMessage; }

1.  2.获取合约消息函数 function getMessage() public view returns (string memory) {        return message;    }

一个 Solidity 函数定义为关键字 function，后跟

+   函数的名称。这里“update”是函数名称。

+   函数的参数列表用括号括起来，并用逗号分隔（parameter1, parameter2, ...）。它可能是空的（）。（string memory newMessage）是 HelloWorld 函数的参数。

+   函数可见性 - 公共、私有、内部和外部。

+   函数行为 - 纯净、视图和可支付。

+   当函数有返回值时，接下来是可选的返回关键字和返回值类型（type1, type2, ...）。在我们的更新函数中，没有返回值。但在 getMessage 函数中，我们返回（string memory）。

+   定义函数的语句块，由大括号{}包围。

##### 语法

基本语法如下：function function_name(<parameter types>…) {internal|external|private|public} [pure |view|payable] [returns(<return types>…)] {        //statements}

##### 函数可见性

一个函数的可见性范围可以通过这四个修改器之一来设置：

+   **公共** - 它可以在内部或外部调用。

+   **内部** - 内部函数只能从当前合约和相关派生合约中访问。

+   **外部** - 它可以被其他外部合约调用，但不能被内部调用（在当前合约内）。

+   **私有** - 类似于内部可见性，但函数不能从相关派生合约中访问。

##### 函数行为

纯净的、常量的、视图的和可支付的关键字决定了 Solidity 函数的行为。

如果函数行为未指定，它将读取和修改区块链的状态。

纯净函数：它确保调用者无法读取或修改状态。

视图函数：视图函数是只读函数，确保在调用它们之后状态变量不会被修改。

可支付：可支付回退函数也适用于简单的以太坊转账。

一旦你完成了 HelloWorld.sol，你应该有 15 行代码，如图 5-9 所示。![](img/535492_1_En_5_Fig9_HTML.jpg)

完成后的 hello world 代码的屏幕截图。

图 5-9

HelloWorld 完成的合约

### 编译合约

正如我们在 EVM 部分所学习的那样，在将合约部署到区块链之前，需要将其编译成字节码。在这个步骤中，我们将编译我们的 HelloWorld 智能合约。

Remix IDE 允许我们从浏览器直接编译我们的 Solidity 智能合约。点击导航中的编译器图标。在 Solidity 编译器页面，选择 0.8.15 编译器版本；点击编译按钮来编译 HelloWorld 智能合约。如果编译成功，您将在导航中的编译器图标上看到一个绿色的勾选标记。注意，编译详情按钮（包含应用程序二进制接口（ABI）和字节码）在编译后会出现。ABI 包含 JSON 格式的数据，编码了 EVM 理解的智能合约信息，并为 Dapp 与合约交互提供了标准方式。您可以通过点击按钮查看编译详情，如图 5-10 所示。结果将包含字节码、ABI、汇编（操作码）以及其他有用的编译合约信息。您应该将 abi 内容复制到某个地方；我们将在 Dapp 部分使用这个 abi 字符串来与智能合约调用。![](img/535492_1_En_5_Fig10_HTML.png)

合约的快照，其中用字节码标记了部分，存储布局，Web3 部署，元数据哈希，函数哈希，燃料估算，开发文档，用户文档，运行时字节码和汇编语言。

图 5-10

编译的 HelloWorld 合约

### 部署和运行合约

要部署我们的合约，请点击左侧菜单的部署和运行交易模块。您应该会看到一个下拉菜单，其中列出了所有可用的智能合约，合约标题下为 HelloWorld。HelloWorld.sol 将是默认选中的合约，下面有一个橙色的部署按钮。![](img/535492_1_En_5_Fig11_HTML.png)

显示 hello world 代码在右侧的部署和运行交易界面。左侧说明了选择环境、账户、燃料限制、值和合约的选项。

图 5-11

HelloWorld 合约部署

到目前为止，合约还没有被部署。所以，要部署 HelloWorld，我们只需在部署按钮旁边提供字符串 initMessage。

我们可以将环境保留为默认选中的 JavaScript VM，默认选中的账户，燃料限制和值。输入 Hello Solidity 并点击部署按钮。![](img/535492_1_En_5_Fig12_HTML.png)

一个界面截图，标有部署和运行交易，左边显示了 hello world 合约入口和已部署合约，右边是代码。

图 5-12

部署了 HelloWorld 合约

内置终端控制台显示部署信息。默认账户的以太币余额减少了少量的燃料费，或者交易费，从 100.00000 ETH 降至 99.99999 ETH。

在已部署合约面板下，您将看到已部署的 HelloWorld 合约和合约地址。

如果您展开已部署的 HelloWorld 合约条目，它将显示所有作为*public*在您的智能合约中定义的合约项—状态变量或函数。

我们可以看到在我们的案例中更新、getMessage 函数和 message 变量。

当你点击信息按钮时，你应该在信息按钮下方看到“Hello Solidity”。当你点击 getMessage 按钮时，情况也是如此。![](img/535492_1_En_5_Fig13_HTML.jpg)

一个标有已部署合约的截图，展示了 hello world 信息部署到合约的部分。

图 5-13

调用 HelloWorld 合约信息

要更改信息，请为更新函数输入“Hello Ethereum”，然后点击按钮设置新值。

您可以通过点击 getMessage 函数或 message 变量来验证消息变量是否已更新。![](img/535492_1_En_5_Fig14_HTML.jpg)

一个截图，显示了更新的 hello world 信息。新信息是 hello ethereum。

图 5-14

更新 HelloWorld 合约信息

恭喜您！您已经成功编写了第一个 Solidity 智能合约，并在区块链上部署了它。为了了解更多关于 Solidity 的信息，您可以访问 Solidity 官方文档([`docs.soliditylang.org/en/v0.8.15/contracts.xhtml`](https://docs.soliditylang.org/en/v0.8.15/contracts.xhtml))。

## 控制您的第一个以太坊钱包

在 Remix 中，当我们使用注入式提供者时，MetaMask 是最广泛使用的钱包提供者之一。MetaMask 是由 Aaron Davis 和 Daniel Finlay 于 2016 年创立，目前隶属于 ConsenSys。截至 2022 年 3 月，MetaMask 拥有超过 3000 万月活跃用户。作为一个免费的 Chrome、Firefox、Brave 和 Edge 浏览器扩展程序，MetaMask 允许您的普通浏览器作为 web3 浏览器来存储和交换加密货币，以及与以太坊 Dapps 进行交互，而无需运行以太坊节点。简而言之，MetaMask 是一个可以通过浏览器访问的移动加密钱包。要管理 MetaMask 的访问权限，用户只需要一个密码和 12 个单词的恢复短语，也称为种子短语。种子短语可以由任何真实单词组成，例如 dog、cat 或 chicken。

如果您忘记了或者丢失了钱包恢复短语，就没有办法恢复您的加密钱包密码。非常重要的一点是，您要在一个安全的地方备份这些种子短语，比如硬盘、USB 驱动器或纸张。不要将其存储在可能不安全的地方，比如电子邮件、在线存储等。

MetaMask 可能不是存储大量加密货币或宝贵加密货币资产（如 NFT）的最佳场所。在连接主网进行交易时，请将 MetaMask 作为该浏览器中唯一的标签页使用，并避免在同一个浏览器中连接社交媒体账户——一些社交媒体网站有插件可以窃取您的数据。

从[`metamask.io`](https://metamask.io) 安装 MetaMask。然后将 MetaMask 钱包软件下载到您选择的浏览器中。选择“创建钱包”选项，阅读条款和条件，并创建密码。安装后，您将在浏览器的右上角看到一只狐狸。打开 MetaMask，通过点击设置➤高级➤显示测试网络，并选择一个按钮来“在网络列表中显示测试网络”。测试网络上的交易旨在仅模拟主网交易，或真正的区块链交易。![](img/535492_1_En_5_Fig15_HTML.png)

元掩码界面截图，包括一个设置页面。已选择高级设置选项，选项分别为存储日志、与移动设备同步、重置账户、高级气体控制、显示十六进制数据和网络。

图 5-15

更新 MetaMask 的测试网络设置

现在，您可以从 MetaMask 的网络列表设置中切换到 Goerli 测试网络。![](img/535492_1_En_5_Fig16_HTML.jpg)

Goerli 测试网络添加新网络的截图。

图 5-16

将 MetaMask 连接到 Goerli 测试网络

您会看到账户 1 中有默认账户，但没有以太币。

我们将从 Goerli 测试网络获得一些免费的测试以太币。复制账户 1 的以太坊地址，并使用 Goerli 测试网络水龙头之一通过您的以太坊账户地址获取以太币：

+   官方 Goerli 测试网络水龙头：[`goerli-faucet.slock.it/`](https://goerli-faucet.slock.it/)

+   Starknet Faucet : [`faucet.goerli.starknet.io/`](https://faucet.goerli.starknet.io/)

+   Goerlifaucet: [`goerlifaucet.com/`](https://goerlifaucet.com/) 注意

大多数测试网络在几个月后将会被终止（截至 2022 年 7 月）。目前，Goerli 已确认会在将来继续运行，所以这个网络中的测试以太币通常需求量大。您可能需要尝试几次才能获得一些以太币。

一旦您成功提交了水龙头请求，您将会在您的账户中得到一些以太币。![](img/535492_1_En_5_Fig17_HTML.jpg)

在 Goerli 测试网络上，账户 1 的截图，显示 0.05 goerli E T H。

图 5-17

从 Goerli 测试网络水龙头获取以太币

有了这些以太币，你已经完成了将你的智能合约带入生命的所有艰苦工作。现在该是与世界分享你的第一个智能合约的时候了！让我们从 Remix 部署我们的 HelloWorld 智能合约到 Goerli 测试网络。

在 Remix 中，部署并运行交易模块，选择注入的 Web3 环境。Metamask 将弹出一个提示，要求连接到 Goerli 测试网络中的账户 1。![](img/535492_1_En_5_Fig18_HTML.png)

一张标记有“部署并运行交易”的屏幕截图，右侧有一个标记为“连接 Metamask”的界面，且已选择一个账户。下方部分显示取消和下一步选项。

图 5-18

连接 Remix 到 Goerli 测试网络

点击“下一步”，将连接 Remix IDE 与 Metamask 的 Goerli 测试网络。如图所示，你应该会看到一个显示连接状态的绿色按钮。![](img/535492_1_En_5_Fig19_HTML.png)

一张显示在测试网络中连接的账户，标记为“0.05 goerli E T H”的屏幕截图。

图 5-19

连接到 Goerli 测试网络的 Metamask

现在我们可以将我们的 HelloWorld.sol 部署到 Goerli 测试网络。在橙色的部署按钮右侧输入“Hello Solidity”作为初始信息。然后点击部署。Metamask 将动态计算预计的燃料费。在提交到测试网之前，你可以确认或拒绝这个请求。让我们确认这个部署交易。![](img/535492_1_En_5_Fig20_HTML.png)

一张标记有“部署并运行交易”的界面截图，右侧显示 Meta Mask 通知页面。

图 5-20

将合约部署到 Goerli 测试网络

在 Remix 控制台中，你将看到一个区块交易确认信息，它返回了交易哈希和其他交易信息。交易哈希为：0x7f773384290cff58ff6bb6e4f0411bfb625d3c1aa957208c6e8b8abeeed9d710![](img/535492_1_En_5_Fig21_HTML.png)

一张显示 hello world 合约交易收据的屏幕截图。

图 5-21

带有交易收据的部署合约

在 Metamask 中，我们可以看到在“活动”标签下，新合约的部署信息被显示出来。注意账户的以太币价值被交易燃料费扣除了。原来的值是 0.05 ETH。现在它是 0.0487 ETH。![](img/535492_1_En_5_Fig22_HTML.png)

一张显示“goerli 测试网络”界面，账户 1 被选中的屏幕截图。在中心部分，“0.0487 goerli E T H”显示购买、发送和交换选项。

图 5-22

部署合约时消耗的燃料费当你点击“合约部署”，它将显示部署信息的详细细节。![](img/535492_1_En_5_Fig23_HTML.png)

一张标记有“合约部署状态和交易详情”的屏幕截图，右侧有一个标记为“已确认”的界面。

图 5-23

合约部署详情

你可以点击“在区块链浏览器中查看”。链接将引导你到 etherscan.io 页面，并显示此合约部署的详细信息。你可以看到合约被部署到了地址 0xe02cfad8b29d0aad478862facb2e6a9b1fed7bc9（注意：当你部署它时，它会显示不同的地址号码）。这个地址对所有人公开可用。

既然你已经部署了你的第一个区块链智能合约，交易哈希与我们在 Remix 控制台看到的值相匹配。你可以在 etherscan 搜索栏中搜索该地址。![](img/535492_1_En_5_Fig24_HTML.png)

一个截图，显示了一个 ether scan 合约页面界面，标记了交易详情成功。

图 5-24

在 etherscan 上部署的合约

太好了！你已经将 HelloWorld 合约部署到了 Goerli 测试网络，该网络对公众开放，从任何地方都可以访问。接下来，让我们构建一个简单的 Dapp 来与我们的智能合约交互。

## 去中心化应用（Dapps）

通常，一个 Dapp 是一个由三个主要组件组成的三层应用程序：

+   **前端层** – 带有网页服务器的网络浏览器。

+   **Web3 提供者层** – 前端和智能合约之间的中间层，即 Metamask 钱包。

+   **后端（智能合约）** – 合约在区块链网络上运行。

图 5-25 显示了一个典型的 DApp 层架构：![](img/535492_1_En_5_Fig25_HTML.jpg)

一个带有 web 客户端、web 提供者、智能合约和以太坊区块链的 dapp 层架构流程图。

图 5-25

Dapp 层架构

在以太坊客户端部分，我们使用 web3 API 从 geth 控制台查询一些区块链信息。在本节中，我们将探讨另一个以太坊 JavaScript 开源库——Ether.js，它也使 web 客户端能够与以太坊网络进行通信和交互。

### 开始

在继续本节之前，你需要安装以下内容：

#### 安装 node.js

遵循节点办公室安装指南，下载并安装 node.js：

[`nodejs.org/en/download/`](https://nodejs.org/en/download/)

#### 安装 Git

遵循 Git 办公室安装指南来安装 Git：

[`git-scm.com/book/en/v2/Getting-Started-Installing-Git`](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

#### 使用 Git 克隆 HelloWorld Dapp 项目

安装 node 和 Git 之后，你需要前往本书的 Apress 网站，用 Git 克隆第五章的 HelloWorld Dapp 源代码：git clone https://github.com/Apress/Blockchain-for-Teens.git

#### 安装 HelloWorld Dapp 项目

打开终端，导航到 helloworld 项目位置。运行 npm install

![](img/535492_1_En_5_Figa_HTML.jpg)

hello world 项目位置的截图。

这将安装运行 HelloWorld Dapp 所需的节点库。

项目结构应与图 5-26 所示的类似。![](img/535492_1_En_5_Fig26_HTML.jpg)

项目结构文件夹的截图，说明在选择 client.js 后的选项。

图 5-26

Dapp 项目结构

注意，源代码指向 Goerli 测试网络合约地址：0xe02cfad8b29d0aad478862facb2e6a9b1fed7bc9

您可以使用此地址进行测试，或者修改此地址为您的部署合约地址。

打开 client.js，更新第 3 行您的地址。如果您修改了合约并且有不同的合约 abi，用您自己的合约 abi 替换第 4 行。

![](img/535492_1_En_5_Figb_HTML.png)

截图测试您合约地址的地址。

#### 运行 HelloWorld Dapp 项目

从终端运行以下命令，该命令位于 helloworld 文件夹之后：node index.js 这将启动节点服务器以托管 HelloWorld Dapp。端口号是 3000。![](img/535492_1_En_5_Fig27_HTML.jpg)

Dapp 节点服务器地址的截图。

图 5-27

启动 Dapp 节点服务器

#### 从浏览器打开 HelloWorld Dapp

现在您可以从浏览器中通过输入 http://localhost:3000 来打开 Dapp。您应该看到 HelloWorld Dapp 页面。您可以看到右上角有一个连接按钮，将连接到 MetaMask。页面中间有一个蓝色的消息按钮，可以用来获取区块链消息。带有消息输入框的红色更新按钮将更新合约消息内容。![](img/535492_1_En_5_Fig28_HTML.png)

E 2 E hello world dapp 页面的截图。位于中心的带有标题消息更新的盒子。

图 5-28

Dapp 初始页面

### 连接到 MetaMask

Ether.js 使用 Web3Provider API 连接 MetaMask 钱包：ethers.providers.Web3Provider(window.ethereum)。点击连接按钮。如果您尚未登录，它将提示您登录：await provider.send("eth_requestAccounts", []);

一旦连接，我们就可以从提供商获取用户钱包、网络和账户信息。provider.getSigner()将从 MetaMask 钱包获取以太坊账户。provider.getNetwork()返回钱包连接的当前以太坊网络。

以下是一段代码片段：

![](img/535492_1_En_5_Figc_HTML.png)

代码片段的截图。

由于您是第一次运行 Dapp，并且尚未连接到 MetaMask，Dapp 页面的连接按钮将是橙色的。所以让我们点击连接按钮以连接到 MetaMask。再次，如果您尚未登录，您将看到来自 MetaMask 的弹出窗口，要求您登录。![](img/535492_1_En_5_Fig29_HTML.png)

带有标签 E 2 E hello world dapp 的界面截图和一个要求登录信息的 MetaMask 页面。

图 5-29

Dapp 连接到 MetaMask

登录到 Metamask。页面将自动连接到 Metamask，并在顶部的绿色显示区域显示相关账号和网络信息。![](img/535492_1_En_5_Fig30_HTML.png)

一个界面截图，标签为 E 2 E hello world dapp，右侧有一个成功图标，显示一个用于信息更新的盒子。

图 5-30

Dapp 连接到 Metamask，带有区块链数据

#### 获取合约并调用获取信息

在 Remix 智能合约编译和部署中，我们已经获得了 abi 和合约地址信息。下面提供了 ether.js  api 以获取合约信息，你可以使用新的 ethers.Contract(contactAddress, abi, provider) API 来获取已部署的合约实例。

![](img/535492_1_En_5_Figd_HTML.png)

一个只读合约消息代码的截图。

使用 ether 合约对象，你可以开始调用“getMessag”函数：

![](img/535492_1_En_5_Fige_HTML.jpg)

一个截图，显示调用获取信息函数代码。

你将从 Goerli 测试网络收到“Hello Solidity”消息：![](img/535492_1_En_5_Fig31_HTML.png)

一个截图，显示 E 2 E hello world dapp 界面中的“Hello Solidity”消息更新框。

图 5-31

Dapp 获取第一条信息

#### 获取合约并调用更新信息

当你需要调用改变状态的方法时，例如更新信息，你必须连接到签名者并支付一笔交易费用来发送改变状态的交易：

![](img/535492_1_En_5_Figf_HTML.jpg)

一个截图，显示签名者合约对象输入信息以更新合约。

有了签名者合约对象，你现在可以将输入信息传递给合约以更新合约：

![](img/535492_1_En_5_Figg_HTML.jpg)

一个截图，显示一个同步函数更新信息。

让我们更新我们的信息，输入“你好 Ethereum”。![](img/535492_1_En_5_Fig32_HTML.png)

一个截图，显示 E 2 E hello world dapp 中带有“hello ethereum”消息的拒绝和确认事务页面。

图 5-32

Dapp 更新信息

Metamask 将会弹出，并要求确认带有估算的交易费用的事务。你审查事务并提交。区块浏览器允许你查看事务。![](img/535492_1_En_5_Fig33_HTML.jpg)

一个截图，显示更新信息以及带有已确认交易和来自和到的信息的交易详情。

图 5-33

Dapp 更新信息事务详情

点击区块浏览器中的查看，以在 etherscan 上查看你的事务。![](img/535492_1_En_5_Fig34_HTML.png)

一个截图，显示 etherscan 事务详情，其中成功信息被突出显示。

图 5-34

Dapp 在 etherscan 上的更新信息事务

一旦事务被确认，你将在页面弹出窗口中收到交易收据。![](img/535492_1_En_5_Fig35_HTML.png)

交易收据的屏幕截图，右侧显示成功消息，一个盒子显示本地主机消息，一个选项标记为确定。

图 5-35

带有响应交易收据的 Dapp

最后，通过点击信息按钮验证您的更新信息。“Hello Ethereum”应该显示在页面上。![](img/535492_1_En_5_Fig36_HTML.png)

屏幕截图，显示在 E 2 E hello world dapp 界面中更新信息，说你好以太坊。

图 5-36

Dapp 验证更新信息

恭喜你，你已经成功将你的第一个智能合约发布到公共测试网，并构建了一个 Dapp 来调用和更新信息内容！您现在已经完成了一个端到端的 Dapp 开发周期，这是一个巨大的成就。拍拍自己的背，因为那是一份辛苦的工作。

尽管我们已经花了很多时间探索以太坊 Dapp 和 Solidity 原则，以便让您构建一个 Dapp，但这本书只提供了基础介绍。有很多优秀的在线文档涵盖了 JavaScript、JQuery、express.js 和 ether.js 的所有方面。

以下是一些有用的链接：

+   ether.js：文档可以在[`docs.ethers.io/v5/`](https://docs.ethers.io/v5/)找到

+   JQuery：文档可以在[`jquery.com/`](https://jquery.com/)找到

+   express.js：文档可以在[`expressjs.com/en/starter/hello-world.xhtml`](https://expressjs.com/en/starter/hello-world.xhtml)找到

+   Node.js：文档可以在[`nodejs.org/en/docs/guides/getting-started-guide/`](https://nodejs.org/en/docs/guides/getting-started-guide/)找到

## 代币标准

在第一章中，我们了解到莫卧儿王朝的货币改革家莫卧儿·宾·图格勒克发明了代币货币——坦卡，它使用铜币代表与银币相同的价值。在区块链中，硬币代表原生货币。例如，以太坊中的货币是以太币。而代币是由智能合约创建的，该合约定义了基本代币属性，然后构建和运行。

加密代币是一种代表可编程资产或具有特定价值的共享所有权的虚拟货币代币。代币由智能合约管理，该合约允许高效安全地购买或出售艺术品收藏等物品，进行代币所有权的交换，代币余额的转移，代币价值的存储以及区块链上交易的验证。

为了帮助开发者标准化代币创建，以太坊社区通过以太坊改进提案（EIP）过程开发了许多代币标准。

EIP 包含潜在的新以太坊功能或过程的技术规范，包括核心协议规范、改进、客户端 API 和合约标准。它作为社区的“真相来源”。任何人都可以通过遵循 2015 年发布的 EIP-1 中的标准指南创建 EIP（[`eips.ethereum.org/EIPS/eip-1`](https://eips.ethereum.org/EIPS/eip-1)）。如 EIP-1 所述，以太坊请求评论（ERC）是应用级标准和约定。如果特定的 ERC 在以太坊社区中获得批准，它将成为新的代币标准规则，并通过相关智能合约在文档中概述。

有许多代币标准，包括：

+   代币标准（ERC-20、ERC-721、ERC-1155、ERC-777）

+   名称注册表（ERC-26、ERC-137）

+   统一资源标识符方案（ERC-67）

+   库/数据包格式（EIP-82）

+   钱包格式（EIP-75、EIP-85）

还有许多其他代币仍处于草稿和审查状态。您可以通过此链接查看所有 ERC 代币：[`eips.ethereum.org/erc`](https://eips.ethereum.org/erc)

让我们来看一下两个最受欢迎的 ERC 标准，ERC-20 和 ERC-721。

### ERC-20

ERC-20 是最受欢迎的以太坊代币标准，由 Fabian Vogelsteller 于 2015 年 11 月 19 日提出。大多数在以太坊平台或基于 EVM 的区块链（如 Binance）发行其代币的 ICO（首次代币发行）都是 ERC-20 代币。ICO 是加密货币版本的 IPO（首次公开募股），在股票市场中用于筹集资本或参与投资机会。截至 2022 年 3 月，以太坊主网上有大约 508k ERC-20 代币。所有 ERC-20 代币的总市值约为 187 亿美元，Binance 上有超过 160K ERC-20。

20 是一个独特的识别号码，用于区分 ERC-20 标准与其他标准。

ERC-20 代币有几个可选字段，如名称和符号，并在智能合约中定义了以下规则：contract ERC20Interface {    function totalSupply() public view returns (uint);    function balanceOf(address tokenOwner) public view returns (uint balance);    function allowance(address tokenOwner, address spender) public view returns (uint remaining);    function transfer(address to, uint tokens) public returns (bool success);    function approve(address spender, uint tokens) public returns (bool success);    function transferFrom(address from, address to, uint tokens) public returns (bool success);    event Transfer(address indexed from, address indexed to, uint tokens);    event Approval(address indexed tokenOwner, address indexed spender, uint tokens);}

totalSupply(): 获取代币总供应量。

balanceOf(): 获取指定地址的账户余额。

allowance(): 返回允许从所有者账户中提取的代币数量。

transfer(): 将所有者账户的余额转移到另一个指定地址，并必须触发转移事件。

transferFrom (): 从地址`from`向地址`to`发送代币数量。transferFrom 方法用于提现工作流程，允许合约代表你转移代币。

approve(): 允许花费者从你的账户中多次提取指定数量的代币。

如果你发现自己正在从事一个需要创建和部署 ERC-20 代币的项目，你可以通过实现这些 ERC-20 函数来创建智能合约。这是一个简单的例子：MyToken 是 ERC20 { // 实现 ERC20 接口标准所需的函数 // 其他函数... }在 Etherscan 上，你可以找到许多符合 ERC-20 标准的已部署主网代币。以下是在 Etherscan 上的一个 ERC-20 代币交易的真实世界示例！[](../images/535492_1_En_5_Chapter/535492_1_En_5_Fig37_HTML.png)

一张界面截图，标签为“kucoin token”的代币，展示了概览、简介和 34,718 笔交易记录，标记为转账和转出。

图 5-37

ERC-20 示例

截图显示了通过 transfer 或 transferFrom 方法将 ERC-20 代币从一方地址转移到另一方地址的金额。

在 ERC-20 代币中，代币是可互换的，意味着每个代币与其他代币完全相同类型和价值。如果你用一个 ERC-20 交换另一个，它们的真伪或价值上不会有任何差异；它们是可互换的，代表单一实体。

例如，泰达币（USDT）是一种 ERC-20 代币。它是一种稳定币——一种与美元挂钩的加密货币资产，比例为 1 比 1，100%由泰达币等值储备支持。这些储备包括现金等多种资产。USDT 与 ETH 相似，意味着 1 个代币始终等于所有其他 USDT 代币。它们属于同一类型，代表美元，可以互相替换。USDT 也是可分割的，可以分解成像分币这样的更小单位。

因此，同质化代币具有以下特性：可互换、统一和可分割。

接下来让我们谈谈不可互换的代币，换言之，非同质化代币。

### ERC-721

所有 ERC-20 代币（如 USDT）都是相同的，并提供相同的价值。所以重要的是你的钱包里拥有多少代币，而不是它们各自的独特身份。非同质化代币（NFTs）可以被唯一标识；它们是存储在区块链网络上的数据的资产。NFTs 与其他 NFTs 不可互换，因为它们是独一无二的。想想看，一个由艺术家创作的独特艺术作品，时尚公司的高端品牌物品，以及不同的视频。

ERC-721 是一个非同质化代币的标准接口，也称为产权证明，可在[`eips.ethereum.org/EIPS/eip-721`](https://eips.ethereum.org/EIPS/eip-721)找到。这个新标准的提案是在 2018 年 1 月创建的，由 William Entriken、Dieter Shirley、Jacob Evans 和 Nastassia Sachs 提出。根据彭博社的报道，NFT 市场在 2021 年超过了 400 亿美元，在 2022 年 5 月 1 日的 NFT 市场平台上超过了 370 亿美元。

与 ERC-20 代币标准相似，ERC-721 规格提供了详细信息，并定义了派生合约应实现的功能和事件，以开发 NFT，如下面的代码块所示：interface ERC721 {    event Transfer(address indexed _from, address indexed _to, uint256 indexed _tokenId);    event Approval(address indexed _owner, address indexed _approved, uint256 indexed _tokenId);    event ApprovalForAll(address indexed _owner, address indexed _operator, bool _approved);    function balanceOf(address _owner) external view returns (uint256);    function ownerOf(uint256 _tokenId) external view returns (address);    function safeTransferFrom(address _from, address _to, uint256 _tokenId, bytes data) external payable;    function safeTransferFrom(address _from, address _to, uint256 _tokenId) external payable;    function transferFrom(address _from, address _to, uint256 _tokenId) external payable;    function approve(address _approved, uint256 _tokenId) external payable;    function setApprovalForAll(address _operator, bool _approved) external;    function getApproved(uint256 _tokenId) external view returns (address);    function isApprovedForAll(address _owner, address _operator) external view returns (bool);}

balanceOf: 获取指定地址的账户余额。

ownerOf: 该函数根据提供的 tokenId 返回代币所有者的唯一地址。

safeTransferFrom: 将 NFT 的所有权从一个地址转移到另一个地址。要求 msg.sender 是当前所有者、授权的操作员或此 NFT 的批准地址。

transferFrom (): 从地址`from`向地址`to`发送代币金额。transferFrom 方法用于提现工作流程，允许合约代表您转移代币。

approve(): 允许花费者多次从您的账户中提取指定数量的代币。

setApprovalForAll: 为给定的操作员分配或撤销管理所有`msg.sender`资产的权利。

getApproved: 获取单个 NFT 的已批准地址。

isApprovedForAll: 检查给定的操作员地址是否具有操作给定所有者代币的权利。

ERC-721 最著名的例子是加密猫游戏，这是第一个 NFT 代币。在游戏中，有数千只 CryptoKittie。每只猫都有自己的资料，包括独特的基因、名字、颜色、形状、价格和其他资料。游戏玩家可以收集和繁殖可爱的猫咪。如图 5-38 所示，每只加密猫作为可收藏的数字资产可以被玩家交易、出售和购买：![](img/535492_1_En_5_Fig38_HTML.png)

一张动画猫的屏幕截图，以及标记为 kitty hash 1111 的标签，附有诸如所有者、出生、代数、区块号、区块哈希、官方资料和属性的信息。在标签下方，展示了基因信息。

图 5-38

ERC-721 加密猫示例

我们可以在 etherscan 上找到 CryptoKittie。这些代币每天由游戏玩家进行出价和交易。一些个体的加密猫已经以每只超过 30 万美元的价格售出。![](img/535492_1_En_5_Fig39_HTML.png)

以太坊扫描加密猫库存的屏幕截图。

图 5-39

ERC-721 CryptoKitties 在 Etherscan

随着粉丝参与度的提高，NFT 收藏品市场仍在不断增长，这可能会增加主流采用率。NFT 同一时间只能有一个所有者。真正所有权是任何 NFT 的关键特征之一，它有可能在将数字世界和物理世界联系得比以往任何时候都更紧密方面发挥关键作用。

## 总结

您已经通过 Remix IDE 编写了第一个智能合约，并将 HelloWorld Solidity 文件部署到了 Goerli 测试网络。我们展示了 Dapp 和 web3.js 的基础知识，以及通过与 Metamask 钱包连接来演示 Dapp 如何与智能合约互动。

但我们的旅程并未就此结束——在下一章中，我们将详细介绍 NFT 的更多激动人心之处。
