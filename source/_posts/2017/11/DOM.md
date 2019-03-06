---
title: 浏览器之DOM
tags: JavaScript
categories: 学习笔记
---
** {{ title }}：** <Excerpt in index | 首页摘要>

## DOM--->Document Object Model
DOM定义了表示和修改文档所需的方法。DOM对象即为宿主对象，由浏览器厂商定义，用来操作html和xml功能的一类对象的集合。也有人称DOM是对HTML以及XML的标准编程接口。
DOM不能操作CSS！！！DOM修改CSS的是通过改变HTML间接改变CSS的。改变不了CSS行间样式，改变的是HTML。

DOM之后一些成组出现的东西都是类数组的形式。

每一个词条就是一个query。每个query都是人工自己写的。因为商家都追求不平凡，要和别家的有区分，绚丽一点儿的。


`var div = document.getElementsByTagName('div')[0];
div.style.width = "100px";
div.style.height = "100px";
div.style.backgroundColor = "red";
在div上永久绑定一个方法，每次点击都变色。
var count = 0;
div.onclick = function () {
  count ++;
  if(count % 2 == 1) {
	this.style.background = "green";
  }else{
	this.style.background = "red";
  }
}`



鼠标监控：
`document.onkeydown = function(e) {
  switch(e.which) {
	case 37:
	  div.style.left = perseInt(div.style.left) - speed + 'px';
	case 38:
	  div.style.top = perseInt(div.style.top) + speed + 'px';
	case 39:
	  div.style.left = perseInt(div.style.left) + speed + 'px';
	case 40:
	  div.style.top = perseInt(div.style.top) - speed + 'px';
  }
}`



## 对节点的增删改查
查
查看元素节点
document代表整个文档
document.getElementById() //元素id 在Ie8以下的浏览器，不区分id大小写，而且也返回匹配name属性的元素
.getElementsByTagName() // 标签名
getElementByName(); //，需注意，只有部分标签name可生效（表单，表单元素，img，iframe）
.getElementsByClassName() // 类名 -> ie8和ie8以下的ie版本中没有，可以多个class一起
.querySelector() // css选择器   在ie7和ie7以下的版本中没有
.querySelectorAll() // css选择器 在ie7和ie7以下的版本中没有
但是他和querySelector这两个方法不常用，因为这两个方法不是实时的，静态的。因为js语言就是实时的，后期只要操作HTML就会重新执行一下页面，所以效率低，但是执行的是实时的。


## DOM结构树  --> 一系列继承关系。

Node也是一个构造函数，他是最顶头的那个函数对象。
```
document.__proto__   就是HTMLDocument
document.__proto__.__proto__    就是Document
document.__proto__.__proto__.__proto__   就是Node
document.__proto__.__proto__.__proto__.__proto__   就是EventTarget   这是一个事件
document.__proto__.__proto__.__proto__.__proto__.__proto__   就是系统上的Object的原型，最终都会追溯到系统上的__proto__
document.documentElement   代表的就是HTML标签
Document  --> HTMLDocument.
document代表的是整个页面文档。Document原型链
```
1. getElementById方法定义在Document.prototype上，即Element节点上不能使用。
2. getElementsByName方法定义在HTMLDocument.prototype上，即非html中的document以外不能使用(xml document,Element)
3. getElementsByTagName方法定义在Document.prototype 和 Element.prototype上
4. HTMLDocument.prototype定义了一些常用的属性，body,head,分别指代HTML文档中的<body><head>标签。
5. Document.prototype上定义了documentElement属性，指代文档的根元素，在HTML文档中，他总是指代<html>元素
6. getElementsByClassName、querySelectorAll、querySelector在Document,Element类中均有定义


`<div><span>1</span></div><span></span>`
`var div = document.getElementsByTagName('div')[0];`
`var span = div.getElementsByTagName('span')[0];`
在开发的时候也是先选中父级，然后在父级下选择要选择的子级。


## 节点的类型
元素节点   —— 1
属性节点   —— 2
文本节点   —— 3
注释节点   —— 8
document  —— 9
DocumentFragment  ——  11 （文档碎片节点）
获取节点类型   nodeType 


## 遍历节点树：
 parentNode -> 父节点  每个节点只有一个父节点(最顶端的parentNode为#document。再往上就是null);
 childNodes -> 子节点们
 firstChild -> 第一个子节点
 lastChild -> 最后一个子节点
 nextSibling->后一个兄弟元素 
 previousSibling->前一个兄弟元素

所说的IE不兼容说的都是IE9以下的。IE10以上都兼容W3C标准了。
基于元素节点树的遍历
parentElement -> 返回当前元素的父元素节点 (IE不兼容)
children -> 只返回当前元素的元素子节点  
node.childElementCount  === node.children.length当前元素节点的子元素节点个数(IE不兼容)
firstElementChild -> 返回的是第一个元素节点(IE不兼容)
lastElementChild -> 返回的是最后一个元素节点(IE不兼容)
nextElementSibling / previousElementSibling ->返回后一个/前一个兄弟元素节点（IE不兼容)


## 节点的四个属性
nodeName
元素的标签名，以大写形式表示,只读
nodeValue
Text节点或Comment节点的文本内容,可读写
nodeType（必须记住，很重要的！）
该节点的类型，只读
attributes
Element 节点的属性集合,比如：<div id='only' class='demo'></div>  div.attributes取出来一个集合放到一个类数组里面。 可以改变值div.attributes[0].value = 'abc'; 能赋值能改值，只能改属性值，也就是更改id的值。

节点的一个方法  Node.hasChildNodes();   有没有子节点，返回结果是false或者true。



## DOM基本操作：
增
`document.createElement();
document.createTextNode();
document.createComment();
document.createDocumentFragment();`
插
`PARENTNODE.appendChild();
PARENTNODE.insertBefore(a, b);`
例如：页面中有`<div>`
`<span></span>`
`</div>`
`var str = document.createElement('strong');`
`var div = document.getElementsByTagName('div')[0];`
`div.insertBefore(str, span)`
就是把创建的strong标签插入到div里面的span之前。


删除标签
`div.removeChild();`   其实是剪切,先找到要删除的标签的父级，然后用的是父级删除其中子级的标签功能，一般都用的是这个，因为想用的时候，如果还保存着就还可以找到。真正的删除是用对象`.remove();`   这是新出的方法，原先没有的。这个是真正的删除了，就再也找不到了。

替换标签也是父级调用，`parentNode.replaceChild(new, origin);`用新的去替换久的。被替换的标签不是被删除了，而是被剪切出来了。



`div.appendChild(p)`,在div标签中加上一些内容或者标签等等。


## Element节点的一些属性
`innerHTML`  这个可以获取标签中的内容。不是追加，是可以覆盖原先的内容的，但是可以用+=的方法追加内容。还可以改变CSS样式的，只要写入就能使用。
`innerText(火狐不兼容) / textContent(老版本IE不好使)`   可取可赋值。但是这个方法一定要慎重的去用。因为会把原先的内容给覆盖的。

## Element节点的一些方法
`ele.setAttribute();` 设置原生DOM上的属性 例如：
`div.setArrtibute('id','only')`   这表示在div上加上id属性。还可以加上一些没有的属性，也就是人为加上去的属性。就比如在标签上人为设置一个属性，data-log='0'; 这个认为加上的属性是用来计算数据量的，算流量的，看这些流量从哪些网站分流出来的，计算给钱。   取data-log值就是：  `div.getAttribute('data-log');`


`ele.getAttribute(); ` 取原生DOM上的属性
`div.getArrtibute();`取出行间属性的值。



## 日期对象Date();

先  `var date = new Date();`
然后就能调用Date()方法的一些方法。
`date.getDate(); ` 从Data对象中返回一个月中的某一天 （1-31）  `date.getDay();`   从Data对象返回一周中的某一天（0-6）
`date.getMonth();` 从Data对象返回月份（0-11）
`date.getFullYear();`  从Data对象以四位数字返回年份（后来才有的方法）
`date.getYear(); `  请使用`data.getFullYear()`方法：一开始就有的方法。只不过这个方法有一个缺点，就是它是用六位表示年月日的。95.03.17；到二千年的时候就不够用了。所以才有了上面的那个完整表示的方法。这就是千年虫问题的出现。当然肯定还有万年虫，不过这个就不是我们需要考虑的问题了，离我们太遥远了~~
`date.getHours();`   返回Data对象的小时（0-23）
`date.getMinutes();`   返回Data对象的分钟（0-59）
`date.getSeconds();`   返回Data对象的秒数（0-59）
`date.getMillseconds();`  返回Data对象的毫秒数（0-999）
`date.getTime(); `    返回1970年1月1日至今的毫秒数（这个方法是最常用的，把耶稣出生的那一年当做人类的纪元年，计算机的纪元年就是1970.01.01，所有的计算机和手机的时间的计算都是根据计算机纪元时间来换算出来的。重点是：这个方法能帮我们算时间差，每个功能用的时间差就是根据这个方法来计算的）
`date.getTimezoneOffset();`   返回本地时间与格林威治标准时间（GMT）的分钟差
`date.getUTCDate();`    根据世界时从Data对象返回月中的一天（1-31）
`date.getUTCDay();`   根据世界时从Data对象返回月份（0-6）
`date.getUTCMonth();`  根据世界时从Data对象返回月份（0-11）
`date.getUTCFullYear();` 根据世界时从Data对象返回四位数的年份
`date.getUTCHours();`  根据世界时返回Data对象的小时（0-23）
`date.getUTCMiutes();`  根据世界时返回Data对象的分钟（0-59）
`date.getUTCSeconds();`  根据世界时返回Date对象的秒钟（0-59）
`date.getUTCMillseconds();` 根据世界时返回Date对象的毫秒（0-999）
`date.parse();`   返回1970年1月1日午夜到指定日期（字符串）的毫秒数
人为设置一个时间点，到设置好的时间点执行一个功能，比如淘宝上的定时抢购，就是到达人为设置的时间点之后立即执行函数功能。
`date.setDate();`   设置Date对象中月的某一天（1-31）
`date.setMonth();`   设置Date对象中月份（0-11）
`date.setFullYear();`  设置Date对象中的年份（四位数字）
`date.setYear();`     请使用setFullYear()方法代替
`date.setHours();`    设置Date对象中的小时（0-23）
`date.setMinutes();`  设置Date对象中的分钟（0-59）
`date.setSeconds();`    设置Date对象中的秒钟（0-59）
`date.setMillseconds();`  设置Date对象中的毫秒（0-999）
`date.setTime();`      以毫秒设置Date对象
`date.toSource();`    返回该对象的源代码
`date.toString();`   把Date对象转换为字符串
`date.toTimeString();`  把Date对象的时间部分转换为字符串
`date.toDateString();`  把Date对象的日期部分转换成字符串


# JS定时器
## setInterval()
   `setInterval(function() {}, time);`time只能赋一次值，并不能通过改变time的值来动态改变隔得时间。定时器并不准。如何看时间准不准呢？写一个函数如下：
```
var firstTime = new Date().getTime();
setInterval(function () {
 var lastTime = new Date().getTime();
 console.log(lastTime - firstTime);
 firstTime - lastTime;
}, 1000);
```
在控制台上打印的结果并不总是1000毫秒，所以这个方法的时间间隔并不是很准的。所以要是做的功能对时间有很精确的时间要求就不能寄希望于这个方法上的。与系统执行代码所消耗的时间还有。这个方法的排列机制是基于红黑数的。每一次这个方法都会返回一个唯一标示。应用就是VIP电影有试看时间，就是用这个方法。

`setTimeout();`   只执行一次。
`clearInterval();`
`clearTimeout();`
全局对象window上的方法，内部函数this指向window
注意 ：`setInterval("func()",1000);`



## 查看滚动条的滚动距离
`window.pageXOffset/pageYOffset`
IE8及IE8以下不兼容
IE8及IE8以下用的下面这个方法：
`document.body/documentElement.scrollLeft/scrollTop`
但是这两个方法是在IE浏览器中到底哪个能用是不一定的，又但是这两个问题是互相冲突的，一个有值另一个就没有值了。所以就让两个值加起来用。
兼容性比较混乱，用时取两个值相加，因为不可能存在两个同时有值

## 练习：
**封装兼容性方法，求滚动轮滚动距离**

`getScrollOffset()`
```
function getScrollOffset() {
  if(window.pageXOffset) {
    return {
	x : window.pageXOffset,
	y : window.pageYOffset
    }
  }else{
    return {
	x : document.body.scrollLeft + document.documentElement.scrollLeft,
	y : document.bodu.scrollTop + document.documentElement.scrollTop
    }
  }
}
```
如果放大页面的尺寸。那么返回的可视区窗口就是放大之后的可视区的实际尺寸。

就在编程的html标签的上面还有一个<!DOCTYPE html>表示 文档类型，当有这个标签的时候浏览器的渲染模式就是标准模式，没有这个标签的时候浏览器的渲染模式就是怪异模式。渲染就是识别语法并绘制成页面。
标准模式：正常的渲染模式。一般除了IE浏览器其他的浏览器的与之前的变动并不是很大，所以也用不着去启用怪异模式。
怪异模式又叫混杂模式：试图去兼容浏览器之前的版本。

**有一个方法能看当前浏览器是在什么渲染模式下：**
`document.compatMode`     当返回值为："CSS1Compat";  表示标准模式下			当返回值为："BackCompat"  表示在怪异模式下，向后兼容

## 查看视口的尺寸的方法：
`window.innerWidth/innerHeight`
IE8及IE8以下不兼容
标准模式下，任意浏览器都兼容的方法：
`document.documentElement.clientWidth/clientHeight`
适用于怪异模式下的浏览器的方法：
`document.body.clientWidth/clientHeight`


## 练习：
**封装兼容性方法，返回浏览器视口尺寸**
`getViewportOffset()`
```
function getViewportOffset() {
  if(window.innerWidth) {
    return {
	w : window.innerWidth,
	h : window.innerHeight
    }
  }else if(document.compatMode === "BackCompat"){     
	return {
	  w : document.body.clientWidth,
	  h : document.body.clientHeight
	}
  }else if(document.compatMode === "CSS1Compat"){
	return {
	  w : document.documentElement.clientWidth,
  	  h : document.documentElement.clientHeight
	}
  }
}
```
## 比较获取查看窗口尺寸的方法的取值差异：
使用`$(window).width() `与 `$(window).height();`
获取的是屏幕可视区域的宽高，不包括滚动条与工具条。
`window.outerWidth` 与 `window.outerHeight;`
获取的是加上工具条与滚动条窗口的宽高与高度(总高度算上全部滚动条的高度)。
`window.innerWidth `与 `window.innerHeight;`
获取的是可视区域的宽高，但是宽度包含了纵向滚动条的宽度。
`document.documentElement.clientWidth `与 `document.documentElement.clientHeight;`
获取的是屏幕可视区域的宽高，不包括滚动条与工具条，跟JQuery的获取的结果是一样的。
`document.body.clientWidth` 与 `document.body.clientHeight;`
获取的是宽度可视区域的宽度，获取的高度是是body内容的高度，如果内容只有200px，那么这个高度也是200px，如果想通过它得到屏幕可视区域的宽高，需要样式设置如下：
```
body {
 height: 100%;
 overflow: hidden;
}
body, div, p, ul {
 margin: 0;
 padding: 0;
}
```
## 兼容性：
1. window.innerWidth 和 window.outerWidth 属性方法IE8以及以下不支持，得到的值为undefined。
2. 测试浏览器IE，火狐，谷歌，Safari都支持怪异下的方法属性`document.documentElement.clientWidth` 与 `document.documentElement.clientHeight`。

结论：
获取屏幕的可视区域的宽高可使用jQuery的方式获得，也可以使用原生js获得，即：`document.documentElement.clientWidth `与 `document.documentElement.clientHeight` 方法。



## 查看元素的几何尺寸
`domEle.getBoundingClientRect();`
兼容性很好，返回的是元素相对其他的最近的有定位的元素的真实的值
该方法返回一个对象，对象里面有left,top,right,bottom等属性。left和top代表该元素左上角的X和Y坐标，right和bottom代表元素右下角的X和Y坐标
height和width代表该元素真实的自身可视高度和宽度。
height和width属性老版本IE并未实现
返回的结果并不是“实时的”，并且在Google浏览器中扩大缩小页面的内容left和right的值是会跟着变的。其他值是可视区域真实值。
 

## 查看元素的尺寸
`dom.offsetWidth，dom.offsetHeight`
## 查看元素的位置
`dom.offsetLeft, dom.offsetTop`
不管dom自身有没有定位，他都会把他跟他最近的有定位的父级元素的距离返回出来。对于无定位父级的元素，返回相对文档的坐标。对于有定位父级的元素，返回相对于最近的有定位的父级的坐标。在浏览器下缩放对该方法的取值是有影响的，返回的是真实的可视区域的大小值。
`dom.offsetParent`
返回最近的有定位的父级，如无，返回body，    
`documen.body.offsetParent `返回null


## 练习：
eg：求元素相对于文档的坐标getElementPosition
`function getElementPosition(dom) {
  if(dom.offsetParent !== body) {
    return {
	  x : dom.offsetLeft,
  	  y : dom.offsetTop
	}
  }
}`






## 让滚动条滚动
window上有三个方法
`scroll(),scrollTo()       scrollBy();`
三个方法功能类似，用法都是将x,y坐标传入。即实现让滚动轮滚动到当前位置。前两个方法不做累加，是定点到当前所设置位置。
区别：scrollBy()会在之前的数据基础之上做累加。

eg：利用scrollBy() 快速阅读的功能    加锁式的编程方法
```
<div style='width:100px;height:100px;background-color:orange;color:#fff;font-size:40px;font-weight:bold;text-align:center;line-height:100px;position:fixed;bottom:200px;right:50px;border-radius:50%;opacity:0.5;'> start </div>
<div style='width:100px;height:100px;background-color:red;color:#fff;font-size:40px;font-weight:bold;text-align:center;line-height:100px;position:fixed;bottom:400px;right:50px;border-radius:50%;opacity:0.5;'> stop </div>
<script>
    var start = document.getElementsByTagName('div')[0];
    var stop = document.getElementsByTagName('div')[1];
    var key = true;
    var timer = 0;
    start.onclick = function () {
      if(key) {
          timer = setInterval(function () {
      window.scrollBy(0, 10);

          }, 100);
          key = false;
        }
    }
    stop.onclick = function () {
      clearInterval(timer);
      key = true;
    }
</script>
```


## 间接控制脚本化CSS属性的方法：
读写元素css属性
`dom.style.prop`
可读写行间样式，只能读写行间的值，写到别的地方是读写不出来的。写入操作的唯一方法，其他的方法只能读不能写入了。
没有兼容性问题，碰到float这样的关键字属性，前面应加css
eg:float — > cssFloat
复合属性必须拆解，组合单词变成小驼峰式写法
写入的值必须是字符串格式



## 查询计算样式
这个方法传入的第二个参数null传入的是什么呢？传入的是获取伪元素，原生的方法。获取伪元素的属性，伪元素的display默认是inline-block；例如获取一个DOM元素div的伪元素的样式表。就是`window.getComputedStyle(div, "after")['prop']`就是获取的这个div上的伪元素属性after的一些值，但是不能操作，只能取出来。如何改变伪元素的需求呢？当点击一个DOM元素div的时候，让div上的一个伪元素变化。也就是操作CSS的样式上加上一些东西。改变原先的class名字而且先写好CSS样式。

`window.getComputedStyle(ele,null);`显示获取出来的是显示展示能看见的真实值，获取出来的是一个对象，还可以.属性，获取出具体的一个属性值。
计算样式只读
返回的计算样式的值都是绝对值，没有相对单位（em）
IE8 及 IE8以下不兼容

查看IE8及IE8以下的属性的特有的方法
查询样式
`ele.currentStyle`
计算样式只读
返回的计算样式的值不是经过转换的绝对值
IE独有的属性

## 练习
**封装兼容性方法getStyle(obj,prop);**  这个方法获取的很靠谱。并且这个方法获取的值是字符串形式的eg“8px”；所以用的时候需要用parseInt()方法来把后面的字符串截断成纯数字形式的，这样我们才能使用。

`function getStyle(elem, prop) {
  if(window.getComputedStyle) {
    return window.getComputedStyle(elem, null)[prop];
  }else{
    return elem.currentStyle[prop];
  }
}`




# JSON：
JSON是一种传输数据的格式（以对象为样板，本质上就是对象，但用途有区别，对象就是本地用的，json是用来传输的）   最开始的时候前后端交流的是使用xml的形式的，但是现在用的是JSON的形式；
可以把JSON当成一个构造函数，它里面就有如下两个方法：
JSON.parse();   string--->json
JSON.stringify();   json---->string
是因为我们传输的信息就是字符串形式的：可以互相转换。

## 静态类：
js是面向过程正在朝面向对象过渡的过程：例如：
setInterval() 这个方法是window上的，js上定义的一些方法
Math()这个方法，5年前是定义在function Math() {}上的；现在是一个对象。一些方法直接定义在了Math() 身上，所以想用的时候就不用new了，各有各的好处。他们身上的方法就叫做静态方法，静态类的总称。Math.floor()向下取整；Math.ceil()向上取整；Math.abs()取绝对值(absolute);Math.random()  0-1之间的任意小数；Math.sqrt()开方；


## 时间线：
js加载的缺点：加载工具方法没必要阻塞文档，使得js加载会影响页面效率，一旦网速不好，那么整个网站将等待js加载而不进行后续渲染等工作。
有些工具方法需要按需加载，用到再加载，不用不加载。



## javascript 异步加载 的 三种方案
1. defer 异步加载，下载完不是立刻执行，是要等到dom文档全部解析完才会被执行。只有IE能用。IE10以下的可用。不光是页面内的js文件还是页面外引入的都会变成异步加载的。
<script type="text/javascript" defer="defer" src="xxx.js"></script>可以简化成defer
就比如说页面中有一个img标签，先解析，加到DOM树上；再加载，比如图片需要加载图片的二进制文档，也就是下载，下载完了也就是加载完了；最后绘制渲染出来。

2. async 异步加载，加载完就执行，async只能加载外部脚本，不能把js写在script 标签里。这个方法只能是加载外部js引用时才能异步加载。
<script type="text/javascript" async="async" src="xxx.js"></script>
asynchronous javascript and xml ----->  Ajax

1和2 执行时也不阻塞页面，但是不能两个同时用。一般公司都会采用牺牲IE的方法只用async的。

3. 创建script，插入到DOM中，加载完毕后callBack

## 按需加载异步下载js的兼容性写法：
```
function loadScript(url, callback) {
  var script = document.createElement('script');
  script.type = "text/jacascript";
  script.src = url;
  if(script.readyState) {
    script.onreadystatechange = function () {
      if(script.readyState == "complete" ||  script.readyState == "loaded") {
	  callback();
      }
    }
  }else{
    script.onload = function () {
      callback();
    }
  }
  document.body.appendChild(script);
}
loadScript('tools.js', getScrollOffset);
```
这里有一个问题，就是还没等到工具js包下载完呢，就调用这个包里面的方法肯定会报错的。解决方法为可以`loadScript('tools.js', function() {console.log(getScrollOffset())});`或者把tools.js里面的方法都整合到一个对象里面：在js包里： `var obj={getScrollOffset: function() {console.log('a')}};`然后再把上面这个方法也改了，改成  `obj[callback]();`这样就可以这样用了`loadScript('tools.js', 'getScrollOffset');`



## js时间线：

1. 创建Document对象，开始解析web页面。解析HTML元素和他们的文本内容后添加Element对象和Text节点到文档中。这个阶段document.readyState = 'loading'。
2. 遇到link外部css，创建线程加载，并继续解析文档。
3. 遇到script外部js，并且没有设置async、defer，浏览器加载，并阻塞，等待js加载完成并执行该脚本，然后继续解析文档。
4.  遇到script外部js，并且设置有async、defer，浏览器创建线程加载，并继续解析文档。
对于async属性的脚本，脚本加载完成后立即执行。（异步禁止使用document.write()因为该方法会清空之前写的所有文档流）
5. 遇到img等，先正常解析dom结构，然后浏览器异步加载src，并继续解析文档。
6. 当文档解析完成，document.readyState = 'interactive'。
7. 文档解析完成后，所有设置有defer的脚本会按照顺序执行。（注意与async的不同,但同样禁止使用document.write()）;
8. 当文档解析完成后，document对象触发DOMContentLoaded事件，一触发就标志着解析完毕了。这也标志着程序执行从同步脚本执行阶段，转化为事件驱动阶段。
9. 当所有async的脚本加载完成并执行后、img等加载完成后，document.readyState = 'complete'，也就是当所有的东西都加载完成之后，window对象触发load事件。加载完成就开始渲染，所有的东西都就画出来了，用户可以看见东西了。
10. 从此，以异步响应方式处理用户输入、网络事件等。


**绑定事件的时候，无论多少的单词都不会大写的，但是只有一个特殊的就是'DOMContentLoaded'。**
`document.readyState 三个阶段：loading、interactive、comolete.`
```
document.addEventListener('DOMContentLoaded', function () {
	console.log(document.readyState)
}, false);
```
这样打印出来就是： 'interactive'
再复习一下第三个参数false是什么意思呢，就是捕获，绑定事件监听的事件处理模型只能有两种行为，一个是捕获，另一个是冒泡。true的时候就是冒泡。



## 练习题：

**请编写一段JavaScript脚本生成下面这段DOM结构。要求：使用标准的DOM方法或属性。**
```
<div class="example">
	<p class="slogan">姬成，你最帅!</p>
</div>
```
提示 dom.className 可以读写class
```
var div = document.createElement('div'),
    p = document.createElement('p');
p.innerText = '姬成，你最帅！';      也可以  var text = document.createTextNode('姬成，你最帅！');
div.appendChild(p);
document.body.appendChild(div);
div.setAttribute('class', 'example');
p.setAttribute('class', 'slogan');
有一个注意的点就时appendChild()括号里没有''!!! 应该直接在里面写原生DOM   appendChild(div)
```

1. 封装函数insertAfter()；功能类似insertBefore();
提示:可忽略老版本浏览器，直接在Element.prototype上编程
```
Element.prototype.insertAfter = function (targetNode, afterNode) {
  var beforeNode = afterNode.nextElementSibling;
  if(beforeNode) {
    this.insertBefore(targetNode, beforeNode);
  }else{
    this.appendChild(targetNode);
  }
}
```


2. 将目标节点内部的节点顺序逆序。
eg:
```
<div> <a></a> <em></em></div> 
<div><em></em><a></a></div>

Element.prototype.reverse = function (dom) {
  var len = this.length;
  for(var i = 0; i < len; i ++) {
    this.

  }

}
```



# 作业区：

1. 遍历元素节点树，要求不能用children属性
```
 <div>
   <span>
     <p>
	<strong>
	  <em></em>
	</strong>
     </p>
   </span>
 </div>

var div = document.getElementByTagName('div')[0];
function retElementChild(node) {
  var temp = {
     length : 0,
     push : Array.prototype.push,
     splice : Array.prototype.splice
  },
      child = node.childNodes,
      len = child.length;
  for(var i = 0; i < len; i ++) {
     if(child[i].nodeType === 1) {
	temp.push(child[i]);
     }
  }
}

retElement(div)
```
2. 封装函数，返回元素e的第n层祖先元素
```
 <div>
   <span>
     <p>
	<strong>
	  <em></em>
	</strong>
     </p>
   </span>
 </div>

function retParent(elem, n) {
  while(n && elem) {
    elem = elem.parentElement;
    n --;
  }
  return elem;
}
```

3. 封装函数，返回元素e的第n个兄弟元素节点，n为正，返回后面的兄弟元素节点，n为负，返回前面的，n为0，返回自己。
```
 <div>
   <span>
     <p>
	<strong>
	  <em></em>
	</strong>
     </p>
   </span>
 </div>

function retSibing(e, n) {
  while(n && e) {
    if(n > 0) {
	if(e.nextElementSibling) {
          e = e.nextElementSibling;
	}else{
	  for(var e = e.nextSibling; e && e.nodeType != 1; e = e.nextSibling);
	}
	n --;
    }else{
	if(e.previousElementSibling) {
	  e = e.previousElementSibling;
	}else{
	  for(var e = e.previousSibling; e && e.nodeType != 1; e = e.previousSibling);
	}
	n ++;
    }
  }
  return e;
}
```
4. 编辑函数，封装children功能，解决以前部分浏览器的兼容性问题,就是用自己的方法实现children方法。
```
 <div>
   <span>
     <p>
	<strong>
	  <em></em>
	</strong>
     </p>
   </span>
 </div>

var div = document.getElementsByTagName('div')[0];
Element.prototype.myChildren = function () {
 var child = this.childNodes,
     len = child.length,
     arr = [];
 for(var i = 0；i < len; i ++) {
    if(child[i].nodeType == 1) {
	arr.push(child[i]);
    }
 }
 return arr;
}
div.myChildren();    结果为：[span]
```

5. 自己封装hasChildren()方法，不可用children属性。如果有元素节点返回true，如果没有返回false。
```
 <div>
   <span>
     <p>
	<strong>
	  <em></em>
	</strong>
     </p>
   </span>
 </div>
var div = document.getElementsByTagName('div')[0];
Element.prototype.hasChildren = function () {
  var child = this.childNodes,
      len = child.length,
      arr = [];
  for(var i = 0; i < len; i ++) {
     if(child[i].nodeType == 1) {
	return true;
     }
  }
  return false;
}

div.hasChildren();   结果：true;
```