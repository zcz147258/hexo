---
title: Vue面试-1
date:
updated:
type: "tags"
comments:
categories: 面试
description: Vue面试-1
keywords: Vue面试-1
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=22130535,2850036426&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

# 1.MVVM数据劫持
```js
    var data = {
  name: 'evenyao',
  list: [1, 2, 3]
}
observe(data)

function observe(data) {
  if(!data || typeof data !== 'object') return
  for(let key in data) {
    let val = data[key]
    Object.defineProperty(data, key, {
      enumerable: true,
      configurable: true,
      get: function() {
        console.log(`get ${val}`)
        return val
      },
      set: function(newVal) {
        console.log(`changes happen: ${val} => ${newVal}`)
        val = newVal
      }
    })
    // 如果 val 也为对象 递归
    if(typeof val === 'object') {
      observe(val)
    }
  }
}

```

# 2.几种实现双向绑定的做法
```js
在检查数据变化的时候,由于你并不知道这个事件是对哪些数据进行了更改，以及这个事件有可能造成事件之外的其他任何地方的数据更改,所以必须进行一次大检查，将所有“注册”过的值全部检查一遍，一次检查称为一个周期,每次最少检查两遍，因为第二遍用来确认，前一遍的变动中是否有数据的变动，导致了其他数据的变动，如果第二次有变动的话，会再执行一遍，直到最后两次完全一致，则停止检查（其实就是个（递归（遍历））的过程），考虑到内存的消耗和死循环的风险，脏检查每个周期最多递归执行10遍，所以在程序结构设计中，尽量避免数据与数据之间的紧耦合；
```

# 3.Vue中computed和watch的区别
```js
1.watch擅长处理的场景：一个数据影响多个数据
2.computed擅长处理的场景：一个数据受多个数据影响
对于任何复杂逻辑，你都应当使用计算属性。
计算属性是基于它们的响应式依赖进行缓存的。只在相关响应式依赖发生改变时它们才会重新求值。
```
```js
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```
Vue 通过 watch 选项提供了一个更通用的方法，来响应数据的变化。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。
```js
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```

# 4.对于MVVM的理解
```js
MVVM 是 Model-View-ViewModel 的缩写
Model: 代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑。我们可以把Model称为数据层，因为它仅仅关注数据本身，不关心任何行为
View: 用户操作界面。当ViewModel对Model进行更新的时候，会通过数据绑定更新到View
ViewModel： 业务逻辑层，View需要什么数据，ViewModel要提供这个数据；View有某些操作，ViewModel就要响应这些操作，所以可以说它是Model for View.
总结： MVVM模式简化了界面与业务的依赖，解决了数据频繁更新。MVVM 在使用当中，利用双向绑定技术，使得 Model 变化时，ViewModel 会自动更新，而 ViewModel 变化时，View 也会自动变化。
```

# 5.Eventloop深入理解
第一道题
```js
// => 代码一执行就开始执行了一个宏任务-宏0
console.log('script start'); 

setTimeout(() => { // 宏 1
  console.log('北歌');
}, 1 * 2000);

Promise.resolve()
    .then(function() { // 微1-1
      console.log('promise1');
    })
    .then(function() { // 微1-4 => 这个then中的会等待上一个then执行完成之后得到其状态才会向Queue注册状态对应的回调，假设上一个then中主动抛错且没有捕获，那就注册的是这个then中的第二个回调了。
      console.log('promise2'); 
    });


async function foo() {
  await bar() // => await(promise的语法糖)，会异步等待获取其返回值
  // => 后面的代码可以理解为放到异步队列微任务中。 这里可以保留疑问后面会详细说
  console.log('async1 end') // 微1-2
}
foo()

function bar() {
  console.log('async2 end') 
}

async function errorFunc () {
  try {
    await Promise.reject('error!!!')
  } catch(e) {
      // => 从这后面开始所有的代码可以理解为放到异步队列微任务中
    console.log(e)  // 微1-3
  }
  console.log('async1');
  return Promise.resolve('async1 success')
}
errorFunc().then(res => console.log(res)) // 微1-5

console.log('script end');
//
```
第二道题
```js
console.log('1');

setTimeout(() => {
  console.log('2');
  Promise.resolve().then(() => {
    console.log('3');
  })
  new Promise((resolve) => {
    console.log('4');
    resolve();
  }).then(() => {
    console.log('5')
  })
})

Promise.reject().then(() => {
  console.log('13');
}, () => {
  console.log('12');
})

new Promise((resolve) => {
  console.log('7');
  resolve();
}).then(() => {
  console.log('8')
})

setTimeout(() => {
  console.log('9');
  Promise.resolve().then(() => {
    console.log('10');
  })
  new Promise((resolve) => {
    console.log('11');
    resolve();
  }).then(() => {
    console.log('12')
  })
})
```
第三道题
```js
new Promise((resolve, reject) => {
    console.log(1)
    resolve()
  })
  .then(() => {
    console.log(2)
    new Promise((resolve, reject) => {
        console.log(3)
        setTimeout(() => {
          reject();
        }, 3 * 1000);
        resolve()
    })
      .then(() => {
        console.log(4)
        new Promise((resolve, reject) => {
            console.log(5)
            resolve();
          })
          .then(() => {
            console.log(7)
          })
          .then(() => {
            console.log(9)
          })
      })
      .then(() => {
        console.log(8)
      })
  })
  .then(() => {
    console.log(6)
  })
```
第四道题
```js
Promise.resolve()
  .then(() => {
    console.log('promise1');
    return new Promise((resolve, reject) => {
        setTimeout(() => {
          console.log('timer2')
          resolve()
        }, 0)
    })
      .then(async () => {
        await foo();
        return new Error('error1')
      })
      .then((ret) => {
        setTimeout(() => {
          console.log(ret);
          Promise.resolve()
          .then(() => {
            return new Error('error!!!')
          })
          .then(res => {
            console.log("then: ", res)
          })
          .catch(err => {
            console.log("catch: ", err)
          })
        }, 1 * 3000)
      }, err => {
        console.log(err);
      })
      .finally((res) => {
        console.log(res);
        throw new Error('error2')
      })
      .then((res) => {
        console.log(res);
      }, err => {
        console.log(err);
      })
  })
  .then(() => {
    console.log('promise2');
  })

function foo() {
  setTimeout(() => { 
    console.log('async1');
  }, 2 * 1000);
}

setTimeout(() => {
  console.log('timer1')
  Promise.resolve()
    .then(() => {
      console.log('promise3')
    })
}, 0)

console.log('start');
```

第五道
```js
async function async1() {
  console.log('async1 start');
  new Promise((resolve, reject) => {
    try {
      throw new Error('error1')
    } catch(e) {
      console.log(e);
    }
    setTimeout(() => { // 宏3
      resolve('promise4')
    }, 3 * 1000);
  })
    .then((res) => { // 微3-1
      console.log(res);
    }, err => {
      console.log(err);
    })
    .finally(res => { // 微3-2 // TODO注3
      console.log(res);
    })
  console.log(await async2()); // TODO-注1
  console.log('async1 end'); // 微1-1 // TODO-注2
}

function async2() {
  console.log('async2');
  return new Promise((resolve) => {
    setTimeout(() => { // 宏4
      resolve(2)
    }, 1 * 3000);
  })
}

console.log('script start');

setTimeout(() => { // 宏2
  console.log('setTimeout');
}, 0)

async1();

new Promise((resolve) => {
  console.log('promise1');
  resolve();
})
  .then(() => { // 微1-2
    console.log('promise2');
    return new Promise((resolve) => {
      resolve()
    })
      .then(() => { // 微1-3
        console.log('then 1-1')
      })
  })
  .then(() => { // 微1-4
    console.log('promise3');
  })


console.log('script end');
```

# 6.hash模式 和 history模式
```js
在浏览器中符号“#”，#以及#后面的字符称之为hash，用window.location.hash读取；
特点：hash虽然在URL中，但不被包括在HTTP请求中；用来指导浏览器动作，对服务端安全无用，hash不会重加载页面。
hash 模式下，仅 hash 符号之前的内容会被包含在请求中，如 http://www.xiaogangzai.com，因此对于后端来说，即使没有做到对路由的全覆盖，也不会返回 404 错误。
```

# 7.Vue 的响应式原理中 Object.defineProperty 有什么缺陷？为什么在 Vue3.0 采用了 Proxy，抛弃了 Object.defineProperty？
```js
1.Object.defineProperty无法监控到数组下标的变化，导致通过数组下标添加元素，不能实时响应；
2.Object.defineProperty只能劫持对象的属性，从而需要对每个对象，每个属性进行遍历，如果，属性值是对象，还需要深度遍历。Proxy可以劫持整个对象，并返回一个新的对象。
3.Proxy不仅可以代理对象，还可以代理数组。还可以代理动态增加的属性。
```