© 尼希斯·帕塔克和阿努拉格·班德里 2018 年 尼希斯·帕塔克和阿努拉格·班德里为.NET 开发的物联网、人工智能和区块链`doi.org/10.1007/978-1-4842-3709-0_3`

# 创建智能物联网应用

[尼希斯·帕塔克](https://example.org/nishith_pathak)和[阿努拉格·班德里](https://example.org/anurag_bhandari)（1）印度帕里加尔瓦尔县科特瓦拉（2）印度旁遮普邦贾兰达尔，在第二章中，我们学习了物联网、物联网设备、实际应用案例和消息协议。我们还对 Azure 物联网套件及其各种组件有了概念性的理解，特别是 Azure 物联网中心。拥有了这些知识，现在是时候自己创建一个物联网解决方案了。我们将创建自己的物联网网络，并为该网络中的设备编写应用程序来解决一个真实世界的问题。到本章结束时，您将学会：

+   使用 Azure 的设备 SDK 为物联网设备编写应用程序

+   创建模拟物联网设备

+   创建物联网中心

+   进行设备到云和云到设备的通信

+   使用通知中心服务发送推送通知

## 用例：集中患者监控

我们的用例将围绕解决阿斯克勒庇俄斯财团的问题。请参阅第一章中称为“智能医院”的部分，以获取有关这个虚构协会的更多详细信息。

### 问题

阿斯克勒庇俄斯联盟的成员医院都面临着同样的问题。医生或护士无法始终陪伴每位患者，即使是在重症监护室的患者，也需要照顾其他现有和新来的患者。通常，护士会在设定的固定间隔后访问患者，给予药物并检查重要统计数据，但有时这还不够。曾经发生过由于护士和医生无法及时通知而导致患者生命体征开始恶化而延迟提供必要护理的情况，无论是严重的还是其他情况都发生过。显然，在这种典型的医疗场景中，能够自动监测和通知的解决方案将是一种天赐之物。

### 解决方案

最简单的解决方案涉及创建一个由 Azure IoT Hub 连接的两个物联网设备的网络——一个用于收集患者数据（带有传感器的设备），另一个用于根据收集的数据采取行动（带有执行器的设备）。数据在中心处理，要采取的行动在中心计算。根据医院的规模和其他因素，这种解决方案的实际部署将比我们的两设备设置更大更复杂，但基本原理将保持不变。我们简化的解决方案将为您提供一个良好的起点。Azure IoT 通过提供完全托管的界面，以便稍后添加、删除和维护几乎无限的物联网设备，使扩展解决方案变得非常简单。图 3-1 是所提议的解决方案的视觉描述。![A458845_1_En_3_Fig1_HTML.png](img/A458845_1_En_3_Fig1_HTML.png)图 3-1 所提议的集中式患者监测解决方案的数据流以下是这个解决方案的逐步拆解：

+   步骤 1. 与患者连接的标准医疗设备不断记录他们的生命体征—体温、脉搏、呼吸率和血压。

+   Step 2. 一个物联网设备（设备 1）通过 GPIO 或无线接口连接到病人的医疗设备。设备 1 接收医疗设备记录的所有数据。除此之外，它还具有自己的传感器来测量房间的温度和湿度值。所有这些统计数据的组合对于可靠地监测患者的健康状况是必要的。

+   Step 3. 设备 1 将组合的遥测数据发送到我们的 IoT 中心。一个编写用于接收中心传入消息的应用程序（解决方案后端）不断分析数据流的输入。如果值在正常范围内，不采取任何行动。相反，如果我们的逻辑检测到异常，它会向设备 2 发送消息以触发警报。作为额外的预防措施，通过 Azure 通知中心向医生的手机发送推送通知。

+   Step 4. 设备 2——安装在病人房间外的——持续监听我们的物联网中心。根据从中心收到的消息的严重程度，它会触发与之连接的物理警报作为执行器。

+   Step 5. 物理警报立即引起附近工作人员的注意，减少了患者获得专业医疗帮助的潜在延迟。

在我们实施此解决方案时，我们将使用一个模拟设备和一个实际设备（树莓派）。设备 1 将是一个模拟设备，基本上是一个使用 Azure 的设备 SDK 模拟 IoT 设备并生成随机传感器值的自定义软件程序。学习创建模拟设备将有两个优点：（1）即使没有实际设备和/或其传感器，您也可以学习 IoT 中心的工作原理，（2）您将学会在使用实际设备之前测试您的网络。设备 2 将是树莓派 Zero W，基本上是带有预安装 WiFi 和蓝牙的 Zero Pi。Pi Zero W 价格便宜（$10）且易于使用。

## 获得 Azure 订阅

如果您已经拥有 Azure 帐户，请随意跳过此部分。利用 Azure IoT 套件中的服务，包括 IoT Hub，将需要您拥有有效的 Azure 订阅。Azure 订阅与仅拥有免费的 Microsoft Live ID（@outlook.com 或 @hotmail.com 邮件帐户）不同。订阅可以通过多种方式获得，包括使用您的信用卡在 Azure 网站上创建帐户，并与 Visual Studio Professional 捆绑在一起。为了本书的目的，我们将探讨前一种选项。注册 Azure 帐户很容易，但需要您拥有 Microsoft 帐户 —— 如果您尚未拥有，可在 signup.live.com 免费获取。您有两种选择注册 Azure 帐户 —— 获取按使用量付费的订阅或开始使用为期 30 天的免费试用。通过按使用量付费的订阅，您按使用的服务支付月度费用。该订阅是一种无承诺的订阅，这意味着您不需要支付任何额外的初始费用或固定的月度费用。例如，如果您唯一使用的服务是每月 20 美元的 VM，那么只需每月支付这笔费用，只要您使用它。同样，如果您已激活了 IoT Hub 的免费层，如果保持在免费层强加的限制范围内，则不需要支付 0 美元或任何费用。为期 30 天的免费试用是您的最佳选择，如果您是首次使用者，则强烈推荐使用。通过此试用，您的 Azure 帐户将获得价值 200 美元的免费额度（随时可能更改）。您可以随意使用此信用额度。一旦您用尽了免费信用 —— 这通常是不太可能的情况 —— 您将被要求支付额外的付费服务。在试用期满后的 30 天内，您将有机会切换到按使用量付费的订阅。如果您不这样做，您将失去在试用期间设置的服务的访问权限。但是，与通常的试用情况不同，Azure 在您的试用期到期后不会自动将您升级到付费计划。因此，您的信用卡/借记卡没有被自动收费的风险。值得一提的是，Visual Studio 专业版和企业版订户每月都会获得免费的 Azure 信用额度 —— 专业版订户为 50 美元，企业版订户为 150 美元。此金额将每月自动记入与 Visual Studio 订阅关联的 Microsoft 帐户。假设您没有现有的 Azure 帐户，让我们注册免费试用。使用 Microsoft 帐户，前往 [`azure.microsoft.com/en-in/free`](https://azure.microsoft.com/en-in/free) 并单击“开始免费”按钮。此时可能会要求您使用 Microsoft 帐户登录。登录后，您将收到有关您的帐户没有现有订阅的消息。单击“注册免费试用”链接。这将显示一个注册表单，您需要在其中提供有关自己的基本信息，如图 3-2 中所示。![A458845_1_En_3_Fig2_HTML.jpg](img/A458845_1_En_3_Fig2_HTML.jpg)图 3-2 Azure 试用注册表单接下来，您将被要求输入一些额外信息以进行身份验证。这包括您的手机号码和信用卡详细信息。请注意，仅用于验证需要信用卡详细信息。在注册过程中，您可能会被收取一笔小额虚假费用，但该交易会立即被撤销。正如微软在其网站上所述 —— 我们通过验证账户持有人是否为真实人员而保持价格低廉，而不是机器人或匿名麻烦制造者。不用担心，除非您明确转换为付费服务，否则不会收取您的卡费，尽管您可能会看到临时的授权保留。一旦您的身份验证通过，您将需要接受订阅协议才能完成申请。此时，花点时间快速浏览一下协议条款和提供详细信息的好处，这两个链接都在申请表的协议部分中给出。一旦您接受了协议并单击“注册”按钮，您将被重定向到订户页面。在这里，单击按钮转到 Azure 门户。

## 创建一个物联网中心

IoT Hub 是我们网络的核心。它是使设备能够与解决方案后端安全通信的实体，反之亦然。我们将首先创建这个，然后再处理设备。拥有 Azure 订阅的我们，可以前去创建一个中心。前往[`portal.azure.com`](https://portal.azure.com)，进入 Azure 门户。从左侧菜单中，点击“新建”。从结果中选择“物联网 ➤ IoT Hub”，如图 3-3 所示。或者，在“搜索市场”文本框中搜索“iot hub”。![A458845_1_En_3_Fig3_HTML.jpg](img/A458845_1_En_3_Fig3_HTML.jpg)图 3-3Azure 中的新资源窗格在结果表单中（参见图 3-4），为您的中心输入一个唯一名称。作为一项惯例，我们遵循 <nickname>-<resource type>-<application name> 的表示法，但您可以使用您自己的表示法，只要名称在全球范围内是唯一的即可。将定价层从 S1（付费）更改为 F1（免费）。免费层每日消息限制为 8000 条，这对我们的测试是足够的。或者，您可以利用 Azure 试用订阅所获得的免费信用额度选择付费帐户，以便将我们的实验推进到下一个水平，因为如果创建免费层中心，您将无法升级到更高的计划。免费层中将禁用 IoT Hub 单元和设备到云分区字段：前者涉及管理每日消息配额，后者影响中心的可用性和一致性，因为它决定了可以连接到您中心的并发读取器的数量（这是直接从 Azure 的事件中心引入的概念）。现在您可以忽略这些值，然后继续创建中心。![A458845_1_En_3_Fig4_HTML.jpg](img/A458845_1_En_3_Fig4_HTML.jpg)图 3-4 新的 IoT Hub 表单通常需要 1-2 分钟才能完成创建新中心的操作。中心准备好后，您将在顶部的通知中心看到一个通知。单击通知以打开中心的详细信息页面，如图 3-5 所示。请记下主机名字段。这是您的中心托管的 URL，也是设备和解决方案后端将与之交互的 URL。![A458845_1_En_3_Fig5_HTML.jpg](img/A458845_1_En_3_Fig5_HTML.jpg)图 3-5 我们新创建的 IoT Hub 的详细信息刀片主机名值，但是，不能直接用于注册设备或应用程序用于与中心发送/接收消息。您还需要一个共享访问密钥对。主机名和共享访问密钥的组合是连接字符串。稍后您会看到，共享访问密钥对对于每个注册的设备以及注册新设备都是不同的。创建新中心时，Azure 会为您创建具有不同权限的各种角色（策略）。每个策略都有其自己的共享访问密钥集。为了我们解决方案的目的，让我们检索具有完全权限的策略对应的连接字符串。在生产设置中，您可能想要使用更严格的策略。在您的 IoT Hub 详细信息刀片中，导航至设置 ➤ 共享访问策略 ➤ iothubowner。在结果的右侧边栏（参见图 3-6），向下滚动以找到连接字符串—主要密钥。记下它。![A458845_1_En_3_Fig6_HTML.jpg](img/A458845_1_En_3_Fig6_HTML.jpg)图 3-6 获取 IoT Hub 的连接字符串

## 创建设备标识

接下来的步骤是在中心的注册表中注册我们的设备。在第二章中，您看到安全性是物联网中心的头等大事。如果设备未在中心注册，则无法连接到中心。因此，甚至在我们创建模拟设备（设备 1）并配置我们的 Pi Zero（设备 2）之前，我们将创建它们的设备标识。每个设备标识都与设备 ID 和密钥相关联。我们在设备上运行的客户端应用程序将需要这些值来向中心标识自己。有两种创建设备标识的方式——使用代码和通过 Azure 门户。我们将探索两种方式。

### 使用代码

这种方法需要使用 Azure 的设备 SDK 来编写几行代码。 使用这种方法注册一个或两个设备可能有点繁琐，但在注册数百或数千个设备时，或者在自动化设备注册时，它非常有帮助。 我们将创建一个基于 C# 的简单的 Windows 控制台应用程序。 启动您的 Visual Studio。 转到文件 ➤ 新建 ➤ 项目，然后选择 Visual C# ➤ Windows Classic Desktop 下的控制台应用程序。 参考图 3-7。![A458845_1_En_3_Fig7_HTML.jpg](img/A458845_1_En_3_Fig7_HTML.jpg)图 3-7 在 Visual Studio 2017 中创建新的控制台应用程序一旦 Visual Studio 完成创建新应用程序，请在“解决方案资源管理器”中右键单击“AddDeviceToHub”项目，然后选择“管理 NuGet 包”。 在包管理器窗口中，切换到“浏览”选项卡，搜索“Microsoft.Azure.Devices”，并安装列表中的第一个包（与搜索的名称完全匹配）。 您可能会提示安装 Azure IoT 设备 SDK 以及其他几个依赖项； 选择全部安装。 注所示，我们用于所有后续代码示例的版本是 Visual Studio Professional 2017。 如果您没有 Professional 2017 或者正在运行较旧版本，我们强烈建议您升级。 免费提供的 VS Community 2017 将同样有效。 接下来，在 App.config 中添加一个新的 IoT Hub 连接字符串设置。 添加以下代码。 将 value 属性的值替换为您在“创建 IoT Hub”部分末尾记下的连接字符串。<appSettings>  <add key="connectionString" value="" /></appSettings>在 Program.cs 中，复制粘贴以下代码：using System;using System.Threading.Tasks;using Microsoft.Azure.Devices;using Microsoft.Azure.Devices.Common.Exceptions;namespace AddDeviceToHub{    class Program    {        static RegistryManager registryManager;        static string connectionString = System.Configuration.ConfigurationManager.AppSettings["connectionString"];        static void Main(string[] args)        {            registryManager = RegistryManager.CreateFromConnectionString(connectionString);            RegisterDeviceAsync().Wait();            Console.ReadLine();        }        private static async Task RegisterDeviceAsync()        {            string deviceId = "medicaldevice-patient1";            Device device;            try            {                device = await registryManager.AddDeviceAsync(new Device(deviceId));            }            catch (DeviceAlreadyExistsException)            {                device = await registryManager.GetDeviceAsync(deviceId);            }            Console.WriteLine("设备的共享访问密钥：" + device.Authentication.SymmetricKey.PrimaryKey);        }    }}让我们逐步分解这个程序，以了解每个部分中发生了什么。添加 NuGet 包会自动将其 DLL 添加到项目的引用中，但其相应的 using 语句需要手动放置在代码中。 这就是为什么我们在顶部有以下两行代码：using Microsoft.Azure.Devices;using Microsoft.Azure.Devices.Common.Exceptions;我们需要对 hub 的注册管理器进行引用。 所以，我们创建了一个新的静态字段：static RegistryManager registryManager;我们还为连接字符串创建了一个静态字段：static string connectionString = System.Configuration.ConfigurationManager.AppSettings["connectionString"];ConfigurationManager 类默认情况下不在 System.Configuration 命名空间中。 我们必须在项目中添加对 System.Configuration DLL 的引用。 右键单击“解决方案资源管理器”中的“引用”，然后向下滚动以添加所需的引用，如图 3-8 所示。![A458845_1_En_3_Fig8_HTML.jpg](img/A458845_1_En_3_Fig8_HTML.jpg)图 3-8 添加对 System.Configuration 的引用 RegisterDeviceAsync 是注册我们的设备的实际方法。 我们将其用于仅注册设备 1。 它尝试将设备添加到我们的 hub 注册中。 如果具有指定设备 ID 的设备已存在，则会获取现有

### 使用门户

Azure 门户通过提供类似向导的界面，使将设备添加到中心变得非常容易。尽管这种方法更简单，但它涉及逐个创建设备。要创建新设备，请导航到你的物联网中心的详细信息窗格。在其左侧边栏中，向下滚动并选择“Explorers ➤ IoT Devices ➤ Add”。填写如图 3-9 所示的详细信息。![A458845_1_En_3_Fig9_HTML.jpg](img/A458845_1_En_3_Fig9_HTML.jpg)图 3-9 通过 Azure 门户添加设备一旦设备成功添加，它将在设备资源管理器中列出，与我们之前使用代码添加的 Device 1 并列。如果添加的设备状态显示为“已禁用”，请通过打开其设备详细信息窗格来启用该设备。

## 创建模拟设备

创建了我们的中心并注册了设备后，让我们创建一个模拟设备，该设备将定期向中心发送病人遥测数据。

### 创建应用程序

步骤与我们在创建设备标识部分看到的相似。在 Visual Studio 中，创建另一个名为 SimulatedDevice 的控制台应用程序，位于 IoTCentralizedPatientMonitoring 解决方案中。将 NuGet 包 Microsoft.Azure.Devices.Client 安装到新项目中。像之前一样，添加对 System.Configuration 的引用，以便从 App.config 中读取应用程序设置。在 App.config 中，添加以下键值对：<appSettings>  <add key="iotHubHostname" value="" />  <add key="deviceId" value="medicaldevice-patient1" />  <add key="deviceSharedAccessKey" value="" /></appSettings>iotHubHostname 的值是我们在“创建 IoT Hub”部分中记下的主机名，而不是连接字符串。deviceSharedAccessKey 是“创建设备标识”子部分的“使用代码”子部分末尾打印的输出。如果您没有机会记下它，您可以轻松地从 Azure 门户中的 IoT 设备资源管理器中获取它；从那里获取主密钥值。在 SimulatedDevice 项目的 Program.cs 文件中添加以下代码：static void Main(string[] args){  deviceClient = DeviceClient.Create(iotHubHostname, new DeviceAuthenticationWithRegistrySymmetricKey(deviceId, deviceSharedAccessKey), TransportType.Mqtt);  deviceClient.ProductInfo = "Asclepius Consortium Vitals Recorder";  SendPatientTelemetryToHubAsync();  Console.ReadLine();}private static async void SendPatientTelemetryToHubAsync(){  // Minimum values for telemetry parameters  double minBodyTemperature = 36.5; // degrees Celsius  double minPulseRate = 60; // beats per minute  double minRespirationRate = 12; // breaths per minute  double minRoomTemperature = 18; // degrees Celsius  double minRoomHumidity = 30; // percentage  Random random = new Random();  while (true)  {    // Pretentiously received from the medical device    double currentBodyTemperature = minBodyTemperature + random.NextDouble() * 4; // 36.5-40.5 deg    double currentPulseRate = minPulseRate + random.NextDouble() * 40; // 60-100 per min    double currentRespirationRate = minRespirationRate + random.NextDouble() * 4; // 12-16 per min    // Pretentiously received from on-board sensors    double currentTemperature = minRoomTemperature + random.NextDouble() * 12; // 18-30 deg    double currentHumidity = minRoomHumidity + random.NextDouble() * 30; // 30-60%    // Combined telemetry data    var deviceTelemetryData = new    {      messageId = Guid.NewGuid().ToString(),      deviceId = deviceId,      patientBodyTemperature = currentBodyTemperature,      patientPulseRate = currentPulseRate,      patientRespirationRate = currentRespirationRate,      rooomTemperature = currentTemperature,      roomHumidity = currentHumidity    };    // Serialize and send data to hub    var messageString = JsonConvert.SerializeObject(deviceTelemetryData);    var message = new Message(Encoding.ASCII.GetBytes(messageString));    await deviceClient.SendEventAsync(message);    // Output the sent message to console    Console.WriteLine("Message at {0}: {1}", DateTime.Now, messageString);    // Wait for 3 seconds before repeating    await Task.Delay(3000);      }}Let’s break down the code as before.We start by adding the required using statements:using System.Threading.Tasks;using Microsoft.Azure.Devices.Client;using Newtonsoft.Json;using System.Configuration;We create an instance of DeviceClient, the class that exposes methods to communicate with the hub. We also read app setting values into class fields.static DeviceClient deviceClient;static string iotHubHostname = ConfigurationManager.AppSettings["iotHubHostname"];static string deviceId = ConfigurationManager.AppSettings["deviceId"];static string deviceSharedAccessKey = ConfigurationManager.AppSettings["deviceSharedAccessKey"];In the SendPatientTelemetryToHubAsync method, we start by setting minimum values for telemetry parameters that will be recorded (simulated) by the device.double minBodyTemperature = 36.5; // degrees Celsiusdouble minPulseRate = 60; // beats per minutedouble minRespirationRate = 12

1.  1.生成假传感器数值。// 假装从医疗设备接收 double currentBodyTemperature = minBodyTemperature + random.NextDouble() * 4; // 36.5-40.5 度 double currentPulseRate = minPulseRate + random.NextDouble() * 40; // 60-100 每分钟 double currentRespirationRate = minRespirationRate + random.NextDouble() * 4; // 12-16 每分钟// 假装从板载传感器接收 double currentTemperature = minRoomTemperature + random.NextDouble() * 12; // 18-30 度 double currentHumidity = minRoomHumidity + random.NextDouble() * 30; // 30-60%

1.  2.构建遥测数据对象.var deviceTelemetryData = new{  messageId = Guid.NewGuid().ToString(),  deviceId = deviceId,  patientBodyTemperature = currentBodyTemperature,  patientPulseRate = currentPulseRate,  patientRespirationRate = currentRespirationRate,  rooomTemperature = currentTemperature,  roomHumidity = currentHumidity};

1.  3.序列化并发送数据至中枢.var messageString = JsonConvert.SerializeObject(deviceTelemetryData);var message = new Message(Encoding.ASCII.GetBytes(messageString));await deviceClient.SendEventAsync(message);

1.  4.等待 3000 毫秒（三秒）再重复。await Task.Delay(3000);

### 运行应用程序

在 Visual Studio 中将 SimulatedDevice 项目设置为启动项目，并按下键盘上的 F5 按钮（或 VS 中的启动按钮）来运行应用程序。一个命令提示符窗口将弹出，并每三秒显示我们在控制台上输出的消息。图 3-10 显示了示例输出。![A458845_1_En_3_Fig10_HTML.jpg](img/A458845_1_En_3_Fig10_HTML.jpg)图 3-10 模拟设备控制台应用程序的输出要验证消息是否成功发送到中心，请在 Azure 门户中打开中心的详细信息。您应该看到使用情况计数增加，如图 3-11 所示。![A458845_1_En_3_Fig11_HTML.jpg](img/A458845_1_En_3_Fig11_HTML.jpg)图 3-11 每日使用情况-消息交换-可以在 Azure 门户中检查到

## 创建解决方案后端

我们已经创建了一个模拟客户端，从中发送了消息，并在 Azure 门户中验证了它们的计数。下一步是创建一个非常基本的解决方案后端，它可以：

+   在控制台中显示从设备接收到的消息（设备到云）

+   分析接收到的消息并做出决策

+   发送消息到另一台设备（云到设备）

+   通过通知中心向安卓手机发送推送通知

### 创建应用程序

与以前一样，我们将创建解决方案后端作为控制台应用程序。在 Visual Studio 中，将一个新的控制台应用程序项目命名为 SolutionBackend，添加到 IoTCentralizedPatientMonitoring 解决方案中。

#### 创建通知中心

这样做类似于创建 IoT Hub。在 Azure 门户上，转到 New ➤ Web+Mobile ➤ Notification Hubs。 如图 3-12 所示创建一个新的 Hub。![A458845_1_En_3_Fig12_HTML.jpg](img/A458845_1_En_3_Fig12_HTML.jpg)图 3-12 在 Azure 中创建通知中心将你在这里使用的 Hub 名称记下，因为稍后会用到。Namespace 字段可以与 Hub 名称字段具有相同的值。在此练习中，选择免费版。它有一个慷慨的限制，可以发送 100 万条推送通知，并可注册 150 个设备（可以通过 Hub 发送通知）。Azure 通知中心支持所有主要设备平台发送通知 -iOS、Android、Windows、Windows Phone 等。在此练习中，我们将限制我们的推送通知仅发送到 Android 设备。向每个平台发送通知需要在 Hub 中进行单独的设置。对于 Android，我们需要一个 Google Cloud Messaging (GCM) API 密钥。如果您刚接触 Android 开发，通过标准流程获取您的密钥可能会很复杂。我们将通过使用 Firebase 的方式来进行快捷操作。跳转到[`firebase.google.com`](https://firebase.google.com)并创建您的免费帐户。在控制台页面上，创建一个新项目（名称不重要）。在新创建的项目中，找到项目设置选项。在设置页面上，切换到 Cloud Messaging 选项卡，并复制传统服务器密钥的值。图 3-13 显示了项目设置页面。![A458845_1_En_3_Fig13_HTML.jpg](img/A458845_1_En_3_Fig13_HTML.jpg)图 3-13 在 Firebase 中查找 GCM 的 API 密钥一旦 Azure 完成创建我们的通知中心，转到 Notification Settings ➤ Google (GCM)。粘贴我们上面复制的密钥到 API Key 文本框中，如图 3-14 所示。![A458845_1_En_3_Fig14_HTML.jpg](img/A458845_1_En_3_Fig14_HTML.jpg)图 3-14 在通知中心中设置 GCM API 密钥以允许其向 Android 设备发送消息

#### 添加依赖项

我们需要三个 NuGet 包 —— Microsoft.ServiceBus.Messaging（用于读取设备到云的消息）、Microsoft.Azure.Devices（用于发送云到设备的消息）和 Microsoft.Azure.NotificationHubs（用于发送推送通知）。通过 NuGet 包管理器为此项目安装它们。与往常一样，我们还需要在 App.config 中引用应用程序设置。因此，在所有依赖项安装完成后，在 Program.cs 的顶部添加以下 using 语句：using Microsoft.ServiceBus.Messaging;using Microsoft.Azure.Devices;using Microsoft.Azure.NotificationHubs;using Newtonsoft.Json;using System.Configuration;

#### 添加应用程序设置

在 App.config 中添加以下设置：<add key="connectionString" value="" /><add key="deviceToCloudEndPoint" value="messages/events" /><add key="receiverDeviceId" value="alarmdevice-patient1" /><add key="notificationHubName" value="" /><add key="notificationHubConnectionString" value="" />connectionString 将是我们在“创建 IoT Hub”部分中记录的内容。notificationHubName 将是我们刚才在“创建通知中心”小节中记录的内容。要检索 notificationHubConnectionString 的值，请在您的通知中心的 Azure 门户页面上转到 Access Policies ➤ DefaultFullSharedAccessSignature 并复制连接字符串。

#### 添加初始化设置

在 Program.cs 中添加以下静态字段：static EventHubClient eventHubClient;static ServiceClient serviceClient;static NotificationHubClient notificationHubClient;static string connectionString = ConfigurationManager.AppSettings["connectionString"];static string deviceToCloudEndPoint = ConfigurationManager.AppSettings["deviceToCloudEndPoint"];static string receiverDeviceId = ConfigurationManager.AppSettings["receiverDeviceId"];static string notificationHubName = ConfigurationManager.AppSettings["notificationHubName"];static string notificationHubConnectionString = ConfigurationManager.AppSettings["notificationHubConnectionString"];在 Main 方法中进行初始化，如下所示。// 初始化事件中心客户端以接收设备到云消息 eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, deviceToCloudEndPoint);// 初始化服务客户端以发送云到设备消息 serviceClient = ServiceClient.CreateFromConnectionString(connectionString);// 初始化通知中心客户端以发送云到移动端推送通知 notificationHubClient = NotificationHubClient.CreateClientFromConnectionString(notificationHubConnectionString, notificationHubName);

#### 从设备接收消息

让我们为接收连接设备（在我们的情况下仅限医疗设备）发送到 IoT Hub 的消息创建一个新的方法。private static async Task ReceiveMessagesAsync(string partition){  // 创建一个接收器，从给定的分区开始读取消息，从给定的日期时间开始  var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);  // 开始接收消息  while (true)  {    EventData eventData = await eventHubReceiver.ReceiveAsync();    if (eventData == null) continue;    // 提取消息    string serializedMessage = Encoding.UTF8.GetString(eventData.GetBytes()); // 序列化的 JSON 字符串    // 在控制台上显示消息    ShowMessageOnConsole(serializedMessage);    // 分析消息    AnalyzeMessage(serializedMessage);  }}在无限循环中，我们不断地检查中心上的传入消息。我们可以对接收到的消息执行各种操作。在我们的代码中，我们将它们写入控制台，然后执行基本分析以做出决策。重要的是要注意，消息以序列化的 JSON 字符串接收，因为我们在 SimulatedDevice 项目中发送它们。ShowMessageOnConsole() 方法简单到超乎你的想象：private static void ShowMessageOnConsole(string message){  Console.WriteLine();  Console.WriteLine("Message received: " + message);}我们稍后再看 AnalyzeMessage() 方法。首先，让我们在 Main() 方法中连接接收消息方法。在 Main() 的末尾添加以下行:// 获取第一个分区 var firstPartition = eventHubClient.GetRuntimeInformation().PartitionIds[0];// 从医疗设备开始接收消息 ReceiveMessagesAsync(firstPartition).Wait();虽然 IoT Hub 的免费层（F1）允许两个分区，但我们正在阅读第一个分区以保持我们的代码简单。出于这种简单起见，我们牺牲了接收写入第二分区的消息。生产应用程序通常会有更多的分区（4 及以上）。

#### 分析接收到的消息

在 Program.cs 中添加以下方法：private static void AnalyzeMessage(string messageJSONString){  // 反序列化消息  var messageType = new  {    messageId = "",    deviceId = "",    patientBodyTemperature = 0.0d,    patientPulseRate = 0.0d,    patientRespirationRate = 0.0d,    rooomTemperature = 0.0d,    roomHumidity = 0.0d  };  var message = JsonConvert.DeserializeAnonymousType(messageJSONString, messageType);  //  如果患者体温超过 102 华氏度：  //  1\. 向报警设备发送警报，通知医院工作人员  //  2\. 向注册手机发送推送通知，通知医生  if (message.patientBodyTemperature > 38.89)  {    Console.WriteLine("向患者的警报设备发送高体温警报。");    SendMessageToDeviceAsync(receiverDeviceId, "high-body-temp-alert").Wait();    Console.WriteLine("向通知中心发送高体温警报。");    SendPushNotificationAsync("警告：1 号房间的患者发高烧。").Wait();  }}代码基本上是不言自明的。由于接收到的消息是序列化的 JSON 字符串，我们在开始分析之前将其转换为 C# 对象。完成后，我们执行简单的分析，检查患者的体温。

#### 发送消息到设备

与 Azure IoT 设备 SDK 中的其他内容一样，向设备发送消息非常简单。private async static Task SendMessageToDeviceAsync(string deviceId, string message){  var commandMessage = new Message(Encoding.ASCII.GetBytes(message));  await serviceClient.SendAsync(deviceId, commandMessage);}在最后一节的 AnalyzeMessage() 方法中调用此方法。

#### 发送推送通知

向通知中心发送消息以进一步转发为推送通知同样简单。private async static Task SendPushNotificationAsync(string message){  await notificationHubClient.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"" + message + "\"}}");}

### 运行应用程序

我们的简易解决方案后端现已准备好进行测试。在运行之前，请验证 App.config 中的应用程序设置。不正确的应用程序设置值是问题的常见原因。为了能够测试解决方案后端，您需要同时运行 SimulatedDevice 项目。否则，后端将没有消息可以接收和分析。Visual Studio 提供了一种简单的方法来同时运行多个项目。在解决方案资源管理器中，右键单击解决方案 IoTCentralizedPatientMonitoring，然后选择属性。在公共属性 ➤ 启动项目 中，选择多个启动项目选项。将 SimulatedDevice 和 SolutionBackend 项目都设置为启动操作。点击确定以保存。点击运行按钮或按下 F5 键启动应用程序。现在两个项目应该同时运行。解决方案后端的示例输出显示在图 3-15 中。![A458845_1_En_3_Fig15_HTML.jpg](img/A458845_1_En_3_Fig15_HTML.jpg)图 3-15 模拟设备发送的消息由解决方案后端接收如您在图 3-15 中所见，有几次患者体温升高并发送警报到报警设备和通知中心。在下一节中，我们将在实际的 Raspberry Pi Zero 上编写并运行一个应用程序。那时您将能够看到从解决方案后端接收到的警报，通过 IoT Hub 路由。如果您想测试接收通知中心消息，您需要创建一个 Android 应用程序并在移动设备上运行它。为了节省您的时间和精力，Azure 团队已经为此创建了一个可立即使用的 Android 应用程序。访问 [`github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase`](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase) 了解更多信息。图 3-16 是我们的解决方案后端发送的推送通知在我们的 Android 手机上接收到的屏幕截图。![A458845_1_En_3_Fig16_HTML.png](img/A458845_1_En_3_Fig16_HTML.png)图 3-16Azure IoT Hub 演示 Android 应用程序通过通知中心接收的警报通知：（左）作为吐司形式的应用内通知和（右）手机通知区域中的消息提示 Tip 您可以在 Android 应用程序中编写额外的代码，使手机在收到警报通知时立即震动强烈并播放尖锐持续的铃声，以立即引起医生的注意。

## 为 Raspberry Pi 编写物联网应用程序

你一直在等待的东西已经到了。是时候让你的 Raspberry Pi 开始发挥作用了。观看物理设备做出了不可思议的事情的喜悦是无与伦比的。提示：如果你没有实体的 Raspberry Pi Zero，也没关系。Azure 的树莓派网络模拟器是在没有实体设备的情况下测试你的代码的好方法。它完全在浏览器中运行，有两个组成部分——左边是带有其电路配置的 Pi，右边是代码编辑器。截至撰写本书时，该模拟器处于早期预览阶段，并且不允许修改预配置的电路。但这可能会在未来发生变化。Pi 网络模拟器可在 [`azure-samples.github.io/raspberry-pi-web-simulator`](https://azure-samples.github.io/raspberry-pi-web-simulator) 上使用。本节的准备工作已经教会了你许多关于编写物联网设备应用程序的知识。你已经使用 Azure IoT 设备 SDK 创建了一个模拟设备。为实际设备开发将是类似的，因为你将使用相同的 SDK。但这次你将不是用 C# 而是用 JavaScript（使用 node.js）编写应用程序。这是因为 Linux 是 Pi 上最常见的操作系统。在 Linux 上运行 .NET 应用程序是可能的，通过 Mono，但是设置和维护它通常是棘手的。Python 和 node.js 是为 Pi 和其他几种物联网设备开发应用程序的流行选择。注意：本节中的说明不仅适用于 Pi Zero，还适用于所有其他型号的 Raspberry Pi，包括 Model 1 B+、2 和 3。

### 设置你的 Pi

如果你是 Raspberry Pi 的新手，并且以前没有进行过设置，Raspberry Pi 的官方文档是一个很好的起点。访问 [`www.raspberrypi.org/learning/software-guide`](https://www.raspberrypi.org/learning/software-guide) 开始。或者，在 Raspberry Pi 网站的帮助页面上找到软件安装指南。您将被指导：

+   选择合适的操作系统（Raspbian 是官方支持的 Linux 版本之一）

+   下载并安装操作系统到 microSD 卡上

+   连接 Pi 到 LAN 或 WiFi 网络等。

我们建议您安装 Raspbian。一旦您的 Pi 完全设置好，确保您有 SSH 访问权限和启用了 I2C 接口。这很容易，只需运行 raspi-config 命令；您将在 Pi 网站上找到详细的说明。

### 通过 SSH 连接到 Pi

有几种方法可以连接到 Pi，并在其上编写和部署软件。通过 SSH 进行远程访问是最常见和安全的方法。您也可以简单地连接显示器/电视和键盘到您的 Pi 上，并像在笔记本电脑上一样开始编码。或者，使用 VNC 或 xrdp 访问 Pi 的桌面。这两种方法都允许您连接 Pi 的图形界面，就像使用 RDP 连接到远程 Windows VM 时一样。通过 SSH 连接更快且需要更少的硬件。唯一的缺点是 SSH 仅允许命令行访问。您无法访问图形界面。但是，为什么担心呢？我们是开发者！我们喜欢编写代码和执行命令。在 Windows 中连接到 SSH，您需要第三方软件，如 PuTTY。从 [`www.putty.org`](https://www.putty.org) 下载并安装 PuTTY。在设置 Pi 时，您可能已经至少一次通过 SSH 连接到它。如果没有，请在 Pi 的文档中查找如何操作的说明。图 3-17 显示了通常如何通过 PuTTY 连接到 Pi，图 3-18 显示了连接后 Pi 的命令行界面。![A458845_1_En_3_Fig17_HTML.jpg](img/A458845_1_En_3_Fig17_HTML.jpg)图 3-17 通过 PuTTY 连接到 Pi 的过程![A458845_1_En_3_Fig18_HTML.jpg](img/A458845_1_En_3_Fig18_HTML.jpg)图 3-18 连接后的 Pi 的命令行界面

### 安装 node.js

Node.js 是 JavaScript 的服务器端实现。它提供了用于访问 I/O（文件、数据库等）和其他系统级资源的超快速 API。换句话说，Node 是一个应用服务器，用于运行基于 JavaScript 的应用程序。了解有关 Node 的更多信息，请访问[`nodejs.org`](https://nodejs.org)。在 Raspbian 中安装最新版本的 node.js 有多种方法。最好按照在[`nodejs.org`](https://nodejs.org)提到的官方安装说明进行操作。由于 Raspbian 是基于 Debian 的 Linux 操作系统，请按照通过软件包管理器（apt-get）安装 node 的说明操作。以下两个命令理想情况下应该能起作用：curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -sudo apt-get install -y nodejs 要验证 node 是否正确安装，请运行此命令：node -v 如果一切正常，你应该会得到一个输出，例如 v9.5.0。如果此方法不起作用，请转到 nodejs.org 的下载页面，并下载与您的 Pi 型号相对应的 Linux 二进制（ARM）包。例如，对于 Pi Zero，您需要下载 ARMv6 包：wget https://nodejs.org/dist/v9.5.0/node-v9.5.0-linux-armv6l.tar.xz 接下来，将下载的 tarball 存档解压到一个全局可访问的位置。运行以下三个命令：sudo mkdir /usr/lib/nodejssudo tar -xJvf node-v9.5.0-linux-armv6l.tar.xz -C /usr/lib/nodejssudo mv /usr/lib/nodejs/node-v9.5.0-linux-armv6l /usr/lib/nodejs/node-v9.5.0 将上述目录永久添加到您的 PATH 环境变量中。在文本编辑器中打开 .profile 文件：nano ~/.profile 然后在文档末尾添加以下行：export NODEJS_HOME=/usr/lib/nodejs/node-v9.5.0export PATH=$NODEJS_HOME/bin:$PATH 最后，刷新您的 PATH：. ~/.profile

### 创建应用程序

创建一个新目录来存储应用程序，并进入该目录：mkdir AlarmDevice，cd AlarmDevice。将此目录初始化为一个节点应用程序：npm init。系统会询问一系列问题，在最后将生成一个名为 package.json 的新文件。

#### 安装依赖项

现在，安装 Azure IoT 设备 SDK 的依赖项。这一步类似于在 Visual Studio 中安装 NuGet 包。运行以下命令：npm install --save az-iot-bi, azure-iot-device, azure-iot-device-mqtt, wiring-pi。这将在一个名为 node_modules 的新文件夹中安装所需的依赖项，并更新 package.json 文件。我们最终的 package.json 文件如下所示：

#### 连接执行器

在警报设备中我们可以使用的最简单的执行器是 LED，它可以提供有关事件的视觉指示。LED 价格便宜且非常容易获得。我们将把一个红色 LED 连接到我们的 Pi Zero 的 GPIO。您可以做同样的事情或者连接声音设备，如蜂鸣器。连接方式基本保持不变。GPIO 引脚有两种模式 —— 输入模式（用于传感器）和输出模式（用于执行器）。在输出模式下，通过代码可以将引脚的电压设置为高（1）或低（0）以打开或关闭执行器。虽然最近的 Pi 型号上有 40 个 GPIO 引脚，但并非所有引脚都可用于传感器和执行器。此外，还有多个引脚编号系统。访问 [`pinout.xyz/pinout/wiringpi`](https://pinout.xyz/pinout/wiringpi) 查看 Pi Zero 的引脚布局。由于我们使用 wiring-pi 节点模块与引脚交互，所以我们将遵循其编号系统。将 LED 连接到地线和引脚 15。这些是第一行中从左数起的第三和第四个引脚。LED 的短腿（阴极，-ve）将插入地线，长腿（阳极，+ve）将插入引脚 15，如图 3-19 所示。![A458845_1_En_3_Fig19_HTML.jpg](img/A458845_1_En_3_Fig19_HTML.jpg)图 3-19 我们的 Pi Zero 的电路布局。LED 连接到引脚 15（WiringPi 标记）

#### 编写代码以接收消息并采取行动

在当前目录中创建一个名为 index.js 的新文件：nano index.js，并粘贴以下代码：

#### 运行应用程序

使用以下命令运行应用程序：node index.js 如果连接到 IoT Hub 成功，您将在控制台中看到消息“已连接到 IoT Hub”。此时，警报设备正在监听传入的消息。再次启动 Visual Studio，打开 IoTCentralizedPatientMonitoring 解决方案，并运行它。确保 SimulatedDevice 和 SolutionBackend 项目都设置为启动项目。当解决方案后端遇到高体温条件时，它将向警报设备发送警报消息。等待此条件发生。当发生时，返回 PuTTY 并检查警报消息（见图 3-20）。不要忘记在每个警报时检查 LED 灯是否闪烁。![A458845_1_En_3_Fig20_HTML.jpg](img/A458845_1_En_3_Fig20_HTML.jpg)图 3-20 在 Pi 上运行的 node.js 应用程序的控制台输出恭喜。您已成功创建了您的第一个 IoT 网络，其中包含功能设备和解决方案后端！

## 总结

我们意识到这是一个大章节，需要掌握很多内容。但到最后，您已经能够编写 IoT 应用程序并创建自己的网络。您学会了如何：

+   获取 Azure 订阅以使用 IoT 套件服务

+   在 Azure 门户中创建一个 IoT Hub

+   通过代码和门户在 Hub 中注册设备

+   使用 Azure IoT 设备 SDK 创建一个模拟设备，该设备向 Hub 发送遥测数据

+   创建一个接收设备消息、分析消息并发送消息到另一个 IoT 设备的解决方案后端

+   使用 Azure 通知中心服务发送推送通知

+   为真实的 IoT 设备（树莓派 Zero）编写应用程序

在下一章中，您将了解 AI 2.0 应用程序的另一个关键因素——人工智能。
