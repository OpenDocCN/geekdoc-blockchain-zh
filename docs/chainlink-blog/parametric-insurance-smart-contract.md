# 如何构建参数化保险智能合约

> 原文：<https://blog.chain.link/parametric-insurance-smart-contract/>

区块链技术提供了独特的属性，可用于创建创新的[去中心化保险产品](https://blog.chain.link/blockchain-insurance/)，为保险提供商及其客户带来诸多好处。在本技术教程中，我们将向您展示:

*   分散参数保险合同的主要特征
*   为什么 Chainlink [神谕](https://chain.link/education/blockchain-oracles)在这些新的保险产品中发挥着关键作用
*   在分散保险合同中使用链式价格馈送的优势。
*   如何把所有的东西放在一起，创造一个可行的参数作物保险合同。
*   如何使用 Chainlink 节点自动更新保险合同。

下面例子的完整代码可以在 Remix 或 [GitHub](https://github.com/pappas999/Parametric-Crop-Insurance) 上查看，包括下面提到的所有功能以及所有需要的帮助功能。

## 分散保险

分散保险涉及使用区块链技术和智能合同来取代传统的保险协议。分散式保险产品有三个突出的主要特征:

### 数据驱动的自动化

分散式保险合同最重要的方面是它们是数据驱动的和自动执行的。这意味着保险合同自动执行逻辑而不需要人工干预，并且依赖于从外部来源获得的安全和准确的数据来确定合同逻辑的执行。这些保险智能合同还可以连接到外部输出，如支付处理器或企业财务系统，以促进支付的触发。

### 智能合同

[智能合同](https://chain.link/education/smart-contracts)代表保险公司和客户之间的保险合同，本质上是保险公司对客户特定类型的损失、损害或责任进行赔偿的承诺，或者在参数保险的情况下，对特定事件发生的风险进行对冲。它包含保险合同的所有详细信息，例如指数(例如作物保险合同中的降雨量)、支付的客户详细信息(例如钱包地址或外部支付系统的客户 ID)、合同日期或持续时间、指数将在哪里测量、阈值和约定的支付值。因为保险合同是在通常运行在大量节点上的区块链上存储和执行的，所以它具有很高的确定性，不容易被黑客攻击或篡改。

### 索赔流程

与传统的保险合同不同，在分散的保险合同中，索赔过程是作为合同执行的一部分自动处理的。客户不需要提交索赔，不需要提供任何证据，也不需要与保险公司或智能合同进行任何交互。当智能合同认为应该发生支付时，支付作为合同执行的一部分被自动触发。这可以通过直接向客户支付的链上支付来完成，但也可以通过智能合约连接的外部支付轨道或金融系统来完成。

## 创建数据驱动的参数化保险合同

既然我们已经理解了分散参数保险契约的组成，我们将构建一个简单的例子来演示上述三个概念。在这种情况下，我们将创建一个具有以下属性的参数作物保险合同:

*   如果在指定的时间内该地点没有降雨，合同将向客户支付约定的价值，目前设定为三天，以便于演示。该合同将从两个不同的数据源获取降雨数据，以缓解任何数据完整性问题，然后对结果进行平均。
*   该合同将由与商定支付金额的美元价值相等的 ETH 全额资助，以确保在索赔被触发时的完全确定性。它将使用 Chainlink [ETH/USD 价格馈送](https://feeds.chain.link/eth-usd)来确定合同要求的 ETH 数量。



![Decentralized Insurance architecture](img/b00e9dfb7f281f91b5aed5b0b6c8fd73.png)

<figcaption id="caption-attachment-583" class="wp-caption-text">分散保险架构</figcaption>





### 建立保险合同工厂

首先，我们需要创建一个主“合同工厂”合同，它将生成多个保险协议，并允许我们与它们进行交互。该合同将由保险公司所有，并将为每个生成的保险合同提供足够的 ETH 和链接，以确保一旦生成，保险合同可以在其整个持续时间内执行所需的所有操作，包括支付。

首先，我们的 Solidity 代码包含两个契约，一个保险供应商契约和一个保险合同契约。保险供应商合同产生许多保险合同。

InsuranceProvider 合同的构造者在 Kovan 网络上初始化 Chainlink [ETH/USD 价格馈送](https://feeds.chain.link/eth-usd)。保险合同的构造者已经在下面定义了，但是将在后面充实。

```
pragma solidity 0.4.24;
pragma experimental ABIEncoderV2;

//Truffle Imports
import "chainlink/contracts/ChainlinkClient.sol";
import "chainlink/contracts/vendor/Ownable.sol";
import "chainlink/contracts/interfaces/LinkTokenInterface.sol";

contract InsuranceProvider {
    constructor() public payable {
        priceFeed = AggregatorV3Interface(0x9326BFA02ADD2366b30bacB125260Af641031331);
    }
}

contract InsuranceContract is ChainlinkClient, Ownable  {
    constructor(address _client, uint _duration, uint _premium, uint _payoutValue, string _cropLocation, address _link, uint256 _oraclePaymentAmount)  payable Ownable() public { 
    }
}
```

保险供应商合同的一般结构如下:

*   每个生成的合同都存储在保险合同的“合同”映射中，生成的合同以太坊地址是密钥。该值是实例化的保险合同可靠性智能合同。

```
//here is where all the insurance contracts are stored.
mapping (address => InsuranceContract) contracts;
```

*   “newContract”函数接受所需的输入并生成一个新的 InsuranceContract 契约，按照前面定义的构造函数传递所有所需的细节。它还发送与支付值相等的正确的 ETH 金额，以便为生成的合同提供全部资金。它使用 Chainlink [ETH/USD 价格馈送](https://feeds.chain.link/eth-usd)进行转换。然后，它将生成的契约存储在“契约”映射中，并将足够的链接传输到生成的契约，这样，它就有足够的链接来处理每天两次的数据请求，外加一个小的缓冲区。这个小缓冲区是为了解决合同到期后可能需要额外调用的时间问题。合同结束时留下的任何链接都将返还给保险提供商。

```
function newContract
(
    address _client,
    uint _duration,
    uint _premium,
    uint _payoutValue,
    string _cropLocation
) 
    public payable onlyOwner() returns(address)
{
    //create contract, send payout amount so contract is fully funded plus a small buffer
    InsuranceContract i = (new InsuranceContract).value((_payoutValue * 1 ether).div(uint(getLatestPrice())))(_client, _duration, _premium, _payoutValue, _cropLocation, LINK_KOVAN,ORACLE_PAYMENT);

    contracts[address(i)] = i;  //store insurance contract in contracts Map

    //emit an event to say the contract has been created and funded
    emit contractCreated(address(i), msg.value, _payoutValue);

    //now that contract has been created, we need to fund it with enough LINK tokens to fulfil 1 Oracle request per day, with a small buffer added
    LinkTokenInterface link = LinkTokenInterface(i.getChainlinkToken());
    link.transfer(address(i), ((_duration.div(DAY_IN_SECONDS)) + 2) * ORACLE_PAYMENT.mul(2));

    return address(i);
}
```

*   “更新合同”功能用于更新保险合同的数据，并检查是否达到了触发付款的阈值，或者合同是否已到达终止日期。

```
function updateContract(address _contract) external {
    InsuranceContract i = InsuranceContract(_contract);
    i.updateContract();
}
```

*   最后,“getContractRainfall”函数用于返回给定保险合同的降雨量(以毫米为单位),“getContractRequestCount”函数用于查看有多少数据请求成功返回到保险合同。

```
function getContractRainfall(address _contract) external view returns(uint) {
    InsuranceContract i = InsuranceContract(_contract);
    return i.getCurrentRainfall();
}

function getContractRequestCount(address _contract) external view returns(uint) {
    InsuranceContract i = InsuranceContract(_contract);
    return i.getRequestCount();
}

```

### 获取外部数据

生成的保险合同需要获得外部数据才能正确执行。这就是 Chainlink 网络发挥作用的地方，因为您可以使用它将保险合同连接到多个降雨数据来源。在本例中，我们将在两个不同的 Chainlink 节点上使用[作业规范](https://docs.chain.link/docs/job-specifications)，这两个节点从两个不同的 weather APIs 获取数据，然后我们将创建链上值的平均值，以得出最终结果。这两个天气 API 都需要注册来获得一个免费的 API 密钥，以便在每个请求中使用。

*   [韦瑟比特天气 API](https://www.weatherbit.io/api)
*   [OpenWeather API](https://openweathermap.org/)
*   [链接库获取> Uint256 作业](https://market.link/jobs/c17a49d6-8d88-4ff9-b27a-bd3d46d7efb9)
*   [Steelblock 得到> Uint256 工作](https://market.link/jobs/1a310839-7d94-49a0-a98a-e46fb2fb31e5)

一旦我们记下了天气 API 键以及作业规范 id 和上面的 oracle contracts，我们现在就可以创建“InsuranceContract”合同，填充必需的常量字段。在生产场景中，这些将被私有地存储在 Chainlink 节点上，在链上是不可见的，但是为了便于跟随演示，它们被保留在契约中。我们还存储了需要遍历的 JSON 路径，以便在 Chainlink 节点从每个 API 获取天气数据时找到以毫米为单位的日总降雨量。

```
string constant WORLD_WEATHER_ONLINE_URL = "http://api.worldweatheronline.com/premium/v1/weather.ashx?";
string constant WORLD_WEATHER_ONLINE_KEY = "insert API key here";
string constant WORLD_WEATHER_ONLINE_PATH = "data.current_condition.0.precipMM";

string constant WEATHERBIT_URL = "https://api.weatherbit.io/v2.0/current?";
string constant WEATHERBIT_KEY = "insert API key here";
string constant WEATHERBIT_PATH = "data.0.precip";
```

### 完成保险合同

下一步是完成代表客户和保险公司之间的作物保险合同的保险合同。

使用传递给构造函数的所有必需值来实例化协定。它还执行以下操作:

*   使用 chain link[ETH/USD Price Feed](https://feeds.chain.link/eth-usd)检查合同中是否发送了足够的 ETH，以确保在触发支付时资金充足。
*   设置合同执行所需的一些变量
*   将 JobId 和 oracle 数组设置为包含从上述“获取外部数据”部分的两个作业规范中获取的值。但是，如果您想[运行您自己的 Chainlink 节点](https://blog.chain.link/running-a-chainlink-node-for-the-first-time/)以便查看每个作业的输出，您可以设置两个请求使用您的作业规范和 oracle contract。如果您沿着这条路走下去，您需要在 [market.link](https://market.link/jobs/c17a49d6-8d88-4ff9-b27a-bd3d46d7efb9/spec) 上创建一个与此示例相同的新作业规范，并修改运行日志启动器中的地址，使其成为您的 oracle 合同。

```
constructor
(
    address _client,
    uint _duration,
    uint _premium,
    uint _payoutValue,
    string _cropLocation, 
    address _link,
    uint256 _oraclePaymentAmount
)
    payable Ownable() public
{
    priceFeed = AggregatorV3Interface(0x9326BFA02ADD2366b30bacB125260Af641031331);

    //initialize variables required for Chainlink Node interaction
    setChainlinkToken(_link);
    oraclePaymentAmount = _oraclePaymentAmount;

    //first ensure insurer has fully funded the contract
    require(msg.value >= _payoutValue.div(uint(getLatestPrice())), "Not enough funds sent to contract");

    //now initialize values for the contract
    insurer= msg.sender;
    client = _client;
    startDate = now + DAY_IN_SECONDS; //contract will be effective from the next day
    duration = _duration;
    premium = _premium;
    payoutValue = _payoutValue;
    daysWithoutRain = 0;
    contractActive = true;
    cropLocation = _cropLocation;

    //if you have your own node and job setup you can use it for both requests
    oracles[0] = 0x05c8fadf1798437c143683e665800d58a42b6e19;
    oracles[1] = 0x05c8fadf1798437c143683e665800d58a42b6e19;
    jobIds[0] = 'a17e8fbf4cbf46eeb79e04b3eb864a4e';
    jobIds[1] = 'a17e8fbf4cbf46eeb79e04b3eb864a4e';

    emit contractCreated(
        insurer,
        client,
        duration,
        premium,
        payoutValue);
}
```

然后，我们创建一个函数来构建调用，从每个 Chainlink 节点和 weather API 请求降雨量数据。该函数由主保险供应商合同调用。它为每个请求建立所需的 URL，然后为每个请求调用“checkRainfall”函数。但在此之前，它会调用一个“checkEndContract”函数来检查是否已经到达合同结束日期，并且只有在合同仍然有效的情况下才会继续。这个“checkEndContract”函数将在下面进一步定义。

```
function updateContract() public onContractActive() returns (bytes32 requestId) {
    //first call end contract in case of insurance contract duration expiring, if it hasn't then this function execution will resume
    checkEndContract();

    //contract may have been marked inactive above, only do request if needed
    if (contractActive) {
        dataRequestsSent = 0;
        //First build up a request to World Weather Online to get the current rainfall
        string memory url = string(abi.encodePacked(WORLD_WEATHER_ONLINE_URL, "key=",WORLD_WEATHER_ONLINE_KEY,"&q=",cropLocation,"&format=json&num_of_days=1"));
        checkRainfall(oracles[0], jobIds[0], url, WORLD_WEATHER_ONLINE_PATH);

        // Now build up the second request to WeatherBit
        url = string(abi.encodePacked(WEATHERBIT_URL, "city=",cropLocation,"&key=",WEATHERBIT_KEY));
        checkRainfall(oracles[1], jobIds[1], url, WEATHERBIT_PATH);    
    }
}
```

我们现在可以创建“checkRainfall”函数。这是实际执行外部数据请求的函数。它接受所有需要的参数，建立一个请求，然后将它发送到指定的链接节点 oracle contract。

在我们的演示中，传递给‘check rain’函数的 _path 变量值用于遍历请求返回的 JSON 路径，以找到当前的降雨量。这些值取决于正在调用的天气 API，这两个选项都存储在我们的契约中的静态变量中，并根据需要传递给 *_path* 函数参数。

*   [世界天气在线 API 响应格式](https://www.worldweatheronline.com/developer/api/docs/local-city-town-weather-api.aspx)
*   [Weatherbit API 响应格式](https://www.weatherbit.io/api/weather-current)

```
string constant WORLD_WEATHER_ONLINE_PATH = "data.current_condition.0.precipMM";
string constant WEATHERBIT_PATH = "data.0.precip";

function checkRainfall(address _oracle, bytes32 _jobId, string _url, string _path) private onContractActive() returns (bytes32 requestId) {
    //First build up a request to get the current rainfall
    Chainlink.Request memory req = buildChainlinkRequest(_jobId, address(this), this.checkRainfallCallBack.selector);

    req.add("get", _url); //sends the GET request to the oracle
    req.add("path", _path);
    req.addInt("times", 100);

    requestId = sendChainlinkRequestTo(_oracle, req, oraclePaymentAmount); 

    emit dataRequestSent(requestId);
}
```

然后，我们创建一个回调函数，当 Chainlink 节点发回响应时调用这个函数。该函数接收指定位置的更新降雨量数据，如果是第二次数据更新，则执行平均(即，两个响应中的两个已返回)，然后用最新的降雨量数据更新合同。

回调函数还检查是否基于当前合同降雨量数据实现了参数化损失。在这种情况下，它根据给定的阈值检查连续无雨的天数。如果满足支付条件，则调用“payoutContract”函数。

```
function checkRainfallCallBack(bytes32 _requestId, uint256 _rainfall) public recordChainlinkFulfillment(_requestId) onContractActive() callFrequencyOncePerDay() {
    //set current temperature to value returned from Oracle, and store date this was retrieved (to avoid spam and gaming the contract)
    currentRainfallList[dataRequestsSent] = _rainfall; 
    dataRequestsSent = dataRequestsSent + 1;

    //set current rainfall to average of both values
    if (dataRequestsSent > 1) {
        currentRainfall = (currentRainfallList[0].add(currentRainfallList[1]).div(2));
        currentRainfallDateChecked = now;
        requestCount +=1;

        //check if payout conditions have been met, if so call payoutcontract, which should also end/kill contract at the end
        if (currentRainfall == 0 ) { //temp threshold has been  met, add a day of over threshold
            daysWithoutRain += 1;
        } else {
            //there was rain today, so reset daysWithoutRain parameter 
            daysWithoutRain = 0;
            emit ranfallThresholdReset(currentRainfall);
        }

        if (daysWithoutRain >= DROUGHT_DAYS_THRESDHOLD) {  // day threshold has been met
            //need to pay client out insurance amount
            payOutContract();
        }
    }

     emit dataReceived(_rainfall);
}
```

接下来，我们创建 payoutContract 函数。该功能充当索赔处理步骤，并执行保险公司向客户自动支付商定的价值。我们在这里特别小心，确保它只能在契约仍处于活动状态(即未结束)时被调用，并且只能由其他契约函数在内部调用。它还将任何剩余的链接返回给保险提供商主合同，并将合同设置为完成状态，以防止对其执行任何进一步的操作。

```
function payOutContract() private onContractActive()  {
    //Transfer agreed amount to client
    client.transfer(address(this).balance);

    //Transfer any remaining funds (premium) back to Insurer
    LinkTokenInterface link = LinkTokenInterface(chainlinkTokenAddress());
    require(link.transfer(insurer, link.balanceOf(address(this))), "Unable to transfer");

    emit contractPaidOut(now, payoutValue, currentRainfall);

    //now that amount has been transferred, can end the contract 
    //mark contract as ended, so no future calls can be done
    contractActive = false;
    contractPaid = true;
}
```

最后，我们创建一个函数来处理这样的场景:合同结束日期已到，但付款尚未触发，我们需要返回合同中的资金，然后将其标记为结束。该函数执行一项检查，查看协定在整个协定期间是否收到了足够的数据请求。每天需要一个数据请求，只允许错过一个请求。因此，如果契约的持续时间为 30 天，则必须至少有 29 个成功的数据请求。如果合同在其生命周期内收到足够多的请求，所有的资金都将返还给保险提供商。否则，如果在整个合同期限内没有足够的数据请求，客户将自动收到他们的保险费退款，保险提供商将获得任何剩余资金。

该场景还利用 Chainlink [ETH/USD 价格馈送](https://feeds.chain.link/eth-usd)来确定要发送回客户的正确 ETH 数量。这种检查为客户提供了某种程度的保证，即保险提供商不会试图通过在结束日期到来之前不更新降雨量数据来欺骗合同。该函数还将把任何剩余的链接返回给 InsuranceProvider 契约。

```
function checkEndContract() private onContractEnded()   {
    //Insurer needs to have performed at least 1 weather call per day to be eligible to retrieve funds back.
    //We will allow for 1 missed weather call to account for unexpected issues on a given day.
    if (requestCount >= (duration.div(DAY_IN_SECONDS) - 1)) {
        //return funds back to insurance provider then end/kill the contract
        insurer.transfer(address(this).balance);
    } else { //insurer hasn't done the minimum number of data requests, client is eligible to receive his premium back
        client.transfer(premium.div(uint(getLatestPrice())));
        insurer.transfer(address(this).balance);
    }

    //transfer any remaining LINK tokens back to the insurer
    LinkTokenInterface link = LinkTokenInterface(chainlinkTokenAddress());
    require(link.transfer(insurer, link.balanceOf(address(this))), "Unable to transfer remaining LINK tokens");

    //mark contract as ended, so no future state changes can occur on the contract
    contractActive = false;
    emit contractEnded(now, address(this).balance);
}
```

## 部署和测试合同

首先，我们需要部署 InsuranceProvider 契约，并为它提供一些 ETH 和 LINK，以便在生成的 InsuranceContract 契约中使用。

一旦完成了这些，我们就可以创建一个新的 InsuranceContract，并传入所需的值。请注意以下几点:

*   持续时间以秒为单位。在本演示中，1 天被缩短为 60 秒(在 DAY_IN_SECONDS 常量中指定)，因此 300 秒的合同持续时间代表 5 天。
*   premium 和 payoutValue 参数以美元为单位，乘以 100000000，例如 100 美元就是 1000000000



![Creating a new insurance contract](img/3fd4ff96071c906af3a328df01f450ab.png)

<figcaption id="caption-attachment-580" class="wp-caption-text">创建新的保险合同</figcaption>





一旦保险合同生成，我们就可以通过 [Etherscan](https://kovan.etherscan.io/) 中的事务或通过事务输出获得它的地址。



![Viewing the generated contract on Etherscan](img/54a14dfe4d85a0eb91eab529d7c639bb.png)

<figcaption id="caption-attachment-589" class="wp-caption-text">在以太网上查看生成的合同</figcaption>





然后，我们可以获取生成的合同地址，并将其传递给“updateContract”函数，以开始将降雨量数据纳入合同的过程:



![Updating the insurance contract](img/0697c430104fb38b11e713690355dd8d.png)

<figcaption id="caption-attachment-587" class="wp-caption-text">更新保险合同</figcaption>





一旦两个 Chainlink 节点都处理了作业请求并返回结果，我们就可以调用“getContractRainfall”和“getContractRequestCount”函数来查看更新的平均降雨量和增加的数据请求计数。一个数据请求意味着两个节点都返回一个结果，该结果被平均并存储在契约中。在这种情况下，两个数据馈送中爱荷华州当前的平均降雨量为 0.6 毫米。我们还可以调用帮助函数“getContractStatus”来验证合同是否仍处于活动状态。



![Getting the status of the insurance contract](img/864a4155e277e83041509da62056d184.png)

<figcaption id="caption-attachment-585" class="wp-caption-text">取得保险合同的状态</figcaption>





在合同持续时间内(本演示中为 5 次/300 秒),该步骤应每天重复一次(在本例中为 1 分钟),以结束合同。如果无雨天数达到干旱天数阈值中设置的阈值，合同将向客户支付约定的金额，合同状态将结束。

为了演示的目的，我们为一个没有降雨的地点创建了另一个保险合同，并在三分钟内重复上述步骤三次，以演示在发生赔付时会发生什么。在这种情况下，我们可以看到最近的降雨量为 0，请求计数为 3，合同不再处于活动状态。



![Getting the status of the insurance contract](img/c6df31659e32c82be25c5735235a1b81.png)

<figcaption id="caption-attachment-586" class="wp-caption-text">取得保险合同的状态</figcaption>





如果我们在 Etherscan 上检查合同，我们将看到 ETH 中的约定美元支付值已被转移回上面创建合同时指定的客户钱包地址，并且保险合同不再持有任何 ETH 或链接。对保险合同的任何后续操作都将被拒绝，因为它现在处于完成状态。



![Verifying the insurance contracts payments](img/51b503bbddd3a4b0cc3e2c848c0fb5c4.png)

<figcaption id="caption-attachment-588" class="wp-caption-text">核实保险合同款项</figcaption>





### 自动更新数据

对于当前版本的合同，必须有人手动调用“updateContract”函数来使合同与 Chainlink 节点通信并获得降雨量数据。这并不理想，因为它需要在整个合同期间发生多次。自动化的一个好方法是利用链接节点 [cron 启动器。](https://docs.chain.link/docs/initiators#cron)

cron 启动器是一种使用简单的 [cron 语法](https://en.wikipedia.org/wiki/Cron)在 Chainlink 节点上调度重复作业的方法。在这种情况下，我们可以在 Chainlink 节点上创建一个新的作业规范，它使用 Cron 启动器每天触发一次作业规范。但是为了这个演示的目的，我们将它设置为每分钟触发一次，就像前面提到的每天持续的秒数一样。

每当 Cron 作业触发作业规范的执行时，作业规范的剩余部分将简单地调用部署的智能契约‘update contract’函数。这个想法是，保险前端将拥有所有相关的细节(合同地址、开始日期、结束日期)，并可以将它们传入。

```
{
   "initiators": [
      {
         "type": "cron",
         "params": {
            "schedule": "CRON_TZ=UTC 0/' + 6 + ' * * * * *"
         }
      }
   ],
   "tasks": [
      {
         "type": "ethtx",
         "confirmations": 0,
         "params": {
            "address": "' + address + '",
            "functionSelector": "checkContract()"
         }
      }
   ],
   "startAt": "' + startDate + '",
   "endAt": "' + endDate + '"
}
```

不需要通过 Chainlink 节点前端接口手动创建该工作规范，其思想是分散式保险应用前端将向 [Chainlink 节点 API](https://docs.chain.link/reference#specs) 发送请求，以动态生成新的工作规范，该工作规范具有节点自动开始定期更新保险合同所需的所有正确细节。

为此，首先我们需要 Chainlink 节点的 IP 地址和端口，以及登录到该节点的用户名和密码。这些用于为下一个请求生成一个 cookiefile。

```
curl -c cookiefile -X POST -H 'Content-Type: application/json' -d '{"email":"[email protected]", "password":"password"}' http://35.189.58.211:6688/sessions
```

完成后，我们应该会得到一个响应，表明身份验证已经成功。

```
{"data":{"type":"session","id":"sessionID","attributes":{"authenticated":true}}}
```

然后，我们可以向 Chainlink 节点 API 发送另一个请求，这次是向 [/v2/specs](https://docs.chain.link/reference#specs) 端点发送。请求中的 JSON 应该包含您希望定期更新的生成的保险合同的地址，以及开始和结束日期/时间(如果需要，可以有指定的时间偏移),以便节点知道何时停止定期更新保险合同。

```
curl  -b cookiefile -X POST -H 'Content-Type: application/json' -d '{"initiators":[{"type":"cron","params":{"schedule":"CRON_TZ=UTC 0/60 * * * * *"}}],"tasks":[{"type":"ethtx","confirmations":0,"params":{"address":"0xdC71C577A67058fE1fF4Df8654291e00deC28Fbf","functionSelector":"updateContract()"}}],"startAt": "2020-11-10T15:37:00+10:30","endAt": "2020-11-10T15:42:00+10:30"}' http://35.189.58.211:6688/v2/specs
```

这将向注释行返回一条成功消息，其中包含生成的作业规范的详细信息。在此之后，您应该能够登录到 Chainlink 节点前端，并看到新创建的作业规范。



![Cron initiator job specification syntax](img/12436bc143942186eeb4cb188dcbb694.png)

<figcaption id="caption-attachment-582" class="wp-caption-text">Cron 启动器作业规范语法</figcaption>





一旦创建了作业规范，它应该很快就会按照 cron 启动器中设置的参数开始执行请求。我们可以在 Chainlink 节点前端对此进行监控。



![Once the node has successfully completed some requests, we can then go back to the smart contract and see its state has been successfully updated.](img/a78f5615fb806c8aa94d936bf6226074.png)

<figcaption id="caption-attachment-581" class="wp-caption-text">一旦节点成功完成了一些请求，我们就可以返回到智能合同，并看到它的状态已被成功更新。</figcaption>







![Getting the status of the insurance contract](img/23037757c831fa3ad2aafbc0434666f7.png)

<figcaption id="caption-attachment-584" class="wp-caption-text">取得保险合同的状态</figcaption>





## 摘要

在这篇技术文章中，我们展示了如何建立一个分散的农作物保险产品来补偿农民一段时间的无雨。我们已经展示了保险合同拥有准确和分散的数据的重要性，以及 Chainlink oracles 在安全地提供这些数据方面所扮演的角色。

我们还展示了如何利用连接到外部数据和事件的确定性智能合同来完全最小化处理保险索赔的开销和管理成本，以及如何使用 [Chainlink 分散价格馈送](https://feeds.chain.link/)在合同条款以美元为基础但支付以加密货币为基础的情况下准确确定正确的支付金额。最后，我们还演示了如何将 Chainlink 节点 [cron 启动器](https://docs.chain.link/docs/initiators#cron)与 [Chainlink 节点 API](https://docs.chain.link/reference) 结合使用，以自动调度和执行智能合同更新。

虽然此演示包含许多功能，但它可以用作构建完整且功能丰富的分散式保险产品的基本模板。开发人员可以以各种方式在这个模板上进行构建，比如去除手动数据聚合，利用 Chainlink 的[聚合器](https://github.com/smartcontractkit/chainlink/blob/develop/evm-contracts/src/v0.4/Aggregator.sol)或[预协调器](https://github.com/smartcontractkit/chainlink/blob/develop/evm-contracts/src/v0.6/PreCoordinator.sol)契约。另一个选择是将保险合同证券化，并在 [DeFi 生态系统](https://blog.chain.link/analyzing-the-defi-ecosystem-and-the-many-ways-chainlink-can-accelerate-adoption/)或其他市场中用作抵押品。

如果你是一名开发人员，并希望将你的智能合同连接到链外数据和系统，请访问[开发人员文档](https://docs.chain.link/)，并加入关于[不和谐](https://discordapp.com/invite/aSK4zew)的技术讨论。如果您想安排一次电话会议来更深入地讨论整合事宜，请点击此处的。