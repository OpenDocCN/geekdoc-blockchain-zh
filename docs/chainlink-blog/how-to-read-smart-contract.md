# 如何在 Etherscan 上阅读智能合同

> 原文：<https://blog.chain.link/how-to-read-smart-contract/>

什么是 [智能合约](https://chain.link/education/smart-contracts) ？一个基本的定义是: 智能合约是一个防篡改程序，当满足某些预定义的条件时，它运行在 [区块链网络](https://blog.chain.link/what-is-blockchain/) 上。

这是什么意思？简单来说，智能合约就是程序。代码是透明的，通常是不可改变的。智能合约在区块链网络上托管和执行。知道什么是智能合约是很好的，但是你如何阅读智能合约来了解它的作用呢？

## **如何阅读智能合同**

在本指南中，我们将了解一个受欢迎的 NFT 项目的合同、[](https://opensea.io/collection/doodles-official)涂鸦，以及如何在 Etherscan 上阅读这些智能合同。通过查看 OpenSea 上的项目，我们可以调查其中一个 NFT，以找到支持 NFT 项目的合同。拿到合同并阅读它有几个步骤。

### **查找项目合同**

![](img/fe43f54e19b9b45d7fc2c062189c2f6e.png)

在 OpenSea 上的 NFT 项目中，您可以查看单个项目。然后，在“详细信息”下，您会找到合同地址的链接。这个链接会带你去 [以太扫描](https://etherscan.io/) ，这是一个区块链探索者。本质上，它允许您查看有关以太坊区块链的信息。

### **检查已验证的合同**

一旦知道了合同的地址，就可以在 Etherscan 上查看。涂鸦合同的合同地址为 `0x8a90CAb2b38dba80c64b7734e58Ee1dB38B8992e`。 如果合同的代码没有通过验证，你在以太扫描上就没什么可做的了。虽然契约的字节码是可用的，并且可以反编译，但这超出了本教程的范围。如果您没有看到“合同”旁边的绿色复选标记，则代码尚未验证。

![Etherscan smart contract code](img/375efc0bbb432adeb54f9281fe39f27a.png)

### **读取已验证的合同**

如果合同得到验证，你应该能够以一种更易于阅读的格式查看代码。如果你点击**标签页，你将被带到该合同的代码。**

 **![Doodles smart contract code](img/aa9255455e82e1d1a11d942ab44f533c.png)

根据合同作者使用的验证方法，您可能会看到一个大文件，它是智能合同使用的所有合同的串联，或者像涂鸦一样，是单独的文件。这里可以看到多个合同，因为单个智能合同通常会导入其他合同。这使得契约可以重用经过验证的契约，比如我们在 Doodles 项目中看到的 OpenZeppelin ERC-721 和 Ownable 契约。

![Read Contract Write Contract](img/ed3efba6e29db07fa0f2d780cac4e468.png)

至此，你可以通读支持 Doodles NFT 项目的所有代码，以确保它按预期运行。

### **与合同交互**

如果你想通过 Etherscan 与合同互动，如果合同经过验证，也是可行的。“阅读合同”和“编写合同”选项卡提供了对智能合同功能的访问，尽管这不在本文的讨论范围之内。任何人都可以访问 read 函数，并且可以免费执行它们。写函数改变区块链，这需要 gas，并且可能伴随着其他需求，例如所有权。

![Import contract](img/fa4b574dc510977fb931e1e26aa65c40.png)

## **为什么阅读智能合同很重要**

智能合约可以公开阅读，这是使用智能合约的优势之一。普通用户可以看到为合同提供动力的代码，这意味着他们可以确保合同做它所说的事情。这降低了信任开发者的需要。

找到并阅读合同代码仅仅是个开始。为了更好地理解合同中发生的事情，你需要对可靠性有一个基本的了解。

## **何去何从**

查看 [教育中心](https://chain.link/education) 了解更多关于 [智能合约](https://chain.link/education/smart-contracts) 。教育中心拥有大量关于智能合同的资源，以及各种其他区块链主题的材料。

要了解更多，请访问[chain . link](https://chain.link/)，订阅 [Chainlink 简讯](https://chn.lk/newsletter) ，并关注 Chainlink 上的[Twitter](https://twitter.com/chainlink)，[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)，以及[Reddit](https://www.reddit.com/r/Chainlink/)。**