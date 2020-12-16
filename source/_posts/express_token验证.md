---
title: express_token验证
date:
updated:
type: "tags"
comments:
categories: Node
description: express_token验证
keywords: express_token验证
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=3023339532,6928380&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

token验证工具类
```js
/*
 * @Descripttion: token验证类
 * @Author: mikasa
 * @Date: 2020-07-15 17:57:37
 */ 
const jwt = require('jsonwebtoken')
const path = require('path')
const fs = require('fs')

// 创建 token 类
class Jwt {
    constructor(data) {
        this.data = data
    }
    //生成token
    generateToken() {
        let data = this.data
        let created = Math.floor(Date.now() / 1000)
        let cert = fs.readFileSync(path.join(__dirname, './pem/rsa_private_key.pem')) // 私钥
        let token = jwt.sign({
            data,
            exp: created + 60 * 60,
        }, cert, {algorithm: 'RS256'})
        return token
    }
    // 校验token
    verifyToken() {
        let token = this.data
        let cert = fs.readFileSync(path.join(__dirname, './pem/rsa_public_key.pem')) // 公钥
        let res
        try {
            let result = jwt.verify(token, cert, {algorithms: ['RS256']}) || {}
            let {exp = 0} = result, current = Math.floor(Date.now() / 1000)
            if (current <= exp) {
                res = result.data || {}
            }
        } catch (e) {
            res = 'err'
        }
        return res
    }
}
module.exports = Jwt
```

express验证中间件
```js
let Jwt = require('./utils/token')
app.post('/notescan',(req,res)=>{
  let fileid = req.body.fileid;
  const cr = fs.createReadStream(`/root/upload/md/${fileid}`,{
    // highWaterMark:3, //文件一次读多少字节,默认 64*1024
    flags:'r', //默认 'r'
    autoClose:true, //默认读取完毕后自动关闭
    // start:0, //读取文件开始位置
    // end:3, //流是闭合区间 包含start也含end
    encoding:'utf8' //默认null
  })
  cr.on('error',(err)=>{
    res.send(err)
  })
  cr.pipe(res);
})
//token验证中间件
app.use((req, res, next) => {
  const Uri = url.parse(req.url)
  const baseurl = Uri.pathname
  if (baseurl !== '/' && baseurl !== '/login'
   && baseurl !== '/user/email'
   && baseurl !== '/user/add'
   && baseurl !== '/user/userinfoVisit'
   && baseurl !== '/user/recommend'
   && baseurl !== '/note/allNoteVisit'
   && baseurl !== '/note/notedetailvisit'
   && baseurl !== '/note/view'
   && baseurl !== '/blog/single'
   && baseurl !== '/blog/hotall'
   && baseurl !== '/blog/view'
   && baseurl !== '/blog/tagname'
   && baseurl !== '/blog/tagsum'
   && baseurl !== '/blog/hot'){
    let token = req.headers.authorization
    let jwt = new Jwt(token)
    let result = jwt.verifyToken()
    //解析出result
    if (result === 'err') {
        res.send(401,{msg: '请求未授权，请重新登录'})
    } else {
      global.token = result
        next()
    }
  }else{
    next()
  }
})
```