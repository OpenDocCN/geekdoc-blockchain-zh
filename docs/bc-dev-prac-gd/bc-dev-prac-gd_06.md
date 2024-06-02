© Elad Elrom 2019 Elad Elrom 区块链开发者 [`doi.org/10.1007/978-1-4842-4847-8_6`](https://doi.org/10.1007/978-1-4842-4847-8_6)

# 6. EOS.IO 钱包和智能合约

Elad Elrom^(1 )（1）纽约，纽约，美国

在第二章中，当我介绍比特币、山寨币和不同的共识机制时，我介绍了 EOS.IO。具体来说，我讲述了 EOS.IO 是如何成为山寨币转为代币的例子；你创建了一个 EOS 区块生产者，并能够创建一个能够挖掘 EOS 代币的全节点。以太坊是你的区块链智能合约开发的开始，你学会了使用 Solidity 语言编写智能合约和 dapp。EOS.IO 为智能合约和 dapp 开发创造了比以太坊更健壮的架构。

在本章中，我将扩展 EOS.IO 区块链的介绍，并展示如何构建一个可用于去中心化应用（dapps）的 EOS.IO 智能合约。你将设置一个本地测试网环境，并学习如何配置 EOS.IO 工具和库。你将了解 EOS.IO 钱包以及如何创建、删除和备份钱包，以及执行诸如打开、锁定和解锁钱包等操作。我将涵盖钱包的关键对以及如何启动和重新启动本地测试网区块生产者。你将了解权限和单签名、多签名选项。

为了更好地理解 EOS.IO 智能合约，你将创建一个“HelloWorld”智能合约和代币。你将创建账户，编写智能合约 C++代码，编译代码，以及生成 WebAssembly 和 ABI 文件以及 Ricardian 合同。你还将学习如何部署你的智能合约并与之交互，以及发行代币和将代币转让给另一用户。

最后，你将连接到一个公共测试网区块生产者，以便在更真实的环境中进行测试，以及连接和发布在主网区块生产者上。

### 注意

EOS 是推动 EOS.IO 软件的原生加密货币（代币）。EOS.IO 是一种工业级、完全定制的区块链架构协议，通过提供访问构成区块链的部分来使去中心化应用成为可能。把 EOS.IO 看作一个区块链操作系统，因为它模仿了一台真实的计算机，并提供了访问 CPU、GPU、RAM 和硬盘等资源的能力。EOS.IO 在执行每秒数百万笔交易时不会收取交易费。EOS 代币是一种实用代币，拥有代币（质押）提供了 EOS.IO 区块链上的带宽和存储。你按拥有的总质押比例获得资源（拥有 EOS 代币的 1%可使用 EOS.IO 总带宽的 1%）。

> *“* *EOS.IO* *软件引入了一种新的区块链架构，旨在实现去中心化应用的垂直和水平扩展。这是通过在应用程序可以构建的类似于操作系统的结构上创建实现的。该软件提供账户、身份验证、数据库、异步通信以及跨许多 CPU 核心或集群的应用程序调度。 resulting technology is a blockchain architecture that may ultimately scale to millions of transactions per second, eliminates user fees, and allows for quick and easy deployment and maintenance of decentralized applications, in the context of a governed blockchain.”*
> 
> —EOS.IO block.one 白皮书

如第二章所述，EOS.IO 基于委托权益证明（DPoS）共识机制构建。EOS.IO 能够处理低延迟，并支持每天数百万活跃用户（绕过以太坊）。这得益于 DPoS 共识以及 EOS.IO 作为多线程（在多个计算机核心上运行）的操作系统的运作。

这种可扩展性可以使大型企业采用区块链技术。EOS.IO 还提供许多其他功能，如下所示：

+   免费限速交易

+   低延迟交易（如 0.25 秒的广播时间或 0.5 秒的区块时间）

+   恢复被盗密钥

+   应用程序的并行执行

+   具有多个账户的原子交易

我鼓励您阅读 EOS.IO 白皮书并访问 GitHub 页面以获取完整功能列表。

+   [`github.com/EOSIO/eos`](https://github.com/EOSIO/eos)

+   [`github.com/EOSIO/Documentation/blob/master/TechnicalWhitePaper.md`](https://github.com/EOSIO/Documentation/blob/master/TechnicalWhitePaper.md)

从财务角度来看，EOS 由一家名为 block.one 的私人公司开发，并通过 ERC-20 代币销售筹集了惊人的 40 亿美元。在撰写本文时，EOS 的价格约为 2 至 8 美元，总市值约为 20 亿美元，使 EOS 成为市值第七大的加密货币。

EOS 提供了一些代码库以帮助开发 EOS.IO 合约；这些代码库列在[`github.com/EOSIO`](https://github.com/EOSIO)上，包括以下内容：eos，eosio.cdt，eosjs，demux-js，和 eosio.contracts。您将在本章安装 EOS 和 EOSIO.CDT 库。EOS 库是一个开源智能合约平台，而 EOSIO.CDT 库是用于构建 EOS.IO 合约的工具集。

截至撰写本文时，EOS.IO 平台的学习曲线非常陡峭。代码在不断变化，而 EOS.IO 的文档和示例并没有及时更新，所以有时感觉就像是在追一个移动的目标。这导致代码有时无法编译，命令无法工作，文档和示例包含已经过时的代码和命令。在开发合同时，你可能会遇到几次难题；然而，一旦你理解了 EOS.IO，这些障碍就很容易克服。

## 设置测试网环境

在开始编码之前，让我们先安装 EOS.IO 和 EOSIO.CDT。您将构建您的 EOS.IO 版本并设置一个本地测试网块生产者。然后，您将了解称为 cleos、keosd 和 nodeos 的 EOS.IO 工具以及如何配置它们以及使用 cleos 创建和管理钱包。这些工具和库对于开发是必要的。

### 安装 EOS.IO

在 macOS 上安装 EOS.IO 最简单的方法是使用 Brew。> brew tap eosio/eos> brew install eosio

当前的 EOS.IO 版本是 1.7.3。我建议检查 GitHub 上的仓库和 issues 部分（ [`github.com/eosio/eos`](https://github.com/eosio/eos) ）或进行 Google 搜索，以防在安装或构建 EOS.IO 时遇到错误。还要参阅 [`github.com/EOSIO/eos/issues`](https://github.com/EOSIO/eos/issues) 。

安装完成后，您将在终端中看到图 6-1 中的消息。![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig1_HTML.jpg](img/475651_1_En_6_Fig1_HTML.jpg)

图 6-1

EOS.IO 成功构建

接下来，将 EOS.IO 二进制文件位置添加到您的环境变量中，这样您就可以从任何地方运行 nodeos。> export PATH=$PATH:/usr/local/eosio/bin 这将在此终端会话中设置路径变量，但您希望永久设置路径环境变量，因此通过使用 vim 或您喜欢的文本编辑器打开 bash_profile 文件并添加以下内容。> vim ~/.bash_profile 接下来，插入以下行：# 为 EOSIO 设置 PATHEOSIO_PATH="/usr/local/eosio/bin:${PATH}"最后，运行 bash_profile 以提交更改。> . ~/.bash_profileEOS.IO 自带内置工具和程序；它们在这里：/usr/local/eosio/。图 6-2 展示了这些工具的架构图。

+   nodeos：这是核心 EOS.IO 守护进程，使您能够运行区块链节点组件。nodeos 可以配置插件。此外，nodeos 可以配置为在本地开发环境或专用端点上运行块生产者。它通过创建区块与区块链交互。

+   cleos：这是 EOS.IO 的主要命令行工具。它与 nodeos 暴露的 REST API 接口。它还可以访问钱包，因为它与 keosd 交互。要查看 cleos 命令，只需运行以下命令：

    > cleos

+   keosd：这是用来加载和管理钱包密钥的钱包守护进程。它通过加载与钱包相关的插件（如 HTTP 接口和 RPC API）来实现这一点。

+   eosio-launcher：这个工具将帮助你部署多节点区块链网络。

![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig2_HTML.jpg](img/475651_1_En_6_Fig2_HTML.jpg)

图 6-2

EOS 的基本架构。图片来源于：developers.eos.io。

### 安装 EOSIO.CDT

你已经安装了 EOS.IO。你需要的另一个重要库是 EOSIO.CDT（CDT 代表“合同开发工具包”）。EOSIO.CDT 是用于构建 EOS.IO 合同的工具套件。为了安装库，你将使用 Brew。

正如你所回忆的，你使用了 Truffle 和 Remix 来生成以太坊的应用二进制接口（ABI）文件。对于 EOS.IO 智能合约，你使用 eosio-cpp，这是一个生成 WebAssembly (.wasm)文件的编译器，这是智能合约需要上传到区块链的 ABI。eosio-cpp 还生成了帮助函数，用于序列化/反序列化智能合约开发中定义在 ABI 代码中的类型。

你可以在 GitHub 页面上找到关于 EOSIO.CDT 的更多信息：[`github.com/EOSIO/eosio.cdt`](https://github.com/EOSIO/eosio.cdt) 。

将来，如果你需要删除 EOSIO 和 EOSIO.CDT，请运行以下命令：

### 注意

eosio-cpp 是已被弃用的 eosiocpp 的替代品。最初 eosiocpp 是 EOS.IO 安装的一部分，但现在它属于 CDT。

### 构建 EOS.IO

了解 EOS.IO 及其与 EOS.IO 相关的工具的一个很好的方法是查看图 6-2。

### keosd 和 nodeos 配置文件

keosd 和 nodeos 默认端口使用相同的端口：8888。

要配置 nodeos，请查看此配置文件：

在 config.ini 文件中，一个值得更改的变量是您加载的插件列表。你不会做更改，但随着你开发的进步，你可能需要做更改。

与 nodeos 一样，你可以通过编辑此配置文件来配置 keosd：

一旦你打开文件，请注意有一个名为 http-server-address 的变量，你可以用它来改变端口 8888，以防你需要这个端口用于其他软件。这里让我们把它设置成你喜欢的任何端口。

变量已被注释掉。要将其设置为端口 9000，请将其从以下内容更改为：

你可以使用默认端口；然而，了解如何配置 EOS.IO 是有好处的。

### 使用 cleos 创建和管理钱包

在前一节中，我介绍了一些 EOS.IO 内置程序和工具。

如前所述，cleos 提供了一个由 nodeos 暴露的 REST API 接口。cleos 参考指南可以在这里找到：[`developers.eos.io/eosio-cleos/reference`](https://developers.eos.io/eosio-cleos/reference) 。

要找到 cleos --version 号码，运行--version 客户端命令。在撰写本文时，你可以构建 d4ffb4eb。> cleos version client

注意，由于你没有运行节点，所以得不到任何结果和错误信息；然而，在本章后面，当你启动 nodeos 时，你将获得关于你的区块生产者的信息。

### EOS.IO 钱包

EOS.IO 钱包使用密钥，并提供锁定（加密）状态和解锁（解密）状态以保护密钥。锁定和解锁命令需要你在创建钱包时提供的高熵密码。钱包的密钥可以与一个账户关联，为账户的代币提供权限，但创建钱包时并不必要。

钱包的软件使用 cleos 作为 keosd 密钥检索操作和 nodeos 区块链操作之间的中介层。例如，你可以使用 cleos 访问一个账户，因为它需要从密钥中生成签名。要创建默认的钱包，只需运行创建钱包命令。使用--to-console 标志来获取主密钥（密码）。> cleos wallet create --to-console

注意，一旦你创建了你的默认钱包，钱包名称旁边有一个星号。星号意味着它是解锁的。你将在下一节了解更多关于锁定和解锁状态的信息。

### 删除并备份钱包

要删除你创建的钱包，你需要删除实际钱包的文件；它位于这里：~/eosio-wallet。> rm -rf ~/eosio-wallet

要备份钱包，复制钱包的文件并将它们存储在安全的地方。

### 带有自定义名称的 EOS.IO 钱包

到目前为止，你已经创建了默认的钱包。现在假设你想要创建另一个钱包，并将其命名为 mywallet。你只需要使用-n 或--name 标志。选择一个名字，并注意严格的命名限制（只允许 a-z 和 1-5，长度为 12）。我选择的是 mywallet。> cleos wallet create -n mywallet --to-console

### EOS.IO: 打开、锁定和解锁钱包

当你创建你的钱包时，你得到了一个高熵的主密钥，那就是你的密码。这个密码用来加密（锁定）和解密（解锁）你的钱包文件。要锁定和解锁你的钱包，请使用以下命令：> cleos wallet lock -n mywallet

锁定和解锁命令使你的钱包能够设置一个受密码保护的加密和解密状态。你所保护的是钱包的密钥。

要解锁默认的钱包，只需运行以下命令：> cleos wallet unlock

### 生成 EOS.IO 密钥

就像在其他区块链中一样，EOS.IO 在钱包中存储密钥。你生成这些密钥并将它们分配给一个 EOS.IO 账户。有多种创建密钥的方法。你将在此使用 cleos。首先让我们重新创建默认的钱包，以防你之前删除了它。> cleos wallet create --to-console

"[DEFAULT_MASTER_KEY]"

运行钱包列表应该会显示两个钱包。> cleos wallet list

正如你所注意到的，你两次运行了创建密钥命令。这不是错误；你需要两个密钥：一个用于活动用户，一个用于所有者。一旦你创建了账户，你会更多关于这个概念的了解。

您运行的命令输出了公钥和私钥的对。请注意，公钥以 EOS 关键词开头。这些任意的密钥对本身没有意义，因为它们没有权限（它们不属于任何钱包或账户）。要将这些密钥对分配给钱包，您可以将这些密钥导入您的钱包。> cleos wallet import --private-key [PRIVATE_KEY_1]导入的私钥用于：[PRIVATE_KEY_1]导入的私钥用于：[key]> cleos wallet import --private-key [PRIVATE_KEY_2]导入的私钥用于：[PRIVATE_KEY_2]在您的命令的输出中，您从命令行收到了一个确认消息，确认密钥对已添加。然而，您也可以通过调用钱包密钥命令来确认密钥对已添加。> cleos wallet keys[PUBLIC_KEY_1, PUBLIC_KEY_2]此外，您可以请求查看密钥对。> cleos wallet private_keys --password [DEFAULT_MASTER_KEY][[PUBLIC_KEY_1, PRIVATE_KEY_2],[ PUBLIC_KEY_1, PUBLIC_KEY_2]]

在上一个命令中，您传递了--password 参数，而不是等待命令行提示您输入主密码。

最后，您需要导入一个特殊的 EOS.IO 母账户。这个特殊的母账户用于引导 EOS.IO 节点。没有这个私钥，您将无法创建您的账户。EOS.IO 账户需要一个母账户来创建另一个账户；这就是 EOS.IO 分配资源和防止垃圾邮件及黑客的方法。> cleos wallet import --private-key 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3 导入的私钥用于：EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV

### 注意

在撰写本文时，母钱包是可用的；然而，情况可能会发生变化，您可能需要找到一个可以用来引导 EOS.IO 钱包的母钱包。

查看您的输出，以便您想比较您的输出和我的输出；请见图 6-3！../images/475651_1_En_6_Chapter/475651_1_En_6_Fig3_HTML.jpg

图 6-3

使用特殊的母账户设置 EOS.IO 钱包密钥

### 启动一个带有 nodeos 的节点

交易附着在一个块上，你需要一个块生产者才能将这些交易传递到网络上。

如果您直接连接到公共测试网或主网，您可以跳过创建 EOS 节点（nodeos）；然而，在将您的代码提交到公共测试网或主网之前，最好先在本地测试网网络上运行您的智能合约。

到目前为止，您应该已经熟悉了这个过程，因为您在为以太坊开发智能合同时已经做过同样的事情。请随意参考图 6-2，您可以看到 nodeos 和 EOS.IO 区块链关系的图表。

要在另一个终端启动你自己的单节点本地区块链块生产者，运行 nodeos。> nodeos -e -p eosio --plugin eosio::chain_api_plugin --plugin eosio::history_api_plugin --contracts-console 此命令启动块生产者，并在控制台上显示进程。info 2019-04-28T19:03:34.776 thread-0 chain_plugin.cpp:333 plugin_initialize] 初始化链插件 info 2019-04-28T19:03:34.811 thread-0 block_log.cpp:134 open] 日志不为空 info 2019-04-28T19:03:34.820 thread-0 block_log.cpp:161 open] 索引不为空 info 2019-04-28T19:03:34.878 thread-0 http_plugin.cpp:422 plugin_initialize] 配置 http 以监听 127.0.0.1:8888.........

正如你所看到的，控制台显示您的本地网络开始生产区块。注意您使用的命令设置了插件，而且还设置了--contracts-console 标志。

此标志是在开发模式下能够看到您打印到控制台的消息的必要条件。

### 注意

你还可以在 config.ini 文件中设置--contracts-console 标志，而不是每次都使用 nodeos 传递这个参数。

正如您所回忆的，您之前运行了 cleos get info 命令，但没有结果，因为您没有运行块生产者；现在如果您在一个新的终端中运行相同的命令，您可以观察到有关您区块的信息。> cleos get info{ "server_version": "d4ffb4eb", "chain_id": "cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f", "head_block_num": 73699, "last_irreversible_block_num": 73698, "last_irreversible_block_id": "00011fe2a80bf11315396c85e70860122dddc24ac083911fba31f7ee2d64eb3e", "head_block_id": "00011fe36fab1fc2d4885067e1391c72782895d43f14cf7970ac282ddef17d67", "head_block_time": "2019-04-28T19:04:06.500", "head_block_producer": "eosio", "virtual_block_cpu_limit": 200000000, "virtual_block_net_limit": 1048576000, "block_cpu_limit": 199900, "block_net_limit": 1048576, "server_version_string": "v1.5.1-dirty"}

### 重新启动测试网络本地节点（nodeos）。

如果您想清除块生产者的历史记录，删除所有区块，并重新启动您的本地测试网络，您将使用所谓的*硬重放*，使用以下标志：--delete-all-blocks --delete-state-history --hard-replay 这些参数将清除本地测试网络上的账户以及区块。完整的命令将如下所示：> nodeos -e -p eosio --plugin eosio::chain_api_plugin --plugin eosio::history_api_plugin --delete-all-blocks --delete-state-history --hard-replay --contracts-console

### EOS.IO 账户

EOS.IO 账户持有的是存储在 EOS.IO 区块链上的人类可读名称。

要在主网络上创建账户，需要一个 EOS.IO 账户的人为你创建。这种受监管的过程背后的原因是防止垃圾信息和黑客攻击以及资源分配。默认情况下，该账户持有两个本地名称/权限。

+   所有者：这用于恢复其他权限，在权限被泄露的情况下非常有用。

+   积极：这用于进行高级账户更改，例如转移资金或投票选举区块生产者。

当您创建您的测试网账户时，您导入了特殊的 EOS.IO 父账户密钥以启动。每个权限名称都需要一个“父”。父权限是为了能够更改其所有子权限设置中的任何权限。EOS.IO 为本地测试网提供了特殊账户的父密钥，您导入以创建自己的账户。参见图 6-4。![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig4_HTML.jpg](img/475651_1_En_6_Fig4_HTML.jpg)

图 6-4

账户高级架构和权限结构。图片来源：hackernoon.com。

为了使交易有效并签名，每个命名权限都需要满足条件，例如一个解锁的钱包客户端，并且钱包必须授予账户授权权限。如果您不满足这些条件，交易将失败。

既然您已经理解了账户，您就准备好创建自己的账户了。您已经创建了一个钱包并导入了父密钥。要创建账户，您运行以下命令的语法：> cleos create account eosio [ACCOUNT_NAME] [OWNER_PUBLIC_KEY] [ACTIVE_PUBLIC_KEY]

OWNER_KEY 值是账户所有者权限的公钥，ACTIVE_KEY 值是账户的积极权限公钥。

在这个示例中，我们将账户命名为 myaccount，并使用您创建的两个密钥。命令如下所示（参见图 6-5 以获取预期的输出）：> cleos create account eosio myaccount [PUBLIC_KEY_1] [PUBLIC_KEY_2]![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig5_HTML.jpg](img/475651_1_En_6_Fig5_HTML.jpg)

图 6-5

创建您的第一个 EOS.IO 账户，名为 myaccount

您生成了两个密钥，所以您决定将哪个密钥用作积极密钥，哪个用作所有者密钥都无关紧要；只需记住您用于哪个密钥即可。

要查看账户列表，使用这个：> cleos get accounts [PUBLIC_KEY_1]{  "account_names": [    "myaccount"  ]}

### 注意

如果您在尝试创建账户时遗漏了本章中提供的任何步骤，您可能会收到错误消息。错误是“Error 3090003: provided keys, permissions, and delays do not satisfy declared authorizations.”

### 钱包、密钥和账户：完整命令

为了确保您完全理解该过程，这里总结了创建账户的步骤：

1.  1.确保在另一个终端窗口中运行 nodeos。> nodeos -e -p eosio --plugin eosio::chain_api_plugin --plugin eosio::history_api_plugin --delete-all-blocks --delete-state-history --hard-replay --contracts-console

1.  2.

    确保您的钱包已解锁。运行> cleos wallet list（检查钱包名称旁边是否有星号）。

1.  3.

    EOS.IO 特殊账户的父密钥（5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3）已导入以启动 EOS.IO。

    cleos wallet import --private-key 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3

1.  4.

    使用> cleos wallet keys 检查密钥列表。它应该输出您导入的密钥的数组。

为了总结你已经完成的工作或者重新整个创建账户的过程，以下是完整的步骤：> rm -rf ~/eosio-wallet> cleos wallet create --to-console> cleos wallet open> cleos wallet unlock --password [DEFAULT_MASTER_KEY]> cleos create key --to-console> cleos create key --to-console> cleos wallet import --private-key [PRIVATE_KEY_1]> cleos wallet import --private-key [PRIVATE_KEY_2]> cleos wallet import --private-key 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3> cleos wallet keys> cleos create account eosio myaccount [EOS∗ OWNER_KEY] [EOS∗ ACTIVE_KEY]

### 自定义、单签名（单签）、和多重签名（多签）

默认情况下，你配置你的账户具有单个签名（又称单签），因为它被授权具有默认（active 和 owner）权限。然而，你可以配置你的账户具有多重签名（又称多签）或自定义权限。例如，你可以配置你的账户具有多个密钥以授权特定的所有者操作和活跃操作。你可以使用这个功能，例如，创建一个名为“publish”的权限，并把这个权限给一个账户，允许只有发布智能合约而没有提取代币的能力。

## “HelloWorld”智能合约

您将编写一个具有最小代码的智能合约。您将称您的智能合作为“HelloWorld”。

### “HelloWorld”智能合约账户

为了开始，你将为你的智能合约创建两个账户，一个用于发布你的智能合约，一个用于与用户交互。请参阅图 6-6 中的输出。> cleos create account eosio helloworld [PUBLIC_KEY]> cleos create account eosio john [PUBLIC_KEY]![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig6_HTML.jpg](img/475651_1_En_6_Fig6_HTML.jpg)

图 6-6

为“HelloWorld”智能合约创建账户

### “HelloWorld” C++代码

EOS 选择了 C++，这导致了区块链开发社区的混合评论。C++是一种低级语言，它允许更好地管理资源，如内存指针和运算符重载。这可能导致更好的性能；然而，这也带来了增加代码工作量的代价，尤其是如果你不熟悉 C++。

EOS.IO 基础设施是用 C++编写的，因此 EOS.IO 团队选择 C++并不令人惊讶。EOS.IO 智能合约是以 C++保存为 CPP 文件格式编写的；然后你将 C++代码编译成 WebAssembly，然后用于部署。

### 注意

EOS.IO 智能合约源文件可以分为三个：CPP、HPP 和 Ricardian。HPP 文件定义了智能合约类、行为和表。CPP 文件是 C++代码，实现了行为逻辑。Ricardian 文件是数字文档（关于这一点在下一节中有更多介绍）。

首先，通过导航进入目录创建 helloworld 合约目录。> mkdir ~/Desktop/helloworld && cd $_ 注意你使用了你的桌面，但可以使用你喜欢的任何目录。接下来，使用 vim 或你喜欢的文本编辑器粘贴 helloworld.cpp 代码。> vim helloworld.cpp#include <eosiolib/eosio.hpp>using namespace eosio;class helloworld : public contract {  public:      using contract::contract;      [[eosio::action]]      void hello( name user ) {         print( "World: User: ", user);      }};EOSIO_DISPATCH(helloworld, (hello))

代码导入了 EOS.IO 库。HelloWorld 类是契约类型，你创建了一个名为 hello 的方法，该方法是你的行为；你传递用户并打印出*world*和用户名。一旦用户与你的合约互动并调用 hello 行为，他们将得到带有用户名的 world。

注意在这个例子中你包含了 eosio.hpp 文件。为了调试 EOS.IO 智能合约，你需要使用老式的原始调试。

### 注意

原始调试，也称为 printf()调试，不过是在你的代码周围添加打印语句。EOS.IO 打印 API 支持字符数组、64 位和 128 位无符号整数等。打印是通过将 C++代码 printi、prints_l、printi128 等包裹在 print.hpp 中的 printi、prints_l、printi128 等，并包括导入 eosio.hpp 库声明。

## 智能合约 IDE

使用终端是可以接受的，但随着代码变得更加复杂，使用专业 IDE 可以帮助代码补全、高亮和可读性。你可以使用你喜欢的 IDE。既然你已经使用了 WebStorm，你可以继续将项目导入 WebStorm。WebStorm 已经包括了 C++插件，所以无需安装任何特殊插件。图 6-7 显示了 HelloWorld 项目在 WebStorm 中打开。

要导入你的项目，选择文件➤打开，并导航到项目位置：~/Desktop/helloworld.*../images/475651_1_En_6_Chapter/475651_1_En_6_Fig7_HTML.jpg

Figure 6-7

HelloWorld 项目已导入 WebStorm 版本 2018.2.4

## 编译合约并生成 ABI

如前所述，eosio-cpp 工具接受 C++代码并输出 WebAssembly 和 ABI。这是通过运行以下命令完成的：> eosio-cpp -o helloworld.wasm helloworld.cpp --abigen

请注意，在命令中你指定了输出文件的名称，即 helloworld.wasm。运行此命令后，编译器生成了以下文件：helloworld.wasm 和 helloworld.abi。

为了确保编译器如预期工作，你应该能够看到这两个文件；见图 6-7。

### Ricardian Contracts

一旦你生成了你的 WASM 和 ABI 文件，注意你收到了超过 20 个警告。在这些警告中，你应该在输出中找到以下警告：警告，空的 ricardian 条款文件警告，空的 ricardian 条款文件警告，动作<hello>没有 ricardian 合同。

### 注意

Ricardian 合同是由 Ian Grigg 在 1996 年发明的，以帮助弥合软件应用程序与法院之间的鸿沟。EOS 中的 Ricardian 合同文件是格式为 Markdown 语言的数字文档（.md、.markdown），定义了双方之间的互动条款和条件。它被设定为参数，但以可读的文本形式编写。EOS 使用加密技术来签署和验证 Ricardian 合同。

为了帮助生成 Ricardian 合同，你可以复制一个贡献者提供的 Python 脚本和模板，该脚本和模板可以自动生成文件：[`github.com/EOS-Mainnet/governance`](https://github.com/EOS-Mainnet/governance)。

因为这只有三个文件，而不是使用克隆，你可以使用 wget 来下载这些文件。

检查你的机器上是否安装了 wget。> wget --help 如果它没有安装，通过 Ruby 和 Brew 在 macOS 上安装 wget。> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null> brew install wget> brew upgrade wget 接下来，在你的 helloworld 项目中，创建目录并下载你需要的文件。> cd ~/desktop/helloworld> mkdir rc && cd $_> wget https://raw.githubusercontent.com/EOS-Mainnet/governance/master/scripts/abi_to_rc/abi_to_rc.py> wget https://raw.githubusercontent.com/EOS-Mainnet/governance/master/scripts/abi_to_rc/rc-action-template.md> wget https://raw.githubusercontent.com/EOS-Mainnet/governance/master/scripts/abi_to_rc/rc-overview-template.md 接下来，运行 Python 脚本。> cd ../> python rc/abi_to_rc.py helloworld.abi

脚本已经为您自动生成了 helloworld-rc.md 和 helloworld-hello-rc.md，格式化为 Markdown 语言。如果你查看这些文件，你会注意到 Python 脚本使用了你下载的模板来生成你的文件，你可以填写关于你的智能合同的条款和条件。

你可以设定用户正在购买/交换的具体指导方针，并允许双方建立更好的信任；它可以包括意图、保证、补救措施、不可抗力、争端解决、适用法律等内容。密切关注你设定的条款，因为这些可以在法院强制执行。这些条款可以跳过中间人，如律师，让智能合同设定双方同意的条款和条件。

## 部署合同

要部署你的智能合约到你的本地测试网络，使用 set contract 命令上传合约。参见图 6-8 预期的输出。> cleos set contract helloworld ~/Desktop/helloworld -p helloworld@active![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig8_HTML.jpg](img/475651_1_En_6_Fig8_HTML.jpg)

图 6-8

部署智能合约的终端输出

## 与智能合约动作交互

现在你已经在你本地的区块链上部署了你的智能合约，你可以与你创建的 hello 动作交互。你将调用 hello 动作并传递你的用户名到用户的活动密钥。参见图 6-9 的输出。> cleos push action helloworld hello '["john"]' -p john@active![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig9_HTML.jpg](img/475651_1_En_6_Fig9_HTML.jpg)

图 6-9

智能合约的终端推送动作输出

你可以从这里下载整个智能合约项目：[`github.com/Apress/the-blockchain-developer/chapter6/helloworld/`](https://github.com/Apress/the-blockchain-developer/chapter6/helloworld/)。

## 智能合约代币

EOS.IO GitHub 项目有一个智能合约库作为示例可以使用。这些库中的一个称为 eosio.token 的智能合约。这个合约使开发者能够创建其他代币以及转移代币。你将使用这些库来创建你自己的代币。开始时，你将创建一个新的智能合约项目，并将其命名为 eosio.token。**> mkdir ~/Desktop/eosio.token && cd $_**

### 创建账户

代币由“发行者”账户发行。你将开始创建一个名为“发行者”的账户和一个名为 jane 的账户，你可以使用它来转移一些代币。> cleos create account eosio eosio.token [public key]> cleos create account eosio jane [public key]

### 使用最新的 eosio.token 代码编译 wasm

要发行 eosio.token，你将使用定义了合约类、动作和表的 eosio.token.hpp 文件，以及包含逻辑和编码的 eosio.token.cpp。你可以在这里找到这些文件和整个 SmartContract 项目：[`github.com/Apress/the-blockchain-developer/chapter6/eosio.token/`](https://github.com/Apress/the-blockchain-developer/chapter6/eosio.token/)。

接下来，确保你更改 CPP 代码中的包含声明，使其指向你从 GitHub 下载的 HPP 文件，使用 vim 或你喜欢的文本编辑器。> vim eosio.token.cpp 将 eosio.token.cpp 文件第 6 行更改为指向 eosio.token.hpp 文件的位置；在这个例子中，它在這裡：include "~/Desktop/eosio.token/eosio.token.hpp"

### 部署 eosio.token

使用 eosio.token.hpp 和 eosio.token.cpp，你已经拥有了所有需要的文件。你可以使用 eosio-cpp 命令编译最新的 HPP 和 CPP 文件以生成.wasm 代码，就像你在 HelloWorld 智能合约示例中做的那样。> eosio-cpp -o eosio.token.wasm eosio.token.cpp --abigenNext，使用设置合约命令部署 eosio.token 合约。> cleos wallet unlock --password [DEFAULT_MASTER_KEY]> cleos set contract eosio.token ~/Desktop/eosio.token --abi eosio.token.abi -p eosio.token@active

### 创建 EOS.IO 代币

要创建你的新代币，你使用创建动作。你将传递 symbol_name 类型，其中包括两个参数。

+   *最大供应浮动*：在这个例子中，你将设置这个值为 2000 万作为你的最大代币：20000000.0000。

+   *符号*：对于 symbol_name，你需要选择一个名称。这个名字必须是只有大写字母字符；在这个例子中，选择名称 TOKEN。

“发行人”账户有权执行发行动作或其他动作，例如召回、冻结和白名单所有者。

要创建一个新的代币动作，运行以下命令。查看图 6-10 以获取预期输出。> cleos wallet unlock --password [DEFAULT_MASTER_KEY]> cleos push action eosio.token create '[ "eosio", "20000000.0000 TOKEN"]' -p eosio.token@active![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig10_HTML.jpg](img/475651_1_En_6_Fig10_HTML.jpg)

图 6-10

创建 eosio.token 动作的预期输出

你可以通过调用货币统计命令来确认代币已发行。> cleos get currency stats eosio.token TOKEN{  "TOKEN": {    "supply": "0.0000 TOKEN",    "max_supply": "20000000.0000 TOKEN",    "issuer": "eosio"  }}

### 发行代币

让我们创建另一个账户，你可以用来发送你发行的部分代币。我们称这个账户为 jane。> cleos create account eosio jane [public key]接下来，调用“发行”动作以发行代币。在这个例子中，你将向 jane 发行 500 代币。> cleos push action eosio.token issue '[ "jane", "500.0000 TOKEN", "move tokens to Jane" ]' -p eosio@active 要查看 jane 账户中的 TOKEN 余额，你可以使用 get currency 命令。> cleos get currency balance eosio.token jane TOKEN500.0000 TOKEN

### 转移代币

要转移代币，你运行转移动作。作为一个例子，让我们将代币从 Jane 的账户转移到 John 的账户。> cleos push action eosio.token transfer '[ "jane", "john", "100.0000 TOKEN", "transfer tokens" ]' -p jane@active 你可以通过在两个账户上运行货币余额命令来确认 John 的账户收到了代币，确保数学加起来。> cleos get currency balance eosio.token jane TOKEN  400.0000 TOKEN> cleos get currency balance eosio.token john TOKEN  100.0000 TOKEN 图 6-11 显示了预期输出。![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig11_HTML.jpg](img/475651_1_En_6_Fig11_HTML.jpg)

图 6-11

创建、转账和平衡 eosio.token 操作的预期输出

## 连接到公共测试网区块生产者

在撰写本文时，EOS.IO 提供了两个公共测试网，这样你可以在将代码提交到主网之前在一个更现实的环境中进行测试。

+   *Jungle2.0*: [`jungletestnet.io/`](https://jungletestnet.io/)

+   *Kylin*: [`www.cryptokylin.io/`](https://www.cryptokylin.io/)

在这个示例中，我选择了 Jungle2.0 作为公共测试网，但你可以随意测试两者；这个过程只是端点不同。

开始之前，请访问 Jungle 项目的 GitHub 页面：[`github.com/CryptoLions/EOS-Jungle-Testnet`](https://github.com/CryptoLions/EOS-Jungle-Testnet)。

EOS Jungle 测试网与你的本地测试网几乎完全相同。你只需要设置 Jungle API 端点并生成 EOS 水龙头代币来支付账户创建和 RAM 使用费用。

测试网 API 端点是[`jungle.eosio.cr:443`](https://jungle.eosio.cr:443)；只需添加端点，让你的之前的命令正常工作。

### 注意

在将你的代码发布到主网之前，总是要在测试网上进行测试。仅 2018 年 9 月，就有价值 24 万美元的 EOS 代币从 EOSBet 的智能合约账户中被盗，这是因为一个被黑客利用的智能合约编程错误，而不是 EOS.IO 平台本身的错误。你将在第十章了解更多关于安全性的内容。

要创建账户，你会生成两个默认权限：所有者和活跃。你可以通过访问[`nadejde.github.io/eos-token-sale/`](https://nadejde.github.io/eos-token-sale/)或者运行与你之前使用过的相同的命令行两次来完成这个操作。> cleos create key --to-console

接下来，你需要创建一个账户。你可以通过访问 Jungle 页面并使用你生成的公钥来创建账户：[`monitor.jungletestnet.io/#account`](https://monitor.jungletestnet.io/%2523account)。

我随机选择了一个名字 liontestaa11，但你可以使用任何你喜欢的名字。只要小心严格的名称限制（只允许 a-z 和 1-5，长度为 12）。如果你不遵守这种严格的名称限制，你的账户将无法创建。见图 6-12。![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig12_HTML.jpg](img/475651_1_En_6_Fig12_HTML.jpg)

图 6-12

Jungle2.0 的 liontestaa11 账户已创建

请注意，你会得到与你在本地测试网得到的相同的警告，关于交易将被执行，但它没有得到确认。

要获取关于测试网的信息，你可以运行你为本地的测试网运行的同一个 get info 命令。只需添加 Jungle 端点 URL 参数。> cleos --url https://jungle.eosio.cr:443 get info

### 在公共测试网区块生产商上购买资源分配

现在你将发布你在上一节中创建的“HelloWorld”智能合约。

如果你在主网上发布你的合约，你需要购买 RAM 并支付创建你的账户，这样你就可以发布你的智能合约了。EOS 代币用于购买资源。在公共测试网上，你不需要为你的资源花费实际的货币。你获得的水龙头代币可以用于 Jungle 区块生产商购买你的资源。

要获得这些代币，你只需要你的账户名称。输入你的账户名称从 Jungle 水龙头获得代币： [`monitor.jungletestnet.io/#faucet`](http://monitor.jungletestnet.io/%2523faucet)。见图 6-13。

我将在你准备在主网上发布时更详细地解释资源分配。![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig13_HTML.jpg](img/475651_1_En_6_Fig13_HTML.jpg)

图 6-13

Jungle2.0 通过 Jungle 水龙头获得代币

你可以使用 get account 命令检查账户余额； see the output in Figure 6-14。> cleos --url https://jungle.eosio.cr:443 get account liontestaa11

图 6-14

Jungle 水龙头账户余额

现在你有了 EOS 代币，你可以运行 cleos system buyram 命令来购买 RAM，这样你就可以发布你的智能合约了。> cleos --url https://jungle.eosio.cr:443 system buyram liontestaa11 liontestaa11 "10 EOS"

### 在公共测试网上发布你的 HelloWorld 合约

现在您有了代币，您可以将您的 HelloWorld 智能合约发布到公共测试网。运行设置合约命令。> cleos --url https://jungle.eosio.cr:443 set contract liontestaa11 ~/Desktop/helloworld 您可以使用获取代码命令确认代码已经发布。您可以在图 6-15 中看到整个预期输出。> cleos --url https://jungle.eosio.cr:443 get code liontestaa11![../images/475651_1_En_6_Chapter/475651_1_En_6_Fig15_HTML.jpg](img/475651_1_En_6_Fig15_HTML.jpg)

图 6-15

发布合约到公共测试网时预期的输出

## 连接到主网

EOS.IO 主网与测试网几乎相同；您只需要使用不同的 API 端点，并使用真实的 EOS 代币实际支付账户和 RAM。

获取 EOS 代币主要有三种方式：

+   *挖矿*：这创建了一个区块生产者并挖出了 EOS。

+   *购买 EOS 代币*：它们可以在加密货币交易所购买。

+   *赠送*：这是别人送给您一颗 EOS。

如您在前几章所看到的，创建一个区块生产者和被 EOS.IO 网络选中并不是一个简单的过程，也没有保证，而且您只需要硬币来购买 RAM 以开设账户和获取资源，所以您不需要太多硬币。在这个时候，仅仅购买这些代币是很容易的。

您首先需要在法币交易所如 Coinbase、CEX.io 或 Coinmama 上购买比特币、以太坊或其他硬币。然后使用像 Binance 或 Changelly 这样的交易所将您的硬币换成 EOS 代币。原因是截至写作之时，还没有已知交易所可以直接将您的法币换成 EOS。

接下来，您需要一个端点。21 个选定的区块生产者能够为您提供端点。您可以在以下链接找到所有可用的区块生产者和有关正在挖掘的区块的其他数据：

+   [`eosnetworkmonitor.io/`](http://eosnetworkmonitor.io/)

+   [`eostracker.io/producers`](https://eostracker.io/producers)

一旦找到您想要使用的区块生产者，您将 URL 的末尾加上/bp.json 以找到端点。这是一个例子：[`api.eosnewyork.io/bp.json`](https://api.eosnewyork.io/bp.json)。

该 JASON 输出提供了区块生产者的信息，并确保其可供使用。要设置 URL，只需调整--url 标志到您想要连接的区块生产者；其余命令与公共测试网完全相同。> cleos --url https://api.eosnewyork.io:443 get info 与公共测试网一样，您可以像之前一样编辑 bash 配置文件。alias cleos-mainnet='cleos --url https://api.eosnewyork.io:443 --wallet-url http://localhost:8888'您的 bash 配置文件应如下所示：PATH="/usr/local/eosio/bin:${PATH}"alias cleos-testnet='cleos --url https://jungle.eosio.cr:443 --wallet-url http://localhost:8888'alias cleos-mainnet='cleos --url https://api.eosnewyork.io:443 --wallet-url http://localhost:8888'通过运行 get info 命令确认它是否正常工作。> cleos-mainnet get info

我会省略与公共测试网部分相同的步骤，以及花费实际代币在“HelloWorld”示例智能合约上的操作。然而，我会涵盖资源分配，因为了解资源分配对于在主网发布智能合约非常重要。

### 资源分配解释

当我覆盖测试网时，我稍微提到了资源分配，因为您需要获得 EOS 代币才能在公共测试网上发布您的智能合约。

对于主网，您需要使用实际的 EOS 代币来购买 RAM 并创建您的账户。EOS.IO 账户消耗三种资源类型。

+   磁盘：带宽和日志存储（磁盘）

+   计算单元（CPU）：锁定计算资源和计算积压（CPU）

+   内存（RAM）：锁定状态存储

### 在主网上购买 RAM

为了释放 RAM，你需要从账户状态机制中删除数据，然后 RAM 就可以按照当前的 RAM 价格在 RAM 市场上出售。RAM 市场的价格可以在以下链接找到：[`www.feexplorer.io/EOS_RAM_price`](https://www.feexplorer.io/EOS_RAM_price)。

### 在主网上创建一个 EOS.IO 账户

EOS.IO 账户是必要的，因为它们需要与 EOS.IO 网络交互并创建账户。如我之前解释的，已经有一个账户的人需要为创建新账户提供担保。如果您没有能为您创建账户的 EOS 账户，您可以使用第三方提供商来创建账户。第三方提供商通常会向您收取费用。例如，您可以在手机上下载 EOS Lynx 并支付 2 美元来创建一个 EOS.IO 账户。

### 更改账户的公钥和私钥

一旦你获得了一个主网账户，你就没有完成。你需要确保在向账户注资之前更改你的私钥，因为创建你账户的服务可能只是存储你的私钥并拿走你的资金。你对这些步骤已经很熟悉了；这里唯一的新命令是 remove_key，它从你的钱包中删除旧的密钥。你创建一个新的密钥，解锁你的钱包，用新密钥重置权限，同时也删除旧的公钥并导入新的私钥。按照这些步骤操作：> cleos create key> cleos wallet unlock> cleos set account permission [ACCOUNT NAME] active [PUBLIC KEY] owner -p [ACCOUNT NAME]@owner> cleos set account permission MYACCOUNT owner [PUBLIC KEY] -p [ACCOUNT NAME]@owner> cleos wallet remove_key [OLD PUBLIC KEY]> cleos wallet import [PRIVATE KEY]

### CPU 和带宽分配

为了获得带宽和 CPU，你需要分配 EOS 代币，资源将在质押合同期间按照持有的金额自动为你提供。

例如，在质押窗口期间，假设你想消耗 1 个 CPU 单元。为此，你需要与其他账户竞争，以便在你的账户下有 0.1%的 CPU 质押代币，或者让其他人将这些代币委托给你的账户。

在质押期结束后，消耗的资源会释放，你可以重新使用相同的质押代币，因此每次都不需要继续购买更多的 EOS 代币。在你完成操作后，EOS 代币可以被取消委托。

## 从这里出发去哪里

EOS.IO 提供了一个在线资源，带有链接；请参阅[`developers.eos.io`](https://developers.eos.io)。该开发者资源提供了宝贵的文档以及其他我没有涵盖的工具的信息，例如这些：

+   状态处理程序：demux-js

+   JavaScript 库：eosjs

我也建议探索 EOS GitHub 上的智能合约示例，这将帮助你了解 EOS.IO 的所有功能以及什么是可能的。

## 摘要

在本章中，我详细介绍了 EOS.IO 区块链。你通过安装 EOS.IO 和 EOSIO.CDT 库来设置本地测试网络环境，并学习了如何配置 keosd 和 nodeos。你了解了 EOS.IO 钱包，包括如何创建、删除和备份钱包，以及如何创建具有自定义名称的钱包并进行操作，如打开、锁定和解锁钱包。

接下来，我介绍了钱包的密钥对以及如何启动和重新启动本地节点（nodeos）以运行本地区块生产商。你还了解了活动权限和所有者权限以及单签名（single-sig）和多签名（multisig）账户。

为了理解 EOS.IO 智能合约，你首先创建了账户，然后通过编写 C++ 代码创建了一个“HelloWorld”智能合约和代币。接着你编译并生成了 WebAssembly 和 ABI 文件以及 Ricardian 合约。你然后学习了如何部署你创建的合约并与之交互。一旦你的代币生成，你就可以发行并在账户之间转移代币。

你继续通过连接到一个公共测试网区块生产者，在更现实的环境中测试你的智能合约，最后你学习了如何连接并发布到主网，并了解了 EOS.IO 网络上的资源分配。

在下一章，我将介绍 NEO 区块链钱包和 NEO 智能合约。
