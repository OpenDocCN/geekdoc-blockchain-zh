# 如何在多边形上得到一个随机数

> 原文：<https://blog.chain.link/how-to-get-a-random-number-on-polygon/>

[多边形](https://polygon.technology/) (原名 [Matic Network](https://matic.network/) )是构建和连接兼容以太坊的区块链网络的协议和框架。最初专注于利用 Proof of of Stake(PoS)侧链和 Plasma 框架的以太坊扩展解决方案，在更名为 Polygon 的过程中，他们还添加了其他主要的扩展解决方案，如 ZK-roll up 和 Optimistic Rollups，以及链间通信协议。

作为最广泛采用的分散式 [oracle](https://chain.link/education/blockchain-oracles) 网络，Chainlink 是 Polygon 中安全获取外部数据和使用防篡改数据馈送的首选 oracle 网络。最近，Chainlink VRF [在 Polygon mainnet](https://polygontech.medium.com/chainlink-vrf-is-live-on-polygon-providing-developers-with-a-secure-source-of-verifiable-94ec9815bc03) 上线，为开发者提供了在其智能合同中请求可验证随机数的能力。在本技术教程中，我们将向您展示如何部署一个[智能合同](https://chain.link/education/smart-contracts)到多边形，并使用 VRF 链获得一个可证明的随机数。

## 对可证实的随机性的需求

Chainlink VRF 是一个为智能合约设计的可证明公平和可验证的随机性来源。Solidity 开发人员可以将其用作防篡改随机数生成器，为依赖不可预测结果的以太坊应用程序构建安全可靠的智能合约。至关重要的是，Chainlink VRF 不仅提供随机数，还提供密码证明该数字没有被篡改以产生某些可预测的结果。

在智能合约中拥有可验证的随机数使开发人员能够构建广泛的用例，如游戏中的[随机性](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/#gaming-and-randomness)，NFTs 中的随机奖励，[彩票](https://blog.chain.link/how-to-build-a-blockchain-lottery-2/)，以及[公平参与者或随机节点选择](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/#other)。

一个值得注意的现实世界的例子是 [NFT](https://chain.link/education/nfts) 游戏 dApp [Aavegotchi](https://aavegotchi.com/) ，[集成了 Chainlink VRF](https://aavegotchi.medium.com/chainlink-vrf-launches-on-polygon-enabling-provably-rare-aavegotchis-d03e36698795) 作为其可证明的公平随机性的来源，以帮助确定 Aavegotchi 的独特特征，生成不可预测的游戏场景，并随机选择 DAO 陪审员。Aavegotchi 已经在 Polygon 的第二层 PoS 链上推出了,由于接近零的交易费用和快速的结算时间，允许他们经济高效地扩展以满足用户需求。

既然我们已经理解了受益于可验证的随机性的用例，我们将在 Polygon Mumbai Testnet 上演示如何在智能合约上获得可验证的随机数。

## 在多边形上使用链环 VRF

### 连接到多边形孟买测试网

在 Polygon 的 PoS 链上使用 Chainlink VRF 的第一步是设置您的 MetaMask 钱包[连接到 Matic Mumbai Testnet](https://docs.matic.network/docs/develop/metamask/config-matic/) 。为此，您可以选择“网络”，然后选择“自定义 RPC”并输入以下详细信息:

![Details on how to enter the Mumbai Testnet](img/da65e4d57f9791a0bbd5d9d9a5b1682f.png)

<figcaption id="caption-attachment-1648" class="wp-caption-text">Entering the Mumbai Testnet details</figcaption>



### 获取 Testnet MATIC 和链接

MATIC 是多边形网络的原生令牌，需要与网络交互，类似于 ETH 如何被用作以太坊的 gas。要获取 Mumbai Testnet MATIC，请前往 [MATIC 水龙头](https://faucet.matic.network/)，选择 MATIC 令牌和 Mumbai Testnet 网络，输入您的 MetaMask 钱包地址，然后按提交。

与 MATIC 令牌类似，LINK 令牌需要作为对 VRF 协调器的支付，以完成随机数请求。要获得 testnet 链接，只需选择水龙头中的 LINK 标记，而不是 MATIC 标记。

![A picture showing how to obtain MATIC and LINK from the Mumbai testnet](img/18775179ac212025c15fd7791da0f63d.png)

<figcaption id="caption-attachment-1649" class="wp-caption-text">Obtaining Mumbai Testnet MATIC and LINK</figcaption>



虽然在 Mumbai Testnet 上使用水龙头获取链接的过程相对简单，但是在转到 Polygon 的 Mainnet 时就有点复杂了。这是因为由[多边形桥](https://wallet.matic.network/bridge)提供的链接与 [ERC-677](https://github.com/ethereum/EIPs/issues/677) 不兼容，所以它不能与 Chainlink oracles 一起使用。然而，它可以使用 Chainlink 的 [PegSwap 服务](https://pegswap.surge.sh/)转换为 Polygon 上的官方链接令牌，本质上创建了链接令牌的包装版本。

### 构建智能合同

开始构建在多边形上使用 Chainlink VRF 的智能合约的最简单方法是从标准的 [Chainlink VRFConsumer](https://remix.ethereum.org/#version=soljson-v0.6.6+commit.6c089d02.js&optimize=false&evmVersion=null&gist=536123b71478ad4442cfc4278e8de577) 合约开始。这是一个基本的标准化合同，用于通过链接 oracle 发起对随机数的请求。因此，我们将通过上面的链接打开这个合同，并相应地修改它。

*   孟买测试网的 VRF 协调员是*0x8c 7382 F9 D8 f 56 b 33781 Fe 506 e 897 a 4 f1 e 2d 17255*
*   孟买测试网上链接令牌的地址是*0x 326 c 977 e 6 EFC 84 e 512 bb 9 c 30 f 76 e 30 c 160 ed 06 FB*
*   孟买测试网的 KeyHash 是*0x6e 75 b 569 a 01 ef 56d 18 cab 6 A8 e71e 6600 D6 ce 853834 d4a 5748 b 720d 06 f 878 B3 a4*
*   在孟买测试网上提出 VRF 请求的费用是*10000000000000*(0.0001 链接)

```
constructor() 
        VRFConsumerBase(
            0x8C7382F9D8f56b33781fE506E897a4F1e2d17255
            0x326C977E6efc84E512bB9C30f76E30c160eD06FB
        ) public
    {
        keyHash = 0x6e75b569a01ef56d18cab6a8e71e6600d6ce853834d4a5748b720d06f878b3a4;
        fee = 100000000000000; // 0.0001 LINK
    }
```

现在我们的合同已经准备好被编译并部署到孟买测试网。

### 部署和测试智能合约

在 Remix 中编译合同，然后在 deployment 选项卡上，将环境更改为“Injected Web3”，并确保下面的 wallet 地址是包含 MATIC 和 LINK 令牌的 MetaMask wallet 中的地址，按 deploy 按钮，然后按照步骤操作。最终结果是您将智能合同部署到了孟买测试网。您应该通过 Remix 控制台中的事务输出注意到部署的契约地址。

下一步是为与 LINK 的合同提供资金，以便它可以向 VRF 协调员发送请求。要做到这一点，只需从上面的步骤中获取已部署的契约地址，然后从 MetaMask wallet 向它发送至少 0.0001 个链接。

![How to fund a contract with LINK.](img/4719abbdd6dcc5f90ec9d686ca0033a4.png)

<figcaption id="caption-attachment-1650" class="wp-caption-text">Funding the contract with LINK</figcaption>



一旦使用 LINK 部署并资助了合同，我们就可以通过执行“getRandomNumber”函数请求一个随机数，并传入一个给定的[种子](https://en.wikipedia.org/wiki/Random_seed)作为参数。这将把请求和种子一起发送给 VRF 协调员。记住，选择一颗[难以影响或预测](https://docs.chain.link/docs/chainlink-vrf-api-reference#choosing-a-seed)的种子是极其重要的。

![How to enter a seed and send a request to the VRF Coordinator](img/ddcaa456aea99102ca2ed9f6c3906983.png)

<figcaption id="caption-attachment-1651" class="wp-caption-text">Entering a seed and sending a request to the VRF Coordinator</figcaption>



处理完该事务后，我们等待几秒钟，让 Chainlink oracle 完成对随机数的请求，然后调用我们之前创建的“fulfillnommandations”函数将随机数返回给我们的消费者契约。

然后，我们调用“randomresult”getter 函数来查看 Chainlink oracle 使用给定种子生成的可验证随机数的结果。现在，我们已经成功地在智能合约中部署了一个随机数，该随机数是使用给定的种子可验证地创建的。

![An image showing the returned random number](img/2f921d0d32e83e5970244075902655c6.png)

<figcaption id="caption-attachment-1652" class="wp-caption-text">Viewing the returned random number</figcaption>



## 摘要

Poygon 的 PoS 链以其快速、廉价和可靠的交易提供了一个可行的第 2 层解决方案，加上 Chainlink VRF，开发人员现在可以利用可验证的随机数构建各种可扩展的 dApps。

如果你是一个聪明的合同开发者，想要利用 Chainlink VRF 特性，请访问 Chainlink [开发者文档](https://docs.chain.link/docs/chainlink-vrf)并加入关于[不和谐](https://discord.gg/hZMEXKmK)的技术讨论。

## 关于这个话题的更多信息

*   [链环 VRF:链上可验证的随机性](https://blog.chain.link/chainlink-vrf-on-chain-verifiable-randomness/)
*   [使用链环价格进给多边形](https://blog.chain.link/matic-defi-price-feeds/)
*   [使用 Chainlink Oracles 创建动态 NFT 的 16 种方法](https://blog.chain.link/create-dynamic-nfts-using-chainlink-oracles/)

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://www.chain.link/solutions/defi)