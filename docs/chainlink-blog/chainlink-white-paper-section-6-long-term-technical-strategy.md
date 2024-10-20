# ChainLink 白皮书—第 6 节—长期技术战略

> 原文：<https://blog.chain.link/chainlink-white-paper-section-6-long-term-technical-strategy/>

[Chainlink 白皮书](https://chain.link/whitepaper)的这一节深入探讨了第 3 节中提出的理想 oracle 解决方案的一些特性。有三个主要的小节:oracle 机密性、基础设施变化和离线计算。

关于 oracle 机密性，可信硬件是针对故障节点提供保护的更好解决方案。城镇传令者甲骨文由运行可信硬件的节点网络组成，在以太坊的区块链上运行。通过英特尔软件保护扩展(SGX)的可信硬件改进了以前的安全计算方法，因为它的程序执行可以通过密码验证。可信硬件允许软件在被称为飞地的受保护环境中执行。在 enclave 中，任何一方都不能查看或修改数据和代码，包括节点操作者。数据甚至可以由用户名和密码组成，API 密钥可以在查询时提供给节点，即使在受损的机器上也不可能被窃听。

在处理第三方[oracle](https://chain.link/education/blockchain-oracles)时，允许输入和查询保持机密是很困难的，因为为了让查询告诉 oracle 提供商如何以及在哪里获取数据，传统上，该查询需要向 Oracle 披露。那么 oracle 也将能够看到响应，这对于机密性来说是不希望的。

运行 SGX 的可信硬件的优势在于，查询可以交给 oracle，查询可以被解密，其数据可以被检索和处理，并被加密以返回给[智能合同](https://chain.link/education/smart-contracts)，所有这些都在 enclave 内完成。机密数据使用可信硬件的一个例子是如何使用 Town Crier (TC)智能合同传递航班信息。机密的航班信息可以交给运行 SGX 飞地的甲骨文，并返回一个简单的是或否的回答给用户，写在区块链上。另一个例子是在 Steam 上交易游戏。TC 可以允许在查询中给出用户名和密码，验证游戏所有权，并在智能合约中转移所有权。

SGX 的简化抽象如下:

```
Assume: The program operating within the enclave has methods Initialize and Resume

Initialize:
 - Untrusted code Initializes the enclave

 - The attestation of the code within the enclave and its output is generated

 - The attestation is signed to verify that the code was running with the output produced within the enclave

 - The result along with the signed attestation is returned

Resume:
 - Untrusted code calls the Resume method with a session identifier and input parameters

 - An output is produced from the code within the enclave (called with the Resume method)

 - The output is returned
```

运行 SGX 的 oracle 的真实性由其签名来定义。作为查询的一部分给出的输入参数与证明以及执行时间相结合，并用 oracle 的私钥进行签名。这些参数不能以允许系统内接受修改数据的返回的方式再现。

需要实施大规模的基础设施改变，以便在没有可信硬件的情况下以可验证的方式将数据安全地返回到节点，但是也可以用于进一步增强由可信硬件提供的安全性和保密性。例如，HTTPS 不允许对数据进行数字签名，但是 TLS 的扩展 TLS-N 可以通过允许服务器对与客户端的会话进行签名来提高 oracle 的安全性。TLS-N 看起来很有前途，但它确实有一些局限性。数据源需要单独启用扩展，以便 oracles 能够利用它。它不提供聚合离线数据的功能。这将增加智能合约的交易成本。提供凭据将是一次性使用，而不是在智能合约中继续使用。

本节还提出了对离线计算的进一步更改。Oracles 可能需要使用提供的凭据多次连接到 API 端点。为此，需要开发在 enclave 中安全管理这些凭证的能力。目前，离线数据处理仅限于基于正则表达式的语言。未来的目标是让大多数(如果不是全部的话)链外计算在[神谕](https://blog.chain.link/what-is-the-blockchain-oracle-problem/)内完成。然后，这些先知会将计算结果反馈给智能契约。这将降低智能合同的成本，并通过使用可信的硬件来提高保密性。

本节的主要内容应该是了解 SGX 如何提高 oracle 在 Chainlink 网络中的安全性。我试图去掉与图 5 相关的数学，以便任何人阅读它都有意义。然而，在飞地中运行程序的概念仍然很难理解。