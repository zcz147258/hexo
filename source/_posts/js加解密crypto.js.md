---
title: js加解密
date:
updated:
type: "tags"
categories: JavaScript
comments:
description: js加解密
keywords: js加解密
cover: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=4234896097,4021899470&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

```js
/*
 * @Descripttion: 
 * @Author: sueRimn
 * @Date: 2020-07-11 11:31:25
 */ 
//加密
const CryptoJS = require('crypto-js');  //引用AES源码js
const key = CryptoJS.enc.Utf8.parse("1234123412ABCDEF");  //十六位十六进制数作为密钥
const iv = CryptoJS.enc.Utf8.parse('ABCDEF1234123412');   //十六位十六进制数作为密钥偏移量
function encrypt(word) {
    let encrypted = "";
    if (typeof word == "string") {
      const srcs = CryptoJS.enc.Utf8.parse(word);
      encrypted = CryptoJS.AES.encrypt(srcs, key, {
        iv: iv,
        mode: CryptoJS.mode.CBC,
        padding: CryptoJS.pad.Pkcs7
      });
    } else if (typeof word == "object") {
      //对象格式的转成json字符串
      const data = JSON.stringify(word);
      const srcs = CryptoJS.enc.Utf8.parse(data);
      encrypted = CryptoJS.AES.encrypt(srcs, key, {
        iv: iv,
        mode: CryptoJS.mode.CBC,
        padding: CryptoJS.pad.Pkcs7
      });
    }
    return encrypted.ciphertext.toString();
  }
  // aes解密
function decrypt(word) {
  if(word){
    const encryptedHexStr = CryptoJS.enc.Hex.parse(word);
    const srcs = CryptoJS.enc.Base64.stringify(encryptedHexStr);
    const decrypt = CryptoJS.AES.decrypt(srcs, key, {
      iv: iv,
      mode: CryptoJS.mode.CBC,
      padding: CryptoJS.pad.Pkcs7
    });
    const decryptedStr = decrypt.toString(CryptoJS.enc.Utf8);
    return decryptedStr.toString();
  }
  }
export default {
    decrypt,
    encrypt
}
```