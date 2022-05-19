+++
title = "介绍"
description = "introduction"
tags = [
    "go",
    "golang",
    "hugo",
    "development",
]
date = "2022-05-18"
categories = [
    "Development",
    "golang",
]
menu = "main"
weight=10
+++
# 入门

使用Fyne工具包构建跨平台应用程序非常简单，但在开始之前确实需要安装一些工具。如果您的计算机设置为使用Go进行开发，则可能不需要以下步骤，但我们建议您阅读操作系统的提示以防万一。如果本教程中的后续步骤失败，则应重新访问以下先决条件。


## 事前准备

Fyne 需要 3 个基本元素，即 Go 工具（至少 1.12 版）、C 编译器（用于连接系统图形驱动程序）和系统图形驱动。说明因操作系统而异，请选择下面的相应选项卡以获取安装说明。

请注意，这些步骤只是开发所必需的 - 您的`Fyne`应用程序不需要为最终用户进行任何设置或依赖项安装！

### windows

1. 从下载[下载页面](https://golang.org/dl/)Go并按照说明进行操作
2. 为Windows安装一个可用的C编译器，下面已经经过`Go`和`Fyne`测试：
    * MSYS2 with MingW-w64 - [msys2.org](https://www.msys2.org/)
    * TDM-GCC - [tdm-gcc.tdragon.net](https://jmeubank.github.io/tdm-gcc/download/)
    * Cygwin - [cygwin.com](https://www.cygwin.com/)
3. 在 Windows 中，您的图形驱动程序已经安装，但建议确保它们是最新的。

使用 MSYS2（推荐）进行安装的步骤如下：
* 从 [msys2.org](https://www.msys2.org/) 安装 MSYS2
* 安装后，请勿使用打开的 MSYS 终端
* 从开始菜单打开"MSYS2 MinGW 64-bit"
* 执行以下命令（如果要求提供安装选项，请确保选择“全部”）：

```sh
    $ pacman -Syu
    $ pacman -S git mingw-w64-x86_64-toolchain
```

* 您需要将 `/c/Program\Files/Go/bin` 和 `~/Go/bin` 添加到 PATH 中，对于 MSYS2，您可以将以下命令粘贴到终端中：
```sh
        $ echo "export PATH=$PATH:/c/Program\ Files/Go/bin:~/Go/bin" >> ~/.bashrc
```
### macos

1. 从下载[下载页面](https://golang.org/dl/)Go并按照说明进行操作
2. 从[Mac App Store](https://apps.apple.com/us/app/xcode/id497799835?mt=12)安装Xcode
3. 通过打开终端窗口并键入以下内容来设置 Xcode 命令行工具：
    `xcode-select --install`
4. 在 macOS 中，图形驱动程序已经安装。

### linux

* 您需要使用包管理器安装Go，gcc和图形库头文件，以下命令之一可能会起作用。
* **Debian / Ubuntu:**
`sudo apt-get install golang gcc libgl1-mesa-dev xorg-dev`
* **Fedora:**
`sudo dnf install golang gcc libXcursor-devel libXrandr-devel mesa-libGL-devel libXi-devel libXinerama-devel libXxf86vm-devel`
* **Arch Linux:**
`sudo pacman -S go xorg-server-devel libxcursor libxrandr libxinerama libxi`
* **Solus:**
`sudo eopkg it -c system.devel golang mesalib-devel libxrandr-devel libxcursor-devel libxi-devel libxinerama-devel`
* **openSUSE:**
`sudo zypper install go gcc libXcursor-devel libXrandr-devel Mesa-libGL-devel libXi-devel libXinerama-devel libXxf86vm-devel`
* **Void Linux:**
`sudo xbps-install -S go base-devel xorg-server-devel libXrandr-devel libXcursor-devel libXinerama-devel`

### 树莓派

* 您需要使用包管理器安装 Go、gcc 和图形库头文件。
* `sudo apt-get install golang gcc libegl1-mesa-dev xorg-dev`

### bsd

* 您需要使用包管理器安装 Go、gcc 和图形库头文件。
* **FreeBSD:**
`sudo pkg install go gcc xorg pkgconf`

### 安卓

* 要为Android开发应用程序，您首先需要为当前计算机（Windows，macOS或Linux）安装工具
* 完成后，您将需要安装`Android SDK`和`Android NDK` - 推荐的方法是安装`Android Studio`，然后转到`工具> SDK管理器`，然后从SDK工具安装NDK包。

### ios

* 要开发适用于iOS的应用程序，您需要访问根据上面的macOS选项卡配置的Apple Mac计算机。
* 你还需要创建一个[Apple 开发账号](https://developer.apple.com)并注册开发人员计划（需要付费），以获取在任何设备上运行应用所需的证书。

## 下载

使用 Go 模块（Go 1.16 及更高版本需要）时，您需要先设置`module`，然后才能使用包。如果您没有使用模块或已经初始化了模块，则可以将其跳到下一步。运行以下命令并替换`MODULE_NAME`为模块名称（名称在你调用本地包时会使用）。

```sh
    $ cd myapp
    $ go mod init MODULE_NAME
```

您现在需要下载 Fyne 模块。这将使用以下命令完成： 

    $ go get fyne.io/fyne/v2

要完成模块的设置，您现在需要整理模块文件以正确引用 Fyne 作为依赖项。通过使用以下命令执行此操作（如果未使用模块，则可以跳过）：
```sh
    $ go mod tidy
```

如果您不确定 Go 模块的工作原理，请考虑阅读[教程：创建 Go 模块](https://golang.org/doc/tutorial/create-module)。

## 运行demo

如果您想在开始编写自己的应用程序代码之前查看Fyne工具包的运行情况，可以通过执行以下命令来查看我们的演示应用程序在您的计算机上运行：

    $ go run fyne.io/fyne/v2/cmd/fyne_demo

请注意，第一次运行必须编译一些C代码，因此可能需要比平时更长的时间。后续构建会重用缓存，并且速度会快得多。

### 安装

如果需要，也可以使用以下命令安装演示版（需要 Go 1.16 或更高版本）：
```sh
    $ go install fyne.io/fyne/v2/cmd/fyne_demo@latest
```
对于早期版本的 Go，您需要改用以下命令：
```sh
    $ go get fyne.io/fyne/v2/cmd/fyne_demo
```
如果您的`GOBIN`环境已添加到 path（在 macOS 和 Windows 上应为默认），则可以运行该演示：
```sh
    $ fyne_demo
```
这就是它的全部内容！现在，您可以在所选的 IDE 中编写自己的 Fyne 应用程序。如果你想看到一些Fyne代码在运行，那么你可以阅读你的[你的第一个程序](https://darcybook.github.io/docs/started/helloword/)。