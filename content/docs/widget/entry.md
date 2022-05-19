---
title: 输入框
weight: 30
redirect_from:
  - /tour/widget/entry
---

# 输入框

用户通过输入可以输入一些简单的文本内容。
`widget.NewEntry()`可以建立一个输入框。
当你建立组件时要记住名称，方便之后访问`Text`属性。
`OnChanged`回调函数，可以在每次内容修改后触发。

输入空间还可以验证输入的内容类型 -- `Validator`属性设置一个`fyne.StringValidator`。`PlaceHolder`、`MultiLine`都是可以设置的。


```go
package main

import (
	"log"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Entry Widget")

	input := widget.NewEntry()
	input.SetPlaceHolder("Enter text...")

	content := container.NewVBox(input, widget.NewButton("Save", func() {
		log.Println("Content was:", input.Text)
	}))

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```
`NewPasswordEntry()`可以设置一个密码输入框（输入的内容会遮蔽）。
