---
title: 图形
weight: 50
redirect_from:
  - /tour/canvas/image
---

# 图形
---
`canvas.Image`是`Fyne`中可缩放的图形资源。
它可以从资源（像示例中一样）、图像文件、包含图像的url，或者从内存中的`io.Reader`对象或`image.Image`。

默认图形填充方式是`canvas.ImageFillStretch`，可以让它填充指定的空间（通过`Resize()`或者layout布局）。
或者，可以使用`canvas.ImageFillContain`来确保图形的纵横比例在指定范围内。
进一步，可以使用`canvas.ImageFillOriginal`（例如下例），确保纵横比例的同时确保一个最小尺寸。

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/theme"
)

func main() {
	myApp := app.New()
	w := myApp.NewWindow("Image")

	image := canvas.NewImageFromResource(theme.FyneLogo())
	// image := canvas.NewImageFromURI(uri)
	// image := canvas.NewImageFromImage(src)
	// image := canvas.NewImageFromReader(reader, name)
	// image := canvas.NewImageFromFile(fileName)
	image.FillMode = canvas.ImageFillOriginal
	w.SetContent(image)

	w.ShowAndRun()
}
```

图像可以基于位图（如 PNG 和 JPEG）或基于矢量（如 SVG）。
在可能的情况下，我们建议使用矢量图像，因为它们会随着尺寸的变化而继续很好地呈现。
使用原始图像大小时要小心，因为它们在使用不同的用户界面比例时可能无法完全按照预期运行。由于Fyne允许整个用户界面缩放25px图像文件，因此可能与25高度fyne对象的高度不同。
