---
title: 网格环绕
weight: 30
redirect_from:
- /tour/layout/gridwraplayout
---
# Grid Wrap
---

与网格布局一样，网格环绕布局在表格布局中排列元素。
但是网格环绕没有固定列数，用固定大小确认每个单元格的宽，然后在构建的时候指定所需行数。

用`layout.NewGridWrapLayout(size)`命令建立网格环绕布局，并指定所有元素的尺寸，并作为`container.New(...)`的第一个参数传递。
行列数会根据当前的容器自动进行计算。

一开始，网格环绕布局只有一列，如果调整尺寸（如下面示例），子元素将自动排列。

```go
package main

import (
	"image/color"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/layout"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Grid Wrap Layout")

	text1 := canvas.NewText("1", color.White)
	text2 := canvas.NewText("2", color.White)
	text3 := canvas.NewText("3", color.White)
	grid := container.New(layout.NewGridWrapLayout(fyne.NewSize(50, 50)),
		text1, text2, text3)
	myWindow.SetContent(grid)

	// myWindow.Resize(fyne.NewSize(180, 75))
	myWindow.ShowAndRun()
}
```
