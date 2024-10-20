# 用 Visual Studio 代码调试 Chainlink

> 原文：<https://blog.chain.link/debugging-chainlink-with-visual-studio-code/>

本指南面向那些可能是新开发人员，或者刚刚接触 Golang 的人。调试是编程的一个重要部分，可以极大地增强您对正在工作的系统的理解。在本指南中，您将了解如何设置 Visual Studio 代码以使用 Golang 语言。VS Code 是一个轻量级的图形代码编辑器，允许安装扩展(插件)来添加功能，类似于 [Atom](https://atom.io/) 和 [Sublime Text](https://www.sublimetext.com/) 。

## 要求

*   Chainlink 的完整开发环境
*   [钻研](https://github.com/derekparker/delve)
*   [Visual Studio 代码](https://code.visualstudio.com/)

## 设置 Visual Studio 代码

#### 安装 Go 扩展

启动 VS 代码快速打开( *Ctrl+P* )运行: *ext install Go* 。这将把你带到扩展市场，在那里你可以安装 Go 扩展。安装完成后，点击重新加载按钮，界面会短暂刷新。

要打开 Chainlink 项目，键入 *Ctrl+K* *Ctrl+O* 调出打开文件夹对话框。导航到您的*$ GOPATH/src/github . com/smartcontractkit/chain link*目录并打开它。

选择根目录中的 *main.go* 文件，注意屏幕右下角会出现一个对话框。单击“全部安装”按钮。这将在 VS 代码中安装 [Go 工具](https://github.com/Microsoft/vscode-go/wiki/Go-tools-that-the-Go-extension-depends-on)，使得阅读代码和开发更加容易。

#### 设置启动参数

键入 *Ctrl+Shift+D* 调出调试控件，点击左上角附近的齿轮图标，配置一个 *launch.json* 。要针对 [DevNet 运行 Chainlink 节点，](https://github.com/smartcontractkit/devnet)您可以使用以下选项，方法是将下面的文本复制并粘贴到整个文件中(您需要用您部署的 LinkToken 契约的地址替换 *LINK_CONTRACT_ADDRESS* )。

```
    "version": "0.2.0",
    "configurations": [
        {
            "name": "DevNet",
            "type": "go",
            "request": "launch",
            "mode": "debug",
            "remotePath": "",
            "port": 2345,
            "host": "127.0.0.1",
            "program": "${workspaceRoot}",
            "env": {
                "LOG_LEVEL": "debug",
                "ROOT": "./internal/devnet",
                "ETH_URL": "ws://localhost:18546",
                "ETH_CHAIN_ID": 17,
                "TX_MIN_CONFIRMATIONS": "0",
                "TASK_MIN_CONFIRMATIONS": "0",
                "USERNAME": "chainlink",
                "PASSWORD": "twochains",
                "LINK_CONTRACT_ADDRESS": "0x83e41643c2598c4d6a78d68cf506bf209a22ba5d"
},
            "args": ["node", "-p", "T.tLHkcmwePT/p,]sYuntjwHKAsrhm#4eRs4LuKHwvHejWYAC2JP4M8HimwgmbaZ"],
            "showLog": true
        }
    ]
}
```

保存后，您会注意到一个新文件夹*。vscode* 是在项目的根目录下创建的。您需要确保将它添加到您的全局 [gitignore](https://help.github.com/articles/ignoring-files/#create-a-global-gitignore) 中，以便在您创建拉请求时不包含它。

## 在调试模式下运行

首先，您需要在 DevNet 映像的窗口中运行它。

```
*$ cd $GOPATH/src/github.com/smartcontractkit/chainlink*
*$ ./internal/bin/devnet*
```

然后，回到 Visual Studio 代码，通过点击 *F5* 或点击左上角调试窗口中的“play”图标开始调试。如果成功，您应该会在底部的“Debug Console”选项卡上看到与在终端窗口中运行 Chainlink 节点相同的输出。

您还会看到一个在项目根目录下创建的*调试*文件。你会想把它添加到你的全球*。gitignore* 也一样。

## 断点

为了单步执行代码，您需要在想要开始单步执行的地方设置一个断点。为此，首先要通过单击屏幕顶部的“停止”按钮来停止调试正在运行的程序。然后，找到你希望程序暂停执行的一行。理解运行流程的一个很好的起点是在带有 *BuildRun* 函数的 *services/job_runner.go* 文件中。你可以点击那一行的任何地方，然后点击键盘上的 *F9* 按钮，或者点击行号旁边的红点来添加断点。重复这些相同的步骤来删除断点。

现在，再次启动该节点，如果没有作业，则添加一个作业。您可以使用此工作规范开始:

```
*$ chainlink c '{"initiators":[{"type":"web"}],"tasks":[{"type":"HttpGet","url":"https://min-api.cryptocompare.com/data/price?fsym=LINK&tsyms=USD"},{"type":"JsonParse","path":["USD"]},{"type":"noop"}]}'*
```

然后记下顶部表格中返回的“ID”字段的值。您可以通过运行以下命令在终端选项卡中开始运行(用您的实际作业 ID 替换 *$JOBID* ):

```
*$ chainlink r $JOBID*
```

VS 代码应该在 *BuildRun* 函数处暂停。你可以通过点击键盘上的 *F10* 按钮来单步执行代码，而 *F11* 将允许你“单步执行”功能。请注意，Debug 选项卡上的面板 Variables 和 Call Stack 已经填充了关于正在运行的程序的信息。只需在调试控制台的 *>* 提示符下键入变量名，并按 Enter 键以获得关于变量的更多信息，但是您可能希望单击胡萝卜来展开属性。您还可以通过在调试控制台选项卡中查询变量来获取更多信息。

例如:

```
*> job.Initiators[0] # hit enter <github.com/smartcontractkit/chainlink/store/models.Initiator> ID:0 JobID:"1f0daf1b11664da89b9675dc05a4b993" Type:"web" Schedule:"" Time:<github.com/smartcontractkit/chainlink/store/models.Time> Ran:false Address:<github.com/smartcontractkit/chainlink/vendor/github.com/ethereum/go-ethereum/common.Address>*
```

当你想让程序恢复正常时，点击 *F5* 按钮。

* * *

希望本指南对您有用，并帮助您调试和添加功能到 [Chainlink](https://github.com/smartcontractkit/chainlink) ！如果您有任何问题，请随时在我们的 Slack 上提出(电子邮件 [【电子邮件保护】](/cdn-cgi/l/email-protection#c8bbbdb8b8a7babc88bba5a9babcaba7a6bcbaa9abbce6aba7a5) 访问)或 [Gitter](https://gitter.im/smartcontractkit-chainlink/Lobby) 。