---
title: 矩形
weight: 10
redirect_from:
  - /tour/canvas/rectangle
  - /tour/canvas/
  - /canvas/
---
# 矩形
---

`canvas.Rectangle`是`Fyne`中最简单的画布对象。
它显示一个指定颜色的区域，您还可以使用`FillColor`设置颜色。
在下面示例中，只有一个矩形，它会填充整个窗口。

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
	w := myApp.NewWindow("Rectangle")

	rect := canvas.NewRectangle(color.White)
	w.SetContent(rect)

	w.Resize(fyne.NewSize(150, 100))
	w.ShowAndRun()
}
```
其它`fyne.CanvaObject`类型有更多设置，[下一步](text)查看。

其他类型有更多配置，下一步。

Other `fyne.CanvaObject` types have more configuration, let us look
[next](text) at `canvas.Text`.
