© Elad Elrom 2019 Elad Elrom 区块链开发者[`doi.org/10.1007/978-1-4842-4847-8_7`](https://doi.org/10.1007/978-1-4842-4847-8_7)

# 7. NEO 区块链与智能合约

Elad Elrom^(1  )(1)纽约，纽约，美国

在第一章中，我介绍了 NEO 权益证明（PoS）区块链共识机制。在第二章中，你在 AWS Ubuntu 上创建了一个 NEO 记账节点，并学习了如何申请共识权威证书和当选记账节点。

在本章中，我将详细介绍 NEO 区块链，您将学习如何设置本地环境，在 NEO 钱包中进行操作，创建智能合约（NeoContracts），并进行发布。在本章中，我将涵盖 NEO 区块链的高级架构以及如何设置本地环境，创建本地测试网链，用 C#和 Python 创建“你好，世界”项目，发布这些智能合约，并学习比较以太坊、EOS 和 NEO 的标准。

正如你所看到的，理解智能合约、区块链以及发布过程在各个项目中是相似的，涵盖三个项目就足以了解如何与其他 40 个项目（截至撰写本文时）一起编写智能合约。

## NEO 的高级区块链架构

NEO 于 2014 年由达鸿飞和 Erik Zhang 以 AntShares 的名字创立，然后在 2015 年 6 月以 NEO 的名字在 GitHub 上开源。NEO 的共识机制被称为拜占庭容错（dBFT），这是一种修改后的 PoS。这种机制使得 NEO 成为一个可扩展的区块链。记账节点随机选择以验证交易，并可支持每秒 10,000 笔交易。

> “NEO 是一个非盈利性社区驱动的区块链项目。它利用区块链技术和数字身份来数字化资产和利用智能合约自动化管理数字资产。利用分布式网络，旨在创建一个‘智能经济’。”
> 
> —Neo.org

NEO 交易使用 NEO 燃料代币进行支付。NEO 创世块包含 1 亿 NEO。一半卖给了早期投资者，另一半被锁定在 NEO 智能合约代币中。每年有 1500 万 NEO 代币解锁，用于资助 NEO 开发团队的发展目标。NEO 对交易以及与智能合约相关的交易收取费用。NEO 关于智能合约的费用结构列在 NEO 白皮书：[`docs.neo.org/en-us/sc/systemfees.html`](http://docs.neo.org/en-us/sc/systemfees.html)。

在编程语言方面，NEO 智能合约支持 NeoVM（NEO 的通用轻量级虚拟机）编译器、Microsoft.net、Java、Kotlin、Go 和 Python。

以下是一些值得注意的 NEO 开发特性：

+   NEO 可以创建基于通信标准（NEP5）的智能合约代币。这些代币能够与其他 NEO 代币进行通信。

+   智能合约可以与其他区块链进行通信（这一特性称为 NeoX）。

+   NEO 可以通过一个文件共享协议（称为 NeoFS）传递信息。

+   它使用了一种称为量子安全的基于格密码学机制（NeoQS）。

NEO 的“智慧经济”基础设施（我将在下一节解释这个概念）使智能合约能够支持前端应用程序，并通过开放 API 与其他智能合约和其他区块链集成。

NEO 的开放 API 允许你集成来自外部源的数据。图 7-1 显示了 NeoVM 的高级架构图。NeoVM 核心是部署盒（虚线框）。正如你所见，外部数据与执行引擎（绿色框）使智能合约能够交互并执行操作。然后数据可以存储在 NEO 分布式账本上。

> “我们希望这个平台可以用于不同的前端场景，比如数字资产钱包、论坛、投票、资料管理和移动应用程序。该平台还具有一个开放 API，可用于与其他系统的集成。”
> 
> —NEO 的创始人达鸿飞，赵 Chen

![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig1_HTML.jpg](img/475651_1_En_7_Fig1_HTML.jpg)

图 7-1

NEO 的虚拟机架构图。图片来源于：docs.neo.org。

### 什么是 NEO 的智慧经济？

NEO 创造了**智慧经济**这个术语，解释了 NEO 的愿景。这个愿景包括用去中心化区块链的力量将你的现有市场从传统经济转变为智慧经济。为了实现这个目标，NEO 将数字资产、数字身份和智能合约整合到其平台上。

### 注意

NEO 的智慧经济愿景旨在改变现有市场的工作方式，从传统经济转变为“智慧经济”，这是通过去中心化区块链的力量实现的。这通过整合数字资产、数字身份和智能合约来实现。

NEO 的智慧经济概念包括整合以下三个组件：

+   **NEO 数字资产**：这些资产包含电子数据并且可以被编程。将数字资产放在区块链上提供了诸如去中心化、信任、可追溯性和透明性等 PoS 区块链的好处。NEO 区块链允许用户注册、交易和转移不同类型的资产。通过数字身份实现物理资产的数字化；然后这些数字资产可以通过验证受到法律保护。对于一个 ICO，注册一个数字资产需要 5000 个气体。然后每年会有 5000 个气体的续费。

+   **NEO 数字身份**：这是个人、组织或其他实体的身份的数字化。一个 NEO 数字身份基于公钥基础设施（PKI）X.509 标准的实现，同时也支持信任网络点对点证书。

+   *NEO 智能合约*：NEO 上的智能合约称为 NeoContracts，它们支持 C#、VB.NET、F#、Java、Kotlin 和 Python 语言。支持这些语言使得在 Visual Studio、Eclipse 和 WebStorm IDE 中拥有复杂的开发、调试和编译优势。NeoVM 是为可扩展性而构建的。

## Setting Up Your Local Environment

As mentioned, NEO supports enterprise-level programming languages such as C#, VB.NET, F# Java, Kotlin, and Python. This selection of programming languages gives NEO an advantage in building NeoContracts because you can utilize the Visual Studio 2017 IDE, which offers enterprise tools for development. In this chapter, I will be using the following .NET tools:

+   *Visual Studio 2017 IDE* : To follow along, install the Visual Studio (VS) Community Edition for Mac.

+   *.NET Core*: 为了跟上进度，请安装.NET Core，以便能够发布 DLL 库文件。

In addition to .NET, you need the following tools:

+   *Xcode 10.1*: 你需要至少 Xcode 10.2 版本的工具和库。

+   *Docker*: Docker 是一个流行的创建容器和集成软件的工具。你将使用 Docker 在你的私有网络中运行一个完整的 NEO 区块链，以在一个轻量级的 Docker 容器中模拟四个共识节点。

+   *neo-compiler*: NEO 编译器是必需的，它可以将你的代码转换为可以在 NEO 区块链上部署的.avm 文件。

+   *neo-cli*: 你将安装并使用 NEO 命令行工具进行钱包、操作和 RPC 调用 NEO API。

Now that you know what needed, let’s get started.

### Xcode 10.2

At the time of writing, you need Xcode with at least version 10.1 for the tools and libraries needed for NEO. The latest Xcode at the time of writing is Xcode 10.2.1.

You can check whether you already have Xcode installed via the command line.> xcodebuild --versionXcode 10.1Build version 10B61

This command will output the version if Xcode is installed. If you need to upgrade or install, visit the Apple developer portal: [`developer.apple.com/download/`](https://developer.apple.com/download/) .

### Install Visual Studio 2017 IDE

Next, download and install the latest version of Visual Studio (VS) Community Edition for Mac. The community edition is free and can be downloaded from the following URL: [`visualstudio.microsoft.com/vs/community/`](https://visualstudio.microsoft.com/vs/community/) .

For future reference, to uninstall a portion or all of VS, follow the instructions here: [`docs.microsoft.com/en-us/visualstudio/mac/uninstall#net-core-script`](https://docs.microsoft.com/en-us/visualstudio/mac/uninstall%2523net-core-script) .

The complete VS 2017 consumes a lot of disk space; however, you don’t need all the packages downloaded. You need only Xamarin Workbooks in order to develop NeoContracts, so only download what’s needed.

在安装过程中，向导会给你提供一个选项，选择要安装的平台和工具。通过点击复选框选择 Xamarin Workbooks，然后点击安装按钮。见图 7-2 ![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig2_HTML.jpg](img/475651_1_En_7_Fig2_HTML.jpg)

图 7-2

Mac 版 Visual Studio Community Edition 安装向导

### 安装.NET Core

你将安装.NET Core，这样你就可以通过命令行发布 DLL 库文件。这将通过 dotnet publish 命令完成。要下载它，请前往 dotnet Microsoft 网站；见图 7-3。

[`dotnet.microsoft.com/download`](https://dotnet.microsoft.com/download)![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig3_HTML.jpg](img/475651_1_En_7_Fig3_HTML.jpg)

图 7-3

下载 Microsoft dotnet core

你将下载两个：构建应用 - SDK v2.2.101 和 运行应用 - 运行时 v2.2.0。

为了确认安装是否成功，运行 dotnet --version 命令。> dotnet --version2.2.101

此命令将输出 dotnet 版本，截至编写时为 2.2.101。

如果 SDK 没有安装，你会收到以下错误信息：是要运行 dotnet SDK 命令吗？请从 http://go.microsoft.com/fwlink/?LinkID=798306&clcid=0x409 安装 dotnet SDK 你可以通过 info 命令输出你的机器信息。> dotnet --info

#### 安装 Docker

接下来，您将安装 Docker。Docker 是创建您将用于创建本地区块链的容器的必要条件。

+   *从这里下载 Docker*：[`download.docker.com/mac/beta/Docker.dmg`](https://download.docker.com/mac/beta/Docker.dmg)

+   *安装说明*：[`runnable.com/docker/install-docker-on-macos`](https://runnable.com/docker/install-docker-on-macos)

一旦下载并安装了 Docker，双击从应用程序菜单中的 Docker，以启动 Docker。你会在电脑上的顶部菜单看到 Docker 图标。你可以在命令行中输入 docker 来验证是否正确安装；它列出了 Docker 命令。> dockerRun docker ps to view containers running to ensure you do not get any error messages.> docker ps 如果 Docker 没有运行，你会收到以下消息：无法连接到 unix:///var/run/docker.sock 的 Docker 守护进程。Docker 守护进程正在运行吗？ just open Docker in case you get this message. Additionally, if your container is not running but it was already created, you can use the -a (all) flag and find the container ID.> docker ps –aList containers 然后当你有了容器 ID，你可以启动那个容器。> docker start [CONTAINER ID]

目前，你不会看到任何容器列表，因为你还没有创建你的容器。

### 下载 NeoCompiler 并生成 neon.dll

要创建您的 NeoContract，您需要生成一个.avm 文件。为此，您需要创建一个 neon.dll 文件，以便生成智能合约。开始之前，您将克隆 neo-编译器到您的桌面，然后生成 neon.dll 文件。> cd ~/Desktop> git clone https://github.com/neo-project/neo-compiler> cd ~/Desktop/neo-compiler/neon/要发布您的自包含.avm 文件，您需要设置一个运行时标识符。您可以将 neon.csproj 运行时标识符设置为正确的操作系统。由于我在此处使用的是 Mac 而不是 PC，因此需要更改 neon.csproj 文件。为了跟随，首先复制原始文件。> cp neon.csproj neon.csproj.backup 我使用的是 vim，但您可以使用您喜欢的任何编辑器。> vim neon.csproj

文件打开后，请替换以下配置，设置目标框架。

### 注意

您可以在此处与我项目中的输出和设置进行比较：chapter7/NEO/neo-compiler/neon/。那里也有 neon.csproj。

<项目 Sdk="Microsoft.NET.Sdk">  <属性组>    <版权>2016-2017 The Neo Project</版权>    <程序集标题>Neo.Compiler.MSIL</程序集标题>    <版本>2.3.1.1</版本>    <作者>The Neo Project</作者>    <目标框架>netcoreapp2.0</目标框架>    <平台目标>anycpu</平台目标>    <程序集名称>neon</程序集名称>    <输出类型>Exe</输出类型>    <包 ID>Neo.Compiler.MSIL</包 ID>    <运行时标识符>osx.10.12-x64</运行时标识符>    <根命名空间>Neo.Compiler</根命名空间>    <公司>The Neo Project</公司>    <产品>Neo.Compiler.MSIL</产品>    <描述>Neo.Compiler.MSIL</描述>  </属性组>  <属性组 Condition="'$(Configuration)|$(Platform)'=='Release|AnyCPU'">    <定义常量>RELEASE;NETCOREAPP1_0</定义常量>    <调试类型>无</调试类型>    <调试符号>False</调试符号>    <允许不安全块>true</允许不安全块>  </属性组>  <属性组 Condition="'$(Configuration)|$(Platform)'=='Debug|AnyCPU'">    <允许不安全块>true</允许不安全块>  </属性组>  <项目组>    <包引用 Include="Mono.Cecil" Version="0.10.0" />    <包引用 Include="Neo.VM" Version="2.3.0" />  </项目组></项目>现在通过传递运行时标识符 osx.10.11-x64 设置发布指向。> dotnet publish -r osx.10.11-x64 编译器在以下位置创建了您的 neon.dll 文件：bin/Debug/netcoreapp2.0/osx.10.11-x64/publish/neon.dll 请参阅图 7-4 的输出。![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig4_HTML.jpg](img/475651_1_En_7_Fig4_HTML.jpg)

图 7-4

为目标 osx.10.11-x64 编译 neon.dll

### 使用 neo-cli 生成 NEO 节点

接下来，您想创建一个完整的 NEO 节点。要生成一个完整节点，有两个完整节点选项。

+   **neo-gui**：这既可以被开发者也可以被 NEO 用户使用。它可以用于进行基本用户客户端操作，如管理钱包，也可以发布智能合约。它有一个视觉用户界面。然而，在撰写本文时，它只在 Windows 上运行。

+   **neo-cli**：这为基本钱包操作提供了外部 API。它还有助于其他节点与网络保持一致性并生成新区块。

在此例中，我正在 Mac 上安装，因此你将使用 neo-cli 通过命令行管理你的钱包。然而，你知道你可以安装 neo-gui 并创建一个虚拟 PC 也是件好事。

#### neo-cli

对于 neo-cli，你需要安装 LevelDB 包，因为它是一个依赖关系。正如你回忆起来，你已经在第三章通过 Homebrew 安装了 LevelDB。如果你之前没有安装 LevelDB，以下是命令再次：> brew install leveldb 或者，你可以检查你是否已经安装了它并进行升级。> brew upgrade leveldb 接下来，将 neo-cli 克隆到你的桌面。> cd ~/Desktop> git clone https://github.com/neo-project/neo-cli 现在，你可以使用 dotnet 从你下载的源代码中发布 neo-cli。> cd neo-cli> dotnet restore> dotnet publish -c Release.dll 文件应该在 Release 文件夹中创建；请参阅图 7-5 以查看输出。![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig5_HTML.jpg](img/475651_1_En_7_Fig5_HTML.jpg)

图 7-5

构建 neo-cli DLL

### 注意

你可以在这里与我项目的输出和设置进行比较：chapter7/NEO/neo-cli。

要运行 .dll 文件，你使用 dotnet 和 DLL 文件的路径，这将启动 NEO 命令行终端。> cd bin/Release/netcoreapp2.1/> dotnet neo-cli.dll.

neo-cli 也支持插件。例如，你可以使用应用程序日志启用 neo-cli 的日志，或者你可以通过 RPC 安全改进 RPC 节点的安全性。可以在以下网址找到插件列表：[`github.com/neo-project/neo-plugins`](https://github.com/neo-project/neo-plugins) 。

## 创建一个本地 NEO 私有测试网

你可以在公共测试网上像其他区块链一样运行你的 NeoContracts；然而，运行你自己的私有测试网要好得多，因为你拥有完全控制权。私有测试网可以部署在云上，但你需要为服务提供商支付费用，所以最好在本地机器上设置你的测试网。

正如文档所示，NEO 的工具主要是为 PC 用户开发的。然而，由于 City of Zion 社区（CoZ，[`github.com/CityOfZion`](https://github.com/CityOfZion) ）开发的工具，任何支持 Docker 和 Python 的平台都可以运行私有链。

运行本地 NEO 私有测试网所需采取的步骤如下：

1.  1.

    **安装 neo-python**：这可以使你运行一个完整的 NEO 节点并与其他区块链互动。

1.  2.

    创建 `neo-privatenet-docker`：这允许你在一个轻量级的 Docker 容器中运行整个 NEO 区块链，并带有四个共识节点。

1.  3.

    创建一个 NEO 钱包：这连接到私有网络并创建一个钱包。

1.  4.

    领取：这初始为 100,000,000 NEO。

1.  5.

    引导测试网络：这同步*网络*。

### Python 3.6

neo-python 需要 Python 3.6 或更高版本。Mac 自带 Python，并且你可以通过 --version 命令验证你是否安装了 python3。> python3 --versionPython 3.6.x 如果你正在运行 Python 的旧版本并且需要安装/重新安装 Python，请按照以下步骤操作：> brew unlink python 接下来，使用 Brew 安装 Python。> brew install --ignore-dependencies https://raw.githubusercontent.com/Homebrew/homebrew-core/f2a764ef944b1080be64bd88dca9a1d80130c558/Formula/python.rb 现在切换 Python 版本。> brew switch python 3.7.0> brew switch python 3.6.5_1 如果你没有安装 pip，运行这个命令：> curl -O https://bootstrap.pypa.io/get-pip.py> sudo python get-pip.py> pip

### 安装 neo-python

接下来，从 City of Zion 克隆 neo-python 并检出开发分支。> cd ~/Desktop> git clone https://github.com/CityOfZion/neo-python.git> cd neo-python> git checkout development 你可以使用 Python 3.6 创建一个虚拟环境，然后运行激活脚本。> python3.6 -m venv venv> source venv/bin/activate 确保你通过运行这个命令拥有最新版本的 pip：(venv)> pip install --upgrade pip 现在你可以以可编辑的形式安装包。(venv)> pip install -e.你可以将你的输出与我的一致进行比较；对于你迄今为止采取的步骤，请参见图 7-6。![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig6_HTML.jpg](img/475651_1_En_7_Fig6_HTML.jpg)

图 7-6

neo-python 安装输出

为了确认安装是否成功，运行 --version 命令。在撰写本文时，它输出的版本为 0.8.3。> np-prompt --versionneo-python v0.8.3-dev 现在你可以使用 np-prompt 命令打开一个 NEO bash。要退出 bash，运行退出命令。> np-promptneo>exit

### 安装 neo-privatenet-docker

你已经安装了 Docker，所以现在你可以创建一个 Docker 容器，这将创建四个 NEO 节点来创建一个私有的测试网络。继续在你的桌面上安装 Docker 容器并构建文件，如下所示：> cd ~/Desktop> git clone https://github.com/CityOfZion/neo-privatenet-docker.git> cd neo-privatenet-docker> ./docker_build.sh 在镜像构建完成后，你可以像这样启动私有网络：> ./docker_build.shSuccessfully built #build number

### 注意

如果 Docker 需要重新启动或没有运行，运行以下命令：

> ./docker_run.sh

### 启动网络并领取初始 NEO 和 GAS

接下来，您将启动您的私有网络，创建您的钱包，并认领初始的 NEO 和 40 个 GAS。这通过运行 docker_run_and_create_wallet.sh 脚本完成。您可以在图 7-7 中看到输出。> ./docker_run_and_create_wallet.sh![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig7_HTML.jpg](img/475651_1_En_7_Fig7_HTML.jpg)

图 7-7

`docker_run_and_create_wallet`脚本输出

一旦过程完成，您可以获得创建的两个文件的确认（见图 7-7）。

+   `neo-privnet.wallet`：此文件是一个钱包，您可以用 neo-python 使用。

+   `neo-privnet.wif`：此文件是一个 WIF 私钥，您可以在其他客户端（如 neo-gui）中导入。

这些文件为您提供了访问包含您私有网络的 NEO 和 GAS 的钱包的权限。脚本自动为您认领了 NEO 和 GAS。

您可以检查 Docker，并看到名为 neo-privnet 的容器正在运行，如图 7-8 所示。> docker ps![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig8_HTML.jpg](img/475651_1_En_7_Fig8_HTML.jpg)

图 7-8

新私有网络 Docker 容器正在运行

### 引导测试网络

现在您已经有了一个私有测试网络在运行，您需要引导测试网络区块链数据库。这同步了网络，通过运行 np-bootstrap 完成。这可能需要一点时间；完成后，您将得到确认。> np-bootstrap -nconfirmSuccessfully downloaded bootstrap chain!

注意您使用了–n 标志来获取数据库通知。

### 启动 NEO Bash

现在您已经有了四个节点的私有测试网络容器在运行，并且您引导了您的测试网络数据库，您可以通过调用 prompt.py 命令来启动一个 neo-cli bash。> cd ~/Desktop/neo-python/neo/bin> python3.6 prompt.py –p

图 7-9

通过状态命令获取区块链信息

neo-cli 通过 NEO API 提供对许多 RPC 调用的访问；然而，必须打开钱包才能运行这些命令。您可以使用钱包命令和文件位置打开您的钱包。此命令将要求输入钱包的密码。对于密码，使用 coz.neo> 钱包打开 ~/Desktop/neo-privatenet-docker/neo-privnet.wallet 密码：coz

图 7-10

新私有网络钱包显示已认领的硬币

要关闭钱包并退出 bash，请使用钱包关闭命令并退出。neo> 钱包关闭 neo> 退出

你成功创建了一个运行在测试网上的私有的 NEO 区块链，并且声称了 1 亿 NEO 和 40.0 NeoGas，这些你可以用来进行开发。

### 安装过程中可能遇到的问题

NEO 有时候感觉像是在追一个移动的目标。事实上，很可能在你利用这本书中的说明时，代码不会像预期那样工作，因为 NEO 发生了变化。此外，在安装过程中，可能会遇到一些潜在的问题。我建议你在这里检查最新的信息：

[`github.com/CityOfZion/neo-python#getting-started`](https://github.com/CityOfZion/neo-python%2523getting-started)

#### 清理数据库

如果你需要清理 neo-python 数据库以重新引导和同步，运行以下命令：> rm -rf ~/.neopython/Chains/privnet*

#### b’Corruption Message

如果你收到一个“b’Corruption: corrupted compressed block contents”消息，你需要重新安装 LevelDB。> brew reinstall leveldb

#### 重启 Docker

知道如何重启 Docker 是有好处的，以防你需要重启计算机、升级 Docker 版本或升级容器文件。要重启 Docker，从顶部菜单选择 Docker，然后点击重启（见图 7-11）。

状态被删除（整个“旧”区块链将会消失），你也应该从 neo-python 中删除 Chains/privnet 和任何你创建的 privnet 钱包。> rm ~/Desktop/neo-privatenet-docker/*.wallet> rm ~/Desktop/neo-privatenet-docker/*.wif> rm -rf ~/.neopython/Chains/privnet*> docker ps![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig11_HTML.jpg](img/475651_1_En_7_Fig11_HTML.jpg)

Figure 7-11

Docker 顶部菜单图标重启按钮

### NEO “Hello, World”

你已经在你机器上设置好了本地私有测试网环境和 NEO 工具，所以现在你准备好了进行你的 NeoContract 项目的开发。你可以在不同的语言中开发，过程是相似的。我会向你展示 C#以及 Python 的代码。我保持代码简单，是一个工作的“Hello, World”示例，但一旦你能够达到这个阶段，你可以尝试 NEO 提供的不同功能。按照以下步骤创建并发布你的代码：

1.  1.

    *构建 NeoContract 框架*：生成一个 Neo.SmartContract.Framework.dll 文件。

1.  2.

    *创建一个 NEO“Hello, World”项目*：创建你的#C 合约项目。

1.  3.

    *用 C#编写一个 NEO“Hello, World”智能合约*：用 C#编写你的最小示例。

1.  4.

    *用 C#编写一个 NEO“Hello, World”智能合约*：用 C#编写你的最小示例。

1.  5.

    *发布*：将你的合约发布到你的私有测试网链。

### 构建 NeoContract 框架：Neo.SmartContract.Framework.dll

第一步是创建一个文件，该文件包含你需要在你的 NeoContract 中包含的 NeoContract 框架代码，以访问 NEO 功能。

要构建你的 NeoContract，你将下载并安装 NEO 开发包。你将这些工具放在你的桌面上以便于访问。请注意，你总是可以把文件移到一个更好的位置。导航到桌面并克隆 neo-devpack-dotnet 项目。> cd ~/Desktop> git clone https://github.com/neo-project/neo-devpack-dotnet 接下来，通过双击它或运行终端打开命令来运行 neo-devpack-dotnet.sln 文件。> open neo-devpack-dotnet.sln

VS 打开，你应该预期会得到三个错误信息。点击确定忽略这些信息，因为这些错误不会影响你的项目构建。

在左侧窗口，你可以看到解决方案标签，如图 7-12 所示。如果它没有展开，请展开“neo-devpack-dotnet (master)”。

然后，右键点击 Neo.Smartcontract.Framework 并选择构建 Neo.Smartcontract.Framework。见图 7-12。![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig12_HTML.jpg](img/475651_1_En_7_Fig12_HTML.jpg)

图 7-12

构建 Neo.SmartContract.Framework 项目

一旦构建完成，你将在 VS 输出的顶部中间窗口得到一个“构建成功”的消息。你也可以在这里找到 Neo.Smartcontract.Framework.dll 文件：> cat ~/Desktop/neo-devpack-dotnet/Neo.SmartContract.Framework/bin/Debug/netstandard1.6/Neo.SmartContract.Framework.dll

.dll 文件是 .NET 中间语言（IL）文件，你将把它包括在你的库中以访问 NeoContract 框架代码。由于 NeoVM 和 C# IL 文件之间的差异，Neo.SmartContract.Framework 不支持 C# 的全部功能。

### 创建一个 NEO “Hello, World” 项目

既然 Neo.Smartcontract.Framework.dll 文件已经准备好使用，你可以创建你的项目并把 NEO 框架作为依赖包含进来。

开始时，打开 Visual Studio。选择文件 ➤ 新解决方案... ➤ 新项目向导打开。在左侧菜单中，选择库 ➤ .NET 标准库。然后，选择 .NET 标准 2.0 作为 .NET Core 版本，然后点击下一步。见图 7-13。![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig13_HTML.jpg](img/475651_1_En_7_Fig13_HTML.jpg)

图 7-13

新项目模板向导

配置向导在新的项目窗口打开。将项目命名为 **hello_contract**，保留默认设置，然后点击创建按钮。见图 7-14。![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig14_HTML.jpg](img/475651_1_En_7_Fig14_HTML.jpg)

图 7-14

VS 创建新项目向导

一旦项目创建完成，你需要把 Neo.Smartcontract.Framework.dll 文件作为依赖项附上。为此，右键点击解决方案中的 Dependencies 文件夹，然后点击编辑引用。见图 7-15。![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig15_HTML.jpg](img/475651_1_En_7_Fig16_HTML.jpg)

图 7-16

VC 编辑引用.NET 程序集

### 使用 C#编写 NEO“Hello, World”智能合约

在本节中，你将使用 C#在.NET 中开发你的 NEO“Hello, World”智能合约。NeoVM 更紧凑；你可以将有限的 C#/dotnet 功能编译到你的 AVM 文件中。你可以在这里查看可用于开发的特性列表：[`docs.neo.org/en-us/sc/quickstart/limitation.html`](https://docs.neo.org/en-us/sc/quickstart/limitation.html)。

示例将使用 NEO 示例中提供的“Hello, World”示例。

编写代码后，从顶部菜单选择构建，然后构建全部（或命令+B）以编译 Class1.cs 代码。

.dll 库文件是在 bin/Debug/netstandard2.0/目录下创建的。你将使用这个.dll 文件与 neo-compiler 一起使用，并将.dll 文件转换为 AVM 文件。在编译 DLL 文件后，hello_contract.dll 文件在这里创建：

~/Projects/hello_contract/hello_contract/obj/Debug/netstandard2.0/hello_contract.dll

### 注意

NeoContract 框架生成了 NeoVM 字节码。代码以 AVM 文件格式保存。*.avm 文件随后可以部署在 NEO 区块链上。

### 使用 Python 编写 NEO“Hello, World”智能合约

在 C#中，你可以生成一些简约的 Python 代码来打印“Hello, World.”。你可以使用 Eclipse IDE（[`www.eclipse.org/ide/`](https://www.eclipse.org/ide/)）或任何你选择的编辑器。这些说明将使用 vim。在~/Desktop/smartContracts/下创建一个名为 sample1.py 的文件。```vim ~/Desktop/smartContracts/sample1.py``` 输入以下代码来打印“Hello World.”

要在 vim 中关闭并保存文件，输入:wq。

### 编译你的智能合约到.avm

如今你已经有了两个名为 sample1.py 和 hello_contract.dll 的文件，下一步是编译这些文件成为你将在 NEO 区块链上部署的 NEO 虚拟机文件（.avm）。

首先，我们来编译 hello_contract.dll 文件。将目录更改为 DLL 文件所在的目录。`cd ~/Desktop/neo-compiler/neon/bin/Debug/netcoreapp2.0/osx.10.11-x64/publish`，然后复制 Neo.SmartContract.Framework.dll 到 hello_contract 项目目录下的 obj/Debug/netstandard2.0 文件夹中。`cp ~/Projects/hello_contract/hello_contract/bin/Debug/netstandard2.0/Neo.SmartContract.Framework.dll ~/Projects/hello_contract/hello_contract/obj/Debug/netstandard2.0`现在，你可以使用.NET Core 工具将你的 DLL 文件发布为 AVM 文件，如图 7-17 所示。`dotnet neon.dll ~/Projects/hello_contract/hello_contract/obj/Debug/netstandard2.0/hello_contract.dll`你可以看到输出结果，如图 7-17 所示。![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig17_HTML.jpg](img/475651_1_En_7_Fig17_HTML.jpg)

图 7-17

将 DLL 转换为 AVM 字节码

你可以使用 ls 命令查看 AVM 字节码文件。`.> ls ~/Projects/hello_contract/hello_contract/obj/Debug/netstandard2.0/∗.avm`hello_contract.avm 类似地，你也可以将 Python sample1.py 文件编译为 AVM。在 NEO bash 中，使用 sc build 命令。`> cd ~/Desktop/neo-python/neo/bin`，然后运行`> python3.6 prompt.py –p`，接着编译`~/Desktop/smartContracts/sample1.py`文件。`neo> sc build ~/Desktop/smartContracts/sample1.py`输出已保存至`~/Desktop/smartContracts/sample1.avm`。

## 在私有测试网上发布智能合约

下一步是将你的 AVM 文件部署到 NEO 私有测试网络链。你不需要记住所有选项。你可以带有帮助标志调用命令以查看选项。`neo> sc deploy help`部署智能合约（.avm）文件到区块链用法：`sc deploy {path} {storage} {dynamic_invoke} {payable} {params} (returntype)`path - 智能合约的 Python (.py)文件路径 storage - 布尔输入，确定智能合约是否需要存储 dynamic_invoke - 布尔输入，确定智能合约是否需要动态调用 payable - 布尔输入，确定智能合约是否可支付 params - 智能合约的输入参数类型 returntype - （可选）智能合约输出的返回类型关于参数类型更多信息，请参见`https://neo-python.readthedocs.io/en/latest/data-types.html#contractparametertypes`接下来设置 storage、dynamic_invoke 和 payable 为 false，将 params 和 returntype 设置为 01，如图 7-18 所示。`neo> sc deploy ~/Desktop/smartContracts/sample1.avm False False False 01 01`![../images/475651_1_En_7_Chapter/475651_1_En_7_Fig18_HTML.jpg](img/475651_1_En_7_Fig18_HTML.jpg)

图 7-18

在私有测试网络链上发布 AVM 文件

NEO 要求提供一个合约名称；我们称这个合约为 helloWorld。保留版本、作者、电子邮件和描述字段空白，并输入你的钱包密码以支付合约费用。

## 发布到主网

要在大网络上发布，你可以使用与测试网络相同的流程；只需引导到主网络即可。

### 引导到主网络

为了引导到主网区块链，只需运行 np-bootstrap 带-m 标志（它接近 10 GB）。你还可以在主网上使用通知数据库。> np-prompt –m -n

### 安装 neo-gui 客户端

一个更简单的方法是通过 neo-gui 设置并发布 NeoContract。你需要为 PC 设置一个虚拟机，但部署 AVM 文件是轻而易举的。按照以下说明操作：

[`docs.neo.org/en-us/sc/quickstart/deploy-invoke.html`](https://docs.neo.org/en-us/sc/quickstart/deploy-invoke.html)

[`docs.neo.org/en-us/node/gui/install.html`](https://docs.neo.org/en-us/node/gui/install.html)

## 以太坊 vs. EOS vs. NEO：智能合约开发者视角对决

到目前为止，我已经介绍了三个用于开发智能合约的主要区块链，很难不比较它们。然而，在比较这三个区块链时，需要考虑许多因素。此外，在撰写本文时，您可以从超过 40 个区块链项目中选择用于智能合约的部署。每个项目都有优点和缺点，而且超出本书的范围涵盖它们全部。相反，我将重点关注特定的标准，以尝试帮助您了解在选择我迄今为止介绍的三个平台之一时应考虑哪些因素。

有一个组织试图对这些不同的区块链进行评级；它被称为中国信息产业发展中心（CCID）。CCID 利用来自中国最著名教育机构，包括清华大学和北京大学的教授和研究人员的贡献，考虑特性、采用率和其他许多指标来对每个区块链进行排名。然而，这些评级经常变化，你应该在网站上查看最新的区块链评级：[`special.ccidnet.com/pub-bc-eval/index.shtml`](http://special.ccidnet.com/pub-bc-eval/index.shtml)。注意，在撰写本文时，EOS 和 Ethereum 已经连续第四次在 CCID 列表上保持主导地位。

此外，确定要使用哪个区块链来发布智能合约应考虑更多因素，例如您的团队能力、资金、所需交易数量、所需账户数量、钱包、交易所等。

确定区块链健康的一个重要指标是用户和开发者的采用。您可以通过检查这些网站来找到不同智能合约平台的 dapps 当前数量：

+   *EOS*: [`dappradar.com/eos-dapps`](https://dappradar.com/eos-dapps)

+   *Ethereum*: [`dappradar.com/dapps`](https://dappradar.com/dapps)

+   *NEO*: [`ndapp.org/`](http://ndapp.org/)

查看 dapps 列表时，请记住，尽管在撰写本文时 dappradar.com 上有 6050 个 dapps，但只有 106938 个用户，这表明很少有 dapps 被使用，大规模采用还没有到来。

另外，请注意，本次比较是基于编写时的数据，并且基于我的观点。在选择适合您智能合约需求的理想区块链之前，您应该自己进行研究和尽职调查。表 7-1 提供了比较。表 7-1

[以太坊](https://wiki.example.org/ethereum) vs. [EOS](https://wiki.example.org/eos) vs. [NEO](https://wiki.example.org/neo) 智能合约比较

| 类别 | 以太坊 | EOS | NEO |
| --- | --- | --- | --- |
| 采用率 | 目前占据首位 | 采用率稳步增长 | 三者中采用率最低 |
| CCID 排名 | 第 2 名 | 第 1 名 | 第 5 名 |
| 共识机制 | PoW | DPoS | dBFT |
| 每秒交易数 | 15 | 数百万 | 每秒 10,000 笔交易 |
| Dapp 部署成本 | 最低 32,000 gas 费用，加上源代码每字节 200 gas | 约 120 EOS | 固定成本 100 至 1,000 gas；ICO 注册数字资产需要 5,000 gas，每年更新费用 5,000 gas |
| 交易成本 | 0.05 至 3.5 美元 | 0 美元（然而，创建新账户的成本为每个账户 1 至 4 美元，由应用开发者支付） | 初始 10 gas 执行免费，系统调用和指令费用（请参阅白皮书） |
| 可扩展性 | 否；等待硬分叉 | 是 | 是 |
| 开发工具 | 项目和社区成熟的发展工具，包括开发框架、IDEs、通信和测试工具 | 开发工具可以升级；调试仍然使用原始调试 | 成熟的发展工具 |
| 文档 | 项目与社区都提供了良好的文档 | Developers.EOS.IO 文档和社区教程没有跟上 EOS.IO GitHub 的变化；许多 GitHub 问题涉及安装 | 项目文档（[`docs.neo.org`](http://docs.neo.org)）和社区教程 |
| 社区支持 | 以太坊社区基金会（ECF）获得组织支持：微软、英特尔、亚马逊、摩根大通，甚至有政府参与 | 承诺投入 10 亿美元资金，专注于 EOS 生态系统的增长 | 已经举办并支持了超过 100 个社区活动 |
| 开发语言 | Solidity、Bamboo、Vyper、LLL、Flint | C、C++ | C#、VB.NET、F#、Java、Kotlin 和 Python；未来计划支持更多语言 |
| 市值 | 14,068,553,166 美元 | 2,341,702,969 美元 | 488,507,580 美元 |
| Dapp 数量 | 1,324 个 | 226 个 | 不到 100 个 |
| 钱包 | 桌面和硬件钱包，比 EOS 和 NEO 有更多选择 | 桌面和硬件钱包 | 桌面和硬件钱包 |
| 大型交易所支持 | 在所有主要交易所上市 | 尚未在许多主要交易所上市，如 Coinbase | 尚未在许多主要交易所上市，如 Coinbase |
| 图灵完备 | 是 | 否 | 否 |

以下总结是以太坊、EOS.IO 和 NEO 区块链平台的优势和劣势：

+   以太坊最大的优点是它是第一个也是最受欢迎的智能合约平台，拥有最多的开发者、第三方工具、支持、文档和支持社区。最大的缺点是使用 PoW 的以太坊可扩展性问题；在撰写本文时，有一个硬分叉正在进行中，旨在解决这一缺点并将以太坊转移到 PoS。另一个缺点是源代码每字节 200 气体的成本；如果你的代码没有优化，这会很昂贵，尤其是因为你需要不断重新发布你的代码。最后，对不太流行的编程语言（如 Solidity）的支持不如理想。

+   EOS 的优势在于其可扩展性以及在不改变的情况下运行数百万笔交易的能力，以及使用 WASM 更快地执行代码。EOS 支持 C 和 C++，实际编写的区块链使用 C++使其具有优势，因为与 Solidity 相比，C 有更多的开发者基础。然而，在采用方面，EOS 还有很长的路要走，提供 10 亿美元的资金对公司和个人来说可能是有用的，有合适想法的话。它的高评分和出色的功能还不足以取代以太坊在其声称的主导地位。时间会告诉我们。

+   NEO 支持主要的编程语言（C#，VB.NET，Java 和 Python），这给了它一个很大的优势，因为大量的开发者可以编写较小的学习曲线。此外，合同的高效和低成本计算执行是一个优势；然而，NEO 是这三个平台中社区支持最小的，以及每年注册数字资产所需的硬性 5,000 NeoGas 可能会让许多潜在项目望而却步。

## 从这里去哪里

尝试这些资源：

+   阅读 NEO 文档：[`docs.neo.org`](http://docs.neo.org) 。该网站包括样本 NeoContracts 教程、创建 NEO 节点、NEO 实用程序、白皮书等内容。

+   访问[`neo.org/client`](https://neo.org/client)以查找来自第三方的 NEO 钱包。

+   对于调试，请查看 Neunity.Adapter 或 Neo-Debugger 以编写测试用例并在 IDE 中运行源代码：[`github.com/CityOfZion/neo-debugger-tools/releases`](https://github.com/CityOfZion/neo-debugger-tools/releases) 。

+   创建额外的 NeoContracts 并包括 SmartContractEvent，它通过 neo.EventHub 分发；订阅并测试你的合同。

## 总结

在本章中，我介绍了 NEO 区块链和 NEOContracts。你查看了 NEO 的高级区块链架构并学习了 NEO 的智慧经济。你设置了你的本地环境并升级了 Xcode，安装了 Visual Studio 2017 IDE，并安装了.NET Core。

你已经安装了 Docker，所以现在可以创建容器，并且你下载了 neo-compiler 并生成了 neon.dll。最后，你构建了 neo-cli，所以你可以管理你的钱包和其他 RPC 操作。

接下来，你通过安装 neo-python 和 neo-privatenet-docker 创建了一个本地的 NEO 私有测试网。你引导了测试网并启动了 NEO bash，然后能够启动你的网络并领取 NEO 和 GAS。

此外，我涵盖了在安装你的 NEO 工具过程中可能遇到的问题。

接下来，你创建了两个“Hello, World”项目，一个用 C#，一个用 Python，并能够将这些项目编译成 NEO 虚拟机的字节码（AVM）文件。你将这些文件学会了如何发布到 NEO 测试网区块链上，以及 NEO 主网上。

最后，我比较了以太坊、EOS 和 NEO，以帮助你更好地理解这些平台之间的差异，以及在选择用于你的智能合约的平台时应考虑哪些标准。
