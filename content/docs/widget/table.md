---
title: 表格
weight: 90
redirect_from:
  - /tour/widget/table
--- 

# 表格
---

表格组件和像一个二维的列表（另一个聚合组件）。
也是设计来高性能展示大量数据。
因此组件不会引用所有数据，在需要时才引用。

表格在需要数据时调用回调函数。
有三个回调函数，`Length`、`CreateCell`和`UpdateCell`。
长度回调（参数1）时最简单的，范围需要呈现项目数量，它返回两个整数表示行和列数。
两外两个和实际使用的模板有关。

`CreateCell`回调范围一个新模板对象，就像列表一样。
区别在于，`MinSize`会定义每个单元格的标准此村，和表格最小尺寸（至少显示一个单元格）。

就像前面说的， `UpdateCell` 调用用来缓存数据源模板。索引`(row, col)`和数量一致。


```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

var data = [][]string{[]string{"top left", "top right"},
	[]string{"bottom left", "bottom right"}}

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Table Widget")

	list := widget.NewTable(
		func() (int, int) {
			return len(data), len(data[0])
		},
		func() fyne.CanvasObject {
			return widget.NewLabel("wide content")
		},
		func(i widget.TableCellID, o fyne.CanvasObject) {
			o.(*widget.Label).SetText(data[i.Row][i.Col])
		})

	myWindow.SetContent(list)
	myWindow.ShowAndRun()
}
```
