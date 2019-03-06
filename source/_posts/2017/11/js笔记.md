---
title: js笔记
tags: JavaScript
categories: 学习笔记
---
** {{ title }}：** <Excerpt in index | 首页摘要>

## js笔记
typeof 识别不了Object与Array与null（历史遗留性问题）
返回六种数据类型number、string、booblean、undefined、object、function。

隐示类型转化：Number()类型的数据转化，typeof之后会把true返回数值1，false返回值为0。“123”转化成123。undefined转化成数值NaN。null转化成数值0。“”空字符串转化成0。

parseInt("123abc")会把字符串类型的转换成整数类型Number类型的123，并且在非数字位置截断。但是只会把其它的undefined和null和true、false等转化NaN。    parseInt（“123”，radix）radix是基底，取值范围是2--36（0也行，有的浏览器中会把0当做10进制的数）。填上第二位的话会把前面的123按照所填的基底转化成10进制的数。

只有六个值转化成booblean值为false，分别是undefined、null、0、""、false、NaN。其它所有转化成boollean值都为true。

&& 与运算符，找到一个false就返回。如0 && 1；直接返回值0。1 && 2 && 3；返回值为3。全真才为真，有一个假就是假；

|| 或运算符， 找到一个真就返回。如0 || 1 || 2，返回值为1。1 || 0，返回值为1。全假才为假，有一个真就是真。

parseFloat("10.234")可以把字符串类型的转化成小数类型的数值类型，即浮点型。

String（undefined）--> "undefined"  会把一切东西转化成字符串类型的。

对象.toString方法，与String相似，只不过他是一种方法。只有undefined和null没有这个方法，不能调用这个方法。toString(radix),这个radix跟parseInt中的radix正好相反。按照10进制转换成所填基底的数。

数学符号有隐式类型转换，只有+号特别，会与字符形式的连接起来。

null == undefined返回结果为true。 0 == ""返回结果为true。

对象.toFixed(3)方法表示的是保留小数点后3位有效数字，科学计数法。

作用域：当函数执行时，会创建一个称为执行期上下文的内部对象。一个执行期上下文定义了一个函数执行时的环境，函数每次执行时对应的执行期上下文都是独一无二的，所以多次调用一个函数会导致创建多个执行期上下文，当函数执行完毕，   ！！它所产生的！！！  执行期上下文被销毁。
   查找变量：从作用域的顶端依次向下查找。

 ` function a() {
	function b() {
		console.log(b);	
	}
  	var a = 123;
	b();
  }
  var glob = 100;
  a();`
函数a的执行也就是函数b定义的开始，函数b在刚定义的时候就保存了函数a的劳动成果。变量只有在执行的时候才会被赋值。

   闭包
`   function a() {
	var arr = [];
	for(var i = 0; i < 10; i++) {
		arr[i] = function () {
			console.log(i + ",");
		}
	}
	return arr;
   }
   var demo = a();
   for(var j = 0; j < 10; j++) {
	demo[j]();
   }`
上题中的i与函数形成闭包，所以结果会打印出10个10。题中的i在函数还没执行时不会被赋值，要等到函数最后执行的时候才会进行赋值，函数执行时for循环就已经转了10圈了，所以i直接进行赋值就成了10个10。运用立即执行函数可以每一圈都让i赋值。
我们想要依次打印出i从0到9，但是这样的话就打印不出来我们想要的结果。所以只能靠闭包才能实现我们想要的结果。如下：


` function a() {
  var arr = [];
  for(var i = 0; i < 10; i++) {
    (function (j) {
      arr[j] = function () {
        console.log(j);
      }
    }(i))
  }
  return arr;
   }
   var demo = a();
   for(var j = 0; j < 10; j++) {
  demo[j]();
   }`
值得注意的是这个函数中的demo是一个数组，执行时不能像demo()这样，需要如上题那样进行。

	闭包会导致原有作用域链不释放，造成内存泄露。闭包会导致多个执行函数共用一个公有变量，如果不是特殊需要，应尽量防止这种情况放生。
一个函数连续执行的话会在他之前形成的作用域链上再作用。

闭包的作用：1、公有变量   累加器（多次调用的是一个变量）
	   2、可以做缓存，存储变量   （操作的是同一个变量，把变量放在那儿，多个函数都使用它）   3、模块化开发，防止污染全局变量   4、私有化变量
` function Deng () {
  var prepareWife = "xiaozhang";
  var obj = {
    name : "dengxuming",
    age : 40,
    sex : "male",
    wife : "xiaoliu",
    divorce : function () {
      delete this.wife;
    },
     getMarried : function () {
      this.wife = prepareWife;  
    },
    changePrepare : function (someone) {
      prepareWife = someone;
    },
    sayMyWife : function () {
      return this.wife;    }
    }
    return obj;
    }
    var deng = Deng();`


  立即执行函数：此类函数没有声明，在一次执行过后即释放。适合做初始化工作。
（function () {}）()  就是长这个样子。执行完就被销毁，所以一般不写名。    只有表达式才能被执行。123就是一个表达式。函数声明不能被执行。成等式就是表达式。表达式被执行完了它就会被销毁，就找不到了。例如下面这个例子：
`  var a = function () {
                              console.log('a');
                            }()  
                          
                          
                            + function () {
                              console.log('a');
                            }()  `                          (在函数声明之前加上+ - ！之后也能执行)
这个函数执行完之后就不能找到a函数了。

  认识对象
`  var mrYao = {
  firstName : "xiaoyao",
  lastName : "yao",
  age : 99,
  handsome : false, 
  son : {
    name : wang,
    age : 180
  }
  wife : {
    name : zhou,
    age : 90    
  }
  smoke : function () {
    console.log('I am smoking, cool');  
  }
  drink: function () {
    console.log('I am drinking');
  }
  }`
  对象可以增删改查！
  delete后面加空格，就是使用这个方法，可以把对象的属性和方法删除。

对象的创建方法有  1、字面量   2、构造函数  （系统自带 new Object（）；Array（）；Boolean（）；String（）；自定义）  3、

系统的构造方法 var obj = new Object();就相当于var obj = {};叫：对象字面量/对象直接量

系统的构造方法不够好，可以自定义构造函数。

`function Person() {

}
var person = new Person;`
自定义构造函数大头风原则。



构造函数内部原理。使用new操作符会在内部隐式的进行三部曲。
1、在函数最前面隐式的加上this = {}  2、执行 this.xxx = xxx;
  3、隐式的(return)返回this
通过new出来的对象，如果你手动的加上return返回一个引用值的时候，那么系统的new隐式进行的三部曲中的第三步就不能返回this了，而会返回手动加上的return的东西。但是只要你手动加上的return返回的结果不是引用值，而是原始值的话不影响构造函数的内部原理的。

包装类。给原始值加属性、方法，访问原始值的属性、方法等等，都是包装类干的。系统内部自动给你加的。例如：
`  var num = 123;
  num.abc = 'a';
  console.log(num.abc);`结果为：undefined
因为num是一个原始值，数字类型的，系统会在内部隐式的给你转换成系统内部的Number对象，给你new出来。不过系统隐式的给你new出来之后没有保存他，只是没有让他报错，也并没有保存起来，所以访问不到他。再例如：
`  var str = 'abcd';
  str.lenth = 2;
  console.log(str.length);`结果为：4
因为str是一个字符串类型的原始值，他上面并没有.length方法，但是系统会把它隐式的new出来，new String（str）.length也就是4了。


原型  ：原型是对象function的一种属性，它定义了构造函数制造出的对象的公共祖先。通过该构造函数产生的对象，可以继承该原型的属性和方法。原型也是对象。
利用原型特点和概念，可以提取共有属性。
对象如何查看对象的构造函数，constructor。
`Person.prototype.name = "abc";
function Person() {
}
var person = new Person();
Person.prototype.name = "bcd";
console.log(person.name);`
结果为：bcd   (因为这是直接赋值的。注意跟下一题的区别。这个是原始值也就是在栈里面存着)

`Person.prototype = {
 name : "abc"
}
function Person() {
}
var person = new Person();
Person.prototype = {
   name : "bcd"
}
console.log(person.name);`
结果为：abc     (因为这个是引用值也就是在堆内存里面存着。而且这个person是Person  new出来的，所以有隐式的三步，在this里面会有__proto__=Person.prototype。而new又在第二次引用赋值之前，所以并不会改变name的值，因为__proto__已经提取到第一个name的值了)


 `  Son.prototype = {
      eat : function () {
        this.height ++;
        card : [100, 200]
      }
    
       };
       function Son() {
      this.height = 100;
       }
       var son = new Son;
       son.eat();   101
       son.eat();   102
       son.card.pop();`   200   拿出来200，原型里面就没有200了

  son 可以调用父亲Son的值，但是并不能改变父亲Son中的值。也就是说son.__proto__.height的值永远都是100。


绝大数对象的最终都会继承自Object.prototype
`var demo = {
  name : 'abc',
  age :234
  }
var obj = Object.create(demo); `
创建一个obj对象是以demo为原型的对象。括号里必须填东西，想要创建一个没有原型的对象里面要填null。


一个对象上的__proto__是追到他的父级的原型链上的，所有的对象的__proto__都会追到系统的Object上的，所以Object上就没有__proto__了。如果改变了一个对象上的__proto__就相当于改变了他的原型链，也就是改了他的父级的.prototype原型链了。原型链是一个对象，对象是引用值，修改的话就是换地址的，原先的空间并不会换的。比如：
`var obj = {name:"a"}; var obj1 = obj; obj = {name:"b"};console.log(obj1.name)`;结果为：a    ()


`var obj = {};
 document.write(obj); ` 打印结果为：[object Object]   因为打印一个文档流的话会隐式的把obj上的toString方法的结果给你打印出来。例如：`var obj = Object.create(null);obj.toString = function () {return '邓哥身体好'；}  document.write(obj);`  结果为：邓哥身体好
但是数字类型的，布尔类型的，数组类型的他们toString出来的就不是[object Object]形式的，因为他们的原型上就有重写的toString方法。    

toString方法是在原型链上的，所以一般都有，可以完全的分别出来对象，数组等等。但是undefined和null没有toString，因为他俩没有原型链。数字有toString，但是不能直接123.toString，因为数字后面跟着小数点会把这个小数点当做是浮点类型的小数点的。

浏览器有一个存在的bug。就比如0.14*100结果就为140.0000000002；精度不准的问题。
Math.radom().这是生成0-1之间的随机数，比如：for(var i = 0; i < 10; i ++) {var num = Math.random().toFixed(2) * 100;
console.log(num);} 这个就会出现精度不准的问题，就说因为计算机的精度不准，在处理小数不准是因为计算机是基于二进制编码的原因，无法修改的bug。toFixed()就有这个问题。上一题解决的办法就是不用toFixed()在最后取整用floor。比如：for(var i = 0; i < 10; i ++) {var num = Math.floor(Math.random() * 100);  console.log(num);}这次取整就不会出现不精准的问题了。

函数.call方法的使用。test()其实就是test.call();这个方法可以改变this的指向。括号里面的第一位参数就是this指向的对象，第二位开始可以放正常的参数了。缺点就是还调用了另一个函数，如下：
`function Wheel(wheelSize, style) {
  this.style = style;
  this.wheelSize = wheelSize;
}
function Sit(c, sitColor) {
  this.c = c;
  this.sitColor = sitColor;
}
function Model(height, width, leng) {
  this.height = height;
  this.width = width;
  this.leng = leng;
}
function Car(wheelSize, style, c, sitColor, height, width, leng) {
  Wheel.call(this, wheelSite, style);
  Sit.call(this, c, sitColor);
  Model.call(this, height, width, len);
}
var car = new Car(100, '花里胡哨的', '真皮座椅舒适'， 'red', 1800, 1900, 4900);`
企业开发的模块化，最后完工的成品是多个拼接起来的。

call 和apply的区别：call需要把实参按照形参的个数传进去；   apply需要传一个arguments数组。
call和apply都是改变this指向，区别就是传参列表不同。


typeof (new Array).__proto__.constructor()
结果为："object"     解析：先算括号里面的，再算点。优先级顺序。形式上又有typeof的两种形式的用法。

计算输入变量的字节长度，汉字的Unicode长度大于255，英文字母的Unicode长度小于等于255；
`var str = "kjfhasdkjf生命在于学习"
function bytestLength(str) {
   var count = str.length;
   for(var i = 0; i < str.length; i++) {
  if(str.charCodeAt(i) > 255) {
     count ++;
  }
  }
  return count;
}
或者
var str = "aldshfuioasdhf";
function bytestLength(str) {
   var count = 0;
   for(var i = 0, len = str.length; i < len; i ++) {
  if(str.charCodeAt(i) > 255) {
     count += 2;
  }else {
     count ++;
  }
   }
   return count;
}`


继承发展史：
1、传统形式---->原型链    缺点：过多的继承了没用的属性
2、借用构造函数   也就是用call或者apply的方法，其实是调用跟自己完全囊括的属性才能使用的，多调用了一次构造函数浪费效率了。    缺点：不能继承借用构造函数的原型； 每次构造函数都要多走一个函数
3、共享原则，共有原型。     缺点：不能随便改动自己的原型

圣杯模式：(构造函数想完全继承自父亲的原型，并且还可以添加自己特有的原型)
`Father.prototype.lastName = "Deng";
Father.prototype.sex = "male";
function Father() {

}
function Son() {

}
function inherit(Target, Origin) {
   function F() {};
   F.prototype = Origin.prototype;
   Target.prototype = new F();
   Target.prototype.constuctor = Target;
   Target.prototype.uber = Origin.prototype;
}
inherit(Son, Father)
var son = new Son();
var father = new Father();`



yahoo的YUI3库现在不用这个了。现在都用jQuery库了。YUI3库是这样写的  
`var inherit = (function () {
      var F = function () {};
      return function (Target, Origin) {
      F.prototype = Origin.prototype;
      Target.prototype = new F();
      Target.prototype.constuctor = Target;
      Target.prototype.uber = Origin.prototype;
      }
    }()); `    运用闭包的私有化变量属性。必须熟练掌握闭包的属性特点。


命名空间的问题。防止污染全局变量。一般解决办法就是使用立即执行函数，在立即执行函数里命名变量，变量会成为私有化变量，也就是利用闭包的特点。init初始化、入口。


对象还有一种访问属性的方法，除了obj.name访问对象obj的name属性，还可以obj['name'];浏览器在执行obj.name的时候回隐形的转换成name转换成字符串类型的形式执行，所以用字符串的形式更加快，有效率。而且使用字符串的形式这种方法更加的方便，在以后的使用中，字符串的使用频率更加高的。




对象、数组的遍历、枚举；`var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]; for(var i = 0; i < arr.length; i++) {console.log(arr[i]);}`

遍历对象的话就要用到for-in 循环了；
  `var obj = {
       name : 'abc',
       age : 123,
       sex : 'male',
       height : 180,
       weight : 75
     }
     for(var prop in obj) {
     console.log(obj.prop);` 这里有一个错误哦~！应该写成obj[prop]的形式。
  }
 obj.prop---->就相当于obj["prop"]，因为系统会隐式的把前面的改成后面的这种形式。
  这里有一个问题，用对象.prop的话，会访问这个对象上的属性。不过这个对象上并没有prop的属性，所以最后会打印出5个undefined。所以应该写成对象[name]属性的形式。记住哦~！！！

  这样遍历对象的话会把原型上的属性也会给遍历出来，但是不包括系统自己原型上本来就有的，只是自己手动设的才会连着打印出来的。所以要是只想遍历这个对象本身的属性的话，应该先判断一下是否属于自身的属性，用到的方法就是对象.hasOwnProperty

还有一个跟hasOwnProperty差不多的方法就是in，他的作用就是看一下对象上有没有这个这个属性，比如看一下对象是否有name的属性，就是：'name' in obj;属性值必须是字符串形式的。返回值是布尔类型的值。但是有一个缺点就是不管这个属性是不是你本身的，你父亲的他返回值也是true。


instanceof

eg:
`function Person() {};
  var person = new Person();
  person instanceof Person; `  返回结果为：true  看person是不是Person构造出来的；但是   person instanceof Object;  返回结果也为：true；   结论：看A的原型链上有没有B的原型，在原型链上的也认为是，所以这是往原型链上找的。

instanceof 方法检测一个对象A是不是另一个对象B的实例的原理是：查看对象B的prototype指向的对象是否在对象A的[[prototype]]链上。如果在，则返回true，如果不在怎返回false。不过有一个特殊的情况，当对象B的prototype为null将会报错（类似空指针异常）。
还有一个方法很像in的方法，他就是instanceof。官方给出的解释是 A对象是不是B构造函数构造出来的。 比如：A insftanceof B。
但是官方的解释是远远不够的，只要是在原来对象原型链之上的他的返回结果都是true。所以其实他的意思应该是：看一下A对象的原型链上有没有B的原型，也就是找祖先的，往原型链之上找到。所以instanceof解决了一个问题，就是typeof方法不能精确判断出来的问题。
eg：var arr = [] || {};
传进去一个变量，这个变量有可能是数组也有可能是对象，如何判断出来；有三种区分方法：
1. 用constructor可以区分出来
  [].constructor   返回结果为：function Array() {  {native code}  }
 var obj = {};
  obj.constructor   返回结果为：function Object() {  {native code}  }  
2. 用instanceof可以区分出来
  [] instanceof Array
  返回结果为：true
  var obj = {};
  obj instanceof Array
  返回结果为：false
3. 用toString方法可以区分出来（一般也都是用这种方法区分的）
  数组、对象等等都有自己的toString方法
  Object.prototype.toString.call([]);调用数组的toString方法  返回结果为："[object Array]"
  Object.prototype.toString.call({});调用对象的toString方法  返回结果为："[object Object]"
  Object.prototype.toString.call(123);调用数字的toString方法  返回结果为："[object Number]"
  toString方法可以准确区别出来数组和对象。并且在有父子页面的情况下也能准确识别出来，其他的两种方法就不能在子页面中识别出来父页面下类型了。所以一般我们都是用toString方法来区分的。



深度克隆：遍历对象  for(var prop in obj)
	1. 判断是不是原始值   typeof()  object
	2. 判断是数组还是对象，有三种方法：instanceof   toString  constructor  一般用toString方法，因为如果在原先的页面上再引入一个页面的话，引入进来的页面中的数组和对象就不符合原先的原则了，而toString方法则不会发生这种引用错误。
	3. 建立相应的数组或对象
	递归的方法。(必须找出口)

`var obj = {
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
      if(origin.hasOwnProperty(prop)) {
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
var target = deepClone(obj);`


三步运算符：?:
  条件判断  ？  是  ： 否  表达式运算之后会返回值
条件判断？前面的，条件成立的话执行：前面的运算表达式，条件不成立的话执行：后面的运算表达式。
var num = 1 > 0 ? ("10" > "9" ? 1 : 0) : 2;
结果为：0   （字符串形式的数字比较是逐位比较ASCII（阿斯克码）表）



数组
字面量 var arr = [];
var arr = [,,];  arr的结果为2个undefined。
var arr = [1,2,3,,,,7,8]

系统的构造方法：var arr = new Array(10.2);这样会报错的。只填一位的话会形成稀松数组，也就是var arr = new Array(10);会形成10位值为undefined的数组。还可以溢出读和写。

数组常用的方法：
改变原数组：push,pop,shift,unshift,sort,reverse
	   splic

push方法是在数组的最后添加参数，可以添加多位；
pop方法是在数组的最后剪切一位出来，并且（）里面不支持添加参数，添加也没啥用，所以每次只能剪切一位出来；
shift方法是在数组的最前面剪切一位出来；
unshift方法是在数组的最前面添加参数，并且可以添加多位；
reverse方法会把原数组逆转顺序。
splice()括号里填参数：第一位参数是从第几位开始，第二位参数是截取多少的长度，再往后面填的参数就是在切口处添加的参数，可以无穷多个了。切的刀口就在光标处，一般splice方法用的是添加数组的比较多。而且还可以在负数位开始截取。

sort方法是给数组按照升序排序的方法，而且是按照字符串阿斯克码进行排序的。所以一般是我们自己给sort()方法设置他的排序方法。
1、必须写两个形参   2、看返回值（1）当返回值为负数是，那么前面的数放在前面（2）为正数，那么后面的数在前 （3）为0，则不动
   冒泡排序的规则；
arr.sort(function(a, b) {
if(a > b) {
  return 1;
}else {
  return -1;
}
});

简写这个代码的话就是;
`arr.sort(function(a, b) {
  return a - b;   升序
  return b - a;   降序
})
`

给一个有序的数组，乱序
`var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
arr.sort(function() {
  return Math.random() - 0.5;
});
`
按照对象的年龄升序排列；
`var cheng = {
  name : "cheng",
  age : 18,
  sex : 'male',
  face : "handsome"
}
var deng = {
  name : "deng",
  age : 40,
  sex : undefined,
  face : 'amazing'
}
var zhang = {
  name : "zhang",
  age : 20,
  sex : "female"
}
var arr = [cheng, deng, zhang];
arr.sort(function(a, b) {
  return a.age - b.age;
})`


不可改变原数组
concat,join--->split,toString,slice  

concat连接  arr.concat(arr1)  把数组arr1加到数组arr后面。
数组的toString是把数组变成字符串。
slice(从该位开始截取，截取到该位)
join("-")方法可以再数组的每一位之间加上-连接成一个字符串。
split("-")方法可以根据"-"把数组的字符串拆成单个的。可以根据任意的字符串拆分。

例题：
`var str = "alibaba";
var str1 = "baidu";
var str2 = "tencent";
var str3 = "toutiao";
var str4 = "wangyi";
var str5 = "xiaowang";
var str6 = "nvsheng";
var strFinal = "";
var arr = [str, str1, str2, str3, str4, str5, str6];`
字符串放在栈内存里存储，first in, last out;所以字符串的连接是调用每一个字符串进行连接，效率低下，一般我们把字符串先保存到数组中进行调用的，这样效率更高，因为数组的散列结构。


类数组 arguments 
例：
`var obj = {
  "0" : 'a',
  "1" : 'b',
  "2" : 'c',
  "length" : 3,
  "push" : Array.prototype.push,
  "splice" : Array.prototype.splice
}`
属性要为索引(数字)属性，必须有length属性，最好加上push方法。

例题：
`var obj = {
  "2" : 'a',
  "3" : 'b',
  "length" : 2,
  "push" : Array.prototype.push
}
obj.push('c');
obj.push('d');
console.log(obj);`
结果为：obj{
  "2" : "c",
  "3" : "d",
  "length" : 4,
  "push" : Array.prototype.push
}


完美区别各种类型的函数对象

`function type(target) {
  var ret = typeof(target),
  template = {
    "[object Array]" : "array - object",
    "[object String]" : "string - object",
    "[object Number]" : "number - object",
    "[object Boolean]" : "boolean - object",
    "[object Object]" : "object - object"
  }
  if(target === null) {
  return "null";
  }else if(ret == "object") {
  var str = Object.prototype.toString.call(target);
  return template[str];
  }else{
  return ret;
  }
}`

数组去重的方法：hash哈希的方法：基于的就是对象的命名规则就是相同的命名会覆盖，所以达到了数组去重的作用。与当年阿里巴巴考的类数组的例题有点儿相似。
`var arr = [1, 2, 3, 4, 1, 3, 4, 2, 4, 5, 6, 4, 0, 0, 0];
Array.prototype.unique = function () {
  var temp = {},
      arr = [],
      len = this.length;
  for(var i = 0; i < len; i ++){
  if(!temp[this[i]]) {
    temp[this[i]] = "abc";
    arr.push(this[i]);
  }
  }
  return arr;
}`
this[i]代表数组的第i位。随意取名的话“abc”不能换成this[i],因为要是数组里面有undefined或者0等其他为false的值的话，这个去重就失败了。


this问题的例题：谁调用的this方法this就指向谁。
`var name = "window";
var obj = {
  name : 'obj',
  say : function (){
  console.log(this.name);
  }
}
var fun = obj.say();`
console.log(obj.say);    结果为：obj
console.log(obj.say.call(window));    结果为：window
console.log(fun());      结果为：window
console.log(fun.call(obj));    结果为：obj



闭包形成的原因：一个函数套着另一个函数，并且必须要把里面的函数保存到最外面函数的外面才能形成闭包的。把里面的函数保存出来不一定非要用return。也可以在外部调用也可以的。例如：
`var obj = {};
    function a() {
      var aa = 123;
      function b() {
      console.log(aa);
      }
      obj.fun = b;
    }
    a();
    obj.fun(); `    结果就为：123    因为把里面的函数保存到了外部，会形成闭包，所以就能访问到a函数已经销毁的变量。



1、一个字符串[a-z]组成，请找出该字符串第一个只出现一次的字母
2、字符串去重；

`var str =  "adshqwertyuioonpqwertmyuiopasdfghjklasdfghjklzxcvb";
function sayFirst(target) {
  var len = target.length,
      count = 0;
  for(var i = 0; i > len; i ++) {
  if(target) {
    
  }
  }
}`

企业开发中为了防止出错的，出错的话之后的代码就不会执行了；如果网速不好话，代码里有的数据没有下载完就会报错的；
try{}里面的代码有错误的话，如下：不会执行错误代码，而且错误代码下面的正确代码也不会执行了，但是不会报错的。
而try里面有错误的话会直接跳到catch里面执行catch里面的代码，catch就是为了容错，而且是返回错误信息的。e可以随便写。
`try{
  console.log("a");
  console.log(b);
  console.log("c");
}catch(e) {
  alert(e.name + " : " + e.message);
}`

Error.name的六种值对应的信息：
1. EvalErron:eval()的使用与定义不一致
2. RangeErron:数值越界
3. ReferenceError:非法或不能识别的引用数值（没定义就使用的原因）
4. SyntaxError:发生语法解析错误（代码中有中文的标点符号，在解析是就会报错）
5. TypeError:操作书类型错误
6. URLError:URL处理函数使用不当


es5.0严格模式   es3.0 和 es5.0产生冲突的部分，就用es5.0，否则使用es3.0的；严格模式优点是减少了编程错误的发生。

es5.0的启用："use strict"可以写在一个函数里，那么就在这个函数里只能使用严格模式了。在严格模式中不能使用with（改变函数作用域）,arguments.callee(代替匿名函数的作用),func.caller（函数执行时才能调用，也是代替匿名函数的作用）等等方法；而且还有变量赋值前必须声明。this必须被赋值，预编译之前局部为undefined，不再是指向window了。拒绝重复属性和参数。

with()可以改变作用域链，先找括号里面填写的对象的作用域链，没有的话才会找自己的作用域链上的。命名空间的应用，代码简化的作用。但是更改作用域链的话，会使效率降低。

eval()括号里能把字符串当代码使用。是魔鬼！还可以改变作用域，他还有自己独立的作用域。














