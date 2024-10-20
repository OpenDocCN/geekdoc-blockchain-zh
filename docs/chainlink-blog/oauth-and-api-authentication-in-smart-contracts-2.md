# 智能合约中的 OAuth 和 API 身份验证

> 原文：<https://blog.chain.link/oauth-and-api-authentication-in-smart-contracts-2/>

OAuth 是一种流行的 [API 认证和授权](https://swagger.io/docs/specification/authentication/)形式，允许用户访问不同的网站和应用程序，而无需共享他们的凭证。起初，从外部的 Web2 服务(如 OAuth)获取数据到我们的区块链智能合同中似乎很困难。但是， [Chainlink 外部适配器](https://docs.chain.link/docs/external-adapters)使得链外执行困难的计算变得容易，和 OAuth 之类的 API 认证没什么区别。外部适配器使得使用 OAuth 访问更安全的外部数据源成为可能，并且可以从我们的智能合同链上轻松地与它们进行交互。我们可以从我们的 Solidity 或其他智能合约中调用这些安全 API 来访问具有这种高安全级别的多个服务。在本帖中，我们将浏览一个 [Reddit 外部适配器的例子。](https://market.link/adapters/21318744-2f78-4eef-bcbc-808608fde675)

## OAuth 是什么？

在与互联网交互时，为了访问数据，您通常需要证明您是谁。证明你是谁的最简单的方法是使用用户名和密码。这就是所谓的[密码或基本认证](https://swoopnow.com/password-authentication/#:~:text=Password%20authentication%20is%20a%20process,or%20an%20online%20banking%20tool.)方法。然而，我们可以想出另一种方法在网上证明我们就是我们在现实世界中声称的那个人，比如让别人为我们担保。这基本上是 OAuth:它是一种委托[令牌认证](https://www.okta.com/identity-101/what-is-token-based-authentication/)的形式，意味着一方授权给另一方认证。

OAuth 的工作原理是，双方通过一个提供的数字令牌，让一个可信的第三方来证明其中一方的身份。

假设 Bob 想从 Alice 那里获取数据，但不想给 Alice 他的密码或告诉她他是谁。鲍勃和爱丽丝都是玛格丽特的朋友。Margaret 告诉 Bob，她可以给他一个临时令牌，交给 Alice 以获取他的数据，Alice 不需要 Bob 的姓名或他的任何信息。爱丽丝只知道他们信任的某个人正在获取数据。Margaret 借给 Bob 一个令牌来访问 Alice，就像把酒店房间的钥匙借给别人一样。这是对 OAuth 如何工作的一个非常简单的解释。

当使用 OAuth 对系统进行编程时，需要额外的步骤来访问您正在寻找的数据，因为您首先必须等待来自可信第三方的响应才能继续。有了基本认证，你只需出示你的密码，就能在门口被接受或拒绝。对于 OAuth 身份验证，您必须等待来自第三方的令牌，然后您可以使用它在门口被拒绝或接受。

正如我们所知，像以太坊(1.0)这样的区块链在执行过程中是同步的。这意味着它们一次只能做一件事，而且为了进行 API 回调而不得不等待令牌，这可能有点笨拙。对于我们的 Solidity 代码来说，在进行另一个调用之前，必须等待一个令牌返回给我们，这也不是很省油。处理这一切的一个很好的方法是用一个 Chainlink 外部适配器一举脱离链条，使 [smart contract](https://chain.link/education/smart-contracts) OAuth 更快，在汽油方面成本更低。

## 节点中的 OAuth

当构建我们的外部适配器时，它处理来自我们的 Solidity smart 契约的 OAuth 授权，我们首先需要决定是要构建我们自己的 OAuth 处理程序还是要使用别人的。OAuth 处理程序只是一段代码，它允许我们轻松地处理登录和注销。大多数时候，如果有一个可行的解决方案，我们不想重新发明轮子。对于使用 OAuth 的平台，您通常可以在那里找到一个。例如，我们发现这个[神奇的 Reddit 处理程序](https://github.com/feross/reddit/blob/master/index.js)，我们甚至可以运行代码来看看它做了什么。

我们有两个主要功能:

```
async _getToken ()

```

和

```
_makeRequest (method, url, data, token)

```

可以想象，getToken()获取令牌，makeRequest 是我们的函数，它实际上将最终的身份验证请求和令牌一起发送到 Reddit URL。在这个实现中，它们都被包装起来，由 *_sendRequest 调用。*

我们可以看到 _getToken()函数实际上是通过使用基本认证来与第三方进行交互的。

```
return new Promise((resolve, reject) => {
      get.concat({
        url: TOKEN_BASE_URL,
        method: 'POST',
        form: {
          grant_type: 'password',
          username: this.username,
          password: this.password
        },
        headers: {
          authorization: `Basic ${Buffer.from(`${this.appId}:${this.appSecret}`).toString('base64')}`,
          'user-agent': this.userAgent
        },
        json: true,
        timeout: REQUEST_TIMEOUT
      }, (err, res, body) => {
        if (err) {
          err.message = `Error getting token: ${err.message}`
          return reject(err)
        }

```

_makeRequest()函数使用令牌而不是密码。

```
return new Promise((resolve, reject) => {
      const opts = {
        url: url,
        method: method,
        headers: {
          authorization: token,
          'user-agent': this.userAgent
        },
        timeout: REQUEST_TIMEOUT
      }

```

我们可以理解为什么使用已经完成的实现通常是更好的，但是了解它是如何工作的也很重要，这样我们就可以在需要的时候自己构建它。

一旦我们为 OAuth 设置了所有的代码，我们就可以为外部适配器填充样板文件了！您可以随时使用您喜欢的适配器，但我们将使用 [Chainlink 外部适配器模板。](https://github.com/thodges-gh/CL-EA-NodeJS-Template)如果你跟随了[构建外部适配器博客](https://blog.chain.link/build-and-use-external-adapters/)，剩下的就简单了！我们可以重新发明轮子，将所有这些代码复制粘贴到我们的外部适配器中，但是能够导入它会更好，这样我们就可以专注于我们的可靠性和智能契约代码，而不是身份验证。

## Reddit 外部适配器

既然我们已经设置了这个 OAuth 处理程序，我们可以将它添加到我们的 Chainlink 外部适配器中。这与其他[链节适配器](https://docs.chain.link/docs/adapters)的工作方式相似。我们可以将这个适配器添加到我们的列表中，并使用我们需要的 OAuth 授权来执行任何计算。查看 [Reddit 外部适配器](https://github.com/tweether-protocol/reddit-cl-ea)的代码，我们可以看到我们遵循了来自[第一个外部适配器教程](https://blog.chain.link/build-and-use-external-adapters/)的精确框架。正如我们之前关于外部适配器的博文一样，我们只需要更新 index.js 中的代码。主要区别是我们添加了一个新的包，在这个例子中，Reddit 包具有:

```
const Reddit = require('reddit')

```

我们像这样添加所有凭据:

```
const reddit = new Reddit({
  username: process.env.REDDIT_USER,
  password: process.env.REDDIT_PASSWORD,
  appId: process.env.REDDIT_API_KEY,
  appSecret: process.env.REDDIT_API_SECRET,
  userAgent: 'tweether',
})

```

一旦您从 Reddit 站点[创建了一个应用程序](https://www.reddit.com/prefs/apps)，您将获得您的 REDDIT_API_KEY 和 REDDIT_API_SECRET 以在适配器中使用。外部适配器有许多输入，我们可以使用这些输入来自定义我们想要从我们的智能契约发送到 Reddit 的内容。

```
const customParams = {
  sr: false,
  kind: false,
  resubmit: false,
  title: false,
  text: false,
  endpoint: false,
  url: false,
}

```

这些自定义参数都在 [Reddit API 文档](https://www.reddit.com/dev/api/)中进行了标识。

我们与模板的另一个主要区别是:我们没有使用请求者对象发送请求，而是使用 Reddit 对象:

```
 reddit
    .post(endpoint, {
      sr: sr,
      kind: kind,
      resubmit: resubmit,
      title: title,
      text: text,
      url: url,
    })
    .then((response) => {
      response.json.data.result = response.json.data.id
      response.json.status = 200
      callback(response.json.status, Requester.success(jobRunID, response.json))
    })
    .catch((error) => {
      callback(500, Requester.errored(jobRunID, error))
    })

```

做好 app 之后现在就可以自己测试了！

设置完这四个环境变量后，只需运行:

```
git clone https://github.com/tweether-protocol/reddit-cl-ea
cd reddit-cl-ea
yarn
yarn start

```

在另一个 shell 中，您可以使用以下命令进行测试:

```
curl -X POST -H "content-type:application/json" "http://localhost:8080/" --data '{ "id": 0, "data": {"title":"HELLO" }}'

```

你可以查看输出，看看你在 Reddit 上发布了什么！

如果有机会，您可以查看一下 [Twitter Chainlink 外部适配器](https://market.link/adapters/9ebb251e-1d7c-433d-9835-d771996f5b9c)，它允许您基于您的智能合同交互来发布状态。

这只是通过 OAuth 和 Reddit 与智能合约进行交互的第一步。您需要使用托管外部适配器的节点，并在节点中设置凭证。请务必查看关于如何进行下一步的 [Chainlink 文档](https://docs.chain.link/docs)，如果您在您的智能合约中使用了 OAuth，请务必将其上传到 [market.link](https://market.link/adapters/21318744-2f78-4eef-bcbc-808608fde675) ，这样您就可以帮助其他人通过他们的智能合约与现实世界进行交互。这也是展示你聪明的合同构建专业知识的好方法。

如果你是一名开发人员，并希望将你的智能合同连接到链外数据和系统，请访问[开发人员文档](https://docs.chain.link/)，并加入关于[不和谐](https://discordapp.com/invite/aSK4zew)的技术讨论。如果您想安排一次电话会议来更深入地讨论整合事宜，请点击此处的。

[网站](https://chain.link/) | [推特](https://twitter.com/chainlink)|[Reddit](https://www.reddit.com/r/Chainlink/)|[YouTube](https://www.youtube.com/channel/UCnjkrlqaWEBSnKZQ71gdyFA)|[电报](https://t.me/chainlinkofficial) | [事件](https://blog.chain.link/tag/events/) | [GitHub](https://github.com/smartcontractkit/chainlink) | [价格供稿](https://feeds.chain.link/) | [DeFi](https://defi.chain.link/)