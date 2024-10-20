© 作者，独家许可给 Springer Nature Singapore Pte Ltd. 2022M. Dutta Borah 等人（编辑）AI 和区块链技术在 6G 无线网络中的应用区块链技术[`doi.org/10.1007/978-981-19-2868-0_3`](https://doi.org/10.1007/978-981-19-2868-0_3)

# 在 6G 中启用的区块链去中心化网络管理

Steven A. Wright^(1  )(1)乔治亚州立大学，亚特兰大，美国 Steven A. Wright 电子邮件：swright22@gsu.edu

## 摘要

互联网已从容错基础架构发展到支持社交网络和机器用户的语义网络。随着网络威胁和隐私问题日益突出，对数据和基础设施的信任变得越来越重要。通信服务越来越多地通过虚拟化、软件定义的基础设施提供，例如跨多个基础设施提供商的覆盖层。越来越多地认识到服务不仅需要容错性，还需要抵御审查，同时通过服务提供商生态系统的复杂体系交付日益丰富的服务驱使需要像区块链这样的去中心化解决方案。服务提供商传统上依赖合同安排全球端到端服务的交付。现在，一些合同条款可以通过区块链上的智能合同自动化。这是一个具有多个参与者和资源的复杂分布式环境。区块链不仅被提议用于业务服务层，还用于网络基础设施的运营，包括动态频谱管理、SDN 和资源管理、计量和物联网服务。传统的网络管理方法依赖于客户端-服务器协议和集中式架构。网络运营商和许多客户的数字化转型已经导致基于虚拟化网络功能的通信服务的软件定义基础设施。去中心化的网络管理方法已经引起了研究人员的越来越多的关注。运营商对数据、操作和商业交易的信任以及通过软件和设备故障以及网络攻击维护业务连续性的机制的增加需求进一步推动了基于区块链的方法。

关键词零接触服务管理零信任区块链信任抗审查物联网

## 1 引言

互联网已经从容错的基础设施发展到支持社交网络和语义网以供机器用户使用。 6G 无线电技术带来了网络性能的提高（例如，带宽和延迟），这不仅承诺了现有应用程序的性能提升，而且可能还可能在规模上支持新类型的应用程序。触觉技术可能是最容易识别的新类别的应用程序，因为它们为通信引入了一种新的感觉机制（触摸）。触摸是一种人类感官机制，但互联网的机器用户具有不同的通信需求。网络技术的机器使用的部署规模和应用广度大于人类通信部署，并且已经有数十亿台设备部署在物联网中。通过分布式物联网设备生成和分析的数据也预计会显著增长[1]。在可用数据的分析和语义注释方面的进展也支持了通信服务的机器使用的增加。大数法则规定，在这种规模的系统中，故障是不可避免的。复杂的架构和冗余的部署大部分限制了物理故障的范围。随着通信变得更加以数据为中心，并由机器而不是人类使用，与数据故障相关的问题（例如，不完整，格式不正确，无法验证和不可信的数据）变得更加棘手。

信任数据和基础设施已经变得越来越重要，因为网络威胁和隐私问题不断上升。信任和声誉历来是人类评估的概念，但这些概念越来越多地应用于计算和通信环境。无线网络的信任已经研究了超过 10 年[2]。信任是物联网应用程序的一个日益重要的特征[3]。人工智能（AI）方法在计算评估信任方面变得越来越重要[4]。区块链也作为一种信任机制设计模式引起了广泛关注。在不确定和不断演变的实体关系中，信任是至关重要的。随着应用程序，包括网络管理，从集中式的单片架构向分布式微服务架构演变，通信实体的数量必然增加，因此在这些通信中信任的重要性也增加了。网络管理不仅是对其消耗的数据的可信度，还包括对基础设施正常运行所需的信任关系的管理。

通信服务越来越通过虚拟化、软件定义的基础设施进行交付，例如跨多个基础设施提供商的覆盖层。虚拟化基础设施基于对底层资源的某种模型或抽象。该模型可能具有有限的准确性、精度或操作有效性范围。底层资源是多维的（例如，计算、存储和带宽），分布式且异构的。虽然已经有了大量与优化这些资源相关的理论努力，但通过实验方法对资源进行表征也可能是有效的 [5]。软件定义的基础设施使这些基础设施的自动配置成为可能，但配置可调性的最佳程度和资源粒度的级别仍然是开放问题 [6]。然而，这并没有阻止大规模虚拟化基础设施在 5G [7]中的应用。传统网络一直需要多个运营商来提供全球基础设施。5G 网络。5G（和 6G）的更高带宽是通过更高频率的载波来实现的，但代价是更有限的范围，导致更偏向于部署小区作为基础设施。已提出了各种不同的商业模式来支持小区的大规模部署 [8]。最终结果似乎很可能是需要动态组装更多的基础设施提供商，以提供全球服务。这增加了管理此类外部、分散资源的任务的复杂性。

人们越来越认识到服务不仅需要容错性，还需要抗审查性，同时通过服务提供商复杂的生态系统提供越来越多样化的服务，这推动了像区块链这样的去中心化解决方案的需求。通信基础设施的设计和开发是为了在面对各种各样的物理和环境灾害时具有弹性（例如，飓风，龙卷风）。随着全球经济变得更加数据驱动，对基础设施可用性以及传递信息的有效性的敏感性也越来越高。由于政治、商业或个人原因对通信进行审查可以被视为对信息基础设施完整性的攻击，但这些攻击的范围和规模是一个正在进行研究的课题[9]。这类攻击似乎有可能增加而不是减少，因此，在 6G 环境中提供抗审查攻击弹性的基础架构方法似乎是需要的。区块链基础设施被提议作为提供某种程度的抗审查性的机制。无论是通过删除还是扭曲数据，审查都是对通信完整性的基本威胁。检测、测量和控制这类威胁对于通信网络来说是一个重大挑战。

传统上，服务提供商依赖合同安排来全球交付端到端的服务。随着 6G 的到来，服务的种类和服务提供商的数量都有望增加。这导致了对于服务提供商动态组装所需服务伙伴以向客户交付服务的自动化机制的压力增加。随着物联网和其他机器用户的兴起，API 和其他自动化变得必要以实现服务交付。区块链被提议作为远程各方之间进行财务结算的机制。一些合同条款（例如，服务失败时的违约金）现在可以通过区块链上的智能合约进行自动化。对于服务调用和修改（例如，通过 API）的合同自动化对于通信服务来说可能是一种新奇的事物。然而，随着 6G 中机器用户的比例增加，这变得更加必要。这种合同活动的自动化增加了网络管理责任的范围。

在大规模运行的同时升级基础设施和发展服务是一项复杂的任务。基础设施的虚拟化使得数据驱动的自动化成为可能。没有可信的数据来驱动软件自动化，服务提供商的管理操作可能会受到破坏。自动化也可能加剧故障的范围和规模。精心定位的自动化可以帮助克服基础设施的脆弱性。大规模系统中故障的不可避免强调了自动化故障转移和服务恢复机制的重要性。分散化消除了集中式系统中的单点故障。随着 5G 部署现在开始，6G 部署的目标是在 2030 年代开始。

将这个关于区块链启用的 6G 分散网络管理的讨论框架放在一起，需要理解 6G 的背景。接下来的部分概述了 6G，重点介绍了所需的资源和服务管理的范围。第三部分回顾了分散网络管理技术和架构的演变。区块链技术最初是为支持金融科技应用而开发的，特别是远程各方之间的交易。虽然网络管理一直对运营成本有隐含的关注，但在通信市场中使用区块链基础设施是一种颠覆性的方法，这些市场一直受到严格的监管。第四部分考虑了 6G 网络管理的经济模型。智能合约已被用来自动执行金融交易。第五部分考虑了智能合约和 API 在分散网络管理中的作用。智能合约只是自动化的一种形式。在大型通信基础设施中驱动网络管理的数据的体积、种类、速度、价值和真实性显然是一个大数据问题，需要自动化支持。人工智能（AI）经常被提议作为支持大数据问题上的自动化的机制。第六部分回顾了人工智能在分散网络管理中的作用。虽然区块链方法可能很有前途，但这并不意味着它们在设计、实施和运行中没有挑战。第七部分讨论了网络运营商在使用区块链分散网络管理时面临的挑战。然后在第八部分中提出结论。

## 6G 网络管理的范围：服务演变与资源与服务管理

在 6G 中，网络管理的范围受基础设施和商业环境预期的影响。5G 基础设施已经演变成一个由多个参与者构成的复杂分布式环境。通信基础设施已经从面向特定服务的基础设施（例如电报、电话）演变为更复杂的服务混合体。预计 6G 时代的通信服务将对人类和机器用户更加多样化。

随着基础设施和商业环境的复杂性增加，网络管理正从管理设备逐渐演变为更抽象的模式——管理资源和服务。最初的数据模型和信息模型非常专注于设备功能，但通过 NFV/SDN 对基础设施进行虚拟化，使得基础设施从底层硬件中更抽象出来，并在通用计算基础设施上执行软件实现。行业论坛已经制定和标准化了基于软件定义网络、网络功能虚拟化以及许多网络配置功能的编排或自动化的新网络管理架构[10]。网络管理的范围不仅包括物理层（无线、光纤等）基础设施，还包括虚拟化的网络功能及其所在的计算基础设施。预计在 6G 的背景下，自动化或编排的基础设施功能范围将增加。这些新的范式对传统的网络管理系统和运营支持系统（OSS）产生了巨大影响。商业环境的复杂性增加需要更多自动化的商业支持服务，包括操作商业基础设施的报价、订购和计费。行业响应的架构框架包括 TMF 的开放数字架构（ODA）[11]和更加服务特定的 MEF 的生命周期服务编排（LSO）[12]。像这样的框架有助于实现跨多个服务提供商的端到端自动化——包括通过 5G 和 6G 无线接口提供服务的服务提供商。5G 和 6G 部署的新频谱位于更高频率，对应的传输范围更短，更青睐于小区。5G 中的专用服务和小区重点加强了私有网络部署模式，而不是基本的广域公共服务。需要通过各种私有网络交付端到端服务的需求加强了在 6G 背景下这些架构框架的需求。基础设施中要管理的服务范围不仅包括传统的连接服务，还包括这些额外的自动化商业支持功能。

在 6G 中，从通用服务向服务碎片化的趋势预计会持续下去。基础设施的虚拟化与 NFV-SDN 使网络覆盖、网络下层和网络切片等概念普及起来。提出了基于 SDN 控制器的区块链实现，以提高安全性[13]。虚拟化基础设施的选择还使依赖于底层基础设施提供者的虚拟运营商成为可能。当前的 NFV-SDN 实现支持网络切片，但并未适应支持移动网络运营商（MNOs）之间的商业协议。目前 4G 网络提供的服务种类已经包括内容服务（例如视频）和安全服务（例如身份管理）。预计 IoT 设备和边缘计算的增加将增加服务提供商提供各种非传统受信任服务的要求。在 5G 和 6G 中的新服务（例如 URLLC）利用网络切片来针对汽车或智能城市等行业垂直领域。网络切片可以独立管理，这增加了网络管理范围的复杂性[14]。随着这些特定于服务的网络切片的部署和成熟，这些新形式的服务多样性进一步增加了可能需要由服务提供商支持的业务模式的多样性。预计业务模式将越来越多样化，并且动态变化，许多服务提供商依赖于其他服务提供商来提供端到端服务。在这种 6G 环境中，服务管理不仅仅是资源管理，对于端到端服务的供应、保证和适当的收入收取变得越来越需要。已经提出了一系列区块链方法来支持各种计费和结算用例[15]。支持这些区块链用例的行业标准也开始出现[16]，并且开源实现也在涌现[17]。6G 中的服务碎片化创建了一个更加复杂的商业环境，需要相应增加网络管理的范围来提供这些服务。

网络管理的范围传统上包括故障（Fault）、配置（Configuration）、计费（Accounting）、性能（Performance）和安全（Security）（FCAPS）等类别。在这种情况下，服务保障传统上演变为可用性，但这可能不再适用于 6G。政府、企业和个人越来越依赖于数据驱动的信息系统。信息访问设计模式也趋向于采用零信任网络架构[18]。这些方法需要对数据访问进行更精细的控制。这些控制也需要在规模上进行有效管理。随着网络安全威胁不断增加，数据篡改、毒化或审查的风险以及与未经授权或不受欢迎的数据曝光相关的隐私风险也越来越受到关注。这些可以视为信息基础设施的失败。在 6G 时代，服务提供商似乎需要提供超出可用性的网络管理服务保障，包括身份、可信度和抗审查性等方面。6G 网络管理的范围需要扩展到包括支持服务的底层数据的可信度和抗审查性，以及参与服务交付的各种身份。在配置和计费方面，6G 网络管理责任的范围可能与当前的做法类似；尽管需要配置和核算新的资源和服务。在故障、性能和安全方面，网络管理责任的范围似乎会随着对数据资源和服务的新维度的关注而增加。6G 网络管理将需要新的指标、测量和控制技术，以在隐私、可信度和抗审查性等数据维度上提供服务保证。

传统的网络管理方法依赖于客户端-服务器协议和网络管理器的集中式架构。区块链不仅被提议用于业务服务层，还用于网络基础设施的运营，包括动态频谱管理、软件定义网络（SDN）和资源管理、计量和物联网服务。[19]提出了一个增强频谱管理功能的统一 SDN 和区块链架构，以实现用户在移动网络运营商之间的无缝漫游能力。[20]提出了一个基于智能合约的用于共享频谱和基础设施的代币化模型。集中式的网络管理方法通过为单个服务提供商聚合分析和控制来提供运营效率。6G 时代预期的基础设施规模和服务复杂性表明，网络管理视角应该对服务交付所需的多方可用。由于需要多方合作进行服务交付，因此需要机制来支持运营中的信任和共识。在这种情况下，传统的集中式网络管理方法似乎可能被更加去中心化的网络管理方法所取代。

区块链已被提议用于 6G 网络的各种角色[21]。基于区块链的去中心化网络管理可以从两个角度来看待——一是去中心化网络管理需要将区块链作为资源来管理，或者说去中心化网络管理本身是使用区块链技术实现的。然而，为了确定 6G 网络管理任务的范围，更重要的是关注被管理的资源和提供的服务。以下小节进一步探讨了 6G 资源管理和 6G 服务管理的范围。

### 2.1 6G 资源管理

在 6G 中需要管理的基础设施资源可以以各种方式进行分类，而 6G 与用于无线服务的射频基础设施相关联。传统上，大部分核心网络基础设施都是非射频通信基础设施。此外，NFV 的引入将计算基础设施资源纳入网络管理的范围，并且边缘计算加剧了这一趋势。已经提出了在多个应用场景中使用区块链进行 6G 资源管理和共享，包括物联网、设备对设备通信、网络切片和跨域区块链生态系统[22]。6G 基础设施资源将需要包括大量的非射频通信基础设施、6G 射频资源和 6G 计算资源。

6G 时代非无线通信基础设施的网络管理资源是传统的网络管理资源。通信链路（例如光纤）和交换机或路由器提供了 6G 架构的基站、小基站和其他节点之间的传统第 2 层和第 3 层连接。这些资源的信息模型在工业界已经得到了很好的发展。存在多个中心化的协议（例如 SNMP），用于基于这些信息模型的网络操作。这些资源通常由单个运营商管理。非无线通信基础设施预计将保持为边缘提供 6G 无线资源连接和其他服务的重要基础设施。

6G 无线资源的网络管理提供了对专用（许可）频谱以及共享（非许可）频谱的管理机会。频谱许可已将频段分配到指定地理区域内的特定服务提供商。不同地理区域内的独立频段选择为分散化解决方案提供了基础。非许可频谱可以由多个方使用，通常接受干扰风险。甚至许可频谱也可能不总是被使用，提供创新的潜力。利用这种频谱空白通常需要监管或许可变更，以及减少干扰的协调机制。特别是在私人网络中，小基站的部署为频谱共享提供了一个特定的背景，这似乎在 6G 中很可能普遍存在。已经提出了区块链机制用于频谱共享。[23] 提出了区块链作为多个网络运营商之间的频谱共享的可信机制。大规模部署的物联网基础设施也是由多个方以分布式和分散化的模式推动的。ITU-T Y.4464 提供了区块链作为分散式服务平台的框架[24]。6G 无线资源的网络管理似乎可能需要分散化解决方案。

在 6G 时代，计算资源的网络管理可能需要一种新的资源类型来满足一些通信服务提供商的需求。然而，云计算资源的管理是一个众所周知的技术。云计算通常是集中式资源，许多服务提供商已经开发了自己的云基础设施或利用了公共云基础设施。然而，边缘计算创建了一种新的、更为分散的计算资源部署，以支持数据密集型、低延迟的 6G 服务。物理计算资源可以集中在数据中心或分布在边缘。服务提供商可以直接操作计算资源，也可以将其外包给另一个（例如云）服务提供商。服务提供商可以在这些计算资源中为自己的服务部署虚拟网络功能（VNFs），也可以将其提供给其他服务提供商。针对更低延迟的 6G 服务通常需要额外的边缘计算资源。管理分散的 6G 计算资源将成为为提供数据密集型、低延迟的 6G 服务的服务提供商的必要操作技能。

### 6G 服务管理

在 6G 无线网络上提供的服务范围预计将比现有网络上提供的服务种类更多。每种服务都需要有网络管理支持，以管理支持服务的组件的生命周期以及服务实例和客户操作。除了生命周期操作外，还需要保证所提供的服务的质量。这需要适当的服务特定指标和测量技术。管理基于连接的通信服务（例如以太网、互联网）对于大多数服务提供商来说是日常业务。这些服务主要需要合作伙伴来协助范围和市场覆盖范围的规模。更复杂的、数据密集型的服务可能需要额外的合作伙伴来提供必要的功能。扩展交付可能还需要额外的合作伙伴来提供适当的市场覆盖范围。6G 服务的管理需要在更为复杂的商业环境中支持更复杂的服务，并在服务和基础设施规模扩展时有效地执行。

行业垂直服务（零售、制造 4.0、医疗 4.0）提供针对特定行业优化的定制网络配置。这些配置通常包括符合行业特定指南的额外设计和保障方面。随着 5G 垂直和物联网范式的出现，边缘计算已成为最主要的服务交付架构，将增强计算资源置于最终用户附近。边缘云的资源编排依赖于网络切片的概念，该概念提供逻辑上隔离的计算和网络资源。跨域基础设施或多管理员域的编排仍然是一个开放性挑战。参考[25]提出了一个基于区块链的服务编排器，利用智能合约的自动化能力在不同租户的网络切片之间建立跨服务通信。他们还介绍了基于区块链的网络市场的多层架构，并设计了跨服务编排的生命周期。通过为行业垂直服务定制服务，服务提供商在管理更多、更复杂服务的代价上提供了更大的价值。由于这些行业垂直服务不是共置的，基础设施必然变得更加分散和去中心化。行业垂直服务意味着服务提供商需要交付这些服务的网络管理任务的规模、复杂度和分散化增加。图 1 说明了服务提供商关系的复杂性增加。在图 1a 中，客户与服务提供商的关系是主要关注点，但这假定单个服务提供商能够满足客户的需求。对于更全球化的服务（例如，互联网），需要跨多个服务提供商进行合作，这通常通过服务提供商手动策划一组商业关系来实现，然后将这些关系对消费者进行掩盖，如图 1b 所示。随着服务类型的多样化（具有更多类型的服务提供商）和动态化（例如，交易而非订阅），商业信任关系变得更加复杂和动态。新兴的众包基础设施（例如 Helium 网络，[`www.helium.com`](https://www.helium.com)）提供了服务提供商种类日益增多的早期示例（如图 1c 所示），服务使用者需要与之互动。![](img/517376_1_En_3_Fig1_HTML.png)

它展示了服务提供商关系模型的不断复杂化（a）客户与服务提供商的关系是主要关注点。（b）服务提供商手动策划了一组商业关系。（c）提供了服务提供商类型增加的早期例子。

图 1

服务提供商关系模型

受信任服务的管理（身份服务、可信计算、隐私服务）既需要理解适当的信任模型，也需要了解对这些模型的威胁。这些服务主要涉及对数据和其他资源的访问。这些服务通常还依赖于其他服务伙伴提供特定功能，例如特定的数据集和工具。随着预期在 6G 无线网络中物联网设备的主导地位，物联网数据的可信度将成为一个重大挑战。对于物联网环境中的服务管理，对信任计算的工作很少。物联网设备的拥有者在系统中为其他物联网设备提供服务的不端行为似乎是一个特别值得关注的问题。参考[26]根据信任计算模型的五个基本设计维度对物联网系统中的服务管理现有信任计算模型进行了分类：信任组合、信任传播、信任聚合、信任更新和信任形成。为了应对网络安全威胁，大多数 6G 服务将需要在零信任环境中提供交付。在大多数 6G 服务调用时商业关系的多样性和动态性要求基础设施提供自动化协议来建立和维护这些商业关系的基础信任。

由 6G（例如触觉）独特启用的 6G 服务的管理通常需要特定的 I/O 设备用于人机界面。这些服务的新人机 I/O 设备将需要管理以确保正常运行。许多 5G 和 6G 服务也为机器提供——例如，物联网设备。对于机器用户的服务保障任务与对人类用户的任务质量上有所不同。举个简单的例子，机器通常不会打电话给服务提供商的帮助台寻求帮助。虽然服务提供商力图最小化可能导致人类打电话寻求帮助的问题，但在规模上识别和解决机器用户的问题是一项更加困难的任务。由 6G 独特启用的新服务将需要管理。这可能需要零触摸管理以实现运营规模和消费者易用性；但在零信任环境中也将需要增加管理功能。

## 3 分散式网络管理技术和架构的演变

分布式网络管理方法引起了研究人员的日益关注。在 1997 年，Baldi 等人[27]认识到了网络管理中集中式客户端-服务器架构的僵化性，但他们通过强调代码移动性作为设计范式来解决分布式网络管理问题。执行网络管理任务的移动代理分配了部分数据收集带宽和数据处理，但没有提供被管理的网络资源和服务的统一视图。在 2009 年，Brunner 等人[28]提出了一种概率范式来进行分布式网络管理。这种概率方法旨在减少与网络数据收集和分析相关的网络资源，但即使是作者对这种方法的可接受性也持怀疑态度，因为网络运营商通常习惯于更确定性的网络管理系统，同时也因基础设施故障而面临监管处罚的风险。

基于策略的管理已经在许多网络中部署，以提供对网络资源的更高级别抽象。虽然基于策略的管理并不新鲜[29]，但最近基于策略的管理的趋势是捕获和结构化政策以捕获运营意图。很少有工作从经验上分析网络管理实践，以便创建和维护政策。参考[30]对网络管理员进行了半结构化访谈，以确定网络策略的维度，包括用户、设备、地点、流量特征、物理位置、时间性、认证和触发操作。最近的基于策略的网络管理工作主要是针对使用特定于领域的声明性语言来捕获政策。这一趋势加剧了从 2012 年开始网络运营商及其许多客户的数字化转型和虚拟化努力，导致通信服务的软件定义基础设施，基于虚拟化网络功能。Valocchi 等人[31]提出了在虚拟化网络功能和软件定义网络基础设施背景下，认识到集中式网络管理的增加复杂性的提议。他们提出了一种支持虚拟化通信基础设施的分布式管理和控制的信令框架。虽然这种方法将工作负载分配给了本地控制器，但缺乏区块链的一致资源视图机制，特别是共享资源。基于策略的网络管理方法仍然是发展必要的抽象以管理现代通信基础设施的规模和多样性的重要策略。

无线应用的爆炸式增长为超越固定无线的新网络架构提供了动力。诸如点对点网络、移动自组网、延迟容忍网络和普适计算网络等新网络架构。其中许多网络架构是分布式和自组织的，一些人将其称为自治网络[32]。网络中的自治通常与人工智能的使用混为一谈，尤其是运行时学习行为[33]。尽管人工智能在近年取得了重大进展，但认知自主网络还有几个需要进一步研究的领域[34]。衡量自治的各个维度并不是一项简单的任务，因为这些维度通常是从社会或心理学研究人类行为中得出的，而不是从大多数网络工程的物理学中得出的。一些区块链结构，如去中心化自治组织（DAOs），被设计为自主运行[35]。自治网络正从研究课题逐渐发展为商业服务提供商之间的产业化[36]。操作和管理 5G 及其后网络的复杂性加强了网络和服务管理运营闭环自动化的趋势。ETSI 零接触网络和服务管理（ZSM）框架被设想为下一代管理系统，旨在自动执行所有运营过程和任务[37]。基于人工智能的方法被认为是实现这些架构的可能实施技术。这种 ZSM 架构已经在无线网络中提出[38]。零信任网络将网络安全范式从静态的基于网络的边界转移到关注用户、资产和资源上。零信任假设不再仅仅基于资产或用户账户的物理或网络位置（即本地区域网络与互联网）或基于资产所有权（企业或个人所有）而隐含信任。在与资源建立会话之前，进行身份验证和授权（主体和设备）是分离的功能。已经有为 5G 医疗应用提出零信任架构的提议[39]。这些架构趋势朝向*自治*、*零接触*和*零信任*，预计会继续作为对网络要求的响应。区块链基础设施似乎提供了一种解决这些要求的方法。

Maksymyuk 等人 [40] 提出了在共享未授权的 5G 频谱和基础设施的背景下，利用区块链机制进行智能网络管理的方法。这种方法依赖于对应于正在被管理的未授权频谱资源的 180 kHz 的新型区块链代币。这种方法并未解决 5G 和 6G 中的网络管理挑战的广度，也没有考虑到可能是非合作的其他未授权频谱的用户。在关于区块链与 5G 融合的更广泛调查中，Nguyen、Pathirana、Ding 和 Seneviratne [41] 确定了区块链在 5G 使能技术（如 NFV-SDN）、5G 服务和 5G IoT 应用中的角色。区块链在其中扮演的管理角色包括频谱管理、干扰管理和资源管理。[42] 对与区块链在 5G 及更高网络中集成的一系列想法进行了广泛调查，涉及诸如互操作性、安全性、移动性、资源分配、资源共享和管理、能源效率等问题以及其他可取特性，并提出了将区块链分类为网络管理、计算管理、通信管理、安全性和隐私、应用和服务的分类法。这种分类法反映了网络管理的非常狭窄的范围（仅限于 SDN、NFV 和网络切片），而许多其他确定的类别也涉及到运营、管理、维护和配置基础设施，以满足运营商的业务目标。在比较不同的网络管理架构方法时，适用的度量标准有助于比较不同解决方案的有效性。Wang Lu 等人 [43] 提供了一个在特定集中式和去中心化网络管理架构背景下比较操作质量的评估的例子。不幸的是，他们选择的去中心化方法基于传统的地理层次结构，而不是区块链。运营商对于在软件和设备故障以及网络攻击中保持业务连续性的同时确保对数据、操作和商业交易的信任的需求增加，进一步激发了基于区块链的方法的动机。

虽然有关区块链用例的提案，但成功应用该技术需要适当的设计技术。应用功能需要在区块链系统和其他组件之间进行分配。Crowcroft [44] 建议在选择区块链之前考虑性能要求（例如，交易吞吐量、延迟），因为其他架构具有更高的交易性能。使用区块链的大规模应用可能会将重要的计算和存储任务移至链下 [45]。其他人 [46–48] 提出了更严格的方法来选择与应用特性和要求相匹配的适当区块链。在了解应用需求和特性之后，可以评估各种替代区块链基础设施在权限控制与无权限控制架构、共识机制选择、性能目标和扩展考虑等方面提供的支持程度。区块链使用分布式账本记录代币交易。设计考虑需要包括代币的生命周期和这些代币与基础资产之间的绑定机制。在去中心化网络管理的背景下，这些代币要么与被管理的网络资产相关联，要么网络管理任务变成了管理区块链本身。设计模式的使用是工程中的常见做法。网络架构的设计模式比网络管理设计模式更常见地讨论。[49] 讨论了用于 NMIs 的 API 和应用框架的需要，描述并说明了 Layla 框架基础的模式系统，详细介绍了其三个关键模式，并对模式系统进行了分析。也开始出现了基于区块链的应用的设计模式 [50–52]。在部署用于信任保证的区块链的情况下，还需要业务和信任模型的设计模式。协作业务流程的信任模式也开始出现 [53]。尽管区块链展现出了相当大的潜力，但在网络环境中商业实践仍需要进一步的成熟。鉴于提案的众多，合理地预期技术和设计实践在 6G 部署时成熟是合理的。

使用区块链部署分散式网络管理解决方案是一种商业决策，而不仅仅是技术上的决定。部署的商业评估考虑的不仅是技术设计选择，还包括公司交付、运营和维护解决方案的能力评估。准备模型[54]或成熟度模型[55]已被用于衡量组织对变革性技术部署的准备程度。区块链网络管理系统肯定是一种变革性技术部署，但我不知道有哪些被广泛接受的用于支持区块链部署的组织准备就绪的成熟度模型。区块链软件工程是一个新兴的技术专业领域，目前还没有形成行业共识，关于所需的技术技能、教育和经验。从商业角度看，确定和配备适当的技术能力是成功部署区块链解决方案所需的组织成熟度的重要前提条件。许多区块链解决方案依赖于开源区块链软件。在这种情况下，还需要考虑支持开源区块链的社区的成熟度。对组织准备度和成熟度的商业判断对于成功部署网络区块链至关重要。

## 6G 网络管理的经济模型

经济模型意味着存在市场，有买家和卖家进行交易，本例中是网络管理服务。大多数区块链被设计为支持分布式账本中记录的交易。对于 6G 网络管理市场的经济模型进行分类的一种方法是将市场的结构与服务提供商的组织边界进行比较。在这里，我们可以区分单个服务提供商内部的市场；单个服务提供商提供其服务的市场；以及多个服务提供商作为买家和卖家运营的通信资源市场。

内部市场可以存在于服务提供商内部的网络管理服务中。基于监管、税收和其他业务原因，服务提供商可能选择将自己组织成多个内部组织，彼此提供服务。例如，一个企业控股公司可能在不同的司法管辖区内运营多个法人实体；或者组建不同的组织来营销特定服务。内部市场通常是集中的而不是分散的。因为它都是同一家公司，所以建立信任的协议需要的程度较少。

最近出现了一种趋势，即运营商的通信 API、产品和服务通过数字市场向外部用户提供。虽然这为人类用户提供了一种替代渠道，但这些数字市场对于机器用户来说变得至关重要。当今许多网络服务产品主要面向的是大型企业或政府，而不是消费者市场。例如，考虑一个在不同服务提供商的地理覆盖区域之间移动的连接车辆。更具未来感的情景可能是一个依赖底层通信基础设施的 DAO，周期性地重新竞标通信服务，以优化其持续的业务成本。在这样的数字市场背景下，多个参与者正在购买或销售网络服务，这就需要一些机制来支持这些交易的可信度。服务提供商之间的结算已经是漫游语音服务的常见活动。工业机构一直在制定标准[16]和开源实现[17]区块链，以支持这些结算。这通过消除用于结算活动的外部结算中心提供了一些运营效率。这种结算安排也可以被视为一种数字市场的一种类型。

不同类型的市场有各种各样的。共享资源市场通常根据资源的类型进行分隔。集中式云和边缘计算中的计算资源都可以使用市场进行分配。并不是所有的经济模型都能为用户在利用资源方面提供相同的好处；也不是所有的资源提供者都能获得相同的利润。经济模型可以在通常由不同组织拥有的大规模异构资源的协作使用方面发挥作用。经济模型可能彼此不同，因为它们用于用户和提供者之间的互动；它们用于定价，并且它们会根据不同的需求进行调整。[57]研究了在网格计算环境中分配资源的各种市场模型，包括商品市场、双向拍卖、英国拍卖、讨价还价、按比例共享、按比例资源共享、第一价格密封竞标和合同网络协议。网络资源或服务的市场可以使用任何这些方法，当然，要受到监管约束。

区块链技术可以降低交易成本，产生分布式信任并赋予去中心化平台权力。这些去中心化平台可能为新颖的去中心化商业模式提供基础。在金融行业中，去中心化金融服务往往更为去中心化、创新、互操作、无边界和透明。[58]确定了去中心化金融商业模式：去中心化货币、去中心化支付服务、去中心化筹资和去中心化合同。并非所有网络管理功能都具有金融方面，但在 6G 时代预期的服务分散化情况下，增加对不同服务和资源市场的使用是合理的。区块链系统的经济学和运作在许可（联盟）和无许可（公共）区块链基础设施之间可能存在显著差异。在网络环境中，不同的市场可能需要不同的区块链功能。用于服务提供商之间结算的市场可能参与者较少，并且倾向于采用许可的联盟区块链。基于区块链的消费者网络服务市场可能更适合于公共、无许可的区块链。

区块链使用代币进行交易。去中心化金融应用程序依赖代币作为金融资产的形式（例如，加密货币、证券或商品）。作为金融资产的代币意味着相应的金融资产监管对待。电信行业的结算应用可能使用现有的金融加密货币，但也可以设计为使用一些其他更具行业特定使用度量的形式（例如，通话数据记录、使用分钟和带宽）。用于其他更新颖应用（例如，频谱共享）的代币也可以被创建。代币的生命周期操作（例如，创建、删除、分区和转移）可以显著影响代币的经济意义。区块链代币的监管分类仍在不断发展中。对代币的无意分类可能会产生重大的意想不到的商业后果（例如，税收或报告负担）。

## 5 智能合约和 API 在去中心化网络管理中的作用

智能合约是在分散式区块链中执行的程序，允许它们利用底层区块链的共识机制来提供具有一定程度的抗失败、篡改和审查尝试的计算结果。虽然有几个区块链支持智能合约，但这样做的成本是需要支持这些智能合约所需的内部带宽、块存储和计算资源。在许多情况下，可以使用链下计算或存储来提高效率，区块链主要用于存储计算结果的签名。请注意，链下计算可能具有额外的要求（例如，用于保护端到端服务保证目标的机密计算技术）。智能合约最初是在去中心化金融应用的背景下提出的，在那里它们可以自动执行部分金融合同。智能合约不是自动激活的；它们只对区块链上的交易做出响应。预言机需要将链下事件引入区块链上下文。在网络管理的背景下，要监视的事件数量和要控制的链下设备的数量显著大于通常用于标准化金融合同（例如，期权合同）的数据系列。智能合约在数字资产上运行，这些数字资产由底层区块链支持。这些代币可以与实物资产或其他数字资产相关联。文献越来越多地展示了区块链智能合约用于网络应用的示例。

智能合约文献评述反映了最初对去中心化金融应用的关注。智能合约应用于物联网已经成为一个重要的研究领域，并具有网络管理的影响。智能合约通常特定于它们预期执行的区块链架构。以太坊是智能合约文献中被引用最频繁的区块链，但也有其他区块链（例如，IOTA）更专注于物联网应用[59]。智能合约已被提出用于各种与网络相关的任务。这些包括频谱感知[60]、DDoS 缓解[61]、分布式云存储[62]、VANETS[63]、软件定义网络[64]和资源分配[65]。这些区块链智能合约的网络应用越来越多地依赖于非金融代币，即与网络资源而不是金融资产相关联的代币。

智能合约是为了在金融合同的背景下提供一些金融条款的自动执行而开发的，但网络运营商对自动化并不陌生。 作为一种计算机制，智能合约由于分散化和共识机制而效率显著低下。 这种效率是通过共识过程中可用的信任断言进行权衡的。 金融行业的一个常见设计模式是在去中心化的结算中使用智能合约，而不是集中的清算中心。 这种结算安排当然已经存在于服务提供商之间。 其他需要强大信任基础的去中心化应用程序和设计模式也开始在网络环境中出现。 服务合作伙伴的多样性增加，以及通过 API 调用服务的趋势，都需要更多的自动化机制来确保交易的信任。 零信任架构的趋势也支持去中心化身份和授权服务，可以通过智能合约调用。 在 IoT 规模的网络中应用零信任架构进一步推动了建立信任关系的自动化机制。 支持独立实体之间的受信任的网络交易的自动化大规模机制的需求，为预期更广泛地部署智能合约奠定了基础。

## 6 人工智能在去中心化网络管理中的作用

将人工智能应用于网络管理问题并非一种新的方法[66, 67]。 计算基础设施、数据科学和人工智能技术的进步已经足够成熟，以至于标准机构已经开始通过架构和更详细的规范来应对网络管理应用。 这些规范为进一步的产业化和在运营商网络中的部署提供了基础。 值得注意的是，网络管理任务的范围也在从故障识别和分类扩展到闭环控制，其中 AI 系统根据一组策略指令来优化资源使用[68]。 一个完全运作且高效的 5G 网络不能没有人工智能软件的加入。 现有的 4G 网络运营基于一种被动的概念，导致频谱的效率低下。 人工智能及其子类别如机器学习和深度学习已经发展到这样一个程度，以至于这种机制使得 5G 无线网络能够进行预测和主动响应[69]。 可以预期，6G 网络将在较早部署的基础上构建 AI 部署，并在更广泛的网络管理任务中部署 AI。

6G 网络不仅转换和传输大量客户数据，还有可能为网络管理目的生成大量数据。AI 技术，特别是 ML，有可能通过涉及大量数据来有效解决非结构化和看似棘手的问题。AI 角色在学习系统中作为优化机制被充分认可。AI 在无线领域的应用正在从大规模、集中的优化转变为具有更好终端用户整体性能的更独立的本地化优化。网络管理正在从基于模型的优化转变为使用在线软件化网络编排、NFV-SDN 和积极的无线网络优化的数据驱动网络优化。[70] 对无线网络设计和优化的不同方面的 AI 应用进行了调查，包括信道测量、建模、估计、物理层研究和网络管理与优化。AI 部署的应用类型正在从分类转变为运行时操作。6G 网络传输和生成的海量数据为影响网络管理的创造性 AI 设计创造了机会。

人工智能（AI）和机器学习（ML）最近在学术界和工业界已经发展了解决多个领域非常复杂问题的以下方面。[71] 对 SDN 和基于 NFV 的网络中 AI/ML 的主要应用领域进行了调查。预计 AI/ML 将成为部署自配置、自适应和自管理网络的关键技术。实现这一潜力的挑战包括计算复杂性和延迟、计算资源需求、对数据资源的访问以及网络管理数据的存档存储。多个行业机构正在致力于网络的 AI/ML，包括 3GPP、5G PPP、FuTURE、ITU 和 TIP。AI 系统操作标准开始出现，例如[72]，但这些标准尚未经过大量不同操作经验的考验。随着技术进入服务提供商的大规模部署，AI 运营正在成为一个专业领域。

## 区块链去中心化网络管理面临的 7 个挑战

服务提供商面临的历史挑战集中在部署连接性和带宽上。光纤技术提高了骨干带宽，而增加的蜂窝覆盖范围将连接性带给了更广泛的人口。网络运营商在基础设施中巧妙地管理了多个技术过渡——1G（模拟）- > 2G（数字）、2G（电路）- > 3G（数据包）和 3G（语音）- > 4G（视频）。5G 标志着更为根本的转变，以满足多种用例的不同要求。这些要求包括超可靠低延迟通信、大规模机器类型通信和增强移动宽带。从人类使用手机为主 - > 物联网设备，4G - > 5G 将基础设施从物理 - > 虚拟化，并主要用途从人类使用手机 - > 物联网设备。一些技术，如软件定义网络、网络功能虚拟化、机器学习和云计算，正在被整合到 5G 网络中，以满足这些多样化的需求。然而，这些技术也带来了与分权、透明度、互操作性、隐私和安全性相关的几个挑战。为了解决这些问题，区块链作为一个潜在解决方案出现了，因为它具有分布式架构的能力，包括透明度、数据加密、可审计性和不可变性。从服务的多样性到支持的挑战，5G - > 6G 的过渡承诺着额外的挑战，无论是对人类用户还是机器用户。

通信基础设施的运营是一个具有显著规模效应的业务。随着规模的增长，网络的价值规模增加，成本和管理复杂性也随之增加。在 6G 时代，随着运营商努力通过越来越动态和多样化的服务交付价值，同时管理基础设施的成本，规模化演进仍然是一个问题。将功能分散到边缘（例如边缘计算）加剧了这一挑战，因为它增加了操作任务需要执行的位置数量。虽然许多网络功能的虚拟化实现了更自动化的网络管理，但仍然存在着显著的规模影响。考虑到管理虚拟网络功能（VNFs）的软件更新所涉及的问题规模。典型的 VNF 可能具有支持每 6 个月进行更新的开发生命周期，如果发现安全问题，可能会在更频繁的间隔进行一些紧急修补。对于支持不同服务的 100 种不同类型的 VNF 的边缘节点来说，这意味着在 VNF 类型上进行软件更新操作的平均间隔为 < 2 天。如果每种 VNF 类型在边缘计算节点上有 100 个运行实例，那么更新实例之间的平均间隔为 < 1/2 小时。对于分布在基站旁边的国家级运营商，例如有 10,000 个边缘节点的规模，维护基础设施的最新版本所需的自动化规模变得明显。这还没有考虑到移动、添加和更改的额外行政负担，或者新服务的部署。所需的自动化水平越来越多地受到人工智能的推动。规模化管理人工智能操作是运营商需要开发的新能力。各种区块链架构在规模化方面的性能是区块链研究的一个持续领域。对网络运营商的挑战来自于基础设施的多样性——例如，用于结算的区块链可能不使用与用于物联网设备的区块链相同的底层技术。运营商可能需要管理多个不同的分散式基础设施，以支持不同的网络和业务功能。

服务需求的多样性给服务提供商带来了挑战。他们应该尝试“覆盖所有领域”，即保持对不同服务的广泛覆盖，作为一个“一站式购物”；还是专注于一个或多个利基，冒着它们被商品化或受到需求变化的风险？随着需要管理的服务数量增加，网络管理挑战加剧。许多通信服务需要广泛的地理覆盖。全球化趋势和最近的流行病突显了远程工作能力的重要性，通常跨越多个时区。没有单一的服务提供商有能力满足所需的地理范围，因此需要服务提供商之间的商业关系来提供所需的功能。服务需求的多样性增加了管理这些商业关系的挑战——例如，并非所有服务提供商都能够在商业决策中提供所有服务，这些决策基于他们的资源、监管环境、竞争压力等。服务需求多样性增加了网络管理任务的复杂性，因为这些服务变得更加分散化。

业务模式推动基础设施和服务的部署，并将在 6G 中再次如此。业务模式的多样性已经在现有网络中增加。考虑到不提供自己基础设施的服务提供商的崛起，例如虚拟移动网络运营商。 5G 无线特性和服务专业化有利于密集化和本地化部署策略。私人地主可能具有更好的商业可见性，以推动特定场所的 5G 部署，例如娱乐、制造和医疗校园。诸如 AR/VR 和智能环境之类的复杂服务本质上非常局部化，并强调了边缘计算的需求，以将服务延迟降低到可察觉的限制以下。延迟不是唯一关注的性能指标，但它确实给许多通用区块链系统带来了挑战。6G 背景下的频谱可用性和服务多样化可能加剧这些趋势，导致 6G 部署位置和业务模式的多样性增加。因此，服务提供商面临着在这种环境中组建端到端服务的挑战。这种 6G 基础设施部署模型的多样性增加了网络管理挑战。

消费者对通信服务的期望正在从服务可用性转向服务的可信度。现代社会对个人、企业和政府访问互联网数据和计算机系统的依赖性突显了当这些系统和数据受到威胁时的各种不同威胁。个人数据可能因隐私侵犯而被用于商业收益或公开羞辱。通过篡改数据可能破坏各种社会过程的诚信。对数据来源进行审查也可能通过选择性删除数据访问而提供隐性偏见。信任、隐私、审查抵抗等的模型和指标仍在不断发展。其中许多是基于特定技术而不是更广泛的法律概念的隐私、信任、审查等。如果没有适当的度量和测量技术，将难以设计和运营通信基础设施以在这些方面提供保证。网络管理和控制操作将需要在这些领域取得进一步进展，以支持 6G 基础设施和服务，以满足不断发展的消费者对数据可信度的期望。

IoT 流量在部署了数十亿设备并将它们作为 5G 的一部分部署的新网络服务的重要性日益凸显。预计在 6G 中，针对额外类型的机器用户通信服务的 IoT 流量来源和服务将进一步扩展。已经提出区块链作为支持 IoT 基础设施完整性的机制，而 IoT 基础设施的规模仍然是网络管理的挑战。充分设计和运营此类区块链系统需要理解这些区块链系统需要防范的威胁模型。[73] 对潜在的安全攻击进行了详细分析，并提出了可部署为应对此类攻击的现有区块链解决方案，包括区块链安全增强解决方案。确定的区块链安全问题包括交易篡改、网络安全、隐私、冗余、法规合规、犯罪活动以及智能合约的漏洞。IoT 基础设施的规模是网络管理的挑战，推动了对零接触网络管理能力的需求。这样大规模分布式 IoT 基础设施的网络安全挑战推动了朝向零信任机制，以识别受损设备并限制进一步传播范围。

当今基础设施的网络安全能力是在当代冯·诺依曼计算机架构的背景下使用密码学进行开发的。然而，6G 时代预计将于 2030 年代开始。届时，量子计算技术将威胁许多当前密码算法的完整性。量子霸权指的是使用量子计算机解决经典计算机无法在合理时间内解决的问题的目标。已有多个研究团队声称已经实现了量子霸权的示例。虽然当前量子计算能力可能受限，但到 2030 年可以预期量子计算技术将取得可观进展。依赖密码学的网络管理，包括区块链，将需要转向后量子密码方法。这可能意味着对早期行动者而言需要更新密码软件，增加额外成本。然而，需要后量子密码方法的问题并不局限于区块链。预计网络安全将继续是网络管理的一个具有挑战性的部分，即使在去中心化的情况下也是如此。

区块链为在去中心化架构中执行业务逻辑代码的智能合约提供了基础设施。在这种情况下，执行结果有一个基于执行节点共识达成的信任基础。智能合约可以被视为一种分布式计算；然而，支持该领域专业实践的软件工程知识体系仍在形成中。随着区块链在各种环境中的部署和运行，预计区块链软件工程的设计模式和其他实践将得到发展。在多方环境中，解决数据语义的标准化和系统的操作治理是重要的问题。通信行业习惯于开发行业标准以支持此类倡议。区块链使用预言机将离链的外部数据源和控制适应其分布式架构。独立的预言机作为可信数据源可能是某些服务所需的新型业务伙伴。[74]提出了一种基于数据源、信任模型、设计模式和交互模式分类区块链预言机的分类法。商业角色和责任可能会更具挑战性，因为去中心化架构通常意味着业务流程的重大重新工程。在将现有运营服务迁移到区块链基础设施上的智能合约期间，协调跨多方的这种过程重新工程对许多运营商来说可能是具有挑战性的。

## 结论

区块链技术启用的去中心化网络管理是对现有网络管理流程的一场颠覆性变革。20 世纪 30 年代及以后的 6G 网络管理挑战的范围和规模支持这类网络管理架构的需求。从技术和商业角度来看，2030 年代及以后的 6G 时代的网络环境预计将比当前的通信网络更加复杂。随着机器使用主导人类使用，所提供的服务及其调用方法变得更加以数据为中心。即使对于人类用户，网络安全威胁也会带来对服务保障的需求，确保数据可信、私密且抵御审查攻击。在 6G 商业环境中，服务碎片化、资源多样性以及由此产生的复杂性强化了自动化协议的需求，以支持大规模网络范围内的可信交易。人工智能技术在管理网络管理数据收集和分析问题的规模方面表现出了潜力。区块链技术也显示出了作为可信交易和抵制审查数据的启用技术的潜力。在这些技术更广泛应用之前，仍然存在技术、商业或组织上的挑战。区块链技术启用的去中心化网络管理为考虑 6G 通信基础设施中预期出现的运营和管理挑战提供了一个有前景的框架。
