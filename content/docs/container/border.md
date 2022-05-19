---
title: Border
weight: 40
redirect_from:
- /tour/layout/borderlayout
---
# Border 

Border 框布局可能是在构建用户界面时最长使用的方式，它可以将项目定位在中央元素周围，中央元素会扩展填充空间。
使用`fyne.CanvasObject`建立框布局，它需要指定边框位置（就像往常一样）。

语法和其他布局有些不一样，但是基本`layout.NewBorderLayout(top, bottom, left, right)`和下面示例一下。

传递到布局且没有指定位置的项目都会排列到中心区域，并自动填充。
还可以将`nil`传给布局，让位置为空。


```go
package main

import (
	"image/color"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/layout"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Border Layout")

	top := canvas.NewText("top bar", color.White)
	left := canvas.NewText("left", color.White)
	middle := canvas.NewText("content", color.White)
	content := container.New(layout.NewBorderLayout(top, nil, left, nil),
		top, left, middle)
	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```


请注意，中心中的所有项目都将展开以填充空间（就像它们在布局中一样[`layout.MaxLayout`](/docs/container/max)）。要自己管理该区域，您可以创建一个新的`fyne.Container`（使用`container.New()`）并使用您想要的任何布局。

