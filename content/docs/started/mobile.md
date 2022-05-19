+++
title = "移动端打包"
description = "Packaging Mobile Apps"
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
weight=80
+++
# 移动端打包
---

你的 `Fyne` 应用代码将作为移动应用开箱即用，就像它在桌面上一样。但是，打包代码以进行分发会稍微复杂一些。此页面将探讨执行此操作以在iOS和Android上获取应用程序的过程。

首先，您需要安装更多的开发工具才能完成移动打包。对于 Android 版本，您必须安装 Android SDK 和 NDK 并设置适当的环境，以便在命令行上找到这些工具（如`adb`）。要构建iOS应用程序，您需要在macOS计算机上安装Xcode以及命令行工具可选包。

一旦你有了一个工作开发环境，打包就很简单了。要为Android和iOS构建应用程序，以下命令将为您完成所有操作。请确保具有唯一的应用程序标识符，因为在首次发布后不要轻易更改这些标识符。


```
fyne package -os android -appID com.example.myapp -icon mobileIcon.png
fyne package -os ios -appID com.example.myapp -icon mobileIcon.png
```
完成这些命令后（首次编译可能需要一些时间），您将在目录中看到两个新文件，`myapp.apk`以及 `myapp.app`。您将看到后者与darwin应用程序包具有相同的名称 -- 不要被它们迷惑了，因为它们在darwin上不起作用。
要在手机或模拟器上安装Android应用程序，只需运行：

To install the android app on your phone or a simulator simply call:

```
adb install myapp.apk
```
要在设备上安装iOS，请打开Xcode，然后在“窗口”菜单中选择“设备和模拟器”菜单项。然后找到你的手机并将`myapp.app`图标拖到你的应用列表上。要在模拟器上安装，可以使用命令行工具，如下所示：

```
xcrun simctl install booted myapp.app
```

