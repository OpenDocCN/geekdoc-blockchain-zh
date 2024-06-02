© 作者，独家许可给 APress Media, LLC，Springer Nature 的一部分，2021 年 B. Sitnikovski 通过 [`doi.org/10.1007/978-1-4842-6969-5_2`](https://doi.org/10.1007/978-1-4842-6969-5_2) 发布

# 2. Racket 编程语言

Boro Sitnikovski^(1  )(1)斯科普里，北马其顿![../images/510363_1_En_2_Chapter/510363_1_En_2_Figa_HTML.jpg](img/510363_1_En_2_Figa_HTML.jpg)

*Structure, by D. Bozhinovski*

现在我们已经模糊地解释了什么是区块链以及它如何有用，下一个显而易见的步骤是在计算机中实现这些计算，以便它们自动执行。在本章中，我们介绍一个工具，它将允许我们精确地实现这些计算。

## 2.1 Lisp 简介

Lisp，起源于 1958 年，代表*列表处理*，是一系列编程语言。与标准编程语言不同，它具有完全带括号的前缀表示法。例如，不是写 1 + 2，而是写成 (+ 1 2)。

在 Lisp 家族中有许多 Lisp 实现。其中一种实现是 Racket，我们将在本书中使用它，因为这种实现对入门级程序员来说特别容易。该语言在许多情况下都被使用，如研究、计算机科学教育和通用编程。它还被用于商业项目。一个值得注意的例子是运行在 Arc 上的 Hacker News^(1) 网站，Arc 是在 Racket 中开发的编程语言。

Lisp 实现以其极简主义而著称。由于这种极简主义，用 Lisp 构建区块链（或其他任何东西）将意味着你可以轻松地在大多数其他编程语言中完成相同的任务。Lisp 偏爱函数组合——将两个函数链接在一起——例如，给定 *f*(*x*) 和 *g*(*x*)，一个组合是 *f*(*g*(*x*))。在本书的后面，我们将看到组合提供的有趣特性以及我们如何轻松地维护和扩展我们的代码。

### 2.1.1 数据结构和递归

在 Lisp 中有三个重要概念：

+   *基元*或公理（起始点或构建块）。例如，数字 1、2 等等，我们不必自己实现，因为它们已经包含在编程语言中。另一个例子是对数字的操作，例如+和*。

+   *组合*或将基本元素组合起来进行复杂计算的方法。例如，我们可以将 + 和 * 结合起来如下：1 + (2 * 3) 或以前缀（Lisp）表示法：(+ 1 (* 2 3))。

+   *抽象*或捕捉基本元素的组合。例如，如果我们发现自己一遍又一遍地进行计算，最好将其捕捉（抽象或封装）到一个可以轻松重用的函数中。

我们将在整本书中反复依赖这些概念，因为它们允许我们构建复杂的结构。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figb_HTML.gif](img/510363_1_En_2_Figb_HTML.gif) 定义 2-1

**数据结构**是一组值，它们之间的关系以及可以应用于这些值的函数或操作的集合。

数据结构的一个例子是数字与加法和乘法函数的组合。

从上一章的动机中我们可以看到形成这样一个数据结构的需要，例如，一个块是一个包含哈希、所有者和交易金额的结构。

有许多数据结构。一个有序列表就是一个例子，按照顺序表示数字（1，2，3）。此外，还有列表的操作，如计算元素的数量，合并两个列表等等。

在上一个列表示例中，我们使用了数字 1、2 和 3—这些元素是*原语*。列表与其操作一起代表了一种*抽象*。将几个列表操作链接在一起代表了一种*组合*。

现在我们可以转换一些数据结构（通过对其应用操作），那么能够反复根据一些特定规则转换数据结构就很好了。例如，如果我们有一个区块链数据结构，我们可能希望想出一种方法来转换它，比如说，插入一个新区块。这可能需要多次应用相同的操作。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figc_HTML.gif](img/510363_1_En_2_Figc_HTML.gif) 定义 2-2

在数学和计算机科学中，当函数能够由以下两个特性定义时，它们会展示出**递归**行为：

1.  1.

    一个简单的基本情况（或几个基本情况）—返回一个值而不使用递归的终止情况

1.  2.

    一条规则（或几条规则）向基本情况减少

最常见的递归函数例子是阶乘函数，定义如下：![$$ fact(n)=\left\{\begin{array}{l}1,\mathrm{if}\ n=0\\ {}n\cdot fact\left(n-1\right),\mathrm{otherwise}\end{array}\right. $$](img/510363_1_En_2_Chapter_TeX_Equa.png)

例如，使用替换我们可以看到*fact*(3)的求值为 3 ⋅ *fact*(2)，这是 3 ⋅ 2 ⋅ *fact*(1)，最终是 3 ⋅ 2 ⋅ 1 ⋅ *fact*(0)，这就是 6。

我们刚刚讨论的递归是多次应用相同的操作，并为下一个定义提供了动机。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figd_HTML.gif](img/510363_1_En_2_Figd_HTML.gif) 定义 2-3

**树** 是一种层级递归的数据结构，可以有两种可能的值：

1.  1.

    一个空值

1.  2.

    一个单一的值，与另外两个子树配对

家谱是树的一个例子。树的另一个例子是二叉树，其中左子树的值小于当前值，右子树的值大于当前值：1     22    / \3   1   3

在 Lisp 中，树是重要的，因为它们被用来表示程序的结构。我们将在下一节中更详细地讨论这个问题。

### 2.1.2 语言和语法

在本节中，我们快速了解 Lisp 的基础知识，这将为 Lisp 背后的思想提供一个高层次的概述。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Fige_HTML.gif](img/510363_1_En_2_Fige_HTML.gif) 定义 2-4

一种 **语言** 由以下组成：

1.  1.

    符号，可以组合成句子

1.  2.

    语法，它是一组规则，告诉我们哪些句子是良构的

这种语言的定义也反映在编程语言中，它们有一个特殊的语法叫做语法。例如，C 编程语言有一个特殊的语法—在编写程序语句时必须遵循特定的规则。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figf_HTML.gif](img/510363_1_En_2_Figf_HTML.gif) 定义 2-5

**抽象语法树** 是编程语言中源代码的抽象语法结构的树表示。

当你用编程语言写程序时，有一个中间步骤会解析程序的源代码，并生成一个抽象语法树。![../images/510363_1_En_2_Chapter/510363_1_En_2_Fig1_HTML.jpg](img/510363_1_En_2_Fig1_HTML.jpg)

图 2-1

例 1：抽象语法树

例如，图 2-1 中的图像代表以下伪代码的抽象语法树：1   **while** (a > b) {2       a = a - 1;3       b = b * 2;4   }另一个例子，图 2-2 中的图像代表以下伪代码：1   **if** (a == b && b == c) {2       a = a - 1;3       b = b * 2;4   } **else** a = a * b * 2;重要的不是理解这些代码的功能，而是理解编程语言内部如何表示这样的程序。![../images/510363_1_En_2_Chapter/510363_1_En_2_Fig2_HTML.jpg](img/510363_1_En_2_Fig2_HTML.jpg)

图 2-2

例 2：抽象语法树

Lisp 没有像 C 一样的特殊语法限制，例如。我们将编写的代码将是实际的抽象语法树。这就是为什么 Lisp 依赖前缀表示法。我们看到 Lisp 基于一种简约的设计，因为我们不会受到许多其他语言的开销，这些语言具有特殊的语法，有时功能会重叠。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figg_HTML.gif](img/510363_1_En_2_Figg_HTML.gif) 定义 2-6

Lisp 中的语法元素是符号 **表达式** 或 S-表达式。S-表达式可以是以下之一：

1.  1.

    一个符号（一串字符）

1.  2.

    一个 S-表达式的良好形式列表（平衡的括号）

例如，hello 是一个有效的 S-表达式，(hello there) 也是。但 (hello( 不是一个有效的 S-表达式，因为括号不平衡。在构造 S-表达式时，空白很重要。请注意 h ello 与 hello 是不同的。

一个 S-表达式良好形式的条件是抽象语法树是平衡的。

与其他语言相比，在 Lisp 中，语法具有特殊的含义。由于宏是核心语言的一部分，可以扩展此语法。^(2) S-表达式形成 Lisp 的语法。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figh_HTML.gif](img/510363_1_En_2_Figh_HTML.gif) 练习 2-1

我们用加法函数处理数字作为数据结构。想想另一个数据结构。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figi_HTML.gif](img/510363_1_En_2_Figi_HTML.gif) 练习 2-2

在给定以下定义的情况下，求解 sum(3)，sum(5)和 sum(1)：

![$$ sum(n)=\left\{\begin{array}{l}0,\mathrm{if}\ n=0\\ {}n+ sum\left(n-1\right),\mathrm{otherwise}\end{array}\right. $$](img/510363_1_En_2_Chapter_TeX_IEq1.png)

sum(-1)是什么情况？

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figj_HTML.gif](img/510363_1_En_2_Figj_HTML.gif) 练习 2-3

以下哪个 S 表达式是有效的？

1.  hello

2.  123

3.  (hello 123)

4.  (hello (123)

5.  (+ 1 (* 2 3))

6.  (+ (* 3 2) (/ 6 2))

**提示**：为每个表达式绘制抽象语法树可能会更加明显，可以看出其中一个是有效的还是无效的。

## 2.2 配置和安装

Racket 可以通过[`download.racket-lang.org`](https://download.racket-lang.org/)下载和安装。Windows、Linux 和 Mac 都有可用的二进制文件。这本书是使用 Racket 版本 7 编写的，但可能也适用于其他版本。下载并安装完整包后，我们可以运行 DrRacket。如果你看到图 2-3 中显示的屏幕，恭喜！这意味着安装成功了。![../images/510363_1_En_2_Chapter/510363_1_En_2_Fig3_HTML.jpg](img/510363_1_En_2_Fig3_HTML.jpg)

图 2-3

DrRacket

屏幕的上部文本区域是定义区域，我们通常在这里编写定义。或者，下部是交互区域，在这里我们与定义进行交互。

帮助台位于顶部菜单下的帮助 > 帮助台，包含快速介绍、参考手册和示例等有用信息。

使用 Racket 的两种主要方法：

+   使用图形用户界面（GUI），这是推荐的方式，也是我们在整本书中使用的方式。

+   使用命令行实用工具（racket 是解释器/编译器，raco 是包管理器），这是给更高级用户使用的。

## 2.3 Racket 入门

初次接触 Lisp 的新手注意到 Lisp 程序中有太多括号。这是事实，但这是因为我们在一种没有特殊语法的语言中编写我们的抽象语法树所导致的直接后果。

在本书中我们将看到我们得到的表达力的力量。例如，一个优点是不需要特殊的运算顺序。在高中，我们必须记住*和/必须在+和-之前计算。但这在 Lisps 中并不适用，因为我们编写程序的方式使得计算顺序显而易见。

让我们考虑表达式 (+ 1 (* 2 3))。正如我们所提到的，空格是 S-表达式的重要部分，因此 (+1 (* 2 3)) 与 (+ 1 (* 2 3)) 是不同的。为了将其转换为我们心中更熟悉的表示法，我们可以交换运算符，使其以*中缀*表示而不是*前缀*：(+ 1 (* 2 3)) 等同于 (1 + (2 * 3))。现在我们看到这个表达式的值是 7。

接下来，让我们在 DrRacket 编辑器的交互区（底部文本区域）中写下这个表达式，然后按回车键（Enter）：1   > (+ 1 (* 2 3))2   7“>”符号表示后面跟着的命令必须输入到交互区域。![../images/510363_1_En_2_Chapter/510363_1_En_2_Fig4_HTML.jpg](img/510363_1_En_2_Fig4_HTML.jpg)

图 2-4

DrRacket 的第一个计算

我们得到 7 作为结果，如图 2-4 所示。我们在 Racket 中进行了第一次计算。

完成评估后，DrRacket 再次等待新命令。这是因为在交互区域，我们处于 REPL 模式，即读取-求值-打印-循环。也就是说，交互区域会读取我们写的内容，尝试评估它（得出结果），打印结果，然后循环回到读取状态。

Lisp 评估与数学中的替换非常相似。例如，一个表达式 (+ 1 (* 2 3)) 可以如下评估：

1.  1.

    (+ 1 (* 2 3))

1.  2.

    (+ 1 6)

1.  3.

    7

也就是说，在每个步骤中，我们将表达式简化，直到不再有进一步的简化为止。我们立即注意到替换作为一个概念是多么强大。

### 2.3.1 原始类型

在上述评估中，我们得到一个数字作为结果——值为 7 的类型是数字。虽然 Racket 中的值类型是隐式的，但我们仍然有一种方法来检查值的类型，我们稍后将在谓词的帮助下看到。

Racket 有一些原始（内置）类型，例如：

+   符号，如 hello、world

+   列表，如 (1, 2, 3)

+   函数，如 f(x) = x + 1

+   数字，如 1、2、3.14

+   布尔值，如 #t（表示真）和 #f（表示假）

+   字符或单个字母：#\A，#\B，#\C

+   字符串或字符列表："Hello"，"World"

+   字节：根据 ASCII 码，我们可以用数字表示字符（例如，72 代表 H）

+   字节，作为字节列表：#"Hello"，#"World"

1   > 123 2   123 3   > #t 4   #t 5   > #f 6   #f 7   > #\A 8   #\A 9   > "Hello  World"10   "Hello World"11   > (bytes 72 101 108 108 111)12   #"Hello"每次评估都附有特定类型的产生值：

1.  1.

    第一次评估（123）的类型是数字。

1.  2.

    第二次（#t）和第三次（#f）评估的类型是布尔值。

1.  3.

    第四次评估（#\A）的类型是字符。

1.  4.

    第五次评估（"Hello World"）的类型是字符串。

1.  5.

    第六个评估（（字节 72 101 108 108 111））具有字节类型，并使用 ASCII 表来表示字母。

我们在以下章节中介绍符号、列表和函数。

### 2.3.2 列表、评估和引用

为了生成有序列表（1、2、3），我们可以要求 DrRacket 在交互区域评估（list 1 2 3）：1   > (list 1 2 3)2   '(1 2 3)

list 是一个内置函数，就像 + 一样，我们已经使用过。list 接受任意数量的参数，并作为结果返回从它们生成的列表。返回的表达式 '(1 2 3) 只是一种花式表示法，等价于表达式 (quote (1 2 3))，在这里我们告诉 Racket 返回实际的列表 (1 2 3) 而不是评估它。

我们注意到括号是如何用来表示函数调用或评估的。一般来说，代码 (f a_1 a_2 ... a_n) 对 f 进行了函数调用，按顺序传递 n 个参数。例如，对于函数 f(x) = x + 1，一个例子评估是 f(1)，我们写成 (f 1)，作为返回值我们得到 2。

注意，(list 1 2 3) 作为结果返回了 '(1 2 3)。让我们试着理解这里发生了什么。如果 (list 1 2 3) 返回了 (1 2 3)，这并没有太多意义，因为（正如我们讨论过的）这种表示法会尝试调用（不存在的）函数 1，参数为 2 和 3。相反，它返回了一个 *引用* 列表：‘(1 2 3)。

为了理解这如何影响评估，让我们考虑一个例子，你对某人说了以下其中之一的陈述：

+   说出你的名字

+   说“你的名字”

在第一个例子中，你期望对方告诉你他们的名字。在第二个例子中，你期望他们说出“你的名字”，而不是他们的真实名字。

与这个例子类似，有一个内置的句法称为引用，我们可以在任何一组符号上使用它：1   > (**引用** 你好)2   '你好

这允许创建新的符号，对于宏的创建尤其重要。 有一个特殊的列表，称为 *空列表*，表示为 (list)，或 (quote ())，或简单地 '()。 当我们开始使用递归时，我们稍后将看到为什么这个列表很特别。

对于列表（或任何其他函数）的其他信息，您可以单击鼠标使用 F1 按钮点击单词。 这将打开 Racket 的手册屏幕，允许您选择要获取信息的函数。 通常，这是列表中的第一个匹配项。 单击它应该显示类似于图 2-5 的内容。![../images/510363_1_En_2_Chapter/510363_1_En_2_Fig5_HTML.jpg](img/510363_1_En_2_Fig5_HTML.jpg)

图 2-5

Racket 列表的手册

在 Racket 中，括号、方括号和大括号具有相同的效果。 因此，(list 1 2 3) 和 [list 1 2 3] 以及 {list 1 2 3} 是相同的。 在有很多括号时，这种视觉区别可能有用于分组评估。

回想一下 S 表达式可以是符号或列表。 由于我们在本节中讨论了评估、列表和符号，在本书的这一部分，我们已经涵盖了 Lisp 核心的内容。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figk_HTML.gif](img/510363_1_En_2_Figk_HTML.gif) 练习 2-4

在 Racket 中创建一个包含不同类型（数字、字符串）混合的列表。 列表应至少包含两个元素。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figl_HTML.gif](img/510363_1_En_2_Figl_HTML.gif) 练习 2-5

注意列表是一个函数，引用是一种语法。 使用 F1 键阅读手册了解两者。

### 2.3.3 点对

另一个内置函数是 cons，它代表 *构造*。这个函数只接受两个参数，因此它返回一个 (引用的) 对：1   > (cons 1 2)2   '(1 . 2)将 '(1 . 2) 理解为两个数字的序列：1 和 2。![../images/510363_1_En_2_Chapter/510363_1_En_2_Fig6_HTML.jpg](img/510363_1_En_2_Fig6_HTML.jpg)

图 2-6

(cons 'some-value 'nil) 对

还有两个内置函数，称为 car 和 cdr，分别用于检索对的第一个和第二个元素：1   > (car (cons 1 2))2   13   > (cdr (cons 1 2))4   25   > (car '(1 . 2))6   17   > (cdr '(1 . 2))8   2

注意我们在这里如何使用函数组合，即我们在第一个示例中“组合”了 car 和 cons，在第二个示例中“组合”了 cdr 和 cons。

对偶很重要，我们可以用它们编码任何数据结构。事实上，列表是一种特殊类型的对，其中 (list 1 2 3) 等同于 (cons 1 (cons 2 (cons 3 '())))。参见图 2-7。![../images/510363_1_En_2_Chapter/510363_1_En_2_Fig7_HTML.jpg](img/510363_1_En_2_Fig7_HTML.jpg)

图 2-7

一个列表的示例

使用列表的动机是它将允许我们，例如，将几个块链接在一起以形成区块链。

Racket 还支持集合。在列表/对中可能存在重复的元素，但在集合中所有元素都是唯一的。此外，我们可以在集合上使用操作，例如并集（合并两个集合），减法（删除在集合 2 中找到的集合 1 中的元素）等。

例如，考虑以下代码，其中使用了内置函数 list->set、set-union 和 set-subtract：1   > (list->set '(1 2 3 4 4))2   (set 1 3 2 4)3   > '(1 2 3 4 4)4   '(1 2 3 4 4)5   > (set-union (list->set '(1 2 3)) (list->set '(3 4 5)))6   (set 1 5 3 2 4)7   > (set-subtract (list->set '(1 2 3)) (list->set '(3 4 5)))8   (set 1 2)

我们注意到在 Lisp 中，仅依赖于几个原始概念（函数调用、对、和引用），我们就可以捕捉抽象。我们将在第 2.3.13 节中更多地讨论这个问题。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figm_HTML.gif](img/510363_1_En_2_Figm_HTML.gif) 练习 2-6

用 cons 表示您在练习 2-4 中创建的相同列表。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Fign_HTML.gif](img/510363_1_En_2_Fign_HTML.gif) 练习 2-7

使用 car 和 cdr 的组合获取练习 2-6 中列表中的第二个元素。

### 2.3.4 添加定义

到目前为止，我们只在 DrRacket 的交互区域中工作过。让我们尝试在定义区域中做一些有用的事情。![../images/510363_1_En_2_Chapter/510363_1_En_2_Fig8_HTML.jpg](img/510363_1_En_2_Fig8_HTML.jpg)

图 2-8

在 DrRacket 中添加定义

我们可以在图 2-8 的截图中注意到几件事：

+   在定义区域中，我们添加了一些代码。我们注意到我们使用了另一个名为 define 的内置语法，将一个值（123）附加到一个符号/变量（a-number）上。

+   在交互区域中，我们与已在定义区域中定义的内容进行了交互。在这种情况下，交互是仅通过引用其符号来显示定义的值。

在本书中，每个 Racket 程序都将以 #lang racket 开始。这意味着我们将处理 Racket 的普通语法。这可以接受不同的值；例如，我们可以使用专门用于绘制图形的语言，但这超出了本书的范围。

我们在定义区域中写的所有内容也可以在交互区域中写，反之亦然。要使定义在交互区域中可用，我们需要通过选择 Racket > Run 从顶部菜单运行程序。请注意，当我们运行程序时，交互区域会被清除。

如果我们的定义引用了其他定义，我们可以使用鼠标悬停在符号名称上，DrRacket 将绘制一条指向该引用定义的线条（图 2-9）。对于大型复杂的程序，这对于揭示函数的细节将非常有用。![../images/510363_1_En_2_Chapter/510363_1_En_2_Fig9_HTML.jpg](img/510363_1_En_2_Fig9_HTML.jpg)

图 2-9

在 DrRacket 中跟踪引用

通过选择顶部菜单中的 File > Save Definitions 可将定义保存到文件中以供以后使用。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figo_HTML.gif](img/510363_1_En_2_Figo_HTML.gif) 练习 2-8

将练习 2-7 中的列表存储在定义区域中，然后在交互区域使用 car 和 cdr 对该列表进行操作。

### 2.3.5 过程与函数

在 Lisp 中，过程本质上是一个数学函数。调用时，它返回一些数据。然而，与数学函数不同，一些 Lisp 表达式和过程具有副作用。

例如，考虑两个函数：add-1 将数字增加一，get-current-weather 从外部服务获取当前天气。第一个函数在任何时间点都将返回相同的值，而第二个“函数”在不同时间点可能返回不同的值。

因此，在实践中，Lisp 过程并不总是在数学“纯”意义上的函数，但通常会被称为“函数”（即使可能具有副作用），以强调总是返回计算结果。

鉴于前段的推理，从这一点开始，我们将避免使用“函数”一词，而坚持使用“过程”。

有一个特殊的内置语法叫做 lambda ，它接受两个参数并产生一个过程作为结果。第一个参数是过程将接受的参数列表，第二个参数是一个表达式（主体），它作用于列表中的参数。

例如，(lambda (x) (+ x 1)) 返回一个过程，它接受一个单一参数 x，当这个过程被调用时，它会将这个参数的值增加一：(+ x 1)。

求值这个表达式给了我们：1   > (**lambda** (x) (+ x 1))2   #<procedure>为了调用这个过程，我们可以尝试传递一个参数：1   > ((**lambda** (x) (+ x 1)) 1)2   2 当然，用这种方式编写和评估过程是困难的。相反，我们可以在定义区域定义过程，然后在交互区域与之交互：1   (**define** add-one (**lambda** (x) (+ x 1)))交互：1   > (add-one 1)2   23   > (add-one 2)4   35   > (add-one (add-one 1))6   3 为了使事情变得稍微简单些，Racket 有一种特殊的语法来定义过程，所以这两者是等价的：(define add-one (lambda (x) (+ x 1))) <=> (define (add-one x) (+ x 1))过程也可以接受多个参数：(define add (lambda (x y) (+ x y))) <=> (define (add x y) (+ x y))![../images/510363_1_En_2_Chapter/510363_1_En_2_Figp_HTML.gif](img/510363_1_En_2_Figp_HTML.gif) 练习 2-9

在练习 2-7 中，您使用 (car (cdr l)) 从列表中检索了第二个元素。定义一个接受列表并返回该列表中第二个元素的过程。

### 2.3.6 条件过程

存在一些有用的内置过程，比如检查一个值是否为数字，一个数字是否大于另一个数字等等。 1   > (number? 1) 2   #t 3   > (number? "hello") 4   #f 5   > (character? #\A) 6   #t 7   > (string? "hello") 8   #t 9   > (byte? 72)10   #t11   > (bytes? #"Hello")12   #t13   > (procedure? add-one)14   #t15   > (symbol? (quote hey))16   #t17   > (symbol? 1)18   #f19   > (> 1 2)20   #f21   > (= 1 2)22   #f23   > (= 1 1)24   #tif 是一种内置语法，允许根据某个断言的*真值*来评估表达式。它接受三个参数：

+   用于检查的条件

+   如果条件为真，则评估的表达式

+   如果条件为假，则评估的表达式

这是示例用法：1   > (**if** (= 1 1) "It is true" "It is not true")2   "It is true"3   > (**if** (= 1 2) "It is true" "It is not true")4   "It is not true"if 的更一般语法是 cond：1   (**cond** (test-1 action-1)2         (test-2 action-2)3         ...4         (test-n action-n))

可选地，最后一个测试可以是 else，以在没有任何条件匹配时使用特定的动作。

例如，这是一种在定义中使用 cond 的方式：1   (**define** (is-large x)2     (**cond** ((> x 10) #t)3           (**else** #f)))与之交互：1   > (is-large 5)2   #f3   > (is-large 10)4   #f5   > (is-large 11)6   #t 正如我们所见，= 是一个等号谓词，用于检查两个数字是否相等。然而，它只适用于数字，如果我们将其用于其他任何东西，它将引发错误：1   > (= 1 2)2   #f3   > (= 3.14 3.14)4   #t5   > (= '() '())6   =: **contract** violation 还有其他三个重要的等价谓词：

+   eq? 检查两个参数是否指向内存中的同一对象。

+   eqv? 与 eq? 相同，只是它还可以用于原始类型（例如数字、字符串）。

+   equal? 与 eqv? 相同，只是它还可以用于检查参数是否具有相同的递归结构（例如列表）。

请注意，内存中只有一个空列表 '()，^(3) 因此当检查空列表时，所有三个谓词都将返回相同的值。

为了展示 eq? 失败的地方，我们将使用一个名为 integer->char 的内置过程，它将数字转换为字符，按 ASCII 表示。1   > (integer->char 65)2   #\A3   > (eq? '() '())4   #t5   > (eq? (integer->char 65) (integer->char 65))6   #f7   > (eq? '(1) '(1))8   #f

如预期，这将对空列表返回 true，但无法比较不引用相同内存位置的对象或实际上具有元素的列表。

请注意，在这种情况下 eqv? 的不同之处：1   > (eqv? '() '())2   #t3   > (eqv? (integer->char 65) (integer->char 65))4   #t5   > (eqv? '(1) '(1))6   #f 最后，equal? 将递归地比较结构，支持列表：1   > (equal? '() '())2   #t3   > (equal? (integer->char 65) (integer->char 65))4   #t5   > (equal? '(1) '(1))6   #t![../images/510363_1_En_2_Chapter/510363_1_En_2_Figq_HTML.gif](img/510363_1_En_2_Figq_HTML.gif) 练习 2-10

我们已经使用 cond 语法定义了 is-large。请使用 if 语法表示它。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figr_HTML.gif](img/510363_1_En_2_Figr_HTML.gif) 练习 2-11

使用 cond 来表示以下逻辑：如果值是字符串或数字，则返回'foo，否则返回'bar。

### 2.3.7 递归过程

过程就像数据结构一样（例如树）可以是递归的。我们已经看到了一个例子，阶乘过程就是一个例子，在其中调用自身进行计算或循环。

例如，这是我们如何在 Racket 中定义阶乘的方法：1   (**define** (fact n)2     (**if** (= n 0)3         14         (* n (fact (- n 1)))))调用它将产生以下结果：1   > (fact 3)2   63   > (fact 0)4   1 对于一个更高级的示例，我们将定义一个计算列表长度（元素数量）的过程：1   (**define** (list-length x)2     (**cond** ((eq? x '()) 0)3           (**else** (+ 1 (list-length (cdr x))))))我们定义了一个叫做 list-length 的过程，它接受一个参数 x，过程的主体具有条件 ：

1.  1.

    对于空列表，只需返回 0，因为空列表的长度为 0。

1.  2.

    否则，返回一个加一的值加上 (list-length (cdr x)) 的值。

使用几个值进行测试：1   > (list-length '(1 2 3))2   33   > (list-length '())4   05   > (list-length '(1))6   1 记住列表是用对来表示的：1   > (car '(1 2 3))2   13   > (cdr '(1 2 3))4   '(2 3)5   > (car (cdr '(1 2 3)))6   27   > (cdr (cdr '(1 2 3)))8   '(3)换句话说，列表的 cdr 将返回没有第一个元素的相同列表。 这是 Racket 如何计算 (list-length '(1 2 3)) 的方式：1   (list-length '(1 2 3))2   = (+ 1 (list-length '(2 3)))3   = (+ 1 (+ 1 (list-length '(3))))4   = (+ 1 (+ 1 (+ 1 (list-length '()))))5   = (+ 1 (+ 1 (+ 1 0)))6   = (+ 1 (+ 1 1))7   = (+ 1 2)8   = 3

我们刚刚看到了递归行为的一个例子，因为递归情况被减少到基本情况以获得结果。 通过这个例子，我们可以看到递归的强大之处，以及它如何允许我们以重复的方式处理值。

我们可以另一种方式编写 list-length：1   > (**define** (list-length-iter x n)2       (**cond** ((eq? x '()) n)3             (**else** (list-length-iter (cdr x) (+ n 1)))))4   > (list-length-iter '(1 2  3) 0)5   3 这是它的计算过程：1   (list-length-iter '(1 2 3) 0)2   = (list-length-iter '(2 3) 1)3   = (list-length-iter '(3) 2)4   = (list-length-iter  '() 3)5   = 3

这两种过程都是递归的，因为它们生成相同的结果。但是，评估的性质非常不同。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figs_HTML.gif](img/510363_1_En_2_Figs_HTML.gif) 定义 2-7

递归过程可以生成**迭代**或**递归**过程：

1.  1.

    递归过程是指当前计算状态不由参数捕获，因此它依赖于“延迟”的评估。

1.  2.

    迭代过程是指当前计算状态完全由其参数来捕获。

在前面的例子中，list-length 生成一个递归过程，因为它需要下降到基本情况，然后再建立起来执行被“延迟”的计算。相反，list-length-iter 生成一个迭代过程，因为结果被捕获在参数中。

这种区别很重要，因为评估的性质不同意味着一些事情。例如，迭代过程比递归过程评估更快。

相反，一些算法无法使用迭代过程编写，正如我们稍后将在左右折叠中看到的那样。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figt_HTML.gif](img/510363_1_En_2_Figt_HTML.gif) 练习 2-12

我们实现 fact 的方式代表了生成递归过程的递归过程。重新设计它，使其仍然是一个递归过程，并生成一个迭代过程。

### 2.3.8 返回过程的过程

我们可以构建返回其他过程作为结果的过程。例如：1   > (**define** (f x) (**lambda** (y) (+ x y)))2   > f3   #<procedure:f>4   > (f 1)5   #<procedure>6   > ((f 1) 2)7   3

请注意第 3 行的新语法。它说明了前一行表达式的返回值是一个名为 f 的过程。然而，在第 4 行，当我们执行 (f 1) 时，我们得到了一个无名过程。这是因为 lambda 是没有名称的匿名函数。

这个概念非常强大，以至于我们可以实现自己的 cons、car 和 cdr：1   (**define** (my-cons x y) (**lambda** (z) (**if** (= z 1) x y)))2   (**define** (my-car z) (z 1))3   (**define** (my-cdr z) (z 2))求值：1   > (my-cons 1 2)2   #<procedure>3   > (my-car (my-cons 1 2))4   15   > (my-cdr (my-cons 1 2))6   2

请注意我们如何定义 my-cons 以返回另一个接受参数 z 的过程，然后根据该参数的值返回第一个或第二个元素。

使用替换方法，(my-cons 1 2) 求值为 (lambda (z) (if (= z 1 2))。因此，这个 lambda（过程）在某种意义上“捕获”数据。然后，当我们在这个过程上调用 my-car 或 my-cdr 时，我们只需传递 1 或 2 来分别获取第一个或第二个值。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figu_HTML.gif](img/510363_1_En_2_Figu_HTML.gif) 练习 2-13

实现一个过程，当它被求值时，它返回一个返回常数的过程。

**提示**：(lambda () 1) 是一个不接受参数并返回一个常数的过程。

### 2.3.9 通用高阶过程

通过上面的例子，我们已经看到了 Racket 如何将过程作为返回值（输出）返回。但是，它也可以接受过程作为参数（输入）。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figv_HTML.gif](img/510363_1_En_2_Figv_HTML.gif) 定义 2-8

**高阶过程**接受一个或多个过程作为参数或返回一个过程作为结果。

有三种常见的内置高阶过程：map、filter 和 fold。

对于本示例，我们将依赖于以下定义：1   (**定义** my-test-list '(1 2 3))2   (**定义** (add-one x) (+ x 1))3   (**定义** (gt-1 x) (> x 1))map 接受一个带有单个参数的过程和一个列表作为输入，并返回一个列表，其中列表的所有成员都应用了这个过程：1   > (map (**lambda** (x) (+ x 1)) my-test-list)2   '(2 3 4)3   > (map  add-one  my-test-list)4   '(2 3 4)如果我们对 (map add-one my-test-list) 进行替换，我们会得到 (list (add-one 1) (add-one 2) (add-one 3))。然而，最好是自己实现这些过程以了解它们的工作原理。map 接受一个转换过程 f，以及一个列表 l。我们有两种情况需要考虑：

+   对于空列表，我们只需返回空列表。

+   否则，我们提取第一个元素，应用转换过程，并通过递归映射其余元素来重构列表。

1   (**定义** (my-map f l)2     (**cond** ((eq? l '()) '())3           (**else** (cons (f (car l)) (my-map f (cdr l))))))另一个高阶过程 filter，接受一个带有单个参数的谓词和一个列表作为输入，并且它仅返回那些谓词求值为 true 的列表成员：1   > (filter gt-1 my-test-list)2   '(2 3)要重新实现 filter，注意它接受一个谓词 p，以及一个列表 l。有三种情况：

+   对于空列表，与之前一样，我们只需返回空列表。

+   否则，如果谓词匹配当前元素，则将其包含在新列表的生成中，递归地过滤其余元素。

+   否则，我们递归地过滤其余元素，跳过将当前元素添加到列表中。

1   (**define** (my-filter p l)2     (**cond** ((eq? l '()) '())3           ((p (car l)) (cons (car l) (my-filter p (cdr l))))4           (**else** (my-filter p (cdr l)))))最后，fold 接受一个接受两个参数（当前值和累加器）、一个初始值和一个列表的组合过程作为输入。然后，fold 返回与此过程组合的值。有两种类型的折叠，右折叠和左折叠，它们分别从右和左组合：1   > (foldr cons '() '(1 2 3))2   '(1 2 3)3   > (foldl cons '() '(1 2 3))4   '(3 2 1)foldr 接受一个组合操作符（过程）op，以及一个初始值 i 和一个列表 l。我们需要覆盖的两种情况如下：

+   对于空列表，我们返回初始值。

+   否则，我们使用组合操作符应用于列表的折叠余数的当前元素。

1   (**define** (my-foldr op i l)2     (**cond** ((eq? '() l) i)3           (**else** (op (car l)4                     (my-foldr op i (cdr l))))))foldl 有点不同。我们首先定义一个具有两种情况的过程：

+   对于空列表，我们返回初始值。

+   否则，我们再次调用折叠函数，将初始值更改为与当前元素和列表的剩余部分结合。

1   (**define** (my-foldl op i l)2     (**cond** ((eq? '() l) i)3           (**else** (my-foldl op (op (car l) i) (cdr l)))))这个过程的工作方式与 foldr 类似，只是结果被捕获在过程的参数中。例如，这是它对（my-foldl + 0 '(1 2 3)）展开的方式：1   (my-foldl + 0 '(1 2 3))2   = (my-foldl + 1 '(2 3))3   = (my-foldl + 3 '(3))4   = (my-foldl + 6 '())5   = 6

注意，右折叠展示了一个递归过程（想想我的长度），而左折叠展示了一个迭代过程（想想我的长度-迭代）。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figw_HTML.gif](img/510363_1_En_2_Figw_HTML.gif) 练习 2-14

实现一个过程，使其调用在参数中传递的过程。

**提示**：(... (lambda () 1)) 应返回 1。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figx_HTML.gif](img/510363_1_En_2_Figx_HTML.gif) 练习 2-15

使用 DrRacket 的功能跟踪`my-map`、`my-filter`、`my-foldr`和`my-foldl`上的定义，以更好地了解它们的工作原理。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figy_HTML.gif](img/510363_1_En_2_Figy_HTML.gif) 练习 2-16

选择一些运算符和谓词，然后使用`my-map`、`my-filter`、`my-foldr`和`my-foldl`在列表上对它们进行操作，看看它们会评估为何值。

### 2.3.10 包

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figz_HTML.gif](img/510363_1_En_2_Figz_HTML.gif) 定义 2-9

Racket 中的**包**类似于某人为他人编写的一组定义，供他人使用。

例如，如果我们想要使用散列过程，我们会选择一个实现这些过程的包并使用它们。这样可以使我们把重点放在系统设计上，而不是从零开始定义所有内容。

包可以在[`pkgs.racket-lang.org`](https://pkgs.racket-lang.org/)上浏览。它们可以从 DrRacket GUI 安装。当我们尝试使用一个包时，如果它在包存储库中可用，我们将会收到一个安装选项。或者，可以使用命令行从`raco pkg install <package_name>`安装包。我们稍后会利用包。

要从包中导出对象（变量、过程等），我们使用 provide 语法。例如，让我们创建一些过程，然后通过选择顶部菜单中的文件 > 保存定义将它们的定义保存在名为 utils.rkt 的文件中。1   (**define** (sum-list l) (foldl + 0 l))2   (**define** (add-one x) (+ x 1))34   (**provide** sum-list)我们将在与 utils.rkt 相同的文件夹中创建另一个名为 test.rkt 的文件。我们将使用 require 语法：1   (**require** "utils.rkt")23   (**define** (add-two x) (+ x 2))现在我们可以与 test.rkt 交互：1   > (sum-list '(1 2 3))2   63   > (add-two 1)4   35   > (add-one 1)6   add-one: undefined;

注意，add-one 是未定义的，因为只有我们在特殊语法中提供的过程（provide ...）才能被那些需要该包的内容使用。

### 2.3.11 作用域

一开始，让我们考虑以下定义：1   (**define** my-number 123)2   (**define** (add-to-my-number x) (+ my-number x))

我们创建了一个名为 my-number 的变量，并将数字 123 赋给它。我们还创建了一个名为 add-to-my-number 的过程，它会将一个数字（作为参数传递给它）加到 my-number 上。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figaa_HTML.gif](img/510363_1_En_2_Figaa_HTML.gif) 定义 2-10

**作用域** 指的是某些特定定义的可见性，或者是程序的哪些部分可以使用这些定义。

my-number 被定义在与 add-to-my-number 相同的“级别”上，因此它在 add-to-my-number 的作用域内。但是 add-to-my-number 中的 x 只能在过程定义的主体中访问，而不能被外部任何东西访问。

使用 let 语法，我们可以引入仅在某个部分可见的变量：1   (**let** ([var-1 value-1]2         [var-2 value-2])3   ... 我们的代码 ...)这会创建变量 var-1 和 var-2，它们仅在我们的代码部分可见。1   > (**let** ((x 1) (y 2)) (+ x y))2   33   > x4   . . x: undefined;5   > y6   . . y: undefined;letrec 语法与 let 非常相似，不过额外的是变量将在变量作用域中可见：1   > (**letrec** ((x 1) (y (+ x 1))) y)2   2![../images/510363_1_En_2_Chapter/510363_1_En_2_Figab_HTML.gif](img/510363_1_En_2_Figab_HTML.gif) 定义 2-11

**变量“屏蔽”** 是指在作用域内定义的变量与外部作用域中定义的变量同名时发生的情况。

例如，比较这两个评估的结果：1   > (**let** ((x 1)) x)2   13   > (**let** ((x 1)) (**let** ((x 2)) x))4   2

在第二个例子中，我们有一个 let 嵌套在另一个 let 中。内部 let 定义了一个 x，外部 let 也定义了一个 x。然而，内部 let 中的 x 将在内部 let 的主体中使用。

最后，让我们考虑另一个例子：1   (**定义** a-number 3)2   (**定义** (test-1 x) (+ a-number x))3   (**定义** (test-2 a-number) (+ a-number a-number))交互：1   > (test-1 4)2   73   > (test-2 4)4   8

test-1 使用全局范围的 a-number。test-2 使用变量屏蔽来定义 my-number，因此它等同于 (define (test-2 x) (+ x x))。

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figac_HTML.gif](img/510363_1_En_2_Figac_HTML.gif) 练习 2-17

使用 DrRacket 的功能可以跟踪 test-1 和 test-2 的定义。

### 2.3.12 Mutation

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figad_HTML.gif](img/510363_1_En_2_Figad_HTML.gif) 定义 2-12

**Mutation（变异）** 允许变量用不同的值重新定义。

可以使用 set! 语法来实现变异。考虑以下定义：1   (**define** x 123)2   x3   (**define** x 1234)4   x 这个定义将产生一个错误，指出模块：标识符在这里已经定义：x。然而，下一个定义：1   (**define** x 123)2   x3   (**set**! x 1234)4   x

将愉快地打印出 123 接着是 1234。

尽管变异看起来很强大，但良好的 Lisp 实践建议尽可能避免使用变异。这样做的原因是变异会引起副作用，而副作用会使得对程序进行推理变得更加困难。为了证明这个问题，考虑这个定义：1   (**define** some-number 123)23   (**define** (add-one)4     (+ 1 some-number))56   (**define** (add-one-mutation)7     (**begin**8       (**set!** some-number (+ 1 some-number))9       some-number))

begin 允许我们对多个表达式进行排序，按顺序执行它们。

现在让我们与它互动：1   > (add-one)2   1243   > (add-one)4   124 到目前为止一切顺利。没有副作用，因为每次调用 add-one 时它都返回相同的值。然而：1   > (add-one-mutation)2   1243   > (add-one-mutation)4   1255   > (add-one)6   126

这正是使得对程序进行推理变得困难的原因之一——当某些值被修改时，一些过程可能会对相同的输入返回不同的值。因此，在使用变异时必须小心。但是，我们将在后面的点对点实现中使用变异，这将使事情稍微简单一些。

### 2.3.13 结构

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figae_HTML.gif](img/510363_1_En_2_Figae_HTML.gif) 定义 2-13

**结构**是一种复合数据类型，它定义了一组变量的分组列表，以便将它们放在一个名称下。

在 Racket 中，特殊的语法结构 struct 允许我们捕获数据结构并提出一种新的抽象。在某种意义上，我们已经知道如何使用 car、cons 和 cdr 来捕获抽象。然而，struct 更加方便，因为它自动提供了构造数据类型和检索其值的程序。

考虑以下示例代码：1   (**struct** document (author title content))2   (**define** a-document3     (document4      "Boro Sitnikovski"5      "Introducing Blockchain with Lisp"6      "Hello  World"))从第 1 行的表达式中，我们自动得到以下程序：

+   document-author、document-title、document-content 从对象中提取值。

+   document 构造了一个这种类型的对象。

+   document?检查给定对象是否为此类型。

然后，使用第 3 行的 document，我们可以构造一个使用此数据结构的对象。

接下来，我们可以使用自动生成的程序从使用此数据结构的对象中提取值：1   > (document-author a-document) 2   "Boro Sitnikovski" 3   > (document-title a-document) 4   "Introducing Blockchain with Lisp" 5   > (document-content a-document) 6   "Hello World" 7   > (document? a-document) 8   #t 9   > (document? "test")10   #f 还有一种声明可变结构的方法如下：1   (**struct** document (author title content) **#:mutable**)

#:mutable 关键字将为结构中的每个属性自动生成 set-<field>!程序。

现在我们可以进行交互如下：1   > (document-author a-document)2   "Boro Sitnikovski"3   > (set-document-author! a-document "Boro")4   > (document-author  a-document)5   "Boro"![../images/510363_1_En_2_Chapter/510363_1_En_2_Figaf_HTML.gif](img/510363_1_En_2_Figaf_HTML.gif) 练习 2-18

创建一个包含名字、姓氏和年龄的人员结构。

### 2.3.14 线程

![../images/510363_1_En_2_Chapter/510363_1_En_2_Figag_HTML.gif](img/510363_1_En_2_Figag_HTML.gif) 定义 2-14

一个 **线程** 是一系列可以并行执行的指令。

Racket 有一个内置过程 `thread`，它接受一个过程，该过程将在并行执行而不阻塞下一条指令。

我们将展示一个演示线程的例子。我们将实现一个称为 `detailed-fact` 的过程，它类似于 `fact`，但还会打印当前正在处理的内容。`display` 是一个打印文本的过程，而 `displayln` 是相同的，但它还会打印一个换行符。

请注意我们使用了 `(thread (lambda () ...))` 而不是仅仅的 `(thread ...)`。正如我们所说，`thread` 需要一个过程，但在评估结束时，会得到某个数的阶乘的输出（例如 3），所以 `(thread 3)` 没有意义。

在这种并行执行中，输出不像前面的情况那样有序。这意味着 `thread` 内部的 lambda 正在并行执行，因此不能保证执行顺序。

我们将在后面的点对点实现中使用线程进行并行处理，其中我们将为每个对等体使用一个线程，以便在为一个对等体提供服务时不会阻塞其他对等体的服务。

## 2.4 创建一个可执行文件

创建可执行文件的想法是，您可以在其他计算机上运行它，而不需要安装 DrRacket，也不需要共享原始代码。在后面的章节中，我们将创建一个可执行文件，以便其他人可以使用和共享区块链。

要创建一个示例可执行文件，我们从以下代码开始：1   **#lang racket**2   (print "Hello")3   (read-bytes-line)

这段代码只会打印文本 Hello。打印过程打印一些文本（类似于显示），而 read-bytes-line 则等待用户输入。如果我们不使用 read-bytes-line，它会立即打印并退出，而在我们读取文本之前。

接下来，我们选择 Racket > 创建可执行文件。选择分发并选择创建。这样做之后，可执行文件应该会在目标文件夹中创建。![../images/510363_1_En_2_Chapter/510363_1_En_2_Fig10_HTML.jpg](img/510363_1_En_2_Fig10_HTML.jpg)

图 2-10

运行可执行文件

运行可执行文件应该显示类似于图 2-10 的内容。按下回车键将退出程序。

## 2.5 摘要

本章的重点是对 Racket 编程语言有一个基本的理解。以下是本章的学习内容：

+   Lisp 是一系列编程语言的家族，Racket 属于 Lisp 家族。

+   Lisp 与标准编程语言相比没有特殊的语法，语法是通过 S 表达式在 Lisp 中定义的。

+   Lisp 的评估非常类似于数学中的替换。

+   有几种原始类型：符号、布尔值、字符、字符串和列表。

+   列表是一种特殊的配对。

+   过程是捕捉抽象的一种方式。它们可以接受并返回任何类型的值，包括过程本身。它们也可以是递归的。

+   包允许我们重用代码，无论是自己编写的还是他人编写的。

+   生产出的可执行文件可以与朋友共享，以便每个人都可以使用它们。