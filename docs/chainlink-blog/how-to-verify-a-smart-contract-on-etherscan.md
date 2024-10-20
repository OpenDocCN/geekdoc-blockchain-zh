# 如何在 Etherscan 上验证智能合同

> 原文：<https://blog.chain.link/how-to-verify-a-smart-contract-on-etherscan/>

被称为 Web3 的互联网去中心化新愿景的美妙之处在于，任何人都可以与部署在通用区块链上的智能合约进行交互。正如你可能已经知道的，智能合同是在区块链上运行的计算机程序，它的源代码是公开的，任何人都可以验证，而且，正如所说，任何人都可以与它们进行交互，而不需要基于网络的界面。这可以通过运行区块链客户端并使用命令行界面(CLI)创建事务来实现。

Etherscan 介于 web 或移动应用程序和用于与智能合约交互的 CLI 之间，是一个用于各种区块链网络的块浏览器，如以太坊、多边形、Arbitrum、乐观等等。如果你对如何在以太网扫描上与智能合同进行交互感到好奇，可以看看最近这篇关于 [在以太网扫描上阅读智能合同的博文。](https://blog.chain.link/how-to-read-smart-contract/)

也就是说，我们只能在 Etherscan 上与“经过验证的”智能合约进行交互。在本技术教程中，您将学习如何在 Etherscan 上验证智能合约。

## 单一实体文件的验证

从验证流程开始，我们需要首先部署智能合约。导航到 [Remix IDE](https://remix.ethereum.org/) ，新建一个名为“Counter.sol”的文件。粘贴下面的代码:

```
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

contract Counter {
 uint256 internal counter;
 function increment() external {
 unchecked {
 ++counter;
 }
 }

 function getCurrent() external view returns(uint256) {
 return counter;
 }
}
```

在部署之前，我们必须注意我们用于编译该合同的 Solidity 编译器的版本，以及在文件顶部作为“SPDX-License-Identifier”提供的合同许可证。

我们在合同文件里面规定了可以用 0.8.0 到 0.9.0 之间的任何 Solidity 编译器版本进行编译，包含 0.8.0、0.8.1、0.8.2 等多个版本。

进入“Solidity 编译器”选项卡，选择 Solidity 编译器版本(记住，可以是任何 0.8 版本)，点击“编译 Counter.sol”。对于这个例子，我们将使用 0.8.7 编译器版本。

![Using Remix Solidity compiler for Counter contract](img/20f6bead576f88dd81c7116263dcf8f0.png)

编译成功后，导航到当前选项卡正下方的“部署&运行事务”选项卡。从“环境”下拉菜单中，选择“注入的提供者-元掩码”，这将自动显示一个元掩码弹出窗口，以将您的钱包连接到 Remix IDE 网站。之后，选择您希望将合同部署到的区块链网络。

我们将向 Rinkeby 部署此合同，因此我们需要在 MetaMask wallet 中选择“Rinkeby Test Network”。为了部署合同，我们还需要一些乙醚测试试剂。你可以从 [链式水龙头](https://faucets.chain.link/) 中免费抽取一些，只需将你的钱包连接到水龙头上。确保右上角下拉列表中选择的网络是以太坊 Rinkeby。

![Switching to Injected Provider on Remix](img/95497cf7b54a5e08aedfe50264180d39.png)

最后，点击橙色的“部署”按钮，在 MetaMask wallet 内签署交易。等待大约 15 秒钟，直到您的交易被确认。你现在可以通过 Remix IDE UI 与你的智能合约进行交互，但这不是重点，因为我们希望允许任何人使用它。

如果我们在 Etherscan 上跟踪我们的合同，简单地通过跟踪最后的交易散列或通过将合同的地址粘贴到 Etherscan 的搜索栏中，当点击合同选项卡时，我们将只看到合同的字节码。这意味着我们需要在 Etherscan 上“验证”我们的智能合同，以便通过这个 block explorer 使用它。

![Verify and publish button on Etherscan](img/9d0063548f056fb908363e29636d7d6b.png)

要开始验证过程，请点击“验证并发布”蓝色超链接文本。将显示以下页面。

![Verifying and publishing source code](img/589b6ce525c7f6f7098a7cbfb491dd4f.png)

在第一个输入字段中输入您的合同地址(如果默认情况下尚未填写)。然后从“编译器类型”下拉列表中，选择“可靠性(单个文件)”。之后，将显示“编译器版本”下拉列表。在这里，我们需要选择与部署之前用于编译这个智能契约的相同的 Solidity 编译器版本——在我们的例子中，是 0.8.7 版本。最后，从“开源许可类型”下拉列表中，选择 Solidity 文件开头指定的许可为“SPDX-License-Identifier”。在我们的例子中，那是麻省理工学院。单击继续转到下一页。

![Entering a Solidity contract code to Etherscan](img/1f506e3c32c81e55d61c99c0bed28efa.png)

将合同的源代码粘贴到“在下面输入可靠性合同代码”输入框中，求解验证码，点击蓝色的“验证并发布”按钮。 您现在应该可以看到合同选项卡上的绿色对勾。这意味着契约得到了验证，我们现在可以与它进行交互。

![Viewing the verified contract source code](img/a1bf3a5831913bc741c747eaf1e6eb72.png)

如果你点击“阅读合同”按钮，你应该能够调用“getCurrent”函数，并看到我们的计数器变量的当前值，该值默认为零。

![Reading the getCurrent function on Etherscan](img/1e7fe610e7ddd5fb35dbc1e05f5bc5a4.png)

如果您点击“写合同”按钮，您应该能够将您的钱包连接到 Etherscan 网站，并调用我们的“增量”功能。点击按钮后会弹出 MetaMask 进行交易签名(记住需要在 Rinkeby 网络上)。在您的事务被成功地包含在一个块中之后，您可以返回到“Read Contract”部分并再次调用“getCurrent”函数来验证“counter”值现在是 1。

![Writing to the increment function on Etherscan](img/df41d4f6ff0a3fc98c75829ac6099c8f.png)

## 使用拼合插件验证多个实体文件

我们刚刚看到了智能合同的验证流程是如何在 Etherscan 上运行的。该示例向我们展示了如何对单个实体文件执行此操作，但情况并非总是如此。实际上，您的智能合约通常会导入其他合约、接口或库。

让我们以 Chainlink Price Feed 消费者合同为例。创建一个新的实体文件，命名为“PriceFeedConsumer.sol”，从 [官方 Chainlink 文档](https://docs.chain.link/docs/get-the-latest-price/) : 中粘贴以下代码

```
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.7;
import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract PriceConsumerV3 {
 AggregatorV3Interface internal priceFeed;
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
}
```

Line " import " @ chain link/contracts/src/v 0.8/interfaces/aggregator v3 interface . sol "意味着我们正在从另一个文件导入实体界面。接口本身并不是智能合约，而是用于列出相关的方法，而没有实现函数体。接口由“interface”关键字声明。接口既可以由实现所有列出的方法的智能协定继承，也可以用于调用实现了这些列出的功能的其他协定的方法。在本例中，我们使用后一个示例来调用 Chainlink 聚合器契约上的“latestRoundData”函数。

让我们用 0.8.7 Solidity 编译器版本再次部署这个契约。许可证又是 MIT，从我们的智能合约第一行就能看出来。

成功部署后，导航回 Remix IDE 文件浏览器。找到“PriceFeedConsumer.sol”，点击右键，然后点击“展平”。

![Where to find flatten on Remix](img/8569127bd8feee5ab117aabb30a42860.png)

该命令将生成名为“PriceFeedConsumer _ flat.sol”的新文件，并用实际导入的合同、接口或库的源代码替换所有的导入。

![Adding the flattener extension to Remix](img/fed9b5dbef35795ca87f7aaddd97af1a.png)

注意 Remix IDE 的“拼合”扩展，它会自动激活。扁平化契约的第二种方法是通过单击左下角的“扩展”按钮(在“设置”按钮上方，看起来像一个电源插头)并单击“扁平化器”扩展旁边的绿色“激活”按钮来激活该扩展。

![Finding the Plugin Manager in Remix](img/635b43540cc3288d9194e72724584095.png)

然后，转到拼合扩展选项卡，点击“拼合 PriceFeedConsumer.sol”按钮。请注意，此操作不会创建新文件，而是将展平的源代码复制到剪贴板，因此我们可以将其粘贴到 Etherscan 验证页面。

选择这两种扁平化方法中的哪一种取决于你。

现在，如前一章所述，当您进入以太扫描验证页面时，选择:

*   对于编译器类型—可靠性(单个文件)
*   对于编译器版本—v 0 . 8 . 7+commit . e 28d 00 a 7
*   对于开源许可证类型—麻省理工学院许可证(MIT)

然后点击“继续”按钮。

在接下来的页面上，在“在下面输入可靠性合同代码”文本框内，粘贴“PriceFeedConsumer _ flat.sol”文件或剪贴板的内容，具体取决于您用于展平合同的方法。

再次求解验证码，点击“验证并发布”按钮。

## 使用以太扫描插件验证多个 Solidity 文件

由多个 Solidity 文件组成的合同验证的另一种方法是使用“ethers can–合同验证”Remix IDE 插件。

我们将使用已经写好的“PriceFeedConsumer.sol”合同。再次部署它。之后，从扩展选项卡中激活“以太扫描-合同验证”插件。

![Finding Etherscan contract verification plugin on Remix](img/eee70506aa93fa7a4fb6f7218e70b78f.png)

现在去 [以太扫描](https://etherscan.io/register) 注册账号。在您的帐户设置下，找到“API 密钥”部分。使用 Free 计划生成一个 API 密钥。

然后，导航回 Remix IDE，点击“ethers can–Contract Verification”选项卡，将您的 API 密钥粘贴到那里。单击“保存 API 密钥”按钮。

![How to save Etherscan API key on Remix](img/4ef3c5170fd90212395c27460bfda08a.png)

然后，选择您想要验证的合同，并提供其合同地址。点击“验证合同”。就这样，您的合同现在应该在 Etherscan 上得到验证。

![Finalizing contract verification on Remix using Etherscan plugin](img/56581d5a4aef0a4f7959e859580f0d07.png)

## 结论

在本文中，您了解了如何使用各种方法在 Remix IDE 的 Etherscan 上验证智能合约。

访问[chain . link](https://chain.link/)或阅读[docs . chain . link](https://docs.chain.link/)上的文档，了解更多关于 Chainlink 的信息。

讨论一个整合， [联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF?typeform-source=blog.chain.link) 。