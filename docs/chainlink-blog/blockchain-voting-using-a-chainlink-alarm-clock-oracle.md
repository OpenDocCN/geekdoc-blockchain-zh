# 使用 Chainlink 闹钟 Oracle 的区块链投票

> 原文：<https://blog.chain.link/blockchain-voting-using-a-chainlink-alarm-clock-oracle/>

以太坊上的许多[智能合约](https://chain.link/education/smart-contracts)需要外部时间源来触发链上动作。对于使用链上区块链投票系统的 dApps 来说，这是一个挑战，因为投票窗口被限制在特定的时间。如果没有计时器，投票智能契约将需要一些外部资源来修改投票窗口的状态，打开或关闭。

在遗留系统中，计时可能是一项简单的任务。系统调用允许从 NTP 同步操作系统时间中检索时间，有硬件时钟和计数器，也有休眠语句来在指定的时间范围内暂停代码。在 Solidity 智能合约中，事件由链外交易触发，这意味着以太坊和其他区块链需要一个链外闹钟来触发事件/函数调用。幸运的是， [Chainlink](https://chain.link/) 节点可以作为一个可靠的闹钟来触发智能合约。

在这里，我们将向您展示您的 dApp 如何实现简单的时间门控投票，随着越来越多的 dApp 通过 DAOs 将权力放在用户手中，这一过程变得越来越需要。该设置包括以下内容:

*   将 Chainlink 功能继承到您的合同中
*   格式化并提交链接休眠(“直到”)请求
*   限制对合同所有者的投票
*   简单的 KYC 确认每个地址只投一次票
*   检查投票状态的 Getters

你可以在 [GitHub](https://github.com/gmondok/ChainlinkVoting) 上找到这个演示中使用的代码，或者使用易于部署的 [Remix](https://remix.ethereum.org/#version=soljson-v0.6.0+commit.26b70077.js&optimize=false&gist=954e17a510d1c0474e9beeaa78869e49) 链接。

当然，这个基本的例子只是一个开始。您需要在某个时间触发的任何事件都可以用 chain link“until”请求来处理，这个示例可以用作构建其他时间敏感的智能契约的起始框架。

## **合同定义和施工方:**

```
pragma solidity ^0.6.6;

import "github.com/smartcontractkit/chainlink/evm-contracts/src/v0.6/ChainlinkClient.sol";

contract ChainlinkTimedVote is ChainlinkClient
{
    uint private oraclePayment;
    address private oracle;
    bytes32 private jobId;
    uint private yesCount;
    uint private noCount;
    bool private votingLive;
    mapping(address => bool) public voters;

    //only the contract owner should be able to start voting
    address payable owner;
    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }

    constructor() public {
        setPublicChainlinkToken();
        owner = msg.sender;
        oraclePayment = 0.1 * 10 ** 18; // 0.1 LINK
        //Kovan alarm oracle
        oracle = 0x2f90A6D021db21e1B2A077c5a37B3C7E75D15b7e; 
        jobId = "a7ab70d561d34eb49e9b1612fd2e044b";
        //initialize votes
        yesCount = 0;
        noCount = 0;
        votingLive = false;
    }
}
```

导入 ChainlinkClient 并用“is”关键字继承它，就可以访问生成 Chainlink 节点请求的功能。之后，我们要定义一些全局变量，比如我们将用作计时器的 oracle(节点)地址。这些地址可以在 [Chainlinks (Testnet)](https://docs.chain.link/docs/available-oracles#config) 页面上找到。

此外，我们需要一个 job spec ID、一些跟踪投票的变量和一个投票者到布尔值的映射，以便跟踪一个地址是否已经投票。最后，我们定义一个修饰符，稍后我们可以使用它来要求调用函数的消息发送者成为契约所有者。然后，我们初始化所有者地址以及构造函数中的其他变量。注意:映射不需要初始化，对于 bool 类型，它将默认为 false。

## **Chainlink 请求开始投票:**

```
function startVote(uint voteMinutes) public onlyOwner {
    Chainlink.Request memory req = buildChainlinkRequest(jobId, address(this), this.fulfill.selector);
    req.addUint("until", now + voteMinutes * 1 minutes);
    //Start voting window then submit request to sleep for $voteMinutes
    votingLive = true;
    sendChainlinkRequestTo(oracle, req, oraclePayment);
}

//Callback for startVote request
function fulfill(bytes32 _requestId) public recordChainlinkFulfillment(_requestId) {
    //$voteMinutes minutes have elapsed, stop voting
    votingLive = false;
}

```

我们的契约的第一个功能，startVote，是链接请求发挥作用的地方。您可以看到，这是我们使用 onlyOwner 修饰符来确保投票只能由合同所有者启动的地方。

正如我们的 [Connect to Any API](https://blog.chain.link/apis-smart-contracts-and-how-to-connect-them/) 文章中所述，ChainlinkClient 契约公开了一个 Chainlink。请求结构，可以根据请求的性质以各种方式进行格式化。在这种情况下，我们没有向结构添加“get”请求，而是添加了“until”。until 字符串由我们在构造函数中定义的 Chainlink 节点地址识别，在收到该请求时，节点将在指定的时间内暂停其当前任务管道，在本例中为“voteMinutes”分钟数。

在提交这个请求之前，我们将 votingLive 设置为 true，这将打开投票，因为 vote 函数检查该变量的状态以允许或拒绝投票。然后我们提交请求，此时 Chainlink 节点将暂停我们的任务管道。实际上，这会将完成回调延迟我们在 until 请求中指定的时间。因为当调用 fulfill 时，我们期望的时间窗口已经过去，所以我们现在可以将 votingLive 设置回 false，投票现在关闭。

概括地说，用期望的时间构建一个“until”请求，提交给指定的 [oracle 节点](https://chain.link/education/blockchain-oracles)，在节点暂停指定时间后，将调用 fulfill 函数。实现一个链式计时器/闹钟是如此简单。通过一个简单的 votingLive 布尔值，我们可以在 Chainlink 报警请求之前将投票标记为打开，并在延迟后收到回调时将其标记为关闭，从而控制投票的打开和关闭。虽然在这个例子中它只是一个布尔标志，但它可以根据需要适用于任何延时动作。

## **投票和检查投票状态:**

```
//Increments appropriate vote counter if voting is live
function vote(bool voteCast) public {
    require(!voters[msg.sender], "Already voted!");
    //if voting is live and address hasn't voted yet, count vote  
    if(voteCast) {yesCount++;}
    if(!voteCast) {noCount++;}
    //address has voted, mark them as such
    voters[msg.sender] = true;
}

//Outputs current vote counts
function getVotes() public view returns (uint yesVotes, uint noVotes) {
    return(yesCount, noCount);
}

//Lets user know if their vote has been counted
function haveYouVoted() public view returns (bool) {
    return voters[msg.sender];
}

```

当然，现在我们需要实际的投票逻辑。投票函数简单地以真/假(是/否)的形式进行投票，检查用户以前是否投票过，如果他们通过了检查，则对他们的投票进行计数，并通过将他们的地址映射设置为真来标记他们已经投票。我们使用 require 语句而不是 if 来检查地址，以便在他们已经投票的情况下拒绝交易。最后，由于以太坊交易不返回输出，我们添加了一些简单的查看函数来检查当前的投票数，并确认您的投票是否已被计算在内。

希望本指南有助于阐明 Chainlink 的众多用途之一，您可以使用 mainnet 上的 live 来开发这些用途，以增强您的智能合约应用程序的功能。如果您想了解更多的 Chainlink 功能，请查看可证明随机数生成的 [Chainlink VRF](https://chain.link/solutions/chainlink-vrf) ，使用 Chainlink Price Feeds 构建您的第一个 [yield farming dApp](https://blog.chain.link/build-defi-yield-farming-application-with-chainlink/) ，或者阅读我们关于在交易订购中使用 chain link Oracle for[Fair Sequencing Services](https://blog.chain.link/chainlink-fair-sequencing-services-enabling-a-provably-fair-defi-ecosystem/)的最新研究。

如果你是一名开发人员，并希望将你的智能合同连接到链外数据和系统，请访问[开发人员文档](https://docs.chain.link/)，并加入关于[不和谐](https://discordapp.com/invite/aSK4zew)的技术讨论。如果您想安排一次电话会议来更深入地讨论整合事宜，请点击此处的。