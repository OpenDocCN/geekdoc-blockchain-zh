<hgroup>

# 第二部分

# 区块链概述

</hgroup>

<hgroup>

# 第四章

# Python 基础知识

</hgroup>

## 4.1 简介

Python 是一种用于通用编程的高级编程语言，由 Guido Van Rossum 在 1991 年开发。Python 特别设计为高度可读，因为它使用频繁的英语关键字。Python 经常用于在服务器上创建软件和 Web 应用程序。Python 的一些重要特性如下：

+   支持面向对象编程的概念。

+   它可以很容易地与其他编程语言集成，包括 C、C++、Java、公共对象请求代理体系结构（CORBA）等。

+   Python 是可伸缩的，因为它比 Shell 脚本更好地支持大型程序。

+   Python 高度依赖缩进，其中空格用于定义作用域。由于其强大的结构化构造，它支持清晰的编写和逻辑应用。

+   Python 可以很容易地连接到所有主要的商业数据库。

+   Python 是可移植的，因为它可以在多种硬件平台上运行。

+   Python 支持交互模式，可以进行代码的交互测试和调试。

+   Python 支持高级动态数据类型和动态类型检查。

+   Python 是一种脚本语言，因为它适合嵌入和编写小型的非结构化脚本。

+   Python 程序的长度比等效的 C、C++ 程序要短得多，原因如下：

    +   复杂的操作可以在单个语句中用 Python 的高级数据类型来表达。

    +   使用缩进而不是开始和结束括号。

    +   变量和参数的声明并不重要。

**注意：** Python 是一种编译和解释的编程语言。源代码首先被编译成字节码，然后该字节码在 Python 虚拟机上解释为机器语言以生成实际输出。字节码的概念实现了可移植性。然而，要执行 Python 代码，每次都需要 Python 程序代码。

编写程序后，请在文本编辑器中将程序保存为 .py 文件。此外，将该文件在 Python 解释器中执行。然而，在 Python 解释器中键入命令是玩弄 Python 特性的好方法，但不建议用于解决更复杂的问题。

本章的其余部分讨论了 Python 语言的各种重要特性，从简单语句、表达式、数据类型到类、对象、函数、文件处理等概念的示例。让我们开始 Python 编程。

## 4.2 注释

Python 中的注释用“#”表示。在“#”之后的所有内容都将被忽略。值得注意的是，注释不会被 Python 语言解释。

![](img/list4_1.jpg)

输出：5

## 4.3 多行语句

为了表示行应继续（多行语句），Python 允许使用行继续字符，即，例如：

![](img/list4_2.jpg)

## 4.4 块和缩进

Python 用缩进而不是使用起始和结束括号来表示块和嵌套块结构。使用缩进的优点包括减少编码标准的需求，减少不一致性，并减少工作量。缩进的空格数是可变的，但在一个块内，每个语句都必须缩进相同的数量。例如：

![](img/list4_3.jpg)

以下代码将生成一个错误：

![](img/list4_4.jpg)

## 4.5 创建变量并赋值

变量用来在保留的内存位置存储值。创建变量后，将保留内存中的空间。与其他编程语言不同，不需要显式声明变量。将值赋给变量后，使用该变量代替值。等号用于将值赋给变量。Python 字符串用单引号或双引号表示，结果相同。打印语句用于显示变量的值。例如，以下语句

![](img/list4_5.jpg)

输出：100

你好

h

变量的长度可以变化，并且可以任意长。变量可以包含字母和数字，但不能以数字开头。

## 4.6 数据类型

变量可以存储不同类型的数据。数字、字符串、列表、元组、字典是标准数据类型。Python 数字数据类型存储数值。例如：

a=1, b=2.

Python 包括三种不同的数值类型，即 int、float、complex。相比之下，字符串由一系列字符组成。但是，Python 中的字符串是不可变的，这意味着它不能被改变。字符串用单引号或双引号声明。例如：a=”abc”。本章将进一步讨论其余的数据类型。type()函数用于获取任何变量的数据类型。

![](img/list4_6.jpg)

输出：str

整数

浮点

列表

## 4.7 运算符

类似于其他编程语言，Python 支持以下运算符组：

+   算术运算符

+   比较运算符

+   赋值运算符

+   逻辑运算符

+   位运算符

+   成员运算符

+   身份运算符

### 4.7.1 算术运算符

此类别包括数学运算，如- 加法(+), 减法(-), 除法(/), 取模(%), 幂(**)。例如：

![](img/list4_7.jpg)

输出：

14

6

40

2.5

2

10000

### 4.7.2 比较运算符

此运算符用于比较值，并根据条件返回真或假。此类别包括大于(>)、小于(<)、等于(==)、不等于(!=)、大于等于(≥)和小于等于(≤)。例如：

![](img/list4_8.jpg)

输出：

a 不等于 b

a 不等于 b

a 不小于 b

a 大于 b

a 既不小于也不等于 b

b 既不大于也不等于 b

### 4.7.3 逻辑运算符

此类别执行逻辑 AND (and)、逻辑 OR (or) 和逻辑 NOT (not)。例如：

![](img/list4_9.jpg)

输出：

假

真

假

### 4.7.4 Python 位运算符

它执行按位操作。位运算符包括按位与(&)，按位或(∨)，按位非(¬)，按位异或(⊕)，按位右移(≫)和按位左移(≪)。

![](img/list4_10.jpg)

输出：

0

14

−11

14

2

40

### 4.7.5 赋值运算符

此运算符用于将值分配给变量。可用的赋值运算符包括：

=: 将右侧操作数的值赋给左侧操作数

+=: 将右操作数加到左操作数并将结果赋给左操作数

-=: 将右操作数从左操作数中减去，然后将结果赋给左操作数

*=: 将右操作数乘以左操作数并赋给左操作数

:̄ 将左操作数除以右操作数，然后将结果赋给左操作数

%=: 使用左右操作数取模，并将结果赋给左操作数

**=: 对运算符执行指数运算，并将值赋给左操作数

![](img/list4_11a.jpg)![](img/list4_11b.jpg)

输出：

var3 的值为 31

var3 的值为 52

var3 的值为 1092

var3 的值为 52

var3 的值为 2

var3 的值为 2097152

### 4.7.6 成员运算符

-   这个运算符用于检查序列中元素的成员资格。下面讨论了两个成员运算符：

-   in：如果元素存在于序列中，则结果为真，否则为假

-   not in：如果元素不是序列的成员，则结果为真，否则为假。

-   例如：

-   ![](img/list4_12.jpg)

-   

-   a 不在给定的列表中

-   b 不在给定的列表中

### -   4.7.7 身份运算符

-   这些运算符用于比较两个内存位置，即检查两个值是否位于内存的同一部分。Python 中有两个相同的运算符。

-   is：如果操作数相同，则返回真

-   is not：如果操作数不相同，则返回真

-   ![](img/list4_13.jpg)

-   输出：

-   a 和 b 有相同的标识

## -   4.8 Python 中的输入和输出

-   内置的 input() 函数用于从键盘接受用户输入。括号内的参数提示键盘输入。input() 函数会自动识别用户输入的是字符串、数字还是列表。然而，当输入被输入时，首先将其转换为字符串。即使输入整数值，也会使用类型转换将其转换为整数。

-   ![](img/list4_14.jpg)

-   假设用户输入了 abc 作为名称。

-   输出：Hello abc

-   生成输出的方式是使用 print() 函数，通过逗号分隔的零个或多个表达式。不带参数的 print()，即 print() 是为了换行。默认情况下，Python 的 print() 函数以新行结束，即 print() 函数会自动进入下一行。

-   ![](img/list4_15.jpg)

-   输出：

-   one

-   two

## -   4.9 列表

列表是 Python 的一个强大特性。它们与数组相同。列表是用于声明序列的数据类型。列表用方括号内的逗号分隔的项目声明。要访问列表项，使用索引号。值得注意的是，列表可能包含不同类型的项目。列表可以包含字符串、整数以及对象。此外，列表在声明后也可以更改。

![](img/list4_16.jpg)

输出：香蕉

![](img/list4_17.jpg)

输出：

22、'香蕉'、5、6

22、'香蕉'、5

5

**注意：** 元组与列表相同，唯一的区别在于元组是不可变的，即，在声明后它们不能被更改。

## 4.10 字典

Python 字典具有键和值，并用大括号编写。然而，字典中的键应该是唯一的，而值可以相同。要访问任何项，请在方括号内使用键名。

![](img/list4_18.jpg)

输出：10

## 4.11 Python 条件和 if-else

Python 的 if-else 语句与逻辑条件一起使用，如等于、不等于、小于等于、大于等于、大于和小于。如果语句使用 if 关键字指定。

![](img/list4_19.jpg)

输出：b 的值大于 a

**重点** Python 使用缩进来定义作用域

此外，elif 关键字用于检查前一个条件是否不成立，然后尝试此条件，如果任何前面的条件为假，则执行 else。大于等于、大于和小于。Elif 语句使用 elif 关键字指定。

![](img/list4_20.jpg)

输出：b 的值大于 a

## 4.12 循环

一般来说，任何编程语言的语句都是按顺序执行的。但是，可能存在需要执行不同路径的情况。循环块允许多次执行一个或多个语句。Python 支持两个循环命令：

+   While 循环

+   For 循环

**While 循环**：While 循环用于执行语句或语句块，直到满足给定条件。在语句变为 false 后，while 之后的第一条语句将被执行。

![](img/list4_21.jpg)

输出：

0

1

2

3

4

再见

While 也可以与 else 语句一起使用

![](img/list4_22.jpg)

输出：

0

1

2

3

4

再见

**For 循环**：在 Python 中，for 循环用于顺序遍历，例如，列表或数组。

![](img/list4_23.jpg)

输出：

苹果

芒果

香蕉

![](img/list4_24.jpg)

输出：

0,1,2,3,4

## 4.13 Python 中的函数

函数是一组语句块，接受一些输入，执行一些计算，并产生输出。基本上，函数用于将重复执行的任务组合在一起。函数在调用时执行。Python 中有一些内置函数，例如- print()，也可以使用 def 关键字创建函数。要调用函数，请使用该函数的名称，后跟括号。

![](img/list4_25.jpg)![](img/list4_26.jpg)

输出：

奇数

偶数

## 4.14 Python 中的类和对象

正如前面讨论的，Python 是一种面向对象的语言。类似于对象构造函数或创建对象的蓝图的类，而对象是带有实际值的类的副本。类易于将数据和功能捆绑在一起。每个类都保存其自己的数据成员和成员函数，可以使用对象访问。尽管如此，一个类可以有许多对象。类的属性始终是公共的，并且可以使用点 (.) 运算符访问。要创建一个类，使用关键字 class。

![](img/list4_27.jpg)

输出：5

![](img/list4_28a.jpg)![](img/list4_28b.jpg)

输出：

动物

我是一个动物

我是一只狗

要创建现实生活中的应用程序，我们需要了解一个特殊的函数，称为 `init()`，它是创建类的新实例的初始化方法。特别是，当对象被创建时，`init()` 方法用于为对象属性赋值。

![](img/list4_29.jpg)

输出：

约翰

36

## Python 中的文件处理

文件在磁盘上有一个位置，并带有一些存储的信息。与 Java 和 C++ 一样，Python 也支持文件处理，并允许用户通过读取和写入来处理文件。文件中的每行代码都包含一系列字符。此外，每行都以特殊的终止符号结尾，称为行结束符（EOL），告诉解释器新的一行已经开始。大多数文件操作都使用文件对象完成。

### 4.15.1 open() 函数

显然，在读取或写入文件之前，必须首先打开它。要打开文件以进行读取或写入，使用 `open()` 函数。`open()` 函数创建一个文件对象，并接受两个参数，即文件名和模式。语法：

*open(filename; mode)*

`mode` 字段指示文件如何被打开。例如：

r：只读方式打开文件

rb：以二进制格式仅用于读取的方式打开文件

w：只写方式打开文件

r+：以二进制格式同时用于读取和写入的方式打开文件

wb：以二进制格式仅用于写入的方式打开文件

a：以追加的方式打开文件

a+：以追加和读取的方式打开文件

如果指定名称的文件不存在，则会引发 FileNotFoundError 错误。

### 4.15.2 close() 函数

`close()` 方法关闭文件对象，并阻止对该文件的进一步操作。

语法：

`fileObject.close()`

![](img/list4_30.jpg)

输出：

文件名称：foo.txt

### 4.15.3 read() 函数

此函数从打开的文件中读取一个字符串。

语法：

*fileObject:read([count])*

计数参数指定从指定文件中读取的字节数。 如果缺少计数参数，则文件将读取直到文件的末尾。

![](img/list4_31.jpg)

输出：

来自名为 foo.txt 的文件的前 10 个字符。

## 4.16 write() 函数

此函数允许用户将字符串写入打开的文件。 值得注意的是，write 函数不会隐式添加换行符，即字符串的末尾。

语法：

*fileObject:write(string)*

![](img/list4_32.jpg)

输出：

Python 是一种高级语言

Python 遵循 OOPS 概念

## 活动

### 多项选择题

1.  如何在 Python 代码中插入注释？

    1.  \ *这是一个注释* \

    1.  ＃这是一个注释

    1.  “这是一个注释”

    1.  这些都不是

1.  哪个不是合法的变量名？

    1.  abc

    1.  10abc

    1.  _abc

    1.  abc_abc

1.  以下 Python 表达式的值是多少？

    1.  9.0

    1.  9

    1.  4.0

    1.  4

1.  以下代码的输出是什么？

    x = 100

    y = 50

    打印（x 和 y）

    1.  真

    1.  假

    1.  100

    1.  50

1.  什么是在 Python 中输出“hello world”的正确语法？

    1.  print(“hello world”)

    1.  echo(“hello word”)

    1.  put(“hello word”)

    1.  这些都不是

1.  Python 文件的正确文件扩展名是什么？

    1.  .py

    1.  .python

    1.  .pyt

    1.  这些都不是

1.  以下代码的输出是什么？

    打印类型（类型（int））

    1.  类型‘int’

    1.  类型‘类型’

    1.  错误

    1.  0

1.  假设 listA 是 [31, 41, 5, 20, 5, 125, 1, 3]，那么 list1.pop(1) 后 list1 的值是什么？

    1.  31, 41, 5, 20, 5, 125, 1, 3

    1.  31, 41, 5, 20, 5, 125, 1

    1.  31, 41, 5, 20, 5, 125, 1, 3, 3

    1.  这些都不是

1.  以下程序的输出是什么？

    j = 0

    while i ≤ 5：

    print j

    j++

    打印 j+1

    1.  0 2 1 3 2 4

    1.  错误

    1.  5 4 3 2 1

    1.  这些都不是

1.  <math alttext="" display="inline"><mo>¬</mo><mo>¬</mo><mo>¬</mo><mo>¬</mo><mo>¬</mo><mo>¬</mo></math> 5 的值是多少？

    1.  +5

    1.  -5

    1.  10

    1.  11

1\. b  2\. b  3\. a  4\. d  5\. d  6\. a  7\. b  8\. b  9\. b（Python 中没有 ++ 运算符）  10\. a

<hgroup>

# 5

# 密码学原理

</hgroup>

## 5.1 介绍

保密性、完整性、可用性也被称为 CIA 三元模型，是用于定义实现信息安全政策的模型（参见图 5.1）。除此之外，不可否认和身份验证是 P2P 网络需要实现的其他安全属性。

+   保密性：保密性表示信息、数据和资源受到未经授权的各方的保护。数据加密和密码是确保保密性的常见方法。tcolorbox

    **要点** 保密性类似于隐私一词；但它们不能互换使用。事实上，保密性是隐私的延伸，涉及可识别数据。

+   完整性：此属性表示保护信息免受未经授权的更改。完整性确保数据的准确性和完整性。访问控制机制、校验和和哈希是确保数据完整性的一些措施。

+   可用性：此属性确保授权方在需要时能够访问信息。如果服务器/系统保持可用状态，防止服务中断并保持不间断访问，这表示高可用性。即使短时间的服务中断也可能导致收入损失、客户失望和组织声誉受损。在所有可用性攻击中，DoS 是黑客最常使用的攻击方式。代理服务器、防火墙和路由器是确保数据可用性的对策。

+   不可否认性：此属性确保数据的发送者不能否认后来发送了数据，接收者也不能否认收到了数据。在法律术语中，否认意味着否认某事是真实的。数字签名、时间戳、哈希函数是获得不可否认性的一些方法。

+   认证：这是识别个人的行为。然而，认证并不涉及个人的访问权限。特别是，认证确认用户的身份。

![图 5.1](img/fig5_1.jpg)

**图 5.1**

信息安全的 CIA 三元素。

值得注意的是，密码学在确保上述安全属性的实现中发挥着非常重要的作用。接下来，我们将讨论基本的密码原语。我们将首先讨论密码散列函数的细节，然后讨论数字签名的概念。

## 5.2 加密/解密过程

### 5.2.1 加密

加密是将原始数据转换为不可识别形式的过程。数据通常是加密的，以免被窃取。加密由发送方执行。

### 5.2.2 解密

与加密相反，解密是将密文转换回明文的过程。解密在接收方执行。

### 5.2.3 对称密钥加密

这种类型的加密使用相同的密码密钥来加密明文和解密密文。

### 5.2.4 非对称密钥加密

此加密过程涉及 2 对密钥。在这里，发送方和接收方都有一对公钥和私钥。公钥用于加密明文，而私钥用于解密目的。为了完成许多密码任务，使用公钥和私钥。

### 5.2.5 公钥

公钥是为所有其他用户公开的。公钥使用典型的非对称算法生成，以便与关联的私钥匹配。用于创建公钥的最流行算法有：RSA、ECC 和数字签名应用（DSA）。这些提到的算法基于重型计算方法，以创建不同长度的随机数字组合，以防止暴力破解攻击。密钥的长度决定了保护的强度。较大的密钥尺寸能够提供更多的密码安全，以防止黑客阻止它们。

### 5.2.6 私钥

与公钥相反，私钥是仅由密钥所有者知晓的秘密密钥。私钥是使用创建公钥的相同算法创建的。

**关键点** 私钥用于解密、数字签名和身份验证，而公钥用于加密、验证数字签名和身份验证。

## 5.3 密码哈希函数

密码哈希函数 <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>H</mi><mo stretchy="false">)</mo></mrow></math> 接受可变长度的输入或消息 <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></math> 并产生固定大小的输出，称为哈希值或消息摘要 <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">)</mo></mrow></math>，如在 图 5.2 中所示。

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>h</mi><mo>=</mo><mi>H</mi><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></mtd></mtr></mtable></mrow></math>(5.1)

通常，消息摘要的大小小于实际输入数据。因此，哈希函数有时被称为压缩函数。

![图 5.2](img/fig5_2.jpg)

**图 5.2**

密码哈希函数的块图。

要点

+   哈希函数遵循多对一的特性，因此可能会发生碰撞。

+   在区块链中，消息摘要的大小为 256 比特。

+   哈希函数的计算效率很高，因为这些计算不需要大量资源。

+   一个好的哈希函数会产生均匀分布的输出。

+   即使是对 M 的单比特变化也会改变完整的哈希码。

### 5.3.1 哈希函数的典型特性

+   对于给定的哈希值*h[1]*，找到确切散列为*h[1]*的输入*M[1]*应该是一种困难的过程。这种属性称为不可逆性或前像抗性。此类哈希函数也称为单向函数。

+   对于给定的输入及其对应的哈希，要计算出具有相同哈希的不同输入应该是计算上困难的，即，对于具有哈希值*h[1]*的输入*M[1]*，很难找到任何其他输入*M[2]*，使得<math alttext="" display="inline"><mrow><mi>H</mi><mo stretchy="false">(</mo><msub><mi>M</mi><mn>1</mn></msub><mo stretchy="false">)</mo><mo>=</mo><mi>H</mi><mo stretchy="false">(</mo><msub><mi>M</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></math>成立。哈希函数的这种特性称为第二图像抗性。

+   哈希函数的另一个重要属性是无碰撞性，它表明如果两个消息不同，那么它们的消息摘要也将不同，即，如果两个消息 *M[1]*、*M[2]* 不相等（*M1 <math alttext="" display="inline"><mo>≠</mo></math> M2*），那么 <math alttext="" display="inline"><mrow><mi>H</mi><mo stretchy="false">(</mo><msub><mi>M</mi><mn>1</mn></msub><mo stretchy="false">)</mo><mo>≠</mo><mi>H</mi><mo stretchy="false">(</mo><msub><mi>M</mi><mn>2</mn></msub><mo stretchy="false">)</mo></mrow></math>。

+   给定两个消息 *M[1]*、*M[2]*，和一个哈希函数 *h*，要找到一个值 *k*，使得 <math alttext="" display="inline"><mrow><msub><mi>M</mi><mn>2</mn></msub><mo>=</mo><mi>h</mi><mo stretchy="false">(</mo><msub><mi>M</mi><mn>1</mn></msub><mi mathvariant="normal">‖</mi><mi>k</mi><mo stretchy="false">)</mo></mrow></math> 是困难的。哈希函数的这种属性称为难题友好性。

### 5.3.2 哈希函数的要求:

+   **单向性:** 一旦计算出哈希值，就不能用它来恢复原始文档。例如，就像人类的指纹一样，不能通过指纹来还原一个人的外貌。

+   **确定性:** 它表明，如果两个相似的文档通过同一个哈希算法，它们应始终生成相同的哈希值。

+   **雪崩效应:** 它表明，即使在文档中改变一个比特，改变后的文档的哈希值应显著不同于原始文档的哈希值。

+   **必须经受住碰撞:** 这意味着哈希函数应具有碰撞抗性属性。

### 5.3.3 密码哈希函数的应用

+   密码存储：每当用户使用用户名、ID 和密码创建帐户时，ID 提供者不会存储密码。相反，提供者通过哈希算法传递密码，并且仅存储密码的哈希值。每当用户尝试登录时，提供者对用户输入的密码进行哈希处理，并将其与保存的哈希值进行比较。提供者有一个密码文件，该文件包含以 [用户 ID1*h(P1*)] 格式的对表，用于给定的用户 ID（ID1）和密码（P1）。如果两个哈希值匹配，则授权提供给该帐户，否则不提供。整个过程已在图 5.3 中描述。

    ![图 5.3](img/fig5_3.jpg)

    **图 5.3**

    使用哈希函数进行密码存储。

+   数据完整性检查：哈希函数的一个非常流行的应用是数据完整性检查。通过这种方式，哈希函数可以保证数据的正确性，即用户可以检测到对原始文件进行的任何修改、插入和删除。

    **情况 1:**

    消息<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>M</mi><mo stretchy="false">)</mo></mrow></math>与*M*的计算哈希值一起使用对称加密进行加密。加密确保了消息的机密性。为了检查消息的完整性，首先，对接收到的加密块应用解密，然后从块中提取消息。接下来，对消息*M*应用相同的哈希算法，计算得到的哈希值与接收到的哈希值进行匹配。整个过程已在图 5.4 中显示。

    ![图 5.4](img/fig5_4.jpg)

    **图 5.4**

    使用消息加密进行数据完整性检查。

    **情况 2:**

    在某些情况下，仅对哈希代码进行加密，以减轻不需要机密性的应用程序的负担。要检查消息的完整性，请使用密钥解密收到的哈希，然后从消息计算哈希摘要，并将其与源中收到的哈希摘要进行比较。整个过程已在图 5.5 中显示。

    ![图 5.5](img/fig5_5.jpg)

    **图 5.5**

    不进行消息加密的数据完整性检查。

### 5.3.4 MD5 消息摘要算法

消息摘要算法 5（MD5）是消息摘要算法 4（MD4）的扩展，由 Ron Rivest 在 1991 年开发。但是，MD5 比 MD4 稍慢，但确保比 MD4 更好的安全性。特别地，它用于验证数据的完整性。此外，在使用私钥加密文件之前，通过将大文件压缩到安全方式中使用作为 DSA。此哈希算法接受任意长度的输入，并生成 128 位的指纹作为输出。

MD5 的基础是 Merkle-Damgard 结构。该算法以 512 位块处理数据，每个块被分成 16 个 32 位块。MD5 产生 128 位输出的逐步工作定义如下：

+   **追加填充位：** 填充意味着向原始消息添加一些额外位。在这里，消息被填充以使总位长度比精确的 512 的倍数少 64 位。为了填充，第一个位是 1，其余位是 0。例如，对于 1000 位的消息，填充了 472 位（1000 + 472 = 1472，比 512 的倍数少 64 位）。

+   **追加长度：** 在填充后，通过计算原始消息的长度 mod 264，在末尾插入 64 位。因此，结果消息是 512 位的倍数。

+   **分割消息：** 将得到的消息分成 512 位的块。

+   **初始化 MD 缓冲区：**接下来初始化一个四字缓冲区。这四个缓冲区分别为(A、B、C、D)，都是 32 位寄存器，并且其值是预定义的。值得注意的是，最终的输出只存在于这些缓冲区中。

+   **在 16 字块中处理消息：**每个 512 位的块在 4 轮中处理，并且每轮都使用四个函数 F、G、H、I。此外，每轮由 16 个步骤组成，使用一些常量。因此，每个 512 位的块会执行总共 64 次操作，此块的输出作为 A、B、C、D 的值被传递到下一个块中。

### 5.3.5 SHA-256

区块链比特币挖掘利用了一种特殊类型的哈希函数，称为 SHA-256，此哈希函数生成 256 位的消息摘要。SHA 代表安全哈希算法。SHA-256 的操作方式也类似于 MD4、MD5 和 SHA-1\. 哈希函数的计算首先从对消息进行预处理开始。预处理包括：

+   首先，对消息进行填充，以使总消息大小成为 512 位的倍数。为此，请执行以下操作：

    +   假设消息的长度*l*以位为单位，且*l*mod512 ≠ 0。

    +   在消息的末尾附加一个值为 1 的位。

    +   接下来，附加 k 个零位，使得 l+1+k ≡ 448mod512。

    +   在此之后附加一个值为*l*的 64 位块，该长度以二进制形式书写。为了避免平凡的冲突，会追加这个长度。要提取原始消息，请读取最后的 64 位（用于计算消息的长度），然后从左到右开始获取位。

    +   填充后消息的结果长度应为 512 位的倍数。

    例如，给定消息为‘abc’。

    +   它的长度为 24（8*3）。

    +   首先，消息在末尾填充一个 1。

    +   接下来，附加 448-(24+1)个零位，即，423 个零位。

    +   最后，附加一个以二进制写入的值为 24 的 64 位块，结果为：

        <math alttext="" display="block"><mrow><mn>011000101100010011000111</mn><munder><munder><mrow><mn>00.....0</mn></mrow><mo stretchy="true">︸</mo></munder><mrow><mn>423</mn><mtext>times</mtext></mrow></munder><munder><munder><mrow><mn>00.....011000</mn></mrow><mo stretchy="true">︸</mo></munder><mrow><mn>64</mn><mtext>bit</mtext></mrow></munder><mo>.</mo></mrow></math>

        现在，结果的长度为 512 位。

+   接下来，将原始消息*M*解析为 512 位的*N*个块，即，M1、M2、………、MN。

+   每个 512 位块分成 16 个子块<math alttext="" display="inline"><mrow><msubsup><mi>M</mi><mn>0</mn><mi>i</mi></msubsup></mrow></math>, <math alttext="" display="inline"><mrow><msubsup><mi>M</mi><mn>1</mn><mi>i</mi></msubsup></mrow></math>,……., <math alttext="" display="inline"><mrow><msubsup><mi>M</mi><mrow><mn>15</mn></mrow><mi>i</mi></msubsup></mrow></math>，每个子块的长度为 32 位。

+   每个消息块逐个处理。为了处理每个块，初始化一个 256 位的固定哈希值，也称为初始化向量（IV），表示为 h0。

+   接下来，依次计算：

    <math alttext="" display="inline"><mrow><msup><mi>H</mi><mi>i</mi></msup><mo>=</mo><msup><mi>h</mi><mrow><mo stretchy="false">(</mo><mi>i</mi><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></msup><mo>+</mo><msubsup><mi>C</mi><mi>M</mi><mi>i</mi></msubsup><mo stretchy="false">(</mo><msup><mi>H</mi><mrow><mo stretchy="false">(</mo><mi>i</mi><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></msup><mo stretchy="false">)</mo></mrow></math>

    其中，C 是压缩函数，+ 表示模 2³² 的加法。

## 5.4 数字签名

数字签名是安全区块链架构背后的另一个重要基础。它是一种验证数据真实性和完整性的加密方法。数字签名还防止了抵赖，即发送方无法否认文档的来源。数字签名的工作方式类似于物理签名；然而，它们是电子签名。然而，签署权限仅限于签署文档的权限，并且拥有有效密钥的任何人都可以验证签名。此外，一个文档的签名不能转移到另一个文档。

数字签名是通过非对称密钥加密（公钥密码术）的概念实现的。非对称密钥加密使用两把不同的密钥，即公钥和私钥。公钥只有用户知道，而私钥则为宇宙中所有人所知。为了保持数据的机密性，待传输的数据使用接收方的公钥加密，而在目标节点上使用私钥解密。

### 5.4.1 数字签名模型

要生成数字签名，使用发送者的私钥对消息进行签名，在目标端使用发送者的公钥验证签名。然而，通过将密码哈希的概念与数字签名集成，可以减小数字签名的大小。因此，与签署原始消息相比，签署消息摘要。生成数字签名的步骤如下所示：

+   首先，对消息(*M*)进行哈希处理以获取消息摘要*h(M)*。接下来，使用发送者的私钥对生成的哈希进行签名，结果是数字签名。

+   然后，消息和数字签名通过通道传输。

+   接收者在收到特定数字签名后，使用发送者的公钥对其进行解密（这确保了发送者的**真实性**）。应用解密算法后，接收者将获得消息摘要*h(M)*。

+   同时，接收到原始消息的接收者将计算其哈希值。我们称此值为*h’(M)*。

+   如果*h(M)*=*h’(M)*，则原始文档的**完整性**得以保留。

+   由于只有文档签署者知道私钥，因此其他人无法生成签名者的签名。因此，它确保**不可否认**属性。

在图 5.6 中描述了生成哈希函数的整个过程。因此，通过应用哈希函数，可以减小签名的大小。

![图 5.6](img/fig5_6.jpg)

**图 5.6**

数字签名。

关键点

+   密码学密钥应防止他人猜测。但是，假设密码算法为所有人所知。

+   密钥的长度应足够长，因为与短长度密钥相比，长长度密钥难以猜测。

+   密钥应该以足够的熵真正随机生成。

## 5.5 零知识证明

与区块链相关的另一个概念是零知识证明。这是一种加密方法，可以向验证者证明证明者知道一个值，而实际上不透露任何数据，除了透露证明者知道该值的事实。简单地说，通过生成最终输出，证明者应该证明他们可以计算某些东西，而不告诉计算过程，而验证者只知道输出。

例如，A 想向 B 证明他/她知道密钥而不向 B 泄露秘密密钥，并且 B 验证 A 实际拥有密钥。因此，它们有能力彻底改变数据处理、收集的方式，以及数据交易的方式。零知识证明具有 3 个重要特性：

+   完整性：如果事实是真的，证明者应该说服验证者这一事实，并且零知识证明应该返回真。

+   声明的准确性：如果事实/声明是错误的，证明者不能说服验证者证明证明者的陈述是正确的。

+   零知识/隐私：如果证明者提供的信息是真实的，没有验证者会得知除了该信息是真实的这一事实以外的其他信息。换句话说，提供者的信息不应向验证者透露其他内容。

为了更好地理解零知识证明，让我们来看一个广为流传且经典的零知识证明示例，即**两个球和色盲朋友**。

假设 A 有两个相同的球，颜色不同（比如一个红色和一个绿色），而你的朋友 B 是色盲的，这意味着 B 无法根据球的颜色区分它们。但是，A 必须向 B 证明两个球的颜色不同。然而，A 不想透露哪个是红色，哪个是绿色。这就是这个问题的证明系统的工作原理：

+   A 将两个球都给了 B，并把两个球都藏在背后。

+   然后 B 从背后拿出两个球中的一个并展示给别人看。

+   B 再次把球放回他/她的背后，然后随机选择其中一个球，只有一个球会被展示出来，而且概率相同。

+   接下来，B 问 A：“我交换了球吗？”

第三步和第四步一直重复，直到 B 确信有两个不同颜色的球。显然，通过球的颜色，A 可以确定 B 是否交换了它们。此外，如果球的颜色相同且因此无法区分，那么 A 可以以不超过 50%的概率猜测球是否被交换。如果 A 和 B 多次重复此过程，A 如果撒谎就会被抓住。

显然，上述证明系统是零知识的，因为 B 永远不会知道哪个是绿球，哪个是红球。

此外，零知识证明有两个变体：交互式零知识证明和非交互式零知识证明。在交互式证明中，证明者和验证者交换多个消息来证明或验证信息。它要求验证者不断询问证明者所拥有的知识。不幸的是，交互式零知识证明的可转移性有限。相比之下，非交互式证明系统要求证明者和验证者之间没有交互，除了双方之间共同的参考字符串。

关键点

**区块链中的零知识证明应用：** 两种流行的区块链用例，即比特币和以太坊，都是基于公共地址来表示用户的真实身份，从而在网络中保持匿名。值得注意的是，由于区块链的分布式特性，交互式零知识证明不是一个高效的解决方案。此外，零知识证明的现实世界用例是 Zcash，它使本地交易完全加密，同时受到网络共识规则的验证，而 Zcash 是一种非交互式零知识证明系统。

## 5.6 哈希表

这是一种流行的数据结构，支持快速插入和搜索操作，无论数据的大小如何。它基本上是一种从一组相似对象中识别特定对象的方法。特别是，哈希表（也称为散列表）以数组格式存储数据，每个数据值与唯一的索引值相关联。哈希表利用哈希函数生成索引，即数据元素应插入的位置。数据结构中的信息有两个主要组成部分，即唯一键和值。例如，键可以是唯一 ID（键不必每次都是整数），值是电话号码。哈希函数将决定将键映射到何处以及在何处存储相应的值。映射的效率取决于哈希函数的效率。基本上，我们使用输入元素的集合比哈希表的容量要大得多，以便避免冲突。显然，如果表中的项数增加，则冲突也会增加。为了衡量哈希表有多满，使用负载因子（*α*）的概念，它被定义为使用的键数（*n*）和表的总容量（*m*）的比例。

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>α</mi><mo>=</mo><mfrac><mi>n</mi><mi>m</mi></mfrac></mrow></mtd></mtr></mtable></mrow></math>(5.2)

值得注意的是，*n*不能超过表的总容量。如果*α*接近最大值，则冲突的可能性显著增加。

在链表中，插入操作是高效的，而查找仍然需要线性时间。此外，在排序数组中，查找是高效的，但插入则不足够。值得注意的是，对于*n*个元素，链表可以在<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>时间内搜索，而二分查找需要<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mi>o</mi><msub><mi>g</mi><mn>2</mn></msub><mi>n</mi><mo stretchy="false">)</mo></mrow></math>时间，并且数组在搜索时消耗<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>的时间。相比之下，哈希表允许快速插入、删除和搜索，即平均情况下的<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math>时间（请参阅表 5.1）。让我们以哈希表数据结构为例，如图 5.7 所示，其哈希函数为：<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mi>x</mi><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn></mrow></math>，其中*x*为键。假设项目以（键，值）格式排列，项目分别为（1，999）、（2，9876）、（45，5434）、（90，9877）。因此，哈希表组织数据以便可以快速查找给定键的任何数据。然而，可能会出现两个或更多数据项碰撞并散列到同一索引的情况。这称为碰撞问题。例如，如果我们要插入一个项目（55，7767），这个插入将导致碰撞，因为在索引 5 处已经有一个项目。良好的哈希函数避免碰撞。碰撞解决技术分为两个主要部分，即封闭寻址和开放寻址。为了避免碰撞，封闭寻址使用额外的数据结构，而开放寻址哈希将所有数据存储在表内。更正式地说，在使用开放寻址的碰撞解决方案时，连续尝试单元*h0(x), h1(x),……., hm-1(x)*。

**表 5.1**

哈希表的平均和最坏情况复杂度。

|  | 平均复杂度 | 最坏情况复杂度 |
| --- | --- | --- |
| 空间 | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math> | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math> |
| 插入 | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math> | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math> |
| 删除 | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mn>1</mn><mo stretchy="false">)</mo></mrow></math> | <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math> |

![图 5.7](img/fig5_7.jpg)

**图 5.7**

哈希表的示例。

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mi>f</mi><mo stretchy="false">(</mo><mi>i</mi><mo stretchy="false">)</mo><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></mtd></mtr></mtable></mrow></math>(5.3)

其中，*f(0)=0* 函数 *f* 称为冲突解决策略，<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> = 主哈希函数，*x* 为键，*m* 为表大小。接下来，我们将讨论流行的冲突解决技术。冲突解决技术的分类已在图 5.8 中表示。

![图 5.8](img/fig5_8.jpg)

**图 5.8**

冲突解决技术的分类。

### 5.6.1 链接分离

避免冲突的一种可能方法是简单地将具有相同索引的数据存储到数组的相应索引处的链表中。这种方法称为链式存储。在这里，每个数组槽都保存一个指向链接列表的指针，该列表具有散列到相同散列索引的所有键的值，如图 5.9 所示。

**查找：** 当然，这种解决方案最终会以线性时间结束，即在最坏情况下查找的时间复杂度为<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>。因为在最坏情况下，所有的键可能都具有哈希表的相同索引，因此为了执行顺序搜索，时间需求为<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>。此外，该方法的缓存性能不佳。尽管使用此方法易于实现且哈希表永远不会填满。

**删除：** 要删除，首先需要搜索键然后删除。因为搜索的最坏情况时间复杂度为<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>，所以删除所需的时间为<math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>。

![图 5.9](img/fig5_9.jpg)

**图 5.9**

每个数组槽包含指向链表的指针。

### 5.6.2 线性探测

线性探测是处理冲突的常用方法。探测简单地意味着在发生冲突时找到下一个空单元格，将键放入其中。此方法属于使用开放地址法的冲突解决方法之一。在发生冲突时插入，会尝试直到找到一个空单元格为止。因此，表的大小应等于或大于键的总数。正式地，对于线性探测，*f* 是线性函数，通常在方程式 5.3 中表示为 <math alttext="" display="inline"><mrow><mi>f</mi><mo stretchy="false">(</mo><mi>i</mi><mo stretchy="false">)</mo><mo>=</mo><mi>i</mi></mrow></math>，即，<math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mi>i</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> 显然，搜索的最坏情况复杂度为 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>m</mi><mo stretchy="false">)</mo></mrow></math>。

然而，线性探测面临聚类问题，即，如果多个连续项形成一个组，则查找一个空插槽以进行插入或搜索项将需要很长时间。让我们通过一个例子来理解线性探测，假设 3、17、14、6、21、13、7、22 是要依次插入的键，<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>2</mn><mi>x</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn></mrow></math>是键*x*的哈希函数。参见图 5.10，每个键的哈希值如下：

*h(3)*=9

*h(17)*=7

*h(9)*=1

*h(6)*=5

*h(21)*=5

*h(13)*=9

*h(7)*=7

*h(22)*=7

![图 5.10](img/fig5_10.jpg)

**图 5.10**

线性探测的例子。

**插入 3,17,14,6：** 这 4 个元素的插入不会发生冲突。因此，它们被插入到根据给定哈希函数计算的哈希索引位置。

**插入 21**：由于<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mn>21</mn><mo stretchy="false">)</mo></mrow></math> =5，而此位置已经被键 6 占据。因此，让我们尝试使用线性探测方程：<math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mi>i</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math>，其中 i=0 到 m-1

**i=0**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>0</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>5</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>5</mn></mrow></math> 这个位置已经被占据。

接下来，**i=1**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>5</mn><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>6</mn></mrow></math> 这个位置是空闲的。因此，21 被插入到位置 6。

同样地，13、7 和 22 被插入。

这个插入的例子见于图 5.10。

### 5.6.3 二次探测

这是另一种解决哈希表冲突的开放定址方案。它通过取密钥的哈希值并添加二次多项式的连续值来工作。更正式地说，对于二次探测，<math alttext="" display="inline"><mrow><mi>f</mi><mo stretchy="false">(</mo><mi>i</mi><mo stretchy="false">)</mo><mo>=</mo><msup><mi>i</mi><mn>2</mn></msup></mrow></math>，即，<math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><msup><mi>i</mi><mn>2</mn></msup><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> 其中 i=0 到 m-1。

这种方案具有良好的内存缓存，因为它保留了引用的局部性。此外，与线性探测相比，它避免了聚类问题。让我们通过一个例子来了解二次探测。参考 图 5.11。再次考虑 3、17、14、6、21、13、7、22 是要按顺序插入的键，<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>2</mn><mi>x</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn></mrow></math> 是键 *x* 的哈希函数。每个键的哈希值如下：

![图 5.11](img/fig5_11.jpg)

**图 5.11**

二次探测的示例。

*h(3)*=9

*h(17)*=7

*h(9)*=1

*h(6)*=5

*h(21)*=5

*h(13)*=9

*h(7)*=7

*h(22)*=7

**插入 3,17,14,6：** 插入这 4 个元素不会遇到任何冲突。所以，它们被插入到根据给定的哈希函数计算的它们的哈希索引。

**插入 21**：*h(21)* 是 5，被键值 6 占用。所以，让我们尝试使用二次探测方程： <math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><msup><mi>i</mi><mn>2</mn></msup><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math>，其中 i=0 至 m-1 **i=0**： <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> = <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> +0)mod m ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =(5)mod 10 =5 被占用。

接下来，**i=1**： <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> = <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> +1²)mod m ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =(5+1)mod 10= 6，这个位置是空的。所以，21 被插入到位置 6。

**插入 13**： <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mn>13</mn><mo stretchy="false">)</mo></mrow></math> =9，已被占用。所以，让我们尝试二次探测 **i=0**： <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> = <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> +0)mod m ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =(9)mod 10 =9，已被占用。

**i=1**： <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> = <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> +1²)mod m ⟹ h1(x)=(9+1)mod 10= 0，此位置为空。因此，13 被插入到位置 0。

**插入 7**：由于 <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mn>7</mn><mo stretchy="false">)</mo></mrow></math> =7 已被占用，所以让我们尝试二次探测。 **i=0**： <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> = <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> +0)mod m ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =(7)mod 10 =7，已被占用。

**i=1**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> = <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> +1²)mod m ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =(7+1)mod 10= 8 这个位置是空的。所以，7 被插入到位置 8。

**插入 22**: <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mn>22</mn><mo stretchy="false">)</mo></mrow></math> =7，这个位置已经被占用。所以，让我们尝试二次探测 **i=0**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =( <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> +0)mod m ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =(7)mod 10 =7 这个位置已经被占用。

**i=1**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =( <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> +1²)mod m ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =(7+1)mod 10= 8，而且这个位置也不是空的。 **i=2**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =( <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> +22)mod m ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =(7+4)mod 10= 1，而且这个位置也不是空的。

**i=3**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>3</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =( <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> +22)mod m ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>3</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =(7+9)mod 10= 6，而且这个位置是空的。因此，22 被插入到位置 6。

### 5.6.4 双重哈希

这种技术在冲突的情况下对给定的键应用第二个哈希函数，即，<math alttext="" display="inline"><mrow><mi>f</mi><mo stretchy="false">(</mo><mi>i</mi><mo stretchy="false">)</mo><mo>=</mo><mi>i</mi><mo>*</mo><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> 和 <math alttext="" display="inline"><mrow><mi>i</mi><mo>=</mo><mn>0</mn><mi>t</mi><mi>o</mi><mi>m</mi><mo>−</mo><mn>1</mn></mrow></math> 其中，h2(x) 是另一个哈希函数。第二个哈希函数提供了一个偏移值来解决冲突。这种技术也被称为双重哈希技术。值得注意的是，一个良好的第二个哈希函数确保所有单元都被均匀探查。不幸的是，与其他探查方案相比，双重哈希的计算成本较高。让我们通过一个示例来理解二次探查，如图 5.12 所示。再次考虑要插入的键为 3、17、14、6、21、13、7、22，并且<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>2</mn><mi>x</mi><mo>+</mo><mn>3</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn></mrow></math> 是键 *x* 的哈希函数。假设另一个哈希函数为<math alttext="" display="inline"><mrow><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>3</mn><mi>k</mi><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn></mrow></math>，每个键的哈希值如下：

*h(3)*=9

*h(17)*=7

*h(9)*=1

*h(6)*=5

*h(21)*=5

*h(13)*=9

*h(7)*=7

*h(22)*=7

![图 5.12](img/fig5_12.jpg)

**图 5.12**

双重哈希的示例。

**插入 3,17,14,6:** 这 4 个元素的插入没有发生任何碰撞。因此，它们被插入到根据给定哈希函数计算的哈希索引处。

**插入 21**: <math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mn>21</mn><mo stretchy="false">)</mo></mrow></math> 是 5，已被关键字 6 占据。因此，让我们应用双重哈希，并使用等式：<math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mi>i</mi><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> 其中 i=0 到 m-1。**i=0**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>0</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>5</mn><mo>+</mo><mn>0</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>5</mn></mrow></math> 已被占据。

**i=1**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>1</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>5</mn><mo>+</mo><mn>1</mn><mo>*</mo><mn>4</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>9</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>9</mn></mrow></math> 并且也不是自由的 <math alttext="" display="inline"><mrow><mo stretchy="false">[</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mn>21</mn><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>3</mn><mo>*</mo><mn>21</mn><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>4</mn><mo stretchy="false">]</mo></mrow></math>

**i=2**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>2</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>5</mn><mo>+</mo><mn>2</mn><mo>*</mo><mn>4</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>13</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>3</mn></mrow></math> 并且是免费的。 因此，在位置 3 插入了关键字 21。

**插入 13**：<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mn>13</mn><mo stretchy="false">)</mo></mrow></math> 是 9，由键值 3 占用。因此，让我们应用双重散列的方程式：<math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mi>i</mi><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> 其中 i=0 到 m-1。**i=0**：<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>0</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>9</mn><mo>+</mo><mn>0</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>9</mn></mrow></math> 被占用。

**i=1**：<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>1</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math>。值得注意的是，<math alttext="" display="inline"><mrow><mo stretchy="false">[</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mn>13</mn><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>13</mn><mo>*</mo><mn>3</mn><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>0</mn><mo stretchy="false">]</mo></mrow></math>。因此，这将始终导致哈希索引 9，该索引已被占用。这表明第二个哈希函数的选择不好。因此，我们不能在此哈希表中插入 13。

**插入 7**：<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mn>7</mn><mo stretchy="false">)</mo></mrow></math> 是 7，被关键字 17 占据。因此，让我们应用双重散列，其方程为：<math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mi>i</mi><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> 其中 i=0 到 m-1。

**i=0**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>0</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>+</mo><mn>2</mn><mo>*</mo><mn>0</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>7</mn></mrow></math> 被占用。

**i=1**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>1</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>+</mo><mn>2</mn><mo>*</mo><mn>1</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>9</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>9</mn></mrow></math> 也不是免费的。值得注意的是，<math alttext="" display="inline"><mrow><mo stretchy="false">[</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mn>7</mn><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>*</mo><mn>3</mn><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>2</mn><mo stretchy="false">]</mo></mrow></math>。

**i=2**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>2</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>2</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>+</mo><mn>2</mn><mo>*</mo><mn>2</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>11</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>1</mn></mrow></math> 也不是自由的。

**i=3**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>3</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>3</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>3</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>+</mo><mn>2</mn><mo>*</mo><mn>3</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>13</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>3</mn></mrow></math> 也不是自由的。

**i=4**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>4</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>4</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>4</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>+</mo><mn>2</mn><mo>*</mo><mn>4</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>15</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>5</mn></mrow></math> 也不是免费的。

**i=5**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>5</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>5</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>5</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>+</mo><mn>2</mn><mo>*</mo><mn>5</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>17</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>7</mn></mrow></math> 也不是免费的。

**i=6**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>6</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>6</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>6</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>+</mo><mn>2</mn><mo>*</mo><mn>6</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>19</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>9</mn></mrow></math> which is also not free.

**i=7**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>7</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>7</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>7</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =(7+2*7)mod 10= 21mod10=1 which is also not free.

**i=8**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>8</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>8</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>8</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>+</mo><mn>2</mn><mo>*</mo><mn>8</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>23</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>3</mn></mrow></math> which is also not free.

**i=9**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>9</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> = <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>9</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>9</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>+</mo><mn>2</mn><mo>*</mo><mn>9</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>25</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>5</mn></mrow></math> which is also not free.

现在，我们不能将 i 的值增加到 1，因为 i 的范围是从 0 到 9。因此，i 的值不能超过 9。我们已经检查了 i 从 0 到 9 的所有可能的值。因此，我们不能在这个哈希表中插入 7。

**插入 22**：*h(22)* 是 7，被键 17 占用。因此，让我们应用双重哈希，其方程为：<math alttext="" display="inline"><mrow><msub><mi>h</mi><mi>i</mi></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mi>i</mi><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math>，其中 i=0 至 m-1。

**i=0**：<math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>0</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>0</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>+</mo><mn>7</mn><mo>*</mo><mn>0</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>7</mn></mrow></math>，已被占用。

**i=1**: <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo></mrow></math> =（<math alttext="" display="inline"><mrow><mi>h</mi><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>+</mo><mn>1</mn><mo>*</mo><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mi>m</mi></mrow></math> ⟹ <math alttext="" display="inline"><mrow><msub><mi>h</mi><mn>1</mn></msub><mo stretchy="false">(</mo><mi>x</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>7</mn><mo>+</mo><mn>7</mn><mo>*</mo><mn>1</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>14</mn><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>4</mn></mrow></math> ，这是自由的。值得注意的是，[ <math alttext="" display="inline"><mrow><mi>h</mi><mtext>′</mtext><mo stretchy="false">(</mo><mn>7</mn><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mn>22</mn><mo>*</mo><mn>3</mn><mo>+</mo><mn>1</mn><mo stretchy="false">)</mo><mi>m</mi><mi>o</mi><mi>d</mi><mn>10</mn><mo>=</mo><mn>7</mn></mrow></math>].

## 5.7 RSA

RSA（Rivest, Shamir, Adleman）于 1978 年推出，是第一个广泛采用的密码系统。RSA 遵循基于两个组件的公钥加密思想，即公钥和私钥。网络上的每个人都有自己的公钥和私钥对。公钥为网络上的所有人所知，用于加密消息并验证签名。相反，私钥只有接收者知道，用于解密发送的消息并创建签名。RSA 的应用包括数字签名和公钥加密。在 RSA 中，接收者的公钥用于加密消息，而接收者的私钥用于解密消息，如 图 5.13 所示。加密是将原始消息转换为称为密文的不可识别形式的过程，而解密是将加密消息转换回原始消息的过程。RSA 的过程包括 3 个步骤，即密钥生成、加密和解密。

### 5.7.1 密钥生成步骤：

+   选择变量 *p* 和 *q*，其中 *p* 和 *q* 都是大素数且 p≠q。RSA 的整个安全性取决于大素数的因数分解的难度。选择 *p* 和 *q* 不当会使 RSA 不够安全，并且容易受到不同攻击的影响。

+   计算 <math alttext="" display="inline"><mrow><mi>n</mi><mo>=</mo><mi>p</mi><mo>*</mo><mi>q</mi></mrow></math>，*n* 是公钥的一部分，并且应该足够大，以至于从中提取 *p* 和 *q* 是困难的。

+   计算 *ϕ*(n)=(p-1)(q-1)。*ϕ*(n)被称为欧拉函数。

+   接下来，生成公钥 *e*，使得 gcd(*ϕ*(n), e)=1 或者 *e* 应该与 *ϕ*(n) 互质；1¡e¡*ϕ*(n)。

+   最后，创建私钥 *d*，使得 d≡e-1mod*ϕ*(n)。

<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>n</mi><mo>,</mo><mi>e</mi><mo stretchy="false">)</mo></mrow></math> 都是 RSA 公钥的一部分，是公开可用的，而私钥包括 <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>n</mi><mo>,</mo><mi>d</mi><mo stretchy="false">)</mo></mrow></math>。

### 5.7.2 加密

假设发送者必须将明文消息 *M* 发送给具有公钥 <math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mi>n</mi><mo>,</mo><mi>e</mi><mo stretchy="false">)</mo></mrow></math> 的接收者。要加密消息，请使用：

密文= <math alttext="" display="inline"><mrow><msup><mi>M</mi><mi>e</mi></msup><mi>m</mi><mi>o</mi><mi>d</mi><mi>n</mi></mrow></math>。

### 5.7.3 解密

解密时，接收者使用其私钥如下：

明文= <math alttext="" display="inline"><mrow><msup><mi>C</mi><mi>d</mi></msup><mi>m</mi><mi>o</mi><mi>d</mi><mi>n</mi></mrow></math>

![图 5.13](img/fig5_13.jpg)

**图 5.13**

RSA 算法结构。

### 5.7.4 RSA 示例

**密钥生成**

+   假设 *p*=17，*q*=11。

+   计算 *n*；*n*= 17*11=187。

+   计算 *ϕ*(n)；*ϕ*(n)=(17-1)*(11-1)=160。

+   选择 *e* 使得 gcd(*ϕ*(n), e)=1；选择 *e*=7。

+   计算 *d* 使得 d≡e-1mod*ϕ*(n)；d*e≡1mod160 且 d¡160 ⟹ d=23 因为 23*7=10*160+1。

因此，公钥=(7, 187)

private key= (23, 187).tcolorbox

**关键点** 公钥密码系统遵循非对称属性，因为加密消息的人或验证消息上的签名的人不能解密消息或对消息上的签名进行签名。

## 5.8 椭圆曲线加密

通过椭圆曲线进行公钥密码学是另一种方法。ECC 是密码学中最强大的概念之一。ECC 用于身份验证，以及 SSL/TLS 上的安全网页浏览。流行的加密货币，如比特币和以太坊，使用椭圆曲线的概念。ECC 适用于密钥生成、数字签名和加密/解密服务。值得注意的是，与 RSA 相比，ECC 需要更小的密钥大小以提供相同的安全性。显然，更小的密钥大小更易于管理和使用。256 位 ECC 相当于 3072 位 RSA 算法的密钥大小。由于 ECC 实现了与 RSA 相当的安全性，并且需要更低的计算能力和电池使用量，因此 ECC 已广泛用于移动应用程序。ECC 的密钥生成算法使用了椭圆曲线方程的性质，如下所述：

椭圆曲线被定义为满足立方数学方程的一组点（参见图 5.14），即，

<math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><msup><mi>y</mi><mn>2</mn></msup><mo>=</mo><msup><mi>x</mi><mn>3</mn></msup><mo>+</mo><mi>a</mi><mi>x</mi><mo>+</mo><mi>b</mi></mrow></mtd></mtr></mtable></mrow></math>(5.4)

其中 <math alttext="" display="inline"><mrow><mn>4</mn><msup><mi>a</mi><mn>3</mn></msup><mo>+</mo><mn>27</mn><msup><mi>b</mi><mn>2</mn></msup><mo>≠</mo><mn>0</mn></mrow></math>

要绘制这样的曲线，我们需要计算每个*a*和*b*的组合 <math alttext="" display="inline"><mrow><mi>y</mi><mo>=</mo><mo>±</mo><msqrt><mrow><msup><mi>x</mi><mn>3</mn></msup><mo>+</mo><mi>a</mi><mi>x</mi><mo>+</mo><mi>b</mi></mrow></msqrt></mrow></math>。

![图 5.14](img/fig5_14.jpg)

**图 5.14**

椭圆曲线的示意图。

**椭圆曲线的性质**

+   根据 a 和 b 的值不同，椭圆曲线在平面上呈现不同的形状

+   所有椭圆曲线都关于 x 轴对称。例如，如果我们取<math alttext="" display="inline"><mrow><mi>a</mi><mo>=</mo><mn>27</mn></mrow></math>和<math alttext="" display="inline"><mrow><mi>b</mi><mo>=</mo><mn>2</mn></mrow></math>，那么对于<math alttext="" display="inline"><mrow><mi>x</mi><mo>=</mo><mn>2</mn></mrow></math>，<math alttext="" display="inline"><mrow><mi>y</mi><mo>=</mo><mo>±</mo><mn>8</mn></mrow></math>，即，<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mn>2</mn><mo>,</mo><mo>−</mo><mn>8</mn><mo stretchy="false">)</mo></mrow></math>和<math alttext="" display="inline"><mrow><mo stretchy="false">(</mo><mn>2</mn><mo>,</mo><mn>8</mn><mo stretchy="false">)</mo></mrow></math>是结果点。

+   任何非垂直线在曲线上最多交于三点。

+   椭圆曲线上的点形成一个群。适用于椭圆曲线上的点的群操作称为加法法则。要将曲线上的点 P 与另一个点 Q 相加，请使用以下规则：

    +   首先，用一条直线连接 P 和 Q。

    +   称此点为-R，其中这条直线与曲线相交。

    +   相对于 x 坐标的此点的镜像定义了点 P 和 Q 的加法，并在图 5.15 中用 R 表示。

![图 5.15](img/fig5_15.jpg)

**图 5.15**

椭圆曲线上的点的加法。

关键点

陷阱门函数*f*被定义为一个易于计算但其逆<mrow><msup><mi>f</mi><mrow><mo>−</mo><mn>1</mn></mrow></msup></mrow>难以计算的函数。

## 活动

### 多项选择题

1.  哪个加密/解密密钥只有交换秘密消息的各方知道？

    1.  公钥

    1.  私钥

    1.  安全令牌

    1.  电子签名

1.  哪个不是私钥的功能？

    1.  加密文本

    1.  认证

    1.  解密文本

    1.  以上皆非

1.  密码是什么？

    1.  加密算法

    1.  解密消息

    1.  加密消息

    1.  密钥

1.  密码哈希函数将任意块转换为……？

    1.  可变大小的字符串

    1.  固定大小的字符串

    1.  固定大小和可变大小的字符串都是

    1.  不能确定

1.  以下哪个是 CIA 三位一体的组成部分？

    1.  机密性

    1.  完整性

    1.  身份验证

    1.  可用性

1.  哈希函数的要求是什么？

    1.  单向的

    1.  雪崩效应

    1.  确定性的

    1.  以上所有

1.  密码分析是……

    1.  为了降低加密速度

    1.  为了增加加密速度

    1.  生成密文

    1.  为了找到加密算法中的不安全性

1.  数字签名是基于……？

    1.  公钥加密

    1.  私钥加密

    1.  区块链技术

    1.  以上都不是

1.  零知识证明的特性是什么？

    1.  完备性

    1.  声明

    1.  零知识

    1.  以上都不是

1.  以下哪种是冲突解决技术？

    1.  二次探测

    1.  ECC

    1.  DSA

    1.  以上所有

1\. b  2\. a  3\. c  4\. b  5\. c  6\. d  7\. d  8\. a  9\. a, b, c  10\. a

<hgroup>

# 6

# 区块链技术与技术基础

</hgroup>

## 6.1 区块链基础

区块链是一个不断增长的区块列表，结合了密码学和分布式计算，以提供去中心化、透明和强一致性支持。特别是，区块链技术正在取代现有的交易管理系统[112]。值得注意的是，在共享文档中传统的写作方式是用户 1 将文档发送给用户 2，用户 2 在接收到文档后用自己的内容更新文档，并将其发送回用户 1。然而，这种方法不允许双方同时在文档上写作。作为解决方案，通过由微软 Word 提供的 Google Docs，用户 1 和用户 2 都可以同时进行写作。尽管如此，这个 Google 文档平台是集中化的，涉及第三方。大多数传统的分布式数据库都是集中化的，复杂性很高，并且依赖于可信的数据库公司。

集中式架构具有一个中央协调系统，网络上的每个节点都连接到这个系统。网络中任何信息共享都必须涉及这个中央协调系统。尽管如此，集中式系统也有一些缺点。

+   单点故障: 如果系统或服务器崩溃怎么办。不幸的是，在中央系统崩溃的情况下，网络上的所有节点都会断开连接，所有操作都会终止。这种情况可能导致整个信息的丢失。因此，完全依赖单个服务器是不高效的。

+   瓶颈: 在交通量增加的情况下，瓶颈很常见。

+   单一攻击点: 由于存在单一中央权威，存在着单一攻击点的可能性。因此，这种类型的架构很容易遭受到拒绝服务攻击。

+   延迟: 由于集中式服务器通常位于用户远处的位置，因此访问数据的时间增加了。

+   更高的隐私风险：由于集中式架构涉及到一个可信赖的第三方，因此用户不知道用户信息如何与第三方安全保护。可信赖的第三方可能会与其他方分享用户的私人信息。

除此之外，还有其他架构支持信息共享，即分布式和分散式架构：

在分散式架构中，与单一的协调者不同，存在多个协调者，网络节点连接到任何一个协调者。因此，如果一个协调者节点发生故障，网络节点可以连接到任何其他协调者共享信息。分散化支持容错性，因为分散系统不太可能意外崩溃。而且，由于存在多个协调者，不存在单一攻击点的可能。另一方面，在分布式架构中，网络的所有节点参与计算，没有单一的权威机构。网络的所有节点相互协调，并共同参与信息共享过程。分散式系统实际上是分布式系统的一部分。在分散和分布式网络中，用户 1 和用户 2 都有自己的文档的本地副本，并且两个用户都可以同时编辑文档。

区块链是一个平台，为去中心化和分布式架构提供支持，网络节点可以在彼此之间共享信息。与客户端-服务器模型相反，区块链实现了数字 P2P 网络。在区块链网络中，通过互联网连接着多个节点，每个节点维护着全局表的本地副本。然而，这些本地副本应始终根据全局信息进行更新。具体来说，这些数据的本地副本称为公共账本。公共账本的一个常见例子是银行交易，而区块链的第一个流行用例是比特币网络。区块链比特币被称为去中心化的加密货币交换系统，它还共享分布式账本。许多其他区块链加密货币平台也相继推出，包括以比特币相同的公共模型为基础的以太坊，而像超级账本、瑞波这样的平台则属于一些许可的区块链。尽管区块链的分布式应用在许多其他领域中得到应用，包括医疗保健、物联网、智能电网等。区块链为不信任彼此且涉及信息共享或理性决策过程的多个参与方提供了一个去中心化的共同平台。这项技术提供了一种安全、透明且高度抗攻击的存储交易的有效方式。区块链网络确保了文档的一致性和同步性。存储在区块链上的任何内容都具有透明的特性，对其进行修改的任何人都要对其行为负责。此外，该网络的去中心化性质确保网络上的单个节点无法向链中追加无效的区块。在将交易添加到区块链网络之前，它需要由区块链网络上的所有参与者进行验证。在将新区块添加到区块链网络之前，它始终与前一个区块通过立即前一个区块的密码哈希进行链接。因此，密码链接确保了网络的完整性。由于每个区块都与前一个区块的哈希密码链接，所以区块链这个名字是可被捍卫的。如果任何一个区块被修改，攻击者需要修改所有后续的区块，这是相当困难的。

根据维基百科，区块链是一个不断增长的记录列表，称为区块，它们使用加密技术链接在一起。

区块链技术主要基于加密学和分布式账本技术的基础。具体而言，区块链利用哈希函数、ECC、数字签名和椭圆曲线数字签名算法（ECDSA）的概念来维护系统的完整性、机密性和不可否认性。分布式账本是一种数据库，它在去中心化网络的节点之间共享和同步。此外，分布式账本中的每一条记录都有时间戳，以实现文档的完整性。然而，在分布式环境中，网络参与者使用共识机制来就网络的单一状态达成共识协议。显然，共识机制能够降低欺诈交易的风险。

区块链挖矿是在交易被添加到网络之前验证交易的过程，矿工是负责验证并在网络中生成新区块的实体。一些具有一些特殊特性（每个区块链网络都不同）的特殊节点才被视为矿工。此后，挖出的区块在网络中广播，以便其他节点在最终纳入网络之前对其进行验证。每当进行新的比特币交易时，它首先被放置在一个交易池中。矿工不是验证单个交易，而是从交易池中收集一定数量的交易来形成候选区块。因此，候选区块是指由矿工创建但尚未添加到网络中的区块。可能会出现多个矿工同时或几乎在相同的时间内挖掘出具有完全相同或部分不同交易的区块的情况。然而，当两个区块同时被挖出时，有可能只有一个矿工的区块上面有更多的区块。如果出现多个有效区块到现有链的情况，那么只接受最长的子分支并继续进行；而未被接受的区块称为孤立区块，该路径称为分叉。换句话说，孤立区块是由于缺少前任而没有与主分支相关联的区块。此外，如果有两条长度相同的不同链，则接受被更多数量的矿工广播的链。这些未经验证的区块中的交易被送回到交易池。在这种情况下，矿工的努力变得无用，因为已挖出的区块变得未记录。

### 6.1.1 区块链技术的特性

+   去中心化：区块链技术不依赖于集中式系统或任何治理机构来执行所有交易。相反，网络由网络节点控制，使其去中心化。网络上的每个节点都有其更新的共享账本副本。此外，它解决了单点故障的问题。

+   更好的安全性：网络安全被定义为防止和从网络攻击中恢复的能力。区块链技术提供了更好的安全性，因为不存在任何系统失败的机会。区块链采用的加密系统为用户提供了保护。区块链技术受欢迎的另一个原因基本上是其处理个人隐私威胁的能力。所有交易都经过验证，修改这些交易是相当困难的。

+   不可变性：不可变账本是区块链系统的主要优势。不可变性意味着网络上的数据无法更改或更改。区块链存储交易的永久记录。一旦区块被验证并添加到网络中，就无法修改或删除。此外，去中心化的特性促进了可伸缩性和鲁棒性。集中化架构可能受到篡改，并需要对第三方的信任来维护完整性。

+   匿名性：区块链提供了匿名性，因为节点在网络上是以其公钥而非身份来识别的。因此，节点的身份被保持私密。

+   透明度：网络上的任何节点都可以审计交易，每个节点都可以访问相同的通用账本。网络中的每个数据状态和每个更新状态对节点都是可见的。

+   冗余性：由于分布式账本的副本存储在网络上的每个完整节点上，因此区块链具有固有的冗余性。

+   效率：所有交易都通过预设的程序自动执行。因此，区块链技术降低了劳动成本，并提高了效率。

### 6.1.2 什么构成了区块链的一个区块？

区块链中的第一个区块称为创世区块，该区块没有任何前一个区块。为了确保区块链网络的正确性，所有网络参与者都应该有相同的创世区块。创世区块的前一哈希值为零。区块链的结构包括一系列区块，每个区块包含数据和元数据的交易。区块中的数据包含网络参与者生成的交易，而区块以安全的方式保存交易，以防篡改。交易是由特定协议允许的原子事件或最小的构建块。例如，在比特币区块链中，交易是用户的支付。另一方面，元数据包含有关区块的信息，包括父区块哈希值、时间戳等。这些信息性的元数据由矿工或网络的其他节点用于验证一个区块或将一个区块附加到区块链上。链式区块的结构由图 6.1 表示。区块的元数据存储在区块头中，包括以下字段：

+   版本：版本号用于跟踪区块链节点使用的协议升级。

+   时间戳：它指定了区块的创建时间。

+   随机数：它是一个随机数，用于解决工作量证明（PoW）密码难题，如式 6.1.2 所示。

    <math alttext="" display="block"><mrow><mtable columnalign="left"><mtr columnalign="left"><mtd columnalign="left"><mrow><mi>S</mi><mi>H</mi><mi>A</mi><mo>−</mo><mn>256</mn><mo stretchy="false">(</mo><mi>S</mi><mi>H</mi><mi>A</mi><mo>−</mo><mn>256</mn><mo stretchy="false">(</mo><mi>P</mi><mi>r</mi><mi>e</mi><mi>v</mi><mi>i</mi><mi>o</mi><mi>u</mi><mi>s</mi><mi>b</mi><mi>l</mi><mi>o</mi><mi>c</mi><mi>k</mi><mi>h</mi><mi>a</mi><mi>s</mi><mi>h</mi><mo>|</mo><mo>|</mo><mi>T</mi><msub><mi>x</mi><mn>1</mn></msub></mrow></mtd></mtr><mtr columnalign="left"><mtd columnalign="left"><mrow><mo>|</mo><mo>|</mo><mi>T</mi><msub><mi>x</mi><mn>2</mn></msub><mo>|</mo><mo>|</mo><mn>.......</mn><mo>|</mo><mo>|</mo><mi>T</mi><msub><mi>x</mi><mi>n</mi></msub><mo>|</mo><mo>|</mo><mi>n</mi><mi>o</mi><mi>n</mi><mi>c</mi><mi>e</mi><mo stretchy="false">)</mo><mo stretchy="false">)</mo><mo><</mo><mi>D</mi><mi>i</mi><mi>f</mi><mi>f</mi><mi>i</mi><mi>c</mi><mi>u</mi><mi>l</mi><mi>t</mi><mi>y</mi></mrow></mtd></mtr></mtable></mrow></math>(6.1)

+   难度/目标值：这是 PoW 算法用于解决挖矿过程的。要将一个区块添加到区块链网络中，它必须生成一个有效的哈希值，难度值用于完成这个任务。

+   上一个区块的哈希值：如前所述，区块链的每个第 n 个区块都存储前一个区块，即第 (n-1) 个区块的哈希值。为了计算第 (n-1) 个区块的哈希值，需要将第 (n-1) 个区块的所有头部字段集体哈希两次。

+   Merkle 树：它包含 Merkle 树根的值，稍后在下一章节详细解释。它基本上是一个树形结构，其中叶节点包含文档的哈希值，每个中间节点包含左右子节点的哈希值。正如在 图 6.2 中所示，有 8 个交易，即 t1、t2、……、t8。Merkle 树的叶节点包含这些交易的直接哈希值，然后第 1 层具有中间节点，其左右子节点的哈希值（即，获取的哈希值再次成对计算以计算下一级别的哈希）。此哈希将递归计算，直到获得单个根哈希。

![图 6.1](img/fig6_1.jpg)

**图 6.1**

区块链的结构。

**关键点** 强制字段是交易、Merkle 根哈希和上一个区块的哈希，每个区块链网络都使用这些字段，其余字段特定于特定的区块链应用程序。

![图 6.2](img/fig6_2.jpg)

**图 6.2**

Merkle 树的结构。

除此之外，Merkle 哈希树还用于成员身份验证。值得注意的是，为了验证任何给定交易的成员身份，验证者不需要拥有完整的 Merle 树，而仅仅(log n)个数据就足够了，其中 n 是树中节点的总数。由于每个节点都可以访问区块头，所以 Merle 哈希树的根值可以从那里下载。假设用户 A 拥有块的 Merkle 树根节点，而用户 B 想要向用户 A 证明交易 t4 在块中。（参见 图 6.2）。为了实现这一点，用户 2 必须向用户 1 提供树路径中与 t4 相关的节点的一些兄弟节点，以便用户 A 可以重新计算树的根哈希，并将其与从块中下载的哈希进行匹配。例如，为了验证交易 t4 是否存在于块中，用户 2 实际上必须向用户 1 提供 c、a' 和 b''，以及交易 t4 的哈希值。知道 c 和 a 后，可以计算出 b'，而 b' 与 a' 结合后可以计算出 a''，最终可以使用 a'' 和 b'' 计算出根哈希。事实上，用户 2 甚至可以仅通过证明 t4 的哈希值而无需透露其内容就证明 t4 存在于块中。

因此，即使在 Merkle 树中有大量的区块的情况下，任何元素的成员身份也可以在相对较短的时间内证明。只需拥有顶级节点的哈希值，就可以轻松地遍历到任何叶节点，以检查它是否被篡改。

**关键点** 使用 Merkle 树，任何交易的成员身份都可以在 O(log n) 的时间和空间复杂度内进行验证。

### 6.1.3 比特币基础知识

比特币被视为第一个完全功能的数字货币。它完全执行了一个无需任何中央金融机构的 P2P 银行系统 [160]。比特币区块链网络是一个用户之间可以发送或接收加密货币的网络。它属于公共区块链，世界上的任何人都可以成为比特币网络的一部分。在这里，交易是网络中一个节点向另一个节点转移加密货币。区块链网络上的每个注册节点都有一对公钥和私钥，保存在该人的比特币钱包中。此外，比特币钱包地址从不带有人的姓名或身份。基本上，钱包地址是用户使用的公钥的数学对应。因此，使用比特币地址可以维护网络的匿名性。值得注意的是，用户可以拥有多个地址。假设用户 A 想向用户 B 转移一些比特币。拥有用户 B 的钱包地址的任何人都可以将比特币转入其账户，但是，仅需要用户 B 的公钥才能释放资金。为了实现这一点，用户 A 将创建一个指定用户 A 想要转移的金额和用户 B 地址的交易。接下来，用户将签署交易并在网络中广播此交易。要创建数字签名，取交易的哈希并使用发送方的私钥进行加密。网络中的任何人或特定的矿工都可以使用用户 A 的公钥验证此交易的完整性、认证性和不可否认性。值得注意的是，当用户向另一个地址发送比特币时，该用户的钱包创建一个交易输出，其中包含要转账的另一个用户的地址，并且此交易记录在区块链网络上，发送者的比特币地址作为交易输入。另一种方式，在多个交易的情况下，所有总硬币价值将被加起来，并且可以由新交易的输出使用。例如，在 图 6.3 中，支付者 B 通过使用自己从交易 1 收到的硬币签署了一个交易 Y，并添加了自己的公钥和受益者 C 的地址。网络上的任何人都可以使用 B 的公钥来验证交易，并确保 B 花费了正确的硬币。然而，要使网络的其余部分接受任何交易，需要验证交易块，并且验证节点的矿工必须在块中包含 PoW。在这里，矿工是具有良好的计算能力和资源的特殊节点。值得注意的是，在比特币网络中，区块大小不能超过 1 MB，以实现快速传播。

![图 6.3](img/fig6_3.jpg)

**图 6.3**

比特币交易的图示。

PoW 是由矿工生成的密码学难题哈希。特别是，它是比特币共识算法。 PoW 和挖矿的概念使得修改交易在计算上变得不切实际。在 PoW 中，基本上，矿工必须找到一个随机值，使得区块的哈希具有特定的哈希值。第一个解决难题的矿工从网络中获得奖励的激励。网络中的所有其他节点验证矿工挖掘的区块。要将区块添加到比特币网络中，超过 51%的网络节点应批准该区块。因此，攻击区块链网络的唯一方法是当攻击者控制 51%的哈希算力时。该算法的详细信息在接下来的部分中解释。

比特币另一个受欢迎的原因是它解决了双重支付的问题。双重支付是指同一比特币被用于多笔交易的问题。例如，用户 A 有 100 个比特币，用户 A 试图将相同数量的 100 个比特币同时发送给用户 B 和用户 C。时间戳和分布式分类账的属性确保了比特币的双重支付。tcolorbox

**要点** 比特币地址是随机数，可能会出现两个不同的用户最终创建相同的地址并导致冲突的情况。在这种情况下，地址的原始拥有者和冲突的拥有者都可以花费发送到该地址的比特币。

**多重签名交易：** 这是一种由多个用户签名的交易类型，它从多重签名地址转移资金。如果有多个人被指定来监管比特币的所有权，则使用这种类型的交易。为了附加这样的比特币，每个人或他们中的大多数人都必须签署交易。这意味着使用多个私钥创建数字签名。

## 6.2 区块链的类型

区块链的主要应用是执行安全交易。然而，根据用户的需求，区块链网络可以以多种方式实现：

+   公共区块链：公共区块链网络是一个无需许可的系统，任何具有互联网访问权限的节点都可以参与网络。在这里，网络的任何用户都可以访问记录、验证、验证交易并执行挖矿任务。公共区块链网络中的参与者越多，它就越安全，因为块会由更多的网络参与者验证和验证。比特币、以太坊、莱特币、恒星、达世币都是公共区块链的例子。

+   私有区块链：相反，私有区块链由组织或企业拥有，参与者受限，只允许经过身份验证的用户。实际上，私有区块链是公共区块链的限制版本。私有区块链用于私有组织存储敏感信息。新用户无法在没有网络邀请的情况下加入网络。邀请程序涉及使用条件，新用户必须满足条件才能加入。与公共区块链相比，私有区块链更快。值得注意的是，私有区块链相对于公共区块链具有集中化特性。Hyperledger、multichain、Corda 是私有区块链的流行示例。高度可定制性、更好的访问控制、更好的可扩展性是私有区块链的一些优点[47]。

+   联盟区块链：这种类型的区块链被视为半私有系统。显然，它不是一个公共网络，而是一个受许可的网络。然而，不是单一组织进行管理，而是多个组织共同管理网络。这种类型对于多个组织在同一行业运营的情况非常有益。在这里，只有少数被选中的节点有权监督共识机制并授权交易。与公共区块链相比，联盟区块链提供更快的速度。此外，这种区块链类型不会面临可扩展性问题。Quorum 是这一类别下的一个流行例子。

上述讨论的区块链类型在表格形式中的差异在表 6.1 中讨论。

**表格 6.1**

区块链类型的差异。

| 区块链类型 |
| --- |
| 特征 | 公共 | 私人 | 联盟 |
| 无需许可 | 是 | 否 | 否 |
| 阅读权限 | 任何人 | 仅邀请用户 | 取决 |
| 写入权限 | 任何人 | 已批准参与者 | 已批准参与者 |
| 所有权 | 无 | 单一实体 | 多个实体 |
| 交易速度 | 慢 | 快 | 快 |
| 中心化 | 否 | 是 | 部分 |

## 6.3 区块链应用

由于其分布式、不可变和可信任的特性，区块链技术对所有交易都有各种应用。不仅金融部门，区块链技术还有潜力革新商业、工业、教育部门等领域。[182]的作者建议，区块链应用的增长可以分为三个阶段，即区块链 1.0、区块链 2.0 和区块链 3.0。区块链 1.0 包括使用加密货币作为点对点支付系统。区块链 2.0 包括智能合约、智能财产和简单现金交易的去中心化应用程序。区块链 3.0 则涵盖超越金融和加密货币的应用，如医疗保健、治理、农业和智能电网等[49]。

+   教育：区块链的一个值得一提的应用领域是教育部门。与金融类似，教育部门已经利用区块链来确保学生数据在未来几年内的安全性。由于区块链能够高效地跟踪信息，大学和学校的图书馆信息服务可以实施区块链技术。一些大学和研究机构已经利用区块链来支持课程学习成果的学位管理和评估。另一个用途是基于区块链网络上存储的透明记录奖励学生的成功和成就。例如，尼科西亚大学是第一个使用区块链管理来自大规模在线开放课程（MOOC）平台的学生证书的地方[170]。除此之外，区块链技术有助于减少学生的欺诈学位。使用区块链，所有学位和证书都以数字方式存储在区块链网络上，无需任何中介来验证它们。此外，拼车服务也可以使用区块链来组织拼车服务，这肯定会减轻公共交通的负担。

+   健康医疗：大多数情况下，现有的医疗系统由中央机构维护。因此，患者生成的所有数据可以被这些第三方访问，而无需患者的同意，这引发了隐私问题。为解决这一问题，近年来区块链技术在医疗网络中得到广泛应用，用于各种应用，如数据管理、数据共享、数据存储、数据分析和访问管理系统。在健康领域中的首要用例是改进和确保医疗记录管理[208]。通过区块链，由物联网传感器测量的信息，如体温、血压、心率和脉搏率，可以在区块链网络上安全透明地共享。患者现在可以控制和检查要与医生或其他医疗人员共享的信息内容和数量。另一个用例是验证针对医疗保健融资任务的声称交易。文献支持许多将区块链与医疗系统集成的工作，例如[102]，[97]。

+   投票系统：在一个民主国家中，维护选举系统的安全是国家安全的重要问题。如今，政府采用电子投票机来成功实现投票机制。值得注意的是，这些电子投票系统是基于一个中心化网络的，一切都由可信赖的第三方处理。然而，这种系统存在着物理安全、隐私和缺乏透明性的问题。重要的是，这类系统的主要关注点之一是防止数据库篡改。通过利用区块链和智能合约的基础知识，可以创建一个透明民主的安全电子投票系统。利用 SHA-256 哈希函数和利用密码学将当前块链接到前一个块可以防止对数据库进行任何修改。此外，数字签名的使用确保了系统的可靠性。此外，区块链支持的匿名概念确保选民可以提交他们的选票，而无需担心身份泄露。

+   智能电网：为了设计一个智能城市物联网基础设施，需要一个智能化和自动化的电力分配系统。在这个背景下，智能电网在许多方面革命了能源行业。智能电网旨在建立一个能够最小化能源浪费的自动化电力基础设施。尽管在现有文献中，智能电网实用程序由一个中央第三方提供服务，该第三方平衡用户的电力负载和付款。这个中央管理机构存储了与电力生成、消耗和转移相关的所有信息。然而，由于时间消耗更多、单点故障增多以及分布式资源数量增加，集中式管理不再有效。通过区块链，不同的电力实用程序可以在没有第三方的情况下交换能源并进行支付。所有涉及的交易在经过所有网络参与者的验证后都存储在公开分布式账本上。每个网络参与者都存储所有记录和能源交易，从而确保网络上的信任和透明度。与此同时，由于对单点故障的抵抗力，通过将区块链与智能电网集成，可以最小化 DDoS 攻击。此外，消除第三方可以降低交易成本。此外，网络参与者之间的互连实现了 P2P 信息共享，实现了自动调度。此外，可以利用区块链实现电费的自动交付。因此，区块链实现了自我参与、安全支付、电力分配和生成的透明度、灵活的需求响应管理、P2P 能源交易和实时定价数据。

+   区块链技术的另一个潜在应用场景是发展智能交通系统（ITS）或自动驾驶汽车。随着汽车工业、计算技术和设备的快速增长，ITS 的发展越来越受欢迎。然而，ITS 的不同传感单元、路侧单元（RSU）和基站（BS）采集的信息通常存储在基于云的平台上，因此面临着由于集中化而带来的安全和隐私风险。ITS 需要保护和验证数据以做出实时决策。区块链提供可信赖的数据，整个网络共同贡献于数据验证和验证。通过其去中心化特性，区块链可以促进自动运输系统中车辆和 RSU 之间的信任通信。此外，分布式数据验证机制确保了不可变和可追溯的分布式分类账，有助于建立 ITS 的 P2P 资金转移安全财务系统。对于电动汽车（EV）和充电站之间的能源交易，区块链提供了安全的支付处理和交易管理[155]。同样，收费支付可以通过区块链实现标准化的收费。此外，拼车服务可以利用区块链进行安全支付和显示透明信息[98]。此外，保险合同可以存储在区块链网络上，并可以部署智能合同来采取行动来要求资金并检测任何合同违约。此外，借助智能合同功能，海关清关可以更快速和更有效，从而减少了在检查点的处理时间[99]。

## 6.4 智能合同

智能合约是在分布式环境中实现的自动且不可逆转的应用程序。除了完全访问代码的开发者外，没有其他人可以编辑或修改智能合约的执行行为。智能合约能够高效管理数字文档，因为它们是自执行和自验证的[95]。实际上，智能合约是一段代码，用于建立多方之间的协议，在执行之前有一些条件需要满足。每个参与方必须根据协议履行自己的承诺。例如，一个针对特定日期和时间付款的智能合约，意味着在特定日期和时间到达时，预定义的条件得到满足，付款会自动转账到接收者的账户。因此，消除了对可信第三方的需求。当部署在区块链环境中时，它利用了区块链技术的属性（如- 不可逆性、防篡改、透明性等）。智能合约的字节码对区块链网络上的所有人都是可见的。值得注意的是，一个智能合约可能需要另一个智能合约的结果。智能合约不仅用于支付交易，还用于执行许多不同的流程，例如保险、供应链管理、抵押贷款、房地产、投票等。随着物联网技术的普及，智能合约被用于实现机器对机器的交互。

目前，智能合约的最大平台是以太坊。Solidity 是一种面向对象的高级语言，专门用于实现智能合约。Solidity 受到常见语言的启发，如 C++、Python 和 javascript，具有继承、库等功能。Solidity 的编译器将代码转换为 EVM 字节码。执行智能合约的基本步骤为：

+   合同条款最终确定后，会编写编程代码，指定预定义的条件和结果。

+   将智能合约部署到区块链网络，并在网络的所有参与者之间复制它。

+   一旦条款和条件得到满足，合同就会执行，结果就会触发。

值得注意的是，比特币网络是第一个在区块链中使用智能合约概念的网络，以一种方式使得一个节点可以按照一些规则将硬币转移到另一个节点。此外，只有在满足一些预定义条件时，网络参与者才会验证交易。相比之下，以太坊用一种允许开发人员编写自己程序代码的语言取代了比特币的限制性语言。这意味着，使用以太坊，开发人员可以编写自己的程序。

## 6.5 区块链问题

区块链技术有潜力颠覆广泛的行业，但它面临着一系列挑战，如图 6.4 所示。然而，随着时间的推移，文献介绍了许多改进措施来消除这些挑战。

+   **存储**：区块链的首要问题是数据存储，因为网络上的每个完整节点都有分布式账本的副本。显然，这个不断增加的数据存储库很难处理。在这种情况下，应该鼓励研究机制，如侧链或子链[32]。

+   **可扩展性**：另一个问题是公共区块链网络规模的增长。随着交易数量的增加，区块链的大小也变得更大。例如，比特币区块链当前的大小约为 269 GB [9]。将网络上发生的所有交易存储起来以进行验证是很重要的。因此，区块链中存在着可扩展性问题。此外，共识协议也影响着网络的可扩展性。另外，随着网络规模的增加，将需要更多的资源，因此系统的容量规模将会降低。由于高可扩展性，区块链中的交易执行可能变得缓慢。分片是一种改善可扩展性和增加事务吞吐量的新方法。它是一种分区方法，将参与者的子集分组成较小的网络，只负责处理其分片的交易。这样，每个分片都将有其独特的智能合约集，将易于执行。

+   **高计算量**：市场上大多数区块链消耗大量能源，因为它们基于比特币基础设施并使用 PoW 作为共识算法。该协议涉及复杂的数学难题，并需要高计算能力进行验证。然而，这种计算密集型任务对于在区块链中生成新的区块至关重要。此外，该算法涉及消耗大量能源资源。解决数学难题消耗的能量相当于 2020 年丹麦的年电力消耗量 [10]。因此，区块链可能对环境造成昂贵的代价。为了解决 PoW 所面临的能源挑战，已经引入了许多其他共识算法，包括股权证明（PoS）、身份证明（PoI）等。

+   **缺乏标准**：根据[11]的研究，区块链技术没有被广泛采用的一个原因是用户之间缺乏信任。缺乏标准可能会在用户之间产生争议。此外，缺乏标准化会导致区块链网络中大量节点之间的互操作性问题。市场上有多个区块链项目，具有不同的协议、隐私措施、共识算法和编码语言。此外，这些不同项目导致的不统一性也给安全解决方案带来了一致性问题。此外，区块链网络包括公共、私有和财团等多种类型，每种类型都有其优缺点。因此，不同类型的区块链由于互操作性问题而无法通信。区块链的标准化可以帮助降低成本和互操作性问题。在这方面，市场上有一个名为[12]的项目，它依赖智能桥接架构来支持通用互操作性。

+   **延迟**：交易验证是分布式共识的另一个属性。一个区块中的交易总数以及区块之间的生成时间对交易的确认时间有显著影响。这在区块链网络中引入了延迟或延迟，因为验证和验证块时的数据量大且网络规模不断增大。因此，区块链网络的每秒交易数较慢。解决这个问题的一种方法是在移动区块链网络中使用边缘计算，特别是采用 PoW 共识机制。然而，这种解决方案面临着将有限的边缘计算资源分配给不同网络中的各个矿工的困难。比特币-NG《77》，莱特币《13》，幽灵《176》是一些旨在改善网络延迟的比特币网络的变体。

+   **隐私泄露**：区块链另一个值得一提的问题是隐私泄露。在区块链中，隐私意味着可以在不泄露身份信息的情况下执行交易。相比之下，比特币默认不支持隐私，因为比特币的关键特性是透明的。网络上发生的所有交易都可以被任何人检查、追踪和审核。《139》的作者总结道，区块链无法实现交易隐私，因为每个公钥对应的交易价值都是公开可见的。除此之外，轻量级客户端存在隐私问题，因为全节点拥有轻量级客户端感兴趣的钱包地址的所有信息。

    为了增强数据隐私，区块链网络的数据可以进行加密。例如，[122]所提出的模型以加密形式存储交易信息。该模型中的编译器将加密形式的代码翻译成可识别的形式。同样，Enigma 项目在[1]中将数据分成分布在网络中的片段，以确保没有节点可以访问数据。提供数据隐私的另一解决方案是将私人和敏感数据存储在链外，这种机制被称为链外解决方案。这种系统更适合于高度敏感的数据，例如医疗保健或军事应用。

+   **安全威胁**：除了隐私问题外，另一个挑战是区块链网络面临的安全威胁。区块链系统中可以发动许多安全攻击，包括肖比尔攻击、路由攻击、DoS 攻击、日食攻击等。读者可以参考[148]，[133]等进一步了解这些攻击的详细信息。然而，最流行的攻击是多数派或 51%攻击。在比特币网络中，任何拥有超过 51%的计算能力的网络参与者可以比其他人更快地发现随机数，这意味着节点有权决定哪个区块是可接受的。大多数在有限用户之间集中的共识算法容易受到多数攻击。如果区块链节点控制了超过 51%的散列（挖矿）功率，就会发生这种攻击。要解决区块链中的安全问题，需要使用最新的机器学习技术对区块链数据进行数据分析[185]，[63]，[14]。

+   **匿名性问题**：匿名性意味着发送者不可识别性。如今，用户在保持用户匿名的同时进行用户身份验证也是用户的另一个要求[39]。按设计，区块链支持匿名性，因为钱包地址与个人身份之间没有直接链接。区块链不使用真实身份，而是使用伪名，而公钥大多是区块链网络的伪名。不幸的是，这种不可追踪的特性激励人们进行非法网络购买。然而，使用公共地址在一定程度上可以保护匿名性。一旦一个人与另一个人进行交易，它就会公开其公共地址。由于区块链记录了每个钱包的整个历史记录，因此通过公共地址可以检查所有以前的活动、钱包余额等。此外，任何一方都可以拦截交易以查找原始 IP 地址。显然，这个公共分类账通过简单分析交易来轻松地将钱包地址与可识别的名称进行关联。解决这个问题的一种方法是使用虚拟专用网络（VPN）技术，该技术使用其他人的互联网连接。另外，对于每一笔交易使用一个新的比特币地址也可能有所帮助。例如，Monero 是另一种加密货币，每次新交易都使用不同的秘密地址。另一种流行的预防技术是洋葱路由，它模糊了节点上线的 IP 地址。在这方面，Tor[15]是实现洋葱路由的开源平台。该软件还有助于隐藏节点的 IP 地址。

![图 6.4](img/fig6_4.jpg)

**图 6.4**

区块链技术存在的问题。

### 6.5.1 IPFS：去中心化数据存储问题的解决方案

正如上文所讨论的，将大文件存储在区块链上是具有挑战性的。在存储容量的背景下，值得一提的是星际文件系统（Inter Planetary File System，IPFS）[16]。IPFS 网络适用于共享需要大带宽上传/下载的大文件。IPFS 是一个去中心化的 P2P 分布式文件系统，用于存储共享文件。IPFS 是一种高效的存储方式，因为它消除了数据的重复。在一个 P2P 连接的 IPFS 中，如果一个节点崩溃了，其他节点仍然可以提供所需的文件。这个分布式文件系统将所有计算设备连接到同一个文件系统下。IPFS 基本上是超文本传输协议（HTTP）的替代品，用于访问互联网上的内容。在 IPFS 中，网络上的文件托管在一个去中心化的服务器上，这意味着内容不是存储在单个系统上，而是托管在互联网上分散的多个节点上。IPFS 节约了约 60% 的网络带宽。与从单台机器下载单个文件的 HTTP 不同，IPFS 同时从多个分散的机器上下载文件的多个部分。

与将文件按其在 IPFS 上存储的名称命名不同，该系统通过它们的加密哈希值来引用文件。文件的加密哈希也被用作地址。这个哈希表示一个根对象和路径中可以找到的所有其他对象。特别是，在 HTTP 层使用内容寻址的概念，这意味着不是通过位置引用文件（基于位置的引用模型支持集中化），而是通过内容本身的任何表示来寻址。IPFS 依赖于分布式哈希表（DHT）来存储文件。DHT 是一个类似字典的接口，用于存储在网络上分布的节点上的数据。网络上的节点使用一种称为 bitswamp 的机制来在节点之间交换数据。

当新文件添加到 IPFS 网络时，IPFS 使用其内容和节点 ID 生成文件的多哈希地址。要访问特定文件，IPFS 会查询具有匹配哈希的文件的网络。计算文件的加密哈希后，向网络的节点询问内容与该哈希匹配的对等节点。接下来，直接从具有所需数据的节点下载内容。因此，IPFS 网络上的任何节点都可以通过其内容 ID 和匹配该 IP 的节点查找特定文件。

IPFS 模型可以与区块链模型集成，例如比特币和以太坊，因为这两个系统具有相似的结构。IPFS 不是将实际值存储在区块链上，而是简单地将文件的哈希存储在区块链上。此外，使用这些哈希可以找到文件的实际位置。

图 6.5 展示了作者讨论的一种使用 IPFS 的数据共享模式[152]。首先，文件的所有者将其上传到 IPFS，包括文件的元数据。其次，IPFS 生成文件的哈希并返回给所有者。第三步，所有者在智能合约中查找提供加密/解密服务的节点。接下来，所有者将 IPFS 哈希分成 *k* 个部分，对其进行加密，最后将其存储在区块链网络上。

![图 6.5](img/fig6_5.jpg)

**图 6.5**

在 IPFS 上的数据共享。

## 6.6 区块链的 Python 实现

我们使用了包括在 anaconda 中的 Scientific Python Development Environment (Spyder) 来实现区块链。它能够进行编辑、调试和交互式测试。除此之外，我们还使用了 Flash 和 Postman 应用程序成功地创建了一个区块链网络。Flask 是一个用于构建 web 应用程序的 web 框架，它可以在没有外部库依赖的情况下工作。要安装 flask，请使用以下命令：<math alttext="" display="inline"><mrow><mi>p</mi><mi>i</mi><mi>p</mi><mi>i</mi><mi>n</mi><mi>s</mi><mi>t</mi><mi>a</mi><mi>l</mi><mi>l</mi><mi>F</mi><mi>l</mi><mi>a</mi><mi>s</mi><mi>k</mi><mo>=</mo><mo>=</mo><mn>0.12.2</mn></mrow></math> Postman 是一个 HTTP 客户端，用于通过向 web 服务器发送请求然后收到响应来测试应用程序接口（API）。它提供了一个简单易用的界面，允许任何人通过服务器在线加入区块链网络。

![](img/list6_1.jpg)![](img/list6_2a.jpg)![](img/list6_2b.jpg)![](img/list6_3.jpg)![](img/list6_4.jpg)

接下来，我们将创建一个函数来检查区块是否有效。为了检查区块的有效性，需要检查两个主要点，即

+   每个区块的证明应在加密哈希中具有 4 个前导零。

+   Previous hash 字段的值应该与区块的上一个哈希值完全相同。

![](img/list6_5.jpg)![](img/list6_6.jpg)

已创建 blockchain 类。此外，我们将使用 flask 创建一个 web 应用程序，以便与区块链进行交互。

+   首先，我们将通过创建一个 flask 类对象来创建基于 flask 的 web 应用程序。实际上，我们将通过 flask 与区块链进行交互。

+   接下来，我们将创建一个 blockchain 类的实例。

+   然后，我们将发出 GET 请求来通过解决 PoW 问题来挖掘一个区块。

+   接下来，我们将再次进行 GET 请求以获得区块链。

![](img/list6_7.jpg)![](img/list6_8.jpg)

现在，我们将通过基于 flask 的应用程序发出新请求来挖掘新区块。为此，路由装饰器将用于告知 flask 哪个统一资源定位器（URL）应该触发我们的函数以挖掘区块。在 URL 中，我们必须指定其他参数，即请求的方法。它可以是 GET 或 POST。GET 将获取一些信息，POST 将创建某些内容，例如，交易。

![](img/list6_9.jpg)

现在，我们将创建第二个 GET 请求，以在用户界面 postman 应用程序中显示完整的区块链。

![](img/list6_10.jpg)

最后，现在我们将从我们的 flask 应用程序运行区块链应用程序。我们将使用 postman 发出挖掘区块和获取链请求以检查链的实际状态。为了实现这一点，从 flask 类的 app 对象中，我们将调用 run 方法，该方法接受两个参数，即主机和端口。从 flask 文档中，我们可以检查此应用程序正在 http://127.0.0.1.5000/ 上运行。此 URL 将输入 postman 中。此外，文档中指定，要使服务器公开可用，请设置 host=0.0.0.0 并将端口设置为 5000。

![](img/list6_11.jpg)

编写完代码后，在编辑器上执行代码。从图 6.6 可以看出，应用程序成功在 http:\ \0.0.0.0\ 上运行。现在，我们将使用 postman 应用程序发出 GET 请求。在 postman 应用程序中，我们必须输入请求 URL，并选择请求类型为 GET，如图 6.7 所示。要挖掘区块，我们必须使用 mine_block 请求，并且要获取区块链状态，我们必须使用 get_chain 请求。

![图 6.6](img/fig6_6.jpg)

**图 6.6**

区块链应用程序。

![图 6.7](img/fig6_7.jpg)

**图 6.7**

使用 postman 的区块链应用程序说明。

首先，我们将使用 get_chain 请求，可以看到网络中只有一个区块，即创世区块，因为我们还没有挖掘任何区块。参见 图 6.8。这个创世区块的索引为 1，previous_hash=0，proof 为 1。

![图 6.8](img/fig6_8.jpg)

**图 6.8**

使用 postman 的区块链应用示例。

现在，我们将挖掘网络的第一个区块，索引为 2，如 图 6.9 所示。该区块的证明值为 533，这意味着编码字符串 <math alttext="" display="inline"><mrow><msup><mrow><mn>533</mn></mrow><mn>2</mn></msup><mo>−</mo><msup><mn>1</mn><mn>2</mn></msup></mrow></math> 的密码学哈希以四个前导零开始。

![图 6.9](img/fig6_9.jpg)

**图 6.9**

使用 postman 的区块链块挖掘示例。

在挖出第一个区块后，让我们通过 get_chain 请求来检查区块链的状态。参见 图 6.10。

![图 6.10](img/fig6_10.jpg)

**图 6.10**

使用 postman 的区块链 get_chain 示例。

## 活动

### 多项选择题

1.  P2P 的全称是什么？

    1.  产品对产品

    1.  点对点

    1.  梨对产品

    1.  产品对对等

1.  以下哪项定义了矿工？

    1.  一种区块链类型

    1.  加密文本的人员

    1.  用于存储数据的计算机

    1.  验证区块链交易并将其存储在全球总账上的人员

1.  用于定义区块链分裂的术语是什么？

    1.  分叉

    1.  挖矿

    1.  随机数

    1.  创世

1.  Nonce 的用途是什么？

    1.  作为哈希函数的功能

    1.  防止双重支付

    1.  防止 51% 攻击

    1.  以上都不是

1.  创世区块是什么？

    1.  区块链的第一个区块

    1.  区块链的最大块大小

    1.  区块链的最小块大小

    1.  包含最大交易数量的区块

1.  什么赋予以太坊虚拟机权力？

    1.  比特币

    1.  CoinDesk

    1.  以太币

    1.  Gas

1.  什么是 PoW？

    1.  一个交易验证协议

    1.  一个哈希算法

    1.  一种加密算法

    1.  安装区块链所需的证书

1.  以下哪个用于存储比特币？

    1.  背袋

    1.  盒子

    1.  钱包

    1.  银行

1.  以下哪些构成一个区块？

    1.  一个哈希指针

    1.  随机数值

    1.  交易

    1.  所有这些

1.  比特币的中央服务器在哪里？

    1.  印度

    1.  华盛顿

    1.  伦敦

    1.  这些中的任何一个

1.  以下哪个行业可以使用区块链技术？

    1.  医疗保健

    1.  智能电网

    1.  P2P 货币交换

    1.  所有这些

1\. b  2\. d  3\. a  4\. b  5\. a  6\. d  7\. a  8\. c  9\. d  10\. d  11\. d

<hgroup>

# 7

# 区块链使用的验证和验证方法

</hgroup>

## 7.1 共识机制

区块链作为一个自我调节的系统运行，不涉及任何中央权威。由于去中心化和分布式的特性，区块链面临拜占庭将军问题[129]。这是一个在去中心化环境中做出共识的问题，其中通信渠道不能被信任。因此，区块链网络应该在存在不诚实节点的情况下保持可靠。此外，在没有中央权威的情况下，必须有人确保块的有效性和验证。共识机制是在分散框架中达成共识的过程。共识机制确保所有节点就共享块的单一状态达成一致，否则网络将面临拜占庭将军问题[48]。它确保可靠性、正确操作和容错性，即使存在故障节点。共识必须是确定性的、同步的和能源充足的。图 7.1 展示了高效共识算法的一些要求。然而，在分布式和去中心化的环境中达成共识是困难的。

**要点** 公共区块链的共识算法具有低可扩展性，但实现低延迟和高吞吐量，而私有区块链共识算法具有高可扩展性。

![图 7.1](img/fig7_1.jpg)

**图 7.1**

共识算法的特点。

接下来讨论了不同的共识算法。这些讨论的共识之间的表格比较在表 7.1 和 7.2 中进行了讨论。

**表 7.1**

不同共识算法的比较。

![表 7.1](img/tab7_1.jpg)

**表 7.2**

不同共识算法的比较。

![表 7.2](img/tab7_2.jpg)

### 7.1.1 工作证明

这是区块链网络用来实现拜占庭容错的第一个也是最流行的共识算法。最初，工作量证明（PoW）是为公共区块链设计的，但在许多现有的研究中，PoW 已被私有和联盟网络使用。PoW 的基础是一个信念，即如果一个节点足够能够执行困难的密码学计算，那么该节点不太可能对网络发起攻击。与证明相关的共识算法的好处在于，无需等待其他网络成员的批准即可挖掘区块。为了将一个区块添加到区块链网络中，每个矿工都会尝试找到一个特定的随机值，以生成区块头中指定的 SHA 哈希。为了解决这种密码难题，随机值在每一轮后递增，以实现哈希值等于或低于为该区块定义的目标值。特别是，区块哈希应该在开头有一定数量的零，也称为系统的难度。挖矿后，矿工将向网络广播该区块。只有当大多数网络成员接受该区块时，它才会成功附加到区块链上。如果一个矿工或一组矿工控制了 51%的哈希算力，那么就会导致 51%攻击。显然，通过 PoW 机制，大量能量被浪费，因为多个矿工同时竞争挖掘一个区块，最终只有一个区块被网络接受。

### 7.1.2 权益证明

股权证明（PoS）是专门设计用来解决 PoW 高能耗问题的。与 PoW 相比，PoS 在挖矿时涉及的 CPU 计算较少，因此能耗更低。PoS 不像 PoW 那样依赖外部投资，而是仅使用内部投资（即加密货币）。尽管与 PoW 类似，PoS 也是为无需许可的区块链设计的。然而，在 PoS 中，矿工被称为验证者，而不是矿工，并且区块是被铸造而不是被挖掘出来的。它基于这样一个基础：网络上参与度和加密货币更多的节点更不可能攻击网络。要成为验证者，节点必须抵押一些加密货币作为赌注。持有者可以将新区块附加到链上的概率与其账户中的赌注数量成比例。PoS 通过成员的赌注处于风险之中来为网络提供安全性。不幸的是，这种方法导致富者越富，因为验证者为验证交易而获得激励，这增加了同一节点再次被选择为验证者的可能性。此外，只有具有足够赌注的节点才能通过投资赌注攻击系统，而 PoW 则需要投资电力、CPU 计算和时间。显然，要发动 51%攻击，验证者必须控制至少 51%的网络中存在的总数字货币，这使得 PoS 攻击更加昂贵。显然，不成功的攻击将导致巨额财务损失。PoS 的第一个用例是 PPCoin，其中拥有最老和最多硬币的参与者具有更大的挖矿可能性（这也称为基于硬币年龄的选择）。在这里，赌注是硬币数量乘以持有期[119]。

### 7.1.3 委托股权证明

这也是对 PoW 的一种替代方案，因为 PoW 需要大量外部资源。相比之下，委托权益证明（DPoS）需要较少的资源，并且在设计上更加环保。DPoS 基于一个投票系统，利益相关者投票选出少数代表（见证人），他们将代表他们负责保护网络。在这里，矿工被称为见证人，他们有责任成功创建一个新的区块。节点的投票权与每个用户持有的加密货币数量成正比。见证人根据声誉选举产生，声誉由每个见证人持有的股份数量决定 [130]。投票数最多的 *m* 个见证人参与区块链网络的决策制定。选取值 *m* 使至少有 50% 的投票人得出有足够的去中心化 [17]。为了验证一个区块，见证人会得到一些好处。选举产生的见证人逐一验证区块。如果一个见证人在固定时间内未能验证通过，那么该区块将被分配给队列中的下一个见证人，同时选取一个新的见证人来替换不负责任的人。要发动 51% 攻击，攻击者必须控制选取的 51% 见证人。值得注意的是，利益相关者在选取见证人方面的更多参与，对于攻击者发动攻击变得越来越困难。

### 7.1.4 实用拜占庭容错

拜占庭容错被描述为分布式系统在网络中存在攻击者节点发送误导信息的情况下仍能达成一致的能力。实用拜占庭容错（PBFT）旨在优化拜占庭容错，以便在区块链网络中实现。实用拜占庭容错（PBFT）[59]旨在解决异步环境中的拜占庭将军问题[129]。它基于这样一个假设，即网络中不到总节点数的 30%是恶意的。换句话说，至少需要<math alttext="" display="inline"><mrow><mn>3</mn><mi>f</mi><mo>+</mo><mn>1</mn></mrow></math>个节点协作，其中 *f* 是故障副本的数量。基于 PBFT 的区块链最多可以容忍 33%的恶意节点。PBFT 的过程包括 3 个阶段，其中包括。

+   预准备：对于每个请求，领导节点广播预准备消息，询问网络中其他节点想要提交的值。

+   准备：节点广播准备消息，指定它们即将提交的值。

+   提交：如果前一阶段有<math alttext="" display="inline"><mrow><mn>2</mn><mi>f</mi><mo>+</mo><mn>1</mn></mrow></math>个节点同意，则领导节点确认请求。

但是，在 PBFT 中，如果有事先列出参与者的先验列表，就可以在低事务延迟和低网络通信开销的情况下达成共识。此外，有限的可伸缩性使其不适用于物联网应用[107]。

### 7.1.5 权威证明

权威证明（PoA）[18] 是 PoS 模型的优化变体，网络上的权威方为了公平运作网络而抵押其身份。 Parity [19] 和 Geth [20] 已经实现了 PoA。 PoA 假设权威是诚实和可信任的。通过抵押身份，验证者不希望与负面声誉联系在一起。与指定一个权威不同，一组权威被用来就网络状态达成一致，并且最终决定必须得到权威的验证。当一个区块被创建时，权威依赖于挖矿轮换方法[36]。这是基于这样一个假设：对于 *N* 个权威，至少应有 <math alttext="" display="inline"><mrow><mfrac><mi>N</mi><mn>2</mn></mfrac><mo>+</mo><mn>1</mn></mrow></math> 个可信节点。PoA 算法设计用于受许可和无许可网络。然而，[68] 的作者表明，PoA 不适用于受许可的区块链，因为它面临一致性问题。与 PBFT 不同，PoA 在网络中涉及少量的消息交换，这提高了性能。然而，使用集中式权威限制了 PoA 在一些应用中的使用。

### 7.1.6 容量证明

不同于 PoW，在容量证明（PoC）中为了添加新区块必须专用存储空间，而不是使用 CPU 和 GPU 进行计算 [75]。通过这种共识机制，可以节省大量能源。PoC 也被称为紧缩型工作证明，因为验证者在挖矿开始之前就已经预先执行了所有计算，并将这些工作的结果（绘图文件）缓存在硬盘上。绘图的过程通过使用 shabal 哈希机制创建一个随机值。挖矿过程只需要读取绘图文件。如果存储介质包含对最近生成的区块难题的快速解决方案，验证者的账户将获得激励。然而，硬盘的大小决定了创建唯一绘图文件所需的时间。与 PoS 不同，因为存储介质价格便宜且易得，网络上的每个人都有公平的挖矿机会。

### 7.1.7 烧币证明

Proof-of-Burn（PoB）[21]旨在解决 PoW 中高能耗的问题，并减少对硬件资源的依赖。在 PoB 中，矿工将硬币投资到一个不可花费地址（在这个地址上，硬币变得无用和不可访问）。该不可花费地址没有分配任何私钥，这意味着只能向该地址发送硬币，但发送到该地址的硬币不能再次使用或花费。通过烧毁或投资硬币，矿工表示愿意承担短期损失。在燃烧硬币时，会执行一个交易给不可花费地址，并通过此交易计算出一个燃烧哈希。燃烧哈希是通过将乘数与内部哈希相乘来计算的。如果燃烧哈希的值小于某个预定义值，则从 PoB 生成区块。矿工烧毁加密货币越多，挖矿的概率就越高。成功挖出一个区块后，矿工会受到奖励。然而，从个人矿工的角度来看，这个方案是昂贵的。

### 7.1.8 幸运证明

幸运证明（PoL）[142] 使用可信执行环境（TEE）来正确处理关键操作。 PoL 背后的理念是网络上的每个节点都向 TEE 请求一个随机数（幸运值）。 幸运值越高，被选为矿工节点的机会就越大。 与 PoW 类似，网络上的节点接收交易，矿工节点竞争在由 TEE 生成的幸运值的区块中提交待处理的交易。 接下来，节点将生成的区块广播到网络，幸运区块被添加到网络中。 在这里，假设少于一半的节点是有故障的。 PoL 还需要安装专用硬件，如 SGX。

## 7.2 简化支付验证

值得注意的是，区块链网络生成了大量数据，这使得资源受限的设备难以在其设备上存储所有数据。这个问题特别困扰移动设备。区块链的不断增长显然对内存受限的设备、物联网设备和比特币移动用户构成了问题。根据[22]的报道，到 2020 年 3 月底，比特币区块链的总大小为 270.11 GB，显然，这个数据在未来几年将会增长。

要解决这个问题，区块链支持区块链网络中的两种客户端，即轻量级客户端和完整客户端。完整节点是遵循区块链的所有规则的区块链网络节点，而轻量级节点是引用可信任的完整节点的节点。轻量级客户端也称为瘦客户端。与完整客户端相比，轻量级客户端不需要下载整个区块链网络。尽管如此，轻量级客户端会下载所有块的块头。显然，由于没有实际交易被下载，这导致了更少的空间和带宽消耗。然而，这些节点参与简单的网络操作，包括确认余额、接收交易历史、检查交易是否存在于块中、验证块难度以及下载块头等操作，而要执行这些操作，这些客户端依赖于完整客户端。这些客户端参考一个或多个完整客户端进行验证、交易验证和挖矿任务。此外，这些客户端不会接收网络中广播的所有交易。相反，它们从连接的完整客户端接收一些它们感兴趣的经过筛选的交易。此外，与完整客户端相比，轻量级客户端只能执行有限的验证。如果轻量级节点想要验证某个交易是否包含在任何块中，它将请求从完整节点获取 Merkle 树。接下来，轻量级节点将使用从完整节点接收的哈希值计算 Merkle 哈希值，并将其与从块头下载的 Merkle 哈希值进行比较。这个确认特定交易被包含在区块链中的整个过程，而不需要实际下载整个区块链，被称为简化支付验证（SPV）。然而，SPV 过程与安全和隐私问题有关。值得注意的是，任何攻击者都可以通过虚假交易欺骗轻量级节点。尽管这个问题可以通过连接到不同的完整节点并确保每个人都同意相同的区块链链解决。

**关键点** 为了解决可伸缩性问题，中本聪描述了回收磁盘空间的过程，提到了从区块中消除不必要的旧交易。然而，在丢弃用于保存磁盘空间的支出交易之前，请确保硬币中的交易已被足够多的区块所埋藏。为了在不干扰区块哈希的情况下实现这一点，只有默克尔根哈希被包含在区块中。

## 7.3 区块验证

即使在挖矿过程之后，网络节点也会在将其添加到主区块链之前验证区块。在将区块包含在区块链中之前，应检查以下几点：

+   语法结构：这是一项首要的验证，确保区块应该符合该区块链网络定义的语法结构。

+   时间戳验证：如果时间戳值大于直接前 11 个区块的中间时间戳值且小于网络调整时间的 2+，则区块被视为有效。网络调整时间是由所有连接的对验证节点返回的时间戳值的中位数。

+   交易：该区块中应该至少存在一笔交易。

+   默克尔哈希：默克尔哈希是从接收到的区块中的交易计算出来的，并与区块头中的默克尔哈希匹配。哈希实际上被认为是区块链网络的核心安全元素。

+   前一个哈希：验证当前区块应该包含直接前一个区块的哈希。

+   目标：区块的哈希值应该小于目标哈希值。

## 7.4 交易验证

在网络中广播的交易需要进行验证，以确保硬币是由授权所有者而不是任意用户花费的。交易验证规则如下所示：

+   空：此属性确保输入和输出交易中没有一个为空。

+   结构：交易的定义的语法结构是正确的。

+   大小：交易的总大小应小于或等于最大区块大小。

+   范围：每个交易的输出值必须在合法货币范围内。

+   货币不足：如果输入价值的总和小于输出价值的总和，则应拒绝交易。

+   低交易费用：如果交易费用低于定义的交易费用，则拒绝交易。

+   公钥：验证每个输入是否接受公钥。

+   双重花费：对于每个输入，如果交易池中任何交易存在引用的输出，则该交易将被拒绝。

+   没有输出交易：对于每个输入，如果不存在任何被引用的输出，则拒绝该交易。

+   孤立交易：对于每个输入，探查主分支和交易池以搜索引用的输出。如果任何输入没有输出交易存在，则该交易是孤立交易。

## 活动

### 多项选择题

1.  共识算法的目的是什么？

    1.  确保所有节点对单一状态达成一致

    1.  解决拜占庭将军问题

    1.  确保在存在故障节点的情况下容错性

    1.  以上所有

1.  PoW 的最大挑战是什么？

    1.  需要高计算能力

    1.  单个矿工无法进行挖矿

    1.  矿工不能一次挖掘一个单一区块

    1.  以上都不是

1.  PoS 代表什么？

    1.  股权证明

    1.  标准证明

    1.  来源证明

    1.  次级证明

1.  PPCoin 加密货币使用哪种共识算法？

    1.  PoW

    1.  PoA

    1.  PoB

    1.  PoS

1.  DPoS 算法如何选择矿工？

    1.  投票系统

    1.  拥有更多电力的人

    1.  拥有更多计算机的人

    1.  以上都不是

1.  PBFT 共识算法的缺点是什么？

    1.  可靠性有限

    1.  有限的可扩展性

    1.  需要高计算能力

    1.  没有容错性

1.  在 PoB 中，矿工将硬币投资到一个以太地址。

    1.  真

    1.  假

1.  Parity 使用哪种共识算法？

    1.  PoB

    1.  PoA

    1.  PoW

    1.  PoS

1\. d  2\. a  3\. a  4\. d  5\. a  6\. b  7\. a  8\. b

<hgroup>

# 8

# 区块链数据结构

</hgroup>

## 8.1 区块链数据结构

本节将讨论区块链使用的重要数据结构。

+   哈希指针：在数据结构中，指针用于指向存储在内存中的值的地址。获取存储在任何内存位置的值的过程称为解引用指针（参见 图 8.1）。此外，哈希指针是一种指针类型，用于指向哈希值的地址，以使其防篡改。特别地，它不仅包含上一个块的地址，还包含上一个块中数据的哈希值。值得注意的是，哈希指针用于构造称为区块链的链表。在区块链中，哈希指针指向存储在上一个块中的数据的哈希。因此，对链中的任何修改都将通过哈希指针检测到。假设一个恶意人篡改了区块链的一个块，比如块 10。随着块 10 内容的更改，此块的哈希值也会更改（哈希的无冲突属性）。为了欺骗其他人，他还必须更改下一个块的哈希指针，即块 11。此外，块 12 的哈希指针也必须更改，依此类推。请参阅 图 8.2 了解哈希指针链的示意图。

    ![图 8.1](img/fig8_1.jpg)

    **图 8.1**

    哈希指针的示意图。

    ![图 8.2](img/fig8_2.jpg)

    **图 8.2**

    哈希指针链的示意图。

    **关键点** 哈希指针可以用于任何基于指针的数据结构，而没有任何循环。如果数据结构中存在循环，则无法使所有哈希匹配起来。显然，在一个带有循环的结构中，我们没有可以从中开始并向后计算的结尾。

+   链表：链表是最流行的数据结构之一。特别是，它是一系列包含一些信息的块，通过指针链接到下一个块。每个块中的指针包含下一个块的地址。最后一个块有一个空指针，意味着它不指向任何内容。区块链基本上是包含数据和指向前一个块的哈希指针的链表。

+   默克尔树：另一个使用哈希指针构造的重要数据结构是二叉树。特别是，这个带有哈希指针的二叉树称为默克尔树。这是区块链概念的主要基础。默克尔树也称为哈希树，以拉尔夫·默克尔[140]的名字命名。它基本上是一种树结构，叶子节点包含文档的哈希，每个中间节点包含其左右子节点的哈希。正如在图 8.3 中所示，有 8 个交易，即，t1，t2，…………，t8。默克尔树的叶子节点包含这些交易的直接哈希，然后第 1 级有包含其左右子节点哈希值的中间节点（即，获得的哈希再次配对以计算下一级的哈希）。这个哈希将递归地计算，直到获得单个根哈希。这意味着任何交易的更改都将反映在每个级别的哈希值中，包括根哈希值。因此，通过单个哈希值，即根哈希，可以在一个块中集体存储交易而不用担心更改。因此，默克尔哈希树确保了存储在区块链上的数据保持完整和未更改。换句话说，默克尔哈希保持文档的完整性。

    ![图 8.3](img/fig8_3.jpg)

    **图 8.3**

    默克尔树的结构。

    **要点** 计算默克尔哈希，比特币使用 SHA-256 哈希。

+   字典树：字典树是一种有序树数据结构，用于维护一组字符串。如果两个字符串有一个共同的前缀，则它们在字典树中将有相同的祖先。字典树是存储词典的理想数据结构。此外，它还用于编码和解码。值得注意的是，字典树与二叉树不同，而是一种 N 叉树。实际上，字典树支持比二叉搜索树和哈希表更好的搜索。哈希表不支持基于前缀的搜索。此外，使用字典树可以轻松按字母顺序打印所有单词。

    Trie（字典树）存储键-值对，其中键是树中达到其对应值的路径。使用字典树时，节点可以有任意数量的子节点。然而，所有节点的后代都有一个共同的前缀。特别是，每个节点最多可以有 26 个子节点。每个节点的子节点按字母顺序排序。可以将其视为每个节点内置一个大小为 26 的数组。然而，更好的选择是在每个节点上使用链表来节省空间。

    不幸的是，trie 对于存储字符串需要大量内存，因为对于每个节点都有更多的指针。此外，如果有长键并且没有其他键共享公共前缀，则 trie 会变得低效。标准 trie 占用 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>W</mi><mo stretchy="false">)</mo></mrow></math> 空间，其中 *W* 是集合中字符串的总大小。trie 的插入、删除和搜索操作的时间复杂度为 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>l</mi><mo>*</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>，其中 *l* 是单词的平均长度，*n* 是单词的总数，而创建 trie 的最坏情况运行时复杂度为 <math alttext="" display="inline"><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>m</mi><mo>*</mo><mi>n</mi><mo stretchy="false">)</mo></mrow></math>，其中 *m* 是字符串中最长的单词，*n* 是单词的总数。例如，字符串集合 S=bear，bell，bid，bull，buy，sell，stock，stop 的 trie 数据结构在 图 8.4 中表示。

    ![图 8.4](img/fig8_4.jpg)

    **图 8.4**

    trie 数据结构的说明。

+   Patricia 树：Patricia 代表实用的字母数字编码信息检索算法。它也基于节点具有相同前缀共享相同路径的基本原理（也称为前缀树）。然而，它需要比 trie 数据结构更低的内存。实际上，它是 trie 的一种紧凑表示，在这种表示中，具有单个子节点的节点与其父节点合并。换句话说，Patricia 树类似于基数树，其基数值等于 2。特别是，以太坊区块链基于 Merkle-Patricia 树，它是具有包含整个数据结构的哈希值的根节点的树。图 8.5 表示了字符串 S = bear，bell，bid，bull，buy，sell，stock，stop 的 Patricia 树。

    ![图 8.5](img/fig8_5.jpg)

    **图 8.5**

    Patricia 树数据结构的示例。

+   Merkle Patricia trie：这种数据结构是 Merkle 树和 Patricia 树的组合。Merkle 树用于维护数据完整性，而 Patricia 树特别是用于快速搜索信息。这些 Merkle Patricia 还展示了某种形式的验证和防篡改。以太坊区块链加密货币使用 Merkle Patricia 树来存储交易和世界状态。值得注意的是，以太坊与比特币非常不同，因为它使用智能合约，每次都在更新。此外，以太坊不是使用一个 Merkle 树，而是使用 3 个不同的 Merkle 树来获得全局状态，并对区块链中的数据进行额外查询的能力，这些能力描述如下：

    +   stateRoot：指定了区块的状态。

    +   transactionRoot：指定了区块中的交易哈希。

    +   receiptRoot：指定了区块中使用的燃气量。

    在以太坊中，所有状态信息都以键值对的形式存储。键主要是指向搜索索引的字符串值。例如，帐户地址是键，余额是对应于该键的值。Merkle Patricia 树引入了 4 种类型的节点，描述如下：

    +   空节点：这些只是空白节点。

    +   叶节点：它是树中路径结束的节点。叶节点不会有进一步的子节点，并且它总是包含与某个键对应的某些值。它由两个项目组成，第一个对应于后缀，第二个对应于任何值。

    +   分支节点：它是一个具有多个分支的节点。它是一个 17 项结构，其中前 16 项是十六进制值（0—F），第 17 项对应于终止节点。

    +   扩展节点：它是一种分支节点，但只有一个子节点。这是分支节点的优化版本。它是一个两项节点，第一个部分表示键部分，大小大于一个节点，并且至少被两个不同的键共享。第二部分对应于指向分支节点的指针。

    值得注意的是，为了区分叶节点和扩展节点，有一个叫做 nibble 的概念。一个 nibble 被添加到键的开头，以区分奇偶性（偶数/奇数长度的键）和终止符状态（节点是叶节点还是扩展节点）。较低有效位表示奇偶性，而次低位表示终止符状态。此外，如果键的长度是偶数，则添加一个额外的 nibble 以实现整体偶数长度。图 8.6 显示了 Merkle Patricia 树的示例。

    ![图 8.6](img/fig8_6.jpg)

    **图 8.6**

    Merkle Patricia 树数据结构的示例。

+   二叉堆：二叉堆属于二叉树的一种。特别地，二叉堆是一个完全二叉树，这意味着除了可能是最低层的每一层都是完全填充的，而最低层始终从左边填充。此外，二叉堆根据排序属性被归类为最大堆或最小堆。在最大堆中，每个节点中存储的键值必须大于等于节点子节点中存储的键值。相反，在最小堆中，每个节点中存储的键值必须小于或等于节点子节点中存储的键值。最小堆和最大堆数据结构的示例分别在 Figs. 8.7 和 8.8 中表示。以太坊区块链使用二叉堆数据结构来解决以太坊的区块燃气限制和迭代问题。以太坊燃气是在以太坊区块链中执行某些操作的价格。例如，所有以太坊交易都由交易发送者支付。在这种情况下，攻击者可以通过运行任意智能合约来消耗更多的燃气。此外，当以太坊网络的用户在智能合约中插入数据时，通过迭代可能导致过多的燃气成本。特别地，如果开发人员依赖于数组数据结构，攻击者可以填充数组直到通过它进行迭代的成本比单个交易应该用于执行的成本更高。显然，二叉堆解决了这个问题，因为这种数据结构不要求迭代整个树的所有元素，而只需迭代树的高度。此外，最大堆的自平衡属性保留了使树退化的树，这导致即使在最坏的情况下（对于总共的*n*个元素）也需要*O(log n)*的成本。

    ![图 8.7](img/fig8_7.jpg)

    **图 8.7**

    最大堆的示例。

    ![图 8.8](img/fig8_8.jpg)

    **图 8.8**

    最小堆的示例。

## 活动

### 多项选择题

1.  区块链中使用以下哪种数据结构？

    1.  默克尔哈希树

    1.  Trie

    1.  二叉树

    1.  以上所有

1.  在区块链中使用哈希指针进行连接性的主要目的是什么？

    1.  防止区块中的修改

    1.  加密区块

    1.  解密区块

    1.  寻找区块的随机数值

1.  比特币用于计算默克尔哈希的哈希算法是什么？

    1.  MD4

    1.  MD5

    1.  SHA-256

    1.  所有这些

1.  如果 *w* 是集合中字符串的总大小，则 trie 数据结构的总空间占用是多少？

    1.  *O(w)*

    1.  *O(w2)*

    1.  *O(log w)*

    1.  以上都不是

1.  Patricia 树的另一个名称是什么？

    1.  前缀树

    1.  后缀树

    1.  最大堆

    1.  二进制堆

1.  使用默克尔帕特里夏树的主要目的是什么？

    1.  防止区块中的修改

    1.  加密区块

    1.  解密区块

    1.  寻找区块的随机数值

1.  以下哪种节点是默克尔帕特里夏树的一种类型？

    1.  叶子节点

    1.  分支节点

    1.  扩展节点

    1.  所有这些

1.  以太坊为什么使用二进制堆数据结构？

    1.  解决区块气体限制和迭代问题

    1.  解决 PoS 问题

    1.  在网络上验证节点

    1.  生成更多以太币

1.  哈希指针可以与具有循环的任何数据结构一起使用？

    1.  正确

    1.  错误

1.  使用默克尔哈希树的主要目的是什么？

    1.  保护区块的完整性

    1.  解密区块

    1.  加密一个区块

    1.  寻找随机数值

1\. d  2\. a  3\. c  4\. a  5\. a  6\. a  7\. d  8\. a  9\. b  10\. a
