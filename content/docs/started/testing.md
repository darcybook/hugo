+++
title = "单元测试"
description = "Testing Graphical Apps"
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
weight=60
+++
# 测试图形应用

---
一个好的测试组件应该时能快速写测试单元并定期运行。
Fyne 的 API非常容易写测试。将组件逻辑和渲染逻辑分离，我们可以加载程序的时候不用显示它们来进行测试功能。

### 示例

我们可以通过扩展我们的[Hello World](/docs/started/hello)应用程序来演示单元测试，增加让用户输入他们姓名的控件。
我们用`Label`录入姓名，一个`Entry`来显示欢迎词。我们用`container.NewVBox`将一个显示在另一个上面。
更新的用户界面如下：

```go
func makeUI() (*widget.Label, *widget.Entry) {
	return widget.NewLabel("Hello world!"),
		widget.NewEntry()
}

func main() {
	a := app.New()
	w := a.NewWindow("Hello Person")

	w.SetContent(container.NewVBox(makeUI()))
	w.ShowAndRun()
}
```
为了测试此输入动作，我们创建一个包含`TestGreeter`测试函数的的新文件（名称结尾需要是`_test.go`，才会识别位测试文件）。

 ```go
 package main

import (
	"testing"
)

func TestGreeting(t *testing.T) {
}
```
我们可以添加一个验证初始状态的初始测试，为此，我们断言`Label`的`Text`返回的字段，如果测试不正确，则抛出一个错误。将以下代码添加到测试方法中：

```go
	out, in := makeUI()

	if out.Text != "Hello world!" {
		t.Error("Incorrect initial greeting")
	}
```
此测试将通过 -- 接下来我们新增测试区验证欢迎词。我们使用Fyne包`fyne.io/fyne/v2/test`，它被调用来模拟用户输入。
以下测试代码将检查输入用户名时输出是否更新（请确保同时添加`import`）：

```go
	test.Type(in, "Andy")
	if out.Text != "Hello Andy!" {
		t.Error("Incorrect user greeting")
	}
```
您可以使用`go test .`全部运行 -- 就像普通的go测试一样。这样做，您现在将看到报错 -- 因为我们没有添加欢迎程序逻辑。将函数更新为以下代码：

```go
func makeUI() (*widget.Label, *widget.Entry) {
	out := widget.NewLabel("Hello world!")
	in := widget.NewEntry()

	in.OnChanged = func(content string) {
		out.SetText("Hello " + content + "!")
	}
	return out, in
}
```
这样做，您将看到测试现在通过。您还可以运行完整的应用程序（使用`go run .`），并在字段中输入名称时查看问候语更新。另请注意，这些测试在没显示窗口或者拦截鼠标的情况下运行 -- 这是Fyne单元测试设置的另一个好处。
 
