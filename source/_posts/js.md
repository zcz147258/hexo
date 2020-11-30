---
title: JavaScript基础
date:
updated:
type: "tags"
categories: JavaScript
comments:
description: JavaScript基础
keywords: JavaScript基础
top_img: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=4234896097,4021899470&fm=26&gp=0.jpg
cover: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=4234896097,4021899470&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 一.基本语法

1.alert();浏览器弹出一个警示框

2.document.write();在标签中写入内容

3.console.log();在控制台输出结果

常用浏览器内核

IE浏览器  -ms-

Opera浏览器    -o- 

Safari浏览器   -webkit-

Firefox浏览器   -moz-

Chrome浏览器  -webkit-

# 二.字面量与变量

1.字面量  都是一些不可改变的量 ，容易出错，不方便使用。

2.变量  可以用来保存字面量，而且变量的值也是可以任意改变的

```javascript
var a;
//  声明过变量之后需要对该变量进行赋值
a = 1;
// 在控制台中输出a变量的结果
console.log(a);   --> 1

// 这要声明变量需要两步  比较麻烦  我们可以缩写为一步 也就是 声明与赋值同时进行
var a = 1;
console.log(a);

// 现在有一个字面量 80  我们现在不知道这个字面量到底代表着什么
// 这时候 变量可以对该字面量进行一个描述 例如：
var age = 80;
age == 年龄;
```

# 三.标识符

在js中我们可以自主命名的都是标识符，例如变量名，函数名，属性名都是与标识符，

*但是标识符的命名需要注意以下几点

1.标识符可以含有 字母 数字 下划线 $

2.标识符不能以数字开头

3.标识符中不能是ES中的关键字或者保留字

4.标识符一般采用驼峰命名法 首字母小写 ，每个单词的开头字母大写，其余字母小写

# 四，数据类型

js中总共有6中数据类型

返回字符串类型  用typeof

String 字符串

Number 数值

Boolean 布尔值

Null 空值  用typeif检查  得到 object

Undefined 未定义

Object 对象

前五个都是基本数据类型  后面Object属于引用数据类型

## 4.1字符串

String 字符串 

在JS中字符串需要用引号 括起来 

 var str = "我是字符串"; 

 单双引号都可以 引号不能嵌套，双引号内不能在有双引号，单引号内不能在有单引号  双引号内可以有单引号  单引号内可以有双引号

在字符串中 我们可以使用 \ 作为转义字符

例如： \n 代表  换行

​			\t 代表制表符

## 4.2Number

在JS中所有的数值都是 Number类型，包括整数和浮点数，在谷歌浏览器中控制台中 数值是蓝色 字符串是黑色

在JS中我们可以使用一个运算符  typeof   来检查一个数据类型

如果使用JS 对浮点数进行运算，可能得到一个不精确的结果

```javascript
var a = 0.1 + 0.2;
console.log(a);  -->  0.3000000000000000
```

```
console.log(typeof(a))
```

a为null  输出  object

a为 NaN返回 number

isNAN函数表示 是不是非数字  如果是非数字则返回true;

## 4.3 Boolean 布尔值

布尔值主要有两个，主要用来逻辑判断

true代表真

false代表假

## 4.4 Null 和 Undefined

Null 类型的值只有一个，那就是 null

null 这个值专门用来表示一个为空的对象

使用typeof 检查一个null 值的时候，会返回object

​	Undefined（未定义）类型的值只有一个，就是undefined

​		当声明一个变量，但是并不给变量赋值时，它的值就是undefined

​		使用typeof 检查一个undefined 时，也会返回 undefined

  console.log(null == undefined); //true 

  console.log(null === undefined); //false 

# 五、强制数据类型转换

指将一个数据类型强制转换为其他的数据类型

类型转换主要指，将其他的数据类型，转换为 String Number Boolean

## 5.1 将其他数据类型转换为String

```javascript
var a = 123;
console.log(typeof a);
console.log(a);
// 将 a 变量转换为字符串
/*
	第一种方法：
		调用被转换数据类型的toString()方法
*/
a.toString(); // 注意大小写

console.log(typeof a); --> number  // 结果没有变化
console.log(a);
// 注意：该方法不会影响到原变量，它会将转换的结果返回

var b = a.toString();
console.log(typeof b);
// 布尔值转换字符串
var a = true;
a = a.toString();
console.log(typeof a);
// null 和 undefined 这两个值没有toString()方法
/*
	方法二：
		调用String()函数，并将被转换的数据作为参数传递给函数
		使用String()函数做强制类型转换时，
			对于Number和Boolean实际上就是调用toString()方法
			但是对于null和undefined，就不会调用toString()
				它会直接将null 转换为 "null" undefined同理
*/
```

## 5.2将其他数据类型转换为number

只有   NAN和数字！



null == underfined

```javascript
/*
	将其他的数据类型转换为Number
		方式一：
			调用Number()函数
				字符串 转换 数字
					1. 如果是纯数字的字符串，则直接将其转换为数字
					2. 如果字符串中有非数字的内容，则转换为NaN underfined
					3. 如果字符串是一个空串或者是一个全是空格的字符串，则转换为0 null false 
*/
var a = "123";
a = Number(a);
console.log(typeof a, a); --> number

var a = "abc1";
a = Number(a);
console.log(typeof a, a); --> number NaN

var a = "   ";
a = Number(a); --> 0

// 布尔值 转换 数字
var a = true;
a = Number(a); --> 1

var a = false;
a = Number(a); --> 0

// null 转换为 数字
var a = null;
a = Number(a); --> 0

// undefined 转换为 数字
var a = undefined;
a = Number(a); --> NaN

// 现在我们可以将 一个纯数字的字符串转换为数字 现在我们通过js获取到一个元素的 宽度 ："125px"
// 刚好我需要用这个值 进行计算 这时候用我们的Number()函数肯定是不行的 
// 我们有新的函数可以解决这个问题 parseInt() 注意大小写
var a = "125px";
a = parseInt(a); --> 125
// parseInt()函数的作用就是 从左到右 依次去找数字 如果碰到非数字的话就会停止查找将结果返回

// 对应的还有一个 parseFloat()函数  用来取小数
var a = "123.1234566px";
a = parseFloat(a); --> 123.1234566


总结
```

## 5.3 将其他数据类型转换为 布尔值（Boolean）

```javascript
/*
	转换为Boolean 我们使用的就是Boolean()函数
*/
var a = 123;
// 调用Boolean()函数
a = Boolean(a); --> true
// 数字 0 是 false NaN 也是 false
var a = NaN;
a = Boolean(a); --> false
// 除了 0 和 NaN 以外 都是true

// 字符串转布尔值
var str = "abcd";
str = Boolean(str); --> true

var str = "false";
str = Boolean(str); --> true
// 字符串转换布尔值 除了空串 其余的都是true
var str = '';
str = Boolean(str); --> false

// null 和 undefined 转换为布尔值
var a = null;
a = Boolean(a); --> false
var a = undefined;
a = Boolean(a); --> false
// null 和 undefined 都可以转换为布尔值 false
// 对象也会转换为 true
```

总结  空的字符串 null NAN undefined 0   都转化为  false 剩下的都是 true 

# 六、运算符

typeof 就是一个运算符  用来获取一个值的数据类型

## 6.1 一元运算符

+正号

—负号

## 6.2自增与自减

++a  先自加后运算 

a++ 先运算后自加

## 6.3逻辑运算符

！     &      ||   

非   与    或

取反    有一个假都假    有一个真为真

```javascript
// 对与非布尔值进行与或运算时，会先将其转换为布尔值，然后在进行运算，并且返回原值
var result = 1 && 2;
console.log(result); --> 2
var result = 2 && 1;
console.log(result); --> 1
// 如果两个值 都为true 则返回后面的

// 第一个值为false 则返回第一个值
var result = 0 && 2;
console.log(result); --> 0

// 第一个值为true 第二个为false 则返回第二个值
var result = 1 && NaN;
console.log(result); --> NaN

// 逻辑或 也是先将其转换为布尔值 然后进行运算
// 第一个值为true 则直接返回第一个值
var result = 1 || 0;
console.log(result); --> 1
// 第一个值为false 则回去看第二个值 并返回第二个值
var result = NaN || 100;
console.log(result); --> 100

var result = "" || "hello"; --> ???
var result = -1 || "你好"; --> ???
```

## 6.6 关系运算符

​	通过关系运算符可以比较两个值之间的大小关系，如果关系成立返回 true 不成立则返回 false

```javascript
result = 1 > true; // false
result = 1 >= true; // true
result = 1 > "0"; // true
result = 10 > null; // true
result = 10 > "hello"; // false  NaN 与任何值比较时 都时false
result = 10 < undefined; // false
result = true > false; // true
result = false > true; // false
// 比较两个字符串时，不会转换为number类型在进行比较，而是去比较字符的Unicode编码
// 在比较字符编码时是一位一位的比较
result = "1" < "5"; // true
result = "a" > "b"; // false
// 字符串中可以使用转义字符输入unicode编码  \u四位编码
console.log("\u2620")
// HTMl中使用编码 &#四位编码;  注意编码要从十六进制转换为十进制
<p>&#9760;</p>
```

## 6.7  相等运算符

​	相等运算符用来比较两个值是否相等

​		如果相等会返回true，否则返回false

===   严格相等运算符

!==    严格不等运算符

！=     不相等运算符

## 6.8 条件运算符  三元运算符

语法：条件表达式 ? 语句1 : 语句2;



## 6.9 运算符的优先级

 https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Operator_Precedence 





# 七 代码块 

# 八 流程控制语句

​	1. 条件判断语句

​		2. 条件分支语句

		3. 循环语句

## 8.1条件判断语句   if

## 8.2条件分支语句  switch

```javascript
// 语法：
/*
	switch(条件表达式){
		case 表达式:
			语句...
			break;
		case 表达式:
			语句...
			break;
		case 表达式:
			语句...
			break;
		default:
			语句...
			break;
	}
	switch...case..语句
	在执行时会依次将case后的表达式的值和switch后的条件表达式的值进行严格相等比较
	如果比较结果为true，则从当前case处开始执行代码
*/
// 根据num的值，输出对应的中文
```

## 8.3while 循环语句

# 九、对象

```javascript
// 如果使用基本数据类型的数据，我们所创建的变量都是独立的，不能成为一个整体。

// 对象属于一种复合的数据类型，在对象中可以保存多个不同数据类型的属性
// 让这些变量都存储在一个对象中，那他们就有联系了，都在一个对象中
// 对象的分类：
/*
	1. 内置对象
		由ES标准中定义的对象，在任何的ES的实现中都可以使用
		比如：Math String Number Boolean Function Object...
	2. 宿主对象
		由JS的运行环境提供的对象，目前来讲主要指浏览器提供的对象
		比如： BOM DOM
	3. 自定义对象
		由开发人员自己创建的对象
*/
// 创建对象
var obj = new Object(); // 使用new关键字调用的函数，是构造函数
// 构造函数是专门用来创建对象的函数


// 去读取一个对象中没有的属性时，会返回undefined，并不会报错

// JS中的基本数据类型都是保存在栈内存中，值与值之间会独立存在的，修改一个不会影响另外一个
// 对象是保存在堆内存中的，每创建一个新的对象，都会在堆内存中开辟出一个新的空间
// 而变量保存的是对象的内存地址（对象的引用）
var obj1 = new Object();
var obj2 = new Object();
console.log(obj1 == obj2); --> false

/*
	对象的字面量写法
*/
var obj = {
    name:"www",
    age:18
}
```

## 9.1对象的两种取值方式

```
通过点(.) 和 方括号 ( [] ) 的不同之处
1、(.) 点操作符: 静态的。
2、([]) 中括号操作符: 动态的。

区别
1.([]) 可以用变量作为属性名或访问，而点方法不可以  中括号内容需要加’‘引号
2.[]中括号法--可以用数字作为属性名,而点语法不可以; 
3, [] 可以动态访问的属性名，可以在程序运行时创建和修改属性，点操作符就不行！
4,如果属性名中包含会导致语法错误的字符，或者属性名是关键字或者保留字，也可以使用方括号表示法。
```



# 十 函数

```javascript
构造函数创建 
var bbb=new Function(
                console.log("kkkkkkkk")
            );
 bbb();
我们会使用 函数声明 来创建一个函数
    语法：
 function 函数名(形参1，形参2，形参...){
            语句...
      }
function fun(){
    console.log(1);
}
fun();

函数表达式来创建一个函数 （匿名函数）
var fun = function(){
    console.log(1);
}
fun();
     
     
 函数的参数
 在函数体中可以使用形参 但是如果没有传入实参，则返回默认值undefined;
     
     
     
  立即执行函数（自执行函数）
 (function(){

 })
 这样我们的匿名函数没有报错，但是这个时候并没有执行它，那执行它的方法就是在括号外面进行一次调用
 (function(){
    alert(1);
 })()
 函数在定义完之后，立即被调用
 立即执行函数只会执行一次
 也可以说是一次性函数
 自执行函数的形参 实参 和 普通函数是一样的
他的功能
它可以帮你封装大量的工作而不会在背后遗留任何全局变量。
你定义的所有变量都会成员立即执行函数的局部变量，所以你不用担心这些临时变量会污染全局空间
可以使用这种技术可以模仿一个私有作用域，用匿名函数作为一个“容器”，“容器”内部可以访问外部的变量，而外部环境不能访问“容器”内部的变量
可以添加更多的加强模块，移除它们，单独测试它们，允许用户去禁用它们等等



我们可以使用 for...in语句来枚举对象中的所有属性
 for(var i in obj){
    console.log(i); i 代表的就是对象中的属性名
 }

     
     
    JS中的作用域：
    全局作用域：函数外就是全局作用域
        全局作用域中有一个全局对象window，我们可以直接使用，它代表浏览器的窗口
        是由我们的浏览器创建的
        在全局作用域中，创建的变量都作为window对象的属性来保存
        var a = 1;
        window.a; --> 1
        但是我们在使用的时候可以将window对象省略掉
        创建的函数都会作为window对象的方法保存
        function fun(){
            alert(1);
        }
        window.fun();
        同样window可以不写
        alert() == window.alert()
    函数作用域：函数内部
    全局作用域中声明的变量，可以在任何地方使用
    函数作用域中用var声明的变量，在全局作用域中无法使用
        在函数作用域中使用一个变量时，它会先在函数中寻找，如果没有就去上一级找


```

## 10.1 函数中的隐藏参数 this

​	this 会指向一个对象

​	这个对象我们称为函数指向的上下文对象

​	根据函数调用方式的不同，this会指向不同的对象

```javascript
function fun(){
    console.log(this);   window
}
以函数的形式调用时，this永远指向window

var obj = {
    sayName: function(){
        console.log(this);
    }
}
以一个方法的形式来调用，this永远指向调用该方法的对象

构造函数中 this 指向的是一个空对象
```

## 10.2 工厂模式创建对象

​	在函数中定义一个对象的模板 需要一个对象 就调用一次函数

​	但是我们使用工厂模式创建的对象 没有一个类型的区别

​	定义一个人的工厂 定义一个机器人的工厂 最终出来的对象都是Object 无法区分

```javascript
function person(name, sex, age){
    var obj = {};
    obj.name = name;
    obj.sex = sex;
    obj.age = age;
    return obj;
}
var a = person("刘能", "male", 60);
var b = person("赵四", "male", 61);
```

## 10.3 构造函数创建对象

​	构造函数就是用来创造对象实例的 和 工厂模式相似

​	构造函数就是一个普通的函数，不同的是构造函数首字母大写

​	构造函数和普通函数的区别就是，调用的方式不同

​		普通函数是函数名调用，而构造函数是通过new关键字调用(重要)

```javascript
function Person(name, age){
    // 写法不同于 工厂模式
    this.name = name;
    this.age = age;
    this.sayName = function(){
        console.log(this.name);
    }
}
var person1 = new Person("谢广坤", 180);
使用同一个构造函数创建的对象，我们称为一类对象，也将一个构造函数称为一个类
我们将通过一个构造函数创建的对象，称为是该类的实例
```

**new 关键字的作用：**

​		**1. 在函数体中声明了一个空对象**

​		**2. 将函数体中的所有this 指向这个空对象**

​		**3. 逐行执行函数中的代码**

  4. **将空对象 return 返回出去**

     ```javascript
     instanceof 可以检查一个对象是否是一个类的实例
     语法：
     	对象 instanceof 类（构造函数）
     	如果是 返回 true 否则 返回 false
     console.log(per instanceof Person); true
     console.log(per instanceof Dog); false
     所有的对象都是Object的后代
     所以任何对象和Object做instanceof检查时都会返回true
     
     ```

in   关键字用来检查一个属性是否属于一个对象
​       name in obj
​     ```
​     
~~~js
 ```javascript
 这样就导致了构造函数执行一次就会创建一个新的方法，执行一万次就创建一万个方法，
 最重要的是这些方法做的事都是一样的
 那我们可以让所有对象 共享这个方法 这样就没必要创建多个方法了
 function Person(name, age){
     this.name = name;
     this.age = age;
     this.sayName = sayName;  ******
 }
 function sayName(){
     console.log(this.name);
 }
 var person1 = new Person("谢广坤", 180);
 我把sayName方法定义在了全局作用域中 这样的话就只有一个函数
~~~
我们每个对象只需要去调用公共的函数就OK了 
​     但是我们把函数定义在全局作用域中 会污染我们的命名空间

##      10.4 原型

```javascript
   
     ```javascript
     每个对象都有 __proto__ 属性，但只有函数对象才有 prototype 属性
     
     在默认情况下，所有的原型对象都会自动获得一个 constructor（构造函数）属性，这个属性（是一个指针）指向 prototype 属性所在的函数（Person）
     
     结论：原型对象（Person.prototype）是 构造函数（Person）的一个实例。
     
     对象 person1 有一个 __proto__属性，创建它的构造函数是 Person，构造函数的原型对象是 Person.prototype ，所以：
     person1.__proto__ == Person.prototype
     
     
     
     
     Person.prototype.constructor == Person;
person1.__proto__ == Person.prototype;
     person1.constructor == Person;

     

     原型面试题
         var A = function() {};
		A.prototype.n = 1;
     	var b = new A();
     	A.prototype = {
     	  n: 2,
     	  m: 3
     	}
     	var c = new A();
     
     	// console.log(b.n);  1
     	// console.log(b.m);  undefined
     
     	// console.log(c.n);  2
     	// console.log(c.m);  3
     
     
     var F = function() {};
     	// console.log(Object.prototype.__proto__)
     	Object.prototype.a = function() {
     		// 最顶层的object 里面的函数
     	  console.log('a');
     	}
     	Function.prototype.b = function() {
     	  console.log('b');
     	}
     
     	var f = new F();
     
     	f.a();
     	// f.b();报错
     
     	F.a();
     	F.b();
     	
     	
     	原型面试题
     	function A(){
     		B = function(){console.log(10)}
			return this;
     	}
		A.B = function(){
			console.log(20)
		}
		A.prototype.B = function(){
			console.log(30)
		}
		var B = function(){
			console.log(40)
		}
		function B(){
			console.log(50)
		}

		A.B()  20
		B()   40
		A().B()  10
		B()  10
		new A.B()  20
		new A().B()   30



		var B = function () {console.log(40)}

		function B() {console.log(50)}
同名 -> 函数提升会 > 变量提升
// 换言之 同名的函数表达式和函数声明同时存在时 总是执行表达式

new  关键字的作用
创建一个新对象；
将构造函数的作用域赋值给新对象；
执行构造函数中的代码；
返回新对象
```

##      10.5 call apply bind

console.dir()查看详情信息

```js
相同点
  都可以改变函数内得this指向，第一个参数为改变成那个对象
不同点
	1.call 方法第二个参数就开始为函数的参数  函数使用这个方法会自动执行
    2.apply 方法第二个参数就开始为数组,数组中为函数的参数  函数使用这个方法会自动执行
    3.bind 方法使用之后,会将函数当作返回值返回，在返回值中穿参数就是函数的参数。
```

## 10.6 arguments

```js
在调用函数时，浏览器会传入两个隐藏的参数：
	1. this
	2. arguments
function fn(){
    console.log(arguments);
}
fn();
arguments 是一个类数组对象 它不是数组 但是它也可以通过索引来操作数据，也可以获取长度
arguments instanceof Array   false
arguments 代表函数调用传入的所有实参 
arguments 的length属性就是用来获取实参的长度
这时候就算没有形参 我们也可以使用实参  arguments[0]就是第一个实参

利用argument进行数组去重
function deleterepeat(){
    var b = [];
    for (var i = 0; i < arguments.length; i++) {
        if(b.indexOf(arguments[i]) == -1){
            b.push(arguments[i]);
        }
    }
    console.log(b);
}
deleterepeat(1,3,2,4,5,9,8,7,6,4,2,5);
```

## 10.7 拷贝

```js
浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存。
但深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象。

浅拷贝 var a = {
	hobby = 'football';
	sex = 'male';
}
var b = a;

深拷贝
 var a = {
     name:'ddd',
     sex:'aaa'
 }
 var b = {};
 for( i in a){
     b[i] = a[i];
 }
 console.log(a);
 
 常见的拷贝
 Object.assign()   浅拷贝
 解构赋值  浅拷贝
 json.stringify  深拷贝
 Object.create()  深拷贝
```

## 10.8 继承

```js
1.原型链继承
继承的本质就是复制，即重写原型对象，代之以一个新类型的实例。
原型链方案存在的缺点：多个实例对引用类型的操作会被篡改。
function Person(name,sex){
		 	this.name = name;
		 	this.sex = sex;
            }
            Person.prototype.text = function(){
            console.log(this.name);
            }
            function Monkey(p){
            this.p = p;
            }
            Monkey.prototype = new Person('ppp','bbb');
            // console.log(Monkey.prototype.__proto__);
            var swk = new Monkey('18');
            console.log(swk)
            swk.text();

2.构造函数继承
使用父类的构造函数来增强子类实例，等同于复制父类的实例给子类（不使用原型

缺点：
只能继承父类的实例属性和方法，不能继承原型属性/方法
无法实现复用，每个子类都有父类实例函数的副本，影响性能
function Person(name,sex){
			this.name = name;
			this.sex = sex;
		}
		Person.prototype.text = function(){
			console.log(this.name);
		}
		function Monkey(p){
			Person.call(this,'ppp','bbb');

			this.p = p;
		}
		var swk = new Monkey('18');
		console.log(swk)

		// var swk = new Monkey('18');
		// Person.call(swk,'ppp','bbb');
		// console.log(swk)
3.组合继承
组合上述两种方法就是组合继承。用原型链实现对原型属性和方法的继承，用借用构造函数技术来实现实例属性的继承。

缺点
实例对象instance1上的两个属性就屏蔽了其原型对象SubType.prototype的两个同名属性。所以，组合模式的缺点就是在使用子类创建实例对象时，其原型中会存在两份相同的属性/方法。

function Person(name,sex){
			this.name = name;
			this.sex = sex;
		}
		Person.prototype.text = function(){
			console.log(this.name);
		}
		function Monkey(p){
			Person.call(this,'mmm','lll');
			this.p = p;
		}
		Monkey.prototype = new Person('ppp','bbb');
		var swk = new Monkey('18');
		console.log(swk)
		
4.原型式继承
利用一个空对象作为中介，将某个对象直接赋值给空对象构造函数的原型。
object()对传入其中的对象执行了一次浅复制，将构造函数F的原型直接指向传入的对象。
        function object(obj){
          function F(){}
          F.prototype = obj;
          return new F();
        }
        var person = {
              name: "Nicholas",
              friends: ["Shelby", "Court", "Van"]
            };
  缺点 原型链继承多个实例的引用类型属性指向相同，存在篡改的可能。  篡改 person即原型
无法传递参数 
ES5中存在Object.create()的方法，能够代替上面的object方法。

5.寄生式继承
核心：在原型式继承的基础上，增强对象，返回构造函数
函数的主要作用是为构造函数新增属性和方法，以增强函数

function createAnother(original){
  var clone = object(original); // 通过调用 object() 函数创建一个新对象
  clone.sayHi = function(){  // 以某种方式来增强对象
    alert("hi");
  };
  return clone; // 返回这个对象
}
缺点（同原型式继承）：

原型链继承多个实例的引用类型属性指向相同，存在篡改的可能。
无法传递参数

6、寄生组合式继承
结合借用构造函数传递参数和寄生模式实现继承

这个例子的高效率体现在它只调用了一次SuperType 构造函数，并且因此避免了在SubType.prototype 上创建不必要的、多余的属性。于此同时，原型链还能保持不变；因此，还能够正常使用instanceof 和isPrototypeOf()
这是最成熟的方法，也是现在库实现的方法

7.、混入方式继承多个对象

function MyClass() {
     SuperClass.call(this);
     OtherSuperClass.call(this);
}

// 继承一个类
MyClass.prototype = Object.create(SuperClass.prototype);
// 混合其它
Object.assign(MyClass.prototype, OtherSuperClass.prototype);
// 重新指定constructor
MyClass.prototype.constructor = MyClass;

MyClass.prototype.myMethod = function() {
     // do something
};
Object.assign会把 OtherSuperClass原型上的函数拷贝到 MyClass原型上，使 MyClass 的所有实例都可用 OtherSuperClass 的方法。

8.8、ES6类继承extends
extends关键字主要用于类声明或者类表达式中，以创建一个类，该类是另一个类的子类。其中constructor表示构造函数，一个类中只能有一个构造函数，有多个会报出SyntaxError错误,如果没有显式指定构造方法，则会添加默认的 constructor方法，使用例子如下。



```

## 10.9 垃圾回收机制

```js
程序运行过程中会产生垃圾
	这些垃圾积攒过多以后，会导致程序运行的速度过慢，
    所以我们需要一个垃圾回收的机制，来处理程序运行过程中产生的垃圾
var obj = new Object();

这个对象我们进行了一系列的操作 最后不使用这个对象了 这时候干啥呢
我们将这个变量与这个对象断开链接
var obj = null;
那这时候在堆内存中的这个对象 就是一个垃圾 虽然断开连接 但是它还存在
这种对象过多会占用大量的内存

问题就是咋样去清理这个垃圾
在JS中拥有自动的垃圾回收机制，会自动将这些垃圾对象从内存中销毁
我们不需要也不能进行垃圾回收的操作
但是你如果不断开连接的话 浏览器不会去清理这个对象的
那我们需要做的就是 将用完的对象设置为 null

js中最常用的垃圾回收方式就是标记清除。当变量进入环境时，例如，在函数中声明一个变量，就将这个变量标记为“进入环境”。从逻辑上讲，永远不能释放进入环境的变量所占用的内存，因为只要执行流进入相应的环境，就可能会用到它们。而当变量离开环境时，则将其标记为“离开环境”。

  1、意外的全局变量引起的内存泄漏
  2.、闭包引起的内存泄漏
  3.没有清理的DOM元素引用
  4.被遗忘的定时器或者回调
```

## 10.10闭包

```js
函数内部的不用关键字声明的变量 会被提升到全局变量  叫做隐式全局变量

只有函数内部的子函数才能读取局部变量，因此可以把闭包简单理解成"定义在一个函数内部的函数"。
所以，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。

闭包的用途   一个是前面提到的可以读取函数内部的变量
			第二个 是让这些变量的值始终保持在内存中。
因此f1也始终在内存中，不会在调用结束后，被垃圾回收机制（garbage collection）回收。

闭包的注意点
1.由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除
2.闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。


for (var i = 0; i < 5; i++) {
    setTimeout(function() {
        console.log(new Date, i);
    }, 1000);
}

console.log(new Date, i);
如果我们约定，用箭头表示其前后的两次输出之间有 1 秒的时间间隔，而逗号表示其前后的两次输出之间的时间间隔可以忽略，
如果期望代码的输出变成：5 -> 0,1,2,3,4，该怎么改造代码？
```



#      十一、数组





​     


​     

```js
        数组的存储性能比普通对象要好，在开发中我们经常使用数组来存储一些数据
     创建数组对象


    
     读取数组中的元素
     	语法：数组[索引]
     	console.log(arr[0]); 10
     	console.log(arr[3]); undefined
     	如果读取数组中不存在的元素，不会报错，而会返回undefined
     获取数组的长度
     利用length属性 向数组最后一位添加一个新元素
     	语法：数组[数组.length] = 新值
     	arr[arr.length] = 33;
    console.log(arr); [10,20,33]
     


     使用构造函数创建数组时，也可以同时添加元素，将要写的元素写在实参中
     var arr = new Array(1,2,3,4);
     console.log(arr); [1,2,3,4];
     当你在实参中只写一个数字的时候代表创建一个长度为多少的数组
     var arr = new Array(10);
     console.log(arr.length); 10
     数组中的元素可以是任意的数据类型
     var arr = [1,"a",true,null,undefined,{},[1,2,3]];
     二维数组就是数组套数组



	var arr = ["刘能","赵四","谢广坤"];
     push方法 向数组的最后一位添加一个或多个新的元素，并返回数组的长度
     var result = arr.push("宋小宝","小沈阳","小沈龙");
     console.log(arr); ["刘能","赵四","谢广坤","宋小宝","小沈阳","小沈龙"]
     push方法有返回值 返回新的长度
     console.log(result); 6
     
     pop方法 可以删除数组的最后一位并返回它
     var result = arr.pop();
     console.log(arr); ["刘能","赵四","谢广坤","宋小宝","小沈阳"]
     console.log(result); "小沈龙"
     
     unshift方法 向数组的第一位添加一个或者多个新元素 并返回新的数组长度
     var result = arr.unshift("王宝强");
     console.log(arr); ["王宝强","刘能","赵四","谢广坤","宋小宝","小沈阳"]
     console.log(result); 6
     向第一位添加完新元素以后，后面的元素的索引会被改变
     
     shift方法 删除数组第一位的元素，并返回它
     var result = arr.shift();
     console.log(arr); ["刘能","赵四","谢广坤","宋小宝","小沈阳"]
     console.log(result); "王宝强"
     
     sort方法 对数组中的元素进行排序
     sort排序是按照 unicode编码进行比较 也就是说会将数组中的值转换为字符串在进行比较 例如：
     var arr = ["b","d","t","a",4,3,31,56];
     var result = arr.sort();
     console.log(result); [3, 31, 4, 56, "a", "b", "d", "t"]
```

11. ## 1函数arguments

```js
  数组去重！！！
      var b = [];
             var a = [1,1,3,1,2,5,5,6,8,6,9,8,5];
             for(var i = 0; i < a.length; i++){
                 var flag=true;

                 if(flag){
                     b.push(a[i]);
                 }
             }
             console.log(b);
```

调用函数时，浏览器会传入两个隐藏的参数：
​	1. this
​	2. arguments
function fn(){
​    console.log(arguments);
}
fn();
arguments 是一个类数组对象 它不是数组 但是它也可以通过索引来操作数据，也可以获取长度
arguments instanceof Array   false
arguments 代表函数调用传入的所有实参 
arguments 的length属性就是用来获取实参的长度
这时候就算没有形参 我们也可以使用实参  arguments[0]就是第一个实参

利用argument进行数组去重
function deleterepeat(){
​    var b = [];
​    for (var i = 0; i < arguments.length; i++) {
​        if(b.indexOf(arguments[i]) == -1){
​            b.push(arguments[i]);
​        }
​    }
​    console.log(b);
}
deleterepeat(1,3,2,4,5,9,8,7,6,4,2,5);
```

#          十二 字符串方法

​     

~~~js
 ```javascript
  var str = "http://baidu.com";
             console.log(str.indexOf(":"))
             console.log(str.replace("http","hppt"))
             console.log(str.charAt(5))
             console.log(str.split(":"))
             console.log(str.substring(5,8))
             console.log(str.substr(5,3))
~~~


​     


​    

​```js
     字符串处理
                var str = "https://www.baidu.com/s?wd=sadasdasdas&rsv_spt=1&rsv_iqid=0x90a7a1050001e1c7&issp=1&f=8&rsv_bp=1&rsv_idx=2&ie=utf-8&rqlang=cn&tn=baiduhome_pg&rsv_enter=1&rsv_dl=tb&oq=%25E5%25AD%2597%25E8%25B0%259Csadasdasdas&inputT=768&rsv_t=c658E9CKHnumxQM9j%2BCIJVAbT5njVj3fdwmash6aoWtb1xKLR9glkhYdZtOxIN2s8ncg&rsv_pq=c32234aa0000c137&rsv_sug3=21&rsv_sug1=6&rsv_sug7=000&rsv_sug2=0&rsv_sug4=852&rsv_sug=1";
                 var result = str.indexOf("?") + 1;
                 var obj={};
                 result = str.substring(result);
                 result = result.split("&");
                 for(i=0;i<result.length;i++){
                     // console.log(result[i])
                     var a = result[i].split("=");
                     // console.log(a);
                     obj[a[0]] = a[1];
                 }
                 console.log(obj);
```


​     ```
​     

###       for in

​     

~~~javascript
   枚举对象
 
 // for in
             for(var i in obj){
                 console.log(obj[i]);
             }
 
 # 13.Math
 
 ```javascript
 经常使用的 math'  方法
 	abs 取绝对值
     sqrt  算术平方根
     random 随机数
     PI  圆周率
     max  求几个数字中的最大数
     min  求几个数字的最小数
 	pow  求 x  的  y  次幂 
     floor  往下舍
     ceil  往上入  
     round  四舍五入取整数 
 //   随机颜色
         //    var arr = [0,1,2,3,4,5,6,7,8,9,"a","b","c","d","e","f"];
         //    var color = "#";
         //    for(i=0;i<6;i++){
 
         //        color += arr[Math.floor(Math.random() * 16)];
         //    }
         //    document.body.style.backgroundColor = color;
 ```
 
 # 14 Date
 
 ```    
 方法  
 Date()   返回当前时间和日期
 getDate()   返回某一天
 getDy()   返回一周中的某一天
 getMonth()  返回月份
 getFullYear()  以四位数返回月份
 getHours()  返回小时
 getMinutes() 返回分钟
 getSeconds() 返回秒
 getMillisecond()  返回毫秒
 getTime() 返回1970年1月1日至今的毫秒数
 getUTCDate()  根据世界时间返回某一天
 setDate() 返回某月中的某一天
 ```
 
 # 15 Dom
 
 ```javascript
 Node节点下的属性：
 	innerText   获取元素内容
 	style 获取元素的行内样式  返回值是一个对象  这个对象下面的属性就是css属性  可以直接去给单独的css属性写值
 		node.style.opacity = 1   node.style.marginLeft = '20px' backgroundColor
 		node.style = 'margin-left: 10px;'
 	className 返回元素的类名
~~~

# 十三、DOM    

##      13.1查找节点

```js
// DOM节点的查找属性
Node.parentNode   找他父级节点
Node.children   找所有子级节点    Node.childNodes  高版本浏览器会获取到文本节点  IE中获取的就是Node节点
Node.nextElementSibling  查找下一级兄弟节点   Node.nextSibling  IE的 你懂
Node.previousElementSibling 查找上一级兄弟节点 Node.previousSibling IE的
Node.firstElementChild  查找第一个子级节点 Node.firstChild IE的
Node.lastElementChild 查找最后一个子级节点 Node.lastChild IE的

 获取 类名DOM操作得还有一种方法,不兼容ie 6 7 8 
 
 document.querySelector()
 Document.querySelectorAll()
     function queryselect(){
                 var result = document.querySelectall(".class");
                 if(result.length == 1){
                     result(result[0]);
                 }
                 else{
                     result result;
                 }
       }
   获取元素的区别
       简单的说，query选择符选出来的元素及元素数组是静态的，而getElement这种方法选出的元素是动态的。


```



     Node节点下的方法：
     	setAttribute(); 设置自定义属性 第一个实参代表属性名 第二个实参代表属性值
     	getAttribute();	获取自定义属性 实参就是 属性名

```js
     排他*********************************
     
     
         用来实现 点击后取消另一个点击效果
                 <script>
                 window.onload = function (){
                     var a = document.getElementsByTagName("li");
                     for( i = 0; i < a.length; i++){
                         a[i].onclick = function() {
                             for(j = 0; j < a.length; j++){
                             a[j].style = "";
                              }
                             this.style = "background-color:black;color:white;"
                         }
                     }
                 }
                 </script>
     

```

## 13.2排他的具体实现

```js
         实现 哔哩哔哩 的栏目 周一到周日
     window.onload = function (){
                     var banner = document.getElementById("banner");
                     var a = banner.getElementsByTagName("li");
                     var arr = ['最新','一','二','三','四','五','六','日'];
                     for( i = 0; i < a.length; i++){
                         a[i].onclick = function() {
                             var b = this.getElementsByTagName("span");
                             var c = this.getElementsByTagName("div");
                             for(j = 0; j < a.length; j++){
                             a[j].className = "";
                             a[j].style = "";
                             a[j].getElementsByTagName("div")[0].style = "display:none;"
                             a[j].getElementsByTagName("span")[0].innerText = arr[j];
                              }
                             this.className = "triangle";
                             this.style = "background-color:white;color:#00a1d6;border-bottom: 1px solid #00a1d6;"
                             c[0].style = "display:block";
                             b[0].innerText = '周'+b[0].innerText;
                             a[0].getElementsByTagName("span")[0].innerText = arr[0];
                         }
                     }
                 }
     onmouseover(){
}
 鼠标移入
 onmouseout(){
     
 }
 鼠标移出
```

## 13.3DOM节点下面的事件

```js
onclick   单击事件
onmouseover   鼠标移上事件    触碰到子级也会触发一次
onmouseout    鼠标移出事件    触碰到子级也会触发一次
onmouseenter  鼠标移上事件    解决上述问题
onmouseleave  鼠标移出事件    解决上述问题
onmousedown   鼠标按下事件
onmouseup     鼠标弹起事件
onmousemove   鼠标移动事件
onmousewheel  鼠标滚轮事件    没有滚动条也可以触发
onscroll      鼠标滚轮事件    有滚动条才会触发
onfocus       获取焦点事件
onblur        失去焦点事件
onchange      内容发生改变时触发的事件
onkeydown     键盘按下事件
onkeyup       键盘弹起事件
onkeypress    键盘按下事件
```

## 13.4Dom节点下面的属性


```js
nodeName  返回大写的标签名
nodeType  返回节点类型    1 Element  2 属性  3 text  9 document
nodeValue 返回节点的值   Node节点的nodeValue返回null  文本节点返回文本内容
innerText 可读写节点内容  IE的 不会写进去标签 不会解析标签 只解析内容
innerHTML 可读写节点内容  除IE以外  将标签解析到HTML中 读取的时候会拿到标签
className 可读写类名
id        可读写id名
style     读取的时候会拿到一个对象，这个对象中有每个行内css属性 写的时候会覆盖行内样式
src       可读取src属性值
标签内的属性  都可以用一个方法来替代
Node.setAttribute('属性名', '属性值')   设置自定义属性
Node.getAttribute('属性名')   获取属性值
删除属性  delete 
```

##     13.5表单元素属性

```js
// 表单元素属性
type      可读写input的类型
disabled  true 禁用 false 开启
value     可读写input的内容
placeholder 可读写文本占位符
```



```js
 一般不要使用
 Node.childNodes;    // 查询子节点 会获取到文本节点 不会找子孙
 Node.firstChild;    // 获取该元素的第一个子节点 会获取到文本节点
 Node.lastChild;     // 获取该元素的最后个子节点 会获取到文本节点
 Node.children;  // 查找改元素的子级元素节点 不会去找子孙级元素
 Node.firstElementChild; // 查询第一个子元素节点
 Node.lastElementChild;  // 查询最后一个子元素节点
 Node.parentNode;    // 查询改元素的父级节点
 
 查找兄弟节点
 Node.nextElementSibling;    // 查找后一个兄弟节点
 Node.previousElementSibling;    // 查找前一个兄弟节点
 查找父级节点
 Node.parentNode;   寻找一个元素的父亲节点；
```

##     13.6节点的增加删除替换

   

```js
// DOM的增删改  方法
创造一个标签
document.createElement()
向该元素末尾添加新的元素
Node.appendChild()
向目标元素之前添加一个新元素
Node.insertBefore(新元素, 目标)
删除元素
Node.removeChild(删除目标)
替换元素
Node.replaceChild(新元素, 替换目标)
  // 克隆节点
  cloneNode(布尔值 默认值为false);   // 如果实参为true 将会把该node节点的子孙节点都克隆
```



## 13.7事件委托

```js
###### 将子级的事件委托给父级去做

	优点：

1。解决了动态添加元素无法绑定事件

2。优化性能，将多个事件转换为一个事件

##### 缺点：

3this 指向被破坏， 解决方法为 利用事件对象下的target属性当做this

///////事件委托  运用 target
     			var body = queryselect("tbody");
     			body.onclick = function(events){
     				var tar = events.target;
     				if(tar.children[0] == undefined && tar.nodeName.toLocaleLowerCase() == "td"){
     					var input = document.createElement("input");
     					input.type = "text";
     					input.value = tar.innerText;
     					input.className = "form-control";
     					tar.innerText = "";
     					tar.appendChild(input);
     					input.focus();
     					input.onblur=function(){
     						tar.innerText = this.value;
     					}
     				}
     				else if(tar.className == "btn btn-success"){
     					alert("你已经提交成功，请下次再来");
     				}
     				else if(tar.className == "btn btn-primary"){
     					queryselect("tbody").removeChild(tar.parentNode.parentNode)
     				}else if(tar.className == "btn btn-info"){
     					var clone = queryselect("#clone").cloneNode(true);
     					clone.id ='';
     					queryselect("tbody").insertBefore(clone,tar.parentNode.parentNode);
     				}
     			}
```

## 13.8函数节流


```javascript

     轮播图   
   
     函数节流  可以用来控制定时器之内 不能在进行点击 定时器运行完了之后才可以进行 点击函数

     响应函数  onclick() 
     		focus()
     		onblur()
     		onmouseover()鼠标移上 受子集影响
     		onmouseout()鼠标移出  受子集影响
     		onmouseleave()鼠标离开   不会受自己影响
     		onmouseenter()鼠标进入   不会受自己影响
           
       ul.onmouseenter=function(){
     			clearInterval(time1);
     		}
     		ul.onmouseleave =function(){
     			autoChange();
     		}
键盘的事件
```

## 13.9事件对象

```js
所有的事件处理函数中，都有一个参数event，这个event就是事件对象
事件对象获取兼容：形参event 可以直接获取  google   window.event IE
常用的事件对象下的属性有：
	target    触发事件的元素
    srcElement IE中的target
    wheelDelta 判断滚轮向下滚还是向上滚  IE google
    deltaY 判断滚轮向下滚还是向上滚 google
    detail 判断滚轮向下滚还是向上滚  firefox
    clientX  当前鼠标距离浏览器最左边的距离
    clientY  当前鼠标距离浏览器最上边的距离
    offsetX  获取当前鼠标距离事件源左边的距离
    offsetY  获取当前鼠标距离事件源上边的距离
    pageX    获取当前鼠标距离浏览器左部的距离（包括被卷曲的距离）
    pageY    获取当前鼠标距离浏览器顶部的距离（包括被卷曲的距离）
    screenX  获取当前鼠标距离屏幕左侧的距离
    screenY  获取当前鼠标距离屏幕顶部的距离
```



## 13.10时间传播机制

```
1. 捕获阶段
2. 目标阶段
3. 冒泡阶段
事件触发默认是在冒泡阶段触发
新的绑定事件的方法是 addEventListener('事件名', '匿名函数', booolean) true 代表 捕获阶段触发 默认 false
addEventListener 不会覆盖事件  会叠加
```



## 13.11添加滚轮事件监听事件

addEventListener 添加事件监听  

有利的地方	,1    不与原来相同的节点冲突  事件 可以绑定多个对象

2. 可以阻止事件捕获和冒泡

onmousewheel  鼠标滚动事件

阻止浏览器事件冒泡 preventDefault();

阻止自身事件冒泡	stoppropagation

可能值：

- true - 事件句柄在捕获阶段执行
- false- 默认。事件句柄在冒泡阶段执行

滚轮事件对象的 哦。判断事件滚轮方向 

detail   火狐浏览器的

deltaY  谷歌浏览器

wheelDelta   ie浏览器的兼容  取消浏览器冒泡  cancelbubble;

```js
if(document.addEventListener){
			wheel.addEventListener('DOMMouseScroll',function(e){
				var e = e || window.events;
				var direcition = e.detail > 0 ? 'left' : 'right';
				move(direcition);
				e.preventDefault();
			},false);
}
ie浏览器给window 添加一个 class属性
if (!document.getElementsByClassName) {
			document.getElementsByClassName = function (className, element) {
				var children = (element || document).getElementsByTagName('*');
				var elements = new Array();
				for (var i = 0; i < children.length; i++) {
					var child = children[i];
					var classNames = child.className.split(' ');
					for (var j = 0; j < classNames.length; j++) {
						if (classNames[j] == className) {
							elements.push(child);
							break;
						}
					}
				}
			return elements;
			};
		}
		
```

## 13.12键盘事件

```
1）keypress 对中文输入法支持不好，无法响应中文输入
2）keypress 无法响应系统功能键（如delete，backspace）   只有按下字符键盘才会触发
3）由于前面两个限制，keydown和keyup对keyCode不敏感

首先会触发keydown事件
然后就触发keyup事件
如果用户按下了一个非字符键不放，就会重复触发keydown事件，直到用户松开该键为止

如果用户按下键盘上的字符键时，顺序为keydown -> keypress ->keyup。keydown、
如果用户按下非字符键时，首先触发keydown,然后触发keyup事件。
在keyup事件中无法阻止浏览器默认事件，因为在keypress时，浏览器默认行为已经完成，即将文字输入文本框（尽管这时还没显示），这个时候不管是preventDefault还是returnValue = false，都不能阻止在文本框中输入文字的行为，如要阻止默认行为，必须在keydown或keypress时阻止。
```



## 13.13 DOMMouseScroll  火狐浏览器鼠标滚轮时间

火狐绑定事件

1.    document.addEventListener('DOMMouseScroll',scrollFunc,false); 

2. ```javascript
    wheel.onmousewheel = function(e){
      			var e = e || window.events;
      			var direcition = e.deltaY > 0 ? 'left' : 'right';
      			move(direcition);
      			return false;
      	}
       function move(direcition){
           if(direcition == 'left'){
               left = left + 20;
           }else{
               left = left - 20;
           }
           left = left < 0 ? 0 : left;
           left = left > (linewidth - slidewidth) ? (linewidth - slidewidth) : left;
           slide.style.left = left + 'px';
           ul.style.left = -parseInt(slide.style.left)/(linewidth - slidewidth) * ulleft + 'px';
      
      		}
    ```
   ```

   ## 13.14 定时器
   
   ```
   setInterval(function(){}, time)  每隔多少毫秒执行一次匿名函数
   clearInterval()
   setTimeout(function(){}, time)   多少毫秒之后执行一次匿名函数
   clearTimeout()
   ```
   
   ## 13.15函数防抖
   
   ```
   规定一个单位时间，在这个单位时间内，只能有一次触发事件的回调函数执行，如果在同一个单位时间内某事件被触发多次，只有一次能生效。
   ```
   
   

# 十四，正则表达式

     ```javascript
     (?=.*[a-z]).{5,} 会找出最少有一个字母而且5位数以上
     
     表达式写法
        var  reg = new RegExp("[a-z]",i);
        reg.test(str)
    字面量写法
    	var reg = /[a-z]/i;
    
    修饰符
    i  执行对大小写不敏感
    g   执行全局匹配
    m  执行多行匹配
    
    表达式
    [abc]  表示方括号内的任何字符
    [0-9]   查找任何0-9的数字
    [A-z]   查找大写A到小写z的字符
    [^adgk] 查找给定集合外的任何字符


    
    量词
    
    +  匹配任何至少含有一个n的字符串
    
    * 匹配任何包含0或多个的字符串
      ？  破配包含0个或一个的字符串
      {x}   包含x个n的序列的字符串
      {x,y}  包含x到y个序列的字符串
    
      n{x,}  	匹配包含至少X个n的序列的字符串
      ^  匹配以任何开头为n的字符串
      $  匹配以任何结尾的字符串
      ？=n  匹配紧随其后指定n的字符串
      ?!n   匹配任何后没有紧随字符串n的字符串


    
    
    元字符  指的是拥有特殊含义的字符
    
    .        除了换行符以外任意字符
    \w       字母、数字、下划线
    \W       非字母、数字、下划线
    \d       数字
    \D       非数字
    \s       空格
    \S       非空格
    [\u4e00-\u9fa5] 所有中文


    [u4e00-u9fa5]   中文字符
    
    数字：^[0-9]*$
    n位的数字：^d{n}$
    至少n位的数字：^d{n,}$
    m-n位的数字：^d{m,n}$
    零和非零开头的数字：^(0|[1-9][0-9]*)$
    非零开头的最多带两位小数的数字：^([1-9][0-9]*)+(.[0-9]{1,2})?$
    带1-2位小数的正数或负数：^(-)?d+(.d{1,2})?$
    正数、负数、和小数：^(-|+)?d+(.d+)?$
    有两位小数的正实数：^[0-9]+(.[0-9]{2})?$
    有1~3位小数的正实数：^[0-9]+(.[0-9]{1,3})?$
    非零的正整数：^[1-9]d*$ 或 ^([1-9][0-9]*){1,3}$ 或 ^+?[1-9][0-9]*$
    非零的负整数：^-[1-9][]0-9″*$ 或 ^-[1-9]d*$
    非负整数：^d+$ 或 ^[1-9]d*|0$
    非正整数：^-[1-9]d*|0$ 或 ^((-d+)|(0+))$
    非负浮点数：^d+(.d+)?$ 或 ^[1-9]d*.d*|0.d*[1-9]d*|0?.0+|0$
    非正浮点数：^((-d+(.d+)?)|(0+(.0+)?))$ 或 ^(-([1-9]d*.d*|0.d*[1-9]d*))|0?.0+|0$
    正浮点数：^[1-9]d*.d*|0.d*[1-9]d*$ 或 ^(([0-9]+.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*.[0-9]+)|([0-9]*[1-9][0-9]*))$
    负浮点数：^-([1-9]d*.d*|0.d*[1-9]d*)$ 或 ^(-(([0-9]+.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*.[0-9]+)|([0-9]*[1-9][0-9]*)))$
    浮点数：^(-?d+)(.d+)?$ 或 ^-?([1-9]d*.d*|0.d*[1-9]d*|0?.0+|0)$


    
      汉字：^[一-龥]{0,}$
        英文和数字：^[A-Za-z0-9]+$ 或 ^[A-Za-z0-9]{4,40}$
        长度为3-20的所有字符：^.{3,20}$
        由26个英文字母组成的字符串：^[A-Za-z]+$
        由26个大写英文字母组成的字符串：^[A-Z]+$
        由26个小写英文字母组成的字符串：^[a-z]+$
        由数字和26个英文字母组成的字符串：^[A-Za-z0-9]+$
        由数字、26个英文字母或者下划线组成的字符串：^w+$ 或 ^w{3,20}$
        中文、英文、数字包括下划线：^[一-龥A-Za-z0-9_]+$
        中文、英文、数字但不包括下划线等符号：^[一-龥A-Za-z0-9]+$ 或 ^[一-龥A-Za-z0-9]{2,20}$
        可以输入含有^%&’,;=?$”等字符：[^%&',;=?$"]+
        禁止输入含有~的字符：[^~"]+
    
        Email地址：^w+([-+.]w+)*@w+([-.]w+)*.w+([-.]w+)*$
        域名：[a-zA-Z0-9][-a-zA-Z0-9]{0,62}(/.[a-zA-Z0-9][-a-zA-Z0-9]{0,62})+/.?
        InternetURL：[a-zA-z]+://[^s]* 或 ^http://([w-]+.)+[w-]+(/[w-./?%&=]*)?$
        手机号码：^(13[0-9]|14[5|7]|15[0|1|2|3|5|6|7|8|9]|18[0|1|2|3|5|6|7|8|9])d{8}$
        电话号码(“XXX-XXXXXXX”、”XXXX-XXXXXXXX”、”XXX-XXXXXXX”、”XXX-XXXXXXXX”、”XXXXXXX”和”XXXXXXXX)：^($$d{3,4}-)|d{3.4}-)?d{7,8}$
        国内电话号码(0511-4405222、021-87888822)：d{3}-d{8}|d{4}-d{7}
        身份证号(15位、18位数字)：^d{15}|d{18}$
        短身份证号码(数字、字母x结尾)：^([0-9]){7,18}(x|X)?$ 或 ^d{8,18}|[0-9x]{8,18}|[0-9X]{8,18}?$
        帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：^[a-zA-Z][a-zA-Z0-9_]{4,15}$
        密码(以字母开头，长度在6~18之间，只能包含字母、数字和下划线)：^[a-zA-Z]w{5,17}$
        强密码(必须包含大小写字母和数字的组合，不能使用特殊字符，长度在8-10之间)：^(?=.*d)(?=.*[a-z])(?=.*[A-Z]).{8,10}$
        日期格式：^d{4}-d{1,2}-d{1,2}
        一年的12个月(01～09和1～12)：^(0?[1-9]|1[0-2])$
        一个月的31天(01～09和1～31)：^((0?[1-9])|((1|2)[0-9])|30|31)$
        钱的输入格式：
        有四种钱的表示形式我们可以接受:”10000.00″ 和 “10,000.00″, 和没有 “分” 的 “10000″ 和 “10,000″：^[1-9][0-9]*$
        这表示任意一个不以0开头的数字，但是，这也意味着一个字符”0″不通过，所以我们采用下面的形式：^(0|[1-9][0-9]*)$
        一个0或者一个不以0开头的数字.我们还可以允许开头有一个负号：^(0|-?[1-9][0-9]*)$
        这表示一个0或者一个可能为负的开头不为0的数字.让用户以0开头好了.把负号的也去掉，因为钱总不能是负的吧.下面我们要加的是说明可能的小数部分：^[0-9]+(.[0-9]+)?$
        必须说明的是，小数点后面至少应该有1位数，所以”10.”是不通过的，但是 “10″ 和 “10.2″ 是通过的：^[0-9]+(.[0-9]{2})?$
        这样我们规定小数点后面必须有两位，如果你认为太苛刻了，可以这样：^[0-9]+(.[0-9]{1,2})?$
        这样就允许用户只写一位小数。下面我们该考虑数字中的逗号了，我们可以这样：^[0-9]{1,3}(,[0-9]{3})*(.[0-9]{1,2})?$
        1到3个数字，后面跟着任意个 逗号+3个数字，逗号成为可选，而不是必须：^([0-9]+|[0-9]{1,3}(,[0-9]{3})*)(.[0-9]{1,2})?$
        备注：这就是最终结果了，别忘了”+”可以用”*”替代。如果你觉得空字符串也可以接受的话(奇怪，为什么?)最后，别忘了在用函数时去掉去掉那个反斜杠，一般的错误都在这里
        xml文件：^([a-zA-Z]+-?)+[a-zA-Z0-9]+.[x|X][m|M][l|L]$
        中文字符的正则表达式：[一-龥]
        双字节字符：[^-ÿ] (包括汉字在内，可以用来计算字符串的长度(一个双字节字符长度计2，ASCII字符计1))
        空白行的正则表达式：s* (可以用来删除空白行)
        HTML标记的正则表达式：<(S*?)[^>]*>.*?</>|<.*? /> (网上流传的版本太糟糕，上面这个也仅仅能部分，对于复杂的嵌套标记依旧无能为力)
        首尾空白字符的正则表达式：^s*|s*$或(^s*)|(s*$) (可以用来删除行首行尾的空白字符(包括空格、制表符、换页符等等)，非常有用的表达式)
        腾讯QQ号：[1-9][0-9]{4,} (腾讯QQ号从10000开始)
        中国邮政编码：[1-9]d{5}(?!d) (中国邮政编码为6位数字)
        IP地址：d+.d+.d+.d+ (提取IP地址时有用)
        IP地址：((?:(?:25[0-5]|2[0-4]d|[01]?d?d).){3}(?:25[0-5]|2[0-4]d|[01]?d?d)) (由@飞龙三少 提供，感谢共享)




# 十五，Math对象和Date对象



   ```
Date对象来表示一个时间
要用一个对象 就要new 一个实例出来
var d = new Date();
console.log(d); Wed Sep 04 2019 22:06:48 GMT+0800 (中国标准时间)
这要就能获取当前对应的时间

创建一个指定的时间对象
var d1 = new Date("11/06/2019 11:30:10");
console.log(d1);
日期的格式 月份/日/年 时:分:秒

下来就是看Date对象下的方法
getDate() 返回一个月中的某一天 1-31
getDay() 返回一周中的某一天 0-6
getMonth() 返回月份 0-11
getFullYear() 以四位数返回年份
getHours() 返回Date对象的小时
getMinutes() 返回Date对象的分钟
getSeconds() 返回Date对象的秒
getTime() 返回1970年1月1日至今的毫秒数
getUTCDate() 根据世界时间返回对象月中的某一天
setDate() 设置月中的某一天
setTime() 以毫秒设置Date()

```

```
我们的Math不需要创建实例 Math直接就是一个对象 它里面封装了一些数学运算相关的属性和方法
console.log(Math.PI); 3.1415926

math.abs(x)  返回数的绝对值
math.ceil(x) 对数进行上舍入
math.floor(x) 对数进行下舍入
math.max(x,y) 返回下x,y中的最高值
math.pow(x,y) 返回x的y次幂
math.random() 返回0到1的随机数
math.round() 四舍五入为最接近的整数
```



# 十六，BOM

## 16.1 三大家族

```
offset  client  scroll
offsetWidth      获取元素宽度（自身宽度 + 内填充 + 边框）
offsetHeight     获取元素高度（自身高度 + 内填充 + 边框）
offsetLeft       获取元素距离上一级定位元素的左边距
offsetTop        获取元素距离上一级定位元素的上边距
offsetParent     获取上一级定位元素

clientWidth      获取元素宽度（自身宽度 + 内填充）
clientHeight     获取元素高度（自身高度 + 内填充）

scrollWidth      获取元素的宽度（自身宽度 + 内填充 + 溢出范围）
scrollHeight     获取元素的宽度（自身高度 + 内填充 + 溢出范围）
scrollLeft       获取页面x轴被卷曲的距离
scrollTop        获取页面y轴被卷曲的距离
document.body.scrollTop || document.documentElement.scrollTop

### 三大家族

document.documentElement  document.body  获取 html  和 body 

返回值为  number   node节点下面的属性

###### offsetwidth  返回元素的宽度    包括元素宽度、内边距和边框，不包括外边距 

###### clientwidth   返回元素的宽度（包括元素宽度、内边距，不包括边框和外边距） 

###### scrollwidth  返回元素的宽度（包括元素宽度、内边距和溢出尺寸，不包括边框和外边距），无溢出的情况，与clientWidth相同 

###### offsetleft  返回元素的上左缘距离最近采用定位父元素内壁的距离，如果父元素中没有采用定位的，则是获取左外边缘距离文档内壁的距离 

###### scrollLeft    //此属性可以获取或者设置对象的最左边到对象在当前窗口显示的范围内的左边的距离，也就是元素被滚动条向左拉动的距离

###### scrollTop  //此属性可以获取或者设置对象的最顶部到对象在当前窗口显示的范围内的顶边的距离，也就是元素滚动条被向下拉动的距离。

###### clientX     鼠标相对于浏览器（这里说的是浏览器的有效区域）左上角x轴的坐标；  不随滚动条滚动而改变；

###### clientY     鼠标相对于浏览器（这里说的是浏览器的有效区域）左上角y轴的坐标； 不随滚动条滚动而改变；

###### pageX     鼠标相对于浏览器（这里说的是浏览器的有效区域）左上角x轴的坐标；  随滚动条滚动而改变；

###### pageY     鼠标相对于浏览器（这里说的是浏览器的有效区域）左上角y轴的坐标；  随滚动条滚动而改变；

###### screenX   鼠标相对于显示器屏幕左上角x轴的坐标； 

###### screenY    鼠标相对于显示器屏幕左上角y轴的坐标； 

###### offsetX     鼠标相对于事件源左上角X轴的坐标

###### offsetY     鼠标相对于事件源左上角Y轴的坐标

###### window.onscroll  鼠标滚动时候执行事件
```

##      16.2 window对象

```
window.onload=function(){
}  该方法用于在网页加载完毕后立刻执行的操作，即当html加载完毕后，立刻执行某个方法等。
但，以上方式也仅仅适用于绑定的函数不是很多的场合
四、window.onload()方法的衍生:
不管你打算在页面加载完毕时执行多少个函数，一百个一千个等，它都可以应付自如，使用一个函数addLoadEvent，它是由Simon Willison(详见 http://simon.incutio.com)编写的，它只有一个参数---需要执行的函数名。

alert为系统提示框
confirm为确认框
prompt为系统输入框

获取窗口大小
window.innnerHeight   获取窗口的高度
window.innerWidth  获取窗口的宽度

getComputedStyle 获取css属性值  标准浏览器，ie9+以上支持 getComputedStyle。
IE 下 currentStyle 获取css 属性值    只在 IE 下支持（网上 opera 也支持，但未测）。
```

## 16.3location对象

```
它提供了与当前窗口中加载的文档有关的信息，还提供了一些导航功能

hash 返回URL中的hash（#号后跟零或多个字符），如果URL中不包含散列，则返回空字符串,例"#contents"

host 返回服务器名称和端口号(如果有).例"www.zhaosywz.com:80"

hostname 返回不带端口号的服务器名称.例"www.zhaosywz.com"

href 返回当前页面的完整url.例"www.zhaosywz.com/index.html"

pathname 返回url中的目录或文件名,例"/category/shoes"

port 返回url的端口号,如果没有则返回空字符串.例"8080"

protocol 返回页面使用的协议。通常是http:或https:

search 返回URL的查询字符串。这个字符串以问号开头,'?id=100'

通过reload()可以重新加载当前页面
```

## 16.4navigator对象

```
appCodeName 浏览器的名称。通常都是Mozilla，即使在非Mozilla浏览器中也是如此

appName 完整的浏览器名称

appVersion 浏览器版本，一般不与实际的浏览器版本对应.

cookieEnabled 表示cookie是否启用

javaEnabled() 表示单签浏览器是否启用Java

onLine 表示浏览器是否连接到了因特网

mimeTypes 在浏览器中注册的MIME类型数组

platform 浏览器的系统平台

plugins 浏览器中安装的插件信息的数组

userAgent 浏览器用户代理字符串
userAgent是最常用的属性.
```

## 16.5history对象

```
//后退一页
history.go(-1);

//前进一页
history.go(1);

//前进两页
history.go(2);

//跳转到最近的包含'wrox.com'字符的页面
history.go("wrox.com");

//后退一页
history.back();
//前进一页
history.forward();

```

# 十七,jquery

```
获取元素 直接写选择器

$('.name > ul >li')    
$("*")  通配符选择器
$('~')  兄弟元素选择器 选区之后
$(":header") 获取网页中所有的h1,h2,h3;
$("div: animated")  选区正在执行动画的div

获取CSS

CSS 样式 >>> $("#id").css('backgroundColor', 'blue');
CSS 样式 >>> .css(
{'color':'red', 
'width':'300px'}
);
innerText >>> .text('改变的文本内容');
innerHTML >>> .html();
高度 >>> .height();
宽度 >>> .width();
value >>> .val('改变的 value 值');
获取属性值 >>> .attr(‘name');
设置 name 属性 >>> .attr('name', 'value');
设置 name 属性 >>> .attr({'title':'TTT', 'name':'zzz'});
删除属性 >>> .removeAttr();
追加一个类 >>> .addClass('cls');
移除多个类 >>> .removeClass('cls1, cls2');

DOm操作

创建节点 >>> var $li = $("<li>苹果</li>");
删除节点 >>> .remove()
删除子节点 >>> .empty();
复制节点 >>> .clone();
复制元素所绑定的事件 >>> .clone(true);  可以克隆事件
将元素替换为指定的对象 >>> .replaceWith("<a href=’#'>Test</a>");
替换所有匹配元素 >>> .replaceAll("p");
把所有匹配的元素用其他元素的结构化标记包裹起来 >>> .wrap("<b></b>");
将所有匹配的元素用单个元素包裹起来 >>> .wrapAll("p");
判断是否应用了 cls 类 >>> .hasClass("cls");
隐藏 / 显示该元素 >>> .toggle();
切换这个 cls 类 >>> .toggleClass(‘cls’);
筛选元素 >>> .filter();
向每个匹配元素追加内容 >>> .append();
把所有匹配元素追加到另一个指定的元素元素集合中 >>> .appendTo();
在被选元素的开头插入指定内容 >>> .prepend(); $("p").prepend("<b>love</b>");
在被选元素的开头插入指定内容 >>> .prependTo(); $("<b>love</b>").prependTo("p");
再次元素之后添加元素 >>> .after();
将此元素添加到（参数）的后面 >>> .insertAfter();
在每个匹配的元素之前添加元素 >>> .before();
将此元素添加到（参数）的前面 >>> .insertBefore();
取得元素的子元素集合 >>> .children();
判断 >>> .is(':visible')

动画

隐藏元素 >>> .hide(3000);
显示元素 >>> .show();
淡入 >>> .fadeIn();
淡出 >>> .fadeOut();
淡入淡出切换 >>> .fadeToggle()
达到透明度多少 >>> .fadeTo(2000, 0.3);
向上收缩隐藏 >>> .slideUp();
向下收缩显示 >>> .slideDown();
显示隐藏切换 >>> .slideToggle();

获取兄弟元素
查找最近的 <li> 元素 >>> .closest('li');
获取当前元素的所有 <span> 元素 >>> .find("span");
返回上一层操作的对象 >>> .end();
为每个匹配元素的特定事件绑定事件处理函数。  bind()

数组遍历   $(selector).each(function(index,element))
停止动画  jQuery stop() 方法用于在动画或效果完成前对它们进行停止。
eq()    获取当前链式操作中第N个jQuery对象，返回jQuery对象，当参数大于等于0时为正向选取，比如0代表第一个，1代表第二个。当参数为负数时为反向选取，比如-1为倒数第一个，具体可以看以下示例。

```

# 十八 ES6

## 18.1新增的三个数组遍历方法

```
arr.forEach(function(item,index){
​	
})
他总是返回underfined

arr.map(function(item,index){
​	return  
})
可以修改或者增加原有数组，并且返回数组,不改变原有数组

arr.filter(function(item,index){
​	return item>3
})
可以用来筛选过滤出数组,并且将其返回不改变原有数组

```

## 18.2let 和 const 命令

```
1. 没有变量提升
2. 不能重复声明变量
3. 块级作用域

const
4. 声明的常量不能被修改
```

## 18.3变量的解构赋值

```
ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构

数组（字符串）的解构赋值  [] = Array
对象的解构赋值  {key: 自定义名字} = Object 
函数形参的解构赋值

let arr = [1, 2, 3];
let [a, b, c] = arr;

let obj = {name: 1};
let {name: n} = obj;

4.圆括号问题
以下三种解构赋值不得使用圆括号。
（1）变量声明语句
（2）函数参数
（3）赋值语句的模式

可以使用圆括号的情况
赋值语句的非模式部分，可以使用圆括号。

5.变量的解构赋值用途很多。
（1）交换变量的值
（2）从函数返回多个值
（3）函数参数的定义
（4）提取 JSON 数据
（5）函数参数的默认值
（6）遍历 Map 结构
（7）输入模块的指定方法
```

## 18.4 字符串的扩展和新增方法

```
模板字符串中拼接变量 使用 ${}

let str = 'china';
let str1 = 'No.1';

console.log('say${str}${str1}'); --> saychinaNo.1

```

## 18.5 number 扩展

```
Number.isFinite()用来检查一个数值是否为有限的（finite），即不是Infinity。
如果参数类型不是数值，Number.isFinite一律返回false。
Number.isNaN()用来检查一个值是否为NaN。
Number.isInteger()用来判断一个数值是否为整数。
```

## 18.6函数的扩展

```
1.name 属性 返回函数的函数名
2.函数形参的默认值
3.rest参数 剩余的实参
4.箭头函数  this的指向发生改变  this指向定义的作用域中的this
匿名函数可以改写为 箭头函数

let fn = () => {
​    console.log(this);
}

形参只有一个的时候 可以省略掉小括号
返回语句只有一条的时候 可以省略掉代码块

*******箭头函数有几个使用注意点
（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。

（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。

（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

（4）不可以使用yield命令，因此箭头函数不能用作 Generator 函数。
```

## 18.7数组的扩展

```
扩展运算符（...） 将一个数组转为用逗号分隔的参数序列。
由于扩展运算符可以展开数组，所以不再需要apply方法，将数组转为函数的参数

扩展运算符 ...
​	展开数组、伪数组
​	
扩展运算符的应用
（1）复制数组
 (2)合并数组  浅拷贝
(3)扩展运算符还可以将字符串转为真正的数组。
[...'hello']
(4) 实现了 Iterator 接口的对象
任何定义了遍历器（Iterator）接口的对象（参阅 Iterator 一章），都可以用扩展运算符转为***真正的数组。
(5)Map 和 Set 结构，Generator 函数



Array.from()  
将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）。
下面是一个类似数组的对象，Array.from将它转为真正的数组。


Array.of()  Array.of方法用于将一组值，转换为数组。


数组去重
let a = (...value) => {let b = new Set([...value]);console.log([...b])}
​	let c = a(1,2,3,4,5,6,7,8,9,10,1,2,2,2,3);
```

## 18.8对象的扩展

```
属性的可枚举性和遍历
​    Object.getOwnPropertyDescriptor方法可以获取该属性的描述对象
​    value: 123,
​    writable: true,
​    enumerable: true,
​    configurable: true
描述对象的enumerable属性，称为“可枚举性”，如果该属性为false，就表示某些操作会忽略当前属性。
遍历对象的五种方法
（1）for...in
（2）Object.keys(obj)
（3）Object.getOwnPropertyNames(obj)
（4）Object.getOwnPropertySymbols(obj)
（5）Reflect.ownKeys(obj)


super关键字
我们知道，this关键字总是指向函数所在的当前对象，ES6 又新增了另一个类似的关键字super，指向当前对象的原型对象。

Object.is()  比较两个值是否相等  不同之处只有两个：一是+0不等于-0，二是NaN等于自身。

Object.assign() Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。
Object.assign(target, source1, source2);
（1）浅拷贝
（2）同名属性的替换
（3）数组的处理
（4）取值函数的处理

Object.getOwnPropertyDescriptors() 会返回某个对象属性的描述对象

Object.keys()，Object.values()，Object.entries()

Object.fromEntries()方法是Object.entries()的逆操作，用于将一个键值对数组转为对象。
```

## 18.9 symbol函数

```
比如，你使用了一个他人提供的对象，但又想为这个对象添加新的方法（mixin 模式），新方法的名字就有可能与现有方法产生冲突。如果有一种机制，保证每个属性的名字都是独一无二的就好了，这样就从根本上防止属性名的冲突。这就是 ES6 引入Symbol的原因。 是 Javascript的第七种语言

2.Symbol 值通过Symbol函数生成
凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。
不能用 new 关键字生成

const sym = Symbol(描述);
sym.description 获取symbol的描述字符串

3.作为属性名的symbol
// 第一种写法
let a = {};
a[mySymbol] = 'Hello!';
// 第二种写法
let a = {
[mySymbol]: 'Hello!'
};
// 第三种写法
let a = {};
Object.defineProperty(a, mySymbol, { value: 'Hello!' });

4.写一个symbol

    const PROP_NAME = Symbol()
    const PROP_AGE = Symbol()
    
    let obj = {
      [PROP_NAME]: "一斤代码"
    }
    obj[PROP_AGE] = 18
    
    obj[PROP_NAME] // '一斤代码'
    obj[PROP_AGE] // 18

######属性名的遍历
有一个Object.getOwnPropertySymbols()方法，可以获取指定对象的所有 Symbol 属性名。该方法返回一个数组，成员是当前对象的所有用作属性名的 Symbol 值。

另一个新的 API，Reflect.ownKeys()方法可以返回所有类型的键名，包括常规键名和 Symbol 键名。
由于以 Symbol 值作为键名，不会被常规方法遍历得到。我们可以利用这个特性，为对象定义一些非私有的、但又希望只用于内部的方法。
```

## 18.10 set和map数据结构

```
ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

Set本身是一个构造函数，用来生成 Set 数据结构。
const s = new Set();

可以用来数组去重
var a = [1,2,2,3,4,5,6,7,8,9,8,7,8];
​	var arr = new Set(a);
***Array.from方法可以将 Set 结构转为数组。

向 Set 加入值的时候，不会发生类型转换
let set = new Set();
let a = NaN;
let b = NaN;
set.add(a);
set.add(b);
上面代码向 Set 实例添加了两次NaN，但是只会加入一个


Map容器

JavaScript 的对象（Object），本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键。这给它的使用带来了很大的限制。
ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。

let map = new Map([[key, value], [key, value]]);
map.set(key, value);  向map容器中加入新的键值对
map.get(key);  读取map容器中key的value
map.has(key);  检查map容器中是否含有这个键值对
map.delete(key); 删除map容器中的键值对
map.clear();  清空map容器
```

## 18.11Proxy

Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”。

```
Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。
ES6 原生提供 Proxy 构造函数，用来生成 Proxy 实例。
var proxy = new Proxy(target, handler);

let obj = {
​	name: 'yj666',
​	age: 22
}
let pro = new Proxy(obj, {
​	set(target, key, value){
​		console.log(`监听到改变属性${key}的值为${value}`);
​		Reflect.set(target, key, value);
​	},
​	get(target, key){
​		console.log(`监听到获取属性${key}`);
​		return Reflect.get(target, key);
​	}
})
console.log(pro);
pro.name = 'lzx';

console.log(obj.name);

Reflect.set(target, key, value); 给目标对象添加属性和值
Reflect.get(target, key); 获取目标对象的属性值
```

## 18.12Reflect

```
Reflect对象与Proxy对象一样，也是 ES6 为了操作对象而提供的新 API。Reflect对象的设计目的有这样几个
（1） 将Object对象的一些明显属于语言内部的方法放到Reflect对象上
（2） 修改某些Object方法的返回结果，让其变得更合理
(3)让Object操作都变成函数行为。
（4）Reflect对象的方法与Proxy对象的方法一一对应，



静态方法
```

## 18.13Promise 对象

```
Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。
所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

Promise对象有以下两个特点。
（1）对象的状态不受外界影响。 pending（进行中）、fulfilled（已成功）和rejected（已失败）
（2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。pending变为fulfilled和从pending变为rejected。
（3）.promise构造函数是同步执行的，then方法是异步执行的


 例子
 var lock = false;
​	var promise = new Promise((resolove,reject) =>{
​		if(lock){
​			resolove();
​		}else{
​			reject();
​		}

```js
})
promise.then(() => {
	console.log('成功')
}, ()=>{
	console.log('失败')
})
```

3.Promise.prototype.then()  链式操作
4.Promise.prototype.catch()

Promise的all方法提供了并行执行异步操作的能力，并且在所有异步操作执行完后才执行回调。

race的用法
```

## 18.14 Iterator 和 for...of 循环

```
Iterator 的作用有三个：一是为各种数据结构，提供一个统一的、简便的访问接口；二是使得数据结构的成员能够按某种次序排列；三是 ES6 创造了一种新的遍历命令for...of循环，Iterator 接口主要供for...of消费。

一种数据结构只要部署了 Iterator 接口，我们就称这种数据结构是“可遍历的”

原生具备 Iterator 接口的数据结构如下。
Array
Map
Set
String
TypedArray
函数的 arguments 对象
NodeList 对象

一个数据结构只要部署了Symbol.iterator属性，就被视为具有 iterator 接口，就可以用for...of循环遍历它的成员。也就是说，for...of循环内部调用的是数据结构的Symbol.iterator方法。

function iterator(...values){
​	let index = 0;
​	return {
​		next(){
​			return {value: values[index++],done: index > values.length ? true : false}
​		}
​	}
}
let iter = iterator('赵四', '刘能', '广坤', '李泽欣', '超星空', '巧碧螺');
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());


let arr = ['赵四', '刘能', '广坤', '李泽欣', '超星空', '巧碧螺'];
for(let i of arr){
​	console.log(i);
}
// 给对象添加iterator接口
let obj = {
​	name: 1,
​	age: 22,
​	[Symbol.iterator]: function(){
​		let index = 0;
​		let arr = Object.keys(this);
​		return {
​			next: () => {
​				return {value: this[arr[index++]],done: index > arr.length ? true : false};
​			}
​		}
​	}
}
for(let i of obj){
​	console.log(i);
}
```js

## 18.15  Class 类

Class 类 就是 构造函数的另外一种写法

可以解决构造函数继承的问题

继承用到的是 extends 关键字以及super函数

class Person {
    constructor(name, age){
        this.name = name;
        this.age = age;
        this.hi = function(){
            console.log(1);
        }
    }
    sayHi(){ // 写在原型对象上的方法
        console.log(this.name);
    }
}
let p = new Person('yj', 22);
console.log(p);
p.sayHi();
			// 继承 Person 类
class Son extends Person {
    constructor(name, age, gender){
        super(name, age); // 调用Person类的constructor
        this.gender = gender;
    }
    sayHi(){ // 给子类原型对象添加一个方法
        console.log(this.age);
    }
}
let p1 = new Son('a', 22,'xxx');
console.log(p1);
p1.sayHi();
```

## 18.16. Generator 函数

Generator 函数是一个状态机，封装了多个内部状态。

执行Generator函数是会返回一个遍历器对象，通过调用遍历器对象下的next方法来去改变函数内部的状态，

函数内部的yield语句执行完毕以后再去调用next方法就会一直返回{value: undefined, done: true}

Generator 函数就是一个普通函数，不同的是 函数 与 函数名之间加了一个 * 号，普通函数只会 被调用  或者 定义，generator函数可以暂停。

```javascript
function* cxk(){
    let a = yield 'A';
    console.log(`a:${a}`);
    let b = yield 'B';
    console.log(`b:${b}`);
    let c = yield 'C';
    console.log(`c:${c}`);
}
let iter = cxk();
iter.next();  --> {value: yield后的表达式的返回值,done: false}

//////*********************长轮询
	function* long(){
		yield new Promise((resolve,reject)=>{
			setTimeout(()=>{
				resolve({status: 0});
			},1000)
		})
	}
	// let str = long();
	// let b = str.next().value;
	function request(){
		let str = long();
		let b = str.next().value;
		b.then((data)=>{
			console.log(data);
			if(data.status != 1){
				request();
				// setTimeout(()=>{
				// 	resolve({status: 0});
				// },1000)
			}
		}).catch((error)=>{
			console.log(error);
		})
	}
	request();
```

## 18.17. async 函数 ES2017

Generator的语法糖

await 关键字的作用 暂停当前async函数等待 表达式的返回结果 拿到表达式的返回结果后 接着执行async函数 如何再一次遇到await 就会进行上一次的操作

```javascript
function getJson(url){
	return new Promise((resolve, reject) => {
		let xhr = new XMLHttpRequest();
		xhr.onreadystatechange = function () {
			if (xhr.readyState == 4) {
				if(xhr.status == 200){
					resolve(xhr.response);
				}else {
					reject('error');
				}
			}
		}
		xhr.open('GET', url);
		xhr.send();
	})
}


async function get(){
	let a = await getJson('https://pujie1213.top:424/rcGame');
	console.log(`a:${a}`);
	let b = await getJson('https://pujie1213.top:424/rcGame');
	console.log(`b:${b}`);
}

get();


async关键字的意思很简单，就是函数返回的是一个promise。
async函数会返回一个promise对象，如果function中返回的是一个值，async直接会用Promise.resolve()包裹一下返回。
```

## 18.18 eventloop

```js
宏任务  \
	当前调用栈中执行的代码成为宏任务 定时器 I/O、setTimeout、setInterval、				setImmediate、requestAnimationFrame
微任务 
	当前（此次事件循环中）宏任务执行完，在下一个宏任务开始之前需要执行的任务,可以理解为回调事件。（promise.then，process.nextTick等等） promise async generator
	process.nextTick、MutationObserver、Promise.then catch finally

先执行 微任务  再执行宏任务
```





# 十九，AJAX

 **AJAX 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。** 

## 19.1 http状态码

```
200("OK")
一切正常。实体主体中的文档（若存在的话）是某资源的表示。
400("Bad Request")
客户端方面的问题。实体主题中的文档（若存在的话）是一个错误消息。希望客户端能够理解此错误消息，并改正问题。
500("Internal Server Error")
服务期方面的问题。实体主体中的文档（如果存在的话）是一个错误消息。该错误消息通常无济于事，因为客户端无法修复服务器方面的问题。
301("Moved Permanently")
当客户端触发的动作引起了资源URI的变化时发送此响应代码。另外，当客户端向一个资源的旧URI发送请求时，也发送此响应代码。
404("Not Found") 和410("Gone")
当客户端所请求的URI不对应于任何资源时，发送此响应代码。404用于服务器端不知道客户端要请求哪个资源的情况；410用于服务器端知道客户端所请求的资源曾经存在，但现在已经不存在了的情况。
409("Conflict")
当客户端试图执行一个”会导致一个或多个资源处于不一致状态“的操作时，发送此响应代码。


2xx (成功)表示成功处理了请求的状态代码
3xx (重定向) 表示要完成请求，需要进一步操作。 通常，这些状态代码用来重定向。
4xx(请求错误) 这些状态代码表示请求可能出错，妨碍了服务器的处理
5xx(服务器错误)这些状态代码表示服务器在尝试处理请求时发生内部错误。 这些错误可能是服务器本身的错误，而不是请求出错
```

## 19.2 发送同步请求

```js
var http = new XMLHttpRequest();   生成一个实例
http.open('method','url',false)  最后一个参数控制同步异步
http.send();   发送请求

发请求的同源组策略 同请求 同域名  同端口  缺一不可

get post 的区别

GET - 从指定的资源请求数据。
POST - 向指定的资源提交要被处理的数据

###代码上的区别
 1:get通过url传递参数
 2:post设置请求头  规定请求数据类型
###使用上的区别
 1:post比get安全
 (因为post参数在请求体中。get参数在url上面)
 2:get传输速度比post快 根据传参决定的。
 (post通过请求体传参，后台通过数据流接收。速度稍微慢一些。而get通过url传参可以直接获取)
 3:post传输文件大理论没有限制  get传输文件小大概7-8k ie4k左右
 4:get获取数据	post上传数据
 (上传的数据比较多  而且上传数据都是重要数据。所以不论在安全性还是数据量级 post是最好的选择)

GET后退按钮/刷新无害，POST数据会被重新提交（浏览器应该告知用户数据会被重新提交）。
GET书签可收藏，POST为书签不可收藏。
GET能被缓存，POST不能缓存 。
GET编码类型application/x-www-form-url，POST编码类型encodedapplication/x-www-form-urlencoded 或 multipart/form-data。为二进制数据使用多重编码。
GET历史参数保留在浏览器历史中。POST参数不会保存在浏览器历史中。
GET对数据长度有限制，当发送数据时，GET 方法向 URL 添加数据；URL 的长度是受限制的（URL 的最大长度是 2048 个字符）。POST无限制。
GET只允许 ASCII 字符。POST没有限制。也允许二进制数据。
与 POST 相比，GET 的安全性较差，因为所发送的数据是 URL 的一部分。
** 在发送密码或其他敏感信息时绝不要使用 GET ！**
POST 比 GET 更安全，因为参数不会被保存在浏览器历史或 web 服务器日志中。G
ET的数据在 URL 中对所有人都是可见的。POST的数据不会显示在 URL 中。

同步发请求的注意
在同一个目录下
访问的时候用和等同于访问的地址

跨域解决方案：

		1. JSONP

		2. CORS（跨域资源访问）

		3. 服务器代理
```

## 19.3异步请求

```js
状态码
1**：请求收到，继续处理
2**：操作成功收到，分析、接受
3**：完成此请求必须进一步处理
4**：请求包含一个错误语法或不能完成S
5**：服务器执行一个完全有效请求失败

onreadystatechange  当状态码改变时

readyState   准备状态 

status  状态码

检查ajax状态码
	window.onload = function(){
		var http = new XMLHttpRequest();
		http.onreadystatechange = function(){
            console.log(http.readyState,http.status)
			if(http.readyState == 4 && http.status == 200){
				console.log('成功')
			}

		}
        http.open('get','http://localhost');
        http.send();
	}
```

## 19.4JSON

```js
JSON(JavaScript Object Notation, JS 对象简谱) 是一种轻量级的数据交换格式。它基于 ECMAScript (欧洲计算机协会制定的js规范)的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

要实现从JSON字符串转换为JS对象，使用 JSON.parse() 方法：

要实现从JS对象转换为JSON字符串，使用 JSON.stringify() 方法


var json = http.response;
                var arr = JSON.parse(json);
                arr.forEach(function(item,index){
                    console.log(item.name);
                })
```

## 19.5 JSONP

```js
jsonp的核心原理就是目标页面回调本地页面的方法,并带入参数
只能发送get请求
jsonp的原理：script标签具有跨域性，可以利用Script标签的src属性发送跨域请求，获取相应数据

原理：动态创建一个script标签。利用script标签的src属性不受同源策略限制。因为所有的src属性和href属性都不受同源策略限制。可以请求第三方服务器数据内容。

步骤

去创建一个script标签
script的src属性设置接口地址
接口参数,必须要带一个自定义函数名 要不然后台无法返回数据。
通过定义函数名去接收后台返回数据

 function getjson(data){
            console.log(data);
        }
	// }
	</script>
    <script type="text/javascript" src = 'https://pujie1213.top:424/rcGame?callback=getjson'></script>
```

## 19.6接口API

## 19.7 发送post请求

```js
var http = new XMLHttpRequest();
				http.onreadystatechange = function(){
					if(http.readyState == 4){
						if(http.status == 200){
							console.log(http.response);
						}
					}
				}
				http.open('post','https://pujie1213.top:424/login');
				//设置请求头
				http.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
				http.send('username='+ username.value + '&password=' + password.value);
						
				
Content-Type的类型				
application/x-www-form-urlencoded 与 application/json 的区别：
如果是通过页面表单方式提交，那就是”application/x-www-form-urlencoded”；
如果是json（要反序列化成字符串），那就是”application/json”

text/xml    multipart/form-data

```

## 19.8 jqury AJAX

```js
var option = {
    url: 请求地址,
    type: 请求方式 GET POST,
    data: {
    	传递给后端的参数
	},
    dataType: 返回的数据类型 (jsonp),
    success: function(data, textStatus, XHR){
        请求成功以后的回调函数
    },
    error: function(XHR, textStatus, error){
        请求失败后的回调函数
    },
    complete: function(){
        请求发送完毕以后触发的回调函数
    }
}
$.ajax(option);

$.get(url, data, success)

$.post(url, data, success)



$.get('https://pujie1213.top:424/rcGame',function(data){
				console.log(data)
			});
$.post('https://pujie1213.top:424/login',{
	username: 'ppp',
	password: 'bbb'
	},function(data){
		console.log(data)
})

发 jsonp 请求 
$.ajax({
				url: 'https://pujie1213.top:424/rcGamejsonp',
				type: 'get',
				datatype: 'jsonp',
				// data: {
				// 	username: 'ppp',
				// 	password: 'bbb'
				// },
				success: function(data){
					console.log(data);
				}
	})

发 post请求

$.ajax({
				url: 'https://pujie1213.top:424/login',
				type: 'post',
				// datatype: 'jsonp',
				data: {
					username: 'ppp',
					password: 'bbb'
				},
				success: function(data){
					console.log(data);
				}
})

发 get请求
$.ajax({
				url: 'https://pujie1213.top:424/rcGame',
				type: 'get',
				// datatype: 'jsonp',
				// data: {
				// 	username: 'ppp',
				// 	password: 'bbb'
				// },
				success: function(data){
					console.log(data);
				}
			})
			
			
表单发请求和 ajax发 请求的区别
1. Ajax在提交、请求、接收时，都是异步进行的，网页不需要刷新；
Form提交则是新建一个页面，哪怕是提交给自己本身的页面，也是需要刷新的；
2. A在提交时，是在后台新建一个请求；
F却是放弃本页面，而后再请求；
3. A必须要使用JS来实现，不启用JS的浏览器，无法完成该操作；
F却是浏览器的本能，无论是否开启JS，都可以提交表单；
```

## 19.9 cookie localStorage sessionStorage

```js
document.cookie = 'username=1;expires='+ date.toUTCString();
document.cookie = 'password=sdadjajdal'

当浏览器再请求该网站时，浏览器把请求的网址连同该Cookie一同提交给服务器。
Expires  该属性用来设置Cookie的有效期
HTTP cookie，通常称为cookie，用于在客户端存储会话信息。

cookie的优点

通过良好的编程，控制保存在cookie中的session对象的大小。
通过加密和安全传输技术（SSL），减少cookie被破解的可能性。
只在cookie中存放不敏感数据，即使被盗也不会有重大损失。
控制cookie的生命期，使之不会永远有效。偷盗者很可能拿到一个过期的cookie。、
不需要服务器资源，直接存储在本地。

cookie的缺点

cookie大小的限制
安全性
cookie的清理
每个域的cookie总数是有限的，不同浏览器之间各有不同。


cookie的应用

购物车（网购）
自动登录（登录账号时的自动登录）
精准广告
平常浏览网页时有时会推出商品刚好是你最近浏览过，买过的类似东西，这些是通过cookie记录的。
记住登录状态

cookie的封装
function setCookie(key, value, expires){
	var date = new Date();
	date.setDate(date.getDate() + expires);
	document.cookie = key + '=' + value + ';expires=' + date.toUTCString();
}
function removeCookie(key){
	setCookie(key, 1, -1);
}
function getCookie(key){
	var data = document.cookie;
	if(data.length == 0){
		return undefined;
	}else{
		var result = new Object();
		data = data.replace(/\s/g, '');
		if(/;/.test(data)){
			var arr = data.split(';');
			arr.forEach(function(item, index){
				var arr = item.split('=');
				result[arr[0]] = arr[1];
			})
		}else{
			var arr = data.split('=');
			result[arr[0]] = arr[1];
		}

		return result[key];
	}
}
	
	
	他们之间的区别@@@@@@@@@@@@@@@@@@@@@
	特性
    Cookie 一般由服务器生成，可设置失效时间。如果在浏览器端生成Cookie，默认是关闭浏览器后失效   4K左右  每次都会携带在HTTP头中，如果使用cookie保存过多数据会带来性能问题  需要程序员自己封装，源生的Cookie接口不友好
    
    localStorage 除非被清除，否则永久保存 一般为5MB 仅在客户端（即浏览器）中保存，不参与和服务器的通信 源生接口可以接受，亦可再次封装来对Object和Array有更好的支持
    
    sessionStorage 仅在当前会话下有效，关闭页面或浏览器后被清除 一般为5MB 仅在客户端（即浏览器）中保存，不参与和服务器的通信   源生接口可以接受，亦可再次封装来对Object和Array有更好的支持
    
    localStorage.setItem("b","isaac");//设置b为"isaac"
    var b = localStorage.getItem("b");//获取b的值,为"isaac"
    var a = localStorage.key(0); // 获取第0个数据项的键名，此处即为“b”
    localStorage.removeItem("b");//清除c的值
    localStorage.clear();//清除当前域名下的所有localstorage数据


```

## 19.10、ES five

#### 1.严格模式

```javascript
开启方法：
	在执行的代码顶部写一个字符串 'use strict'
	函数内部顶端也可以开启 同上
严格模式
    为了消除JavaScript语法的不合理不严谨之处，减少怪异行为
    消除代码运行的不安全之处，保证代码安全执行
    提高编译效率，增加运行速度
    为未来新版本的JavaScript做好铺垫
    1. 必须使用 var 关键字声明变量
    2. eval()函数有独立的作用域
    3. 对象下不能存在相同的属性名
    4. 禁止this指向 window

函数内部也可以开始严格模式
```

#### 2. eval()

将字符串转换为JS代码并执行

```
'use strict'
var a = 1;
eval('var a = 2');
console.log(a);
严格模式  不执行eval();
普通模式覆盖
```



#### 3. Object.defineProperty()

```javascript
给目标对象扩展属性描述

描述默认为false

var obj = {};
Object.defineProperty(obj, 'litwo', {
    value: 'cxk', 属性值
    writable: true, 是否可以修改内容
    enumerable: true, 是否可以被for in 枚举
    configurable: true  是否可以被 delete 删除
});

set 方法  修改属性的值时发生的改变的时候执行函数
get 方法	获取属性的时候执行函数

双向绑定
var input = document.getElementById('input');
	var text = document.getElementById('text');
	input.onkeyup = function(){
		this.in = this.value;
	}
	Object.defineProperty(input,'in',{
		get: function(){

		},
		set: function(value){
			text.innerHTML = value;
		}
	})
```

# 二十一：XSS攻击

```
Cross-Site Scripting（跨站脚本攻击）简称 XSS，是一种代码注入攻击。攻击者通过在目标网站上注入恶意脚本，使之在用户的浏览器上运行。利用这些恶意脚本，攻击者可获取用户的敏感信息如 Cookie、SessionID 等，进而危害数据安全。

XSS 的本质是：恶意代码未经过滤，与网站正常的代码混在一起；浏览器无法分辨哪些脚本是可信的，导致恶意脚本被执行。
而由于直接在用户的终端执行，恶意代码能够直接获取用户的信息，或者利用这些信息冒充用户向网站发起攻击者定义的请求。
在部分情况下，由于输入的限制，注入的恶意脚本比较短。但可以通过引入外部的脚本，并由浏览器执行，来完成比较复杂的攻击策略
```

## 1.XSS 分类

根据攻击的来源，XSS 攻击可分为存储型、反射型和 DOM 型三种。

## 2.**XSS的危害**

```
1.窃取网页浏览中的cookie值
2.劫持流量实现恶意跳转

```

## 3.**利用与绕过**

```
1.大小写绕过
2.利用过滤后返回语句再次构成攻击语句来绕过
3.并不是只有script标签才可以插入代码
4.编码脚本代码绕过关键字过滤
5.主动闭合标签实现注入代码

```



# 二十二、模块化开发

## 1.AMD（异步模块定义）

AMD主要用于浏览器端，RequireJS 就是它的实现

异步加载模块不会造成页面加载的阻塞

RequireJS是一个工具库，主要用于客户端的模块管理。它可以让客户端的代码分成一个个模块，实现异步或动态加载，从而提高代码的性能和可维护性。它的模块管理遵守[AMD规范](https://github.com/amdjs/amdjs-api/wiki/AMD)（Asynchronous Module Definition）。

语法：

​		定义模块

```javascript
//定义没有依赖的模块
define(function () {
    return {
        method1: function() {},
        method2: function() {},
    };
})
//定义有依赖的模块
define([module1,module2],function (module1,module2) {
    return 模块
})
```

​		引入模块

```javascript
require([module1,module2],function (module1,module2) {
    //使用module1，module2
})
```

## 2.ES6 Module

```javascript
暴露模块
export const a = 10;
export const obj = {};
const obj1 = {};
export {obj1};

暴露默认模块
export default {
    
}
export default function(){
    
}

引入
按需引入
import {a,obj} from 模块路径

引入所有
import 自定义名字 from 模块路径

script标签使用ES6 Module 要注意 type="module"  
ES6 Module 是异步的 下载完毕后就执行
```

## 3. CommenJS规范（Nodejs）

```javascript
引入模块
require(模块名);

暴露模块
exports.属性名 = 属性值

module.exports = {
    
}
```

## 4.CMD

```js
规范是  sea.js

define(function(require,exports,module){
	var spinning = require('');
})


通过define()定义，没有依赖前置，通过require加载jQuery插件，CMD是依赖就近，在什么地方使用到插件就在什么地方require该插件，即用即返，这是一个同步的概念
```



# 二十三 前端面试题补充

## 20.1meta标签的详细

```
name 属性 
"keywords" 是一个经常被用到的名称。它为文档定义了一组关键字。某些搜索引擎在遇到这些关键字时，会用这些关键字对文档进行分类。
http-equiv 属性
这将告诉浏览器准备接受一个 HTML 文档。
charset="UTF-8"  语言编码

```

## 20.1css层叠等级

```
z-index正值 > z-index:auto 或等于0 >行内>浮动>块级>z-index负>background
```

## 20.2遍历的对比

```js
for循环 麻烦
forEach方法。 无法中途跳出forEach循环，break命令或return命令都不能奏效。
for in方法  数组的键名是数字，但是for...in循环是以字符串作为键名“0”、“1”、“2”等等。
            for...in循环不仅遍历数字键名，还会遍历手动添加的其他键甚至包括原型链上的键
            某些情况下，for...in循环会以任意顺序遍历键名。for...in循环主要是为遍历对象				而设计的
for...of   有着同for...in一样的简洁语法，但是没有for...in那些缺点。
            不同于forEach方法，它可以与break、continue和return配合使用。
            提供了遍历所有数据结构的统一操作接口。
```

## 20.3网站性能优化实践总结

```
1.资源缓存
	1.1 使用CDN
	1.2 利用HTTP缓存机制
2. 资源的合并压缩
	2.1 减少HTTP请求
	2.2 JS文件
	2.3 CSS文件
	2.4 图片
	2.5 服务器端开启gzip
3.浏览器加载、解析、渲染机制
```

## 20.5找出出现次数最多的一个数

```js
let a = [1,2,3,4,4,5,8,4,3,2,7,1,2,1,2,3,4,2,2];
	let b = (...value) => {let c = new Set([...value]);return c};
	let d = b(...a);
		var obj = {};
		d.forEach((item1,index) =>{
			obj[item1] = 0;
			for(let i =0 ; i < a.length; i++){
				if(item1 == a[i]){
					obj[item1]++;
				}
			}
		})
		var max = 0;
		var maxj = 0;
		for(let j in obj){
			if(obj[j] > max){
				max = obj[j];
				maxj = j;
			}
		}
		console.log(maxj,max)
```

## 20.6理解 async/await以及对Generator的优势*

```
　　 async await 是用来解决异步的，async函数是Generator函数的语法糖

　　使用关键字async来表示，在函数内部使用 await 来表示异步

　　async函数返回一个 Promise 对象，可以使用then方法添加回调函数

　　当函数执行的时候，一旦遇到await就会先返回，等到异步操作完成，再接着执行函数体内后面的语句

　　async较Generator的优势：

　　（1）内置执行器。Generator 函数的执行必须依靠执行器，而 Aysnc 函数自带执行器，调用方式跟普通函数的调用一样

　　（2）更好的语义。async 和 await 相较于 * 和 yield 更加语义化　　

　　（3）更广的适用性。yield命令后面只能是 Thunk 函数或 Promise对象，async函数的await后面可以是Promise也可以是原始类型的值

　　（4）返回值是 Promise。async 函数返回的是 Promise 对象，比Generator函数返回的Iterator对象方便，可以直接使用 then() 方法进行调用
```

## 20.7 innerhtml 和 innertext  css

```c&#39;s
innerHTML指的是从对象的起始位置到终止位置的全部内容,包括Html标签。可以读取标签
innerText   指的是从起始位置到终止位置的内容,但它去除Html标签。不能du'q
outerHTML指的是除了包含innerHTML的全部内容外, 还包含对象标签本身。

前端页面由  结构层 表示层  行为层 构成

如何居中一个浮动元素
div{
		position: relative;
		left: 50%;
		float: left;
		height: 500px;
		background: #f99;
		width: 500px;
	}
	p{
		position: relative;
		right: 50%;
		float: left;
		height: 200px;
		background: blue;
		width: 200px;
	}
```

## 20.8 less

```
用@来声明一个变量@pink:pink 
作为普通属性值来使用直接用 @pink
作为选择器来使用#@{selector的值}的形式
作为url @{url}
变量的延迟加载

&的使用 代表平级别

定义混合用. 
```

## 20.9Blob转化

```
var reader = new FileReader(); reader.onload = function(event){ var content = reader.result;//内容就在这里 }; reader.readAsText(blob);
```

