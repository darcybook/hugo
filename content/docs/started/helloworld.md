+++
title = "Hello World"
description = "Hello World"
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
weight=20
+++


# 开始你的第一个app
---

完成[入门](/docs/started/introduction/)文档中的步骤后，即可开始构建您的第一个应用。为了说明这个过程，我们将构建一个简单的 hello world 应用程序。

用`app.New()`建立一个简单的app，然后用`app.NewWindow()`打开一个窗口。用`SetContent()`将控件数添加到窗口上。最后利用`ShowAndRun()`运行你的`app UI`就会显示了


```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello World")

	w.SetContent(widget.NewLabel("Hello World!"))
	w.ShowAndRun()
}
```
`ShowAndRun()`可以使用该命令生成上述代码，然后通过运行`go build .`该命令或双击图标来执行该代码。您也可以绕过编译步骤，直接使用`go run .`运行代码。

这两种方法都会显示一个窗口，如下所示：

![](/mk_img/helloword-26-847-1.png)  


如果您更喜欢浅色主题，那么只需设置环境变量`FYNE_THEME=light`，您将获得：

![FYNE_THEME=light](/mk_img/helloword-28-876-4.png)  

这就是入门的全部内容。要了解更多信息，您可以阅读完整的[API文档](https://darcybook.github.io/docs/api/)。


