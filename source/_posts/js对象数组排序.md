---
title: js对象数组排序
date:
updated:
type: "tags"
categories: JavaScript
comments:
description: js对象数组排序
keywords: js对象数组排序
cover: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=4234896097,4021899470&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

```js
compare(key) {
      return function (a, b) {
        var value1 = a[key];
        var value2 = b[key];
        return value1 - value2;
      };
    },
let result = res.data.sort(this.compare('parentId'));
```