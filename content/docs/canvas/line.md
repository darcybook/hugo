---
title: 线
weight: 30
redirect_from:
  - /tour/canvas/line
---

# 线
---
`canvas.Line`对象从`Position1`（默认top,left）到`Position1`（默认bottom,right）绘制一条线。
你可以指定它的颜色和笔画粗细，默认粗细为`1`。

线的位置可以通过`Position1`或`Position2`或者通过`Move()`和`Resize()`函数操作。
例如宽度为0的区域会显示一条垂直线，0高度将显示水平线。

```go
package main

import (
	"image/color"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
)

func main() {
	myApp := app.New()
	w := myApp.NewWindow("Line")

	line := canvas.NewLine(color.White)
	line.StrokeWidth = 5
	w.SetContent(line)

	w.Resize(fyne.NewSize(100, 100))
	w.ShowAndRun()
}
```

线条通常在自定义布局中使用或手动控制。与文本不同，它们没有自然（最小）大小，但可以在复杂的布局中使用。

