© 作者，独家许可给 APress Media, LLC，属于 Springer Nature 2022J. T. George 介绍区块链应用[`doi.org/10.1007/978-1-4842-7480-4_6`](https://doi.org/10.1007/978-1-4842-7480-4_6)

# 6. Hyperledger Fabric

约瑟夫·塔基尔·乔治^(1  )(1)意大利罗马

公共区块链的成功，如比特币和以太坊，已经导致人们对区块链技术及其作为分布式系统在最创新的业务用例中的应用越来越感兴趣。

然而，企业的专有权利基于公共和无需许可的区块链仍然无法提供的原则和特征。

因此，私人和授权的区块链诞生了，能够满足业务妥协。

实际上，私有和授权的区块链使您能够设计系统，其中：

+   网络已经获得授权

+   参与者被确认并可识别

+   有数据隐私和保密的保证

+   交易确认延迟低

因此，有许多不同的企业使用授权的区块链项目。Hyperledger Fabric 是基于分布式账本的自由软件企业会计系统，与其他著名的分布式账本以及区块链系统有一些重要的区别。

然而，要将 Hyperledger 与 Hyperledger Fabric 区分开来是至关重要的。Hyperledger 项目是由 Linux 基金会发起的开源区块链项目。

Hyperledger Fabric 旨在作为应用开发或模块化架构解决方案的基础。Hyperledger Fabric 能够提供诸如同意和成员服务等即插即用的组件。其模块化和适应性设计可适应各种行业用例。它采用了一种新颖的同意方法，既可以保护隐私，又可以实现全面的性能。

这是一种企业级解决方案，用于开发各种用例的应用程序，正如 IBM 所宣传的，它为各种应用领域提供了创新和多样性。

这是一个*授权*解决方案，因此参与者是已知的，没有公共网络和许可证带来的问题。因此，参与者之间存在信任。

这对共识产生了重大影响。在由受信任的权威管理的系统中，不需要共识。事实上，在这些情况下，从性能和速度的角度来看，这将是低效的。

这使得 Hyperledger Fabric 平台具有高性能。这个区块链被专门设计为高度模块化、可配置和可定制，以适应各种业务需求。

## 6.1 高层视角

本节通过提供高层视角来介绍 Hyperledger Fabric。它包括以下组件：

+   通过确定交易顺序并因此将新区块传输给对等体来建立系统共识的公司举动。

+   订阅网络运营商负责使用加密标识符验证网络身份。

+   为向其他对等体广播和排序服务结果块而设置的额外对等体间的消息传播通道。

+   可以配置分类帐以与各种数据库管理系统一起工作。

+   每个应用程序的可定制认可策略。因此，平台的每个方面都是模块化和可配置的。

+   在 Hyperledger Fabric 中，智能合约称为*链代码*。Hyperledger Fabric 的执行共识架构被称为*执行-排序-验证*。

实际上，它将交易流程分为三个阶段：

+   进行交易并验证其有效性，以此方式批准它。

+   使用可编程共识协议对交易进行排序。

+   在将交易注册到分类帐之前，必须根据应用程序区块链的策略对其进行验证。

Hyperledger Fabric 提供了一个通道结构。假设每个通道对应于一个且只有一个区块链。因此，一个区块链只与一个通道相关联。这意味着只有参与通道的组织才有权访问通道本身的数据，因此也有权访问该通道的区块链数据。

这个概念与私人数据的概念一起，提供了一定程度的数据安全和隐私保障。

将条目分类的任务委托给一个概念上与执行交易和维护分类帐的节点明显不同的模块化组件。这就是排序过程的工作原理。

只要这是模块化的，就可以将同意事项调整到对特定分发或解决方案的信任假设。

在讨论 Hyperledger Fabric 背后的概念和机制时，本章遵循并信任网络上可用的官方 Hyperledger Fabric 文档，尝试总结这些概念。因此，关于 Hyperledger Fabric 的所有信息都源自对其官方文档的研究和分析。

## 6.2 资产

Hyperledger Fabric 允许您使用 chaincode 构建任何类型的资产，无论是实物（财产、商品、产品等）还是无形的（合同条款、知识产权、文件等）。

在 Hyperledger Fabric 中，资产被指定为关键对的数量，状态变化被存储为分类帐上的交易（与通道相关）。资产可用于二进制和/或 JSON 表示。

## 6.3 Chaincode

Chaincode 是一种指定业务逻辑的软件类型。换句话说，它定义了一项活动或一组活动以及改变这些活动的交易指令。因此，chaincode 定义了改变活动状态的操作。它使用规则来读取或更改键值对。

结算提案触发链码功能，该功能在当前数据库账本上执行。当链码运行时，它创建了一组可以广播到网络并添加到所有对等体账本的写入。

## 6.4 账本的特点

账本按顺序跟踪所有网络状态转换。由参与方提供的链码调用（交易）产生状态转换。每个操作包含一组会话密钥，用于在账本中创建、更新或删除的资源。

账本包括：

+   用链存储不可改变的数据。

+   记录区块链当前位置的状态数据库。正如前面提到的，每个频道都有自己的账本。每个参与频道的对等体都有数据副本。

这里有一些账本特性：

+   执行基于关键字的搜索和查询，以及范围和通常依赖的查询。

+   使用先进的查询语言执行只读查询。（CouchDB）。

+   从历史记录中执行只读查询，并为键查询账本记录，允许数据来源的选项。

+   交易包含每个同行的签名，在转发到服务进行订单放置之前由他们批准。

+   交易包含每个同行的签名，在转发到排序服务之前由他们批准。

+   条目被分类到块中，并通过排序服务“分发”到频道上的对等体。

+   对等体通过检查事件来强制执行批准策略。

+   在添加块之前，进行版本检查以确认自链码代码执行以来读取资产的状态未更改。

+   一旦交易经过验证和提交，它就是不可变的。频道账本中的配置块定义了策略、访问控制和其他相关信息。

通道是成员提供者实例，允许从多个认证机构获取加密材料。

## 6.5 隐私

我之前说过，分类帐仅存在于一个通道中，在一个通道中只有一个分类帐。因此，只有通道的成员才能访问该通道的分类帐。这可以在确保隐私和保密性的同时做很多事情。

举个例子，假设存在供应商公司和各种客户公司的情景。如果供应商公司根据客户公司应用不同的价格，但不想透露这个细节，那么通道就是解决方案。事实上，只需为每个商业关系实施一个通道，任何信息的机密性都得到了保证。

此外，在通道内部还可以获得额外的保密级别。事实上，链码可以定义一个资产，用于改变后者的状态。在这方面，只有拥有该链码的对等方才能读取与该链码相关的资产。

如果该通道中的一组组织需要保持财务数据的机密性，它们可以收集数据并将其存储在与通道注册概念上不同的私有数据库中，仅可由机构内部的有限人员访问。

通过这种方式，通道为网络的其余部分维护私有交易，集合在通道组织子集之间存储私有数据。

在将交易提交给排序服务并将区块添加到账户之前，可以使用加密方法对链码的值进行加密，以进一步混淆数据。只有具有用于生成密文的相应密钥的用户才能在数据被打印到分类帐后解码加密数据。

## 6.6 身份

一旦加密数据被解密，区块链由多个参与者组成：

+   对等方

+   订单者

+   客户端应用程序

+   董事们

+   用户们

要验证身份，需要一个受信任的机构。成员服务提供商（MSP）是 Fabric 最受信任的机构。MSP 是制定该组织授权身份规则的元素。默认实现使用标准 PKI（公钥基础设施）模型，该模型采用 X.509 身份证书。

### 6.6.1 公钥基础设施（PKI）

*公钥基础设施* 是一种安全架构，允许生成、管理和使用加密密钥和数字证书。因此，它是一组技术，允许安全的网络连接。(见图 6-1.)

PKI 的元素包括：

+   认证机构（CA）

+   公钥和私钥

+   数字证书

+   证书吊销

认证机构（CA）颁发证书。MSP 确定某一组织受信任成员的福利。![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig1_HTML.jpg](img/520777_1_En_6_Fig1_HTML.jpg)

图 6-1

CA 电子数字证书示例

### 6.6.2 数字证书

数字证书是关于证书持有者的信息集合。

X: 509 数字证书的元素包括：

+   版本

+   序列号

+   算法 ID

+   发行机构

+   有效性

+   主题

+   主题的公钥信息

+   证书签名算法

+   证书签名

证书是加密的，因此防止篡改。任何变更都将使证书无效。实际上，它是用认证机构的私钥签名的，通过该认证机构的公钥验证。任何变更都将使验证过程无效。 (见图 6-2.)![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig2_HTML.jpg](img/520777_1_En_6_Fig2_HTML.jpg)

图 6-2

证书颁发机构和数字证书示例

它证明了公钥与主体身份之间的唯一关联。

数字证书的目的是确保公钥与声称拥有它的主体的真实身份相关联。实际上，应用的签名证明了声明的公钥是准确的。

实际上，应用的签名检查证书的公钥是否与证书内容中指定的主题相匹配。

因此，在开始阶段，如果马里奥·罗西想要对文档进行数字签名，他必须向通信中的其他参与者透露他的公钥。任何拥有该公钥的人都可以从他那里接收用私钥签名的文档，然后使用前述公钥验证签名；但是，任何人都可以透露一个不同的公钥，他知道其相对私钥，并声明这是马里奥·罗西的公钥。

为了避免这个问题，每个用户随后将其密钥输入由可靠的第三方签名的证书中（在 PKI 案例中，为证书颁发机构）。所有认可这个第三方的人只需检查其签名，就可以决定该公钥是否真的属于该用户。

## 6.7 证书颁发机构

认证机构将身份（公钥对和私钥）和证书分发给各种参与者。此证书将原告与参与者的公钥连接起来，并由认证机构进行数字签名（以及可能带有完整的属性）。因此，如果 CA 是受信任的（且公钥已知），则可以信任个体参与者。因此，如果信任 CA（并知道其公钥），则可以确保所识别的参与者与证书中提供的公钥相关联，并具有包含的特征，从而验证原告证书上的 CA 签名。 CA 负责确保组织中的所有参与者都具有经过验证的数字身份。（参见图 6-3。）![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig3_HTML.jpg](img/520777_1_En_6_Fig3_HTML.jpg)

图 6-3

证书颁发机构

## 6.8 会员服务提供商（MSP）

MSP 能够验证身份。换句话说，它们确定一个身份是否属于某个组织，以及在组织内担任的角色。因此，尽管 CA 可以发布身份和数字证书，但 MSP 可以在网络上识别这些身份。

MSP 还为成员在网络内提供各种角色和权限。

MSP 是将组织的身份与其成员资格相关联的方法。成员的公钥（也称为证书、证书签名）被添加到组织的 MSP 以获得成员资格。

MSP 还用于为网络参与者分配各种角色和权限。MSP 是将身份连接到组织成员资格的机制。成员的公钥（也称为证书、证书签名）被添加到组织的 MSP 以获得成员资格。

另一方面，MSP 的功能不仅仅是列出谁是网络或通道成员。通过识别节点或通道上参与者的独特权利，MSP 负责将身份转换为角色。当使用像管理员、对等方、客户、订购者或成员这样的角色在 CA Fabric 注册时，用户必须被分配一个角色。

### 6.8.1 本地 MSP

对客户和节点（对等方和订购者）的 MSP 是基于每个客户和每个节点指定的。本地 MSP 控制节点的权限（可以运行节点的对等方管理员）。在 MSP 的客户端处，用户可以作为通道的成员（例如，在链代码交易中）或系统中某个角色的持有者（作为管理员组织）进行身份验证。

客户本地 MSP 设置在节点的系统文件中，仅适用于该节点。因为订购者和对等节点像是单个机构的一部分，所以它们有一个单独的 MSP 来识别它们信任的参与者或节点。

### 6.8.2 通道 MSP

另一方面，通道 MSP 在通道级别建立管理和参与权利。应用程序通道上的对等方和排序节点与通道 MSP 拥有相同的视角，使它们能够适当地验证通道访客。这意味着，如果一个公司想要加入通道，通道设置应包括一个与该组织内部人员合作的 MSP。因此，涉及该组织身份的交易将被拒绝。

本地 MSP 在通道配置中记录，而通道 MSP 在文件系统中表示为文件夹结构。通道 MSP 确定了在通道级别谁具有权力。通道 MSP 定义了通道成员身份和执行通道级别规则之间的联系。

MSP 通道将所有参与组织的 MSP 链接到单个排序系统。排序服务很可能会拥有来自多家企业的排序节点，整个排序服务由这些企业共同管理。

### 6.8.3 存储 MSP 数据

本地 MSP 在通道配置中有记录，而通道 MSP 则以文件系统中的文件夹结构表示。通道 MSP 确定了谁在通道级别具有权限。通道 MSP 定义了通道成员身份与通道级别规则执行之间的联系。

MSP 通道将所有参与组织的 MSP 链接到单个排序系统。排序服务很可能会拥有来自多家企业的排序节点，整个排序服务由这些企业共同管理。

因此，通道 MSP 在逻辑上驻留并由通道或网络处理，但每个节点的本地文件系统都包含每个通道 MSP 的副本。

## 6.9 节点

区块链主要由相互通信的节点组成。由于它们拥有分类帐和智能合约，因此节点是网络的关键组成部分。分类帐以不可变的方式记录所有智能合约交易。可以添加、删除、重新启动、重新配置和删除节点。![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig4_HTML.jpg](img/520777_1_En_6_Fig4_HTML.jpg)

图 6-4

分类帐和链码

因此，一个节点具有一个或多个分类帐实例以及一个或多个不同链码的实例。（见图 6-4。）

实际上，一个节点可以参与不同的通道，因此拥有不同的分类帐实例（每个通道对应一个独立的分类帐）。

此外，根据网络的配置方式和设计目的，可能存在多个链码。 因此，对等方可以承载多个链码实例。![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig5_HTML.jpg](img/520777_1_En_6_Fig5_HTML.jpg)

图 6-5

应用程序和对等方

然后，为了获得对分类帐的访问权限，您展示了应用程序如何与对等方连接。 （见图 6-5。）Hyperledger Fabric 使 Fabric API 可用于开发人员的软件开发工具包（SDK），这使他们可以与对等方、链码以及分类帐进行交互。

应用程序可以通过对等方连接查询或更新分类帐。 分类帐查询的建议交易结果会迅速返回，但分类帐更新需要应用程序、对等方和排序器之间的更复杂交互。

图 6-6 以非常基本的方式显示了这一点。![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig6_HTML.jpg](img/520777_1_En_6_Fig6_HTML.jpg)

图 6-6

连接到对等方的应用程序

在图 6-6 中，应用程序 A 链接到 P1，并使用链码 S1 查询或修改 L1 分类帐。 P1 使用计划中的分类帐查询或更新的结果请求 S1 的响应。 应用程序 A 已收到提案响应，程序的查询阶段现在已完成。

应用程序 A 从所有更新回复生成交易，并将其发送到 O1 进行排序。 O1 从所有对等方，包括 P1，收集并分发交易。 P1 在提交到 L1 之前验证交易。 一旦 L1 被更改，从 A 接收后，P1 创建事件以表示完成。

在大多数情况下，应用程序必须连接到它们代表的对等方，以便批准账本更新主。 这在“事务流程”部分中有所示。

### 6.9.1 对等方和组织

不同的公司控制区块链网络，或者单个公司管理所有区块链网络。由于这些公司拥有它们，同行在构建这种形式的分布式网络中至关重要。同行也是组织网络的连接点。

在这种情况下，一个网络由四个贡献组织和八个同行组成。通过通道 C 连接的网络 N 中的五个同行是 P1、P3、P5、P7 和 P8。虽然这些公司的其他同行没有进入这个通道，但他们通常至少是另一个通道的成员。一家公司开发的应用程序将连接该公司内部以及其他公司的员工。为了清晰起见，在图 6-7 中没有显示出一个排序节点。![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig7_HTML.jpg](img/520777_1_En_6_Fig7_HTML.jpg)

图 6-7

连接组织和同行

多个贡献组织通过资源建立和管理网络。这个主题中的资源是同行；然而，组织提供的资源不仅仅是同行。如果没有向它提供独特资源的组织，协作网络将无法存在。由于这些成员实体提供的资源，网络会增长和缩小。

### 6.9.2 同行和身份

同行通过某个认证机构的数字证书被分配一个身份。当同行通过通道连接到区块链时，根据他们的身份在通道配置中的规则确定同行的权限。

因此，（通道）MSP 通过其*数字证书*识别它所属的组织。 (见图 6-8.)![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig8_HTML.jpg](img/520777_1_En_6_Fig8_HTML.jpg)

图 6-8

同行的身份

在这种情况下，CA1 已为 P1 和 P2 提供了身份。CA1 颁发的身份与 Org1 相关联，使用 ORG1.MSP，由通道 C 利用 MSP 通道确定。ORG2.MSP 还将 P3/P4 识别为 Org2 组件。

### 6.9.3 同行、共识和命令

为了确保网络区块链上几乎所有对等方都保持其信息同步，想要修改分类账的应用程序必须经过一个三步过程。

+   在第一步中，应用程序与一组支持的对等方连接，这些对等方分别提供了尚未应用于分类账的建议响应。应用程序与之交互以更新分类账的认可对等方子集由网络策略确定。

+   这些提案答案在第二步由一个应用程序收集，该应用程序：

    +   验证其一致性。

    +   作为结果将交易发送到排序服务。

+   在第三个也是最后一个阶段，排序服务将所有传入的交易命令排序组合成一个区块，然后发送到每个相邻节点，每个交易在记录之前都经过验证。

因此，组成排序服务的排序节点处于一切事务的中心。接下来的部分将深入探讨这个过程。

## 6.10 超级账本 Fabric 共识

超级账本 Fabric 中的同意经历三个阶段：

+   提议

+   交易在区块中的排序和打包

+   验证和提交

### 6.10.1 第一阶段：提议

首先，程序选择一组对等方来生成对所建议的分类账的更新。

批准策略（针对链码）确定必须批准所建议的分类账交易的组织，然后才能由网络接受并因此注册。

这就是达成共识的含义：每个相关组织都必须同意所提议的分类账更新，然后才能将其接受到任何对等方的分类账中。

应用程序开发提出的交易，它们将其传输给必须批准它的每一个同行组。每个都是唯一的。支持同行然后通过独立执行基于交易提议的链码来生成对结算提议的响应。此更新不适用于账本主节点；相反，它被签名并返回给应用程序。 (参见图 6-9。)![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig9_HTML.jpg](img/520777_1_En_6_Fig9_HTML.jpg)

图 6-9

提议

同行通过用他的私钥签署整个有效载荷并附加其数字签名来接受建议的答案。此权限稍后可用于证明某个响应是由公司内的同行生成的。

当应用程序获得足够数量的同行回复时，第 1 阶段结束。请注意，各种同行可能会返回给应用程序不同的交易答案，使结算提议产生矛盾。

这有两种可能的原因。由于链码的非确定性（链码中要避免的一个特性），或者是因为同行不一致。

如果一个应用程序试图使用不一致的回复交易更新分类账，它将被拒绝。如果提议成功，每个响应都是一致的，因此等同于其他响应。

### 6.10.2 阶段 2：交易被排序并打包成块

交易工作流继续进行打包阶段。因为他收到包含各种应用程序接受的结算提议的回复的交易，并将它们整理成片段，所以支付方对此过程至关重要。

授权人员除了其他职责外，还负责收集提议的交易更改、安排它们，并将其打包成块，以便交付给节点。 (参见图 6-10.)![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig10_HTML.jpg](img/520777_1_En_6_Fig10_HTML.jpg)

图 6-10

交易排序

阶段 3 从计算机将块分发给所有连接到它的节点开始。当生成新的块时，通过通道将节点链接到排序器，以便将新块的副本传播到所有连接到发起者的节点。每个节点将独立处理此块，但方式与通道上的其他节点相同。图 6-11 说明了如何以此方式保持分类帐恒定。值得注意的是，并非所有节点都需要连接到计算机：节点可以通过流言协议级联连接到其他节点。![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig11_HTML.jpg](img/520777_1_En_6_Fig11_HTML.jpg)

图 6-11

验证和最终确认

当一个节点收到一个块时，它会按照交易发生的顺序处理块中的每个交易。对于每笔交易，每个节点都将检查该交易是否已经被请求的组织授权，根据启动交易的链码的批准规则。 (参见图 6-11.)

例如，有些交易可能只需要单个组织的批准，而其他交易可能需要多个批准后才能被认为是真实的。

这个验证过程确保所有相关公司产生相同的结果。 这种验证与第一阶段的批准检查不同，在第一阶段，申请将收到授权的同行的答复，并选择是否传输所提议的交易。 如果申请违反批准规则，提交错误交易，对等方可能仍然会在第三阶段拒绝交易，即验证阶段。

如果交易已被正确接受，对等方将寻求在区块链上强制执行它。 为此，对等方必须进行检查账本一致性以确认当前状态的账本主状态是否与提议更新创建时的账本状态相对应。

即使交易已完全获得批准，这也不总是可行的。 例如，账本中的相同资源可能已更改到交易更新不再适用且无法实施的程度。 因为通道中的所有对等方都遵循相同的交易验证标准，所以账本保持不变。

## 6.11 账本

Hyperledger Fabric 的 IA 账本由两个独立但相互连接的部分组成：区块链和全局状态。 （见图 6-12。）

两者代表了一组业务项的信息捆绑。 ![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig12_HTML.jpg](img/520777_1_En_6_Fig12_HTML.jpg)

图 6-12

账本

第一步是使用区块链。 交易日志记录导致世界现状的所有事件。 交易被收集在添加到区块链的块中，这使您可以查看导致当前情况的事件路径。 由于一旦编写就是不可变的，区块链的数据结构与世界其他部分的数据结构相差很大。

第二，存在全局状态。一组业务对象状态的当前值存储在数据库中。程序可以直接访问它，而不必通过跨越整个交易注册来计算状态的当前值，因为状态使用全局状态。默认情况下，会计状态表示为键值对。状态可以生成、更新和消除，因此全局状态可能会经常更改。

因此，全局状态是从区块链的子集生成的。

### 6.11.1 区块链

区块链跟踪导致资产当前状态的事件。

区块链一直以文件形式实现，而状态则利用数据库。（参见图 6-13。）![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig13_HTML.jpg](img/520777_1_En_6_Fig13_HTML.jpg)

图 6-13

具有数据库的分类账

包含通道初始条件的网络配置事务包含在分类账的创世帧中。块结构是标准的，就像您在“区块链基础知识”中看到的那样。

### 6.11.2 交易

另一方面，交易的结构很有趣。它们的设计如图 6-14 所示。![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig14_HTML.jpg](img/520777_1_En_6_Fig14_HTML.jpg)

图 6-14

具有交易的分类账

在这个例子中，您可以看到以下字段：

+   **头部：** 包含一些关键的交易元数据，例如交易的链码名称和版本。

+   **签名：** 应用程序客户端生成数字签名，提供。此功能用于验证交易信息是否已更改，因为它需要应用程序的私钥来创建。

+   **提案：** 将应用程序的输入参数编码到生成提议分类账更新的链码中。

    当链码执行时，此提案提供一组输入变量，当与现有世界状态配对时，产生新的世界状态。

+   **响应：**涵盖了之前和之后的世界的值。这是智能合约的结果，如果交易被正确验证，它将被添加到账本中以更新全局系统。

+   **认可：**这是所有已批准交易答案的列表，必须遵守每家公司的批准政策。如果足够多的人签署了交易，全局状态就不会发生变化。

### 6.11.3 世界状态

*世界状态*反映了业务对象特性的主要价值，作为一个单一的会计状态。大多数应用程序需要对象的当前值；在整个区块链上衡量物品的真实价值将会很麻烦；相反，您可以直接从全局状态获取它。（见图 6-15。）![../images/520777_1_En_6_Chapter/520777_1_En_6_Fig15_HTML.jpg](img/520777_1_En_6_Fig15_HTML.jpg)

图 6-15

状态

数据库跟踪了地球当前状态。这是可以理解的，因为数据库提供了各种归档运算符以及快速的状态恢复。

全局状态数据库有两个选项：LevelDB 和 CouchDB。每个链码都有其自己的全局状态，这与所有其他链码的状态是独立的。这意味着世界状态存储在一个命名空间中，只能由来自相同链码的智能合约访问。因此，一个链码不能看到另一个链码的世界状态。

## 6.12 排序服务实现

在最新版本的 Hyperledger Fabric 中，排序服务是一个具有崩溃容错性的提供者。它被称为*Raft*。

Raft 使用“领导者和跟随者”范式，其中通道的排序节点动态选举领导者，然后将消息复制到通道的跟随者节点。Raft 具有崩溃容错性，因为它可以承受某些节点的丢失，例如领导者节点，只要大部分排序节点仍然可操作（CFT）。

## 6.13 总结

本章详细讨论了超级账本 Fabric。它从超级账本 Fabric 的特性开始，然后加深了您对超级账本 Fabric 的理解。超级账本的概念之所以重要，有以下几个原因：

+   许可制区块链

+   良好的性能和低事务延迟

+   根据您的需求进行模块化和配置

+   数据库抽象以加速与世界状态的交互

+   能够创建不同的通道，从而形成分类账

+   能够使用不同的编程语言开发应用程序和链代码

这个平台没有特别的缺点。讨论超级账本时，还必须考虑分布式系统以及超级账本如何在分布式系统中使用。这就是共识算法的概念发挥作用的地方。下一章将重点介绍分布式环境中的共识算法。