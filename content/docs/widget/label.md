---
title: 标签
weight: 10
redirect_from:
  - /widget/
  - /tour/widget/label
  - /tour/widget/
---

组件是`Fyne`应用程序GUI的主要组件，它们可以在基本可以`fyne.CanvasObject`的任何地方使用。它们管理用户交互，并将始终与当前主题匹配。fyne.CanvasObject

标签组件是其中最简单的 -- 它向用户显示文本。
和`canvas.Text`不同，它可以处理一些转义（such as `\n`）和一些换行（通过`Wrapping`设置）。
你可以通过调用`widget.NewLabel("some text")`来创建标签，可以分配一个变量或者直接传给容器。


```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Label Widget")

	content := widget.NewLabel("text")

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```
