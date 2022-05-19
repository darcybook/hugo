+++
title = "Canvas 和 CanvasObject"
description = "Canvas and CanvasObject"
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

# Canvas 和 CanvasObject
---
在 Fyne 中，`Canvas`是绘制应用程序的区域。每个窗口都有一个画布，您可以使用`Window.Canvas()`进行访问，但通常您会在`Window`上找到避免直接访问画布的功能。

在Fyne中可以绘制的所有内容都是一种`CanvasObject`。
下面这个示例通过在canvas设置原始图形元素的却别。

可以通过多种方式自定义每种类型的对象，如文本和圆圈示例所示。
就像`Canvas.SetContent()`改变content显示，它也会改变当前看视图。你可以将`FillColour`改为rectangle，你可以使用`rect.Refresh()`请求刷新。 

```go
package main

import (
	"image/color"
	"time"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Canvas")
	myCanvas := myWindow.Canvas()

	blue := color.NRGBA{R: 0, G: 0, B: 180, A: 255}
	rect := canvas.NewRectangle(blue)
	myCanvas.SetContent(rect)

	go func() {
		time.Sleep(time.Second)
		green := color.NRGBA{R: 0, G: 180, B: 0, A: 255}
		rect.FillColor = green
		rect.Refresh()
	}()

	myWindow.Resize(fyne.NewSize(100, 100))
	myWindow.ShowAndRun()
}
```
我们可以用相同的方式绘制许多不同的绘图元素，例如圆形和文本。

```go
func setContentToText(c fyne.Canvas) {
	green := color.NRGBA{R: 0, G: 180, B: 0, A: 255}
	text := canvas.NewText("Text", green)
	text.TextStyle.Bold = true
	c.SetContent(text)
}

func setContentToCircle(c fyne.Canvas) {
	red := color.NRGBA{R: 0xff, G: 0x33, B: 0x33, A: 0xff}
	circle := canvas.NewCircle(color.White)
	circle.StrokeWidth = 4
	circle.StrokeColor = red
	c.SetContent(circle)
}
```

## Widget

`fyne.Widget`是一种特殊类型的画布对象，它具有相关的交互式元素。在widgets中，逻辑与它的外观（也称为`WidgetRenderer`）是分开的。

小部件也是`CanvasObject`的类型，因此我们可以将窗口的内容设置为单个小部件。在此示例中，请参阅我们如何创建一个新的窗口并`widget.Entry`将其设置为窗口的内容。


```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Widget")

	myWindow.SetContent(widget.NewEntry())
	myWindow.ShowAndRun()
}
```
