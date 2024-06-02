## 第四部分

第四部分 针对那些急于构建自己的 Dapp 并计划将其部署到以太坊主网（MAINNET，生产以太坊网络）的读者。 第十三章 涵盖了重要的运营方面，例如事件日志和合约的可升级性。您将了解不同的技术，这些技术允许您在发现错误或安全漏洞后修改已部署的合约。 第十四章 完全专注于安全性，并描述常见的漏洞和智能合约攻击的典型形式。 第十五章 适合所有希望继续学习以太坊和区块链技术一般内容的读者。它概述了针对企业使用的不同以太坊实现。它还简要介绍了其他区块链和分布式账本平台。如果您想继续超越以太坊的旅程，您将有很多选择可以考虑。

## 第十三章. 使 Dapp 达到生产准备状态

|  |
| --- |

**本章内容**

+   如何生成事件日志

+   部署库后如何升级

+   部署后如何升级您的合约

|  |
| --- |

在上一章中，您第一次从零开始构建了一个完整的 Dapp，使用了您在整本书中学到的知识，以及大多数可用的以太坊开发工具。尽管这是一个很好的练习，有助于您巩固以太坊开发技能，但您可能还没有准备好将您的第一个 Dapp 部署到公共生产网络。在这样做之前，您可能想要考虑加强您的 Dapp，使其能够处理现实世界的运营需求，例如能够生成、在区块链上存储和在区块链上查询事件日志；在部署后升级您的库；在部署后升级您的合约。

我已经简要接触过这些主题中的某些内容，但在这一章中，我将更详细地重新讨论它们。我将保持我通常的务实方法，并通过示例和代码引导您。设计一个可升级的库或合约，尽管需要高级技术，其实施触及了超出本书范围的 Solidity 语法。但我仍然认为您应该了解这些概念，我将尝试通过绘制一些合约或序列图来说明它们。

您可能会惊讶我没有把安全性包括在内。我认为这是一个如此重要的主题，以至于我打算用下一整章来专门介绍它。

### 13.1. 事件日志

让我们从事件日志开始。您已经知道如何在智能合约上声明和引发事件。在上一章中，您看到了如何从 Web UI 处理合约事件。

例如，每次投票过程移动到新步骤时，你都会在管理员和选民页面的顶部刷新工作流状态描述。另外，每当一个选民注册一个新的提案时，你会在选民页面的顶部刷新提案表格。提案注册的工作流，以及相关的事件处理，如图 13.1 所示，如果你还记得，它与第一章的图 1.8 非常相似。如果你在第一章没有完全理解，现在应该恍然大悟了。

如果你之前做过事件驱动或反应式编程，你可能会认为合约发布事件的方式以及合约的客户端（例如一个网页）处理它们的方式并没有什么不寻常的。但合约在重要方面有所不同：在大多数语言中，事件处理后就会从系统中消失，而以太坊事件则被永久记录在区块链上。因此，如果你想的话，你也可以在启动 UI 客户端之前检索发生的事件。想知道怎么做吗？继续阅读！

#### 13.1.1\. 检索过去的事件

你已经看到了如何用`eventFilter.watch`在 JavaScript 上注册合约事件的监听器。例如，你在 SimpleVoting.js 顶部写了这样的代码来注册一个工作流状态变更事件的回调（虽然这里我稍微简化了一下）：

```
var workflowStatusChangeEvent  =
    contractInstance.WorkflowStatusChangeEvent();    *1*

workflowStatusChangeEvent
   .watch(function(error, result) {                  *2*
    if (!error)
        refreshWorkflowStatus();
    else
        console.log(error);
});
```

+   ***1*** **设置一个事件过滤器，监听工作流状态变更事件**

+   ***2*** **向事件过滤器注册回调**

##### 图 13.1\. 选民页面的事件处理。从网页提交新的提案到投票合约。合约在注册完成时触发`ProposalRegisteredEvent`事件。事件在整个网络上传播，直到它到达与网页通信的节点。最后，网页处理事件，并在提案表格中添加新条目。

![](img/fig13-01_alt.jpg)

变量`workflowStatusChangeEvent`被称为*事件过滤器*，因为它定义了要监听的事件集合——在我们这个例子中，所有类型为`WorkflowStatusChangeEvent`的事件。正如你稍后看到的，你可以以更严格的方式定义过滤器。

当你通过`eventFilter.watch`为一个事件过滤器注册回调时，你会处理从网页打开时刻开始发生的事件。如果你想访问过去的事件——例如，为了验证工作流状态变更是否按正确的顺序发生——你可以通过`eventFilter.get`来实现，它接受一个与`watch`类似的回调。首先，你必须以稍微不同方式定义过滤器，通过指定事件搜索的起始区块和最终区块：

```
var pastWorkflowStatusChangeEvent =
    contractInstance.WorkflowStatusChangeEvent(
       {},
       {fromBlock: 5000, toBlock: 'latest'});        *1*
```

+   ***1*** **只获取区块 5000 之后的事件**

然后你用`get`而不是`watch`向事件过滤器注册回调：

```
pastWorkflowStatusChangeEvent.get(
   function(error, logs) {                           *1*
   if (!error)
       logs.forEach(log => console.log(log.args));   *2*
   else
    console.log(error);
});
```

+   ***1*** **检索过去的事件**

+   ***2*** **将过去的事件参数显示在控制台**

如果你想检索*所有*合约广播的过去事件，不仅仅是`WorkflowStatusChangeEvent`事件，你可以使用`allEvents`函数创建事件过滤器，如下所示：

```
var allEventPastEvents = contractInstance.allEvents(
    {}, {fromBlock: 1000000, toBlock: 'latest'});        *1*
```

+   ***1*** **过滤自合约成立以来产生的所有事件日志**

然后，你可以通过`get`注册一个回调，就像以前一样：

```
allEventPastEvents.get((error, logs) => { 
  logs.forEach(log => console.log(log.args))
});
```

如果你只想检索过去事件的一个子集——例如，某个特定选民注册的提案——你可以通过索引所讨论事件的某些参数，更高效地执行搜索。你马上就会看到如何操作。

#### 13.1.2\. 事件索引

当在合约上声明一个事件时，你可以索引其中的最多三个参数。与这些参数相关的事件过滤器将表现得更好。例如，在 SimpleCoin 的情况下，你可能还记得从第 3.5.1 节得知`Transfer`事件被定义为

```
event Transfer(address indexed from, address indexed to, uint256 value);
```

这允许你在检索事件日志时，高效地过滤出针对特定源地址和目标地址的转账事件：

```
var specificSourceAccountAddress =
    '0x8062a8850ef59dCd3469A83E04b4A40692a873Ba';
var transactionsFromSpecificAccount =
    simpleCoinInstance.Transferred(
    {from: specificSourceAccountAddress},
    {fromBlock: 5000, toBlock: 'latest'});
transactionsFromSpecificAccount.get((error, logs) => {
    logs.forEach(log => console.log(log.args));
});
```

在`SimpleVoting`的情况下，你可能还记得`ProposalRegisteredEvent`事件被定义为

```
event ProposalRegisteredEvent(uint proposalId);
```

目前，你不能将此事件作为日志以有意义的方式使用。你会如何修改其定义，以便你可以查询它以提供有用的信息？思考几秒钟......你可以这样修改：

```
event ProposalRegisteredEvent(
    address author, uint proposalId, string proposalDescription);
```

作为一个练习，这里有一个问题供你思考：你会如何索引这个事件，以便高效地检索出特定地址注册的所有提案？慢慢思考...是的，你说得对！显然，你会把作者参数作为**索引**。

```
event ProposalRegisteredEvent(
    address indexed author,
    uint proposalId, string proposalDescription);
```

现在让我们转换到一个完全不同的主题，从操作角度来看这也是非常重要的：当你的合约中出现问题时，你应该怎么做？是否可以像对待传统软件组件（如库或微服务）一样修复它并重新部署？我将在接下来的几节中讨论这个问题的答案。

### 13.2\. 设计可升级的库

当开发一个新的合约时，你的一些要求可能与其他开发者在区块链上已经部署的合约的要求相似。你在第七章中看到了如何将公共功能放入库中，并从各种合约中引用它，从而避免了重复实现的努力和代码重复。例如，你实践了如何使用 OpenZeppelin SafeMath 库的副本执行安全的算术操作。然而，你所做的一切仍然不是理想的：你部署的 OpenZeppelin 库可能是区块链上存在的许多实例中的一个。像你这样的其他开发者可能已经将此类库的副本包含在他们的解决方案中，并可能进行了自己的私有部署，如图 13.2 所示。

##### 图 13.2。OpenZeppelin 库的重复部署。只有每个私有部署的实例的一个客户端合约使用。

![](img/fig13-02_alt.jpg)

你可以想象一下在 TESTNET 和 MAINNET 上有多少 OpenZeppelin 库的实例！这种方法的危害包括以下几点：

+   *不必要的成本*——每个相同的库的单独部署都必须支付自己的部署交易燃气费。

+   *不必要的字节码复制*——相同的字节码与区块链上的不同部署地址相关联（尽管节点实际上会去重相同的字节码）。

+   *不协调的维护*——如果检测到库中的问题，您不能集中修复它；每个合约实例的所有者必须独立修补，后果显然。

这些问题最明显的解决方案是，在区块链上有一个官方的*黄金实例*，并期望所有客户端都引用这个单一地址，正如你在第七章中简要看到的，7.5.2 节。这个解决方案有一个主要缺点：一旦部署了一个库，你就无法修复它。如果你发现一个问题，一个新的部署是必要的，结果是所有客户端合约也必须重新指向新的库地址并重新部署，如图 13.3 所示。这远非理想的解决方案！

##### 图 13.3。修复共享库意味着将其部署到新地址，这需要修改并重新部署客户端合约。

![](img/fig13-03_alt.jpg)

一个优雅的解决方案，由 Zeppelin 的 CTO 曼努埃尔·阿罗兹在一篇 Medium 文章中提出（[1])，是创建一个库的代理。他的解决方案是一个库代理合约，作为使用库的客户端合约与库本身之间的间接层，如图 13.4 所示。

> ¹
> 
> 参见“Solidity 中的代理库”，2017 年 3 月 6 日，[`mng.bz/Xgd1`](http://mng.bz/Xgd1)。

##### 图 13.4。当你向库引入一个代理时，客户端合约不再直接引用库的一个实例；它们与代理（或库调度器）通信，从另一个合约获取库的最新有效地址，然后将调用转发给有效的实例。

![](img/fig13-04_alt.jpg)

这是代理库解决方案的组件：

+   客户端合约引用的是库代理（或调度器）合约（`SafeMathProxy`）的地址，而不是直接引用库的实例。

+   *库代理*（`SafeMathProxy`）是一个合约，它从库代理注册合约（`SafeMathProxyRegistry`）中检索最新有效部署的库实例的地址，然后将调用转发到最新部署的库实例。

+   **库代理注册合约**（`SafeMathProxyRegistry`）是一个包含不同版本库地址列表的合约。它可能还包含一个状态变量，持有默认地址，通常是添加到列表中的最新地址。库所有者在每次部署库时更新地址列表和默认地址。

当客户端合约调用库函数时，它会在库代理上执行相应的`delegatecall`。这从库代理注册表中获取客户端合约要使用的正确库地址，然后对库的相关实例执行`delegatecall`。从客户端合约的角度来看，整个调用链的行为与正常调用库函数完全一样。

|  |
| --- |

##### 注意

库函数是通过`delegatecall` EVM 操作码隐式调用的，如第 3.2.5 节所述，我将在第十四章进一步解释。

|  |
| --- |

总之，如果您发现您想使用的库提供了代理，请使用它，而不是硬编码到特定的已部署实例。你会得到可维护性。但要注意，您必须信任合约所有者不会恶意地将您的调用转发到与原库无关的新库实现。

如果您对设计可升级的库这个想法感兴趣并想进一步学习，我鼓励您回顾 Araoz 的 Medium 文章，那里有代码示例。

|  |
| --- |

##### 警告

在尝试实现之前，您应该彻底理解代理库技术；已经发现薄弱的实现容易受到恶意攻击。我建议您阅读 Patricio Palladino 在 Medium 上发表的文章“Ethereum Proxies 中的恶意后门”，以确保您知道薄弱环节：[`mng.bz/vNz1`](http://mng.bz/vNz1)。

|  |
| --- |

### 13.3. 设计可升级的合约

正如您可能已经猜到的那样，智能合约与库一样存在相同的局限性：一旦部署了一个合约，你就固定下来了。如果你在部署后发现了一个错误或安全漏洞，你最多只能冻结或销毁它——如果你包含了这种紧急停止功能的按钮。最好的办法是在此之前计划好最坏的情况，并设计一个具有内置可升级性的合约。

与代理库的情况一样，尽管这种解决方案使合约从您的角度来看更安全，但从用户的角度来看，您引入了一层混淆。最注重安全的用户可能不信任您的良好意愿，可能会担心您突然开始将客户端调用重定向到恶意合约。

我将为您说明使合约可升级的这两种主要技术：

+   对库使用相同的代理技术

+   将状态和逻辑分成两个合同，都继承自抽象的`Upgradeable`合同

#### 13.3.1\. 通过代理连接到升级后的合同

想象一下各种合同，其中`SimpleCrowdsale`，在第六章和第七章中，想要使用你神奇的`SimpleCoin`合同。你决定通过一个`SimpleCoinProxy`合同使`SimpleCoin`可升级，以避免给包括你在内的所有客户带来头疼的问题。正如图 13.5 所示，这个解决方案与 SafeMath 中你看到的一致。

##### 图 13.5\. 如果你决定通过`SimpleCoinProxy`使`SimpleCoin`可升级，像`SimpleCrowdsale`这样的客户合同将会在`SimpleCoinProxy`上调用函数，它会调度到`SimpleCoin`的具体部署版本，通常是最新版本。

![](img/fig13-05_alt.jpg)

#### 13.3.2\. 从抽象的 Upgradeable 合同继承

ENS 的创作者 Nick Johnson 采取了一种略有不同的方法来使合同可升级。^([2])他提议将状态（存储和以太币）和合同的逻辑分成两个分开的合同，都继承自同一个名为`Upgradeable`的抽象合同：

> ²
> 
> 参见“Mad blockchain science: A 100% upgradeable contract，” Reddit+r/ethereum，May 24, 2016， [`mng.bz/y1Yo`](http://mng.bz/y1Yo)。

合同的逻辑分成两个分开的合同，都继承自抽象的`Upgradeable`合同：

+   *一个调度器*——这将保存状态，并通过 Solidity `delegatecall()`函数（执行显式的 EVM `delegatecall`操作码）将所有调用调度到目标合同。因此，该函数将在调度器的上下文中执行。你将在第十四章中看到更多关于`delegatecall()`的内容，关于安全方面。

+   *一个目标合同* *合同*——你将把全部功能委托给这个合同，以后可以升级。这个合同还将控制升级过程。

如图 13.6 所示，在目标合同升级时，调度器仍然保持未更改的状态，同时将所有调用传递到目标合同的最新版本。

##### 图 13.6\. 通过将合同分成两个继承自同一抽象`Upgradeable`合同的合同来实现升级性：一个保存状态的调度器和一个保存功能的 target contract。调度器将所有调用转发给目标合同。如果发生升级，调度器将保持相同的未更改状态并将调用转发给目标合同的最新版本。

![](img/fig13-06_alt.jpg)

如果你急于尝试这种方法，我鼓励你查看尼克在[`mng.bz/4OZD`](http://mng.bz/4OZD)的代码。如果你对围绕库或合约可升级性的解决方案感兴趣，我推荐基于他研究所有目前已知技术的 Medium 文章“以太坊可升级智能合约研发总结”，作者是杰克·坦纳：[`mng.bz/QQmR`](http://mng.bz/QQmR)。

|  |
| --- |

##### 警告

使用尼克的技术设计一个可升级的合约需要对以太坊虚拟机（EVM）及其汇编语言有深入的了解，这超出了本书的范围。此外，使用可升级的合约存在风险，我之前已经解释过了。

|  |
| --- |

### 摘要

+   在大多数语言中，事件是短暂的对象，在处理后从系统中消失，而以太坊事件则永久记录在区块链上。

+   你可以通过在事件过滤器上注册`get`而不是`watch`来重新播放和查询过去的事件。

+   你可以通过在定义事件时索引一些事件参数来提高过去事件检索的性能。

+   你可以通过向库中引入代理来使库可升级。客户端合约不再直接引用库的实例，而是与代理（或库调度器）通信，代理从注册合约获取库的最新有效地址，然后将调用转发给有效的实例。

+   你可以通过使用代理合约（就像库一样）或将状态和逻辑分离到两个合约中，这两个合约都继承自抽象的`Upgradeable`合约，使合约可升级。

+   使合约可升级一方面使其更安全；例如，如果在部署后发现问题，你可以修复合约并将调用路由到新的修订版本。但如果不正确实现，它可能会引入安全风险。

+   使用可升级的库从合约用户的角度来看会引发安全担忧，用户可能会担心被引导到非预期的功能。

## 第十四章。安全考虑

|  |
| --- |

**本章内容**

+   理解 Solidity 的弱点以及与外部调用的相关风险

+   执行安全的外部调用

+   避免已知的攻击手段

+   通用安全指南

|  |
| --- |

在上一章中，我给你提供了一些建议，告诉你部署你的 Dapp 到生产网络之前应该关注哪些方面。我相信安全是如此重要的话题，应该单独介绍，因此我决定将整章都献给它。

我会先提醒你一些在 Solidity 语言中的限制，如果你忽视它们，它们可能会变成安全漏洞。在这些限制中，我将特别关注外部调用，并解释在执行它们时你可能面临的各种风险，但我也会尝试给你一些避免或最小化这些风险的技巧。最后，我会介绍可能针对以太坊 Dapps 发起的经典攻击，这样你就可以避免在以太币受到威胁时犯下昂贵的错误。

### 14.1. 理解一般的网络安全弱点

你应该关注 Solidity 语言中的一些限制，因为它们通常被恶意参与者作为攻击的第一步，针对不知情的开发者：

+   **数据隐私**——如果隐私是一个要求，你应该以加密形式存储数据，而不是明文形式。

+   **随机性**——一些 Dapps，例如，赌博游戏，偶尔需要随机化。你必须确保在所有节点上进行平等的处理，而不暴露应用程序以利用伪随机生成器的可预测性，这可能会很棘手。

+   **视图函数**——你应该知道定义为`view`的函数可能会修改状态变量，如在第五章中提到的 5.3.5 节。

+   **燃料限制**——你在设置交易的燃料限制时应该小心，无论它们是低还是高，因为攻击者可能会试图利用它们的优势。

一些漏洞，比如与随机性相关的漏洞，可能会导致更严重的后果，比如丢失以太币。其他的漏洞，比如与燃料限制相关的漏洞，后果不那么严重；例如，它们可以被利用来进行服务拒绝攻击，只能造成暂时的故障。无论它们看起来是否严重，你不应该低估*这些漏洞*中的任何一个。

#### 14.1.1. 私人信息

正如你所知，存储在区块链上的数据总是公开的，不管它是对合约状态变量的访问级别如何。例如，每个人仍然可以看到被声明为私有的合约状态变量的值。

如果你需要隐私，你需要实现一个*哈希提交-揭露*方案，就像 MAINNET ENS 域名注册使用的那个一样，在第九章中描述的 9.3.2 节。例如，为了在拍卖中隐藏一个出价，原始值不必提交。相反，出价应该分为两个阶段，如图 14.1 所示：

1.  **哈希提交**——你首先应该*提交*原始值的哈希，以及可能标识发送者的某些独特数据。

1.  **揭露**——你在第二阶段*揭露*原始值，那时拍卖结束，必须确定赢家。

##### 图 14.1. 用于拍卖出价隐私的哈希提交-揭示方案。1. 在提交阶段，你提交包含发送者地址、出价值和秘密（而不是明文中的出价值）的文档的哈希。2. 在揭示阶段，你揭示出价值和它们的秘密。3. 赢家由揭示的最高出价确定。然后你通过计算从其发送者地址、出价值和密码生成的哈希，并与之前提交的哈希进行比较，来验证结果。

![](img/fig14-01_alt.jpg)

#### 14.1.2. 随机性

如果你希望去中心化应用程序的状态依赖于随机性，你将面临与隐藏私有信息相关的相同挑战，如前一部分所述。主要关注的是防止矿工操纵随机性以获得优势，同时确保在所有节点上以完全相同的方式执行你的合约逻辑。

因此，在 Dapp 中处理随机性的方式应类似于私有数据的提交-揭示方案。例如，如您在图 14.2 中看到的，在去中心化轮盘赌游戏中应该发生以下情况：

1.  所有玩家提交他们的赌注（特定的数字、颜色、奇数或对）。

1.  请求随机值提供者提供一个随机数，为了在最后一刻之前保持数字的秘密，提供者最初返回（提交）使用单向哈希算法编码的数字。

1.  完成的交易，包括赌注和生成的随机数，所有节点都会处理，这些节点将查询随机性提供者与哈希相关联的原始数字。提供者揭示原始随机数，确定赢家。如果随机性提供者提供一个与哈希不兼容的随机数，轮盘赌旋转交易失败。

##### 图 14.2. 用于提供可复现随机性的哈希提交-揭示方案。1. 所有玩家提交他们的赌注。2. 随机数提供者提交生成的随机数的哈希，模仿轮盘赌的旋转。3. 处理包括赌注和随机数哈希的交易。所有节点查询提供者，该提供者揭示随机数，以便确定赢家和输家。

![](img/fig14-02_alt.jpg)

#### 14.1.3. 调用视图函数

将函数定义为 `view` 并不能保证在您运行它时合同状态不会被修改。编译器不执行此类检查（但 Solidity 编译器的版本 0.5.0 或更高版本将执行此检查），EVM 也不执行。编译器只会返回一个警告。例如，如果您定义 SimpleCoin 的 `authorize()` 函数为

```
    function authorize(address _authorizedAccount, uint256 _allowance)
        public view returns (bool success) {
        allowance[msg.sender][_authorizedAccount] = _allowance;
        return true;
    }
```

你将得到以下警告，因为允许映射的状态正在被修改：

```
Warning: Function declared as view, but this expression (potentially)
     modifies the state...
```

如果合同状态被修改，执行交易（而不是简单调用），这会消耗 gas。攻击者可能会利用合同所有者没有预见到此功能的 gas 消耗，可能会导致从几个交易失败到持续的 DoS 攻击等一系列后果。为了避免

在编写代码时，你应该注意编译器警告，并确保相应地修正代码。

#### 14.1.4\. Gas 限制

如您所知，为了成功处理，交易发送者设置的区块 gas 限制不能超过。如果交易失败是因为达到了 gas 限制，合同状态将回滚，但发送者必须支付交易费用，并且不会退款。

交易发送者设置的 gas 限制可能对安全有利或不利，这取决于如何使用。以下是对立面案例，如图 14.3 所示：

+   *高 gas 限制*——这使得交易在不耗尽 gas 的情况下完成的可能性更大，它对试图通过耗尽 gas 来失败的攻击更安全。另一方面，高 gas 限制允许恶意攻击者更容易地操纵交易，因为他们可以利用更昂贵的资源和计算来改变交易的预期流程。

+   *低 gas 限制*——这使得交易因为耗尽 gas 而失败的可能性更大，特别是如果发生意外情况。因此，如果出现意外，交易将更容易受到试图通过耗尽 gas 来失败的攻击。另一方面，低 gas 限制限制了恶意攻击者如何操纵交易。

##### 图 14.3\. 高低 gas 限制的利弊

![](img/fig14-03_alt.jpg)

一般来说，最好的建议是设置尽可能低的 gas 限制，以允许所有真实交易完成预期的逻辑。但是，很难确定一个既安全又能完成交易的合理 gas 估计。

例如，如果执行交易的逻辑包含循环，交易发送者可能会决定设置一个相对较高的 gas 限制，以覆盖循环次数多的可能性。但是，预先判断 gas 限制是否会达到很难，特别是如果循环次数是动态确定的，并取决于状态变量。如果状态变量中任何一个受到用户输入的影响，攻击者可以操纵它们，使循环次数变得非常大，交易更有可能耗尽 gas。通过设置一个非常高的 gas 限制来试图绕过这个问题，实际上否定了限制本身的目的，这不是正确的解决方案。在接下来的几节中，我们将探讨正确的解决方案。

### 14.2\. 理解与外部调用相关的风险

对外部合同的调用引入了几个潜在的对您应用程序的威胁。本节将帮助您避免或最小化这些威胁。

首先的建议是，如果可以使用替代解决方案，则避免调用外部合约。外部调用将您的逻辑流程转移到可能具有恶意的不信任方，即使只是间接的。例如，即使您调用的外部合约本身不是恶意的，其功能可能会进而调用一个恶意合约，如图 14.4 所示(图 14.4)。

##### Figure 14.4. 即使您确信与之直接交互的合约是合法的，您的合约仍可能被外部恶意合约操纵。

![](img/fig14-04_alt.jpg)

由于您失去了对逻辑执行的直接控制，您容易受到基于*竞态条件*和*重入*的攻击，我们稍后会进行探讨。此外，在外部调用完成后，您必须小心处理返回值，尤其是在异常情况下。但是通常，即使可能感觉有风险，您也没有选择，只能与外部合约进行交互，例如，在项目开始时，您希望通过利用经过验证的组件来快速取得进展。在这种情况下，最安全的做法是了解相关的潜在陷阱，并编写代码预防它们——继续阅读！

#### 14.2.1. 理解外部调用执行类型

您可以执行外部调用以调用外部合约中的函数或向外部合约发送以太币。同时发送以太币并执行代码也是可能的。表 14.1 总结了执行外部调用的每种方式的特点。

|  |
| --- |

##### 警告

`send()`和`call()`从 Solidity 编译器的 0.5 版本开始逐渐被淘汰。

|  |
| --- |

##### Table 14.1. 每种外部调用执行类型的特点

| 调用执行类型 | 目的 | 调用的外部函数 | 抛出异常 | 执行上下文 | 消息对象 | 气体限制 |
| --- | --- | --- | --- | --- | --- | --- |
| externalContractAddress .send(etherAmount) | 原始以太币转账 | 回退函数 | 否 | N/A | N/A | 2,300 |
| externalContractAddress .transfer(etherAmount) | 安全的以太币转账 | 回退函数 | 是 | N/A | N/A | 2,300 |
| externalContractAddress .call.(bytes4(sha3( "externalFunction()"))) | 外部合约上下文中的原始函数调用 | 指定函数 | 否 | 外部合约 | 原始消息 | 原始调用的气体限制 |
| externalContractAddress .callcode.(bytes4(sha3( "externalFunction()"))) | 调用者上下文中的原始函数调用 | 指定函数 | 否 | 调用合约 | 调用者创建的新消息 | 原始调用的气体限制 |
| externalContractAddress .delegatecall.(bytes4(sha3("externalFunction()"))) | 调用者上下文中的原始函数调用 | 指定函数 | 否 | 调用合约 | 原始消息 | 原始调用的气体限制 |
| ExternalContract(external ContractAddress).externalFunction() | 安全的函数调用 | 指定函数 | 是 | 外部合约 | 原始消息 | 原始调用的气体限制 |

使用`call()`、`callcode()`和`delegatecall()`时，你可以通过使用`value`关键字指定以太币金额，同时调用调用，如下：

```
externalContractAddress.call.value(etherAmount)(
    bytes4(sha3("externalFunction()")
```

也可以不调用任何函数而纯粹地转移以太币，这样做：

```
externalContractAddress.call.value(etherAmount)()
```

这种发送以太币的方式有其优点和缺点：它允许接收者拥有更复杂的后备函数，但出于同样的原因，它也使发送者面临恶意操纵的风险。正如你可以从表 14.1 理解的那样，外部调用的各个方面可能会在执行外部调用时影响安全性：

+   你可以调用哪个外部函数？

+   如果外部调用失败，是否会抛出异常？

+   外部调用在什么上下文中执行？

+   接收到的消息对象是什么？

+   什么是气体限制？

让我们逐一检查它们。

#### 14.2.2. 你可以调用哪个外部函数？

可以将调用执行类型分组为两组：一组只允许转移以太币，另一组允许调用任何函数。

##### 纯以太币转移

`send()`和`transfer()`调用只能调用（隐式地）外部合约的`fallback()`函数，如下所示：

```
contract ExternalContract {
   ...
   function payable() { }          *1*
}

contract A {
   ...
   function doSomething()
   {
      ...
      externalContractAddress.send(etherAmount); 
   }
}
```

+   **1** **这是一个后备函数，send()会隐式调用，如 5.3.2 节所解释的那样。**

通常，后备函数可以包含任何复杂度的逻辑。但`send()`和`transfer()`对后备函数的执行施加了 2,300 的气体限制，通过只向外部函数预算 2,300 来执行。这是一个如此低的气体限制，除了转移以太币外，后备函数只能执行日志操作。

低限制确保了发送者免受潜在的*重入*攻击（我稍后会描述）。之所以这样做，是因为当控制流传递给后备函数时，外部合约无法执行除了接受以太币转移之外的其他操作。另一方面，这意味着如果你需要在以太币支付周围执行任何实质性的逻辑，你不能使用`send()`和`transfer()`。如果你还没有完全理解这个观点，不要担心：当你在学习接下来的页面中的重入攻击时，这将变得清晰。

##### 调用自定义函数

所有其他执行类型都可以在向外部合约转移以太币时调用自定义外部函数。这种灵活性的缺点是，尽管你可以将任何复杂度的逻辑与以太币转移关联（感谢可以高达发送者愿望的气体限制），但外部调用的恶意操纵风险，以及因此导致的以太币转移风险，也会更高。

如我之前解释的，也可以纯粹地转移以太币而不调用任何函数，如下：

```
externalContractAddress.call.value(etherAmount)()
```

通过`call()`进行外部调用的优缺点都与这种发送以太币的方式有关。`call()`上的无限制燃料限制允许接收方拥有更复杂的回退函数，该函数也可以访问合约状态，但出于同样的原因，它使发送方面临潜在的恶意外部操纵风险。

|  |
| --- |

##### 提示

执行以太币转账最安全的方式是通过`send()`或`transfer()`执行，并且相应地使其完全与任何业务逻辑解耦。

|  |
| --- |

#### 14.2.3\. 如果外部调用失败，是否会抛出异常？

从外部调用出错时的行为角度来看，你可以将调用执行类型分为原始和安全的。我将在这里讨论这些类型，然后继续讨论可以执行调用的不同上下文。

##### 原始调用

大多数调用执行类型都被认为是*原始*的，因为如果外部函数抛出异常，它们会返回一个布尔`false`结果，但不会自动回滚合约状态。因此，如果在失败调用后没有采取任何行动，调用合约的状态可能是不正确的，你发送的任何以太币都会丢失，而没有产生预期的经济效益。以下是一些未处理的外部调用的示例：

```
externalContractAddress.send(etherAmount);          *1*

externalContractAddress.call.value(etherAmount)();  *2*

externalContractAddress.call.value(etherAmount)(
    bytes4(sha3("externalFunction()");              *3*
```

+   ***1*** **如果 send()失败并且没有处理，以太币金额会丢失；转移到外部回退函数的 2,300 燃料预算也会丢失。**

+   ***2*** **如果 call()失败并且没有处理，以太币金额会丢失；所有的燃料都会转移到外部回退函数并且丢失。**

+   ***3*** **如果外部函数失败，发送的以太币金额不会返回并且丢失；转移给外部函数的所有燃料也同样丢失。**

在外部调用失败后，你有两种方法可以回滚合约状态。你可以使用`require`或`revert()`。

如果在错误发生时手动回滚状态的第一种方法是引入一些状态变量的`require()`条件。你必须设计`require()`条件，使其在外部调用失败时失败，因此合约状态会自动回滚，如下面的片段所示：

```
contract ExternalContract {
   ... 
   function externalFunction payable (uint _input) {
   ...                                                           *1*
   } 
}

contract A {
   ...
   function doSomething ()
   {
      uint stateVariable;

      uint initialBalance = this.Balance;
      uint commission = 60;
      externalContractAddress.call.value(commission)(
           bytes4(sha3("externalFunction()")), 10);            *2*

      require(this.Balance == initialBalance - commission);    *3*
      require(stateVariable == expectedValue);                 *3*
   }
}
```

+   ***1*** **出错了，外部函数抛出了一个异常。**

+   ***2*** **调用了外部函数，在其失败后返回了一个布尔值 false。**

+   ***3*** **针对以太币余额和合约状态设置了两个`require()`条件。如果任何条件不满足，以太币余额和合约状态都会被回滚。**

第二种方法是先执行显式的检查，如果检查不成功，则调用`revert()`，如下面的代码所示：

```
contract ExternalContract {
   ...

   function externalFunction payable (uint _input) {
   ...                                                *1*
   } 
}

contract A {
   uint stateVariable;

   ...
   function doSomething ()
   { 
      uint initialBalance = this.Balance;
      uint commission = 60;

      if (!externalContractAddress.call.value(commission)(
         bytes4(sha3("externalFunction()")), 10))
         revert();
   }
   ...
```

+   ***1*** **出错了，外部函数抛出了一个异常。**

##### 安全调用

有两种外部调用被认为是*安全的*，因为外部调用的失败会将异常传播到调用代码，并且这将回滚合约状态和以太币余额。安全调用的第一种类型是

```
externalContractAddress.transfer(etherAmount);        *1*
```

+   ***1*** **如果 transfer()失败，外部失败将触发一个本地异常，回滚调用合约的状态和余额。**

第二种安全调用类型是对外部合约的高级调用：

```
ExternalContract(externalContractAddress)
    .externalFunction();                      *1*
```

+   ***1*** **如果 externalFunction 失败，这将触发一个本地异常，回滚调用合约的状态和余额。**

|  |
| --- |

##### 提示

建议通过`transfer()`安全调用进行以太币转账，或通过直接高级自定义合约函数进行逻辑执行。避免使用像`send()`进行以太币发送和`call()`进行逻辑执行的不安全调用。如果安全调用失败，合约状态将干净地回滚，而如果安全调用失败，您需要负责处理错误并回滚状态。

|  |
| --- |

#### 14.2.4\. 外部调用是在哪个上下文中执行的？

您可以在*调用合约的上下文中*执行一个调用，这意味着它影响（并使用）调用合约的状态。您还可以在外部合约的*上下文中*执行它，这意味着它影响（并使用）外部合约的状态。

##### 外部合约上下文的执行

如果您浏览表 14.1 的执行上下文列，您会意识到大多数调用执行类型都涉及在外部合约的上下文中执行。以下列表显示了在外部合约上下文中发生的 external call。

##### 列表 14.1\. 外部合约上下文执行示例

```
contract A {
   uint value;                                     *1*
   address  msgSender;                             *1*
   address externalContractAddress = 0x5;

   function setValue(uint _value)
   {
      externalContractAddress.call.(
          bytes4(sha3("setValue()")), _value);     *2*
   }
}

contract ExternalContract {

   uint value;                                     *3*
   address msgSender;                              *3*

   function setValue(uint _value) {
       value = _value;                             *4*
       msgSender = msg.sender;                     *5*
   } 
} 
```

+   ***1*** **状态变量**

+   ***2*** **在外部合约.setValue()上执行的外部调用**

+   ***3*** **在合约 A 上定义的状态变量**

+   ***4*** **修改 ExternalContract.value 并将其设置为 _value**

+   ***5*** **修改 ExternalContract.msgSender 并将其设置为发送到合约 A 的原始 msg.sender。**

通过图 14.5 所示的例子，我将向你展示如何在外部调用列表 14.1 中实现的外部合约调用后，`ContractA`和`ExternalContract`的状态发生变化。

##### 图 14.5\. 外部合约上下文执行示例

![](img/fig14-05_alt.jpg)

例子中使用的用户和合约账户地址总结在表 14.2 中。

##### 表 14.2\. 用户和合约账户地址

| 账户 | 地址 |
| --- | --- |
| user1 | 0x1 |
| user2 | 0x2 |
| ContractA | 0x3 |
| ContractB | 0x4 |
| ExternalContract | 0x5 |

外部调用发生前合约的初始状态总结在表 14.3 中。合约的状态将变为表 14.4 所示的状态。

##### 表 14.3\. 合约的初始状态

|  | ContractA | ExternalContract |
| --- | --- | --- |
| 值 | 16 | 24 |

现在想象一下，user1 在`ContractA`上执行以下调用；例如，从一个网络用户界面，通过 Web3.js，正如你在第十二章所看到的：

```
ContractA.setValue(33)
```

##### 表 14.4. 外部调用之后合同的状态和`msg`对象

|  | ContractA | ExternalContract |
| --- | --- | --- |
| 值 | 16 | **33** |
| msg 发送者 | 0x1 | **0x1** |

总结来说，`ContractA`的状态没有改变，而`ExternalContract`的状态却被修改了，正如表 14.4 所展示的。`ExternalContract`处理的`msg`对象就是用户 1 在调用`ContractA`时生成的原始`msg`对象。

##### 在调用合同中的上下文执行`delegatecall`

通过`delegatecall`的执行是在调用合同的上下文中进行的。下列清单中的代码显示了一个外部合同在调用合同的上下文中发生的外部调用。

##### 清单 14.2. 在调用合同中上下文执行`delegatecall`的例子

```
contract A {
   uint value;                                   *1*
   address msgSender;                            *1*
   address externalContractAddress = 0x5;

   function setValue(uint _value)
   {
      externalContractAddress.delegatecall.(
        bytes4(sha3("setValue()")), _value);     *2*

   }
}

contract ExternalContract {

   uint value;                                   *3*
   address msgSender;                            *3*

   function setValue(uint _value) {
      value = _value;                            *4*
      msgSender = msg.sender;                    *5*
   } 
}
```

+   ***1*** **对外部合同 ExternalContract.setValue () 的调用**

+   ***2*** **对外部合同 ExternalContract.setValue () 的调用**

+   ***3*** **定义为 ContractA 的状态变量**

+   ***4*** **修改 ContractA.value 并将其设置为 _value**

+   ***5*** **修改 ContractA.msgSender 并将其设置为发送到 ContractA 的原始 msg.Sender**

像我之前做的那样，通过图 14.6 这个例子，我会向你展示在清单 14.2 中实现的外部调用之后`ContractA`和`ExternalContract`状态的变化。

##### 图 14.6. 调用合同中执行`delegatecall`的例子

![](img/fig14-06_alt.jpg)

在外部调用发生之前的合同初始状态总结在表 14.5 中。

##### 表 14.5. 合同的初始状态

|  | ContractA | ExternalContract |
| --- | --- | --- |
| 值 | 16 | 24 |

现在想象用户 1 在`ContractA`上执行以下调用，例如，从一个网络 UI 中：

```
ContractA.setValue(33)
```

总结来说，`ContractA`的状态已经被修改，而`ExternalContract`的状态却没有改变，正如表 14.6 所展示的。`ExternalContract`处理的`msg`对象仍然是用户 1 在调用`ContractA`时生成的原始`msg`对象。

##### 表 14.6. 外部通过`delegatecall`调用之后合同的状态和`msg`对象

|  | ContractA | ExternalContract |
| --- | --- | --- |
| 值 | 33 | 24 |
| msg 发送者 | 0x1 | 0x1 |

##### 在调用合同中的上下文执行`callcode`

最后一个要检查的情况是`ContractA.setValue()`的实现使用了`callcode`而不是`delegatecall`，如下所示：

```
function setValue(uint _value)
{
   externalContractAddress.callcode.(bytes4(sha3("setValue()")), _value);
}
```

假设和之前一样的初始状态，在用户 1 的调用后，如图 14.7 所示，合同的状态将变为表 14.7 中所示。

##### 图 14.7. 调用合同中执行`callcode`的例子

![](img/fig14-07_alt.jpg)

##### 表 14.7. 通过`callcode`的外部调用之后合同的状态

|  | ContractA | ExternalContract |
| --- | --- | --- |
| 值 | 33 | 24 |
| msg 发送者 | 0x1 | 0x3 |

正如你所看到的，`callcode`调用的外部函数仍然在调用者的上下文中执行，就像通过`delegatecall`执行调用一样。但是当外部调用发生时，`ContractA`生成了一个新的`msg`对象，消息发送者是`ContractA`。

从安全角度来看，在调用合约的上下文中执行明显比在外部合约的上下文中执行更安全。当在调用合约的上下文中执行时，例如通过`callcode`或`delegatecall`调用外部函数，调用者允许外部合约对其状态变量进行读/写访问。正如你可以想象，仅在有限的情况下才安全这样做，主要是当外部合约在你的直接控制之下（例如，你是合约所有者）。您可以在表 14.8 中找到每种调用类型使用的上下文和`msg`对象的总结。

##### 表 14.8\. 每种调用类型中执行上下文和`msg`对象的总结

| 调用类型 | 执行上下文 | msg 对象 |
| --- | --- | --- |
| 调用 | 外部合约 | 原始 msg 对象 |
| delegatecall | 调用者合约 | 原始 msg 对象 |
| callcode | 调用者合约 | 调用者合约生成的 msg 对象 |
|  |

##### 提示

如果你需要使用`call()`，倾向于通过`call()`在外部合约的上下文中调用，而不是在调用合约的上下文中调用。不过，要注意从 Solidity 0.5 版本开始，`call()`将变得过时。

|  |
| --- |

#### 14.2.5\. 接收到的 msg 对象是什么？

通常，消息对象应该从其创建点流向外部调用链的最后一个合约，这可能跨越多个合约。当通过所有外部调用类型调用外部调用时，这是正确的，除了`callcode`，它生成一个新的消息，正如你在比较`callcode`和`delegatecall`下的外部调用执行时所看到的那样。`delegatecall`操作码是为了修复`callcode`的意外消息创建行为而引入的。因此，您应该尽可能避免使用`callcode`。

|  |
| --- |

##### 提示

尽可能避免`callcode`，选择`delegatecall`。

|  |
| --- |

#### 14.2.6\. 燃料限制是多少？

除了`send()`和`transfer()`对外部调用的燃料限制为 2300 燃料，这仅足以执行以太币传输和日志操作外，所有其他外部调用类型都将原始调用中的全部燃料限制传递给外部调用。如我之前解释过，低燃料限制和高燃料限制都有安全含义，但当涉及到传输以太币时，较低的限制更受欢迎，因为它在以太币处于危险时防止外部操纵。

|  |
| --- |

##### 提示

倾向于较低的燃料限制而不是较高的燃料限制。

|  |
| --- |

### 14.3\. 如何更安全地执行外部调用

你现在应该对每种外部调用类型的特性和权衡有更好的了解，并且你可能能够根据你的需求选择最合适的一种。但是，即使你选择了正确的调用类型，如果你不正确地使用它，你可能会遇到麻烦。在本节中，我将向你展示一些安全执行外部调用的技术。你将看到，即使通过看似安全无害的`transfer()`进行以太币转账，如果你没有考虑所有可能导致调用失败的场景，最终也可能犯下昂贵的错误。

#### 14.3.1\. 实现拉取支付

想象你已经开发了一个拍卖 Dapp，并且你已经实现了一个像开源项目 Ethereum Smart Contract Best Practices 指南中由 ConsenSys 协调的`Auction`合约。我在下面的列表中提供了一个示例。仔细研究这个列表，因为我在本章中会多次引用它。

> ¹
> 
> 参见“Solidity 中的智能合约安全建议”，[`mng.bz/MxXD`](http://mng.bz)， Apache License 2.0 许可。

##### 列表 14.3\. `Auction`合约的不正确实现

```
contract Auction {//INCORRECT CODE //DO NOT USE!//UNDER APACHE LICENSE 2.0
    // Copyright 2016 Smart Contract Best Practices Authors
    address highestBidder;
    uint highestBid;

    function bid() payable {
        require(msg.value >= highestBid);           *1*

        if (highestBidder != 0) { 
           highestBidder.transfer(highestBid);      *2*
        }

       highestBidder = msg.sender;                  *3*
       highestBid = msg.value;                      *3*
    }
}
```

+   ***1*** **如果当前出价不是最高的，则回滚交易**

+   ***2*** **如果当前出价最高，退还给之前的最高出价者**

+   ***3*** **更新最高出价和出价者的细节**

如果其中一个出价者实现了回退函数，如下面的列表所示，然后他们提交了一个比最高出价还要高的出价会发生什么？

##### 列表 14.4\. 恶意合约调用`Auction`合约

```
contract MaliciousBidder {
   address auctionContractAddress = 0x123;
   function submitBid() public {
      auctionContractAddress.call.value(
          100000000000)(bytes4(sha3("bid()")));
   }

   function payable() { 
      revert ();            *1*
   } 
...
}
```

+   ***1*** **此合约每次收到以太币支付时都会回滚其状态并抛出异常。**

一旦`MaliciousBidder`合约通过`submitBid()`提交了最高出价，`Auction.bid()`将退还给之前的最高出价者，然后将最高出价的地址和价值设置为`MaliciousBidder`的地址和价值。到目前为止，一切顺利。接下来会发生什么？

现在有一个新的出价者提出了最高出价。`Auction.bid()`将尝试退还给`MaliciousBidder`，但是下面的代码行失败了，即使新的出价者没有做错任何事，并且`bid()`函数的逻辑似乎是正确的：

```
highestBidder.transfer(highestBid);
```

这个代码行失败是因为当前的`highestBidder`仍然是`MaliciousBidder`的地址，其回退函数在`highestBidder.transfer()`调用时抛出了异常。如果你仔细思考，任何新的出价者都不可能通过这一行，因为在每次尝试退款给`MaliciousBidder`的情况下。同时，`highestBidder.transfer()`的调用将一直失败，在地址和价值更新为新的最高出价之前，如图 14.8 所示。这就是为什么`MaliciousBidder`是恶意的。

那么用`send()`替换`transfer()`怎么样？在`send()`失败后，`bid()`函数将抛出异常。因此，按照推荐的方式使用`send()`而不是`transfer()`，如以下代码行所示，并不能解决问题：

```
require(highestBidder.send(highestBid));
```

##### 图 14.8。在恶意合约成为最高出价者之后，`Auction`合约变得无法使用，因为它会尝试向恶意合约退款（每次新的更高出价都会失败），并且永远无法设置新的最高出价者。

![](img/fig14-08_alt.jpg)

使用您当前的`bid()`实现，您甚至不需要一个恶意的外部出价者合约就会遇到麻烦。此外，任何具有错误`fallback()`的外部出价合约抛出的非故意异常都可能颠覆船只。例如，一个粗心的出价合约开发者，没有意识到与`transfer()`（或`send()`）相关的气体限制，可能已经决定实现一个复杂的回退函数，如以下代码所示，该函数接受退款并通过修改其自己的合约状态来处理它。这将进而耗尽`transfer()`的 2,300 气体配额，并几乎立即抛出一个“气体耗尽”的异常：

```
function () payable() {
      refunds +=  msg.value;       *1*
}
```

+   ***1*** **一旦状态变量 refund 被更新，函数执行就会耗尽`transfer()`施加的 2,300 气体配额并失败。**

正如您所见，`bid()`的当前实现严重依赖于您正在与诚实和有能力的外部合约开发者合作的假设。这可能并不总是实际情况。

接受出价的一种更安全的方法是将更新最高出价者的逻辑与向前任最高出价者执行退款分离。现在退款不再自动推送到前任最高出价者，而应该通过单独的请求由他们拉取，如下面的列表所示。（这个解决方案也来自我之前提到的 ConsenSys 指南。）

##### 列表 14.5。`Auction`合约的正确实现

```
//UNDER APACHE LICENSE 2.0
//Copyright 2016 Smart Contract Best Practices Authors
//https://consensys.github.io/smart-contract-best-practices/
contract Auction {
    address highestBidder;
    uint highestBid;
    mapping(address => uint) refunds;

    function bid() payable external {
         require(msg.value >= highestBid);

        if (highestBidder != 0) {
            refunds[highestBidder] += highestBid;     *1*
        }

        highestBidder = msg.sender;                   *2*
        highestBid = msg.value;                       *2*
    }

    function withdrawRefund() external {
        uint refund = refunds[msg.sender];
        refunds[msg.sender] = 0;
        msg.sender.transfer(refund);                  *3*
        }
    }
}
```

+   ***1*** **现在这个函数只存储因新的更高出价者而产生的退款金额。没有以太币的转移。**

+   ***2*** **现在更新新的最高出价和出价者将会成功，因为`bid()`不再包含可能被劫持的外部操作，例如之前的`transfer()`调用。**

+   ***3*** **如果这个转移失败——例如，当支付给 MaliciousBidder 时——`Auction`合约的状态现在不受影响。**

拉取支付在函数执行循环中执行多次支付时也很有用。一个例子可能是退款所有投资者在失败的众筹中的账户，如下面的列表所示。

##### 列表 14.6。一个执行多次支付的函数的不正确实现

```
contract Crowdsale {
   address[] investors;
   mapping(address => uint) investments;

   function refundAllInvestors() payable onlyOwner external {
      //INCORRECT CODE //DO NOT USE!

      for (int i =0; i< investors.length; ++i) {
         investors[i].send(investments[investors[i]]);     
    }
}
```

如果攻击者从一个很高的账户数量中进行非常小的投资，投资者数组中的项目数量可能会变得如此之大，以至于 `for` 循环在完成之前会耗尽燃料，因为循环的每一步都有固定的燃料成本。这是一种利用燃料限制的 DoS 攻击。一个更安全的实现是，在 `refundAllInvestors()` 中只保留退款分配，并将以太币转账操作移动到一个名为 `withdrawalRefund()` 的单独提取支付函数中。这与你在 `Auction` 合约中看到的类似，正如你在下面的清单中所看到的。

##### 清单 14.7. 改进的 `refundAllInvestors()` 实现

```
contract Crowdsale {
   address[] investors;
   mapping(address => uint) investments;
   mapping(address => uint) refunds;

   function refundAllInvestors() payable onlyOwner external {

      for (int i =0; i< investors.length; ++i) {
         refunds[investors [i]] = investments[i];
         investments[investors[i]] = 0;     
      }
   }

   function withdrawRefund() external {
      uint refund = refunds[msg.sender];
      refunds[msg.sender] = 0;
      msg.sender.transfer(refund); 
   }
}    
```

#### 14.3.2. 实现一个最小的回退函数

尽管从合约转移以太币的角度来看，提取支付是一个不错的解决方案，但设身处地为出价者考虑一下。如果你期望从外部合约（如拍卖合约）获得以太币，不要假设外部合约实现了安全的提取支付功能，正如清单 14.7 所示。相反，假设外部合约是以一种次优的方式实现的，就像你之前看到的[清单 14.6] 中的初始实现。在这种情况下，如果你想确保使用 `transfer()`（或 `send()`）执行的退款操作成功，你必须提供一个最小的回退函数：为空或者最多包含单个日志操作，如图所示：

```
function() public payable {}
```

#### 14.3.3. 小心通过 `selfdestruct()` 来到你这里的以太币

不幸的是，你不能确保你的合约不会从未知来源接收以太币。你可能会认为，拥有一个总是在被调用时抛出异常或回滚合约状态的回退函数，如所示，应该足以阻止这种不受欢迎的以太币流入：

```
 function() public payable {revert ();}
```

但是，我担心有一种方法可以将以太币转移到任何地址，而不需要在接收方实现任何可支付函数——甚至不需要回退函数。这可以通过调用

```
selfdestruct(recipientAddress);
```

`selfdestruct()` 函数是为了在紧急情况下提供一种摧毁合约的方法，并通过同一操作，将合约账户关联的所有以太币转移到指定地址。通常，这会在发现关键错误或合约被黑客攻击时执行。

不幸的是，`selfdestruct()` 也容易遭到滥用。如果外部合约包含至少 1 Wei 并自我销毁，目标是你的合约地址，你几乎无能为力。你可能会认为接收不受欢迎的以太币不是一个严重的问题，但如果你的合约逻辑依赖于对以太币余额的检查和协调，例如，通过 `require()`，你可能会有麻烦。

### 14.4. 避免已知的网络安全攻击

现在我们已经回顾了与外部调用相关联的 Solidity 已知的安全漏洞，接下来是分析利用这些弱点的已知攻击。你可以根据攻击者的高级目标，把 Solidity 合约的攻击分为三大类。目标是

+   操纵单个交易的输出结果

+   偏袒某笔交易

+   使合约不可用

表 14.9 总结了与每种攻击类别相关的操纵技术。接下来的几节将定义并详细介绍表中包含的每种攻击技术。

##### 表 14.9. 安全攻击、策略和技术

| 攻击目标 | 攻击策略 | 攻击技术 |
| --- | --- | --- |
| 个别交易操纵 | 竞态条件 | 重入，跨函数竞态条件 |
| 偏袒某笔交易 | 抢跑 | 抢跑 |
| 使合约不可用 | 服务拒绝 | 回退调用 revert()，利用燃料限制 |
|  |

##### 警告

本节只涵盖最常见的攻击，主要是让你了解恶意参与者如何操纵合约。此外，新的安全攻击正在不断被发现，因此你必须通过查阅官方 Solidity 文档和其他许多涵盖该主题的网站和博客，了解并不断更新最新的安全漏洞。我会在第 14.5 节中为你指出一些资源。

|  |
| --- |

#### 14.4.1. 重入

重入攻击针对包含外部调用的函数，并利用此函数同时调用之间可能发生的时间延迟引起的竞态条件。攻击的目标通常是操纵合约的状态，通常与 Ether 或自定义加密货币余额有关，通过同时多次回调目标函数，而攻击者劫持外部调用的执行。如果我们回到我之前向你展示的拍卖 Dapp 的例子，攻击者可以通过并行地多次请求退款，同时劫持每个退款调用，对`withdrawRefund()`的错误实现发起重入攻击，如图 14.9 所示。

##### 图 14.9. 如果你错误地实现`Auction.withdrawRefund()`，例如，在 Ether 转移完成后才清除调用者的余额，攻击者可以并行地多次调用它，同时劫持每个调用，通过减慢接收`fallback()`函数的执行。这些同时的 Ether 转移被允许，并且可以成功完成，直到其中一个最终完成并清除调用者的余额。在这之前，可能会发生许多不正当的退款。

![](img/fig14-09_alt.jpg)

以下代码展示了`withdrawRefund()`的错误实现（也来自 ConsenSys 指南），这将使你的合约处于危险之中：

```
function withdrawRefund() external { {//INCORRECT CODE //DO NOT USE!
    // UNDER APACHE LICENSE 2.0
    // Copyright 2016 Smart Contract Best Practices Authors
   uint refund = refunds[msg.sender];
   require (msg.sender.call.value(refund)());     *1*
   refunds[msg.sender] = 0;                       *2*
}
```

+   ***1*** **对外部合约回退函数的调用可能会相对较慢**

+   ***2*** **仅在之前的 external call 完成后执行**

正如我提到的，攻击者合约可能会在劫持每个执行支付的回退函数的外部调用时多次调用`withdrawRefund()`，如下所示：

```
contract ReentrancyAttacker {
   function() payable public () {
     uint maxUint = 2 ** 256 - 1;
     for (uint I = 0; i < maxUint; ++i)
     { 
        for (uint j =0; j  < maxUint; ++j)
        {
           for  (uint k =0; k < maxUint; ++k)       *1*
           {
                ...
     }
}
```

+   ***1*** **回退函数中只包含延迟完成的代码。在它完成之前，攻击者多次调用 withdrawRefund()。**

以太币转账的这种缓慢执行将阻止`withdrawRefund()`在很长时间内达到清除调用者余额的代码行：

```
refunds[msg.sender] = 0;
```

在这行代码之前，可能会发生各种以太币转账，每个转账金额都与调用者应得的金额相等。因此，调用者可能会收到比应得的更多的以太币，如图 14.10 中的序列图所示。

|  |
| --- |

##### 注意

我之所以想在本书中包含来自 ConsenSys 指南的拍卖 Dapp，特别是其`withdrawRefund()`函数的错误实现，是因为这段代码展示了导致 DAO 攻击最初成功的其中一个漏洞。

|  |
| --- |

##### 图 14.10. 攻击者并行调用`withdrawRefund()`错误实现的序列图

![](img/fig14-10_alt.jpg)

你可以使用以下几种方法防止这种攻击：

+   如果你能的话，使用`transfer()`或`send()`而不是`call.value()()`，这样攻击者的 gas 限制将是 2300，从而阻止他们在`fallback()`函数中实现任何转账延迟代码。

+   将执行以太币转账的外部调用作为最后操作，这样在调用发生前而不是发生后清空以太币余额，正如列表 14.8 所示。如果攻击者再次尝试调用`withdrawRefund()`，`refunds[msg.sender]`的值将变为零，因此退款也将被设置为零。因此，新的以太币支付将不会产生任何效果。

##### 列表 14.8. `withdrawRefund()`的正确实现

```
function withdrawRefund() external {
   uint refund = refunds[msg.sender];
   refunds[msg.sender] = 0;
   require (msg.sender.call.value(refund)());         *1*
}
```

+   ***1*** **现在转账在余额被清空后进行，所以随后调用 withdrawRefund()将没有效果。**

#### 14.4.2. 跨函数竞态条件

你已经了解到，重入攻击利用了同一函数同时调用的竞态条件。但攻击者也可以利用尝试修改同一合同状态的分离函数之间的竞态条件——例如，特定账户的以太币余额。

在`SimpleCoin`上，跨竞态条件也可能发生。回顾`SimpleCoin`的`transfer()`函数：

```
function transfer(address _to, uint256 _amount) public {
    require(coinBalance[msg.sender] > _amount);
    require(coinBalance[_to] + _amount >= coinBalance[_to] );
    coinBalance[msg.sender] -= _amount;  
    coinBalance[_to] += _amount;   
    emit Transfer(msg.sender, _to, _amount);  
}
```

现在，想象一下你决定提供一个`withdrawFullBalance()`函数，该函数关闭调用者的 SimpleCoin 账户，并将等值的以太币发送给他们。如果你像下面这样实现这个函数，你会使合约面临潜在的跨函数竞态条件：

```
function withdrawFullBalance() public {//INCORRECT CODE //DO NOT USE!
    uint amountToWithdraw = coinBalance[msg.sender] * exchangeRate;
    require(msg.sender.call.value(
        amountToWithdraw)());               *1*
    coinBalance[msg.sender] = 0;
}
```

+   ***1*** **攻击者在执行 withdrawFullBalance()函数时调用 transfer()函数。**

跨函数竞态条件攻击的方式与之前看到的递归性攻击类似。攻击者首先调用`withdrawFullBalance()`，在他们从回退函数中劫持外部调用时，他们会调用`transfer()`，将完整的 SimpleCoin 余额移动到他们拥有的另一个地址，在`withdrawBalance()`执行清除这个余额之前。这样，他们既能保留完整的 SimpleCoin 余额，又能得到等值的以太币金额：

```
contract RaceConditionAttacker {
   function() payable public () {
      uint maxUint = 2 ** 256 - 1;
         for (uint I = 0; i < maxUint; ++i)
         { 
            for (uint j =0; j  < maxUint; ++j)
            {
               for   (uint k =0; k < maxUint; k++)
               {
                  ...
     }
}
```

解决方案，正如递归性攻击的情况一样，用`send()`或`transfer()`替换`call.value()()`。你还需要确保执行余额提现的外部调用发生在函数的最后一行，在调用者余额已经被设置为 0 之后：

```
function withdrawFullBalance() public {
    uint amountToWithdraw = coinBalance[msg.sender];
    coinBalance[msg.sender] = 0;
    require(msg.sender.call.value(
        amountToWithdraw)());              *1*
}
```

+   ***1*** **现在外部调用在调用者余额被清除之后执行。**

更复杂的递归性攻击案例涉及多个合约之间的调用链。一般的建议总是将外部调用或包含外部调用的函数放在函数体的最后。

#### 14.4.3. 前置运行攻击

到目前为止你所看到的基于竞态条件的攻击试图通过改变交易的预期执行流程来操纵交易的结果，通常是通过劫持在外部执行的部分。

其他的攻击策略在更高层次，针对的是交易执行顺序重要的去中心化应用。攻击者试图通过偏袒和优先处理某些交易来影响交易执行的时间或顺序。例如，一个恶意矿工可能会在内存池中发现许多对某只股票的买入订单时，创建新的买入订单交易。矿工会将他们自己的买入订单交易包含在新块中，这样他们的交易就会在内存池中任何其他类似订单之前执行，如图 14.11 所示。如果矿工的 PoW 成功，他们的买入订单就会成为正式的。随后，由于提交了许多但尚未执行的买入订单，股票价格会上涨。这将给矿工带来即时利润。

##### 图 14.11\. 前端运行攻击的一个例子。恶意矿工可以检测到发送到股票市场制造 Dapp 且仍处于内存池中的大买入或卖出订单。他们可以决定通过忽略这些大订单并在尝试创建的新区块中包含自己的订单来前端运行它们，如果区块被挖出，他们就能获得不公平的利润。

![](img/fig14-11_alt.jpg)

这种操纵是*前端运行*的一个例子，这是恶意股票经纪人将他们自己的订单执行放在客户订单之前的行为。避免这种攻击的方法之一是设计基于*批量执行*的订单清算逻辑，而不是单个执行，实现方式与批量拍卖类似。采用这种设置，拍卖合约收集所有出价，然后通过单一操作确定赢家。另一种解决方案是实现一个类似于本章早期描述的提交-揭示方案，以掩盖订单信息。

#### 14.4.4\. 基于 revert()的 DoS 攻击

一些攻击旨在完全摧毁合约，这些被称为服务拒绝（DoS）攻击。

正如我在本章开头在`Auction`合约中向你展示的，攻击者可以通过实现以下回退函数，然后以触发传入支付的方式调用目标合约，从而使合约无法使用：

```
function payable() { 
   revert ();              *1*
} 
```

+   ***1*** **每当此合约收到以太币支付时，它将回滚其状态并抛出异常。**

如果目标合约实现了如下所示的函数，那么它在尝试向攻击者发送以太币时将变得无法使用：

```
function bid() payable {//INCORRECT CODE//DO NOT USE!
   //UNDER APACHE LICENSE 2.0
   //Copyright 2016 Smart Contract Best Practices Authors

   require(msg.value >= highestBid);          *1*

   if (highestBidder != 0) { 
      highestBidder.transfer(highestBid));    *2*
   }

   highestBidder = msg.sender;                *3*
   highestBid = msg.value;                    *3*
}
```

+   ***1*** **检查当前出价是否高于当前最高出价**

+   ***2*** **前一个最高出价者将被退款，但当前一个最高出价者是恶意合约时，转账失败，无法再设置新的最高出价者和出价值.**

+   ***3*** **设置新的最高出价者和出价值**

正如你所知，你可以通过实现拉取支付功能而不是自动推送支付来避免这种攻击。（更多详情请参见 14.3.1 节）

#### 14.4.5\. 基于燃料限制的 DoS 攻击

在拉取支付部分，你看到了一个错误实现的函数，该函数在众筹失败时向所有投资者退款示例：

```
contract Crowdsale {
   address[] investors;
   mapping(address => uint) investments;

   function refundAllInvestors() payable onlyOwner external {
      //INCORRECT CODE //DO NOT USE!    
      for (int i =0; i< investors.length; ++i) {
         investors[i].send(investments[investors[i]]);     
    }
}
```

我已经警告过你，这个实现方式容易受到攻击者通过从一个很高的账户中进行非常小的投资来进行操纵。大量投资数组所需的`for`循环数量将永久损害合约，因为任何函数的调用都会耗尽燃料限制。这是一种利用燃料限制的 DoS 攻击。基于拉取支付功能的退款也能防止这种攻击。

你已经了解了与外部调用相关的陷阱以及如何避免最常见的安全攻击形式。现在，我将通过分享一些我从各种来源收集的安全建议来结束本章。

### 14.5 通用安全指南

官方 Solidity 文档有一个完整的部分致力于安全考虑和建议，^([2])在将您的合约部署到公共网络之前，我建议您参考该部分。还有其他优秀的资源，例如由 Diligence([`consensys.net/diligence/`](https://consensys.net/diligence/))部门发起和维护的开源*以太坊智能合约最佳实践*指南([`mng.bz/dP4g`](http://mng.bz/dP4g))，该指南专注于安全并旨在提高在此领域的最佳实践方面的意识。我在本章的各个地方引用了这本指南，它被认为是以太坊安全的主要参考资料。我决定采用其术语，以确保您如果决定想了解更多关于我这里涵盖的内容，可以轻松查找概念。|

> ²
> 
> 参见“安全考虑”中的[`mng.bz/a7o9`](http://mng.bz/a7o9)。

在表 14.10 中，我列出了 ConsenSys Diligence 创建的另外一些有用的免费以太坊安全资源。Ethereum 的 Solidity 负责人 Christian Reitwiessner 的演讲和帖子也是必读的。|

> ³
> 
> 参见“智能合约安全”，2016 年 6 月 10 日，[`mng.bz/GWxA`](http://mng.bz/GWxA)和“如何编写安全的智能合约”，2015 年 11 月 10 日，[`mng.bz/zMx6`](http://mng.bz/zMx6)。

##### 表 14.10. ConsenSys Diligence 分发的以太坊安全资源|

| 资源 | 描述 |
| --- | --- |
| 安全的智能合约哲学¹ | ConsenSys Diligence 在 Medium 上发表的一系列文章，介绍如何对待智能合约安全 |
| EIP 1470: SWC² | 对智能合约的标准化弱点分类，使工具供应商和安全从业者可以以更一致的方式对弱点进行分类 |
| 0x 安全审计报告³ | ConsenSys 0x 智能合约系统的全面安全审计，由 ConsenSys Diligence 执行。这为您提供了一个在彻底的安全审计中评估弱点的良好思路。 |
| 审计准备指南⁴ | 关于如何为智能合约安全审计做准备的指导方针 |
| 1. 参见“构建安全的智能合约哲学”，[`mng.bz/ed5G`](http://mng.bz/ed5G)。 |
| 2. 参见这些 GitHub 页面：[`github.com/ethereum/EIPs/issues/1469andhttp://mng.bz/pgVR`](https://github.com/ethereum/EIPs/issues/1469andhttp://mng.bz/pgVR)。 |
| 3. 参见 http://mng.bz/O2Ej。 |
| 4. 参见 Maurelian 的“为智能合约代码审计做准备”，2017 年 9 月 6 日，[`mng.bz/YPqj`](http://mng.bz/YPqj)。 |

我会用一个简短的列表总结所有我提到的资源倾向于同意的最重要观点。不过，我要重申，不断跟上最新的安全漏洞和被发现的漏洞，如[`hackingdistributed.com`](http://hackingdistributed.com)，[`cryptonews.com`](https://cryptonews.com)，或[`cryptoslate.com`](https://cryptoslate.com)等网站的信息是非常重要的。列表如下：

+   **优先设计简单的合约**。通常适用于面向对象类的相同设计建议也适用于智能合约。力求小型合约，专注于单一功能，状态变量数量少，函数简短。这将帮助你避免错误，并帮助其他开发者正确理解你的代码。

+   **修正引发编译器警告的代码**。理解任何编译器警告并相应修正你的代码。如果可能的话，力求移除你收到的所有警告，尤其是与弃用功能相关的。Solidity 语法经常因为安全问题而修改，所以要认真对待警告的建议。

+   尽可能晚地*调用外部合约*。正如你在关于重入性的章节中学习到的，你应该避免在从外部调用返回后改变你的合约状态。这次调用可能会被劫持，你可能无法安全地返回。建议采用的模式称为*检查-效果-交互*，根据这个模式，你应按照以下有序步骤结构一个函数：

    +   **检查**—验证消息发送者是授权的，函数输入参数有效，转移的以太币可用等。你通常直接通过`require`语句或间接通过函数修饰符来做这个。

    +   **效果**—根据验证过的函数输入改变你的合约状态。

    +   **交互**—使用新的合约状态调用外部合约或库。

+   规划灾难。正如你在上一章所学的，一旦合约部署完成，你就无法修改它。如果你发现了一个错误，或者是更糟糕的安全漏洞，并且 Ether 处于风险之中，你不能像对待传统的集中式应用程序那样应用热修复。你应该提前为此可能性做好准备，并为合约所有者提供一个紧急函数，如`freeze()`或`selfDestruct()`，正如我在第六章和第七章介绍`Simple-Crowdsale`时提到的那样。这些函数可以暂时禁用合约，直到你理解了缺陷，或者甚至永久性地禁用。一些开发者采取了更为主动的方法，并在每个合约函数的预先或后置条件检查的基础上实现了自动冻结（或安全保护）功能。如果条件未满足，合约将进入安全保护模式，其中所有或大部分其功能被禁用。无论你决定为你的合约配备交互式或自动紧急停车装置，理想情况下你也应该计划一个升级策略，正如我在第十三章讨论的那样。

+   使用代码审查工具。代码审查工具是一种静态代码分析工具，旨在捕捉违反推荐风格、高效实现或已知安全漏洞的情况。Solidity 最著名的两个代码审查工具是 Solium（现在称为 Ethlint）([`github.com/duaraghav8/Solium`](https://github.com/duaraghav8/Solium))和 Solint([`github.com/SilentCicero/solint`](https://github.com/SilentCicero/solint))。它们都为大多数常见的通用代码编辑器（如 Atom、Sublime、VS Code 和 JetBrains IDEA）提供了集成插件。除了突出安全漏洞外，这些工具还提供了关于编码风格和最佳实践的反馈，因此它们可以帮助你快速学习 Solidity。

+   使用安全分析框架。如果你想要更进一步，不要止步于代码审查工具。相反，目标应该是在你的开发周期中整合安全分析，使用诸如 Mythril 平台，^([4])它结合了各种静态和动态分析器。

    > ⁴
    > 
    > 参见 Bernhard Mueller，“MythX 正在提升智能合约安全游戏的水平，”[`mng.bz/0WmE`](http://mng.bz/0WmE)，了解 Mythril 的入门知识。

+   遵循群体智慧。如果你对你想要连接的智能合约的安全性不够自信，你可以查阅 Panvala 的评分，^([5])这是一个试图从用户那里收集智能合约安全级别的系统。

    > ⁵
    > 
    > 参见“介绍 Panvala，”[`mng.bz/K1Mg`](http://mng.bz/K1Mg)，了解 Panvala 的入门知识。

+   ```Commission a formal security audit```. If your smart contract handles anything valuable, such as cryptocurrency or tokens, before going into production you should consider commissioning a formal security audit from one of the many consultancies that are starting to specialize in this area.

### 总结

+   攻击者通常会利用 Solidity 语言、EVM 和区块链中的限制作为对不知情的开发者的第一攻击线，特别是在数据隐私、随机数、整数溢出和燃料限制等方面。

+   如果不被充分理解，外部调用可能会使合约受到恶意参与者的操纵。例如，一些外部调用会抛出异常，而另一些则不会，或者一些在调用者合约的上下文中执行，而另一些则在被调用合约的上下文中执行。你必须了解每种类型的风险，并相应地处理返回值和合约状态。

+   有多种技术可用于执行更安全的远程调用并减少外部操纵的机会。例如，拉取支付（而不是自动支付）功能以及基于`transfer()`和`send()`的以太币传输，后者在外部回退函数上限制了燃料限制。

+   最基本的防御线是要至少准备好防御已知攻击，比如重入攻击、抢跑攻击和服务拒绝（DoS）攻击。

+   官方 Solidity 文档和各种在线安全指南、网站和博客提供了关于最新攻击和避免它们的指南的最新信息。

## 第十五章。结论

| ``` |
| --- |

**本章内容**

+   以太坊的演变

+   以太坊替代实现

+   超越以太坊区块链的能力

| ``` |
| --- |

你终于读完了这本书。我相信你已经学到了很多知识，现在你应该感觉到有装备可以自己继续旅程了。不过，你不要沾沾自喜。以太坊及其周围的环境都在不断变化。

在我告别之前，我想提醒你，如果你正在考虑构建自己的 Dapp，你应该特别关注一些话题。我还想简要向你介绍一些主流以太坊的分叉，以防主流实现无法满足你的需求。最后，我会给你一个区块链现状的快速概述，以防你想探索其他区块链产品。

在开始之前，我想澄清一点：本章只是为了给你提供进一步学习的想法，所以我不会深入覆盖任何话题。我只试图激发你的思想和热情。

### 15.1。以太坊的演变

正如我在书中多次重复的那样，以太坊在不断发展，在这个阶段，它的许多构件仍然在变化中，比如 EVM、Solidity 语言、Web3.js 库、共识算法以及生态系统的一些元素。我会给你一个这些元素可能如何演变的概述，但我强烈建议您通过在线资源保持更新。

#### 15.1.1 节：EVM 的演变

当前的 EVM 实现支持动态跳转（这意味着地址作为栈上的参数提供），但这会使控制流和数据流分析变得复杂且缓慢。以太坊改进提案 615（EIP 615）([1])旨在对 EVM（版本 1.5）进行部分重新设计，引入子例程（通过静态跳转和`return`）并禁止动态跳转和其他栈的滥用。这将带来几个好处，包括更好的 Solidity 到原生代码的编译、更快的解释、改进到原生代码的优化，以及更好的静态分析和形式验证工具。它还将允许更好的 Solidity 到 eWASM 的编译。

> ¹
> 
> 请参阅 GitHub 上的 EIPs/eip-615.md 文件，网址为[`mng.bz/9OMq`](http://mng.bz/9OMq)。

如果你想知道 eWASM 是什么，WASM 代表 WebAssembly([`webassembly.org/`](https://webassembly.org/))，它是一种新的二进制指令格式，W3C 正在将其设计为开放标准。这个标准定义了一个指令集、一个中间源格式（WAST）和一个二进制编码格式（WASM）。包括 Node.js、Chrome、Edge 和 Firefox 在内的主流 JavaScript 引擎将提供对 WebAssembly 的本地支持。eWASM([`github.com/ewasm`](https://github.com/ewasm))是 WASM 的一个子集，旨在支持以太坊智能合约。最终目标是，提供库和指令，以便用 C 和 Rust 编写以太坊合约。

#### 15.1.2 节：Solidity 的演变

如果你是本书 MEAP 读者之一，你可能会注意到自从你开始研究 Solidity 以来，它已经发生了许多变化。Solidity 开发者经常引入新关键字并废弃旧关键字。这种持续的演变使 Solidity 成为一个更健壮的语言，特别是在安全方面。目前正在发生的最重大变化是`send()`和`call()`的废弃，所以我强烈鼓励你使用`transfer()`。

#### 15.1.3 节：Web3.js 的演变

虽然在这本书中我一直引用 Web3.js 版本 0.24，因为它能与所有现有工具可靠地工作，但您应该尽可能快地尝试升级到版本 1.0。截至写作时，它仍处于测试阶段，但候选版本即将发布。

#### 15.1.4 节：共识算法的演变

主网络（MAINNET），公共生产网络，仍然基于工作量证明（PoW）共识算法。正如您可能回忆起来的，PoW 算法设计成让许多矿工竞争性地将新区块添加到区块链上，同时尝试解决一个密码学难题。他们不断重新哈希拟议的新区块，直到找到一个*nonce*，它生成了一个正确的哈希值（例如，一个有很多前导零的哈希值）。哈希过程是 CPU 密集型的，因此也是能耗密集型的。在整个以太坊网络上每秒执行万亿次的新区块同时重新哈希操作，已经被广泛指责为能源浪费。开发者正在尝试几种替代的共识算法来解决这一问题，即*权益证明*（PoS）和*权威证明*（PoA）。

##### 权益证明（Proof of Stake，PoS）

权益证明算法*（Proof of Stake algorithm）*设计成在一定时间槽内只有唯一一个矿工有权添加一个新区块。因此，整个网络每几秒钟处理一次新区块，而不是每秒万亿次，这消除了电力消耗的问题。如您所想象的，在这种算法下，“矿工”这个术语不再适用：添加区块的候选者被称为*验证者*，如图 15.1 所示。

> ²
> 
> 有关权益证明的常见问题，请参阅 GitHub 上以太坊维基的“Proof of Stake FAQs”页面：[`mng.bz/jO48`](http://mng.bz/jO48)。

##### 图 15.1\. 权益证明与工作量证明对比。在 PoW 下，许多矿工同时执行工作（消耗电力）以添加一个区块，而在 PoS 下，在一个时间槽内只有一个节点，称为验证者，提出一个新的区块。

![](img/fig15-01_alt.jpg)

验证者向以太坊提交存款，这笔存款代表了他们在基础设施中的股份。通过一个随机数生成器或按股份权重轮询函数选出的验证者提出一个新的区块。然后，根据 PoS 算法的具体实现，验证者将拟议的区块提交给几个次级验证者以求得批准。他们就区块进行投票（投票可能会根据他们的股份加权），如果结果是积极的，该区块将被添加到区块链上，并奖励以太坊给验证者。另一方面，如果区块被证明是错误的，初始（主）验证者可能会被列入黑名单并失去他们的存款。此外，次级验证者也鼓励诚实：如果他们的投票与同行的投票相差太大，他们可能会受到惩罚并失去部分存款，正如您在图 15.2 中所看到的。

PoS 算法，及其激励和抑制措施，可能提供各种好处，例如减少网络对先进硬件的依赖，降低由少数矿工进行集中处理的风险，以及降低 51% 攻击的可能性（这将变得非常昂贵）。PoS 算法的项目名称是 Casper，该项目在 2018 年 1 月发布了一个测试网络。

##### 图 15.2. PoS 算法。首先，验证者提交一笔存款。然后，被选中的验证者提出一个新的区块并提交给次级验证者审批。如果他们认为这个区块是正确的，它就会被添加到区块链上。如果主验证者或次级验证者被发现不诚实，他们可能会在以太币上受到惩罚。

![](img/fig15-02_alt.jpg)

##### Proof of Authority

许多实践者和研究者批评了 PoS 激励措施的本质，认为它可能是不平衡的，因为它没有考虑到每个验证者的总持有量。例如，一个国家赞助的验证者可能已经承诺了一定数量的以太币，而这个数量对于算法的设计者来说被认为是大的。但是，如果与他们的总资产（包括加密货币和传统资产）的价值相比，这个数量相对较小，他们可能不会被阻止行为不诚实。

证明 of Authority*^([3]) 是一种基于验证者池的共识算法的替代形式，但在这个情况下，每个验证者投入的是他们的声誉而不是他们的以太币。想要加入验证者池的节点需要通过正式的识别过程：他们披露他们的真实身份，这通过与传统公证人相同的方式来验证。一旦一个节点被批准为验证者，它就成为了一个*权威*（因此这个算法的名称）。该算法的核心思想是将区块验证过程与节点的声誉而不是他们存款的预期价值相链接，这更为健壮，如图 15.3 所示。

> ³
> 
> 请参阅维基百科的“Proof-of-Authority”页面：[`en.wikipedia.org/wiki/Proof-of-authority`](https://en.wikipedia.org/wiki/Proof-of-authority)。

##### 图 15.3. PoA 与 PoS 对比。在 PoS 下，一个恶意节点失去他们的以太币存款后，他们的赞助商可以建立一个新的节点并继续恶意行为。在 PoA 下，一旦发现一个权威节点具有恶意，他们的赞助商（及其所有相关身份）将无法重新进入网络。

![](img/fig15-03_alt.jpg)

目前，两个公共测试网络支持 PoA 的不同实现：Rinkeby 和 Kovan。2018 年 8 月，微软在 Azure 上发布了 Ethereum PoA，针对私人化和联合授权的网络。（更多有关授权网络的详细信息请参见第 15.2 节。）

#### 15.1.5. 生态系统的发展

我在第九章中介绍的以太坊生态系统的许多组件都在发展变化。例如，在 ENS 网站上([`ens.domains/`](https://ens.domains/)），你可以找到一个路线图，指示目前基于提交-揭示拍卖的生产 ENS 注册商将在未来几个月内被简化版本所取代。另外，Swarm 团队发布了一个未来发展的路线图^([4])，用于去中心化文件系统。更戏剧性的变化是 Zeppelin。最初作为一个开源的以太坊智能合约库，现在正在发展成为 ZeppelinOS([`zeppelinos.org/`](https://zeppelinos.org/)），一个为智能合约提供完整功能的操作系统。

> ⁴
> 
> 请参见 GitHub 上的 Swarm“路线图”[`github.com/ethersphere/swarm/wiki/roadmap`](https://github.com/ethersphere/swarm/wiki/roadmap)。

### 15.2. 替代以太坊实现

虽然你可能被这项技术迷住了，但如果你在企业工作，你可能会认为以太坊很难采用。一个很好的原因是，它没有提供开箱即用的三个企业应用程序最需要的特性：可扩展性、权限管理和数据隐私。企业以太坊联盟是一个试图将此类特性扩展到公共以太坊实现的机构。

#### 15.2.1. 企业以太坊联盟

企业以太坊联盟（EEA）([`entethalliance.org/`](https://entethalliance.org/)）是一个由约 500 家公司组成的非盈利性组织，该组织于 2017 年 3 月由 30 个创始成员组成，包括科技公司（微软、英特尔），研究机构（丰田研究院），咨询公司（德勤、埃森哲、三星 SDS）以及金融机构（桑坦德银行、ING）。该组织的任务是提出并推动企业特性和需求路线图；塑造围绕开源技术的许可治理模型；为企业提供资源，帮助它们学习以太坊并解决可以利用该技术的行业用例。

企业以太坊联盟发布了企业以太坊架构堆栈（EEAS），该堆栈提供了一个标准化的企业以太坊生态系统视图，从网络层到应用层。这在表 15.1 中有所说明，该表比较了公共以太坊构建模块与企业以太坊对应的构建模块。（更全面的视图可在官方文档中找到。）

##### 表 15.1. 公共以太坊与企业以太坊构建模块对比

| 级别 | 公共以太坊 | 企业以太坊 |
| --- | --- | --- |
| 权限和凭证 | 密钥管理 | 权限和认证 |
| 集成和部署工具 | 集成库 | 企业管理系统 |
| 隐私 | 链上 | 私人和链下交易 |
| 存储 | 链上公共状态和存储；链下存储 | 链上私有状态 |
| 执行 | EVM | 可信执行 |
| 共识 | 公共共识 | 私人共识 |
| 网络 | DevP2P | 企业 P2P |

企业以太坊客户端规范（EECS）的第一个版本（EECS），详细介绍了支持企业部署所需的权限控制、隐私和可扩展性对公共以太坊区块链的扩展，于 2018 年 5 月发布，你可以从 EEA 网站下载。这个规范的目标是作为一个灵活的标准，可以允许不同供应商的实现。例如，该规范定义了各种隐私级别，用 A、B 和 C 表示，这取决于节点之间的连接性、权限控制和交易隐私的需求。供应商可以决定针对哪个级别，并相应地获得认证。

##### 表 15.2\. EECS 的广泛要求

| 要求 | 描述 |
| --- | --- |
| 权限控制 | 一个区块链系统当其网络不公开，但节点由一个受限的、已知的参与者群体所拥有时，被称为权限控制的。 |
| 隐私 | 交易的內容只应 visible to the parties involved in the transaction. |
| 可扩展性 | 区块链基础设施的性能不应该随着交易数量的增加而下降，并且理想情况下应该与处理信用卡交易的大型企业系统相当。 |

#### 15.2.2\. Quorum

企业以太坊的第一个实现之一是 Quorum([www.jpmorgan.com/global/Quorum](http://www.jpmorgan.com/global/Quorum))。这是一个由台湾金融机构的合资企业 AMIS 和银行摩根大通在 2016 年创建的以太坊分叉。Quorum 通过一个星群网络扩展了共享的私有以太坊网络，该网络处理权限控制和数据隐私，正如你在图 15.4 中看到的。当两个或更多的参与者之间发生交易时，星群网络只在交易的成员之间部署相关的智能合约。交易的内容由交易管理器加密并存储在链下，其哈希存储在共享的以太坊区块链上。

##### 图 15.4\. 星群网络允许 Quorum 处理权限控制和隐私。只有涉及交易的各方才会部署智能合约；交易是加密的，存储在链下，其哈希存储在共享的以太坊区块链上。

![](img/fig15-04_alt.jpg)

Quorum 是第一个

+   利用 geth 的可插拔共识接口允许一个*可配置的共识算法*。

+   使用*zk-SNARKs*的加密隐私技术提供智能合约交易的零知识验证，这意味着验证交易的正确执行，而无需学习已计算出什么。项目参与者已经使用这项技术构建了*零知识安全层*（ZSL），它为 Quorum 提供了在区块链上转移数字资产的能力，而不会透露发件人和收件人资产本身的信息，从而保证完全的隐私。

|  |
| --- |

##### 注意

zk-SNARKs 是使 ZCash 成为一个真正匿名的加密货币的技术，与比特币不同，比特币的交易可以追溯到其所有者。

|  |
| --- |

### 15.3. 超越以太坊区块链

正如你所知，区块链技术非常适合解决与证明资产所有权和可追溯性相关的问题。但是，正如你之前所学的，像以太坊这样的公共区块链可能不适合解决这些问题的企业应用，因为它们没有关注企业需求，例如表 15.2 中列出的那些：权限管理、隐私和可扩展性。尽管 EEA 正在通过各种扩展尝试使以太坊区块链满足这些要求（Quorum 就是一个例子），但其他组织决定采取完全不同的方法。供应商同意分布式数据库将是任何解决方案的核心组件，但在架构的许多实现方面他们存在分歧：

+   *分布式数据库技术*——这并不一定基于区块链结构，因此行业提出了更一般的术语*分布式账本技术*（DLT）。

+   *权限管理*——供应商同意，只有通过限制在已知参与者的受限网络中，才能安全且可接受地扩展地访问分布式账本。

+   *共识*——区块链领域的共识机制已经从 PoW 演变而来，基于大量匿名矿工同时处理相同的交易，到 PoS，基于较小的一组参与者提交押金并以协调的方式处理不同集成的交易，再到 PoA，基于一组有限的已知参与者。这些方法之间的共同点是，它们都涉及到两个根本的网络角色：交易提交者（任何节点）和验证者（或矿工）。另一方面，分布式账本的共识可能涉及许多角色之间的更复杂交互，以提供更好的可扩展性，同时不损害存储数据的完整性。

+   *加密货币*——基于非区块链结构的分布式账本的共识算法不是基于 PoW 或 PoS，因此不需要加密货币，但某些平台仍然允许生成加密货币或代币，以在需要时促进货币价值的交换。

两个已经获得相当关注的分布式账本倡议是超账本和 Corda。我会简要介绍它们提供的内容，以便你可以更好地了解基于区块链的分布式账本的发展情况。

#### 15.3.1. 超账本

大约在 2015 年 12 月，Linux 基金会启动了一个名为超账本的项目，其战略目标是通过分布式账本的发展促进跨行业合作。在这个成功的项目中，已经有大约 250 个成员组织提供了资金和技术 expertise。其中的两个例子是 Hyperledger Burrow，它包括自己的以太坊虚拟机实现，以及 Hyperledger Iroha，它专注于移动应用。

超账本 Fabric（[www.hyperledger.org/projects/fabric](http://www.hyperledger.org/projects/fabric)），可能是超账本项目中最受欢迎的一个，其目标是构建企业区块链应用的框架。其代码库是在几个月前举行的一次黑客马拉松中由 IBM、Digital Asset 和 Blockstream 开发的一些代码的基础上建立起来的。超账本 Fabric 基于区块链技术，但它是一个开放的插件式框架，允许你更改和定制架构中的许多组件，并将平台适应于许多行业用例。例如，共识算法的设计是可插拔的，你可以用多种主流语言编写智能合约，如 Java、JavaScript 和 Go。如果你有时间，官方文档（[`hyperledger-fabric.readthedocs.io`](https://hyperledger-fabric.readthedocs.io)）提供了从高级架构到平台低级实现细节的全面信息。

以下是与以太坊等传统区块链系统相比，Hyperledger Fabric 的主要特点：

+   一个交易中可以有四个角色参与并共同达成共识：（见[5])

    > ⁵
    > 
    > 参见超账本 Fabric 文档中的“交易流程”[`mng.bz/Wadl`](http://mng.bz/Wadl)。

    +   提交客户端是一个提交交易的节点。

    +   背书者（或背书对等节点）是一个通过背书策略在交易提交到账本之前验证电子签名并背书的节点；背书者通常是所有必须批准交易的一方。

    +   排序者是一个在交易需要时运行消息服务的节点，提供排序和交付保证。

    +   提交者（或对等节点）是一个提交交易并持有账本副本的节点。

+   交易的详细信息仅对感兴趣的参与者私有。这是通过*通道*实现的，通道是提供隔离和保密通信的子网络—有点像 WhatsApp 群组。

另一个有趣的区块链框架是 Hyperledger 项目在其伞下开发的其他区块链框架 Hyperledger Sawtooth，([6])，它引入了以下创新特性：

> ⁶
> 
> 参见“Hyperledger 发布 Hyperledger Sawtooth 1.0，”2018 年 1 月 30 日，[`mng.bz/Ee2X`](http://mng.bz/Ee2X)。

+   *并行事务执行*—大多数区块链系统只能按顺序处理事务。

+   *链上治理*—参与者可以通过基于智能合约的投票积极配置自己的网络。

+   *对以太坊的支持*—与 Hyperledger Burrow 一样，Sawtooth 提供了一个符合 EVM 的智能合约运行环境，能够运行 Solidity 合约。

+   *动态共识*—这超出了 Fabric 的插件共识设计，因为你可以随时更改共识算法。

+   *更广泛的智能合约语言选择*—除了 Fabric 支持的语言之外，Sawtooth 还支持 Python。

Hyperledger 项目还协调了区块链工具的开发，如 Hyperledger Composer，专注于帮助用户创建智能合约，以及 Hyperledger Explorer，允许用户查看和分析区块和交易信息。

#### 15.3.2\. Corda

R3 是一个成立于 2015 年的公司联盟，现已增长到约 200 个成员，最初主要来自金融部门，但越来越多地来自其他行业。他们于 2016 年开始将 Corda 作为一个开源项目。

他们为创建 Corda 采取的方法与 EEA 和 Hyperledger 项目的做法不同。首先，技术堆栈由标准的现成组件组成，如 Java 虚拟机、关系数据库和消息队列。其次，Corda 通过在个体交易层面而不是在 Hyperledger 通道中交互的一组参与者之间共享数据来实现隐私。具体来说，两个或更多节点可以共享一个或多个事实，每个节点都维护其自己的本地事实副本。没有包含所有事实的中心数据库，如图 15.5 和官方文档中更详细地描述的那样。图 15.5 展示了 Corda 网络中事实是如何共享的。每个节点都维护其自己的事实副本，但它可以与其他节点共享一些事实。例如，事实 1 和 5 在节点 A 和 B 之间共享；事实 4 只有节点 C、D 和 E 可见，而 A 和 B 不可见。

> ⁷
> 
> 参见 Corda 文档中的“账本”[`docs.corda.net/key-concepts-ledger.html`](https://docs.corda.net/key-concepts-ledger.html)。

##### 图 15.5\. Corda 网络中事实的共享方式。每个节点都维护其自己的事实副本，但它可以与其他节点共享一些事实。例如，事实 1 和 5 在节点 A 和 B 之间共享；事实 4 只有节点 C、D 和 E 可见，而 A 和 B 不可见。

![](img/fig15-05_alt.jpg)

正如你所看到的，这是一个不断发展的领域，有许多不同的解决问题的方法。紧握不放，期待更多的创新！

### 摘要

+   EVM 正在升级到一个更通用的版本，支持 eWASM，最终能够执行从 Rust 和 C 编译的代码。

+   Solidity 语法的持续改进导致了诸如`send()`和`call()`被废弃，转而使用`transfer()`等变化。

+   处于撰写时正处于测试阶段的 Web3.js 1.0 版本即将成为以太坊生态系统的官方版本。我强烈建议您一旦它发布就立即参考。

+   一些以太坊网络采用了不同于工作量证明的共识算法：Kovan 和 Rinkeby 支持权威证明，而 Casper 项目正在引入股份证明。

+   一个企业以太坊平台，如 Quorum，支持企业 Dapp 需求，如可扩展性、权限管理和隐私。

+   其他分布式账本平台，如 Hyperledger 或 Corda，提供了企业以太坊的替代方案。
