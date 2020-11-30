---
title: Node基础
date:
updated:
type: "tags"
comments:
categories: Node
description: Node基础
keywords: Node基础
top_img: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=3023339532,6928380&fm=26&gp=0.jpg
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=3023339532,6928380&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 一，命令提示符常用命令

```
1.  清屏  cls
2.  推出 cmd exit
3.查看当前文件夹中间的所有文件 dir
4.进入文件  cd
5.返回上一级目录  cd..
6.返回根目录    cd/ 或 cd\
7.创建文件夹 md 
8.删除文件夹 rd
9.创建文件 echo>文件名后缀
10.删除文件  del 文件名
```

# 二，模块

## 1.http 

```
#### try {

//可能会导致错误的代码

#### } catch(error){

	在错误发生时候怎么处理

#### }finally{

	报错也执行//

#### }
```

```js
let http = require('http');
let a = http.createServer((request,response)=>{
    response.end('hello nodejs')
})
a.listen(88);

设置请求头
res.writeHead(200, { 'Content-Type': 'text/html;charset=UTF8' })
let http = require('http');

let a = http.createServer((request,response)=>{
	response.writeHead(200,{'Content-Type’:'test-plain'})
	res.write('this is node')
    response.end('hello nodejs')
})
a.listen(88);
1.加载 http 模块
2.调用 http.createServer() 方法创建服务，方法接受一个回调函数，回调函数中有两个参数，第一个是请求体，第二个是响应体。
3.在回调函数中一定要使用 response.end() 方法，用于结束当前请求，不然当前请求会一直处在等待的状态。
4.调用 listen 监听一个端口


参数接受 get、
当以 GET 请求服务器的时候，服务器可以通过 request.mothod 来判断当前的请求方式并通过 request.url 来获取当前请求的参数

参数接受 post
事件监听
  let post = ''
req.on('data', function(chunk){    
        post += chunk;
    });
    
     req.on('end', function(){    
        post = querystring.parse(post);
        res.end(util.inspect(post));
    });
```



```javascript
1. http 模块

引入模块
const http = require('http');

创建服务器
const app = http.createServer(function(request, response){
    request 代表请求
    response 代表响应
    response.writeHead(状态码, {'Content-Type':'文件类型;charset=UTF8'}) 写响应头
    response.write(); 给浏览器写内容 可以多次使用
    response.end(); 结束响应 只能使用一次
    
    
    http模块解析 post请求参数
    request.method == POST 判断是否是POST请求
    let data = '';
    request.on('data', function(chunk){
        data += chunk;
    })
    request.on('end'), function(){
        数据接收完毕的回调
    }
})
设置监听端口
app.listen(port)
```

## 2. fs模块（文件操作）

```javascript
fs.stat() 检查文件是 目录 还是 文件
fs.mkdir() 创建一个目录
fs.unlink() 删除单独一个文件
fs.readFile() 读取一个文件
fs.readdir() 读取目录
fs.rename() 替换文件名字
fs.rmdir() 删除一个目录
fs.appendFile() 向文件中追加内容，不会覆盖
fs.writeFile(路径, 内容, 回调函数) 创建一个文件，并写入内容

fs.stat(文件路径, function(err, files){
    files.isFile()  检查是否是一个文件
    files.isDirectory() 检查是否是一个目录
})

fs.mkdir(创建目录的路径, function(err){
    
})

fs.unlink(删除文件的路径, function(err){
    
})

fs.readFile(读取文件的路径, function(err, data){
    err 错误
    data 拿到的文件的内容
})

fs.readdir(目录路径, function(err, files){
    files 数组 存放所有目录下的文件
})

fs.rename(要该的文件地址, 改之后文件存放的地址, function(err){
    
})

fs.rmdir(删除目录的地址（注：空目录才可以删除）, function(err){
    
})

fs.appendFile(追加内容的文件名, 追加的内容 ,function(err){
    
})

fs.writeFile(创建文件的路径, 文件的内容, function(err){
    
})

//流的方式读取文件
    const fs = require('fs')

    var readStream = fs.createReadStream('./index.txt')
    var count = 0;
    var str = ''
    //监听数据
    readStream.on('data',(data)=>{
        str += data;
        count++;
    })
    //监听读取完毕
    readStream.on('end',()=>{
        console.log(str)
        console.log(count)
    })
    //监听读取错误
    readStream.on('error',(err)=>{
        console.log(err)
    })

	//流的方式写入文件

    const fs = require('fs')
    var str = "你睡撒大大是a你睡撒大大是a你睡撒大大是a"

    var writeStream = fs.createWriteStream('./output.txt')
    writeStream.write(str)

    //标记写入完成
    writeStream.end();
    //监听写入完成
    writeStream.on('finish',()=>{
        console.log('写入完成')
    })
	
	//管道复制
	const fs = require('fs')
    var readStream = fs.createReadStream('./1.jpg')
    var writeStream = fs.createWriteStream('./image/2.jpg')
    readStream.pipe(writeStream)
```

## 3.querystring模块（解决中文乱码）

```javascript
const querystring = require('querystring');
querystring.unescape(目标字符串);
```

## 4. url模块（解析GET请求的参数）

```javascript
const url = require('url');
url.parse(字符串, 是否转换为对象).query;
url.parse(字符串, 是否转换为对象).pathname; 返回除掉GET传值的路由
```

## 5. 第三方模块的使用

```javascript
npm init 生成项目配置文件 package.json
{
  "name": "项目名称",
  "version": "版本号",
  "description": "描述",
  "main": "入口文件",
  "scripts": {
    "test": "node app.js" 快捷指令  npm run scripts里面的属性名
  },
  "keywords": [],
  "author": "作者",
  "license": "ISC 许可",
  "dependencies": { 运行依赖
    "art-template": "^4.13.2",
    "express": "^4.17.1",
    "request": "^2.88.0"
  }
  "devDependencies":{
      开发依赖
  }
}
使用 npm install 第三方包名称 下载包
npm install 包 --save === npm install 包 -S
npm install 包 --save-dev === npm install 包 -D

npm 服务器架设在国外 国内下载包可能会速度很慢或者直接下载不了  我们可以选择cnpm 淘宝镜像
淘宝镜像安装方法：
	CMD 中 输入以下指令
    npm install -g cnpm --registry=https://registry.npm.taobao.org
淘宝镜像安装完成以后就可以使用 cnpm 来下载 后续指令 跟 npm 同理
```



## 6. request 模块(发送http请求)

```javascript
// 第三方模块 npm install request -S
const request = require('request');

request.get(url, function(err, response, data){
    err  错误
    response 响应
    data 请求到的数据
})

例子：服务器代理 解决跨域
const http = require('http');
const url = require('url');
const fs = require('fs');
const request = require('request');
const app = http.createServer((req, response) => {
    let router = url.parse(req.url, true).pathname;
    if(router == "/" || router == "index" || router == "index.html"){
        fs.readFile(`${__dirname}/index.html`, (err, data) => {
            try{
                response.end(data);
            }catch(err){
                console.log(err);
            }
        })
    }
    if(router == '/rcGame'){
        request.get('https://pujie1213.top:424/rcGame', (err, res, data) => {
            console.log(response);
            response.end(data);
        })
    }
})
app.listen(93);
```

## 7. https模块（配置SSL证书）

```javascript
const https = require("https");
const option = {
    key: fs.readFileSync .key  同步读取密钥
    cert .pem
}
const app = https.createServer(option, function(req, res){
    
})
app.listen(port);
```

## 8. formidable（处理文件上传）

```javascript
let form = new formidable.IncomingForm();
form.uploadDir = 存放文件的路径
form.keepExtensions = true;  是否保存上传文件的后缀名 默认值为false
form.parse(requset, function(err, response, files){
    files.file.path 本地上传文件的路径 有乱码的文件名 方便fs.rename修改名字
})


案例：
let form = new formidable.IncomingForm();
form.uploadDir = `${__dirname}/images`;
form.keepExtensions = true;
form.parse(req, (err, response, files) => {
    let num1 = files.file.path.indexOf('node\\') + 5;
    let data = files.file.path.substring(num1);
    fs.rename(data, `images/${files.file.name}`, (err) => {
        try{
            console.log('文件上传成功，名字修改成功');
        }catch(err){
            console.log(err);
        }
    })
})
```

## 9. express（WEB框架）

```javascript
npm install express -S

const express = require('express');
生成对象
const app = express();
配置路由
app.get('路由名称', function(req, res, next){
    req 请求
    res 响应
    next 跳到下一个中间件
})
app.post() 同上

app.listen(port) 监听端口

内置中间件
app.use(express.static(静态资源路径))
```

## 10. CORS(跨域资源访问)

```javascript
app.all('*', function(req, res, next){
    res.header("Access-Control-Allow-Origin", "*");  
	res.header("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");
})

cors 模块
cnpm install cors -S
const cors = require('cors');

app.use(cors());
```

## 11. morgan模块（日志管理）

```javascript
cnpm install morgan -S
const morgan = require("morgan");

app.use(morgan('dev'));  放在路由的上面
```

## 12. web服务器案例

```javascript
const http = require('http');

const url = require('url');

const fs = require('fs');

const formidable = require('formidable');

const app = http.createServer((req, res) => {
    // 获取请求路由（不附带参数）
    let router = url.parse(req.url).pathname;

    if (router == '/') {
        fs.readFile(`${__dirname}/public/file.html`, (err, data) => {
            if (err)
                throw err;
            else {
                res.writeHead(200, { "Content-Type": "text/html;charset=UTF8" });
                res.end(data);
                return;
            }
        })
    } else if (router == '/file') {
        console.log(1);
        fs.readFile(`${__dirname}/public/file.html`, (err, data) => {
            if (err)
                throw err;
            else {
                res.writeHead(200, { "Content-Type": "text/html;charset=UTF8" });
                res.end(data);
                return;
            }
        })
    } else if (router == '/favicon.ico') {
        fs.readFile(`${__dirname}/favicon.ico`, (err, data) => {
            try {
                res.end(data);
                return;
            } catch (err) {
                console.log(err);
            }
        })
    } else if (/(css|js)/g.test(router)) {
        fs.readFile(`${__dirname}/public${router}`, (err, data) => {
            try {
                res.end(data);
                return;
            } catch (err) {
                console.log(err);
            }
        })
    } else if (req.method == "POST" && router == '/login') {
        let data = '?';
        req.on('data', (chunk) => {
            data += chunk;
        })
        req.on('end', () => {
            let datas = url.parse(data, true).query;
            console.log(datas);
        })
    } else if (req.method == 'POST' && router == '/upload'){
        let form = new formidable.IncomingForm();

        form.uploadDir = `${__dirname}/images`;

        form.keepExtensions = true;

        form.parse(req, (err, response, files) => {
            let num1 = files.file.path.indexOf('node\\') + 5;
            let data = files.file.path.substring(num1);
            fs.rename(data, `images/${files.file.name}`, (err) => {
                try{
                    console.log('文件上传成功，名字修改成功');
                }catch(err){
                    console.log(err);
                }
            })
        })
    } else {
        res.end('404 not found');
        return;
    }
})
app.listen(82, function () {
    console.log('server is running at port:82');
});
```

## 13.art-template

```javascript
app.all('*',(res,res,next)=>{
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Methods", "PUT,POST");
    // res.header("Access-Control-Allow-Headers", "Content-Type,Content-Length, Authorization, Accept,X-Requested-With");
    next();
})
app.use(morgan('dev'));  //日志
app.get('/', (req, res) => {
    fs.readFile(`${__dirname}/template.html`,(err,data)=>{
        try{ 
            var datas = String(data);
            request.get('https://pujie1213.top:424/rcGame', (err, response, body) => {
                let json = JSON.parse(body);
                try {
                    let a = art.render(datas, json);
                    res.end(a);
                } catch (err) {
                    console.log(err)
                }
            })
        }catch(err){
            console.log(err)
        }
    })
   
})

app.listen(3000, () => console.log('Server 3000 is running...'))
```

## 14.supervisor

```
npm install -g supervisor
//监听node服务的改变 实现热部署
supervisor server.js
```



# 三，写一个服务器



```javascript
const http = require('http');

const url = require('url');

const fs = require('fs');

const formidable = require('formidable');

const app = http.createServer((req, res) => {
    // 获取请求路由（不附带参数）
    let router = url.parse(req.url).pathname;

    if (router == '/') {
        fs.readFile(`${__dirname}/public/file.html`, (err, data) => {
            if (err)
                throw err;
            else {
                res.writeHead(200, { "Content-Type": "text/html;charset=UTF8" });
                res.end(data);
                return;
            }
        })
    } else if (router == '/file') {
        console.log(1);
        fs.readFile(`${__dirname}/public/file.html`, (err, data) => {
            if (err)
                throw err;
            else {
                res.writeHead(200, { "Content-Type": "text/html;charset=UTF8" });
                res.end(data);
                return;
            }
        })
    } else if (router == '/favicon.ico') {
        fs.readFile(`${__dirname}/favicon.ico`, (err, data) => {
            try {
                res.end(data);
                return;
            } catch (err) {
                console.log(err);
            }
        })
    } else if (/(css|js)/g.test(router)) {
        fs.readFile(`${__dirname}/public${router}`, (err, data) => {
            try {
                res.end(data);
                return;
            } catch (err) {
                console.log(err);
            }
        })
    } else if (req.method == "POST" && router == '/login') {
        let data = '?';
        req.on('data', (chunk) => {
            data += chunk;
        })
        req.on('end', () => {
            let datas = url.parse(data, true).query;
            console.log(datas);
        })
    } else if (req.method == 'POST' && router == '/upload'){
        let form = new formidable.IncomingForm();

        form.uploadDir = `${__dirname}/images`;

        form.keepExtensions = true;

        form.parse(req, (err, response, files) => {
            let num1 = files.file.path.indexOf('node\\') + 5;
            let data = files.file.path.substring(num1);
            fs.rename(data, `images/${files.file.name}`, (err) => {
                try{
                    console.log('文件上传成功，名字修改成功');
                }catch(err){
                    console.log(err);
                }
            })
        })
    } else {
        res.end('404 not found');
        return;
    }
})
app.listen(82, function () {
    console.log('server is running at port:82');
});
```

# 四。包的导入和使用

```
导入  exports.age = 1;
	exports.age2 = 2;
	exports.age = 3;
	
	module.export = {
	
	}
	
	
引入  require('url相对地址')
```

# 五.npm

```
npm init;
初始化 npm
npm install md5
```

# 六  服务器代理

```
if(dd == '/rcGame'){
    		request.get('https://pujie1213.top:424/rcGame',(err,response,data)=>{
    			res.end(data);
    		})
    	}
    	
    	var xhr = new XMLHttpRequest();
	xhr.open('get','http://localhost:300/rcGame',false);
	xhr.send();
	console.log(xhr.responseText);
```

# 七 Nginx

```
Nginx是一个高性能的HTTP和反向代理服务器（反向代理就是通常所说的web服务器加速，它是一种通过在繁忙的web服务器和internet之间增加一个高速的web缓冲服务器来降低实际的web服务器的负载），Nginx由俄罗斯程序员利用C语言开发，以稳定、低系统资源消耗闻名，腾讯、百度、阿里、京东、网易等均有部署使用。此外，在高连接并发的情况下，Nginx是Apache的不错替代品，其能够支持高达50000个并发连接数的响应。
```

## 7.1Nginx的配置

# 八爬虫

```
安装request和
它的功能就是建立起对目标网页的链接，并返回相应的数据，这个不难理解。

cheerio依赖包
cheerio的功能是用来操作dom元素的，他可以把request返回来的数据转换成可供dom操作的数据，更重要的cheerio的api跟jquery一样，用$来选取对应的dom结点，
```

## 1.发请求  拿页面

```
request  传入地址

关于编码的问题 可以导入 iconv-lite  包 解决,
const bufs = iconv.decode(body,'gb2312');
const html = bufs.tostring('utf8');

有必要在url 请求 第二个参数传{ encodding: null}
```

## 2.操作数据

```
const $ = cheerio.load(res)  //res为数据  加载之后才可以用 jqury
利用 $找到目标位置 
$('').each(i,item)=>{$(item).attr('href')}
拿到链接 

然后利用异步的请求  async  await 执行 Promise  发请求  放到 循环里面
定义一个对象 将内容放在里面


这只是拿到一页的数据  分析多少页 
利用 异步减少程序错误率
arr.reduce((rs,url)=>{
	retrun re.then(()=>{
		return new Promise(async (resolve)=>{
			await getList(url);
			resolve();
		})
	})
},Promise.resolve());

```

## 3.保存文件

```
将 fs.appendFileSync('./public/index.html',movie);  保存到这个地址
```

# 九，判断登陆

```javascript
var express = require('express');
var app = express.Router();

/* GET home page. */
var mysql = require('mysql');
let conn = mysql.createConnection({
	host:'localhost',
	user: 'root',
	password: 'root',
	database: 'login'
})

conn.connect(()=>{
	console.log('数据库链接成功');
})

app.post('/login',(req,res)=>{
	let username = req.body.username;
	let password = req.body.password;
	console.log(username,password);
	conn.query(`select * from users1 where username = '${username}' and password = '${password}'`,(err,data)=>{
		if(err) throw err;
		else{
			if(data.length != 0){
				res.send('success')
			}else{
				res.send('error')
			}
		}
	})
})
module.exports = app;
```

# 十登陆验证 

```javascript
 <script type="text/javascript" src="/logincheck"></script>



app.get('/logincheck',(req,res)=>{
	let cookie = req.cookies.username;
	if(!cookie){
		res.send(`alert('请登陆之后，在进入');location.href = "/admin/pages/login.html"`);
	}else{
		res.send('');
	}
})
```

# 十一.操作MongoDB数据库(mogondb驱动)

```javascript
npm init
cnpm install mongodb --save
//cnpm 
npm install -g cnpm --registry=https://registry.npm.taobao.org
//如果vscode不行的话
需要更改策略
get-ExecutionPolicy   //获取策略
set-ExecutionPolicy RemoteSigned  //设置策略
//代码提示
npm install --save-dev @types/node
npm Intellisense

```

```javascript
const { MongoClient } = require("mongodb");

//定义数据库的连接地址
const url = "mongodb://admin:123456@127.0.0.1:27017";

//定义要操作的数据库
const dbname = "mongodomo";

//实例化
const client = new MongoClient(url, { useUnifiedTopology: true });

//链接数据库n

client.connect((err) => {
  if (err) {
    console.log("连接失败");
    return;
  }
  console.log("连接数据库成功");
  let db = client.db(dbname);

  //查找数据
  //异步
  db.collection("info")
    .find({})
    .toArray((err, data) => {
      console.log(data);
      //操作完成后完毕数据库连接
      client.close();
    });
    增加数据
    db.collection("info").insertOne({username:"nodejs操作",age:25},(err,result)=>{
        if(err){
            console.log("增加失败")
            return;
        }
        console.log("增加成功")
        console.log(result)
        client.close()
    })
});

```

# 十二.Node应用的场景

```
1. Web开发：Express + EJS + Mongoose/MySQL
2. Web聊天室(IM)：Express + Socket.io
3. Web爬虫：Cheerio/Request
4. Web博客：Hexo
5. Web论坛: nodeclub
6. Web幻灯片：Cleaver
7.前端包管理平台: bower.js
8.OAuth认证：Passport
9.定时任务工具: later
10. 浏览器环境工具: browserify
11.命令行编程工具：Commander
12.客户端应用工具: node-webwit
13.操作系统: node-os
14.Meteor 
```

# 十三.搭建博客

```javascript
npm install -g hexo-cli
hexo init myblog  //初始化
http://localhost:4000/

//生成密钥
git config --global user.name "yourname"
git config --global user.email "youremail"
git config user.name
git config user.email
ssh-keygen -t rsa -C "youremail"

//将hexo部署到GitHub
//打开站点配置文件 _config.yml
npm install hexo-deployer-git --save
//deploy:
  type: git
  repo: https://github.com/zcz147258/zhangcz.github.io.git
  branch: master
  //部署
hexo clean清除了你之前生成的东西，也可以不加。
hexo generate 顾名思义，生成静态文章，可以用 hexo g缩写
hexo deploy 部署文章，可以用hexo d缩写

```

# 十四.events处理异步

```javascript
var Event = require("events").EventEmitter;
var ev = new Event(); //实例化events
router.get("/authority", (req, res) => {
  let username = req.param("username");
  var obj = {};
  obj.info = [];
  //事件1
  ev.on("error", function () {
    console.log("error");
  });
  ev.on("FindId", async function () {
    await User.findByName(username, function (err, docs) {
      if (err) {
        emitter.emit("error");
      }
      var arr = docs[0].resource;
      var length = arr.length;
      arr.forEach((id) => {
        ev.emit("findInfo", id, length);
      });
    });
  });
  //事件2
  ev.on("findInfo", function (id, length) {
    Resource.findAuthority(id, function (err, docs) {
      if (err) {
        emitter.emit("error");
      }
      obj.info.push(docs);
      ev.emit("getinfo", length);
    });
  });
  ev.on("getinfo", function (length) {
    try {
      if (obj.info.length == length) {
        return res.json(obj);
      } else {
        return;
      }
    } catch (e) {}
  });
  ev.emit("FindId");
});
```

