---
layout: page
title: 自定义布局
weight: 10
redirect_from:
 - /tutorial/custom-layout
---

# 自定义布局
---
在 Fyne 应用程序中，每个元素都使用简单的布局算法排列其子元素。Fyne 定义了包中可用的许多布局。如果你看一下代码，你会发现它们都实现了接口。
`Fyne`每个容器都使用简单的布局算法排列元素。
`fyne.io/fyne/v2/layout`包中定义了需要布局变量。
如果你看了源码会发现它们都实现了`Layout`接口。

```go
type Layout interface {
	Layout([]CanvasObject, Size)
	MinSize(objects []CanvasObject) Size
}
```

为了说明这一点，我们将创建一个新的布局，该布局以对角线排列元素，并排列在其容器的左下角

首先，我们将定义一个新类型，并定义它的最小大小。要计算这一点，我们只需将所有子元素的宽度和高度（指定为 参数）

任何应用都可以用自定义布局用非标准方式排列组件，实现上面接口就可以自定义。
为了说明这一点，我们将创建一个新的布局，该布局以对角线排列元素，并排列在其容器的左下角

首先顶一个一个新类型`diagonal`，定义它的最小尺寸。
要计算尺寸，我们只需要给所有子元素增加宽和高（指定`[]fyne.CanvasObject`为`MinSize`参数）。


```go
import "fyne.io/fyne/v2"

type diagonal struct {
}

func (d *diagonal) MinSize(objects []fyne.CanvasObject) fyne.Size {
	w, h := float32(0), float32(0)
	for _, o := range objects {
		childSize := o.MinSize()

		w += childSize.Width
		h += childSize.Height
	}
	return fyne.NewSize(w, h)
}
```

对于此类型，我们添加一个`Layout()`函数，该函数应将所有指定的对象移动到第二个参数中指定的`fyne.Size`中。

在我们的实现中，我们计算小部件的左上角（这是`0`x 参数，y位置是容器高度减去所有子项高度的总和）。从顶部位置开始，我们只需按照前一个子项的大小推进每个项目的位置。


```go
func (d *diagonal) Layout(objects []fyne.CanvasObject, containerSize fyne.Size) {
	pos := fyne.NewPos(0, containerSize.Height - d.MinSize(objects).Height)
	for _, o := range objects {
		size := o.MinSize()
		o.Resize(size)
		o.Move(pos)

		pos = pos.Add(fyne.NewPos(size.Width, size.Height))
	}
}
```


这就是创建自定义布局的全部内容。
现在代码已经全部编写完毕，我们可以将其用作`container.New`的`layout`参数。
下面的代码设置了3个`Label`组件，并将它们放置在具有新布局的容器中。
如果运行此应用程序，您将看到对角线窗口小部件的排列，并且在调整窗口大小时，它们将与可用空间的左下角对齐。

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Diagonal")

	text1 := widget.NewLabel("topleft")
	text2 := widget.NewLabel("Middle Label")
	text3 := widget.NewLabel("bottomright")

	w.SetContent(container.New(&diagonal{}, text1, text2, text3))
	w.ShowAndRun()
}
```
