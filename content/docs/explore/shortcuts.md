+++
title = "快捷键"
description = "Adding Shortcuts to an App"
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
weight=60
+++

# 快捷键
---
## 在应用上增加快捷键
---

快捷键是利用组合键触发的常见任务。
快捷键和键盘事件非常相似，可以附加到一个触发的元素或者注册到`Canvas`使它在`Window`一直有效。

## 通过`Canvas`注册

有需要标准的快捷键和鼠标右键菜单已经定义了（例如`fyne.ShortcutCopy`）。
添加`Shortcut`的第一步就是定义一个shortcut。大多数用途是作为桌面扩展的快捷键。
我们用`desktop.CustomShortcut`去实现，比如用Tab键和Control你可以参照下面这样做：

```go
	ctrlTab := desktop.CustomShortcut{KeyName: fyne.KeyTab, Modifier: desktop.ControlModifier}
```
要注意的是快捷键是可以重复使用的，这样你就可以将它增加到其它元素或菜单上。
比如说我们想要它一直有效，我们可以这样在`Canvas`上注册。

```go
	ctrlTab := desktop.CustomShortcut{KeyName: fyne.KeyTab, Modifier: desktop.ControlModifier}
	w.Canvas().AddShortcut(&ctrlTab, func(shortcut fyne.Shortcut) {
		log.Println("We tapped Ctrl+Tab")
	})
```
如你所见，这种方式注册快捷键有两个步骤 -- 快捷键定义和一个回调函数。
如果用户用户按下了快捷键，函数就会调用，并输出打印内容。

## 输入框增加快捷键

只有当前元素获得焦点时才触发快捷键也是很有用的。
任何可以聚焦的空间都可以使用，添加一个`TypedShortcut`扩展来管理快捷键。
和增加一个键盘时间很像，除了它的参数是一个`fyne.Shortcut`。

```go
type myEntry struct {
	widget.Entry
}

func (m *myEntry) TypedShortcut(s fyne.Shortcut) {
	if _, ok := s.(*desktop.CustomShortcut); !ok {
		m.Entry.TypedShortcut(s)
		return
	}

	log.Println("Shortcut typed:", s)
}
```
从上面的代码中，你可以看到`TypedShortcut` handler怎是如何调用的。
在这个函数中，你需要检查快捷键是否是之前使用的自定义类型。如果快捷键是标准的，最好调用原始的快捷键处理程序（如果有的化）。
检查完成后，你可以对比下你处理的不同类型的快捷键。