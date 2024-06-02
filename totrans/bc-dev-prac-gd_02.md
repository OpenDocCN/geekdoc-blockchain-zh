© Elad Elrom 2019 Elad Elrom 区块链开发者[`doi.org/10.1007/978-1-4842-4847-8_2`](https://doi.org/10.1007/978-1-4842-4847-8_2)

# 2. 区块链节点

Elad Elrom^(1 )（1）纽约，纽约，美国

在上一章中，我介绍了与区块链相关的基本概念和构成单个区块链的各个部分。我介绍了区块链技术如何通过利用 P2P 网络来解决双重支付问题，从而创建了一个全球分布式共享账本和数字货币。区块链 P2P 网络通过连接多个节点而成，在本章中，你将深入了解构成网络的节点。

节点或对等体是维护区块链网络上交易和记录的机器。每种加密货币都有自己的区块链和节点；然而，我将介绍如何安装三种使用不同共识机制的区块链。

此外，我还将介绍如何与节点进行交互。我将使用比特币核心 API 作为例子，以便你更好地理解账本、区块、交易和钱包。这些概念将继续为接下来的章节打下基础和基本概念。

## 运行区块链节点

正如我们提到的，区块链 P2P 网络由存储网络中所有块的完整副本的节点组成，这就是共享账本。每个区块链通过特定的共识机制验证块，并能够拒绝不符合网络达成一致的规则的块。为了能够连接到块并执行命令，你需要有一个与区块链连接的节点。在本章中，你将设置一个完整节点，并学习如何为帮助网络获得奖励；因此，你将完全理解不同网络上节点的运作方式。你将为以下区块链创建节点：比特币、NEO 和 EOS。由于区块链技术在不同的共识机制上运行，它们对于能够管理区块链的节点也有不同的名称。

+   对于比特币来说，能够创建块的节点被称为*矿工*。

+   对于 NEO 来说，拥有管理权的节点被称为*记账节点*。

+   对于 EOS 来说，运行底层网络层并能够处理所有交易的节点被称为*区块生产者*。

我选择这些区块链的原因是，你可以研究不同节点在不同网络上使用不同共识机制是如何运作的。一旦你能够处理不同的区块链，你将开始注意到一个模式，并在区块链技术方面变得全面。

### 创建比特币矿工

在本节中，您将把自己的电脑变成一个比特币矿工并开始挖矿。在这样做之前，您需要明白，您的电脑的哈希能力所产生的哈希功率不足以使比特币挖矿产生利润。尽管如此，它将使您全面了解整个流程，您可能还能找到其他使用 CPU/GPU 挖矿可以产生利润的硬币，如 ETN、BCN、XMR 和 ETH。所有基于 PoW 的网络过程都相似。

如今，要使矿工产生利润，关键在于哈希率、功耗、电力价格、比特币谜题难度率以及维护成本等因素。

### 注意

*哈希率*是您的计算机每秒可以执行的计算次数，试图解决数学难题。

在比特币的早期阶段，您的桌面电脑可以使用中央处理单元（CPU）或图形处理单元（GPU）来处理比特币，这足以使比特币挖矿产生利润。您的电脑能够支持比特币网络；然而，竞争加剧，您现在需要一个现场可编程门阵列（FPGA）或应用特定集成电路（ASIC）矿工才能产生利润。

ASIC 和 FPGA 矿工是什么？ FPGA 是一种在构建后可以配置的集成电路。与 CPU 和 GPU 挖矿相比，矿工的性能更好；它们每秒可以哈希运算 750 兆次。

ASIC 是一种计算机，其集成电路专门用于执行挖矿任务，而不是像普通计算机那样运行。该计算机上没有其他东西；其他所有东西都被去除了。

这使得计算机在处理交易时变得更快更有效率，并且能够进行更多的哈希运算。在撰写本文时，有 ASIC 芯片的哈希速度超过了 56 TH/s，而且它们的功耗比上一代 ASIC 芯片要低。

这种挖矿设备不仅限于比特币；在撰写本文时，还有针对其他加密货币（如莱特币、Zcash、以太坊等）的 ASIC 矿工。

开始之前，您首先需要挖矿软件。有很多挖矿软件供您选择。例如，macOS 用户可以选择这个免费、开源且易于使用的软件：[`downloads.fabulouspanda.co.uk/macminer/`](http://downloads.fabulouspanda.co.uk/macminer/)。

一旦下载了软件，就要安装它。接下来，您需要加入一个挖矿池。在这里，我将介绍如何连接到 Antpool，最大的比特币池；然而，任何池都可以使用。在 Antpool 上注册： [`www.antpool.com`](https://www.antpool.com)。

Antpool 将矿工称为 *工人*。 您可以通过点击仪表板选项卡，然后点击矿工链接，最后点击创建工人，如图 2-1 所示！../images/475651_1_En_2_Chapter/475651_1_En_2_Fig1_HTML.jpg

图 2-1

Antpool 创建矿工工人页面

现在你的工人已经准备好了，你将把你的矿工设置为利用 CPU 的 CPU 矿工，对于你的 GPU，你可以将你的矿工设置为利用你的显卡。

打开你下载的 MacMiner 软件，然后点击文件然后从文件下拉菜单中选择偏好选项。在偏好设置部分，将矿工设置为 CPU 和/或 GPU 矿工，如图 2-2 所示。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig2_HTML.png](img/475651_1_En_2_Fig2_HTML.png)

图 2-2

MacMiner 偏好设置

在偏好设置的下一步，你设置了池 URL 和你的用户名。Antpool 设置时没有密码，所以不需要，池 URL 列在 Antpool 网站上：startum+tcp://startum.antpool.com:3333。见图 2-3 。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig3_HTML.png](img/475651_1_En_2_Fig3_HTML.png)

图 2-3

MacMiner 设置矿工池窗口

就这样。点击开始按钮开始挖掘，点击停止按钮停止挖掘，如图 2-4 所示。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig4_HTML.jpg](img/475651_1_En_2_Fig4_HTML.jpg)

图 2-4

MacMiner 启动矿工

六年前，你完全可以用你的 GPU 挖掘超过 100 个 BTC。正如你所见，我的 2018 年 MacBook 矿工算力只有 13.74 Mh（兆哈希）。

网上有很多资源可以帮助你计算挖矿盈利能力；试试 [`www.bitcoinx.com/profit/`](http://www.bitcoinx.com/profit/) 。如预期的那样，根据他们的计算，在当前条件下是没有盈利的。

### 创建 NEO 记账节点

之前我介绍过 NEO 作为一种流行的 PoS 区块链的例子。

在本节中，你将设置一个节点（NEO 称之为*记账节点*）并让机器准备好，以便被选中协助管理网络并获得交易奖励。

### 注意

NEO 不将其管理节点称为矿工。矿工可以是对节点为维护基于 PoW 的区块链所做的艰苦工作的一种比喻。由于 NEO 使用 PoS 普查算法并使用技术民主来选择管理节点，使用 PoW 普查算法时没有算力，也没有艰苦的劳动。为了更好地了解 Neo 节点的工作原理，建议阅读 NEO 白皮书，地址为 [`github.com/neo-project/docs/blob/master/en-us/whitepaper.md`](https://github.com/neo-project/docs/blob/master/en-us/whitepaper.md) 。

节点验证区块链区块并支付一种名为 *gas* 的加密货币币。为了被选中，你需要在一台有能力的机器上设置一个完整节点。要求的最低机器配置列在 NEO 项目维基上，地址为 [`github.com/neo-project/neo/wiki/Bookkeeping-Node-Deployment`](https://github.com/neo-project/neo/wiki/Bookkeeping-Node-Deployment) 。

接下来，您需要获得一个共识权威证书并获得质押气体以被提名为记账节点。

### 注意

您可能需要是中国公民并设立一家中国公司以获得身份证书；请参阅 NEO 文档：[`docs.neo.org/en-us/index.html`](http://docs.neo.org/en-us/index.html) 。您还需要 1000 个质押气体以被提名为记账节点。

要从支持 NEO 网络中收到费用，您需要按照这些步骤创建一个完整节点：

1.  1.

    设置一个完整的 NEO 节点。

1.  2.

    请求一个共识权威证书。

1.  3.

    锁定 1000 个气体。

1.  4.

    被 NEO 持有者选举。

要设置一个完整的 NEO 节点，您还需要满足此处列出的系统最低要求：[`github.com/neo-project/neo/wiki/Bookkeeping-Node-Deployment`](https://github.com/neo-project/neo/wiki/Bookkeeping-Node-Deployment) 。

#### 在 AWS 上设置 NEO Ubuntu 节点

由于我的计算机不满足最低要求列表，我将使用 AWS 设置一个完整节点。但是，如果您有满足这些要求的计算机，可以自由选择使用亚马逊 AWS 或选择其他服务提供商来设置您的节点。

对于 AWS，请访问以下网址：[`aws.amazon.com/free/`](https://aws.amazon.com/free/) 。选择“创建免费账户”并注册。

完成注册过程后，选择免费的基础计划。然后登录到[`us-east-2.console.aws.amazon.com/console/home`](https://us-east-2.console.aws.amazon.com/console/home)控制台并选择“启动虚拟机。”

在第一步中，您可以选择机器类型。选择 Ubuntu。“在第一步向导页面：选择一个亚马逊机器镜像（AMI）” ➤ 下一步，选择：Ubuntu Server 16.04 LTS（HVM），SSD 卷类型 ➤ 点击“选择”按钮。见图 2-5。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig5_HTML.jpg](img/475651_1_En_2_Fig5_HTML.jpg)

图 2-5

AWS，选择 Ubuntu Server 16.04 LTS

在下一页，选择通用目的 - t2.micro - 免费层可用的复选框。见图 2-6。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig6_HTML.jpg](img/475651_1_En_2_Fig6_HTML.jpg)

图 2-6

AWS，选择 t2.micro 机器

在下一页，您将提示创建密钥对：选择“创建新的密钥对” ➤ 下一步，选择“密钥对名称” ➤ 给密钥命名为“neo” ➤ 然后下载密钥：“下载密钥对” ➤ 最后选择“启动实例。”见图 2-7。确保您下载了密钥，因为没有密钥，您将无法连接到没有密钥的 SSH 盒子。

### 注意

安全外壳（SSH）使用端口 22 将您的计算机连接到互联网上的另一台计算机。

![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig7_HTML.jpg](img/475651_1_En_2_Fig7_HTML.jpg)

图 2-7

AWS 密钥对

接下来，您将收到一条消息，带有一个链接：您的实例现在正在启动。已启动以下实例：[实例 id]。

点击链接后，您将能够查看实例，如图 2-8 所示。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig8_HTML.jpg](img/475651_1_En_2_Fig8_HTML.jpg)

图 2-8

AWS，启动实例

在实例中，您会找到一个安全设置的链接。将屏幕向右滚动，或者前往顶部左侧导航栏，选择网络与安全➤安全组。您将能够更改安全设置。

对于 HTTP 和 SSH，您需要向世界开放端口（0.0.0.0/0），但 SSH 将限制您只能连接到自己的计算机，称为我的 IP。参见图 2-9。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig9_HTML.jpg](img/475651_1_En_2_Fig9_HTML.jpg)

图 2-9

AWS 入站安全规则

接下来，您可以创建一个 SSH 快捷方式，通过一个命令访问服务器，如下所示：> mkdir ~/.ssh> vim ~/.ssh/config 将以下内容粘贴到配置文件中：Host NEOHostName [ip address]User ubuntuIdentityFile /[location of key]/neo.pem 将这些设置与机器的 IP 地址和您的密钥位置配置好。接下来设置密钥的权限。> chmod 400 /[location of key]/neo.pem 现在，您可以使用一个命令访问您的机器，如图 2-10 所示。> ssh NEO![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig10_HTML.jpg](img/475651_1_En_2_Fig10_HTML.jpg)

图 2-10

通过 SSH 连接到 AWS 机器

如果您在连接机器时遇到任何问题，请使用 AWS 故障排除页面，您可以在[`docs.aws.amazon.com/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html#TroubleshootingInstancesConnectingMindTerm`](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html%2523TroubleshootingInstancesConnectingMindTerm)找到。

#### 在 Ubuntu 16.04 上安装 Bookkeeping-Node-Deployment

既然你已经有一台满足完整节点最小需求的机器，你可以安装所需的软件。首先安装依赖项，如下所示：`sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'` `sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893` `sudo apt-get update` `sudo apt-get install dotnet-dev-1.0.4`看起来 NEO 文档中的当前安装说明在安装过程中会产生错误，如下所示：Depends:dotnet-sharedframework-microsoft.netcore.app-1.0.4, dotnet-sharedframework-microsoft.netcore.app-1.1.1 解决方法是安装一个不同的 dotnet core 环境源列表并更新，然后你将能够安装 dotnet-dev-1.0.4 核心环境。`sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'` `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893` `sudo apt-get update`记得将源列表改回以下内容：`sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'`现在 dotnet core 环境已经安装，使用以下命令检查 dotnet core 环境是否成功安装：`mkdir hwapp` `cd hwapp` `dotnet new xunit --framework netcoreapp1.1` `dotnet restore hwapp.csproj` `dotnet run` `cd ..` `rm -rf hwapp/`

#### 记账节点部署

既然你已经安装了 dotnet core 环境，你可以安装额外的依赖项并检出 NEO 项目。`sudo apt-get install libleveldb-dev sqlite3 libsqlite3-dev libunwind8-dev` `git clone https://github.com/neo-project/neo-cli` `git branch -a` `git checkout v3.0` `git checkout head`

要运行 NEO 节点，你需要.NET Core 的 1.1.2 版本。下载 SDK 二进制文件；对于 Ubuntu 16.4，命令如下：[`www.microsoft.com/net/download/linux-package-manager/ubuntu16-04/sdk-2.1.300`](https://www.microsoft.com/net/download/linux-package-manager/ubuntu16-04/sdk-2.1.300)。

接下来，运行 dpkg 包管理器来安装包：> wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb> sudo dpkg -i packages-microsoft-prod.deb 现在您可以恢复 NEO 构建和编译，如下所示：> dotnet restore> dotnet publish -c Release 一旦编译代码，您就会得到 DLL 的位置。.neo-cli -> /home/ubuntu/neo-cli/neo-cli/bin/Release/netcoreapp2.0/neo-cli.dll。.neo-cli -> /home/ubuntu/neo-cli/neo-cli/bin/Release/netcoreapp2.0/publish/运行完整节点：> dotnet /home/ubuntu/neo-cli/neo-cli/bin/Release/netcoreapp2.0/neo-cli.dll。此命令会打开一个名为“neo”的终端命令行。NEO-CLI Version: 3.0.0.0 在 neo 终端中，您可以查询版本以确认它是否正常工作。neo> show state 您还可以创建一个钱包。neo> create wallet wallet.db3 此命令将要求您输入密码。password: [选择一个密码]password: [选择一个密码]然后它为您钱包生成了公钥和地址。address: AXZmWZckF55xb1p566No2qh19uj8vt5d2R pubkey: 03b80edc66c9324077c8c1c4bbad1e1ace7e1b7e8ac63945a3b5bb9f642f4520f1

您现在在 AWS 机器上有一个 NEO 节点，并且能够与 NEO 命令行界面（CLI）交互。在接下来的章节中，您将与之交互。您可以在这里提前学习并复习智能合约和去中心化应用（DApp）开发的 NEO 文档：[`docs.neo.org/en-us/node/cli.html`](http://docs.neo.org/en-us/node/cli.html)。

#### 请求共识权威证书

如今您在合格的 Ubuntu 服务器上已经有了一个运行中的节点，您可以获取共识权威证书。NEO 白皮书讨论了需要一个真实的实际身份：

> “DBFT 结合了数字身份技术，意味着记账员可以是个人或机构的真实姓名。因此，冻结、吊销、继承、检索以及影响司法决定都是可能的。这有助于在 NEO 网络上注册合规的金融资产。NEO 网络计划在必要时支持此类操作。”

您可以直接从 OnChain/Neo 获取 CA 证书。此外，您还可以在 NEO 论坛上找到更多信息：[`www.reddit.com/r/NEO/`](https://www.reddit.com/r/NEO/)。这个过程超出了本书的范围，但为了被选为节点，它是必需的。

#### 加油

为了被选为节点，您还需要质押 1000 个燃料来成为记账员。购买燃料的最简单方法是交易所。另一种选择是持有 NEO，您将获得 0.33 个燃料/1000。见图 2-11 展示了持有 NEO 硬币时领取燃料硬币的按钮。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig11_HTML.jpg](img/475651_1_En_2_Fig11_HTML.jpg)

图 2-11

Neotracker.io 提供了一个领取燃料（Gas）的选项

简单计算在撰写本文时 NEO 和燃料的价格，显示这是一个巨大的投资。

#### 当选记账节点

NEO 是一个电子民主，NEO 持有者可以投票决定谁应该担任记账员。在撰写本文时，NEO 团队尚未实现投票功能；然而，根据 GitHub wiki 显示的支付结构，包括为投票记账员支付 10 个气体费，这些功能很可能会在未来实现：[`github.com/neo-project/neo/wiki/Network-Protocol`](https://github.com/neo-project/neo/wiki/Network-Protocol) 。

目前，停止 EC2 节点，这样你就不会被收费。

要停止实例，选择 EC2 仪表板 ➤运行中的实例 ➤操作 ➤实例状态 ➤停止。见图 2-12。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig12_HTML.jpg](img/475651_1_En_2_Fig12_HTML.jpg)

图 2-12

AWS，停止实例操作

### 提示

亚马逊可以为附加到已停止实例的 EBS 卷收取存储费用。费用为每千兆字节五美分。亚马逊提供一年免费。为了避免被收费，你需要“终止”实例，而不仅仅是停止它。

你可以通过这个网址确保你不会被收费：[`console.aws.amazon.com/billing/home`](https://console.aws.amazon.com/billing/home) 。

### 创建一个 EOS 区块生产者

你现在将学习如何在专用服务器上运行一个完整的 EOS 节点；你只需要确保满足最低硬件要求。要求如下：[`developers.eos.io/eosio-nodeos/docs/install-nodeos`](https://developers.eos.io/eosio-nodeos/docs/install-nodeos) 。

在撰写本文时，所有平台上的系统要求如下：

+   需要 7 GB RAM 免费

+   20 GB 的可用存储空间

你将学习如何设置一个 Ubuntu 服务器。我将使用 AWS。在 AWS 中，选择 Ubuntu Server 16.04 LTS (HVM)，SSD Volume Type ➤选择实例类型 ➤通用 ➤ t2.large。这种机器有 8 GB RAM 免费。

一个 EOS 节点至少需要 20 GB 的存储空间，所以你会将这个机器设置为 25 GB 以确保安全。为此，选择配置实例详细信息。接下来选择：添加存储。在下一个窗口中选择：大小（GiB）25 GB。在下一个向导窗口中，你可以：查看并启动。启动实例。

为了安全起见，设置与 NEO 完整节点服务器相同的设置：选择一个现有的安全组。接下来，选择：启动向导-1，包括 SSH 的端口 22 和公共 HTTP/HTTPS。现在我们可以：在下一个窗口中查看并启动，最后，启动。

在密钥对中，使用为 NEO 创建的同一个密钥，或者创建一个新的密钥。要选择同一个密钥，选择选择现有密钥对。我们将这个密钥称为：EOS。

就这样。现在，你可以更新 SSH 配置文件，以便能够快速连接新服务器。> vim ~/.ssh/config

#### 安装 EOS 完整节点

现在你已经将 Ubuntu 服务器配置好了 8 GB 的内存和 25 GB 的硬盘，你可以克隆项目并进行构建。> git clone https://github.com/EOSIO/eos --recursive> cd eos> ./eosio_build.sh #大约需要 30 分钟到 1 小时。构建完成后，你会看到图 2-13 所示的屏幕。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig13_HTML.jpg](img/475651_1_En_2_Fig13_HTML.jpg)

图 2-13

EOS 完整节点构建，完整输出

确保守护进程正确运行，通过运行 -h 标志获取命令列表。> cd build/programs/nodeos> ./nodeos -h #命令列表现在你可以运行 EOS 节点守护进程；图 2-14 显示了输出。> ./nodeos -e -p eosio --plugin eosio::chain_api_plugin --plugin eosio::history_api_plugin![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig14_HTML.jpg](img/475651_1_En_2_Fig14_HTML.jpg)

图 2-14

运行 EOS 完整节点

EOS 在 [`developers.eos.io/`](https://developers.eos.io/) 提供了一个门户，开始了解节点、dapps、智能合约、代币等。在接下来的章节中，你将更多地与 EOS 平台互动。

#### 营销和上市

现在你已经运行了一个 EOS 节点，你需要创建一个营销活动以便被选举。你可以将提交配置设置为类似于这个网址： [`github.com/consenlabs/eos-bp-profile`](https://github.com/consenlabs/eos-bp-profile) 。

接下来，你准备接收投票。你可以通过 imToken 2.0 应用程序（iPhone 或 Android）接收投票。它提供区块生产者投票；按照这个指南进行操作： [`medium.com/imtoken/guide-imtoken-2-0-block-producers-voting-141983f9a76e`](https://medium.com/imtoken/guide-imtoken-2-0-block-producers-voting-141983f9a76e) 。

#### 终止 EOS 节点

你需要确保终止节点，这样你才不会被收费，因为这种机器配置不是亚马逊免费层服务器的一部分。就像之前一样，选择 EC2 仪表板 ➤ 运行实例 ➤ 操作 ➤ 实例状态 ➤ 终止。

你还需要终止你创建的 25 GB 卷。从左侧导航菜单中选择卷，然后选择 操作 ➤ 卸载卷。然后选择 删除卷。见图 2-15。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig15_HTML.jpg](img/475651_1_En_2_Fig15_HTML.jpg)

图 2-15

卸载卷和删除卷

## 比特币核心 API

作为一名开发者，你希望深入了解一项技术是如何工作的，为了更好地理解区块链以及比特币区块链，你将下载并安装比特币核心代码。之前在比特币核心上设置的全节点和比特币矿工可以从源代码编译，或者你可以使用预编译的可执行文件。

之前你在计算机上设置了一个能够进行挖矿的比特币节点。为了与比特币核心 API 进行交互，你需要一个完整节点。那么完整节点和矿工之间有什么区别呢？

一个完整节点是区块链的完整副本，能够验证自第一个区块创建以来在区块链上发生的所有交易。这需要 180 GB 的存储空间。然而，正如你所看到的，你可以设置完整节点不下载整个账本。完整节点不需要解决任何数学问题，哈希也不是问题。

矿工是网络中的一个节点；然而，正如你所看到的，它的任务是通过处理交易并找出最佳的区块（或哈希）来存储信息来生成区块。矿工们竞争并花费大约 10 分钟来解决问题。完整节点在数据库中永久保存区块，并与其他节点进行验证。另一方面，矿工不需要了解之前的区块，只需要了解之前的区块，并专注于哈希。然而，比特币矿工确实下载了整个 180 GB 的区块链账本。

在下面的练习中，你将安装和配置一个完整节点，以便能够连接并与比特币核心 API 进行交互。

### 安装和配置比特币全节点

**设置您的系统**

在这个练习中，你将设置你的环境，然后下载、配置并启动一个比特币的全功能节点。这将对你继续研究比特币和区块链的工作原理非常有帮助。你将使用比特币核心源代码。比特币核心代码包括文档，提供了在不同的操作系统上安装代码的完整说明。在这本书中，我重点介绍 macOS，所以我会提供说明以加快安装过程；然而，你可以在其他平台上安装比特币核心。以下是针对 Mac 和 PC 的完整安装说明的链接：

+   macOS 安装说明：[`github.com/bitcoin/bitcoin/blob/master/doc/build-osx.md`](https://github.com/bitcoin/bitcoin/blob/master/doc/build-osx.md)

+   Windows：[`github.com/bitcoin/bitcoin/blob/master/doc/build-windows.md`](https://github.com/bitcoin/bitcoin/blob/master/doc/build-windows.md)

要开始，你需要安装 Xcode 和 Xcode 工具，所以如果你还没有这些工具，现在是安装它们的好时机。要检查 Xcode 是否已安装在你的计算机上，请打开命令行终端，点击 Spotlight 搜索，并输入**Terminal**。

在命令行中，输入以下命令以检查你是否安装了 Xcode：> xcode-select –v 它应该返回 xcode-select 和版本号，如图 2-16 所示。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig16_HTML.jpg](img/475651_1_En_2_Fig16_HTML.jpg)

图 2-16

Terminal xcode-select 版本

如果你还没有安装 Xcode，可以从 [`developer.apple.com/xcode/`](https://developer.apple.com/xcode/) 下载。

**注意**  安装过程可能需要数小时，具体取决于你的网络连接速度。

既然你已经下载了 Xcode，就执行 Xcode 的命令行工具。> xcode-select –install 命令行工具安装后，你可以使用这些命令安装 Homebrew 和 wget：> /usr/bin/ruby -e "$(curl –fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"> brew install wget 安装 Homebrew 和 wget 后，你可以安装比特币核心所需的其余依赖项，如下所示：> brew install automake berkeley-db4 libtool boost miniupnpc openssl pkg-config protobuf python qt libevent qrencode librsvg

**安装比特币核心**

到现在为止，你已经安装了所需的工具和依赖项，可以克隆比特币代码项目，编译并运行它。> git clone https://github.com/bitcoin/bitcoin.git> cd bitcoin/现在，你可以构建比特币核心节点所使用的 Berkeley DB 版本 4：> ./contrib/install_db4.sh .继续安装；> ./autogen.sh> ./configure> make> make check && sudo make install 比特币核心代码包括两个工具：bitcoind 和 bitcoin-CLI。

+   *bitcoind (比特币守护进程)*：这实现了用于远程过程调用（RPC）的比特币协议。一旦安装，你就可以进行 API 调用。这里有一个所有 API 调用的列表：[`en.bitcoin.it/wiki/Original_Bitcoin_client/API_Calls_list`](https://en.bitcoin.it/wiki/Original_Bitcoin_client/API_Calls_list) 。

+   *bitcoin-CLI (比特币命令行界面)*：这使你能够与比特币核心守护进程进行交互。为了确保安装顺利进行，你可以检查比特币守护进程和 bitcoin-CLI 是否配置正确且按预期工作。

为了确保这些工具被正确安装，你可以对这些工具执行 which 命令以获取它们的位置。> which bitcoind> which bitcoin-cli 返回了 bitcoind 和 bitcoin-cli 的位置：/usr/local/bin/bitcoind/usr/local/bin/bitcoin-cli

**配置和编译比特币核心**

接下来，你需要配置一个节点。每个比特币核心节点不进行挖矿，但为比特币网络做出贡献，包括客户端、矿工、钱包等。要配置节点，你可以在终端中输入以下命令来查找配置文件的位置：> bitcoind -printtoconsole 几秒钟后，停止此服务（Control+C）。该命令显示了 bitcoin.conf 配置文件的位置。请参阅图 2-17 以查看输出。" 使用配置文件 /[path]/.bitcoin/bitcoin.conf"![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig17_HTML.jpg](img/475651_1_En_2_Fig17_HTML.jpg)

Figure 2-17

bitcoin.conf 文件位置

在撰写本文时，一个完整的比特币核心节点需要 2GB 的 RAM 和至少 180GB 的磁盘空间（ [`blockchain.info/charts/blocks-size`](https://blockchain.info/charts/blocks-size) ）。另外，由于比特币节点不断发送和接收交易和区块，你需要一个快速的互联网连接。

完整的节点对于运行矿工的实际项目是建议的，因为你可以运行专用服务器并通过 Bitcoin-CLI 与 bitcoind 交互；然而，为了本书的目的，大部分时间你不需要完整的节点。我建议你限制你的计算机上比特币节点资源的使用，以免占用你的计算机资源和互联网带宽。

为了限制你的节点下载整个共享账本，使用 vim 或你喜欢的编辑器编辑 bitcoin.conf 文件。vim /[path]/.bitcoin/bitcoin.conf 在 vim 打开 bitcoin.conf 后，粘贴以下配置：alertnotify=myemailscript.sh "Alert: %s"prune=3000maxconnections=10dbcache=150maxmempool=100maxsendbuffer=500maxreceivebuffer=2000txindex=0 确保你不删除下面已经存在的行：rpcuser=bitcoinrpcrpcpassword=[password]为你所知，配置文件包含以下参数：

+   ***prune***: 使用 prune，你可以限制磁盘使用。将此设置为 3000。

+   ***Maxconnections***: 通过设置有限的 maxconnections 值，你限制了最大节点数为十个连接

+   ***dbcache***: 在 dbcache 中，你将 UTXO 缓存大小从 300 MiB 减小到 100 MiB。

+   ***Maxsendbuffer 和 maxreceivebuffer***: 你可以限制每个连接的内存缓冲区大小为你设置的数字；例如，将 maxreceivebuffer 设置为 2000MB。

+   ***Txindex***: 将此设置为 1 以获取区块链上的任何交易的交易数据；然而，这将占用更多的磁盘空间。

**运行比特币核心守护进程**

配置好你的节点后，你可以启动比特币核心守护进程。要运行 bitcoind，请在终端中执行以下命令：bitcoind -printtoconsole 首次运行守护进程时，它会下载区块链。这可能需要几个小时（取决于你的互联网连接）。因为你设置了打印到控制台（-printtoconsole）的参数，所以你可以查看整个区块链下载过程。见图 2-18。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig18_HTML.jpg](img/475651_1_En_2_Fig18_HTML.jpg)

图 2-18

比特币核心守护进程（bitcoind）

在进程运行时，打开另一个终端窗口以查询 bitcoind 并通过 bitcoin-cli 与 API 交互。注意：你可以调用帮助功能并获得有关可用 API 的帮助。例如，要获取所有可用 API 的列表，使用这个命令：> bitcoin-cli --help # 输出命令行选项列表。> bitcoin-cli help # 当守护进程运行时，输出 RPC 命令列表。> bitcoin-cli help getblockhash # 获取特定 API 的帮助，例如"getblockhash"；为了能够检索完整信息，你需要运行一个完整节点。在配置文件中运行完整节点时，在 bitcoin.conf 文件中将 txindex=1 更改为 prune=3000。使用你喜欢的编辑器打开 bitcoin.conf。> vim /[path]/.bitcoin/bitcoin.conf 将参数更改为如下：txindex=1 # prune=3000 - 注释掉这一行此更改将允许你运行一个完整节点并提供索引信息，以便你可以查看区块链上的任何交易的交易数据。现在你可以再次启动 bitcoind 核心守护进程，并告诉守护进程重新索引所有数据。> bitcoind -reindex –printtoconsole

这个过程可能需要数小时；然而，在下载区块的过程中，你可以与已下载的区块进行交互。

要获取区块链信息，你可以查询守护进程以显示你节点的进度。参见图 2-19 中的预期输出。> bitcoin-cli getblockchaininfo![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig19_HTML.jpg](img/475651_1_En_2_Fig19_HTML.jpg)

图 2-19

获取区块链信息

这没有完成比特币节点的完整下载；然而，你已经拥有了 209,513 个区块和 538,726 个区块头部。节点首先下载最佳链块的区块头部，然后下载完整区块。

在这个练习中，你设置了你的环境并下载了区块，配置了它们，并启动了一个比特币节点。

### 序列化区块

每个完整节点都持有相同的验证区块并遵循相同的规则（共识规则）。每个比特币链中的区块包含根据当前比特币共识规则的 1 MB 序列化代码。

区块头部包含以下编码信息：

+   版本

+   前一个区块头部

+   默克尔根哈希

+   时间

+   位数

+   随机数

+   交易计数（持有交易总数）

+   交易（原始交易）

这些数据正在被哈希，是工作量证明算法和共识规则的一部分。中本聪的白皮书解释了共识规则。

> “他们用 CPU 功率进行投票，通过扩展有效区块来表达接受，并通过拒绝为无效区块工作来拒绝它们。任何需要的规则和激励措施都可以通过这种共识机制来执行。”
> 
> ——《比特币：一种点对点的电子现金系统》

比特币的工作量证明（PoW）基于亚当·巴克的 Hashcash。每个矿工都在争夺解决问题；一旦问题解决，过程将重新开始。这个问题是一个被称为*工作量证明问题*的数学难题，奖励是第一个解决问题的矿工。然后，验证的交易被存储在公共账本中。你将在下一节了解更多关于这方面的内容。生成大约 25 个比特币需要 9.9 分钟。根据中本聪的白皮书：

> *“一个没有交易的区块头部大约是 80 字节。如果我们假设每 10 分钟产生一个区块，80 字节 * 6 * 24 * 365 = 4.2MB 每年”*
> 
> —*比特币：一种点对点电子现金系统*。

在撰写本文时，比特币每秒处理三个交易，如果比特币交易增加到每秒四个，那么比特币将达到峰值容量。另一方面，以太坊目前每秒处理五个交易，如果增加到八个，也将达到峰值容量。这种设计存在可扩展性问题，因为大型企业需要每秒处理数百万笔交易，而不仅仅是四到八笔。

### 区块头部

正如所说，比特币网络中的节点共享一个区块。每个区块头部是一个序列化的 80 字节格式。以下信息编码在每一个区块头部：

+   ***版本***：在撰写本文时，有四个区块版本。版本 1 是创世区块（2009 年），版本 2 是比特币核心 0.7.0 中的软分叉（2012 年）。版本 3 区块是比特币核心 0.10.0 中的软分叉（2015 年）。版本 4 区块是比特币核心 0.11.2 中的 BIP65。

### 注意

BIP 是什么？BIP 是*比特币改进提案*（BIP）。这是一份介绍比特币新功能或信息的文档。BIP 是沟通想法的标准，因为比特币是开源的，并且没有正式的结构。

+   ***前一个区块头部哈希***：这是前一个区块头部的 SHA256(SHA256())哈希。这确保了完整性，因为改变一个前一个区块将需要改变每一个前一个区块。

+   ***Merkle 根哈希***：Merkle 树是一个二叉树，包含树中所有哈希对的哈希值。

+   ***时间***：这是矿工开始哈希头部时的 Unix 纪元时间。

+   ***nBits***：nBits 是区块头部的目标部分。

+   ***nonce***：这是一个矿工任意更改以修改头部哈希以产生小于或等于目标阈值的哈希的数。

你已经下载了区块链的一部分，并且你能够查询已经下载的区块高度。> bitcoin-cli getblockhash 375617 守护进程返回了一个包含索引 375617 处最佳区块链的区块哈希的字符串。然后，你可以请求获取实际的区块。> bitcoin-cli getblock 00000000000000000f270563d7f2187beec75cdc04f98823572e5a31baf0a261 图 2-20 显示了结果。正如你所看到的，区块信息包括前区块哈希键和下一个区块哈希键。这些键是 SHA256(SHA256())哈希加密的键。规则确保区块无法被更改。这些规则是共识规则的一部分，旨在通过不可信节点维护区块链的安全。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig20_HTML.jpg](img/475651_1_En_2_Fig20_HTML.jpg)

图 2-20

获取区块信息

### 区块版本

区块版本是区块头的一部分。你可以看到在区块中使用的区块版本。在图 2-20 中，你可以看到只有版本 1 用于区块 00000000000000000f270563d7f2187beec75cdc04f98823572e5a31baf0a261。

共识机制只能由比特币开源开发团队更改，该团队发布了处理升级建议的说明。在版本 2、3 和 4 中使用了引入了处理版本化交易和区块升级方法的 BIP。

添加到比特币核心的功能管理软分叉。你可以了解更多关于这个 BIP 特性的信息，点击这里：[`github.com/bitcoin/bips/blob/master/bip-0034.mediawiki`](https://github.com/bitcoin/bips/blob/master/bip-0034.mediawiki)。

#### 梅克尔树

你调用获取区块信息并接收了一个 Merkle 根哈希键。Merkle 树是一个二叉树。Merkle 树的根节点持有树中所有哈希对的全部。为了帮助理解这个过程，请看以下简单的 ASCII 示例，这是一个已哈希的二叉列表的区块：*交易列表：H(A)->H(B)->H(C)->H(D)*            *Hash(A|B|C|D)*         */               \*     *Hash(A|B)         Hash(C|D)*        */ \          /         \* *Hash(A)  Hash(B)  Hash(C)   Hash(D)*包含在这个 Merkle 根中的区块头是该区块中所有交易的后代的表示。HASH(A|B|C|D)是 Merkle 根。每个元素 A、B、C 和 D 将是该区块中所有交易的哈希。在我们这个例子中，每个区块中只有一个交易.*Merkle Root: H(A)*         */*     *Hash(A)*

#### 目标 nBits

区块头包括 nBits.* nBits 是区块头的目标部分。nBits 是 256 位目标阈值的 32 位紧凑编码。它像科学记数法一样工作，但使用的是 256 进制而不是 10 进制。每 2016 个区块的比特币核心重定位一次，并根据比特币难度规则调整 nBits。比特币难度会根据找到 2016 个区块所需的时间少于或超过两周而增加或减少。换句话说，如果哈希率增加，难度会增加；如果网络哈希率降低，难度会减少。

例如，要将 nBits 0x181b8330 转换为目标阈值，你可以使用与常规科学记数法相同的简写方式进行计算；参见图 2-21。

图 2-21

计算 nBits。图片来源于 stackexchange.com。

将 0x1bc3300000000000000000000000000000000000000000000 转换为 0x181b8330 的 nBits。这将是我们的目标阈值。

#### txn_count

txn_count 参数代表给定区块中包括 coinbase 交易的总交易数。

Coinbase 是一个特殊字段，用作 coinbase 交易的输入。coinbase 允许你领取区块奖励，并提供了最多 100 字节的自定义数据。

每个区块包含交易，区块中的第一个交易由矿工创建，它包括一个 coinbase。

#### 区块奖励

比特币矿工为创建区块领取奖励。奖励是区块补贴加上包含在区块中的交易的交易费用。

区块补贴是新可用的 satoshis 奖励。它始于 50 比特币，每 210,000 个区块减半，大约每四年一次。在撰写本文时，大约是 12.5 比特币。区块补贴的 80%已经支付，只剩下 420 万比特币可供挖掘，直到达到 21 百万的总供应量。到那时，矿工会只收到交易费用作为奖励。

正如提到的，每个区块包含交易，区块中的第一个交易由矿工创建，它包括一个 coinbase，作为奖励。

#### txns：解码交易

txns 是区块中的原始交易。为了更好地理解这个过程，让我们用一个实际的交易来工作。存储在区块链账本中的比特币交易以序列化字节格式（原始格式或原始交易）在不同对等体之间传播。为了解码 SHA256 原始交易，你可以调用比特币客户端并使用不同的 API。

首先，你可以获取一个你想要处理的区块。你正在运行的守护进程列出了区块作为新的最佳区块，如图 2-22 所示。

图 2-22

Bitcoin 守护进程将结果显示在控制台上。

正如你所看到的，通过查看比特币守护进程的输出，你可以找到新的最佳区块。在这个例子中，你选择了哈希 000000000000ea2ca199cafd1362ece59d7c6f3867b5e0d6f20c12af6752fb48。

最佳区块链是选择最难重建的区块链。记住，在区块链中，每个区块都引用它之前的区块；这就是你如何创建一个区块链来提供安全性和防止双重花费的。

现在你已经得到了新的最佳区块，你可以检索该区块的哈希数据。> bitcoin-cli getblock 000000000000ea2ca199cafd1362ece59d7c6f3867b5e0d6f20c12af6752fb48getblock 命令返回了关于你请求的区块的编码 SHA256 哈希数据（图 2-23）。![图](img/475651_1_En_2_Fig23_HTML.jpg)

图 2-23

getblock 检索区块信息

让我们检查一下 getblock 调用的结果。你得到了一个 Merkle 根哈希以及该区块中所有交易的哈希 `tx`。例如："a73226fc261f95db14eba45cd734aeb0b8784911aeb24f301f94858a09184036"，交易哈希 02，交易哈希 03 等。

正如你所看到的，这个区块中的数组中包含多个 `tx`（交易）。你现在可以请求检索每个交易（`tx`）的原始交易数据。

`getrawtransaction`命令将返回原始数据。> bitcoin-cli getrawtransaction a73226fc261f95db14eba45cd734aeb0b8784911aeb24f301f94858a09184036 以下是 SHA256 原始交易的原始交易数据：01000000010000000000000000000000000000000000000000000000000000000000000000ffffffff070439f3001b0141ffffffff0100f2052a01000000434104b5a750a0ca4bb5a47b6f169b8a8f42b39e2dbb7967d046f1bf018d927d102c280f1123ebfd973f6e651f2e5ff4486e18a90cc67d6d17ccdb95cd6bf028d791cfac00000000 你现在可以使用解码原始交易命令来解码 SHA256 原始交易数据。> bitcoin-cli decoderawtransaction 01000000010000000000000000000000000000000000000000000000000000000000000000ffffffff070439f3001b0141ffffffff0100f2052a01000000434104b5a750a0ca4bb5a47b6f169b8a8f42b39e2dbb7967d046f1bf018d927d102c280f1123ebfd973f6e651f2e5ff4486e18a90cc67d6d17ccdb95cd6bf028d791cfac00000000 该命令将以可读格式返回交易结果，如图 2-24 所示。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig24_HTML.jpg](img/475651_1_En_2_Fig24_HTML.jpg)

图 2-24

使用解码原始交易命令来解码交易

### 比特币钱包

正如你在图 2-24 中看到的，钱包地址是 1Mr2G632PfQuq4uJXRBNWLoRKH71Qwor51，币值为 50 枚硬币。

您还可以通过访问包含完整节点的服务并检查钱包余额来在线确认该钱包的交易。图 2-25 显示了来自[`bitref.com/1Mr2G632PfQuq4uJXRBNWLoRKH71Qwor51`](https://bitref.com/1Mr2G632PfQuq4uJXRBNWLoRKH71Qwor51)的屏幕截图。![../images/475651_1_En_2_Chapter/475651_1_En_2_Fig25_HTML.jpg](img/475651_1_En_2_Fig25_HTML.jpg)

图 2-25

1Mr2G632PfQuq4uJXRBNWLoRKH71Qwor51 钱包余额

同样，您可以通过命令行界面（CLI）查询您的钱包可用资金：`bitcoin-cli getbalance 1Mr2G632PfQuq4uJXRBNWLoRKH71Qwor51`

在接下来的章节中，我将介绍钱包，所以我将更详细地解释钱包的操作，但现在，您可以看到用户在 2003 年购买了 50 枚硬币，并在 2012 年出售了它们。请注意，尽管您不知道拥有钱包的人的身份，但您可以看到钱包的当前余额，因为这是公开信息。

## 总结

在本章中，您学习了如何运行一个可以协助管理区块链的区块链节点。对于比特币，您创建了一个名为*矿工*的节点。对于 NEO，您创建了一个具有管理权的节点，称为 b*ookkeeping node*。对于 EOS，您创建了一个*区块生产者*。您还探索了要使您的节点当选或运行以便盈利您需要做什么。

接下来，您安装了一个能够运行比特币核心 API 的全功能比特币节点。您安装并配置了您的节点，并学习了如何运行比特币核心守护进程。然后您与比特币核心 API 进行了交互，并能够学习如何序列化区块，更好地理解每个区块内的数据。

我介绍了区块奖励、交易和比特币钱包。在下一章，您将构建自己的区块链 P2P 网络，以更深入地了解区块链是如何工作的。
