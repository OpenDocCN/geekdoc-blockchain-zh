# 使用 Chainlink 外部适配器提取智能合同中的 IPFS 数据

> 原文：<https://blog.chain.link/fetch-ipfs-api-data-token-distribution/>

*chain link 2021 秋季黑客马拉松于 10 月 22 日拉开帷幕。* [*今天报名。*](https://chain.link/hackathon?utm_medium=referral&utm_source=chainlink-blog&utm_campaign=fall-2021-hackathon&utm_content=fetch-ipfs-data-in-smart-contracts-using-a-chainlink-external-adapter)

使用 [Chainlink 外部适配器](https://docs.chain.link/docs/external-adapters)连接分散式基础设施的各种组件是 Chainlink 网络帮助智能合约开发者更轻松地构建新用例及完全分散式应用的方式之一。来自 [ETHOnline Hackaton](https://blog.chain.link/ethonline-2020-chainlink-hackathon-winners/) 的 Chainlink 获奖者 Toshiake Takase 和 Tsukasa Noguchi 使用 Chainlink 的 oracle 基础设施和 IPFS，使 Audius 位于区块链的音乐流媒体平台上的艺术家能够向他们的粉丝分发代币奖励，而无需支付与成百上千笔个人交易相关的昂贵汽油费。

在本教程中，Iroiro 团队展示了如何使用 Chainlink 连接到 IPFS，以实现经济高效的令牌分发和各种其他以太坊基础设施用例。

* * *

由[高濑俊彦](https://twitter.com/toshiaki_takase)和[冢野口](https://twitter.com/wildmouse_)

## 介绍

除了作为货币有用之外，以太坊上的 ERC20 令牌标准还可以充当公用令牌。

在这种背景下，我们专注于代币作为创作者和粉丝之间交流方式的有用性，并开发了“[Iroiro](http://app.iroiro.social/)”(GitHub repository 在这里是)作为一个平台，使艺术创作者能够生成自己的 ERC20 代币并将其分发给粉丝。

这种类型的创建者令牌有许多潜在的使用案例，向粉丝分发这些令牌的目的会因创建者而异。有时只是为了表达感谢，有时是为了允许访问独家内容或体验，如私人聊天频道、直播或现场表演津贴。潜在独家奖励的范围是艺术家探索的另一个创作空间。

然而，以太坊目前的交易成本为许多交易设置了障碍。发送代币的成本很容易超过艺术家从增加的粉丝忠诚度中可能获得的任何好处。为了使粉丝奖励计划成为 ERC20 令牌的可扩展用例，我们需要实现一些支持基础设施，使其成为创作者的合理用例。

在本文中，我们将解释用于构建 Iroiro 的 Chainlink 和 IPFS 集成的技术细节。该实现可以作为其他 [Chainlink](https://chain.link/) 和 IPFS 用例的模型，以创建更高效的令牌分发模型。

## 奥迪斯 API

对于 ETHOnline 黑客马拉松，我们决定使用 [Audius](https://audius.org/) 来实现令牌分发。Audius 是一种分散式音乐流协议。

由于 Audius 拥有用户账户，并促进艺术家和追随者之间的关系，我们决定，作为这种关系的延伸，我们可以建立一个艺术家创建令牌并根据用户账户将其分发给粉丝的流程。

Audius 提供了一个 [API](https://github.com/AudiusProject/audius-protocol/tree/master/libs/src/api) ，通过它可以获取 Audius 开发的刺猬钱包中存储的账号的钱包地址，以及关注者地址。

因此，我们决定实施以下流程:

1.  生成创建者令牌的用户在其 Audius 帐户后获得一个地址列表
2.  创建者令牌生成器接收并存储追随者地址信息作为契约上的快照，并将地址设置为令牌分发目标
3.  每个追随者都会收到一个通知，通知他们在 dApp 之外有一个分发活动，如果他们有资格进行分发，他们就可以执行声明功能并收到一个令牌

## 智能合同和大量数据

然而，这个流程中的实现有一个问题，因为有时追随者的数量很大，特别是对于像 [RAC](https://audius.co/rac) 这样的著名艺术家。追随者的数量可以攀升到数万或数十万，随着像奥迪斯这样的创作者平台获得采纳，这个数字可能会增加。

如果我们试图在一个链上合同中记录所有追随者的地址，这将花费大量的汽油费，特别是在网络拥塞的时候，这将增加创造者的交易成本。

因此，我们的实现没有在契约中写入追随者信息，而是使用 IPFS 将其保存为一个离线文件。我们使用 Chainlink 来检查 IPFS 的地址是否作为奥迪斯钱包存在，从而将合同链接到大量数据，而无需在创建活动时消耗大量汽油。

## IPFS 外部适配器

### 关于 IPFS

IPFS 是一个存储媒体文件的分布式系统。上传的文件存储在分布式网络上。

在 Iroiro 中，由 Audius API 获得的追随者地址列表作为 JSON 文件中的字符串数组存储在 IPFS 中，因此它可以由 Chainlink IPFS 外部适配器检索。

### 连接 IPFS 和链环的问题

如果我们在这里简单地使用 Chainlink，我们将遇到一个问题，当它链接到 IPFS。这是因为 Chainlink 的[内置 HTTP GET 适配器](https://docs.chain.link/docs/adapters#httpget)可以检索 JSON 字符串中特定路径的值，但不能检索和返回整个值数组。

要保存和存储在 IPFS 上的 JSON 文件包含一个数组形式的地址列表，如下例所示。这意味着，为了让跟随者检查他们自己的地址是否存储在 JSON 文件中，必须构建一个 Chainlink 外部适配器来处理对地址数组的搜索。

```
{ 
    "addresses": [
        "address1", 
        "address2", 
        ...
    ]
}

```

### IPFS 外部适配器

我们开发了一个 Chainlink 外部适配器来实现上述问题中所需的功能。

外部适配器是一个独立的应用程序，它接受来自 Chainlink 节点的请求并执行必要的处理，以 Chainlink 节点可以处理的格式返回结果。

通过构建一个外部适配器，我们可以利用 Chainlink 实现灵活的功能，这是单独使用内置适配器无法实现的。

外部适配器将执行以下过程:

*   通过使用合同中的 Chainlink 请求时收到的 IPFS cid(指示文件的唯一密钥)获取 IPFS 文件。
*   验证用户地址是否存储在 IPFS 文件的字段中，以确认令牌分发目标。
*   如果存储了目标地址，Chainlink 将通过返回用户地址、活动地址和地址存储信息(布尔值)的散列作为返回值来完成请求。

## 我们如何整合 Chainlink

我们现在将使用代码来解释事件的顺序。

### 创作者一方

首先，我们来看看创作者这边的流程。

在前端登录 Audius。刺猬钱包允许你用你的邮箱地址和密码登录。

```
const audiusSignIn = useCallback(async () => {
    setIsSigningIn(true)
    const email = emailRef.current.value
    const password = passwordRef.current.value
    const { user } = await libs.Account.login(email, password)
    const followers = await libs.User.getFollowersForUser(100, 0, user.user_id)

    setIsSigningIn(false)
    setAudiusAccount(user)
    setAudiusFollowers(followers)
  }, [libs])

```

使用 Audius API
获取关注者列表登录完成后，使用 Audius API 获取关注者列表，然后从用户信息中提取钱包地址列表信息。

```
const signer = await provider.getSigner()
const walletAddress = await signer.getAddress()
const factory = new Contract(addresses.TokenFactory, abis.tokenFactory, provider)
const tokenAmount = await factory.tokenAmountOf(walletAddress)

let tokenId
for(let i = 0; i < tokenAmount.toNumber(); i++) {
    const address = await factory.creatorTokenOf(walletAddress, i+1)
    const lowerAddress = address.toLowerCase()
    const lowerTokenAddress = tokenAddress.toLowerCase()
    if( lowerTokenAddress === lowerAddress ) {
        tokenId = i+1
    }
}

let walletAddresses = []
for(let i = 0; i < audiusFollowers.length; i++) {
    walletAddresses.push(audiusFollowers[i].wallet)
}

```

将提取的地址列表作为 JSON 文件保存到 IPFS。

```
const json = {addresses: walletAddresses}
const { path } = await ipfs.add(JSON.stringify(json))

```

使用 IPFS cid
运行令牌分发活动使用您上传到 IPFS 的 JSON 文件的 cid 作为参数创建令牌分发活动合同。要上传的 cid 将是 Chainlink 将检索和使用的文件的密钥。

```
const audius = new Contract(addresses.Audius, abis.audius, signer)
const _followersNum = audiusFollowers.length

audius.addAudiusList(tokenId, path, _followersNum)

```

[图](https://thegraph.com/)获取当 TokenFactory 契约创建新令牌以及令牌被转移时发出的事件。然后前端使用由[子图](https://thegraph.com/docs/define-a-subgraph)提供的 GraphQL 获取这些信息。

### 风扇侧

接下来，我们来看看使用 Chainlink 的风扇侧的流动。

粉丝向合约发送提款请求，以确认提款的可用性。

```
function requestCheckingAddress(
    address _oracle,
    bytes32 _jobId,
    string memory userAddress,
    string memory tokenAddress,
    address token,
    uint256 fee
) public override returns (bytes32 requestId) {
    uint64 tokenId = tokenIdList[token];
    require(tokenId > 0, "Token is not registered");

    uint64 userId;
    if (userIdList[msg.sender] == 0) {
        userId = nextUserId;
        userIdList[msg.sender] = userId;
        nextUserId = nextUserId.add(1);
    } else {
        userId = userIdList[msg.sender];
    }
    string memory followersHash = followersHash[token];

    Chainlink.Request memory request = buildChainlinkRequest(_jobId, address(this), this.fulfill.selector);
    request.add("cid", followersHash);
    request.add("tokenAddress", tokenAddress);
    request.add("userAddress", userAddress);

    return sendChainlinkRequestTo(_oracle, request, fee);
}

```

接收请求的链式链接节点然后将使用外部适配器来获得 IPFS 信息。

在这种情况下，工作是检查提交请求的用户的地址是否包含在活动中要分发的地址列表中，并履行合同的结果。

使用外部适配器来实现 IPFS 是否具有特定信息的结果。IPFS 外部适配器执行以下流程并实现活动合同的结果。

*   接收存储在事件中的目标文件的用户 ID、用户地址、活动 ID 和 cid。
*   使用接收到的 cid 获取 IPFS 文件。检查目标用户地址是否在文件的地址数组中。
*   返回用户地址、活动地址和地址存储信息(布尔值)的“哈希值”(如下所述)。

```
app.post('/api', async (req, res) => {
    console.debug("request body: ", req.body)
    const cid = req.body.data.cid
    const userAddress = req.body.data.userAddress
    const tokenAddress = req.body.data.tokenAddress
    const userId = new BN(await Audius.methods.userIdList(userAddress).call())
        .mul(new BN(10).pow(new BN(21)))
    const tokenId = new BN(await Audius.methods.tokenIdList(tokenAddress).call())
        .mul(new BN(10))

    const content = await getFile(cid)

    const isClaimable = content.addresses.includes(userAddress)
    const claimKeyHash = getClaimKeyHash(userId, tokenId, isClaimable)
    console.debug("Claim key hash: ", claimKeyHash)

    return res.send({
        id: req.body.id,
        data: claimKeyHash
    })
})

const getClaimKeyHash = (userId, tokenId, isClimable) => {
    const truthyValue = isClimable ? 1 : 0;
    const truthyBN = new BN(truthyValue)
    const claimKey = userId.add(tokenId).add(truthyBN)
    console.debug("Claim key: ", claimKey.toString())

    return soliditySha3(claimKey)
}

```

## 关于哈希

在最后一个过程中，id 和 Boolean 组合的散列值作为 fulfill 函数的返回值返回，因为目前，Chainlink 请求实现只能接受单个值。

即使在实现函数中只返回一个布尔值，也不可能确定哪个用户或活动可以分发令牌。

因此，用户 id、活动 id 和`"is contained"`信息被组合成一个无符号的整数值，该整数值被转换成一个散列值并作为单个值存储在映射中。然后，契约方使用相同的过程生成散列，并检查目标散列是否存在于映射中。

这样，我们就可以确认撤军是可能的。

履行完毕后，粉丝方确认用户是否可以提现。

使用上述链接作业返回和存储的结果信息，用户调用合同来确认他/她是否可以退出合同。

如果发现结果是可撤销的，用户实际上可以发送一个`claim()`来执行撤销，并接收创建者的令牌。

```
function claim(address token) external override {
    require(isClaimable(token), "Account is not able to claim");

    followerClaimedTokens[token][msg.sender] = true;
    FanToken fanToken = FanToken(token);
    fanToken.transfer(msg.sender, distributedAmount(token));
}

```

这个应用程序的总体情况如下。

![Iroiro Architecture](img/6281b1fc487520f2438922d03ebdde46.png)

<figcaption id="caption-attachment-1644" class="wp-caption-text">Iroiro Architecture</figcaption>





## 我们用链环和 IPFS 完成了什么

我们已经实现了上述用于分发创建者令牌的流程，以及以下内容:

### 大幅降低天然气成本，提高交易效率

在大量数据需要大量汽油的情况下，我们通过使用 IPFS 离线存储数据并通过 Chainlink 检索数据，大幅降低了汽油成本。

这直接导致 Iroiro 用户的天然气价格降低，并有助于降低用户的准入门槛。

### 连接到链外数据

区块链不可能获取 IPFS 的文件内容并执行所需的逻辑，但我们可以使用 Chainlink 做到这一点。

这使得开发使用链外数据的高度可伸缩的智能契约成为可能。

### 一种灵活的令牌分发方法的实现

Iroiro 仅在黑客马拉松期间使用 Audius，但只要可以通过 API 获得要在其他平台上分发的数据，它就可以与各种平台一起工作。

使用 Chainlink 意味着灵活的分配现在是可能的，而不仅仅局限于链上分配方法。

## Iroiro 发展现状

自从赢得 ETHOnline hackathon 大奖后， [Iroiro 在以太坊 mainnet 上推出了](https://medium.com/iroiro-social-token/iroiro-mainnet-launch-and-start-uni-token-distribution-campaign-9bdd10869a6d)，并支持在 [xDai](https://xdai.iroiro.social/) 和 [Polygon 上分发代币。](https://t.co/LuVwyDbIQp?amp=1)

黑客马拉松中开发的平台已经得到了增强，允许更灵活的分发方法，并且将根据需要添加更多。

### IPFS 外部适配器

我们还在与 Iroiro 并行开发 IPFS 外部适配器。

在黑客马拉松中，我们专门为 Iroiro 开发了外部适配器，但在未来，我们将开发一个通用的 IPFS 外部适配器，可以不受限制地由各种合同使用。

如果您需要 Chainlink 外部适配器来实现您想要的功能，请联系我们。

## 关于这个话题的更多信息

*   [智能合同开发者使用 Chainlink 的主要方式](https://blog.chain.link/smart-contract-api-price-random/)
*   [测试 Chainlink 智能合约](https://blog.chain.link/testing-chainlink-smart-contracts/)
*   [实态随机数生成](https://blog.chain.link/random-number-generation-solidity/)

如果你是一个对使用 Chainlink 将智能合同与来自新区块链或任何其他数据源的数据连接起来感兴趣的开发者，请联系这里的[或访问](https://chainlink.typeform.com/to/gEwrPO)[开发者文档](https://docs.chain.link/)。您还可以订阅 [Chainlink 简讯](https://chn.lk/newsletter)，了解 Chainlink 堆栈中的最新信息。

*[chain link 2021 秋季黑客马拉松](https://chain.link/hackathon) 于 2021 年 10 月 22 日开赛。无论您是开发人员、创作人员、艺术家、区块链专家，还是该领域的新手，这个黑客马拉松都是启动您的智能合同开发之旅并向行业领先的导师学习的最佳场所。立即锁定您的席位，争夺超过$ 300，000 的奖金。T9】*

[Sign up today](https://chain.link/hackathon?utm_medium=referral&utm_source=chainlink-blog&utm_campaign=fall-2021-hackathon&utm_content=fetch-ipfs-data-in-smart-contracts-using-a-chainlink-external-adapter)