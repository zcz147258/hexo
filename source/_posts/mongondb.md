---
title: Mongondb
date:
updated:
type: "tags"
comments:
categories: DataBase
description: Mongondb
keywords: Mongondb
top_img: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1139235225,3544810372&fm=26&gp=0.jpg
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1139235225,3544810372&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.下载安装配置

```
https://fastdl.mongodb.org/win32/mongodb-win32-x86_64-2008plus-ssl-4.0.18-signed.msi
```

```
自定义安装  不安装compress
```

# 2.使用

```
mongodb  数据库服务器  可以有多个数据库

collection 集合  类似于数组  在集合中可以存放文档

document  文档  是数据库中最小的单位
```

# 3.基本操作

```
show  dbs  展示当前所有的数据库
user  数据库名   进入指定数据库中
db  表示当前所处的数据库
show collections  展示数据库中有多少集合

数据库的CRUD操作

增加
	db.<collection>.insert(doc)   向集合中插入文档
	如果没有指定_id那么就  自动生成指定_id
	insertone()  插入一个
	insertmany()  插入多个
查询	
	db.<collection>.find()    查询当前集合中的所有文档
	db.first.find({age:18})   查询符合条件的
	db.first.find({name:"李淳风",age:18})
	db.first.findOne({name:"李淳风",age:18})  查找符合的第一个
	db.first.find({name:"李淳风",age:18}).count()  统计数量
	//查询内嵌文档  就是对象内部的对象  .格式来查询  也可以对数组中的元素进行匹配
	db.first.find({"hooby.movies":""hero})
	向数组中添加值
	//比较运算符
   		$get 大于等于
   		查询等于  500的
   			db.frist.find({num:500})
   		查询大于  5000的
   			db.frist.find({num:{$gt:500})
   		查询小于
   			db.frist.find({num:{$lt:500})
   		查询大于小于
   			db.frist.find({num:{$gt:50,$lt:100})
   		查询前10条
   			db.frist.find().limit(10) 
   		查询  11-20条
   			db.frist.find().skip(10).limit(10) 
   		查询  小于10   大于  500的
   			db.frist.find({$or:[{sal:{$lt:10}},{sal:{$gt:500}}]})
   		增加工资 在基础上增加400元
   			db.emp.updateMany({sal:{$lt:1000}},{$inc:{sal:400}})
	
修改
	db.firstup.updateOne('查询条件','修改条件')  //默认是新对象替换旧对象
	修改操作符号
	$set   用来修改文档中的指定属性
	$unset  用来删除文档中的制定属性
	
	db.firstup.updateMany('查询条件','修改条件')   //修改多个符合条件的问答文档
        db.first.updateMany(
            {name:"李淳风"},
            {$set:
                {address:"高老庄"}
            }
   		 )
   	也可以update()第三个参数传  {multi:true}   修改多个
   	db.first.update({username:"唐僧"},{$push:{"hooby.movies":"Inter"}})
   	//$addToSet   像数组中添加一个元素，如果存在就不添加
   	//替换
   	db.user.replaceOne({username:"猪八戒"},{username:"唐僧"});
   	
   	
   	
删除
	db.firstup.remove()   //删除符合的所有文档
	db.firstup.removeOne()   //删除符合的第一个文件
	db.firstup.removeMany()   //指定删除多个
	db.first.remove({})  //清空
	db.first.drop()  //清空 性能好点
```



# 4.破解

```
按住运win 和 r 键输入 regedit
HKEY_USERS\S-1-5-21-xxxxxxxxxxxxxx\SOFTWARE\JavaSoft\Prefs\3t\mongochef\enterprise

将除了 installation-date-2019.2.1（这个是软件安装日期的时间戳）这个项以外的项数据修改为空，再次打开软件就又是30天试用了

```

# 5.文档之间的关系

```
一对一  内嵌文档的方式处理

一对多  
		还可以通过分表  userid关联数据
		也可以通过内嵌文档
		
多对多	
		分类  商品的关系
		也可以通过分表  userid来查询数据
```

# 6.排序

```
//以工资排序
db.first.find({}).sort({sal:1})  	 升序
db.first.find({}).sort({sal:-1})      降序
db.first.find({}).sort({sal:1,empno:-1})     先按照升序，再按照降序排序


先  sort limit  skip  没有顺序关系

```

# 7.查询

```
//查询时候，可以在第二个参数的位置来设置投影
db.emp.find({},{ename:1,_id:0})   1显示字段   0不显示字段


//查询去掉重复的
db.user.distinct("name")
//查询大于
db.user.find({age:{$gt:22})
//查询小于
db.user.find({age:{$lt:22})
//查询大于等于
db.user.find({age:{$gte:22})
//查询区间数字
db.user.find({age:{$gte:22,$lte:26})
//查询包含关键字的
db.user.find({"name":/Z/})
//查找Z开头的
db.user.find({"name":/^Z/})
//查找结尾的
db.user.find({"name":/Z$/})
//查找指定列
db.user.find({},{name:1,age:1 })  //前者写条件
//升序降序
db.user.find().sort({age:1})  //升序
db.user.find().sort({age:-1})  //升序
//查询前五条
db.user.find().limit(5)
//查询10条以后
db.user.find().skip(10) 
//查询11-15条
db.user.find().skip(10).limit(5)
//统计数量
db.user.find().count()
//或者查询 or
db.user.find({$or:[{age:22},{age:25}]})
//查询第一条符合数据
db.user.findOne()
```

# 8.修改

```
//新增列增加数据
db.user.update({"name":"小明"},{$set:{"age":16}})
//不加$set
$set  就是完整替换
//批量修改数据
db.user.update({"name":"小明"},{$set:{"age":16}},{multi:true})
```

# 9.大数据查询的优化

```
索引是对数据库表中一列或者多列进行排序的一种结构，可以让查询数据库变得很快，但是会让更新和增加慢点

//查询语句的具体执行时间
tb.user.find().explain("executionStates")

//查看有没有设置索引
db.user.getIndexes()

//设置索引
db.userensureIndex({"username":1})
//删除索引
db.user.dropIndex({"username":1})

//复合索引
一般会以第一个索引为主索引，查询比较快

//唯一索引
db.user.ensureIndex({"userid":1},{"unique":true})
```

# 10.账户权限配置

```
//创建超级管理员账户
db.createUser({
    user:'admin',
    pwd:'123456',
    roles:[{role:'root',db:'admin'}]
})
//第二步修改配置文件
配置
security:
  authorization: enabled
//第三步
	重新启动
	services.msc
//mongo admin -u 用户名 -p 密码
//给其中一个数据库分配权限
db.createUser({
    user:'root',
    pwd:'123456',
    roles:[{role:'dbOwner',db:'mongoose'}]
})
mongo nest-blog-api -u blog -p 123456  进入指定数据库

//角色命令
show users  //显示角色
db.dropUser("nest-blog-api")  //删除用户
db.updateUser("admin",{pwd:"123456"})  //修改密码
db.auth("admin","password")
```

# 11.聚合管道

```
使用聚合管道可以对集合中的文档进行变换和组合
管道操作符号
	$project  //增加 删除重命名字段
	$match    //条件匹配  只满足条件的文档才能进入下一阶段
	$limit    //限制结果的数量
	$skip     //跳过文档的数量
	$sort     //条件排序
	$group    //条件组合结果
	$loopup   //引入其他的集合的数据
	$sum      //求和
	//$project
        db.order.aggregate([
            {
                $project:{name:1,age:1}  //只查找部分列
            }
        ])
	//$match
		db.order.aggregate([
            {
                $project:{name:1,age:1}  //只查找部分列
            },
            {
                $match:{"age":{$gte:90}}  //查找大于90的数据
            }
		])
	//$group
		db.order.aggregate([
            {
                $group:{_id:"$order_id",total:{$sum:"$num"}}//分组求和
            }
		]}
	//$sort
		db.order.aggregate([
            {
                $project:{name:1,age:1}  //只查找部分列
            },
            {
                $match:{"age":{$gte:90}}  //查找大于90的数据
            },
            {
                $sort:{"price":-1}    //降序排序
            }
		]}
	$limit
    	db.order.aggregate([
            {
                $project:{name:1,age:1}  //只查找部分列
            },
            {
                $match:{"age":{$gte:90}}  //查找大于90的数据
            },
            {
                $sort:{"price":-1}    //降序排序
            }，
             {
                $limit:10    //分页
            }，
		]}
	//$skip
		db.order.aggregate([
            {
                $project:{name:1,age:1}  //只查找部分列
            },
            {
                $match:{"age":{$gte:90}}  //查找大于90的数据
            },
            {
                $sort:{"price":-1}    //降序排序
            }，
             {
                $limit:10    //分页
            }，
            {
                $skip:10    //跳过
            }
		]}
		//表关联 $lookup
		db.order.aggregate([
            {
                $lookup:{
                    from: "order_item",//关联的表,
                    localField:"order_id",//关联字段,
                    foreignField:"order_id", //关联的表的id,
                    as:"items"//查询完重新命名
                }
            }
		])
```

