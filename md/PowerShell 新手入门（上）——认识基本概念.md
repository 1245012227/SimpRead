> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [sspai.com](https://sspai.com/prime/story/powershell-primer-01)

> 本文将为读者介绍 PowerShell 的安装使用、基本概念和初步用法，希望为读者认识和进一步学习这个有价值的工具提供一个入门指引。

引言
--

在大多数 Windows 用户的心目中，Windows 似乎就是图形界面（GUI）操作系统的代名词。的确，历史上，图形界面虽然不是由 Windows 首创，但确实是随着 Windows 的普及而广为人知。同时，图形化界面有着易用易上手的特性，绝大部分的日常工作已经不再需要通过命令行来进行。

不过，对于那些追求高效率的用户而言，命令行在执行批量处理、系统维护等任务时，仍然有着无法替代的优势。用一行命令可以解决的问题，鼠标点击往往要花上多步；一些高级操作更是只能通过命令来调节。

事实上，命令行不仅一直是 Windows 的内置功能，而且还伴随着它一起进化：从最初的 COMMAND.COM，到 NT 时代的命令提示符，再到面向未来的 PowerShell。如今，用 PowerShell 不仅可以执行各种系统命令和设置操作，还可以进行脚本编程，执行自动化任务等各种高级操作，与 Unix 阵营的命令行相比丝毫不落下风。

本文将为读者介绍 PowerShell 的安装使用、基本概念和初步用法，希望为读者认识和进一步学习这个有价值的工具提供一个入门指引。

PowerShell 的安装与启动
-----------------

PowerShell 最早推出于 2006 年，从 2.0 版本起内置在当时的 Windows 7 中，随后在每一代的 Windows 里都会预装。

从 2016 年的 6.0 版本起，PowerShell 已经成为了一个跨平台的命令行界面，支持了 Linux 和 macOS 操作系统，也随之去掉了名字里「Windows」的前缀。

Windows 预装的 PowerShell 版本并不是最新的。对于大多数人使用的 Windows 10 或 Windows 11 而言，内置的版本为 Windows PowerShell 5.1——最后一个专为 Windows 系统设计的版本。而目前最新的 PowerShell 是 7.x 版，在与旧版基本兼容的基础上，增加了一些语法和内置命令，但就日常使用而言差异不大。

因此，如果你使用现代版本的 Windows 系统，无需额外安装更新也可以继续阅读；考虑到通用性，本文仍将以内置的 5.1 版本为例演示。但如果你希望使用新版，也可以通过以下任意方式安装，它会与内置的旧版共存，互不干扰：

*   从 [Microsoft 商店](https://www.microsoft.com/store/apps/9MZ1SNWT0N5D)安装
*   下载 [`.msi` 安装包](https://github.com/PowerShell/PowerShell/releases/)
*   使用 `winget` 包管理器安装：`winget search Microsoft.PowerShell`

（更多安装方法可参阅[官方文档](https://docs.microsoft.com/zh-cn/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.2)）

PowerShell 可以通过开始菜单中的「Windows PowerShell」（对于内置版本）或者「PowerShell 7」（对于单独安装的新版）选项启动，但这种启动方式是通过比较简陋的 [Windows Console](https://en.wikipedia.org/wiki/Windows_Console) 窗口运行，不够美观也缺少一些常用功能。

因此，我们建议通过较为现代的 Windows Terminal（内置于 Windows 11 和较新的 Windows 10 中，也可从[商店](https://www.microsoft.com/zh-cn/p/windows-terminal-preview/9n8g5rfz9xk3)或 [GitHub](https://github.com/microsoft/terminal#other-install-methods) 安装）来和 PowerShell 打交道；后文也将以此为演示环境。

如上所述，PowerShell 也支持 macOS 和 Linux 系统，安装方式则各有差异，有兴趣的读者可以直接参阅官方的详细说明：[在 macOS 上安装 PowerShell](https://docs.microsoft.com/zh-cn/powershell/scripting/install/installing-powershell-on-macos?view=powershell-7.2)、[在 Linux 上安装 PowerShell](https://docs.microsoft.com/zh-cn/powershell/scripting/install/installing-powershell-on-linux?view=powershell-7.2)。

PowerShell 的基础概念
----------------

### PowerShell 的命令与别名

作为一个命令行界面，PowerShell 交互的基础自然是命令，这在 PowerShell 中被称作是 cmdlet。

在 Bash 等传统 shell 环境中，命令的名称大多是单个「词语」，并且很多因为历史原因和「黑客」习惯而难以理解。相比之下，cmdlet 基本上都是使用「动词–名词」的固定形式，这使得输入命令更像是英语的正常表达。

例如，想要确定当前运行了哪些进程，那么就使用 `Get-Process`；如果想要知道当前系统的服务状态列表，那么就使用 `Get-Service`——是不是很像写一个英语短语？

不过，虽然「动词—名词」的命令结构非常容易理解，但相应的缺点就是有点「啰嗦」，对于熟悉了 Unix 阵营终端的用户也有些陌生。

对此，PowerShell 的解决方案是引入一系列「别名」（alias），可以理解为命令的简短「昵称」，这样记忆和输入起来都更方便。

我们可以使用 `Get-Alias` 命令来获取 PowerShell 内置的命令和别名对应关系表：

```
CommandType     Name                  Version    Source
-----------     ----                  -------    ------
Alias           ? -> Where-Object
Alias           % -> ForEach-Object
Alias           cd -> Set-Location
Alias           chdir -> Set-Location
...
```

如果想要知道某个具体命令对应的别名，那么可以使用 `-Definition` 参数。例如，想筛选出复制文件命令 `Copy-Item` 的别名，可以运行：

```
Get-Alias -Definition Copy-Item
```

从输出结果：

```
CommandType     Name                 Version    Source
-----------     ----                 -------    ------
Alias           copy -> Copy-Item
Alias           cp -> Copy-Item
Alias           cpi -> Copy-Item
```

可以看出 `cp`、`cpi` 和 `copy` 都是 `Copy-Item` 的简化写法。

下面的表格列举了一些常用操作的原名和别名：

<table><thead><tr><th>命令</th><th>别名</th><th>功能</th></tr></thead><tbody><tr><td>Get-ChildItem</td><td>gci, dir, ls</td><td>列出所有文件和文件夹</td></tr><tr><td>Test-Connection</td><td>ping</td><td>发送 Ping</td></tr><tr><td>Get-Content</td><td>gc, type, cat</td><td>获取文件内容</td></tr><tr><td>Get-Help</td><td>help, man</td><td>在控制台上打印命令的文档</td></tr><tr><td>Clear-Host</td><td>cls, clear</td><td>清除屏幕</td></tr><tr><td>Copy-Item</td><td>cpi, copy, cp</td><td>复制文件和文件夹</td></tr><tr><td>Move-Item</td><td>mi, move, mv</td><td>移动文件和文件夹</td></tr><tr><td>Remove-Item</td><td>ri, del, erase, rmdir, rd, rm</td><td>删除文件或文件夹</td></tr><tr><td>Rename-Item</td><td>rni, ren, mv</td><td>重命名文件、文件夹等</td></tr><tr><td>Get-Location</td><td>gl, cd, pwd</td><td>显示工作路径（目前文件夹）</td></tr><tr><td>Set-Location</td><td>sl, cd, chdir</td><td>改变工作路径</td></tr><tr><td>Write-Output</td><td>echo, write</td><td>打印字符串</td></tr><tr><td>Get-Process</td><td>gps, ps</td><td>列出进程</td></tr><tr><td>Stop-Process</td><td>spps, kill</td><td>停止进程</td></tr><tr><td>Set-Variable</td><td>sv, set</td><td>创建或更改环境变量</td></tr></tbody></table>

可以看出，预置的别名基本都是在复刻 Unix 类终端和 Windows 传统终端「命令提示符」的对应命令；这有助于习惯其他终端环境的用户快速迁移。

除了直接使用内置的命令别名之外，我们也可以通过 `New-Alias` 命令，为任意命令创建别名。

例如，我们希望给 `Get-Process` 命令创建 `gpr` 的别名，那么就可以运行：

```
New-Alias -Name gpr -Value Get-Process
```

创建完成，我们直接在当前的 PowerShell 窗口中输入 `gpr`，其打印结果和 `Get-Process` 是基本一样的。

不过这个创建的新别名只能用在当前会话（终端窗口）中，如果想要在其他会话中使用别名，那么就需要将创建的别名保存到 PowerShell 的配置文件中，或者使用 `Export-Alias` 将别名保存到文件中。

### 管道：将命令串联起来

管道（pipe）是命令行环境的一大魅力所在。所谓管道，简言之是将命令串联起来的方式，就像工厂里的流水线一样，前一个命令的结果可以通过管道符号（`|`）发送到下一个命令中继续处理。

例如，下面的命令作用是获取 Edge 浏览器进程，然后将其停止：

```
Get-Process msedge | Stop-Process
```

这里，第一个命令就是获取当前的系统进程并选中目标对象 `msedge`，之后通过管道符号（`|`）将目标进程对象送到 `Stop-Process`，由后者完成停止操作。

还可以通过管道将一些本机命令输出内容传递给其他命令进一步处理。例如，`systeminfo.exe` 是用于输出系统信息的工具，但默认状态下输出的内容太多，不便查找。而通过类似下面的用法：

```
systeminfo.exe | Select-String -Pattern '^OS'
```

就可以将以「OS」开头的条目过滤出来：

```
OS Name:                   Microsoft Windows 10 Pro for Workstations
OS Version:                10.0.19044 N/A Build 19044
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Workstation
OS Build Type:             Multiprocessor Free
```

管道的用法还有很多，大家也可以根据实际的操作掌握情况融会贯通，也可以查看微软提供了管道相关的帮助[文档](https://docs.microsoft.com/zh-cn/PowerShell/module/microsoft.PowerShell.core/about/about_pipelines?view=PowerShell-5.1)来实现更高级的用法。

### 函数：快速完成繁复任务

和很多 Shell 语言一样，我们同样也可以使用 PowerShell 编程来解决更为复杂的工作，这就涉及函数的使用。

作为入门，这里还是用 Hello World 做演示。下面，我需要创建一个简单的函数，函数名为 `sspai-demo`，在使用 PowerShell 执行这个函数时输出「Hi, SSPAI!」：

```
function Greet-SSPAI {
    "Hi, SSPAI!"
}
```

编写完成之后，在 PowerShell 中输入 `Greet-SSPAI`，就会看到它向少数派的问好。

当然，函数的价值在于可以接收用户的输入。例如，想要输入一个用户名称，然后显示对应的问候语，那么可以使用类似下面的语法：

```
function Intro-SSPAI($guest)
{
    "$guest, welcome to SSPAI!"
}
```

这样，执行：

```
Intro-SSPAI "化学心情下 2"
```

就可以看到输出：

```
化学心情下 2, welcome to SSPAI!
```

### 对象：PowerShell 的核心特征

如果你熟悉了 Unix 类系统下的终端相比，看到这里可能觉得 PowerShell 只是换了换语法。然而，PowerShell 与 Bash 等环境有一个本质不同：处理的不是「文本」则是「对象」。

如果你对编程有一定了解，那么这种差异带来的优势无需多解释。如果对这个概念比较陌生，可以认为 PowerShell 中输出的任何结果都是「一体多面」的，可以像魔方一样展示出更多侧面，或者灵活变形；这为组合命令、过滤和处理命令输出结果带来了很大便利。

例如，一个最简单的命令

```
echo "Hello World"
```

在 Bash 中只是打印出「Hello World」这串字符。如果想知道它的长度，或者做切割、查找替换等进一步处理，就必须依赖其他命令（或者依赖于 shell 所提供的特定语法）。

但在 PowerShell 下，同一行命令得到的就是一个字符串「对象」，它本身就记录了自己的长度，只要通过

```
"Hello World".Length
```

就可以显示出来。

事实上，PowerShell 中任何命令的输出都是一个对象，取决于所属类型，它们各有不同的属性（property）和方法（method）。例如，Get-Process 命令找出的进程对象记录了自身的名称、编号，可以调用终止、刷新等方法来控制；而注册表键则会具有路径、值等属性，以及修改、删除等方法。

这种以对象为中心的特征，让 PowerShell 相比于 Unix shell 更接近于高级编程语言，在编写复杂命令或脚本时能带来很大的便利，节约处理纯文本、与特殊字符作斗争的时间。

### 请教 PowerShell 的帮助系统

PowrShell 中包含了形形色色的 cmdlet，显然我们不可能像是被英语单词那样把他全部记下来，而是在需要用到的时候去检索帮助来如何使用。

和在 Unix 终端下可以使用 `man` 命令查询帮助手册类似，PowerShell 同样也提供了一个相当强大的帮助系统，因此对于初学者而言，「遇事不决先问帮助」是快速掌握并使用 PowerShell 的关键。

首次查询 PowerShell 的帮助前，需要将帮助内容下载到本地。为此，运行：

```
Update-Help
```

在完成之后，我们就可以使用 `Get-Help`（或更广为人知的别名 `man`）来查询指定的命令了，比如说你想要查询的是 `Get-Process` 的用法，那么就在 PowerShell 中输入：

```
Get-Help -Name Get-Process
```

PowerShell 打印出来的就是 `Get-Process` 详细介绍，分别为名称、摘要、语法、说明、相关链接以及备注：

```
NAME
    Get-Process

SYNOPSIS
    Gets the processes that are running on the local computer.


SYNTAX
    Get-Process [[-Name] <System.String[]>] [-FileVersionInfo] [-Module]
    [<CommonParameters>]
...


DESCRIPTION
    The `Get-Process` cmdlet gets the processes on a local or remote computer.
...
```

你还可以在上述命令之后增加各种参数来查阅更具体的信息，例如，`-Examples` 可以查阅用法指导，`-Detailed` 可以进一步查阅细节说明，`-Online` 可以跳转到在线版本帮助等。

上面提到的是针对某一个已知的命令来查看命令的详细使用方法，那么如果只是知道某个命令的关键字，那么可以通过如下语法来查找包含这一关键字的命令：

```
Get-Help Process
```

得到结果如下：

```
Name                              Category  Module                    Synopsis
----                              --------  ------                    --------
Enter-PSHostProcess               Cmdlet    Microsoft.PowerShell.Core Connects to and enters into an interactive session with a local process.
Exit-PSHostProcess                Cmdlet    Microsoft.PowerShell.Core Closes an interactive session with a local process.
Get-PSHostProcessInfo             Cmdlet    Microsoft.PowerShell.Core Gets process information about the PowerShell host.
...
```

[下篇](https://sspai.com/prime/story/powershell-primer-02)中，我们将继续了解用 PowerShell 进行目录和文件操作、管理服务和进程、安装应用等具体操作方法。