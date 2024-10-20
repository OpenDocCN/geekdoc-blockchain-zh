# 如何创建 NFT

> 原文：<https://blog.chain.link/how-to-create-an-nft/>

[](https://chain.link/education/nfts)不可替代代币，或 NFT，是区块链上的数字代币，每个代币代表一些独特的东西，如一件数字艺术品、一件特殊的游戏内物品、一张稀有的交易卡收藏品或任何其他独特的数字/实物资产。NFT 与可替换的令牌相反:每个都是唯一的，不能与自身的另一个版本交换。持有人关心的是他们持有哪个代币，而不是有多少。

在本技术教程中，您将学习如何开发 NFT 收藏并将其部署到 OpenSea 市场。你的表情符号将是不同背景颜色的单一表情符号。每个 NFT 的表情符号和背景颜色的组合将使用来自[chain link VRF](https://docs.chain.link/docs/chainlink-vrf/)的可验证随机数生成。

让我们开始吧。

## 克隆回购

第一步是继续进行并克隆 [Chainlink 智能合同实例库](https://github.com/smartcontractkit/smart-contract-examples) 。完成后，导航到随机 SVG NFT 目录并安装必要的依赖项。

```
git clone https://github.com/smartcontractkit/smart-contract-examples.git
cd smart-contract-examples/random-svg-nft

yarn
```

然后，在您选择的代码编辑器中打开项目。按照项目的“Readme”文件中的说明设置所需的环境变量(您需要注册一个免费的 [炼金术](https://www.alchemy.com/) 账户和一个免费的 [以太扫描 API 密钥](https://etherscan.io/apis) )。在本教程中，我们将在以太坊上使用 Rinkeby testnet。

```
ETHERSCAN_API_KEY=<YOUR ETHERSCAN API>

RINKEBY_URL=https://eth-rinkeby.alchemyapi.io/v2/<YOUR ALCHEMY KEY>

PRIVATE_KEY=<YOUR PRIVATE KEY>
```

## NFT 元数据

链接到 NFT 的元数据提供了描述性信息，使 marketplaces 和 dApps 能够显示该令牌的可视化表示。开发人员要做的第一个决定是如何以及在哪里存储这些数据:这些数据可以完全写在智能合约本身中(链上)，也可以托管在 IPFS 或 Filecoin 这样的分散存储解决方案上(链下)。在本教程中，我们将通过基于随机值生成 NFT 艺术并将这些值的 SVG 表示存储在智能合约中来存储链上的元数据。

## 开发 NFT 智能合同

创建一个名为`EmojiNFT.sol`的新实体文件。我们将从 OpenZeppelin library 继承一些智能合同，并使用 Chainlink VRF。

让我们也初始化存储变量，并用您最喜欢的表情符号填充一个`emojis`数组。为什么不用你手机上用过的最后十个表情符号？

```
//SPDX-License-Identifier: MIT

pragma solidity ^0.8.7;

import "@chainlink/contracts/src/v0.8/interfaces/VRFCoordinatorV2Interface.sol";

import "@chainlink/contracts/src/v0.8/VRFConsumerBaseV2.sol";

import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";

import "@openzeppelin/contracts/utils/Counters.sol";

import "@openzeppelin/contracts/utils/Strings.sol";

import "@openzeppelin/contracts/utils/Base64.sol";

contract EmojiNFT is ERC721URIStorage, VRFConsumerBaseV2 {

  using Counters for Counters.Counter;

  Counters.Counter private tokenIds;

  string[] private emojis = [

    unicode"😁",

    unicode"😂",

    unicode"😍",

    unicode"😭",

    unicode"😴",

    unicode"😎",

    unicode"🤑",

    unicode"🥳",

    unicode"😱",

    unicode"🙄"

  ];

  VRFCoordinatorV2Interface internal immutable vrfCoordinator;

  bytes32 internal immutable keyHash;

  uint64 internal immutable subscriptionId;

  uint32 internal immutable callbackGasLimit;

  uint32 internal immutable numWords;

  uint16 internal immutable requestConfirmations;

  mapping(uint256 => address) requestToSender;

  event RandomnessRequested(uint256 indexed requestId);
```

为了确保智能合约将被正确部署，让我们添加一个`constructor`函数，并使用“EmojiNFT”作为集合名称，使用“EMOJI”作为滚动条。您可以随意更改这些值，并随意命名您的集合。

```
  constructor(

    address _vrfCoordinator,

    bytes32 _keyHash,

    uint64 _subscriptionId,

    uint32 _callbackGasLimit,

    uint16 _requestConfirmations

  ) VRFConsumerBaseV2(_vrfCoordinator) ERC721("EmojiNFT", "EMOJI") {

    vrfCoordinator = VRFCoordinatorV2Interface(_vrfCoordinator);

    keyHash = _keyHash;

    subscriptionId = _subscriptionId;

    callbackGasLimit = _callbackGasLimit;

    numWords = 4;

    requestConfirmations = _requestConfirmations;

  }
```

现在让我们添加一个创建新的 NFT 的方法。我们的方法将从 Chainlink VRF 请求四个随机值，然后在`fulfillRandomWords`函数中，根据第一个随机值从数组中获取表情符号，根据其余三个随机值生成随机颜色，生成链上 SVG 文件，创建 OpenSea 兼容的令牌 URL，并创建一个新的 NFT。由于链节 VRF 是异步的，我们将使用`requestToSender`将所有链节 VRF 请求映射到令牌的 minter。

```
  function mint() public returns (uint256 requestId) {

    requestId = vrfCoordinator.requestRandomWords(

      keyHash,

      subscriptionId,

      requestConfirmations,

      callbackGasLimit,

      numWords

    );

    requestToSender[requestId] = msg.sender;

    emit RandomnessRequested(requestId);

  }

  function fulfillRandomWords(uint256 requestId, uint256[] memory randomNumbers)

    internal

    override

  {

    uint256 tokenId = tokenIds.current();

    uint256 emojiIndex = (randomNumbers[0] % emojis.length) + 1;

    string memory emoji = emojis[emojiIndex];

    string memory color = pickRandomColor(randomNumbers[1], randomNumbers[2], randomNumbers[3]);

    string memory svg = createOnChainSvg(emoji, color);

    string memory tokenUri = createTokenUri(emoji, svg);

    _safeMint(requestToSender[requestId], tokenId);

    _setTokenURI(tokenId, tokenUri);

    tokenIds.increment();

  }

}
```

最后一步是为缺失的`pickRandomColor`、`createOnChainSvg`和`createTokenUri`函数添加代码。

我们将使用 VRF 链为我们的 NFT 作品生成一个随机背景色，要求三个不同的随机值，每个值代表 RGB 格式的颜色。RGB 是一种颜色模型，其中三原色被组合以产生另一种颜色。RGB 通常用于计算机科学以及电视、摄像机和显示器。

每个参数(红色、绿色和蓝色)将颜色的强度定义为 0 到 255 之间的整数。例如，rgb(0，0，255)渲染为蓝色，因为蓝色参数设置为其最高值(255)，其他参数设置为 0。类似地，rgb(255，0，0)呈现为红色。

由于 VRF 提供的值可能远大于 255，我们需要执行模除法来计算 r、g 和 b 参数。

```
  function pickRandomColor(uint256 firstRandomNumber, uint256 secondRandomNumber, uint256 thirdRandomNumber)

    internal

    pure

    returns (string memory)

  {

    uint256 r = firstRandomNumber % 256;

    uint256 g = secondRandomNumber % 256;

    uint256 b = thirdRandomNumber % 256;

    return

      string(

        abi.encodePacked(

          "rgb(",

          Strings.toString(r),

          ", ",

          Strings.toString(g),

          ", ",

          Strings.toString(b),

          ");"

        )

      );

  }
```

SVG(可缩放矢量图形)是一种基于 XML 的标记语言，用于描述基于二维的矢量图形。基本上，SVG 是一个图像，但是是用代码构建的图像。这些图像可以以任何分辨率高质量打印，即使调整大小也不会损失任何质量。这就是为什么 SVG 是我们用例的完美格式，我们在链上完全存储 NFT 元数据，并创建真正永久的令牌-我们的 SVG 可以从令牌元数据生成，不依赖于外部托管。

```
  function createOnChainSvg(string memory emoji, string memory color) internal pure returns(string memory svg) {

    string memory baseSvg = "<svg xmlns='http://www.w3.org/2000/svg' preserveAspectRatio='xMinYMin meet' viewBox='0 0 350 350'><style>.base { font-size: 100px; }</style><rect width='100%' height='100%' style='fill:";

    string memory afterColorSvg = "' /><text x='50%' y='50%' class='base' dominant-baseline='middle' text-anchor='middle'>";

    svg = string(abi.encodePacked(baseSvg, color, afterColorSvg, emoji, "</text></svg>"));

  }
```

令牌 URL 是指向令牌元数据的链接。在我们的例子中，它将包含带有“名称”、“描述”和“图像”属性的 JSON，看起来像这样:

```
{"name": "😍", "description": "Random Emoji NFT Collection Powered by Chainlink VRF", "image": "data:image/svg+xml;base64,PHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHByZXNlcnZlQXNwZWN0UmF0aW89J3hNaW5ZTWluIG1lZXQnIHZpZXdCb3g9JzAgMCAzNTAgMzUwJz48c3R5bGU+LmJhc2UgeyBmb250LXNpemU6IDEwMHB4OyB9PC9zdHlsZT48cmVjdCB3aWR0aD0nMTAwJScgaGVpZ2h0PScxMDAlJyBzdHlsZT0nZmlsbDpyZ2IoNDcsIDIyNCwgNzYpOycgLz48dGV4dCB4PSc1MCUnIHk9JzUwJScgY2xhc3M9J2Jhc2UnIGRvbWluYW50LWJhc2VsaW5lPSdtaWRkbGUnIHRleHQtYW5jaG9yPSdtaWRkbGUnPvCfmI08L3RleHQ+PC9zdmc+"}
Notice that the SVG image representation is Base64 encoded to match OpenSea’s requirements.
```

```
  function createTokenUri(string memory emoji, string memory svg) internal pure returns(string memory tokenUri) {

    string memory json = Base64.encode(

      bytes(

        string(

          abi.encodePacked(

            '{"name": "',

            emoji,

            '", "description": "Random Emoji NFT Collection Powered by Chainlink VRF", "image": "data:image/svg+xml;base64,',

            Base64.encode(bytes(svg)),

            '"}'

          )

        )

      )

    );

      tokenUri = string(

      abi.encodePacked("data:application/json;base64,", json)

    );

  }
```

## VRF v2 的应用

为了获得区块链的随机值，我们将使用最近发布的 Chainlink VRF v2。新版本的 VRF 对你的智能合约的融资和请求随机性的方式进行了一些改进。

首先，导航至 [VRF 订阅页面](https://vrf.chain.link/) ，选择 Rinkeby 网络，连接钱包，点击“创建订阅”。然后，将您的`subscriptionId`保存为`SUBSCRIPTION_ID`环境变量。通过键入:部署 EmojiNFT 智能合约

```
yarn deploy
```

或

```
SUBSCRIPTION_ID=<your_subscription_id> yarn deploy
```

部署后，返回 VRF 订阅页面，导航至您的订阅，点击“添加消费者”按钮，粘贴最近部署的合同的地址。

最后，用几个 Rinkeby 测试链接代币资助你的订阅。你可以在 [水龙头处得到它们。](https://faucets.chain.link/)

## 铸造您的代币并在 OpenSea 上交易

现在，您可以轻松铸造您的代币，方法是将您的钱包连接到 Etherscan 并点击“铸造”功能，或者创建一个 dApp UI 来与您的智能合约交互。铸币后，前往 Rinkeby 上的 [OpenSea，搜索你的 NFT 收藏或钱包地址。](https://testnets.opensea.io/)

## 总结

在这篇文章中，你已经学习了如何写一个 NFT 智能合同，链上和链下 NFT 元数据的区别，如何使用 VRF 链，以及如何在 Solidity 中生成 SVG 图像，并在 NFT 市场如 OpenSea 上正确显示它们。要了解更多信息，请访问 [Chainlink 智能合同示例库](https://github.com/smartcontractkit/smart-contract-examples) ，开始尝试这个和其他示例项目。 

[![A clickable link to a guide on how to build a successful NFT project.](img/e3fddcb2a3e50e1a361f25b80c541699.png)](https://chain.link/resources/5-steps-to-building-nft-project)

<figcaption id="caption-attachment-5082" class="wp-caption-text">A downloadable guide to building a successful NFT project.</figcaption>



访问[chain . link](https://chain.link/)或阅读[docs . chain . link](https://docs.chain.link/)上的文档，了解更多关于 Chainlink 的信息。要讨论整合，[联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF)。