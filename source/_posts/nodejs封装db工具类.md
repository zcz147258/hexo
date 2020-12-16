---
title: nodejs封装db工具类
date:
updated:
type: "tags"
categories: Node
comments:
description: nodejs封装db工具类
keywords: nodejs封装db工具类
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=4068303333,250769197&fm=11&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

操作mongon 使用mongoose模块
```js
//作用链接数据库
const mongoose = require("mongoose");
mongoose.set('useCreateIndex', true)
mongoose.connect(
  "mongodb://adminroot:xxxxx@xxxxxxx:27017/blog?authSource=admin",
  { useNewUrlParser: true, useUnifiedTopology: true }
);
mongoose.connection.on('error', () => {
    console.log('连接数据库失败')
  });
  mongoose.connection.on('open', () => {
    console.log('链接数据库成功')
  });

module.exports = mongoose
```