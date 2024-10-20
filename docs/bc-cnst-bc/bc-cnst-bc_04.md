© 作者，独家许可给 Springer Nature Singapore Pte Ltd. 2022T. Dounas, D. Lombardi（编辑）Blockchain for ConstructionBlockchain Technologies[`doi.org/10.1007/978-981-19-3759-0_4`](https://doi.org/10.1007/978-981-19-3759-0_4)

# 自动 BIM 验证与智能合同的集成，以确保设计符合性和支付可靠性的设计过程

Giulia Pattini^(1  )，Giuseppe Martino Di Giuda^(2  ) 和 Lavinia Chiara Tagliabue^(3  )(1) 意大利米兰，米兰理工大学建筑、建筑环境和土木工程系(2) 意大利都灵，都灵大学管理系(3) 意大利都灵，都灵大学计算机科学系 Giulia Pattini（通讯作者）邮箱：giulia.pattini@polimi.itGiuseppe Martino Di Giuda 邮箱：giuseppemartino.digiuda@unito.itLavinia Chiara Tagliabue 邮箱：laviniachiara.tagliabue@unito.it

## 摘要

本研究旨在通过结合自动 BIM 验证和智能合同来简化设计阶段的执行。建筑行业通常不愿意接纳新技术，但由于承诺改变信息管理，建筑信息建模（BIM）目前正引领数字化。尽管如此，其采用显示出了信息完整性和可靠性的问题。对信息要求的误解可能导致延迟、意外成本和需要重新工作。基于这些原因，本章建议将基于 BIM 和区块链的信息管理进行整合，并强调其前景。本章阐述了应用自动 BIM 验证和智能合同在设计阶段的研究框架，并指出了它们在自动化信息审查、减少延迟交付和逾期付款方面的潜在影响。还介绍和讨论了潜在技术工具的架构。该研究提出了一个数据驱动的流程，在该流程中，所有与设计验证相关的基本信息都被记录下来，而在每个 BIM 模型的自动验证中，付款批准会自动发布。该系统旨在确保与项目信息要求的全面合规，并保护承包双方免受潜在的延迟支付。该框架目前仍然是理论性的，然而，对其未来通过概念验证的预期结果最终进行了讨论。

关键词信息管理信息验证设计自动化区块链智能合同 BIM 支付可靠性

## 1 引言

由于建筑行业是数字化程度最低的行业之一，因此创新方法和工具被确定为传统方法转型和提高效率的驱动力[1]。因此，数字化转型似乎是改变的第一个冲动[2]，特别是引入建筑信息模型（BIM）通过基于结构化程序和协议的信息管理支持透明项目开发。在结构化数字环境中生产、审核和维护信息促进了参与者之间的全面信息共享和合作（参见第 2.1 节）[3, 4]。BIM 的推广承诺优化数字信息管理，最近观察到建筑行业数字化的增长。其主要实施目标在于改善信息定义和交换。其次，它旨在消除传统的信息不对称，以此阻碍满足要求、透明的信息共享和项目文件间的一致性。尽管期望很高，BIM 的采用出现了与在过程中交换的大量信息相关的问题。特别是这些问题与信息的属性、可靠性、完整性和准确性有关[2]。信息需求和生产信息中的误解或模糊可能导致延迟，需要重新操作，从而产生意想不到的成本[5, 6]。最近，现有文献确定了区块链技术在建筑行业中作为一个激动人心的研究和测试领域[3, 7, 8]。进一步研究还确定了智能合约作为优化和自动化某些活动和支付系统的有价值工具[9, 10]。因此，在可以积极提升数字化行业的技术创新中，所提出的研究提议基于区块链的数字化信息管理，以确保信息的可靠性，并通过智能合约的使用缩短和自动化流程的开发[11, 12]。尽管存在障碍，BIM 目前是最适合的用于信息的协作和结构化生产、验证和管理的解决方案。因此，区块链可以是解决设计、招标、施工和维护阶段中的信息不对称和可靠性问题的可能答案[13, 14]。此外，部署智能合约可以确保特定活动的编程和自动执行。

关于这些前提，通过未来的具体发展，提出的研究框架意在研究使用 BIM 和区块链进行数字信息管理，以突显它们在建筑行业当前数字化流程中的潜力和有用链接。具体来说，研究目标集中在区块链在使用 BIM 进行信息管理中如何确保信息的可信度，以及自动 BIM 验证与智能合约的整合如何缩短执行特定工作阶段所需的时间。实际上，通过自动 BIM 验证和智能合约的整合使用来自动批准设计，可以通过减少等待批准的等待时间和减少重新提交或更改导致的延迟交付，从而优化流程的效率。

提出并开发将自动 BIM 验证和智能合同结合起来，以缩短设计阶段的执行时间，通过自动批准程序，这一研究框架的雄心受到了欧洲和意大利报告的支持[15, 16]。首先，欧洲经济整体面临着拖欠款项和长期付款期限的挑战，引起了行政和财务负担，可能会导致影响企业增长的争端。在整个欧盟范围内，建筑业似乎最受拖欠款项的影响[16]。付款行为的差异破坏了行业的正常运转，并越来越威胁着中小企业的生存[16, 17]。毫无疑问，建筑行业的性质导致了不公平的付款期限和延迟次数上升。特别是，拖欠款项的原因通常直接与建筑公司以及有时是与顾问合作的政府部门的行为有关。面对这种情况，拖欠款项受到了决策者和私营部门协会的日益关注。而对意大利建筑行业的聚焦，一项针对该国情况的分析揭示了公共机构在行业中倾向于拖欠款项的平均付款期限较长，从而影响了顾问和公司的流动性。2017 年，几乎 70%的公司表示公共管理部门拖欠款项[18, 19]。支付延迟伴随着第二个主要问题，即建筑过程中的延迟交付。特别是，意大利的“公共工程实施时间报告”[15]强调了完成流程阶段（设计、采购、建设和维护）所需的时间周期长。具体来说，报告突出了“等待时间”的影响，即一个阶段结束和下一个阶段开始之间的时间间隔在每个阶段的总持续时间中所占的比例。该报告指出，设计阶段的整体持续时间受到验证和验证程序、授权和官僚程序在等待时间期间的影响[15]。

这一分析证实了在设计阶段进行研究实验的宝贵范围。根据迄今为止所述，触发研究框架发展的研究问题是数字方法和工具如何影响设计阶段延迟交付和逾期付款的减少。所提出的研究框架为上述问题提供了理论回应。它阐述了一个流程，如果真正实施，就可以远离传统实践，确保缩短流程开发时间并满足合同各方的需求。研究的进一步发展将通过实施概念验证来体验和展示该框架，证明其有效性和创新性。

本章按以下部分组织。第二部分概述了主要研究领域的现状，即基于 BIM 和区块链技术的信息管理。第三部分通过采用自动 BIM 验证和智能合同，提出了基于 BIM 和区块链的数字信息管理的高层研究框架。第四部分展示了自动验证信息的操作架构和区块链网络的潜在配置。第五部分讨论了所描绘框架带来的主要收益。由于提出的框架仍处在理论水平，所讨论的结果是预期的。最后，在第六部分中披露了研究的主要价值和未来发展方向。

## 基于 BIM 和区块链的数字信息管理研究现状

预计，该研究提出了将自动 BIM 验证和智能合同集成，以自动化和缩短设计阶段的发展。研究建议的框架强调了这些技术所提供的潜力。特别是，基于区块链的 BIM 流程的实施可以通过记录任何活动，持续监测进展，全面验证和确认信息需求以及识别责任方来改善信息管理。这种组合可以给共享、生产、审查和存储的信息带来信心和和谐。该框架相应地可以改善流程的执行和管理。在建筑行业典型的合同环境中，自动化传统上由多方之间的互动实施的某些流程的机会是一个有效的实验领域。为了支持和推动框架的发展，本节讨论了两个主要主题。首先，使用 BIM 进行信息管理，并重点介绍验证和确认信息需求的程序。然后，讨论了建筑领域关于区块链的当前研究领域，并着重介绍了数字信息管理，以及潜在的区块链网络在该框架中的采用。  

### 2.1 基于 BIM 的数字信息管理

信息管理的渐进数字化转型正在推动整个建设过程的革命。在这一背景下，无论是公共还是私人客户，都对利用信息管理改善建筑环境的沟通、效率、安全和生产力的创新实践产生了兴趣。数字化正在促进设计、投标、建设和维护阶段的更多自动化，优化建筑的生命周期，提高客户的满意度和最终用户的体验[20]。在这种情况下，建筑信息模型可以被看作是推动数字转型的方法论。作为一种基于数字信息管理的方法，它对于更好的决策、可预测性和对预期结果的信心可能至关重要。它显著影响着贯穿资产生命周期的数字信息的创建、收集、使用和共享的系统，涉及所有利益相关者。作为定义资产生命周期中数字信息管理程序的国际标准，ISO 19650 系列鼓励引入 BIM，并统一指导专家们如何使用[21]。ISO 19650 将 BIM 定义为一种有益的方法，基于对关于设计、施工、运营和维护的正确数量信息的更好规范和数字交付，使用适当的技术[22]。信息管理过程包括定义信息需求以及信息的生成、交付和审查活动。在这样的过程中，每个参与者都有责任完成特定的信息管理功能。因此，每个参与方根据其角色和责任与信息管理有关。事实上，ISO 19650 确定了过程中的主要参与者，称为指定方、主要委派方和被委派方[22]。第一方通常由客户代表，负责定义信息需求。第二方负责协调交换的信息，第三方负责信息的生产。根据 ISO 19650，为了使用 BIM 实现成功的信息管理，每个参与方都必须完成三项主要任务。第一项任务是明确定义信息需求以及其生成和审查的标准。第二项任务是适量和合格的所需信息的正确生产。第三项任务是各参与方之间信息的高效交换。具体来说，指定方是启动流程的一方，陈述信息需求并确保对其进行明确定义。这份声明定义了信息的类型，并澄清了不同类型信息应如何构造和交换。然后，每个潜在的主要委派方通过编制 BIM 执行计划（BEP）来回应阐明的信息需求，在选择主要委派方时指定方会考虑这一计划。在这个阶段之后，所有参与方合作，以协商关键角色和责任，并制定一个信息交付计划，概述协调和交付方案。这使合适的信息管理得以配置，并考虑了参与方的要求、交付过程和使用适当的技术。在每个项目阶段结束时，需要审查所生成的信息，以验证信息需求的适当达成。这一审查过程通常通过手动和自动化的方法和应用来进行。

前述的信息需求定义基于结构化信息管理，允许明确定义需求，对不同方进行可访问，并持续审查其实现情况 [23]。每个制作的信息都必须经过审查，以确保符合信息需求，因此被接受（或拒绝）。在这一背景下，ISO 19650 系列标准 [22] 规定客户负责定义项目目标和信息需求，并审查资产生命周期各阶段交付的信息。然而，由于 ISO 19650 标准未提供组织或项目特定细节，并考虑到客户高度参与，由通用标准出发，逐渐明显起来需要包含个性化客户需求的 BIM 指南。标准的定制使客户能够以结构化方式创建专有的 BIM 指南，并根据特定需求规范后续程序。定制客户需求组织程序促进了 BIM 在建筑行业中受控和逐渐集成。特别是，为了指导大型客户制定有效的 BIM 指南 [20]，ISO/TS 12911 支持为信息管理定义个性化方法 [24]。的确，ISO/TS 12911 提供了一个结构化和可复用的框架，可以指导 BIM 过程的发展 [24]。建议的框架允许创建 BIM 应用的共同结构，并使 BIM 指南可管理和可测试。BIM 指南的准备和使用用于：(i) 定义期望的信息输出及其预期质量，(ii) 定制项目信息的结构化实施，(iii) 确定资源和工具以及其适当的管理，(iv) 在项目内获取和维护共享知识，(v) 支持 BIM 背后的技术。在设计阶段开始之前，专属 BIM 指南的准备使客户能够以结构化方式制定信息需求，这对确保合同各方明确了所有需生产和管理的信息类型是至关重要的 [25]。由于专有 BIM 指南由特定的客户起草，它们允许根据精确需求标准化和指导流程。因此，现有的专有指南可能在目标、标准化方法、技术要求和所需信息水平等方面存在着很大差异 [26]。但是，它们是推动和指导使用 BIM 进行信息管理的强有力工具。由于建筑行业中的价值生成取决于客户需求的识别、处理和实现，具体指南的存在可以支持过程的发展并保证实现需求。BIM 指南对 BIM 环境中的结构化信息请求、生产、审查和管理进行规范化，促进了不同参与者之间的一致信息，增强了透明和协作的工作流程，并减少了信息不对称或需求误解的发生。

在研究框架的背景下，这些概念是基础性的。研究环境确实位于由特定客户要求的设计阶段（见第三部分）。目标客户拥有专有的 BIM 指南，设计阶段必须按照这些指南进行开发。因此，研究的第一个目标是确定一种能够自动验证和验证 BIM 模型中包含的信息是否符合客户 BIM 指南的应用，并概述其潜在的架构和功能（见第 4.1 节）。

### 2.2 基于区块链的数字信息管理

由于其日益增长的兴趣，区块链技术的引入推动了新类型的应用，因此它可以被认为是当前被世界上最先进的经济体研究的数字转型的主要技术[27, 28]。属于分布式账本技术（DLTs）的区块链被定义为一种*无需信任*的技术，它确保了非常高的可信度、完整性和不可变性[29]，并且允许各方使用点对点网络发送交易，无需受到可信第三方（TTP）的控制[30, 31]。技术的设计保证了信任的建立和维护。使用该技术共享和存储信息的透明度、可访问性和可追溯性水平由其架构设计所定义。在 DLTs 中，区块链提供了独特的功能，包括大量的用例和实施智能合约的可能性。如前所述，智能合约将是本研究的重要研究和应用主题。毫无疑问，根据一些研究人员认为，建筑行业的迟付款导致了多起索赔，但智能合约的采用可以显著减少实际的负面影响[32–34]。选择和配置适当的区块链网络使得制定和执行智能合约成为可能。尽管智能合约是自动和确定性的，但它们并非完全*无需信任*。由于区块链无法自行访问其网络之外的数据，智能合约的主要限制是与现实世界的通信。因此，有必要整合第三方系统，允许访问和验证现实世界中发生的情况，并通过智能合约将信息发送到区块链。这样的服务被定义为预言机[35]。通过这种方式，整个网络可以验证请求，合约能够自动接受或拒绝。当条件符合计划的流程时，智能合约会自动执行，批准释放或直接发放支付[36]。这些服务的使用对于研究框架非常重要，因为它们可以保证外部世界与区块链世界的连接，即设计阶段的信息生产和验证以及流程阶段的自动批准的记录。

由于技术提供的主要优势，如信息的透明性和不可变性，使得可以限制误解的发生，以及过程的自动化，可以确保支付的发放和交付的尊重，所以提出的研究被置于其他与 BIM 和区块链在设计阶段集成的信息管理相关的新兴研究和实验中。的确，利用区块链在 BIM 模型中开发和维护信息的可能性允许记录任何活动，因此可以随时控制所考虑阶段的真正进展和相关责任方。在 BIM 流程中整合区块链为共享、生产、审核和存储的信息提供了信任和同步。信息存储在全体参与者共享的分布式平台上，这使得可以公证每一条信息的创建、修改和更新，随着流程的进行。通过这种方式，过程的进展和项目目标的合规监控为客户和所有涉及指定方所知。在现有文献中，可以辨认出一些与区块链在设计阶段数字信息管理中的采用相关的不同研究。Dounas 等提出了一个用于分散式建筑设计的框架，允许多个参与者以协作和竞争的方式解决设计问题，并且通过区块链的集成，能够记录所有设计尝试，包括那些‘失败’的尝试，以及朝向设计优化的所有积极步骤[12]。Schönhals 等提出了一种方法，使得可以在系统化发展过程中保护开发的想法和早期概念。它意图通过数字化记录口头、书面或素描的知识产权，甚至在创新发展过程中实时进行建模或构建结果[37]。另一项值得引用的工作来自 Zheng 等，他们提出了一款移动设备应用，使用户能够在其便携设备上检查 BIM 模型是否是最新版本，其中 BIM 模型的哈希存储在区块链上，允许搜索服务用下载模型的哈希和链上存储的哈希进行交叉检查，之后，该应用将为用户提供验证收据，声明该模型的有效性[38]。

一些主要的现有研究主题的描述突显了拟议研究的前沿范围，该研究意图融合并为当前不断发展的研究领域做出贡献。为了确定支持研究框架并配置其组件的最合适的网络，对不同类型的区块链网络进行了分析。尽管区块链技术最初是为部署公共的*无需批准*和*无需信任*网络而设计的，这些网络不需要 TTP 的存在，但其设计已经发展到了创建私有和受控许可的网络。在这些网络中，参与是受控的。参与者在写入权限（数据验证）和/或读取权限（访问数据）方面有限制。与公共网络一样，受控网络是不可改变的，节点共享相同的账本，但对网络的访问是受控的，这意味着必须授予每个节点的角色[39]。

如在第三部分中指定的那样，研究框架侧重于设计阶段，特定的客户委托设计团队根据 BIM 准则产生和管理与特定项目相关的信息。基于这些原因，区块链网络的架构必须是客户和涉及的合同方的需求的回应和平衡。因此，在评估设计过程实施的结构化环境时，区块链网络的起初理论调查涉及许可的网络。为了建立一个支持研究框架实施的许可区块链，Hyperledger Fabric（HLF）已经被分析和选定为可能最适合配置和集成在研究框架中的网络（参见第四部分）。HLF 是最流行的许可网络，非常适应于一系列使用通用编程语言编写的分布式应用程序。因此，那些在业务中创建和部署区块链应用程序的公司使用它。网络由承载区块链、执行智能合约并相互维护账本状态的各种节点组成。在 HLF 中，智能合约被称为*链码*，它们可以被公司内所有实体共享，也可以被私下共享并由特定组的实体访问。HLF 中的智能合约仅在网络共享的节点上执行，因此对其他人不可访问。通过渠道概念，选择特定节点的可能性是有保障的：在特定渠道中存在的信息和智能合约仅对渠道参与者可访问。在网络设置阶段，参与节点得到识别和认证，因此可以确定某个节点是否属于某个渠道。目前，HLF 支持以太坊虚拟机（EVM）字节码智能合约，允许使用与以太坊相同的工具编写和管理合约，从而简化配置过程。根据现有文献的调查，Hyperledger Fabric 在性能、架构和组件方面表现更好，因此被确定为潜在可在研究框架中设置并测试的网络。通过权限，当设置和运行网络时，网络参与者是已知且被承认的。在发展研究中采用区块链技术将允许创建一个网络，通过该网络，选定的参与者可以透明共享信息并安全进行交易。

基于对当前研究和应用领域的探索以及对最合适的区块链网络进行潜在识别，研究的第二个主要目标是概述所选网络的潜在设置条件。参与者、资产和预期交易也将得到说明，以及有必要在方案中引入 Oracle 服务（见第 4.2 节）。区块链网络的采用支持自动化活动的实施。这意味着，网络可以伴随设计阶段的信息管理，消除任何中间商，并利用共识协议和智能合同确保共享数据的机密性。

## 3. 研究框架

前一节讨论的主题阐明了所提出研究的两个主要创新领域。通过基于 BIM 的信息管理和区块链网络的集成，该研究旨在为传统设计阶段的发展提供创新方法。目前，与建筑领域的区块链相关的研究尚未集中于 BIM 基础数字信息管理和基于区块链的协议的集成，以自动化生产、验证和按照特定客户信息需求在设计阶段进行验证。研究提出的框架为 BIM 环境中设计阶段的区块链应用研究提供了新的视角，促进和优化了流程的可靠性和准确性。

以强调自动化流程、减少因人为干预而引起的错误或误解以及满足合同双方的要求为志向，该结合系统积极地区别于传统方法。关于研究范围和在第二部分中讨论的内容，提供了对高级框架的详细描述，突出了其价值和创新。总体流程框架通过图形表示进行说明，解释每个活动和目标。对研究中的主要关键问题的简要讨论（见第一部分）和研究中考虑的主要创新技术的描述（见第二部分）可以更好地勾勒和理解框架。具体地，通过自动信息验证和智能合同的组合来支持特定客户设计阶段的发展，主要目标是：

+   通过信任网络进行信息交流，改善客户与设计团队之间的透明度；

+   通过自动化和高效的设计验证，缩短分配任务的交付时间；

+   通过批准程序和启动系统的自动化，确保及时付款。

因此，研究的价值主要与缩短设计阶段的执行时间、项目的自动验证以及其目标的可信性以及自动付款释放有关。该研究的创新在于可能将自动 BIM 验证公证，并将批准程序与支付释放相连接。

建议的框架（图 1）提出了使用 BIM 和区块链进行信息管理整合的方式，可以改善客户与设计团队之间的互动。共同的数字化环境允许参与者在过程中共享和访问相同的信息。它与区块链的连接使信息可以追踪和不可更改，因此各方之间的信任增加。实际上，分布式环境可以帮助减少客户需求和设计团队文件之间的差异和不一致经常导致的误解！[](../images/504856_1_En_4_Chapter/504856_1_En_4_Fig1_HTML.png)

图 1

研究的高级框架

信息管理程序和区块链的结合可以提供巨大的价值，并且可以被认为是该领域有效发展的合适方向。 正如在本节开头所述，研究框架勾勒了设计阶段的执行过程，基于创新方法和技术的采用，承诺了可观的好处。该框架的主要目的目前仅限于自动符合客户的信息要求，因此在信息模型中进行其他验证（如代码检查和冲突检测）超出了研究范围。这意味着自动支付释放涉及完成整个 BIM 模型检查的一部分，该检查预期用于设计文件的最终批准。在研究的进展过程中，该框架可以扩展和普及，包括其他类型的模型验证，并定义用于验证 BIM 模型的整个自动化过程。

这个决定与为实施和验证研究框架选择的项目有关，通过概念验证。选择的项目处于设计阶段，由特定的私人客户领导。客户由意大利公共服务广播的独家特许经营商 RAI 代表。RAI 制定了 RAI-BIM 指南，以数字化其房地产资产，包括新建筑和用于办公室、录音室、剧院和仓库的现有建筑。这种创新的结果是一个综合的数字系统，由若干专有的 BIM 指南组成，分别用于信息建模和管理：（i）新建筑干预、（ii）现有建筑干预和（iii）常规和非常规维护干预。所提出的研究框架将在由 RAI 遵循的设计过程中进行配置、定制和测试，该设计过程通常由指定的设计团队开展，制定 BIM 模型（即建筑、结构、机械和电气），并根据 RAI-BIM 指南验证其符合性。在 RAI 的情况下，交付的模型获得客户批准的符合水平为 90%。

为展示研究的业务逻辑、各方互动的动态以及创新技术工具的使用，下面逐步解释了框架应用的一个示例。致力于在设计阶段执行过程中验证客户的信息需求，驱动力是专有的 BIM 指南内容，所述过程基于 ISO 19650 系列推荐的信息管理结构化程序。正如先前所述，参与信息生产和管理过程的各方具有具体的责任和任务。在研究案例中，参与的各方是客户、设计团队和验证者（图 1）。作为项目的所有者或项目承办方，客户必须进行一切活动，以确保满足准确的信息管理。因此，客户定义项目信息需求、信息生产协议、交付里程碑，并设置支持模型和信息在各方之间进行生产、共享和存档的共同数据环境（CDE）解决方案。符合 ISO 19650 系列和 ISO/TS 12911 的规定，客户已经在专有的 BIM 指南中个性化并设置了所需的信息需求、协议和里程碑。这些指南在任命过程中传达给了设计团队。一旦项目被承接，设计团队就会根据专有的 BIM 指南内容开发项目。团队根据定义的信息需求制作所有包含在 BIM 模型中的信息。这样，产生的信息将完全符合客户设定的需求，因此设计将以合规和优化的方式实现。与信息模型的开发同时进行，客户任命的验证者也接收到了专有的 BIM 指南。验证者是客户的顾问，负责详细分析指南，通过配置适当的工具将信息需求从语义语言翻译为机器可读语言。由于 BIM 项目的创建和管理需要大量数字信息的生产，手动验证难以客观和全面地进行。因此，为了确保信息需求得到完全满足，验证者确定了适用的应用程序，开发符合指南内容的自动规则集。这样的工具可以被实施在建模软件中，能够自动和完全验证根据客户需求生产的信息内容（见第四部分）。信息生产完成后，设计团队将为每个项目学科（例如建筑、结构、机械和电气）制作的 BIM 模型交付给客户。交付的模型唯一存储在 CDE 解决方案中，被视为链下数据库。CDE 中存储的文件也与区块链网络进行存储和关联，使用分布式存储系统，以跟踪模型交付周期。由于模型的尺寸很大，系统为每个交付的 BIM 模型创建一个加密哈希，通过智能合约将其存储到区块链网络中。哈希添加到区块链网络中，能够检查存储在具有相同名称的对等方计算机内存上的映射 BIM 模型。这样可以以一种统一且安全的方式控制对 BIM 模型的访问和更改。当交付新模型时，将比较其哈希和已存储模型的哈希。这样可以透明地检查同一模型是否被重复交付，以及在验证过程之后宣称已经进行了修订的模型是否被修改。

在交付过程后，验证人员使用预先编程的应用程序自动验证和验证 BIM 模型中包含的信息。对于每个验证的模型，应用程序独立生成包含验证结果的报告。生成的报告存储在 CDE 中，并且模型的哈希值可能被记录在区块链网络上，因此可以透明地记录和映射建模过程的进展。在这种环境下，项目验证和验证活动得到明显管理，改善了客户和设计团队之间的沟通。信息的自动验证加快和优化了审查和交付过程。结果的归档使客户能够评估信息需求的符合性。该框架还确保了在阶段进展期间不存在不符合和争议。报告的结果显示了生产的信息与客户要求和交付的时机的符合性。交付的模型被批准的符合水平在开始时由客户定义，并在约定时通知设计团队。模型中包含的信息的自动验证分别针对每个学科进行，因此每个验证周期会创建四个独立的报告。

如果信息模型的自动验证生成的报告结果低于设定的合规水平，设计团队将收到报告，其中包含所有检测到的不符合情况，并必须进行更改和指示的修正。然后设计团队必须随后进行新的交付。另一方面，如果达到了设定的合规水平，即生成的信息满足客户的信息需求，模型将被接受并存储在 CDE 中，以便进行未来的建筑和/或建筑运营和维护。因此，与区块链网络连接的自动验证过程结合了通过采用客户与设计团队之间的智能合同自动执行合同性能。由于区块链不能直接检索外部信息，因此需要使用 Oracle 创建智能合同和链下数据源之间的连接。在任命时，客户和设计团队已经建立了任务完成后付款批准的条款和条件。这些条件决定了在交付模型的验证达到设定的合规水平时才授权释放付款。为了自动化此批准过程并直接与模型验证结果关联，付款条件被转化为智能合同。因此，后端 Oracle 确保了验证报告结果与区块链之间的连接，以传输和存储结果在 Oracle 智能合同中。存储在 Oracle 智能合同中的数据可以通过用于付款的智能合同检索，比较达到的合规水平是否等于或大于设定的水平，如果是，则启动交易。付款的智能合同与托管账户相连，只有在任务按预期完成时才持有和发放资金，确保向设计团队释放付款。

所追求的业务逻辑使得编码的支付条件在每个信息模型的验证周期结束时自我执行，如果合规水平等于或高于客户设定的水平。事实上，在每个模型验证周期中，应用程序报告验证的模型类型、验证时间和达到的合规水平，并自动与各方之间约定的设定水平进行比较。该过程激励参与者按照合同规定执行其分配的任务。制定的信息并包含在 BIM 模型中，是通过遵循客户要求开发的，并且设计团队经智能合同批准完成的每个交付阶段的支付。因此，设计周期以及随后的验证是一个迭代过程。只有当报告的结果等于或超过允许验证标志的合规水平的定义阈值时，模型才会被归档，并且该活动的付款会自动获得批准。

## 4. 研究框架的拟议技术

前一节展示了研究框架的整体流程。该框架的创新和价值在于自动 BIM 验证与智能合同应用的整合。因此，尽管所提出的框架的解释仍然停留在理论水平，本节致力于描述预期用于通过概念验证框架的实际测试中配置和使用的技术的一般功能。因此，首先强调了信息验证和验证的重要性。然后，解释了根据客户要求设置自动验证 BIM 模型应用的一般方法。第二部分侧重于潜在区块链网络的架构，定义了其使用的组件和规则。并且说明了使用 BIM 进行设计开发和验证以及使用区块链进行设计跟踪的整合。

### 4.1 自动验证信息的方法

信息制作、审核、验证和管理是研究框架的基础，必须在专有的 BIM 指南中明确的信息要求得到客户的同意后才能完成。如上所述，研究范围仅限于设计阶段，客户在其中扮演委托方的角色，要求根据其 BIM 指南生产和管理数字信息。研究的提出框架旨在测试其在第三部分简要介绍的项目中的操作、有效性和创新性，被视为研究的概念验证。因此，由客户要求并由设计团队用于设计阶段模型实现的软件是已知的且为 Autodesk Revit 撰写工具。因此，用于执行数字信息的自动验证的应用必须能够与该建模软件进行通信。在 Revit 应用程序中，允许对 BIM 模型进行个性化检查的应用程序中，Autodesk Model Checker for Revit 已经被选择，因为它允许创建可定制的验证规则集用于数据和命名约定检查。在项目开发过程中信息的逐步数字化使其数量和复杂性显著增加。BIM 模型可以被定义为必须符合客户要求的项目所有信息的储存库[22, 24]。事实上，根据国际标准，在项目开发期间生产和管理的信息必须在过程的每个计划阶段结束时进行验证。在该研究背景下，因此，对 BIM 模型中包含的信息进行审查和验证成为实现指南内容合规的基本活动。

为自动信息验证设置一个应用程序变得至关重要，因为经常验证 BIM 模型是手动实施的。这项活动耗时且容易出错，可能会导致后续阶段的争端和不满。鉴于这些验证操作被证明是至关重要的，创建自动化 BIM 验证流程在数字信息管理中至关重要。为了开始解决这些问题，研究的第一个目标是描述信息验证的工具操作框架。为了给信息审核过程带来更大的可靠性和完整性，在 BIM 模型活动验证方面定义的整体方法在图 2 中有所阐述。这种方法是从专有 BIM 指南的分析和解释开始实施的。客户使用语义语言来定义设计的信息需求，并将它们集成到自动验证的应用程序中，必须将其翻译为可被选定软件（即 Autodesk Model Checker Configurator）解释的机器可读语言。这两种语言之间的中介是通过一个面向领域的语言实现的，其术语允许专业人员在其中操作的领域进行简单和直接的定义。确定的应用程序不会修改要分析的信息模型，但是基于规则集，如果模型与领域不一致，则会报告任何错误信息。规则集包括将指南信息需求翻译为验证领域，并代表验证领域的验证。![](img/504856_1_En_4_Fig2_HTML.png)

图 2

自动验证的流程方法

因此，自动验证的功能逻辑是基于创建验证域（即指南的内容），该域用作参考来验证模型是否落在该域内。BIM 模型中规则集的实施生成了每个验证要求的“已通过”或“已拒绝”的结果。实际上，规则集是在每个 BIM 模型（即建筑、结构、机械和电气）中实施并执行，从而完成全面的验证循环。活动最后的结果是为每个 BIM 模型生成一个报告，其中包含验证结果。这些报告包含了模型中所含信息与专有 BIM 指南中信息要求之间的所有错误和不一致之处。设置自动信息验证流程的方法始于识别需要翻译并纳入应用程序的专有 BIM 指南内容，以及制定需要遵守的每个规则集的一般组织架构的定义。由于建筑工艺的数字转型使信息数量增加，客户建立的信息要求相当多。特别是所选项目的专有 BIM 指南的内容可以分为三大类需要验证的信息要求：(i) BIM 对象命名约定，(ii) BIM 模型模板命名约定和(iii) BIM 对象参数。在第一类别中，针对每个专业（即建筑、结构、机械和电气），定义了 BIM 模型的命名约定，可加载家族、系统家族及其类型的名称，以及图纸和材料的命名约定。在第二类别中，针对每个专业，定义了关卡、视图（图纸、立面和剖面）、时间表和网格的命名约定。最后，第三类别定义了与每个对象的参数及其值的关联。针对专有 BIM 指南的重要内容进行评估后，使用 Autodesk Model Checker for Revit 应用程序进行信息要求的解释和翻译的工作无疑是繁重的。该应用程序的操作框架必须涉及为每个专业确定的两大类规则集，即与所有命名约定有关的规则和与参数有关的规则。通过选择的应用程序的支持，这两个宏观规则集从语义语言翻译成机器可读语言，以在 BIM 模型中实施。

通过这种方式，创建了要包含在构成验证领域的更大规则集中的每条规则。然后，在模型中实施每个验证规则集，并在应用程序执行结束时，自动获得包含检测到的错误的验证报告。为了展示一个具体的例子，图 3 显示了按照专有 BIM 指南开发的结构 BIM 模型中规则的实施和验证，以测试自动验证工具。实施的规则旨在验证结构墙类型的命名约定，并在性能结束时获得验证报告。报告对每个识别的元素进行了详细说明。在本例中，与结构 BIM 模型中包含的墙体类型相比，检测到两种不符合指南的名称不同。根据应用程序报告的客户要求中定义的墙体类型使用的命名约定与结构模型中使用的命名约定之间的符合百分比为 82%。正如本示例意图展示的那样，仅验证结构墙体类型的命名约定，所获得的 82%代表了模型相对于单个信息要求的符合水平，而不是 BIM 指南的整体内容。图 3 说明了对于每个被拒绝的元素，报告都显示了 ID，从而方便快速在模型中识别并进行适当的更正。通过对所选应用程序的体系结构设置的简要说明，可以理解一旦定义了逻辑过程，将规则集在应用程序中的详尽实现最初需要投入时间来进行创建和定义，但最终可以节省大量时间在未来的设计和验证过程中。![](img/504856_1_En_4_Fig3_HTML.png)

图 3

结构 BIM 模型中规则实施的示例

### 4.2 可与信息自动验证集成的潜在区块链网络

正如所示，用于自动验证 BIM 模型中包含的信息的第二个主要目标是研究框架的架构定义所选择的潜在区块链网络。第 2.2 节表明潜在的要评估的区块链网络是超级账本 Fabric（HLF）。正如先前宣布的，研究项目是在专有环境中应用的。因此，标识和未来使用以身份管理、隐私和高效处理著称的网络在这一研究中显得是适当的。从技术角度看，HLF 架构的关键特性包括（i）身份管理，（ii）通道，（iii）账本，（iv）共识机制，（v）智能合约和（vi）政策。不同于*无许可*网络，HLF 通过分配数字身份证书登记成员，管理用户 ID 并实现对所有网络参与者的认证，以创建访问控制列表[41]。如此一来，隐私成为网络运作的关键要求，在这个网络中，相互认识的各方交换敏感和机密信息。通过创建通道，参与者可以组成不同的交易分类账。通道使信息（交易）根据约定的政策交换给一组对等体（参与者）。创建私有通道使需要机密交易的任何群体可以在同一有许可的网络上共存。作为一个区块链网络，HLF 的记账是不可变的，并且它把每个通道中的交易历史和当前状态都记录下来。每个通道都有一个记账，并且每个对等方都保留着它所属的每个通道的副本。在 HLF 中，共识机制由网络选择，以确定最能代表参与者之间关系类型的一种。共识机制允许网络验证区块中包含的交易的正确性。当区块中的交易顺序和结果满足网络的政策时，共识就实现了。背书政策是 HLF 与其他区块链不同的地方。事实上，HLF 更真实地模拟实际世界，因此交易必须由网络中的可信方验证。背书政策与在 HLF 中代表智能合约的每个*链码*相关联（参见第 2.2 节）。每个智能合约都允许对在通道上调用某种类型的交易的逻辑进行编码。还存在其他政策，例如关于谁可以查询或更新分类账，或者谁可以添加或删除参与方的政策。最后，HLF 可以通过管理资产来代表有形或无形价值，通过这些资产，网络上几乎可以交换任何具有货币价值的东西。

上述概述便于理解研究框架所建议的 HLF 架构。确切地说，关于描述的关键特性和在高级框架中指出的参与方（图 1），在这里识别和说明了 HLF 的组件，这些组件定义和确定了系统的功能，并按照创建的连续顺序进行了说明（图 4）。特别是，参与者是参与区块链网络的一方，资产是参与者之间交换的价值，交易是指定过程中的某些事件并控制其发展的逻辑智能合约。通过身份管理，每个参与者都可靠地带有姓名和唯一 ID。通过网络的隐私性，访问根据每个参与者的角色进行控制，在此环境中，各方彼此了解。每个资产都以名称、ID 和类型识别。同样，每个交易都用唯一的 ID、名称、时间戳和发送者定义。在每个交易发生之前，都要定义和检查基于共识的政策和规则。![](img/504856_1_En_4_Fig4_HTML.png)

图 4

区块链网络组件

批准政策旨在指示必须签署交易以声明其有效的参与者。只有有效交易才能更新分类帐的状态。在研究中，这项政策主要委托给负责验证交易的客户。设计团队提出了用于 BIM 模型交付的交易，验证者提出了用于验证报告的交易。第二项政策涉及更新和查询分类帐的责任。在研究中，设计团队和验证者是主要负责更新和维护分类帐中数据的一方，而客户可以查询以检索即时数据。确定要在研究中实施的 HLF 网络的元素和逻辑允许完整地了解系统中涉及的技术的集成和操作架构。由于拟议的框架的范围是自动 BIM 验证和智能合约的组合，该架构需要实施 oracle。引入 oracle 需要创建一个专用渠道，即全局渠道，在其中网络参与者作为负责维护和更新分类帐与外部来源的可信任人员。该渠道配备有一个 oracle 智能合约，用于更新网络，并可以查询更新后的数据（图 5）。![](img/504856_1_En_4_Fig5_HTML.png)

图 5

高级集成结构

参与者，在另一通道操作，确实可以查询总帐，以便咨询和获取某些更新的信息。就像已经解释的那样，流程始于通过专有 BIM 指南界定客户信息需求。然后，设计团队根据这些指南开发的 BIM 模型通过设置应用程序提交，并自动由验证者验证。验证会自动生成一个包含达到的合规级别的验证报告。报告中包含验证的模型指示，验证日期，未通过的元素以及合规百分比，它代表了要连接到区块链网络（即智能合约协议）的外部数据源，因为它是由网络外部的工具生成的。作为验证活动的监督者，验证者在全局通道上操作，代表着可信数据的提供者。验证者确实有规则和政策的授权来调用验证报告更新总帐。部署在全局通道上的智能合约请求外部数据，提供更新和查询事务。在另一个通道，即客户-设计团队通道上，客户随后可以调用智能合约，利用跨通道查询能力检索最新的更新值。智能合约逻辑被激活，验证外部源的值是否等于或大于建立的合规级别。如果是这种情况，根据共识规则执行逻辑，并批准释放付款。这意味着智能合约逻辑设置执行给定指令，如果满足其他给定条件。它可以重复验证已建立的条件（达到设定的合规级别），并仅在条件达到时执行计划的操作（BIM 模型已达到设定的合规级别）。

## 5 预期结果讨论

通过对 BIM 模型信息内容的自动验证以及智能合同的应用，该研究框架旨在缩短设计阶段的执行时间，确保满足客户需求并获得对设计团队付款的批准。由于项目复杂度的增加，信息需求的实现和延迟付款是产业趋势中相关的因素[1]。所提出的研究框架仍处于理论水平，在第三部分中，将预期测试该框架的项目作为概念验证。未来对框架进行测试以及分析所得结果将确实是所提议研究发展的下一步。因此，在本节中，披露和讨论了预期的结果，其识别可被视为比较未来结果的基准。框架的主要目的在于基于 BIM 的信息管理和区块链网络之间的集成，以改善客户与设计团队在设计阶段之间的联系。研究中呈现的综合环境使合同各方能够全面生成、审核和维护相同的信息。通过专注于流程自动化，控制和验证信息的活动，以及批准付款释放的活动，都是由编码应用程序而不是人类执行的程序执行。这种创新的方法促进了设计阶段执行时间的缩短，便于控制任何返工，并确保在符合合同条件时批准付款释放。

ISO 19650 系列推荐的信息管理实践促进了过程中各方的不断互动。基于 BIM 的信息管理的特征在于完全交换数字信息，其修订动态报告并整合，提高了对项目进展的控制，并减少了不符合规定的情况。由于 BIM 模型的信息含量很高，采用能够自动检测错误和不符合情况的应用程序是适当的，有利于积极响应客户的信息需求。一旦 BIM 模型中包含的所有信息完成，就有必要进行验证，以确认与指南要求的符合性。正如前面所强调的，在 BIM 环境中，设计团队产生的信息的验证成为尊重客户需求的一项基本活动。事实上，这一活动的不准确执行不仅会对项目的发展和管理产生负面影响，而且还可能导致潜在的昂贵的不准确性，因此必须予以避免。为支持这一任务，开发一款允许自动验证信息的应用程序变得至关重要，以全面检查与 BIM 指南的符合性。

旨在自动和数字化验证客户信息需求的满足，应用程序的架构是通过四个主要活动开发的。通过对该应用程序的初步测试，可以总结一些预期的益处。首先，建立用于自动信息验证的应用程序可以为客户提供一个有效的工具，仔细审核设计团队所产生的信息。采用这样的验证流程有助于改善客户和设计团队之间的沟通。在设计阶段产生的信息的验证不再是手工、耗时和曲折的活动，事实上它变得全面和详细。其次，因此，设计团队将被鼓励按照客户的信息需求生产信息，以减少工作时间和返工的可能性。同时，在出现负面审核结果的情况下，获取一个包含所有被拒绝元素的详细报告，有助于设计团队实施有针对性和快速的修正和补充。最后，客户可以监控项目的实际进展和设计团队的准确性。模型的详细验证确保满足信息需求，并且过程的自动化大大减少了传统验证和验证时间。根据一些初步实验，在使用传统流程和自动化流程验证项目所花费的时间进行了统计比较，结果显示两栋建筑（图 6）样本中，使用自动化流程的时间减少了近 60%。这些建筑的 BIM 模型由外部设计团队开发，用于 RAI 要求和发起的房地产资产的真实数字化。这些 BIM 模型与办公楼和录音室有关，其面积分别为项目 A 的 15000 平方米和项目 B 的 12000 平方米。为每个 BIM 模型，指定的设计团队开发了涵盖四个主要学科的四个 BIM 模型。为了突出研究提出的自动验证的创新价值，这些模型的验证是根据在第 4.1 节中介绍的两个宏范畴的规则集的手动和自动方式进行的。统计分析将在研究的进化过程中进一步完善和改进。![](img/504856_1_En_4_Fig6_HTML.png)

图 6

自动设计验证和验证与手动验证的时间比较

意味着在设计阶段实施区块链网络，其架构需要适当的选择和配置。在可能的区块链类型中，许可区块链被认为是最适合研究的网络类型，设置在专有环境中。提出使用 Hyperledger Fabric，因为它是专为企业业务而建立的。许可网络只允许选定的参与者进行协作和交易，实际上在设置和运行网络时已知和认可网络参与者。该网络保证了隐私和身份的控制。由于数字身份与每个对等体的社交身份之间的对应关系，私有网络在真实场景中比公共网络更容易实施，具有更高的运行效率，更好的交易性能和更低的成本[42]。在探索的设计阶段，使用这样的网络允许客户过滤访问，识别参与者，并保证通信和信息交换的隐私和安全。为了在研究中设置和测试已确定的网络，其架构通过确定工作通道、参与者、资产和预期交易来定义。自动化 BIM 模型中所包含的信息的验证以及随后批准支付释放所需的目标，使用智能合约，强调了需要可靠地将 BIM 流程与区块链网络连接起来。将外部数据导入区块链使用了一个 oracle，能够以受信任的方式连接自动 BIM 验证之前定义的应用程序和智能合约的自动业务逻辑。这意味着一个参与者，在这种情况下是 BIM 模型的验证者，成为在一个单独通道中运行的信任组织。只有 oracle 被授权向 oracle 智能合约发布更新，这些更新将是与自动验证结果相关的外部数据。由于所添加的 oracle 在不同的通道中操作，因此客户和设计团队之间的智能合约将通过一个跨通道智能合约查询访问所需的数据（即验证报告）。

一个许可网络的潜在设置允许确定一些预期的优势。首先，将区块链网络整合到通用框架中，支持自动化活动的实施。这意味着网络可以与设计阶段的信息管理相结合，消除任何中间人，并确保使用共识协议和智能合约保证共享信息的保密性。其次，客户与设计团队之间的智能合约将确保客户愿意支付并在自动批准后确定支付的确定交付。

在研究的理论阶段，选择了一个获得许可的网络，因为从架构和功能的角度来看，它为研究框架的环境提供了适当的网络。另外，考虑到选定的真实项目，选择这一方案是为了避免与公开信息可视化和使用公共网络的费用相关的问题。在为概念验证开发区块链网络的实际过程中，还将考虑、调查和测试其他类型的网络以及与公共区块链的可能链接，以保持技术的性质和原始含义。采用公共网络应考虑组织、经济和监管问题，并分析可能的替代解决方案，以最小化运营成本。能够真正实现并响应研究目标的系统将被选择并用于将来研究发展中概念验证的实施过程中。总之，主要预期成果与以下相关：(i) 过程效率的增长，(ii) 信息生产、审查和验证的改善，(iii) 过程自动化的增加，以及 (iv) 交付时间的尊重和支付的释放。

## 6 结论和进一步发展

展示的研究框架旨在表明，新技术的出现可以积极支持建筑行业的数字化。提出的框架说明了自动 BIM 验证和智能合同的采用如何可以简化和缩短设计阶段的执行。本章指出了基于 BIM 和区块链的信息管理的整合，作为解决客户要求兑现、可靠信息审核和验证、以及迟付款等弱点的解决方案。这两种技术的结合提供了巨大的价值，并且可以被认为是设计阶段高效发展的合适方向，从而吸引行业参与者。该框架提供的潜力可以充分发挥基于 BIM 项目的信息。在讨论预期结果时，简要展示了如何自动验证 BIM 模型中包含的信息可以显著减少验证项目符合客户信息需求所花费的时间。应用自动设计验证可以通过区块链的整合和使用实现对整个流程的自动化验证，直到完成验证，并且这将通过概念验证的开发和测试得到证明。进一步的研究发展可能涉及对框架进行其他验证程序的验证，如冲突检测和代码检查，以便批准的 BIM 模型可以在招标和施工阶段作为法律参考，作为监控所有项目要求和规格兑现的参考，或在维护和运营阶段作为建筑寿命周期的更新数据库。
