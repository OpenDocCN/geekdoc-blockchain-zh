© 作者，独家许可 APress Media，LLC，Springer Nature 的一部分 2022 D. P. Bauer Ethereum 入门 [`doi.org/10.1007/978-1-4842-8045-4_5`](https://doi.org/10.1007/978-1-4842-8045-4_5)

# ERC-721 不可替代令牌

Davi Pedro Bauer^(1) (1) 巴西南部，格兰杜州，坎波博姆

不可替代令牌（NFT）是代表艺术品、音乐、游戏物品和视频等实物的数字资产。在本章中，我将向您展示如何创建 NFT ERC-721 并将其部署到以太坊测试网络，以及如何将其添加到您的 MetaMask 移动钱包中。

在本章结束时，您将能够执行以下操作：

+   创建一个新的 NFT 项目

+   配置网络以部署到 Ganache

+   配置私钥

+   创建徽章图像

+   将徽章添加到本地 IPFS

+   将徽章固定到远程 IPFS

+   创建徽章元数据

+   部署智能合约

+   将徽章授予您的钱包

+   在 Etherscan 上检查徽章

+   将徽章添加到您的移动钱包

## 使用 Ganache 和 OpenZeppelin 创建您的艺术 NFT

让我们使用 OpenZeppelin 库配置您的第一个 NFT，并创建将存储令牌信息的元数据，然后将其部署到测试网络。最后，您将在您的钱包中查看令牌。

### 创建项目

使用 Truffle 创建一个新项目。$ truffle init 安装 OpenZeppelin 合约。$ npm install @openzeppelin/contracts 创建一个新的 Solidity 智能合约。$ touch contracts/UniqueAsset.sol

打开 UniqueAsset.sol 文件并导入 ERC721URIStorage.sol 扩展和 Counters.sol 实用程序。创建一个扩展 ERC721URIStorage 的新类。声明计数器变量并声明传递币名称和代码的构造函数。

创建一个名为 awardItem 的新方法。在新方法内部，增加令牌 ID。使用 _tokenIds.current() 获取新的令牌编号。

使用方法 _mint 铸造新物品。最后，通过使用方法 _setTokenURI 传递元数据来设置令牌 URI。// SPDX-License-Identifier: MITpragma solidity ⁰.8.0;import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";import "@openzeppelin/contracts/utils/Counters.sol";contract UniqueAsset is ERC721URIStorage {    using Counters for Counters.Counter;    Counters.Counter private _tokenIds;    constructor() ERC721("UniqueAsset", "UNA") {}    function awardItem(address recipient, string memory metadata)    public    returns (uint256)    {        _tokenIds.increment();        uint256 newItemId = _tokenIds.current();        _mint(recipient, newItemId);        _setTokenURI(newItemId, metadata);        return newItemId;    }}使用 touch 命令创建一个新的迁移文件。该命令在迁移文件夹中创建一个新文件。$ touch migrations/2_deploy_contracts.sol 在 2_deploy_contracts.js 文件中，导出迁移文件中的智能合约。const UniqueAsset = artifacts.require("UniqueAsset");module.exports = function (deployer) {    deployer.deploy(UniqueAsset);}

### 配置钱包以签署交易

安装文件系统 fs 包。$ npm install fs 安装钱包提供程序 hdwallet 包。$ npm install @truffle/hdwallet-provider@1.2.3 打开 truffle-config.js 文件并取消注释 HDWalletProvider 代码部分。const HDWalletProvider = require('@truffle/hdwallet-provider');const infuraKey = '<your_infura_key>';const fs = require('fs');const mnemonic = fs.readFileSync(".secret").toString().trim();

将您的 Infura 项目 ID 粘贴为变量 infuraKey 的值。

### 配置网络

在 truffle-config.js 文件中取消注释 ropsten 网络部分，并进行以下更改：

+   将 ropsten 更改为 rinkeby。

+   将 Ropsten Infura URL 更改为 rinkeby。

+   将 YOU-PROJECT-ID 更改为 ${infuraKey}。

+   将 network_id 更改为 42。

rinkeby: {    provider: () => new HDWalletProvider(mnemonic, `https://rinkeby.infura.io/v3/${infuraKey}`),    network_id: 42,    gas: 5500000,    confirmations: 2,    timeoutBlocks: 200,    skipDryRun: true},

### 配置 Solidity 编译器

还要在 truffle-config.js 文件内部取消注释编译器部分，并将版本更改为 0.8.0*.*编译器: {    solc: {        version: "0.8.0",        docker: true,        settings: {            optimizer: {                enabled: false,                runs: 200            },            evmVersion: "byzantium"        }    }},

### 配置私钥

打开浏览器并打开连接到 Infura 网络的 MetaMask 钱包。点击“*您的账户*”，然后点击“设置”。最后，点击“安全性与隐私”（见图 5-1）。

您可以选择查看您的种子短语，但请注意，此信息是敏感的，如果有人可以访问它，他们将能够恢复您的钱包并使用您的资金！[](../images/521550_1_En_5_Chapter/521550_1_En_5_Fig1_HTML.jpg)

在 Ropsten 测试网络的安全性与隐私窗口的截图。屏幕上有一个短语写着“显示种子短语”。屏幕底部有一个带有光标的按钮，上面也写着“显示种子短语”。

图 5-1

MetaMask：显示种子短语

单击“显示种子短语”并输入您的钱包密码以继续。复制私钥。

返回到 Visual Studio Code 并创建一个名为 .secret 的新文件。将私人秘密恢复短语粘贴到此文件中。

### 创建徽章图像

创建徽章文件夹。$ mkdir 徽章现在，转到徽章根目录。$ cd 徽章从互联网上下载您要用作徽章的图像。您还可以将现有图像复制并粘贴到此文件夹中。curl 命令用于通过 URL 语法传输数据。$ curl https://planouhost.z15.web.core.windows.net/badge.png > 徽章图像.png

### 将徽章添加到您的本地 IPFS

初始化您的本地 IPFS 节点。此命令将在 127.0.0.1:5001 上启动一个 IPFS 本地服务器。$ ipfs daemon 将您的徽章图像添加到 IPFS。$ ipfs add badge-image.png 运行此命令，您将收到一个哈希。此哈希是您在 IPFS 中的图像地址。确保您看到与图 5-2 中显示的输出相同。![](img/521550_1_En_5_Fig2_HTML.jpg)

添加文件后的 IPFS 输出的截图。它显示：dollar, i p f s add badge-image dot p n g。接下来的几行呈现了文件的更多细节，包括文件大小和进度条。

图 5-2

添加文件后的 IPFS 输出

### 固定徽章到远程 IPFS 节点

使用 Pinata 作为远程 IPFS 服务固定您的徽章。ipfs pin remote add --service=pinata --name=badge-image.png QmZPxKJWqJTdudyaZUyf6uBzwwAT41QQyxhTHmMZWB9yx4 您将收到一个指示文件成功固定的响应。CID: QmZPxKJWqJTdudyaZUyf6uBzwwAT41QQyxhTHmMZWB9yx4Name: badge-image.pngStatus: pinned

### 创建徽章元数据

创建徽章元数据 JSON 文件。创建 badge-metadata.json 文件。打开文件 badge-metadata.json，并设置徽章名称、描述和图像地址。对于最后一个，您可以使用 IPFS 网关来显示图像，以便在支持此徽章类型的任何钱包上显示图像；否则，您将依赖于目标钱包支持直接从 IPFS 哈希显示图像。{    "name": "我的徽章",    "description": "我的徽章描述",    "image": "https://ipfs.io/ipfs/QmZPxKJWqJTdudyaZUyf6uBzwwAT41QQyxhTHmMZWB9yx4"}将您的徽章元数据添加到 IPFS。$ ipfs add badge-metadata.json 使用远程 IPFS 服务固定您的徽章元数据。$ ipfs pin remote add --service=pinata --name=badge-metadata.json QmRzcwAtLWbeYqyaZUyf6uBzwwAT41QQyxhTHmMZWBfUTa

### 编译智能合约

使用 Truffle 编译合约。$ truffle compile

### 迁移智能合约

使用 Truffle 将合约迁移到 Rinkeby 网络。$ truffle migrate --network rinkeby

### 实例化智能合约

使用 Truffle 控制台实例化合约。$ truffle console --network rinkeby 获取部署的合约实例。truffle（rinkeby）让实例 = await UniqueAsset.deployed()

### 给钱包颁发徽章

调用 awardItem 方法，并将以太坊地址作为第一个参数传递，并将徽章元数据的 IPFS 地址作为第二个参数。确保 IPFS 地址对应您的徽章元数据。truffle（rinkeby）让结果 = await instance.awardItem("0x62761466bB3A3Da83B408B5F5fE00ac7b2a5A996","https://ipfs.io/ipfs/QmRzcwAtLWBeYqUx3ba1BkYKubSDLNTHCuiUB7WAmdfUTa")

### 在 Etherscan 上检查徽章

一旦您的合约部署完成，您将能够看到您的合约的公共地址。在终端中找到创建的合约地址并复制它。

转到 [`rinkeby.etherscan.io`](https://rinkeby.etherscan.io)，并将合约地址粘贴到搜索栏中（图 5-3）。您可以使用 Rinkeby Testnet Explorer 工具查看创建的智能合约的详细信息。![](img/521550_1_En_5_Fig3_HTML.jpg)

Rinkeby Testnet Explorer 的屏幕截图。顶部是 Rinkeby Testnet Explorer 的标题。在标题下方是一个标有所有过滤器的下拉选项，以及带有随机字母数字地址的输入栏。

图 5-3

Rinkeby Testnet Explorer：搜索智能合约

点击搜索图标。现在您可以看到合约已成功部署（图 5-4）。在此详细信息页面上，您可以查看诸如交易之类的数据。![](img/521550_1_En_5_Fig4_HTML.jpg)

一个名为 contract 的页面的截图。左上角和右上角分别标有合同概述和更多信息。底部有 3 个选项，标有交易、合同和事件，其中第一个选项卡交易被选中。

图 5-4

Rinkeby Testnet Explorer：查看智能合约交易

您还可以意识到最后一笔交易是为授予新项目而进行的。

### 将 NFT 代币添加到您的钱包。

在您的手机上打开 MetaMask 钱包并点击“收藏品”（图 5-5）。请注意，收藏品仅在移动版本上可用！[](../images/521550_1_En_5_Chapter/521550_1_En_5_Fig5_HTML.jpg)

Metamask 钱包的截图。顶部是标题钱包，Rinkeby 测试网络。标题下方是账户 2，金额为 8548.21009 美元，0 x 6276 椭圆形 A 996。底部有接收、发送和交换选项。

图 5-5

MetaMask：收藏品选项卡

点击“添加收藏品”。粘贴令牌合约地址（与上一节中复制的相同）并输入令牌 ID（因为这是您将输入的第一个令牌，因此在这里输入 1）。

点击“添加”并等待几秒钟（图 5-6）。NFT 代币已添加！！[](../images/521550_1_En_5_Chapter/521550_1_En_5_Fig6_HTML.jpg)

Metamask 钱包的截图。页面标题为“钱包”，Rinkeby 测试网络。标题下方是账户 2，金额为 8548.21009 美元，0 x 6276 椭圆形 A996。接收、发送和交换选项。底部有 2 个选项卡，分别是代币和收藏品。选择了收藏品选项卡，一个名为 0 U N A 的唯一资产位于选项卡下方。

图 5-6

MetaMask：添加智能合约后，它将出现在这里

点击“UniqueAsset”。现在您将能够看到您赚取的所有徽章（图 5-7）。您可以拥有多个源自同一智能合约的令牌，每个令牌都将通过唯一标识符加以区分！[](../images/521550_1_En_5_Chapter/521550_1_En_5_Fig7_HTML.jpg)

Metamask 唯一资产的截图。页面标题为“唯一资产”，Rinkeby 测试网络。标题下方是一个标有 1 个唯一资产的图标，以及发送、添加和信息选项。底部是一个标有“我的徽章”的图标，带有一个可选择的选项。

图 5-7

MetaMask：徽章列表

点击“我的徽章”。现在您可以看到徽章的详细信息！此外，您有一个发送按钮，可以将徽章发送到另一个钱包（图 5-8）。![](img/521550_1_En_5_Fig8_HTML.jpg)

MetaMask 独特资产的屏幕截图。页面标题为独特资产，Rinkeby 测试网络。标题下方是一个标有 M E S T R E 的徽章。文本是我的徽章标签 1，并且底部有一个发送按钮。

图 5-8

MetaMask：徽章显示

就这样！您刚刚创建了您的第一个 NFT 代币！

## 在 OpenSea 上销售您的艺术 NFT

OpenSea 是一个数字商品市场，例如收藏品、游戏道具、数字艺术以及其他基于区块链（如以太坊）支持的数字资产。您可以在 OpenSea 上与全球任何人购买、出售和交易这些物品。

### 连接到 OpenSea

前往 OpenSea^(1)，确保您连接到包含 NFT 的钱包，并且您正在使用 Rinkeby 测试网络。

### 查看您的徽章

转到我的个人资料。点击活动，然后点击徽章标题。这些是您的徽章详情。详情页面允许您查看关于徽章交易的各种信息。

### 上架您的徽章出售

点击出售，然后点击设置价格。在价格中，设置您希望出售 NFT 的价格。在此页面上，您可以设置徽章的定价方式，并安排将其列出在未来的日期（图 5-9）。![](img/521550_1_En_5_Fig9_HTML.jpg)

我的徽章独特资产的屏幕截图。它有三种选择以选择您的销售方式，它们是设置价格、最高出价和捆绑包。它们下面是一个价格输入选项。包括最终价格、未来时间安排和隐私选项均为切换选项。

图 5-9

OpenSea：徽章定价页面

点击发布您的列表。您将被重定向到摘要页面（图 5-10）。在此页面上，您可以看到出售您的徽章时将被扣除的总费用。![](img/521550_1_En_5_Fig10_HTML.jpg)

摘要页面的屏幕截图。有 3 个部分，列出、悬赏和费用。列出有一个可选择的选项来发布你的列表。悬赏和费用有关于合作伙伴的说明和细节。在悬赏旁边有一个编辑按钮，而在费用下有一个了解更多的链接。

图 5-10

OpenSea：徽章的摘要页面

MetaMask 将打开以验证交易（图 5-11）。点击确认。在这一步中，您需要批准将确认您的徽章在平台上出售的交易。![](img/521550_1_En_5_Fig11_HTML.jpg)

MetaMask 通知窗口的屏幕截图。顶部是 Rinkeby 测试网络，账户 1 向右箭头 0 x 3301 省略号 f 83 A。它们下面是一个链接和一个设置全部批准的按钮。2 个选项卡详情和数据，其中数据被选中并显示燃气费和总费用。底部是拒绝和确认按钮。

图 5-11

MetaMask：确认 OpenSea 交易

现在您需要提供更多关于您的信息，比如您的邮箱和昵称。在交易获得批准后，您将被要求提供额外的信息（图 5-12）。![](img/521550_1_En_5_Fig12_HTML.jpg)

一个名为“列表成功”的窗口的屏幕截图。截图包含了邮箱星号和昵称星号的输入选项，选中了“发送关于 Opensea 的偶尔更新”选项，并在左下角有一个保存按钮。

图 5-12

OpenSea：附加信息

点击保存。现在，OpenSea 将为您列出您的 NFT！

### 探索列表详情

滚动到交易历史（图 5-13）；如你所见，创建了一个名为列表的新事件，并将价格设定为 US 10\. 在此页面上，你可以看到平台上所有徽章的交易历史。![](img/521550_1_En_5_Fig13_HTML.jpg)

交易历史页面的截图。顶部有一个名为筛选器的选项。底部有名为事件、价格、来自和到的列。在事件下，有三个标题，即列表、转移和创建。

图 5-13

OpenSea：交易历史

点击分享图标。你可以复制链接或在社交网络上分享。

## 总结

在本章中，你学会了如何在 ERC-721 标准中创建代币，在 IPFS 中固定图像，并在 OpenSea 中导入并将其出售。

在下一章中，我们将了解如何使用水龙头以及它们在测试网络中的重要性。
