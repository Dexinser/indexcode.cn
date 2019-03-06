---
title: Vue
tags: 学习笔记
categories: 前端框架
---
**{{title}}** <Excerpt in index | 首页摘要>
总结一下使用vue的一些方法吧~
用vue-cli来创建一个vue项目的过程：
首先在命令行工具页面输入：vue init `<template-name>` [project-name];之后按提示进行就行了。
创建成功脚手架之后打开创建成功的文件夹，在所在的文件夹下面：cnpm install 安装开发项目所需要的所有依赖； 
npm run dev  运行本地测试开发开一个本地服务器。

# VUE中h()函数和render()函数用js的简单实现：

`function vElement(tagName, prop, children){
  if(!(this instanceof vElement)){
    return new vElement(tagName, prop, children)
  }
  if(Object.prototype.toString.call(prop) === "[object Array]") {
    children = prop;
    prop = {};
  }
  this.tagName = tagName;
  this.prop = prop;
  this.children = children;
  var count = 0;
  this.children.forEach(function(child, index){
    if(child instanceof vElement){
	count += this.count;
    }
    count ++;
  })
  this.count = count;
}`

`vElement.prototype.render = function(){
  var el = document.createElement(this.tagName);
  var children = this.children;
  var prop = this.prop;
  for(var item in prop){
    var curProp = prop[item];
    el.setAttribute(item, curProp);
  }
  children.forEach(function(child, index){
    if(child instanceof vElement){
	var childDom = child.render();
    }else{
	var childDom = document.createTextNode(child)
    }
    el.appendChild(childDom)
  })
  return el;
}`

# Vue的三种模板：
1、html模板；-->  v-html  仅仅解析html样式；但是解析不出来绑定的数据。
2、字符串模板；-->  template  ` `  可以解析出绑定的数据。可以用script标签，类型改为：x/template 加上属性名就可以用属性名来调用了。
3、render()函数；-->  render(creatElement){var dom = creatElement('div',['hello',creatElemnt('p',['world'])])};
创建出来之后直接return创建的对象就行了！前两个本质上都是调用render函数来创建的。但是这样创建就不能插入vue的一些指令了。


# vue中父子组件之间的交互：
父组件通过props的这个接口与子组件实现交互功能，具体做法是在子组件中定义一个props属性传递数据到父组件中去；子组件通过自定义事件来与父组件进行交互，通过在父组件中调用子组件中的自定义时间来完成；但是要是嵌套的层次太深，也就是父组件中有很多层的子组件，那么他们之间的交互效率就非常的慢了，为了解决这个问题我们可以用vue官方给我们的一个库来管理这些需要交互的数据---即vuex，专为vue.js应用程序开发的状态管理模式；他采用集中式存储管理应用的所有组件的状态；并以相应的规则保证状态以一种可预测的方式发生变化。

# Vue中一些类似方法比较
计算属性computed  vs  方法mothods：
computed刷新的时候会缓存，更加提高性能。

v-show  vs  v-if
v-show：直接添加一个css属性display：none；要是频繁的使用这个dom节点的话，应该使用v-show，提高性能。
v-if： 直接删除一个dom节点

脚手架vue-cli，顾名思义就是一般我们自己做项目要配置的一些东西。但是脚手架会帮我们配置好一套东西。非常方便有木有~工程师就是能让电脑帮我们做的就不要自己动手做了嘛~~嘿嘿嘿。懒人秘籍-必学编程技能哦~

路由设置里面有一个属性方法是mode：这个属性是加载url的方式是用history还是用hash模式，history模式需要我们跟后端去配合，因为会想后端去请求一个新页面替换掉我们现在的页面，hash模式就不用跟后端去配合，是我们想要的单页面应用，当然了，这个是我们没有用router-link这个标签时的情况。用来router-link标签后不管是哪种模式都不会像后台去请求数据了。history模式是直接在当前的url下加上/的，而hash模式是先加上#再加上/的。注意两者的区别


node 中的path路径：
**__dirname**就是文件所处的当前文件夹；

created函数:在实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。
