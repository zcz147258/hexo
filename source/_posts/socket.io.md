---
title: nodejs-socket.io
date:
updated:
type: "tags"
categories: Node
comments:
description: nodejs-socket.io
keywords: nodejs-socket.io
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=4068303333,250769197&fm=11&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
原生
```js

//服务端
const ws = require('nodejs-websocket')

let count = 0 //记录当前用户数量
const server =  ws.createServer(connect =>{
    count++
    connect.userName = `用户${count}` 
    broadcast(`${connect.userName}进入了聊天室`)
    connect.on('text',data =>{
      // connect.send(data)
      broadcast(data)
    })
    connect.on('close',data =>{
      connect.send('连接已关闭')
      count--
      broadcast(`${connect.userName}推出了聊天室`)
    })
    connect.on('error',() =>{
      console.log('用户链接异常')
      count--
      // broadcast(`${connect.userName}推出了聊天室`)
    })
})

//广播
function broadcast(msg){
  server.connections.forEach(item=>{
    item.send(msg)
  })
}
server.listen(3000,()=>{
  console.log('websocket 启动成功')
})

//客户端
<!--
 * @Descripttion: 
 * @Author: mikasa
 * @Date: 2020-09-25 15:36:52
-->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    div{
      width: 200px;
      height: 200px;
      border: 1px solid #000;
    }
  </style>
</head>
<body>
  <input type="text" placeholder="请输入内容">
  <button>发送请求</button>
  <div></div>

  <script>
     var input = document.querySelector('input')
     var button = document.querySelector('button')
     var div = document.querySelector('div')

     var socket = new WebSocket('ws://localhost:3000')

     socket.addEventListener('open',function(){
        div.innerHTML = '连接服务器成功' + '<br/>'
     })
     button.addEventListener('click',function(){
       var value = input.value
       socket.send(value)
     })

     socket.addEventListener('message',function(e){
        console.log(e.data)
       div.innerHTML += e.data+'<br/>'
     })

     socket.addEventListener('close',function(){

     })

  </script>
</body>
</html>
```

socket io

```js
//服务端
var app = require('http').createServer(handler)
var io = require('socket.io')(app)
var fs = require('socket.io')

app.listen(3000)

function handler(){

}

io.on('connection',socket=>{
    console.log('新用户连接了')

    socket.on('hehe',data =>{
        socket.emit('send',data)
    })
})

//客户端
 <script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/2.3.0/socket.io.js"></script>
    <script>
        const socket = io('http://localhost:3000');
        //接收服务器返回的数据
        socket.on('send',data=>{
            console.log(data)
        })

        socket.emit('hehe',{name:'zcz',age:20})
    </script>
```