# Chainlink 如何实现区块链物联网集成

> 原文：<https://blog.chain.link/how-chainlink-enables-blockchain-iot-integrations/>

随着物联网(IoT)设备的数量预计将在 2021 年超过 250 亿，以及[智能合同](https://chain.link/education/smart-contracts)创新现已全面展开，区块链物联网应用已成为将不断增长的互联网连接传感器网络与区块链网络的安全自动化相结合的一个引人注目的用例。物联网设备是具有嵌入式技术的物理对象，使它们能够在没有任何人类交互的情况下通过互联网发送和接收数据。如今，物联网设备涵盖了智能手表、支持 WiFi 的电器和无线耳机等日常消费产品，以及支持智能城市、自动驾驶汽车和智能工厂的智能基础设施。

将物联网设备引入供应链管理和能源生产等各种行业，极大地提高了业务工作流程的效率，实现了对性能和资源消耗的实时监控。通过利用[区块链技术](https://blog.chain.link/what-is-a-blockchain-and-how-can-it-impact-the-world/)，企业可以利用智能合同、基于数学和防篡改的合同协议，为各方提供单一的真实来源，并根据预定义的业务逻辑自动化交易。智能合约是确定性的，这意味着它们将根据计算机代码定义的设置参数自动执行。因此，任何一方都不能违反合同义务——延期付款、价格差异和拒绝付款等问题都可以通过智能合同消除。

通过将物联网设备的真实输入与区块链强大的执行框架相结合，企业有机会构建由加密保证支持的日益数据驱动的流程，并围绕链上数据集推出新产品和市场。

## 区块链技术给物联网带来的好处

通过将现有的物联网设备连接到区块链，企业可以立即提高设备安全性，自动化业务工作流，并围绕以前分散和不透明的系统实现端到端透明。

### 安全性

虽然它们与互联网的连接为物联网设备提供了丰富的功能、特性和设计，但这也使它们容易受到攻击。黑客可以[操纵智能城市中的交通传感器](https://www.wired.com/2014/04/traffic-lights-hacking/)，[劫持自动驾驶汽车，](https://physicsworld.com/a/how-to-hack-a-self-driving-car/)或[利用智能工厂中的关键机器](https://www.trendmicro.com/vinfo/fr/security/news/internet-of-things/security-threats-and-risks-in-smart-factories)。能够访问个人数据的物联网设备也可能[将这些敏感信息](https://www.bitdefender.com/box/blog/iot-news/iot-devices-leak-data-third-parties-study-reveals/)泄露给第三方。通过分散式 oracles，物联网设备可以安全地将数据传输到区块链，在那里数据被记录在链上，然后可以触发超可靠的输出。对于黑客来说，要操纵区块链上的记录数据，他们必须破坏区块链本身，为物联网设备数据提供一个防篡改的安全层。

### 自动化

企业可以利用物联网设备的精细传感器读数结合智能合同来自动化和优化现有的业务流程。例如，在工业环境中，开发人员可以将智能合同与物联网传感器集成，以进行预测性维护。制造工厂中的物联网设备可以定期向区块链传输诊断机器数据，智能合同可以被编程为在个别机器偏离建议的健康设置时关闭它们。在未来，自主的机器对机器交易可以发生，其中只需要人工输入来对初始智能合约变量进行编程。

### 透明度

通过将物联网设备连接到智能合同，管理复杂供应链网络交易的企业可以利用区块链的单一真实来源来实现产品移动的端到端透明。从历史上看，现有业务网络中的信息通常是孤立的，分散在不同的系统中，导致过多的后台成本、合同错误和处理延迟。将通常用于识别和跟踪库存商品的 RFID 标签与基于区块链的智能合同相集成，提供了从源头到最终客户的全球材料分配的防篡改和可审计记录。

## 通过分散式 Oracles 安全连接区块链和物联网

为了确保安全性和可靠性，区块链特意与外部输入(如真实世界的数据)断开连接。为了让区块链安全地与链外资源交互，他们需要 oracle 的帮助，Oracle 是一种中间件，将智能合同连接到外部系统，包括企业资源规划(ERP)系统。Oracles 对于将物联网设备连接到区块链环境至关重要，有助于企业利用智能合同的诸多优势。

![Chainlink connects any IoT device to any blockchain and any output.](img/a48d0fbdfa711bd8661ac8059e5caea4.png)

<figcaption id="caption-attachment-1801" class="wp-caption-text">Connect any IoT device to any blockchain and any output with Chainlink oracles.</figcaption>



[Chainlink 的](https://blog.chain.link/what-is-chainlink/)广泛采用的 oracle 网络使任何区块链上的智能合同能够与来自任何[应用程序编程接口(API)](https://blog.chain.link/understanding-how-data-and-apis-power-next-generation-economies/) 的任何数据进行交互。由于物联网设备目前使用 API 通过互联网与应用程序进行通信，因此它们可以通过 web 服务器连接到 Chainlink oracle 网络。设备还可以配置 Chainlink oracle 节点，以直接向智能合约提供数据，允许数据提供商为分散式应用提供基于物联网的链上数据。

Chainlink 是区块链不可知的，这意味着企业可以使用 Chainlink oracles 将其物联网设备连接到他们选择的任何区块链环境。现在已经出现了数百个区块链，它们在性能和许可方面具有不同的特性，这使得潜在的企业集成商面临巨大的选择。Chainlink 消除了围绕单个区块链构建内部支持和集成的成本，使企业能够高效地连接到快速增长的多链生态系统中的任何区块链。

尤其对于企业而言，在集成任何新技术时，安全性都是至关重要的。Chainlink 的防篡改和久经考验的基础设施确保 oracle networks 在将区块链网络连接到外部世界时满足分散计算的底层安全保证。

## 使用 Chainlink 的真实世界区块链物联网应用

Chainlink 的分散式 oracles 正在支持区块链联网设备的新生态系统，为不同行业的各种组织提高自动化和效率。

### 高效的供应链跟踪

供应链是复杂的系统，通常需要多个中介机构来确保支付得到正确处理，货物得到有效跟踪。 [PingNET](https://medium.com/@pingnet/ping-to-integrate-chainlink-oracles-to-provide-iot-data-to-smart-contracts-2fd9d5a1abe2) 是一个面向物联网设备的分散传输网络，计划利用 Chainlink 实现供应链支付自动化。例如，嵌入运输托盘的物联网传感器将位置数据发送到 Chainlink 节点，以证明它们是否已经到达正确的交付地址。如果位置数据证明托盘到达了正确的地址，该数据将自动触发[智能合同](https://www.computerworld.com/article/3412140/whats-a-smart-contract-and-how-does-it-work.html)向运输公司付款，防止运输和处理延迟。

### 会计透明度

会计中财务差异的头号原因是[人为错误](https://incisive.com/the-financial-damage-caused-by-human-error-and-how-to-prevent-it/)。区块链创建一个共享的事务分类帐，可以减少会计流程中的人工错误，并建立可核实的交易资产历史记录。[开放图书馆项目](https://blog.chain.link/rfid-blockchain-integration-with-chainlink-external-adapters/)通过使用 Chainlink oracles 创建一个分散的图书租赁系统展示了这一功能。这些书嵌入了射频识别(RFID)标签，这使得它们可以在通过无边界租赁系统从一个客户到另一个客户的过程中被有效地跟踪。公司可以将 RFID 技术应用于产品，通过供应链循环跟踪产品，实现从源头到目的地的透明。

### 健康可穿戴设备

通过改善数据共享和透明度，区块链连接的物联网设备正在释放体育和健康领域的新激励机制。 [Gran Fondo，](https://blog.chain.link/detailing-the-winning-chainlink-projects-from-ethdenver-hackathon/)一个健身挑战 dApp，在 2019 年的 ETH Denver chain link 的黑客马拉松中获得第二名，因为它使用 Chainlink oracles 将智能手表数据与智能合同连接起来，激励运动员根据表现目标争夺 ETH 奖金。随着医疗保险欺诈估计每年花费超过[600 亿美元](https://www.bcbsm.com/health-care-fraud/fraud-statistics.html#:~:text=The%20National%20Heath%20Care%20Anti,care%20expenditure%2C%20or%20%24230%20billion.)，医疗保险公司也可以使用 Chainlink 来分析来自物联网可穿戴设备的身体活动水平和生物识别数据的可验证、防篡改记录，以正确估计投保人的公平保险费。

### 参数保险

![Chainlink connects weather data sources to nodes for Arbol’s decentralized insurance.](img/33ba023e698a39d2744537373a4751e0.png)

<figcaption id="caption-attachment-1803" class="wp-caption-text">Chainlink connects IoT sensors for Arbol’s decentralized insurance products.</figcaption>



智能合同正在通过启用决定性的[参数保险](https://blog.chain.link/parametric-insurance-smart-contract/)产品来[改革保险行业](https://blog.chain.link/blockchain-insurance/)，该产品在满足预定条件时自动向投保人付款。例如，当物联网传感器确定特定地点的降雨量符合智能合同的预定义条款时，分散保险协议 [Arbol](https://www.arbolmarket.com/) 使用 Chainlink 神谕自动向投保人支付降雨量保险索赔。块状链连接的物联网设备可以为各种各样的参数化保险产品供电，从记录航运保险位置数据的全球定位系统传感器，到监测地震的压力传感设备，以提供灾难保险。

### 自动化车辆租赁

Chainlink 的安全分散式 oracles 使开发人员能够快速构建新的应用程序，利用区块链网络来触发现实世界中的输出。 [Link My Ride](https://blog.chain.link/create-tesla-smart-contract-rental/) ，Chainlink 虚拟黑客马拉松大奖获得者，将他们的 Tesla API 连接到 Chainlink oracle，用于区块链的点对点车辆租赁应用程序。随着车辆变得完全自动化，人们可以想象一种只需最少人力投入的[机器对机器](https://internetofthingsagenda.techtarget.com/definition/machine-to-machine-M2M)租赁模式。Chainlink 易于集成的 oracle 基础设施由广泛的[集成文档](https://docs.chain.link/docs/getting-started)支持，使开发人员能够从其智能合同中安全地调用外部 API，并探索区块链物联网的各种可能用例。

### 衡量消费和污染

除了流程效率和透明度，区块链物联网集成还使企业能够探索鼓励可持续消费的新激励模式。自动化引擎 [NetObjex](https://www.netobjex.com/) 正在为有意识的旅行者建立一个忠诚度计划，该计划使用物联网传感器来测量他们在选定酒店的水和能源使用情况。对于低于平均消费水平的旅行者，智能合同将自动授予他们奖励代币，这些代币可以转换为现金或兑换为未来的酒店入住。政府甚至可以通过将工厂的排放监控物联网设备连接到区块链来强制执行污染限制，这也有助于减少排放报告欺诈。Chainlink 的分散式 oracles 可确保将外部的原始签名数据安全地传送到区块链网络，然后智能合同可以使用这些数据来触发现实世界的输出并实施环境可持续的做法。

[https://www.youtube.com/embed/BHsPaKtgioE?feature=oembed](https://www.youtube.com/embed/BHsPaKtgioE?feature=oembed)

## 结论

区块链连接的物联网设备已准备好转变一系列行业，但要安全轻松地将物联网设备与快速增长的区块链生态系统集成，需要高度分散和灵活的 oracle 解决方案。Chainlink 久经考验且不受供应链限制的 oracle 基础设施已成为这一关键桥梁，它已经启动了与外部输入交互的新一波智能合同应用程序，并实现了基于区块链的流程为外部世界带来公平、透明和高效的潜力。

如果您是一名开发人员，并希望将您的智能合同连接到现有的数据和基础设施，请访问 [Chainlink 开发人员文档](https://docs.chain.link/)。对于更深入的整合，[请咨询专家](https://chainlink.typeform.com/to/gEwrPO)。

### 关于这个话题的更多信息

*   [77 个由 Chainlink 支持的智能合约用例](https://blog.chain.link/44-ways-to-enhance-your-smart-contract-with-chainlink/)
*   [区块链甲骨文问题是什么？](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)
*   [使用 Chainlink 外部适配器构建 RFID 区块链集成](https://blog.chain.link/rfid-blockchain-integration-with-chainlink-external-adapters/)