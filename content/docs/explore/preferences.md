+++
title = "首选项API"
description = "Using the Preferences API"
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
weight=70
+++
# 首选项API
---
## 使用首选项API
---
保存用户的配置是开发人员的常见任务，跨平台实现时非常复杂耗时。
为了简化这个工作，`Fyne`使用一个API可以简单易懂的方式在文件系统上保存值，同时接管比较复杂的部分。

让我们从API设置开始。
它时首选项界面的一部分，首选项是用来保存和加载以后的不同类型的值，值包括bool、浮点、整型和字符串。
它们每个都有三个不同函数：加载、带有回退值的加载和一个保存值。
下面可以看到字符串类型的三个函数和它使用示例：

```go
// String looks up a string value for the key
String(key string) string
// StringWithFallback looks up a string value and returns the given fallback if not found
StringWithFallback(key, fallback string) string
// SetString saves a string value for the given key
SetString(key string, value string)
```
创建应用变量和调用`Preferences()`可以访问这些函数。
注意有必要使用唯一ID（类似一个颠倒的url com.baidu.www）建立应用。
要使用`app.NewWithID()`来使用创建应用，以便申请应用存储位置。

```go
a := app.NewWithID("com.example.tutorial.preferences")
[...]
a.Preferences().SetBool("Boolean", true)
number := a.Preferences().IntWithFallback("ApplicationLuckyNumber", 21)
expression := a.Preferences().String("RegularExpression")
[...]
```

为了说明这一点，我们建立一个简单应用，让应用在设定的时间后关闭。
设定的时间用户可以修改，并在应用下次启动时生效。
```go
var timeout time.Duration
```
接着，我们建立一个下拉框，让用户选择超时时间，变量*秒数得到超时时间。
最后`"AppTimeout"`key保存选择的值。

```go
timeoutSelector := widget.NewSelect([]string{"10 seconds", "30 seconds", "1 minute"}, func(selected string) {
    switch selected {
    case "10 seconds":
        timeout = 10 * time.Second
    case "30 seconds":
        timeout = 30 * time.Second
    case "1 minute":
        timeout = time.Minute
    }

    a.Preferences().SetString("AppTimeout", selected)
})
```

紧接着，我们需要抓取设置的值，如果没有我们需要一个尽可能短的超时回退值，以节省用户等待时间。
这可以通过设置`timeoutSelector`默认值，或者使用回退。
通过这种方式，下拉框运行时会有一个默认值。

```go
timeoutSelector.SetSelected(a.Preferences().StringWithFallback("AppTimeout", "10 seconds"))
```

最后，我们需要一个单独的goroutine函数运行，告诉应用在指定的时间后退出。

```go
go func() {
    time.Sleep(timeout)
    a.Quit()
}()
```

最后，生成的代码应如下所示：

```go
package main

import (
    "time"

    "fyne.io/fyne/v2/app"
    "fyne.io/fyne/v2/widget"
)

func main() {
    a := app.NewWithID("com.example.tutorial.preferences")
    w := a.NewWindow("Timeout")

    var timeout time.Duration

    timeoutSelector := widget.NewSelect([]string{"10 seconds", "30 seconds", "1 minute"}, func(selected string) {
        switch selected {
        case "10 seconds":
            timeout = 10 * time.Second
        case "30 seconds":
            timeout = 30 * time.Second
        case "1 minute":
            timeout = time.Minute
        }

        a.Preferences().SetString("AppTimeout", selected)
    })

    timeoutSelector.SetSelected(a.Preferences().StringWithFallback("AppTimeout", "10 seconds"))

    go func() {
        time.Sleep(timeout)
        a.Quit()
    }()

    w.SetContent(timeoutSelector)
    w.ShowAndRun()
}
```
