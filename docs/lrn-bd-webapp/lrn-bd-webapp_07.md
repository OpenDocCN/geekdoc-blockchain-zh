© Santiago Palladino 2019 S. Palladino《面向 Web 开发人员的以太坊》[`doi.org/10.1007/978-1-4842-5278-9_7`](https://doi.org/10.1007/978-1-4842-5278-9_7)

# 7. 用户入门

Santiago Palladino（1）阿根廷布宜诺斯艾利斯自治城

复杂的用户入门体验是以太坊实现大规模采用的主要问题之一。对于新手用户来说，需要安装专用浏览器或扩展程序，创建并备份帐户，然后才能开始与 DApp 进行交互。尽管在之前的章节中我们已经与启用了 web3 的用户合作过，但在本章中，我们将探讨简化新用户入门体验的方法。

我们将从探讨与区块链进行交互的场景开始，而无需创建帐户或在幕后为我们的用户创建帐户。我们将进一步将帐户管理本身移至区块链，并在此过程中探讨合约升级性。然后，我们将把重点转移到与以太坊交互需要 ETH 的问题上，并介绍无需您的用户支付 gas 费用的无 gas 交易技术。最后，我们将回顾以太坊命名系统，该系统将原始地址隐藏在用户友好的名称后面，使其更易于您的用户访问。

## 问题

试着回忆一下您在使用基于以太坊的应用程序时的第一步是什么。第一步可能是获取 ETH 来为您的交易提供动力。如果您没有幸运地被人赠送加密货币，这需要在交易所注册并可能需要验证您的帐户。根据交易所的不同，有时甚至需要上传一张拿着您的护照或水电费账单的自拍照来证明您的地址。一旦被列入白名单，您需要以老式的方式，例如通过银行汇款，将资金发送到交易所以获取您的 ETH。

下一步是将您的资金从交易所转移到您控制的账户中。经过对硬件、移动、桌面和在线钱包的仔细研究，您可以选择一个并实际创建您的账户。无论您选择了哪种钱包，都需要写下一组 12 个随机单词并将它们放在一个安全的地方 - 但不要太安全，因为丢失它们意味着丢失您唯一的备份，从而丢失您所有的加密货币。选择了钱包的密码后（但您刚刚不是为了安全性而写下了 12 个单词吗？），最后您会被呈现出您的公共地址，可以将您的资金从交易所转移到您的控制之下。

拥有资金的账户后，您现在打开浏览器去一个 DApp 中尝试它。但是，遗憾的是，该网站找不到 web3 提供程序，并要求您安装一个专用的浏览器扩展程序（例如 Metamask）或使用一个支持 web3 的浏览器（如 Opera）来进行交互。在这样做之后，您需要决定是否信任这个新组件来处理您的 12 个单词 - 这些单词应该被保持非常安全，将它们输入您刚刚下载的浏览器扩展程序是一个好主意吗？ - 还是设置另一个新账户。如果您选择了后者，您需要再次经历同样的备份过程，通过 12 个单词选择一个密码，写下新账户，并将您的 ETH 转移到其中。

完成这些步骤后，您现在终于可以发送您的第一笔交易，并从您喜爱的去中心化商店购买数字收藏品加密帽。万岁。

现在，如果您正在阅读本书，您很可能是一名程序员，并且善于解决技术挑战。虽然设置自己的账户可能会很麻烦，但它带来了成为去中心化革命先锋的激动。

但想象一下您的普通用户的立场，如果页面加载超过几秒钟，他们会直接关闭页面。大多数用户要求立即得到满足，要求他们经历如此复杂的过程才能开始使用您的应用程序，这是一场灾难。

尽管不总是可能删除所有前面所需的步骤，但肯定可以对用户隐藏其中一些步骤，或者延迟这些步骤直到他们在你的应用程序中参与到足够程度，愿意投入几分钟时间来*进入下一个层次*。我们将在本章中审查一些实现这一目标的技术。但要注意，对于这个问题并没有万能的解决方案。

## 不需要账户交互

我们将从设置账户的任务开始——这涉及选择钱包、写下助记词、设置密码等等。解决这些步骤的最简单方法是，您的应用程序根本*不需要任何账户*来与之交互。虽然这并不适用于所有情况，但可以进行调整以涵盖比您期望的更多的情况。

### 从交易所发送资金

使用这种方法开始的最简单的情景就是在一个地址接收普通的 ETH。例如，一个捐赠应用程序只需要列出一个支付地址，用户可以直接从交易所或他们控制的任何钱包发送普通交易，而无需强制他们使用支持 web3 的浏览器。某些服务甚至提供可嵌入的小部件，您可以将其集成到您的应用程序中，这样用户可以使用法定货币购买他们需要的 ETH，甚至无需离开您的网站。

#### 普通交易和回退函数

对于用户来说，只是发送以太币是最简单的操作（图 7-1）。所列的接收地址可以是一个外部拥有账户，也可以是一个在每次转账时执行一些简单处理的智能合约。![../images/476252_1_En_7_Chapter/476252_1_En_7_Fig1_HTML.jpg](img/476252_1_En_7_Fig1_HTML.jpg)

图 7-1

捐赠账户用于 ethereum.org。这个地址可能在这个截图被拍摄之后已经发生了变化，所以在检查原始来源 [www.ethereum.org/donate](http://www.ethereum.org/donate) 之前，请不要向它发送任何资金。

### 注意

请记住，交易所不会为每个用户或交易生成唯一的以太坊地址。这意味着你不能依赖于 msg.sender 在你的合约中尝试识别用户以触发交易，如果你期望你的用户直接从交易所发送资金。

请记住，每当一个合约接收到资金的普通转账时，回退函数就会被执行，这意味着你实际上可以通过某种操作对转账做出反应。特别是，你可以依赖于发送的 ETH 的确切金额。然而，一些交易所只会以最少的 gas 发送转账，所以可能无法对 ETH 转账作出复杂的响应。

### 注意

一个未能为其转账设置合理的 gas 限制的交易所实际上是可以被利用的。正如 Chris Whinfrey 和其他人在漏洞“未能适当设置 gasLimit 可滥用”^(1) 中所描述的那样：“许多交易所允许将以太币提取到任意地址而没有 gas 使用限制。由于将以太币发送到合约地址会执行其回退函数，攻击者可以让这些交易所为任意计算付费。这允许攻击者迫使交易所在高交易成本上烧毁自己的以太币。” 所有交易所都应该为他们的出站交易设置严格的 gas 限制。

#### 转发合约

允许用户在其贡献中发送额外信息的一个巧妙技巧是设置几个充当转发代理的合约，并将某些函数执行为它们的回退函数的主合约。虽然这不允许发送任意数据，但它允许运行预定义的一组函数。

举例来说，假设我们有一个合约，用于接受两个竞争方（A 和 B）的资金。这样的合约的一个简单实现可能看起来像 7-1 中的列表所示。

为接受两方其中之一的捐款的合约的示例实现。用户在发送资金时必须调用 donateA 或 donateB 中的一个。

就目前而言，这个合约要求您的用户在每次转账时指定他们是为 A 还是 B 捐款 - 从低层次来看，这意味着要求他们添加对 donateA 或 donateB 调用的数据。请记住，使用 web3js 可以轻松生成这些数据，给定合约的 ABI（见 7-2 中的列表）。> let donations = new web3.eth.Contract(DonationsABI)> donations.methods.donateA().encodeABI()0x63420a5c

获取给定其 ABI 的 Donations 合约的 donateA 方法的交易的数据组件。

然而，要求用户在其转账中包含任意十六进制字符串可能会成为一个问题，因为大多数交易所不支持在其提款中包含数据。而对于常规钱包来说，包含数据通常被呈现为一项高级功能（见图 7-2）。![../images/476252_1_En_7_Chapter/476252_1_En_7_Fig2_HTML.jpg](img/476252_1_En_7_Fig2_HTML.jpg)

图 7-2

来自 myetherwallet.com 的发送 ETH 对话框，一个在线钱包。请注意，包含数据的选项位于高级部分下， 默认情况下隐藏。

一个更好的替代方案是，随主要合约一起部署两个小合约，其唯一目的是将每个调用转发到 donateA 或 donateB 函数（见清单 7-3）。这样，用户只需要将他们的资金发送到 DonateA 或 DonateB 的两个地址中的一个，就能将他们的贡献发送给他们选择的一方，实际上*通过只将 ETH 移动到某个地址来执行两个函数之一*。 // 01-forwarding-contracts/contracts/DonateA.solcontract DonateA {  Donations donations;  constructor(Donations _donations) public {    donations = _donations;  }  **function() external payable {**    **donations.donateA.value(msg.value)();**  **}**}清单 7-3

一个样本 DonateA 合约，通过调用 donateA 将所有转账转发到主要的 Donations 合约。 DonateB 的代码是等效的。

### 单次使用地址

正如我们刚刚看到的，让用户直接从交易所将 ETH 转移到智能合约具有几个限制：

+   不能依赖 msg.sender，因为交易所可能对多个提款使用相同的地址，或者对同一用户使用不同的地址。

+   交易中包含的气体可能不足以执行计算密集型操作，甚至写入存储。

+   转账中不能包含数据。

拥有自己钱包的用户不会面临这些问题，因为他们持有自己账户的资金，可以从中发送任意的交易。尽管我们可以即时为用户创建一个账户（正如我们将在本章后面看到的那样），但是有一个更简单的解决方案适用于短暂的交互：*单次使用地址。*^(2) 这些是外部拥有的地址，在它们的生命周期内只能发出一个预定义的交易。在执行该交易之后，该地址将无法再次使用。

#### 如何使用单次使用地址

单次使用地址可以作为一个中间账户，接收来自交易所的资金并用于执行预定义的操作。这样的操作可以设置尽可能高的 gas 限额，并包含任意数据。用户流程如下：

1.  1.

    用户在应用程序中选择要执行的操作，包括任意数据、要转移的资金或要使用的 gas。

1.  2.

    生成只能执行该交易的单次使用地址。

1.  3.

    用户将资金从交易所发送到该单次使用地址。

1.  4.

    一旦资金到账，交易就会执行。

注意，如果单次使用地址的交易因任何原因失败（无论是合约中的失败要求还是缺乏 gas），都无法发出具有必要修复的第二个交易。这意味着用户在步骤 3 中发送的任何资金将永远被锁定。因此，请确保在交易可能因状态变化而失败时避免使用单次使用地址。  

举例来说，前一节中的捐赠合约就不是一个好选择，因为接受捐赠的时间有限。用户可能在捐款开放时设置他们的单次使用地址，但如果他们在关闭后再发起，那么他们的资金将被锁定。

单次使用地址的另一个陷阱是它们必须用于其执行所需的精确数量的 ETH 进行资金化。发送到地址的任何额外资金都将永远丢失。确保向用户清楚地传达这一点！

#### 创建一次性地址

如何创建一次性地址？值得注意的是，它们并不是特殊的以太坊构造，而是巧妙的黑客结果。此外，创建它们根本不需要初始 gas。

从前面的章节中可以回顾到，为了使以太坊的所有交易有效，它们都需要用发送者的私钥签名。然后可以从交易的签名中派生出发送者的地址，因此“from”实际上从未包含在交易的数据中 - 只有在需要时才会从签名中计算出来。

总结一下，发送交易包括以下步骤：

1.  1.

    将交易参数（收件人、gas、gas 价格、nonce、数据、价值等）打包到一个二进制对象中。

1.  2.

    对交易二进制进行哈希处理，并使用发送者的私钥对其进行签名。

1.  3.

    广播交易的二进制和签名。

另一方面，处理交易包括以下步骤：

1.  4.

    计算交易二进制的哈希值。

1.  5.

    从哈希和签名中派生出发送者的地址（即“from”）。

1.  6.

    将交易二进制解包成其参数（收件人、gas、gas 价格、nonce、数据、价值等）。

生成一次性地址的技巧在于在交易中发送一个随机签名。我们在第 2 步中不实际对交易进行签名，而是在第 3 步中只包含一组随机字节作为签名。这样，该过程就没有与之关联的私钥。

在处理交易时，这将导致从签名派生的随机发送者地址。鉴于与此地址关联的私钥是未知的，因此无法为同一地址生成任何其他交易。这有效地产生了一个只能广播一个特定交易的一次性地址。然后，一旦地址被 ETH 充值，gas 费用就可以支付，交易就可以广播到网络中。

#### 示例代码

我们将使用前一节中的捐赠示例的变体，其中只有一个受益人和一个 donate 方法，该方法接受要在每次捐赠时与事件一起发出的字符串（见 7-4）。然后，我们将依靠一次性地址与之交互。// 02-single-use-addresses/contracts/Donations.solcontract Donations {  address payable wallet;  event Donation(uint256 value, string text);  constructor(address payable _wallet) public {    wallet = _wallet;  }  **function donate(string calldata text) external payable {**    **require(msg.value > 0);**    **emit Donation(msg.value, text);**  **}**  function withdraw() external { ... }}Listing 7-4

接受自定义字符串的简化捐赠合约，该字符串在每次捐赠时作为事件发出

让我们假设我们的用户想要发送 1 ETH 的捐赠，并附带传统的“Hello world”。我们首先需要生成执行该函数的编码数据，并估算执行调用的 gas 成本。// 02-single-use-addresses/index.jslet donations = new web3.eth.Contract(abi, address);let call = donations.methods.donate("Hello world");let data = call.encodeABI();let gas = await call.estimateGas({ value: 1e18 });

### 注意

请记住，实际的燃气使用量可能会因交易执行时的状态而改变。由于单次使用地址的性质，如果交易因燃气不足而失败，就无法再次使用更高的燃气允许量执行。这将导致用户资金永远锁定在地址中。如果您的功能将来可能会消耗更多的燃气，请在构建即将进行的步骤中的交易对象时考虑这一点。

我们现在拥有了构建具有随机签名的交易所需的所有参数。为了构建此交易对象，我们将使用 ethereumjs-tx@1.3.7 库。const Tx = require('ethereumjs-tx');let tx = new Tx({  value: 1e18,  data,  gas,  gasPrice: 1e9,  to: address,  nonce: "0x0",  v: networkId * 2 + 35,  s: '0x' + '2'.repeat(61),  r: '0x' + '3'.repeat(61)});let sender = tx.getSenderAddress().toString('hex');

前述片段中的大多数参数现在应该很熟悉了：收件人地址、发送的 ETH 金额、燃气允许量和价格以及交易数据。由于此交易将从一个尚未发送其他交易的新地址发送，因此 nonce 必须为零。

这里我们看到的新参数是 v、r 和 s，它们对应于交易的签名。其中第一个必须从链 ID 派生[³]，而另外两个通常是从用户的私钥计算得出的——在这里，我们将它们替换为任意的字节序列。

### 注意

使用可识别的伪造序列作为 r 和 s 是非常重要的，例如清晰地重复相同的字节集，或者大量的前导零。否则，第三方无法知道生成的交易对象是否确实属于单次使用地址，或者签名是否是从实际私钥获得的。如果确实使用了私钥来生成交易，则其持有者在用户将其资金发送到所谓的单次使用地址时可以生成不同的交易。

现在，如果您尝试运行上述代码以获取发送者地址，则将收到由 getSenderAddress 调用抛出的“无效签名”错误。这是因为在以太坊中，并非所有签名都是有效的 - 大约一半是有效的。绕过这个问题的最简单方法就是尝试几个不同的值，直到我们找到一个有效的任意签名。例如，我们可以每次将 r 增加一个值，直到我们获得有效值为止。const BN = require('bignumber.js');let sender = null;while (!sender) {  try {    sender = '0x' + tx.getSenderAddress().toString('hex');  } catch(ex) {    const r = new BN('0x' + tx.r.toString('hex'));    tx.r = '0x' + r.plus(1).toString(16);  }}拥有有效的预签名交易后，我们现在可以尝试将其广播到网络。const rawTx = '0x' + tx.serialize().toString('hex');await web3.eth.sendSignedTransaction(rawTx);

但是，由于我们尚未为发送者地址提供资金，因此我们将收到“发送者没有足够的资金发送 tx”错误。请记住，派生的发送者是一个新账户，因此它永远不会有任何之前的资金。

此时，我们应该要求用户资助派生的一次性地址，并监视地址的余额变化，以便在有足够资金时广播交易。为此，我们首先需要计算所需的精确 ETH 数量：这是燃气津贴乘以燃气价格，加上交易中发送的任何价值。let required = (new BN(gas)).times(gasPrice).plus(value);

### 注意

请记住，发送到一次性地址的任何额外以太币都将丢失。

现在让我们模拟用户将这些资金发送到一次性地址。const [funder] = await web3.eth.getAccounts();await web3.eth.sendTransaction({  from: funder, value: required, to: sender});现在我们可以最终将交易发送到网络并验证事件是否正确发出。let rawTx = '0x' + tx.serialize().toString('hex');await web3.eth.sendSignedTransaction(rawTx);let events = await donations.getPastEvents('Donation');console.log(events[0].returnValues.text);// 输出 "Hello world  "

## 应用本地账户

在前几节中，我们看到了一些与智能合约应用程序进行交互的技巧，而无需使用以太坊账户，现在我们将探讨另一种选择：在应用程序*内部*为用户创建账户。与其要求用户下载一个支持 web3 的浏览器或安装扩展程序，我们可以管理在我们应用中直接创建钱包的整个流程。这允许任何访问我们应用的用户立即获得一个以太坊地址以开始交互。另一方面，我们还需要为用户提供安全备份他们的新钱包的手段，而不成为他们资金的托管者。

### 创建和使用本地钱包

创建以太坊账户需要一组随机字节来推导出私钥，从中计算出地址。我们可以使用 web3@1.2.0 库的账户方法集来完成这个过程^(4)（见代码清单 7-5），这将自动从浏览器的加密 API 中提取所需的熵。let account = web3.eth.accounts.create();代码清单 7-5

使用 web3 创建账户。注意，创建私钥无需连接网络。

现在，我们可以使用此账户对象的私钥对交易进行签名并广播到网络上（见代码清单 7-6）。let tx = await web3.eth.accounts.signTransaction({    to: account.address,    value: 1e17,    gas: 21000,    gasPrice: 1e9 },  account.privateKey);await web3.eth.sendSignedTransaction(tx.rawTransaction);代码清单 7-6

使用账户的私钥签署发送 ETH 的交易，并手动将其发送到网络。注意，发起此交易需要在发送者地址中存入一些 ETH。

为了避免手动生成、签署和广播每个交易，web3 库允许将账户注册为钱包（见代码清单 7-7），这将自动用于发送任何交易。web3.eth.accounts.wallet.add(account);await web3.eth.sendTransaction({  from: account.address,  to: account.address,  value: 1e17,  gas: 21000});代码清单 7-7

在 web3 中将账户注册为钱包。从钱包地址发送的任何交易将自动由库本地签名，然后发送到网络。

### 注意

从之前的章节中可以回顾到，Metamask 通过 web3 子提供程序实现了类似的行为。不是依赖节点签署交易，而是拦截交易，客户端签署，然后广播。

### 加密的密钥存储

下一个问题是如何在生成用户的钱包后存储它。最直接的方法就是将私钥保存在浏览器的本地存储中，这样当用户再次访问我们的网站时，我们就可以轻松重建账户对象。// 将私钥存储在本地存储中 localStorage.setItem("ethereum_pk", account.privateKey);// 从本地存储加载私钥并重新创建账户 let pk = localStorage.getItem("ethereum_pk");let account = web3.eth.accounts.privateKeyToAccount(pk);

然而，这种选择极其不安全，因为浏览器的本地存储不应该用于保存敏感信息，因为它容易受到 XSS 攻击^(5)的影响 - 更不用说如果用户清除站点数据或丢失设备，则密钥会丢失。像这样存储明文私钥只有在管理非常少量的 ETH 并且资金损失可接受时才推荐，换句话说，当可用性优先于安全性时。^(6)

更安全的方法是在存储之前对私钥进行加密（见列表 7-8）——无论是在浏览器的本地存储中，还是在远程服务器上，或者下载到用户的计算机上，或者在云存储中同步。以太坊的*钱包 v3 格式*是一个标准化的 JSON，其中包含用密码加密的私钥，不易破解^(7)。它在节点内部用于存储您的密钥，在浏览器中也可以用于在存储之前加密您的用户账户。$ web3.eth.accounts.encrypt(account.privateKey, 'PASSWORD');> { version: 3,  id: 'b8c62b04-041c-49d6-966a-205bb5f70528',  address: 'af0a9c8d7f74dff1ce64f9c322108c336502bbd4',  crypto:   { ciphertext: 'ba09a90b5...7b0e5e24da79d7f9efda613fd298',     cipherparams: { iv: '2e72184026373b69d21ce157b1d93bba' },     cipher: 'aes-128-ctr',     kdf: 'scrypt',     kdfparams:      { dklen: 32,        salt: 'eab3860a...d1d378abbc55a65cae3c83e0a39e',        n: 8192,        r: 8,        p: 1 },     mac: '60177f2af3...bd900315e46e2d' } }Listing 7-8

将用户的私钥用密码加密以生成 v3 密钥库对象。相反的方法，decrypt，接受密钥库和密码，并返回解密的账户对象。

虽然这是一个更安全的选项，但它通过向用户请求密码引入了额外的复杂性。尽管密码是网页用户的常见烦恼，但他们也习惯了*在忘记密码时*能够重置它们——而这种选项在这种情况下是不可用的。如果用户忘记了 keystore 的密码，其中的内容就永远丢失了。

除了这个问题之外，密钥库本身也不能被误放。如果您只是在浏览器中存储加密的私钥，并且用户恰好清除了本地数据或者简单地丢失了设备，那么所有的资金也会随之消失。您必须确保用户进行适当的备份（要求他们从您的页面下载密钥库并将其保存在其他位置），或者在您的应用程序服务器之一的安全位置保存它们（假设您有一个！）。

### 注意

在成为您的用户资金的托管人和成为一个用于存储他们的加密私钥备份的位置之间存在很大的区别。在前者上，您服务器的任何黑客攻击都意味着您的用户资金的损失，而后者只是为了方便您的用户保护他们的加密密钥。

但是，从法律角度来看，这种差异可能并不是很大。确保在您的司法管辖区内了解法律要求，如果您确实将用户的加密密钥存储在服务器端。

### 记忆法

一个去中心化的备份用户密钥的替代方法是生成一个*记忆法*。记忆法是一系列词（通常在 12 到 24 之间），可以由人类轻松地书写以供保管，当您在钱包中创建帐户时，您可能已经遇到过它们。请记住，它们仅仅是作为备份的一种手段，如果密钥库丢失了，那么要求您的用户每次想使用您的应用程序时都要求其提供一个 24 个字的序列是不合理的。

记忆法的主要好处在于它们提供了一种在传统物理介质（纸张）中存储数字信息（私钥）的方法。这样，即使用户所有的电子设备被盗或者被黑客攻击，他们仍然可以依靠一种老式的方法来恢复他们的帐户。

不幸的是，无法从私钥生成助记词。正如我们在第五章中所看到的，派生过程是单向的：助记词用于计算扩展密钥，然后依次从中派生一个或多个私钥。这意味着，如果您希望允许用户通过此方法备份他们的账户，您需要从头开始构建。

要创建助记词并从中派生种子，我们将使用 bip39 库。要从中创建分层确定性钱包并派生私钥，我们将使用 ethereumjs-wallet 库（见列表 7-9）。

创建助记词和派生相应的私钥。请注意，可以使用不同的派生路径从相同的助记词生成更多的私钥。

此片段允许您为用户的账户生成助记词。只需注意，您的用户需要在刷新页面之前将助记词保存在安全的地方，因为您绝不能在任何地方存储纯文本的单词序列，因为这与存储未加密的私钥一样不安全。

到目前为止，我们已经添加了几种机制来确保用户资金的安全，例如用密码加密他们的私钥，并提供一个易于书写的单词集来备份它们。

但是，我们也复制了最初试图避免的同样复杂性，这种复杂性阻止了大多数用户真正加入以太坊。虽然我们会看到其他方法，但本节的关键要点是让您了解可用的工具，这样您就可以找到最适合您的应用程序的安全性、可用性和去中心化之间的适当平衡。

## 智能账户

本地钱包存在几个缺点：它们不仅需要额外的安全保管步骤，而且为从多个不同设备访问您的应用程序的用户提供了非常有限的选项。即使您可以依靠云服务来同步加密的私钥到用户的设备，但是撤销设备的访问是不可能的。更糟糕的是，对于关键交易的双因素身份验证等额外安全措施无法实施，除非信任基金的托管者。

幸运的是，我们已经拥有了一个分散且安全的计算平台，我们可以依靠它为用户账户构建任何额外的安全或恢复功能。只需要将他们的账户移至区块链作为合约即可。

### 智能合约作为身份

*智能账户*背后的关键概念，也被称为*身份合约*，是用户身份（及其资金）由单个智能合约代表，而不是一个或多个外部拥有的账户。用户控制一个合约，将其调用转发给其他应用程序，并集中保存用户的资产。从新设备管理此身份只是将新的外部拥有的账户注册为合约的管理者的问题。

### 注意

对这些合约的研究被称为身份合约、智能账户、弹簧代理、多签钱包或钱包合约。这些合约通常与元交易或燃气中继一起使用，我们将在本章后面进行审查。虽然很难确定最先提出这个想法的人，但值得一提的是 Alex Van de Sande、Philippe Castonguay、Panashe Mahachi、Austin Griffith、Christian Lundkvist 和 Fabian Vogelsteller 他们在这个主题上的工作。这个领域的工作也受到 Vitalik Buterin 的“账户抽象化提案”^(8)的启发，该提案旨在将外部拥有的账户和合约账户合并为一个类型，并将签名验证的负担转移到 EVM 上。

将用户的身份转移到智能合约中，我们可以以无需信任的方式直接在链上实现用户习惯的任何类型的账户管理功能：

+   用户可以注册多个设备，其中每个设备都有自己的外部拥有账户，以管理相同的身份合约。

+   不同的密钥可以有不同的访问级别：从管理身份合约本身到仅能够转移有限金额的权限。

+   重要交易可以要求超过一个密钥来确认操作，有效地对关键操作实施双因素身份验证（2FA）。

+   通过指定一组受信任的方来实现账户的社交恢复。这意味着你可以选择一群亲密的朋友，他们可以一起在你丢失密钥时授予你重新访问身份合约的权限。甚至可以扩展到遗嘱。

请记住，使用智能账户并不意味着不再需要生成本地外部拥有账户。如果用户没有 web3 启用的浏览器，我们的应用程序仍然需要为每个设备创建一个本地密钥来管理身份合约。相对于常规账户，智能合约的改进在于可以以去中心化方式实现额外的安全性和恢复功能 - 例如，社交恢复可以用作替代写下 24 个单词的助记词。

### 实现示例

最简单的身份账户版本（见 7-10）应处理两个主要问题：管理被授权在合同上操作的用户账户列表，并转发调用和转账。// 04-identity-contracts/contracts/Identity.solpragma solidity ⁰.5.0;contract Identity {  mapping(address => bool) public accounts;  event AccountAdded(address indexed account);  event AccountRemoved(address indexed account);  constructor(address owner) public payable {    accounts[owner] = true;    emit AccountAdded(owner);  }  modifier onlyUser {    require(accounts[msg.sender], "Sender is not recognized");    _;  }  function addAccount(address newAccount) onlyUser public {    accounts[newAccount] = true;    emit AccountAdded(newAccount);  }  function removeAccount(address toRemove) onlyUser public {    accounts[toRemove] = false;    emit AccountRemoved(toRemove);  }  // 转发任意调用和资金至第三方  function forward(    address to, uint256 value, bytes memory data  ) onlyUser public returns (bytes memory) {    (bool success, bytes memory returnData) =      **to.call.value(value)(data)**;    require(success, "Forwarded call failed");    return returnData;  }  // 空的回退函数以接受存款  function() external payable { }}列表 7-10

一个非常基本的身份合约，支持管理用户账户和转发调用

当此合约首次部署时，用户的第一个帐户将被注册。然后，任何来自新设备的新帐户都可以从以前的帐户注册（见清单 7-11）。// 04-identity-contracts/index.jsconst identity = await new web3.eth.Contract(identityAbi)  .deploy({ arguments: [mainDevice], data: identityBytecode })  .send({ from: mainDevice, gasPrice: 1e9, value: 10e18 });await identity.methods.addAccount(anotherDevice)  .send({ from: mainDevice });清单 7-11

创建一个资金为 10 ETH 的身份合约并添加第二个设备。在此示例中，mainDevice 和 anotherDevice 是用户设备上创建的帐户

任何两个注册帐户都可以使用 forward 方法将资金从身份发送到第三方（见清单 7-12）。const emptyData = [];await identity.methods  .forward(thirdParty, 1e18.toString(), emptyData)  .send({ from: anotherDevice });await web3.eth.getBalance(identity.options.address);// => 9 ETHawait web3.eth.getBalance(thirdParty);// => +1 ETH 清单 7-12

使用 anotherDevice 从身份合约发送资金

调用另一个合约类似；只需对合约的调用进行编码，并将其作为数据提供给转发函数即可（见清单 7-13）。例如，我们可以从前几章编写的 Greeter 合约中调用 setGreeter 方法。const data = greeter.methods.setGreeting("Hey").encodeABI();await identity.methods  .forward(greeter.options.address, "5000", data)  .send({ from: anotherDevice });await greeter.methods.greet().call();// => "Hey"清单 7-13

从身份合约调用 greeter 合约实例的 setGreeting 方法，包括在交易中包含 5000 Wei

大多数前面讨论过的功能都可以建立在这个基本合约之上：可以为帐户分配不同的许可级别，同时可以根据转移的价值对转发函数施加限制。

这方面的一个很好的例子是多签钱包[⁹]。这些合约被设计为注册了 N 个账户，并且每笔交易都需要至少 M（其中 M < N）个确认。虽然它们经常被用于通过将密钥分配给团队的不同成员来保管大量资金，但它们也可以用于通过将不同的密钥分配给不同的设备来管理个人资金。

### 部署智能账户（第一部分）

由于本章的重点是让用户更容易上手，要求用户不仅要生成本地的外部拥有账户，还要部署合约、为其注资，并在其中注册他们的设备，似乎是朝着相反的方向迈出的一步（或许是很多步）。

然而，许多这些步骤可以由应用程序代表用户完成，包括部署。在用户在我们系统内执行了一定数量的操作后，我们可以选择代表他们部署身份合约，并将其所有权转移到他们的账户上。尽管这意味着需要支付燃气费用，但在许多情况下，这种补贴可以被视为用户获取的必要成本。

然而，一个更为去中心化（对我们更为便宜）的选择是依赖于用于设置合约的一次性地址。我们的应用程序可以在幕后生成一个本地钱包，作为身份合约的初始所有者（如果用户尚未拥有 Web3 浏览器），以及一个一次性地址，可以在资金到位后触发智能账户的部署和配置。当一次性地址从交易所获得资金时，身份就会被部署，并以预定义数量的 ETH 进行初始化。从那时起，用户可以直接通过他们的新身份合约进行操作。

### 注：

请记住，在单次使用地址部分提到，发送到地址的额外资金将被永久性地丢失。用户必须选择要最初发送到他们身份的 ETH 金额，然后创建交易并用确切的结果金额资助它。

为部署合约生成单次使用地址类似于调用合约，不同之处在于，交易必须发送到 null 地址（见 7-14）。// 05-single-use-address-deploy-identity-contract/index.jslet call = new web3.eth.Contract(identityABI)  .deploy({ arguments:[owner], data: identityBytecode });let data = call.encodeABI(); // Encode data for deploymentlet gas = await call.estimateGas();let gasPrice = 1e9;let value = 1e18; // Seed identity with 1ETH on deploymentlet nonce = "0x00";**let to = null; // Set tx recipient to null**Listing 7-14

用于部署合约的交易参数。请注意，接收者被设置为 null，因为我们正在创建新的合约，而不是与现有的合约交互。签名参数设置如本章单次使用地址部分所示。

此方法的另一个有趣特性是，由于合约创建地址是确定性的，所以可以在合约*部署之前*向用户显示他们的身份合约地址（见 7-15）。合约部署的地址是发送者地址和 nonce 的函数。const Util = require('ethereumjs-util');let deploymentAddress = '0x' + Util.generateAddress(  Buffer.from(sender.substring(2), 'hex'),  Buffer.from(nonce, 'hex')).toString('hex')Listing 7-15

使用 ethereumjs-util 库预先计算部署地址

然而，这种方法的一个问题是我们向用户展示了两个不同的地址：一个地址是他需要一次性为部署提供资金的地址，另一个地址实际上将成为他们的身份合约。这与向地址发送的任何额外 ETH 丢失的事实结合在一起，会在设置他们的智能账户时损害用户体验。在我们熟悉了元交易的概念后，我们将在本章后面分析一个更健壮的方法。

### 注意

更简单的选择是让用户将资金转移到他们的设备账户，无论是本地应用程序还是由 web3 浏览器管理，然后从中执行部署。然而，这仍然存在一个问题，即向用户呈现两个地址 - 一个用于初始资金和一个用于身份。

### 升级用户账户

正如我们所见，身份合约可以为您的用户提供多种功能，如双因素身份验证、社交恢复、每日转账限额等。这引发了一个问题，即要在这些合约中构建什么。由于合约是不可变的，要添加新功能的任何更改都需要您的用户放弃当前的身份并部署新的身份。然而，强迫用户将所有资产移动到新合约相当于强迫他们在想要访问新功能时切换到新的电子邮件帐户 - 包括在可能使用的所有在线服务中更改他们的电子邮件。

尽管如此，在以太坊中实际上是可以在部署后升级合约的，从而允许像传统软件开发中那样进行迭代部署和错误修复。要实现这一点，我们首先需要熟悉以太坊虚拟机（EVM）中的*委托调用*的概念。

#### DELEGATECALL 指令

在 EVM 中，从一个合约向另一个合约进行常规 CALL 的工作方式类似于从一个参与者或进程向另一个进行调用：一个新的上下文被创建，在这个上下文中加载了被调用者的状态（存储和余额），调用者被设置为 msg.sender，然后执行被调用者的代码。另一方面，DELEGATECALL 通过执行被调用者的代码但*保持调用者的原始上下文*来工作。换句话说，存储、余额甚至 msg.sender 都不会被 DELEGATECALL 更改 - 只有被执行的代码会更改。

这个低级指令允许我们跳转到一个任意合约并执行其代码，其中该代码实际上修改了当前合约的状态。然后被调用的合约充当一个库，^(10)仅被用作共享代码的存储库，而不使用其状态。

#### 代理代理

DELEGATECALL 指令允许我们构建一个合约，简单地将所有调用委托给另一个合约，该合约保存了要执行的实际逻辑。这些合约通常被称为*代理代理*，因为它们将所有调用委托给另一个合约，或者*透明代理*，因为与它们交互的任何客户端都不知道它们的存在。实际执行代码的代理调用的合约通常被称为*逻辑合约*、*实现合约*或*主合约*。

一个委托代理（见列表 7-16）可以在 Solidity 中作为一个合约实现，该合约将其实现合约的地址作为唯一的状态变量，并且只有一个回退函数，其中将所有调用委托给它。代理将在其构造函数中接收实现地址以及可选的 calldata 以初始化它。// 06-upgrading-identity-contracts/contracts/DelegateProxy.solcontract DelegateProxy {  // 在第一个槽中存储地址  // 目标合约必须将地址定义为第一个变量  address private implementation;  constructor(    address _implementation,    bytes memory _data  ) public payable {    implementation = _implementation;    if (_data.length > 0) {      (bool success,) = _implementation.delegatecall(_data);      require(success);    }  }  // 回退函数将所有调用委托给实现  function () payable external {    address impl = implementation;    assembly {      calldatacopy(0, 0, calldatasize)      let result := delegatecall(        gas, impl, 0, calldatasize, 0, 0      )      returndatacopy(0, 0, returndatasize)      switch result      case 0 { revert(0, returndatasize) }      default { return(0, returndatasize) }    }  }}列表 7-16

基于来自 github.com/zeppelinos/zos 代码的委托代理合约的实现。请注意在回退函数中使用了 assembly，因为 Solidity 不允许回退函数返回任意数据。如果我们不返回任何数据，那么对我们合约的任何调用都将产生空响应

### 注意

在以太坊虚拟机中实现可升级性可能非常棘手，并且会施加一些限制。例如，当创建代理合约时，代理合约不能执行逻辑合约的构造函数，因此任何需要可升级性的合约都需要依赖于充当*初始化器*的常规函数。另一个问题是，将代理更新为具有不同状态变量集的逻辑合约也可能无意中损坏合约的状态。如果您计划在应用程序中依赖于可升级合约，无论它们是智能账户还是任何其他合约，强烈建议您使用现有的升级性解决方案，而不是自己开发。

这里的关键概念是逻辑合约的地址不需要硬编码到代理中 - 它实际上可以保存在存储中。当这个地址被更改时，这实际上更新了代理执行的代码，同时保持了其状态和地址。我们现在可以将这个功能添加到我们的身份合约中。

#### 升级身份验证

有了这个新的构建模块，我们可以部署一个单一的身份合约作为逻辑合约，并为我们的每个用户部署一个代理。请记住，由于所有状态都保存在代理中，因此不需要多个逻辑合约的副本，一个逻辑合约就可以在多个代理之间共享（就像一个库）。

这不仅在部署时节省了燃料，因为代理合约要比身份合约小得多（因此更便宜），而且还允许我们的用户随时升级到不同的身份合约。让我们将*升级*功能构建到我们的新可升级身份中（见 7-17）。// 06-upgrading-identity-contracts/.../UpgradeableIdentity.solcontract UpgradeableIdentity {  // 第一个变量用于实现合约  // 记住代理使用相同的变量位置！  address private implementation;  // 跟踪此实例是否已初始化  bool private initialized;  // 初始化函数而不是构造函数  function initialize(address owner) public payable {    require(!initialized);    initialized = true;    accounts[owner] = true;    emit AccountAdded(owner);  }  // 升级到新的实现  function upgradeTo(    address newImplementation  ) onlyUserAccount public {    implementation = newImplementation;  }  // 身份合约代码的其余部分放在这里...}Listing 7-17

支持可升级性的身份合约的变体。请注意，第一个合约变量是实现合约地址，构造函数已被替换为一个普通函数，该函数依赖于一个标志来跟踪实例是否已初始化。将身份实现升级到不同的实现只需要在存储的第一个位置更改实现地址即可。

请记住，此合约上定义的任何状态变量实际上不会存储在此合约的存储中，而是存储在代理的存储中 - 这要归功于委托调用的魔法。例如，initialized 标志实际上不会设置在单个 UpgradeableIdentity 合约上，后者作为共享实现部署，而是在由其支持的每个代理上设置。

因此，此合约上声明的第一个变量必须是实现地址，就像代理一样。此外，合约不能扩展自定义义额外的合约变量。这确保实现地址存储在与代理将要查找的位置相同的存储位置中。^(11)

### 注意

合约升级性对于以太坊的许多人来说是一个有争议的问题。具有不可变合约的用户可以通过知道由它定义的规则不会受到更改来信任应用程序。添加可升级性会破坏这一保证。然而，这不是可升级性本身的问题，而是**谁**可以决定何时升级合约的问题。由单个开发人员控制的分散式代币可以随意修改合约，比如增加交易税，这绝对不好。另一方面，具有明确所有者（或一组所有者）的合约是可以升级的良好候选对象——在这里，身份合约就是一个完美的例子。

为用户创建身份合约现在意味着部署的不是合约实例，而是一个代理——假设我们已经部署了单个共享实现合约（见列表 7-18）。// 06-upgrading-identity-contracts/index.js// 逻辑合约是 Identity 的预先部署实例 let logic = new web3.eth.Contract(identityABI, identityAddr);// 构建初始化数据以在创建代理时调用 initialize(user)let initData = logic.methods.initialize(user).encodeABI();// 使用身份合约作为其实现部署代理，并将用户设置为其初始所有者 let proxy = await new web3.eth.Contract(proxyABI, null, { data: proxyBin })  .deploy({ arguments: [logic.options.address, initData] })  .send({ from: application, gasPrice: 1e9, value: 1e18 });列表 7-18

创建一个到身份合约的代理。请注意，我们需要使用逻辑合约 ABI 来构建初始化数据，然后在部署代理时使用它。

部署代理后，我们可以像与常规身份合约交互一样与其进行交互。我们需要使用身份合约 ABI 创建一个新的 web3 合约对象，代理的地址为 (Listing 7-19)。let proxyAddr = proxy.options.address;let identity = new web3.eth.Contract(identityABI, proxyAddr);await identity.methods  .addAccount(anotherDevice)  .send({ from: user });Listing 7-19

与新部署的代理交互，就像它是一个常规的身份合约一样。代理将把所有调用委托给逻辑合约，并且表现得完全一样

与身份合约的任何其他方法一样，用户可以调用升级函数并切换到不同的实现 (Listing 7-20)。但是需要注意的是，新实现必须具有与原始实现相同的合约状态变量；否则，代理的状态可能会被破坏.await identity.methods  .upgradeTo(identityV2addr)  .send({ from: user });Listing 7-20

升级到身份合约的 V2 版本。用户的身份地址未修改，其余的余额和状态也未修改，但它可以访问具有潜在新功能和 bug 修复的新代码

在智能账户中实现这种模式允许我们逐步开发应用程序，逐渐添加对新功能的支持或修复错误，并在用户希望时让他们采用这些功能。

我们可能希望向我们的身份合约添加的一个很好的功能示例是元交易支持，我们将在下一节中看到。

## 无 Gas 交易

用户入门的根本问题之一是，与以太坊网络进行交互需要一些 ETH 作为开始，以便能够支付燃气费用。这涉及一系列烦人的步骤，只是为了用其他货币购买初始的 ETH。在多设备解决方案中，燃气费用也是一个问题：用户的所有设备必须持有一些 ETH 才能执行任何交易，即使依赖智能账户来集中用户身份也是如此。

上述所有情况意味着，移除以太坊交易的燃料要求在可用性方面带来了重大的好处。*无燃料交易*，也称为*元交易*，通过提供一种机制来解耦交易的发起者和燃料的支付者来解决这个问题。换句话说，一个账户可以发起交易，而其他人支付其执行。这使得您应用程序中的用户可以执行任何交易，而无需担心是否有 ETH 来支付他们的燃气费用。

### 注意

在撰写本文时，无燃料交易是以太坊生态系统中发展最活跃的技术之一，并且已经有许多不同的变体。这使得本节成为本书中最复杂的部分之一。可以忽略技术细节，并考虑查阅已经建立的库，例如 Universal Login、Marmo 或 Gas Station Network。

### 以太坊中的签名

要理解无气交易，我们首先需要回顾以太坊中签名是如何工作的。正如我们之前所见，以太坊交易需要用发送者的私钥进行密码学*签名*才能有效。然而，用户的密钥不仅可以用来签署交易，还可以用来签署任意消息（见 7-21）。

使用 web3 使用用户的私钥签署消息^(12)

### 注意

在幕后，web3 的 sign 方法会在消息前添加字符串"\x19Ethereum Signed Message:\n"以及其长度，然后对其进行哈希处理后再进行签名。这样做是为了避免用户被欺骗签署实际交易。大多数 API，即使是节点或硬件钱包中的 API，都会自动处理这一点。

鉴于原始消息及其签名，可以恢复对应于首次签署它的私钥的地址。> hash = web3.utils.keccak256(message);> web3.eth.accounts.recover(hash, signed.signature)*0xACa94ef8bD5ffEE41947b4585a84BdA5a3d3DA6E*恢复不仅可以从离线脚本中进行，还可以从智能合约内部进行（见列表 7-22），因为 Solidity 提供了一个 ecrecover 函数来执行此任务。^(13) 我们将通过 openzeppelin-solidity@2.2.0 库中的 ECDSA 合约来使用它，该库提供了一个更友好的界面并执行额外的检查。// 07-signing-messages/contracts/Signatures.solpragma solidity ⁰.5.0;import "openzeppelin-solidity/contracts/cryptography/ECDSA.sol";contract Signatures {  using ECDSA for bytes32;  function recover(    string memory message, bytes memory signature  ) public pure returns (address) {    **bytes32 hash = keccak256(bytes(message));**    **return hash.toEthSignedMessageHash().recover(signature);**  }}列表 7-22

基于 OpenZeppelin 的 ECDSA 来从消息及其签名中恢复签名者的简单合约。

我们可以检查调用前述合约的 recover 函数，使用与之前相同的参数是否产生相同的签名者（见列表 7-23）。> await signatures.methods    .recover(message, signed.signature).call();*0xACa94ef8bD5ffEE41947b4585a84BdA5a3d3DA6E*列表 7-23

使用前面列出的智能合约从原始消息中恢复签名者。这里，signatures 是一个 web3 合约实例，代表着部署的智能合约的一个实例。

以太坊签名通常用于链下验证用户控制某个账户，或者账户的所有者通过签署特定消息来表达意图（例如，在链下投票）。但签名也可以在链上用于验证账户所有者打算*执行*某个操作。这就是元交易的用武之地。

### 介绍元交易

*元交易*或*无 gas 交易*与常规交易类似，它是一个签名的元组，包含收件人、转移的 ETH 金额、调用中包含的数据集、gas 津贴和价格以及一个随机数。但是，元交易不是广播到网络，而是包装在另一个交易中发送到特定的合约。这个合约知道如何展开嵌套交易，验证其签名，并执行请求的操作。

注意，首先接收和处理交易的合约实际上正在复制以太坊协议的相同行为：它验证嵌套交易的签名和随机数，并对指定值和数据调用接收方。

那么元交易的价值是什么呢？关键在于元交易可以被一个不同于签署原始意图的账户*中继*到网络。这样，打算执行操作的用户和支付其 gas 费用的用户就分离开来了，实际上*允许任何用户执行交易而无需任何 gas*，也就是说，只要另一个用户愿意为其支付。因此，元交易涉及两个主要角色：

+   用户签署一份他们希望执行的元交易，但并未将其发送到网络。

+   中继器捡起该交易，将其包装在自己的另一笔交易中，并发送到一个合约，为其执行支付费用。

我们将在本章后面详细讨论中继器。首先让我们深入到智能合约层面的元交易实现中。

#### 在我们的智能账户基础上构建

元交易需要一个能够处理它们、验证它们、检查签名者是否被授权执行所请求操作，并代表他们执行该操作的合约。幸运的是，我们已经有一个能够保存资金并代表用户持有的不同帐户执行操作的合约：身份合约。

我们将修改我们一直在构建的身份合约，以处理元交易。我们的转发函数现在将接收到一个由用户帐户之一预签名的元交易，而不是直接来自其中一个用户的调用。

因此，用户无需实际发送交易到身份合约，只需签署一个操作，并让中继发送它。这允许用户在单个智能账户中**持有所有资金，而无需在设备上存储任何 ETH 来支付燃气费用**。让我们看看在修改后的身份合约中是如何实现的（见列表 7-24）。// 08-meta-txs/contracts/IdentityWithMetaTxs.sol// 防止重放攻击 uint256 public nonce;// 使用 ECDSA 库来检索签名者 using ECDSA for bytes32;// 转发操作到验证签名者的接收者// 注意，不再需要 onlyUser 修饰符 function forward(  address to, uint256 value, bytes memory data,  bytes memory signature) public returns (bytes memory) {  // 获取被签名的交易哈希  bytes32 hash = getHash(to, value, data)    .toEthSignedMessageHash();  // 检索签名者地址并验证  address signer = hash.recover(signature);  require(accounts[signer], "签名者未注册");  // 增加 nonce 并执行调用  nonce++;  (bool success, bytes memory returnData) =    to.call.value(value)(data);  require(success, "转发调用失败");  return returnData;}// 返回预签名交易的哈希 function getHash(  address to, uint256 value, bytes memory data) public view returns (bytes32) {  return keccak256(abi.encodePacked(    to, value, data, nonce, address(this)  ));}列表 7-24

修改后的转发函数，从之前章节中的身份合约处理元交易

首先需要注意的是，转发方法需要一个签名以及其原始参数。该签名是在包括所有交易参数（接收者、数值和数据）及两个额外项的哈希上计算的。

+   验证者的地址，即检查签名的合约

+   每笔执行的交易都会增加一个一次性数字。

验证者的地址包含在内，以防止将元交易发送到另一个验证者并在此交易中重复使用，而 nonce 则防止重放攻击（即多次中继相同的交易）。结果哈希会在前面加上魔术前缀"\x19 以太坊签名消息：\n"，以便与普通以太坊交易区分开来，然后再次进行哈希运算。

### 注意

某些实现会跟踪每个签名者的一次性号码，而不是全局的合约号码。这完全取决于您的用例：如果可能有多个列入白名单的帐户同时发送元交易，那么您应该有特定于签名者的一次性号码。

接下来是对发送方的验证。请注意，合约不再检查 msg.sender 是否是注册账户，而是检查交易的*签名者*。在这个阶段，中继交易的发送者变得无关紧要，因为谁中继了交易在这个阶段并不重要。

最后，在执行交易之前，nonce 会增加。这可以防止恶意中继者多次将相同的交易发送到合约。

### 注意

值得一提的是，几乎所有的智能账户、身份合约或守门员代理实现都包含一些元交易的变体。一旦用户身份转移到链上，将它们绑定到协议的限制，比如让发送方账户为其交易支付 gas 费，就没有意义了。

#### 发送元交易

我们将从智能账户部分继续示例，这次是通过我们的 Identity 合约向 Greeter 合约发送元交易。第一步（见 7-25）是用户签署要执行的交易。// 08-meta-txs/01-identity-with-meta-txs.jslet recipient = greeter.options.address;let value = 5000;let data = greeter.methods.setGreeting("Hey").encodeABI();let hash = await identity.methods.getHash(recipient, value, data).call();let signature = web3.eth.accounts.sign(hash, pk).signature;Listing 7-25

用户制作并签署要中继的交易。这里的 pk 是用户的私钥，greeter 是一个具有 setGreeting 方法的合约实例。

然后将结果交易及其签名通过 HTTP 或其他链下传输发送到中继。中继应该验证交易，包装它，然后将其发送到用户的身份合约（见 7-26）。等待 identity.methods.forward(recipient, value, data, signature).send({ from: relayer });await greeter.methods.greet().call();// => 嗨 7-26

中继使用用户提供的参数和签名调用身份合约的转发函数。身份合约将进一步调用 greeter，从而更改其状态。

我们故意从此示例中省略了用户如何与中继通信以及中继如何决定是否为用户的交易付款。这将因应用程序而异。例如，一个应用程序可以提供一个位于众所周知的 URL 上的中心化中继，该中继为其系统中的每笔交易付款。它也可以强制用户通过验证码以防止垃圾邮件。

也有努力构建完全去中心化的 relayer 网络，其中支付用户交易是否真正作为应用程序的智能合约的一部分。这些努力还包括 relayer 收回其执行的方法，我们将在下一节中看到。^(14)

### Relayers 和奖励

[Relayer](https://example.org/relayer) 最终是一个具有公共接口（通常为 HTTP）的过程，接受用户的签名消息，验证它们，将它们包装成交易，并推送到网络。对于这最后一步，Relayer 使用自己的账户 - 手续费从该账户余额中扣除。

在我们迄今为止的所有示例中，我们假设执行元交易的 gas 成本由应用程序的所有者承担。该所有者将启动一个 relayer 并免费为其自己应用程序的用户转发所有交易。

然而，用户实际上可以*回馈*给为其提供服务的 relayer。在转发功能中添加一项操作是将一些 ETH 发送回 relayer（即，msg.sender），以支付执行成本。这样，用户确实支付了与他们的交易相关的 gas 费用 - 只是这些费用是从他们的智能账户中支付的，完全消除了在每个设备中保留 ETH 作为 gas 的必要性。

这为新的激励系统打开了大门：relayer 不需要被应用程序所有者集中管理并补贴执行成本，而是可以去中心化并从中继交易中获利。这导致了一个新的概念 *桌面挖矿*，用户可以通过为其他用户中继元交易而获得费用，而不是通过计算密集型的工作证明。

#### Relayer 奖励

实现对 relayer 的回馈最简单的方法是在每个执行请求中包含一个 *奖励*。Relayer 然后可以根据其估计的执行成本决定是否中继交易。

用户甚至可以为其交易请求特定的燃气价格和燃气津贴，并验证这些是否在身份合同中得到满足。这可以防止中继使用非常低的燃气价格发送交易，以牺牲用户的时间来支付较低的费用。

让我们再次修改转发函数，以考虑上述所有内容（清单 7-27）。我们需要添加参数来指定奖励和燃气要求，并由用户签名。// 08-meta-txs/contracts/IdentityWithRewards.sol**事件 Forwarded(uint256 nonce, bool success, address relayer);**函数 forward(  **uint256 reward, uint256 gasPrice, uint256 gasLimit,**  address to, uint256 value, bytes memory data,  bytes memory signature) public returns (bytes memory) {  // 验证交易的燃气价格  **require(tx.gasPrice >= gasPrice, "Gas price too low");**  // 获取已签名交易的哈希  bytes32 hash = getHash(    **reward, gasPrice, gasLimit**, to, value, data  ).toEthSignedMessageHash();  // 检索签名者地址并验证  address signer = hash.recover(signature);  require(accounts[signer], "Signer not registered");  // 增加 nonce，执行调用，并通知成功  nonce++;  **require(gasleft() >= gasLimit);**  (bool success, bytes memory returnData) =    to.call.value(value)**.gas(gasLimit)**(data);  **emit Forwarded(nonce, success, msg.sender);**  // 向中继支付回报  **msg.sender.transfer(reward);**  return returnData;}函数 getHash(  **uint256 reward, uint256 gasPrice, uint256 gasLimit,**  address to, uint256 value, bytes memory data) public view returns (bytes32) {  return keccak256(abi.encodePacked(    **reward, gasPrice, gasLimit,**    to, value, data, nonce, address(this)  ));}清单 7-27

Forwarding function of the identity contract with support for relayer rewards. The modified sections are highlighted in bold

在前述代码片段中的一个重要变化是该函数不再需要转发的调用成功（require(success)）。这样做的理由是，如果转发的调用失败并回滚整个交易，则转发者将不会收到任何奖励，但仍将失去执行回滚事务的气费。为了避免惩罚一个正确转发但失败的交易的转发者，我们取消了该要求。并且为了允许确定转发调用是否回滚，我们添加了在每个交易中报告成功的事件。

此外，请注意，气价验证是在方法开始时执行的，因为气价相对于整个交易，并且不能在合约调用之间更改。另一方面，气限可以在交易中的每次调用中强制执行，因此如果剩余气量不足，则可以回滚。在这种情况下，将额外的气量包含在请求中以考虑元交易处理（在此实现中约为 60K）是转发者的责任。

#### 利润估算

在这种情况下生成签名交易的代码类似于上一个场景，唯一的区别是用户现在需要包括气价、气限和奖励的值。前两者可以通过使用价格预言机（如 ethgasstation API）或者 gasPrice JSON-RPC 方法来估算气价，并对待发送的交易运行 estimateGas 来估算气限，如第五章所示。奖励的值可能取决于其他因素，但必须大于转发者的总执行成本，以激励转发交易。

在这种情况下，中继人不仅需要中继请求的交易，还需要评估是否应该中继 - 通过计算利润。估计利润低于一定阈值的交易应该被丢弃，并且如果排队了多个交易（来自不同的身份），则利润可以用来确定优先执行哪个交易。

利润可以通过实际估算整个调用来轻松计算，将估算乘以气价，然后从奖励中减去。// 08-meta-txs/02-identity-with-rewards.jslet estimatedGas = await identity.methods  .forward(reward, gasPrice, gasLimit,           recipient, value, data, signature)  .estimateGas({ from: relayer, gasPrice });let estimatedProfit =  BN(reward).minus(BN(estimatedGas).times(gasPrice));请记住，如果用户请求的 gasLimit 更高，则实际上可能需要比估计更高的气体值。要实际执行交易，中继人应发送一个气体津贴，等于 gasLimit 加上处理元交易所需的额外气体。这额外的气体可以粗略地计算为直接向接收方合约发送交易和通过身份作为元交易发送之间的差异。在我们的实现中，该差异大约为 60K 气体，尽管此值不是恒定的：它稍微波动取决于交易数据的大小。await identity.methods  .forward(reward, gasPrice, gasLimit,           recipient, value, data, signature)  .send({ from: relayer, gasPrice, gas: gasLimit + 60000 });

请注意，如果估计和实际使用不同，这种差异实际上可能导致交易成本高于中继人预期，因为中继人可能设置了较高的气体津贴。

#### 以实物支付

交易执行产生的 gas 费用以以太币支付，因为它是以太坊网络的本地货币。然而，并没有什么强制性规定我们必须以相同的货币向中继器支付奖励，因为以太坊上有大量其他的交换媒介：每个可替代代币（ERC20）都是一种潜在的货币。

这打开了一个大门，允许我们的用户仅使用代币进行交易，因为以太币不再需要用于支付 gas 费用。如果我们的应用程序构建在基于代币的协议之上，这一点尤其有趣：它允许我们在用户参与我们的网络时向他们发送代币，这些代币又被用来支付中继器的奖励。我们的用户不需要持有或购买任何以太币；他们只与我们应用程序的代币打交道。

支持令牌支付的代码是直接从之前的代码修改而来的。我们在转发函数中添加了一个新的 rewardToken 参数，并在该地址上发送令牌，如果该参数设置为零地址，则发送以太币。// 08-meta-txs/contracts/IdentityWithTokenRewards.sol**import "openzeppelin-solidity/contracts/token/ERC20/IERC20.sol";**function forward(  uint256 reward, **address rewardToken**,  uint256 gasPrice, uint256 gasLimit,  address to, uint256 value, bytes memory data,  bytes memory signature) public returns (bytes memory) {  // 验证交易的燃料价格  require(tx.gasPrice >= gasPrice, "Gas price too low");  // 获取被签名的交易的哈希  bytes32 hash = getHash(    reward, **rewardToken**, gasPrice, gasLimit, to, value, data  ).toEthSignedMessageHash();  // 检索签名者地址并验证  address signer = hash.recover(signature);  require(accounts[signer], "Signer not registered");  // 增加 nonce，执行调用，并通知成功  nonce++;  require(gasleft() >= gasLimit);  (bool success, bytes memory returnData) =    to.call.value(value).gas(gasLimit)(data);  emit Forwarded(nonce, success, msg.sender);  // 支付给中继  **if (rewardToken == address(0)) {**    **msg.sender.transfer(reward);**  **} else {**    **require(IERC20(rewardToken).transfer(msg.sender, reward));**  **}**  return returnData;}

请记住，当你的应用程序启动中继进行令牌交易时，这种机制特别有用，但对于去中心化的中继来说，它带来了额外的困难。现在，进行桌面挖矿的随机中继需要检查奖励令牌的市场价值与执行成本之间的关系，以确定利润。不仅如此，它还需要确保市场上有足够的流动性来交易这种令牌以换取以太币，当他们想要兑现利润时 —— 这还没有考虑到交易的费用。

换句话说，如果您使用的中继基础设施与您的应用程序特定，则将中继奖励支付为特定协议的 ERC20 会很有用，但是 ETH 或广泛使用的 ERC20^(15) 可能是与去中心化中继一起使用的更好选择。

### 本地元事务

元事务，正如我们刚刚看到的，需要使用身份合约作为一个跳板代理来代替用户正在交互的实际合约。身份合约保存了处理已签名事务的逻辑，然后调用第三方合约，该合约不需要知道元事务的存在。

然而，如果应用合约已经支持处理元事务，就可以消除身份合约的需求。这种方法被称为*本地元事务*^(16)，因为它是在应用合约上内置的，而不是需要一个代理身份合约。

作为示例，让我们给 ERC721 合约添加原生的元交易^(17)，允许任何持有非同质代币的用户签署一个交易，使其在不花费 gas 的情况下转移（见清单 7-28）。代码与我们之前处理的转发函数类似，只是专门用于执行代币转移。// 08-meta-txs/contracts/ERC721WithNativeMetaTxs.solpragma solidity ⁰.5.0;import "openzeppelin-solidity/contracts/token/ERC721/ERC721.sol";import "openzeppelin-solidity/contracts/cryptography/ECDSA.sol";contract ERC721WithNativeMetaTxs is ERC721 {  using ECDSA for bytes32;  // 每个签名者跟踪 nonce  mapping (address => uint256) nonces;  function signedTransferFrom(    address from, address to, uint256 tokenId,    uint256 nonce, bytes memory signature  ) public {    // 检索签名者    bytes32 hash = getTransferHash(      from, to, tokenId, nonce, signature    ).toEthSignedMessageHash();    address signer = hash.recover(signature);    // 确保签名者能处理此代币    require(_isApprovedOrOwner(signer, tokenId));    // 验证 nonce 并增加它    require(nonce == nonces[signer]);    nonces[signer]++;    // 执行转移    _transferFrom(from, to, tokenId);  }  // 计算要为转移签名的哈希  function getTransferHash(    address from, address to, uint256 tokenId, uint256 nonce  ) public view returns (bytes32) {    return keccak256(abi.encodePacked(      from, to, tokenId, nonce, address(this)    ));  }}清单 7-28

向 ERC721 合约添加原生的元交易。请注意，现在需要跟踪每个签名者的 nonce。

通过直接将此逻辑捆绑在奖励代币合约中，我们的用户可以直接签署由中继器发送并由 ERC721 合约执行的代币转账。这使得拥有现有账户的用户能够受益于元交易（这可能是由我们的应用程序补贴的），而无需部署身份合约。

#### 原生元交易中的奖励

将元交易逻辑直接移至应用合约可降低用户的复杂性，但同时引入了另一个难题：如何处理中继器的奖励。身份合约没有面临这个问题，因为它们已经持有用户的所有资产，所以它们可以直接将它们转移到中继器作为支付。

对于 ERC20 代币的情况，解决方案很简单：代币合约可以管理签名者的代币，并直接使用这些代币将奖励转移到交易的中继器（见列表 7-29）。// 08-meta-txs/contracts/ERC20WithNativeMetaTxs.solfunction signedTransfer(   address to, uint256 value,   uint256 nonce, **uint256 reward**, bytes memory signature) public {   bytes32 hash = getTransferHash(     to, value, nonce, reward   ).toEthSignedMessageHash();   address signer = hash.recover(signature);   require(nonce == nonces[signer]);   nonces[signer]++;   **_transfer(signer, msg.sender, reward);**   _transfer(signer, to, value);}列表 7-29

在支持元交易和中继器奖励的 ERC20 合约中的 signedTransfer 函数示例，使用相同的 ERC20 代币

然而，这个解决方案不允许在不同于相同代币的任何货币中进行奖励 - 例如，ETH 奖励在此方案下不可行。它也不能很好地转化为其他资产。转移 ERC721 非同质化代币的奖励会是什么呢？数字收藏品无法被削减并作为奖励给中继器。

解决这个问题的一种方法是依赖于 ERC20 的*批准*。回顾第三章节，ERC20 代币允许持有者指定其他地址来管理他们的资金。这样，用户可以向处理转发器奖励的应用合约授予其代币的批准，然后该合约将代币发送给转发器作为支付。然而，这种方法仍然需要用户有以太币来支付初始批准交易的燃气费用 - 除非奖励代币合约本身具有本地元交易支持批准。

另一个选择是简单地补贴用户的交易，并让应用本身支付给转发器。这需要应用合约中的谨慎逻辑来确定*何时*接受元交易 - 否则，恶意的转发器可能会向应用发送假交易并耗尽整个奖励池。这样的逻辑完全取决于您的用例，但请记住您有很大的灵活性：您的合约可能需要元交易附带应用密钥的额外签名，以便您可以在链下执行验证来批准交易。

### 重新审视智能账户部署

我们将再次讨论部署智能账户合约的过程。在“智能账户”部分，我们讨论了如何使用一次性地址来实现这一点，尽管它具有某些限制。我们现在将探讨另一种方法，支持转发器奖励，基于不同的 EVM 操作：CREATE2。

#### CREATE2 指令

以太坊自其最初版本以来，提供了一个 CREATE 指令，用于从另一个合约创建新合约。如前所述，新创建的合约地址是发送者地址和其 nonce 的函数。虽然这允许确定性部署，但这也意味着保留地址是棘手的，因为发送者不能发送除部署之外的任何其他交易，以防止更改其 nonce。

为了解决这个问题，引入了一个新的 CREATE2 指令。这个低级操作与 CREATE 类似，但还接受一个*salt*参数：部署地址现在是根据发送者、盐和合约创建代码计算的函数。这允许通过设置一个使用这个指令的工厂合约来启动合约，从而实现更加有趣的流程。工厂身份工厂带奖励 {  function deploy(    bytes code, uint256 salt  ) public returns (address) {    address deployed;    assembly {      deployed:= create2(0, add(code,0x20), mload(code), salt)      if iszero(extcodesize(deployed)) { revert(0, 0) }    }    return deployed;  }}

用户现在可以选择一个合约，连同其构造函数参数，生成一个随机盐，并知道结果合约将部署到的地址。不仅如此，*任何*知道这些参数的人现在都可以执行部署。

这意味着用户可以简单地共享创建参数和盐，以及要使用的工厂合约的地址，让任何中继执行交易，甚至不需要签名交易，而且肯定不需要支付任何 gas 费用。如果中继尝试修改代码或创建参数，则合约将部署到不同的地址。让我们使用这种方法来部署我们的身份合约，为中继提供奖励。

#### 部署奖励

在进入代码之前，我们需要定义如何管理对转发器的支付以及最初由用户资助的地址。

请回想一下之前方法的一个缺点是单次使用地址的用户需要从交易所资助一个地址，但是他或她的身份生成在另一个地址上。更糟糕的是，任何额外发送到单次使用地址的资金都将丢失。因此，如果我们可以让用户直接资助身份合约的地址，那将是可取的。

解决这个问题的最简单方法是在部署时由身份合约支付转发器奖励，也就是在其构造函数中（见 7-30）。在这种情况下，转发器根据定义是发起交易的账户 - 或者在 Solidity 中是 `tx.origin`。// 08-meta-txs/contracts/IdentityFactoryWithRewards.sol

修改后的身份合约，用于向交易的转发器支付奖励

这种方法允许用户简单地指定所有者账户和要支付的奖励，并广播这些参数以及选择的盐，因为仅这些值就足以确定部署地址。然后，任何转发器都可以接收此交易，验证部署地址上是否有足够的资金来支付奖励，并将交易发送到工厂合约。作为奖励，任何额外发送到部署地址的资金在合约创建后仍将保留在那里，准备供其所有者使用。

#### 身份合约工厂

工厂合同必须提供一个可由任何人调用的部署函数，接受身份合同部署参数和盐（见 7-31）。此函数组装创建代码并使用 CREATE2 指令执行实际创建。// 08-meta-txs/contracts/IdentityFactoryWithRewards.sol

IdentityFactory 合同的 deploy 函数。合同类型的 creationCode 属性返回创建时使用的字节码，任何构造函数参数只需附加在末尾。

请注意，无需验证所有者的签名，因为对创建参数的任何更改都会产生不同的部署地址，即没有资金用于支付回扣给中继者的地址。中继者应验证部署地址确实有足够的资金来支付回扣。

这个合约的一个补充是一个视图函数，用于根据构造函数参数和盐获取部署地址。 可以使用此函数告知用户他们的身份合约将部署在哪个地址上，也就是说，他们需要资助的地址。function getDeploymentAddress(  address owner, uint256 reward, uint256 salt) public view returns (address) {  bytes memory code = getCode(owner, reward);  bytes32 codeHash = keccak256(code);  bytes32 rawAddress = keccak256(    abi.encodePacked(      bytes1(0xff),      address(this),      salt,      codeHash    )  );  return address(bytes20(rawAddress << 96));}

使用这种策略，您可以预先计算出用户的身份将被创建的地址，然后将该地址与他或她共享。 用户确认该地址为自己的地址，并从交易所提供资金。 这反过来触发了中继在资金到位后在该地址创建身份合约。

### 注意

这种策略实际上可以通过使用单次使用地址而不是 CREATE2 来执行，使用稍微复杂的流程。 应用程序可以选择一个中继并创建一个单次使用地址，该地址将生成一个新的身份合约并向预先选择的中继发送奖励。 用户资助部署身份的地址后，中继再资助单次使用地址，执行部署并收到奖励。

## 以太坊名称

我们在本章中将解决的最后一个入职挑战是以太坊地址本身。 虽然地址对于任何以太坊应用程序都是至关重要的，因为它们标识了分散系统的参与者，但它们远非用户友好。 要求用户将他们的 40 个字符的明显胡言乱语字符串理解为他们的全局标识符并不是一个好的设计。 为了解决这个问题，我们将研究 ENS（以太坊名称服务）。

### 以太坊的 DNS

大多数 web 开发人员都熟悉 DNS（域名服务）的概念，这是一种将易于识别的域名（如“google.com”）映射到机器友好的地址（如 172.217.28.206）的协议，该地址标识了互联网协议中的服务器。^(18)

以太坊名称服务^(19)（或 ENS）是一种类似的协议，它将用户友好的名称（如“ethereumfoundation.eth”）解析为以太坊地址（例如此示例中的 0xfB6916095ca1df60bB79Ce92cE3Ea74c37c5d359，这是以太坊基金会的小费罐）。与 DNS 一样，它支持注册非地址记录（如内容哈希或纯文本），以及反向查找。

ENS 中涉及的组件大致模拟了 DNS 的组件，不同之处在于它们作为智能合约在以太坊网络中实现。ENS **注册表**本身是一个单例合约，用于跟踪所有域名及其所有者，并将每个域名映射到一个**解析器**。解析器合约提供了将名称解析为地址的方法，以及可选的附加信息，如文本、内容哈希或公钥记录。最后，ENS 注册表通过**注册器**进行更新，这些合约管理树的不同级别的子域名注册，每个级别都有自己的政策。

ENS 最广泛使用的顶级域是 .eth，^(20) 由所谓的 *.eth 永久注册商* 运营。该注册商使用一种提交-揭示方案来购买二级域名，并允许任何人为扩展名称注册做出贡献。虽然可以直接与此合约交互，但建议使用工具（如 mycrypto^(21) 或 myetherwallet^(22））来购买和管理您的二级域名。

### 名称解析

使您的应用程序具备 ENS 意识的关键部分是允许用户在需要地址的任何地方输入 ENS 名称。允许用户在应用程序中输入 ENS 名称而不是地址有助于抽象出以太坊地址的复杂性，这意味着您的用户需要掌握的概念少了一个。这相当于允许用户通过在浏览器中输入域名而不是强制他们键入其 IP 地址来导航至“google.com”。

与 DNS 类似，从 ENS 名称到地址的转换是一个称为*解析*的过程（见列表 7-32）。鉴于 ENS 的架构，解析名称是一个两步过程：首先，我们需要查询中央 ENS 注册表以获取名称的*解析器合约*的地址，然后查询解析器以获取该名称的实际*地址*。域名还需要通过一种称为*namehash*的过程进行规范化和哈希处理。^(23)// 09-ens/01-resolve.jsconst ensAddr = '0x314159265dd8dbb310642f98f50c066173c1259b';async function resolve (domain) {  let domainHash = namehash(domain);  let ens = new web3.eth.Contract(ensABI, ensAddr);  let resAddr = await ens.methods.resolver(domainHash).call();  let resolver = new web3.eth.Contract(resolverABI, resAddr);  return await resolver.methods.addr(domainHash).call();}列表 7-32

使用主网上的中央 ENS 注册表将域名解析为地址

由于名称解析是一个常见操作，因此几个库都会默认实现此操作。特别是，官方 ethereum-ens@0.7.6 javascript 包提供了大多数操作的绑定，使名称解析变得更加简单。$ let ens = new ENS(web3.eth.currentProvider);$ let domain = "ethereumfoundation.eth";$ await **ens.resolver(domain).addr()**;> 0xfB6916095ca1df60bB79Ce92cE3Ea74c37c5d359

对以太坊地址的用户进行抽象化还意味着您的应用程序在显示信息时必须使用以太坊名称而不是原始地址。如果您的用户输入一个用户友好的以太坊名称，而您的应用程序回答一个堆积如山的 40 个字符的十六进制字符串，那就不好了。

在 ENS 中支持反向解析是通过查询一个特殊的“addr.reverse”域来实现的，该域将地址映射到完整的以太坊名称。该域是与“eth”分开管理的，并且用户可以选择不在其中注册他们的地址 - 因此，并非每个具有以太坊名称的地址都会有反向解析记录。

### 注意

ENS 不会强制执行反向记录的正确性；这意味着任何人都可以注册他们的地址映射到“ethereumfoundation.eth”。为了防止这种情况发生，您应该始终对反向解析的结果进行正向名称解析，并验证它是否与原始地址匹配。

### 给我们的用户命名

ENS 是智能账户的完美匹配。我们不再要求用户记住智能合约的地址，而是允许他们为其分配一个以太坊名称。

正如在 DNS 中一样，我们可以在我们自己的域内分配名称，而不是直接从网络信息中心（NIC）购买二级域。电子邮件是这方面的一个很好的类比，也是用户习惯的事情 - 大多数人有一个由提供者管理的电子邮件帐户，比如 john@gmail.com，而不是由他们自己管理的，比如 hello@john.com。同样，在 ENS 中，我们可以为我们应用程序的每个用户分配一个子域，比如 *john.myapp.eth*。

要实现这一点，我们需要设置自己的注册器合约来管理我们的以太坊域名并管理所有子域名注册。我们将使用一个简单的 FIFS（先到先得）注册器合约，它将自由接受所有子域名注册。这和其他我们将要使用的合约的规范实现可以在 @ensdomains/ens@0.3.5 和 @ensdomains/resolver@0.1.3 包中找到。

第一步是实际获取一个域名。虽然在主网上这是一个非平凡的过程，但 ENS 在测试网络中为 .test 域提供了 FIFS 注册器，限制是这些注册会在 4 周后过期。让我们从在 Rinkeby 测试网上注册一个测试域名开始（见 7-33）。// 09-ens/02-register.js

在 Rinkeby 上注册以太坊域名 “myapp.test”。此代码片段中的哈希函数是 keccak256。

现在我们可以部署我们的 FIFS 注册器合约，它将自由分配“myapp.test”的子域，并将域名的所有权转让给它。// 部署新的注册器合约 let arguments = [ensAddress, namehash(domain)];let myRegistrar = await new web3.eth.Contract(fifsRegistrarABI) .deploy({ data: fifsRegistrarBytecode, arguments }) .send({ from: owner });// 将我们的域名所有权转让给我们的注册器 await ens.methodslet myRegistrarAddress = myRegistrar.options.address; .setOwner(namehash(domain), myRegistrarAddress) .send({ from: owner });现在，我们可以通过一个方法来使用此注册器在 ENS 上注册我们的身份合约（清单 7-34）。该方法包括三个步骤：

1.  1.

    在我们的注册器中注册一个自定义名称（即“john”），并任命身份合约为所有者。

1.  2.

    在 ENS 注册表中为新的身份名称（“john.myapp.test”）设置解析器。

1.  3.

    在前一步中的解析器中设置身份合约地址。

我们将使用*公共解析器*来完成第二步。公共解析器是一个公共合约，接受管理任何地址记录的请求，但仅限于该地址的所有者。这样可以避免我们为应用程序部署自定义解析器的麻烦。

### 注意

另一种方法是在我们的身份合约中添加解析器方法，并在解析请求时让身份返回其自身地址。然而，这会给我们的合约增加更多复杂性。

// 09-ens/contracts/IdentityWithENS.sol 合约 IdentityWithENS 是 Identity {  function registerENS(    bytes32 _hashLabel, bytes32 _node,    ENS ens, FIFSRegistrar registrar, PublicResolver resolver  ) onlyUserAccount public {    registrar.register(_hashLabel, address(this));    ens.setResolver(_node, address(resolver));    resolver.setAddr(_node, address(this));  }}清单 7-34

身份合约函数用于注册名称并将其映射到身份本身，使用我们的自定义注册器和公共解析器。 代码改编自 UniversalLoginSDK 仓库^(24)

然后，只需让我们的用户从他们的某个外部账户调用此函数，就可以在 ENS 上注册身份合约（见列表 7-35）。 请注意，注册名称的所有者设置为身份本身，因此用户最终保留了对其子域名的控制。const publicResolverAddress = '0xb14fdee4391732ea9d2267054ead2084684c0ad8';let userName = `john`;let userDomain = `${userName}.${domain}`;await identity.methods.registerENS( hash(userName), namehash(userDomain), ensAddress, myRegistrar.options.address, publicResolverAddress).send({ from: user });Listing 7-35

通过我们的自定义注册器和 Rinkeby 公共解析器将身份合约注册为 john.myapp.test。

对于每个新用户运行此流程，使他们可以使用我们应用提供的友好名称引用其身份 - 这个名称可以传递到其他应用程序，并用作全局以太坊身份，由 ENS 处理。

## 摘要

我们已经研究了几种处理用户入门和账户管理的工具和技术，使得这成为本书中最内容丰富的章节之一：回退函数、转发合约、一次性地址、本地账户、助记词、智能账户、可升级性、元交易、本地元交易、保留的部署地址以及以太坊名称等等。 所有这些技术在用户入门的不同方面都有所帮助，它们的权衡使得很难选择一个适合所有用例的解决方案。

用户入职工作在以太坊仍然是一个非常活跃的研究领域，而且在不久的将来肯定会开发出新的机制来增加你的工具箱。在撰写本文时，值得强调的是在 Universal Logins[²⁵] 下正在进行的工作。 Universal Logins 是一个框架，为用户创建智能账户，由每个设备上自动生成的本地账户自动管理，并支持元交易，以及为用户允许轻松连接到他们的账户的 ENS。 它还推动补贴早期用户行为，以简化入职流程，并奖励应用内为增加账户安全而尽最大努力的用户。

无论你实施什么解决方案，记住用户必须经过更多步骤才能开始使用你的应用，他们就越有可能放弃。另一方面，为了可用性而牺牲安全性是一个巨大的风险，因为“最糟糕的用户体验是当人们失去他们的加密货币。”[²⁶] 找到在你正在构建的用例中两者之间的完美折衷是一项艰巨的任务。
