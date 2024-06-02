第四章：JavaScript 和 JQuery 让我们学习 JavaScript 最重要的一些特性，以便更好地理解它是如何工作的。第一个特性是变量。变量就像值的存储容器。数据可以放入这些容器中，然后您可以通过给容器命名来引用它。每个值得编程任务都需要一个变量。如果值不能改变，您的网页将不够交互。在 JavaScript 程序中使用变量之前必须声明变量。在 JavaScript 中，变量的关键字（如第一章所示）是 var。<script type= “text/javascript”>​<! --​var age;​var race;​// -- ></script>您还可以使用相同的关键字声明不同的变量。看起来是这样的：<script type= “text/javascript”>​<! --​var age, race;​// -- ></script>（JavaScript - 语法，n.d.）变量初始化发生在我们将值存储在变量中时。您可以在任何时候添加值。我们创建了一个名为 race 的变量，因此我们可以在以后的时间点为其添加值“black”，并且可以在初始化时添加年龄的值。看起来是这样的：<script type= “text/javascript”>​<! --​var age = “39”var race;race= black;​// -- ></script>（JavaScript - 语法，n.d.）var 关键字只需要在初始化时使用一次。变量的作用域是定义变量的程序区域。在 JavaScript 中，只有两种：●     全局变量 - 可以在 JavaScript 代码的任何地方定义。● 局部变量 - 仅在定义它的函数的范围内可见。局部变量优先于函数体内同名的全局变量。当局部变量或函数参数与全局变量同名时，全局变量实际上被隐藏。例如：<html>​<body onload = checkscope();>​<script type = “text/javascript”>​ <! --​var myVar = “global”; // 全局变量​function checkscope( ) {​var myVar = “local”; // 局部变量​document.write(myVar);​}​// —-></script><body><html>（JavaScript - 语法，n.d.）有关命名变量的规则。您变量的名称区分大小写，因此 race 和 Race 是两个不同的变量。变量名不能以数字开头。它们必须以字母或下划线开头。如果您的变量名为 345age，那么它将无效。但如果它被命名为 _345age，它将有效。有一些 JavaScript 保留关键字不能用作变量名。列表如下：

| abstract | boolean | break | byte | case | catch |
| --- | --- | --- | --- | --- | --- |
| char | class | const | continue | debugger | default |
| delete | do | double | else | enum | export |
| extends | false | final | finally | float | for |  |
| function | goto | if | implements | import | in |
| instanceof | int | interface | long | native | new |
| null | package | private | protected | public | return |
| short | static | super | switch | synchronized | this |
| throw | throws | transient | true | try | typeof |
| var | void | volatile | while | with |  |

(JavaScript - Syntax, n.d.)大部分应用程序正常工作是因为客户端和远程服务器之间的交互。客户端指的是最终用户设备。客户端向服务器请求数据，服务器接收并处理请求，然后客户端以可读格式获取数据。在大多数情况下，我们确实需要客户端服务器模型，但使用 JavaScript 可以完全避免它。JavaScript 有助于通过在不需要服务器输入的情况下验证表单来减少流量。JavaScript 引擎是将源代码转换为计算机可以理解的语言的程序。所有现代浏览器都带有 JavaScript 引擎，每个引擎都有两个组件：MemoryHeap 和 Call Stack。MemoryHeap 是在任何给定时间分配内存的地方。Call Stack 处理从脚本中添加到它的信息。JavaScript 框架 JavaScript 的框架使语言能够在最小的设置下表现最佳。它们为开发人员提供了创建 JavaScript 应用程序所需的构建块。这些构建块是一组代码库。这些库会生成代码，调用特定功能，用于开发的应用程序类型。框架建立了整个应用程序的结构。有几个 JavaScript 框架，但最流行的是：

| Node.js | Node.js 是一个跨平台、开源的后端 JavaScript 运行环境，它利用 V8 引擎在 Web 浏览器之外执行 JavaScript 代码。 |
| --- | --- |
| Vue.js | Vue.js 是一个开源的 JavaScript 框架，用于创建用户界面和单页应用。它使用模型-视图-视图模型（MVVM）架构模式。 |
| AngularJS | AngularJS 是一个基于 JavaScript 构建单页应用的开源前端框架。 |
| Ember.js | Ember.js 是一个用于构建 Web 应用的开源 JavaScript 客户端框架。它通过提供包括数据管理和应用程序流程在内的综合解决方案，使客户端应用程序的开发成为可能。 |
| React | React 是一个前端 JavaScript 工具包，用于使用 UI 组件创建用户界面。React 可用作创建单页或移动应用的基础。 |

(JavaScript - 语法，无日期)JQuery 的特性 HTML 操作 JQuery 允许用户访问 DOM，因此可以操作 HTML 文档中的元素。DOM 操作 JQuery 提供对 DOM 的 API 访问，以便对 HTML 文档进行任何必要的更改。您可以随意添加、删除和重新排列元素。通过这样做，您的网页可以显示更新的信息，而无需多次刷新页面。CSS 操作 JQuery 库具有可以用于控制和更改 CSS 和 DOM 元素的代码行。效果和动画 JQuery 有一个使添加不同效果和动画更容易的动画函数。它还允许您通过操作 CSS 来对 HTML 元素进行动画处理。这些效果的示例包括：显示、隐藏、淡入、淡出和滑动。AjaxAjax 代表异步 JavaScript 和 XML。它让您可以将来自服务器或数据库的内容放到您的网站上，而无需每次刷新网站。如果您正在访问一个不断接收数据的网站，每次都需要刷新页面将会非常不方便。实用程序实用程序是优化计算机性能的软件程序。一些实用程序非常适合保持计算机无病毒，而其他实用程序则只是让桌面看起来不错。JQuery 可以被认为是传统的代码，因为它是在 2006 年引入的。它经受了时间的考验，并可用于今天存在的大多数应用程序中。JQuery 在大多数 Wordpress 站点上都被使用，如果没有则全部。截至 2022 年，有整整 45.5 亿个站点在使用。它可以教会您很多关于 JavaScript，并且是最容易使用的编码库。
