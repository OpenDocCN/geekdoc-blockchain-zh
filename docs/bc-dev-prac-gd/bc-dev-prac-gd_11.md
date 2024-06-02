© Elad Elrom 2019 Elad Elrom 区块链开发者

# 11. 安全和合规

Elad Elrom¹（1）纽约，纽约州，美国

正如你所看到的，大多数区块链都是去中心化的，每个方的身份通常得到保护；然而，大多数与区块链相关的代码涉及存储一些机密数据，如用户的个人信息、密码、加密货币和钱包。

与区块链相关的代码具有吸引黑客的特点。

+   代码通常是开源的，以提高透明度并鼓励贡献者。

+   目前大部分代码还不够成熟，不能被视为发布级别。

+   在加密货币相关的区块链中，丢失数据不仅仅是隐私泄露那么简单。一旦资金转账，追踪它们将很困难，而且转账可能无法撤销。

这些担忧随着区块链技术的普及和越来越多的人投资于区块链而加剧。实际上，关于区块链相关的损失的报道越来越多，几乎每天都有关于新攻击的新闻发布。例如，在撰写本书期间，从币安交易所盗窃了 4000 万美元。此外，在过去的 12 个月里，估计有 2300 万美元在双重支付攻击中被盗。同样，有 15 亿美元从加密货币交易所被盗。

事后的报告有时会显示一种复杂的盗窃方法，要想预防这种方法，你需要是个天才。然而，大多数攻击是可以轻易预防的，它们不过是简单的人为疏忽或没有使用能够揭示漏洞的工具的结果。

> “知识分子解决问题；天才预防问题。”
> 
> ——阿尔伯特·爱因斯坦

作为专业人士，对那些信任你的客户，以及你的声誉和受托责任负责，减轻这些风险并确保数据得到保护是你的责任。在开发周期的所有阶段都应考虑安全措施；实际上，安全应该是你开发中最重要的方面。然而，假设我能在一个章节中涵盖所有的安全方面是不现实的，因为已知的具体攻击有数千种。

除了安全，还需要解决的问题就是监管。监管机构一直在塑造通用技术，特别是区块链行业，每个地理位置都有多个需要遵守的监管规定。

由于新的攻击方法每天都在被发明，监管法规也需要经常修订。理解常见的攻击、安全、隐私、合规和法规可能是一项挑战。

在本章中，我将向你展示安全思维，并帮助你更加了解安全、隐私和合规。本章分为三部分。

+   安全准备状态：我将介绍你在开发平台之前和开发过程中应该考虑的方面。

+   常见区块链攻击：我将介绍一些最著名和常见的区块链攻击。

+   开发周期：我将为你提供推荐的开发周期，以便你在开发过程中考虑安全和合规。

具体来说，我将介绍安全测试、隐私和合规要求，以确保你的代码考虑尽可能多的场景，以帮助保护用户数据。我将介绍导致巨大损失的常见区块链相关网络攻击，以及区块链网络特定的攻击。我将介绍作为用户和开发者如何预防这些攻击。最后，我将介绍一个建议的开发周期，你可以采用它来降低损失风险和平台关闭的风险。

## 安全和合规准备状态

在本节中，我将介绍在安全测试方面你需要考虑的一般性领域以及达到安全准备状态的含义。此外，通过查看欧洲和美国的法规为例，你将理解达到合规准备意味着什么。最后，我将强调在开发周期中及发布代码之前你应该考虑的建议。

### 安全准备状态

在传统的编码环境中，你需要考虑安全测试以发现代码中的安全缺陷，确保它如预期那样正确运行，以及数据得到保护。

### 注意

安全测试是一个旨在发现代码中安全缺陷的过程，以确保代码和数据如预期那样运行。

安全测试包括以下措施：

+   机密性：确保用户信息得到保护。例如，实现一个仅会员区域，通过安全套接层（SSL）连接，该连接通过互联网发送数据时使用加密。

+   信息完整性：保护信息不被更改。例如，当数据在你系统的不同层次之间传递时，对其进行加密和解密。

+   认证：确认用户身份，以及确保系统受到信任。例如，登录系统。

+   可用性：确保你的系统正常运行。例如，安装防火墙以防止攻击。

+   授权：确保请求者被允许接收服务或执行操作。例如，创建一个限制特定实体访问的 Hyperledger 权限区块链。

+   不可否认性：确保在发送和接收消息时有一个确认系统，以便各方不能否认收到消息。例如，发送电子邮件通知以确认数字资产的转让。

### 合规准备状态

除了这些传统的网络安全测试考虑之外，您还需要考虑区块链特有的安全和地方合规性，以确保您的平台符合监管要求。

### 注意

安全性合规是实体的法律问题。它是一个提供隐私建议以及提高安全性的监管标准。

合规性并不直接关注安全；然而，许多地方合规性要求都考虑了安全问题，确保用户和数据都得到保护，因此它们是有间接联系的。许多大型公司都聘请了安全和合规性专家以确保两者都得到满足。

您可能想知道，为什么我还需要考虑法规呢？区块链不就是想成为去中心化的吗？

确实如此；然而，近年来，由于持续的欺诈和攻击，区块链运营商受到了监管机构的制约，导致了重大的损失，许多国家也实施了隐私政策和安全措施。因此，你需要检查合规性和安全法规，以确保不违反任何法律。

实际上，许多机构和当局已经发布了研究论文，分析区块链与数据保护法规之间的关系以及如何准备实现“合规性准备”。

### 注意

合规性准备确保实施符合治理要求。区块链在全球许多地方的法律和法规中并没有特例。

例如，在欧洲和美国，与数据保护影响评估（DPIA）和通用数据保护条例（GDPR）相关的合规性立法和政策具体规定了在区块链上不允许存储哪些信息。

这不仅仅是关于可以和不可以存储的数据；许多国家实施了隐私法律，限制了可以跨地理边界传输的数据类型。

与区块链社区中的许多人不同，他们认为合规性法律只是为了限制和控制区块链技术以取代传统机构，许多规则是为了保护投资者免受损失，以及保护用户的隐私。此外，在某些国家，有法律和规定要求您进行记录保管，并存储用户数据以帮助防止欺诈、洗钱和恐怖主义。

例如，2013 年，在美国，银行保密法（BSA）1970 年和金融罪行执行网络（FinCEN）向交易所和 ICO 发布了指导方针，将它们归类为需要注册、报告和记录保管的货币服务业务（MSB）。这意味着在美国，交易所和 ICO 需要向 FinCEN 注册为 MSB。

忽视合规可能会导致传票、罚款、停业，甚至可能面临刑事指控。例如，在欧洲，GDPR 设定了遵守特定合规的截止日期。无法遵守的公司可能会面临重罚。这适用于移动设备、电视应用、网页门户、网站、API 和云存储。事实上，在 2019 年，法国数据保护机构 CNIL 对谷歌处以 5000 万欧元的罚款。另一个例子是稳定币泰达币，在撰写本文时，纽约最高法院命令其在 Bitfinex 交易所冻结其货币的转让。

每个地理位置在处理区块链技术方面都受到特定的要求，因此在开发软件之前，了解法律、安全和隐私规则非常重要。

实际上，每个地理区域的监管机构都可以设定自己的规则。如果你以美国和欧洲为例，每个国家对区块链的规定都不相同；如果你甚至有一个来自这些国家的访客，你也应该遵守这些规定。在本章中，你将查看美国为例；然而，你需要查看每个具体的地理区域适用于当地的特定规则。

#### 美国合规

美国有安全规定和货币转移法律，要求你遵守特定州的法律，如果你转移加密货币，你甚至可能需要申请一个州级许可证。美国处理与区块链相关的技术的机构是证券交易委员会（SEC）和替代交易系统（ATS）。

在撰写本文时，美国证券交易委员会（SEC）将初始代币发行（ICO）和证券代币发行（STO）都视为证券。因此，它们受到 1934 年证券交易法案的监管，该法案规定了如何在不同实体间转让证券。例如，SEC 要求交易所向国家证券交易所及/或自动交易系统（ATS）注册。

### 提示

在美国，STO 和 ICO 都被视为证券；然而，STO 在投资者中比 ICO 更受欢迎，因为许多 ICO 在 2018 年和 2019 年被迫退还投资者的资金。

交易所也必须遵守特定的规定；例如，由于 1936 年商品交易法案（CEA），涉及衍生品的交易所必须向商品期货交易委员会（CFTC）注册为 CFTC 交易所或指定商品市场（DCM）。

### 注意

为了更好地了解如何在美国合规，请阅读 NIST 发布的以下报告：[`nvlpubs.nist.gov/nistpubs/ir/2018/NIST.IR.8202.pdf`](https://nvlpubs.nist.gov/nistpubs/ir/2018/NIST.IR.8202.pdf) 。

#### 欧盟合规

欧盟正在实施针对区块链和加密货币市场的特定要求；这些要求将考虑一种名为了解你的客户（KYC）的协议和反洗钱（AML）法律。

关于数字资产，欧盟目前的法规并不反对加密货币与法定货币之间的兑换。大多数担忧是确保加密货币不被用于资助非法活动，例如洗钱和恐怖主义。

为了考虑这些担忧，加密货币平台需要对客户进行尽职调查，并根据 KYC 报告任何可疑交易。

为了更好地了解如何在欧洲合规，阅读这些 EUBOF 和 CNIL 的报告：

+   [`www.eublockchainforum.eu/sites/default/files/reports/eu_observatory_blockchain_in_government_services_v1_2018-12-07.pdf`](https://www.eublockchainforum.eu/sites/default/files/reports/eu_observatory_blockchain_in_government_services_v1_2018-12-07.pdf)

+   [`www.cnil.fr/sites/default/files/atoms/files/blockchain.pdf`](https://www.cnil.fr/sites/default/files/atoms/files/blockchain.pdf)

### 提示

法规经常变化；留意 SEC、EUBOF 等组织发布的新闻和信息，这些组织发布了你的平台。如果你在社交媒体上，关注这些组织的账户或把新闻更新添加到你的阅读列表中。

### 准备建议

通过提高意识，你可以实现合规和安全准备，确保你的平台为生产做好准备，并帮助防止攻击者或政府导致的平台关闭。

没有一个确切的全球规则集可以确保准备就绪，因为合规在地理边界之间是不同的；然而，有一些关键要素是良好的实践，可以帮助你做好安全和合规准备。在下一节中，我将介绍具体的攻击；这些一般性建议是在你仍在开发应用程序时需要考虑的基本建议。

+   地理位置：如果你打算在你的平台上注册哪怕一个用户，你需要在那个用户的所在地准备好合规，并了解那里的规则和法规。

+   解决问题：确保你实际上在解决问题。问自己，我的独特卖点（USP）是什么？不要仅仅为了加入区块链热潮而使用区块链。2017 年的 ICO 盛宴已经结束，许多硬币被除名，ICO 被迫退还投资者。

+   基于权限的区块链：如果你正在建立一个基于权限的区块链，你应该定义成员的角色，如管理员、发布者、用户等。

+   隐私：关于提供用户信息，越多越好。就隐私问题尽可能多地通知你的用户。当你收集数据时，越少越好；只捕获你所需要的。以下是一些关于隐私的具体建议。

    **提示** 根据 CNIL、NIST 和 EUBOF 的报告，遵循通用数据保护条例（GDPR）实施你的代码。

    +   **隐私政策**：设定隐私政策，告知用户存储了哪些信息以及与第三方共享了哪些信息。例如，在隐私政策中告知用户将数据日志输入到分析工具中。

    +   **取消订阅**：在您的平台上发布一个用于同意、撤销和投诉隐私政策的表单或电子邮件地址。

    +   **政策更改**：告知用户任何隐私政策的变化。

    +   **收集用户数据**：在收集所有用户信息时，采取简约主义方法；只存储所需的内容。

    +   **收集的数据**：将数据分为运行平台所需的 data 和其他收集的数据。

    +   **匿名化**：考虑对平台进行全面匿名化。

    +   **地理位置**：在存储数据时，确保数据按照该地理位置的指南进行收集。

    +   **许可**：在存储任何数据时，例如在 cookies、本地数据库或云中，请求用户的许可。

    +   **清除所有内容**：用户登出后，清除 cookies、会话和其他存储内容。允许用户清除平台上的任何第三方工具中的数据。

    +   **清理**：允许用户删除数据并清理历史记录。

    +   **导出**：允许用户导出数据。

    +   **通知**：告知用户任何数据泄露。

+   以下是一些一般性安全建议：

    +   **安全套接字层（SSL）**：在整个 Web 应用程序中使用 HTTPS，特别是在请求和导出数据时。

    +   **零知识证明（ZKP）** ：对于区块链，使用零知识证明（ZKP）；参见 [`github.com/topics/zero-knowledge-proofs`](https://github.com/topics/zero-knowledge-proofs) 。

        **注意** ZKP 是一种方法，其中一方向验证者证明他们知道 x 的值。一个现实生活中的类比就是敲门并提供一个秘密词来获取进入一个私人、会员制俱乐部的权限。

    +   **加密**：使用同态加密或安全多方计算。

    +   **安全认证系统**：使用安全的认证系统，如 OAuth 2.0 标准。示例：[`developer.github.com/apps/building-oauth-apps/`](https://developer.github.com/apps/building-oauth-apps/) 。

    +   **服务超时和限制**：为服务设置超时机制，以延迟响应，确保不会使服务变得缓慢（减速）。实现登录尝试的节流。在各个地方设置安全握手。

    +   **常见安全漏洞**：防范如分布式拒绝服务（DDoS）和跨源资源共享（CORS）等常见安全漏洞。

        **注意** CORS 使用额外的 HTTP 头，使在一个域名上运行的应用程序能够访问不同域名服务器上的资源。

    +   **敏感信息**：将密码和其他敏感信息以散列数据的形式保存，使用加密方法。

    +   **IP 限制**：限制可以访问你端口的 IP 地址。例如，只允许对你的 IP 地址有 root 和 FTP 访问，而不是任何 IP 地址。

    +   **安全度量**：将安全措施纳入开发周期（请参阅本章后面的“开发周期”部分）。

总结一下，我回顾了什么是安全准备，什么是安全测试，以及如何做到合规准备。你了解了美国和欧盟关于区块链技术的合规法规，最后，我介绍了你应该在开发周期的早期阶段考虑的安全准备建议。在本章的下一节中，你将了解可能导致重大损失的具体加密货币钱包攻击以及如何预防它们。

## 常见区块链攻击

在本节中，我将涵盖一些最著名和常见的区块链攻击。我已经将这些攻击分为三个类别。

+   **钱包网络攻击**：针对加密货币钱包。

+   **区块链网络攻击**：针对区块链 P2P 网络。

+   **平台攻击**：针对支持区块链的平台，如交易所、网站和借贷平台。

请记住，尽管我已经将过程分为三个类别，但大多数这些攻击使用不同的技术和技术目标，但都有相同的目标，即捕获加密货币私钥。

### 钱包网络攻击

在本节中，我将回顾针对加密货币钱包的具体网络攻击。正如我在本章开头所强调的，一旦加密货币资金被转移，要追踪它们是很困难的，因为它们可以从一个钱包转到另一个钱包，而且转移是不可逆的，除非网络上的大多数节点同意改变区块。

> **“对于每把锁，总有人试图去撬开它或闯入。”**
> 
> ——大卫·伯恩斯坦

常见的钱包攻击可以采取多种形式，通过产生用户丢失私钥同样的结果。攻击者通常从“网络钓鱼攻击”开始，导致用户机密信息被泄露，然后犯罪者能够将资金转出账户。

### 注意

**网络钓鱼攻击**（想想信息钓鱼）是试图欺诈性地捕获用户机密信息，如用户名、密码、账户号码等的一种尝试。这是通过使用电子邮件等电子通信，将攻击者伪装成可信赖实体来实现的。

实际上，除了 Bitconnect 和 iFan 等加密货币骗局，与钱包相关的盗窃导致了加密货币资产的第二大损失，总计接近 50 亿美元（见图 11-1）。![../images/475651_1_En_11_Chapter/475651_1_En_11_Fig1_HTML.jpg](img/475651_1_En_11_Fig1_HTML.jpg)

图 11-1

最大的加密货币盗窃事件

对抗钱包攻击的最佳方案是在不使用时彻底移除加密货币交易所中的加密货币，并将其存储在您自己的“冷钱包”中。这可以通过使用如 Nano、Trezor、KeepKey 等硬件钱包来实现。将加密货币转移到冷钱包中可以为您提供最高级别的保护，避免 Mt. Gox 等交易所发生的管理员密码被破解，许多用户失去了他们的钱包钥匙等损失。

### 注意

冷存储*是一种将加密货币私钥存储在 USB 驱动器、纸钱包或其他数据存储介质中的方法，并将其存放在安全位置。将其视为自己的银行。

在下一节中，您将了解常见的钱包攻击。我将提供事后分析，以帮助确保您不会重复其他开发者和用户犯过的错误。

#### 在线钱包钓鱼-恶意软件攻击

在线钱包比离线钱包更容易受到攻击，因为它们连接到互联网。例如，最近对 Electrum 钱包发起了一次钓鱼-恶意软件攻击，造成了超过 100 万美元的损失。

### 注意

恶意软件来自*恶意*和*软件*这两个词的组合。这种软件旨在破坏、损坏或获取受害者电脑的访问权限。

黑客通过设置恶意服务器来实现这一点；当用户钱包连接到这些服务器之一并尝试发送 BTC 交易时，攻击者的代码会显示一个看起来官方的消息，告诉用户需要更新他们的 Electrum 钱包，并提供一个虚假的网址下载带有恶意软件的 Electrum 钱包虚假版本。

一旦用户使用了攻击者的 URL 并下载了新的 Electrum 虚假版本，钱包要求用户重新输入他们的密码，然后发送给黑客。然后黑客拥有了用户的登录信息，并能够登录到真正的 Electrum 钱包中，并将用户的私钥转移到自己的钱包中。

##### 事后分析

作为用户，除了避免使用在线钱包并使用冷存储外，您还可以通过以下方式降低风险：

+   仅*下载官方软件*：不要从任何其他来源下载在线钱包或升级，除非是钱包的官方网站。通过悬停在链接上但不点击它们来检查 URL，特别是检查小拼写错误；看看您是否能在这里注意到小错误：paypaI.com, Electrom.com。

+   保护您的*信息*：小心通过电子邮件分享的信息。要求您确认账户凭证的电子邮件必须来自您认识的业务，或者您发起请求的电子邮件。

+   确保*身份验证*：下载钱包软件并检查 GPG 签名。永远不要将您的加密资产私钥透露给任何“官方”代表。

+   - 识别**假冒的客服电话**：通常，那些想要获取你信息的钓鱼公司会使用一个假的客服电话。许多人通过在谷歌上搜索公司电话号码而成为这种攻击的受害者。

作为开发者，你应该做以下事情：

+   - 使用**GPG 签名验证**：实施 GPG 签名验证。

### 小贴士

GPG/GNU 是一套用于加密的加密软件，通过检查签名与下载的文件相对以确保真实性。为了确保防止钱包攻击，实施 GPG 或 GNU 隐私守护。作为用户，不要忘记也检查实际的 GPG/GNU 本身是否经过认证，并且来自开发者。

+   - 教育你的用户：设置页面、视频教程和博客文章来教育你的用户，防止用户犯常见错误。

#### 键盘记录器恶意软件

大多数恶意软件旨在损害你的计算机。流行的可以用来提取你的加密货币的恶意软件是键盘记录器或屏幕抓取器。这种软件记录你输入的所有内容，以及截图你的电脑，试图捕捉密码和个人信息。这类攻击在家中发生的可能性较小，因为攻击者需要将一个实际的通用串行总线（USB）密钥连接到你的电脑来记录键盘日志；然而，当你使用公共电脑时，例如在大堂或图书馆，这种情况可能发生。

##### 事后分析

如前所述，在家中你不太可能受到键盘记录器的攻击；然而，当你登录公共计算机时，要小心，检查计算机上是否附有 USB 密钥，并避免访问你的重要账户。在自己的计算机上，在 Mac 上，检查活动监视器以确保你认出所有后台运行的服务。如有需要，进行网络搜索以找到任何你不认识的服务，如果任何东西看起来不正常，停止并删除服务和应用程序。如果有疑问，安装杀毒软件并重新安装你的操作系统。

#### 尘埃攻击

尘埃攻击是由攻击者发送一个微小的（尘埃）交易，黑客要么用来占用区块链网络的区块空间，要么用来标记目标地址，希望用户交易这些加密货币，这可以帮助攻击者通过追踪交易历史来识别用户的个人信息。

##### 事后分析

作为用户，不要花费未被识别的交易。

作为开发者，实现一个币控制功能，以便未被识别的交易可以被标记为“不要花费”并且不包括在你的交易中。

阅读有关比特币的隐私文档，它提供了关于保护隐私的宝贵信息，这些信息可以适用于许多场景：[`en.bitcoin.it/wiki/Privacy`](https://en.bitcoin.it/wiki/Privacy) 。

#### 热钱包攻击

在热钱包攻击中，攻击者会从存储在线的“热钱包”中通过钓鱼、破解密码或其他方法获取钱包的私钥。一旦私钥从在线网络中提取，攻击者可以将这些钥匙转移到自己的钱包中。

### 注意

交易所将用户的加密货币私钥在线存储在所谓的**热钱包**中，或称运营钱包。这些私钥之所以在线存储，是为了允许从钱包中实时提现。

##### 事后分析（Postmortem）

作为用户，避免这些损失的最好方法是将你的加密货币控制在自己的冷钱包中，而不是在中心化交易所上。

作为开发者，请执行以下操作：

+   **保持冷钱包**：将用户的密钥存储在冷钱包中，并尽可能避免热钱包。例如，Coinbase.com 声称它将 98%的用户资金以纸张备份的形式存储在地理分布的安全保险箱中。

+   **加密私钥**：如果你需要在连接到在线网络的存储设备上存储私钥，至少要用强加密密钥加密这些钥匙。

+   **关注异常活动**：例如，许多交易所会手动批准大额提现。

### 区块链网络攻击

在本节中，我将介绍针对区块链网络的常见攻击。

#### 女巫攻击（Sybil Attacks）

“Sybil”这个名字与多重人格障碍患者同义。

### 注意

区块链女巫攻击是一个实体通过创建多个身份和控制多个节点来试图影响 P2P 网络。

女巫攻击通过创建多个虚假账户来控制一个网络。控制这些多个账户的实体然后在民主网络中拥有额外的投票权，从而影响网络。

一个容易理解这个概念的方法是 2017 年美国的选举，其中一个实体，俄罗斯，通过创建多个社交媒体账户并控制这些账户的内容来影响选举过程。

一个区块链的例子是攻击者通过创建多个 Sybil 身份在 P2P 网络上投票超过诚实的节点。拥有多数投票权后，攻击者可以拒绝接收区块或传输假区块。

如果女巫攻击执行足够大的攻击，它们能够控制 P2P 网络的大部分哈希率并改变区块，这就构成了双重支付攻击。

##### 事后分析（Postmortem）

作为开发者，你可以通过让女巫攻击变得不切实际来阻止女巫攻击。如果启动女巫攻击有成本，比如创建账户、运行服务器、用电等成本，这可以阻止或使攻击变得不切实际。但请确保你考虑了需要创建多个账户的合法用户。

实际上，流行的区块链一直都在考虑 Sybil 攻击。例如，比特币的 PoW 普查算法需要大量的计算能力，所以创建一个区块与总计算能力成比例。这会阻止攻击者，因为矿工宁愿进行实际的挖矿，也不愿意在失败的 Sybil 攻击中损失。同样，PoS 普查算法需要质押币，所以攻击者会冒着失去这些币的风险。

此外，正如您在之前的章节中看到的那样，以太坊、EOS 和 NEO 部署 dapps 时的成本很高。以太坊有最低 32,000 gas 的费用和每字节 200 gas 的费用，EOS 大约需要 120 个币，NEO 的固定成本在 100 到 1,000 gas 之间。此外，许多区块链（如比特币、以太坊和 NEO）都会收取交易费，这有助于阻止攻击者。同样，EOS 不收取交易费，但它采用了一种“信任链”来对抗攻击者。

### 注意

一个 *信任链* 是一种通过在允许新身份加入网络之前要求信任来对抗 Sybil 攻击的方法。信任链的一个版本可能包括允许用户创建新账户，但一定时间内不赋予它全部权限。

EOS 向开发者收取 1 美元至 4 美元的新账户费用；显然，开发者会不愿意创建账户并采取缓解措施以获得账户批准。

另一种对抗 Sybil 攻击的方法是将等级制度从民主转变为英才制度（由选定的人管理）。很久以前创建且信誉良好的用户比新账户拥有更多的权重。想想 Stackoverflow.com 或 Wikipedia.com 的信誉系统；参见 [`stackoverflow.com/help/whats-reputation`](https://stackoverflow.com/help/whats-reputation) 。

#### 双重支付或 51% 攻击

在本书的前面，我谈到了针对加密货币的潜在双重支付攻击，其中一个恶意节点控制了区块链网络的 51% 以上的哈希率，并能够修改和操纵区块。像比特币和以太坊这样的大型区块链由于矿工竞争，要求有很高的资源，因此不容易被 51% 攻击所攻克。例如，根据 [`www.crypto51.app`](https://www.crypto51.app) ，在撰写本文时，攻击比特币的理论成本为 257,472 美元；参见图 11-2。![../images/475651_1_En_11_Chapter/475651_1_En_11_Fig2_HTML.jpg](img/475651_1_En_11_Fig2_HTML.jpg)

图 11-2

各种区块链的 51% 攻击理论成本

然而，较小型的区块链已经成为 51%攻击的目标。这发生在 Verge 区块链上，在两次攻击中损失了近 300 万美元。比特币黄金遭受了最大的 1800 万美元损失，以太坊经典损失了 110 万美元。实际上，在 2018 年和 2019 年不到一年的时间里，总损失达到了 2300 万美元；见图 11-3。![../images/475651_1_En_11_Chapter/475651_1_En_11_Fig3_HTML.png](img/475651_1_En_11_Fig3_HTML.png)

图 11-3

2018 年 1 月至 2019 年 1 月的双重支付损失

##### 事后分析

作为投资者，你应该检查攻击您感兴趣的区块链的成本，并检查区块链是否有安全网机制。

区块链开发者应该创建某种安全网机制，例如创建一个哈希，持有您每个块的所有交易和余额的快照，然后将该哈希存储到更大的区块链中。例如，您可以利用比特币的 OP_RETURN，正如你在第四章所做的那样，将哈希作为备份，以防 51%攻击发生。

事实上，[`komodoplatform.com`](http://komodoplatform.com) 能够通过创建一个延迟工作量证明（dPoW）安全机制来解决双重支付问题。

#### 矿工勒索软件

如我所说，到目前为止，比特币还没有受到 51%攻击的影响；然而，黑客已经找到了一种通过攻击矿工的勒索软件来影响区块链的新方法。

### 注意

勒索软件是一种旨在封锁电脑直到支付金钱的恶意软件。这个名字是“赎金”和“软件”这两个词的混音。

黑客使用与勒索软件相似的技术锁定挖矿设备。在个人电脑上，恶意软件（如 NotPetya 勒索软件）被下载并安装，然后能够锁定用户的电脑，直到向一个钱包地址支付赎金。

迄今为止，勒索软件只针对个人电脑；然而，像 hAnt 这样的新勒索软件正在针对矿工。hAnt 是如何安装的尚不清楚，但据估计，它可能是与采矿设备固件的一个版本一起下载的。然后，勒索软件就可以访问矿工的固件并控制矿工。

攻击者在管理员登录后显示一条消息，威胁要过热并摧毁矿工。如果受害者不感染其他设备或支付比特币赎金，可以通过关闭风扇来实现，如图 11-4 所示。到目前为止，只有 Antminer 和 Avalon 生产的比特币和莱特币矿工受到影响，但这种攻击可以潜在地针对任何矿工。![../images/475651_1_En_11_Chapter/475651_1_En_11_Fig4_HTML.jpg](img/475651_1_En_11_Fig4_HTML.jpg)

图 11-4

hAnt 勒索软件信息。图片来源：sensorstechforum.com。

##### 事后分析

删除勒索软件并不容易。该软件可能包含一个“绊线”脚本，如果矿工断开与互联网的连接，该脚本可能会损坏矿工。为了解决这个问题，你需要首先从矿工的 Secure Digital (SD) 卡中手术式地移除勒索软件。此外，矿场短时间离线是昂贵的。

最佳的做法是完全避免这种攻击，不要从任何非官方供应商的网站下载固件升级。

#### 对 P2P 网络的日食攻击

信息日食攻击可以单独进行，也可以作为其他攻击的一部分，如 51%攻击。攻击者通过操纵网络，使节点只与恶意节点通信，从而控制 peer 在 P2P 网络中的信息访问。然后，攻击者可以操纵挖矿和共识机制。

##### 事后分析

进行分析、模拟和实验，以找到避免日食攻击的对抗措施。有关增加比特币对抗日食攻击安全性的潜在对抗措施的优秀研究可以在这里找到（并且可以应用于许多其他区块链网络）：[`hackernoon.com/eclipse-attacks-on-blockchains-peer-to-peer-network-26a62f85f11`](https://hackernoon.com/eclipse-attacks-on-blockchains-peer-to-peer-network-26a62f85f11) 。

#### 路由攻击

互联网路由攻击包括 BGP 劫持，针对互联网服务提供商（ISP）的恶意攻击也可以针对区块链执行。

### 注意

边界网关协议（BGP）劫持是一种恶意重定向互联网流量的攻击方式。这种方式通过虚假宣布对一组 IP 地址（IP 前缀）的所有权来实现。

大型矿场集中在少数地理区域内，这使得它们成为 ISP 类型攻击的理想目标。攻击者可以执行以下行为：

+   **分区攻击**：ISP 可以通过劫持几个 IP 前缀来分区 P2P 网络。

+   **延迟攻击**：ISP 延迟与区块链节点的双向流量，导致区块传播延迟，减慢交易速度。

这类攻击可能会减少节点的收入，并且随着影响网络的节点数量减少，还可能演变成 50%的攻击。此外，这些攻击还可以阻止像交易所这样的大型实体发送交易。

##### 事后分析

创建一个自定义脚本或安装硬件来监控网络。许多互联网服务提供商（ISP）提供付费解决方案来监控网络并预防攻击。参考“拒绝服务和分布式拒绝服务攻击”的事后分析部分，了解可以缓解此攻击的更多解决方案。

### 平台攻击

比特币的区块链网络设计之初就是一个安全的网络，并且已经证明是可靠的。比特币于 2009 年发布，截至撰写本文时，还没有成功的针对比特币区块链网络的攻击。

比特币的区块链之所以具有很高的安全性，是因为数据分布在节点之间。此外，挖掘比特币耗能巨大，因此攻击比特币网络可能比挖矿本身成本还要高，攻击者尝试攻击时可能会损失资金。然而，这并不是唯一的原因；比特币能够经受住时间的考验，一个重要因素是它是开源的，使开发者能够根据研究和安全专家的建议快速实施更改。

话说回来，这并不能保证其他建立在安全区块链之上的服务平台的安全，例如交易所、借贷平台、基于钱包的服务以及存储私钥的去中心化应用（dapps）。

例如，交易所持有数十亿的存款，成为黑客的完美目标。如前所述，交易所以私钥的形式保存用户的加密货币，其中一些密钥保存在在线的热钱包中，以允许实时提款和交易。不妥善处理这些私钥可能会导致损失。

Mt. Gox 2011 年的安全漏洞是一个很好的例子。这次攻击发生是因为一名黑客成功破解了 Mt. Gox 审计师的密码，并将 800,000 个比特币转给了自己。除了 Mt. Gox，不断有关于交易所因加密货币损失而关闭的新闻。

从图 11-5 中，您可以看到，Mt. Gox 在两次攻击中损失了近 10 亿美元，而加密货币历史上最大的盗窃是由 2018 年对 Coincheck 交易所网络的攻击造成的。![../images/475651_1_En_11_Chapter/475651_1_En_11_Fig5_HTML.jpg](img/475651_1_En_11_Fig5_HTML.jpg)

图 11-5

交易所损失的比特币最多

在下一节中，我将回顾一些最大的攻击，并给您提供如何预防这些攻击的建议。

#### 凭证攻击

例如，密码破解等认证相关攻击导致了数百万的损失。

+   直接攻击交易所：如前所述，2011 年 Mt. Gox 的 51%攻击导致了两次独立的损失：2,609 个比特币和超过 750,000 个比特币。黑客能够获取审计师的凭证，并将这些比特币转移到黑客的地址。

+   针对用户的攻击：由于接管用户账户，造成了数百万的损失。例如，电话公司通过提供简单的账单信息，使账户接管变得容易。黑客可以将号码转移到新提供商，并通过短信验证批准交易所账户的重置密码。

##### 事后分析

作为用户，避免这些损失的最好方法是将您的加密货币资产保存在冷钱包中，而不是中心化的交易所。

在自己的计算机上：

+   SSL 证书：不要在未提供 SSL 证书的网站上注册。

+   使用强密码：使用独特且复杂的密码，长度要长，并包含数字、字符和特殊字符。

+   使用独特密码：不要在不同平台上重复使用相同的密码。

+   多层次安全：设置所有推荐的安全层次，如 SMS、启用 2FA、邮件确认等。

+   杀毒软件：安装付费或免费的病毒扫描软件。在个人电脑上，Avast 安全有一个免费版本，被 4.35 亿人使用：[`www.avast.com`](https://www.avast.com) 。它包括一个用于 Chrome 的插件，可以警告用户免钓鱼网站。

+   VPN：尽可能在公共且不安全的网络中使用 VPN 连接。

+   避免恶意软件和勒索软件：注意你安装的软件，并确保它来自信誉良好的供应商。安装软件时阅读所有信息，不要只是同意所有信息。安装防止勒索软件的软件。

### 小贴士

将你的加密资产控制在冷钱包中，不要放在中心化交易所上。在重要账户上设置比 SMS 验证更多的层次。安全层可以是 2FA 认证、电子邮件验证和 IP 限制。

作为一名开发者，密码破解是获取 Web 应用访问权限的最常见方式。实现一个安全测试员，确保系统要求强加密密码。

此类解决方案的一个好例子是 John the Ripper 密码破解器：[`github.com/magnumripper/JohnTheRipper`](https://github.com/magnumripper/JohnTheRipper) 。

此外，实施以下措施：

+   保护凭据：使用多重层保护你的用户凭据。

    +   强密码：在账户创建时强制使用强密码并重置密码。

    +   启用 2FA：设置双因素认证（也称为启用 2FA）；一个流行的例子是 Google 认证器。

    +   确认：在进行重要操作（如转账）时，要求短信确认和电子邮件验证。

+   存储：将用户的敏感数据（如私钥）加密并存储在与互联网断开的服务器上。

+   加密：在所有页面上使用 SSL。使用 AES-256 加密。使用成本因子为 12 的哈希密码。

+   账户锁定：限制登录尝试，多次失败后锁定账户。

+   在你的开发个人电脑上：

    +   远程连接：特别是如果你远程连接到你的机器，使用强登录密码。

    +   数据加密：加密你的硬盘以开启加密。前往“系统偏好设置”并选择“隐私与安全”。点击“开启文件保险库”。

    +   非活动锁定：在“高级”标签下的“常规”中，设置五分钟非活动后登出，并通过选择“需要管理员密码才能访问系统偏好设置”来启用屏幕锁定。

    +   防火墙：在你的电脑上设置防火墙；在防火墙标签上，打开防火墙。

    +   VPN：在不安全的网络环境中使用 VPN。

    +   软件：注意你安装的软件，并确保它来自信誉良好的供应商。

    +   图书馆：尽可能避免使用 root 权限安装代码库。

#### 错误代码

错误的代码是损失的最大原因之一。它变得如此重要，以至于许多大型公司为白帽黑客发现漏洞设置了赏金，使黑客指出漏洞而不是盗窃变得有利可图。

### 注意

白帽黑客是一个道德人，他未经授权获取数据以指出系统中的漏洞。

例如，2014 年黑客利用了 Poloniex 的一个有缺陷的提现代码。公司没有分享被窃取的比特币的确切数量。

##### 事后的分析

作为开发者：

+   **SQL 注入**：通过测试和实施 SQL 注入过滤器来避免 SQL 注入。您可以在以下链接找到更多信息：[`sqlmap.org/`](http://sqlmap.org/)。

    **注意**：SQL 注入是一种攻击，黑客通过文本输入框传递非法 SQL 语句来获取内容访问权限。然后，黑客可以利用这个漏洞对 SQL 数据库进行添加、更改或删除数据。

+   **CSRF 攻击**：黑客利用服务请求来修改和检索数据以及验证 POST、PUT 和 DELETE 请求的真实性。为了避免这种情况，请遵循以下建议：

    +   **限制 IP**：将服务设置为只响应某些 IP。

    +   **设置工具和库**：在这里找到避免 CSRF 攻击的工具：[`github.com/0xInfection/XSRFProbe`](https://github.com/0xInfection/XSRFProbe)。

+   **跨站脚本攻击（XSS）**：通过使用这些工具和库来避免 XSS 攻击：

    +   [`pentest-tools.com/website-vulnerability-scanning/xss-scanner-online`](https://pentest-tools.com/website-vulnerability-scanning/xss-scanner-online)

    +   [`github.com/topics/xss-scanner`](https://github.com/topics/xss-scanner)

### 注意

跨站脚本攻击通过将恶意代码注入受信任的网站来执行。

#### 依赖后门攻击

依赖后门攻击始于社交工程攻击，并包括恶意代码的注入。

### 注意

社交工程攻击中，工程师是骗子。攻击者隐藏其真实身份和动机以获取访问或数据。例如，你收到一封似乎来自你经理的合法邮件，要求提供特定信息。

例如，2018 年下半年，一名黑客成功地将恶意代码插入到 npm JavaScript 库 event-stream 中（ [`www.npmjs.com/package/event-stream`](https://www.npmjs.com/package/event-stream) ）。这个库由数百万人使用，针对一家名为 Bitpay 的公司，该公司有一个 Git 库叫 copay。copay 是一个在 GitHub 上托管的开源钱包（ [`github.com/bitpay/copay`](https://github.com/bitpay/copay) ）。

与许多开源库一样，开发者没有为在 event-stream 上的工作获得报酬，并在将其交给新的维护者之前失去了对项目的兴趣。新的维护者注入了针对 copay 的恶意代码。该代码捕获了拥有超过 100 个比特币或 1000 个比特币现金余额的账户的账户详细信息和私钥。copay 然后在版本 5.0.2 上更新了其依赖库，并包含了攻击者代码，导致了数百万的损失。

代码捕获了受害者的账户数据和私钥，然后，通过服务调用，将数据发送到攻击者的服务器而不被察觉。

这次攻击的详细信息和分析可以在这里找到：[`snyk.io/vuln`](https://snyk.io/vuln)

+   关于事件流事件的详细信息，请参阅：[`blog.npmjs.org/post/180565383195/details-about-the-event-stream-incident`](https://blog.npmjs.org/post/180565383195/details-about-the-event-stream-incident)

+   关于恶意事件流后门的死后分析，请参阅：[`snyk.io/blog/a-post-mortem-of-the-malicious-event-stream-backdoor/`](https://snyk.io/blog/a-post-mortem-of-the-malicious-event-stream-backdoor/)

##### 事后分析

作为用户，如本章中所建议的那样，将加密货币存放在冷钱包中。作为开发者，在处理开源库时要小心。开源模型依赖于许多包，但支持库的开发者很少，这可能使恶意接管成为可能。为了帮助避免这种情况，运行 npm audit 以检测任何易受攻击的依赖项。> npm audit

请检查并在漏洞数据库（如 snyk.io 网站）上测试你的代码，以查找任何已报告的漏洞：[`snyk.io/vuln`](https://snyk.io/vuln) 。

不要将你的 package.json 文件设置为包括库的自动更新。"dependencies": { "some-library": "latest" } 相反，检查你想要更新的库的 pull 请求，并手动检查你使用的依赖项的变化。使用库特定的版本。"dependencies": { "some-library": "1.0.0" }这适用于 npm install。安装特定的库，特别是对于不太知名的库。> npm install -g some-library@1.0.0

#### DoS 和 DDoS 攻击

*拒绝服务*（DoS）攻击是一种常见的攻击手段，旨在阻止用户访问服务。*分布式拒绝服务*（DDoS）攻击与 DoS 攻击类似，但不同之处在于，攻击者不是利用单台机器进行攻击，而是利用多台机器同时进行攻击。由于使用了多台机器，成功攻击的概率增加，而且攻击者的确切位置更难以确定。

交易所和网站是 DoS 和 DDoS 攻击的热门目标。例如，当比特币黄金正式推出时，它遭到了 DDoS 攻击，最终导致网站瘫痪数小时。

流行的区块链网络有一个简单的内置 DoS 预防机制；然而，许多网络对更复杂的攻击没有保护。

最常见的攻击类型如下：

+   *缓冲区溢出*：这种攻击向目标服务发送比服务能够处理更多的流量。这种攻击可以使攻击者获得使目标服务崩溃甚至控制目标服务的能力。

+   *ICMP 洪水*：也被称为“死亡 ping”或“蓝屏攻击”，这种攻击旨在通过迫使节点向所有节点分发伪造数据包来过载网络。

+   *SYN 洪水*：发送一个连接请求，但它从未完全认证。请求者然后攻击服务器上所有打开的端口，直到服务器崩溃。

+   *NTP/DNS 放大攻击*：这是一种针对 NTP 服务器的攻击，攻击者发送大量的 UDP 数据包，并伪造源 IP 地址，使 NTP 服务器相信这些数据包是来自预期目标的合法流量。这种过载导致 NTP 服务器崩溃。

##### 事后分析

作为一名开发者，你需要考虑 Dos/DDoS 攻击，并实现针对它们的对策。以下是一些例子：

+   *过滤恶意流量*：

    +   *脚本*：防止的一种方法是实现一个脚本来检查 DOS/DDOS 攻击。查看 GitHub 的 DDOS 保护库：[`github.com/topics/ddos-protection`](https://github.com/topics/ddos-protection)。[`vddos.voduy.com/`](http://vddos.voduy.com/) 是一个流行的选择。

    +   *防火墙*：使用防火墙来阻止恶意流量。参见图 11-6。![../images/475651_1_En_11_Chapter/475651_1_En_11_Fig6_HTML.jpg](img/475651_1_En_11_Fig6_HTML.jpg)

        图 11-6

        DDoS 保护反向代理解释。图片来源：vddos.voduy.com。

+   *专用硬件*：购买并部署专用硬件来处理 DDoS 攻击的缓解。这种硬件位于数据中心的服务器和路由器前面，可以检测和过滤恶意流量。此类硬件的一个例子是来自[www.fortinet.com](http://www.fortinet.com)的 FortiDDoS。

+   *ISP*：ISP 为用户提供 DDoS 缓解解决方案。例如，亚马逊提供了一个保护层，所有 AWS 客户都能从中受益于自动保护，并提供针对攻击的高级保护层；参见[`aws.amazon.com/shield`](https://aws.amazon.com/shield)。

+   *云缓解*：一些云服务提供 DDoS 缓解。这些服务清洗流量以消除任何恶意流量。一个流行的提供商是[cloudflare.com](http://cloudflare.com)，它提供免费的标准化版本和付费的企业解决方案。

在区块链网络 DDoS/DoS 攻击方面，检查现有区块链预防实现，例如比特币中继客户端保护，在 0.7.0 版本中实现；参见[`en.bitcoin.it/wiki/Weaknesses`](https://en.bitcoin.it/wiki/Weaknesses)。

总结来说，我回顾了针对平台的常见攻击。您查看了凭据攻击、错误代码、依赖后门攻击以及 DoS/DDoS 攻击。此外，我还回顾了帮助您降低风险和预防这些攻击的方法。在下一节中，我将向您提供一个建议的开发周期，您可以采用它来帮助降低风险，并使用系统化的方法来防止攻击。

## 开发周期

正如您在本章中所看到的，您的平台需要安全并保护免受潜在攻击的侵害。您不能依赖运气，需要确保您使用所有可用的措施来降低平台遭受攻击的风险，并确保您实施所有最新的与您地区相关的法规。

该过程可以分为以下几个阶段：

+   进行*设计和编码*

+   进行*发现、审计和测试*

+   进行*准备情况评估*

+   进行*发布*

从图 11-7 中可以看出，每个阶段可能导致回到设计和编码阶段，因为发现可能会导致安全风险或障碍物。![../images/475651_1_En_11_Chapter/475651_1_En_11_Fig7_HTML.jpg](img/475651_1_En_11_Fig7_HTML.jpg)

图 11-7

减少安全和合规风险的推荐开发周期

### 提示

此开发是一种基本的开发生命周期方法。您可以自由地使用自己的方法或更适合您的平台和需求的不同方法。

### 设计和编码

在设计和编码阶段之前和期间，您应该融入本章前面部分讨论的所有安全、隐私和合规要素。这些应该考虑您平台的各个元素，包括页面、登录系统、隐私页面、与第三方插件的集成、服务的创建、服务器的设置等。

您创建一个检查列表，列出需要融入和考虑的所有内容，这特别适用于您独特的平台是一个好主意。不可能有一个适合一切的列表。每个平台都应该有一个独特的检查列表。另外，当您开始一个新的开发周期时，您可能需要更新要求。例如，假设您希望您的平台支持新的地区；这将需要一个新的检查列表。

### 发现、审计和测试

这一步骤可以分为三个步骤。这些步骤相互交织，相互依赖，因此您应该将这些步骤视为一个阶段。这些步骤如下：

+   进行*发现*：找出您平台中使用的各种版本，如库版本、固件版本、软件版本、第三方 SDK 版本等。

+   进行*审计*：审计您的代码和平台，以发现常见问题、服务的可访问性以及可能降低性能并使您的平台无法访问的性能问题。

+   **测试**：这是针对您的平台运行实际测试的情况。目的是确定您的平台正在使用哪些系统和潜在的安全漏洞。

### 发现

发现阶段是关于发现您平台中使用哪些版本的问题。例如，您需要运行一个发现阶段来找出您正在使用的固件版本。了解版本信息在某个版本被标记为安全漏洞或已经过时的情况下非常有价值。发现阶段随后可以用来进行审计和测试，并提供您平台中可能存在的潜在漏洞的指示。

您可能会在发现检查过程中发现，由于版本问题，您需要回到编码和设计阶段。例如，一旦您更改了一个库或固件的版本，您的代码可能会中断，您可能需要重构您的代码。

### 审计

在审计阶段，您应该对具体的潜在问题进行系统审查。

正如会计师审计公司的财务方面，甚至这本书也由一个团队进行审计一样，您的平台需要进行审计和测试，以确保您的代码遵循最佳实践，从而提高性能、可访问性，并符合安全性和监管要求。

审计检查可以由您自己的平台团队完成，但通常由一个独立的实体完成。重要的是要认识到，审计无法期望检测到所有需要解决的问题。基于区块链的平台还应考虑安全性和合规性审计。

#### 安全审计

安全审计可以采用完全的手动方法，也可以利用自动化工具进行漏洞评估、安全评估和渗透测试，以确定需要解决的问题。有超过 1500 个利用方式，因此依赖自动化审计工具至少在一定程度上作为您开发周期的一个组成部分，并确保您的平台能够通过常见问题的测试，这是一个好主意。即使雇佣第三方审计师，开始更严格的审计之前，最好先检查常见问题。

#### 合规审计

在区块链中，您需要检查的不仅仅是安全方面；您还需要进行合规性审计，以确保根据法律实施隐私和合规性。

就像安全审计一样，合规审计可以由第三方审计师或内部进行。正如您在本章前面所看到的，许多在不同地区引起立法者关注的问题与安全漏洞有关。如我所说，合规规定可能会经常变化，并且在不同地区之间也有所不同，因此，合规评估通常以手动方式进行比自动化方式进行要好。

### 测试

发现和审计依赖于测试来提出建议，以解决您平台中的问题。在测试方面，有三种类型。

+   [`www.wireshark.org/`](https://www.wireshark.org/)

+   静态测试：这是一种由内而外的方法，用于测试平台源代码中的漏洞。这种测试为您提供了平台及其组成库的更深入的实时快照。

+   渗透测试：这种测试模拟实际的恶意攻击。渗透测试可以依赖发现的漏洞进一步访问您的平台。这可以帮助您了解攻击者可以获取机密信息的途径。

测试可以通过自动化工具进行，但建议您还包括由实际测试人员进行的手动测试，他们可以依靠自己的经验和知识找到自动化工具未发现的漏洞。

#### 自动化工具

![../images/475651_1_En_11_Chapter/475651_1_En_11_Fig8_HTML.jpg](img/475651_1_En_11_Fig8_HTML.jpg)

图 11-8

Google Chrome 开发者工具审计报告

浏览器的开发者工具提供了一个简单的网络代理工具；然而，这些工具没有你可能需要的许多功能，如导出数据、运行仿真和过滤数据。在审计阶段，你可能发现使用第三方网络代理工具很有用。网络代理工具主要是一个网络协议分析器，可以提供你的网络协议、数据包信息、解密等详细信息。两个流行的工具是 Charlesproxy 和 Wireshark。

+   [`www.charlesproxy.com/`](https://www.charlesproxy.com/)

+   有许多测试工具可以帮助你进行这三种测试。例如，对于库的静态测试，我已经提到了 npm audit，它帮助检测依赖版本中的任何漏洞。

在自动化渗透工具方面，有很多工具可供选择。以下是一些流行工具的示例：

1.  1.安全自动化工具

    1.  动态测试：检测攻击者可能针对的漏洞。试图利用你平台的攻击者无法访问你的代码和平台，所以这些测试是在不访问你的源代码的情况下运行的。

        [`www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project`](http://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project)

    1.  b.

        [`www.portswigger.net/burp`](http://www.portswigger.net/burp)

1.  2.

    [`www.rapid7.com/products/metasploit/download/editions/`](https://www.rapid7.com/products/metasploit/download/editions/)

1.  3.

    *CORE Impact*：Core Impact Pro 测试移动设备渗透、密码识别、破解等。它还有图形用户界面和命令行界面，但价格昂贵。详见[`www.coresecurity.com/core-impact/`](https://www.coresecurity.com/core-impact/)。

1.  4.

    *Netsparker*：这包括一个网络应用扫描器，可以帮助识别访问敏感数据等漏洞，并建议解决方案。它包括 SQL 注入和本地文件诱导（LFI）。渗透测试制造内部或外部未授权攻击。详见[`www.netsparker.com/`](https://www.netsparker.com/)。

1.  5.

    *谷歌免费的网络安全工具（ratproxy）：详见* [`code.google.com/archive/p/ratproxy/`](https://code.google.com/archive/p/ratproxy/) *.*

1.  6.

    *Kali Linux 操作系统（OS）*：这个工具适合黑客，已经预装了许多黑客工具。该操作系统作为虚拟机安装在您的 Mac/PC 上。

1.  7.SQL 注入：

    1.  a.

        *SQLmap*：这是一个开源的自动化渗透测试工具，用于检测和利用 SQL 注入。详见[`sqlmap.org`](https://sqlmap.org)。

    1.  b.

        *SQLNinja*：这个工具用于检查针对微软 SQL 服务器的 SQL 注入漏洞。详见[`sqlninja.sourceforge.net`](https://sqlninja.sourceforge.net)。

    1.  c.

        名为 Hackbar 的*火狐浏览器插件*：这个测试帮助您测试网站安全，包括 SQL 注入和 XSS 漏洞。详见[`www.addons.mozilla.org/en-US/firefox/addon/hackbartool/`](https://www.addons.mozilla.org/en-US/firefox/addon/hackbartool/)。

### 注意

文件包含允许攻击者通过利用动态文件包含（如 jQuery 的$.getScript）来插入文件，该功能是在应用程序中实现的，以包含另一个文件。然后用户输入上传文件，并且没有适当的验证来检查文件。解决方案是实现动态文件包含的验证，以确保来源和内容。

有许多安全测试自动化工具需要列表；然而，您可以在网上找到一些精选的安全测试自动化工具列表，这些工具适合您要运行的精确测试：

+   [`github.com/topics/testing-tools`](https://github.com/topics/testing-tools)

+   [`github.com/atinfo/awesome-test-automation`](https://github.com/atinfo/awesome-test-automation)

+   [`forum.bugcrowd.com/t/researcher-resources-tools/167`](https://forum.bugcrowd.com/t/researcher-resources-tools/167)

遵循 OWASP IoT 测试指南和 OWASP IoT 测试资料建议：

+   打印并遵循：[`www.owasp.org/images/2/2d/Iot_testing_methodology.JPG`](https://www.owasp.org/images/2/2d/Iot_testing_methodology.JPG)

+   遵循这个检查表：[www.owasp.org/index.php/IoT_Testing_Guides](http://www.owasp.org/index.php/IoT_Testing_Guides)

在发现、审计和测试阶段，您很可能会发现小到主要的安全漏洞，这可能需要您回到编码阶段，重复这个过程，直到您的平台通过所有测试。

### 准备评估

一旦您的平台通过了发现、审计和测试阶段，您就准备好深入研究区块链应用程序的技术方面，以确保已经实施了安全和合规性。这是通过手动运行安全和合规性评估来完成的。

#### 安全和合规性评估

这个评估建立在你在之前阶段进行的安全漏洞评估的基础上。在发布之前，建议你增加一个手动验证步骤，以确认您的平台已经应用了行业和/或内部安全标准，并评估风险和暴露。这个阶段还应该包括我在本章第一部分讨论的安全准备问题。

此外，验证可能还会检查以下内容：

+   检查对您平台的授权访问并确认系统设置

+   检查平台和服务器日志

+   确保符合当前的法规

+   检查和跟踪错误代码和消息

+   检查最新的隐私和法律

+   检查设计和技术文档，确保代码符合这些要求

+   执行代码审查

记住，安全和合规性评估是要考虑的更广泛画面，你不应该只关注一个漏洞的具体暴露。相反，应该把整个平台考虑在内。评估可能会发现一些不可接受的其他风险和暴露，这将需要你回到设计编码阶段，重新开始这个过程。

### 发布

一旦您的平台通过了准备评估阶段，就可以发布您的平台。建议您在实际生产代码上再次运行相同的测试和检查，以确保平台仍然通过测试和评估。一旦您完成了这个周期，您可以为新的开发周期重复这个流程。

## 从这里开始做什么

+   关于区块链安全的相关链接，有一个很好的在线资源：[`github.com/1522402210/BlockChain-Security-List`](https://github.com/1522402210/BlockChain-Security-List)。

+   根据您的特定平台和地区创建一个合规性和安全检查表。

+   如果您有一个平台/网站，请在您现有的平台或网站上运行审计和自动化测试工具。

## 总结

在本章中，我将区块链过程的安全性和合规性分为三部分：安全准备，常见的区块链攻击和一个推荐的开发周期。

第一部分作为引言，以便你更好地理解构建安全平台的相关术语和心态。我介绍了安全测试和合规准备，特别是研究了美国和欧盟的合规要求作为例子。我涵盖了在设计和编码阶段应考虑的安全准备建议。然后我介绍了导致数十亿美元损失的常见区块链攻击。这些攻击主要针对加密货币钱包，但也包括区块链网络和基于区块链的平台。最后，我给出了一个建议的开发周期，以确保你考虑所有必要的安全和合规问题。

在下一章也是最后一章中，你将探索区块链不仅仅是加密货币。我将介绍区块链的力量以及如何利用它，以及特定行业的去中心化，研究几个被区块链颠覆的行业和具体的案例研究。