+++
title = "编译选项"
description = "Compile Options"
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
weight=80
+++

# 编译选项
---

## Build tags
`Fyne`会选择驱动程序和设置来自动配置你的应用。
下面的`build tags`可以帮助。
例如，你希望在桌面计算机上模拟移动应用，可以使用下面命令：

```sh
	go run -tags mobile main.go
```

| Tag               | Description                                                                                                                                                      |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `gles`            | 强制使用嵌入式 OpenGL （GLES） 而不是完整的 OpenGL。这通常由目标设备控制，通常不需要。                                                                           |
| `hints`           | 显示开发人员提示以进行改进或优化。使用`hints`运行，会记录您的应用程序不遵循材料设计或其他建议。                                                                  |
| `mobile`          | 此标记在模拟的移动窗口中运行应用程序。当您想要在移动平台上预览应用程序而无需编译和安装到设备时非常有用。                                                         |
| `no_native_menus` | 此标志专门用于 macOS，指示应用程序不应使用 macOS 本机菜单。相反，菜单将显示在应用程序窗口内。对于在 macOS 上测试应用程序以模拟 Windows 或 Linux 上的行为最有用。 |
