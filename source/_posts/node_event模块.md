---
title: nodejs_event模块
date:
updated:
type: "tags"
categories: Node
comments:
description: nodejs_event模块
keywords: nodejs_event模块
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=4068303333,250769197&fm=11&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

```js
var Event = require("events").EventEmitter; 
var ev = new Event(); //实例化events
事件1
    ev.once("error", function () {
      return;
    });
    ev.once("FindId",  function () {
       User.findByName(username, function (err, docs) {
        if (err) {
          emitter.emit("error");
        }
        var arr = docs[0].resource;
        var length = arr.length;
        console.log(length)
        arr.forEach((id) => {
          ev.emit("findInfo", id, length);
        });
      });
    });
    //事件2
    ev.on("findInfo", function (id, length) {
      Resource.findAuthority(id, function (err, docs) {
        if (err) {
          emitter.emit("error");
        }
        obj.info.push(docs[0]);
        ev.emit("getinfo", length);
      });
    });
    ev.on("getinfo", function (length) {
      try {
        if (obj.info.length == length) {
          ev.removeAllListeners();
          return res.send(obj);
        } else {
          return;
        }
      } catch (e) {}
    });
    ev.emit("FindId");
```