# 如何通过三个步骤构建 dApp

> 原文：<https://blog.chain.link/how-to-build-a-dapp/>

分散式应用程序，或 dApps，是不依赖于中央服务器或后端的应用程序，而是利用 Web3 技术，如 [【区块链】](https://blog.chain.link/what-is-blockchain/) 和[Oracle](https://chain.link/education/blockchain-oracles)来包含它们的逻辑和后端功能，使它们防篡改和安全。

在本技术教程中，您将学习如何创建一个简单的端到端 dApp，允许用户在智能合约中检索和存储以太坊的当前价格。 [完成的 demo](https://github.com/pappas999/chainlink-dapp-tutorial) 可以在 GitHub 上找到。

## 要求

请确保您安装了以下软件:

*   [【nodejs】](https://nodejs.org/)
*   [MetaMask](https://metamask.io/)

## 什么是分散式应用？

与后端代码运行在集中式服务器上的传统应用程序相反，dApp 的后端代码运行在区块链上。dApp 可以拥有以任何语言编写的前端代码和用户界面，并部署在任何服务器上，以与后端逻辑进行交互。

由于将后端逻辑置于高度安全、防篡改的 [智能合约](https://chain.link/education/smart-contracts) 中，dApps 可以享受传统 Web2 系统无法实现的诸多优势:

*   零停机时间
*   增强隐私
*   审查阻力
*   逻辑的信任最小化执行

然而，这些好处也伴随着一些缺点。dApps 的维护更加复杂，因为部署到区块链的代码在默认情况下是不可修改的。由于通过分布式网络而不是集中式服务器运行逻辑，还会产生性能开销。除此之外，用户体验也会受到影响，因为 dApp 用户需要经历拥有 Web3 钱包并为其提供足够的加密货币来支付交易费用的复杂性。

## dApp 的组件

dApp 的组件可以分为三个不同的类别:智能合约、前端逻辑和用户界面以及数据存储。

### 智能合约

智能合约存储 dApp 的业务逻辑以及应用程序的状态。这是 dApp 和传统 web 应用程序的最大区别，也是 dApp 拥有上述所有优势的原因。

### 前端/用户界面

虽然 dApp 的后端逻辑要求开发人员编写要在区块链上部署的智能合约代码，但 dApp 的前端或客户端可以使用标准的 web 技术，如 HTML 和 JavaScript。这允许开发人员使用熟悉的工具、库和框架。客户端用户界面通常通过 [Web3.js](https://web3js.readthedocs.io/en/v1.7.4/) 或[ethers . js](https://docs.ethers.io/v5/)等客户端库链接到智能合约，与前端资源捆绑在一起，随 UI 一起发送到浏览器。与智能合约的交互，如签署消息和向智能合约发送交易，通常通过基于浏览器的 Web3 wallet 进行，如[meta mask](https://metamask.io/)。

### 数据存储

大多数应用程序都需要存储数据，但是由于区块链的分布式特性，在链上存储大量数据是不可行的，而且会非常昂贵。这就是为什么许多需要存储数据的 dApps 使用链外数据存储服务，如[【IPFS】](https://ipfs.io/)或[Filecoin](https://filecoin.io/)，而让区块链只存储关键的业务逻辑和状态。

您也可以使用传统的基于云的存储服务。然而，许多开发人员选择分散选项来维护和扩展区块链驱动的 dApp 提供的信任最小化属性。

![Diagram of Ethereum dApp architecture](img/19337b26048d1b66a725faf23fafc396.png)

<figcaption id="caption-attachment-4156" class="wp-caption-text">Ethereum dApp Architecture. Source: [The Architecture of a Web3 Application](https://www.preethikasireddy.com/post/the-architecture-of-a-web-3-0-application)</figcaption>



现在我们已经知道了 dApp 的组件，让我们来看一个构建简单的端到端示例的例子。

## 第一步:创建智能合同

我们 dApp 中的智能合约将是一个简单的例子，用于查找数据并反映区块链上的状态变化。在这种情况下，我们将使用 [ETH/USD Chainlink 数据馈送](https://data.chain.link/ethereum/mainnet/crypto-usd/eth-usd) 查找 ETH/USD 的值，然后将结果永久存储在智能合约中。

第一步是打开我们的文档，使用数据馈送 页面进入 [。您可以从那里复制示例源代码并将其粘贴到您选择的 IDE 中的一个新文件中(例如](https://docs.chain.link/docs/get-the-latest-price/) [可视代码](https://code.visualstudio.com/) )，或者您可以按下“在 Remix 中打开”按钮并从 Remix 的 web 版本中工作。

在这个例子中，我们将使用 Visual Studio 代码和以太坊虚拟机开发框架[](https://hardhat.org/)。

首先，我们将为 dApp 创建一个新的目录结构，并为智能合同代码创建一个后端文件夹:

```
mkdir chainlink-dapp-example
cd chainlink-dapp-example
mkdir backend
cd backend
```

接下来，我们将在 VS 代码编辑器中打开为 dApp 创建的目录，然后安装 Hardhat:

```
npm init -y
npm install --save-dev hardhat
npx hardhat 
(choose create javascript project, choose default parameters)
```

完成后，删除“合同”文件夹中的`Touch.sol`文件，在该文件夹中创建一个名为`PriceConsumerV3.sol`的新文件，然后保存。这是我们将创建智能契约的地方，所以将 Chainlink docs 示例中的代码复制到这个文件中并保存它。

在示例代码中，您将看到演示合同已经有了一个函数`getLatestPrice`，用于在 Rinkeby ETH/USD 数据提要上查找以太坊的当前价格。

```
    function getLatestPrice() public view returns (int) {
        (
            /*uint80 roundID*/,
            int price,
            /*uint startedAt*/,
            /*uint timeStamp*/,
            /*uint80 answeredInRound*/
        ) = priceFeed.latestRoundData();
        return price;

```

我们需要创建一个新变量和一个新函数来存储智能合约上的值。第一步是在现有的`priceFeed`下创建一个新变量来存储以太坊的价格:

```
    int public storedPrice;
```

接下来，我们需要创建一个可以被 dApp 前端调用的新函数。该函数应该通过调用现有的`getLatestPrice`函数来查找以太坊的最新价格。那么它应该将该值存储在新的`storedPrice`参数中:

```
    function storeLatestPrice() external {
        storedPrice = getLatestPrice();
    }
```

你的新合同应该是这样的:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract PriceConsumerV3 {

    AggregatorV3Interface internal priceFeed;
    int public storedPrice;

    /**
     * Network: Rinkeby
     * Aggregator: ETH/USD
     * Address: 0x8A753747A1Fa494EC906cE90E9f37563A8AF630e
     */
    constructor() {
        priceFeed = 
AggregatorV3Interface(0x8A753747A1Fa494EC906cE90E9f37563A8AF630e);
    }

    /**
     * Returns the latest price
     */
    function getLatestPrice() public view returns (int) {
        (
            /*uint80 roundID*/,
            int price,
            /*uint startedAt*/,
            /*uint timeStamp*/,
            /*uint80 answeredInRound*/
        ) = priceFeed.latestRoundData();
        return price;
    }

    function storeLatestPrice() external {
        storedPrice = getLatestPrice();
    }
}
```

## 第二步:部署智能合约

现在，您已经准备好编译您的合同并将其部署到 Rinkeby 测试网络。确保先用一些 Rinkeby ETH 为你的 MetaMask 钱包 充值 [。](https://faucets.chain.link/)

如果您正在使用 Remix，您可以使用标准的 Remix 流程来编译和部署您的合同。如果你使用像 Visual Studio 代码这样的 IDE，我们建议你使用 Hardhat 来管理你的合同。

编译和部署合同的第一步是安装 Hardhat 工具库、Chainlink 合同库和 dotenv 库，用于将密码和敏感密钥存储在单独的。环境文件:

```
npm install --save-dev @nomicfoundation/hardhat-toolbox
npm install @chainlink/contracts --save
npm install dotenv
```

接下来，用以下内容替换`hardhat-config.js`文件的内容:

```
require("@nomicfoundation/hardhat-toolbox");

//require("@nomiclabs/hardhat-ethers")
 require('dotenv').config()

 const RINKEBY_RPC_URL = process.env.RINKEBY_RPC_URL || 
"https://eth-rinkeby.alchemyapi.io/v2/your-api-key"
 const PRIVATE_KEY = process.env.PRIVATE_KEY || "abcdef"

 module.exports = {
     defaultNetwork: "rinkeby",
     networks: {
         hardhat: {
             // // If you want to do some forking, uncomment this
             // forking: {
             // url: MAINNET_RPC_URL
             // }
         },
         localhost: {
         },
         rinkeby: {
             url: RINKEBY_RPC_URL,
             accounts: [PRIVATE_KEY],
             saveDeployments: true,
         },
     },

  solidity: "0.8.9",
};
```

下一步是在你的`backend folder`中创建一个`.env`文件。然后您需要 [从您的 Web3 钱包](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-export-an-account-s-private-key) 中提取您的私钥，并将其粘贴到。环境文件。请确保您使用的新 Web3 钱包在 mainnet 上没有任何资金。

完成后，您需要获得一个 RPC 端点来访问 Rinkeby 网络。您可以通过将 RPC URL 粘贴到。环境文件。我们推荐注册一个免费的 [Infura](https://infura.io/) 或[Alchemy](https://www.alchemy.com/)账号来获得一个 RPC URL。

![Creating the .env fi](img/30beef9fe51addd2740b88dce54fd596.png)

<figcaption id="caption-attachment-4156" class="wp-caption-text">Creating the .env file</figcaption>



下一步是修改“脚本”文件夹中的`deploy.js`文件的内容，以确保它将部署您的新合同。打开文件，确保下面的代码替换了已经存在的代码。这将简单地获取您编译的 PriceConsumerV3 契约，并尝试部署它。请记住保存您的更改。

```
// We require the Hardhat Runtime Environment explicitly here. This is optional
// but useful for running the script in a standalone fashion through `node <script>`.
//
// You can also run a script with `npx hardhat run <script>`. If you do that, Hardhat
// will compile your contracts, add the Hardhat Runtime Environment's members to the
// global scope, and execute the script.
const hre = require("hardhat");

async function main() {

  const PriceConsumer = await hre.ethers.getContractFactory("PriceConsumerV3");
  const priceConsumer = await PriceConsumer.deploy();

  await priceConsumer.deployed();

  console.log("Contract deployed to:", priceConsumer.address);
}

// We recommend this pattern to be able to use async/await everywhere
// and properly handle errors.
main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

现在，您已经准备好使用 Hardhat 编译您的智能合同并将其部署到 Rinkeby 网络:

```
npx hardhat compile
npx hardhat run --network rinkeby scripts/deploy.js
```

您应该会看到类似下面的消息，显示您的智能合约部署到的 Rinkeby 上的地址。记下这个地址，我们下一步会用到它。

![Screenshot of deployed smart contract](img/c720c4a9e7d263fe9b520b3b78cb2944.png)

<figcaption id="caption-attachment-4159" class="wp-caption-text">Deployed smart contract.</figcaption>



祝贺您，您现在已经准备好进入 dApp 的前端部分了！

## 第三步:创建前端应用

您的 dApp 的前端逻辑和用户界面可以使用各种不同的框架来构建。

[React](https://reactjs.org/) 是用于构建功能丰富的 web 用户界面的最流行的 JavaScript 库之一，因此被许多 Web3 dApps 使用。除此之外，[ethers . js](https://docs.ethers.io/v5/)是一个 JavaScript 库，用于连接到基于 EVM 的区块链和智能合约并与之交互。当您将两者结合起来时，您就有了构建 dApp 前端的合理起点。

在本节中，我们将使用[create-React-app](https://create-react-app.dev/)样板文件生成器创建一个新的 React 应用程序。然后，我们将介绍一些使用 Ethers.js 将用户界面与部署的智能合约连接起来的链外逻辑，为我们提供一个完整的端到端 dApp。

### 创建 React 应用程序

创建前端的第一步是安装和实现 create-react-app 样板项目，然后修改它以适应我们的 dApp。第一步是将库安装到一个新的“前端”文件夹:

```
cd ..
npx create-react-app frontend 
```

完成后，你应该会在你的项目中看到一个新的“前端”文件夹，里面有所有相关的 React 代码。展开“前端”文件夹并执行以下操作:

*   删除/src/setupTests.js
*   删除/src/ReportWebVitals.js
*   【delete/src/logo】SVG㎡t1㎡
*   删除/src/App.test.js
*   删除/src/App.css

文件夹结构应该如下所示:

![Screenshot of React front-end folder structure](img/89f0d1a1f5d79af9a706314ebf6cab1a.png)

<figcaption id="caption-attachment-4160" class="wp-caption-text">React front-end folder structure.</figcaption>



我们现在几乎准备好开始修改 React 应用程序代码了。不过首先一定要安装[Bootstrap](https://getbootstrap.com/)和[ethers . js](https://docs.ethers.io/v5/)的库。Bootstrap 是一个流行的前端 CSS 框架，带有应用 CSS 样式的 React 友好的 UI 小部件，而 Ethers.js 允许我们将前端连接到区块链上部署的智能合同。确保这些命令从“前端”文件夹中运行。

```
cd frontend
npm install bootstrap npm install ethers 
```

现在我们准备修改 React 应用程序代码。打开/src/文件夹中的`App.js`文件并删除内容。我们将从头开始构建它。

第一步是告诉应用我们要使用 React(包括 useEffect 和 useState 库)和 Ethers.js:

```
import React, { useEffect, useState } from 'react';
import { ethers } from "ethers";
```

接下来，创建一个名为“App”的函数并导出:

```
function App() {

}

export default App; 
```

现在我们开始填写“App”功能的内容。向其中添加以下代码。该代码执行以下操作:

*   设置 storedPrice 和 setStoresPrice react 挂钩。
*   创建与您的 MetaMask Web3 钱包的连接。
*   设置已部署的智能合约地址和 ABI。Ethers.js 需要这两者来与部署的智能契约进行交互。
    *   智能合约地址可以从本指南前面的部署步骤中获得。将此值插入到 **替换 _ 替换 _ 已部署 _ 合同 _ 地址** 字符串中。
    *   智能合约 ABI 可以从/back end/artifacts/contracts/priceconserv 3 . JSON 文件的`abi`元素中获得。您可以使用一个 [代码精简器](https://codebeautify.org/jsonminifier) 以更好的方式将其格式化，以便存储在您的应用程序中。

```
  const [storedPrice, setStoredPrice] = useState('');
  const provider = new ethers.providers.Web3Provider(window.ethereum)
  const signer = provider.getSigner()
  const contractAddress = <REPLACE_WITH_DEPLOYED_CONTRACT_ADDRESS>’';
  const ABI = 
'[{"inputs":[],"stateMutability":"nonpayable","type":"constructor"},{"inputs":[],"name":"getLatestPrice","outputs":[{"internalType":"int256","name":"","type":"int256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"storeLatestPrice","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"storedPrice","outputs":[{"internalType":"int256","name":"","type":"int256"}],"stateMutability":"view","type":"function"}]'
  const contract = new ethers.Contract(contractAddress, ABI, signer);
```

现在我们将创建两个函数用于我们的应用程序:

*   getStoredPrice 将连接到已部署的智能契约，并获取`storedPrice()` getter 函数的当前值。
*   setNewPrice 将调用部署的智能合约的`storeLatestPrice`函数，等待交易完成，然后调用`getStoredPrice`函数检索智能合约中存储的价格。

我们还将在我们的应用程序函数中添加对`getStoredPrice`的调用，这样它将在页面加载时首先调用 getter 函数:

```
const getStoredPrice = async () => {
    try {
      const contractPrice = await contract.storedPrice();
      setStoredPrice(parseInt(contractPrice) / 100000000);
    } catch (error) {
      console.log("getStoredPrice Error: ", error);
    }
  }

  async function updateNewPrice() {
    try {
      const transaction = await contract.storeLatestPrice();
      await transaction.wait();
      await getStoredPrice();
    } catch (error) {
      console.log("updateNewPrice Error: ", error);
    }

  }

  getStoredPrice()
  .catch(console.error)
```

创建前端的最后一步是让你的应用程序返回 JSX 代码供浏览器渲染。将以下代码粘贴到应用程序函数底部的 getStorePrice()调用下。这段代码执行以下操作:

*   返回一个简单的两列网格布局。
*   第一列包含智能合约中当前存储的 ETH/USD 价格。
*   第二列包含一个按钮，用户可以使用它与智能合约交互并更新存储的价格。按下按钮调用上面的`setNewPrice`功能。

```
  return (
    
      

        
          <h3>Stored Price</h3>
          <p>Stored ETH/USD Price: {storedPrice}</p>
        

        
          <h3>Update Price</h3>
          <button type="submit" className="btn btn-dark" 
onClick={updateNewPrice}>Update</button>
        
      
    
  );
```

你的申请已经准备好了。如果需要，您可以将您的代码与 [完成的示例](https://github.com/pappas999/chainlink-dapp-tutorial) 进行比较，以确保您正确地完成了所有事情。现在你已经准备好运行你的 dApp 了。

### 运行您的 dApp

确保保存了所有文件后，从前端文件夹运行以下命令，在本地启动 dApp:

```
npm run start
```

应用程序加载后，浏览器中会出现一个新窗口，显示您的 dApp 用户界面。您还应该会收到来自 MetaMask 的弹出通知，要求将您的钱包连接到应用程序。

![React frontend](img/bac4aa9d634c895b34fd7c1e52de6029.png)

<figcaption id="caption-attachment-4161" class="wp-caption-text">React frontend.</figcaption>



在您确认您已经通过 Rinkeby ETH 的 [向](https://faucet.chain.link/)meta mask 帐户提供资金后，单击 dApp UI 上的“更新”按钮，与您在 Rinkeby 网络上部署的智能合约进行交互。您应该会收到来自 MetaMask 的通知，要求您确认交易。在你完成这个之后，几秒钟之内，你的 dApp 应该会自动刷新，以太坊的当前价格应该会出现在“存储价格”部分:

![React frontend showing Data Feed result](img/c711f45ffc56632206fffa3f97863065.png)

<figcaption id="caption-attachment-4162" class="wp-caption-text">React frontend showing Data Feed result.</figcaption>



祝贺您，您现在已经成功地创建、部署了一个简单的 dApp 并与之交互！在本指南中，您只是在您的计算机上本地运行前端，但是如果您愿意，您可以将它部署到基于云的服务器上，或者甚至将前端分散部署到[【IPFS】](https://ipfs.io/)！你也可以使用应用程序的 [CSS](https://www.w3schools.com/css/) 来改变用户界面的外观和感觉。

## 总结

分散式应用程序是用区块链和智能合同等 Web3 技术取代传统后端服务器处理的应用程序，为它们提供了传统 Web 应用程序无法提供的独特的安全性和防审查保证。

在这个技术演示中，我们创建了一个简单的 dApp，其中包含一个智能合约，该合约从 ETH/USD Chainlink 数据馈送中获取最新价格，并将结果存储在智能合约中。然后，我们创建了一个简单的 UI，它利用 React 和 Ethers.js 连接到已部署的智能契约并与之交互。

访问[chain . link](https://chain.link/)或阅读[docs . chain . link](https://docs.chain.link/)上的文档，了解更多关于 Chainlink 的信息。您还可以订阅 [Chainlink 简讯](https://chn.lk/newsletter) 以了解 Chainlink 堆栈中的最新信息。 [要讨论一个整合，就要求助于专家 。T25】](https://chainlinkcommunity.typeform.com/to/OYQO67EF?typeform-source=blog.chain.link)