© Elad Elrom 2019Elad ElromThe Blockchain Developer[`doi.org/10.1007/978-1-4842-4847-8_10`](https://doi.org/10.1007/978-1-4842-4847-8_10)

# 10. 使用 Angular 构建 Dapp：第 II 部分

Elad Elrom^(1 )(1)New York, NY, USA

在上一章中，你开始开发你的 dapp。具体来说，你了解了 dapp 的分类和项目，以及你可以将你的 dapp 项目分为五个步骤。然后你查看了为什么要使用 Angular 以及它的好处。接下来，你创建了一个 Angular 项目，首先确保预先安装了必备条件，然后安装了 Angular CLI。你了解了组成 Angular 的部分，如组件、模块和指令。你还学会了如何通过理解 Angular 风格架构和工作于 Angular Material 来样式化 dapp。你开始构建自己的自定义组件和创建内容；你将你的应用分为页脚、页头和正文，并创建了一个自定义的传输组件，你将在本章中使用它。

在本章中，我将介绍以下内容：

+   使用 Truffle 创建 dapp 的智能合约

+   在你的 dapp 的 Angular 项目中集成智能合约

+   将你的 dapp 连接到以太坊网络

你将利用我到目前为止介绍的工具：Angular CLI、Truffle、ganache-cli 和 MetaMask。你将使用 Truffle 创建一个智能合约，用于你的 dapp，然后你将使用 web3 库连接到以太坊本地网络，并调用智能合约的功能和事件。MetaMask 将用于管理和连接到你的账户。

### 提示

建议你在学习本章之前完成上一章和第五章，以便完全理解这里的示例，这些示例基于第九章和第五章中介绍的概念、工具和已安装的库。

## 传输智能合约

你已经在上一章中为你的应用创建了前端逻辑，用于传输代币；然而，你还没有一个智能合约与区块链交互。智能合约可以在前端部分之前、之后或同时创建（如果你与开发团队一起工作）。

你已经在第五章中创建了一个以太坊智能合约，所以本节中的步骤应该对你来说很熟悉。随意复习第五章以刷新你的记忆，因为我在本章中不会详细介绍使用的工具和命令。

开始之前，你将在你的 ethdapp 项目中创建一个新文件夹，以保存 Truffle 项目。你可以从这里下载最新的步骤，继续你上次的进度：[`github.com/Apress/the-blockchain-developer/chapter9/step5.zip`](https://github.com/Apress/the-blockchain-developer/chapter9/step5.zip) 。

在具有多个开发者的实际项目中，智能合约可能是一个单独的项目。为了简化，你将将其包含在你的项目中，这样你就可以利用 WebStorm 终端窗口的底部标签来运行命令。

首先在你的项目中创建一个名为 truffle 的文件夹，并初始化 Truffle 以创建项目。你可以在图 10-1 中看到预期的输出。

图 10-1

创建 Truffle 项目的输出

### 提示

如果你遇到错误，如“Error: Truffle Box”，则卸载 Truffle，然后重新安装并再次尝试。

如果出现错误消息需要重新安装 truffle，请先卸载 truffle 全局，然后再次安装。

图 10-2

Truffle 编译、迁移和测试你的项目

### 创建智能合约

你将创建一个智能合约，并将其命名为 Transfer.sol；将其放在这里：truffle/contracts/Transfer.sol。该合约允许你将资金从一个账户转移到另一个账户。首先导航到 Truffle 中合约的位置，并使用编辑器创建一个新文件。

就是这些。你只保留了一个事件和一个函数，使得一切简单明了。你可以从这里下载这个步骤：[`github.com/Apress/the-blockchain-developer/chapter10/step1.zip`](https://github.com/Apress/the-blockchain-developer/chapter10/step1.zip) .

### 创建 Truffle 开发网络

下一步是替换 truffle/truffle-config.js 文件，用以下配置：module.exports = {  networks: {    development: {      host: "127.0.0.1",      port: 8545,      network_id: "*",      gas: 5000000,      gasPrice: 100000000000    }  }};

注意你指向了端口 8545，这将在本章稍后当你运行 MetaMask 时帮助你。

### 部署智能合同

你需要另一个配置文件，即部署合同文件。创建一个部署文件，命名为 truffle/migrations/2_deploy_contracts.js。在这个配置文件中，你只需指向你创建的 Transfer 智能合同 SOL 代码。var Transfer = artifacts.require("./Transfer.sol");module.exports = function(deployer) {  deployer.deploy(Transfer);};现在你准备好使用 Ganache 在端口 8545 上创建你的网络，所以请导航到 Truffle 项目，并运行此命令：> cd ethdapp/truffle> ganache-cli -p 8545

### 提示

如果你遇到任何错误，例如“NODE_MODULE_VERSION 不匹配”，请卸载并重新安装 ganache-cli。然后打开一个新的终端窗口，确保它正在正确运行。

如果需要重新安装 ganache-cli，请运行此命令：> npm uninstall -g ganache-cli> npm install -g ganache-cli 为确保其正确运行，请运行此命令：> ganache-cli help 接下来，在另一个终端窗口中，当 ganache 仍在运行时，让我们编译并部署你的合同。> truffle compile 编译输出应该提供成功，在 Contract 文件夹中创建你的合同。编译./contracts/Transfer.sol...将工件写入./build/contracts 创建的文件是 Transfer.json，你将在 dapp 中使用它来与网络交互。接下来，你将使用 migrate 命令部署你的合同。> truffle migrate --network development 输出应确认合同已迁移到网络，如图 10-3 所示。![../images/475651_1_En_10_Chapter/475651_1_En_10_Fig3_HTML.jpg](img/475651_1_En_10_Fig3_HTML.jpg)

图 10-3

Truffle 迁移项目

输出摘要还应显示部署顺利进行并且有收费。摘要=======> 总部署：      2> 最终费用：          0.0525573 ETH

#### Truffle 控制台

现在你已经将合同编译并部署，要与网络交互，请启动一个控制台，如下所示：> truffle console --network development

你可以针对 Truffle CLI 运行的命令的好资源是在 Ethereum JavaScript API 维基页面 here: [`github.com/ethereum/wiki/wiki/JavaScript-API`](https://github.com/ethereum/wiki/wiki/JavaScript-API) .

#### 账户

如果你运行 getAccounts，你会得到与你钱包关联的账户列表。truffle(development)> web3.eth.getAccounts()[ '0x1eFf25A40C82EA65BC88E45d02368897EC922FEf', '0xC135058b33d5df78636Cf14b74F281f95c4a407c', '0xe682300Ef633F7d4f0d8Cb07c1bAD5d9B4eaE974'...]。然后你可以定义 address1 和 address2 为第一个和第二个账户。truffle(development)> web3.eth.getAccounts().then(function(a){address1=a[0]})undefinedtruffle(development)> web3.eth.getAccounts().then(function(a){address2=a[1]})undefined 现在它们已经被定义了，你可以在输出中调用它们并获取第一个和第二个账户。truffle(development)> address1'0x1eFf25A40C82EA65BC88E45d02368897EC922FEf'truffle(development)> address2'0xC135058b33d5df78636Cf14b74F281f95c4a407c'你也可以使用 getBalance 获取这些地址的余额。truffle(development)> web3.eth.getBalance(address1)'99942134400000000000'truffle(development)> web3.eth.getBalance(address2)'100000000000000000000'

#### 测试智能合约的转移

既然你已经定义了两个地址并知道这些账户的余额，你可以定义你的合约并在账户之间转移一些资金。为此，首先定义合约并将其称为 transferSmartContract。truffle(development)> Transfer.deployed().then(function(instance){transferSmartContract = instance;})undefined 接下来，运行你定义的 transferSmartContract 变量以确保它工作正常并显示对象值。> transferSmartContract 现在你可以用你的智能合约在两个账户之间转移资金。账户 2 有一个很圆润的数字，所以你会转移 5 eth。> transferSmartContract.pay(address2, {from: address1, value: 5});命令输出显示有关交易和采矿的信息。现在你能够看到余额更新了。> web3.eth.getBalance(address1);'99942134399999999995'> web3.eth.getBalance(address2);'100000000000000000005'

正如你所看到的，余额发生了变化，你能够在两个地址之间转移代币。

## 与以太坊网络的链接

你已经在终端中让你的合约运行；下一步是你 的 dapp 与合约交互。这是通过 web3.js 完成的，web3.js 是一组库，允许你使用 HTTP 或 IPC 连接与本地或远程以太坊节点交互。首先回到你的 Angular 项目文件夹，然后使用--save 标志安装 web3.js 以保存你安装的库。> cd ethdapp/> npm install web3 –save+ web3@1.0.0-beta.55

如果安装成功，你将在输出中看到版本确实已经安装。在撰写本文时，web3 版本为 1.0.0-beta55。

你还需要安装 truffle-contract，它提供了封装代码，使与你的合约交互变得更容易。在撰写本文时，最新版本是 4.0.7，但到你读到这本书时可能已经变了。> npm install truffle-contract –save+ truffle-contract@4.0.15

### 提示

web3 版本 1.0.0 测试版和 truffle-contract 版本 4.0.15 是最新版本，与 Angular 7.3.x 兼容。然而，这可能会发生变化，所以要注意你正在安装的版本，以确保其兼容并避免错误。如果你遇到兼容性问题，可以重新安装确切的@[版本]，例如@4.0.15。

### 转账服务

现在你已经安装了你的库，你可以继续操作。在本节中，你将创建并编写一个服务类。服务类将作为你前端的中间层与 web3 进行交互。开始时，你可以使用 ng s 标志，它代表“服务”。

注意你将代码包裹在 console.log 信息中，这样你可以在开发者工具模式下的浏览器控制台消息部分看到这些信息，以帮助你理解正在发生的事情。为此，请以开发者工具模式打开浏览器。对于 Chrome，选择查看开发者视图➤开发者➤开发者工具。

你需要一个异步方法来获取账户地址和余额，所以你可以使用一个承诺函数。如果你之前没有检索到账户，你将像在终端中一样调用 web3.eth.getAccounts 来获取数据。如果你遇到问题，你还需要错误代码。private async getAccount(): Promise<any> {    console.log('transfer.service :: getAccount :: start');    if (this._account == null) {        this._account = await new Promise((resolve, reject) => {            console.log('transfer.service :: getAccount :: eth');            console.log(window.web3.eth);            window.web3.eth.getAccounts((err, retAccount) => {                console.log('transfer.service :: getAccount: retAccount');                console.log(retAccount);                if (retAccount.length > 0) {                    this._account = retAccount[0];                    resolve(this._account);                } else {                    alert('transfer.service :: getAccount :: no accounts found.');                    reject('No accounts found.');                }                if (err != null) {                    alert('transfer.service :: getAccount :: error retrieving account');                    reject('Error retrieving account');                }            });        }) as Promise<any>;    }    return Promise.resolve(this._account);  }同样，你需要一个服务方法来与账户交互并获取其余额。你像在终端中一样调用 web3.eth.getBalance，并包裹一些错误检查。你还将此设置为一个承诺。你需要承诺的原因是这些调用是异步的，而 JavaScript 不是。  public async getUserBalance(): Promise<any> {    const account = await this.getAccount();    console.log('transfer.service :: getUserBalance :: account');    console.log(account);    return new Promise((resolve, reject) => {        window.web3.eth.getBalance(account, function(err, balance) {            console.log('transfer.service :: getUserBalance :: getBalance');            console.log(balance);            if (!err) {                const retVal = {account: account, balance: balance};                console.log('transfer.service :: getUserBalance :: getBalance :: retVal');                console.log(retVal);                resolve(retVal);            } else {                reject({account: 'error', balance: 0});            }        });    }) as Promise<any>;  }最后，你需要一个方法来传递表单中的值并将支付从一个账户转移到另一个账户。使用合约支付方法，并包裹一些错误检查。  transferEther(value) {    const that = this;    console.log('transfer.service :: transferEther to: ' + value.transferAddress + ', from: ' + that._account + ', amount: ' + value.amount);    return new Promise((resolve, reject) => {        console.log('transfer.service :: transferEther :: tokenAbi');        console.log(tokenAbi);        const transferContract = TruffleContract(tokenAbi);        transferContract.setProvider(that._web3);        console.log('transfer.service :: transferEther :: transferContract');        console.log(transferContract);        transferContract.deployed().then(function(instance) {            return instance.pay(            value.transferAddress,            {                from: that._account,                value: value.amount            });        }).then(function(status) {            if (status) {                return resolve({status: true});            }        }).catch(function(error) {            console.log(error);            return reject('transfer.service error');        });    });  }}

既然你已经完成了转账服务，那么你可以连接转账.组件以获取用户的账户地址和余额，在表单填写完成后就可以进行资金转账了。

首先，你需要定义你创建的服务组件。打开`src/app/component/transfer/transfer.component.ts`文件，在文档顶部添加导入声明。```typescript

你可以从这里下载完整的步骤：[`github.com/Apress/the-blockchain-developer/chapter10/step2.zip`](https://github.com/Apress/the-blockchain-developer/chapter10/step2.zip) 。

## 连接到 MetaMask

至此，你的 dapp 代码已经完成。然而，如果你现在测试你的 dapp，web3 将无法连接到一个账户。你需要做的是连接到 MetaMask。与 dapps 相关的隐私问题是，恶意网站能够注入代码来查看用户的活动和以太坊地址，然后找到余额、交易历史和个人信息。

这些恶意网站随后能够代表用户发起不受欢迎的交易，而用户可能不小心批准了未经授权的交易并损失了资金。

为了避免这些问题并连接你的 Angular 服务，你将通过 MetaMask 将浏览器连接到网络。

你已经使用了 MetaMask，所以你应该已经安装了它。

让我们退一步。正如你所回忆的，你通过 ganache-cli 在 8545 端口上启动了一个网络。```bash

然后你能够在 8545 端口上连接，并在终端中运行命令。

你现在可以在浏览器中连接 MetaMask。要连接，选择 MetaMask 并在下拉菜单中选择 Localhost 8545。见图 10-4。![../images/475651_1_En_10_Chapter/475651_1_En_10_Fig4_HTML.jpg](img/475651_1_En_10_Fig4_HTML.jpg)

图 10-4

将 MetaMask 连接到端口 8545 的私有网络

注意你在本章中选择的端口 8545。这是 MetaMask 的默认端口，因此通过选择下拉菜单项而不是指向自定义端口，很容易连接到你的私有网络。

然而，当你检查账户列表时，你不会看到任何账户。你看不到账户的原因是，每次你启动你的网络，你都需要更新账户。有两种方法可以更新 MetaMask 账户列表。

*选项 1*：当你运行 Ganache 时，使用 m 标志来传递代表你在 Ganache 中的私钥的助记词。例如，命令将像这样：`ganache-cli -p 8545 -m 'journey badge medal slender behind junk develop produce spy enemy transfer room'`*选项 2*：当你运行 ganache-cli 时，你会看到账户、私钥和助记词的列表。`ganache-cli -p 8545`寻找这个输出并复制助记词。HD 钱包==================助记词：journey badge medal slender behind junk develop produce spy enemy transfer room 基础 HD 路径：`m/44'/60'/0'/0/{account_index}`然后，退出 MetaMask 并手动粘贴助记词。点击右边的按钮，选择“登出”，如图 10-5 所示。![../images/475651_1_En_10_Chapter/475651_1_En_10_Fig5_HTML.jpg](img/475651_1_En_10_Fig5_HTML.jpg)

图 10-5

MetaMask 登出账户

登出后，欢迎屏幕再次出现，下面有一个链接，写着“使用账户种子短语导入”。点击那个链接，如图 10-6 所示。![../images/475651_1_En_10_Chapter/475651_1_En_10_Fig6_HTML.jpg](img/475651_1_En_10_Fig7_HTML.jpg)

图 10-7

使用助记词恢复 MetaMask 账户

## 测试你的 Dapp 功能

现在你终于可以测试你的 Dapp 了。一旦浏览器刷新，你将看到地址和余额。

接下来，填写表格并初始化转账。注意 MetaMask 会打开以确认转账。这是一种额外的安全措施，以确保只有得到授权的转账才会被批准。

参见图[10-8]。![../images/475651_1_En_10_Chapter/475651_1_En_10_Fig8_HTML.jpg](img/475651_1_En_10_Fig8_HTML.jpg)

图 10-8

MetaMask 通知完成转账

## 从这里出发去哪里

继续创建 Dapp 的工作并改进。例如，你可以做以下事情：

+   创建一个用户服务类和一个共享服务类来保存用户的信息和共享信息

+   创建一个登录/登出服务

+   创建一个切换账户的选项

+   创建一个侧边菜单以便更好地导航应用

+   更新智能合约并且添加更多的方法和事件

## 总结

在这一章，你创建了一个转账智能合约以及 Truffle 开发项目并且连接到了 Ganache 本地开发网络。你学习了如何通过 Truffle 与以太坊网络交互以及如何测试你的智能合约。你通过命令行使用你的智能合约进行了资金转移的测试。

最后，你使用你创建的 Angular TransferService 组件将你的 dapp 与以太坊网络链接起来。运用 web3 库，你进行了某些服务调用。最后，你连接到 MetaMask 以管理你的账户。

在下一章，你将学习关于区块链安全和合规性。
