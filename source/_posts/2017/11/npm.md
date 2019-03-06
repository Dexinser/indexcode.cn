---
title: npm相关问题
tags: node
categories: 开发工具
---
** {{ title }}：** <Excerpt in index | 首页摘要>
简单的来说npm就是nodejs的包管理工具。

所以说到它就不得不提一下nodejs这个前端发展中出现的里程碑式的后端JavaScript语言。让我们摆脱了浏览器这一个单一的环境限制，开始向后端迈进。

正是由于nodejs的火爆发展，也带动着前端JavaScript模块化的步伐。由于后端开发是非常复杂的，所以必须使用模块化的开发模式，而随着前端也越来越复杂的应用开发，所以类似后端开发中的模块化开发不得不应用到前端中来了。

# 前端模块化开发带来的好处

## 命名冲突
随着前端开发应用的复杂度越来越高，应用开发的团队成员也越来越多，不可避免的就有了命名上的一些冲突，为了解决命名冲突所带来的问题，我们可以用模块化的思想，把各个功能封装在一个模块中。

## 文件依赖
在JavaScript中，由于语言的单线程性质，如果要加载一个js文件，而这个文件依赖于很多个其他的js文件，那么就要很小心的处理加载的先后顺序问题，先把依赖加载进来，在加载依赖这些js的js文件。说起来很拗口哦~（没办法，就这个表达能力啊~）比如：
`<script src="util.js"></script>
<script src="dialog.js"></script>
<script>
  org.CoolSite.Dialog.init({ /* 传入配置 */ });
</script>`
dialog.js依赖util.js文件中的一些方法，所以必须先要加载完成util.js文件才能正常使用dialog.js中的方法。
上面讲的是最简单的文件依赖问题的一些使用方法。但是像上面那样使用很麻烦，所以借鉴后端node的模块化方法，前端引入了类似YUI3库的加载方法，简单实用还美观，如下：
`YUI.add('my-module', function (Y) {
  // ...
}, '0.0.1', {
    requires: ['node', 'event']
});`

上面的代码，通过 requires 等方式来指定当前模块的依赖。这很大程度上可以解决依赖问题，但不够优雅。当模块很多，依赖很复杂时，烦琐的配置会带来不少隐患。

命名冲突和文件依赖，是前端开发过程中的两个经典问题。下来我们看如何通过模块化开发来解决。为了方便描述，我们使用 Sea.js 来作为模块化开发框架。

# 使用Sea.js来解决
先说一下这些模块的发展吧。前面说了前端模块化是借鉴的node后端模块化的思想。而node又是遵循的服务器端模块的规范-->CommonJs。

## CommonJS （服务器端的模块化规范）
根据CommonJs规范，一个单独的文件就是一个模块。加载模块使用require方法，该方法读取一个文件并执行，最后返回文件内部的exports对象。如下：

```
1> math.js
exports.add = function() {
    var sum = 0, i = 0, args = arguments, l = args.length;
    while (i < l) {
        sum += args[i++];
    }
    return sum;
};
2> increment.js
var add = require('math').add;
exports.increment = function(val) {
    return add(val, 1);
};
3> main.js，该文件为入口文件
var inc = require('increment').increment;
var a = 1;
inc(a); // 2
```
CommonJS 加载模块是同步的，所以只有加载完成才能执行后面的操作。像Node.js主要用于服务器的编程，加载的模块文件一般都已经存在本地硬盘，所以加载起来比较快，不用考虑异步加载的方式，所以CommonJS规范比较适用。但如果是浏览器环境，要从服务器加载模块，网络请求资源的方式，速度相对较慢，就必须采用异步加载的模式。所以就有了 AMD  CMD 的解决方案。
模块的要求如下：
> 标示符require，为一个函数，它仅有一个参数为字符串，该字符串须遵守Module Identifiers的6点规定
> require方法返回指定的模块API
> 如果存在依赖的其它模块，那么依次加载
> require不能返回，则抛异常
> 仅能使用标示符exports导出API

## AMD（Asynchromous Module Definition）异步模块定义
AMD 是 RequireJS 在推广过程中对模块定义的规范化产出。
AMD异步加载模块。它的模块支持 对象、 函数、 构造器、 字符串、 JSON 等各种类型的模块。 

使用AMD规范适用define方法定义模块。如下：

```
//通过数组引入依赖 ，回调函数通过形参传入依赖 
define(['someModule1', ‘someModule2’], function (someModule1, someModule2) { 

    function foo () { 
        /// something 
        someModule1.test(); 
    } 

    return {foo: foo} 
}); 
AMD规范允许输出模块兼容CommonJS规范，这时define方法如下： 

define(function (require, exports, module) { 
     
    var reqModule = require("./someModule"); 
    requModule.test(); 
     
    exports.asplode = function () { 
        //something 
    } 
}); 
```
> 定义模块用module变量，它有一个方法declare
> declare接受一个函数类型的参数，如称为factory
> factory有三个参数分别为require、exports、module
> factory使用返回值和exports导出API
> factory如果是对象类型，则将该对象作为模块输出

目前，实现AMD的库有 RequireJS  、 curl  、 Dojo  、 bdLoad 、 JSLocalnet  、 Nodules  等。

## CMD
CMD是SeaJS 在推广过程中对模块定义的规范化产出。
Sea.js 是国内前端大神玉伯写出来的一个成熟的开源项目，核心目标是给前端开发提供简单、极致的模块化开发体验。这里不多做介绍，有兴趣的可以访问 seajs.org 查看官方文档。

使用 Sea.js，在书写文件时，需要遵守 CMD （Common Module Definition）模块定义规范。一个文件就是一个模块。如下：
```
define(function(require, exports) {
  exports.each = function (arr) {
    // 实现代码
  };

  exports.log = function (str) {
    // 实现代码
  };
});
通过 exports 就可以向外提供接口。这样，dialog.js 的代码变成

define(function(require, exports) {
  var util = require('./util.js');

  exports.init = function() {
    // 实现代码
  };
});
```
关键部分到了！我们通过 require('./util.js') 就可以拿到 util.js 中通过 exports 暴露的接口。这里的 require 可以认为是 Sea.js 给 JavaScript 语言增加的一个语法关键字，通过 require 可以获取其他模块提供的接口。

这其实一点也不神奇。作为前端工程师，对 CSS 代码一定也不陌生。

`@import url("base.css");`

`#id { ... }
.class { ... }`
Sea.js 增加的 require 语法关键字，就如 CSS 文件中的 @import 一样，给我们的源码赋予了依赖引入功能。

# CMD和AMD的区别有以下几点： 

1. 对于依赖的模块AMD是提前执行，CMD是延迟执行。不过RequireJS从2.0开始，也改成可以延迟执行（根据写法不同，处理方式也不同）。 

2. AMD推崇依赖前置，CMD推崇依赖就近。
```
//AMD 
define(['./a','./b'], function (a, b) { 
    //依赖一开始就写好 
    a.test(); 
    b.test(); 
}); 

//CMD 
define(function (require, exports, module) { 
    //依赖可以就近书写 
    var a = require('./a'); 
    a.test(); 
    ... 
    //软依赖 
    if (status) { 
        var b = require('./b'); 
        b.test(); 
    } 
}); 
```
虽然 AMD也支持CMD写法，但依赖前置是官方文档的默认模块定义写法。 

3. AMD的API默认是一个当多个用，CMD严格的区分推崇职责单一。例如：AMD里require分全局的和局部的。CMD里面没有全局的 require ,提供 seajs.use()来实现模块系统的加载启动。CMD里每个API都简单纯粹。 

***
***
好了，说完了上面的介绍，该正式讲一下正文了~

# npm 三个版本的区别简介
如今npm包管理已经有3个版本了，那就来讲一下他们之间的区别吧~

## npm v2解析包的依赖关系
想像一下现在有三个模块module A、module B、module C。A依赖B的V1版本，C依赖于B的V2版本。 npm采取的方式是把依赖的模块包嵌入子目录。

## npm V3 解析包的依赖关系
npm3和npm2的不同之处在于：
> npm2使用嵌套的方式来管理依赖包，npm3尝试缓和过长的包依赖路径问题。 把二级依赖的包安装在同一级目录下。

假设我们有一个模块A依赖模块B。我们在安装模块A的时候，在项目的node_modules文件夹下： 可以看到 npm v2与npm v3的差异是npm v3中A和B是再同一层文件夹中的，而npm v2中B是再A文件夹下嵌套的。

现在我们需要安装一个模块C，模块C依赖模块B但是版本与模块A依赖的不同。

由于B v1.0已经安装在node_modules目录的根目录下了，不能把B v2.0也安装在根目录下。这个时候npm v3的处理方式和npm v2类似。

通过 npm ls 查看当前项目所有包的依赖关系。如果只是想看顶级包的依赖关系可以执行npm ls --depth=0。

## npm v3去重
也正因为npm v3版本中的新特性，所以就会出现一些重复的包下载，我们可以用提供给我们的API来进行删除重复的包。
__npm dedupe__

该命令会删除node_modules顶级目录下没有被使用的模块，并且把被重复依赖的模块移动到顶级目录下。

接下来看一下最新版的npm的一些命令用法吧~
# npm 最新用法
## npm install
用过npm的对这个命令一定熟悉的不能再熟悉了吧~
`$ npm install <packageName>`
安装之前，npm install会先检查，node_modules目录之中是否已经存在制定模块。如果存在，就不再重新安装，既是运程仓库已经有了一个新版本，也是如此。

如果你希望，一个模块不管是狗安装过，npm都要强制重新安装，可以使用-f或者--force命令参数。
`$ npm install <packageName> --force`

## npm update
如果想更新已安装模块，就要用到npm update命令了。
`$ npm update <packageName>`
它会先到远程仓库查询最新版本，然后查询本地版本。如果本地版本不存在，或者远程版本有更新，就会安装最新版本。

## registry
npm update命令怎么知道每个模块的最新版本呢？
答案是npm模块仓库提供了一个查询服务，叫做registry。以npmjs.org为例，它的查询网址是https://registry.npmjs.org/。

这个网址后面跟上模块名，就会得到一个 JSON 对象，里面是该模块所有版本的信息。比如，访问 https://registry.npmjs.org/react，就会看到 react 模块所有版本的信息。

它跟下面命令的效果是一样的。

`$ npm view react
# npm view 的别名
$ npm info react
$ npm show react
$ npm v react`

registry 网址的模块名后面，还可以跟上版本号或者标签，用来查询某个具体版本的信息。比如， 访问 https://registry.npmjs.org/react/v0.14.6 ，就可以看到 React 的 0.14.6 版。


# npm 的常用命令行代码：
1. npm install moduleNames：安装Node包（moduleNames包名称）
（1）npm install moduleNames -g 为全局安装 
（2）npm install moduleNames@5.1.1  安装特定版本插件
（3）npm install moduleNames --save 会在package.json的dependencies属性下添加moduleNames  即发布依赖时候任依赖的插件
（4）npm install moduleNames --save-dev  会在package.json的devDependencies属性下添加moduleNames依赖 即开发依赖插件
总结：npm install 在安装 npm 包时，有两种命令参数可以把它们的信息写入 package.json 文件，一个是npm install --save另一个是 npm install --save-dev，他们表面上的区别是--save 会把依赖包名称添加到 package.json 文件 dependencies 键下，--save-dev 则添加到 package.json 文件 devDependencies 键下。
真正跑在用户浏览器中的代码，比如jquery,react这些，是需要安装到dependencies中的。
--save是对生产环境所需依赖的声明(开发应用中使用的框架，库),--save-dev是对开发环境所需依赖的声明(构建工具，测试工具).正常使用npm install时，会下载dependencies和devDependencies中的模块，当使用npm install --production或者注明NODE_ENV变量值为production时，只会下载dependencies中的模块。
2. npm config set registry https://registry.npm.taobao.org  修改包下载源，此例修改为了淘宝镜像
3. npm config get prefix  查看全局安装路径
4. npm config set prefix G:/node_modules_global  修改全局安装路径
5. npm init  初始化目录
6. npm install -g gulp  全局安装（如gulp）
7. npm uninstall -g gulp    全局包卸载（如gulp）
8. npm uninstall gulp --save-dev  项目本地卸载（如gulp）
9. npm ls --global    会查看到安装包所包含的所有依赖文件   npm ls --global -depth 0  只查看顶级安装包
10. npm ls  查看本地安装包
11. npm cache clean  删除安装包缓存
12. npm  update xxx  更新安装包
13. npm search xxx  查找验证某个包是否已经存在
14. npm root 查看当前包安装路径  npm root -g  查看全局包安装路径
15. npm outdated：检查包是否已经过时，此命令会列出所有已经过时的包，可以及时进行包的更新
16. npm view xxx engines：查看包所依赖的Node的版本
17. npm view xxx repository.url：查看包的源文件地址
18. npm view xxxpendencies：查看包的依赖关系