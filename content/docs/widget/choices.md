---
title: 选择组件
weight: 40
redirect_from:
  - /tour/widget/choices
---
# 选择组件
---

有各种不同组件可以让客户进行一个选择，例如单选框、多选框、和下拉框。

`widget.Check` 单选框创建时使用一个字符串标签，提供一个是/否选择。
每一个组件都有一个"changed"`func(...)`有对应的参数。
`widget.NewCheck(..)`有一个`string`参数，有一个`func(bool)`参数作为改变监听事件。
你还可以使用`Checked`字段获取当前值。

多选框也是类似的，但是第一个参数是一个`string`数组，用来标识每个子元素。
更改函数要求这次有一个`string`参数返回当前选定的值。调用`widget.NewRadioGroup(...)`以构造单选按钮组小部件，以后可以使用此引用来读取`Selected`字段，而不是使用更改回调。

下拉框组件和多选框有相同的参数。调用`widget.NewSelect(...)`会显示一个按钮，点击时出现弹窗，用户可以从中选择。
对于列表使用这个更好。

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
	myWindow := myApp.NewWindow("Choice Widgets")

	check := widget.NewCheck("Optional", func(value bool) {
		log.Println("Check set to", value)
	})
	radio := widget.NewRadioGroup([]string{"Option 1", "Option 2"}, func(value string) {
		log.Println("Radio set to", value)
	})
	combo := widget.NewSelect([]string{"Option 1", "Option 2"}, func(value string) {
		log.Println("Select set to", value)
	})

	myWindow.SetContent(container.NewVBox(check, radio, combo))
	myWindow.ShowAndRun()
}
```
