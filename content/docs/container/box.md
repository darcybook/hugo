---
title: 盒布局
weight: 10
redirect_from:
- /tour/layout/boxlayout
- /container/
---
# 盒布局
---

如[容器和布局](/docs/explore/container)的描述一样，容器内的元素可以使用布局进行排列。本节探讨内置布局以及如何使用它们。

最常用的布局是`layout.BoxLayout`，它有两种变体，水平和垂直。Box局将所有元素排列在单个行或列中，并带有可选空间以帮助对齐。

水平Box布局，使用`layout.NewHBoxLayout()`创建单行中的项排列。Box中每个项目的宽度都将设置为`MinSize().Width`宽度，并且所有项目的高度都相等 -- `MinSize().Height`中最大的值。
布局可以在容器中使用，或者你可以使用`widget.NewHBox()`box控件。

垂直框布局类似，但它在列中排列项目。每个项目的高度将设置为最小值，并且所有宽度将相等，设置为最小宽度中的最大宽度。

添加一个`layout.NewSpacer()`在元素之前创建一个可扩展空间（例如，是某些元素左对齐，其他）。
一个间隔将会填充所有可用的空间。
在一个垂直box开始增加一个间隔会导致所有元素底对齐。你可以在水平Box的开始和结束添加一个间隔创建一个居中布局。


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
	myWindow := myApp.NewWindow("Box Layout")

	text1 := canvas.NewText("Hello", color.White)
	text2 := canvas.NewText("There", color.White)
	text3 := canvas.NewText("(right)", color.White)
	content := container.New(layout.NewHBoxLayout(), text1, text2, layout.NewSpacer(), text3)

	text4 := canvas.NewText("centered", color.White)
	centered := container.New(layout.NewHBoxLayout(), layout.NewSpacer(), text4, layout.NewSpacer())
	myWindow.SetContent(container.New(layout.NewVBoxLayout(), content, centered))
	myWindow.ShowAndRun()
}
```
