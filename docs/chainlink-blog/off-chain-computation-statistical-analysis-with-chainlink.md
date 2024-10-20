# 离链计算:使用 Chainlink 进行统计分析

> 原文：<https://blog.chain.link/off-chain-computation-statistical-analysis-with-chainlink/>

随着世界发现智能合约不断扩展的可能性，整个区块链的交易量呈指数级增长。随着这种采用的激增，开发人员正在不断扩展智能合同可以处理和计算的内容。在智能合同的快速增长的使用和复杂性之间，安全的链外计算正在成为优化天然气成本、减少网络拥塞和实现功能丰富的 dApps 的日益重要的服务。

然而，由于其变化的性质，计算任务本质上很难概括。例如，与从具有一些标准化 GET/POST 方法的 API 中检索数据不同，计算可以以多种方式执行，并且可以跨多个数据集执行，这些数据集之间可能没有任何一致性。我们将在本教程中对天气数据进行统计分析，这与对图像识别进行计算有很大不同。由于任务的多样性，需要一个灵活的框架来允许开发者根据他们特定的计算任务来定制他们的解决方案。

## 利用 Chainlink 高度可配置的 Oracle 网络计算天气数据

[Chainlink](https://blog.chain.link/what-is-chainlink/) 旨在为智能合约开发人员提供这种计算灵活性，提供一个与链无关且适应性强的框架，允许 oracle 网络中的节点承担多种任务，包括服务[任何数据请求和执行任何链外计算](https://blog.chain.link/how-chainlink-supports-any-off-chain-data-resource-and-computation/)。 [Chainlink 外部适配器](https://blog.chain.link/build-and-use-external-adapters/)允许开发人员创建部分离链代码，这些代码可以以开发人员认为合适的任何方式运行，只要输入和输出符合 Chainlink 节点定义的接口，然后将结果提交回链上。这种可插拔架构使 Chainlink 节点能够混合和匹配外部适配器，这些适配器具有手头任务所需的非常不同的功能。要了解更多关于开发外部适配器的信息，请查看我们的[构建和使用外部适配器](https://blog.chain.link/build-and-use-external-adapters/)文章。

对于本指南，我们将从 PatrickAlphaC 的 OpenWeather 外部适配器开始作为我们的模板，并修改它以包括一些额外的计算。在这个 OpenWeather 适配器中，为 Chainlink 节点提供了一个位置，并使用 OpenWeather API 返回一个 JSON 对象，该对象包含该位置的当前天气数据。如果您需要当前的原始天气数据，这是非常好的，但有时原始数据是不够的。用户可能希望根据历史数据做出决策，或者更具体地说，根据历史数据的统计分析做出决策。用户现在需要在多天内进行多次调用，而不是对原始数据进行一次 API 调用，此外还需要对数据进行修整，然后对其执行任何所需的分析。

在我们的例子中，我们希望找到过去 5 天的标准偏差(免费层 OpenWeather API 的限制)。正如您所看到的，这个问题需要比仅仅检索 API 数据多一个数量级的步骤。如果我们在链上这样做，天然气成本将会迅速膨胀，因为要在链上发布多条数据，然后对数据集进行多次循环迭代，以计算标准偏差。这种计算实际上将变得不可能在线执行，因为天然气成本将上升到没有合理的用户会使用它的程度。

链式网络通过将所有繁重工作从链上卸下来，提供了一种具有成本效益的解决方案，在这种情况下，它可以以本机计算机硬件的全计算速度执行无气体计算。分散式 [oracle](https://chain.link/education/blockchain-oracles) 网络中的节点仅提交链上的可验证输出，这得益于区块链的可审计性和一致性。通过这种方式，智能合约开发人员可以构建[混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/)，利用两个领域的优势——链上合约逻辑的可信执行和由 Chainlink oracles 支持的链外服务的成本效益。

随着 [Chainlink 2.0 白皮书](https://chain.link/whitepaper)中概述的分散式 Oracle Networks(don)功能的扩展，外部适配器的功能将通过链外共识机制得到进一步扩展。目前，离线计算必须在多个节点上运行，然后如果用户希望通过分散的计算输入获得高价值合同，则检查链上的一致性。这仍然留下一些计算，共识，在链上。利用 don，链式网络的子网可以专用于计算任务，并可以通过密码证明机制(如离链报告(OCR)、门限签名和安全多方计算)达成自己的共识。这进一步减少了链上负载，因为节点只需要在链上发布它们的分布式计算一致性的加密证明。这种非链共识模型将使 don 能够以比我们今天已经拥有的标准外部适配器插件架构更强大的方式来增强区块链网络和第 2 层解决方案。

## 设计离线计算

现在，让我们从如何使用当前可用的外部适配器功能来设计这种链外计算开始。你可以在 GitHub 上找到这个适配器的完整代码: [Chainlink 离链计算天气适配器](https://github.com/gmondok/compute_weather_5d_sd_ea)。具体来说，我们想用这个外部适配器计算的是当天的温度是否大于过去四天的标准偏差。这可能对农作物保险智能合同有用，这种合同将在极端天气条件下向农民支付费用。有了这样一份在天气变化时向农民付款的合同，农民可以对冲风险，并自动获得保险赔付，以抵消潜在的作物和收入损失。

```
const createRequest = (input, callback) => {
    // The Validator helps you validate the Chainlink request data
    const validator = new Validator(callback, input, customParams)
    const jobRunID = validator.validated.id
    const endpoint = validator.validated.data.endpoint || 'timemachine'
    const url = `https://api.openweathermap.org/data/2.5/onecall/${endpoint}`
    const lat = validator.validated.data.lat
    const lon = validator.validated.data.lon
    var date = new Date();
    var dt = Math.floor(date.getTime() / 1000);
    const appid = process.env.API_KEY;
    console.log(appid);
    var tempArray = [];
```

首先，根据 OpenWeather 的 API 文档，我们需要修改 API 端点，因为我们现在请求的是历史数据而不是当前数据。我们用的是“onecall/timemachine”，这是他们的历史终点。此外，还添加了一个时间变量，因为 API 请求现在需要一个历史时间来指定应该检索哪一天的数据。最后，我们添加了一个 tempArray 来保存多天的数据，这些数据将被检索和计算。

```
//loop for 5 requests (5 days of data)
for (i = 0; i < 5; i++) {
    var  params = {
        lat,
        lon,
        dt,
        appid
    }

    var config = {
        url,
        params
    }

    // The Requester allows API calls be retry in case of timeout
    // or connection failure
    Requester.request(config, customError)
    .then(response => {
        //Store average temp data from this day (average across 24hrs)
        var sum = 0;
        for (j = 0; j < 24; j++) {
            sum = sum + response.data.hourly[j].temp;
        }
        tempArray[i] = sum/24;
    })
    .catch(error => {
        callback(500, Requester.errored(jobRunID, error))
    })
    //Subtract 1d in seconds each loop
    dt = dt - 86400;
}
```

构建 API 请求循环

接下来，我们有主 API 请求循环。由于需要五天的数据，我们必须循环五次，每天发出一个 API 请求，并将数据累积在`tempArray`中。具体来说，我们需要每天的平均温度，因为我们的最终目标是确定当天的温度是否大于过去四天的标准偏差。因此，对于每一天，我们将所有 24 小时的温度相加，然后除以 24 得到平均值。对于每个循环，我们以秒为单位减去一天，这样下面的 API 请求就是前一天的。

```
//tempArray is now populated with 5d of average temps
    //Calc standard deviation of prev 4 days
    let calc = calcStandardDev(tempArray);
    const mean = calc[0];
    const sd = calc[1];
```

```
//Calculates standard deviation of an array of data, in this case, temperatures
//Returns mean and sd in an array
function calcStandardDev(temps) {
    var tmp = 0;
    for (i = 1; i < temps.length; i++) {
        tmp = tmp + temps[i];
    }
    const mean = tmp/(temps.length-1);
    var diffArray = [];
    for (i =1; i < temps.length; i++) {
        diffArray[i] = Math.pow((temps[i]-mean), 2);
    }
    var variance = 0;
    for (i =1; i < temps.length; i++) {
        variance = variance + diffArray[i];
    }
    variance = variance/(temps.length-1);
    return [mean, Math.sqrt(variance)];
}
```

现在我们已经收集了平均温度，我们可以开始对数据进行主要的计算，以确定标准偏差。函数 `calcStandardDev(temps)` 对此进行处理。注意，这段代码是标准的 JavaScript。没有特定的可靠性函数或语法，因为这段代码完全是离线的。这里执行的数学只是计算标准差的方法，就像在任何编程语言中一样。这种方法是找出所有温度的平均值，存储在 `mean` const 中，从每个温度中减去平均值，对它们求平方，并将这些值存储在 `diffArray` 中，对所有的平方差求和，并除以差的数量，得到方差，最后对方差求平方，得到标准偏差。

在这一点上，我们现在有 5 个 API 请求循环，4 个循环用于平均 temps，4 个循环用于生成差异，每个循环都涉及一些重要的操作，比如 API 数据检索、指数幂函数和平方根函数。很明显，即使对于这种计算标准差的相对标准的任务，执行这种链上操作的成本也会超过成本效益点，特别是当考虑超过五天的数据时，就像我们在这里做的那样。

```
//Report if current day is > 1/2 standard deviation from mean
    var result = false;
    if ((tempArray[0] > sd/2 + mean) || (tempArray[0] < mean - sd/2)) {
        result = true;
    }
// console.log(statusSum);
    callback(200,
        {
            "id": jobRunID,
            "data": {"answer": result}
        });
```

计算出标准偏差后，剩下的就是在回调中将我们的响应返回给请求合同。我们试图确定今天的温度(tempArray[0])是否大于过去四天温度平均值的标准差。这意味着上面的偏差和下面的偏差都存在，所以如果满足任何一种情况，我们都返回 true。由于我们返回到契约的是一个 JSON 对象，我们将其格式化以满足在 [Chainlink 外部适配器文档](https://docs.chain.link/docs/developers/) 中定义的 JSON 有效负载。第一个键是 id(在请求中传递),第二个键是数据，在我们的例子中，只包含答案，真或假。

## 创建一座桥梁

为了支持外部适配器，执行此任务的节点操作员必须[在他们的节点 UI 中为其创建一个桥](https://docs.chain.link/docs/node-operators#config)，并将适配器的桥名和地址:port(缺省值:8080)添加到他们支持的任务中。

![Chainlink Node Operator New Bridge Page](img/7e42456b45b0b8d0f019392fd7cfaa67.png)

该桥将在指定 URL 提供数据的外部适配器连接到节点，然后节点可以在其作业中利用该数据。在 Chainlink 操作符仪表板的作业页面下，节点操作符以 JSON 格式定义了一系列任务，如下所示:

```
{
  "initiators": [
    { "type": "runLog" }
  ],
  "tasks": [
    { "type": "standarddev" },
    { "type": "ethbool" },
    { "type": "ethtx" }
  ]
}
```

首先我们有运行日志任务。这是一个默认任务，当合同发出请求时，它充当作业的发起者。然后，我们使用我们定义并命名为 `standarddev` 的桥来执行我们的标准偏差计算。由于响应是 Boolean 类型，我们添加了一个 ethbool 任务来处理该响应。最后是 ethtx 任务，它将完成的响应返回给通过该任务的特定 jobID 请求它的智能契约。

这就完成了创建外部适配器和配置 Chainlink 节点以通过桥和作业规范运行它的整个过程。现在，我们准备在智能合同中使用它。

## 提出请求

```
pragma solidity ^0.6.0;

import "@chainlink/contracts/src/v0.6/ChainlinkClient.sol";

contract offchainCalc is ChainlinkClient {

    bool public isGreaterThanHalfSD = false;
    address private oracle;
    bytes32 private jobId;
    uint256 private fee;

    constructor() public {
        setPublicChainlinkToken();
        oracle = 0x8E1da67ca96cECB7DBFab7959655F245c650Eb26;
        jobId = "7d0495356d4946dd8d9921d5003cc12c";
        fee = 1 * 10 ** 18; // 1 LINK;
    }

    //Chainlink request
    function requestStandardDev() public {
        Chainlink.Request memory req = buildChainlinkRequest(jobId, address(this), this.fulfillStandardDev.selector);
        req.add("lat", 35);
        req.add("lon", 139);  
        req.add("copyPath", "answer");
        sendChainlinkRequestTo(oracle, req, fee);
    }

    //Callback function
    function fulfillStandardDev(bytes32 _requestId, bool _isGreaterThanHalfSD) public recordChainlinkFulfillment(_requestId) {
        isGreaterThanHalfSD = _isGreaterThanHalfSD;
        //Perform desired action here based on result 
    }
}
```

这个代码片段就是发出请求并实现请求所需的全部内容。首先，您需要 jobID，它特定于您希望运行的标准差任务以及运行它的 oracle 节点的地址。至于请求本身，一般请求结构中唯一被修改的部分是我们将回调指定为`fulfillStandardDev` 函数，并将两个输入(纬度和经度)和“答案”的复制路径添加到我们的请求中。这告诉节点用 JSON 数据中的应答键来完成请求，因为“应答”是外部适配器对键的命名，它返回 true 或 false。最后，我们在回调函数中将我们的响应保存到我们的 `isGreaterThanHalfSD` 布尔中。此时，我们可以根据结果执行任何所需的操作，例如，当天气条件满足特定的预定义参数(在本例中，天气与过去四天的偏差大于 SD)时，向购买农作物保险的农民发放资金。

## 结论

如您所见，链上代码比外部适配器中的链外代码要简单得多。在链上，我们简单地发送一个请求结构到一个链接节点并接收一个布尔回答，而在链外，有多个加法、减法、除法、指数和平方根的循环。在以这种方式构建我们的智能合约(作为一种混合智能合约)时，我们为用户节省了大量在链上执行计算的气体成本，同时仍保持链上的可审计性和一致性，从而以更高的效率为用户提供更广泛的功能。

如果你是一名开发人员，想要将 Chainlink 集成到你的智能合同应用程序中，请查看 [Chainlink 开发人员文档](https://docs.chain.link/docs)或[点击这里](https://chainlink.typeform.com/to/gEwrPO)。

### 关于这个话题的更多信息

*   [Chainlink 2.0 为采用混合智能合约奠定基础](https://blog.chain.link/chainlink-2-0-lays-foundation-for-adoption-of-hybrid-smart-contracts/)
*   【Chainlink 如何支持任何链外数据资源和计算
*   [构建和使用外部适配器](https://blog.chain.link/build-and-use-external-adapters/)