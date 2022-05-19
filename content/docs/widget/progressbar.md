---
title: 进度条
weight: 60
redirect_from:
  - /tour/widget/progressbar
---

# 进度条
---
进度条组件有两种样式，一种显示已经到达`Value`，从`Min`到`Max`。
默认最小值为`0.0`最大值为`1.0`。
调用`widget.NewProgressBar()`直接使用默认值创建组件。
创建之后你可以设置当前`Value`。

设置自定义的范围，你可以手动设置`Min` 和 `Max`字段。标签始终显示的是完成的百分比。

另一种形式是无限进度条，这个版本进度条左右来回往复。
调用`widget.NewProgressBarInfinite()` 创建，并会立即动起来。


```go
package main

import (
	"time"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("ProgressBar Widget")

	progress := widget.NewProgressBar()
	infinite := widget.NewProgressBarInfinite()

	go func() {
		for i := 0.0; i <= 1.0; i += 0.1 {
			time.Sleep(time.Millisecond * 250)
			progress.SetValue(i)
		}
	}()

	myWindow.SetContent(container.NewVBox(progress, infinite))
	myWindow.ShowAndRun()
}
```
