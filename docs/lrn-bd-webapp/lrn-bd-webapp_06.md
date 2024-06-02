© Santiago Palladino 2019S. PalladinoWeb 开发人员的以太坊[`doi.org/10.1007/978-1-4842-5278-9_6`](https://doi.org/10.1007/978-1-4842-5278-9_6)

# 6. 索引和存储

Santiago Palladino^(1 )(1)阿根廷布宜诺斯艾利斯自治城

在前两章中，我们学习了如何从以太坊网络中读取和写入数据。读取可以作为常规调用合约或查询已记录的事件来进行，而写入总是在事务的上下文中执行。然而，这些操作只适用于基本用例。如果我们想要从区块链显示聚合数据，仅仅在客户端查询事件就很快不够用了。同样，如果我们想要在合约中存储大量信息，燃气费用会使其在经济上不可行。在本章中，我们将使用链外组件来解决这两个问题。我们将首先介绍在服务器中索引区块链数据以从客户端应用程序查询它的过程，然后探讨链外存储解决方案。我们还将讨论处理重组和测试的技术，并在此过程中讨论集中化与去中心化解决方案的价值。

## 索引数据

我们将从区块链数据的索引问题开始讨论。在这个上下文中，*索引*指的是从网络中收集某些信息（如代币余额、发送的交易或创建的合约）并将其存储在可查询的数据存储中，如关系型数据库或像 ElasticSearch 这样的分析引擎，以执行复杂的查询。在本章中，我们将选择一个特定的数据集，并为其构建一个量身定制的解决方案，而不是尝试索引整个链。

需要在记录数据时执行任何类型的*聚合*操作时，例如求和或平均值时，都需要进行索引，因为以太坊事件 API 并不适合执行此类操作。例如，很难轻松地获取持有一定余额的某种 ERC20 资产的唯一地址数量——这是在关系型数据库上运行的一个简单查询。

当查询大量事件时，索引也可用于提高性能，充当查询缓存。与常规以太坊节点相比，专用数据库可以更快地回答事件查询。

### 注意

某些公共节点提供商，如 Infura，实际上包括一个事件查询层，^(1) 与它们的节点分开，以极大地减少它们为服务日志所需的基础设施的占用。

我们现在将专注于一个特定的索引使用案例，并设计一个收集索引信息的解决方案。

### 跟踪 ERC20 代币持有者

我们将跟踪特定 ERC20 代币的持有者。请记住，ERC20 非同质化代币可以充当代币，其中每个地址都有一定的余额。然而，合约没有提供实际列出它们的方法。即使有，一些代币的用户群体远远超出了仅查询以太坊节点的客户端应用程序的能力。例如，在撰写本文时，OmiseGO（OMG）代币拥有超过 650,000 个唯一持有者。^(2)

#### 重新审视 ERC20 接口

我们将回顾 ERC20 合约接口，以确定我们将使用的基本组件。暂时不考虑与授权相关的功能，ERC20 标准包括这些方法和事件。函数**transfer**(address to, uint256 value) 返回（bool）；函数**totalSupply**() view 返回（uint256）；函数**balanceOf**(address who) view 返回（uint256）；事件**Transfer**（  address indexed from, address indexed to, uint256 value）；

正如提到的，与扩展的 ERC721 标准不同，ERC20 并不提供列出所有代币持有者的方法。构建这样一个列表的唯一方法是通过每个 *Transfer* 事件并收集所有接收者地址。

### 注意

某些 ERC20 合约在铸造新令牌时不会发出转账事件，而是发出一个非标准的铸币事件。在这种情况下，我们需要跟踪这两种事件，以便构建完整的持有者集合。

#### 查询转账事件

我们将从给定合约查询所有转账事件开始。我们将构建一个 ERC20Indexer 类，依赖于 web3 连接提供程序、一个 ERC20 令牌地址和一个开始查询的区块号（见列表 6-1）。这最后一个参数仅出于性能原因添加：在令牌合约部署之前查询任何区块是没有意义的。// 01-indexing/simple-indexer.js

构造 ERC20Indexer 类的构造函数，我们将在其中工作。我们再次依赖 openzeppelin-solidity@2.2.0 来获取 ERC20 合约 ABI。我们将所有令牌持有者地址的列表存储在持有者集合中，并且 lastBlock 字段将跟踪我们已处理的最后一个区块。

现在我们可以向这个类添加一个方法来获取给定合约的转账事件列表（见 6-2）。由于该列表的长度可能大于我们可以容纳在单个请求中的长度（OMG 目前已经超过 200 万次转账），所以我们需要将其拆分为多个请求，因此我们将从一个处理区块范围内的所有事件的方法开始。async processBlocks(startBlock, endBlock) {  for (let fromBlock = startBlock;       fromBlock <= endBlock;       fromBlock += BATCH_SIZE) {    const toBlock = Math.min(      fromBlock + BATCH_SIZE - 1, endBlock    );    const events = await this.contract      .getPastEvents('Transfer', { fromBlock, toBlock });    events.forEach((e) => this.reduceEvent(e));  }}Listing 6-2

批量从一系列区块中查询所有转账事件。在这里 BATCH_SIZE 应该取决于合约每个区块的交易量。

此方法将获取合约中一个区块范围内的所有转账事件，并将它们发送到一个 reduceEvent 函数（见 6-3）。此减少函数应接收一个事件并使用它来更新令牌持有者列表。const ZERO_ADDRESS = '0x0000000000000000000000000000000000000000';async reduceEvent(event) {  const { to } = event.returnValues;  if (to !== ZERO_ADDRESS) {    this.holders.add(to);  }}Listing 6-3

检索令牌转移的接收者以将其添加到令牌持有者列表中。转移到零地址的转账通常是令牌被销毁，因此我们将其排除在我们的列表之外。

### 注意

在生产实现中，您不希望将持有者列表存储在一个在进程停止时被清除的 JavaScript 数据结构中的内存中。您应该使用数据库来存储所有数据并为客户端的查询提供服务。数据库引擎的选择不在本书的范围之内，它严重依赖于您的用例。

然而，这种方法可能会产生一些误报。如果某个地址曾经持有一些余额，但后来将其全部转移，那么它将被添加到我们的持有者列表中，但永远不会被移除。这意味着我们需要检查一个地址的余额是否为非零才能列出它。既然如此，我们将额外努力追踪每个持有者的当前余额。我们有两种选项来做到这一点，每种选项都有其自身的利弊：

+   我们可以依靠 ERC20 的 `balanceOf` 方法来检查我们添加到列表中的每个地址的余额。我们可以在找到新地址并将其添加到集合中后立即这样做，并且具有其余额的持有者已经准备好。然而，这意味着我们为每个令牌持有者进行了额外的请求，并且每当我们看到一个新的区块有新的转账时，我们也需要重新运行此查询。

+   我们可以利用 ERC20 合约中任何地址的余额只需查看转账事件这一事实。由于我们已经在查询它们，我们可以跟踪每个地址的所有收入和支出，并相应地更新它们。这将需要我们端的一些逻辑，但不需要额外向以太坊网络发送请求。其缺点是，我们无法在扫描到链中最新区块之前依赖于一个地址的余额。

为了优先减少请求数量，我们将采用第二种策略（见 6-4）。这意味着我们用于减少事件的函数还需要考虑每个转账的 *value*。async reduceEvent(event) {  const { from, to, value } = event.returnValues;  if (from !== ZERO_ADDRESS) {    this.balances[from] = this.balances[from]      ? this.balances[from].minus(value)      : BigNumber(value).negated();  }  if (to !== ZERO_ADDRESS) {    this.balances[to] = this.balances[to]      ? this.balances[to].plus(value)      : BigNumber(value);  }}Listing 6-4

将事件简化为更新每个持有人的余额。这里的 balances 是一个替换了原来持有人集合的对象。请注意，我们排除了零地址作为发送方和接收方，因为从零地址的转账代表铸币事件，而向零地址的转账代表销毁。

拥有一个可以为给定区块范围生成持有人及其余额列表的类后，我们现在需要在新区块被挖掘时保持此列表更新。我们将使用轮询来获取新区块，虽然订阅也是一个可行的替代方案。CONFIRMATIONS = 12; INTERVAL = 1000;async processNewBlocks() { const lastBlock = this.lastBlock; const currentBlock = await this.web3.eth.getBlockNumber(); const confirmedBlock = currentBlock - CONFIRMATIONS; if (!lastBlock || confirmedBlock >= lastBlock) { await this.processBlocks(lastBlock, confirmedBlock); this.lastBlock= confirmedBlock + 1; }}start() { this.timeout = setTimeout(async () => { await this.processNewBlocks() this.start(); }, INTERVAL);}Listing 6-5

轮询新区块并检索任何新的转账事件。processNewBlocks 函数将查询最新的区块并调用 processBlocks 处理新区块范围，而 start 函数则启动一个无限循环，不断轮询然后休眠 1 秒。

我们实现的一个重要细节是，我们不会处理直到最新的区块，而只会处理到一定数量的区块之前。这确保我们已经处理的任何转账事件都已经确认，并且不会作为重组的一部分被回滚。随后，我们将研究查询最新区块并在检测到重组时处理的策略。

#### 分享我们的数据

最后一步是实际提供我们收集到的数据的访问权限（见 6-6）。 我们将建立一个简单的表达服务器，在 HTTP GET 请求时以 JSON 格式暴露余额集合。const express = require('express')const mapValues = require('lodash.mapvalues');// 用于测试主网代币的示例值 const API_TOKEN = 'YOUR_INFURA_API_TOKEN';const PROVIDER = 'https://mainnet.infura.io/v3/' + API_TOKEN;const ADDRESS = '0x00fdae9174357424a78afaad98da36fd66dd9e03';const START_BLOCK = 6563800;// 初始化表达应用程序和索引器 const app = express()const indexer = new Indexer({  address: ADDRESS,  startBlock: START_BLOCK,  provider: PROVIDER});// 注册用于查询余额的路由 app.get('/balances.json', (_req, res) => {  res.send(    mapValues(indexer.balances, b => b.toString(10))  );});// 开始！app.listen(3000);indexer.start();Listing 6-6

一个简单的表达服务器，通过 HTTP 端点暴露索引器中的余额。 在将它们序列化为 JSON 之前，使用 mapValues lodash 助手来格式化 BigNumber 值。 确保获取 Infura 令牌以设置 API_TOKEN 变量。

我们可以通过在节点上运行它并在不同的控制台中使用 curl 查询余额来测试这个脚本（见 6-7）。 确保等待几秒钟，以便脚本可以处理一些块以收集转账数据。$ curl -s "localhost:3000/balances.json" | jq .{  "0xB048...": "26000000000000000000000",  "0x58b2...": "77997707535390983471493397",  "0x352B...": "4666667000000000000000000",  "0xBC96...": "3000000000000000000000000",  ...}Listing 6-7

查询表达端点以检索令牌余额。 我们只是使用 jq^(3) 实用程序来漂亮地打印 JSON 输出

这种简单的实现利用了所有索引数据都存储在索引器实例中的事实。 请记住，对于实际部署，您将希望将所有数据存储在单独的数据存储中，例如关系数据库。 这将允许您直接向数据库运行查询，并将 Web 服务器和索引器进程解耦，使它们分开运行。 它还将允许您根据需要从客户端添加聚合、过滤器、排序和分页：在单个请求中返回五十万个代币持有者的列表在某些情况下可能不太好。

### 处理链重组

到目前为止，我们通过仅处理可以被视为已完成的转账来避免链重组的问题，换句话说，那些发生在足够多区块之前的转账，以至于这些区块被从链上移除的机会可以忽略不计。 现在我们将取消此限制，并查看如何通过正确地对重组做出反应来安全处理最新的事件。

#### 使用订阅

检测和对抗链重组的最简单方法是通过订阅。 对事件的订阅，例如 ERC20 转账，不仅会实时推送新事件到我们的流程中，还会通知任何因重组而*移除*的事件。 这意味着我们可以编写我们的 reduceEvent 函数的对应部分以撤销一个事件，并在以太坊节点推送事件移除时运行它（见列表 6-8）。// 01-indexing/subs-indexer.jsundoTransfer(event) {  const { from, to, value } = event.returnValues;  if (from !== ZERO_ADDRESS) {    this.balances[from] = this.balances[from].plus(value);  }  if (to !== ZERO_ADDRESS) {    this.balances[to] = this.balances[to].minus(value);  }}列表 6-8

在我们的余额列表中撤销转账事件。 这里的逻辑与 reduceEvent 方法相反

这种方式，不再依赖`getPastEvents`方法轮询新区块，而是可以简单地打开一个订阅并监听事件的添加和移除（见 6-9）。async function start() {  // 处理所有过去的区块  const currentBlock = await this.web3.eth.getBlockNumber();  await this.processBlocks(this.startBlock, currentBlock);  // 订阅新的区块  this.subscription = this.contract.events    .Transfer({ fromBlock: currentBlock + 1 })      .on('data', e => this.reduceEvent(e))      .on('changed', e => this.undoTransfer(e.returnValues))      .on('error', err => console.error("Error", err));}Listing 6-9

使用订阅来监视新事件并跟踪由于重组而删除的事件。数据处理程序在有新事件时触发，而更改处理程序在由于重组而从链中删除事件时触发

但是，这种方法有一个主要缺点。如果在重新组织发生时与节点的 websocket 连接丢失，则我们的脚本将永远不会被通知已删除的事件。这意味着我们不会回滚已撤消的转账，并最终导致无效状态。另一个问题是，订阅仅返回新事件，因此如果在`processBlocks`调用和安装订阅之间铸造任何区块，我们可能会错过一些事件。那么我们就尝试一个不同的、更简单的方法吧。我们首先需要手动检测何时发生了重组。

#### 检测重组

当链分叉聚集的累积哈希功率超过当前头部时，就会发生重组，并且该分叉将成为官方链。如果不同的矿工组在不同的分叉上工作，则可能发生这种情况。

这意味着在重组中，一个或多个区块（从当前头部开始向后）将被其他区块替换。这些新区块可能包含与以前的区块不同的交易，也可能按不同的顺序排列，^(4) 从而产生不同的结果。

通过检查区块标识符，我们可以检测到一次重组。回想一下第三章，每个区块都由其哈希标识。此哈希是从区块的数据和前一个区块的哈希计算得出的。这就是区块链的本质：每个区块都与前一个区块相连。这意味着旧区块不能更改而不强制更改所有后续区块的标识符。

这正是我们可以轻松检测到重组的原因。当给定高度的区块的哈希值发生变化时，这意味着该区块以及可能在它之前的其他区块也发生了变化。然后我们只需监视我们已处理的最新区块，如果其哈希在任何时候发生变化，我们就会向后扫描其他更改的哈希，直到我们检测到一个共同的祖先（清单 6-10）。

让我们修改我们的脚本，使用这种策略添加对重组的检查，这将要求我们跟踪我们已处理的块哈希。 // 01-indexing/reorgs-indexer.jsasync processNewBlocks() {  // 跟踪当前块号和其哈希  const currentBlockNumber =   await this.web3.eth.getBlockNumber() - CONFIRMATIONS;  const currentBlockHash =   await this.getBlockHash(currentBlockNumber);  // 检查可能的重组  if (this.lastBlockNumber && this.lastBlockHash) {    const newLastBlockHash     = await this.getBlockHash(this.lastBlockNumber);    if (this.lastBlockHash !== newLastBlockHash) {     // 发生了重组！ 撤销所有受影响的块，     // 并从未从主链中移除的最近一个重新处理块     const lastBlock = await this.undoBlocks();     this.lastBlockHash = lastBlock.hash;     this.lastBlockNumber = lastBlock.number;    }  }  // 从 lastBlockNumber 处理块直到 currentBlock  // 更新 this.lastBlockNumber 和 this.lastBlockHash  // ...}async getBlockHash(number) {  const { hash } = await this.web3.eth.getBlock(number);  return hash;}6-10

更新了 `processNewBlocks` 函数，该函数在每次迭代中检查重组。 函数 `undoBlocks`（见 6-12）应撤消所有与已移除块相关的转账，并返回未受重组影响的最新块。

请注意，我们现在不仅跟踪最新的块号，还跟踪其哈希。 每当开始新的迭代时，我们都会检查该高度处块的哈希是否更改。 如果是，则我们遇到了重组，必须撤消所有已删除块的更改。

#### 恢复更改

当检测到重组时，我们需要撤消我们从已删除块中处理的任何转账。 为此，我们首先需要跟踪在每个块上我们处理的哪些转账（见 6-11）。

我们将向我们的 Indexer 类添加一个新字段：一个堆栈，每个块我们在处理转账事件时都会看到一个项目。每个项目将保存块编号、哈希和它包含的转账列表。我们将在每次减少新事件时向其中添加新项目。

跟踪每个块的转账事件。此函数从 reduceEvent 中调用。请注意，必须按顺序调用此函数，因为正在处理新事件，以确保块列表保持排序，最新的块位于其末尾。

现在我们有了我们处理过的块列表，我们可以从末尾开始迭代它，并撤消我们在余额列表上聚合的所有转账事件。

向后遍历已处理事件的列表并撤消所有转账。该函数必须返回未在重新组织中移除的最近的区块，以便脚本可以从中重新处理链。函数 undoTransfer 类似于本章前面的订阅子节中提到的函数。

总结一下，我们已经实施的变化，使我们的脚本能够抵御重新组织的变化如下：

1.  1.

    处理转账事件时，将其区块号和哈希保存在列表中，将最近的一次添加到末尾。

1.  2.

    在检查新区块时，验证我们已处理的最新区块的哈希是否已更改。

1.  3.

    如果已更改，则撤消发生在每个更改的区块上的每个转账事件，从最近的一个开始。当我们到达一个未更改的区块时，停止。

1.  4.

    将最新的区块重置为未更改的区块，并从那里恢复处理。

虽然这些变化给我们的解决方案引入了很多复杂性，但它们确保其状态不会因重新组织而失去同步。根据您的用例，您可以选择如何处理它们：忽略最新的区块直到它们被确认，使用订阅来让节点跟踪已移除的事件，假设连接稳定，或者实施类似于这个的基于客户端的设计。

### 单元测试

到目前为止，我们忽略了软件开发的一个关键方面：测试。虽然以太坊中的测试与其他应用程序并没有实质性的不同，但我们将利用我们的索引器示例来介绍一些特定于区块链测试的有用技术。

#### 选择一个节点

第一个决定在于选择在测试中使用哪个节点。回想前面章节提到的，我们可以使用 ganache，一个区块链模拟器，或者在开发模式下运行的实际节点，比如 Geth 或 Parity。前者更轻量，并提供了额外的方法来操作区块链状态，这些方法在单元测试中非常有用。另一方面，使用实际节点将更具代表性，适合你的应用的实际生产设置。

一个很好的折衷方案是在单元测试中使用具有即时封存功能的 ganache，而在端到端集成测试中可以使用一个 Geth 或 Parity 开发节点，以固定的区块时间运行。这样可以在单元测试中获得更精细的控制，并在集成测试中提供更具代表性的环境。

### 注意

在软件开发中，单元测试是否允许调用外部服务通常是一个有争议的问题。在传统应用中，一些开发者倾向于建立一个用于支持他们的单元测试的测试数据库，而其他人则对它的所有调用进行存根处理，以便在隔离状态下测试他们的代码，他们认为单元测试必须只测试单个代码片段。在这里，我们将支持前一组，并将在我们的单元测试中连接到一个 ganache 实例。无论如何，这只是关于我们如何理解单元测试的语义问题。

#### 测试我们的索引器

我们现在将为我们的索引器编写一些单元测试。我们将使用 ganache 作为后端，mocha^(5) 作为测试运行器，并使用 chai^(6) 以及 bignumber 插件^(7) 来编写断言。

首先，我们需要为我们的索引器部署一个 ERC20 代币以进行监视（见 6-13）。我们将使用 OpenZeppelin 的默认 ERC20 实现来扩展，增加一个公共铸币方法，这样我们就可以轻松地为任何我们想要测试的地址铸造代币。

具有公共铸币方法的 ERC20 代币合约，允许任何人创建新的代币。请勿在生产中使用！

让我们为我们的测试文件创建样板代码（见 6-14）。我们需要导入所有相关组件，为与我们的 ganache 实例进行交互创建一个新的 web3 实例，并部署新的合约。

用于 Indexer 的测试套件的样板代码。它初始化一个新的 web3 实例并部署一个 ERC20 代币合约的实例。注意，为了简洁起见，一些 require 语句已被删除。

使用此模板，我们现在可以在我们的 *describe* 块内编写我们的第一个测试，以检查我们合约中铸造的任何余额是否被索引器正确拾取（见 6-15）。it('记录铸造的余额', async function () {  const indexer = new Indexer({    address: this.erc20.options.address    provider: 'http://localhost:9545'  });  const [from, holder] = this.accounts;  await this.erc20.methods.mint(holder, 1000).send({ from });  await indexer.processNewBlocks();  expect(indexer.getBalances()[holder])    .to.be.bignumber.eq("1000");});列表 6-15

用于检查从铸造中转账是否被正确处理的测试。我们为新部署的代币合约初始化一个新的 Indexer 实例，为一个地址铸造一些代币，并执行索引器以检查结果。

我们可以使用 mocha 运行此测试。确保在另一个终端上运行 ganache 实例，并监听端口 9545（见 6-16）。$ ganache-cli -p 9545$ npx mocha 列表 6-16

分别启动 ganache 实例并运行测试套件。每个命令应在不同的终端上运行。

然而，如果我们运行我们的测试，它会失败 - 索引器不会为持有人地址拾取任何余额。这是因为我们构建索引器忽略了最新区块的任何信息，并且仅在一定数量的确认后考虑转账。

我们将使用 ganache 的 *mine* 方法（见 6-17）来修复此问题。这个方法在 Geth 或 Parity 中不可用，它告诉 ganache 模拟一个新的区块被挖掘出来。它像任何其他消息一样通过低级 JSON-RPC 接口发送。function rpcSend(web3, method, ... params) {  return require('util')    .promisify(web3.currentProvider.send)    .call(web3.currentProvider, {      jsonrpc: "2.0", method, params    });}function mineBlocks(web3, number) {  return Promise.all(    Array.from({ length: number }, () => (      rpcSend(web3, "evm_mine")    ))  );}列表 6-17

辅助方法指示 ganache 开采一定数量的区块。 `mineBlocks` 中的代码并行触发了一定数量的请求，当所有请求都成功时返回。

我们现在可以在我们的测试中，在指示索引器处理新区块之前，添加一次调用 `mineBlocks`，再次运行它，并看到它通过。

#### 使用快照

我们现在可以编写更多测试来测试我们索引器的其他场景。然而，在任何良好的测试套件中，所有测试都应该相互独立，但这里并非如此，因为我们部署了我们 ERC20 合约的单个实例。这意味着测试中发生的任何铸币或转账都将传递到后续的测试中。

显而易见的解决方案是将我们的 `before` 步骤替换为 `beforeEach` 步骤，^(8) 这样每个测试都会部署一个新的 ERC20，但我们将利用这个机会引入 ganache 特有的一个新概念：快照（见清单 6-18）。快照允许我们保存模拟区块链的当前状态，运行一组操作，然后回滚到保存的状态。函数 `takeSnapshot(web3)` {  return rpcSend(web3, "evm_snapshot").then(r => r.result);}函数 `revertToSnapshot(web3, id)` {  return rpcSend(web3, "evm_revert", id);}清单 6-18

用于获取新快照的辅助函数，返回快照 id，并用于根据快照 id 回滚到特定快照的辅助函数

快照的一个很好的用例是通过消除为每个测试重新创建新状态的需求来节省时间（见 6-19）。我们不需要在每个测试中部署新的 ERC20 合约，而是只需部署一次，保存一个快照，执行一个测试，然后在运行下一个测试之前恢复快照以清除任何更改。虽然这不会在我们的测试中提供任何性能改进，但是对于需要创建多个合约的更复杂设置的测试套件来说，将受益匪浅。

在每次测试之前都会创建一个新的快照，并在测试结束后恢复到该快照。请注意，我们不能多次恢复到同一个快照，因此我们需要为每个测试创建一个新的快照。

快照的另一个有趣的用例是测试*重组*。在常规的 Geth 或 Parity 节点上触发重组是复杂的，因为它涉及设置我们自己的私有节点网络，并断开和重新连接节点以模拟链分裂。另一方面，在 ganache 上测试重组要简单得多：我们可以拍摄一个快照，挖掘几个区块，然后回滚并挖掘另一组带有不同交易集的区块。

### 注意

这不等同于实际的链重组，因为订阅不会报告任何*移除*事件。尽管如此，由于我们的索引器依赖于普通轮询来检测任何更改，因此在这种情况下使用快照就足够了。

让我们编写一个测试，检查我们的索引器是否正确处理链重组，通过撤消删除的块的任何余额更改并处理新块。it('handles reorganizations', async function () {  // 设置一个新的索引器  const indexer = new Indexer({    address: this.erc20.options.address,    provider: 'http://localhost:9545'  });  // 为发送者帐户铸造余额并拍摄快照  const [from, sender, r1, r2] = this.accounts;  await this.erc20.methods.mint(sender, 1000).send({ from });  const snapshotId = await takeSnapshot(web3);  // 将 200 个代币转移到 r1 和 r2，然后确认挖掘  const transfer = this.erc20.methods.transfer;  await transfer(r1, 200).send({ from: sender });  await transfer(r2, 200).send({ from: sender });  await mineBlocks(web3, 12);  // 运行索引器并断言它们被拾取  await this.indexer.processNewBlocks();  const balances = this.indexer.getBalances();  expect(balances[sender]).to.be.bignumber.eq("600");  expect(balances[r1]).to.be.bignumber.eq("200");  expect(balances[r2]).to.be.bignumber.eq("200");  // 回滚以模拟重组并发送新的转账  await revertToSnapshot(web3, snapshotId);  await transfer(r1, 300).send({ from: sender });  await mineBlocks(web3, 15);  // 检查旧状态是否被丢弃  await this.indexer.processNewBlocks();  const newBalances = this.indexer.getBalances();  expect(newBalances[sender]).to.be.bignumber.eq("700");  expect(newBalances[r1]).to.be.bignumber.eq("300");  expect(newBalances[r2]).to.be.bignumber.eq("0");});

### 注意

这些测试技术不仅可用于测试与智能合约交互的组件，还可用于测试智能合约本身。在部署到网络的任何代码中都保持良好的测试覆盖率是一个良好的实践，特别是考虑到您以后可能无法修改它（在大多数情况下^(9)）以修复任何错误。

### 关于中心化的说明

在本书中，我们首次为我们的应用引入了一个服务器端组件。我们不仅构建了一个仅客户端的应用，直接连接到区块链，现在我们还有一个新的中心化依赖项，必须使我们的应用程序运行。可以认为我们的应用程序因此不再符合去中心化应用程序的条件，因为它盲目地信任由单个团队运行的服务器返回的数据。

根据查询的数据类型不同，这个问题可以通过让客户端 *验证* 服务器提供的部分数据来缓解。以 ERC20 余额示例为例，客户端可以从索引服务器请求一个代币的前 10 个持有者，然后对比区块链以确认他们的余额是否正确。它们可能仍然不是前 10 个持有者 - 但至少客户端可以保证余额没有被篡改。

然而，这并不是解决问题的方法，因为并非所有数据都可以针对区块链进行验证而无需重新查询所有事件。此外，我们的应用程序现在依赖于一个随时可能关闭的组件，使其无法使用。

让我们讨论两种不同的解决方案。即将进行的讨论不仅适用于索引，还适用于任何其他链下服务，如存储或密集计算。

#### 去中心化服务

解决这个问题的一种方法是寻找 *去中心化* 的链下解决方案。例如，在撰写本文时，一种名为 *EthQL* 的区块链数据 GraphQL 接口正在审核中。这可以作为所有以太坊节点的标准接口的一部分添加，从而允许任何客户端更轻松地查询事件。另一个例子是 thegraph，这是一个为不同协议提供定制的 GraphQL 模式的项目。他们依赖于一个令牌激励的去中心化节点网络，这些节点保持这些模式的最新状态并回答用户的任何查询。

尽管优雅，这些分散化解决方案可能还没有为所有用例做好准备。分散化的索引或计算解决方案仍在设计中。即使准备就绪，通用的分散解决方案也可能不总是满足你的应用程序的特定需求。考虑到这一点，我们将讨论第二种方法。

#### 中心化应用程序

解决这个问题的一个明显的非解决方案是接受应用程序*可以是中心化的*。这可能是一个有争议的声明，因为在整本书中都强调了分散式应用程序，但实际上并非如此。

可以说，基于区块链的系统的强大之处不在于应用程序，而在于协议层。通过依赖链作为最终真相的来源，并构建在其上运行的开放协议，任何开发者都可以自由地构建一个与这些协议进行交互的应用程序。这使得用户可以在共同的分散式协议层中移动不同的充当其数据*入口*的应用程序之间。分散化随之被理解为能够随时收拾起来离开，同时保留所有数据和网络效应的自由，这些效应来自共享的分散化层。

这个理由赋予我们作为开发者在应用层构建尽可能强大的解决方案的自由，通过利用任意数量的中心化组件进行查询、存储、计算或任何其他可能需要的服务。这些解决方案有可能提供比完全分散的解决方案更丰富的用户体验。

你可以想象，中心化是以太坊开发社区中一个有争议的问题。对于这个话题，没有对与错的答案，讨论可能会随着时间不断发展。无论你采取什么样的方法，一定要理解其利弊，并将其与你要构建的解决方案的需求进行权衡。

## 存储

现在我们将关注以太坊的另一个问题：存储。在以太坊区块链上存储数据非常昂贵，每字节消耗 625 gas（四舍五入到 32 字节槽位），再加上每个非零字节的基础 68 gas，仅用于将数据发送到区块链。以 1GWei 的 gas 价格计算，这意味着存储一个 100kb 的 PNG 将花费约 0.07 ETH。另一方面，为了链下访问而将数据保存在日志中要便宜得多，每字节消耗 8 gas 单位，再加上发送数据的基础 68 gas（这相当于我们样本图像成本的十分之一），但随着规模扩大，这仍然昂贵。这意味着我们需要寻找存储大型应用数据的替代解决方案。

### 链下存储

我们将采用类似于我们用于索引的方法，建立一个提供存储能力的单独的集中式服务器。我们不会将实际数据存储在区块链上，而是存储可以从中检索数据的 URL。当然，这种方法仅适用于不需要用于合约执行逻辑的数据，而是用于链下目的的数据 - 例如显示与资产关联的图像。

除了 URL 之外，我们还应该存储存储数据的哈希值。这使得检索该信息的任何客户端都能够验证存储服务器没有篡改数据。尽管由于存储服务器崩溃而导致数据无法访问，但哈希值保证了任何客户端可以检查提供的数据是否正确。换句话说，**通过将数据移到链下，我们可能会牺牲数据的可用性，但不会牺牲数据的完整性**。

我们将从上一章节中的 ERC721 铸币应用程序继续作为一个示例用例，以说明如何实现此功能，并在链下站点存储与每个代币相关的元数据（如名称和描述）。

#### ERC721 元数据扩展

在我们进入实现之前，我们将简要回顾 ERC721 标准的一个扩展：元数据扩展（见列表 6-20）。这个扩展规定每个代币都有一个相关的 *token URI*，其中包含其元数据。这个 URI 可以是一个 HTTP URL，其中包含一个 JSON 文档，其中包含每个代币的信息。这些元数据可以是规范名称、一些描述文本、标签、作者信息、图像或与可收藏品领域特定的任何其他字段。函数 tokenURI(uint256 tokenId)  外部视图返回（字符串记忆）；列表 6-20

ERC721 元数据扩展所需的 tokenURI 方法规范

我们将扩展我们的 ERC721 合约（见列表 6-21），包括 openzeppelin-solidity@2.2.0 包提供的 ERC721Metadata 基础合约，它跟踪每个代币的 URI。// 02-storage/contracts/ERC721PayPerMint.solpragma solidity ⁰.5.0;// 导入 SafeMath、ERC721、ERC721Enumerable、ERC721Metadatacontract ERC721PayPerMint  是 ERC721、ERC721Enumerable、**ERC721Metadata** 使用 SafeMath for uint256;  构造函数() 公共 ERC721Metadata("PayPerMint", "PPM") { }  function exists(uint256 id) 公共视图返回（布尔值） {    返回 _exists(id);  }  function mint(    地址 到, uint256 tokenId, **字符串内存 tokenURI**  ) 公共付费返回（布尔值） {    要求(msg.value >= tokenId.mul(1e12));    _mint(to, tokenId);    **_setTokenURI**(tokenId, tokenURI);    返回 true;  }}列表 6-21

更新的 ERC721 合约，在铸造代币时接受一个相关的 tokenURI。回顾一下，这个合约要求支付与代币 ID 成比例的 ETH 金额，以供娱乐和盈利之用

让我们修改我们的应用程序，将元数据保存在存储服务器中，并将包含数据的 URL 添加到代币合约中，以及内容哈希。

#### 保存代币元数据

我们将修改我们的主要铸币方法，在 ERC721 组件中，以便它不仅接受 ID，还接受标题和描述字符串字段（见 6-22）。我们将保存此数据离线，获取一个 URL，并将其传递给以下合同 *铸币* 调用。// 02-storage/src/components/ERC721.jsasync mint({ id, **title, description** }) {  const { contract, owner } = this.props;  const data = JSON.stringify({ id, **title, description** });  **const url = await save(data);**  const value = new BigNumber(id).shiftedBy(12).toString(10);  const gasPrice = await getGasPrice();  const gas = await contract.methods    .mint(owner, id, **url**).estimateGas({ value, from: owner });  contract.methods.mint(owner, id, **url**)    .send({ value, gas, gasPrice, from: owner })    .on('transactionHash', () => {      this.addToken(id, **{ title, description }**);    })}Listing 6-22

更新了铸币方法以处理令牌元数据。请注意，这还需要修改铸币组件，添加标题和描述输入，以便用户可以提供这些值。

保存功能将计算数据的哈希值，将其用作标识符，并将其存储在存储服务器中（见 6-23）。请注意，通过使用哈希作为标识符，^(12) 任何客户端都可以验证检索到的数据是否已被篡改。// 02-storage/src/storage/local.jsimport { createHash } from 'crypto';const server = 'http://localhost:3010';export async function save(data) {  let hash = createHash('sha256').update(data).digest('hex');  let url = `${server}/${hash}`;  await fetch(url, {    method: 'POST', mode: 'cors', body: data,    headers: { "Content-Type": "application/json" }  });  return url;}Listing 6-23

将数据保存到本地存储服务器，使用数据哈希作为标识符

在这个例子中，接收 POST 请求的服务器是一个 NodeJS 进程，它将在 URL 路径接受任意 JSON 数据，将其保存在本地文件中，然后在收到 GET 请求时提供服务。在实际应用中，您可能希望依赖真实的存储服务。

现在我们可以在初始加载时加载令牌的元数据（见清单 6-24）。当主要组件加载并且已检索到现有令牌列表后，我们将调用一个新的 loadTokensData 函数。// 02-storage/src/components/ERC721.jsloadTokensData(tokens) {  const { contract } = this.props;  tokens.forEach(async ({ id }) => {    // 从合同中检索元数据 URL    const url = await contract.methods.tokenURI(id).call();    // 从 URL 检索数据    const data = await fetch(url)      .then(res => res.json()).catch(() => "");    // 验证数据完整性并更新状态    const hash = createHash('sha256')      .update(JSON.stringify(data)).digest('hex');    const path = new URL(url).pathname.slice(1);    if (path === hash) this.setTokenData(id, data);  });}清单 6-24

循环遍历所有当前代币，并通过查询合同来检索存储它的 URL，然后检索实际元数据的 URL，加载它们的元数据。

请注意，在接受元数据之前，会通过计算其哈希来验证其完整性。您可以通过修改本地文件系统中保存的元数据（查看项目中的 server/data 文件夹）来进行测试，并检查是否未显示修改后的令牌的任何元数据。

这使我们能够在铸造每个非同质化代币时关联附加数据，该数据实际上可以被显示代币信息的任何应用程序所利用。在这方面，您可以将代币元数据视为常规 HTML 页面的 opengraph 元数据^(13) 的等价物。

### 行星间存储

作为集中式存储解决方案的替代，我们可以将数据存储在*星际文件系统*（IPFS）中。IPFS 是“用于存储和访问文件、网站、应用程序和数据的分布式系统。”^(14) 换句话说，它充当了分散式存储系统。

#### IPFS 是什么？

IPFS 作为一种点对点内容分发系统。任何节点都可以加入网络，从专用的 IPFS 服务器到家用电脑上的普通用户。每当用户从网络请求文件时，该文件将从最近的具有文件的节点下载，并且可以从这个新位置供其他用户下载。一段内容的可用性取决于是否有足够的用户愿意存储相关文件。

在 IPFS 中，任何数据单元都不是通过其位置来识别，正如大多数传统文件系统那样，而是通过其内容来识别。当从 IPFS 网络请求文件时，您通过其标识符来寻址，这不过就是内容的哈希。这确保了所有内容的完整性，因为客户端将根据其标识符验证接收到的所有内容。这也允许客户端请求文件而无需知道它在网络中的*位置*。

这意味着 IPFS 中的内容是不可变的。对其进行的任何更改都需要将其完全存储为新标识符下的新副本。只要有人保留其副本，先前的文件将被网络保留。

所有这些特性使得 IPFS 与区块链应用程序非常匹配。我们在前一节手动构建的内容哈希验证已经被协议本身提供。通过在智能合约中索引内容标识符而不是其位置，我们可以将区块链数据与任何集中式内容提供者解耦。

### 注意

IPFS 依赖于愿意保存和共享内容的用户的可用性，这可能使其看起来不适合构建关键应用程序。尽管如此，您的应用程序的数据可用性可以通过依赖 IPFS 固定服务来提供。这些服务充当传统存储服务器，但通过使 *您的* 内容对所有用户可用来参与 IPFS 网络 - 当然需要付费。

#### 在我们的应用程序中使用 IPFS

要在我们的应用程序中启用 IPFS 支持，我们首先需要连接到一个 IPFS 节点。这类似于连接到以太坊节点以访问以太坊网络，不同之处在于我们不需要私钥或货币来将任何数据写入 IPFS。

我们可以将我们自己的 IPFS 公共节点作为应用程序的一部分进行托管，也可以依赖第三方提供商。例如，Infura 不仅提供以太坊公共节点，还提供 IPFS 节点，这意味着我们可以直接使用它们的 IPFS 网关。

但是，也有可能用户在他们的计算机上运行自己的 IPFS 节点。IPFS 提供了一个浏览器扩展程序，即 IPFS companion，连接到本地节点并使浏览器启用了 IPFS。这包括添加对 ipfs 链接的支持，并在所有站点的全局窗口对象中注入一个 ipfs 对象 - 就像 Metamask 在所有站点上添加了一个以太坊提供者对象一样。

### 注意

还有一个选项，就是在 *您自己的网站* 中运行 IPFS 节点。js-ipfs 库提供了整个 IPFS 协议的浏览器兼容实现，因此您可以在用户访问您的应用程序时启动一个 IPFS 守护程序。然而，这可能会使您的应用程序变得更加沉重，并且应用内的 IPFS 进程不像专用进程稳定。因此，与网络交互的建议方法是使用 IPFS HTTP API 连接到单独的节点。

在我们的应用中打开一个 IPFS 连接与打开以太坊连接非常相似：首先检查是否有全局连接对象可用，如果不是，回退到一个众所周知的公共节点（列表 6-25）。我们将使用 ipfs-http-client@30.1 javascript 库来访问网络，这是 web3.js 的 IPFS 等效库。// 02-storage/src/storage/ipfs.js 导入 ipfsClient 'ipfs-http-client';异步功能 getClient() { 如果 (window.ipfs && window.ipfs.enable) { 返回 await window.ipfs.enable({ 命令：['id', '版本', '添加', '得到'] }); } else { 返回 ipfsClient({ 主机：'ipfs.infura.io', 端口：'5001', 协议：'https'，'api-path'：'/api/v0/' }); }}清单 6-25

创建一个新的 ipfs 客户端实例。首先，我们检查通过伴生扩展注入的全局对象是否可用。如果不可用，我们将回退到连接到 Infura IPFS 网关。

使用这个新的 IPFS 客户端，我们现在可以很容易地将我们的令牌元数据保存到 IPFS 网络而不是中心化服务器。导出异步功能保存数据 { const ipfs = await getClient(); const [result] = await ipfs.add(Buffer.from(data)); return `/ipfs/${result.path}`; }从 IPFS 网络中取回结果给定 URL 也很简单。请注意，我们不再需要验证其完整性，因为协议会自动处理。导出异步功能加载 URL { const ipfs = await getClient(); const [result] = await ipfs.get(url); return JSON.parse(result.content.toString()); }

#### 在 IPFS 上托管我们的应用

IPFS 不仅可用于存储我们的应用数据，还可以存储应用本身，以实现最大程度的分权化。我们应用的客户端代码可以上传到 IPFS 并从那里提供。但用户如何能在普通浏览器中访问它？或者在不必指定哈希的情况下对其进行定址？

第一个问题可以通过 IPFS 网关解决（参见列表 6-26 中的示例）。IPFS 网关是一个普通的网站，用于从 IPFS 网络提供内容。它允许您访问任何 IPFS 项目的路径`/ipfs/CID`，其中 CID 是在网络上标识每个对象的内容哈希。https://**gateway.ipfs.io**/ipfs/QmeYYwD4y4DgVVdAzhT7wW5vrvmbKPQj8wcV2pAzjbj886/https://**ipfs.infura.io**/ipfs/QmeYYwD4y4DgVVdAzhT7wW5vrvmbKPQj8wcV2pAzjbj886/https://**cloudflare-ipfs.com**/ipfs/QmeYYwD4y4DgVVdAzhT7wW5vrvmbKPQj8wcV2pAzjbj886/列表 6-26

您可以直接通过列出的任何公共网关在浏览器中访问以下地址的 ipfs.io 网站的旧版本。由于内容的 ID 是其哈希值，您可以确信所有网关将提供完全相同的对象。

第二个问题，为 IPFS 站点提供用户友好的名称，可以使用*DNSLink*解决。DNSLink 是一种通过 DNS TXT 记录将 DNS 名称映射到 IPFS 内容的过程。

假设我们想将我们的站点在 IPFS 中映射到`example.com`域。通过在`_dnslink.example.com`添加一个 TXT 记录，并将值设置为`dnslink=/ipfs/CID`，任何 IPFS 网关都将自动将任何请求映射到`/ipfs/example.com`到指定的内容。

不仅如此，我们还可以为我们的域指定一个 CNAME DNS 记录，指向一个网关。这使我们可以自动在`example.com`直接从 IPFS 指定的网关中提供我们的页面。^(16) 总之，访问我们站点的完整过程将是

+   用户向`example.com`发出请求。

+   DNS 查询回答带有指向`gateway.ipfs.io`的 CNAME。

+   用户使用`example.com`作为主机头向`gateway.ipfs.io`的 IP 发出请求。

+   网关对`example.com`和`_dnslink.example.com`进行 DNS TXT 查询，并获取 IPFS CID 作为响应。

+   网关透明地向终端用户提供来自 IPFS 的内容。

通过依赖*IPNS*（InterPlanetary Name System），可以引入另一级间接性。该系统允许您拥有可变链接，这些链接指向 IPFS 内容，尽管 IPNS 链接也是哈希值。然后，您可以让您的 DNSLink 指向您的 IPNS 名称，而不是 IPFS ID，并通过仅更新 IPNS 链接到内容的新版本来更新您的站点。这样一来，您就无需在部署站点的新版本时修改 DNS TXT 记录。

## 摘要

在构建非平凡的以太坊应用程序时，我们遇到了两个问题：如何在链上数据上执行复杂查询，以及如何存储大量数据。这两个问题都需要查看以太坊之外的内容，并依赖其他服务，无论是集中式的还是去中心化的。我们还研究了如何编写与以太坊网络交互的单元测试，并处理链的重新组织的一些策略。

除了本章详细介绍的特定问题或策略之外，或许最重要的要点是定义您的应用程序对*去中心化*的需求。虽然我们习惯于传统的非功能性需求，如性能、安全性或可用性，但区块链应用程序也需要考虑去中心化。去中心化是区块链首先被使用的核心原因，因此特别重视它是有意义的。

像其他非功能性需求一样，去中心化不是二元的。我们的应用程序可以具有不同程度的去中心化，这取决于堆栈中的哪些组件是集中化的，我们对商业第三方和点对点网络之间的信任程度有多少，或者我们的用户对自己的数据有多少控制权。

例如，一个金融应用程序可以是纯粹的集中式，除了管理用户资产的基础协议之外，允许高性能和良好的用户体验，同时确保其用户随时都可以与他们的资产分开。另一方面，一个专注于绕过审查的应用程序可能需要是纯粹的去中心化，以免因其托管提供商而面临被关闭的风险。

不同的应用程序会有不同的需求。重要的是你明确自己的需求，这样你就知道你可以访问哪些解决方案，并相应地构建你的应用程序架构。
