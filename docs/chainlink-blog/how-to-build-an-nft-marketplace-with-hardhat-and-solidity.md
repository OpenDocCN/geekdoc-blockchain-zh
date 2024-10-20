# 如何建立一个稳健的 NFT 市场

> 原文：<https://blog.chain.link/how-to-build-an-nft-marketplace-with-hardhat-and-solidity/>

[不可替代代币](https://chain.link/education/nfts) (NFTs)抓住了 [Web3](https://chain.link/education/web3) 社区的想象力。虽然最强大的 NFT 用例可能还没有出现，但这项技术已经在改变数字所有权、身份、创意表达和社区成员。

因为 NFT 是可以买卖或交易的数字资产，NFT 市场在保存库存和连接买家和卖家方面发挥着重要作用。

在这篇博客中，我们将使用 Solidity 构建一个 NFT 市场的“后端”。我们将逐步完成构建智能合同的过程，这些合同包含我们 NFT 市场的业务逻辑。在实践中，这意味着创建一个单独的 `NftMarketplace.sol` 智能合约和一个样本 [ERC721 兼容令牌](https://eips.ethereum.org/EIPS/eip-721)【NFT】合约，我们可以使用它在我们的市场上列出。

这个博客是为那些有一些编程经验的人设计的。如果你对基本的 JavaScript 很熟悉，你将能够理解。熟悉一些常见的以太坊术语也会有所帮助，你可以通过浏览 [这个术语表](https://ethereum.org/en/glossary/) 来温习一下。

市场将有以下基本操作:

*   列举 NFT。
*   更新和取消列表。
*   购买 NFT(转让所有权)。
*   获取列表。
*   获得卖家的收益。

这些操作将在市场智能合同上实施。建议您花点时间理解上面的操作，因为它们的编码逻辑自然来自对每个操作的输入和输出的分析。

例如，我们需要什么数据才能将 NFT 上市？我们肯定需要令牌 ID。由于这是一个可以列出多个不相关的 NFT 的市场，我们还需要每个 NFT“家族”的合同地址。此外，由于我们列出了待售的 NFT，我们还需要能够添加每个令牌的价格。

我们将很快更深入地定义我们的函数签名，但是首先让我们建立我们的项目和环境。

如果您想查看该项目的参考回购，您可以在这里 找到 [。它比我们将在这里讨论的内容更深入，所以如果您想更深入地研究这个项目，它是很有用的。](https://github.com/PatrickAlphaC/hardhat-nft-marketplace-fcc#hardhat-nextjs-nft-marketplace.)

## 项目设置

我们将使用 yarn，所以在您的机器上运行 `npm install -g yarn` 来全局安装它。你还需要确保你的机器上也有 [nodeJS 运行时](https://nodejs.org/en/) ，所以通过运行 `node –version` 来检查你已经安装了它。

我们将使用 [Hardhat](http://hardhat.org) 以太坊开发环境来编译、部署、测试我们的智能合约并与之交互，因此请花点时间通读 Hardhat [入门指南](https://hardhat.org/getting-started/) 。

我们将在路径中引用您的项目目录为 `<<root>>` ，因此打开终端应用程序并将 `cd` 放入您的根目录，然后打开您的 IDE(您可以使用任何您熟悉的支持 Javascript 的 IDE)。在项目目录下创建一个 `package.json` 文件，将 [中的内容粘贴到](https://github.com/PatrickAlphaC/hardhat-nft-marketplace-fcc/blob/main/package.json) 中。你会看到它包含了[NPM](https://en.wikipedia.org/wiki/Npm_(software)#:~:text=npm%20(originally%20short%20for%20Node,js.)依赖包，包括那些在 Hardhat 的入门指南中提到的。然后运行 `yarn install` 安装所有的项目依赖项。安装完成后，你应该会在你的项目根目录下看到一个 `node_modules` 文件夹。这包含了你所有的依赖，包括 Hardhat。

在本教程中，我们将在哈德哈特的本地区块链网络上进行开发，这意味着我们不会与测试网或以太坊主网进行交互。当你准备在像 Rinkeby 这样的测试网上测试时，请按照 [回购的自述](https://github.com/PatrickAlphaC/hardhat-nft-marketplace-fcc#deployment-to-a-testnet-or-mainnet) 中的这些步骤。

在你的项目根目录下，运行 `/<<root>> yarn hardhat` 初始化 Hardhat，选择选项 4:“创建一个空的 hardhat.config.js”。

![Creating empty Hardhat config](img/3a2c4c26105c003da0aa40c390038376.png)

一旦 Hardhat 初始化完成，你的项目根目录下就会有一个空的 `hardhat.config.js` 文件。现在您有一个选择:如果您计划在一个活动的 testnet 上部署，您可以将这个内容 [粘贴到那个文件中，因为您将需要在那里声明的各种常量来指定不同 testnet 和 mainnet 网络的配置细节。请注意，要访问 testnet 或 mainnet 节点，您需要使用以太坊节点访问提供程序，如](https://github.com/PatrickAlphaC/hardhat-nft-marketplace-fcc/blob/main/hardhat.config.js)[in fura](http://infura.io)，[Alchemy](http://alchemy.io)， 或[Moralis](http://moralis.io)。我们在这个博客中不需要它们，但是当你决定在外部测试网上测试或者在 mainnet 上部署到生产环境时，它们是必要的。

或者，如果你只是想关注这个博客，你可以复制并粘贴下面的配置代码片段。我们将把这个文件称为“安全帽配置”，对于本教程来说，重要的部分是导出的对象( `module.exports = {defaultNetwork: {...} }` )。这是保存我们的项目配置的对象，它定义了我们的默认、hardhat 和 localhost 网络。

为了本文和本博客的目的，您导出的配置对象可以看起来像这个最小配置，所以您可以用这个替换链接文件中的导出对象:

```
require("@nomiclabs/hardhat-waffle");
require("@nomiclabs/hardhat-etherscan");
require("hardhat-deploy");
require("solidity-coverage");
require("hardhat-contract-sizer");
require("dotenv").config();

module.exports = {
defaultNetwork: "hardhat",
 networks: {
 hardhat: {
chainId: 31337,
    },

 localhost: {
chainId: 31337,
 },
 },
 namedAccounts: {
 deployer: {
      default: 0, // here this will by default take the first account as deployer
      1: 0, // similarly on mainnet (network 1) it will take the first
account as deployer. Note though that depending on how hardhat network are 
configured, the account 0 on one network can be different than on another
 },
 },
 solidity: {
 compilers: [
 {
version: "0.8.7",
 },
 {
version: "0.4.24",
 },
 ],
 },
 mocha: {
timeout: 200000, // 200 seconds max for running tests
 },
};
```

我们的项目将有以下文件夹:

*   一个 `contracts` 文件夹。这是我们 NFT 市场的逻辑，也是 NFT 合同的样本。
*   一个 `deploy` 文件夹。这与 hardhat-deploy 插件一起使用，并包含我们的部署脚本，这些脚本将把编译好的智能合同部署到 hardhat 提供的本地开发区块链。
*   一个 `scripts` 文件夹。它保存了我们用来与我们的 Hardhat 开发区块链本地部署的合同进行交互的脚本。

让我们开始建设我们的市场吧。

## 建设 NFT 市场

在你的项目根目录下，新建一个 `contracts` 文件夹。在那个文件夹里面，创建 `NftMarketplace.sol` `file (your file path will look like `../<< root >>/contracts/NftMarketplace.sol` )。`

 `现在让我们考虑一下在 `NftMarketplace` 智能契约中我们需要的方法签名，用于我们上面讨论的各种操作。它们看起来会像这样:

```
function listItem(
 address nftAddress,
 uint256 tokenId,
 uint256 price
    ) {} 

function cancelListing(address nftAddress, uint256 tokenId){} 

function buyItem(address nftAddress, uint256 tokenId){}

function updateListing(
 address nftAddress,
 uint256 tokenId,
 uint256 newPrice
 ){}
function withdrawProceeds(){} // method caller should be withdrawer

function getListing(address nftAddress, uint256 tokenId){}
```

虽然这看起来很简单，但是构建智能合同需要很多仔细的思考、检查和克服限制。所以我们再深入一点。我们还想防止[重入攻击](https://blog.openzeppelin.com/reentrancy-after-istanbul/)，这种攻击利用以太坊智能合约的工作方式来重复运行不受欢迎的代码执行——通常是转移令牌所有权的代码。优秀的智能合约开发人员必须熟悉这些潜在的漏洞。

在实现市场逻辑时，我们将使用以下字段和数据结构:

*   一个 `Listing` struct 带 price 和 seller 属性变量。
*   三个 [事件](https://docs.soliditylang.org/en/v0.8.13/contracts.html#events)——`ItemListed`、 `ItemCanceled` 和 `ItemBought`。
*   两个映射——`s_listings`和 `s_proceeds` ，分别是存储在区块链上的 [状态变量](https://docs.soliditylang.org/en/v0.8.13/contracts.html#events) 。
*   三个 [功能修饰符](https://docs.soliditylang.org/en/v0.8.13/contracts.html#function-modifiers) 。

不要担心——随着我们继续构建我们的智能合同，你会理解其中的每一部分。

让我们从声明智能合约开始。

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

import "@openzeppelin/contracts/token/ERC721/IERC721.sol";
import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

contract NftMarketplace is ReentrancyGuard {
// TODO…
}
```

您将看到我们正在从[open zeppelin](https://openzeppelin.com/contracts/)导入两个文件，这两个文件提供了可重用的开源、经审计且安全的智能合同模板。我们的智能契约继承了它的 `ReentrancyGuard` 智能契约( [参见 Github](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/security/ReentrancyGuard.sol) )，它提供了我们可以使用的非常有价值的保护、修饰符和方法。我们还必须导入`IERC721.sol`文件，我们很快就会用到这个接口。但是，我们的市场智能合约没有实现 ERC721 令牌标准，因为它不是令牌合约。

### 实施`listItem()`

让我们从 `listItem()` 方法开始，这是你已经熟悉的签名。我们将使它成为一个 外部 函数，因为它需要被其他契约或最终用户帐户调用(例如，从前端 web 应用程序)。我们还希望 listItem() 执行以下操作:

*   确保正在列出的项目尚未列出。我们用一个 [实度函数修改器](https://docs.soliditylang.org/en/v0.8.13/contracts.html#function-modifiers) 来做到这一点。
*   确保列出该项目的人(即调用此方法的人)是所有者。
*   确保代币的合同已经“批准”我们的 NFT 市场运营代币(转让代币等)。).
*   检查价格是否大于零魏。
*   发出一个列表事件。
*   将列表详细信息存储在智能合同的状态中(即市场应用程序的状态)。

现在让我们在市场契约中编写这个方法。

```
function listItem(
 address nftAddress,
 uint256 tokenId,
 uint256 price
 )
 external
 notListed(nftAddress, tokenId, msg.sender)
 isOwner(nftAddress, tokenId, msg.sender)
 {
 if (price <= 0) {
 revert PriceMustBeAboveZero();
 }
 IERC721 nft = IERC721(nftAddress);
 if (nft.getApproved(tokenId) != address(this)) {
 revert NotApprovedForMarketplace();
 }
 s_listings[nftAddress][tokenId] = Listing(price, msg.sender);
 emit ItemListed(msg.sender, nftAddress, tokenId, price);
    }
```

### 函数修饰符、事件和状态变量 

现在让我们实现 [函数修饰符](https://docs.soliditylang.org/en/v0.8.13/contracts.html#function-modifiers)[事件](https://docs.soliditylang.org/en/v0.8.13/contracts.html#events) ，以及应用 [状态变量](https://docs.soliditylang.org/en/v0.8.13/structure-of-a-contract.html#state-variables) 来保存数据。仔细看看下面的评论就知道这些棋子放在哪里了，或者参考 [参考 Github repo](https://github.com/PatrickAlphaC/hardhat-nft-marketplace-fcc/blob/main/contracts/NftMarketplace.sol) 。

```
contract NftMarketplace is ReentrancyGuard {

 struct Listing {
 uint256 price;
 address seller;
    }

 event ItemListed(
 address indexed seller,
 address indexed nftAddress,
 uint256 indexed tokenId,
 uint256 price
    );

   // State Variables
 mapping(address => mapping(uint256 => Listing)) private s_listings;
   mapping(address => uint256) private s_proceeds;

 // Function modifiers
 modifier notListed(
 address nftAddress,
 uint256 tokenId,
 address owner
 ) {
 Listing memory listing = s_listings[nftAddress][tokenId];
 if (listing.price > 0) {
 revert AlreadyListed(nftAddress, tokenId);
 }
 _;
    }

 modifier isOwner(
 address nftAddress,
 uint256 tokenId,
 address spender
 ) {
 IERC721 nft = IERC721(nftAddress);
 address owner = nft.ownerOf(tokenId);
 if (spender != owner) {
 revert NotOwner();
 }
 _;
    }

 //….. Rest of smart contract …..
}
```

你会看到:

*   `Listing`结构体只保存两条信息——卖家的以太坊账户地址和卖家代币的挂牌价格。
*   状态变量 `s_listings` 是 NFT 契约地址到自身指向 `Listing` 数据结构的令牌 id 的映射。因此，每个监听令牌 ID 都指向标识该令牌的销售者和该令牌的价格的数据。
*   状态变量 `s_proceeds` 是卖家地址和他们销售收入之间的映射。
*   `ItemListed`事件包含有用的信息——卖家的账户地址、代币 ID、代币合同地址和所列商品的价格。

我们还添加了两个函数修饰符。 `notListed` 检查令牌 ID 当前是否未列出(我们不想通过计算操作列出已经包含在 `s_listings` 中的内容)。如果有这样的清单，它会用一个 `AlreadyListed` 错误来恢复交易。我们稍后将实现这些错误。 `notListed` 也接受关于令牌的细节，然后检查该列表是否具有非零价格(如果您记得，我们的 `listItem()` 方法要求价格必须高于零)。如果条件不满足，将返回一个 `PriceMustBeAboveZero()` 错误)。

第二个修饰符是`isOwner()`修饰符，它检查调用`listItem()`的实体是否实际拥有该项。否则，对`listItem()`的调用返回`notOwner()`错误。

### 自定义错误

那么我们来谈谈这些错误。它们是可靠性 [自定义错误](https://blog.soliditylang.org/2021/04/21/custom-errors/) 我们还没有实现它们。它们实际上是在智能协定的主体之外声明的。让我们现在声明它们中的一部分，因为我们很快就会在市场函数中使用它们。请注意，我们在 import 语句之后、smart contract 声明之前声明它们。

```
import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

error PriceNotMet(address nftAddress, uint256 tokenId, uint256 price);
error ItemNotForSale(address nftAddress, uint256 tokenId);
error NotListed(address nftAddress, uint256 tokenId);
error AlreadyListed(address nftAddress, uint256 tokenId);
error NoProceeds();
error NotOwner();
error NotApprovedForMarketplace();
error PriceMustBeAboveZero();

contract NftMarketplace is ReentrancyGuard { … }
```

还要注意自定义错误可能会也可能不会接受参数。参数如果被传递，则包含关于错误的有用数据。

你会看到我们的第一个方法， `listItem()` 方法，使用了三个自定义错误:

*   `NotOwner()`错误(通过 `isOwner()` 修饰符)。
*   `PriceMustBeAboveZero()`错误。
*   `NotApprovedForMarketplace()`错误。

这些错误被“抛出”,这实际上意味着当某些检查和条件失败时，周围函数的执行被“恢复”。

### 实施`cancelListing()`
T3】

如果令牌拥有者想要将他们的令牌从列表中删除，这确实是一个不再持有处于应用状态的 `Listing` 的问题。这意味着我们必须从 `s_listings` 状态映射中删除相应的条目。所以我们把下面的方法写在 `listItem()` 之后。

```
function cancelListing(address nftAddress, uint256 tokenId)
 external
 isOwner(nftAddress, tokenId, msg.sender)
 isListed(nftAddress, tokenId)
 {
 delete (s_listings[nftAddress][tokenId]);
 emit ItemCanceled(msg.sender, nftAddress, tokenId);
    }
```

这是一个外部可调用的方法，它接受令牌的契约地址和令牌 ID 作为参数。它使用两个函数修饰符来检查调用者是否是所有者，以及令牌是否被列出(值得检查，因为我们试图删除一个条目！).我们删除列表，然后发出一个事件。

我们还没有实现 `isOwner` 修改器——我们只做了相反的检查， `isNotOwner` ！所以回到代码的修饰符部分，插入下面的修饰符:

```
modifier isListed(address nftAddress, uint256 tokenId) {
 Listing memory listing = s_listings[nftAddress][tokenId];
 if (listing.price <= 0) {
 revert NotListed(nftAddress, tokenId);
 }
 _;
    }
```

如果你研究这个，你会发现它与 `isNotListed` 的逻辑正好相反。如果该物品未列出，此修改器会恢复，而如果该物品已列出，则 `isNotListed` 会恢复。如果这令人困惑，请记住修饰符的名称——它指的是被检查的期望条件。

现在我们需要同时编写 `ItemCanceled` 事件，该事件在 `cancelListing()` 方法中发出。但是不管怎样，我们还需要一堆其他方法的事件，所以我们最好现在就实现它们，把它们去掉。

### 其他事件

如果我们看看我们的操作列表和它们的函数签名，我们知道接下来需要写 `ItemCanceled` 和 `ItemBought` 事件。

所以，在我们的 `ItemListed` 事件下我们插入:

```
event ItemCanceled(
 address indexed seller,
 address indexed nftAddress,
 uint256 indexed tokenId
    );

 event ItemBought(
 address indexed buyer,
 address indexed nftAddress,
 uint256 indexed tokenId,
 uint256 price
    );
```

你会发现唯一真正的区别是，一个指的是卖方，另一个指的是买方——很简单。

现在，让我们实施市场运营的其余部分。

### 实施`BuyItem()`

这种方法是市场的核心。它直接处理支付——意思是用 NFT 实际交换某种数字资产。在这种情况下，我们将让我们的市场接受以太支付( [【魏】](https://ethdocs.org/en/latest/ether.html#denominations) )。这也是我们需要我们之前讨论过的重入防护来防止恶意帐户耗尽所有令牌的地方。

考虑到所有这些，我们需要确保以下几点:

*   `BuyItem()`是外部可调用的，接受付款，并防止重入。
*   收到的付款不少于刊登物品的价格。
*   收到的付款被添加到卖方的收益中。
*   价值交换后清单被删除。
*   代币实际上被转让给买方。
*   发出正确的事件。

请注意，我们在这里做了一个重要的假设，即卖方没有取消批准市场作为令牌的运营商。请记住，我们在 `ListItem()` 方法中进行了批准检查，但是在列表销售之间，卖方可能已经更改了批准。

所以，考虑到以上所有因素，这个方法看起来是这样的:

```
function buyItem(address nftAddress, uint256 tokenId)
 external
 payable
 isListed(nftAddress, tokenId)
 nonReentrant
 {
 Listing memory listedItem = s_listings[nftAddress][tokenId];
 if (msg.value < listedItem.price) {
 revert PriceNotMet(nftAddress, tokenId, listedItem.price);
        }

 s_proceeds[listedItem.seller] += msg.value;
 delete (s_listings[nftAddress][tokenId]);
 IERC721(nftAddress).safeTransferFrom(listedItem.seller, msg.sender, tokenId);
 emit ItemBought(msg.sender, nftAddress, tokenId, listedItem.price);
    }
```

在上面的代码片段中，需要注意的是我们在 `s_proceeds` 中更新了卖家的余额。这存储了卖方因出售其 NFT 而收到的总乙醚量。然后，我们调用列出的令牌的契约将令牌的所有权转移给买方( `msg.sender` 是买方调用此方法)。但是我们不会把他们的收入寄给卖家。这是因为我们后来有了 `withdrawProceeds` 的方法。这种模式“拉动”而不是“推动”收益；设计背后的原理在 [这篇文章](https://fravoll.github.io/solidity-patterns/pull_over_push.html) 中有所涉及。简而言之，让卖方主动撤回资金比让我们的市场合约将资金推给他们更安全，因为推可能会导致我们的合约无法控制的执行失败。最好将转让销售收入的权力、选择和责任委托给卖方，由我们的合同单独负责存储销售收入的余额。

### 实施`updateListing()`
T3】

这个方法允许卖家更新他们列表中的价格。这简直就是一个问题:

*   检查物品是否已经列出，呼叫者是否拥有令牌。
*   检查新价格是否不为零。
*   防范再入境。
*   更新了 `s_listing` 状态映射以便正确的 `Listing` 数据对象现在指的是更新后的价格。
*   发出正确的事件。

让我们开始吧！

```
function updateListing(
 address nftAddress,
 uint256 tokenId,
 uint256 newPrice
 )
 external
 isListed(nftAddress, tokenId)
 nonReentrant
 isOwner(nftAddress, tokenId, msg.sender)
 {
 if (newPrice == 0) {
 revert PriceMustBeAboveZero();
        }

 s_listings[nftAddress][tokenId].price = newPrice;
 emit ItemListed(msg.sender, nftAddress, tokenId, newPrice);
    }
```

### 实施`withdrawProceeds()`

由于我们使用的是实现 `BuyItem()` 时讨论过的拉方法，撤销收益意味着简单地发送方法的调用者，无论他们在 `s_proceeds` 状态变量中的余额是多少。如果调用者没有任何收益，我们会回复一个 `NoProceeds()` 自定义错误。如果我们相信我们的代码正确地更新了 `s_proceeds` 状态变量，这是可行的，在我们简单的市场中，确实如此。重要的是，我们需要将卖方的收益余额更新为零。

```
function withdrawProceeds() external {
 uint256 proceeds = s_proceeds[msg.sender];
 if (proceeds <= 0) {
 revert NoProceeds();
 }
        s_proceeds[msg.sender] = 0;

 (bool success, ) = payable(msg.sender).call{value: proceeds}("");
 require(success, "Transfer failed");
    }
```

在上面的方法中，有一个不同寻常的说法: `payable(msg.sender).call{value: proceeds}("");` 。这就是新版 Solidity 如何向呼叫者地址发送值。 `Value` 这里指的是正在发送的以太量，看起来很奇怪的 `(“”)` 基本上是说 Solidity`call()`函数正在被无参数调用，由传入的空字符串表示。你可以在这里 阅读更多关于这个语法 [。](https://ethereum.stackexchange.com/questions/96685/how-to-use-address-call-in-solidity)

`.call()`函数返回两个值，一个表示成功或失败的布尔值，以及数据字节——我们不使用这些数据字节，因此不会将其分配给任何变量。

如果 `success` 为假整个方法调用通过[语句的操作恢复(被视为异常)。T15】](https://docs.soliditylang.org/en/v0.4.25/units-and-global-variables.html#error-handling)

### 实现实用 Getter 方法

现在我们几乎完成了 NFT 市场！我们只需要再添加两个实用方法。一个实用程序方法将帮助我们检索与特定令牌 ID 相关联的 `Listing` 对象，这样我们就可以找出卖家是谁以及该令牌的标价是多少。第二个效用函数帮助我们检索卖家赚了多少钱(即他们的销售收入)。注意，这两个方法是状态变量中特定值的“getter”函数。

```
function getListing(address nftAddress, uint256 tokenId)
 external
 view
 returns (Listing memory)
 {
 return s_listings[nftAddress][tokenId];
    }

 function getProceeds(address seller) external view returns (uint256) {
 return s_proceeds[seller];
    }
```

有了这个，我们的 NFT 市场就完整了！现在我们需要做的是编写一些脚本来部署到我们的 Hardhat 本地区块链，然后运行一些脚本来列出令牌。

在我们继续之前，让我们做一个快速编译检查。在您的终端中，从您的项目根目录中，运行 `yarn hardhat compile` 。如果成功了，那你就成功了。如果没有，请检查错误消息并返回您的步骤。调试是开发过程的关键部分！

### 样本 NFT 智能合同 

但是，在我们进入脚本之前，我们需要一个样本 NFT 智能合同，以便我们可以铸造代币，并在我们的市场上列出它们。我们将遵循 ERC721 令牌规范，这样我们就可以继承 OpenZeppelin 的 ERC721 库。在参考回购中有两个样本 NFT 合约 `<<root>>/contracts/test` 。它们不必在文件夹中，但是它们必须在 `contracts` 文件夹下。

因此，让我们制作 `BasicNft.sol` ，它指向 IPFS 上的一只可爱的狗，它将作为我们令牌的艺术品。NFT 合同相当简单。

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract BasicNft is ERC721 {
    string public constant TOKEN_URI =
 "ipfs://bafybeig37ioir76s7mg5oobetncojcm3c3hxasyd4rvid4jqhy4gkaheg4/?filename=0-PUG.json";
    uint256 private s_tokenCounter;

    event DogMinted(uint256 indexed tokenId);

 constructor() ERC721("Dogie", "DOG") {
 s_tokenCounter = 0;
    }

 function mintNft() public {
 _safeMint(msg.sender, s_tokenCounter);
 emit DogMinted(s_tokenCounter);
 s_tokenCounter = s_tokenCounter + 1;
    }

 function tokenURI(uint256 tokenId) public view override returns (string memory) {
 require(_exists(tokenId), "ERC721Metadata: URI query for nonexistent token");
 return TOKEN_URI;
    }

 function getTokenCounter() public view returns (uint256) {
 return s_tokenCounter;
 }
}
```

注意 `tokenURI()` 和 `getTokenCounter()` 是状态变量的 getters。这里真正的逻辑是在 `mintNft()` 方法中，我们利用了我们继承的 OpenZeppelin ERC721 基础契约。 `mintNft()` 铸造令牌，并用第二个参数中传递的令牌 ID 将 `msg.sender` (即函数的调用者)注册为 NFT 的所有者。我们使用 `s_tokenCounter` 状态变量来跟踪制造了多少令牌以及令牌 id。所以我们需要在发出 `DogMinted` 事件后递增计数器。

如果你想在你的市场上有多种类型的 NFT，你可以复制第二个样本 NFT 合同，名为 `BasicNftTwo.sol`， 从 [到这里](https://github.com/PatrickAlphaC/hardhat-nft-marketplace-fcc/blob/main/contracts/test/BasicNftTwo.sol) (本博客中的代码指两者，但它是可选的)。你会看到它和 `BasicNft.sol` 差不多，但是TOKEN _ URI状态变量指向不同的 IPFS 文件(不同种类的狗！).注意，两个契约都进入 `<<root>>/contracts/test` 。

再次运行 `yarn hardhat compile` 以确保一切按预期编译，并确保检查您的 NFT 市场合同和您的 NFT 合同编译无误。

## 部署脚本 

现在，让我们从这些部署脚本开始。

第一步是理解什么是部署脚本。部署脚本将 Solidity 编译成字节码，然后可以部署到 EVM 兼容的区块链上执行。实时智能合约是存储在区块链上的数据，它们以字节码的形式存储。编译步骤还会生成一个 JSON 工件文件，该文件包含 [契约元数据](https://docs.soliditylang.org/en/v0.8.12/metadata.html#contract-metadata) ，其中包括一些有用的数据，如 ABI(应用程序二进制接口)——一个我们可以用来与智能契约交互的“模式”。

部署脚本是编译我们的智能合同并将其部署到区块链的脚本。您可以快速阅读关于部署合同 的 [Hardhat 文档来掌握原则，但是我们使用一个名为“](https://hardhat.org/guides/deploying.html)[hard hat-deploy](https://github.com/wighawag/hardhat-deploy)”的 NPM 包，它为我们自动化了一些步骤。它还会自动运行我们放在 `deploy` 文件夹中的所有脚本，并添加一个[Hardhattask](https://hardhat.org/getting-started/#running-tasks)称为 `deploy` 到 hard hat 注册的任务中，这样我们只需运行 `yarn hardhat deploy` 即可运行我们所有的脚本。

那么让我们从一个 `deploy` 文件夹开始，与 `contracts` 在同一个文件夹层次级别，就像这样: `<<root>>/deploy` 。

### 部署`NftMarketplace.sol`
T3】

你可以看到下面的代码，但是要确保你的 Hardhat 配置文件( `hardhat.config.js` )拥有 repo 中指定的所有导入 [。Hardhat 将这些对象注入到部署脚本中。在 `deploy` 文件夹内，创建一个 `01-deploy-nft-marketplace.js` 脚本。我们使用 `01-` 前缀对我们的脚本进行编号，这样它们可以由 hardhat-deploy 按照字典顺序执行。](https://github.com/PatrickAlphaC/hardhat-nft-marketplace-fcc/blob/main/hardhat.config.js)

```
const { network } = require("hardhat")
const { developmentChains, VERIFICATION_BLOCK_CONFIRMATIONS } = require("../helper-hardhat-config")
const { verify } = require("../utils/verify")

module.exports = async ({ getNamedAccounts, deployments }) => {
 const { deploy, log } = deployments
 const { deployer } = await getNamedAccounts()
 const waitBlockConfirmations = developmentChains.includes(network.name)
 ? 1
        : VERIFICATION_BLOCK_CONFIRMATIONS

 log("----------------------------------------------------")
 const arguments = []
 const nftMarketplace = await deploy("NftMarketplace", {
 from: deployer,
 args: arguments,
 log: true,
 waitConfirmations: waitBlockConfirmations,
    })

 // Verify the deployment
 if (!developmentChains.includes(network.name) && process.env.ETHERSCAN_API_KEY) {
 log("Verifying...")
 await verify(nftMarketplace.address, arguments)
 }
 log("----------------------------------------------------")
}

module.exports.tags = ["all", "nftmarketplace"]
```

那么这到底是怎么回事？首先，我们导入我们需要的相关对象和项目。稍后将解释从 `helper-hardhat-config` 和 `utils/verify` 的导入。

然后，我们导出一个异步函数，它将一个对象作为参数。这个论点就是 HRE ( [Hardhat 运行时环境](https://hardhat.org/advanced/hardhat-runtime-environment.html) )，这是我们需要访问的有用的开发工具的集合。插件也丰富了 HRE，包括我们之前讨论的 hardhat-deploy 插件。

该异步函数执行以下操作:

*   访问实用程序功能以部署合同并登录到控制台。
*   从 `hardhat.config.js` 文件的 `namedAccounts` 属性中取出部署者索引。这将默认为索引 0，也就是 `deployer` 。那就是部署合约的 Hardhat 钱包(账号)(Hardhat 给我们的测试钱包)。这个实用程序属性是由 hardhat-deploy 包添加的。详见 [本](https://github.com/wighawag/hardhat-deploy#hardhat-environment-extensions) 和 [本](https://github.com/wighawag/hardhat-deploy#configuration) 。

使用来自 HRE 的 `deploy()` 函数，我们将我们的智能合约部署到本地的 Hardhat 开发链，并传入一个配置对象，该对象指定谁在部署合约、合约构造器采用什么参数以及其他配置数据。

你也会看到我们导入并使用 `developmentChains` 。这是为了运行条件逻辑，脚本中的一些逻辑的运行取决于我们是否在开发链上，在这种情况下是 `hardhat` 或 `localhost` 。你会看到这些网络被称为 `hardhat.config.js` 。

在我们的项目根目录下，我们应该创建一个名为 `helper-hardhat-config.js` 的文件，并从中导出两条数据:

```
const developmentChains = ["hardhat", "localhost"]
const VERIFICATION_BLOCK_CONFIRMATIONS = 6

module.exports = {developmentChains, VERIFICATION_BLOCK_CONFIRMATIONS }
```

`VERIFICATION_BLOCK_CONFIRMATIONS` 是指在我们假设一个交易(包括一个新的智能合约的创建)被“确认”之前，必须添加到区块链的块数。

如果你看看我们的 `01` 脚本，你会看到，对于开发链，我们只等待一个区块确认。如果我们不在本地 Hardhat 链上(即，我们在 testnet 或 mainnet 上)并且我们有一个 Etherscan API 密匙(你可以在这里的 [免费计划](https://etherscan.io/apis) 上获得这个密匙，但是我们在本地 Hardhat 链上运行时不需要它)，我们只在ethers can上验证我们的智能契约。要了解 `verify()` 实用程序的实现，请查阅 Hardhat 的 [文档](https://hardhat.org/plugins/nomiclabs-hardhat-etherscan.html#using-programmatically) 。

虽然我们不需要在本地网络上验证，但我还是会把它留在脚本中，这样你就能掌握它了。所以我们导入了一个 `verify()` 实用函数，我们需要创建它以便我们的代码可以编译。我们创建 `<<root>>/utils` 文件夹，把 `verify.js` 放在里面。你可以从 [这里复制](https://github.com/PatrickAlphaC/hardhat-nft-marketplace-fcc/blob/main/utils/verify.js) 的代码。

所以真的，这个脚本的核心重点是将我们的 `NftMarketplace.sol` 智能合约部署到本地 Hardhat 开发网络。如果你运行 `yarn hardhat` ，你应该看到 `deploy` 任务被列出。如果不是，您需要检查您的 `hardhat.config.js` 文件和您的 `deploy` 文件夹是否与本博客和参考回购中指定的一致。

![The “deploy” task correctly showing in the terminal](img/2c7347b9f32b68215ff2c3c239c27de2.png)

<figcaption id="caption-attachment-3804" class="wp-caption-text">The “deploy” task correctly showing in the terminal.</figcaption>



然后简单地用 `yarn hardhat deploy` 运行任务。如果出现“无法识别的任务部署”错误，这意味着`hardhat-deploy`的配置不正确——部署任务不会出现在上面显示的可用任务列表中。

但是，如果一切都按预期运行，那么应该会产生一条消息，说明您已经编译并部署了 marketplace 契约，以及所部署的智能契约的交易散列和以太坊地址。

![NftMarketplace.sol successfully deployed](img/deaa801ff9f19b582c5262b040b363cb.png)

<figcaption id="caption-attachment-3805" class="wp-caption-text">NftMarketplace.sol successfully deployed.</figcaption>



如果你想知道为什么它说编译了 14 个 Solidity 文件，那是因为我们依赖的开放 Zeppelin 库也需要编译！

### 部署 NFT 合同 

接下来，我们创建脚本 `02-deploy-basic-nft.js` ，它将 NFTs 部署到我们的本地开发链。您会注意到它看起来非常熟悉，因为两个函数签名逻辑都与 NFT 市场契约相同。关键的区别在于，正如脚本名称所示，我们部署的是示例 NFT 契约，而不是 NFT 市场契约。

```
const { network } = require("hardhat")
const { developmentChains, VERIFICATION_BLOCK_CONFIRMATIONS } = require("../helper-hardhat-config")
const { verify } = require("../utils/verify")

module.exports = async ({ getNamedAccounts, deployments }) => {
 const { deploy, log } = deployments
 const { deployer } = await getNamedAccounts()
 const waitBlockConfirmations = developmentChains.includes(network.name)
 ? 1
        : VERIFICATION_BLOCK_CONFIRMATIONS

 log("----------------------------------------------------")
 const args = []
 const basicNft = await deploy("BasicNft", {
 from: deployer,
 args: args,
 log: true,
 waitConfirmations: waitBlockConfirmations,
    })

 const basicNftTwo = await deploy("BasicNftTwo", {
 from: deployer,
 args: args,
 log: true,
 waitConfirmations: waitBlockConfirmations,
    })

 // Verify the deployment
 if (!developmentChains.includes(network.name) && process.env.ETHERSCAN_API_KEY) {
 log("Verifying...")
 await verify(basicNft.address, args)
 await verify(basicNftTwo.address, args)
 }
 log("----------------------------------------------------")
}

module.exports.tags = ["all", "basicnft"]
```

现在您已经掌握了窍门，您知道下一步该做什么:我们需要运行 `yarn hardhat deploy` 来确保我们所有的合同都部署好了。

![Successfully run the “deploy” task to compile and deploy all smart contracts.](img/f80b1c1c9bef53d84118d6e7723e2b05.png)

<figcaption id="caption-attachment-3806" class="wp-caption-text">Successfully run the “deploy” task to compile and deploy all smart contracts.</figcaption>



检查参考回购时，会看到 `<<root>>/deploy` 中有 [第三个脚本](https://github.com/PatrickAlphaC/hardhat-nft-marketplace-fcc/blob/main/deploy/03-update-front-end.js) 。我们现在不需要这个。该脚本用于将 ABI JSON 文件(在编译步骤之后，这些 JSON 文件显示在 `<<root>>/artifacts/contracts/…` 中)复制到一个单独的目录中，该目录包含前端 web 应用程序的 repo，该应用程序提供了一个 UI，我们可以在该 UI 中开始与智能合约进行交互。这超出了本博客的范围，所以我们不需要创建第三个脚本。你的 `deploy` 文件夹应该只包含我们在这篇博客中提到的两个脚本。

## 一个独立的 RPC 网络 

在我们讨论交互脚本之前，让我们回顾一下。我们已经编写了两个 NFT 合同和一个 NFT 市场智能合同，并且我们已经使用部署脚本将合同部署到我们本地的安全帽开发链。但是，我们如何与这些智能合约交互，并检查我们的市场智能合约是否正确运行我们在本博客开始时讨论的操作？

这就是交互脚本的用武之地。交互脚本类似于我们的部署脚本，因为它们是用 JavaScript 编写的，但是它们的目的是以编程方式与我们部署的智能合约进行交互。

为了与我们部署的合同进行交互，我们需要与略有不同的由安全帽提供的本地开发链合作。这次我们使用的网络名为 `localhost` ，这是我们在 `hardhat.config.js` 文件中指定的。我们称之为“独立网络”(以前我们运行的是“进程内”网络)。你可以在安全帽文档 [这里](https://hardhat.org/hardhat-network/#running-stand-alone-in-order-to-support-wallets-and-other-software) 读到这个。Hardhat 独立网络在本地主机 IP 地址 127.0.0.1 的端口 8545 上公开了一个[JSON RPC](https://eth.wiki/json-rpc/API)端点。

在你的控制台中，输入 `yarn hardhat` ，在“可用任务”标题下查看。您会看到有一个名为 `node` 的任务，它“在 EVM 的硬盘上启动一个 JSON-RPC 服务器”这就是独立的 `localhost` 发展链。

进入 `yarn hardhat node` 就火起来了。您将获得多个值得研究的控制台输出。滚动到输出的顶部，看起来会像这样:

![Firing up the standalone JSON-RPC local development blockchain.](img/7f7696aa6c8943ab342615ea65a4c0d0.png)

<figcaption id="caption-attachment-3807" class="wp-caption-text">Firing up the standalone JSON-RPC local development blockchain.</figcaption>



注意，节点任务编译并自动将我们的合同部署到这个独立的开发链中。它还告诉我们它“在 http://127.0.0.1:8545/启动了 HTTP 和 WebSocket JSON-RPC 服务器”

再往下，它会转储出一堆钱包账户和它们的私钥。请阅读此处的警告——这些仅是开发以太坊账户，不得用于实际交易！

拥有独立 RPC 端点的好处是，我们可以将前端 web 应用连接到我们的开发网络及其智能合约。我们甚至可以将 Metamask 等钱包应用程序连接到它。

既然我们了解了这个独立网络是怎么回事，那就让我们用 `ctrl+c` 干掉那个网络吧。无论如何，每次我们更改代码时，我们都需要重新部署我们的合同。当我们的合同陷入糟糕的状态时，我们还需要终止并重启这个区块链本地开发项目，这样我们就可以重新开始我们的 NFT 市场和代币合同。

## 交互脚本

为了与我们的合同进行交互，我们需要做以下事情:

*   使用我们的部署者帐户(索引为 0 的 Hardhat 测试帐户)部署合同。
*   创建并列出 3 个拥有“所有者”账户的非功能性交易账户(指数为 1 的 Hardhat 测试账户)。
*   用买家账户(指数为 2 的安全帽测试账户)购买 NFT #0。
*   更新 NFT #1 的价格并查看列表。
*   取消 NFT #2，并检查它是否不再列出。
*   检查 marketplace 是否正确记录了所有者/卖方出售 NFT #0 的收益。

这些步骤涵盖了我们市场合同的主要操作。本节博客中的代码与参考回购略有不同，但您可以在 [本要诀](https://gist.github.com/zeuslawyer/032f61b04495ca00cfbe8d125fd4574c) 中找到本博客的交互脚本代码，每个脚本都在自己的文件中。

### 铸造并上市三家 NFT 

为了以编程方式与我们部署的契约进行交互，我们将使用 [安全帽-乙醚插件](https://hardhat.org/plugins/nomiclabs-hardhat-ethers.html) 。这个插件包装了 ethers.js 库，它提供了有用的 API 来处理 EVM 链。

这里有几个细微差别需要记住。您应该还记得在这篇博客的前面，NFT 的所有者可以批准另一个以太坊地址来管理和操作令牌相关的操作，比如令牌转移。这意味着在用户铸造令牌后，他们需要“批准”市场，以便市场可以在调用其 `buyItem()` 函数时转移所有权。关于 ERC721 的 `approve()` 方法 [可以在这里](https://docs.openzeppelin.com/contracts/3.x/api/token/erc721#IERC721-approve-address-uint256-) 阅读。

请注意，在下面的代码中，所有者铸造了一个令牌，然后批准市场代表所有者操作它，然后所有者将它列在市场上。 为此，首先在您的项目目录中创建一个新的 `<<root>>/scripts` 文件夹。然后创建一个新的`mint-and-list-item.js`文件并粘贴到下面的脚本中。

```
const { ethers } = require("hardhat")

const PRICE = ethers.utils.parseEther("0.1")

async function mintAndList() {
 const accounts = await ethers.getSigners()
    const [deployer, owner, buyer1] = accounts

 const IDENTITIES = {
 [deployer.address]: "DEPLOYER",
 [owner.address]: "OWNER",
 [buyer1.address]: "BUYER_1",
    }

 const nftMarketplaceContract = await ethers.getContract("NftMarketplace")
    const basicNftContract = await ethers.getContract("BasicNft")

    console.log(Minting NFT for ${owner.address})
 const mintTx = await basicNftContract.connect(owner).mintNft()
 const mintTxReceipt = await mintTx.wait(1)
    const tokenId = mintTxReceipt.events[0].args.tokenId

 console.log("Approving Marketplace as operator of NFT...")
 const approvalTx = await basicNftContract
 .connect(owner)
 .approve(nftMarketplaceContract.address, tokenId)
    await approvalTx.wait(1)

 console.log("Listing NFT...")
 const tx = await nftMarketplaceContract
 .connect(owner)
 .listItem(basicNftContract.address, tokenId, PRICE)
 await tx.wait(1)
    console.log("NFT Listed with token ID: ", tokenId.toString())

 const mintedBy = await basicNftContract.ownerOf(tokenId)
 console.log(
        NFT with ID ${tokenId} minted and listed by owner ${mintedBy} 
with identity ${IDENTITIES[mintedBy]}.
 )
}

mintAndList()
 .then(() => process.exit(0))
 .catch((error) => {
 console.error(error)
 process.exit(1)
    })
```

让我们对此进行分解，因为相同的模式将在剩余的脚本中重复。

首先注意异步 `mintAndList()` 函数在底层被调用，如果它出错，我们将错误打印到控制台，然后用一个 [非零错误](https://www.gnu.org/software/bash/manual/html_node/Exit-Status.html#:~:text=A%20non%2Dzero%20exit%20status,N%20as%20the%20exit%20status.) 退出。

在函数体中，我们使用 `getSigners()` 获得 20 个 Hardhat 帐户的列表，并使用 [JS 析构赋值](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) 访问前三个地址对象并给它们变量名——`deployer`是部署智能合约的地址， `owner` 铸币厂并拥有 NFT， 【T3

我们还创建了一个 `IDENTITIES` 助手对象，它将地址映射到角色。这使得控制台中的调试更加容易。

然后，我们访问合同并运行造币厂、批准和列表操作。我们可以确认 `mintedBy` 的值是否是从市场智能合约中读取的，并且地址是否与 `owner` 相同。清单时，我们在 `PRICE` 中传递常数，也就是 0.1 的醚类计价魏。你会注意到，我们为此使用了 ethers.js 实用函数`parseEther()`([文档](https://docs.ethers.io/v5/api/utils/display-logic/#utils-parseEther) )。

现在，在我们运行脚本之前，我们需要准备好使用我们独立的 Hardhat RPC local testnet。为此，我们需要打开两个终端窗口。在第一个中，键入 `yarn hardhat node` 。这将启动我们之前讨论过的独立 RPC 网络。

在第二个终端窗口，键入 `yarn hardhat run scripts/mint-and-list-item.js --network localhost` 。如果到目前为止您做得对，您应该会看到类似这样的内容:

![Successfully mint and list your NFT.](img/03a359d928a8a4187e1f31dc16d0cf85.png)

<figcaption id="caption-attachment-3808" class="wp-caption-text">Successfully mint and list your NFT.</figcaption>



如果您想知道本地 RPC 服务器是如何记录您的事务的，请切换到第一个终端窗口并阅读那里的输出。

那是 0 号令牌。我们需要为后面的剧本再创造两个。只需再运行两次相同的 造币清单 脚本，就可以得到令牌 ID 2。

### 购买代币

从我们上面的脚本列表中，您会记得接下来我们要让其中一个帐户购买令牌 ID 0。第二个脚本的结构将与 `mint-and-list`， 相同，但我们需要改变脚本内部的实际逻辑。在您的 `scripts` 文件夹中新建一个 `buy-item.js` 脚本，如下图:

```
const { ethers } = require("hardhat")

const TOKEN_ID = 0 // SET THIS BEFORE RUNNING SCRIPT

async function buyItem() {
 const accounts = await ethers.getSigners()
    const [deployer, owner, buyer1] = accounts

 const IDENTITIES = {
 [deployer.address]: "DEPLOYER",
 [owner.address]: "OWNER",
 [buyer1.address]: "BUYER_1",
    }

 const nftMarketplaceContract = await ethers.getContract("NftMarketplace")
    const basicNftContract = await ethers.getContract("BasicNft")

 const listing = await nftMarketplaceContract
       .getListing(basicNftContract.address, TOKEN_ID)

 const price = listing.price.toString()
 const tx = await nftMarketplaceContract
 .connect(buyer1)
 .buyItem(basicNftContract.address, TOKEN_ID, {
 value: price,
 })
 await tx.wait(1)
    console.log("NFT Bought!")

 const newOwner = await basicNftContract.ownerOf(TOKEN_ID)
 console.log(
        New owner of Token ID ${TOKEN_ID} is ${newOwner} with identity of 
${IDENTITIES[newOwner]} 
 )
}

buyItem()
 .then(() => process.exit(0))
 .catch((error) => {
 console.error(error)
 process.exit(1)
    })
```

这看起来越来越熟悉了！这里的关键区别在于，我们使用 ethers.js `.connect(signer)` 方法从另一个帐户发送事务。在这种情况下，我们要确保 `buyer1` 是 marketplace 契约中 `buyItem()` 方法的调用方。还要注意，我们使用 `getListing()` 方法来访问 `Listing` 的详细信息并检索价格，因为那是我们需要在 `buyItem()` 中支付的金额。最后，我们通过直接从 NFT 契约的状态读取数据，检查令牌的新所有者实际上是 `buyer` 。

运行 `yarn hardhat run scripts/buy-item --network localhost` 你应该会看到这样的东西:

![Successfully buy a listed NFT.](img/83e804268691e6bd3efafbeb3bc842e5.png)

<figcaption id="caption-attachment-3809" class="wp-caption-text">Successfully buy a listed NFT.</figcaption>



### 更新代币的价格 

现在我们已经出售了代币 0，它不再在市场上列出。下一步是更新令牌 ID 1 的价格，它是在开始时铸造和列出的。您将看到模式在这里重复，因此创建 `update-listing` 脚本，并从这个要点 粘贴正确的代码 [。如果您运行 `yarn hardhat run scripts/update-listing --network localhost` 并设置了正确的 `TOKEN_ID` ，那么您应该会看到如下所示的日志，显示价格已经更新:](https://gist.github.com/zeuslawyer/032f61b04495ca00cfbe8d125fd4574c)

![Successfully update the price of a listed NFT.](img/967786094b7790491753998733249733.png)

<figcaption id="caption-attachment-3810" class="wp-caption-text">Successfully update the price of a listed NFT.</figcaption>



### 剩下的两个操作

剩下的工作就是编写两个脚本——一个用于取消列表，另一个用于让店主/卖家知道他们的代币销售收入。再次检查代码的 gists，当您运行 `scripts/cancel-item.js` : 时，您应该会在控制台中得到如下所示的日志

![Cancel the listing of a NFT.](img/962b9590995c3ec06cb65c60e412f567.png)

<figcaption id="caption-attachment-3811" class="wp-caption-text">Cancel the listing of an NFT.</figcaption>



为了查看 NFTs 的所有者从出售他们的令牌中得到多少，我们运行 `get-seller-proceeds.js` ，它应该产生以下结果:

![Check a seller’s proceeds stored in the marketplace smart contract.](img/777a84e5de60a5ca76091d5bc56fe9ff.png)

<figcaption id="caption-attachment-3812" class="wp-caption-text">Check a seller’s proceeds stored in the marketplace smart contract.</figcaption>



注意，卖方的收益，储存在市集契约的`s_proceeds`映射中，都是以魏计价的。为了将其转换回更具可读性的 ETH 数量，我们使用 ether.js 实用函数`.formatEther()`([docs](https://docs.ethers.io/v5/api/utils/display-logic/#utils-formatEther))。

## 结束

对你的代码进行自动化测试总是一个好主意。本参考资料 [回购](https://github.com/PatrickAlphaC/hardhat-nft-marketplace-fcc#hardhat-nextjs-nft-marketplace.) 有一套测试，你可以参考使用 [安全帽工具](https://hardhat.org/tutorial/testing-contracts.html) 利用摩卡和华夫实用程序。测试还检查了我们期望的 `revert()` 、函数修饰符和异常处理行为。它们对于理解要注意的边缘案例非常有用，所以请务必查看它们。

如果你想建立一个与 NFTMarketplace 智能合约交互的前端，看看这个来自 Chainlink Spring 2022 黑客马拉松的 [视频。](https://www.youtube.com/watch?v=l4r0IXjAlpc) 建立一个前端将是一个有趣的挑战，并给你在自己的 NFT 市场上销售 NFT 系列所需的所有技能！

访问[chain . link](https://chain.link/)或阅读[docs . chain . link](https://docs.chain.link/)上的文档，了解更多关于 Chainlink 的信息。您还可以订阅 [Chainlink 简讯](https://chn.lk/newsletter)以了解 Chainlink 堆栈中的最新信息。 [要讨论一个集成，就去找专家。T19】](https://chainlinkcommunity.typeform.com/to/OYQO67EF?typeform-source=blog.chain.link)`