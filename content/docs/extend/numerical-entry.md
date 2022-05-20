---
layout: page
title: 数字输入框
weight: 60
redirect_from:
 - /tutorial/keypress-on-entry.html
 - /tutorial/numerical-entry
---
# 数字输入框
---

传统意义上，GUI程序在组件上使用调用回调和自定义操作。
`Fyne`不会暴露回调函数来捕获小部件上的事件，但它不需要这样做。
Go语言具有丰富的扩展来实现。

相反，我们可以简单地使用类型嵌入并扩展小部件，使其只能输入数值。

首先创建一个新的类型结构，我们将它称为`numericalEntry`。

```go
type numericalEntry struct {
    widget.Entry
}
```
如[扩展组件](extending-widgets)中所述，我们遵循实用练习并创建一个构造函数并扩展`BaseWidget`。

```go
func newNumericalEntry() *numericalEntry {
    entry := &numericalEntry{}
    entry.ExtendBaseWidget(entry)
    return entry
}
```

如果没有，我们就忽略输入。此实现将仅允许输入整数，但可以在将来根据需要轻松扩展以检查其他键。

现在我们只需要让输入框值接受数字。
重写`fyne.Focusable`的部门方法`TypedRune(rune)`来实现。
这允许我们拦截标准输入处理，处理我们键入的内容，并只允许录入我们想要的。

在此方法中，我们将使用条件来检查内容是否与0到9之间的任何数字匹配。
如果匹配到了，我们将内容委派到`TypedRune(rune)`方法中。
如果没有匹配到，我们就忽略输入，这个实现仅仅允许整数输入，但是后面我们有其他需求也可以轻松扩展。


```go
func (e *numericalEntry) TypedRune(r rune) {
	switch r {
	case '0', '1', '2', '3', '4', '5', '6', '7', '8', '9':
		e.Entry.TypedRune(r)
	}
}
```
如果我们想更新实现以允许十进制数字，我们可以简单地添加并允许的符文列表（某些语言使用逗号而不是点作为十进制表示法）。

如果我们允许小数，我们可以只增加`.`和`,`到列表就可以录入（有些语言使用逗号表示小数点）。


```go
func (e *numericalEntry) TypedRune(r rune) {
	switch r {
	case '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '.', ',':
		e.Entry.TypedRune(r)
	}
}
```

如果是这样，我们通过使用（如果您只想允许整数，就可以了）来检查剪贴板内容是否为数字，然后如果剪贴板内容可以解析而不会出错，则将快捷方式委派回嵌入的条目。

现在，输入框只运行用户输入数字类型。但是粘贴的时候仍然允许文本。
我们重写`fyne.Shortcutable`的部分方法`TypedShortcut(fyne.Shortcut)`来解决这个问题。

首先我们用一个断言去检查快捷键是不是`*fyne.ShortcutPaste`。
如果不是，我们可以将快捷方式委托回嵌入的条目。
如果是，我们通过使用`strconv.ParseFloat()`（如果您只想允许整数，`strconv.Atoi()`就可以了）来检查剪贴板内容是否为数字，然后如果剪贴板内容可以解析而不会出错，则将快捷方式委派回嵌入的条目。

```go
func (e *numericalEntry) TypedShortcut(shortcut fyne.Shortcut) {
	paste, ok := shortcut.(*fyne.ShortcutPaste)
	if !ok {
		e.Entry.TypedShortcut(shortcut)
		return
	}

	content := paste.Clipboard.Content()
	if _, err := strconv.ParseFloat(content, 64); err == nil {
		e.Entry.TypedShortcut(shortcut)
	}
}
```

我们还可以确保移动操作系统打开数字键盘而不是默认键盘。这可以通过首先导入`fyne.io/fyne/v2/driver/mobile`包并覆盖`Keyboard() mobile.KeyboardType`作为`m̀obile.Keyboardable`接口一部分的方法来完成。在函数内部，我们只需返回`mobile.NumberKeyboard`类型。

```go
func (e *numericalEntry) Keyboard() mobile.KeyboardType {
	return mobile.NumberKeyboard
}
```

In the end, the resulting code could look something like this:

```go
package main

import (
	"strconv"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/driver/mobile"
	"fyne.io/fyne/v2/widget"
)

type numericalEntry struct {
	widget.Entry
}

func newNumericalEntry() *numericalEntry {
	entry := &numericalEntry{}
	entry.ExtendBaseWidget(entry)
	return entry
}

func (e *numericalEntry) TypedRune(r rune) {
	switch r {
	case '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '.', ',':
		e.Entry.TypedRune(r)
	}
}

func (e *numericalEntry) TypedShortcut(shortcut fyne.Shortcut) {
	paste, ok := shortcut.(*fyne.ShortcutPaste)
	if !ok {
		e.Entry.TypedShortcut(shortcut)
		return
	}

	content := paste.Clipboard.Content()
	if _, err := strconv.ParseFloat(content, 64); err == nil {
		e.Entry.TypedShortcut(shortcut)
	}
}

func (e *numericalEntry) Keyboard() mobile.KeyboardType {
	return mobile.NumberKeyboard
}

func main() {
	a := app.New()
	w := a.NewWindow("Numerical")

	entry := newNumericalEntry()

	w.SetContent(entry)
	w.ShowAndRun()
}
```
