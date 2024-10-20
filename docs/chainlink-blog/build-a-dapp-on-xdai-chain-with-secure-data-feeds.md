# 使用安全数据馈送在 xDai 链上构建 dApp

> 原文：<https://blog.chain.link/build-a-dapp-on-xdai-chain-with-secure-data-feeds/>

[xDai chain](https://www.xdaichain.com/) 是一个基于以太坊的稳定侧链，使用美元支持的 stable coin xDai(DAI 令牌的一种表示)作为网络的原生币，为开发者提供快速、廉价、稳定的交易。

作为最广泛采用的分散式 oracle 网络，Chainlink 是 xDai 开发人员的[首选 oracle 解决方案](https://www.xdaichain.com/about-xdai/project-spotlights/chainlink)，它与 xDai Chain 进行了本机集成，以支持防篡改的外部数据馈送。

在这篇技术文章中，我们将向您展示如何使用 Chainlink [价格馈送](https://data.chain.link/)让您的 xDai Chain 智能合约访问高质量、防篡改的价格数据，从而提供广泛的市场覆盖，并保护您的 dApp 免受潜在的 [oracle 漏洞和 flash loan 资助的攻击](https://blog.chain.link/flash-loans-and-the-importance-of-tamper-proof-oracles/)。

## 对可伸缩和稳定事务的需求

今年，DeFi 协议出现了爆炸性增长，DeFi 协议锁定的总价值(TVL)从 1 月份的 160 亿美元飙升至现在的 400 多亿美元(T1)。然而，随着这种增长而来的是链上交易量的增加，这对于可能经历不可预测的高燃气费和缓慢交易时间的用户来说具有流动效应。

xDai Chain 之类的第 2 层网络已经出现，通过基于 xDai 令牌提供更高的可扩展性、更高的吞吐量和更稳定的交易来支持 [DeFi](https://chain.link/education/defi) 的增长。在 xDai 的令牌模型中，网络上广播交易的所有天然气费用都以 xDai 支付，为开发商创造了一个稳定且经济上可预测的区块链环境。此外，xDai Chain 是一个完全兼容 EVM 的以太坊侧链，这意味着那些熟悉使用 Solidity，MetaMask 和其他以太坊专用工具和语言的人可以轻松地与 xDai Chain 工作和交互，而不必学习新的语言或设置新的钱包来生成交易。

然而，像任何其他支持智能合约的区块链或第 2 层解决方案一样，迫切需要为智能合约提供对[高质量和可靠的外部数据](https://blog.chain.link/the-importance-of-data-quality-for-defi/)的访问，并使 dApps 能够对真实世界的事件做出反应，如资产价格的变化，以及向链外系统的输出。

[Chainlink 价格馈送](https://data.chain.link/)已经成为区块链数据馈送的标准，成为为需要外部价格数据的智能合同获取实际价值的最广泛使用的馈送。Chainlink oracle networks 的分散式架构和各种优质数据源可确保任何订阅源中的最新价格得到安全汇总，并反映广泛的市场覆盖面。

现在，我们已经了解了在 xDai Chain 上构建分散式应用程序的优势，以及 Chainlink 价格提要在提供高质量和安全的价格数据方面的重要作用，我们将通过一个示例来了解在 xDai 上构建 dApp 时如何使用 Chainlink 价格提要。

## 在 xDai 链上使用 Chainlink 价格馈送

在 xDai Chain 上使用 Chainlink Price Feeds 的第一步是设置你的 MetaMask 钱包[连接到 xDai Chain mainnet](https://www.xdaichain.com/for-developers/developer-resources#json-rpc-endpoints) 。主 RPC 是一个具有 4 个节点、健康检查和故障转移的负载平衡器，但是如果需要，还有[备用 RPC](https://www.xdaichain.com/for-developers/developer-resources#json-rpc-endpoints)也可以连接。

![How to connect to xDai chain. ](img/bf3be2041e80a031fb0b32f53217ee61.png)

<figcaption id="caption-attachment-1669" class="wp-caption-text">How to connect to xDai chain.</figcaption>



一旦你连接到 xDai 链，你就可以使用 [BlockScout 水龙头](https://blockscout.com/xdai/mainnet/faucet)获得少量免费 mainnet xDai。xDai 是 xDai 侧链的本机令牌，用作事务的 gas。如果水龙头是空的，你可以通过[坡道](https://ramp.network/buy/?swapAsset=XDAI)或 [MtPelerin](https://www.mtpelerin.com/buy-xdai#) 用菲亚特购买 xDAI，通过 [BitMax](https://bitmax.io/en/basic/cashtrade-spottrading/usdt/xdai) 上的 USDT/xDAI 对，或者你可以使用 [Dai 到 xDai 桥](https://www.xdaichain.com/for-users/bridges/converting-xdai-via-bridge)。

![How to obtain free mainnet xDai](img/cd85a8ba1b97aae4600c77661c113e3e.png)

<figcaption id="caption-attachment-1672" class="wp-caption-text">Obtaining free mainnet xDai</figcaption>



### 创建智能合同

在 xDai 上开始构建使用 Chainlink 价格提要的智能合约的最简单方法是从标准的[价格消费者](https://remix.ethereum.org/#version=soljson-v0.6.7+commit.b8d736ae.js&optimize=false&evmVersion=null&gist=0c5928a00094810d2ba01fd8d1083581)合约开始。这是一个基本的标准化合同，用于启动链接价格馈送请求。我们将在 Remix 中打开此合同，并修改它以适应我们的需要。出于本演示的目的，我们将使用 ETH/USD 价格源。第一步是在我们的构造函数中初始化一个 [xDai 价格馈送引用契约](https://docs.chain.link/docs/xdai-price-feeds)。 [ETH/USD](https://data.chain.link/xdai/mainnet/crypto-usd/eth-usd) 价馈参考合约部署在地址 0xa 767 f 745331d 267 c 7751297d 982 b 050 c 93985627*。*

```
priceFeed = AggregatorV3Interface(0xa767f745331D267c7751297D982b050c93985627);
```

接下来，我们需要定义一个函数，从上面的构造函数中实例化的价格提要聚合器契约中获取最新价格。为此，我们定义了一个新函数，它从聚合器契约中调用 [latestRoundData](https://docs.chain.link/docs/price-feeds-api-reference#latestrounddata) 函数。这个函数返回聚合器契约的当前状态，在本例中，我们获取当前价格并将其返回到消费函数中。

```
function getLatestPrice() public view returns (int) {
        (
            uint80 roundID, 
            int price,
            uint startedAt,
            uint timeStamp,
            uint80 answeredInRound
        ) = priceFeed.latestRoundData();
        return price;
    }
```

### 部署和测试智能合约

现在我们已经准备好部署和测试我们的契约了。在 Remix 中编译合同，然后在 deployment 选项卡上，将环境更改为“Injected Web3”，并确保下面的 wallet 地址是包含 xDai 令牌的 MetaMask wallet 中的地址，按 deploy 按钮，然后按照步骤操作。最终结果是您将智能合约部署到了 xDai Chain mainnet。您应该通过 Remix 控制台中的事务输出注意到部署的契约地址。

部署完成后，我们只需执行 getLatestPrice 函数。结果应该是该函数从 ETH/USD 聚合器合同返回最新价格，然后可以在 xDai 链上的分散式应用程序中使用该价格。

![Viewing the ETH/USD Price Feed result](img/cb6251db38e00a7134d83a84edf62ac1.png)

<figcaption id="caption-attachment-1673" class="wp-caption-text">ETH/USD Price Feed result</figcaption>



## 摘要

xDai Chain 以其快速、廉价和稳定的交易，为要构建的分散应用程序提供了稳定和经济上可预测的第 2 层选项。Chainlink Price Feeds 进一步增强了这一价值主张，它与 sidechain 进行了本机集成，使 xDai smart contracts 能够访问高质量的聚合价格数据，这些数据可用于[各种应用](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/#decentralized-finance)。

如果您是一名开发人员，并希望快速将您的应用程序连接到 Chainlink 价格参考数据，请访问[开发人员文档](https://docs.chain.link/)，并参加 [Discord](https://discordapp.com/invite/aSK4zew) 中的技术讨论。如果您想安排一次电话会议来更深入地讨论 xDai/Chainlink 集成，请点击此处的。

### 关于这个话题的更多信息

*   [Protofire 因与 xDai 整合而获得 Chainlink 社区资助](https://blog.chain.link/protofire-receives-a-chainlink-community-grant-for-an-integration-with-xdai/)
*   [chain link 价格馈送中的 3 级数据聚合](https://blog.chain.link/levels-of-data-aggregation-in-chainlink-price-feeds/)