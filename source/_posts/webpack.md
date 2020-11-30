---
title: Webpack
date:
updated:
type: "tags"
comments:
categories: Webpack
description: Webpack
keywords: Webpack
top_img: https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3483345719,214526697&fm=26&gp=0.jpg
cover: https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3483345719,214526697&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 一.webpack简介

```js
前端资源构建工具，是一个静态模块打包工具，
前端的所有资源都会作为模块处理

安装
		再更新npm到最新版本：
        npm install -g npm
        
        再卸载webpack，对应命令：
        npm  uninstall  webpack  -g
        npm  uninstall  webpack-cli  -g
        
        然后再全局安装webpack和本地安装：
        npm install webpack webpack-cli –g
        npm install webpack webpack-cli --save-dev
安装不了解决
	1.无法加载文件 D:\nodejs\node_global\webpack.ps1，因为在此系统上禁止运行脚本，有关详细信息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170
		1.get-ExecutionPolicy
		2.set-ExecutionPolicy RemoteSigned
		
		
	初始化 webpack  npm init
	
	
	webpack  五个核心概念
		Entry   从哪个文件开始打包
		Output  输出 打包后的资源 bundles 输出到哪里，如何命名
		Loader loader让webpack处理非 js 文件
		Plugins 可以用于执行范围更广的任务，从打包优化压缩，重新定义变量等
		Mode 指示webpack使用响应模式的配置 有 development开发模式 和 production生产模式
	
	npm i webpack webpack-cli -g  全局安装
	npm i webpack webpack-cli -D  本地安装
```

# 二.初体验

```js
npm init
刚开始默认只有  三个文件  node modules 和  package.json  和 package-lock.json
开发环境：webpack-cli ./src/index.js -o ./build/built.js --mode=development
        webpack会以./src/index.js 为入口文件 
        打包输出到./build/built.js 
        整体打包环境是开发环境
生产环境:  webpack-cli ./src/index.js -o ./build/built.js --mode=production
        压缩代码
	
	总结 
	1.webpack能处理  js/json  不能处理css/img等其他资源
	2.生产环境比开发环境多个压缩js代码
	3.生产环境和开发环境将ES6模块化编译成为浏览器能识别的模块化

```

# 三.打包

```javascript
打包样式资源
	webpack.config.js是
	 webpack配置文件
     作用指示  webpack 具体如何打包
     模块化默认采用common.js
     
      npm i webpack webpack-cli -D   创建项目下必须安装到本地
      
webpack-cli 命令打包
```



## 3.1打包js json

```javascript
//引入nodejs path模块
//resolve用来拼接路径的方法
const { resolve } = require("path");
module.exports = {
  //webpack配置
  //入口文件起点
  entry: "./src/index.js",
  //输出
  output: {
    //输出文件名
    filename: "built.js",
    //输出路劲
    //__dirname nodejs的变量，代表当前文件目录的绝对路径
    path: resolve(__dirname, "build"),
  },
  // loader的配置
  module: {
      //不同loader必须配置不同的loader处理
    rules: [
      {
        //匹配那些文件
        test: /\.css$/,
        //使用那些loader进行处理
        use: [
          //执行顺序,从右到左，从下到上
          //创建style标签,将js中的样式插入到html head中
          "style-loader",
          //将css文件变成commonjs模块加载到js中,里面内容是字符串
          "css-loader",
        ],
      },
      {
          test: /\.less$/,
          use:[
              'style-loader',
              'css-loader',
              'less-loader'
          ]
      }
    ],
  },
  //插件的配置
  plugins: [

  ],
  //模式
  mode: "development",
  //mode:'production'
};
```

## 3.2打包css less sass

```javascript
module: {
      //不同loader必须配置不同的loader处理
    rules: [
      {
        //匹配那些文件
        test: /\.css$/,
        //使用那些loader进行处理
        use: [
          //执行顺序,从右到左，从下到上
          //创建style标签,将js中的样式插入到html head中
          "style-loader",
          //将css文件变成commonjs模块加载到js中,里面内容是字符串
          "css-loader",
        ],
      },
      {
          test: /\.less$/,
          use:[
              'style-loader',
              'css-loader',
              'less-loader'
          ]
      }
    ],
  },
```



## 3.3打包html文件

```javascript
// html资源处理   plugins  插件 1.下载 2.引入 3.使用
// css资源处理   loader   1.下载  2.使用(配置loader)
//cnpm i html-webpack-plugin -D

const HtmlWebpackPlugin = require('html-webpack-plugin')
plugins:[
        //默认会创建一个html文件 引入打包输出所有资源 (JS/CSS)
        //需求 需要有结构的HTML文件
        new HtmlWebpackPlugin({
            //复制这个文件,并且自动引入打包输出所有资源
            template: './src/index.html'

        })
    ],
```

## 3.4打包图片资源

```javascript
 rules: [
      //loader的配置
      {
        test: /\.less$/,
        use: ["style-loader", "css-loader", "less-loader"],
      },
      {
        //处理图片资源
        //问题  处理不了html里面的图片，再加一个loader处理
        test: /\.(jpg|png|gif)$/,
        //如果只有一个loader 直接写 不写use数组
        //url-loader依赖于file-loader
        loader: "url-loader",
        options: {
          //图片小于8kb,就会被 base64处理
          // 优点 减少请求数量
          // 缺点  图片体积会更大
          limit: 8 * 1024,
           //url-loader默认使用es6模块化解析
            //html-loader默认使用common.js解析
            //问题解决 关闭 url-loader的es6模块化解析，使用commonjs解析
            esModule: false,
            //不想要hash值这么长的文件名,重命名图片 取图片的哈希值前10位
            name:'[hash:10].[ext]'
        },
      },
      {
        test: /\.html$/,
        //处理html里面的img文件(负责引入img,从而被url-loader处理)
        loader: "html-loader"
      },]
```

## 3.5打包其他资源(字体)

```javascript
//打包其他资源
      {
          //判断 css js html
          exclude: /\.(css|js|html)$/,
          loader: 'file-loader'  
      }
```

# 四.devServer

```javascript
保持看到最新的js代码等
避免重复打包 
mode: "development",
  //开发服务器 devServer: 用来自动化(自动编译，自动打开浏览器，自动刷新)
  //特点 只会在内存中打包，不会有任何输出
  //启动指令npx webpack-dev-server  不会有任何输出
  devServer:{
      contentBase: resolve(__dirname,'build'),
      //启动gzip压缩
      compress: true,
      //端口号
      port:3000,
      //运行手动打开浏览器
      open: true
  }
```

# 五.开发环境基本配置

```javascript
const { resolve } = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin')
module.exports = {
    entry: './src/index.js',
    output: {
        filename: 'js/built.js',
        path: resolve(__dirname, 'build')
    },
    module: {
        rules: [
            //loader的配置
            {
                test: /\.less$/,
                use: ['style-loader', 'css-loader', 'less-loader']
            },
            {
                test: /\.css$/,
                use: ['style-loader', 'css-loader']
            },
            {
                //处理图片资源
                test: /\.(jpg|png|gif)$/,
                loader: 'url-loader',
                options:{
                    limit: 8 * 1024,
                    name: '[hash:10].[ext]',
                    //开启commonjs
                    esModule: false,
                    //输出文件夹
                    outputPath: 'imgs'
                }
            },
            {
                //处理html的图片资源
                test: /\.html$/,
                loader: 'html-loader',
                //输出文件夹
                outputPath: 'imgs'
            },
            {
                exclude: /\.(html|js|css|less|jpg|png|gif)/,
                loader: 'file-loader',
                options:{
                    name: '[hash:10].[ext]'
                }
            }
        ]
    },
    plugins:[
        new HtmlWebpackPlugin({
            template: './src/index.html'
        })
    ],
    mode: 'development',
    devServer:{
        contentBase: resolve(__dirname, 'build'),
        compress: true,
        port: 3000,
        open: true
    }
}
```

# 六.提取css成单独文件

```javascript
cnpm i mini-css-extract-plugin -D
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
	//loader
		test: /\.css$/,
         use: [
         // 'style-loader', 
         //取代style loader
         MiniCssExtractPlugin.loader,
         'css-loader'
        ]
             
     plugins:[
        new HtmlWebpackPlugin({
            template: './src/index.html'
        }),
        new MiniCssExtractPlugin()
        //new MiniCssExtractPlugin({
        //    filename: 'css/built.css'
        //})
    ],
```

# 七.css兼容性处理

```javascript
postcss-loader  		 postcss-preset-env  识别环境
cnpm i postcss-loader postcss-preset-env -D


	//package.json配置
		"browserslist":{
            "development":[
              "last 1 chrome version",
              "last 1 firefox version",
              "last 1 safari version"
            ],
            "production":[
              ">0.2%",
              "not dead",
              "not op_mini all"
            ]
          }
          
          //设置node的环境变量
		process.env.NODE_ENV = 'development';
		
		 {
                test: /\.css$/,
                use: [
                    // 'style-loader', 
                    //取代style loader
                    MiniCssExtractPlugin.loader,
                    'css-loader',
                    {
                        loader: 'postcss-loader',
                        options:{
                            ident: 'postcss',
                            plugins: () => {
                                //postcss的插件
                                //帮助postcss找到package.json的browserlist的配置,加载指定的css兼容性样式
                                require('postcss-preset-env')()
                            }
                        }
                    }
                ]
            },
            
            new MiniCssExtractPlugin({
                filename: 'css/built.css'
            })
```

# 八.压缩css

```javascript
cnpm i optimize-css-assets-webpack-plugin -D
  const OptimizeCssAssetsWebpackPlugin = require('optimize-css-assets-webpack-plugin');

  new OptimizeCssAssetsWebpackPlugin() 
```

# 九.代码校验

```javascript
 		 //loader的配置
            // eslint-loader eslint  代码校验
            //注意  只检查代码
            //设置检查规则
            // package.json 中的 eslintConfig
            // airbnb --> eslintbase  eslint  eslint-plugin-import
        
        
        {
                test: /\.js$/,
                loader: 'eslint-loader',
                exclude: /node_modules/,
                options:{
                    fix: true
                }
            },
            
             "eslintConfig":{
                "extends": "airbnb-base"
              }
```

# 十.js兼容性处理

```javascript
babel
	//只能转化基本语法
	cnpm i babel-loader @babel/preset-env -D
	cnpm i @babel/core -D
	//都可以转化
	@babel/polyfill
	js中 引入   import '@babel/polyfill'
	//解决按需引入
	core-js
	{
                test: /\.js$/,
                exclude: /node_modules/,
                loader: 'babel-loader',
                options:{
                    presets:[
                        '@babel/preset-env',
                        {
                            useBuiltins: 'usage',
                            corejs:{
                                version:3
                            },
                            targets: {
                                chrome: '60',
                                firefox: '60',
                                ie: '9',
                                safari: '10',
                                edge: '19'
                            }
                        }
                    ]
                }
            }
            
        第三种和第二种只能要一种
```

# 十一.html,js代码压缩



```javascript
 压缩  html
 new HtmlWebpackPlugin({
            template: './src/index.html',
            minify:{
                
                collapseWhitespace:true,
                removeComments: true
            }
        }),
        
  js压缩生产环境即可
```

# 十二.性能优化

```
开发环境
	优化打包构建速度
	优化代码调试
生产环境
	优化打包构建速度
	优化代码运行性能
```

## 12.1开发环境

```javascript
问题 1
	HMR
	修改器其中一个代码,其它模块会被重新加载
	HMR  hot module replacement  热模块替换
	
	开启
	devServer:{
        contentBase: resolve(__dirname, 'build'),
        compress: true,
        port: 3000,
        open: true,
        hot: true  **************
    }
    样式文件 默认使用HMR
    js文件 默认不能使用  需要修改  js代码
    	加一个 if(module.hot){
            module.hot.accept('./print.js',function(){
                print();
            })
    	}
    html  默认不能使用   html文件不能热更新(不需要HML功能)
    	解决 修改 entry  入口将 html文件引入
    	 entry: ['./src/js/index.js','./src/index.html'],
    	 
问题2
	Source-map
	提供一种技术，源代码到构建后代码映射技术 如果构建后代码出错，可以追踪到源代码出错
	
		  // inline-source-map   内联速度快 只生成一个map
        // hidden-source-map   外部
        // eval-source-map    内联 每一个文件生成map  都在 eval
        // source-map   准备提示错误信息

        devtool: 'source-map'
```

## 12.2生产环境

```javascript
rules  支持写法
1.OneOf
    rules:[
        {
            OneOf: [
                //loader  正常来说一个文件只能被一个loader处理
            ]
        }
    ]

//注意  不能有两个配置文件处理同一个类型的文件
	可以拿出去 OneOf  外面
	
	
2.缓存
  babel缓存
      生产环境没有HMR  
      开启babel缓存
      			cacheDirectory:true  强制缓存   
      			改变资源名称
      			产生 bug 无法变化 解决
      			 output: {
                    filename: 'js/built.[hash:10].js',
                    path: resolve(__dirname, 'build')
                },
                又产生问题,同时使用一个hash值，如果重新打包,会导致所有缓存失效
                
                chunkhash  打包来源于同一个chunk,hash就不一样
                contenthash  根据文件内容生成
3.tree shaking
	去掉没有引用的代码
	去除无用代码
	必须使用es6模块化/  开启production
	作用 减少代码体积
	package.json
	"slideEffects": false    //都会干掉
	"slideEffects": ['*.css','*.less']
4.code split
	codesplit
	入口文件
	单入口和多入口
	如果有多入口，会打包成一个chunk
	
		//多入口,最终输出就有两个bundle
   			 main:'./src/index.js',
    		test: './src/js/test.js'
		 // 可以将node_modules中代码单独打包成一个chunk最终输出
          optimization:{
              splitChunks:{
                chunks: 'all'
              }
          },
  5.懒加载和预加载
	点击按钮的时候才加载
	$('#id').click({懒加载    预加载
        import(/*webpackChunkName:'test',webpackPrefetch:true*/'./test').then(({key})=>{
            console.log(mul(4,5))
        })
	})
	懒加载之后会使用缓存
	
6.PWA
	让离线也可以访问,渐进式网络开发应用程序
	workbox -->  workbox-webpack-plugin
	 cnpm i workbox-webpack-plugin -D
	 
	 plugins: [
      new WorkboxWebpackPlugin.GenerateSW({
      	帮我们生成servicework，
        clientsClaim:true,
        skipWaiting:true
      })
  ],
  		再入口js文件中注册servicework  处理兼容性
  		if('serviceWork' in navigator){
            window.addEventListener('load',()=>{
                navigator.serviceWorker.register('./service-worker.js')
                .then(()=>{
                    console.log('sw注册成功了')
                })
                .catch(()=>{
                    console.log('sw注册失败了')
                })
            })
        }
        配置json
         "eslintConfig":{
            "extends":"airbnd-base",
            "env":{
              "browser":true
            }
          }
          
          sw代码必须运行再服务器上
          -->nodejs
          -->npm i serve -g  安装
          	serve -s  build
 7.多进程打包
		thread-loader
		用在bable loader上面
		loader: 'thread-loader'，
		options:{
            workers: 2   //两个进程
		}
8.externals:{
    //忽略的库名字
    jquery: 'jQuery'
}
手动引入  cdn
9.dll
	动态链接库
	//引入nodejs path模块
//resolve用来拼接路径的方法
const { resolve } = require("path");
const webpack =  require('webpack')
module.exports = {
  
  entry: {
      jquery: ['jquery']
  },
  output: {
    filename: [name].js,
    path: resolve(__dirname, "dll"),
    library: '[name]_[hash]'
  },
  plugins:[
      new webpack.DllPlugin({
          name: '[name]_[hash]'   //暴露库的名称内容
          path: resolve(__dirname,'dll/manifest.json')  //文件输出路径
      })
  ]，
  mode: 'production'
};
 		///运行webpack  默认查找  webpack.config.js
 		运行其他   webpack --config  webpack.dll.js
 		
 		
 		然后再 webpack.config.js里卖弄
 		const webpack =  require('webpack')
 		//告诉那些库不参与打包
 		 new webpack.DllPlugin({
          manifest: resolve(__dirname,'dll/manifest.json')
      })
      
      
      //此时没有 jquery
      引入插件   add-assets-webpack-plugin
      new AddAssetsWebpackPlugin({
          filepath: resolve(__dirname 'dll/jquery.js')
      })
```

# 十三.配置详解

```javascript
webpack配置详解

const { resolve } = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
module.exports = {
    //入口起点
    // 1.string 单入口 './src/add.js'  打包形成一个chunk   chunk的名称默认值是 main
    // 2.array 多入口 ['./src/add.js','./src/index.js']  所有入口文件  HMR热更新使用
    // 3.object {index: './src/add.js',add:'./src/add.js'}  入口文件几个形成几个chunk 名称是key
    // -- >    特殊用法  {index: ['./src/add.js','./src/index.js'],add:'./src/add.js'} 多入口打包多个文件到一个
    entry: './src/add.js',
    //output出口
    //publicPath: '/'  所有引入资源的公共路径前缀   /src/img/a.jpg  一般用于生产环境
    //chunkfilename: '[name]_chunk.js'   非入口chunk的文件名称
    //library: '[name]'  //全局库向外暴漏  var   main = export{}
    //libraryTarget: 'window'   //  添加到哪个 browser上面  'common.js'  就是通过nodejs语法暴露
    output: {
        filename: 'js/[name].js',
        path: resolve(__dirname, 'build'),
        publicPath: '/'
    },
    module: {
        //loader的配置
        rules: [
            // {
            //     test: /\.js$/,
            //     exclude: /node_moudeles/,
            //     //include: resolve(__dirname,'src'),
            //     //优先执行 pre  //延后执行 post
            //     enforce: 'post',
            //     loader: 'eslint-loader'
            // }
            // {
            //     //只会匹配一个
            //     OneOf:[]
            // }
        ]
    },
    plugins: [
        new HtmlWebpackPlugin()
    ],
    mode: 'development',
    //解析模块的规则
    resolve: {
        //配置路径别名:写路径的时候可以少些  简写路径
        alias: {
            $js: resolve(__dirname, './src')
        },
        //配置省略文件后缀名的规则
        extensions: ['.js', '.json', '.css'],
        //告诉webpack去找那个目录 //默认 mode_modules
        //给一个绝对路径 resolve(__dirname,'../node_modules')
        modules: ['mode_modules']
    },
    //代码分割
    optimization:{
        splitChunks:{
            chunks: 'all',
            minSize:30 * 1024, //分割的chunk最小30kb,
            maxSiza:0, //最大没有限制
            minChunks: 1 ,//要提取的chunks最少引用一次
            maxAsyncRequest:5,//按需加载并行加载的文件的最大数量  
            maxInitialRequest: 3,//入口js文件最大的并行数量
            automaticNameDelimiter: '~',//名称连接符
            name:true,//可以使用内部命名规则
            cacheGroups:{//分割chuak的组
                //node_modules会被打包到 vendors的chunk中
                vendors:{
                    test: /[\\/]node_modules[\\/]/,
                    priority: -10
                },
                default:{
                    minChunks:2,
                    priority: -20,
                    //如果之前打包的模块，和之前被提取的模块是同一个，不会重复打包
                    reuseExistingChunk:true
                }
            } 
        }
    },
    devServer: {
        //项目构建后路径 运行代码的目录
        contentBase: resolve(__dirname, 'build'),
        //启动gzip压缩
        compress: true,
        port: 5000,
        open: true,
        //域名
        host: 'localhost',
        //开启  HMR 功能
        hot: true,
        //监视文件目录的变化,一旦文件变化就会reload
        watchContentBase: true,
        //监视文件 忽略某些文件
        watchOptions: {
            ignored: /node_modules/
        },
        //日志
        clientLogLevel: 'none',
        //除了一些基本的启动信息外，其他内容不要打印
        quiet: true,
        //如果出现错误，不要全屏提示~~~~
        overlay: false,
        //服务器代理  开发环境的跨域问题
        proxy: {
            //一旦devServer5000接收到/api/xxx的请求，就会把请求转发到另外一个服务器3000
            '/api': {
                target: 'http:localhost:3000',
                //发送请求时侯  请求路径重写   将/api/xxx  改为  /xxx
                pathRewrite: {
                    '^/api': ''
                }
            }
        }
    }
}
```

