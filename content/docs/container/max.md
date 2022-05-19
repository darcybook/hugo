---
title: 最大布局
weight: 70
redirect_from:
- /tour/layout/maxlayout
---
# 最大布局
---
`layout.MaxLayout`最大布局时最简单的布局，将所有元素设置和容器一样大小。这在一般容器中没啥用，但在编写小部件的时候很合适。

最大布局会将容器扩展为至少元素的最小尺寸。
按照传递的顺序绘制，最后一个对象在最上面。


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
	myWindow := myApp.NewWindow("Max Layout")

	img := canvas.NewImageFromResource(theme.FyneLogo())
	text := canvas.NewText("Overlay", color.Black)
	content := container.New(layout.NewMaxLayout(), img, text)

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```
