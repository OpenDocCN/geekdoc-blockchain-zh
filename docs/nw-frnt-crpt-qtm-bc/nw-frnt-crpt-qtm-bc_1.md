© 编辑（如适用）和作者，独家许可给 Springer Nature Switzerland AG 2020。K. S. Mohamed《密码学的新前沿》[`doi.org/10.1007/978-3-030-58996-7_1`](https://doi.org/10.1007/978-3-030-58996-7_1)

# 1. 网络安全介绍

卡里德·萨拉赫·莫哈迪^1（1）Siemens Business，美国加利福尼亚州弗里蒙特关键词机密性完整性可用性漏洞威胁网络安全攻击加密 SSLIPSec 如今，密码学在每个电子和通信系统中都发挥着至关重要的作用。每天，许多用户通过互联网、电话对话和电子商务交易在各个领域生成和交换大量信息。在现代片上系统（SoCs）中，网络安全在保护信息的机密性和完整性方面发挥着至关重要的作用。*网络安全* 是保护计算机、服务器、移动设备、网络、电子设备和数据免受恶意攻击的影响 [1]。近年来，对数据安全的威胁数量不幸地和破坏性地增长。主要有三种对数据安全的威胁 [2，3]：

+   盗取它们（机密性/隐私）。

+   修改它们（完整性）。

+   你被阻止获取它们（访问/可用性）。

任何安全系统的目标都是禁止这些威胁。有许多实现此目标的技术，如加密和数据隐藏。我们将在本书中涵盖它们。

## 1.1 安全术语

+   *机密性* 指的是保护信息，例如计算机文件或数据库元素，以便只有授权人员可以以受控的方式访问它 [4]。

+   *完整性* 意味着除非使用适当的授权，否则不能修改信息。*可用性* 意味着在授权人员需要时信息存在，并且使用适当的安全措施访问。

+   *漏洞* 意味着安全系统的弱点。

+   *威胁* 是一系列可能导致损失或伤害的情况。

+   *攻击*是人类利用系统中的漏洞进行的行为 [5]。

+   *特洛伊木马*是表面上表现正常但具有恶意副作用的软件。

+   *病毒*是一种自我传播的特洛伊木马；会感染其他软件。

+   *蠕虫*是一种在网络上传播的病毒。

## 1.2 安全威胁/攻击

安全意味着没有风险或危险。一般来说，没有什么是 100%安全的。在足够的时间、资源和动机下，攻击者可以破坏任何系统。数据安全面临许多威胁（图 1.1）：

+   *拦截*：窃取它们（保密/*隐私攻击* ），即，*窃听（非破坏性）。*

+   *修改*：修改它们（完整性攻击），即 *在连接中插入* 消息（破坏性）。 *劫持* 通过删除发送者或接收者，将自己插入攻击者位置，接管正在进行的连接。也称为数据伪造或伪造数据 [6, 7]。

+   *中断*：你被阻止获取它们（访问/*可用性攻击* ），即，*拒绝服务 (DoS)* 因为攻击者可以阻止其他人使用服务（例如，通过过度加载资源）。

![../images/501530_1_En_1_Chapter/501530_1_En_1_Fig1_HTML.png](img/501530_1_En_1_Fig1_HTML.png)

图 1.1

安全攻击和威胁

网络犯罪是通过互联网或其他形式的计算机技术协助的犯罪行为。在涉及到机密信息被截取或披露时，网络犯罪存在许多隐私问题，无论是合法还是非法 [8]。

## 1.3 安全要求/服务/目标/目的

下面我们描述了克服安全威胁的主要安全要求（图 1.2）：![../images/501530_1_En_1_Chapter/501530_1_En_1_Fig2_HTML.png](img/501530_1_En_1_Fig2_HTML.png)

图 1.2

安全目标的交叉点

### 1.3.1 机密性

指的是保护信息（如计算机文件或数据库元素）的方式，以便只有经过授权的人员可以以受控的方式访问它。保密性确保消息被编码以将其隐藏，因此发送者将消息（明文）加密以创建传输的密文。拥有加密密钥的接收者将密文解密为原始明文。

### 1.3.2 认证

认证回答了以下问题：“接收者如何知道远程通信实体是它所声称的？”。它也被称为*识别*。如今，大多数加密算法都支持认证加密（AE）或带相关数据的认证加密（AEAD）。这基本上意味着数据的机密性和真实性都得到了保证。在提及 AEAD 方案时，假定接收者能够验证加密和解密消息的完整性。为了更进一步澄清这一点，相关数据（AD）被用来将密文绑定到它所应该的上下文。因此，任何试图将有效的密文与不同的上下文放置在一起的尝试都是可检测的，并且可以被拒绝。

### 1.3.3 完整性

指的是除非使用适当的授权，否则无法修改信息。发送的信息和数据不能在存储或在源和目标之间的传输过程中被修改，以至于无法检测到更改。数据完整性确保接收到的消息与发送者发送的消息完全相同。这可以通过使用哈希函数（如 SHA256）来实现，该函数从原始消息创建一个唯一的摘要，并与消息一起发送。

### 1.3.4 访问控制/授权

谁可以做什么。访问控制是控制谁做什么的过程，从管理设备的物理访问到指定谁可以访问资源（如文件）及其可以做什么（如读取或更改文件）。许多安全漏洞是由不正确使用访问控制造成的。

### 1.3.5 可用性

指授权人员需要时可以访问信息，并使用适当的安全措施进行访问。

### 1.3.6 不可否认性

确保合同或通信的一方不能否认其在文档上的签名的真实性或发送的消息的真实性。你不能否认你做过的事情。通常，这是发送方不能否认传输的消息有效性的保证。这是通过使用数字签名（尤其是在线交易中使用的）和消息认证码实现的，后者基本上是包含密钥的哈希函数。应注意，这种加密原语也以比简单哈希函数更强大的方式确保信息的完整性。

当实现所有这些目标时，系统是安全的（图 1.2）。

## 1.4 安全机制/工具/防御

安全工具总结如下（图 1.3）：

+   *密码算法*（表 1.1）：可以是对称（一个共享密钥）或非对称算法（我们有两个密钥：一个是秘密的，另一个是公开的）[9, 10]。

+   *身份认证* *:* 用户真实身份。通过数字签名实现。

+   *公钥/私钥*：公开公钥。用此加密。用私钥解密。

+   *哈希* *:* 创建数据集的唯一、固定长度的签名（哈希）。

+   *数字签名* *:* 用私钥加密哈希值。用公钥解密。加密不能确保完整性。

+   *密码* *:* 你知道的东西。应该足够复杂。

+   *防火墙* *：防火墙就像一座带有吊桥的城堡。网络只有一个访问点。

+   *可信第三方* *：可信第三方可以发布声明，例如“持有此密钥的人是法律上认可的人。”

![../images/501530_1_En_1_Chapter/501530_1_En_1_Fig3_HTML.png](img/501530_1_En_1_Fig3_HTML.png)

图 1.3

安全服务和工具

表 1.1

加密算法的分类

|   | 对称算法 | 非对称算法（公钥/私钥） | 散列算法 |
| --- | --- | --- | --- |
| 示例 | DES, AES, 3DES, RC5 | RSA, ECC, DH, ECDH | MD4, HMAC, SHA-1 |
| 数学 | 表查找置换乘法模加模乘固定位移/旋转可变位移/旋转 | 模指数椭圆曲线上的点乘 | 乘法加法逻辑运算固定位移/旋转 |

## 1.5 安全层级/级别

计算系统是硬件（HW）、软件（SW）、存储介质、数据、网络以及与其交互的人的集合。我们需要保护软件、数据和通信，以及硬件（图 1.4）。![../images/501530_1_En_1_Chapter/501530_1_En_1_Fig4_HTML.png](img/501530_1_En_1_Fig4_HTML.png)

图 1.4

安全层级示例

安全层级的另一个视角如图 1.5 所示。漏洞可能发生在硬件、软件和数据级别[11, 12]。![../images/501530_1_En_1_Chapter/501530_1_En_1_Fig5_HTML.png](img/501530_1_En_1_Fig5_HTML.png)

图 1.5

安全层级。另一个视角

+   *硬件漏洞：* 添加设备，更改它们，移除它们，拦截发送至它们的流量，或者向它们发送大量流量直到它们无法正常工作。硬件漏洞通常由硬件设计缺陷引入。例如，RAM 内存本质上是安装在彼此非常接近的电容器。人们发现，由于接近性，对其中一个电容器的不断更改可能会影响相邻的电容器。基于这个设计缺陷，一个称为 Rowhammer 的漏洞被创建出来。通过反复在相同地址重写内存，Rowhammer 漏洞允许从附近地址的内存单元中检索数据，即使这些单元受到保护。

+   *软件漏洞：* 软件可能被恶意替换、更改或破坏，也可能被意外地修改、删除或丢失。无论是故意还是无意的，这些攻击都利用了软件的漏洞。*恶意软件*是指任何可用于窃取数据、绕过访问控制或对系统造成伤害或威胁的代码，如间谍软件和勒索软件。软件漏洞通常是由操作系统或应用程序代码中的错误引入的；尽管公司为发现和修补软件漏洞付出了所有的努力，但新的漏洞仍然很常见。微软、苹果和其他操作系统生产商几乎每天都发布补丁和更新。应用程序更新也很常见。诸如网络浏览器、移动应用程序和网络服务器等应用程序通常由负责它们的公司或组织更新。*钓鱼*是指恶意方发送伪装成来自合法、可信任来源的欺诈性电子邮件。消息的目的是欺骗收件人在其设备上安装恶意软件或共享个人或财务信息。钓鱼的一个例子是伪造成来自零售商的电子邮件，要求用户点击链接来领取奖品。该链接可能会跳转到一个虚假网站，要求提供个人信息，或者安装病毒。 

+   *数据漏洞：* 机密数据泄露给竞争对手。

嵌入式系统攻击的不同类型示例如图 1.6 所示。IP 保护也是一个重要话题。没有 IP 保护，公司可能会损失收入和市场份额。![../images/501530_1_En_1_Chapter/501530_1_En_1_Fig6_HTML.png](img/501530_1_En_1_Fig6_HTML.png)

图 1.6

嵌入式系统攻击[13]

IP 供应商面临着保护硬件 IP 免受 IP 盗版的重大挑战，因为最近 IP 盗版和逆向工程努力生产伪造 IC 的趋势已经引起了 IC 设计社区的严重关注。IP 盗版可以采取几种形式，如下所示：

1.  1.

    一个芯片设计公司从一个 IP 供应商那里购买了一个 IP 核，并制作了一个违法的复制品或“克隆”该 IP。然后 IC 设计公司在进行微小修改后将其销售给另一个芯片设计公司，并声称该 IP 是自己的。

1.  2.

    一个不可信任的制造厂商制作了一个芯片设计公司提供的 GDS-II 数据库的违法副本，然后非法将其作为硬件 IP 出售。

1.  3.

    一个不受信任的晶圆厂商制造并销售 IC 的伪造副本，并以不同的品牌名称销售。

1.  4.

    一个对手对 IC 进行后硅逆向工程，以制造其非法克隆品。

这些情景表明，参与 IC 设计流程的所有方都容易受到不同形式的知识产权侵犯的影响，这可能导致收入和市场份额的损失。因此，迫切需要一种防盗版的设计流程，既有利于 IP 供应商、芯片设计者，又有利于系统设计者。这样一个安全设计流程的一个可取特点是，它应对最终用户透明，即，它不应对最终用户的使用、成本或性能施加任何限制。

要保护 IP，我们需要对其进行混淆，然后在发送给客户之前加密内容。*混淆*是一种将应用程序或设计转换为在功能上等效于原始设计但在逆向工程上更加困难的技术。因此，混淆将所有信号的名称更改为数字和字符的组合。第二级别是对整个文件进行加密。尽管加密是有效的，但代码混淆是一种有效的增强技术，可以进一步阻止攻击者理解代码。此外，*水印*可以用于保护软 IP。它包括模块复制或模块分割。对于 ASIC，电路伪装是使用的一种方法。*电路伪装*使得单个逻辑单元在每个掩模层中看起来是相同的，但实际上存在微小的更改来区分逻辑功能。这些更改被设计成使得逆向工程师无法自动识别单元。为了保护 PCB，我们将 PCB 封装到环氧树脂（黑色斑点）中，并添加了一些虚假的层以增加复杂性。

## 1.6 数学背景

### 1.6.1 模算术

在模算术中，我们将任何计算的乘积（加法、乘法）映射到一组有界的整数中。这个界限由*模数*（或基数）定义。设*a, r, m*为整数，*m > 0*，那么

+   如果*m*整除*a − r*，则*a* ≡ *r* mod *m*。一个例子是 43 ≡ 1 mod 7。

### 1.6.2 最大公约数

假设我们需要找到 gcd (*r*[0], *r*[1])。一个解决方案是对*r*[0]、*r*[1]进行因式分解，然后 gcd 应该是最大公因数。对于大数来说，因式分解是复杂且困难的。下面是一个示例：

+   *r*[0] = 72 = 2 × 2 × 3 × 7，*r*[1] = 24 = 2 × 3 × 4，那么 gcd (*r*[0], *r*[1]) = 6。

## 1.7 安全协议

协议是由两个或多个实体执行的一系列步骤。安全协议是在不受信任的环境中运行并尝试实现安全目标的协议。安全协议的示例包括*IPSec*和*SSL*。如今，通过互联网进行数据加密时，HTTPS（安全超文本传输协议）协议使用 SSL/TLS-based 加密来创建安全通道以共享数据。HTTPS 使用的加密协议 TLS（传输层安全）和 SSL（安全套接字层）使用了非对称加密，它使用一对密钥发送信息，更可靠地验证接收者。

### 1.7.1 SSL

它是广泛部署的安全协议，几乎所有浏览器、网络服务器都支持。此外，它适用于所有 TCP 应用程序 [14]。SSL 在 OSI 模型的*表示层*（第 6 层）运行，如图 1.7 所示 [15]。公钥加密是安全套接字层的核心，这是互联网上另一种常见的加密形式。在 SSL 连接中，您的计算机和目标计算机扮演两个通信者的角色，交换公钥并对两台计算机之间传输的所有数据进行编码。这确保文件传输和其他通信保持安全，尽管外部人员仍然可能通过查看公共数据包信息来确定传输的性质——例如，数据包的目的地端口可能会透露传输的类型，因为大多数 Internet 协议使用易于识别的端口号。![../images/501530_1_En_1_Chapter/501530_1_En_1_Fig7_HTML.png](img/501530_1_En_1_Fig7_HTML.png)

图 1.7

开放系统互连（OSI）模型

### 1.7.2 IPSec

它是 Internet 工程任务组（IETF）在 IP 网络上两个通信点之间的标准协议套件，提供数据认证、完整性和机密性。它还定义了加密、解密和认证数据包[16, 17]。SSL 和 IPSec 都拥有强大的安全基因，具有可比较的吞吐速度、安全性和易用性，适用于大多数商业 VPN 服务的客户[18]。IPSec 在 OSI 模型的*网络层*上工作（图 1.7）。OSI 模型中有七个层级的层次结构，即：

1.  1.

    物理层

1.  2.

    数据链路层

1.  3.

    网络层

1.  4.

    传输层

1.  5.

    会话层

1.  6.

    表示层

1.  7.

    应用层

IPSec 加密可能会导致显著的网络瓶颈，而第二层加密几乎不会给网络带来延迟或额外开销。

## 1.8 结论

本章讨论了密码学的基础知识。它全面研究了安全的三个关键方面：保密性、完整性和认证。密码学在实现安全目标方面发挥着至关重要的作用，如认证、完整性、保密性和不可否认性。密码算法的开发旨在实现这些目标。