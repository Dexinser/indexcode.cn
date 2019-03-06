---
title: CSS小技巧
tags: CSS
categories: 学习笔记
---
** {{ title }}：** <Excerpt in index | 首页摘要>
清除浮动元素的技巧解析:
display:block;
height:0;
line-height:0;
content:' ';
clear:both;
visibility:hidden;
这些是设置在元素的伪元素上的，比如要是想在当前元素的后面设置清除浮动，那就设置元素的:after设置上面的属性；要是想在当前元素的前面清除浮动，那就设置当前元素的:before上设置前面的属性。