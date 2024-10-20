# 如何通过 Chainlink 外部适配器将 Tesla 车辆 API 连接到智能合同

> 原文：<https://blog.chain.link/create-tesla-smart-contract-rental/>

作为 Chainlink 虚拟黑客马拉松的大奖得主，智能合同开发者 Harry Papacharissiou 和 Matt Durkin 使用 Chainlink 外部适配器将特斯拉汽车 API 连接到 Chainlink [甲骨文](https://chain.link/education/blockchain-oracles)，用于点对点汽车租赁应用。他们的[特斯拉智能合约](https://github.com/pappas999/Link-My-Ride)是一个很好的例子，说明了 Chainlink 如何用于将链外 API 连接到智能合约，并实现全新的商业模式。在这篇文章中，Harry 和 Matt 讲述了他们是如何创建这个实现的。

* * *

*由[哈里](https://twitter.com/pappas9999?lang=en)和[马特](https://twitter.com/mdurkin92)杜金*

Chainlink 的[外部适配器](https://docs.chain.link/docs/external-adapters)功能可以轻松地将[智能合约](https://chain.link/education/smart-contracts)连接到任何 API，使智能合约的各种用例能够触发链外事件，并将防篡改数字协议带到外部系统。

特斯拉公司生产一系列创新的电动汽车，配备了技术先进的功能和特点。其中一个特性是一个丰富的 API，它可以为经过身份验证的客户端提供大量的车辆数据，以及远程执行各种车辆状态更改功能的权限。

通过外部适配器和 Chainlink 节点使用该 API，允许我们的特斯拉智能合约与特斯拉汽车完全集成，这开辟了几个独特的用例。

在这篇技术文章中，我们将讨论:

*   如何使用 Tesla 外部适配器与 Tesla API 交互
*   如何编写一个智能契约，通过 Chainlink 节点使用 Tesla 外部适配器来获取车辆数据并修改车辆状态

## 特斯拉 API

官方[特斯拉移动应用](https://play.google.com/store/apps/details?id=com.teslamotors.tesla&hl=en-US)让特斯拉车主可以访问车辆位置、里程表读数、车辆电池充电状态等数据，如[车辆数据 API](https://www.teslaapi.io/vehicles/state-and-settings#vehicle-data) 所示。手机应用程序还允许用户执行各种远程命令，如[锁定](https://www.teslaapi.io/vehicles/commands#lock-doors)和[解锁](https://www.teslaapi.io/vehicles/commands#unlock-doors)车辆、[远程启动车辆](https://www.teslaapi.io/vehicles/commands#remote-start-drive)、[打开](https://www.teslaapi.io/vehicles/commands#open-charge-port)和[关闭](https://www.teslaapi.io/vehicles/commands#close-charge-port)充电端口、[设置速度限制](https://www.teslaapi.io/vehicles/commands#speed-limit-set-limit)，以及[特斯拉远程命令列表](https://www.teslaapi.io/vehicles/commands)中列出的更多命令。

这个移动应用程序使用 REST API 连接到特斯拉的服务器，服务器反过来与每辆车通信。在撰写本文时，特斯拉还没有为他们的车主 API 发布任何官方文档，但社区开发者已经通过逆向工程的方式制作了[非官方文档](https://www.teslaapi.io/)。社区现在已经在几个有用的第三方应用程序中实现了 API，比如这个[自托管数据记录器](https://github.com/adriankumpf/teslamate)。

Tesla API 使用 [OAuth](https://blog.chain.link/oauth-and-api-authentication-in-smart-contracts-2/) 标准进行认证，由此 API 在对[认证端点](https://www.teslaapi.io/authentication/oauth#get-access-token)的请求成功后授予访问令牌。要求认证的对 API 的连续请求可以在请求报头中包括认证令牌，只要它没有过期或被[撤销](https://www.teslaapi.io/authentication/oauth#revoke-access-token)。Tesla API 生成的访问令牌具有相对较长的 45 天到期时间，并为每个身份验证请求生成一个寿命更长的刷新令牌。如果即将到期或过期，我们也可以请求新的访问令牌。

在您可以与 Tesla 车辆通信之前，您必须首先通过 HTTP POST 请求向认证 API 端点成功获取这些认证令牌之一。使用下面请求正文中的参数来完成此操作。在[特斯拉网站](https://www.tesla.com/)上设置特斯拉车辆账户所有者的登录邮箱和密码。

```
{
   "grant_type": "password",
   "client_id": "81527cff06843c8634fdc09e8ac0abefb46ac849f38fe1e431c2ef2106796384",
   "client_secret": "c7257eb71a564034f9419ee651c7d0e5f7aa6bfbd18bafb5c5c033b093bb2fa3",
   "email": "[email protected]",
   "password": "password"
}
```

然后，您将收到包含访问令牌的响应:

```
{
    "access_token": "bc031af9351deb7a33e92f689be9eaad4b840e98b49f050a5e951347f140493d",
    "token_type": "bearer",
    "expires_in": 3888000,
    "refresh_token": "77bfff0afe006b7093d7ee23e85d3c667d36c23181e1e938a049237c35aba19c",
    "created_at": 1598934492
}
```

一旦您有了一个有效的身份验证令牌，您就需要[找出您的车辆 ID](https://www.teslaapi.io/vehicles/list) ,方法是将报头中的身份验证令牌传递给所需的 API 端点:

```
curl -X POST https://owner-api.teslamotors.com/api/1/vehicles -H "content-type:application/json" -H "Authorization: Bearer bc031af9351deb7a33e92f689be9eaad4b840e98b49f050a5e951347f140493d"
```

所需的车辆 ID 将在 responses 'id_s '元素中返回。这是 Tesla 服务器将成功验证的车辆 ID。其他“id”和“vehicle_id”字段用于其他目的，不适用于 web 服务请求。

```
{
    "response": [
        {
            "id": 42555797050350370,
            "vehicle_id": 1832501921,
            "vin": "5YJ3F7EB1KF447777",
            "display_name": "BASED",
            "option_codes": "AD15,MDL3,PBSB,RENA,BT37,ID3W,RF3G,S3PB,DRLH,DV2W,W39B,APF0,COUS,BC3B,CH07,PC30,FC3P,FG31,GLFR,HL31,HM31,IL31,LTPB,MR31,FM3B,RS3H,SA3P,STCP,SC04,SU3C,T3CA,TW00,TM00,UT3P,WR00,AU3P,APH3,AF00,ZCST,MI00,CDM0",
            "color": null,
            "access_type": "OWNER",
            "tokens": [
                "7e6c201b322e9a43",
                "3487a30d7e9ff6ec"
            ],
            "state": "asleep",
            "in_service": false,
            "id_s": "42555797050350366",
            "calendar_enabled": true,
            "api_version": 10,
            "backseat_token": null,
            "backseat_token_updated_at": null,
            "vehicle_config": null
        }
    ],
    "count": 1
}
```

在上面的例子中，认证令牌**BC 031 af 9351 deb 7 a 33 e 92 f 689 be 9 ea ad 4b 840 e 98 b 49 f 050 a5e 951347 f 140493d**和车辆 ID **42555797050350366** 都将在对车辆的后续 API 调用中使用。

## Tesla 外部适配器

作为 Chainlink 虚拟黑客马拉松 2020 获奖作品 [Link My Ride](http://devpost.com/software/link-my-ride) 的一部分，我们创建了一个外部适配器，将 Chainlink 节点连接到特斯拉 API 的特定端点，以促进车主和租车者之间的点对点车辆租赁协议。

这个外部适配器现在已经[列在 chain link market](https://market.link/adapters/1c70368e-c2df-4e05-adde-27b257092cbe)t 上，可供其他开发人员使用、修改或扩展。

一旦你从 [Github](https://github.com/pappas999/Tesla-External-Adapter) 下载了外部适配器的代码，并按照说明让它运行，你就可以[将你的外部适配器添加到你的 Chainlink 节点](https://docs.chain.link/docs/node-operators)，然后创建一个使用它的[作业规范](https://docs.chain.link/docs/job-specifications)。如果你需要帮助设置一个链接节点，你可以看看这个指南。

这个示例作业规范查找来自特定的 [oracle 契约](https://docs.chain.link/docs/architecture-request-model#oracle-contract)地址的传入请求，将请求传递给外部适配器，然后将结果返回给智能契约。

```
{
  "initiators": [
    {
      "type": "runlog",
      "params": {
        "address": "0x05c8fadf1798437c143683e665800d58a42b6e19"
      }
    }
  ],
  "tasks": [
    {
      "type": "tesla-external-adapter",
      "confirmations": null,
      "params": {
      }
    },
    {
      "type": "ethbytes32",
      "confirmations": null,
      "params": {
      }
    },
    {
      "type": "ethtx",
      "confirmations": null,
      "params": {
      }
    }
  ],
  "startAt": null,
  "endAt": null
}
```

如果你没有特斯拉汽车，但仍然想使用外部适配器，你可以在以下位置使用部署为无服务器功能的适配器。这一个目前指向一个[模拟特斯拉服务器](https://github.com/mseminatore/teslamock)，它模仿真实特斯拉服务器的端点和响应:

```
https://australia-southeast1-link-my-ride.cloudfunctions.net/Tesla-External-Adapter
```

## 存储车辆认证令牌

如上所述，认证令牌认证对车辆的请求。将这些令牌暴露在链上是一种安全风险，因为它们控制对车辆的访问，并可用于精确定位车辆的确切位置。因此，我们需要一个解决方案来确保身份认证令牌可以被保留和使用，但不会暴露在链上其他人可以看到的地方。

如果您只需要将一辆车集成到您的智能合约中，那么最简单的解决方案是将身份验证令牌作为环境变量存储在适配器运行的主机上。您可以在本[构建外部适配器指南](https://blog.chain.link/build-and-use-external-adapters/)中找到演示。但是，如果需要为多辆车存储和访问多个身份验证令牌，该怎么办呢？

在这样的场景中，外部适配器需要存储和检索多个键/值对。密钥是车辆 ID 或每辆车的某个唯一标识符，值是认证令牌。在外部适配器中存储和使用多个键/值对有许多解决方案。最具创新性的解决方案之一是将云无服务器 NoSQL 数据存储用于身份验证令牌。如果您还将外部适配器作为无服务器功能在首选云提供商上运行，您的外部适配器将成为真正的无服务器、高度可用和可扩展的混合区块链/云功能。

这个外部适配器使用[谷歌云的 Firestore NoSQL 文档数据库](https://cloud.google.com/firestore)来支持存储&检索多个车辆认证令牌。要建立 Firestore 数据库，请遵循[指南](https://firebase.google.com/docs/firestore/quickstart)。如果你没有谷歌云账户，你可以注册一个[免费](https://cloud.google.com/free)账户。

一旦设置好 Firestore 数据库，您就可以为外部适配器设置所需的环境变量，然后按照[外部适配器文档](https://github.com/pappas999/Tesla-External-Adapter)中的说明启动它。

一旦外部适配器和 Firestore 数据库开始运行，进入智能合同的最后一步就是对车辆进行认证。身份验证过程是这样的:适配器获取关于车辆的特定信息，使用这些信息连接到 Tesla 服务器，然后将给定的车辆 ID 和身份验证令牌作为新的键/值对存储在 Firestore 数据库中，最后返回成功消息。从这一点开始，对给定车辆 ID 的任何请求都不需要身份验证令牌。当需要时，外部适配器将从 Firestore 数据库获得它。

要执行此步骤，请按以下格式向外部适配器 URL 发出 HTTP POST 请求。在本例中，作业 ID 是 534 ea 675 a 9524 e8e 834585 b 00368 b 178；我们将在对 Tesla 服务器的请求中使用车辆 ID 和 apiToken 字段。authenticate 动作告诉适配器对给定的车辆详细信息进行身份验证，然后如果凭证有效，它将车辆详细信息存储在 Firestore 数据库中。

```
curl -X POST -H "content-type:application/json" "http://localhost:8080/" --data '{ "id": 534ea675a9524e8e834585b00368b178, "data": { "apiToken": "81527cff06843c8634fdc09e8ac0abefb46ac849f38fe1e431c2ef2106796384", "vehicleId": "42555797050350777", "action": "authenticate" } }'
```

我们可以使用 REST 客户端手动发出请求，直接通过 web 应用程序，或者如果适配器安全性只允许来自特定 Chainlink 节点的连接，那么您可以通过下面演示的 [web 发起的](https://docs.chain.link/docs/initiators#web)作业规范来发起请求。在此示例中，身份验证请求进入 Chainlink 节点，该节点将其转发到外部适配器(以及所有参数)，然后外部适配器将结果发送到智能合约中的链上函数:

```
{
  "initiators": [
    {
      "type": "web",
      "params": {
      }
    }
  ],
  "tasks": [
    {
      "type": "tesla-external-adapter",
      "confirmations": null,
      "params": {
      }
    },
    {
      "type": "ethtx",
      "confirmations": 0,
      "params": {
        "address": "0x1EF45689050F47BAc80Df38A10a199bb26af0f6b",
        "functionSelector": "approveVehicle(address)"
      }
    }
  ],
  "startAt": null,
  "endAt": null
}
```

一旦外部适配器正在运行并且已经认证了车辆，我们需要采取适当的步骤来保护对适配器的访问。我们可以在适配器内部和周围构建额外的安全性，以确保只有授权的 Chainlink 节点或进程有权调用外部适配器。您可以通过[白名单](https://en.wikipedia.org/wiki/Whitelisting)在适配器内部实现这一点。如果适配器在云环境中作为[无服务器功能运行，您可以在那里配置安全性和角色访问。](https://cloud.google.com/functions/docs/securing)

## 创建智能合同

现在，我们正在运行一个外部适配器，我们已经将它添加到 Chainlink 节点作业规范中，并且我们还安全地存储了一个经过验证的车辆身份验证令牌。接下来，我们可以创建一个智能契约来对车辆执行操作，同时获取关于车辆位置、里程表和电量的数据。

第一步是创建一个新的 [API 消费者契约](https://docs.chain.link/docs/make-a-http-get-request#config)，为您首选的以太坊网络设置所有必需的参数。

您应该在合同中创建两个函数:“unlockVehicle”和“unlockVehicleCallback”，如下例所示。调用 unlockVehicle 函数与 Tesla 车辆进行交互。

unlockVehicle 函数将车辆 ID 和作业 ID 作为参数。这应该是前面 Tesla 外部适配器部分提到的第一个作业规范的 ID。我们将链接支付金额设置为 0.1 链接。这是我们的 Solidity 示例，它通过我们的 Chainlink oracle 发出 HTTP POST 请求。

```
function unlockVehicle(string _vehicleId, bytes32 _jobId) external {
    Chainlink.Request memory req = buildChainlinkRequest(jobId, address(this), this.unlockVehicleCallback.selector);
    req.add("apiToken", "");
    req.add("vehicleId", _vehicleId);
    req.add("action", "unlock");
    sendChainlinkRequestTo(chainlinkOracleAddress(), req, 0.1 * 1 ether); 
}
```

如果对 Tesla 服务器的调用成功，车辆将解锁车门，并返回一条成功消息和一个 JSON 对象，其中包含车辆里程表、电量百分比和位置坐标:

```
{
    "jobRunID": 134ea675a9524e8e231585b00368b178,
    "data": "{50000,55,-35008518,138575206}",
    "result": null,
    "statusCode": 200
}
```

该响应数据将被返回到 unlockVehicleCallback 函数，在该函数中，我们可以手动提取链上存储的每个值:

```
function unlockVehicleCallback(bytes32 _requestId, bytes32 _vehicleData) public recordChainlinkFulfillment(_requestId) {
    //first split the results into individual strings based on the delimiter
    var s = bytes32ToString(_vehicleData).toSlice();
    var delim = ",".toSlice();

    //store each string in an array
    string[] memory splitResults = new string[](s.count(delim)+ 1);                  
    for (uint i = 0; i < splitResults.length; i++) {                              
        splitResults[i] = s.split(delim).toString();                              
    }                                                        

    //Now for each one, convert to uint
    odometer = stringToUint(splitResults[0]);
    chargeState = stringToUint(splitResults[1]);
    tmpLongitude = stringToUint(splitResults[2]);
    tmpLatitude = stringToUint(splitResults[3]);

    //Now store location coordinates in signed variables. Will always be positive, but will check in the next step if need to make negative
    vehicleLongitude =  int(tmpLongitude);
    vehicleLatitude =  int(tmpLatitude);

    //Finally, check first bye in the string for the location variables. If it was a '-', then multiply location coordinate by -1
    //first get the first byte of each location coordinate string
    longitudeBytes = bytes(splitResults[2]);
    latitudeBytes = bytes(splitResults[3]);

    //First check longitude
    if (uint(longitudeBytes[0]) == 0x2d) {
        //first byte was a '-', multiply result by -1
        vehicleLongitude = vehicleLongitude * -1;
    }

    //Now check latitude
    if (uint(latitudeBytes[0]) == 0x2d) {
        //first byte was a '-', multiply result by -1
        vehicleLatitude = vehicleLatitude * -1;
    }

    //Emit an event with the vehicle data
    emit vehicleDetails(odometer, chargeState, vehicleLongitude, vehicleLatitude);
}
```

上述合同的完整工作版本可以在 GitHub 上获得，或者你可以使用易于部署的 T2 Remix 链接。该实现目前连接到一个模拟 Tesla 服务器，用于开发和测试。为了将其修改为生产环境并连接到实际的 Tesla 车辆，我们需要将作业规范更新为在 Tesla 外部适配器上运行的作业规范，该适配器指向实时 Tesla 生产服务器。

## 摘要

使用 Chainlink 网络及其多功能外部适配器功能，我们展示了如何将智能合同与特斯拉汽车集成。这种集成使智能合同能够完全访问特斯拉丰富的车辆数据，并能够执行所有可以远程在车辆上执行的各种操作。

这一演示为智能合同和车辆集成开辟了许多令人兴奋的潜在用例，如点对点车辆租赁，正如我们的 Chainlink 虚拟黑客马拉松 2020 获奖作品 [Link My Ride](https://devpost.com/software/link-my-ride) 所示。其他用例可能包括短期的每次使用车辆注册或数据驱动的车辆保险，可以实时适应驾驶员的行为。随着我们快速迈向一个拥有自动驾驶汽车的世界，我们越来越容易想象在无人驾驶汽车中预订和旅行，由一个高度安全、确定性的智能合同管理车主和客户之间的协议和交易。

## 了解更多信息

如果您是一名开发人员，并且希望将您的智能合约连接到底层区块链之外的现有数据和基础设施，请联系此处的[或访问](https://chainlink.typeform.com/to/gEwrPO)[开发人员文档](https://docs.chain.link/)。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[|](https://www.reddit.com/r/Chainlink/)[不和](https://discordapp.com/invite/aSK4zew)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://defi.chain.link/)