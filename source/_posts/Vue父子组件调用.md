---
title: Vue父子组件调用
date:
updated:
type: "tags"
comments:
categories: Vue
description: Vue父子组件调用
keywords: Vue父子组件调用
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=22130535,2850036426&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

父组件调用子组件方法
```js
//子组件方法
methods: {
      childClick(e) {
        console.log(e)
      }
    }
//父组件方法
<search-swiper
    ref="mychild"
    @myevent="passdata(arguments)"
    :infoList="infoList"
    :tabIndex="tabIndex"
    v-if="infoList.length"
    :tabList="tabList"
    :safeHeight="safeHeight"
    :filter="filter"></search-swiper>

//uniapp
onReachBottom(){
this.$refs.mychild.childonReachBottom()
},
```

子组件调用父组件方法
```js
//方法1
//父组件方法
fatherMethod() {
        console.log('测试');
}
//子组件
  <button @click="childMethod()">点击</button>
  methods: {
      childMethod() {
        this.$parent.fatherMethod();
      }
    }

//第二种方法
//组件传值
//第二种方法是在子组件里用$emit向父组件触发一个事件，父组件监听这个事件就行了。
```