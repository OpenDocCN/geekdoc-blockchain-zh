## 第十四章

## Blockstack

一切始于 Neal Stephenson 在 1992 年小说《雪崩》中的“元宇宙”，这是一个在现实世界之上的虚拟世界的愿景。一个季度世纪后，它仍然激发着极客浪漫主义者的兴奋之情，因为它的预言性音乐：

当 Hiro 十年前第一次看到这个地方时，单轨列车还没有被建造。他和他的朋友们不得不编写汽车和摩托车软件才能四处移动。他们会把软件拿出来，在电子夜的黑色沙漠中进行比赛。²

Muneeb Ali 在他的壮丽论文《一个新互联网的信任设计》开篇引用了《雪崩》中的这一段话，这是他与 Ryan Shea 和 Jude Nelson 以及他们的普林斯顿顾问 Michael J. Freedman 合作的成果。³ 这个团队走出了电子夜，试图用一种改变互联网的架构点亮它——一个超越通信技术七层的信任元世界。

阿里，这个大胆项目 Blockstack 中的关键人物，自从他十二岁在巴基斯坦第一次接触互联网以来，走了很长的路。作为在学校所有课程都拿到 A 的奖励，他的母亲给了他一台电脑。这个男孩感激而兴奋。尽管他的父亲是自己国家的军事情报主管，但家里并不富裕。购买电脑意味着延迟购买洗衣机。

“那是什么样的电脑？”我在 2017 年十五年后问他，在 Blockstack 在曼哈顿鲍威尔街附近的办公室里。

“哦，那是英特尔 386。”

“是的，”我说，“那是微处理器，但是这是什么品牌的电脑？是哪家公司制造的？”

阿里看起来困惑，然后回答说：“哦，我不知道。这台电脑是我自己组装的。”

我意识到我们在谈论一个严肃的十二岁的巴基斯坦技术人才。在他 2016 年在曼哈顿举行的 TED 演讲中展示的 PowerPoint 中，我们可以看到他在十五年前的一张照片中，一个穿着有勋章学校制服的红色短裤和衬衫的小男孩，右臂搂着他的弟弟。他们互相鼓励，站在巴基斯坦一条混浊河流的木桥上，这是文化和技术不同世界之间的象征性桥梁。

那个组装现代计算机的小男孩将长大成为一个重新构想全球网络的人。但要突破需要大胆和创造力。桥的另一端提供了无法逃脱的安全港和保证，就像他现在对互联网的新的信任模式一样。

阿里后来在拉合尔大学管理学院学习计算机科学。2005 年毕业后，他发现在巴基斯坦几乎没有机会，所以他构思了一个大胆的计划，在斯德哥尔摩的瑞典计算机科学研究所获得奖学金。瑞典人很高兴接受他，但没有提供财政支持。沮丧的是，没有钱也没有工作，阿里考虑要不要退回桥后，但他的偏见总是向前迈进。

他构想了一种计策——一种可能推动他前进的桥梁贷款。他向瑞典人保证他已经获得来自拉合尔的留学奖学金，他们同意承认它。然后他去了银行，以他的瑞典“奖学金”为基础获得了一千美元的贷款，只带着对斯堪的纳维亚城市食宿费用模糊的想法前往斯德哥尔摩。

该研究所雇佣了阿里并为他提供了住所。但食物是每天的挑战。当他的一千美元逐渐减少时，他每天五点步行到麦当劳购买一个鱼三明治和薯条。早晨，他会吃研究所咖啡时间的松饼和饮料。

他的父母得知阿里看起来苍白而消瘦。他们很担心。但是，才华终究会胜出，特别是当它饥渴时。他的计算机界面工作令教授们印象深刻，他回顾起在斯德哥尔摩的三个月是他最为富有成效的时期。他写了三篇重要的研究论文，获得了重要的推荐，并在桥的另一端获得了不稳定的立足点。

当时正当阿里（Ali）与欧洲共同体标准机构的联合主席在荷兰确立了一份关于当时未来主义的“物联网”（IoT）研究工作之时，他手头的一千美元用完了。他在这个物联网项目中负责媒体访问控制层，必须关注将“物”连接到网络的安全问题。在获得更多推荐后，他便跻身于美国计算机科学研究的顶峰——在普林斯顿攻读博士学位，暑期则前往斯坦福。

在普林斯顿的导师、计算机科学家和密码学家迈克尔·弗里德曼（Michael Freedman）已经在对等网络的理论和实践上工作了二十年。他是标准教科书《Peer to Peer》中的两章合著者，也与马丁·卡萨多（Martin Casado）合著了标志性的“开放流”软件定义网络（SDN）论文。如今，他是 TimescaleDB 的首席技术官，这是一款备受称赞的开源时间序列数据库。阿里感谢弗里德曼“与我一同思考各种分布式系统问题的每一个细节。我通过观察他设计和优化系统来学会了作为一个系统研究员的未记录的艺术。”

在普林斯顿与 Jennifer Rexford 一起研究网络处理器和虚拟机，在斯坦福与 Casado 一起研究软件定义网络的夏天，阿里成为了一个严肃的学者，研究将计算机和路由功能从固定硬件转移到可编程软件的实践和哲学。Casado 随后创立了开创性的网络虚拟化公司 Nicira，将其以 12 亿美元的价格出售给了 VMWare。大胆直言的大卫·霍洛维茨的儿子本·霍洛维茨通过在 VMWare 发明软件而发了财，Casado 最终加入了他，成为 Andreessen Horowitz 的风险合伙人。

无论是 SDN 还是网络功能虚拟化，都淹没了阿里的虚拟化运动正在改变网络。它从一个由硬件功能主导的七层结构变成了一个主要由软件模拟硬件功能定义的两层结构。就像斯蒂芬森的广岛和化名为 Satoshi 的人一样，阿里生活在一个可以摆脱物质世界限制的领域，进入电子世界并创造一个能实现你梦想的元宇宙。

七层模型由一个层次结构堆栈组成，在这个堆栈中，较低的功能由较高的功能控制。在底部是物理层，光纤线、微波振荡器、混频器、1550 和 900 纳米激光器、光电探测器、硅路由器、铒掺杂放大器和双绞线电话线，天线、同轴电缆——这个列表是无穷无尽的——它们在上层的指示下携带数据包穿过网络。设计和构建困难，这一层硬件设备是现代电子奇迹的核心。但当阿里在普林斯顿学习的时候，许多行业都忽视了硬件，而是在虚拟空间中构建图灵机。

要理解当代互联网，你必须理所当然地接受这些硬件奇迹，并在虚拟线程、核心和链中建造“天空中的城堡”——用计算机语言来说，“堆栈”——这些堆栈可以模仿硬件并在虚拟线程、核心和链中超越它。但是，从微观物质到元宇宙的演变始于国际标准化组织的开放系统互联模型（OSI）的七层网结构方案。

在 OSI 堆栈中，物理层之上是数据链路层。这是硬件变为“固件”和定义电气规格、定时规则和电子-光子转换的软件的媒介，这些规范使得信息能够在链路上从一个节点或计算地址传输到下一个节点。交换机在这里在第二层操作，只将数据包传递给下一个节点。诸如以太网或 WiFi 之类的局域网在此级别运行。如果你避开互联网的高速公路，你可以在数据链路层之间传输你的比特和字节，第二层。

第三层是网络层，是路由器的领域，它与传输层（第四层）结合起来建立端到端的连接，构成 TCP/IP 互联网协议。这是 IP 地址和传输控制协议流量洗牌的整个系统，构成了从端到端跨越网络的连接。第三层在数据包头部进行处理，包括身份和地址；第四层进行数据包的实际传输和接收以及流量管理、负载平衡和确认（我收到了！）和否定确认（我还在等待）以确保连接。第三层和第四层往往是中央权力的堡垒，政府及其情报机构在这里追踪域名和地址，诸如 ICANN 甚至联合国的 ITU。当他们发现一条丝绸之路或者也许是一个阿尔法湾时，他们会在第三层追踪它。

在第四层以上是第五层——至关重要的会话层——它从头到尾管理着特定的双向通信，无论是视频流，Skype 电话，会话初始协议会议，消息交换，电子邮件发布，甚至——这将证明是命运攸关的——交易。

第六层和第七层是演示和应用的方案——用户界面，窗口，格式，操作系统等等。这些都被概括在巧妙的超链接方案（单击一个单词即可转到新页面）和统一资源定位符（URL）地址中。1989 年，位于日内瓦的欧洲核子研究中心的 Tim Berners-Lee 发明了它们作为他的万维网的一部分。伯纳斯-李想要将所有数据链接成一个 Web，一个工具的编织，使得建立一个“共享创意协作空间，每个人都可以一起玩”的 Web 页面变得容易。

由于 70％的所有链接通过谷歌和 Facebook 进行处理，伯纳斯-李担心他的网络正在衰落。他将成为 Blockstack 的支持者。“当他听到我们正在做的事情时，他跳起了小舞，”Blockstack 的软件主管朱德·纳尔逊说道。

在《泰勒科斯姆》中描述 OSI（开放系统互连）模型时，我使用了一个电话呼叫的例子。拿起听筒并听取拨号音（物理层信号），现在通常是模拟的；拨打号码（每个数字将呼叫移向目的地的另一个链路）；等待铃声响起（表示网络连接和信号传输）。当你与某人通话时，你已经通过了 OSI 模型的前四层。然后你的“喂”开始了一个会话，选择英语定义了演示，对话构成了应用层，挂断电话结束了会话。

虽然唯物主义者可能认为物质层面是一切，而软件凯旋者则认为一切都在他的头脑中，但网络的天才是二元的。由数以万亿计的微芯片晶体管、过孔和迹线驱动，物理层最终像巧妙和不可或缺一样晦涩和深不可测。软件逻辑在上方层次中繁衍，定义了硬件的功能。

随着每个组件都按照摩尔定律加速，许多特殊用途的设备，如 ASIC、网络芯片、网络处理器、TCP 加速器、流量管理器和路由查找表内容寻址内存，都不再那么需要。取而代之的是越来越快速、密集和可编程的通用硬件。

在路由器、交换机和其他网络设备中替代定制设备的是基于 Intel、Cavium 和 Mellanox 等公司的多核通用微处理器的强大服务器。它们在日益复杂和集成的软件指导下连接在一起。通用硬件指挥着行业内广阔的市场——从数以亿计的智能手机和视频游戏主机——变得越来越快速和便宜。随着时间的推移，这些芯片可能会取代以前在互联网上以光纤速度执行每秒数万亿次操作所需的更昂贵的专用硬件阵列。

通过合适的软件，快速服务器中的 Intel Xeon 微处理器可以执行以前需要 Cisco 的复杂定制硬件（如 Tiger 和 Quantum Flow）或以色列的 EZchip/Mellanox 的巧妙光纤速度网络处理器执行的路由器和交换功能。

最后，谷歌放弃了大部分专用的网络硬件，而是选择了部署在庞大数据中心中的成千上万台服务器，并通过软件集成起来。图灵机和图灵脑中一样，是无形且可变的。路由器、计算机、交换机或互联网实现可以被“虚拟化”，根本没有具体的硬件表现。

引领这一变革的人物包括卡萨多、雷克斯福德、弗里德曼、霍洛维茨以及整个行业的数百人。这些网络科学家向阿里和其他 Blockstack 发明者介绍了这些原则的区块链工程。他们严格地将高级的控制平面与低级的数据平面分开。这种设计确保了这些架构的独特精简和可扩展性。

一切都始于巴基斯坦的第一台计算机，一台诱人的奖品，一旦他混合搭配了组件，并从套件中组装好了它。他回忆起，当他完成了工作时，计算机让他感到困惑。在二十一世纪初的巴基斯坦，一台计算机就像寓言中的“丛林中的汽车”一样。汽车可能提供吸引人的特点——光明、热量、空调、庇护、保护——但只有与道路结合才会变得真正令人兴奋。阿里的计算机只有在他获得一款网景浏览器并上网后，才真正吸引了他，并改变了他的生活。在巴基斯坦，他可以穿梭于整个万维网的道路上，并成为全球信息经济的一名公民。

阿里感觉到，网景的崛起标志着网络历史上的一个转折点——为数据提供了新的可访问道路。它的浏览器为网络提供了交互性、文本、图像、安全性和跨网络的交易可能性。它嵌入了 Brendan Eich 的 JavaScript，用于动态网页和交易表单，一个安全套接字层，使跨网络的商业链接安全，以及一个 Java 虚拟机，用于从任何“通天塔”操作系统移植应用程序。

网景的创始人认为网络是各种创意表达的交织竞技场，从照片到视频。它的创始人马克·安德森和投资者吉姆·克拉克，Silicon Graphics 的 3D “几何引擎” 发明者，都预见到了一个三维虚拟世界的游戏和虚拟世界。通过网景，安德森、艾克、克拉克和同事们赋予了阿里激活网页、与世界分享并可能在网络上赚钱的能力。

1995 年的网景 IPO 也意味着互联网奖励的分发。在第一天，股票价格几乎翻了两番，达到了超过 30 亿美元的估值，使公众受益，激励并资助了挑战计算机界的企业家。在接下来的五年中，谷歌、亚马逊等公司的一系列 IPO 推动了分布式互联网应用的繁荣。根据我所谓的“微观法则”，创新决定性地转移到了网络的边缘。

这是技术创业的高峰。然而，在 2000 年之后，初创公司的数量将停滞不前，IPO 几乎只留给了最大的科技公司。在安然公司的倒闭事件之后，萨班斯-奥克斯法案下的规定对于达到公开市场收取了大约两百万美元的代价，并实施了一套高度繁琐、信任度低的严格会计制度。这对初创企业文化和金融完全不利。

作为让公司成为公开公司成本高昂且充满险阻的典型表现是“公平披露”化所有公司通信的律师化。如果你必须经过律师批准，你可能不会说出任何有趣的事情。除了最大的公司之外，所有公司几乎都成为了几乎零熵通信的领域——全是回头数字，没有任何内部细节使其显得重要。

阿里 2012 年来到普林斯顿时，Netscape 已经失败了。它的浏览器被微软的 Explorer 取代，免费提供并与 Windows 95 捆绑销售。微软通过收购 Spyglass 浏览器，发起了现在常见的互联网巨头购买创新的做法，成功地镇压了 Netscape 的挑战。碰巧，Spyglass 的主要设计师是 Netscape 的安德森和埃里克·比纳，他们在伊利诺伊大学的超级计算机中心开发了其基础版本作为 Mosaic。微软收购了一款优雅的模块化浏览器，并让 Netscape 的发明者们与自己竞争。

IPO 寒冬持续了十多年。2016 年的九个月里，美国根本没有 IPO。相反，风险投资家们把数百家“独角兽”——估值超过十亿美元的私营公司——留在了他们的牲口圈里。由 Uber 和 Airbnb 领导，几乎所有这些公司在私人市场的市值都高于 Netscape 的 IPO。大多数公司对上市不感兴趣，而是更愿意与 Google/Alphabet 或 Facebook 这样的巨头合并。与早期互联网公司如 Microsoft 和 Netscape 的增值不同，独角兽的增值主要不会惠及公众。收益（和烧钱速度）大多流向持有它们的风险投资家和收购其中一些最好公司的巨头们。

这就是 2012 年，阿里和他的朋友瑞安·谢在普林斯顿大学创业俱乐部加入，并共同投入到推出新互联网应用的努力中的情况。到 2013 年春季，他们发现自己陷入了奇怪的困境。他们所走的互联网之路现在汇聚在提供微薄安全或隐私以及少量经济收益的巨型数据中心枢纽上。

这是一个关键缺陷的封闭运动。一个不安全的网络无法保护财产权，捍卫隐私，承载安全和高效的交易，允许微支付以阻止垃圾邮件，或者建立确凿的身份。谷歌、Facebook、亚马逊、苹果等公司对此作出了响应，建立了自己的专有“安全空间”。在那里，他们可以容纳其大多数固定用户之间的商业活动。

正如阿里所述，“目前，随着在线服务的频繁使用，用户数据被锁定在‘数据孤岛’中，例如，数据被 Facebook、Yahoo!、Google 等了解和存储，但不能在服务之间迁移。这导致了集中式数据模型；数据孤岛最终不可避免地被黑客攻击，例如，最近有 5 亿 Yahoo!用户的黑客攻击。”⁷

这些孤岛，或者说“围墙花园”，正是让伯纳斯-李感到沮丧的所在。⁸它们对于它们的所有者来说效果很好，但却破坏了网络的全球连贯性，并导致了日益增加的分割。在这些分割中，谷歌、苹果、Facebook、亚马逊等收集了越来越多的私人数据，并用防火墙和加密来保护它们。但随着时间的推移，他们发现集中化并不安全。将数据放在中央仓库中解决了黑客们最困难的问题：它告诉了他们哪些数据是重要的，以及它们在哪里，从而使整个互联网面临风险。

Google 动员了“一支全明星黑客突击队”来打击黑暗面的黑客。一个整个安全公司行业崛起，以保护用户数据蜜罐，通过对病毒爆发、大规模数据窃取、阻断服务攻击、恶意软件、恶意广告、钓鱼计划、勒索软件等的应对来反应。每个互联网领地都通过强加给其客户一连串的安全繁忙工作来回应，这些工作对改善安全没有任何作用，并且从各个方面来看，每年都在恶化。“安全”计划只是让粗心大意的数据持有者告诉法庭他们已经尽了全力，指出他们在这些计划上的巨额支出。

利维坦的数据储存设施激发了世界各地的暴君们孤立他们自己的互联网。如果 Google 的两个书呆子可以拥有自己的互联网，Facebook 的一个专家也可以拥有自己的互联网，那么为什么中国政府就不能有一个呢？或者伊朗的神职人员？或者，不怕笑话，欧洲联盟呢？Google 将会从他们所有人那里听到消息。

互联网堆栈已经成为一个多孔的、多孔的方案，在这个方案中，大部分资金和权力都被顶端由 Google 等公司运营的大应用程序吸走了。所需的是一个能够将关键的 ID 和个人数据以及指向存储地址的指针安全地保留在区块链上的安全且不可变的数据库。

正如阿里和谢亚所理解的那样，安全不是一个应用程序或视频游戏。它是一种架构。决心设计这种架构，阿里成为了一名美国公民，并且——与布兰登·艾奇、维塔利克·布特林和其他先驱者一起——成为了重新建立互联网的领导者，采用了他在巴基斯坦少年时期体验到的去中心化、点对点的原则。