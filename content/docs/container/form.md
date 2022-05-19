---
title: 表单布局
weight: 50
redirect_from:
- /tour/layout/formlayout
---
# 表单布局
---
`layout.FormLayout`表单布局类似一个两列的[表格布局](/docs/container/grid)，调整成一个适合表单的样式。
每个元素的高是每两者最小高度中最高的，左侧的宽度是第一列中每项的最小宽度中最大的，第二列的元素展开自动填充。

这个布局通常用在`widget.Form`部件，但也可以利用`layout.NewFormLayout()`传给`container.New(...)`。

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
	myWindow := myApp.NewWindow("Form Layout")

	label1 := canvas.NewText("Label 1", color.Black)
	value1 := canvas.NewText("Value", color.White)
	label2 := canvas.NewText("Label 2", color.Black)
	value2 := canvas.NewText("Something", color.White)
	grid := container.New(layout.NewFormLayout(), label1, value1, label2, value2)
	myWindow.SetContent(grid)
	myWindow.ShowAndRun()
}
```
