> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/JimsZack/article/details/122125036)

Files - File Manager for Windows（files-community）卸载完全指北
=======================================================

问题 1
----

在应用商店里面安装了之后，点击实验性的

![](https://img-blog.csdnimg.cn/img_convert/a5bbd264839636f086a9b1ea740135dc.png)

在卸载又安装之后就会出现神奇的一幕。

![](https://img-blog.csdnimg.cn/7f25ae5274714d699680a475dcf4bbd1.gif#pic_center)

它自动化了。。。。

于是再次卸载按下 Win+E 出现这个

> 找不到应用程序

![](https://img-blog.csdnimg.cn/img_convert/dbd42172f0c572904015b700522c8d2c.png)

解决方法：

将下面文件保存为. reg 文件，然后改回[注册表](https://so.csdn.net/so/search?q=%E6%B3%A8%E5%86%8C%E8%A1%A8&spm=1001.2101.3001.7020)。

```
; Revert Win+E
[-HKEY_CURRENT_USER\SOFTWARE\Classes\CLSID\{52205fd8-5dfb-447d-801a-d0b52f2e83e1}]
```

然后 Win+E 就回来了。

问题 2
----

### window+E 键出现 explore.exe 找不到

或者

### 卸载后打开任意文件夹出错，提示找不到应用程序。

![](https://img-blog.csdnimg.cn/img_convert/04b9be93684a4eee58e4096dad6ea095.png)

或者提示

> shell::{52205fd8-5dfb-447d-801a-d0b52f2e83e1} 找不到运行程序

改了好久的注册表，发现找不到改的地方。。。

最后准备重置系统的时候，先给了一个差评，然后在商店看见了一个神器的评论：

```
lt's important to point out that there are a couple of warnings in place regarding this option and using itdespite that is an acknowledgment of the risk on the user's part. 1.The option is in the experimentalsettings page, 2.There is a clear warning of the risk and it explicitly mentions to turn off the settingbefore uninstalling the app, 3.There is a UAC prompt confirming your decision to modify the registry.That being said, we are working on improving the way we inform the user of the risks. In the meantimeyou can revert the changes using this script https://raw.githubusercontent.com/files-community/files-community.github.io/main/data/SetFilesAsDefault.zip.
```

```
翻译过来：
需要指出的是，对于这个选项和使用它有一些警告，尽管这是对用户的风险的承认。1.选项在实验设置页面，2。有一个明确的风险警告，并明确提到在卸载应用程序之前关闭设置，3。会出现一个UAC提示符，确认您修改注册表的决定。话虽如此，我们正在努力改进我们告知用户风险的方式。与此同时，您可以使用这个脚本https://raw.githubusercontent.com/files-community/files-community.github.io/main/data/SetFilesAsDefault.zip恢复更改。
```

下载地址：[https://raw.githubusercontent.com/files-community/files-community.github.io/main/data/SetFilesAsDefault.zip](https://raw.githubusercontent.com/files-community/files-community.github.io/main/data/SetFilesAsDefault.zip)

于是乎

![](https://img-blog.csdnimg.cn/img_convert/870d8d11e6cbc594d7170934d3ce613b.gif)

注册表文件
-----

### SetFilesAsDefault.reg

```
Windows Registry Editor Version 5.00

; Set Default
[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell]
@="openinfiles"

[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell\openinfiles]
@="Open In Files"

[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell\openinfiles\command]
@=hex(2):22,00,25,00,4c,00,4f,00,43,00,41,00,4c,00,41,00,50,00,50,00,44,\
  00,41,00,54,00,41,00,25,00,5c,00,4d,00,69,00,63,00,72,00,6f,00,73,00,6f,00,\
  66,00,74,00,5c,00,57,00,69,00,6e,00,64,00,6f,00,77,00,73,00,41,00,70,00,70,\
  00,73,00,5c,00,66,00,69,00,6c,00,65,00,73,00,2e,00,65,00,78,00,65,00,22,00,\
  20,00,22,00,25,00,31,00,22,00,00,00

; Set Win+E
[HKEY_CURRENT_USER\SOFTWARE\Classes\CLSID\{52205fd8-5dfb-447d-801a-d0b52f2e83e1}\shell\opennewwindow\command]
@=hex(2):22,00,25,00,4c,00,4f,00,43,00,41,00,4c,00,41,00,50,00,50,00,44,\
  00,41,00,54,00,41,00,25,00,5c,00,4d,00,69,00,63,00,72,00,6f,00,73,00,6f,00,\
  66,00,74,00,5c,00,57,00,69,00,6e,00,64,00,6f,00,77,00,73,00,41,00,70,00,70,\
  00,73,00,5c,00,66,00,69,00,6c,00,65,00,73,00,2e,00,65,00,78,00,65,00,22,00,\
  00,00
"DelegateExecute"=""
```

### UnsetFilesAsDefault.reg

```
Windows Registry Editor Version 5.00

; Revert Default
[HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell]
@=-

[-HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\shell\openinfiles]

; Revert Win+E
[-HKEY_CURRENT_USER\SOFTWARE\Classes\CLSID\{52205fd8-5dfb-447d-801a-d0b52f2e83e1}]
```

好了，还是江湖再见。