---
title: Electron
date:
updated:
type: "tags"
categories: electron
comments:
description: Electron开发桌面应用
keywords: Electron,Vue,JS
top_img: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=4068303333,250769197&fm=11&gp=0.jpg
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=4068303333,250769197&fm=11&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
<!-- <div class="aplayer no-destroy" data-id="000PeZCQ1i4XVs" data-server="tencent" data-type="artist" data-fixed="true" data-mini="true" data-listFolded="false" data-order="random" data-preload="none" data-autoplay="true" muted></div> -->

# 1.介绍

使用 JavaScript，HTML 和 CSS 构建跨平台的桌面应用程序

官网 

> https://www.electronjs.org/
>
> 构建的软件 Vscode Twitch  Figma WhatsApp 
>
> 如果你可以建一个网站，你就可以建一个桌面应用程序。 Electron 是一个使用 JavaScript, HTML 和 CSS 等 Web 技术创建原生程序的框架，它负责比较难搞的部分，你只需把精力放在你的应用的核心上即可。

# 2.开发环境搭建

```js
cnpm i electron --save-dev  //下载
npx electron -v  //检测版本
electron . //启动应用
```

## Helloword

```js
//main.js
var electron = require('electron')

var app = electron.app //引用app
var BrowserWindow = electron.BrowserWindow //窗口引用
var mainWindow = null //声明要打开的主窗口

app.on('ready',()=>{
    mainWindow = new BrowserWindow({width:300,height:300}) //设置主窗口大小
    mainWindow.loadFile('index.html') //加载html页面
    mainWindow.on('close',()=>{ // 监听关闭 释放内存
        mainWindow = null
    })
})
```

```
//运行流程  
//先找  package.json 
//找入口 main.js
//读取页面布局和演示
//主进程每一个分支都是渲染程序
```

```js
//调用 node api
mainWindow = new BrowserWindow({
	width:800,
	height:800,
	webPreferences:{nodeIntegration:true}//启动nodeapi可以使用
}) //设置主窗口大小
```

# 3.remote

```js
//渲染进程 新的页面
//webPreferences:{nodeIntegration:true,enableRemoteModule:true}//启动nodeapi可以使用

//渲染进程
const btn = this.document.querySelector('#btn')
const BrowserWindow = require('electron').remote.BrowserWindow
window.onload = (function(){
    btn.onclick = () =>{
        newWin = new BrowserWindow({
            width:500,
            height:500
        })
        newWin.loadFile('yellow.html')
        newWin.on('close',()=>{
            newWin = null
        })
    }
})
```

# 4.菜单制作

```js
//menu.js
const { Menu, BrowserWindow } = require("electron");
var template = [
  {
    label: "会所1",
    submenu: [
      {
        label: "精品spa",
        accelerator:'ctrl+n',//快捷键
        click: () => {
          var win = new BrowserWindow({
            width: 500,
            height: 500,
            webPreferences:{nodeIntegration:true}
          });
          win.loadFile('yellow.html')
          win.on('closed',()=>{
              win = null
          })
        },
      },
      { label: "按摩" },
    ],
  },
  {
    label: "大浪淘沙",
    submenu: [{ label: "牛奶玫瑰与" }, { label: "爱情拍手" }],
  },
];
var m = Menu.buildFromTemplate(template);

Menu.setApplicationMenu(m);


//在main.js 引入
app.on('ready',()=>{
    mainWindow = new BrowserWindow({
            width:800,
            height:800,
            webPreferences:{nodeIntegration:true,enableRemoteModule:true}//启动nodeapi可以使用
        }) //设置主窗口大小
    require('./main/menu')//引入Menu菜单
    mainWindow.loadFile('demo2.html') //加载html页面
    mainWindow.on('close',()=>{ // 监听关闭 释放内存
        mainWindow = null
    })
})


//mainWindow.webContents.openDevTools()  打开调试模式
```

# 5.右键菜单的制作

```js
//渲染进程 利用remote

//响应事件
//单一事件
window.addEventListener("click", function () {
  alert("左键点击");
});
//右击事件
const { remote } = require("electron");
//右击菜单模板
var rightTemplate = [
    {label:'粘贴',accelerator:'ctrl+v'},
    {label:'复制',accelerator:'ctrl+c'}
]
var m = remote.Menu.buildFromTemplate(rightTemplate)
window.addEventListener("contextmenu", function (e) {
  e.preventDefault(); //阻止冒泡
  m.popup({window:remote.getCurrentWindow()})
});

```

# 6.打开浏览器

```js
<button id="btn">打开新的窗口</button>
<a id="aHref" href="http://www.zczsylm.top">博客</a>
<script src="render/demo2.js"></script>

//打开浏览器
var aHref = document.querySelector('#aHref')
aHref.onclick = function(e){
    e.preventDefault()//阻止默认打开
    var href = this.getAttribute('href')
    shell.openExternal(href)
    
```

# 7.嵌入网页和打开子窗口

```js
//嵌入网页 类似broserview 
app.on('ready',()=>{
    mainWindow = new BrowserWindow({
            width:800,
            height:800,
            webPreferences:{nodeIntegration:true,enableRemoteModule:true}//启动nodeapi可以使用
        }) //设置主窗口大小
    //打开调试模式
    mainWindow.webContents.openDevTools()
    require('./main/menu')//引入Menu菜单

    var BrowserView = electron.BrowserView
    var view = new BrowserView()
    mainWindow.setBrowserView(view)
    view.setBounds({x:100,y:120,width:200,height:300})//设置样式
    view.webContents.loadURL('http://www.zczsylm.top')
    //

    mainWindow.loadFile('demo2.html') //加载html页面
    mainWindow.on('close',()=>{ // 监听关闭 释放内存
        mainWindow = null
    })
})


//打开子窗口
//打开子窗口
var openNew = document.querySelector('#mybtn')
openNew.onclick = function(e){
    window.open('http://www.zczsylm.top')
}
```

# 8.子窗口向父窗口通信

```js
//子窗口
var openNew = document.querySelector('#mybtn')
openNew.onclick = function(e){
    window.open('yellow.html')
}

//父窗口接受
//监听消息
window.addEventListener('message',function(msg){
    console.log(111)
    var content = document.querySelector('#mycontent')
    content.innerHTML = JSON.stringify(msg.data)
})


//只能是window.open才可以接受
```

# 9.选择文件，保存文件

```js
//文件对话  对应的渲染殷勤里面
const { dialog } = require('electron').remote
var bubbon = document.querySelector('#openpictrue')
bubbon.onclick = function(){
    dialog.showOpenDialog({
      title:'请选择',
      // defaultPath:''
      filters:[{name:'img',extensions:['jpg','png']}],
      buttonLabel:'打开选中'//button自定义
    }).then(res =>{
      let image = document.getElementById('imgs')
      image.setAttribute('src',res.filePaths[0])
    }).catch(e =>{
      alert('选择错误')
    })
}
//保存文件
var btn2 = document.getElementById('saveimg')
btn2.onclick = function(){
  dialog.showSaveDialog({
    title:'保存文件'
  }).then(res=>{
    alert(res)
  }).catch(err=>{
    alert(err)
  })
}

```

# 10.消息对话框

```js
//断网提醒
window.addEventListener('online',function(){
  alert('上线')
})

window.addEventListener('offline',function(){
  alert('断线')
})
```

# 11.底部消息通知

```js
var messagebtn2 = document.getElementById('messagebtn2')
var option = {
  title:'小儿,来订单了',
  body:'这里是订单内容'
}
messagebtn2.onclick = function(){
  new window.Notification(option.title,option)
}
```

# 12.全局快捷键

```js
//main.js
//全局快捷键
var globalShortcut = electron.globalShortcut
globalShortcut.register('ctrl+e',function(){
    mainWindow.loadURL('http://www.zczsylm.top')
})
let regist = globalShortcut.isRegistered('ctrl+e')?'success':'fail'
console.log(regist)
```

# 13.剪切板

```js
//复制激活码
const { clipboard } = require('electron')
var code = document.getElementById('code')
var copycon = document.getElementById('copycon')
copycon.onclick = function(){
  clipboard.writeText(code.innerHTML)
}
```

# 14.vue-electron

```js
vue init simulatedgreg/electron-vue my-project

//如果报错 process报错 
//在.electron-vue/webpack.renderer.config.js和.electron-vue/webpack.web.config.js文件中找//到HtmlWebpackPlugin代码段并更改为如下代码：
new HtmlWebpackPlugin({
      filename: 'index.html',
      template: path.resolve(__dirname, '../src/index.ejs'),
      // 添加内容-start
      templateParameters(compilation, assets, options) {
        return {
          compilation: compilation,
          webpack: compilation.getStats().toJson(),
          webpackConfig: compilation.options,
          htmlWebpackPlugin: {
            files: assets,
            options: options
          },
          process,
        };
      },
       // 添加内容-end
      minify: {
        collapseWhitespace: true,
        removeAttributeQuotes: true,
        removeComments: true
      },
      nodeModules: process.env.NODE_ENV !== 'production'
        ? path.resolve(__dirname, '../node_modules')
        : false
    }),

```

## 14.1隐藏标题栏或者隐藏菜单栏目

```js
//mian index.js

//隐藏标题栏
import { app, BrowserWindow,Menu  } from 'electron'
  Menu.setApplicationMenu(null)

//隐藏 主窗体的剩下标题栏整块
mainWindow = new BrowserWindow({
    height: 563,
    useContentSize: true,
    width: 1000,
    frame:false
})
```

## 14.2使用less或者sass

```js
npm install sass-resources-loader --save-dev
npm install less less-loader --save-dev


1、我们在.eleectron-vue/webpack.renderer.config.js中的module配置中找到如下代码
module: {
    rules: [
      {
        test: /\.less$/,
        use: ['vue-style-loader', 'css-loader', 'less-loader']
      }
    ]
  },
2、然后修改代码将这段代码修改如下
module: {
    rules: [
      {
        test: /\.less$/,
        use: [
            'vue-style-loader',
            'css-loader',
            'less-loader',
            {
              loader: 'sass-resources-loader',
              options: {
                resources: path.resolve(__dirname,'../src/renderer/assets/less/common.less'),//改路径为存放less全局变量的路径
              }
            }
        ]
      }
    ]
  },
```

## 14.3eletaron-vue bug问题

```
https://blog.csdn.net/weixin_34220623/article/details/88029445
```

## 14.4手动实现最大化,最小化,关闭

```javascript
//渲染进程
//最小化
    minimizeWin() {
      ipcRenderer.send('min'); // 窗口最小化
    },
    maximizeWin() {
      ipcRenderer.send('max');
    },
    closeWin() {
        ipcRenderer.send('close'); // 关闭窗口，也结束了所有进程
    },
 //主进程 main.js
  //最大化,最小化,关闭
    ipcMain.on('min', e=> mainWindow.minimize());
    ipcMain.on('max', e=> {
        if (mainWindow.isMaximized()) {
            mainWindow.unmaximize()
        } else {
            mainWindow.maximize()
        }
    });
    ipcMain.on('close', e=> mainWindow.close());
```

## 14.5 Antd vue引入

```js
import Antd from 'ant-design-vue';
import 'ant-design-vue/dist/antd.css';
Vue.use(Antd);
```

## 14.6 使用音乐播放器插件

```js
cnpm install vue-aplayer --save

//使用方法

 <aplayer
      ref="player"
      @ended='playend'
        theme="#C62F2F"
        :list="playList"
        :music="currentMusic"
        :listFolded="true"
        :volume="volume"
        :muted="muted"
      />
    </div>
  <c-progress class="c-progress"
       :percent="50" 
@percentChange="onPercentChange"
       :show-slider="true" 
progress-color="#C62F2F"
:width="50"/>
    
	//改变暂停播放
    changeStatus() {
        this.pause = !this.pause;
        if(this.pause){
            this.playDom.play()
        }else{
            this.playDom.pause()
        }
    },
   //暂停
    novolume(){
        this.muted = !this.muted
    },
   //改变音量
   onPercentChange(e){
       console.log(e)
       this.volume = e/100
   },

```

## 14.7 轮播图插件的使用

```js
npm install  vue-awesome-swiper
cnpm inatall vue-awesome-swiper

//全局使用
import VueAwesomeSwiper from 'vue-awesome-swiper'
// import style
import 'swiper/swiper-bundle.css' //6.0以上版本
import 'swiper/css/swiper.css'//6.0版本一下

//less
.swipers {
    padding-top: 15px;
    padding-bottom: 15px;
    width: 700px;
    height: 250px;
    margin: auto;
    overflow: hidden;
    .swipers-all {
      height: 100%;
      .item {
        width: 600px;
        img {
          width: 100%;
          // height: 100%;
        }
      }
    }
  }
options//配置
swiperOptions: {
        notNextTick: true,
        // loop: true, // 无限循环
        pagination: {
          el: ".swiper-pagination",
          type: "bullets"
        },
        autoplay:{
　　　　　　　　delay: 3000,
　　　　　　　　stopOnLastSlide: false,
　　　　　　　　/* 触摸滑动后是否继续轮播 */
　　　　　　　　disableOnInteraction: false
　　　　　},
        effect: "coverflow",
        grabCursor: true,
        centeredSlides: true,
        slidesPerView: "auto",
        coverflowEffect: {
          rotate: 0,
          stretch: 10, // slide左右距离
          depth: 180, // slide前后距离
          modifier: 2, //
          slideShadows: false, // 滑块遮罩层
        },
      },
    };

```

## 14.8 table表格插件

```
选择vxe-table的优势：
可以自定义选择引入的模块，减少项目体积；
多主题，多图标；
表格种类繁多；
扩展插件库；


npm install xe-utils vxe-table

import 'xe-utils'
import VXETable from 'vxe-table'
import 'vxe-table/lib/style.css'

Vue.use(VXETable)
```

