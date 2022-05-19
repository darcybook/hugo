+++
title = "更新 content"
description = "Updating Content"
tags = [
    "go",
    "golang",
    "hugo",
    "development",
    "fyne",
]
date = "2022-05-18"
categories = [
    "Development",
    "golang",
]
menu = "main"
weight=40
+++

# 更新 content

---

完成[hello world](/docs/started/hello)教程或其他示例后，您将创建一个基本的用户界面。在此页面中，我们将了解如何从代码中更新 GUI 的content。

第一步是将要更新的小部件分配给变量。在 [hello world](/docs/started/hello) 教程中，我们直接传入 `widget.NewLabel` 到 `SetContent()`，为了更新它，我们将其更改为两行不同的行，例如：

```go
	clock := widget.NewLabel("")
	w.SetContent(clock)
```

只要`content`被分配给`变量`，我们就可以调用类似`SetText("new text")`。对于我们的示例，我们将在`Time.Format`的帮助下将标签的`content`设置为当前时间。


```go
	formatted := time.Now().Format("Time: 03:04:05")
	clock.SetText(formatted)
```
这就是我们需要去改变可见元素的`content`的全部操作（有关完整代码，请参见下文）。
但是,我们可以更进一步的定期更新`content`。

## 后台背景执行

大多数应用程序都需要具有在后台运行的进程，例如下载数据或响应事件。为了模拟这一点，我们将扩展上面的代码以每秒运行一次。

与大多数`go`代码一样，我们可以创建一个`goroutine`（使用`go`关键字）并在那里运行我们的代码。如果我们将文本更新代码移动到新函数，则可以在初始显示和计时器上调用它以进行定期更新。通过将 `goroutine` 和内部`time.Tick` 循环组合在一起，我们可以每秒更新一次`label`。

```go
	go func() {
		for range time.Tick(time.Second) {
			updateTime(clock)
		}
	}()
```

注意,将此代码放在`ShowAndRun` 或 `Run`调用之前，因为它们在应用程序关闭之前不会return。最终运行结果，代码将每秒运行并更新用户界面，从而创建一个基本的时钟小部件。完整代码如下：

```go
package main

import (
	"time"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func updateTime(clock *widget.Label) {
	formatted := time.Now().Format("Time: 03:04:05")
	clock.SetText(formatted)
}

func main() {
	a := app.New()
	w := a.NewWindow("Clock")

	clock := widget.NewLabel("")
	updateTime(clock)

	w.SetContent(clock)
	go func() {
		for range time.Tick(time.Second) {
			updateTime(clock)
		}
	}()
	w.ShowAndRun()
}
```