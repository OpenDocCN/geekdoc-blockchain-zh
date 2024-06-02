# 第四章 智能合约开发

在本章中，您将通过查看一个简单的智能合约和用于实现 Fabric 智能合约的 Fabric API 来学习 Fabric 智能合约的开发。一旦您了解了编写智能合约和 API 的基础知识，我们就可以继续进行第五章，在那里我们将从本章内容中获取内容并应用于调用智能合约。首先，为了开始，我们需要下载 Hyperledger Fabric 开发工具。它们通过封装一个完整的双组织 Fabric 运行时和脚本来启动和关闭，提供了一个快速开始开发 Fabric 智能合约的方法。

我们将使用 Hyperledger 提供的二进制文件和来自 Fabric 项目的示例项目。这些二进制文件和示例项目将帮助我们启动一个 Fabric 测试网络，示例项目提供了几个示例智能合约，供我们学习如何开发自己的。本章将从一个名为 Fabcar 的示例项目中的示例智能合约中进行讨论。我们使用的二进制文件在所有支持的操作系统上都具有相同的名称。

本章将帮助您实现以下实际目标：

+   使用 JavaScript 编程语言编写 Fabric 智能合约

+   安装和实例化一个 Fabric 智能合约

+   验证和清理智能合约中的输入和参数

+   创建和运行简单或复杂的查询

+   在 Fabric 中使用私有数据集

# 安装先决条件并设置 Hyperledger Fabric

在我们能够开发 Fabric 智能合约之前，我们需要下载并安装下载 Hyperledger Fabric 所需的软件。要下载并设置 Hyperledger Fabric 以开发 Fabric 智能合约，我们将执行一个脚本，该脚本需要存在于您正在开发的平台上——Windows、Linux 或 Mac 上的某些软件。我们需要安装 Git、cURL、Node.js、npm、Docker 和 Docker Compose，以及 Fabric 安装脚本。

## Git

Git 用于从 GitHub 克隆 *fabric-samples* 存储库到您的本地计算机。如果您尚未安装 Git，则可以从[*https://git-scm.com/downloads*](https://git-scm.com/downloads)下载。下载并安装完成后，通过以下命令验证 Git 安装：

```
$ git --version
git version 2.26.2
```

## cURL

我们使用 cURL 从网络上下载 Fabric 二进制文件。您可以从[*https://curl.haxx.se/download.html*](https://curl.haxx.se/download.html)下载 cURL。下载并安装完成后，通过执行以下命令验证安装：

```
$ curl -V
curl 7.54.0 (x86_64-apple-darwin18.0) libcurl/7.54.0 LibreSSL/2.6.5 zlib/1.2.11 nghttp2/1.24.1
Protocols: dict file ftp ftps gopher http https imap imaps ldap ldaps pop3 pop3s rtsp smb smbs smtp smtps
telnet tftp
Features: AsynchDNS IPv6 Largefile GSS-API Kerberos SPNEGO NTLM NTLM_WB SSL libz HTTP2 UnixSockets HTTPS-
proxy
```

## Node.js 和 npm

我们将使用 JavaScript 开发我们的 Fabric 智能合约。Fabric 使用 Node.js 和 npm 处理智能合约。支持的 Node.js 版本为 10.15.3 及更高版本，以及 12.13.1 及更高版本。支持的 npm 版本为 6 及更高版本。Node.js 在安装中包含 npm。您可以从[*https://nodejs.org/en/download/*](https://nodejs.org/en/download/)下载 Node.js。您可以通过执行以下命令验证 Node.js 和 npm 的安装：

```
$ node -v
v10.15.3

$ npm -v
6.11.2
```

## Docker 和 Docker Compose

Hyperledger Fabric 由几个组件组成，每个组件都作为单独的可执行服务运行，因此 Fabric 维护了每个组件的 Docker 镜像。这些镜像托管在官方 Docker Hub 网站上。最低要求是 Docker 版本 17.06.2-ce。你可以在[*https://www.docker.com/get-started*](https://www.docker.com/get-started)获取最新版本的 Docker。安装 Docker 后，Docker Compose 也会被安装。你可以通过执行以下命令验证 Docker 版本：

```
$ docker -v
Docker version 19.03.13, build 4484c46d9d
```

然后执行以下命令验证你的 Docker Compose 版本：

```
$ docker-compose --version
docker-compose version 1.27.4, build 40524192
```

在继续之前，启动 Docker，因为 Docker 需要运行以完成 Fabric 安装脚本的安装。

## Fabric 安装脚本

创建并切换到你将用于安装 Fabric 二进制文件和样本项目的目录。脚本需要 Docker 运行，因为它需要 Docker 下载 Fabric 镜像。

该脚本将执行以下操作：

1.  下载 Fabric 二进制文件

1.  从 GitHub 仓库克隆*fabric-samples*

1.  下载 Hyperledger Fabric Docker 镜像

这是执行脚本的命令：

```
curl -sSL https://bit.ly/2ysbOFE | bash -s
```

但我们暂时不会执行这个命令。首先，我们要保存命令的输出，这样我们就可以检查它。确保你在你创建的目录中来安装 Fabric 二进制文件和样本项目，然后执行以下命令：

```
curl -sSL https://bit.ly/2ysbOFE > FabricDevInstall.sh
```

现在你可以在你喜欢的编辑器中打开*FabricDevInstall.sh*并检查脚本，看看它是如何从 GitHub 克隆*fabric-samples*，下载 Fabric 二进制文件和下载 Docker 镜像的。理解这个脚本的操作可能有助于你以后如果想要根据你的工作流程定制你的 Fabric 开发环境或者优化它。

完成脚本检查后，在 shell 中打开*FabricDevInstall.sh*，通过执行以下命令将其更改为可执行文件：

```
$ chmod +x FabricDevInstall.sh
```

现在让我们通过以下命令执行*FabricDevInstall.sh*：

```
FabricDevInstall.sh
```

一旦脚本执行完毕，我们应该已经准备好了。 *fabric-samples* 目录、Docker 映像和 Fabric 二进制文件都安装在 *fabric-samples/bin* 目录中。在您运行命令的目录中，现在应该有一个名为 *fabric-samples* 的目录。我们所需的一切都在 *fabric-samples* 中。首先，我们将深入了解 Fabcar 示例智能合约，您可以在 *fabric-samples* 目录中找到它。

## 智能合约的基本要求

Fabcar 示例智能合约是一个有效的、功能完善的基本智能合约示例。在准备投入生产之前，我们还有很多工作要做，包括安全性、错误管理、报告、监控和测试。我们想从这个示例智能合约中记住几个重要点。让我们逐一看看：

`Contract` 类

智能合约扩展了 `Contract` 类。这是一个简单的类，具有很少的函数。我们将在本章后面查看这个类。

交易上下文

所有智能合约交易函数都将交易上下文对象作为它们的第一个参数传递。此交易上下文对象是一个 `Context` 类。当我们查看 `Contract` 类时，我们也会查看这个类。

构造函数

所有智能合约都必须有一个构造函数。构造函数参数是可选的，并表示合约的名称。如果未传递，将使用类名。我们建议您传递一个唯一的名称，并将其考虑为命名空间，类似于反向域名结构。

交易函数

一个初始化智能合约的交易函数可以在客户端请求之前创建和调用。您可以使用此功能设置和执行您的智能合约以及任何所需的资源。这些资源可以是用于查找、翻译、解码、验证、丰富、安全等用途的数据表或地图。

世界状态

我们可以以多种方式查询世界状态。*简单查询*是一个键查找，*范围查询*获取一个集合。还有一种称为*丰富查询*。我们在第五章中查看世界状态。

`putState`

要将数据写入分类帐，我们使用`putState`函数。它的参数是`key`和`value`。`value`是一个字节数组，因此分类帐可以存储任何数据。通常，我们将存储事务前的转换为字节数组的业务对象的等价物，然后将其作为`value`参数传递。

`ChaincodeStub`

`ChaincodeStub`类包含用于与分类帐和世界状态交互的几个函数。所有智能合约都会得到该类的一个实现，作为包含和公开由称为`ctx`的`Context`类实现所包含的`stub`对象，所有事务函数都将其作为第一个参数接收。

读/写事务

智能合约中的更新分为三个步骤执行：读取事务、对从读取事务返回的内存数据进行更新，然后进行写入事务。这为密钥创建了一个新的世界状态，同时保持了密钥在不可变的基于文件的分类帐中的历史。

这一点很重要记住：*你不能在同一个事务中更新（或写入）分类帐并读取你在同一事务中写入的内容*。不管你从事务函数中调用多少其他事务函数，都需要考虑事务请求的数据流。客户端向对等方提交事务请求，对等方支持请求事务（这是智能合约执行的地方），具有读取和写入集的认可发送回客户端；经认可的请求发送到排序器，排序器对事务进行排序并创建区块。排序器将排序后的请求发送给提交对等方，在将写入提交到分类帐并更新世界状态之前验证读取和写入集。

在最简单的形式中，智能合约是围绕着`ChaincodeStub`的封装，因为智能合约必须使用通过这个类暴露的接口与账本和世界状态进行交互。这是一个重要的要点需要记住。你应该考虑以模块化的设计来实现业务逻辑，将你的`Contract`子类视为数据源。这样做有助于随着时间的推移演进代码并将逻辑分区成可以共享和重用的功能组件。在第五章中，我们将在打包和部署的上下文中探讨设计，在第六章中，我们深入探讨模块化设计和实现以促进维护和测试。

多个对等节点，即背书对等节点，将执行您的智能合约。今天的架构将智能合约放置在一个网关后面，该网关是智能合约 SDK 中的中间件。网关接收智能合约请求，处理它们，并将它们发送到一个或多个对等节点。对等节点实例化链码以执行。

## SDK

Fabric 提供了用于开发智能合约的 Go、Java 和 Node.js（JavaScript）实现的 SDK。我们对 Node.js 的 Hyperledger Fabric 智能合约开发 SDK 感兴趣，它被称为*fabric-chaincode-node*。虽然你在智能合约开发中不需要下载它，但你可以从[GitHub](https://github.com/hyperledger/fabric-chaincode-node)下载或克隆*fabric-chaincode-node*。

*fabric-chaincode-node* SDK 有很多功能。我们对一些对于开发智能合约至关重要的组件感兴趣。其余的文件是低级接口、支持工件、工具等，是用于使用 Node.js 实现`Contract`接口所需的更多内容。这个 SDK 通过提供高级 API 来帮助像我们这样的开发者，这样我们就可以快速学习并专注于我们的智能合约业务逻辑和设计。

我们感兴趣的第一个 API 是 *fabric-contract-api*。它位于 *fabric-chaincode-node* 的 *apis* 子目录下。另一个 API *fabric-shim-api* 是 *fabric-shim* 库的类型定义和纯接口，我们稍后在本章中会看到。

当我们启动智能合约项目并执行 `npm install` 时，npm 会从 npm 公共存储库中下载 *fabric-contract-api* 作为模块，以及 *fabric-shim*。这种下载发生是因为我们有两个明确的智能合约依赖项用于开发 Hyperledger Fabric 智能合约。这些显示在 Fabcar 智能合约的 *package.json* 文件中的摘录中：

```
"dependencies": {
    "fabric-contract-api": "².0.0",
    "fabric-shim": "².0.0"
},
```

*fabric-contract-api* 和 *fabric-shim* 是我们开发智能合约所需的唯一模块。*fabric-contract-api* 包含实现 `Contract` 和 `Context` 类的 *contract.js* 和 *context.js* 文件。

### 合约类

`Contract` 是一个简单的类。除构造函数外，还有一些实用函数，您可以重写这些函数以在事务之前和之后实现逻辑：

```
constructor(name) {
    this.__isContract = true;
    if (typeof name === 'undefined' || name === null) {
        this.name = this.constructor.name;
    } else {
        this.name = name.trim();
    }
    logger.info('Creating new Contract', name);
}
```

在调用任何合约事务函数之前都会调用 `beforeTransaction` 函数。您可以重写此方法以实现自己的定制逻辑：

```
async beforeTransaction(ctx) {
// default implementation is do nothing
}
```

在调用任何合约事务函数之后都会调用 `afterTransaction` 函数。您可以重写此方法以实现自己的定制逻辑：

```
async afterTransaction(ctx, result) {
    // default implementation is do nothing
}
```

`getName` 函数是一个 getter，返回合约名称：

```
getName() {
    return this.name;
}
```

`createContext` 函数创建一个自定义事务上下文：

```
createContext() {
    return new Context();
}
```

### 事务上下文

您可以创建一个自定义事务上下文来存储您自己的对象，这些对象可以通过所有事务函数的第一个参数 `ctx` 对象来访问。这里是创建自定义上下文的一个示例：

```
const AssetList = require('./assetlist.js');

class MyContext extends Context {
    constructor() {
        super();
        this.assetList = new AssetList(this);
    }

}

class AssetContract extends Contract {
    constructor() {
        super('org.my.asset');
    }

    createContext() {
        return new MyContext();
    }
}
```

使用自定义上下文 `MyContext`，事务可以通过 *ctx.assetList* 访问 *assetList*。

正如你所见，创建一个简单而智能的合约很容易。你需要从*fabric-contract-api*中导入`Contract`并对其进行扩展。然后创建一个无参数的构造函数并导出我们的合约。就是这样。

### 上下文类

好的，这就是 `Contract` 类，但 `Context` 类呢？你刚学会了如何创建自定义事务上下文，但 `Context` 类包含了什么？正如你所学的，每个事务函数都会获得一个名为 `ctx` 的 `Context` 对象作为其第一个参数。这就是事务上下文。它包含两个重要对象：`stub` 和 `clientIdentity`。`stub` 是 `ChaincodeStub` 类的实现，而 `clientIdentity` 是 `ClientIdentity` 类的实现。我们接下来会讨论这些类。

`ChaincodeStub` 拥有我们与分类账和世界状态交互所需的所有函数。它是我们与分类账和世界状态交互的 API。它包含在 *lib* 目录下的 *fabric-shim* 模块中，并在 *stub.js* 文件中实现。其两个主要函数是 `getState` 和 `putState`。还提供了几个其他函数。大多数可以分为以下几类：

+   与状态相关

+   查询相关

+   事务相关

+   与私有数据相关

这四个组代表了大部分功能。*与状态相关的函数*用于从分类账中读取和写入数据。它们使用或涉及使用密钥。

*查询相关的函数*有两个丰富的查询函数，其中一个包含分页功能。*丰富查询*是数据库原生的字符串查询。要使用丰富查询，您需要在数据库中使用 CouchDB。我们将在第五章中进行这样的操作，届时您将学习如何调用智能合约。另一个独特的查询函数是 `getHistoryForKey`，它接受一个键并返回其历史记录。这可用于审计更改并找到失败的交易。

Hyperledger 有五个*与事务相关的函数*：

+   `getTxID(): *string*;`

+   `getChannelID(): *string*;`

+   `getCreator(): SerializedIdentity;`

+   `getMspID(): *string*;`

+   `getTransient(): Map<*string*, *Uint8Array*>;`

使用 `getTxID` 来检索交易 ID，`getChannelID` 来获取通道 ID，`getCreator` 来获取客户端，`getMspID` 来获取客户端所属的组织，以及 `getTransient` 来获取私有数据。在接下来的两个章节中，我们将执行每一个。

Hyperledger 有九个 *私有数据相关的函数*：

+   `getPrivateData(collection: *string*, key: *string*): Promise<*Uint8Array*>;`

+   `getPrivateDataHash(collection: *string*, key: *string*): Promise<*Uint8Array*>;`

+   `putPrivateData(collection: *string*, key: *string*, value: *Uint8Array*): Promise<void>;`

+   `deletePrivateData(collection: string, key: string): Promise<void>;`

+   `setPrivateDataValidationParameter(collection: *string*, key: *string*, ep: *Uint8Array*): Promise<void>;`

+   `getPrivateDataValidationParameter(collection: *string*, key: *string*): Promise<*Uint8Array*>;`

+   `getPrivateDataByRange(collection: *string*, startKey: *string*, endKey: *string*): Promise<Iterators.StateQueryIterator> & AsyncIterable<Iterators.KV>;`

+   `getPrivateDataByPartialCompositeKey(collection: *string*, objectType: *string*, attributes: *string[]*): Promise<Iterators.StateQueryIterator> & AsyncIterable<Iterators.KV>;`

+   `getPrivateDataQueryResult(collection: *string*, query: *string*): Promise<Iterators.StateQueryIterator> & AsyncIterable<Iterators.KV>;`

这九个私有数据函数提供了读取和写入私有数据集合的能力，获取私有数据哈希，从私有数据中删除，设置和获取私有数据验证的背书策略，通过范围或部分复合键获取私有数据，以及通过丰富的查询。当我们在智能合约交易中使用私有数据时，我们将在第五章和第六章执行其中一些。

现在，您已经对我们从`ctx`对象中获取的`stub`对象可以提供什么样的功能有了一个很好的了解，让我们看一看事务上下文中的另一个对象`ClientIdentity`。

事务上下文中包含的`clientIdentity`对象，即`ctx.clientIdentity`，是`ClientIdentity`类的实现，它是一个仅具有五个函数的小类：

+   `assertAttributeValue(attrName: *string*, attrValue: *string*): boolean;`

+   `getAttributeValue(attrName: *string*): string | null;`

+   `getID(): *string*;`

+   `getIDBytes(): *Uint8Array*;`

+   `getMSPID(): *string*;`

`assertAttributeValue`和`getAttributeValue`函数作用于客户端证书。使用这些函数，可以通过使用证书属性值实现细粒度安全。`getID`和`getIDBytes`函数检索客户端的身份，`getMSPID`用于获取客户端所属的组织。使用这些函数，您可以实现各种身份验证和授权设计模式。

### 事务函数

*事务函数*是客户端调用的智能合约函数。这些是您在智能合约中设计和实现的业务函数。以下是来自 Fabcar 智能合约的三个事务函数的示例。我们将在“定义智能合约”中定义它们：

```
async queryCar(*ctx*, *carNumber*) 
async createCar(*ctx*, *carNumber*, *make*, *model*, *color*, *owner*)
async queryAllCars(*ctx*)
```

所有事务函数都将事务上下文`ctx`对象作为第一个参数。事务函数使用此对象来引用`stub`和`clientIdentity`对象，例如`ctx.stub`和`ctx.clientIdentity`。`stub`是`ChaincodeStub`的一个实例。`clientIdentity`是`ClientIdentity`的实现，并公开用于获取事务 ID、客户端 ID、任何客户端属性和组织 ID 的函数。这些函数可用于应用程序和事务特定的身份验证和授权。

大多数交易函数包含对总账或世界状态的调用是很常见的。`stub`提供了从世界状态读取和写入总账的函数，从而更新世界状态。

您设计交易函数的方式完全由您控制。您可以将它们分组、混合、创建库等等。请记住，对于写入的交易，所有指定的背书节点都必须执行您的智能合约。

背书策略决定了交易是否被提交。例如，一个背书策略可能规定四个节点中有三个节点必须对交易进行背书。如果由于某种原因，少于三个节点可以对交易进行背书，那么交易将不会被提交，这意味着数据将不会在总账上可用。

需要记住的一点是，即使写入事务可能失败，它也将被标记为无效并写入总账。无效的交易不会成为世界状态的一部分。

作为最佳实践，Fabric 智能合约要求确定性代码。许多节点需要执行代码，并且它们都需要得出相同的结果。因此，输入必须始终返回相同的结果。无论哪个节点执行代码，都不应该有关系。给定相同的输入，节点应该返回相同的结果。无论代码执行多少次，这都应该发生。

代码应该有一个开始和一个结束。它永远不应该依赖于动态数据或长时间的随机执行。代码应该快速有效，具有清晰的逻辑流程，而不是循环的。例如：

```
async CreateAsset(*ctx*, *id*, *amount*, *owner*) {
        const asset = {
            ID: id,
            Amount: *amount*,
            Owner: *owner*
        };
        return ctx.stub.putState(id,Buffer.from(
           JSON.stringify(asset)));
}
```

创建资产时，我们将期望资产 ID、数量和所有者作为输入。

### 验证和清理参数

交易必须验证和清理其参数。这不是智能合约独有的。如果您想确保智能合约的完整性和可用性，这是一个明智的默认做法。

使用已知的技术验证您的参数并防止可能损害智能合约的任何数据。您还希望清理您的参数并确保您期望的数据的质量。您希望限制不必要的数据处理，在您的逻辑中稍后可能会导致失败或未涵盖的边缘情况。以下是一个检查函数是否为 `Process` 的示例；如果不是，则会引发异常：

```
func (c *Asset) Invoke(stub shim.ChaincodeStubInterface) pb.Response {
    function, args := stub.GetFunctionAndParameters()
    if function == "Process" {
        return c.Process(stub, args)
    } 
    return shim.Error("Invalid function name")
}
```

### 简单的状态交互（获取、放置、删除）

Fabric 智能合约在核心上是随着时间演变的状态机，保留了所有先前状态的不可变历史记录。您将使用的三个主要 `stub` 函数如下：

```
getState(key: *string*): Promise<*Uint8Array*>;
putState(key: *string*, value: *Uint8Array*): Promise<void>;
deleteState(key: *string*): Promise<void>;
```

`stub` 函数提供了智能合约读取世界状态、写入账本和从世界状态删除的功能。

账本和世界状态是键值数据存储。这使得它简单易用，但允许在账本上存储丰富的数据，并由世界状态、文档或 NoSQL 数据库查询和查看。目前支持 LevelDB 和 CouchDB。LevelDB 是一个简单的键值数据存储，而 CouchDB 是一个丰富且强大的 NoSQL 文档数据库。这意味着您可以将简单到复杂的 JSON 数据结构写入账本并查询世界状态数据库以获取丰富的数据。有几个函数可用于查询。

## 创建和执行查询

在处理交易时，智能合约通常需要查找或查询世界状态中的数据。还记得我们的 Fabcar 示例智能合约的更新吗？要执行更新，智能合约通常必须找到并加载要更新的现有对象。然后它会更新内存中的数据并将更新后的数据写入账本——记住使用 `putState` 写入和 `getState` 读取。

与关系数据库不同，我们可以在不先选择行的情况下更新字段，但是在 Fabric 智能合约中，我们必须加载键的值并更新该值。 这可能是非常大且复杂的 JSON 数据结构中的一个字段，也可能是一个带有一个字段的简单对象，该字段是我们正在更新的字段。 为什么这样？ 因为所有数据都与唯一键绑定。 如果键的关联值是一个具有四个字段的对象，我们将每个字段视为一个值，但对于分类帐来说，它们仅是一个由单个唯一键标识的值对象。

这里是你可以用来查找数据的可用`stub`函数：

+   `getState(key: *string*): Promise<*Uint8Array*>;`

+   `getStateByRange(startKey: *string*, endKey: *string*): Promise<Iterators.StateQueryIterator> & AsyncIterable<Iterators.KV>;`

+   `getStateByRangeWithPagination(startKey: *string*, endKey: *string*, pageSize: *number*, bookmark?: *string*): Promise<StateQueryResponse<Iterators.StateQueryIterator>> & AsyncIterable<Iterators.KV>;`

+   `getQueryResult(query: *string*): Promise<Iterators.StateQueryIterator> & AsyncIterable<Iterators.KV>;`

+   `getQueryResultWithPagination(query: *string*, pageSize: *number*, bookmark?: *string*): Promise<StateQueryResponse<Iterators.StateQueryIterator>> & AsyncIterable<Iterators.KV>;`

+   `getHistoryForKey(key: *string*): Promise<Iterators.HistoryQueryIterator> & AsyncIterable<Iterators.KeyModification>;`

当我们在智能合约中使用它们并从客户端调用它们时，我们会在第五章讨论这些内容。

# 定义智能合约

让我们从简单的 Fabcar 智能合约开始。在 *fabric-samples* 目录中，找到 *chaincode* 目录。在 *chaincode* 目录中，找到 *fabcar* 目录。在 *fabcar* 目录中，找到 *javascript* 目录。在你的 shell 中切换到此目录并执行以下命令：

```
$ npm install
```

这将创建 *node_modules* 目录，并安装 *package.json* 中定义的依赖模块。我们这样做是因为我们依赖于 *fabric-contract-api* 和 *fabric-shim* 模块。这两个模块是我们在 JavaScript 中开发 Fabric 智能合约时使用的。我们将在检查 Fabcar 智能合约后查看这些内容。

现在让我们来查看 Fabcar 智能合约。这个简单的智能合约是学习 Fabric 智能合约开发的一个很好的例子，因为它包含了形成更高级智能合约基础的必要细节。它位于当前目录中的 *lib* 目录中，应该是 *fabric-samples/chaincode/fabcar/javascript* 目录。在您喜欢的编辑器中打开 *fabcar.js*；示例 4-1 显示了源代码。

##### 示例 4-1\. fabcar.js

```
/*
 * Copyright IBM Corp. All Rights Reserved.
 *
 * SPDX-License-Identifier: Apache-2.0
 */
'use strict';
const { Contract } = require('fabric-contract-api');<1>
class FabCar extends Contract {<2>
    async initLedger(ctx) {<3>
        console.info('============= START : Initialize Ledger ===========');

        const cars = [<4>
            {
                color: 'blue',
                make: 'Toyota',
                model: 'Prius',
                owner: 'Tomoko',
            },
...
        ];
        for (let i = 0; i < cars.length; i++) {<5>
            cars[i].docType = 'car';
            await ctx.stub.putState('CAR' + i, 
            Buffer.from(JSON.stringify(cars[i])));<6>
        }
    }
    async queryCar(ctx, carNumber) {<7>
        const carAsBytes = await ctx.stub.getState(
        carNumber); // get the car from chaincode state<8>
        if (!carAsBytes || carAsBytes.length === 0) {
            throw new Error(`${carNumber} does not exist`);
        return carAsBytes.toString();
    }
    async createCar(ctx, carNumber, make, model, color, owner) {<9>
        console.info('============= START : Create Car ===========');
        const car = {color, docType: 'car',make, model, owner}

        await ctx.stub.putState(carNumber, Buffer.from(
        JSON.stringify(car)));<10>
    }
    async queryAllCars(ctx) {<11>
        const startKey = '';
        const endKey = '';
        const allResults = [];
        for await (const {key, value} of ctx.stub.getStateByRange(
            startKey, endKey)) {<12>
            const strValue = Buffer.from(value).toString('utf8');

            let record;
            try {
                record = JSON.parse(strValue);
            } catch (err) {
                record = strValue;
            }
            allResults.push({ Key: key, Record: record });
        }
        return JSON.stringify(allResults);
    }
    async changeCarOwner(ctx, carNumber, newOwner) {<13>

const carAsBytes = await ctx.stub.getState(carNumber);<14>
if (!carAsBytes || carAsBytes.length === 0) {
            throw new Error(`${carNumber} does not exist`);
        }
        const car = JSON.parse(carAsBytes.toString());
        car.owner = newOwner;
        await ctx.stub.putState(carNumber, Buffer.from(
JSON.stringify(car)));<15>
    }
}
module.exports = FabCar;<16>
```

(1) 我们首先导入 *fabric-contract-api* 模块。

(2) 所有 Fabric 智能合约都扩展自 `Contract` 类。我们从第 1 行导入的 *fabric-contract-api* 模块中获取 `Contract` 类。

(3) 智能合约可以使用交易在处理客户端应用程序请求之前对其进行初始化。这行是初始化智能合约的函数的开头。所有智能合约函数按照约定都接收一个称为 `ctx` 的交易上下文对象作为参数。

(4) 在这个例子中，`initLedger` 函数正在创建一个名为 `cars` 的对象数组。每个数组对象包含键值对。您可以将对象数组视为资产的记录，将对象键值对视为字段。此函数有效地预加载了一个包含 `car` 对象的数组，以便在智能合约中执行交易函数。

(5) 接下来，`initLedger` 函数正在遍历 `car` 资产对象的数组，并向每个对象添加一个名为 `docType` 的字段，并为每个对象赋予字符串值 `car`。

（6）这一行是第一次使用传递给所有`Contract`类事务函数的第一个函数参数 `ctx` 对象（`Context` 类）。`ctx` 对象包含 `stub` 对象，它是 `ChaincodeStub` 类。`ChaincodeStub` 类实现了一个 API 来访问账本。这一行调用了 `putState` 函数，将键和值写入账本和世界状态。

###### 注意

Hyperledger Fabric 实现了两个组件的区块链账本：一个基于文件的组件和一个数据库组件。*基于文件的组件*是实现账本的底层不可变数据结构，*数据库组件*则暴露了基于文件的账本的当前状态。数据库组件被称为*世界状态*，因为它代表了账本的当前状态。基于文件的组件维护着永久不变的账本。*fabric-contact-api* 访问世界状态。更低级别的 API 访问基于文件的账本。

（7）接下来是第一个事务函数。如前所述，所有智能合约事务函数的第一个参数是表示事务上下文的 `ctx` 对象，它是一个 `Context` 类。任何其他参数都是可选的。

(8) `queryCars` 函数是一个读事务。使用 `ctx` 对象，它调用 `stub` 的 `getState` 函数，该函数将从世界状态——即数据库中读取数据。`stub` 是 `ChaincodeStub` 类的实现，我们稍后会介绍。对于这个函数，被称为 `carNumber` 的参数是传递给 `getState` 函数的 `key`，该函数将在世界状态数据库中搜索 `key` 并返回与其关联的值。函数的其余部分检查是否返回了数据，如果是，则将返回的字节数组转换为字符串，并返回表示存储在世界状态中的键值的字符串。请记住，世界状态是永久不变的基于文件的分类帐的当前状态的表示，用于存储在分类帐中的任何键值对。虽然数据库可能是可变的，但基于文件的分类帐不是。因此，即使从数据库或世界状态中删除了键值对，该键值对仍然存在于基于文件的分类帐中，其中所有历史记录都在永久不变的分类帐中维护。

(9) 接下来是第二个事务函数。它传递了创建新的 `car` 记录对象所需的值，我们将将其添加到分类帐中。

(10) 使用从函数参数构建的 `car` 记录对象，我们调用由 `stub` 实现的 `ChaincodeStub` API 函数，称为 `putState`，它将 `key` 和 `value` 写入分类帐并更新当前的世界状态。传递给 `putState` 函数的前两个参数分别是键和值。我们需要将 `value`——即 `car` 记录对象转换为字节数组，这是 `ChaincodeStub` API 所要求的。

(11) 下一个交易函数名为`queryAllCars`，是一个读取交易，并演示了一个范围查询。与所有查询一样，范围查询由接收到请求的对等方执行。范围查询需要两个参数：起始键和结束键。这两个键代表范围的起始和结束。所有落入范围内的键以及它们的关联值都会返回。你可以为两个键都传递空字符串以检索所有键和值。

(12) 执行一个`for`循环，该循环将从`ChaincodeStub` API 函数`getStateByRange`返回的所有键和关联值存储起来。

(13) 最后一个交易函数`changeCarOwner`结合了读取和写入任务来更改世界状态。这里的业务逻辑是所有权的转移。除了`ctx`参数之外，还传递了两个参数：一个名为`carNumber`的`key`和一个名为`newOwner`的`value`对象。

(14) 接下来，我们需要从世界状态中检索记录对象，该对象表示此记录的当前键和值。`key`是`carNumber`。我们使用它来执行`ChaincodeStub` API 的`getState`，将其传递给`key`。一旦我们检索到`carNumber`的当前`car`记录对象，我们就将`owner`字段更改为`newOwner`。

（15）在检索表示世界状态的分类账数据并更新检索到的数据后，我们通过执行`ChaincodeStub`API`putState`更新此`car`记录对象的分类账。这将向表示世界状态的分类账写入一个新的`key`和`value`。如果现在检索`car`记录对象，分类账将不会显示新的所有者，直到记录对象提交到分类账。重要的是要理解，一旦提交，分类账就会被追加，数据库状态将会改变（世界状态将会更新）。你可以把分类账想象成一个不断增长的对象堆栈，每个对象都有一个称为*key*的唯一标识符。可以有许多具有相同值的键，但只有一个表示当前或世界状态。这是数据库实现世界状态视图的方式，而基于文件的分类账实现了所有键的不可变历史按时间戳顺序。

###### 注意

基于文件的分类账存储所有写入交易。成功和失败的写入交易都是基于文件的不可变分类账的一部分。标志控制存储在不可变文件分类账中的交易的有效性。这有助于审计所有提交的写入交易。

（16）这一行是特定于 Node.js 的。当我们讨论智能合约执行时，包括项目结构、打包和部署时，我们将在第五章中讨论导出智能合约模块。

这完成了这个简单的智能合约。我们现在将简要讨论它，以指出开发智能合约的基本要求。从这个基本的智能合约开始，可以设计和开发复杂的智能合约应用。

## 使用键值对定义资产

当设计智能合约时，您可能需要考虑资产的问题。*资产*是通用的，可以代表许多事物，包括有形和无形物体。它们可以是机器零件、狗食、货币或绿色衍生品。我们使用名称-值对或键-值对来创建我们的数据结构，这取决于您如何想要思考它。下面是一个我们可以讨论的示例：

```
const assets = [
    {
        color: 'blue',
        make: 'Honda',
        model: 'Accord',
        owner: 'Jones',
    },  
    {
        color: 'red',
        make: 'Ford',
        model: 'Mustang',
        owner: 'Smith',
    },
];
for (let i = 0; i < assets.length; i++) { 
    assets[i].docType = 'asset';
    await ctx.stub.putState('ASSET' + i,     Buffer.from(JSON.stringify(assets[i])));
}
```

我们之前在 Fabcar 示例中见过这个。这是一个基本处理的好例子，可以根据您独特的用例进行进阶。此示例创建了一个代表资产的对象数组。键-值对定义了每个资产的属性或特征。该数组充当资产的简单数据库。每个资产通过调用`ctx.stub.putState`写入分类帐，该方法接受键和值。值必须是字节数组，因此我们将 JSON 对象转换为字符串，然后将字符串转换为字节数组。您将经常执行此操作，并可能希望简化它并开始构建实用程序或库。此特定代码用于初始化智能合约。

我们还可以通过智能合约交易定义资产。接下来展示的`createAsset`交易函数说明了创建资产并将其写入分类帐是多么简单。这个函数将由客户端调用。客户端可以是用户或进程。重要的是要记住，在交易提交到分类帐之前，资产是不可用的。因此，你不能在分类帐上写入大量资产，并期望在智能合约中读取和使用它们的数据来继续处理。在开始设计和头脑风暴时，这种断开的状态是需要考虑的事情。这是`createAsset`交易函数：

```
async createAsset(ctx, assetNumber, make, model, color, owner) {
        const asset = {
        color,
        docType: 'asset',
        make,
        model,
        owner,
        };
    await  ctx.stub.putState(assetNumber,Buffer.from(JSON.stringify(asset)));
}
```

## 收集私有数据

*私有数据集合*（*PDC*）是属于一个组织的分类账数据的一部分，它存储私有数据，并将数据与通道上的其他组织保持私密。这包括私有数据和私有数据的哈希值。第九章提供了更多细节。需要保持特定数据私密对于开发智能合约非常重要。许多智能合约需要符合隐私和安全要求。Fabric 支持用于交易函数和智能合约的私有数据。

私有数据可以共享或保持隔离和安全。我们可以在创建了一定数量的区块或按需时使私有数据过期。放入 PDC 的数据与公共数据保持分离，并且 PDC 是本地和受保护的。可以通过哈希和公钥将世界状态与 PDC 结合使用。

表 4-1 列出了可从`stub`中使用的几个函数。

Table 4-1\. 用于处理私有数据的命令

| API | 注释 |
| --- | --- |

|

```
getPrivateData(collection: *string*, key: *string*): Promise<*Uint8Array*>
```

| 从集合名称和指定的键返回认可策略。 |
| --- |
| `putPrivateData(collection: `*string*`, key: `*string*`, value: `*Uint8Array*`): Promise<void>` | 将集合名称、指定的键和值放入交易的私有`writeSet`中。 |
| `deletePrivateData(collection: `*string*`, key: `*string*`): Promise<void>` | 通过提供集合名称和私有数据变量键删除认可策略。 |
| `setPrivateDataValidationParameter(collection: `*string*`, key: `*string*`, ep: `*Uint8Array*`): Promise<void>` | 通过提供集合名称和私有数据变量键设置认可策略。 |
| `getPrivateDataValidationParameter(collection: `*string*`, key: `*string*`): Promise<Uint8Array>` | 通过提供集合名称和私有数据变量键返回认可策略。 |
| `getPrivateDataByRange(collection: `*string*`, startKey: `*string*`, endKey: `*string*`): Promise<Iterators.StateQueryIterator> & AsyncIterable<Iterators.KV>` | 通过集合名称和私有数据变量键返回认可策略。 |
| `getPrivateDataByPartialCompositeKey(collection: `*string*`, objectType: `*string*`, attributes: string[]): Promise<Iterators.StateQueryIterator> & AsyncIterable<Iterators.KV>` | 查询给定集合名称和给定部分复合键的认可策略。 |
| `getPrivateDataQueryResult(collection: `*string*`, query: `*string*`): Promise<Iterators.StateQueryIterator> & AsyncIterable<Iterators.KV>` | 对给定私有集合执行丰富的查询。支持可以运行丰富查询的状态数据库（例如，CouchDB）。 |

使用私有数据可能会有些棘手，并且存在用于在不同情况下使用它的模式。我们将在第五章中涵盖大多数这些功能，当我们实现私有数据函数以调用时，并且在第六章中再次使用它们进行维护和测试。

## 设置基于属性的访问控制

最终，您将需要一种实现细粒度认证和授权的方式。客户端具有控制访问的身份。这些身份必须属于授权组织，组织属于托管链码的通道。证书代表客户端的身份。证书支持可以用来实现交易和智能合约级别的认证控制和授权策略的属性。

您可以从事务上下文中包含的`clientIdentity`对象中访问此信息。该对象有两个与属性值相关的函数：

```
assertAttributeValue(attrName: *string*, attrValue: *string*): *boolean*;
getAttributeValue(attrName: *string*): *string* | null;
```

使用 `assertAttributeValue` 检查属性是否存在，并使用 `getAttributeValue` 检索特定属性。在检索之前断言属性是一个好习惯。在第五章和第六章中，我们将利用属性进行安全和其他目的。

## 初始化账本状态

账本的初始化通常是一个必需的任务。我们之前看过的 Fabcar 代码示例清楚地说明了如何初始化智能合约状态。你将在提交后立即初始化它。之后，你可以开始提交交易并通过调用智能合约方法查询账本数据。

创建一个函数，用于执行初始化；在这里，它被称为 `initLedger`。在 `initLedger` 函数中，你可以执行初始化所需的操作。在这个例子中，我们创建一个业务对象数组，遍历 `cars` 数组，然后为 `cars` 数组中的每个 `car` 对象添加一个额外的属性 `docType`。下面是 `initLedger` 的逻辑：

```
async initLedger(ctx) {
    const cars = [
         {
              color: 'blue',
              make: 'Toyota',
              model: 'Prius',
              owner: 'Tomoko',
         },
         .
         .
         .
         {
              color: 'brown',
              make: 'Holden',
              model: 'Barina',
              owner: 'Shotaro',
              },
    ];
    for (let i = 0; i < cars.length; i++) {
              cars[i].docType = 'car';
              await ctx.stub.putState('CAR' + i,
              Buffer.from(JSON.stringify(cars[i])));
              console.info('Added <--> ', cars[i]);
    }
}
```

`initLedger` 函数使用 `putState` 函数将数组对象写入账本。要执行 `initLedger` 函数，我们需要调用智能合约。我们可以使用对等命令行接口（CLI）的 `invoke` 命令。让我们看看如何通过 `invoke` 命令调用 `initLedger`。

### 链码调用初始化

要在我们的智能合约上执行事务函数，我们可以使用 *peer* 二进制提供的 `invoke` 命令。该二进制提供了许多命令，其中几个你将在第五章和第六章学到。这里我们用它来调用我们的 `initLedger` 函数：

###### 注意

我们将以下命令打印在多行上以增强可读性。当你输入命令时，它必须在一行上，否则将无法执行。

```
peer chaincode invoke 
-o localhost:7050 
--ordererTLSHostnameOverride orderer.example.com 
--tls true 
--cafile /OReilly/fabric-samples/test-network/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tls
ca.example.com-cert.pem 
-C mychannel 
-n fabcar 
--peerAddresses localhost:7051 
--tlsRootCertFiles /OReilly/fabric-samples/test-network/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt 
--isInit 
-c '{"function":"initLedger","Args":[]}'

[chaincodeCmd] chaincodeInvokeOrQuery -> INFO 001 Chaincode invoke successful. result: status:200
```

`invoke`命令执行紧随`-c`命令参数标志的命令对象。命令对象指定要执行的函数以及任何函数参数。在这里，我们正在执行`initLedger`函数，没有函数参数。

我们可以测试`initLedger`函数的结果。我们期望返回写入账本的数组内容。我们将使用`query`命令；让我们看看如何查询账本数据。

### 链码查询

使用 peer 的`query`命令，我们可以执行我们的智能合约查询函数之一。在这种情况下，我们设置`-c`命令标志以执行`queryAllCars`：

```
peer chaincode query 
-C mychannel 
-n fabcar 
-c '{"Args":["queryAllCars"]}'
```

这是返回输出：

```
[{"Key":"CAR0","Record":{"color":"blue","docType":"car","make":"Toyota","model":"Prius","owner":"Tomoko"}},
.
.
.
{"Key":"CAR9","Record":{"color":"brown","docType":"car","make":"Holden","model":"Barina","owner":"Shotaro"}}]
```

结果显示`initLedger`函数已执行，并且我们的智能合约已初始化。

# 安装和实例化智能合约

为了准备第五章，让我们看看在编写智能合约完成后我们需要做什么。本节讨论了我们需要执行的几个步骤，以便达到可以从命令行或智能合约客户端调用我们的智能合约的程度。这些步骤如下：

1.  打包链码。

1.  安装链码。

1.  查询安装情况。

1.  批准该包。

1.  检查提交准备情况。

1.  提交链码定义，

1.  查询链码是否提交。

1.  初始化合约。

1.  执行查询。

第五章详细介绍了这些步骤。它们包含示例命令行代码，有些还有输出。可以在[Hyperledger Fabric 文档](https://hyperledger-fabric.readthedocs.io/en/latest/commands/peerlifecycle.html)中参考以下`peer`命令。

## 打包链码

我们需要做的第一件事就是打包我们的代码。正如您从以下命令中看到的那样，我们使用`peer` CLI 来执行此步骤和所有剩余步骤。

为了准备我们的智能合约，我们使用以下`peer`打包命令：

```
peer lifecycle chaincode package fabcar.tar.gz \ 
        --path ../chaincode/fabcar/javascript/ \
        --lang node \
        --label fabcar_1
```

一旦此命令完成，我们就会得到一个包含智能合约的*tar.gz*文件。接下来，我们需要安装此包。

## 安装链码

在打包智能合约之后，我们可以安装它。如果有几个组织在协作，那么没有必要让所有组织单独打包智能合约。一个智能合约包可以被所有组织使用。一旦组织收到包，它就会被安装在它们的背书节点上。第九章中详细介绍了这一点。

这是安装命令，显示成功输出消息：

```
peer lifecycle chaincode install fabcar.tar.gz

[cli.lifecycle.chaincode] submitInstallProposal -> INFO 001 Installed
```

一旦合同安装完成，您可能希望进行验证。

## 查询安装情况

您可以执行以下命令来获取最新安装的链码的详细信息：

```
peer lifecycle chaincode queryinstalled

Installed chaincodes on peer:
Package ID: fabcar_1:5a00a40697…330bf5de39, 
Label: fabcar_1
```

您可能会收到许多包标识符，这取决于已安装的包数量。如果您需要自动化依赖特定包是否已安装或未安装的任务，则可以使用脚本来过滤输出。一旦安装了链码包，就必须对其进行批准。

## 批准包

安装包后，组织必须批准才能提交和访问。此命令具有许多参数。对我们而言最感兴趣的是`–package-id`。我们可以从前面的`queryinstalled`命令的输出中获取它。`package-id`用作链码安装包的标识符：

```
peer lifecycle chaincode approveformyorg 
-o localhost:7050 
--ordererTLSHostnameOverride orderer.example.com 
--tls true 
--cafile /OReilly/fabric-samples/test-network/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.
example.com-cert.pem 
--channelID mychannel 
--name fabcar 
--version 1 
--init-required 
--package-id fabcar_1:5a00a406972168ac5856857b5867f51d5244208b876206b7e0e418330bf5de39 
--sequence 1
```

一旦批准命令完成，我们就可以确定是否可以提交。我们使用`checkcommitreadiness`命令。

## 检查提交就绪性

在提交链码包之前，必须有一些组织批准它。 数量取决于政策，该政策可能要求所有组织或一些组织的批准。 理想情况下，您希望所有组织都同意。 我们可以使用 `checkcommitreadiness` 命令来确定是否可以提交该包。 在这种情况下，我们不能，因为 `Org2` 还没有批准。 一旦批准，此命令将对 `Org1` 和 `Org2` 显示 `true`：

```
peer lifecycle chaincode checkcommitreadiness 
--channelID mychannel 
--name fabcar 
--version 1 
--sequence 1 
--output json 
--init-required

{
    "approvals": {
        "Org1MSP": true,
        "Org2MSP": false
    }
}
```

在 Hyperledger 配置中，我们可以定义不同类型的生命周期背书政策。 默认为 `MAJORITY Endorsement`。 这要求大多数同行支持链码事务以在通道中进行验证和执行，并将事务提交到分类账中。第九章对此进行了更详细的介绍。 一旦所有批准都为真，我们就可以提交链码包。

## 提交链码定义

一旦所有组织或组织的子集已获得批准以满足提到的政策，链码就可以提交到分类账中。 要提交链码，我们使用如下的 commit 命令：

```
peer lifecycle chaincode commit 
-o localhost:7050 
--ordererTLSHostnameOverride orderer.example.com 
--tls true 
--cafile /OReilly/fabric-samples/test-network/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.
example.com-cert.pem 
--channelID mychannel 
--name fabcar 
--peerAddresses localhost:7051 
--tlsRootCertFiles /OReilly/fabric-samples/test-network/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
--version 1 
--sequence 1
--init-required
```

在运行命令后，以下是输出结果：

```
[chaincodeCmd] ClientWait -> INFO 001 txid
[ef59101c320469be3242daa9ebe262771fc8cc8bd5cd0854c6424e1d2a0c61c2] committed with status (VALID) at
localhost:9051
```

接下来，我们可以使用 `querycommitted` 检查链码是否已提交。

## 查询链码是否已提交

在调用链码之前，必须提交链码。 要确定链码是否已提交，请使用 `querycommitted` 链码命令：

```
peer lifecycle chaincode querycommitted 
--channelID mychannel 
--name fabcar
```

输出如下：

```
Committed chaincode definition for chaincode 'fabcar' on channel 'mychannel':
Version: 1, Sequence: 1, Endorsement Plugin: escc, Validation Plugin: vscc, Approvals: [Org1MSP: true,
Org2MSP: true]
```

运行 `querycommitted` 命令会告诉我们我们的链码已准备就绪。 此链码包含一个需要初始化的智能合约。 要对其进行初始化，我们将调用它。

## 初始化合同

因为链码已经获得批准并已提交，所以我们最终可以初始化我们的智能合约。 我们可以使用 `invoke` 命令来执行智能合约事务：

```
peer chaincode invoke 
-o localhost:7050 
--ordererTLSHostnameOverride orderer.example.com 
--tls true 
--cafile /OReilly/fabric-samples/test-network/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.
example.com-cert.pem 
-C mychannel 
-n fabcar 
--peerAddresses localhost:7051 
--tlsRootCertFiles /OReilly/fabric-samples/test-
network/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt 
--peerAddresses localhost:9051 
--tlsRootCertFiles /OReilly/fabric-samples/test-network/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt 
--isInit 
-c '{"function":"initLedger","Args":[]}'
```

在执行`invoke`命令后，我们将看到以下输出；如果链码调用成功，它将返回 200 的响应状态：

```
[chaincodeCmd] chaincodeInvokeOrQuery -> INFO 001 Chaincode invoke successful. result: status:200
```

在`invoke`命令的底部，我们看到了`-c`命令标志和命令对象，其中包含了没有参数的函数键和值`initLedger`。这意味着将执行智能合约事务函数`initLedger`。输出显示成功的结果。我们的智能合约现在已初始化并准备好接受客户端。我们现在可以通过执行查询来测试我们的智能合约。

## 执行查询

我们已经完成了将您的智能合约源代码项目实例化的步骤。我们可以通过执行像这样的查询来测试它：

```
peer chaincode query 
-C mychannel 
-n fabcar 
-c '{"Args":["queryAllCars"]}'
```

在执行`queryAllCars`命令后，以下是输出：

```
[{"Key":"CAR0","Record":{"color":"blue","docType":"car","make":"Toyota","model":"Prius","owner":"Tomoko"}},
.
.
.
{"Key":"CAR9","Record":{"color":"brown","docType":"car","make":"Holden","model":"Barina","owner":"Shotaro"}}]
```

这个查询执行智能合约的事务函数，称为`queryAllCars`。写入将被提交，因此需要背书，这涉及到多个对等体。一个查询不应该要求执行超过一个对等体。这就是客户端代码为我们所做的。这个示例说明了事务函数如何封装`ChaincodeStub`函数，这种情况下是一个抽象为`queryAllCars`的`rangeQuery`。

# 总结

我们开始设置我们的超级账本 Fabric 开发环境，以准备进行第五章和第六章的操作，并使用它来探索和检查一个简单但完整的智能合约称为 Fabcar。我们编写的代码取决于 SDK 提供的 API。我们涵盖了 Fabcar 代码，因为它小而且容易学习。这使我们能够专注于智能合约的代码，使用的类和接口，以及我们依赖的超级账本智能合约 API。

Fabric 智能合约 SDK 提供了 JavaScript、Java 和 Go 的版本，更多版本正在开发中。我们使用了 Node.js 的 JavaScript Fabric 智能合约 SDK。使用它使我们能够探索 *fabric-contract-api*，以及我们开发 Fabric 智能合约所需的核心类和对象。

通过了解 API，我们介绍了如何创建智能合约以及智能合约交易函数是什么。函数执行我们的智能合约交易，因此介绍了一些重要主题，如验证和净化函数参数、初始化智能合约以及与分类账交互。Fabric 合约 API 提供了与分类账的接口，你学会了如何通过每个事务接收的交易上下文在我们的智能合约中访问它。需要涵盖的内容很多，但我们试图保持简单，同时为你提供对 *fabric-contract-api* 的了解，其中包含你需要设计和实现强大智能合约的接口。

一旦智能合约代码编写完成，我们需要将其打包并部署到 Fabric 网络。这需要完成几个步骤。我们逐步进行了每一步。了解这些步骤对于将我们的智能合约从源代码转换为已实例化的链码非常重要。我们只能执行已实例化的代码。

在第五章和第六章中，我们将使用本章学到的知识，打包和实例化我们创建的智能合约。现在我们可以继续阅读第五章，并关注智能合约的调用。
