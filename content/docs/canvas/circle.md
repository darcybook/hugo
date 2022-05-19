---
title: 圆
weight: 40
redirect_from:
  - /tour/canvas/circle
---

# 圆
---

`canvas.Circle`定义一个指定颜色的圆形。
你可以设置一个`StrokeWidth`或者`StrokeColor`设置不同的圆形。

圆形通过`Resize()`调整填充的小时。
由于该示例将圆圈设置为窗口content，因此它将填充真个窗口，有一个基础padding（由主题控制）。

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
	w := myApp.NewWindow("Circle")

	circle := canvas.NewCircle(color.White)
	circle.StrokeColor = color.Gray{0x99}
	circle.StrokeWidth = 5
	w.SetContent(circle)

	w.Resize(fyne.NewSize(100, 100))
	w.ShowAndRun()
}
```

所有这些都是基本类型，可以由我们的驱动程序呈现，而无需其他信息。接下来，我们将从 [`Image`](image) 开始查看更复杂的类型。
