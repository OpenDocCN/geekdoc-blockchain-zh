# 用 Chainlink Oracles 构建房地产 dApp

> 原文：<https://blog.chain.link/build-a-real-estate-dapp-with-chainlink-oracles/>

[智能合同](https://chain.link/education/smart-contracts)开发商可以使用 Chainlink oracles 直接在线获取房地产估价，为房地产行业提供新的 DeFi 产品和市场。

[分散金融(DeFi)](https://chain.link/education/defi) 已经展示了各种各样的隐货币、商品、指数、股票等如何在链上表现为以真正的链外资产或合成代币为后盾的[NFT](https://chain.link/education/nfts)，这些资产为没有实际所有权的基础资产提供风险敞口。Chainlink 一直处于这些 DeFi 市场的核心，为每种资产类型提供价格预测。这使得新产品和市场能够在借贷、衍生品、资产管理等领域迅速推出。

Chainlink 现在带来了一个新的资产类别:房地产。仅房地产行业就很庞大，预计从 2020 年的 26873.5 亿美元增长到 2025 年的 37170.3 亿美元。不仅房地产资产可以在区块链作为代币数字化，而且[混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/)可以将逻辑应用到它们的链上使用，例如根据基准进行交易，用作贷款的抵押品，实现基于行业趋势的预测市场，或者通过分散的 ETF 作为链上流动性来支持被动收益率。

在下面的教程中，我们将展示开发人员如何使用 chain link[Oracle](https://chain.link/education/blockchain-oracles)来获取关于住宅房地产估价的高质量数据。这涉及到访问两个高级数据提供商。

*   **[SmartZip](https://smartzip.com/)** —根据其专利自动估价模型(AVM)提供住宅房地产价值的估计。
*   **[ProspectNow](https://www.prospectnow.com/)** —提供给定特定邮政编码的上一季度住宅房地产每平方英尺平均价格的数据。

然后，可以对 SmartZip 和 ProspectNow 的数据进行平均，以生成多源估价，用于可靠地对链上的令牌化或合成房地产资产进行定价，并实现新的 DeFi 产品和市场。要了解混合智能合同如何扰乱房地产行业，请参考我们的博客文章[区块链技术如何改变房地产行业。](https://blog.chain.link/blockchain-technology-real-estate/)

## 使用 SmartZip 和 ProspectNow 数据

### 合同设置

我们从使用 Chainlink Any-API 功能的契约的典型契约初始化开始。导入 ChainlinkClient 协定以访问 Chainlink 请求函数，然后将该协定定义为 ChainlinkClient 及其构造函数。

```
import "https://raw.githubusercontent.com/smartcontractkit/chainlink/master/evm-contracts/src/v0.6/ChainlinkClient.sol";

contract RealEstateDataConsumer is ChainlinkClient {

    uint256 oraclePayment;

    constructor(uint256 _oraclePayment) public {
        setPublicChainlinkToken();
        oraclePayment = _oraclePayment;
    }
    // Additional functions here:

}

```

### SmartZip 数据请求

实际的数据请求是使用 Chainlink 执行的。请求结构，它是以前导入的 ChainlinkClient 协定的一部分。使用这个请求结构很简单，只需用默认的 buildChainlinkRequest 函数初始化该结构，然后使用 add 方法将所需的参数添加到请求中。您添加的参数取决于您需要的数据和您使用的 API。

对于 SmartZip 的 API，检索估价数据所需的请求参数是 property_id SmartZip 房地产 AVM Oracle 页面。

```
function requestDataSmartZip
(
    address _oracle,
    bytes32 _jobId,
    string memory _propertyId
) 
    public 
    returns (bytes32 requestId)
{
    Chainlink.Request memory req = buildChainlinkRequest(_jobId, address(this), this.fulfillSmartZip.selector);
    req.add("property_id", _propertyId);
    return sendChainlinkRequestTo(_oracle, req, oraclePayment);
}

```

### SmartZip 数据实现

一旦发送了请求，完成请求的 SmartZip oracle 节点将检索数据，格式化数据，并将其返回给构建请求时指定的回调函数。在本例中，我们将该函数命名为 fulfillSmartZip，由请求构建的`this.fulfillSmartZip.selector`参数指定。对于 SmartZip，数据以 256 位无符号整数的形式返回，即属性的值。这个实现函数的存在只是为了接受数据。一旦检索到，数据现在就在链上，您可以随意使用它:记录它，将其发送给另一个函数进行处理，根据值触发另一个函数，等等。

```
uint256 public smartZipData;

function fulfillSmartZip(bytes32 _requestId, uint256 _data)
    public
    recordChainlinkFulfillment(_requestId)
{
    smartZipData = _data;
}
```

### 展望未来数据请求

现在，我们的智能合同中已经有了 SmartZip 数据，让我们也使用 ProspectNow 数据，这样我们就可以使用这两组数据来对价格信息进行三角分析。我们首先创建另一个函数来执行对 ProspectNow oracle 的请求，这次将邮政编码传入“propertyZip”参数。这将用于提供指定邮政编码的最后一个季度的住宅房地产每平方英尺的平均价格。一旦添加，我们只需将它发送到 ProspectNow oracle，以及指定的付款。可以在 Chainlink 文档中的 [ProspectNow 房地产数据 oracle](https://docs.chain.link/docs/prospectnow-data-oracle/) 页面上找到用于作业 ID、Oracle 合同和费用的详细信息。

```
function requestDataProspectNow
(
    address _oracle,
    bytes32 _jobId,
    string memory _propertyZip
) 
    public 
    returns (bytes32 requestId) onlyOwner  
{
    Chainlink.Request memory req = buildChainlinkRequest(_jobId, address(this), this.fulfillProspectNow.selector);
    req.add("propertyZip", _propertyZip);
    return sendChainlinkRequestTo(_oracle, req, oraclePayment);
}

```

### PropertyNow 数据实现

一旦发送了请求，完成请求的 ProspectNow oracle 将检索数据、格式化数据，并将其返回给构建请求时指定的回调函数。在本例中，我们将该函数命名为 fulfillProspectNow，由请求的`this.fulfillProspectNow.selector`参数指定。对于 ProspectNow，数据以无符号整数的形式返回，即指定邮政编码的最后一个季度每平方英尺住宅房地产的平均价格。

```
uint256 public prospectNowData;

function fulfillProspectNow(bytes32 _requestId, uint256 _data)
    public
    recordChainlinkFulfillment(_requestId)
{
    prospectNowData = _data;
}

```

## 部署和测试合同

现在我们有了合同，我们可以将它部署到 Kovan 测试网络，并用一些数据进行测试。由于 SmartZip 和 ProspectNow oracles 在 Chainlink 文档中各自的页面中都指定了相同的费用 0.1 LINK，因此在部署契约时，我们将`100000000000000000`作为参数传递给构造函数。然后，一旦我们[为我们与 LINK 的合同](https://docs.chain.link/docs/fund-your-contract/)提供了资金，我们只需执行`requestDataSmartZip`和`requestDataProspectNow`函数，并传入所需的参数。

![Requesting data from SmartZip](img/45f835876d91a4eff8520f6128624885.png)

![Requesting data from PropectNow](img/6ddd703e7de9eb87c1344572c1d611b4.png)

一旦请求得到满足，我们就可以通过执行`smartZipData`和`zipData`函数来查看 SmartZip Oracle 和 ProspectNow Oracle 返回的值。在 ProspectNow 数据的情况下，每平方英尺的价格乘以 100000000，以确保结果中没有小数。

![Viewing returned data from SmartZip](img/e2dbeb83a619f472cc2a5ae3639d1873.png)

![Viewing returned data from ProspectNow](img/574188fb1d1304b167594046648baf2c.png)

## 将数据整合在一起

既然我们的智能合约中有来自 SmartZip 和 ProspectNow 的数据，我们就可以对数据进行三角分析，并得出各种有用和有意义的信息，这些信息可以用作执行智能合约事件和逻辑的基础。

从 SmartZip 接收的数据提供了通过 SmartZip 的自动估价模型(AVM)计算的房屋估价，从 ProspectNow 接收的数据提供了指定邮政编码的最后一个季度的住宅房地产每平方英尺的平均价格。如果我们结合给定邮政编码的房产的这两条数据，我们可以确定指定房产的估价是高于还是低于过去一个季度的平均价格，然后根据结果在我们的智能合同中采取某种行动。

```
 function isPropertyOverAverage (uint _squareFootage) public view returns (bool) {
     //return true if property valuation is over the average 
     //price per sqft x given sqft
     return ((smartZipData * 10**8)  > (prospectNowData * _squareFootage));
  }

```

![Calculating if the SmartZip Automated Valuation Model valuation is greater than the average for the given ZIP code for the given square footage](img/eaaf2e002cdd91e16ebe82ccdcebadce.png)

<figcaption id="caption-attachment-2058" class="wp-caption-text">Calculating if the SmartZip Automated Valuation Model valuation is greater than the average for the given ZIP code for the given square footage</figcaption>



除此之外，我们可以使用组合数据来获得相对值，例如两个价格的平均值，一个是预测估计值，另一个是基于 ProspectNow 平方英尺的平均值。

```
  function getPropertyAverage (uint _squareFootage) public view returns (uint) {
      //return average of property value and ZIP code average x square footage
      return (((smartZipData * 10**8)  + (prospectNowData * _squareFootage)) / 2);
  }

```

![Obtaining the average property valuation based on the two different pricing valuation models](img/377ca096d4f74a15e7e251d9818d88cf.png)

<figcaption id="caption-attachment-2059" class="wp-caption-text">Obtaining the average property valuation based on the two different pricing valuation models</figcaption>



然后，开发商可以使用这些价值来为房地产资产定价，结算预测市场，检查房地产支持的贷款抵押，设定交易价格基准，等等。

## 额外发展资源

除了上面的数据提供者之外，开发人员可以遵循我们的外部适配器文档来构建到任何外部 API 的连接，以便获取数据或将新数据集与上面的值相结合。[https://docs.chain.link/docs/external-adapters/](https://docs.chain.link/docs/external-adapters/)

开发人员可以在我们的 [Discord](https://discordapp.com/invite/aSK4zew) 中提出任何技术问题，也可以使用[chain link Solutions Typeform](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog)与 Chainlink Labs 团队建立电话联系，讨论更深入的产品供应。

要了解更多关于 Chainlink 的信息，请访问 [chain.link](https://chain.link/) ，订阅 [Chainlink 简讯](https://chn.lk/newsletter)，并在 Twitter 上关注 [@chainlink](http://www.twitter.com/chainlink) 。要了解 Chainlink 网络的完整愿景，请阅读 [Chainlink 2.0 白皮书](https://chain.link/whitepaper)。