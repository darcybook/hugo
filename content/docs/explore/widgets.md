+++
title = "Widget List"
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


## Standard Widgets (in `widget` package)

---

### Accordion

Accordion displays a list of AccordionItems. Each item is represented by a button that reveals a detailed view when tapped.

![Accordion](/mk_img/widgets-55-112-2.png)  


### Button

Button widget has a text label and icon, both are optional.

![Button](/mk_img/widgets-56-921-3.png)  

 

### Card

Card widget groups elements with a header and subheader, all are optional.

![Card](/mk_img/widgets-56-817-8.png)  


### Check

Check widget has a text label and a checked (or unchecked) icon.

![Check](/mk_img/widgets-56-397-4.png)  


### Entry

Entry widget allows simple text to be input when focused.

![Entry ](/mk_img/widgets-58-401-7.png)  


PasswordEntry widget hides text input and adds a button to display the text.

![PasswordEntry](/mk_img/widgets-58-977-6.png)  
 
### FileIcon

FileIcon provides helpful standard icons for various types of file.
It displays the type of file as an indicator icon and shows the extension of the file type.
 
![FileIcon](/mk_img/widgets-59-910-6.png)  

### Form

Form widget is two column grid where each row has a label and a widget (usually an input). The last row of the grid will contain the appropriate form control buttons if any should be shown.

![Form](/mk_img/widgets-00-304-7.png)  


### Hyperlink

Hyperlink widget is a text component with appropriate padding and layout. When clicked, the URL opens in your default web browser.

![Hyperlink](/mk_img/widgets-00-544-7.png)  


### Icon

Icon widget is a basic image component that load's its resource to match the theme.

![Icon](/mk_img/widgets-01-413-1.png)  

### Label

Label widget is a label component with appropriate padding and layout.

![Label](/mk_img/widgets-01-051-8.png)  

 
### Progress bar

ProgressBar widget creates a horizontal panel that indicates progress.

![Progress bar](/mk_img/widgets-01-814-9.png)  


ProgressBarInfinite widget creates a horizontal panel that indicates waiting indefinitely An infinite progress bar loops 0% -> 100% repeatedly until Stop() is called.

![Progress bar](/mk_img/widgets-02-220-8.png)  


### RadioGroup

RadioGroup widget has a list of text labels and radio check icons next to each.

![图 16](/mk_img/widgets-02-469-5.png)  


### Select

Select widget has a list of options, with the current one shown, and triggers an event function when clicked.

![图 17](/mk_img/widgets-02-873-8.png)  


### SelectEntry

Select entry widget adds an editable component to the select widget.
Users can select an option or enter their own value.

![图 18](/mk_img/widgets-02-274-0.png)  


### Separator

Separator widget shows a dividing line between other elements.

![图 19](/mk_img/widgets-03-927-0.png)

### Slider

Slider if a widget that can slide between two fixed values.

![图 20](/mk_img/widgets-03-974-1.png)  

### TextGrid

TextGrid is a monospaced grid of characters. This is designed to be used by a text editor, code preview or terminal emulator.

![图 21](/mk_img/widgets-03-299-2.png) 

### Toolbar

Toolbar widget creates a horizontal list of tool buttons.

![图 22](/mk_img/widgets-04-250-9.png) 


## Collection Widgets (in `widget` package)

Collection widgets provide advanced caching functionality to provide high performance rendering of massive data. This does lead to a more complex constructor,
but is a good balance for the outcome it enables.
Each of these widgets uses a series of callbacks, the minimum set is defined by their constructor function, which includes the data size, the creation of template items that can be re-used and finally the function that applies data to a widget as it is about to be added to the display.

### List

List provides a high performance vertical scroll of many sub-items.

![图 23](/mk_img/widgets-04-253-5.png)  


### Table

Table provides a high performance scrolled two dimensional display of many sub-items.
![图 24](/mk_img/widgets-04-887-9.png)  
 

### Tree

Tree provides a high performance vertical scroll of items that can be expanded to reveal child elements..

![图 25](/mk_img/widgets-05-657-0.png)


## Container Widgets (in `container` package)

Container widgets are like regular containers but they provide some additional functionality.

### AppTabs

AppTabs widget allows switching visible content from a list of TabItems. Each item is represented by a button at the top of the widget.

![图 26](/mk_img/widgets-05-001-9.png)   

### Scroll

ScrollContainer defines a container that is smaller than the Content.

![图 27](/mk_img/widgets-05-866-9.png)  


### Split

SplitContainer defines a container whose size is split between two children.

![图 28](/mk_img/widgets-05-910-5.png) 
