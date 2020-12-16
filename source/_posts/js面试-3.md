---
title: JavaScript面试-3
date:
updated:
type: "tags"
categories: 面试
comments:
description: JavaScript面试-3
keywords: JavaScript面试-3
cover: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=4234896097,4021899470&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

# 1..for循环和forEach循环性能对比
for循环是常见的循环语句forEach和map是在ES5出的，但是在性能上后者不如前者，在次数少的情况下forEach会比for要快，但是到达了十万次时forEach明显就跟不上了。在大数据量的情况下for循环的兼容性和多环境运行表现比较优秀，forEach的优点是在数据量小时占优势，语义话更简洁。循环时没有返回值。map和forEach差不多但是map循环有返回值 10w量级下foreach优秀 大于10wfor循环优秀

# 2.使用 JavaScript Proxy 实现简单的数据绑定
```js
<body>
  hello,world
  <input type="text" id="model">
  <p id="word"></p>
</body>
<script>
  const model = document.getElementById("model")
  const word = document.getElementById("word")
  var obj= {};

  const newObj = new Proxy(obj, {
      get: function(target, key, receiver) {
        console.log(`getting ${key}!`);
        return Reflect.get(target, key, receiver);
      },
      set: function(target, key, value, receiver) {
        console.log('setting',target, key, value, receiver);
        if (key === "text") {
          model.value = value;
          word.innerHTML = value;
        }
        return Reflect.set(target, key, value, receiver);
      }
    });

  model.addEventListener("keyup",function(e){
    newObj.text = e.target.value
  })
</script>
```

# 3.输入框的防抖和节流
```html
//防抖
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
</head>
<body>
    用户名: <input onblur="checkUsername" placeholder="请输入用户名" id="username" />

    <script>
        var timer;
        var count = 0;
        var $username = document.getElementById('username');
        $username.addEventListener('input', function () {
            console.log(++count);
            // 每次输入就清除定时器,一直输入就一直清除,下面的console.log就永远不会触发,
            // 直到你不输入一秒后才触发 
            clearTimeout(timer);
            timer = setTimeout(function () {
                console.log('发请求到后台,检查用户是否已注册');
            }, 1000)
        }, false)
    </script>
</body>
// 节流
用户名: <input placeholder="请输入用户名" id="username" />
    <script>
        var timer;
        var count = 0;

        var $username = document.getElementById('username');
        $username.addEventListener('input', throttle(function () {
            console.log(++count);
        }), false)

        function throttle(callback) {
            // 上一次点击的时间
            let preTime = Date.now();
            return function () {
                let args = arguments;
                // 现在点击时间
                let now = Date.now();
                // 现在点击的时间跟上一次点击的时间如果超过了一秒,执行回调
                if (now - preTime >= 1000) {
                    callback(args);
                    // 从新计时,这次点击的时间成为下一次点击时间的起点
                    preTime = now;
                }
            }
        }
    </script>
```

# 4.var、let 和 const 区别的实现原理是什么
```js
区别
####var 和 let 用以声明变量，const 用于声明只读的常量；
var 声明的变量，不存在块级作用域，在全局范围内都有效，let 和 const 声明的，只在它所在的代码块内有效；
let 和 const 不存在像 var 那样的 “变量提升” 现象，所以 var 定义变量可以先使用，后声明，而 let 和 const 只可先声明，后使用；
let 声明的变量存在暂时性死区，即只要块级作用域中存在 let，那么它所声明的变量就绑定了这个区域，不再受外部的影响。
let 不允许在相同作用域内，重复声明同一个变量；
const 在声明时必须初始化赋值，一旦声明，其声明的值就不允许改变，更不允许重复声明；
5.箭头函数和普通函数的区别
1、函数体内的 this 对象，就是定义时所在的对象，而不是使用时所在的对象。
2、不可以使用 arguments 对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
3、不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数。
4、不可以使用 new 命令，因为：
没有自己的 this，无法调用 call，apply。
没有 prototype 属性 ，而 new 命令在执行时需要将构造函数的 prototype 赋值给新的对象的 proto
```

# 5.简单实现async/await中的async函数
```js
function spawn(genF) {
    return new Promise(function(resolve, reject) {
        const gen = genF();
        function step(nextF) {
            let next;
            try {
                next = nextF();
            } catch (e) {
                return reject(e);
            }
            if (next.done) {
                return resolve(next.value);
            }
            Promise.resolve(next.value).then(
                function(v) {
                    step(function() {
                        return gen.next(v);
                    });
                },
                function(e) {
                    step(function() {
                        return gen.throw(e);
                    });
                }
            );
        }
        step(function() {
            return gen.next(undefined);
        });
    });
}
```

# 6.new 操作符干了什么
```js
    (1) 创建一个新对象；
    (2) 将构造函数的作用域赋给新对象（因此 this 就指向了这个新对象） ；
    (3) 执行构造函数中的代码（为这个新对象添加属性） ；
    (4) 返回新对象。
```

# 7.实现sleep函数
```js
const sleep = (time) => {
  return new Promise(resolve => setTimeout(resolve, time))
}
sleep(1000).then(() => {
    // 这里写你的骚操作
})
//操作

//Promise
const sleep = time => {
  return new Promise(resolve => setTimeout(resolve,time))
}
sleep(1000).then(()=>{
  console.log(1)
})

//Generator
function* sleepGenerator(time) {
  yield new Promise(function(resolve,reject){
    setTimeout(resolve,time);
  })
}
sleepGenerator(1000).next().value.then(()=>{console.log(1)})

//async
function sleep(time) {
  return new Promise(resolve => setTimeout(resolve,time))
}
async function output() {
  let out = await sleep(1000);
  console.log(1);
  return out;
}
output();

//ES5
function sleep(callback,time) {
  if(typeof callback === 'function')
    setTimeout(callback,time)
}

function output(){
  console.log(1);
}
sleep(output,1000);
```
# 8.实现一个Promise
```js
const PENDING = "pending";
const FULFILLED = "fulfilled";
const REJECTED = "rejected";

function Promise(excutor) {
    let that = this; // 缓存当前promise实例对象
    that.status = PENDING; // 初始状态
    that.value = undefined; // fulfilled状态时 返回的信息
    that.reason = undefined; // rejected状态时 拒绝的原因
    that.onFulfilledCallbacks = []; // 存储fulfilled状态对应的onFulfilled函数
    that.onRejectedCallbacks = []; // 存储rejected状态对应的onRejected函数

    function resolve(value) { // value成功态时接收的终值
        if(value instanceof Promise) {
            return value.then(resolve, reject);
        }
        // 实践中要确保 onFulfilled 和 onRejected 方法异步执行，且应该在 then 方法被调用的那一轮事件循环之后的新执行栈中执行。
        setTimeout(() => {
            // 调用resolve 回调对应onFulfilled函数
            if (that.status === PENDING) {
                // 只能由pending状态 => fulfilled状态 (避免调用多次resolve reject)
                that.status = FULFILLED;
                that.value = value;
                that.onFulfilledCallbacks.forEach(cb => cb(that.value));
            }
        });
    }
    function reject(reason) { // reason失败态时接收的拒因
        setTimeout(() => {
            // 调用reject 回调对应onRejected函数
            if (that.status === PENDING) {
                // 只能由pending状态 => rejected状态 (避免调用多次resolve reject)
                that.status = REJECTED;
                that.reason = reason;
                that.onRejectedCallbacks.forEach(cb => cb(that.reason));
            }
        });
    }

    // 捕获在excutor执行器中抛出的异常
    // new Promise((resolve, reject) => {
    //     throw new Error('error in excutor')
    // })
    try {
        excutor(resolve, reject);
    } catch (e) {
        reject(e);
    }
}

Promise.prototype.then = function(onFulfilled, onRejected) {
    const that = this;
    let newPromise;
    // 处理参数默认值 保证参数后续能够继续执行
    onFulfilled =
        typeof onFulfilled === "function" ? onFulfilled : value => value;
    onRejected =
        typeof onRejected === "function" ? onRejected : reason => {
            throw reason;
        };
    if (that.status === FULFILLED) { // 成功态
        return newPromise = new Promise((resolve, reject) => {
            setTimeout(() => {
                try{
                    let x = onFulfilled(that.value);
                    resolvePromise(newPromise, x, resolve, reject); // 新的promise resolve 上一个onFulfilled的返回值
                } catch(e) {
                    reject(e); // 捕获前面onFulfilled中抛出的异常 then(onFulfilled, onRejected);
                }
            });
        })
    }

    if (that.status === REJECTED) { // 失败态
        return newPromise = new Promise((resolve, reject) => {
            setTimeout(() => {
                try {
                    let x = onRejected(that.reason);
                    resolvePromise(newPromise, x, resolve, reject);
                } catch(e) {
                    reject(e);
                }
            });
        });
    }

    if (that.status === PENDING) { // 等待态
        // 当异步调用resolve/rejected时 将onFulfilled/onRejected收集暂存到集合中
        return newPromise = new Promise((resolve, reject) => {
            that.onFulfilledCallbacks.push((value) => {
                try {
                    let x = onFulfilled(value);
                    resolvePromise(newPromise, x, resolve, reject);
                } catch(e) {
                    reject(e);
                }
            });
            that.onRejectedCallbacks.push((reason) => {
                try {
                    let x = onRejected(reason);
                    resolvePromise(newPromise, x, resolve, reject);
                } catch(e) {
                    reject(e);
                }
            });
        });
    }
};
```

# 9.实现深拷贝
```js
const mapTag = "[object Map]";
const setTag = "[object Set]";
const arrayTag = "[object Array]";
const objectTag = "[object Object]";

const boolTag = "[object Boolean]";
const dateTag = "[object Date]";
const errorTag = "[object Error]";
const numberTag = "[object Number]";
const regexpTag = "[object RegExp]";
const stringTag = "[object String]";
const symbolTag = "[object Symbol]";

const otherTags = [dateTag, errorTag, numberTag, stringTag];
const deepTags = [mapTag, setTag, arrayTag, objectTag, argumentTag];

// 判断类型
function getType(original) {
  return Object.prototype.toString.call(original);
}

// 判断是否为引用类型
function isObject(original) {
  const type = typeof original;
  return original !== null && type === "object";
}

// 初始化被克隆的对象
function initCopy(original) {
  const Ctor = original.constructor;
  return new Ctor();
}

export function deepClone(original, map = new WeakMap()) {
  const type = getType(original);

  // 判断引用类型,原始数据直接返回
  // copy function是没有实际应用场景的，两个对象使用同一个引用地址的function没有任何问题，所以这里直接返回
  if (!isObject(original)) {
    return original;
  }

  if (deepTags.includes(type)) {
    let targetClone = initCopy(original);

    // 处理环
    if (map.get(original)) {
      return map.get(original);
    }
    // 处理Set
    if (type === setTag) {
      original.forEach(value => {
        targetClone.add(value);
      });
    }
    // 处理map
    if (type === mapTag) {
      original.forEach((value, key) => {
        targetClone.set(key, value);
      });
    }
    map.set(original, targetClone);
    Object.keys(original).forEach(key => {
      targetClone[key] = deepClone(original[key], map);
    });
    return targetClone;
  } else {
    // 处理其他数据类型
    const Ctor = original.constructor;
    if (otherTags.includes(type)) {
      return new Ctor(original);
    }
    // 处理Boolean
    if (type === boolTag) {
      return new original.constructor(original.valueOf());
    }
    // 处理Symbol
    if (type === symbolTag) {
      return Object(Symbol.prototype.valueOf.call(original));
    }
    // 处理reg
    if (type === regexpTag) {
      const reFlags = /w*$/;
      const result = new original.constructor(
        original.source,
        reFlags.exec(original)
      );
      result.lastIndex = original.lastIndex;
      return result;
    }
    return null;
  }
}
```