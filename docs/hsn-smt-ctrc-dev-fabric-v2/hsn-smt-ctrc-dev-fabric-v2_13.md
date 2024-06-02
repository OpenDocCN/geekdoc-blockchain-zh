# 第八章。在云上部署 Hyperledger Fabric

在第七章中，您通过应用第 III 部分中的所有概念来构建了一个端到端的 Hyperledger Fabric 区块链供应链，您学会了如何构建、部署、测试、调用和维护 Fabric 智能合约。本章建立在您在第 III 部分和第 IV 部分学到的基础上；您将把所有的 Fabric 技能付诸实践，通过在 Amazon、IBM 和 Oracle 云平台上创建和部署 Fabric 应用程序来实现这一目标。因此，本章涵盖了对于那些希望将其 Fabric 应用程序从试点阶段转移到生产阶段的人来说非常实用的步骤。

本章将帮助您实现以下实际目标：

+   设置 Amazon 托管的 Fabric 应用程序的区块链

+   在 AWS 上创建和部署 Fabric 应用程序

+   回顾用于构建区块链应用程序的 IBM 云平台

+   在 IBM 云平台上创建和加入 Fabric 网络

+   回顾 Oracle 区块链平台及其提供的服务

+   在 Oracle 区块链平台上构建和运行 Fabric 应用程序

我们首先回顾了 AWS 的特性，然后是 IBM 和 Oracle 云平台，这对于构建和部署 Hyperledger Fabric 是必不可少的。每个平台都有自己的要求、考虑因素和必要特性，以成功部署和管理 Fabric 应用程序。我们采用了简洁而全面的方法，从零开始覆盖了实践步骤——从建立网络到安装和实例化链代码。

# 在 Amazon 区块链服务上部署 Hyperledger Fabric

亚马逊提供了各种云服务，用于部署和管理集中式和分布式应用程序。为了简洁起见，本节仅关注亚马逊托管区块链服务及其上如何部署和管理 Hyperledger Fabric。亚马逊网络服务（AWS）拥有一支积极的社区，从系统架构师到开发人员和工程师都有。

AWS 提供以下三种方式创建区块链服务：

亚马逊量子分类账数据库（QLDB）

这个完全托管的半 SQL 和半 NoSQL 不可变和透明的分类账数据库由区块链驱动。追加模式的分类账数据提供了一个由中央可信任机构拥有的具有密码学验证的交易历史和审计日志。AWS QLDB 在应用程序需要更多读写限制容量时会自动扩展。

AWS 区块链模板

这些模板为您提供了在网络上快速、简单创建和部署区块链项目，并在 AWS 平台上测试应用程序的方式。通过 AWS CloudFormation 栈构建用户预设的区块链框架，帮助开发人员专注于构建区块链应用程序，减少设置区块链网络的时间。AWS 目前提供两种类型的区块链模板：以太坊和 Hyperledger Fabric。

AWS CloudFormation 加载 AWS 区块链模板，并将区块链框架部署为 Amazon 弹性容器服务（ECS）集群上的容器或直接部署在运行 Docker 的 Amazon 弹性计算云（EC2）实例上。该网络运行在您自己的 Amazon 虚拟专用云（VPC）内。VPC 是云中的虚拟数据中心，提供完全隔离的环境，以自定义方式托管您的机器。子网是 IP 网络的逻辑子分区；VPC 子网使网络更加高效。通过 Amazon 的 VPC 子网和网络 ACL，您可以控制客户端如何访问 AWS 区块链网络。您可以使用 AWS 身份和访问管理（IAM）定义权限策略，限制 Amazon ECS 集群或 Amazon EC2 实例可以访问的资源。

Amazon 托管区块链

这项完全托管的服务提供了生产级别的区块链网络。它可以轻松扩展，支持运行数千个应用程序并处理数百万笔交易。您可以使用 AWS 管理控制台、AWS 命令行界面（CLI）或托管区块链软件开发工具包（SDK）快速设置托管区块链应用。

托管区块链管理您的证书；参与者可以与对等节点交易，而无需了解或信任彼此。

Amazon 托管区块链服务用于创建和操作超级账本（Hyperledger Fabric）区块链网络。

## 准备工作：设置 Amazon 托管区块链

我们可以以多种方式设置 Amazon 托管的区块链，如前面讨论的那样。在设置托管的区块链应用程序时，我们将使用 AWS 管理控制台创建区块链网络和成员。然后，我们将创建一个 VPC 和安全策略，并将策略分配给 IAM 角色。我们还将创建和配置一个 EC2 实例来运行 AWS CLI 以与 Amazon 托管的区块链进行交互。EC2 实例将是运行区块链网络的主节点。通过 AWS 管理控制台，我们将创建一个对等节点以加入网络。最后，我们将在网络中创建一个通道，然后安装和运行链代码。

要在 AWS 托管的区块链上部署 Fabric，您需要已经创建了以下内容：

+   一个 AWS 账户。

+   VPC 和子网-将其命名为`**HF-VPC**`。

+   AWS EC2 安全组-将其命名为`**HF-SG**`。Hyperledger Fabric 客户端 Amazon EC2 实例必须具有允许来自受信任 SSH 客户端的 SSH 流量（端口 22）的入站规则。

+   作为堡垒主机的 EC2 实例；我们使用 Amazon Linux 2 AMI（HVM）作为 Amazon Machine Image（AMI），使用`t2.micro` AWS 免费使用的实例类型进行此设置。通过输入标记，将 EC2 实例命名为`**HF-Node**`。将`HF-SG`与`HF-Node` EC2 实例关联。

+   分配给`HF-Node` EC2 实例的弹性 IP 地址。

+   具有以下策略语句的 AWS IAM 策略-将其命名为`**HyperledgerFabricClientAccess**`，将`*youraccountId*`替换为您的实际 AWS 账户 ID，并将`*us-east-1*`替换为适当的区域。然后附加到`HF-Node` EC2 实例的 IAM 角色：

    ```
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "ListNetworkMembers",
          "Effect": "Allow",
          "Action": [
              "managedblockchain:GetNetwork",
              "managedblockchain:ListMembers"
          ],
          "Resource": [
              "arn:aws:managedblockchain:*:youraccountId:networks/*"
          ]
        },
        {
          "Sid": "AccessManagedBlockchainBucket",
          "Effect": "Allow",
          "Action": [
            "s3:GetObject"
          ],
          "Resource": "arn:aws:s3:::us-east-1.managedblockchain/*"
        },
        {
          "Sid": "ManageNetworkResources",
          "Effect": "Allow",
          "Action": [
            "managedblockchain:CreateProposal",
            "managedblockchain:GetProposal",
            "managedblockchain:DeleteMember",
            "managedblockchain:VoteOnProposal",
            "managedblockchain:ListProposals",
            "managedblockchain:GetNetwork",
            "managedblockchain:ListMembers",
            "managedblockchain:ListProposalVotes",
            "managedblockchain:RejectInvitation",
            "managedblockchain:GetNode",
            "managedblockchain:GetMember",
            "managedblockchain:DeleteNode",
            "managedblockchain:CreateNode",
            "managedblockchain:CreateMember",
            "managedblockchain:ListNodes"
          ],
          "Resource": [
            "arn:aws:managedblockchain:*::networks/*",
            "arn:aws:managedblockchain:*::proposals/*",
            "arn:aws:managedblockchain:*:youraccountId:members/*",
            "arn:aws:managedblockchain:*:youraccountId:invitations/*",
            "arn:aws:managedblockchain:*:youraccountId:nodes/*"
          ]
        },
        {
          "Sid": "WorkWithNetworksForAcct",
          "Effect": "Allow",
          "Action": [
            "managedblockchain:ListNetworks",
            "managedblockchain:ListInvitations",
            "managedblockchain:CreateNetwork"
          ],
          "Resource": "*"
        }
      ]
    }
    ```

+   名为`**ServiceRoleForHyperledgerFabricClient**`的 AWS IAM 角色。选择先前创建的策略*ServiceRoleForHyperledgerFabricClient*，并将此角色与`HF-Node` EC2 实例关联。

我们现在已经完成了使用 AWS 托管的区块链控制台设置 Hyperledger Fabric 网络的所有先决条件。我们将在下一节开始设置区块链网络。

## 设置 Hyperledger Fabric 网络

在本节中，我们将开始设置我们的 HF 网络并在其上运行一个 Fabric 应用程序。目前，AWS Managed Blockchain 仅支持 Hyperledger Fabric 的 1.4 版本。请按照以下步骤操作：

1.  打开 Managed Blockchain 控制台，点击“创建网络”，然后输入一个网络名称。你可以保持大部分默认设置。

1.  在创建成员页面上，通过输入 `**member1**` 作为成员名称来创建一个成员。

1.  在 Hyperledger Fabric 证书颁发机构（CA）配置下，指定管理员在 Hyperledger Fabric CA 上使用的管理员用户名和密码。

1.  创建网络和成员。

    创建你的第一个网络需要几分钟的时间。一旦网络创建完成，你将看到它的摘要。AWS Managed Blockchain 创建了一个网络并为我们的 `member1` 分配了一个网络 ID 和一个成员 ID。记下这两个重要的信息，因为我们将在后续的设置步骤中使用它们。

1.  我们需要通过创建一个 VPC 端点将我们之前创建的 `HF-VPC` 关联到第一个网络上。在第一个网络摘要屏幕上，点击“创建 VPC 端点”，然后选择 `HF-VPC` 作为 VPC。选择 `HF-SG EC2` 安全组来创建 VPC 端点。

## 设置 Hyperledger Fabric 客户端

现在我们将安装我们的 Fabric 客户端并加入一个对等节点。但首先，我们需要在 `HF-Node` EC2 客户端节点上设置所有必要的包和示例，这样你就可以运行 Managed Blockchain 命令来构建我们的 Fabric 网络和链码。

你将首先使用 `ssh` 访问 `HF-Node` EC2 实例。你可以使用此命令连接到你的实例，或者你可以使用另一个 SSH 客户端工具登录：

```
ssh -i /path/…/your-aws-private-ket.pem ec2-user@your-ec2-public-ip
```

一旦你访问到你的 EC2 实例，通过输入 `**AWS –version**` 来检查 AWS 版本。

此 EC2 实例必须安装了 AWS CLI 的版本为 1.16.149 或更高版本。AWS CLI 的早期版本不包含 Managed Blockchain 命令。我们假设您已安装了用于安装和使用 Hyperledger 工具的先决条件，如 Go、Docker、Docker Compose 和其他实用程序（参见第四章）。

接下来让我们设置 Hyperledger Fabric CA 客户端。在此步骤中，您将通过使用之前配置的 VPC 端点验证您是否可以连接到 Hyperledger Fabric CA。然后，您将安装 Hyperledger Fabric CA 客户端，该客户端向管理员和网络对等方发放证书。

要验证与 Hyperledger Fabric CA 的连接，请获取 `CAEndpoint`。通过传递 `network-id` 和 `member-id` 运行以下 AWS `managedblockchain get-member` 命令。您可以从 AWS 托管的 Blockchain 控制台获取这两个 ID：

```
aws managedblockchain get-member \
--network-id n-UYEFPPMBENFFFEITGTS6IJ6TDY \
--member-id m-G4Q5XLRCCJFBTII7PYINITSZH4
{
    "Member": {
        "NetworkId": "n-UYEFPPMBENFFFEITGTS6IJ6TDY",
        "Status": "AVAILABLE",
        "Name": "member1",
        "FrameworkAttributes": {
            "Fabric": {
                "AdminUsername": "admin",
                "CaEndpoint": "ca.m-g4q5xlrccjfbtii7pyinitszh4.n-
uyefppmbenfffeitgts6ij6tdy.managedblockchain.us-east-1.amazonaws.com:30002"
            }
        },
..
        "Id": "m-G4Q5XLRCCJFBTII7PYINITSZH4"
    }
}
```

使用 cURL 或 Telnet 验证 `CAEndpoint` 是否能解析。将 `CAEndpoint` 替换为 `get-member` 命令返回的 `CAEndpoint`：

```
curl https://ca.m-g4q5xlrccjfbtii7pyinitszh4.n-uyefppmbenfffeitgts6ij6tdy.managedblockchain.us-east-
1.amazonaws.com:30002/cainfo -k
```

命令应返回类似以下内容的输出：

```
         {"result":{"CAName":" m-
G4Q5XLRCCJFBTII7PYINITSZH4","CAChain":"LongStringOfCharacters","Version":"1.4.7”,"errors":[],"messages":[],"success"
:true}
```

或者，您可以使用 Telnet 连接到 Fabric CA：

```
telnet CaEndpoint-Without-Port CaPort
```

命令应返回类似以下内容的输出：

```
Trying 10.0.0.24...
Connected to ca.m-g4q5xlrccjfbtii7pyinitszh4.n-uyefppmbenfffeitgts6ij6tdy.managedblockchain.us-east-
1.amazonaws.com.
Escape character is '^]'..
```

现在您已经验证了可以连接到 Hyperledger Fabric CA，运行以下命令配置 CA 客户端：

```
   mkdir -p /home/ec2-user/go/src/github.com/hyperledger/fabric-ca
cd /home/ec2-user/go/src/github.com/hyperledger/fabric-ca
wget https://github.com/hyperledger/fabric-ca/releases/download/v1.4.7/hyperledger-fabric-ca-linux-
amd64-1.4.7.tar.gz
tar -xzf hyperledger-fabric-ca-linux-amd64-1.4.7.tar.gz
```

## 克隆样本库

我们将在 AWS 托管的 Blockchain 中使用 *fabric-samples* 作为 HF 应用的示例。通过在 EC2 实例上运行以下命令来克隆 Git 代码：

```
 cd /home/ec2-user
 git clone --branch v1.4.7 https://github.com/hyperledger/fabric-samples.git
```

### 注册管理员用户

因为只有管理员身份可以在 Fabric 中安装、实例化和查询链码，所以我们需要为管理员用户注册并发放证书文件。我们首先需要通过运行以下命令将 *managedblockchain-tls-chain.pem* 文件复制到 */home/ec2-user* 目录中创建证书文件。将 `*us-east-1*` 替换为您正在使用的 AWS 区域：

```
aws s3 cp s3://us-east-1.managedblockchain/etc/managedblockchain-tls-chain.pem  /home/ec2-
user/managedblockchain-tls-chain.pem
```

运行以下命令来测试您是否已正确将内容复制到文件中：

```
   openssl x509 -noout -text -in /home/ec2-user/managedblockchain-tls-chain.pem
```

该命令应返回证书内容的人类可读格式。一旦证书文件创建完成，我们需要注册成员管理员。通过运行 `fabric-ca-client enroll` 命令来注册成员管理员，需要提供 CA 端点、管理员配置文件和证书文件：

```
[ec2-user@ip-10-0-0-235 ~]$ fabric-ca-client enroll \
 > -u https://admin:Password_1234@ca.m-g4q5xlrccjfbtii7pyinitszh4.n-
uyefppmbenfffeitgts6ij6tdy.managedblockchain.us-east-1.amazonaws.com:30002 \
 > --tls.certfiles /home/ec2-user/managedblockchain-tls-chain.pem -M
```

在 Fabric 中，MSP 标识允许定义信任域成员的根 CA 和中间 CA。在我们的设置中，我们将通过运行此命令为管理员的 MSP 复制证书，存储在 */home/ec2-user/admin-msp*。

```
cp -r /home/ec2-user/admin-msp/signcerts admin-msp/admincerts
```

### 在您的成员身份中创建一个对等节点。

Fabric 对等节点执行账本数据的验证和更新。它们保留共享账本的本地副本。一个典型的 Fabric 网络将在网络中有多个对等节点。在我们的设置中，我们将在 HF 网络中创建一个对等节点。

要使用 AWS 管理控制台创建对等节点，请在 Managed Blockchain 控制台上打开 [*https://console.aws.amazon.com/managedblockchain/*](https://console.aws.amazon.com/managedblockchain/)。

选择 Networks，从列表中选择网络，然后选择查看详细信息。接下来，从列表中选择一个成员，然后点击“创建对等节点”。选择对等节点的配置参数。在这个设置中，我们可以保留所有默认设置。然后选择“创建对等节点”。一旦对等节点创建完成，您可以通过点击对等节点 ID 在成员页面获取所有对等节点信息。我们将在后续设置中使用一个对等节点端点。

## 运行 Hyperledger Fabric 应用程序。

在上一步中启动对等节点后，在本节中我们将最终开始配置和运行 Hyperledger Fabric 应用程序。让我们首先启动 Hyperledger Fabric CLI。

### 配置和运行 Docker Compose 以启动 Hyperledger Fabric CLI。

在 */home/ec2-user* 目录下创建一个名为 *docker-compose-cli.yaml* 的 Docker Compose 配置文件：

```
touch docker-compose-cli.yaml
```

你将配置这个文件以运行 Hyperledger Fabric CLI。让我们打开 *docker-compose-cli.yaml*。将以下内容复制到文件中，并替换 `MyMemberID` 和 `*MyPeerNodeEndpoint*` 的值。你可以从 AWS 托管的区块链控制台的成员页面找到成员 ID 和对等节点 ID：

```
 version: '2'
services:
  cli:
    container_name: cli
    image: hyperledger/fabric-tools:1.4
    tty: true
    environment:
      - GOPATH=/opt/gopath
      - CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
      - FABRIC_LOGGING_SPEC=info # Set logging level to debug for more verbose logging
      - CORE_PEER_ID=cli
      - CORE_CHAINCODE_KEEPALIVE=10
      - CORE_PEER_TLS_ENABLED=true
      - CORE_PEER_TLS_ROOTCERT_FILE=/opt/home/managedblockchain-tls-chain.pem
      - CORE_PEER_LOCALMSPID=m-G4Q5XLRCCJFBTII7PYINITSZH4
      - CORE_PEER_MSPCONFIGPATH=/opt/home/admin-msp
      - CORE_PEER_ADDRESS=nd-fmwonqhh6vgexehznnpv4ydzyq.m-g4q5xlrccjfbtii7pyinitszh4.n-
uyefppmbenfffeitgts6ij6tdy.managedblockchain.us-east-1.amazonaws.com:30003
    working_dir: /opt/gopath/src/github.com/hyperledger/fabric/peer
    command: /bin/bash
    volumes:
        - /var/run/:/host/var/run/
        - /home/ec2-user/fabric-samples/chaincode:/opt/gopath/src/github.com/
        - /home/ec2-user:/opt/home
```

运行 `docker-compose` 启动 Hyperledger Fabric CLI：

```
 docker-compose -f docker-compose-cli.yaml up -d
```

一旦 Hyperledger Fabric CLI Docker Compose 启动，你就可以像往常一样开始创建 Hyperledger Fabric 通道。

### 为 Hyperledger Fabric 通道创建 configtx

*configtx.yaml* 文件包含通道配置的详细信息。更多信息请参阅第四章。

使用 vi 在 */home/ec2-user* 目录下创建一个名为 *configtx.yaml* 的文件。

将 `*MemberID*` 替换为你自己的成员 ID。

`MSPDir` 设置为相同的目录位置 */opt/home/admin-msp*，这个目录是你在 *docker-compose-cli.yaml* 中为 Hyperledger Fabric CLI Docker 容器使用 `CORE_PEER_MSPCONFIGPATH` 环境变量所建立的：

```
Organizations:
   - &Org1
       Name: m-G4Q5XLRCCJFBTII7PYINITSZH4
       ID: m-G4Q5XLRCCJFBTII7PYINITSZH4
       MSPDir: /opt/home/admin-msp
  ..
Profiles:
    OneOrgChannel:
        Consortium: AWSSystemConsortium
        Application:
            <<: *ApplicationDefaults
            Organizations:
                - *Org1
```

配置完成后，运行此 Docker 命令生成通道的 *configtx*：

```
docker exec cli configtxgen -outputCreateChannelTx /opt/home/mychannel.pb \
-profile OneOrgchannel -channelID mychannel \
--configPath /opt/home
```

### 为 orderer 设置环境变量

通过编辑 *.bash_profile* 设置 `$ORDERER` 环境变量以方便使用。将 `ORDERER` 值替换为你自己的排序服务端点。你可以在托管的区块链控制台上找到该端点。

更新 *.bash_profile* 后，通过运行 `source` 命令应用更改：

```
source ~/.bash_profile
```

在下一步中，我们将开始创建通道。运行以下命令从 *channel.tx* 中读取一个创世区块，该区块将创建通道：

```
docker exec cli peer channel create -c mychannel \
-f /opt/home/mychannel.pb -o $ORDERER \
--cafile /opt/home/managedblockchain-tls-chain.pem --tls
```

通道创建完成后，通过运行以下 Docker 命令将对等节点加入通道：

```
docker exec cli peer channel join -b mychannel.block \
-o $ORDERER --cafile /opt/home/managedblockchain-tls-chain.pem –tls
```

成功创建 *mychannel* 后，我们可以在网络中安装示例链码。运行以下命令在对等节点上安装示例链码：

```
docker exec cli peer chaincode install \
-n mycc -v v0 -p github.com/chaincode_example02/go
```

现在我们需要实例化链码：

```
 docker exec cli peer chaincode instantiate \
-o $ORDERER -C mychannel -n mycc -v v0 \
-c '{"Args":["init","a","100","b","200"]}' \
--cafile /opt/home/managedblockchain-tls-chain.pem --tls
```

获取结果可能需要一分钟；您可以使用以下命令验证实例化结果：

```
docker exec cli peer chaincode list --instantiated \
-o $ORDERER -C mychannel \
--cafile /opt/home/managedblockchain-tls-chain.pem --tls
```

在此阶段，我们可以与 HF 网络中的链码进行交互。让我们开始查询链码。运行此命令查询一个值：

```
docker exec cli peer chaincode query -C mychannel \
-n mycc -c '{"Args":["query","a"]}'
```

由于我们初始化了变量 `a` 并将其值设置为 `100`，所以命令应该返回一个值为 `100`。您应该看到类似于以下的结果：

```
> -n mycc -c '{"Args":["query","a"]}'
100
```

在上一个命令中，我们实例化并查询了一个值为 100 的变量 `a`。使用 `invoke` 命令从初始值中减去 10：

```
 docker exec cli peer chaincode invoke -C mychannel \
-n mycc -c  '{"Args":["invoke","a","b","10"]}' \
-o $ORDERER --cafile /opt/home/managedblockchain-tls-chain.pem --tls
```

重新使用以下命令查询：

```
docker exec cli peer chaincode query -C mychannel \
-n mycc -c '{"Args":["query","a"]}'
```

应返回新值 90，如以下输出所示：

```
docker exec cli peer chaincode query -C mychannel \
> -n mycc -c '{"Args":["query","a"]}'
90
```

[此](https://www.youtube.com/watch?v=x-AjS-WuF2Q) [视频](https://www.youtube.com/watch?v=x-AjS-WuF2Q) 由 Carl Youngblood 提供的 “构建区块链溯源应用程序” 演示了如何通过使用区块链服务提供的 AWS 中搭建 Fabric 网络。

# 使用 IBM Cloud 进行区块链应用程序开发

作为 Hyperledger Fabric 项目的主要贡献者之一，IBM 提供了一个完整而直观的平台，IBM Blockchain Platform，用于构建 Fabric 网络和部署 Fabric 应用程序。IBM Cloud 允许用户完全管理其部署、证书和私钥。它提供了一个简化的用户界面，允许开发人员将 Fabric 组件轻松部署到 Kubernetes/Red Hat OpenShift 集群中。

## 了解平台功能

简而言之，IBM Blockchain Platform 的功能可以分为三个领域：开发、运营和可伸缩性。

### 开发

在开发 Fabric 应用程序时，IBM 提供了一套开发工具，简化了开发和部署工作。具体而言，您可以执行以下操作：

+   使用 Ansible Playbooks 或 Red Hat Marketplace 更快地部署网络

+   通过增加 Kubernetes 资源，将概念验证快速转化为生产环境

+   利用 IBM 区块链平台开发人员工具轻松编码

### 操作

在 IBM 云上运行 Fabric 应用时，您可以利用以下优秀功能：

+   能够将对等点部署到多个通道上的多个云，或允许其他成员加入您的联盟。

+   统一的代码库功能允许您在任何由 IBM 云和第三方公共云支持的环境上运行您的组件。

+   动态签名集合功能促进了对通道配置的协作治理。

+   移除了 Docker-in-Docker 对链码的影响，使链码 Pod 更安全地运行，而不需要对等方请求特权访问。

+   能够轻松将运行在较旧 Fabric 版本上的节点升级到最新版本的 Fabric。升级后，您的通道和网络的功能也将相应增加。

+   集成日志记录和监控工具，利用 IBM 云服务如 IBM Log Analysis；IBM Cloud 监控有助于管理区块链网络。

### 可伸缩性

作为一个显著的性能因素，可伸缩性在 Fabric 应用的增长中扮演着重要角色。IBM 云为您提供以下可伸缩性能力：

+   通过设置您希望在 Kubernetes 集群中预配的 CPU、内存和存储的数量，灵活地利用网络中被利用的计算能力

+   通过轻松扩展 Kubernetes 集群中的资源来调整网络中被利用的资源量

+   可以在多个区域或区域之间复制您的 Kubernetes 部署，以确保您的组件具有高可用性以及灾难恢复能力

此外，使用 IBM 区块链平台控制台，您可以轻松创建和管理区块链应用程序。具体而言，一旦在 IBM 云上预配了区块链服务实例，您就可以将其链接到您的 Kubernetes 集群，之后您可以通过控制台创建和管理您的区块链组件，如 CA、对等体和排序服务镜像。但是，在使用控制台之前，您需要知道您将负责以下事项：

+   监控 Kubernetes 集群的健康、安全性和日志记录。

+   管理和保护您的证书和私钥。IBM 不会在 Kubernetes 集群中保存您的证书。

关于使用 IBM 区块链平台的其他注意事项或要求，请参阅[IBM 云](https://cloud.ibm.com/docs/blockchain-multicloud?topic=blockchain-hyperledger-fabric)文档。

## 创建 IBM 云账户

在我们讨论如何在 IBM 云上创建和管理 Fabric 网络之前，您需要创建或拥有一个 IBM 云账户。对于新用户注册，请访问 IBM 云站点并按照说明操作。

一旦您拥有 IBM 云账户，您可以从 IBM 云目录或 Red Hat Marketplace 中添加 IBM 区块链平台。有关更多详细信息，请参阅 IBM 文档。请注意，如果您希望使用硬件安全模块（HSM）为您的对等体和排序者节点生成和保存私钥，您应在部署平台之前配置 HSM。有关 IBM 云上的 HSM 实施和其他注意事项的更多详细信息，请访问 IBM 文档页面。

###### 注意

所有链接服务到 Kubernetes 集群的用户都需要存储管理权限。只需转到仪表板，选择管理 ® 访问（IAM），选择用户，然后单击将连接服务到 Kubernetes 集群的用户。单击经典基础设施选项卡，展开服务部分，然后选择存储管理。单击“应用”以授予用户权限。

## 决定区块链网络的结构

正如你所知，一个企业的各方必须同意成为区块链网络的一部分。区块链网络的参与者类型和交易对其结构的决定起着至关重要的作用。作为第一步，根据业务需求，您需要确定区块链参与者的数量、组织的数量、每个组织中的对等体数量、证书颁发机构等等。一旦确定了区块链网络的组件，您就可以进一步设置网络。

举个例子，假设我们的 Fabric 网络包括以下内容：

+   两个 CAs

+   两个 MSPs

+   一个对等体

+   一个排序方

+   一个通道，包括一个对等方组织和一个排序方组织

这个示例网络结构适用于学习目的，但我们需要添加更多的对等体和组织，使其看起来像一个真正的区块链网络。接下来的章节将逐步向您介绍如何在 IBM Cloud 上创建样本 Fabric 网络，然后您将向其中添加 Fabric 组件，如对等方、排序方和通道。

## 创建并加入 Fabric 网络

在 IBM Cloud 上允许您设置 Fabric 网络的区块链服务称为 IBM 区块链平台，被视为区块链即服务系统。

首先登录 IBM Cloud。这将带您到 IBM Cloud 仪表板，列出了您账户创建的资源（应用程序、存储服务、集群等）（如果有的话）。您可以在“目录”选项卡上找到 IBM Cloud 上所有可用服务的列表。

要创建新的服务实例，请单击“目录”选项卡，然后搜索`**Blockchain**`。然后，单击服务瓷砖 IBM 区块链平台。这将重定向您到区块链服务实例创建。

首先，选择一个位置。位置指定了各种地理区域（如亚太地区、北美、欧洲等）。然后，选择定价计划。接下来，提供一个服务名称。这可以是您选择的任何名称。然后，选择资源组。资源组是组织云账户中资源的一种方式。在您的云账户中，默认将创建一个“默认”资源组。如果您想创建一个新的资源组，请选择“管理”®“账户”®“账户资源”®“资源组”®“创建”。

提供所有必需的值后，点击“创建”以创建区块链服务的实例。此服务实例充当您的 Fabric 网络的占位符；网络尚未创建。服务创建将带您进入欢迎页面，逐步设置您的网络。欢迎页面显示了管理区块链服务所需的步骤。正如您所知，Hyperledger Fabric 使用容器构建网络，因此您可以使用 IBM 云 Kubernetes 集群或 Red Hat OpenShift on IBM 云来部署区块链网络组件。下一步是创建新的集群并将现有集群链接到设置网络。

请注意，如果您的云账户中存在一个集群（即，您已经创建了一个集群），则跳过此步骤。您无需再次创建新的集群。

如果您通过“管理服务”页面在 IBM 云上创建一个新的集群，它会列出集群的要求，因此首先参考这些要求并决定适当的大小（工作节点数量、虚拟 CPU、RAM 大小、单区域或多区域）。

在创建 Kubernetes/Red Hat OpenShift 集群时，将要求您提供集群名称、位置、大小等。每个都有自己的定价计划。创建集群后，设置集群将需要一些时间。等待直到集群完全部署。

接下来是将您的集群与此区块链服务关联起来。单击该选项，它会为您提供帐户中所有可用集群的列表。选择您想要用于区块链网络的集群。它将把集群与您的区块链服务关联起来。现在，您已经准备好启动服务控制台。

您可以通过成功将您的区块链服务与集群关联来启动 IBM 区块链平台控制台。它会带您转到 IBM 区块链平台页面，您将在那里开始创建您的实际网络组件。

## 构建区块链网络

CA、MSP、节点、排序服务、组织、通道等概念已在第三章中有所解释；请参考该章节以获取更多详情。本节重点介绍在 IBM 云上设置 Fabric 网络，使用 IBM 区块链平台。

我们将详细介绍设置示例网络的步骤——一个排序服务、一个单个节点组织和一个单个通道，正如“决定区块链网络的结构”中所解释的那样。

IBM 区块链平台控制台提供了一个界面，用于处理节点（节点、CA、排序服务）、通道、智能合约、钱包、组织和用户。让我们开始吧。

### 添加证书颁发机构

要部署节点，您首先需要创建它们的组织。这需要您的组织的 MSP 定义，而 MSP 定义又需要组织管理员用户身份。 CA 是为所有网络参与者创建身份的实体。因此，在设置区块链网络的第一步中，您需要为组织创建 CA。

从 IBM 区块链平台控制台中，选择节点 ® 添加证书颁发机构。要创建一个新的 CA，请提供以下值：

+   CA 显示名称（例如，`Org1CA`）

+   CA 管理员注册 ID

+   CA 管理员注册密码

+   还提供了高级部署选项，比如创建高可用 CA、多区域 CA 和 HSM。有关更多详细信息，请参考 IBM 文档。

你也可以使用自己的 CA。如果你有自己的 CA，你需要通过使用 JSON 文件导入它。CA 必须满足某些规范，比如发行证书的格式。你可以参考 IBM 文档了解规范。

### 关联管理员身份

部署 CA 后，你需要关联一个管理员身份。这个身份将允许你与 CA 进行交互，并用于创建组织的 MSP、注册用户和将对等节点添加到网络中。

从 IBM 区块链平台控制台中选择节点 ® [CA 节点] ® 关联身份。

提供 CA 管理员注册 ID 和上一步中提供的注册密码。点击“关联身份”后，CA 管理员身份将与 CA 节点关联，并添加到钱包中。你可以通过转到 IBM 区块链平台控制台并选择钱包来查看钱包。这个管理员身份将用于注册新用户和生成证书。

### 注册用户

正如先前所述，每个节点在区块链网络中参与都需要一个证书和一个私钥。因此，使用组织的 CA 管理员身份，你需要注册以下两个身份：

+   一个将作为组织管理员的身份

+   对等节点本身的身份，将用于签署对等节点的操作

请注意，如果一个组织拥有多个对等节点，一个管理员身份就足够了，但你需要为每个对等节点创建一个对等节点身份。

要继续进行身份注册，请转到 IBM 区块链平台控制台，并选择节点 ® [CA 节点] ® 注册用户。如果这是您为组织注册管理员的第一次，使用以下步骤：

###### 注意

除了第一步之外，这些步骤适用于更高级的用户。有关更多详细信息，请参考 IBM 文档。

1.  为组织管理员提供注册 ID 和注册密码，然后选择类型为 Admin。

1.  对于基于角色的访问控制所需的从属关系，请保留默认选择。

1.  对于可选的最大注册字段，请保留默认值，即空白。

1.  如果您希望设置基于属性的访问控制，请创建键值对。

现在管理员用户已注册，我们可以继续注册节点身份。为此，请选择类型为 Peer 而不是 Admin，重复第 1 步。

检查钱包以查看这些身份。您可能会认为这些身份尚未在钱包中可用。这是正确的！

您已注册了身份，但尚未注册。一旦身份注册，其证书将生成，并且可以在钱包中查看身份。在接下来的部分中，您将学习如何注册这些身份。

### 创建节点组织的 MSP 定义

现在我们将创建 MSP，这是节点组织的正式定义。为此，请转到 IBM 区块链平台控制台，然后选择组织 ® 创建 MSP 定义。根据以下列出的要求提供所需的值：

+   MSP 名称（例如，`Org1MSP`）及其 ID

+   根 CA 的详细信息，例如用于为组织创建节点和身份的根 CA

+   管理员证书，如您在上一节中使用管理员身份注册的用户的 ID 和密钥

在此步骤中生成了管理员身份的证书，同时此身份被导出到钱包。同样，您可以通过导出管理员证书并将其保存到您的文件系统来管理证书。

下一步，我们创建一个 MSP 定义，您可以使用它在组织中添加节点。

### 创建节点

节点是托管智能合约并维护账本的节点。要创建一个节点，请转到 IBM 区块链平台控制台，然后选择节点 ® 添加节点。创建节点需要以下详细信息：

+   对等节点的名称（例如，`peer1`）

+   CA 详细信息——使用您用于创建组织 MSP 的 CA

+   用户 ID 和密码，注册为对等节点类型

+   选择组织 MSP

+   关联对等节点管理员身份。这将作为你的对等节点的管理员。你可以将组织管理员设置为对等节点管理员；但是，你可以注册和注册一个不同的身份，使组织 CA 成为你的对等节点的管理员。

有了所有这些信息，你已经创建了对等节点。还有高级部署选项可用——例如，如果你想使用自己的 CA、状态数据库或 HSM，可以参考 IBM 文档了解更多信息。

###### 注意

要向同一组织添加更多对等节点，你需要注册一个新用户，具有对等节点的身份，并重复提到的步骤。

### 创建订购服务

订购服务是一个节点或节点集群。你可以创建一个节点的订购服务（足以用于测试目的）或一个具有多个节点的崩溃容错订购服务。有关更多信息，请参考 IBM 文档。

要创建一个订购服务节点，我们需要按照同等步骤进行操作，就像创建对等节点一样。与之前一样，你必须创建一个 CA，使用该 CA 创建新的身份，并创建一个组织定义；同样地，在创建订购服务之前，你需要执行接下来的相同步骤：

1.  为订购服务组织创建一个 CA（比如，`OrdererCA`）。按照“添加证书颁发机构”中的相同步骤进行操作。

1.  通过按照“关联管理员身份”中的相同步骤来关联 CA 管理员身份。

1.  注册新的身份。你需要注册两个身份，一个管理员身份作为 Admin 类型，另一个节点身份作为 Orderer 类型。重复“注册用户”中给出的相同步骤。

1.  以与“创建对等方组织的 MSP 定义”相同的方式为排序服务组织创建一个 MSP（例如，`OrdererMSP`）。在此步骤中，请确保您适当地使用与排序服务相关的身份。

1.  通过选择节点 ® 添加排序服务，从 IBM 区块链平台控制台创建排序服务节点。

在创建排序服务节点时，您需要输入排序服务名称、排序节点数量以及排序服务 CA 的详细信息，具有排序者身份的用户以及 MSP。最后，关联您钱包中的身份，该身份将充当您的排序服务的管理员。您可以选择 Orderer 服务 MSP 管理员进行此操作，或者创建一个新的身份。

### 将组织添加为联盟成员

现在您已经创建了对等节点、其组织以及排序服务，排序服务在创建区块链网络中的通道之前应该知道这些组织。因此，在创建通道之前，您需要将组织添加为已知于排序服务。这个过程称为*加入联盟*。

从 IBM 区块链平台控制台，在联盟成员部分，选择节点 ® [Ordering Service Node] ® 添加组织。从所有可用的组织中选择组织，然后点击添加组织。为将成为联盟一部分的所有组织重复相同的步骤。

完成此步骤后，组织可以在区块链网络中托管在排序服务上创建或加入通道。

### 创建一个通道

通道充当对等方通过排序服务之间的消息传递介质。在创建通道之前，请确保您已部署了排序服务和对等组织，并且该组织已加入联盟。要创建一个通道，请转到 IBM 区块链平台控制台，然后选择通道 ® 创建通道。然后完成以下步骤：

1.  提供频道名称并选择排序服务。

1.  将组织的 MSP 添加为频道成员，并附带其操作员、读取器或写入器权限。每个频道必须至少有一个具有操作员权限的组织。

1.  频道更新策略指定每当需要时，需要批准频道配置更新的组织数量。如果您的网络中有一个组织，则策略将是“1 个中的 1 个”。

1.  接下来，选择频道创建者组织及其管理员身份。这指定了哪个组织正在创建频道。

创建频道后，下一步是加入频道。

### 加入频道

Peer 加入频道后，示例区块链网络的设置完成。要加入频道，请转到 IBM 区块链平台控制台并选择频道。

在上一步创建的频道中，还没有加入的对等方，并显示状态为“待定 - 添加对等方”。单击此选项将为您提供可用的对等方列表，您可以从中选择对等方。

或者，您可以转到 IBM 区块链平台控制台并选择频道 ® 加入频道。然后，您需要选择与您的频道关联的排序服务并提供频道名称。然后，您将看到可用的对等方列表，您可以从中选择对等方。

在选择对等方后，您将看到使您的对等方成为锚定对等方的选项。有关锚定对等方的更多信息，请参阅第三章。您可以将一个对等方或许多/全部对等方作为锚定对等方。使您的对等方成为锚定对等方并继续加入频道。

现在，您的区块链网络设置已完成，这样，您就拥有了一个完全功能的区块链网络。作为下一步，您可以在频道上开始部署您的智能合约并开始在网络中进行交易。

## 部署智能合约

通过 IBM 区块链平台控制台，您可以管理智能合约的部署，但无法管理其开发。智能合约在安装到 Fabric 网络之前应打包为 *.cds*（对于较旧的 Fabric 版本）或 *.tgz* 或 *.tar.gz*。

对于较旧版本的 Fabric（< 2.*x*），请转到 IBM 区块链平台控制台，然后选择 Smart Contracts ® Install Smart Contract。

提供已打包的（*.cds*）智能合约，它将被安装在所有对等节点上。一旦安装完成，您可以选择实例化智能合约。在此过程中，您需要设置认可策略、函数名称及其初始化合约所需的参数。成功实例化后，合约可在已实例化的智能合约下查看。

对于当前的 Fabric 版本（> 2.*x*），智能合约的管理方式有所不同。您需要执行以下三个步骤：

1.  提出智能合约。

    从 IBM 区块链平台控制台中选择 Channels ® [*Your channel node*] ® Propose smart contract definition。然后提供对等节点管理员身份、智能合约名称及其版本以及认可策略。然后单击提议。这将在所选对等节点上安装已打包的智能合约，并将智能合约提议给通道。将智能合约提议给通道意味着它将通知通道成员以获取他们的批准。

1.  为智能合约指定成员。

    通道成员可以在控制台的 Channels 下查看此提议的智能合约。选择您的组织和关联的对等节点管理员身份以进行您的批准/拒绝操作。

1.  将智能合约提交到通道。

    一旦所有必需的批准都已到位，您就可以提交智能合约。此过程与智能合约实例化类似。任何通道成员都可以在通道上提交智能合约。选择您的组织，提供对等节点管理员身份，并提交智能合约。

一旦智能合约被实例化，或者提交到通道，你的网络就准备好接受交易了。

## 创建应用程序

一旦成功创建了区块链网络，并且智能合约已经在你的网络的某个通道中提交，你就可以开始编写客户端应用程序来在网络中进行交易。应用程序可以使用 Fabric SDK 与 Fabric 网络进行交互。Fabric 为各种编程语言提供了几种 SDK。SDK 使用连接配置文件连接到你的网络。连接配置文件包含对等体、CA 和组织 MSP 的端点信息。

要下载连接配置文件，请转到 IBM 区块链平台控制台，选择 Organizations ® [*Organization Name*] ® Create connection profile。然后选择对等体并下载连接配置文件。

下一步是使用 SDK 和连接配置文件从你的应用程序连接到你的区块链网络，然后执行交易以创建、更新或转移你的网络中的资产。

# Oracle 区块链平台概述

在本节中，我们深入探讨了 Oracle 区块链平台及其提供的内容。接下来将全面介绍设计并部署在 Oracle 上的区块链使用案例。

*Oracle 区块链平台* (*OBP*) 是一个预装平台，提供了构建和运行链代码以及维护不可变分布式账本的便利性。在我们深入了解 OBP 之前，重要的是要了解，区块链平台使用 Oracle 云基础设施（OCI）虚拟机来部署和运行区块链网络以及其他支持服务，包括对象存储（产品和相关二进制文件和日志）、身份服务（用户、角色、认证、安全性）和负载均衡器。

OBP 上的典型区块链网络将包括验证交易并通过执行链码来响应查询的节点。外部应用程序可以使用 SDK 或 REST API 在区块链网络上调用交易。一个或多个背书对等体对链码执行结果进行数字签名（背书），然后由排序服务进一步验证。达成共识后，交易将被排序、分组，并发送到对等节点进行验证，然后追加到分类帐中。

控制台允许管理员配置区块链网络并监视其操作，检查日志等。在配置区块链网络时，您需要完成一些简单的实例创建步骤，然后 Oracle 负责服务管理、打补丁、备份和恢复以及其他服务生命周期任务。您首先要创建一个区块链实例，其中包含构建、部署、运行和监视由 Fabric 提供支持的生产级权限区块链分类帐所需的一切。

在这一部分中，您将使用 Oracle 区块链平台云服务构建一个演示 OBP 的示例用例。Oracle 提供以下区块链产品：

Oracle 区块链平台云服务

这个云服务包括一个基于模板的预装平台即服务（PaaS）。它利用了 OCI，处理依赖项如容器、虚拟机、身份管理以及块和对象存储。

Oracle 区块链平台企业版

这是为需要更高数据隐私或更喜欢在本地管理其数据的客户而设计的。这个版本提供了一个预装的、本地部署的区块链，可以部署在您的数据中心上。它具有与基于云的 Oracle 区块链平台相同的功能对等性，并提供相同的 API 和应用程序的可移植性。

预构建解决方案

这个预构建选项提供了预集成的、快速部署的区块链解决方案。这些解决方案可以与供应链管理等 SaaS 应用无缝连接。例如，Intelligent Track and Trace 是一个预集成的区块链解决方案，用于实现端到端的供应链可见性。

Oracle 数据库中的防篡改区块链表

这个解决方案设计用于企业需要不可变存储的用例，比如防篡改的交易日志、审计跟踪、合规数据、财务分类账或法律保留数据。这是 Oracle 数据库中的一个防篡改选项，只允许插入操作。每一行包含上一行的哈希值，从而将这些行链接在一起。不可否认性是有保障的，因为用户用基于 PKI 的签名对行的内容进行签名。

图 8-1 展示了 OBP 的高层架构。这个许可的区块链提供了一个封闭的生态系统，在这个生态系统中，创始组织邀请其他参与组织。它遵循一个三步共识流程：认可、排序和验证。该平台本身是一个托管服务，具有零停机的托管补丁、升级和账本及配置的备份。

![Oracle 区块链平台架构](img/HLF_0801.png)

###### 图 8-1\. Oracle 区块链平台架构

基于 OCI 基础架构租户模型，这个架构有助于隔离组织的数据，并提供了增强的安全性和在传输和静态数据加密方面的保护。它提供了 Web 应用程序防火墙 (WAF) 来防御攻击。身份管理云服务提供了用户和角色管理。它还提供了一个简化的生态系统，用于组建联盟、简化参与者加入区块链网络以及对 CA、REST 代理和平台控制台进行身份验证。

每个组织的实例使用每个节点的托管 VM 和容器。为了避免中断，*排序者*、*控制台*、REST 代理和 *fabric-ca* 节点进行了复制。为链代码执行容器预配了单独的 VM。为了抵御数据中心中断，对象存储自动在 OCI 可用性域（AD）之间进行了复制。

现在我们已经涵盖了各种服务和 OBP 架构，让我们专注于 Oracle 区块链平台，从一个示例用例开始。

# Oracle 区块链平台用例

在本节中，我们通过四个步骤顺序设置和部署 Fabric 应用于 OBP：探索、参与、实验和体验。具体来说，我们通过定义用例开始“探索”步骤。然后我们按照“参与”步骤来审查交易、通道、数字资产和其他与我们用例相关的工件。在“实验”步骤中，我们在 OBP 上配置 Fabric 网络和交易基础设施。最后，在“体验”步骤中，我们通过部署和实例化我们的链代码为我们的 Fabric 网络添加“智能”。

## 探索用例

在我们开始任何工作之前，我们需要评估用例，确定是否适合基于区块链的解决方案，并确定可以帮助建立业务案例的网络类型。

本节简要描述了我们的用例。在本示例中，一所大学使用 Fabric 管理其学生凭证的真实性。在此过程中，您将学习如何使用 Fabric 解决业务问题以及如何在 OBP 上部署解决方案。

与其他行业一样，大学和其他高等教育机构正在投资并采用数字解决方案，以提高学生的效率和体验。高等教育机构正在为未来的劳动力做准备，而这一劳动力已经精通技术。他们需要一个蓬勃发展的生态系统，高效的随时随地学习能力，以及防篡改的证书存储，以向未来雇主展示他们的技能。总的来说，教育行业在构建这一生态系统方面面临着关键挑战，如传统技术、数据孤岛、与同行大学的低合作、证书验证、纸质学位和证书、IP 的跟踪和保护，以及对有才能和有需要的人公平分配资助等。

我们的用例针对证书验证。很多人都会同意，证书验证是缓慢的，主要是手工操作。假证书和学位可以在很多方面损害大学并伤害雇主。

这个用例涉及由 CA 发放证书，并允许证书所有者（学生/学习者）、雇主和其他机构验证证书所有者的防篡改证书。这个示例包括以下利益相关者：

证书查看器/验证器（CVs）

学生、雇主、其他大学

Oracle 商学院（OBS）

证书创建者（学习院）

Oracle 全球大学（OGU）

证书审核者和发放者（大学）

## 参与解决方案

要开始，我们需要定义解决方案的整体设计，如图 8-2 所示，以确保流程、用例和技术之间的同步性。这个阶段侧重于定义基于区块链的业务网络及其组件，如业务拓扑、访问控制、数字资产、交易、事件和通道。最后，它以定义解决方案架构告终。

![解决方案组件](img/HLF_0802.png)

###### 图 8-2\. 解决方案组件

### 业务拓扑

我们的用例有三个利益相关者。Oracle 全球大学（OGU）是主管机构，拥有几个附属商学院，如 Oracle 商学院（OBS）。学习者被录取到 OBS，OBS 将他们的凭据提交给 OGU，后者向学习者颁发数字证书。以下是利益相关者：

Oracle 全球大学（OGU）

这是证书机构（数字资产），充当证书的批准者和发行者。它也是网络的创建者。

Oracle 商学院（OBS）

证书（数字资产）的创建者和请求者。

数字证书验证者（CVs）

潜在雇主、其他证书提供者（例如 Pearson VUE）、大学和其他权威机构。它还包括证书所有者，即学习者。

### 访问控制

不同的利益相关者对于访问和管理网络具有不同的权限。这些权限是通过访问权限设置的，比如赋予每个利益相关者的读或写权限，如 表 8-1 中所列。

表 8-1\. 网络参与者访问控制列表

| 组织 | 实体类型 | 访问类型 |
| --- | --- | --- |
| OGU | 创始人 | 读/写 |
| OBS | 认可参与者 | 读/写 |
| CVs | 参与者 | 读 |

### 通道

在我们的创始者发起的业务网络中，参与利益相关者（如 OBS 和 CVs）将通过区块链通道进行通信。此外，所有利益相关者都在处理相同的数字资产；参与者需要在具有适当访问权限的同一通道上。因此，我们将有一个通道，由创始者定义，其他参与者将加入该通道。

### 数字资产

一旦确定了利益相关者和网络拓扑，您需要专注于定义将存储在账本中的数字资产。对于这个用例，我们将有两个数字资产：学习者（证书所有者）信息和数字证书数据。

### 交易

在设计用例的解决方案时，我们建议绘制交易和事件。在数字资产的生命周期中，利益相关者将执行 表 8-2 中列出的交易。

表 8-2\. 交易和事件

| 交易 | 利益相关者 | 里程碑 | 描述 |
| --- | --- | --- | --- |
| `CreateReceiver` | OBS | 创建接收者 | 创建新的接收者或学生 |
| `AddCertificate` | OBS | 添加证书 | 为接收者插入证书 |
| `ApproveCertificate` | OGU | 证书已批准 | 批准证书 |
| **搜索操作** |  |  |  |
| `QueryByCert_id` | 所有 | N/A | 查询证书 |
| `QueryByRecev_id` | 所有 | N/A | 按 ID 查询接收者 |
| `GetCertificateHistory` | OGU/OBS/接收者 | N/A | 查询记录中一个键的历史 |
| `QueryAllCerts` | OGU/OBS | N/A | 查询所有学生的所有证书 |

### 解决方案架构

让我们检查用例的高层解决方案架构。几个组件以不同的方式相互交互和集成，通过协作以实现解决方案：

OBP 仪表板

这是为授权参与者提供执行各种任务的控制台。例如，OGU 用户可以创建隔间（Oracle 基础架构逻辑分区），定义区块链网络，创建通道，并允许其他参与者在通道上合作。

客户端 UI

不同的参与者和证书查看者可以使用客户端应用程序 UI 执行以下任务，例如：

+   具有 OBS 访问控制权限的用户可以搜索特定学习者的证书数据。他们还可以创建学习者条目，请求证书批准，并在账本上为学生插入证书数据。

+   具有 OGU 访问控制权限的用户可以搜索特定学习者的证书数据，还可以批准或拒绝学习者的证书数据。

+   证书验证器（CVs）包括学习者和查看者。学习者（证书所有者）可以使用客户端应用程序查看其证书数据及其批准状态，并生成一个令牌与其他证书验证者共享以验证其凭据。查看者是可以使用令牌验证学习者凭据的用户。

## 体验 Oracle Blockchain Platform

现在我们已经定义了关键组件，我们可以开始使用 OBP 创建具有 OBP 实例的网络利益相关者，配置 OBP 网络基础设施，并配置 OBP 交易基础设施。图 8-3 展示了本节中的主要任务和子任务。添加智能将在“体验解决方案”中进行讨论。

![任务和子任务的工作流程](img/HLF_0803.png)

###### 图 8-3\. 任务和子任务的工作流程

### 配置 Oracle Cloud 基础设施

在您深入创建区块链网络和运行交易之前，您将从 OCI 配置开始。需要执行的任务包括登录或注册，规划区块链版本，以及创建一个隔离区。

登录或注册

要开始，您需要一个 Oracle Cloud 账户。您可以注册一个免费的 Oracle 云促销活动，或者下订单购买 OBP。您的 Oracle Cloud 账户将包括 Oracle 身份和访问管理（IAM）和身份云服务（IDCS）。使用 IAM，您可以控制谁可以访问哪些云资源。作为云管理员，您使用 IDCS 添加用户，分配角色，并管理对区块链平台的访问。角色与 IAM 进行映射。

规划区块链版本

OBP 在包括欧洲、北美和 APAC 在内的许多地区都可用，并且其受欢迎程度正在增长。在您设置区块链网络之前，您需要计划使用任何特定的区块链平台版本。OBP 云服务提供两个版本：标准版包括两个 CPU、50 GB 存储和两个对等节点；企业版根据规模（小、中、大或 XL）提供从 4 到 32 个 CPU、150 GB 存储和两到六个对等节点不等。您可以根据负载需求调整企业版的规模（扩展或缩小）。为了简单起见，我们将创建一个标准版实例。

创建一个隔间

我们建议您为区块链网络创建一个单独的隔间。当您首次登录 OCI 时，Oracle 会自动为您的租户创建一个根隔间。作为 OCI 管理员，您可以在根隔间下创建额外的隔间，用于区块链网络。

以管理员用户身份登录，转到区块链平台，并选择适当的隔间。我们已为此用例创建了一个单独的隔间，即 `OracleBlockchainCompartment`。

### 创建 OBP 实例

根据业务拓扑，您将创建三个区块链实例：一个用于创始人（OGU），一个用于每个参与者（OBS 和 CV）。以下是本节的子任务：

1.  为 OGU 创建创始人区块链实例。

1.  为 OBS 创建参与者区块链实例。

1.  为 CVs 创建参与者区块链实例。

步骤如下：

1.  以联合 Oracle Identity Cloud 服务管理员用户的身份登录到您的 Oracle 云基础架构帐户。

1.  在控制台中，单击左上角的导航菜单，然后选择区块链平台。

1.  从隔间列表中选择要创建服务的隔间（`OracleBlockchainCompartment`）。

1.  输入创始人区块链实例显示名称 `**OGUInstance**` 和描述。

1.  选择“创建新网络”作为平台角色，因为这是一个创始者实例。

1.  选择标准版，该版本将提供两个 CPU、50 GB 存储和两个对等节点。

1.  点击创建实例。

1.  实例转到创建状态。配置区块链实例需要几分钟时间。一旦实例创建完成，状态将变为活动。

1.  点击服务控制台以导航至创始者的区块链实例。

1.  在区块链实例仪表板上，导航至节点选项卡。该选项卡列出所有节点，如下所示：

    1.  使用标准版，您将收到两个对等节点（`peer0` 和 `peer1`）、三个 Orderer 节点、一个 CA 和一个代理节点。还将有一个控制台节点。

    1.  您还将获得一个 `default` 通道。

同样，创建其他参与者实例。但是，在创建参与者实例时，请选择“加入网络”作为参与者角色。

### 创建一个区块链网络

一旦利益相关方实例建立完成，我们将为区块链实例创建区块链事务网络，这将在区块链实例之间建立连接，并在它们之间启用底层共享账本基础设施。要继续，初始任务是导出参与者组织证书，然后将参与者证书导入创始人组织。下一步是从创始人处导出 Orderer 设置，然后将 Orderer 设置导入参与者处。

### 导出参与者组织证书

参与者证书包含管理员、CA 和 TLS 的密钥，以及其签名。它是一个 JSON 文件。请按照以下步骤操作：

1.  导航至参与者的区块链实例并转至他们的仪表板。

1.  导航至网络选项卡。

1.  在其中一个参与者处点击导出证书。

1.  对所有其他参与者重复步骤 1 到 3。

### 将参与者证书导入创始人组织

在本节中，我们将把参与者的证书导入创始人组织。以下是步骤：

1.  转到创始人区块链仪表板。

1.  导航到“网络”选项卡。

1.  点击“添加组织”。

1.  在“添加组织”对话框中，浏览导出的证书的 JSON 文件，然后点击“添加”。

1.  成功添加文件后，点击“完成”。

### 从创始人导出 orderer 设置

接下来，我们将从创始人导出 orderer 配置到参与者。Orderers 与创始人关联，为了确保相同的 orderers 验证参与者提交的交易，我们建议将 orderer 设置从创始人导出并导入到参与者。

Orderer 设置包含创始人的证书、签名和 orderer 终端点，因此请按照以下步骤进行：

1.  转到创始人区块链实例的仪表板。

1.  导航到“网络”选项卡。

1.  点击“导出订单设置”。

1.  下载 JSON 文件，将在参与者处导入。

### 将 orderer 设置导入到参与者

现在，我们将按照以下步骤将 orderer 配置导入到参与者：

1.  转到参与者区块链实例的仪表板。

1.  导航到“网络”选项卡。

1.  点击 Orderer 设置。

1.  选择“导入”选项。

1.  浏览创始人的 orderer 设置 JSON 文件。

1.  点击“提交”以导入 orderer 设置。

### 创建交易基础设施

一旦创建了区块链网络和实例，并且创始人与参与者之间交换了 orderer 信息，您就可以创建区块链交易基础设施。基本上，此步骤将定义一个共享账本和相关的用于读取或读/写到共享账本的交易区块链实例。

### 在创始人处创建一个频道

在本节中，我们将创建频道。频道包括对等方、共享账本、实例化的链代码以及一个或多个 orderers。频道允许利益相关者（区块链实例）通过共享账本共享数据。按照以下步骤创建频道：

1.  转到创始人的仪表板。

1.  转到“频道”选项卡。

1.  点击“创建新频道”。

1.  输入通道的名称：`**verifyed**`（小写）。

1.  选择一个或多个参与者组织。

1.  根据前面定义的访问控制，选择参与者的访问控制。

1.  对于每个参与者，选择一个或多个对等体加入通道。我们为两个参与者选择了`peer0`。

1.  点击提交以创建通道。

### 将参与者的对等节点添加到通道

一旦在创始人实例上创建了通道，我们将向相同通道添加参与者的对等节点。这确保了由客户端应用程序在区块链网络上执行的交易由定义的对等节点处理。这些对等节点将验证和执行链代码，并执行 RWSet（ReadWriteSet）的创建。这些 RWSets 稍后会提交给排序节点进行排序并添加到分类帐中。按照以下步骤将参与者添加到通道：

1.  转到参与者仪表板。

1.  点击节点。

1.  找到对等体（`peer0`）。

1.  选择“加入新通道”。

1.  选择通道`verifyed`。

1.  点击提交。

这些步骤将向通道添加 OBS 和 CV 参与者的`peer0`。

###### 提示

你可以通过访问 Oracle 区块链平台控制台来查看区块链平台和 Hyperledger Fabric 版本。然后找到你的登录用户名，点击“关于”。这会显示区块链平台和 Hyperledger 版本号。

## 体验解决方案

现在我们已经定义了 OBP 实例，配置了 OBP 网络基础设施和 OBP 交易基础设施，我们可以专注于开发链代码并对其进行验证了。让我们继续通过将智能性添加到我们的 Fabric 网络来部署和实例化我们的 Fabric 链代码的最后一步。

### 开发链代码

链码可以用各种语言编写，如 Go、Node.js 和 Java。所有链码都需要打包成 ZIP 文件进行部署。但如果你的链码是一个单独的 *.go* 文件，你可以直接在 OBP 上部署和实例化链码，而不需要打包它。对于我们的用例，你可以在 [*https://myhsts.org/hyperledger-fabric-book/*](https://myhsts.org/hyperledger-fabric-book/) 找到源代码文件 *verifyed.go*。

### 使用 OBP 的应用程序构建器

OBP 为区块链应用程序构建者提供了简化和简化链码开发过程的功能。OBP 为链码开发注入了速度和灵活性。平台自动生成 CRUD 方法，可通过 REST API 直接使用或从自定义函数中调用。它支持各种类型的资产，包括嵌入式资产（模块化和嵌套的资产结构）和用户控制的链码版本管理。

OBP 允许您从规范文件生成链码，您可以在其中为 TypeScript（用于 Node.js 链码）或 Go（用于 Go 链码）指定资产。规范文件允许您定义多个资产、它们的数据模式、行为和验证规则。它促进了快速的链码生成，可以在本地机器上进行测试，或者通过在区块链应用程序构建器内的预配置区块链实例上部署到 OBP 网络（云或本地版本）。该平台包括两个接口：用于 CI/CD 自动化的 CLI（命令行）和用于基于 IDE 的交互式开发的 Visual Studio Code 扩展。

### 部署和实例化链码

OBP 提供了两种部署选项：快速和高级。快速部署选项可用于测试和开发 PoC。高级选项用于选定的对等节点和背书策略；因此，高级选项的步骤如下：

1.  转到创始人仪表板。

1.  导航至链码选项卡。

1.  单击部署新链码，然后选择高级选项。

1.  在高级选项对话框中，输入链码名称（`**verifyed**`）和链码版本（v1）。选择对等节点（`peer0`）并选择链码源，它将是一个单一（点）Go 文件。

1.  单击“下一步”以安装（部署）链码。

1.  成功安装链码后，高级部署对话框将跳转到实例化链码选项。输入频道名称（`**verifyed**`）。

1.  选择要参与交易的节点（`peer0`），并选择其他默认值。

1.  单击“下一步”。

REST 代理默认启用。创始人和其他参与者的 REST 代理列在仪表板的节点选项卡上。

### 在参与者处部署链码

一旦在创始人节点部署和实例化了链码，您可以导航到参与者的仪表板，然后转到链码选项卡，以在所有参与者处部署相同版本的链码，因为您不需要实例化链码。一旦在创始人处实例化，链码将保持实例化状态，因为实例化是特定于通道的，而不是特定于组织或对等方。

### 测试链码

链码部署和实例化后，您可以通过 REST 代理或使用模拟的 shim 来调用它。OBP 提供了一个 REST 代理，通过 REST 端点连接到链码。在实例化后，分类帐是空的，因此让我们继续进行测试。

首先，导航到创始人或参与者的仪表板，然后转到节点选项卡。启用了 `RESTPROXY` 节点。复制此 URL 以用于 REST 代理：

*https://<blockchain instance name>-<tenancy>-region.blockchain.ocp.oraclecloud.com:port/restproxy*

接下来，发送对`restproxy`端点的请求，它们以 JSON 格式并包含通道和链码信息。因为您可以在单个 REST 代理中配置多个链码，通道和链码信息有助于将请求发送到正确的链码。每次调用都应包含授权和内容类型。另外，REST 代理提供两个目标端点：*transaction/invocation*和*transaction/query*。您可以使用像 Postman 或 ReadyAPI 这样的任何 REST 测试工具来测试 REST 端点。标头有以下三个部分：

授权

使用您的 Oracle 云用户名和密码。

内容类型

使用*application/json*。

目标端点

使用此格式：*https://<blockchaininstancename>-<tenancy>-region.blockchain.ocp.oraclecloud.com:port/restproxy/bcsgw/rest/v1/transaction/invocation*

一旦测试步骤完成，您可以执行调用以插入证书接收者信息。将目标端点设置为`/invocation`，目标方法设置为`insertReceiver`。另外，设置`Input JSON`如下所示：

```
Input JSON - {
    "channel": "verified",
    "chaincode": "verifyed",
    "method": "insertReceiver",
    "args": [
       "008",
       "Noah",
       "App Dev"
    ],
    "chaincodeVer": "v1"
}
```

对于最后一步，我们查询端点。与查询证书所有者（接收者）类似，您可以通过其 ID 查询它，使用具有三个参数的查询端点：目标端点（`/query`），目标方法（`queryReceiverById`）和`Input JSON`：

```
Input JSON - {
   "channel": "verifyed",
    "chaincode": "verifyed",
    "method": "queryReceiverById",
    "args": [
       "008"
    ],
    "chaincodeVer": "v1"
}
```

### 验证分类账上的交易。

每个通道只有一个分类账，由创始人和参与组织共享。OBP 提供了在给定通道上查看共享分类账上的交易块的选项。按照以下步骤访问分类账并查看交易： 

1.  转到创始人仪表板。

1.  导航至通道。

1.  选择通道`verifyed`。

1.  点击分类账。

这列出了分类账上的所有区块。您可以从创世区块到最新区块找到区块。它还将用户交易与系统和创世区块分开。很明显，每个区块都存储了诸如交易 ID、状态、链码名称、方法名称、参数、结果、发起者和背书者等各种信息。

# 摘要

在本章中，您将学习如何在 AWS、IBM 和 Oracle 云平台上部署 Fabric。我们从讨论 Amazon 云平台开始。您学会了设置 Amazon 托管的区块链服务、一个 Fabric 网络和一个 Fabric 客户端来运行和管理链码。通过配置和运行 Fabric 应用程序，我们完成了 AWS 之旅。

接下来，我们解释了 IBM 云平台用于构建 Fabric 应用程序的特性、注意事项和能力。具体来说，我们向您展示了如何在 IBM 云上创建和加入 Fabric 网络，包括如何构建一个 Fabric 网络和创建一个排序器或通道。通过在 IBM 云上部署智能合约，我们结束了 IBM 部分。

最后，我们探讨了 Oracle 区块链平台、其提供的服务和架构。我们深入探讨了定义业务拓扑、访问控制、分区、资产和交易。此外，您还通过实验了解了 Oracle 区块链平台，体验了在其中设置 Fabric 网络、部署和测试链码的简便性。

下一章介绍了 Hyperledger Fabric v2 的新特性，例如新的链码应用模式和外部链码启动器。我们还讨论了如何更新 Fabric 组件以及通道的能力级别。
