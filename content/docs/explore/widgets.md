+++
title = "组件清单"
description = "Widget List"
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
# 组件清单
---


## 标准组件 (`widget`包中)

---

### Accordion

可折叠控件（Accordion）显示项目列表，每个项目都由一个按钮表示，点击该按钮时会显示详细视图。


![Accordion](/mk_img/widgets-55-112-2.png)  


### Button

按钮空间由有一个文本和图标，两者都是可选的。


![Button](/mk_img/widgets-56-921-3.png)  

 

### Card

卡片控件是标题副标题的合计，都是可选的。

![Card](/mk_img/widgets-56-817-8.png)  


### Check

单选框 有一个文本和单选（未选中）按钮。

![Check](/mk_img/widgets-56-397-4.png)  


### Entry

输入框空间触发时允许录入简单文本。

![Entry ](/mk_img/widgets-58-401-7.png)  

密码输入框隐藏输入内容，还有一个控制它显示的按钮。

![PasswordEntry](/mk_img/widgets-58-977-6.png)  
 
### FileIcon

文件图标未不同文件提供标准图标。
将文件显示未不同的图标，并显示文件的扩展名。
 
![FileIcon](/mk_img/widgets-59-910-6.png)  

### Form

表单是两列网格，其中每行都有一个标签和一个小部件（通常是输入）。网格的最后一行将包含相应的窗体控件按钮（如果有）。

![Form](/mk_img/widgets-00-304-7.png)  


### Hyperlink

超链接构件是具有适当填充和布局的文本组件。单击后，URL 将在默认 Web 浏览器中打开。

![Hyperlink](/mk_img/widgets-00-544-7.png)  


### Icon

图标小部件是一个基本的图像组件，可加载其资源以匹配主题。

![Icon](/mk_img/widgets-01-413-1.png)  

### Label

标签是具有适当填充和布局的标签组件。

![Label](/mk_img/widgets-01-051-8.png)  
 
### Progress bar

进度条提供一个横条，显示进度。

![Progress bar](/mk_img/widgets-01-814-9.png)  

无限进度条，提供一个横条，一直循环0%-100%，知道条用stop()。

![Progress bar](/mk_img/widgets-02-220-8.png)  


### RadioGroup

多选框控件有一个可选的标签列表，每个文本旁都有一个多选图标。

![RadioGroup](/mk_img/widgets-02-469-5.png)  


### Select

下拉框有一个可选清单，显示当前选中的，单击出发。

![Select](/mk_img/widgets-02-873-8.png)  


### SelectEntry

可选输入框，用户可以输入或者选择一个选项。

![SelectEntry](/mk_img/widgets-02-274-0.png)  


### Separator

分隔符，将不同组件分割开。

![Separator](/mk_img/widgets-03-927-0.png)

### Slider

滑块可在固定的值之前滑动选择。

![Slider](/mk_img/widgets-03-974-1.png)  

### TextGrid

文本域是一个等宽的文字输入框，被设计用来文本输入，代码预览或者终端仿真。

![TextGrid](/mk_img/widgets-03-299-2.png) 

### Toolbar

工具栏可创建工具按钮的水平列表。

![Toolbar](/mk_img/widgets-04-250-9.png) 


## Collection Widgets (在`widget`包中)

**集合小组件**提供高级缓存功能，以提供海量数据的高性能呈现。
这确实会需要更复杂的构造函数，但对于它所展示的结果来说是一个很好的平衡。
这些小部件中的每一个都使用一系列回调函数，最小集由其构造函数定义，其中包括数据大小，可以重用的模板项的创建，以及最后将数据应用于小部件的函数，因为它即将被添加到显示中。

### List

列表提供了大量子元素的高性能垂直方向滚动。

![List](/mk_img/widgets-04-253-5.png)  


### Table

表格提供大量数据二维方向高性能展示。

![Table](/mk_img/widgets-04-887-9.png)  
 

### Tree

树控件提供了子元素垂直滚动，并且点击可以展开子元素。

![Tree](/mk_img/widgets-05-657-0.png)


## Container Widgets (在`container`中)

容器小部件类似于常规容器，但它们另外提供了一些附加功能。

### AppTabs

应用选项卡，允许切换显示内容。每个项目由顶部的按钮表示。

![AppTabs](/mk_img/widgets-05-001-9.png)   

### Scroll

ScrollContainer 滚动条实现了一个比Content小的container。

![Scroll](/mk_img/widgets-05-866-9.png)  


### Split
SplitContainer 拆分容器实现了内部子元素大小拆分的container。

![图 28](/mk_img/widgets-05-910-5.png) 
