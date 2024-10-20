# 如何使用 Hardhat 在 Etherscan 上验证智能合约

> 原文：<https://blog.chain.link/how-to-verify-smart-contract-on-etherscan-hardhat/>

在很大程度上，由于部署到通用区块链的智能合约的不可更改性，安全性始终是用户和企业的第一要务。因此，在以太坊上开发智能合约的一个关键步骤是在初始部署后进行以太扫描验证。Etherscan 使任何人，从用户到有经验的开发人员和 bug 猎人，都能检查代码的有效性、正确性和安全性。

在之前的文章中，我们已经了解了如何在 Etherscan 上 [读取智能合约，以及如何使用 Remix IDE](https://blog.chain.link/how-to-read-smart-contract/) 在 Etherscan 上 [验证智能合约。在本教程中，我们的目标是了解如何使用最常用的智能契约开发框架之一—](https://blog.chain.link/how-to-verify-a-smart-contract-on-etherscan/)[hard hat](https://hardhat.org/)来完成验证。

让我们开始吧。

# 创建一个安全帽项目

让我们创建一个新的安全帽项目。 首先，我们要检查安装在我们机器上的 npm 版本。打开你的终端，输入:  

```
npm -v
```

如果你没有安装 npm，就按照本指南[](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)。然后，输入以下命令来安装 Hardhat:

```
npm install --save-dev hardhat
```

如果你用 [纱](https://yarnpkg.com/getting-started/install) 代替 npm，输入:

```
yarn add --dev hardhat
```

如果使用的是 Windows，强烈建议使用 [WSL 2](https://learn.microsoft.com/en-us/windows/wsl/about) 。

要创建示例项目，在您的项目文件夹中运行以下命令，然后选择“创建一个 TypeScript 项目”:

```
npx hardhat
```

![Screenshot of Welcome to Hardhat](img/879bb057d899c277f10d2a7a55a51deb.png)

# 开发智能合同

如果前面的步骤工作正常，你现在应该可以看到三个主要的安全帽文件夹:“合同”、“测试”和“脚本”。转到“contracts”文件夹，创建一个新的 Solidity 文件，并将其命名为“PriceFeedConsumer.sol”。然后，复制以下源代码，摘自 [Chainlink 官方文档](https://docs.chain.link/) 。

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract PriceConsumerV3 {

 AggregatorV3Interface internal priceFeed;

 /**
 * Network: Goerli
 * Aggregator: ETH/USD
 * Address: 0xD4a33860578De61DBAbDc8BFdb98FD742fA7028e
 */
 constructor(address priceFeedAddress) {
 priceFeed = AggregatorV3Interface(priceFeedAddress);
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
}
```

现在通过运行下一个命令安装@chainlink/contracts 包:

```
npm install --save-dev @chainlink/contracts
```

之后，通过运行编译我们的智能合同

```
npx hardhat compile
```

# 选项 1:使用部署脚本中的 hardhat-etherscan 插件验证您的合同

使用 Hardhat，您可以使用[hard hat-Etherscan](https://hardhat.org/hardhat-runner/plugins/nomiclabs-hardhat-etherscan)插件在 ethers can 上验证您的智能合约。

要开始使用，您需要一个 Etherscan API 密钥。要获得一个，请前往 [以太扫描网站](https://etherscan.io/login) ，免费创建一个新帐户并登录。之后，单击“API 密钥”选项卡。最后，单击“Add”按钮生成新的 API 密钥。

我们将把我们的智能合同部署到 Goerli 测试网络中。如果您以前从未这样做过，您可能想知道为了从 Hardhat 部署智能契约，您必须提供您的钱包的私钥和 JSON RPC URL。可以免费报名领取一把 [炼金术](https://www.alchemy.com/) 钥匙。

你还需要一些测试 ETH，你可以从 [链环龙头](https://faucets.chain.link/) 中轻松获得。

导航回到您的 Hardhat 项目。修改“hardhat.config.ts”文件: 

```
export default {
 // rest of the config
 networks: {
 hardhat: {},
 goerli: {
 url: `https://eth-goerli.alchemyapi.io/v2/${ALCHEMY_API_KEY}`,
 accounts: [GOERLI_PRIVATE_KEY],
 },
 },
 etherscan: {
 apiKey: "ABCDE12345ABCDE12345ABCDE123456789", // Your Etherscan API key
 },
};

```

在“scripts”文件夹中创建新文件，并将其命名为“deployPriceFeedConsumer.ts”。该脚本将部署 PriceFeedConsumer.sol 智能合约，等待由于安全原因而被包含在链中的几个块，并尝试在 Etherscan 上验证它。

```
import { ethers, network, run } from "hardhat";

async function main() {
  const priceFeedAddress = “0xD4a33860578De61DBAbDc8BFdb98FD742fA7028e”;

  const priceFeedConsumerFactory = await ethers.getContractFactory(“PriceConsumerV3”);
 const priceFeedConsumer = await priceFeedConsumerFactory.deploy(priceFeedAddress);

 const WAIT_BLOCK_CONFIRMATIONS = 6;
  await priceFeedConsumer.deployTransaction.wait(WAIT_BLOCK_CONFIRMATIONS);

  console.log(`Contract deployed to ${priceFeedConsumer.address} on ${network.name}`);

  console.log(`Verifying contract on Etherscan...`);

 await run(`verify:verify`, {
 address: priceFeedConsumer.address,
 constructorArguments: [priceFeedAddress],
 });
}

main().catch((error) => {
 console.error(error);
 process.exitCode = 1;
});
```

保存文件并从终端运行下一个命令:

```
npx hardhat run scripts/deployPriceFeedConsumer.ts --network goerli
```

您的合同现在应该部署到 Goerli testnet，并在 Etherscan explorer 上验证。

# 选项 2:从您的 CLI 使用 hardhat-etherscan 插件验证您的合同

我们将再次使用[hard hat-etherscan](https://hardhat.org/hardhat-runner/plugins/nomiclabs-hardhat-etherscan)插件来验证我们的智能合约。

  要入门，去 [以太扫描](https://etherscan.io/login) 注册一个账号。在您的帐户设置下，找到“API 密钥”部分。使用 Free 计划生成一个 API 密钥。

我们将再次将我们的智能合同部署到 Goerli 测试网络。如果需要测试令牌，请访问 [链环龙头](https://faucets.chain.link/) 。

修改“hardhat.config.ts”文件:

```
export default {
 // rest of the config
 networks: {
 hardhat: {},
 goerli: {
 url: `https://eth-goerli.alchemyapi.io/v2/${ALCHEMY_API_KEY}`,
 accounts: [GOERLI_PRIVATE_KEY],
 },
 },
 etherscan: {
 apiKey: "ABCDE12345ABCDE12345ABCDE123456789", // Your Etherscan API key
 },
};

```

在“scripts”文件夹中创建新文件，并将其命名为“deployPriceFeedConsumer.ts”。这将部署 PriceFeedConsumer.sol 智能契约，并等待出于安全原因将几个块包含在链中。

```
import { ethers, network } from "hardhat";

async function main() {
  const priceFeedAddress = “0xD4a33860578De61DBAbDc8BFdb98FD742fA7028e”;

  const priceFeedConsumerFactory = await ethers.getContractFactory(“PriceConsumerV3”);
  const priceFeedConsumer = await priceFeedConsumerFactory.deploy(priceFeedAddress);

 const WAIT_BLOCK_CONFIRMATIONS = 6;
 await priceFeedConsumer.deployTransaction.wait(WAIT_BLOCK_CONFIRMATIONS);

 console.log(`Contract deployed to ${priceFeedConsumer.address} on ${network.name}`);
}

main().catch((error) => {
 console.error(error);
 process.exitCode = 1;
});
```

使用以下命令部署您的智能合约:

```
npx hardhat run scripts/deployPriceFeedConsumer.ts --network goerli
```

我们现在将使用 Hardhat 的“验证”任务从 CLI 验证 Etherscan 上的智能合约。该命令的一般语法如下:  

```
npx hardhat verify --network <network> <contract address> <constructor parameters>
```

我们将通过以下方式进行调整:

```
npx hardhat verify --network goerli <contract address> 0xD4a33860578De61DBAbDc8BFdb98FD742fA7028e
```

你应该可以在 Etherscan 上看到我们合同的公开验证源代码的链接。如果您得到一个错误，说地址没有字节码，这可能意味着 Etherscan 还没有索引您的合同。在这种情况下，请等待一分钟，然后再试一次。

# 选项 3:使用安全帽展平任务验证您的合同

使用 Hardhat 进行 Etherscan 验证的第三个选项类似于通过 Remix IDE 进行验证的过程，在我们之前的一篇 [博文](https://blog.chain.link/how-to-verify-a-smart-contract-on-etherscan/) 中有所描述。

我们再次部署到 Goerli 测试网络，如果您需要测试令牌，请导航到[](https://faucets.chain.link/)。你不需要一个 Etherscan API 密匙。

你的“hardhat.config.ts”文件应该是这样的:  

```
export default {
 // rest of the config
 solidity: "0.8.9",
 networks: {
 hardhat: {},
 goerli: {
 url: `https://eth-goerli.alchemyapi.io/v2/${ALCHEMY_API_KEY}`,
 accounts: [GOERLI_PRIVATE_KEY],
 },
 }
};
```

我们将重用上一章的部署脚本:

```
import { ethers, network } from "hardhat";

async function main() {
  const priceFeedAddress = “0xD4a33860578De61DBAbDc8BFdb98FD742fA7028e”;

  const priceFeedConsumerFactory = await ethers.getContractFactory(“PriceConsumerV3”);
 const priceFeedConsumer = await priceFeedConsumerFactory.deploy(priceFeedAddress);

 const WAIT_BLOCK_CONFIRMATIONS = 6;
  await priceFeedConsumer.deployTransaction.wait(WAIT_BLOCK_CONFIRMATIONS);

 console.log(`Contract deployed to ${priceFeedConsumer.address} on ${network.name}`);
}

main().catch((error) => {
 console.error(error);
 process.exitCode = 1;
});
```

运行部署脚本:

```
npx hardhat run scripts/deployPriceFeedConsumer.ts --network goerli
```

如果您在 Etherscan 上搜索您的合同地址，当您点击合同标签时，您将只能看到合同的字节码。

![Screenshot of Etherscan contract](img/1bccbb4387b96c595134b9790aa5fca8.png)

要开始验证过程，请点击“验证并发布”链接。将显示以下页面。

![Screenshot of Etherscan](img/501352087c9734361c45e739bdc894ad.png)

在第一个输入字段中输入您的合同地址(如果默认情况下尚未填写)。

然后，从“编译器类型”下拉菜单中，选择“可靠性(单个文件)”。

之后，会出现“编译器版本”下拉菜单。在这里，您需要选择在部署之前用于编译这个智能契约的相同 Solidity 编译器版本。如果你回头看“hardhat.config.ts”文件，你可以看到在我们的例子中，那是 0.8.9 版本。

最后，从“开源许可类型”下拉列表中，选择 Solidity 文件开头指定的许可，命名为“SPDX-License-Identifier”，在我们的例子中为 MIT。点击“继续”进入下一页。

在接下来的页面上，你应该粘贴智能合同的源代码。不幸的是，如果你已经像我们一样导入了其他契约或接口，你就不能在这里简单地复制粘贴了。Etherscan 还需要知道那些导入的契约的源代码。为此，您需要通过键入以下命令来“展平”您的智能契约:  

```
npx hardhat flatten
```

智能合同的“展平”版本将在终端中打印出来。或者，您可能希望将它保存在一个单独的文件中，这可以通过键入:来完成

```
npx hardhat flatten contracts/PriceFeedConsumer.sol > cotracts/PriceFeedConsumer_flat.sol
```

现在您可以将合同的源代码粘贴到“在下面输入可靠性合同代码”输入框中。然后，解决验证码，并点击蓝色的“验证和发布”按钮。您应该可以在 Contract 选项卡上看到绿色复选标记。这意味着您已经成功验证了您的合同。

# 结论

在本文中，我们介绍了如何使用三种不同的方法在 Hardhat 的 Etherscan 上验证智能合约。智能契约验证是部署过程中的关键步骤之一，因为它允许社区在使用源代码之前检查源代码。

访问[chain . link](https://chain.link/)或阅读 docs.chain.link 上的文档，了解有关 Chainlink 的更多信息。要讨论集成，请联系专家。