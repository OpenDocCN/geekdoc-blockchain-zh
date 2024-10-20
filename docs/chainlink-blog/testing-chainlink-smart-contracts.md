# 测试 Chainlink 智能合约

> 原文：<https://blog.chain.link/testing-chainlink-smart-contracts/>

由于[智能合约](https://chain.link/education/smart-contracts)的不变性，在部署之前对其进行彻底测试至关重要。当谈到编写自动化测试时，开发人员有几个选择:

1.  坚固性测试
2.  JavaScript/Python/其他语言测试

通常，用两种方式测试合同是有用的，你可以从这个 T2 样本测试报告中看到，用 JavaScript 和 Solidity 来测试是非常有用的。大多数 dApps 以这种方式与契约交互，所以它们是有用的测试。另一方面，当你测试一个契约/库时，如果主要的使用点来自另一个链上契约，那么最有可能使用 Solidity。

显然，为了更加彻底，两者都要用。如果您有一个简单的智能合同，如:

```
pragma solidity >=0.5.0;

contract Background {
    uint[] private values;

    function storeValue(uint value) public {
        values.push(value);
    }

    function getValue(uint initial) public view returns(uint) {
        return values[initial];
    }

    function getNumberOfValues() public view returns(uint) {
        return values.length;
    }
}

```

编写一些可靠性测试非常简单，比如:

```
pragma solidity >=0.5.0;

import "truffle/Assert.sol";
import "truffle/DeployedAddresses.sol";
import "../../../contracts/Background.sol";

contract TestBackground {
    Background public background;

    // Run before every test function
    function beforeEach() public {
        background = new Background();
    }

    // Test that it stores a value correctly
    function testItStoresAValue() public {
        uint value = 5;
        background.storeValue(value);
        uint result = background.getValue(0);
        Assert.equal(result, value, "It should store the correct value");
    }

    // Test that it gets the correct number of values
    function testItGetsCorrectNumberOfValues() public {
        background.storeValue(99);
        uint newSize = background.getNumberOfValues();
        Assert.equal(newSize, 1, "It should increase the size");
    }

    // Test that it stores multiple values correctly
    function testItStoresMultipleValues() public {
        for (uint8 i = 0; i < 10; i++) {
            uint value = i;
            background.storeValue(value);
            uint result = background.getValue(i);
            Assert.equal(result, value, "It should store the correct value for multiple values");
        }
    }
}

```

对于那些想了解更多关于测试智能合约的人来说，这里有一些额外的资源供你参考。

*   [Ethereum.org](https://ethereum.org/en/developers/docs/smart-contracts/testing/)
*   [松露](https://www.trufflesuite.com/docs/truffle/testing/testing-your-contracts)
*   [安全帽和华夫饼](https://hardhat.org/guides/waffle-testing.html)

对于本文档的其余部分，您至少需要熟悉 Truffle 或 HardHat(以前称为 Buidler)。您也可以从我们之前的一些文章中了解如何使用 Truffle 部署和测试 Chainlink 智能合约。同样，理想情况下，你应该已经明白[单元测试和](https://www.guru99.com/unit-test-vs-integration-test.html)集成测试是不同的，它们都有非常重要的特性。

然而，当使用 chain link[Oracle](https://chain.link/education/blockchain-oracles)和链上数据时，测试会变得有点棘手。一些传统的方法并不能涵盖所有的结果。在本文中，我们将几乎只关注 JavaScript 测试，但是如果您也喜欢这样运行测试，这些方法当然可以与 Solidity 集成。

## 测试 Chainlink 智能合约的最简单方法

测试 [Chainlink](https://chain.link/) 智能合约最简单的方法就是使用测试网！大多数项目会在进入 mainnet 之前部署到 testnet，但是他们也可以继续重新部署来迭代他们的测试，因为 testnet ETH 是免费的。目前，Kovan 或 Rinkeby 有大量的链接节点、价格信息，以及你正在寻找的任何东西。在你的测试文件中，确保获得一些 testnet 链接和 ETH，你就可以开始了。另一个简单的方法是运行你自己的 Chainlink 节点，让它监控你正在运行的本地链。

与本地区块链相比，在测试网上运行测试并不是特别快。你也有达到水龙头极限的风险。让我们看看如何在本地测试 Chainlink 智能合约。

### 使用分叉

意式冰淇淋是一个使用分叉和链环的项目的例子。

[Chainlink 价格反馈](https://data.chain.link/)是 Chainlink 提供的最受欢迎的服务之一。oracle networks 从分散的独立来源收集数据，并创建一个可靠的链上事实来源。问题是，你如何测试你是否正确地消费了这些价格数据？

*   您是否部署了自己的价格源？
*   你会忽略测试价格信息吗？
*   你会跳过所有的测试，祈祷你的 dApp 不会崩溃吗？

现在，非常欢迎您执行第三个项目，但是强烈建议不要这样做，尤其是因为测试它们是轻而易举的事情！我们需要做的就是[叉上我们正在使用的链条](https://hardhat.org/guides/mainnet-forking.html)。如果你以前没有使用过 Chainlink Price Feeds，一定要查看一下[我们的文档](https://docs.chain.link/docs/using-chainlink-reference-contracts)。这部分的所有代码都可以在[链节-安全帽报告](https://github.com/PatrickAlphaC/chainlink-hardhat)中找到。对于那些不熟悉 Hardhat 的人来说，这是一个类似松露的设置，有许多美好的生活质量差异。

假设我们有一个使用 Chainlink 价格源的合同，看起来像这样:

```
pragma solidity ^0.6.6;

import "@chainlink/contracts/src/v0.6/interfaces/AggregatorV3Interface.sol";

contract PriceConsumerV3 {

    AggregatorV3Interface internal priceFeed;

    /**
     * Network: Mainnet
     * Aggregator: ETH/USD
     * Address: 0x5f4eC3Df9cbd43714FE2740f5E3616155c5b8419
     */
    constructor() public {
        priceFeed = AggregatorV3Interface(0x5f4eC3Df9cbd43714FE2740f5E3616155c5b8419);
    }

    /**
     * Returns the latest price
     */
    function getLatestPrice() public view returns (int) {
        (
            uint80 roundID, 
            int price,
            uint startedAt,
            uint timeStamp,
            uint80 answeredInRound
        ) = priceFeed.latestRoundData();
        // If the round is not complete yet, timestamp is 0
        require(timeStamp > 0, "Round not complete");
        return price;
    }
}

```

首先，是的，我们使用了 mainnet 价格馈送地址，但不要惊慌。这是故意的。通常，要与 mainnet 价格源交互，我们必须部署在 mainnet 上。然而，当运行我们的测试时，我们实际上可以分叉链，以查看如果它们被部署在 mainnet 上，它们看起来会是什么样子，而不用实际地将它们部署在 mainnet 上。使用 [HardHat 的设置](https://hardhat.org/)，我们可以添加到我们的 hardhat.config.js 文件，我们想从这个网络分叉。

下面是我们的 hardhat.config.js 文件的样子:

```
require("@nomiclabs/hardhat-waffle")

module.exports = {
  defaultNetwork: "hardhat",
  networks: {
    hardhat: {
      forking: {
        url: process.env.ALCHEMY_MAINNET_RPC_URL
      }
    },
    kovan: {
      url: process.env.KOVAN_RPC_URL,
      accounts: {
        mnemonic: process.env.MNEMONIC
      }
    }
  },
  solidity: "0.6.6",
}

```

你会看到我们的*安全帽*网络有一个*分叉*密钥。这意味着当我们在 hardhat 网络上部署一个脚本时，我们将首先派生我们的 RPC_URL 中的内容(目前设置为 *ALCHEMY_MAINNET_RPC_URL* ，然后将它部署到那个网络。这对于测试来说非常好，因为我们实际上可以将我们的智能合约部署到 mainnet 的分叉版本上，并使用我们的价格反馈进行测试。

你自己试试！

```
git clone https://github.com/PatrickAlphaC/chainlink-hardhat

cd chainlink-hardhat

yarn

npx hardhat test

```

这将通过将智能合约部署到分叉的 mainnet 来测试我们的智能合约。松露团队也有一个特性，你可以分叉 mainnet 和基于分叉网络的测试。

### 使用模拟

Aave 是一个使用模拟和链接进行测试的项目的例子。

不幸的是，分叉 mainnet 来测试与 Chainlink oracles 的交互是行不通的。这是因为我们没有任何链接神谕来监控我们的分叉网络。所以我们经常需要去别的地方看看。测试具有依赖关系的对象和服务并不是什么新鲜事，但是在编写单元测试时会出现困难。一个好的解决方案是[模仿](https://medium.com/@piraveenaparalogarajah/what-is-mocking-in-testing-d4b0f2dbe20a#:~:text=We%20use%20mocking%20in%20unit,behavior%20of%20the%20real%20objects.)任何依赖，并且将测试仅仅集中在合同本身上。

模仿本质上是用简单的对象代替复杂的对象，模仿我们想要做的功能。这对于使用 [Chainlink API 调用](https://docs.chain.link/docs/request-and-receive-data)、 [Chainlink VRF](https://docs.chain.link/docs/vrf-contracts) 或任何 [Chainlink 外部适配器](https://docs.chain.link/docs/external-adapters)的项目来说非常有用。通常，工程师会在他们的测试文件夹中创建一个*模拟*文件，其中包含所有的虚拟模拟。我们可以看到一个简单的版本，用这样的文件模拟 ERC20，在测试时模拟使用真实的 ERC20:

```
pragma solidity ^0.6.10;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MockERC20 is ERC20 {
    constructor() public ERC20("MOCK", "MCK") {
        _mint(msg.sender, 100*10**18);
    }
}

```

一个更相关的模拟将与模拟链接消费者一起工作，或者与链接 oracle 交互的智能契约。看起来大概是这样的:

```
pragma solidity ^0.6.10;

import "@chainlink/contracts/src/v0.6/ChainlinkClient.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MockOracleClient is ChainlinkClient, Ownable {
    event Tweet(string content);

    constructor(address _link) public {
        link = _link;
    }

    function sendTweet(string memory content) external override onlyGovernance {
        emit Tweet(content);
    }
}

```

在这个模拟中，我们有 *sendTweet* 函数——在 _real _Chainlink 消费者契约中，它将向 Chainlink 节点发出 Chainlink API 请求以“发送 Tweet”。然而，在我们的模拟中，我们只是发出一条 tweet 被发送的日志，这可以是一种简单的方法来模拟获得对 Chainlink 节点的响应。你可以在[推特回购](https://github.com/tweether-protocol/tweether/tree/master/contracts/mocks)中看到所有这些模仿。回购使用了块菌和安全帽的组合，所以你可以看到两者配合得很好。

您可以看到许多使用这种方法的生产项目。例如，Aave 使用 [Chainlink 模拟](https://github.com/aave/aave-protocol/tree/1ff8418eb5c73ce233ac44bfb7541d07828b273f/contracts/mocks/oracle)来运行他们的测试。

### 使用助手进行部署

最复杂的测试可以在 [truffle smartcontractkit 工具箱中找到。](https://github.com/smartcontractkit/box/blob/master/test/MyContract_test.js)* * * *这是 Chainlink 工程师用来构建智能合同的首批产品之一。一旦您安装了 Truffle，您可以通过打开一个新的 repo 来快速启动您自己的机器，然后运行:

*松露拆箱 smartcontractkit/盒子*

一旦你完成了这个，你将会看到 *MyContract_test.js* ，它贯穿了你在进行 Chainlink API 调用时想要涵盖的所有潜在场景。在 [Chainlink 块菌回购看看吧。](https://github.com/smartcontractkit/box)

## 摘要

测试 Chainlink smart contracts 是确保您的代码在开发过程中保持高质量的一个好方法，上面的一系列选项使测试比以往任何时候都更容易。不要认为在测试中运行复杂的对象太难了。当涉及到扩展您的 dApp 和构建令人惊叹的东西时，集成测试是至关重要的。

对于那些希望开始使用所有这些神奇工具进行构建的人来说，一定要点击示例中的链接，或者直接前往 [Chainlink 文档](https://docs.chain.link/)。你会找到一切你需要开始，并成为一个坚实的区块链工程硕士。