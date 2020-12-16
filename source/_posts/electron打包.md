---
title: Electron
date:
updated:
type: "tags"
categories: electron
comments:
description: Electron开发桌面应用
keywords: Electron,Vue,JS
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=4068303333,250769197&fm=11&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
electron打包
```js
cnpm install electron-packager -g
cd到electron-quick-start文件夹，执行如下最简单的命令，即可开始打包。

命令行打包参数：

electron-packager <location of project> <name of project> <platform> <architecture> <electron version> <optional options>

参数说明： 
* location of project：项目所在路径 
* name of project：打包的项目名字 
* platform：确定了你要构建哪个平台的应用（Windows、Mac 还是 Linux） 
* architecture：决定了使用 x86 还是 x64 还是两个架构都用 
* electron version：electron 的版本 
* optional options：可选选项
```
