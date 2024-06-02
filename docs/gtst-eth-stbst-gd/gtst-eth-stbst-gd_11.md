© 作者，独家许可给 APress Media，LLC，Springer Nature 的一部分 2022 年 D. P. Bauer 使用以太坊入门 [`doi.org/10.1007/978-1-4842-8045-4_11`](https://doi.org/10.1007/978-1-4842-8045-4_11)

# 11. Nethereum

Davi Pedro Bauer^(1  )(1)Campo Bom, Rio Grande do Sul, Brazil

Nethereum^(1) 是一个用于以太坊的开源 .NET 集成库，简化了智能合约的维护和与公共和私有以太坊节点的交互。该框架公开了一个 Web3 类，在该类中可以与钱包或智能合约的方法进行交互。在本章中您将看到的示例中，您将使用钱包的 GetBalance 方法来查找其余额。

在本章结束时，您将能够执行以下操作：

+   使用 dotnet 创建一个新的控制台项目

+   创建一个使用 Nethereum 获取钱包余额的方法

+   在控制台中显示结果

## 使用 Nethereum 获取您的以太币余额

让我们从创建一个新的控制台项目并将 Nethereum Web3 包添加到我们的应用程序开始。然后，您将创建一个将获取特定钱包地址的余额的方法。最后，您将以 wei 和以太的形式将此信息打印到控制台上。

### 创建项目

转到终端并单击新终端。根据以下方式创建一个新的 dotnet 控制台项目。此命令基于指定的模板创建新项目、配置文件或解决方案：$ dotnet new console -o sample 转到项目的根目录。$ cd sample

### 安装 Web3

安装 Nethereum Web3 包。此命令将向项目文件添加包引用：$ dotnet add package Nethereum.Web3 恢复所有项目包。此命令将恢复项目的依赖项和工具：$ dotnet restore

### 创建方法

打开 Program.cs 文件并添加线程和 Web3 的引用。现在，添加一个新方法来获取账户余额，然后实例化一个新的 Web3 对象。

转到您的 Infura 项目设置，并选择 Ropsten 网络。复制 Ropsten https 端点（图 11-1）。![](img/521550_1_En_11_Fig1_HTML.jpg)

Infura 项目密钥截图显示左上角的项目 ID，右上角的项目密钥和条形码，选择了 Ropsten 选项的端点以及下方提供的 2 个链接，旁边有可点击的复制图标。

图 11-1

Infura 项目密钥

作为 Web3 对象构造函数的参数使用此端点。在 Program.cs 文件中，使用您钱包的公共地址作为参数从 Web3 获取余额。编写代码以以 wei 输出余额，然后将 wei 余额转换为 ether。最后，编写代码以以 ether 输出余额。现在，更改您的主方法以调用 GetAccountBalance()。using System;using System.Threading.Tasks;using Nethereum.Web3;namespace NethereumSample{    class Program    {        static void Main(string[] args)        {            GetAccountBalance().Wait();            Console.ReadLine();        }        static async Task GetAccountBalance()        {            var web3 = new Web3("https://ropsten.infura.io/v3/39180531508b4b659780ef7a36426a86");            var balance = await web3.Eth.GetBalance.SendRequestAsync("0x03d1b3162DBFaB4A175038eAa4EA4b39423d5A6F");            Console.WriteLine($"以 Wei 表示的余额：{balance.Value}");            var etherAmount = Web3.Convert.FromWei(balance.Value);            Console.WriteLine($"以 Ether 表示的余额：{etherAmount}");        }    }}

### 获取余额

构建项目。此命令构建项目及其所有依赖项：$ dotnet build 运行项目。此命令运行源代码，无需任何显式编译或启动命令：$ dotnet run 检查终端输出，并确保您得到图 11-2 中显示的结果！[](../images/521550_1_En_11_Chapter/521550_1_En_11_Fig2_HTML.jpg)

在这个 V S code 的屏幕截图中，以 Wei 和以太坊为单位的余额显示。选择了 Program dot c s 文件，并打开了终端选项卡。在相同的细节中，Wei 余额和以太余额在命令：美元符号点 net run 下方的窗口中显示。命令中的点和 net 之间没有空格。

图 11-2

V S code 中以 wei 和 ether 为单位的余额

## 概要

在本章中，您学习了如何使用 Nethereum 创建一个获取钱包余额的控制台项目。
