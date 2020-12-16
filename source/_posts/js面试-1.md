---
title: JavaScript面试-1
date:
updated:
type: "tags"
categories: 面试
comments:
description: JavaScript面试-1
keywords: JavaScript面试-1
cover: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=4234896097,4021899470&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

# 1.addEventListener 的第三个参数
capture: Boolean，表示 listener 会在该类型的事件捕获阶段传播到该 EventTarget 时触发。
once: Boolean，表示 listener 在添加之后最多只调用一次。如果是 true， listener 会在其被调用之后自动移除。
passive: Boolean，设置为 true 时，表示 listener 永远不会调用 preventDefault()。如果 listener 仍然调用了这个函数，客户端将会忽略它并抛出一个控制台警告。查看 使用 passive 改善的滚屏性能 了解更多.

# 2.Promise.all 并发限制
Promise.all 可以保证，promises 数组中所有 promise 对象都达到 resolve 状态，才执行 then 回调。npm 中有很多实现这个功能的第三方包，比如 async-pool、es6-promise-pool、p-limit，这里我直接拿 async-pool 的代码来分析一下实现原理
```js
function asyncPool(poolLimit, array, iteratorFn) {
    let i = 0;
    const ret = [];
    const executing = [];
    const enqueue = function () {
        // 边界处理，array为空数组
        if (i === array.length) {
            return Promise.resolve();
        }
        // 每调一次enqueue，初始化一个promise
        const item = array[i++];
        const p = Promise.resolve().then(() => iteratorFn(item, array));
        // 放入promises数组
        ret.push(p);
        // promise执行完毕，从executing数组中删除
        const e = p.then(() => executing.splice(executing.indexOf(e), 1));
        // 插入executing数字，表示正在执行的promise
        executing.push(e);
        // 使用Promise.rece，每当executing数组中promise数量低于poolLimit，就实例化新的promise并执行
        let r = Promise.resolve();
        if (executing.length >= poolLimit) {
            r = Promise.race(executing);
        }
        // 递归，直到遍历完array
        return r.then(() => enqueue());
    };
    return enqueue().then(() => Promise.all(ret));
}

//从array第1个元素开始，初始化promise对象，同时用一个executing数组保存正在执行的promise
//不断初始化promise，直到达到poolLimt
//使用Promise.race，获得executing中promise的执行情况，当有一个promise执行完毕，继续初始化promise并放入executing中
//所有promise都执行完了，调用Promise.all返回

//使用方法
const timeout = i => new Promise(resolve => setTimeout(() => resolve(i), i));
return asyncPool(2, [1000, 5000, 3000, 2000], timeout).then(results => {
    ...
});
```

# 3.Es6 promise then 对异常处理的方法
## 1. then()里有两个回调函数，第一个是成功后（resolve 返回）的回调 function(data) {}, 另一个是失败后（reject 返回）的回调 function(err) {}，异常发生时可以放在第二个回调里面处理。
## 2. 也可以在 then 后面加.catch，在这里面进行异常处理
## 建议用 2 第二种写法可以捕获 then 方法中的错误 也更加接近同步的写法 而不是建议使用 then 方法的第二个参数

# 4.对象数组排序
```js
   compare(key) {
      return function (a, b) {
        var value1 = a[key];
        var value2 = b[key];
        return value1 - value2;
      };
    },
    //sort()方法在原数组上排序，不生成副本。
    let result = res.data.sort(this.compare('parentId'));
```

# 5.对象数去重
```js
 //reduce
    arr.reduce(function(prev,cur,index,arr){
    ...
    }, init);
    // arr 表示原数组；
    // prev 表示上一次调用回调时的返回值，或者初始值 init;
    // cur 表示当前正在处理的数组元素；
    // index 表示当前正在处理的数组元素的索引，若提供 init 值，则索引为0，否则索引为1；
    // init 表示初始值。
    const result = responseList.reduce((acc, cur) => {
    const ids = acc.map(item => item.id);
    return ids.includes(cur.id) ? acc : [...acc, cur];
}, []);
```

# 6.手动封装一个请求函数，可以设置最大请求次数，请求成功则不再请求，请求失败则继续请求直到超过最大次数
```js
function request(url, body, successCallback, errorCallback, maxCount = 3) {
  return fetch(url, body)
    .then((response) => successCallback(response))
    .catch((err) => {
      if (maxCount <= 0) return errorCallback("请求超时");
      return request(url, body, successCallback, errorCallback, --maxCount);
    });
}

// 调用
request(
  "https://some/path",
  { method: "GET", headers: {} },
  (response) => {
    console.log(response.json());
  },
  (err) => console.error(err)
);
```

# 7.函数柯里化
```js
//解释
//是把接受多个参数的函数变换成接受一个单一参数（最初函数的第一个参数）的函数
//并且返回接受余下的参数而且返回结果的新函数的技术。
// 普通的add函数
function add(x, y) {
  return x + y;
}
// Currying后
function curryingAdd(x) {
  return function (y) {
    return x + y;
  };
}
add(1, 2); // 3
curryingAdd(1)(2); // 3
//实现函数柯里化
const curry = (fn, ...args1) => (...args2) =>
  ((arg) => (arg.length === fn.length ? fn(...arg) : curry(fn, ...arg)))([
    ...args1,
    ...args2,
  ]);
```
# 8.实现一个函数判断数据类型
```js
function getType(obj) {
   if (obj === null) return String(obj);
   return typeof obj === 'object' 
   ? Object.prototype.toString.call(obj).replace('[object ', '').replace(']', '').toLowerCase()
   : typeof obj;
}
```

# 9.性能优化
```js
 //页面优化
    DNS解析时间： domainLookupEnd - domainLookupStart
    TCP建立连接时间： connectEnd - connectStart
    白屏时间： responseStart - navigationStart
    dom渲染完成时间： domContentLoadedEventEnd - navigationStart
    页面onload时间： loadEventEnd - navigationStart

    //编码优化
    //数据读取
    通过作用域链 / 原型链 读取变量或方法时，需要更多的耗时，且越长越慢；
    对象嵌套越深，读取值也越慢；
    最佳实践:
        尽量在局部作用域中进行 变量缓存；
        避免嵌套过深的数据结构，数据扁平化 有利于数据的读取和维护；
    循环
        代码的性能问题会再循环中被指数倍放大
    最佳实践:
        尽可能 减少循环次数；
        减少遍历的数据量；
        完成目的后马上结束循环；
        避免在循环中执行大量的运算，避免重复计算，相同的执行结果应该使用缓存；
        js 中使用 倒序循环 会略微提升性能；
        尽量避免使用 for-in 循环，因为它会枚举原型对象，耗时大于普通循环
    减少 cookie 体积: 
        减少访问 dom 的次数，如需多次，将 dom 缓存于变量中；
        减少重绘与回流
        多次操作合并为一次；
    减少对计算属性的访问；
        例如 offsetTop， getComputedStyle 等
        因为浏览器需要获取最新准确的值，因此必须立即进行重排，这样会破坏了浏览器的队列整合，尽量将值进行缓存使用；
    大量操作时，可将 dom 脱离文档流或者隐藏，待操作完成后再重新恢复；
        使用DocumentFragment / cloneNode / replaceChild进行操作；
    使用事件委托，避免大量的事件绑定；

    css 优化:
        层级扁平，避免过于多层级的选择器嵌套；
        层级扁平，避免过于多层级的选择器嵌套；
        特定的选择器 好过一层一层查找:  .xxx-child-text{} 优于 .xxx .child .text{}
        减少使用通配符与属性选择器；
        减少不必要的多余属性；
        使用 动画属性 实现动画，动画时脱离文档流，开启硬件加速，优先使用 css 动画；
        使用 <link> 替代原生 @import；
    html 优化
        减少 dom 数量，避免不必要的节点或嵌套；
        避免<img src="" />空标签，能减少服务器压力，因为 src 为空时，浏览器仍然会发起请求
        图片提前 指定宽高 或者 脱离文档流，能有效减少因图片加载导致的页面回流；
        语义化标签 有利于 SEO 与浏览器的解析时间；
        减少使用 table 进行布局，避免使用<br />与<hr />;
    页面基础优化
        引入位置: css 文件<head>中引入， js 文件<body>底部引入
        减少请求 (http 1.0 - 1.1)，合并请求，正确设置 http 缓存
        小图片合成 雪碧图，低于 5K 的图片可以转换成 base64 内嵌；
        合适场景下，使用 iconfont 或者 svg
    使用缓存:
        浏览器缓存: 通过设置请求的过期时间，合理运用浏览器缓存
        CDN缓存: 静态文件合理使用 CDN 缓存技术
        打包后的图片 / js / css 等资源上传到 CDN 上，文件带上 hash 值；
        服务器缓存: 将不变的数据、页面缓存到 内存 或 远程存储(redis等) 上；
        数据缓存: 通过各种存储将不常变的数据进行缓存，缩短数据的获取时间；
    首屏渲染优化
        css / js 分割，使首屏依赖的文件体积最小，内联首屏关键 css / js
        非关键性的文件尽可能的 异步加载和懒加载，避免阻塞首页渲染；
        使用dns-prefetch / preconnect / prefetch / preload等浏览器提供的资源提示，加快文件传输；
        重要的元素优先渲染；视窗内的元素优先渲染；
    服务端渲染(SSR)
    优化用户感知
        利用一些动画 过渡效果，能有效减少用户对卡顿的感知；
        尽可能利用 骨架屏(Placeholder) / Loading 等减少用户对白屏的感知；
        动画帧数尽量保证在 30帧 以上，低帧数、卡顿的动画宁愿不要；
        js 执行时间避免超过 100ms，超过的话就需要做
```