+++
title = "容器和布局"
description = "Container and Layouts"
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
weight=20
+++
# 容器和布局
---

在前面的示例中，我们看到了如何将`CanvasObject`设置为`Canvas`的内容，但通常我们不仅需要显示一个视图。要显示多个项目，我们使用类型`Container`（容器）。

由于`fyne.Container`也是一个`fyne.CanvasObject`，我们可以将其设置为`fyne.Canvas`的content。
在此示例中，我们创建 3 个文本对象，然后使用该函数将它们放在`Container`中。由于没有布局，我们可以像您看到`text2.Move()`的那样移动元素。

```go
package main

import (
	"image/color"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
	//"fyne.io/fyne/v2/layout"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Container")
	green := color.NRGBA{R: 0, G: 180, B: 0, A: 255}

	text1 := canvas.NewText("Hello", green)
	text2 := canvas.NewText("There", green)
	text2.Move(fyne.NewPos(20, 20))
	content := container.NewWithoutLayout(text1, text2)
	// content := container.New(layout.NewGridLayout(2), text1, text2)

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```
`fyne.Layout`是将元素组织在container的工具。
取消对示例的注释，可以将容器改为包含2列的网格布局。
运行此代码并调整窗口尺寸，可以验证布局如何自适应尺寸。
另外需要注意，布局代码会覆盖`text2`指定位置。

要了解更多信息，您可以查看[`Layout 清单`](layouts).
