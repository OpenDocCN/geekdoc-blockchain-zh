# 将智能合约连接到 Twitter API

> 原文：<https://blog.chain.link/connect-smart-contract-to-twitter-api/>

像 Twitter 这样的社交媒体平台拥有丰富的数据，可以显示全球各地的人们认为重要和值得讨论的内容。我们正在进入一个越来越受这种数据驱动的世界，Chainlink 提供了将这种庞大的数据集安全连接到链上世界的机会，将[智能合同](https://chain.link/education/smart-contracts)的可靠性和透明度保证带到了我们的社交媒体生活中。

在本演练中，我们将介绍如何将您的智能合约连接到 [Twitter API](https://developer.twitter.com/en/docs) 。具体来说，我们将解释如何从智能合约中触发推文，但围绕社交媒体数据进行数据分析和智能合约执行的可能性数不胜数。

## 构造器

```
pragma solidity ^0.6.12;

import "https://github.com/smartcontractkit/chainlink/evm-contracts/src/v0.6/ChainlinkClient.sol";

contract ChainlinkTwitter is ChainlinkClient {
    address private oracle;
    bytes32 private jobId;
    uint256 private fee;
    uint256 public statusCode;

    //only the contract owner should be able to tweet
    address payable owner;
    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }

    constructor() public {
    	setPublicChainlinkToken();
    	oracle = 0x4CF0507fe3236DedDbE6cD18508f35D9b5e16e7C; // oracle address
    	jobId = "948db03c9576480a8fa0545bee5b28ab"; //job id
    	fee = 11 * 10 ** 17; // 1.1 LINK
    	owner = msg.sender;
    }
```

我们从熟悉的 ChainlinkClient 导入和继承开始。导入 ChainlinkClient 契约公开了形成请求、将请求提交给一个或多个 Chainlink 节点以及接收应答所需的所有函数。只需定义您选择的 oracle 地址、该节点为其 Twitter 作业提供的作业规范 ID，并定义该节点处理请求所需的费用。此外，我们定义了 onlyOwner 修饰符，以便只有合同创建地址能够通过该合同发布 tweet。

## 推特功能

```
//tweets the supplied string
function tweet(string memory twt) public onlyOwner{
    Chainlink.Request memory req = buildChainlinkRequest(jobId, address(this), this.fulfill.selector);
    //req.add("endpoint", "https://api.twitter.com/1.1/statuses/update.json");
    req.add("status", twt);
    req.add("copyPath", "statusCode")
    sendChainlinkRequestTo(oracle, req, fee);
}

//callback function
function fulfill(bytes32 _requestId, uint256 _statusCode) public recordChainlinkFulfillment(_requestId) {
    statusCode = _statusCode;
}
```

一旦契约建立起来，发推特就非常简单了。tweet 函数接收要发送的字符串，创建请求结构，并将其提交给定义的 Chainlink 节点。在这种情况下，我们的请求结构中需要两个字段:“status”和“copyPath”。Status，即我们希望发布的 tweet，被定义为 [Twitter 外部适配器](https://market.link/adapters/9ebb251e-1d7c-433d-9835-d771996f5b9c)中的一个输入，节点将运行该适配器来完成任务。然而，CopyPath 是所有 Chainlink 节点支持的[默认适配器的一部分，它告诉节点如何解析 JSON 输出。此外,“端点”可以被指定为具有不同功能的不同 Twitter 端点，但是适配器默认发布 tweet 状态，这与现在无关。](https://docs.chain.link/docs/adapters)

```
{
  jobRunID: 0,
  data: { result: 1315380402618499000 },
  result: 1315380402618499000,
  statusCode: 200
}
```

上面是外部适配器的 JSON 输出示例，如其清单 [market.link](http://market.link/) 中所提供的。我们希望 tweet 的 statusCode 确认它是成功的。StatusCode 是输出的 JSON 结构中的第一级键，所以路径只是“statusCode”。如果我们希望检索“data: {result: }”，其中 result 是第二级键，我们可以使用点符号将该路径指定为“data.result”。在[链节适配器](https://docs.chain.link/docs/adapters)文档页面上提供了复制和其他适配器的更多信息。

请求包含 tweet 和要返回的路径，请求被提交，由节点处理，statusCode 在 fulfill()回调中返回。这个简单的请求形成和提交是智能契约端所需要的，因为大部分繁重的工作都是由 Chainlink 节点处理的。

## Twitter 外部适配器和节点配置

在节点端，我们必须做几件事:

*   安装并运行 Twitter 外部适配器
*   在节点和适配器之间创建一个桥
*   创建一个作业规范来使用这个桥正如 Twitter 适配器清单中所概述的，在使用 yarn 运行适配器之前，需要四个定义 Twitter API 连接访问的环境变量:

```
TWITTER_CONSUMER_KEY
TWITTER_CONSUMER_SECRET
TWITTER_ACCESS_TOKEN_KEY
TWITTER_ACCESS_TOKEN_SECRET

git clone https://github.com/tweether-protocol/twitter-cl-ea
cd twitter-cl-ea
yarn
yarn start
```

默认情况下，适配器监听端口 8080。请注意，如果您的节点和适配器不在同一个容器中运行，或者不是本地的，那么 localhost:8080 对它们来说就不一样。在这种情况下，当您定义到节点的桥时，您需要根据您的适配器运行的位置指定您的 docker 容器的 IP (172.x.x.x)或您的主机的本地 IP (192.168.1.x)。此外，您甚至可以将适配器托管在单独的机器上，在这种情况下，如果它在同一个 LAN 中，您可以指定它的公共 IP 或本地 IP。

定义节点和适配器之间的桥很容易。只需用适配器的 URL(适配器 IP:8080)填充节点界面中的新桥页面，给它一个名称，并指定所需的最低确认和付款。



![New Bridge page of node interface](img/dd238f5b57e90609c9dd20bcd7d21f51.png)

<figcaption id="caption-attachment-597" class="wp-caption-text">UI 用于在 Chainlink 操作器中创建新桥。</figcaption>





既然适配器正在运行并连接到您的节点，我们需要定义一个作业规范，以便在智能契约请求调用该桥时使用它。这可以在节点控制面板的“新作业”部分下执行。在这里，我们定义了一个 JSON 规范，说明什么将启动一个作业，以及这个作业将执行什么任务。

在这个 Twitter 适配器的例子中，我们的工作规范应该是这样的:

```
{
 "initiators": [
   {
     "type": "runlog",
     "params": {
       "address": "YOUR ORACLE CONTRACT ADDRESS HERE"
     }
   }
 ],
 "tasks": [
   {
     "type": "twitter-cl-ea",
     "confirmations": null,
     "params": {
     }
   },
   {
     "type": "copy",
     "confirmations": null,
     "params": {
     }
   },
   {
     "type": "ethuint256",
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

首先是发起者。这只是告诉节点 oracle 从哪个[合同中监控和获取作业。这与之前创建请求智能合约时使用的 oracle 地址相同。请求被发送到这个 oracle on-chain，因为节点正在监视它的作业请求，所以当请求进来时，它将启动这个作业。在](https://chain.link/education/blockchain-oracles)[履行 Chainlink 请求](https://docs.chain.link/docs/fulfilling-requests)文档页面可以找到关于部署该 oracle 合同的更多信息。

接下来是任务。当然，我们需要我们的 Twitter 任务——这只需要是 Twitter 适配器的桥的名称。接下来，我们定义了复制适配器任务，这样它将处理请求中的复制路径，然后是将输出转换为 unit256 的 ethuint256 适配器，最后是将答案提交回链上的 ethtx 适配器。至此，节点设置完成。创建此作业规范时将提供一个作业 ID，请求合同在形成其请求时应该使用此作业 ID。

## 结论

希望本演练有助于进一步展示 Chainlink 将任何 API 连接到您的智能合约的潜力，同时还解释了节点操作符处理这些任务所需的一些配置。

如果你是一名开发人员，并希望将你的智能合同连接到链外数据和系统，请访问[开发人员文档](https://docs.chain.link/)，并加入关于[不和谐](https://discordapp.com/invite/aSK4zew)的技术讨论。如果您想安排一次电话会议来更深入地讨论整合问题，请点击这里的。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://defi.chain.link/)