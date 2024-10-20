# 1

# 区块链对企业独特的功能和优势

我首先调查了区块链的颠覆性可能性，指出尽管它能够带来许多好处，但大型企业对这项技术的采用却很慢。在本章中，我深入探讨了区块链的独特能力及其背后的架构，这些能力塑造了它解决数字交易慢性问题的潜力。像其他在其早期阶段的潜在颠覆性技术一样，区块链更能满足非消费者和发现传统解决方案过于复杂或许负担不起的狭窄客户群体的需求。1 区块链仍在发展之中，我指出了使用它的技术缺点。尽管如此，我们可以看到一个未来，届时它的这些缺点将被解决，并成为企业业务中的常见特征。在第二章中讨论的区块链初创公司，正处于逐步克服这些缺点的前沿。在第七章，当我讨论企业区块链战略和实施时，我探讨了公司如何解决区块链推广的经济和组织障碍。

## 什么使区块链独一无二？

区块链的独特价值源于其独特的设计和架构，这为企业提供了强大的优势和利益。数字交易仍然存在几个持久的问题，使企业面临延迟、欺诈和其他额外成本的风险。区块链为以下持久且成本高昂的挑战提供了解决方案，这些挑战在下面详细讨论：

+   • 身份验证

+   • 在交易中信任交易对手

+   • 可靠交易和来源保证

+   • 由于信息不一致而产生的争议和延迟

+   • 整合交易与支付

+   • 保护数字资产

+   • 过度集中的危险

+   • 组织间协作

### 身份验证

在数字交易中，商家如何确保交易另一方的身份？] 身份可能难以检测，使企业容易受到黑客攻击、欺诈和金融损害。错误的身份确认也可能影响企业遵守了解你的客户（KYC）和反洗钱（AML）规定等监管要求。

区块链解决方案：自主主权身份区块链，利用私钥和公钥以及零知识证明（ZKP），创建了由个人控制的简化、去中心化的身份标识，称为自主主权身份（SSI）。公钥-私钥对对每个人都是唯一的。正如术语所暗示的，个人可以将公钥广泛提供，而私钥只有该个人知道。当两个人——*发送者*和*接收者*——寻求进行交易，例如交换价值或传输数据时，发送者可以使用接收者的公钥加密交易。收件人只能使用自己的私钥解密信息，同时使用发送者的公钥验证信息来自发送者。发送者和接收者都保持他们的私钥安全。

****

SSI 利用零知识证明（ZKP）来验证信息，同时尽可能少地透露细节，这样个人和实体可以验证其身份而不透露更多细节。2 例如，房地产经纪人可能希望潜在买家透露他们的工资单和银行对账单，以证明他们有足够的收入和资金购买所展示的房子。ZKP 可以提供这样的收入证明。在这种情况下，ZKP 将使用两个步骤：1)证明潜在购房者的身份；2)将这个已证明的身份与一个已证明的凭证（即收入和资产）相链接。在这个例子中，*验证者*，即维护个人支票或储蓄账户的银行，可以验证余额和直接存款的工资额是否超过了某个数字对于某个加密身份。*证明者*，希望建立财务充足证明的个人，将公钥发送给*请求者*，即房地产经纪人，后者可以在包含加密身份的公共区块链上验证证明者的身份，而无需了解证明者的任何其他信息。因此，房地产经纪人可以获得潜在买家的购买力的保证，而不需要了解证明者的储蓄账户中的确切金额或实际收入。

美国和全球各地的金融监管机构要求金融机构验证其客户的身份证件——了解你的客户（KYC）——以促进对洗钱和非法行为（如资助恐怖主义和人口贩卖）的监控。不遵守规定可能导致巨额的金融罚款，并威胁到金融机构的持续运营。SSI 促进创建和共享普遍验证的身份。一旦建立，普遍验证的身份消除了重复身份验证的需要，并可用于在各种环境中遵守 KYC 规定。确保的身份可以与该个人或实体的声誉相链接，并促进在已识别和信誉良好的各方之间直接交换价值。3 例如，将数据分析应用于区块链中个人的支付记录，可以基于他们的支付可靠性（与信用评分类似）得出声誉评分。作为证明者的个人可以选择与请求者分享这样的评分，并使用上述概述的零知识证明过程。

### 信任交易中的对手方

如何确保公司能够信任对手方如约支付？在未知对手方的情况下，公司可能更愿意依赖像银行这样的中央中介，来为对手方担保并确保交易完成和支付得到保证。这样的中介可以通过控制从总交易流中积累的数据来增加其市场权力，并通过设定高额费用来进行此类交换，特别是在建立和运营专有平台时。

区块链解决方案：基于共识的交易验证机制区块链协议采用不同的共识算法，使网络节点能够验证一个验证过的交易区块。4 工作量证明（PoW）和权益证明（PoS）是两种常用于验证和包含新区块的方法。PoW 需要网络节点消耗资源，例如解决一个复杂的数学难题，这个难题可以通过试错而不是算法来解决，这需要大量的财务投资于计算能力。解决这个数学难题的第一个节点可以获得验证新区块的奖励。在采用 PoW 的加密货币网络中，例如比特币和以太坊，奖励是以这些加密货币的形式发放的，这个过程就是“挖矿”，例如，创建新的比特币或以太坊（分别用于比特币和以太坊网络的货币）。谜题的复杂性随时间增加，需要额外的计算能力投资。成为第一个解决谜题的节点所需的显著财务资源，是对验证虚假区块的威慑。从这种恶意行为中获得的利益将少于控制网络中大多数节点所需的计算资源投资，这是提供大多数交易和区块验证（矿工知道是虚假的）的必要条件。

PoW 计算过程中的能源浪费，以及支付最终确定的延迟（成功完成计算和验证区块需要时间），催生了诸如 PoS 之类的替代方案。在 PoS 中，潜在的区块验证者必须提交一笔财务押金才能参与（“质押验证者”）并且可能因为不诚实的行为而失去他们的押金。大多数验证者需要就交易的真实性达成共识，然后才能将其包含在区块中。基于共识的去中心化验证防止了不诚实的参与者控制验证过程，或是在对方和网络的最佳利益之上批准对自己有益的交易。每个节点都是独立的，所有节点都在竞争中争取第一个满足获得区块奖励的条件。如果第一个满足设定条件的节点随后验证了一个虚假交易，那么对于其他去中心化的节点来说，验证这个虚假交易将不符合它们的利益。如果没有大多数去中心化的节点验证交易，最初的验证节点将无法获得奖励。

### 可靠交易和来源保证

公司如何确保由交易各方维护的特定交易的活动记录是一致的，并且被所有相关各方接受为真实？如果数字交易记录被未经授权的各方访问并更改，交易最终化将陷入危险。当交易各方努力协调并纠正错误时，交易会被延迟，这可能导致取消和负面的财务后果。交易各方之间不一致的记录也使得追踪交易链回到其起始点变得困难，让双方都不确定问题可能起源于何时何地。例如，在供应链中出现污染食品的情况下，可以明确地确定污染发生的时间。

区块链解决方案：防篡改的强加密在区块链加密中，对要加密的输入应用一个数学函数。因此，在供应链中，输入可能包括描述集装箱内容的数字数据、其当前所有者、其他相关信息（如来源）以及当集装箱从卡车转移到集装箱船时，集装箱的物理位置的变化。这些数字数据被加密，产生的输出被称为“哈希”。哈希可以链接并链到后续交易，并进一步加密。链越长，恶意代理回溯到初始交易的哈希系列越困难。5 试图更改已经包含在区块链中的数据将导致哈希与存储的哈希不匹配。不匹配的哈希会警告网络中的其他成员此类更改尝试；更改后的数据将不会被验证，并最终被拒绝。带有时间戳、按顺序链接的加密哈希数据块为后续块提供了交易历史的审计跟踪，并有助于证明来源，追踪交易链回到其起始点。通过将关于当前账户余额和交易状态的准确、更新、及时的记录分发给每个节点，共识机制阻止了*双重花费*。类似的控制可以保护区块链业务应用中的数据（数字资产）传输和共享。

### 减少因信息不一致而产生的争议和延迟

如何让公司快速地与交易方协调不一致的信息，同时避免重复劳动或执行延迟？当多方记录同一笔交易的记录时，由于错误和对事件的误解，这些重复记录之间可能存在不一致性。在这种情况下，必须在交易继续之前协调这些冲突的记录，这是一个耗时且低效的过程。

区块链解决方案：不可篡改且具有篡改追溯能力的审计链 区块链架构提高了信息的准确性，而基于加密的安全性的不可篡改和篡改可追溯特性增加了对区块链数据作为单一共享真实来源的信心。集体验证确保所有各方拥有相同的验证信息，防止接受错误的交易并消除争议的原因。随着交易各方之间数据不一致性的消失，以及不可篡改的数据块防止后续错误的发生，就不需要花费力气和时间去协调不同地点的不同方持有的同一交易的多个记录。这节省了原本在协调交易各方之间不一致信息时浪费的努力和时间。

### 整合交易与支付

*一家公司是否必须依赖一个可信赖的中介，比如金融机构，来验证资产所有权并确保及时支付，同时承担相关中介费用？* 在电子商务交易中，客户选择他们所需的产品或服务，然后单独提供一个支付方式，比如信用卡或银行之间的资金转账（例如，Venmo）。信用卡公司或银行成为可信的中介。由于其声誉使其受到所有当事方的信任，它充当中立方，保护各方利益。如上所述，此类中介互动涉及中介费用，增加了交易成本并减慢了交易执行速度。例如，通过首次公开募股（IPOs）和债券发行筹集资本可能会产生大约 5-7%的投资银行费用。

区块链解决方案：代币化和智能合约的自动化执行 区块链的一个独特特性是能够生成价值代币以促进价值交换。加密货币，区块链的最初应用，是代币——数字化的货币表示。代币化使得在区块链内实现即时支付结算成为可能，其中代币，如加密货币可以被创建和转让。这消除了建立单独支付渠道的需要，使支付中介变得多余。随着中介费用的消失，成本降低。取消中介也消除了一个额外的故障点和风险，例如敏感数据的丢失。这些代币可以是区块链的本地代币，或者是真实资产的数字表示，由特定的共识算法验证。6

智能合约是预先编程在满足合同条件时自动执行的合约。考虑到自动执行的特点，确保 API 的准确性和外部输入用于验证合同条件已满足至关重要。由于这些数据通常来自区块链之外，因此提供安全和不可篡改的输入和计算至关重要。安全的预言机网络是触发智能合约执行的一种途径，例如 Chainlink 等区块链服务公司提供应用程序以获取准确的外部数据，例如确认货物交付的收据。此类证明随后可以触发智能合约释放资金，从而使价值交换成为可能，在区块链内实现合同的履行和相应的支付。以太坊，继比特币之后的第二大加密货币，从一开始就提供智能合约功能，使其成为金融应用开发者的首选。

### 保护数字资产

企业、其业务伙伴和客户如何控制数字资产，如私人数据，并防止未经明确许可的信息共享、分发或出售？* 数字资产可以被复制和修改，未经版权所有者授权使用，可能导致经济损失。为保护此类数字数据而进行的加密可能会使应用程序不太用户友好，干扰更广泛的传播并减少需求。

区块链解决方案：可编程代币 例如歌曲或电影的数字资产可以被代币化，并包含关于该资产特定权利的信息（如只读或读写访问权限）以及使用、转让和处置资产的条件，利用区块链技术防止更改此类使用条款。7 通过将合同条款附加到数字资产上，代币可以控制第三方如何访问和使用该资产，并可以授权更改该资产的状态，如变更所有权。组织还可以保护其数据免受未授权访问，并为每个请求设置访问此类数据的规定。智能合约 thus 控制数字表示的真实资产的处置，将区块链应用的范围扩展到纯粹的数字领域之外。

[*此处原文存在缺失，无法翻译*]

一个有趣的应用是使用区块链来控制土地登记和转让。8 在许多国家，尤其是新兴市场，土地登记处是最近才出现的，不完整，且受到欺诈和腐败的困扰。Bitfury 与格鲁吉亚共和国国家公共登记局合作，创建了一个基于区块链的土地登记系统，以保护财产所有者的权利并加强数据安全。该公司使用了其 Exonum 授权区块链以及数字物业登记流程，用时间戳加密物业标题并发布结果散列。这使得可以验证合法所有权并进行实时审计，以及回溯性地追踪产权变更。9

### 避免过度集中

*一个使用平台的公司如何避免平台所有者/运营商的主导地位及其对平台访问、费用和运营规则的控制？* 集中化允许一个或几个节点在网络访问、费用、客户信息访问、隐私保护程度和其他敏感领域行使控制权。它还可能审查交易流程。例如，如我们在介绍中看到的，苹果和谷歌在智能手机上对视频游戏的分发和访问行使 significant 控制权，允许他们收取 30% 的佣金。Epic 已提起诉讼，要求停止苹果和谷歌使用其各自的 iOS App Store 和 Android 垄断地位对《堡垒之夜》销售收取 Epic 认为过高的 30% 佣金。作为一个垄断企业的集中控制实体，可能会收取更高的价格并防止出现可竞争市场（就像 Facebook 收购 WhatsApp 和 Instagram 来减少对其主导地位的挑战）。集中化还创建了一个潜在的集中故障点。对一个中心中介的成功攻击可能导致私人信息泄露和资产丢失或被盗。

区块链解决方案：分布式 P2P 节点之间的直接通信，以实现更大的透明度。在 Epic 的案例中，每个个别游戏玩家作为去中心化的 P2P 节点，能够通过 Dapp 访问可玩的游戏，Dapp 能够验证玩家身份，并根据他们的会员等级提供不同层次的游戏访问权限。与传统的流游戏平台如 Twitch 或 Steam 类似，Epic 游戏区块链可以免费提供其部分或全部游戏。它可以通过设置基于游戏玩家特征的条件来管理游戏访问，例如，未成年人的年龄和每次游戏允许的最大时间。特别对于家长来说，游戏中未经控制的青少年购买行为是一个问题，使用家长的信用卡进行购买，而访问和预算控制可以缓解这种担忧。它可以通过玩家的身份来确定进行游戏内购买的权限，并为每个游戏玩家设定预算上限（例如，由未成年人的家长确定）。像*Axie Infinity*这样的区块链游戏平台促进了游戏内生物——“Axies”——的创建和销售，因为每个 Axie 都是一个 NFT，它们可以被买卖——而且无需涉及中介平台。10 更广泛地说，去中心化的节点可以协作共同创造客户解决方案，通过建立起源来追踪各自的贡献价值。需要注意的是，这种去中心化确实通过在多个位置存储相同的数据来创建冗余，也增加了成本。

### 实现跨组织协作

如何说服其他独立公司共同协作创造跨组织的解决方案？*随着客户解决方案的复杂性不断增长，要求整合不同的技术。尽管跨组织协作能提高这些整合的成功概率，但这种协作可能充满了关于保护知识产权、认可贡献、公平分配奖励和共享治理的争议。*

区块链解决方案：分布式独立节点之间的共享治理和规则设定区块链的独立网络节点超越了合作公司的边界，有机地创建了跨组织的合作框架——一个生态系统。控制区块链的实体可以创建代币，用于奖励个人对共同创造解决方案的贡献，并激励对网络的忠诚。它们还可以用来激发期望的行为，如提高客户利益的行为。因此，在供应链中，减少清关时间的海关机构可以获得与时间减少相对应的代币。随着网络成员通过增加参与网络活动积累代币，他们在区块链网络治理中的角色可以相应增加，直接与他们的代币持有量成比例。11 总的来说，区块链的技术架构培养了保护个人节点隐私的同时鼓励组织层面协作的生态系统，来源和审计跟踪界定了个人节点的贡献，并促进了与价值创造相匹配的代币奖励。

总之，区块链独特的架构通过前所未有的安全性能，使实体间能够交换有价值的数据和资产，有助于解决困扰数字交易的常见问题。表 1.1 概述了区块链独特架构、潜在企业利益以及在此背景下强大的实用性之间的联系。

区块链架构特性 | 创建 SSI 的能力 | 不可篡改的数据和去中心化交易验证 | 防篡改和可追溯的安全性 | 事件和交易可以被排序和链接 | 基于代币的价值交换；可编程数字资产；真实资产的安全数字化 | 所有节点同时可用最新的交易信息；节点贡献的可追溯性；共享治理；跨境覆盖 |

区块链架构、优势、企业利益及问题解决

| 私有和公钥；零知识证明 | 共识算法：工作量证明、权益证明等 | 强大的加密算法 | 不可变性；时间戳数据条目 | 代币化；本地代币；基于博弈论的激励；智能合约 | 去中心化的点对点独立节点 |
| --- | --- | --- | --- | --- | --- |
| 表 1.1 |
| 企业优势 | 身份验证的便捷性；消除了身份请求的重复；保护非法访问 | 增强与交易对手的信任；从去中介化中获益——消除中介的控制和费用；防止违法行为，减少欺诈 | 防止篡改和修改交易；保护企业不受黑客攻击；提高网络安全 | 创建单一的真实信息源；审计跟踪和确立来源的便利性；减少因信息不一致而引起的争议和延迟 | 无需单独的支付渠道；控制共享私人数据；交易可以与合同关联；基于合同条件履行自动执行合同，由外部数据提供者证明 | 避免过度集中；更大的透明度；消除不一致的对手方交易记录；价值交换、支付结算和最终性； |
|  |  |  |  |  | 使用代币作为激励以促使期望的行为 | 克服实现跨组织共创和协作的困难；公平地归功于网络成员的贡献并分配奖励 |
| 问题解决 | 在数字交易中，商家如何确保交易另一方的身份？ | 企业如何确信客户的账户余额能覆盖交易金额，并且支付能如约发生？ | 企业如何确保特定交易的活跃记录是一致的，并且被所有相关方接受为真实？ | 企业如何在没有重复工作或执行延迟的情况下与对手方对信息进行协调？ | 企业是否必须依赖像银行这样的可信中介来验证资产所有权并确保及时支付？企业、其业务伙伴和客户如何控制私人信息，防止未经明确许可的分享、分发或出售？ | 使用平台的企业如何避免平台所有者的主导控制，掌握平台访问、费用和运营规则的权力？企业如何说服其他独立企业共同创建跨组织解决方案？ |

## 企业如何使用区块链

企业可以以多种方式使用区块链。企业内部的区块链试点和项目可以分为纯粹的组织内部应用以及组织间应用。组织间应用需要与其他独立实体合作和共同行动，而组织内部应用则更容易开发和使用，为企业的子公司和部门提供准确和广泛可用的数据，促进效率提升。这些易于实施的应用，其使用可以在整个组织中强制执行，可以为更复杂的组织间应用奠定基础。企业可以了解区块链能力，制定评估指标来评估成本效益结果，并衡量开发和实施此类应用所需的财务和人力资源。在这个过程中，企业也将意识到区块链应用的复杂性，从学习适当的区块链协议到获取所需技能的教育和培训。

****

具有提供比现有替代方案更优越的协作开发客户解决方案等目标的组织间区块链应用可以增强公司和其合作伙伴的竞争优势，尽管它们设计和实施起来更为复杂。然而，无论强调哪种类型的应用，项目都必须得到业务案例的支持，以吸引资源承诺、组织冠军和组织一致性。我现在回顾各种组织内部和组织间区块链应用。

### 组织内部区块链应用：提高效率

全球各地的证券交易所都使用交易清算和结算系统来记录购买和销售、所有权变更以及支付批准。CHESS 是澳大利亚证券交易所（ASX）二十六年的证券交易清算和结算系统，也为超过 2,200 家发行人维护股东登记册。早在 2015 年，ASX 就开始考虑使用区块链作为改进其 CHESS 系统的基础。

2015 年，ASX 开始设计其 CHESS 替代项目，该项目替换了传统的 CHESS 系统，提升了性能、安全和弹性，并提供了审计跟踪和分析能力。12 ASX 的 David Campbell，首席技术官，指出，一次股份出售转移所有权可能涉及链条中多达十五个人，因此需要从中央数据库转向分布式、共享、实时的单一真相来源。

在 CHESS 替换项目中，所有交易各方都会有一个由法律审批人通过加密技术签名的同步共享复制账本。13 所有各方都会有一个账本的完整副本，更新并打上时间戳以反映交易的成立。然后，随着进一步事件的发生，稍后时间内的这些更新后的账本副本，经过适当的时间戳标记，将在所有节点上复制。因此，每个节点都将拥有账本的最新副本，并不断更新以反映新的交易。ASX 的 DLT 启用的清算和结算系统为所有参与方提供了一个不可篡改的实时交易和所有权变更记录，协调一致的数据标准消除了双方之间数据对账的需要。智能合同将自动化公司行动的更新（即，股息声明和支付，资本提升），独立的第三方可以通过连接到 CHESS DLT 的 API 提供额外的微服务（例如，股东分析和投票应用程序）。ASX 希望鼓励第三方连接到 DLT 将降低进入门槛，鼓励竞争，并提供一系列改进的成本效益高和创新产品。

新产品 CHESS 的设计是在与客户和监管机构协商的基础上分几个阶段演变而成的，全面推出计划于 2023 年 4 月的一个周末进行。然而，ASX 的客户必须选择加入以使用新的分布式账本技术（DLT）系统；那些选择不使用新系统的客户可以使用更新后的 ISO 20022 标准，通过基于消息的连接与系统互动。ASX 在采用分布式账本技术（DLT）方面采取了审慎的方法，经过数年的开发、测试和实施新的 CHESS DLT 系统。它还与外部合作伙伴合作开发该系统，并在大规模推出之前获得独立审计，以确保新系统的就绪。

### 内部组织区块链应用：新的业务和服务

企业可以利用区块链的 capabilities 来开发新的内部组织应用程序，允许组织的子公司和部门安全、一致地共享信息，并追踪这些信息流，从而提高效率、加强合规性并降低成本。

BNP Paribas Securities Services 和公司事件通讯部门。公司事件，无论是收购另一家公司、宣布分红，还是宣布一名关键高管的离职，所有这些都对公司未来有影响。对于上市公司而言，这些事件可能会影响股价。证券交易委员会（SEC）和其他投资监管机构还要求公司事件必须公平地通知所有相关方，企业显然意识到保护声誉和避免因提前获得公司事件新闻而受到内部交易指控的需要。

正文省略。

BNP Paribas Securities Services 的 Philippe Ruault 指出，在 34 个国家运营的管理和传播公司事件信息准确及时长期以来一直是保管行业的痛点。BNP 与塔塔咨询服务（TCS）及其 Quartz 区块链协议合作，确保公司事件分发的安全，旨在避免在过去中介沟通链中发生的失误和重复。TCS 将确保同时向全球所有各方提供安全的唯一信息，最初以七种语言翻译和传达信息。14 此类由区块链指导的公司事件通讯的价值在于，它清楚地表明了同时向所有用户提供市场关键信息，使公司能够为自己辩护，对抗任何支持内部交易的指控。监管机构还可以追踪这些关键信息的流动，并确保公司遵守基本的 公司事件分发规定。

### 组织间应用：提高效率

区块链的颠覆性能力自然使其能够通过与现有系统联合运营甚至取代现有系统来提高效率。我回顾了两个这样的努力：改善跨境汇款服务，以及在社会企业中，为来自贫困背景的学童提供午餐。

Ripple XRP 和跨境汇款。跨境汇款是一个缓慢的过程，手续费高昂，汇款完成细节在几天内都不可用。这样的汇款因为要通过发送者和接收者之间的多家银行而变得缓慢。Ripple 引入了一种基于区块链的解决方案，推出了自己的加密货币 XRP，以及专有的全球网络 RippleNet，提供了一种快速、低成本、安全的替代方案。Ripple 有可能颠覆全球汇款市场，成为现有全球银行的强大竞争对手。随着更多公司采用 Ripple 的解决方案，它作为大型银行传统汇款服务替代品的可行性越来越高。2021 年 10 月，XRP 的月汇款量约为 930 亿美元，结算速度为 4 秒。15 我将在第五章中详细讨论 Ripple 的区块链模型，以及全球供应链的背景。

社会企业与 Akshaya Patra。Akshaya Patra（AP）是印度的一个慈善组织，启动了一个午餐计划，为分布在印度十二个州 19,000 所学校中的 180 多万名儿童提供热腾腾的烹饪营养餐。来自贫困家庭的儿童经常饿着肚子来上学，这损害了他们集中精力的能力，从而影响课堂表现，导致退学。为了实现其目标，AP 运营了 50 多个厨房——一些是集中式厨房，为周边学校提供超过 10 万份餐食；16 在更偏远的地区，它运营的是由当地妇女互助小组管理的分布式厨房。

* * *

AP 必须协调食品和用品的采购，监控食品准备的质量卫生，管理食品配送以防止食品浪费，并从学校获取关于表现和成果的反馈。在 Accenture 的帮助下，AP 引入了区块链来管理其午餐配送计划。其目标是提高效率，促进可持续性，增强透明度，最终实现可扩展性。像其他非政府组织一样，AP 依赖捐赠者的支持，政府补助和私人捐赠都受到明确显示成果的影响。区块链创造了人们对这些成果的信任，提供了前所未有的透明度。AP 在利用区块链进行社会公益方面并不独特。在土地权利、金融包容、农业和教育等领域，组织也开发了创新的区块链解决方案。18

有几种类似的跨组织边界应用，涉及与独立实体的合作，并在整个生态系统中使用区块链。我在随后的章节中讨论了这些应用，例如在第三章中，国家政府试点区块链项目发行国家数字货币（CBDCs），在第五章和第六章中，全球供应链解决方案 TradeLens。

### 组织间区块链与新兴业务和服务

除了发展改进的传统解决方案和新的内部应用之外，区块链还能帮助企业创建新的商业模式和新的收入来源。它擅长于促进多个独立组织之间的协作，这些组织可以共同工作，共同创建解决方案，并因其对整体解决方案的个别贡献而得到认可和奖励。这些举措最终会导致开发新的商业模式、获得新的收入流，在某些情况下，甚至会产生全新的行业。

碳信用与代币化随着世界各企业的尝试减轻二氧化碳排放的有害气候影响，本质上是一种奖励企业和个人改变行为的经济激励——碳信用，已经变得越来越普遍。这些激励推动气候友好型倡议，鼓励转向碳中和和碳高效的过程和活动。碳信用使用一种“封顶与交易”的理念，向那些碳排放低于监管机构设定的目标的公司发放碳信用。这些碳信用可以出售给排放超过监管目标的公司，允许它们使用这些信用来抵消额外的排放。碳信用的价格将由污染公司的需求决定，相对于绿色公司的供应。因此，最初，当污染严重时，需求可能会超过供应，推高碳信用价格。进而，随着更高效的公司将其碳信用出售给效率更低的公司，后者的碳信用购买资金中的一部分将用于排放减少的投资，从而逐渐减少全球温室气体排放。此外，随着监管机构逐渐收紧排放目标，碳信用的价格将上涨，增加污染者的成本，进一步刺激和奖励气候友好型行为。

然而，认证排放和创建与管理碳信用交易市场的过程既昂贵又晦涩。它增加了企业、监管机构和消费者之间的障碍。环境、社会和治理（ESG）投资者更愿意投资于积极改善其环境足迹的公司，但可能会发现明确识别这类公司较为困难。针对这些市场问题，IBM 与 Veridium Labs（位于香港）合作，开发了可以在 Stellar 区块链上进行交换和交易的碳信用代币。19IBM 指出，“通过在公共的、受许可的区块链网络上整合整个碳会计和抵消过程，可以更容易地传输和交易所有权权利。”20

Veridium Lab 的解决方案专注于定价和高效利用自然资本（地球有限资源的价值）。该区块链解决方案包括一个代币化市场和一个让公司能够追踪其环境影响的方法，该解决方案和代币使得公司更容易计算出所需的碳信用额以抵消其碳足迹。21 Veridium 解决了碳信用流动性、追踪、标准化、会计和估值等问题。其代币源自一个由认证机构独立验证的碳资产篮子，这些资产来源于公司和非政府组织，包括其姊妹组织 InfiniteEARTH，后者通过在婆罗洲创建 Rimba Raya 生物多样性保护区和发展准确测量避免森林砍伐所减少排放量的方法，获得了 1.3 亿吨碳信用额。

区块链上的室内装饰：DecorMatters 许多购买新家具和设计或重新设计房间的房主常常不确定不同家具在家里看起来或放进去会是什么样子。室内设计师，尤其是行业新入行者，需要推广他们的设计技能，寻找客户，并为他们提供的服务获得公正的报酬——同时还要保护其独特设计不被抄袭。家具零售商需要渠道来吸引和保留消费者，与室内装饰师和设计顾问合作可能是一种双方都能获利的安排。在这种情况下，DecorMatters22 推出了一种商业模式，该模式包括其 MyDecor iPhone 应用作为结合增强现实（AR）、人工智能（AI）和区块链的网站的前端。AR 功能允许设计师和消费者在购买前在他们家中环境和测试设计（例如，ARKit，苹果商店中提供场景捕获和处理、运动追踪和显示选项的 app，以及 AR Rule，用于在 AR 空间内精确测量房间尺寸）。AI 为用户提供应用内建议，并允许设计师和零售商利用用户在装饰游戏中透露的偏好，从中汲取用户偏好的信息。

区块链允许室内设计师在保护其知识产权和货币化消费者对其受版权保护的设计使用的同时提供装饰建议和计划。家具零售商可以通过应用程序向消费者提供他们的家具系列，而那些推荐推动消费者选择特定系列的设计师可以从零售商的此类销售中获得佣金。然后，零售商可以与设计师和消费者建立更长期的联系，创造忠诚度和重复购买，增加长期消费者价值。例如，DecorMatters 要求用户使用红色并提交各种房间的大胆设计，包括“入口处、生活区、卧室、餐厅，甚至还有露台。” 用户（2021 年 5 月超过四百万）可以通过对设计投票获得奖励，这使他们能够货币化他们的参与并鼓励进一步使用 DecorMatters。这有助于设计师个性化并推广他们的推荐，并帮助零售商规划未来的产品开发。DecorMatters 强调了当区块链与附加技术（在此例中为 AI 和 AR）结合时，其潜力如何增强。DecorMatters 模型可以推广用于类似背景，支持客户体验和客户关系管理。23

Coinbase 是一家中心化的交易交易所，区块链应用导致代币和协议特定的原生数字货币数量不断增加，最知名和使用最广泛的是比特币和以太坊。这类货币和代币的交易交易所对于提供流动性以及相对无摩擦的获取和处置这些代币至关重要，从而促进 underlying business 增长。Coinbase 是美国最大的数字货币交易交易所，上市超过一百种数字资产，是能够利用这种核心基础设施需求的一个实体。24

Coinbase 的增长和盈利能力紧密跟随数字资产的增长兴趣和使用，无论是零售客户还是机构客户。它在 2021 年 4 月比特币达到当时的历史最高价 64,800 美元（从 2020 年初的 7,300 美元起）的同一天上市，市值一度超过 1000 亿美元。Coinbase 服务于机构和零售客户。然而，在 2021 年第一季度，其 3350 亿美元的总额交易量中，约三分之二，但只有约 6%的交易收入来自机构，个人零售投资者提供了大部分费用。零售市场份额的竞争将长期降低向零售客户收取的费用，可能会像股票交易一样实现免佣金交易。因此，一个可持续的商业模式将转向提供机构服务以获取更多收入，如保管和支付，并减少对比特币和以太坊的依赖，后者在同一时期占活动量的 70%以上。

加密货币交易也存在更大的监管风险，例如，中国威胁要禁止加密货币，导致价格下跌超过 40%。然而，随着区块链的普及，数字资产相关的基础设施服务需求日益增长，这创造了长期市场和商业机会。像 Coinbase 这样的早期进入者，凭借其规模优势，将更能承受波动，并随着更广泛的市场接受和使用区块链技术，增长收入和盈利能力。

数字卡片和视频流货币化：上帝解禁收藏数字卡片，NBA Top Shot *魔法：聚合物* 是一款实体卡片的集换式卡牌游戏。玩家购买一套初始的三百张独特卡片，然后选择一定数量的这些卡片组成一个用于与对手对战的卡组。规则规定每张卡的能力，目标是耗尽对手的卡组。该游戏于 1993 年推出，立即受欢迎，*魔法* 在 1994 年底售出超过 10 亿张卡。*魔法* 在产品生命周期中为原始卡组添加了扩展包，总共有超过 20,000 张独特卡片，到 2016 年已售出约 200 亿张。像*精灵宝可梦*这样的模仿者很快就出现了。

不足为奇的是，澳大利亚游戏公司 Immutable 推出了一款基于区块链的数字收藏卡游戏。Immutable 在 2019 年推出了其游戏*Gods Unchained*，该游戏使用了基于以太坊 ERC-721 标准的数字卡片。通过使用 NFT，Immutable 开发了数字卡片，使玩家能够拥有并像使用实体卡片一样在游戏中使用它们。Immutable 还允许玩家交易数字卡片，这与实体卡片的交换方式相似，例如原始的*Magic*卡牌套。随着游戏的发布，Immutable 创建了一个基于以太坊的区块链市场，玩家可以在其中购买和交易卡片（在这种情况下是 NFT），使用 MetaMask 等数字钱包中的以太币。数字卡片的购买和交易在区块链上进行，而游戏玩法则是在链下进行。作为将传统实体卡收集和交易转移到数字世界的先驱，且卡片的所有权和真实性不再成问题，Immutable 在两轮风险投资中筹集了超过 1800 万美元。

使用 NFT 在游戏中产生收入的潜力使得游戏开发者向玩家提供了一种购买基于 NFT 的现场音乐直播的选项，这种直播可以在玩多人在线视频游戏时观看和聆听。许多这样的游戏可以通过视频游戏流媒体平台如 Steam 或 Epic 在线免费玩。由于游戏玩是免费的，游戏开发者通过激励玩家在游戏中购买与游戏相关的物品来赚取收入。玩家使用信用卡和移动钱包等标准支付方式支付此类购买。逻辑上的下一步是增加可以在游戏过程中购买的物品范围。流行音乐团体的现场音乐视频直播的数字文件，作为 NFT 进行代币化，是此类购买选项之一。

例如，当 COVID-19 大流行导致 Coachella 等现场音乐节取消时，许多受影响的音乐团体，如 100 Gecs，在拥有超过 1.3 亿月活跃用户的流行视频游戏《我的世界》中提供了现场音乐会。 casual concert fans 可以进入这些在线视频游戏，与朋友见面，以他们选择的虚拟形象在数字 3D 游戏环境中漫步，然后购买进入现场音乐 NFT 直播的权限。一位音乐会观众通过解释说，这种虚拟体验“感觉就像去音乐会的最好部分，而没有最糟糕的部分——流汗，在外面，害怕自己会丢失钥匙”，25 更不用说价格更低，没有交通或停车障碍，以及无阻碍的视野。在未来，可扩展性可能是一个问题，因为在一个游戏平台上提供大量同时进行的视频直播 NFT 可能会受到服务器基础设施可用性的限制。此外，音乐会粉丝和视频游戏玩家并不总是作为观众重叠。

NBA Top Shot 是区块链作为收入来源潜力的另一个例子。在这种情况下，NBA 篮球比赛精彩瞬间被作为 NFT 出售。NBA Top Shot 时刻是来自 NBA 比赛的视频精彩瞬间，由 NBA 正式授权，由 Dapper Labs 在专用的 Flow 区块链上铸造为 NFT，供收藏家购买。没有加密货币经验或知识的初级收藏家可以使用信用卡购买这些 Top Shot NFT。这种传统的支付方式用于建立包含等值加密货币的数字钱包，这些加密货币可用于支付 Top Shot 时刻。到 2021 年 5 月，Top Shot 的总销售额超过 5.6 亿美元，总共有近 50 万名所有者。

Top Shot 的价值来源于诸如版本大小、稀有度、球员受欢迎程度（即勒布朗·詹姆斯与一位崭露头角的菜鸟）、捕捉的赛事类型及其在比赛中的重要性，以及比赛本身的重要性等因素。潜在买家可以申请购买掉落包（常见的掉落包包含一套三个时刻，序列编号并包装在一起，而价格更高的稀有包则包括一个稀有时刻和几个普通时刻）；这些包的需求大于供应，因此被选中购买包的概率较低。球迷购买这些包的希望在未来的某个时刻，这些包能以远高于购买价格的溢价出售。另一种选择是二级市场，买家在此购买单个时刻，希望其进一步增值。有些收藏家、NBA 球迷喜欢拥有比赛片段的真实版本，尽管它很容易在 ESPN 上看到；NFT 证实了片段的原版性和所有权，这赋予了 Top Shot 片段在二手市场的价值和可交易性。在某种意义上，Top Shots 是包含短视频的贸易卡，而不是静态图片。26

随着每个篮球赛季的推移，可用于购买的 Top Shot 时刻数量增加，目前尚不清楚收藏家的需求是否会持续。其他 NFT 可能变得更加受欢迎，NFT 的创建和销售 surrounding infrastructure 是这一领域的关键要素。Dapper Labs 使用的 Flow 区块链专门用于促进 NFT 的创建和市场，它包括一种独特的多角色架构，以促进可扩展性。Flow 故意分离角色并将它们分为共识、验证、执行和收集节点。它使用一种较新且更易于编程的智能合约语言 Cadence，并旨在对消费者友好，使用户能轻松地将法定货币转移到数字货币进行支付。Dapper Labs 与 NBA 合作创建 NBA Top Shot 业务，使其能在 2021 年 4 月以约 75 亿美元的估值筹集风险资本。27 表 1.2 总结了企业区块链应用的可能性范围。

表 1.2

企业中区块链应用领域及示例应用

|  | 组织内部应用示例 | 组织间应用示例 |
| --- | --- | --- |
| 提高效率 | *区块链证券清算和结算平台*：澳大利亚证券交易所的 CHESS 替代项目——替代遗留的 CHESS 系统；提高性能、安全性和弹性；提供审计跟踪和分析能力 | *跨境支付*：Ripple XRP*社会企业*：Akshay Patra |
| 新业务、新服务 | * 传播公司事件（上市公司必须遵守美国证券交易委员会的要求）*：法国巴黎银行和塔塔咨询服务；企业事件连接；促进安全的同时传输公司事件；最小化内部操纵和交易风险 | *碳信用和代币化*：Veridium Labs 室内装饰：DecorMatters 中心化交易所：Coinbase 非同质代币：Gods Unchained, NBA Top Shot |

所有这些例子都表明区块链在企业中具有广泛的应用性。正如表 1.2 所暗示的，已经开发出了各种各样的组织间应用，既包括商业应用，也包括企业对消费者倡议。在这些努力中，几家独立的公司共同合作，每个成员都提出自己的贡献。每个贡献可能相对较小，但这些多个贡献结合在一起可能会带来重大的突破，一个具有相当潜力的颠覆性解决方案。

尽管取得了这些成功，但区块链的采用进展缓慢，这是由于*技术*、*经济*和*组织*的障碍。在第二章中，我回顾了实施区块链的技术障碍，然后讨论了几家区块链初创公司，它们正在解决并尝试克服这些阻碍采用的障碍。我还考虑了开发出独特商业模式的初创公司，以利用区块链获得竞争优势。然而，尽管区块链初创公司在解决技术障碍方面取得了更大的成功，但经济和组织障碍也需要在用户层面，在企业和其生态系统的内部采取行动。我将在第七章更详细地讨论用户在解决经济和组织障碍中的角色。
