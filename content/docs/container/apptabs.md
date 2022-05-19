---
title: 应用选项卡
weight: 80
redirect_from:
- /tour/container/apptabs
---

# AppTabs 应用选项卡
---

应用选项卡允许用户在不同的面板中切换。
选项卡只有图标或者文本。建议每个选项卡是否有图标保持一致。
`container.NewAppTabs(...)`建立选项卡容器，参数为`container.TabItem`元素（可以通过`container.NewTabItem(...)`建立）。 

选项卡的位置可以用`container.TabLocationTop`、`container.TabLocationBottom`、`container.TabLocationLeading`和`container.TabLocationTrailing`来设置。默认配置是top。


```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	//"fyne.io/fyne/v2/theme"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("TabContainer Widget")

	tabs := container.NewAppTabs(
		container.NewTabItem("Tab 1", widget.NewLabel("Hello")),
		container.NewTabItem("Tab 2", widget.NewLabel("World!")),
	)

	//tabs.Append(container.NewTabItemWithIcon("Home", theme.HomeIcon(), widget.NewLabel("Home tab")))

	tabs.SetTabLocation(container.TabLocationLeading)

	myWindow.SetContent(tabs)
	myWindow.ShowAndRun()
}
```
在移动设备上加载时，选项卡位置可能会被忽略。
在纵向方向中，leading或拖拽位置可以更改为底部。
在横向方向上时，顶部或底部位置将移动到leading位置。

