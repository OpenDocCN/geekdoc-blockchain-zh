编辑：R. Lakshmana Kumar、Yichuan Wang、T. Poongodi 和 Agbotiname Lucky Imoize

# 互联网物联网、人工智能和区块链技术

第一版 2021![../images/504166_1_En_BookFrontmatter_Figa_HTML.png](img/504166_1_En_BookFrontmatter_Figa_HTML.png)出版商标志编辑 R. 拉克什曼纳·库马尔印度泰米尔纳德邦钦那伊维斯坦学院工程与技术 Yichuan 王谢菲尔德大学管理学院，英国谢菲尔德大学 T. 普恩戈迪计算机科学与工程学院，加尔各答大学，德里-全球通信与经济复苏倡议 Agbotiname Lucky Imoize 拉各斯大学，尼日利亚拉各斯 ISBN 978-3-030-74149-5e-ISBN 978-3-030-74150-1[`doi.org/10.1007/978-3-030-74150-1`](https://doi.org/10.1007/978-3-030-74150-1)© 编辑（如果适用）和作者（如果适用），独家许可给施普林格自然瑞士公司 2021 此作品受版权保护。出版商仅独家许可，无论是整体还是部分材料，具体包括翻译权、再版、插图重用、朗诵、广播、微缩胶片复制或以任何其他物理方式复制，以及传输或信息存储和检索、电子适配、计算机软件或通过已知或今后开发的类似或不同方法进行的类似方法。在本出版物中使用通用描述性名称、注册名称、商标、服务标记等，并不意味着即使在没有特定声明的情况下，这些名称也免于相关的保护法律和法规，并因此可以自由使用。出版商、作者和编辑可以安全地假定本书中的建议和信息被认为在出版日期属实和准确。出版商、作者或编辑对本文所含材料或可能存在的任何错误或遗漏不提供明示或暗示的担保。出版商在已发表的地图和机构隶属方面保持中立。

该 Springer 子品牌由注册公司 Springer Nature Switzerland AG 发行。

注册公司地址为：瑞士 Cham，Gewerbestrasse 11，6330。

前言

区块链、物联网和人工智能联盟在第四次工业革命中的重要性，激发了当代社会生活的本质。互联网用户之间的协同作用可能构成一种重要影响，利用区块链中的智能合约，而这些原则的结合坚持合理可能在多个领域是前所未有的。在这本书中，我们尽力探讨了物联网、人工智能和区块链的理论和程序。第一章中，我们定义了物联网架构、通信技术及其应用。第二章讨论了超级账本框架、工具和应用程序。第三章提供了网络韧性能源基础设施和物联网。第四章展示了人工智能、物联网和区块链：商业模型、道德问题和法律视角。第五章考察了应用区块链技术涉及的法律问题。基于物联网的个性化医疗生物医学传感器在第六章中给出。第七章调查了 AIOT 在一致性或融合方面的巨大结合。第八章讨论了物联网、人工智能和区块链技术在工业 4.0 中的影响。使用区块链技术维护电子健康记录（EHRM）在第九章中进行了讨论。在第十章中，针对基于人工智能的临床决策支持工具的区块链安全进行了检查。在第十一章中给出了用于改善临床过程安全系统的决策支持机制，使用了区块链技术。在第十二章中，对情感分析的堆叠嵌入案例研究进行了制定，并将模型命名为 Bi-GRU 模型。在第十三章中，探讨了使用大数据分析进行心脏病预测的系统性框架。在最后一章中，讨论了人工智能和尼日利亚法律实践的未来。

R. Lakshmana Kumar 印度泰米尔纳德邦科伊马托尔致谢 R. Lakshmana Kumar

首先，我要感谢全能者帮助我编辑这本书。没有 Hindusthan 工程技术学院的合作，我就不可能在过去的八年多中在项目、研讨会和咨询项目中开发和测试洞察力相关的想法。我要感谢 Hindusthan 机构的管理层，他们一直鼓励我“完成这本书”。在任何层面上的任何尝试都不能圆满完成，没有家人和朋友的支持和指导。我深感不胜感激地承认所有帮助我将这些想法提升到简单之上、变成具体形态的人。另外感谢 Springer 家族，我对他们的出色编辑支持和指导深感感激。

王一川

我要感谢所有合著者，特别是领导这本书编辑项目的 Dr. Lakshmana Kumar Ramasamy。我感谢所有审阅者在审阅过程中提供宝贵意见和批评。我还感谢所有在这一领域进行研究工作的作者、投稿者。最后，特别感谢谢菲尔德大学管理学院，我有机会支持我的研究之旅，尤其是学习建立充满活力的学术网络的许多方面。

T. Poongodi

衷心感谢全能的上帝、父母、我的知识和智慧来源。特别感谢我的丈夫 Dr. P. Suresh 在每个情况下都站在我身边，以及我的儿子们，S. Nithin 和 S. Nirvin，对成功完成这本书的不断鼓励和道德支持。

我要感谢我的妈妈，Jaya Thangamuthu 女士，在我一生中给予我的不断合作。

Agbotiname Lucky Imoize

我要感谢上帝赐予我编辑这本书的智慧。 没有尼日利亚拉各斯大学和德国鲁尔大学，这本书是不可能完成的。 另外，我感谢尼日利亚石油技术发展基金（PTDF）的支持，以及德国学术交流服务中心（DAAD）通过尼日利亚-德国研究生项目。 特别感谢我的家人和朋友们的鼎力支持。 最后，我要感谢 Springer 对编辑工作的支持。

缩写列表

M2M

机器对机器

物联网

物联网

暖通空调制冷

暖通空调制冷

PIR

被动红外

QoS

服务质量

LPWAN

低功耗广域网

BLE

蓝牙

ISM

工业、科学和医学

SIG

特殊兴趣小组

个人区域网络

个人区域网络

NB-IoT

窄带物联网

RFID

射频识别

AIDC

自动识别与数据捕获

BAP

电池辅助被动

近场通信

近场通信

人工智能

人工智能

ML

机器学习

深度学习

深度学习

工作量证明

工作量证明

POS

股权证明

过去的时间证明

经过时间的证明

HDK

超级账本开发工具包

PMUs

相量测量单元

分布式拒绝服务

分布式拒绝服务

社会物联网

社交物联网

SVM

支持向量机

高级防卫研究项目局

高级防卫研究项目局

ANI

人工狭窄智能

AGI

人工通用智能

ASI

人工超级智能

数据即服务

数据即服务

服务即服务

模型即服务

机器即服务

机器即服务

BMC

商业模式画布

信息与通信技术

信息与通信技术

认识你的客户

认识你的客户

AML

反洗钱

普通数据保护条例

普遍数据保护条例

尼日利亚中央银行

尼日利亚中央银行

证券交易委员会

证券交易委员会

ICOs

初始代币发行

DATOs

数字资产代币发行

ROI

投资回报率

电子健康记录

电子健康记录

HIE

健康信息交换

FFS

服务费

AAL

环境辅助生活

医疗物联网

医疗物联网

控制剥离材料

受控剥离材料

WBANs

无线体域网

磁共振成像

磁共振成像

MEG

脑磁图

MCG

磁心电图

PPG

光电容积描记法

慢性阻塞性肺病

慢性阻塞性肺病

LPM

腰椎盆骨运动

IL

白细胞介素

氧化铪

氧化铪

HDAC

组蛋白去乙酰化酶

人工智能

人工智能

P2P

人与人

P2M

人与机器

ITU

国际电信联盟

NGN

下一代网络

WSN

无线传感器网络

SIA

软件智能与分析

自然语言处理

自然语言处理

国际英语语言测试系统

国际英语语言测试系统

PTE

皮尔逊语言测试

VR

虚拟现实

AR

增强现实

IoE

万物互联

OEMs

原始设备制造商

电子健康记录管理

电子健康记录维护

SCM

服务器-客户端机制

CDSS

临床决策支持系统

BloCHIE

基于区块链的医疗信息交换平台

FHIRchain

快速医疗互操作资源

卫生与公众服务

卫生与公众服务

HGD

医疗数据网关

ICS

使用指标为中心的方案

MPC

多方计算

AD

阿尔茨海默病

PET

正电子发射断层扫描

DSS

决策支持系统

知识库系统

基于知识的系统

个人健康记录

个人健康记录

电子健康记录

电子健康记录

RAMPmedical

应用于医疗实践的研究

QSAR

定量结构-活性关系

RD

关系数据库

SI

统计推断

SA

评分算法

SD

服务设计

DBT

数字乳腺摄影

ONC

国家卫生信息技术协调员办公室

LSTM

长短期记忆网络

GRU

门控循环单元

CNN

卷积神经网络

单字混合模型

单字混合模型

LDA

潜在狄利克雷分配

我

最大熵

自然语言工具包

自然语言工具包

RNN

循环神经网络

HFrEF

保留舒张期射血功能心力衰竭

EF

射血功能

保留收缩期射血功能心力衰竭

保留收缩期射血功能心力衰竭

MCC

移动云计算

HQL

Hive 查询语言

HDFS

分布式文件系统

自由度

自由度

ICAIL

人工智能与法律国际会议

IAAIL

国际人工智能与法律协会

COMPAS

刑事犯罪管理替代制裁剖析

SAT

律师和仲裁员工具包

TAR

技术辅助审查

RPC

职业行为准则

内容 1 物联网架构、通信技术及其应用 1T. Poongodi, R. Gopal 和 Aradhna Saini2 Hyperledger 框架、工具和应用调查 25Sweeti Sah, B. Surendiran, R. Dhanalakshmi 和 N. Arulmurugaselvi3 基于网络的弹性能源基础设施和物联网 45Divya M. Menon, S. Sindhu, M. R. Manu 和 Soumya Varma4 人工智能、物联网和区块链: 商业模式、道德问题和法律视角 67Esther Nehme, Hanine Salloum, Jacques Bou Abdo 和 Ross Taylor5 探讨区块链技术应用涉及的法律问题 89Sadiku Ilegieuno, Okabonye Chukwuani 和 Michelle Eigbobo6 基于物联网的生物医学传感器用于全面和个性化的医疗保健 111R. Indrakumari, T. Poongodi, D. Sumathi, S. Suganthi 和 P. Suresh7 大力促进的 AIoT - 一种一致性还是融合？131G. Ignisha Rajathi, R. Johny Elton, R. Vedhapriyavadhana, N. Pooranam 和 L. R. Priya8 物联网、人工智能和区块链技术在工业 4.0 中的影响 157G. Boopathi Raja9 使用区块链技术维护电子健康记录 (EHRM)179V. R. Balaji 和 J. R. Dinesh Kumar10 面向基于人工智能的临床决策支持工具的区块链安全 209S. Vijayalakshmi, Savita, S. P. Gayathri 和 S. Janarthanan11 决策支持机制以改善使用区块链技术的安全系统的临床流程 241N. Pooranam, G. Ignisha Rajathi, R. Lakshmana Kumar 和 T. Vignesh12 叠加嵌入的 Bi-GRU 模型进行情感分析: 一个案例研究 259Sanjana Kavatagi 和 Vinayak Adimule13 利用大数据分析进行心脏病预测的系统化框架 277T. Poongodi, R. Indrakumari, S. Janarthanan 和 P. Suresh14 人工智能与尼日利亚法律实践的未来 307Sadiku Ilegieuno, Okabonye Chukwuani 和 Ifeoluwa Adaralegbe 索引 327