+++
title = "打包"
description = "Packaging for Desktop"
tags = [
    "go",
    "golang",
    "hugo",
    "development",
    "fyne",
]
date = "2022-05-18"
categories = [
    "Development",
    "golang",
]
menu = "main"
weight=70
+++
# 打包
---
## 桌面程序打包
--- 

打包图形应用程序以进行分发可能很复杂。图形应用程序通常具有与其关联的图标和元数据，以及与每个环境集成所需的特定格式。Windows可执行文件需要嵌入式图标，macOS应用程序是捆绑包，Linux应该安装各种元数据文件。真是麻烦！

值得庆幸的是，`fyne`应用程序具有可以自动处理此情况的`package`命令。只需指定目标操作系统和任何所需的元数据（如 icon）即可生成相应的程序包。图标转换将自动完成.icns或.ico因此只需提供.png文件 :) 即可。您所需要的只是已经为目标平台构建了应用程序...


```sh
go install fyne.io/fyne/v2/cmd/fyne@latest
fyne package -os darwin -icon myapp.png
```

如果您使用的是较旧版本的 Go （<1.16），则应使用`go get`命令安装

```sh
go get fyne.io/fyne/v2/cmd/fyne
fyne package -os darwin -icon myapp.png
```

将创建 myapp.app，这是一个完整的捆绑包结构，用于分发给macOS用户。然后，您也可以构建Linux和Windows版本...

```
fyne package -os linux -icon myapp.png
fyne package -os windows -icon myapp.png
```
这些命令将创建：

 * myapp.tar.gz包含一个从 usr/local/ 开始的文件夹结构，Linux 用户可以扩展到其系统的根目录。
 * myapp.exe（在第二次生成之后，这是 windows 包所必需的）将嵌入图标和应用元数据。

如果您只想在自己的计算机上安装桌面应用程序，则可以使用有用的安装子命令。例如，要在系统范围内安装当前应用程序，您只需执行以下操作：

```
fyne install -icon myapp.png
```
所有这些命令还支持`Icon.png`的默认图标文件，以便您可以避免为每次执行键入参数。从`Fyne 2.1`开始，还有一个[元数据文件](/docs/started/metadata)文件，您可以在其中为项目设置默认选项。

当然，如果您愿意，您仍然可以使用标准的Go工具运行应用程序。