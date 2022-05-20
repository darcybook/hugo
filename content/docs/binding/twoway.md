---
title: 双向绑定
weight: 30
redirect_from:
- /tour/binding/twoway
---

# 双向绑定
---

目前为止，我们看到用户界面可以随着数据绑定保持最新。
更常见的是，需要让变量保持和UI组件的值保持一致。
幸好`Fyne`提供了双向绑定功能，可以将值推送到变量中读取。
数据的改变自动传达到所有连接的代码，而无需增加代码。

实现这个我们建立一个包含`Label`和`Entry`的应用，并绑定到同一个值。
修改输入框的值会看到标签同样改变，我们也没有在代码中调用刷新或引用组件。

将代码迁移到数据绑定，所有组件的指针可以不再保存。
取而代之，使用到绑定值，你的用户界面可以完全分离。
更易读和管理。

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/data/binding"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	w := myApp.NewWindow("Two Way")

	str := binding.NewString()
	str.Set("Hi!")

	w.SetContent(container.NewVBox(
		widget.NewLabelWithData(str),
		widget.NewEntryWithData(str),
	))

	w.ShowAndRun()
}
```

下一步，将介绍如何为数据增加[conversions](conversion)
 
