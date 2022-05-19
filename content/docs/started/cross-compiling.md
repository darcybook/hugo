+++
title = "交叉编译"
description = "Cross Compiling"
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
weight=110
+++
# 交叉编译
---

## 不同平台交叉编译

---

使用Go进行交叉编译的设计很简单 -- 我们只需为目标操作系统设置环境变量`GOOS`（`GOARCH`如果面向不同的体系结构）。不幸的是，当使用原生图形的时候调用时，在Fyne中使用CGo会使这变得更加困难。


### 从开发计算机编译

要交叉编译`Fyne`应用程序，您还必须设置`CGO_ENABLED=1`告诉go启用C编译器（当目标平台与当前系统不同时，通常会关闭）。不幸的是，这样做意味着您必须为要编译的目标平台提供一个C编译器。安装适当的编译器后，您还需要设置环境变量`CC`以告知 Go 要使用哪个编译器。

有许多方法可以安装所需的工具 - 以及可以使用的不同工具。Fyne 开发人员推荐的配置是


| GOOS (target) | CC                               | provider          | download                                                    | notes                                                                                                         |
| ------------- | -------------------------------- | ----------------- | ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `darwin`      | `o32-clang`                      | osxcross          | [from github.com](https://github.com/tpoechtrager/osxcross) | 您还需要安装 macOS SDK (instructions at the download link)                                                    |
| `windows`     | `x86_64-w64-mingw64-gcc`         | mingw64           | package manager                                             | 对于 macOS，请使用[homebrew](https://brew.sh)                                                                 |
| `linux`       | `gcc` or `x86_64-linux-musl-gcc` | gcc or musl-cross | [cygwin](https://www.cygwin.com/) or package manager        | musl-cross 可以从 [homebrew](https://brew.sh) 获得，以提供 linux gcc。您还需要安装 X11 和 mesa 标头进行编译。 |

设置上述环境变量后，您应该能够以通常的方式进行编译。如果发生进一步的错误，则可能是由于缺少包。某些目标平台需要安装其他库或头文件才能成功编译。

### 使用虚拟环境

由于Linux系统能够轻松地交叉编译到macOS和Windows，因此当您不从Linux开发时，使用虚拟化环境会更简单。Docker 映像是复杂构建配置的有用工具，这也适用于 Fyne。可以使用不同的工具。Fyne开发人员推荐的工具是[fyne-cross](https://github.com/fyne-io/fyne-cross)。它受到 [xgo](https://github.com/karalabe/xgo)的启发，并使用构建在[golang-cross](https://github.com/docker/golang-cross)之上的[docker image](https://hub.docker.com/r/fyneio/fyne-cross)，其中包括用于`Windows`的`MinGW`编译器和`macOS SDK`以及`Fyne`要求。

`fyne-cross`允许为以下目标构建二进制文件并创建分发包:

| GOOS    | GOARCH |
| ------- | ------ |
| darwin  | amd64  |
| darwin  | 386    |
| linux   | amd64  |
| linux   | 386    |
| linux   | arm64  |
| linux   | arm    |
| windows | amd64  |
| windows | 386    |
| android | amd64  |
| android | 386    |
| android | arm64  |
| android | arm    |
| ios     |        |
| freebsd | amd64  |
| freebsd | arm64  |

> 注意：iOS 编译仅在darwin主机上受支持。

#### 环境需求

- go >= 1.13
- docker

#### 安装

```
go get github.com/fyne-io/fyne-cross
```

#### 用法

```
fyne-cross <command> [options]

The commands are:

	darwin        Build and package a fyne application for the darwin OS
	linux         Build and package a fyne application for the linux OS
	windows       Build and package a fyne application for the windows OS
	android       Build and package a fyne application for the android OS
	ios           Build and package a fyne application for the iOS OS
	freebsd       Build and package a fyne application for the freebsd OS
	version       Print the fyne-cross version information

Use "fyne-cross <command> -help" for more information about a command.
```

#### Wildcards

`arch`标志支持通配符，以防想要针对指定 GOOS 的所有受支持的 GOARCH 进行编译。

例如:

```
fyne-cross windows -arch=*
```

和下面是一样的

```
fyne-cross windows -arch=amd64,386
```

#### 示例

下面的示例交叉编译和打包 [fyne 示例程序](https://github.com/fyne-io/examples)

```
git clone https://github.com/fyne-io/examples.git
cd examples
```

##### 编译并打开main示例应用

```
fyne-cross linux
```

> 注意：默认情况下，`fyne-cross`会将包编译到当前目录中。
>
> 上面的命令等效于： `fyne-cross linux .`

##### 编译和打包特定示例应用

```
fyne-cross linux -output bugs ./cmd/bugs
```
