# 用安全帽打造你自己的动感 NFT

> 原文：<https://blog.chain.link/dynamic-nft-hardhat/>

现在， [NFTs](https://chain.link/education/nfts) 已经成为主流，开发者、游戏玩家和收藏家都开始探索如何让这些独特的数字资产拥有新的功能，并释放更丰富的应用内动态。在我们过去的教程中，我们已经走过了如何使用 chain link[Oracle](https://chain.link/education/blockchain-oracles)到[构建、部署和销售 NFT](https://blog.chain.link/build-deploy-and-sell-your-own-dynamic-nft/)的过程，这些 NFT 是可验证的独特的，并且对现实世界的输入做出响应。这些[动态 NFT](https://blog.chain.link/create-dynamic-nfts-using-chainlink-oracles/)被证明是下一代 NFT，远远超越静态数字收藏品。想象一下，NFT 每次转让都会发生变化:艺术家可以制作一件艺术品，每次有人购买时，VRF 链家都会产生随机变化，使艺术品对买家来说变得独一无二。

这正是我们在本文中要做的:创建、部署并列出一个动态 NFT (dNFT ),它在每次传输时都会以可验证的随机方式发生变化。具体来说，我们将创造一个薛定谔的猫的衍生产品，在睡觉和攻击之间切换。

## 克隆动态 NFT 回购协议

第一步是继续克隆动态 NFT 回购协议。

```
git clone https://github.com/ZakAyesh/DynamicNFT.git
cd DynamicNFT
```

完成后，继续在您选择的代码编辑器中打开项目。你现在需要按照项目的[自述文件](https://github.com/pappas999/chainlink-hardhat-box)中的说明来设置所需的环境变量(你需要从 [Infura](https://infura.io/) 获得一个免费账户)。在本教程中，我们将在以太坊上使用 Rinkeby testnet。

```
export RINKEBY_RPC_URL='www.infura.io/asdfadsfafdadf'
export PRIVATE_KEY='abcdef'
```

如果您不熟悉环境变量，也可以将环境变量添加到. env 文件中。

```
RINKEBY_RPC_URL='www.infura.io/asdfadsfafdadf
PRIVATE_KEY='abcdef'
```

## 了解智能合同逻辑

转到合同文件夹，打开名为`dNFT.sol`的文件。一旦到了那里，你会注意到一些事情。首先，我们继承了 OpenZeppelin 的 ERC721 契约和 Chainlink 的 VRFConsumerBase。然后我们有 VRF 的存储变量，它将在我们的构造函数中初始化。

```
//State variables to store needed info for VRF
bytes32 internal keyHash;
uint32 internal fee;
```

接下来，我们开始定义 dNFT 所需的所有状态变量。这些对于你自己的 dNFT 可能是不同的，但是你可以把这些作为参考。

```
uint256 public tokenCounter;
enum EigenValue {HESLEEP, HEATTAC, SUPERPOSITION}
string[] IpfsUri = [ .... ];
mapping(uint256 => EigenValue) public tokenIdToEigenValue;
mapping(bytes32 => uint256) public requestIdToTokenId;
```

代币计数器记录我们铸造的每一个 dNFT。`EigenValue`是我们想要在链上跟踪的 dNFT 的属性，IpfsUri 是具有 NFT 的每个突变的所有 Uri 的数组，`tokenIdToEigenValue`跟踪每个 NFT 是什么`EigenValue`。由于 [Chainlink VRF](https://chain.link/solutions/chainlink-vrf) 是异步的，我们使用一个`requestIdToTokenId`将所有 Chainlink VRF 请求映射到我们正在传输的令牌。特征值可以变成你想在链上跟踪的任何类型的属性:颜色、大小、名称等(注意，对于本教程，链上属性实际上并不影响 NFT，但是有更多描述链上存储的 NFT 的不可变信息是很酷的)。

接下来是`createCollectible`函数，它创建我们的 dNFT，并将其初始化为一个初始属性(在本例中是一个初始特征值)。与该属性对应的 URI。该函数做的最后一件事是将令牌计数器加 1。

```
function createCollectible() public {
    uint256 newItemId = tokenCounter;
    string memory initialUri = IpfsUri[2];
    EigenValue initialEigenVal = EigenValue(2);
    _safeMint(msg.sender, newItemId);
    _setTokenURI(newItemId, initialUri);
    tokenIdToEigenValue[newItemId] = initialEigenVal;
    tokenCounter = tokenCounter + 1;
}
```

接下来是`transferFrom`函数，它在被调用时实际调用 VRF。为此，我们覆盖 openzeplin ERC-721 transfer from 函数来添加新的逻辑。然后，该函数使用块号作为我们提供的种子来调用 VRF，并在映射中记录我们的请求。因为在请求时块数据是未知的，Chainlink VRF 确保通知 NFT 和游戏结果的随机性是防篡改和不可预测的。

```
function transferFrom(address from, address to, uint256 tokenId) public override(ERC721) {
    bytes32 requestId =
        requestRandomness(keyHash, fee, uint32(block.number));
    requestIdToTokenId[requestId] = tokenId;
    _transfer(from, to, tokenId);
}
```

最后，我们有一个`fulfillRandomness`方法，在一次传输完成后，由 VRF 链调用。我们将随机数取模 0 到 2 来得到 0 或 1。我们将使用它来切换到第一个或第二个属性(这只猫不会回复到叠加状态)并切换到我们相应的 URI。

```
function fulfillRandomness(bytes32 requestId, uint256 randomNumber) internal override
{
    uint256 _tokenId = requestIdToTokenId[requestId];
    uint256 random2 = (randomNumber % 2);
    EigenValue newEigenVal = EigenValue(random2);
    string memory newUri = IpfsUri[random2];
    tokenIdToEigenValue[_tokenId] = newEigenVal;
    _setTokenURI(_tokenId, newUri);
}
```

就像那样，我们有一个契约，让我们创建动态的 NFT，它在每次传输时都会改变。

## 查看元数据

在本教程中，我们将使用存储在 IPFS 上的外链元数据(因为 OpenSea 目前只读取外链)。如果您想查看元数据，请查看“什么是元数据？”以及我们上一期[动态 NFT 教程](https://blog.chain.link/build-deploy-and-sell-your-own-dynamic-nft/)的“下载 IPFS”部分。“metadata”文件夹中已经有一些回购内的预建元数据文件，这些文件指向 IPFS 上托管的文件。如果您正在制作自己的图像，请随意托管您自己的图像，并更改元数据以指向它们。记得把[智能合约](https://chain.link/education/smart-contracts)里的 URIs 换了就行了。

## 将合同部署到 Rinkeby

现在我们将使用 Hardhat 将合同部署到 Rinkeby testnet，因为这是 OpenSea 目前唯一认可的以太坊测试网。所有部署脚本都在 repo 的 deploy 文件夹中。当发出部署命令时，Hardhat 会自动检查那里。我们需要安装依赖项，然后进行部署

```
yarn install
npx hardhat deploy
```

运行之后，您应该会看到您刚刚部署的契约的地址，以及您可以运行的几个 Hardhat 命令。例如:

```
Compiling 18 files with 0.6.7
Compilation finished successfully
----------------------------------------------------
Deploying dNFT
dNFT deployed to:  0x472fd0039FDD02BcA13a34DaBa788ed1e82bb9A6
Run the following command to fund contract with LINK:
npx hardhat fund-link --contract  0x472fd0039FDD02BcA13a34DaBa788ed1e82bb9A6
Then create a dNFT with the following command:
npx hardhat create-collectible --contract  0x472fd0039FDD02BcA13a34DaBa788ed1e82bb9A6
```

## 创造一个充满活力的 NFT

对于这个版本来说，Hardhat 最有价值的部分之一是它可定制的“任务”。这些可以在“tasks”文件夹中找到，并且都被导入到“hardhat.config.js”文件中。Hardhat 任务总是以关键字“task”开始，并以任务名称和描述作为参数。我们将使用的第一个任务是 create-collectable 任务，它调用我们部署的智能契约上的`create-collectible`函数。要使用 create-collectable 任务，请在终端中运行以下命令(添加您的合同地址):

```
npx hardhat create-collectible --contract INSERT_YOUR_CONTRACT_ADDRESS_HERE
```

恭喜你，你现在有了你的第一个 dNFT！如果您按原样使用提供的代码，您将总是从一只盒子里的猫开始，陷入睡眠和攻击的叠加中。

## 通过 LINK 为您的合同提供资金

LINK 需要向 Chainlink VRF 公司支付服务费。只要我们将足够的链接费用转移到 VRF 合同地址，VRF 就会被呼叫。因此，在我们出售我们的 NFT 之前，这只是一个由上市平台处理的有条件转让，我们需要为我们与 LINK 创建的合同提供资金，否则转让将失败。要为与 [Rinkeby testnet LINK 的合同提供资金，](https://rinkeby.chain.link/)在您的终端中运行以下命令:

```
npx hardhat fund-link --contract INSERT_YOUR_CONTRACT_ADDRESS_HERE
```

## 测试销售您的动态 NFT

要测试出售你的 NFT(它在 Rinkeby testnet 上，所以它不会与 real ETH 一起购买)，请前往[https://testnets.opensea.io/account](https://testnets.opensea.io/account)并使用你用于创建 dNFT 的 MetaMask 帐户登录。点击右上角的账户，进入“我的个人资料”。你应该看到一个盒子的 NFT！请注意，OpenSea 可能需要一个多小时来上传数据。

![Schrodinger's NFT Box](img/b856a392d99e5864050714e6acbc4c03.png)

<figcaption id="caption-attachment-2061" class="wp-caption-text">What’s in the box? You’ll have to transfer it to find out.</figcaption>



如果没有马上看到盒子，也不用担心。你可能需要等待一段时间，让 OpenSea 从 IPFS 加载所有的元数据和图像。一旦你的 NFT 完全显示出来，点击它，你可以点击屏幕右上角的蓝色“出售”按钮，列出你想要的任何条件下的 NFT。

您可能希望给购买您的 NFT 的任何人留下一个免责声明，一旦他们收到它，它可能会改变(在盒子的元数据中已经包含了一个免责声明)！一旦有人购买了 NFT，它将转移到他们，Chainlink VRF 将被调用，特征值+URI 将切换到“攻击猫”或“睡猫”。NFT 转移后，买方可能需要点击 OpenSea 上的“更新元数据”,以便知道寻找新的元数据。更新元数据可能需要一些时间(一个小时以上),因为我们需要等待 Chainlink VRF 的交易被纳入区块链，并等待 OpenSea 刷新前端以反映新的元数据。一旦传输完成，元数据已经更新，您应该看到一个“攻击猫”或“睡觉猫”！下面先睹为快“攻猫”。尝试出售/转让 dNFT，你可能会看到“睡猫”！

![Attack Cat](img/bb62faa77fd75b1a7f36015123540a30.png)

<figcaption id="caption-attachment-2062" class="wp-caption-text">It’s an Attack Cat! This is one of the two images you may see after transferring the dNFT.</figcaption>



## 后续步骤

在本文中，我们学习了如何创建真正动态的 NFT，使用 Hardhat 部署它们，并在 OpenSea 的对等市场上列出它们。这只是 dNFTs 的皮毛。一个很酷的项目是制造在铸造时具有可验证的随机特性，并且在转移时也能动态改变的 NFT！关键是，当谈到新兴的 NFT 生态系统时，仍有许多探索要做，而 VRF 链家是进入这一新领域的有力工具。

如果你在这里学到了一些新东西，想要炫耀你已经建立的东西，或者为一些演示回购开发了一个前端，请确保你在 [Twitter](https://twitter.com/chainlink) 、 [Discord](https://discord.gg/Szt3FYj) 或 [Reddit](https://www.reddit.com/r/Chainlink/) 上分享它，并用#chainlink 标记你的回购。也请停止我们的 [Discord](https://discord.com/invite/aSK4zew) 并分享你创造的任何其他酷 NFT。

一如既往，请务必访问[开发人员文档](https://docs.chain.link/),了解 Chainlink 的各种 oracle 功能。您还可以订阅 [Chainlink 简讯](https://chn.lk/newsletter)，了解 Chainlink 堆栈中的最新信息。

### 关于这个话题的更多信息

*   [构建、部署和销售您自己的动态 NFT](https://blog.chain.link/build-deploy-and-sell-your-own-dynamic-nft/)
*   [如何在 NFT (ERC721)中获取随机数](https://blog.chain.link/random-numbers-nft-erc721/)
*   [如何使用带安全帽的链环](https://blog.chain.link/using-chainlink-with-hardhat/)