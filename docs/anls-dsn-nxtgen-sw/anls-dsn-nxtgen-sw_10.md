© Springer Nature Switzerland AG 2020 A.M.兰格下一代软件架构的分析与设计[`doi.org/10.1007/978-3-030-36899-9_10`](https://doi.org/10.1007/978-3-030-36899-9_10)

# 10. 转换传统系统

阿瑟·M·兰格（1）哥伦比亚大学技术管理中心，纽约，纽约，美国。 阿瑟·M·兰格电子邮件：al261@columbia.edu

## 10.1 介绍

传统系统是指正在运行的现有应用系统。虽然这是一个准确的定义，但有一种看法认为传统系统是在大型机上运行的老旧的、过时的应用程序。实际上，布罗迪和斯通布雷克（1995 年）指出，“传统信息系统是任何显著抵制修改和演进的信息系统”（第 3 页）。他们将典型的传统系统定义为：

+   大型应用程序有数百万行的代码。

+   通常超过 10 年的历史。

+   使用 COBOL 等传统语言编写。

+   它们围绕着传统数据库服务构建（如 IBM 的 IMS），有些不使用数据库管理系统。而是使用较旧的平面文件系统，如 ISAM 和 VSAM。

+   应用程序非常自主。传统应用程序倾向于独立运行，这意味着应用程序之间的接口非常有限。当应用程序之间存在接口时，它们通常基于数据的导出和导入模型，这些接口缺乏数据一致性。

虽然许多传统系统符合这些场景，但也有许多不符合的。那些不符合的可以被认为是传统系统，根据我的原始定义，即任何正在运行的应用程序。这意味着在任何组织中都可能存在我所谓的“代际”传统系统。因此，对于传统系统构成的定义要比布罗迪和斯通布雷克的描述宽泛得多。更重要的问题是解决传统系统与封装软件系统的关系，特别是随着独立 API 从不断发展的物联网设备、区块链产品和云计算的爆炸式增长。通常由第三方供应商支持的封装软件系统涵盖内部和外部应用程序。因此，现有的内部生产系统，包括第三方外包产品，必须成为任何应用程序战略的一部分。此外，还有许多传统系统也执行外部功能，尽管不直接在互联网界面中执行。

本章定义了存在的遗留系统类型，并提供了如何处理它们与包装软件应用程序集成以及转换为支持物联网的新架构的指导方针。项目经理或分析员必须确定是否应该替换、增强或保持现状的遗留系统。本章还提供了处理这三种选择及其对决定整体架构是否制作或购买系统的影响的程序。然而，总体而言，本章建议所有传统的遗留系统在某个时候都需要重新开发以支持移动性和最大化的网络安全保护。

## 10.2 遗留系统的类型

遗留系统的类型往往反映了软件开发的生命周期。软件开发通常在称为“世代”的框架内定义。大多数专业人士都同意，编程语言有五代：

1.  1.

    *第一代*：第一代被称为机器语言。机器语言被认为是低级语言，因为它使用二进制符号向硬件传达指令。这些二进制符号形成了机器语言命令和机器活动之间的一对一关系，即一个机器语言命令执行一个机器指令。很少有遗留系统拥有第一代软件。

1.  2.

    *第二代*：该代表由汇编语言编写的。汇编语言是专有软件，将高级编码方案转换为多个机器语言指令。因此，有必要设计一个汇编器，将符号代码转换为机器指令。主机商可能仍然拥有大量的汇编代码，尤其是对于执行复杂算法和计算的应用程序而言。

1.  3.

    *第三代*：这些语言延续了具有机器代码转换器的高级符号语言的增长。第三代语言的示例包括 COBOL、FORTRAN、BASIC、RPG 和 C。这些语言使用更类似英语的命令，并且从一个指令产生的机器语言比例更高。第三代语言往往更专业化。例如，FORTRAN 更适合数学和科学计算。因此，许多保险公司使用 FORTRAN，因为其高度集中在精算数学计算上。另一方面，COBOL 被设计为商业语言，并具有特殊功能，允许其操纵文件和数据库信息。存在比其他任何编程语言更多的 COBOL 应用程序。大多数主机遗留系统仍然具有 COBOL 应用程序。RPG 是另一种专业化语言，专为在 IBM 的中等机器上使用而设计。这些机器包括 System 36、System 38 和 AS/400 计算机。

1.  4.

    *第四代*（*4GL*）：这些编程语言比第三代语言少了一些程序性质。此外，符号更像英语，并且更强调所需的输出结果，而不是编程语句应该如何编写。由于这个特点，许多不太技术的程序员已经学会使用 4GL 进行编程。4GL 的最强大功能包括数据库查询、代码生成和图形界面生成能力。这些语言包括 Visual Basic、C++、Visual Basic、Powerbuilder、Delphi 等等。此外，4GL 语言还包括所谓的*查询语言*，因为它们包含类似英语的问题，用于通过直接访问关系数据库直接产生结果。最流行的 4GL 查询语言是结构化查询语言（SQL）。

1.  5.

    *第五代*：这些编程语言结合了所谓的基于规则的代码生成、组件管理和可视化编程技术。基于规则的代码生成在 20 世纪 80 年代晚期因人工智能软件的创造而流行起来。这种软件使用一种称为基于知识的编程的方法，这意味着开发人员不告诉计算机如何解决问题，而是告诉问题（Stair 和 Reynolds 1999）。程序会想办法解决问题。虽然基于知识的编程在专业应用中变得流行，比如在医疗行业，但在商业领域并不那么流行。

大多数遗留应用程序将是第三代或第四代语言系统，因此，分析师需要有一个过程和方法论来确定如何转换和重新设计这些应用程序。

## 10.3 第三代语言遗留系统集成

正如之前讨论的那样，大多数第三代语言遗留系统都是使用 COBOL 开发的。COBOL 的开发目的是提供一种方法，强制程序员对其代码进行自我文档化，以便其他程序员可以维护它。不幸的是，COBOL 需要所谓的文件描述表（FD）。FD 为 COBOL 程序使用的每个文件定义了记录布局。换句话说，每个文件都在程序中描述，并且必须与实际物理数据文件的格式匹配。这意味着对文件结构的任何更改都必须与使用该数据文件的每个 COBOL 程序同步。因此，COBOL 有点古怪：没有真正的数据描述和程序逻辑分离。在 COBOL 程序中，数据格式的变化可能需要改变程序代码。这就是为什么 COBOL 程序存在很大程度的代码耦合的原因。耦合被定义为代码片段对另一个代码片段的依赖。

COBOL 程序可能使用关系数据库或者不使用关系数据库作为其数据源。我之前定义了另外两种常见的格式，称为 ISAM 和 VSAM，它们是平面文件格式，这意味着所有数据元素都包含在一个记录中，而不像关系数据库模型中那样包含在多个文件中。然而，许多 COBOL 遗留系统已被转换为与诸如 IBM 的 DB2 等关系数据库一起工作。在这种情况下，FD 表与数据库的文件管理器进行接口，以便这两个实体可以相互通信。图 10.1 描述了程序与数据库之间的接口。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig1_HTML.png](img/480347_1_En_10_Fig1_HTML.png)

图 10.1

COBOL 文件描述与数据库管理器进行接口

无论 COBOL 遗留系统是否使用数据库接口或平面文件，分析人员都需要确定是替换应用程序，增强它还是保持原样。

## 10.4 替换第三代遗留系统

替换第三代遗留系统时，分析人员必须同时关注数据和流程。由于这些系统的年龄，可能会很少有文档可用，并且可用文档的数量很可能已经过时。事实上，缺乏适当的文档是遗留系统被替换的主要原因：在没有文档的情况下重写代码可能是一个艰巨且耗时的任务。不幸的是，所有事物最终都必须被替换。延迟替换会导致遗留系统使企业无法保持竞争力。以下各节提供了一种基于 COBOL 的遗留系统的逐步方法。

## 10.5 逻辑重构的方法

重建 COBOL 应用程序中的逻辑的最佳方法是将数据与流程分离。这可以通过为每个程序创建数据流图（DFD）来实现。拥有 DFD 将导致定义应用程序的所有输入和输出。通过以下任务实现：

1.  1.打印每个应用程序的源代码（实际的 COBOL 编写的代码）。每个应用程序都包含一个定义程序的所有输入和输出的“FD”部分。这些将代表数据流图的数据存储（图 10.2）。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig2_HTML.png](img/480347_1_En_10_Fig2_HTML.png)

    图 10.2

    COBOL 文件描述表

1.  2.

    DFD 应该被分解，以便它们处于功能原语级别（一进一出，首选）。这为旧应用提供了功能分解，并为将其分解为面向对象解决方案奠定了框架。

1.  3.

    通过审查代码，为每个功能原语编写过程规范。

1.  4.

    按照第 3 章概述的步骤来确定哪些功能原始 DFD 成为特定类别的方法。

1.  5.

    捕获每个功能原始 DFD 所需的所有数据元素或属性。这些属性将添加到数据字典（DD）中。

1.  6.

    对每个主要数据存储进行实体化处理。根据第 4 章的流程进行规范化和逻辑数据建模，并根据需要将这些元素与打包软件系统结合起来。

1.  7.

    表示报告的数据存储应与样本输出进行比较。这些报告需要使用报告编写器（如 Crystal 的报告编写器或数据仓库产品）重新开发。

1.  8.

    检查遗留系统中的所有现有数据文件和/或数据库。将这些元素与逻辑重构期间发现的元素进行比较。在第三代产品中，将有许多冗余的数据元素或字段，或用作逻辑“标志”的字段。逻辑标志包括用于存储表示数据特定状态的值的字段。例如，假设记录已由特定程序更新。知道发生这种情况的一种方法是让应用程序设置一个特定的字段，并使用标识已更新的代码。在关系数据库产品中，这种方法不是必要的，因为文件管理器会自动记录上次记录被更新的时间。此示例说明了第三代遗留技术与更现代技术之间的差异。

毫无疑问，替换第三代遗留系统是耗时的。然而，上述程序将证明是准确和有效的。在许多情况下，用户将决定重新审视其遗留流程，特别是在决定重新编写应用程序以与物联网和区块链系统集成时。我们称之为业务流程再造。因此，业务流程再造与增强遗留系统是同义词。

## 10.6 增强第三代遗留系统

业务流程再造（BPR）是用于增强第三代应用程序的较流行的方法之一。 BPR 的更正式定义是“研究基本业务流程的要求，独立于组织单位和信息系统支持，以确定是否可以显着简化和改进基础业务流程。”^(1) BPR 不仅仅是为了将新技术应用于旧系统而重新构建现有应用程序，而且是一个允许应用围绕面向对象系统范式设计的新程序的事件。然而，在这种情况下，BPR 用于增强现有应用程序，而无需用另一种语言重写它们。相反，分析人员需要对系统进行更改，使其更像对象组件，即使它是用第三代语言编写的也是如此。为了完成这项任务，分析人员需要创建遗留操作的基本组件。基本组件代表一个单位的核心业务需求。定义核心业务需求的另一种方法是将基本组件视为单位存在的原因——它是做什么的——以及出于什么原因。例如，图 10.3 描述了银行的基本组件。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig3_HTML.png](img/480347_1_En_10_Fig3_HTML.png)

图 10.3

银行的基本组成部分

一旦创建了基本组件，那么遗留应用程序就需要放置在适当的组件中，以便将其与相关的打包软件应用程序链接，或将其分解为原始 API。

将成功的业务流程再造（BPR）应用于遗留应用程序的第一步是制定一种定义现有系统并提取其数据元素和应用程序的方法。再次强调，这与上述替换第三代遗留应用程序的过程类似，其中需要将数据捕获到数据存储库中，并定义应用程序，并将其与基于基本组件的新模型进行比较。

## 10.7 数据元素增强

分析师将需要设计转换程序，这些程序将访问不在关系数据库格式中的数据文件，并将它们放入数据存储库中。最终的重点是用可以与包装软件数据库链接的关系数据库替换遗留的所有现有数据文件。这种方法与替换遗留不同。在替换工程中，数据文件直接集成到包装软件系统中。这意味着遗留数据通常将用于增强包装软件数据库或与各种云数据库产品集成。然而，增强遗留系统的过程意味着遗留数据将保持分离，但转换为关系或对象数据库模型。对于已经具有关系数据库的遗留系统，除了设置与包装软件数据库的链接外，不需要进行重组。图。10.4 反映了替换遗留数据与增强遗留数据之间的区别。尽管有这些步骤，一旦确定了这些数据元素，分析师应遵循考虑将哪些元素复制到物联网和区块链架构的步骤。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig4_HTML.png](img/480347_1_En_10_Fig4_HTML.png)

图。10.4

替换与增强传统数据

两种方法之间的另一个有趣的区别是，增强的遗留系统可能会有意的数据冗余。这意味着同一个元素可能会存在于多个数据库中；这是物联网和区块链支持的新分布式系统所必需的。重复元素可能具有不同的格式。最明显的是，数据元素具有别名，这意味着一个元素有许多不同的名称，但具有相同的属性。另一种类型是相同的元素名称，但具有不同的属性。第三种类型，也是最具挑战性的，是具有不同名称和不同属性的重复元素。虽然增强的遗留应用程序中可能存在重复的数据元素，这些应用程序已与包装软件产品集成，但仍然重要的是识别重复的数据关系。这可以通过在 CASE 工具和数据库的物理数据字典中记录数据关系来完成，其中可能存在别名。

### 10.7.1 应用程序增强

业务流程重组（BPR）通常涉及一种称为业务领域分析（BAA）的方法。BAA 的目的是：

+   建立将与新架构和/或包装软件系统链接的各种遗留业务领域。

+   重构每个业务领域的新旧需求。

+   制定提供每个遗留业务领域的面向对象（OO）视角的需求，这意味着无需将其需求映射到现有的物理组织结构。

+   定义创建所有遗留业务领域和包装软件业务领域之间关系的链接。

这是通过将业务领域映射到特定的基本组件来实现的。为包装软件系统设计的应用程序也必须映射到一个基本组件。一旦发生了这种情况，遗留应用程序和包装软件应用程序必须被设计成共享常见的流程和数据库，如图 10.5 所示。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig5_HTML.png](img/480347_1_En_10_Fig5_HTML.png)

图 10.5

使用基本组件对 BPR 遗留建模

一旦将遗留和包装软件应用程序放置在适当的基本组件中，它们将需要被链接，也就是彼此通信以完成内部 IoT 和外部系统的集成。链接有两种方式：参数消息和数据库。参数消息要求修改遗留程序以接收参数形式的数据。这允许应用系统直接向遗留程序传递信息。相反，遗留程序可能需要将信息返回给包装软件系统。因此，遗留应用程序需要被增强，以便它们实际上可以格式化并发送数据消息到包装软件系统。数据库接口本质上是相同的概念，只是它的发生方式不同。与应用程序将数据直接发送到另一个程序不同，它将其作为数据库文件中的记录转发。返回数据的遗留程序还需要被修改，以将消息转发到可能的云数据库。

使用任一方法都有优点和缺点。首先，参数使用的开销很小，编程容易。它们不提供可重用的数据，也就是说，一旦收到消息，它就不再对另一个程序可用。参数的大小也受限制。另一方面，数据库允许程序将信息发送到多个目的地，因为它可以被多次读取。不幸的是，很难控制哪些应用程序或查询可以访问数据，这确实引发了关于数据安全性的问题。此外，如果不再需要记录，应用程序必须记住在数据库中删除记录。图 10.6 反映了在遗留系统和包装软件应用程序之间传输数据的两种方法。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig6_HTML.png](img/480347_1_En_10_Fig6_HTML.png)

图 10.6

在遗留和包装软件系统之间链接数据

一旦将遗留应用和新应用都映射到基本组件，分析师就可以使用 CRUD 图来帮助他们协调是否已经找到所有的数据和流程。CRUD 图的重要性在于它确保：

+   一个重要组件完全控制其数据，

+   所有实体至少被一个进程访问，并且

+   进程正在访问数据（见图 10.7）。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig7_HTML.png](img/480347_1_En_10_Fig7_HTML.png)

    图 10.7

    示例 CRUD 图

CRUD 不是 100% 准确，但它确实揭示了可能存在的问题，如上所示。即使不使用 BPR，CRUD 图也是一个用于确定重要组件或对象所需的过程和数据的优秀工具。一旦 CRUD 图完成，对象和类将如图 10.8 所示创建；其中一些对象仍以第三代 COBOL 程序的形式存在，而另一些可能以基于 API 的打包软件格式存在。然而，重要的是要注意，“U” 和 “D” 在区块链应用中是不允许的，因为账本系统不允许修改现有交易！../images/480347_1_En_10_Chapter/480347_1_En_10_Fig8_HTML.png

图 10.8

重要组件对象图

## 10.8“按原样离开”——第三代遗留系统

从类似 COBOL 这样的第三代产品转向面向对象和 API 范式可能并不可行。第三代过程化程序的语言设计可能导致过程式和面向对象哲学之间的概念差距。例如，分布式面向对象程序需要比旧的传统系统更详细的技术基础知识和图形处理。原生的面向对象特性，比如继承、多态和封装，在传统的第三代过程化设计中不适用。在直接将 COBOL 转换为 JAVA API 时，很难，甚至不可能引入新的对象概念和哲学，如果不进行重大重构（正如本章前面讨论的）。如果尝试翻译而不进行重大重组（如本章前所述），则结果产品可能包含更难维护的较慢的代码。

也可能存在文化分歧。老练的 COBOL 程序员和新手 JAVA API 开发人员互相不理解对方的技术。这种情况往往会在任何转换工作中产生偏见。此外，COBOL 程序员学习新技术可能会对他们的文化地位构成自我认定的威胁。此外，COBOL 和 RPG 应用程序经过了比较新的编程世代更长时间的测试、调试和整体改进。虽然 JAVA 更具动态性，但它不太稳定，调试和解决问题的程序与 COBOL 或 RPG 完全不同。因此，分析人员将保持遗留系统的“原样”，仅创建必要的打包软件链接以传递所需的信息。虽然这与提升遗留系统所提出的“链接”类似，但不同之处在于，除了传递信息所需的外部链接外，遗留程序不会得到增强。这在图 10.9 中以图形方式显示。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig9_HTML.png](img/480347_1_En_10_Fig9_HTML.png)

图 10.9

“原样”遗留链接

使用参数或数据库来连接信息仍然是相关的，但分析人员必须意识到遗留数据格式不会改变。这意味着遗留应用程序将继续使用其原始文件格式。用于描述“链接”的另一个概念称为“桥梁”。这个词表明，链接用于连接打包软件系统和遗留应用程序之间的差距。桥接也可以暗示临时链接。很多时候，“原样”可以被视为一个临时条件，因为遗留转换不能一次性完成，因此通常是分阶段计划的。但是，在系统的部分部分被转换的同时，一些部分可能需要临时桥梁，直到实际增强它们的时候。人们可以将其视为临时的“路障”或绕行路线，当高速公路上有施工时会发生这种情况。

## 10.9 第四代语言遗留系统集成

将第四代遗留系统与打包软件技术集成要比第三代语言容易得多。原因有两个。首先，大多数第四代实现已经在使用关系数据库，因此将数据转换到打包软件系统的复杂度较低。其次，第四代语言应用通常使用基于 SQL 的代码，因此转换为面向对象的系统也较少涉及。

## 10.10 替换第四代遗留系统

如上所述，与打包软件转换相关的第四代语言系统的替换比第三代语言更不复杂。与任何系统替换一样，分离数据和过程是建议的方法。幸运的是，在第四代语言系统中，由于其架构的性质，过程和数据可能已经分开。具体而言，第四代语言通常使用关系数据库，其在架构上分离数据和过程。因此，替换遗留系统更多地涉及检查现有流程，并确定应该对应用程序进行重新工程设计的位置。

## 10.11 逻辑重构方法

对逻辑分析的最佳方法是打印出程序的源代码。如果源代码是用 SQL 编写的，则分析师应搜索所有 SELECT 语句。SQL SELECT FROM 语句定义程序正在使用的数据库，如图 10.10 所示。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig10_HTML.png](img/480347_1_En_10_Fig10_HTML.png)

图 10.10

第四代语言应用程序中的 SELECT 语句

就像第三代语言逻辑重构一样，分析师应该为每个程序生成一个 DFD，如下所示：

1.  1.

    SELECT 语句定义程序使用的所有输入和输出。每个 SELECT 语句文件将由一个 DFD 数据存储表示。审查应用程序的逻辑将揭示数据是被创建、读取、更新还是删除（CRUD）。

1.  2.

    DFD 应分解到功能原始级别，以建立面向对象的系统框架。

1.  3.对于每个 DFD，复制相关的 SQL 代码，根据需要进行修改，以向程序提供更多面向对象的功能。这意味着代码的分解可能需要添加一些新的逻辑来将其转换为方法。如图 10.11 所示。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig11_HTML.png](img/480347_1_En_10_Fig11_HTML.png)

    图 10.11

    SQL 代码过渡到对象方法

1.  4.

    检查现有系统对象，确定功能原始 DFD 是否属于现有类作为新方法，还是真正表示打包软件系统中的新对象。

1.  5.

    捕获新方法所需的所有数据元素，并将它们添加到各自的对象中。确保打包软件 DD 得到适当更新。

1.  6.

    确定是否有任何新对象需要成为 TP 监视器（中间件）中的可重用组件，客户端应用程序中的可重用组件，或者作为数据库级别的存储过程。

1.  7.

    检查遗留数据库并进行逻辑数据建模，将实体放置在第三正规形式（3NF）中。

1.  8.

    将数据元素与打包软件数据库结合并整合，确保遗留系统中的每个数据字段与打包软件数据元素正确匹配。新元素必须添加到适当的实体中，或者需要为它们创建新的实体。

1.  9.

    使用第三范式参照完整性规则将新实体与现有模型关联起来。

1.  10.确定哪些数据元素是多余的，例如计算。这些数据元素将被删除；然而，可能需要为它们的计算添加逻辑，如图 10.12 所示的方法。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig12_HTML.png](img/480347_1_En_10_Fig12_HTML.png)

    图 10.12

    将多余的数据元素转换为处理规范。

## 10.12 加强第四代遗留系统

加强第四代语言遗留系统实际上是将其转换为面向对象的客户端/服务器系统。 BPR（业务流程再造）也用于第四代语言遗留系统以完成这一过渡。正如人们可能期望的那样，与第三代语言相比，该过程要容易得多；但是，确定必要组件的过程在两种类型的系统中是相同的。一旦建立了必要的组件，就需要将现有应用程序进行分解和重新对齐。这是通过使用 BAA 来实现的，就像它用于第三代遗留应用程序一样。第四代语言比第三代语言少程序化的事实极大地促进了这一过渡。通过简单查看 SQL SELECT 语句，第四代语言系统可以确定应用程序使用哪些数据文件。使用逻辑模块化规则，分析人员可以根据使用相同数据的应用程序建立凝聚的类。这可以在不使用 DFD 的情况下完成，尽管使用 DFD 进行重新工程始终是分析人员遵循的更彻底的方法。

第四代语言遗留和打包软件应用程序的链接需要在应用程序重构完成后完成。与第三代语言系统一样，这可以通过使用数据参数或创建专用数据库来完成。但是，使用第四代语言时，应用集成可能会使用数据库，因为这两个系统都在其本地架构中使用它们。分析人员很可能会发现，与第四代语言的应用通信并不总是需要专门设计用于系统链接目的的独立数据库。集成的更有吸引力的解决方案是识别两个系统之间共同的数据元素，以便在一个中央数据库中共享，该数据库对所有应用程序都可用，如图所示。 10.13。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig13_HTML.png](img/480347_1_En_10_Fig13_HTML.png)

图 10.13

第四代语言遗留共享数据库架构

在第四代语言中使用 CRUD 的情况较少，但肯定适用，并且如果分析人员认为代码过于程序化，应该实施。换句话说，代码架构类似于第三代而不是第四代。

## 10.13 “保持不变”—第四代遗留系统

限制集成仅限于数据共享的过程类似于我用于第三代语言系统的设计架构。实际上，将单独且不同的软件系统链接的架构只能通过共享公共数据来实现。再次强调，这些数据可以使用数据参数或数据文件共享。

由于许多第四代语言系统利用与打包软件系统相同的架构（使用 Windows NT 或 UNIX/LINUX 的三层客户端/服务器），有时候利用某些操作系统级通信设施是有利的。例如，UNIX 允许应用程序使用称为“管道”的操作系统设施传递数据。管道类似于参数，它允许一个应用程序向另一个应用程序传递消息或数据，而不创建实际的新数据结构，例如数据库。此外，管道使用一种称为“FIFO”（先进先出）的访问方法，这是参数使用的相同访问标准。FIFO 还要求一旦数据被读取，就不能再次读取。使用管道的主要优点是消息/数据可以在创建消息的应用程序终止后长时间存储在内存中。因此，信息在 IoT、打包软件和第四代语言应用程序之间的链接可以在执行时通过 RAM 完成，这称为“应用内通信”。这种能力减少了开销，以及设计需要处理数据通信的单独模块的需求，如图 10.14 所示。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig14_HTML.png](img/480347_1_En_10_Fig14_HTML.png)

图 10.14

使用 UNIX 管道进行应用内通信

## 10.14 混合方法：网关方法

到目前为止，在本章中，我已经专注于特定类型的遗留系统与物联网、区块链和/或打包软件系统之间的接口。每种类型都是根据其“代”类型定义的。然而，在现实中，遗留系统并不是那么自我定义的。许多大型组织都有“遗留层”，这意味着整个企业存在多代。在这种情况下，试图将每一代与一个中央打包软件系统集成在一起是困难且耗时的。事实上，迁移和集成遗留系统已经足够困难了。在这些复杂的模型中，用于迁移遗留应用程序的另一种方法是一种名为“混合”的方法，称为“网关”。网关方法意味着将有一个软件模块在打包软件系统和遗留应用程序之间进行请求中介。在许多方面，网关执行类似于 TP 系统的任务。因此，网关充当应用程序之间的代理。具体来说，网关：

+   将不同代语言的组件分离但整合在一起。它允许多个代语言系统之间的链接。

+   在多个组件之间转换请求和数据。

+   协调多个组件以确保更新一致性。这意味着网关将确保冗余数据元素同步。

典型的网关架构设计如图 10.15 所示。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig15_HTML.png](img/480347_1_En_10_Fig15_HTML.png)

图 10.15

传统集成的网关架构

网关最有益的作用是允许对传统组件进行分阶段处理。基础设施通过为数据和应用程序建立一致的更新流程，提供了逐步转换的方法。

## 10.15 增量应用集成

网关为图形用户界面（GUI）、基于字符的界面和自动化接口（批量更新）建立了透明度，使其对打包软件系统看起来是相同的。因此，网关使传统系统与打包软件系统的接口看起来是无缝的。这通过一个接口来实现，该接口将对流程功能的请求进行转换，并将其路由到相应的应用程序，而不管软件的生成和其在打包软件迁移中的特定阶段如何。图 10.16 描述了网关系统的流程功能。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig16_HTML.png](img/480347_1_En_10_Fig16_HTML.png)

图 10.16

传统网关的应用功能

网关方法最显著的好处是与面向对象范式和应用程序可重用性概念的一致性。具体来说，它允许任何模块表现出“像”可重用组件一样的行为，尽管其技术设计不同。在这种架构哲学下，一个特定的程序，比如说，一个第三代语言系统，最终可能会被替换并放入网关中，直到整体迁移完成为止会建立临时桥梁。这一过程还支持对企业的更“全局”的视图，而不仅仅关注于特定子系统。图 10.17 描绘了使用网关架构进行流程集成的概念。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig17_HTML.png](img/480347_1_En_10_Fig17_HTML.png)

图 10.17

使用网关架构进行流程集成和迁移

## 10.16 增量数据集成

增量数据集成关注于如何在打包软件系统中保持多组数据的协调。

与数据集成相关的两个主要问题集中在查询和更新上。查询涉及跨多个系统访问有关数据集（相关数据元素的集合）的完整信息。使用数据仓库或数据挖掘架构可以解决许多查询挑战。网关将作为基础设施，确定数据的副本数量及其位置。

数据集成的更困难和更重要的概念是网关协调多个数据库和平面文件系统的更新能力。这意味着在一个组件中更改数据元素将“触发”对其他组件的自动更新。关于数据元素不同定义存在的四种情况：

1.  1.

    每个系统中的数据元素具有相同的名称。这至少允许分析员确定系统中存在多少个元素副本。

1.  2.

    数据元素名称不匹配。这要求分析员设计一个“映射”算法，跟踪每个别名的对应名称。

1.  3.数据元素通过名称匹配，但不通过属性匹配。在这种情况下，分析员必须通过跟踪不同系统中的属性定义来传播数据元素的更新。这些差异可能会变化很大。最明显的是元素长度。如果数据元素的长度比已更新的长度短，则会出现字段截断的问题。这意味着当值传播到具有较短长度定义的系统时，字符串的起始值或结束值将丢失。另一方面，如果目标长度较长，则进程必须填充字符串的开头或结尾，以便元素具有完整的值。这在图 10.18 中以图形方式表示。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig18_HTML.png](img/480347_1_En_10_Fig18_HTML.png)

    图 10.18

    传播具有不同字段长度的数据元素

    此外，相同的数据元素可能具有不同的数据类型，这意味着一个是字母数字，另一个是数字。在这种情况下，分析员需要知道某些值（例如，前导零）将根据其数据类型分类方式存储不同。

1.  4.数据元素之间不存在一对一的关系。这意味着一个系统中的数据元素可能是基于计算结果的（派生数据元素）。这将需要进行更深入的分析和映射，通常通过创建一个复制业务规则以计算数据元素值的存储过程来解决。因此，在这种情况下，可能会有简单的元素副本从一个系统移动到另一个系统，以及需要首先计算然后在多个系统之间传播的一个数据元素值。例如，如果在一个系统中输入了数据元素“总金额”，但在另一个系统中将其计算为数量乘以价格，则值的传播非常复杂。首先，分析人员必须知道计算值是在结果值之前还是之后进行的，在这种情况下，“总金额”重新输入到另一个系统中。如果是这样，那么传播就容易得多；一旦进行了计算，那么结果就会被复制到“输入”元素中。相反的情况则复杂得多。如果“总金额”已经输入，但数量和价格的值尚未输入，则在输入数量和价格之前很难传播。如果对数量、价格或总金额进行了调整，则此示例进一步复杂化。对于任何更改，系统都需要自动“触发”重新计算值，以确保它们同步。图 10.19 图形化显示了这个过程。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig19_HTML.png](img/480347_1_En_10_Fig19_HTML.png)

    图 10.19

    计算数据元素的传播

## 10.17 转换遗留基于字符的屏幕

大多数遗留系统都不使用基于图形用户界面（GUI）的字符屏幕是很天真的假设。字符屏幕指的是不使用 GUI 的屏幕。虽然现存的大多数字符屏幕都源自第三代语言的大型机实现，但也有许多早期的第四代语言系统先于 GUI 范式。不幸的是，字符屏幕通常不容易映射到其 GUI 对应物。分析人员必须特别小心，不要试图简单地复制遗留软件中的屏幕。图 10.20 显示了一个典型的基于字符的遗留屏幕。请注意，右上角显示了最多四个合同/采购订单。用户需要在单独的屏幕上输入每个合同/采购订单。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig20_HTML.png](img/480347_1_En_10_Fig20_HTML.png)

图 10.20

基于字符的用户屏幕

另一方面，在图 10.21 中的替代 GUI 屏幕利用了视图栏，允许在窗口中滚动。因此，GUI 版本仅需要一个物理屏幕，而不是四个。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig21_HTML.png](img/480347_1_En_10_Fig21_HTML.png)

第 10.21 图

将基于字符的屏幕转换为 GUI 屏幕

## 10.18 带编码的遗留屏幕值的挑战

在大多数遗留的基于字符的屏幕中，通常使用一种常见的做法来创建表示另一个更有意义的数据值的代码。例如，数字代码（1、2、3、4 等）可能用于表示产品颜色，如蓝色、绿色、深红色等。传统应用程序使用代码是因为它们减少了在屏幕上输入值所需的字符数。实现下拉菜单和弹出窗口等常见 GUI 功能的技术是不可用的。事实上，许多人出于习惯使用代码，或者必须使用代码来实现计算机系统。在过渡到 GUI 系统时，特别是在 Web 上，明智的做法是逐步淘汰任何以编码形式存在的数据元素，除非这些代码是用户定义的并且在行业或业务领域内有意义。这基本上意味着某些代码，如州（NY、CT、CA 等）是业界标准，是业务所必需的，而不是为了帮助软件实施而创建的代码——如颜色代码。在后一种情况下，颜色名称本身是唯一的，并且将存储在仅具有其描述性名称的实体中，而不是代码，然后标识实际描述。图 10.22 显示了基于字符和 GUI 屏幕的过渡。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig22_HTML.png](img/480347_1_En_10_Fig22_HTML.png)

第 10.22 图

编码值 GUI 屏幕过渡

更改包含编码值的基于字符的屏幕对数据字典，然后对逻辑数据建模具有涓滴效应。首先，删除编码值必然会从数据字典中删除一个数据元素。其次，代码通常是关键属性，这些属性成为实体的主键。因此，删除代码将删除实体的主键。新的主键可能是元素名称。然后必须对实体关系图（ERD）进行这些更改，并将其投入生产（见图 10.23）。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig23_HTML.png](img/480347_1_En_10_Fig23_HTML.png)

第 10.23 图

过渡到编码数据库

第三，在代码消除之后，会影响先前使用对编码值进行查询的存储过程。因此，分析员必须确保重新设计使用这些编码的所有查询。这个转变将会增加巨大的价值，因为编码元素通常会给查询增加不必要的开销和时间延迟。最终，消除编码值将释放大量空间和索引开销。这将提高遗留系统的性能。

## 10.19 遗留迁移方法论

正如前面所述，所有遗留系统不可避免地必须到达其原始生命周期的终点。因此，不管某些组件是否会保持“原样”或增强，最终 IT 管理部门都必须计划迁移到另一个系统。本节解决的问题是如何建立一个迁移生命周期，考虑到对企业计算机系统中各种遗留组件进行逐步替换的增量方法。前几节提供了遗留系统及其与其他系统集成的框架。本节提供了一种逐步模板程序，可以协助分析员跟踪遗留迁移计划的时间表，包括临时和永久集成。这种方法是一个逐步的方法，因此分析员可以将其用作遗留迁移生命周期中所取得进展的检查表。总共有 12 个步骤，如下所示：

1.  1。

    分析现有遗留系统。

1.  2。

    分解遗留系统，确定迁移和链接策略的时间表。

1.  3。

    设计“原样”链接。

1.  4。

    设计遗留系统增强。

1.  5。

    设计遗留系统替代品。

1.  6。

    设计和整合新数据库。

1.  7。

    确定新的基础设施和环境，包括网关。

1.  8。

    实施增强。

1.  9。

    实施链接。

1.  10。

    迁移遗留数据库。

1.  11。

    迁移替代遗留应用程序。

1.  12。

    渐进式过渡到新系统。

上述步骤在图 10.24 中有图形描述。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig24_HTML.png](img/480347_1_En_10_Fig24_HTML.png)

图 10.24

遗留迁移生命周期

请注意，有两组步骤，即步骤 3–5 和 8–10 可以并行进行。这些步骤包括可以做出的三种遗留迁移选择：替换、增强和“原样”。虽然这个生命周期看起来很简单，但实际上对于大多数迁移来说，对这些步骤及其相互作用进行策划、管理和修改是一个重大挑战。事实上，制定一个迁移计划并充分协调增量和并行步骤是一个困难的项目。接下来的章节将为这 12 个步骤提供更多详细信息。

+   步骤 1：分析现有的遗留系统

很明显，分析人员完全理解系统中存在的所有现有遗留组件非常重要。目标是提供每个系统的要求以及它与系统的关系。分析人员必须记住，几乎没有文档可用于充分表示遗留系统的架构。然而，分析人员应尽可能收集尽可能多的信息，包括但不限于：

+   用户和编程文档

+   现有用户、软件开发人员和管理人员

+   遗留系统的所需输入和输出以及已知服务

+   关于系统本身历史的任何历史视角。

无论现有信息和文档如何，都必须使用逆向工程的某些方面。应该使用各种 CASE（计算机辅助软件工程）工具，允许分析人员创建数据存储库和某些级别的代码分析，特别是针对第三代语言迁移。分析人员应为过程分析创建 DFDs 和 PFDs，为数据表示创建逻辑数据建模（LDM）和实体关系图（ERD）。分析人员还应确定哪些遗留组件是可分解的，哪些是不可分解的。无论最终决定是立即替换、增强还是保持“原样”，最终遗留系统的迁移将使现有代码几乎无一幸免（Brodie 和 Stonebraker 1995）。

+   第二步：分解遗留系统以确定迁移时间表和链接策略

遗留系统的逐步迁移最容易通过分解工程来实现。前几章概述了功能分解的过程，它基于将系统分解为其功能组件。分解导致组件的产生，也允许代码的重用。由于包系统的基本前提是可重用性，分解的过程是任何遗留迁移生命周期的强制性部分。因此，分析人员应该将所有 DFD 分解为功能原语。过程分析继续，为每个功能原语编写过程规范。这些功能原语将从现有代码或文档中重写，或者从分析程序功能中重新创建。分析人员需要删除将遗留代码中的模块链接起来的所有依赖逻辑，因为它代表了程序之间的耦合。通过从遗留代码中找到过程调用，可以通常识别模块依赖性。最终，这些过程规范将成为方法。最终，所有方法都将映射到类，并确定每个类需要的属性。虽然这听起来很简单，但对于其中一些过程，分解将是有问题的。这通常会发生在遗留代码过于琳琅满目，需要简单地重新设计的情况。在这些情况下，分析人员可能希望采访用户，了解所需的功能，而不仅仅依赖于书面遗留代码。

从数据的角度来看，实体关系图（ERD）需要进行规范化。请记住，步骤 1 中产生的 DD 和 ERD 是现有系统的镜像，这个系统很可能不是第三范式。因此，这一步将导致新实体的传播，甚至新的数据元素。此外，还将发现数据冗余以及应该从逻辑模型中删除的派生元素。然而，当这些步骤正在进行时，分析人员需要意识到规范化过程代表了数据应该最初如何设计的全新蓝图。实际上，元素的移除或物理数据库的重建需要根据整体遗留系统迁移工作的阶段计划。因此，第二步提供了分解的框架，但没有实施计划的时间表。

最后，分析人员必须始终意识到分解的挑战，特别是过度分解，意味着形成了太多的类，最终会损害系统性能。需要有各种分解级别的混合，这将作为新迁移架构的基础。

+   第三步：设计“现状”链接

这一步涉及确定和设计哪些组件将保持不变，除了与其他打包软件组件必要的链接之外。 这些模块被确定为不属于初始迁移计划的一部分； 但是，它们需要在打包软件系统基础架构内运行，并因此成为其架构的一部分。 决策的一部分需要包括数据将如何迁移到打包软件框架中。 在大多数情况下，“按原样”组件继续使用其遗留数据源。 必须考虑如何将遗留数据传输到打包软件系统中的其他组件。 分析师需要考虑早期概述的参数化通信系统或中央共享数据库存储库的使用。

+   第四步：设计遗留增强

这一步确定了哪些模块将被增强。 BPR（业务流程再造）将被用于设计每个业务领域的新功能和功能。 分析师应该确定关键组件，并确定需要采用哪些变更来使现有系统更像面向对象的系统。 还需要映射常见的流程和数据库，以便可以在遗留系统和打包软件系统之间设计共享资源。 还将需要新的链接，并且分析师必须确定是使用参数还是数据库，还是两者都用于实现应用系统之间的通信。

根据需要，用户屏幕可能还需要进行更新，特别是为了删除编码值或将某些基于字符的屏幕移到 GUI 中。 对遗留应用程序的许多增强都是基于第 1 步中执行的分析实施的。 任何修改都需要最终在遗留系统的总迁移完成后在新平台上运行。 分析师需要意识到，额外的要求意味着风险增加，应尽可能避免。 但是，在考虑增强时，几乎不可能忽视新要求。 因此，分析师需要将风险评估作为遗留迁移生命周期的一部分进行关注。

+   第五步：设计遗留替代方案。

分析师必须专注于如何在后代软件架构中重构逻辑。 因此，了解世代语言设计的差异至关重要。 本章提供了两种类型的遗留软件系统：第三代和第四代语言。 第三代语言被描述为更为程序化且更难转换。

分析员必须设计目标应用程序，使其能够根据新系统环境中将支持的业务规则和流程进行操作。由于这种整合，大多数替换传统遗留迁移需要进行重大的重新工程活动。这些活动需要包含自遗留系统投入生产以来可能已经发展的新业务规则。此外，新的业务规则可以简单地通过成为打包软件系统的要求而创建。

遗留迁移的另一个重要组成部分是屏幕设计。当替换遗留系统时，分析员必须将迁移视为同化，即，旧系统正在成为新系统的一部分。因此，必须审查所有现有的打包软件屏幕，以便设计师确定它们是否需要修改以采用一些遗留功能。这并不意味着所有遗留系统屏幕都将被吸收到现有的打包软件系统中。相反，将在目标环境中添加一些新功能和吸收的功能的组合。

+   第六步：设计和集成新数据库

从企业的角度来看，分析员必须收集所有现有的遗留系统排列组合，并设法提供如何将数据整合到一个源中的计划。对于“现状”解决方案，遗留数据文件很可能会与打包软件系统分开，直到完整的遗留系统迁移完成。然而，增强和替换遗留数据的过程应该旨在创建一个将为整个打包软件企业系统提供服务的中央数据库源的目标。实际上，中央数据源减少了数据冗余，并显著提高了数据完整性。

数据集成的过程只能通过“合并用户视图”来完成，这是将重叠的多个数据元素定义进行匹配并识别数据冗余和备选定义的过程。这只能通过创建数据元素存储库并使用 ERD 图形化地表示数据来完成。一旦每个系统以这种方式表示，然后分析员必须按照第九章的规定执行逻辑数据建模。结果将是创建一个能够提供成功的打包软件实现所需的集成类型的一个中央数据库系统集群。

尽管这是所有分析师的目标，但成功实施的道路是具有挑战性的。首先，规范化过程将要求删除一些数据元素（例如，编码值），而其他数据元素则需要添加。其次，直到所有替换屏幕完成，才能实现完全的数据集成。第三，必须重新设计应用程序，以假定数据源的中心性存在。由于这个过程可能非常耗时，因此可能无法一次性尝试完全的数据库迁移。因此，可能需要逻辑分区遗留数据，以便促进增量数据库迁移。因此，将创建的遗留数据子集保持独立于中央数据库，直到一些后续迁移阶段被认为可行。当然，这种策略需要设计临时“桥梁”，以使整个打包软件系统对用户看起来是连贯的。

在规划数据迁移时，另一个重要因素是确定对遗留数据本身了解多少。了解越少，遗留数据和打包软件数据需要分别并行运行的时间就越长。

+   第七步：确定新基础设施和环境，包括网关。

在迁移任何系统之前，必须计划并安装必要的硬件和软件基础设施。遗留迁移中的一个常见错误是没有考虑提供这种基础设施的时间和精力。此外，这个过程可能会创建一个新的网络环境，需要确定在三层客户/服务器平台中放置软件的位置。这意味着可能需要进一步分解所有流程，特别是对象类。您可能还记得第八章中提到的类可能会根据需要在网络中分解应用程序。

另一个重要因素是性能。在许多情况下，网络工程师很难预测大型应用系统环境中的性能。在设计阶段的早期可能需要计划进行几个性能基准测试。基准测试是设置一个复制生产网络的环境，以便在必要时对系统设计进行修改以提高性能的过程。

此时必须做出的另一个决定是是否创建网关基础设施来调解遗留层。当然，这个决定高度依赖于迁移生命周期；随着时间推移逐步引入更多的遗留层，数据和应用程序的网关处理器可能会更加必要。决定选择网关是重要的，不仅从软件设计的角度来看，还涉及网络基础设施。建立网关可能非常昂贵。这涉及从头编写系统或调整商业产品以满足迁移要求。此外，由于需要优化网关服务器性能，所以需要大量额外的硬件，这也是昂贵的。然而，网关的好处是实实在在的，因为它可以为缓慢迁移新系统环境中的所有组件提供可靠的结构。

+   第 8 步：实现增强

这一步需要一个时间表，说明遗留增强将何时实施并成为生产系统的一部分。许多分析师建议首先将最简单的模块投入生产，以便能够快速有效地解决任何意外问题。此外，简单的模块倾向于在处理或性能方面出现问题时有较小的后果。然而，还有一些协调方面的问题。例如，那些依赖相同数据或使用相同子系统的增强显然应该同时实施。

影响决定哪些增强型组件先行的另一个因素与其对其他子系统的影响有关。这意味着优先级的确可能受到其他系统需要或依赖其他系统的影响。另一个问题可能是遗留链接的性质。如果一个链接非常复杂或依赖于其他子系统的增强，其计划可能会受到影响。最后，增强型的性质对决策有很大影响，而不仅仅是应用的复杂性。可能有些简单的增强对打包软件系统至关重要，反之亦然。

+   第 9 步：实现链接

正如我在第 8 步中所暗示的，遗留链接的确定对迁移周期的安排有很大影响。一旦在第 8 步中确定了这一点，相关的遗留链接必须放置好。这也可能意味着网关，如果设计好了，也必须运行，因为许多链接可能会通过网关基础设施进行过滤。因此，遗留链接的实现既涉及硬件又涉及软件。不管网关是否就位，数据库链接通常需要单独的服务器。在许多情况下，由于这些“服务器”与互联网进行接口，有必要安装防火墙以确保安全保护。

从软件的角度来看，传统链接几乎可以像转换程序一样对待。需要进行大量的测试以确保它们正常工作。一旦传统链接投入生产，就像数据转换一样，它们往往会持续工作。确保对传统链接进行文档化也很重要。事实上，任何链接最终都会根据增量迁移时间表进行更改。请记住，大多数传统链接都是通过建立临时“桥梁”来完成的。临时概念可能是危险的，因为这些链接中的许多，随着时间的推移，往往会变得更加永久。也就是说，它们的临时寿命有时会超出永久组件的预期寿命。这里的信息应该是，传统链接，虽然它们是一种临时解决方案，但应该以与任何其他软件开发组件相同的强度和质量坚持进行设计。

+   第 10 步：迁移传统数据库

数据迁移如此复杂，以至于应该将其作为迁移生命周期中的一个单独而独特的步骤来处理。数据影响系统中的一切，如果不正确地迁移，往往会引起巨大问题。首先，分析员必须根据应用程序迁移的时间表决定数据的分阶段迁移。希望数据迁移的过程应该与第 8 和第 9 步并行进行。

数据迁移最具挑战性的方面是过程中的物理步骤。迁移新实体和模式更改是复杂的。例如，对数据库的更改要求“删除”表，意味着它们被脱机。数据字典需要更新，对存储过程和触发器的更改非常耗时。最麻烦的是质量保证过程。虽然一些测试可以在受控环境中进行，但大部分最终测试必须在系统实际投入生产后进行。因此，与用户协调及早测试系统至关重要。此外，必须制定备份程序以防数据库迁移不正常。这意味着如果出现重大问题，有一种备用的安全失败计划可以重新安装旧系统。最后，一个编程团队应该准备好处理出现的任何问题，这些问题不值得重新安装旧版本。这可能包括发现可以在合理时间内修复且不被视为关键运营问题的应用程序“错误”（这意味着通常有问题的“解决方案”）。分析员必须明白，每次进行新的数据库迁移时都必须遵循这个过程！

当存在网关时，数据库迁移变得更加复杂。原因在于，从增量的角度来看，每次迁移时网关都包含着越来越多的数据库责任。因此，对于每次迁移，潜在受影响的数据量都会变得更大。此外，通常情况下集成的数据量会呈指数增长，因此规划和转换过程成为成功迁移生命周期的关键路径。由于随着项目的推进，遗留数据库的迁移变得更加困难，因此生命周期的结束变得更加具有挑战性。这就是为什么许多迁移从未完成的原因！

+   步骤 11：迁移替换的遗留应用程序

一旦数据库迁移完成，剩余的遗留应用程序就可以迁移到新系统上了。这些应用程序通常是替换组件，已经在面向对象的范式下进行了重新设计。然后，这些程序已经被设计为针对新功能要求的目标数据库运行，以适应打包软件系统。由于替换应用程序通常不会创建链接，因此通常对网关操作影响不大。更具挑战性的是质量保证过程。用户需要意识到代码相对较新，并且无论进行了多少预生产测试，都会存在问题。无论如何，程序员、数据库管理员和质量保证人员都应该在系统过渡后的数周内随时待命。

+   步骤 12：逐步过渡到新系统

如上所述，测试和应用交接是经常被忽视的两个领域。因为项目通常超出预算和进度，所以最终的程序，比如测试和验证，通常会被缩短。这种决定的结果对于成功的遗留系统迁移可能是毁灭性的。由于许多打包软件系统的规模和复杂性，完全“戒断”是不现实和不负责任的。因此，分析师应考虑提供能够更有信心表明系统准备好过渡的测试场景。这种方法称为“验收测试”，并要求用户参与确定在系统准备上线之前必须执行哪些测试。因此，验收测试计划可以定义为一组测试，如果通过，则确定软件可以投入生产使用。验收测试需要在产品生命周期的早期建立，并应在分析阶段开始。那么，逻辑上只有验收测试计划的制定应该涉及分析师。与需求开发一样，分析师必须与用户社区合作。只有用户才能最终决定测试计划的内容和范围。验收测试计划的设计和开发不应与软件开发生命周期的测试阶段混淆。

对验收测试的另一种看法是，它成为了一个正式的检查清单，定义了逐步迁移系统的最低标准。然而，必须认识到没有新产品会是无缺陷的。测试所有内容的排列组合将使完成时间表不可接受并且成本高昂。因此，验收测试计划是一个策略，以便对最重要的组件进行足够完整的测试以进行生产。图 10.25 代表了一个样本验收测试计划。![../images/480347_1_En_10_Chapter/480347_1_En_10_Fig25_HTML.png](img/480347_1_En_10_Fig25_HTML.png)

图 10.25

验收测试计划

## 10.20 问题和练习

1.  1.

    什么是遗留系统？解释。

1.  2.

    描述五代语言。每一代都会增加什么？

1.  3.

    什么是基本组件？

1.  4.

    什么是面向对象的范式的意思？

1.  5.

    面向对象与业务领域分析有什么关系？

1.  6.

    什么是遗留链接？

1.  7.

    解释逻辑重构的概念。

1.  8.

    什么是 UNIX 管道？

1.  9.

    解释遗留集成是如何通过网关架构进行的。

1.  10.

    什么是传播？

1.  11.

    字符界面和图形用户界面之间的基本区别是什么？

1.  12.

    什么是编码值？

1.  13.

    对象和 API 之间有什么关系？

1.  14.

    CRUD 在区块链架构中的限制是什么？为什么在基于分类帐的系统中这种差异如此重要？