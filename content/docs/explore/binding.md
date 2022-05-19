+++
title = "数据绑定"
description = "Data Binding"
tags = [
    "go",
    "golang",
    "hugo",
    "development",
]
date = "2022-05-18"
categories = [
    "Development",
    "golang",
]
menu = "main"
weight=80
+++

# 数据绑定
---

数据绑定在`Fyne v2.0.0`中引入，这可以使组件和数据源更好的关联起来。
`data/binding` 包有许多有用的绑定，可以用来管理应用中用到的几乎所有标准类型。
数据绑定可以通过绑定API管理（例如`NewString`），也可以关联到外部的数据元素（`BindInt(*int)`）。

支持绑定的组件通常有一个`...WithData`构造函数，在创建组件时可以设置绑定的数据。
当然你还可以调用`Bind()`或者`Unbind()`来管理组件绑定的数据。

下面这个示例展示了如何`String`数据绑定到`Label`控件：

```go
package main

import (
	"time"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/data/binding"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")

	str := binding.NewString()
	go func() {
		dots := "....."
		for i := 5; i >= 0; i-- {
			str.Set("Count down" + dots[:i])
			time.Sleep(time.Second)
		}
		str.Set("Blast off!")
	}()

	w.SetContent(widget.NewLabelWithData(str))
	w.ShowAndRun()
}
```
在本站[数据绑定](/docs/binding/)中找到更多信息。