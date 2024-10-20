# 使用 Chainlink 价格馈送转换自动售货机以接受加密货币支付

> 原文：<https://blog.chain.link/cryptocurrency-vending-machine/>

*chain link 2021 秋季黑客马拉松于 10 月 22 日拉开帷幕。* [*今天报名。*](https://chain.link/hackathon?utm_medium=referral&utm_source=chainlink-blog&utm_campaign=fall-2021-hackathon&utm_content=convert-a-vending-machine-to-accept-cryptocurrency-payments-using-chainlink-price-feeds)

如何升级自动售货机，使其能够接受加密货币？

对于允许人们以自己选择的货币(包括加密货币)进行交易的自动化现实世界系统，这些外部系统需要能够与区块链对话，并交换对两种环境都有意义的交易逻辑。chain link[Oracle](https://chain.link/education/blockchain-oracles)是这些系统之间的桥梁，旨在将外部输入安全地连接到智能合约。

作为这种现实世界连接的一个很好的例子， [Chainlink 虚拟黑客马拉松奖获得者](https://blog.chain.link/congratulations-to-the-winners-of-the-chainlink-virtual-hackathon-2020/)之一，开发者 Ted Nivan，使用 Chainlink 外部适配器将模拟水果自动售货机连接到 Chainlink ETH/USD 价格馈送 oracle，以便它可以接受 ETH 作为购买单份水果的货币。在这篇文章中，Ted 解释了他是如何建造它的。

* * *

*由* [到*泰德·尼文*到](https://www.linkedin.com/in/ted-nivan-027680b2/)

水果市场是一个开放的概念证明，旨在试验一种使用加密货币进行自动售货机购买的新方法。使用水果市场，用户将能够在移动电话钱包上使用区块链技术进行自动售货机购买，而无需收银员。具体来说，本教程将通过参考 [Chainlink ETH/USD 价格馈送](https://feeds.chain.link/eth-usd)以公平的市场价格为产品定价，向开发人员展示将自动售货机转换为使用 ETH 作为货币所需的步骤。

您将学到的内容:

1.  如何集成 Chainlink ETH/USD 价格馈送 oracle
2.  如何将硬件设备连接到网络

# 开发人员先决条件

这个 dApp 需要软件和硬件组件。

软件:

1.  [Infura](https://infura.io/) :用于连接以太坊网络。作为开发者，你需要一个 Infura 密钥。
2.  [Web3JS](https://web3js.readthedocs.io/en/v1.3.0/) :前端用于与以太坊网络交互。
3.  [WebUSB](https://web.dev/usb/) :用于通过 web 与硬件设备对话。
4.  [Arduino IDE](https://www.arduino.cc/en/software) :用于刷新设备固件。

硬件:

1.  需要一台服务器或笔记本电脑作为主机。
2.  [Arduino Nano 33 IoT](https://store.arduino.cc/usa/nano-33-iot) :用作模拟自动售货机的硬件设备。Arduino 板是硬件开发板的流行选择，因为它们易于使用和编程。

# 技术概述

本教程将引导开发者完成从[到 GitHub repo](https://github.com/TedNIVAN/fruity-market) 的步骤，你可以在开始之前熟悉一下。为 Chainlink 虚拟黑客马拉松提交的视频也是了解组件如何协同工作的好地方。

[![](img/aacaf8bf57c1c442691460e60fd92fb5.png)](https://www.youtube.com/watch?v=hlyVUyzjXPQ&width=1000&height=640) 



![Fruity Market Proof of Concept System Logic Diagram](img/7d591a701aeb776853c55a0a3d3feac7.png)

<figcaption id="caption-attachment-1437" class="wp-caption-text">果味市场概念验证系统逻辑图</figcaption>





在左侧，我们有一个运行在以太坊上的应用程序，它使用 Chainlink ETH/USD 价格提要。我们将使用这个价格提要将水果的美元价格转换成乙醚(ETH)。一旦支付成功，dApp 就会从主机(电脑)向设备(Arduino 板)发送信号，让水果送货上门。假设我们没有物理自动售货机，我们将通过打开 LED 来确认水果交付来模拟这种行为。

# 设置项目

在这里，我们将了解如何在本地运行应用程序。

1.  克隆水果市场存储库。

```
>git clone https://github.com/TedNIVAN/fruity-market.git
```

2.初始化项目。

```
cd fruity-market
npm i
```

3.在 *src/中设置您的 [Infura API 密钥](https://infura.io/)。环境样本*

4.重命名 *src/。env_sample* 到 *src/。环境*

5.构建项目。

```
npm run dev
```

应用程序应该运行在:[*http://localhost:1234*](http://localhost:1234/)

## 刷新 Arduino 固件

一旦我们运行了应用程序，下一步就是[安装 Arduino IDE](https://www.arduino.cc/en/software) ，然后刷新 [Arduino](https://www.arduino.cc/en/Guide/ArduinoUno) 固件。必须这样做才能实现设备和应用程序之间的通信，并解释传输的数据。

此步骤[所需的 Arduino 固件可在此处找到。](https://github.com/TedNIVAN/fruity-market/tree/master/arduino)

该代码执行以下任务:

1.  它只授权设备通过 HTTPS 与应用程序页面*tednivan.github.io/fruity-market/app*通信。注意，如果在本地运行，通信也可以工作(http://localhost:1234/)。
2.  它建立了串行通信。
3.  它等待字符 *H* 触发 LED。
    代码运行在 Arduino NANO 33 物联网上，但受大多数 Arduino 主板支持。[点击](https://github.com/webusb/arduino#compatible-hardware)查看受支持电路板的完整列表。

```
#include <WebUSB.h>

/**
 * Creating an instance of WebUSBSerial will add an additional USB interface to
 * the device that is marked as vendor-specific (rather than USB CDC-ACM) and
 * is therefore accessible to the browser.
 *
 * The URL here provides a hint to the browser about what page the user should
 * navigate to to interact with the device.
 */
WebUSB WebUSBSerial(1 /* https:// */, "tednivan.github.io/fruity-market/app");

#define Serial WebUSBSerial

const int ledPin = 13;

void setup() {
  while (!Serial) {
    ;
  }
  Serial.begin(9600);
  Serial.write("Sketch begins.\r\n> ");
  Serial.flush();
  pinMode(ledPin, OUTPUT);
}

void loop() {
  if (Serial && Serial.available()) {
    int byte = Serial.read();
    Serial.write(byte);
    if (byte == 'H') {
      Serial.write("\r\nTurning LED on.");
      digitalWrite(ledPin, HIGH);
      delay(2000);
      Serial.write("\r\nTurning LED off.");
      digitalWrite(ledPin, LOW);
      delay(2000);
    } 

    Serial.write("\r\n> ");
    Serial.flush();
  }
}
```

刷新固件需要以下步骤:

1.  用 USB 线将 Arduino 连接到您的 PC 或任何用于主机的设备。
2.  打开 Arduino 软件(IDE)。
3.  选择相应的端口和板。
4.  打开从项目的 GitHub 库中获取的 [fruity-market.ino](https://github.com/TedNIVAN/fruity-market/blob/master/arduino/fruity-market.ino) 草图。
5.  上传草图。如果你不熟悉 Arduino，请查看本指南[。](https://www.arduino.cc/en/Guide/ArduinoUno)

## 进入智能合同

该项目的下一部分是[智能合约](https://github.com/TedNIVAN/fruity-market/blob/master/contract/FruityMarket.sol)。智能合约负责获取以太坊价格馈送( **getLatestPrice** 函数)，并在收到付款时触发事件(**收到**事件)。然后在[客户端](https://github.com/TedNIVAN/fruity-market/blob/master/src/js/web3entry.js)完成支付处理。

```
import "https://github.com/smartcontractkit/chainlink/blob/master/evm-contracts/src/v0.6/interfaces/AggregatorV3Interface.sol";

contract FruityMarket {

    AggregatorV3Interface internal priceFeed;

    /**
     * Network: Kovan
     * Aggregator: ETH/USD
     * Address: 0x9326BFA02ADD2366b30bacB125260Af641031331
     */
    constructor() public {
        priceFeed = AggregatorV3Interface(0x9326BFA02ADD2366b30bacB125260Af641031331);
    }

    /**
     * Sends event on receive
     */
    event Received(address, uint);

    receive() external payable {
        emit Received(msg.sender, msg.value);
    }

    /**
     * Returns the latest price
     */
    function getLatestPrice() public view returns (int) {
        (
            uint80 roundID, 
            int price,
            uint startedAt,
            uint timeStamp,
            uint80 answeredInRound
        ) = priceFeed.latestRoundData();
        // If the round is not complete yet, timestamp is 0
        require(timeStamp > 0, "Round not complete");
        return price;
    }
}
```

这个智能契约必须部署到以太网，然后生成的契约的地址应该存储在前端 web 应用程序使用的 [web3entry.js](https://github.com/TedNIVAN/fruity-market/blob/master/src/js/web3entry.js) 文件中的 addr 参数中。这个 JavaScript 文件创建了前端和我们正在部署的链上契约之间的连接。你可以通过 [Remix](https://remix.ethereum.org/#version=soljson-v0.6.12+commit.27d51765.js&optimize=false&evmVersion=null&gist=46ed95d698a468d27083f9fdef9a3574&runs=200) 轻松部署智能合约。

现在我们可以测试最终完成的水果市场概念验证。

## 测试最终确定的水果市场概念验证

如果您在本地部署了应用程序，请打开本地部署的应用程序。否则，你可以使用[我们已经部署的版本](https://tednivan.github.io/fruity-market/)。



![The Fruity Market App Launch Screen](img/fe3e55e55176042dfb12b35978ac61d1.png)

<figcaption id="caption-attachment-1444" class="wp-caption-text">果味市场 App 启动画面</figcaption>





首先，点击“启动应用程序”按钮。



![The simulated fruit vending machine.](img/d0480631fb10e060c7b64a03f4bdba66.png)

<figcaption id="caption-attachment-1443" class="wp-caption-text">模拟水果自动售货机。</figcaption>





单击“连接设备”按钮连接到 Arduino 板。



![The finder will locate the relevant available hardware.](img/85ff2fc200676eaf4e08e8f8920c2757.png)

<figcaption id="caption-attachment-1442" class="wp-caption-text">查找器将定位相关的可用硬件。</figcaption>





选择“Arduino NANO 33 IoT”板，然后按“连接”按钮。



![The Fruity Market launch screen will indicate whether the hardware has been connected.](img/e9ad4e7217f0920887d56b6d0fcaf9ab.png)

<figcaption id="caption-attachment-1441" class="wp-caption-text">水果市场启动画面会显示硬件是否已连接。</figcaption>





如果成功建立连接，右上角的绿色按钮将变为“断开设备连接”。如果是这样，你现在可以挑选一种水果购买。



![A payment screen using the Ethereum Kovan test network.](img/6970a1c741927054d81d0c3510fd9ab3.png)

<figcaption id="caption-attachment-1440" class="wp-caption-text">一个使用以太坊 Kovan 测试网络的支付屏幕。</figcaption>





通过扫描二维码并输入所需的 ETH 金额(这将取决于当前的 ETH/USD 价格)，使用 Kovan 网络使用任何以太坊钱包进行支付。



![Successful payment confirmation screen.](img/6c09d8433237ebef25a1929f75cac020.png)

<figcaption id="caption-attachment-1439" class="wp-caption-text">成功支付确认画面。</figcaption>





在成功支付的情况下，将出现此页面。Arduino 板上的 LED 也将打开一小段时间，以模拟水果递送。



![A failed transaction screen.](img/f7f0f8e41a9549f5bd83fc8f74efd74c.png)

<figcaption id="caption-attachment-1438" class="wp-caption-text">一个失败的交易画面。</figcaption>





如果顾客发送的金额低于水果的价格，付款将被拒绝。

## 水果市场的下一步是什么

Fruity Market 的下一步是改进智能合同逻辑，以便在用户支付超过所需金额的情况下处理支付。其他后续步骤包括集成硬件，使用带有触摸屏的 Raspberry Pi 4 复制更真实的自动售货机用户体验。

随着硬件和智能合约逻辑与当前的企业自动售货机功能越来越紧密地结合在一起，增加额外的支付选项，如 20 stablecoins(如戴或)支持的 Chainlink Price Feeds 将增强体验，并突出加密货币作为支付系统的可互操作性。

* * *

## 开始建设与链接价格饲料

如果你是一名致力于将 Arduino 或其他[硬件](https://blog.chain.link/rfid-blockchain-integration-with-chainlink-external-adapters/)连接到区块链的开发人员，加入充满活力的 Chainlink 社区寻求支持和协作。点击[这里](https://chainlink.typeform.com/to/gEwrPO)或者访问[开发者文档](https://docs.chain.link/)，你也可以订阅 [Chainlink 时事通讯](https://chn.lk/newsletter)来了解 Chainlink 栈的最新消息。

如果你在这里学到了一些新东西，想要炫耀你已经建立的东西，或者为一些演示回购开发了一个前端，请确保你在 [Twitter](https://twitter.com/chainlink) 、 [Discord](https://discord.gg/Szt3FYj) 或 [Reddit](https://www.reddit.com/r/Chainlink/) 上分享它，并用#chainlink 标记你的回购。

*[chain link 2021 秋季黑客马拉松](https://chain.link/hackathon) 于 2021 年 10 月 22 日开赛。无论您是开发人员、创作人员、艺术家、区块链专家，还是该领域的新手，这个黑客马拉松都是启动您的智能合同开发之旅并向行业领先的导师学习的最佳场所。立即锁定您的席位，争夺超过$ 300，000 的奖金。T9】*

[Sign up today](https://chain.link/hackathon?utm_medium=referral&utm_source=chainlink-blog&utm_campaign=fall-2021-hackathon&utm_content=convert-a-vending-machine-to-accept-cryptocurrency-payments-using-chainlink-price-feeds)