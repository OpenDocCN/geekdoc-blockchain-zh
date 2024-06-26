© 作者（S）独家许可给 Springer Nature Switzerland AG 2021 年 Y. Maleh et al. (eds.)未来网络安全应用的人工智能和区块链 Big Data 研究[`doi.org/10.1007/978-3-030-74575-2_9`](https://doi.org/10.1007/978-3-030-74575-2_9)

# AntiPhishTuner：针对钓鱼网址检测的参数调优的多级方法

Md. Fahim Muntasir^(1, 2  ), Sheikh Shah Mohammad Motiur Rahman^(1, 2  ), Nusrat Jahan^(1  ), Abu Bakkar Siddikk^(1, 2  ) 和 Takia Islam^(1, 2  )(1)软件工程系，孟加拉国达菲迪尔国际大学，达卡(2)nFuture 研究实验室，达卡，孟加拉国 Md. Fahim Muntasir（通讯作者）电子邮件：fahim35-1900@diu.edu.bdSheikh Shah Mohammad Motiur Rahman （通讯作者）电子邮件：motiur.swe@diu.edu.bdNusrat Jahan 电子邮件：nusrat.swe@diu.edu.bdAbu Bakkar Siddikk 电子邮件：abu35-1994@diu.edu.bdTakia Islam 电子邮件：takia35-1014@diu.edu.bd

## 摘要

钓鱼是网络犯罪分子之间的一个令人担忧的问题。在过去的十年里，在线服务已经彻底改变了世界。由于网络服务的革命性转变，人们对网络的依赖日益增加。由于对在线导向的依赖日益增加，安全威胁已经出现。有许多种类型的反钓鱼解决方案是由许多研究人员提出的。然而，本章旨在提出一种智能框架，以基于优化学习体系结构方案的方式检测钓鱼网址。采用了基于多层结构的深度神经网络（DNN）、神经网络（NN）和堆叠来检测钓鱼网址。这些体系结构是通过对各种调整超参数进行评估来实现的，以获得名为 AntiPhishTuner 的优化输出。因此，基于五层 DNN 的结果可以提供 0.95 的准确度，最小均方误差（MSE）0.30，以及平均绝对误差（MAE）0.074，其中周期数为 50，优化器为 Adam。使用两层 NN 和 AdaGard 优化器可以提供 0.95 的准确度，MSE 为 0.30，MAE 为 0.074\. NN 通过 150 个周期提供这些结果。堆叠泛化在二进制分类中可以达到 0.97 的最大准确度，MAE 为 2.1\. 本章可以为研究人员和反钓鱼工具开发者提供更好的引导，使他们能够就应该遵循的方法做出初步决定，以进行进一步扩展。

关键词统一资源定位符（URL）钓鱼深度神经网络（DNN）神经网络（NN）堆叠

## 1 引言

**钓鱼**是一种欺诈技术，既涉及社会工程学，又涉及技术工程，目的是窃取用户身份和个人账户信息以及金融账户的凭据 Huang [22]。有各种各样的钓鱼形式，包括算法、链接处理、电子邮件钓鱼、域欺骗、使用 HTTPS 的钓鱼、短信钓鱼、弹出窗口。前缀、后缀、子域、IP 地址、URL 长度、'@' 符号、鱼叉式钓鱼、双斜线属性、端口、https 令牌、请求 URL、URL 锚、标签链接、域名年龄是钓鱼的特征 Rahman [13]。

**钓鱼平台**的元素通常在字面上和外观上与几个合法网站相当。如今，由于钓鱼活动的增加，安全问题越来越受到关注。根据华盛顿一家知名的网络安全公司 F5 Systems, Inc. 的说法，该公司在目标选择、社会学和技术渗透方面留下了它的印记，钓鱼者的策略结合了三个特殊任务 Pompon [23]。根据反钓鱼工作组的说法，2006 年 3 月有 18,480 次重大的钓鱼攻击和 9666 个奇怪的钓鱼域。它影响了数十亿个网站客户，对企业造成了巨大的成本障碍 Viktorov [24]。全球计算犯罪的未来支出可能达到惊人的 5000 亿美元，根据微软在 2018 年的证据，一个线索泄露将使普通组织遭受约 380 万美元的支出。

研究人员提出了几种解决方案。例如，通过分层聚类方法检测钓鱼网站，该方法将从 DOM 产生的向量聚集在一起，根据它们的相应距离进行聚类，Cui [25]。一些考虑集中在利用 URL 的潜在特征来检测钓鱼 URL 上。神经网络通常使用一到两个隐藏层。在某些深度学习的情况下，层数会有所不同。但是它需要近 150 层以上的 Le [11]。有一些规则来决定层数，其中包括用于基本数据集的两层或更少的层，以及用于计算机视觉、时间序列或复杂数据集的额外层可以获得更好的结果 Rahman [13]。大多数情况下，分类数据模式是以结构化方式可访问的。但是 URL 信息并不以固定模式可访问。将分类方法或机器学习技术应用于 URL 数据。通过这种方式，应该使用额外的方法来管理 URLs Woogue [26]。钓鱼是网络安全中的一个关键问题。钓鱼检测技术通过各种 URL 评估来识别 URLs。关于评估 URLs，有许多方法可供选择。在可用方法中，机器学习技术更加有效和准确。通过这些技术，恶意 URL 的模式通过分类算法变得熟悉，当需要时，它可以区分是钓鱼还是合法的 URLs Dong [6]。Phish tank 数据库是一个标准收藏，跟踪各种网络安全组织报告的钓鱼 URLs。这个数据库存储了各种特征 Mohammad [27]。

钓鱼是最为人知的网络安全威胁，可以称之为犯罪活动的欺诈性实践。这是钓鱼攻击者的主要关注点。通常，钓鱼攻击者模仿合法网站以获取用户的凭证信息，例如在线银行、电子商务网站，以便用户透露其敏感信息，例如姓名、密码、登录凭证、信用卡信息、与健康相关的信息等，这些都是模仿网站。攻击者收集用户信息，并通过钓鱼攻击进行各种欺诈活动 Abutair [1]。

URL 在钓鱼攻击中起着重要作用，攻击者通过各种通信渠道（例如电子邮件、社交媒体等）向用户发送恶意 URL，并发送的 URL 看起来像是一个有效的 URLs Shirazi [17]。

通常，有三种方式用来利用钓鱼攻击 Hutchinson [9]。首先，模仿合法的网络界面，看起来完全像合法界面，被称为基于网络的钓鱼。考虑到它是有效的，网络钓鱼者欺骗用户提供凭据信息。其次，攻击者使用基于网络的技术通过电子邮件发送钓鱼内容。第三种方式是钓鱼攻击也是通过恶意软件为基础的，攻击者向用户系统注入恶意代码 Dong [6]。无论哪种情况，为什么使用基于机器学习的反钓鱼框架进行钓鱼检测？因为为了检测那些钓鱼攻击，一些传统方法如黑名单、正则表达式和签名匹配被使用，然而这些方法无法检测未知的 URL Rahman [13]。

检测恶意 URL 数据库签名的未知模式始终保持更新。然而，通过对基于机器学习的恶意 URL 检测研究数量的扩展，观察到深度学习架构比现有的机器学习算法提供更好的性能 Harikrishnan [10]。

本章的主要目标可以概括如下：

+   使用调优器对神经网络以及深度学习（深度神经网络）进行 AntiPhishTuner 的评估。

+   通过堆叠概念实现了钓鱼网址检测，以提高准确性。

+   结合所有类型的分类可以执行钓鱼堆叠，如机器学习、集成学习和基于神经网络的方法作为基本分类。

+   用优化调整来表达智能反钓鱼体系结构。

+   神经网络技术中学习率的影响。

+   评估训练准确率与学习率变化的关系。

+   检测适合开发 DNN 和 NN 结果的优化参数。

+   检测自适应学习优化算法与 DNN 和 NN 的组合。

本文的剩余部分安排如下：第二部分表示文献综述。在第三部分中，描述了使用多层方法检测钓鱼网址的方法以及用于实验和评估的数据集信息。在第四部分中识别和分析了实验、评估参数以及获得的结果。最后，第五部分总结了本文。

## 2 文献综述

Adebowale [2] 提出了一个普通的技术，即有些用户从网站上窃取机密信息，并称这些用户是钓鱼用户。这种活动通常发生在伪造网站或恶意 URL 上，被称为欺诈性行为。网络犯罪分子利用欺诈行为创建精心设计的钓鱼攻击。访问受害者的系统，网络犯罪分子可能安装恶意软件或不当地保护用户系统。

Acquisti [4]建议减少网络钓鱼攻击的威胁，指出要针对网络钓鱼攻击的风险，建议采取各种策略来准备和教育最终用户识别网络钓鱼网址。

Wang [20]建议对电子邮件过滤器使用集成分类器，排除了五种算法，分别是支持向量机、K 近邻、高斯朴素贝叶斯、伯努利朴素贝叶斯和随机森林分类器。

最终，随机森林的准确率从 94.09%提高到了 98.02%。Gupta, S.和 Singhal, A. [8]建议，对于最短执行时间，随机森林树是检测恶意 URL 的一种令人钦佩的策略。

Vrbančič [19]建议设置基于群体智能技术的深度学习神经网络的参数。之后，所提出的技术应用于网络钓鱼网站的分类，并通过与现有算法的比较能够更好地检测出。

El-Alfy, E. S. M. [7]建议为培训节点系统应用无监督和监督算法。网络钓鱼网站依赖于可行性神经网络和聚类 K 中心点。使用特征选择和模块来减少空间容量，使用 K 中心点技术。通过所需技术，30 个特征达到了 96.79%的准确率。

Le [11]建议对 DNN 进行训练，采用暗示的深度堆叠。对过去框架的估计覆盖范围进行优化，因为它们在每个 DNN 训练周期的结尾处，并且，更新后的估计蒙版为其他周期内的 DNN 训练提供了额外的输入。在测试阶段，DNN 以迭代的方式连续进行预测。此外，我们建议使用 L1 损失进行训练。内含。

Winterrose [21]声称探索真实外贸方法的不同属性，以识别网络钓鱼网址。使用深度玻尔兹曼机（DBM）、堆叠自动编码器（SAE）和深度神经网络（DNN）等深度学习方法来识别网络钓鱼网址。DBM 和 SAE 用于对模型进行预训练，以更好地描述数据以进行属性确定。DNN 用于在识别模糊网址时进行二元分类，即将其判定为网络钓鱼网址或真实网址。所提出的方法在高于其他机器学习技术的大多数误报率的情况下，达到了 94%的更高区域率。

Rahman [30] 建议，在几个反钓鱼系统中检测钓鱼攻击的原因是由于缺乏正确选择机器学习分类器，使用了六种机器学习分类器（KNN、DT、SVM、RF、ERT 和 GBT）和三个公开可访问的具有多维属性的数据集。使用混淆矩阵、精确率、召回率、F1 分数、准确率和误分类率来评估分类器的性能。发现随机森林和极端随机树的性能最佳，分别为 97%和 98%的准确率来检测钓鱼 URL。梯度提升树对多类特征集提供了 92%的准确率，性能最佳。

Sahingoz [31] 提出了一种实时反钓鱼过程，结合了七种不同的分类算法，还使用了不同的特征集。通过使用基于自然语言处理的随机森林算法，观察到了 97.98%的准确率。

## 3 反钓鱼调谐器：提出的方法

提出的方法已在图 1 中描述，并在本节中逐步详细描述。表 1

数据集信息

| 数据集的总特征数 | 30 个特征 |
| --- | --- |
| 总 URL 数量 | 11,055 个 URL |
| 钓鱼网址 | 4898 |
| 合法的网址 | 6157 |

### 3.1 数据集

用于训练或创建体系结构的公开可访问数据集。此模型的初始部分是收集数据并分析数据集。该数据集是从 UCI 存储库中收集的。它总共有 11055 种不同类型的 URL。共有 30 个特征用于训练模型 Rahman [14]。表 1 表示所使用数据集的各个方面。表 2

基于地址栏的特征

| 特征名称 | 解释 |
| --- | --- |
| IP 地址 | 如果 IP 地址被用作 URL 中域名的替代，则为钓鱼网站，用户几乎可以确定有人试图窃取他的凭据信息。从这个数据集中，发现有 570 个 URL 带有 IP 地址，占数据集的 22.8%，提出了一个规则，即 URL 中有 IP 地址则称为钓鱼，否则为合法。 |
| URL 的长度 | 长 URL 主要用于覆盖地址栏中的可疑部分，因为它包含恶意内容。从逻辑上讲，无法确定识别合法 URL 和钓鱼 URL 的长度是否有充分依据。因此，提出了 URL 的合法长度为 75。在本研究中，为了保证测量准确性，测量了此数据集中 URL 的长度是否可疑、合法或钓鱼网站，并提出了一个平均长度。根据提出的条件，URL 长度小于或等于 54 则被归类为合法，如果 URL 长度大于 74，则属于钓鱼。根据数据集，发现了长度大于或等于 54 的 URL 有 1220 个 |
| TinyURLs | 为了缩短 URL 长度，使用 TinyURL。它将大多数页面重定向到单击较短 URL。此界面类似于钓鱼站点，因为它将最终用户重定向到假站点而不是真实站点 |
| 操作 @ 符号 | Web 浏览器主要忽略与 @ 符号附加的部分。因为它远离真实地址。根据数据集，发现具有 '@' 符号的 90 个 URL 仅占总数的 3.6% |
| 操作“//”符号 | 在 HTTP 或 HTTPS 后，使用“//”符号作为合法的 URL。如果在初始协议声明后存在，则认为是钓鱼 URL。 “//”符号用于重定向到其他网站。 |
| 由“-”符号分隔的域名前缀或后缀 | 如果任何 URL 在其域名中包含“-”符号，则认为是钓鱼 URL。通常，经过验证的 URL 不包含“-”符号 |
| 在域中操作“.”符号 | 当添加域名的子域时，必须包含点。如果掉出多个子域并且大于那个大小，将指向它像是钓鱼 |
| 具有安全套接字层的 HTTPS | 大多数合法网站使用 HTTPS 协议，证书的年龄对于使用 HTTPS 非常重要。因此需要受信任的证书 |
| 域的到期日期 | 主要域名具有较长的到期日期，适用于合法站点 |
| Favicon | 当从外部加载时，Favicon 可以将用户重定向到可疑网站。它通常用于网站，是一种图形图像 |
| 利用不必要的端口 | 钓鱼者不断发现漏洞，并试图利用任何具有不必要的开放端口的 URL |
| 域中的超文本传输协议 | 如果此网站的任何 URL 具有 HTTPS，则认为是钓鱼网站 |

### 3.2 功能描述

在分析特征选择部分之前，需要评估功能和使用这些功能的能力。基本上，有四个主要功能和总共 30 个子功能。根据详细信息，每个功能提供有关网站可能是钓鱼、合法或可疑的详细信息。此段提供了强调这些功能的计划。

**1\. 基于地址栏的特征:** 地址栏，即 URL 栏或位置栏，是显示当前 URL 的 GUI 设备。根据数据集，它有 12 个子功能。请参见下表 2。|

**2\. 基于异常的特征:** 它主要关注网站上的异常活动。根据数据集，它有 5 个子功能。请参见下表 3。Table 3

基于异常的特征

| 功能名称 | 说明 |
| --- | --- |
| 请求 URL | 如果页面包含大量来自其他域的 URL，则认为是可疑或钓鱼的 |
| 锚文本的 URL | 类似于请求 URL 特性，使用更多的<a>标签在网站内使用时，钓鱼的可能性会增加 |
| (Meta, script, Link)标签之间的链接 | 根据其包含的外部链接数量，标签中包含大量外部链接时被认为是可疑或钓鱼的 |
| 服务器形式处理程序 | 如果服务器形式处理程序为空，则被认为是钓鱼。服务器形式处理程序重定向到不同的域，这被视为可疑 |
| 提交信息的电子邮件 | 与服务器不同，将 Web 表单定向到个人电子邮件提交信息被视为钓鱼 |
| 异常的 URL | 如果 URL 中不包含字符，则被视为钓鱼 |

**3\. 基于 HTML 和 JavaScript 的特性：** 根据数据集，它有 5 个子特性。见下表 4 。表 4

基于 HTML 和 JavaScript 的特性

| 特性名称 | 解释 |
| --- | --- |
| 转发网站 | 如果发生多次重定向，则可能会让人害怕 |
| 状态栏的自定义 | 通过“Mouseover”事件可以修改 URL 的状态栏。它会持续显示真实的 URL 并隐藏伪造的 URL。当应用于网站时，这会被视为钓鱼 |
| 禁用右键点击 | 用户无法检查源代码；右键点击功能主要由钓鱼者禁用。当网站中禁用该功能时，这是作为钓鱼的 |
| 弹出窗口 | 具有文本字段的弹出窗口由网页组成，这是作为钓鱼的 |
| 定制 IFrame | 将它们隐藏在网站钓鱼者中可以利用 IFrame。通常来说，将外部内容连接到 IFrame 使用的域中以显示 |

**4\. 基于域的特性：** 使用域名准备易于识别和记忆的数字名称。根据数据集，它有 7 个子特性。见下表 5 。表 5

基于域的特性

| 特性名称 | 解释 |
| --- | --- |
| 域名年龄 | 如果域名的年龄超过六个月，则倾向于将合法网站视为钓鱼网站 |
| DNS 记录 | 如果网站中不包含 DNS 记录，则强烈建议作为钓鱼网站 |
| 网站流量 | 大量人们访问网站主要是因为它可能具有较高的排名。排名可以识别一个地址是否是钓鱼的。钓鱼网站往往比排名较高的网站具有更低的几率 |
| 页面排名 | 大多数情况下，钓鱼网站没有 PageRank 值，因为该值是根据其重要性分配的 |
| 谷歌索引 | 在谷歌索引中具有标题的网站可以被接受为合法网站 |
| 报告统计 | 在事件中猜测它是否为网络钓鱼网页，如果网页的任何部分在任何击败网络钓鱼 IP 或域中有位置 |
| 加入表明页面 | 网络钓鱼网站禁止有指向它的链接，因为它的生命周期较短 |

### 3.3 深度学习算法

这项研究考虑了五种自适应优化器，例如随机梯度下降（Stochastic Gradient Descent，SGD）、ADAM、ADADELTA、ADAGARD 和 RMSPROP，用于对 NN 和 DNN 进行评估。

### 3.4 机器学习算法

这项研究考虑了一些用于堆叠的机器学习算法，例如支持向量机（Support Vector Machine，SVM）、决策树（Decision Tree，DT）、朴素贝叶斯（Naive Bayes，GNB）、线性判别分析（Linear Discriminant Analysis，LDA）、随机森林（Random Forest，RF）、多层感知器（Multilayer Perceptron，MLP）、随机梯度下降（Stochastic Gradient Descent，SGD）、逻辑回归（Logistic Regression，LR）、k 近邻（k nearest neighbors，KNN）和高斯，用作堆叠泛化的基本分类器的第一步，并且使用了 10 折交叉验证 Adebowale [3]。在这里，XGBoost 分类器被用作第二步中的元估计器进行最终预测。

### 3.5 模型生成阶段

上述方法表明了三种多层次方法：NN、DNN 和堆叠泛化。该模型的主要目的是通过应用堆叠技术和神经网络以及深度神经网络对处理后的数据集进行评估，确定最佳输出，并提出基于该输出的优化模型。

现在，通过在该数据集上应用神经网络和深度神经网络技术，将提供一个优化的输出。

在从数据集加载特征后，数据集被分成两部分，测试集和训练集。训练集部分分别应用于两层神经网络架构和 Somesha [16] 的五层深度神经网络架构。

由于数据集是二进制类型的，对于二分类问题，非线性激活函数 ReLU 已经被用于隐藏层的神经元，而 Sigmoid 函数已经被用于输出层的神经元 Vrbančič [19]。根据这个架构，这里使用了五种类型的自适应优化器。

下一步是使用这些自适应优化器编译模型。然后，通过分割训练集将其分为两部分，训练和验证。使用一些周期和早期停止技术来适应模型，以防止过拟合。现在通过使用测试集评估两个模型可以得到两个输出。应用这种方法后，堆叠泛化技术已经在数据集中应用。

堆叠的评估技术已在图中描述。这是一种多层次方法。堆叠通常分两步进行。在第一层堆叠中，使用基于分类器的 k 折交叉验证提供临时预测，并且输出概率预测被揭示。在系统形成期间，第一步的输出预测和临时预测在第二步中使用。Phish 堆叠的估计理论如下所述 Rahman [14]:![../images/507793_1_En_9_Chapter/507793_1_En_9_Fig1_HTML.png](img/507793_1_En_9_Fig1_HTML.png)

图 1

针对钓鱼 URL 检测的方法论

+   在使用基分类器进行堆叠的第一步中，根据第二步的预期预测来预测训练集和测试集，然后将其视为特征。

+   堆叠是一种多层方法，因此可以使用任何类型的算法在两个步骤中进行预测。

+   该提出的系统使用 k 折交叉验证，以避免过拟合该训练集，并且在训练部分的每个折叠中，它可能使用折叠外的数据进行预测。根据这个提出的模型，k 折交叉验证中使用值 3 到 10，最后使用测试集提供输出。

在培训数据结束时的第一步中，使用测试集预测输出。这一次，它使用了所有折叠技术，这需要对所有折叠中的所有值进行平均以进行估计。

在第二步中，连接到另一个称为元估计器的分类器，它在训练集上执行终端预测，从测试集中进行预测。这种方法需要额外的时间，因为它再次添加了一个分类器来进行其性能。当第一步中进行 k 折交叉验证时，预测尚未完成，这些在第二步中完成。

从上述多层技术中获得三个输出，然后根据输出的值选择模型。基于该模型提出了优化的架构。表 6

评估参数

| 评估参数 | 评估参数公式 | 评估参数说明 |
| --- | --- | --- |
| 平均绝对误差（MAE） | ![$${\text {MAE = }}\frac{{\sum \nolimits _{{i = 1}}^{n} {\left | # {y_{i} - x_{i} } \right | } }}{n}$$](img/507793_1_En_9_Chapter_TeX_IEq1.png) | 这是所有绝对误差的平均值 [5] |
| 均方误差（MSE） | ![$${\text {MSE = }}\frac{1}{n}\sum \limits _{{i = 1}}^{n} {\left( {Y_{i} - \hat{{Y_{i} }}} \right) ^{2} }$$](img/507793_1_En_9_Chapter_TeX_IEq2.png) | 这是所有平方误差的平均值 |
| AUC-ROC 曲线 | 对于正召回 TRP = TP/(TP + FN)。对于负召回 FPR = 1 − 特异性 = 1 − TN/(TN+FP) = FP/TN+FP | AUC - ROC 曲线是与真正率相关的，它位于 y 轴上，与假正率相反，后者位于 x 轴上[1] |
| 精确度 - 召回率曲线 | 对于正精确度 P = TP/(TP + FP) 对于负精确度 N = TN/(TN+FN) 对于正召回 PR = TP/(TP + FN) 对于负召回 NR = TN/(TN+FP) | 根据单个分类器的精确度-召回率曲线，估计和研究了精确度与召回率的关系[12] |
| 准确率 | 准确率 = (TP + TN)/(TP + TN + FP + FN) | 准确率指的是模型执行的预测率[15] |
| 分类错误率 | 错误率 = 1 − 准确率 | 未能识别不适合分类的值 |

## 4 结果与讨论

### 4.1 环境设置

所进行的实验是在 Intel(R) Core(TM) i3-7100 CPU @2.40 GHz 处理器、64 位 PC 上进行的，配备了 4 GB RAM。操作系统为 Windows 10 pro Education，python 被用来实现检测钓鱼网址的架构，所用到的 python 包括 TensorFlow、scikit-learn、Keras、Pandas 和 NumPy。

### 4.2 评估参数

该系统主要侧重于基于数据钓鱼或二元分类识别的评估。混淆矩阵、准确率、精确度-召回率曲线、分类报告、AUC-ROC 曲线、平均绝对误差（MAE）、均方误差（MSE）用于评估该系统的性能。评估参数[14]如表 6 所述：

### 4.3 实验结果

DNN 和 NN 的各种优化器的表示在表 7 和表 8 中展示出来。对于此实验使用了五种单独的自适应优化器，隐藏层的数量、学习率和迭代大小被考虑为 HL、LR 和 EPS。根据这个条件，HL5 表示隐藏层数为 5，而隐藏层 2 的数量是 HL2。对于这个评估，使用了 15 种学习率和 10 种迭代大小，对这五个优化器进行了 20 次迭代。经过 20 次迭代后，选择了更好的迭代大小和学习率组合，以达到优化的性能，使得此模型更加准确。

#### 4.3.1 案例研究 #1

DNN 的五个自适应优化器的准确率和损失的评估率。![../images/507793_1_En_9_Chapter/507793_1_En_9_Fig2_HTML.png](img/507793_1_En_9_Fig2_HTML.png)

图 2

准确率和损失 DNN 五个优化器

如图 2 所示，使用不同的深度学习自适应优化器来决定哪个优化器最适合反钓鱼提出的模型。在这种情况下，Adam 优化器在所有优化器中获得了最高的准确度，而 SGD 优化器的性能稍微低一些。相反，当使用所选的优化器调整模型以预测所提出的模型时，模型优化器会失去性能。在这种情况下，理解根据性能和损失准确度选择优化器是最适合反钓鱼提出的模型的摇摆。

图 3

用于 DNN 的 ROC 曲线和精度-召回曲线的不同优化器

ROC 曲线和精度-召回曲线在图 3 中已经显示。最大准确度 0.955 是从 Adam 单独获得的。在精度-召回曲线和 AUC-ROC 曲线方面，SGD 和 AdaGard 提供了更好的性能。在 ROC 曲线和精度-召回曲线中，SGD 和 AdaGard 的性能比其他优化器更好。表 7

DNN 的评估表

| 序号 | 优化器 | 标签 | 学习率 | Epochs | 准确度 | MSE | MAE |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Adam | HL5 | 0.01 | 50 | 0.955 | 0.030 | 0.074 |
| 2 | SGD | HL5 | 0.001 | 100 | 0.951 | 0.021 | 0.049 |
| 3 | RMSprop | HL5 | 0.0003 | 150 | 0.953 | 0.028 | 0.076 |
| 4 | AdaDelta | HL5 | 0.0027570 | 250 | 0.954 | 0.023 | 0.078 |
| 5 | AdaGard | HL5 | 0.0017470 | 150 | 0.953 | 0.018 | 0.049 |

分析清楚地显示在表 7 中，学习速率对所有测量或评估参数中深度神经系统的成功有着重要的贡献。发现使用 Adam 优化器的五层隐藏层的最大准确度为 0.955，MSE 为 0.030，MAE 为 0.074，以及 50 个 epochs 和 0.01 的学习速率（HL5 EPs50）。从上面观察表 7 的所有结果可以看出，所有的优化器都提供了 95%的准确度，其中 Adam 稍微多一点，Adam 是顶尖得分者 Vrbančič [19]。

#### 4.3.2 案例研究 #2

五个自适应优化器在 NN 的准确度和损失评估率![../images/507793_1_En_9_Chapter/507793_1_En_9_Fig4_HTML.png](img/507793_1_En_9_Fig4_HTML.png)

图 4

神经网络的准确度和损失五个优化器

如前所述，在图 2 中类似地，在这个阶段根据图 4 中的说明使用不同的深度学习自适应优化器，其中 AdaGard 优化器在所有优化器中为两层 NN 提供了最高的准确性，而 Adam 和 RMSprop 优化器为 NN 两层提供了略低的性能。根据它们的性能，模型在评估模型时会失去性能，以找到最佳优化器，如果两个 NN 层用于所有自适应优化器。![../images/507793_1_En_9_Chapter/507793_1_En_9_Fig5_HTML.png](img/507793_1_En_9_Fig5_HTML.png)

图 5

不同优化器的 ROC 曲线和 Precision-Recall 曲线用于 NN

ROC 曲线和 Precision-Recall 曲线已在图 5 中显示。从 AdaGard 单独获得最大准确率为 0.955。在 Precision-Recall 曲线和 AUC-ROC 曲线方面，Adam、SGD、AdaDelta 和 AdaGard 表现更好，提供 0.95，期望 RMSprop。表 8

NN 的评估表

| Serial | Optimizer | Label | 学习率 | Epochs | 准确率 | MSE | MAE |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Adam | HL2 | 0.0017470 | 150 | 0.948 | 0.014 | 0.058 |
| 2 | SGD | HL2 | 0.001 | 128 | 0.945 | 0.026 | 0.086 |
| 3 | RMSprop | HL2 | 0.0003 | 200 | 0.948 | 0.026 | 0.080 |
| 4 | AdaDelta | HL2 | 0.0027570 | 250 | 0.949 | 0.016 | 0.067 |
| 5 | AdaGard | HL2 | 0.0017470 | 150 | 0.955 | 0.030 | 0.074 |

从实验中清楚地显示，在表 8 中学习率对于所有测量或评估参数中深度神经系统的成功具有重要贡献。发现使用 AdaGard 优化器的隐藏五层的最大准确度为 0.955，MSE 为 0.030，MAE 为 0.074，并且 150 个 epoch 和 0.0017470 的学习率（HL2，EPs150）与 DNN 略有接近。

#### 4.3.3 案例研究 #3

堆叠泛化的主要目的是使用更高级别的模型来组合低级别的模型，以实现更高的预测准确性。堆叠将多个模型结合起来，并为分类任务学习它。表 9

机器学习分类算法的准确度

| LR | LDA | KNN | DT | GNB | SVM |
| --- | --- | --- | --- | --- | --- |
| 0.927 | 0.921 | 0.936 | 0.955 | 0.593 | 0.944 |

根据表 9，首先在所需数据集的数据上使用了 6 种机器学习算法，然后根据该算法找到了一些准确度。这些算法用于构建堆栈模型。表 10

构建模型堆叠及机器学习算法的增加准确度

| LR | LDA | KNN | DT | GNB | SVM |
| --- | --- | --- | --- | --- | --- |
| 0.966 | 0.965 | 0.965 | 0.966 | 0.965 | 0.966 |

在这一步中，通过应用这些算法生成了一个栈模型。根据表 10，在生成栈模型后，这些算法的准确性发生了变化。栈规定它结合了多个模型并学习用于分类任务。因此，这一步的目的是堆栈学习堆栈。表 11

临时预测的误分类率和准确率

| 算法 | 准确率 | 误分类率 |
| --- | --- | --- |
| RF | 0.96 | 0.0047 |
| DT | 0.95 | 0.0063 |
| MLP | 0.96 | 0.0022 |
| SVM | 0.94 | 0.0072 |
| SGD | 0.91 | 0.0073 |
| GNB | 0.59 | 0.012 |

栈已经学会了，现在它知道如何处理模型。表 11 代表第一步的最终准确率和误分类率。这项工作分为两步完成。因此，该表的数值表示第一步的预测或临时预测，因为在第二步预测之后将找到最终预测。接下来的步骤是构建模型，根据研究已经创建了一个 XGBClassifier 模型，通过该模型拟合了先前训练的数据并预测了最终结果。![../images/507793_1_En_9_Chapter/507793_1_En_9_Fig6_HTML.png](img/507793_1_En_9_Fig6_HTML.png)

图 6

不同算法的 ROC 曲线和 Precision-Recall 曲线

Precision-Recall 曲线和 ROC 曲线已在图 6 中显示。第一步显示最大准确率为 0.96，最小误差率。RF 和 MLP 在个别情况下表现更好，其中 Precision-Recall 曲线和 AUC-ROC 曲线，堆叠泛化性能较低。然而，在最终预测时，堆栈泛化提供了 0.97 的准确率。

#### 4.3.4 对三种多层方法的差异进行讨论

**栈泛化**表 12

堆叠评估率

| 算法 | 准确率 | 栈泛化的准确率 |
| --- | --- | --- |
| LR | 0.927 | 0.966 |
| LDA | 0.921 | 0.965 |
| KNN | 0.936 | 0.965 |
| DT | 0.955 | 0.966 |
| GNB | 0.953 | 0.965 |
| SVM | 0.944 | 0.966 |

在这项研究中，选择了二元分类类型数据集来评估三种多层方法。众所周知，机器学习算法对二元分类类型的数据集提供了良好的结果。栈泛化的主要特点是，它将低等级模型与高等级模型集成在一起，也被称为集成算法，基本上是在两层中工作。根据堆叠的概念，它在第一层学习多种机器学习算法，然后将预测作为输出，该输出用作第二层中另一种算法的学习。作为最终预测器使用的机器学习算法，这种学习更加无误。栈泛化的主要目标是开发低等级模型的结果，Li [28]新模型是由已经从数据集中训练过的其他模型训练的。通常使用简单线性函数（平均值、中位数、平均值等）来组装其他模型的预测。根据用于二元分类类型数据集的堆叠技术，将提供比 NN 和 DNN 更高的准确性。因此，可以使用这种堆叠概念获得优化的输出（表 12）。

**神经网络**表 13

NN 的最高准确率

| 优化器 | 标签 | 学习率 | 迭代轮数 | 准确率 | MSE | MAE |
| --- | --- | --- | --- | --- | --- | --- |
| AdaGard | HL2 | 0.0017470 | 150 | 0.955 | 0.030 | 0.074 |

根据决定规则，使用了两个隐藏层的数量来进行具有合理激活函数的任意决策 Rahman [13]。因此，对于给定的数据集，两个隐藏层神经网络是最佳方法。根据神经元的结构，第一层称为输入层。前一层的输出被作为下一层的加权输入获得，每层之间没有相关性，但是 NN 显示出了渴望的行为，通过了解 NN Fister [29] 来找到正确的权重。神经网络的结构类似于树结构。神经网络的每一层都有单元。这些单元表示这些层可以有多深。单元的值基本上表示数据将走多深，以及将会有多少基于树的组合。从多个值的平均值中获得完全准确的结果。对于给定的数据集，堆叠比神经网络提供更高的准确性，因此神经网络比堆叠提供更优化的结果。堆叠是在两层中完成的，而神经网络从许多基于树的组合中提供优化的输出。堆叠是在两层中完成的，因此在复杂数据的情况下它将执行较低，而神经网络的每个隐藏层都有单元，这些单元表示它将在基于树的结构中走多深，因此它将从多个组合中提供优化的输出（表 13）。

**深度神经网络**表 14

DNN 的最高准确率

| 优化器 | 标签 | 学习率 | 迭代轮数 | 准确率 | 均方误差 | 平均绝对误差 |
| --- | --- | --- | --- | --- | --- | --- |
| Adam | HL5 | 0.01 | 50 | 0.955 | 0.030 | 0.074 |

此研究最终确定了三种多层 NN、DNN 和堆叠策略。评估它们的输出显示，它们在这些堆叠中的结果几乎相同。这里使用了 2 层 NN，5 层 DNN，堆叠则使用了两个步骤。对于基本数据集，堆叠技术和 NN 具有不错的结果，即使数据集的输出降低了，数据集具有复杂或复杂的值。根据 DNN，它可以处理大量的层，并根据需要使用单位值。从这项研究中可以看出，基于 DNN 模型的架构通常对任何形式的数据集都提供了良好的结果（表 14）。

## 5 结论

尽管网络钓鱼是当今网络空间中的一个轰动现象，但调查和保障未来的安全问题仍然是值得关注的。在这项研究中，基于 NN、DNN 和堆叠概念已经开发出了防网络钓鱼技术。参数调整对这些技术起着至关重要的作用。在这些参数中，学习率是其中之一。这是一个无法想象的步骤，可以增加基于 NN 和 DNN 的系统的性能。这里对参数的影响进行了评估，这将成为发展基于 NN 和 DNN 的系统的证据。数据集中的数据量影响系统的学习基础。在堆叠的情况下，随机森林和多层感知提供了更好的精度和召回率结果。然而，堆叠泛化有助于提高整体准确性。

基本上，本章指出了三种多层技术，即 NN、DNN 和堆叠，以及基于神经网络架构的参数调整。评估它们的性能表明，它们提供的结果几乎相同。除此之外，堆叠在处理较简单的数据集时提供了更好的准确性。这里使用了 2 层 NN，5 层 DNN 和 两层堆叠。NN 和 DNN 层的单位指示这些层可以有多深。NN 和 DNN 之间的基本区别在于 NN 代表着两层，而 DNN 则代表着两层以上。

总结一下，最终结果是从多个输出的平均值得出的。如果数据集具有简单性，则堆叠技术和 NN 可以提供更好的结果；如果数据集具有复杂或更复杂的值，则性能会下降。根据 DNN，它可以处理大量的层，并根据需要使用单位值。从这项研究中可以看出，基于 DNN 模型的架构通常对任何类型的数据集都提供更好的结果。
