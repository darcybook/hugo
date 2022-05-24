---
layout: page
title: 组件扩展

redirect_from:
 - /develop/extending-widgets.html
 - /tutorial/extending-widgets
 - /tutorial/
---
# 组件扩展
---
标准组件提供最少的功能和定制功能，来支持大部分案例。
某些时候我们需要更高级功能，那么开发者自己构建组件，不如直接在已有的组件扩展。

例如我们扩展图标组件让它能被点击。
我们申明一个新的结构体嵌入`widget.Icon`类型。
我们新增一个构造函数让它可以调用`ExtendBaseWidget`函数。


```go
import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/widget"
)

type tappableIcon struct {
	widget.Icon
}

func newTappableIcon(res fyne.Resource) *tappableIcon {
	icon := &tappableIcon{}
	icon.ExtendBaseWidget(icon)
	icon.SetResource(res)

	return icon
}
```

> **注意：**像`widget.NewIcon`函数可能不会用于扩展，因为它已经调用了 。

然后，我们添加新函数来实现`fyne.Tappable`接口，添加这些函数后，每次用户点击我们的新图标时，都会调用新函数`Tapped`。所需的接口有两个函数`Tapped(*PointEvent)`和`TappedSecondary(*PointEvent)`，因此我们将两个都加上。


```go
import "log"

func (t *tappableIcon) Tapped(_ *fyne.PointEvent) {
	log.Println("I have been tapped")
}

func (t *tappableIcon) TappedSecondary(_ *fyne.PointEvent) {
}
```
我们可以使用简单的应用程序测试这个新的小部件，如下所示。

```go
import (
    "fyne.io/fyne/v2/app"
    "fyne.io/fyne/v2/theme"
)

func main() {
	a := app.New()
	w := a.NewWindow("Tappable")
	w.SetContent(newTappableIcon(theme.FyneLogo()))
	w.ShowAndRun()
}
```
