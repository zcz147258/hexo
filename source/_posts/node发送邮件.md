---
title: nodejs发送邮件
date:
updated:
type: "tags"
categories: Node
comments:
description: nodejs发送邮件
keywords: nodejs发送邮件
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=4068303333,250769197&fm=11&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

封装工具类
```js
const nodemailer = require('nodemailer')

var path=require('path');
var mailTransport = nodemailer.createTransport({
    // host : 'smtp.exmail.qq.com',
    service:'qq',
    secureConnection: true, // 使用SSL方式（安全方式，防止被窃取信息）
    secure: true,
    port:465,
    auth : {
        user : '1092283755@qq.com',
        pass : 'owegztbndnfmgcii'
    },
});


function mail(tos,str) {
    return new Promise((resolve,reject)=>{
        mailTransport.sendMail({
            from    : '1092283755@qq.com',
            to      : tos,
            subject : '三笠博客验证',//邮件主题
            html    : '<h1>你好，这是一封来自三笠博客的邮件！验证码为' + str + '</h1><p><img src="cid:00000001"/></p>',
            attachments :[
                    {
                        filename: 'emial.jpg',            // 改成你的附件名
                        path: path.join(__dirname,'../')+'/public/images/email.jpg',  // 改成你的附件路径
                        cid : '00000001'               // cid可被邮件使用
                    }
            ]
        }, function(err, res) {
            if (err){
                console.log('err')
                err = '发送错误'
                resolve(err)
            }else{
                console.log('success')
                reject(res)
                global.emailcode = str
            }
        });
    })
}
async function sendMail(tos){
        var a = [1,2,3,4,5,6,7,8,9,0]
        var str = ''
        var result = ''
        for (let index = 0; index < 6; index++) {
            const num = Math.floor((Math.random()*10))
            str += a[num]
        }
        await mail(tos,str).then(res=>{
            result = res
        }).catch(err=>{
            result = err
        })
        return result;
}
module.exports = sendMail
```

使用工具类
```js
const sendMail = require("../utils/email");
router.get("/email", (req, res) => {
  let email = req.param("email");
  if (email) {
    let result = sendMail(email).then((resopnse) => {
      res.send(resopnse);
    });
  } else {
    res.send("请输入邮箱");
  }
});
```