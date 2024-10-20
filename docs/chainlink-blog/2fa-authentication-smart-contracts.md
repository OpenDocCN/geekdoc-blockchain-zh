# 如何使用 Chainlink 将双因素身份验证(2FA) API 连接到智能合约

> 原文：<https://blog.chain.link/2fa-authentication-smart-contracts/>

[Digital Bridge](https://twitter.com/DigitalBridgeIO/) ，来自[United Hackathon](https://blog.chain.link/showcasing-the-winners-of-the-2020-unitize-hackathon/)的 Chainlink 评委精选奖，使用一个 [Chainlink 外部适配器](https://blog.chain.link/build-and-use-external-adapters/)将一个 2FA API 连接到一个 Chainlink oracle，用于分散验证 2FA PIN 的有效性。他们的 2FA 智能合约是一个很好的例子，说明了 Chainlink 可定制的安全 oracle 基础设施如何用于将链外 API 连接到智能合约，从而实现新的、高度可配置的链内安全工作流。

在这篇文章中， [Digital Bridge](https://twitter.com/DigitalBridgeIO/) 团队 Javier Salomon、Alejandro Pronotti 和 Mateo Hepp 解释了如何将 Chainlink 2FA 适配器集成到以太坊 dApp 中，以便它可以用于许多用例，从保护 DeFi 基金到 KYC 验证。

* * *

*由* [*亚历杭德罗*](http://www.linkedin.com/in/alejandro-pronotti-91667b57)*[*哈维尔【所罗门】*](https://www.linkedin.com/in/javier-salomon/)*[*马特奥*](https://www.linkedin.com/in/mateo-hepp-722978108/)**

 **Chainlink 的[外部适配器功能](https://docs.chain.link/docs/external-adapters)可以轻松地[将智能合约连接到任何 API](https://blog.chain.link/apis-smart-contracts-and-how-to-connect-them/) ，支持智能合约的各种[用例](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/)触发链外事件，并将防篡改数字协议带到外部系统。

对于数字桥技术集成，我们开发了一个 Chainlink 外部适配器来读取离线、高可用性 2FA API 认证服务，并且我们还配置了一个定制的数字桥 Chainlink [oracle](https://chain.link/education/blockchain-oracles) 节点，该节点传递确认 2FA 所需的密码。oracle 可以使用 Amazon AWS Lambda、Google Cloud Platform 函数或 Docker 实现外部适配器。

为了验证持有 2FA 密码的用户，用户提交一个包含其客户 ID 和由他们的验证器应用程序生成的临时一次性密码散列的链上交易。扫描区块链的一个指定的链接节点随后接收这个事务，并查询一个链外服务器(通过 API)来验证 2FA 代码的真实性。一旦 Chainlink 节点接收到响应，它就在链上传递这个布尔值，如果得到授权`TRUE`，则触发[智能契约](https://chain.link/education/smart-contracts)向原始用户授予授权。

这种实现通过使用 PIN 的散列和外部适配器来比较 PIN 和链外身份验证器，避免了中间人攻击。

在这篇技术文章中，我们将讨论:

*   2FA API 用法
*   安装和运行 2FA 外部适配器
*   如何通过网桥和作业规范将此外部适配器连接到 Chainlink 节点
*   如何编写智能合约以通过 Chainlink 节点使用 2FA 外部适配器来验证 2FA PIN 有效性

## 2 使用 API

要调用 2FA API，您可以使用自己定制的 API 或第三方 API，只需对适配器做一些微小的更改。为了便于测试和开发，我们为示例用户提供了一个演示 API，可以使用演示 API 密钥访问它。

2FA 演示 API 允许使用以下“customerid”变量值和 API_KEYs 验证 2FA PIN 的有效性。

演示示例用户

*   `customerid = 'alice' , secretcode = 'VPPRAX5ZS3EAT3ID'`
*   `customerid = 'bob' , secretcode = 'O73Y5FPODOZXHJ4G'`
*   `customerid = 'joe' , secretcode = '6VG5WWIDWHLR3SYE'`

演示授权的 API 密钥

*   `yyTHPaT2n27n3bva9mhX`
*   `sDVRwdc4NXaKP4PZ7CuW`
*   `viaMmedQyaWb2DQeF7dL`

输入参数

JSON 输入的结构如下。

```
 {
  "id": "f82dfad608254bc7a36364f317e47a4d", 
  "data": {
      "customerid": "alice", 
      "hashedpin": "32532605273527"}
}

```

在这个例子中，jobSpec 是`f82dfad608254bc7a36364f317e47a4d`。动作可以是以下任何一种:`customerid`或`hashedpin`。

要计算 **`hashedpin`** 执行以下命令:

### 在 [Python](https://www.python.org/downloads/release/latest) 中(默认，2020 年 7 月 28 日，12:59:40)

```
>>> import datetime
>>> import sha3
>>> PIN = “534204”
>>> int(sha3.keccak_256(PIN.encode('utf-8')).hexdigest()[:12],16)
32532605273527

hashedpin is: 32532605273527
```

下面是另一种使用 JavaScript 计算`hashedpin`的方法，其中安装了 web3 模块。

### 安装了 [web3 模块](https://www.npmjs.com/package/web3)的 JavaScript

```
[email protected]:~/nodejs-web3-project$ node 
Welcome to Node.js v12.20.0.
Type ".help" for more information.
> const Web3 = require('web3');
> var PIN = '534204';
> parseInt(Web3.utils.sha3(PIN).slice(2,14),16);
32532605273527
```

下一步是进行 REST API 调用。

```
curl -H "authorization:Apikey yyTHPaT2n27n3bva9mhX" "https://us-central1-digitalbridge.cloudfunctions.net/TwoFA-chekpin-api?customerid=alice&hashedpin=42646170711749"
```

输出示例

`{"result": true }`

您将收到指示 PIN 是否有效的 true 或 false 值。

## 安装和运行 2FA 外部适配器

我们创建了一个外部适配器，将 Chainlink 节点连接到 2FA API，以利用 Chainlink oracle 对 2FA PIN 有效性进行链上对等验证。

这个外部适配器现在已经在 [Chainlink Market](https://market.link/adapters/1172bf75-c6b6-42cf-8186-48468b44d477) 上列出，可供其他开发者使用、修改或扩展。

一旦你从 [GitHub](https://github.com/digitalbridgekit/2fa-cl-ea) 下载了外部适配器的代码，你可以如下安装并运行它。

## 本地安装

### 要求

*   `yarn`

### 安装依赖项:

`yarn`

### 奔跑

`node -e 'require("./index.js").server()'`

一旦安装完毕，你可以将[外部适配器](https://docs.chain.link/docs/node-operators)添加到你的[链节节点](https://docs.chain.link/docs/node-operator-overview)中，然后创建一个使用它的[工作规范](https://docs.chain.link/docs/job-specifications)。

## 通过桥和作业规范将外部适配器连接到 Chainlink 节点

首先，使用以下数据在 Chainlink 节点中创建桥和作业:

**桥(在这种情况下，我们使用 GCP 云函数)**

```
Name: 2fa-maticmumbai
URL: https://us-central1-digitalbridge.cloudfunctions.net/twofa-adapter

```

**工作规范**

```
{
  "initiators": [
    {
      "type": "runlog",
      "params": {
        "address": "0xa244b30a48559d16078bb151f342d3f12219142f"
      }
    }
  ],
  "tasks": [
    {
      "type": "2fa-maticmumbai",
      "confirmations": null,
      "params": {
      }
    },
    {
      "type": "ethbool",
      "confirmations": null,
      "params": {
      }
    },
    {
      "type": "ethtx",
      "confirmations": null,
      "params": {
      }
    }
  ],
  "startAt": null,
  "endAt": null
}
```

在作业规范中，`initiator`是触发或启动作业的东西。在这种情况下，启动器被设置为`RunLog`，这意味着当 Oracle 契约在`0xa244b30a48559d16078bb151f342d3f12219142f.`发出`OracleRequest`事件时，节点将触发此作业运行。这是我们之前部署的 Oracle 契约，对于您向其发出请求的任何一个 Chainlink 节点都是唯一的。

然后我们的请求将由适配器按照它们被定义的顺序进行处理:

1.  创建桥类型请求。这个桥将从客户端智能契约中给出`customerid`和`hashedpin`参数，然后执行对外部 API 的请求。响应通过管道传输到下一个任务。
2.  将结果解析到 JSON，并获取客户机契约作为请求参数给出的路径中定义的值。
3.  将字符串类型的结果值转换为以太坊布尔类型的值。
4.  将结果作为事务处理。

如果想测试适配器，可以使用这个`curl`命令，但是需要用部署 oracle smart contract 和创建作业时获得的值替换`jobid`和`Oracle address`。

**智能合约参数**

```
Jobid: f82dfad608254bc7a36364f317e47a4d
Oracle Address: 0xA244B30a48559d16078BB151f342d3f12219142F
```

**测试适配器的命令**

```
curl -X POST  -H 'Content-Type: application/json' -d '{"id": "f82dfad608254bc7a36364f317e47a4d", "data": {"customerid": "alice", "hashedpin": "74856005982787"}}' "https://us-central1-digitalbridge.cloudfunctions.net/twofa-adapter"
```

**响应**

```
{
  "jobRunID":"f82dfad608254bc7a36364f317e47a4d",
  "data":{"result":true},
  "result":true,
  "statusCode":200
}
```

## 使用智能合约验证 2FA PIN 的有效性

现在我们正在运行一个外部适配器，我们已经将它添加到 Chainlink 节点作业规范中，并且我们已经添加了一个桥。最后，我们需要一个智能契约客户端来消费这些数据。

第一步是创建一个新的 API 消费者契约，设置所有必需的参数。

您应该在合同中创建两个函数:`requestGAPINCheck`和`fulfillGAPINCheck`，如下例所示。调用`requestGAPINCheck`函数与 2FA API 服务进行交互。

`requestGAPINCheck`函数接受客户 ID 和散列 PIN 作为参数。这应该是前面 2FA 外部适配器一节中提到的第一个作业规范的 ID。我们将链接支付金额设置为 0.1 链接。这是我们的 Solidity 示例，它通过我们的 Chainlink oracle 发出 HTTP POST 请求。

```
function requestGAPINCheck(string memory _customerId, int256 _hashedpin)
    public
  {
    Chainlink.Request memory req = buildChainlinkRequest(JOBID, address(this), this.fulfillGAPINCheck.selector);

    req.add("customerid", _customerId);
    req.addInt("hashedpin", _hashedpin);
    req.add("path","result");

    sendChainlinkRequestTo(ORACLE_ADDRESS, req, 0.1 * 1 ether);
  }
```

`JOBID`是我们`buildChainlinkRequest`的第一个参数。第二个参数是契约返回数据的地址，也称为`callbackaddress`。最后一个参数是收集数据后处理数据的函数，也就是“回调函数签名”。我们想将数据返回到这个契约，所以我们放入`address(this)`，我们将处理数据的函数将被实现。

如果 PIN 有效，契约将返回一条成功消息和一个包含布尔值的 JSON 对象:

```
{
    "result": true
}
```

该响应数据将被返回到`requestGAPINCheck function`，如`Chainlink.Request`字段中所指定的，在此我们可以手动添加所需的动作:

```
function fulfillGAPINCheck(bytes32 _requestId, bool _allowed)
    public
    recordChainlinkFulfillment(_requestId)
  {
    currentPermission = _allowed;
    emit RequestGAPINCheckFulfilled(_requestId, currentPermission);
    if (currentPermission) {
        //*********************************************************************
        // TO DO THE SPECIAL ACTION
        //*********************************************************************
        //currentPermission = false;
    }
  }

```

布尔参数`type _allowed`是 Chainlink 节点输入从 HTTP POST 请求中收集的 2FA 授权的地方。让我们回顾一下每个适配器的功能:

`bridge`

Chainlink 节点将发出 HTTP POST 请求。
我们希望在参数中发出的 HTTP POST 请求被传递给 req 变量。该变量在 requestGAPINCheck 函数中作为智能合约代码的一部分被赋值(您可以在本节的上面看到)。

`eq.add("customerid", _customerId);
req.addInt("hashedpin", _hashedpin);`

`jsonparse`

一旦节点发出 HTTP POST 请求，它将遍历 JSON 并只找到我们想要的值。存储 HTTP POST 请求的全部返回将非常昂贵，因为你在以太坊区块链上存储的越多，你必须支付的汽油费就越多。所以，我们想尽量少退货。

`req.add("path", "result");`

这将从返回值(`{“result”:true}`)的 JSON 中将 HTTP POST 请求的返回压缩为值`true`。

`ethbool`

您会注意到，在上面的代码中，我们没有向这个适配器传递任何参数；那是因为我们不需要。这个适配器只是将我们的答案`true`转换成可靠可读的格式。

`ethtx`

这个也不需要任何参数。这是使用`sendChainlinkRequestTo`方法将数据发送回链上的适配器。

上述合同的完整工作版本可在 [GitHub](https://github.com/digitalbridgekit/2fa-for-smartcontracts-matic/blob/master/contract/GAPINCheck-mumbai-maticnetwork.sol) 上获得。这个实现目前连接到一个演示 2FA API 服务器，用于开发和测试。要将其修改为生产环境并连接到实际的 2FA 服务，我们需要将作业规范更新为运行在指向活动的 2FA 生产服务器的 2FA 外部适配器上的规范。

如果您需要关于外部适配器的更多技术细节，可以在 [market.link](https://market.link/adapters/1172bf75-c6b6-42cf-8186-48468b44d477) 上查看。

## 摘要

使用 [Chainlink Network](https://chain.link/) 及其多功能外部适配器功能，我们展示了如何将智能合约与 2FA 服务集成。它的集成为用户在智能合约中提供了额外的安全层，同时只使用链上的散列数据。

该演示展示了智能合同和服务集成的许多有趣的潜在使用案例，这些案例可能需要 2FA 作为管理敏感数据的公司的额外安全层。

### 了解更多信息

如果您是一名开发人员，并且希望将您的智能合约连接到底层区块链之外的现有数据和基础设施，请联系此处的[或访问](https://chainlink.typeform.com/to/gEwrPO) [Chainlink 开发人员文档](https://docs.chain.link/)。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink) | [不和](https://discordapp.com/invite/aSK4zew)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://data.chain.link/) | [DeFi](https://defi.chain.link/)**