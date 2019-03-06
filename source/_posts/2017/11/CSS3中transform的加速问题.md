---
title: 使用CSS3开启GPU硬件加速提升网站动画渲染性能
tags: CSS3
categories: 学习笔记
---

** {{title}} ** <Excerpt in index | 首页摘要>

今天再来说一下CSS3中的新特性，transform。说他之前先来解释图片中的两个格式的区别：PNG8和PNG24。
# png8
每一张“png8”图像，都最多只能展示256种颜色，所以“png8”格式更适合那些颜色比较单一的图像，例如纯色、logo、图标等；因为颜色数量少，所以图片的体积也会更小；
# png 24
每一张“png24”图像，可展示的颜色就远远多于“png8”了，最多可展示的颜色数量可多达1600万；所以“png24”所展示的图片颜色会更丰富，图片的清晰度也会更好，图片质量更高，当然图片的大小也会相应增加，所以“png24”的图片比较适合像摄影作品之类颜色比较丰富的图片；

所以一些网站如果需要加载一些很大的PNG24类型的图片的话，那么图片加载的时间就会有点长甚至导致网站出现卡顿现象，进而影响用户体验。我们如何解决这个问题呢？或者说如何优化这个麻烦呢？这就需要我们今天要说到的CSS3中的transform属性了。为什么添加这个属性之后就会提升性能呢？因为为动画DOM元素添加CSS3样式-webkit-transform:transition3d(0,0,0)或-webkit-transform:translateZ(0);，这两个属性都会开启GPU硬件加速模式，从而让浏览器在渲染动画时从CPU转向GPU，其实说白了这是一个小伎俩，也可以算是一个Hack，-webkit-transform:transition3d和-webkit-transform:translateZ其实是为了渲染3D样式，但我们设置值为0后，并没有真正使用3D效果，但浏览器却因此开启了GPU硬件加速模式。
　　这种GPU硬件加速在当今PC机及移动设备上都已普及，在移动端的性能提升是相当显著地，所以建议大家在做动画时可以尝试一下开启GPU硬件加速。

当然也可以这样开启所有浏览器的GPU硬件加速：

>-webkit-transform: translateZ(0);
-moz-transform: translateZ(0);
-ms-transform: translateZ(0);
-o-transform: translateZ(0);
transform: translateZ(0);

或者：

>-webkit-transform: translate3d(0,0,0);
-moz-transform: translate3d(0,0,0);
-ms-transform: translate3d(0,0,0);
-o-transform: translate3d(0,0,0);
transform: translate3d(0,0,0);

但是我们要注意的是：开启GUI加速之后，会出现一些意想不到的BUG问题。当你有多个position:absolute;元素添加-webkit-transform:transition3d(0,0,0);开启GPU硬件加速之后，会有几个元素凭空消失，调试许久无果遂Google之，国内暂时没有人发表过关于这类问题的文章，于是在国外网站找呀找，找到了很多与我遇到同样问题的人，但都没有真正靠谱的解决办法，这可能是跟添加-webkit-transform之后chrome尝试使用GPU硬件加速有关系。
在使用-webkit-transform尝试对很多DOM元素编写3D动画时，尽量不要对这些元素及他们的父元素使用position:absolute/fixed。(其实这种情况很难避免)

通过-webkit-transform:transition3d/translateZ开启GPU硬件加速之后，有些时候可能会导致浏览器频繁闪烁或抖动，可以尝试以下办法解决之：
>-webkit-backface-visibility:hidden;
-webkit-perspective:1000;

通过-webkit-transform:transition3d/translateZ开启GPU硬件加速的适用范围：

1. 使用很多大尺寸图片(尤其是PNG24图)进行动画的页面。
2. 页面有很多大尺寸图片并且进行了css缩放处理，页面可以滚动时。
3. 使用background-size:cover设置大尺寸背景图，并且页面可以滚动时。(详见: <https://coderwall.com/p/j5udlw> )
4. 编写大量DOM元素进行CSS3动画时(transition/transform/keyframes/absTop&Left)
5. 使用很多PNG图片拼接成CSS Sprite时