---
title: 绑定简单组件
weight: 20
redirect_from:
- /tour/binding/simple
---

# 绑定简单组件
---

绑定小部件的最简单形式使用绑定元素而不是静态值。
许多组件提供`WithData`构造函数接受一个数据类型绑定。
要设置绑定，您需要做的就是传入正确的类型。

尽管这在初始代码中可能看起来不是很大的好处，但您可以看到它如何确保显示的内容始终与数据源保持同步。您会注意到我们不需要调用小部件，甚至不需要保留对它的引用，但它会相应地更新。

一开始可能在代码中看它没有什么用处，但你能看到显示内容怎么和数据源保持同步的。
你可以看到我们不需要用`Refresh()`刷新`Label`，label可以自己更新。

```go
package main

import (
	"time"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/data/binding"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	w := myApp.NewWindow("Simple")

	str := binding.NewString()
	str.Set("Initial value")

	text := widget.NewLabelWithData(str)
	w.SetContent(text)

	go func() {
		time.Sleep(time.Second * 2)
		str.Set("A new string")
	}()

	w.ShowAndRun()
}
```

下一步我们介绍如何设置[双向绑定](twoway)。

In the next step we look at how to set up widgets 
that edit values through  binding.
