---
title: 数组
weight: 50
redirect_from:
- /tour/binding/list
---

# 数组
---
我们用列表组件演示怎么能更简单绑定一个复杂类型。
我们先创建一个字符串数组的数据绑定。
有个数组类型我们可以关联到标准列表组件，像其它组件一样，`widget.NewListWithData`可以绑定数据。

使用此回调结构时，我们应该使用模板标签小部件，而不是调用 。这意味着，如果数据源中的任何字符串发生更改，则表的每个受影响的行都将刷新。

和[list教程](/docs/widget/list)比较一下，主要有2个地方变了，第一个是我们第一个参数传递数组而不是长度回调函数。
第二个是最后参数`UpdateItem`回调函数。
改进的版本使用`binding.DataItem`而不是`widget.ListIndexID`。

当我们使用回调结构时，我们`Bind`模板标签组件而不是调用`SetText`。
这意味着，如果数据源中任何字符串改变，表中每个受到影响的行都会刷新。

```go
package main

import (
	"fmt"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/data/binding"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("List Data")

	data := binding.BindStringList(
		&[]string{"Item 1", "Item 2", "Item 3"},
	)

	list := widget.NewListWithData(data,
		func() fyne.CanvasObject {
			return widget.NewLabel("template")
		},
		func(i binding.DataItem, o fyne.CanvasObject) {
			o.(*widget.Label).Bind(i.(binding.String))
		})

	add := widget.NewButton("Append", func() {
		val := fmt.Sprintf("Item %d", data.Length()+1)
		data.Append(val)
	})
	myWindow.SetContent(container.NewBorder(nil, add, nil, nil, list))
	myWindow.ShowAndRun()
}
```

在示例代码中有一个"Append"按钮，点击的时候数据会增加一行。
列表组件会自动显示增加的数据。

