---
title: generator和iterator
date:
updated:
type: "tags"
categories: JavaScript
comments:
description: generator和iterator
keywords: generator和iterator
cover: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=4234896097,4021899470&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

```js
// 1. 迭代器

let iterator = (items)=>{
  let iter = {
    index:0,
    max:items.length,
    next:function(){ // 返回调用结果
      return this.index === this.max ? {value:undefined,done:true} : {value:items[this.index++],done:false};
    }
  }

  return iter;
}

export default iterator;

//调用上面的迭代器，并执行
let iter = iterator([1,2,3,4]);
let result = null;
console.log('``````iterator````````');
do{
  result = iter.next();
  console.log(result);
}while (!result.done)
可以看到，迭代器每次调用next()方法，都会返回{value:xx,done:xx}结构的对象，这个就是迭代器协议中next()方法需要遵循的规则，前面说过generator函数也是遵循迭代器协议的，下面用generator实现此功能。
```

```js
//generator
function *generator(items){
  let index = 0;
  let max = items.length;

  while (index < max){
    yield items[index++];
  }

}

let gene = generator([1,2,3,4]);
result = null;
console.log('``````````generator`````````');
do{
  result = gene.next();
  console.log(result)
}while(!result.done)
对比两次运行的结果，得出一个结论：生成器(function*)函数，运行时，返回的是一个生成器对象，这个生成器对象是可以迭代(gene.next())的，并且next()的返回值包含value，done两个字段。
```


