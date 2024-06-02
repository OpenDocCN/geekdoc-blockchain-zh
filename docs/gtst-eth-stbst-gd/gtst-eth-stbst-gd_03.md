© 作者(们)，独家许可给 APress Media, LLC，Springer Nature 其中一部分 2022D. P. Bauer 开始使用以太坊 [`doi.org/10.1007/978-1-4842-8045-4_3`](https://doi.org/10.1007/978-1-4842-8045-4_3)

# 3. ERC-20：可替代通证

Davi Pedro Bauer^(1  )(1)Campo Bom, Rio Grande do Sul, Brazil

可替代通证是每个单位具有相同价值的通证，就像法定货币一样。这意味着你可以用同等价值的另一个单位交换这种货币的一个单位。考虑在区块链上复制此行为，Fabian Vogelsteller 和 Vitalik Buterin 在 2015 年 11 月提出了 ERC-20，“以太坊请求评论 20”，以创建以太坊基于通证的简单格式。这些通证在以太坊区块链内运行，并能与网络上的其他加密货币进行交互。在本章中，你将创建符合 ERC-20 标准的简单合约，并学习如何将它们部署到测试和生产网络。

在本章结束时，你将能够完成以下任务：

+   编写符合 ERC-20 标准的简单合约。

+   编写固定供应合约。

+   使用 OpenZeppelin 继承关键实现。

+   使用 Truffle 编译合约。

+   使用 Ganache 启动本地主机区块链。

+   将现有合约部署到 Ganache。

+   配置 MetaMask 连接到 Ganache。

+   将部署的通证合约添加到你的 MetaMask 钱包。

+   将合约迁移到 Ganache。

+   在账户之间转移通证。

+   将 Polygon Mumbai 添加到 MetaMask 网络。

+   在 Infura 上启用 Polygon 插件。

+   配置私钥以签署合约。

+   在 Polygon Mumbai 上部署智能合约。

+   将 Polygon 主网添加到 MetaMask 网络。

+   配置网络以使用 Polygon 主网。

+   在 Polygon 主网上部署智能合约。

+   在 Polygon 主网上验证智能合约。

## 使用 OpenZeppelin 编写简单的 ERC-20 通证。

让我们使用 Truffle 开发一个简单的 ERC-20 以太坊^(1) 智能合约，然后导入 OpenZeppelin 合约库。

OpenZeppelin 是一个开源且可审计的库，允许您从更常见的实现中重复使用代码，因此作为始终相同的初始代码库。使用 OpenZeppelin 可以让您更专注于编码业务需求，而不是重复不必要的代码。

我们将在这个示例和本书的后续章节中使用 OpenZeppelin 库。

代币可以在以太坊中代表几乎一切，比如以下内容：

+   在线平台上的声誉积分

+   游戏中一个角色的技能

+   彩票

+   类似公司股份这样的金融资产

+   像美元（USD）这样的法定货币

+   一盎司黄金

### 准备环境

使用以下命令初始化 Truffle：$ truffle init 现在，初始化项目文件夹：$ npm init 最后，安装 OpenZeppelin 合约包：$ npm install @openzeppelin/contracts

### 编写合约

在 contracts 文件夹下创建一个名为 ERC20MinerReward.sol 的新文件。 添加许可证指令，定义 Solidity 的最低版本，并导入 OpenZeppelin ERC-20 合约库。 最后，定义合约类、合约构造函数、合约名称和合约符号。// SPDX-License-Identifier: MITpragma solidity ⁰.8.0;import "@openzeppelin/contracts/token/ERC20/ERC20.sol";contract ERC20MinerReward is ERC20 {    constructor() ERC20("MinerReward", "MRW"){}}

### 设置 Solidity 编译器版本

复制此合约中使用的 Solidity 版本，然后打开 truffle-config.js*.* 取消注释 solc 块，并通过粘贴复制的值设置 Solidity 版本。compilers: {    solc: {        version: "0.8.0",        docker: true,        settings: {            optimizer: {                enabled: false,                runs: 200            },            evmVersion: "byzantium"        }    }},

### 编译合约

现在是时候编译合约了。$ truffle compile

合约成功编译！

### 验证结果

注意到一个新文件夹 build/contract 被创建了（见图 3-1）。新合约在那里！![](img/521550_1_En_3_Fig1_HTML.jpg)

Truffle 编译结果的截图。左侧是标题为“资源管理器”的部分，在其中选择了 Solidity、构建/合约。主屏幕顶部选择了终端，终端下面的程序显示“$ truffle compile”，并列出了编译的列表。

图 3-1

Truffle 编译结果

## 将 ERC-20 代币部署到 Ganache 开发区块链

Ethereum Ganache 是一个本地内存区块链，用于开发和测试。它模拟了真实以太坊网络的特性，包括可用于测试以太的多个账户。

这是在将合约移至主网络之前部署合约的一种好方法。使用开发区块链，您可以专注于实施而不必担心花费真钱来部署合约。

### 准备迁移

在迁移文件夹下创建一个名为 2_deploy_contracts.js 的新迁移文件。在第一行添加一个指向智能合约的引用，并添加一个导出函数以部署智能合约（见图 3-2）。![](img/521550_1_En_3_Fig2_HTML.jpg)

在 Solidity 区块下的迁移文件夹的截图，其中选择了 2_deploy_contracts.js 标签。命令提示符显示，const ERC20MinerReward = artifacts.require("ERC20MinerReward")。下方是继续的命令。

图 3-2

新迁移文件

### 启动区块链

打开一个新的终端并启动 Ganache 区块链。$ ganache-cli

一个新的 Ganache 区块链正在监听 127.0.0.1:8545。

### 配置区块链网络

打开 truffle-config.js 并取消对网络中的开发块的注释。 确保主机和端口是正确的（图 3-3）。![](img/521550_1_En_3_Fig3_HTML.jpg)

选择 truffle-hyphen-config.js 标签页的屏幕截图。 在其中，网络部分已打开。 提供了几个网络下的指令。 提供的其他部分如下：开发，其中提供了主机、端口和网络 ID 的详细信息。 底部提供了高级选项的进一步信息。

图 3-3

开发网络

### 部署合同

使用以下命令编译合同：$ truffle compile 使用以下命令迁移合同：$ truffle migrate 合同已部署到 Ganache 区块链，并创建了合同地址（图 3-4）。![](img/521550_1_En_3_Fig4_HTML.jpg)

一个 truffle migrate contract 的屏幕截图有 4 个标签页，分别是问题、输出、调试控制台和终端，其中终端被选中。 终端中有 4 个主要部分：编译您的合同、开始迁移、1_ 初始迁移.j s 和摘要。

图 3-4

Truffle 迁移合同

### 将 Ganache 添加到 MetaMask 网络

打开 MetaMask 扩展并点击网络下拉菜单。 选择自定义 RPC 选项，并设置以下字段，如图 3-5 所示：

+   将网络名称设置为 **Localhost 8545**。

+   将 RPC URL 设置为 **http://localhost:8545**。

+   将链 ID 设置为 **1337**。

+   将货币符号设置为 **ETH**。

![](img/521550_1_En_3_Fig5_HTML.jpg)

在以太坊主网下的网络窗格的屏幕截图。 有关恶意网络的警告消息，随后是网络名称、本地主机 8 5 4 5、新的 RPC URL 链接、链 ID、1 3 3 7、货币符号，可选的，为 E T H。 底部的文本显示区块浏览器 URL，这也是可选的。

图 3-5

MetaMask 网络配置

### 将令牌添加到钱包

转到 Brave 浏览器（或任何与 MetaMask 兼容的浏览器），并选择“Localhost 8585”网络。

点击“添加令牌”，然后点击“自定义令牌”。 复制合同地址。 将其粘贴到“令牌合同地址”字段中。

“令牌符号”和“小数精度”字段将自动填充。点击“下一步”，然后点击“添加令牌”。 令牌已添加到 MetaMask 钱包。 令牌已经在那里了！

## 创建具有固定供应的 ERC-20 令牌

智能合同中允许的代币总数由 ERC-20 固定供应代币定义。 一旦部署到区块链上，您将无法更新合同。 这意味着在部署后，您的硬币将有固定数量，您将无法以后用更多硬币进行资助。

### 创建项目

初始化一个新的空以太坊项目。$ truffle init 为项目创建一个 package.json 文件。$ npm init 安装 OpenZeppelin 合同包。 它包含用 Solidity 编写的可重用智能合同。$ npm install @openzeppelin/contracts

### 编写固定供应合同

创建一个新的 solidity 文件，并执行以下操作：

1.  1.

    包含许可声明（这是强制性的）。

1.  2.

    定义 Solidity 最低版本。

1.  3.

    导入 OpenZeppelin ERC-20 合同库。

1.  4.

    定义固定供应合同类，继承自 ERC-20。

1.  5.

    调用构造函数，传递名称和符号。

1.  6.

    将总供应量分配给发送方地址（创建合同的人）。

1.  7.

    覆盖小数函数。

1.  8.

    设置此令牌将具有的小数位数。

// SPDX-License-Identifier: MITpragma solidity ⁰.8.0;import "@openzeppelin/contracts/token/ERC20/ERC20.sol";contract ERC20FixedSupply is ERC20 {    constructor() ERC20("Fixed", "FIX"){        _mint(msg.sender, 1000);    }    function decimals() public view virtual override returns (uint8){        return 0;    }}打开 truffle-config.js 文件并取消注释 solc 块（Ctrl+;）。现在，更新 Solidity 版本号。compilers: {    solc: {        version: "0.8.0",        docker: true,        settings: {            optimizer: {                enabled: false,                runs: 200            },            evmVersion: "byzantium"        }    }},在迁移文件夹下，创建一个新文件。将名称设置为 2_deploy_contracts.sol。$ touch migrations/2_deploy_contracts.sol 在此文件中，将所需方法设置为您的合约文件，并导出一个函数以部署合约。var ERC20FixedSupply = artifacts.require("./ERC20FixedSupply.sol");module.exports = function(deployer){    deployer.deploy(ERC20FixedSupply);}

### 编译合约

现在是编译合约的时候了。$ truffle compile

合约编译成功！

### 启动 Ganache 开发区块链

分割终端视图。现在，在 127.0.0.1:8545 上启动 Ganache 开发区块链。$ ganache-cli 打开 truffle-config.js 文件，在网络下取消注释开发块。networks: {    development: {        host: "127.0.0.1",        port: 8545,        network_id: "*"    },}

### 将合约迁移到 Ganache

运行迁移命令以部署合约，如图 3-6 所示。$ truffle migrate![](img/521550_1_En_3_Fig6_HTML.jpg)

显示了 truffle 编译结果的截图，左侧有菜单栏，选择了 truffle-config.js。 屏幕的主要部分有四个选项卡：问题、输出、终端和调试控制台，其中终端被选中。 终端文本显示正在编译您的合约。 它已经编译完毕，正在等待输入。

图 3-6

VS Code：使用 truffle 命令行迁移项目

在继续下一节之前，请复制部署代币的账户的私钥。

### 配置 MetaMask

打开 MetaMask。 点击您的账户，然后点击“导入账户”。 在此步骤中，粘贴账户私钥。 点击“导入”，如图 3-7 所示。![](img/521550_1_En_3_Fig7_HTML.jpg)

导入账户页面的截图。 在“导入账户”标题下面，有一条消息，内容是“导入的账户将不与您最初创建的 Metamask 账户关联”。 下面是选择类型字段，私钥已被选择。 在下面，输入私钥字符串的字段有一个虚线。 导入按钮在底部突出显示。

图 3-7

MetaMask：使用种子短语导入现有钱包 点击网络列表，然后点击本地主机：8545。 使用本地主机网络意味着您将把钱包指向您的本地开发区块链，如图 3-8 所示。![](img/521550_1_En_3_Fig8_HTML.jpg)

网络页面的截图。 顶部的文本显示显示或隐藏测试网络，右侧有一个关闭按钮。 一些可见网络的列表如下。 Polygon Mumbai，ropsten 测试网络，kovan 测试网络，rinkeby 测试网络等。 在左侧的 ropsten 测试网络旁边有勾选标记。 添加网络按钮位于底部。

图 3-8

MetaMask：网络选择列表

### 将代币添加到 MetaMask

点击“添加代币”，然后选择“自定义代币”。粘贴代币合约地址，然后点击“下一步”。

添加代币只是添加所创建代币的合约公共地址的问题。之后，MetaMask 将自动读取符号和小数位数。确保获得与图 3-9 中显示的相同结果。![](img/521550_1_En_3_Fig9_HTML.jpg)

添加代币窗口的屏幕截图有 2 个选项卡，搜索和自定义代币。已选择自定义代币。下方有一个用于 Token 合约地址的条形码，其中包含地址，代币符号为 fix，精度小数位为 0。

图 3-9

MetaMask：添加自定义代币

点击“添加代币”。屏幕上将显示代币符号以及您的余额（图 3-10）。![](img/521550_1_En_3_Fig10_HTML.jpg)

添加代币窗口的屏幕截图有一个问题，问：“是否要添加这些代币？” 左侧是单词 “代币” 和一个名为 Fix 的彩色圆形图标。右侧给出了单词 “余额” 和 1000 Fix。

图 3-10

MetaMask：新自定义代币概览

现在，返回到 VS Code（参见图 3-6，显示 ganache-cli 终端视图），并复制另一个账户的私钥。返回到 MetaMask 并重复为第一个账户所做的步骤，包括添加代币。

### 在账户之间转移代币

现在，切换到第一个导入的账户（拥有所有代币的账户）。点击“发送”，然后点击“在我的账户之间转移”。选择第二个创建的账户。输入 **115 FIX** 作为要转移的金额，然后点击“下一步”。最后，点击“确认”。

交易已发送，但处于待处理状态。请等待片刻，直到交易得到确认。确认后，代币的总数将会更新。选择第二个导入的账户；现在这个账户有 115 FIX！

## 将 ERC-20 代币部署到测试网络使用 Infura

Infura 可用于将智能合约部署到测试网络，如 Ropsten、Kovan、Rinkeby、Goerli，还有主网络。对于测试网络，您需要在 Infura 上创建一个新项目，并访问钱包的私钥，用于部署合约。为了执行合约创建交易，此钱包必须有以太坊余额。

### 安装前提条件

打开一个新的终端并安装 fs 包。安装此包提供了访问和与文件系统交互的有用功能。$ npm install fs 现在，安装钱包提供者 hdwallet 包。这用于为从 12 或 24 个字的助记词派生的地址签署交易。$ npm install @truffle/hdwallet-provider@1.2.3

### 设置你的 Infura 项目

前往 [`infura.io`](http://infura.io) 并访问你的仪表板。点击 “Ethereum”，然后点击 “创建一个项目”。定义项目名称。注意你可以连接到不同的测试网络，也可以连接到主网络。复制项目 ID 并保存更改。

### 设置你的智能合约

打开 Visual Studio Code 并打开 truffle-config.js 文件。取消注释四个常量：hdwalletprovider、infurakey、fs 和 mnemonic。将项目 ID 粘贴为 Infurakey 常量的值。取消注释 ropsten 区块。确保你在 ropsten 终端使用了正确的项目 ID。const HDWalletProvider = require('@truffle/hdwallet-provider');const infuraKey = "fj4jll3k.....";const fs = require('fs');const mnemonic = fs.readFileSync(".secret").toString().trim();

### 配置私钥

前往浏览器并打开连接到 Infura 网络的你的 MetaMask 钱包。点击 “*your account*”，然后点击 “settings”，最后点击 “security & privacy”（图 3-11）。

您可以选择查看您的助记词，但请注意这些信息是敏感的，如果有人可以访问它，他们将能够恢复您的钱包并使用您的资金。![](img/521550_1_En_3_Fig11_HTML.jpg)

在 Ropsten 测试网络的《安全与隐私》窗口的屏幕截图。屏幕上有一个短语写着“显示助记词”，有一个带光标的按钮，上面也写着“显示助记词”。

图 3-11

MetaMask：显示助记词

点击“显示助记词”，并输入您的钱包密码以继续；然后复制私钥。

回到 Visual Studio Code（图 3-6）并创建一个名为 .secret 的新文件。将私钥粘贴到此文件中。您也可以使用命令行创建此文件（图 3-12）。$ touch .secret![](img/521550_1_En_3_Fig12_HTML.jpg)

一个屏幕截图显示了在 Solidity 区块下选择了迁移文件夹。命令提示符上写着美元符号 touch 空格 点秘密。

图 3-12

秘密文件

### 部署智能合约

打开终端并运行迁移命令在 Ropsten 网络部署合约。$ truffle migrate --network ropsten

### 检查您的钱包余额

再次转到您的 MetaMask 钱包，并注意到您的余额已经减少了。

### 在 Etherscan 上验证智能合约

打开一个新窗口并复制在部署阶段创建的合同地址。转到 [`ropsten.etherscan.io`](https://ropsten.etherscan.io) 并将合同地址粘贴到搜索栏中。点击“查找”按钮。智能合约就在那里！

代币被创建并转移到创建合约的钱包。点击“固定(FIX)”代币链接。在这里你可以看到你的新创建的代币的概述。

## 部署 ERC-20 代币到 Polygon Testnet（第 2 层）

Polygon 是用于构建和连接与以太坊兼容的区块链网络的协议和框架。您可以在以太坊上聚合可扩展的解决方案，以支持多链以太坊生态系统。

MATIC，Polygon 的原生代币，是在以太坊区块链上运行的 ERC-20 代币。这些代币用于 Polygon 上的支付服务，并作为 Polygon 生态系统内的用户之间的结算货币。

### 安装先决条件

打开一个新的终端并安装 fs 包，如果您还没有安装的话。此包提供了许多有用的功能，用于访问和与文件系统交互。$ npm install fs 现在，如果您还没有安装的话，请安装钱包提供者 hdwallet 包。它用于为从 12 或 24 个单词的助记符派生的地址签名交易。$ npm install @truffle/hdwallet-provider@1.4.0

### 将 Polygon Mumbai 添加到 MetaMask 网络

打开 MetaMask 扩展程序，点击网络下拉菜单。然后选择自定义 RPC 选项。设置以下值，如图 3-13 所示：

+   将网络名称设置为**Matic Testnet**。

+   将 RPC URL 设置为[**https://rpc-mumbai.maticvigil.com**](https://rpc-mumbai.maticvigil.com)。

+   将链 ID 设置为**80001**。

+   将货币符号设置为**MATIC**。

+   将区块浏览器 URL 设置为[**https://explore-mumbai.maticvigil.com**](https://explore-mumbai.maticvigil.com)。

![图](img/521550_1_En_3_Fig13_HTML.jpg)

MetaMask 网络配置页面的截图如下所示。网络名称，Matic Testnet。新的 RPC URL 下方有输入的链接。Chain ID 为 80001；货币符号，可选为 MATIC。最后一行写着区块浏览器 URL，可选，使用提供的链接。

图 3-13

MetaMask：网络配置页面

### 在 Infura 上激活 Polygon 插件

转到[`infura.io/upgrade`](https://infura.io/upgrade)，点击 Polygon PoS 下的网络附加组件中的选择插件，如图 3-14 所示。Polygon PoS 目前在 Infura 上是 beta 版本，您需要激活它。![](img/521550_1_En_3_Fig14_HTML.jpg)

网络附加组件窗口的屏幕截图将 Polygon PoS 描述为以太坊主网的混合 Plasma 权益证明侧链，该侧链利用 Tendermint 共识验证层和 Plasma 侧链进行区块生产。下方显示了选择附加组件和更多功能即将推出的按钮。每月`$200`的定价已被划掉。

图 3-14

Infura：Polygon PoS 激活页面

激活后，您将被重定向到摘要页面。免费层每天限制为`100,000`个请求。您将被要求提供信用卡以进行确认；由于总费用为零，您将不会被收费。如果同意，请单击立即开始。您应该会看到一个类似于图 3-15 所示的页面。![](img/521550_1_En_3_Fig15_HTML.jpg)

摘要窗口的屏幕截图将订单总额列为每月`$0`，总请求数为每天`100,000`，核心层为每天`100,000`个请求的费用为每月`$0`，Polygon PoS 的附加组件费用为每月`$0`。还有一个可以应用的折扣代码。下方有一个已保存信用卡的结账部分。

图 3-15

Infura：添加 Polygon PoS 插件后的摘要页面订单

### 设置您的 Infura 项目

确保您在 Infura 上已经设置了一个项目。如果还没有，请按照第一章中的步骤操作。

### 设置您的智能合约

前往 Visual Studio Code 并打开 truffle-config.js 文件。取消注释四个常量：hdwalletprovider、infurakey、fs 和 mnemonic，并将项目 ID 粘贴为 infurakey 常量的值。const HDWalletProvider = require('@truffle/hdwallet-provider');const infuraKey = "fj4jll3k.....";const fs = require('fs');const mnemonic = fs.readFileSync(".secret").toString().trim();

### 配置网络（使用 Matic 终端）

连接到 Polygon 网络的第一种方法是使用 Matic 网络。现在，在 truffle-config.js 文件的 networks 下创建一个名为 matic_testnet 的配置，并设置以下值：

+   将钱包 URL 设置为 [`rpc-mumbai.maticvigil.com`](https://rpc-mumbai.maticvigil.com)。

+   将 network_id 设置为 80001。

matic_testnet: {  provider: () => new HDWalletProvider(mnemonic, `https://rpc-mumbai.maticvigil.com`),  network_id: 80001,  confirmations: 2,  timeoutBlocks: 200,  skipDryRun: true},

### 配置网络（使用 Infura 终端）

另一种连接到 Polygon 网络的方法是使用 Infura 终端。在 networks 下创建一个名为 matic_testnet 的配置，并设置以下值：

+   将钱包 URL 设置为 [`polygon-mumbai.infura.io/v3/${infuraKey}`](https://polygon-mumbai.infura.io/v3/%2524%257binfuraKey%257d)。

+   将 network_id 设置为 80001。

matic_testnet: {  provider: () => new HDWalletProvider(mnemonic, `https://polygon-mumbai.infura.io/v3/${infuraKey}`),  network_id: 80001,  confirmations: 2,  timeoutBlocks: 200,  skipDryRun: true,  chainId: 80001,  networkCheckTimeout: 1000000},

要使用 Polygon 网络，您需要激活网络附加组件。

### 配置私钥

转到浏览器并打开连接到 Infura 网络的 MetaMask 钱包。单击“*your account*”，然后单击“settings”。最后，单击“security & privacy”，如图 3-16 所示。![](img/521550_1_En_3_Fig16_HTML.jpg)

在 Ropsten 测试网络的安全与隐私窗口的屏幕截图。屏幕上的短语为“显示种子短语”，有一个带有光标的长按钮，上面也写着“显示种子短语”。

图 3-16

MetaMask：显示种子短语

您可以选择查看您的种子短语，但请注意此信息非常敏感，如果有人可以访问它，他们将能够恢复您的钱包并使用您的资金。

点击“显示种子短语”，输入您的钱包密码以继续。复制私钥。

返回到 VS Code（在 ganache-cli 终端视图上）并创建一个名为 .secret 的新文件。将私有的恢复短语粘贴到此文件中。

### 部署智能合约

运行 migrate 命令将合约部署到 matic_testnet 网络。$ truffle migrate --network matic_testnet 如果在终端上出现此错误，则需要先从 Faucet 获取测试 MATIC。1_initial_migration.js====================== 部署'Migrations'----------------------错误：*** 部署失败 ***“迁移”--燃料不足以支付 gas * 价格 + 值。

### 检查您的钱包余额

再次转到您的 MetaMask 钱包，注意您的余额已经减少。这是因为您需要为每个合约部署支付费用。它具有 gas 的等价成本，并且该成本是根据您在智能合约中使用的指令计算的。这意味着您需要更多的机器处理，您执行此合约的 gas 成本就越高。您可以在[Ethereum 黄皮书](https://ethereum.github.io/yellowpaper/paper.pdf)中找到更详细的解释。

### 在 PolygonScan 上验证智能合约

复制在部署中创建的合约地址（此地址将在 truffle migrate 运行完成后显示在控制台中），然后转到[`mumbai.polygonscan.com`](https://mumbai.polygonscan.com)。将合约地址粘贴到搜索栏中，然后点击“查找”按钮。智能合约就在这里！

代币已经创建并转移到创建合约的钱包中。现在，点击“Fixed (FIX) token”链接，在这里你可以看到你新创建的代币的概述！

## 将 ERC-20 代币部署到 Polygon 主网（Layer 2）

主网用于真实交易，而测试网用于测试智能合约和去中心化应用（DApps）。Polygon 作为第二层而受到欢迎，因为其交易成本低于主网。

### 向 MetaMask 网络添加 Polygon 主网

打开 MetaMask 扩展程序，点击网络下拉菜单，然后选择自定义 RPC 选项。按照图 3-17 所示设置以下值：

+   将网络名称设置为**Matic Mainnet**。

+   将 RPC URL 设置为[**https://rpc-mainnet.maticvigil.com**](https://rpc-mainnet.maticvigil.com)。

+   将链 ID 设置为**137**。

+   将货币符号设置为**MATIC**。

+   将区块浏览器 U R L 设置为[**https://explore-mainnet.maticvigil.com**](https://explore-mainnet.maticvigil.com)。

![](img/521550_1_En_3_Fig17_HTML.jpg)

网络配置页面的截图如下字段已填写。网络名称，Matic Mainnet。新 R P C U R L，带有链接。链 ID，137。货币符号，可选。Matic。区块浏览器 U R L，可选，带有链接添加。

图 3-17

MetaMask：网络配置页面

### 配置网络（使用 Infura 端点）

连接到 Polygon 网络的另一种方法是使用 Infura 端点。在网络下创建一个 matic_mainnet 配置，并设置以下值：

+   将钱包 URL 设置为[`polygon-mainnet.infura.io/v3/${infuraKey}`](https://polygon-mumbai.infura.io/v3/%2524%257binfuraKey%257d)。

+   将 network_id 设置为 137。

matic_mainnet: {  provider: () => new HDWalletProvider(mnemonic, `https://polygon-mainnet.infura.io/v3/${infuraKey}`),  network_id: 137,  gasPrice: 100000000,  confirmations: 2,  timeoutBlocks: 200,  skipDryRun: true,  chainId: 137,  networkCheckTimeout: 1000000},

### 部署智能合约

运行 migrate 命令以将合约部署到 matic_mainnet 网络。truffle migrate --network matic_mainnet

### 检查您的钱包余额

再次打开你的 MetaMask 钱包，注意你的余额已经减少。

### 在 PolygonScan 上验证智能合约

复制在部署中创建的合约地址，然后前往 PolygonScan。^(2)将合约地址粘贴到搜索字段中，然后点击查找按钮。智能合约就在那里！

代币已被创建并转入了创建合约的钱包。现在，点击固定(FIX)代币链接，在这里你可以看到你新创建代币的概览。

## 总结

在本章中，你学习了 ERC-20 代币标准是什么，并学会了如何将通证化代币部署到 Ganache 以及部署到以太坊和 Polygon 区块链上的测试网和主网。

在下一章中，您将探索智能合约上的单元测试，并学习如何编写您的第一个单元测试。
