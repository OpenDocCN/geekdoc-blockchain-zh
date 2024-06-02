© Elad Elrom 2019 Elad Elrom The Blockchain Developer [`doi.org/10.1007/978-1-4842-4847-8_8`](https://doi.org/10.1007/978-1-4842-4847-8_8)

# 8. 超账本

Elad Elrom^(1 )（1）纽约，纽约，美国

在之前的章节中，我介绍了专注于加密货币的区块链技术，实际上，到目前为止我所涵盖的每个项目都包含了自己的货币。超账本不同；它没有附加的货币，尽管您需要时可以创建一个硬币。相反，超账本旨在成为一个开源平台，旨在利用区块链满足业务需求。

超账本始于 2015 年，由数字资产公司和 IBM 发起的一个黑客马拉松（现在称为超账本 Fabric）开源区块链项目，并扩展为多个可插拔模块的集合，整个项目被称为超账本，旨在提高区块链的性能和可靠性，以便您可以组装模块创建您独特的平台以满足您的业务需求。

### 注意

超账本项目是一个伞形战略模块化架构，由一系列用于为企业创建自定义区块链解决方案的可插拔组件集合构成。超账本架构旨在提供可扩展性、性能、机密性、弹性和灵活性。请注意，如果您访问超账本的文档，您经常会看到“分布式账本技术”（DLT）这个术语；这个术语与“区块链”是同义的。

## 超账本概览

模块化架构允许您调整诸如区块链的共识机制之类的设置，以及管理存储、为身份设置服务、为设置的身份设置权限以及创建智能合约（在超账本 Fabric 中，智能合约被称为*链码*）。就编程语言而言，超账本的链码是用 Go（Golang）编写的；然而，您可以使用 Hyperledger Composer 工具使用 JavaScript。链码随后可用于实现和自动化业务逻辑。

超账本项目的管理团队由十名成员组成，写作时项目的执行总监是 Brian Behlendorf。此外，根据 developer.ibm.com 的数据，有来自 27 个组织的 159 名工程师为超账本 Fabric v1.0 做出了贡献。

> *“* *超账本* *是一个开源开发项目，旨在造福基于超账本的解决方案提供商和用户生态系统。它专注于将在各种工业部门工作的区块链相关用例。”*
> 
> —Brian Behlendorf（超账本执行总监）

超账本由 Linux 基金会托管，在采用方面，它得到了 IBM、英特尔和 SAP 等大型企业公司的支持，同时也被甲骨文、埃森哲、美国房地产经纪人协会、德意志交易所集团、索尼全球教育等实施。

Hyperledger 共识机制允许网络节点在无操作（无共识）机制和名为实用拜占庭容错（PBFT）的协议之间进行选择。PBFT 共识通过赋予节点完全控制权，使两个或更多节点达成一致。这排除了网络上其他节点强制一个区块，这可以防止潜在的双重花费攻击，正如你从 PoW 的 51%潜在挖矿攻击中看到的那样。Hyperledger 控制着共识机制，你可以限制对交易的访问。这导致了性能和可伸缩性的提高，因为需要达成共识的节点更少。此外，PBFT 为网络提供了隐私性，这对于企业来说比其他区块链提供的完全透明性更适合。

为了让你了解 Hyperledger 的灵活性，你可以使用动态共识，并启用所谓的*热交换*，即在网络运行时更换共识算法（由 Hyperledger Sawtooth 完成）。

专注于加密货币的区块链通常提供交易和网络数据的透明度，因为它们处理资金，并且大多数情况下成员是不可信的。然而，这也限制了灵活性，以及你可以修改网络和控制的程度，因为你受到一组规则的限制。Hyperledger 没有自己的货币支持，提供更加细粒度的控制。

Hyperledger 项目建立在基本功能之上，采用原生风味，旨在使开发者尽可能地进行定制，从区块链的共识机制到 Web 界面身份的权限，向成员提供有限的数据。

这种模块化架构方法允许开发者创建特定且定制的个性化区块链，以满足确切的企业需求。Hyperledger 包含以下主要的开源框架和工具。

+   Hyperledger 框架：

    +   **Hyperledger Fabric（由 IBM 贡献）**：这是一个具有 Node.js、Java 和 GoLang SDK 的权限型区块链基础设施。Hyperledger Fabric 是 Hyperledger 的心脏，支持 GoLang 和 JavaScript（利用 Hyperledger Composer 或原生支持）的链码。区块链基于背书者/排序者架构。关于这一点，你将在本章后面了解更多。

    +   **Hyperledger Burrow**：这是一个按照规格构建的以太坊虚拟机。

    +   **Hyperledger Indy**：想想独立。这是一个在分布式账本上运行独立身份的工具和库。

    +   **Hyperledger Iroha**：重点是移动应用；代码基于 Hyperledger Fabric。

    +   **Hyperledger Grid**：这是一个基于分布式账本的供应链解决方案。该框架封装了数据类型、模型和智能合约的 Hyperledger 实现，以及展示创建供应链业务解决方案的实际方法。

    +   *Hyperledger Sawtooth（由英特尔贡献）*：这个框架包括动态共识，并允许在运行网络中热插拔共识算法。这是一个更传统的区块链架构。

+   Hyperledger 工具：

    +   *Hyperledger Caliper*：这是一个区块链基准测试工具。

    +   *Hyperledger Cello*：这是一个用于创建、管理和终止区块链的按需区块链模块工具包。

    +   *Hyperledger Composer*：这个工具有用于与 Hyperledger Fabric 合作构建针对企业区块链应用的链码和区块链功能的协作特性。

    +   *Hyperledger Explorer*：这是一个用于查看、调用、部署和查询区块、交易和网络数据的模块。

    +   *Hyperledger URSA*：这是一个共享密码学库；它包括诸如不同签名方案（基本密码学库）实现和 Z-mix，零知识证明（ [`github.com/hyperledger-labs/z-mix`](https://github.com/hyperledger-labs/z-mix) ）等共享项目。

    +   *Hyperledger Quilt/Interledger.js*：这是一个 Interledger 协议（ILP），意味着账本之间的原子交换。该支付协议允许在分布式和非分布式账本之间转移资产（价值）。有两个实现：Java 的一个叫 Quilt，JavaScript 的一个叫 Interledger.js。

可以构建一个 Hyperledger 项目，使交易在需要时既透明又保密。例如，考虑以下业务需求：一家航空公司想要将座位卖给另一家商业公司，比如说 Expedia。航空公司业务需求是创建自己的区块链以跟踪库存、创建交易、设定价格并保持数据保密。航空公司可以利用区块链，但它不需要加密货币，也不想公开所有数据。航空公司可以利用 Hyperledger，建立一个私有的权限网络，不将数据暴露给全世界，正如你会在公共账本上做的那样。

航空公司可以设置特殊的权限，通过发布具有有限访问权限的加密密钥，然后只将这些加密密钥交给特定的各方。例如，只有一个组织，比如说 Expedia，能够查看与 Expedia 相关的交易、座位定价和航班信息，而其他身份，如实际客户，只能查看与他们的账户和航班信息相关的预订信息。

财务团队可以持有加密密钥，提供更多数据，如利润和损失、燃油成本和其他内部使用所需的数据。这对企业有益，因为它们可以在账本上运行数据，而不是中央数据库，这更容易受到黑客攻击。

正如你所见，Hyperledger 是一个涵盖六个框架以及五个工具的大型项目。在一个章节中涵盖所有内容是不切实际的；实际上，这很容易占据一整本书。在本章中，我将为你提供一个良好的基础，帮助你理解 Hyperledger 的基本知识，然后你可以继续使用其他平台和工具自行实验。在本章中，你将重点关注 Hyperledger Fabric，因为它是最受欢迎的 Hyperledger 平台。

## 理解 Hyperledger Fabric

如我所说，Hyperledger Fabric 是一个开源框架实现，旨在为私有和基于权限的商业网络服务。

在本章中，你将创建私有网络权限身份，然后创建链码来实现特定的业务逻辑。

Hyperledger Fabric 被设计为 Hyperledger 的基础框架，你可以根据业务需求使用 Hyperledger 的模块化架构添加特定模块。Hyperledger Fabric 网络由以下组件组成：

+   资产: 资产是代表价值的键值对。价值可以是任何东西，比如文件、股票或加密货币代币。每个资产都持有状态和所有权。

+   共享账本: 共享账本持有账本的状态以及资产的状态。这个账本被称为*世界状态*。共享账本还持有区块链的副本，通过记录交易历史来存储资产的所有权。

+   智能合约（链码）: Hyperledger Fabric 将智能合约称为*链码*，可以用 Go（GoLang）或 JavaScript（Node.js）编程。链码可以与共享账本、资产和交易进行交互。这里没有新内容；你在其他区块链中已经看到了这个。链码包含业务逻辑，并可以设置背书策略。

### 注意

在 Hyperledger Fabric 中，用户可以为链码的执行定义一个资产背书策略。背书策略设置了需要达成一致并认为有效的交易以及添加到共享账本所需的对等节点。

+   成员服务提供者（MSP）: MSP 是数字证书的管理机构，它管理用户 ID 并验证网络上的所有参与者。所有成员必须是已知的身份才能在 Fabric 上进行交易。这是因为网络是私有的，基于权限。MSP 用于验证和验证这些成员的身份和权限。MSP 使用一个名为*cryptogen*的证书生成工具。为了更好地了解 MSP，请访问这里的文档：[`hyperledger-fabric.readthedocs.io/en/latest/msp.html`](https://hyperledger-fabric.readthedocs.io/en/latest/msp.html) 。

+   *对等节点*：Hyperledger Fabric 网络建立在由网络成员拥有和贡献的对等节点上。节点可以是组织或个人。节点持有共享账本，并可以执行链码。节点可以访问账本数据；它们可以背书交易并与应用程序接口。节点可以具有背书对等节点或背书者的权限。对等节点接收按顺序的账本状态更新，作为它们接收的块的一部分，以维护账本，或 Hyperledger 称之为 *世界状态*。

+   *通道*：通道可以由一组对等节点创建。一组节点可以创建一个单独的交易账本。通道类似于您在第三章中创建自己的区块链时创建的 P2P 通道。

+   *组织*：每个对等节点贡献资源，它们共同形成集体网络。拥有组织可以使用数字证书通过 MSP 分配对等节点。此外，来自不同组织的对等节点可以加入一个通道。具有不同对等节点的组织可以共享相同的 MSP。最佳实践是为每个组织提供一个 MSP。

+   *排序服务：* 此服务将交易打包成区块。然后可以将区块广播到共享 P2P 通道上的对等节点和客户端。通道将具有相同逻辑顺序的相同消息输出到所有对等节点。一致的逻辑顺序称为 *原子交付*。

请查看图 8-1，这是组成 Hyperledger Fabric 的组件的图形表示。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig1_HTML.jpg](img/475651_1_En_8_Fig1_HTML.jpg)

图 8-1

Hyperledger Fabric 图形解释。图片来源：developer.ibm.com。

让我们通过图 8-1 中的 10,000 英尺图形概览来了解 Fabric 网络。Hyperledger Fabric 网络作为客户端应用程序的后端层。

客户端应用程序可以是任何东西，如 dapp、门户、业务活动或网站；这些类型的应用程序是前端层，它们可以通过编码 Hyperledger Fabric SDK 或 REST web 服务来访问链码、交易和事件。客户端调用链码节点，该节点使用 SDK 与网络交互。与迄今为止涵盖的传统区块链不同，Fabric 之所以不同，是因为并非所有对等节点都有相同的权限。

与传统区块链不同，Hyperledger Fabric 不允许未知身份在网络上进行交易。组织被称为*成员*，它们建立 Hyperledger Fabric 网络，每个成员可以通过 MSP 设置他们的节点对。您可以在图 8-1 中看到示例有 ORG1 MSP 和 ORG2 MSP。

对等节点可以在网络上设置不同的规则：背书节点、锚节点和排序节点。

+   *背书节点* *:* 该节点接收执行交易和链码的请求。背书节点可以批准或拒绝交易。只有背书节点执行链码，因此无需在所有节点上安装链码。

+   *锚定节点* *:* 这些节点接收消息并与其他组织内的节点发送消息。P2P 网络由不同的通道组成，可以设置权限，使其不对网络上的所有人可见。

+   *排序节点* *:* 此节点处理共享账本，并负责在网络中保持状态。排序节点生成区块并向所有节点广播。排序节点可以设置为 Solo 或 Kafka。

    *Solo:* 此选项用于具有单一故障点的开发。在本章中，你将在开发环境中设置此选项。

    *Kafka:* 此选项用于生产环境。Kafka 具有容错特性。

你将在 Solo 节点上创建链码并部署到 Fabric 网络，然后你将能够访问和运行功能。要发送交易，你的客户端应用程序可以连接到 SDK 并创建交易。然后交易会被发送到背书的 Solo 节点，该节点验证签名并发送背书签名。背书签名被发送到排序服务。在生产环境中，排序服务会将交易发送到所有网络连接的节点，这些节点在其账本上更新其世界状态。

我鼓励你访问 Hyperledger 页面以了解更多信息并阅读白皮书：[`www.hyperledger.org/projects/fabric`](https://www.hyperledger.org/projects/fabric) 。

## 安装 Hyperledger Fabric 和 Composer

开始使用 Hyperledger 网络的一个好方法是安装 Hyperledger Fabric 和 Composer。你将通过安装所有工具和库以及 Hyperledger Fabric 和 Composer 来设置环境；然后，通过启动和停止 Hyperledger Fabric 并检查 Composer 库是否正确安装来验证安装是否成功。

### 先决条件

Hyperledger Fabric 和 Hyperledger Composer 依赖于许多工具和库，由于每个用户使用不同的机器，这个过程可能不会很快很简单，可能会限制 Hyperledger 的适应性。我将这个过程分解为这些步骤：

1.  1)

    验证已安装的先决条件。

1.  2)

    更新 Git。

1.  3)

    安装 Node 版本管理器。

1.  4)

    更新 Node.js。

1.  5)

    安装 VSCode。

1.  6)

    安装 Hyperledger Composer 扩展。

1.  7)

    安装 Hyperledger Composer 基础 CLI 工具。

1.  8)

    安装 Hyperledger Fabric。

建议你访问 Hyperledger Fabric 的先决条件页面，因为版本和需求可能已经更改：[`hyperledger.github.io/composer/v0.19/installing/installing-prereqs.html`](https://hyperledger.github.io/composer/v0.19/installing/installing-prereqs.html) 。

在开始之前，建议如果你有一段时间没更新过 Brew，那么现在更新和升级一下 Brew。> brew update && brew upgrade

#### 验证已安装的先决条件

安装 Hyperledger Fabric 需要一个长长的先决条件列表；然而，如果您一直跟随本书的章节，您电脑上应该已经安装了大部分的先决条件。

对于操作系统（OS），Fabric 至少需要 macOS 10.12。您可以通过计算机左上角的菜单来检查您的版本。点击苹果图标，然后点击“关于本机”。打开概述标签页，并显示 macOS 版本。如果您正在运行一个较旧的版本，那么通过点击软件更新按钮来获取 10.12 更新。截至编写本文时，macOS 被称为 Mojave，版本为 10.14.4。

您还需要 Xcode 和 Docker。这些在前面的章节中已经安装，但您需要确认它们已经安装并且版本正确。只需运行 xcode-select --version 命令确保 Xcode 正在运行。您可以将自己的结果与我显示的结果进行比较：> xcode-select -vxcode-select 版本 2354。> docker --versionDocker 版本 19.03.0-beta3，构建 c55e026 您需要 Docker-Compose 版本 1.8 或更高。> docker-compose --versiondocker-compose 版本 1.24.0，构建 0aa59064 您需要 npm 版本 v5.x 或更高。> npm --version6.8.0 您需要 Python 2.7.x 或更高。> python --versionPython 2.7.10

#### 更新 Git

安装正在请求 Git 2.2.x 或更高版本。然而，Mac 附带的是一个较老的 Git 版本；您可以使用这个命令来检查您的版本：> git --versiongit 版本 2.20.1（Apple Git-117）要升级 Git，您将通过 Brew 安装 Git，并设置您的机器使用 Brew 中的 Git 版本而不是随 Mac 附带的版本。首先，通过 Brew 安装 Git。> brew install git 接下来，您将设置您的路径指向新的 Git 位置；使用 vim 或您喜欢的文本编辑器。> vim ~/.bash_profile 在 PATH 中添加以下内容：#git 指向 brewPATH=/usr/local/bin:$PATH 别忘了在保存并退出 bash 配置文件后运行 bash_profile，以确保更改生效。> . ~/.bash_profile 最后，您可以验证 Git 的版本。> git --version 你现在指向的是用 Brew 安装的 Git 的位置，对于未来的 Git 升级，您可以简单地运行以下操作：> brew upgrade gitgit 版本 2.21.0

#### 安装 Node Version Manager (nvm)

Node Version Manager (nvm) 需要安装。要下载或更新 nvm，请查看 GitHub 页面上的[`github.com/creationix/nvm/blob/master/README.md`](https://github.com/creationix/nvm/blob/master/README.md)，并运行以下命令：> curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash 安装完成后，您可以确认它是否正确安装。打开一个新的终端，并输入以下内容。我已经安装了版本 0.34.0。> nvm --version0.34.0

#### 更新 Node.js

节点需要版本 8。要检查你正在运行的版本，运行这个命令：`node --version

在撰写本文时，hyperledger.github.io 页面指出你应该安装最新（长期支持）版本的 Node；然而，它一直在产生致命错误，并在 GitHub 上记录了一个错误。在撰写本文时，Node.js 版本 9 也不受支持。

要让 Hyperledger Composer 工作，你需要安装 node 8 并将 nvm 指向使用 node 8。`nvm install 8``npm config delete prefix``nvm use 8`你可以确认 node 8 已正确安装。`node --version`v8.15.0

### 使用 Hyperledger Composer 扩展安装 VSCode

建议你安装带有 Hyperledger Composer 扩展的 Visual Studio Code（VSCode）并将其作为代码编辑器。扩展将提供代码高亮显示，并且是一个专业的免费 IDE。要开始使用，请从以下链接下载 VSCode：[`code.visualstudio.com`](https://code.visualstudio.com) 。点击为 Mac 下载，如图 8-2 所示。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig2_HTML.jpg](img/475651_1_En_8_Fig2_HTML.jpg)

图 8-2

Visual Studio Code 安装页面

安装完成后，启动 VSCode。

要安装 Hyperledger Composer 扩展，请点击 VSCode 的左侧菜单，从左侧菜单栏选择扩展（两个正方形图标），然后在搜索框中输入**Hyperledger Composer**。选择：Hyperledger Composer。然后点击安装。最后，重新加载以激活它。见图 8-3。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig3_HTML.jpg](img/475651_1_En_8_Fig3_HTML.jpg)

图 8-3

VSCode Hyperledger Composer 扩展

#### Hyperledger Composer 基本 CLI 工具

您将安装包括 composer-rest-server、Composer Playground 和 Yeoman 生成器的 Hyperledger Composer Essential CLI 工具。

安装 Composer CLI，运行以下命令。`npm install -g composer-cli @0.19

### 注意

我使用的是版本 0.19。Hyperledger 的最新版本 0.20.6 与所有工具和库有关的一些开放错误，所以我使用的是 Hyperledger Composer 和 Hyperledger Fabric 的先前版本。这可能会改变，所以你可能想检查文档并安装另一个版本。此外，我还收集了许多在安装和运行 Hyperledger Composer 和 Fabric 时可能会遇到的潜在错误；请参阅本章后面的“错误故障排除”部分。

接下来，安装用于生成 Hyperledger Composer 应用程序的 Yeoman 工具，该工具使用 generator-hyperledger-composer。执行以下命令：> npm install -g generator-hyperledger-composer@0.19 你现在可以使用 npm 全局安装 Composer Playground。> npm install -g composer-playground@0.19Composer 的一部分是一个名为 composer-rest-server 的工具，该工具生成一个基于 loopback 的 REST 接口，以便能够访问你将创建的网络。要安装该工具，请执行此命令：> npm install -g composer-rest-server@0.19> npm install -g Yeoman 你可以通过运行--version 标志来验证安装是否成功。> composer --versionv0.19.20> composer-rest-server --versionv0.15.2> composer-playground --version0.20.6 为确保生成器工具已安装，如果你运行 Yeoman 命令，它应该列出 Hyperledger Composer 生成器。> Yeoman 它将输出以下内容？'Allo! What would you like to do? (Use arrow keys) 运行一个生成器◻ Hyperledger Composer

按下 Control+C 退出 Yeoman 命令。

#### 使用 Docker 安装 Composer Playground

除了使用 npm 全局安装 Composer 工具外，你还可以使用 Docker 运行 Hyperledger Composer Playground；只需运行容器并将 composer-playground 作为名称。你将在端口 8080 上运行它。> docker run --name composer-playground --publish 8080:8080 hyperledger/composer-playground Docker 命令下载图像，你可以看到输出在图 8-4 中。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig4_HTML.jpg](img/475651_1_En_8_Fig4_HTML.jpg)

图 8-4

容器输出 Composer-playground docker

要取消容器，请按 Control+C。

现在要在外部浏览器上端口 8080 上运行 Playground，请按 Command+T 打开新终端窗口并运行打开命令。> open http://localhost:8080 你可以看到 Hyperledger Composer Playground 欢迎页面，如图 8-5 所示。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig5_HTML.jpg](img/475651_1_En_8_Fig5_HTML.jpg)

图 8-5

播放场欢迎屏幕

记住，要停止 Docker，你可以运行停止命令。> docker stop composer-playground 要删除 composer-playground 名称，以便你可以再次使用它，你需要运行以下命令：> docker rm --force composer-playground

#### 安装 Hyperledger Fabric Dev Servers

在撰写本文时，Hyperledger Fabric 的最新版本是 v1.4.1；你应该访问 GitHub 页面以获取最新版本和文档，因为这些可能会更改；参见[`github.com/hyperledger/fabric`](https://github.com/hyperledger/fabric)。

Hyperledger Fabric dev servers 有不同版本可供选择。你将为你开发设置一个 Hyperledger Fabric v1.2 网络。

然后，您可以部署使用 Hyperledger Composer 构建的区块链业务网络并测试您的应用程序。

创建一个目录来下载 Fabric；我选择~/fabric-dev-servers，但您可以选择任何目录。> mkdir ~/fabric-dev-servers && cd ~/fabric-dev-servers 您将使用 curl 获取安装 Hyperledger Fabric 所需的.tar.gz 文件，如下所示：> curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.tar.gz 使用 tar 提取您下载的文件。> tar xzf fabric-dev-servers.tar.gz

一旦这些文件被提取，您就有脚本文件帮助您快速启动 Hyperledger Fabric 实例。

运行 ls 命令，您可以看到其他有用文件中的.sh 文件。> ls startFabric.sh teardownAllDocker.sh stopFabric.sh teardownFabric.sh 当你运行 Composer –v 命令时，你可以检查你正在运行的版本。你看到你确实安装了 Hyperledger Composer v0.19，所以根据文档，你需要使用 Hyperledger Fabric v1.1，你还可以将 Fabric 启动超时设置为 30 秒；这是运行脚本后确保网络运行的等待时间。> export FABRIC_VERSION=hlfv11> export FABRIC_START_TIMEOUT=30

### 提示

如果你正在运行不同版本的 Hyperledger Composer，请查看 GitHub 页面以确定需要设置哪个版本的 Fabric：[`github.com/hyperledger/composer-tools/tree/master/packages/fabric-dev-servers`](https://github.com/hyperledger/composer-tools/tree/master/packages/fabric-dev-servers) 。

要启动您的 Hyperledger Fabric 网络，您需要首先执行下载 Fabric 脚本；这取决于您的互联网连接速度可能需要一些时间。> ./downloadFabric.sh 这就对了；您应该看到图 8-6 中显示的输出。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig6_HTML.jpg](img/475651_1_En_8_Fig6_HTML.jpg)

图 8-6

下载 Hyperledger Fabric 输出

下载完成后，您可以确认您有 Docker 容器。> docker image ls hyperledger/*hyperledger/fabric-cahyperledger/fabric-ordererhyperledger/fabric-peerhyperledger/fabric-ccenvhyperledger/fabric-couchdb

#### 网络连接配置

有一个名为 DevServer_connection.json 的网络连接配置文件。

在本节中，您将修改该文件以适应您将创建的 Docker localhost 容器。在修改文件之前，先做一份副本是个好主意。> cd ~/fabric-tools/> cp DevServer_connection.json DevServer_connection-backup.json

将原始文件的或 derers、peers 和证书权威更改为指向 localhost，因为您将在网络中以 Docker 容器的形式运行 Composer Rest Server，并访问网络上的这些主机名。

使用 vm 或您喜欢的编辑器编辑 DevServer_connection 文件。> vim DevServer_connection.json 查看图 8-7 ![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig7_HTML.jpg](img/475651_1_En_8_Fig7_HTML.jpg)

图 8-7

将 devServer.json 更改为指向 localhost

您还需要编辑 hosts 文件，使其指向本地服务器上的 127.0.0.1。`sudo vim /etc/hosts`# fabric127.0.0.1 orderer.example.com peer0.org1.example.com ca.org1.example.com

### 启动本地 Hyperledger Fabric 商业网络

第一次运行 Hyperledger Fabric 时，您需要执行命令来启动本地 Hyperledger Fabric 实例并为管理员发行 ID 卡。默认的管理员称为 PeerAdmin。要开始，请运行启动 Fabric 命令。`.`/startFabric.sh`。预期的输出是确认您的变量。Hyperledger Fabric 控制的发展专用脚本正在运行`startFabric.sh`FABRIC_VERSION 被设置为[版本号]...创建名为"composer_default"的网络 Creating ca.org1.example.comCreating orderer.example.com

作为启动脚本的一部分，您可以看到确认创建了 composer_default Docker 网络并运行在创建的网络中的容器的输出行。容器能够使用自定义的主机名进行通信：ca.org1.example.com 和 orderer.example.com。

#### 创建管理员 ID 卡

现在您已经有了一个运行的网络，最后一步设置是创建凭据。

您可以使用 Hyperledger Composer 来创建 Hyperledger Fabric 所说的`.card`文件。

您可以通过执行以下命令来生成管理员 ID 卡：`.`/createPeerAdminCard.sh`。您可以将您的输出与我的进行比较，如图 8-8 所示。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig8_HTML.jpg](img/475651_1_En_8_Fig8_HTML.jpg)

图 8-8

Hyperledger Composer 生成卡片

为了确认卡片是否正确创建，请使用`<card name>`执行以下命令：`composer card list --card PeerAdmin@hlfv1`。此命令输出有关 ID 卡的信息。请参考图 8-9。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig9_HTML.jpg](img/475651_1_En_8_Fig9_HTML.jpg)

图 8-9

查看 Hyperledger Composer 卡片列表

#### 停止 Hyperledger Fabric

暂时让 Fabric 运行，但完成练习后，您可以通过执行停止命令来关闭 Hyperledger Fabric 运行时。`.`/stopFabric.sh`。此外，您应该在开发周期结束时执行拆卸脚本，以确保释放内存。`.`/teardownFabric.sh`。

### 注意

如果您运行了拆卸脚本，下次启动运行时，您需要像首次启动时那样创建一个新的 PeerAdmin 卡。请参考以下步骤。

#### 重新创建 PeerAdmin ID 卡

在你停止并拆除这些命令后：> ./stopFabric.sh> ./teardownFabric.sh 你需要重新创建管理员 ID 卡，所以只需按照相同的命令进行操作。> ./startFabric.sh> ./createPeerAdminCard.sh> composer card list --card PeerAdmin@hlfv1 遵循图 8-10 的过程是个好主意，它展示了你需要做的一切来启动、停止、创建和拆除卡片。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig10_HTML.jpg](img/475651_1_En_8_Fig10_HTML.jpg)

图 8-10

布料开发服务器启动停止流程。图片来源：github.com/hyperledger/composer-tools。

## 超级账本 Composer

既然你已经安装并运行了超级账本 Fabric 网络，下一步就是编写链码。你可以用 Go 本地方法超级账本 Fabric 编写链码；然而，你也可以利用超级账本 Composer 来帮助通过编写 JavaScript 而不是 Go 来创建链码和区块链应用程序。超级账本 Composer 生成业务网络归档 (.bna) 文件，然后你可以将其部署到超级账本网络上来运行。Composer 易于使用，并不仅仅针对开发者，也面向商务人士。

超级账本 Composer 由三个组件组成（见图 8-11）。

+   **业务网络归档 (.bna)**：这由四个文件组成。

+   **超级账本 Composer 游乐场**：这个用途是为了配置和部署网络以及测试代码，而不必推出区块链。

+   **REST API 支持**：这暴露了供前端客户端（如 dapps）使用的方法。

![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig11_HTML.jpg](img/475651_1_En_8_Fig11_HTML.jpg)

图 8-11

超级账本 Composer 图形解释。图片来源：developer.ibm.com。

## “你好，世界”与游乐场

你将创建一个“你好，世界”应用程序，并使用游乐场将其部署在网络上。开始的话，通过命令行打开游乐场并执行这个命令：> composer-playground

另外，你可以使用 Docker。打开后，点击“让我们区块链！”来关闭欢迎屏幕。

### 部署业务网络

接下来，选择“部署一个新的业务网络”。在部署向导中，输入基本信息，例如在“给你的新业务网络取名”输入框中输入**hello-network**。

选择中间的“空业务网络”网络定义，并点击部署，如图 8-12 所示。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig12_HTML.jpg](img/475651_1_En_8_Fig12_HTML.jpg)

图 8-12

超级账本 Composer 游乐场，部署新业务网络向导

为你的网络创建了管理员 ID 卡。要连接到网络，点击图 8-13 中显示的“现在连接”链接。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig13_HTML.jpg](img/475651_1_En_8_Fig13_HTML.jpg)

图 8-13

连接到 hello-network 业务网络定义

你现在已连接到业务网络定义网络，可以定义和工作在模型上。

### 业务网络存档（.bna）

业务网络模型包括资产及其相关的交易。Hyperledger Composer 需要以下内容一起打包：一个网络模型文件、一个 JavaScript 文件（.js）、一个访问控制文件（.acl）和一个查询文件（.qry）。这些文件是定义文件，生成你的网络。

+   *网络模型（.cto）*：这个文件定义了资产、交易以及可以与这些资产交互的参与者。该文件是用名为 CTO（源自原始项目名称 Concerto）的建模语言创建的。

+   *JavaScript 文件（.js）*：这个文件定义了交易处理函数。它是链码。

+   *访问控制（ACL）文件（.acl）*：这个文件包含了定义不同参与者权利的访问控制规则。

+   *查询文件（.qry）*：这个文件定义了可以在网络上运行的查询。

Hyperledger Composer 取这四个文件并创建一个业务网络定义，打包成.bna 文件。.bna 文件可以部署在 Hyperledger Fabric 网络上。

然后，你可以编写一个客户端应用程序，如 dapp，使用 Hyperledger Composer API 来访问通过 Hyperledger Fabric 网络编写的智能合约（.bna 函数）。

### 添加模型文件

创建模型文件时，你可以添加构成.bna 归档的文件。例如，要添加一个模型文件，点击“添加文件”，选择“模型文件（.cto）”，然后点击添加，如图 8-14 所示！../images/475651_1_En_8_Chapter/475651_1_En_8_Fig14_HTML.jpg

图 8-14

向业务网络模型添加文件

对于.cto 文件，你将定义处理函数和交易。

对于命名空间，你将使用一个名为 Skynet 的虚构公司，其标识 ID 为字符串类型。你还将创建一个 msg 字符串和一个交易 Hello，并传递包含消息的 Myfunction 资产。

### 添加链码

接下来，通过点击“添加文件”来添加一个 JS 文件。将链码作为交易的逻辑来将消息打印到控制台，如下所示：

交易代表了链码，即你应用的业务逻辑。注意注释指出代码是一个交易函数和命名空间。点击“部署更改”以更新你的定义模型。

### 创建资产

接下来，为了测试模型，您将创建一个新资产，扩展它并存储它。为此，点击顶部右上角的+创建新资产。创建新资产向导打开，如图 8-15 所示。模型已经有一个 ID；然而，为了这个例子，您将它更改为 001（但字符串可以是任何字符串）。对于消息，您将传递 world。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig15_HTML.jpg](img/475651_1_En_8_Fig15_HTML.jpg)

图 8-15

创建新资产向导

### 访问控制

请注意，有一个权限选项与权限.acl 文件作为定义标签页在屏幕左下角，如图 8-16 所示。

正如您所看到的，规则授予了广泛的“允许所有”访问权限，这可以进行更改。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig16_HTML.png](img/475651_1_En_8_Fig16_HTML.png)

图 8-16

您 hello-network 上的 ACL 权限文件

### 测试模型

模型实例保存后，您可以提交事务以调用事务。在左侧，点击“提交事务”按钮。提交事务向导打开。将 ID 设置为 001，如图 8-17 所示。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig17_HTML.jpg](img/475651_1_En_8_Fig17_HTML.jpg)

图 8-17

超级账本 Playground，提交事务向导

测试之前，请打开开发者控制台，这样您就可以看到 JavaScript 消息。对于 Safari，请按照这些说明操作。

在顶部菜单中，选择 Safari ➤ 偏好设置。点击高级标签页，然后选择“在菜单栏中显示 Develop 菜单”复选框。

按照这些步骤操作后，您将在顶部菜单中看到 Develop 作为一个选项。选择“显示 JavaScript 控制台”（或者按 Command+Option+C）。

接下来，点击提交；您将在 JavaScript 控制台中看到“Hello world”消息，如图 8-18 所示。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig18_HTML.jpg](img/475651_1_En_8_Fig18_HTML.jpg)

图 8-18

“Hello world”消息显示在 JavaScript 控制台中

### 导入/导出模型

导出模型，您可以生成业务网络归档（.bna）文件。该.bna 文件可以随后在生产环境中部署。您要做的就是点击如图 8-19 所示的导出链接。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig19_HTML.jpg](img/475651_1_En_8_Fig19_HTML.jpg)

图 8-19

导出.bna 文件

Playground 生成 hello-network.bna 文件，该文件将下载到您的计算机上。

同样，您可以导入一个.bna 文件，点击“添加文件”链接，然后在“从您的计算机上传文件...”下，您可以浏览或拖放.bna 文件。

导入/导出不仅仅是为了发布，还可以用来与他人分享模型以进行测试、开发或其他原因。我附上了本书代码中的 hello-network.bna 文件，所以你可以随意导入；请参阅[`github.com/Apress/the-blockchain-developer/chapter8/hello-network`](https://github.com/Apress/the-blockchain-developer/chapter8/hello-network)。

`.bna`文件只不过是一个名为 bna 的压缩文件夹。实际上，你可以将`.bna`文件复制为`.zip`并解压文件。> cp hello-network.bna hello-network.zip> unzip hello-network.zipVSCode 可以作为你整个 Hyperledger 项目的 IDE。例如，现在你已经解压了你的文件，你可以在 VSCode 中打开并拖放模型文件 models/org.example.model.cto 到 VSCode 中。你可以看到代码被突出显示，如图 8-20 所示。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig20_HTML.jpg](img/475651_1_En_8_Fig20_HTML.jpg)

图 8-20

在 VSCode 中模型 CTO 文件

你使用 Composer Playground 的网页界面编写了你的文件。这个套装是对开发者不太友好的方法；然而，一个更大的项目可以包含复杂的业务逻辑、事件、许多交易和测试，因此建议使用 VSCode 创建你的项目并管理文件，然后将那些文件上传到 Playground 进行部署。

### 在线 Playground

Hyperledger Composer Playground 在线版本可在[`composer-playground.mybluemix.net/`](https://composer-playground.mybluemix.net/)找到。你可以使用与之前相同的步骤来创建你的网络和文件。见图 8-21。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig21_HTML.jpg](img/475651_1_En_8_Fig21_HTML.jpg)

图 8-21

Composer Playground

要测试在线 Playground，你可以导入你之前创建的 hello-network.bna 文件。为此，首先点击“让我们区块链！”在“2. 模型网络起点模板”下选择“拖放这里上传或浏览”并上传 hello-network.bna 文件。点击右下角的“部署”按钮。你可以看到创建的网络。点击“现在连接”链接以连接到新网络。见图 8-22。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig22_HTML.jpg](img/475651_1_En_8_Fig22_HTML.jpg)

图 8-22

hello-network 连接链接

你可以重复在本地 Playground 上创建资产和测试的相同步骤。

#### 使用 Yeoman 创建商业网络

你使用 Hyperledger Playground 生成你的商业网络。Hyperledger Playground 不仅面向开发者，还面向企业主，因为它的简单性；然而，你也可以在终端中创建一个网络。

Yeoman 提供了一个向导，你可以使用它。如果你不熟悉 Yeoman，它通过命令行提供了一个向导生成器。你可以要么运行 Yeoman 并选择 Hyperledger Composer 和业务网络生成器，要么运行以下命令：> Yeoman hyperledger-composer:businessnetwork 记住，Hyperledger Composer 不仅仅用于生成业务网络；它还可以用于 Angular、LoopBack 和 Model。见图 8-23。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig23_HTML.jpg](img/475651_1_En_8_Fig23_HTML.jpg)

图 8-23

使用 Yeoman 向导生成 hello-network

生成了 hello-network 文件夹，包括 permissions.acl、models、features、test 和 lib。接下来，要创建.bna 文件，你可以使用 Hyperledger Composer。见图 8-24。> cd hello-network> composer archive create -t dir -n .![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig24_HTML.jpg](img/475651_1_En_8_Fig24_HTML.jpg)

图 8-24

使用 Hyperledger Composer 生成 hello-network BNA 文件

运行 ls 命令并确认生成了 hello-network@0.0.1.bna 文件。> ls *.bnahello-network@0.0.1.bna

## 在本地 Hyperledger Fabric 网络中部署

要将在本地 Hyperledger Fabric 网络中部署.bna 文件，请运行 composer network install 命令，同时指向.bna 文件并指定身份卡。> cd ~/fabric-dev-servers/> composer network install --archiveFile ~/Desktop/hello-network.bna --card PeerAdmin@hlfv1 这将导致如图 8-25 所示的成功输出。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig25_HTML.jpg](img/475651_1_En_8_Fig25_HTML.jpg)

图 8-25

安装本地 Hyperledger Fabric 命令输出

## 运行“hello-network”网络

Hyperledger Composer 是基于 Hyperledger Fabric 的区块链应用开发框架。

Hyperledger Composer 基于你创建的业务网络定义生成 REST API。这是通过所谓的 LoopBack 连接器来实现的。你可以将这些 REST API 提供给 a)如 dapp 这样的客户端 b)与非区块链客户端（如网站）集成。这使得你可以像使用任何其他数据库一样使用区块链账本，配合中间件。这是非常强大的。

Hyperledger Composer 可以生成一个 REST 接口。你可以在电脑上运行 Hyperledger Fabric，并生成一个 GUI，然后你可以使用它来像在真实生产服务器上一样与运行在电脑上的网络进行交互。

### 启动“hello-network”业务网络和管理卡

要运行你的“hello-network”网络，请运行以下命令，并在图 8-26 中查看输出：> composer network start --networkName hello-network --networkVersion 0.0.2-deploy.3 -A admin -S adminpw -c PeerAdmin@hlfv1 --file networkadmin.card![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig26_HTML.jpg](img/475651_1_En_8_Fig26_HTML.jpg)

图 8-26

启动商业网络

为了确认这是否成功，你可以运行 docker ps 命令。你应该会看到创建的 dev-peer0.org1.example.com-hello-network-0.0.2-deploy.3-0 镜像，如图 8-27 所示。> docker ps![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig27_HTML.jpg](img/475651_1_En_8_Fig27_HTML.jpg)

图 8-27

Docker 容器 hello-network

### 导入商业名片

接下来，导入一个新的网络管理员名片，这样你就可以在启动的商业网络中使用 admin@hello-network。> composer card import --file networkadmin.card 此命令导入网络管理员名片，其中将包括 admin@hello-network。> composer network ping --card admin@hello-network 你可以将你的输出与我显示在图 8-28 中的输出进行比较。![../images/475651_1_En_8_Chapter/475651_1_En_8_Fig28_HTML.jpg](img/475651_1_En_8_Fig28_HTML.jpg)

图 8-28

导入商业网络名片

## 从这里出发，接下来去哪里

从这里，你可以为你的用户选择多种护照策略。例如，你可以使用谷歌 OAUTH2.0、SAML、Passport-JWT 或者 LDAP，这取决于你的组织正在使用什么。

然后，你将能够以多用户模式运行 REST 服务器，并测试与客户端应用程序（例如你创建的应用程序）的交互。

以下是一些可以帮助你设置应用程序以验证多个用户的文章：

+   *Passport-JWT*：[`hyperledger.github.io/composer/latest/tutorials/google_oauth2_rest`](https://hyperledger.github.io/composer/latest/tutorials/google_oauth2_rest)

+   *谷歌 OAUTH2.0*：hyperledger/fabric-ca docker hyperledger/fabric-orderer hyperledger/fabric-peer hyperledger/fabric-ccenv hyperledger/fabric-couchdb

Hyperledger 是一个大型项目，它包括五个主要平台以及五个主要工具。本章只讨论 Hyperledger Fabric。然而，我们鼓励你继续尝试其他 Hyperledger 平台和工具，如 Hyperledger Sawtooth，包括设置环境、创建账户、编写更复杂的链码，以及部署和连接你的链码到 dapp。

要获取更多关于入门的信息，请访问官方网站：[`sawtooth.hyperledger.org/docs/seth/releases/latest/getting_started.html`](https://sawtooth.hyperledger.org/docs/seth/releases/latest/getting_started.html) 。

实际上，你可以在这里找到关于所有平台和工具的更多信息：[`www.hyperledger.org/`](https://www.hyperledger.org/) 。

最后，收藏 Hyperledger 开发者中心：[`developer.ibm.com/technologies/blockchain/`](https://developer.ibm.com/technologies/blockchain/)

## 错误故障排除

Hyperledger 旨在简洁，允许您将模块缝合在一起，但并非没有问题。Hyperledger 为更高级的用户设置，可能需要系统管理员权限来设置服务器。您可能遇到一些错误，所以我将它们编译到这个部分中。

### Composer 运行时安装错误或找不到卡

如果您遇到这些错误：

+   “composer 运行时安装错误找不到 peerAdmin 卡”

+   “错误：找不到卡片：PeerAdmin@hlfv1”

这是因为管理员 ID 卡未能成功创建或未遵循正确的过程；您需要做的就是删除 ID 卡并重新创建。您需要删除 composer 文件夹，创建一个新的文件夹，然后再次运行命令。> rm -rf ~/.composer> mkdir ~/.composer> ./createPeerAdminCard.sh

### Docker 未授权身份验证 required 错误

在下载 Hyperledger Fabric 时，您可能会遇到以下错误：

+   “未授权：需要身份验证”

认证或代理到 Docker Hub 时存在问题，而不是 Hyperledger Fabric。

为了解决这个问题，请将您的计算机时间设置为与 UTC 时区一致：[`www.timeanddate.com/worldclock/timezone/utc`](https://www.timeanddate.com/worldclock/timezone/utc) 。

在[`hub.docker.com`](https://hub.docker.com)上创建一个 Docker 账户，然后登录。> docker login 或者，退出后再试一次。> docker logout

### Docker 容器冲突错误

当您使用 Docker 容器进行项目时，您可能需要重新创建容器或停止容器；否则，您可能会遇到冲突错误。

您需要做的所有事情就是停止并删除容器。> docker stop [容器 ID]> docker rm [容器 ID]

### 小贴士

如果您已经创建了一个 Mongo-Docker 容器或其他任何创建冲突的 Docker 容器，当您尝试创建一个新的容器时，您会得到以下冲突错误：“容器名称[容器 ID]已由容器使用。” 您需要做的就是停止容器并删除它。

> docker stop [容器 ID]
> 
> docker rm [容器 ID]

### 不匹配和清理

如果您在 Hyperledger Composer 和 Hyperledger Fabric 版本之间存在不匹配，您可能会遇到以下错误：

+   “开始业务网络定义。这可能需要一分钟...错误：尝试启动业务网络时出错。错误：未能连接到任何对等事件中心。至少连接到一个事件中心是接收提交事件命令的必要条件。命令失败。”

此错误在 Hyperledger Fabric 1.2 和 Hyperledger Composer 0.20.6 上也由开放的错误生成。为了解决这个问题，您需要检查您的 Hyperledger Composer 并卸载通过 npm，以及重新安装 Hyperledger Fabric。

此外，如果你需要彻底清理，你需要停止并拆除 Fabric。要删除 Docker 镜像，先删除`fabric-dev-servers`，最后删除 Composer，按照以下步骤操作：>  cd ~/fabric-tools> ./stopFabric.sh> ./teardownFabric.sh 接下来，停止 Docker 容器，删除它们，以及通过运行以下命令删除所有 Docker 镜像：> docker kill $(docker ps -q)> docker rm $(docker ps -a -q) –f> docker rmi $(docker images -q) -f 你现在可以彻底删除`fabric-dev-servers`。> rm -rf ~/fabric-dev-servers 要删除 Composer 和 admin ID 卡，运行以下命令：> sudo rm -rf ~/.composer> npm uninstall -g composer-cli

`npm uninstall`命令将输出一个确认库已卸载的确认信息。

## 总结

在本章中，我介绍了 Hyperledger，帮助你入门并理解其强大功能。我涵盖了 Hyperledger 生态系统和术语，并让你对组成网络的各个部分以及可用的主要 Hyperledger 平台和工具有了很好的了解。你安装了 Hyperledger Fabric 和 Hyperledger Composer，确保预先安装了必需的库。你在 Playground 中创建了“Hello, World”应用程序，以及创建了一个在本地网络上部署的`.bna`文件。我还提到了 Hyperledger Playground Online，并解释了如何使用 Yeoman 生成器生成一个网络。我涵盖了组成`.bna`归档文件的不同部分，包括处理 ID 卡。我还涵盖了可能的错误和故障排除，以确保你的安装顺利进行。最后，我介绍了一些关于从这里继续学习 Hyperledger 的建议。

在下一章，你将学习如何使用 Angular 构建一个 dapp。dapp 可以与你在前三章开发的智能合约进行交互，是区块链生态系统中的重要组成部分。
