---
title: 动画
weight: 70
since: 2.0
---

`Fyne` 包含一个动画框架，允许您随着时间的推移将画布属性从一个值平滑地过渡到另一个值。动画可以包含任何代码，这意味着可以管理任何类型的对象属性，但是只能有针对大小，位置和颜色的内置动画。

动画通常使用画布包内置工具（`NewSizeAnimation`）创建，运行`Start()`调用创建的动画。您可以将动画设置为重复或自动反转，如下图所示。

首先用矩形演示一下颜色渐变的动画。
在下面示例代码中，我们设置一个矩形画布，就像哦我们之前的代码一样。
最大的不同是动画在显示窗口之前。动画用`NewColorRGBAAnimation`创建，它可使颜色从`red`变为`blue`，并且中间有2秒（指定的持续时间）的过度时间。


```go
package main

import (
	"image/color"
	"time"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")

	obj := canvas.NewRectangle(color.Black)
	obj.Resize(fyne.NewSize(50, 50))
	w.SetContent(container.NewWithoutLayout(obj))

	red := color.NRGBA{R:0xff, A:0xff}
	blue := color.NRGBA{B:0xff, A:0xff}
	canvas.NewColorRGBAAnimation(red, blue, time.Second*2, func(c color.Color) {
		obj.FillColor = c
		canvas.Refresh(obj)
	}).Start()

	w.Resize(fyne.NewSize(250, 50))
	w.SetPadded(false)
	w.ShowAndRun()
}
```

还可以同时对多个属性进行处理。如果你观察比较仔细，你可以看到我们的矩形没有添加到布局容器中 -- 这意味着我们可以手动指定位置和尺寸。让我们添加一个新的动画位置，这个动画奖在整个窗口中移动，并自动反转。

```go
move := canvas.NewPositionAnimation(fyne.NewPos(0, 0), fyne.NewPos(200, 0), time.Second, obj.Move)
move.AutoReverse = true
move.Start()
```

因为`CanvasObject`对象的`Move()`函数需要一个`fyne.Position`参数，并且动画回调也需要，我们可以简单的传递这个方法名称而不是新建一个新函数。

如果你在第一个动画下方添加上述代码，你会看到图片在变色的同时在移动。