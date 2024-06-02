# 第四章\. 区块链

在我们深入了解区块链技术的任何技术细节之前，了解区块链解决的问题很重要。我们为什么需要区块链，以及它做了什么，我们的现有技术做不到？

比特币和区块链技术的早期采用者发现了他们在交易、信任和社会制度方面的根本性缺陷的看法。最早的区块链版本正是在 2007 年美国金融危机前后出现的，当时许多人失去了对本应保护普通人利益的 societal institutions 的信心。当然，危机之后人们对银行系统的幻想破灭了，但他们还失去了对政府调节金融市场的信心和对媒体调查潜在危机的信心。

大多数人会同意我们的制度存在缺陷，并不是完美的解决方案。但它们确实解决了信任问题，并且它们已经这样做了数百年。事实上，我们可能正生活在人类历史上最和平、最舒适的时期。任何对我们当前制度的替代品都需要有明确的优点和优势。

区块链背后的想法是用能做得更好的技术替换由不完美的人类运行的机构，同时也赋予个人权力。如果你能创造一种让陌生人彼此信任的方式，而不需要银行或政府作为中介，你就能解决社会最大的瓶颈之一。但为了做到这一点，你需要一个强大的系统来在陌生人之间创建共识，区块链的创造者认为力量在于去中心化。

基本上，所有区块链（及其他加密技术）的应用都围绕去中心化的概念。而不是一个僵化、缓慢的中心权威做出决策和治理关系，区块链试图将监管权力归还给个人。不是信任一个主要机构，区块链通过共识建立信任。

## 区块链是如何工作的？

用最简单的话来说，区块链通过结合密码学和公共账本来在各方之间建立信任的同时保持隐私。深入理解这一机制的工作原理稍微有些困难，但为了全面欣赏区块链技术的巧妙之处，我们需要深入了解其技术细节。

区块链虽然可以包含更多功能，但其核心在于其技术的名称所体现的基本原理：

区块：区块是一段时间内交易列表。它包含了网络在过去几分钟内处理的所有信息。网络一次只创建一个区块。

链：每个块通过加密算法与之前的块链接。这些算法对计算机来说很难计算，通常需要世界上最快的计算机几分钟时间来解决。一旦解决，加密链将块锁定到位，使其难以更改。我们稍后会更深入地了解这一点。

链随时间变得越来越长。一旦创建了一个新块，网络上的计算机就会一起工作，验证块中的交易并确保该块在链中的位置。

区块链最基础的部分是账本。这里存储着网络上账户的信息。区块链内的账本替代了银行或其他机构中的账本。对于加密货币来说，这个账本通常由账户号码、交易和余额组成。当你向区块链提交交易时，你正在向账本中添加关于货币来源和去向的信息。

区块链账本是分布在整个网络中的。网络上的每个节点都保留着账本的一份副本，并在有人提交新交易时更新它。这种“共享账本”是区块链试图取代银行和其他机构的方式。银行保存一个官方账本副本，每个人都会保留他们自己的账本副本，然后我们通过共识来验证交易。

每种区块链技术都有自己的账本，各种账本工作方式非常不同（我们稍后会看到）。然而比特币账本，第一个区块链账本，需要三部分信息来记录一笔交易：

1.  输入：如果约翰想要发送一个比特币给大卫，他需要告诉网络他最初从哪里得到这个比特币。也许约翰昨天从莎拉那里收到了比特币，所以账本条目的第一部分就这样说明了。

1.  金额：这是约翰想要发送给大卫的金额。

1.  输出：这是大卫的比特币地址，以及比特币应存放的位置。

现在来谈谈难以理解的概念：比特币这种东西根本不存在。当然，物理比特币也是不存在的。你可能已经知道了这一点。然而，某个硬盘上的比特币也是不存在的。你不能指向一个物理物体、数字文件或代码片段并说：“这就是比特币。”相反，整个比特币网络只是一系列交易记录。比特币历史上的每一笔交易都存储在比特币区块链的分布式账本中。如果你想证明你拥有 20 个比特币，你能做的唯一方式是指向那些你收到 20 个比特币的交易。

几乎所有的区块链都具有这一共同特征：交易历史就是货币，两者没有区别。一些新的加密货币正在改变记账的方式，以在交易中提供更大的匿名性和隐私性。它们使用某些身份遮蔽技术来隐藏交易的发送者和接收者，同时仍保持一个功能性的分布式账本。

### 创建区块

账本是区块的核心，但它不是构成新创建区块的唯一东西。每个区块都需要有一个头部和底部。此外，区块中包含的交易要经过一个压缩、编码和标准化的过程。当验证者创建一个新的区块时，它看起来与基于它的账本完全不同。然而，底层的账本仍然存在，并且可以在将来新的交易需要关于之前区块的信息时被访问。

### 添加交易

构建区块的第一步是将所有当前的交易收集添加到区块的账本中。当用户创建一个新的交易时，他们会将该交易广播到整个网络。然后验证者的计算机将审查交易以确保它是有效的。

由于区块链货币不过是一系列交易，验证交易的第一步是查看发送者说他们最初从哪里得到钱。验证者然后将查看区块链的历史，找到发送者收到钱的区块和交易。如果那个输入交易在区块链上得到确认，那么交易是有效的，他们需要确认接收方的地址。如果输入交易没有得到确认，那么当前交易是无效的，它不会被包含在账本中。

当一个区块中的所有交易都被验证后，该是创建账本的时候了。这是一个简单的例子，其中交易被一个接一个地列出：

输入[金额][输出地址]，输入[金额][输出地址]，输入[金额][输出地址]，输入[金额][输出地址]，输入[金额][输出地址]...

然后验证者将对每个交易应用一种加密技术，称为哈希。在最基本的定义上，哈希取一个字符串并生成另一个字符串。所以，当你将输入、金额和输出地址喂给哈希算法时，它会将交易转换成只对该交易独特的字符串，如下所示：

aba128d3931e54ce63a69d8c2c1c705ea9f39ca950df13655d92db662515eacf

（这是一个来自比特币区块链的实际交易哈希。）

因此，哈希用于标准化数据，同时确保它没有被篡改。如果有人试图在区块链中更改交易，他们必须重新哈希那个交易，它看起来会完全不同。很明显它被篡改了。

为了使篡改区块链变得更加困难并减少存储交易账本所需的内存，大多数区块链进行了多次哈希。这意味着他们取一个交易的哈希，将其与另一个交易的哈希结合，然后重新哈希成一个新的较小的哈希。以这种方式组合交易被称为默克尔树，所有交易的根哈希包括在区块的开始处。理解我们为什么需要默克尔树是一个更深入的话题，但在基本层面上，默克尔树显示了区块中的所有交易都是有效的，同时长期使用内存更少。

### 时间戳和区块 ID

区块中的最后一个元素是时间戳和任何区块 ID 信息。这样使得以后查找之前的区块变得容易。未来的交易也将能够指向这个区块 ID，作为包含当前交易输入交易（也称为“币基”）的区块。

### 链接区块在一起

创建区块的最后一步是将它链接到链中的前一个区块。有几种方法可以做到这一点，但几乎所有方法都涉及到以某种方式哈希，使前一个区块的内容成为新区块的一部分。

记住，哈希无论输入大小如何，都会将其转换为字符串。即使输入稍微改变，整个输出也会改变。为了将前一个区块的内容包括在新区块中，我们可以取整个前区块的哈希并将其添加到下一个区块的开始处。这样做意味着我们有效地链接了旧区块到新区块，因为如果旧区块中发生任何变化，即使是最小的变化，整个区块的哈希也会改变。

现在，一旦一个区块完成，要修改它就变得非常困难。对一个较旧的区块进行编辑意味着你必须重新哈希整个区块。一旦你重新哈希了整个区块 1，你必须打开区块 2，删除区块 1 的旧哈希，插入区块 1 的新哈希，现在重新哈希整个区块 2。但新的区块正在不断创建，所以为了改变一个较旧的交易，你必须编辑那个交易发生后所有的区块。随着时间的推移，黑客网络和成功改变交易变得越困难。这就是哈希是区块链安全核心的原因。密码学使交易账本难以更改，意味着账本可以同时是公共和安全的。

然而，散列（hashing）本身并不那么困难。大多数计算机都能在几秒钟内重新散列一个区块链。因此，为了保证散列安全起作用，我们需要在新区块的创建中引入一定的难度。理想情况下，这应该是一些能够减缓攻击者速度，并使网络中诚实的成员更有可能获胜的东西。在比特币区块链（以及大多数其他现代区块链）中，这种增加的难度被称为“工作量证明”（proof of work）。

在这里我不会解释工作量证明，关于工作量证明的基本解释我在这本书的第三章中已经涵盖，或者你可以通过阅读我的书《[区块链技术解释](https://www.amazon.com/Blockchain-Technology-Explained-Beginners-Contracts-ebook/dp/B0785WDHS3/ref=sr_1_5?ie=UTF8&qid=1513029050&sr=8-5&keywords=blockchain)》来了解这项技术的深入细节。