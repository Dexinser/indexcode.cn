---
title: 编程相关-杂（relative）
tags: others
categories: 开发工具
---
** {{ title }}：** <Excerpt in index | 首页摘要>
```
<li> vscode</li>
<li> atom</li>
<li> webstrom</li>
<li>sublime的插件问题</li>
<li>emmet</li>
emmet插件的简单使用规则：div.demo#only*3>p[style="background-color:orange;width:100px;height:100px;"]
div>(p^span.demo#only{内容})
ul>li{a$}*10
```
# Sublime Text 3 快捷键精华版:
Ctrl+Shift+P：打开命令面板
Ctrl+P：搜索项目中的文件
Ctrl+G：跳转到第几行
Ctrl+W：关闭当前打开文件
Ctrl+Shift+W：关闭所有打开文件
Ctrl+Shift+V：粘贴并格式化
Ctrl+D：选择单词，重复可增加选择下一个相同的单词
Ctrl+L：选择行，重复可依次增加选择下一行
Ctrl+Shift+L：选择多行
Ctrl+Shift+Enter：在当前行前插入新行
Ctrl+X：删除当前行
Ctrl+M：跳转到对应括号
Ctrl+U：软撤销，撤销光标位置
Ctrl+J：选择标签内容
Ctrl+F：查找内容
Ctrl+Shift+F：查找并替换
Ctrl+H：替换
Ctrl+R：前往 method
Ctrl+N：新建窗口
Ctrl+K+B：开关侧栏
Ctrl+Shift+M：选中当前括号内容，重复可选着括号本身
Ctrl+F2：设置/删除标记
Ctrl+/：注释当前行
Ctrl+Shift+/：当前位置插入注释
Ctrl+Alt+/：块注释，并Focus到首行，写注释说明用的
Ctrl+Shift+A：选择当前标签前后，修改标签用的
F11：全屏
Shift+F11：全屏免打扰模式，只编辑当前文件
Alt+F3：选择所有相同的词
Alt+.：闭合标签
Alt+Shift+数字：分屏显示
Alt+数字：切换打开第N个文件
Shift+右键拖动：光标多不，用来更改或插入列内容
鼠标的前进后退键可切换Tab文件
按Ctrl，依次点击或选取，可需要编辑的多个位置
按Ctrl+Shift+上下键，可替换行
选择类
Ctrl+D 选中光标所占的文本，继续操作则会选中下一个相同的文本。
Alt+F3 选中文本按下快捷键，即可一次性选择全部的相同文本进行同时编辑。举个栗子：快速选中并更改所有相同的变量名、函数名等。
Ctrl+L 选中整行，继续操作则继续选择下一行，效果和 Shift+↓ 效果一样。
Ctrl+Shift+L 先选中多行，再按下快捷键，会在每行行尾插入光标，即可同时编辑这些行。
Ctrl+Shift+M 选择括号内的内容（继续选择父括号）。举个栗子：快速选中删除函数中的代码，重写函数体代码或重写括号内里的内容。
Ctrl+M 光标移动至括号内结束或开始的位置。
Ctrl+Enter 在下一行插入新行。举个栗子：即使光标不在行尾，也能快速向下插入一行。
Ctrl+Shift+Enter 在上一行插入新行。举个栗子：即使光标不在行首，也能快速向上插入一行。
Ctrl+Shift+[ 选中代码，按下快捷键，折叠代码。
Ctrl+Shift+] 选中代码，按下快捷键，展开代码。
Ctrl+K+0 展开所有折叠代码。
Ctrl+← 向左单位性地移动光标，快速移动光标。
Ctrl+→ 向右单位性地移动光标，快速移动光标。
shift+↑ 向上选中多行。
shift+↓ 向下选中多行。
Shift+← 向左选中文本。
Shift+→ 向右选中文本。
Ctrl+Shift+← 向左单位性地选中文本。
Ctrl+Shift+→ 向右单位性地选中文本。
Ctrl+Shift+↑ 将光标所在行和上一行代码互换（将光标所在行插入到上一行之前）。
Ctrl+Shift+↓ 将光标所在行和下一行代码互换（将光标所在行插入到下一行之后）。
Ctrl+Alt+↑ 向上添加多行光标，可同时编辑多行。
Ctrl+Alt+↓ 向下添加多行光标，可同时编辑多行。
编辑类
Ctrl+J 合并选中的多行代码为一行。举个栗子：将多行格式的CSS属性合并为一行。
Ctrl+Shift+D 复制光标所在整行，插入到下一行。
Tab 向右缩进。
Shift+Tab 向左缩进。
Ctrl+K+K 从光标处开始删除代码至行尾。
Ctrl+Shift+K 删除整行。
Ctrl+/ 注释单行。
Ctrl+Shift+/ 注释多行。
Ctrl+K+U 转换大写。
Ctrl+K+L 转换小写。
Ctrl+Z 撤销。
Ctrl+Y 恢复撤销。
Ctrl+U 软撤销，感觉和 Gtrl+Z 一样。
Ctrl+F2 设置书签
Ctrl+T 左右字母互换。
F6 单词检测拼写
搜索类
Ctrl+F 打开底部搜索框，查找关键字。
Ctrl+shift+F 在文件夹内查找，与普通编辑器不同的地方是sublime允许添加多个文件夹进行查找，略高端，未研究。
Ctrl+P 打开搜索框。举个栗子：1、输入当前项目中的文件名，快速搜索文件，2、输入@和关键字，查找文件中函数名，3、输入：和数字，跳转到文件中该行代码，4、输入#和关键字，查找变量名。
Ctrl+G 打开搜索框，自动带：，输入数字跳转到该行代码。举个栗子：在页面代码比较长的文件中快速定位。
Ctrl+R 打开搜索框，自动带@，输入关键字，查找文件中的函数名。举个栗子：在函数较多的页面快速查找某个函数。
Ctrl+： 打开搜索框，自动带#，输入关键字，查找文件中的变量名、属性名等。
Ctrl+Shift+P 打开命令框。场景栗子：打开命名框，输入关键字，调用sublime text或插件的功能，例如使用package安装插件。
Esc 退出光标多行选择，退出搜索框，命令框等。
显示类
Ctrl+Tab 按文件浏览过的顺序，切换当前窗口的标签页。
Ctrl+PageDown 向左切换当前窗口的标签页。
Ctrl+PageUp 向右切换当前窗口的标签页。
Alt+Shift+1 窗口分屏，恢复默认1屏（非小键盘的数字）
Alt+Shift+2 左右分屏-2列
Alt+Shift+3 左右分屏-3列
Alt+Shift+4 左右分屏-4列
Alt+Shift+5 等分4屏
Alt+Shift+8 垂直分屏-2屏
Alt+Shift+9 垂直分屏-3屏
Ctrl+K+B 开启/关闭侧边栏。
F11 全屏模式
Shift+F11 免打扰模式

# 微信小程序的一些简单简介：
微信小程序中没有关联或者引入标签，只能靠相同的命名来产生关联，比如：index.wxml--index.wxss--index.js--index.json;只能命名相同的名字，然后微信页面就会自动找相同名字来进行关联了。自动进行绑定关联，根据命名把一些东西捆绑在一起。
rpx：就是最开始是为了不让在苹果手机上失真而人为设置的一种与真实的px（像素）所在不同手机上的换算关系。所以rpx也就具有了根据不同屏幕进行自适应的功能了。
wxml上并没有通配符选择器，但是有json配置文件。没有body标签，但是有pages标签就相当于html中的body标签了。
wxml中有很多强大的内置标签，也就是人为封装的组件，恩，很强大的。例如：轮播图组件<swiper>标签，下面有<swiper-item>，<swiper>上有autoplay属性，并伴随着interval="时间"，是否采用衔接滑动circular="true";
图标<icon>组件：上面有不同的类型：type='success/info/..' color="color";
地图<map>组件：map组件上还有很多其他的标签和属性方法。总之很强大了！

wxml没有dom节点，不能像JavaScript一样操作dom元素。但是wxml给了我们一个数据绑定的.js文件。里面有page({});函数调用的形式。通过调用page()这个函数，来注册了一个页面，通过改变page()这个函数来影响UI层面的东西。page()函数里面有一些函数来监听页面的渲染。
生命周期函数：`onLoad:function(options){}`--监听页面加载。
生命周期函数：`onReady:function(){}`--监听页面初次渲染完成。
生命周期函数：`onShow:function(){}`--监听页面显示
生命周期函数：`onHide:function(){}`--监听页面隐藏
生命周期函数：`onUnload:function(){}`--监听页面卸载
生命周期函数执行的顺序为：页面先加载触发`onLoad`函数；再调用`onShow`函数；之后再调用onReady函数。

两个层---一个给用户看的视图层，另一个应用层js操作视图层。
首先是视图层的初始化init..和应用层的创建creat..一个实例
视图层向应用层要一些初始化是数据。切换页面，那么这个页面生命周期就结束了，调用`onUnload`函数。this就代表这个页面实例。

## 编写微信小程序的简单步骤：
首先会在app.json文件下查找我们所配置的东西，创建的页面，页面之间的关联还有页面的导航栏（最顶上的一栏）的设置和底边的tabpar分页的切换设置等等都是在这儿实现的。在app.json中配置好了主页面和分页面之后就可以开始编写代码了。
如何在微信地图上添加功能按钮：因为在地图上添加`<button>`按钮是显示不出来的，因为map组件的层级永远在最上面，只能用map组价提供好的controls属性，配合监听对control的点击的回调函数。然后在.js文件中有wx.getSystemInfo这个方法监听设备信息来获取需要设置的相应数据。
bindcontroltap，在onShow函数内定义一个app-map执行器上下文（类似canvas的执行期上下文），这个执行器上下文中有一个方法是moveToLocaltion方法，定义一个movetoCenter方法就是执行moveToLocation方法的，然后在switch case中，case到指定的controlId就调用定义好的movetoCenter方法。

模拟假数据的一个很好用的网站，easy-mock网站，恩，很有年头了。简单的使用：直接进去没有用户名他直接会让你登录，没有的话就会直接帮你注册成功了。注册成功直接创建项目就行了。非常简单就能使用的。假数据写成JSON形式的，然后窗口打开，复制窗口URL地址，然后就能使用这个假数据了。

http://easy-mock.com/mock/5983e3d1a1d30433d852e683/ofo/getbike

## a++ 和 ++a 的区别：
    他们都是已经执行了代码，也就是都已经加一了。但是++a是显示的加上去了，也就是说显示出来了，但是a++是到下一次执行才显示出来，但是上一次的代码已经执行了。ok？

## 命名上的一些英文单词：
wrapper：包装；
navigation：航行（学），航海（术），海上交通；
contain：内容；
footer: 页脚；
header： 页头；
未完待续...