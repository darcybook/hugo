---
title: 按钮
weight: 20
redirect_from:
  - /tour/widget/button
---

# 按钮
---

按钮组件可以包含文本，图标或者都有，可通过`widget.NewButton()`和`widget.NewButtonWithIcon()`构造。
创建一个文本按钮许哟啊2个参数，一个`string` 内容额一个没有参数的回调函数，点击按钮时会调用此函数。

带图标按钮构造函数包括一个额外参数`fyne.Resource`，参数从包含图标资料。
`theme`包中有内建的图标，在切换主题时候会自动切换。你可以传递自己的图片 -- 通过`fyne.LoadResourceFromPath()`可以帮助加载为resource资源，尽可能的打包资源。

`widget.NewButtonWithIcon()`只传递空字符串，可以建立一个只有图标的按钮。


```go
package main

import (
	"log"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
	//"fyne.io/fyne/v2/theme"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Button Widget")

	content := widget.NewButton("click me", func() {
		log.Println("tapped")
	})

	//content := widget.NewButtonWithIcon("Home", theme.HomeIcon(), func() {
	//	log.Println("tapped home")
	//})

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
````
