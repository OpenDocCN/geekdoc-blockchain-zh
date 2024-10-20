# 使用 Chainlink 外部适配器构建 RFID 区块链集成

> 原文：<https://blog.chain.link/rfid-blockchain-integration-with-chainlink-external-adapters/>

庞大且不断增长的物联网数据世界正在跟踪比以往任何时候都多的真实世界对象和流程。 [Chainlink 外部适配器](https://blog.chain.link/build-and-use-external-adapters/)非常适合通过安全可靠的 [oracle](https://chain.link/education/blockchain-oracles) 网络向各种物联网智能合同用例提供物联网数据，例如链上供应链逻辑或智能合同保险索赔的跟踪温度数据。将 [RFID 扫描仪](https://www.techopedia.com/definition/26992/radio-frequency-identification-reader-rfid-reader#:~:text=A%20radio%20frequency%20identification%20reader%20(RFID%20reader)%20is%20a%20device,in%20theory%20to%20bar%20codes.)(射频识别)数据集成到区块链就是这样一个例子。

在 [Chainlink 虚拟黑客马拉松](https://blog.chain.link/congratulations-to-the-winners-of-the-chainlink-virtual-hackathon-2020/)中获得最佳开放项目奖的开发者阿拉姆·莫哈达斯和亚伦·乏色曼使用 Chainlink 外部适配器将 Arduino RFID 连接到 Chainlink oracle，用于分散式图书借阅和跟踪系统，称为[开放图书馆项目](https://devpost.com/software/the-open-library-project)。

在这篇教程文章中，Aram Moghaddassi 解释了他们是如何实现这个项目的。

* * *

*由* [到*阿拉姆*到](http://about.me/AramMogha)

区块链上启用的硬件系统是智能合约开发者的新领域。这篇文章将涵盖构建这种系统的灵感、应用和技术设计，并作为一个教程(通过示例)介绍如何将 Chainlink 节点上的 [RFID 传感器的模拟硬件后端集成到智能合同中。](https://market.link/jobs/1f42390a-7c19-42ec-a785-a0fc9d609b28)

## 物联网硬件和智能合同的潜力

区块链和[智能合同](https://chain.link/education/smart-contracts)有可能保护目前部署的数百亿物联网设备，这些设备每年都会产生 zettabytes 的数据。从智能家居、城市、工厂、供应链等等，物联网设备正在彻底改变传统基础设施，自动化系统有可能在这一领域创造强大的效率和业务逻辑。为此，我们开发了定制的外部适配器，允许智能合约与实时硬件系统接口。我们目前正在托管一个带有虚拟硬件后端的 RFID 外部适配器，因此您可以跟随本教程并亲自尝试一下。



![How a Chainlink decentralized oracle network securely feeds IoT data to smart contracts.](img/56f698e72d98d89ba7f7d0528bef5bd0.png)

<figcaption id="caption-attachment-620" class="wp-caption-text">一个 Chainlink 分散式 oracle 网络如何安全地向智能合同提供物联网数据。</figcaption>





我们的目标是:在 10 分钟内，您将部署一个智能合同，可以从我们的 RFID 适配器查询数据。我们希望让现有的 Web3 开发者尽可能直观地开始将硬件集成到您的 dApps 中。

## 建议的先决条件

*   熟悉使用 Chainlink 开发 Solidity 非常重要。我们将在 Kovan testnet 上使用 [Remix 以太坊 IDE](https://remix.ethereum.org/) 。
*   不需要硬件！[我们现在已经开始集成 RFID 传感器](https://market.link/jobs/1f42390a-7c19-42ec-a785-a0fc9d609b28)(更多设备即将推出)。它发送样本数据，您可以使用这些数据快速启动并运行 dApp。

本教程将是在我们的 [GitHub repo](https://github.com/amoghaddassi/rfid-external-adapter) 上找到的演示的书面版本，您可以在开始之前熟悉一下。

[![](img/238d2507484fea6a2d67c090c9fc6750.png)](https://www.youtube.com/watch?v=NdmyUhuQpgI&width=640&height=480) 

## 构建 RFID 数据提供商智能合同

### 工作/Oracle 规格

为了遵循这个指南，我们将使用在 Kovan testnet 上运行的这个[作业](https://market.link/jobs/1f42390a-7c19-42ec-a785-a0fc9d609b28)和[节点](https://market.link/profile/nodes/305e6143-288c-4acc-bf23-e9524549d3e8/overview)。

RFID 扫描仪适配器将以字节格式返回一个示例卡 UID。

### 基本合同

以下是调用节点的 RFID 作业并将响应存储在变量中的基本约定:

[部署本合同并重新混合](https://remix.ethereum.org/#version=soljson-v0.6.0+commit.26b70077.js&optimize=false&evmVersion=null&gist=15eae06de1a102701ac6c8cb23eb48e5):

```
pragma solidity ^0.6.0;

import "https://github.com/smartcontractkit/chainlink/blob/develop/evm-contracts/src/v0.6/ChainlinkClient.sol";

contract Client is ChainlinkClient {
    // where to store the last id scanned
    bytes32 public last_uid;
    // Chainlink vars for communicating with the RFID external adapter
    address private oracle;
    bytes32 private jobId;
    uint256 private fee;

    constructor() public {
        setPublicChainlinkToken();
        oracle = 0x42149D794A135989319b66Dbcb770Ad36075a92e;
        jobId = "785558e0bed6466b9567322cc2f4ca91";
        fee = 1 * 10 ** 18; // 0.1 LINK
    }

    function requestData() public returns (bytes32 requestId) {
        // creates the Request
        Chainlink.Request memory req = buildChainlinkRequest(jobId, address(this), this.fulfill.selector);
        // Sends the request
        return sendChainlinkRequestTo(oracle, req, fee);
    }

    function fulfill(bytes32 _requestId, bytes32 uid) public recordChainlinkFulfillment(_requestId) {
        last_uid = uid;
    }
}

```

### 部署合同并与之交互

遵循本 [Chainlink 指南](https://docs.chain.link/docs/example-walkthrough#introduction)了解如何使用 testnet LINK 部署合同和资金。我们建议为至少 10 个链接的合同提供资金。

契约的 requestData 方法将向 RFID 作业发出 Chainlink 请求，完成后，将把最后一次扫描的 UID 放入 last_uid 变量中。

## 应用和未来集成

我们的 RFID 集成是一个概念证明，我们可以在智能合同上运行实时硬件设备。我们希望继续构建硬件集成，并最终在 Chainlink 社区中引导一个硬件生态系统。尽管如此，最终还是要靠开发者来找到使用这项技术的杀手级应用。

以下是我们对 RFID 适配器的一些想法，您可以立即着手实施:

*   **实物保管管理**–贴有 RFID 芯片的物品可以在不同的路径点进行扫描，以安全地跟踪位置。该系统可能有利于区块链的供应链管理应用。
*   **酒店入住/退房系统**–当用户入住某个地点时，Airbnb/hotels 可以自动启动租赁合同。智能合同可以实时自动收取任何滞纳金。
*   **用于签署数字协议的物理验证系统**–使用 RFID 扫描来验证用户的物理存在。
*   **发挥创意！**RFID 接口非常普通，你能想到的任何东西都有可能被制造出来。

最好的链上硬件应用程序将利用智能合约的独特属性来获得超越传统软件的优势。智能合同是确定性的、去中心化的数字协议。在硬件环境中，区块链带来的最有价值的好处是(1)强大的机器对机器通信协议和(2)来自传感器的防篡改数据。

## 构建您自己的硬件外部适配器

我们的团队在构建开放图书馆项目时学到了一些经验。如果您正在考虑自己构建硬件外部适配器，我们发现这些原则非常有用。虽然我们在构建 RFID 扫描仪的硬件适配器时做出了设计决策，但这些原则应该适用于任何实时硬件传感器集成。

**原则 0:** 适配器服务器结构与所有其他服务器结构相同。您可以使用任何现有的外部适配器模板作为起点。主要区别在于以下原则。

**原则 1:** 硬件必须有一些软件接口/API，外部适配器可以调用。

对于 RFID 扫描仪，我们使用 [pyserial](https://pyserial.readthedocs.io/en/latest/) 编写了一个定制的[解析器](https://github.com/amoghaddassi/embed.network/blob/main/adapters/rfid/rfid.py)，它创建了一个简单的接口来从每次扫描中获取 UID 代码。然后我们可以编写一个简单的 [flask 服务器](https://github.com/amoghaddassi/embed.network/blob/main/adapters/rfid/rfid_adapter.py)，接受 POST 请求来读取 UID。

对于定制程度较低的硬件(即非 Arduino)，该软件接口可能由开箱即用的 API 提供。在这种情况下，您只需要担心编写外部适配器接口。

**原则 2:** 外部适配器必须在本地运行(忽略虚拟硬件后端)。

对于那些熟悉在云服务器上部署适配器的人来说，这可能有点奇怪。但是，考虑到我们要将数据从本地硬件传感器移动到远程 Chainlink 节点，为节点提供数据的适配器服务器必须在本地运行。我们设想一个最佳设置，使用专用的 Raspberry Pi 来运行硬件和服务器(尽管我们在开发期间使用了笔记本电脑)。

* * *

## 立即开始使用外部适配器进行构建

如果您是一名开发人员，并且希望将您的智能合约连接到底层区块链之外的现有硬件或数据，请联系此处的[或访问](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=blog)[开发人员文档](https://docs.chain.link/)。

如果你在这里学到了一些新东西，想要炫耀你已经建立的东西，或者为一些演示回购开发了一个前端，请确保你在 [Twitter](https://twitter.com/chainlink) 、 [Discord](https://discord.gg/Szt3FYj) 或 [Reddit](https://www.reddit.com/r/Chainlink/) 上分享它，并用#Chainlink 标记你的回购。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[|](https://www.reddit.com/r/Chainlink/)[不和](https://discordapp.com/invite/aSK4zew)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://defi.chain.link/)