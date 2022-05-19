+++
title = "元数据"
description = "App Metadata"
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
weight=100
+++
# 元数据
---


## App 元数据
---

`fyne`自v2.1.0 版本起，我们支持元数据文件，该文件允许您在存储库中存储有关应用程序的信息。此文件是可选的，但有助于避免必须记住每个包和 release 命令的特定生成参数。

文件需要命名为`FyneApp.toml`，目录为你运行的`fyne`目录，（通常是`main`包位置）。
文件内容如下所示：

```toml
Website = "https://example.com"

[Details]
Icon = "Icon.png"
Name = "My App"
ID = "com.example.app"
Version = "1.0.0"
Build = 1
```
该文件的顶部是元数据，如果将应用上传到 https://apps.fyne.io 列表页面，将使用元数据，因此它是可选的。[详细信息] 部分包含其他应用商店和操作系统在发布过程中使用的有关应用程序的数据。如果找到此文件，`fyne` 工具将使用该文件，如果元数据存在，则不需要许多必需的命令参数。您仍然可以使用命令行参数覆盖这些值。


