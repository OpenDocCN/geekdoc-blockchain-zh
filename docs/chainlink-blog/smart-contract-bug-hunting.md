# 查找智能合约漏洞的 7 大策略

> 原文：<https://blog.chain.link/smart-contract-bug-hunting/>

*特别感谢* [*艾德里安·赫特曼*](https://twitter.com/adrianhetman)[*阿莱航德罗·穆尼奥斯-麦克唐纳*](https://twitter.com/unsafe_call)[*伊万·贝纳维德斯*](https://twitter.com/Ivanbenavides_) *，以及*[](https://twitter.com/leonspacewalker)

[https://www.youtube.com/embed/sgHHbWvWj9A?feature=oembed](https://www.youtube.com/embed/sgHHbWvWj9A?feature=oembed)

## 智能合同漏洞追踪的 7 大策略

搜寻智能合同漏洞可能是一份报酬高得离谱的工作，也是保护生态系统免受黑客攻击的一个组成部分。最近，我有幸在 [采访了一位开发人员](https://twitter.com/leonspacewalker) ，他发现了一个价值 70 亿美元的漏洞，而 [因为报告了这个漏洞而获得了 220 万美元的报酬。](https://medium.com/immunefi/polygon-lack-of-balance-check-bugfix-postmortem-2-2m-bounty-64ec66c24c7d)

在这篇博客中，我们将讨论这个开发者发现的漏洞，以及它如何有可能损害 70 亿美元的价值，然后提供一些策略和工具来帮助你发现漏洞。

让我们开始吧。

## 多边形智能合约 Bug 示例

### 集结

2020 年 5 月 31 日， [Matic 区块链上线](https://crypto.news/matic-network-mainnet-live/) (Matic 后来更名为 [多边形](https://polygon.technology/) )。Polygon 是一个与 EVM 兼容的区块链，以其低汽油费和短阻塞时间而闻名。链家最近开始探索 [zk-rollup 技术](https://www.alchemy.com/overviews/polygon-zk-rollups) 。

如果你看一看多边形的 [区块 0](https://polygonscan.com/block/0) ，区块链的绝对第一区块，也被称为它的“创世纪”区块，你会看到 10 笔交易。其中一个交易创建了一个名为 MRC20 的合同。

![Screenshot of Polygon genesis block.](img/50a5260d5f16ecc248beff3c46b643de.png)

<figcaption id="caption-attachment-4804" class="wp-caption-text">Polygon genesis block.</figcaption>



这是什么合同？

当我们发送区块链本地令牌时，我们不得不花费汽油。因此，Polygon 团队部署了一份合同，允许您签署一项交易，向某人发送 ETH，而其他人能够支付这笔交易的汽油费。这种功能被称为“元事务”，随着[【EIP】-712](https://eips.ethereum.org/EIPS/eip-712)的引入而普及。

你可以看到，这份合同被赋予了近 100 亿 MATIC tokens，以帮助促进这些无汽油交易。然而，这个巧妙的契约包含一个漏洞，该漏洞可能被利用来耗尽整个余额！

2021 年 12 月 3 日故事的主人公，伪匿名开发者 [莱昂](https://twitter.com/leonspacewalker) ，向[Immunefi bug bounty](https://immunefi.com/bounty/immunefi/)程序提交了一份报告，规划出了这个确切功能的细节。第二个英雄，我们姑且称之为怀特哈特 2，也在一天后报告了这个漏洞。

2021 年 12 月 5 日，大约 800，000 枚 MATIC 代币在链条最终分叉、回滚并固定 [之前被盗。](https://github.com/maticnetwork/bor/releases/tag/v0.2.12)

这给我们留下了更多的问题:漏洞是什么？它怎么会这么久没被发现？是怎么找到的？

## 漏洞利用

下面是促进这些无汽油交易的功能。

```
   function transferWithSig(
       bytes calldata sig,
       uint256 amount,
       bytes32 data,
       uint256 expiration,
       address to
   ) external returns (address from) {
       require(amount > 0);
       require(
           expiration == 0 || block.number <= expiration,
           "Signature is expired"
       );

       bytes32 dataHash = getTokenTransferOrderHash(
           msg.sender,
           amount,
           data,
           expiration
       );
       require(disabledHashes[dataHash] == false, "Sig deactivated");
       disabledHashes[dataHash] = true;

       from = ecrecovery(dataHash, sig);

       _transferFrom(from, address(uint160(to)), amount);
   }
```

乍看之下，这似乎是无害的:它获取用户的签名、多少代币以及他们想要发送给谁，以及任何进一步的数据，还有交易的截止日期。

它运行一些要求，获取数据散列以发送元事务，确保数据散列未被使用，并执行此 `ecrecovery` 功能。

这个函数本质上是 [实度恢复函数](https://docs.soliditylang.org/en/latest/cheatsheet.html?highlight=ecrecover#global-variables) 的包装器。

![Screenshot of Solidity ecrecover function wrapper.](img/85191a3579e55ff09c8f3d40a42a82bd.png)

<figcaption id="caption-attachment-4805" class="wp-caption-text">Solidity ecrecover function wrapper.</figcaption>



这个函数就是我们如何验证已签名的交易来自哪里。你会注意到，即使在 Solidity 文档中，它也说它将“出错时返回零”。`ecrecovery`函数复制了这个，如果它有问题，它将返回 0。正如许多开发人员所知，这可能很可怕。如果出错时返回零，这意味着我们应该检查以确保返回的地址不是零，对吗？

下面是实际的代码:

![ecrecovery screenshot](img/62e38e6daa81542e13e0bd1c4b6f2292.png)

这里是应该有的:

![ecrecovery screenshot](img/efb31dc2e269cb49b49ce9fb3bee0a24.png)

所以我们不会对地址进行检查以确保它不会导致错误。没问题。我们的`transferWithSig`函数中的最后一行代码执行实际的传输，我们肯定会在那里执行某种检查，对吗？

```
function _transfer(address sender, address recipient, uint256 amount)
   internal
{
   require(recipient != address(this), "can't send to MRC20");
   address(uint160(recipient)).transfer(amount); // It just sends the money!
   emit Transfer(sender, recipient, amount);
}
```

`_transferFrom`函数刚刚调用了我们的`_transfer`函数，如上图。你会注意到它并没有检查`from`地址是否有足够的钱。

这意味着有人可以发送无效签名，这将导致从 ecrecovery 返回零地址，但是 MRC20 契约仍然会向`to`地址发送一定数量的钱。这就是 9，999，993，000 MATIC 被消耗的方式，因为 MRC20 合同直接从它自己发送钱！

进行检查以确保`from`地址有足够的资金用于这笔已签名的交易可以防止这一问题。

## 智能合同漏洞是如何躲避发现如此之久的？

让我感到奇怪的是，这个漏洞在潜伏了将近一年半之后，在几天之内被另一个白帽黑客 Leon 发现了。

似乎有猫腻。但是 Immunefi 团队告诉我这种情况经常发生。一些漏洞可以基于一篇文章、报道或 [挑战](https://github.com/code-423n4/2021-09-swivel-findings/issues/61) 而变得流行，然后人们开始寻找该漏洞，导致几个人同时找到它。

但更有可能的是，事实证明，polygon 在 Polygonscan 上验证了这一契约——所以那是当人们 *真的* 开始关注它的时候。

也许故事还有更多，但也许没有。

无论如何，让我们把这个 bug 作为一个可教的时刻，看看 Leon 和其他 bug 猎人用来寻找 bug 的一些技巧，帮助保护 Web3 生态系统。

## 七大战略

现在，我们将学习 Leon 和其他 bug 猎人用来找到这些漏洞并获得 bug 奖金的技巧。这份提示清单假设你已经了解了智能合约的基础知识，那么是的， [学习扎实是前提](https://www.youtube.com/watch?v=gyMwXuJrbJQ&t=23615s) 。

使用这些超能力进行 [道德黑客](https://www.eccouncil.org/ethical-hacking/) ，并且请记住 [负责任地披露](https://www.hackerone.com/vulnerability-management/what-responsible-disclosure-policy-and-why-you-need-one) 你发现的任何漏洞。

很多寻找漏洞的工作来自于查看代码和运行像 [slither](https://github.com/crytic/slither) 这样的工具。对于这笔 220 万美元的支出，Leon 说他能够通过逐行查看智能合同代码来找到漏洞，所以请记住，找到漏洞通常是一项巨大的人工任务！

除了下面的实用技巧，Leon 最大的收获是让聪明的合同 bug 猎人“找到你的优势”，但他这么说是什么意思呢？通常，这意味着找到让你与其他黑客不同的东西。作为一个社区，我们需要覆盖智能合同领域的每个角落，所以找到一个你特别擅长和擅长的部分。

这里有七个策略和技巧可以帮助你找到优势，让你成为一个成功的智能合同 bug 猎人。

### 1。找到一个项目并搜索 bug

找到漏洞的第一个方法是了解协议的每一个细节。这是每个聪明的契约式 bug 猎人需要学习的首要技能之一:端到端理解协议的能力。

浏览文档，尝试自己重新实现一个协议，并在 block explorer 上通过该协议查看事务。

莱昂说这个策略对其他猎人有效，但对他无效。他将重点放在接下来的三个方面，但是对于每个 bug 猎人来说，能够做到这一点是很重要的。

### 2。找到一个 Bug 并搜索项目

寻找 bug 的一个更简单的方法是找到一个没有多少人知道的 bug，并尝试查看哪些协议实现了它。

这个策略需要大量的研究，因为有很多人在研究向公众暴露 bug 的[](https://swcregistry.io/)。

你首先需要了解所有基本的智能合约漏洞，然后是它们的高级版本。您需要了解最佳实践，并查看是否有没有遵循它们的协议。

一旦你发现一个你认为很多项目可能都没有防范的智能合约漏洞，就开始搜索那个漏洞。真正熟悉这个新的 bug 以及如何找到它。一定要写博客或某种帖子来帮助其他遇到这种错误的智能合约开发人员保护自己。

### 3。要快

想让 bug 猎人看自己智能合约的项目，需要注册类似 [Immunefi](https://immunefi.com/) 这样的 bug 赏金计划。你会想成为第一批发现新奖金的开发者之一。如果你在其他猎人之前开始看合同，你会比其他猎人有更多的时间来发现漏洞。

有几种快速的方法 Leon 能够在其他人之前发现智能合约漏洞的方法之一是打开 [的通知，Immunifi 更新 Discord channel](https://discord.gg/nVE8WqH3MH) 。每当有新项目进来或项目更新时，他都会收到通知。像这样的工具可以帮助你在别人之前深入研究代码。

### 4。有创意

Leon 另一个能够获得优势的方法是浏览 [社区论坛](https://forum.makerdao.com/) ，发现他们正在考虑提交一个 bug。甚至在奖金被批准之前，他就开始查看智能合同。这给了他比其他开发人员更多的时间来看合同，因为他们会等待 bug 奖金的提交。

### 5。了解你的工具

Bug 猎人使用的工具有 vs code Solidity visual developer extension、Hardhat、Foundry、Brownie、Dune、Etherscan 以及其他一些工具。

典型的 bug 搜索策略可能是加载 VSCode，使用 Solidity 可视化扩展将代码添加到 VSCode 中，并逐行查找常见的 bug 或糟糕的最佳实践。

在发现一个弱点之后，建立一个测试环境来对合同进行测试是一个很好的下一步。您通常可以重用协议开发人员最初使用的许多测试。

### 6。不要害怕被审计的项目

这里没什么可说的了。审计公司会犯错。Leon 发现漏洞的许多项目都被顶级公司审计过。

使用我们在这篇博客中谈到的技巧可以让你发现这些问题！

### 7。特定行业知识

找到自己优势的最大优势之一就是专攻某个特定的领域。如果您非常了解某个领域，那么您将拥有了解所有功能如何相互作用的优势。如果你是一个非凡的智能合同漏洞专家，但对 DeFi 一无所知，那么很难在 DeFi 合同中找到漏洞。例如，很多开发人员理解代码，但不理解财务原语。

你可能会非常擅长理解分散式交换、借用协议，或者仅仅是 NFT！

如果你能成为 Web3 中的安全大师和某个垂直领域的大师，你就能在其他寻找漏洞的人面前占得先机。

## 总结

我希望这篇文章对你的智能合同 bug 搜索之旅有用。如果您想在编写智能合同时了解更多关于安全性的信息，请务必查看 [十大 DeFi 安全性最佳实践](https://blog.chain.link/defi-security-best-practices/) 。

一如既往，我希望看到你们在那里建设和维护一个更安全的生态系统。

### 链接

[MRC20 契约。T3】](https://polygonscan.com/address/0x0000000000000000000000000000000000001010#code)

[Immunefi 书面报告。T3T5】](https://medium.com/immunefi/polygon-lack-of-balance-check-bugfix-postmortem-2-2m-bounty-64ec66c24c7d)

[改变为多边形契约](https://github.com/maticnetwork/contracts/commit/55e8118ad406c9cb0e9b457ca4f275c5977809e4#diff-cc4ed03464edad9d87d48cff647eb6940dfe9a4c419f63e3994bdc91b01bfecb) 。

[先前的多边形契约。T3】](https://github.com/maticnetwork/contracts/blob/56ec7eb257ce10a9f70621f56f6e3f37eb8e0c57/contracts/child/MRC20.sol)

[Ecrecovery 挑战。T3】](https://github.com/code-423n4/2021-09-swivel-findings/issues/61)

*本文中表达的观点仅是作者个人的观点，并不代表链家基金会或链家实验室的观点和信念。T3】*