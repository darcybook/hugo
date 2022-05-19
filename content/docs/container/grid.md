---
title: 网格布局
weight: 20
redirect_from:
- /tour/layout/gridlayout
---
# 网格布局
---

网格布局以网格模式对容器的元素进行布局，网格模式具有固定数量的列。项将填充一行，直到达到列数，在此之后将创建一个新行。垂直空间将在每行对象之间平均分配。

用`layout.NewGridLayout(cols)`建立网格布局，你希望每行的列数。
这将作为`container.New(...)`的第一个参数。

如果调整容器的尺寸，则每个单元格都将平均调整大小共享空间。

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
	myWindow := myApp.NewWindow("Grid Layout")

	text1 := canvas.NewText("1", color.White)
	text2 := canvas.NewText("2", color.White)
	text3 := canvas.NewText("3", color.White)
	grid := container.New(layout.NewGridLayout(2), text1, text2, text3)
	myWindow.SetContent(grid)
	myWindow.ShowAndRun()
}
```
