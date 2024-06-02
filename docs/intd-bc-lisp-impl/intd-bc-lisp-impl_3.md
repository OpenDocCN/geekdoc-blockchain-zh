© 作者（们），独家许可给 APress Media, LLC，Springer Nature 子公司 2021B. Sitnikovski《用 Lisp 介绍区块链》[`doi.org/10.1007/978-1-4842-6969-5_3`](https://doi.org/10.1007/978-1-4842-6969-5_3)

# 3. 区块链实现

Boro Sitnikovski^(1  )(1)北马其顿斯科普里![../images/510363_1_En_3_Chapter/510363_1_En_3_Figa_HTML.jpg](img/510363_1_En_3_Figa_HTML.jpg)

*《通往抽象的门户》，作者 D. Bozhinovski*

现在我们已经具备了编写计算机程序的能力，我们将实现区块链的组件（数据结构和操作）。在本章中，我们将使用一些新的程序。对于其中一些程序，我们将提供简要解释。对于其他程序，如果你感兴趣，可以从 Racket 的手册中获得更多详细信息。

本章的每一节都是动手操作的，这意味着在我们进行操作时，你将不得不实现它们。我们提供了练习，以确保你了解我们构建的过程将如何使用。在我们开始之前，请记住在每个文件的顶部加上 #lang racket，就像我们在上一章中提到的那样。

与以前一样，以 > 开头的代码片段应在 REPL 中进行评估。不要将它们的定义保存在实际的目标文件中。

我们从定义序列化开始。在下一章中，当节点互相发送信息时，我们将大量依赖它。把它看作是一种将数据结构转换为易于在节点之间传输的对象的整洁方式。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figb_HTML.gif](img/510363_1_En_3_Figb_HTML.gif)定义 3-1

**序列化**是将对象转换为字节流以存储对象或将其传输到内存、数据库或文件的过程。**反序列化**是相反的过程——将字节流转换为对象。

## 3.1 钱包.rkt 文件

在本节中，我们将实现钱包。它们将由后续交易使用，以确定发送/接收资金的来源和目的地。

正如我们之前讨论的，钱包是包含公钥和私钥的结构。钱包具有以下形式：1   (**struct** 钱包 2     (私钥 公钥)3     **#:prefab**)

#: 运算符代表**可选关键字参数**—基本上是一个参数，其值可以通过引用此参数的名称来设置。相反，对于普通参数，我们必须依赖它们的顺序来设置它们的值。例如，在 (lambda (x y z) ...) 中，我们必须在为 z 传递值之前传递 x 和 y 的值。

#:prefab 部分是新内容。一个预制结构类型是一种内置类型，Racket 打印机已知它。我们可以打印/显示结构及其所有内容。此外，我们可以序列化/反序列化这些类型的结构。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figc_HTML.gif](img/510363_1_En_3_Figc_HTML.gif)定义 3-2

**RSA** 是一种用于加密和解密消息的非对称密钥算法，与第 1.2.2 节描述的算法类似。

我们将创建一个过程，通过生成随机的公钥和私钥来创建一个钱包，并且它将依赖于 RSA 算法。1   (**define** (make-wallet)2     (**letrec** ([rsa-impl (get-pk 'rsa libcrypto-factory)]3              [privkey (generate-private-key rsa-impl '((nbits 512)))]4              [pubkey (pk-key->public-only-key privkey)])5       (wallet (bytes->hex-string6                (pk-key->datum privkey 'PrivateKeyInfo))7               (bytes->hex-string8                (pk-key->datum pubkey 'SubjectPublicKeyInfo)))))我们使用的所有过程都来自 crypto 包：

+   get-pk 返回 RSA 实现算法。

+   generate-private-key 生成给定算法（在本例中为 RSA）的私钥。

+   pk-key->public-only-key 返回给定公钥/私钥的公钥。

+   pk-key->datum 返回一个公钥/私钥，以便下一个列表中的程序可以轻松序列化。

+   bytes->hex-string 将十六进制字符串（比如数字）转换为字节，例如"0102030304" -> "Hello"。

我们需要引入必要的软件包：1   (**require** crypto)2   (**require** crypto/all)并且我们导出所有内容，以便该过程可以作为一个软件包使用。1   (**provide** (**struct-out** wallet) make-wallet)

struct-out 语法是将结构与其生成的过程一起导出。

以下是一个生成的钱包示例：1   > (make-wallet)2   '#s(wallet3       "3082015502010030..."4       "305c300d06092a86...")

现在，我们可以为我们的区块链创建钱包的方式了。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figd_HTML.gif](img/510363_1_En_3_Figd_HTML.gif)练习 3-1

使用 make-wallet 创建一个钱包，并使用 define 将其存储在一个变量中。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Fige_HTML.gif](img/510363_1_En_3_Fige_HTML.gif)练习 3-2

提取先前创建的钱包的私钥和公钥。代码应该看起来像 (wallet-?? (make-wallet))。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figf_HTML.gif](img/510363_1_En_3_Figf_HTML.gif)练习 3-3

通过阅读手册，简要了解加密软件包中使用的过程。

**提示**：如果你的本地文档中没有有关加密包的信息，请参考[`docs.racket-lang.org`](https://docs.racket-lang.org/)。

## 3.2 区块.rkt 文件

请记住，区块链就是一个块的列表，如图 1-4 (第 1) 中所示。因此，区块是区块链的基本组成部分，在本节中，我们将提供块的实现。

### 3.2.1 构造

区块应包含当前哈希、上一个哈希、数据以及生成时间戳：1   > (**struct** block2   (current-hash previous-hash data timestamp)3   **#:prefab**)

使用散列算法将使我们能够确认区块是否有效。

一般来说，区块可以包含任何数据，不仅限于交易，但我们目前将其限制为交易。我们还将为 Hashcash 算法添加一个 nonce 字段。我们稍后会看到这个字段的用途：1   (**struct** block2     (current-hash previous-hash transaction timestamp nonce)3     **#:prefab**)我们的区块还包含一个大致如下形式的交易：1   > (**struct** transaction2     (signature from to value)3     **#:prefab**)

我们稍后会详细实现交易。

生成区块的一种方式如下：1   > (block "123456" "234" (transaction "BoroS" "Boro" "You" 123) 1 1)2   '#s(block "123456" "234" #s(transaction "BoroS" "Boro" "You" 123)3   1 1)

例如，这个区块将从“Boro”转账给“You”，金额为 123，时间戳和 nonce 为 1。

### 3.2.2 散列和验证

接下来，我们将实现一个计算区块哈希的过程。我们将使用 SHA 散列算法。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figg_HTML.gif](img/510363_1_En_3_Figg_HTML.gif)

定义 3-3

**SHA** 是一种散列算法，它接受一个输入并产生一个哈希值。

下面是该过程的样子：1   (**define** (calculate-block-hash previous-hash timestamp transaction nonce)2     (bytes->hex-string (sha256 (bytes-append3              (string->bytes/utf-8 previous-hash)4              (string->bytes/utf-8 (number->string timestamp))5              (string->bytes/utf-8 (~a (serialize transaction)))6              (string->bytes/utf-8 (number->string nonce))))))这里有几点需要注意：

+   我们期望结构中的每个字段都是字符串类型。这样将在后面（例如在我们想要将区块链存储到数据文件时）使事情变得更简单。

+   如果你查阅 sha256 的手册，你会注意到它接受字节。这意味着我们必须使用`string->bytes/utf-8`将每个字段转换为字节，然后在散列它们之前将所有这些字节拼接在一起。

+   `number->string`将一个数字转换为字符串，例如 3 -> "3"，而`~a`也做同样的事情，但它也可以将对象转换为字符串。

+   我们对一个交易使用`serialize`函数。这个程序接受一个对象，并返回包含相同内容的 S 表达式。并非所有对象都可以被序列化；然而，在这种情况下，我们使用`#:prefab`，它还使结构可序列化。

+   最后，我们将哈希值存储为十六进制字符串。将十六进制视为一种将字符串从可读字符转换为数字的方式，例如，“Hello” -> "0102030304"。

作为一个例子，这是我们如何计算我们早期示例区块的哈希值：1   >  (calculate-block-hash  "234"  1  (transaction  "BoroS"  "Boro"  "You"2   "a book") 1)3   "5e2889a76a464ea19a493a74d2da991a78626fc1fa9070340c2284ad92f4dd17"现在我们有了计算区块哈希的方法，我们还需要一种验证它的方法。为此，我们只需再次对区块内容进行哈希处理，并将此哈希与存储在区块中的哈希进行比较：1   (**定义** (valid-block? bl)2     (equal? (block-current-hash bl)3             (calculate-block-hash (block-previous-hash bl)4                                   (block-timestamp bl)5                                   (block-transaction bl)6                                   (block-nonce bl))))

### 3.2.3 Hashcash 算法

此时，我们已经拥有了实现 Hashcash 算法所需的一切。1   (**定义** 难度 2)2   (**定义** 目标 (`bytes->hex-string` (`make-bytes` 难度 32)))

我们将难度设置为 2，因此目标将包含使用名为`make-bytes`的内置程序生成的难度数目的字节。

如果哈希与目标匹配，则将认为区块已挖掘，考虑到难度：1   (**define** (mined-block? block-hash)2     (equal? (subbytes (hex-string->bytes block-hash) 1 difficulty)3             (subbytes (hex-string->bytes target) 1 difficulty)))这里需要注意的几件事：

+   hex-string->bytes 只是一种将十六进制字符串转换为字节的方法，例如，"0102030304" -> #"\1\2\3\3\4"。

+   subbytes 接受一个字节列表、一个起始点和一个结束点，并返回该子列表。

+   因此，给定一个随机哈希，在此情况下，如果其前两个字节与目标匹配，我们认为它是有效的。

实际的 Hashcash 过程如下：1   (**define** (make-and-mine-block2             previous-hash timestamp transaction nonce)3     (**let** ([current-hash (calculate-block-hash4                   previous-hash timestamp transaction nonce)])5       (**if** (mined-block? current-hash)6           (block current-hash previous-hash transaction timestamp nonce)7           (make-and-mine-block8            previous-hash timestamp transaction (+ nonce 1)))))

该过程会不断增加 nonce，直到出现有效的区块，此时会返回该区块。也就是说，我们不断地改变 nonce，直到 sha256 生成与目标匹配的哈希为止。这定义了挖矿（工作证明）的基础。

例如，这是我们如何挖掘我们之前提到的区块的示例：1   > (**define** mined-block (make-and-mine-block "234" 1 (transaction "BoroS"2     "Boro" "You" "a book") 1))3   > (block-nonce mined-block)4   3375   > (block-previous-hash mined-block)6   "234"7   > (block-current-hash mined-block)8   "e920d627196658b64e349c1d3d6f2de1ab308d98d1c48130ee36df47ef25ee9a"

注意，nonce 必须增加到 337 才能满足挖矿条件。这是所需的“工作量”。在某些情况下，它会更小，在其他情况下，它会更大。

最后，我们需要一个小的辅助程序：1   (**定义** (mine-block transaction previous-hash)2     (make-and-mine-block3      previous-hash (current-milliseconds) transaction 1))

current-milliseconds 返回自 1970 年 1 月 1 日午夜 UTC 以来的当前时间（以毫秒为单位）。

我们提供以下结构和程序：1   (**提供** (**struct-out block**) mine-block valid-block? mined-block?)并确保我们需要所有必要的包：1   (**需要** (**only-in** file/sha1 hex-string->bytes))2   (**需要** (**only-in** sha sha256))3   (**需要** (**only-in** sha bytes->hex-string))4   (**需要** racket/serialize)

only-in 语法仅从我们指定的包中导入特定对象，而不是导入所有内容。

此时，除了能够创建和签名钱包外，我们现在还有了创建和挖掘区块所需的程序。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figh_HTML.gif](img/510363_1_En_3_Figh_HTML.gif)练习 3-4

使用 block（和 transaction）创建一个区块（含一笔交易），并使用 define 存储在一个变量中。然后使用 calculate-block-hash 计算其哈希值。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figi_HTML.gif](img/510363_1_En_3_Figi_HTML.gif)练习 3-5

在你生成的区块上使用 make-and-mine-block。随机数计数是多少，即挖掘该区块需要多少“工作”（处理）？

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figj_HTML.gif](img/510363_1_En_3_Figj_HTML.gif)练习 3-6

在前一个练习中的区块上使用 valid-block?。现在在随机数为 1 的那个区块上使用 valid-block?。

**提示**：为了从一个名为 bl 的现有区块生成一个“新”的区块，你可以使用：

1   (block (block-current-hash bl)

2          (block-previous-hash bl)

3          (block-transaction bl)

4          (block-timestamp bl)

5          (block-nonce bl))

## 3.3 utils.rkt 文件

此文件将包含其他组件将使用的常见过程。

我们经常使用的一个过程是 true-for-all?。如果谓词满足列表的所有成员，则返回 true，否则返回 false：1   （**定义**（true-for-all? pred list）2     （**cond**3       （（empty? list）#t）4       （（pred（car list））（true-for-all? pred（cdr list）））5       [**else** #f]））以下是我们如何使用它的示例：1   >（true-for-all?（**lambda**（x）（> x 3））'（1 2 3））2   #f3   >（true-for-all?（**lambda**（x）（> x 3））'（4 5 6））4   #t 接下来，我们需要一个将结构导出到文件的过程：1   （**定义**（struct->file object **file**）2     （**let**（[out（open-output-file **file #:exists** 'replace）]）3     （write（serialize object）out）4     （close-output-port out）））

open-output-file 返回内存中的一个对象，我们可以使用 write 将其写入。当我们这样做时，它将写入已打开的文件。close-output-port 关闭内存中的这个对象。此过程将序列化一个结构，然后将序列化的内容写入文件。

以下过程是 struct->file 的相反过程：给定一个文件，它将通过打开文件、读取其内容和反序列化其内容来返回一个结构。1   （**定义**（file->struct **file**）2     （**letrec**（[in（open-input-file **file**）]3              [result（read in）]）4     （close-input-port in）5     （deserialize result）））这里有几点需要注意：

+   read 将从 in 中读取数据并返回（与 write 相反）。

+   open-input-file 与 open-output-file 类似，只是它用于使用 read 从文件中读取。

+   deserialize 是 serialize 的相反操作。

我们提供这些过程：1   （**提供** true-for-all? struct->file file->struct）并确保我们需要所有必要的包：1   （**要求** racket/serialize）

现在我们有一种将我们的区块链数据写入文件系统（并从文件系统中读取）的方法。这样，我们的区块链数据就可以持久化了。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figk_HTML.gif](img/510363_1_En_3_Figk_HTML.gif)练习 3-7

在某个区块上使用 struct->file 将其存储到文件中。然后，在同一个文件上使用 file->struct。你得到了相同的区块吗？接下来，使用文本编辑器打开你创建的文件。文件内容是什么样子的？

## 3.4 交易

在本节中，我们将实现签名和验证交易的过程，如图 1-2 所示（第一章）。

### 3.4.1 交易-io.rkt 文件

交易结构将由一个交易-io 结构（交易输入/输出）组成。交易输入将代表从哪个区块链地址发送了资金，而交易输出将代表资金发送至哪个区块链地址。

此结构包含一个哈希，以便我们能够验证其有效性。它还具有一个值，一个所有者和一个时间戳。1   (**struct** transaction-io2     (transaction-hash value owner timestamp)3     **#:prefab**)类似于一个区块，我们将使用相同的代码来创建一个哈希，并依赖于序列化：1   (**define** (calculate-transaction-io-hash value owner timestamp)2     (bytes->hex-string  (sha256  (bytes-append3              (string->bytes/utf-8 (number->string value))4              (string->bytes/utf-8 (~a (serialize owner)))5              (string->bytes/utf-8  (number->string  timestamp))))))make-transaction-io 是一个帮助程序，它将初始化时间戳：1   (**define** (make-transaction-io value owner)2     (**let** ([timestamp (current-milliseconds)])3       (transaction-io4        (calculate-transaction-io-hash value owner timestamp)5        value6        owner7        timestamp)))一个 transaction-io 结构如果其哈希等于值、所有者和时间戳的哈希，则有效：1   (**define** (valid-transaction-io? t-in)2     (equal? (transaction-io-transaction-hash t-in)3             (calculate-transaction-io-hash4              (transaction-io-value t-in)5              (transaction-io-owner t-in)6              (transaction-io-timestamp  t-in))))下面是一个使用示例：1   > (make-transaction-io 123 "Some person")2   '#s(transaction-io "df652a3c15feba2eb9071cfdd810130c971f7fe7494a4710ee623   2fca11f0d83e" 123 "Some person" 1573765357289)4   > (valid-transaction-io? (transaction-io "df652a3c15feba2eb9071cfdd810135   0c971f7fe7494a4710ee622fca11f0d83e" 123 "Some person" 1573765357289))6   #t7   > (valid-transaction-io? (transaction-io "badhash" 123 "Some person"8   1573765357289))9   #f 最后，我们导入必要的包并导出这些程序：1   (**require** (**only-in** sha sha256))2   (**require** (**only-in** sha bytes->hex-string))3   (**require** racket/serialize)45   (**provide** (**struct-out** transaction-io)6             make-transaction-io valid-transaction-io?)

现在我们有了一种方法来存储交易输入/输出，我们可以继续进行实际的交易实现。

### 3.4.2 交易.rkt 文件

此文件将包含用于签署和验证交易的过程。它还将使用交易输入和输出，并将它们存储在单个交易中。

这是我们需要的所有内容：1   (**require** "transaction-io.rkt")2   (**require** "utils.rkt")3   (**require** (**only-in** file/sha1 hex-string->bytes))4   (**require** "wallet.rkt")5   (**require** crypto)6   (**require** crypto/all)7   (**require** racket/serialize)交易包含一个签名、发送方、接收方、价值和输入输出列表（transaction-io 对象）。1   (**struct** transaction2     (signature from to value inputs outputs)3     **#:prefab**)

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figl_HTML.gif](img/510363_1_En_3_Figl_HTML.gif)

定义 3-4

在 Racket 中，**加密工厂** 包括特定的加密算法实现。

除了代码之外，我们还需要使用所有加密工厂。它们将允许我们使用一些程序，例如 hex<->pk-key：1   (use-all-factories!)我们需要一个过程，它制作一个空的、未签名的、未处理的（没有输入输出）交易。稍后在我们发送资金或创建第一个（创世）交易时将使用此过程。1   (**define** (make-transaction from to value inputs)2     (transaction3       ""4       from5       to6       value7       inputs8       '()))

#### 3.4.2.1 数字签名

接下来，我们需要一个流程来签署交易。它类似于我们之前编写的使用哈希的流程，因为我们从结构中获取所有字节并追加它们。不同之处在于，在这种情况下，我们将使用数字签名来签署和验证数据。

要创建数字签名，我们使用哈希过程（在本例中，使用 SHA 算法）。然后使用私钥加密生成的哈希。加密的哈希将表示数字签名。 1 （**定义**（sign-transaction from to value）2 （**让**（[privkey（钱包私钥 from）] 3 [pubkey（钱包公钥 from）]）4 （bytes->hex-string 5 （digest/sign 6 （datum->pk-key（hex-string->bytes privkey）'PrivateKeyInfo）7 'sha1 8 （bytes-append 9 （string->bytes/utf-8（~a（serialize from）））10 （string->bytes/utf-8（~a（serialize to）））11 （string->bytes/utf-8（number->string value）））））））

digest/sign 是执行哈希和加密的过程。它接受一个私钥、一个算法^(1)和字节，并返回加密数据。

#### 3.4.2.2 处理交易

接下来，我们实现一个处理交易的流程，它将：

+   对 inputs-sum 中的所有输入求和。

+   计算剩余量，即输入总和与当前交易价值的差异。

+   根据交易的价值和剩余量生成新输出。

+   将旧输出（outputs）和新输出（new-outputs）合并到新生成的交易中（输入保持不变，稍后将由 UTXO 实现使用）。

+   使用 foldr + 0 l 计算数字列表 l 的总和。

换句话说，基于一些交易输入，该过程将创建包含交易价值和剩余资金的交易输出： 1   (**定义** (process-transaction t) 2     (**letrec** 3         ([inputs (transaction-inputs t)] 4          [outputs (transaction-outputs t)] 5          [value (transaction-value t)] 6          [inputs-sum 7           (foldr + 0 (map (lambda (i) (transaction-io-value i)) inputs))] 8          [leftover (- inputs-sum value)] 9          [new-outputs10           (list11            (make-transaction-io value (transaction-to t))12            (make-transaction-io leftover (transaction-from t)))])13       (transaction14        (sign-transaction (transaction-from t)15                          (transaction-to t)16                          (transaction-value t))17        (transaction-from t)18        (transaction-to t)19        value20        inputs21        (append new-outputs outputs))))我们还需要一个检查交易签名的过程： 1   (**定义** (valid-transaction-signature? t) 2     (**let** ([pubkey (wallet-public-key (transaction-from t))]) 3       (digest/verify 4        (datum->pk-key (hex-string->bytes pubkey) 'SubjectPublicKeyInfo) 5        'sha1 6        (bytes-append 7         (string->bytes/utf-8 (~a (serialize (transaction-from t)))) 8         (string->bytes/utf-8 (~a (serialize (transaction-to t)))) 9         (string->bytes/utf-8 (number->string (transaction-value t))))10         (hex-string->bytes (transaction-signature t)))))

digest/verify 是 digest/sign 的反义词，它确定签名是否有效。

最后，我们需要一个在以下条件下确定交易有效性的过程：

+   其签名是有效的：valid-transaction-signature?

+   所有的输出都是有效的：valid-transaction-io?

+   输入的总和大于或等于输出的总和：>= sum-inputs sum-outputs。这解决了双重支付的问题。

1   (**定义** (valid-transaction? t) 2     (**let** ([sum-inputs 3            (foldr + 0 (map (**lambda** (t) (transaction-io-value t)) 4                            (transaction-inputs t)))] 5           [sum-outputs 6            (foldr + 0 (map (**lambda** (t) (transaction-io-value t)) 7                            (transaction-outputs t)))]) 8       (**and** 9        (valid-transaction-signature? t)10        (true-for-all? valid-transaction-io? (transaction-outputs t))11        (>= sum-inputs sum-outputs))))

(and ...) 语法如果传递给它的所有值都是 #t，则返回 #t，否则返回 #f。相反，(or ...) 如果传递给它的至少有一个值是 #t，则返回 #t，否则返回 #f。

最后，我们导出以下内容：1   (**提供** (**all-from-out** "transaction-io.rkt")2            (**struct-out** transaction)3            make-transaction process-transaction valid-transaction?)

all-from-out 语法指定我们从目标中导入的所有对象（并且导出的对象）。在本例中，除了导出带有一些过程的交易结构的文件之外，它还从 transaction-io.rkt 中导出了所有内容。

除了钱包和区块之外，我们的实现还支持交易的创建和处理。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figm_HTML.gif](img/510363_1_En_3_Figm_HTML.gif)练习 3-8

使用上述过程创建、处理和验证交易。

**提示**：分别使用 make-transaction、process-transaction 和 valid-transaction?。

## 3.5 区块链.rkt 文件

现在我们将实现最后一个组件——区块链。我们需要引入一堆东西：1   (**require** "block.rkt")2   (**require** "transaction.rkt")3   (**require** "utils.rkt")4   (**require** "wallet.rkt")回想一下，UTXO 只是一个交易-io 对象的列表，其中它表示未花费的交易输出。在某种程度上，它类似于钱包的初始余额。因此，结构将包含一个块和 UTXO 的列表：1   (**struct** blockchain2     (blocks utxo)3     **#:prefab**)

### 3.5.1 初始化

我们将需要一个过程来初始化区块链。它应该接受创世交易、创世哈希和 UTXO：1   (**define** (init-blockchain t seed-hash utxo)2     (blockchain (cons (mine-block (process-transaction t) seed-hash) '())3                 utxo))初始化区块链的一种方式如下：1   > (**define** coin-base (make-wallet))2   > (**define** wallet-a (make-wallet))3   > (**define** genesis-t (make-transaction coin-base wallet-a 100  '()))4   > (**define** utxo (list5   >              (make-transaction-io 100 wallet-a)))6   > (**define** blockchain (init-blockchain genesis-t "1337cafe"  utxo))

### 3.5.2 奖励

在原始比特币实现中，区块奖励从第一个区块的 50 个硬币开始，并且在每 210000 个区块后减半。这意味着直到第 210000 个区块之前的每个区块都将奖励 50 个硬币，而第 210001 个区块将奖励 25 个硬币。换句话说，奖励使用以下公式计算，其中 *b* 是区块的数量。![$$ \frac{2^{\left\lfloor \frac{b}{210000}\right\rfloor }}{50} $$](img/510363_1_En_3_Chapter_TeX_Equa.png)我们遵循相同的算法。我们最初从 50 个硬币开始，然后在每 210000 个区块后减半。1   (**define** (mining-reward-factor blocks)2     (/ 50 (expt 2 (floor (/ (length blocks) 210000)))))

### 3.5.3 添加一个交易

下一个步骤将向区块链添加一个交易。它应该：

1.  1.

    挖掘一个区块。

1.  2.

    根据处理后的交易输出、输入和当前的 UTXO 创建一个新的 UTXO。

1.  3.

    通过添加新挖掘的区块生成一个新的区块链列表。

1.  4.

    根据当前的 UTXO 计算奖励。

另外，UTXO 将被视为一个集合，以便我们可以轻松地使用集合操作删除特定的输入并追加新的交易。1（**定义**（add-transaction-to-blockchain b t）2 （**letrec**（[hashed-blockchain 3 （mine-block t 4 （block-current-hash（car（blockchain-blocks b））））] 5 [processed-inputs（transaction-inputs t）] 6 [processed-outputs（transaction-outputs t）] 7 [utxo（set-union processed-outputs 8 （set-subtract（blockchain-utxo b）9 processed-inputs））]10 [new-blocks（cons hashed-blockchain（blockchain-blocks b））]11 [utxo-rewarded（cons12 （make-transaction-io13 （mining-reward-factor new-blocks）14 （transaction-from t））15 utxo））16）（blockchain17 new-blocks18 utxo-rewarded））

在关于 add-transaction-to-blockchain 的另一件事情是：给定一个区块链和一个交易，它返回一个新的、更新的区块链。这个新返回的区块链将是应该使用的最新的，因为之前的区块链不会包含这个新交易。这样，我们就避免了对之前的区块链进行变异。

接下来，我们将创建一个过程，用于确定钱包的余额——匹配所有未花费交易的总和：1   (**define** (balance-wallet-blockchain  b  w)2     (**letrec** ([utxo (blockchain-utxo b)]3             [my-ts (filter4                         (**lambda** (t) (equal? w (transaction-io-owner t)))5                         utxo)])6       (foldr + 0 (map (**lambda** (t) (transaction-io-value t)) my-ts))))我们还需要一个过程，通过启动交易然后将其添加到区块链进行处理，从一个钱包发送钱到另一个钱包。my-ts 将包含当前接收者的交易输入。最后，我们只有在交易有效时才将交易添加到区块链。1   (**define** (send-money-blockchain b from to value) 2     (**letrec** ([my-ts 3                       (filter (**lambda** (t) (equal? from (transaction-io-owner t))) 4                               (blockchain-utxo b))] 5                     [t (make-transaction from to value my-ts)]) 6       (**if** (transaction? t) 7           (**let** ([processed-transaction (process-transaction t)]) 8             (**if** (**and** 9                     (>= (balance-wallet-blockchain b from) value)10                     (valid-transaction? processed-transaction))11                     (add-transaction-to-blockchain b processed-transaction)12                     b))13           (add-transaction-to-blockchain b '()))))

### 3.5.4 验证

我们现在将介绍一个过程，在以下条件下确定区块链的有效性：

+   所有区块都是通过 `valid-block?` 进行验证的。

+   使用 `equal?` 检查前一个哈希的匹配情况，通过将所有区块（除最后一个之外）的前一个哈希与所有区块（除第一个之外）的当前哈希进行比较。

+   使用 `valid-transaction?` 来验证所有交易是否有效。

+   所有区块都是通过 `mined-block?` 进行挖掘的。

1   (**define** (valid-blockchain? b) 2     (**let** ([blocks (blockchain-blocks b)]) 3       (**and** 4        (true-for-all? valid-block? blocks) 5        (equal? (drop-right (map block-previous-hash blocks) 1) 6                (cdr (map block-current-hash blocks))) 7        (true-for-all? 8         valid-transaction? (map 9                            (**lambda** (block) (block-transaction block))10                            blocks))11         (true-for-all?12         mined-block? (map block-current-hash blocks)))))最后，我们导出所有内容：1   (**provide** (**all-from-out** "block.rkt")2            (**all-from-out** "transaction.rkt")3            (**all-from-out** "wallet.rkt")4            (**struct-out** blockchain)5            init-blockchain send-money-blockchain6            balance-wallet-blockchain valid-blockchain?)

现在我们拥有所有必要的组件：管理钱包、区块、交易，最后是区块链。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Fign_HTML.gif](img/510363_1_En_3_Fign_HTML.gif)练习 3-9

创建两个集合，并对它们使用 set-subtract、set-union 和 set-intersect。观察结果。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figo_HTML.gif](img/510363_1_En_3_Figo_HTML.gif)练习 3-10

使用 init-blockchain 初始化区块链，并使用 add-transaction-to-blockchain 添加交易到其中。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figp_HTML.gif](img/510363_1_En_3_Figp_HTML.gif)练习 3-11

在上一个练习中的区块链上使用 valid-blockchain?（在添加新交易之前执行此操作，然后在添加新交易之后再次执行）。

![../images/510363_1_En_3_Chapter/510363_1_En_3_Figq_HTML.gif](img/510363_1_En_3_Figq_HTML.gif)练习 3-12

在区块链中进行转账，使用 send-money-blockchain。

## 3.6 集成组件

在这一部分中，我们将把所有各部分组合成一个单一的要点，并展示它们如何轻松使用。

### 3.6.1 主助手.rkt 文件

这个文件将从`blockchain.rkt`和`utils.rkt`导入所有内容，并提供一些打印过程。1   (**require** "blockchain.rkt")2   (**require** "utils.rkt")接下来的过程将把交易对象转换为可打印的字符串。它将使用`substring`仅打印哈希的子集（因为可能太大），并且还将使用`format`，这是一个字符串格式化过程，它将字符串中的每个∼a 替换为传递的参数。1   (**define** (format-transaction t)2     (format "...~a... 发送 ...~a... 数量为 ~a。"3             (substring (wallet-public-key (transaction-from t)) 64 80)4             (substring  (wallet-public-key  (transaction-to  t)) 64  80)5             (transaction-value t)))接下来的过程将打印一个块的详细信息。`printf`类似于`print`，但它可以像`format`一样使用：1   (**define** (print-block bl)2     (printf "块信息**\n**=================3   哈希:**\t**~a**\n**前一个哈希:**\t**~a**\n**时间戳:**\t**~a**\n**随机数:**\t**~a**\n**数据:**\t**~a**\n**"4         (block-current-hash bl)5         (block-previous-hash bl)6         (block-timestamp bl)7         (block-nonce bl)8         (format-transaction (block-transaction bl))))除了显式使用递归，还有一个内置的`for`语法，也允许重复的计算。为了打印区块链，我们将使用`for`语法遍历所有区块，将它们打印到标准输出，然后使用`newline`添加一个换行字符，使每个块的分隔明显：1   (**define** (print-blockchain b)2     (**for** ([block (blockchain-blocks b)])3       (print-block block)4       (newline)))我们类似地打印钱包：1   (**define** (print-wallets b wallet-a wallet-b)2     (printf "**\n**钱包 A 余额: ~a**\n**钱包 B 余额: ~a**\n\n**"3             (balance-wallet-blockchain b wallet-a)4             (balance-wallet-blockchain b wallet-b)))并导出过程：1   (**provide** (**all-from-out** "blockchain.rkt")2            (**all-from-out** "utils.rkt")3            format-transaction print-block print-blockchain print-wallets)![../images/510363_1_En_3_Chapter/510363_1_En_3_Figr_HTML.gif](img/510363_1_En_3_Figr_HTML.gif)练习 3-13

创建一个交易并使用 format-transaction 查看其输出。对一个块（print-block）、区块链（print-blockchain）和钱包（print-wallets）重复相同步骤。

### 3.6.2 主文件 main.rkt

这是我们将所有组件放在一起并使用它们的地方。我们首先通过使用 file-exists? 来检查 blockchain.data 文件是否存在。如果该文件存在，则它将包含来自先前区块链的内容。如果不存在，我们将创建一个新的区块链。 （**require** "main-helper.rkt") （**when** (file-exists? "blockchain.data") （**begin** （printf "发现 'blockchain.data'，正在读取...**\n**") （print-blockchain (file->struct "blockchain.data")) （exit)））

我们使用了 when，它类似于 if，但省略了 else 分支。

接下来，我们初始化钱包：1   (**define** coin-base (make-wallet))2   (**define** wallet-a (make-wallet))3   (**define** wallet-b (make-wallet))我们通过创建创世交易来初始化交易：1   (printf "制作创世交易...**\n**")2   (**define** genesis-t (make-transaction coin-base wallet-a 100 '()))我们初始化未花费的交易——创世交易：1   (**define** utxo (list2                 (make-transaction-io 100 wallet-a)))最后，我们通过挖掘创世交易来初始化区块链：1   (printf "挖掘创世区块...**\n**")2   (**define** blockchain (init-blockchain genesis-t "1337cafe" utxo))3   (print-wallets blockchain wallet-a wallet-b)制作第二笔交易：1   (printf "挖掘第二笔交易...**\n**")2   (**set!** blockchain (send-money-blockchain blockchain wallet-a wallet-b 2))3   (print-wallets blockchain wallet-a wallet-b)制作第三笔交易：1   (printf "挖掘第三笔交易...**\n**")2   (**set!** blockchain (send-money-blockchain blockchain wallet-b wallet-a 1))3   (print-wallets blockchain wallet-a wallet-b)尝试制作第四笔交易：1   (printf "尝试挖掘第四笔（无效）交易...**\n**")2   (**set!** blockchain (send-money-blockchain blockchain wallet-b wallet-a 3))3   (print-wallets blockchain wallet-a wallet-b)检查区块链的有效性：1   (printf "区块链是否有效: ~a**\n\n**" (valid-blockchain? blockchain))从区块链中打印每个区块：1   (**for** ([block (blockchain-blocks blockchain)])2     (print-block block)3     (newline))并将区块链导出到 blockchain.data，以便稍后重用：1   (struct->file blockchain "blockchain.data")2   (printf "已导出区块链到 'blockchain.data'...**\n**")创建 main.rkt 后，我们可以从 Racket > Run 菜单中运行它。它应该显示以下输出：1   制作创世交易... 2   挖掘创世区块... 3 4   钱包 A 余额: 100 5   钱包 B 余额: 0 6 7   挖掘第二笔交易... 8 9   钱包 A 余额: 13010   钱包 B 余额: 201112   挖掘第三笔交易...1314   钱包 A 余额: 14015   钱包 B 余额: 601617   尝试挖掘第四笔（无效）交易...1819   钱包 A 余额: 14020   钱包 B 余额: 602122   区块链是否有效: #t2324   区块信息 25   =================26   哈希:   e720bb198279a76057280bdf8eb667fe1883d0ae263c5d5d1be08697a2f534d127   哈希 _p: 38200563c1f807be2a5d10ec42dd53acae1f6f804b4c93016b87c974817f065d28   时间戳:  152992361057429   随机数:  21630   数据:   ...bb6... 发送 ...896... 金额为 10.3132   区块信息 33   =================34   哈希:   38200563c1f807be2a5d10ec42dd53acae1f6f804b4c93016b87c974817f065d35   哈希 _p: 6a20fbe4038bb3b83090e7f767bb24af5164218bba5c751a1858262df2a2a84736   时间戳:  152992361040537   随机数

## 3.7 总结

我们逐个构建每个组件，逐渐地。一些组件是*正交*的——它们彼此独立。例如，钱包实现不调用块中的任何过程，块可以独立于钱包使用。当我们将所有组件组合在一起时，我们得到一个区块链系统。

这种设计使我们能够轻松地扩展我们的系统。在下一章中，我们将扩展系统，增加点对点和智能合约功能，而无需更改基本组件。
