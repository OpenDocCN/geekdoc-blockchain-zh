# 使用 Chainlink 构建海上保险智能合同

> 原文：<https://blog.chain.link/build-a-marine-insurance-smart-contract-with-chainlink/>

[Chainlink 虚拟黑客马拉松](https://blog.chain.link/congratulations-to-the-winners-of-the-chainlink-virtual-hackathon-2020/) 获奖者 Lukas Sexton、Luis Ramírez、Ahmad S 和 Mike Robinson 使用 [Chainlink 外部适配器](https://blog.chain.link/build-and-use-external-adapters/) 将海洋航运水位 API 连接到 Chainlink oracle，创建了一个海洋航运参数化保险产品。 [参数保险智能合约](https://blog.chain.link/blockchain-insurance/) 是开发人员如何使用 Chainlink 将[智能合约](https://chain.link/education/smart-contracts)与链外 API 连接起来以自动化遗留保险模型的很好例子。在这篇文章中，团队解释了该项目的思路和实现。

* * *

*由* [*卢卡斯*](https://www.lukassexton.com/)*[*麦克·罗宾逊*](https://www.linkedin.com/in/1mikerobinson/)*[*路易斯·拉米雷斯*](https://twitter.com/cenobyte321) *，以及* [*艾哈迈德·S*](https://twitter.com/waveguide1)**

 **与气候相关的不确定性正在导致更不可预测的航道条件，如低水位或高水位，这可能导致主要航运通道暂时关闭。如果圣劳伦斯航道暂时关闭，估计美国经济每周会损失 1 . 93 亿美元。去年，该频道关闭了 12 天，美国经济损失估计为 3.31 亿美元。

由于世界海运贸易的增长，全球海上保险业接近 300 亿美元，并且还在增长。然而，主要海运航道不可预测的关闭给商业航运公司和下游经济体带来了巨大的金融风险。

我们希望通过提供一种 21 世纪的保险解决方案来帮助内陆海运企业适应气候变化的影响，从而在最重要的时期让内陆海运企业的现代生活更易于管理。

## 什么是参数保险？

参数保险是一种金融工具，通过保护自己免受潜在的灾难性事件来降低风险。参数保险是一种保险，投保人根据特定的预定事件获得预定的赔付。

传统上，参数保险产品是在全球范围内购买的。例如，[国际复兴开发银行(IBRD)](https://www.artemis.bm/news/mexicos-parametric-world-bank-cat-bond-looks-safe-from-m7-4-earthquake/#:~:text=This%20catastrophe%20bond%20was%20Mexico's,earthquake%20and%20hurricane%20insurance%20protection.&text=%E2%80%9CWithin%20the%20Cat%20Bond%20market,to%20earthquake%20risk%20in%20Mexico.) 向墨西哥发行了 4 . 85 亿美元的巨灾债券，为该国提供为期四年的参数地震和飓风保险保护。这些自然灾害风险的参数触发器考虑了发生的强度和位置，本金的 25%、50%、75%和 100%的赔付率由飓风袭击的地点或地震的强度决定。

如果保单索赔成功，保险公司会立即付款，因为支付的条件明确而直接。参数保险非常适合区块链和智能合约，因为智能合约可以自动执行保险流程。智能合同消除了对第三方仲裁的要求，区块链的分布式账本创建了不可变的、可审计的跟踪。这种结合为参数保险中数量惊人的用例提供了机会。

参数保险产品的本质意味着它们非常依赖安全、可信的数据——这就是 chain link[Oracle](https://chain.link/education/blockchain-oracles)发挥作用的地方。Chainlink 使用实时数据并通过智能合同执行协议，为以消费者为中心、自我执行的[分散式保险产品](https://blog.chain.link/how-smart-contracts-can-decrease-information-asymmetry-build-trust-and-revolutionize-the-insurance-industry/)铺平了道路。通过将参数保险协议移动到区块链，并使用 Chainlink 将数据连接到智能合同，参数保险产品可以完全分散，并在商定的数据驱动条件发生时自动执行。

### 分散海运保险

这种 dApp 是一种保险产品，可以防范水路运输延误的风险。dApp 监控通过 [stormglass.io API](https://stormglass.io/) 生成的水位数据，并在特定航道的水位达到预定水平时触发支出。智能合同根据每条水道不可运行的水位范围计算并确定赔付水平(北美各地的情况各不相同)。最后，智能合同向投保人发送一笔付款。



![The components of the parametric marine shipping insurance dApp using Chainlink to deliver off-chain data to smart contracts.](img/77b4a53aba6e412572bdbc7e30d925be.png)

<figcaption id="caption-attachment-1405" class="wp-caption-text">参数化海运保险 dApp 的组件使用 Chainlink 向智能合约传递链外数据。</figcaption>







![An example use case for one of the most extensive shipping waterways in North America, the St. Lawrence Seaway System](img/23026842ec915c615a50748b1ec0c349.png)

<figcaption id="caption-attachment-1404" class="wp-caption-text">以北美最广泛的航运水道之一的圣劳伦斯航道系统</figcaption>



为例

# 技术描述

在黑客马拉松中，我们通过创建一个智能合同和 web 应用程序实现了一个概念验证，允许任何用户购买海运货物保险。用户将提交保险天数和货船的水体位置。购买保险后，智能合同会在水位超出预定范围的每一天自动向投保人付款。

我们首先起草了一个初始的应用程序流，这个应用程序流经历了连续的迭代，产生了一个 UI，这个 UI 执行了我们在概念验证中希望实现的基本流。同时，我们研究了将提供水位数据的 web APIs 和数据源。最后，我们选择 stormglass.io 作为我们的提供商，因为它的 web API 返回相对于世界各地许多站点的平均海平面的海平面数据，类似于一个分散的数据聚合器。在理解了 API 的工作方式及其响应之后，我们构建了一个 Chainlink 外部适配器来将 Storm Glass API 连接到区块链。

对 web APIs 进行去中心化调用需要一个 Oracle 和数据源网络来避免 Oracle 问题。不幸的是，由于时间限制，我们只使用了一个数据源，但是我们仍然希望为我们的 API 调用增加一定程度的分散化。因此，我们决定在两个不同的服务中托管我们的外部适配器，并在两个 Chainlink 节点中注册它。我们在 Google 云平台的云功能中部署了外部适配器的一个实例，在 Microsoft Azure 云功能中部署了另一个实例。然后，我们联系了两个节点操作员，他们帮助我们注册了外部适配器，并在他们的节点中创建了一个工作描述。最后，我们部署了一个 Chainlink [预协调器](https://towardsdatascience.com/api-calls-on-blockchain-best-practice-for-data-collection-11f1fc86a2be#7f8e)契约，它通过取来自两个节点的值的中间值来合并来自两个节点的数据。我们使用 Remix IDE 部署和配置了这个契约。

根据我们设计的业务逻辑，平台应该每天请求每个保单的水位，并评估合同是否应该向投保人支付当天的索赔。我们使用 [Chainlink 警报](https://docs.chain.link/docs/chainlink-alarm-clock)集成实现了这一点，它将在启动后 24 小时触发请求和评估。然而，满足这种设计的更好的实现是使用一个 [Cron 启动器](https://docs.chain.link/docs/initiators#cron)。这种发起程序类型计划一个作业，链节节点应该定期运行该作业。

最后，我们创建了一组管理脚本，帮助我们在 Kovan 和 Rinkeby 测试网络中测试项目。

与智能合约并行，我们使用 React、Rimble UI、Material UI 和毛毛雨框架开发了 web UI。在前端，我们实现了一个 ENS 解析器。

总的来说，下图显示了项目架构的概述:



![The architecture of the marine shipping insurance smart contract and oracle logic.](img/4adeafed294f5932cb29b611caeb6907.png)

<figcaption id="caption-attachment-1403" class="wp-caption-text">海运保险智能合约和甲骨文逻辑的架构。</figcaption>





我们通过使用来自 GitHub 库的代码库[，使用 Chainlink Trufflebox 和外部适配器来引导智能合约代码。](https://github.com/thodges-gh/CL-EA-NodeJS-Template)

## 如何构建和部署项目

### ***获取源代码***

仓库的源代码[位于这个 GitHub 仓库](https://github.com/chainlink-hackathon2020-insurance)中。

*   ***保险-产品***
    **(**[https://github . com/chain link-hackathon 2020-insurance/insurance-product](https://github.com/chainlink-hackathon2020-insurance/insurance-product)**)**:包含项目的智能合约、测试用例、管理脚本、前端代码库。
*   ***风暴玻璃-海平面-适配器*(**[https://github . com/chain link-hackathon 2020-insurance/风暴玻璃-海平面-适配器](https://github.com/chainlink-hackathon2020-insurance/stormglass-sealevel-adapter) **)** :包含风暴玻璃海平面 API Chainlink 适配器。

使用以下命令克隆两个存储库:

```
$ git clone https://github.com/chainlink-hackathon2020-insurance/insurance-product.git
$ git clone https://github.com/chainlink-hackathon2020-insurance/stormglass-sealevel-adapter 

```

### 编译和部署智能合同

作为先决条件，我们需要通过运行以下命令来确保安装了 Truffle:

```
$ npm install -g truffle

```

我们首先需要通过运行以下命令来安装所有依赖项:

```
$ npm install

```

为了运行*保险产品*代码库的测试，我们将运行:

```
$ npm test

```

为了将合同部署到网络，我们将使用适当的值设置 truffle-config.js 文件中使用的环境变量*助记符*和 *RPC_URL* 。最简单的方法是创建一个定义了这些变量的. env 文件。

然后，我们将运行命令:

```
$ npm migrate:live

```

### 设置和部署外部适配器

为了测试和部署外部适配器，我们需要创建一个帐户，并从 Storm Glass 获得我们的 API 密钥:[https://stormglass.io/](https://stormglass.io/)。

为了运行*stormglass-sealevel-adapter*的测试，我们首先需要用从 Storm Glass 获得的密钥定义环境变量 *API_KEY* ，然后运行命令:

```
$ npm test

```

我们也可以通过运行以下命令来手动测试外部适配器:

```
$ npm start

```

这将在本地服务器上运行适配器。然后，我们可以通过运行以下 curl 命令调用适配器，该命令请求特定坐标的水位:

```
$ curl -X POST -H "content-type:application/json" "http://localhost:8080/" --data '{ "id": 0, "data": { "lat": 43.38, "lng": -3.01 } }'

```

最后，为了使适配器对公众可用，我们需要将它部署在公共环境中。最简单的方法是使用无服务器功能服务。我们使用的代码库是为 GCP 函数和 AWS Lambda 设置的。我们还增加了对 Azure 云功能的支持。自述文件详细描述了如何在这些平台上执行部署。这里要考虑的关键问题是在部署环境中设置 *API_KEY* 变量。

### 在 Chainlink 节点中注册外部适配器

当我们注册外部适配器时，我们将使用之前的部署。我们将把桥 URL 设置为我们部署的无服务器功能的 URL。

接下来，我们将创建一个使用外部适配器的作业规范:

```
{
  "initiators": [
    {
      "type": "runlog",
      "params": {
        "address": "<input Chainlink Oracle contract address>"
      }
    }
  ],
  "tasks": [
    {
      "type": "stormglass-sealevel-adapter"
    },
    {
      "type": "copy",
      "params": {
        "copyPath": "result"
      }
    },
    {
      "type": "multiply",
      "params": {
        "times": 100
      }
    },
    {
      "type": "ethint256"
    },
    {
      "type": "ethtx"
    }
  ]
}

```

请注意，在本规范中，我们使用*乘*本机适配器将外部适配器响应乘以 100。原因是 Solidity 不支持浮点数，Storm Glass API 返回的结果以米为单位，以厘米为单位。

### 部署预协调器合同

要对 Storm Glass 进行真正分散的 API 调用，我们需要在不同的平台上托管外部适配器，并在多个 Chainlink oracles 中注册它。越多越好。为了合并所有 Chainlink oracles 返回的数据，我们将部署和配置一个 PreCoordinator 契约。您可以在项目的*合同*文件夹(*marinensuranceeapcordinator . sol*)中找到预协调人合同。为了方便起见，我们将使用 Remix IDE 部署这个契约。

首先，添加文件或创建新合同，并复制和粘贴 PreCoordinator 合同的内容。接下来，编译契约，并使用“注入的 Web3”环境部署它，将元掩码插件设置为 oracles 所在的适当网络。在 deployment 选项卡中，确保在“Contract”下拉列表中选择 PreCoordinator。

部署合同后，使用 *createServiceAgreement* 函数创建一个服务协议。该函数接受以下参数:

*_minResponses* :在计算值的中值和调用原始契约的回调函数之前，我们期望响应的 oracles 的最小数量。
*_ Oracle*:服务协议将包含的 Oracle 数组。
*_jobIds* :我们在上一步中创建的作业规范的标识符数组。
*_payments* :我们在最后一步创建作业规范时定义的执行作业规范的链接费用数组。

对于*_ Oracle*数组的每个元素，必须有一个作业 id 和付款，分别在 *_jobIds* 和 *_payments* 数组中的相同位置定义。示例:



![Service agreement array model for Remix IDE.](img/07ddecd917310ec5858a7e090e422a70.png)

<figcaption id="caption-attachment-1402" class="wp-caption-text">混合集成开发环境的服务协议数组模型。</figcaption>





在我们的项目中，我们的价值观是这样的:



![Snapshot of Remix IDE array with sample values.](img/b2184f063b67db9612ea15d9c6bd4d6b.png)

<figcaption id="caption-attachment-1401" class="wp-caption-text">用样本值重新混合 IDE 数组的快照。</figcaption>





执行该函数后，我们将查看提交的事务。在第一个位置的主题中返回的值将是我们将在我们的海上保险 Chainlink-secured 合同中指定的作业 ID。我们还将把预协调者的合同地址设置为 oracle 地址。



![Example of a submitted transaction on the Kovan Network Etherscan.](img/b14769b7307ee9f89535e3011a744fc1.png)

<figcaption id="caption-attachment-1400" class="wp-caption-text">在科万网络以太网上提交交易的例子。</figcaption>





### 块菌管理脚本

该项目附带了一组 Truffle 脚本，用于资助、配置和测试我们在上一节中部署的智能契约。

我们可以使用以下命令来执行这些脚本:

```
$ truffle exec scripts/<script_file_name> --network live

```

进行初始配置的脚本按照理想的执行顺序进行编号。

*1_set_oracle_data.js* :设置 oracle 数据取水级别:oracle 地址、作业 id、付款。
*2 _ set _ evaluation _ period . js*:以秒为单位设置水位评估周期。默认情况下，是一天。
*3 _ fund _ contract _ eth . js*:向 ETH 提供合约资金。
*4 _ fund _ contract _ link . js*:用 LINK 为合同提供资金。
*5 _ create _ insurance _ policy . js*:用预定义的数据创建保险单。
*6 _ start _ evaluation _ period . js*:触发 Chainlink 报警，在设定的时间段后评估水位。

我们需要检查每个脚本的值，以确保它们是足够的和正确的。

该项目还有另一组用于测试和演示的脚本:

*change _ water _ level _ Manually . js*:手动改变给定策略的水位。这是用于演示的目的。
*get _ insurance _ policies . js*:返回当前用户的保单及保单标识。
*request _ water _ level _ manually . js*:手动执行所有已注册保单的水位请求。

### 运行前端

当我们执行 migrate 命令时，abi 将输出到客户机文件夹(client/src/abi ),并带有其部署的相应地址。在运行前端之前做这件事是很重要的。

要运行前端，我们将首先通过运行以下命令转到客户端文件夹:

```
$ cd client

```

接下来，我们将通过运行以下命令来安装客户端依赖项:

```
$ npm install

```

最后，我们将使用以下代码运行前端:

```
$ npm start

```

控制台将显示前端可用的本地 URL。在安装了 MetaMask 插件的浏览器中打开 URL。

## 智能合同亮点

### 存储结构

存储保险单相关值的主要结构有:

```
   InsurancePolicy[] public insurancePolicies;
   mapping(address => uint[]) public insurancePolicyOwnership;
   mapping(bytes32 => uint) requestToInsurancePolicyId;

```

*insurancePolicies* 数组存储所有保险单及其货物和位置数据、水位值和状态。数组索引充当保险单标识符。

*insurancePolicyOwnership* 映射将以太坊地址与一组策略标识符相关联。

*requestToInsurancePolicyId*映射将 Chainlink 请求与策略标识符相关联。

### 主要功能

智能合约中的三个主要功能概括了我们平台的主要业务逻辑:

```
function registerInsurancePolicy(
    ShipData memory _shipData,
    Coordinate memory _location,
    uint256 _startDate,
    uint256 _endDate
)
    public payable returns(uint256) 
{
    uint256 premium = calculatePremium(_shipData);	
    require(premium == msg.value, "You need to pay the policy premium");
    uint256 claimPaymentAmount = calculateDailyClaimPayouts(_shipData);

    TrackingData memory initialTrackingData = TrackingData({
        location: _location,
        currentWaterLevel: -9999,
        currentRequestId: "0x0",
        requestStatus : RequestStatus.CREATED
    });

    CoverageData memory coverageData = CoverageData({
        startDate: _startDate,
        endDate: _endDate,
        dailyClaimAmount: claimPaymentAmount,
        waterLevelMin: -50,
        waterLevelMax: 50,
        beneficiary: msg.sender
    });

    InsurancePolicy memory policy = InsurancePolicy({
        coverageData: coverageData,
        shipData: _shipData,
        trackingData: initialTrackingData
    });

    insurancePolicies.push(policy);
    uint256 identifier = insurancePolicies.length - 1;
    insurancePolicyOwnership[msg.sender].push(identifier);
    emit InsurancePolicyCreation(msg.sender, identifier);
    return identifier;
}

```

这个函数接收货船数据、它将要行驶的水体的位置，以及保单生效的日期范围。它检查发送者已经发送了保险费的准确数量(在这个版本中是常数)。然后，它通过调用另一个函数并将船数据作为参数传递来计算索赔金额(在这个版本中，该函数返回一个常数)。然后，它用状态、请求标识符和水位的初始值设置所有保险单信息。接下来，它将策略添加到保险单数组中，获取标识符，并将发件人地址与策略标识符相关联。最后，它发出一个事件来表示保险单的创建。

```
function requestWaterLevels() private {
    for(uint i = 0; i < insurancePolicies.length; i++) {
        InsurancePolicy storage insurancePolicy = insurancePolicies[i];
        if(isPolicyActive(insurancePolicy)){
            insurancePolicy.trackingData.requestStatus = RequestStatus.INITIATED;
            Chainlink.Request memory request = buildChainlinkRequest(waterLevelJobId, address(this), this.receiveWaterLevel.selector);
            request.add("lat", insurancePolicy.trackingData.location.lat);
            request.add("lng", insurancePolicy.trackingData.location.lng);
            bytes32 requestId = sendChainlinkRequestTo(waterLevelOracle, request, waterLevelFee);
            requestToInsurancePolicyId[requestId] = i;
        }
    }
}

```

这个私有函数遍历 *insurancePolicy* 数组中的所有策略。它使用 Chainlink oracle 或 PreCoordinator 为所有活动的策略请求水位数据。另外两个函数调用这个函数:手动请求水位的函数和 Chainlink 警报。该函数指定一旦 oracle 获得数据，必须将其作为参数传递给*receive level 函数*，我们接下来将会看到这个函数。

```
function receiveWaterLevel(bytes32 _requestId, int256 _level) public recordChainlinkFulfillment(_requestId){
    InsurancePolicy storage insurancePolicy = insurancePolicies[requestToInsurancePolicyId[_requestId]];
    insurancePolicy.trackingData.currentWaterLevel = _level;
    insurancePolicy.trackingData.requestStatus = RequestStatus.COMPLETED;
    delete requestToInsurancePolicyId[_requestId];

    if (_level > insurancePolicy.coverageData.waterLevelMin &&
        _level < insurancePolicy.coverageData.waterLevelMax) {
        return;
    }
    //Create and pay claim
    else {
        uint amountToPayToday = insurancePolicy.coverageData.dailyClaimAmount;
        insurancePolicy.coverageData.beneficiary.transfer(amountToPayToday);
        emit ClaimPayout(insurancePolicy.coverageData.beneficiary,
            requestToInsurancePolicyId[_requestId],
            amountToPayToday);
    }

    if(!isPolicyActive(insurancePolicy)) {
        emit InsurancePolicyExpired(insurancePolicy.coverageData.beneficiary,
            requestToInsurancePolicyId[_requestId], now);
    }

    if(waterLevelEvaluationPeriodActive) {
        startWaterLevelEvaluationRequestPeriod();
    }
}

```

从广义上讲， *receiveWaterLevel* 函数执行以下操作。它通过使用 *_requestId* 作为对*requeststoinsurancepolicyid*映射的索引来获取保险单，该映射返回同时作为保险单数组的索引传递的保险单标识符。之后，它将水位设置到保险单跟踪数据部分。然后，它会评估水位是否超出预设范围。如果是这种情况，那么智能契约将索赔金额转移到保险单受益人，在这个特定的契约中，受益人是注册保险单的地址。最后，如果保险单已经过期，它会发出一个事件。

## 建立分散参数保险

从这里开始，该团队正在考虑探索更多分散参数保险产品的用例，这些产品可以在我们已经构建的相同智能合同框架上运行。我们选择将重点放在一条海上航道上进行概念验证，但该保险产品可扩展到北美所有重要的海上航道。我们的目标是从那些处理最多海洋运输和经历最大水位波动的地方开始。我们的愿景是在全球范围内提供完全分散的参数海上保险，以保护企业和经济免受波动的航道条件造成的财务困难。

以我们在黑客马拉松中构建的 MVP 为例，我们设想了以下任务来使它成为一个成熟的产品:

*   向用户请求船舶和货物数据，并使用它来确定索赔和保险费金额。目前，这两个值在智能合约中是恒定的。
*   查看输入数据并添加更多检查，例如，确保 *_startDate* 参数始终小于 *_endDate* 参数。
*   在连接到 mainnet 的 Chainlink 节点中注册外部适配器。
*   Storm Glass 返回了世界范围内大量水文站的数据，但这并不是海洋数据的全部。我们将找到其他数据源，从 Storm Glass 没有注册的站点返回水位数据，以扩大保险市场覆盖范围。
*   不是追踪船将要使用的水体坐标，而是追踪船的位置坐标。
*   根据提交的客户数据量添加保险等级或套餐。例如，我们可以从将与 ENS 地址相关的帐户放入更高的层开始。

我们对 Chainlink 和智能合约为参数保险行业带来的未来机遇感到兴奋。我们欢迎任何邀请，与行业专家、其他热情的开发者或 Chainlink 社区联系，进一步讨论我们的想法。希望本指南提供了关于如何使用 Chainlink 开发参数化保险产品以增强其智能合同功能的指导。

* * *

## 了解更多信息

建立自己的分散保险产品？如果您是一名开发人员，并且希望将您的智能合约连接到底层区块链之外的数据，请访问[开发人员文档](https://docs.chain.link/)，并参加 [Discord](https://discordapp.com/invite/aSK4zew) 中的技术讨论。如果您想安排一次电话会议来更深入地讨论整合事宜，请点击此处的。你还应该访问 [chain.link](https://chain.link/) ，订阅 [Chainlink 简讯](https://chn.lk/newsletter)，在 Twitter 上关注 [@chainlink](http://www.twitter.com/chainlink) 。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[|](https://www.reddit.com/r/Chainlink/)[不和](https://discordapp.com/invite/aSK4zew)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://defi.chain.link/)**