---
layout: page
title: 资源绑定 
weight: 30
redirect_from:
 - /tutorial/bundle
---

# 资源绑定
---

基于 Go 的应用程序通常构建为单个二进制可执行文件，对于 Fyne 应用程序也是如此。单个文件可以更轻松地分发安装我们的软件。遗憾的是，GUI 应用程序通常需要额外的资源来呈现用户界面。为了管理这一挑战，Go应用程序可以将资产捆绑到二进制文件本身中。Fyne 工具包更喜欢使用“fyne 捆绑包”，因为它具有各种好处，我们将在下面探讨。

和go的其它应用一样，`Fyne`也通常打包为一个二进制可执行文件。
单个文件可以简单的分发我们的软件，但是一个GUI应用需要额外的资源显示用户界面。
go应用可以将资源绑定到二进制文件中。`Fyne`可以使用"fyne bundle"，因为它有很多好处，下面我们会探讨一下。

绑定资源的基础命令时"fyne bundle"。
这个工具用各种参数可以自定义输出，下面基本命令，可以将文件转化为go源代码。


```bash
$ ls
image.png	main.go
$ fyne bundle image.png >> bundled.go
$ ls
bundled.go	image.png	main.go
$ 
```

`bundled.go` 中有一个资源变量的数组，我们可以在代码中使用这些变量。
例如上面的代码中会产生类型下面的文件：

```go
var resourceImagePng = &fyne.StaticResource{
	StaticName: "image.png",
	StaticContent: []byte{
...
	}}
```

如你所见默认的名称时"resource\<Name\>.\<Ext\>"。文件和包的名称也可以自定义。
之后我们就可以在画布中加载图像：


```go
img := canvas.NewImageFromResource(resourceImagePng)
```

fyne 资源只是具有唯一名称的字节的集合，因此这可能是字体、声音文件或您希望加载的任何其他数据。您还可以使用该参数将许多资源捆绑到单个文件中。如果要捆绑许多文件，建议将命令保存在shell脚本中，例如此文件：

`fyne`资源只是唯一标识的字节集合，因此它可以时一个字体、声音文件或者任何你需要加载的文件。
`-append` 参数允许你将多个资源绑定到单一文件。

如果你要绑定多个资源建议将命令写到脚本中，例如下面的`gen.sh`：

```go
#!/bin/bash
fyne bundle image1.png > bundled.go
fyne bundle -append image2.png >> bundled.go
```
如果您随后更改任何资产或添加新资产，则可以更新此文件并运行一次以更新文件。然后，您应该添加到版本控制中，以便其他人可以构建您的应用程序，而无需运行“fyne捆绑包”。添加也是一个好主意，以便其他人可以根据需要重新生成捆绑的资源。

后面你要更改资源或者增加资源，你可以运行这个脚本更新`bundled.go`文件。
你应该将`bundled.go`加入到版本控制中，否则其他人运行时还需要运行`fyne bundle`.
将你写好的脚本放到版本控制中也是一个好主意，这样别人就可以重新生产这个文件。