---
title: 中央布局
weight: 60
redirect_from:
- /tour/layout/centerlayout
---
# 中央布局
---
`layout.CenterLayout`中央布局排列所有项目到空间中心。
对象按照传递的顺序绘制，最后的排列在最上面。

```go
package main

import (
	"image/color"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/layout"
	"fyne.io/fyne/v2/theme"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Center Layout")

	img := canvas.NewImageFromResource(theme.FyneLogo())
	img.FillMode = canvas.ImageFillOriginal
	text := canvas.NewText("Overlay", color.Black)
	content := container.New(layout.NewCenterLayout(), img, text)

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```

中央布局是所有元素保持最小大小，如果希望展开项目填充，可参阅[`layout.MaxLayout`](max).
