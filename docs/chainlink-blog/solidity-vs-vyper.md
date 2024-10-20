# Solidity vs. Vyper:哪种智能合同语言适合我？

> 原文：<https://blog.chain.link/solidity-vs-vyper/>

*本文根据 2022 年 9 月的资料撰写。特别感谢*[*0x kitsune*](https://twitter.com/0xKitsune)[*Hari*](https://twitter.com/_hrkrshnn)[*Doggie B*](https://twitter.com/fubuloubu)[*Alex beregszi*](https://twitter.com/alexberegszaszi)

本文探讨了以下问题——Solidity 和 Vyper 哪个智能合同语言更适合我？最近，有很多关于哪种是“最好的”智能合同语言的争论，双方都支持自己选择的语言。

我在这里回答这场辩论最底层的主要问题:

## 我应该使用哪种智能合同语言？

为了弄清这个问题，在考虑任何智能合同开发者的主要问题之一:gas 优化之前，我们将讨论工具和可用性。具体来说，我们要看四种[【EVM】](https://ethereum.org/en/developers/docs/evm/)语言(工作在类似 [以太坊](https://ethereum.org/en/) 、 [雪崩](https://docs.avax.network/) 、 [多边形](https://polygon.technology/) 等链条上的语言)。):[](https://docs.soliditylang.org/en/v0.8.16/)[Vyper](https://vyper.readthedocs.io/en/stable/index.html)[Huff](https://docs.huff.sh/)，以及[Yul](https://docs.soliditylang.org/en/latest/yul.html)。抱歉 [生锈](https://docs.solana.com/developing/on-chain-programs/developing-rust) ，你得等着看一篇报道非 EVM 链条的文章。

但是首先，剧透一下。

Solidity、Vyper、Huff 和 Yul 都是出色的语言，可以完成工作。Solidity 和 Vyper 是大多数人应该使用的奇妙的高级语言。如果您对编写近似汇编代码感兴趣，Yul 和 Huff 可以胜任这项工作。T3】

猜猜看，如果你坚持要选择一种语言， [抛硬币](https://justflipacoin.com/) :无论你选择哪种语言，我保证你都会成功。如果你是智能契约编程语言的新手，你可以用你最喜欢的语言，或者你随机选择的语言做很多事情。

此外，这些语言一直在变化，你可以很容易地挑选智能合约和数据，让不同的语言看起来更好或更差。当我们进行气体优化比较时，请记住这一点。我们选择了一个最小的合同进行比较，如果你认为你有一个更好的例子，我们很乐意看到它！

现在，如果你是这个领域的老手，让我们深入了解这些语言。准备出去玩吧。

[https://www.youtube.com/embed/sbc74oU94FM?feature=oembed](https://www.youtube.com/embed/sbc74oU94FM?feature=oembed)

## EVM 编程语言

我们将要学习的四种语言如下:

*   [](https://docs.soliditylang.org/en/v0.8.16/):目前最流行的语言由 [DeFi TVL](https://impermax.medium.com/defi-explained-what-is-tvl-9800eda80b0b) 。高级，类似于 JavaScript。
*   [【Vyper】](https://vyper.readthedocs.io/en/stable/index.html):目前第二大流行语言由德菲 TVL。高级，类似 Python。
*   [哈夫](https://huff.sh/) :类似汇编的低级语言。
*   [Yul](https://docs.soliditylang.org/en/latest/yul.html) :一种类似汇编的低级语言，内置了 Solidity(虽然有人认为是 [还是太高级别了](https://github.com/ethereum/solidity/issues/13247) )。

### 为什么是这四个？

我们使用这四种语言，因为它们都兼容 EVM，Solidity 和 Vyper 是目前最受欢迎的两种语言。我添加了 Yul，因为在不考虑 Yul 的情况下将气体优化与坚固性进行比较是不公平的。我们添加了 Huff，因为我们想对一种语言进行基准测试，这种语言几乎与用操作码编写的语言相同，但不是 Yul。

就 EVM 而言，在 Vyper 和 Solidity 之后，第三、第四和第五的受欢迎程度大幅下降。抱歉没有进行这种比较的语言；领养的事不存在。然而，有许多有前途的智能合同语言正在兴起，我期待着在未来尝试它们。

## **什么是扎实？**

Solidity 是一种面向对象的编程语言，用于在以太坊和其他区块链上实现智能合约。Solidity 深受 C++、Python 和 JavaScript 的影响，是为 EVM 设计的。

## **什么是 Vyper？**

Vyper 是一种面向契约的 pythonic 编程语言，也是为 EVM 设计的。Vyper 旨在通过增强可读性和限制某些做法来提高可靠性。从高层次来看，Vyper 寻求优化智能合同的安全性和可审计性。

## 当前的景观

![A cumulative chart showing programming language by TVL](img/2e02cac89d42000253428bb49123ad87.png)

<figcaption id="caption-attachment-4754" class="wp-caption-text">Adapted from [DefiLlama’s languages tab](https://defillama.com/languages).</figcaption>



据[DefiLlama](https://defillama.com/languages)报道，截至目前，在 DeFi 领域，Solidity 智能合约安全了 TVL 87%的份额，而 Vyper 智能合约安全了 8%。

因此，如果你在寻找纯粹的受欢迎程度，你不需要看得比可靠更远。

## 比较相同的合同

现在让我们来看看每种语言的样子，然后比较它们的气体性能。

这里有四份用各种语言写成的几乎完全相同的合同。他们都做大致相同的事情，他们都:

1.  在存储槽 0 有一个专用号码(uint256)。
2.  使用 readNumber() [函数签名](https://ethereum.stackexchange.com/q/135205/57451) 读取存储槽 0 中的内容。
3.  允许您用 storeNumber(uint256)函数签名更新该数字。

就这样。这些是合同。

*我们用来比较语言的所有代码都位于* [*本 GitHub repo*](https://github.com/PatrickAlphaC/sc-language-comparison)*。T13】*

### 🐉固态

![Example of a Solidity Contract](img/380129ed2072d732ecf2baf7e637bf2c.png)

### (鲁瓦)

![An Example of a Vyper Contract](img/d6664ac10f94d984e9a87527a83937db.png)

### ♞·赫夫

![An Example of a Huff Contract](img/0685662b96bcfcd33cd4971e999aaadf.png)

### 🧮·尤尔

![An Example of a Yul Contract](img/d698f40cec344a378fd996758d42be6e.png)

### 开发者体验

仅仅通过看这四张图片，我们就可以开始了解每种语言的书写感觉。就开发人员的经验而言， **编写可靠和高效的代码要快得多。** 这很有道理:那些语言是更高级的，而 Yul 和 Huff 本来就是低级代码。仅仅因为这个原因，很容易理解为什么这么多人采用 Vyper 和 Solidity(以及它们各自存在的时间更长的事实)。

关注 Vyper 和 Solidity 一秒钟，你可以清楚地看到，Vyper 从 Python 中汲取灵感，Solidity 从 JavaScript 和 Java 中汲取灵感。所以如果你喜欢其中一种语言的感觉，很好——使用它。

Vyper 的本意是成为一种 [极简、易于审计的编程语言](https://vyper.readthedocs.io/en/stable/index.html#principles-and-goals) ，而 Solidity 的本意是成为一种通用的智能合约语言。从语法层面上来说，编码的体验确实也是如此，但是我会让你在这个主观问题上做出自己的决定。

我不打算过多地讨论工具，因为大多数语言都有非常相似的工具。大多数主框架，包括 [安全帽](https://hardhat.org/) 、ape、titanoboa、 [布朗尼](https://github.com/eth-brownie/brownie) ，以及 [铸造厂](https://github.com/foundry-rs/foundry) ，都有 Vyper 和 Solidity 支持。Solidity 对这些框架中的大多数都有“优先公民权”，而 Vyper 需要 [使用一个插件](https://www.npmjs.com/package/@nomiclabs/hardhat-vyper) 来与像 Hardhat 这样的工具一起工作。然而，titanoboa 是专门为与 Vyper 一起工作而构建的，大多数工具都很容易与这两者一起使用。

## 哪种智能合约语言更 Gas 优化？

现在是主要事件。在比较智能合约的天然气性能时，有两个主要事项需要记住:

1.  合同生成天然气成本
2.  运行时气体成本

如何实施智能合同会对这些因素产生重大影响。例如，您可以在契约的代码中存储一个大规模数组，这样部署起来很昂贵，但运行一个函数却比较便宜。或者，您可以让您的函数动态地生成数组，使契约的部署成本更低，但运行成本更高。

那么，让我们来看看这四份合同，比较它们的合同生成天然气成本和运行时天然气成本。你可以在我的[sc-language-comparison repo 中找到我所有的代码，包括用来比较它们的框架和工具。](https://github.com/PatrickAlphaC/sc-language-comparison)

### 天然气成本比较汇总

以下是我们如何编制该部分的合同:

```
vyper src/vyper/VSimpleStorage.vy

huffc src/huff/HSimpleStorage.huff -b
solc --strict-assembly --optimize --optimize-runs 20000 
yul/YYSimpleStorage.yul --bin

solc --optimize --optimize-runs 20000 src/yulsol/YSimpleStorage.sol --bin

solc --optimize --optimize-runs 20000 src/solidity/SSimpleStorage.sol --bin 
```

*注意:我也可以使用–via-IR 标志进行可靠性编译。还要注意的是，Vyper 和 Solidity 在他们的合同末尾添加了“元数据”。这占了天然气总成本的一小部分，但不足以改变下面的排名。我将在元数据部分详细讨论这一点。T3】*

结果:

![A bar graph comparing gas costs by programming language.](img/ef3431acc1e39b240c14a1c41af272ca.png)

<figcaption id="caption-attachment-4759" class="wp-caption-text">Contract creation gas costs across languages.</figcaption>



正如我们所见，像 Huff 和 Yul 这样的低级语言比 Vyper 和 Solidity 更高效，但这是为什么呢？Vyper 似乎比 Solidity 更有效，我们有了这个新的“Sol 和 Yul”部分。嗯，那是因为你其实可以在 里面写 Yul *实度。Yul 是 Solidity 开发人员在需要接近机器代码时编写的语言。*

在上图中，我们比较了生 Yul、生 Solidity 和 Solidity-Yul 混合物。我们代码的 Solidity-Yul 版本如下所示:

![A code snippet of Yul and Solidity combined.](img/c2c142df78b3d29dee0679820377e59f.png)

<figcaption id="caption-attachment-4760" class="wp-caption-text">Yul and Solidity combined.</figcaption>



稍后你会看到一个例子，这种内嵌的 Yul 使**的天然气成本产生重大差异。我们稍后再来看看为什么会存在这些气体差异，但现在让我们看看 [铸造](https://github.com/foundry-rs/foundry) 中与单次测试相关的气体成本。**

 **![Gas cost testing function for Solidity-Yul contract](img/30e412009c2e34b037f4c9785669aa57.png)

<figcaption id="caption-attachment-4761" class="wp-caption-text">Our testing function.</figcaption>



这将测试存储 中的气体成本数字 77，然后从存储器中读取 中的数字。下面是运行这个测试的结果。

![Bar graph showing the different in gas costs for reading and writing by language.](img/1efd97e65bfc5e012e1407f4c0ebda01.png)

<figcaption id="caption-attachment-4762" class="wp-caption-text">SimpleStorage read and write gas comparisons.</figcaption>



我们没有 Yul 的数据，因为我们必须做一个 Yul-Foundry 插件，这是我不想做的——我敢打赌结果会和 Huff 差不多。请记住，这是运行整个测试功能的气体成本，而不仅仅是单个功能。

## 天然气成本比较

好了，我们来分析一下这个数据。我们需要回答的第一个问题是:为什么 Huff 和 Yul 的合同创建比 Vyper 和 Solidity 的效率高得多？嗯，我们可以通过直接查看这些合同的字节码来找到答案。

当你起草一份合同时，它通常被分成两三个不同的部分。

1.  合同创建代码
2.  运行时代码
3.  元数据(可选)

对于本节，理解操作码的基础很重要。OpenZeppelin 关于 [的博客解构一个契约](https://blog.openzeppelin.com/deconstructing-a-solidity-contract-part-i-introduction-832efd2d7737/) 是一个很棒的起点。

## 合同创建代码

契约创建代码是字节码的第一部分，它告诉 EVM 将契约粘在链上。您通常可以通过在生成的二进制文件中查找 CODECOPY 操作码(39)来找到它，然后找到它在链上的位置，并返回 RETURN 操作码(f3)并结束调用。

```
Huff:
602f8060093d393df3 
Yul:
603e80600c6000396000f3fe 
Vyper:
61006b61000f60003961006b6000f3 
Solidity:
6080604052348015600f57600080fd5b5060ac8061001e6000396000f3fe 
Solidity-Yul:
608060405234801561001057600080fd5b5060bc8061001f6000396000f3fe
```

你还会注意到很多 fe 操作码，也就是 无效的 操作码。Solidity 添加了这些标记，以显示运行时、契约创建和元数据代码之间的区别。“f3”是“RETURN”操作码，通常是函数或上下文的结尾。

你可能认为因为 Yul-Solidity 有最大的合同创建字节码，而 Huff 有最小的，这就是 Huff 最便宜而 Yul-Solidity 最贵的原因。但是当你复制整个代码库并把它粘在链上时，代码库的大小就有很大的不同，并且是主要的决定因素。然而，这个契约创建代码确实让我们看到了这些编译器是如何思考的，并且让我们很好地了解了它们将如何编译我们的契约。

### 如何读取操作码和堆栈

现在，EVM 是一个基于堆栈的机器[](https://www.evm.codes/about)，意思是你做的大部分“事情”都是把东西从一个 [堆栈](https://www.geeksforgeeks.org/stack-data-structure/) 中推出来。你会看到左边有 [操作码](https://www.evm.codes/) ，右边有两条斜线(//)表示它们是注释，以及在同一行执行操作码后堆栈的样子，堆栈的顶部在左边，底部在右边。

### 哈夫解释道

Huff 契约创建只做它能做的最少的事情。它抓取你写的代码，并返回它。

```
PUSH 0x2f // [2f]
DUP1 // [2f, 2f]
PUSH 0x09 // [09, 2f, 2f]
RETURNDATASIZE // [0, 09, 2f, 2f]
CODECOPY // [2f]
RETURNDATASIZE // [0, 2f]
RETURN  // []
```

### 尤尔解释道

Yul 做了同样的事情，它使用了一些不同的操作码，但本质上，它只是用尽可能少的操作码和一个无效的操作码将你的代码放到链上。

```
PUSH 0x3e // [3e]
DUP1 // [3e, 3e]
PUSH 0x0c // [0c, 3e, 3e]
PUSH 0x0 // [0, 0c, 3e, 3e]
CODECOPY // [3e]
PUSH 0x0 // [0, e3]
RETURN  // []
INVALID // []
```

### Vyper 解释道

Vyper 也差不多。

```
PUSH2 0x06B // [06B]
PUSH2 0x0F // [0F, 06B]
PUSH1 0x0 // [0, 0F, 06B]
CODECOPY // []
PUSH2 0x06B // [06B]
PUSH1 0x0 // [0, 06B]
RETURN // []
```

### 解释了坚固性

现在让我们来看看坚固性操作码。

```
// Free Memory Pointer
PUSH1 0x80 // [80]
PUSH1 0x40 // [40]
MSTORE // []

// Check msg.value
CALLVALUE // [msg.value]
DUP1 // [msg.value, msg.value]
ISZERO // [msg.value == 0, msg.value]
PUSH1 0xF // [F, msg.value == 0, msg.value]
JUMPI // [msg.value] Jump to JUMPDEST if value is not sent

// We only reach this part if msg.value has value
PUSH1 0x0 // [0, msg.value]
DUP1 // [0, 0, msg.value]
REVERT // [msg.value]

// Finally, put our code on-chain
JUMPDEST // [msg.value]
POP // []
PUSH1 0xAC // [AC]
DUP1 // [AC, AC]
PUSH2 0x1E // [1E, AC, AC]
PUSH1 0x0 // [0, 1E, AC, AC]
CODECOPY // [AC]
PUSH1 0x0 // [0, AC]
RETURN // []
INVALID // []
```

稳健能做更多的事情。Solidity 做的第一件事是创建所谓的 [空闲内存指针](https://docs.soliditylang.org/en/v0.8.16/assembly.html?highlight=free%20memory%20pointer#memory-management) 。为了在内存中创建动态数组，您需要跟踪内存中哪些部分是空闲的。在我们的契约构造代码中，我们不使用这个空闲内存指针，但是它总是首先使用。这是我们发现的语言之间的第一个主要差异:内存管理。每种语言处理记忆的方式不同。

接下来，Solidity 编译器查看你的代码，注意到你没有指定一个可支付的构造函数。因此，为了确保您不会搬起石头砸自己的脚，不小心在创建合同时发送了 ETH，它使用 CALLVALUE 操作码并开始检查，以确保您没有在创建合同时发送任何令牌。这给我们带来了语言之间的第二个主要区别:它们各自对共同的问题有不同的检查和保护 。

最后，Solidity 做了其他语言所做的事情:它将你的契约固定在链上。

我们将跳过 Solidity-Yul，它的工作方式与 Solidity 本身相似。

### 检查和保护

从这个意义上看，Solidity 似乎更“安全”,因为它比其他语言有更多的保护。然而，如果您要在 Vyper 代码中添加一个构造函数，然后重新编译，您会注意到一些不同。

![A Vyper language constructor](img/00eba0a100e37f41bb73a041e0270e9c.png)

<figcaption id="caption-attachment-4763" class="wp-caption-text">Vyper Constructor</figcaption>



编译这个，你的合同创建代码开始看起来更像 Solidity 的了。

```
// First, we check the callvalue, and jump to a JUMPDEST much later in the opcodes
CALLVALUE
PUSH2 0x080
JUMPI
// This part is identical to the original compilation
PUSH2 0x06B
PUSH2 0x014
PUSH1 0x0
CODECOPY
PUSH2 0x06B
PUSH1 0x0
RETURN
```

它仍然没有 Solidity 拥有的内存管理，但是你会看到它用一个构造函数来检查 callvalue。如果你让构造函数可支付并重新编译，那么检查将再次消失。

因此，我们可以通过查看这些合同创建设置得出两个结论:

1.  在 Huff and Yul 中，你需要清楚地说明支票的内容，并亲自书写。
2.  Solidity 和 Vyper 会帮你做检查，Solidity 可能会做更多现成的事情。

这将是不同语言之间最大的权衡之一: W 他们在幕后进行了哪些检查？用 Huff 和 Yul 写会更有效，因为这两种语言并不意味着在幕后做任何事情。因此，当然你的代码会更加高效，但是你很难跟踪所有正在发生的事情。

## 运行时代码

现在我们已经对幕后发生的事情有了一些了解，我们可以看看合同的不同功能是如何执行的，以及它们为什么以这样的方式执行。

让我们来看看如何调用 storeNumber()函数，每种语言的值为 77。我通过使用类似 Forge test-debug“testStorageAndReadSol”的命令遍历 [Forge debug 特性](https://book.getfoundry.sh/forge/debugger) 来获取操作码。我还用了 [Huff VSCode 扩展](https://github.com/huff-language/vscode-huff) 。

### 哈夫解释道

```
// First, we get the function selector of the call and jump to the code for our storeNumber function
PUSH 0x0         // [0] 
CALLDATALOAD // [b6339418] The function selector for storing 
PUSH 0xe         // [e, b6339418]                                                                                   
SHR              // [b6339418]                                                                                                                                               
DUP1 // [b6339418, b6339418]                                                                                                                                              
PUSH 0xb6339418  // [b6339418, b6339418, b6339418]                                                                                      
EQ // [true, b6339418]                                                                                                                                              
PUSH 0x1c        // [1c, true, b6339418]                                                                                  
JUMPI            // [b6339418]  
// We skip a bunch of opcodes since we jumped
// We place the 77 in storage, and end the call
JUMPDEST // [b6339418]                                                                                                                                           
PUSH 0x4         // [4, b6339418]                                                                                
CALLDATALOAD // [4d, b6339418] We load 77 from the calldata 
PUSH 0x0         // [0, 4d, b6339418]                                                                                                                                          
SSTORE // [b6339418] Place the 77 in storage 
STOP // [b6339418] End call
```

有趣的是，如果我们没有 STOP 操作码，我们的 Huff 代码实际上会添加一组操作码来返回我们刚刚存储的值，这比我们的 Vyper 代码更昂贵。但是这段代码看起来仍然非常简单，所以让我们看看 Vyper 是如何做到的。我们现在跳过 Yul，因为结果会非常相似。

### Vyper 解释道

```
// First, we do a check on the calldata size to make sure we have at least 4 bytes for a function selector
PUSH 0x3 // [3]
CALLDATASIZE // [3, 24]
GT // [true]
PUSH 0x000c // [000c, true]
JUMPI // []
// Then, we jump to our location, and get the function selector
JUMPDEST
PUSH 0x0 // [0]
CALLDATALOAD // [b6339418]
PUSH 0xe // [e, b6339418]
SHR // [b6339418]
// And we do a check for sending value
CALLVALUE // [0, b6339418]
PUSH 0x0059 // [59, 0, b6339418]
JUMPI // [b6339418]
// Value looks good, so we compare selectors, and jump if the selector is something else
PUSH 0xb6339418 // [b6339418, b6339418]
DUP2 // [b6339418, b6339418, b6339418]
XOR // [0, b6339418]
PUSH 0x0032 // [32, 0, b6339418]
JUMPI // [b6339418]
// We do a check to make sure the calldata size is big enough for a function selector and a uint256
PUSH 0x24 // [24, b6339418]
CALLDATASIZE // [24, 24, b6339418]
XOR // [0, b6339418]
PUSH 0x0059 // [59, 0, b6339418]
JUMPI // [b6339418]
// Then, we store the variable and end the call
PUSH 0x04 // [4, b6339418]
CALLDATALOAD // [4d, b6339418]
PUSH 0x0 // [0, 4d, b6339418]
SSTORE // [b6339418]
STOP
```

我们可以看到，我们在存储值时做了一些检查:

1.  函数选择器的调用数据有足够的字节吗？
2.  他们的价值是否随电话一起发送？
3.  call data 大小是函数选择器+ uint256 大小吗？

所有这些检查给我们的计算增加了负担，但它们也意味着我们有更大的机会不搬起石头砸自己的脚。

### 解释了坚固性

```
// Free Memory Pointer
PUSH 0x80 // [80]
PUSH 0x40 // [40,80]
MSTORE // []
// msg.value check, jump to function, revert otherwise
CALLVALUE // [0]
DUP1 // [0,0]
ISZERO // [true, 0]
PUSH 0x0f // [0f, true, 0]
JUMPI // [0]
// Skip reverting code
// We do a check to make sure the calldata size is big enough for a function selector and a uint256
JUMPDEST // [0]
POP // []
PUSH 0x04 // [4]
CALLDATASIZE // [24, 4]
LT // [false]
PUSH 0x32 // [32, false]
JUMPI // []
// Find the function selector and jump to it's code
PUSH 0x00 // [0]
CALLDATALOAD // [b6339418]
PUSH 0xe0 // [e0, b6339418]
SHR // [b6339418]
DUP1 // [b6339418, b6339418]
PUSH 0xb6339418 // [b6339418, b6339418, b6339418]
EQ // [true, b6339418]
PUSH 0x37 // [37, true, b6339418]
JUMPI // [b6339418]
// Setup the function by checking the calldata size, and setup the stack for the function
JUMPDEST
PUSH 0x47 // [47, b6339418]
PUSH 0x42 // [42, 47, b6339418]
CALLDATASIZE // [24, 42, 47, b6339418]
PUSH 0x04 // [4, 24, 42, 47, b6339418]
PUSH 0x5e // [5e, 4, 24, 42, 47, b6339418]
JUMP // [4, 24, 42, 47, b6339418]
JUMPDEST // [4, 24, 42, 47, b6339418]
PUSH 0x00 // [0, 4, 24, 42, 47, b6339418]
PUSH 0x20 // [20, 0, 4, 24, 42, 47, b6339418]
DUP3 // [4, 20, 0, 4, 24, 42, 47, b6339418]
DUP5 // [24, 4, 20, 0, 4, 24, 42, 47, b6339418]
SUB // [20, 20, 0, 4, 24, 42, 47, b6339418]
// See if the calldatasize minus the function selector size is smaller than 32 bytes
SLT // [false(0), 0, 4, 24, 42, 47, b6339418]
ISZERO // [true, 0, 4, 24, 42, 47, b6339418]
PUSH 0x6f // [6f, true, 0, 4, 24, 42, 47, b6339418]
JUMPI // [0, 4, 24, 42, 47, b6339418]
// Get the 77 value, and jump to the function selector code
JUMPDEST
POP // [24, 42, 47, b6339418]
CALLDATALOAD // [4d, 24, 42, 47, b6339418]
SWAP2 // [42, 24, 4d, 47, b6339418]
SWAP1 // [24, 42, 4d, 47, b6339418]
POP // [42, 4d, 47, b6339418]
JUMP // [4d, 47, b6339418]
JUMPDEST // [4d, 47, b6339418]
// Store our 77 value to storage and end the function call
PUSH 0x00 // [0, 4d, 47, b6339418]
SSTORE // [47, b6339418]
JUMP // [b6339418]
JUMPDEST // [b6339418]
STOP
```

这里有很多东西需要解开。这和 Huff 代码的主要区别是什么？

1.  我们设置了一个空闲内存指针。
2.  我们对发送的值进行了检查。
3.  我们检查了函数选择器的调用数据大小。
4.  我们检查了 uint256 的尺寸。

【Solidity 和 Vyper 的主要区别是什么？

1.  空闲内存指针设置。
2.  在某些地方，堆栈要深得多。

这两个因素结合起来似乎就是 Vyper 比 Solidity 便宜的原因。同样有趣的是，Solidity 使用 ISZERO 进行检查，Vyper 使用 XOR 不过，两者似乎需要差不多同样的汽油。正是这些小小的设计差异造就了所有的不同！

所以我们现在可以明白为什么 Huff 和 Yul 的汽油更便宜了:他们非常专注于做你让他们做的事情，而 Vyper 和 Solidity 试图保护你不做傻事。

## 空闲内存指针

那么这个空闲内存指针是怎么回事呢？这似乎在坚固性和 Vyper 的油耗上造成了很大的差异。空闲内存指针是一个控制内存管理的特性——任何时候你向内存数组添加东西，你的空闲内存指针就指向它的末尾，就像这样:

![A diagram of how Solidity memory works.](img/620d87a916b575266c7df99607b2eb48.png)

这很好，因为我们可能需要将动态数组这样的数据结构加载到内存中。对于动态数组，我们不知道它会有多大，所以我们需要知道内存在哪里结束。

在 Vyper 中，没有动态的数据结构，你被迫说出一个像数组这样的对象到底有多大。知道了这一点，Vyper 就可以在编译时分配内存，而没有空闲的内存指针。

![A diagram explaining how Vyper memory works.](img/8725fada7a1c4804266d770577b31514.png)

这意味着在内存管理方面，Vyper 可能比 Solidity 更适合 gas。缺点是，使用 Vyper，你需要显式地声明数据结构的大小，并且不能拥有动态内存。然而，Vyper 团队实际上将此视为优势。

## 动态数组

暂且把内存放在一边，使用 Vyper 确实需要声明数组的边界。在 Solidity 中，可以声明一个没有大小的数组。在 Vyper 中，你可以有一个动态数组，但是它必须是“有界的”。

这可能会让开发人员感到沮丧，然而，在 Web3 中，这也可以被看作是对拒绝服务攻击的保护，并防止您的功能中的大量气体成本。

如果你有一个变得太大的数组，你迭代它，它会耗费一吨的气体。但是，如果您显式地声明数组的界限，您将确切地知道您的智能合约的最坏情况性能是什么。

## 坚实度对尤尔对索尤尔

看着我上面的图表，使用 Solidity 和 Yul 似乎是最糟糕的选择，因为合同创建代码要昂贵得多。对于较小的项目来说可能是这样，因为 Solidity 做了一些体操来使 Yul 运行，但是在大规模上呢？

用 Solidity 版本和 SolYul 版本编写的最流行的项目之一是 [海港](https://github.com/ProjectOpenSea/seaport) 项目。

![A logo of the Seaport Project.](img/943aac9e4017c2724553c7a32dc537b7.png)

<figcaption id="caption-attachment-5040" class="wp-caption-text">[Seaport Project Logo](https://github.com/ProjectOpenSea/seaport).</figcaption>



使用这些语言的一个最好的方面是，你可以直接从源代码中运行命令来测试每个合同的 gas 有效性。我们添加了一个 [拉式请求](https://github.com/ProjectOpenSea/seaport/pull/646/files) 来帮助测试纯固体合同的气体成本，因为 Sol-Yul 合同已经进行了测试。这个结果是相当惊人的，你可以在[gas-report . txt](https://github.com/PatrickAlphaC/seaport/blob/added-gas-profiling-for-reference-contracts/gas-report-reference.txt)和[gas-report-reference . txt](https://github.com/PatrickAlphaC/seaport/blob/added-gas-profiling-for-reference-contracts/gas-report-reference.txt)中看到所有的数据。

![A graph comparing gas cost between Solidity and SolYul for contract creation.](img/7f1434425990abb84fee284ab107e43a.png)

<figcaption id="caption-attachment-4768" class="wp-caption-text">Contract creation gas cost differences in Seaport.</figcaption>



![A graph showing gas cost differences for function calls in Solidity vs SolYul](img/c99f21185216482e96273d54e4afe708.png)

<figcaption id="caption-attachment-4769" class="wp-caption-text">Function calls gas cost differences in Seaport.</figcaption>



平均而言，SolYul 版本的函数调用性能提高了 25%,契约创建性能提高了 40%。

节省了很多汽油。我想知道他们在纯粹的圣诞节能省下多少钱？我想知道在维普对索尔-尤尔的比赛中他们能省下多少钱？

## [计]元数据

最后，元数据。Vyper 和 Solidity 都在合同末尾添加了一些额外的“元数据”。尽管数量如此之少，我们在这里进行比较时基本上可以忽略不计。你总是可以手动砍掉它(并根据你的 Solidity 代码的长度调整标记)，但是 Solidity 团队也在开发一个 PR，你可以在编译时删除它 [。](https://github.com/ethereum/solidity/pull/13265)

## 摘要

以下是我对这些语言的看法:

1.  如果你正在编写智能合同，使用 Vyper 或 Solidity。它们都是高级语言，通过查看调用数据大小以及是否在不应该的时候意外发送了 ETH，可以防止你搬起石头砸自己的脚。这两种语言都很棒，所以随便挑一种，玩得开心点。
2.  如果你需要特别高性能的代码，Yul 和 Huff 是很好的学习资源或工具。我不推荐大多数人用这些语言写作，但是我认为学习和理解它们都很棒。它们都会让你对 EVM 有更好的了解。
3.  Solidity 和 Vyper 在 gas 成本上的一个主要区别是 Solidity 中的空闲内存指针——当你达到高级水平并希望了解这两种工具之间的一个根本区别时，请记住这一点。

## 展望未来

这些语言将继续发展，我们很可能会看到更多的语言出现，如 [Reach 编程语言](https://docs.reach.sh/) [和 fe](https://fe-lang.org/) 。

Solidity 和 Vyper 团队致力于中间表示的编译步骤。Solidity 团队在产品中有一个“via-ir”标志，这将有助于优化 Solidity 代码，Vyper 团队也有他们的“毒液”中间表示。

无论你选择哪种语言，你都可以写出一些很棒的智能合同。编码快乐！

*本文中表达的观点仅是作者个人的观点，并不代表链家基金会或链家实验室的观点和信念。T3】***