© 作者，独家许可给 APress Media, LLC，Springer Nature 的一部分 2022 D. P. Bauer 通过[`doi.org/10.1007/978-1-4842-8045-4_7`](https://doi.org/10.1007/978-1-4842-8045-4_7)开始学习以太坊

# 7. 星际文件系统

Davi Pedro Bauer（1）巴西南里奥格兰德州坎普翁邦

[星际文件系统](https://zh.wikipedia.org/wiki/%E6%98%9F%E7%90%83%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F)（IPFS）是一种协议和点对点网络，允许数据在分布式文件系统中存储和共享。IPFS 使用内容寻址来区分全球命名空间中的每个文件，连接所有计算设备。

在本章结束时，您将能够执行以下操作：

+   安装 IPFS 节点包并初始化一个节点

+   查看 IPFS 节点的对等节点

+   测试和探索 IPFS 节点

+   将文件添加到 IPFS

+   在控制台上查看文件内容并在 web UI 中检查文件

+   直接在浏览器中查看文件内容

+   安装 IPFS 浏览器扩展

+   配置 IPFS 节点类型并启动节点

+   将文件导入 IPFS 节点

+   启动本地 IPFS 节点并向其中添加文件

+   检查添加的文件并验证是否已固定文件

+   手动固定文件

+   在 Pinata 上设置 API 密钥

+   将 Pinata 设置为远程服务

+   将文件固定到远程 IPFS 节点，并取消固定

+   登录 Fleek

+   克隆现有存储库

+   安装和初始化 Fleek 包

+   将网站部署到 Fleek

## 创建您的 IPFS 节点

现在，让我们使用命令行创建一个 IPFS 节点并上传你的第一个文件。

### 安装节点

使用 Choco 软件包管理器安装 IPFS。go-ipfs 包是 Go 中的一个 IPFS 实现。$ choco install go-ipfs

### 配置节点

初始化 IPFS 本地存储库。$ ipfs init 启动 IPFS 本地服务器。daemon 命令在 127.0.0.1:5001 上启动 IPFS 本地服务器。$ ipfs daemon

### 测试节点

您可以测试显示直接连接到您节点的节点的 IPFS 节点。$ ipfs swarm peers 您还可以使用 cat 命令并将哈希作为参数传递来查看一些 IPFS 文件内容（见图 7-1）。$ ipfs cat <hash>![](img/521550_1_En_7_Fig1_HTML.jpg)

I P F S 命令输出的屏幕截图显示终端选项卡打开，并提供了链接。下面的文本显示“Hello and Welcome to I P F S”，其中 I P F S 是大写并且具有特殊样式。底部的文本显示：“如果您看到此消息，则已成功安装 I P F S 并现在正在与 I P F S merkledag 进行交互。”

图 7-1

IPFS cat 命令输出

### 探索您的 IPFS 节点

在浏览器中输入 http://127.0.0.1:5002/ 访问 web UI。您的节点现已连接到 I P F S！现在，点击“文件”，注意这里还没有文件（见图 7-2）。

点击“探索”，然后点击“节点”。这些是您连接到的节点。最后，点击“设置”。这是您可以查看节点设置的地方！[](../images/521550_1_En_7_Chapter/521550_1_En_7_Fig2_HTML.png)

I P F S Web U I 的屏幕截图具有以下图标：状态、文件，光标所在位置、探索、节点和设置。在文件窗口中，有一条提示信息，显示：还没有文件！通过点击上面的导入按钮，将文件添加到本地 I P F S 节点。包含导入按钮及其他细节的部分位于右上角。

图 7-2

IPFS Web UI

## 将文件添加到 IPFS

运行 IPFS 的计算机可以询问所有连接的节点是否有具有特定哈希的文件，如果其中一个有，则该节点会将整个文件发送回来。没有像加密哈希这样的短、唯一标识符，这是不可能的。

### 添加文件

启动 IPFS 本地服务器。daemon 命令在 127.0.0.1:5001 上启动一个 IPFS 本地服务器。$ ipfs daemon 现在，使用 echo 命令创建一个名为 hello.txt 的新文件。此命令将给定文本输出到一个新文件。$ echo "test" hello.txt 使用 ipfs add 命令将新创建的文件添加到您的本地 IPFS 节点。$ ipfs add hello.txt

文件被添加到了 IPFS，导致了一个哈希标识符的产生。

### 在控制台上查看文件内容

您可以简单地使用 ipfs cat 命令后跟哈希来查看此新添加文件的文件内容。为此，请用“ipfs add hello.txt”命令在上一步中生成的结果哈希标识符替换<*your_hash*>代码片段。$ ipfs cat <your_hash>

运行此命令后，文件内容将显示在终端上。

### 在 Web UI 中检查文件

转到[`127.0.0.1:5001/webui`](http://127.0.0.1:5001/webui)并单击“文件”。现在，单击“Pins”并复制哈希。通过使用此哈希进行搜索，您将看到此哈希存在。

### 在浏览器中查看文件内容

打开一个新标签，转到 ipfs://<*your_hash*>。现在你可以在浏览器中看到你的文件内容。同样，在这里，用命令“ipfs cat <your_hash>”将<*your_hash*>代码片段替换为为你的文件生成的结果哈希标识符。

## 设置 IPFS 浏览器扩展

IPFS Companion Extension^(3)允许您在您喜欢的浏览器内部本地运行一个 IPFS 节点，提供对 ipfs://地址的支持，网站和文件路径的自动 IPFS 网关加载，简单的 IPFS 文件导入和共享，以及更多功能。

### 安装浏览器扩展

转到 IPFS Companion Extension^(4)并单击“添加到 Brave”或您的浏览器的名称。单击“添加扩展”，然后单击“扩展”图标。最后，将 IPFS Companion Extension 固定到扩展栏。

### 配置节点类型

单击 IPFS Companion 图标，然后单击齿轮图标。对于 IPFS 节点类型，请选择 External。

### 启动外部节点

前往 Visual Studio Code 并打开一个新终端。启动一个新的 IPFS 本地服务器。$ ipfs daemon

### 导入文件

点击 IPFS Companion 图标，然后点击“导入”。点击“选择文件”并选择本地磁盘上的文件。文件将存储在你的 IPFS 节点中。

## 在本地节点上固定和取消固定 IPFS 文件

数据可以固定到一个或多个 IPFS 节点，以确保它在 IPFS 上保留，并且不会在垃圾收集期间被删除。固定允许你管理存储空间和数据保留。因此，你应该继续固定任何你希望永久保留在 IPFS 上的内容。IPFS 的默认行为是将文件固定到你的本地 IPFS 节点。

### 启动你的本地节点

启动 IPFS 本地服务器。daemon 命令在 127.0.0.1:5001 上启动了一个 IPFS 本地服务器。$ ipfs daemon

### 向你的节点添加文件

现在，使用 echo 命令创建一个名为 hello.txt 的新文件。该命令将给定的文本输出到一个新文件中。$ echo "world" hello.txt 使用 ipfs add 命令将新创建的文件添加到你的本地 IPFS 节点中。$ ipfs add hello.txt

文件已添加到 IPFS，生成了一个哈希标识符。当你添加一个文件时，它会自动固定到你的本地节点。

### 检查文件是否已添加

要检查你的文件是否已添加，你可以使用 ipfs cat 命令将文件内容输出到终端。$ ipfs cat your_file_hash

### 验证你的文件是否已被固定

前往 http://127.0.0.1:5001/webui，点击文件，然后点击固定。你的文件就在那里！

### 取消固定你的文件

你可以简单地使用以下命令从你的本地 IPFS 节点中取消固定文件。$ ipfs pin rm <your_file_hash>

### 手动固定你的文件

你可以使用以下命令手动固定文件。请记住，你需要复制你的文件哈希来固定或取消固定它。$ ipfs pin add <your_file_hash>

完成了；你的文件再次被固定了！

## 使用 Pinata 在远程节点上固定和取消固定文件

您还可以将文件固定到远程固定服务。这些第三方服务允许您将文件固定到它们运行的节点，而不是您自己的本地节点。您不必担心自己节点的磁盘空间或正常运行时间。

虽然您可以使用其自己的 GUI、CLI 或其他开发工具管理固定到远程固定服务的 IPFS 文件，但您也可以直接使用本地 IPFS 安装与固定服务一起工作，从而无需学习固定服务的独特 API 或其他工具。

### 在 Pinata 上设置 API 密钥

登录到您的 Pinata 帐户并转到 API 密钥。单击 New Key，然后选中 Admin 复选框。将**admin-cli**输入为您的密钥名称，最后单击创建密钥。将为您生成一个新密钥。从此窗口复制 JWT 值。

### 在终端上设置 Pinata 作为远程服务

将 Pinata 添加为固定远程服务。将您的 JWT 粘贴到<*your_jwt_key*>块中。$ ipfs pin remote service add pinata https://api.pinata.cloud/psa <your_jwt_key>列出所有现有的远程服务，并检查 Pinata 是否存在。$ ipfs pin remote service ls

### 向您的本地 IPFS 节点添加新文件

向您的 IPFS 本地节点添加新文件。$ echo "world" > hello.txt$ ipfs add hello.txt

复制在将文件添加到本地节点后生成的哈希标识符。

### 将您的文件固定到远程 IPFS 节点

使用以下命令固定您的文件。将文件哈希粘贴到<*your_file_hash*>块中。$ ipfs pin remote add --service=pinata -name=hello.txt <your_file_hash>

返回到 Pinata 网站，单击 Pin Manager。您的文件将显示在此页面上！

### 从远程 IPFS 节点取消固定您的文件

使用以下命令取消固定您的文件。将文件哈希粘贴到<*your_file_hash*>块中。$ ipfs pin remote rm --service=pinata -name=hello.txt <your_file_hash>

返回到 Pinata 网站，单击 Pin Manager。您的文件将不再显示在此页面上；这意味着您的文件已取消固定。

## 使用 Fleek 在 IPFS 上托管您的网站

Fleek 使您能够基于开放网络协议创建基础层架构。在不信任、无权限且开放的技术上创建和托管您的站点、应用程序、DApps 和其他服务，旨在实现用户控制的、加密的、私密的、点对点的体验。

### 在 Fleek 上登录

转到 [`fleek.co`](https://fleek.co) 并使用您的帐户登录；然后转到您的 VS Code 编辑器。

### 克隆您现有的仓库

使用一些示例代码克隆现有的仓库。$ git clone https://github.com/johnnymatthews/random-planet-facts

### 安装 Fleek

安装 Fleek 命令行。$ npm install -g @fleekhq/fleek-cli 登录到您的 Fleek 帐户（系统将提示您在浏览器中完成此流程）。$ fleek login

### 初始化 Fleek

在当前目录初始化 Fleek 站点。$ fleek site:init

系统将要求您选择要使用的团队（使用箭头键进行选择）。还要选择要使用的站点。最后，选择要部署的公共目录。

### 部署您的站点

部署您的发布目录中的更改。$ fleek site:deploy

返回到 Fleek 站点并点击托管，然后点击 IPFS 上的验证。这是您托管在 IPFS 上的站点。您现在可以在线查看您部署的站点。

返回到托管并点击 your-site.on.fleek.co。这是您站点托管的友好地址（图 7-3）。![](img/521550_1_En_7_Fig3_HTML.jpg)

屏幕截图显示 Hosting 节点下的霜状连字蛙连字 8 1 5 8 文件夹已打开。下面有 2 点，分别是本地部署和在 IPFS 上验证。接下来的部分是概述标签页已打开，其中提供了 2 点。1. 站点已部署。2. 使用 S S L 设置自定义域名。

图 7-3

Fleek 托管概述

## 摘要

在本章中，您学会了如何安装和创建 IPFS 节点，以及如何使用此协议管理文件。

在下一章中，您将学习如何创建一个 Filecoin 项目。
