---
title: JavaScript面试-2
date:
updated:
type: "tags"
categories: 面试
comments:
description: JavaScript面试-2
keywords: JavaScript面试-2
cover: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=4234896097,4021899470&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.手写 filter 方法
call 和 apply 的传参不同，call 接收逗号分隔的参数，
apply 接收数组（如何记不清这两个方法的区别的话，可以记 apply 接收 array，
都是 a 开头的，这样比较好记），调用都会立即执行。
而 bind 调用完返回的是一个函数，需要再次调用才会执行
```js
Array.prototype.filter = function (fn, context) {
  if (typeof fn != "function") {
    throw new TypeError(`${fn} is not a function`);
  }
  let arr = this;
  let reuslt = [];
  for (var i = 0; i < arr.length; i++) {
    let temp = fn.call(context, arr[i], i, arr);
    if (temp) {
      result.push(arr[i]);
    }
  }
  return result;
};
```
# 2.严格模式
“use strict”;关键字
如果这行语句不在第一行，则无效
将”use strict”放在函数体的第一行，则整个函数以”严格模式”运行。
####　 - 消除 Javascript 语法的一些不合理、不严谨之处，减少一些怪异行为; ####　　- 消除代码运行的一些不安全之处，保证代码运行的安全； ####　　- 提高编译器效率，增加运行速度； ####　　- 为未来新版本的 Javascript 做好铺垫。

## 1.在正常模式中，如果一个变量没有声明就赋值，默认是全局变量。严格模式禁止这种用法，全局变量必须显式声明。
## 2.静态绑定
Javascript 语言的一个特点，就是允许”动态绑定”，即某些属性和方法到底属于哪一个对象，不是在编译时确定的，而是在运行时（runtime）确定的。
### (1)禁止使用 with 语句因为 with 语句无法在编译时就确定，属性到底归属哪个对象。
### (2)创设 eval 作用域 eval 语句的作用域，取决于它处于全局作用域，还是处于函数作用域。严格模式下，eval 语句本身就是一个作用域，不再能够生成全局变量了，它所生成的变量只能用于 eval 内部。
## 3. 增强的安全措施
### (1)禁止 this 关键字指向全局对象
```js
function f() {
  return !this;
} // 返回false，因为"this"指向全局对象，"!this"就是false
function f() {
  "use strict";
  return !this;
} // 返回true，因为严格模式下，this的值为undefined，所以"!this"为true。
```
### (2)禁止在函数内部遍历调用栈
## 4. 禁止删除变量
严格模式下无法删除变量。只有 configurable 设置为 true 的对象属性，才能被删除。
```js
"use strict";
var x;
delete x; // 语法错误
var o = Object.create(null, {
  x: {
    value: 1,
    configurable: true,
  },
});
delete o.x; // 删除成功
```

## 5.显式报错
正常模式下，对一个对象的只读属性进行赋值，不会报错，只会默默地失败。严格模式下，将报错。
严格模式下，对禁止扩展的对象添加新属性，会报错。
严格模式下，删除一个不可删除的属性，会报错。
```js
"use strict";
var o = {};
Object.defineProperty(o, "v", { value: 1, writable: false });
o.v = 2; // 报错

var o = {};
Object.preventExtensions(o);
o.v = 1; // 报错

("use strict");
delete Object.prototype; // 报错
```
## 6.重名错误
```js
（1）对象不能有重名的属性 正常模式下，如果对象有多个重名属性，最后赋值的那个属性会覆盖前面的值。严格模式下，这属于语法错误。
（2）函数不能有重名的参数
（3）禁止八进制表示法
（4）arguments 对象的限制
（5）arguments 不再追踪参数的变化
（6）禁止使用 arguments.callee
（7）保留字 implements, interface, let, package, private, protected, public, static, yield。
```
# 3.实现一个方法，可以给 obj 所有的属性添加动态绑定事件，当属性值发生变化时会触发事件
```js
// 实现一个方法，可以给 obj 所有的属性添加动态绑定事件，当属性值发生变化时会触发事件
let obj = {
  key_1: 1,
  key_2: 2,
};
function func(key) {
  console.log(key + " 的值发生改变：" + this[key]);
}
bindData(obj, func);
obj.key_1 = 2; // 此时自动输出 "key_1 的值发生改变：2"
obj.key_2 = 1; // 此时自动输出 "key_2 的值发生改变：1"

function bindData(obj, fn) {
  for (let key in obj) {
    Object.defineProperty(obj, key, {
      set(newVal) {
        if (this.value !== newVal) {
          this.value = newVal;
          fn.call(obj, key);
        }
      },
      get() {
        return this.value;
      },
    });
  }
}
```
# 4.Proxy 相比于 defineProperty 的优势
```js
Object.defineProperty() 的问题主要有三个：
不能监听数组的变化
必须遍历对象的每个属性
必须深层遍历嵌套的对象
针对对象：针对整个对象，而不是对象的某个属性，所以也就不需要对 keys 进行遍历。这解决了上述 Object.defineProperty() 第二个问题
支持数组：Proxy 不需要对数组的方法进行重载，省去了众多 hack，减少代码量等于减少了维护成本，而且标准的就是最好的
Proxy 的第二个参数可以有 13 种拦截方法，这比起 Object.defineProperty() 要更加丰富
Proxy 作为新标准受到浏览器厂商的重点关注和性能优化，相比之下 Object.defineProperty() 是一个已有的老方法。
```

# 5.nextTick
```js
在Vue生命周期的created()钩子函数进行的DOM操作一定要放在Vue.nextTick()的回调函数中
在数据变化后要执行的某个操作，而这个操作需要使用随数据改变而改变的DOM结构的时候，这个操作都应该放进Vue.nextTick()的回调函数中。
```

# 6.首页白屏
```js
优化 webpack 减少模块打包体积，code-split 按需加载
服务端渲染，在服务端事先拼装好首页所需的 html
首页加 loading 或 骨架屏 （仅仅是优化体验）
1.使用首屏SSR + 跳转SPA方式来优化
2.改单页应用为多页应用，需要修改webpack的entry
3.改成多页以后使用应该使用prefetch的就使用
4.处理加载的时间片，合理安排加载顺序，尽量不要有大面积空隙
5.CDN资源还是很重要的，最好分开，也能减少一些不必要的资源损耗
6.使用Quicklink，在网速好的时候 可以帮助你预加载页面资源
7.骨架屏这种的用户体验的东西一定要上，最好借助stream先将这部分输出给浏览器解析
8.合理使用web worker优化一些计算
9.缓存一定要使用，但是请注意合理使用
10.大概就这么多，最后可以借助一些工具进行性能评测，重点调优，例如使用performance自己实现下等
```
