---
title: 列表
weight: 80
redirect_from:
  - /tour/widget/list
---

# 列表
---

列表组件时工具包的聚合组件之一。这些组件能够高性能的呈现大量数据。
你可以看到[Table](table)和`Tree` 组件有类似的API。
由于这种设计，用起来比较复杂。

列表需要数据时使用回调函数请求。有3各主要的回调函数，`Length`、`CreateItem` 和 `UpdateItem`。
长度回调（参数1）时最简单的，呈现数据中有多少个项目。
其他的和模板有关 -- 图形元素如何创建、缓存和重用。

`CreateItem` 回调函数范围一个模板对象。实际数据会和模板对象一起显示。
`MinSize`字段会影响列表的最小尺寸。

最后`UpdateItem`被调用时会将数据线缓存。可以用来设置内容可供显示。



```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

var data = []string{"a", "string", "list"}

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("List Widget")

	list := widget.NewList(
		func() int {
			return len(data)
		},
		func() fyne.CanvasObject {
			return widget.NewLabel("template")
		},
		func(i widget.ListItemID, o fyne.CanvasObject) {
			o.(*widget.Label).SetText(data[i])
		})

	myWindow.SetContent(list)
	myWindow.ShowAndRun()
}
```
