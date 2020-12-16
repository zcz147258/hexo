---
title: 计算机网络
date:
updated:
type: "tags"
categories: 计算机网络
comments:
description: Http状态码
keywords: Http状态码
cover: https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=283932388,350254066&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

# 2XX(Success 成功状态码)
200 OK 表示从客户端发来的请求在服务器端被正常处理了
204 请求成功,但是没有资源可以返回 一般在只需要从客户端往服务器发送信息，而对客户端不需要发送新信息内容的情况下使用
206 对资源某一部分的请求 该状态码表示客户端进行了范围请求，而服务器成功执行了这部分的 GET 请求
响应报文中包含由 Content-Range 指定范围的实体内容

# 3XX(Redirection 重定向状态码)
301 永久性重定向
302 临时性重定向
303 该状态码表示由于请求对应的资源存在着另一个 URI，应使用 GET 方法定向获取请求的资源。
304 附带条件的请求是指采用 GET 方法的请求报文中包含 If-Match，If-Modified-Since，If-None-Match，If-Range，If-Unmodified-Since 中任一首部
307 临时重定向。该状态码与 302 Found 有着相同的含义。尽管 302 标准禁止 POST 变换成 GET，但实际使用时大家并不遵守

# 4XX(Client Error 客户端错误状态码)
400 Bad Request 该状态码表示请求报文中存在语法错误
401 Unauthorized 用户认证失败
403 Forbidden 该状态码表明对请求资源的访问被服务器拒绝了
404 该状态码表明服务器上无法找到请求的资源
405 Method Not Allowed 但是服务器禁止使用该方法

# 5XX(Server Error 服务器错误状态码)
500 Internal Server Error 服务器端在执行请求时发生了错误
502 Bad Gateway 502 错误通常不是客户端能够修复的，而是需要由途径的 Web 服务器或者代理服务器对其进行修复
503 Service Unavailable 该状态码表明服务器暂时处于超负载或正在进行停机维护，现在无法处理请求