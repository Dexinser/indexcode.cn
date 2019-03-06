---
title: CSS3动画的使用方法
tags: CSS3
categories: 必备知识
---
# CSS3动画的使用方法

## 形状变换  —   高级动画基础 

### transform -- 可以实现元素的形状、角度、位置等的变化。
他的值有很多种：
#### 旋转：
rotate(); 以x/y/z为轴进行旋转，默认为z
rotatex(), rotatey(), rotatez(), rotate3d(x, y, z, angle) x, y, z --->
#### 缩放：
scale(); 以x/y为轴进行缩放
scale(x, y) 接受两个值，如果第二参数未提供，则第二个参数使用第一个参数的值
scalex(),scaley() 值是数字表示倍数，不加任何单位
scalez()
scale3d()  scale3d(sx,sy,sz)
#### 扭曲：
skew(); 对元素进行倾斜扭曲
skew(x, y);接受两个值，第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则默认值为0
skewx(), skewy()
#### 平移：
translate(); 可以移动距离,相对于自身位置。
translate(x, [y])
translatex(),translatey(),translatez(),translate3d(x, y, z)  正规的写法是XYZ都应该是大写的。括号里面的值可以是像素(px, %)  当不知道元素自身的宽高是应该用这个百分比法来进行居中处理(-50%,-50%);
#### transform-origin 变换原点
任何一个元素都有一个中心点，
默认情况下，其中心点是居于元素x轴和y轴的50%处。配合缩放的方法来使用，根据中心点的位置进行缩放。

#### transition  过渡动画
transition  属性是css3的一个复合属性，主要包括一下几个子属性
transition-property:指定过渡或动态模拟的css属性
transition-duration:指定过渡所需要的时间
transition-timing-function:指定过渡函数
transition-delay:指定开始出现的延迟时间

transition  过渡动画可以参与过渡的属性

#### animation -- 动画铺垫
动画关键帧 
@keyframes 

animation 动画会按照keyframes 关键帧里面指定的帧状态而过渡执行。
0% - 100% 代表动画的时间过渡
@keyframes demoMove{
0%{ background-color:red;}
10%{ background-color:green;}
20%{ background-color:white;}
50%{ width:200px;}
100%{ height:200px;}

animation 属性为css3的复合属性，主要包括以下子属性
animation-name:  此属性为执行动画的 keyframe 名
animation-duration:此属性为动画执行的时间
animation-timing-function:指定过渡函数速率
animation-delay: 执行延迟时间
animation-direction: normal/reverse/alternate/alternate-reverse; 
animation-iteration-count:infinite/number;
animation-fill-mode:forwards/backwards/both/none;

animation-iteration-count:
            属性主要用来定义动画的播放次数。
            n 播放次数
            infinite 无限次
       animation-direction:
            属性主要用来设置动画播放方向
            normal  默认值。动画按正常播放。    测试 »
            reverse 动画反向播放。 测试 »
            alternate   动画在奇数次（1、3、5...）正向播放，在偶数次（2、4、6...）反向播放。    测试 »
            alternate-reverse   动画在奇数次（1、3、5...）反向播放，在偶数次（2、4、6...）正向播放。    测试 »

animation-play-state:
            属性主要用来控制元素动画的播放状态。
            running 播放
            paused  暂停
       animation-fill-mode:
            属性定义在动画开始之前和结束之后发生的操作。主要具有四个属性值：
            none:
                默认值，表示动画将按预期进行和结束，在动画完成其最后一帧时，动画会反转到初始帧处
                
            forwards:
                表示动画在结束后继续应用最后的关键帧的位置
            backwards:
                会在向元素应用动画样式时迅速应用动画的初始帧
            both:
                元素动画同时具有forwards和backwards效果







