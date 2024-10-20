# 如何创建一个具有可靠性的“Hello World”智能契约

> 原文：<https://blog.chain.link/how-to-create-a-hello-world-smart-contract-with-solidity/>

成为专业智能合同开发人员的旅程始于一步。

在本教程中，您将学习如何使用智能合约开发语言 Solidity 构建一个“Hello World”智能合约。不需要任何先验知识——本教程是初学者友好的。即使您不是开发人员，也可以按照一步一步的说明，使用 Solidity 语言创建您的第一个智能合同。

## 什么是智能合约？

[智能合约](https://chain.link/education/smart-contracts) 是在区块链环境中发布并执行的计算机程序。由于它们运行在区块链，它们可以在没有中央党或服务器的情况下运行。

智能合约一旦发布，由于区块链的不可改变性，就不可能更新或更改其代码。然而，智能合同可能已经被编程为具有改变数据的功能。这些信息可以记录在一个块中，在另一个块中删除，但是历史记录保留下来，可以进行审计。

## 可靠性编程语言

[Solidity](https://docs.soliditylang.org/) 是一种面向对象的高级语言，用于实现智能合约。它是一种 [花括号](https://en.wikipedia.org/wiki/List_of_programming_languages_by_type#Curly-bracket_languages) 语言，这意味着字符“{”和“}”定义语句块。

Solidity 受 C++、Python、JavaScript 影响，设计运行在以太坊虚拟机(EVM)上。它是静态类型的，支持继承、库和复杂的用户定义类型，以及其他特性。

## 混音

Remix 是一个在线网络工具。它是一个 IDE(集成开发环境),用于编写、编译、部署和调试 Solidity 代码。Remix 有一个名为 JavaScriptVM 的环境，这是一个在你的浏览器中运行的区块链模拟器。本教程将使用它。前往 remix.ethereum.org[](https://remix.ethereum.org/)入门。

## 创建智能合同

点击左边栏的第二个图标“文件浏览器”。

点击按钮“创建新文件”。

文件名:HelloWord.sol

用 Solidity 编写的文件使用扩展名”。索尔”。

复制并粘贴此示例:

```
// SPDX-License-Identifier: MIT
pragma solidity 0.8.13;
contract HelloWorld {
    function sayHelloWorld() public pure returns (string memory) {
        return "Hello World";
 }
}
```

现在让我们看看智能合同中有什么。

### //SPDX-许可证-标识符

**“//”**表示这是注释，不是代码行。

[SPDX 许可](https://spdx.org/licenses/) 列表规范是自由开放或协作软件中使用的常见许可列表。

Solidity 0.6.8 引入了 SPDX 许可证标识符，因此开发人员可以指定智能合约使用的许可证。

使用标识符**"///**将 SPDX 许可证标识符添加到合同文件的顶部

```
// SPDX-License-Identifier: MIT
```

### 语用学〔t1〕

使用语义版本化来指定 Solidity 的版本。在这里了解更多[](https://docs.soliditylang.org/en/v0.8.13/layout-of-source-files.html)。

```
pragma solidity 0.8.13;
```

### 契约 HelloWorld

这定义了一个名为“HelloWorld”的契约。

契约是功能和数据(其状态)的集合。

一旦部署，合同将存在于以太坊区块链的一个地址。在这里了解更多[](https://solidity.readthedocs.io/en/v0.8.13/structure-of-a-contract.html)。

### 功能`sayHelloWorld`

这是一个 **公共** 函数，返回字符串“Hello World”。它被声明为 **纯** ，因为它不读取或修改区块链状态。

## 编制智能合同

在左侧栏中找到一个名为“可靠性编译器”的按钮。

点击按钮“编译 HelloWorld.sol”。

启用自动编译选项很有用。

检查显示编译成功消息的按钮上的绿色标志。

## 部署智能合同

在左侧面板中，转到“部署和运行事务”按钮。

目前，我们只有一个智能合同，所以在下拉菜单中自动选择“合同**”**。

点击“部署”按钮。

## 与智能合约互动

在 Remix 中部署智能合约时，我们可以在左侧面板的“部署和运行交易”下看到它:

1.  向下滚动左侧，直至到达“已部署合同”。
2.  展开“HelloWorld”。
3.  点击“sayHelloWorld”按钮。
4.  它会返回智能合约中记录的消息:“Hello World”。

祝贺您，您已经创建了“Hello World”智能合约！

## 接下来的步骤

现在你已经使用 Solidity 语言创建了你的“Hello World”智能合约，有许多可能性可供你使用。您可以将合同部署到 testnet 甚至 mainnet，更改消息，创建一个状态变量来存储消息，创建一个函数来更新消息，或者将消息永久保存到区块链中！

访问[chain . link](https://chain.link)或阅读[docs . chain . link](https://docs.chain.link)上的文档，了解更多关于 Chainlink 的信息。 [要讨论一个集成，就去找专家。](https://chainlinkcommunity.typeform.com/to/OYQO67EF?typeform-source=blog.chain.link)