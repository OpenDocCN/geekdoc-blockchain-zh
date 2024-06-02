© Santiago Palladino 2019S. Palladino《面向 Web 开发者的以太坊》[`doi.org/10.1007/978-1-4842-5278-9_8`](https://doi.org/10.1007/978-1-4842-5278-9_8)

# 8. 可扩展性

Santiago Palladino^(1 )(1)阿根廷布宜诺斯艾利斯自治市

在上一章中，我们解决了用户入门挑战，这是以太坊大规模采用的两个主要问题之一。第二个问题是可扩展性，我们将在本章中讨论。以太坊网络，就目前而言，每秒可以处理约 15 笔交易——而这个吞吐量必须在全球范围内的所有以太坊应用之间共享。这导致单个应用在使用量激增的情况下将整个网络拥塞，使得所有 dapp 在短时间内无法使用。在本章中，我们将介绍状态通道和侧链，这两种最广泛使用的可扩展性解决方案。

## 什么是第二层？

以太坊区块链可以看作是一个全球单一的数据库，复制到网络中的每个节点，需要处理每个发送的交易。仅仅这一点，甚至没有考虑块传播时间或工作证明，已经对可以处理的交易量施加了限制。

> *核心限制在于，像以太坊这样的公共区块链要求每个交易都由网络中的每个节点处理。(...) 这是设计之中的——这是使公共区块链具有权威性的一部分。节点无需依赖他人告诉他们区块链的当前状态。(...) 这给以太坊的交易吞吐量设置了一个基本限制：它不能高于我们愿意要求单个节点的水平。*
> 
> —Josh Stark，《理解以太坊的第二层扩展解决方案：状态通道、Plasma 和 Truebit》^(1)

但是，如果我们*不要求*每笔交易都通过整个网络运行会怎样呢？例如，一组交易，在一小群参与者之间运行，可以在一个单独的网络上处理。只有在一定的时间后，产生的余额才能上传到主要的以太坊网络。

这些并行（或*侧*）网络需要某些安全保障 - 否则，我们可以只使用常规数据库。关键在于，这些网络可以依赖于主网络作为安全的去中心化基础层，上面可以构建新的共识机制。因此，这些可伸缩性解决方案被认为属于*第二层*，因为它们不是作为以太坊协议本身的一部分构建的，而是在其之上构建的。今天，有三种主要类型的第二层解决方案：

+   *通道*是短暂的闭合网络，通常在两个参与者之间，在其中它们相互交换多个交易。每个参与方都必须通过签名来确认每笔交易。为了打开通道，他们首先必须在以太坊网络上的智能合约上存入押金。然后，该合约可以验证他们的签名，在需要时执行支付。

+   *侧链*是使用不同于主网络的共识算法的并行网络，例如权威证明或股权证明。这些通常与主网络桥接，允许用户在侧链和主链之间转移资产。侧链的一种变体是*Plasma 链*，其中侧链的良好行为可以通过主网络上的智能合约完全执行。

+   *外部计算*解决方案并不提供更高的交易吞吐量，但它们确实允许在每个交易中执行更有趣的任务。它们在主网络之外运行计算密集型任务，这些任务在以太坊虚拟机上运行将是成本高昂的，并将结果注入回去。

在本章中，我们将探讨前两个解决方案。如今，有几个团队正在研究每个解决方案的实施或新的变体。我们将沿途提到其中一些，但在尝试每个解决方案之前，我们也会自己做些尝试。^(2)

## 通道

通道是一个涵盖了许多不同变体的第二层可扩展性解决方案家族，从单向支付通道到反事实广义状态通道。它们也可以推广到完整的通道网络，而不是孤立的点对点解决方案。

我们将从*支付通道*开始。^(3) 在支付通道中，两个或更多参与者通过在主网络上进行初始存款来开启通道，然后在通道之外执行多笔支付。然后，这些支付会在主网络上的智能合约上被可信地结算。

### 单向支付通道

支付通道的最简单变体是*单向支付通道*。在这里，有两个不同的参与方：接收方和发送方。通常是一个提供者，在一段时间内提供服务并收集多笔支付，以及执行这些支付的用户。这在游戏中进行微交易的玩家是一个很好的例子。

#### 通道是如何工作的？

让我们假设一个场景，用户需要向服务提供者进行多次小额购买。服务提供者提供什么并不重要，只要用户需要在一段时间内向同一接收方进行多笔支付，并且提供者需要每笔小额支付的证明来继续提供服务。

如果每一笔小支付都在区块链上作为交易进行，累积的交易手续费可能对实际支付产生相当大的影响。为每一笔 20 美分的支付向网络支付 20 美分的费用并不划算。此外，由于服务提供商要求在每次支付后进行验证，确认时间将不断给服务增加显著的延迟。

一种解决方案可能是由可信任的第三方从用户收取大额的初始存款，并监控提供的服务。然后用户用他们的私钥对每一笔*微交易*进行签名，承认每笔要付款项。在所有的微支付都完成后，第三方会发布一个包括总支付给服务提供商和将剩余的初始存款退还给用户的单一链上交易。假设用户和服务提供商都信任这个第三方，这可以将所有的微支付减少到网络上的仅两笔交易：一笔是存款，另一笔是支付。

*单向支付通道*是使用智能合约作为可信第三方的一种实现方案。用户在部署支付通道智能合约并存入初始存款时，“开启”对服务提供者的支付通道。用户直接向服务提供者发送每笔微支付作为*签名消息*。这些消息不是通过以太坊网络发送的，而是通过一个独立的协议，比如 HTTPS，全部是在链下进行的。当服务提供商想要兑现时，他们可以向支付通道智能合约提交签名消息并收取他们的支付（图 8-1）。![../images/476252_1_En_8_Chapter/476252_1_En_8_Fig1_HTML.png](img/476252_1_En_8_Fig1_HTML.png)

图 8-1

支付通道的流程图。用户首先用初始的 1 ETH 存款打开通道。每当用户需要向服务提供商进行微支付时，他们会签署一条带有累积支付金额的消息并将其发送到链下。当提供商想要兑现时，他们会向合约提交最新签署的消息并收到他们的支付。

在支付通道内，大多数交易完全发生在链下，直接从用户发送到接收方。这就是为什么通道被认为是一个*第二层*解决方案，建立在主以太坊网络，即*第一层*之上，同时继承了许多其安全属性。

与第一层相比，通道具有一些非常有趣的优势。通道一旦打开，通过它发送的任何交易都没有 gas 费用，并且一旦发送，它们也可以被视为立即完成，因为无需等待任何区块被挖掘来确认它。此外，由于交易是在两个参与者之间交换的，因此在提交到区块链之前，它们完全是私密的。

#### 实现单向通道

为了说明单向支付通道的工作原理，我们将从零开始实现一个（见 8-1）。我们的支付通道将有一个发送者和一个接收者，将由发送者提供初始存款，并设定一个预定的结束时间。在指定的结束时间之后，如果接收者没有收取他们的付款，发送者将被允许取回存款。如果服务提供商从未提交付款消息，这个机制就是必需的，以防止用户存款永远被锁定在合约中。// contracts/PaymentChannel.solpragma solidity ⁰.5.0;import "openzeppelin-solidity/contracts/cryptography/ECDSA.sol";contract PaymentChannel {  using ECDSA for bytes32;  address payable sender;  address payable recipient;  uint256 endTime;  bool closed;  constructor(    address payable _recipient, uint256 _endTime  ) public payable {    sender = msg.sender;    recipient = _recipient;    endTime = _endTime;  }}Listing 8-1

单向支付通道合约的定义、状态变量和构造函数。我们将使用 openzeppelin-solidity@2.1 中的 ECDSA 库来验证合约上的签名。请注意，构造函数是可支付的，因此发送者可以在部署时进行初始存款。

由于大多数支付通道中的交易发生在链下，我们只需要实现两个方法。第一个方法，close，将由服务提供商调用以提交发送者的带有支付的签名，收取他们的资金，并关闭通道（见 8-2）。

### 注意

我们要求发送者始终签署消息以支付给接收者的总额。这使我们只需向合约提交一个已签名的消息，而不是处理多个消息。

此方法仅可由收款方调用，以防止发送方尝试使用他们签名的零值消息过早关闭通道。此外，由于发送方可以为大于通道中存款的总价值签署消息，因此我们需要限制转入合约余额的价值。由收款方决定是否接受比通道实际支付的更高价值的付款通知。^(4)

向收款方支付完成后，剩余的存款全部返还给发送方。由于此时通道合约已无进一步用处，我们还将销毁合约以获得少量的燃气退款。// contracts/PaymentChannel.sol 函数 close(  uint256 value, bytes memory signature) public {  require(msg.sender == recipient);  bytes32 hash = keccak256(    abi.encodePacked(value, address(this))  ).toEthSignedMessage();  address signer = hash.recover(signature);  require(signer == sender);  uint256 funds = address(this).balance;  recipient.transfer(funds < value ? funds : value);  selfdestruct(sender); // 销毁合约，将资金发送给发送方}Listing 8-2

收款方关闭支付通道。这需要提交发送方签名的消息，其中包含要转移的价值。请注意，签名的消息还包括合约地址，以防止在具有相同发送方的其他通道上进行重放攻击。

要实现的第二个函数对应于不愉快的情况，即收款方从不调用关闭函数，而发送方在预定的结束期间终止合约（见 8-3）。// contracts/PaymentChannel.sol 函数 forceClose() public {  require(now > endTime);  require(msg.sender == sender);  selfdestruct(sender);}Listing 8-3

如果收款方从未兑现，则发送方强制关闭通道以恢复存款。

这种实现可以修改为交换 ERC20 代币而不是 ETH，从而打开*代币支付通道*的大门。发送方不再需要存入 ETH 的初始押金，而是必须将 ERC20 代币转移到通道合约作为押金。一旦通道关闭，这些代币就会再次转移。请参考代码示例中的 TokenPaymentChannel.sol 进行实现。

#### 构建支付应用程序

现在，我们将使用我们的合约来构建一个简单的应用程序，在这个应用程序中，发送方可以与接收方建立支付通道合约，通过直接的离线连接发送多笔微支付，最终结算。与前几章一样，我们将使用 create-react-app 作为样板。

为了保持应用程序的简单性，我们将在同一台计算机的同一应用程序中打开的两个浏览器窗口之间建立连接，其中一个充当发送方，另一个充当接收方。我们将使用*广播通道*^(5)在两个浏览器窗口之间传递消息。在真实的应用程序中，您会想要使用不同的方法，比如*WebRTC 数据通道*^(6)以及一个服务器来管理用户之间的发现。

我们将进行另一个简化：不使用 Metamask，而是直接从 Web 应用程序中管理帐户。这是为了避免在同一台计算机的同一应用程序中模拟两个不同帐户与相同应用程序交互时遇到的困难。我们将直接调用 ganache 从发送方和接收方帐户发送交易，并在需要时签署消息。

我们的应用程序将由两个主要视图构建：一个为发送方，一个为接收方，都由一个根 App 组件设置。它将是 App 的责任来设置 web3 对象，并将发送方和接收方地址注入组件中。有关其实现，请参阅代码示例中的 src/App.js。

让我们从发送者视角开始。开启通道将由发送者负责，通过部署智能合约并进行初始存款（见 8-4）。完成此操作后，我们将通过广播通道通知接收者。我们将使用自定义协议进行通信，在这种情况下，我们通过一个动作参数识别不同的消息类型，其值为 CHANNEL_DEPLOYED。// src/components/Sender.jsasync deployChannel(deposit) {  const { web3, sender, recipient } = this.props;  // 部署合约并转移初始存款  const from = sender;  const endTime = +(new Date()) +(300 * 1000); // 5 min from now  const channel = await PaymentChannel(web3)    .deploy({ arguments: [recipient, endTime] })    .send({ value: deposit.toString(), from, gas: 1e6 });  // 通过广播通道通知接收者  const address = channel.options.address;  this.broadcastChannel.postMessage({    action: "CHANNEL_DEPLOYED", address  });  // 使用存款和通道对象更新发送者状态  this.setState({ channel, deposit, sent: BN(0) });}8-4 清单

发送者组件函数，用于部署支付通道合约，资助它，并通知接收者已部署。应用组件将 web3 实例和发送者和接收者地址作为 props 传递。在这里，PaymentChannel 是一个返回新的 web3 合约实例的函数，而 BN 是一个 BigNumber 构造函数。

我们将此函数连接到一个简单的表单（见 8-2），在该表单中，我们要求用户选择要在通道上存入的 ETH 金额。![../images/476252_1_En_8_Chapter/476252_1_En_8_Fig2_HTML.jpg](img/476252_1_En_8_Fig2_HTML.jpg)

图 8-2

简单的支付通道部署表单。此表单的代码可以在 src/components/CreateChannel.js 中找到。

一旦通道部署完成，我们的用户应该能够向收件人发送微支付^(7)（见 8-5）。这意味着签署消息（而不是发送交易），其中包括了一旦通道关闭时要支付给收件人的总以太币金额。这些消息通过相同的广播通道以不同的操作标识符发送给收件人。// src/components/Sender.jsasync sendEth(value) {  const { web3, sender } = this.props;  const { sent, channel } = this.state;  // 计算新的累积以太币发送量  const newSent = sent.plus(value);  // 使用发送者的密钥进行签名  const signature = await signPayment(    web3, newSent, channel.options.address, sender  );  // 将消息发送给收件人  this.broadcastChannel.postMessage({    action: "PAYMENT", sent: newSent.toString(), signature  });  // 使用新的累积以太币发送量更新状态  this.setState({ sent: newSent });}Listing 8-5

发件人功能，用于向收件人发送微支付。每条消息携带要支付的以太币总额。该组件需要跟踪到目前为止已发送的总量，因此用户选择的微支付金额会在签名和发送之前添加到该值中。

签名是根据要支付的总值的哈希和通道地址计算的（见 8-6）。在签名中包含通道地址可以防止*重放攻击*，即在同一用户打开的另一个通道中重用相同的消息。// src/contracts/PaymentChannel.jsasync function signPayment(web3, value, address, sender) {  const hash = web3.utils.soliditySha3(    { type: 'uint256', value: value.toString() },    { type: 'address', value: address }  );  const signature = await web3.eth.sign(hash, sender);  return signature;}Listing 8-6

使用 web3 对每个微支付消息进行签名^(8)

类似于通道部署，这个动作以一个简单的形式呈现给用户，在这个形式中，用户选择要转移的金额（图 8-3）。我们还可以显示有关通道的一些基本统计信息，如其地址、总存款和到目前为止已经承诺了多少 ETH。

图 8-3

展示用户通道信息并请求通过通道发送的值。这些组件的代码可以在 src/components/ChannelStats.js 和 src/components/SendEther.js 中找到。

### 注意

为了简洁起见，在这个例子中，我们将跳过发送者在示例中调用 forceClose 的实现。

我们现在可以把重点转向接收者视图了。在我们的应用程序中，接收者除了监视发送者的操作之外什么也不需要做，直到他们决定兑现。我们将首先为发送者的消息安装一个监听器，以便对其做出反应（见列表 8-7），根据消息动作调用不同的函数（见列表 8-8）。// src/components/Recipient.jsconst bc = new BroadcastChannel('payments');bc.onmessage = (evt) => this.handleMessage(evt.data);this.broadcastChannel = bc;Listing 8-7

初始化一个新的广播通道以接收来自发送者的消息并添加事件处理程序。此代码是 Recipient 组件构造函数的一部分。

// src/components/Recipient.jshandleMessage(data) {  const action = data.action;  switch (action) {    case "CHANNEL_DEPLOYED":      this.onChannelDeployed(data);      break;    case "PAYMENT":      this.onPaymentReceived(data);      break;    default:      console.error("Unexpected message", data);  }}Listing 8-8

委托给不同的处理程序函数，根据消息动作进行区分。

首先让我们看一下收件人应如何对部署的新通道做出反应（清单 8-9）。除了通过添加对通道的引用来更新自己的状态之外，收件人还应检查通道的存款以了解发送方能够支付的最大金额。收件人还应检查部署的合同确实是一个付款通道。我们可以通过检查部署的字节码是否与通道的代码匹配来做到这一点（清单 8-10）。// src/components/Recipient.js 异步 onChannelDeployed（数据）{  const { web3 } = this.props;  if（！await checkBytecode（web3，data.address））{    console.error（"合同字节码不匹配"）;    返回;  }  const deposit = await web3.eth.getBalance（data.address）;  这.setState（{    channel：PaymentChannel（web3，data.address），    存款：BN（存款），    received：BN（0）  }）;}清单 8-9

收件人通过验证新部署的通道来做出反应，检索其存款，并更新自己的状态。在这里，PaymentChannel 是一个在指定地址返回 web3 合同实例的函数

// src/components/Recipient.js 异步函数检查字节码（web3，地址）{  const actual = await web3.eth.getCode（地址）;  const { compilerOutput } = Artifact;  const expected = compilerOutput.evm.deployedBytecode.object;  return actual === expected;}清单 8-10

验证地址部署的字节码与合同编译的字节码相匹配。请注意，我们检查合同的 deployedBytecode，而不是字节码，因为后者包括未保存在区块链中的构造函数代码

收款方必须处理的另一条消息是支付消息。在这里，我们需要验证发送者的签名，并使用最新传输的值更新收款方状态（见列表 8-11）。我们还需要保存关联的签名，因为我们将需要它来关闭通道。

收款方对支付消息做出反应，更新收到的总 ETH 数量和相应的签名。验证每条消息意味着恢复签名地址并检查其与发送者是否匹配，因为无效的签名将产生不同的签名地址。我们还会丢弃任何总支付金额少于最新总额的消息。

然后，可以使用 web3 库中的 recover 方法来实现恢复发送者的签名（见列表 8-12）。

恢复支付消息签名者的辅助函数。请注意，签名恢复的哈希与 signPayment 方法中计算的完全相同。

收件人展示了通道的当前状态，总共接收到的以太币数量，以及随时关闭通道的选项（图 8-4）。![../images/476252_1_En_8_Chapter/476252_1_En_8_Fig4_HTML.jpg](img/476252_1_En_8_Fig4_HTML.jpg)

图 8-4

收件人接口，显示当前余额和通道状态信息，包括通过通道发送的以太币数量

收件人实现的最后一步是通过向通道合约发送带有最新值和签名的交易来关闭通道（参见 8-13）。这将通过向收件人发送累积值并将存款余额返回给发送者来结算所有的微支付。

收件人使用发送者发送的最新值和签名关闭通道

调用此方法后，频道合约应被销毁，并且收件人应该已经收到发送者所做的所有微支付的总和。

现在我们已经建立了一个建立在单向支付通道之上的工作应用程序，是时候进入更有趣的通道变体了。

### 双向支付通道

另一种支付通道的场景是两个相等的参与方之间互换资金。不再有区分发送者和接收者，通道中的每个参与者都可以发送和接收资金。

参与者角色的对称性使得通道实现更加困难。在这个模型中，这两个参与者中的哪一个应该被允许关闭通道？由于他们是平等的，他们都应该被允许这样做，但这引入了一个问题。

假设 Alice 和 Bob 正在进行微交易。在某个时刻，Bob 通过通道向 Alice 发送了一笔非常大的付款，但在她能兑现之前，他向通道提交了一条旧消息并关闭了通道。然后问题是，恶意参与者可以在方便的时候尝试将通道关闭至*更早状态*（见图 8-5）。![../images/476252_1_En_8_Chapter/476252_1_En_8_Fig5_HTML.jpg](img/476252_1_En_8_Fig5_HTML.jpg)

图 8-5

Bob 尝试使用更旧的状态关闭通道的双向支付通道场景，损害了 Alice

#### 挑战期

通过在通道关闭时添加*挑战期*来解决这种情况。当 Bob 请求关闭通道时，通道进入“关闭”状态一段固定时间。在此期间，Alice 可以确认通道关闭，或者她可以提交更近期的状态并开始新的关闭期（见图 8-6）。

如果在挑战期内她未向通道发送任何交易，则通道关闭，并根据 Bob 提交的状态执行支付。这种情况等同于接收方未提交消息并导致发送方进行强制关闭。因此，添加挑战期可消除通道的预定义结束时间需求。

### 注意

挑战期是第二层解决方案中非常常见的机制，不仅限于通道，正如我们将在本章后面看到的那样。这使得可以单方面执行一个动作，而无需从每个其他参与方收集确认，但仍然让它们注意到不法行为并采取行动。

这种机制要求智能合约识别一条消息是否比另一条消息*更新*。换句话说，它需要在 Alice 和 Bob 之间交换的消息中添加*排序*的概念。在先前的示例中，这使得通道能够验证 Alice 的消息比 Bob 的消息更新，并因此放弃 Bob 的消息而选择 Alice 的消息。

这种排序是通过在每条消息中添加一个计数器或*nonce*来处理的，该计数器随每条发送的消息增加。双方都应验证 nonce 在每条消息上是否正确增加：如果其中一方收到带有重复 nonce 的签名消息，他们应立即丢弃它。![../images/476252_1_En_8_Chapter/476252_1_En_8_Fig6_HTML.png](img/476252_1_En_8_Fig6_HTML.png)

图 8-6

继续前一个场景。Alice 看到 Bob 试图提交一个旧状态，并提交 S2 作为回应。挑战期结束后，合约根据提交的最新状态 S2 执行支付。

这些挑战机制有一个重要的缺点：通道中的各方不能离线时间超过挑战期限的长度。在我们的 Alice 和 Bob 示例中，如果通道的挑战期限为几个小时，Bob 可以在 Alice 离线时提交对他方便的状态，因此当她重新上线时，通道已经关闭。另一方面，极长的挑战期限可能导致存款长时间被锁定，如果 Bob 试图合理关闭通道而 Alice 从未接受关闭。选择正确的挑战期限将严重依赖通道部署的用例。

### 注意

作为通道的补充，有*监视塔*服务，可以代表用户监视通道，以防他们离线并且他们的对方试图非法关闭通道。这些提供者可能会要求按通道中锁定的价值比例收取服务费。

#### 一个样本交换

为了确保激励是对齐的，Alice 签署了在余额对 Bob 有利变化的消息，反之亦然。一个示例场景，其中两者都以 1 ETH 的存款开始，可能是以下情况：

+   Alice 通过签署余额（0.6, 1.4）^(9) 使用 nonce 1 签署了 0.4 ETH。

+   Bob 签署了 0.3 ETH，通过签署余额（0.9, 1.1），使用 nonce 2。

+   Alice 通过签署余额（0.8, 1.2）使用 nonce 3 签署了 0.1 ETH。

+   Alice 通过签署余额（0.7, 1.3）使用 nonce 4 签署了 0.1 ETH。

让我们根据这组消息进行一些可能的情景分析：

+   当交换结束时，Bob 正当地选择了由 Alice 签署的最新消息，并将其用于关闭通道。请注意，对他来说选择 nonce 3 而不是 4 永远没有意义，因为 4 对他更有利，因为它对应了 Alice 的一次支付。

+   Bob 没有签署另一条消息，也没有关闭通道。作为回应，Alice 上传了对她有利的最后一条消息：由 Bob 签署的最后一条（nonce 2）。她没有理由提交任何更近的消息，其中她进行了额外的支付。或者，她也可以尝试关闭通道，就好像没有交换过任何消息一样。

+   Alice 恶意上传了具有 nonce 2 的消息，试图关闭通道。Bob 应立即提交更近的消息，最好是具有 nonce 4 的消息。

+   Bob 恶意尝试关闭具有 nonce 1 的消息的通道，在该消息中，余额对他最有利。然后，Alice 应提交具有 nonce 2 的消息作为回应，因为这对她更有利。这将我们带回了之前的情景，Bob 应提交 nonce 4。

如我们所见，通过使用逐笔支付时递增的 nonce 对消息进行签名，参与者被激励始终提交其对方签署的最新消息。这导致最近的消息被用于关闭通道。

#### 实现双向通道

现在我们将实现一个示例双向状态通道（见列表 8-14）。在我们的实现中，任何用户都可以通过提供对方用户的签名消息来请求通道的关闭。然后可以在对方确认或挑战期结束时执行支付。

我们的通道将跟踪每个用户的余额，初始为他们各自存入的押金。通道由其中一个用户创建，然后由第二个用户加入，当他们自己存入押金时。^(10)contract BidirectionalPaymentChannel {  using ECDSA for bytes32;  uint256 constant closePeriod = 1 days;  address payable user1;  address payable user2;  uint256 balance1;  uint256 balance2;  uint256 lastNonce;  uint256 closeTime;  address closeRequestedBy;  constructor(address payable _user2) public payable {    balance1 = msg.value;    user1 = msg.sender;    user2 = _user2;  }  function join() public payable {    require(msg.sender == user2 && balance2 == 0);    balance2 = msg.value;  }}列表 8-14

我们双向状态通道实现的合约变量和初始化函数。我们使用的是与单向实现相同的 ECDSA 库。

准备就绪后，我们现在可以查看合同的关闭函数（见 8-15）。此函数与单向通道中的函数类似，因为它验证了用户对状态的签名。然而，与立即执行支付不同的是，它开始了挑战（或关闭）期。函数 closeWithState(  uint256 newBalance1, uint256 newBalance2,  uint256 nonce, bytes memory signature) public {  // 检查发件人是否为用户，状态是否正常，如果挑战，则 nonce 是否增加  require(msg.sender == user1 || msg.sender == user2);  require(nonce > lastNonce);  require(newBalance1 + newBalance2 == address(this).balance);  // 验证签名是否属于另一个用户  bytes32 hash = keccak256(abi.encodePacked(    newBalance1, newBalance2, nonce, address(this)  )).toEthSignedMessageHash();  address signer = hash.recover(signature);  require(signer == user1 || signer == user2);  require(signer != msg.sender);  // 更新余额、nonce，并开始挑战期  balance1 = newBalance1;  balance2 = newBalance2;  lastNonce = nonce;  closeRequestedBy = msg.sender;  closeTime = now;}见 8-15

为双向状态通道关闭的结束函数。只要参与者之一提交了由另一用户签名的消息，并且其 nonce 比上一次提交的新（如果有的话），就可以调用该函数。

现在，我们需要添加一个实际关闭通道的函数，可由未在首次发起关闭的用户或在挑战期结束后调用（见 8-16）。函数 confirmClose() public {  require(msg.sender == user1 || msg.sender == user2);  bool challengeEnded = closeTime != 0    && closeTime + closePeriod > now;  require(closeRequestedBy != msg.sender || challengeEnded);  user2.send(balance2);  selfdestruct(user1);}见 8-16

有效地关闭双向支付通道并执行支付。

### 注意

我们在 confirmClose 中使用 send 而不是 transfer 来防止攻击。如果 user2 是一个合约账户而不是 EOA，它可以被编码为在每笔传入交易时回滚。这将使得 user1 无法关闭通道并恢复初始存款，因为对 user2 的转账调用将失败，并回滚整个交易。通过使用 send，以太币的发送可能会失败，但关闭允许成功进行。

我们的实现需要最后一个函数才能完成。如果其中一个用户从未签署任何消息，另一个用户需要能够请求关闭，并将初始存款退还给每个用户（见 8-17）。否则，首先创建通道的用户的资金可能会永久锁定。函数 close() public {  require(msg.sender == user1 || msg.sender == user2);  require(closeTime == 0);  closeRequestedBy = msg.sender;  closeTime = now;}Listing 8-17

从初始状态开始关闭通道

请注意，任何用户仍然可以在关闭后调用 closeWithState，以防某一方恶意尝试在初始状态下关闭通道。

#### 优化和扩展

到目前为止，我们已经审查过的支付通道实现相对简单，但仍有很大的改进空间：

+   一种可能的优化是使用*单一合约*来管理所有通道。与为每个通道部署一个合约相反，每个通道实际上是存储在单个支付通道合约中的结构。这大大降低了创建新通道的成本，但以增加的复杂性为代价。此外，它将所有参与者的资金集中在单个合约中，为可能使攻击者同时从所有通道中提取资金的错误打开了大门。

+   通道也可以修改为可重用。在我们的实现中，我们要求在执行支付之前关闭通道，但在支付执行后可以保持通道开放。这允许部分资金被提取用于其他应用，而无需销毁通道合约。

+   对于双向通道，可以通过添加由两个用户签署的特殊消息来优化通道关闭，该消息表示在某个状态下达成的协议完成。这条消息可以由任何参与者上传，并且不需要第二笔交易来确认关闭或经过挑战期。

+   通道的一个有趣扩展是增加参与者的数量。尽管在我们的所有示例中，我们探讨了具有两个成员的点对点通道，但更多用户可以参与其中。随着用户数量的增加，协调可能会变得更加复杂，因为可能需要多个通道参与者签署消息才能被视为有效。

### 状态通道

支付通道可以看作是一种更普遍的通道类别的特例，称为*状态通道*。与两个方当事人交换有关待支付余额状态的签名消息不同，状态通道允许用户交换关于*任何状态*的消息。

举例来说，一个简单的游戏可以通过状态通道进行。玩家可以在游戏状态上签署消息，例如棋盘上的棋子摆放。移动棋子通过发送带有移动或棋盘新配置的签名消息完成。

状态通道通常涉及初始存款和支付，就像支付通道一样。规定支付条件的是游戏，并且可以由智能合约在链上执行。

#### 将游戏编码到状态通道中

回合制游戏是状态通道的一个绝佳应用案例，因为它们具有一些有用的特性。首先，所有游戏状态都可以在消息之间安全地交换，并在需要时在链上处理。此外，在任何时刻，都很明确哪位玩家应该下一步行动，并且关于谁先行动的争论是不存在的。此外，游戏的状态是解决挑战所需的全部内容，因为它们不依赖于任何外部状态。^(11)

让我们以井字棋游戏为例。状态可以定义为一个 3x3 的矩阵，每个单元格有三个可能的值：圆圈、叉叉或空白。游戏规则容易编码，以及获胜（或平局）的条件。

在这里，玩家将通过他们的动作交换消息，每个动作只能是放下他们的一个标记。然而，与支付通道不同，每个动作（即每个消息）都对进行动作的玩家（签名者）有利，而不是对接收者有利。这带来了一个重大的机制转变：玩家不再被激励发布对手提交的最新状态，而是最后由自己做出的动作。让我们看一个例子：

+   Alice 在中间放置 X，因此她签署了一个消息，只有中间有一个 X 和 nonce 1，然后将其发送给 Bob。

+   Bob 在中右角放置 O，使用 nonce 2 签名，然后将其发送给 Alice。

+   Alice 在右上角放置 X，使用 nonce 3 签名，然后将其发送给 Bob。

+   Bob 在中左角放置 O，使用 nonce 4 签名，然后将其发送给 Alice。

+   Alice 在左下角放置 X 获胜，使用 nonce 5 签名，然后将其发送给 Bob。

然后，棋盘如下所示，下标表示每次移动的回合：

|   |   | X[3] |
| --- | --- | --- |
| O[4] | X[1] | O[2] |
| X[5] |   |   |

在最后一步之后，鲍勃应该签署由爱丽丝收到的消息并将其发送回给她，这样她就可以将其上传到链上并要求奖励。然而，如果鲍勃是一个输不起的人，他可以拒绝这样做。在这种情况下，爱丽丝必须能够仅仅在链上上传由鲍勃签名的最后状态（4），以及她的获胜移动，并且让状态通道验证她已经赢得比赛。请注意，这要求**状态通道必须能够验证她的移动确实是有效且是获胜的移动**。

鲍勃也可以简单地拖延比赛。例如，当他收到来自爱丽丝的消息 3 时，他注意到自己将输掉比赛时，他可以选择停止比赛。在这种情况下，爱丽丝必须能够在链上使用鲍勃的最后签名状态（2）以及她的后续移动（3），并*挑战*鲍勃移动。如果他在分配的时间内没有在链上作出回应，那么状态通道应该宣布爱丽丝为赢家。在这里，我们不仅使用挑战期限来进行关闭，还用于强制移动。

正如我们所说，状态通道必须能够*验证*在链上的移动是否有效。让我们看一个清楚表明这种需求的场景：鲍勃决定忽略来自爱丽丝的获胜消息 5，而不是在他接收到该消息时停顿。然后，他挑战她在链上使用虚假状态进行移动。他取得了爱丽丝之前的签名状态（3），并向合约提交了一个带有以下无效棋盘的新状态：

| X[3] |   |   |
| --- | --- | --- |
|   | X[1] | O[2] |
|   |   | O[4] |

如果状态通道合约无法验证他的移动无效（他改变了 X[3] 的位置），那么爱丽丝将被迫在这个无效棋盘上作出链上的移动。

### 注意

使状态通道合约验证每个转换的替代方法是默认接受所有转换，但接受证明某个移动是无效的。在某些情况下，验证转换无效的证明可能比验证转换本身更容易。国际象棋是一个很好的例子：验证将军可能会在气体使用方面成本过高。解决这个问题的方法是允许任何玩家宣称将军，并让对手证明这不是事实，方法是提交任何有效的移动。^(12) 这种模式只是挑战-响应的另一种形式，并遵循智能合约的座右铭“*验证，不计算*”。

与常规支付通道相比，状态通道本质上更复杂，因为它们需要验证正在进行的游戏的逻辑以验证状态转换。

### 注意

对于支付通道描述的大多数优化也适用于状态通道。例如，可能可以在状态通道上的两个参与者之间运行多个游戏实例，而无需每次想要重新比赛时都关闭和打开新通道。此外，可以设置状态通道以使其存款为 ERC20 甚至非同质化的 ERC721 代币——想象一下将奖杯表示为数字收藏品！

#### 广义状态通道

正如我们所见，给定游戏的状态通道有两个主要责任：管理通道本身和验证游戏的转换。这使得实现更加复杂，因为两个责任的逻辑交织在一起。它还使状态通道合约更加昂贵，因为它们需要包含通道和游戏的逻辑。

这导致了*广义状态通道*框架的发展。广义状态通道是管理用户存款并允许新游戏或应用程序逐步*安装*到通道上的通道。这有效地将状态通道逻辑与应用程序逻辑分离开来。

> 通用状态通道将区块链应用程序的所有链上状态组件移到链下。与要求每个应用程序开发者从头构建整个状态通道架构不同，通用状态通道的通用框架是一种其中状态只需存入一次，然后之后任何应用程序或一组应用程序都可以使用的框架。
> 
> —Jeff Coleman、Liam Horne 和 Li Xuanji，《反事实：通用状态通道》^(13)

这打开了一个新的通道复用级别。用户现在可以在同一个通道上玩多个游戏实例，甚至玩多个不同的游戏，从而在单个通道内创建几个子通道。此外，我们可以在这些子通道之间建立依赖关系，例如只有在一组游戏子通道解决后才触发支付通道。

通用状态通道解决方案正在由不同团队积极开发，尽管有工作朝着提供一定程度的相互操作性的共同标准方向进行。其中一些实现，例如来自 Counterfactual 团队的实现，依赖于*反事实*行动的概念。在这里，“反事实”一词用来指代通道中的任何参与者都可以在链上采取的行动，但实际上并没有采取，这会导致参与者表现得好像它实际上已经发生过一样。^(14) 让我们看看这意味着什么。

在我们的井字游戏状态通道中，我们可以说如果有一个由 Alice 和 Bob 都签署的状态，显示 Alice 赢得了比赛，那么 Alice 已经*反事实地*赢得了比赛。两名玩家都知道他们中的任何一人都可以随时在链上提交获胜状态以触发支付。然而，他们也可以决定继续玩第二局比赛，知道 Alice 已经赢得了第一局，而且可以在需要时随时在链上进行。换句话说，玩家们正在处理反事实状态。

在广义状态通道中，应用可以*反事实地安装*：如果所有参与者都表现良好，且争议从未发生过，那么应用合约就不需要实际创建，整个游戏都可以在链下解决。这也被称为合约的*反事实实例化*：一个可以部署但实际上未部署的合约。

任何玩家都可以在链上执行某个动作的事实足以促进良好的链下行为 —— 只要它与一组对恶意玩家施加惩罚的措施相辅相成，迫使对手浪费燃气上链。

总的来说，反事实广义状态通道提供了一个有趣的框架，可以最小化链上操作的数量，从而减少了每次在以太坊网络上执行操作时产生的延迟和燃气费用。作为额外的好处，它们还为参与者的行为提供了一层隐私保护：如果除了存款和支付之外没有进行任何链上交易，那么只有参与者知道通过状态通道交换了哪些消息。

### 通道网络

当涉及到在固定的小型参与者集合内解决支付或状态时，通道是有用的解决方案（通常是两个）。然而，当我们想要连接一个动态成员集合时，这个解决方案就显得不够了：对于我们想要与之进行交易的每个用户，我们都需要在链上打开一个新的通道。

要解决这个问题，有协议可以在两个对等方之间建立*虚拟通道*，利用通过多个中间人的通道路径。这有效地创建了一个由点对点连接构成的网络，只要两者之间存在有效路径，任何参与者都可以连接到另一个参与者，就像互联网本身一样。

### 注意

本节涵盖了目前正在进行大量研究和持续发展的主题。如果您考虑在状态通道网络上构建，请将其用作进行最新研究的起点。

网络中最简单的构建再次来自比特币，即 *多跳支付通道*。这种方法允许通过一个或多个中间人安全地路由支付。例如，Alice 可以将支付发送给一个中间人 Ingrid，与此同时她与 Ingrid 建立了一个支付通道，并让 Ingrid 转发支付给 Bob（假设 Ingrid 也与 Bob 有一个通道）。由于这些通道的建立方式^(15)，Ingrid 没有办法将这些资金据为己有。

这种类型的通道直接导致了一种简单而有效的网络布局，即 *枢纽与辐射式通道网络*，其中多个客户端连接到一个充当所有人的中间人的枢纽。通过与枢纽建立一个单一的通道，用户可以与网络中的任何其他人进行交易。另一方面，它的缺点是中心化，需要枢纽可用。

也有一些项目致力于更有趣的网络布局，比如灵感来自比特币闪电网络的 Raiden 网络^(16)。这些网络的最终目标是以一种无需信任的方式允许任何两个参与者建立一个共享的通道，通常称为 *虚拟通道* 或 *元通道*。这些通道不仅可以是支付通道，还可以是完整的广义状态通道，并且在每次交换中潜在地可以不需要中间人的积极参与。

## Sidechains

在它们最基本的版本中，*侧链* 是一个并行的以太坊网络，可能运行不同的共识算法，比如 *权威证明*，并通过 *桥接器* 连接到主网络。在较小的规模上工作使得侧链能够实现比主以太坊网络高得多的吞吐量。

### Note

尽管技术上来说，侧链可以使用工作证明，但这是极不安全的。请记住，工作证明依赖于攻击者无法产生比网络其余部分更多的计算能力。由于侧链往往与主网络相比较小，它们的难度也相对较低，这使得攻击者更容易对它们发动攻击。这就是为什么大多数侧链与一组封闭的矿工或验证者一起工作的原因。

### Proof of Authority

在权威证明，或简称 PoA 中，有一组预定义的节点充当添加到网络中的块的*验证者*。验证者是 PoA 中矿工的等价物，在其中它们添加新的块。每隔一定数量的秒数，这些验证者轮流提出一个新的块。这些块被广播给其他验证者，并且需要大多数验证者批准才能添加到区块链中。验证者的集合可以随时间变化，一些验证者被投票淘汰，新的验证者被允许加入集合。

区块是如何被广播、批准和达成共识的取决于所采用的具体*共识*算法。虽然有许多不同的共识算法，如 Clique，^(17) Aura，^(18) Raft，^(19) 或 Istanbul BFT，^(20) 但它们都分享了先前概述的相同基本方案。不同的算法可能提供不同的保护措施，防止恶意行为者或节点从网络中掉落，以及不同的性能。

侧链的另一个组成部分是与主网络的连接，通常称为*桥接*。桥接是用户在主链和侧链之间转移资产的机制。例如，一个简单的桥梁可以允许用户通过让用户将资金锁定在特定的主网合约中，将他们的资产从主网络转移到侧链。侧链验证者监视此合约，并在他们在主链上注册用户锁定资金时，在侧链中创建相应的资金。我们将在本章后期实施此机制。

#### 安全和信任

一个普通的 PoA 侧链的安全性完全取决于其验证者。如果他们中的大多数串通一气，他们可以有效地窃取锁定在侧链中的所有用户资金。因此，关键是验证者集合由多个不同方控制，并且不全由单一组织控制。用户只应该信任 PoA 网络，如果他或她信任大多数验证者节点。

为了遏制此类恶意行为，一些网络依赖于**股权证明**而不是权威证明。在这个方案中，验证节点需要存入（抵押）大量资金。如果证明他们恶意行为，那么他们的抵押将被削减作为惩罚 - 尽管如何执行这种惩罚是另一回事。

重要的是，验证者通过攻击网络可能获得的价值要少于他们因抵押而损失的价值，以保持激励的一致性。目前有不同的股权证明方法。然而，从用户的角度来看，体验与在权威证明网络中操作非常相似。

### 注意

鉴于恶意验证者可能从用户那里窃取资金，与主链相比，侧链的安全保证较差。这个事实使得侧链**不**被认为是在某些定义下的第二层解决方案。尽管如此，还有一些构建（如 Plasma，稍后我们将看到）允许用户通过调用主网络合约上的非法验证者行为来保护他们的资产。

#### 部署我们自己的链

为了说明 PoA 网络的工作原理，我们将使用 Geth 以太坊节点客户端手动设置一个。虽然 Geth 可以在工作量证明的主以太坊网络中运行，但也可以配置为在使用 Clique 共识算法的 PoA 网络中运行（例如 Rinkeby 测试网络），并充当验证者节点。

让我们首先设置三个矿工节点，它们都将在同一台计算机上运行。我们将首先为每个矿工创建新的账户。为方便起见，我们将为所有账户使用相同的密码，因此创建一个包含随机字符串用作密码的文件 password.txt。然后，为三个矿工中的每一个运行以下命令以创建地址，将 miner1 替换为 miner2 和 miner3。确保 password.txt 文件位于运行该命令的路径中。$ geth --datadir miner1 --password password.txt account new> 地址: {8305ccac...58269a7d}

你应该获得三个不同的地址，我们将其设置为此网络的验证者（请确保记下这些地址）。我们现在将为我们的网络创建一个*创世块*。创世块是网络的配置，将包括哪些是经授权的验证者集合、共识引擎、初始余额、区块燃气限制等信息。在 geth 中，这些信息被编译到一个 JSON 配置文件中，该文件用于引导每个节点。

Geth 包含一个名为 puppeth 的工具，它简化了这样一个文件的创建。只需在控制台中运行 puppeth，并回答提示的问题（见列表 8-18）。为你的网络命名，创建一个新的起源，使用 5 秒区块的 Clique 共识机制，并选择你的矿工作为“允许封存的账户”。你还应该选择第四个账户作为预先资助，或选择现有验证器之一来持有你的网络的初始 ETH。$ puppeth 请指定一个网络名称以管理（请勿使用空格、连字符或大写字母）> mysidechain 你想要做什么？（默认 = 统计） 1\. 显示网络统计信息 2\. 配置新的起源 3\. 跟踪新的远程服务器 4\. 部署网络组件> 2 你想要做什么？（默认 = 创建） 1\. 从头开始创建新的起源 2\. 导入已经存在的起源> 1 如果您想要明确指定您的链/网络 ID，请指定（默认 = 随机）> 1212 列表 8-18

Geth puppeth 配置向导的片段，用于设置带有 id 1212 的 PoA 网络。完成后，你应该有一个新的 mysidechain.json 起源文件

在启动我们的 Geth 节点之前，我们将设置一个 *bootnode*。bootnode 是网络中的一个节点，其唯一目的是帮助发现其他节点。我们将使用它来简化我们的矿工节点之间的通信。

要设置一个 bootnode，我们首先需要创建一个 boot key 并使用它来派生 bootnode 的 *enode 地址*（见列表 8-19）。enode 地址是去中心化网络中节点的唯一标识符，后跟节点可以找到的 IP 地址和端口。然后，我们将使用生成的 boot key 启动 bootnode，并让它侦听本地端口 30100。^(23)$ bootnode -genkey boot.key$ bootnode -nodekey boot.key -writeaddress> c190f2af...ee34b40a$ bootnode -nodekey boot.key -addr :30100 列表 8-19

生成一个 boot key 并运行一个 bootnode

### 注意

我们不需要使用创世配置文件来启动引导节点，因为引导节点不需要任何关于网络是否运行工作证明或授权，或者验证器是谁的信息。它只需要知道节点在哪里，以便与网络共享此信息。

现在我们已经运行了一个引导节点并有了创世配置文件，是时候真正启动网络了。在三个不同的终端中，启动三个不同的 Geth 验证器节点（见 8-20），配置为挖矿（即，封装）新块，并在本地通过 HTTP 公开 JSON-RPC API。geth \--datadir miner1 \--port 30201 \--rpc --rpcaddr localhost --rpcport 12001 \--rpcapi 'eth,personal' \--networkid 1212 \--gasprice 10000 \--unlock 8305ccac...58269a7d \--password password.txt \--mine \--bootnodes 'enode://c190f2af...ee34b40a@127.0.0.1:30100'8-20

使用之前生成的创世配置和引导节点 ID 启动 Geth 验证器节点。在不同的终端中运行此命令三次，每次一个验证器，更改解锁地址、数据目录、端口和 rpc 端口。

我们的网络现在应该在运行中，每 5 秒封装一个新块。查看三个验证器的日志，了解它们的进展情况。

现在我们可以启动一个新的客户端节点并连接到现有网络（见 8-21）。请记住，即使验证器的集合有限，网络仍然是公开的，任何节点都可以连接到它。我们可以使用它的控制台每 5 秒检查最新块号如何增加，运行 web3.eth.blockNumber。$ geth \--datadir node1 --port 30204 \--rpc --rpcaddr localhost --rpcport 12004 \--rpcapi 'eth,personal' \--networkid 1212 \--bootnodes 'enode://c190f2af...ee34b40a@127.0.0.1:30100' \console8-21

启动一个新节点加入网络，并启用控制台。请注意，我们没有以任何方式对这个新节点进行身份验证，因为网络是公开的，任何人都可以加入。

现在让我们将这个网络与现有的网络连接起来，比如 Rinkeby。

#### 建立桥梁

我们将建立一个简单的桥梁，完全依赖于验证人账户，使用在主网络和侧链上部署的合约，以及每个验证人运行的脚本。在这个模型中，用户进入侧链并稍后退出的步骤如下：

1.  1.

    用户将资金转移到主网上的桥合约。

1.  2.

    桥合约保留资金并发出事件。

1.  3.

    验证人注意到事件，并且每个验证人都调用侧链上的桥合约，请求解锁相同数量的资金。

1.  4.

    用户将资金存入侧链并在那里进行操作。

1.  5.

    当用户想要退出侧链时，通过将侧链资金转移到侧链桥合约并由验证人在主网桥合约上解锁它们，重复相同的流程。

我们将首先建立桥合约。这个合约将有两个主要职责：（1）接受和锁定用户资金，（2）在验证人的请求下解锁它们。请注意，我们将在两个链上部署合约的两个实例。一个链上的锁定功能将与另一个链上的解锁功能对应，反之亦然。

### 注意

在这个例子中，我们正在建立一个桥梁，它接受以太币，并在另一端发放侧链的本地货币。然而，我们也可以建立接受主链上某种 ERC20 代币甚至非同质化 ERC721 资产的桥梁。

首先，桥将需要知道验证者的地址（列表 8-22）。我们还将指定多少个验证者需要同意释放用户的资金。在我们的场景中有三个验证者，如果其中一个验证者退出，我们只需要两个验证者同意即可释放资金。pragma solidity ⁰.5.0;contract Bridge {  uint256 threshold;  mapping(address => bool) validators;  constructor(    uint256 _threshold,    address[] memory _validators  ) public payable {    threshold = _threshold;    for (uint256 i = 0; i < _validators.length; i++) {      validators[_validators[i]] = true;    }  }}Listing 8-22

桥合约的定义，初始化时包含验证者的地址。

请注意我们将构造函数设置为可支付。在侧链部署合约时，我们需要用主网络（在本例中为 Rinkeby）中允许用户转移的最大 ETH 金额来初始化该合约，这样合约就可以在验证者的提示下解锁这些资金。

我们现在将进入锁定函数（列表 8-23），这个函数相当简单。我们需要接受发送者的资金，允许他们指定桥的另一端的接收地址，并发出一个事件。我们将为每个锁定操作分配一个自增的 ID，以便验证者在另一端解锁时可以参考它。事件 Locked(uint256 id, uint256 amount, address recipient);uint256 lastId;function lock(address recipient) public payable {  require(msg.value > 0);  emit Locked(++lastId, msg.value, recipient);}Listing 8-23

桥合约的锁定函数

最后但并非最不重要的，我们将处理解锁功能（见 8-24）。这个函数将由桥的另一端的验证者调用。每个验证者都应该授权解锁与在另一端发生的锁定操作相对应的资金。请记住，由于桥的两端没有链上通信，因此验证者有责任将正确金额的资金解锁到用户请求的地址上。mapping(uint256 => Request) requests;struct Request {  uint256 amount;  address payable recipient;  bool paid;  uint256 approveCount;  mapping(address => bool) approvedBy;}event Unlocked(uint256 id, uint256 amount, address recipient);function unlock(  uint256 id, uint256 amount, address payable recipient) public {  Request storage request = requests[id];  require(validators[msg.sender]);  require(!request.approvedBy[msg.sender]);  require(request.recipient == address(0)    || request.recipient == recipient);  require(request.amount == 0 || request.amount == amount);  request.approveCount++;  request.approvedBy[msg.sender] = true;  request.recipient = recipient;  request.amount = amount;  if (request.approveCount >= threshold && !request.paid) {    request.paid = true;    recipient.transfer(amount);    emit Unlocked(id, amount, recipient);  }}列表 8-24

代币桥的解锁功能。当验证者第一次请求解锁时，我们将创建一个新的解锁请求，然后每次再次调用时记录一个批准。当达到所需数量的批准时，资金将被解锁。

### 注意

此实现允许恶意验证者阻止用户的资金解锁。验证者可以向桥接合约发送虚假的解锁请求，针对即将到来的请求 ID。这样，当诚实的验证者实际尝试满足解锁请求时，参数（如金额或收件人）将不匹配，操作将失败。我们将忽略此攻击，因为此桥的目的仅在于说明基本用法。尽管如此，这提醒我们，即使是最简单的实现也可能隐藏着安全问题，您应该始终使用经过审查和审计的合约。

现在我们可以在两个网络上部署此合约（见 8-25），使用我们之前定义的验证者集合，并选择解锁所需的两个批准阈值。在部署到侧链时，记得同时转移大量资金到合约中，以便在请求时进行解锁。const Web3 = require('web3');const Artifact = require('../artifacts/Bridge.json');const web3 = new Web3(PROVIDER_URL);const abi = Artifact.compilerOutput.abi;const data = Artifact.compilerOutput.evm.bytecode.object;const Bridge = new web3.eth.Contract(abi, null, { data });const bridge = await Bridge.deploy({  arguments: [THRESHOLD, VALIDATORS]}).send({  from: FROM, gas: 1e6, gasPrice: GAS_PRICE, value: VALUE});console.log("Bridge deployed at", bridge.options.address);8-25 号清单

桥接合约的部署脚本。使用不同的 PROVIDER_URL 两次运行此脚本：一个用于 Rinkeby 以太坊网络，另一个用于侧链。

最后，我们需要设置监视器脚本，每个验证器都会运行它们（见列表 8-26）。这些脚本将在一个网络中监视桥接合约以查找已锁定的事件，并在另一侧执行相应的解锁。const Web3 = require('web3');const Artifact = require('../artifacts/Bridge.json');const abi = Artifact.compilerOutput.abi;const remoteWeb3 = new Web3(REMOTE_PROVIDER_URL);const localWeb3 = new Web3(LOCAL_PROVIDER_URL);const remoteBridge = new remoteWeb3.eth.Contract(abi, REMOTE);const localBridge = new localWeb3.eth.Contract(abi, LOCAL);remoteBridge.events.Locked().on('data', function(e) {  const { id, amount, recipient } = e.returnValues;  localBridge.methods    .unlock(id, amount, recipient)    .send({ from: VALIDATOR, gas: 1e6, gasPrice: GAS_PRICE });});localBridge.events.Locked().on('data', function(e) {  const { id, amount, recipient } = e.returnValues;  remoteBridge.methods    .unlock(id, amount, recipient)    .send({ from: VALIDATOR, gas: 1e6, gasPrice: GAS_PRICE });});列表 8-26

每个验证器上运行的监视器脚本。请注意，我们创建了两个 web3 实例：一个连接到主网络，在那里我们监听桥接端的事件，另一个连接到本地网络，在那里我们执行解锁操作。然后我们反之亦然，允许资金从侧链返回到主网络。

现在我们可以在每个验证器节点上运行此脚本（或至少在其中两个上）。一旦它在运行，尝试在桥接的 Rinkeby 端调用锁定功能。几秒钟后，您应该可以在侧链中所选地址上使用您的资金。

在实际应用中，您需要决定要向用户公开多少这种复杂性。正如我们在第七章中所看到的，入职已经足够麻烦了，再添加另一个需要将资金从一网络发送到另一网络的步骤并不是一个好主意。

但是，实际上您可以利用特定于应用程序的侧链来改善入门体验。您可以直接为您的用户的初始账户在您的侧链上提供资金，或者构建一个病毒式的邀请方案，其中现有用户可以直接在更便宜、更快速的侧链上邀请新用户。然后，桥梁仅供希望从主网络转移价值或者到主网络转移价值的高级用户使用，但对于以太坊新手来说，应用程序简单流畅地运行而不知道其背后的原理。

一个很好的例子是在上一章中已经提到的**Burner Wallet**。[²⁴] 这个钱包在一个由四个不同团队充当验证者的权威证明侧链上运行，[²⁵] 用户通过接收一个在侧链上预先资助的账户链接很快就可以入门，并且由于低燃气成本和 5 秒区块，他们可以很容易地与他人进行交易。对于最高级的用户，还可以选择将资金转移到主以太坊网络，甚至从他们的主网账户向他们的临时钱包提供种子资金。

### 等离子链

[写作时的第 2 层解决方案的最新技术水平](https://zh.wikipedia.org/wiki/%E7%AC%AC%E4%BA%8C%E5%B1%82%E7%9A%84%E5%8A%A0%E5%AF%86%E7%94%B5%E5%AD%90%E5%AF%86%E7%A0%81)是由**维塔利克·布特林**和**约瑟夫·普恩**在 2017 年首次设计的等离子链。[²⁶]

等离子链不同于侧链，因为它们的安全性可以由主链（或等离子术语中的*父链*）强制执行，因此不完全依赖于侧链的共识机制。这意味着如果子链上的验证者集合（称为*等离子操作员*）行为不端，任何用户都可以构建一个加密证据并将其带到主链上的智能合约（称为*根合约*）。如果没有犯规行为，子链上的交易将以减少的燃气成本和延迟进行，这是侧链的典型特点。

然而，这种额外的安全性是有代价的。每当用户想要退出子链（即将其资产转移到主链时），他们必须经过*挑战期*，类似于我们在状态通道中看到的那种。如果一个恶意验证者创建了一个虚假的区块，在其中窃取了用户的资产，并使用它来控制主链中的这些资产，用户可以在这个挑战期间提交欺诈证据，并重新获得他们的资产。因此，退出等离子链并不是瞬间完成的，需要用户等待一段时间。[²⁷]

另外，由于智能合约需要能够处理子链上一组交易是否合法，因此子链上允许的操作不能过于复杂。特别是，在撰写本文时，没有一种等离子实现支持任意智能合约，并且只提供用户之间交换资产的手段。这个主题的研究是在*广义等离子*实现下进行的。

另一方面，等离子链设计为具有类似树状结构。等离子链的父链可以是*另一条*等离子链，通过简单地在其他链中组合等离子链，可以实现可伸缩性。这意味着，如果一个特定应用的等离子链变得过拥挤，它可以简单地产生新的子链并将用户群集移至其中。

值得一提的是，等离子本身不是一个规范，而是用于构建可伸缩的第二层基础设施的框架。这导致了许多不同团队开发了许多不同类型的等离子，例如最小可行等离子、等离子现金、等离子借记或等离子主链。[²⁸] 很可能在本书到达你手中的时候，这个领域会有新的重大发展。

## 摘要

像比特币或以太坊这样的公共区块链传统上为了去中心化和安全性而牺牲了性能。虽然有多个努力构建以太坊 2.0 的项目，其中包括分片机制以帮助网络扩展，但有趣的是看到许多解决可扩展性问题的解决方案在现有基础设施上不断涌现。

本章介绍的一些解决方案，如早期版本的 Plasma 或状态通道，已经准备就绪并且今天已经在生产中，帮助现实生活中的应用程序突破了以太坊主网络的限制。

这些解决方案不仅允许您的应用程序实现更高的交易吞吐量，而且还可以用于提供更好的整体用户体验。如果双方行为得当，通道为点对点交易提供即时的终局性，而不是等待十几个确认。而侧链可以提供可靠的区块时间，远低于主网络，并且具有相当低的 Gas 费用。

这些技术甚至可以结合使用：你可以在侧链中的各方之间建立状态通道，甚至可以在 Plasma 链中使用通道作为实际交易的资产。^(29) 这里的可能性是无限的。

你如何利用这些解决方案并向用户展示（或隐藏）它们将取决于你正在构建的内容。记住你的用户从你的应用程序中需要什么，并利用现有的构建模块为他们创造最佳的体验。

祝愉快编码！