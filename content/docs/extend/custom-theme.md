---
layout: page
title: 创建自定义主题
weight: 40
redirect_from:
 - /tutorial/custom-theme
---

# 创建自定义主题
---

应用可以自己加载自定义主题，这些主题可能修改一个小部分，也可能完全不一样。主题需要实现`fyne.Theme`接口：

```go
type Theme interface {
	Color(ThemeColorName, ThemeVariant) color.Color
	Font(TextStyle) Resource
	Icon(ThemeIconName) Resource
	Size(ThemeSizeName) float32
}
```

要应用我们的主题更改，我们将首先定义一个实现此接口的新类型。

### 定义主题

我们首先定义一个新类型，它将是我们的主题，一个简单的空结构就可以了：

```go
type myTheme struct {}
```
最好断言我们实现了一个接口，这样编译器错误就更靠近类型定义。


```go
var _ fyne.Theme = (*myTheme)(nil)
```

在这里你可以看到编译错误，因为我们还没实现接口，我们从颜色开始改变。
#### 自定义颜色

接口中定义的函数要求我们定义命名颜色，并为用户所需的变体（例如或 ）提供提示。在我们的主题中，我们将返回自定义背景颜色 - 使用不同的浅色和深色值。
`Theme`接口中定义了一个`Color`函数，我们可以定义一个客户想要的颜色（例如`theme.VariantLight`或`theme.VariantDark`）。在我们的主题中，我们返回一个自定义的颜色 -- 区分light和dark。

```go
func (m myTheme) Color(name fyne.ThemeColorName, variant fyne.ThemeVariant) color.Color {
	if name == theme.ColorNameBackground {
		if variant == theme.VariantLight {
			return color.White
		}
		return color.Black
	}

	return theme.DefaultTheme().Color(name, variant)
}
```

您将看到此处的最后一行引用了`theme.DefaultTheme()`查找标准值。这使我们能够提供自定义值，但在我们未提供自定义值时回退到标准主题。

当然颜色比资源简单，我们看一下自定义图标。

#### 覆盖默认图标

图标（和字体）使用`fyne.Resource`而不是基本数据类型。
使用`fyne.NewStaticResource`我们可以新建立自己的资源，或者你可以传递通过[资源嵌入](bundle)建立的资源。


```go
func (m myTheme) Icon(name fyne.ThemeIconName) fyne.Resource {
	if name == theme.IconNameHome {
		fyne.NewStaticResource("myHome", homeBytes)
	}
	
	return theme.DefaultTheme().Icon(name)
}
```
如果我们不想提供指定的覆盖值，我们直接返回默认主题的图标。

### 加载主题

在我们加载主题之前，您还需要实现`Size`和`Font`方法。如果您愿意使用默认值，则可以只使用这些空实现。

```go
func (m myTheme) Font(style fyne.TextStyle) fyne.Resource {
	return theme.DefaultTheme().Font(style)
}

func (m myTheme) Size(name fyne.ThemeSizeName) float32 {
	return theme.DefaultTheme().Size(name)
}
```

若要设置应用的主题，需要添加以下代码行：

```go
app.Settings().SetTheme(&myTheme{})
```

通过这些更改，您可以应用自己的样式，进行小的调整或提供完全自定义的外观应用程序！
