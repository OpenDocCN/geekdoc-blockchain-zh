© 埃拉德·埃尔罗姆 2019 埃拉德·埃尔罗姆区块链开发者[`doi.org/10.1007/978-1-4842-4847-8_4`](https://doi.org/10.1007/978-1-4842-4847-8_4)

# 4. 比特币钱包和交易

埃拉德·埃尔罗姆^(1 )(1)纽约，纽约州，美国

在本章中，你将深入研究比特币的核心 RPC，并学习关于钱包和交易的知识。你将了解如何使用旧版和 SegWit 的比特币钱包。你将提取钱包的公钥和私钥。

本章的大部分内容将涉及交易，从利用比特币的测试区块链以简单的方式发送资金到更复杂的交易。此外，你还将学习如何通过比特币的核心钱包 GUI 发送硬币，以及如何在外部区块浏览器中查看交易并理解确认。你将研究原始交易，并学习如何创建具有一个输出的原始交易以及如何创建多个用户签名的事务。此外，你可以替换你的交易并设置锁定时间。你还将了解支付选项和费用之间的区别。

最后，我将介绍如何在原始交易中传递数据。在本章结束时，你将对交易、钱包、费用、支付选项和比特币的核心 RPC 有更深入的了解。

## 比特币核心 RPC 资源

你已经学会了如何利用比特币守护进程和比特币核心作为 HTTP JSON-RPC 服务器与比特币核心进行交互，并且你现在能够进行调用并接收 JSON 响应。在本节中，你将在此基础上了解钱包和交易。

第一步是初始化并运行比特币守护进程。> bitcoind –printtoconsole

在撰写本文档时，最新的 RPC 版本是比特币核心版本 v0.18.99.0-56376f336（发布版本）；随着比特币核心的新版本的发布，本章中的命令可能会发生变化，因此检查[`bitcoincore.org/en/doc/`](https://bitcoincore.org/en/doc/)上的最新 RPC 命令很有用。

请注意，v0.18 的文档在撰写本文档时尚未上线；v0.17 是最新文档([`bitcoincore.org/en/doc/0.17.0/`](https://bitcoincore.org/en/doc/0.17.0/)）。在右侧菜单中，选择 RAWTRANSACTIONS 和 WALLET 以获取与本章相关的 RPC 命令列表。

### 注意

除了比特币核心文档外，还有两个免费的网络资源可以帮助你更好地理解本章未涵盖的比特币 RPC 命令行。它们是[`github.com/ChristopherA/Learning-bitcoin-from-the-Command-Line`](https://github.com/ChristopherA/Learning-bitcoin-from-the-Command-Line)和[`learnmeabitcoin.com/guide/transactions`](http://learnmeabitcoin.com/guide/transactions)。

## 比特币钱包

在第二章中，你使用 getbalance 命令查询了钱包的可用资金，并使用 getnewaddress 命令创建了一个新的比特币钱包。

在第三章中，你为你自己的区块链创建了一个区块链钱包；你是通过创建一个钱包.js 文件并利用椭圆曲线加密 Node.js 库生成一个私钥-公钥组合，然后你通过命令行界面(CLI)暴露了这个组合。在本节中，我将在此基础上进一步探讨比特币的核心以及钱包和交易是如何生成的。

比特币允许用户发送和接收币。用户可以生成一个钱包，其中包含一个公钥，发送者会将币发送到接收者钱包的公钥地址。

发送币的过程遵循相同的步骤，但顺序相反。接收者向发送者提供一个钱包的公钥地址，他们在该地址期待收到付款，发送者将币发送到该公钥地址。钱包地址是公钥，由公钥/私钥散列算法生成。接收者可以在用户期待付款的任何时候生成一个新的公钥。不需要匿名性的用户可以对多个交易使用一个公钥；然而，比特币的原始愿景鼓励用户为每个交易提供一个不同的公钥，以及设置许多与许多公钥对应的私钥。私钥存储在钱包中，每个公钥代表一个钱包地址。

### 创建遗留钱包地址和检索私钥

最常见的比特币地址，也是你在第二章中生成的地址，称为支付到公钥哈希（P2PKH）地址。P2PKH 是公钥，公钥地址由算法进行哈希。

比特币还支持 P2SH-SEGWIT 协议，我将在本章后面讨论此协议。

### 注意

分隔见证（SegWit）是通过一次软分叉对比特币核心代码进行的扩展，它通过移除解锁交易的签名数据来增加比特币的区块大小限制。当解锁代码被移除时，额外空间可用于在链中包含更多交易。

要生成支持 P2SH-SEGWIT 和 P2PKH 的地址，只需运行以下命令：> bitcoin-cli getnewaddress2N96AMUEX4VMNTApPAbUaA6wzP4V9QrbveK 生成 P2PKH 地址时，你将使用传统标志。> bitcoin-cli getnewaddress "" legacy13oWKiVQ7C5Ewwjv6KRpP3Xm5YstzqFixT 正如你所见，这些命令返回了公钥。通过将密钥转存到一个文件中，或者像你之前所做的那样，直接使用 dumpprivkey 命令，都可以查看钱包的私钥。> bitcoin-cli dumpprivkey "13oWKiVQ7C5Ewwjv6KRpP3Xm5YstzqFixT"L5gDpFvfEkUSFeMSQb92kueD1BuX4JeZLAhQkXoEtjcZMog3uXB4

私钥不应该和任何人分享，因为它们可以解锁与公地址关联的资金。话虽如此，我在此处与你分享这个例子是为了教学目的。

### 注意

保护你的私钥。如果你的私钥丢失了，你将失去你的硬币/资金。

正如你所知，你可以将私钥转存到一个文本文件中。> bitcoin-cli dumpwallet ~/mywallet.txt{  "filename": "/Users/Eli/mywallet.txt"}然后，你可以获取钱包的位置，并查看你的密钥。> vim /Users/[location]/mywallet.txt

你保存的数据文件不仅包含公钥和私钥，还包含与你的钱包相关的交易。

你可能还记得，另一个有用的 RPC 特性是你可以查询比特币守护进程关于特定钱包的资金。> bitcoin-cli getbalance 1Mr2G632PfQuq4uJXRBNWLoRKH71Qwor51 要获取钱包中的可用资金，你只需运行 getbalance 命令，该命令返回 0 余额，因为你还没有存入任何资金。> bitcoin-cli getbalance0.00000000

### 支付给见证公钥哈希（P2WPKH）：SegWit 软分叉

比特币（BTC）和比特币现金（BCH）主要因为区块大小的问题而进行了硬分叉，也就是说每个区块可以包含的数据量。2017 年，比特币核心代码硬分叉成了比特币现金，并允许增加区块的大小限制。2019 年，比特币现金再次因为对每个分叉的新特性存在争议而分叉。

比特币的区块大小限制意味着交易有时必须等待被包含在一个区块中；然而，由于 1MB 的限制，它们可能不会被包含在下一个区块中，导致网络中交易过多时交易速度变慢，从而增加了矿工费用。为了解决这个问题，比特币开源开发者创建了一个软分叉，并包含了隔离见证（SegWit）。SegWit 通过移除解锁交易的签名数据来增加比特币的区块大小限制。当解锁代码被移除时，额外空间可以用来在链中包含更多交易。这种方法将区块大小增加到 4MB。

### 注意

SegWit 是一个过程，通过从比特币交易中移除签名数据来增加区块链的区块大小限制。这个过程释放了空间，允许您添加更多的交易。SegWit 使用在 BIP173 中定义的 Bech32 地址。它有 90 个字符，由人类可读部分、分隔符和数据组成。

解锁验证代码是*见证*数据。您可以说新代码“隔离了见证”。这个名字就是这么来的。

在我们使用的构建中，v17.0，钱包和交易有一个见证公钥哈希选项，以替换`scriptSig`参数并检查交易的有效性。旧的代码仍然有效，因为这是一个软分叉。

您在`getaddressinfo`命令中已经看到了这一点，该命令包含了支持旧地址的`scriptPubKey`以及`iswitness`。您可以运行`getaddressinfo`命令并查看这些参数。> bitcoin-cli getaddressinfo $address1

在`bitcoin core` v0.16 之前，您需要使用`addwitnessaddress`命令将旧地址转换为`P2WPKH`。自`bitcoin core` v0.16.0 以来，一个地址同时支持`P2SH`和`P2WPKH`。因此，钱包是`P2SH-P2WPKH`。如果您使用的是 v0.18，您可以看到`getaddressinfo`地址具有旧`scriptSig`参数和 SegWit 的参数。

### 椭圆曲线数字签名算法

`Bitcoin core`允许您利用椭圆曲线数字签名算法（ECDSA）创建签名。这可以通过使用`signmessage`命令来实现。添加签名允许您证明拥有钱包的私钥，从而为发送方增加了一个安全层，以确保他们正在将资金发送到正确的地址。> bitcoin-cli signmessage "13oWKiVQ7C5Ewwjv6KRpP3Xm5YstzqFixT" "John Doe"此命令输出一个哈希:HzicuTXMl1COVh7Xw9ky9A/cl7ZjMSWNH10Y/invAgHWa74gS8EOvio3FJkofpH0nunIA7pJoGwWLRa0UdD7dc8=发送方可以在发送资金前验证钱包。> bitcoin-cli verifymessage "13oWKiVQ7C5Ewwjv6KRpP3Xm5YstzqFixT" "HzicuTXMl1COVh7Xw9ky9A/cl7ZjMSWNH10Y/invAgHWa74gS8EOvio3FJkofpH0nunIA7pJoGwWLRa0UdD7dc8=" "John Doe"验证命令将输出一个真或假响应。在这种情况下，它会回应如下：true

这允许用户确认他们实际上拥有一个钱包。这在代码层面上很有用，因为`P2PKH`地址将利用私钥生成签名。`P2PKH`地址是对应于生成签名的私钥的公钥的哈希。

### 注意

ECDSA 是比特币用来确保资金所有权的加密算法。它用于生成公/私钥，也可以将签名包含在算法中。

ECDSA 签名可以与多达四个可能的 ECDSA 公钥进行核对。这些公钥将从签名哈希中重建；每个密钥进行哈希并与提供的 P2PKH 钱包地址进行比较以匹配。结果要么是真，要么是假。正如您之前看到的，示例在运行 verifymessage 命令后获得了真。

### 注意

二维码是字符串的图像表示。二维码阅读器用于读取 URL 或编码钱包的公钥地址等事物。

您可以使用 Chart Google API 生成二维码： [`chart.googleapis.com`](https://chart.googleapis.com) 。例如，要为地址：13oWKiVQ7C5Ewwjv6KRpP3Xm5YstzqFixT 生成 0.00016 BTC 的二维码，您将生成以下 URL：

[通过 Chart Google API 生成二维码](https://chart.googleapis.com/chart%253Fchs%253D250x250%2526cht%253Dqr%2526chl%253Dbitcoin:13oWKiVQ7C5Ewwjv6KRpP3Xm5YstzqFixT%253F%2526amount%253D0.00016) 。见图 4-1 ！../images/475651_1_En_4_Chapter/475651_1_En_4_Fig1_HTML.jpg

图 4-1

通过 Chart.googleapi.com 的比特币二维码

## 交易

在本节中，我将介绍交易。您将学习如何使用比特币守护进程在测试网上发送硬币，同时使用命令行和比特币核心钱包 GUI。您将学习如何使用比特币浏览器查看您的交易。然后，我将通过展示如何创建一个带有单个输出的原始交易以及利用多重签名（multisig）创建更复杂交易的方法来介绍更高级的交易创建，这需要超过一个单一密钥来授权交易。此外，我还将介绍如何更改其他选项，例如为更改费用替换交易以及设置锁时间。您将了解 P2PKH 和 P2SH-SEGWIT 之间的区别。最后，您将学习如何使用 OP_RETURN 参数附加非硬币数据。让我们开始吧。

### 简单命令

一个区块中的第一个交易被称为 *coinbase* 交易；这个交易由包含在区块中的交易的交易费用组成。要发送交易，您需要向矿工支付交易费用。如果费用过低或没有支付费用，交易可能会在 P2P 网络中长时间或永久地卡住，直到费用被更改。

为了设置交易费用，你可以在比特币.conf 文件中添加一个参数并设定默认费用。首先，你需要找到文件的位置。为此，在运行守护进程之后，你可以追踪到文件的所在位置。> `bitcoind –printtoconsole`几秒钟后，通过按 Ctrl+C 停止此服务。该命令显示了比特币.conf 文件的位置。它返回了配置文件的位置。然后你可以打开文件并添加默认费用进行修改。在这个例子中，它在应用程序支持文件夹内嵌套./Users/[我的用户]/Library/Application Support/Bitcoin/bitcoin.conf

当你打开文件时，你可以看到默认交易费用被设定为 0.00000020（`mintxfee=0.00000020`）。

### 注意

比特币中还有其他费用和设置。你可以修改你发送的交易（`paytxfee`）、最大总费用（`maxtxfee`）、回退费用等等。访问这个比特币页面查看所有可用的选项：[运行比特币](https://en.bitcoin.it/wiki/Running_Bitcoin)。

监控和更新比特币交易费用可以确保发送的资金受到市场力量的改变。有一些网站、应用程序和表格试图预测需要支付的费用。有许多网站帮助计算交易费用预测，比如这个 API，你可以在你的代码中调用它：

[`bitcoinfees.earn.com/api/v1/fees/recommended`](https://bitcoinfees.earn.com/api/v1/fees/recommended)

在撰写时，API 返回了 20 Satoshis 的费用。{"fastestFee":20,"halfHourFee":20,"hourFee":18}

另一个例子是 [`bitcoinfees.net/`](https://bitcoinfees.net/)。这个网站显示，大多数交易在不到六小时内为五个到六个 Satoshis，或者在撰写时不到 20 分钟为 49 到 50 Satoshis。

### 注意

Satoshi 是一个比特币的一百万分之一，以 Satoshi Nakamoto 命名。这是可以发送的最小比特币份额：0.00000001 比特币。撰写时，更快的费用是 20 Satoshi。

现在你知道了费用，你可以将配置文件中的最小费用修改为更高的费用，比如 50 Satoshis。> 使用 `vim` 修改 '/[位置]/bitcoin/bitcoin.conf' 文件 mintxfee=0.00000050txconfirmtarget=3

参数`mintxfee`设定了 50 个 Satoshis 的最小交易费用，即 0.00000050 比特币。这将设定你的交易中每字节数据为 20 Satoshis。这意味着浮动费用需要确定一个合适的金额，以便将交易纳入下一个三个区块中。正如你所回忆的，每个区块需要大约 10 分钟来计算，所以它将目标定为 30 分钟以包含你的交易。

一旦你修改了配置文件，记得重新启动 bitcoind。> `bitcoind –printtoconsole`

### 测试网络

在本节中，你将了解更多关于交易的信息，为了更好地理解交易，你需要发送和接收比特币。要在主网络（实际的生成链）上获取比特币，你需要挖掘硬币或交易它们。然而，在学习过程中你不想处理实际的硬币，因为你需要支付费用，如果你犯错误还可能丢失硬币。此外，比特币的价格可能下跌。

幸运的是，比特币提供了用于测试的替代区块链，它被称为 *测试网络* 。这个替代的区块链让你可以在不使用真实比特币或滥用比特币链的情况下进行实验。你可以用 -testnet 标志启动比特币核心实例。在测试网络上，这是通过 *水龙头* 完成的，假装的硬币。通过停止比特币核心守护进程并带有 testnet 标志重新启动它，你连接到测试网络区块链而不是主区块链。`bitcoind –testnet`

请记住，与比特币主网络链一样，同步和索引部分可能需要数小时，这取决于你的互联网连接速度。如果你想要开始处理区块，运行该命令并喝杯长咖啡。

测试网络比特币水龙头为你提供用于测试的自由硬币。测试网络请求你在完成测试后将这些硬币归还，因为这项服务是免费的，归还这些硬币将有助于需要它们的下一个开发者。

你可以在以下链接中了解更多关于测试网络的信息：[测试网络](https://en.bitcoin.it/wiki/Testnet)。在撰写本文时，testnet3 是用于测试的最新区块链。

你将使用 coinfaucet.eu，该网站可在此处找到：[`coinfaucet.eu/en/btc-testnet/`](https://coinfaucet.eu/en/btc-testnet/)。然而，还有其他水龙头以防这个网站不再存在。第一步是将硬币发送到你的钱包。首先，使用以下命令生成一个新的 P2PKH 钱包地址：`bitcoin-cli getnewaddress "" legacymnMs77edsGV8VKwtB3d7fsnvrNuZ8ECKfh`。正如你所见，你收到的输出是你可以用来接收资金的公钥。接下来，将该地址粘贴到 [`coinfaucet.eu`](https://coinfaucet.eu) 上，选择“比特币测试网络”，验证你不是机器人，然后点击“获取比特币！”按钮，如图 4-2 所示。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig2_HTML.jpg](img/475651_1_En_4_Fig2_HTML.jpg)

图 4-2

测试网络硬币水龙头，请求用于测试的资金

一旦硬币被发送到你的钱包，你就会收到带有交易编号的确认信息，如图 4-3 所示。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig3_HTML.jpg](img/475651_1_En_4_Fig3_HTML.jpg)

图 4-3

测试网络硬币水龙头，比特币已发送

### 注意

请注意，这些水龙头测试网站点经常会下线，你可能需要找到一个新的水龙头测试网站点。为了方便起见，这里有一个在撰写本文时仍在工作的站点：[`testnet-faucet.mempool.co/`](https://testnet-faucet.mempool.co/) 。

### 在区块浏览器上查看交易

在测试网水龙头上，你可以像在主测试生产比特币的区块链上一样监控已发送的比特币。这是在测试网区块链浏览器中完成的；请查看“tx”链接，如图 4-3 所示。正如你所回忆的，“tx ID”代表交易 ID。或者，你可以直接将该交易 ID 粘贴到 [`live.blockcypher.com/btc-testnet/`](https://live.blockcypher.com/btc-testnet/) 的区块浏览器中。见图 4-4 ！../images/475651_1_En_4_Chapter/475651_1_En_4_Fig4_HTML.jpg

图 4-4

在 live.blockcypher.com 上查看交易信息

实际上，区块链上发生的每一笔交易都可以公开地供任何人查看，包括所有交易数据，除了用户的私钥。尽管交易数据是公开的，但关于所有者的识别信息不是公开信息，也不需要进行交易。连接用户与您发送的硬币的是与公钥关联的私钥。

同样，你也可以通过 RPC 命令行进行同样的信息检查。你已经知道如何检查你的钱包余额，如图所示：> bitcoin-cli getbalance0.0000000

当收到硬币时，它们将在交易被挖出的块的确认后才能用于支出。这就是为什么如果您立即检查您的余额，它仍然会显示 0 的原因。

你将能够通过运行 getunconfirmedbalance 命令看到你的交易在下一次区块中被包含后的下一个区块中作为未确认的硬币。进行检查，运行 getunconfirmedbalance 命令。> bitcoin-cli getunconfirmedbalance0.10413028

一旦您有足够的确认，getbalance 命令将显示您的新余额，而 getunconfirmedbalance 将显示 0。

同样，你可以更具体地请求最小确认数为 2。> bitcoin-cli getbalance "*" 2

### 注意

交易保持“未确认”状态，直到创建下一个新块。一旦创建了新块，新交易将被验证并包含在该块中。现在，该交易将有一个确认。大约十分钟后，创建了一个新块，交易得到了确认。每次确认都会增加交易的安全性，交易被撤销的可能性也会降低。交易所的常规做法是，需要四到六个确认才能让您使用硬币；对于大量硬币，等待六十个确认可能是明智的，这需要大约十个小时。

另一个有用的命令是列表交易命令；它提供了与你的钱包相关的所有交易数据的完整列表。`bitcoin-cli listtransactions`[    {        "address": "mnMs77edsGV8VKwtB3d7fsnvrNuZ8ECKfh",        "category": "receive",        "amount": 0.10413028,        "label": "",        "vout": 0,        "confirmations": 420,        "blockhash": "0000000000125d2714882704562c8442a6700c58a41cad0b4108305474be3bb1",        "blockindex": 4,        "blocktime": 1541783585,        "txid": "645a34a5cbdd66b126e6f81560dc79957c6e1a175a68f8ad23ca7fd38046df85",        "walletconflicts": [        ],        "time": 1541783585,        "timereceived": 1541890511,        "bip125-replaceable": "no"    }]

### 通过比特币核心钱包 GUI 发送测试网络货币

你初始化了一个带有测试网络标志的比特币核心实例；然而，发送和接收硬币还有另一种更简单的方法。比特币核心包含一个图形用户界面（GUI）钱包，你可以使用它。你将使用随比特币核心提供的 GUI 软件。要开始，请在终端中终止 bitcoind 守护进程，通过按下控制+C，然后运行带有测试网络标志的命令行终端中的 bitcoin-qt，这样你就可以连接到测试网络，而不是主网络。`bitcoin-qt –testnet`这个命令会打开一个新窗口，然后与测试网络区块链同步。就像之前一样，如果你没有完成测试网络同步，它可能需要数小时，这取决于你的互联网连接，如图 4-5 所示。然而，在钱包 GUI 中，你会看到同步所需时间的估计值。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig5_HTML.jpg](img/475651_1_En_4_Fig5_HTML.jpg)

图 4-5

比特币钱包测试网络 GUI 与测试网络同步

像以前一样，你需要等待同步完成；只有这样你才能提取你的钱包的公钥地址并花费你的货币。在概览菜单中，你会看到余额，包括已确认（可用）资金和未确认（挂起）资金。你还可以通过点击顶部的交易按钮来获取交易列表。见图 4-6。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig6_HTML.jpg](img/475651_1_En_4_Fig6_HTML.jpg)

图 4-6

比特币核心钱包概览屏幕

要创建一个新的钱包公钥地址，点击顶部的人民币，然后点击请求付款按钮。这将为您生成一个钱包地址，如图 4-7 所示。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig7_HTML.jpg](img/475651_1_En_4_Fig7_HTML.jpg)

图 4-7

比特币核心钱包，接收货币屏幕

正如你所看到的，GUI 创建了一个二维码以便你的方便。当你发送货币时，你可以扫描它，只要有这个功能的支持。现在，让我们通过在[`live.blockcypher.com/btc-testnet/`](https://live.blockcypher.com/btc-testnet/)的测试网络水龙头上发送更多货币到你的钱包。*.*

正如你所看到的，你随后也可以像通过命令行一样收到硬币。接下来，你会发送一些硬币。

你将向测试网络水龙头发送 0.01 BTC，供其他开发者使用。为此，点击 GUI 顶部的发送按钮，并粘贴在向你的钱包发送硬币时提供给你的测试网络水龙头钱包地址。

请注意，在比特币核心钱包 GUI 中，Transaction Fee 旁边有一个选择按钮。这让你可以选择费用以及确认次数。它还包括启用“替换 by”费用的方法。这个功能让你在费用太低且交易不包括在区块中时改变费用。见图 4-8。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig8_HTML.jpg](img/475651_1_En_4_Fig8_HTML.jpg)

图 4-8

比特币核心钱包发送屏幕

测试网络水龙头将硬币发送到您提供的钱包地址。当你发送和接收硬币时，GUI 会弹出一个通知窗口，并在概览屏幕上更新余额。点击交易按钮查看交易信息。您还可以点击每个交易以查看实际交易数据。这与您看到的 listtransactions 命令类似。见图 4-9。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig9_HTML.jpg](img/475651_1_En_4_Fig9_HTML.jpg)

图 4-9

比特币核心钱包交易

#### 原始交易

到目前为止，你通过命令行收到了一个交易，以及使用比特币核心 GUI 得到的硬币。你还能够查看确认、费用余额和交易。如果你向测试网络水龙头发送资金并收到硬币，事情就很简单。这称为单输入单输出交易，因为你有一个发送者和一个接收者，你花费的金额与你收到的金额相同（减去费用）。在现实生活中，随着交易变得更加复杂，存在许多用例，在这些用例中，有一个输入和多个输出或多个输入和多个输出。比特币核心提供了几组命令来访问原始交易（RawTransaction），以便你可以对自己的交易有更细粒度的控制。

你将从通过 RPC 命令行进行简单的单输入单输出交易开始。

### 注意

创建和使用 RawTransaction 对于构建软件是有用的，因为你对自己的交易有完全细粒度的控制。然而，犯错误可能会导致灾难性的后果和硬币的丢失，所以在发送任何资金之前要小心并仔细检查一切。

当你收到一个交易时，这笔交易会存在于你的钱包中的一个称为*未花费交易输出*（UTXO）的状态。要发送一个单输入单输出的交易，你需要你的金额等于你想要发送的基金。然后，你可以为接收你硬币的人生成一个新的 UTXO。接收者可以使用这些 UTXOs 向新的接收者发送交易，这个过程可以无限继续。

### 注意

一个 UTXO 是你钱包中的一个单独的 incoming coin transaction。当你向一个或多个钱包地址接收多个交易时，每个都会作为一个 UTXO 存在，所以你将会有多个 UTXO。要创建一个新的传出交易，你需要根据你试图发送的金额收集一个或多个 UTXO。

那么，如果你的 UTXO 包含比你想要花费的金额更大的金额怎么办？那么你需要将剩余的硬币发送回你的钱包。为了获取未花费硬币的列表，你可以使用 listunspent 命令。

通过 Ctrl+C 关闭比特币核心 GUI 钱包，并用 testnet 标志重新启动守护进程。> bitcoind -testnet 当你运行 getbalance 命令时，你会得到你的钱包余额，这包括从[`live.blockcypher.com/btc-testnet/`](https://live.blockcypher.com/btc-testnet/)接收到的两个交易，减去你发送回测试网络水龙头的那笔交易。> bitcoin-cli getbalance0.18505841 我想指出的是，任何时候你都可以使用-named 标志而不是使用顺序参数。命名参数有助于确保你在使用主网络时不会犯错误。例如，带有命名参数的 getbalance 命令如下所示：> bitcoin-cli -named getbalance minconf=20.18505841

接下来，我们来看看 listunspent 命令。正如其名所示，它返回一个包含你未花费的硬币的交易信息的 JSON，换言之，即你的未花费交易输出（UTXO）。listunspent 命令还返回一个名为 vout 的变量的 JSON，代表交易中的输出索引号。

### 注意

vout 值代表交易的输出索引号。你将使用 txid 和 vout 来选择现有输出作为新交易的输入。

> bitcoin-cli listunspent

这些未使用的交易输出（UTXO）显示了一个名为 txid 的属性，该属性包含在比特币块中。txid 属性允许你跟踪交易，正如你通过区块链浏览器所看到的那样。

注意，索引从 0 开始，因为你有两个交易，现在是 0 然后是 1。如果你有更多的交易，这个索引会继续增加。图 [4-10 说明了当你有两个 UTXO 时 listunspent 的结果。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig10_HTML.jpg](img/475651_1_En_4_Fig10_HTML.jpg)

图 4-10

vout index illustration

您可以通过`getrawtransaction`命令获取有关交易的的所有数据。在这里，我从您收到的 UTXO 中选择了第一个`tx`属性，然后我添加了`1`标志以解码十六进制编码的交易数据；看看命令和整个输出，如下所示：`bitcoin-cli getrawtransaction 50e91c9b73a90bd883f4a9a8a51be729770df20fae0445a9090b80a8621f4538 1`{  "txid": "50e91c9b73a90bd883f4a9a8a51be729770df20fae0445a9090b80a8621f4538",  "hash": "e420b350f5b95e29f51b722a5bd44ea2e9d27a7239d2e17da02f28e04c757b14",  "version": 2,  "size": 248,  "vsize": 166,  "weight": 662,  "locktime": 1443113,  "vin": [    {     "txid": "2645c128d68194640a7207eeae6ea42e8e528bcba2369eec0ba572566228b507",     "vout": 0,     "scriptSig": {         "asm": "00143bfa0326c076fa6cab0d23aea170bac38ac9a164",         "hex": "1600143bfa0326c076fa6cab0d23aea170bac38ac9a164"     },     "txinwitness": [         "3045022100fb7f0fc2cf99c8174eb3d14169e1c206157d434d8290b2efbefa5a37d0773923022065f0b671c0596816c062b9bdc7b30931edfd99a846a0f1633d301bfb7c03db3c01",         "02d208ff6da0583b99392d30e33c5a12da61b9d9de4c35bb0d20c33ba3bfc49302"    ],     "sequence": 4294967294    }  ],  "vout": [    {     "value": 0.09092813,     "n": 0,     "scriptPubKey": {         "asm": "OP_HASH160 8d1c6e108c60cfdfa61565ac328be6624591404b OP_EQUAL",         "hex": "a9148d1c6e108c60cfdfa61565ac328be6624591404b87",         "reqSigs": 1,         "type": "scripthash",         "addresses": [            "2N67MKgL5rYcbuySDFUdypU5DvKjmwZoYEb"            ]     }    },    {     "value": 1453.63689543,     "n": 1,     "scriptPubKey": {         "asm": "OP_HASH160 f4eb3fe1578076853a77

请注意，您有关区块、确认、输入、输出等方面的信息。

### 生成具有一个输出的原始交易。

交易很容易变得复杂，因为通常需要不止一个输入或输出。例如，如果你想将未使用的币发送回你的钱包，同时发送币到多个地址，这就开始变得复杂了。使用原始交易，你可以完全控制币的流向并实现复杂的交易。

你将开始通过将一个未使用的交易输出（UTXO）从一个钱包发送到另一个钱包来创建一个简单的原始交易。在此之前，你是通过比特币核心钱包图形用户界面（GUI）将币发送回测试网络水龙头。我们现在用原始交易命令来做同样的事情。

为了开始，让我们先确认你在发送币之前钱包的余额。`bitcoin-cli getbalance`0.18505841 接下来，让我们选择你将用来资助交易的 UTXO。正如你回忆的那样，你可以通过`listunspent`命令获取 UTXO 列表，然后查看 JSON 响应并选择交易 ID。选择一个有足够资金来资助你新交易的交易，并且这个交易已经被确认了。`utxo_txid="50e91c9b73a90bd883f4a9a8a51be729770df20fae0445a9090b80a8621f4538"`正如你可能还记得的，`vout`是交易中一个输出的索引号。在这个例子中，我将指向一个`vout`并生成一个新的交易。新的交易可以包括多个其他的`vout`，如图 4-11 所示。![新的交易输出](img/475651_1_En_4_Fig11_HTML.jpg)

图 4-11

新的交易输出示例

在这个例子中，你将为 vout 设置第一个索引。> utxo_vout="0"你需要的最后一个变量是接收者地址。在这里，你将使用与之前发送你的硬币相同的钱包地址。> recipient="mv4rnyY3Su5gjcDNzbMLKBQkBicCtHUtFB"最后，你可以使用 echo 命令来验证和核对你是否正确设置了你的变量。> echo $utxo_txid> echo $utxo_vout> echo $recipient 现在你已经设置了你的变量，你可以通过 createrawtransaction 命令生成一个 RawTransaction 对象。你通过包括所有你设置的变量和声明你想要花费的金额来实现。你使用 0.xxx，但你需要使用 UTXO 减去你想支付的费用以发送 UTXO 中的全部硬币。> rawtxhex=$(bitcoin-cli createrawtransaction "'[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]"' "'{ "'$recipient'": 0.xxx }"')接下来，你可以提取 rawtxhex 值。> echo $rawtxhex020000000138451f62a8800b09a94504ae0ff20d7729e71ba5a8a9f483d80ba9739b1ce9500000000000ffffffff0140420f00000000001976a9149f9a7abd600c0caa03983a77c8c3df8e062cb2fa88ac00000000rawtxhex 值包括你的新交易信息作为十六进制编码的数据。以下解码交易命令将返回一些带有交易解码数据的 JSON 输出：> bitcoin-cli decoderawtransaction $rawtxhex{  "txid": "91d4e108f8957251d2997e1f8dcdd0eec97192e8accf85a9e81f772f586118af",  "hash": "91d4e108f8957251d2997e1f8dcdd0eec97192e8accf85a9e81f772f586118af",  "version": 2,  "size": 85,  "vsize": 85,  "weight": 340,  "locktime": 0,  "vin": [    {

正如你所看到的，要创建交易，你需要从钱包的公钥散列和私钥散列生成签名。交易输出脚本取公钥和签名，并检查你是否与公钥散列匹配。如果结果为真，你就可以花费硬币；否则，你不能。

### 注意

交易中可见的公钥是一种称为 Pay to Pubkey (P2PK)的交易类型。你一直在使用的隐藏公钥是一种称为 Pay to PubKey Hash (P2PKH)的交易类型。

你将通过 P2PKH 签署你的交易，以匹配你的钱包类型。签署交易有两种方法；你可以使用 signrawtransactionwithkey 或 signrawtransactionwithwallet。

这两个签名方法在 0.18.0 RPC 版本中可用，包括以序列化的十六进制编码格式提供的原始交易的输入。

`signrawtransactionwithwallet`命令格式如下：`signrawtransactionwithwallet "十六进制字符串"` ( [{"txid":"交易 ID","vout":n,"scriptPubKey":"公钥脚本","redeemScript":"赎回脚本"},...] `sighashtype` )

请注意，`signrawtransactionwithwallet`命令允许你包含一个名为“prevtxs”的第二个参数。“prevtxs”格式为一个数组，包括之前的交易输出。如果你决定使用并插入“prevtxs”的值，该交易将依赖于之前的交易，而之前的交易可能甚至不在区块链中。如果你不需要这个功能，只需将“prevtxs”设置为 null。

`signrawtransactionwithkey`命令格式如下：`signrawtransactionwithkey "十六进制字符串"` ["私钥 1",...]

请注意，第二个参数是一个 base58 编码的私钥数组，它将是签署交易的唯一把钥匙。第三个可选参数是一个之前交易输出的数组，该交易依赖于这些输出，但可能尚未进入区块链。

在我们的案例中，你不会包含第二个参数，因为你的交易不需要依赖其他条件。> bitcoin-cli signrawtransactionwithwallet $rawtxhex{  "hex": "0200000000010138451f62a8800b09a94504ae0ff20d7729e71ba5a8a9f483d80ba9739b1ce9500000000017160014c27b4e6bd8eb821ee80a239e0edd59070f57233dffffffff0140420f00000000001976a9149f9a7abd600c0caa03983a77c8c3df8e062cb2fa88ac0247304402205cc4b04859e34aa6b1e924745f33a7643fbe45fcd6e900fdaa29281feae3f8f6022059d4083a3cf81c3bb82267931660afb8ffc4bae87ede8dfa11efcb6af6a14ac90121028926735fcd5bf6580e6f669c240da8975dddf23a6d4015e4e0bc1ca3f1d2b7f100000000",  "complete": true}The previous command returned signed, hex-encoded data in the JSON response. Use that data to set the hex for the signedtx variable.> signedtx="0200000000010138451f62a8800b09a94504ae0ff20d7729e71ba5a8a9f483d80ba9739b1ce9500000000017160014c27b4e6bd8eb821ee80a239e0edd59070f57233dffffffff0140420f00000000001976a9149f9a7abd600c0caa03983a77c8c3df8e062cb2fa88ac0247304402205cc4b04859e34aa6b1e924745f33a7643fbe45fcd6e900fdaa29281feae3f8f6022059d4083a3cf81c3bb82267931660afb8ffc4bae87ede8dfa11efcb6af6a14ac90121028926735fcd5bf6580e6f669c240da8975dddf23a6d4015e4e0bc1ca3f1d2b7f100000000"That’s it; you can now send your transaction via the sendrawtransaction command.> bitcoin-cli sendrawtransaction $signedtxff75dbb08da6f4dc6463dd32d8f9b1a4781e1eeee338e93e82820d0fdfbd43ffThe output gets you a txid response that you can check in the Blockchain Explorer as you did before. You can also verify that the funds were removed from your account via the getbalance command.> bitcoin-cli getbalance0.09413028As well as listunspent command.> bitcoin-cli listunspent

### 需要多签的交易

迄今为止，您一直在进行标准的“单签名交易”，因为您只需要一个签署人及其一个签名来签署交易并执行转账。但是，比特币网络支持更复杂的交易。这些交易可以设置为需要多个签署人的签名。例如，机构，合作伙伴，配偶或编程脚本可能希望所有各方签字，而不仅仅是其中一个。这些情况需要所有用户的所有私钥才能发送资金。

要进行多重签署人交易，您将创建两个用于测试的分开的钱包。您可以在两个不同的机器上运行 bitcoin core 并使用 RPC 调用为每个钱包生成一个新的公共地址，或者您可以下载 Electrum 钱包[`electrum.org/#download`](https://electrum.org/%2523download)并在测试网络模式下运行以生成您的第二个钱包。

作为一个第一个例子，您将运行 Electrum，因为您可以使用其内置的多重签名钱包来理解此过程。一旦您完成下载 Electrum，请通过命令行以测试网络方式运行 Electrum。> open -n /Applications/Electrum.app --args –testnet

### 设置具有多重签名钱包的 Electrum

启动 Electrum 后，在创建钱包选项中选择“多重签名钱包”然后点击下一步。请参见图 4-12。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig12_HTML.jpg](img/475651_1_En_4_Fig12_HTML.jpg)

图 4-12

Electrum 多重签名钱包

在下一个屏幕上，您可以选择需要多少共同签署人以及需要多少签名。这些交易通常被称为*M-of-N 交易*，例如，2-of-3 场景。2-of-3 意味着您需要至少两个私钥（签名）来自三个共同签署人来授权交易。您可以移动滑块更好地理解这个功能，如图 4-13 所示。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig13_HTML.jpg](img/475651_1_En_4_Fig13_HTML.jpg)

图 4-13

Electrum 多重签名钱包共同签署人和签名

这里，选择一个 2-of-2 多重签名钱包，这意味着两个共同签署人和两个签名。然后点击下一步按钮。在接下来的屏幕上，点击“创建一个新的种子”并点击下一步按钮。

在接下来的屏幕上，您可以选择种子类型。标准意味着 P2PKH 或 SegWit，这意味着一个 P2SH-SEGWIT，因此选择标准并点击下一步。

对于下一步，您得到了一个代表您私钥的种子。存储您的种子，并小心不要与任何人分享。然后提供了 Electrum 所说的您的*主*公钥，并要求您与您的共同签署人分享，如图 4-14 所示。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig14_HTML.jpg](img/475651_1_En_4_Fig14_HTML.jpg)

图 4-14

Electrum 安装向导主公钥

### 注意

Electrum 公共主密钥是 Electrum 分层确定性（HD）钱包的一部分，该钱包基于主种子生成一个地址，该种子可以用来备份你所有的资金。种子由单词组成，用于获取你的钱包私钥；丢失你的种子就意味着丢失你的私钥。

点击下一步，你可以输入一个联签名人的公钥或私钥。见图 4-15。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig15_HTML.jpg](img/475651_1_En_4_Fig15_HTML.jpg)

图 4-15

Electrum 安装向导联签名人密钥

在向导的下一页，你将使用比特币核心钱包的 主私钥来允许 Electrum 代表你签署第二个钱包。你可以从私钥备份文件内部获取私钥。它显示在扩展的私钥主密钥下。> vim /Users/[位置]/mywallet.txt# 扩展的私钥主密钥: [密钥]

Electrum 向导为您设置联签名人，安装向导的下一步询问您是否设置密码，如果需要，可以增加额外的安全性。

就这样。现在向导已经完成了你的账户设置，你可以向你的联签名人钱包发送和接收资金。点击顶部接收以获取你的钱包地址，如图 4-16 所示。![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig16_HTML.jpg](img/475651_1_En_4_Fig16_HTML.jpg)

图 4-16

Electrum 钱包接收地址和二维码

你将再次使用 Coinfaucet.eu 来资助你的新钱包：[`coinfaucet.eu/en/btc-testnet/`](https://coinfaucet.eu/en/btc-testnet/)。

然后你可以将这些硬币确认后发送回 Coinfaucet.eu 钱包的地址；这是 Coinfaucet.eu 钱包的地址：2N7RzS3j2eKHVj1E5yV7iGuwfgUtobrCnrc。

由于你已经提供了两位联签名人的私钥，这笔交易将使用发送命令进行。然而，如果你设置了两个账户并提供了一个公钥，第二个联签名人需要在他的账户上批准这笔交易，发送命令才会实际发送硬币。

同样，你可以通过 RPC 命令行进行这笔交易。

要开始，点击文件➤删除顶部的 Electrum 以创建标准钱包而不是联签名人钱包。

一旦这个钱包被删除，你可以重新开始并创建一个新的标准（P2PKH）钱包，你将作为第二个联签名人使用。要获取你的钱包地址，点击顶部的查看链接，然后点击地址。

接下来，右键单击一个地址，你希望查看其公钥。这将显示地址的公钥。见图 4-17。

+   以下是示例的钱包地址：mxaFFFW5CFfJi6fbhn1qFDi8gv6eFsSBKQ

+   以下是示例的公钥：038e6fb8b842c750eb68bfccfd0fa1aa1ce8e455d58137e260a067e6d2fb853ea6

![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig17_HTML.jpg](img/475651_1_En_4_Fig17_HTML.jpg)

图 4-17

电子标准钱包地址和公钥

接下来，您将通过命令行 RPC 为您的联合签署者创建一个新的地址。> bitcoin-cli getnewaddress2Msggcttx7wDDbcib6yD8ng2oKRdq8Bz4wV 之后，您可以设置两个联合签署者的地址。> address1=2Msggcttx7wDDbcib6yD8ng2oKRdq8Bz4wV> address2=mxaFFFW5CFfJi6fbhn1qFDi8gv6eFsSBKQ 确保地址正确，使用 validateaddress 命令。> bitcoin-cli validateaddress $address2 创建联合签署者钱包，您需要两个签署者的公钥。您已经拥有 Electrum 钱包的公钥；现在您需要比特币核心的 RPC 公钥。要获取此公钥，您可以使用 getaddressinfo 命令查看 RPC JSON 响应和 pubkey 变量。> bitcoin-cli getaddressinfo $address1{  "address": "2Msggcttx7wDDbcib6yD8ng2oKRdq8Bz4wV",  "scriptPubKey": "a91404d0a132b5796d4462f39865d56af4ff7255d1b287",  "ismine": true,  "iswatchonly": false,  "isscript": true,  "iswitness": false,  "script": "witness_v0_keyhash",  "hex": "001440bbb1a949badb3a12a941a44bc994f7127c595c",  "pubkey": "034ffed96ffc416b90daa97df5c09b618d7fbf99076ed8100900cfa0890e763ac0",  "embedded": {    "isscript": false,    "iswitness": true,    "witness_version": 0,    "witness_program": "40bbb1a949badb3a12a941a44bc994f7127c595c",    "pubkey": "034ffed96ffc416b90daa97df5c09b618d7fbf99076ed8100900cfa0890e763ac0",    "address": "tb1qgzamr22fhtdn5y4fgxjyhjv57uf8ck2u4glnj9",    "scriptPubKey": "001440bbb1a949badb3a12a941a44bc994f7127c595c"  },  "label": "",  "timestamp": 1541782726,  "hdkeypath": "m/0'/0'/9'",  "hdseedid": "572deaa922cbf31076701942878c3e5fc2e23b60",  "hdmasterkeyid": "572deaa922cbf31076701942878c3e5fc2e23b60",  "labels": [    {      "name": "",      "purpose": "receive"    }  ]}现在，您已准备好通过 createmultisig 命令创建联合签署者的多签地址，因为您已经拥有两个签署者的公钥。> bitcoin-cli -named createmultisig nrequired=2 keys="'["034ffed96ffc416b90daa97df5c09b618d7fbf99076ed8100900cfa0890e763ac0","038e6fb8b842c750eb68bfccfd0fa1aa1ce8e455d58137e260a067e6d2fb853ea6"]"'{  "address": "2MtBkhgVLJ6VA1nFbjam36iUY1dCiWFf4ix",  "redeemScript": "5221034ffed96ffc416b90daa97df5c09b618d7fbf99076ed8100900cfa0890e763ac021038e6fb8b842c750eb68bfccfd0fa1aa1ce8e455d58137e260a067e6d2fb853ea652ae"}接下来，您需要选择一个 UTXO txid 和 vout 来签署您的交易，就像您在之前的原始交易中所做的一样。> bitcoin-cli listunspent[  {    "txid": "ea3fb46ab103d15120e02ed6b60e3d83b265fed26794e3ed739496b62445410b",    "vout": 0,    ...]然后，设置 utxo_txid 属性。> utxo_txid=ea3fb46ab103d15120e02ed6b60e3d83b265fed26794e3ed739496b62445410b> utxo_vout=0> recipient="mv4rnyY3Su5gjcDNzbMLKBQkBicCtHUtFB"> rawtxhex=$(bitcoin-cli -named createrawtransaction inputs="'[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]"' outputs="'{ "'$recipient'": 0.001}"')现在解码并设置 hexstring 属性。> bitcoin-cli -named decoderawtransaction hexstring=$rawtxhex> bitcoin-cli signrawtransactionwithwallet $rawtxhex{  "hex": "020000000001010b414524b6969473ede39467d2fe65b2833d0eb6d62ee02051d103b16ab43fea0000000017160014040c578cf60bf00980bfde1920f54459eaab3a09ffffffff01a0860100000000001976a9149f9a7abd600c0caa03983a77c8c3df8e062cb2fa88ac024730440220603883ace41bdf5cf85c87e80f7362b45e35949114f46ac5e5b89f5e13d8d95002205c5eb45ca7de8b2da88c41c4311711beb14e8e0d679e40d1fbc2cb8e81e053fb01210205e848e0f22dfe0c428d02c356d0c9a8d064a789a6bbcaa43a245d701948aba200000000",  "complete": true}最后，通过 signed

### 可替换交易与锁时间

当使用 createrawtransaction 命令创建 RawTransaction 时，你可以包含两个更多变量，你可以利用：锁时间和可替换。createrawtransaction [{"txid":"id","vout":n},...] [{"address":amount},{"data":"hex"},...] ( locktime ) ( replaceable )

你可以在这里了解更多关于这些参数的信息：

[`bitcoincore.org/en/doc/0.17.0/rpc/rawtransactions/createrawtransaction/`](https://bitcoincore.org/en/doc/0.17.0/rpc/rawtransactions/createrawtransaction/)

正如名字 suggest 的那样，replaceable allows a raw transaction to be replaced by a new transaction with higher fees. This happens when the fee you set is too low, causing the transaction not to go through. For instance, if the fee you are trying to pay is too high, you can get the following error message:absurdly-high-fee, 11563419 > 10000000 (code 256)

Bitcoin core 支持在 raw transaction 中的锁时间参数；这个参数允许你在未来某个时间发送交易，直到它们被发送，发送者可以取消交易。

有两个选项。区块高度用于小数字，UNIX 时间戳用于大数字。这些参数意味着在满足条件之前，交易不会插入到区块中。

### 注意

区块高度是链中任何特定块和链上第一个块之间的区块数量。

## 比特币彩色币

比特币交易具有一个名为 OP_RETURN 的属性。这个属性可以用来存储最多 80 个字节的数据显示，这可以用来传递数据。这可能看起来并不多，但对于证明所有权或传递用于认证的小数据片段来说已经足够了。利用 OP_RETURN 属性是通过在交易的 vout 属性中设置数据代码词来完成的。要传递我们想要包含在交易中的数据，你仍然需要为交易 inclusion in the blockchain 发送资金，但你可以将收款人设置为你的自己的钱包，以防你不想付钱给某人。这样，你就可以在比特币持久性区块链中存储数据，而且你只需要支付交易费用，因为你不需要付给任何人。

### 注意

OP_RETURN 是定义交易为有效或无效的操作码脚本；它可以用来插入数据到交易中，这将导致存储该数据在比特币区块链中。请注意，关于是否可以利用这个属性存在不同的意见。一些人认为在区块链中存储非货币数据是个坏主意；因为存储数据有更低成本和更有效的方式，这真的取决于使用方式。

### 使用 OP_RETURN 发送交易

在设置你的交易之前，你将想要引入一个叫做 jq 的小型轻量级工具程序来简化创建 RawTranaction 对象。这是一个命令行 JSON 处理器，你可以用它在终端处理你的 RPC JSON。你可以在[`stedolan.github.io/jq/download`](https://stedolan.github.io/jq/download)下载它。

用 Brew 安装它。> brew install jq

jq 工具允许你检索返回 JSON 的部分内容，这样你就能更快地流式传输交易，且错误更少。

接下来，你可以设置一些数据通过 OP_RETURN 参数发送。这个例子将创建一个文件的 MD5。在现实生活中，这可以是双方之间的合同版本或任何你需要的代码片段。

### 注意

Message-Digest 5（MD5）算法是一个生成 128 位哈希值的函数。因为每个文件更改都会导致新的 MD5 结果，所以通常创建一个文件来保存校验和文件，以确保数据的完整性。

你可以选择比特币的核心文件，如 config.log 来生成 MD5 散列，并设置 op_return_data 变量。> md5 config.logMD5（config.log）= 634ef85e038cea45bd20900fc97e09dc> op_return_data="634ef85e038cea45bd20900fc97e09dc"正如你在本章前面所看到的，你可以使用 listunspent 命令来选择你想花费的 UTXO。> bitcoin-cli listunspent 现在使用 jq 工具，你可以流式传输过程，因此你不需要复制和粘贴，也可以避免错误。> utxo_txid=$(bitcoin-cli listunspent | jq -r '.[0] | .txid')>

注意这里的一些事情。你在这里设置了第一个 JSON 项目[0]，但你可以选择任何你想要的项目，比如[1]或[2]。另外，注意你需要运行 listunspent 命令来找出 UTXO 的“金额”。对于这个例子，金额是 0.1166341，既然你想要支付 0.00000200 作为费用（200 个比特币），那么你将总共发送 0.1166321。

如果你没有正确设置费用，你可能会在费用上花太多钱，或者收到如下错误信息：- 最小中继费用未满足，29 < 161（代码 66）- 费用过高，24432219 > 10000000（代码 256）你可以使用 echo 命令来确保你的变量设置正确。然后你可以继续设置你的交易数据。> rawtxhex=$(bitcoin-cli -named createrawtransaction inputs="'[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]' outputs="'{ "data": "'$op_return_data'", "'$recipient'": 0.1166321}"')接下来，你需要签名并发送交易。> signedtx=$(bitcoin-cli signrawtransactionwithwallet $rawtxhex | jq -r '.hex')> bitcoin-cli sendrawtransaction $signedtx43a14c3b1ac446e4774c5338e5ae4e23839ab65a38c45da8b790f4449b090ae5

现在，你可以在测试网区块链浏览器账本上跟踪 RawTransaction 对象，如图 4-18 所示。这里是网址：[`stedolan.github.io/jq/download`](https://stedolan.github.io/jq/download)。

[`live.blockcypher.com/btc-testnet/tx/43a14c3b1ac446e4774c5338e5ae4e23839ab65a38c45da8b790f4449b090ae5/`](https://live.blockcypher.com/btc-testnet/tx/43a14c3b1ac446e4774c5338e5ae4e23839ab65a38c45da8b790f4449b090ae5/) ![../images/475651_1_En_4_Chapter/475651_1_En_4_Fig18_HTML.jpg](img/475651_1_En_4_Fig18_HTML.jpg)

图 4-18

测试网络块浏览器，带有数据的交易

正如您在图 4-18 中看到的，您收到了“交易中嵌入未知协议的数据”的信息。如果您设计一些经常使用这种方法的软件，您将希望包含一个关键词来识别您的数据。

### 比特币的彩色硬币

彩色硬币的名称来源于比特币核心的较早实现 EPOBC 协议，其中资产与 satoshis（因此称为“着色”）相关联。现在，您可以通过 OP_RETURN 参数实现着色。

OP_RETURN 为您的硬币赋予了颜色，并为比特币区块链提供了新功能，因为您能够嵌入提供所有权证明的数据。您还可以设置其他条件，在特定时间发生或在您插入区块链的交易中传递相关数据。OP_RETURN 功能强大，在本书的后文中，您将了解到 OP_RETURN 如何在生产级项目中得到应用，以解决各种问题。

## 总结

在本章中，您深入研究了比特币核心 RPC。您生成了一个遗留的比特币钱包和一个 SegWit 比特币钱包，并且能够检索到钱包的私钥，更好地理解了椭圆曲线数字签名算法（ECDSA）以及公钥和私钥是如何创建的。

在本章中，您的大部分时间都花在了研究交易上；您在比特币守护进程上测试网络发送硬币，也使用了比特币核心钱包 GUI 发送硬币。在发送硬币之后，您学习了如何在比特币块浏览器中查看您的交易。接着，您研究了 RawTransaction，并学会了如何使用一个输出生成交易，以及如何通过 Electrum 以及命令行生成更复杂的具有多个签署人的交易。

此外，您还了解到其他选项，如为更改费用替换您的交易以及设置锁定时间变量。您了解了 P2PKH 和 P2SH-SEGWIT 之间的区别。最后，我介绍了如何使用 OP_RETURN 参数传递数据，这可以用于比特币彩色硬币，或者只是利用比特币的区块链传递附加数据，而不仅仅是花费硬币。在下一章中，您将更详细地了解以太坊以及如何编写智能合约。
