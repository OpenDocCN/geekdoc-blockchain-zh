第九章

# 区块链与物联网：推动供应链效率和成本的新范式的应用和用例

阿纳布·巴内尔吉    ^(印度班加罗尔 Infosys 有限公司)

## 摘要

本章讨论了区块链与物联网在供应链领域的使用案例，以及其他系统/实践，以实现供应链的新范式。本章确定了供应链各个领域的即时挑战，从产品或订单跟踪、可追溯性和召回、仿冒、农业供应链、汽车供应链、数字家庭、办公室和仓库到制造和分销供应链。详细介绍了物联网和区块链的关键特性和能力，并通过示例说明了如何利用这两种强大的技术以及外围系统和主干 ERP 来解决列出的业务问题。它探讨了物联网和区块链组合的流程流程、技术架构和业务影响。本章最后列出了物联网和区块链组合为供应链带来的经济价值和成本节约，以及未来的机会。

### 关键词

区块链；物联网；供应链管理；仿冒；ERP；汽车供应链；农业供应链；可追溯性；产品召回；来源

## 1 引言

在当今全球化经济中，供应链是复杂的。在零售店或在线销售的产品由多个地点的团队设计，某些地方进行制造，存放在某处，然后交付到各处。产品在交付给最终消费者之前会经过各个国家、仓库、天气条件、处理方法和存储情况。产品流动的物理领域与信息流动的数字方面相辅相成。随着技术的不断进步，这些数字信息变得越来越重要。及时提供这些信息，以安全、透明和结构化的方式，对于更快、更准确地做出决策以及节省成本和资源的明智使用至关重要。

Clive Humby 在 2006 年在 Kellogg 商学院举办的 ANA 高级营销峰会上发表演讲时将数据比作原油。他指出，就像原油一样，数据可以分解和分析以获得巨大的价值。公司必须学会处理这些海量数据，以获得洞见并做出可行的决策[[1]](S0065245819300336.xhtml#bb0010)。更近期的例子是在 2017 年，万事达卡的首席执行官 Ajay Banga 引用了他的话：“数据是新的石油”[[1a]](S0065245819300336.xhtml#bb0010)。从产品概念或原材料到产品在货架或网络门户上亮相都会产生大量数据。引导这些数据进行分析以进行未来改进、决策制定和成本削减是每个供应链领导者的方向和意图。成品的众多组成部分、多种采购选项、不同的地理和气候条件、存储情况、实时跟踪需求和物理处理使得跟踪和监控物理、气候和仓储条件至关重要。只有当信息是安全的、结构化的、实时的并且易于获取时，所有这些才是可能的。

今天，每个组织都与系统相连，相互交织在一起。随着数字化旅程的推进，组织内部存在着诸如 ERP、MRP、WMS、CRM 等系统，这些系统改善了组织的流程，提高了效率，降低了成本，帮助其更好地运作。但真正能够为决策和其他方面带来好处的是组织之间能够无缝交互和沟通的能力。焦点逐渐从组织间数据交互转向与物理机器和其他领域的数据交互。如今，大多数组织间的通信是通过 EDI、B2B 消息传递和手工报告驱动的，并且没有与机器和其他物理领域（如压力、温度等）进行通信的机制。这些技术中的组织间通信既不可靠也不实时，也不安全。这些通信大多是批量处理的，需要手工干预，并带来了自身的一系列限制。本章将探讨不同类型供应链面临的挑战以及现有技术如何解决这些问题，以及区块链与物联网（IOT）能力的现代成熟技术将如何解决这些问题，提高效率并降低成本。

## 2 供应链挑战

根据麦肯锡公司的报告，在大多数行业中，供应链是一个独立的组织，由首席供应链官（CSO）领导[[2]](S0065245819300336.xhtml#bb0015)。这种范式转变的原因是意识到供应链对资产负债表的整体底线的影响。根据 O'Byrne 的说法[[3]](S0065245819300336.xhtml#bb0020)，今天的供应链具有在任何行业中节省成本和推动效率的最大潜力，无论是制造业、医疗保健还是分销。此外，客户的各种要求，如实时跟踪产品、追溯产品或组件的原始来源（出处）、无缝召回产品、改进制造过程以降低成本、根据客户反馈推动产品功能、更环保的产品、寻找最优质的资源、以最佳成本资源、提供更好的客户服务等，全部都属于供应链的范围。

让我们从各个领域的供应链和行业中看一些相关的供应链挑战。这些挑战在当前技术格局下面临着，其中 ERP、WMS、CRM 大多已实施。

### 2.1 产品/订单跟踪

在将产品提供给客户的过程中涉及多个利益相关者。例如，一家制造路由器的公司收到了客户的需求。需求被转交给合同制造商，然后运送到仓库。产品由合同制造商通过物流服务提供商运送。产品到达公司的仓库，然后运送给客户。由于在这个需求/供应交易中涉及多个利益相关者，实时信息共享是一个挑战。这些公司使用报告和 EDI/B2B 消息来提供产品到达或离开某个地点的信息。在这之间发生的情况是信息真空。药品和食品行业也存在类似的信息断链。目前/现有的大多数追溯解决方案使用仓库管理解决方案以及 RFI 标签[[4]](S0065245819300336.xhtml#bb0025)。这是信息真空，供应链挑战仍需要解决方案。

### 2.2 产品追溯/召回/防伪

为解决伪造、产品和药品污染、产品和药品降解等问题，美国食品药品监督管理局（FDA）颁布了药品供应链和安全法案（DSCSA）。该法案要求所有制造商、分销商和第三方物流提供商开发电子和互操作系统以跟踪药品。这需要几乎实时和高度安全的数据交换，可以随时进行分析。同样，美国 FDA 要求制造商尽快从客户处召回产品，如果美国 FDA 已经要求召回产品（在它损害客户之前）。如今，制造商对最终客户的访问或信息非常有限。产品伪造是另一个供应链挑战，因为极其难以确定伪造产品被注入到供应链的位置。所有这些情况都要求具有安全的实时追溯产品的能力，可靠且迅速。这些挑战随着电子商务和全渠道供应链不断发展，并且市场上几乎没有可靠的解决方案来解决这些问题。

### 2.3 农产品供应链

农业供应链复杂而敏感。它始于农民，终于零售商或产品在消费者手中的消费。它之所以特别复杂，有四个原因：首先，在最初阶段，由于处于农民手中，技术或复杂度的使用有限；其次，大多数时候，产品经历多次转换，除非直接消费；第三，它具有多个利益相关者或价值链成员，其复杂程度各不相同；最后，它特别长，并跨越时间和地理范围。对于特定的最终产品，唯一确定的收获土地、知道种植它的农民以及作物种植的环境影响、作物种植的农业实践、作物产量、使用的化肥、土壤准备类型等，对许多政府机构、零售商甚至消费者特别感兴趣 [[4]](S0065245819300336.xhtml#bb0025)。由于供应链冗长，最终消费者对上游复杂性一无所知，因此它不仅错综复杂，而且多方面。

### 2.4 数字化汽车

汽车行业数字化转型的两个关键趋势。首先是自动驾驶汽车，其次是互联汽车。在这两者中，互联汽车的发展速度快，转型巨大，并且可能颠覆汽车供应链。互联汽车的概念，即连接到互联网并向云发送数据以传输汽车功能和其他相关信息的汽车，可以为汽车所有者和汽车价值链的其他成员开启各种选项。这些选项包括但不限于预测性维护、汽车信息娱乐、安全、安全召回、驾驶信息、高级导航、客户洞察和保险信息。预测到 2020 年，连接到互联网的新汽车销量将达到 98% [[5]](S0065245819300336.xhtml#bb0030)。如今，互联汽车仅限于与技术公司合作的汽车制造商。例如，雷诺-日产-三菱计划在 2021 年推出与微软和安卓相连的车辆 [[6]](S0065245819300336.xhtml#bb0035)。但实际的供应链优势在于汽车合作伙伴，如经销商、服务公司、零部件制造商和保险公司的连接。它们可以访问相同的数据源，然后做出决策或与车主联系，帮助他们节省时间、金钱，并提供更好的体验。这些是敏感信息，难以捕捉、连接和共享，目前几乎没有现成的解决方案。

### 2.5 数字化家庭和办公室

智能家居和办公室的概念正在不断发展，它们的使用方式也在变化。大多数连接的家庭和办公室的使用都围绕着一个智能设备，可以或不可以通过手机应用来控制，它控制着各种设备，如恒温器、电视、洗衣机、冰箱或灯光。但随着更多应用和服务的出现，越来越清楚的是，只有当这些设备及其应用连接到服务时，技术的好处才能实现。如今的智能家居有助于节能高效使用，提高生活质量并最大限度地提升安全性。由于市场目前尚不成熟且正在发展，智能家庭或办公室的真正好处将在硬件制造商、消费电子产品、零售商、软件和生态系统开发人员、公用事业服务提供商和家庭安全解决方案都连接起来时才能实现。连接必须从设备到设备、从服务到服务。这是一个单独开发产品的情况，需要进行全面的审视并将各方/合作伙伴聚集在一起。成熟技术的缺乏正在阻碍这个方向的发展。

### 2.6 分销行业的透明度

分销行业中最具挑战性的方面之一是信任。分销商与供应商之间对产品的可用性、特定国家/地理位置的产品价格，或者针对客户群的产品价格，以及货物的运输应该是不可辩驳的信任。除此之外，分销行业独特的信任领域还包括发货和借款索赔。今天主要的挑战是发货和借款索赔在供应商和分销商双方进行的手工对账。索赔的数量和复杂性导致数百万美元的资金被困在分销商的索赔中。索赔在产品发货和收货、库存、价格差异、协议价值等方面总是存在信任赤字。销售点报告是分销行业的另一个重要组成部分，它影响了许多货币决策，比如佣金、销售量回扣等，并且由于信任和透明度不足，而受到影响。这些问题大多是通过手工干预、报告、讨论和电子邮件来解决的。这主要是因为公司之间的技术平台有限或者根本没有。电子数据交换（EDI）、企业间消息传递（B2B messaging）无法解决这些问题。因此，每个分销商都需要解决这个问题，并需要一种成熟的技术来弥合这一差距。

### 2.7 制造系统

技术一直在改变核心制造流程。这一点从多年来制造业随着全球供应链和产品本土化的演变方式可以看出。实时集成伙伴之间的关系迫使公司和产品经理寻求共享数据进行分析的方法。这引起了对数据安全性、数据透明性、数据访问以及基于准确且未篡改的数据进行实时决策的考虑。这产生了数字孪生的需求，它帮助模拟真实世界的影响/行动，以通过网络世界中的模拟改善物理世界 [[7]](S0065245819300336.xhtml#bb0040)。在多伙伴生态系统中进行实时决策和数字孪生对于制造业只有在存在安全、透明和安全的数据共享和可用性机制时才可能。由于缺乏成熟的技术，如今这样的实时数据共享和数字孪生并不是那么普遍。

## 3 当前一代解决方案

基于各种行业、流程、产品、供应链战略类型的多样性，从以上讨论可以很明显地看出，为了为客户提供服务并做出有效的决策，需要进行顺畅的组织间数据共享。如今，这些数据以某种方式被管理，而它们被管理的方式将为我们铺平道路，帮助我们理解如何更好地利用技术来解决问题。订单跟踪和产品可追溯性目前是通过电子数据交换（EDI）/消息系统以及各种检查点处的报告和门控扫描来管理的。这表明未来系统的需求是像这些扫描一样实时地从任何地方提供数据。同样，EDI/消息系统表明信息必须到达正确和准确的目的地，以便做出知情决策。农业供应链面临着技术在基层的采用不足的问题。这可能是由于易用性、缺乏技术配置和成本等原因。由于这个原因，大多数产品缺乏所需的作物透明度、土地利用、环境影响等方面的透明度。基层数据的收集和透明地共享以及安全地跨多个机构共享这些数据是当前的挑战，这限制了农业供应链和其信息能够被最终消费者获取。数字汽车、数字家庭、分销和制造业也面临着实时捕获和安全地跨多个机构/利益相关者共享数据与在数字孪生中进行分析的挑战。所有这些都表明，技术当下的需求是提供一种安全地捕获数据和将其安全传输至多个利益相关者并保持透明度的手段和机制。本章进一步探讨了物联网技术及其与区块链结合作为解决上述问题的可信和成熟的解决机制。

## 4 物联网与区块链：强大的组合

根据上面的讨论，很明显需求有三个方面。特征上，这些可以分开，首先是从源头实时捕获数据的能力，无间断地，使数据从物理世界无缝转化为网络世界。它必须具有成本效益，并且必须完全与人类、系统、操作和过程无关。第二，捕获的数据必须尽可能安全。数据应该是完美无缺的，可信赖的，未经篡改的。第三，必须有一种无缝的机制，几乎实时地在企业/合作伙伴之间共享这些数据，而不依赖于任何过程，并且额外成本最小。所有这三个要求的需求迫使企业超越现有的 ERP 系统、点对点接口、EDI、消息系统和报告机制。这就是新技术及其机制、架构和成熟度显现的地方。对于供应链中讨论的挑战以及今天事物处理的方式，分布式账本技术（DLT）基于区块链系统以及物联网（IOT）的使用可以解决大部分问题。数据捕获、存储、安全和分发的技术能力和架构极大地支持这种组合。这种组合还可以提供许多意想不到的好处，如无缝同步、实时分析和数据的可移植性。

### 4.1 区块链

区块链系统是通过分布式账本技术连接在一起的成员网络。区块链系统记录交易作为区块，并且是不可变的和安全的（在很大程度上），并且按时间顺序维护交易之间的数据块。这些数据块在许多计算机/节点之间共享，而不是存储在中央服务器上。区块链还可以被描述为不可篡改的交易数字账本。区块链可以将物理产品标记为虚拟/数字令牌。区块链的一个强大特性是基于智能合约，仅控制特定成员的数据访问。在区块链中，交易数据可以通过规则（智能合约）进行验证，而不是通过单一的中央机构。区块链的最大好处是能够与合作伙伴组织无缝且安全地共享数据。

如今使用的区块链提供了三种类型的架构，帮助公司之间进行整合。它们是:

#### 4.1.1 开放区块链或无需许可的区块链架构

在这种架构中，没有一个合作伙伴或节点拥有或读取/写入/审计区块链。在这里，所有合作伙伴共同拥有它，每个人在网络中都是平等的。比特币、莱特币网络是开放区块链架构的例子。开放区块链网络通常不适用于特定目的或特定拥有组织的网络。这种区块链架构依赖共识机制运作。共识机制是通过工作证明来实现的。工作证明驱动着对验证者或矿工的需求。他们发挥着至关重要的作用，因为他们是接纳成员、验证交易并计算信用的守门人。这种架构需要大量的计算能力来维护大规模的分布式账本，并在众多参与者和验证者之间进行标准化计算。由于这一挑战，开放的区块链架构并不那么容易被接受。虽然比特币网络是最好的、最早的已知的区块链系统之一，但同类产品并不多见。

#### 4.1.2 许可或私有区块链网络

如果它是为了特定的目的，这种架构更加合适。在这种架构中，网络有一个特定的组织或单一定义的所有者。网络的所有者制定了其他成员的业务特定规则和/或智能合约。智能合约是为了成员之间的参与而定义的规则。这些标准化和明确定义的标准是许可区块链的基石。在许可网络中，参与者的加入由现有成员、监管机构或财团决定。一些私有区块链网络的例子是基于 Hyperledger Fabric 开发的 Oracle 区块链云服务。

#### 4.1.3 联盟区块链网络

共识网络类似于半私有的区块链架构，由预先选定的成员群体拥有和控制。这些成员群体决定未来的成员资格、规则等。阅读区块链的权利可能是公开的，也可能仅限于参与者。例如，人们可以想象一个由 15 家金融机构组成的财团，每家机构都运营一个节点，其中有 10 家机构必须签署每个区块，以使该区块有效。财团区块链提供了许多与私有区块链相关的好处，如效率和交易隐私。R3 是财团区块链的一个示例。

区块链网络可以连接到多个应用程序。将区块链网络连接到企业资源规划（ERP）系统的能力一直是最可信的[8,[9]](S0065245819300336.xhtml#bb0050)。这打开了将交易系统数据安全地连接并传输给合作伙伴以进行无缝数据共享、决策和透明度的机会。正如 Litan 等人所指出的[[10]](S0065245819300336.xhtml#bb0055)，区块链网络已成为肯定多方流程协作中共享数据完整性的有前途的创新。这打开了实时协作和分析的机会，这在几年前是不可能的。大多数组织都在试图通过 EDI 或报告机制解决这个问题，但这种方法效率低下且需要大量人力。

对于前文讨论的供应链挑战，区块链系统网络无疑是解决这些问题的可靠选择。但是，单独作为解决方案的区块链系统可能还不够。基本限制在于数据的捕获和将其提供给不同系统的可用性。区块链系统将提供一个安全而无缝的措施来共享数据。但是，数据的捕获本身就构成了一个挑战，特别是当我们考虑到数据源并非总是像 ERP 这样的交易系统时。它可能是来自任何来源和任何地方的实体信息和数据。因此，离线能力、系统和设备独立性成为一个关键缺陷。这引入了物联网的方面，以无缝地捕获数据并具有根据需要共享数据的架构。

### 4.2 物联网：物联网

物联网（IOT）是一个概念，用于连接或捕获设备或机器的任何类型信息，并通过互联网从其源传输到任何独立于平台的目的地。物联网也可以被描述为一个巨大的连接设备之间相互通信和共享信息的网络。物联网特别在供应链领域引起兴趣，因为它提供了从远程位置或自动流程捕获和共享数据的能力，否则是不可能的。它打开了在供应链框架内由于信息不可用而被认为是无法解决的问题的可能性。

IOT 设备的数据收集和共享基于如射频识别（RFID）和无线通信标准等技术和标准。RFID 技术提供了一种简单且经济高效的物理数据捕获机制，用于在工厂、仓库或零售店中的货物移动。将这些货物移动信息转换为技术平台能够使数据可见，并供各种分析使用。需要标签和标签读卡器来捕获这些信息。标签需要放在需要捕获数据的源头上，而标签读卡器则读取标签并捕获信息。它们实时捕获任何类型的移动。对于无线通信标准，IOT 系统通常使用无线传感器网络（WSNs），它们是从物理世界或机器收集数据并传输到中央控制器的整体架构的重要部分，随后传输到数据库以存储信息并用于进一步分析 [[7]](S0065245819300336.xhtml#bb0040)。今天有各种其他的 IOT 设备技术可用，如 ZigBee、Z-Wave、WiMax、LPWAN 等。物联网在连接三种类型的事物之间的信息。虽然事物没有明确的定义，但可以广义地分类为：

1.  1. 连接人群—这涉及通过社会联系、社区联系来改善人们的生活。

1.  2. 将产品与人连接—这涉及将设备个别或作为一个整体连接到人们身上。比如把家用设备与人们连接，无论是为了更好的生活还是家用产品与人们的连接，从洗衣机到冰箱。

1.  连接资产与机器——这些是一种工业应用，其中锅炉、炉子、涡轮机和机器使用传感器连接到其他机器或计算机进行监控和决策。这也使数字孪生技术成为可能。这些可以扩展到卡车、船舶、地点和仓库，用于连接和监控。

一个物联网系统需要能够连接到任何类型的异构系统。它应该能够以高可靠性和实时性安装或连接到任何操作系统。它应该有能力启动和停止数据流动，并且需要是一个可配置的系统。它在性质上应该是动态的，也就是说，它应该能够睡眠或唤醒，并根据设计连接或断开连接。一个物联网系统需要有能力检测物理世界的现象及其变化，并将其转换为数字信号。最后，最重要的方面是数据处理的规模。设备应该能够处理庞大的数据量。

这无疑开启了在供应链中探索和解决的许多机会，但也带来了可能和可信的数据安全问题。另一个问题是安全存储这些物联网数据。物联网是关于从源头捕获和传输数据到其接收者，但物联网并没有解决或提供任何存储数据的机制。

物联网作为一项技术有两个目的，首先它提供了捕获数据的能力和将其传输到目的地的架构。但在当今数字世界中，物联网的两个关键方面是无法忽视的，即其无法存储数据以及捕获数据的安全性。据研究和咨询公司 Gartner 估计，到 2020 年，安装的物联网设备数量将达到 204 亿 [[13]](S0065245819300336.xhtml#bb0070)。Business Insider 预测，到 2020 年，将安装 240 亿个物联网设备，其中大多数将由企业或政府使用 [[14]](S0065245819300336.xhtml#bb0075)。IBM 引用 IDC 的数据，并预测到 2020 年将有 300 亿个物联网设备连接到互联网 [[15]](S0065245819300336.xhtml#bb0080)。这一庞大的数量表明，必须有一种可信、可扩展和安全的机制来捕获、存储和传输跨网络/合作伙伴组织的数据。物联网系统依赖于集中式架构。信息从物联网系统发送到互联网，其中数据被存储和处理。随着物联网设备数量将达到数十亿台，集中式系统将限制可扩展性，并暴露出许多弱点，从而危及安全性。对于供应链应用程序来说，拥有可扩展且安全的机制至关重要，因为敏感数据将跨越组织边界进行决策。

### 4.3 区块链与物联网结合：解决供应链挑战的方案

查看供应链的需求和商业需求/挑战，如数据捕获和访问的安全性、无缝和设备独立的数据捕获、独立于供应链/交易实体的物理位置、数据的实时和可靠的可用性以及成本效益性，可以指出所需的技术类型。除此之外，数据的捕获和分析需要具有可扩展性和可靠性以实现实际利益。到目前为止讨论的供应链问题可以通过同时采用区块链和物联网解决或最小化。区块链和物联网一起将物理世界数据无缝地带入计算环境，并在多方场景中将其存储在分布式账本中，从而弥合了信任差距。请参考图 1 了解高级架构。区块链和物联网结合解决供应链挑战的主要原因是：

![图 1](img/f09-01-9780128171899.jpg)

图 1 高级物联网区块链架构。

#### 4.3.1 可扩展性

多个物联网设备可以将数据传输到一个引导数据进入区块链网络的网关，该网络采用分布式账本技术运作。将会有多个网关将数据馈送到区块链网络中。物联网网关正在为这样的大容量设计。当今的区块链网络是企业级系统，处理大量数据。因此，对于大规模数据驱动型供应链组织来说，这是一种可扩展的方法来处理数据量。

#### 4.3.2 可靠性

根据 Gartner 的预测，到 2020 年将有 2000 亿个互联网连接的物品[[16]](S0065245819300336.xhtml#bb0085)。其中许多互联网连接的物品将利用、开发和使用物联网设备。物联网设备被设计和调整用于高速、大容量、低功耗、低延迟数据传输，短距离和长距离数据传输。正在进行研究以减少数据丢失、数据锁定、数据损坏和连接问题。越来越多的先进芯片组和架构被设计用来提高相应的标准。像 ZigBee、WiFi、WiMax、Z-Wave、LPWAN 等技术正在被开发以提高可靠性。

#### 4.3.3 安全

这个物联网-区块链系统的数据安全威胁在于物联网设备及其网络。一旦数据进入区块链网络，数据就是防篡改的和不可变的，因此是安全的。各种类型的设备及其与网关的集成，使用 WiFi 和其他无线通信确实对物联网数据构成威胁。物联网数据安全漏洞更可能发生在物联网网络中，其安全性和安全性与网络安全相同。物联网安全正在被研究和努力使这种技术组合成功[[17]](S0065245819300336.xhtml#bb0090)。

#### 4.3.4 成本效益/拥有成本

许多区块链系统都作为一种服务提供，按交易数据的单位计费。例如，甲骨文区块链平台云服务按每笔交易基础提供[[18]](S0065245819300336.xhtml#bb0095)。因此，区块链成本拥有数据驱动。随着区块链在云平台上的可用性以及没有基础设施的前期成本，解决方案变得负担得起，许多公司正在试用。此外，许多公司也提供免费试用版本以便于采用。物联网确实需要对传感器进行投资，诸如甲骨文等公司正在提供与这些传感器的连接器。总的来说，拥有成本是存在的，并且主要由传感器的数量和数据量驱动。但随着它为企业带来的好处，没有前期成本和拥有成本的减少，投资是非常负担得起的。

#### 4.3.5 透明度和可访问性

随着数据存储在区块链网络中，所有区块链服务（包括基于超级账本的甲骨文区块链服务等企业级解决方案）均提供基于移动应用的数据访问，具有所有安全性和可访问性。随着区块链系统作为基础数据存储系统从物联网系统中获取数据，区块链中的智能合约使数据对合作伙伴具有无缝透明的访问权限。

图 1 展示了供应链解决方案的高级区块链物联网概念架构。可以看出，它将所有供应链合作伙伴汇集到区块链系统（共同平台）中，通过物联网机制从各种系统中捕获数据。捕获的数据可以是任何物理或环境数据到特定产品数据。该图描述了一个基于云的区块链架构。该架构的起源在于通过传感器或 RFID 等任何机制捕获数据并将其传输到网关。网关将向区块链提交数据。在这种架构中，通过物联网捕获的数据直接输入区块链，没有中间数据存储。该架构没有物联网平台来存储数据，然后将其传输到区块链系统。因此，该架构消除了物联网平台中捕获数据的基础设施需求。相反，由于缺乏物联网平台，在网络上传输数据之前无法对数据进行加密，只有基本身份验证的可能性。拥有物联网平台可以帮助在网络传输之前进行高级身份验证和加密。如图 1 所示的架构将具有最低的所有权成本，并且应该是任何公司朝这个方向迈出的第一步。

区块链和物联网相结合的这种架构可以帮助解决各种供应链问题。让我们浏览一下列出的供应链问题及其所提供的解决方案。

产品/订单追踪和产品可追溯性/召回/防伪 — 这是识别出的供应链挑战之一。解决这两个问题的方法非常相似。在供应链中产品跟踪和可追溯性的主要挑战是多个利益相关者、实时跟踪跨利益相关者的物理货物运动信息以及能够在产品生命周期的任何给定时间点追溯所有权。这些信息不仅对供应链内的利益相关者和希望获得其需求实时信息的最终客户有用和值得，而且在这些领域的信息空白是透明度和失去客户满意度。区块链和物联网的结合可以帮助跟踪供应网络中物理货物运动的信息，并使其对任何利益相关者都可用。这可以可靠、实时且以一种受控的方式提供信息，否则是不可能的。解决方案的核心在于在各个关键供应链基点设置传感器，这些传感器可以捕获被认为的信息并将其传输到基于云的网关系统，最终将其传输到区块链网络。一旦数据在区块链网络中可用，就可以使用智能合约安全地与合作伙伴共享数据，从而带来控制和真实性。智能合约可以决定合作伙伴的访问级别和信息。

图 2 展示了一种带有物联网区块链组合的供应链合作伙伴协调机制。该机制不仅将帮助建立订单的跟踪和追踪，还将帮助建立可用于认证和产品召回的产品可追溯性。该机制还将提供订单的实时监控。

![图 2](img/f09-02-9780128171899.jpg)

图 2 物联网区块链架构的供应链合作伙伴机制。

此机制的好处和用途如下：

母公司—这是接收要履行的客户订单的公司。它可以有机制在区块链网络中共享订单详情，这可以进一步帮助合同制造商（和供应商）了解需求（零件）的透明度。根据来自其他合作伙伴的区块链中的 IOT 数据，它可以得出以下结论：

+   • 基于区块链数据的实时订单跟踪（从供应商的零件追踪，服务追踪，物流追踪，到制造追踪）。

+   • 产品从制造到客户的可追溯性。

+   • 更容易的产品召回。

+   • 基于区块链可用数据和 IOT 捕获的数据，更好地分析故障的根本原因。

合同制造商—如今，世界制造业的中心在低成本经济体中。区块链中可用的实时 IOT 数据（特别是子装配或合同制造商）可以帮助所有供应链合作伙伴更好地了解情况，并做出知情决策。来自制造商到的数据可用性的一些好处是：

+   • 产品序列化报告用于认证和追溯性。

+   • 基于 IOT 数据的制造状态的实时报告。

+   • 用于可追溯性/故障分析和召回目的的制造/存储条件的分钟级细节。

+   • 来自供应工厂到主要工厂的子装配到达的确认。

+   • 供应商材料装运时间表和确认。

+   • 故障信息/潜在供应链中断。

第三方仓库—由于这是在途存储，到达和出发的实时数据，这些信息对所有供应链合作伙伴都有帮助。此外，由 IOT 捕获的物理存储条件数据非常重要，因为这些条件大多数组织很难监测并且超出了他们的控制范围。这些提供以下好处：

+   • 与制造商的同步物流，使用 IOT 实时出发扫描。

+   • 产品存储条件的分钟级细节，用于追溯/故障分析和召回目的。

+   • 跨地理区域的货物实时监控。

分销中心/仓库 - 由于这是供应给客户或零售商的最后一个存储点，到货和离开的实时数据有助于通知客户即将到货、到达的确切时间表等。以下是好处：

+   • 使用区块链智能合约同步现场服务和产品交付。

+   • 制造商使用区块链智能合约的高级警报/ASN。

+   • 产品存储条件的分钟级细节，用于追溯/故障分析和召回目的。

+   • 根据时间表同步仓库人员配置，从而减少不必要的人员配置。

最终客户 - 今天的客户几乎没有机会验证产品的真实性和了解其来源。同样，大多数制造商几乎无法获得最终客户的信息，这在召回情况下非常困难。通过物联网，当产品交付给客户时可以捕获数据，并将其存储在区块链中，从而使这些信息对多个利益相关者可用：

+   • 母公司知道最终客户产品已交付。

+   • 客户扫描以根据区块链智能合约检查产品来源。

+   • 产品序列化和最终客户信息以供召回。

+   • 可能性，即最终客户向制造商提供产品反馈。

图 2 描述了一个使用案例，其中客户在公司下订单，由合同制造商完成制造，并且物联网区块链机制如何帮助在跨地理区域的多方合作伙伴场景中进行跟踪和追踪。

#### 4.3.6 农业供应链

农业供应链中的挑战主要集中在最后一环的农场级连接性、各种农场和农民信息的获取，以及将这些信息提供给其他合作伙伴以实现可追溯性、真实性和来源的目的。农场和农民级别的电子数据捕获特别具有挑战性，原因是缺乏基础设施、农民缺乏采用数字方法的动力以及对农民进行培训。解决这个问题有两个方面。一方面是激励农民进行数字化，另一方面是引入物联网和区块链等技术，使其价格合理且易于适应，从而革新基层农业供应链。对于激励农民的问题，考虑以下几点：

+   • 激励计划鼓励农民将农产品数字化。这意味着农民必须将农场和产品级信息转换为数字格式并共享。这些可以通过某些移动或网络应用完成。

+   • 为农民提供数字化土地数据、收获类型、土地位置等激励，不仅限于农场数据，并通过某些移动或网络应用使其易于数字化。如果能加载相应的照片就更好了。特别适用于像棕榈果等大型农产品。

+   • 每个农民输入系统的数据都会获得激励，以便他们更喜欢数字化。提供的激励应以货币价值形式提供。

+   • 当农民将产品/产物销售给代理商、磨坊或第三方时，所有权的转移需要进行注册。这些也需要以数字格式捕获，并激励农民进行数字交易。

图 3 如何 IOT 区块链组合可以帮助振兴农业供应链。这种架构将通过引入土地信息、收获日期、收获产品、土壤类型、农场采用的农业实践、农民详细信息、农药使用等信息实现实时溯源和可追溯性，最终为顾客提供附加价值的最终产品。激励措施和支付是这一解决方案的重要组成部分，将与供应链解决方案并驾齐驱。激励措施将使农民意识到并激励他们采用数字方法。

![图 3](img/f09-03-9780128171899.jpg)

图 3 农业供应链解决方案与 IOT 区块链架构。

以下是此数字解决方案中各种农业供应链合作伙伴及其角色。

让我们看看各个合作伙伴以及他们在 IOT 区块链系统中的使用方式：

农民——根据描述，农民将被提供移动和网络应用程序，以数字化农产品和所有其他信息。物联网将在从田野捕捉这些信息并将其传输到区块链中起关键作用。这种解决方案也可以不基于物联网的数据捕获，而在那种机制中，农民可能需要手动输入这些数据。农民数据必须通过移动或网络应用程序分别捕获，并不是通过物联网系统。

收获产品的物联网数据捕获可以自动分配批次/序列号，从而帮助对产品进行个体跟踪。通过物联网捕获的数据或手动输入的数据可以传输到区块链，供最终消费者使用的任何报告和分析。当农民将产品出售给代理商和其他人时，所有权的转移将被注册，从而实现追溯性和建立溯源。农业价值链的其他成员，如代理商等，在 Fig. 3 中没有描绘出来。这些也可以成为区块链网络的一部分。

加工厂 - 大部分的农产品，无论是棕榈果、稻米、可可、咖啡还是其他水果如石榴、橙子、苹果，都会在加工厂进行清洁、提取、包装。这些场所和储存地点的物联网传感器可以极大地增强追溯性，并为最终客户提供产品储存标准的信息，如压力、温度、湿度等的物理条件。到达/离开的扫描（通过 RFID 可能实现）可以准确指出产品在任何位置的到达/离开时间和停留时间。在区块链中拥有这些信息可以极大地改善收成的追溯性，以便在出现问题或建立溯源时向任何合作伙伴提供支持。这些信息在认证油品，如 RSPO 认证的棕榈油（RSPO 代表可持续棕榈油圆桌会议）中起着关键作用。

运输——任何易腐食品的安全运输，如巧克力、水果、果汁，是确保消费者手中获得安全和新鲜产品的重要部分。 今天，消费者对这些产品的运输了解非常有限甚至没有信息。 在运输过程中或仓库出库扫描时捕获物联网数据可以极大地帮助弥合这一重要差距。 卡车/海运、仓库中的传感器可以捕获物理存储条件，并将其提供给区块链网络。 基于智能合同，各个合作伙伴可以访问这些信息，并为产品做出明智的决策。 即使需要，此信息也可以提供给最终客户，以确保真实性和透明度。

制造商——有许多农产品用于制造食品和非食品产品。 这可以包括消费者可食用的产品，如饼干、巧克力、罐头食品、婴儿产品，以及消费者产品，如护肤品、肥皂、洗涤剂，以及工业产品，如润滑脂和油。 追踪所有权转移给制造商是溯源中的一个重要方面。 物联网传感器可以在交易发生时帮助跟踪此过程。 将它们存储在区块链中将有助于建立溯源和根据智能合同为任何利益相关者提供访问数据的可追溯性。 在制造过程中以及之后，各种环境/物理和与产品相关的属性的状态可以帮助确定最终产品的质量、新鲜度和消费者手中的其他特性。 在制造过程中的异常情况（例如婴儿产品）可能非常危险，但今天这些信息是不可用的。 通过物联网区块链机制，这些信息可以被提供并分析，并在发生任何错误或在随机样本测试中检测到任何问题时帮助建立根本原因分析。

零售商-对于零售商来说，食品的质量和新鲜度至关重要。根据 Banerjee 和 Venkatesh 的观察[[4]](S0065245819300336.xhtml#bb0025)，美国大约有 4800 万人每年因食源性疾病而生病，因此质量的重视是非常必要的。像快餐店发生大肠杆菌感染这样的问题，对于零售商和最终消费者而言，对生产过程、采摘过程、储存等方面的清晰可见度是极其重要的。当这些数据从农场到餐桌都可以在区块链上追踪和分析时，所有这些就是可能的。换句话说，IOT 区块链架构可以帮助获取从源头/起源到最终消费的信息。零售商店中的储存条件在维持产品的新鲜度和无菌性方面起着关键作用。这些可以通过使用 IOT 传感器追踪和使用区块链网络存储信息进行分析和预防来检查和控制。

如图 3 所示的整个解决方案，农业物资供应链结合了 IOT 和区块链，可以实现从农场到餐桌的溯源，这只有在农民被激励数字化的情况下才能实现。

#### 4.3.7 数字化汽车供应链

如今，汽车行业的技术更多地关注于增强汽车与外界的连接能力和车内体验，而不是车辆的内部性能[[19]](S0065245819300336.xhtml#bb0100)。这些是连接到互联网的汽车，通过传感器传递车辆状态和工作状况的数据，并将数据存储在云中。特斯拉是连接车的一个很好的例子，车辆本身就像一台计算机一样运作。我们已经进入了汽车出厂即连接到互联网并且正在成熟的时代。如今，几乎所有的汽车制造商都提供从中档到高端的连接车服务。车辆的信息或运营统计数据大多存储在云端，主要由汽车制造商使用，用于分析运营数据，为车主提供更优质的汽车拥有体验，创造新的收入流，提供先进的导航和/或预测性的车辆警报。但是数字汽车领域的下一个级别，即汽车制造商、经销商、服务提供商、零部件制造商和保险公司都与一个真实数据源相互连接的级别，目前仍处于发展中，尚未开发。对于汽车制造商来说，他们不仅要意识到他们之间的竞争，而且还要意识到他们正在与优步、谷歌和许多其他利用颠覆性技术开发各种服务和功能的公司竞争。这些范围从自动驾驶车辆、二手车购买流程（Carvana、fair、vroom）、汽车融资、安全系统、自动化和在线服务等等。这就是 IOT 区块链组合解决方案可以帮助解决这一不可逾越的问题，为车主提供无缝服务、安全性、预测性警报和体验的地方。

图 4 描述了一个未来主义汽车供应链，其中每个供应链合作伙伴都通过物联网相互连接，物联网是数据捕获机制，区块链是横跨系统和位置的中央存储库。它聚焦了将受益于物联网区块链架构的供应链关键成员。

![图 4](img/f09-04-9780128171899.jpg)

图 4 汽车供应链解决方案与物联网区块链架构。

图 4 展示了可以集合在单一区块链平台上的汽车合作伙伴。需要注意的是，所有合作伙伴都将成为区块链网络中的节点。安装在汽车上的物联网传感器将捕获数据并传输到集中式区块链网络中。每辆车都将有一个唯一的车辆识别号，该号码将被标记到区块链中。汽车制造商在获得车辆识别号（VIN）时将车辆注册到区块链中。从汽车制造商到经销商的所有权转移时，区块链网络将进行注册。汽车上的物联网传感器将通过物联网网关将数据传输到区块链网络。这些数据可以被经销商、服务公司、保险公司和零部件制造商访问。这将有助于进行维护或故障的预测分析。当汽车从汽车制造商转移所有权到经销商再到车主时，将建立追溯性。这种架构可以实现对车主所经历的任何问题的远程诊断能力，节省时间和精力。零部件制造商将从服务技术人员那里获得零件所需的提前警报，这将有助于建立零件的起源并跟踪更换车辆中的零件，从而缩短供应链的交货时间。保险公司将透明地了解车辆历史的状态，以及有关其以前所有者和车辆使用情况的信息。它还将了解以前车辆所有者的驾驶历史，这可以帮助他们评估保费。车辆特定信息不会因所有权转移而丢失，就像今天发生的一样，因为车辆将通过区块链中的唯一 VIN 号码进行跟踪。这将极大地帮助保险公司，并使他们能够更好地了解车辆性能、驾驶历史、对车辆进行的维护，从而根据情况调整保险。

#### 4.3.8 数字家庭和办公室

智能家居不仅关乎设备，还涉及服务。设备与服务的结合将使消费者的生活更加舒适、安全和高效。这些服务包括但不限于家庭安全、能源控制、照明控制、健康、交通、环境和信息传播，将提升消费者日常生活的效率。目前的限制主要在于这些设备的互操作性不足，这主要是由于缺乏共同的协议、可访问性问题和信息的单一存储库。市场上已有一些关键的智能家居参与者（在特定领域），这些参与者需要结合起来以提升客户体验。图 5 展示了这些关键领域以及它们如何相互交互。这些产品已经存在并在市场上发展到一定程度，可以帮助改善并将用户体验推向新的高度。

![图 5](img/f09-05-9780128171899.jpg)

图 5 展示了基于物联网和区块链架构的智能家居/办公室解决方案。

在图 5 中，物联网（IOT）和区块链的最早应用之一是在家庭安全领域。目前这些系统尚未采用区块链系统运行，因此无法为某人提供部分访问权限或精确到邻居级别的访问权限。为了实现这一点，需要使用物联网和区块链进行严格和灵活的认证。区块链系统将保存智能合约，以允许或拒绝特定用户的登录。区块链中的智能合约还可以与物联网一起实现对房屋或办公室的部分访问。在美国，Comcast 已经在家庭安全领域的部分和临时访问中尝试使用物联网和区块链 [[20]](S0065245819300336.xhtml#bb0105)，但需要注意的是，这些仍然处于公司（服务提供者）的孤立状态。

IOT 和 Blockchain 结合的另一个主要用例是家庭/办公室/仓库照明、温度和警报控制。这些范围从持续监测温度和照明到根据消费者的需求设置警报。远程管理温度、警报、烟雾探测器、照明设备、冰箱、洗衣机、洗碗机等能力是今天设备的关键目标。这些设备正在独立运行并且是孤立的。这些系统今天专注于自动化和向消费者传播信息的目的。当务之急是将它们汇聚起来，以便它们可以引领下一代服务。这些可以将这些设备连接到公用事业公司进行账单结算或电气故障的根本原因。可以开发能力将零售店与洗衣机或洗碗机连接起来，以便无缝地（有或无用户干预地）下订单洗涤剂或洗涤袋。一个系统中的警报也可以对其他系统有所帮助，例如温度下降可能是安全漏洞的指示，或者火警可能是公用事业服务提供商的良好信息。同样，如果安全信息和其他方面（如探测器和控制）对保险公司透明，这将帮助它们提供更好的保障，最终节省消费者的成本。

IOT 区块链集成可以扩展到从照明、温度、洗衣机、冰箱、洗碗机、警报和控制设备到家庭、办公室和仓库的整个设备和服务的范围。当一个系统或应用程序能够智能地控制家庭或办公室中的所有设备时，真正的好处将开始显现。这种应用将基于一个集成的 IOT 和区块链平台系统，而不是一个独立的应用程序。在这些情况下，IOT 将发挥关键作用，因为它是传感器，将捕捉异常以触发警报或其他操作。区块链中的数据将帮助在系统之间进行协调和交叉引用（提供透明度）。

#### 4.3.9 制造系统和分销行业

制造业已经全球化。它有着分布在各地的多个合作伙伴。这些制造系统的同步是非常重要的。由于合作伙伴的多样性，几乎不可能将它们全部带到同一个信息平台上，除非由区块链驱动。用于数据捕获的 IOT 系统和用于数据存储的区块链网络是一个强大的组合，可以彻底改变制造系统。图 6 描述了如何使用 IOT/区块链组合将来自多个合作伙伴的多个 ERP 系统汇集在一起的高层架构。这张图帮助我们理解了 IOT 的独特作用，即从各个 ERP 捕获数据并将其传输到区块链网络。该图还描述了可以直接从 ERP 系统捕获数据并与区块链进行接口连接（无需 IOT）。从 IOT 系统捕获的数据可能包括运输、物流、生产产出、制造线问题、物料质量问题等。从 ERP 系统捕获的数据（无需 IOT）可能包括订单、供应、主数据等，并可以直接输入到区块链中。区块链系统使数据、合作伙伴和平台独立，并使其可供任何分析或决策使用。例如，如图 6 所示，来自 ERP 的供应信息，如现有库存、在制品数据，以及来自子组装厂（工厂 1）的制造问题（如果它是多个装配厂（如工厂 2）的前级工厂）是对多个合作伙伴的关键信息。这就是通过 IOT 捕获的信息，并在区块链中可用的地方需要是独立于各个工厂系统，并对每个供应链合作伙伴都可用的地方。智能合约和对合作伙伴数据的控制访问可以在区块链网络中启用。所有这些都将成为这种 IOT 区块链解决方案的可能性。

![图 6](img/f09-06-9780128171899.jpg)

图 6 展示了使用物联网和区块链进行多系统同步的表示。

同样地，对于拥有熔炉、汽轮机和锅炉的重工业来说，数字孪生是当务之急。数字孪生是物理设备的虚拟副本，用于运行模拟。数字孪生是一个计算机程序，它以物理对象或系统的真实世界数据作为输入，并生成预测或模拟，展示这些物理对象或系统将如何受到这些输入的影响。数字孪生之所以存在，完全依赖于物联网系统。物联网传感器安装在物理设备上，并传输用于分析的数据。这些数据可以是系统状态或某些输入的行为。如果这些数据传输到区块链，那么它将帮助根据其访问权限使其可用于合作伙伴，并将根据其专业知识使数据民主化，以供分析。像 GE、Chevron、Schneider Electric 等大多数主要制造公司已经投资于数字孪生，并从中获得数百万的好处 [[21]](S0065245819300336.xhtml#bb0110)。

在分销行业，供应链交易可以输入到区块链中，这可以帮助使此信息对所有供应链合作伙伴可用。这些合作伙伴包括但不限于制造商和供应商，这可以帮助 POS 报告和船舶和借记索赔。图 7 描述了分销行业供应链交易的简化视图，可以输入到区块链中。这个简单的图表展示了如何从区块链中提取供应商/制造商的 POS 报告和船舶和借记索赔，而不是从单独的系统（ERP 或其他交易系统）。这将带来以下好处：

![图 7](img/f09-07-9780128171899.jpg)

图 7 分销行业供应链交易和使用的简化表示。

##### 4.3.9.1 提高运营效率

通过简化船货索赔流程，通过区块链进行销售点报告，将不再需要单独的库存报告和对账。这将改进索赔流程，因为它将减少供应商和分销商的手工干预。这将减少手工报告和对账，从而为其他目的释放资源，提高效率。

##### 4.3.9.2 减少索赔拒绝并加速资金流动

通过直接从区块链系统提取的数据，索赔将获得未经篡改的数据，这将是准确的，并且对所有合作伙伴完全可接受。此外，通过区块链系统的透明度在库存追溯中与销售和采购订单详细信息可以提供正确的成本给客户，从而提高索赔减少并加速资金流入系统。

在分销业务中，物联网可以在仓储和物流领域发挥作用，在存储或运输过程中帮助追踪温度或物理条件。它可以跟踪对于敏感产品的湿度、压力、温度或震动。这在产品追溯的解决方案中已经进行了详细讨论。

本节讨论的解决方案提供了一个统一的观点，即区块链与物联网是非常有效的供应链解决方案。区块链在其采用和增长方面较慢，但其应用范围广泛而全面。与物联网结合，它将成为一个强大而重要的架构，将使许多工具和报告能够帮助管理者改进供应链操作。这种组合将使数据民主化，打破个别系统的障碍。该解决方案最终将增加产品价值，简化供应链，并赋予客户权力。

## 5 物联网-区块链组合在供应链解决方案中的经济价值

市场研究公司 Gartner 预测，区块链将在 2025 年增加 1760 亿美元的业务价值，并在 2030 年增加 3.1 万亿美元[[22]](S0065245819300336.xhtml#bb0115)。哥伦布[[23]](S0065245819300336.xhtml#bb0120)分享了来自各种研究的预测，并表示全球物联网市场将从 2016 年的 1570 亿美元增长到 2020 年的 4570 亿美元。哥伦布[[23]](S0065245819300336.xhtml#bb0120)还表示，离散制造业、运输和物流以及公用事业将在 2020 年带领所有行业的物联网支出，平均每个行业都达到 400 亿美元。贝恩公司预测，到 2020 年，业务对业务的物联网细分市场将每年产生超过 3000 亿美元的收入。波士顿咨询集团预测，到 2020 年，物联网市场将达到 2670 亿美元。物联网和区块链的结合肯定会有助于实现这些数字，甚至可能超过预测。

IOT-Blockchain 结合可以以不同方式为任何供应链解决方案带来价值。显然，其建立、流程定义和实施都需要一定的投资。但一旦实施，它可以通过摆脱外围系统、减少人力依赖、消除冗余流程、简化仓储流程和自动化供应链流程来帮助降低成本，这些流程原本是依赖报告和人工驱动的。它还可以通过能够追踪和溯源、建立起源和更顺畅的召回来增强品牌价值。它还可以通过解锁因系统孤立工作而不可能实现的机会来增加收入。随着产品和服务在各个领域的同步以及采用以区块链为骨干、由物联网支持的供应链单一平台，收入将会比今天更好地增长。

经济价值可以立即通过流程优化开始，从而实现成本降低。随着时间的推移，随着技术的成熟，新的收入生成模型将出现。这种供应链解决方案的显著特点是信任和时间。强调的重点是，在供应链伙伴之间缺乏信任的情况下，整个讨论是无效的。此外，物联网和区块链技术正在成熟，它们需要时间来发展和进一步演变，才能完全吸收和增强供应链流程。

数字革命的特征在于不同技术的融合，以改善客户和业务流程。物联网和区块链结合的未来也将融合，模糊数字和物理世界的界限。它将利用人工智能和机器学习算法，并利用区块链数据进行决策。作为区块链物联网平台，它将能够引入更多合作伙伴和他们的数据用于决策，这将使世界变得更加宜居！

## 6 结论

物联网和区块链作为独立技术在任何领域的应用都受到限制。在供应链和物流领域，通过物联网、区块链和其他供应链系统（如 ERP）的组合架构，可以获得显著的收益。所呈现的架构是通用的，可以帮助任何类型的供应链编排，并且强调和讨论了一些具体问题。本章分别讨论了今天在农业供应链、汽车供应链、产品或订单跟踪、可追溯性和召回、伪造、数字家庭、制造和分销供应链中面临的问题，以及如何利用物联网区块链组合来解决这些挑战。从通用供应链流程到特定的农业或汽车供应链，通过消除中间商、带来透明度并建立起溯源或追踪到详细层面的好处是相似的。区块链和物联网作为一种技术正在共同成熟和发展。它们彼此依存，与两者在一起发展的变化最大。物联网迫切需要区块链的特性，因为它带来了安全性、不可变性和智能合约，而区块链需要物联网来引导数据的流向，将每个方面转化为供应链更加有效的巨大机遇。物联网区块链组合将彻底改变供应链合作伙伴今天的互动方式。这种组合将为产品增加价值，建立伙伴之间的信任，降低供应链成本，提高流程效率，避免信息空白，并赋予客户更大的权力。

## 参考资料

[1] Palmer M. 数据就是新的石油。在：*ANA MarketingMaestros.* CNBC; 2006\. 3 November [`ana.blogs.com/maestros/2006/11/data_is_the_new.html`](http://ana.blogs.com/maestros/2006/11/data_is_the_new.html). (a) Reid D. ‘万事达卡（Mastercard）的老板刚刚告诉沙特听众‘数据就是新的石油’。2017\. [`www.cnbc.com/2017/10/24/mastercard-boss-just-said-data-is-the-new-oil.html`](https://www.cnbc.com/2017/10/24/mastercard-boss-just-said-data-is-the-new-oil.html).

[2] Alicke K., Rachor J. *供应链 4.0——下一代数字供应链。* McKinsey & Company; 2016\. [`www.mckinsey.com/business-functions/operations/our-insights/supply-chain-40--the-next-generation-digital-supply-chain`](https://www.mckinsey.com/business-functions/operations/our-insights/supply-chain-40--the-next-generation-digital-supply-chain)。

[3] O'Byrne R. 每个人都可以削减供应链成本的 7 种方法。在：*CSCMP's Supply Chain Quarterly.* 2011\. [`www.supplychainquarterly.com/topics/Strategy/scq201102seven/`](https://www.supplychainquarterly.com/topics/Strategy/scq201102seven/).

[4] Banerjee A., Venkatesh M. *使用物联网和区块链进行产品追踪和溯源。* Infosys Ltd; 2019\. [`www.infosys.com/Oracle/insights/Documents/product-tracking-tracing.pdf`](https://www.infosys.com/Oracle/insights/Documents/product-tracking-tracing.pdf).

[5] Leeson T. *汽车制造商如何从连接的供应链中受益。* [`blogs.opentext.com/how-auto-makers-benefit-from-the-connected-supply-chain/`](https://blogs.opentext.com/how-auto-makers-benefit-from-the-connected-supply-chain/). 2018.

[6] Foley M.J. *首批大规模使用微软连接车辆平台的汽车即将上市。* ZDNet; 2019\. [`www.zdnet.com/article/the-first-cars-using-microsoft-connected-vehicle-platform-at-scale-are-coming/`](https://www.zdnet.com/article/the-first-cars-using-microsoft-connected-vehicle-platform-at-scale-are-coming/).

[7] Zhong R.Y., Xu X., Klotz E., Newman S.T. 在工业 4.0 环境下的智能制造: 一项综述。 *Engineering.* 2017;3:616–663.

[8] Banerjee A. *Infosys.* [`www.infosys.com/Oracle/white-papers/Documents/integrating-blockchain-erp.pdf`](https://www.infosys.com/Oracle/white-papers/Documents/integrating-blockchain-erp.pdf). 2018.

[9] Banerjee A. 第三章—区块链技术: 从 ERP 中获取的供应链见解。 *Adv. Comput.* 2018;111:69–98 2018.

[10] Litan A., Lheureux B., Pradhan A. *将区块链与物联网整合，加强多方流程中的信任.* Gartner Research; 2019.

[11] Elena-Lenz C. *物联网: 六大关键特征.* Frog; 2015\. [`designmind.frogdesign.com/2014/08/internet-things-six-key-characteristics/`](https://designmind.frogdesign.com/2014/08/internet-things-six-key-characteristics/).

[12] Patel K.K., Patel S.M. 互联网物联网-IOT: 定义、特征、架构、技术支持、应用及未来挑战。 *Int. J. Eng. Sci. Comput.* 2016;6(5):6122–6131.

[13] Meulen R.V. *Gartner 称 2017 年将有 84 亿个连接的“事物”被使用，比 2016 年增长了 31%.* Gartner Research; 2017\. [`www.gartner.com/en/newsroom/press-releases/2017-02-07-gartner-says-8-billion-connected-things-will-be-in-use-in-2017-up-31-percent-from-2016`](https://www.gartner.com/en/newsroom/press-releases/2017-02-07-gartner-says-8-billion-connected-things-will-be-in-use-in-2017-up-31-percent-from-2016).

[14] 商业内幕情报. 到 2020 年，地球上将安装 240 亿个物联网设备。 在: *商业内幕.* 2016\. [`www.businessinsider.com/there-will-be-34-billion-iot-devices-installed-on-earth-by-2020-2016-5?IR=T`](https://www.businessinsider.com/there-will-be-34-billion-iot-devices-installed-on-earth-by-2020-2016-5?IR=T).

[15] Lewis K. *数字转型是一次旅程，企业规模的物联网平台：沃森，物联网博客.* [`www.ibm.com/blogs/internet-of-things/enterprise-scale-iot-platform-watson/`](https://www.ibm.com/blogs/internet-of-things/enterprise-scale-iot-platform-watson/). 2017.

[16] Hung M. *引领物联网.* Gartner; 2017\. [`www.gartner.com/imagesrv/books/iot/iotEbook_digital.pdf`](https://www.gartner.com/imagesrv/books/iot/iotEbook_digital.pdf).

[17] Pal A. *物联网（IoT）-威胁与对策.* CSO; 2019\. [`www.cso.com.au/article/575407/internet-things-iot-threats-countermeasures/`](https://www.cso.com.au/article/575407/internet-things-iot-threats-countermeasures/).

[18] Oracle. *区块链平台定价选项.* [`cloud.oracle.com/blockchain/pricing`](https://cloud.oracle.com/blockchain/pricing). 2018.

[19] 麦肯锡公司. *驱动联网汽车的因素.* 麦肯锡公司-汽车与装配; 2014\. [`www.mckinsey.com/industries/automotive-and-assembly/our-insights/whats-driving-the-connected-car`](https://www.mckinsey.com/industries/automotive-and-assembly/our-insights/whats-driving-the-connected-car).

[20] Davis N. *连接家庭的区块链：结合安全性和灵活性.* 康卡斯特实验室; 2018\. [`labs.comcast.com/blockchain-for-the-connected-home-combining-security-and-flexibility`](http://labs.comcast.com/blockchain-for-the-connected-home-combining-security-and-flexibility).

[21] Eshkenazi A. *数字孪生的真正好处.* APICS 供应链管理现在; 2018\. [`www.apics.org/sites/apics-blog/think-supply-chain-landing-page/thinking-supply-chain/2018/09/21/real-benefits-from-digital-twins`](http://www.apics.org/sites/apics-blog/think-supply-chain-landing-page/thinking-supply-chain/2018/09/21/real-benefits-from-digital-twins).

[22] Granetto B., Kandaswamy R., Lovelock J., Reynolds M. *预测：区块链商业价值，全球范围内，2017 年至 2030 年.* Gartner 研究; 2017\. [`www.gartner.com/en/documents/3627117`](https://www.gartner.com/en/documents/3627117).

[23] Columbus L. *2018 年物联网预测和市场估值综述.* Forbes; 2018\. [`www.forbes.com/sites/louiscolumbus/2017/12/10/2017-roundup-of-internet-of-things-forecasts/#671f2fe51480`](https://www.forbes.com/sites/louiscolumbus/2017/12/10/2017-roundup-of-internet-of-things-forecasts/#671f2fe51480).

![u09-01-9780128171899](img/u09-01-9780128171899.jpg)

**阿纳布·巴内尔吉，博士**

**印度 Infosys 有限公司**

高级顾问，企业应用服务

电子邮件: Arnab_banerjee08@infosys.com

领英: [`www.linkedin.com/in/arnab-banerjee-a44697b/`](https://www.linkedin.com/in/arnab-banerjee-a44697b/)

**Arnab Banerjee** 是印孚瑟斯有限公司企业应用服务的首席顾问。他在 ERP、IOT 和区块链技术领域提供咨询服务。他拥有超过 17 年的咨询经验，跨越北美、欧洲和亚洲。在他的区块链咨询工作中，他帮助实施 Oracle 区块链云服务。这涵盖了从识别用例、解决方案架构到实施的全过程。对于 IOT 应用咨询角色，他帮助实施与 ERP 系统集成的企业级工业 IOT 解决方案架构。他是供应链领域的 ERP 实施专家。他的研究兴趣包括信息技术、IOT 和区块链应用与 ERP 和其他卫星系统的整合。他在逆向供应链、精益/敏捷/敏捷化举措、约束理论、供应链转型和人道主义物流领域有广泛的发表，多年来在各种同行评议的国际期刊、国际研究会议、案例研究、书籍章节、白皮书和观点文章上发表了超过 35 篇研究论文。他拥有供应链管理博士学位、工业工程硕士学位和机械工程学士学位。他是认证的 Six Sigma 黑带冠军。他被列入《世界名人录》2015 年版。
