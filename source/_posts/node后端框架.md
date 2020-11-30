---
title: Node框架
date:
updated:
type: "tags"
comments:
categories: Node
description: Node框架
keywords: Node框架
top_img: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2390865986,918155965&fm=26&gp=0.jpg
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2390865986,918155965&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.Nest.js

```js
Egg.js和Nest.js都是为企业级框架和应用
Egg.js基于Koa,Nest.js基于Express
Egg.js的文档优秀很多

安装
	npm i -g @nestjs/cli
	cnpm i -g @nestjs/cli
	yarn global add @nestjs/cli
使用脚手架创建项目
	nest new nestdemo01
	cd nestdemo01
	nest start//或者  npm run start
	http://localhost:3000/  访问结果
	
	热加载 npm run start:dev
```

## 1.1目录结构

```js
test  测试相关目录 
src  开发项目
	main.js  入口 全局中间件
	
```

## 1.2控制器

```js
nest g controller news
nest g  --help
@Controller('article')
export class ArticleController {
    @Get()
    index(){
        return "我是文章页面"
    }
    @Get('add')
    add(){
        return "增加新闻"
    }
}
```

## 1.3装饰器获取参数

```js
//get
    @Get("add")
    addData(@Query() query){
        console.log(query)
        return query
    }
    也可以通过 @Request 装饰器来获取  req.query获取
 //post
 	@Body装饰器来获取
 	
 //动态路由
 	@Get("id")
 	index(@Param() param){
        console.log(param)
 	}
 //获取固定属性
 	@Get("add")
 	index(@Query('id') id){
        console.log(id)  //只会获取id
 	}
 	//注意路由的匹配路由
 //路由模糊匹配
 	@Get("a*a")
```

## 1.4配置视图模板引擎

```js
引入 express平台
//引入express平台
import { NestExpressApplication } from '@nestjs/platform-express'

async function bootstrap() {
  //传入泛型方法
  const app = await NestFactory.create<NestExpressApplication>(AppModule);
  //配置静态资源
  app.useStaticAssets('public')
  //配置虚拟目录
  // app.useStaticAssets('public',{
  //   prefix:'/static/'
  // })
  await app.listen(3000);
}
```

## 1.5服务

```js
创建服务
nest g service news
```

# 2.Express

```
npm install express --save
```

## 2.1搭建服务器

```js
const express = require('express')
//实例化
const app = express()
app.get("/",(req,res)=>{
    res.send("你好expresss")
})
//动态路由
app.get("/article/:id",(req,res)=>{
    var id = req.params["id"]
    res.send(id)
})
//获取传值
app.get("/login",(req,res)=>{
    let query = req.query
    res.send(`username=${query.username};password=${query.password}`)
})
//监听端口
app.listen(3000)
```

## 2.2静态文件托管

```ejs
使用ejs模板
npm install ejs --save
//npm install -g supervisor
supervisor app.js
 	//变量
    let title = "你好呀"
    //对象
    let userinfo = {
        username:"张三",
        password:123456
    }
    //html

    //数组
    let arr = ['111111','222222','333333']
    let article = "<h3 style='color:red'>我是一个h3</h3>"
    res.render("index",{
        userinfo:userinfo,
        title:title,
        article:article,
        flag:false,
        arr:arr
    })
    
    //模版语法
    <h2>我是EJS模板引擎</h2>
    <p><%=title%></p>
    <div><%=userinfo.username%></div>
    <div><%=userinfo.password%></div>
    <div><%-article%></div>
    <!-- 判断语句 -->
    <%if(flag==true){%>
        <p>条件判断进入</p>
    <%}else{%>
        <p>条件判断无法进入</p>
    <%}%>
    <!-- 循环便利 -->
    <ul>
        <%for(var i = 0;i<arr.length;i++){%>
            <li><%=arr[i]%></li>
        <%}%>
    </ul>
    
    //模版引擎引入其他的ejs模版
    <%-include('footer.ejs')%>
	
    //指定模版位置
    // app.set("views")
    //配置html
    //修改ejs模版引擎的后缀为html
    app.engine("html",ejs.__express)
    //配置模板殷勤
    app.set("view engine","html")

	//配置静态资源托管
	app.use(express.static("static"))
    <link rel="stylesheet" href="css/index.css">

```

## 2.3中间件

```javascript
应用级中间件//一般用于权限控制
    //配置应用及中间件
    app.use((req,res,next)=>{
        console.log(new Date())
        next()
    })
路由及中间件
	app.get("/",(req,res,nest)=>{
		next() //匹配下一个路由
	})
错误处理中间件
	app.use((req,res,next)=>{
        res.status(404).send("404")
    })
内置中间件
	app.use(express.static("static"))
第三方中间件
	//使用第三方中间件获取post数据
	//body-parser
	var bodyParser = require('body-parser')
	app.use(bodyParser.urlencoded({ extended: false }))
	app.use(bodyParser.json())
	
	app.post("/login",(req,res)=>{
        var body = req.body
        console.log(req.body)
        res.send("提交数据"+body.username)
    })
    
    //express cookie    
    //cookie-parser
    var cookieParser = require("cookie-parser")
    app.use(cookieParser())
    res.cookie("username","zhangsan",{maxAge:1000*60*60})
    let body = req.cookies.username
    
	// //多个域名共享cookie  domain
	
	//cookie
    app.use(cookieParser("mima"))
    res.cookie("username","zhangsan",{maxAge:1000*60*60,signed:true})

//session存放在服务器
	express-session中间件
	cnpm install express-session --save
	var session = require("express-session")
	app.use(session({
        secret:"keyboard", //生成服务器端签名
        resave: false,  //强制存储
        saveUninitialized: true, 
        cookie: {
            secure:false,
            maxAge:1000*6
        } //配置session
    }))
     //session
    	req.session.username = "张三"
    //获取
    	req.session
    	参数
    	rolling:true  重新设置session过期的时间
	//销毁
		res.session.cookie.maxAge = 0
		
	//多服务器负载均衡  保存session
	//保存在mongodb里面  connect-mongo
	var MongoStore = require("connect-mongo")(session)
	 store: new MongoStore({
        url:'mongodb://admin:123456@127.0.0.1:27017/sessions',
        touchAfter: 24 * 3600   //24小时内只更新一次session
    })
```

## 2.4路由模块化

```javascript
//login.js    
    const express = require('express')
    //实例化
    var router = express.Router()
    router.get("/",(req,res)=>{
        res.send("页面首页")
    })
    router.get("/login",(req,res)=>{
        res.send("执行登录")
    })
    module.exports = router
//app.js
	const login = require('./routes/login')
    const express = require('express')
    const app = express()
    //挂载
    app.use("/",login)
    app.use("/login",login)
    app.listen(3000)
    
    //封装 一级路由
    	const login = require('./routes/login')
        const admin = require('./routes/admin')
        const api = require('./routes/api')
        const express = require('express')

        const app = express()
        //挂载
        app.use("/",login)
        app.use("/login",login)
        app.use("/admin",admin)
        app.use("/api",api)
        app.listen(3000)
     //封装 二级路由
     	const express = require('express')
        //实例化、
        const user = require('./admin/user')
        const nav = require('./admin/nav')
        var router = express.Router()
        router.use("/user",user)
        router.use("/nav",nav)
        router.get("/",(req,res)=>{
            res.send("后台管理页面")
        })
        module.exports = router
```

## 2.5应用程序生成器

```javascript
npx express-generator
cnpm install -g express-generator

//生成
express --view=ejs expressdemo
```

## 2.6文件上传

```javascript
npm install --save multer

const multer = require('multer')
const path = require('path')
//实例化
var router = express.Router()
var storage = multer.diskStorage({
    //目录
    destination: function(req,res,cb){
        cb(null,'static/uploads')
    },
    //文件名
    filename:function(req,file,cb){
        let extname = path.extname(file.originalname)
        cb(null,Date.now() + extname)
    }
})
//配置上传文件的中间件
var upload = multer({ storage:storage })

router.post("/doadd",upload.single("pic"),(req,res)=>{
    //获取表单传的数据
    res.send({
        body: req.body,
        file: req.file
    })
})

//封装
	const multer = require('multer')
	const path = require('path')
    let tools = {
        multer(){
            var storage = multer.diskStorage({
                //目录
                destination: function(req,res,cb){
                    cb(null,'static/uploads')
                },
                //文件名
                filename:function(req,file,cb){
                    let extname = path.extname(file.originalname)
                    cb(null,Date.now() + extname)
                }
            })
            //配置上传文件的中间件
            var upload = multer({ storage:storage })
            return upload
        }
    }
    module.exports = tools
    
    
    //按照日期生成上传文件的目录
    安装日期模块
    	const sd = require('silly-datetime')
		const mkdirp = require('mkdirp')
        destination: async (req,res,cb) => {
            let day = sd.format(new Date(), 'YYYYMMDD')
            let dir = path.join('static/uploads',day)
            //生成目录
            await mkdirp(dir);
            cb(null,dir)
        },
        //多文件上传
        var cpUpload = tools.multer().fields([{ name:"pic1"}, { name:"pic2"}])
```

## 2.7mongoose

```
链接mongodb时候一定给 文档或者数据库创建一个用户
mongoose链接时候用   创建的用户链接
```

### 2.7.1CRUD

```javascript
const mongoose = require('mongoose')

mongoose.connect('mongodb://root:123456@127.0.0.1:27017/mongoose',{ useNewUrlParser: true , useUnifiedTopology: true})

//定义Schema
var Userschema = mongoose.Schema({
    //表的映射
    name:String,
    age:Number,
    status:Boolean
})

//定义模型
//第一个参数首字母大写,和集合对应起来
//第二个参数把Schema放进去，默认匹配复数
//第三个参数表示对应匹配
var User = mongoose.model('User',Userschema,'user')

//查询users表的数据

User.find({},function(err,doc){
    if(err){
        console.log(err);
        return;
    }
    console.log(doc)
})
//增加数据
var  u = new User({
    name:"老王",
    age:20,
    status:false
})
u.save(function(err){
    if(err){
        console.log('增加失败')
        console.log(err)
        return;
    }
    console.log('增加成功')
}); //执行增加操作

//修改数据
User.updateOne({"name":"老王"},{"name":"老张"},function(err,data){
    if(err){
        console.log(err)
        return;
    }
    console.log(data)
})
//删除数据
User.deleteOne({"name":"老张"},(err,data)=>{
    if(err){
        console.log(err)
        return;
    }
    console.log(data)
})
```

### 2.7.2.默认参数 模块化 性能

```
//默认数据
	var Userschema = mongoose.Schema({
        //表的映射
        name:String,
        age:Number,
        status:{
            type:Number,
            default: 1 //默认数据
        }
    })
//模块化
	文件夹 model 
	下面  有
    	db.js负责连接数据库
    	user.js   user表的映射和模型
    	admin.js   admin表的映射和模型
```

### 2.7.3.预定义模式修饰符，自定义模式修饰符

```
预定义模式修饰符可以对数据进行格式化
    var Userschema = mongoose.Schema({
        //表的映射
        name:｛
        	type:String,
        	tirm:true    //表示去除空格
        ｝,
        age:Number,
        status:{
            type:Number,
            default: 1 //默认数据
        }
    })
    trim,lowercase,uppercase  
    
 自定义修饰符
 	比如数据库中地址保存 http://
 	
 	 age:{
         type:NUmber,
         set(params){
         		//增加数据
             //params获取参数
             if(!params){
                 return;
             }
             if(params.indexOf("http://") != "0"){
                 retunr http:// + parmas
             }
         },
         get(){
             //获取实例数据对数据进行格式化
         }
 	 }
```

### 2.7.4索引,内置crud方法,扩展静态方法和实例方法

```javascript
	//索引   优化查询的速度
		sn:{
			//唯一索引
            type:Number,
            unique:true
		},
		name:{
            //普通索引
            type:String,
            index:true
		}
   //内置CRUD方法
   		
   //在model里面书写方法，直接调用
   	静态方法
   		UserSchema.static.findBySn = function(sn,cb){
            this.find({"sn"}:sn,function(err,data){
                cb(err,docs)
            })
   		}
   	实例方法
   		UserSchema.methods.print= function(){
            console.log('实例方法')
   		}
```

### 2.7.5数据校验

```javascript
验证数据存储时候的合法性
	//内置数据校验
		sn:{
			//唯一索引
            type:Number,
            unique:true
		},
		age:{
            tyep:Number,
            max:150,
            min:0，
            macth    //必须满足正则表达式
		}
		name:{
            //普通索引
            type:String,
            index:true，
            required:true  //数据必须传入
            maxlength:20,   //最大20位
            minlength:8    //最小8位
            match:/^sn(.*)/i,
            //自定义验证器
            validate:function(sn){
                return sn.length >=10
            }
		},
		sex:{
            type:Number,
            //性别必须为男女  枚举是用在string类型上面
            enum:['男','女']
		}
```

### 2.7.6聚合管道 (aggregation pipe)

```javascript
对文档的组合查询
	//比如
		order order-item    //订单和具体的订单详情
		order的主表
		orderModel.aggregate([
            {
                $lookup:{
                    from: "order_item",
                    localField:"order_id",
                    foreignField:"order_id",
                    as:"items"
                }
            }
		],function(err,docs){
            if(err){
                return ;
            }
            console.log(docs)
		})
		
		//查找单个项目
		查询两次
		先去一个表中查找 id，然后使用id查询第二张表 然后关联
		
		//第二种办法、
		orderItemModel.aggregate([
            {
                $lookup:{
					from: "order",
                    localField:"order_id",
                    foreignField:"order_id",
                    as:"order-info"
                }
            },
            {
                $match:{
                    "id":"dsadsadsadsafsadfasdsa556fg4as65d"
                }
            }
            
		],function（err,docs）{
            if(err){
                return;
            }
            console.log(docs)
		})
		
		//mongoose中获取 objcetId
		mongoose.Types.ObjectId


//查询数组
	User.aggregate([
    {
      $lookup: {
        from: "resource",
        localField: "resource",
        foreignField: "_id",
        as: "items",
      },
    },
    {
      $project:{ _id:0,username:1,items:1}
    },
    {
      $match: {
        "username": username,
      },
    },
  ],(err,docs)=>{
    return res.send(docs)
  });
```

### 2.7.7populate

```javascript
类似聚合管道

**`Query.populate(path, [select], [model], [match], [options])`**
    
    const arr = await User.find({username:username},{password:0,username:0}).populate({
    path:'resource',//表
    model: Resource,//关联的model
    select: {},//筛选关联表的字段
    // populate:{ path:'resource'},
  }).exec()
```

# 3.Koa

```javascript
Nodejs是一个异步的世界，回调函数形式的异步编程，
	会带来许多问题
		1.callback嵌套问题，
		2.异步编程中可能同步调用callback返回数据，带来不一致性
		
		Koa解决这些问题
		而且koa框架中不绑定任何中间件
		
		最大的特点可以避免异步嵌套
		安装
		npm install --save koa 
		
		const koa = require('koa')

        //实例化
        var app = new koa()

        app.use(async (ctx)=>{
            ctx.body = "你好 koa"
        })

        //监听端口
        app.listen(3000)
```

## 3.1路由

```javascript
koa-router   //需要引入路由
npm install --save koa-router
	//路由的简单使用
		const koa = require("koa");
        var Router = require("koa-router");
        //实例化
        var app = new koa();
        var router = new Router();
        // app.use(async (ctx)=>{
        //     ctx.body = "你好 koa"
        // })

        //配置路由
        //ctx表示上下文继承了 req,res的信息
        router.get("/", async (ctx) => {
            ctx.body = "首页"; //返回数据
          })
        router.get("/news", async (ctx) => {
            ctx.body = "新闻页面";
        });

        //启动路由
        	app
            .use(router.routes())  //启动路由
            .use(router.allowedMethods()); //推荐配置 当所有路由中间件最后调用时候, 
        //监听端口
        	app.listen(3000);
        
        //获取get传值
            //从ctx中读取get传值
            console.log(ctx.query)  //获取的是对象
            console.log(ctx.querystring)  //获取的是字符串 url
            console.log(ctx.request)
            
       //动态路由
            router.get('/newscontent/:id',async (ctx) =>{
                console.log(ctx.params)
            })
```

## 3.2中间件

```javascript
//应用及中间件
	app.use(async (ctx,next)=>{
        console.log(ctx.query)
        await next()
    })
//路由中间件
	
//错误处理中间件
	无论写到哪里，都匹配  和express有区别  
//错误处理中间件
    app.use(async (ctx,nest)=>{
        console.log('错误处理中间件')
    })
	
```

## 3.3koa post提交数据

```javascript
koa-bodyparser

 //原生nodejs封装
      exports.getPostdata = function getPostdata(ctx) {
        return new Promise((resolve,reject)=>{
            try{
                var str = ''
                ctx.req.on('data',function(chunk){
                    str += chunk
                })
                ctx.req.on('end',function(){
                    resolve(str)
                })
            }catch(err){
                reject(err)
            }

        })
    };
//中间件 body-bodyparser
	const bodyParser = require("koa-bodyparser");
	app.use(bodyParser())
    ctx.body = ctx.request.body

```

## 3.4静态资源中间件

```
//中间件  koa-static
	<link rel="stylesheet" href="/css/index.css">
    const staic = require("koa-static")
	app.use(staic('static'))
//使用模板
	//使用模板
    app.use(views('views',{
        extension:'ejs'
    }))

```

## 3.5模板引擎(art-template)

```javascript
npm install --save art-template
npm install --save koa-art-template
const render = require("koa-art-template")
const path = require("path")
//引入模板引擎中间件
render(app,{
    root: path.join(__dirname,"views"),
    extname:'.html',
    debug:process.env.NODE_ENV !== 'production' //是否开启调试模式
})
router.get("/", async (ctx) => {
    // ctx.body = "首页"; //返回数据
    await ctx.render("index")
})
//一部分语法和比较相似
```

## 3.6cookie和session

```javascript
koa中cookie中自动集成
	ctx.cookies.set(name,value,{option})

//中间件 koa-session
	npm install koa-session --save
	//引入
    const session = require('koa-session')
    //配置
    const CONFIG = {
        key:"",
        maxAge:864000,
        overwrite:ture,
        httpOnly:true,//只有服务器端才可以获取
        signed:true,
        rolling:false,//每次访问都更新
        renew:false//快到期 重新设置
    }
    //中间件
    
    //设置
    ctx.session.username = ""
	//获取
	ctx.session.username
```

## 3.7koa操作数据

```javascript
const  dbInfo  = {
    host: "127.0.0.1",
    port: "27017",
    dbName: "xxx"
};
const {
    dbInfo
} = require("../../config/server.config.js");
const MongoClient = require('mongodb').MongoClient;
class mongodbHelper {
    /***连接数据库***/
    connection() {
        return new Promise(function (resolve, reject) {
            var url = `mongodb://${dbInfo.host}:${dbInfo.port}/${dbInfo.dbName}`;
            MongoClient.connect(url, {
                useUnifiedTopology: true,
                useNewUrlParser: true
            }, function (err, db) {
                if (err) {
                    reject(err);
                }
                console.log("连接成功！", url);
                resolve(db);
            });
        })
    }
    /**关闭数据库连接
     *db:数据库实例
     ***/
    close(db) {
        db.close;
    }
    /**创建集合
     * db:数据库实例
     * collectionName：集合名称
     * **/
    createCollection(collectionName) {
        return new Promise((resolve, reject) => {
            this.connection().then(db => {
                var dbase = db.db(dbInfo.dbName);
                dbase.createCollection(collectionName, function (err, res) {
                    db.close();
                    if (err) {
                        reject(err);
                    }
                    resolve(1);
                });
            }).catch(err => {
                reject(err);
            })

        })
    }
    /**添加一条数据
     * collectionName：集合名称
     * data：数据，Object
     * */
    insertOne(collectionName, data) {
        return new Promise((resolve, reject) => {
            this.connection().then(db => {
                var dbase = db.db(dbInfo.dbName);
                dbase.collection(collectionName).insertOne(data, function (err, res) {
                    db.close();
                    if (err) {
                        reject(err);
                    }
                    resolve(1);
                });
            }).catch(err => {
                reject(err);
            })
        })
    }
    /**添加多条数据
     *collectionName：数据集合
     *datas：数据，Array
     ****/
    insertMany(collectionName, datas) {
        return new Promise((resolve, reject) => {
            this.connection().then(db => {
                var dbase = db.db(dbInfo.dbName);
                dbase.collection(collectionName).insertMany(datas, function (err, res) {
                    db.close();
                    if (err) {
                        reject(err);
                    }
                    resolve(datas.length);
                });
            }).catch(err => {
                reject(err);
            })
        })
    }
    /**查询
     *collectionName：集合名称
     *search：查询条件
     * **/
    find(collectionName, search) {
        return new Promise((resolve, reject) => {
            this.connection().then(db => {
                var dbase = db.db(dbInfo.dbName);
                dbase.collection(collectionName).find(search).toArray(function (err, result) {
                    db.close();
                    if (err) {
                        reject(err);
                    }
                    resolve(result);
                });
            }).catch(err => {
                reject(err);
            })
        })
    }
    /**修改数据
     * collectionName：表名
     * query：查询条件，Object
     * update：更新的数据，Object
     * option={upsert, multi}
     */
    update(collectionName, query, update) {
        return new Promise((resolve, reject) => {
            this.connection().then(db => {
                var dbase = db.db(dbInfo.dbName);
                dbase.collection(collectionName).updateOne(query, {
                    $set: update
                }, function (err, res) {
                    db.close();
                    if (err) {
                        reject(err);
                    }
                    resolve(1);
                });
            }).catch(err => {
                reject(err);
            })
        })
    }

    /**修改数据
     * collectionName：表名
     * query：查询条件，Object
     * update：更新的数据，Object
     * option={upsert, multi}
     */
    delete(collectionName, obj) {
        return new Promise((resolve, reject) => {
            this.connection().then(db => {
                var dbase = db.db(dbInfo.dbName);
                dbase.collection(collectionName).remove(obj, function (err, res) {
                    db.close();
                    if (err) {
                        reject(err);
                    }
                    resolve(1);
                });
            }).catch(err => {
                reject(err);
            })
        });
    }
}


module.exports = mongodbHelper

//2.
	const dbHelper = require("./mongodbHelper .js")();
class userModel {
    constructor() {
        this.tbName = "tb_user";
        this.email = "";
        this.userName = "";
        this.loginName = "";
        this.email = "";
        this.phone = "";
        this.time = "";
    }
    async add(user) {
        if (!user) {
            user = {
                userName: this.userName,
                loginName: this.loginName,
                email: this.email,
                phone: this.phone,
            }
        }
        user.time = new Date();
        let result = await dbHelper.insertOne(this.tbName, user);
        return result;
    }
    async getOne(searchObj) {
        let list = await this.getList(searchObj);
        if (list && list.length) {
            return list[0];
        }
        return null;
    }
    async getList(searchObj) {
        let list = await dbHelper.find(this.tbName, searchObj);
        return list;
    }
}
module.exports = userModel;
```

## 3.8使用koa脚手架

```js
npm install koa-generator -g
koa koademo

//路由模块化
 配置子路由
 module.exports = router
 router.use('/admin',admin.routes)
```

# 4.Egg

```shell
基于nodejs和koa的一个企业级应用开发框架
$ mkdir egg-example && cd egg-example
$ npm init egg --type=simple
$ npm i

$ npm run dev
$ open http://localhost:7001
```

## 1.路由控制器

```js
//controller 目录下新建 product.js
const Controller = require('egg').Controller
class ProductController extends Controller{
    async index(){
        const { ctx } = this;
        ctx.body = 'product'
    }
}
module.exports = ProductController

//在router.js里面注册
module.exports = app => {
  const { router, controller } = app;
  router.get('/', controller.home.index);
  router.get('/product',controller.product.index)
};
//实现路由
```

## 2.路由传参

```js
//GET
async detail(){
    const { ctx } = this
    //ctx.query 来获取参数 键值对 json格式
    ctx.body = ctx.query
}
async detail2(){
    const { ctx } = this
    //ctx.params 来获取动态参数 键值对 json格式
    ctx.body = ctx.params
}

//可以在config.default.js开启或者关闭csrf
config.security = {
    csrf:{
      enable: false
    }
  }

//POST
 async create(){
     const { ctx } = this
     //ctx.request.body来获取参数 键值对 json格式
     ctx.body = ctx.request.body
 }
async update(){
    const { ctx } = this
    //ctx.params.id 来获取动态参数 键值对 json格式
    ctx.body = ctx.params.id
}


```

## 3.Service

```js
//业务逻辑抽象层
const Service = require('egg').Service

class ProductService extends Service{
    async index(){
        return {
            id:100,
            name:'test'
        }
    }
}
module.exports = ProductService

//在Controller调用Service
const res = await ctx.service.product.index();
```

## 4.引入模版引擎

```js
npm i egg-view-nunjucks --save


// config/plugin.js
//exports.nunjucks = {
//  enable: true,
//  package: 'egg-view-nunjucks',
//};

// {app_root}/config/config.default.js
exports.view = {
  defaultViewEngine: 'nunjucks',
  mapping: {
    '.nj': 'nunjucks',
  },
};
config.view = {
    defaultViewEngine: 'nunjucks',
    mapping: {
      '.nj': 'nunjucks',
    },
  };

//传递参数
 async index(){
     const { ctx } = this;
     //调用service服务
     // const res = await ctx.service.product.index();
     await ctx.render('index.nj',{ name: 'view test' })
     // ctx.body = res
 }
```

# 5.静态资源

```js
//静态资源文件放在 public里面
//引入的时候 /public/css/css.css
```

# 6.操作数据库

## 1.创建sql

```sql
create DATABASE egg_atricle;
use egg_atricle;
create TABLE article(
	id INT(10) not null auto_increment,
	img text DEFAULT NULL COMMENT '缩略图',
	title VARCHAR(80) DEFAULT NULL COMMENT '文章标题',
	summary VARCHAR(300) DEFAULT NULL COMMENT '文章简介',
	content text DEFAULT null COMMENT '文章内容',
#	create_time TIMESTAMP DEFAULT NULL COMMENT '发布时间',
	PRIMARY KEY(id)
)ENGINE=INNODB AUTO_INCREMENT=1 COMMENT '文章表'
```

## 2.连接数据库

```js
//egg-myql
npm i --save egg-mysql

//开启插件
// config/plugin.js
exports.mysql = {
  enable: true,
  package: 'egg-mysql',
};

//单数据源
exports.mysql = {
  // 单数据库信息配置
  client: {
    // host
    host: 'mysql.com',
    // 端口号
    port: '3306',
    // 用户名
    user: 'test_user',
    // 密码
    password: 'test_password',
    // 数据库名
    database: 'test',
  },
  // 是否加载到 app 上，默认开启
  app: true,
  // 是否加载到 agent 上，默认关闭
  agent: false,
};
//使用方式
await app.mysql.query(sql, values); // 单实例可以直接通过 app.mysql 访问


//多数据源
exports.mysql = {
  clients: {
    // clientId, 获取client实例，需要通过 app.mysql.get('clientId') 获取
    db1: {
      // host
      host: 'mysql.com',
      // 端口号
      port: '3306',
      // 用户名
      user: 'test_user',
      // 密码
      password: 'test_password',
      // 数据库名
      database: 'test',
    },
    db2: {
      // host
      host: 'mysql2.com',
      // 端口号
      port: '3307',
      // 用户名
      user: 'test_user',
      // 密码
      password: 'test_password',
      // 数据库名
      database: 'test',
    },
    // ...
  },
  // 所有数据库配置的默认值
  default: {

  },

  // 是否加载到 app 上，默认开启
  app: true,
  // 是否加载到 agent 上，默认关闭
  agent: false,
};


//使用方式
const client1 = app.mysql.get('db1');
await client1.query(sql, values);

const client2 = app.mysql.get('db2');
await client2.query(sql, values);


//使用实例
async index() {
    const { ctx,app } = this;
    const res = await app.mysql.select('article')
    console.log(res)
    ctx.body = res;
  }
}
```

