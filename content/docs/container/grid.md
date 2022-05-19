---
title: 网格布局
weight: 20
redirect_from:
- /tour/layout/gridlayout
---
# 网格布局
---

网格布局以网格模式对容器的元素进行布局，网格模式具有固定数量的列。项将填充一行，直到达到列数，在此之后将创建一个新行。垂直空间将在每行对象之间平均分配。



You create a grid layout using `layout.NewGridLayout(cols)` where cols
is the number of items (columns) you wish to have in each row. This
layout is then passed as the first parameter to
`container.New(...)`.

If you resize the container then each of the cells will resize equally
to share the available space.

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
