# Cozy Reef 如何使用多个 Chainlink 服务来支持其高级游戏 dApp

> 原文：<https://blog.chain.link/using-multiple-chainlink-services-for-blockchain-gaming/>

Chainlink 服务使分散的游戏生态系统能够避开区块链游戏面临的一些常见陷阱，并为玩家创造更深入、更有益的体验。对于他们的 Chainlink Hackathon 2021 项目，Cozy Reef Labs 将多个 Chainlink 服务集成到他们的第一款游戏 Slingshot Sailers 中，使用 [Chainlink 自动化](https://chain.link/automation) 进行分散式游戏状态管理，[chain link VRF](https://chain.link/chainlink-vrf)进行可证明的随机性，以及 [Chainlink 外部适配器](https://docs.chain.link/docs/external-adapters/) 利用不同的区块链进行结算和游戏层。在这个技术演练中，深入 Cozy Reef 构建的幕后，了解他们的团队如何利用这些不同的 Chainlink 服务来构建一个高级游戏 dApp。

由 [惬意礁实验室](https://twitter.com/TheCozyReef)

## 欢迎来到舒适礁

![Welcome to Cozy Reef](img/978ee5c3846366aad21b1cd97ef1a751.png)

Cozy Reef Labs 成立的目的是利用区块链科技公司的独特能力，创造深度的、基于社区的游戏体验。

团队的每个成员都有丰富的视频游戏行业工作经验，他们希望将有趣、有意义的玩家体验放在首位。为了做好这一点，该团队设定了一个雄心勃勃的目标:我们将建立一个游戏生态系统，玩家可以随着时间的推移回来玩，而不是建立一个单一的游戏。这些游戏容易学习但很难掌握，适合玩家想要探索和体验的更大的世界，并且具有竞争力，值得玩家花费时间。

我们意识到 Chainlink 技术可以帮助我们实现这些目标，甚至更多。我们将能够构建完全的在线游戏，为玩家提供前所未有的透明度，同时营造一个具有游戏赚钱精神的竞争性游戏环境。通过将公共区块链与 Chainlink 服务的生态系统相结合，我们能够建立一个分散的平台，将重点放在游戏体验上。

舒适礁将推出一系列淘汰赛，幸存者将被邀请作为舒适礁黑仔参与平台的未来发展方向。每款游戏都可以在一个更广阔的生态系统中重新播放，玩家可以在这个生态系统中进行游戏、比赛并获得奖励。

## 链环自动化驱动核心游戏循环

![Slingshot Sailors](img/c0248d84d0b25c2f19d728e30c1d5b3c.png)

《弹弓水手》是《舒适礁》第一季的第一场淘汰赛。玩家必须从五个不同属性的弹弓中选择一个，让自己远离追逐舒适的暗礁杀手。吊索上的玩家越多，它的距离奖励和射击机会就越高。但这并不都是阳光和大乘数——吊索中的球员数量也增加了哑火的机会，导致距离惩罚。为了在整个游戏中成功躲避舒适的暗礁杀手，玩家必须在每一轮中平衡风险和回报，并对其他玩家的决定做出反应。核心游戏循环经历以下阶段:  

*   运动——玩家可以选择跳上哪个吊索。弹弓上玩家的数量会改变弹弓开火或逆火的几率，并影响距离乘数。
*   锁定——玩家不再能够选择投石器。这段时间是为了让链在块确认上达到终结，以防止 VRF 调用和块重组的提前运行。
*   VRF _ 请求——向 VRF 链环公司请求一个随机数，该随机数决定每个吊索的结果。
*   VRF _ 已接收—随机数已成功处理，并计算了舍入。我们创建这个附加状态是因为舍入计算超过了 VRF 调用中允许的最大 gas([200，000](https://docs.chain.link/docs/get-a-random-number/) gas)。注意:开发人员可以在将 dApp 注册到 Automation 时配置最大 gas。

![Slingshot Sailors screenshot 2](img/60a2c00013c29319e64f6be82633cd72.png)

智能合约本身不足以在基于时间的环境中充当游戏运行者，因为它需要外部调用来促进阶段转换。Chainlink Automation 允许我们以分散的方式检查和触发阶段转换。我们通过连接“check maintenance”函数来检查我们是否需要将游戏移动到下一阶段，这主要是由“block.timestamp”驱动的:

```
function checkUpkeep(bytes calldata) external view override returns (bool, bytes memory) {
    bytes memory empty;
    return (canTick(), empty);
  }

function canTick() public view returns (bool) {
    return
      state.game.phase != Phase.NONE &&
      state.game.phase != Phase.END &&
      block.timestamp >= state.game.phaseScheduledEnd;
  }
```

当“check maintenance”函数返回 true 时，自动程序调用“perform maintenance”将游戏转换到下一阶段:

```
function performUpkeep(bytes calldata) external override {
    tickState(false);
  }

function tickState(bool force) public {
    if (!(force || canTick())) return;

    if (state.game.phase == Phase.LOCKOUT) {
      require(LINK.balanceOf(address(this)) >= vrfState.fee, "Not enough LINK");
      requestRandomness(vrfState.keyHash, vrfState.fee);
    }

    if (state.game.phase == Phase.VRF_RECEIVED) {
      sweepLanes(state.game.random);
      state.game.sweep++;
      state.game.lastRandom = state.game.random;
    }

    Phase previous = state.game.phase;
    state.gotoNextState();
    emit StateUpdated(previous, state.game.phase);
    return;
  }
```

在“tickState”功能中，根据游戏阶段发生不同的动作。例如，如果该阶段当前处于锁定阶段，则发出 VRF 请求，并且状态将变为 VRF _ 已请求。契约发出一个“状态更新”事件，玩家的浏览器通过调用视图函数来响应更新后的契约状态。为了节省汽油和成本，游戏契约只存储原始游戏事件(发射弹弓、玩家移动历史等)。).运行游戏的浏览器然后从游戏契约中获取这些事件，并懒洋洋地计算玩家在他们的屏幕上看到的游戏状态(这个过程在 [白皮书](https://cozyreef.io/docs/Cozy%20Reef%20Season%20One%20Whitepaper.pdf) 中有更全面的描述)。)弹弓水手的完整游戏合约将在游戏第一个实例上线后不久开源。我们鼓励社区为他们自己的游戏项目参考这个合同！

## 链环 VRF 启用动态玩家互动

![Cozy Reef Chainlink Keepers and VRF diagram](img/adbdef82e4196f928204040ac89cb674.png)

玩家必须围绕风险管理做出决定，并选择他们认为相对于风险(逆火机会，距离惩罚)有最佳回报(射击机会，距离乘数)的弹弓。根据概率和其他玩家的行为做出决定是弹弓水手兴奋的核心。Chainlink VRF 允许我们以分散的方式生成可证明的随机数，以驱动每一轮的独特结果。通过一个 VRF 呼叫，我们能够确定五个弹弓中的每一个是否发射，逆火，或者什么也不做。

如前所述，当游戏阶段从“锁定”过渡到“VRF _ 请求”时，调用“请求随机性”函数，传入 keyHash 值和费用。VRF 将通过“fulfillnommandations”回调函数生成并传回一个随机数，如下所示:

```
*function fulfillRandomness(bytes32, uint256 randomness) internal override {*
 *state.game.random = randomness;*
 *state.gotoNextPhase();*
*  }**function gotoNextPhase(State storage self) public {*
 *…*
 *} else if (self.game.phase == Phase.VRF_REQUESTED) {*
 *self.game.phase = Phase.VRF_RECEIVED;*
 *self.game.phaseScheduledEnd = uint48(block.timestamp);*
 *}*
 *…*
 *self.game.phaseStart = uint48(block.timestamp);*
*  }**function tickState(bool force) public {*
 *…*
 *if (state.game.phase == Phase.VRF_RECEIVED) {*
 *sweepLanes(state.game.random);*
 *state.game.sweep++;*
 *state.game.lastRandom = state.game.random;*
*    }*

 *Phase previous = state.game.phase;*
 *state.gotoNextState();*
 *emit StateUpdated(previous, state.game.phase);*
 *return;*
*  }*
```

回调函数设置随机数并触发下一个相位变化，链节自动化节点更新该相位变化，最终调用“tickState”函数并通过“sweepLanes”求解该轮

## Chainlink 外部适配器支持多链生态系统

![Cozy Reef Chainlink External Adapters diagram](img/4b79da5d11f06e5c7ad4de757b4cfc92.png)

我们开发 Cozy Reef 的核心原则之一是可访问性:玩家不应该支付过高的价格来玩我们的在线游戏。通过一些初步的成本分析(参考我们的 [白皮书](https://cozyreef.io/docs/Cozy%20Reef%20Season%20One%20Whitepaper.pdf) )，我们估计在 Polygon 等侧链上玩弹弓水手比在以太坊 mainnet 上便宜 7500 倍。然而，我们认识到以太坊主网仍然是理想的区块链定居点。

我们的解决方案是在以太坊主网上制作创世纪 NFT，在 Polygon 上运行游戏。为了验证所有权并允许玩家加入游戏，我们利用 [视图功能外部适配器](https://github.com/smartcontractkit/external-adapters-js/tree/develop/packages/sources/view-function) 构建了一个[保留证明](https://chain.link/proof-of-reserve)服务。在以太坊主网上拥有舒适礁 NFT 的玩家调用多边形上的验证器，该验证器验证令牌所有权并允许玩家进入游戏实例。采用这种方法可以实现多链功能，同时将玩家体验放在首位:  

*   所有的契约调用都在边链上进行，这比玩家在以太坊主网上通过契约调用进行桥接要便宜得多。
*   短暂的游戏实例和对每个游戏实例的验证消除了跨链取消同步所有权的主要挑战。
*   与 NFT 桥相比，使用准备金证明模型消除了通过托管账户管理非金融交易的安全风险。
*   侧链代币的成本很低，Cozy Reef Labs 可以持续利用收入向玩家空投代币，以抵消成本和抽象代币桥接的复杂性。

在 [GitHub](https://github.com/CozyReef/prototype-chainlink-proof-of-reserves) 上可以找到 NFT 储备证明的原型以及技术故障。未来的发展将包括进一步分散这一组成部分的权力，该协议与一个链环唐。

## 未来的发展

舒适礁的第一个重要里程碑是发布第一季的在线淘汰赛，并邀请幸存者加入舒适礁杀手。随着 Cozy Reef 成长为一个更广泛的游戏平台，我们将需要建立更多的基础设施。我们很高兴能够继续利用 Chainlink Automation 的功能来完全分散整个生态系统。

**游戏日程**——弹弓水手将在每个实例的基础上运行，每个游戏周期都有一个设定的开始和结束时间。我们打算在循环的基础上重新运行这个和未来的游戏，让玩家继续竞争并获得奖励。链式自动化是以可预测和可靠的方式分散游戏调度的一个很好的候选。

**赛后处理**——玩家将根据他们在每场比赛中的表现赢得代币。Chainlink Automation 是大规模分散和管理游戏后处理(如奖励分配)的绝佳候选。

**奖学金和赌注管理**—我们希望为舒适珊瑚礁的所有者创造机会，让他们将自己的代币作为赌注，并参与链上支持的奖学金项目。Chainlink Automation 解放了我们构建综合系统来管理这些计划和分配奖励的能力。

![Cozy Reef artwork](img/87efb2241d72acbd1b4ac6bcbf11acbe.png)

随着《舒适礁石》第一季即将开播，该团队希望拓展区块链游戏空间的可能性。Chainlink 技术使我们能够以一种透明、引人入胜且更广泛的游戏社区可访问的方式将体验完全带到链上。

## 了解更多信息

如果您是一名开发人员，并且希望将您的智能合约连接到底层区块链之外的现有数据和基础设施，请在此处联系[](https://chainlink.typeform.com/to/gEwrPO)或访问 [开发人员文档](https://docs.chain.link/) 。