---
title: SSR服务端渲染
date:
updated:
type: "tags"
comments:
categories: Node
description: SSR服务端渲染
keywords: SSR服务端渲染
top_img: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3519339501,3990679385&fm=26&gp=0.jpg
cover: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3519339501,3990679385&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.SSR的优点和缺点

```
SSR的优点
1. 更利于SEO。
	使用了React或者其它MVVM框架之后，页面大多数DOM元素都是在客户端根据js动态生成，可供爬虫抓取分析的内容大大减少(如图一)。
2.更利于首屏渲染
	首屏的渲染是node发送过来的html字符串，并不依赖于js文件了，
	
SSR的局限
1.服务端压力较大
	本来是通过客户端完成渲染，现在统一到服务端node服务去做。尤其是高并发访问的情况，会大量占用服务端CPU资源；
2.开发条件受限
	在服务端渲染中，只会执行到componentDidMount之前的生命周期钩子，因此项目引用的第三方的库也不可用其它生命周期钩子，这对引用库的选择产生了很大的限制；
3.学习成本相对较高
	除了对webpack、React要熟悉，还需要掌握node、Koa2等相关技术。相对于客户端渲染，项目构建、部署过程更加复杂。
```

```
耗时比较
	1.数据请求，
	由服务端请求首屏数据，而不是客户端请求首屏数据，这是“快”的一个主要原因。服务端在内网进行请求，数据响应速度快。客户端在不同网络环境进行数据请求，且外网http请求开销大，导致时间差。
	2.html渲染
	服务端渲染是先向后端服务器请求数据，然后生成完整首屏html返回给浏览器；而客户端渲染是等js代码下载、加载、解析完成后再请求数据渲染，等待的过程页面是什么都没有的，就是用户看到的白屏。就是服务端渲染不需要等待js代码下载完成并请求数据，就可以返回一个已有完整数据的首屏页面。

```

# 2.Nuxt.js

## 2.1安装

```js
前提安装 npm install vue-cli -g
vue -V  检查版本
vue init nuxt/starter    //检查  使用 npm run dev  就是一个nuxt.js项目
```

## 2.2目录介绍

```js
.nuxt 是自动生成
assets    less  sass  js代码
components  组件
layouts   布局
middleware   中间件
node_modules  模块
pages   页面
plugins  插件
static  静态资源 图片等
store   状态管理  
eslint  代码校验
editorconfig  配置编辑器
gitignore   git上传忽略
nuxt.config.js  配置头部标签
package.json   配置命令打包等

配置nuxt的端口域名
 "config":{
     "nuxt":{
         "host":"127.0.0.1",
         "port":"1818"
     }
 }
 
配置全局样式
  css:['~assets/normalize.css'],
  
配置webpack	
    loader:[
          {
            test: /\.(png|jpg|jpeg|gif|svg)$/,
            loader:"url-loader",
            query:{
              limit:10000,
              name:'img/[name].[hash].[ext]'
            }
          }
        ],
```

## 2.3路由

```js
nuxt.js  路由是自动生成的
<ul>
	<li><nuxt-link :to="{name:'index'}">Home</nuxt-link></li>
	<li><nuxt-link :to="{name:'about'}">About</nuxt-link></li>
	<li><nuxt-link :to="{name:'news'}">News</nuxt-link></li>
</ul>

传递参数 
	<li><nuxt-link :to="{name:'index',params:{newsId:3306}}">Home</nuxt-link></li>
获取参数
	{{ $route.params.newsId }}
```

## 2.4动态路由

```js
下划线开始的动态路由
<li><a href="/news/123">news-1</a></li>
<li><a href="/news/456">news-2</a></li>

参数校验 
	validate({params}){
        return /^\d+$/.test(params.id)
    }
```

## 2.5过度

```js
必须使用 nuxt-link 标签
/* css过度页面 */
.page-enter-active,.page-leave-active{
    transition: all 0.5s;
}
.page-enter,.page-leave-active{
    opacity: 0;
}
.test-enter-active,.test-leave-active{
    transition: all 0.5s;
    font-size: 12px;
}
.test-enter,.test-leave-active{
    opacity: 0;
    font-size: 20px;
}
export default {
  transition:'test'
}
```

## 2.6默认模板和默认布局

```
名字  app.html
默认模板和默认布局大同小异
```

## 2.7错误页面和个性meta标签设置

```js
新建一个error   404找不到就会显示

设置头部
	js代码里面
	head(){
        return{
            title:this.title,
            meta:[
                {hid:'bbb',name：'news1',content:'This is  new info'}
            ]
        }
	}
```

## 2.8异步请求数据

```js
asyncData(){
    return axios.get('https://api.myjson.com/?')
    .then((res)=>{
        return {info:res.data}
    })
}
```

## 2.9生成静态资源

```js
~代表项目根目录下
打包 npm run generate

npm install -g live-server
使用live-server
```

# 3.Next.js

```js
yarn add react react-dom next

手动配置

使用create-next-app快速创建项目
```

## 3.1创建

```js
npx create-next-app  
yarn dev  运行项目
```

## 3.2 page和component的使用

```js
路由自动配置
以及路由自动配置 
二级路由 
	文件夹的方式   http://localhost:3000/blog/nextblog
	
组件
	export default ({children})=><button>{children}</button>
	引入直接使用
```

## 3.2路由跳转

```js
标签跳转 Link
		 <Link href="/blog/nextblog"><a>去博客页面</a></Link>
		  <Link href="/"><a>返回首页</a></Link>
		  
		  加A标签包裹起来
编程跳转
		import Router from 'next/router'
		<div onClick={()=>{Router.push('/')}}>
        	返回首页
        </div>
```

## 3.3路由跳转传递参数接收参数

```js
LInk  标签跳转
	<Link href="/blog/nextblog?name=结义"><a>结义</a></Link><br></br>
      <Link href="/blog/nextblog?name=进空"><a>进空</a></Link>
      
      接受
      	import { withRouter } from 'next/router'
      	export default withRouter(NextBlog)
      	 <h2>{router.query.name}</h2>
 编程时传递
 		import Router from 'next/router'
        let gotoname = ()=>{
          Router.push('/blog/nextblog?name=结义')
        }
        
        2.对象
        	let gotoname = ()=>{
              Router.push({
                pathname:'/blog/nextblog',
                query:{name:'进空'}
              })
            }
```

## 3.4路由中的钩子事件

```js
//routeChangeStart  1 11111
  //routeChangeComplete   
  //beforeHistoryChange   2222
  //routeChangeError  路由发生错误  
  //hashChangeStart
  //hashChangeComplete
  Router.events.on('routeChangeStart',(...args)=>{
    console.log('11111',...args)
  })
  Router.events.on('beforeHistoryChange',(...args)=>{
    console.log('2222',...args)
  })
  Router.events.on('routeChangeComplete',(...args)=>{
    console.log('3333',...args)
  })
```

## 3.5获取远端数据axios

```js
getInitialProps
	NextBlog.getInitialProps = async ()=>{
    const promise = new Promise((resolve)=>{
        axios('http://rap2.taobao.org:38080/app/mock/256761/api/v1/article').then((res)=>{
            // console.log(res)
            resolve(res.data.data)
        })
    })
    return await promise
}
export default withRouter(NextBlog)


接受
		function NextBlog({router,list})就可以拿到数据
		
		<p>数据：{list.map((item)=>{
            return (
            <div>{item.title}</div>
            )
        })}</p>
        
        注意返回的结果和   list或者result接受的参数匹配上
```

## 3.6css样式

```js
<style jsx>
	{
        div{
            color:red
        }
	}
</style>
```

## 3.7moment.js  处理时间

```js
引入moment
moment.dafault(Date.now().format())

懒加载 
	const moment  = await import('moment')
```

## 3.8SEO

```js
import Head from 'next/head'
function Header(){
    return(
        <>
            <div>Jspang.com</div>
            <Head>
                <title>我是最棒的</title>
                <meta charSet="utf-8"></meta>
            </Head>
        </>
    )
}
```

## 3.9打包的坑

```
antd的css样式不合适  需要全局引入   新建一个页面 app  抛出去
```

# 4.vue-SSR渲染

## 4.1预渲染

```js
cnpm i prerender-spa-plugin
//预渲染
const PrerenderSpaPlugin= require('prerender-spa-plugin')
//调用渲染器
const Renderer = PrerenderSpaPlugin.PuppeteerRenderer
const env = require('../config/prod.env')

 new PrerenderSpaPlugin({
      staticDir:path.join(__dirname,'../dist'),
      routes: [ '/','/service','/companyintroduction','/jobchance','/contactus','/home'],
      renderer:new Renderer({
        inject:{
          foo:'far'
        },
        headless:false,
        //项目的入口中使用
        renderAfterDocumentEvent:'render-event'
      })
    })

 mounted(){
    document.dispatchEvent(new Event('render-event'))
  }

//assetsPublicPath: '/',

然后 npm run build

//全局安装  npm install http-server -g
// hs -o -p 9999
//预渲染不适用的场景
//什么场景下不适合使用预渲染
　　预渲染不适用于渲染路由过多（不建议预渲染非常多的路由，因为这会严重拖慢你的构建进程） 和 动态路由 （如/detail/参数，因为页面内容依据看它的参数而显得不同），只是适用于几个简单的固定路由的情景（例如 /index /about /contact）
//SSR的优势
SSR的优势
　　（1）更利于SEO：不同爬虫工作原理类似，只会爬取源码，不会执行网站的任何脚本（Google除外，据说Googlebot可以运行javaScript）。使用了React或者其它MVVM框架之后，页面大多数DOM元素都是在客户端根据js动态生成，可供爬虫抓取分析的内容大大减少。另外，浏览器爬虫不会等待我们的数据完成之后再去抓取我们的页面数据。服务端渲染返回给客户端的是已经获取了异步数据并执行JavaScript脚本的最终HTML，网络爬中就可以抓取到完整页面的信息。
　　（2）更利于首屏渲染：首屏的渲染是node发送过来的html字符串，并不依赖于js文件了，这就会使用户更快的看到页面的内容。尤其是针对大型单页应用，打包后文件体积比较大，普通客户端渲染加载所有所需文件时间较长，首页就会有一个很长的白屏等待时间。
 //服务端渲染与预渲染区别
　　客户端渲染：用户访问 url，请求 html 文件，前端根据路由动态渲染页面内容。关键链路较长，有一定的白屏时间；
　　服务端渲染：用户访问 url，服务端根据访问路径请求所需数据，拼接成 html 字符串，返回给前端。前端接收到 html 时已有部分内容；
　　预渲染：构建阶段生成匹配预渲染路径的 html 文件（注意：每个需要预渲染的路由都有一个对应的 html）。构建出来的 html 文件已有部分内容
 //服务端渲染与预渲染共同点
　　针对单页应用，服务端渲染和预渲染共同解决的问题：
　　（1）SEO：单页应用的网站内容是根据当前路径动态渲染的，html 文件中往往没有内容，网络爬虫不会等到页面脚本执行完再抓取；
　　（2）弱网环境：当用户在一个弱环境中访问你的站点时，你会想要尽可能快的将内容呈现给他们。甚至是在 js 脚本被加载和解析前；
　　（3）低版本浏览器：用户的浏览器可能不支持你使用的 js 特性，预渲染或服务端渲染能够让用户至少能够看到首屏的内容，而不是一个空白的网页。
　　预渲染能与服务端渲染一样提高 SEO 优化，但前者比后者需要更少的配置，实现成本低。弱网环境下，预渲染能更快地呈现页面内容，减少页面可见时间。
```

## 4.2SSR

### 4.2.1webpack.server.conf.js

```js
npm i vue express vue-server-renderer
// 在package.json 里
//   "server":"webpack --config build/webpack.server.config.js"
// 把basse.conf.js  的入口文件注释掉

///node_modules/vue-loader/lib/template-compiler/index.js
//遇见babel打吧错误
    if (!isProduction) {
      code = prettier.format(code, { semi: false, parser: 'babylon' })
    }
    //babylon改为babel
 if (!isProduction) {
      code = prettier.format(code, { semi: false, parser: 'babel' })
    }
// cnpm i webpack-node-externals

//  webpack.server.conf.js
const merge = require('webpack-merge')
const VueSSRServerPlugin = require('vue-server-renderer/server-plugin')
const nodeExternals = require('webpack-node-externals')
//引入配置
const base = require('./webpack.base.conf')

module.exports = merge(base,{
    target:'node',
    devtool: 'source-map',
    entry:'./src/entry-server.js',
    output:{
        filename: 'bundle.server.js',
        libraryTarget: 'commonjs2'
    },
    externals: nodeExternals({
        // 不要外置化 webpack 需要处理的依赖模块。
        // 你可以在这里添加更多的文件类型。例如，未处理 *.vue 原始文件，
        // 你还应该将修改 `global`（例如 polyfill）的依赖模块列入白名单
        whitelist: /\.css$/
    }),
    plugins:[
        new VueSSRServerPlugin()
    ]
})
```

### 4.2.2  entry-server.js

```js
import { createApp } from './main'

export default context =>{
    return new Promise((resolve,reject)=>{
        //创建路由
        const { app } = createApp()
        const router = app.$router

        const { url } = context
        const { fullPath } = router.resolve(url).route

        if(fullPath !== url){
            return reject({ url:fullPath })
        }
        //更改路由
        router.push(url)

        router.onReady(()=>{
            const matchedComponents = router.getMatchedComponents()
            //没有匹配的路由
            if(!matchedComponents.length){
                return reject({code: 404})
            }
            //匹配到路由
            resolve(app)
        },reject)
    })
}
```

### 4.2.3修改工厂模式

```js
//main.js
// main.js
import Vue from 'vue'
import App from './App.vue'
import { createRouter } from './router'
import { createStore } from './store/store.js'
import { sync } from 'vuex-router-sync'

export function createApp () {
 // 创建 router 实例
 const router = createRouter()
 const store = createStore()

 // 同步路由状态(route state)到 store
 sync(store, router)

 const app = new Vue({
  // 注入 router 到根 Vue 实例
  router,
  store,
  render: h => h(App)
 })

 // 返回 app 和 router
 return { app, router, store }
}

//路由
    // router.js
    import Vue from 'vue'
    import Router from 'vue-router'
    import HelloWorld from '@/components/HelloWorld'

    Vue.use(Router)


    export let createRouter = () => {
     let route = new Router({
      mode:'history',
      routes: []
     })
     return route
    }

//商店
	import Vue from 'vue'
    import Vuex from 'vuex'

    Vue.use(Vuex)

    export function createStore () {
     return new Vuex.Store({
      state: {
      },
      actions: {
      },
      mutations: {
      }
     })
    }
```

### 4.2.4客户端渲染

```js
//webpack
const webpack = require('webpack')
const merge = require('webpack-merge')
const baseConfig = require('./webpack.base.conf.js')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const path = require('path')
const VueSSRClientPlugin = require('vue-server-renderer/client-plugin')

module.exports = merge(baseConfig, {
 entry: './src/entry-client.js',
 plugins: [
  new webpack.optimize.CommonsChunkPlugin({
   name: "manifest",
   minChunks: Infinity
  }),
  // 此插件在输出目录中
  // 生成 `vue-ssr-client-manifest.json`。
  new VueSSRClientPlugin(),
  new HtmlWebpackPlugin({
   template: path.resolve(__dirname, './../src/index.template.html'),
   filename: 'index.template.html'
  })
 ]
    
    
   //    "client": "webpack --config build/webpack.client.conf.js"

```

### 5.2.5数据预取和存储

```js
服务器渲染，可以理解为在被访问的时候，服务端做预渲染生成页面，上面说过，预渲染的缺点就是，实时数据的获取。所以如果应用程序依赖于一些异步数据，那么在开始渲染过程之前，需要先预取和解析好这些数据。

另一个需要关注的问题是在客户端，在挂载 (mount) 到客户端应用程序之前，需要获取到与服务器端应用程序完全相同的数据 - 否则，客户端应用程序会因为使用与服务器端应用程序不同的状态，然后导致混合失败。这个地方上面提过，叫同构（服务端渲染一遍，客户端拿到数据再渲染一遍）。

//同构流程
	客户端访问网站 —> 服务器获取动态数据，生成页面，并把数据存入vuex中，然后返回html —> 客户端获取html（此时已经返回了完整的页面） —> 客户端获取到vuex的数据，并解析到vue里面，然后再一次找到根元素挂载vue,重复渲染页面。（同构阶段）
官网 //
//1.自定义函数asyncData
	<!-- Item.vue -->
    <template>
     <div>{{ item.title }}</div>
    </template>

    <script>
    export default {
     asyncData ({ store, route }) {
      // 触发 action 后，会返回 Promise
      return store.dispatch('fetchItem', route.params.id)
     },
     computed: {
      // 从 store 的 state 对象中的获取 item。
      item () {
       return this.$store.state.items[this.$route.params.id]
      }
     }
    }
    </script>

//entry-server.js,

// entry-server.js
    import { createApp } from './app'
    export default context => {
     return new Promise((resolve, reject) => {
      const { app, router, store } = createApp()

      router.push(context.url)

      router.onReady(() => {
       const matchedComponents = router.getMatchedComponents()
       if (!matchedComponents.length) {
        return reject({ code: 404 })
       }

       // 对所有匹配的路由组件调用 `asyncData()`
       Promise.all(matchedComponents.map(Component => {
        if (Component.asyncData) {
         return Component.asyncData({
          store,
          route: router.currentRoute
         })
        }
       })).then(() => {
        // 在所有预取钩子(preFetch hook) resolve 后，
        // 我们的 store 现在已经填充入渲染应用程序所需的状态。
        // 当我们将状态附加到上下文，
        // 并且 `template` 选项用于 renderer 时，
        // 状态将自动序列化为 `window.__INITIAL_STATE__`，并注入 HTML。
        context.state = store.state

        resolve(app)
       }).catch(reject)
      }, reject)
     })
    }
```

### 5.2.6客户端入口

```js
const { app, router, store } = createApp()
if (window.__INITIAL_STATE__) {
 store.replaceState(window.__INITIAL_STATE__)
}
```

### 5.3.7服务端

```js
const express = require("express");

const fs = require('fs');
let path = require("path");
const server = express()
const { createBundleRenderer } = require('vue-server-renderer')

let renderer

const resolve = file => path.resolve(__dirname, file)
const templatePath = resolve('./src/index.template.html')
function createRenderer (bundle, options) {

 return createBundleRenderer(bundle, Object.assign(options, {
  runInNewContext: false
 }))
}

const template = fs.readFileSync(templatePath, 'utf-8')
const bundle = require('./dist/vue-ssr-server-bundle.json')
const clientManifest = require('./dist/vue-ssr-client-manifest.json')
renderer = createRenderer(bundle, {
 template,
 clientManifest
})

server.use(express.static('./dist'))
// 在服务器处理函数中……
server.get('*', (req, res) => {
 const context = { url: req.url }
 // 这里无需传入一个应用程序，因为在执行 bundle 时已经自动创建过。
 renderer.renderToString(context, (err, html) => {
  // 处理异常……
  res.end(html)
 })
})
server.listen(3001, () => {
  console.log('服务已开启')
})
```

### 5.3.8热更新和本地调试

```js
server.dev.conf.js
//server.dev.conf.js

const fs = require('fs')
const path = require('path')
const MFS = require('memory-fs')
const webpack = require('webpack')
const chokidar = require('chokidar')
const clientConfig = require('./webpack.client.conf.js')
const serverConfig = require('./webpack.server.conf.js')

const readFile = (fs, file) => {
 try {
  return fs.readFileSync(path.join(clientConfig.output.path, file), 'utf-8')
 } catch (e) {}
}

module.exports = function setupDevServer (app, templatePath, cb) {
 let bundle
 let template
 let clientManifest

 let ready
 const readyPromise = new Promise(r => { ready = r })
 const update = () => {
  if (bundle && clientManifest) {
   ready()
   cb(bundle, {
    template,
    clientManifest
   })
  }
 }

 // read template from disk and watch
 template = fs.readFileSync(templatePath, 'utf-8')
 chokidar.watch(templatePath).on('change', () => {
  template = fs.readFileSync(templatePath, 'utf-8')
  console.log('index.html template updated.')
  update()
 })

 // modify client config to work with hot middleware
 clientConfig.entry.app = ['webpack-hot-middleware/client', clientConfig.entry.app]
 clientConfig.output.filename = '[name].js'
 clientConfig.plugins.push(
  new webpack.HotModuleReplacementPlugin(),
  new webpack.NoEmitOnErrorsPlugin()
 )

 // dev middleware
 const clientCompiler = webpack(clientConfig)
 const devMiddleware = require('webpack-dev-middleware')(clientCompiler, {
  publicPath: clientConfig.output.publicPath,
  noInfo: true
 })
 app.use(devMiddleware)
 clientCompiler.plugin('done', stats => {
  stats = stats.toJson()
  stats.errors.forEach(err => console.error(err))
  stats.warnings.forEach(err => console.warn(err))
  if (stats.errors.length) return
  clientManifest = JSON.parse(readFile(
   devMiddleware.fileSystem,
   'vue-ssr-client-manifest.json'
  ))
  update()
 })

 // hot middleware
 app.use(require('webpack-hot-middleware')(clientCompiler, { heartbeat: 5000 }))

 // watch and update server renderer
 const serverCompiler = webpack(serverConfig)
 const mfs = new MFS()
 serverCompiler.outputFileSystem = mfs
 serverCompiler.watch({}, (err, stats) => {
  if (err) throw err
  stats = stats.toJson()
  if (stats.errors.length) return

  // read bundle generated by vue-ssr-webpack-plugin
  bundle = JSON.parse(readFile(mfs, 'vue-ssr-server-bundle.json'))
  update()
 })

 return readyPromise
}
```

```js
//server.js  修改
//server.js
const express = require("express");

const fs = require('fs');
let path = require("path");
const server = express()
const { createBundleRenderer } = require('vue-server-renderer')
const isProd = process.env.NODE_ENV === 'production'
let renderer
let readyPromise
const resolve = file => path.resolve(__dirname, file)
const templatePath = resolve('./src/index.template.html')
function createRenderer (bundle, options) {
 return createBundleRenderer(bundle, Object.assign(options, {
  runInNewContext: false
 }))
}

if(isProd){
 const template = fs.readFileSync(templatePath, 'utf-8')
 const bundle = require('./dist/vue-ssr-server-bundle.json')
 const clientManifest = require('./dist/vue-ssr-client-manifest.json')
 renderer = createRenderer(bundle, {
  template,
  clientManifest
 })

}else{
 readyPromise = require('./build/server.dev.conf.js')(
  server,
  templatePath,
  (bundle, options) => {
   renderer = createRenderer(bundle, options)
  }
 )
}
server.use(express.static('./dist'))
// 在服务器处理函数中……
server.get('*', (req, res) => {
 const context = { url: req.url }
 // 这里无需传入一个应用程序，因为在执行 bundle 时已经自动创建过。
 // 现在我们的服务器与应用程序已经解耦！
 if(isProd){
  renderer.renderToString(context, (err, html) => {
   // 处理异常……
   res.end(html)
  })
 }else{
  readyPromise.then(()=>{
   renderer.renderToString(context, (err, html) => {
    // 处理异常……
    res.end(html)
   })
  })
 }
})
server.listen(3001, () => {
  console.log('服务已开启')
})
```

# 5.nextjs 博客实战

## 5.1准备

```js
cnpm i -g create-next-app
npx create-next-app react_blog_front
yarn dev

//支持使用css
yarn add @zeit/next-css

//yarn and antd
//按需加载
//yarn add babel-plugin-import


//配置babel 和 css插件
//babelrc
{
    "presets": ["next/babel"],
    "plugins": [
        [
            "import",
            {
                "libraryName":"antd"
            }
        ]
    ]
}
//next.config.js
const WithCss = require('@zeit/next-css')
if(typeof require !== undefined){
    require.extensions['css'] = file =>{}
}
module.exports = WithCss({})

//引入less
cnpm install --save @zeit/next-less node-less
```

## 5.2实战头部

```react
//公共头部
 <div className="header">
      <Row type="flex" justify="center">
        <Col className="header-left">
          <span className="header-logo">mikasa</span>
          <span className="header-txt">专注前端开发</span>
        </Col>
        <Col>
          <Menu mode="horizontal">
            <Menu.Item
              key="home"
              className="header-right-item"
              icon={<BookOutlined />}
            >
              首页
            </Menu.Item>
            <Menu.Item
              key="blog"
              className="header-right-item"
              icon={<FileWordOutlined />}
            >
              博客
            </Menu.Item>
            <Menu.Item
              key="note"
              className="header-right-item"
              icon={<ContainerOutlined />}
            >
              笔记
            </Menu.Item>
            <Menu.Item
              key="github"
              className="header-right-item"
              icon={<GithubOutlined />}
            >
              点赞
            </Menu.Item>
          </Menu>
        </Col>
      </Row>
    </div>

//头部样式
.header {
    background-color: #fff;
    overflow: hidden;
    height: 2.8rem;
    border-bottom: 1px solid #fff;
    font-size: 1.2rem;
    font-weight: bolder;
    padding: 0.3rem;
    box-sizing: content-box;

    .header-left {
        margin-right: 10rem;

        .header-logo {
            line-height: 2.8rem;
            color: rgb(46, 157, 221);
            font-size: 1.5rem;
            margin-right: .4rem;
        }

        .header-txt {
            line-height: 2.8rem;
        }
    }

    .header-right-item {
        font-size: 1rem;
    }

    .header-right-item svg {
        font-size: 1.2rem;
    }

    @media screen and (max-width: 375px) {
        height: 7rem;
        .header-left {
            margin-right: 1rem;
        }
    }
}
```

## 5.3markdown代码高亮

```react
import marked from "marked";
import hljs from "highlight.js";
import MarkNav from "markdown-navbar";
import "highlight.js/styles/monokai-sublime.css";

var [data, setData] = useState('loading....');
  useEffect(() => {
    // marked相关配置
    marked.setOptions({
      renderer: new marked.Renderer(),
      gfm: true,
      pedantic: false,
      sanitize: false,
      tables: true,
      breaks: true,
      smartLists: true,
      smartypants: true,
      highlight: function (code) {
        return hljs.highlightAuto(code).value;
      },
    });
    Readfile({ fileid: "015d1d96-9d66-424d-b9d9-34d6a9439cea.md" }).then(
      (res) => {
        setData(res);
      }
    );
  }, []);


 <div
     id="content"
     className="article-detail"
     dangerouslySetInnerHTML={{__html:marked(data)}}
     />

 <div className="detailed-nav comm-box">
    <div className="nav-title">文章目录</div>
    <MarkNav className="article-menu" source={data} ordered={false} />
</div>


//对markdown样式的补充
/*对 markdown 样式的补充*/
pre {
    display: block;
    padding: 10px;
    margin: 0 0 10px;
    font-size: 14px;
    line-height: 1.42857143;
    color: #abb2bf;
    background: #282c34;
    word-break: break-all;
    word-wrap: break-word;
    overflow: auto;
}
h1,h2,h3,h4,h5,h6{
    margin-top: 1rem;
    font-weight: bolder;
    margin-bottom: 1rem;
    /* margin-bottom: 1em; */
}
h1{
    font-size: 24px;
    font-weight: bolder;
}
strong {
    font-weight: bold;
}

p > code:not([class]) {
    padding: 2px 4px;
    font-size: 90%;
    color: #c7254e;
    background-color: #f9f2f4;
    border-radius: 4px;
}
p img{
    /* 图片居中 */
    margin: 0 auto;
    display: flex;
}

/*对 markdown 样式的补充*/
pre {
    display: block;
    padding: .1rem;
    margin: 0 0 5px;
    font-size: 14px;
    line-height: 1.42857143;
    color: #000000;
    background: #282c34;
    word-break: break-all;
    word-wrap: break-word;
    overflow: auto;
}
h1,h2,h3,h4,h5,h6{
    margin-top: 1em;
    /* margin-bottom: 1em; */
}
strong {
    font-weight: bold;
}

p > code:not([class]) {
    padding: 2px 4px;
    font-size: 90%;
    color: #c7254e;
    background-color: #f9f2f4;
    border-radius: 4px;
}
p img{
    /* 图片居中 */
    margin: 0 auto;
    display: flex;
}

#content {
    font-family: "Microsoft YaHei",  'sans-serif';
    font-size: 16px;
    line-height: 30px;
}

#content .desc ul,#content .desc ol {
    color: #333333;
    margin: .3rem 0 0 25px;
}

#content .desc h1, #content .desc h2 {
    border-bottom: 1px solid #eee;
    padding-bottom: 10px;
}

#content .desc a {
    color: #009a61;
}

```

## 5.4Hooks的使用

```react
//hookes
//定义变量
    const [data,setData] = useState({description:''})
//实现循环两次
    useEffect(()=>{
        UserInfo({uid:props.uid}).then(res=>{
          setData(res[0])
        })
      },[])
//实现componentDidMount 
useEffect(() => {
    console.log('hello world')
  }, [])
//componentDidMount componentDidUpdate
const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
//componentDidMount componentWillUnmount
 const [count, setCount] = useState(0);
  useEffect(() => {
    const id = setInterval(() => {
      setCount(c => c + 1);
    }, 1000);
    return () => clearInterval(id);
  }, []);
//componentDidUpdate 
const [count, setCount] = useState(0);
  const prevCountRef = useRef(false);
  useEffect(() => {
    if (prevCountRef.current) {
      console.log('更新时候的数据')
    } else {
      prevCountRef.current = true
    }
  });
```

