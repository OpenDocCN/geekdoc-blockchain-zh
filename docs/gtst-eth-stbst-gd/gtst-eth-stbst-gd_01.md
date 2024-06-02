© 作者，独家许可给 APress Media，LLC，Springer Nature 旗下的一部分 2022D. P. Bauer 开始使用以太坊 [`doi.org/10.1007/978-1-4842-8045-4_1`](https://doi.org/10.1007/978-1-4842-8045-4_1)

# 1. 入门

大卫·佩德罗·鲍尔^(1  )(1) 圣保罗，巴西南部，巴西

在本章中，我将解释以太坊是什么，并带领你完成必须执行的安装，然后才能开始使用它。

## 以太坊是什么？

以太坊解决了超越比特币的问题。在开发去中心化应用程序时，我们需要一个平台，我们不仅可以编码硬币，还可以编码各种各样的解决方案。

以太坊是一个允许您使用 Solidity 语言编写智能合约的平台。使用它，您可以将代码编译成字节码，以供以太坊虚拟机（EVM）解释。

此虚拟机将解释智能合约字节码中包含的指令，并根据合同中描述的规则创建新状态。就像你手里有一个状态机，每次新状态更新时，区块链上的新记录都会更新。

类似 EVM 的虚拟机会消耗资源，因此您需要一种机制来激励更多的人成为网络中的节点，同时防止垃圾邮件攻击。因此，执行操作需要一个称为*气体*的元素。

要确保使用气体，你首先必须拥有*Ether*，这是以太坊网络的货币。你使用气体来支付计算费用，因此可以将其视为使用系统的成本。你将需要气体来执行本书中描述的大多数活动。

以太坊平台允许您构建去中心化应用程序，这些应用程序的源代码是不可变的，数据在编写后无法更改。这开辟了一系列新的解决方案，如投票、供应链和去中心化金融等。

最佳学习方式是编码，所以让我们开始吧。

## 安装 Visual Studio Code

在开始使用以太坊之前，您需要安装一些软件。首先是 Visual Studio Code，^(1) 这是一个开源的代码编辑器，包含了调试、任务执行和版本管理等功能。它为开发人员提供了只需要的工具，以进行快速的代码构建和调试循环，将更复杂的过程留给像 Visual Studio IDE 这样的完整功能的 IDE。

你可以免费下载它，适用于不同平台，如 Windows、Linux 和 Mac。本书中的所有练习都是基于使用这个工具的。

## 安装 Docker

Docker^(2) 是一个免费且开放的平台，用于创建、交付和执行应用程序。Docker 允许您将应用程序与基础架构解耦，从而可以更快地部署软件。Docker 允许您以与控制应用程序相同的方式来管理基础架构。通过利用 Docker 的快速交付、测试和部署代码的技术，您可以大大缩短开发代码和将其在生产中执行之间的时间。在使用 Truffle 进行编译之前，您需要启动 Docker。

## 在 VS Code 上安装区块链开发工具包扩展

以太坊区块链开发工具包^(3) 专为新手和已经熟悉流程的用户设计。其主要目标之一是帮助用户为这些智能合约创建项目结构；它还帮助用户编译和构建资产、将资产部署到区块链端点，并执行合约调试。^(4)

### 安装扩展

前往扩展并搜索*以太坊区块链开发工具包*。点击由微软创建的扩展；通常会是第一个（图 1-1）。![](img/521550_1_En_1_Fig1_HTML.jpg)

市场扩展窗口的截图。搜索栏显示以太坊区块链开发工具包。区块链开发扩展是第一个并且被选中的。此扩展的属性包括开发、部署、调试和管理。

图 1-1

安装以太坊区块链开发工具包

单击安装，等待安装完成。完成！

## 安装 Truffle

Truffle^(5) 是一个以太坊开发环境、测试框架和资产管道，旨在为以太坊开发者提供更轻松的生活。我们将在本书中使用这个工具。^(6)

### 安装 Truffle

转到终端窗口并安装 Truffle 包。$ npm install -g truffle

### 检查 Truffle 安装

现在您可以检查安装是否成功。如果您看到图 1-2 中显示的结果，那么安装成功了。$ truffle![](img/521550_1_En_1_Fig2_HTML.jpg)

Truffle 命令输出的屏幕截图显示了顶部的安装详细信息，接着是 Truffle v 5.2.6，这是用于以太坊的开发框架。更下面提供了使用详情，并列出了一长串命令及其功能。

图 1-2

Truffle 命令输出结果

## 安装 Ganache 命令行界面

Ganache^(7) 是一个个人区块链，可快速开发以太坊和 Corda 分布式应用。Ganache 可在开发周期中使用，让您在安全且确定性的环境中开发、部署和测试您的 DApps。^(8)

### 安装 Ganache

转到终端窗口并安装 Ganache 命令行界面。npm install -g ganache-cli

### 在本地启动 Ganache

使用以下命令在 127.0.0.1:8545 上启动 Ganache CLI：ganache-cli。通过这个命令，除了在本地启动 Ganache 外，它还会生成十个带有各自公钥和私钥的账户，以便您用于测试目的（见图 1-3）。

一个由 Ganache 生成的可用账户的截图。安装详情显示在顶部，后跟 Ganache C L 1 v 6\. 点 12 点 2，ganache-core: 2 点 13 点 2。更下面，有一个可用账户列表，每个账户都有长代码和括号内的 100 E T H。

图 1-3

Ganache 生成的账户

## 安装并设置 MetaMask 钱包

MetaMask^(9) 是一个浏览器扩展，允许您访问基于以太坊的分布式应用程序，或 DApps。此附加组件将以太坊 Web3 API^(10) 注入到每个网站的 JavaScript 上下文中，使 DApps 能够从区块链中读取数据。^(11)

当一个 DApp 想要执行交易并将其发布到区块链时，MetaMask 会为用户提供一个安全界面，以通过私钥、本地客户端钱包和像 Trezor 这样的硬件钱包评估交易并批准或拒绝它。^(12)

### 安装钱包

前往 [`metamask.io`](https://metamask.io)，点击安装 MetaMask。点击添加到 Brave 或您的浏览器名称，然后点击“添加扩展”。最后，点击“开始”。

### 配置钱包

点击“创建钱包”，然后点击“不，谢谢”（如果您愿意，也可以点击“我同意”）。定义您将用于打开钱包的密码，然后确认密码。同意使用条款。最后，点击创建。现在您可以备份您的秘密短语（您也可以稍后进行）。暂时点击“稍后提醒我”。您的钱包已经完成了！

### 访问您的钱包

点击扩展并将 MetaMask 固定到您的栏中。现在，点击 MetaMask 图标，您的钱包将显示。

### 发现你的钱包地址

点击右上角的三个点，然后点击“账户详细信息”。注意你可以以哈希格式和二维码格式查看你的钱包地址。你也可以通过点击账户名复制你的钱包地址。就是这样！

### 在 Infura 上创建账户

Infura^(13) 提供工具和基础设施，使开发人员能够快速将他们的区块链应用从测试转移到规模化部署，同时保持对以太坊和 IPFS 的简单、可靠的访问。一个常见的使用 Infura 作为数据接口的用例是 Uniswap。^(14)^,^(15)

### 创建一个新账户

前往 [Infura](https://infura.io/)^(16) 并点击“免费入门”。输入你的电子邮件和密码，然后点击“注册”。一封验证电子邮件将发送到你的地址（图 1-4）。![](img/521550_1_En_1_Fig4_HTML.jpg)

Infura 欢迎页面的屏幕截图左侧有以太坊和 Filecoin。窗口显示，“让我们开始吧。我们的 E t h 2 A P I 已上线。立即申请我们的私人测试版。正在使用 Filecoin 进行构建？加入 Infura Filecoin A P I 的等待列表。开始并创建你的第一个项目以访问以太坊网络！”

图 1-4

登录后你将看到的 Infura 欢迎页面

检查你的电子邮件，并通过点击验证链接确认你的账户。之后，你将被重定向到你的仪表板。点击左侧菜单中的以太坊选项卡。

现在你的账户已创建，你可以开始设置一个新项目（图 1-5）。![](img/521550_1_En_1_Fig5_HTML.jpg)

该项目的主页左侧有以太坊和 Filecoin，选择了以太坊。窗口显示，“通过 H T T P S 和 Web Sockets 即时访问以太坊网络。文本下方显示“创建项目”按钮。

图 1-5

点击以太坊将你带到项目的主页

### 设置您的 Infura 项目

登录您的仪表板，点击以太坊。然后点击“创建项目”并定义项目名称。请注意，您可以连接不同的测试网络，也可以连接到主网。保存更改。

创建项目后，提供有关连接的 ID、密钥和端点的信息（图 1-6）。![](img/521550_1_En_1_Fig6_HTML.jpg)

Infura 项目页面顶部显示项目详情，下面是 Keys。顶部有一个名称栏和一个标记为保存更改的按钮。在 keys 下面，部分是项目 I D，显示的 I D，项目密钥，带有一个栏，和端点，其中输入了 Mainnet。下面有两个链接。

图 1-6

Infura 项目详情页面

## 概要

在本章中，您学习了以太坊是什么，以及如何安装必要的软件开始开发智能合约。

在下一章中，您将探索 Solidity 并学习如何在此语言中设置您的第一个项目。