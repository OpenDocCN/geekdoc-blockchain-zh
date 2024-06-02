© Elad Elrom 2019 Elad Elrom 区块链开发者 [`doi.org/10.1007/978-1-4842-4847-8_9`](https://doi.org/10.1007/978-1-4842-4847-8_9)

# 9. 使用 Angular 构建 dapp：第一部分

Elad Elrom^(1 )(1)纽约，纽约，美国

在之前的章节中，我介绍了不同的区块链，并学习了如何创建可以与区块链交互的智能合约。你在以太坊、NEO、EOS 和 Hyperledger 上创建了智能合约。在第一章中，我将过程分解为五层：共识层、矿工或预定层、传播层、语义层和应用层。智能合约是开发周期中应用层的一部分；然而，如果没有前端界面，使得最终用户能够与区块链交互，那么应用层是不完整的。

### 提示

很多时候，你会听到去中心化应用（dapps）被称为智能合约。智能合约是自执行的合同。dapps 使用智能合约，但运行在 P2P 网络中，而不是单一系统上。

开发者和更熟练的用户可以通过前几章中提到的命令行界面和工具与您创建的智能合约交互，但是为所有其他用户开发能够与区块链交互的前端应用程序是必不可少的。您通过创建去中心化应用程序（dapp）来实现这一点。在本章和下一章中，您将使用 Angular 创建一个去中心化应用程序，以便用户可以使用友好且直观的用户界面（UI）与智能合约交互。我将过程分为两部分。

第一部分，在本章中，包含以下主题：

+   开发去中心化应用（dapp），包括其益处和分类

+   使用 Angular，包括其架构、益处、先决条件和创建 Angular 骨架应用

+   创建和样式化 Angular 自定义组件

第二部分，在第十章中，包含以下主题：

+   使用 Truffle 创建 dapp 的智能合约

+   将智能合约集成到 dapp

+   将你的 dapp 连接到以太坊网络

让我们开始吧。

## 什么是 dapp？

*去中心化应用*（缩写为ÐApp、dapp、Dapp、dApp 或 DApp，发音为“dee-app”）是一个能够与智能合约交互的网页应用。dapps 在区块链上运行并利用分布式账本。目前，以太坊区块链是运行 dapps 最受欢迎的平台；然而，您在前几章中看到的其他分布式账本技术（DLTs）也提供了创建 dapps 的能力。我介绍了 NEO、EOS 和 Hyperledger；其他包括 ICON、Cardano 和 Hedera（Hbar）。

> “一切可以去中心化的事物都将去中心化。”
> 
> —David Johnston，DApp Fund 的 CEO [`github.com/DavidJohnstonCEO/DecentralizedApplications`](https://github.com/DavidJohnstonCEO/DecentralizedApplications)

如果你曾经开发过一个标准的桌面、网络或移动应用，你会发现 dapp 与它们相似，但也有很大不同。

一个去中心化应用（dapp）是使用与构建其他任何应用相同的工具和语言构建的，但要想将一个应用归类为 dapp，它需要满足以下标准：

+   开源：其代码作为开源发布，不应由一个实体（中心化）管理。请记住，应用程序可能会根据提出的改进和市场反馈适应其自己的协议；然而，是其用户共识推动所有变化。

+   去中心化：dapp 利用区块链或 P2P 网络。

+   激励型：dapp 使用数字资产进行资金筹集。

+   算法/协议：dapp 通常生成代币，并包括一种共识机制，如 PoW、PoS，甚至有自己的。

这些标准确保了 dapp 不会像你从 iTunes 或 Google Play 等市场下载的其他应用那样出现宕机；dapp 还将控制权交给了一个社区，而不是一个实体。这些标准可能是重要的。例如，苹果和谷歌经常因为应用不符合它们任意或基于货币的政策而拒绝这些应用。这些政策并不总是合乎逻辑，也不总是符合最终用户的最佳利益；它们经常是为了阻止使用竞争对手的应用或为了获得货币收益而存在。

基于开源代码、在去中心化区块链上实现、并通过特定共识机制生成的代币进行资金筹集的 dapp，被许多人认为将是所有商业的未来。时间会告诉我们答案。

此外，开源软件的一个优点是它允许用户查看源代码，并可能进行贡献。使用区块链进行去中心化利用了区块链作为分布式账本技术的优势，并取代了传统的单服务器数据库。

最后，向账本添加记录/交易通常是通过使用代币来完成的，而代币的共识机制也是 dapp 所有用户之间的一个协议。

### Dapp 分类

除了上述标准之外，dapp 还可以进行分类。这种分类是基于 dapp 所利用的基础设施，可以细分为这三个类别：

+   专用区块链 dapp：这些是直接使用专用区块链的 dapp，例如比特币、以太坊、EOS 和 NEO。

+   依赖另一个区块链的 dapp：例如，Omni Layer Protocol（曾称为 Mastercoin）是一个建立在对比特币区块链之上的数字货币和通信协议。

+   依赖另一个建立在另一个区块链之上的协议的 dapp：这些 dapp 使用的是建立在一个区块链之上的协议。一个例子是使用 Omni Layer Protocol 的 safe network。

理解分类概念的一个好例子是 USDT（泰达币）代币。这个代币基于两个区块链：比特币和以太坊发行了两次。在这种情况下，有两种 USDT 类型。基于比特币的原始版本是通过使用 Omni Layer 协议生成代币，而基于以太坊的 USDT 与以太坊的 ERC20 标准兼容。请查看图 9-1 ![../images/475651_1_En_9_Chapter/475651_1_En_9_Fig1_HTML.jpg](img/475651_1_En_9_Fig1_HTML.jpg)

图 9-1

USDT 的分类表示

### Dapp 项目

大多数 dapp 直接建立在以太坊区块链之上，或者使用区块链作为其代币。然而，有些 dapp 甚至构建自己的专用区块链。请查看表 9-1 一个不同 dapp 及其分类的示例。表 9-1

Dapps 及其分类示例

| **Dapp** | **描述** | **分类** | **代币** | **区块链** |
| --- | --- | --- | --- | --- |
| Ethlance | 发布职位和雇佣自由职业者的市场。0%的费用。 | 直接使用以太坊 | 无代币 | 以太坊区块链 |
| Golem | 全球闲置计算机能力的市场。 | 基于以太坊的代币 | GNT | 以太坊区块链 |
| 安全网络 | 数据存储和通信网络。 | 依赖于另一种协议（Omni 协议）的实现，该协议建立在另一种区块链（比特币）之上 | SFE | 比特币 |

除了表 9-1 中的信息外，还有许多资源可以找到更多的 dapp；这两个网站提供了可以检查的 dapp 列表：[`dapps.ethercasts.com/`](https://dapps.ethercasts.com/) 和 [`coinsutra.com`](https://coinsutra.com) 。

### 如何创建自己的 Dapp？

比特币和区块链的成功带来了 dapp 的爆炸式增长。开发者和企业主们创建了一个基本的开发 dapp 的流程。你不必完全遵循这一点，并且随着时间的推移，它可能会有所变化；然而，许多已发布的 dapp 都是遵循这个流程的。这个过程包括以下五个步骤：

1.  1.

    编写白皮书。

1.  2.

    进行首次代币发行（ICO）。

1.  3.

    开发 Dapp。

1.  4.

    启动你的 Dapp。

1.  5.

    推广你的 Dapp。

让我们回顾这些步骤。

#### 编写白皮书

白皮书类似于公司面向投资者的商业计划。然而，它针对的不仅仅是投资者；它是技术蓝图。白皮书是技术文档以及商业计划，应解释所解决的问题以及 Dapp 的概念、特点和技术方面。

与商业计划一样，包含你的独特卖点（USP）、路线图、成员简历、能力和历史，以帮助建立信誉。

### 注意

独特卖点（USP）是你的 dapp 旨在解决的问题。

一旦白皮书发布，在早期阶段和开发之前，从同行和社区获取反馈意见是个好主意。社交媒体、论坛和出版物通常用于推广 dapp，并帮助建立信誉。

#### 进行首次代币发行（ICO）

一旦白皮书发布，下一步就是启动 ICO，并通过销售代币或硬币来筹集资金支持你的 dapp。代币应该有存在的理由，而不是与其他代币/硬币相同，因此你应该解释你的 dapp 为什么需要自己的代币或硬币。

你还需要决定你的 dapp 的分类类型，这将决定你是否需要以下所有或部分内容：1)发行代币；2)设置使用费用；3)拥有专用区块链；4)拥有挖矿机制；5)设置费用分配；6)奖励投资者；7)将费用分配给你的业务的不同部门：支持、开发、营销和商业。

#### 开发 dapp

开发应该是开源的，通常使用 GitHub 来管理开发过程中的代码仓库。在每次发布时，告知投资者和其他人关于发布的消息是个不错的主意，这样可以围绕你的项目建立用户和开发者社区。许多 dapp 试图筹集资金但未能提供实用的产品；你需要与监管机构区分开来，避免潜在的问题。（我将在第十一章中讨论监管机构。）

#### 发布你的 dapp

发布你的 dapp，并附上你的发布说明、文档、路线图和维护计划。如期满足发布日期至关重要。

#### 推广你的 dapp

最后一步是市场营销。除了传统营销外，在 dapp 的早期阶段或发布后，通常会聘请或与推广者合作，以便让更多人了解。对于 dapp 来说，独特的一点是将代币/硬币列入交易所。这是认可的最终标志。一些交易所设有投票系统，用以挑选下一个待上市的代币或硬币。一些交易所滥用这一流程，对上市代币或硬币收取高额费用。例如，在 Binance 交易所上市一个实用代币可能需要花费从 50 万美元到 300 万美元不等。

许多早期投资者，包括 dapp 的所有者，如果代币能被主要交易所上市，通常能够“套现”，因为上市往往会使代币价格上涨；然而，dapp 上市变得越来越困难，它需要提供真正的价值。骗子经常被曝光，代币/硬币上市后很快就会被取消上市。

## 为什么选择 Angular？

在使用 dapps 时，就像使用任何传统应用一样，你可以将应用程序原生编写为发布到的设备的应用程序（例如使用设备支持的语言如 Xcode 的 iOS）；然而，已经证明使用框架可以加快开发速度。例如，如果你想要利用相同的代码并在具有不同屏幕尺寸的多台设备上部署应用程序，对于小团队来说可能是一个挑战。Angular 能帮助你同时为 Web、移动端和桌面构建跨平台的现代应用程序。Angular CLI 和组件开发套件（CDK）可以帮助加速应用程序的开发。

使用 Angular 可以是很有益的，原因如下：

+   大量社区支持

+   企业架构和扩展

+   跨平台支持

+   文档

**Angular** 是一个结构框架，能让你创建前端客户端应用程序。它的各个部分松散耦合，以模块化的方式构建，这意味着编写更少的代码，增加灵活性，代码更易读，开发时间更短。

Angular 允许开发者构建一个工具集，以满足你的应用程序的确切需求。你可以使用 HTML 作为模板语言，并扩展 HTML 的语法，以便应用程序的组件易于阅读。除了 HTML，编码是用 TypeScript 完成的，它将 JavaScript 转换成面向对象的编程语言，并为你提供企业级环境。

此外，Angular 结构良好，完全符合可访问丰富的互联网应用（ARIAs）的标准，因此你的应用或网站可以正确地为残疾人构建。

Angular 也与其他 JavaScript 库相处得很好，所以你可以使用 npm 管理器安装像以太坊 JavaScript API web3.js 这样的库。最后，Angular 的功能可以轻松修改或替换，以满足你的确切需求。

### 注意

单词 *angular* 意味着具有多个角度或通过角度来测量。Angular 是一个结构框架，能让你为 Web、移动端和桌面创建前端客户端应用程序。它是一个用于动态应用开发的开放源代码前端框架。

Angular 的主要功能是数据绑定和依赖注入。这些可以帮助减少代码量。此外，Angular 已经存在多年，现在是第七个版本。

### 注意

依赖注入是一种设计模式技术。正如其名，这意味着通过注入代码，使用一个对象作为另一个对象的依赖。

Angular 2 是 AngularJS 的完全重写，并带来了一次重大变革；然而，从 Angular 2 到版本 8 之间并没有重大差异。

在撰写本文时，最新版本的 Angular 是 7.3.1，在这一版本中，添加了以下几个功能：

+   **依赖项**：依赖项得到了升级，并添加了对 TypeScript 3.1、RxJS 6.3 和 Node 10 的支持。

+   *捆绑预算*：你可以为应用程序的大小设置一个警告，以确保你不超过限制（默认是 2 MB）。

+   *Angular CLI*：通过运行 CLI 向导，你可以添加如路由等组件，并决定 CSS 的格式。

+   *Angular Material 的组件开发工具包（CDK）*：添加新的特性，如开箱即用的虚拟滚动、拖放功能以及对原生选择字段的支持。（我将在本章后面介绍 Material。）

Angular 8 处于发布候选 2（rc.2）阶段，预期的新特性主要是提高性能。它将包括一个改进的视图引擎，名为 Angular Ivy，改进的针对支持 ES2015+的现代浏览器的 JavaScript 上传支持，支持使用硬件进行重负载操作的 web workers，支持 TypeScript，一个基准测试工具，以及更多内容。

### 提示

我选择了 Angular，但 Angular 并不是唯一可以加快开发速度的框架。你可以使用其他框架，比如 React（[`reactjs.org`](https://reactjs.org)），以获得类似的好处。这个决定真的取决于个人喜好和你的团队技能。你可以通过将你的项目的文件复制到 React 项目中，很容易地将这个项目转换为 React 项目。

### 创建 Angular Dapp

在本节中，你将创建一个实际的 dapp，它将连接到以太坊网络，并从一个账户向另一个账户转账资金。这是任何 dapp 的核心功能。例如，你可以构建一个销售产品、提供服务或支付用户做测验的 dapp，所有这些类型的 dapp 都需要有一个机制来转账币/代币。在本章的这一部分，你将利用 Angular 创建一个 dapp。

在环境和部署方面，你将使用在第五章中使用的 Truffle 网络框架，因为它有助于快速创建智能合约。Truffle 不仅能帮助编译你的智能合约，还能为你做一切你需要的事情，将智能合约注入到网页应用中，并可以运行测试套件。你还将再次使用 MetaMask 来在浏览器中获取安全的区块链账户。最后，你将使用和运行 Ganache 来创建一个本地区块链 RPC 服务器，以进行测试和开发。

#### 先决条件

大部分你需要的都已经安装好了。Angular 需要 Node 和 npm 管理器，你之前已经安装过了。通过运行带有 v 标志的库来确认正确版本是否已安装，就像你在之前的章节中做的那样。`node -v` `npm -v`如果你没有 npm 和 node，只需运行以下命令：`brew install node`给你的用户拥有 npm 的所有权，这样你就不需要使用 sudo 来安装库了。`sudo chown -R $USER:$GROUP ~/.npm` `sudo chown -R $USER:$GROUP ~/.config`建议你升级 npm，以确保你使用的是最新版本；截止到撰写本文时，版本为 6.9.0。`[sudo] npm install -g npm@6.9.0`

#### Angular CLI

接下来，你需要安装 Angular 命令行接口（CLI）。对于 Angular CLI，建议（但不是必须）使用 sudo 和 allow-root 安装 Angular CLI，并确保 Angular CLI 具有正确的权限。你将安装版本 7.3.9，这是 Angular 的最新稳定版本。> sudo npm install -g @angular/cli@7.3.9 --unsafe-perm=true --allow-root+ @angular/cli@7.3.9added 363 packages from 197 contributors in 13.691s 你也可以安装 Angular 的最新版本，但你的示例代码可能会在新版本的 Angular 中损坏。> sudo npm install -g @angular/cli --unsafe-perm=true --allow-root 为验证安装是否成功，运行版本标志，你应该看到版本 7.3.9；图 9-2 显示了预期的输出。> ng version![../images/475651_1_En_9_Chapter/475651_1_En_9_Fig2_HTML.jpg](img/475651_1_En_9_Fig2_HTML.jpg)

图 9-2

Angular CLI 安装验证

#### 创建一个 Angular 项目

现在你已经安装了主要工具和库，你可以从头开始创建你的项目，通过下载其他需要的库、测试库和构建脚本，以及创建自己的文件夹结构；然而，为了加快这个过程，你可以使用包含骨架项目的 Angular 种子项目来快速引导你的项目。

使用 Angular 种子项目可以帮助你快速、高效地开始开发，遵循 Angular 的最佳实践。使用模板骨架代码有其优点和缺点。你可以自己决定是否为未来的项目使用这个骨架，但对于这个演示应用来说，它是理想的。

有许多方法可以使用 Angular 种子骨架来创建你的项目。在这里我会向你展示两个选项：使用 Angular CLI 和 WebStorm。

`ng new`命令将运行一个脚本来创建你的应用。你可以运行 CLI 新命令并将应用名称设为 ethdapp。> 切换到~/桌面> ng new ethdapp 你想添加 Angular 路由吗？（y/N）y 你想使用哪种样式表格式？（CSS）

注意我在这里添加了路由，并决定使用 CSS 进行样式设计。我会在本章后面详细介绍这些内容。

安装完成后，它会输出所有创建的文件。CREATE ethdapp/README.md (1024 字节)CREATE ethdapp/angular.json (3557 字节)CREATE ethdapp/package.json (1313 字节)...切换到新创建的文件夹并确认你有初始的文件和目录。> cd ethdapp 运行以下命令将分析你的 package.json 配置文件并提出建议：> ng update 你可以运行以下命令来遵循建议：> ng update --all 接下来，全局安装 Bower。Bower 是一个经常与 Angular 一起使用的包管理器。在撰写本文时，它处于版本 1.8.8。> npm install -g bower> bower -v1.8.8 让我们回顾一下在工作区和启动项目文件中创建了什么（见图 9-3）。![../images/475651_1_En_9_Chapter/475651_1_En_9_Fig3_HTML.jpg](img/475651_1_En_9_Fig3_HTML.jpg)

图 9-3

由 Angular CLI 创建的 Ethdapp 文件

+   新的工作区：这是名为 ethdapp 的根文件夹。

+   e2e 文件夹：这里包含一个端到端测试项目，位于此处：ethdapp/e2e。测试文件夹包括 Jasmin 库的 JSON 配置文件。

+   源文件夹：这是你的项目文件夹，包括你项目的所有文件。

    +   一个初始的骨架应用项目，位于此处：ethdapp/src/app

    +   包含入口文件 index.html 的资产文件夹

    +   其他配置文件

+   .gitignore：在这里列出你希望在将项目上传到 Git 时忽略的文件和文件夹。

+   angular.json：这是你的项目配置文件，包括有关你的项目的信息。

+   package.json：这是 npm 管理器的配置文件，包括你将在项目中使用的所有库。

+   README.MD：这是关于你的项目的文档；这将是你的项目“主页”文档，也是开发者首先阅读以获取如何运行项目的指导的文件。

+   tsconfig.json：这是 TypeScript 配置文件。

+   tslint.json：这是用于设置最佳实践格式化、间距等内容的 Lint 配置文件。

##### 服务于应用程序

要查看你的实际 dapp，你将使用 ng serve 命令，该命令会构建应用、启动开发服务器、监视源文件，并在你更改这些文件时重新构建应用。使用--open 标志会在本地端口 4200 上打开应用：http://localhost:4200/。运行带有 open 标志的 ng serve 命令。> ng serve --open 你应该能在浏览器中看到运行的 dapp，如图 9-4 所示。![../images/475651_1_En_9_Chapter/475651_1_En_9_Fig4_HTML.jpg](img/475651_1_En_9_Fig4_HTML.jpg)

图 9-4

在浏览器中运行的 Angular 种子应用

骨架应用包含了通往教程、文档和一个 Angular 博客的链接。通过浏览“英雄之旅”和 CLI 文档，你可以很好地理解 Angular 是如何工作的，收藏 Angular 博客可以让你了解未来的版本更新和公告。

要在终端中停止应用程序的运行，请按 Command+C。

##### 在 WebStorm 中的 Angular 项目

启动 Angular 种子项目的另一个选项是使用 WebStorm IDE，你已经在之前的章节中使用过了。WebStorm 允许你导入用 Angular CLI 创建的种子项目，或者创建一个新的种子项目。

要导入使用 Angular CLI 的 ng new 命令创建的 ethdapp 项目，请打开 WebStorm，选择文件➤打开，然后导航到 ethdapp 目录。就这样；WebStorm 将自动导入该项目。

或者，要在 WebStorm 中启动新的 Angular 种子项目，请从顶部菜单选择文件➤新建➤项目。接下来，选择 Angular CLI 并命名你的项目**ethdapp**。使用下拉菜单选择 Angular CLI 的版本，如图 9-5 所示。![../images/475651_1_En_9_Chapter/475651_1_En_9_Fig5_HTML.jpg](img/475651_1_En_9_Fig5_HTML.jpg)

图 9-5

在 WebStorm 中生成 Angular 种子项目

项目创建完成后，你可以运行同样的命令，利用 WebStorm 底部菜单中的终端标签页，如图 9-6 所示。> ng serve –open![../images/475651_1_En_9_Chapter/475651_1_En_9_Fig6_HTML.jpg](img/475651_1_En_9_Fig6_HTML.jpg)

图 9-6

在 WebStorm 的终端中运行 ethdapp

你可以从书籍仓库下载骨架应用程序：[`github.com/Apress/the-blockchain-developer/chapter9/step1.zip`](https://www.scala-sbt.org/1.x/docs/Installing-sbt-on-Windows.html) 。

当你下载你的步骤时，确保你运行了 npm install，因为我去掉了 node 模块来减小项目的大小。> npm install

### 注意

我排除了包含项目所有依赖的 node_modules 目录。由于其大小，通常不将其包含在项目中；你可以使用 npm install 命令来安装它。

##### 确保 Angular CLI 版本无冲突

你可以使用 WebStorm 或通过 ng 命令来创建你的 Angular 种子项目，你需要检查全局 Angular CLI 与本地项目 Angular CLI 是否有冲突。这可能发生在设置指向以前版本的文件时，或者你可能以前用过较老版本的 Angular。发生的情况是，你的本地项目 Angular 显示的版本比计算机上安装的全局 Angular CLI 要老。

为了确保这不是情况，运行任何 ng 命令，如果存在这个问题，您将看到以下错误消息：> ng 您的全局 Angular CLI 版本（7.3.9）大于您的本地版本（6.2.9）。使用本地 Angular CLI 版本。如果您继续使用这些设置，您将运行 6.x 版本而不是 7.x 版本。要解决这个问题，您需要做的是从您的开发环境中卸载 Angular CLI，然后安装 7.x 版本。> npm uninstall --save-dev angular-cli> npm install --save-dev @angular/cli@7.3.9 注意您使用--save-dev 标志，以便新版本将保存在您的 package.json 项目文件中。现在如果您再次运行版本命令，您应该看到没有警告消息的正确版本。> ng --versionAngular CLI: 7.3.2

现在您已经确保您正在运行正确的 Angular CLI 版本，您可以继续开发并修改种子启动应用。

#### Angular 组件

一个 Angular 的最佳实践是使用模型-视图-控制器（MVC）风格的架构。Angular 像其他任何成熟的框架一样，支持用关注点分离的方式编写代码。

Angular MVC 包括以下三个元素：

+   *模型*：这包含应用程序的数据和 Angular 数据绑定，允许数据的反射。

### 注意

与数据绑定相关的反射，绑定到数据的元素和任何数据变化都会自动反映。例如，您将价格变化绑定到多个视图元素，一旦价格变化数据被更新，所有视图元素都会自动更新。

+   *视图*：这包含 HTML 或模板和指令。

+   *控制器*：这是将模型和视图粘合在一起的胶水。控制器获取数据，应用业务逻辑，并将结果发送给视图。

正如您可能回忆到的，当您运行 serve 命令时，Angular 的欢迎页面打开了。欢迎组件是应用的外壳。这个外壳是由一个名为 AppComponent 的 Angular 组件控制的。

组件是 Angular 应用的基本构建块。它们在屏幕上显示数据，监听用户输入，并根据这些输入采取行动。

您将创建一个名为 transfer 的组件，用于将硬币转移到另一个地址。要创建 transfer 组件，请运行 ng generate component 命令。> ng g c components/transfer

请注意，您使用了代表“生成”和“组件”的快捷键 g 和 c，但您也可以使用缩写的全名。

ng 命令为您生成了以下四个文件：

+   transfer.component.css：组件特定的 CSS 样式

+   transfer.component.html：用 HTML 编写的组件模板

+   transfer.component.spec.ts：测试文件

+   transfer.component.ts：用 TypeScript 编写的组件类代码。

这四个文件共同构成了传输组件的实现。你可以查看图 9-7 中的文件结构！../images/475651_1_En_9_Chapter/475651_1_En_9_Fig7_HTML.jpg

图 9-7

传输组件文件结构

一个应用的结构通常由头部、底部和导航菜单组成，这样你就可以导航到不同的部分视图。

使用这种头部和底部组件架构可以帮助你创建不同的视图，并将页面视图分割成单独的文件。把每一部分看作是一个独立的、可重复使用的 UI 模块。Angular Seed 提倡这种架构，并且已经包含了欢迎组件。让我们创建一个开始组件、一个头部和一个底部组件。> ng g c components/start> ng g c components/header> ng g c components/footer 你可以在输出中看到，每个组件生成了以下文件：CREATE src/app/components/[component-name]/[component-name].component.cssCREATE src/app/components/[component-name]/[component-name].component.htmlCREATE src/app/components/[component-name]/[component-name].component.spec.tsCREATE src/app/components/[component-name]/[component-name].component.ts

除了这些文件，你可以打开 ethdapp/src/app/app.module.ts，并注意每次创建一个组件时 app.module.ts 文件都被修改了。app.module.ts 文件是 Angular 中最重要的文件之一；它是用 TypeScript 编写的应用控制器。控制器是一个全局文件，将你的组件联系在一起，所以你的每个应用中想要使用的组件都需要在文件中定义。如果你没有使用 ng 脚本，你需要自己修改 app.module.ts 以链接到新的组件。

由于你使用了命令行界面（CLI），这些导入自动为你包含：*import* { TransferComponent } *from* './components/transfer/transfer.component';*import* { StartComponent } *from* './components/start/start.component';*import* { HeaderComponent } *from* './components/header/header.component';*import* { FooterComponent } *from* './components/footer/footer.component';

#### 路由模块

另一个重要的文件，以及一个良好的创建实践，是创建一个 app-routing 模块。这个文件作为控制器，指导 Angular 如何导航到应用中的不同视图。

通常，为了为你的应用生成路由，你不需要手动操作，因为在创建你的应用时，你已经决定创建一个名为 app-routing 的路由文件。

如果你需要创建 app-routing 文件，你可以运行以下模块命令：> ng generate module app-routing --flat --module=appCREATE src/app/app-routing.module.tsUPDATE src/app/app.module.ts

注意这次在你的命令中，你使用的是生成模块的全名，而不是只是 g 和 m 的首字母。这两个选项工作方式相同。

`generate module`命令为`src/app/app-routing.module.ts`创建了初始代码，如列表 9-1 所示。`import` { NgModule } `from` '@angular/core';`import` { Routes, RouterModule } `from` '@angular/router';`const` routes: Routes = [];@NgModule({  declarations: [],  imports: [RouterModule.forRoot(routes)],  exports: [RouterModule]})`export class` AppRoutingModule `{ }`列表[9-1]。

`app-routing`的初始启动代码。

初始代码包括一个导入 Angular 代码和模块标签的`import`语句。接下来，用列表 9-2 中的代码替换`app-routing.module.ts`文件中的预填充代码。`import` { NgModule } `from` '@angular/core';`import` { CommonModule } `from` '@angular/common';`import` { RouterModule, Routes } `from` '@angular/router';`import` { StartComponent } `from` './components/start/start.component';`import` { TransferComponent } `from` './components/transfer/transfer.component';const routes: Routes = [  { path: '', redirectTo: '/start', pathMatch: 'full' },  { path: 'start', component: StartComponent },  { path: 'transfer', component: TransferComponent }];@NgModule({  declarations: [],  imports: [ RouterModule.forRoot(routes), CommonModule ],  exports: [ RouterModule ]})`export class` AppRoutingModule `{ }`列表[9-2]。

`app-routing`路由视图的代码。

在列表 9-2 中，你导入了你将要使用的视图组件；这些是`start`和`transfer`。它们将作为网站上的网页或移动应用上的部分视图。路由告诉你的应用如何将视图与关键词匹配，最后你设置导入语句以告诉 Angular 谁可以访问这个模块。

现在路由设置完成了，你可以让页面的页脚、页头和主体显示出来。你只需要打开`src/app/app.component.html`文件，从欢迎页面的 HTML 代码更新到以下三行：`<app-header></app-header><router-outlet></router-outlet><app-footer></app-footer>`。为了测试你对应用程序所做的更改，你不需要再次发布你的应用或运行任何脚本；只需保存文件并运行你在终端中之前运行过的相同的`serve`命令。`ng serve`命令成功编译后，会显示`wdm: Compiled successfully.`。

`serve`脚本包括监控文件变化并自动更新你的应用的脚本，所以当你对你的文件做出更改时，你只需要回到浏览器。大多数时候你甚至不需要刷新你的网页；更改会自动出现。访问`http://localhost:4200`以查看更改。

如果你想要直接转到转账页面，你只需要在设置路由机制时在 URL 末尾添加你选择的关键词：`http://localhost:4200/transfer`。见图 9-8。![../images/475651_1_En_9_Chapter/475651_1_En_9_Fig8_HTML.jpg](img/475651_1_En_9_Fig8_HTML.jpg)。

图 9-8。

以太坊应用的页脚、页头和转账页面。

你可以从这里下载这个步骤：[`github.com/Apress/the-blockchain-developer/chapter9/step2.zip`](https://www.scala-sbt.org/1.x/docs/Installing-sbt-on-Windows.html) 。

### 为 Angular 应用程序设置样式

此时，你的应用程序没有样式，只显示带有标题、页面和页脚的文本；然而，在你开始样式设计之前，了解 Angular 样式架构是有帮助的，以确保你不会最终创建一个太大而难以管理的 Cascading Style Sheets (CSS)文件。你可以为整个应用程序设置全局样式，以及只适用于一个组件的独特样式。

此外，快速从零开始构建一个有样式的应用程序会很有趣。这可以通过 Angular Material 实现。Angular Material 为你提供了一个捷径，让你无需考虑跨浏览器、跨设备编程的所有麻烦，就能为你的应用程序带来一致的“外观”。让我们来看看。

#### Angular 样式架构

Angular 设置了一个全局 CSS 文件。这个 CSS 文件叫做 style.css，你可以在项目的根目录中找到它。src/style.css 文件包含了你想要为整个应用程序使用的样式，例如字体、主题、所有组件的样式等。

正如你所见，每个组件还包括一个私有的 CSS 文件。特定组件的 CSS 文件是你放置只用于该组件的独特样式的地方。

例如，/src/app/components/footer/footer.component.css 文件包含了特定于页脚组件的样式。

#### Angular Material

目前，你的起始应用程序很快，因为它包含了最少的代码；然而，随着你添加越来越多的组件、资产和样式，你的应用程序可能会存在潜在的性能问题。你的应用程序很容易变得庞大，每一毫秒的延迟都很重要。

另一个潜在的问题是测试。所有不同的浏览器、浏览器的不同版本、屏幕尺寸和设备都需要进行测试，从头开始创建你的页面将需要严格的测试和质量保证（QA）团队，以确保它在一系列设备上都能保持一致性工作。

Angular Material 解决了所有这些问题，并提供可访问性和国际化功能。这是因为 Angular Material 针对 Angular 进行了优化，由 Angular 团队构建，因此它与 Angular 无缝集成。它已经通过了所有这些兼容性测试。

有关更多信息，请查看 Angular Material 入门页面：[`material.angular.io/guide/getting-started`](https://material.angular.io/guide/getting-started) 。

#### 安装 Angular Material

安装 Material 有几种方法。因为你已经安装了 Angular DevKit，所以你可以运行 ng add 命令来获取 Angular Material 库。你需要先安装 cdk，因为它是一个依赖。> ng add @angular/cdkNext，安装 Material。> ng add @angular/material 注意输出会询问你想要哪种主题颜色以及相应的链接。我将在本章的下一节中介绍主题，但现在，选择第一个或你喜欢的任何颜色。? 选择一个预设的主题名，或者"custom"用于自定义主题：（使用箭头键）□ Indigo/Pink [预览：https://material.angular.io?theme=indigo-pink]  Deep Purple/Amber [预览：https://material.angular.io?theme=deeppurple-amber]  Pink/Blue Grey [预览：https://material.angular.io?theme=pink-bluegrey]  Purple/Green [预览：https://material.angular.io?theme=purple-green]你还可以设置手势识别和动画。? 为手势识别设置 HammerJS？ 是? 为 Angular Material 设置浏览器动画？ 是预期的输出应该显示被更新的文件：UPDATE package.jsonUPDATE angular.jsonUPDATE src/app/app.module.tsUPDATE src/index.htmlUPDATE src/styles.css

#### 导入 Angular Material 模块

接下来，你希望修改你的应用，使其包含 Angular Material 的动画、Material 图标、手势支持和组件模块。

在你的项目中，你将只使用组件模块，并不会使用 Angular Material 提供的所有功能；你需要做的是为每个你想使用的组件导入 NgModule。打开 src/app/app.module.ts，并添加导入语句。import {  MatButtonModule,  MatCheckboxModule,  MatInputModule,  MatSelectModule,  MatDatepickerModule,  MatNativeDateModule} from '@angular/material';接下来，更新@NgModule 的导入语句，包含你导入的 Material 模块。imports: [    BrowserModule,    AppRoutingModule,    BrowserAnimationsModule,    MatButtonModule,    MatInputModule,    MatDatepickerModule,    MatNativeDateModule,    MatCheckboxModule,    MatSelectModule  ]

就是这样。现在你可以访问你包含的 Angular Material 组件了。

#### 主题你的 Angular Material 应用

既然你已经可以访问 Angular Material 组件了，你可以使用主题来为它们设置样式。*主题*是一组颜色，将用于你的 Angular Material 组件。

在 Angular Material 中，通过创建多个调色板来创建一个主题。

+   *主调色板*：这些颜色在所有屏幕和组件中最常使用。

+   *强调调色板*：这些颜色用于按钮和交互元素。

+   *警告调色板*：这些颜色用于错误。

+   *前景调色板*：这些颜色用于文本和图标。

+   *背景调色板*：这些颜色用于元素的背景。

在 Angular Material 中，所有主题样式在构建时静态生成，以避免在应用启动时减慢应用速度。

Angular Material 随附了几个预构建的主题 CSS 文件。正如你可能记得的，当你安装 Material 时，你有一个选择主题的机会。

这些主题文件包含了所有核心样式（所有组件共有的样式），因此你只需在你的应用程序中包含一个 Angular Material 的 CSS 文件。你可以直接从@angular/material/prebuilt-themes 中把主题文件引入到你的应用程序中。

以下是可用的预构建主题：

+   deeppurple-amber.css

+   indigo-pink.css

+   pink-bluegrey.css

+   purple-green.css

你在这里使用的是 Angular CLI，所以你只需在全球 src/styles.css 文件中包含你想要的样式。

原始的初始预代码是这样的：html, body { height: 100%; }body { margin: 0; font-family: 'Roboto', sans-serif; }在文档顶部添加以下导入语句：@import "~@angular/material/prebuilt-themes/indigo-pink.css";在你打开 src/style.css 文件的同时，你还可以为容器、段落和按钮创建一个样式，这样你就可以在整个应用程序中为你的页面使用这些样式。p {  padding-left: 20px;  font-size: 12px;}.container {  margin-right: auto;  margin-left: auto;  padding: 20px 15px 30px;  width: 750px;}.button {  color: #ffffff;  background-color: #611BBD;  border-color: #130269;  display: inline-block;  margin-bottom: 0;  font-weight: normal;  text-align: center;  vertical-align: middle;  touch-action: manipulation;  cursor: pointer;  white-space: nowrap;  padding: 6px 12px;  font-size: 12px;  line-height: 1.42857143;  border-radius: 4px;  -webkit-user-select: none;  -moz-user-select: none;  -ms-user-select: none;  user-select: none;}.

你可以和你我的文件进行比较：[`github.com/Apress/the-blockchain-developer/chapter9/step3.zip`](https://www.scala-sbt.org/1.x/docs/Installing-sbt-on-Windows.html) 。

### 创建内容

至此，你已经有一个带有头部、身体和脚部的骨架应用程序。通过在浏览器中更改 URL，身体可以在起始页面和转移页面之间切换。你还导入了并注入了 Material 模块，为你的应用程序设置了全局样式。下一步是创建实际内容来替换你放在头部、脚部和起始组件中的临时文本消息。

#### 页脚组件

对于页脚组件，你只需替换你公司版权的信息。为此，你只需要打开 src/app/components/footer/footer.component.html 文件，并替换默认代码。<p>  footer works!</p>用你在全局 CSS 文件中添加的样式创建一个 div 容器替换代码。<div class="ng-scope">  <div class="container">    <p>Copyright (c) 2019 公司名称。保留所有权利。</p>  </div></div>你还将为页脚组件创建一个特定的样式，所以每次你使用 p 标签时，你的字体大小将是 12px，并且左边没有内边距。打开 src/app/components/footer/footer.component.css 并插入以下内容：p {  padding-left: 0;  font-size: 11px;}.

请注意，您在全局 CSS 文件和组件级别定义了两次`<p>`标签。发生的情况是全局`<p>`标签将被组件`<p>`覆盖，因此您可以在页脚中使用`<p>`标签，为开始和转账页面等其他组件使用不同的`<p>`标签，同时保持 HTML 代码中不包含 CSS 代码。

#### 头部组件

对于头部组件，您将创建一个导航菜单，以便能够在开始页面和转账页面之间进行切换。对于头部组件特定的样式，请打开`src/app/components/header/header.component.css`，并添加导航列表样式。.nav {  margin-bottom: 0;  padding-left: 0;  list-style: none;}li {  display: block;  float: left;  width: 100px;  height: 25px;  padding: 5px;}.nav>li>a {  margin-bottom: 0;  padding-left: 0;  font-weight: 500;  font-size: 12px;  text-transform: uppercase;  position: relative;}对于`src/app/components/header/header.component.html`，您创建一个容器和一个到页面开始和转账的链接列表。为此，将初始代码：<p>  header works!</p>替换为以下内容：<div class="ng-scope">  <div class="container">    <ul class="nav">      <li>        <a routerLink='/start'>home</a>      </li>      <li>        <a routerLink='/transfer'>transfer</a>      </li>    </ul>  </div></div>现在，运行中的 dapp 包括了基本的样式和功能导航，如图 9-9 所示！../images/475651_1_En_9_Chapter/475651_1_En_9_Fig9_HTML.jpg

图 9-9

具有基本样式和导航功能的 Ethdapp

您可以在此处下载此步骤：[`github.com/Apress/the-blockchain-developer/chapter9/step4.zip`](https://www.scala-sbt.org/1.x/docs/Installing-sbt-on-Windows.html)。

#### 转账组件

转账组件将包含一个表单，您将提交该表单以将以太坊硬币从一个账户地址转移到另一个。您将使用表单模块来加速创建您的表单。为此，您需要在`app.module.ts`中包含 Material FormsModule 和 ReactiveFormsModule 表单模块，就像您对其他 Material 模块所做的那样。

打开`src/app/app.module.ts`并添加以下导入语句：import { FormsModule, ReactiveFormsModule } from '@angular/forms';您还需要更新导入语句。  imports: [    FormsModule,    ReactiveFormsModule,    ..]

您将使用`<mat-form-field>`标签，该标签代表一个包装多个 Angular Material 组件并应用常见文本字段样式的组件，如下划线、浮动标签和提示信息。这将加快开发速度，因为您不需要实现所有这些并测试它们在多种设备/浏览器上。

表单字段是名为`<mat-form-field>`的包装组件。您可以使用任何表单字段控件（如输入、文本区域、列表等）。

你可以在这里找到关于 mat-forms 的信息：[`material.angular.io/components/form-field/overview`](https://material.angular.io/components/form-field/overview) 。

对于`src/app/components/transfer/transfer.component.ts`，你需要更新初始代码。首先，你需要导入你将要使用的组件；在这个案例中，你需要初始化类并使用表单、表单控制和验证器。```typescript

请注意你已经使用了`transfer-container`样式，你还没有定义它；你将在你的 CSS 文件中定义它，并用来格式化你的表单。

对于表单控件，你需要为你要转账的账户、金额和一个消息输入框，你还需要设置你的验证。

图 9-10。

包含用户信息、验证器和提交按钮的 Ethereum DApp 转账页面。

你可以在这里下载这个步骤：[`github.com/Apress/the-blockchain-developer/chapter9/step5.zip`](https://github.com/Apress/the-blockchain-developer/chapter9/step5.zip)。

#### Angular 指令。

在 Angular 中创建指令为你提供了通过几行代码创建你自己的自定义 HTML 标签的能力，正如你在 Material 表单中看到的那样。你能够包含许多组件的自定义标签。在高级层面上，指令是 DOM 元素上的标记。

这些标记可以指向任何 DOM 组件，从属性到元素名称，甚至是注释或 CSS 类。这些标记然后告诉 AngularJS 的 HTML 编译器附加一个指定的行为，或者根据特定逻辑将整个 DOM 元素及其子元素转换。

Angular 自带了许多这些指令。然而，在开发过程中，你很可能会创建你自己的指令。你的 dapp 现在很简单，所以你不需要创建任何指令，而且这超出了本章节的解释范围。当你需要生成一个骨架指令时，就像你生成其他组件一样使用 Angular CLI。> ng generate directive {directive-name}

尽管你在你的应用中没有创建指令，但我还是想向你介绍这个概念，因为它是创建 Angular 项目的一个组成部分。

## 总结

在本章节，你深入了解了什么是 dapp，并查看了 dapp 的分类和项目。你学习了如何通过五个步骤开始你自己的 dapp 项目：编写白皮书，启动 ICO，开发 dapp，启动它，以及推广你的 dapp。

然后你了解了为什么使用 Angular。接下来，你创建了一个 Angular dapp，首先确保预先安装了必备条件并安装了 Angular CLI。然后你创建了一个 Angular 项目并服务了应用程序。

接下来，你学习了如何将你的 Angular 项目导入 WebStorm 或创建一个新的项目。你查看了使 Angular 成为可能的部分，比如组件、模块和指令。你还学会了如何通过理解 Angular 风格架构和与 Angular Material 一起工作来样式化 dapp。

你开始构建组件并创建内容；你将你的应用分为页脚、页头和主体，并创建了一个名为 transfer 的自定义组件，其中包含了一个表单，以便后来转移代币。

在下一章节，你将创建一个转移智能合约和一个 Truffle 开发项目，以及连接到 Ganache 开发网络。你将学习如何通过 Truffle 与以太坊网络交互，并测试你的智能合约。你还将把你的 dapp 与以太坊网络的 web3 库链接起来，并通过 MetaMask 进行连接。
