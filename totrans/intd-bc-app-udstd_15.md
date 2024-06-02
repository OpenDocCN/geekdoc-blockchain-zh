© 作者授权 APress Media, LLC 独家许可，属于 Springer Nature 2022 约瑟夫·T·乔治介绍区块链应用[`doi.org/10.1007/978-1-4842-7480-4_15`](https://doi.org/10.1007/978-1-4842-7480-4_15)

# 15. *Platoon*项目

约瑟夫·塔奇尔·乔治^(1  )（1）意大利罗马

本章解释了如何基于名为*Platoon*的游戏开发一个物联网系统。

*Platoon*是由 Ocean Software 于 1987-1988 年发布的一款视频游戏，首先针对 8 位家用电脑，然后针对 16 位电脑和任天堂娱乐系统。灵感来自战争电影*Platoon*，由不同的游戏机制组成不同关卡，既有第三人称又有第一人称。1988 年，Sunsoft 还开发了一款街机转换版，称为*Vs. Platoon*，基于任天堂授权的 NES 和任天堂 Vs.系列系统。据维基百科介绍，游戏有几个阶段。^(1)

游戏分为四个关卡¹。

+   *丛林与村庄：* “通过迷宫般的水平滚动环境，由垂直通道连接，具有二维移动和第三人称侧视”。路径上布满陷阱和越南人民军。玩家一次只能控制一名士兵，但可以随时用其他士兵替换，例如为了避免将已受伤的人置于危险之中。他们可以跳跃和蹲下，射击和投掷手榴弹，弹药有限。在最后一部分，探索村庄的小屋，这些小屋会暂时变透明，以寻找继续的必要物品。

+   *游击队：* 游戏变成了一款第一人称射击游戏，半个屏幕被迷你地图占据。当你遇到游击队时，他们也会从淹没隧道的水中出现，移动停止，你转向查看镜头。当你进入一个房间时，观景镜变成一个用于检查物品的指针；通过这种方式有必要继续的元素——补给和陷阱。

+   *掩体：* 这是一个固定的屏幕视角射击游戏；画面很暗，只有枪声的闪光能被敌人注意到，除非玩家暂时用信号弹照亮场景。弹药和信号弹数量有限。

+   *巴恩斯丛林和掩体：* 一个固定的 2.5D 第三人称屏幕迷宫，从屏幕底部到顶部穿过，避开障碍物并借助指南针射击敌人。弹药和总时间有限。最终老板是巴恩斯，要用手榴弹击中他。

五名队员中的每一名可以承受四次打击才会死亡。还有一个总体士气表，当无辜平民受伤或被击中时会减少，通过收集食物和药品来充电。如果士气降至零，以及如果所有队员都死亡，则失败。

在本章中，您将学习如何借助 Kilobots 的移动来实现这个游戏。

## 15.1 游戏环境

1.  1.

    AE-1：Kilobots 将在白板上操作。

1.  2.

    AE-2：一个障碍物将位于白板的中间。

### 15.1.1 SoS 组织

1.  1.

    ASoS-1：SoS 由 N 个 Kilobots 组成。

1.  2.

    ASoS-2：SoS 还由一个控制器组成，该控制器将程序加载到 Kilobots 的内存中。

1.  3.

    ASoS-3：SoS 编队在组成 SoS 的 Kilobots 之间进行。

1.  4.

    ASoS-4：当 SoS 启动时，Kilobots 被放置在一条直线上，距离为 D 厘米。

1.  5.

    ASoS-5：当 SoS 运行时，Kilobots 之间的距离保持在大约 D 厘米。

1.  6.

    ASoS-6：在执行之前确定领导者。

1.  7.

    ASoS-7：所有 Kilobots 都知道领导者的 ID。

### 15.1.2 CS 级别

1.  1.

    CCS-1：每个 Kilobot 都有一个 RUMI 来交换消息。

1.  2.

    每个 Kilobot 都有一个 RUMI 与控制器进行通信。

1.  3.

    控制器有一个 RUMI 与 Kilobots 进行通信。

1.  4.

    每个 Kilobot 都有一个 RUMI 来估算距离。

### 15.1.3 SOS 级别

1.  1.

    CSoS-1：每个 Kilobot 都将使用其 RUMI 来交换有关方向的信息，当它加入编队时以及当它离开编队时。

1.  2.

    CSoS-2：当 SoS 开始时，每个 Kilobot 通过发送消息通知相邻的跟随者它是领袖。

1.  3.

    CSoS-3：每个 Kilobot 都有一个 RUPI 来估算发送方和接收方之间的距离，使用信号功率。

### 15.1.4 观点出现

1.  1.

    E-1：多个 Kilobot 的互动导致了一个独特的车队。

### 15.1.5 观点动态性

1.  1.

    D-1：车队允许任何 Kilobot 成为成员。

1.  2.

    D-2：车队由至少两个 Kilobot 组成。

1.  3.

    D-3：只有在尾部允许将 Kilobot 引入车队。

1.  4.

    D-4：车队只允许最后一个 Kilobot 离开。

### 15.1.6 观点时间

1.  1.

    T-1：Kilobot 将根据本地时钟 T-2 测量时间。与时间有关的事件是通过消息交换触发的。

1.  2.

    T-3：当 Kilobot 启动时，它将为 Mms 准备电机。

## 15.2 电子物理系统

Kilobots 将帮助您将概念付诸实践。Kilobots 用于执行车队移动。Kilobot 群体是一个一万个机器人（1024）的群体，可用于开发和测试高增长群体的集体行为。

每个机器人都具有独立群体机器人的基本功能（可配置控制器、基本移动和本地通信），但它们采用廉价零件制造，主要由自动系统建造。

此外，系统的架构使得单个操作员可以简单灵活地控制大型 Kilobot 集合，包括“无需手动”编码、开启和为所有机器人充电。该项目利用 Kilobot 群体来研究集体“人工”智能（例如，同步、集体运输和身份），并测试将最小个体能力与群体行为相关的新理念。

该项目希望通过混合理论和实验方法，对稳健性、可伸缩性、自组织性和利用受限个体的新型集合体进行新的算法洞察。

## 15.3 Kilobot 源代码

#include <kilombo.h>#include "platoon.h"#include <math.h>#ifdef SIMULATOR#include <stdio.h> // for printf#include <stdlib.h>#else#include <avr/io.h>  // for microcontroller register defs#endif#define RED RGB(3,0,0)#define GREEN RGB(0,3,0)#define BLUE RGB(0,0,3)#define WHITE RGB(3,3,3)#define STRAIGHT 1#define LEFT 2#define JOIN 3#define QUIT 4#define OK 5#define LEAVE 6#define SPEED_DOWN 7#define TURN_LEFT_DELAY 126#define GO_STRAIGHT_DELAY 700#define JOIN_DELAY 150#define FOLLOW_DELAY 220#define STANDARD_DISTANCE 80#define NORMAL_SPEED 70#define CAN_LEAVE 2#define CAN_JOIN 3#define LEAVE_TIME 2500#define END_TIME 20000REGISTER_USERDATA(USERDATA)void message_rx(message_t *m, distance_measurement_t *d) {    mydata->new_message = 1;    mydata->received_msg=*m;    mydata->dist = *d;}void setup_message(uint8_t data) {      mydata->transmit_msg.type = NORMAL;      mydata->transmit_msg.data[0] = kilo_uid & 0xff; //low byte of ID, currently not really used for anything      mydata->transmit_msg.data[1] = data;      mydata->transmit_msg.crc = message_crc(&mydata->transmit_msg);}message_t *message_tx() {  return &mydata->transmit_msg;}void setupUserData(){    mydata->cur_distance = 0;      mydata->new_message = 0;      mydata->turning = 0;    mydata->joining = 0;    mydata->following = 0;      mydata->follower_id = kilo_uid+1;}void setup() {      setupUserData();      if (kilo_uid == 0)            set_color(WHITE); // 领航机器人的颜色为白色      else if(kilo_uid == CAN_JOIN)      {            mydata->my_leader = 255;            set_color(BLUE); // 加入机器人的颜色为蓝色      }      else      {            set_color(RED); // 移动机器人的颜色为红色            mydata->my_leader = kilo_uid-1;      }}// 领航机器人代码/*********************************************************************/int checkDistance() {      if (mydata->new_message && mydata->received_msg.data[0] == mydata->follower_id) {            if (estimate_distance(&mydata->dist) > STANDARD_DISTANCE+3)                  return SPEED_DOWN;      }      return -1;}void speedCorrection(int distance){    if (distance == SPEED_DOWN)      set_motors(0,0);    else      set_motors(kilo_turn_left, kilo_turn_right);}void leader() {      mydata->myClock = kilo_ticks%(GO_STRAIGHT_DELAY+TURN_LEFT_DELAY);      if (mydata->myClock < GO_STRAIGHT_DELAY) {            speedCorrection(checkDistance());            setup_message(STRAIGHT);      } else {            setup_message(LEFT);            set_motors(kilo_turn_left, 0);      }}/*********************************************************************/// 跟随机器人代码/*********************************************************************/int handleMessage() {      if (mydata->new_message && mydata->received_msg.data[0] == mydata->my_leader) {            return mydata->received_msg.data[1];      }      return 0;}int handleOther() {    if(mydata->new_message && mydata->received_msg.data[0] != mydata->my_leader) {        return mydata->received_msg.data[1];    }    return 0;}int goStraight() {    return (kilo_ticks - mydata->message_timestamp < 346);}int goLeft() {    int timestamp_isok = (kilo_ticks - mydata->message_timestamp >= 346);    int passed_delay = kilo_ticks - mydata->message_timestamp < 346 +TURN_LEFT_DELAY;    return (timestamp_isok && passed_delay);}int handleTurnLeft() {      if (goStraight

排队源代码

{"bot_states": [{"ID": 0, "direction": 9.3774271885570943, "state": {}, "x_position": 263.28312031961627, "y_position": -153.00242098913}, {"ID": 1, "direction": 9.2974330575267956, "state": {}, "x_position": 272.14245496760822, "y_position": -78.255749422064071}, {"ID": 2, "direction": 4.7057699363876493, "state": {}, "x_position": -324.34376414595039, "y_position": -186.66926101606919}, {"ID": 3, "direction": 2.785910791660513, "state": {}, "x_position": 266.71626481529483, "y_position": -17.907987160522111}], "ticks": 4830}Listing 15-2

终态.json

{"botName" : "Join Tail", "randSeed" : 1, "nBots" : 4, "formation": "rline", "timeStep" : 0.0416666, "__note" : "0.04166 是 24 FPS，与电影帧速率相匹配", "__timeStep" : 0.03225, "simulationTime" : 0, "commsRadius" : 100, "showComms" : 1, "showCommsRadius" : 0, "distributePercent" : 0.8, "displayWidth" : 640, "displayHeight" : 424, "displayWidthPercent" : 80, "displayHeightPercent" : 80, "displayScale" : 1, "showHist" : 1, "histLength": 4000, "storeHistory": 1, "imageName" : "./movie4/f%04d.bmp", "saveVideo" : 0, "saveVideoN" : 1, "stepsPerFrame" : 1, "finalImage" : null, "stateFileName" : "simstates.json", "stateFileSteps" : 0, "colorscheme" : "bright", "speed": 7, "turnRate" : 22, "GUI" : 1 , "msgSuccessRate" : 0.8, "distanceNoise" : 2}Listing 15-3

kilombo json

{  "bot_states": [      {      "ID": 0,      "direction": 1.57,      "state": {},      "x_position": 100.0,      "y_position": 0.0    },    {      "ID": 1,      "direction": 1.57,      "state": {},      "x_position": 20.0,      "y_position": 0.0    },    {      "ID": 2,      "direction": 1.57,      "state": {},      "x_position": -60.0,      "y_position": 0.0    },    {      "ID": 3,      "direction": 1.57,      "state": {},      "x_position": -210.0,      "y_position": 0.0    }  ],  "ticks": 7292}列表 15-4

start-positions.json

#ifndef M_PI#define M_PI 3.141592653589793238462643383279502884197169399375105820974944#endif// 声明运动变量类型 typedef enum {    STOP,    FORWARD,    LEFT,    RIGHT} motion_t;// 声明状态变量类型 typedef enum {    ORBIT_TOOCLOSE,    ORBIT_NORMAL,} orbit_state_t;// 声明变量 stypedef struct {      uint8_t cur_distance;      uint8_t new_message;      distance_measurement_t dist;      message_t received_msg;      message_t transmit_msg;      uint8_t my_leader;    uint8_t joining;    uint8_t following;      int message_timestamp;      int turning;      int myClock;      int turn_timestamp;      int follower_id;    int follow_timestamp;} USERDATA;列表 15-5

platoon.h

{    "botName" : "Join Tail",    "randSeed" : 1,    "nBots" : 4,    "formation": "rline",    "timeStep" : 0.0416666,    "__note" : "0.04166 是 24 FPS，与电影帧速率匹配",    "__timeStep" : 0.03225,    "simulationTime" : 0,    "commsRadius" : 100,    "showComms" : 1,    "showCommsRadius" : 0,    "distributePercent" : 0.8,    "displayWidth"  : 640,    "displayHeight" : 424,    "displayWidthPercent" : 80,    "displayHeightPercent" : 80,    "displayScale"  : 1,    "showHist" : 1,    "histLength": 4000,    "storeHistory": 1,    "imageName" : "./movie4/f%04d.bmp",    "saveVideo" :  0,    "saveVideoN" : 1,    "stepsPerFrame" : 1,    "finalImage" : null,    "stateFileName" : "simstates.json",    "stateFileSteps" : 0,    "colorscheme" : "bright",    "speed": 7,    "turnRate" : 22,    "GUI"  : 1 ,    "msgSuccessRate" : 0.8,    "distanceNoise" : 2}Listing 15-6

kilombo.json

Kilobots 能够进行合作运输，这意味着它们可以通过集体努力移动一个巨大的物体。Kilobot 集体还可以使用 S-DASH 来塑造各种形状并在形状变形时进行修复。它们还可以根据类型变化其大小。

他们在一个程序中模仿昆虫，从一个静态 Kilobot“家”站点启动，并在区域内寻找“食物”，即另一个静态 Kilobot。当一个 Kilobot 发现了“食物”，它就会返回到它的“家”位置放下它。

另一个程序带领一组机器人跟随一个领头机器人单行列队。这些机器人小心翼翼地不要领先其他人太远，以免落后。他们还通过传感器协调他们的活动，例如闪烁他们的灯光。用户可以使用红外控制器和红外接收器执行可扩展的任务。这意味着他们不必逐个访问每个机器人来执行像充电或编程这样的简单任务。

## 15.4 Kilobots 运动

这是 Kilobots 的一般运动情况：

1.  1.

    进展已经取得。

1.  2.

    机器人旋转。

1.  3.

    机器人与相邻单位保持联系。

1.  4.

    计算相邻单位之间的距离。

1.  5.

    验证是否有足够的 RAM 来执行 S-DASH。

为了扩展其应用，以下额外的部分被添加到 Kilobot 中：

+   测量环境中光的量的能力。

+   允许可扩展操作的能力。

## 15.5 个物理建模

您可以在 GitHub 存储库中找到此模型。在[`github.com/JosephThachilGeorge/Platoon-Project`](https://github.com/JosephThachilGeorge/Platoon-Project)中查找 final-model.xml 文件。

由于 XML 文件较大，本节解释了代码的一些部分。

要添加块建模图，请按照以下说明操作：

1.  1.

    用鼠标拖动块/工作区。

1.  2.

    通过双击块来最小化/最大化/部分最小化块。

1.  3.

    从左侧的工具箱中拖放新的块。

1.  4.

    通过点击(+)下拉菜单将相关块添加到此块。

1.  5.

    右键单击块/工作区以查看菜单。

1.  6.

    通过点击按钮关闭此评论。

项目开始时，SOS 组织有各种需求，这些需求显示在 XML 文件中。这些是关于系统之间的网络系统（CSoS）的需求：-------------------------------------1\. CSoS-1.4                              </requirement>                              <data>CSoS-1.4</data>                              <statement name="cs:CS">                                <block type="__link" id="136">                                  <field name="link_to">CS / Kilobot</field>                                  <data>CS : 3 : 1</data>                                </block>                              </statement>                            </block>                          </statement>                          <next>                            <block type="execute$s" id="120">                              <field name="function"> joinPlatoon</field>                              <field name="#CS">+</field>                              <requirement pinned="false" h="100" w="200">Satisfies requirement(s) :-------------------------------------1\. CSoS-1.42\. CSoS-1.6                              </requirement>                              <data>CSoS-1.4,CSoS-1.6</data>                              <statement name="cs:CS">                                <block type="__link" id="129">                                  <field name="link_to">CS / Kilobot</field>                                  <data>CS : 3 : 1</data>-------------------------------------------------------------------------------------------------------------------。                              </statement>-------------------------------------------------------------------------------------------------------------------                            </block>-------------------------------------------------------------------------------------------------------------------                          </next>-------------------------------------------------------------------------------------------------------------------        </block>----------------------------------------------------------------------的这一部分还有一个名称为 T1、T2、T3 和 T4 的内容，用于传输消息。它们帮助说明消息在 CCS-1、CSoS-1、T-2 或 TI 或 T3 或 T4 之间的传输。

+   T-1：Kilobots 根据本地时钟来测量时间。

+   T-2：与时间相关的事件是通过消息交换触发的。

+   T-3：当一个 Kilobot 启动时，它会为 Mms 准备电机。

+   D-1：这个排将允许任何基斯博特成为成员。

+   D-2：这个排至少由两个基斯博特组成。

+   D-3：在这个排中引入一个基斯博特只允许在它的尾部。

+   D-4：这个排只允许最后一个基斯博特离开。

这些要求是通过以下代码实现的：-------------------------------------1\. D-42\. D-5        </requirement>        <data>D-4,D-5</data>        <statement name="can_access:state_variable">          <block type="__link" id="243">            <field name="link_to">状态变量 / leader_uid</field>            <data>state_variable : 67 : 0</data>            <next>              <block type="__link" id="149">                <field name="link_to">状态变量 / kilo_uid</field>                <data>state_variable : 66 : 0</data>              </block>            </next>          </block>        </statement>        <next>          <block type="service$s" id="244" collapsed="true">            <field name="name">Join</field>            <field name="#state_variable">+</field>            <requirement pinned="false" h="100" w="200">满足要求 :-------------------------------------1\. D-12\. D-3            </requirement>            <data>D-1,D-3</data>            <statement name="can_access:state_variable">              <block type="__link" id="248">                <field name="link_to">状态变量 / kilo_uid</field>                <data>state_variable : 66 : 0</data>              </block>            </statement>          </block>        </next>      </block>    </statement>  </block>  <block type="emergent_phenomenon$s" id="228" collapsed="true" x="748" y="1454">    <field name="name">编队</field>    <field name="#behaviour">+</field>    <statement name="causes:behaviour">      <block type="expected_and_beneficial_behaviour$i" id="229">        <field name="name">Unique Platoon</field>        <requirement pinned="false" h="100" w="200">满足要求 :-------------------------------------2\. D-2            </requirement>            <data>ASoS-1,D-2</data>            <statement name="has:RUI">              <block type="RUPI$s" id="61">                <field name="name">Calculate Distance</field>                <field name="has_connection">FALSE</field>                <field name="#connecting_strategy">+</field>                <field name="#interface_specification">+</field>                <field name="#interface_port">+</field>                <field name="#afferent_environment">+</field>                <field name="#efferent_environment">+</field>                <field name="#interface_model">+</field>                <field name="#thing">+</field>                <field name="#environment">+</field>                <field name="#RUPI">+</field>                <field name="#probe">+</field>                <field name="#security">+</field>                <requirement pinned="false" h="100" w="200">满足要求 :-------------------------------------

SOS 级别设计如下。CSoS-1：每个 Kilobot 将使用其 RUMI 交换关于方向的信息，在它加入编队时和离开编队时。CSoS-2：当 SoS 开始时，每个 Kilobot 通过传递消息通知其相邻的跟随者它是领导者。CSoS-3：每个 Kilobot 都有一个 RUPI，用于使用信号强度估算发送者和接收者之间的距离。

此 xml 代码列在此 GitHub 存储库中：

[`github.com/JosephThachilGeorge/Platoon-Project/blob/main/final-model.xml`](https://github.com/JosephThachilGeorge/Platoon-Project/blob/main/final-model.xml)

请注意，要运行此代码，您可以使用接受 xml 文件的任何模型模拟器。

执行后，您将看到 15-1a 和 15-1b 图中显示的模型。![../images/520777_1_En_15_Chapter/520777_1_En_15_Fig1_HTML.jpg](img/520777_1_En_15_Fig1_HTML.jpg)

图 15-1a

模型

![../images/520777_1_En_15_Chapter/520777_1_En_15_Fig2_HTML.jpg](img/520777_1_En_15_Fig2_HTML.jpg)

图 15-1b

模型，续

## 15.6 总结

项目排班帮助您设计和实现网络物理系统。相同的概念可以用来设计现实世界中的任何网络物理系统。Kilobot 运动说明了网络物理系统的各个部分及其特点。本章总结了与网络物理系统相关的项目。到目前为止，您已经学习了如何开发区块链和分布式系统。在下一章中，您将了解区块链和分布式网络物理系统的未来。
