---
title: React面试-1
date:
updated:
type: "tags"
comments:
categories: 面试
description: React面试-1
keywords: React面试-1
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2431606259,2554064138&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

# 1.react生命周期
### 1.第一个是组件初始化(initialization)阶段
```js
第一个是组件初始化(initialization)阶段
也就是以下代码中类的构造方法( constructor() ),Test类继承了react Component这个基类，也就继承这个react的基类，才能有render(),生命周期等方法可以使用，这也说明为什么函数组件不能使用这些方法的原因。
super(props)用来调用基类的构造方法( constructor() ), 也将父组件的props注入给子组件，功子组件读取(组件中props只读不可变，state可变)。
而constructor()用来做一些组件的初始化工作，如定义this.state的初始内容

import React, { Component } from 'react';
class Test extends Component {
  constructor(props) {
    super(props);
  }
}
```
### 2.第二个是组件的挂载(Mounting)阶段。此阶段分为componentWillMount，render，componentDidMount三个时期
```js
componentWillMount:在组件挂载到DOM前调用，且只会被调用一次，在这边调用this.setState不会引起组件重新渲染，也可以把写在这边的内容提前到constructor()中，所以项目中很少用。
render:不能在里面执行this.setState，会有改变组件状态的副作用。
componentDidMount:组件挂载到DOM后调用，且只会被调用一次
```
### 3.第三个是组件的更新(update)阶段
```js
setState引起的state更新或父组件重新render引起的props更新，更新后的state和props相对之前无论是否有变化，都将引起子组件的重新render。
造成组件更新有两类（三种）情况：
1.父组件重新render
2.组件本身调用setState，无论state有没有变化。可通过shouldComponentUpdate方法优化。
此阶段分为componentWillReceiveProps，shouldComponentUpdate，componentWillUpdate，render，componentDidUpdate
1.componentWillReceiveProps(nextProps):所以在此方法中根据nextProps和this.props来查明重传的props是否改变，以及如果改变了要执行啥.此方法只调用于props引起的组件更新过程中，响应 Props 变化之后进行更新的唯一方式，参数nextProps是父组件传给当前组件的新props
2.shouldComponentUpdate(nextProps, nextState):此方法通过比较nextProps，nextState及当前组件的this.props，this.state，返回true时当前组件将继续执行更新过程，返回false则当前组件更新停止，以此可用来减少组件的不必要渲染，优化组件性能。
3.componentWillUpdate(nextProps, nextState) 此方法在调用render方法前执行，在这边可执行一些组件更新发生前的工作，一般较少用。
4.componentDidUpdate(prevProps, prevState)此方法在组件更新后被调用，可以操作组件更新的DOM，prevProps和prevState这两个参数指的是组件更新前的props和state
```

### 4.卸载阶段
```js
componentWillUnmount 此方法在组件被卸载前调用，可以在这里执行一些清理工作，比如清楚组件中使用的定时器，清楚componentDidMount中手动创建的DOM元素等，以避免引起内存泄漏。
```

# 2.Setstate机制
```js
setState是react的一步操作，每次调用setState都会触发更新，异步操作是为了提高性能，将多个状态合并一起更新，减少re-render调用，
实现两个功能:
    1.异步更新state，将短时间内的多个setState合并成一个
    2.为了解决异步更新导致的问题，增加另一种形式的setState：接受一个函数作为参数，在函数中可以得到前一个状态并返回下一个状态
    this.setState({
      msg: "我被改变了"
    },()=>{
        //回调函数
    });

    this.setState(state => ({ msg: "hello world" }));
```

# 3.React和Vue区别和相似点
```js
相似点
    1.Virtual DOM
    2.组件化
    3.Props
    4.构建工具
    5.Chrome 开发工具
    6.配套框架
区别
    1.模板 vs JSX
    2.状态管理 vs 对象属性
    3.React Native vs Weex
    4.监听数据变化的实现原理不同 这是因为Vue和React设计理念上的区别，Vue使用的是可变数据，而React更强调数据的不可变，两者没有好坏之分，Vue更加简单，而React构建大型应用的时候更加鲁棒。
    5.React单向数据流,Vue双向绑定
    6.渲染过程 React在应用的状态被改变时，全部子组件都会重新渲染。通过shouldComponentUpdate这个生命周期方法可以进行控制，但Vue将此视为默认的优化。如果应用中交互复杂，需要处理大量的UI变化，那么使用Virtual DOM是一个好主意。如果更新元素并不频繁，那么Virtual DOM并不一定适用，性能很可能还不如直接操控DOM。
```

# 4.路由鉴权
```js
https://www.jb51.net/article/169346.htm
```

# 5.react项目中，constructor(){ this.target = this.func.bind(this); },JSX里onChange={this.target}的写法，为什么要比非bind的func = () => {}的写法效率高 请解释其中的原理
```js
bind之后锁定了上下文，不用向上查找
```
# 6.为什么 Vuex 的 mutation 和 Redux 的 reducer 中不能做异步操作
```js
应该是各自对于状态管理机制的一种涉及。vue和redux都是一种状态管理机制。 然后他们会有自己的state、和修改state的方法， 修改state的方法涉及到同步和异步，vuex的处理方式是同步在mutation里面，异步在actions里面，然后redux的同步就是reducer ，异步更多的是用户自己去通过中间件的方式去实现的把。 没写过redux 我只能理解到这里了。
单一数据源，也就是state
state 是只读，Redux并没有暴露出直接修改state的接口，必须通过action来触发修改
使用纯函数来修改state，reducer必须是纯函数
```

# 7.redux 为什么要把 reducer 设计成纯函数
```js
redux的设计思想就是不产生副作用，数据更改的状态可回溯，所以redux中处处都是纯函数
Redux三大原则
    单一数据流
        整个应用state都被储存在一个store里面 构成一个Object tree
    State是只读的
        唯一改变state的方法就是触发action, action是一个用于描述已发生事件的普通对象
    使用纯函数来执行修改
        为了描述action如何改变state tree， 你需要编写reducers
```

# 8.为什么列表循环渲染的key最好不要用index
```js
变化前数组的值是[1,2,3,4]，key就是对应的下标：0，1，2，3
变化后数组的值是[4,3,2,1]，key对应的下标也是：0，1，2，3
那么diff算法在变化前的数组找到key =0的值是1，在变化后数组里找到的key=0的值是4
因为子元素不一样就重新删除并更新
但是如果加了唯一的key,如下


变化前数组的值是[1,2,3,4]，key就是对应的下标：id0，id1，id2，id3
变化后数组的值是[4,3,2,1]，key对应的下标也是：id3，id2，id1，id0
那么diff算法在变化前的数组找到key =id0的值是1，在变化后数组里找到的key=id0的值也是1
因为子元素相同，就不删除并更新，只做移动操作，这就提升了性能
```

# 9.redux异步中间件之间的优劣?
```js
redux-thunk优点:

体积小: redux-thunk的实现方式很简单,只有不到20行代码
使用简单: redux-thunk没有引入像redux-saga或者redux-observable额外的范式,上手简单

redux-thunk缺陷:

样板代码过多: 与redux本身一样,通常一个请求需要大量的代码,而且很多都是重复性质的
耦合严重: 异步操作与redux的action偶合在一起,不方便管理
功能孱弱: 有一些实际开发中常用的功能需要自己进行封装

redux-saga优点:

异步解耦: 异步操作被被转移到单独 saga.js 中，不再是掺杂在 action.js 或 component.js 中
action摆脱thunk function: dispatch 的参数依然是一个纯粹的 action (FSA)，而不是充满 “黑魔法” thunk function
异常处理: 受益于 generator function 的 saga 实现，代码异常/请求失败 都可以直接通过 try/catch 语法直接捕获处理
功能强大: redux-saga提供了大量的Saga 辅助函数和Effect 创建器供开发者使用,开发者无须封装或者简单封装即可使用
灵活: redux-saga可以将多个Saga可以串行/并行组合起来,形成一个非常实用的异步flow
易测试，提供了各种case的测试方案，包括mock task，分支覆盖等等

redux-saga缺陷:

额外的学习成本: redux-saga不仅在使用难以理解的 generator function,而且有数十个API,学习成本远超redux-thunk,最重要的是你的额外学习成本是只服务于这个库的,与redux-observable不同,redux-observable虽然也有额外学习成本但是背后是rxjs和一整套思想
体积庞大: 体积略大,代码近2000行，min版25KB左右
功能过剩: 实际上并发控制等功能很难用到,但是我们依然需要引入这些代码
ts支持不友好: yield无法返回TS类型

redux-observable优点:

功能最强: 由于背靠rxjs这个强大的响应式编程的库,借助rxjs的操作符,你可以几乎做任何你能想到的异步处理
背靠rxjs: 由于有rxjs的加持,如果你已经学习了rxjs,redux-observable的学习成本并不高,而且随着rxjs的升级redux-observable也会变得更强大

redux-observable缺陷:

学习成本奇高: 如果你不会rxjs,则需要额外学习两个复杂的库
社区一般: redux-observable的下载量只有redux-saga的1/5,社区也不够活跃,在复杂异步流中间件这个层面redux-saga仍处于领导地位
```
# 10.请简单谈一下react的事件机制
```js
当用户在为onClick添加函数时，React并没有将Click时间绑定在DOM上面。
而是在document处监听所有支持的事件，当事件发生并冒泡至document处时，React将事件内容封装交给中间层SyntheticEvent（负责所有事件合成）
所以当事件触发的时候，对使用统一的分发函数dispatchEvent将指定函数执行。


```