---
title: 表单
weight: 50
redirect_from:
  - /tour/widget/form
---
# 表单
---

表单组件可以展示需要带有标签的输入框，并提供一个可选的取消或提交按钮。
没有修饰的表单，每个标签对其到输入框左侧。
设置OnCancel或OnSubmit可以增加一个按钮栏，并可以通过回调函数触发。

使用多个`widget.FormItem`参数传给`widget.NewForm(...)`建立一个表单，或者示例中`&widget.Form{}`方式。
`Form.Append(label, widget)`也可以用来构造表单。

在下面示例中，我们建立了两个输入框，其中一个是多行的（类似HTML中的TextArea）。
有一个提交事件去在应用关闭前打印信息（）。


```go
package main

import (
	"log"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Form Widget")

	entry := widget.NewEntry()
	textArea := widget.NewMultiLineEntry()

	form := &widget.Form{
		Items: []*widget.FormItem{ // we can specify items in the constructor
			{Text: "Entry", Widget: entry}},
		OnSubmit: func() { // optional, handle form submission
			log.Println("Form submitted:", entry.Text)
			log.Println("multiline:", textArea.Text)
			myWindow.Close()
		},
	}

	// we can also append items
	form.Append("Text", textArea)

	myWindow.SetContent(form)
	myWindow.ShowAndRun()
}
```
