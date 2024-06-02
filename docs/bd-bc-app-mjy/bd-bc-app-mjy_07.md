# 第四章：构建应用协议

尽管以太坊的原始愿景是一个单一的公共区块链，作为“世界电脑”，但现实要复杂得多。现在很清楚，单一的公共区块链无法扩展到支持大规模消费者应用所需的容量。以太坊本身正在朝着多个互联的区块链方向发展，用于分片和状态通道（有关侧链的更多信息，请参见第十三章）。实际上，一个很有吸引力的分片想法是根据业务应用将计算负载分配到各种区块链上。例如，可以有一个专注于电子商务的区块链，另一个专注于赌博游戏，还有一个专注于支付和稳定币的区块链。这些专业区块链被称为*应用协议*区块链。

我预见一个由众多互联的应用协议区块链组成的世界，每个区块链都配备了专门优化的虚拟机，以高效处理某一类型的应用。以太坊协议将通过为所有这些专门化和优化的区块链提供互操作性层而蓬勃发展。

实际上，在企业软件工程的历史中，成功的产品总是针对其特定的应用用例进行优化的。一刀切的方法行不通。在这本书的这部分，我将讨论如何为特定的应用协议开发优化的区块链。在这本书中，我们将使用 Second State 开发的开源软件来定制和优化以太坊平台，包括对 Solidity 的 Lity 语言扩展([www.LityLang.org](http://www.LityLang.org))。我们还将以 CyberMiles 公共区块链([www.CyberMiles.io](http://www.CyberMiles.io))作为一个案例研究。CyberMiles 公共区块链与以太坊完全兼容，但针对电子商务应用进行了优化。

## 14. 扩展以太坊协议

在这本书的前几章中，你了解了以太坊的力量以及它的局限。以太坊是第一个，当然也是最流行的区块链智能合约平台之一。它是一个有社区提供的多个开源实现的协议，并且有一个健全的软件升级过程，称为以太坊改进提案（EIPs）。然而，作为一个拥有许多利益相关者的大家庭，以太坊的改进是一个缓慢的过程。作为“世界电脑”，以太坊也不太可能针对特定应用进行优化。

我相信有许多不同的公共区块链都有机会。每个它们都将优化以太坊以适应特定的应用协议。然而，它们都需要至少解决以太坊在这里描述的最为突出的几个问题：

+   以太坊虚拟机（EVM）存在许多局限性。虽然 EVM 是图灵完备的，但实现许多算法效率低下。例如，目前在以太坊上实现公私钥应用是不可能的，因为一次公钥基础设施（PKI）加密操作将消耗价值数百美元的以太坊燃料费。即使是基本字符串操作，在标准 EVM 上也慢且昂贵。

+   以太坊太慢了。大约每秒 20 笔交易（智能合约交易更少），以太坊不适用于大多数应用场景。

+   它尚未实现可扩展。在 2019 年的以太坊公有区块链上，使用它的人越多，用户体验就越差。

+   这可能会存在安全隐患，尤其是对初学者来说。很容易因为地址写错而将以太坊资产发送到错误的地方，或者因为智能合约编写不当而丢失资产。

+   智能合约编程是困难的。代码审计显示，以太坊智能合约平均每 1000 行代码就有大约 100 个明显的错误。这对于管理金融资产的应用来说是一个惊人的数字。相比之下，微软的商业应用程序，其关键性远小于以太坊，平均每 1000 行代码大约有 15 个错误。

在本章中，我概述了可能有助于缓解以太坊这些不足的技术方法。

### 完全兼容，然而更快

第二状态创造了可以运行在多种底层共识机制上的以太坊兼容虚拟机。这使得开发者可以选用最适合部署应用的区块链。例如，该虚拟机可以作为 Tendermint 应用运行（参见第二十章），以利用拜占庭容错（BFT）Tendermint 共识引擎，以及可以在 Tendermint 之上实现的各类委托证明-权益（DPoS）机制（例如，CyberMiles 公有区块链）。

以太坊的性能瓶颈主要是其工作量证明（PoW）共识机制所导致的。每个可以添加到区块链的数据块都需要执行大量无意义的计算。一个以太坊兼容的区块链仅通过将 PoW 模块替换为 DPoS 或委托拜占庭容错（DBFT）模块，就能轻松实现 100 倍的性能提升。例如，在 CyberMiles 区块链上，在创建新块之前，需要 19 个验证节点（即超级节点）达成共识。这些验证节点由 CyberMiles 代币持有者选举产生，并需在一流的数据中心运行高性能硬件。

**注意**

作为以太坊兼容的，所有以太坊可扩展性解决方案也适用于基于 EVM 的区块链。这使用户能够利用以太坊社区进行的大量研究，并将改进贡献给以太坊社区。这里的典型例子是 Plasma 协议，其旨在构建第二层网络，使以太坊能够扩展到每秒数百万笔交易。

此外，正如我们在下一节中讨论的，虚拟机可以将复杂的计算任务卸载到本地方法库函数。这允许智能合约执行速度大幅提高，并为此类任务大幅降低燃气成本。对于许多操作，本地方法可能代表性能提升四个到六个数量级（更多内容参见第十八章）。

### Smart Enhancements to the EVM

Lity 是 Solidity 的新编程语言扩展，支持在扩展的 EVM 版本中其特性。以下是 Lity 的一些特性：

+   Lity 提供了一个新的语言关键字，用于调用用 C 或 C++编写的本地方法库函数。这被称为 libENI 框架。通过 libENI，每个基于 Lity 的区块链都可以根据特定地址的应用场景进行定制和优化。我将在第十八章中讨论 libENI。

+   Lity 支持固定点数学和复杂的数学运算。它为分数数运算提供了确定性的结果，这是以太坊的一个关键限制。

+   Lity 支持基于定时器的未来时间安排的操作。计划执行对于许多用例类至关重要，例如利息和股息支付、信托和遗嘱、交货确认等。这也被称为*长期运行合约*。

+   Lity 支持“可信”操作，只能由底层区块链的当前验证者或超级节点调用。这允许在区块链上实现可信的智能合约，为社区基础的预言机提供一等替代品，将区块链连接到外部世界。

+   Lity 支持由底层区块链的验证者或超级节点生成的安全随机数。

+   Lity 支持在需要执行智能合约时支付燃气费用的区块链上的替代机制。

+   Lity 支持一种新的“可升级”智能合约。这些合约只向合约地址公开函数接口。这些函数的实际实现是部署在区块链上其他地址的代理合约。Lity 支持虚拟机操作来更改智能合约的代理实现。这允许开发者升级或修复智能合约中的关键错误。

+   Lity 支持如规则表达式等新语言构造，以便应用开发者可以直接在智能合约中构建业务规则（参见第十七章）。这些通常被称为*领域特定语言*（DSL）特性。

接下来，让我们看看这个列表中的一些具体例子。

#### 可信预言机

区块链上最重要的服务之一是预言机服务。一个*预言机*通常是一个智能合约，它使外部数据（即链下、现实世界或跨链数据）在区块链上确定性地可用。它为链下状态提供了一个真相来源，从而使区块链节点能够达成共识。

传统的预言机高度集中，与去中心化区块链的精神相悖。例如，Fedex 可能会建立一个交付服务预言机，提供包裹的交付状态。一个气象站可能会建立一个气象预言机。要使用这些预言机，区块链用户和 dapp 必须信任这些预言机背后的实体。

第二种预言机的方法是创建一个基于社区的加密经济游戏，让社区成员在智能合约中竞争并提供真相。此类预言机的例子包括提供比特币区块链信息的 BTC Relay，以及提供时间的以太坊闹钟。

然而，Lity 采取了不同的方法来创建可信的智能合约，并使预言机成为一等公民。这种方法适用于 DPoS 区块链。在 DPoS 区块链中，验证者（超级节点）是可信实体。他们必须质押大量来自他们自己账户和他们的支持者/社区的代币。如果验证者行为不端，这些代币可能会被削减和没收。因此，如果一个智能合约只能由当前的验证者更新，那么这个合约中的数据在 DPoS 区块链上应该具有很高的信任度。

在 Lity 语言中，有一个内置函数`isValidator`，用于检查当前交易发送者/函数调用者是否是验证者。它在任何基于 Lity 的 DPoS 区块链上都能工作。

请点击这里查看代码图片

```
// isValidator is a built-in function provided by Lity.
// isValidator only takes one parameter, an address,
// to check this address is a validator or not.
isValidator(<address>) returns (bool returnValue);
```

然后，利用`ValidatorOnly`修饰符，我们可以在区块链上构建作为可信预言机的智能合约。

请点击这里查看代码图片

```
contract BTCRelay {
  uint[] BTCHeaders;
  modifier ValidatorOnly() {
      require(isValidator(msg.sender));
      _;
  }

  function saveBTCHeader(uint blockHash) ValidatorOnly {
    BTCHeaders.append(headerHash);
  }

  function getBTCHeader(uint blockNum) pure public returns (uint) {
    return BTCHeaders[blockNum];
  }
}
```

#### 安全随机数

获取安全随机数对于区块链智能合约来说是一个重大挑战。Lity 开创了一种方法，从当前区块头的种子中访问随机数系列。随机种子基于当前区块中所有交易的哈希，即使对于构建和提出区块的验证节点来说，也很难操纵。

在智能合约内部，您可以通过简单地调用内置函数`rand()`来访问随机数系列。以下是一个示例：

请点击这里查看代码图片

```
pragma lity >=1.2.6;

contract RandDemo {
  uint x;
  function getRand () public returns (uint) {
    x = rand();
    return x;
  }
}
```

你不应该在`view`或`pure`函数中调用`rand()`。如果随机数不需要记录在区块链上（即，在单个节点上执行的`view`函数中的交易之外），它不需要由区块链生成。调用应用程序应该简单地在本地生成一个随机数，这在资源消耗方面要便宜得多。

#### 替代燃料费

区块链应用采纳的主要障碍之一是要求终端用户支付燃料费以在区块链上执行某些功能。燃料机制对区块链的安全至关重要，因为它防止 DoS 攻击者通过计算密集型请求淹没区块链节点。然而，燃料要求也意味着新的终端用户在使用去中心化应用之前必须先被教会购买加密货币和管理私钥。

Lity 为将新用户引入区块链应用提供了一种替代方法。通过`freegas`关键字，智能合约所有者可以指定一个应由所有者本人支付燃料费的合约函数。当用户调用这些函数时，她会表明她没有支付燃料费，通过将`gasPrice`设置为 0。

+   如果`gasPrice=0`的交易调用了一个不是`freegas`的函数，交易将会失败。

+   如果`gasPrice=0`的交易调用了一个没有余额的合约中的`freegas`函数，交易将会失败。

当然，调用者可以指定一个常规的`gasPrice`（例如，2Gwei），在这种情况下，即使合约函数是`freegas`，调用者也需要支付燃料费。

如果`gasPrice=0`的交易调用了一个余额充足的合约中的`freegas`函数，那么该函数将执行，并且燃料费将从合约地址扣除。调用者不用支付任何费用，合约按照系统标准的燃料价格支付燃料费。

**注意**

对于`gasPrice=0`的交易有一个可配置的速率限制。区块链节点软件可以防止用户通过发送大量免费交易来利用系统。

以下是一个示例。在 CyberMiles 区块链上，如果一个终端用户用`gasPrice=0`调用测试函数，并且合约地址有 CMT 余额，那么交易的燃料费将来自合约地址。

点击此处查看代码图片

```
pragma lity >= 1.2.7;

contract FreeGasDemo {
  int a;
  function test (int input) public freegas returns (int) {
    a = input;
    return a;
  }

  function () public payable {}
}
```

`payable`函数很重要，因为它允许合约接收稍后用作燃料的资金。 图 14.1 展示了在 CyberMiles 公共区块链上`freegas`交易的运作情况。

![image](img/yuan_f14_01.jpg)

**图 14.1** 调用者通过将`gasPrice`设置为零来发起一个`freegas`交易。

### 安全第一

通过在 Lity 中进行语言和虚拟机增强，我们可以主动预防许多安全问题的类别。以下是一些示例：

+   Lity 编译器会自动检查它编译的智能合约的结构签名。如果检测到智能合约很可能是流行类型之一（例如，一个 ERC20 或 ERC721 代币合约），它会检查是否实现了所有必需的方法，并且合约没有常见的错误。如果看到一个不符合规定的 ERC20 合约，Lity 编译器会抛出错误（在第十五章了解更多）。

+   Lity 编译器检查已知的代码问题和错误模式，例如 ERC20 合约对 ERC223 安全标准的遵守。它会发出警告，并尝试自动修复一些最严重的问题。

+   Lity 语言提供了对由区块链验证者生成的安全随机数的访问，当共识机制允许时。

+   Lity 虚拟机在运行时自动检查不安全操作，例如整数溢出，这是 ERC20 常见的导致数十亿美元价值毁灭的问题。当在 Lity 运行时合约遇到整数溢出时，它会停止执行并抛出错误，而不是像以太坊今天那样继续处理溢出的缓冲区。这消除了一类错误。

作为一个开源的协作努力，Lity 项目旨在持续向社区带来更新，例如支持新的 ERCs 和新的代码漏洞模式等安全特性。

### 结论

在本章中，我讨论了 Lity 项目如何扩展以太坊协议，既在共识层也在虚拟机层，以创建支持性能/安全性/易用性改进以及实验性特性的以太坊兼容区块链。在接下来的几章中，我们将深入探讨在 Lity 语言和虚拟机上进行应用设计和开发。

## 15. 扩展以太坊工具

在上一章中，你看到了 Lity 语言和虚拟机如何扩展和改进以太坊协议。开源的以太坊生态系统也鼓励这样的平台扩展和分叉现有工具以整合新特性。

Lity 工具包括钱包、区块链浏览器和编码/部署工具。这些工具针对每个区块链进行定制和配置，并由商业提供商支持，例如 Second State（[www.SecondState.io](http://www.SecondState.io)）。

在本章中，我将介绍适用于 CyberMiles 公共区块链的 Lity 定制工具。它们包括以下内容：

+   Venus 浏览器扩展是 CyberMiles 对 Metamask 以太坊钱包的扩展。

+   Europa 集成开发环境（IDE）是 Lity 和 CyberMiles 分叉的以太坊 Remix IDE。

+   web3-cmt.js 库是支持 CyberMiles 区块链上 CMT 加密货币的定制 web3 库。它可以定制为任何基于 Lity 的区块链。

+   CyberMiles App（又名 CMT 钱包）是一个移动钱包应用程序，可以在钱包内运行 CyberMiles dapps。

+   `lityc`项目提供了分析和安全 Lity 智能合约源代码的工具。

+   区块链浏览器 Web 服务提供了一个查询和搜索界面，用于查询基于 Lity 的区块链的数据。在 CyberMiles 上，这项数据服务可在[www.CMTTracking.io](http://www.CMTTracking.io)获得。

**注意**

使用 Second State 的 BUIDL 在线 IDE（[`buidl.secondstate.io`](http://buidl.secondstate.io)），您可以在活区块链上尝试最新的 Lity 功能。无需处理加密货币或燃料费或事件钱包，只需 Lity 合约和 web3 JavaScript 应用程序。在第三章了解更多。

### Smart Contract Tools

在本节中，我将回顾如何使用 Europa 在线 IDE 以及 Venus 钱包在 CyberMiles 区块链上开发和部署智能合约。

#### Venus Wallet

Venus 钱包（图 15.1）是 Chrome 浏览器的一个扩展程序，用于管理您的 CyberMiles 区块链账户。它基于开源的 Metamask 软件。它存储和管理您在这些账户上的计算机上的私钥（即私钥钱包，以及由此扩展的在这些账户中存储的加密货币）。对于开发者来说，Venus 是一个很好的工具，因为它与其他开发工具集成，并允许您与 CyberMiles 账户互动。

![image](img/yuan_f15_01.jpg)

**图 15.1** Venus 钱包基于开源的 Metamask 项目。

首先，请确保您已安装最新版本的 Google Chrome 浏览器。您可以在[`www.google.com/chrome/`](https://www.google.com/chrome/)获取它。

接下来，按照 CyberMiles 网站上的说明在您的 Chrome 浏览器上安装 Venus：[`cybermiles.io/venus`](https://cybermiles.io/venus)。

现在，您应该在 Chrome 工具栏上看到 Venus 图标。点击它以打开其用户界面（UI）。您应该为您的 Venus 钱包创建一个密码。这很重要，因为您的密码保护存储在这台计算机上的账户私钥。创建密码后，Venus 将为您提供一个 12 个单词的恢复短语。这是您恢复密码的唯一方式，所以要妥善保管！

出于开发目的，从 Venus UI 的左上角下拉列表中选择，并选择 CyberMiles Testnet，这是用于测试目的的 CyberMiles 公共区块链。

您还需要在测试网上创建一个账户来存储您的测试网 CMT。在 Venus UI 的右上角点击图标，然后点击**创建账户**。Venus 将为您创建一个账户地址及其关联的私钥。您可以给这个账户命名，以便稍后可以在 Venus UI 中访问。您还可以使用 Venus 管理主网 CMT，这些 CMT 可以在交易所兑换成美元。但要做到这一点，您应该确保您的计算机物理安全，因为真实货币将面临风险。

当然，您仍然需要用一些测试网 CMT 为您的账户注资以使用它。访问公共 CyberMiles 测试网水龙头[`travis-faucet.cybermiles.io/`](https://travis-faucet.cybermiles.io/)并为您的地址请求 1,000 个测试网 CMT！测试网 CMT 只能在测试网上使用。它们在任何交易所上都不会交易，并且当测试网退役时随时可能消失。与主网 CMT 不同，测试网 CMT 没有货币价值。

现在您已经设置了 Venus，准备好与 CyberMiles 测试网上的第一个智能合约进行交互了！

#### Europa IDE

Europa IDE 基于 Ethereum 区块链上的 Remix 但为 CyberMiles 进行了定制。Europa 是完全基于 web 的。只需访问其网站即可加载 web 应用：[`europa.cybermiles.io/`](http://europa.cybermiles.io/)。

在右侧的代码编辑器中，让我们输入一个简单的智能合约。以下是`HelloWorld`智能合约的示例。它用 Solidity/Lity 编写。

点击此处查看代码图片

```
pragma solidity ⁰.4.17;

contract HelloWorld  {

    string helloMessage;
    address public owner;

    constructor () public {
        helloMessage = "Hello, World!";
        owner = msg.sender;
    }

    function updateMessage (string _new_msg) public {
        helloMessage = _new_msg;
    }

    function sayHello () public constant returns (string) {
        return helloMessage;
    }
 function kill() public {
        if (msg.sender == owner) selfdestruct(owner);
    }
}
```

`HelloWorld`智能合约有两个关键方法。

+   `sayHello()`方法向其调用者返回一个问候。当智能合约部署时，问候被初始化为“Hello, World!”。

+   `updateMessage()`方法允许调用者将问候从“Hello, World!”更改为另一条消息。

在右侧面板中点击**开始编译**按钮（图 15.2）以编译此合约。这将生成稍后使用的字节码和应用程序二进制接口（ABI）。当您点击 ABI 或字节码按钮时，ABI 或字节码将被复制到计算机的剪贴板，稍后您可以在其他文件或应用程序中粘贴它们。

![image](img/yuan_f15_02.jpg)

**图 15.2** 在 Europa 上编译 CyberMiles 智能合约

接下来，在 Europa 的 Run 标签页上，您可以通过 Injected Web3 下拉框将 Europa 连接到您的 Venus 账户。Europa 将自动检测您当前选择的 Venus 账户。

您现在应该看到将智能合约部署到区块链的选项。点击**部署**按钮将合约部署到区块链。合约将在 CyberMiles 测试网上部署。此时，Europa 会弹出，要求您从您的账户地址发送“燃料费”（图 15.3）。燃料费是 CyberMiles 区块链要求支付部署您合约所需的网络服务费。

![image](img/yuan_f15_03.jpg)

**图 15.3** 支付部署合约的燃料费

提交请求后，请等待几分钟，让 CyberMiles 网络确认您的合约部署。合约部署的地址将在确认信息中显示（图 15.4），部署的合约及其可用方法也将在 Europa Run 标签页中可用。

![image](img/yuan_f15_04.jpg)

**图 15.4** 合约现已部署，展示了可用方法。

如果您已经在测试网上部署了智能合约，您已经知道合约的部署地址。您只需在 At Address 按钮旁边的框中输入合约地址，然后点击按钮。这将配置 Europa 以使用已经部署的合约。在这种情况下无需支付燃料费。

一旦 Europa 连接到您部署的合约，它会在运行标签上显示合约方法。您可以在 updateMessage 按钮旁边输入一个新的问候语，然后点击按钮更新消息(图 15.5)。由于区块链存储需要存储更新的消息，您将再次被提示通过 Venus 支付燃料费。

![image](img/yuan_f15_05.jpg)

**图 15.5** 调用`updateMessage()`方法

一旦网络确认了消息更新，您将再次看到一条确认信息。在`updateMessage()`被确认之后，您可以从 Europa 调用`sayHello()`(图 15.6)，然后您将看到更新的消息。

![image](img/yuan_f15_06.jpg)

**图 15.6** 调用`sayHello()`方法

Europa IDE 易于使用。它是初学者的优秀选择。你还可以通过每个节点的命令行工具与区块链互动。节点软件提供更多功能，我们将在本章后面讨论。

#### `lityc`编译器和分析工具

`lityc`软件扩展了以太坊`solc`，提供了一个 Lity 语言的编译器。它将 Lity 智能合约编译为 ABI 和字节码。然后您可以使用 Travis 节点控制台或 web3-cmt.js 将 ABI 和字节码部署到 CyberMiles 公共区块链作为智能合约。请参阅附录 A 以获取更多详细信息。

虽然编译和部署也可以在 Europa 等工具中完成，但命令行`lityc`的一个更有趣的功能是其源代码静态分析器。例如，`lityc`编译器可以检查合约是否符合特定的 ERC 规范。让我们考虑下面的合约。`totalSupply()`函数不符合 ERC20 规范。

点击此处查看代码图片

```
pragma lity ¹.2.4;
contract ERC20Interface {
  // mutability should be view, not pure
  function totalSupply() public pure returns (uint);
  function balanceOf(address owner) public view returns (uint);
  function allowance(address owner, address spender)
                               public view returns (uint);
  function transfer(address to, uint tokens) public returns (bool);
  function approve(address spender, uint tokens) public returns (bool);
  function transferFrom(address from, address to,
    uint tokens) public returns (bool);
 event Transfer(address indexed from, address indexed to, uint tokens);
  event Approval(address indexed owner, address indexed spender, uint tokens);
}
```

运行`lityc`编译程序会显示以下错误信息：

点击此处查看代码图片

```
$ lityc --contract-standard ERC20 wrong_mutability.sol

wrong_mutability.sol:3:1: Info: Missing 'totalSupply' with
type signature 'function () view external returns
(uint256)'. ERC20Interface is not compatible to ERC20.
contract ERC20Interface {
^ (Relevant source part starts here and spans across multiple lines).
```

截至本文写作时，`lityc`支持以下 ERC 规范，并且定期增加更多：

+   ERC20

+   ERC223

+   ERC721

+   ERC827

+   ERC884

此外，如果您在计算机上安装了 Oyente 静态分析工具，`lityc`在编译时可以自动运行 Oyente。以下代码为例：

点击此处查看代码图片

```
$ lityc --abi StringReverse.sol

======= StringReverse.sol:StringReverse =======
Contract JSON ABI
[…]

INFO:root:contract StringReverse.sol:StringReverse:
INFO:oyente.symExec:    ============ Results ===========
INFO:oyente.symExec:      EVM Code Coverage:                     29.8%
INFO:oyente.symExec:      Parity Multisig Bug 2:                 False
INFO:oyente.symExec:      Callstack Depth Attack Vulnerability:  False
INFO:oyente.symExec:      Transaction-Ordering Dependence (TOD): False
INFO:oyente.symExec:      Timestamp Dependency:                  False
INFO:oyente.symExec:      Re-Entrancy Vulnerability:             False
INFO:oyente.symExec:    ====== Analysis Completed ======
```

Oyente 是一个开源项目，它正在积极开发和更新，以检测智能合约源代码的更多问题模式。Oyente 与`lityc`的集成可能会推动区块链应用中静态分析工具的采用。

### Dapp Tools

虽然 Europa 是一个很好的工具，但对于普通人来说太难了。为了让你的智能合约对大众可用，你通常需要构建一个基于 web 的用户界面。为此，你需要 web3-cmt.js JavaScript 库与 CyberMiles 区块链交互。

从这一点开始，我假设您已经成功将之前的`HelloWorld`合约部署到大米链主网，并记录了其部署的合约地址。原因是大米链应用（CMT 钱包）的生产版本只与大米链主网合约（参见“大米链应用”部分）一起使用。

#### web3-cmt

一旦安装了 Europa，它将自动向页面的 JavaScript 上下文中注入`web3`对象的自定义实例（或`web3.cmt`对象）。需要私钥的方法调用将自动提示用户选择一个账户，MetaMask 将使用选定的私钥签署交易，然后将其发送到以太坊网络。此外，所有 web3 API 调用都必须是异步的。所以，我们使用 web3 回调 API 来处理返回值。`helloworld_europa.html`文件的源代码如下：

点击此处查看代码图片

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <script>
      window.addEventListener('load', function() {
        var hello = web3.cmt.contract(...).at("...");

        var new_mesg = location.search.split('new_mesg=')[1];
        if (new_mesg === undefined || new_mesg == null) {
        } else {
          new_mesg = decodeURIComponent(new_mesg.replace(/\+/g, '%20'));

          web3.cmt.getAccounts(function (error, address) {
            if(!error) {
              hello.updateMessage(new_mesg, {
                  from: address.toString()
              }, function(e, r){
                if(!e)
                  document.getElementById("status").innerHTML =
                    "<b>Submitted to blockchain</b>. " +
                    "New message will take a few seconds to show up! " +
                    "<a href=\"helloworld_europa.html\">Reload page.</a>";
              });
            }
          });
        }
 hello.sayHello(function(error, result){
          if(!error)
            document.getElementById("mesg").innerHTML = result;
        });
      })
    </script>
  </head>

  <body>
  <h2>Hello World</h2>
    <form method=GET>
      New message:<br/><br/>
      <input type="text" name="new_mesg"/><br/><br/>
      <input type="submit"/>
      <p id="status"/>
    </form>
    <p>The current message is: <span id="mesg"/></p>
  </body>
</html>
```

`web3.cmt.contract(...).at("...")`函数将区块链上的合约部署地址作为参数。您可以在 Europa 的运行标签中找到它。`contract`函数采用一个被称为合约的 ABI 的 JSON 结构，您可以从 Europa 复制，如图 15.2 所示。

现在，web 应用允许用户直接从 Web 与`HelloWorld`智能合约交互(图 15.7)。 “提交新消息”操作需要 Europa 发送燃料费，因为它调用了合约上的`updateMessage()`方法。注意所有 web3 函数都是嵌套的，异步调用。

![image](img/yuan_f15_07.jpg)

**图 15.7** 使用 Europa 钱包向合约写入

使用 Europa 与`web3-cmt`一起是目前开始开发 CyberMiles 应用的最佳方式。但对于普通用户来说，安装和使用 Europa 的过程是进入的一个显著障碍。接下来，让我们探索如何在大米链应用（CMT 钱包）移动应用内运行 dapps。

#### 大米链应用

大米链应用是一个消费级别的移动钱包应用，无需复杂安装。您可以在[`app.cybermiles.io/`](http://app.cybermiles.io/)获取大米链应用。

要从 CyberMiles App 运行 dapp，最简单的方法是创建一个由 dapp 的 URL 生成的二维码，然后使用钱包应用程序扫描该 URL。你可以在 [www.qr-code-generator.com/](http://www.qr-code-generator.com/) 为任何 URL 创建一个二维码。**图 15.8** 显示了整个过程。

![image](img/yuan_f15_08.jpg)

**图 15.8** 在 CyberMiles App 中扫描条形码以加载 dapp

另外，dapp 可能位于一个普通的网站上，当需要将交易发送到区块链时，它会重定向到 CyberMiles App。在第十一章中讨论的 FairPlay dapp 是这种情况的一个很好的例子。**图 15.9** 显示了另一个更简单的例子。

![image](img/yuan_f15_09.jpg)

**图 15.9** 使用 CyberMiles App 运行 dapp 和支付燃气费

CyberMiles App 中的 dapp 用户体验是 CyberMiles 优于以太坊的优点之一。

### 结论

在本章中，我回顾了适用于以太坊兼容的 CyberMiles 区块链的工具。我回顾了 CyberMiles 可用的钱包、web3 库以及开发/部署工具。在下一章中，我们将把这些工具结合起来，看看一些使用 Lity 开发并部署在 CyberMiles 公共区块链上的完整示例 dapp。

## 16. 示例 dapps

在前两章中，我讨论了如何扩展以太坊协议和相关开发工具。但是，这些扩展和改进如何转化为现实世界的应用呢？在本章中，我将讨论几个在 CyberMiles 上部署的完整 dapp，以说明以太坊扩展如何使开发者能够为区块链创建互动式 dapp。

本章讨论的一切都与以太坊兼容。但是，正如所讨论的，作为以太坊兼容的开发和部署平台，CyberMiles 提供了一些重要的优势。

+   CyberMiles 的交易确认时间比以太坊快得多。这对于互动式 dapp 用户体验（UX）很重要，因为它减少了操作被确认和记录在区块链上的时间。

+   CyberMiles 有一个移动钱包应用程序，可以在嵌入模式下运行基于 web3 的 JavaScript 应用程序。CMT 钱包在所有 iOS 和 Android 应用商店都可以找到，你可以通过扫描指向 JavaScript 代码的条形码来加载 dapp。

+   CyberMiles 区块链使用 CMT 代币支付燃气费。由于 CMT 价格远低于 ETH，因此可以用更少的钱完成更多任务。

接下来，让我们开始吧。

### 案例研究 1：情人节

情人节 dapp 是为了让人们永久地在区块链上声明和记录他们的爱。通过 CyberMiles App（CMT 钱包），任何人都可以创建一个爱情宣言并分享二维码（见**图 16.1**）。

![image](img/yuan_f16_01.jpg)

**图 16-1** 宣告你的爱

声明的接收者使用她的 CyberMiles App 扫描二维码并打开 DApp。从那里，她可以回复声明。回复后，她可以向世界分享二维码，这样任何人都可以打开 DApp 并见证记录在区块链上的声明和回复(图 16.2)。

![image](img/yuan_f16_02.jpg)

**图 16-2** 回复和见证声明

接下来，让我们回顾一下情人节合约背后的智能合约代码，然后是用于与情人节合约交互的 JavaScript DApp。

#### 情人节智能合约

情人节智能合约包含了从 DApp 提交的所有声明和回复（每一个都是情人节的礼物）。它有两个主要功能：`declare()`用于创建一个新的声明，`reply()`用于回复一个现有的声明。它还有两个信息函数（`view`函数），`getDeclaration()`和`getReplies()`，帮助 DApp 从区块链检索信息。

点击此处查看代码图片

```
contract Valentines {
    struct Declaration {
        string stmt;
        address reply_from;
        string reply_stmt;
    }
    mapping(address => Declaration) declarations;
    mapping(address => address[]) replies;
    function declare (string _stmt) public {
        Declaration memory d = Declaration(_stmt, 0, "");
        declarations[msg.sender] = d;
    }
    function reply (address _from, string _stmt) public {
        declarations[_from].reply_from = msg.sender;
        declarations[_from].reply_stmt = _stmt;
        replies[msg.sender].push(_from);
    }
    function getDeclaration (address _from) public view returns (string,
        address, string) {
        return (declarations[_from].stmt, declarations[_from].reply_from,
            declarations[_from].reply_stmt);
    }
    function getReplies (address _from) public view returns (address[]) {
        return (replies[_from]);
    }
}
```

合约的四个函数都是自解释的。`Declaration`结构包含一个声明及其回复。声明被映射到其在`declarations`映射数组中的创建者。`replies`数组将每个地址映射到它回复的声明。请注意，每个地址可以发表一个声明，但可以回复多个声明。

然后，您可以将合约部署到 CyberMiles 区块链，并记录部署的合约地址。最简单的方法可能是使用 CyberMiles Europa 工具或配置为 CyberMiles 的 Second State BUIDL 工具。JavaScript DApp 访问这个部署的合约。

#### JavaScript DApp

该 DApp 用 JavaScript 编写，在与钱包应用程序结合的客户端浏览器中运行。`declare.js`文件中的`getDeclaration()`函数调用智能合约的`getDeclaration()`函数，然后使用结果更新`declare.html`文件中的 HTML 用户界面（UI）。以下代码片段显示了 JavaScript DApp 中的`getDeclaration()`函数。请注意，所有与 web3 相关的操作都是异步进行的，因为很多都是远程调用，我们必须保证执行的正确顺序。`contract_address`值是在成功部署后提到的合约地址。它被硬编码到 DApp 中。`targetAddress`值是这个声明是从哪个地址发出的。`userAddress`值是当前用户的 CMT 地址。

点击此处查看代码图片

```
var getDeclaration = function () {
    web3.cmt.getAccounts(function (e, address) {
        if (e) {
            // ...
        } else {
            userAddress = address.toString();
            if (!targetAddress) {
                targetAddress = userAddress;
            }
            contract = web3.cmt.contract(abi);
            instance = contract.at(contract_address);
            instance.getDeclaration (targetAddress, function (e, r) {
                if (e) {
                    // ...
                } else {
                    stmt = r[0];
                    reply_from = r[1];
                    reply_stmt = r[2];
                    // show the UI based on the state
                    // of this targetAddress’s declaration
                }
            });
            instance.getReplies (userAddress, function (e, r) {
                if (e) {
                    // ...
                } else {
                    // show replies on UI
                }
            });
        }
    });
}
```

当用户做出选择时，会调用合约的 `declare()` 函数。请注意，由于它会在区块链上保存数据，我们必须支付一点燃料费来调用这个函数。在合约函数调用成功返回后，JavaScript 会等待交易在区块链上被确认（当区块被生产并被验证者接受），然后重新加载 `getDeclaration()` 函数以更新用户界面。

点击此处查看代码图片](Images/ch16_images.xhtml#pro16_3)

```
var declare = function () {
    var v = $("#declaration-field").val();
    if (v == null || v == '') {
        // ...
    }
    $(".main-button").css("background-color", "#696969");
    $('#declaration-submit').text(lgb.wait);
    $('#declaration-submit').removeAttr('onclick');
    instance.declare(v, {
        gas: '200000',
        gasPrice: 2000000000
    }, function (e, result) {
        if (e) {
            // ...
        } else {
            setTimeout(function () {
                getDeclaration();
            }, 20 * 1000);
        }
    });
}
```

当第二个用户回复投注声明时，该 DApp 会调用合约的 `reply()` 函数，在区块链上确认交易后在用户界面上更新信息。

点击此处查看代码图片

```
var reply = function () {
    var v = $("#reply-field").val();
    if (v == null || v == '') {
        // ...
    }
    $(".main-button").css("background-color", "#696969");
    $('#reply-submit').text(lgb.wait);
    $('#reply-submit').removeAttr('onclick');
    instance.reply(targetAddress, v, {
        gas: '200000',
        gasPrice: 2000000000
    }, function (e, result) {
 if (e) {
            // ...
        } else {
            setTimeout(function () {
                getDeclaration();
            }, 20 * 1000);
        }
    });
}
```

到目前为止，我们已经回顾了 Valentines DApp 的核心逻辑以及它是如何通过 web3 与区块链上的数据和函数交互的。该 DApp 使用开源库来执行其他重要任务。例如，它使用 `qrcode.js` 脚本动态生成二维码。它使用 `IUToast` 脚本为用户提供消息和警告。

Valentines DApp 只有一个网页和一个 JavaScript 控制文件。它与已经部署的智能合约交互。在下一节中，我们将研究一个更复杂的 DApp 称为 WeBet。

### 案例研究 2：WeBet

WeBet 去中心化应用（DApp）是一个点对点的投注平台。它允许任何人在 CyberMiles 应用内创建一个投注合约（图 16.3）并分享投注（图 16.4）。投注是一个多选题。

![image](img/yuan_f16_03.jpg)

**图 16-3** 创建一个新的 WeBet 合约

![image](img/yuan_f16_04.jpg)

**图 16-4** 分享 WeBet 合约

其他人可以使用他们自己的 CyberMiles 应用来下注（图 16.5）。他们通过扫描由投注合约创建者分享的唯一二维码轻松找到投注。他们各自选择一个选项，并将 CMT 发送到合约作为对该选项的投注。

![image](img/yuan_f16_05.jpg)

**图 16-5** 在 WeBet 合约上下注

创建者可以在下注后宣布一个获胜选项（图 16.6）。由于多个人可能选择同一个选项，可能有多个赢家。

![image](img/yuan_f16_06.jpg)

**图 16-6** 宣布获胜选项

获胜者使用他们的 CMT 钱包从投注中领取奖金（图 16.7）。

![image](img/yuan_f16_07.jpg)

**图 16-7** 领取 WeBet 奖金

WeBet dapp 的另一个用例是创建“承诺合约”。也就是说，某人可以创建一个个人目标（例如，一个月内减轻 10 磅），并用大量 CMT（例如，10,000 CMT）作为赌注来下注。然后，亲朋好友各自对相反的结果下注一小笔（例如，1 CMT）。如果创建者实现了他的目标，他将得到承诺的 CMT。如果没有，亲朋好友将平分承诺的 CMT。

这类个人投注应用非常适合公链。区块链 dapp 可能会提供比传统 web 应用更好的用户体验。

+   公链上的智能合约确保应用开发者或主机无法通过更改投注记录，甚至携款潜逃来作弊。同样，政府或其他实体也很难关闭这些合约。

+   在区块链上转移“价值”要容易得多。要用法定货币小额投注，你仍然需要整个银行基础设施以及其高昂的费用。在像 CyberMiles 或以太坊这样的成熟公链上，代币与美元有确定的汇率，并且作为支付手段要容易得多，费用也低。

接下来，让我们回顾一下 WeBet 合约背后的智能合约代码，然后是用于与 WeBet 合约交互的 JavaScript dapp。

**注意**

你可能已经注意到，WeBet 合约的所有者必须声明投注的获胜选项。合约所有者能在这里作弊吗？是的，将现实世界的离链信息（即他是否减轻了 10 磅）映射到区块链上总是挑战性的。然而，也需要注意的是，与 WeBet 合约有关的所有信息，包括声明和所有投注，都记录在区块链上，供所有人查看。如果合约所有者作弊，他将永远损害自己的声誉。

我们也可以修改产品，要求多个已知的“仲裁者”在合约所有者的声明生效前验证该声明。然而，那样会使产品更复杂难用。

#### WeBet 智能合约

WeBet 用 Solidity 编写的智能合约的整体结构如下。正如所讨论的，dapp 为每个新的投注合约创建 WeBet 合约的新实例。

点击此处查看代码图片

```
contract BettingGame {

    address public owner;

    struct Bet {
        int8 choice;
        uint256 amount;
        bool paid;
        bool initialized;
    }
    mapping(address => Bet) bets;

    string public game_desc;
    int8 public number_of_choices;
    uint256 public min_bet_amount;
    bool public allow_user_bet_amount;
    uint256 total_bet_amount;
    int8 public total_bet_count;

    mapping(int8 => uint256) choice_bet_amounts;

    int8 public correct_choice;
    string public correct_choice_txt;

    int8 public game_status; // 0 not started; 1 running;
                             //2 stopped; 3 ended; 4 cancelled

    modifier onlyOwner() {
        assert(msg.sender == owner);
        _;
    }

    constructor (string _game_desc, int8 _number_of_choices,
          uint256 _min_bet_amount, bool _allow_user_bet_amount) public {
        require(_number_of_choices > 0);
        require(_min_bet_amount > 0);

        owner = msg.sender;
        game_status = 1;
        game_desc = _game_desc;
        number_of_choices = _number_of_choices;
        min_bet_amount = _min_bet_amount;
        allow_user_bet_amount = _allow_user_bet_amount;

        total_bet_count = 0;
        total_bet_amount = 0;
        correct_choice = -1;
        correct_choice_txt = "";
    }
 function placeBet (int8 _choice) public payable {
        // see later
    }

    function stopGame() external onlyOwner {
        require (game_status == 1);
        game_status = 2;
    }

    function resumeGame() external onlyOwner {
        require (game_status == 2);
        game_status = 1;
    }

    function endGame(int8 _correct_choice, string _correct_choice_txt)
          external onlyOwner {
        correct_choice = _correct_choice;
        correct_choice_txt = _correct_choice_txt;
        game_status = 3;
    }

    function cancelGame() public {
        require (msg.sender == owner || isValidator(msg.sender));
        game_status = 4;
    }
    function payMe () public {
        // See later
    }

    function checkStatus (address _addr) public view returns (int8,
          string, int8, uint256, uint256, bool, int8) {
        // see later
    }

    function getBetInfo()public view returns(int8,string,int8,int8,uint256,bool){
        return (game_status, game_desc, correct_choice, total_bet_count,
          total_bet_amount, allow_user_bet_amount);
    }

    function getAnswer() public view returns (int8, string) {
        return (correct_choice, correct_choice_txt);
    }

    function terminate() external onlyOwner {
        selfdestruct(owner);
    }
}
```

构造函数方法用所有必要的信息创建合约以设置投注。

+   `game_desc`字符串包含投注的标题、描述和所有选项。它们用`;`符号构建成一个字符串，以分隔各个组件。例如，`game_desc`字符串可能如下所示：`bet title;choice 1;choice 2;choice 3`。我们没有以字符串数组的形式传递和存储选项，因为 Solidity 对字符串数组有限制。解析工作留给了 dapp 中的 JavaScript，因为这并不是合约交易逻辑的核心。

+   `number_of_choices`值指定了`game_desc`字符串中包含的选择数量。在我们示例中，将是`3`。这有助于 dapp JavaScript 解析信息组件。

+   `min_bet_amount`值是每个用户必须下注的最低金额，以参与游戏。它的单位是 CMT。

+   `allow_user_bet_amount`值是一个`boolean`变量，用于指定用户是否可以下注超过`min_bet_amount`的金额。

一旦合约创建，`game_status`变量默认为`1`，这意味着下注已经开始了。通过诸如`stopGame()`、`resumeGame()`、`endGame()`和`cancelGame()`等方法，你可以改变游戏状态。这允许合约所有者在宣布赢家之前停止投票。例如，体育博彩应该在现实世界的比赛开始时停止，而真正的赢家将在现实世界比赛结束时宣布。`getBetInfo()`函数返回博彩的基本信息和状态。

合约中的`bets`数组将地址映射到`Bet`。数组中的每个`Bet`结构都是由一次下注创建的。它包含了下注者的选择、她下注的金额以及如果她赢了，她是否已经领取了她的奖金。下注者的地址是`bets`数组中的关键。

合约中的`choice_bet_amounts`数组将每个选择映射到其汇总下注金额（以 CMT 为单位）。它允许轻松计算每个下注地址的赢面。`checkStatus()`函数由 dapp 调用，以检查当前用户地址的博彩状态和赢面。

请点击此处查看代码图片

```
function checkStatus (address _addr) public view returns (int8, string,
      int8, uint256, uint256, bool, int8) {
    safeuint payout = 0;
    if (game_status == 3 && bets[_addr].choice == correct_choice) {
        payout = bets[_addr].amount * total_bet_amount / choice_bet_amounts[correct_choice];
    } else if (game_status == 4) {
        payout = bets[_addr].amount;
    }
    return (game_status, game_desc, bets[_addr].choice,
      uint256(bets[_addr].amount), uint256(payout),
      bets[_addr].paid, correct_choice);
}
```

整个合约中的关键功能是`placeBet()`函数。任何想要在这个合约上下注的用户都会调用这个函数。这个函数是`payable`的，意味着用户可以附带支付来进行调用。这个支付就是下注的金额。它至少要满足`min_bet_amount`。一旦下注，合约的`bets`和`choice_bet_amounts`数组都会更新。

请点击此处查看代码图片

```
function placeBet (int8 _choice) public payable {
    require (game_status == 1); // game is running
    require (_choice <= number_of_choices); // Valid choice
    require (msg.value >= min_bet_amount); // Meet min bet amount
    require (bets[msg.sender].initialized == false); // Only bet once

    Bet memory newBet = Bet(_choice, msg.value, false, true);
    bets[msg.sender] = newBet;

    choice_bet_amounts[_choice] = choice_bet_amounts[_choice] + msg.value;
    total_bet_amount = total_bet_amount + msg.value;
    total_bet_count += 1;
}
```

用户通过从她的下注地址调用`checkStatus()`函数来检查她的奖金。如果用户赢了，她可以通过调用`payMe()`函数从合约中获取支付。注意，如果`game_status`表明所有者取消了博彩，每个下注者都将退款。

请点击此处查看代码图片

```
function payMe () public {
    require (bets[msg.sender].initialized); // Must have a bet
    require (bets[msg.sender].amount > 0); // More than zero
    require (bets[msg.sender].paid == false); // chose correctly

    if (game_status == 3) {
        // game ended normally
        require (bets[msg.sender].choice == correct_choice);
        uint256 payout = bets[msg.sender].amount * total_bet_amount /
          choice_bet_amounts[correct_choice];
        if (payout > 0) {
            msg.sender.transfer(uint256(payout));
            bets[msg.sender].paid = true; // cannot claim twice
        }
    } else if (game_status == 4) {
        // Just refund the bet
        msg.sender.transfer(uint256(bets[msg.sender].amount));
        bets[msg.sender].paid = true; // cannot claim twice
    } else {
        require (false); // Just fail
    }
}
```

Solidity 智能合约故意设计得很简单。它主要处理重要的应用状态和“资金”（即在此情况下的 CMT）的自动转移。它是 JavaScript dapp 的后端服务。

#### WeBet JavaScript 应用程序

WeBet dapp 是一个可以在 CyberMiles App 内执行或在启用了 CyberMiles Venus（CMT 的 Metamask 扩展）的 Chrome 浏览器内执行的 JavaScript 应用程序。在`browser.js`文件中，我们测试`web3.cmt`对象是否为`nil`。如果是，用户将被引导在移动设备上安装 CMT 钱包或在 PC 上安装 Venus Chrome 扩展，然后重新启动 dapp。

由于 dapp 只是一个静态 JavaScript 和 HTML 文件的集合，这些文件可以由任何匿名 Web 服务器提供，甚至可以捆绑在设备客户端内部。不需要中心服务器来管理应用程序状态。在我们示例中，dapp 文件从[`webet.codeislaw.co/`](http://webet.codeislaw.co/)提供。

##### 创建新的 WeBet 合约

在 dapp 中的`start.html`和`start.js`文件协同工作，支持新 WeBet 合约的创建和部署。HTML 文件捕获用户关于合约细节的输入（例如，标题，选项，最低投注金额），而 JS 文件在区块链上创建合约。以下是`start.js`脚本的初始化代码：

点击此处查看代码图片](Images/ch16_images.xhtml#pro16_12)

```
$(function () {
    webBrowser.openBrowser();
    getAbi();
    getBin();
    initLanguage();
    initUserAddress();
    // ...
});

var initUserAddress = function () {
    var interval = setInterval(function () {
        web3.cmt.getAccounts(function (e, address) {
            if (address) {
                userAddress = address.toString();
                $("#userAddress").val(address);
                userAddress = address;
                tip.closeLoad();
                clearInterval(interval);
            }
        });
    }, 300);
}
```

注意，所有与区块链相关的操作都是异步完成的。应用程序显示一个加载器，并要求用户在发现用户从钱包中获取当前账户地址时等待。当用户点击提交按钮以创建 WeBet 合约时，`startGame()`JavaScript 函数映射到点击事件。

点击此处查看代码图片

```
var startGame = function () {
    var inputs = document.getElementsByName("choice");
    var numChoices = 0;
    var gameDesc = '';

    for (var i = 0; i < inputs.length; i++) {
        if (inputs[i].value != null && inputs[i].value != '') {
            var inputValue = inputs[i].value
            gameDesc += inputValue.trim() + ";";
            numChoices++;
        }
    }
    var title = $("#title").val();
    var betMinAmount = $("#betMinAmount").val();
    var allowUserBet = $("#allowUserBetCheckbox").val();
    var allowUserBetAmount = false;
    var minBetAmount = web3.toWei(betMinAmount, "cmt");
gameDesc = gameDesc.replace(/(^;)|(;$)/g, "");
    // deploy and start the game
    var contract = web3.cmt.contract(betAbi);
    var feeDate = '0x' + contract.new.getData(gameDesc, numChoices - 1,
      minBetAmount, allowUserBetAmount, {data: betBin.object});
    web3.cmt.estimateGas({data: feeDate}, function (e, returnGas) {
        var gas = '1700000';
        if (!e) {
            gas = Number(returnGas * 2);
        }
        contract.new([gameDesc, numChoices - 1, minBetAmount,
              allowUserBetAmount], {
            from: userAddress.toString(),
            data: feeDate,
            gas: gas,
            gasPrice: '2000000000'
        }, function (e, instance) {
            if (e) {
                tip.close();
                tip.error(lang.tip.createFailed);
            } else {
                contract_address = instance.address;
                // ...
                setTheContractAddressAndTurn(instance);
            }
        });
    });
};
```

除了常规输入验证和处理代码之外，函数的主要部分嵌套在两个异步块中。`estimateGas()`函数请求连接的区块链节点估计创建此合约所需的燃气费。由于估计有时过于保守，所以我们将燃气费乘以 2。请注意，这是*燃气限制*，即用户授权使用的最大燃气量。用户在创建合约时只会有实际使用的燃气费。然后，`contract.new()`函数向合约的`constructor()`函数传递信息，并异步返回新创建的合约地址。

dapp UI 在成功创建并返回合约地址之前显示加载器。然后调用`setTheContractAddressAndTurn()`函数导航到投注屏幕。

点击此处查看代码图片](Images/ch16_images.xhtml#pro16_15)

```
var setTheContractAddressAndTurn = function (result) {
    if (result != null && (result.contractAddress != 'undefined'
          || result.address != 'undefined')) {
        tip.right(lang.bet.betCreated);
        setTimeout(function () {
            var turnAddress = result.contractAddress;
            if (turnAddress == 'undefined') {
                turnAddress = result.address
                saveLocalStorageBet(turnAddress);
            }
            console.log(turnAddress);
            window.location.href = './join.html?contract=' + turnAddress;
        }, 2000);
    }
};
```

现在 dapp 导航到`join.html`屏幕。带有合约地址的 URL 是其他人通过他们的 CyberMiles App（CMT 钱包）从他们的 CyberMiles App 访问这个赌注的方式。`join.html`屏幕可以创建一个二维码与朋友和潜在的下注者分享。

##### 下注选择

`join.html`和`bet.js`文件协同工作来呈现投注 UI。`getGameStatus()`函数从合约的`checkStatus()`函数检索信息。它是一个`pure view`函数，因此无需燃料即可操作。一旦 JavaScript `getGameStatus()`函数收到结果，它解析标题、选项、当前选项、当前投注和用户的奖金状态，然后将这些信息项显示在`join.html`屏幕上。我不会在这本书中重复这段代码，因为它很长，但你可以 在源代码列表中看到它。

当用户提交她的投注时，会调用`confirmOptionSubmit()`函数。在估计燃料后，它异步调用合约的`placeBet()`函数。投注作为可支付`placeBet()`函数的值发送到合约。

点击此处查看代码图片

```
var confirmOptionSubmit = function () {
    var amount = $("#minBetAmount").val();
    var selectedValue = $("#selectedValue").val();
    // ... validate game status ...
    var allowBet = $("#allowUserBetAmount").val();
    if (allowBet == 'true') {
        var betAmount = $("#SubmitValue").val();
        betAmount = onlyNumber(betAmount);
        if (betAmount <= 0 || betAmount < amount) {
            tip.error(lgb.tip.moreThanZero);
            return;
        }
        amount = betAmount;
    }

// change the submit button color and event

    var feeData = instance.placeBet.getData(selectedValue + "");
    var amountStr = String(web3.toWei(amount, "cmt"));
    web3.cmt.estimateGas({
        data: feeData,
        to: contract_address,
        value: amountStr
    }, function (error, gas) {
        var virtualGas = '20000000';
        if (error) {
            console.log("error estimating gas");
        } else {
            virtualGas = gas;
        }
        instance.placeBet(selectedValue, {
            value: web3.toWei(amount, "cmt"),
            gas: virtualGas,
            gasPrice: 2000000000
        }, function (e, result) {
            if (e) {
                // ...
            } else {
                showUserChoice(gameStatus, userChoice, correctChoice);
                $("#msg").html(lgb.bet.pendingBet);
                $('#msg').css('display', 'block');
                getGameStatus('bet');
            }
        });
    });
}
```

一旦`placeBet()`函数调用返回，dapp 不会等待交易被确认。它只是继续更新 UI，显示当前选中的选项和显示投注已提交的消息。每十秒刷新一次`getGameStatus()`函数来获取区块链的最新信息。一旦交易在区块链上被确认，消息将更改为显示投注已被记录。

##### 声明胜利选项

当`bet.js`脚本从 WeBet 智能合约中显示信息时，它会确定是否显示所有者的控制选项，例如停止投注或宣布胜利选项等选项。

点击此处查看代码图片

```
web3.cmt.getAccounts(function (e, address) {
    // ...
    contract = web3.cmt.contract(betAbi, contract_address);
    instance = contract.at(contract_address);
instance.checkStatus(userAddress, function (gameError, result) {
// ...
        instance.owner(function (e, owner) {
            if (owner && owner.toLowerCase()==userAddress.toLowerCase()) {
                if (gameStatus != 3) {
                    showBetSetting(contentId, afterBtnName,
                      lgb.bet.setting, betSetting);
                }
            }
    });
    });
});

var showBetSetting = function (btnId, afterBtnName, buttonName, betFun) {
    var showColor = "#1976d2";
    if (!document.getElementById(btnId)) {
        fun.addButton(btnId, afterBtnName, buttonName, showColor, betFun);
    }
}
```

当用户触摸所有者按钮时，她会看到一个对话框来声明一个胜利选项。该操作映射到`declareBetGame()`函数。

点击此处查看代码图片

```
var declareBetGame = function () {
    var choiceValue = $("#declareValue").val();
    var dateTime = new Date();
    var desc = "This Bet Game stop at the Time : " +
        dateTime + "and the correct choice is" +
        fun.getLetterByNum(choiceValue);
    if (choiceValue <= 0) {
        tip.error(lgb.tip.selectOption);
        return;
    }
    var feeData = instance.endGame.getData(choiceValue, desc);

    web3.cmt.estimateGas({
        data: feeData,
        to: contract_address
    }, function (error, gas) {
        var virtualGas = '20000000';
        if (error) {
            console.log("error getting gas");
        } else {
            virtualGas = gas;
        }
 instance.endGame(Number(choiceValue), desc, {
            gas: virtualGas,
            gasPrice: 2000000000
        }, function (e, result) {
            if (e) {
                // ...
            } else {
                getGameStatus('declare');
            }
        });
    });
}
```

合约的`endGame()`函数被调用。这允许合约为每个投注参与者计算奖金。远程函数调用返回后，WeBet UI 将刷新。

##### 领取你的奖金

当用户在宣布胜利选项后再次加载 dapp 时，她会看到她的投注选项是否是胜利的那个。如果她赢了，她会看到一个将奖励转入她当前账户地址的选项。

点击此处查看代码图片

```
var showRightChoice = function (contentId, userChoice, correctChoice,
          afterBtnName, withdrawButtonName, statusPaid, payoutAmount) {
    if (userChoice > 0) {
        if (correctChoice == userChoice) {
            if (statusPaid) {
                showWithdrawSuccess(contentId, payoutAmount);
            } else {
                showWithdraw(contentId, afterBtnName,
                  withdrawButtonName, withdraw);
            }
        } else {
            showFailed(contentId);
        }
    } else {
        showNotJoin(contentId);
    }
}

var showWithdraw = function (contentId, afterBtnName, buttonName, betFun) {
    var id = "winner-div";
    var showColor = "#1976d2";
    if (!document.getElementById(id)) {
        fun.addButton(contentId, afterBtnName, buttonName, showColor, betFun);
    }
    var content = '<div class="winner-show">...</div>';
    fun.addDivInnerhtml(domType[0], [attrType[0]], appendType[1],
      content, [id], contentId);
}
```

当用户点击领取奖金的按钮时，合约的`payMe()`函数被调用。

点击此处查看代码图片

```
var withdraw = function () {
    instance.payMe(function (e, result) {
        if (e != null) {
            if (e.code == '1001') {
                tip.error(lgb.withdraw.info + lgb.cancelled)
            } else {
                tip.error(lgb.withdraw.info + lgb.error)
            }
        } else {
            console.log(result);
            $("#msg").html(lgb.bet.pendingWithdraw);
            $('#msg').css('display', 'block');
            document.getElementById(contentId).style.display = 'none';
            getGameStatus('withdraw');
        }
    });
}
```

这种设计需要用户回到她的投注并支付燃料费以领取她的奖金。另一种选择是自动化合约，使所有者 在`endGame()`时支付燃料费，合约自动分配奖金。

目前 WeBet 的设计中，dapp 用户需要访问她的过去投注。在我们设置中，我们使用存储在本地或可替换服务器上的数据来实现去中心化。这是下一节的主题。

#### Dapp 离线操作

WeBet dapp 展示了如何将非核心应用数据存储在离线服务中。离线数据不是存储在像典型 Web 应用那样的中心服务器上。数据属于每个 WeBet dapp 用户。

##### JavaScript 本地存储

WeBet dapp 使用 JavaScript 的`localStorage` API 来存储与当前用户相关的数据。例如，在`start.js`文件中，我们使用本地存储来保存用户的当前地址和新建的合约地址。它们是下一个页面`join.html`所需的，可以与其他投注参与者共享。

请点击此处查看代码图片

```
var saveLocalStorageBet = function (contractAddress) {
    if (window.localStorage) {
        var storage = window.localStorage;
        var item = {"userAddress": userAddress,
                    "contractAddress": contractAddress};
        storage.setItem("bets", item);
    }
}
```

本地存储可用于存储仅对当前用户私有的数据。它存储在运行钱包的设备上。只有有权访问该设备的人才能获取这些数据。

##### 可替换的第三方服务

`my.html`和`my.js`文件共同工作，展示当前用户参与过的 WeBet 合约列表。以太坊协议没有提供查询区块链节点此类信息的方式。对于 WeBet dapp，我们构建了一个在线服务，从 CyberMiles 节点摄入区块，为区块中的数据（例如，合约、所有者和投注）建立关系数据库，然后提供 API 以查询数据库。

这个数据库是去中心化的，因为任何人都可以使用开源软件部署它。所以，dapp 有众多潜在的数据源选择。没有单一的故障点或控制点。以下是`my.js`中的相关代码：

请点击此处查看代码图片

```
var requestListInfo = function (pageNo) {
    var methodId = 'de2fd8ab,83bd72ba,3cc4c6ce,9c16667c,340190ec';
    var url = 'https://api.cmttracking.io/api/v3/contractsByType?funcIds='
      + methodId + "&limit=" + pageSize + "&page=" + pageNo
    $.ajax({
        url: url,
        dataType: 'json',
        type: 'GET',
        async: true,
        success: function (result) {
            if (result && result.data && result.data.objects) {
                $("#totalCount").val(result.data.meta.total);
                var totalPage = parseInt(
                    result.data.meta.total / pageSize) + 1;
                $("#totalPage").val(totalPage);
                var lastCount = result.data.meta.total % pageSize;
                if (pageNo < totalPage) {
                    lastCount = pageSize;
                }
                var id = "listContent";
                divCount = 0;
                if (result.data.objects.length <= 0) {
                    tip.closeLoad();
                    return;
                }
                console.log(result.data.objects);
                for (var i = 0; i < result.data.objects.length; i++) {
                    var obj = result.data.objects[i];
                    appendChildList(obj.address, id,
                                    lastCount, userAddress);
                }
            }
        },
        error: function (e) {
            console.log("Get user contract address failed" + e)
        }
    });
}
```

在这种情况下，该服务部署在`api.cmttracking.io`，允许通过字节码签名搜索智能合约地址。

### 结论

在本章中，我以 Valentines 和 WeBet 为例，展示了如何在 CyberMiles 公有区块链上创建完整的 dapps。

## 17. 业务规则与合约

区块链虚拟机本质上是一个状态机，它对账户的状态变化（即交易）做出反应。当然，作为反应的一部分，虚拟机也可以引起额外的状态变化。在许多情况下，这种状态变化可以由一套正式规则定义和描述（“如果这个，那么那个”，即 IFTTT）。实际上，在现代计算机系统中，大多数机器间的交互都是由这样的规则定义的。

然而，当我们有多个相互作用的系统时，即使是经验丰富的计算机程序员使用通用编程语言显式编码和执行规则也是不可能的。例如，在典型的航空公司里程计划中，一个人赚取的积分取决于她账户状态、账户历史、购买的机票和乘坐的航班的复杂规则。每个系统都有自己的规则，最终执行结果（这次航班后获得的积分）是所有这些规则的“连接”操作。此外，这些规则不应该由计算机程序员编写或维护，因为它们通常根据业务需求而变化。业务分析师必须能够创建、验证和维护这些规则。这催生了业务规则引擎（BRE）。

典型的 BRE 包括一个专门的计算机编程语言（正式规则语言）、运行时执行规则和可选的视觉工具创建和管理规则。BRE 几乎在每种编程语言中都可以找到，并且广泛由商业和开源提供商提供。知名 BRE 的例子包括 Drools、Jess、Pega、ILOG 和 InRule。Lity 编程语言和虚拟机是基于区块链的第一个 BRE。

支持区块链智能合约中的规则语言和工具可以帮助将大量业务分析师/程序员和他们现有的规则应用带入区块链生态系统。业务规则引擎（BRE）允许人们使用熟悉的工具构建去中心化的金融、电子商务和其他应用。另一方面，区块链提供了一个安全和可验证的平台来执行业务规则，并可能为 BRE 带来一个新的信任层次。

在本章中，我们将探讨 Lity 智能合约语言和 CyberMiles 公共区块链如何支持智能合约中的正式业务规则。

### 示例

Lity 规则定义很简单。总体方法是首先定义规则何时应被触发，然后定义被触发的动作。

让我们来看一个规则，该规则在有可用的预算时给退休者发放养老金。BRE 有一个“工作内存”空间来存储个人简介以及预算。当规则被触发时，Lity 虚拟机中的执行引擎将遍历工作内存中的所有对象，并识别满足`when`子句的组合。它执行`then`子句并更新工作内存中对象的状态。虚拟机对这个规则对工作内存中的所有对象执行，直到`when`子句无法再匹配工作内存中的任何对象。

点击此处查看代码图片

```
rule "payPension" when {
  p: Person(age >= 65, eligible == true);
  b: Budget(amount >= 10);
} then {
  p.addr.transfer(10);
  p.eligible = false;
  b.amount -= 10;
}
```

在前面的代码片段中，Lity 虚拟机匹配一个年龄超过 60 岁且有资格获得补贴的人。然后它检查预算是否仍然可用。如果满足这两个条件，`when`子句找到匹配项，然后触发`then`子句。`then`子句将资金发送给该人并减少预算。`then`动作之一是将该人的`eligible`属性更改为`false`，这样此人将不再被`when`子句匹配，因为如前所述，规则引擎会反复运行规则，直到找不到更多的匹配项。

现在，我们如何将`Person`对象和`Budget`对象放入 Lity 规则引擎的工作内存中呢？这是通过 Lity 中的`factInsert`和`factDelete`声明来完成的。下面的代码清单展示了整个合约。当合约创建时，`Budget`对象被插入到工作内存中。`addPerson()`函数将一个`Person`对象添加到工作内存中。它保留了在`ps`数组中对该人物的引用，这样如果需要的话，以后可以将其从工作内存中移除。`pay()`函数对工作内存中的所有对象触发规则。

点击此处查看代码图片

```
contract AgePension {
    struct Person {
        int age;
        bool eligible;
        address addr;
    }

    struct Budget {
        int amount;
    }

    mapping (address => uint256) addr2idx;
    Person[] ps;
    Budget;

    constructor () public {
        factInsert budget;
        budget.amount = 100;
    }

    function addPerson(int age) public {
        ps.push(Person(age, true, msg.sender));
        addr2idx[msg.sender] = factInsert ps[ps.length-1];
    }

    function deletePerson() public {
        factDelete addr2idx[msg.sender];
    }

    function pay() public {
        fireAllRules;
    }

    function () public payable { }

    rule "payPension" when {
        p: Person(age >= 65, eligible == true);
        b: Budget(amount >= 10);
    } then {
        p.addr.transfer(10);
        p.eligible = false;
        b.amount -= 10;
    }
}
```

您可以将此合约输入到 CyberMiles 的 Europa 在线集成开发环境（IDE）中，并将其部署到 CyberMiles 的公有区块链网络上（图 17.1）。您可以使用 Europa UI 直接与合约方法（如`addPerson()`和`pay()`）交互，以查看规则执行的实际效果。

![image](img/yuan_f17_01.jpg)

**图 17-1** 通过 Europa 在 CyberMiles 公有区块链上部署规则合约

**注意**

**BUIDL IDE**也能编译并部署内嵌规则的 Lity 智能合约。试试看！

现在您已经看到了 Lity 规则智能合约的一个简单示例。在这个例子中，功能可以通过普通的`if-then`语句很容易地实现。在下一节中，让我们深入了解规则语言和更常见的规则用例。

### 规则语言

现代 BREs（包括 Lity）使用 Rete 算法来构建、评估，然后执行一个相互干扰的规则网络。

所有规则都可以序列化为一系列嵌套的`if-then`语句。然而，当规则复杂时，`if-then`结构可能会变得复杂。考虑以下简单的航空公司奖励规则：

+   当奖励里程达到 25,000 英里时，客户获得银卡地位。

+   当奖励里程达到 50,000 英里时，客户获得金卡地位。

+   银卡客户可以从任何航班中获得 10%的奖励里程。

+   金卡客户可以从任何航班中获得 20%的奖励里程。

这个例子只涉及两套简单的推理规则，即客户状态和航班奖励。现在，考虑计算航班上所有客户的奖励规则。一些客户可能在航班上达到银牌或金牌状态。因此，`if-then`序列需要首先计算奖励里程，然后更新状态，然后再次为一些客户重新计算奖励里程。

如果规则更复杂，并且包含几个更多的推理规则集，`if-then`序列可能会复杂得多。每个规则集都需要在其它规则集的每一种组合内部进行评估和执行。深层嵌套的序列无法手工构建，也无法测试和验证。此外，如果根据业务需求更改规则，那么需要重新构建整个评估、重新评估和执行的序列。

#### Rete 算法

Rete 算法由查尔斯·福格博士发明，优雅地解决了这个问题。不详细讨论算法的具体细节，它允许我们将个别规则作为网络中的节点（称为 Rete 网络）并将规则之间的推理关系连接起来。一旦定义了 Rete 网络，该算法自动应用于工作记忆中的对象集合（即航空公司的例子中的客户和航班对象）。Rete 算法通过遍历网络节点高效地评估和重新评估对象，然后执行规则。

对于开发人员和业务分析师，我们可以简单地声明规则并将对象放入工作记忆中。我们不再需要构建高度嵌套的`if-then`序列，并且现在可以依靠计算机在规则和对象上执行 Rete 算法。

Lity 规则引擎实现了 Rete 算法。Lity 规则的总体语法如下：

点击此处查看代码图片

```
contract C {
    rule "ruleName"
    // Rule attributes
    when {
        // Filter Statements
    } then {
        // Action Statements
    }
}
```

接下来，让我们看看规则的结构。

#### 规则属性

规则可以有以下属性。

`salience`属性表示规则的激活优先级。一个合同可以有多个规则，它们按`salience`排序。优先级越高的规则首先进行评估和执行。它默认为整数值 0。在以下示例中，首先评估第二个规则。

点击此处查看代码图片

```
rule "test1" salience 20 when {
  p: Person(val >= 10);
} then {
  p.addr.send(1);
  p.val--;
  update p;
}

rule "test2" salience 30 when {
  p: Person(val >= 20);
} then {
  p.addr.send(2);
  p.val--;
  update p;
}
```

当`no_loop`属性为真时，它禁止使用相同的事实集激活规则。这是为了防止无限循环。它默认为`false`。在以下示例中，对于工作记忆中的每个`Person`，规则只触发一次。

点击此处查看代码图片

```
rule "test" no_loop true when {
  p: Person(age >= 20);
} then {
  p.age++;
  p.addr.send(1);
  update p;
}
```

当`lock_on_active`属性为真时，它禁止使用相同的事实集激活规则多次。这比`no_loop`更强，因为它还可以防止即使是由其他规则的操作引起的规则重新激活。

#### 规则筛选

筛选语句指定了如何将事实（结构和对象）与规则匹配。它是一系列用`AND`连接的语句，意味着它们都必须满足，一组对象才能匹配并筛选。

每个语句指定了一个对象类型及其属性的筛选条件。它从模式绑定开始，指定了在此规则作用域内引用的的事实标识符。绑定后，模式类型指定了事实对象类型。然后，一系列约束描述了这一事实的条件。这些约束必须是`boolean`表达式。

点击此处查看代码图片

```
rule "test" when {
  p: Person(age >= 65, eligible == true);
} then {
  ... ...
}
```

前一个模式描述了一个类型为`Person`的事实`p`；它的约束是`age`必须大于或等于`65`，且`eligible`必须是`true`。

#### 规则动作

动作语句指定了对筛选的事实调用的函数。例如，动作块中的以下代码调用`transfer()`，然后更新人的资格：

点击此处查看代码图片

```
rule "test" when {
  p: Person(age >= 65, eligible == true);
} then {
  p.addr.transfer(10);
  p.eligible = false;
  update p;
}
```

动作块中的`update`关键词是规则语言的一个特殊关键词。更新对象语句通知规则引擎这个对象可能会被修改，规则可能需要重新评估。

#### 规则继承

规则可以被继承。有时一个规则的约束是基于另一个规则的约束。在这种情况下，这个规则可以扩展另一个规则。

例如，一个百货商店想要给年长的顾客提供 10%的折扣和免费停车。折扣规则如下所述：

点击此处查看代码图片

```
rule "test1"
when {
    customer : Customer( age > 60 );
} then {
    customer.discount = 10;
}
```

免费停车规则可以扩展 60 岁以上顾客的约束（年龄大于 60 岁）。然后这个规则可以写成如下：

点击此处查看代码图片

```
rule "test2"
    extends "test1"
when {
    car : Car ( ownerID == customer.id );
} then {
    car.freeParking = true ;
}
```

继承允许开发人员和分析师基于过去的工作构建复杂规则库。

#### 工作内存

正如我们在示例中看到的那样，`factInsert`和`factDelete`语句用于管理工作内存中规则筛选和执行的动作的事实。

`factInsert`操作符接受一个具有存储数据位置的对象，并评估为事实处理，其类型为`uint256`。将存储对象的引用插入工作内存。例如如下：

点击此处查看代码图片

```
contract C {
  struct fact { int x; }
  fact[] facts;
  constructor() public {
    facts.push(fact(0));
    // insert the fact into working memory
    factInsert facts[facts.length-1];
  }
}
```

请注意`factInsert fact(0)`；不能编译。原因是`fact(0)`是一个具有内存数据位置的引用，它不是持久的，因此不能插入工作内存。

`factDelete`操作符接受一个事实处理（一个`uint256`）并评估为`void`。它将事实的引用从工作内存中移除。

最后，`fireAllRules`是一个特殊的声明，它启动了 Lity 规则引擎的执行。

### 更多商业案例

智能合约中有很多应用规则的例子。你已经看到了一个简单的航空公司积分计划的例子。一般来说，公共区块链是这类积分计划的好平台，因为它们在供应、发行和使用这些积分方面提供了透明度，并且可以使来自不同商家的积分得以交换和交易。在本节中，我将通过一些更简单的例子向您介绍一些规则的实际应用用例。

#### 保险理赔

考虑一家提供航班延误索赔的旅行保险公司：

+   如果航班延误超过四小时，每个人都至少获得 100 美元。

+   如果航班延误超过六小时，每个人都可获得最多 300 美元的报销。

第一个规则（四小时或更多）表示如下：

点击此处查看代码图片

```
rule "four hour fix amount" when {
    p: Person()
    f: Flight(delay >= 4, id == p.flightID)
} then {
    p.claimAmount = max(100, p.claimAmount);
}
```

对于第二个规则（六小时或更多），第一个规则中已经暗示了 100 美元的补偿，因此我们在这里只需要考虑有限的费用。

点击此处查看代码图片

```
rule "six hour limited amount" when {
    p: Person()
    f: Flight(delay >= 6, id == p.flightID)
} then {
    p.claimAmount = max(min(p.delayExpense, 300), p.claimAmount);
}
```

规则引擎在评估保险索赔方面可能很有用，因为所有的赔偿金都在保险合同中的规则中。

#### 税收

这个例子说明了如何使用规则引擎计算税费。在大多数国家，税率是分级的。也就是说，一定的收入范围对应着相应的税率。通常，收入越高，税率也越高。例如，在 2018 年的美国联邦税系统中，单身申报者根据他们的收入支付以下税率：

+   *$0 至$9,525*：10%

+   *$9,526 至$38,700*：12%

+   *$38,701 至$82,500*：22%

+   *$82,501 至$157,500*：24%

+   *$157,501 至$200,000*：32%

+   *$200,001 至$500,000*：35%

+   *$500,001 或更高*：37%

这些税率是边际税率，意味着纳税人仅在她收入落入指定范围的金额上支付该税率。例如，如果您有 10,000 美元的应税收入，前 9,525 美元适用 10%的税率，剩下的 475 美元适用下一个税级的税率，即 12%。现在，让我们来看看规则。对于第一个税级，从 0 美元至 9,525 美元的净收入按 10%征税。

点击此处查看代码图片

```
rule "first bracket" when{
    p: Person(income > 0)
} then {
    p.tax += min(9525, p.income) * 10 / 100;
}
```

同样，第二个税级的$9,526 至$38,700 的净收入按 12%征税。请注意，$9,525 的收入已经在第一个税级中征过税了，所以在这里应该从应税金额中减去$9,525。

点击此处查看代码图片

```
rule "second bracket" when{
    p: Person(income > 9525)
} then {
    p.tax += (min(38700, p.income) - 9525) * 12 / 100;
}
```

同样地，其他税级如下表示：

点击此处查看代码图片

```
rule "third bracket" when{
    p: Person(income > 38700)
} then {
    p.tax += (min(82500, p.income) - 38700) * 22 / 100;
}

rule "fourth bracket" when{
    p: Person(income > 82500)
} then {
    p.tax += (min(157500, p.income) - 82500) * 24 / 100;
}

rule "fifth bracket" when{
    p: Person(income > 157500)
} then {
    p.tax += (min(200000, p.income) - 157500) * 32 / 100;
}

rule "sixth bracket" when{
    p: Person(income > 200000)
} then {
    p.tax += (min(500000, p.income) - 200000) * 35 / 100;
}

rule "seventh bracket" when{
    p: Person(income > 500000)
} then {
    p.tax += (p.income - 500000) * 37 / 100;
}
```

当然，税法有许多其他规则来调整个人的应税收入，将收入分类到额外税率区间（例如，所有资本收益都按 10%征税），并在满足某些规则时退还部分税款。税法是规则引擎的一个很有说服力的用例！

#### 产品组合

最后，让我们看看一个商业应用的例子。网上和线下商店提供顾客同时订购多个产品的折扣是常见的做法。考虑餐馆为例；汉堡的价格为 $11，饮料的价格为 $3，这些加起来 $14。这个求和规则可以简单地表示如下：

点击此处查看代码图片

```
rule "Burger"
  salience 10
  lock_on_active
when{
    b: Burger();
    bl: Bill();
} then {
    bl.amount += 11;
}

rule "Drink"
  salience 10
  lock_on_active
when{
    d: Drink();
    bl: Bill();
} then {
    bl.amount += 3;
}
```

然而，许多餐馆提供套餐折扣。例如，汉堡和饮料的组合折扣为 $2。借助规则引擎，此折扣规则可以如下自动应用：

点击此处查看代码图片

```
rule "Combo" when{
    b: Burger(combo==-1);
    d: Drink(combo==-1);
    bl: Bill();
} then {
    b.combo = bl.nCombo;
    d.combo = bl.nCombo;
    bl.nCombo++;
    bl.amount -= 2;
    update b;
    update d;
}
```

`nCombo` 是账单中的组合数，汉堡/饮料的 `combo` 值表示组合编号（`-1` 表示没有组合） that the 汉堡/饮料属于。每个汉堡或饮料至多属于一个组合，以防止重复折扣。

### 结论

区块链智能合约非常适合正式规则。智能合约是在满足某些条件时由计算机自动执行的一组规则。反过来，区块链保证了规则的正确执行。

在本章中，我讨论了 Lity 规则语言和引擎。它使正式的业务规则可以在区块链智能合约中构建和执行。请注意，本章中出现的许多示例最初出现在 Lity 文档中。

## 18. 构建应用特定的 EVM

**Lity** 的一个关键特性是 **libENI** 设施。它允许开发者向 Lity 虚拟机添加本地的 C/C++ 函数。虽然 Solidity 和 Lity 都是图灵完备的语言，但它们效率不高。这转化为在区块链上进行许多常见计算机操作（如字符串操作和加密/解密）时的低性能和高燃料成本。**libENI** 本机函数允许开发者以一种高度有效的方式在区块链智能合约中支持这些操作。**libENI** 的重要性有两点。

+   如果你正在建立自己的区块链，你可以通过捆绑选定的 **libENI** 函数库来为特定的应用用例进行定制。例如，如果你正在建立一个专门用于交换隐私数据的区块链，你可以捆绑常用于数据加密的 **libENI** 函数。商业提供商，如 Second State，为您提供创建自定义 **libENI** 捆绑包的工具。

+   如果你正在一个支持 Lity 的公共区块链上开发智能合约，比如 CyberMiles 公共区块链，你可以通过 libENI 添加新的系统级函数。在 CyberMiles 区块链上，libENI 模块和函数可以由任何人开发，并通过验证者的共识添加到区块链虚拟机中。这是扩展区块链虚拟机最民主的方式。

**注意**

以太坊路线图还呼吁实现本机和预编译合约。这些合约由以太坊核心开发者开发，并通过以太坊软件更新部署。另一方面，面向公共区块链的 libENI 扩展可以由任何人开发，只需得到底层区块链共识的批准。

例如，在 CyberMiles 区块链上，任何人都可以通过治理交易提出向区块链添加 libENI 函数的提案。CyberMiles 的验证者或超级节点会对治理交易进行投票，以批准或拒绝它。这使得虚拟机可以在软件开发生命周期之外，在“核心”开发者社区之外实现动态和民主的扩展。由社区开发的 libENI 函数可以在不停止、分叉或重新启动区块链的情况下添加到虚拟机中。

在本章中，我将解释如何使用、开发和部署 libENI 函数。我们将使用 CyberMiles 作为例子，展示 libENI 链上治理是如何工作的。Lity 团队正在定期增加对 libENI 实现的补充。它正在为 Lity 虚拟机开发完整套的字符串库、加密库、JSON 库等常用工具，作为高效且可选的 libENI 函数。

### 使用 libENI 函数

CyberMiles 区块链软件已经预装了几个简单的 libENI 函数。它们允许我们立即在智能合约中实验 libENI 函数。但首先，你需要安装`lityc`编译器以构建用 Lity 编程语言编写的智能合约。

你可以选择从源代码构建`lityc`编译器，或者直接下载其支持的一个操作系统平台的可执行文件。可执行文件的发布页面在 GitHub 上，链接为[`github.com/CyberMiles/lity/releases`](https://github.com/CyberMiles/lity/releases)。但如果你倾向于自己构建，请使用以下内容：

点击此处查看代码图片

```
$ git clone https://github.com/second-state/lity.git
$ cd lity
$ mkdir build
$ cd build
$ sudo apt-get install cmake libblkid-dev e2fslibs-dev
    libboost-all-dev libaudit-dev
$ cmake ..
$ make
... ...
$ ./lityc/lityc --help
```

现在你已经安装了`lityc`，我们将通过几个示例来了解如何在智能合约中使用 libENI 函数。

#### 字符串反转示例

这个示例展示了一个相当简单的 libENI 函数，它可以反转任何接收到的字符串。以下是一个示例合约。正如你所见，它与普通的 Solidity 合约类似。然而，在 Solidity 中并不存在`eni`这个关键字，因此它不能使用普通的 Solidity 编译器编译。

点击此处查看代码图片

```
pragma solidity ⁰.4.23;

contract ReverseContract {
  function reverse(string input) public returns(string) {
    string memory output = eni("reverse", input);
    return output;
  }
}
```

关键字`eni`后面跟着两个参数。`reverse`是 libENI 函数的名称。添加到虚拟机的每个 libENI 函数都必须有一个独特的名称。字符串参数`input`是传递给`reverse`libENI 函数的参数。您可以向您的 libENI 函数传递任意数量的参数。

让我们将代码保存到一个名为`Reverse.lity`的文件中。您必须使用`lityc`编译器编译源代码以生成字节码和应用程序二进制接口（ABI）定义。

点击此处查看代码图片

```
$ ./lityc/lityc --bin Reverse.lity
======= ./Reverse.lity:ReverseContract =======
Binary:
608060405234...

$ ./lityc/lityc --abi Reverse.lity
======= ./Reverse.lity:ReverseContract =======
Contract JSON ABI
[{"constant":false,"inputs":[{"name":"input","type":"string"}],
"name":"reverse","outputs":[{"name":"","type":"string"}],
"payable":false,"stateMutability":"nonpayable","type":"function"}]
```

在 travis 客户端的 web3-cmt 控制台（类似于以太坊上的 GETH 控制台）上，您可以现在将合约字节码和 ABI 部署到您运行的 CyberMiles 节点。

点击此处查看代码图片

```
> personal.unlockAccount(cmt.accounts[0],'1234');
> bytecode="0x608060..."
> abi = [{"constant":false,"inputs":[{"name":"input",
"type":"string"}],"name":"reverse","outputs":[{"name":"","type":"string"}],
"payable":false,"stateMutability":"nonpayable","type":"function"}]
> contract = web3.cmt.contract(abi);
> contractInstance = contract.new(
  {
    from: web3.cmt.accounts[0],
    data: bytecode,
    gas: "4700000"
  },
  function(e, contract) {
    console.log("contract address: " + contract.address);
    console.log("transactionHash: " + contract.transactionHash);
  }
 );
```

一旦合约在区块链上部署并获得确认，您将在控制台上看到其合约地址。您可以调用其`reverse`方法。

点击此处查看代码图片

```
> contractInstance.reverse.call("hello", {from: cmt.accounts[0]})
olleh
```

由于大多数 libENI 函数需要区块链节点执行工作，它们通常需要燃料费。这就是为什么我们有`from`账户来支付此 libENI 函数调用的燃料费。

#### RSA 示例

RSA 示例展示了如何在智能合约内使用一对 RSA 公钥和私钥来加密和解密数据。此类功能使区块链账户能够通过智能合约交换私人信息。它们是包括数据市场和内容分发在内的广泛应用的关键构建块。

**注意**

一个有趣的 RSA 应用是一个数据市场。让我们用一个医疗记录市场来说明在这个背景下 RSA 重新加密方案是如何工作的。患者拥有自己的医疗记录，并授权鲍勃（数据经纪人或医院）代表他们聚合和出售医疗记录。爱丽丝（数据用户或研究人员）从鲍勃那里购买患者的数据。然后鲍勃将利润分发给患者。我们如何能在链上自动化并记录整个过程？

鲍勃设置三个 RSA 密钥（一个公钥 1 加密，一个公钥 2 重新加密，一个私钥 3 解密）并设置一个智能合约进行交易。智能合约包含公钥 1 和 2。

患者通过使用密钥 1 加密记录并将其上传到合约，授权鲍勃出售她的记录。爱丽丝同意从鲍勃那里购买数据并向智能合约付款。智能合约使用密钥 2 重新加密所有记录并使其公开可用。鲍勃然后将私钥 3 直接离线发送给爱丽丝，这使得爱丽丝能够解密合约中持有的所有记录。爱丽丝确认收到私钥 3，合约自动将付款分发给患者和鲍勃。

在这个过程中，Alice 和 Bob 是唯一可以解密整个数据集的人。所有患者都知道自己的数据。公众可以验证交易，包括所有的货币支付，但无法看到任何数据。

以下代码展示了一个简单的合约，它使用 RSA 公钥加密一个明文字符串，然后使用 RSA 私钥进行解密：

点击此处查看代码图片

```
pragma solidity ⁰.4.0;

contract RSACrypto {
    function encrypt(string pubkey, string plaintext)
                        public pure returns (string) {
        string memory ret;
        ret = eni("rsa_encrypt", pubkey, plaintext);
        return ret;
    }

    function decrypt(string prikey, string ciphertext)
                        public pure returns (string) {
        string memory ret;
        ret = eni("rsa_decrypt", prikey, ciphertext);
        return ret;
    }
}
```

在这个例子中，你可以看到 libENI 函数`rsa_encrypt`和`rsa_decrypt`采取了多个输入参数。在本节中，我将向您展示如何使用`lityc`一次性生成字节码和 ABI 接口。

点击此处查看代码图片

```
$ ./lityc/lityc --abi --bin -o output RSACrypto.lity
$ cat output/RSACrypto.abi
[{"constant":true,"inputs":...}]
$ cat output/RSACrypto.bin
608060405234801...
```

接下来，将字节码和 ABI 部署到本地或测试网 CyberMiles 区块链，并在部署成功后收到合约地址。

点击此处查看代码图片

```
> personal.unlockAccount(cmt.accounts[0],'1234');
> bytecode="0x608060..."
> abi = [{"constant":false,"inputs":...}]
> contract = web3.cmt.contract(abi);
> c = contract.new(
  {
    from: web3.cmt.accounts[0],
    data: bytecode,
    gas: "4700000"
  },
  function(e, contract) {
    console.log("contract address: " + contract.address);
    console.log("transactionHash: " + contract.transactionHash);
  }
 );
```

要使用 RSA 函数，你需要调用智能合约方法，并传入密钥和数据。

点击此处查看代码图片

```
prikey = "-----BEGIN RSA PRIVATE KEY-----\nMIIEowIBAA...";
pubkey = "-----BEGIN PUBLIC KEY-----\ +X\nlNlozUy...";

# Encrypt
> ciphertext = c.encrypt.call(pubkey, 'Hello World!',
                                {from: cmt.accounts[0]})
"49d511a44a3d2a24...b258e70282a"

# Decrypt
> c.decrypt.call(prikey, ciphertext, {from: cmt.accounts[0]})
"Hello World!"
```

当然，在现实世界中，我们无法使用私钥调用智能合约方法，因为所有这些交易都是公共记录。这个例子只是为了说明。

#### Scrypt 示例

这个 scrypt 示例是为了在 Lity 智能合约中验证 Dogecoin 区块链头部。为什么有人会这样做呢？原因是 Dogecoin 是比特币区块链的一个克隆。验证 Dogecoin 区块头部使智能合约能够进一步验证该区块内的交易。通过将此计算扩展到比特币，我们可以开发能够在跨链资产交换中自动验证和响应比特币交易的以太坊智能合约。

然而，验证 Dogecoin 头部需要智能合约执行 scrypt 操作，这对于 Solidity 和 EVM 来说计算成本很高。Vitalik Buterin 估计，执行此操作需要 3.9 亿以太坊单位气体，远远超过以太坊的区块气体限制。为了解决这个问题，以太坊和 Dogecoin 社区设立了一个 25 万美元的赏金，以奖励第一个提出在以太坊上执行 scrypt 操作验证 Dogecoin 区块的有效解决方案的人。在本节中，我们将展示 libENI 在一个完全兼容以太坊的区块链虚拟机上以低成本提供此类解决方案。

**注意**

BTCRely 是一个社区服务，用于在以太坊上验证比特币交易。它被设置为以太坊智能合约，允许其他合约请求验证并支付费用。这笔费用用于激励一群离线工作者在自己的电脑上进行验证，并提交结果。Truebit 项目对于离线验证也有类似的方法。然而，最终，这些离线方案都是依赖“良好行为”激励的加密经济游戏。它们既昂贵、又慢、又繁琐，并且不可靠。

`scrypt`示例的完整源代码可在 Lity 文档网站上找到，网址为[`lity.readthedocs.io/en/latest/verify-dogecoin-block-on-travis.html`](http://lity.readthedocs.io/en/latest/verify-dogecoin-block-on-travis.html)。在这里，你可以看到智能合约调用`libENI`函数`scrypt`执行工作的关键部分：

点击此处查看代码图片链接

```
pragma solidity ⁰.4.23;

contract DogecoinVerifier {

  ...

  function verifyBlock(uint version, string prev_block,
        string merkle_root, uint timestamp, string bits, uint nonce)
        pure public returns (bool) {
    DogecoinBlockHeader memory block_header =
        DogecoinBlockHeader(version, prev_block, merkle_root,
                            timestamp, bits, nonce);
    string memory block_header_hex = generateBlockHeader(block_header);
    string memory pow_hash = reverseHex(eni("scrypt", block_header_hex));
    uint256 target = bitsToTarget(bits);
    if (hexToUint(pow_hash) > target) {
      return false;
    }
    return true;
  }

  ...
}
```

再次，我们使用`lityc`一次性生成字节码和 ABI 接口。

点击此处查看代码图片链接

```
$ ./lityc/lityc --abi --bin -o output DogecoinVerifier.lity
$ cat output/DogecoinVerifier.abi
[{"constant":true,"inputs":...}]
$ cat output/DogecoinVerifier.bin
608060405234801561001057600080fd5b506111d5...
```

现在，我们可以将字节码和 ABI 部署到区块链上，成功部署后获得合约地址。

点击此处查看代码图片链接

```
> personal.unlockAccount(cmt.accounts[0],'1234');
> bytecode="0x608060..."
> abi = [{"constant":false,"inputs":...}]
> contract = web3.cmt.contract(abi);
> contractInstance = contract.new(
  {
    from: web3.cmt.accounts[0],
    data: bytecode,
    gas: "4700000"
  },
  function(e, contract) {
    console.log("contract address: " + contract.address);
    console.log("transactionHash: " + contract.transactionHash);
  }
 );
```

要调用合约并验证 Dogecoin 区块头，我们需要以下信息。它们通过算法链接在一起，形成一个有效的区块链头。所有这些信息都可以从 Dogecoin 区块链浏览器中轻松获取。在以下示例中，我们使用 Dogecoin 区块链中的区块 2。

+   版本：`1`

+   前一个区块哈希：`82bc68038f6034c0596b6e313729793a887fded6e92a31fbdf70863f89d9bea2`

+   交易 Merkle 根哈希：`3b14b76d22a3f2859d73316002bc1b9bfc7f37e2c3393be9b722b62bbd786983`

+   时间戳：`1386474933`（从`2013-12-07 19:55:33 -0800`转换而来）

+   难度(位)：`1e0ffff0`

+   非 ce：`3404207872`

现在，我们可以使用之前的数据在合约上调用`verifyBlock`方法。

点击此处查看代码图片链接

```
# Block #2 of dogecoin
> c.verifyBlock.call(1, "82...", "3b...", 1386474933, "1e0ffff0",
                              3404207872, {from: cmt.accounts[0]})
true

# 1-bit of nonce changed
> c.verifyBlock.call(1, "82...", "3b...", 1386474933, "1e0ffff0",
                                3404207871, {from: cmt.accounts[0]})
false
```

虽然超出了本书的范围，但原生的`scrypt`函数为基于比特币区块链的去中心化跨链操作奠定了基础。

### 编写`libENI`函数

现在我们已经了解了如何使用`libENI`函数。在本节中，我将讨论如何编写自己的`libENI`函数，该函数可以动态部署到 CyberMiles 区块链作为虚拟机扩展。让我们以简单的`reverse` `libENI`函数为例。整个示例可在 CyberMiles 的`libENI`公共 GitHub 仓库中找到。

`libENI`函数是用 C++编写的，作为操作系统本地库函数。你需要使用`#include <eni.h>`，创建`eni::EniBase`的子类，并实现以下函数：

+   一个接受字符串作为参数的构造函数。请记得将字符串传递给超类`eni::EniBase`的构造函数，它将原始字符串转换为包含您 ENI 操作参数的`json::Array`。

+   一个析构函数。

+   用于解析参数的`parse`虚拟函数。

+   用于从参数计算燃料消耗的`gas`虚拟函数。

+   用于执行您的 ENI 操作的`run`虚拟函数和参数。

`reverse`函数的骨架代码如下：

点击此处查看代码图片

```
#include <eni.h>
class Reverse : public eni::EniBase {
public:
  Reverse(const std::string& pArgStr)
    : eni::EniBase(pArgStr) { ... }
  ~Reverse() { ... }

private:
  bool parse(const json::Array& pArgs) override { ... }
  eni::Gas gas() const override { ... }

  bool run(json::Array& pRetVal) override { ... }
};
```

接下来，让我们来看看这三个虚拟函数的实现。

#### 解析参数

`parse`函数接受一个包含给您的 libENI 操作的参数的`json::Array`。为了确保其他两个函数`gas`和`run`以相同的方式处理参数，请在`parse`函数中验证、预处理并将参数存储到成员变量中。

`parse`函数在所有参数都正确时应返回`true`，否则返回`false`（例如，缺少参数或类型错误）。

在这个示例中，由`eni::EniBase`构造的`json::Array`只包含用于 libENI 操作`reverse`的参数字符串。以下是`parse`的实现：

点击此处查看代码图片

```
class Reverse : public eni::EniBase {

  ...
private:
  bool parse(const json::Array& pArgs) override {
    m_Str = pArgs[0].toString();
    return true;
  }

  std::string m_Str;
};
```

#### 预估燃料

在您的 libENI 函数运行之前，您需要预估它将消耗多少燃料。重写虚拟函数`gas`并返回您预估的燃料成本。在这个示例中，我们用字符串长度作为其燃料消耗。

点击此处查看代码图片

```
class Reverse : public eni::EniBase {

  ...
private:
  eni::Gas gas() const override {
    return m_Str.length();
  }
};
```

您可以为燃料计算错误返回`0`。如果`gas`返回`0`，虚拟机将不会执行 libENI 函数。

#### 执行函数

重写`run`虚拟函数，并将您的 libENI 函数的结果推回到`json::Array`作为返回值。

点击此处查看代码图片

```
class Reverse : public eni::EniBase {
  ...
private:
  bool run(json::Array& pRetVal) override {
    std::string ret(m_Str.rbegin(), m_Str.rend());
    pRetVal.emplace_back(ret);
    return true;
  }
};
```

#### 映射到 libENI 函数名称

最后，我们需要将反向 C++类映射到反向 libENI 函数名称。为此，我们使用`ENI_C_INTERFACE(OP, CLASS)`导出 C 接口，其中`OP`是您的 libENI 函数名称（即，在这个示例中的`reverse`），`CLASS`是实现类的名称（即，在这个示例中的`Reverse`）。

```
ENI_C_INTERFACE(reverse, Reverse)
```

就这样。您已经为 libENI 函数编写了一个 C++程序。在下一节中，我们将回顾如何将该函数构建成共享库文件，并将该文件部署到运行中的区块链上。

### 部署 libENI 函数

我们使用 GCC 将 libENI 类构建成二进制库文件。您可以查看 libENI 公共 GitHub 仓库中`examples/eni/reverse`目录下的`Makefile`。以下是关键编译器设置：

点击此处查看代码图片

```
CPPFLAGS=-I${LIBENI_PATH}/include
CXXFLAGS=-std=c++11 -fPIC
LDFLAGS=-L${LIBENI_PATH}/lib
LDADD=-leni

all:
  g++ ${CPPFLAGS} ${CXXFLAGS} ${LDFLAGS} -shared -oeni_reverse.so
    eni_reverse.cpp ${LDADD}
```

`${LIBENI_PATH}`是在您的开发机器上定位 libENI 支持库的路径。具体细节请查阅 GitHub 文档。一旦您运行`make all`，应为您的操作系统生成`reverse.so`库文件。

#### CyberMiles 治理

要向正在运行的 CyberMiles 区块链部署`reverse` libENI 函数，我们将使用 CyberMiles 治理交易。首先，您需要设置一个 CyberMiles 区块链节点，然后使用 travis 客户端连接到它（具体操作请参阅附录 A）。

从 travis 客户端控制台，您可以访问 web3-cmt JavaScript 模块。现在，您可以创建一个新的交易来提出一个新的 libENI 函数。该交易包括对库函数的简短描述以及下载库二进制文件的位置，供人们尝试。它还包括这些文件的 MD5 散列值。以下是一个示例：

点击此处查看代码图片

```
> personal.unlockAccount(cmt.accounts[0],'1234');
> var payload = {
  from: cmt.accounts[0],
  name: "reverse",
  version: "v1.0.0",
  fileUrl:
    '{"ubuntu":"http://host/eni_reverse_ubuntu16.04.so",
      "centos":"http://host/eni_reverse_centos7.so"}',
  md5:
    '{"ubuntu":"b44...906d", "centos":"04a...851"}'
}
> web3.cmt.governance.proposeDeployLibEni(payload, (err, res) => {
  if (!err) {
    console.log(res)
  } else {
    console.log(err)
  }
})
```

一旦处理了`proposeDeployLibEni`交易，CyberMiles 区块链上的所有节点都将下载并缓存库文件，并开始七天的投票期。投票期可以通过`proposeDeployLibEni`交易中的`expireBlockHeight`或`expireTimestamp`参数进行自定义。在投票期间，所有验证节点都可以对提案进行投票。`proposalId`是`proposeDeployLibEni`交易的结果值。

点击此处查看代码图片

```
> personal.unlockAccount(cmt.accounts[0],'1234');
> var payload = {
  from: "0x7eff122b94897ea5b0e2a9abf47b86337fafebdc",
  proposalId: "JTUx+ODH0/OSdgfC0Sn66qjn2tX8LfvbiwnArzNpIus=",
  answer: "Y"
}
> web3.cmt.governance.vote(payload, (err, res) => {
  if (!err) {
    console.log(res)
  } else {
    console.log(err)
  }
})
```

如果至少有三分之二投票权的人对`proposalId`投了赞成票，所有节点都将部署新的 libENI 函数，并在七天后或指定的`expireBlockHeight`或`expireTimestamp`时使其可用。

### 结论

在本章中，我们讨论了如何创建并部署新的 libENI 函数以扩展以太坊虚拟机（EVM）。这使得开发者甚至公链社区能够在不停止或分叉区块链的情况下，动态地扩展虚拟机的新功能。
