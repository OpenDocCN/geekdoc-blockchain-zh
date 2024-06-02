© 作者，独家许可由 APress Media, LLC 持有，隶属于 Springer Nature 2021B。Sitnikovski 以 Lisp 介绍区块链[`doi.org/10.1007/978-1-4842-6969-5_4`](https://doi.org/10.1007/978-1-4842-6969-5_4)

# 4. 扩展区块链

Boro Sitnikovski^(1  )(1) 马其顿首都斯科普里![../images/510363_1_En_4_Chapter/510363_1_En_4_Figa_HTML.jpg](img/510363_1_En_4_Figa_HTML.jpg)

*扩展，作者 D. Bozhinovski*

在上一章中，我们实现了区块链的基本组件。在本章中，我们将通过智能合约和点对点支持来扩展区块链。

## 4.1 智能合约的实现

比特币的区块链是可编程的，这意味着交易条件本身可以由用户编程。例如，用户可以编写*脚本*（短小的代码片段）来添加在进行交易之前必须满足的要求。

在第 2.4 节，我们创建了一个可执行文件，可以发送给我们的朋友，但他们无法更改可执行文件，因为他们没有原始代码。即使他们有原始代码，也并非所有用户都具有编程技能。

智能合约的要点是允许非程序员调整交易流程的行为，而无需更改原始代码。

### 4.1.1 smart-contracts.rkt 文件

这个想法是实现一个小语言，用户可以使用。我们的实现将依赖于事务：1   (**require** "transaction.rkt")我们必须扩展原始的 valid-transaction?，使其在计算有效性时也考虑合同：1   (**define** (valid-transaction-contract? t c)2     (**and** (eval-contract t c)3          (valid-transaction? t)))现在我们将实现一个过程，它将接受一个事务、一个合同、一个脚本语言（实际上只是一个 S 表达式），并返回一些值。返回的值可以是 true、false、数字或字符串。1   (**define** (eval-contract t c) 2     (**match** c 3       [(? number? x) x] 4       [(? string? x) x] 5       [`() #t] 6       [`true #t] 7       [`false #f] 8       [`(if ,co ,tr ,fa) (**if** co tr fa)] 9       [`(+ ,l ,r) (+ l r)]10       [**else** #f]))

我们在这里使用了称为匹配(match)的新语法。它类似于 cond，不同之处在于它可以直接比较对象的结构。例如，? <expr> <pat> 在<expr>为真时匹配并将值存储在<pat>中。在前面的代码中，如果我们传递一个数字，它将返回相同的数字。另外，如果我们传递 true 值（即 c 匹配 true），那么它将返回#t。另一个例子是如果 c 匹配形式为(if X Y Z)的结构（引用自 1），那么它将返回(if X Y Z)的评估结果。

这里有几个示例用法：1   > (**define** test-transaction (transaction "BoroS" "Boro" "You" "a book" 2     '() '())) 3   > (eval-contract test-transaction 123) 4   123 5   > (eval-contract test-transaction "Hi") 6   "Hi" 7   > (eval-contract test-transaction '()) 8   #t 9   > (eval-contract test-transaction 'true)10   #t11   > (eval-contract test-transaction 'false)12   #f13   > (eval-contract test-transaction '(if #t "Hi" "Hey"))14   "Hi"15   > (eval-contract test-transaction '(if #f "Hi" "Hey"))16   "Hey"17   > (eval-contract test-transaction '(+ 1 2))18   3 然而，我们仍然没有在我们的语言中使用任何交易的值。让我们用几个更多的命令来扩展它：1   ...2        [`from (transaction-from t)]3        [`to (transaction-to t)]4        [`value (transaction-value t)]5   ...现在我们可以这样做：1   > (eval-contract test-transaction 'from)2   "Boro"3   > (eval-contract test-transaction 'to)4   "You"5   > (eval-contract test-transaction 'value)6   "a book"我们将实现更多的操作符，以使脚本语言变得更具表现力：1   ...2        [`(* ,l ,r) (* l r)]3        [`(- ,l ,r) (- l r)]4        [`(= ,l ,r) (equal? l r)]5        [`(> ,l ,r) (> l r)]6        [`(\< ,l ,r) (\< l r)]7        [`(and ,l ,r) (**and** l r)]8        [`(or ,l ,r) (**or** l r)]9   ...然而，在语言实现中存在问题。考虑到(+ 1 2)和(+ (+ 1 2) 3)的计算：1   > (eval-contract test-transaction '(+ 1 2))2   33   > (eval-contract test-transaction '(+ (+ 1 2) 3))4   . . +: **contract** violation

匹配子句[`(+ ,l ,r) (+ l r)]出现问题。当我们匹配 '(+ (+ 1 2) 3)) 时，我们得到了 (+ '(+ 1 2) 3)，而 Racket 不能将一个带引号的列表与一个数字相加。解决此问题的方法是对每个子表达式进行*递归*评估。因此，匹配从[`(+ ,l ,r) (+ l r)]变为[`(+ ,l ,r) (+ (eval-contract t l) (eval-contract t r))]。

在这种情况下，评估将按如下进行：1   (eval-contract t '(+ (+ 1 2) 3))2   = (eval-contract t (list '+ (eval-contract t '(+ 1 2))3                               (eval-contract t 3)))4   = (eval-contract t (list '+ (+ 1 2) 3))5   = (eval-contract t (list '+ 3 3))6   = (eval-contract t '(+ 3 3))7   = (eval-contract t 6)8   = 6

记住引用列表和非引用列表之间的区别是很重要的；后者将尝试评估。在这种情况下，我们调整了引号以产生期望的结果。

我们将不得不重新编写所有的运算符： 1   ... 2        [`(+ ,l ,r) (+ (eval-contract t l) (eval-contract t r))] 3        [`(* ,l ,r) (* (eval-contract t l) (eval-contract t r))] 4        [`(- ,l ,r) (- (eval-contract t l) (eval-contract t r))] 5        [`(= ,l ,r) (= (eval-contract t l) (eval-contract t r))] 6        [`(> ,l ,r) (> (eval-contract t l) (eval-contract t r))] 7        [`(< ,l ,r) (< (eval-contract t l) (eval-contract t r))] 8        [`(**and** ,l ,r) (and (eval-contract t l) (eval-contract t r))] 9        [`(**or** ,l ,r) (or (eval-contract t l) (eval-contract t r))]10   ...语言中的 if 实现也存在相同的问题。因此，我们也会更改它：1   ...2        [`(if ,co ,tr ,fa) (**if** (eval-contract t co)3                           (eval-contract t tr)4                           (eval-contract t fa))]5   ...因此，最终的过程变为： 1   (**define** (eval-contract t c) 2     (**match** c 3       [(? number? x) x] 4       [(? string? x) x] 5       [`() #t] 6       [`true #t] 7       [`false #f] 8       [`(if ,co ,tr ,fa) (**if** (eval-contract t co) 9                              (eval-contract t tr)10                              (eval-contract t fa))]11       [`(+ ,l ,r) (+ (eval-contract t l) (eval-contract t r))]12       [`from (transaction-from t)]13       [`to (transaction-to t)]14       [`value (transaction-value t)]15       [`(+ ,l ,r) (+ (eval-contract t l) (eval-contract t r))]16       [`(* ,l ,r) (* (eval-contract t l) (eval-contract t r))]17       [`(- ,l ,r) (- (eval-contract t l) (eval-contract t r))]18       [`(= ,l ,r) (= (eval-contract t l) (eval-contract t r))]19       [`(> ,l ,r) (> (eval-contract t l) (eval-contract t r))]20       [`(< ,l ,r) (< (eval-contract t l) (eval-contract t r))]21       [`(**and** ,l ,r) (and (eval-contract t l) (eval-contract t r))]22       [`(**or** ,l ,r) (or (eval-contract t l) (eval-contract t r))]23       [**else** #f]))现在用户可以提供脚本代码，比如 (if (= (+ 1 2) 3) from to)：1   > (eval-contract test-transaction '(if (= (+ 1 2) 3) from to))2   "Boro"3   > (eval-contract test-transaction '(if (= (+ 1 2) 4) from to))4   "You"最后，我们提供输出，这只是交易有效性检查：1   (**provide** valid-transaction-contract?)

### 4.1.2 更新现有代码

现在我们已经实现了智能合约的逻辑，接下来需要解决的是前端——用户如何使用其功能。为此，我们将更新实现以支持通过读取文件来使用合约。如果存在名为 contract.script 的文件，我们将读取并解析它（使用 read），然后运行代码。

我们将在 blockchain.rkt 中重新编写发送货币的过程以接受合约。这是相同的过程，只是我们使用 valid-transaction-contract? 代替 valid-transaction?。

在这里，我们使用了 with-handlers，它接受一个处理当某些事情可能失败时的过程——在本例中为 read 或 open-input-file。

最后，请确保将 file->contract 添加到 utils.rkt 中提供的列表中。此外，在 main.rkt 中更新每次使用 send-money-blockchain 时，额外发送 (file->contract "contract.script") 作为参数，以便处理的合约是从 contract.script 中读取的那个。

我们还需要更新 blockchain.rkt 和 main.rkt，因为它们现在依赖于智能合约包中实现的一个过程。我们将在它们中添加 (require "smart-contracts.rkt")。

![../images/510363_1_En_4_Chapter/510363_1_En_4_Figb_HTML.gif](img/510363_1_En_4_Figb_HTML.gif)练习 4-1

想出几个有效的表达式，并使用 eval-contract 来评估它们。

![../images/510363_1_En_4_Chapter/510363_1_En_4_Figc_HTML.gif](img/510363_1_En_4_Figc_HTML.gif)练习 4-2

重复上一个练习，但使用 contract.script 文件。

**提示**：此练习可能需要您创建一个可执行文件。

## 4.2 对等体实现

在第 3.6.2 节，我们使用 DrRacket 来执行区块链实现。这对于测试目的来说没问题。但是，如果我们想要与其他用户分享该实现并要求他们执行它，那将会有点不方便，因为没有办法在不同用户之间共享数据。

在本节中，我们将实现对等支持，以便对我们的实现感兴趣的用户可以加入系统/社区。

在我们深入实现之前，图 4-1 展示了我们将构建的架构的高层概述。![../images/510363_1_En_4_Chapter/510363_1_En_4_Fig1_HTML.jpg](img/510363_1_En_4_Fig1_HTML.jpg)

图 4-1

对等体架构

每个对等节点（连接到系统的用户）列表将包括以下内容：

+   *对等体上下文数据：* 诸如与其他对等体的关系、连接的对等体列表等信息。

+   *通用处理程序：* 转换对等体上下文数据。

此外，将有两种与其他对等体建立通信的方式：

+   对等体将接受来自其他对等体的新连接。

+   对等体将尝试连接/建立新的与其他对等体的连接。

每当建立连接时，对等方将通过通用处理程序进行通信，解析和评估命令，例如同步/更新区块链，更新对等方列表等。

考虑以下示例场景：假设有三个对等方 - 对等方 1、对等方 2 和对等方 3。对等方 1 和对等方 2 在线，对等方 3 目前离线。对等方 1 有以下有效对等方列表：(对等方 1，对等方 2，对等方 3)。对等方 2 的对等方列表为空。根据图示，对等方 1 将接受新连接并尝试连接到对等方。因此，对等方 1 将尝试连接到对等方 2。此连接将成功，下一步是对等方 1 向对等方 2 发送一些数据（例如，有效对等方列表）。

对等方 2 的对等方列表为空，但现在它将与对等方 1 合并，因此它将变为 (对等方 1，对等方 2，对等方 3)。 对等方 1 和对等方 2 互相连接，并且它们将继续尝试连接到对等方 3。一旦对等方 3 可用，将执行相同的算法，对等方 3 将加入网络。

采用这种方法，目标是构建类似于图 1-1 和 1-3 （第一章）中显示的高级描述的系统。

构建这种类型的通信系统自然复杂。建议您为您将使用的每个过程参考 Racket 手册（通过按下 F1 键）。

### 4.2.1 对等方对等方.rkt 文件

要开始，我们将添加块实现的依赖项，并依靠序列化将数据发送到其他对等方：1   (**require** "blockchain.rkt")2   (**require** "block.rkt")3   (**require** racket/serialize)

#### 4.2.1.1 对等方上下文结构

我们将实现保存有关对等方信息的结构，以便我们有一个参考可以将数据发送到正确的目的地。peer-info 结构包含对等方的 IP 地址和端口信息。可以将 IP 地址和端口类比为街道地址和号码。1   (**结构体** peer-info2     (ip port)3     **#:prefab**)peer-info-io 结构还包含了用于对等方之间发送和接收数据的 IO 端口（通信通道）：1   (**结构体** peer-info-io2     (peer-info input-port output-port)3     **#:prefab**)

我们将 peer-info 和 peer-info-io 分开的原因是，在 main-p2p.rkt 中稍后，我们不会拥有输入/输出端口的上下文（在建立到对等方的连接之前），因此这为我们提供了重用结构的良好方法。

最后，peer-context-data 包含了单个对等方所需的所有信息，即：

+   有效对等方列表

+   连接的对等方列表

+   区块链的引用

1   (**结构体** peer-context-data2     (name3      port4      [valid-peers **#:mutable**]5      [connected-peers **#:mutable**]6      [blockchain **#:mutable**])7     **#:prefab**)

根据从连接的对等方检索到的信息，有效对等方的列表^(2) 将进行更新。连接的对等方列表将是有效对等方的（不一定严格的）子集。区块链将使用从所有对等方组合的数据进行更新。我们将它们设置为可变的，因为这提供了一种轻松更新数据的方法。

#### 4.2.1.2 通用处理器

通用处理器将是一个处理器过程，将由服务器（图中的“接受新连接”部分）和客户端（图中的“连接到新对等方”部分）共同使用。它将是一个接受命令的过程（命令的性质类似于智能合约的 eval-contract 实现），然后根据命令执行相应操作。

这里是对等方将发送给彼此的命令的列表：

| **请求** | **响应** | **备注** |
| --- | --- | --- |
| 获取有效的节点 | 有效的节点:X | 一个节点可以请求有效节点的列表。响应将是 X - 有效的节点。请注意，此响应应自动触发有效的节点命令。 |
| 获取最新的区块链 | 最新的区块链:X | 一个节点可以向另一个节点请求最新的区块链。响应将是 X - 区块链的最新版本。这应该触发最新的区块链命令。 |
| 最新的区块链:X |   | 当一个节点收到此请求时，如果它是有效的，它将更新区块链。 |
| 有效的节点:X |   | 当一个节点收到此请求时，它将更新有效节点列表。 |

在这张表中的命令将允许对等体彼此同步数据。我们现在将提供处理程序的实现。它接受一个对等体上下文和输入/输出端口。有了这些，它将读取输入（命令）并将适当的输出（评估后的命令）发送回对等体：1   (**define** (handler peer-context in out) 2     (flush-output out) 3     (**define** line (read-line in)) 4     (**when** (string? line) *; 它可能是 eof* 5       (**cond** [(string-prefix? line "get-valid-peers") 6              (fprintf out "valid-peers:~a\n" 7                       (serialize 8                        (set->list 9                         (peer-context-data-valid-peers peer-context))))10              (handler peer-context in out)]11             [(string-prefix? line "get-latest-blockchain")12              (fprintf out "latest-blockchain:")13              (write14               (serialize (peer-context-data-blockchain peer-context)) out)15              (handler peer-context in out)]16             [(string-prefix? line "latest-blockchain:")17              (**begin** (maybe-update-blockchain peer-context line)18                     (handler peer-context in out))]19             [(string-prefix? line "valid-peers:")20              (**begin** (maybe-update-valid-peers peer-context line)21                     (handler peer-context in out))]22             [(string-prefix? line "exit")23              (fprintf out "bye\n")]24             [**else** (handler peer-context in out)])))我们在这里使用了一些新的过程：

+   输出缓冲区（与对等体通信的输出通道）通常由字节填充。每次我们想发送消息时，我们需要刷新（清空）此缓冲区，以避免重新发送先前的消息。我们使用`flush-output`来实现这一点。

+   `read-line`类似于`read`，但是一旦读取到换行符就会停止读取。

+   `string-prefix?`用于检查字符串是否以另一个字符串开头。

+   fprintf 类似于 printf，只是我们还可以提供第一个参数来指定消息应该发送到哪里。

+   set->list 将一个集合转换为一个列表。

在 latest-blockchain 情况中涉及到一个小技巧 —— 我们使用了 write 而不是 (fprintf out "latest-blockchain:∼a\n")。其原因是 print（以及 printf 和 fprintf）不能保证以特定方式格式化输出。例如，print 打印带有引号的字符串（以使打印的数据对用户更易读），当我们尝试对接收到的数据进行反序列化时，这会混乱，因此我们希望以“原始”格式发送数据。

下一步是在区块链有效且具有更高工作量的情况下，实现更新区块链和有效对等方列表的程序。 1 (**定义** (maybe-update-blockchain peer-context line) 2 (**让** ([latest-blockchain 3 (trim-helper line #rx"(latest-blockchain:|[\r\n]+)")] 4 [current-blockchain 5 (peer-context-data-blockchain peer-context)]) 6 (**当** (**和** (valid-blockchain? latest-blockchain) 7 (> (get-blockchain-effort latest-blockchain) 8 (get-blockchain-effort current-blockchain))) 9 (printf "已更新对等方 ~a 的区块链\n" 10 (peer-context-data-name peer-context)) 11 (set-peer-context-data-blockchain! peer-context 12 latest-blockchain))))

我们首次使用了 #rx"..."，这指定了一个正则表达式。将其视为在某个字符串中定义搜索模式的一种方式。

例如，#rx"(latest-blockchain:|[\r\n]+)" 匹配以下字符串：

+   latest-blockchain:a\n

+   latest-blockchain:b\n

+   一般来说，latest-blockchain:...\n

上述过程仅在区块链有效且努力大于当前区块链时才会更新区块链。我们将努力定义为所有区块的 nonce 之和：1   (**define** (get-blockchain-effort b)2     (foldl + 0 (map block-nonce (blockchain-blocks b))))更新有效同行列表是将当前有效同行列表与新接收的列表合并，从而改变同行上下文结构：1   (**define** (maybe-update-valid-peers peer-context line)2     (**let** ([valid-peers (list->set3                         (trim-helper line #rx"(valid-peers:|[\r\n]+)"))]4           [current-valid-peers (peer-context-data-valid-peers5                                 peer-context)])6       (set-peer-context-data-valid-peers!7        peer-context8        (set-union current-valid-peers valid-peers))))我们还使用了这个过程，这只是一个辅助过程，它将从字符串中删除命令（前缀），使我们能够专注于输入。例如，当我们接收到 valid-peers:X 时，它将删除 valid-peers:，使我们可以轻松检索 X。1   (**define** (trim-helper line x)2     (deserialize3      (read4       (open-input-string5        (string-replace line x "")))))

这结束了处理程序的实现。现在有一个流程可供同行使用，接受命令并更新同行和区块链的列表。在下一节中，我们将实现同行之间的通信——他们应该使用我们实现的这些命令相互通信。

#### 4.2.1.3 服务器实现

当一个同行连接到另一个同行（服务器）时，应该发生以下情况：

1.  1.

    服务器应该等待传入的同行发送一些命令。

1.  2.

    服务器应该使用处理程序来处理必要的数据。

1.  3.

    服务器应该将转换后的数据发送回传入的同行。

然而，如果多个对等体连接，则该过程将“阻塞”，即第二个对等体必须等待第一个被服务，第三个必须等待第二个，依此类推。

为了解决这个问题，我们转向线程。accept-and-handle 是主要的过程，用于为传入的对等体提供服务。该过程接受一个连接（监听器对象）和一个对等体上下文，并为每个传入连接启动一个处理程序线程：1   (**define** (accept-and-handle listener peer-context)2     (**define-values** (in out) (tcp-accept listener))3     (thread4      (**lambda** ()5        (handler peer-context in out)6        (close-input-port in)7        (close-output-port out))))

我们使用了一个名为 tcp-accept 的新过程，它接受一个连接并返回输入（用于读取数据）和输出端口（用于发送数据）。使用 define-values 语法，我们存储了这两个值。

peers/serve 是主服务器监听器。这直接从 Racket 文档中复制粘贴过来的，并且对于好奇的读者可以导航到文档并阅读更多关于实现细节的内容。简而言之，*custodian* 是一种容器，确保内存中没有虚假的线程或输入/输出端口，并且为我们处理这些。1   (**define** (peers/serve peer-context) 2     (**define** main-cust (make-custodian)) 3     (**parameterize** ([current-custodian main-cust]) 4       (**define** listener 5         (tcp-listen (peer-context-data-port peer-context) 5 #t)) 6       (**define** (loop) 7         (accept-and-handle listener peer-context) 8         (loop)) 9       (thread loop))10     (**lambda** ()11       (custodian-shutdown-all main-cust)))

tcp-listen 过程持续监听特定端口，以获取新的传入连接。

#### 4.2.1.4 客户端实现

接下来，我们将实现`connect-and-handle`——一种尝试连接其他对等节点的过程，而之前我们构建的是一个用于服务传入对等节点的过程。这个过程类似于`accept-and-handle`，但有些双重，因为它不接受新的连接。相反，它试图建立新的连接： 1   (**define** (connect-and-handle peer-context peer) 2     (**begin** 3       (**define-values** (in out) 4         (tcp-connect (peer-info-ip peer) 5                      (peer-info-port peer))) 6 7       (**define** current-peer-io (peer-info-io peer in out)) 8 9       (set-peer-context-data-connected-peers!10        peer-context11        (cons current-peer-io12              (peer-context-data-connected-peers peer-context)))1314        (thread15         (**lambda** ()16           (handler peer-context in out)17           (close-input-port in)18           (close-output-port out)1920           (set-peer-context-data-connected-peers!21            peer-context22            (set-remove23             (peer-context-data-connected-peers peer-context)24             current-peer-io))))))这个过程相当长，因此值得拆分一下：

1.  1.

    `tcp-connect`过程试图连接到特定的 IP 地址和端口（我们从`peer-info`结构中提取的值）。

1.  2.

    当连接成功时，`tcp-connect`将返回输入和输出端口，我们可以分别用于读取数据和写入数据。

1.  3.

    接下来，当前上下文的已连接对等节点的具体列表将被更新。

1.  4.

    最后，我们启动一个线程，使用`handler`来处理通信。当连接结束时，我们进行清理，并从对等节点列表中移除对等节点。

下一步是确保我们与所有已知的对等体连接。我们再次使用线程，出于与服务器相同的原因——我们不希望此过程阻止程序在尝试连接一个客户端时连接到其他客户端。此过程对等于 peers/serve，而 tcp-connect 对等于 tcp-accept。我们使用 sleep 在再次处理之前等待几秒钟，以使该过程更具性能。 1   (**定义** (peers/connect peer-context) 2     (**定义** main-cust (make-custodian)) 3     (**参数化** ([current-custodian main-cust]) 4       (**定义** (loop) 5         (**让** ([potential-peers (get-potential-peers peer-context)]) 6           (**对于** ([peer potential-peers]) 7             (**处理程序** ([exn:fail? (**lambda** (x) #t)]) 8               (connect-and-handle peer-context peer)))) 9         (sleep 10)10         (loop))11       (线程 loop))12     (**lambda** ()13       (custodian-shutdown-all main-cust)))要实现 get-potential-peers，我们首先从对等上下文获取已连接和有效对等体的列表。不在已连接对等体列表中的有效对等体是我们可以建立新连接的潜在对等体。1   (**定义** (get-potential-peers peer-context)2     (**让** ([current-connected-peers3            (list->set4             (map peer-info-io-peer-info5                  (peer-context-data-connected-peers peer-context)))]6           [valid-peers (peer-context-data-valid-peers peer-context)])7       (set-subtract valid-peers current-connected-peers)))

#### 4.2.1.5 零件的集成

下一个过程将 ping 所有的对等节点（连接到我们或我们连接到的对等节点）以尝试同步区块链数据并更新其他内容，比如有效对等节点列表： 1   (**define** (peers/sync-data peer-context) 2     (**define** (loop) 3       (sleep 10) 4       (**for** [(p (peer-context-data-connected-peers peer-context))] 5         (**let** ([in (peer-info-io-input-port p)] 6               [out (peer-info-io-output-port p)]) 7           (fprintf out "get-latest-blockchain\nget-valid-peers\n") 8           (flush-output out))) 9       (printf "Peer ~a reports ~a valid and ~a connected peers.\n"10               (peer-context-data-name peer-context)11               (set-count12                (peer-context-data-valid-peers peer-context))13               (set-count14                (peer-context-data-connected-peers peer-context)))15       (loop))16     (**define** t (thread loop))17     (**lambda** ()18       (kill-thread t)))最后，我们导出必要的对象：1   (**provide** (**struct-out** peer-context-data)2             (**struct-out** peer-info)3             run-peer)

### 4.2.2 更新现有代码

我们需要修改 main-helper.rkt，以包括点对点实现：1   ; ...2   (**require** "peer-to-peer.rkt")3   ; ...45   (**provide** (**all-from-out** "blockchain.rkt")6             (**all-from-out** "utils.rkt")7             (**all-from-out** "peer-to-peer.rkt")8             format-transaction print-block print-blockchain print-wallets)

### 4.2.3 main-p2p.rkt 文件

这是我们将所有组件放在一起并使用它们的地方。我们希望这个实现能够接受一些输入参数，比如区块链数据库文件和每个对等节点的 IP 和端口地址。

一旦我们创建了一个可执行文件，我们可以通过使用*命令行参数*的方式向其传递输入。例如，如果我们的可执行文件名为 blockchain，我们可以通过运行./blockchain <param1> <param2> <...> 来向其传递附加数据。Racket 提供了一个名为 current-command-line-arguments 的内置过程，它将这些参数读入一个向量（类似于列表），然后我们使用 vector->list 将其转换为一个列表以进行进一步处理。1   (**require** "main-helper.rkt")23   (**define** args (vector->list  (current-command-line-arguments)))45   (**when** (not (= 3 (length args)))6     (begin7       (printf "Usage: main-p2p.rkt db.data port ip1:port1,ip2:port2...")8       (newline)9       (exit)))string-to-peer-info 是一个辅助过程，用于对对等体信息进行进一步解析：1   (**define** (string-to-peer-info s)2     (**let** ([s (string-split s ":")])3       (peer-info (car s) (string->number (cadr s)))))我们继续通过解析参数进行下一步操作：1   (**define** db-filename (car args))2   (**define** port (string->number (cadr args)))3   (**define** valid-peers4     (map string-to-peer-info (string-split (caddr args) ",")))接着我们检查数据库文件是否存在，使用 file-exists?。如果该文件存在，它将包含来自先前区块链的内容。如果文件不存在，我们将继续创建一个。1   (**define** db-blockchain2     (**if** (file-exists? db-filename)3         (file->struct db-filename)4         (initialize-new-blockchain)))我们提供了创建新区块链的功能： 1   (**define** wallet-a (make-wallet)) 2 3   (**define** (initialize-new-blockchain) 4     (**begin** 5       (**define** coin-base (make-wallet)) 6 7       (printf "Making genesis transaction...\n") 8       (**define** genesis-t (make-transaction coin-base wallet-a 100 '())) 910       (**define** utxo (list11                      (make-transaction-io 100 wallet-a)))1213       (printf "Mining genesis block...\n")14       (**define** b (init-blockchain genesis-t "1337cafe" utxo))15       b))接下来是初始化当前对等体的代码——它被命名为 Test peer，并包含来自解析的命令行参数的数据（端口、有效对等体等）。1   (**define** peer-context2     (peer-context-data "Test peer"3                        port4                        (list->set valid-peers)5                        '()6                        db-blockchain))7   (**define** (get-blockchain) (peer-context-data-blockchain peer-context))89   (run-peer peer-context)我们持续导出数据库以便在用户退出应用程序时获取最新信息。1   (**define** (export-loop)2     (**begin**3       (sleep 10)4       (struct->file (get-blockchain) db-filename)5       (printf "Exported blockchain to '~a'...\n" db-filename)6       (export-loop)))78   (thread export-loop)最后，我们创建一个过程来持续挖掘空块。请注意，对等体间的实现以线程模式运行，因此如果我们持续运行此过程，将不会出现阻塞。 1   (**define** (mine-loop) 2     (**let** ([newer-blockchain 3            (send-money-blockchain (get-blockchain) 4                                   wallet-a 5                                   wallet-a 6                                   1 7                                   (file->contract "contract.script"))]) 8       (set-peer-context-data-blockchain! peer-context newer-blockchain

我们可以通过创建一个可执行文件并与朋友分享来继续进行。如果我们知道他们的 IP 地址（或者他们知道我们的 IP 地址），我们可以建立连接，从而形成一个系统。

## 4.3 总结

恭喜！作为本章的一部分，我们向区块链实现添加了两个重要的新功能：智能合约和点对点支持。这标志着本书对区块链的实现工作的结束。
