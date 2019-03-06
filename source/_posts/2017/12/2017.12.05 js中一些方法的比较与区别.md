---
title: js中一些相似方法/属性的区别
tags: 学习笔记
categories: JavaScript
---
**{{title}}**   <Excerpt in index | 首页摘要>
# forEach 与 map 方法比较
forEach()和map()两个方法都是ECMA5中Array引进的新方法，主要作用是对数组的每个元素都执行一次所提供的函数，但是它们之间还是有区别的。jQuery也有一个方法$.each(),长得和forEach()有点像，功能也类似。但是从本质上还是有很大的区别的。

`//forEach
array.forEach(callback(currentValue, index, array){
    //do something
}, this)
 
//或者
array.forEach(callback(currentValue, index, array){
    //do something
})　　
 
//map:
var new_array = arr.map(callback[, thisArg])　
 
//$.each()
$(selector).each(function(index,element))  //注意参数的顺序`

callback: 为数组中每个元素执行的函数,该函数接收三个参数，

**参数一：当前数组中元素；参数二：索引； 参数三：当前数组。**

**this：可选，执行会掉时候，this的指向。**
***
区别：
1. forEach()返回值是undefined，不可以链式调用。

2. map()返回一个新数组，原数组不会改变。

3. 没有办法终止或者跳出forEach()循环，除非抛出异常，所以想执行一个数组是否满足什么条件，返回布尔值，可以用一般的for循环实现，或者用Array.every()或者Array.some();

4. $.each()方法规定为每个匹配元素规定运行的函数，可以返回 false 可用于及早停止循环。
***
Array 在 Javascript 中是一个对象， Array 的索引是属性名。
事实上， Javascript 中的 “array” 有些误导性， Javascript 中的 Array 并不像大部分其他语言的数组。首先， Javascript 中的 Array 在内存上并不连续，其次， Array 的索引并不是指偏移量。
实际上， Array 的索引也不是 Number 类型，而是 String 类型的。我们可以正确使用如 arr[0] 的写法的原因是语言可以自动将 Number 类型的 0 转换成 String 类型的 "0" 。
所以，在 Javascript 中从来就没有 Array 的索引，而只有类似 "0" 、 "1" 等等的属性。有趣的是，每个 Array 对象都有一个 length 的属性，导致其表现地更像其他语言的数组。
但为什么在遍历 Array 对象的时候没有输出 length 这一条属性呢？那是因为 for-in 只能遍历“可枚举的属性”， length 属于不可枚举属性，实际上， Array 对象还有许多其他不可枚举的属性。

map可以做链式操作，forEach不可以，
for不用担心兼容性的问题，还有可以break跳出循环，是基础循环，可以有for...in,foo...of,for(let i=0;i<len;i++)等。可以用continue和break控制
forEach是for(let i=0;i<len;i++)的缩写，不支持continue和break，可以return来控制循环，forEach是不能退出循环本身的
map循环当前可循环对象，并且返回新的可循环对象，而forEach没有返回值
forEach只有在火狐和谷歌浏览器中Array有这个方法，在IE中就米有，需要用prototype手动添加这个方法。

# 类数组与数组的区别
类数组对象：
console.log(typeof a);//object 注意：数组也是对象哦
console.log(a); //  Object {0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25, 6: 36, 7: 49, 8: 64, 9: 81} 很明显对象啊
console.log(a.length); //undefined  区别就在这了  类数组对象没有长度的属性和数组的方法
console.log(Object.prototype.toString.call(a));//[object Object] 
数组对象：
console.log(typeof b);//object
console.log(b);//  [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]  很明显数组啊 
console.log(b.length); //8
console.log(Object.prototype.toString.call(b));//[object Array]