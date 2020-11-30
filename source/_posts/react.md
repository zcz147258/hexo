---
title: React
date:
updated:
type: "tags"
comments:
categories: React
description: React
keywords: React
top_img: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2431606259,2554064138&fm=26&gp=0.jpg
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2431606259,2554064138&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 一.react简介

```
起源于 facebook 的内部项目   ins
```

# 二.React和vue的对比

```
1.组件化方面
	模块化  代码角度   复用的代码，抽离为单个模块，便于开发和维护
	组件化  UI界面角度
	
	Vue  
		.vue创建组件  
				template 结构 
				script 行为  
                style  样式 
	React 
		有组件化的概念，一切都是以  js来表现得
2.开发团队
	facebook
	尤雨溪
	
3.移动app的开发体验
	Vue   Weex
	React  ReactNative
```

# 三.虚拟Dom

```
Dom的本质是什么，浏览器中的概念，用js对象来表示页面上的元素，并且提供了操作Dom的Api

什么是虚拟Dom  用js来模拟页面上的DOM和DOM嵌套

为什么要实现虚拟DOM 为了实现页面中 Dom的高效更新
```

## 3.1DOM树的概念

```
一个网页呈现的过程
1.浏览器请求服务器获取页面HTML代码
2.浏览器在内存中 解析DOM树，并且在浏览器内存中，渲染出一颗DOM树
3.浏览器把DOM树，呈现到页面上

```

## 3.2虚拟DOM

```
获取到内存中的新旧两颗DOM树，进行对比，得到需要按需更新的DOM元素
程序员可以模拟新旧两颗DOM树，

 用js来模拟新旧两颗DOM树
 模拟的两颗新旧DOM树，就是虚拟DOM
 
 目地：实现页面元素的高效更新
 
 本质：用js对象来模拟元素和嵌套关系
```

# 四.DIff算法

```
tree diff     新旧两颗DOM树，逐层对比的过程
component diff  每一层中 组件级别的对比 组件相同不需要更新，不同删除旧的，创建新的组件
element diff  如果两个组件类型相同，那么就需要元素级别的对比
```

# 五.在项目中使用react

```
cnpm i react ract-dom -S
安装react包
react   创建组件和虚拟Dom的
react-dom  专门进行操作dom的，最主要的场景就是 ReactDOM.render()
```

```react
import React from 'react'
import ReactDOM from 'react-dom'

//创建虚拟DOM
	//参数1   创建元素的类型，字符串，表示元素的名称
	//参数2   是一个对象或者null  表示整个DOm元素的属性
	//参数3   子节点(包括其他虚拟DOM或者文本子节点)
	//参数4    其他子节点
const myh1 = React.createElement('h1',null,'这是一个大大H1')

使用 reactdom 把虚拟dom渲染到页面上
//参数1   要渲染那个虚拟dom元素
//参数2   指定页面上的一个容器

React.render(myh1,document.getElementByid('app')); 
```

```
渲染页面shang的DOM结构，最好的方式  写HTML代码
```

# 六.JSX

```react
在js中不能写 HTML代码
解决问题可以写  
babel 来转化js中的标签

在js中，写入混合的HTML的代码，叫做JSX的语法

如何启用jsx语法
1.安装 babel插件 
	cnpm i babel-core babel-loader babel-plugin-transform-runtime  -D
	cnpm  i babel-preset-env  babel-preset-stage-0 -D
安装能够识别 jsx语法的包
	babel-preset-react
	cnpm i babel-preset-react
	
2.webpack-config-js 中
	rules;[
        { test: /\.js|jsx$/,user :'babel-loader',exclude:/node_modules/ }
	]
3.项目根目录创建一个 .babelrc
	json配置文件
	{
        “preset”: ["env","stage-0","react"],
        "plugins": ["transform-runtime"]
	}
```

## 6.1语法

```react
let a =10
ReactDOM.render(<div>{a}</div>),document.getElementById('app')

花括号可以写入 
		数字      10
		字符串    ‘dsada’
        布尔值     false
		属性绑定值   title='999'              title = {title}
		渲染jsx元素  h1 = <h1>红红火炬哦</h1>
		渲染jsx数组	[<h1>红红火炬哦</h1>,<h2>红红火炬哦</h2>,<h3>红红火炬哦</h3>]
		将普通字符数组转为jsx数组并且渲染到页面上
			
			方法1
				const arr = ['我是','校长','教师','老师','师傅'],
				const nameArr = [];
				arr.forEach(item = >{
                    const temp = <h1> { item } </h1>
                    nameArr.push(temp)
				})
				然后渲染到页面
			
			方法2
				内部for循环
				{arr.map(item = >{
                    retrun <h3 key={id}>{item}</h3> 
				})}
				
```

## 6.2KEY

如果  v-for  map 循环的时候，如果需要保存状态的时候，必须用key

## 6.3注意事项

```
注释
	{/*     */}
标签必须成对出现

元素class类名用 className代替
htmlfor 替换 label 的 for  属性

jsx创建的DOM中 所有的节点，必须有唯一的根元素进行包裹
```

# 七 展开运算符...

```react
const dog = {
    name: '大黄',
    age: 3,
    gender: '雄'
}
<h1 { ...dog }></h1>   就可以渲染


const dog2 = {
    class: sdada
    ...dog
}  就可以实现赋值
```

# 八.组件化

```react
1.父组件向子组件传值
2.使用{ ...obj } 属性扩散传递数据
3.是组件封装到单独的文件中‘
4.组件的名称首字母必须是大写

function Hello(){
    return <h1>的撒老大</h1>
}
render(<hello></hello>)

抽离成一个文件
	jsx  组件
然后导入React

webpack   
	resolve中配置   .jsx  就可以省略不写
	resolve   alias   @   =  ./src  配置路径
```

## 8.1第二种创建组件方式class

```react
class Animal(){
	//构造器 每一个类中都有  new的时候就会执行  构造器的代码
    constructor(name,age){
        this.name = name;
        this.age = age
    }
    //静态属性
    static info = 'aaa'
    //实例方法
    chi(){
        
    }
    //静态方法
    static sleep(){
        
    }
}
const al = new Animal('大黄',3)

	静态属性  通过构造函数 直接访问到的属性
Animal.gender = ’男‘	

//注意点
	内部只能写  构造器  实例方法  静态方法和静态属性
	class内部 还是function实现 语法糖
	
	
	子类继承父类  extends
	 在子类的构造期内  必须优先调用 super()
	 super就是父类的构造器  super(name,age)
	 
	 为子类挂载独有的方法
	 方法super()方法之后  this.idcard = card
```

```react
class 组件名 extends  React.Component(){
    render(){
        return <div>class创建的组件</div>
    }
}

组件传值

子组件直接   {this.props.name}  就可以访问传过来的属性  this标识当前组件实例对象

组件传值的属性的值 都是只读的 

对比  class  和 function(){}的区别
	
	class创建组件有自己的私有数据  和生命周期函数
	function创建的组件只有props，没有私有数据和生命周期函数
	
	constructor(){
        super();
        this.state = {
            msg:’大家好‘
        }  //相当于 vue的  data
	}
	
	访问属性 就是 this.state.msg  也可以修改  this.state.msg = "修改后"
	
	路径问题优化
			放绝对路径  @/components/item
```

## 8.2高阶函数和高阶组件

```
高阶函数
	1.接受函数类型的参数
	2.返回值式函数
	
	//定时器  Promise  数组遍历的方法   函数对象的bind
高阶组件
	1.本质是一个函数
	2.接受一个组件，返回一个组件
	
	//例如 Form.create()(Login)
```



# 九.样式

```react
jsx中 
	写行内样式
		数字类型不用 引号  字符串类型的值   需要用引号
		style = {{ color: 'red' }}
	className="title"
	
	引入样式表  在全局生效   默认没有独立作用域
	import   obj  from 'css'
	React中类似的 scoped
	css-loader?modules   表示为普通的css样式表  启动模块化
	css模块化  也支持 类选择器  和  ID选择器生效  不会对标签模块化
	使用   obj.title
	
	id = { obj.title2 }
	
	自定义模块化的类型
	css-loader?modules&localidentName=[path][name]-[local]-[hash:5]
	
	不想被模块化
	:local   会被模块化
	:global(.test){   不会被模块化
        color；red
	}
	
	使用 多个类名 
		{obj.title + 'test'}
		{[obj.title,'test'].join(' ')}
		
		
	在项目中 用 less 或者 scss  
	引入 bootstrap 的样式
	import  bootcss from 'bootstrap/dist/css/bootstrap.css'
	
	我们可以自己规定
		第三方的样式表都是css
		自己的样式表都是 scss 或者 less
```

# 十.绑定事件

```react
事件的首字母必须大写  onMouseover
<button onClick={function(){}}></button>  或者 this.myevent   不加括号

标准用法 
	<button onClick={ () => this.show(参数) }></button>
	
	show = (参数) =>{
        console.log(1)
	}
	
	修改state
	this.state.msg = '000'  可以改变state 但是页面上却没有改变
	重新赋值需要
		this.setState({
            msg: '123'
		})
	注意点
		1.setstate只会把 state状态更新，不会覆盖其他的state
		2.SetState方法是一个异步的，用回调函数来拿到最新的值
			this.SetStae({},function(){
                console.log('最新的值')
			})
绑定文本框
	单向数据流通 和上面类似
	双向绑定  修改文本框 自动同步值
	1.e.target.value
	<input onChange={(e) = > this.txtChange(e)} />   要么提供一个readonly    要么提供一个 onChange函数	
	txtChange = (e)=>{
        console.log(e.target.value)
        this.setState({
            msg: e.target.value
        })
	}
	2.this.refs.txt.value
```

# 十一.生命周期

``` react
生命周期流程
	1.第一次初始化渲染显示：ReactDOM.render()
			constructor()  创建初始化 state
			componentWillMount()   将要插入回调
			render()   用于插入虚拟DOM回调
			componentDidMount()  已经插入回调
	2.每次更新state  this.setState()
		componentWillUpdate()   将要更新回调
		render()   更新  重新渲染
		componentDidUpdate()   已经更新回调
	3.移除组件
		ReactDom.unmountcomponentAtNode(Dom)
        componentWillUnmount()  组件将要被移除  回调
```

# 十二.脚手架创建

```react
用 creat-react-app创建 app应用
创建项目并且启动
	1.npm install -g create-react-app
	2.create-react-app hello-react
	3.cd hello-react
	4.npm start
```

# 十三.使用axios

```react
index.js 引入

import axios from 'axios';

添加到原型上
React.Component.prototype.axios = axios;

组件中直接使用
this.axios.get('/api/login').then().catch()
```

# 十四.组件之间的通信

```react
1.props
2.使用消息订阅  发布 pubSubjs  机制   

父组件向子组件传值
父组件通过属性进行传递，子组件通过props获取
	//父组件
class CommentList extends Component{
    render(){
        return(
            <div>
               <Comment comment={information}/>
            </div>
        )
    }
}
//子组件
class Comment extends Component{
    render(){
        return(
            <div>
                <span>{this.props.comment}:</span>
            </div>
        )
    }
}
子组件向父组件传值
	//父组件
class CommentApp extends Component{
    constructor(){
        super();
        this.state = {comments:[]}
    }
    printContent(comment){
        this.setState({comment});
    }
    render(){
        return (
            <div>
                <CommentInput onSubmit={this.printContent.bind(this)} />
            </div>
        )
    }
}
//子组件
class CommentInput extends Component{
    constructor(){
        super();
        this.state = {
            usrName:'',
            content:''
        };
    }
    submit(){
        if(this.props.onSubmit){
            var {usrName,content} = this.state;
            this.props.onSubmit({usrName,content})
        }
        this.setState({content:''});
    }
    render(){
        return(
              <div>
               <div>
                   <span>用户名：</span>
                   <div className="usrName">
                       <input type="text" value={this.state.usrName} />
                  </div>
               </div>
                <div>
                    <span>评论内容：</span>
                    <div className="content">
                       <textarea value={this.state.content} />
                   </div>
                </div>
                <button onClick={this.submit.bind(this)}>submit</button>
            </div>
        )
    }
}
兄弟之间传值
	通过发布/订阅进行传递
	在子组件A中 commentDidMount函数中，发布事件，在子组件B中commentDidMount函数中对事件进行监听 
```

# 十五.React-Router

## 15.1路由简介

```react
4的  版本

	组件
		<BrowserRouter>
		<HashRouter>
		<Route>
		<Redirect>
		<Link>
		<NavLink>
		<Swtich>
	对象
		history
		match
        withRouter
```

## 15.2路由使用

```react
下载
	npm install --save react-router-dom
	
	路由组件  views
	非路由组件 components
	
	1.指定视图
        <BrowserRouter>
            <APP />
        </BrowserRouter>
	
        <HashRouter>
            <APP />
        </HashRouter>
    2.在要跳转的位置加
    	<NavLink to='/about'>About</NavLink>
    	<NavLink to='/about'>Home</NavLink>
    
    3.变化的路由组件显示的部分
    	可以切换的路由组件
    	<Swtich>
    		//引入组件
    		<Route path="/about" components={About}/>
    		<Route path="/home" components={Home}/>
    	</Swtich>
```

## 15.3路由嵌套

```react
在父路由中指定
	路由链接 <NavLink>
	路由  <Route>
	
	<Route to='/home/news'>
	<Route to='/home/messages'>
	点击父路由，子路由显示
	<Redirect to='/home/news'>
```

## 15.4向路由组件传递数据

```react
传值
	<a href={`/home/message/messagedetails/${m.id}`}>{m.title}</a>
	<Route  path="/home/message/messagedetails/:id" components={MessqgeDetails} />
接受
	const {id} = this.props.match.params  //获取

路由链接 和 非路由链接
	因为是 a标签  所以是  非路由链接
```

## 15.5完整的书写路由方式

第一种

```react
定义路由跳转的地方和组件信息
			<Sw>
              <Route path='/dashboard/guide' component={Guide}/>
              <Route path='/dashboard/partner' component={Partner}/>
              <Route path='/dashboard/product' component={Product}/>
              {/* 默认跳转 */}
              {/* <Redirect to="/dashboard/product"></Redirect> */}
          </Sw>
 使用 link跳转
 		<Link to="/dashboard/partner">合作伙伴</Link>
```

第二种

```react
  写事件
  switch (params) {
      case '开发向导':
        // this.props.history.push('/article')
        this.props.history.push('/dashboard/guide')
        console.log(this.props.history)
        break;
      case '产品中心':
        this.props.history.push('/dashboard/product')
        break;
      case '数据中心':
        // this.props.history.push('/article')
        break;
      case '合作伙伴':
        this.props.history.push('/dashboard/partner')
        break;
    }
    
    export default withRouter(index);
```

## 15.6路由传值的区别和使用

```react
Params
    <Route path='/path/:name' component={Path}/>
    <link to="/path/2">xxx</Link>
    this.props.history.push({pathname:"/path/" + name});
    读取参数用:this.props.match.params.name
	//缺点
	//优势 ： 刷新地址栏，参数依然存在
	//缺点:只能传字符串，并且，如果传的值太多的话，url会变得长而丑陋。
query
	<Route path='/query' component={Query}/>
	<Link to={{ path : ' /query' , query : { name : 'sunny' }}}>
	this.props.history.push({pathname:"/query",query: { name : 'sunny' }});
	读取参数用: this.props.location.query.name
    //优势：传参优雅，传递参数可传对象；
	//缺点：刷新地址栏，参数丢失
state
    <Route path='/sort ' component={Sort}/>
	<Link to={{ path : ' /sort ' , state : { name : 'sunny' }}}> 
	this.props.history.push({pathname:"/sort ",state : { name : 'sunny' }});
	读取参数用: this.props.location.query.state 
    //优缺点同query
search
    <Route path='/web/departManange ' component={DepartManange}/>
	<link to="web/departManange?tenantId=12121212">xxx</Link>
	this.props.history.push({pathname:"/web/departManange?tenantId" + row.tenantId});
	读取参数用: this.props.location.search
    //优缺点同params
```



# 十六.material-ui的使用

```react
// 安装material-ui
npm  install  @material-ui/core

// 安装material  icons
npm  install  @material-ui/icons

import Button from '@material-ui/core/Button';  // 导入Button组件
```

# 十七.打包

```react
{
  "name": "wap-v2",
  "version": "0.1.0",
  "private": true,
  "homepage": "./",         //加上此句即可
  "dependencies": {...}
}


无报错但空白页
HashRouter与BrowserRouter的异同
将BrowserRouter 改为 HashRouter
```

# 十八.坑

```react
书写方案1：this.setstate({},()=>{})
书写方案2：this.setstate(()=({}),()=>{})


create(){
   this.setState({
     controll: !this.state.controll
   },function(){
     console.log(this.state.controll)
   })
  }

引入图片
	src:require('../../../assets/images/工位占用状态传感器.jpg')}
```

# 十九.ui库

```react
yarn add antd

在要使用的地方引入
import { Button } from 'antd';

在app.css中引入
@import '~antd/dist/antd.css';
```

# 二十.redux

```react
redux是一个独立专门用于状态管理的js库
它可以用在react angular vue等项目中 但基本与react配合使用
作用 管理react 应用中多个组件共享的状态

下载redux的包
npm install --save redux

什么情况下使用 redux

某个组件的状态需要共享
某个状态在任何地方都可以拿到
一个组件需要改变全局状态
一个组件需要改变另外一个组件的状态
```

```react
不使用 redux
//  得到选择的数量
	const number = this.select.value * 1
// 得到原本的count状态,并且计算新的count
	const count = this.state.conut + number
// 更新状态
	this.setState({count:count})
```

## 20.1redux核心api

```react
createStore()   创建包含指定redux的store对象

    store对象
            redux库最核心的管理对象
            它内部维护着
                state
                reducer
            核心方法
                getState()
                dispatch(action)
                subscribe(listener)
            编码
                store.getState()
                store.dispatch({type:'INCREMENT}',number)
                store.subcribe(render)
applyMiddleware()
	应用于基于redux的中间件
	异步中间件等
combineReducers()
	作用  合并多个reducer函数
```

## 20.2redux的核心概念

```react
action	
		标识要执行行为的对象
		包含2个方面的属性
		type:标识属性，值为字符串，唯一，必要属性
		data也可以是其他:数据属性，值类型任意，可选属性

reducer
		根据老的state和action 产生新的state的纯函数
		返回一个新的状态

store
		将state,action和reducer联系在一起的对象 
```

## 20.3开始使用

```react
1.// 引入redux
import {createStore} from 'redux'

2.//生成一个store对象
//引入reducer
//内部会第一次调用reducer函数，得到初始state
import {counter} from './redux/reducers'
const store = createStore(counter)

3.//将action type 的常量字符串定义在
export const INCREMENT = 'INCREMENT'
export const DECREMENT = 'DECREMENT'

4.//书写reducer
// 包含多个reducer函数
//引入 action type
import {INCREMENT,DECREMENT} from './action-type'
export function counter(state = 0, action) {
  //形参默认值
  console.log("counter():", state, action);
  switch (action.type) {
    case INCREMENT:
      return state + action.data;
    case DECREMENT:
      return state - action.data;
    default:
      return state;
  }
}

5.将store传给  APP组件
  <APP store={store}></APP>
  再组件内部
  状态可以用 
  const count  = this.props.store.getState()  //获取旧的count
  
  //更新状态
  import {INCREMENT,DECREMENT} from '../../action-type'
  this.props.store.dispatch({
      type:INCREMENT,
      data: number
  })
 6.//订阅监听,store状态变化了 就进行重绘
    store.subscribe(
      function(){
        ReactDOM.render(
          <React.StrictMode>
            <App />
          </React.StrictMode>,
          document.getElementById('root')
        )
      }
    )
  7.抽离封装 action creator
  //增加
    export const incrementCreate = (number) =>{
        return ({
            type: INCREMENT,
            data: number
        })
    }
    //减少
    export const decreamentCreate = (number) =>{
        return ({
            type: INCREMENT,
            data: number
        })
    }
    8.抽离store对象
    import {createStore} from 'redux'
        //引入reducer
        import {counter} from './redux/reducers'

        //生成一个store对象
        const store = createStore(counter)
        export default store
```

# 二十一.Antd 加 react

```
dva  dmi   脚手架 自动安装 react + 
```

## 21.1开启装饰器

```react
当我们需要在多个不同的类之间共享或者扩展一些方法或行为的时候，代码会变得错综复杂，极其不优雅，这也就是装饰器被提出的一个很重要的原因。

@decorator
class Cat {}

class Dog {
    @decorator
    run() {}
}

我们在定义装饰器的时候，参数是有三个，target、name、descriptor 。
其实装饰器在作用于属性的时候，实际上是通过 Object.defineProperty 来进行扩展和封装的。


安装 
	react-app-rewired  customize-cra
	yarn add react-app-rewired  customize-cra
	
修改package.json
	"scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test",
    "eject": "react-app-rewired eject"
  },
  增加 config-overrides.js
  const {
  override,
  addDecoratorsLegacy
    } = require("customize-cra");
    module.exports = override(
      // enable legacy decorators babel plugin
      addDecoratorsLegacy()
    );
```

## 21.2安装antd

```react
yarn add antd
antd 里面的组件库都是less预编译语言开发的  默认有一整套完整的主题

例如  primary 关键字  颜色是 蓝色  danger是红色 
	那我们如何修改这种样式
	
修改装饰器和 全局主题   默认主题样式
安装  yarn add babel-plugin-import
+ module.exports = override(
+   fixBabelImports('import', {
+     libraryName: 'antd',
+     libraryDirectory: 'es',
+     style: 'css',
+   }),
+ );

安装  yarn add less less-loader

	去除默认的  严格模式
	
踩坑  对于eject报错的问题
	git add .
	git commit -m 'init'
	npm run eject


465行  sass-loader改为 less-loader

// style files regexes
const cssRegex = /\.css$/;
const cssModuleRegex = /\.module\.css$/;
const sassRegex = /\.(scss|less)$/;
const sassModuleRegex = /\.module\.(scss|less)$/;

遇到问题无法yarn start
之后  yarn add react-scripts   

重新操作
```

## 21.3安装react生态

```react
yarn add react-router-dom
yarn add axios redux react-redux redux
```

## 21.4默认英文转化

```react
import zhCN from 'antd/es/locale/zh_CN';
import { ConfigProvider } from 'antd';
ReactDOM.render(
  <ConfigProvider locale={zhCN}>
  <App />
</ConfigProvider>,
```

## 21.5路由规划和懒加载

```react
公共路由
私有路由


权限控制 RBAC  基于角色权限管理
图标美化
	npm install --save @ant-design/icons
	
	
	懒加载
		yarn add react-loadable
		
		
import Loadable from 'react-loadable';
import Loading from '../components/loading';
 
const Article = Loadable({
  loader: () => import('../views/Article/index'),
  loading: Loading,
});

	 render() {
        return (
            <div>Loading...</div>
        );
    }
```

## 21.6axios

```react
axios.defaults.timeout = 50000 //设置接口响应时间
axios.defaults.baseURL = 'http://rap2.taobao.org:38080/app/mock/256761/api/v1' // 这是调用数据接口,公共接口url+调用接口名
axios.defaults.withCredentials= true;

//拦截器
axios.interceptors.request.use(
    //config包含每次请求的信息
    config => {
        //拿请求路径
        //console.log('请求路径', config.url)
        //去缓存中拿token
        // let token = store.state.token;  //从缓存中取token
        //有token
        // if (token) {
        //     // config.headers.Authorization = token;    //将token放到请求头发送给服务器
        // } else {
        //     //localStorage.clear();  //清空缓存
        //     //排除login请求接口
        //     if (router.currentRoute.name && router.currentRoute.name.toLowerCase() == "login") {

        //     } else {
        //         //否则 全部返回null
        //     }
        // }
        return config
    },
    err => {
        return Promise.reject(err)
    }
)
// http response 拦截器
axios.interceptors.response.use(
    response => {
        return response; //请求成功的时候返回的data
    },
    error => {
        try {
            // if (error.response) {
            //     switch (error.response.status) {
            //         case 401: //token过期，清除token并跳转到登录页面
            //             //localStorage.clear();
            //             var baurl = window.location.href;
            //             console.log(baurl)
            //             router.replace({
            //                 path: 'login',
            //                 query: { backUrl: baurl }
            //             });
            //             return;
            //     }
            // }
            return Promise.reject(error.response.data)
        }
        catch (e) {
        }
    }
)

/ 封装axios的get请求
export function getData(url, params) {
    return new Promise((resolve, reject) => {
      axios.get(url, {params:params}).then(response => {
          resolve(response.data);
        })
        .catch(error => {
          reject(error);
        });
    });
  }
  // 封装axios的post请求
  export function postData(url, params) {
    return new Promise((resolve, reject) => {
      axios.post(url, QS.stringify(params)).then(response => {
          console.log(response)
          resolve(response.data);
        })
        .catch(error => {
          reject(error);
        });
    });
  }
  export function Postdownload(url, params,responsetype) {
    return new Promise((resolve, reject) => {
      //{responseType:'blob'}
      axios.post(url, QS.stringify(params)).then(response => {
          resolve(response);
        })
        .catch(error => {
          reject(error);
        });
    });
  }
export default axios


//在  api.js中使用
import {getData,postData,Postdownload} from '../utils/http'
export function GetArticle(data={}){
    return getData('/article',data)
}




2.构造函数axios
const isDev  = process.env.NODE_ENV === 'development'
	const service = axios.create({
        baseURl: isDev? '测试地址':'线上地址'
	})
	
	const getTopics = ()=>{
        return service.get(‘/article’)
	}
```

## 21.7.对象返回标签内容

```react
 return {
            title: mapTableTitle[item],
            dataIndex: item,
            key: item,
            render:(text,record,index)=>{
               return (
                <Tooltip title={record.amount >=100? '阅读数超过1000':'阅读数低于1000'}>
                <Tag color={record.amount >=100? 'red':'green'}>{record.amount}</Tag>
                </Tooltip>
               )
            }
          }
```

## 21.8.标题随着内容变化

```react
在 APP.js里面的构造函数
this.props.history.listen((location)=>{
        var pathname = location.pathname;
        var one = privateRoutes.find(item =>{
          return item.pathname == pathname;
        })
        document.title = one && one.title;
    })
```

# 二十二.Redux

## 22.1Redux的工作流程

```react
首先 是 React组件向 action发送请求
然后 到 store
然后到  reducer
然后返回 store
然后返回给组件
```

## 22.2redux dev

```react
//增加调试
 window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
```

## 22.3流程

```react
1.创建仓库

	import { createStore } from 'redux'
	//引入reducer
    import reducer from './reducer'
    //创建了一个仓库
    //然后注入reducer
	const store = createStore(
    reducer,
    window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
    )
	export default store

2.组件构造函数里面引入state

	this.state = store.getState();

3.actiontypes
	
    export const CHANGE_INPUT = 'changeInput'
    export const ADD_ITEM = 'additem'
    export const DEL = 'delitem'

4.actioncreators
	
	import { CHANGE_INPUT,ADD_ITEM,DEL} from './actiontypes'
    export const changeInputAction = (value) => ({
        type: CHANGE_INPUT,
        value
    })
    export const addAction = () => ({
        type: ADD_ITEM
    })
    export const delAction = (index) => ({
        type: DEL,
        index
    })
5.订阅实时更新

    constructor(props) {
        super(props);
        this.state = store.getState();
        //该白this指向
        // this.changeInputValue = this.changeInputValue.bind(this)
        //store 订阅
        store.subscribe(this.storeChange);
      }
      //订阅
      storeChange = () => {
        this.setState(store.getState);
      };
6. 主函数改变操作

    //改变store的值
      changeInputValue = (e) => {
        const action = changeInputAction(e.target.value)
        store.dispatch(action);
      };
      //增加
      ClickBtn = () => {
        const action = addAction()
        store.dispatch(action);
      };
      //删除
      DelItem = (index) => {
        const action = delAction(index)
        store.dispatch(action);
      };
```

## 22.4注意事项

```react
1.store必须是唯一的

2.reducer不能直接改变store里面的state  只能接收

3.Reducer只能是纯函数
```

## 22.5组件UI和逻辑部分的拆分

```react
定义TodolistUI

	 <ToDoListUI 
      inputValue = {this.state.inputValue}
      changeInputValue={this.changeInputValue}
      ClickBtn = {this.ClickBtn}
      list = {this.state.list}
      DelItem = {this.DelItem}
      />在··
      
      UI组件接受使用props
      onChange={(e) => this.props.changeInputValue(e)}
	
```

## 22.6无状态组件

```
没有class constructor
函数的返回值为  UI组件

无状态组件就是一个标准的函数
```

## 22.7axios和redux的结合

```react
export const GetList = 'getlist'
export const getListAction = (data) => ({
    type: GetList,
    data
})

if(action.type === GetList){
        let newState = JSON.parse(JSON.stringify(state))
        newState.list = action.data.result
        console.log(action.data.result)
        return newState
    }
    
 componentDidMount(){
    GetList().then((res)=>{
        const data = res
        const action = getListAction(data)
        store.dispatch(action)
    })
  }
```

## 22.8中间件Redux-thunk

```react
安装redux-thunk
npm install --save redux-thunk

配置以及兼容行
	import { createStore,applyMiddleware,compose } from 'redux'
    //引入reducer
    import reducer from './reducer'
    //配置中间件
    import thunk from 'redux-thunk'
    //创建了一个仓库
    //然后注入reducer
    //解决兼容问题
    const composeEnhances = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__?
        window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}):compose
    const enhancer = composeEnhances(applyMiddleware(thunk))
    const store = createStore(
        reducer,
        enhancer
        // applyMiddleware(thunk),
        // window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
        )
    export default store
    
    
    //使用  作用是延长生命周期 放到全局 而不是局部变量里面
    export const ToDoListAction = () =>{
        return (dispatch) => {
            GetToDoList().then((res)=>{
                const data = res
                const action = getListAction(res)
                dispatch(action)
            })
        }
    }
    
    componentDidMount(){
        const action = ToDoListAction()
        store.dispatch(action)
      }
```

## 22.9中间件Redux-saga

```javascript
安装
	yarn add saga
 import createSagaMiddleware from 'redux-saga'
const sagaMiddleWare = createSagaMiddleware();
```

## 22.10React-Redux

```react
Provider 提供器 和  connect  连接器

 <Provider store={store}>
                  <App {...rootprops} />
   </Provider>
   
   
   //映射关系
 const stateprops = (state) =>{
     return {
         inputValue:state.inputValue
     }
 }
 	//派发
const mapDispatchToProps = (dispatch) => {
    return {
        changeInputValue: (e) => {
            let action = {
                type:'change_input',
                value:e.target.value
            }
            dispatch(action)
        }
    }
}
export default connect(stateprops,mapDispatchToProps)(Setting)
```

# 二十三.React_hooks

```react
原本写法
	this.setState({
            count:this.state.count+1
        })
        
        
        
hooks实现
 import React, { useState } from "react";
 function Example() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <div>You Click {count} times</div>
      <button onClick={()=>{setCount(count+1)}}>增加</button>
    </div>
  );
}
```

## 23.1UseState

```react
const [count, setCount] = useState(0);
useState方法内部接受的是 初始值
//不用解构赋值
	let _userState = useState(0)
	let count = _userState[0]
	let setState = _userState[1]
	
**userState不能存在于条件判断语句中
```

## 23.2UseEffect

```react
和主流逻辑关系不大，起到监听数据修改Dom的时候
	//异步的不会影响异步更新
 const [count, setCount] = useState(0);
  useEffect(()=>{
    console.log(`你点击了${count}次`)
  })
  return (
    <div>
      <div>You Click {count} times</div>
      <button onClick={()=>{setCount(count+1)}}>增加</button>
    </div>
  );
  
  //相当于生命周期函数componentDidMount 和 componentDidUpdate
  
   
  useEffect实现生命周期ComponentWillUnmount  解绑 应用于退出 解绑定时器
  	useEffect(()=>{
        console.log(`你点击了${count}次`)
        return ()=>{
          console.log('你走了Example')
        }
      },[count])
```

## 23.3useContext

```react
import React, { useState, createContext, useContext } from "react";
//创建一个共享的组件
const CountContext = createContext();


//父组件内部
<CountContext.Provider value={count}>
		//字组件
        <Counter></Counter>
  </CountContext.Provider>
  
 //子组件
 //字组件
function  Counter(){
    let count = useContext(CountContext)
    return(
        <h2>{count}</h2>
    )
}
```

## 23.4userReducer

```react
//基本语法
 原生reducer
 	//原生reducer
    // function countReducer(state,action){
    //     switch(action.type){
    //         case 'add':
    //             return state + 1
    //         case 'sub':
    //             return state - 1
    //         default:
    //             return state
    //     }
    // }
   如何使用
   import React, { useReducer } from "react";
    function ReducerDemo() {
      const [count, dispatch] = useReducer((state, action) => {
        switch (action) {
          case "add":
            return state + 1;
          case "sub":
            return state - 1;
          default:
            return state;
        }
      }, 0);
      return (
        <div>
          <div>You Click {count} times</div>
          <button onClick={()=>{dispatch('add')}}>增加</button>
          <button onClick={()=>{dispatch('sub')}}>减少</button>
        </div>
      );
    }
    export default ReducerDemo
    
    
    UseReducer 和 UserContext 实现redux的效果
    color.js
    	import React, { createContext,useReducer } from 'react'
        export const ColorContent = createContext({})
        //reducer
        export const reducer = (state, action) => {
            switch (action.type) {
                case 'updatecolor':
                    return action.color
                default:
                    return state
            }
        }
        export const Color = props =>{
            const [color,dispatch] = useReducer(reducer,'blue')
            return (
                <ColorContent.Provider value={{color,dispatch}}>
                    {props.children}
                </ColorContent.Provider>
            )
        }
        
      Button.js
      	function Buttons(){
            const {dispatch} = useContext(ColorContent)
            return(
                <div>
                    <button onClick={()=>{dispatch({type:'updatecolor',color:"red"})}}>红色</button>
                    <button onClick={()=>{dispatch({type:'updatecolor',color:"yellow"})}}>黄色</button>
                </div>
            )
        }
        
       ShowArea.js
        const {color} = useContext(ColorContent)
        return(
            <div style={{ color: color}}>字体颜色为blue</div>
        )
        
        Example6.js
         return(
            <div>
                <Color>
                    <ShowArea></ShowArea>
                    <Buttons></Buttons>
                </Color>
            </div>
        )
```

# 二十四.项目实战

```javascript
打包发布的时候  下载  
运行打包后生成的项目build
npm install -g serve
serve build
//下载antd
	yarn add antd
//mian.js引入
	import 'antd/dist/antd.css';
//按需打包
	参照官方文档
//自定义主题配置
```

```javascript
less修改
安装  yarn add less less-loader
踩坑  对于eject报错的问题
	git add .
	git commit -m 'init'
	npm run eject

465行  sass-loader改为 less-loader

// style files regexes
const cssRegex = /\.css$/;
const cssModuleRegex = /\.module\.css$/;
const sassRegex = /\.(scss|less)$/;
const sassModuleRegex = /\.module\.(scss|less)$/;

遇到问题无法yarn start
之后  yarn add react-scripts   

重新操作
```

```react
//登陆表单验证 
//声明式验证
	form item里面
    rules:[
        {required: true,message:''},
        {min: 4,message:'最小值不'},
        {max: 12,message:''},
        {pattern: /^[a-zA-Z0-9_]+$/,message:''},
    ]
//自定义验证
	form item里面
    rules:[
        {validator: this.valitdatePWD}
    ]
    valitdatePWD = (rule,value,callback)=>{
        callback()//验证通过
        callback('验证失败')
    }
```

## 24.1加密

```javascript
yarn add crypto-js 或 npm install crypto-js
//MD5
import MD5 from 'crypto-js/md5'
let obj = {};
obj.username = MD5(this.state.userinfo.username).toString()
obj.password = MD5(this.state.userinfo.password).toString()
//Hmac-MD5
CryptoJS.HmacMD5(secret,pwd)
//AES
const key = CryptoJS.enc.Utf8.parse('1234567812345678') // 十六位十六进制数作为密钥
const iv = CryptoJS.enc.Utf8.parse("1234567812345678");//十六位十六进制数作为密钥偏移量
// 解密方法
function Decrypt(word) {
    let decrypt = CryptoJS.AES.decrypt(word, key, {
        mode: CryptoJS.mode.ECB,
        padding: CryptoJS.pad.Pkcs7
    })
    let decryptedStr = decrypt.toString(CryptoJS.enc.Utf8)
    return decryptedStr.toString()
}
 
// 加密方法
function Encrypt(word) {
    let encrypted = CryptoJS.AES.encrypt(word, key, { 
        mode: CryptoJS.mode.ECB, 
        padding: CryptoJS.pad.Pkcs7 
    });
    return encrypted.toString()
}


//使用 jsencrypt 进行RSA加密
import JSEncrypt from 'jsencrypt';
const Encrypt = new JSEncrypt();
let publicKey = '';
publicKey += '-----BEGIN PUBLIC KEY-----';
publicKey += 'FJDLSKAJKLJ3L2J49FIDSAJFLKSDJAK32FKJDSAFJKDKFKDFJKDSLAFLSAFDKSAFKDASLFD';
publicKey += 'FJDLSKAJKLJ3L2J49FIDSAJFLKSDJAK32FKJDSAFJKDKFKDFJKDSLAFLSAFDKSAFKDASLFD';
publicKey += 'FJDLSKAJKLJ3L2J49FIDSAJFLKSDJAK32FKJDSAFJKDKFKDFJKDSLAFLSAFDKSAFKDASLFD';
publicKey += 'FJDLSKAJKLJ3L2J49FIDSAJF';
publicKey += '-----END PUBLIC KEY-----';
export default {
  /**
   * 加密一个参数
   * @param {*} value 需要加密的值
   */
  encrypt(value) {
    Encrypt.setPublicKey(publicKey);
    return Encrypt.encrypt(value);
  },
};

//解密
	npm install node-rsa --save
    const fs = require('fs');
const path = require('path');
const RSA = require('node-rsa');
// RSA解密
const keyPath = path.resolve(__dirname, './pem/rsa_private_key.pem');
const privatePem = fs.readFileSync(keyPath).toString();
const privateKey = new RSA(privatePem);
// 转成pkcs1格式
privateKey.setOptions({ encryptionScheme: 'pkcs1' });
module.exports = {
  /**
   * 解密
   * @param {*} value 需要解密的值
   */
  decrypt(value) {
    let data = value;
    // 使用try...catch...捕获解密失败错误（如公钥错误），返回controller处理
    try {
      data = privateKey.decrypt(value, 'utf8');
      return data;
    } catch (err) {
      return false;
    }
  },
};
//后台node目录结构
   -- pem
   		-- rsa_private_key.pem
   		-- rsa_public_key.pem
   -- rsa.js
```

## 24.2react实现权限控制

```javascript
//1.路由
//定义映射名称和组件
const mapper = {
  "/admin/note":note,
  "/admin/info":info,
  "/admin/selfinfo":selfinfo,
  "/admin/back":back,
  "/admin/front":front,
  "/admin/pic":pic,
  "/admin/auth":Auth,
  "/admin/article":article,
  "/admin/tag":tag,
}
//公有路由
const commonRoutes = [
    {
      pathname: "/login",
      component: Login,
    },
    {
      pathname: "/404",
      component: NotFound,
    }
];
//私有路由
const privateRoutes = [];
var routers = null;

function InitPrivate(){
  State.AuthorityList.info.forEach(element => {
      if(!element.isTop){
        let obj = {}
        obj.pathname = element.pathname;
        obj.component = mapper[element.pathname]
        privateRoutes.push(obj)
      }else{
        element.children.forEach(item =>{
          let obj = {}
          obj.pathname = item.pathname;
          obj.component = mapper[item.pathname]
          privateRoutes.push(obj)
        })
      }
  });
}
//2.redux控制
	//index.js
	constructor(props) {
        super(props);
        this.state = store.getState();
        store.subscribe(this.storeChange);
      }
      storeChange = () => {
        this.setState(store.getState,function(){
          console.log(this.state)
        });
      };
	//action
	export const  ToGetAuthority = (value) => {
    return dispatch => {
    Authority({ username:crypt.Decrypt(localStorage.getItem('username')) }).then((res) => {
      const action = GetAuthority(res);
      dispatch(action);
    });
      };
    };
    export const GetAuthority = (value) => ({
        type: GET_AUTHORITY,
        value
    })
    //reducer
    case LOGIN_SUCCESS:
{
    localStorage.setItem("username",action.value.username);
    localStorage.setItem("password",action.value.password);
    return;
}
case GET_AUTHORITY:
{
    let newState = JSON.parse(JSON.stringify(state))
    newState.AuthorityList = action.value
    localStorage.setItem("AuthorityList",JSON.stringify(action.value));
    return newState;
}
	//渲染
	
```

## 25.3vscode注解插件

```
KoroFileHeader  
//配置
https://www.cnblogs.com/suRimn/p/10450372.html
（1）文件头部注释
快捷键：crtl+alt+i（window）,ctrl+cmd+t (mac)
（2）函数注释
快捷键：ctrl+alt+t (window), ctrl+alt+t(mac)
```

## 25.4路由权限

```react
最重要的点是Route组建里面用render属性替换component来渲染页面
<Route
  path={item.pathname} key={index}
   render = {
    () =>{
   return (this.state.token ? (item.auth ? (<item.Component />) : (<Redirect to={{pathname:'/toAuth'}}/>))
  :(<Redirect to={{pathname:'/login',query :{ operate : 'tologin' }}}/>)
           )
    }
    }
    ></Route>
        //路由权限
        <Route
            path={item.pathname}
            key={index}
            render = {
                () =>{
                    var Temp = item.component
                    return !item.auth ? (<Temp/>) : (<Redirect to="/toAuth"/>)
                }
            }
            // component={item.component}
            ></Route>
```



## 25.5 token验证

```js
安装 ActivePerl https://www.activestate.com/activeperl/downloads
安装 OpenSSl http://slproweb.com/products/Win32OpenSSL.html
在 ras 文件 终端夹下输入 openssl
生成私钥
//token.js
const jwt = require('jsonwebtoken')
// 创建 token 类
class Jwt {
    constructor(data) {
        this.data = data
    }
    //生成token
    generateToken() {
        let data = this.data
        let created = Math.floor(Date.now() / 1000)
        let cert = fs.readFileSync(path.join(__dirname, './pem/private_key.pem')) // 私钥
        let token = jwt.sign({
            data,
            exp: created + 60 * 30,
        }, cert, {algorithm: 'RS256'})
        return token
    }
    // 校验token
    verifyToken() {
        let token = this.data
        let cert = fs.readFileSync(path.join(__dirname, './pem/public_key.pem')) // 公钥
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

//login.js
 //生成token
let jwt = new Jwt(username)
let token = jwt.generateToken()
obj.success = "success";
obj.token = token
//app.js
//token验证中间件
app.use((req, res, next) => {
  if (req.url !== '/' && req.url !== '/login' ){
    console.log(req)
    let jwt = new Jwt(token)
    let result = jwt.verifyToken()
    console.log(result)
    if (result === 'err') {
        res.status(401).send({msg: '请求未授权，请重新登录'})
    } else {
        next()
    }
  }
})

//前端redux
```

## 25.6React中使用可视化

```react
bizcharts  
cnpm i bizcharts --save

// {
          $project: {
              //只有被设置进去的字段才会显示出来，其他列就不会被显示。
            day : {$substr: [{"$add":["$create_time", 28800000]}, 0, 7] },
            view: 1,
            commets:1,
            uid:1
          },
        },
        {
            $match:{
                uid:uid
            }
        },
        {
            $group:{
                _id:"$day",
                totalViews:{$sum: "$view"}, //统计price
                totalComments:{$sum: "$commets"}, //统计price
            }
        },
            //统计总的评论数量和浏览数量
```

## 25.7打包部署

```js
体积优化  //webpack.config.js
 // devtool: isEnvProduction
    //   ? shouldUseSourceMap
    //     ? 'source-map'
    //     : false
    //   : isEnvDevelopment && 'cheap-module-source-map',
    devtool:false,
        
yarn global add serve
cnpm install -g serve
serve -s build  
http://localhost:5000/#/login
        
HashRouter与BrowserRouter的异同
项目中控制路由跳转使用的是BrowserRouter。
在开发过程中使用是没有问题的，但是将页面上传至服务器之后，问题就来了：用户访问的资源不存在，页面是空白的，就像上面。
原因：
在browserHistory 模式下，URL 是指向真实 URL 的资源路径，当通过真实 URL 访问网站的时候，由于路径是指向服务器的真实路径，但该路径下并没有相关资源，所以用户访问的资源不存在。
解决
将BrowserRouter 改为 HashRouter
```

# 26.React+TS构建

## 26.1初始化项目

```shell
npx create-react-app antd-demo-ts --typescript
yarn create react-app antd-demo-ts --template typescript

安装TS插件
TypeScript Importer
```

## 26.2简单数据传递

```typescript
interface IProps{//接口必须I开头
    title:string,
    age:number,
    work?:string//可选项
}

export default class Hello extends React.Component<IProps,any>{
    public constructor(props:any){
        super(props)
    }
    public render(){
        return(
        <div>
            {this.props.title}
            {this.props.age}
        </div>
        )
    }
}
```

## 26.3简单状态管理

```react
public changeCount(){
        this.setState({
            count:2000
        })
    }
    
public readonly state: Readonly<IState> = {//只读
    count:100
}

export default class Hello extends React.Component<IProps,IState>{//第一个泛型为props 第二个泛型为state
```

## 26.4父子事件

```react
class App extends React.Component{

  public myClick(data:string){
    console.log(data)
  }

  public render(){
    return(
      <div className="App">
      <Hello title="打撒打撒阿德飒飒" age={18} onMyClick={(data:any)=>{ 		    this.myClick(data) }} ></Hello>
    </div>
    )
  }
}

//子事件
interface IProps{//接口必须I开头
    title:string,
    age:number,
    work?:string//可选项
    onMyClick:any
  }

  //通过接口申明state
interface IState{
    count:number
}

export default class Hello extends React.Component<IProps,IState>{//第一个泛型为props 第二个泛型为state
    public constructor(props:IProps){
        super(props);
        
        this.changeCount = this.changeCount.bind(this);//改变this指向
    }

    public readonly state: Readonly<IState> = {//只读
            count:100
    }
    //修改事件
    public changeCount(){
        this.setState({
            count:2000
        })
    }
    public sendParentMessage(){
        this.props.onMyClick("child message")
    }
    public render(){
        return(
        <div>
            {this.props.title}<br/>
            {this.props.age}<br/>
            {this.state.count}<br/>
            <button onClick={()=>this.changeCount()}>按钮</button>
            <button onClick={()=>this.sendParentMessage()}>向父级发送</button>
        </div>
        )
    }
}
```

# 27.项目源码阅读

## 1.Hooks + TS

```react
React.FC<>的在typescript使用的一个泛型，FC就是FunctionComponent的缩写，是函数组件，在这个泛型里面可以使用useState，个人觉得useState挺好用的
```

# 28.Umi+Dva

## 28.1dva介绍

```
Dva是将redux redux-sage react-router fetch 进行一个整合
dva 首先是一个基于 redux 和 redux-saga 的数据流方案，然后为了简化开发体验，dva 还额外内置了 react-router 和 fetch，所以也可以理解为一个轻量级的应用框架。
```

## 28.2Umi介绍

```
Umi，中文可发音为乌米，是可扩展的企业级前端应用框架。Umi 以路由为基础的，同时支持配置式路由和约定式路由，保证路由的功能完备，并以此进行功能扩展。然后配以生命周期完善的插件体系，覆盖从源码到构建产物的每个生命周期，支持各种功能扩展和业务需求


yarn create @umijs/umi-app  创建dva
yarn 运行
```

## 28.3Umi路由

```js
配置路由

在配置文件中通过 routes 进行配置，格式为路由信息的数组。


export default {
  routes: [
    { exact: true, path: '/', component: 'index' },
    { exact: true, path: '/user', component: 'user' },
  ],
}

如果没有 routes 配置，Umi 会进入约定式路由模式，然后分析 src/pages 目录拿到路由配置。
[
  { exact: true, path: '/', component: '@/pages/index' },
  { exact: true, path: '/users', component: '@/pages/users' },
]
```

## 28.4Model

//手写model

```js
/*
 * @Descripttion: 
 * @Author: mikasa
 * @Date: 2020-11-29 11:29:43
 */
import {Reducer,Effect,Subscription} from 'umi'
import { getRemoteList } from './service'
interface UserModelType{//约束
    namespace:'users',
    state:{},
    reducers:{
        getList:Reducer
    },
    effects:{
        getRemote:Effect
    },
    subscriptions:{
		setup:Subscription
    }
}
const UserModel:UserModelType = {
    namespace:'users',//命名空间
    state:{},//初始值
    reducers:{//同步
        getList(state,{payload}){
            return payload
        }
    },
    effects:{//异步
        *getRemote({payload},{put,call}){
            const data = yield call(getRemoteList)
            yield put({
                type:'getList',
                payload:data
            })
        }
    },
    subscriptions:{//订阅
    	setup({dispatch,history},done){
            history.listen((location,action)=>{
                if(location.pathname === '/users'){
                    dispatch({
                        type:'getRemote'
                    })         
                }
            })
        }
	}
}
export default UserModel
```

service.ts

```js
import { request } from 'umi'
export const getRemoteList = async params =>{
    return request('http://public-api-v1.aspirantzhang.com/users',{
        method:'get',
        params:{page:1}
    }).then(res=>{
        return res;
    }).catch(err=>{
    })
}
```

index.tsc

```js
function index({users}) {
    return (
        <div className='list-table'>
            <Table columns={columns} dataSource={users.data}/>
        </div>
    )
}
const mapStateToProps = ({users}) =>{
    return{
        users
    }
}
export default connect(mapStateToProps)(index)
```

