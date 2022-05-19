---
title: 文本
weight: 20
redirect_from:
  - /tour/canvas/text
---

# 文本

`Fyne`所有文本都用`canvas.Text`呈现。创建时需要指定文本和颜色。
文本由当前主题默认字体呈现。

文本对象允许设置`Alignment`和`TextStyle`这些值。
例如下列示例，指定了等宽字体`fyne.TextStyle{Monospace: true}`：

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
	w := myApp.NewWindow("Text")

	text := canvas.NewText("Text Object", color.White)
	text.Alignment = fyne.TextAlignTrailing
	text.TextStyle = fyne.TextStyle{Italic: true}
	w.SetContent(text)

	w.ShowAndRun()
}
```
通过`FYNE_FONT`可以设定环境变量字体。
使用此方式设定一个`.ttf`文件，替代`Fyne`工具包或当前主题提供的字体。
