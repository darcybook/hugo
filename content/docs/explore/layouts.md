+++
title = "Layout List"
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

## Standard Layouts

---

### Horizontal Box (HBox)

Horizontal Box arranges items in a horizontal row.
Every element will have the same height (the height of the tallest item in the container)
and objects will be left-aligned at their minimum width.

![图 29](/mk_img/layouts-32-393-4.png)

### Vertical Box (VBox)

Vertical Box arranges items in a vertical column.
Every element will have the same width (the width of the widest item in the container)
and objects will be top-aligned at their minimum height.

![图 30](/mk_img/layouts-33-795-6.png)  

### Center

Center layout positions all container elements in the center of the container.
Every object will be set to it's minimum size.

![图 31](/mk_img/layouts-33-256-2.png)  


### Form

Form layout arranges items in pairs where the first column is at minimum width.
This is normally useful for labelling elements in a form, where the label is in the first
column and the item it describes is in the second.
You should always add an even number of elements to a form layout.

![图 32](/mk_img/layouts-33-410-6.png)  


### Grid

Grid layout arranges items equally in the available space.
A number of columns is specified, with objects being positioned horizontally
until the number of columns is reached at which point a new row is started.
All objects have the same size, that is width divided by column total and
the height will be total height divided by the number of rows required. Minus padding.

![图 33](/mk_img/layouts-33-423-2.png)  


### GridWrap

GridWrap layout arranges all items to flow along a row, wrapping to a new row if there is insufficient space.
All objects will be set to the same size, which is the size passed to the layout.
This layout may not respect item MinSize to manage this uniform layout.
Often used in file managers or image thumbnail lists.

![图 34](/mk_img/layouts-33-779-3.png)  


### Border

Border layout supports positioning of items at the outside of available space.
The border is passed pointers to the objects for (top, left, bottom, right).
All items in the container that are not positioned on a border will fill the remaining space.

![图 35](/mk_img/layouts-34-441-8.png)  


### Max

Max layout positions all container elements to fill the available space.
The objects will all be full-sized and drawn in the order they were added
to the container (last-most is on top).

![图 36](/mk_img/layouts-34-736-5.png)  


### Padded

Padded layout positions all container elements to fill the available space
but with a small padding around the outside. The size of the padding is theme
specific. The objects will all be drawn in the order they were added
to the container (last-most is on top).

![图 37](/mk_img/layouts-34-766-7.png)  


## Combining Layouts

It is possible to build up more complex application structures by using multiple layouts.
Multiple containers that each have their own layout can be nested to create complete user 
interface arrangements using only the standard layouts listed above.
For example a horizontal box for a header, a vertical box for a left side file panel and a grid 
wrap layout in the content area - all inside a container using a border layout can build the result illustrated below.

![图 38](/mk_img/layouts-34-368-8.png)  

