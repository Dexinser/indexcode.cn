---
title: JQuery
tags: JavaScript
categories: 学习笔记
---
** {{ title }}：** <Excerpt in index | 首页摘要>

## jQuery笔记
jQuery是一个非常优秀的js库。现在有一万行以上的代码了，重在他的封装思想，使用方法会用就可以先查先用。移动端有一个zepto的库就是从jQuery中精简来的。因为移动端的网速没有PC端的快、还有就是不稳定。
像百度等等的一些比较大的互联网公司一般都会有在网上的jQuery库的，我们可以在网上直接应用他们的jQuery库，可以用src的方法直接引用过来，当然我们也可以下载下来直接在我们的服务器上直接调用。


### 简单模仿jQuery的功能：
```
(function() {
  function jQuery (selector, content) {
	return new jQuery.prototype.init(selector, context)
  }
  jQuery.prototype.init = function (selector, context) {
    var DomArray = document.getElementByTagName(selector, context);
    for(var i = 0; i < DomArray.length; i ++) {
      this[i] = DomArray[i];		
    }
    this.length = DomArray.length;
  }
  jQuery.prototype.css = function (parm) {
    for (var i = 0; i < this.length; i ++) {
      for () {
        this[i].style[attr] = parm[attr];
      }
    }
  }
  jQuery.prototype.init.prototype = jQuery.prototype;
  window.$ = window.jQuery = jQuery;
})();
$('div').css({width: '100px', height: '100px', background: 'red'});
```
这样就能使用我们所写的jQuery实现一般的功能。


> init()方法一般在公司里是用来初始化的作用，整个功能的开始或者是主入口。

## jQuery的选择元素：
1. $();括号里面和CSS选择一样，注意对选择出的一组元素，一起处理，省略循环，这里在js里是不允许的。
2. 括号里面可以写elements, selector.等  eg：$('.demo').css('background-color':'red');单个是这样写的，多个的话就写在花括号里面eg：({backgroundColor:'red',width:100,height:100px,})
3. 括号里面可以是 null false undefined
4. 括号里面可以是 function() {}
当$()括号里填的是函数function时；
`$(function () {
  alert('jQuery load');
});
window.onload = function () {
  alert('window load');
};`
结果顺序为：先弹出 window  后弹出 jQuery
因为jQuery里面是这样写的：
`function $(selector) {
  if(typeof selector === 'function') {
	function temp () {
	  window.setTimeout(selector, 0);
	}
	document.addEventListener('DOMContentLoaded', temp)
  }
}`
虽然DOMContentLoaded是较window.onload先执行触发的，也就是先执行temp，但是setTimeout加入任务队列中虽然写的是0毫秒立即执行的，但是最快也要4毫秒之后才能执行，也就是说虽然你应该最先执行，但是因为js是单线程，4毫秒之后也就在windo.onload之后才能执行了。但是要是页面上有很多资源需要加载的话，图片或者文件等等那么window.onload就需要加载一些时间了，也就是在4毫秒之后那么setTimeout就会在window.onload之前了。

5. 括号里面可以是 上下文context
$(selector, context)
eg: $('div', 'span').css(background: 'red')
这样就表示是在div里面的span标签执行css操作。
6. 特有的操作；
```
$('ul li:first').css('background', 'red')；
$('ul li:last').css('background', 'red')；

$('ul li:eq(0)').css('background', 'red')；
$('ul li').eq(0).css('background', 'red')；

$('ul li:odd').css('background', 'red')；
$('ul li:even').css('background', 'red')；
```
```
var arr[];
arr.filter(function (ele, index) {
  如果第一个元素和索引满足条件，就把这个元素留下来，放到一个新数组中。起到了一个过滤的作用。
})
jQuery里面也有这个方法。也能起到过滤的作用。
$().filter(selectoe\function\element\jQuery Object)
$('ul li').filter(':even').css('background', 'orange')
```
> 过滤一下是偶数的li执行它。

`$('ul li').filter(function (index) {
  index % 4 === 0;
}).css('background', 'orange');`

# 下面介绍一些再jQuery中常用的方法：
## not()方法
not()方法功能正好跟上面的filter()相反。
## has()方法
has()方法功能
`$('ul li').has('span').css('background', 'orange')`  表示的是li标签中有span标签的操作它
## is()方法
is()方法。他之后就不能再进行链式调用了。因为他返回的结果为boolean类型的。
`$('ul .demo').is($('ul li').eq(2))` 返回的结果为 true，表示的是看前面所选的跟后面的是否相同。
## find()方法
`$('ul').find('.demo').css('background', 'orange')` 表示的是在ul里面找满足条件的li并进行操作li。跟之前的是不同的。因为他操作的不是最前面的ul了，而是操作的是find找到的满足条件的li。而且通过find()返回的结果里面还有一个prevObject对象，这个是找到这个之前的标签，与end()方法是一样的，可以往上回退到之前的标签。
`$('ul').find('.demo').prevObject === $('ul')` 结果为：false  （因为之前是new出来的对象，后面是另一个new出来的另一个对象）
## html()方法
html()方法,是基于innerHTML的方法的，是获取集合中第一个匹配元素的HTML内容 或 设置每一个匹配元素的html内容。
`$('ul li').html();`表示的是取出来一个li。   取值取一个，赋值赋一组。
`$('ul li').html('<span style="color: orange;">haha</span>');`表示的是在每一个li标签中都添加了一个span标签
## text()方法
text()方法，是基于innerTEXT的方法，是得到匹配元素集合中每个元素的文本内容结合，包括他们的后代，或设置匹配元素集合中每个元素的文本内容为指定的文本内容。hahahahahaahahahhhahhahaha十个li中的文本内容全部返回。`$('ul li').text('123')`会把ul下的所有东西都替换了。
## .css()方法
`$('ul li').css()`当赋值为颜色的时候会把颜色内部转换成RGB形式的。取值取一个，赋值赋一组。
## .setAttribute()方法
`.setAttribute`**是设置DOM元素上的属性的。DOM上的标签上的特性像id、class等等会与DOM设置的形成一一映射的关系，而属性是你自己设置的所以则没有这种映射关系。**
## .attr()方法
`attr()`方法,是基于setAttribute()方法的
`$('ul li').attr('data', 'duyi');`  表示的是在每一个li上面都加上了一个属性名称data="duyi";
`$('ul li').attr('data');`  结果为一个duyi,这就是取值，取值取一个，赋值赋一组。
## .prop()方法
prop()方法，是标签上的特性，才能添加上去的。
`$('ul li').prop('id', 'demo')`,表示在每一个li标签上添加了一个id特性值为demo。
再比如表单`<input type="radio" checked="checked">`
`$('input').attr('checked');`当被选中的时候就是checked没有选中的时候就是undefined。但是你不了解的话就不会知道的。但是用prop()方法就不会不了解了，这个点返回值是true或者false。一般表单这个我们都用prop方法。
## next()、prev()方法
next()的下一个标签   prev()的前一个标签   index()返回这个标签的索引是第几位。
`$('li').click(function () {
  console.log(this);
  console.log($(this).index());
})`


因为jQuery是链式操作，所以下面的这些方法是有相反的。
```
$('.box3').inserBefore( $('.box1') );在box1之前加入box3
$('.box1').before( $('.box3') );同上

$('.box3').appendTo( $('.wrapper') );往.wrapper里加入box3
$('.wrapper').append( $('.box3') );

$('.box3').prependTo( $('.wrapper') );往.wrapper之前加入box3
$('.wrapper').prepend( $('.box3') );
```
## remove()方法
remove()方法：是把标签移除。

# jQuery中的注册事件方法
## bind()方法
注册事件bind() （老版本）绑定事件的，可以改变this指向
## on()方法
on() （新版本）  括号里面传参数是第一个是绑定的事件类型，第二个是绑定事件的方法 on('click', function() {})   第三个参数可以是数组对象，那么传的参数就会在这个绑定on方法的对象上了。第四个参数最重要是可以实现事件委托。`$('.wrapper').on('click', 'div', [{name: 'cst'}, '18'], function() {});`就相当于给.wrapper下的div加上了绑定事件，事件委托了，就是说不管是不是原来就在.wrapper下的div，因为这是给.wrapper上绑定了事件，会把这个事件直接加到他下面的div中。功能很强大啊！
## off()方法
alert()会阻塞页面。   off(this) 解除绑定事件，会把调用off事件的所有绑定的事件全部清除。

`$('.wrapper').on('click', function () {alert(0)}).on('click', function () {alert(1)});`
`$('.wrapper').off('click')`
**怎么绑定的就怎么来解绑。**


## 点赞有次数限制
```
function good() {
  console.log('赞')；
  if (++times === 10) {
	$(this).off('click', good);
  }
}
$('.wrapper').on('click', good);
$('.wrapper').one('click', function () {
	console.log('ok');
})
```
**on()方法不仅可以绑定系统固有的事件，还可以绑定自定义事件。自定义事件可以通过trigger来触发。**
## offsetWidth()方法
```
var oDiv = document.getElementById('wp');
document.write(oDiv.offsetWidth);    oDiv.offsetWidth()这个方法显示的就是“content + padding + border”
oDiv.innerWidth   这个显示的是“content + padding” 
oDiv.outerWidth()
```
传参数，参数是true的时候会加上margin，没有参数就没有margin的值   这个显示的是“content + padding + border + margin”
`$('.content').offset()`这个方法会返回一个对象，这个对象里面有top:  和  left:   并且值是与浏览器边框的距离值。
`$('.content').position()`这个方法也会返回一个对象，这个对象里面的top:   和   left:   的值是与最近的父级元素的距离，父级元素要有相对定位或者绝对定位等等的可以让子级找到的属性。   
## 创建dom方法
$('<div> div </div>')可以这样创建一个div
$('</div>')这样也可以，只不过这样就不能填写里面的内容了。