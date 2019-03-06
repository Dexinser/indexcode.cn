---
title: CSS3新增加的功能和属性方法--之选择器
tags: CSS3
categories: 必备知识
---

# CSS3---选择器

提供了更加强大且精准的选择器，提供多种背景填充方案，可以实现渐变颜色，可以改变元素的形状、角度等，可以加阴影效果，报纸布局，弹性盒子，ie6混杂模式的盒模型，新的计量单位，动画效果等等等...

  在CSS3的一些新特性或方法还没正式使用之前，有一些浏览器商为了竞争用户使用人数或者说是为了一些商业目的，在CSS3还没有正式通过使用时就在自家的浏览器上实现了CSS3新出的功能。而这些浏览器商为了显示出这是自家的浏览器上实现的CSS3新功能，所以他们就在新实现的CSS3功能的属性之前加上了自家的标志。添加的前缀标志如下：
  在编写CSS3样式时，不同的浏览器可能需要不同的前缀。它表示该CSS属性或规则尚未成为W3C标准的一部分，是浏览器的私有属性，虽然目前较新版本的浏览器都是不需要前缀的，但为了更好的向前兼容前缀还是少不了的。
### 以CSS3新属性border-radius为例：
> -webkit-border-radius          
> Chrome和Safari
> 
> -moz-border-radius    
> Firefox
> 
> -ms-border-radius         
> IE
> 
> -o-border-radius          
> Opera

CSS3新添加的属性方法有哪些?
## 1
添加圆角 -- border-radius 这是一个复合属性，分别为代表左上角、右上角、右下角、左下角；而且他们的所代表的左上角还是一个小的复合属性，又可以分成x轴和y轴的偏移量。 还有一种写法border-radius： 1em 2em 3em 4em / 2em 3em 4em 5em;
## 2
添加盒子阴影 --  box-shadow  这也是一个复合属性，是添加盒子阴影的方法。
box-shadow: X轴偏移量 Y轴偏移量 [阴影模糊半径] [阴影扩展半径] [阴影颜色] [投影方式];  []里面的属性代表可以省略的属性。需要注意的是最后的一个可选属性即投影方式默认是outset投影方式，如果想设置成默认向外投影方式的话，一定注意不要把这个属性值写上去，写上去的话就不好使了，就没有阴影了，但是如果想改变投影方式为其他的形式需要写上去的。同一盒子，可以同时加多个阴影，阴影之间用“,”隔开。
## 3
添加文本阴影  text-shadow 
语法
text-shadow:X-Offset Y-Offset blur color;
X-Offset：表示阴影的水平偏移距离，其值为正值时阴影向右偏移，反之向左偏移；
Y-Offset：是指阴影的垂直偏移距离，如果其值是正值时，阴影向下偏移，反之向上偏移
Blur：是指阴影的模糊程度，其值不能是负值，如果值越大，阴影越模糊，反之阴影越清晰，如果不需要阴影模糊可以将Blur值设置为0；
Color：是指阴影的颜色，其可以使用rgba色。
## 4
颜色值RGBA  再原先RGB的基础上添加了透明度这一参数。
## 5
CSS3的渐变分为两种
1）线性渐变（linear - to）
语法: linear-gradient([direction], color [percent], color [percent], …)
[] 内为选填
direction角度的单位为 “deg” 也可以用to bottom, to left, to top left等的方式来表达
2）径向渐变（radial - at）
语法:radial-gradient(shape at position, color [percent] , color, …)
shape:放射的形状，可以为原型circle，可以为椭圆ellipse
position: 圆心位置，可以两个值，也可以一个，如果为一个时，第二个值默认center 即 50%。值类型可以为，百分数，距离像素，也可以是方位值(left,top...); /*x 轴主半径 y轴次半径*/
## 6
文字边界换行
word-wrap:normal|break-word;
## 7
可以下载网上的好看的字体想要引入的话就用下面的方式把下载到包用到我们的网页上，字体的包有很多格式，有的浏览器不支持某一种格式的话就换一种：
`font-face
@font-face{
font-family:”myFirstFont”;
src:url('Sansation_Light.ttf'),
url(‘Sansation_Light.eot') format(‘eot’)；下载前面的优先选用
}
@font-face {
    font-family: 'diyfont';
    src: url('diyfont.eot'); /* IE9+ */
    src: url('diyfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
         url('diyfont.woff') format('woff'), /* chrome、firefox */
         url('diyfont.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
         url('diyfont.svg#fontname') format('svg'); /* iOS 4.1- */
}`
[字体](http://www.w3cplus.com/content/css3-font-face) (字体包下载地址)
[字体](www.dafont.com) (字体包下载地址)

## 8
border-image方法--边框应用背景
border-image: url(xxx.png)  number 
               stretch 很好理解就是拉伸，有多长拉多长。有多远“滚”多远
               repeat (和4角上 同等大小图片进行平铺  当边框中间区域长度不是4角图片大小的整数倍时 会被切割)
               铺满(round)(4角上的图片 进行拉伸平铺  不会被切割)
（共三个参数）
number 为截取指定图片四周的宽度作为border的背景填充部分(截取图可按border-width 大小伸缩), number为一个数字时是复合写法。最后一个属性为border-image的展示策略

## 9
背景图片起始位置background-origin
语法：
background-origin ： border-box | padding-box | content-box;
参数分别表示背景图片是从边框，还是内边距（默认值），或者是内容区域开始显示。

## 10
裁剪背景图片background-clip
语法：
background-clip ： border-box | padding-box | content-box | no-clip
参数分别表示从边框、或内填充，或者内容区域向外裁剪背景。no-clip表示不裁切，和参数border-box显示同样的效果。background-clip默认值为border-box。
text : background-clip : text ;
从前景内容的形状（比如文字）作为裁剪区域向外裁剪，如此即可实现使用背景作为填充色之类的遮罩效果。这个很炫哦~~
注意：webkit独有属性，且必须配合text-fill-color属性
`-webkit-background-clip:text;-webkit-text-fill-color:transparent;
text-fill-color:-webkit-background-clip;
-webkit-background-clip: text;
-webkit-text-fill-color:transparent;`

## 11
背景图片尺寸background-size
设置背景图片的大小，以长度值或百分比显示，还可以通过cover和contain来对图片进行伸缩。
语法：
background-size: auto | <长度值> | <百分比> | cover | contain
取值说明：
1. auto：默认值，不改变背景图片的原始高度和宽度；
2. <长度值>：成对出现如200px 50px，将背景图片宽高依次设置为前面两个值，当设置一个值时，将其作为图片宽度值来等比缩放；
3. <百分比>：0％~100％之间的任何值，将背景图片宽高依次设置为所在元素宽高乘以前面百分比得出的数值，当设置一个值时同上；
4. cover：用一张图片铺满整个背景，如果比例不符，则截断图片
5. contain：尽量让背景内，存在一整张图片


