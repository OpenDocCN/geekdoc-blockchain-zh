© 2020 斯普林格自然瑞士公司 A. M. Langer 下一代软件架构的分析与设计[`doi.org/10.1007/978-3-030-36899-9_1`](https://doi.org/10.1007/978-3-030-36899-9_1)

# 1. 引言

Arthur M. Langer^(1  )(1)哥伦比亚大学技术管理中心，美国纽约，纽约州 Arthur M. Langer 电子邮件：al261@columbia.edu

## 1.1 传统分析与设计的局限性

从系统开发的开始，分析员和设计师基本上遵循一种需要对用户进行访谈、创建逻辑模型、在网络上设计并开发产品的方法。毫无疑问，我们经历了不同的世代，特别是在客户/服务器系统出现后，我们首先需要确定服务器上将驻留哪些软件，以及在客户端停留哪些更有意义。很多决定都与系统性能能力有关。一旦互联网成为应用通信和功能的基础，服务器技术就成为设计系统的首选方法，因为它具有版本控制和在新设备上的分发能力。不幸的是，这些世代导致我们创造了一个网络版的“科学怪人”。虽然主机系统中的安全性仍然相对安全，但互联网上的分布式产品并未设计足够的安全性。事实上，安全性关注的缺失后果导致了暗网的出现，以及全球范围内的网络暴露危机。我们的“科学怪人”已经创造了超出我们最疯狂想象的问题，不仅影响到我们的系统，还影响到我们的道德基础、我们的法律、我们的战略，最重要的是我们的隐私。就像弗兰肯斯坦小说中的情况一样，这个怪物不容易被销毁，甚至根本无法销毁——这就是我们的挑战。总之，我们现有的基于中央数据库和客户端/服务器思维的系统无法保护我们，也永远不会。

因此，这本书讨论的是下一代系统架构，首先必须要求解决问题的架构。这意味着所有现有系统必须被一种不再仅仅依赖用户输入的新架构所取代，并且必须被设计为考虑未来消费者可能需要什么，并始终考虑安全性暴露。接下来的分析与设计就是一本致力于重新构建我们的遗留应用程序、整合我们的新数字技术以及确保我们的网络能够最大程度保护使用者的安全的书。好消息是，我们即将拥有新的工具和能力，可以完成这个任务，尽管可能需要多长时间。这些能力始于 2019 年 5G 的到来，这将使网络以前所未有的速度运行。这种性能提升将推动物联网（IoT）的大规模普及，进而需要创建大规模网络。这些网络将需要最大程度的安全性。为了最大程度地保护安全性，我们的系统将需要摆脱中央数据库客户/服务器范式，转向基于分布式账本和面向对象的基于区块链架构和云接口的网络。为了解决区块链架构的延迟暴露问题，将需要某种形式的量子计算。这本书将提供一种完成这一过渡的方法或路线图，特别是重新设计现有遗留系统。

## 1.2 数字时代技术的消费者化

当互联网作为一项改变游戏规则的技术出现时，许多人认为这个时代将被称为互联网革命。随着数字开始成为一个常见的行业陈词滥调，似乎更加确定“互联网”可能会被“数字”所取代。然而，经过进一步分析，我相信这场革命历史上将被称为“消费者”革命。问题是为什么？看起来互联网的真正影响以及数字技术的到来已经创造出了一群聪明的消费者，也就是那些了解技术如何让他们在供需关系中拥有更多控制权的消费者。事实上，消费者掌握着主动权。结果显而易见；消费者偏好以加快的速度变化，并导致供应商不断提供更多选择和更复杂的产品和服务。因此，企业必须更具敏捷性和“按需”以应对兰格（2018）所称的响应式组织动态（ROD），即衡量组织如何应对变化的指标。

数字时代的消费主义意味着分析和设计将更多地源自消费者的角度。这意味着分析师必须将他们的需求收集扩展到内部用户群体之外，并寻求更大比例的消费者需求，更重要的是购买习惯。让我们进一步探讨这一点。在创建新软件应用方面最重要的转变不仅仅基于当前用户需求，还有未来的消费者趋势。这代表着消费市场的新需求周期。新需求基于消费者商业需求与数字产品和服务在家庭中的使用之间的密切关系。从设计的角度来看，商业和家庭的需求必须无缝融合——这是 21 世纪数字生活的最终表现！

但是技术的消费化需要设计上更大的飞跃；例如，由人工智能（AI）和机器学习（ML）驱动的预测分析。因为正是 AI 和 ML 将赋予我们使用更强大和自动化的范式来预测未来消费者行为的能力。因此，系统必须设计成像生物一样进化的形式。换句话说，应用程序必须包含我所说的*架构敏捷性*。架构敏捷性的第一步是应用数字再工程。应用开发的世界只能通过创建包含功能原始操作的巨大对象库来实现（Langer 1997）。功能原始对象是执行非常基本操作的程序，也就是说，那些提供一个简单操作的程序。基本功能操作程序可以在执行时组合在一起，以提供更灵活的应用程序。通过这些基本对象在执行时聚合，也可以更容易地更新新的特性和功能。执行时的这些动态链接提供了更具进化性和敏捷性的系统。对象范式并不新颖；架构敏捷性的区别在于这些对象必须分解为其最简单的功能。以前限制原语创建的是执行延迟或性能问题。与网络和操作系统动态链接原语以满足性能要求的能力有关的性能限制。

以前，功能原始对象设计的阻碍因素是硬件和软件环境之间的不兼容性，这些环境正在不断发展以解决这个问题。我认为我们会同意，架构之间的失效仍然存在。只需问问仍然在微软和苹果系统之间遇到挑战的人们。当设计基于 IPOD 和手机设计的新 Apple 架构时，史蒂夫·乔布斯确实可谓是革新了消费者界面。这种设计代表了执行较少特定应用程序但服务于未来基于无线的架构的设备，该架构可以执行更多的按需操作以满足消费者需求。最终，技术的消费化将企业应用程序、个人需求和日常生活视为一组集成的操作。然后，苹果架构一直处于一个可以比以前的计算机系统更快、更高效地发展新硬件和软件的演变平台的前沿。为了跟上加速发展的消费者，企业集中精力将如何将其传统应用程序转化为这种敏捷的数字框架至关重要。

## 1.3 演变中分析师的角色

建立在前一节的基础上，数字重塑代表了将传统架构转化为满足更多消费者需求的挑战。因此，重新设计的过程不再仅限于与传统内部用户合作，而必须在任何需求评估中将两个社区整合起来。此外，分析不仅必须包括现有的消费者需求，还必须包括可能是未来趋势的需求！例如，以下是我之前的出版物（Langer 2016）中提出的六种方法：

1.  1.

    *销售/营销*：这些个人向公司的买家销售产品。因此，他们对客户寻找什么、他们喜欢公司的什么东西以及他们不喜欢什么有很好的认识。销售和营销团队的力量在于他们推动直接影响收入机会的现实需求。这种资源的局限性在于它仍然依赖于消费者的内部视角。

1.  2.

    *第三方市场分析/报告*：有外部资源可用来审查和报告各行业部门内的市场趋势。这些组织通常拥有庞大的信息数据库，并且利用各种搜索和分析可以提供客户群体的各种观点和行为模式。他们还可以提供关于公司与替代选择之间竞争情况的分析，以及为什么买家可能选择替代解决方案。这种方法的不足之处在于，通常数据可能不够具体，无法满足为业务获取竞争优势所需的应用系统需求。

1.  3.

    *预测性分析*：这是当今竞争激烈的商业环境中的热门话题。预测性分析是从大型数据集中获取信息并预测未来行为模式的过程。预测性分析方法通常在内部处理，同时得到第三方产品或咨询服务的协助。预测性分析的价值在于使用数据设计能够提供未来消费者需求的系统。其局限性在于风险——预测可能不如计划中发生。

1.  4.

    *消费者支持部门*：内部团队和外部（外包的托管服务）供应商支持消费者，对他们的偏好有很好的了解，因为他们与他们交谈。更具体地说，他们正在回答问题，处理问题并获取关于什么起作用的反馈。这些支持部门通常依赖应用程序来帮助购买者。因此，他们是提供系统不提供给他们的最新内容的极好资源，而消费者作为服务或提供物可能会需要。然而，消费者支持组织通常将他们的需求限制在他们经历的内容上，而不是作为竞争力量的结果可能的未来需求。

1.  5.

    *调查*：分析师可以设计调查问卷并发送给消费者以获取反馈。使用调查问卷可能具有重要价值，因为问题可以针对特定的应用需求。调查设计和管理可以由第三方公司处理，这可能具有优势，因为问题是由可能不会识别公司的独立来源转发的。另一方面，这可能被认为是一个负面因素，这一切取决于分析师从购买者那里寻求什么。

1.  6.

    *焦点小组*：这种方法类似于调查的使用。焦点小组通常用于理解消费者行为模式和偏好。它们通常由外部公司进行。焦点小组和调查的区别在于（1）调查非常定量化，使用评分机制评估结果。消费者有时可能不理解问题，从而提供扭曲的信息，（2）焦点小组更具定性，允许分析师与消费者进行双向对话。

图 1.1 反映了对消费者分析信息来源的图形描述。![../images/480347_1_En_1_Chapter/480347_1_En_1_Fig1_HTML.png](img/480347_1_En_1_Fig1_HTML.png)

图 1.1

消费者分析的信息来源

表 1.1 进一步阐述了分析师在制定规范时应考虑的方法和成果。表 1.1

分析师评估消费者需求的方法和成果

| 分析师的信息来源 | 方法 | 成果 |
| --- | --- | --- |
| 销售/市场营销 | 面试 | 应该与典型最终用户面试类似。与高级销售人员密切合作。与关键业务利益相关者安排面试 |
|   | 赢/输销售回顾 | 回顾销售努力的结果。许多公司举行正式的赢/输回顾会议，这些会议可能传达当前应用程序和系统能力的重要限制 |
| 第三方数据库 | 文档报告审查 | 获取消费者行为趋势摘要，并确定当前应用程序和系统可能存在的不足之处 |
|   | 数据分析 | 在数据库上执行定向分析，以发现报告中未能传达的趋势 |
|   | 预测性分析 | 通过使用分析公式来审查数据，这些公式可能使消费者行为的趋势可预测 |
| 支持部门 | 面试 | 采访关键的支持部门人员（内部和第三方），以识别可能的应用缺陷 |
|   | 数据/报告 | 审查消费者与支持人员之间的通话记录和录音通话，以暴露可能存在的系统缺陷 |
| 调查 | 内部和外部问卷 | 与内部部门合作确定他们支持消费者时的应用问题。与一部分客户进行类似的调查，以验证和微调内部调查结果 |
|   |   | 使用类似的针对非客户的消费者的调查并比较结果。现有客户群体与非客户之间的差异可能会暴露出消费者需求的新趋势 |
| 焦点小组 | 进行内部和外部会议 | 分析师可以促成内部焦点小组。选择具有意外结果或混合反馈的特定调查结果，并与焦点小组与会者一起审查这些结果。内部参与者应来自运营管理和销售。外部焦点小组应由第三方供应商促成，并在独立场所举行。与客户的讨论应与内部焦点小组的结果进行比较。消费者焦点小组也应由专业的第三方公司促成 |

*Source* 软件开发指南：设计与生命周期管理，2016

## 1.4 为未来消费者需求制定需求

5G 到物联网演进可能面临的最大挑战也许是确定未来消费者可能想要的东西。问题是如何完成这个挑战？数字发明带来的变革将在前所未有的短时间内介绍给大量消费者。让我们简单看一下达到 5000 万消费者所需的时间![../images/480347_1_En_1_Chapter/480347_1_En_1_Figa_HTML.png](img/480347_1_En_1_Figa_HTML.png)

从 38 年到 19 天描述了数字技术所创造的令人难以置信的加速。因此，消费者非常快地意识到他们如何对新产品做出反应是非常不确定的。例如，史蒂夫·乔布斯真的知道当 Mac 设计和首次引入消费市场时，它会主要用作桌面出版计算机吗？我们是否知道 iPad 对高管如此具有吸引力？答案当然是否定的，并且请记住，“几乎”在这个例子中等同于“否”。最终，分析和设计将发展到更具预测性的要求，并且将因此有失败率！风险分析的概念将在第二章进一步讨论。最终，分析和设计已过渡到更多地收集数据而不是自包含应用系统。这种转变正在推动对这种新构建的系统架构的需求。

## 1.5 新范式：5G、物联网、区块链、云、网络安全和量子

本节将概述系统架构变化的组成部分，并简要描述每个组成部分与新的更分布式的硬件和软件组件网络的关系。

### 1.5.1 5G

虽然 5G 移动网络和系统显然是全球电信的下一代，但更重要的是，它代表了家庭、机器之间和工业通信能力的深刻演变。这些新的性能能力将允许我们在利用机器学习驱动的人工智能方面取得重大进展，以及在我们生活的每个方面学习和互动的方式。因此，5G 是下一代系统架构的发起者。这种新架构将基于通过分布式网络实现的增强无线连接。

如今，全球约有 48 亿人使用移动服务。这几乎占据了全球三分之二的人口。预计到 2020 年底，连接人数将超过 56 亿人。鉴于世界上许多地方的物理网络基础设施有限，加强移动通信代表了连接数据和应用网络的唯一可行方法。因此，5G 是推动未来新经济的动力，这将由先进的移动通信驱动。这不可避免地将创造一个由无线移动性驱动的全球经济。最终，5G 是一种启用器——一种允许专业网络参与我所说的“全球系统集成”的无缝组件的启用器。它还代表了网络的可扩展性，可以动态地链接和整合消费者、社区、企业和政府实体。这种整合将允许这些多个系统通过一个共同平台通信，以服务个人生活的所有方面。图 1.2 提供了 5G 性能改进所实现的新现实的图形描述！../images/480347_1_En_1_Chapter/480347_1_En_1_Fig2_HTML.png

Fig. 1.2

5G 移动连接生态系统的启用

图 1.2 的影响对分析和设计至关重要，因为它扩大了消费者需求的范围和复杂性，并将其与生活的所有方面集成在一起。表 1.2 显示了扩展覆盖范围以获得任何产品最大要求的扩展。Table 1.2

5G 的分析和设计要求范围

| 用户/消费者覆盖 | A&S 响应 | 评论 |
| --- | --- | --- |
| 企业到企业（BtoB） | 内部用户和安全 | 目前流程但缺乏安全流程 |
| 企业到消费者（BtoC） | 内部用户和外部消费者以及安全 | 目前在大多数组织中并不完全整合 |
| 消费者到消费者（CtoC） | 除了在特定交易平台上很少见 | 需要更新的平台和手机到手机的通信 |
| 企业到政府 | 除了信息、文件提交和付款等方面很少见 | 政府和企业系统的全面改革 |
| 个人到政府 | 除了信息、文件提交和付款等方面很少见 | 智慧城市和合规驱动 |
| 个人到消费者（ItoC） | 与会员门户相关 | 主要限于 Facebook/Linkedin |
| 个人到个人（ItoI） | 基于知识的门户 | 实践社区和知识门户 |

最终，5G 提供了跨无线网络更好的性能，这需要更复杂的系统设计。更好的性能使得能够在多种类型的系统之间传递更复杂的数据集。最重要的是，移动设备将能够利用这些复杂的数据集跨无线设备进行通信。这将进而推动基于移动性的全新经济体。移动性将加速创新需求，如图 1.3 所示。

图 1.3

创新与技术和市场需求相结合

图 1.3 展示了一个有趣的创新循环，它与新产品和服务的创建相关。该图反映了 5G 性能创新将会创造出新的市场——比如移动应用。另一方面，无线市场将反过来需求更多的技术特性和功能，这需要做出响应——比如消费者希望在他们的应用中看到的新特性和功能。因此，5G 将推动无线运营的新的更先进的需求。

5G 创新的一个挑战将是其对移动和链接遗留应用的重要性。也就是说，组织如何将其现有系统转换为更复杂的“数字原生”产品来竞争？此外，5G 的性能提升使应用开发人员能够更好地整合多种类型的数据集，包括图片、视频和流媒体音频服务的增加。我们预计非文本数据的存在将从 2015 年增加 45%到 2020 年，这将导致移动流量从 55%增长到 72%！

连接车辆是另一个巨大的增长市场，因为行业迅速向提供增强和自动驾驶方向发展。根据爱立信移动报告（2016 年）的结果，消费者期望设备的反应时间低于 6 秒，这是积极消费者体验的关键绩效指标之一。后续章节将概述如何将分析和设计领域的扩展与创建下一代架构相结合，以支持 5G 在个人生活的各个方面提供的内容。

## 1.6 物联网（IoT）

为了更好地理解 IoT，最好将其定义为根据数据收集提供结果的一种促成因素。IoT 的目标可以被视为更快地完善产品的一种方式。这意味着新产品发布可以实现，并且供应商/企业可以获得更即时的反馈，然后进行调整。这也意味着它创造了一种更为全天候的分析和设计范式。由于数据更新将更接近实时，产品可以满足消费者倾向于喜欢的东西——可以检测到消费者行为和需求的变化并在应用程序中进行修改。在许多方面，物联网创建了一个超级智能的监控系统——一个数据聚合器结合行为活动。

IoT 是由一系列交互式组件层构建的网络堆栈。从商业角度来看，物联网具有六个基本的分析和设计问题：

1.  1.

    设备上将安装哪些软件应用程序？

1.  2.

    哪种硬件最适合跨网络使用？

1.  3.

    哪些数据将被刷新并存储在设备上？

1.  4.

    有哪些外部系统接口？

1.  5.

    有哪些安全考虑？

1.  6.

    有什么性能要求？

图 1.4 提供了另一种观点来解释这六个问题。![../images/480347_1_En_1_Chapter/480347_1_En_1_Fig4_HTML.png](img/480347_1_En_1_Fig4_HTML.png)

图 1.4

IoT 的交互式组件

IoT 是建立在允许应用程序跨多个网络存在的架构上的。这些应用程序的确切位置是分析师所面临的挑战的一部分。具体来说，由于 5G 提供了更高的性能支持，支持 IoT 的设备将允许应用程序在设备本身上执行。这目前被称为边缘计算，其中设备将包含更多的软件应用程序和数据，从而推动性能。显然，设备上的本地程序执行将优于从远程服务器下载程序和数据。然后，可将常驻程序和数据集分解为更小的单位，这些单位可以在独立且更自主的设备上执行所需的特定功能。这最终表明，更大更复杂的传统应用程序需要被重新设计为可以在集合设备上运行的更小的组件程序，如图 1.5 所示。![../images/480347_1_En_1_Chapter/480347_1_En_1_Fig5_HTML.png](img/480347_1_En_1_Fig5_HTML.png)

图 1.5

物联网分解

我们可以在图 1.5 中看到，原始遗留 A 应用程序模块的一个特定子功能现在被分解为三个子功能，以在物联网设备上最大化性能。我必须强调，以这种方式设计应用程序的关键增强功能源于 5G 能够更有效地在节点之间传输本地数据。它还增加了在“边缘”上修改和更新移动程序的速度。物联网分解应用程序的一个示例可能是微软 Word 产品的子集或轻量级版本。考虑一下可能在只允许查看 Word 文档但没有所有功能的设备上提供的子集版本。我们已经在 iPad 和 iPhone 产品上看到了这样的子集！物联网在 5G 的支持下将增加这些类型的子版本，因为能够更快地在相关设备之间传输数据。

## 1.7 云

云计算和物联网将发展出另一个有趣的组合，以确定数据存放位置和应用程序最佳执行位置的替代方案。显然，云提供了更多的运行性能和存储空间。云已经成为存储本地应用程序和数据库存储的经济替代方案；更重要的是，它提供了随时随地的访问。对于移动性来说，后者非常重要。关于云存储应该是公共的还是私有的，或者两者都有，存在许多争论，其中关于组织如何利用这项技术的对话集中在网络安全和控制问题上。似乎由亚马逊（AWS）、微软（Azure）、IBM Watson、谷歌云、思科和甲骨文等第三方托管公司支持的公共云将成为该技术的主要供应商。事实上，云正迅速被称为“云平台即服务”。5G 的出现增强了迁移到云的吸引力，因为分布式网络的复杂性必须依赖产品和大量数据存储来支持人工智能和机器学习处理。

为了支持临时处理和数据操纵，提供内部支持的数据中心的挑战可能对任何组织来说都是巨大的。这些挑战大部分是成本和全球运营的能力，以支持更复杂的供应链，以交付和修改产品性能。也许自动驾驶车辆是如何使 5G、物联网和云能够几乎覆盖每一个可以想象到的偏远位置以最大程度满足消费者需求和服务的最佳示例。当然，卫星技术的使用使大部分这一切成为可能，但是如果不能根据消费者行为增加实时性能和修改数据的能力，连接性对于提供联系点运营的吸引力就很小。

从分析和设计的角度来看，云服务主要是设计功能原始应用程序。这些原始应用程序本质上被称为应用程序接口或 API，可以动态链接以拼凑出出色且灵活的应用程序。云提供商将基于价格竞争，当然，还有它们提供的 API，这些 API 可以轻松提供开发工具，帮助实现快速程序开发。因此，所有这些云提供商都提供了自己的工具包，用于连接和构建这些 API 产品。分析师和设计师面临的挑战是使用提供最大可转移性的工具包，因为大型组织很可能会选择拥有多个外部云提供商。

对于云依赖的物联网发展的扩展预测是重要的。根据 Linthicum (2019)的分析，EDC 物联网研究表明，55%的物联网开发者通过云接口连接，32%通过中间层连接，26%将云与物联网视为基本组成部分。随着物联网市场预计将在 2020 年达到 7.1 万亿美元，这些统计数据只会增加！

## 1.8 区块链

区块链代表了下一代主要的系统架构。区块链实际上是建立在链式连接概念基础上的数据结构。每个链接或区块都包含相同的交易历史。因此，区块可以包含元数据——例如触发器、条件和业务逻辑（规则）以及存储过程。区块还可以包含数据的不同方面。区块链背后的设计理念是，当新交易产生时，所有区块或节点都会得到更新，作为必须被链中所有区块接受的数据包。区块链设计的另一个重要方面是，访问是基于密钥密码学和数字签名的，这将增强安全性。因此，人们希望区块链提供的架构可以最大程度地增强网络安全，尤其是随着物联网设备和无线通信的普及，网络安全变得越来越受关注。当前区块链架构面临的挑战是对时效性更新要求的延迟考虑，尤其是对金融机构而言，这一点尤为重要。

区块链通过向链结构添加新的“区块”来运行。当数据成为任何新交易的一部分时，它变得不可变且不可抵赖，也就是说，所有有效交易都是实时添加并更新的。区块链具有 5 个特性：

1.  1.

    *不可变性*：对象的事件不可更改，因此交易的审计追踪是可追溯的。

1.  2.

    *不可抵赖性*：交易的作者身份在区块链的所有成员中得到保证。

1.  3.

    *数据完整性*：由于(1)和(2)，数据输入、操作和非法修改大大减少。

1.  4.

    *透明度*：所有区块链的成员或矿工都知道变化。

1.  5.

    *平等权利*：权利可以在链条的所有成员之间设定为平等。

从安全的角度看，区块链架构提供了以下特性：

1.  1.

    因为用户或矿工的权利在区块链上设定，授权可以被控制。由于区块链是分布式的，所有成员都会动态地了解任何变化。

1.  2.

    对于任何新成员的验证必须是自我验证的，因此入侵不能来自外部或外部系统。验证者作为智能合约在区块链内部运作，并消除了在去中心化网络系统中通常相关的“单点故障”。可以在集成的分布式网络中实施多个验证者以及仲裁软件。

目前有三种区块链架构：*公共、联盟/社区和私有*。公共区块链基本上是开放系统，任何具有互联网连接的人都可以访问。大多数数字金融货币使用公共区块链，因为它提供更好的信息透明度和审计性。不幸的是，公共设计牺牲了性能，因为它严重依赖更多的加密或密码哈希算法。私有区块链是内部设计，为一组特定的参与者建立访问权限，他们处理特定的业务需求。联盟/社区区块链是混合或“半私有”设计。它类似于私有区块链，但在更广泛的独立成员或组织之间运作。在许多方面，联盟区块链允许不同实体共享共同的产品和服务。换句话说，它是一个处理独立团体之间共同需求的共同利益实体。

区块链的重要方面是它是一个分类账系统。这意味着它会保存有关交易的信息——理论上，你可以重放区块链中的所有交易，应该得到相同的净结果或数据及其相关活动的安排。链中的区块存储诸如日期、时间和任何交易金额之类的信息——就像购买商品一样。此外，区块链还会存储参与任何交易的人的信息，因此个人或实体的身份被记录并且必须被知晓。从安全的角度来看，链中的区块还存储着唯一的“哈希”码，它们充当访问某些类型信息和执行某些类型交易的密钥。

从分析和设计的角度来看，首先选择组织将使用的第三方区块链产品非常重要。一旦进行了评估，就有很多关于区块链如何运行的决策，包括区块链的管理和配置（数据和计算）。具体来说，有许多数据和计算决策需要做，例如将存储在区块中的内容，将给不同组的什么管理权限，以及需要访问各种类型的云存储数据的通用接口是什么。这其中很多内容将在后续章节中介绍。最终，区块链代表了一种新型的分布式应用架构，一种更加点对点的新型客户端-服务器模型，其中包含嵌入式数据和开发应用程序。分析师需要了解网络中的流量挑战，避免单点故障，并确定 API 接口，这只是几个设计问题中的一部分。

## 1.9 网络安全

网络安全在分析和设计中可能是设计硬件和软件架构变革的拓展维度。网络是下一代的唯一组成部分。它简单地是每个分析和设计决策的一部分。表达这一观点的另一种方式是接受网络安全现在必须是分析和设计过程的一部分！必须设计安全以避免创建弗兰肯斯坦 2.0。整合网络分析和设计的第一步是接受其重要性或承认并意识到其重要性。分析师必须导航这一新一代架构的每个组件，并了解其系统存在哪些暴露。确定系统暴露现在是分析的最重要部分，因为网络保护更多是一项业务决策，而不是设计决定。事实上，大多数网络安全专业人士会说几乎任何系统都可以设计成最大化安全。不幸的是，最大化安全无疑会限制性能，以满足许多消费者的需求。因此，网络设计职业不能没有风险的存在。因此，大多数安全架构必须成为任何风险对话的一部分。这就导致分析师的工作要与组织中必要的业务和风险专业人员接触。由于法规限制和法律限制，一些风险决策受到限制，例如欧洲的 GDPR 法律。但许多决策必须在架构设计过程中暴露，有人在其中会对能力与暴露做出决策。因此，网络安全是系统开发生命周期（SDLC）的一个新组成部分。

另一部分网络设计包括存在于任何组织内部社区中的多种素养因素——古拉克（2001）所定义的网络素养作为一种新的互联网意识。事实上，网络意识涉及组织的文化，分析师必须评估人群的网络成熟度水平。事实上，今天我们知道许多违规行为是由组织员工的粗心行为造成的。因此，分析必须采用一种方法来衡量组织的网络成熟度，然后将风险作为设计新架构和应用程序的基本部分加以考虑。

## 1.10 量子计算

量子计算是否有朝一日能够取代硅片存在争议和不确定性。大多数量子实现和应用仍然是理论性的。量子计算机的功能组件称为量子比特。量子比特是一种复杂和多维度的二进制比特。当然，二进制计算仅基于 0 和 1 的比特组合，一次执行一次计算。在量子比特中，可以进行多个 0 和 1 的同时计算，并利用多个可用资源来实现输出。事实上，即使重复相同的计算，量子比特可能会以不同的方式利用原子、离子、光子或电子。实际上，量子比特就像动态处理中心，利用多个可用部分以每次执行完成任务。虽然资源可以在每次执行时唯一确定，但在特定情况或在请求时的状态下，可以预测数学概率。因此，量子计算机可能比今天的计算机强大一百万倍。

迄今为止讨论的问题的许多细节将在后续章节中更详细地讨论。下面简要描述每一章的内容。

### 第二章：合并内部用户和消费者需求

分析师传统上关注内部用户需求。这些内部用户负责了解业务需要以支持他们的客户。根据业务不同，客户可以是另一个业务（B2B）或消费者（B2C）。本章讨论了分析师必须评估业务需求的需求，超越内部组织的界限，直接与外部客户和消费者合作的必要性。下一代分析师必须面对新的挑战，通过提供与其商业环境的不确定性相匹配的持续和动态需求。因此，分析师必须根据市场趋势创建更多的推测性需求。本章还将讨论在分析过程中集成人工智能和机器学习的必要性。

### 第三章：审查对象范例

许多物联网应用程序的开发将需要大量的基于对象的可重用应用程序，在复杂网络中进行复制，并在移动环境中运行。本章将介绍对象导向工作原理、将当前较大产品分解为功能原语的方法，以及确定应用程序需要驻留的位置的方法。本章还概述了分析师必须使用的工具或核心概念，以创建规范或系统需要执行的逻辑等效。这包括完成系统的逻辑架构。无论是否需要软件包系统还是系统需要内部开发，组织都必须在真正了解业务和其消费者的需求之前创建逻辑分析。本章旨在为分析师提供将传统系统转变为分析和设计的新移动范式的路径。

### 第四章：分布式客户端/服务器和数据

本章介绍了后端数据库引擎的设计过程。包括逻辑数据建模过程以生成完整的实体关系图，以及将数据传输到多个数据存储设施的方法。还讨论了数据存储库的创建。本章有效地完成了需求文档中的数据部分。此外，还介绍了规范化和去规范化的实践以及在移动系统中确定数据复制的方法。

### 第五章：无线通信的影响

了解 5G 无线如何影响应用程序分析和设计至关重要。为了评估这种影响，有必要审查 5G 对性能的技术影响。本章讨论了市场对增加的无线性能可能会做出的反应，以及应用软件开发人员如何利用 5G 技术。本章展示了无线革命如何提高移动环境中的性能，增加安全性并降低延迟。我还涵盖了分析师与 5G 架构相关的不断发展的责任。

### 第六章：物联网

物联网（IoT）代表了将为人工智能和机器学习收集数据的物理设备。本章介绍了物联网如何通过在全球各处放置中间智能硬件来使技术变得可行。本章讨论了物联网如何提高正常运行时间和实时处理能力，以及减少未经计划的网络故障的能力。本章提供了关于安全风险和与第三方供应商合作的工作方向。

### 第七章：区块链

这一章提供了区块链架构概述以及其在未来移动网络中的作用。该章定义了每种类型的区块链，以及它如何使用基于账本的设计来最大化安全性。该章还确定了区块链的优缺点以及分析和设计应该如何进行。最终，我将展示区块链是如何对于扩展物联网和与云计算进行接口的必要性。

### 第八章：量子计算、人工智能、机器学习和云计算

这一章定义了量子计算如何有潜力改变计算的处理能力，特别是对于机器学习和人工智能处理。量子的优势在于它可以同时进行许多计算，并显著降低延迟。因此，量子的角色将是处理海量数据以获取可用于进行预测的有价值信息。本章将阐述预测分析如何迅速地通过使用先进的 AI API 实现自动化。这些 API 还将用于支持更多的机器学习功能，因为数据量远远超过了人类手动进行分析的能力。本章介绍了机器学习的不同方法，并总结了使用它们的优缺点。当然，云处理成为了如何最佳地在从移动物联网设备捕获数据的大型分布式网络中分发和处理数据的重要部分。

### 第九章：分析与设计中的网络安全

这一章展示了网络安全架构如何需要与公司的软件开发生命周期（SDLC）进行集成，特别是在包括战略分析和设计、工程以及分布式移动环境中的操作步骤中。移动驱动的应用程序需要遵守一般标准，以使它们有用，特别是如果它们正在与传统应用程序集成或者作为使用云进行完全重设计的一部分。ISO 9000 是一种国际质量标准化的概念，在这一转型过程中需要被采纳。本章涵盖了许多关于网络风险和当前被使用和被考虑用来应对网络相关犯罪激增的最佳实践。来自欧盟的《通用数据保护条例》（GDPR）也被讨论，并提出了分析师如何提供最佳实践的建议。

### 第十章：转型的传统系统

本章概述了将新的基于移动的系统与现有应用程序（称为*遗留系统*）进行接口的过程。涵盖了产品实现、遗留数据库和流程的连接以及多个系统架构的集成等问题。本章结合了前几章涵盖的用户界面和应用程序规格开发的建议方法。本章的目标还包括提供一个详细的路径，最终转换遗留系统。

### 第十一章：构建与购买

经典问题是，挑战商业组织的是，是在内部构建应用程序还是购买预打包软件。本章将提供关于确定正确选择的适当步骤的指导。显然，决策可能很复杂，并且因应用程序、应用程序本身的通用性以及满足业务需求的功能应用程序所需的时间而异。构建决策更加复杂，因为它们可以在内部开发或由外包提供商开发。购买还可能涉及到所需的自定义修改的数量选择——一般规则是，超过 20%的修改往往对购买方程式是一个不好的选择。云计算是支持物联网和区块链技术的终极基于服务器的范例，我们预测大多数公司将参与开发和第三方产品。

### 第十二章：分析师与项目管理

本章提供了有关系统开发生命周期方法和下一代系统项目管理的最佳实践的指导。涵盖了项目组织，包括角色和责任。下一代系统（5G、物联网、区块链）有许多方面是通用的；然而，在管理这些基于移动的系统时，肯定有许多独特的方面。因此，本章提供了对软件开发生命周期中这些独特挑战发生的地方的理解。它还关注了必须解决的持续支持问题，以达到最佳实践。本章的重点是建议分析师在项目管理角色中参与，除了他们在系统分析和设计中的责任之外。本章还提供了必要的流程、推荐的程序和报告技术，这些技术倾向于支持更高的项目成功率。此外，许多项目之所以遭受损失，是因为管理层无法适当地管理签约的供应商。组织犯了一个错误，即认为外包开发和管理是确保项目成功完成的保障。组织必须明白，第三方供应商并不是一切安逸的解决方案，必须建立严格的管理流程，以确保项目成功。

### 章节 13：结论与未来之路

本章总结了本书的目标。首先，本章概述了成功转变为数字化组织所需的技术和社会架构。分析师必须捕捉机会、做出反应，并将风险因素视为分析和设计功能的一部分。本章还定义了组织中不同世代的类型及整合婴儿潮世代、X 世代和千禧世代（Y 世代）人口的重要性。最后，本章旨在强调分析师角色的重要性以及可以承担的各种角色和责任，以提高在移动世界中由消费者驱动的组织转型的可能性。

## 1.11 问题和练习

1.  1.

    传统分析和设计的一些局限性是什么？

1.  2.

    “技术消费化”是什么意思？

1.  3.

    在数字时代，分析师的角色如何扩展？提供一些例子。

1.  4.

    定义并描述“新范式”的组成部分。每个组成部分如何增加更多的复杂性？

1.  5.

    讨论什么是移动连接架构。有哪些共同点？

1.  6.

    解释市场与技术进步之间的关系。

1.  7.

    6 个基本分析和设计问题是什么？

1.  8.

    解释物联网分解。

1.  9.

    区块链的安全优势是什么？

1.  10.

    量子计算如何改变世界？