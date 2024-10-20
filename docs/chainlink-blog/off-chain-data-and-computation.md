# 什么是链外数据和计算？

> 原文：<https://blog.chain.link/off-chain-data-and-computation/>

什么是外链数据？链外数据有时也称为真实世界的数据，是区块链外部的任何数据，如体育比分、天气数据和金融市场数据，以及其他区块链上的数据。就其本质而言，区块链是孤立的系统，因此将区块链连接到离线数据就像将计算机连接到互联网一样，它使孤立的系统能够与现实世界进行交互。在访问链外数据时，必须维护区块链的高安全性保证，这就是为什么 [Chainlink](https://blog.chain.link/what-is-chainlink/) 信任最小化服务已经成为行业标准的原因。

另一种增加区块链效用的链外机制是链外计算，它包括可验证的随机性、交易订购服务和智能合同自动化。链外计算是发生在区块链之外的简单计算。Oracle networks 可以提供一种信任最小化形式的离链计算来扩展区块链的功能，这被称为 [oracle 计算](https://blog.chain.link/what-is-oracle-computation/) 。让区块链拥有离线计算能力就像把笔记本电脑连接到 AWS 这样的云服务上一样；它成倍地扩展了可用的计算能力，并支持构建高性能且经济高效的应用。

为什么离线数据和计算对 Web3 生态系统如此重要？90%的智能合约用例需要访问链外数据，包括许多分散金融(DeFi)用例、参数保险、 [动态 NFTs](https://blog.chain.link/what-is-a-dynamic-nft/) 。离线计算有助于这些应用以经济高效和保护隐私的方式进行扩展，并引入自动化和随机性等更高级的功能。总之，链外数据和链外计算使开发人员能够构建功能丰富、可扩展的混合智能契约，帮助数百万乃至数十亿用户解决现实世界中的问题。

在本文中，您将了解 oracles 如何将区块链与链外数据和计算联系起来，链外数据和链内数据的区别，探索链外资源带来的优势，以及为什么 Chainlink 是连接链外资源和区块链的领先解决方案。

## 通过分散的 Oracle 网络将链外资源连接到区块链

当区块链连接到链外资源时，智能合约可用的计算能力和数据急剧扩展。虽然有可能利用像 Web2 中那样的集中式离链服务，但这会引入单点故障，破坏区块链提供的安全保证。

为了将区块链连接到链外数据，开发人员需要克服“ [【甲骨文问题】，](https://blog.chain.link/what-is-the-blockchain-oracle-problem/) ”这描述了区块链无法以高度安全和防篡改的方式连接到外部资源。Chainlink 通过使分散式 oracle networks (DONs)作为一个安全的中间件层将链外资源连接到区块链来解决 oracle 问题。Chainlink Network 是业界领先的 oracle 网络，负责确保整个 Web3 生态系统中数百亿美元的安全。

分散式 oracle networks (DONs)以信任最小化的方式扩展了区块链和智能合约的数据可访问性和计算能力，以保证安全性。通过启用[](https://blog.chain.link/hybrid-smart-contracts-explained/)混合智能合约，don 增强了区块链的性能、功能和互操作性。这些合同将区块链的信任最小化属性与链外计算资源和数据的丰富特性融合在一起，以实现更高级的应用程序和用例，这些应用程序和用例是链上系统无法单独实现的。

![Image showing how smart contracts connect to external data. ](img/e992ba2e92589b267004cc21a8afcfe8.png)

<figcaption id="caption-attachment-3839" class="wp-caption-text">Decentralized Oracle Networks (DONs) enable smart contracts to securely connect with external data and systems.</figcaption>



## 链上与链下

区块链是不可变的、确定的、高度安全的、抗审查的分类账，由全节点网络保护。虽然这种设计赋予了区块链高度的安全性和确定性，但它也意味着区块链经常不得不在隐私、速度和去中心化之间做出权衡。然而，通过将区块链与离线系统相结合，区块链能够扩展他们的能力，从通过将计算移出链来降低成本和增加吞吐量，到将真实世界的信息合并到链上执行。

![Image comparing off-chain and on-chain resources.](img/836cc90be4ca2348fc9e66db9ed59ec3.png)

<figcaption id="caption-attachment-3842" class="wp-caption-text">Hybrid smart contracts combine on-chain code with off-chain decentralized oracle networks to enable more advanced blockchain-based applications.</figcaption>



### 链上数据

链上数据仅限于区块链网络内本地生成的数据。这包括账户地址及其相关余额，以及 [智能合同](https://chain.link/education/smart-contracts) 状态。

在链数据包括:

*   **账户**—区块链账户是可以发送和接收交易的个人地址。
*   **余额**—一个账户拥有的原生币数量，如比特币区块链上的 10 个 BTC 或以太坊上的 100 个 ETH。
*   **智能合约**—存储在区块链的全局状态中的分布式计算机程序，例如 ERC20 令牌合约或 [自动做市商(AMM)](https://blog.chain.link/challenges-in-defi-how-to-bring-more-capital-and-less-risk-to-automated-market-maker-dexs/) 应用。

### 链外数据

非连锁数据是区块链以外的信息。使区块链能够与现实世界进行交互，可以在许多不同的行业中实现多种 [智能合同用例](https://blog.chain.link/smart-contract-use-cases/) 。

chain link don 以高度安全可靠的方式将大量链外数据集纳入链中，并由智能合约消费:

 ***   **金融数据** — [Chainlink 价格提要](https://data.chain.link) 为[DeFi](https://chain.link/education/defi)经济提供超可靠的全球精确价格数据，用于分散稳定信贷、借贷协议等。
*   **天气数据** — [Chainlink 数据馈送](https://chain.link/solutions/defi) 向天气预测市场、对冲市场和动态 NFTs 提供降雨、温度和其他天气数据。 例如，[Arbol](https://www.arbolmarket.com/)通过 Chainlink 数据馈送获取天气数据，以支持其向发展中国家的农民提供参数作物保险。
*   **体育、供应链和经济数据**—数据馈送还提供广泛的链上数据，如体育统计数据、供应链信息、选举结果、通货膨胀率等等。
*   **准备金数据** — [准备金链证明](https://chain.link/solutions/proof-of-reserve) 提供对菲亚特支持的稳定资本和跨链资产的准备金审计，帮助 DeFi 应用减轻部分准备金活动的负面影响。
*   **身份数据**—chain link Oracle 可以使用电子签名、凭证和域名以保护隐私的方式验证分散应用程序的用户身份。
*   **Any API**—[Chainlink Any API](https://docs.chain.link/docs/request-and-receive-data/)使开发者能够使用现有的 chain link 节点以向后兼容的方式访问任何外部数据源。

chain link 数据馈送和其他信任最小化服务在链上提供的数据点总数超过 20 亿，为区块链生态系统中的数百个项目提供支持，其中包括行业领先的协议，如 Aave、Compound、dYdX、 [、Liquity](https://chain.link/case-studies/liquity) 、Synthetix 等。

![Image of the interactions between on-chain and off-chain resources.](img/e49aeaa30bc26daac4da9ca83a17e99f.png)

<figcaption id="caption-attachment-3843" class="wp-caption-text">Visualizing the interactions between off-chain and on-chain resources.</figcaption>



### 链上计算

区块链在执行特定类别的计算方面独树一帜，并在交易方面产生强烈的共识。虽然它们擅长验证所有权、执行不可变的智能契约，并提供单一的事实来源，但它们缺乏链外系统所提供的丰富特性。

链上计算的例子包括:

*   **验证所有权**—当用户从其账户进行交易时，区块链将检查所使用的私钥签名是否与公钥匹配。
*   **执行智能合约**—当智能合约功能接收到输入时，例如在[分散式交易所](https://blog.chain.link/dex-decentralized-exchange/)进行代币交易，区块链计算交易并执行状态更改。
*   **添加新块**—节点定期向区块链添加新的事务块，其他节点通过重新执行块中的所有事务来检查。

### 链外计算

通过由 oracle 网络执行的信任最小化的链外计算，由于成本、可伸缩性或其他考虑而不可能或不适合在链上执行的计算可以在链外执行，然后在链上中继。

链式网络执行的链外计算包括:

*   **可验证的随机性** — [链环 VRF](https://chain.link/solutions/chainlink-vrf) 生成加密证明支持的随机性，然后交付并在线验证。这使得链上游戏 dApps 能够引入不可预测的游戏事件，并以可证明的公平方式进行 NFTs 铸造。
*   **智能合约自动化**—[chain link Automation](https://chain.link/automation)提供分散式交易执行服务，可用于自动触发重要的智能合约功能，如执行清算、重置代币、结算限价单等。这是通过离线执行智能契约的一部分来检测是否需要调用链上函数来实现的。
*   **链外报告**—Chain link 数据馈送中的多个节点可以通过 [链外报告(OCR)](https://docs.chain.link/docs/off-chain-reporting/) 协议将其响应链外聚合到一个 oracle 报告中，从而提高成本效益，支持更大的节点委员会，并在区块链网络极度拥塞期间提高可靠性。

## 离线数据和离线计算的优势

链外资源释放高级智能合约功能，使开发人员能够构建功能丰富的应用。

### 链外数据优势

没有链外资源，区块链仅限于简单的功能，如代币的创建和转移。将外链数据引入区块链网络使开发者能够构建更高级的应用，如参数保险、预测市场、稳定积分等。

为区块链提供对真实世界信息的访问支持多种高级用例:

*   **对冲金融风险**—金融市场数据使交易者能够利用预测市场对冲金融头寸。
*   **参数保险**—参数保险有助于减轻现实世界风险的财务影响。例如，天气数据使得农民可以通过购买区块链的参数作物保险来防范干旱带来的经济损失。
*   **供应链跟踪** —RFID 跟踪、物联网传感器和清关数据使协议能够验证供应链中的货物位置。
*   **身份验证**—通过交叉引用安全数据库中的电子签名或生物特征数据，应用程序可以验证用户身份。
*   **支持可持续发展**—物联网传感器和卫星图像可用于测量温室气体排放和重新造林项目，并且这些数据可用于多个智能合同用例，如碳信用验证。
*   **储备验证**—验证稳定币和跨链资产的储备有助于用户确保代币得到完全支持。

### 链外计算优势

随着工作从区块链节点卸载，开发人员能够构建用例，否则仅仅通过链上计算是不可能的。

由 DONs 提供的信任最小化的链外计算扩展了区块链网络的能力，具有如下特征:

*   **增强的隐私**—离线完成计算可以确保私人用户数据，如身份相关信息，不会发布在公共区块链账本上供任何人查看。
*   **速度和可扩展性**—大量计算可以快速离线执行，其输出在链上记录，使开发人员能够构建快速和可扩展的 dApps。
*   **成本效率**—在单次交易中将数据发布到链上之前，聚合链外数据可以显著降低成本。
*   **灵活性**—非链计算允许用户决定他们愿意在安全性和性能之间做出的具体权衡。他们可以定制他们的分散化程度、加密经济安全性和其他安全因素。

## 由链节驱动的链外资源

chain link 网络是连接区块链和包括数据和计算在内的链外资源的行业领先解决方案。Chainlink 生态系统中的服务积极支持十几个区块链的数百个高级智能合同，目前帮助确保整个 Web3 经济价值数百亿美元。

在此视频中，了解 Chainlink 如何通过提供真实世界的数据和离线计算，为分散式应用带来无与伦比的效用水平:

[https://www.youtube.com/embed/n7zyqVopiEU?feature=oembed](https://www.youtube.com/embed/n7zyqVopiEU?feature=oembed)

通过集成 Chainlink 信任最小化服务，开发人员现在就可以开始使用离线数据和计算。您可以使用chain link Data Feeds访问高质量、超可靠的真实世界数据， Chainlink VRF 作为密码安全随机性的防篡改来源，chain link Automation以分散、经济高效且高度安全的方式触发您的智能合约功能，以及chain link Proof Reserve使用自动化审计监控储备资产。

通过组合这些服务，开发人员可以构建功能丰富、经济高效且可扩展的应用程序，以维护区块链的安全保证。 如果你想在你的以太坊或索拉纳 dApp 中利用链外计算，请访问 [文档](https://docs.chain.link/) 、 [不和谐](https://discord.com/invite/aSK4zew) ，或 [与专家聊天](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=homepage&typeform-source=blog.chain.link) 。

## 附加资源

*   [什么是智能合约？T3T5】](https://chain.link/education/smart-contracts)
*   [什么是区块链甲骨文？T3T5】](https://chain.link/education/blockchain-oracles)
*   [Chain link 如何支持任何链外数据资源和计算](https://blog.chain.link/how-chainlink-supports-any-off-chain-data-resource-and-computation/)
*   [链外计算:统计分析用链](https://blog.chain.link/off-chain-computation-statistical-analysis-with-chainlink/)**