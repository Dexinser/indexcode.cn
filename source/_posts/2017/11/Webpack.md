---
title: Webpack学习笔记
tags: JavaScript
categories: 学习笔记
---
** {{ title }}：** <Excerpt in index | 首页摘要>

# 什么是Webpack？
Webpack的中文叫法--我更愿意叫它“前端自动化构建工具”，是用来进行模块化加载并且打包的，它能把各种资源，例如图片、js文件、css预处理语言等等，统统进行处理，打包成符合生产环境部署的前端资源。

模块化的问题解决之后，webpack 就能把各种资源模块打包合并成一个文件输出给浏览器。在打包的过程中还能对这些资源进行处理，比如压缩减少体积，把 sass 编译成 css, coffee 编译成 js。所以它在某些程度上，跟 grunt/gulp 的功能有些相同。
![Webpack工作模式](http://outwcl4zh.bkt.clouddn.com/webpack.jpg)
# 与grunt/gulp的区别
grunt/gulp 强调的是前端开发的工作流程，我们可以通过配置一系列的 task，定义 task 处理的事务（例如文件压缩合并、雪碧图、启动 server、版本控制等），然后定义执行顺序，来让 grunt/gulp 执行这些 task，从而构建项目的整个前端开发流程。
![grunt/gulp](http://outwcl4zh.bkt.clouddn.com/gulp+grunt.png)




