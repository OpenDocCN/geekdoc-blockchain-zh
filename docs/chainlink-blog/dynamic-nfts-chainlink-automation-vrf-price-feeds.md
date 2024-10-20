# 如何使用三链信任最小化服务构建动态 ERC-721 NFT

> 原文：<https://blog.chain.link/dynamic-nfts-chainlink-automation-vrf-price-feeds/>

[](https://blog.chain.link/what-is-a-dynamic-nft/)动态 NFT 本身就很有趣，但它们也有助于更好地理解智能合约技术，提高软件设计技能，以及学习如何使用在行业中广泛使用的令人兴奋的新工具。

![LaMelo Ball dynamic NFT](img/890c51b077ece8e080ad752bc151a499.png)

<figcaption id="caption-attachment-4229" class="wp-caption-text">This NFT of NBA player LaMelo Ball changed after he won Rookie of the Year.</figcaption>



在这个项目中，我们将构建一个动态的 NFT，它不仅会更新，而且会随机更新——它的图像会根据资产的价格而变化，这将从 [Chainlink 价格馈送](https://docs.chain.link/docs/get-the-latest-price/) 中获得。新图像将被随机选择。如果价格上涨，就会出现一个公牛的图像。

![Bull Dynamic NFTs](img/bc543f5d71311ede2ba33193b803a825.png)

<figcaption id="caption-attachment-4230" class="wp-caption-text">The three bull images for the dynamic NFTs.</figcaption>



如果价格下跌，就会出现一只熊的图片。

![Bear Dynamic NFTs](img/b6dd33a7642303195dbe8427dadf0169.png)

<figcaption id="caption-attachment-4231" class="wp-caption-text">The three bear images for the dynamic NFTs.</figcaption>



无论哪种方式，实际图像都是随机选择的。

在区块链上实现真正的随机性是一个非常困难的问题，因为它们的一致性算法的工作方式决定了它们固有的确定性。但是使用[chain link VRF](https://docs.chain.link/docs/chainlink-vrf/)就很容易了，它是一个可证明公平且可验证的随机数生成器(RNG)，使智能合约能够访问随机值，而不会损害安全性或可用性。

动态 NFT 将自动对市场变化做出反应，开发商无需检查价格或触发 NFT 变化。在 [Chainlink Automation](https://chain.link/automation) 的帮助下，这是可能的，它自动化了项目，因此一旦部署了您的 NFT，您需要做的就是保持您的 VRF 订阅和自动化注册表由链接令牌资助。 智能合同执行和动态 NFT 选择以可验证和密码安全的分散方式完成。

## 这是给谁的

这个项目假设你有一些编码知识，最好是 JavaScript 或 Python 这样的语言。我们在 Solidity 中编写智能合同，所以如果你以前没有使用 Solidity 的经验，你应该看看 Alchemy 编写的[web 之路 3](https://docs.alchemy.com/alchemy/road-to-web3/welcome-to-the-road-to-web3) 程序(该项目最初是为该系列创建的！).你也可以在 这里找到进一步的教育资源 [。](https://blockchain.education)

你可以在基于浏览器的混音代码编辑器中完成整个项目。您将在这里找到这个项目的 [Github 回购](https://github.com/zeuslawyer/chainlink-dynamic-nft-alchemy)——回购中的每个分支代表项目中的一个阶段。

## 项目阶段

以下是构建项目的阶段:

*   构建基线 ERC-721 令牌。我们使用 [OpenZeppelin 向导](https://docs.openzeppelin.com/contracts/4.x/wizard) 为此生成被审计的库代码。参考回购的 主 分支可以按照这个步骤操作。
*   添加 Chainlink 自动化实现并连接到 Chainlink 价格馈送，以跟踪特定资产的价格。你可以在参考回购的价格馈送分支中遵循这个步骤。
*   添加可验证的随机性，以便我们的动态 NFT 图像是从可用的 NFT 图像中随机选择的。这部分是给你的，作为一个特殊的任务来培养你的技能！你可以按照这个步骤在 随机性 分支中参考回购。

## 你将学到的东西

这个项目将教会你:

*   如何编写、构建和设计 Solidity 智能合同代码
*   ERC-721 非可替代令牌的基本原理及其功能
*   如何使用基本工具，如 Remix、开放式 Zeppelin 库和三大链接服务
*   智能合约如何相互作用

你可以用两种方法中的一种来做这件事——你可以跟随下面的 [视频教程](https://www.youtube.com/watch?v=hNdXSMKLDi4&t=2567s) 或者跟随《炼金术之路 3》第五课的这个 [动态 NFT 教程](https://docs.alchemy.com/alchemy/road-to-web3/weekly-learning-challenges/5.-connect-apis-to-your-smart-contracts-using-chainlink) 的扩展书面版本。

[https://www.youtube.com/embed/hNdXSMKLDi4?start=2567&feature=oembed](https://www.youtube.com/embed/hNdXSMKLDi4?start=2567&feature=oembed)

## 更多可能性！

完成后，你可以通过使用安全帽和 Solidity 建立自己的[NFT 市场，进一步扩展你的巧妙合同技巧。本教程向您展示了如何为一个市场编写逻辑，该市场允许用户列出商品，然后购买和出售它们，并提取他们的收入。](https://blog.chain.link/how-to-build-an-nft-marketplace-with-hardhat-and-solidity/)

如果你想更深入地了解，请查看 [如何在多边形](https://blog.chain.link/how-to-build-dynamic-nfts-on-polygon/) 上构建动态 NFTs，以及如何 [构建、部署和销售你自己的动态 NFT](https://blog.chain.link/build-deploy-and-sell-your-own-dynamic-nft/) 。你还可以阅读更多关于拉梅洛·鲍尔 dnft如何重新定义玩家粉丝体验的内容。

访问[chain . link](https://chain.link)或阅读[docs . chain . link](https://docs.chain.link/)上的文档，了解更多关于 Chainlink 的信息。您还可以订阅 [Chainlink 简讯](https://chn.lk/newsletter) 以了解 Chainlink 堆栈中的最新信息。 [要讨论一个整合，就要联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF?typeform-source=blog.chain.link) 。如果你正在寻找一个端到端的区块链开发者教育，请查看[block chain . education](https://blockchain.education)。