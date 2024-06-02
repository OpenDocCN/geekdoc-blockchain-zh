© 作者（作者）在 Springer Nature Singapore Pte Ltd. 2022T 的独家许可下。Dounas，D. Lombardi（编）施工区块链区块链技术[`doi.org/10.1007/978-981-19-3759-0_8`](https://doi.org/10.1007/978-981-19-3759-0_8)

# 利用区块链构建项目银行账户（PBA）支付的概念模型在建筑行业中实现自动化

丹尼斯·J·斯科特^（1  ）, 蒂姆·布洛伊德^（1  ）和马玲^（1  ）（1）伦敦大学学院（UCL）巴特莱特可持续建筑学院，英国伦敦丹尼斯·J·斯科特电子邮箱：Denis.scott.19@ucl.ac.uk 蒂姆·布洛伊德（对应作者）电子邮箱：Tim.broyd@ucl.ac.uk 

## 摘要

英国政府于 2012 年发布了一份指导文件，规定使用项目银行账户（PBA）以促进建筑行业的公平和及时支付惯例。本文提供了一个高水平的概念模型，利用区块链来自动化项目银行账户支付。在 PBA 中，项目资金被分割存放在一个独立的银行账户中，就像一个第三方托管账户。在 PBA 之前，总承包商会利用客户的项目支付来重新投资新的工作，或者策略性地拖欠供应链支付以维持正现金流。PBA 废除了总包商作为项目预算的唯一受益者，并为客户提供了对项目支出的透明度。所提出的概念模型允许项目参与者通过用户仪表板批准并执行自动支付。智能合约的安全性之一是它们一旦部署便不可更改的属性；然而，这是有问题的，因为建筑项目经常要进行变更和项目计划的修改。此外，在当前环境中基于以太坊的智能合约由于审计成本和链上托管费用的限制而受到限制。为了减轻这一问题，在 PBA 区块链模型中，交易是通过一个离链应用程序实例化的，该应用程序以签名消息的形式存储预执行的交易。这些消息被推送到区块链，并在获得验证机构的批准后转换为交易。其结果是通过更经济的成本实现支付自动化的一种策略。所提出的模型阐述了 PBA、区块链、离链和资产代币化的高级融合。本文的一个局限是它没有包括任何编程，而是以流程图的形式呈现了这些想法。未来的工作包括对解决方案进行编程。

## 1 引言

建筑业以拖延期限的不良付款惯例而闻名，此外，行业仍在从 2008 年金融危机的相关影响中复苏，这导致许多建筑公司的资本支出增加、竞争加剧以及更大程度面临财务不确定性[2]。商业解决方案包括母公司担保、担保凭证以及对手风险评估[3]。然而，这些解决方案并未解决减少拖延付款的首要问题。解决这个问题将通过改善流动性、减少供应链破产从而增加信任和降低项目风险来增加行业稳定性[4]。2019 年英国国家统计办公室的数据表明，建筑行业每家大公司平均有 1000 家中小企业[5]。这种不平衡导致了过度竞争，并迫使分包商接受不公平的合同条件，比如为了更少的报酬承担高风险工作[6]。

建筑和土木工程行业以风险规避而闻名。从结构角度来看，倒塌的风险与公共安全有关；因此，默认情况下，安全标准很高[7]。从财务角度来看，创新面临挑战，因为利润率低，导致了传统系统的过度使用[8]。技术系统中缺乏创新是生产力低下、对立的供应链关系以及工作流程碎片化的主要原因[9]。制造业等邻近产业成功地通过多个世代不断增加效率，导致了年复一年的渐进性生产力[10]。由于缺乏创新，基础设施项目的平均预算超支 80%，进度落后 20%；此外，自 1990 年以来生产力一直在下降[11]。建筑业还存在公司报告缺乏透明度的问题，利益相关者对项目状况得到不准确的反馈[12]。

全球人口增长给建筑行业带来了额外的压力，要求在技能短缺的情况下更少的资源开发更多的项目[13]。此外，该行业正面临压力，要求在建筑资产的整个生命周期内合并智能技术和减碳解决方案[14]。数字改革的需求是为了满足现代经济的工业依赖关系[15]。区块链包括提高多个领域的效率的潜力，如支付、数据管理、自动化和系统集成[16]。然而，单单依靠区块链不能推动数字革命。它只是科技服务生态系统中需要协调工作的许多组件之一。

项目银行账户（PBA）在建筑项目中的首次记录使用发生在 2005 年，当时英国国防部（MOD）和主承包商的联合企业创建了这个账户，旨在确保政府在整个项目期间的资金审计[17]。英国政府 PBA 指导文件于 2012 年发布，讨论了将项目账户从承包商分离出来以减缓现金挤占和向供应链的级联支付[18]。现金挤占是指承包商不公平地拖欠供应链的支付以改善内部现金流。

本文介绍了一个概念模型，将区块链与 PBA 相结合，以自动处理供应链支付，无需使用中介来管理 PBA。在建议的模型中，分区帐户由一个离线数据库代表，控制客户向供应链释放资金。PBA 区块链模型试图绕过在链上（在区块链上）智能合约的托管，以减少交易费用、开发成本以及项目变更时的重新编码。离线数据库用于存储预先执行的交易，这些交易将在以后的某个时候转换为交易。本文提供了 PBA 区块链模型的高级流程图以及每个交易方的责任。

## 2 文献综述

英国建筑行业中支付延迟的有害影响已在 1964 年班威尔报告[19]中有所记录，该报告是由 Harold Banwell 爵士撰写，他负责记录该行业的现状。建筑业是全球国内生产总值（GDP）的主要贡献者之一；然而，通过创新长期及过时的流程，它可以进一步增加贡献[20]。该行业尤其因采购方式不当、现金流问题和缺乏协作而闻名[21]。因此，客户因未披露的风险和薄利而犹豫承担新工作，导致项目的选择基于低成本而不是长期价值[22]。尽管在数字解决方案方面取得进展，如建筑信息建模（BIM），创新仍然是一个持续存在的问题[23]。

建筑行业的供应链通过不高效的碎片化系统进行交易和沟通，这些系统不进行有效的整合[24]。这些系统使得准确地报告项目状态变得困难，并且缺乏透明度和可追溯性[24]。尽管如此，该行业正在通过国际标准化组织（ISO）、IFC 建筑智能等机构以及支持 BIM 等数字工具的政府法规，推动向更大程度的标准化以提高生产力[25]。

建筑行业由少数主要承包商主导，为许多中小企业（SMEs）提供工作，这导致了 SMEs 之间的过度竞争，并为主要承包商提供了对供应链的控制权 [26]。由于行业的等级性质，SMEs 被迫接受不公平的合同条件和过长的支付期限；承包商实施*现金农场*技术和*付款时支付*条款 [4]。现金农场是承包商实施的一种策略，可以改善内部现金流，但以向供应链迟缓付款为代价，此外，它允许项目预算用于投资新工作，而不是支付未清偿债务 [27]。尽管现金农场对承包商有利，但它是 SME 破产的主要原因 [28]。英国国家统计局的数据表明，英国建筑行业每年平均有 2595 起个体破产案件，占英国整体破产人口的 18%，是英国所有其他行业中最高的 [29]。现金流管理不善的危险体现在卡里利安公司的破产上，该公司曾是英国第二大建筑公司（根据营业额计算）；然而，在 2018 年的清算时，其对中小企业欠下了 13 亿英镑的未支付债务 [30]。从 2009 年到 2018 年，卡里利安的债务从 2.42 亿英镑增加到 13 亿英镑；此外，他们给予中小企业 120 天的支付期限，是英国建筑合同中通常约定的四倍长 [31]。

在建筑行业，纠纷通常通过调解来解决，这是一个轻量级的过程，涉及公正的第三方来管理和解决纠纷；然而，大型公司可以采取更昂贵的方法来对付不满意的解决方法，比如诉讼 [32]。这使中小企业处于不利地位，因为对供应链的付款被扣留，直到法院解决纠纷，这可能需要超过 12 个月的时间 [32]。法国和澳大利亚等国家的法规允许中小企业直接向客户要求拖欠款项；此外，日本对强加不公平支付条件的建筑公司实行严厉的政府强制处罚 [33]。

### 2.1 英国政府公平支付立法

本章节简要概述了促进公平付款实践的英国立法文件。其中一个共同趋势是如何保护中小企业（SMEs）免受不公平合同条件的影响，通过减少支付期限和要求承包商提供本票作为对供应链的善意证据。这些立法文件是相同解决方案的变体，因为支付问题仍未解决，同时采用了不同的方法。英国政府要求其中一些列出的法规是强制性的；然而，由于缺乏政府监督，英国建筑公司仍将这些列出的法规视为建议文件。以下是目前在英国有效的几个支付立法的概述。

**2021: 迅速付款守则（最初于 2008 年发布）**：*商务、能源和工业战略部*修改了其法规，将对中小企业支付的期限从 60 天缩短到 30 天[34]。承包商的违规行为将导致会员资格暂停，需要进行强制恢复计划才能保持身份 [35].

**2014: 建筑供应链支付宪章**：*建筑领导委员会*要求所有承包商向公平支付条款签字承诺书，为客户和他们的供应链提供良好的资金流管理保证[36]。该宪章规定了 30 天的最长支付期限，并建议在公共部门工作中使用项目银行账户（PBA）；此外，宪章还规定对承包商进行关键绩效指标的周期性检查，以确保其遵守[37]。

**2013: 修订的商业债务迟付法规（最初于 1998 年发布）**：由*商务、创新和技能部*发布 [38]。该法规允许供应链对未经支付 30 天的发票收取 8.5%的法定利息[39]。然而，这并不包括 30 天的结算期，因此，承包商可以在发生利息之前策略性地延迟支付长达 60 天（30 天检查工程和 30 天工程获得批准后）[40].

**2012: 项目银行账户（PBA）指导文件**：由英国政府内阁办公室*发布，PBA 使用项目特定的银行账户，该账户与主承包商的银行账户分隔开，为客户提供了在整个项目施工阶段对项目支出的完全可审计性。对供应链的所有付款都将直接从 PBA 执行，从而减轻承包商进行现金农业的风险 [18]。

**2012 年：供应链融资方案**：2012 年由英国政府成立，旨在支持中小企业获得供应链融资，鼓励银行根据获得客户批准的发票向建筑供应链提供低息贷款[41]。

**2011 年：住房资助建筑和重建法案 1996 第二部分**：该法案由英国议会与*商务、能源和工业战略部*共同提出[42, 43]。该法案允许供应链在雇主未付款的情况下合法退出工程，并要求雇主提供已经签署的证据，证明他们有义务在合同约定的付款条件内向他们的供应链提供公平支付[44]。

### 2.2 项目银行账户（PBA）

2005 年，建筑项目中首次记录到项目银行账户（PBA）的使用是通过一个公共部门客户（英国国防地产）和一个主承包商的合资企业；此外，PBA 的建立是由于建筑行业的对抗性质和客户与他们的中小企业有着信任关系[17]。其结果是成功的，PBA 按时管理了对分包商的所有付款，并且在约定预算范围内；此外，所有支出在整个建筑过程中都是公开可审计的[17]。 根据英国政府商务办公室关于 PBA 实施的报告，客户可以在公共部门项目上节省高达 2.5%的费用[45]。PBA 在 2012 年至 2015 年在公共部门进行了试验，并用于管理价值超过 40 亿英镑的工作[18]。 2013 年，北爱尔兰政府规定了价值超过 100 万英镑的建筑项目必须采用 PBA；同样，同一年，威尔士规定了在价值超过 200 万英镑的项目中使用 PBA。

在典型的建筑合同中，总承包商定制合同条款以保护自己免受法律争端[47]。 中小企业要求在合同中使用 PBA 的障碍是来自总承包商潜在报复的恐惧，这可能包括被排除在未来工作之外[48]。 在拉夫堡大学博士研究人员 Rachel Griffiths 和 Wayne Lord 针对 PBA 采用的主题进行的问卷调查中，共有 58 名建筑供应链参与者，其中 42％的受访者投票表示*报复性的恐惧*是阻止 PBA 采用的主要因素，其次是 34％的*法律费用*和 25％的*行业文化*[49]。 此外，标准合同形式包括各种认证、估值和合规性检查，需要修改以适应 PBA 的实施； 然而，受访者建议这些属于非技术性障碍[49]。 此外，英国政府部门内阁办公室断言 PBA 不会干扰合同估值和认证[50]。

移除总承包商进行现金奶牛项目的风险有助于促进负责任的工作实践[50]。 在诸如 NEC、JCT 和 FIDIC 等现有合同中采用 PBA 的进展稳步增加； 但是，由于建筑项目的多样化和定制化性质，PBA 在所有建筑环境合同中的强制执行具有挑战性[51]。 加拿大出现了 PBA 的类似变体，称为安大略省建筑留置权法，其中讨论了使用多项目银行账户[52]。 该方式在多个项目间执行付款使用分区银行账户[53]。 该方式的付款期限为从客户到承包商的 28 天，从承包商到分包商的 7 天； 但是，它允许*按时支付*条款，因此容易因通过供应链级联支付而导致延迟[54]。 此外，关于任命可以监督跨多个项目的私人/敏感数据的账户经理，它存在着责任和信任问题。

区块链具有与 PBA 整合的潜力，通过将支付直接链接到已签署的批准，通过自动释放支付到供应链的智能合同[55]。其优势包括减少由行政处理引起的延迟，增加交易可追溯性[56]。支付可以通过预编程功能自动化，控制交易执行；此外，这些编码的指令可以通过监管控制进行审计，以确保符合政府强制性立法[57]。区块链的固有属性，如不可变性和数据可信度，使其成为价值转移的合适介质，在争议解决情况下提供可靠的数据跟踪[58]。存储在区块链上的数据可以通过集成区块链与遗留系统的应用程序编程接口（API）传输到企业系统中[59]。例如，通常在各种 IT 系统中管理的服务，如资产所有权证书、会计数据和已签署合同协议，可以通过基于区块链的系统进行集成[60]。

### 2.3 密码学和加密

区块链融合了不对称加密（同义词为公钥密码学），其中包括使用公钥和私钥对[61]。这些密钥具有两个主要功能，即加密和签名[62]。公钥是用于接收资金的数字地址（类似于写在个人银行卡上的账号），而私钥则提供了从用户钱包执行交易的权限（类似于个人银行卡上的卡号）[63]。由于不对称加密，公钥可以公开共享，而无需泄露其关联的私钥风险[64]。它于 1976 年发明，并是对称加密的演进[65]。对称加密只使用一个密钥来加密和解密数据，而不对称加密使用两个密钥，一个公钥和一个私钥对[66]*.*

此外，不对称密钥也用于在点对点网络中发送数据时提供加密，这使用户能够提供已签署证据，证明特定数据未被篡改或更改[67]。不对称加密也在互联网安全中起着根本作用，使计算机能够在网上进行隐私数据交换，如互联网银行，电子商务，电子邮件和任何其他在线数据交换系统[68]。

### 2.4 离链消息

非对称密钥并非区块链的产物，尽管在其功能中起着至关重要的作用[69]。 非对称密钥是通过椭圆曲线数字签名算法（ECDSA）生成的，在大多数编程语言中都可以使用[70]。 由于这一点，公私钥对可以在断开互联网的情况下创建，以增加安全性[71]。

区块链交易也可以通过线下（区块链之外）实例化，通过存储一条签名消息来陈述在将来某个时间点发送交易的意图，这可以作为支付应用程序的一部分纳入以自动化交付工作的支付[123]。 区块链广泛使用的一个线下应用示例是去中心化交易所（DEX），它允许用户在对等的方式下交易而无需中心化交易所。 DEX 等去中心化应用程序可以防范黑客攻击，提供更低的交易费用，并允许用户进行点对点的交易[122]。 DEX 具有一个独特的特性，即在进行交易时不需要交易方的公钥，因此交换是匿名进行的[124]。 DEX 的线下功能已被适配并实施到 PBA 区块链模型中。

### 2.5 智能合约

目前，由于审计、开发和链上部署费用，智能合约的建立成本较高[72]。 外包一个智能合约的预估成本可根据其商业逻辑的复杂性在每个合约范围内从 7000 美元到 100,000 美元不等[73]。 然而，外包智能合约只是问题的一部分，还必须进行审计，每个审计费用可在 4000 美元到 100,000 美元之间[74]。 要完全自动化施工项目中的付款，所需的智能合约数量实际上可能达到数千个，这是由于典型项目中涉及的参与者和活动的数量。 此外，向智能合约加入更多技术特性同时会增加其成本，因此对于智能合约随着复杂性的增加而递减的程度也是存在的[75]。

PBA 区块链模型的技术功能源自去中心化应用程序（dApp），具有链下功能。区块链交易是一条已签名消息，说明了从一人向另一人发送加密货币的意图[76]。然而，这种意图可以存储在链下，并且是所提出的 dApp 的基础。允许消息发布到区块链的规则将由预先编程到链下数据库中的条件所控制。这些条件将对所有用户公开审计，以便他们在进入基于区块链的协议之前验证其条款和条件。与链上相对，链下的一个缺点是更高的集中率[77]。为了增加安全性，PBA dApp 需要由多个节点托管，以撤销任何一方对 dApp 拥有控制权的可能性。最实际的参与者选择将是直接参与项目的人，如客户和供应链。dApp 的外部参与者可能包括银行、政府机构和标准组织。

## 3. 方法论

研究课题是通过调查建筑行业长期存在的有害支付惯例而选择的，这些惯例是由上层承包商强制执行的延迟支付和不公平的合同条件造成的。从 1998 年到 2008 年，英国建筑行业个体破产率的平均值年均达到 2145 例，占英国破产人口的 14%，这是所有其他行业中最高的[28]。此外，根据国家统计局 2018 年至 2020 年的更近期的数据，每年平均有 2595 起记录的案例，占英国破产人口的 18%[29]。本文提供了一个概念模型，讨论了区块链如何可能作为支付系统的一部分被纳入以自动化 PBA 交易。

所提出的 PBA 区块链模型是通过从现有文献中汇编的想法形成的[78]。其中包括审查政府支付战略和现有的区块链应用程序。其中，选定了英国政府有关项目银行账户（PBA）的指导文件，作为一个可以受益于区块链加入的可行战略[79]。PBA 区块链应用程序的构思来源于一种去中心化的链下支付应用程序，允许用户预定交易条件而无需使用智能合约[80]。

## 4. 概念模型

概念模型使用三个流程图来解释基于区块链的离线应用程序的功能。 图 1 解释了消息签名的核心功能，图 2 提供了 PBA 区块链应用程序如何处理交易的整体视图，图 3 讨论了项目参与者如何通过提议的系统建立合同协议。![](img/504856_1_En_8_Fig1_HTML.png)

图 1

链下消息签名

![](img/504856_1_En_8_Fig2_HTML.png)

图 2

PBA 区块链模型流程

![](img/504856_1_En_8_Fig3_HTML.png)

图 3

支付保证流程

### 4.1 消息签名

区块链交易是提供加密证据的已签名消息，证明付款人希望从其钱包发送加密货币给接收方。但是，这些消息可以在链下实例化和管理，这就是提议应用程序的目的。其目的是使用包括执行项目支付给供应链参与者的指示的已签名消息在内。每条消息都将使用账户持有人的私钥进行签名，这提供了将消息上传到区块链时转换为交易的授权 [81]。此外，已签名消息可以与期票一起使用，提供了客户打算进行公平支付的证据。消息签名过程显示在图 1 中，并用数字标注来讨论消息签名功能的顺序步骤。

1.  1.

    **私钥**：这主要用于授权可以在链下通过密码签名实现的区块链交易。私钥还可以用于加密/解密数据。例如，可以使用用户的公钥对文件进行加密，从而只允许相应的私钥解密数据。

1.  2.

    **已签名的消息**：这只能使用账户持有人的私钥进行。每条消息都会经过签名以确保其真实性，并提供证据表明其未被篡改。用于签署这些消息的算法是椭圆曲线数字签名算法（ECDSA），它在大多数编程语言中都得到支持，并允许签名过程在断开与互联网的连接或链下进行 [82]。区块链交易还包括在其数据输入字段中存储短字符串文本的能力，这可以用于存储以数据哈希形式存储的参考代码或存储库链接 [83]。

1.  3.

    **链下数据库**：这是用于存储已签名消息的存储库。链下数据库可以托管自己的 IF/THEN 语句，用于控制消息向区块链的发布[84]。前端应用程序将允许用户使用他们的区块链钱包地址执行消息签名过程，而无需任何编码知识。针对公共区块链存在一种公钥恢复算法（PKR），允许用户匿名签署链下消息而不显示其公钥，从而增加链下应用程序的安全性[85]。以太坊等公共区块链包括 PKR 内置到其协议中，因此当消息上传到链上时，发送者的公钥会自动生成，交易可执行[86]。由于 PKR，链下应用程序中参与付款的数字密钥不需要披露，从而降低数据隐私风险。

1.  4.

    **区块链**：用于处理从链下数据库接收的已签名消息。一旦消息从链下数据库推送到区块链，只要发送者在钱包中有足够的资金，交易就会执行。区块链钱包不能透支。因此，需要基于区块链的付款担保来覆盖任何遗漏的责任。关于这一点将在后面的部分讨论。

### 4.2 项目银行账户（PBA）区块链模型

图 2 流程图被数字标注，显示了构想的 PBA 区块链模型的顺序步骤。它讨论了每个参与者的责任和流程。PBA 区块链应用程序将利用各种界面，相互操作以控制消息从链下数据库流向区块链。链下用于数据存储、管理和计算处理，而区块链用于支付执行和哈希索引。

1.  1.

    **客户**：这个用户负责通过 PBA 应用程序批准项目预算。批准是通过陈述意图向供应链付款的已签名消息进行的，前提是工程验证完成。指定的项目验证者，如总承包商和顾问，将被授权控制已签名消息从链下数据库发布到区块链上。

1.  2.

    **项目银行账户（PBA）支付应用程序**：这是允许用户实例化已签名消息、输入项目数据、验证工作并提供完成证书的前端接口。PBA 区块链模型的主要参与者包括客户、银行、总承包商、顾问和分包商。

1.  3.

    **离链数据库**：用于表示分区的 PBA 账户。离链应用包括在其管理委员会（如客户、承包商和银行）可以选择适合项目的可扩展性（以每秒交易次数衡量）和隐私等级的更大模块化[87]。

1.  4.

    **区块链**：这将自主地并定期地接收来自离链数据库的签名消息，以执行交易。区块链交易的数据输入字段可用于存储在离链环境中实例化的验证签名，例如对工作完成签名的哈希值[83]。这些数据可以通过集成应用程序编程接口与企业系统进行互操作，通过用户仪表板过滤并中继相关的区块链数据[88]。

    步骤五到七包括在客户无法在项目里程碑上支付负债时，获得项目融资的流程。该流程是通过一个金融机构（如银行）自动化执行的，该机构签署一条声明其意图覆盖未支付负债的消息。该消息存储在离链数据库中，并在触发非支付事件时自主执行。

1.  5.

    **代币化抵押物**：这可能在客户未付款的情况下提供流动性，通过金融机构提供的基于区块链的代币化证券服务[89]。在这种情况下，银行等金融机构可能以客户的代币化抵押物交换提供项目融资。尽管这是区块链的新兴方面，但自 2019 年以来，包括汇丰银行、摩根大通、中国银行、中国建设银行和桑坦德银行在内的主要银行已经将数十亿美元价值的资产迁移至区块链证券[90]。另外，去中心化金融（DeFi）是 2020 年出现的另一种新兴基于区块链的服务，通过去中心化网络引入了抵押担保的点对点借贷[91]。然而，在当前环境中，DeFi 还没有发展到足以将其服务扩展到企业对企业或个人对企业借贷，因为企业的 DeFi 更加繁琐的合规要求，而监管是区块链面临的最大挑战之一。

1.  6.

    **基于资产的贷款**：这是银行提供的一种现有的金融服务，用于在承包商未交付的情况下向客户提供补偿，同样，承包商也获得了支付担保以保险和避免客户不支付[92]*.* 这两种补偿事件通常在建筑合同中实施以对冲风险，但是这一过程也会由于银行为其服务收取高额费用而增加项目预算[93]*.* 证券交易所集团、IBM 和 Borsa Italiana 合作开发了基于区块链的资产交易平台，允许企业将证券代币化，而无需使用银行的服务[94]。这些代币包括与去中心化金融结合使用的潜力。

1.  7.

    **付款担保**：这是目前一个在行政上耗时的任务，因为需要银行重新熟悉签署在之前许多个月前的付款担保支出请求之前的协议，导致不必要的数据再处理和延迟[92]。可以通过银行存储签署的区块链消息来减轻这种情况，这些消息表明根据客户欠款的责任金额执行补偿的意图。这些消息将存储在 PBA 离链数据库中，并根据非支付事件的触发自主释放。

1.  8.

    **总承包商**：该方放弃了作为项目预算的唯一所有者的责任；然而，他们在通过 PBA 区块链应用程序验证分包商工作方面发挥着至关重要的作用。总承包商负责验证工程完成的百分比，而顾问负责确保工程按约定标准交付。验证是通过 PBA 前端应用程序进行的签名区块链消息完成的。成功的验证允许消息从离链数据库流向区块链。总承包商的角色还包括通过 PBA 前端上传项目成本和进度数据，以便由客户签名批准。客户将通过签名的区块链消息批准这些消息，指示从其钱包向供应链转移资金。

1.  9.

    **分包商**：这些方在建筑行业长期承受不利的支付条件，已经延续了多代。来自英国领先的零售支付管理机构的统计数据显示，78%的中小型企业被迫等待超过约定支付期限 30 天或更长时间[95]。一旦分包商通过 PBA 应用程序注册工程完成情况，这将自动通知验证方，告知他们批准工程工作的责任。一旦获得批准，根据项目的里程碑计划，将执行自动支付。来自非链上数据库的支付释放将受到预定义的 IF/THEN 语句的控制，该语句已经编入应用程序。为了防止验证方的疏忽，可以将自动奖励/处罚系统嵌入到 PBA 区块链应用程序中。

## 5 支付保证

图 3 显示了支付保证文件、存储和执行的高级流程图。

1.  1.

    **总包商**：这方可以通过联合融资方式从多家银行获得支付保证，从而减轻短期波动，如高额支付[96]。联合融资是一项通常由支付保证接收方提出的服务，然而银行也可以提供。2018 年，区块链交付的第一笔联合贷款价值 1.5 亿美元，其中包括三家银行的合资企业，它们是西班牙国家银行（BBVA）、三菱日联金融集团（MUFG）和法国国民银行（BNP）[97]。

1.  2.

    **银行**：这方目前是建筑项目中支付保证的供应方[98]。他们参与 PBA 区块链模型至关重要，需要有动力将他们的服务与之整合。然而，这涉及的架构超出了本文的调查范围。完全有可能另写一篇文章，探讨银行是否愿意向建筑项目提供基于区块链的金融服务。

1.  3.

    **支付保证合同**：这种保证是在现有的建筑协议中实施的，旨在为投资者、利益相关者和供应链提供财务保障，因为建筑项目长期以来一直以高风险和低回报著称[98]。这种支付保证是银行提供的一项复杂服务，因此对此收取高额费用，这有助于减少项目利润[92]。区块链的自动化和可追溯的特性使其成为可靠传播支付保证的合适技术，而不会产生过多的中介费和处理延迟。

1.  4.

    **对文档进行哈希处理**：这是为任何给定数字文件生成唯一标识符的一种方法[99]。可以使用任何计算机算法生成哈希，因此它是普遍可接受的，并且在数学上是准确的，而不必依赖于信任的第三*方*来生成哈希[100]。像[`​emn178.​github.​io/​online-tools/​sha256_​checksum.​html`](https://emn178.github.io/online-tools/sha256_checksum.html)这样的网站允许用户通过上传文件来测试哈希函数，它会自动生成文件的唯一哈希值。

1.  5.

    **数据存储库**：如果意图是将文件链接到区块链，则这是一个强制要求，因为区块链只能用于存储文本字符串（如哈希）。去中心化的存储提供商（如 IPFS）与区块链集成，为在分散式存储库中存储数据提供了额外的安全层，因为中心化存储存在更大的被黑客攻击的风险，以及受到服务提供商的数据挖掘的控制[101]。在区块链上签署消息的数字密钥也可以用于加密和解密文件，发送方可以使用接收方的公钥对文件进行加密，从而只允许接收方使用其私钥解密文件。这使得文档可以在公共领域中安全存储和交换，而不会有数据隐私泄露的风险。然而，如果需要存储未加密的文件，并同时允许公众验证其真实性，则可通过发送方对文件进行哈希处理，用其私钥对此哈希进行加密，并将加密的哈希与其公钥一起存储在可公开访问的文件夹中，从而允许任何人使用发送方公钥解密文件的哈希，以验证其真实性[102]。这样一来，文档可以公开存储，而所有参与方都可以在不依赖信任的情况下验证其真实性。

1.  6.

    **PBA 支付应用程序**：该应用程序的前端允许银行签署区块链消息，说明担保客户项目支付的意向，该消息稍后在推送到区块链时转化为交易。支付代码等数据可以存储在每个区块链交易的数据输入字段中，从而允许在区块链上引用链下数据[83]。

1.  7.

    **链下数据库**：这里存储了银行签署的准备部署的区块链消息，当触发补偿事件时。由于非对称加密，签署的消息无法被伪造，因为每条消息都是用账户持有者的私钥签署的。

1.  8.

    **分包商**：这一方会通过 PBA 区块链应用注册他们工作的完成情况，同时通知验证者他们有责任批准已完成的工作。如果客户在支付到期日资金不足，那么分包商会从银行接收自动赔偿支付，数额等同于客户欠款。通常支付保证只覆盖客户总预算的一部分。然而，所有供应链各方会在事前签署的合同协议中得知这一点。为了让分包商放心，拟议的 PBA 应用会通过应用程序接口（API）提供银行待付赔偿支付的统计数据，可以通过其真实性。

1.  9.

    **客户**：这一方会通过 PBA 应用自动收到关于偿还贷款担保贷款的通知。贷款偿还的隐私可以通过零知识证明来维护，这是允许在公共区块链上进行私人交易的密码机制[103]。另外，客户还可以通过手动向银行发送等额的区块链交易来偿还贷款。

1.  10.

    **贷款偿还**：这一活动将通过 PBA 区块链应用进行。这允许参考代码通过自动化管理（通过 API）以减少数据输入错误。这些 API 也可以设计成与现有的遗留企业系统集成。

## 6 讨论

1964 年的班韦尔报告，标题为《建筑和土木工程工程合同的订立和管理》，讨论了建筑行业付款文化变革的重要性，并概述了合作合同的重要性，然而，50 年后，同样的问题依然存在[19]。这在 1994 年的拉瑟姆报告[104]和 1998 年的斯休工程任务奥尼甘报告[105]中再次强调。另外，从 1996 年到 2021 年的 25 年间，英国政府出版了六份关于建筑行业可持续支付实践的重要立法文件。尽管如此，从 2008 年到 2013 年，逾期付款期限的持续时间增加了 22％，而用于建筑项目的银行贷款减少了 38％[106]。这使中小企业（SMEs）承受越来越大的压力来承受金融逆境，因为银行越来越不愿提供财务支持和允许不支持的支付条件的建筑合同。例如：不公平地拖延供应链付款（现金农业）和由供应链每个层级造成的不必要的处理延迟。

建筑信息模型（BIM）并没有提供预期的数字化改革，这是由于许多因素超出了本文调查的范围；然而，其中一些包括行业文化抵制变革、技能短缺和技术成本[107]。此外，许多关于 BIM 的期望被夸大了，并基于过早的预测。虽然 BIM 是一个以建筑行业为中心的创新，但区块链在其他行业中包含了重大发展，其中包括适用于建筑行业的解决方案[108]。技术领导者如 Facebook、Amazon、Microsoft、Google 和 Apple（FAMGA）正在为企业和消费者提供基于区块链的服务，以与现有 IT 系统整合[109]。由于区块链是一个多产业创新，它包括了来自更广泛社区的更大贡献和发展，不像 BIM 是一个以建筑行业为中心的创新。

项目银行账户（PBA）与区块链具有几个主要特征，例如透明性、可审计性和去中心化，通过创建一个由项目参与者共同管理的分区银行账户。PBA 区块链模型的构想源自一个去中心化应用。它包括预先编程在区块链应用中的支付条件，以自动执行供应链支付。拟议的 PBA 区块链模型假设银行已经采用了区块链技术，并可以通过代币化抵押品提供支付保证；然而，银行是否愿意为建筑行业提供区块链服务还需要进一步的研究[110]。如果银行不愿意协助提供担保，DeFi 和通过抵押品支持的借贷的资产代币化存在机会[111]。然而，企业 DeFi 的技术方面尚处于概念化和测试阶段，需要监管成熟度。此外，由于技术的新生，目前很难预测区块链相关风险的保险。这不利于本已风险厌恶的建筑行业。DeFi 在 2020 年变成现实，在同一年，发生了一起 2500 万美元的 DeFi 平台黑客攻击事件，由于公共区块链的匿名特性，此事件无法追踪到[112]。通过 DeFi 的抵押贷款目前仅适用于点对点借贷，不适用于基于 DeFi 的点对企业或企业对企业金融[113]。

当客户通过 PBA 应用程序创建的签名的区块链消息批准项目预算时，这可以作为保证供应链财务确定性水平的期票的一部分使用。预计客户的签名消息可以作为正式数字文件的一部分集成，以提供提供良好支付实践意图的法律保证。由于 PBA 应用程序是离链的，它可以更容易地适应特定于合同的变更或可能由 GDPR 强加的新规定。这可以在不必从大型公共区块链网络获得一致意见的情况下实现，因为该应用程序是离链的。与区块链相关的一些主要风险包括编写不正确的代码和黑客攻击。如果项目资金由于黑客攻击而被盗，由于区块链上用户钱包的匿名性质，几乎不可能恢复。

提议的 PBA 区块链模型基于客户未支付的责任自动贷款；然而，客户可能会对此提出异议，因为他们通常不会因逾期付款而受到处罚。为了应对这一点，可以将项目预算的一小部分汇集起来，以支付任何逾期支付费用。如果客户没有产生任何滞纳金，那么他们在交接阶段将收到退款。客户使用 PBA 区块链应用程序的动机包括能够向供应链提供支付保证、支付自动化和良好支付实践的数学证明。

未对开发 PBA 区块链应用程序的成本进行定量调查；但是，与直接在区块链上部署智能合约相比，采用离链应用程序提供了更经济的替代方案。通过将计算处理转移到离链[114]，这些开销被减少了。由于所提议的应用程序是离链的，更容易集成和定制隐私功能；然而，为更大的集中化而交换的增加模块化性，在设计离链应用程序的安全方面和将被任命来管理它的治理团队时，这种权衡至关重要。

提出的 PBA 区块链模型规避了使用智能合约。这减轻了与它们的开发、审计和链上托管费用有关的成本。根据 Block Geeks 的首席执行官 Andrew Zapotochnyi 的说法，该公司是一家智能合约审计和教育公司，审计智能合约的估计成本可以从每个智能合约 4000 美元到 10 万美元不等，这取决于编码的先进程度[74]。而非营利性智能合约技术组织 iOlite 估计，开发智能合约的成本可以从每个智能合约的 7000 美元到 10 万美元不等，这取决于其业务逻辑的复杂性[73]。此外，直接在区块链上部署智能合约会产生需要考虑的托管费用。尽管这些成本的一般性质，即使是最低的范围也不经济可行，因为可能需要数千个智能合约才能完全自动化支付一个建筑项目，这是由于典型项目中涉及的参与者数量和活动的数量。尽管如此，随着区块链和智能合约的成熟，它可能会变得成本指数上更具实惠。在那之前，必须探索其他选择，比如离链。

由于加密货币的波动性，支付需要通过稳定币或央行数字货币（CBDC）进行。CBDC 是国家货币的数字复制品，由政府发行和管理；然而，它目前还处于测试阶段，中国是 2021 年首个进行全面试点的国家[115]。英格兰银行和英国财政部于 2021 年成立了 CBDC 工作组，以进一步探讨其作为法定货币的可行性[116]。稳定币与 CBDC 类似，它们是与国家货币按一比一比例挂钩的加密货币，例如美元或欧元；然而，它们不是由中央银行铸造或控制的[117]。PBA 区块链模型的采用取决于主机国家是否有其国家货币的稳定币或 CBDC。像美元、欧元和英镑等许多主要货币都包括稳定币变种；然而，这些稳定币的流通供应量有限，它们也缺乏政府监管，并且很难让流动性提供者大规模地将其立即转换回国家货币。

英国建筑行业培训委员会（CITB）和建筑技能认证方案（CSCS）进行的一项调查显示，在过去 12 个月内，有 419 名证书核验员中有 18%遇到至少一张伪造证书被用于项目中 [118]。英国标准协会（BSI）已与 OriginTrail 区块链应用合作，在以太坊区块链上存储证书核验信息。这使分包商可以在证书上附加 QR 码，直接链接到区块链，以提供符合标准的证明 [119]。这是一个私人企业应用的典范，在公共区块链平台上托管。大部分区块链的创新来自公共平台，因为它们是无许可的，提供免费协议基础架构和可开发者无论测试还是构建应用都无需付费或向平台请求许可 [120]。

## 7 结论

从 1996 年到 2021 年，英国政府发布了六份重要的立法文件，以解决建筑行业的支付问题。从中，发现了项目银行账户（PBA）策略可以从区块链的整合中受益。尽管区块链还处于初期阶段，但它正在迅速发展，并改变了企业、个人和服务运作的前景。在一份讨论区块链潜在影响的报告中，发现可能会全球转型 58 个行业，其中包括建筑行业 [121]。所提出的 PBA 区块链模型概述了项目参与者如何与区块链应用互动，上传支付活动，验证工程，并自动执行对供应链的责任。PBA 模型还讨论了如何通过代币化抵押品来减轻客户拖欠支付的风险的潜在区块链解决方案，这可以作为与银行进行交换的交换媒介，从而允许银行自动执行以抵押品交换逾期支付。

PBA 和区块链的价值在透明度、可审计性和去中介化等几个关键属性上是一致的。然而，这项研究需要进一步调查，通过开发和编码所提出的 PBA 区块链应用并模拟其流程。此外，与熟悉 PBA 的行业从业者进行采访，他们对所提出的模型中被忽视的领域提出建设性的批评，如在建立 PBA 时所需的正式决策过程，会提供有益的意见。