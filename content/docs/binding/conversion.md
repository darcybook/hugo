---
title: 数据转换
weight: 40
redirect_from:
- /tour/binding/conversion
---

# 数据转换
---
目前，我们已经用到了一些输出类型的数据绑定（`String` 和 `Label` 或 `Entry`）。
通常我们希望展现的不是实际的格式。因此`binding`包提供了一系列转换的函数。

在代码中查看如何将 a 转换为 using 。可以通过移动滑块来编辑原始值。每次数据更改时，它都会运行转换代码并更新任何连接的小部件。
最常见的是将不同数据类型转化为字符串再`Label`或`Entry`显示。
下面示例用`binding.FloatToString`将`Float`转化为`String`。
原始的数据通过滑块调整，每次值改变都会自动转化并关联组件。 

还可以格式化字符串让用户界面看起来更自然。
你可以看下使用`WithFormat`可以传递一个字符串格式化后（类似`fmt`包）再输出。


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
	w := myApp.NewWindow("Conversion")

	f := binding.NewFloat()
	str := binding.FloatToString(f)
	short := binding.FloatToStringWithFormat(f, "%0.0f%%")
	f.Set(25.0)

	w.SetContent(container.NewVBox(
		widget.NewSliderWithData(0, 100.0, f),
		widget.NewLabelWithData(str),
		widget.NewLabelWithData(short),
	))

	w.ShowAndRun()
}
```

下面介绍，[list](list)数据
Lastly in this section we will look at [list](/binding/list) data.
