© 作者，独家许可给 APress Media, LLC，属于 Springer Nature 2022 J. T. George《介绍区块链应用》[`doi.org/10.1007/978-1-4842-7480-4_13`](https://doi.org/10.1007/978-1-4842-7480-4_13)

# 13. 物联网项目

Joseph Thachil George^(1  )(1)意大利罗马

在本章中，您将学习如何基于一款名为 Witch Calls Color 的意大利游戏开发物联网系统。

这个游戏有以下规则：

+   选中一名玩家成为女巫。

+   他们呼喊一个颜色，比如蓝色。

+   然后其他孩子跑去触摸那种颜色的物体。（衣服不包括在内，而且只有一个人可以触摸一个物体。）

+   如果女巫抓住了一个没有触摸颜色的孩子，他们就会成为下一个女巫。然后原来的女巫加入其他孩子。

您将借助 Kilobots 实现此项目。女巫的移动和颜色都是在 Kilobots 中实现的。

## 13.1 使用 Kilobots

*Kilobot* 群是一个由 1,000 个机器人组成的群集，可以用来创建自动且具有长时间持续性的集体行为。每个机器人具有自主群体机器人的基本功能，但由有限数量的零件组成，并且主要由自动系统组装。

另外，该系统设计允许单个个体以高效且可扩展的方式操作大型 Kilobot 协作，包括对其进行编程、启动和为所有机器人添加燃料。Kilobot 群被用于研究集体“虚拟”智能，并测试将最小个人特征与群集特性联系起来的创新理论。参见图 13-1。

使用混合概念技术，您可以获得关于稳健性、适应性、个性以及有限个体群体中的新算法理解。

### 13.1.1 Kilobots 的运动

以下列表显示了基本的 Kilobots 运动：

+   向上运动

+   旋转特性

+   保持与相邻单元的联系

+   计算相邻单元之间的差异。

+   具有足够的 RAM 来执行 Kilobots

向 Kilobot 添加以下额外部件以扩展其实现：

+   估计环境中光的数量的能力

+   使操作更加灵活

![../images/520777_1_En_13_Chapter/520777_1_En_13_Fig1_HTML.jpg](img/520777_1_En_13_Fig1_HTML.jpg)

图 13-1

一个 Kilobot

## 13.2 项目要求

### 13.2.1 架构

1.  1.

    Kilobots 将在至少 100x80cm 的空间中操作。

1.  2.

    表面应光滑且反射，以使红外线正常工作。

1.  3.

    SoS 由至少五个 Kilobots 和一个控制器组成（一个巫师、两个玩家和两种颜色）。

1.  4.

    SoS 由至少五个 Kilobots 和一个控制器组成（一个巫师、两个玩家和两种颜色）。

1.  5.

    在程序执行开始时，为 Kilobots 分配了位置。

1.  6.

    每个 Kilobot 都有一个 ID、颜色和位置。

1.  7.

    游戏开始时，玩家搜索颜色，而巫师搜索玩家。

1.  8.

    巫师和玩家 Kilobots 正在等待彼此的信号以开始运行。

1.  9.

    目标颜色由程序选择。

1.  10.

    游戏期间，所有 Kilobots 都在互相搜索。

1.  11.

    游戏期间，巫师试图抓住玩家，而玩家则在寻找颜色。 如果巫师抓住了一名玩家，那名玩家将成为下一轮的巫师。

1.  12.

    当 Kilobots 抓住颜色时，回合结束。

1.  13.

    每个 Kilobot 都有两个独立的电机。

1.  14.

    每个 Kilobot 都有红外发射器和接收器。

1.  15.

    Kilobots 可以从环境中估计与其他机器人的相对距离。

1.  16.

    Kilobots 将在至少三种状态中的一种操作：运行、引导加载或休眠。

1.  17.

    通过消息接口，每个 Kilobot 都可以与其他每个 Kilobot 进行通信。

### 13.2.2 项目通信

1.  1.

    Kilobots 可以接收来自顶层控制器的消息。

1.  2.

    当 Kilobots 相距不超过 7.5 厘米时，它们正在通信。

1.  3.

    所有 Kilobots 之间的连接在每一轮开始时建立。

1.  4.

    应该有一个唯一的 Kilobot 作为中央通信协调员。

### 13.2.3 时间

每个 Kilobot 都将拥有一个基于时间的内部时钟。Kilobots 可以在发送的每条消息后的 10 秒内通过网络通信。

### 13.2.4 动态性

一个移出通信范围的 Kilobot 将开始移动，以寻找其他 Kilobots，以便重新成为网络的一部分。

### 13.2.5 可靠性

1.  1.

    可用性：Kilobots 需要有充电电池。

1.  2.

    可靠性：Kilobots 只有当它们能够与所有其他 Kilobots 通信时，才能开始每一轮游戏，因为它们没有提供必要的服务。

1.  3.

    完整性：SoS 不应该有不当状态才能正常运行。

## 13.3 Blockly4SoS 模型

在这个模型中，我们有一个由五个 Kilobots 和一个顶层控制器组成的 SoS。

1.  1.

    顶层控制器有一个 RUMI（一个可靠的消息接口），它用来向 Kilobots 发送关于它们必须进入的状态的信息，或者发送定义 Kilobots 行为的代码。

1.  2.

    ID=0 的 Kilobot 是通信的中心点；它帮助你定义更好的通信协议。

1.  3.

    每个 Kilobot 都有一个 RUMI，它是它们用来交换消息的接口，还有一个 RUPI（Relied Upon Physical Interface），它由红外传感器表示，用于捕捉环境信息（例如，与其他机器人的距离）。消息通道基于硬件层上的红外传感器，但由于它被用来直接通信数据和交换消息，因此它们是 RUMIs。Kilobots 的每一个特征都与一个需求相关联。

## 13.4 实施项目

在这个项目中，你分配 Kilobots 的起始位置并在 endstate.json 文件中指定它们。首先，一个 Kilobot 以螺旋方式移动，试图与其他 Kilobots 建立连接以接收信号。

在第一阶段，每个 Kilobot 发送一个包含 10 位的数组，其中所有位都为 0，除了数组位置等于 Kilobot ID 的那个位。当每个 Kilobot 都有一个数组时，这意味着每个 Kilobot 与所有其他 Kilobots 单向连接，并且它们已经准备好进行通信。第一阶段终止。

在第二阶段，所有 Kilobots 形成了一个网络，现在作为一个 SoS 进行操作。它们选择女巫并通过 Kilobots 网络广播这一信息。每个 Kilobot 重新发送收到的消息，直到被选择的女巫收到。然后女巫选择要捕捉的目标颜色并广播这一信息。

在下一阶段，Kilobots 尝试捕捉目标。每个 Kilobot 评估到目标 Kilobot 的距离，识别出哪些邻居具有比其他邻居都小的“到目标的距离”字段。通过将邻居的“到目标的距离”与 Kilobot X 到邻居最接近目标的距离相加，可以得到对目标的近似距离。这个过程从与目标有效通信的 Kilobots 开始，因为他们是唯一能够获得与目标的实际距离的人。之后，这个过程将递归地发生直到网络的最外部节点。

因此，与通信范围内的每个 Kilobot 都可以知道到目标的近似距离和它需要跟随的最近邻居。Kilobots 可能会超出通信范围。在这种情况下，它们开始以螺旋方式移动，直到找到与目标通信的人。

出现了一种意想不到的正面行为——当一个基洛机器人退出范围时，它会 360 度转身并再次进入范围。

## 13.5 执行项目

在这个项目中，您分配了基洛机器人的起始位置，并将它们指定在 endstate.json 文件中。现在，我们将根据您选择的设置（最重要的是 randSeed = 2）描述模拟。 

在图 13-2 中，您可以看到此模拟中机器人的起始位置。圆圈围绕着机器人表示它正在传输；两个机器人之间的线表示它们正在通信。

因此，从图 13-2 中可以看到，在开始时，只有一个机器人（ID = 1）在传输。最初，机器人的目标是创建一个网络，在这个网络中它们彼此连接并可以向任何机器人发送和接收消息，因此它们开始四处移动，只有当它们从与不断增长的网络连接的机器人收到消息时才停止移动，从机器人 1 开始。机器人 1 保持静止。

在机器人创建网络之后，它们使用这个共同的信道来协商主要的游戏参数，然后开始游戏。在此阶段，它们的工作要么是逃离其他机器人，要么是捕捉具有选定颜色的机器人。此外，此阶段始于只有一个机器人在传输；这是目标机器人或逃跑者，它不断发送其颜色和与目标的距离（当然是 0）。

没有收到消息的机器人开始四处移动寻找任何人，实际收到消息的机器人，并尝试使用这些消息中包含的有关目标机器人距离的信息来捕捉该机器人。见图 13-3。！../images/520777_1_En_13_Chapter/520777_1_En_13_Fig2_HTML.jpg

图 13-2

机器人轨道

！../images/520777_1_En_13_Chapter/520777_1_En_13_Fig3_HTML.jpg

图 13-3

机器人轨道

## 13.6 项目代码

这   这是项目的主要代码。它是用 C 语言开发的。要执行此代码，您需要一个 C 语言编译器。机器人的旋转和运动（左、右、前、后）在代码中的不同函数中定义。使用 `void setup_message()` 函数定义了每个机器人的消息处理。`orbit_tooclose()` 函数检查了相邻机器人的移动（见列表 13-1）。*void smooth_set_motors(uint8_t ccw, uint8_t cw)**{**#ifdef KILOBOT* *uint8_t l = 0, r = 0;* *if (ccw && !**OCR**2A)* *l = 0xff;* *if (cw && !**OCR**2B)* *r = 0xff;* *if (l || r)* *{* *set_motors(l, r);* *delay(15);* *}**#endif* *set_motors(ccw, cw);**}**void set_motion(motion_t new_motion)**{* *switch(new_motion) {* *case STOP:* *smooth_set_motors(0,0);* *break;* *case FORWARD:* *smooth_set_motors(kilo_straight_left, kilo_straight_right);* *break;* *case LEFT:* *smooth_set_motors(kilo_turn_left, 0);* *break;* *case RIGHT:* *smooth_set_motors(0, kilo_turn_right);* *break;* *}**}**void orbit_normal()**{* *if (mydata->cur_distance < TOOCLOSE_DISTANCE) {* *mydata->orbit_state = ORBIT_TOOCLOSE;* *} else {* *if (mydata->cur_distance < DESIRED_DISTANCE)* *set_motion(LEFT);* *else* *set_motion(RIGHT);* *}**}**void orbit_tooclose() {* *if (mydata->cur_distance >= DESIRED_DISTANCE)* *mydata->orbit_state = ORBIT_NORMAL;* *else* *set_motion(FORWARD);**}**int EffectId;**int dist;**int id=10;**void loop() {**if(mydata->type==2)**{* *set_color(**RGB**(0,1,0));**}**if(id<10)**{* *if(kilo_uid==id){**printf("id : %d   %d    %d   id:%d \n",kilo_uid,mydata->type,mydata->typeEffect,id);**mydata->type=1;**set_color(**RGB**(1,0,0));**id=10;}**}**if(mydata->IdEffect<10){**switch(mydata->type)**{* *case 1:{**if(mydata->typeEffect==2)**{* *printf("this =>   %d    %d   %d\n",mydata->type,mydata->typeEffect,mydata->IdEffect);**if(mydata->nowDist<40)**{* *id=mydata->IdEffect;**set_color(**RGB**(0,1,0));**mydata->type=2;**set_motion(RIGHT);**}**else   if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist>mydata->beforDist){**printf("befor :%d  now: %d   befordist:%d   nowdist:%d   move:%d\n",**mydata->beforIdEffect,mydata->IdEffect,mydata->beforDist,mydata->nowDist,mydata->move);* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**break;}* *case 2:{**if(mydata->typeEffect==3)**{* *if(mydata->nowDist<40)**{* *set_color(**RGB**(0,0,0));**set_motion(FORWARD);**}**}**if(mydata->typeEffect==1)**{* *if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist<mydata->beforDist){* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**if(mydata->typeEffect==3)**{* *if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist>mydata->beforDist){* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**break;}* *case 3:{break;}**}**}**else  if(mydata->beforIdEffect<10){* *if(mydata->type<3){* *if(mydata->countmove>125){* *mydata->countmove=0;* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *mydata->countmove=100;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**mydata->countmove=mydata->count-   这是项目的主要代码。它是用 C 语言开发的。要执行此代码，您需要一个 C 语言编译器。机器人的旋转和运动（左、右、前、后）在代码中的不同函数中定义。使用 `void setup_message()` 函数定义了每个机器人的消息处理。`orbit_tooclose()` 函数检查了相邻机器人的移动（见列表 13-1）。*void smooth_set_motors(uint8_t ccw, uint8_t cw)**{**#ifdef KILOBOT* *uint8_t l = 0, r = 0;* *if (ccw && !**OCR**2A)* *l = 0xff;* *if (cw && !**OCR**2B)* *r = 0xff;* *if (l || r)* *{* *set_motors(l, r);* *delay(15);* *}**#endif* *set_motors(ccw, cw);**}**void set_motion(motion_t new_motion)**{* *switch(new_motion) {* *case STOP:* *smooth_set_motors(0,0);* *break;* *case FORWARD:* *smooth_set_motors(kilo_straight_left, kilo_straight_right);* *break;* *case LEFT:* *smooth_set_motors(kilo_turn_left, 0);* *break;* *case RIGHT:* *smooth_set_motors(0, kilo_turn_right);* *break;* *}**}**void orbit_normal()**{* *if (mydata->cur_distance < TOOCLOSE_DISTANCE) {* *mydata->orbit_state = ORBIT_TOOCLOSE;* *} else {* *if (mydata->cur_distance < DESIRED_DISTANCE)* *set_motion(LEFT);* *else* *set_motion(RIGHT);* *}**}**void orbit_tooclose() {* *if (mydata->cur_distance >= DESIRED_DISTANCE)* *mydata->orbit_state = ORBIT_NORMAL;* *else* *set_motion(FORWARD);**}**int EffectId;**int dist;**int id=10;**void loop() {**if(mydata->type==2)**{* *set_color(**RGB**(0,1,0));**}**if(id<10)**{* *if(kilo_uid==id){**printf("id : %d   %d    %d   id:%d \n",kilo_uid,mydata->type,mydata->typeEffect,id);**mydata->type=1;**set_color(**RGB**(1,0,0));**id=10;}**}**if(mydata->IdEffect<10){**switch(mydata->type)**{* *case 1:{**if(mydata->typeEffect==2)**{* *printf("this =>   %d    %d   %d\n",mydata->type,mydata->typeEffect,mydata->IdEffect);**if(mydata->nowDist<40)**{* *id=mydata->IdEffect;**set_color(**RGB**(0,1,0));**mydata->type=2;**set_motion(RIGHT);**}**else   if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist>mydata->beforDist){**printf("befor :%d  now: %d   befordist:%d   nowdist:%d   move:%d\n",**mydata->beforIdEffect,mydata->IdEffect,mydata->beforDist,mydata->nowDist,mydata->move);* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**break;}* *case 2:{**if(mydata->typeEffect==3)**{* *if(mydata->nowDist<40)**{* *set_color(**RGB**(0,0,0));**set_motion(FORWARD);**}**}**if(mydata->typeEffect==1)**{* *if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist<mydata->beforDist){* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**if(mydata->typeEffect==3)**{* *if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist>mydata->beforDist){* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**break;}* *case 3:{break;}**}**}**else  if(mydata->beforIdEffect<10){* *if(mydata->type<3){* *if(mydata->countmove>125){* *mydata->countmove=0;* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *mydata->countmove=100;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**mydata->countmove=mydata->countmove-   这是项目的主要代码。它是用 C 语言开发的。要执行此代码，您需要一个 C 语言编译器。机器人的旋转和运动（左、右、前、后）在代码中的不同函数中定义。使用 `void setup_message()` 函数定义了每个机器人的消息处理。`orbit_tooclose()` 函数检查了相邻机器人的移动（见列表 13-1）。*void smooth_set_motors(uint8_t ccw, uint8_t cw)**{**#ifdef KILOBOT* *uint8_t l = 0, r = 0;* *if (ccw && !**OCR**2A)* *l = 0xff;* *if (cw && !**OCR**2B)* *r = 0xff;* *if (l || r)* *{* *set_motors(l, r);* *delay(15);* *}**#endif* *set_motors(ccw, cw);**}**void set_motion(motion_t new_motion)**{* *switch(new_motion) {* *case STOP:* *smooth_set_motors(0,0);* *break;* *case FORWARD:* *smooth_set_motors(kilo_straight_left, kilo_straight_right);* *break;* *case LEFT:* *smooth_set_motors(kilo_turn_left, 0);* *break;* *case RIGHT:* *smooth_set_motors(0, kilo_turn_right);* *break;* *}**}**void orbit_normal()**{* *if (mydata->cur_distance < TOOCLOSE_DISTANCE) {* *mydata->orbit_state = ORBIT_TOOCLOSE;* *} else {* *if (mydata->cur_distance < DESIRED_DISTANCE)* *set_motion(LEFT);* *else* *set_motion(RIGHT);* *}**}**void orbit_tooclose() {* *if (mydata->cur_distance >= DESIRED_DISTANCE)* *mydata->orbit_state = ORBIT_NORMAL;* *else* *set_motion(FORWARD);**}**int EffectId;**int dist;**int id=10;**void loop() {**if(mydata->type==2)**{* *set_color(**RGB**(0,1,0));**}**if(id<10)**{* *if(kilo_uid==id){**printf("id : %d   %d    %d   id:%d \n",kilo_uid,mydata->type,mydata->typeEffect,id);**mydata->type=1;**set_color(**RGB**(1,0,0));**id=10;}**}**if(mydata->IdEffect<10){**switch(mydata->type)**{* *case 1:{**if(mydata->typeEffect==2)**{* *printf("this =>   %d    %d   %d\n",mydata->type,mydata->typeEffect,mydata->IdEffect);**if(mydata->nowDist<40)**{* *id=mydata->IdEffect;**set_color(**RGB**(0,1,0));**mydata->type=2;**set_motion(RIGHT);**}**else   if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist>mydata->beforDist){**printf("befor :%d  now: %d   befordist:%d   nowdist:%d   move:%d\n",**mydata->beforIdEffect,mydata->IdEffect,mydata->beforDist,mydata->nowDist,mydata->move);* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**break;}* *case 2:{**if(mydata->typeEffect==3)**{* *if(mydata->nowDist<40)**{* *set_color(**RGB**(0,0,0));**set_motion(FORWARD);**}**}**if(mydata->typeEffect==1)**{* *if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist<mydata->beforDist){* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**if(mydata->typeEffect==3)**{* *if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist>mydata->beforDist){* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**break;}* *case 3:{break;}**}**}**else  if(mydata->beforIdEffect<10){* *if(mydata->type<3){* *if(mydata->countmove>125){* *mydata->countmove=0;* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *mydata->countmove=100;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**mydata->countmove=mydata->countmove+-   这是项目的主要代码。它是用 C 语言开发的。要执行此代码，您需要一个 C 语言编译器。机器人的旋转和运动（左、右、前、后）在代码中的不同函数中定义。使用 `void setup_message()` 函数定义了每个机器人的消息处理。`orbit_tooclose()` 函数检查了相邻机器人的移动（见列表 13-1）。*void smooth_set_motors(uint8_t ccw, uint8_t cw)**{**#ifdef KILOBOT* *uint8_t l = 0, r = 0;* *if (ccw && !**OCR**2A)* *l = 0xff;* *if (cw && !**OCR**2B)* *r = 0xff;* *if (l || r)* *{* *set_motors(l, r);* *delay(15);* *}**#endif* *set_motors(ccw, cw);**}**void set_motion(motion_t new_motion)**{* *switch(new_motion) {* *case STOP:* *smooth_set_motors(0,0);* *break;* *case FORWARD:* *smooth_set_motors(kilo_straight_left, kilo_straight_right);* *break;* *case LEFT:* *smooth_set_motors(kilo_turn_left, 0);* *break;* *case RIGHT:* *smooth_set_motors(0, kilo_turn_right);* *break;* *}**}**void orbit_normal()**{* *if (mydata->cur_distance < TOOCLOSE_DISTANCE) {* *mydata->orbit_state = ORBIT_TOOCLOSE;* *} else {* *if (mydata->cur_distance < DESIRED_DISTANCE)* *set_motion(LEFT);* *else* *set_motion(RIGHT);* *}**}**void orbit_tooclose() {* *if (mydata->cur_distance >= DESIRED_DISTANCE)* *mydata->orbit_state = ORBIT_NORMAL;* *else* *set_motion(FORWARD);**}**int EffectId;**int dist;**int id=10;**void loop() {**if(mydata->type==2)**{* *set_color(**RGB**(0,1,0));**}**if(id<10)**{* *if(kilo_uid==id){**printf("id : %d   %d    %d   id:%d \n",kilo_uid,mydata->type,mydata->typeEffect,id);**mydata->type=1;**set_color(**RGB**(1,0,0));**id=10;}**}**if(mydata->IdEffect<10){**switch(mydata->type)**{* *case 1:{**if(mydata->typeEffect==2)**{* *printf("this =>   %d    %d   %d\n",mydata->type,mydata->typeEffect,mydata->IdEffect);**if(mydata->nowDist<40)**{* *id=mydata->IdEffect;**set_color(**RGB**(0,1,0));**mydata->type=2;**set_motion(RIGHT);**}**else   if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist>mydata->beforDist){**printf("befor :%d  now: %d   befordist:%d   nowdist:%d   move:%d\n",**mydata->beforIdEffect,mydata->IdEffect,mydata->beforDist,mydata->nowDist,mydata->move);* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**break;}* *case 2:{**if(mydata->typeEffect==3)**{* *if(mydata->nowDist<40)**{* *set_color(**RGB**(0,0,0));**set_motion(FORWARD);**}**}**if(mydata->typeEffect==1)**{* *if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist<mydata->beforDist){* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**if(mydata->typeEffect==3)**{* *if(mydata->beforIdEffect==mydata->IdEffect)**{* *if(mydata->nowDist>mydata->beforDist){* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**}**}**mydata->beforIdEffect=mydata->IdEffect;**mydata->beforDist=mydata->nowDist;**mydata->IdEffect=10;**}**break;}* *case 3:{break;}**}**}**else  if(mydata->beforIdEffect<10){* *if(mydata->type<3){* *if(mydata->countmove>125){* *mydata->countmove=0;* *switch(mydata->move){* *case 0:* *set_motion(LEFT);mydata->move=1;* *break;* *case 1:set_motion(FORWARD);mydata->move=2;* *mydata->countmove=100;* *break;* *case 2:set_motion(RIGHT);mydata->move=0;* *break;* *}**mydata->countmove=mydata->countmove+1;**}**}**}**}**void message_rx(message_t *m, distance_measurement_t *d) {*mydata->nowDist = estimate_distance(d);* *mydata->dist = *d;**mydata->IdEffect= m->data[0];**mydata->typeEffect= m->data[1];**}**void setup_message

Orbit.c

在接下来的项目中，我们为 Kilobots 分配了起始位置，并在 endstate.json 文件中指定，如清单 13-2 所示。

***{***  ***"bot_states": [***    ***{***      ***"ID": 0,***      ***"direction": 0.24680567903004347,***      ***"state": {},***      ***"x_position": -223.0,***      ***"y_position": -156.0***    ***},***    ***{***      ***"ID": 1,***      ***"direction": 5.8484504331042393,***      ***"state": {},***      ***"x_position": -258.0,***      ***"y_position": 185.0***    ***},***    ***{***      ***"ID": 2,***      ***"direction": 4.8963292787052639,***      ***"state": {},***      ***"x_position": 56.320128808496456,***      ***"y_position": -190.86350829767215***    ***},***    ***{***      ***"ID": 3,***      ***"direction": 4.3219605347985022,***      ***"state": {},***      ***"x_position": 32.498282727499863,***      ***"y_position": -215.63645771384685***    ***},***    ***{***      ***"ID": 4,***      ***"direction": 5.5296756682271786,***      ***"state": {},***      ***"x_position": 248.0,***      ***"y_position": -44.0***    ***}***  ***],***  ***"ticks": 224******}***Listing 13-2

*endstate.json*

在这个项目中，Kilobots 的基本结构在 kilombo.json 文件中被定义和指定，如清单 13-3 所示。

***清单 13-3.*** *kilombo.json*{    "botName" : "轨道机器人",    "randSeed" : 1,    "nBots" : 5,    "timeStep" : 0.0416666,    "__note" : "0.04166 是 24 FPS，与电影帧率相匹配",    "__timeStep" : 0.03225,    "simulationTime" : 0,    "commsRadius" : 100,    "showComms" : 0,    "showCommsRadius" : 0,    "distributePercent" : 0.8,    "displayWidth"  : 800,    "displayHeight" : 700,    "displayWidthPercent" : 80,    "displayHeightPercent" : 80,    "displayScale"  : 1,    "showHist" : 1,    "histLength": 4000,    "storeHistory": 1,    "imageName" : "./movie4/f%04d.bmp",    "saveVideo" :  0,    "saveVideoN" : 1,    "stepsPerFrame" : 1,    "finalImage" : null,    "stateFileName" : "simstates.json",    "stateFileSteps" : 0,    "colorscheme" : "bright",    "speed": 7,    "turnRate" : 22,    "GUI"  : 1 ,    "msgSuccessRate" : 0.8,    "distanceNoise" : 2}

在接下来的项目中，轨道的基本结构在 orbit.h 文件中定义和指定，如清单 13-4 所示。

***清单 13-4.*** *orbit.h**{*    *"botName" : "轨道机器人",*    *"randSeed" : 1,*    *"nBots" : 5,*    *"timeStep" : 0.0416666,*    *"__note" : "0.04166 是 24 FPS，与电影帧率相匹配",*    *"__timeStep" : 0.03225,*    *"simulationTime" : 0,*    *"commsRadius" : 100,*    *"showComms" : 0,*    *"showCommsRadius" : 0,*    *"distributePercent" : 0.8,*    *"displayWidth"  : 800,*    *"displayHeight" : 700,*    *"displayWidthPercent" : 80,*    *"displayHeightPercent" : 80,*    *"displayScale"  : 1,*    *"showHist" : 1,*    *"histLength": 4000,*    *"storeHistory": 1,*    *"imageName" : "./movie4/f%04d.bmp",*    *"saveVideo" :  0,*    *"saveVideoN" : 1,*    *"stepsPerFrame" : 1,*    *"finalImage" : null,*    *"stateFileName" : "simstates.json",*    *"stateFileSteps" : 0,*    *"colorscheme" : "bright",*    *"speed": 7,*    *"turnRate" : 22,*    *"GUI"  : 1 ,*    *"msgSuccessRate" : 0.8,*    *"distanceNoise" : 2**}*

如果您将以下 GitHub 文件上传到[`blockly4sos.resiltech.com/latest/demos/amadeos/i.html`](https://blockly4sos.resiltech.com/latest/demos/amadeos/i.html)，您将获得该项目的 Blockly4Sos 图表。图 13-4 显示了输出。

[`github.com/JosephThachilGeorge/Blockly4SoS`](https://github.com/JosephThachilGeorge/Blockly4SoS)![../images/520777_1_En_13_Chapter/520777_1_En_13_Fig4_HTML.jpg](img/520777_1_En_13_Fig4_HTML.jpg)

图 13-4

BlocklySoS 输出

## 13.7 总结

本章讨论了如何基于意大利游戏《巫婆呼叫颜色》创建一个网络物理系统。该项目说明了网络物理系统的特性以及分布式系统使用的通信方式。该项目是借助 BlocklySoS 建模图进行建模的。下一章将深入探讨一个更复杂的项目，这将帮助您更好地理解分布式系统架构。
