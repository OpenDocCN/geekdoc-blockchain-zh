© 作者，独家授权给 APress Media, LLC，隶属于 Springer Nature 2022D. P. Bauer 使用 Ethereum 入门[`doi.org/10.1007/978-1-4842-8045-4_8`](https://doi.org/10.1007/978-1-4842-8045-4_8)

# 8. Filecoin

戴维·佩德罗·鲍尔^(1  )(1)巴西南部格兰德杜苏尔州坎普鲍姆

Protocol Labs，同一家发明并维护 IPFS 的公司，创建了 Filecoin。它通过建立一个开源的去中心化存储网络并激励用户将数据固定到 IPFS 来扩展了 IPFS 的概念。

Filecoin 很棒，因为它提供了一种不需要依赖更大型的中心化存储解决方案的去中心化存储解决方案。与纯 IPFS 解决方案不同，Filecoin 节点有财务激励来保持活动状态。

在此示例中，我们将使用一个名为 Lotus 的 Filecoin 实现。它验证网络交易，管理一个 FIL 钱包，并可以执行存储和检索交易。

在本章结束时，您将能够执行以下操作：

+   创建一个 Filecoin 项目

+   配置 Truffle 以使用 Filecoin 端点

+   启动本地 Filecoin 服务器

+   添加要保存在 Filecoin 上的图像

## 如何在 Filecoin 本地节点上保存文件

要在 Filecoin 中保存文件，您将学习如何从头开始创建项目，并配置 Truffle，使其指向正确的地址。您将启动本地端点，最后使用命令行将图像添加到 Filecoin。

### 创建项目

转到终端，然后单击“新终端”。现在，创建一个新文件夹来启动您的项目。$ mkdir create filecoin

### 配置 Truffle

创建 truffle-config.js 文件。$ touch truffle-config.js 在此文件中，配置 IPFS 和 Filecoin lotus 服务器的文件设置。设置以下值：

+   将 IPFS 地址设置为 http://127.0.0.1:5001。

+   将 Filecoin 地址设置为 http://localhost:7777/rpc/v0。

以后你将使用 Ganache Filecoin 启动这些端点。module.exports = {  environments: {    development: {      ipfs: {        address: "http://127.0.0.1:5001",      },      filecoin: {        address: "http://localhost:7777/rpc/v0",        storageDealOptions: {          epochPrice: "2500",          duration: 518400,        }      },    }  }};

### 添加要保留的图像

创建徽章文件夹。$ mkdir badge 前往徽章根目录。$ cd badge 下载你要在 Filecoin 上保存的图像。你也可以复制并粘贴现有图像到此文件夹中。使用 curl 命令传输带有 URL 语法的数据。$ curl https://planouhost.z15.web.core.windows.net/badge.png > badge-image.png

### 安装依赖项

使用带有 Filecoin 标签的基本 Ganache 包进行安装。$ npm install ganache@filecoin 安装 Filecoin 对等依赖包。$ npm install @ganache/filecoin

使用 Ganache 启动 Lotus 和 IPFS 本地服务器。它还创建了 10 个开发帐户，每个帐户都有 100 个 Filecoin（FIL）。

### 启动本地端点

在本地启动 Ganache Filecoin。$ npx ganache filecoin

### 将文件保留到 Filecoin

打开一个新的终端，并保存文件夹 badge。$ truffle preserve ./badge/ --filecoin 如果一切顺利，输出将如下所示：保存目标：./badge/===========================警告：发现多个输出标签为“ipfs-cid”的插件。  ✓ 加载目标...    ✓ 读取目录 ./badge/...      ✓ 打开 ./badge\badge-image.png...  ✓ 保存至 IPFS...    ✓ 连接到 IPFS 节点，位于 http://127.0.0.1:5001    ✓ 上传中...      根 CID：QmNjGGACAMpm718WjeM7oN3WJ5ntXKgwurH4mMivU6JXoS        ./badge-image.png: QmemrBxhPpg8Hw9sPpAUTWRq3kNAFhCPKUDhMnc5U9KptS  ✓ 保存至 Filecoin...    ✓ 连接到 Filecoin 节点，位于 http://localhost:7777/rpc/v0    ✓ 检索矿工...    ✓ 提议存储交易...      交易 CID：bafyreidrt2pvuh44umo7vzebnxnw46qzntneyojah6oym4ximokyzvwxgq    ✓ 等待交易完成...      交易状态：StorageDealActive

现在你已经在本地的 Filecoin 节点中保存了图片！

## 摘要

在这一章中，你学习了如何使用 Filecoin 保存文件。

在下一章中，你将学习 ENS 是什么，以及如何使用它。
