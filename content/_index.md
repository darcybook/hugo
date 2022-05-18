---
title: Introduction
type: docs
---



# 关于

[Fyne](https://fyne.io) 是一个用GO构建的易用的UI工具包和应用API。
它旨在构建在桌面和移动设备上运行的应用程序，这些应用程序具使用相同的代码。

版本2.1是`Fyne API`的当前版本，它引入了`RichText`和`DocTabs`容器，以及文档存储`API`和`FyneApp.toml`元数据支持。我们现在正朝着下一个大版本努力，代号为[bowmore](https://github.com/fyne-io/fyne/milestone/15)，更多的最新消息将出现在我们的新闻提要和GitHub项目中。

# 事前准备

要使用Fyne开发应用程序，您需要Go版本1.14或更高版本，C编译器开发工具。如果您不确定是否全部安装，或者您不知道如何安装，请查看我们的[入门](https://darcybook.github.io/develop/)文档。

使用标准的 go 工具，您可以使用以下命令安装 Fyne 的核心库：


```go
    $ go get fyne.io/fyne/v2
```
# 部件示例

要运行Fyne功能的展示，请执行以下命令：

```
    $ go get fyne.io/fyne/v2/cmd/fyne_demo/
    $ fyne_demo
```

您应该看到类似下面的内容（单击几个按钮后）

![图 1](/mk_img/index-00-851-8.png)  


如果您使用的是浅色主题：

![图 2](/mk_img/index-01-458-4.png)  


甚至在移动设备上运行：

![图 3](/mk_img/index-01-729-6.png)  


# 入门

Fyne被设计地非常容易编程。如果您完成了上述准备，那么您只需要一个Go IDE（或文本编辑器）。

打开一个新文件，您就可以编写您的第一个应用程序了！

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")

	hello := widget.NewLabel("Hello Fyne!")
	w.SetContent(container.NewVBox(
		hello,
		widget.NewButton("Hi!", func() {
			hello.SetText("Welcome :)")
		}),
	))

	w.ShowAndRun()
}
```

您可以简单地运行：
```go
    $ go run main.go
```
它应该看起来像这样：

![图 4](/mk_img/index-01-675-4.png)  

> 请注意，默认情况下，Windows 应用程序从命令提示符加载，这意味着如果单击图标，可能会看到一个命令窗口。
> 若要解决此问题，请将参数添加到运行或生成命令中。`-ldflags -H=windowsgui`

## 移动设备模拟运行

There is a helpful mobile simulation mode that gives a hint of how your app would work on a mobile device:

    $ go run -tags mobile main.go

# 安装

使用`go install`会将可执行文件复制到您的 go 目录。要将带有图标等的应用程序安装到操作系统的标准应用程序位置，您可以使用`fyne`实用程序和`install`子命令。
```sh
    $ go get fyne.io/fyne/v2/cmd/fyne
    $ fyne install
```
# 移动程序打包

要在移动设备上运行，必须打包应用程序。为此，我们可以使用`fyne`实用程序`package`子命令。您需要根据提示添加适当的参数，但基本命令如下所示。打包后，您可以使用平台开发工具或`fyne install`子命令进行安装。

```sh
    $ fyne package -os android -appID my.domain.appname
    $ fyne install -os android
```


# 发布

使用`fyne`实用程序`release`子命令，您可以打包应用程序以发布到应用程序商店和市场。确保已安装标准生成工具，并已按照平台文档进行设置帐户和签名。然后，您可以执行类似以下内容的内容，请注意`-os ios`该参数允许从`macOS`计算机构建iOS应用程序。其他组合也 :)
```sh
    $ fyne release -os ios -certificate "Apple Distribution" -profile "My App Distribution" -appID "com.example.myapp"
```    
上述命令将创建一个`.ipa`文件，然后可以将其上传到iOS App Store。

# 文档

更多文档可在 [Fyne 开发网站(中文版)](https://darcybook.github.io/) 或 [pkg.go.dev](https://pkg.go.dev/fyne.io/fyne/v2?tab=doc) 上找到。

# 示例

您可以在[示例github库](https://github.com/fyne-io/examples/)中找到许多示例应用程序。或者，可以在[fyne 网站](https://apps.fyne.io/)上找到使用fyne的应用程序列表。


# 发布fyne工具包

所有`Fyne`应用程序都可以在没有预安装库的情况下工作，这是应用程序如此便携的原因之一。但是，如果您希望在操作系统上以更大的方式支持Fyne，那么您可以安装一些有助于提供更完整体验的实用程序。

## 额外程序

建议您安装以下附加应用：

| 应用程序      | go get                              | 说明                                                                  |
| ------------- | ----------------------------------- | --------------------------------------------------------------------- |
| fyne_settings | `fyne.io/fyne/v2/cmd/fyne_settings` | 用于管理全局 `Fyne` 设置（如主题和缩放）的 图形界面                   |
| apps          | `github.com/fyne-io/apps`           | [https://apps.fyne.io](https://apps.fyne.io) 上的一个图形安装管理程序 |

这些是可选的应用程序，但可以帮助创建更完整的桌面体验。

## FyneDesk (Linux / BSD)

要在台式机/笔记本电脑上使用Fyne，您也可以安装[FyneDesk](https://github.com/fyne-io/fynedesk):)
