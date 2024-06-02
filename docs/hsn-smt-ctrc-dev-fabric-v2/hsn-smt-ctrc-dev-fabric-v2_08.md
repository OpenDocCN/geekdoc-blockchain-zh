# 第五章 智能合约调用

本章将为您提供调用智能合约所需的知识。我们将使用在第四章安装的先决条件。然后，使用脚本，我们将启动和停止本地 Fabric 测试网络并部署 Fabcar 智能合约。

由于我们正在利用 Fabcar 和 Fabric 测试网络，我们从回顾*fabric-samples*、Fabcar 智能合约和 Fabric 测试网络开始。然后，我们将启动我们的测试网络并部署 Fabcar 智能合约。接下来，我们将详细介绍脚本执行的步骤。一旦我们的测试网络运行起来并部署了 Fabcar 智能合约，我们将调用 Fabcar 智能合约功能。我们将使用`peer invoke`命令以及命令行 Node.js 应用程序来执行 Fabcar 智能合约功能。Node.js 应用程序将使用 Fabric 客户端 SDK for Node.js。

本章将帮助您实现以下实际目标：

+   通过命令行界面调用智能合约

+   评估查询的事务函数

+   提交交易和查询交易历史

+   创建和发行应用合约

# fabric-samples、Fabcar 和测试网络概述

在本节中，您将学习如何在 Hyperledger Fabric 测试网络上启动、部署和调用智能合约。我们首先看一下*fabric-samples*的结构和组件。然后，我们将详细介绍部署我们的示例智能合约 Fabcar 的基本步骤。一旦 Fabric 设置并运行，我们将通过`peer`命令和 Node.js 方法开始调用 Fabric 智能合约。Fabric 测试网络是一个进行实验和在将您的 Fabric 应用程序移至生产之前运行智能合约的重要操作的好地方。

## fabric-samples

在第四章安装先决条件时，包括了*fabric-samples*，这是超级账本 Fabric 项目，旨在帮助开发者学习 Fabric 智能合约开发。它包含许多智能合约示例和用于快速开发 Fabric 智能合约的工具。其中包括一个完整的开发 Fabric 网络，包括两个组织。每个组织都有一个对等方和 CA。网络使用 Docker 容器化，这使得启动和管理变得简单快捷。

如果您按照第四章中的说明安装了先决条件，您应该有*fabric-samples*目录。我们将在本章和第六章中使用*bin*、*test-network*、*chaincode*和*fabcar*子目录。

超级账本 Fabric 坚定支持*fabric-samples*。Fabric 继续引入新功能，改进现有代码，并推进一起使*fabric-samples*成为超级账本 Fabric 智能合约开发者的主要项目的工具。

*bin*子目录包含`peer`可执行文件，我们将使用它作为调用 Fabcar 智能合约的第一种方法。*chaincode*子目录包含 Fabcar 智能合约，而*fabcar*目录包含 Fabcar 智能合约的命令行客户端。我们将使用*test-network*部署*fabcar*智能合约。合约一旦部署完毕，我们就可以调用它。

在本章中，我们将使用*fabcar*脚本的帮助启动 Fabcar 的测试网络。每个 Fabric 智能合约都需要一个 Fabric 网络。您可以通过利用测试网络来提高自己的技能，并将本章学到的应用到*fabric-samples*中的其他智能合约上。

## Fabcar

Fabric 智能合约 Fabcar 是 *fabric-samples* 中最早和最简单的样本智能合约之一。它非常适合学习 Fabric 智能合约操作和开发的基础知识。通过 Fabcar，我们可以轻松快速地实践 Fabric 智能合约开发，因为它在设计上成熟、稳定且简单，但功能齐全。它实现了我们需要理解和开发 Fabric 智能合约的核心功能。

Fabcar 有两个部分。第一部分是 Fabcar 智能合约，我们在第四章中对其进行了研究。另一部分是 Fabcar 客户端。客户端调用智能合约。

### Fabcar 客户端

正如您在图 5-1 中所见，Fabcar 客户端有多种实现。我们对 JavaScript 实现感兴趣。

![Fabcar 客户端实现](img/HLF_0501.png)

###### 图 5-1\. Fabcar 客户端实现

提供了两个 shell 脚本，*startFabric.sh* 和 *networkDown.sh*，用于启动和停止我们的 Fabcar 测试网络。*startFabric.sh* 脚本准备并运行一个新环境；然后部署和初始化我们的 Fabcar 智能合约。*networkDown.sh* 脚本关闭所有 Docker 容器，删除它们，并清理环境。

###### 警告

当 Fabric 网络重新启动时，通常会清除所有数据。如果您需要保留 Fabcar 测试网络中的任何容器中的工作，则需要在启动或停止测试网络之前持久化数据。通常，您需要为排序器和对等体 Docker 容器中的目录 */var/hyperledger/production* 挂载卷。

Fabcar 客户端实现为四个 Node.js 命令行应用程序，在 图 5-2 中有重点标出。其中两个应用程序，*enrollAdmin.js* 和 *registerUser.js*，处理管理员注册和应用程序用户注册。另外两个 Node.js 应用程序，*invoke.js* 和 *query.js*，分别处理调用交易和查询评估。

![Fabcar Node.js 应用程序](img/HLF_0502.png)

###### 图 5-2\. Fabcar Node.js 应用程序

这些都是我们将要检查并执行以调用 **Fabcar** 智能合约的四个 Node.js 应用程序。在第六章中，我们将重构并将它们整合到一个我们开发的新的 Node.js Express web 应用程序中，称为 Fabcar UI。

使用特定语言版本的 Fabric 客户端 SDK 的 Fabric 智能合约客户端。用 JavaScript 开发的客户端可以使用 [Fabric 客户端 SDK for Node.js](https://github.com/hyperledger/fabric-sdk-node) 来整合 Fabric 智能合约功能，进行身份验证、提交交易和评估查询。由于这些 Node.js 包依赖关系来自 *package.json* 文件，npm 安装了 图 5-3 中突出显示的四个 Node.js 模块：

```
"dependencies": {
    "fabric-ca-client": "².1.0",
    "fabric-network": "².1.0"
},
```

![Fabcar 客户端 Fabric SDK for Node.js 模块](img/HLF_0503.png)

###### 图 5-3. Fabcar 客户端 Fabric SDK for Node.js 模块

我们将直接使用的两个包是 *fabric-ca-client*，它处理与权威机构进行注册、注册和管理身份的交互；以及 *fabric-network*，它提供了 `gateway`、`network`（通道）和 `contract` 对象来与 Fabric 智能合约交互。

### **Fabcar** 智能合约

**fabcar.js** 是一个 Fabcar 智能合约，和客户端一样，它也实现了多种语言；我们在第四章讨论了它的实现。应选择带有 *lib* 子目录的 *chaincode/fabcar/javascript* 子目录。本章我们将部署和调用的 Fabcar 智能合约位于 *lib* 子目录中。

Node.js 智能合约有依赖关系：

```
"dependencies": {
    "fabric-contract-api": "².0.0",
    "fabric-shim": "².0.0"
},
```

这两个依赖项，**fabric-contract-api** 和 **fabric-shim**，导致了 Node.js 包被导入到项目中。对于 Fabric 智能合约，只需要一个导入，即 *fabcar.js*：

```
const { Contract } = require('fabric-contract-api');
```

**fabric-shim** 包是一个提供给链码的低级接口，而**fabric-shim-api** 则被**fabric-shim** 和 **fabric-contract-api** 共同使用，用于提供类型定义。

## Fabric 测试网络

Fabric 测试网络将启动一个可用的 Fabric 网络，用于智能合约的部署。当我们使用 Fabcar 脚本 *startFabric.sh* 启动和 *networkDown.sh* 停止测试网络时，间接使用 *network.sh* 脚本。这个脚本是模块化的，可以重构为一系列细粒度的工具，适合你的工作流程和风格。它也可以作为一个很好的例子，学习如何开发脚本来启动和管理你自己的自定义 Fabric 网络。对于我们开发来说，这是一个快速启动，减轻了设计、配置和管理实现功能性 Fabric 网络所需的所有资源的痛苦。

一旦您开发了一个可以投入生产的智能合约，您可以将其打包并推广到生产环境中。部署的过程取决于要部署到的网络。每个生产网络都将不同，但您的智能合约的功能在每个网络上都是一致的。在 第九章 中，我们讨论了 Hyperledger Fabric v2 的测试网络。随着应用程序复杂性的增加，您将需要设计新的自定义网络来满足您的特定需求。Fabric 测试网络是一个最小化的网络，但是功能齐全。它设计有两个组织，每个都运行一个对等体。每个组织都有一个 CA 来向组织成员发放 X.509 证书。

### Docker 容器和 CouchDB 数据库

Docker Dashboard 中 Fabcar 的测试网络配置在 Docker 容器中运行以下服务器：

*ca_org2*

组织 2 的凭证机构

*ca_orderer*

网络排序器的凭证机构

*ca_org1*

组织 1 的凭证机构

*couchdb1*

组织 2 的世界状态数据库

*orderer.example.com*

创建区块并将其发送以提交的网络排序器

*couchdb0*

组织 1 的世界状态数据库

*peer0.org2.example.com*

组织 2 的对等体

*peer0.org1.example.com*

组织 1 的对等体

两个顶级容器分别是每个组织对等体的智能合约运行时容器。

我们测试网络中组织的世界状态数据库是 CouchDB。我们可以通过浏览器使用 CouchDB 的 Fauxton web 应用程序访问 CouchDB。打开您的浏览器并转到以下 CouchDB URL：[*http://127.0.0.1:5984/_utils/*](http://127.0.0.1:5984/_utils/)。

您将收到一个登录 CouchDB 的页面。您可以输入`**admin**`作为用户名，输入`**adminpw**`作为密码，这是默认设置。这些在生产环境中会被更改和限制访问以确保安全，但是在开发过程中，这很有效。此外，用户名和密码将成为网络配置的一部分，并且将在您的 *.yaml* 文件中可用。

登录后，您将收到显示组织 1 的 *couchdb0* 数据库的页面。第九行显示 *mychannel_fabcar*。这是我们的 Fabcar 世界状态数据库。*mychannel* 是 Fabcar Fabric 通道的名称，*fabcar* 是我们链代码的名称。

我们测试网络中的每个 CouchDB 实例都可以通过更改 URL 中的端口号来访问。Docker 仪表板中 Fabric 容器列表显示端口 5984 是 *couchdb0*，端口 7984 是 *couchdb1*。因此，在 CouchDB URL 中将端口更改为`**7984**`，我们可以访问 *couchdb1*，这是组织 2 的世界状态数据库。请注意，它们是相同的，正如它们应该是的那样，因为它们代表了 Fabcar 的世界状态。

以下是要点摘要：

+   Fabric 网络中的每个组织都可以拥有一个或多个通道。

+   每个通道将有一个世界状态（类似数据库）对应于智能合约。

+   对于每个通道，世界状态数据库（及其内容）都将不同。

+   每个智能合约的实例将同时在 Fabric 网络中的所有通道上运行。

现在您已经了解了 *fabric-samples*、*fabcar* 和 *test-network* 的基础知识，我们准备启动一个 Fabcar 测试网络并部署 Fabcar 智能合约。

# 部署智能合约

我们需要一个 Fabric 网络来部署我们的 Fabcar 智能合约。对于开发来说，使用 *fabric-samples* 中的 *test-network* 部分非常方便。虽然您可以执行 *test-network* 的 *network.sh* 来启动一个默认网络，但我们使用 *startFabric.sh* 来启动 *test-network*，使用 *networkDown.sh* 来停止 *test-network*。

当执行 *startFabric.sh* 时，除了设置默认的实现语言之外，它的第一步是停止网络。这是为了防止与资源及其运行时状态相关的运行时问题。

###### 警告

测试网络没有持久性，每次执行都会启动一个新的网络。

## 理解 startFabric.sh 的结构

在执行 *startFabric.sh* 之前，让我们先来看一下它。默认的实现语言是 Go。脚本中的这一行设置了默认的实现为 Go：

```
CC_SRC_LANGUAGE=${1:-"go"}
```

您可以通过提供支持的参数来选择另一种支持的实现语言，比如 JavaScript，如下所示：

```
$ ./startFabric.sh javascript
```

在设置实现语言之后，运行以下命令：

```
# clean out any old identities in the wallets
rm -rf javascript/wallet/*
rm -rf java/wallet/*
rm -rf typescript/wallet/*
rm -rf go/wallet/*
```

正如您所见，所有的实现都删除了它们的 *wallet* 子目录内容。在执行 Fabcar 客户端应用程序时，我们将讨论钱包。

最后，脚本执行：

```
./network.sh down
./network.sh up createChannel -ca -s couchdb
./network.sh deployCC -ccn fabcar -ccv 1 -cci initLedger -ccl ${CC_SRC_LANGUAGE} -ccp ${CC_SRC_PATH}
```

正如您所见，*startFabric.sh* 调用 *network.sh* 脚本三次，并提供不同的参数。第一次调用指示 *network.sh* 关闭网络。如果网络未运行，也不会出错；它总是运行，并且是确保启动一个新的无错误网络的安全措施。

第二次执行，或者 `createChannel` 命令，启动网络，创建一个通道（网络），并将世界状态数据库设置为 CouchDB。此命令完成后，网络就可以运行了。

第三次执行将 Fabcar 链码（智能合约）部署到网络中。网络提供许多默认的*.sh*脚本，例如通道名称为*mychannel*。完成后，Fabcar 网络已启动运行，并且我们的 Fabcar 智能合约已部署和初始化。

## 执行 startFabric.sh

现在我们已经看过了*startFabric.sh*脚本并理解了它的作用，让我们执行它并简要审查输出。它很冗长但信息丰富，因此熟悉它将有助于我们更好地理解*network.sh*脚本为我们所完成的工作。

打开一个 shell 并确保 Docker 正在运行。您可以通过执行以下操作来检查 Docker 是否正在运行：

```
$ docker -v
Docker version 19.03.13, build 4484c46d9d
```

切换到安装了第四章中描述的先决条件的位置，并执行以下操作：

```
$ ./startFabric.sh javascript
```

您的控制台将开始滚动文本输出并继续完成。该脚本将需要几分钟才能完成。完成后，您可以保存文本输出以供使用和学习。它包含用于启动网络的逐步序列。我们对最后一个命令和用于部署 Fabcar 智能合约的命令序列感兴趣。

在我们查看智能合约部署之前，让我们快速浏览一下输出的第一部分，因为它提供了有用的信息，包括通道名称和版本：

```
Start network command
Creating channel 'mychannel'.

If network is not up, starting nodes with CLI timeout of '5' tries and CLI delay of '3' seconds and
using database 'couchdb with crypto from 'Certificate Authorities'

Bringing up network
LOCAL_VERSION=2.3.0
DOCKER_IMAGE_VERSION=2.3.0
CA_LOCAL_VERSION=1.4.9
CA_DOCKER_IMAGE_VERSION=1.4.9
```

我们看到我们的通道名称是*mychannel*，Fabric 版本是 2.3.0，由`LOCAL_VERSION`和`DOCKER_IMAGE_VERSION`表示。凭证颁发机构的版本为 1.4.9。

## 生成 Fabric 证书颁发机构

接下来，我们被告知脚本将为 CAs 生成证书，创建网络，并为组织 1、组织 2 和订单凭证颁发机构（如以下输出所示）创建 Docker 容器。凭证颁发机构在管理每个组织和订单者的身份方面起着重要作用：

```
Generate certificates using Fabric CA's

Creating network "net_test" with the default driver

Creating ca_org2    ... done
Creating ca_org1    ... done
Creating ca_orderer ... done
```

接下来我们被告知脚本将为组织 1 创建身份。这将需要几个命令来完成。脚本为组织 2 和订购者重复这些步骤。

## 创建 Org1 身份

我们可以使用这个输出来捕捉命令并记录它们的预期结果。您可以使用一个简单的模式来实现这一点。首先，脚本使用描述性和信息性文本来引导读者。其次，脚本命令以前导的`+`符号清晰地标识出来。例如，以下信息性文本告诉我们，动作是注册 CA 管理员，接着是`+`字符和下一行的命令。执行此操作的命令是`fabric-ca-client`。命令后跟着命令输出：

```
Enroll the CA admin
+ fabric-ca-client enroll -u https://admin:adminpw@localhost:7054 --caname ca-org1 --tls.certfiles
/markmorris/Desktop/fabric-samples/test-network/organizations/fabric-ca/org1/tls-cert.pem
2021/02/14 17:26:55 [INFO] Created a default configuration file at /markmorris/Desktop/fabric-
samples/test-network/organizations/peerOrganizations/org1.example.com/fabric-ca-client-config.yaml
2021/02/14 17:26:55 [INFO] TLS Enabled
2021/02/14 17:26:55 [INFO] generating key: &{A:ecdsa S:256}
2021/02/14 17:26:55 [INFO] encoded CSR
2021/02/14 17:26:55 [INFO] Stored client certificate at /markmorris/Desktop/fabric-samples/test-
network/organizations/peerOrganizations/org1.example.com/msp/signcerts/cert.pem
2021/02/14 17:26:55 [INFO] Stored root CA certificate at /markmorris/Desktop/fabric-samples/test-
network/organizations/peerOrganizations/org1.example.com/msp/cacerts/localhost-7054-ca-org1.pem
2021/02/14 17:26:55 [INFO] Stored Issuer public key at /markmorris/Desktop/fabric-samples/test-
network/organizations/peerOrganizations/org1.example.com/msp/IssuerPublicKey
2021/02/14 17:26:55 [INFO] Stored Issuer revocation public key at /markmorris/Desktop/fabric-
samples/test-network/organizations/peerOrganizations/org1.example.com/msp/IssuerRevocationPublicKey
```

脚本执行的命令，包括`fabric-ca-client`，都包含在 *fabric-samples* 的 *bin* 子目录中。这意味着我们可以使用此输出作为模型或指南来执行这些命令。这种模式对于每个命令和命令组重复。脚本分组可重复的序列；例如，我们使用一个通用序列来创建 org1 身份，创建 org2 身份和创建订购者身份，但提供不同的参数。

## 调用 Peer Chaincode

在查看脚本执行的最后一个命令之后，即`peer chaincode invoke`之后，我们将讨论智能合约部署。我们使用这个最后一个命令来初始化 Fabcar 智能合约：

```
+ peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls
--cafile /markmorris/Desktop/fabric-samples/test-
network/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.
example.com-cert.pem -C mychannel -n fabcar --peerAddresses localhost:7051 --tlsRootCertFiles
/markmorris/Desktop/fabric-samples/test-
network/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --
peerAddresses localhost:9051 --tlsRootCertFiles /markmorris/Desktop/fabric-samples/test-
network/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt --isInit
-c '{"function":"initLedger","Args":[]}'
```

`peer`命令有许多子命令，我们感兴趣的一个是`peer chaincode invoke`。`invoke`子命令可以调用智能合约函数，我们很快将这样做。最后一个参数开关是`-c`。它后面跟着一个指定要执行的智能合约函数和任何可选参数的参数。我们将使用此命令作为调用智能合约事务和评估查询的一种方法。

我们此脚本的主要目的是启动我们的完全功能的 Fabric 网络，以便我们可以开发 Fabric 智能合约。次要目的是捕获并利用脚本输出。为了实现这个次要目的，我们已经有一个命令可以用来调用我们的智能合约并查询它。接下来，我们可以利用脚本输出的智能合约部署部分，通过在维护和测试中利用它，我们将在第六章中讨论。

在开发智能合约时，我们希望有一个快速的迭代周期。当我们需要重复部署或重新部署智能合约时，启动和停止网络将不起作用，因此我们需要定制脚本并定制如何执行我们的部署以促进快速迭代。Hyperledger Fabric v2 配备了外部构建器和启动器，允许链码独立部署和执行（第九章更详细地介绍了此内容）。首先，我们可以检查脚本输出部署智能合约的点，以捕获显示如何部署它的步骤。

要找到脚本输出的部署部分，请转到输出的末尾，向上滚动到最后一个命令的开头：

```
+ peer chaincode invoke...
```

从那里，向上滚动，直到看到这个：

```
Query chaincode definition successful on peer0.org2 on channel 'mychannel'
```

这是脚本输出的部署部分的结尾。要找到脚本输出的部署部分的开头，请向上滚动，直到看到以下内容：

```
deploying chaincode on channel 'mychannel'
```

这是脚本输出的部署部分的开头。

在第六章中，我们将查看所需的命令，并使用脚本输出帮助我们进行维护和测试的部署。现在，让我们看一下脚本执行的六步部署顺序：

1.  *peer0.org1* 上已打包链码

1.  *peer0.org1* 上已安装链码

1.  *peer0.org2* 上已安装链码

1.  *peer0.org1* 上的链码定义已获批准，通道为 *mychannel*

1.  链码定义已经在通道*mychannel*上由*peer0.org2*批准。

1.  链码定义已经提交到通道*mychannel*。

这六个步骤是我们部署智能合约以便调用它们所必须执行的操作。我们不包括脚本执行的检查或查询，因为它们只是状态的信息。从这六个操作中，我们可以得出我们需要执行的四组部署操作：

1.  打包

1.  安装

1.  批准

1.  提交

我们只需执行一次打包操作——在这种情况下，在*peer0.org1*上。然后，我们可以根据需要将包分发给组织（*peer0.org2*）。安装操作必须为每个背书节点执行。批准操作必须按照策略由所有组织执行，并且提交操作只执行一次，但在命令中包括所有组织的背书节点。在第七章中，我们提供了执行所有这些命令的脚本文件。

通过成功完成*startFabric.sh*，Fabcar 测试网络已经启动运行。您可以随时生成此输出，以获取命令示例或验证可能进行的更改。

我们的 Fabcar 智能合约已部署并初始化。脚本执行了一个调用 Fabcar 的命令。我们还可以使用该命令来调用 Fabcar，下面我们将看到。但在离开之前，我们应该赞赏此输出的效用。它映射了用于从头创建具有订购者、订购者凭证授权机构和两个组织（每个组织都有一个对等节点、一个数据库和一个凭证授权机构）的 Fabric 网络的命令和命令响应。负责该输出的*network.sh*脚本是一个资源，我们可以根据需要加以利用。目前，我们所需要的一切都由此脚本提供。它启动了我们的测试网络，部署了 Fabcar 智能合约并对其进行了初始化。

我们现在可以调用 Fabcar 的智能合约函数。

# 调用智能合约事务

`peer chaincode invoke`命令是我们将查看并执行以调用我们的 Fabcar 智能合约函数的第一种方法。我们将查看并使用下一种方法，其中包含可以用于开发智能合约客户端的 Hyperledger Fabric SDK for Node.js。

通过使用 Hyperledger Fabric SDK for Node.js，您可以开发命令行 Fabric 智能合约客户端，例如 Fabcar，以及将 UI 合并到 Fabric 智能合约客户端应用程序设计中的 Fabric 智能合约客户端。我们在第六章中讨论了命令行 Fabcar 智能合约客户端的 UI 版本。现在让我们来看一下并执行`peer chaincode invoke`方法。

## 节点命令

`peer`命令是 Hyperledger Fabric 核心二进制文件。当您安装先决条件时，*peer*二进制文件以及其他几个二进制文件将被下载并放置在*fabric-samples*的*bin*子目录中。该二进制文件有五个功能或子命令，它执行：

```
peer chaincode [*option*] [*flags*]
peer channel   [*option*] [*flags*]
peer node      [*option*] [*flags*]
peer version   [*option*] [*flags*]
```

`peer node`命令是用于充当 Fabric 节点或 Fabric 节点的子命令：

```
Creating peer0.org1.example.com ... done
Creating peer0.org2.example.com ... done
```

在*test-network*的*docker*子目录中检查*docker-compose-test-net.yaml*，您会看到执行启动节点的启动命令：

```
command: peer node start
```

我们感兴趣的`peer`子命令是`chaincode`子命令。该子命令还有几个子命令：

```
install
instantiate
invoke
list
package
query
signpackage
upgrade
```

我们想使用`invoke`子命令。在启动测试网络的脚本中使用了其他一些`peer chaincode`子命令，并且可以通过搜索我们从启动时保存的输出文本找到。

使用`peer`命令涉及许多参数，因此在实践环境中，我们使用变量来最小化生成的`peer`命令行文本的长度。我们将使用环境变量，以便我们可以针对我们的 Fabcar 测试网络执行`peer chaincode invoke`。

当我们执行*startFabric.sh*时，我们位于*fabric-samples/fabcar*子目录中。脚本执行了一个改变目录的命令，同时保存了当前目录，即*fabric-samples/fabcar*。脚本切换到*fabric-samples/test-network*。这使*fabric-samples/test-network*成为执行脚本的当前目录。这对我们很重要，因为我们将从脚本中重用`peer chaincode invoke`命令来执行我们的`invoke 命令`。为了使其工作，我们需要打开一个 shell 并将目录更改为*fabric-samples/test-network*。然后执行这些导出命令以配置您的环境，以便在*bin*子目录中找到*peer*二进制文件，在*fabric-samples/config*中找到创建的*test-network*配置，并且`peer`需要找到的其他信息以正确执行：

```
export PATH=${PWD}/../bin:$PATH 
export FABRIC_CFG_PATH=$PWD/../config/
export CORE_PEER_TLS_ENABLED=true
export CORE_PEER_LOCALMSPID="Org1MSP"
export
CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.
example.com/tls/ca.crt
export
CORE_PEER_MSPCONFIGPATH=${PWD}/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.
com/msp
export CORE_PEER_ADDRESS=localhost:7051
```

一旦您执行了这些，您的环境就配置为执行`peer`。要测试这个，请执行以下操作：

```
peer version
```

您的版本可能不同，但您应该看到类似于这样的结果：

```
peer:
 Version: 2.3.0
 Commit SHA: ec81f3e74
 Go version: go1.14.12
 OS/Arch: darwin/amd64
 Chaincode:
  Base Docker Label: org.hyperledger.fabric
  Docker Namespace: hyperledger
```

定位初始化 Fabcar 智能合约的`peer chaincode invoke`命令，并将其复制到您的编辑器中，以便我们进行重构。请记住，它是在启动脚本输出中执行的最后一个命令，并且看起来像这样，除了您的路径将不同：

```
peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls --
cafile /Volumes/WDCWD10JPLX/markmorris/Desktop/v2.3.0/fabric-samples/test-
network/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.
example.com-cert.pem -C mychannel -n fabcar --peerAddresses localhost:7051 --tlsRootCertFiles
/Volumes/WDCWD10JPLX/markmorris/Desktop/v2.3.0/fabric-samples/test-
network/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt 
--peerAddresses localhost:9051 --tlsRootCertFiles /Volumes/WDCWD10JPLX/markmorris/Desktop/v2.3.0/fabric-
samples/test-
network/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt 
--isInit -c '{"function":"initLedger","Args":[]}'
```

我们想要修改此命令末尾的以下文本

```
--isInit -c '{"function":"initLedger","Args":[]}'
```

转换为这样：

```
-c '{"Args":["queryAllCars"]}'
```

确保删除`--isInit`开关。由于我们移除了初始化执行的命令，它会失败并报错，因为此开关是通知对等方执行初始化的。

一旦您修改了命令文本，它应该是这样的：

```
peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls--cafile
/Volumes/WDCWD10JPLX/markmorris/Desktop/v2.3.0/fabric-samples/test-
network/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.
example.com-cert.pem -C mychannel -n fabcar --peerAddresses localhost:7051 --tlsRootCertFiles
/Volumes/WDCWD10JPLX/markmorris/Desktop/v2.3.0/fabric-samples/test-
network/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --
peerAddresses localhost:9051 --tlsRootCertFiles /Volumes/WDCWD10JPLX/markmorris/Desktop/v2.3.0/fabric-
samples/test-
network/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt -c
'{"Args":["queryAllCars"]}'
```

现在将命令复制到您的 shell 并执行它。输出将如下所示：

```
 [chaincodeCmd] chaincodeInvokeOrQuery -> INFO 001 Chaincode invoke successful. result: status:200
payload:"[{\"Key\":\"CAR0\",\"Record\":{\"color\":\"blue\",\"docType\":\"car\",\"make\":\"Toyota\", \"model\":
\"Prius\",\"owner\":\"Tomoko\"}},{\"Key\":\"CAR1\",\"Record\":{\"color\":\"red\", \"docType\":\"car\",
\"make\":\"Ford\",\"model\":\"Mustang\",\"owner\":\"Brad\"}},{\"Key\":\"CAR2\",\”Record\":{\”color\":\"green\",
\"docType\":\"car\",\"make\":\"Hyundai\",\"model\":\"Tucson\",\"owner\":\"Jin
Soo\"}},{\"Key\":\"CAR3\",\"Record\":{\"color\":\"yellow\",\"docType\":\"car\",\"make\":\"Volkswagen\",
\"model\":\"Passat\",\"owner\":\"Max\"}},{\"Key\":\"CAR4\",\"Record\":{\"color\":\"black\",\"docType\":
\"car\",\"make\":\"Tesla\",\"model\":\"S\",\"owner\":\"Adriana\"}},{\"Key\":\"CAR5\",\"Record\":{\"color"\”:\
"purple\",\"docType\":\"car\",\"make\":\"Peugeot\",\”model\”:\”205\”,\”owner\":\”Michel"\"}},{\"Key\":\
"CAR6\",\"Record\":{\"color\":\"white\",\"docType\":\"car\",\"make\":\"Chery\",\"model\":\"S22L\",\"owner\"
:\"Aarav\"}},{\"Key\":\"CAR7\",\”Record\”:{\”color\":\"violet\",\"docType\":\"car\",\"make\”:\"Fiat\",
\"model\":\"Punto\",\"owner\":\"Pari\"}},{\"Key\":\"CAR8\",\"Record\":{\"color\":\"indigo\",\"docType\":\"car\",
\"make\":"Tata\",\"model\":\"Nano\",\"owner\":\"Valeria\"}},{\"Key\":\"CAR9\",\"Record\":{\"color\"
:\"brown\",\"docType\":\"car\",\"make\”":\"”Holden\",\"model\":\"Barina\",\"owner\":\"Shotaro\"}}]"
```

我们刚刚调用了 Fabcar 智能合约。我们调用的是一个查询，即读取事务。当我们调用时，我们执行的是写入或读取事务。读取事务不会提交到总账上；只有写入事务会提交，前提是它们得到了正确的认可和验证。

我们调用的 Fabcar 智能合约事务是 `queryAllCars` 事务。查看 *fabcar.js*，这个 Fabcar 事务调用了 `getStateByRange`，参数设置为空字符串。这将返回特定汽车键的所有数据，我们在结果中看到了这一点：

```
ctx.stub.getStateByRange(startKey, endKey)
```

记住，`ctx` 对象是传递给每个智能合约事务的第一个参数。

它提供对 `stub` 对象的访问，该对象实例化了一个 `ChaincodeStub` 类（`IChaincodeStub` 的实现），以及对 `clientIdentity` 对象的访问，该对象实例化了一个 `ClientIdentity` 类（实现了 `IClientIdentity`）：

```
export class Context {
    stub: ChaincodeStub;
    clientIdentity: ClientIdentity;
```

这两个类，`ChaincodeStub` 和 `ClientIdentity`，是 *fabric-shim* 包的一部分，这是一个 Node.js 模块。我们不直接使用 *fabric-shim* 模块，因为我们使用 *fabric-contract-api* 包，它为我们提供了 `Contract` 对象供我们使用：

```
const { Contract } = require('fabric-contract-api');
```

`Contract` 对象通过 `Context` 对象 `ctx` 提供对 `ChaincodeStub` 和 `ClientIdentity` 的访问，所有智能合约函数都将其作为第一个参数接收。`Contract` 对象还提供了我们可以在调用事务之前和之后使用的拦截器函数。在下一章中，我们将讨论维护和测试时会看到这些内容。

现在让我们使用 `peer chaincode invoke` 来调用 Fabcar 写入事务。我们可以使用与查询相同的命令。我们所需要做的就是更改 `-c` 开关的参数。让我们执行 `changeCarOwner`：

```
-c '{"Args":["changeCarOwner", "CAR0", "Mark"]}'
```

当你改变 `-c` 开关参数后，你应该有这样的一个命令：

```
peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls --cafile
/Volumes/WDCWD10JPLX/markmorris/Desktop/v2.3.0/fabric-samples/test-
network/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.
example.com-cert.pem -C mychannel -n fabcar --peerAddresses localhost:7051 --tlsRootCertFiles
/Volumes/WDCWD10JPLX/markmorris/Desktop/v2.3.0/fabric-samples/test-
network/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt --
peerAddresses localhost:9051 --tlsRootCertFiles /Volumes/WDCWD10JPLX/markmorris/Desktop/v2.3.0/fabric-
samples/test-
network/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt -c
'{"Args":["changeCarOwner", "CAR0", "Mark"]}'
```

现在执行它并查看结果：

```
[chaincodeCmd] chaincodeInvokeOrQuery -> INFO 001 Chaincode invoke successful. result: status:200
```

这显示了事务成功执行。由于我们更改了`CAR0`的所有者，请让我们使用另一个查询再次检查它，但这次是针对特定数据。再次使用相同的`peer`命令，我们只需要更改`-c`开关参数：

```
-c '{"Args":["queryCar", "CAR0"]}'
```

执行后，您应该看到这个：

```
[chaincodeCmd] chaincodeInvokeOrQuery -> INFO 001 Chaincode invoke successful. result: status:200
payload:"{\"color\":\"blue\",\"docType\":\"car\",\"make\":\"Toyota\",\"model\":\"Prius\",\"owner\":\"Mark
\"}"
```

成功了！我们改变了所有者。稍后您将看到如何获取与同一键关联的交易历史记录。我们的写入事务`changeCarOwner`的键是`CAR0`。请记住，总账有两个部分：世界状态和区块链总账（简单来说，是不可变链接列表的基于文件的实现）。世界状态是给定键的区块链的当前状态。我们的世界状态由 CouchDB 为我们的 Fabcar 测试网络实现。

我们可以通过使用本章前面讨论的 CouchDB 浏览器界面来查看我们的更改。让我们在世界状态数据库中查看我们的更改。由于我们在本章前面已经讨论过访问 CouchDB，打开您的浏览器并使用用户名`**admin**`和密码`**adminpw**`登录 CouchDB：

[*http://127.0.0.1:5984/_utils/#login*](http://127.0.0.1:5984/_utils/#login)

然后在 CouchDB 中转到此 URL：

[*http://127.0.0.1:5984/_utils/#database/mychannel_fabcar/CAR0*](http://127.0.0.1:5984/_utils/#database/mychannel_fabcar/CAR0)

您应该看到`CAR0`的所有者是`Mark`，如图 5-4 中所示。

![CouchDB 中的 CAR0 记录](img/HLF_0504.png)

###### 图 5-4。CouchDB 中的`CAR0`记录

我们将在下一章节中更深入地使用`peer chaincode invoke`命令进行更高级的目的。现在让我们看一下 Fabcar 客户端，看看它如何调用 Fabcar 智能合约。

## Node.js 命令行应用程序的 Fabric SDK

在 第四章 中，我们深入研究了 Fabcar 智能合约。现在，我们将研究 Fabcar 智能合约客户端，并使用它来调用合约。如本章前面所述，Fabcar 智能合约客户端是四个 Node.js JavaScript 命令行应用程序的组合：*enrollAdmin.js, invoke.js, query.js,* 和 *registerUser.js*。

我们将执行每个模块，并查看它们如何工作来调用 Fabcar 智能合约。首先，打开一个 shell 并切换到目录 *fabric-samples/fabcar/javascript*。Fabcar 客户端是一个 Node.js 命令行应用程序，因此我们需要执行以下操作：

```
npm install
```

此命令将安装项目依赖项到我们的 Fabcar 项目中。当命令完成时，您应该会有一个 *node_modules* 子目录。这是这里列出的依赖项放置的位置：

```
"dependencies": {
    "fabric-ca-client": "².1.0",
    "fabric-network": "².1.0"
},
```

如果我们在 *node_modules* 子目录中查找已安装的 Fabric 模块，我们会发现列在这里的 Fabric 模块：

```
fabric-ca-client
fabric-common
fabric-network
fabric-protos
```

这些模块代表了 Hyperledger Fabric 的 Node.js SDK，可以在 [Fabric GitHub 仓库](https://github.com/hyperledger/fabric-sdk-node) *[fabric-sdk-node](https://github.com/hyperledger/fabric-sdk-node)* 中找到。*fabric-protos* 模块实现了 Protocol Buffers 协议，这是一种二进制编码的通信协议。我们不必担心这个模块，也不直接使用它。*fabric-common* 模块包含 *fabric-ca-client* 和 *fabric-network* 模块共同使用的代码。*fabric-ca-client* 模块被 Fabcar 客户端使用，但对于 Fabric 智能合约客户端并非必需。只有当您的智能合约客户端需要与 Fabric CA 交互以管理用户证书的生命周期时，才需要导入和使用 *fabric-ca-client*。这包括注册、注册、续订和撤销用户的能力。如果您的智能合约客户端不执行这些功能，则不需要 *fabric-ca-client*。

*fabric-network*模块是唯一需要的 Fabric 模块，用于 Fabric 智能合约客户端。它将您的客户端连接到网络，并提供了调用交易（包括写入分类账、查询世界状态和分类账）的能力。

现在我们的依赖已经安装好了，我们可以进行以下操作：

+   注册我们的应用程序管理员。

+   注册我们的应用用户。

+   调用一个写入交易。

+   查询世界状态。

首先，我们需要注册一个应用程序管理员来创建一个管理员级别的钱包。然后我们可以在应用程序中注册用户，并为其分配一个用户钱包，以确保网络访问的安全性。

### 注册我们的应用程序管理员。

要注册我们的管理员，我们执行*enrollAdmin.js*应用程序：

```
node ./enrollAdmin.js
```

你应该看到以下结果：

```
Successfully enrolled admin user "admin" and imported it into the wallet
```

现在我们可以执行*registerUser.js*来注册我们的用户：

```
node ./registerUser.js
```

你应该看到以下结果：

```
Successfully registered and enrolled admin user "appUser" and imported it into the wallet
```

太棒了！现在我们可以使用刚刚注册的用户身份来调用我们的智能合约。但首先让我们看看这里发生了什么。我们需要了解这两个应用程序的情况，以便在调用交易时使用身份。

身份证明将我们与组织联系起来，成为成员并且允许我们执行交易。让我们首先执行*enrollAdmin.js*应用程序，因为它必须首先执行。在你的编辑器中打开*enrollAdmin.js*。我们不会逐行解析，而是专注于重要的部分。首先是导入：

```
const FabricCAServices = require('fabric-ca-client');
const { Wallets } = require('fabric-network');
```

我们可以看到从*fabric-ca-client*和*fabric-network*导入的内容。我们从*fabric-ca-client*中导入所有内容，只从*fabric-network*中导入*Wallets*。这是一个 Node.js 命令行应用程序，因此我们有一个`main`函数来执行所有应用逻辑。当我们看 Fabcar UI 时，这将派上用场，因为我们将 Fabcar 转移到了 UI。现在主要逻辑开始了：

```
// load the network configuration
const ccpPath = path.resolve(__dirname, '..', '..', 'test-network', 'organizations', 'peerOrganizations',
'org1.example.com', 'connection-org1.json');
const ccp = JSON.parse(fs.readFileSync(ccpPath, 'utf8'));

// Create a new CA client for interacting with the CA.
const caInfo = ccp.certificateAuthorities['ca.org1.example.com'];
const caTLSCACerts = caInfo.tlsCACerts.pem;
const ca = new FabricCAServices(caInfo.url, { trustedRoots: caTLSCACerts, verify: false },
caInfo.caName);
```

首先，组织 1 的连接配置文件的文件系统路径被组装并读取。此路径通常使用 *ccp-template.json* 和 *ccp-template.yaml* 文件作为模板，传递组织名称、对等端口、CA 端口和 CA Privacy Enhanced Mail (PEM) 证书以生成组织连接文件。第七章更详细地讨论了这一点。这将网络配置定义给客户端。

一旦加载连接配置文件，将设置证书颁发机构信息和证书颁发机构 TLS 证书。使用 CA 信息和 TLS 证书，创建 CA 对象。我们使用自签名证书，因此将 `verify` 参数设置为 `false`。

在我们创建了我们的 CA 之后，我们创建了我们的钱包：

```
// Create a new filesystem-based wallet for managing identities.
const walletPath = path.join(process.cwd(), 'wallet');
const wallet = await Wallets.newFileSystemWallet(walletPath);
console.log(`Wallet path: ${walletPath}`);
```

首先，我们创建一个路径。代码正在使用当前路径，应该是我们的 *fabric-samples/fabcar/javascript* 子目录所在的位置。代码将 *wallet* 追加到路径中。这是我们 *fabric-samples/fabcar/javascript* 子目录中 *wallet* 子目录。将完整路径作为 `Wallets.newFileSystemWallet` 函数的参数，我们创建一个将用于存储身份的钱包对象。接下来，我们检查 *admin* 是否已经注册：

```
// Check to see if we've already enrolled the admin user.
const identity = await wallet.get('admin');
if (identity) {
    console.log('An identity for the admin user "admin" already exists in the wallet');
    return;
}
```

我们设计只能注册一次。如果管理员尚未注册，我们将继续并注册管理员：

```
// Enroll the admin user, and import the new identity into the wallet.
const enrollment = await ca.enroll({ enrollmentID: 'admin', enrollmentSecret: 'adminpw' });
const x509Identity = {
    credentials: {
        certificate: enrollment.certificate,
        privateKey: enrollment.key.toBytes(),
    },
    mspId: 'Org1MSP',
    type: 'X.509',
};
await wallet.put('admin', x509Identity);
console.log('Successfully enrolled admin user "admin" and imported it into the wallet');
```

我们创建的 CA 现在用于执行注册函数。我们可以看到它将用户 ID 和密码作为 `admin` 的 `enrollmentID` 和 `enrollmentSecret`。然后，我们使用刚刚创建的注册对象创建了一个 `x509Identity` 对象。我们正在创建一个包含凭据的 `x509Identity`——一个包含证书和私钥的对象，这两者都是由 CA 注册函数创建并返回的。

除了凭证之外，我们还添加了标识该身份所属组织和身份类型的对象元数据。这里的 `x509Identity` 表示包含与私钥配对的公钥的证书。创建了身份后，我们将其传递给我们创建的钱包，该钱包将其存储。

你应该在 *wallet* 子目录中看到一个名为 *admin.id* 的文件。如果你查看它，你可以看到我们刚刚讨论过的数据结构。这就是 *enrollAdmin.js* 应用程序的全部内容。它的目的是注册管理员。为了实现这一点，它需要一个 CA 和一个钱包。CA 来自 *fabric-ca-client*，钱包来自 *fabric-network*。这个顺序是特定于管理员的。现在让我们看看 *registerUser.js* 有什么不同。

### 注册我们的应用用户。

*registerUser.js* 的开头包含与 *enrollAdmin.js* 相同的导入，但顺序不同，这没关系。像 *enrollAdmin.js* 一样，它的逻辑包含在一个 `main` 函数中。`main` 逻辑开始与 *enrollAdmin.js* 相同，加载网络配置，创建证书颁发机构和创建钱包。我们可以看到一个模式：

+   加载网络配置。

+   创建证书颁发机构。

+   创建钱包。

然后跟随的是检查，以确定用户是否在钱包中拥有身份，这表明用户已经注册和注册：

```
const userIdentity = await wallet.get('appUser');
```

如果用户已经在钱包中，我们就返回。如果你执行*startFabric.sh*并且*钱包*子目录包含这些身份，就会发生这种情况。此时，这些身份在 Fabcar 测试网络中并不存在。Fabcar 应用程序不适用于用户的多次注册。当发生这种情况时，你需要删除*钱包*子目录的内容，然后再次尝试客户端。接下来，我们检查*钱包*子目录中的`admin`身份，因为我们总是首先执行*enrollAdmin.js*。如果没有找到`admin`，我们就返回。在代码的这一点上，*registerUser.js*和*enrollAdmin.js*不同。它们不同是因为构建用户的身份与构建管理员身份不同。

要构建用户身份，我们首先使用*钱包*来获取`x509`类型的`提供者`，并使用它从`admin`身份创建一个`用户`对象。我们将使用这个身份来在注册我们的应用用户时向 CA 进行身份验证：

```
const provider = wallet.getProviderRegistry().getProvider(adminIdentity.type);
const adminUser = await provider.getUserContext(adminIdentity, 'admin');
```

接下来，我们使用 CA 注册我们的应用用户，提供我们的组织、我们的 ID 和我们的角色。我们提供了通过`x509 提供者`创建的`admin`用户。CA 注册我们的应用用户，并返回一个注册密钥：

```
const secret = await ca.register({
    affiliation: 'org1.department1',
    enrollmentID: 'appUser',
    role: 'client'
}, adminUser);
```

从这一点开始，逻辑与*enrollAdmin.js*中相同，只是*enrollAdmin.js*使用管理员密码作为注册证书的密钥，而*registerUser.js*将使用我们在使用管理员用户注册时从 CA 获得的密钥来进行身份验证。因此，我们需要管理员身份，因为它用于注册用户。应用用户密钥就像密码一样，只是用户不会知道它，也不需要知道。他们有一个身份，在这个实现中是`x509`类型，并且存储在钱包中，这是一个基于文件系统的存储。现在我们可以执行*invoke.js*，然后执行*query.js*并比较两者。

### 调用写事务

*invoke.js* 应用程序有一个主函数，所有逻辑都包含在主函数中。该应用程序仅从 *fabric-network* 导入：

```
const { Gateway, Wallets } = require('fabric-network');
```

这意味着不需要与 CA 交互来调用事务。像 *enrollAdmin.js* 和 *registerUser.js* 一样，它也利用了 *fabric-network* 中的 *Wallets*。这是有道理的，因为我们需要一个身份来向网络提交请求，而客户端的身份存储在 *wallet* 中。

###### 注意

用户可以拥有多个身份，每个身份都有唯一的名称和用途，就像驾驶执照、学生证、护照等等。

来自 *fabric-network* 的 `Gateway` 是我们连接到网络的手段，我们很快就会看到。

逻辑从我们在 *enrollAdmin.js* 和 *registerUser.js* 中看到的熟悉代码开始加载网络配置，该配置包含了连接到网络、创建钱包和检查身份的信息。我们在这里看到的是贯穿应用程序的样板代码，这是我们希望提取并放置在公共代码中的内容：

```
// load the network configuration
const ccpPath = path.resolve(__dirname, '..', '..', 'test-network', 'organizations', 'peerOrganizations',
'org1.example.com', 'connection-org1.json');
let ccp = JSON.parse(fs.readFileSync(ccpPath, 'utf8'));

// Create a new filesystem-based wallet for managing identities.
const walletPath = path.join(process.cwd(), 'wallet');
const wallet = await Wallets.newFileSystemWallet(walletPath);
console.log(`Wallet path: ${walletPath}`);

// Check to see if we've already enrolled the user.
const identity = await wallet.get('appUser');
if (!identity) {
    console.log('An identity for the user "appUser" does not exist in the wallet');
    console.log('Run the registerUser.js application before retrying');
    return;
}
```

我们需要用户身份存在，以便网关可以找到它，如果不存在，我们就返回。要连接到网络，我们使用从 *fabric-network* 导入的 `Gateway` 来创建一个 `gateway` 对象，并使用它来连接。我们传递给 `connect` 函数的参数是连接信息、钱包、要使用的身份名称以及用于定位对等方的一些发现选项：

```
// Create a new gateway for connecting to our peer node.
const gateway = new Gateway();
await gateway.connect(ccp, { wallet, identity: 'appUser', discovery: { enabled: true, asLocalhost: true }
});
```

连接后，我们使用网关获取网络，这是由我们的通道名称标识的通道：

```
// Get the network (channel) our contract is deployed to.
const network = await gateway.getNetwork('mychannel');
```

使用 `network` 对象，我们获得了与 Fabcar 智能合约的连接：

```
// Get the contract from the network.
const contract = network.getContract('fabcar');
```

最后，我们开始调用我们的智能合约。我们正在执行一个将更改分类帐的事务，因此这是一个写事务，并且我们希望它被提交。我们要使用的 `contract` API 函数是 `submitTransaction`。这将使用以下参数调用我们的 `createCar` 智能合约函数：

```
// Submit the specified transaction.
// createCar transaction - requires 5 argument, ex: ('createCar', 'CAR12', 'Honda', 'Accord', 'Black', 'Tom')
// changeCarOwner transaction - requires 2 args , ex: ('changeCarOwner', 'CAR12', 'Dave')
await contract.submitTransaction('createCar', 'CAR12', 'Honda', 'Accord', 'Black', 'Tom');
console.log('Transaction has been submitted');
```

如你所见，我们通过`contract` API 间接调用智能合约。这种设计模式非常强大，但如果不实施措施来防止由于意外字符或二进制数据而导致的意外副作用，就会带来风险。应该实施最佳的行业实践来验证和保护数据完整性。

最后，网关断开连接，应用程序退出：

```
// Disconnect from the gateway.
await gateway.disconnect();
```

现在让我们执行*invoke.js*：

```
node ./invoke.js
```

你应该看到以下结果：

```
Transaction has been submitted
```

你注意到处理和返回的时间了吗？提交与查询的处理时间有很大的差异，下一步当我们执行*query.js*并返回我们提交的事务结果时，我们会看到这一点，这个事务创建了一辆新的汽车。

### 查询世界状态

让我们执行*query.js*，比较它的逻辑与*invoke.js*，看看它们之间的差异和共性：

```
node ./query.js
```

你应该看到以下结果：

```
Transaction has been evaluated, result is:
[{"Key":"CAR0","Record":{"color":"blue","docType":"car","make":"Toyota","model":"Prius","owner":"Tomoko"}
}, {"Key":"CAR1","Record":{"color":"red","docType":"car","make":"Ford","model":"Mustang","owner":"Brad"}},
{"Key":"CAR12","Record":{"color":"Black","docType":"car","make":"Honda","model":"Accord", "owner":"Tom"}},
{"Key":"CAR2","Record":{"color":"green","docType":"car","make":"Hyundai","model":"Tucson", "owner":"Jin
Soo"}},{"Key":"CAR3","Record":{"color":"yellow","docType":"car","make":"Volkswagen","model":"Passat", "own
er":"Max"}},{"Key":"CAR4","Record":{"color":"black","docType":"car","make":"Tesla","model":"S", "owner":
"Adriana"}},{"Key":"CAR5","Record":{"color":"purple","docType":"car","make":"Peugeot","model": "205","owner":
"Michel"}},{"Key":"CAR6","Record":{"color":"white","docType":"car","make":"Chery","model":"S22L", "owner":
"Aarav"}},{"Key":"CAR7","Record":{"color":"violet","docType":"car","make":"Fiat", "model":"Punto","owner":
"Pari"}},{"Key":"CAR8","Record":{"color":"indigo”,"docType":"car","make":"Tata", "model":"Nano","owner":
"Valeria"}},{"Key":"CAR9","Record":{"color":"brown","docType":"car","make":"Holden", "model":"Barina",
"owner":"Shotaro"}}]
```

你能找到我们创建的汽车，`CAR12`吗？它是在`CAR1`之后的第三辆。太好了，我们的`submitTransaction`已经提交。如果我们查看 CouchDB，我们会在我们的世界状态数据库*mychannel_fabcar*中看到这些数据。

让我们看看代码。代码是一样的，只是调用的合约 API 函数不同：

```
const result = await contract.evaluateTransaction('queryAllCars');
```

对于查询，我们使用`evaluateTransaction`，因为查询事务不会提交到总账。查询不遵循与写入事务相同的处理路径，后者将使用`submitTransaction`，因此该事务将被处理以提交到总账。

你注意到与*invoke.js*相比的处理速度的差异了吗？查询要快得多，并且可以被缓存，使它们变得更快，因为它们不访问数据库。写入时间要长得多，甚至可能永远不会提交。作为一个 Fabric 智能合约开发者，你需要为这种长时间的延迟和不确定性进行设计。在第六章中，我们将看到事件如何帮助解决这些运行约束。

我们已经执行了组成 Fabcar 智能合约客户端的四个应用程序。我们看到了它们使用的不同和相同的代码。每个应用程序执行一个应用功能，并且具有确定其执行顺序的依赖关系。您学到了我们需要首先注册一个应用程序管理员，然后使用管理员注册和登录应用程序用户。一旦我们拥有了用户身份，我们就可以提交交易以将数据提交到分类账并查询世界状态。这些应用程序是用命令行应用程序（如批处理作业或无服务器命令）实现最佳的解决方案的良好示例。

# 总结

在这一章中，你学会了如何调用 Fabric 智能合约。我们从回顾 Hyperledger *fabric-samples*、Fabcar 智能合约和 Fabric 测试网络开始。这为你提供了理解本章和下一章所使用的资源所需的背景知识。

然后，我们启动了我们的 Fabric 测试网络，并讨论了启动脚本及其输出，以了解为开发 Fabric 智能合约建立 Fabric 网络需要哪些工作。除了启动测试网络外，该脚本还部署了 Fabcar 智能合约。我们详细讨论了脚本用于部署智能合约的步骤，这将帮助您理解并执行自己智能合约的部署任务。

接下来，我们执行了组成 Fabcar 智能合约客户端的四个 Fabcar 客户端的 Node.js 命令行应用程序。与此同时，我们检查了每个 Fabcar 应用程序的代码，注意了应用程序中的通用代码和差异，以及它们对 Fabric SDK for Node.js 的使用。Fabcar 应用程序使用 SDK 调用 Fabric API 与 Fabric 智能合约、凭证机构、钱包和调用智能合约进行交互。

在下一章中，我们将把这四个应用程序重构成可以导入到一个名为 Fabcar UI 的 Node.js 和 Express.js Web 应用程序中的 Node.js 模块。该应用程序反映了四个命令行 Fabcar 应用程序的功能，但带有用户界面。您将继续学习有关 Fabric SDK for Node.js 和可用于 Fabric 智能合约开发人员的 API 的更多信息。
