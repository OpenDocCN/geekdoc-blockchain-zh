# 固体事件和记录

> 原文：<https://blog.chain.link/events-and-logging-in-solidity/>

Solidity 事件对于智能合约开发人员来说是不可或缺的，允许针对特定变量测试智能合约，以自动化方式更改前端，等等。总的来说，知道如何在 Solidity 中使用事件使得智能契约开发变得更加容易。

在这篇文章中，我们将从智能合约开发者的角度来研究 [以太坊虚拟机](https://ethereum.org/en/developers/docs/evm/)【EVM】的日志和事件特性，包括日志和事件的用途、索引事件以及如何在 Hardhat 和 Brownie 中使用日志和事件。此外，在本教程的最后，我们将重点介绍两个视频，展示如何在 Brownie 和 Solidity 中处理 Solidity 事件。

EVM 是以太坊和许多其他区块链的标志。EVM 有一个 [日志](https://docs.soliditylang.org/en/v0.8.9/introduction-to-smart-contracts.html?highlight=logs#logs) 功能，用于将数据“写入”智能合约之外的结构。一个这样重要的数据是 [坚固性事件](https://docs.soliditylang.org/en/develop/contracts.html?highlight=events#events) 。Solidity 中的事件允许我们“打印”区块链上的信息，这种方式比仅保存到智能合约中的公共存储变量更可搜索，也更节能。

Solidity 中的日志是区块链上一种特殊的数据结构。它们 **不能被智能合约** 访问，并给出交易和区块中发生的信息。正是由于他们无法获得智能合同，使得他们的排放成本更低。

你也可以在这里观看我们的活动和登录视频:

[https://www.youtube.com/embed/KDYJC85eS5M?feature=oembed](https://www.youtube.com/embed/KDYJC85eS5M?feature=oembed)

## 什么是坚固中的事件？

Solidity events 允许我们方便地查询发生在块和事务中的“东西”。如果你运行一个区块链节点，你可以通过 [订阅](https://infura.io/docs/ethereum/wss/eth-subscribe) 来“监听”某些事件。事实上， [链式网络](https://chain.link/) 就是这样工作的:网络订阅某些地址的某些事件，并根据发出的事件内容从现实世界返回数据。

## 事件是为了什么？

现在，如果你不是 Chainlink 或 Ethereum node 的操作员，你可能会问 Solidity 中的事件是为了什么？使用实体事件，您可以:

1.  测试你的 [智能合约](https://chain.link/education/smart-contracts) 的具体变量；
2.  索引变量以重建存储状态；
3.  监听事件以改变前端；
4.  创建 [子图](https://thegraph.com/en/) 用于更快读取数据；

还有许多其他的东西。事件有各种各样的用例，可以挽救你作为一名工程师的生命。事实上，事件是 Chainlink 节点如何工作的核心部分之一！Chainlink 节点监听数据请求和外部计算事件，这就是它们知道如何响应的方式。

## 坚实度事件示例

这是在 Solidity 中定义事件的样子:

```
event storedNumber(
    uint256 indexed oldNumber,
    uint256 indexed newNumber,
    uint256 addedNumber,
    address sender
);
```

你可以认为这是一种新的特殊类型。我们创建了一种“类型”的事件，称为“storedNumber”。坚固性事件名称为“storedNumber ”,可以包含许多变量。在这个事件中有两种参数:索引的和非索引的。索引参数也称为“主题”，是事件中可搜索的参数。我们稍后会详细讨论这些内容。

然后我们可以发出这样一个事件:

```
uint256 favoriteNumber;

function store(uint256 _favoriteNumber) public {
    emit storedNumber(
        favoriteNumber,
        _favoriteNumber,
        _favoriteNumber + favoriteNumber,
        msg.sender
    );
    favoriteNumber = _favoriteNumber;
}
```

这里是一个完整的合同示例:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

contract SimpleStorage {
    uint256 favoriteNumber;

    event storedNumber(
        uint256 indexed oldNumber,
        uint256 indexed newNumber,
        uint256 addedNumber,
        address sender
    );

    function store(uint256 _favoriteNumber) public {
        emit storedNumber(
            favoriteNumber,
            _favoriteNumber,
            _favoriteNumber + favoriteNumber,
            msg.sender
        );
        favoriteNumber = _favoriteNumber;
    }

    function retrieve() public view returns (uint256) {
        return favoriteNumber;
    }
}
```

现在，在这个例子中，每当我们调用“store”函数时，它都会发出一个 storedNumber 类型的事件。让我们来看一个调用输入为“1”的“store”函数的示例事务。我们可以看到 [上的交易【科万】以太网](https://kovan.etherscan.io/tx/0x4d9278ccfa782007c3848987a679cf4bd64113bfa0846c4758525037eef7bfae) 。

滚动到事务的“logs”部分，我们看到下图:

![Screenshot of transaction on Etherscan, decoded](img/d638a04f3c95451101408428719c46b2.png)

一个事件被分解成这样:

**地址:** 发出事件的合同或帐户的地址。

**主题:** 事件的索引参数。

**数据:**[ABI 编码的](https://blog.chain.link/what-are-abi-and-bytecode-in-solidity/) 或“散列”的事件的非索引参数。因为我们知道合同的 ABI(因为我们在 Etherscan 上验证了合同)，所以我们可以以“Dec”或“decoded”模式查看它，或者以其原始的“hex”、“Hexidecimal”或“Encoded”模式查看它。如果我们没有对合同进行验证，我们就无法看到解码后的版本。

![Screenshot of transaction on Etherscan, not decoded](img/c2c922f09913f9574c4de0b9034627f2.png)

你可以在 [实体文档](https://docs.soliditylang.org/en/develop/abi-spec.html#abi-events) 中了解更多关于活动的布局。“日志”和“事件”经常互换使用，因为作为智能合约开发人员，我们通常只关心记录的“事件”。然而，从技术上讲，Solidity 中的日志还包括“块散列”、“地址”以及通过调用[` eth _ get logs`](https://eth.wiki/json-rpc/API#eth_getlogs)到您的区块链节点返回的所有内容。你也可以阅读更多关于[bloom filter](https://ethereum.stackexchange.com/questions/3418/how-does-ethereum-make-use-of-bloom-filters/3426)的内容，这就是为什么这些 Solidity 事件如此容易被查询。

## 安全帽中的坚固性事件

现在我们已经了解了什么是事件，让我们学习如何在 Hardhat 中访问和使用它们。您可以克隆以下回购并跟进:

```
git clone https://github.com/PatrickAlphaC/hardhat-events-logs
cd hardhat-events-logs
```

你需要跟随“README.md”来获得 [先决条件](https://github.com/PatrickAlphaC/hardhat-events-logs#requirements) ，其中包括节点、纱线和 Git。

如果您遵循“README.md ”,您将能够:

1.  部署智能合同；
2.  创建一个发出事件的事务；
3.  查看这些事件的背景。

如果中途遇到问题，在 [Github 回购](https://github.com/PatrickAlphaC/hardhat-events-logs) 上打开问题！我们可以通过检查“transactionReceipt”对象的 logs 属性来查看日志。

```
console.log(transactionReceipt.events[0].args.oldNumber.toString())
```

## 布朗尼中的固体事件

布朗尼的事件几乎相同，因为合同完全相同。

您可以克隆以下回购并跟进:

```
git clone https://github.com/PatrickAlphaC/brownie-events-logs
cd brownie-events-logs
```

你需要跟随“README.md”来获得 [先决条件](https://github.com/PatrickAlphaC/brownie-events-logs#requirements) ，其中包括 Node、Python、eth-brownie 和 Git。

如果您遵循“README.md ”,您将能够:

1.  部署智能合同；
2.  创建一个发出事件的事务；
3.  查看这些事件的背景。

如果中途遇到问题，在 [Github 回购](https://github.com/PatrickAlphaC/brownie-events-logs) 上打开问题！您将看到这里的主要区别是，我们使用 print 语句来打印事务的日志:

```
print(tx.events[0]["oldNumber"])
```

## 总结

Solidity 中的日志和事件是智能合同开发的重要组成部分，也是 Chainlink 和 The Graph 等项目的关键基础设施。要了解更多关于构建极其强大的智能合约(利用您的新事件技能)，请务必前往 [Chainlink 文档](https://docs.chain.link/docs/beginners-tutorial/) 立即开始构建。