---
title: html标签举例
tags: JavaScript
categories: 学习笔记
---
** {{ title }}：** <Excerpt in index | 首页摘要>
## html标签举例
这是我最最开始学习HTML的时候保存下来的第一个HTML文件
```
<!-- html:hyperText markup language! -->
<html lang="zh-cmn,en">
<head>
    <meta charset="utf-8">    <!-- gb2312 gbk unicode utf:8-bit unicode transformation format万国码 -->
	<title>京东，惊动世界!</title>
	<!-- SEO  搜索引擎爬虫在html中写的lang=“zh-cmn,en”<meta name="description" content="一段幸福的婚姻">
	<meta name="keywords" content="王宝强，马蓉"> -->
</head>
<body>
    <p>成段落展示1</p>
    <p>成段落展示2</p>
    <h1>head标题1自带加粗</h1>
    <h3>head标题3自带加粗</h3>
    <strong>加粗1</strong><!-- <b>加粗</b> -->
    <em>斜体1</em><!-- <i>斜体2</i> -->
    <address>段落加加粗</address><!-- <b><em>段落加斜体</em></b> -->
    <del>原价50元 </del><!-- html不能掺和css的功能，样式、结构、功能相分离 -->
    <div>相当于容器，没功能，没样式，自成段落</div><!-- 容器里面东西多的话加功能比较方便，规格化和绑定操作 -->
    <span>容器</span>
    <!-- 空格在编辑器中被认为是文字分隔符 -->
   <!--  html编码,空格 -->&nbsp;
   <!-- html编码，大于小于号 -->&gt;div&lt;
   <br><!-- 单独出现的标签，和meta标签也是单独出现的，没有尾标签，既然是尾标签那写的内容就的写在标签内，包住内容，这是换行标签，相当于回车 -->
   <ol type="I" reversed="reversed">
   	<li>west world</li>
   	<li>big bang</li>
   	<li>journey to the west</li>
   </ol>
   <ul type="square">
   	<li>衣服</li>
   	<li>鞋包</li>
   	<li>帽子</li>
   	<li>眼镜</li>
   </ul><!-- 很重要的，但凡是导航栏就是用ul做的，配合css样式做出来的 div配合span也能做，不过不好，为了维护下来比较方便，人为规范-->
  <!--  <img style="width:100px;" src="china.jpg" alt="这是中国高清地图" title="China map"> -->
  <!--1.网上的url
   2.本地的绝对路径
   3.本地的相对路径  -->
   <!-- 注释的功能：1.注释记载下来 2.锁定错误，检查错误，挑错-->
   <a href="http://www.baidu.com">百度一下</a><!-- 超链接功能hyperlink    来源于anchor汽车抛锚，起初是当锚点作用的 -->
   <!-- a标签的功能有：1.超链接  2.锚点   3.协议限定符  就是用javescript在herf里写代码例如：herf=javescript:while(1){alert('中毒了，哦也！！！')}   4.自动调用电话或者邮件功能 -->
   <div style="width:100px;height: 100px;background-color:black;" id="only"></div>
   <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
   <a href="#only">原来你在这儿呢，找到你了吧！</a>
   <table border="0px" cellpadding="100px" cellspacing="0px" style="width:800px;height: 400px;"><!-- border边线cellpadding內边距cellspacing表格空隙 -->
   	   <tr align="center">
   	   	 <td colspan="3">1</td>
   	   </tr>
       <tr>
   	   	 <td>2</td>
   	   	 <td>2</td>
   	   	 <td>2</td>
   	   </tr>
       <tr>
   	   	 <td colspan="3">3</td>
   	   </tr>
   </table>
   <!-- 写一个网站就需要一个服务器，网站就在服务器里面的一个地址，用户访问这个网站的话就需要下载这个网站的文件，但是用表格做的网页的话浏览器的加载方式是全部下载完并且执行，完成渲染之后才能展示这个网页。所以加载太慢用户体验差就不用了 -->
   <!-- 前端fe(front end engnieer) 后端rd form前端向后端要信息的功能,发送信息的method中有俩值get|post,给谁后端发送信息的地址action。发送信息必要的2个东西：数据名(name)和数据值(用户提交的数据).有很多input组件，是单标签，里面必须有属性映衬type-->
   <form method="get" action="file:///file:///E:/duyi/message.html">
          <p>
             username:<input type="text" name="username" value="请输入关键字" style="color:#999" onfocus="if(this.value=='请输入关键字'){this.value='';this.style.color='#424242'}" onblur="if(this.value==''){this.value='请输入关键字';this.style.color='#999'}">
          </p>
          <p>
          	  password:<input type="password" name="password"></input>
           </p>
      <input type="submit"></input>
         <!-- <h1>你们喜欢吃啥水果？(单选框)</h1>
         <p>1.Apple<input type="radio" name="fruit" value="苹果"></input></p>
         <p>2.orange<input type="radio" name="fruit" value="橙子"></input></p>
         <p>3.banana<input type="radio" name="fruit" value="香蕉"></input></p>
      <input type="submit"></input>
      <h1>你有什么喜欢的运动？(多选)</h1>
      <p>1.跑步<input type="checkbox" name="yundong" value="paobu"></input></p>
      <p>2.骑行<input type="checkbox" name="yundong" value="qixing"></input></p>
      <p>3.旅游<input type="checkbox" name="yundong" value="lvyou"></input></p>
      <input type="submit"></input>
      <h1>CHOOSE YOUR SEX!</h1>
      <p>
         1.female<input type="radio" name="sex" value="female" checked="checked"></input></p>
      <p>
         2.male<input type="radio" name="sex" value="male" checked="checked"></input></p>
      <input type="submit"></input> -->
     <h1>直辖市</h1> 
      <select name="直辖市">
      	<option value="beijing">北京市</option>
      	<option value="beijing">上海市</option>
      	<option>天津市</option>
      </select>   <!-- 下拉菜单，选择用户所在省份,不用填value，填了以value为主，选票可以作弊.. -->
   </form>
</body>`
</html>`
```