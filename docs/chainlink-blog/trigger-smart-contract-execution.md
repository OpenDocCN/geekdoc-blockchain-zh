# 通过 Chainlink Automation 触发智能合同执行

> 原文：<https://blog.chain.link/trigger-smart-contract-execution/>

智能合约不是自动执行的，这意味着它们需要外部拥有的帐户、oracle 或合约来触发它们自己的功能。这给许多 dApps 带来了问题，这些 dApps 要求它们的智能合约以固定的时间间隔(例如，每 24 小时)执行，当满足预定义的条件时(例如，以太坊达到特定价格)，或者在计算之后(例如，贷款被计算为抵押不足)。

过去，开发人员会通过创建和维护他们自己的集中式脚本来触发他们的智能合约，或者手动触发它们，来解决这个问题。然而，这实际上破坏了构建分散式区块链应用程序的目的，并且如果集中式脚本或手动触发过程失败，还可能导致停机。

在本教程中，您将学习如何使用 Chainlink Automation 以可靠、自动和分散的方式触发智能合同执行。

## 为什么要使用分散自动化来触发智能合同？

Chainlink Automation 开启了一种以分散方式触发智能合同执行的新方式，使开发人员能够转变他们构建和维护 dApps 的方式。分散式智能联系人自动化有三个主要好处。

首先，消除运营中的任何集中故障点至关重要。Chainlink Automation 由一个分散的节点网络提供支持，这些节点高度可靠，目前通过 Chainlink 数据馈送在 DeFi 中保护了数百亿美元的价值，消除了集中的故障点。

其次，开发人员无需投入时间和资源来创建用于在线监控和触发智能合同执行的脚本，只需创建一个与自动化兼容的合同并进行注册，即可接入 Chainlink Automation 的优化基础设施。这节省了时间，减少了 DevOps 的工作量，并允许开发人员专注于编写更好的代码。

最后，通过使用 Chainlink Automation，开发者可以增强他们协议的安全性。当从集中式服务器发起事务时，开发人员不再需要冒着暴露自己的私钥的风险 Chainlink 自动化网络上的节点将签署链上事务。

## 开始使用 Chainlink 自动化

您可以通过 Chainlink Automation 分两步实现智能合约的自动化:

1.  创建并部署一个 [自动化兼容合同](https://docs.chain.link/docs/chainlink-keepers/compatible-contracts/)
2.  在 [Chainlink 自动化 app](https://keepers.chain.link/) 上注册合同，创建保养

完成这些步骤后，Chainlink Automation 将执行指定的维护工作，无需任何进一步输入。

如果您是 Solidity 的新手，我们建议您在继续之前先学习一些初学者教程。 [这个教程](https://youtu.be/M576WGiDBdQ) 特别全面有用。我们现在将向您展示如何使您的合同自动化兼容。如果你喜欢看关于这个话题的视频，请观看我们的 [视频](https://www.youtube.com/watch?v=-Wkw5JVQGUo) 教程。

## 如何为智能合同创建自动触发器

要创建智能合同执行的自动化触发器，您需要编写一个自动化兼容的智能合同。自动化兼容合同有一个`checkUpkeep`函数和一个`performUpkeep`函数，其中包含 Chainlink Automation 预期的所需输入和输出。为了帮助防止错误，我们将在指定我们的检查和执行函数应该做什么之前使用自动化兼容的接口。

### 导入自动化兼容接口

首先将 `KeeperCompatibleInterface` 导入到您的合同中。

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// KeeperCompatible.sol imports the functions from both ./KeeperBase.sol and
// ./interfaces/KeeperCompatibleInterface.sol

import "@chainlink/contracts/src/v0.8/KeeperCompatible.sol";
```

该界面有两个功能:

#### `checkUpkeep`功能

Chainlink Automation 使用分散式网络，在每个模块期间安全、经济高效地监控`checkUpkeep`功能，然后在满足预定义条件时启动链上交易，以执行智能合同功能。

```
function checkUpkeep(
  bytes calldata checkData
)
  external
  returns (
    bool upkeepNeeded,
    bytes memory performData
  );
```

`checkUpkeep`函数需要一个 字节 参数，名为 `checkData`，是当你[在](https://keepers.chain.link/new)[自动化应用](https://keepers.chain.link/)上注册你的保养时设置的。这个值是可选的，可以在您的逻辑中用来确定 `checkUpkeep`是否返回``true`` 。

`checkUpkeep` 返回一个 bool 称为 `upkeepNeeded` 。为真时，这将调用 `performUpkeep` 。它还以 字节 格式返回 `performData` (可选附加数据)，如果需要维护，自动化节点应该调用`performUpkeep`。更多信息请参见 [开发者文档](https://docs.chain.link/docs/chainlink-keepers/compatible-contracts/#performdata) 。

#### `performUpkeep`功能

如果您的 `checkUpkeep` 的链外模拟确认您的预定义条件得到满足(`upkeepNeeded == true` from `checkUpkeep` )，自动化节点将向执行 `performUpkeep` 的区块链广播一个事务，并将`performData`作为输入 。

```
function performUpkeep(
  bytes calldata performData
) external;
```

循环节点选择流程可防止节点之间的天然气价格拍卖战，并稳定自动化合同的成本。

![An animation showing how Keepers work](img/30d9fb7847d42e6417f0bc57bbd63737.png)

以下是 Chainlink Automation 用户[Entropyfi](https://medium.com/entropyfi/entropyfi-saves-engineering-hours-with-chainlink-keepers-6ec172a76249)的合同片段示例，其中 `checkUpkeep` 检查 Entropyfi 预测游戏是否到期结算。

```
/**
* @dev chainlink keeper checkUpkeep function to constantly check whether we need function call
**/
function checkUpkeep(bytes calldata checkData) external override returns (bool upkeepNeeded, bytes memory performData) {
     PoolStatus currState = status.currState;
     uint256 lastUpdateTimestamp = status.lastUpdateTimestamp;
     uint256 durationOfGame = status.durationOfGame;
     uint256 durationOfBidding = status.durationOfBidding;

     if (currState == PoolStatus.Accepting && block.timestamp > lastUpdateTimestamp.add(durationOfBidding)) {
          upkeepNeeded = true;
     } else if (currState == PoolStatus.Locked && block.timestamp > lastUpdateTimestamp.add(durationOfGame)) {
          upkeepNeeded = true;
     } else {
          upkeepNeeded = false;
     }
     performData = checkData;
}
```

Chainlink 自动化节点会不断调用`checkUpkeep`函数，如果`upkeepNeeded`被求值为`true`，那么节点会执行 `performUpkeep` 函数。

```
/**
* @dev once checkUpKeep been triggered, keeper will call performUpKeep
**/
function performUpkeep(bytes calldata performData) external override {
     PoolStatus currState = status.currState;
     uint256 lastUpdateTimestamp = status.lastUpdateTimestamp;
     uint256 durationOfGame = status.durationOfGame;
     uint256 durationOfBidding = status.durationOfBidding;

     if (currState == PoolStatus.Accepting && block.timestamp > lastUpdateTimestamp.add(durationOfBidding)) {
          startGame();
     }
     if (currState == PoolStatus.Locked && block.timestamp > lastUpdateTimestamp.add(durationOfGame)) {
          endGame();
     }
     performData;
}
```

## 从一些示例代码开始

无论您是在创建新合同，还是已经部署了包含需要自动化的功能的合同，Chainlink Automation [开发人员文档](https://docs.chain.link/docs/chainlink-keepers/utility-contracts/) 都有帮助您入门的指南。

先以 [为例合同此处](https://docs.chain.link/docs/chainlink-keepers/compatible-contracts/#example-contract) 。下面的例子代表了一个简单的反向契约。

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.7.0;

// KeeperCompatible.sol imports the functions from both ./KeeperBase.sol and
// ./interfaces/KeeperCompatibleInterface.sol
import "@chainlink/contracts/src/v0.7/KeeperCompatible.sol";

contract Counter is KeeperCompatibleInterface {
    /**
 * Public counter variable
 */
    uint public counter;

    /**
 * Use an interval in seconds and a timestamp to slow execution of Upkeep
 */
    uint public immutable interval;
    uint public lastTimeStamp;

    constructor(uint updateInterval) {
 interval = updateInterval;
      lastTimeStamp = block.timestamp;

counter = 0;
    }

    function checkUpkeep(bytes calldata /* checkData */) external override returns (bool upkeepNeeded, bytes memory /* performData */) {
 upkeepNeeded = (block.timestamp - lastTimeStamp) > interval;
        // We don't use the checkData in this example. The checkData is defined when the Upkeep was registered.
 }
    function performUpkeep(bytes calldata /* performData */) external override {
        //We highly recommend revalidating the upkeep in the performUpkeep function
        if ((block.timestamp - lastTimeStamp) > interval ) {
 lastTimeStamp = block.timestamp;
counter = counter + 1;
 }
        // We don't use the performData in this example. The performData is generated by the Keeper's call to your checkUpkeep function
 }
}
```

![Diagram showing potential Keepers triggers](img/5e29e278db3b46032597bd78d33e3026.png)

<figcaption id="caption-attachment-3401" class="wp-caption-text">There are a huge range of possible triggers for smart contract automation.</figcaption>



Chainlink Automation 可以监控任何链上或链下条件的状态，例如时间的流逝(例如，24 小时过去了吗？)或计算(例如，贷款是否计算为抵押不足？).一旦满足条件，自动化节点提交链上的事务，以触发智能合约的执行。

你也可以从一个 Chainlink 自动化实用契约开始，比如[EthBalanceMonitor](https://github.com/smartcontractkit/upkeep-contracts/blob/master/contracts/upkeeps/EthBalanceMonitor.sol)[契约](https://github.com/smartcontractkit/upkeep-contracts/blob/master/contracts/upkeeps/EthBalanceMonitor.sol) 或 [这些例子](https://docs.chain.link/docs/chainlink-keepers/utility-contracts/) 。

## 如何在网络上注册您的合同作为维护费

一旦你有了你的自动化兼容合同，前往 [Chainlink 自动化应用](https://keepers.chain.link/) 并点击“注册新维护”。

![Registering a new Upkeep](img/31667f36d66fa2e116d3a6ea803e6e2a.png)

有关如何注册的详细分步指南，请参见 [Chainlink 开发者文档](https://docs.chain.link/docs/chainlink-keepers/register-upkeep/) 。

***重要提示(非 ETH 链):*** *你的维持费必须用 ERC-677 链接资助(* ***不是*** *ERC-20，这是很多令牌桥通用的)。使用 PegSwap 将* [*使您的链接令牌兼容*](https://pegswap.chain.link/) *。T25】*

注册并获得批准后，您可以添加额外的资金，并在 Chainlink Automation 应用程序上查看您的保养详情。

![Screenshot illustrating how to register a timed Upkeep](img/523b4a7c4fceed84f79f93c21c3b8545.png)

![Image of the Keepers dashboard](img/b0cd5d36890c207617378de481b46ccb.png)

## 今天就开始

现在，您已经知道使用 Chainlink Automation 实现智能合约自动化是多么简单，您可以开始集成 Chainlink Automation 并解锁 [大量用例](https://blog.chain.link/smart-contract-automation-use-cases-powered-by-chainlink-keepers/) ，例如 DEX 限价单、跨链 NFT 铸造、重置基础和重新平衡代币等等。

访问 [开发者文档](https://docs.chain.link/docs/chainlink-keepers/introduction/) 了解更多信息，并加入 [不和谐](https://discordapp.com/invite/aSK4zew) 中的技术讨论。如果您想安排一次电话会议来更深入地讨论集成，请点击此处的[](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=announcement)。

要了解更多，请访问[chain . link](https://chain.link/)，订阅 [Chainlink 简讯](https://chn.lk/newsletter) ，并关注 Chainlink 上的[Twitter](https://twitter.com/chainlink)，[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)，以及[Reddit](https://www.reddit.com/r/Chainlink/)。