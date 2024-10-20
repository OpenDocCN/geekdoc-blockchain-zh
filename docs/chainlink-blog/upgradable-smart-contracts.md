# 可升级智能合同:什么是智能合同以及如何部署您自己的智能合同

> 原文：<https://blog.chain.link/upgradable-smart-contracts/>

在这篇博客中，我们将学习构建可升级智能合约背后的基本设计原则。最后，您应该了解我们为什么要升级智能合约，如何升级智能合约，以及在升级时需要考虑哪些问题。本博客主要关注以太坊和基于[【EVM】](https://ethereum.org/en/developers/docs/evm/)的智能合约。观看本视频的第一部分，了解什么是 EVM。

为了充分利用这个博客，你应该对 [区块链如何工作](https://blog.chain.link/what-is-blockchain/) 有一个初级的工作知识，特别是以太坊区块链。在这篇博客的后面有一个简短的代码演练，所以至少有三个月的编程经验将是有用的，因为对 Solidity 以及如何编译它、 [有一些基本的了解，什么是智能契约](https://chain.link/education/smart-contracts#:~:text=A%20smart%20contract%20is%20a,certain%20predefined%20conditions%20are%20satisfied.) 以及它们是如何部署的，以及如何使用 Metamask 和 Hardhat 之类的工具。

# 什么是可升级智能合约？

区块链注定是不可改变的——这是区块链技术的核心原则之一。存储在以太坊区块链上的数据(包括部署在其上的智能合约)也是不可变的。

在我们深入了解如何升级智能合约的细节之前，让我们考虑一下为什么我们会想要升级智能合约。

主要原因有:

*   修复错误。
*   改善功能。
*   修改不再需要或不再有用的功能。
*   优化代码，更有效地利用以太坊气体。
*   应对技术、市场或社会的发展。
*   不再需要将整个用户群体迁移到新版本的应用程序。

如果有足够的时间，大多数东西都需要修理。但是存储在区块链上的数据是不可变的。那么，智能合约如何能够升级呢？

简短的回答是，智能合约本身无法改变——一旦部署到区块链，它们就是永久不变的。但是 dApp 可以被设计成让一个或多个智能合约一起运行来提供它的“后端”。这意味着我们可以升级这些智能合约之间的交互模式。升级智能合约并不意味着我们修改已部署的智能合约的代码，而是意味着我们用一个智能合约替换另一个智能合约。我们这样做的方式(在大多数情况下)意味着最终用户不必改变他们与 dApp 的交互方式。

因此，升级智能合约实际上是用新的智能合约替换旧合约的过程。实际上，新的智能契约被使用，旧的被“抛弃”在链上，因为它们是不可变的。

# 升级是如何进行的？

智能合同通常通过使用一种称为“代理模式”的软件架构模式来升级。但是“代理”这个词在软件设计中是什么意思呢？你可以参考 [本系统设计入门](https://www.freecodecamp.org/news/systems-design-for-interviews/) 第五节我写的，但是 TL；DR 是指代理是大型软件系统中的一个软件，代表系统的另一部分。在传统的 Web2 计算中，代理位于客户端应用程序和服务器应用程序之间。正向代理代表客户端应用，反向代理代表服务器应用。

在智能合约领域，代理更像是一个反向代理，代表另一个智能合约。它是一种中间件，将来自前端的传入流量重定向到系统后端的正确智能契约。作为一个智能契约，代理拥有自己的以太坊契约地址，该地址是“稳定的”(即不变的)。因此，您可以换出系统中的其他智能合约，只需用新部署的智能合约的正确地址更新代理智能合约。dApp 的最终用户直接与代理交互，而仅通过代理间接与其他智能合约交互。

因此，在智能合约开发中，代理模式是通过以下两部分实现的:

在这篇博客中，我们将这些元素分别称为代理契约和逻辑契约。

代理模式有三种常见的变体，我们将在下面讨论。

### 简单代理模式

一个简单的代理具有如下所示的架构。

![Image showing end user, proxy contract, and logic contract.](img/7f57de9f492db95cf433b4bf324af7fc.png)

让我们更深入地了解它是如何工作的。

在 EVM，有一种东西叫做“执行语境”。可以把它想象成执行代码的空间。

因此，代理契约有自己的执行上下文，所有其他智能契约也是如此。代理契约也有自己的存储，数据永久存储在区块链上，还有自己的以太网余额。智能合约持有的数据和余额统称为其“状态”，状态是其执行上下文的一部分。

代理契约使用存储变量来跟踪构成 dApp 的其他智能契约的地址。这就是它重定向事务并调用相关智能契约的方式。

但是有一个巧妙的技巧，用于将消息调用传递给正确的契约。代理契约不只是对逻辑契约进行常规的函数调用；它使用了一个叫做 [的东西](https://docs.soliditylang.org/en/v0.8.6/introduction-to-smart-contracts.html?highlight=delegatecall#delegatecall-callcode-and-libraries) 。 `Delegatecall` 除了目标地址的代码在调用契约的上下文中执行之外，类似于常规的函数调用。如果逻辑契约的代码更改了存储变量，这些更改将反映在代理契约的存储变量中，即反映在代理契约的状态中。T13
T15】

那么 `delegatecall` `逻辑在代理合同中处于什么位置呢？答案就在代理合同的 [回退功能](https://docs.soliditylang.org/en/v0.8.17/contracts.html#fallback-function) 。当代理协定收到对它不支持的函数的函数调用时，将调用代理协定的回退函数来处理该函数。代理协定在其回退函数中使用自定义逻辑将调用重定向到逻辑协定。`

 `将这一原则应用于代理和逻辑契约， `delegatecall` 将调用逻辑契约的代码，但是该代码在代理契约的执行上下文中运行。这意味着逻辑契约中的代码有能力改变代理契约中的状态——它可以改变代理契约中存储的状态变量和其他数据。这有效地将应用程序的状态从执行的代码中分离出来。代理契约有效地保存了所有 dApp 的状态，这意味着可以在不丢失状态的情况下更改逻辑。

现在，应用程序状态和应用程序逻辑在 EVM 中是分离的，我们可以通过更改逻辑契约来升级应用程序，并为代理提供新的地址。但是应用程序的状态不会受到这次升级的影响。

使用代理时，我们需要注意两个常见问题。

一期是 [储存碰撞](https://docs.openzeppelin.com/upgrades-plugins/1.x/proxies#unstructured-storage-proxies)；另一种是另一种类型的碰撞，称为 [代理选择器碰撞](https://medium.com/nomic-foundation-blog/malicious-backdoors-in-ethereum-proxies-62629adf3357) 。您可以阅读关于存储冲突的链接文章来了解更多信息，但是现在我们将集中讨论选择器冲突，因为它们是我们将要研究的代理模式的根本原因。

正如我们之前看到的，代理将所有的函数调用委托给逻辑契约。然而，代理契约本身也有功能，这些功能是它们内部的，并且是它们运行所必需的。例如，一个代理契约需要像 `upgradeTo(address newAdd)` 这样的函数来升级到新的逻辑契约的地址。那么，如果代理契约和逻辑契约具有相同名称和签名(参数和类型)的函数，会发生什么呢？代理契约如何知道是调用自己的函数还是调用逻辑契约的 `delegatecall` `？这被称为“ [代理选择器冲突](https://medium.com/nomic-foundation-blog/malicious-backdoors-in-ethereum-proxies-62629adf3357) ”，是一个可以被利用的安全漏洞，或者至少是令人讨厌的错误的来源。`

 `从技术上讲，这种冲突也可能发生在函数之间，即使它们的名称不同。这是因为每个可公开调用的函数(可以在[【ABI】](https://blog.chain.link/what-are-abi-and-bytecode-in-solidity/)中定义的函数)都在字节码级别由一个四字节长的[](https://solidity.readthedocs.io/en/v0.4.24/abi-spec.html?highlight=signature#function-selector)标识符来标识。因为只有四个字节，所以从技术上讲，两个完全不同的函数签名的前四个字节可能恰好相同，从而为不同的函数签名产生相同的标识符，从而导致冲突。

幸运的是，当冲突由同一契约内的函数签名产生时，Solidity 编译器可以检测到这种子类型的选择器冲突，但当这种冲突发生在不同的契约上时，则不能。例如，如果代理契约和逻辑契约之间发生冲突，编译器将无法检测到它，但在同一个代理契约中，编译器会检测到冲突。

解决这个问题的方法是“透明”代理模式，目前已经普及的有 [开放齐柏林](https://blog.openzeppelin.com/the-transparent-proxy-pattern/) 。

### 透明代理模式

在透明代理模式中，由最终用户(调用者)发起的函数调用总是被路由到逻辑契约，而不是代理契约。但是，如果调用者是代理的管理员，代理将知道调用它自己的管理功能。这具有直观的意义，因为在代理契约中调用管理功能来管理可升级性和其他管理任务应该仅由管理员来完成，并且如果存在冲突，可以合理地假设管理员打算调用代理契约的功能，而不是逻辑契约的功能。但如果调用者是任何其他非 admin 地址，代理将总是将 `delegatecall` 调出到相关的逻辑契约中。我们可以通过检查 `message.sender` 值来识别调用者。

在这种模式中，代理契约在其回退函数中会有逻辑来解析 `message.sender` 和被调用的函数选择器，并相应地调用它自己的一个函数或委托给一个逻辑契约。

OpenZeppelin 契约，正如我们将在我们的代码演练中看到的，添加了另一个抽象级别，具有由 [代理管理员契约](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/proxy/transparent/ProxyAdmin.sol) 拥有的升级功能，该智能契约是一个或多个代理契约的管理员。此代理管理合同必须是升级相关功能的调用方。因此，最终用户将直接与代理交互，代理将 `delegatecall` 输出到逻辑契约，但是升级和管理请求将通过 ProxyAdmin 契约传递，然后代理将升级请求转发到代理。

透明代理模式确实有一些缺点。如果不小心处理，它们容易受到函数选择器冲突的影响，运行它们会耗费更多的资源(因为 EVM 需要额外的资源来加载每个 `delegatecall` 的逻辑契约地址)，以这种模式部署代理契约也会耗费更多的资源。

### UUPS 模式

通用可升级代理标准(UUPS)是在 [EIP1822](https://eips.ethereum.org/EIPS/eip-1822) 中提出的，作为一种创建与所有合同通用兼容的代理合同标准的方式。它克服了代理函数选择器冲突的问题。这种模式也使用 Solidity 的 `delegatecall` 操作，但是在简单/透明代理模式中，所有升级都由代理契约管理，而在 UUPS 中，升级由逻辑契约处理，特别是逻辑契约继承的“可代理”智能契约。

逻辑契约仍将在代理契约的上下文中执行，从而利用代理契约的存储、余额和地址，但是逻辑契约从包含升级功能的可代理父契约继承。包含在可代理的智能协定中的升级逻辑用于更新存储在代理协定中的逻辑协定的地址。

由于 Solidity 编译器能够检测在同一契约中出现的函数选择器冲突，父可代理契约中升级逻辑的存在有助于编译器识别这种冲突，从而降低其可能性。

UUPS 代理模式也有缺点。虽然以这种模式部署更便宜(更省油)，但是使用这种模式维护 dApp 的智能合约可能更具挑战性。

一个重要的问题是，由于升级逻辑不在代理契约中，而是在逻辑契约的可代理父契约中，如果更新的逻辑契约未能继承可代理，则升级功能不会被继承，并且将来不可能升级智能契约。

但是这个问题有一个好处:UUPS 模式允许通过简单地不再继承 proxiable 契约来实现可升级性，这是透明代理模式中所没有的选项。这就是为什么 OpenZeppelin 和其他人 [推荐](https://docs.openzeppelin.com/contracts/4.x/api/proxy#transparent-vs-uups) 在透明代理上使用 UUPS，尽管在撰写本文时透明仍然更受欢迎。

# 码沿

首先，我们将采用透明代理模式，使用[OpenZeppelin](https://docs.openzeppelin.com)升级工具，它与使用 JavaScript 和[hard hat](https://hardhat.org/)的常见 Web3 开发工作流一起工作。OpenZeppelin 提供了与 Hardat 和 Truffle 集成的 [插件](https://docs.openzeppelin.com/upgrades-plugins/1.x/) 。我们将使用安全帽。

hard hat 插件为我们提供了类似于 `deployProxy` 的功能，这些功能为我们跟踪逻辑契约，并使我们能够轻松升级功能。默认情况下，部署合同的地址是拥有升级合同的管理员权限的地址。

让我们创建一个 Hardhat 项目——您可以随意命名它——在该目录中，让我们通过以下步骤开始设置我们的项目工具。

#### 项目设置

安装由 OpenZeppelin 提供的 Hardhat 开发者工具、Web3 库和升级插件。下面的命令也会创建你的 `package.json` 文件。

```
yarn add -D hardhat @openzeppelin/hardhat-upgrades @nomiclabs/hardhat-ethers ethers
```

安装来自 NPM 的合同包，其中包含我们想要使用的 Chainlink 合同接口和 OpenZeppelin 可升级合同库:

```
yarn add @chainlink/contracts  @openzeppelin/contracts-upgradeable
```

然后运行 `yarn hardhat` 在项目根目录下创建一个空的 `hardhat.config.js` 文件在根目录下。在这个配置文件中，粘贴以下内容，告诉 Hardhat 在导入正确的依赖项时，项目将使用哪个编译器版本:

```
require("@nomiclabs/hardhat-ethers");

require("@openzeppelin/hardhat-upgrades");

*const* GOERLI_RPC_URL = process.env.GOERLI_RPC_URL_HTTP
*const* PRIVATE_KEY = process.env.WALLET_PRIVATE_KEY_DEV1;

*const* ETHERSCAN_KEY = process.env.ETHERSCAN_API_KEY;

/** *@type* import('hardhat/config').HardhatUserConfig */
*module*.*exports* = {
solidity: "0.8.17",
defaultNetwork: "hardhat",
 networks: {
 localhost: {
chainId: 31337,
 },
 goerli: {
 url: GOERLI_RPC_URL,
accounts: PRIVATE_KEY ? [PRIVATE_KEY] : [],
chainId: 5,
 },
 },
 etherscan: {
 apiKey: ETHERSCAN_KEY,
 },
};
```

#### 智能合约代码

在您的项目根中，创建一个 `<root>/contracts/PriceFeedTrackerV1.sol` Solidity 文件，并将以下智能合约粘贴到其中:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";
import "@openzeppelin/contracts-upgradeable/proxy/utils/Initializable.sol";

*contract* PriceFeedTracker is Initializable {
   *address* *private* admin;

   *function* initialize(*address* _admin) *public* initializer {
admin = _admin;
 }

   *function* getAdmin() *public* *view* returns (*address*) {
       return admin;
   }

   /**
 * Network: Goerli
 * Aggregator: ETH/USD
 * Address: 0xD4a33860578De61DBAbDc8BFdb98FD742fA7028e
 */
   *function* retrievePrice() *public* *view* returns (*int*) {

AggregatorV3Interface aggregator = AggregatorV3Interface(

           0xD4a33860578De61DBAbDc8BFdb98FD742fA7028e
 );
 (
 ,
           /*uint80 roundID*/
           *int* price, /*uint startedAt*/ /*uint timeStamp*/ /*uint80 answeredInRound*/
 ,
           ,

) = aggregator.latestRoundData();

       return price;
 }
} 
```

如果您现在运行 `yarn hardhat compile` ，您应该会看到 Solidity 代码编译成功，并且您的项目目录中有两个新文件夹，“工件”和“缓存”。

您会注意到，这个 V1 智能合约从 Goerli 网络上的 Chainlink 价格馈送中检索 ETH/USD 价格数据。现在，价格提要的地址是硬编码的，这意味着它只能返回 ETH/USD 价格。将来，我们将升级它来处理 Goerli 网络上任何资产对的价格馈送地址。

现在，让我们考虑一下 `Initializable` 和 `initialize()` 函数是怎么回事。由于可靠性方面的一些怪癖超出了本博客的范围，当我们使用[Open Zeppelin upgradable contracts](https://docs.openzeppelin.com/learn/upgrading-smart-contracts#initialization)时，我们不能在我们的智能合约中包含构造函数。相反，我们通过扩展 `Initializable` `基础契约来创建我们自己的类似解释器的功能，这有助于我们将 `initializer` 修饰符应用于 `initialize()` 函数。我们可以给 initialize 函数起任何我们喜欢的名字，但是通过使用 initialize，Hardhat 插件会识别它，并且在默认情况下会调用这个函数。如果我们有另一个名字的初始化函数，我们需要指定我们的初始化函数的名字。`

 `这个带有修饰符的“初始化”模式通过确保 `initialize()` 只运行一次来模拟构造函数。如果需要，我们可以在这里明确地设置我们的管理地址——默认地址是部署者的地址。 `retrievePrice()` 函数调用 [ETH/USD 价格馈送](https://docs.chain.link/docs/data-feeds/price-feeds/) 智能合约并返回交易价格。

#### 部署脚本

让我们使用下面的脚本在 `scripts/deploy_upgradeable_pricefeedtracker.js` `中部署这个 V1 合同。`

 ````
// The Open Zeppelin upgrades plugin adds the `upgrades` property
// to the Hardhat Runtime Environment.
*const* { ethers, network, upgrades } = require("hardhat");

async *function* main() {
 // Obtain reference to contract and ABI.
 *const* PriceFeedTracker = await ethers.getContractFactory("PriceFeedTracker");
 console.log("Deploying PriceFeedTracker to ", network.name);

 // Get the first account from the list of 20 created for you by Hardhat
 *const* [account1] = await ethers.getSigners();

 //  Deploy logic contract using the proxy pattern.
 *const* pricefeedTracker = await upgrades.deployProxy(
   PriceFeedTracker,

   //Since the logic contract has an initialize() function
   // we need to pass in the arguments to the initialize()
   // function here.
   [account1.address],

   // We don't need to expressly specify this
   // as the Hardhat runtime will default to the name 'initialize'
{ initializer: "initialize" }
 );
 await pricefeedTracker.deployed();

 console.log("PriceFeedTracker deployed to:", pricefeedTracker.address);
}

main();
```

通过使用 [中的](https://docs.openzeppelin.com/upgrades-plugins/1.x/)[`deployProxy()`](https://docs.openzeppelin.com/upgrades-plugins/1.x/api-hardhat-upgrades#deploy-proxy)OpenZeppelin 升级插件 ，可以在以后升级部署的契约实例。默认情况下，只有最初部署合同的地址有权对其进行升级。

`deployProxy` 会创建如下交易:

在我们运行部署脚本之前，请确保您有足够的 Goerli ETH。你可以从 [的链环龙头](https://faucets.chain.link/) 中获得格利埃特。确保您还在环境变量中设置了 RPC 节点 URL 和私有密钥，以便您的 `hardhat.config.js` 文件可以读取它们！

我们可以使用以下命令运行我们的部署脚本，将合同部署到以太坊 Goerli testnet。

```
yarn hardhat run --network goerli scripts/deploy_upgradeable_pricefeedtracker.js
```

这应该会在您的终端中产生一个确认，看起来像下面的，但是具有不同的合同地址。记下这个合同地址。请注意，它是您的代理契约的地址，而不是逻辑契约的地址。我们需要代理契约的地址，因为这是我们将用来与逻辑契约交互的稳定(不变)的地址。

```
Deploying PriceFeedTracker...
PriceFeedTracker deployed to: 0x5FC8d32690cc91D4c39d9d3abcBD16989F875707
```

你可以在这里 研究 `deployProxy()`及其配置选项 [的文档。请注意，默认模式是“透明”的，但是您可以通过显式设置该配置选项来指定您希望您的代理遵循 UUPS 模式。](https://docs.openzeppelin.com/upgrades-plugins/1.x/api-hardhat-upgrades#common-options)

#### 安全帽控制台

在我们升级我们的契约之前，让我们使用 Hardhat 控制台与它交互，它允许我们编写 JavaScript 来与我们的逻辑契约交互，这是通过代理契约部署的。

在新(第三更！)终端窗口，运行以下命令将控制台连接到戈利区块链:

```
yarn hardhat console --network goerli
```

这将打开控制台提示符，您可以在其中单独运行以下命令:

```
> const PriceFeedTracker = await ethers.getContractFactory("PriceFeedTracker");
undefined
```

```
> const priceFeedTracker = await PriceFeedTracker.attach('<<<< YOUR CONTRACT ADDRESS  >>>>') 
undefined
```

然后调用 `getAdmin()` getter 函数，它应该输出您的部署者钱包地址——您在部署脚本中传递给初始化函数参数的地址。

```
> (await priceFeedTracker.getAdmin())
'0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266'
```

接下来尝试检索 ETH/USD 价格。这是一个仅供查看的调用，因为它不会修改状态或发出任何事件，所以您不需要支付汽油费。

```
> (await v1.retrievePrice())
BigNumber { value: "150701000000" }
```

好吧！如果您得到了这些结果，那么代理契约正在正确地与您部署的代理 契约进行交互。

这里有一个有用的提示:转到 `goerli.etherscan.io/address/YOUR_CONTRACT_ADDRESS` ，然后点击事件选项卡。您应该会看到类似下图的几个事件。查找名为“升级”的事件，然后单击旁边的小箭头。这将向您显示实现合同的地址。这是每次升级智能合同时最终都会更改的地址。

![Image showing proxy contract address on Goerli](img/45abb34c9e1134494b8442043e546407.png)

#### 升级后的逻辑契约

现在，让我们一起创建一个更新的逻辑契约，它增加了一些功能。看看下面的`PriceFeedTrackerV2`。您会注意到以下变化:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";
import "@openzeppelin/contracts-upgradeable/proxy/utils/Initializable.sol";

*contract* PriceFeedTrackerV2 is Initializable {
   *address* *private* admin;
   *int* *public* price; // NOTE: new storage slot

   // Emitted when the price is retrieved changes
   *event* PriceRetrievedFrom(*address* feed, *int* price);

   *function* initialize(*address* _admin) *public* initializer {
admin = _admin;
   }

   *function* getAdmin() *public* *view* returns (*address*) {
       return admin;
 }

   // Fetches the price from the feed.
   // Note that the function is no longer a view function as it emits an event.
   *function* retrievePrice(*address* feed) *public* returns (*int*) {
       require(
           feed != *address*(0x0),
           "PriceFeedTrackerV2: Pricefeed address must not be zero address."
       );

AggregatorV3Interface aggregator = AggregatorV3Interface(feed);
 (
 ,
           /*uint80 roundID*/
           *int* _price, /*uint startedAt*/ /*uint timeStamp*/ /*uint80 answeredInRound*/
 ,
           ,

) = aggregator.latestRoundData();

price = _price;

       emit PriceRetrievedFrom(feed, _price); 
       return price;
 }
}
```

#### 部署升级合同脚本

升级逻辑契约具有不同的名称和新功能。我们可以通过调用[upgrade proxy](https://docs.openzeppelin.com/upgrades-plugins/1.x/api-hardhat-upgrades#upgrade-proxy)函数来升级 V1 实例，该函数 创建以下事务:

我们更新后的脚本将在 `scripts/upgrade_pricefeedtracker.js` 中，看起来像这样(注意我们如何使用 `upgradeProxy` 而不是 `deployProxy` )。非常重要的是要注意，在运行脚本之前，您必须添加您部署的合同的地址——忘记这是一个容易犯的错误，可能会让您困惑几个小时！

```
const { ethers, upgrades } = require("hardhat");

async function main() {
  // TODO Check this address is right before deploying.
 const deployedProxyAddress = "<<< YOUR PROXY CONTRACT ADDRESS HERE >>>";

 const PriceFeedTrackerV2 = await ethers.getContractFactory(
 "PriceFeedTrackerV2"
  );
 console.log("Upgrading PriceFeedTracker...");

  await upgrades.upgradeProxy(deployedProxyAddress, PriceFeedTrackerV2);
 console.log("PriceFeedTracker upgraded");
}

main(); 

```

然后我们可以用运行脚本

```
yarn hardhat run --network goerli scripts/upgrade_pricefeedtracker.js
```

我们应该会看到类似的输出

```
Compiled 2 Solidity files successfully
Upgrading PriceFeedTracker...
PriceFeedTracker upgraded
```

注意代理地址不变。但是，如果您返回到 Etherscan 并查看您的代理契约发出的事件，您应该会看到一个新的“升级”事件和一个新的实现契约地址。

如果您的合同需要很长时间才能部署，请向下滚动到本博客的故障排除部分。

现在让我们使用安全帽控制台与升级后的合同进行交互。

运行以下命令，一次一个。我建议在你请求价格后离开 60-90 秒，然后再检查 `price` 状态变量。

```
> var V2 = await ethers.getContractFactory("PriceFeedTrackerV2")
undefined

> var v2 = await V2.attach(///// INSERT PROXY CONTRACT ADDRESS /////)
undefined

// ETH/USD
> var ethusdTx = await v2.retrievePrice('0xD4a33860578De61DBAbDc8BFdb98FD742fA7028e') 
undefined

// Wait about 60-90 seconds then read the updated state variable.
> (await v2.price())
BigNumber { value: "150701000000" } 
// Change to LINK/ETH
> var linkEthTx = await v2.retrievePrice('0xb4c4a493AB6356497713A78FFA6c60FB53517c63')

// Wait about 60-90 seconds then read the updated state variable.
> (await v2.price())
BigNumber { value: "4659009800000000" }
```

您会注意到，我们更新了 `price` 变量，以存储从 ETH/USD 价格提要聚合器合同中检索到的价格，然后再从 LINK/ETH 价格提要中检索到的价格。

这就是你想要的！您刚刚升级了您的逻辑契约，并且您与之交互的契约(代理契约)没有发生变化！代理契约将逻辑函数调用委托给向代理契约注册为最新逻辑契约的逻辑契约！

#### 故障排除

在 Goerli 网络上运行带有可升级合同的交易时，可能会出现一些问题。我写这篇博客时遇到的一个问题是，我的事务被卡在了 mempool 中。这是因为从我的钱包里发出的气体少于当时网络所需的气体——在撰写本文时，Goerli 上有气体峰值。没有错误提示发生了这种情况，所以我花了一段时间才弄明白！我用 [炼金术](https://alchemy.com) 作为我的 RPC 提供者连接到 Goerli，于是我找到了 [这个视频](https://www.youtube.com/watch?v=MhtJLUl51gE) 帮我解封。我创建了 [这个脚本](https://gist.github.com/zeuslawyer/541c941b71df7bba128665d9f7e328bf) 作为一个 Hardhat 脚本运行，它帮助我清除了我的 mempool 事务。

另外，请注意，在任何改变区块链状态的交易之后，最好等待大约 60 秒。例如，在运行`retrievePrice()`之后过早地从 `price` 存储变量读取将从区块链返回较旧的数据，因为状态改变写事务可能还没有被块确认。

# 结论

我们已经介绍了如何升级智能合约，为什么我们想要升级，以及围绕升级智能合约的新兴实践是什么。我们学习了一些设计模式，一些可能会让您出错的问题，还运行了一些代码来部署和升级一个智能合约，该合约使用来自 Chainlink 价格源的数据。如果你关注这个博客有困难，请随时 [发微博给我](https://twitter.com/@zubinpratap) 。

访问[chain . link](https://chain.link)或阅读[docs . chain . link](https://docs.chain.link)上的文档，了解更多关于 Chainlink 的信息。要讨论集成，请联系专家。````