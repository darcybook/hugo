+++
title = "窗口处理"
description = "Window Handling"
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
weight=50
+++
# 窗口处理

---
Windows 是使用`App.NewWindow()`函数创建的，需要使用`Show()`函数进行显示。`fyne.Window`上`ShowAndRun()`的协助你同时显示并运行你的应用。

默认情况下，在通过`MinSize()`函数，窗口大小是正好可以显示`content`。

窗口的尺寸将是正确的，可以通过检查函数来显示其内容（后面的示例可以了解更多）。通过`Window.Resize()`可以设置一个更大的尺寸。函数需要传递具有长宽属性（基于设备无关像素，它在不同设备上将是相同的）的`fyne.Size`，例如默认情况下，要使用正方形，我们可以：

```go
	w.Resize(fyne.NewSize(100, 100))
```
要注意的是，桌面环境可能会显示窗口导致比实际的小。移动设备通常会忽略这一点，一般以全屏显示。

如果你向显示第二个窗口，你只需调用`Show()`。如果你的应用程序启动时，要打开多个窗口，那么将`Window.Show()` 和`App.Run()`分开是个不错的选择。下面的例子，介绍了怎么运行时打开两个窗口：

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello World")

	w.SetContent(widget.NewLabel("Hello World!"))
	w.Show()

	w2 := a.NewWindow("Larger")
	w2.SetContent(widget.NewLabel("More content"))
	w2.Resize(fyne.NewSize(100, 100))
	w2.Show()

	a.Run()
}
```

上述应用程序将在两个窗口都关闭时退出。
如果你向将应用设为一个主窗口，一个是附属窗口，你可以将主窗口设置`master`，这样主窗口关闭时，其它窗口也会关闭。在`Window`上调用`SetMaster()`，可以完成设置。

Windows可以随时创建，我们可以修改上面的代码，新增一个窗口（`w2`），点击一个按钮可以打开新窗口。你可以从更复杂的工作流中加载窗口，但要注意新窗口通常显示在当前活动`content`的上方。

```go
	w2.SetContent(widget.NewButton("Open new", func() {
		w3 := a.NewWindow("Third")
		w3.SetContent(widget.NewLabel("Third"))
		w3.Show()
	}))
```
