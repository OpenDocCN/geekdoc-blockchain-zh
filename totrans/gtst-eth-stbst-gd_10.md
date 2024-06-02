© 作者，Apress Media, LLC 独家许可，Springer Nature 2022D. P. Bauer 使用以太坊入门 [`doi.org/10.1007/978-1-4842-8045-4_10`](https://doi.org/10.1007/978-1-4842-8045-4_10)

# 10. Chainlink

Davi Pedro Bauer^(1  )(1)Campo Bom, Rio Grande do Sul, Brazil

Chainlink^(1) 是一个去中心化的节点网络，使用预言机将来自区块链外部来源的数据和信息传输到区块链智能合约中。在本章中，您将学习如何使用 Kovan 测试网上的 ETH/USD 价格源来访问智能合约内部的最新加密货币价格。

在本章结束时，您将能够执行以下操作：

+   为价格消费创建一个简单的智能合约

+   设置一个 Infura 项目

+   配置用于签署交易的私钥

+   在 Kovan 网络上部署智能合约

+   从 Kovan 网络上的智能合约获取价格信息

## 使用 Chainlink 预言机在智能合约内部获取加密货币价格

让我们从创建一个新项目开始，然后安装 Chainlink 合约包。您将使用一个现有的合约地址，该地址告诉您 ETH/USD 交易对的价格，然后您将能够看到该价格由您的智能合约返回。

### 创建项目

转到终端菜单，点击新终端，并初始化一个新的 Truffle 项目。$ truffle init 现在，初始化项目文件夹。$ npm init 最后，安装 Chainlink 合约包。^(2)$ npm install @chainlink/contracts@0.1.9

### 创建智能合约

为价格消费创建一个新的智能合约。$ touch contracts/PriceConsumer.sol 打开文件 PriceConsumer.sol（图 10-1）。![](img/521550_1_En_10_Fig1_HTML.jpg)

V S code 合同文件夹的屏幕截图显示了 Price Consumer dot s o l 标签页已打开。左侧窗格“资源管理器”有其他部分：合同下有 Migrations dot s o l 和 Price Consumer dot s o l（已选择）的存在，迁移，节点模块，测试以及两个 dot j s o n 和一个 dot j s 文件。

图 10-1

VS Code 合同文件夹

在 PriceConsumer.sol 文件中，定义 Solidity 版本，然后导入 Chainlink 合同接口。之后，定义合同名称和合同构造函数。// SPDX-License-Identifier: MITpragma solidity ⁰.8.0;import "@chainlink/contracts/src/v0.6/interfaces/AggregatorV3Interface.sol";contract PriceConsumer {    AggregatorV3Interface internal priceFeed;    constructor(){        priceFeed = AggregatorV3Interface()    }}转到 [`docs.chain.link/docs/ethereum-addresses`](https://docs.chain.link/docs/ethereum-addresses) 并滚动到 Kovan 部分。复制“ETH/USD”行上的代理地址（图 10-2）。![](img/521550_1_En_10_Fig2_HTML.jpg)

Chainlink 价格源的屏幕截图左侧列出了“使用价格源”。在“使用价格源”下有多个选项，其中之一是“联系地址”，已选中。在其下，“以太坊价格源”被选中。右侧是一个具有 3 列详细信息的表格，显示价格源的详细信息。

图 10-2

Chainlink 价格源

将地址粘贴到 AggregatorV3Interface 构造函数中。之后，创建获取价格的函数。// SPDX-License-Identifier: MITpragma solidity ⁰.8.0;import "@chainlink/contracts/src/v0.6/interfaces/AggregatorV3Interface.sol";contract PriceConsumer {    AggregatorV3Interface internal priceFeed;    constructor(){        priceFeed = AggregatorV3Interface(0x9326BFA02ADD2366b30bacB125260Af641031331);    }    function getThePrice() public view returns (int){        (            uint80 roundID,            int price,            uint startedAt,            uint timeStamp,            uint80 answeredInRound        ) = priceFeed.latestRoundData();        return price;    }}

### 创建迁移

在迁移文件夹中创建迁移文件。$ touch migrations/2_deploy_contracts.sol 编写代码以部署 PriceConsumer 智能合约（见图 10-3）。const PriceConsumer = artifacts.require("PriceConsumer");module.exports = function(deployer){    deployer.deploy(PriceConsumer);};![](img/521550_1_En_10_Fig3_HTML.jpg)

V S code 迁移文件夹的屏幕截图有 2 个下划线 deploy 下划线 contracts dot j s 标签打开。窗口上显示数字 1。

图 10-3

VS Code 迁移文件夹

### 设置你的 Infura 项目

转到 [`infura.io`](https://infura.io) 并访问您的仪表板。点击以太坊，然后点击“创建项目”。最后，定义项目名称并复制项目 ID（见图 10-4）。注意，您可以连接到不同的测试网络，也可以连接到主网络。![](img/521550_1_En_10_Fig4_HTML.jpg)

Infura 设置的屏幕截图左侧有一个仪表板。顶部的条形上有标题以太坊。设置标签已打开。在主屏幕上必须输入项目详细信息。第一部分有一个名为 '以太坊' 的名称，是一个必填字段，第二部分有项目 I D 显示的密钥。

图 10-4

安装钱包提供程序 hdwallet 包。这也会安装启用 HD 钱包的 Web 3 提供程序，用于为从 12 或 24 个字助记符派生的地址签名交易。$ npm install @truffle/hdwallet-provider@1.2.3

将 Ropsten Infura URL 更改为 kovan。

### 在 truffle-config.js 中，取消注释 ropsten 网络部分，并更改以下值：

安装文件系统 fs 包。该包提供了许多有用的功能，用于访问和与文件系统交互。$ npm install fs

转到浏览器，并打开连接到 Infura 网络的您的 MetaMask 钱包。点击“您的账户”，然后点击“设置”。最后，点击“安全与隐私”（图 10-5）。![](img/521550_1_En_10_Fig5_HTML.jpg)

### 配置钱包以签署交易

打开 truffle-config.js 文件，并取消注释 HDWalletProvider 代码部分。const HDWalletProvider = require('@truffle/hdwallet-provider');const infuraKey = '<your_infura_key>';const fs = require('fs');const mnemonic = fs.readFileSync(".secret").toString().trim();

+   创建 secret 文件如下：$ touch .secret

+   配置网络

+   将 ropsten 更改为 kovan。

+   Infura 设置

将 YOUR-PROJECT-ID 更改为 ${infuraKey}。

### 将您的 Infura 项目 ID 粘贴为变量 infuraKey 的值。

配置私钥

### 配置 Solidity 编译器

现在，点击“保存更改”。

Reveal Seed Phrase 设置的安全与隐私窗口截图。有一个文本写着 '显示种子短语'，下面有一个相同文本的按钮，光标放在按钮上。

图 10-5

MetaMask：显示种子短语

您有查看种子短语的选项，但请注意这些信息很敏感，如果有人可以访问它，他们将能够恢复您的钱包并使用您的资金。

单击“显示种子短语”，然后输入您的钱包密码以继续。复制私钥。返回到 Visual Studio Code，并将私密恢复短语粘贴到文件 .secret 中。

### 编译智能合约

使用 Truffle 编译合约。$ truffle compile

### 部署智能合约

使用 Truffle 将合约部署到 Kovan 网络。迁移命令在 Kovan 网络上运行迁移以部署合约。$ truffle migrate --network kovan 等待合约部署和区块链上的交易确认。现在，检查您创建的合约地址（图 10-6）。![](img/521550_1_En_10_Fig6_HTML.jpg)

V S code 部署合约输出窗口的截图包括 Problems、Output、Terminal 和 Debug console 选项卡。代码显示在终端选项卡中，显示了交易、区块、合约地址、区块号、时间戳、账户、余额、使用的 gas、gas 价格、发送的价值和总成本的详细信息。

图 10-6

VS Code 部署合约输出

### 从智能合约获取价格信息

使用 Truffle 控制台实例化合约。此控制台命令将打开一个基本的交互式控制台，连接到 Kovan 网络上的以太坊客户端：$ truffle console --network kovan 现在，使用 deployed 命令在 Kovan 网络上返回已部署的合约实例，如下所示：truffle(kovan) let instance = await PriceConsumer.deployed()调用 getThePrice 方法。let 命令将方法结果存储在变量 price 中，而 await 命令将异步执行该方法。truffle(kovan) let price = await instance.getThePrice()最后，将结果输出为数字。toNumber() 方法将大数对象转换为常规数字。truffle(kovan) price.toNumber()265499339990

就这样，您刚刚创建了一个智能合约，并使用了 Chainlink 价格信息预言机！

## 摘要

在本章中，您学会了如何使用 Chainlink 创建一个简单的智能合约，以从 Chainlink 预言机获取价格信息。

在下一章中，您将了解到 Nethereum，一个用于以太坊的 .NET 库。
