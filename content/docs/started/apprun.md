+++
title = "应用程序与循环运行"
description = "Application and RunLoop"
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
weight=30
+++

# 应用程序与循环运行

---

要使 GUI 应用程序正常工作，它需要运行一个事件循环（有时称为 runloop）来处理用户交互和绘制事件。在 Fyne 中，这是使用`App.Run()`或 `Window.ShowAndRun()`函数启动的。这两个命令只能再你的设置代码`main()`函数中调用。
一个应用只能由一个事件循环，所以你的代码中只能调用一次`Run()`，调用第二次会导致错误。


```go
package main

import (
	"fmt"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Hello")
	myWindow.SetContent(widget.NewLabel("Hello"))

	myWindow.Show()
	myApp.Run()
	tidyUp()
}

func tidyUp() {
	fmt.Println("Exited")
}
```
对于桌面运行时，可以通过调用直接退出应用（移动应用不支持此功能） - 通常开发人员代码中不需要写。关闭所有窗口后，应用程序也将退出。
所以说`Run()`之后执行的安徽念书,再应用退出前不会调用。
