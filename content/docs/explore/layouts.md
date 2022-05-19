+++
title = "布局清单"
description = "Layout List"
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
weight=40
+++

# 布局清单
---
## 标准布局

---

### Horizontal Box (HBox)

HBox在水平行排列子元素。
每个子元素有相同的高（容器中最高的元素）并保持最小宽度左对齐。

![HBox](/mk_img/layouts-32-393-4.png)

### Vertical Box (VBox)

VBox在垂直列排列子元素。
每个子元素有相同的宽（容器中最宽的元素）并保持最小高度，顶对齐。

![VBox](/mk_img/layouts-33-795-6.png)  

### Center

居中布局将所有元素放在容器中心。
每个对象设置为最小尺寸。

![Center](/mk_img/layouts-33-256-2.png)  


### Form

表单布局按对进行布局，第一列宽度最小。
对在表单中标签很有用，标签位于第一列，其它对象位于第二列。
此布局需要每次添加偶数个元素。

![Form](/mk_img/layouts-33-410-6.png)  


### Grid

网格布局在可用空间内平局排列元素。
元素水平排放，直到达到指定的列数后自动换行。
所有对象都有相同的尺寸，宽度为宽/列数，高度为高/所需行数。上述计算需要减去padding。

![Grid](/mk_img/layouts-33-423-2.png)  

### GridWrap

网格环绕布局横向排列元素，如果空间不足，就换行。
所有对象都将设置为相同尺寸。
此布局可能不遵循`MinSize`来管理此统一布局。通常用于文件管理器或图像缩略图列表。

![GridWrap](/mk_img/layouts-33-779-3.png)  

### Border

边框布局支持将元素定位在可用空间外部。

![Border](/mk_img/layouts-34-441-8.png)  


### Max

最大布局将所有容器元素填充可用空间。
所有对象都是全尺寸的，并按照添加顺序绘制（最后一个在顶部）。 

![Max](/mk_img/layouts-34-736-5.png)  


### Padded

填充布局定位所有容器元素类似最大布局，但在外部哟一个padding填充。

![Padded](/mk_img/layouts-34-766-7.png)  


## Combining Layouts

通过使用不同布局可以构建更为复杂的布局结构。
每个容器可以拥有不同的布局，且每一个可以嵌套不同的标准布局。
例如，一个水平HBox作为header，一个垂直VBox作为左侧边栏面板，一个网格布局作为内容域 -- 所有容器都使用边框布局。如下图所示的结果：

![Combining Layouts](/mk_img/layouts-34-368-8.png)  

