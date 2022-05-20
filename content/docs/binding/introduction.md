+++
title = "介绍"
description = "introduction"
tags = [
    "go",
    "golang",
    "hugo",
    "development",
]
date = "2022-05-19"
categories = [
    "Development",
    "golang",
]
menu = "main"
weight=9
+++


# 数据绑定
---

数据绑定是 Fyne 工具包的强大新增功能，该工具包在版本中引入。通过使用数据绑定，我们可以避免手动管理许多标准对象，如s，s和s。

数据绑定是`Fyne v2.0.0`引入的强大功能。
使用数据绑定，我们可以省去手动管理一些标准对象，例如：`Label`s、`Button`s 和 `List`s。

内建的绑定支持许多基本类型（`Int`、`String`、`Float` 等），数组、Map和结构体一样支持。
每个类型都可以通过简单构造函数建立。
例如用`binding.NewString()`建立一个空新字符串绑定。
可以用`Get` 和 `Set`方法操作它的值。 

也可以用`Bind`开头函数绑定已有的变更了，接受一个指向类型的指针。
例如用`binding.BindInt(&myInt)`绑定有已有的整形。

使用指定类型指针而不是原始的变量，我们可以设置组件和函数在数据变化时自动做出反应。
如果你直接改变了外部变量，调用`Reload`()确保绑定功能正常读取到值。


```go
package main

import (
	"log"

	"fyne.io/fyne/v2/data/binding"
)

func main() {
	boundString := binding.NewString()
	s, _ := boundString.Get()
	log.Printf("Bound = '%s'", s)

	myInt := 5
	boundInt := binding.BindInt(&myInt)
	i, _ := boundInt.Get()
	log.Printf("Source = %d, bound = %d", myInt, i)
}
```
下面我面学习组件怎么绑定[简单值](simple)。

