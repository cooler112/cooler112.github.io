---
title: CSS over-flow的使用
date: 2021-01-16 14:07:59
tags: CSS
categories: 前端开发
---



当元素溢出内容区，需要使用overflow属性来进行裁剪

overflow有以下几个可选值：

| visible | 默认值。内容不会被修剪，会呈现在元素框之外。             |
| ------- | -------------------------------------------------------- |
| hidden  | 内容会被修剪，并且其余内容是不可见的。                   |
| scroll  | 内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。 |
| auto    | 如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。 |
| inherit | 规定应该从父元素继承 overflow 属性的值。                 |

**overflow-X | overflow-y**

　　overflow-x和overflow-y的属性原本是IE浏览器独自拓展的属性，后来被CSS3采用，并标准化。overflow-x主要用来定义对水平方向内容溢出的剪切，而overflow-y主要用来定义对垂直方向内容溢出的剪切

　　[注意]如果overflow-x和overflow-y值相同则等同于overflow。如果overflow-x和overflow-y值不同，且其中一个值显式设置为visible或未设置默认为visible，而另外一个值是非visible的值。则visible值会被重置为auto

两个独有的值：

no-display：如果内容不适合内容框，则删除整个框。

no-content：如果内容不适合内容框，则隐藏整个内容。