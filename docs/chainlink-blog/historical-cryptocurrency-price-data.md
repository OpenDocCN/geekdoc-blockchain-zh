# 如何使用 Chainlink 价格源获取历史加密货币价格数据

> 原文：<https://blog.chain.link/historical-cryptocurrency-price-data/>

将历史加密货币价格数据提取到智能合约中是 Web3 应用的常见要求，许多协议依赖高质量的最新价格数据来运行和保护 DeFi 应用。除此之外，历史加密价格数据也是智能合同开发人员有时提出的一项要求，一些协议除了最新价格之外，还需要准确、高质量的历史价格数据。

在这篇技术文章中，我们将向您展示一个 [工作解决方案](https://github.com/pappas999/historical-price-feed-data) 如何从 Chainlink [价格源](https://data.chain.link/) 获取历史价格数据，并在链上验证结果。

## 需要准确的历史加密价格数据

在过去的几年里，DeFi 出现了爆炸性的增长。DeFi 协议的一个常见要求是高度安全、准确和可靠的价格数据。[chain link Price Feeds](https://data.chain.link/)已经成为 DeFi 生态系统中使用最广泛的价格先知，已经为领先和新兴的协议如[Aave](https://aave.com/)[Synthetix](https://synthetix.io/)和[Trader Joe](https://traderjoexyz.com/)获得了数百亿美元的价值。

价格馈送最常见的用例是消费给定资产对的最新价格数据。然而，有时 DeFi 协议或 dApp 要求在某个时间点查找给定资产的历史价格。这种用例的一个例子是一个金融产品，它需要比较各个时间段的价格，如 [加密货币保险](https://insureteam.medium.com/insure-defi-integrates-chainlinks-historical-price-data-oracles-to-power-its-decentralized-crypto-fb6ef97af75b) ，它需要历史数据来计算市场波动并动态调整保费。

历史价格数据已经可以通过众多市场 API 轻松获得，然后使用 chain link[Any API](https://docs.chain.link/docs/request-and-receive-data/)功能在链上消费。但是，这种解决方案存在一些安全问题—数据源和交付数据的 oracle 可能是集中式的，无法验证数据是否准确。与实时价格数据一样，历史价格数据也应该是分散的，并具有足够的市场覆盖范围，以反映当时全市场的价格发现。这不需要使用单一的数据源、交换或 API。

Chainlink 价格馈送通过提供来自优质数据提供商的分散、高质量的价格数据，使用数量加权平均价格进行汇总，缓解了这些问题。当具体查看历史价格数据时，价格馈送有助于让用户相信所报告的价格是准确的，并且反映了当时整个市场的价格，而不仅仅是单个交易所的价格。

已经有解决方案可以用来获取历史的 Chainlink 价格 Feed 数据，比如 [Reputation.link 的 API](https://docs.chain.link/docs/request-and-receive-data/) 或者图 上的一个 [子图。虽然这些是有效的解决方案，但它们仍然依赖于可用的 API 或正确的外链索引数据。](https://thegraph.com/explorer/subgraph?id=0x9d196973c0c5bd65ccfb797a2c23eb5c1faba7ab-0&view=Overview)

在本解决方案中，我们将展示如何使用 Chainlink oracle 从 Chainlink 价格馈送中获取历史价格数据，以执行所需的链外计算，作为消费智能合约的输入，从而以信任最小化的方式获取链上历史价格数据。

## 价格进料合同概述

从消费契约的角度来看，Chainlink Price Feeds 智能契约一般可以分为两类——[代理契约](https://docs.chain.link/docs/architecture-decentralized-model/#proxy) 和 [聚合器契约](https://docs.chain.link/docs/architecture-decentralized-model/#aggregators) 。

代理合约代表一个特定的价格对(如 ETH/USD)，是用户与之交互的合约。该契约包含各种外部面向函数，以基于某些参数获得回合数据，例如根据价格对获得最新回合细节，或者在特定回合获得答案。

这些代理契约还存储对特定代理契约的所有底层聚合器契约的引用，以及当前聚合器契约是哪一个。这个信息可以通过`aggregator`和`phaseAggregators` getter 函数获得，传递一个阶段 ID。在下面的示例中，我们可以看到[Kovan ETH/USD](https://kovan.etherscan.io/address/0x9326BFA02ADD2366b30bacB125260Af641031331#readContract)代理契约的第二个聚合器契约(阶段 ID = 2)是当前契约。

![Screenshot of the Kovan ETH/USD Proxy contract](img/36b0ab94425f737623e8fbb3e3f4fb3c.png)

<figcaption id="caption-attachment-4337" class="wp-caption-text">Obtaining the second aggregator in the [Kovan ETH/USD](https://kovan.etherscan.io/address/0x9326BFA02ADD2366b30bacB125260Af641031331) proxy contract.</figcaption>



![Screenshot of obtaining the current aggregator in the Kovan ETH/USD Proxy contract.](img/9879b0e94b84921270f330280d6ad265.png)

<figcaption id="caption-attachment-4338" class="wp-caption-text">Obtaining the current aggregator in the Kovan ETH/USD proxy contract.</figcaption>



底层聚合器契约的实现略有不同，这取决于它们的版本(FluxAggregator、legacy Aggregator 等)。)，但它们都存储聚合的舍入数据，并为 oracles 提供提交答案的函数。

![Diagram of Chainlink Price Feeds' contracts overview](img/d05b6e28ba81183f3be1ab90cfb259d9.png)

<figcaption id="caption-attachment-4339" class="wp-caption-text">Chainlink Price Feeds contracts overview.</figcaption>



## 解决方案概述

Chainlink Price Feeds 价格数据存储在链上，开发人员可以执行`getLatestRoundData`函数来获取价格对的最新价格数据。然而，从价格提要中获取历史价格数据并不简单，而且有些复杂。

Chainlink 价格馈送将价格数据存储在聚合回合中，这些回合通过其唯一的回合 ID 来标识。当价格偏离大于价格对指定的 [偏离阈值](https://docs.chain.link/docs/architecture-decentralized-model/#deviation-threshold) 时，或者当 [心跳阈值](https://docs.chain.link/docs/architecture-decentralized-model/#deviation-threshold) 到期时，发起新一轮。如果开发人员知道正确的 round ID，他们可以轻松地运行[getHistoricalPrice](https://docs.chain.link/docs/historical-price-data/)函数来查找历史价格，但是，round ID 和时间戳、块或任何其他可用于确定时间点的东西之间没有直接的关联。

此外，还有多个不同版本的 Chainlink Price Feed aggregator 合同，如[flux aggregator](https://github.com/smartcontractkit/chainlink/blob/develop/contracts/src/v0.6/FluxAggregator.sol)和 Off-Chain Reporting[Off Chain aggregator](https://github.com/smartcontractkit/libocr/blob/1f3b15df1ec9e458fd200398e52a640a60cc38ed/contract/OffchainAggregator.sol)合同。一个价格源可能已经使用 FluxAggregator 合同一段时间，然后更新为 OCR 兼容的 OffchainAggregator 合同。这意味着，根据消费合同希望从哪个时间点获取历史价格数据，解决方案需要能够查看多个不同的聚合器合同。

除此之外，面向外部的代理契约和底层聚合器契约之间的回合 id 被有意地分阶段，代理契约回合总是比聚合器回合 id 大得多。这是因为面向外部的轮 ID 总是需要一个递增的数字，而当部署新的聚合器契约时，底层聚合器轮 ID 可能会再次从 1 开始。给定内部聚合器回合 ID 的外部代理契约的回合 ID 可以通过以下计算来确定性地确定，其中阶段是所部署的聚合器契约(第一、第二、第三等等。)相对于代理协定，originalRoundId 是基础聚合器协定的回合。您可以通过针对代理契约调用`phaseAggregators` getter 方法来确定阶段。

```
external proxy round ID = uint80(uint256(phase) << 64 | originalRoundId);
```

最后，并非所有回合都可以假定有价格数据。由于超时或当时特定于环境的问题，一些回合(主要在测试网上)的价格和时间戳字段可能为零值。

由于这些复杂性，很明显，如果没有效率低下的解决方案，就不容易获得准确且可验证的纯链历史价格数据，例如对轮次数据进行大量迭代，或者通过读取和存储轮次和链上时间戳的映射，这将变得非常昂贵。

除了让智能合约访问离线数据和事件，Chainlink 分散式 oracle 网络还为执行离线计算提供了一个通用框架。这意味着，需要历史价格数据的链上智能合约可以利用运行自定义外部适配器的 oracle 来确定在指定日期给定价格对的正确回合 ID，而不是存储链上的大量数据或进行未知回合数的迭代。然后，oracle 可以将该回合 ID 返回到链上，并且消费合同可以使用该信息，通过使用现有的 [历史价格数据 API](https://docs.chain.link/docs/historical-price-data/) ，将时间戳与返回的回合和搜索参数时间戳进行比较，来立即验证链上的历史价格数据。

这个解决方案符合这样的概念，即先知 [负责区块链不负责](https://blog.chain.link/how-the-chainlink-network-goes-beyond-data-delivery/) 的任何事情，以及区块链由于能力限制或效率考虑而不能或不应该做的任何事情。除此之外，以这种方式获得历史价格数据还有多个额外的好处:

*   没有链上存储大量数据，也没有链上循环数据的繁重迭代
*   使用现有的历史价格函数在链上验证离线计算的结果，降低恶意 oracle 提供不正确数据的风险
*   外部适配器以无状态的方式运行，从不存储数据，并提供一种通用的方法来获取任何节点运营商都可以在其 Chainlink 节点上运行的历史价格数据
*   外部适配器纯粹处理链上数据，不依赖外部 API 或其他系统来提供解决方案

![Diagram of using External Adapters with on-chain smart contracts](img/e64a08ce96ce7709eaad84b13fd7d3de.png)

<figcaption id="caption-attachment-4340" class="wp-caption-text">Using External Adapters with on-chain smart contracts.</figcaption>



## 如何使用 Chainlink Oracle 获取历史加密货币价格数据

### 创建历史价格数据请求

要发起对历史价格数据的请求，消费契约只需向 oracle 提交一个 [API 请求](https://docs.chain.link/docs/request-and-receive-data/) ，Oracle 在作业规范中运行自定义历史价格 [外部适配器](https://github.com/pappas999/historical-price-feed-data) ，传入一个 [有效代理契约地址](https://docs.chain.link/docs/reference-contracts/') ，以及要返回价格数据的时间戳(在 Unix 时间中)。

```
 function getHistoricalPrice(address _proxyAddress, uint _unixTime) public returns (bytes32
requestId)
    {

        Chainlink.Request memory request = buildChainlinkRequest(jobId, address(this), 
this.singleResponseFulfill.selector);

        // Set the URL to perform the GET request on
        request.add("proxyAddress", addressToString(_proxyAddress));
        request.add("unixDateTime", uint2str(_unixTime));

        //set the timestamp being searched, we will use it for verification after
        searchTimestamp = _unixTime;

        //reset any previous values
        answerRound = 0;
        previousRound = 0;
        nextRound = 0;
        nextPrice = 0;
        nextPriceTimestamp = 0;
        previousPrice = 0;
        previousPriceTimestamp = 0;
        priceAnswer = 0;
        priceTimestamp = 0;

        // Sends the request
        return sendChainlinkRequestTo(oracle, request, fee);
    }
```

## 历史价格外部适配器

一旦 Chainlink 节点接收到该请求，它就将输入数据发送到历史价格外部适配器，该适配器将找出包含被搜索时间戳答案的正确回合 ID，以及随后的回合 ID。这两个额外的 round ID 是验证所必需的，因此我们可以验证返回的 round ID 答案是否最接近正在搜索的时间戳，其中 round 的 updatedAt 时间戳小于 search timestamp 参数。

一旦外部适配器接收到代理契约地址和搜索时间戳参数，它就执行以下计算:

*   对传入的地址和时间戳进行一些验证
*   确定在指定的时间戳哪个基础聚合器契约将包含该轮
*   对于生成的聚合器契约，获取聚合器中存储的所有轮 id 的列表(使用[eth _ get logs](https://docs.alchemy.com/alchemy/guides/eth_getlogs))
*   使用返回的回合 ID 列表，对列表执行 [【二分搜索法】](https://en.wikipedia.org/wiki/Binary_search_algorithm) 操作，以找到正在搜索的时间戳的正确回合 ID。与效率较低的 [线性搜索](https://en.wikipedia.org/wiki/Linear_search) 相比，这种方法的时间效率为**【O(N)**
*   如果发现任何轮次含有空数据或无效数据(由于超时等原因)，该算法将确定存在多少轮次空数据或无效数据，在该轮次被二分搜索法检查后，它将剔除所有无效轮次，并在新的轮次列表上开始新的二分搜索法
*   当找到结果轮 ID 时，外部适配器将使用该轮 ID 以及聚合器契约中的上一轮和下一轮 ID，计算三个值中每个值的分阶段代理契约轮 ID，然后在元素`roundAnswer`、`earlierRoundAnswer`和`laterRoundAnswer`、下的适配器输出中返回它们
*   处理历史价格数据请求的 oracle 将获取这三个结果，并使用 Chainlink 的 [多变量响应](https://docs.chain.link/docs/multi-variable-responses/) 特性将它们链上返回给消费合同

```
{
    "jobRunID": "534ea675a9524e8e834585b00368b178",
    "data": {
        "roundAnswer": "36893488147419111519",
        "earlierRoundAnswer": "36893488147419111518",
        "laterRoundAnswer": "36893488147419111520"
    },
    "result": null,
    "statusCode": 200
}
```

## 在链上验证结果

对历史价格数据使用集中式数据源或 oracle 会给智能合约带来潜在的安全漏洞。然而，在这种情况下，对于来自 oracle 的报告的回合 ID，我们可以利用现有的历史价格数据函数来验证链上的回合 ID，从而创建用于获取历史价格数据的信任最小化验证方法，因为数据仍然是从链上的价格馈送合同中获取的，而 oracle 仅计算并返回未知的回合 ID。

我们可以验证返回的回合信息，然后使用它通过以下验证获得最终的历史价格:

首先，我们验证所有三个返回回合(answerRound、previousRound、nextRound)都包含有效的返回回合数据

```
//verify the responses
        //first get back the responses for each round
        (
            uint80 id,
            int price,
            uint startedAt,
            uint timeStamp,
            uint80 answeredInRound
        ) = priceFeed.getRoundData(_answerRound);
        require(timeStamp > 0, "Round not complete");
        priceAnswer = price;
        priceTimestamp = timeStamp;

        (
            id,
            price,
            startedAt,
            timeStamp,
            answeredInRound
        ) = priceFeed.getRoundData(_previousRound);
        require(timeStamp > 0, "Round not complete");
        previousPrice = price;
        previousPriceTimestamp = timeStamp;

        (
            id,
            price,
            startedAt,
            timeStamp,
            answeredInRound
        ) = priceFeed.getRoundData(_previousRound);
        require(timeStamp > 0, "Round not complete");
        nextPrice = price;
        nextPriceTimestamp = timeStamp;
```

接下来，我们对轮次和每个轮次的时间戳进行一些验证。

*   确保回合顺序正确
*   确保三轮的时间戳都按照正确的时间顺序排列
*   如果循环数中有任何间隔(即 previousRound = 1625097600 和 answerRound = 1625097605)，确保返回的循环 id 之间没有任何循环 id 的有效循环数据。因此，对于这个 previousRound = 1625097600 和 answerRound = 1625097605 的示例，协定将确保回合 1625097601、1625097602、1625097603 和 1625097604 不返回有效的回合数据

```
​​//first, make sure order of rounds is correct
        require(previousPriceTimestamp < timeStamp, "Previous price timetamp must be < answer
timestamp");
        require(timeStamp < nextPriceTimestamp, "Answer timetamp must be < next round
timestamp");

        //next, make sure prev round is before timestamp that was searched, and next round is
after
        require(previousPriceTimestamp < searchTimestamp, "Previous price timetamp must be < 
search timestamp");
        require(searchTimestamp < nextPriceTimestamp, "Search timetamp must be < next round 
timestamp");
require(priceTimestamp <= searchTimestamp, "Answer timetamp must be less than or equal to 
searchTimestamp timestamp");

        //check if gaps in round numbers, and if so, ensure there's no valid data in between
        if (answerRound - previousRound > 1) {
            for (uint80 i= previousRound; i<answerRound; i++) {
                (uint80 id,
                int price,
                uint startedAt,
                uint timeStamp,
                uint80 answeredInRound
                ) = priceFeed.getRoundData(i);
                require(timeStamp == 0, "Missing Round Data");
            }
        }

        if (nextRound - answerRound > 1) {
            for (uint80 i= answerRound; i<nextRound; i++) {
                (uint80 id,
                int price,
                uint startedAt,
                uint timeStamp,
                uint80 answeredInRound
                ) = priceFeed.getRoundData(i);
                require(timeStamp == 0, "Missing Round Data");
            }
        }
```

如果上述所有检查都成功通过，则返回回合(answerRound)的价格答案是指定时间戳的价格对的验证价格。

## 总结

Chainlink 价格馈送提供了一种将高质量价格数据导入 Solidity 智能合同的可靠方式。除此之外，Chainlink 的 oracle 框架提供了执行链外计算的能力，允许开发人员以高度安全、信任最小化和可验证的方式访问历史价格数据。

如果您是一名开发人员，并且希望将您的智能合约连接到底层区块链之外的现有数据和基础设施，请在此处联系[](https://chainlink.typeform.com/to/gEwrPO)或访问 [开发人员文档](https://docs.chain.link/)t[ation](https://docs.chain.link/)。

### **关于这个话题的更多信息**

*   [如何获取 Solidity 中以太坊、比特币等加密货币的当前价格](https://blog.chain.link/fetch-current-crypto-price-data-solidity/)
*   [DeFi 的数据质量](https://blog.chain.link/the-importance-of-data-quality-for-defi/) [了解如何获取 Solidity 中资产的当前价格](https://blog.chain.link/fetch-current-crypto-price-data-solidity/) [智能合约](https://blog.chain.link/the-importance-of-data-quality-for-defi/)