---
title: 工具栏
weight: 70
redirect_from:
  - /tour/widget/toolbar
---

# 工具栏
---
工具栏组件用不同图标建立一行操作按钮。`widget.NewToolbar(...)`函数可以传一个`widget.ToolbarItem`数组。内建的组件类型有操作按钮、分隔符、和间隔符。

`widget.NewToolbarItemAction(..)`创建一个最常用的操作。一个操作包含两个参数，一个是图标资源，另一个是`func()`回调函数。

`widget.NewToolbarSeparator()`创建一个分隔符（通常是垂直的线）在工具栏中分割action。可以使用`widget.NewToolbarSpacer()`灵活的在action之间创建空间。

一个工具栏应该使用在区域最上面，通常使用`layout.BorderLayout`加到 `fyne.Container`容器中。


```go
package main

import (
	"log"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/theme"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Toolbar Widget")

	toolbar := widget.NewToolbar(
		widget.NewToolbarAction(theme.DocumentCreateIcon(), func() {
			log.Println("New document")
		}),
		widget.NewToolbarSeparator(),
		widget.NewToolbarAction(theme.ContentCutIcon(), func() {}),
		widget.NewToolbarAction(theme.ContentCopyIcon(), func() {}),
		widget.NewToolbarAction(theme.ContentPasteIcon(), func() {}),
		widget.NewToolbarSpacer(),
		widget.NewToolbarAction(theme.HelpIcon(), func() {
			log.Println("Display help")
		}),
	)

	content := container.NewBorder(toolbar, nil, nil, nil, widget.NewLabel("Content"))
	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```
