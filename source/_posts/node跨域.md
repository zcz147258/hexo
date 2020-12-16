---
title: nodejs跨域
date:
updated:
type: "tags"
categories: Node
comments:
description: nodejs跨域
keywords: nodejs跨域
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=4068303333,250769197&fm=11&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

```js
var app = express();
//设置允许跨域访问该服务.
app.all('*', function (req, res, next) {
    res.header("Access-Control-Allow-Origin", "*");
    res.header('Access-Control-Allow-Methods', 'PUT, GET, POST, DELETE, OPTIONS');
    // res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // res.header('Access-Control-Allow-Headers', 'Content-Type');
    res.setHeader('Access-Control-Allow-Headers','Content-Type,Access-Control-Allow-Headers,Authorization,X-Requested-With')
    if(req.method=="OPTIONS"){
      res.send(200)
    }else{
      next();
    }
});
```