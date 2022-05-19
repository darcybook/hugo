---
title: 渐变
weight: 70
since: 1.1

redirect_from:
  - /tour/canvas/gradient
---
# 渐变

最后一个基本画布类型是`Gradient`,使用`canvas.LinearGradient`和`canvas.RadialGradient`可以绘制一种颜色到另一种颜色的渐变。
你可以通过`NewHorizontalGradient()`，`NewVerticalGradient()` 或者 `NewRadialGradient()`创建渐变。

要创建渐变，首先需要一个开始和结束的颜色 -- 两者之前的每个颜色都有画布计算。
在下面的示例中，我们使用`color.Transparent`来展示一个渐变如何使用`alpha`值设置半透明。

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
	w := myApp.NewWindow("Gradient")

	gradient := canvas.NewHorizontalGradient(color.White, color.Transparent)
	//gradient := canvas.NewRadialGradient(color.White, color.Transparent)
	w.SetContent(gradient)

	w.Resize(fyne.NewSize(100, 100))
	w.ShowAndRun()
}
```
