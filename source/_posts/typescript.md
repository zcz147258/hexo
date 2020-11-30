---
title: TypeScript
date:
updated:
type: "tags"
comments:
categories: JavaScript
description: TypeScript
keywords: TypeScript
top_img: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1550560693,1596858350&fm=26&gp=0.jpg
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1550560693,1596858350&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.安装

```typescript
cnpm install -g typescript

tsc -v  检查版本

//或者
安装 
npm install -g yarn
yarn global add typescript
```

# 2.编译

```typescript
tsc  加文件名称

自动编译
在vscode中
tsc --init   生成配置文件
 "outDir": "./js",     修改这个文件放置到
 选择终端  typescript 监视json
  Ctrl+shift+B
```

# 3.typescript数据类型

```typescript
boolean  布尔类型  true false
		var flag:boolean = true
number 数字类型
		var a:number = 123
string  字符串类型
		var str:string = "this is ts"

array  	数组类型
		第一种
			let num:number[] = [1,2,3,4,5,6]
		第二种
			let arr:Array<number> = [1,2,3,4,5]
tuple	元组类型   属于数组的一种
		let arr:[string,number,boolean] = ["ts",123,true]
enum	枚举类型
		1.情况1
		enum Flag { success=1,error=-1 }
		var f:Flag = Flag.success
		console.log(f)  1
		2.情况2
		enum Color { red,blue,orange }
		var f:Color = Color.red
		console.log(f)  默认输出索引值  0
		3.情况3
		enum Color { red,blue=5,orange }
		var f:Color = Color.blue
		console.log(f)  输出5   
		var f:Color = Color.orange
		console.log(f)  输出6  自动加1
any
		var num:number = 123  任意类型和es5有点相似
		用多来改变元素的状态  而且不报错
null	
		var num:null   console.log(num)   null
undefined   
		var num:undefined   console.log(num)   underfined
		var num:number | null |underfined   
viod  	没有任何类型 一般用于定义方法没有返回值
		function run():void{
            console.log('run')
		}
		run()
never   其他类型  从不会出现的值  never申明的变量只能被never类型赋值 包括(null和undefined)
		var a:undefined ;
		a =undefined  //不会报错
		
		var a:never;
		a=(()=>{
            throw new Error('错误')
		})()   //这就是其他类型
```

# 4.函数

```typescript
函数的定义 
	// 函数声明
	function run():string{
        return 'name'
	}
	//匿名函数
	var fun2 = function():number{
        return 123
	}
传参数
	function getinfo(name:string,age:number):string{
        return `${name}---${number}`
	}
	
可选参数
	//参数前面加一个?  就是可选参数
	//注意可选参数必须配置到后面	
	function getinfo(name:string,age?:number):string{
        return `${name}---${number}`
	}
默认参数
	function getinfo(name:string,age?:number=30):string{
        return `${name}---${number}`
	}
剩余参数
	function sum(...result:number[]):number{
        return 综合
	}
	sum(1,2,3,4)
函数重载
	function getInfo(name:string):string;
	function getInfo(name:number):number;	
	function getInfo(name:any):any{
        
	}
	function getInfo(name:string,age:number):string;	
```

# 5.类

```typescript
类里面的修饰符
	public   :公有  类里面 子类 类外面都可以访问
	protected	：保护  在类里面还有子类里面可以访问
	private	 :只能在子类里面访问
	
静态方法static修饰    静态方法没办法调用类里面的属性


抽象
	抽象方法只能放在抽象类里面
	抽象类的子类必须实现抽象类里面的抽象方法
	多态
	
	abstract class Animal{
        public name:string;
        constructor(name:string){
            this.name = name;
        }
        abstract eat():any;
        
	}
```

# 6.接口

```typescript
属性接口
	对象约束
        interface FullName{
            firstName：string;
            secondName: string;
        }
        function printName(name:FullName){
            //必须传入对象并且 包含 firstName  secondName
        }
        严格按照接口
	
	
	接口可选属性
		interface FullName{
            firstName？：string;
            secondName: string;
        }
函数类型接口
	模拟加密的函数类型接口
	interface encrypt(){
        (key:string,value:string):string;
	}
	var md5:encrypt = function(key:string,value:string):string{
        return key + value
	}
可索引接口
	数组的约束
		interface UserArr{
            [index:number]:string
		}
		var arr:UserArr = ['aaa','bbb']
	对象的约束
		interface UserObj{
            [index:string]:string
		}
		var arr:UserObj = {name:'20'}
类类型接口
	interface Animal{
        name:string;
        eat(str:string):void;
	}
	class Dog implements Animal{
        name:string;
        constructor(name:string){
            this.name = name
        }
        eat(){
            console.log('sdsdadadsa')
        }
	}
```

# 7.泛型

```typescript
解决类接口方法的复用性
T表示泛型  
function getData<T>(value:T):T{
    return value;
}
getData<number>(1);
getData<string>('2')

泛型接口
	//第一种定义
    interface ConfigFn(){
        <T>(value:T):T;
    }
    var getData:CongifFn = function<T>(value:T):T{
        return value;
    }

	//第二种定义
     interface ConfigFn()<T>{
            (value:T):T;
     }
    function<T>(value:T):T{
        return value;
    }	
```

# 8.模块

```typescript
export default 和 export{}的区别  
前者 只能暴漏一次   后者可以暴露多个变量
前者引入  直接引入     后者需要  {}  引入
```

# 9.命名空间

```typescript
namespace A{
    class....
}
避免命名冲突   

命名空间外部使用命名空间内部的方法  ，必须暴露出去才可以

如果命名空间暴露的方法都是一样的  需要用命名空间.方法使用

暴露命名空间 然后作为模块
```

# 10.装饰器

```typescript
装饰器是一种特殊类型的声明，它能够被附加到类申明，方法，属性或者参数上面，可以修改类的行为

类装饰器
	//无参
	定义一个装饰器
    //普通装饰器
    function logClass(params:any){
        params   就是当前类
        console.log(params)
        params.prototype.apiUrl = 'xxxxx'
    }
	@logClass
    class Httpclient{
		
    }
	var http:any = new Httpclient();
	console.log(http.apiUrl)
	//有参
	//装饰器工厂
     function logClass(params:string){
         return function(target:any){
             console.log(params)
             console.log(target)
         }
    }
	@logClass('hello')
    class Httpclient{
		
    }
	//属性构造器
        //第一个参数原型对象，第二个参数成员的名字
    function logProperty(params:any){
        return function(target:any,attr:any){
            console.log(target) //原型对象  target.attr = params
            console.log(attr)  //属性名称
        }
    }
	//方法装饰器
	//第一个参数静态成员来说是类的构造函数，实例成员来说是类的原型对象
	//第二个参数是成员的名字
	//第三个参数是成员的属性描述符
    function  logMethod(params:any){
        return function(target:any,methodName:any,desc:any){
            console.log(target)
            console.log(methodName)
            console.log(desc)
        }
	}
	//方法参数装饰器
	//第一个参数静态成员来说是类的构造函数，实例成员来说是类的原型对象
	//第二个参数是参数的名字
	//第三个参数是函数参数列表中的索引
	执行顺序
    	属性装饰器(从后向前)
        方法装饰器(从后向前)
        方法参数装饰器(从后向前)
        类装饰器(从后向前)
```

