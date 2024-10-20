# 链上数据目录简介:Data.eth

> 原文：<https://blog.chain.link/introducing-the-chainlink-on-chain-data-directory/>

Chainlink 的[价格参考数据源](https://chain.link/solutions/defi)是 DeFi 生态系统中使用最广泛的分散式 oracle 网络，提供加密货币、稳定货币、商品、外汇、指数等金融市场数据的防篡改和高度可靠的来源。随着 Chainlink Price Feeds 现在为领先的 [DeFi](https://chain.link/education/defi) 应用程序(如 Aave 和 Synthetix)获得数十亿用户存款，我们不断努力为我们的用户构建更多的安全功能，以便 DeFi 生态系统可以继续扩展以获得更多价值。

鉴于我们以安全为中心的方法，**我们很自豪地宣布使用 ENS 推出 Chainlink 链上数据目录，该目录创建了一个易于识别的 Chainlink 价格馈送地址链上索引，为用户提供了额外的保证，即他们依赖和/或发送资金到正确的链上地址。**以太坊域名服务(ENS)是一种分散式协议，用于创建人类可读的[域名](https://blog.chain.link/how-to-create-nft-domain-names/)，这些域名指向特定的链上地址或合同。因为 ENS 在链上存储所有元数据，只要以太坊网络继续运行，用户就能够以直接和分散的方式发现他们的合同并将其连接到 Chainlink 价格馈送。

Chainlink 链上数据目录的主要优势包括:

*   每个链上链接价格馈送的人类可读域名
*   使用链上数据的链接价格馈送的抗审查可发现性
*   通过链上 ENS 事件无缝跟踪价格反馈升级
*   整个链式生态系统的进一步分散化
*   一个开放标准，任何开发人员或项目都可以采用它作为自己的协议

目前，在我们的 [feeds 页面](https://data.chain.link/)和[开发者文档](https://docs.chain.link/docs/ethereum-addresses)上都可以找到 Chainlink 价格 Feeds。通过 Chainlink On-Chain 数据目录，除了我们当前的资源之外，我们正在增加人们如何访问 Chainlink 价格源的分散化。链上数据目录也使各种[智能合同](https://chain.link/education/smart-contracts)更容易安全地消费各种链链接价格馈送，因为所有域名都清楚地说明了与特定馈送相关的人类可读名称。这是第一次创建 oracle 网络的防篡改链上目录，我们相信这将改善开发人员和用户发现和跟踪链接价格变化的体验。

## Chainlink 链上数据目录如何工作

利用 ENS 协议，Chainlink 将使用 [data.eth](https://etherscan.io/enslookup-search?search=data.eth) 域名为以太坊区块链直播的每个 Chainlink 支持的价格馈送提供人类可读的子域名。每个价格源的域名可以通过简单地将价格源的名称附加到域名的前面来轻松访问，例如 [eth-usd.data.eth](https://etherscan.io/enslookup-search?search=eth-usd.data.eth) 。其他域名包括:

*   [btc-usd.data.eth](https://etherscan.io/enslookup-search?search=btc-usd.data.eth)
*   [link-usd.data.eth](https://etherscan.io/enslookup-search?search=link-usd.data.eth)
*   [xau-usd.data.eth](https://etherscan.io/enslookup-search?search=xau-usd.data.eth)
*   [澳元-美元数据. eth](https://etherscan.io/enslookup-search?search=aud-usd.data.eth)
*   [sdefi-usd.data.eth](https://etherscan.io/enslookup-search?search=sdefi-usd.data.eth)
*   [uni-usd.data.eth](https://etherscan.io/enslookup-search?search=uni-usd.data.eth)
*   [bnb-usd.data.eth](https://etherscan.io/enslookup-search?search=bnb-usd.data.eth)
*   [aave-usd.data.eth](https://etherscan.io/enslookup-search?search=aave-usd.data.eth)
*   [yfi-usd.data.eth](https://etherscan.io/enslookup-search?search=yfi-usd.data.eth)
*   [英镑-美元.数据. eth](https://etherscan.io/enslookup-search?search=gbp-usd.data.eth)
*   [dai-eth.data.eth](https://etherscan.io/enslookup-search?search=dai-eth.data.eth)
*   [link-eth.data.eth](https://etherscan.io/enslookup-search?search=link-eth.data.eth)
*   [tusd-eth.data.eth](https://etherscan.io/enslookup-search?search=tusd-eth.data.eth)
*   [snx-eth.data.eth](https://etherscan.io/enslookup-search?search=snx-eth.data.eth)
*   [fast-gas-gwei.data.eth](https://etherscan.io/enslookup-search?search=fast-gas-gwei.data.eth)
*   [bnt-eth.data.eth](https://etherscan.io/enslookup-search?search=bnt-eth.data.eth)
*   [eth-xdr.data.eth](https://etherscan.io/enslookup-search?search=eth-xdr.data.eth)
*   [dmg-eth.data.eth](https://etherscan.io/enslookup-search?search=dmg-eth.data.eth)
*   [uma-eth.data.eth](https://etherscan.io/enslookup-search?search=uma-eth.data.eth)
*   [tusd-reserves.data.eth](https://etherscan.io/enslookup-search?search=tusd-reserves.data.eth)
*   [tusd-supply.data.eth](https://etherscan.io/enslookup-search?search=tusd-supply.data.eth)
*   更多的

data.eth 子域名的使用确保了即使 [Chainlink feeds 页面](https://feeds.chain.link/)和文档遇到不可预见的问题，用户仍然可以访问他们的智能合同应用程序所需的价格源。为了利用这些域名，用户可以在 [ens.domains](https://app.ens.domains/) 网站上执行简单的搜索，使用像 [Etherscan](http://etherscan.io/) 这样的可信块浏览器，或者使用他们自己的以太坊完整节点，仅使用链上数据来按需查询提要的当前地址。此外，开发人员可以利用这些域来跟踪 Chainlink 价格源的升级，因为 ENS 域的每次更改都会生成一个标准化的链上事件，开发人员可以轻松找到，从而消除了手动搜索更改的需要。

![eth-usd.data.eth on ens.domains](img/b6690832d1481fe907eb66e67c548edf.png)

<figcaption id="caption-attachment-405" class="wp-caption-text">Results of a search for the eth-usd.data.eth on ens.domains, which resolves to the ETH/USD Price Feed contract.</figcaption>



智能合同还可以利用 data.eth 子域来确保升级得到无缝支持，而无需开发人员进行任何集成工作。data.eth 域名及其子域名通过分布式多签名合同进行管理，随着时间的推移，通过增加其他关键生态系统利益相关方，该合同将继续分散管理，从而进一步确保 data.eth 子域名的完整性。在 ENS 的支持下，我们将继续尽可能无缝地让用户以分散的端到端方式发现和连接 Chainlink 价格源。

通过整合 ENS 域名，我们希望将链上域名的使用标准化，以跟踪关键任务智能合同，如价格参考数据馈送。这确保了最终用户和开发人员在合同更新方面的完全透明性，在构建智能合同应用程序时易于识别的地址，以及新的和现有的价格馈送的抗审查发现性。关于链上数据目录的更多信息可以在我们的[文档页面](https://docs.chain.link/docs/ens#config)中找到。

如果你是一名开发人员，想要将 Chainlink 价格馈送集成到你的智能合同应用程序中，请查看[开发人员文档](https://docs.chain.link/)或[点击这里](https://chainlink.typeform.com/to/gEwrPO)。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[|](https://www.reddit.com/r/Chainlink/)[不和](https://discordapp.com/invite/aSK4zew)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://defi.chain.link/)