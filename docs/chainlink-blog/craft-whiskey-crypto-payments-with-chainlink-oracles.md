# 用链状神谕制作威士忌加密支付

> 原文：<https://blog.chain.link/craft-whiskey-crypto-payments-with-chainlink-oracles/>

贾斯珀和蒂尔曼·德根斯在 2021 年全球做市商黑客马拉松上提交了 Chainlink bounty 获奖作品，他们创建了[威士忌做市商](https://whiskey-marketmaker.surge.sh/)，这是一个 DeFi 平台，利用 Chainlink oracles 使小批量威士忌酒厂能够为投资者标记和列出即将到期的威士忌，同时还允许酒厂通过 Aave 计息池从销售中赚取 ETH 利息。在这篇文章中，Jasper 和 Tillman 讲述了他们是如何用 Chainlink 的 ETH/USD 价格源构建获奖的提交文件的，以及他们是如何克服在 Solidity [智能合约](https://chain.link/education/smart-contracts)中准确表示浮点数的挑战的。

* * *

*由[贾斯珀·德根斯](https://www.linkedin.com/in/jasper-degens-7269a256/)和[蒂尔曼·德根斯](https://www.linkedin.com/in/tillman-degens/)T5】*

对于 2021 年 MarketMake 黑客马拉松，我们努力创建了一个名为[威士忌 MarketMaker](https://whiskey-marketmaker.surge.sh/) 的原型，这是一个连接威士忌爱好者和手工酿酒厂的平台。我们的家族经营着 [Stone Barn Brandyworks](https://www.stonebarnbrandyworks.com/) ，这是一家位于俄勒冈州波特兰市的手工酿酒厂，随着我们对 DeFi space 的了解越来越多，我们意识到桶装陈年威士忌和通过 Aave 这样的平台开设的计息账户有很多共同点:在这两种情况下，你存入一项资产，它的价值会随着时间的推移而增长——每桶威士忌本质上都是一个计息桶。我们想出了一个主意，允许投资者在陈酿过程的早期购买威士忌，同时为小规模酿酒厂提供即时、可获得的资金。简而言之，该平台将金融流动性换成了可饮用的流动性。



![How Whiskey MarketMaker integrates smart contracts into product design](img/3f2cf7880a3138a43bf4f0523c205c84.png)

<figcaption id="caption-attachment-2127" class="wp-caption-text">威士忌做市商如何将威士忌爱好者和手工酿酒厂联系在一起，生产连锁威士忌酒瓶。</figcaption>





我们希望我们的原型具有的一个基本品质是一个简单的酒厂入职流程。对我们来说，这意味着酿酒厂应该专注于他们最擅长的事情(酿造令人难以置信的威士忌)，并在销售产品时尽可能减少摩擦。酒厂以法定货币确定材料、产品和瓶子的成本，并需要遵守严格的政府税收和法规。因此，在平台上保持一致的定价和法定货币是必要的，当需要时， [Chainlink Price Feeds](https://data.chain.link/) 提供对 ETH 的转换。

## 在 DeFi 平台中转换价格

因为我们的总部在美国，所以我们决定以美元定价。为了实现一个基于美元的链上平台，我们考虑了两种方法:第一种方法是接受像或戴这样的稳定成员。这里的一个缺点是，稳定币模式需要购买者拥有多项资产:ETH 用于支付汽油费，稳定币用于购买代币化威士忌。每笔交易都需要 ERC-20 批准和转移步骤来购买瓶子。对我们来说，使用 chain link[ETH/USD](https://data.chain.link/eth-usd)Price Feed 处理 ETH 中的所有支付并在 ETH 和 USD 之间转换更有意义。通过这种方式，酒厂可以像往常一样以美元定价，并选择接受以美元支付的回扣，或者，如果有兴趣，以瑞士法郎支付。

为了在 USD 和 ETH 之间进行转换，我们需要访问一个可靠、准确、防篡改的价格源。在用资金兑换威士忌时，不准确或可操纵的数据输入可能会导致严重的失衡。如果我们的汇率低估了美元，那么酒厂就收不到他们产品的真正价值，如果 ETH 定价太低，顾客就会为他们的威士忌多付了钱。我们需要反映广泛市场覆盖面的可靠汇率，以保证诚实交易。这就是 Chainlink 用分散价格数据来拯救的地方。

任何集成之旅的第一站都是前往 [Chainlink 文档](https://docs.chain.link/docs/using-chainlink-reference-contracts)。我们的用例非常简单，因为我们只想[从 ETH/USD 价格提要中获取最新价格](https://docs.chain.link/docs/get-the-latest-price#config)。对于我们的平台，我们需要处理智能合约和前端的转换:检查在智能合约中购买威士忌时是否发送了足够的 ETH，并确保用户在通过我们的网站购买时也发送了正确数量的 ETH。Chainlink 文档友好地提供了 Solidity 和 JavaScript 的例子(对于 Python 爱好者来说也是 Python)。

## 构建后端

我们将我们的智能合约网络设计成一个小型二重奏:我们有存储定价数据并处理购买和验证逻辑的 [WhiskeyPlatformV1](https://github.com/jasperdegens/whiskeyContracts/blob/main/contracts/WhiskeyPlatformV1.sol) 合约，我们的 [BarrelHouse](https://github.com/jasperdegens/whiskeyContracts/blob/main/contracts/BarrelHouse.sol) 合约存储并管理代表威士忌酒瓶的 ERC1155 代币的所有权。我们选择将这两个组件分开，这样当我们发布一个新平台时，我们可以保持现有令牌所有权的数据层不受影响。

我们将 [Chainlink ETH/USD 价格反馈](https://data.chain.link/eth-usd)与我们的 WhiskeyPlatformV1 合同整合在一起。当酿酒厂创建一个新的酒桶清单时，他们会以美元为单位指定以下详细信息:每瓶酒的起始价格、到期价格和费用(包括酒桶存储成本)。对于每次购买，我们使用购买日期，基于起始价格和到期价格之间的线性插值计算当前的瓶子价格，然后添加存储费用成本。因此，我们为客户提供的价格如下:

```
// clamp date to avoid overflow
uint256 startTimestamp = barrel.startTimestamp;
uint256 endTimestamp = barrel.endTimestamp;
uint256 clampedDate = Math.max(startTimestamp, Math.min(endTimestamp, targetDate));
uint256 totalAgingDuration = endTimestamp - startTimestamp;
uint256 elapsedDuration = clampedDate - startTimestamp;

uint32 startPrice = barrel.startPriceUsd;
uint32 endPrice = barrel.endPriceUsd;
uint32 priceRange = endPrice - startPrice;
uint32 additionalPrice = uint32(uint256(priceRange).mul(elapsedDuration).div(totalAgingDuration));

uint32 currBottlePrice = barrel.startPriceUsd + additionalPrice;
uint256 totalPriceUSD = currBottlePrice * numberOfBottlesToPurchase;
```

这是我们需要用价格馈送转换成 ETH 的美元值。在查询价格提要契约之前，我们需要获得货币对的正确地址。这些文档列出了许多不同网络上的价格对的广泛集合的[合同地址。我们使用了 Kovan testnet 和 ETH/USD 聚合器，所以我们的目标地址是 0x 9326 BFA 02 add 2366 b 30 bacb 125260 af 641031331。因此，我们的下一步是获取价格，并使用该聚合器合同进行转换:](https://docs.chain.link/docs/ethereum-addresses)

```
// Use ChainLink Oracle for price feed for production
AggregatorV3Interface priceFeed = AggregatorV3Interface(0x9326BFA02ADD2366b30bacB125260Af641031331);
(, int256 usdToEthRate, , , ) = priceFeed.latestRoundData();
uint256 totalPriceEth = totalPriceUSD / usdToEthRate;
```

但是，如果我们尝试这样计算，比如说，totalPriceUSD 为 75 美元，汇率为 147139000000，那么我们的总价将是 0！这肯定是不正确的。在这里，我们学到了使用 Solidity 时的第一课:你需要非常小心小数是如何表示的，你需要知道乘法和除法的顺序。

Solidity [本身并不支持浮点运算](https://docs.soliditylang.org/en/v0.5.3/types.html)，所以绕过这一限制的最常见解决方案是对金额使用无符号或有符号整数，然后跟踪货币的小数位数。通常，货币使用许多小数位，例如 ETH 和稳定的货币戴使用 18 位小数。例如，DAI 合同上的余额 12000000000000000 将具有 120000000000000/10^18 的值，大约为 0.12 美元。

当专门处理有符号和无符号整数时，您还需要考虑在合同中存储表示实际金额的值的最佳方式。对我们来说，因为大多数酒厂都用美元来表示他们的价格，所以最有意义的做法是用小数点后两位来表示美元金额，而不是用分币来表示。在我们的平台上，uint“3999”将表示 39.99 美元的美元价值。

我们下一个缺失的信息是找出 USD/ETH 价格馈送合同中有多少个小数位。如果我们看一下[聚合器 v3 接口](https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/interfaces/AggregatorV3Interface.sol)，有一个方便的函数 decimals()，与 ERC 20 国货币相同。因此，如果我们查询，我们可以正确地转换我们的价格！新的逻辑如下。

```
// Use ChainLink Oracle for price feed for production
AggregatorV3Interface priceFeed = AggregatorV3Interface(0x9326BFA02ADD2366b30bacB125260Af641031331);
(, int256 usdToEthRate, , , ) = priceFeed.latestRoundData();
uint8 priceFeedDecimals = priceFeed.decimals();
uint256 totalPriceEth = totalPriceUSD / (usdToEthRate / 10^priceFeedDecimals);
```

如果我把这个计算输入我的计算器，我们得到的价格是 0.02 ETH。但是请记住，我们处在一个没有浮点数的环境中，因为整数向下舍入，这实际上也等于 0——又错了！我们需要从头开始。

对人类来说，用 ETH 来考虑价格很好，但对智能合约来说，用 wei (1 ETH = 10^18 wei)来考虑价格更有用。通过在 wei 中工作，我们可以避免舍入问题以及由此导致的精度损失。此外，以太坊上的支付值都是以魏为单位的，所以如果我们需要验证支付，如果我们已经在用那个单位工作，这将是非常有用的。我们没有从 USD 转到 ETH，而是直接从 USD 转到 wei。我们的新公式看起来像这样:

```
uint256 usdToWei = ( 10^exchangeRateDecimals * 10^18 ) / usdToEthExchangeRate;
```

请注意，这里我们在除以汇率之前首先计算了完整的分子，以便不会由于舍入而损失任何精度。

对于我们的合同，因为我们用两位小数表示美元，为了从合同中存储的金额进行转换，我们采取了一个额外的步骤:

```
uint8 constant INTERNAL_DECIMALS = 2;
uint256 usdToWei = usdToWei / 10^INTERNAL_DECIMALS;
```

现在我们用这一汇率乘以我们的美元数额来确定它的等值魏！价格验证变得超级简单:

```
uint256 totalPriceUsd = (bottlePrice + feesPerBottle) * numBottlesToPurchase;
uint256 requiredWei = totalPriceUsd * usdToWei;
// revert transaction if not enough payment was sent
require(msg.value >= requiredWei, “Payment does not cover the price of bottles”);
```

瞧，我们已经完成了智能合同支付验证！

请注意，如果我们使用这种方法来转换美元兑日元汇率，那么如果我们需要执行多种货币转换计算，我们可以重复使用这种汇率。通过预先计算这个数量，我们确实失去了一点精确性(大约 2e-14%)，相比之下，如果我们先将所有东西相乘，然后再除以，但是我们可以通过减少数学计算来节省更多的汽油成本。

## 构建前端

当一个消费者想买瓶子时，我们需要创建一个以美元表示的价格值转换为 wei 的交易。我们通过 JavaScript 再次查询 Chainlink 价格提要[以获得当前价格。](https://docs.chain.link/docs/get-the-latest-price#javascript)[文档](https://docs.chain.link/docs/get-the-latest-price)使用 web3.js 库与链上合同进行交互，但是对于我们的项目，我们使用了 [ethers.js](https://docs.ethers.io/v5/) :

```
const priceFeed = new ethers.Contract(addr, aggregatorV3InterfaceABI, library);
const roundData = await priceFeed.latestRoundData();
const currRate = roundData.answer.toNumber();
```

由于我们知道了以美元表示的交易金额，我们经历了与智能合约相同的过程，并将美元/瑞士法郎汇率转换为美元/魏。这里有两个重要的注意事项:首先，确保在进行这些计算时使用的是一个[大数字库](https://docs.ethers.io/v5/api/utils/bignumber/)，因为 JavaScript 的内置数字类型在 2^53-1 时达到最大值(在 Solidity 中，我们可以在 uint256 中表示高达 2^256-1 的值)。此外，请记住，您不能在数字中使用小数，因此，如果您的价格格式为$55.25，您的大数库将会出错。根据 dApp 所需的小数位数(如前所述，我们使用 2 位小数)，您需要扩展该数量级，最后除以该数量级。数量级应该与您的智能合约一致，否则您可能会在精确度上有差异，这可能会导致恢复交易。

```
const chainlinkDecimals = await priceFeed.decimals();
// used to expand out decimal places
const internalDecimals = 2;
const usdToWei = ethers.constants.WeiPerEther.mul(chainlinkDecimals).div(ethToUsdRate);
const priceInWei = usdToWei.mul(Math.floor(props.totalPriceUsd * 10**internalDecimals)).div(10**internalDecimals);
```

在此之后，我们使用 ethers.js 将 priceInWei 作为我们的交易值:

```
const trx = await whiskeyPlatform.purchaseBottles(props.tokenId, props.numBottles, {value: priceInWei.toString()});
```

就这样，我们从前端发送了正确的 wei 值，并在后端验证了金额！这一过程确保了平台用户不会支付过高的价格，同时酒厂也获得了产品的真正价值。所有的当事人都可以高枕无忧，给自己倒一杯。

# 摘要

我们使用[chain link ETH/USD Price Feed](https://data.chain.link/eth-usd)来获取 USD 和 ETH 之间的真实汇率，然后使用该汇率来计算在我们的 [DeFi](https://chain.link/education/defi) 平台前端支付所需的 wei，并最终在我们的智能合同中验证支付。这一过程本身相当简单，但在连接现实世界和数字资产、减轻买家和生产商的交易负担时，它可能会非常强大。随着越来越多的市场过渡到接受加密货币，我们相信我们为威士忌做市商开发的转换和支付技术将越来越适用于各种各样的令牌化资产。我们渴望看到接下来哪些实物商品将被令牌化，以及智能合同和 Chainlink [神谕](https://chain.link/education/blockchain-oracles)将如何被用来帮助大大小小的企业。



<figcaption>

![Photo of the author Tilman Degens and a cask and bottle of Hoppin’ Eights whiskey from Stone Barn Brandy Work](img/9d79eb391cc1cfe1e96eab72c5e7f38f.png)

<figcaption id="caption-attachment-2128" class="wp-caption-text">Author Tillman Degens with his own cask of Hoppin’ Eights whiskey.</figcaption>



</figcaption>



## 了解更多信息

如果您是一名开发人员，并且希望将您的智能合约连接到底层区块链之外的现有数据和基础架构，请联系此处或访问开发人员文档。

[Docs](https://docs.chain.link/docs/getting-started)|[Discord](https://discordapp.com/invite/aSK4zew)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[Telegram](https://t.me/chainlinkofficial)|[Events](https://blog.chain.link/category/events/)|[GitHub](https://github.com/smartcontractkit/chainlink)|[Price Feeds](https://feeds.chain.link/)|[DeFi](https://www.chain.link/solutions/defi)|[VRF](https://chain.link/solutions/chainlink-vrf)