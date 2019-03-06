---
title: Math.floor()等方法的用法
tags: JavaScript
categories: 基础方法分享
---

## Math.floor()方法的深层解析
  大家都知道这是一个JavaScript的基础的方法---向下取整，但是你们有没有遇到过这个方法不听话呢？哈哈，接下来就让我们来领教一下这个方法什么时候才会出现不听话吧！
  `!function test(){
			var is = 100;
			window.setInterval(function(){
				is = is/7;
				Math.floor(is);
				console.log(is)
			},10)
		}()`
        这个方法之后的结果为14.124235...
这段代码中就用到了Math.floor()这个方法，但是这个方法就在这个时候不听话了，is这个变量居然一直取到了小数点后好多好多位。这是为什么呢？其实并不是这个方法不好用了，只是我们把这个方法用错了而已，因为is这个变量是一个Number类型的数字，是一个原始值（栈类型）不可改变。所以上面的代码我们访问的其实还是原来的is的值，并没有访问Math.floor()之后的is值。
我们可以这样访问到Math.floor()之后的is值。代码如下：
`!function test(){
			var is = 100;
			window.setInterval(function(){
				is = is/7;
				console.log(Math.floor(is);)
			},10)
		}()`
这样之后的结果就是14了。
通过这篇文章，只是想告诉你，JavaScript语言的一些值的类型，有引用值和原始值，引用值也就是堆数据类型的值，原始值在JavaScript语言中有undefined、Number、Boolean、String等，并且不同的值类型之间的不同的区别是什么，尤其重要的是千万不要试图去改变原始值，因为你真的拗不过他们的！哈哈，好了，就这样了。