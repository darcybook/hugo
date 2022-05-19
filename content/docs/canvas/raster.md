---
title: Raster
weight: 60
redirect_from:
  - /tour/canvas/raster
---

# 光栅
---

`canvas.Raster`就像一个图像，为屏幕每个像素只绘制一个点。
随之用户界面尺寸或图形尺寸调整，会请求更多像素填充。
我们使用`Generator`函数 -- 它将返回每个像素的颜色。

`Generator`函数可以基础像素（在下面例子中我们为每个像素生产随机颜色），也可以基础完整图像。
生产完整图像（使用`canvas.NewRaster()`）更有效，但有时直接控制像素更方便。

```go
package main

import (
	"image/color"
	"math/rand"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
)

func main() {
	myApp := app.New()
	w := myApp.NewWindow("Raster")

	raster := canvas.NewRasterWithPixels(
		func(_, _, w, h int) color.Color {
			return color.RGBA{uint8(rand.Intn(255)),
				uint8(rand.Intn(255)),
				uint8(rand.Intn(255)), 0xff}
		})
	// raster := canvas.NewRasterFromImage()
	w.SetContent(raster)
	w.Resize(fyne.NewSize(120, 100))
	w.ShowAndRun()
}
```

如果您的像素数据存储在图像中，您可以通过`NewRasterFromImage()`功能加载它，该功能将加载图像以在屏幕上显示完美的像素。
