© 作者，独家许可给施普林格自然瑞士公司 2021Y。Maleh 等人（编辑）未来网络安全应用的人工智能和区块链大数据研究[`doi.org/10.1007/978-3-030-74575-2_17`](https://doi.org/10.1007/978-3-030-74575-2_17)

# 网络安全分析：调查 AWS 和 Azure 云平台中的数据完整性和隐私

Sivaranjith Galiveeti^(1  ), Lo’ai Tawalbeh^(2  ), Mais Tawalbeh^(3  ) and Ahmed A. Abd El-Latif^(4  )(1)肯塔基州威廉斯堡坎伯兰大学(2)德克萨斯州圣安东尼奥的计算与网络安全系，德克萨斯农工大学(3)约旦伊尔比德科学技术大学计算机工程系(4)埃及舍宾科姆的门努菲耶大学 Sivaranjith Galiveeti 邮箱：sgaliveeti6276@ucumberlands.eduLo’ai Tawalbeh（通讯作者）邮箱：ltawalbeh@tamusa.eduMais Tawalbeh 邮箱：matawalbeh18@cit.just.edu.joAhmed A. Abd El-Latif 邮箱：aabdellatif@nu.edu.eg

## 摘要

在采用现代技术方面，信息技术领域仍然占主导地位。此外，各种领域和行业对技术的采用不断增加。其中一种迅速崛起的技术就是云计算的发展。如今，云平台受到大量用户和组织的追捧，以利用其操作和生产力。这项技术在 IT 业务领域持续受到更多关注。云平台在支持实时计算方面提供了更大的灵活性，并成为通过互联网提供服务的更为强大的框架。亚马逊云服务（AWS）和微软 Azure 是两个关键的云平台，允许用户将云用作数据存储、访问和检索的源。在全球技术迅速变化的现代时期，AWS 和 Azure 云解决方案被广泛采用作为大规模信息系统的公共存储平台。这两个服务器平台为不同的组织提供了私有、公共、混合和社区服务。

此外，这两种云技术可以升级以防止信息强加。不同的安全功能允许不同的用户为存储和访问数据分配共同的基础。系统评估考虑了各种特性，包括平台独立性、大规模就业、客户需求、安全性、数据大小以及其他相关资产。

这项研究旨在审查云技术中出现的基础设施、平台和数据安全问题，特别是在应用 Azure 和 AWS 时。个人用户和实体希望体验到云技术平台所具有的灵活性和可扩展性。这些客户希望通过迁移到云平台来更快地开发和执行新手应用程序，并降低成本。亚马逊 AWS 和微软 Azure 支持不同的数据库管理系统。云提供商展示了不同的架构、资源管理模式和信息系统增强器的复杂程度，影响着可扩展性、性能和价格。尽管云平台继续提供巨大的数据安全解决方案，但主要挑战限制了它们的增长和应用。未来的研究需要集中精力寻找更强大的解决方案和最佳实践，以保持云数据的安全性和完整性。

## 1 引言

在 IT 领域，使用云平台是一项迅速发展的技术。目前，许多个人和组织在进行日常任务时都在使用云。云平台的常见示例包括 Gmail 和 Microsoft Office 365 [18]。云技术的宣告带来了巨大的好处，包括改善了位置覆盖范围、降低了系统设置成本以及更好的可访问性。然而，这些好处容易受到影响云平台应用的重大限制的影响，例如有限的资源、缺乏技术人员和安全问题。考虑到低维护成本，加上云工具适应性增强，这些技术得到了广泛利用。不同的供应商提供不同的产品。

对于云技术框架，敏感信息是从广泛的领域收集而来 [15]。一个详细的例子是健康数据，这需要高度安全的云计算环境。鉴于近年来云技术的增长，保密和信息保护需求持续转变，从而保护用户免受信息披露和监视。保护性法规要求在处理可识别个人数据时维持保密性 [15]。近年来，已经付出了相当大的努力，以利用各种方法来提高数据隐私性并实现更安全的云解决方案。在提高这些平台更高安全性方面采用的策略的示例包括多方计算、匿名化、真正的解决方案模块和加密 [27]。尽管如此，关于如何适当地开发可用的隐私维护云平台以安全地管理敏感数据仍然存在一个关键挑战。导致出现这些担忧的两个主要方面是现有的隐私和数据保护法律压力以及有限或缺乏对建立强大云技术所必需的不同安全解决方案的了解。

在一个迅速发展的商业环境中应用最新技术方面，信息技术部门仍然占据主导地位。如今，互联网成为一个重要的工具，使不同的用户能够快速共享资源。随着对互联网的需求增加，一个新的网络和计算时代已经爆发，并且目前在云计算领域变得明显 [28]。这些技术已经提升了组织的能力以及用于在各种设备上存储数据的控制机制。作为一个面向服务的框架，云计算包括许多功能，例如，Web 2.0 和分布式分类帐。这些功能使云计算能够为用户提供可伸缩的数据存储能力，并且从任何地理位置更容易地访问资源。本研究关注于云技术服务提供商的数据安全和完整性管理，特别是微软 Azure 和亚马逊 Web 服务（AWS）。

云技术是基于互联网的未来创新形式。云计算为客户提供了可定制和简化的服务，以便访问文档并集成各种云解决方案[25]。通过云技术，用户可以通过互联网连接到相关应用程序，从而在任何地理位置存储和访问云环境中的信息[13]。用户决定选择哪些服务提供商进行信息存储以及存储的信息类型。最近，云技术的吸引人特性加速了信息技术部门对云设置的整合。IT 部门和学术领域都对相关创新进行了广泛的审查。随着简化的支付系统以及按需流程，组织计算模型正在发生转变[12]。企业已经从场内数据库转移到了可通过互联网访问并由云服务提供商控制的场外数据库。虽然云计算由于提供巨大优势而在未来系统中发挥着关键作用，但也带来了安全挑战，并被视为一个发展中的关注点[34]。各种研究都集中在相关的安全问题上。

全球超过 33%的公司将信息存储在云平台上，无论是在私有还是公有平台上[9]。随着企业采用多云设计，恶意攻击者利用现有的易感性导致基础架构配置错误的情况越来越多。一个全面的保护方法可以帮助解决这些多云系统中的威胁，并使企业能够实现与技术相关的收益。包括 Microsoft Azure 和 AWS 在内的云环境，持续为用户提供比其他数据存储环境更多的回报[9]。预计在长期内，随着越来越多的个人和组织继续采用云技术，多云用户数量将迅速增加。

有趣的是，超过 20%的云环境中可用的文档包含敏感数据，例如知识产权[29]。考虑到一个不安全的云平台，这意味着这些机密数据对黑客是可访问的。今天，实体在规定的指导方针和管理信息的规定下运作。根据这样的法律框架，组织必须了解如何访问其数据，谁访问它，以及在此类访问之后采取什么行动[29]。此外，在内部利益相关者（如员工）以不可接受的方式使用数据的情况下，公司可能面临恶意攻击，导致不信任和可能的法律处罚。

业务利益相关者的共识通常限制了数据的使用方式和被允许访问的方。当内部用户在未经认证的情况下在云环境中传输私人数据时，这些协议就会被违反或忽视，从而导致法律程序。随着数据泄露量的增加，客户对云计算的信任减少。采用云技术满足了用户对 IT 资源（包括服务、应用程序和网络）的需求。作为一个基于互联网的框架，云计算提供了检索和使用所需的便利和大量资源[35]。随着越来越多的云平台被采用并集成到系统中，信息安全日益受到关注。这些挑战一直是制约云技术利用的关键因素。未来的研究迫切需要专注于潜在解决方案，以减轻出现的风险和架构挑战。

本章将探讨云技术基础设施、特性、安全性、定价和遵守管理对个人用户选择接受和使用云技术服务平台的影响。此外，我们还调查了云服务基础设施与云技术服务平台接受度之间的联系。更具体地说，在本章中，我们的目标是：

+   确定云服务特性对云技术服务平台接受度的影响。

+   揭示云服务安全与云技术服务平台接受度之间的相关性。

+   揭示云服务定价对云计算采用的影响。

+   确定云服务监管框架是否影响云计算的采用。

该研究的重要性在于它包括隐私、机密性、技术基础设施、监管框架和解决方案。该研究的关键贡献包括：制定一个清晰的框架，以识别存在于云技术中的安全模式；识别与云工具和资源客户面临的安全相关问题以及隐私和机密性问题；提供了该研究领域的现有差距，以及旨在缓解云平台安全风险的潜在解决方案。首先，介绍了云计算和安全问题的概念。接下来，制定了符合性和监管框架，描述了当前云技术的情况。

鉴于对关键解决方案的研究有限，本研究还关注了与云中数据安全相关的不同研究之间的现有差距。基于 Azure 和 AWS 云平台的特点提出了解决方案。其他现代策略，包括整合机器学习，被推荐用于未来的适用性。最后，论文总结了，提出了未来的影响。这项研究的重要性在于通过个人、企业和组织来塑造有关选择高效云技术的决策。这些决策基于满足潜在用户或客户需求的典型特征，包括性能和成本效益，以及帮助云提供商认识到相对于其他竞争解决方案的现有限制。

本章的其余部分组织如下：第二部分介绍了云计算技术的概述，包括其定义、历史和基础设施。此外，它讨论了以往研究中的差距。第三部分研究了几个理论和框架，允许用户洞察如何采纳新技术。在第四部分中，我们讨论了本研究选择的两个流行的云服务平台，亚马逊网络服务和微软 Windows Azure，然后说明了这些平台的应用和优势。第五部分讨论了云计算平台中的安全问题，包括其问题和模式。AWS 和 Windows Azure 提供的最佳数据安全和完整性解决方案在第六部分中提供。最后，第七部分总结了本章，并根据本研究提出了一些建议。

## 2 文献综述

第二节提供了对云计算技术的概述。本研究讨论了其定义、历史、基础设施、主要特征、交付和部署模型、安全模式以及为本研究选择的两个流行的云服务平台。

### 2.1 云计算

全球范围内，随着新的发展成果为个人和组织提供便利，技术采纳以不同方式改变着人们的生活，这些发展成果使个人定期开展活动的方式发生变化 [24]。多年来，各种实体已经设计出更好且成本更低的创新来解决信息存储和可靠性问题，这一术语目前被称为云计算。在 21 世纪初，美国的各种组织开始采用云技术来按需访问服务，并且这一创新在其他国家也得到了采纳 [24]。客户将信息存储并通过网络访问，使用户能够访问云存储区域。由于其快速增长和需求，云技术已经改变了 IT 领域。云计算的快速发展促使了大量数据中心的建设，这些数据中心包含复杂的服务器。

#### 2.1.1 定义

从不同的研究中可以找到云计算的各种定义。然而，普遍接受的定义归因于 NIST，该定义将云计算称为“促进简单、迅速的网络连接到一个独立的 PC 利用资源系统的框架，可以在有限的管理干预或客户干预下分配和释放” [24]。

与传统计算选项相比，区分云计算的主要特点已被认可并通常包括：可扩展性和响应性设施的模式，按需提供服务的购买，云系统资源的使用支付而无需公开忠诚于云客户，相互和多租户，以及通过互联网访问所有设备 [24]。

#### 2.1.2 云技术的历史

云技术在历史上经历了从 1960 年代到当今以及未来的快速变化 [24]。在 1960 年代的后期，被认为是推动 APRANET 发展的人物 J. Licklider 提出了星际计算机网络的概念，类似于今天的互联网 [24]。随后在 1970 年，引入了虚拟化技术，其中包括在受限环境中同时运行不同操作系统的软件，如 VMware。随后，这一发展导致了虚拟机的引入。到了 1990 年，电信公司开始提供 VPN 服务，通过为客户提供对现有架构的共享连接 [24]。在 2000 年代初期，亚马逊成为了云计算的领军者，通过弹性处理云和更简单的存储提供服务。此外，该公司推出了面向个人和组织的“按需付费”框架。在 2000 年代后期，谷歌成为互联网业务领域的主要竞争对手，到 2006 年，该公司推出了其第一个基于云的解决方案，称为 Google Docs；该工具允许用户准确地保存和共享文档 [24]。

### 2.2 云技术的基础设施

国家标准与技术研究所（NIST）作为一个在全球范围内知名的组织，在 IT 领域进行了广泛的研究。该组织对云技术基础设施设计中的五个基本特征、三种服务和四种部署方式进行了典型示例 [24]。

在云计算领域中，存在着五个关键参与者或角色。这些角色包括消费者、服务提供商、审计员、运营商和经纪人[18]。云消费者是在商业连接景观中利用云服务提供商提供的服务的个人或实体。云服务提供商确保相关的云服务可供潜在客户或用户使用。审计员对云服务、安全性以及与云部署相关的流程进行独立评估。从云提供商到客户的云服务的连接和交付是云运营商的责任[15]。经纪人管理云服务的消费、执行和交付，同时促进云提供商和消费者之间的积极关系。所有这些参与方都涉及在云平台上创建和使用数据。在部署方面，类别包括私有、公共、混合和群体平台。

#### 2.2.1 云计算交付模型

在分发服务时，主要平台包括软件即服务、基础设施即服务和平台即服务。

2.2.1.1 软件即服务（SaaS）在软件即服务平台上，所有服务均由服务供应商提供。这些利用模型容易受到安全风险的影响。SaaS 提供服务，用户无需管理任何操作系统的安装和设置。服务提供者执行这些角色。SaaS 的示例包括电子邮件、客户关系管理（CRM）和游戏（图 1）。![../images/507793_1_En_17_Chapter/507793_1_En_17_Fig1_HTML.png](img/507793_1_En_17_Fig1_HTML.png)

图 1

SaaS 模型

2.2.1.2 平台即服务（PaaS）平台即服务工具由服务提供商负责，服务使用者只关注数据和应用程序。PaaS 提供服务使客户能够利用云平台支持的工具和设置开发应用程序。用户还负责管理安装和配置活动。示例包括 Web 服务器和决策支持（图 2）。![../images/507793_1_En_17_Chapter/507793_1_En_17_Fig2_HTML.png](img/507793_1_En_17_Fig2_HTML.png)

图 2

PaaS 模型

2.2.1.3 基础设施即服务（IaaS）基于基础设施即服务，服务提供商负责启用存储、网络和服务器配置。此外，提供者还控制数据、操作系统和应用程序。IaaS 为组织提供了重要的网络设计访问权限，例如服务器，而无需购买和控制互联网设置设施。一个主要的优势是用户只需要支付所消耗的服务的时间。该平台可用于防止购买、存储和管理基本操作系统服务部件，快速地来回测量以满足需求。示例包括服务器和虚拟机。该技术的五个特点是度量服务提供、资源池化、广泛的网络访问、按需自助服务和即时响应（图 3）。![../images/507793_1_En_17_Chapter/507793_1_En_17_Fig3_HTML.png](img/507793_1_En_17_Fig3_HTML.png)

图 3

IaaS 模型

#### 2.2.2 云计算部署模型

在这一部分中，描述了各种云利用模型，包括公共、私有、社区和混合云。

2.2.2.1 公共云这是云服务提供的常规和最常见的方法，在这种方法中，商家或组织通过网络架构提供不同的云服务，特别是 SaaS、IaaS 和 PaaS。每个潜在的客户都可以通过在网络上制作传统应用程序并经历云服务提供商的注册流程来访问他们的云服务。对于部署范例，服务对所有网络客户都是可见的，并且可以同时对许多客户开放。公共云基础设施跨越公共和本地地理边界。服务和控制由提供或出售服务的组织负责。可公开使用的云解决方案的示例包括 Google 的 Google AppEngine，亚马逊的 Amazon Elastic Compute Cloud (EC2)和微软的 Windows Azure Services 平台。服务向客户提供了一些优势，因为客户只需支付他们使用的服务。它可以轻松扩展以满足客户的需求，应用程序和相关的支持成本由云提供商承担（图 4）。![../images/507793_1_En_17_Chapter/507793_1_En_17_Fig4_HTML.png](img/507793_1_En_17_Fig4_HTML.png)

图 4

公共云模型

2.2.2.2 私有云这描述了为多个用户提供托管服务的专有云架构。它通过防火墙与互联网或公共网络隔离，并由特定实体的工作人员访问。它由拥有云基础架构的单一组织构建和管理。实施私有云的优点包括与公司需求相适应的架构和软件，安全策略和实施由组织执行，从而允许一种控制感（图 5）。![../images/507793_1_En_17_Chapter/507793_1_En_17_Fig5_HTML.png](img/507793_1_En_17_Fig5_HTML.png)

图 5

私有云模型

2.2.2.3 社区云在这种设置中，现有的框架由几个协会共同形成网络。通过制定共享管理指南，框架的管理可能由组织之间共享。在某些情况下，控制可能由代表形成社区的企业的外部方进行。社区云模型描述了在组成社区的相关实体之间分享成本的优点，并确保访问相似的数据，使合作变得更简单（图 6）。![../images/507793_1_En_17_Chapter/507793_1_En_17_Fig6_HTML.png](img/507793_1_En_17_Fig6_HTML.png)

图 6

社区云模型

2.2.2.4 混合云该模型涵盖了私有云和公共云。它通常在一个实体建立了一个私有云来提供最机密和基本的服务时使用。此外，混合模型从公共云服务提供商那里重新分配云服务，以提供不太基本的服务。该模型还允许实体在核心服务和相关成本之间达到协调。因此，混合云的使用在最小化公司 IT 架构执行的资本成本方面扮演了重要角色，因为组织所需的部分服务是从公共云供应商重新分配的（图 7）。![../images/507793_1_En_17_Chapter/507793_1_En_17_Fig7_HTML.png](img/507793_1_En_17_Fig7_HTML.png)

图 7

混合云模型

关于部署框架，公共云存在严重的安全问题。这是由于它普遍使用互联网作为连接手段以及其开放特性所致。这意味着针对安全性制定的政策和指南需要针对个体利用模型进行明确定义。总的来说，服务提供商有责任管理云基础架构和这些平台内存储的数据。鉴于这些不同的功能，安全性成为服务提供商和消费者的共同责任（图 8）。![../images/507793_1_En_17_Chapter/507793_1_En_17_Fig8_HTML.png](img/507793_1_En_17_Fig8_HTML.png)

图 8

云计算架构

### 2.3 过去研究中的差距分析

过去的一些研究已经将注意力转向了信息技术的实践视角，通过评估软件即服务框架的实施来利用改进的业务流程，而不是仅仅考虑技术基础设施本身。企业资源规划应用的概念是云计算景观中的一个新想法[6]。ERP 应用允许将不同的业务流程迁移到云平台，并将解决方案定制为可见的独立任务。从这个角度来看，Gerhardter 和 Ortner 的一项研究[14]旨在评估采用软件即服务框架的成功方面。为了确定相关因素，研究人员从传统和现代的视角来考察 ERP 的实施，后者涉及采用云平台来实施企业资源规划策略。

在决定是否利用云技术时，存在许多模型。这些模型探讨了 IT 提供与适当的业务框架之间的关系，以确保成功实施云解决方案[7]。在实施云解决方案时，需要考虑的主要因素包括企业可持续性分类、组织模型联动和服务的可移植性。其他研究侧重于根据单一业务流程确定特定策略，例如涉及组织内供应链活动管理的供应链框架。

对于激励个人或组织采用云技术的因素的澄清知识有限。被认为是推动采用云技术的重要因素之一的主要因素是对信息技术资源的可伸缩性和灵活性的需求，以及对可用资源的最大化需求[6]。在实施云技术之前，成本是一个重要考虑因素，但各种研究已经得出结论，成本并不是任何决策的基本要求。考虑采用云技术所采取的标准时提供了多种理由，研究强调了成本与价值组成部分。对于可能有限资金投入云技术的中小企业来说，了解从采用中获得的确切价值将是决定是否利用该技术的关键因素[7]。从研究中可以看出，云技术被接受的主要因素与技术优势或对成本节省的预期利益相关。在实施云技术之前，需要商业观点。一开始，某些领域通过采用云技术展现出成功的潜力，而其他领域可能需要相当长的时间才能繁荣。根据 Bildosola 等人的研究[6]，需要通过应用展示云技术演进路径的模型来帮助关键利益相关者。此外，每个组织都需要认识到其在云平台内的路径。

根据 Nemade 等人的研究[23]，云用户将持续对技术性能有更高的期望。考虑到 IT 领域数据分发的复杂和不断增长的链，世界各地有许多服务提供商。云计算的概念涉及到在实用软件框架内提升能力的各种工具。微软的 Windows Azure 是云平台工具的一个复杂示例，为其用户提供了巨大的优势。在研究客户利用云技术的概念时，信息质量的问题至关重要。特别是，维持数据质量要求新用户对云技术有积极的体验。今天，初学者占云用户整体人口的相当大比例。

在 ETAM

Windows Azure 容易出现各种问题，这需要有效的解决方案来确保这些平台高度安全。IDC 对首席信息官和 IT 高管进行的一项调查显示，云计算技术的主要问题是安全性[1]。此外，Singh 等人[30]得出结论，云平台中使用的控制措施不够安全。云技术的服务提供商有责任确保数据受到保护。

云工具的使用正在迅速增长。根据 Alam 最近的一项研究[2]，在特定时间内，个人用户至少使用四个应用程序，超过 40% 的商业实体在公共域上运行关键应用程序。尽管云计算的出现，仍然存在重大安全问题，需要供应商识别和评估用途和资源，以可靠地提供服务。在这方面，Alam 的研究[2]认为，误用是数据安全和完整性的主要问题。一个例子是恶意攻击者使用僵尸网络，从而导致恶意软件的创建。这项研究提出了几点建议，包括彻底自查用户网络，以及强有力的身份验证流程。Alam 的研究[2]还着重关注网络接口的脆弱性。服务消费者使用边界与可用的云资源进行互动，这意味着需要对数据处理进行安全的身份验证、确认和监控。

恶意内部人员是组织的另一个主要关注点。由于在聘用验证和可访问性两个公司主要资产方面存在的约束，一个实体容易受到其员工的恶意攻击[2, 19]。因此，由于缺乏或管理不善的监控和管理实践，风险的潜在性增加。防止此类问题的可能解决方案包括可靠的供应链管理，利用更透明的信息安全和控制过程以及报告合规实践。此外，由于共享基础设施，云技术的使用面临着易受攻击的问题。

具体来说，作为服务平台的互联网供应商使用的单个元素与整个云工具或基础设施并不容易协调一致[2, 19]。这意味着供应商必须检查和加强分隔，以确保云应用程序的安全配置。此外，需要一个有效的确认和访问控制流程，以及评估潜在漏洞。最后，云平台面临的一个关键挑战在于数据丢失。由于数据备份不足和用户访问未经验证，导致信息被盗或未经授权检索。如果不采取积极的措施，这将成为企业的重大问题，因为其声誉会受到影响。对于这个问题，可能的解决方法包括在传输过程中保持信息的完整性、使用强密码密钥以及严格控制接口访问。

在他们的研究中，Kofahi 和 Al-Rabadi [17] 指出，企业在采用云技术方面面临的一个主要问题是交付维护整个系统所需的流程和需求，而不是技术本身。从这个角度看，采用云计算后，不再需要硬件专家和员工的服务，利用信息中心，利用团队可以对硬件进行简要概述。在云计算中，关于数据安全问题以及完全控制相关威胁的最佳实践存在普遍的不一致性。未来的研究涉及云技术易感性以及调查防止此类问题的明确策略至关重要。

另外，Das 等人最近的一项研究 [8] 对边缘计算作为解决云技术问题的有效技术模型的概念进行了研究。在该框架中，引入了一个称为边缘计算层的新层，以补充传统的计算模型。只有实际的信息处理被传递到该层，其他复杂的过程在云平台上实施 [8]。总的来说，边缘 IT 系统包括消费者设备、云服务器和边缘计算层。

鉴于信息的分布性和在不同层次上任务的集成，安全性能和保密性方面存在重大问题。人工智能工具广泛应用于边缘计算事件。这些技术被用于补充这三层，并增加数据存储和网络容量。边缘框架通常用于自动驾驶汽车、监控摄像头和智能城市 [8]。事件复杂，因为存在各种客户设备、数据的更大异构性以及隐私和安全问题。

此外，事件对网络带宽和延迟提出了重要需求。边缘计算系统目前处于初期阶段，并缺乏此类事件的通用标准。这需要一个全面的计算基准集合，可用于测量和增强应用程序。边缘框架的测试能力不足，并且由于隐私顾虑，缺乏分享信息的诱因。这些复杂性意味着未来的研究需要开发全面的端到端应用程序事件，验证或确认特定环境中应用的体系结构和算法。

## 3 种技术采纳理论

对于决策者来说，理解影响用户接受某一技术系统的判断的流行问题变得至关重要[32]。这样的理解可以帮助开发者集中在系统的开发阶段。在这方面，研究人员和从业者的一个主要问题是为什么个人和组织会采用新技术？通过回答这个问题，决策者可以确定改进的设计评估方法，并预测用户对新创新的响应。技术接受范式已被应用于各个领域，以更清晰地了解用户及其行为。已建立了几个框架，以允许了解用户对新技术的采纳。

### 3.1 理性行为理论（TRA）

最初，TRA 是由 Fishbeine 和 Azjen 于 1975 年为社会学和心理学研究而制定的。最近，该模型已用于检验使用信息技术的采用行为。从这个角度来看，非人类行为被预测并描述了三个主要的认知元素：态度、社会价值观和意图。这种个人行为是自愿的，并且以理性的方式进行。通过利用各种方法如上下文和行动，可以增强态度和意愿之间的关系。该模型的一个关键局限性是需要自愿的用户参与来验证该范式的应用。此外，该模型未能回应人类行为调查偏见和道德方面的规则。

### 3.2 技术接受模型（TAM）

TAM 源自 TRA。在 TAM 中，用户规范和偏好的元素被排除在外。在描述用户动机时，该模型考虑了三个主要组成部分，包括感知有用性、感知易用性和采纳态度，其中前两者是主导价值。前者对个人或组织对技术采用的态度产生重要影响。因此，这两个主要元素可以被认为是对技术系统的积极性或消极性。此外，该模型还考虑了外部因素，包括用户的知识和经验、用户系统参与系统设计的特点以及执行活动的特性。该模型已在 IT 领域广泛应用，并获得了相当大的实证支持。

尽管技术接受模型存在一定的限制，因为忽略了技术采用的社会影响。此外，仍然需要向模型中添加外部因素，以提供更一致的 IT 系统采用预测。TAM 中忽略了内部的激励因素，这意味着该模型在客户导向的环境中的利用能力有限，其中对 IT 的接受和利用导致任务的实现和满足用户的情感需求。

### 3.3 TAM 的扩展（ETAM）

在 ETAM 中，TAM2 内的附加变量增强了对原始 TAM 的详细描述和特定性的理解。两项主要研究推荐了 ETAM 的利用。其中一项研究考察了行为意图和感知有用性的原因。对于这个模型，即 TAM2，提出了两类概念，即对 TAM 的认知和社会影响。结果，感知有用性的预测稳健性得到了提高。第二项研究确定了影响感知易用性的概念。感知易用性的原因被归类为修改和锚定。对于前者，考虑了从直接用户体验到给定 IT 系统的价值，而后者则涉及到 IT 系统采用的一般规范。

### 计划行为理论（TPB）

TPB 将感知行为控制作为一个新的方面，扩展了 TRA 范 paradigm。该标准的确定性由技能资产的可用性、感知到的可用资产的重要性以及实现结果的能力。虽然 TRA 和 TPB 都关注个体的行为意愿，但 TPB 模型考虑了对用户行为的感知行为控制，这些行为不能被视为自愿的。因此，计划行为理论模型增加了一个自我效能的元素，并消除了限制。对所述的行为管理的关注直接影响了实际行为，并间接影响了行为违规。

简而言之，计划行为理论旨在影响行为意图的三个关键方面。其中包括感知行为控制、态度和主观信念。使用 TPB 的两个主要限制出现在对其的态度上，如果 IT 系统无法访问，则这可能会非常重要。其次，计划行为理论的修订版本可能更具可行性，作为概念开发的框架，特别是对于影响个体在工作环境中选择采用 IT 的自愿程度方面。

### PC 利用模型

该模型以信息安全视角出发，预测用户接受和 PC 使用。行为意图在 PC 利用模型中被忽略，因为重点是评估实际行为。此外，个人习惯即使与 PC 使用环境中的普遍使用有着总体逻辑联系也被忽略了。PC 利用模型特别关注对用户行为的采用、感知影响、社会因素、复杂性和工作对齐的直接影响。总的来说，就个人电脑使用而言，就业适配、社会因素、长期影响和复杂性都会产生重大影响。然而，加强条件和影响对 IT 相关使用的影响不大。

### 激励模型

内在和外在的激励因素决定了 IT 系统的采用。外在或外部动机涉及用户对实现增值结果的观点，这些结果与特定任务不同，例如提高工作绩效。在这方面，感知有用性被认为是一种外部动机的形式。另一方面，内在动机是指个体希望执行某项活动而没有明显支持的观点，而只是进行任务。在这种情况下，感知乐趣被认为是一种内在动机的形式。总的来说，感知易用性和结果的平等性影响了感知乐趣和有用性。此外，给定活动的价值作为感知易用性和结果质量的调节变量，影响了感知有用性。行为意向受结果的价值和感知易用性的影响。 

### 3.7 技术接受与使用的统一理论（UTAUT）

Venkatesh 和 Morris 制定了 UTAUT 框架，因为他们对 IT 系统领域归因于八种先前的范式进行了对比。这八种模型专注于三个关键领域，包括沟通心理学和社会学。它们包括 TAM、TPB、整合 TAM 和 TPB、TRA、创新扩散、PC 使用理论、动机模型和社会认知范式。对于 UTAUT 范式，已确定了关于采用 IT 结构的预测因素。这些因素是通过匹配从先前的理论基础中得出的原始概念而生成的，包括努力预期、绩效预期、共同影响和启用联系。性别、年龄、熟悉度和采用的深思熟虑程度是 UTAUT 模型中确定的四个额外的调节因素。

### 3.8 兼容性 UTAUT（C-UTAUT）

最初，Agarwal 和 Karahanna 确定了兼容性价值，这些价值被 Bouten 纳入了 UTAUT 模型中。兼容性 UTAUT 模型旨在增强范式的信息能力，并通过识别和检查新的边界背景来提供对模型的认知体验的更深入的了解[32]。该研究旨在探索行为观点和兼容性规范之间的关系，因此，确定采用的实际行为是不必要的。此外，该研究是横断面的，这意味着对行为意向的关注会偏离对回顾性评估的关键问题[32]。

### 3.9 创新扩散（DOI）理论

DOI 模型关注于通过考虑四个影响新概念分发的主要方面来实现各种技术进步：时间、通信渠道、创新和社会系统。DOI 不仅仅适用于个人或组织，而且还允许一种假设框架来检验国际范围内的接受度。创新扩散理论整合了三个主要元素：采用者特征、技术特征和创新决策活动。技术选择决策活动包括验证、洞察力、执行、决策和影响五个主要阶段，这些阶段通过社区结构成员的连续通信路线，在规定的时间内发生。有关创新特征的五个重要因素包括相对优点、兼容性、复杂性、可试验性和可观察性，所有这些因素都影响了技术的接受[32]。有五个采用者特征：早期采纳者、创新者、落后者、早期多数人和晚期多数人。总体而言，创新扩散模型更加强调 IT 系统特征、公司质量和环境因素。此外，相对于其他技术使用理论，它对结果的解释性较弱，对结果的预测较不合理。

### 3.10 社会认知理论

社会认知模型源自社会心理学，并以三个主要因素为基础：行为、气质和环境。这三个方面相互关联，以预测个人和群体行为。从这一范式中，用户行为可以通过确定清晰的方法来修改。该理论将行为视为主要方面，并关注接受、利用和绩效作为此类行为的核心要素[32]。社会认知模型被纳入以利用多个概念来评估 IT 使用，如自我效能、结果期望的绩效、情感、恐惧和个人结果期望。

## 4 云计算服务平台和示例

存在着多种具有巨大益处的云计算解决方案。本研究考虑了两种广泛采用的平台，包括亚马逊网络服务和微软 Windows Azure。

### 4.1 亚马逊网络服务（AWS）

鉴于亚马逊的正面形象和长年的经验，该组织在信息技术，特别是云技术方面继续获得信任。

为了建立信任，该组织在很大程度上专注于遵守设定的安全标准[28]。因此，该公司处于有利地位，可以提供与云相关的服务。亚马逊采取了几项措施，以确保其云服务为客户提供积极的体验。在这方面，一个关键系统是身份访问管理（IAM）框架，公司利用这一框架来管理对其庞大资源的访问[33]。该模型应用于识别、验证和确认组或个人用户，以允许访问其资源。与框架的通用接口控制用户访问密钥、指南和密码。这种框架允许清晰地定义哪个个人被允许访问特定资源。

IAM 模型在几个步骤下运作。首先，个人用户通过使用他们的电子邮件地址和密码注册账户。这种认证给予用户完全访问 AWS 平台上的可用资源和服务[28]。在创建用户账户后，将提供一个确定的密码、访问密钥和用户名，以授予给定用户账户权限。建议使用 IAM 用户功能，以便没有用户能够更改 AWS 平台上的资源。考虑到权限的程度或日常使用情况，可以建立一个用于框架的群组[28]。通过明确的管理指南可以建立这样的群组。这意味着群组的级别应确定权限，而不是个人的程度。结果，用户体验到了改进的访问权限。最小权限的使用也是确保更好的访问控制的关键方法。除了最小权限外，IAM 角色的使用也是有效的，因为这些工具加强了临时安全验证的利用。一个明显的例子是 Amazon S3，它提供了访问指南的备选方案，包括面向用户的指南和面向资源的策略[28]。这意味着用户可以覆盖其他策略，或利用两种策略来确保对可用资源的增强访问权限。

复制版本是用户可以利用的另一个工具，以确保数据随时可用[28]。用户浏览器和控制台端点之间可以通过 AWS 控制台管理系统建立安全连接。此外，亚马逊包括完整性评估，以验证客户或用户请求，同时通过使用多种技术，如数字签名[28]，维护数据的完整性。公司还将多变量验证作为确保设置安全标准最佳实践的手段。多因素认证工具也可以与 IAM 用户账户结合使用，成功地排除用户凭证，涉及将数字代码发送到虚拟或硬件工具中。

### 4.2 Microsoft Windows Azure

同样地，微软是信息技术领域的引领者之一，因为它在提供基于云的解决方案方面非常突出。该组织以其高数据标准而闻名，因为它符合许多与数据安全相关的指南[28]。具体来说，该公司提供了一个个人登录的选择，允许访问大量的应用程序。这个选择是作为一个云定向的目录出现的，被称为 Azure 活动目录或 Azure AD。该目录使应用程序开发人员能够通过建立指南和政策的设置来建立一个共同的身份验证控制。Azure AD 的应用涉及基于规则的访问控制，这涉及允许个人、组或应用程序查看 Azure 平台上可用资源的权限。基于规则的访问控制由管理员提供，管理员监督资源管理活动的存储和授权[28]。在管理员分配了对用户帐户的访问权限后，用户帐户被赋予一个功能。虽然管理员可以管理用户帐户活动的可访问性，但他们不能更改信息对象。对于这样的允许，管理员可以授予查看存储平台访问密钥的权限。

客户可以利用一个共同的访问签名，在规定的时间内获得对某些信息对象的权限。这些签名是一串与网站相关的安全符号，用于启用对存储账户的访问，并且概述了限制条件，例如访问日期[28]。共享密钥是用户可以用来加密存储账户访问密钥和其他需要用户登录的限制的另一种策略。对于这种方法，访问密钥的存储只能在客户端应用程序中进行。如果云平台是公共的，存储账户也可以进行匿名访问。建议使用 Azure AD 来验证对 Azure 资源的权限和访问[28]。在多因素身份验证过程中，会提供一次性密码，并以电话呼叫、移动应用程序或短信的形式发送给用户。

### 4.3 云技术平台的应用和好处

今天，组织着眼于不同的投资，以满足投资回报真正的盈利最大化、改善决策和降低成本。组织的重要投资形式之一在于开发强大的 ERP 框架 [11]。鉴于企业资源规划系统，企业可以搜集、记录、管理和传递所有运营单元的信息。此外，ERP 框架帮助农场拆分存在于生产、库存规划、工程、人力资源、销售和市场营销、生产和所有公司部门的数据。因此，应用 ERP 系统意味着组织的质量得到了改善，沟通更顺畅，成本更低，生产力更高 [11]。随着成本的降低，公司更有能力提供客户价值并提高在行业中的份额，从而获得更高的利润。

对于当前的 ERP 系统，互联网成为连接涉及方的手段 [11]。ERP 框架与电子商务平台集成，以确保与合作伙伴、供应商和其他关键利益相关者更紧密的协作。这意味着对进出库存的监控得到了改善，从而提高了对其活动的可见性和控制。在实施此类系统之前，组织需要考虑相关预算，包括硬件维护费用、培训成本和许可证。简而言之，ERP 系统用于将公司内的功能单元合并，以执行协作任务或流程 [11]。

此外，组织外部的第三方，例如供应商和客户，也可以包含在此框架内。作为基础设施的主要组成部分，ERP 系统提供了业务解决方案。该框架作为一个全面的应用程序出现，集成了实体的所有单元，从而形成了公司的整体 IT 视角。

多年来，ERP 系统的应用并未因功能和协作特性的提升而停滞不前。例如，Oracle 等 ERP 服务提供商已建立了支持公司功能单元的不同模型 [11]。传统上，企业资源规划框架有两个主要类别，包括托管和本地系统。前者是指由服务提供商提供给用户或组织的一种提供，其承载物理服务并远程管理。在这种情况下，采用直接网络链接意味着将忽略互联网。后者涉及在组织的基础设施内运行 ERP 系统，例如计算机、网络和服务器。在这方面，组织对系统的运营和管理负有全部责任，并根据许可证模型操作。

在云计算中，存在大量的应用程序和解决方案。由于 ERP 系统旨在连接组织内部和外部的全球参与者，因此集成更加容易。采用按订阅模式付费的方式，云平台的成本比传统的 ERP 平台更加透明[11]。这意味着组织只为他们所需的付费。采购流程的自动化意味着服务提供商可以向全球范围内的消费者提供解决方案。云平台允许来自不同地理位置的用户访问资源。

此外，服务提供商执行加密指南，从而制定保护标准，保护数据免受消费者的侵害。在实施 ERP 系统之前，客户可以尝试云系统的三种形式[11]。免费试用使消费者对所提供的云 ERP 解决方案充满信心。

目前，由于存储和处理工具的增强发展以及互联网的增长[10]，信息技术硬件变得更加可获得、廉价和强大。这一趋势导致了应用计算机的新框架的建立，称为云技术。信息技术的云计算资源被视为可以通过网络租用和提供的功能。根特公司的调查文档显示，公共云解决方案预计到 2020 年将达到 4000 多亿美元[10]。考虑到对 IT 框架的认识和采用的增加，有必要选择一个具有正确解决方案以确保长期成功的云服务提供商。然而，面临的挑战在于在各种替代方案中做出正确决策，例如 Azure 和 AWS。这两个平台被认为是云计算领域的全球领导者。

软件即服务框架在北美占主导地位，代表了新技术的一个领先且成熟的领域。此外，Gartner 的研究表明，在利用云工具方面，美国和欧洲地区存在着意想不到的差异。在这方面，鉴于欧盟的隐私规定、多个地区的商业交易以及即将到来的经济衰退，预计美国将领先采用这项技术。随着云解决方案的推出，不同的组织以不同的方式采用这项技术。在这种情况下，预计到 2015 年，西班牙的许多组织将利用云计算，只有 69%的中小企业考虑使用这项技术。对于中小企业来说，从 2011 年的 13%增加到 2015 年的 69%，云技术的采用明显增加了。根据专家统计，预计主要公司将利用云计算中的混合系统，并将其与其他功能结合使用，包括 IaaS、SaaS 和 PaaS。相反，由于对 SaaS 应用的需求增加，预计中小型企业将不再关注公共云。

对于高管和组织来说，一个重要的关键是，云技术的应用与其他快速发展的工具相辅相成，包括社交网络、移动计算和大数据分析。这些技术或工具是相互依存的，可以被使用或结合起来提高性能。此外，对于云技术的概念以及其对用户或组织的价值，目前知之甚少。根据这项研究，超过 54%的中小企业提到了对云计算的了解不足，这意味着竞争优势的丧失。另一方面，对云技术优势的认识不足也成为了云平台采用的障碍。

由于没有广泛接受的云服务指南，决定转向云平台是具有挑战性的。因此，制定规定和明确的基础以帮助组织了解他们的需求至关重要。此外，决策者和政策制定者应该有支持工具，以便迅速过渡到云上运行的 IT 系统。由于云计算是一种新兴技术，管理创新是必要的，因为领导干预各种企业流程将需要解决传统做法在处理或应对新技术时的低效率。采用这样的技术也意味着由于员工抵制而产生的组织变革。在这种情况下，组织内的高级管理层应通过提供培训机会并及时沟通变化来为成功实施云技术做好准备。简而言之，组织内的关键利益相关者应该意识到所需的变化，并对采用云工具的好处有更多了解。

云技术解决方案非常复杂，具有陌生的基础设施。一个明显的例子是 Azure 计算结构，它控制着微软数据中心内的虚拟和物理资产。在这种情况下，管理系统是容器调度、虚拟机和其他控制角色。此外，云工具的应用往往会导致开发和运行成本高昂。因此，开发人员需要最大化地利用这些平台来获取价值。一种有前景的方法是利用机器学习作为云资源管理的手段。

## 云计算中的 5 种安全模式

针对云计算，安全模式问题成为软件或应用程序安全的重要组成部分。近年来，由于对抗更高数据攻击和弱点的需求日益增长，云平台中的安全模式得到了极大的发展。今天，数据安全的概念从简单威胁的传统观点扩展到了所有组织和用户确保数据保护的要求。云计算中的软件即服务平台需要关于建议解决方案和知识的结构化数据，以帮助开发安全的云平台。目前正在进行多个安全模式的研究，其中数据被引导到特定领域的安全，如 Web 开发。此外，关于最佳实践和数据安全培训的数据组织和标准化很差。这意味着软件即服务开发人员缺乏开发云应用所需的最佳实践和安全信息的清晰指导。

Rath 等人[26]的研究着眼于一种在定义和分类云计算中现有安全模式方面应用的方法。确定了五个主要阶段，从安全需求确定到安全模式的分类。关键步骤在于云平台的安全需求。这需要清晰定义云计算中的安全需求。最终的主要目标是概述建立保护信任和遵守法律准则所需的所有潜在安全需求。考虑了不同的数据处理需求，例如私人信息控制的责任，从监管框架的角度进行。最后，提供了一个安全数据检查表，以实现软件即服务的最佳应用。下一阶段包括评估风险，这涉及检查云平台中的现有易感性和风险或不确定性。在这一点上，审查必要的安全性和身份和猎人，以确保在云平台的软件即服务项目的设计和执行中保护系统和适当的数据安全控制。最终，该活动产生了一份管理良好的安全性分析报告，列出了可能影响云项目的所有可能安全威胁。有了这样的数据，安全和威胁评估文件可以评估和检索软件即服务平台中的安全功能。

第三，关键是确定现有的安全属性，以确保有效防范恶意攻击。由于有不同类型的攻击针对特定用户、资源或系统，因此需要多样化的安全功能来处理此类攻击。云技术容易受到重大安全风险的影响，例如拒绝服务攻击。这意味着必须考虑关键问题，如隐私完整性和信任。第四阶段涉及根据前一阶段确定的安全功能来定义安全模式。在这一步骤中，关键是调查传统框架的潜在安全模式，以确定其他模型中的现有模式是否可以应用于云环境。为了正确定义安全模式，考虑了三个主要的安全组件，包括数据的安全性，系统的安全性以及有效的通信或受保护的对话[26]。最后一个阶段涉及安全模式的分类。这意味着当存在类似问题或情境时，将确定的模式进行分类。

### 5.1 云技术中的安全问题

对于实体，数据存储主要是组织的整体责任。另一方面，云平台要求数据存储在用户或客户端的外部点，并由服务提供商控制。这意味着在云计算中需要更多的安全措施，以补充现有的传统措施，以确保数据保护[18]。在创建信息后，信息在各个阶段之间自由分发。在数据生命周期过程的每个阶段，都需要对数据进行适当的保护，从其创建到其删除。加密是在数据传输阶段保护数据的一种技术[4]。

云计算中的一个关键步骤在于审计。在这方面，追踪信息路径尤其重要，特别是在处理公共云时。CIA 三角形具有三个关键数据质量，包括机密性、完整性和可用性。前者涉及信息隐私，个人用户的数据受到未经授权的访问的保护。另一方面，完整性保证云数据不受恶意攻击的保证。后者指的是在需要时服务消费者可以访问其数据而不受任何拒绝。在使用公共云时，这三个基本特征在应用之前都会得到检查。

确认和验证控制旨在确定用户在访问和利用云平台资源时的身份。在组织中，计算的概念要求验证存储在服务器目录中。私有云中的身份验证是通过虚拟网络进行的[3]。对于公共云，互联网被用作连接服务提供商和消费者的手段。这意味着公共云平台比其他平台更容易受到风险的影响。

此外，密码的使用可能无法有效地确保公共云中的数据保护。服务提供商必须建立严格的控制措施，旨在通过高度安全的技术确保数据保护。云技术中的验证过程延伸到机器，这些机器需要对特定操作（如系统更新）进行授权。由于使用了各种设备，云应用程序应使用强大的验证方法。Alsmadi 和 Prybutok 最近的研究[3]研究了信息的分发和存储行为，以及关于云技术的学术文献和市场报告之间的现有不一致。

### 5.2 合规和监管框架

在世界各地，不同国家有不同的法规和合规要求。在这个视角下，确保对设置的指南的严格和严格的依从标准至关重要。因此，各种地理位置可以在需要时访问信息[26]。审查监管框架问题时一个重要的考虑因素是安全模式。

信息公民权是一个关键焦点，要求在私人数据被操纵时需要法律制裁。当用户输入和存储数据在云平台上时，如果这些信息被不当使用或处理，开发者和服务提供商要负责并可能会受到法律制裁。这意味着提供商需要开发一种符合已建立的监管框架的解决方案。提供服务的地理位置也是一个重要考虑因素。另一个组成部分在于数据擦除，这是通过使用摄影来进行的过程。开发者需要找到一种策略，确保信息在存储在云平台后被安全且实际地擦除。因此，搜索方法确保了完全满足了法律依从需求。第三，一个常见的角色框架出现了。重要的是要确定谁对数据丢失、修改或任何其他形式的更改负责。云服务消费者必须有效地控制他们在云应用中的法律和监管依从性[26]。与典型信息相反，机密数据处理易受到严格控制和受监管框架管辖的影响。

不同的国家对云平台中发生的信息保留有不同的政策。这需要服务提供商进行相关的适应性。信息生命周期的另一个关键方面是数据处理阶段，从其生成到擦除[26]。特别是对于在云环境中运营的服务提供商来说，有效控制数据，特别是私人数据，是一个重要的角色。数据安全中的一个主要问题在于意外删除信息。在这方面，服务提供商需要了解恢复被恶意删除的信息的最佳实践，并制定预防措施，消除任何恶意攻击者访问和删除现有信息的机会。

## 数据安全和数据完整性最佳实践和解决方案

如今，许多实体都在考虑将云平台作为其大量数据的存储来源。随着组织采用云工具的趋势上升，来自内部和外部方的攻击直接增加。这些黑客识别云网络中存在的漏洞，并触发未经授权的访问，导致数据丢失、共享和泄露私人信息[22]。一个全面的网络安全方法可以帮助解决多云环境中的潜在风险，并为公司实现云技术的好处提供机会。AWS 和 Microsoft Azure 是全球公司使用的主要数据存储云平台。

### 6.1 AWS

对于数据完整性合规性，使用 AWS 提供了几种工具，以确保实体遵守设定的法规框架和数据管理需求。考虑到信息国籍，AWS 的应用提供了地理标签服务，被识别为位置阻止工具，用于控制访问。一个主要的策略在于 CloudFront 应用程序，根据原始国家限制对数据进行访问[26]。此外，该工具在来自可接受位置的请求时提供内容访问，而忽略来自被列入黑名单的国家的请求。更强大的措施将包括将 CloudFront 与其他服务组合以基于各种限制（包括纬度和邮政编码）提供更大的信息访问管理。在加密的数据擦除方面，AWS 提供了一种称为 KMS 的产品来控制应用密钥。该服务使个人能够建立和管理密钥，并在不同的应用程序中管理加密[20]。

符合共同责任框架的使用，使用 AWS 保证了多样的提供以保护信息和系统[26]。用户可以选择使用免费或购买类型。AWS 的重点之一在于确保云平台内数据的可用性和保护性。地理限制工具可以跨区域边界管理信息[26]。AWS 包括不同形式的工具，用于数据备份和存储以保留信息，从而防止恶意攻击。AWS 信息生命周期功能负责使客户能够控制相关资源和应用数据的过程。

### 6.2 Windows Azure

采用全球存储方式提供了各种服务和工具，用于执行法律依从性处理和数据控制。对于信息公民身份，使用 Azure Front Door 是一种可行的解决方案，可以用于限制对信息和应用程序的访问，考虑到地理位置[26]。此外，Front Door 工具包括 Web 应用程序防火墙或 WAF，允许用户在端点的特定路径上操作预定义的自定义访问策略，以允许来自指定区域的访问。在信息消除方面，Azure 密钥保管库包括其他提供，如证书管理[26]。在一个通用的角色框架内，使用不同的工具来确保数据和整个系统得到必要的保护。虽然并非所有的服务都是免费提供的，用户可以根据自己的需求选择免费或付费的工具。

Windows Azure 受到法律需求的限制，以确保云平台的基本安全性和可用性。Front Door 服务还可用于控制信息在不同位置之间的传输[26]。在信息保留方面，使用 Azure 提供了不同的数据存储和备份技术，可以用于保护数据免受意外删除或恶意攻击。一个明显的例子是 Azure cosmos DB，它源于一个多框架目录服务[26]。考虑到信息的生命周期，应用一个全球存储生命周期和一套基于指南的政策，客户可以应用这些政策来管理数据的产生、使用和销毁。最后，Azure 备份工具可以用于数据存储，即使攻击者试图删除内容，数据也会被保留[26]。该工具为 Windows Azure 中的所有资源提供备份服务。

云数据中的另一种攻击形式是拒绝服务问题。为了消除相关的攻击技术，如基于签名的策略、基于过滤器的策略和防火墙是必要的[31]。使用过滤器方法，应用流标签过滤器来识别发生在低速率的拒绝服务攻击。拒绝服务攻击逐渐增加流量的速率，从而影响网络。通过采用签名策略，评估云网络流量，并将攻击模式与数据库中的预定义攻击模式进行比较[31]。给定签名目录，开发了几个预定义的签名，导致阻止可能与数据库匹配的攻击。

另一种攻击类型是恶意软件注入。在典型情况下，服务消费者在平台上创建一个账户，服务提供商在目录结构中开发了客户机生成的账户的副本[31]。服务提供商以高度的诚信和有效性来衡量用户的活动。建议在硬件位置保持数据完整性，因为任何攻击者在试图干扰基础设施即服务云平台时都会面临明显的挑战。最终位置表，或者如果它被用于控制操作系统中的虚拟内容。在给定的工具下，服务提供商可以识别我们的客户将要实施的应用程序[31]。

另外，服务提供商可以与从客户设备获得的早期情况进行验证，以确保后续事件的完整性和有效性。因此，安装一个虚拟化程序很重要，服务提供商可以使用它来测量云平台中最受保护的部分，任何攻击者都无法干扰。虚拟化程序工具有助于记录影响云平台中虚拟机中文件分配表的所有事件[31]。另一个解决方法是，在注册新账户时将客户操作系统存储在第一阶段或初始阶段。在这里，与功能系统进行交叉评估。

由于 CIA 三角形，可以采取各种步骤来确保用户对云平台有最佳体验。在数据创建后，对其进行分类，确定敏感类型，明确定义指南，并为不同数据类型创建访问策略是必要的步骤。此外，重要的是制定信息销毁和存档的政策[18]。其次，确保数据存储伴随着高效的逻辑和物理保护，包括信息恢复和备份计划，至关重要。第三，理解要与谁共享的信息类型，以及共享的过程和定义与常见数据框架相关的政策。服务级别协议或 SLA 是一个集体术语，用于描述适用于云计算的各种政策。

另一个步骤是建立纠正行动策略，以确保数据在被黑客攻击或因网络或通信设备中存在的漏洞而被恶意篡改时的安全性。这意味着数据完整性应在竞争水平和信息水平进行评估。从这个角度来看，竞争的完整性涉及到允许访问可用信息的已验证应用程序。防止任何违反典型计算过程的行动是很重要的。通过适当的身份和访问管理或 IAM 系统，可以解决完整性、机密性和可用性的问题。

在购买云解决方案之前，用户对于利用此类服务的优先事项有所了解。鉴于云平台（如 Azure 和 AWS）的多样性特性，服务消费者可能很难理解他们可能需要的项目所需的必要特性。以往的研究未能对从 IT 视角和系统基础设施中实际需要的特性做出有效结论。鉴于最适用特性的数据有限，客户必须首先评估自己的需求，以更深入地了解他们可能需要的解决方案类型。Kamal 等人[16] 的研究比较了 AWS 和 Microsoft Azure 的特性。在这方面，AWS 推荐用于互联网服务框架。

尽管如此，该平台相对较昂贵且安全性较低，与 Microsoft Azure 相比。而 Azure 则具有崇高的特性，并且在 SaaS 和 PaaS 框架中保持主导地位。此外，该解决方案归功于微软公司，这是一个全球品牌。

云平台内的服务提供商投入巨资开发强大的硬件和软件系统。这些提供商的一个关键考虑因素是优化资源的高投资应用，并确保改善性能和可用性。促进最大程度采用这些资源的一个潜在方法是将机器学习集成到云工具中。在此之上，Bianchini 等人[5] 的研究专注于研究将机器学习纳入云平台资源管理规划的机会和设计。提供了超级计算机框架的案例作为一个示例，展示了如何将机器学习与 Azure 平台相结合，利用服务和容器中行为的预测。研究中建立的预测系统导致云平台的这种转变。虽然该研究描绘了机器学习模型可以帮助管理者在规划资源方面做出更加明智的决策，但对于这个主题的研究仍然有限。

## 7 结论和建议

在云计算中，关键问题在于云工具中的数据保密性和保护。鉴于云设置的资源共享、虚拟化、移动计算、服务级别协议和异构性，云平台极易受到攻击。该研究着重于阐述数据安全问题和缓解所产生问题的补救措施。然而，存在着新兴挑战，缺乏明确的缓解方法，给云技术的潜在客户带来长期风险。云技术有了新的发展，如物联网和面向软件的网络，这意味着提供了更强大的功能和存储条件，以解决云平台中出现的问题。随着这些发展而来的是云技术的相关挑战，需要采取积极的措施和解决方案。鉴于技术的猛烈变化和动态性，有必要制定清晰的数据安全政策和法规，以及不相关的更新，以维护云计算中的数据完整性。

应进一步实施研究，以保障用户和机构在采用云技术时的可信度。设计能够识别预期的未经授权访问数据的有效框架至关重要，并向客户保证云计算解决方案的安全性。多年来，自互联网问世以来，人们对设备感染、病毒攻击和数据丢失存在巨大关切。目前，越来越多的人和组织通过使用不同的设备来利用互联网，潜在的恶意软件攻击情况有所减少。一些软件公司开始大力投资于构建技术，以识别病毒攻击并防止其访问设备或数据。由于技术的进步和最佳实践，现在恶意攻击的发生率有所降低。

同样，云计算专业供应商和 IT 协会必须更多地投入到开发检测系统中，以识别未经授权的访问、预防措施和实施云技术的最佳实践。应该进行更多的调查，评估是否已经取得了防止未经授权访问数据的进展。正如案例研究所描述的，一些大型组织因为一些盗窃问题而损失了收入。与其重新授权用户使用合法产品，软件公司逐渐构建了一种新技术，告知用户使用盗版软件的潜在风险。

预计还需要更多的检查来确定在教导客户安全使用分布式计算方面所取得的进展。此外，识别最佳指导方针，帮助最终用户或企业增强对分布式计算的信任是至关重要的。此外，需要对云服务提供商承担更大的责任，当数据泄露时，需要对其进行限制。目前，对于云服务提供商因数据丢失或不可用而负责的进展有限。如今，如果数据丢失或未经授权访问存在某些妥协，企业更愿意对最终用户使用其服务做出反应。
