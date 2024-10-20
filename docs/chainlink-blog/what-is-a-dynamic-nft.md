# 什么是动态 NFT？

> 原文：<https://blog.chain.link/what-is-a-dynamic-nft/>

在 Web3 社区获得广泛采用后，[](https://chain.link/education/nfts)不可替代代币(NFT)正在成为主流，各大媒体成为焦点，一系列知名运动员和公众人物推出了自己的系列。因此，NFTs 已经成为区块链技术最著名的应用之一。

NFTs 发展的下一步才刚刚开始。动态 NFT(dnft)正在扩展设计空间，NFT 能够通过其适应和改变以响应外部事件和数据的能力来解决这个问题。在本文中，我们将介绍什么是 NFT，dNFT 如何将它们带到下一个层次，当前和潜在的 dNFT 用例，以及那些希望构建 dNFT 的人如何利用 Chainlink 来访问信任最小化的链外数据和计算。

## 了解 NFTs

简单地说，NFT 是存在于区块链上的独特的数字对象。每个 NFT 都可以通过一对一令牌 ID 及其唯一的合同地址来区分。从那里，可以附加图像、视频文件或其他数据等元数据，这意味着有可能拥有一个代表唯一数字对象的令牌。

当前最常见的 NFT 用例是数字艺术；艺术家铸造代表数字艺术品的代币，收藏家可以购买该代币，标记他们的所有权。一旦创建了 NFT，它们的 tokenIDs 就不会改变。请记住，属性元数据(包含 NFT 的描述、影像等内容)是完全可选的。最简单的形式是，NFT 只是一个具有唯一 tokenID 的可转移令牌。

这种静态的 NFT 模式为世界各地的数字艺术家提供了许多好处。在此之前，数字艺术家无法阻止，甚至无法跟踪未经授权的原创作品的分发，因为没有办法区分任何两个文件之间的差异，因此没有一个真正的文件可以被拥有。互联网历史上第一次，创作者可以通过向粉丝提供可验证的所有权来出售数字艺术，而粉丝可以证明他们拥有一件原创艺术品，即使底层图像是复制的。

## 用动态 NFT(dnft)超越静态 NFT

静态 NFT 是目前最常见的 NFT 类型，大部分用于 NFT 艺术项目和 [即玩即赚](https://blog.chain.link/what-is-play-to-earn/) 游戏项目以及作为数字收藏品。除了这些用例，它们还为现实世界中的数字化项目提供了独特的价值主张，例如房地产契约、专利和其他唯一标识符。

然而，这种模型受限于静态 NFT 的持久性，因为一旦在区块链上创建了它们，附加到它们的元数据就固定了。诸如虚拟化现实世界的资产、构建基于进程的视频游戏或创建基于区块链的梦幻体育联盟等用例经常需要更新数据。dNFTs 提供了一种两全其美的方法，让 NFT 保留它们的惟一标识符，同时能够更新它们的元数据的某些方面。

简单地说，动态 NFT 是一个可以根据外部条件变化的 NFT。dNFT 中的更改通常指智能合约触发的 NFT 元数据的更改。这是通过在 dNFT [智能契约](https://chain.link/education/smart-contracts) 内对自动变化进行编码来完成的，该智能契约向底层 NFT 提供关于其元数据应当何时以及如何变化的指令。

![A diagram showing how dNFTs can be upgraded](img/68f660a4cef2c425628625f7ed55ec29.png)

<figcaption id="caption-attachment-3605" class="wp-caption-text">dNFTs can be upgraded in multiple ways based on external conditions.</figcaption>



除了元数据变更之外还可以存在动态元素。例如，dNFTs 可以基于某些条件来创建，例如当在增强现实应用中发现隐藏点时。动态 NFT 还可以包含通过用户交互而不是在元数据中表现出来的“隐藏特征”。作为完全唯一和可定制的令牌，NFT 可以通过无数种方式进行编程。然而，大多数动态 NFT 必须实现某种形式的元数据更改，以便非技术用户“看到”这些更改。

### 潜在的使用案例

NFT 元数据是指定令牌名称、分配特征和放置文件链接的地方。虽然 tokenID 为可验证的所有权提供了永久标识符，但元数据是 NFT 的本质，包含使其有用的元素。

NFT 艺术项目通常具有多种多样的特征，其中一些较为罕见。这些特征被放置在 NFT 的元数据中，旁边是与 NFT 特征相对应的图像或视频的 IPFS 链接。在 dNFT 中，这些特征根据外部条件而变化。

在区块链游戏中，这一功能对角色进展非常有用，这是许多不同游戏模式的核心原则。当第一次用一个可玩的 dNFT 角色开始一个游戏时，dNFT 的元数据中反映了基础统计数据。随着玩家继续升级，dNFT 中的元数据会发生变化，以反映角色的成长。

![A diagram showing how NFT traits can be upgraded to trigger visual changes](img/b8ccf9690b5e18ba02a6ddb1a9060389.png)

<figcaption id="caption-attachment-3606" class="wp-caption-text">In-game character dNFTs can be upgraded to reflect player progression.</figcaption>



元数据变更有用的另一个例子是现实世界资产的标记化，在这种情况下经常需要大量变更的指标。例如，代表一个属性的 dNFT 可以反映它的维护历史、年龄、市场价值等等。因此，对这些不断变化的资产进行标记需要 NFT，它能够用不断变化的元数据进行更新。

![A diagram showing how a dNFT can represent a real-world house and associated data](img/5bed00be6c22a4d6b4031a1426ba1db0.png)

<figcaption id="caption-attachment-3607" class="wp-caption-text">The metadata of dNFTs representing property can change to reflect maintenance history, past sales, and more.</figcaption>



这些只是 dNFTs 的几个假设使用案例。实际上，对 dNFT 的元数据的改变可以由任意数量的链外或链内事件触发，也就是说[dNFT 对于扩展 NFT 设计空间](https://blog.chain.link/create-dynamic-nfts-using-chainlink-oracles/) 具有无限的潜力。

虽然当前的 Web3 生态系统主要由静态 NFT 组成，但一些杰出的项目已经启动了 dNFT 创新。

## 动态 NFT 示例

### 拉梅洛·鲍尔国家森林公园

在过去的一年里，职业体育运动员，如 NBA 的后起之秀拉梅洛·鲍尔，创造了开创性的 dNFTs，利用 Chainlink 体育数据馈送重新定义了球员与球迷的关系。

目前有八种不同的 [拉梅洛·鲍尔 NFTs](https://blog.chain.link/how-lamelo-ball-dynamic-nfts-redefine-player-fan-experience/) ，每种 NFT 都记录着一组不同的拉梅洛的球员统计数据，从篮板和助攻到得分。根据拉梅洛的持续表现，NFT 持有者可以获得莱佛士和其他 NFT 特有的特殊待遇。

这八个 NFT 之一，黄金进化者 NFT，有一个独特的承诺:如果拉梅洛·鲍尔赢得 2021 年 NBA 赛季的年度最佳新秀，dNFT 本身将进化以反映一个新的形象。拉梅洛获得了这个奖项，dNFT 也随之发展。

<video style="width: 100%;" autoplay="autoplay" loop="loop" muted="" width="600" height="336"><source src="https://blog.chain.link/wp-content/uploads/2022/07/unnamed-3.webm" type="video/webm">T2】</video>

拉梅洛·鲍尔 NFT 是根据外部数据不断变化的 dNFTs 的典型例子。在这种情况下，LaMelo 的玩家统计数据会在 dNFT 中不断更新，并可以触发显示升级、奖励等。

### 再生资源短片 NFTs

再生资源公司(RRC)是一家生态系统服务公司，旨在将退化的土地转化为多产的海水景观。

RRC [宣布](https://medium.com/@neal.spackman/our-first-web3-project-100-million-mangroves-via-dynamic-chainlinked-nfts-7e2b55d2c2ee) 将推出五部由杰出艺术家设计的动态短片 dNFTs，资金将用于 RRC 当前项目中播种和种植 1 亿棵红树林。

每个短片 dNFT 最初只有一帧。然而，每次购买或转售 dNFT 时，都会在连续的过程中释放更多帧，直到持有者可以观看整个短片。

## Chainlink 如何支持 dNFTs

dNFT 设计中一个经常被忽视的部分是如何可靠地获取构建安全、公平和自动化的 dNFT 流程所需的信息和功能。

如上所述，基于 **外部条件** ，可以以多种方式触发 NFT 元数据的动态变化。这些条件可以存在于链上和链下。但是， [天生无法](https://blog.chain.link/what-is-the-blockchain-oracle-problem/) 访问 [链外数据和计算](https://blog.chain.link/how-chainlink-supports-any-off-chain-data-resource-and-computation/) 。

[Chainlink](https://chain.link/) 通过提供可用作触发 dNFT 更新的输入的各种链外数据和计算服务，使这些限制得以克服。随着 dNFT 生态系统的扩展，NFT 与现实世界的整合程度越来越高，Chainlink 在两个互不关联的世界之间架起了一座桥梁，实现了自动化、分散化和参与式 dNFT 流程的构建。

### Chainlink 数据馈送和任何 API

[chain link Data Feeds](https://data.chain.link/)是一个离链数据交付服务，可以安全地交付体育比赛结果、天气预报或任何其他类型的数据，用于更新 dNFT。对于项目特有的数据产品，Chainlink 还可以通过[chain link Any API](https://docs.chain.link/docs/request-and-receive-data/)实现任何 API 和 NFT 智能合约之间的无缝连接。

这项服务对于像拉梅洛·鲍尔 dNFTs 这样需要链上体育数据来触发元数据更改的用例来说至关重要。然而，这只是无数潜在用途中的一种。作为使用最广泛的分散式 oracle 网络，Chainlink 的定位是为任何使用真实世界数据的 dNFT 提供链外数据。

### 链环自动化

[chain link Automation](https://chain.link/automation)是一种安全的智能合同自动化服务，可用于在满足预定义条件时触发动态 NFT 变更；当他达到某个统计阈值，例如 1000 分时，触发 La Melo 球 NFTs 中的视觉变化。

Chainlink Automation 为构建真正自主和分散的 NFT 流程提供了一条简单的途径，并有助于确保用户所有的 d NFT 完全按照详细说明工作。与 Chainlink 数据馈送和任何 API 相结合，Chainlink Automation 可以实现自动化和引人入胜的购物奖励 dNFT 程序的开发、通过 dNFT 的环保行为跟踪等等。

![A diagram showing a hypothetical loyalty rewards program that leverages both Chainlink Data Feeds and Keepers.](img/f0fcf7d5837c9c7cec3fbd1c040a86a4.png)

<figcaption id="caption-attachment-3609" class="wp-caption-text">Retail stores can build robust, automatically executing loyalty reward programs by leveraging Chainlink services within dNFTs.</figcaption>



### 链环可验证随机函数(VRF)

[Chainlink VRF](https://docs.chain.link/docs/chainlink-vrf/) 是一个可验证的 RNG，可用于快速启动 dNFT 中的动态变化——这是一个与 GameFi 项目特别相关的功能。随机性是绝大多数视频游戏不可或缺的一部分，用于确定攻击的成功率，决定什么物品从战利品盒中出来，甚至做一些如决定角色的衬衫在使用布料染料后将是什么颜色这样的具体事情。

因为“玩即赚”游戏具有真正的价值，所以他们使用的 RNG 机制必须透明且防篡改，这一点至关重要。

## 将 NFTs 带入生活

Chainlink 提供了构建下一代 dnft 所需的链外数据和计算，涵盖广泛的使用案例，为 dnft 实现主流采用铺平了道路。

作为可验证的独特数字对象，NFT 赋予了数字世界以有形性 dNFTs 是推进这一范式转变的自然下一步。

要了解更多关于动态 NFTs 的信息，请查看以下内容:

*   [如何在多边形上建立动态 NFTs](https://blog.chain.link/how-to-build-dynamic-nfts-on-polygon/)
*   [打造、部署、销售自己的动态 NFT](https://blog.chain.link/build-deploy-and-sell-your-own-dynamic-nft/)
*   [用拉梅洛·鲍尔 dNFTs](https://blog.chain.link/how-lamelo-ball-dynamic-nfts-redefine-player-fan-experience/) 重新定义玩家-粉丝体验