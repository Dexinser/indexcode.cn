---
title: 编程方法小汇总
tags: JavaScript
categories: 学习笔记
---
** {{ title }}：** <Excerpt in index | 首页摘要>

## 深度克隆：遍历对象  for(var prop in obj)
	1、判断是不是原始值   typeof()  object
	2、判断是数组还是对象，有三种方法：instanceof   toString  constructor  一般用toString方法，因为如果在原先的页面上再引入一个页面的话，引入进来的页面中的数组和对象就不符合原先的原则了，而toString方法则不会发生这种引用错误。
	3、建立相应的数组或对象
	递归的方法。(必须找出口)
```
var obj = {
  name : 'abc',
  age : 123,
  card : ['vasa', 'master'],
  wife : {
	name : 'bcd',
	son : {
	  name : 'aaa'
	}
  }
}
function deepClone(origin, target) {
    var target = target || {},
	toStr = Object.prototype.toString,
	arrStr = "[object Array]";
  for(var prop in origin) {
	if(orgin.hasOwnProperty(prop)) {
	  if(origin[prop] !== 'null' && typeof(origin[prop]) == 'object') {
		if(toStr.call(origin[prop]) == 'arrStr'){
		   target[prop] = [];
		}else{
		   target[prop] = {};
		}
		deepClone(origin[prop], target[prop]);
	  }else{
		target[prop] = origin[prop];
	  }
	}
  }
  return target;
}
deepClone(obj);

```
## 封装Ajax方法：
```
function Ajax(method, url, flag, data, callBack) {
  var app = null;
  if(window.XMLHttpRequest) {
    app = new window.XMLHttpRequest();
  }else{
    app = new window.ActiveXObject('Microsoft.XMLHTTP');
  }
  method = method.toUpperCase();

  if(method === 'GET') {
    app.open(method, url + '?' + data, flag);
    app.send();
  }else if(method === 'POST') {
    app.open(method, url, flag);
    app.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
    app.send(data);
  }
  app.onreadystatechange = function() {
    if(app.readyState === 4) {
	if(app.status === 200) {
	  callBack(app.responseText);
	}else{
	  alert('error');
	}
    }
  }
}
```
__vue重要思想（借鉴React）中的虚拟DOM（真实DOM用js实现的方式），极大的减少了浏览器页面切换间的刷新次数。创新的思想！__
真实实现方法是用：vue.render()函数中的h()函数来实现的！
## 模拟虚拟DOM的实现方法：
```
function vElement(tagName,prop,children)
{
  if(!(this instanceof vElement)){
    return new vElement(tagName,prop,children);
  }
  if(Object.prototype.toString.call(prop) === "[object Array]") {
    children = prop;
    prop = {}
  }
  this.tagName = tagName;
  this.children = children;
  this.prop = prop;
  var count = 0;
  this.children.forEach(function(child, index){
    if(child instanceof vElement) {
	count += child.count;
    }
    count ++;
  })
  this.count = count;
}
vElement.prototype.render = function()
{
  var el = document.createElement(this.tagName);
  var children = this.children;
  var prop = this.prop;
  for(var item in prop){
    var curProp = prop[item];
    el.setAttribute(item, curProp);
  }
  children.forEach(function(child,index){
    if(child instanceof vElement){
	var childDom = child.render();
    }else{
	var childDom = document.createTextNode(child);
    }
    el.appendChild(childDom);
  })
  return el;
}
var dom = vElement("div",{class: "demo", id:"demo1"},["hello world",vElement("p",{class:"demo2"},["我是p标签"])]);
dom.render();
```
结果为：渲染出了两个dom数节点；分别为：
`<div class="demo" id="demo1">
  <p class="demo2">我是p标签</p>
</div>`
