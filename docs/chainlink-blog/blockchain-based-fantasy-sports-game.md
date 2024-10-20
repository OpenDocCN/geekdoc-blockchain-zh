# 使用 Chainlink 外部适配器构建基于区块链的幻想体育游戏

> 原文：<https://blog.chain.link/blockchain-based-fantasy-sports-game/>

在 2021 年 ETHDenver 黑客马拉松上，Chainlink 奖金获得者 [Pr！ce](https://devfolio.co/submissions/stonks-9f8d) 使用一个 [Chainlink 外部适配器](https://docs.chain.link/docs/external-adapters)将非链式 NBA 球员表现数据连接到一个 Chainlink oracle，为一个总部位于区块链的奇幻体育游戏提供动力。这种市场模式也可以应用于其他零和性能资产，并很好地展示了如何使用 Chainlink 的可配置和安全的 oracle 基础设施将独特的链外 API 和自定义数据集连接到[智能合约](https://chain.link/education/smart-contracts)，实现体育、游戏、 [DeFi](https://chain.link/education/defi) 等领域的竞争性应用。

在这个帖子里，公关！ce 团队成员 Anweshi Anavadya、Ishan Ghimire、Sam Orend 和 Jasraj 贝迪解释了他们如何使用 Chainlink 准确计算并在链上提供 NBA 球员元数据，以半可替换的 ERC-1155 令牌的形式创建“份额”。他们还演示了他们的 dApp 如何调用 [Chainlink ETH-USD 价格馈送](https://data.chain.link/eth-usd)来安全地向游戏玩家分发奖品。

* * *

*由* [*山姆*](https://www.linkedin.com/in/sam-orend/) *，* [*伊山*](https://www.linkedin.com/in/ishan-ghimire/) *，* [*安韦士*](https://www.linkedin.com/in/anweshianavadya/) *，以及* [*贾斯拉*](https://twitter.com/ret2jazzy)

遇见 Pr！ce 是一个季节性的区块链市场，用户可以买卖 NBA 球员的股票，甚至可以根据他们的表现获得分红。这篇文章将解释如何公关！ce 从技术角度工作，以及我们的团队如何使用 Chainlink 外部适配器和 price[Oracle](https://chain.link/education/blockchain-oracles)为我们的链上市场安全地获取外部数据。



![The Pr!ce dApp demo launch screen.](img/a2febacd5661f34875956b151c0491e7.png)

<figcaption class="wp-caption-text">公关！ce dApp 演示启动屏幕。</figcaption>



<figcaption></figcaption>



## 季节性市场是如何运作的？

NBA 赛季开始，公关！首席执行官发行 NBA 球员的"股份"。这些股票是什么样的？我们建立了公关！所以我们的股票是 ERC-1155(半可替代)代币。每个令牌都包含将其与特定玩家联系起来的元数据。然后，我们通过 web3.js 提取元数据，并用 React 组件创建元数据的可视化。



![Pr!ce dApp interface featuring NBA players represented as ERC-1155 tokens.](img/3723ece38d456995bf4eafe3f26d7244.png)

<figcaption class="wp-caption-text">公关！ce ERC-1155 用 NBA 球员元数据建造的半可替换代币。</figcaption>



<figcaption></figcaption>



NBA 赛季开始，公关！ce 为每个 NBA 球员铸造了 100 枚 ERC-1155 代币。这些令牌的元数据使用 Chainlink 获取，chain link 调用我们开发的离线 API 来管理不需要在链上的联盟数据，因为它在赛季期间保持不变，但随赛季而变化。在第一周，用户可以使用包装的 ERC-20 代币对他们希望购买其股份的球员进行投标。第一周过后，ERC-1155 代币被转移到每个用户的钱包里，赛季开始了。



![Pr!ce user interface purchasing shares of Kevin Durant using MetaMask browser wallet on the Ethereum network.](img/b2c121a1c4aef4f34f2b286a41c2e081.png)

<figcaption class="wp-caption-text">一个公关！ce 用户购买本季度凯文·杜兰特的股票。</figcaption>



<figcaption></figcaption>



在赛季中，用户可以以市场价格购买/出售任何球员的额外股份。给定玩家的市场价格由我们的 [AMM(自动做市商)](https://blog.chain.link/challenges-in-defi-how-to-bring-more-capital-and-less-risk-to-automated-market-maker-dexs/)决定。与 Uniswap 类似，AMM 根据流动性池确定一只股票的市场价格。



![Pr!ce user interface showing NBA player tokens owned and player metadata.](img/c10a5db90ba5d951e5b9f3795d6ca62d.png)

<figcaption class="wp-caption-text">公关！ce 平台股东门户 UI 显示该季度拥有的股份。</figcaption>



<figcaption></figcaption>



最后，根据用户所持资产的表现，他们可能有资格获得股息。在我们的系统中，绩效被定义为可量化的产出。这对于每种资产类型都是不同的——对于 NBA，我们使用了球员的统计表现。分红是做公关的东西！独一无二。我们使用 Chainlink 价格馈送来计算季末的红利分配。

## 离线计算红利

很像金融市场，公关！ce 奖励你持有顶级 NBA 球员的股份。我们通过向股东支付一部分佣金作为红利来做到这一点。红利支付基于用户持有的运动员的梦幻运动成绩。

为了首先收集球员的表现数据，我们构建了一个定制的 web 抓取 API，使用 Flask 来获取 basketballmonster.com 前 50 名 NBA 梦幻球员的梦幻体育数据。然而，计算我们红利的价值比*只是*获取数据更复杂。它需要一个统计计算，包括用户拥有的股票数量、流通中的股票总数、我们的分红基金的价值以及玩家的幻想产量。

我们在发展公关的时候！ce，我们遇到了一个关于如何经济有效地计算股息的问题。如果我们在链上进行股息计算，用于处理股息支付的汽油费将是巨大的，并且我们将自己置于汽油费的风险中，根据网络拥塞情况，汽油费的成本可能超过实际支付的价值。

出于这个原因，我们决定利用 Chainlink 来获取我们需要的链外数据，并在将数据带到链上之前计算我们的股息支付值。这使得我们能够保持较低的汽油费，并给予用户更多的支出。[我们是这样做的](https://gist.github.com/beshup/19ab2115c47a3e5de8f3a34115a8146c)。

```
function giveDividendPerPlayer(string memory request_uri) public hasSeasonStarted {
    require(lastDividendWithdrawn[msg.sender] < currWeekStart);

    lastDividendWithdrawn[msg.sender] = block.timestamp;
    requestDividendWorthyEntities(request_uri);
}
```

当用户在我们的应用程序前端点击“收集红利”时，我们在我们的 Solidity 智能契约中运行这个方法来开始这个过程。我们首先要求用户本周还没有提取该玩家的红利。然后，我们记录用户今天在当前 block.timestamp 提取了他们的红利，然后调用我们的函数来查看他们的资产是否有资格获得红利。

```
function requestDividendWorthyEntities(string memory request_uri) public onlyOwner {
    Chainlink.Request memory request = buildChainlinkRequest(nba_JOBID, address(this), this.fulfill.selector);
    // Set the URL to perform the request on
    request.add("get", request_uri);
    request.add("path", "to_send");

    bytes32 reqID = sendChainlinkRequestTo(nba_ORACLE, request, fee);
    jobIdMapping[reqID] = msg.sender;
}

function fulfill(bytes32 reqID, uint256 payout) public recordChainlinkFulfillment(reqID)
{
    require(jobIdMapping[reqID] != address(0x0));
    payable(jobIdMapping[reqID]).transfer(payout);
    jobIdMapping[reqID] = address(0x0);
    //payout to jobIdMapping[randomID]
}
```



<figcaption></figcaption>



[在这个函数](https://gist.github.com/beshup/9060296662a21449cd0e60569efd0fac)中，我们构建了我们的 Chainlink 请求，它将决定我们支付给用户的红利的价值。单个参数`request_uri`是在别处构造的，它包含计算查询参数中的被除数所需的数据，这将在后面看到。值得注意的是以下几行:

我们向 Chainlink 请求添加了一个`"get"`请求。这将决定我们股息支付的价值。

`request.add("get", request_uri);`

我们还将`"path"`添加到我们的请求中，它指定了我们想要的数据`to_send`。我们的端点返回我们将发送给`to_send`用户的支付值。添加这个作为`path`有助于我们将想要的数据转换成我们返回给用户的内容。

`request.add("path", "to_send");`

我们存储了从请求 id 到请求红利支付的用户地址的映射。当 fulfill 运行时，我们将计算出的支出转移给消息发送者(请求红利的用户)。

我们将刚刚构建的 Chainlink 请求发送到 Flask API 中的这个端点。让我们把这个分解一下，因为这是我们省油费的地方！

```
@app.route('/to_send_per_entity/<int:entity_id>/<int:shares_owned>/<int:shares_in_circulation>/<int:dividend_fund>', methods=['GET'])
@cross_origin()
def to_send(entity_id, shares_owned, shares_in_circulation, dividend_fund):
    if entity_id > LEAGUE_SIZE:
        entity_id -= LEAGUE_SIZE   

    league = league_data()
    entity_held_score = float(league[entity_id - 1]['fantasy_points'])

    sum_scores = 0.0 
    for entity in league:
        sum_scores += float(entity["fantasy_points"])

    res = (shares_owned/shares_in_circulation)*(entity_held_score / sum_scores)*dividend_fund

    return {"to_send": int(res)}
```



<figcaption></figcaption>



[简而言之，这个端点](https://gist.github.com/beshup/cf68ca20dd3de7b3989263b24a40e953)正在计算支付给用户的 ETH `“to_send”`的金额作为红利。这种支付计算首先包括合计每个 NBA 球员在一周内获得的累积幻想点数。

`for entity in league: sum_scores += float(entity["fantasy_points"])`

然后，我们根据累积的幻想点数、拥有的股份、流通中的总股份和红利基金的价值来计算最终的派息。

`res=(shares_owned/shares_in_circulation)*(entity_held_score/ sum_scores)*dividend_fund`

然后在`“to_send”`中返回股息支付的金额

`return {"to_send": int(res)}`

但是，由于我们在上面的 Chainlink 请求中添加了`“path”`，它将立即启动向用户发送`“to_send”` ETH 的过程。

通过执行这种离线计算，我们避免了与这种计算相关的天然气费用，这种费用通常会在我们的 Solidity smart 合同中以单独的方法处理这种计算时产生。

最后，在赛季结束时，我们向每个球员资产的主要利益相关者发放“冠军奖金”。这鼓励了市场中的竞争和良性波动，并允许用户在换季后保留一件商品。

## 公关的下一步是什么！ce？

展望未来，我们计划扩展我们通过该项目构建的混合智能合约架构，并继续在加密生态系统中创建半可替代的令牌市场。我们目前正在开发一个令人兴奋的项目，希望很快发布，敬请期待！

### 关于这个话题的更多信息

*   [智能合同开发者使用 Chainlink 的主要方式](https://blog.chain.link/smart-contract-api-price-random/)
*   [如何计算违约差额掉期的价格波动](https://blog.chain.link/how-to-calculate-price-volatility-for-defi-variance-swaps/)
*   [链外计算:使用 Chainlink 进行统计分析](https://blog.chain.link/off-chain-computation-statistical-analysis-with-chainlink/)

如果你是一名开发者，想要将你的智能合约连接到底层区块链之外的现有数据和基础设施，请联系此处的[或访问](https://chainlink.typeform.com/to/gEwrPO)[开发者文档](https://docs.chain.link/) t [版](https://docs.chain.link/)。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[|](https://www.reddit.com/r/Chainlink/)[不和](https://discordapp.com/invite/aSK4zew)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://defi.chain.link/)