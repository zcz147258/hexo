---
title: MySql
date:
updated:
type: "tags"
comments:
categories: DataBase
description: MySql
keywords: MySql
top_img: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=2495164343,1369797041&fm=26&gp=0.jpg
cover: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=2495164343,1369797041&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 据库（MySQL）

 

### 1、什么叫数据库？

```
将具有一定逻辑意义的数据组织到一起，叫数据库（存储数据的仓库）。
数据库，是一个长期存储在计算机内的、有组织的、有共享的、统一管理的数据集合。
```

### 2、目前市场上的数据库软件有：

数据库排名：

```
https://db-engines.com/en/ranking
```

![](db.png)

noSQL（非关系型数据库）:

```
JSON
XML
MongoDB
Redis
MemcacheDB
...
```

SQL（SQL:structure query language:结构化查询语言。凡是使用SQL语言的数据库都属于关系型（数据与数据之间是有一定的逻辑关系的）数据库。SQL属于嵌入式语言，不能单独使用！结构化查询语言，用关系表存储数据，属于第三方语言，不能单独使用）:

因为在数据库中是以数据表（关系表：不允许出现表中套表的情况，行和列必须是原子的、不可分割的）形式存储数据的。

```mysql
oracle
mysql
sql server
PGSQL
DB2（IBM）
SQLite
MariaDB(由mysql团队开发，开源的)
```

数据库说明：

```mysql
oracle:企业级数据库，安全性最高   (PL-SQL)
sql server:网络数据库（T-SQL)
mysql:个人关系数据库，安全性小，存储数据量小(SQL)
```

MySQL下载

```mysql
https://dev.mysql.com/downloads/mysql/
```

注意：只有社区版是免费的。

### 3、数据库发展历程

```
结绳记事->竹简记事->纸质->文件管理->数据库管理->大数据
```

### 4、数据库组成

```
DBS（DataBase System）（DBMS（操作数据库或数据表的软件）、DBA（数据库管理员））（计算机硬软件、DBMS、DBA等组成）->DB（数据库）->Table（基表）->data（数据）
```

### 5、SQL主要组成

```mysql
DDL:数据定义语言
    create 创建文件
    alter  修改文件结构
    drop   删除文件（一旦删除，不能恢复）
DML:数据操纵语言
    insert  添加数据
    delete  删除数据
    update  修改数据
DQL:数据查询语言
    select（学习的重点） 数据查询
DCL:数据控制语言
    grant   添加权限
    revoke  删除权限
...
```

### 6、MySQL官网下载（需要注册登录）

```
https://dev.mysql.com/downloads/mysql/5.7.html#downloads
```

### 7、配置环境变量

### 8、启动/停止服务

```mysql
net start mysql
net stop mysql

Tip（技巧）:
    必须先启动服务，然后才能进入到MySQL环境下进行相关操作
```

### 9、进入到MySQL命令界面

```
mysql -uroot -p
输入密码
Tip:
    密码最好不要暴露在外面。
```

```
退出命令行界面
（1） \q
（2）exit
（3）quit
（4）Ctrl+C
```

### 10、查看所有数据库

```
show databases;   //查看所有数据库。每条命令必须有分号结束
```

### 11、打开指定数据库

```
use 数据库名;
```

```
查看当前数据库中的数据表
show tables;
```

### 12、创建数据库

#### 1、图形界面创建

![](createdb.png)

#### 2、用命令创建数据库

```
create database 数据库名 charset="utf8" collate="utf8_general_ci";

说明：
	1）如果只有一个命令行，可以不以分号结束；但是如果要同时执行多条命令，必须在每条命令最后要加上分号，最后一条可以不加；
	2）命令不分大小写，但字符串中的字符是区分大小写。
```

### 13、删除数据库

```
drop database 数据库名;
```

### 14、数据库备份

```
mysqldump -u用户名 -p 被备份的数据库名 > [路径]要备份的文件名.sql   （“>“：重定向符，表示以覆盖方式写入的意思。）
（输入密码）
注意：不能在mysql的环境中使用命令去备份。
备份数据库所有表的数据
    mysqldump –u用户名 –p 数据库名 > 文件名.sql
备份数据库某个表的数据
    mysqldump –u用户名 –p 数据库名  数据表名>文件名.sql
```

### 15、恢复备份文件

```
1）先创建新的数据库
2）mysql -u用户名 –p 新数据库名 < 文件名.sql
```

### 16、图形界面操作数据库

![1560763365878](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1560763365878.png)

### 17、数据库操作步骤：

```
1）需求分析（非常重要！后台开发主管）
2）概念设计（形成E_R图（实体联系图））
3）逻辑设计（把E_R图转换为关系表）
4）实施（利用数据库软件把上面的关系表形成文件）
```

### 18、创建数据表

注意：必须先切换数据库！！！

字段名（表中的一列，叫一个字段｜列｜属性列｜数据项）

记录（表中的一行，叫一条记录｜元组）

```
关系表：是二维表（由行和列组成的表），它的行和列是原子的、不可分割的；不能有重复的列和行；行间是无序的，列也可以是无序的。
```

创建表时，要先创建结构，再输入数据。

表结构包含：字段名（列名）、数据类型（存储数据的方式）、长度、小数位数、约束（主键、是否为空....）

1）图形界面创建。

2）命令创建

### 19、数据类型 （在内存中存储数据的方式）

```mysql
位 bit 1字节(0/1)：主要用于表逻辑关系。

数字（由数字、正负号、小数点和e或E组成，除了decimal、real、numerice需要设置宽度外，其它都不需要设置，系统默认了）
    整数：
    	int（整数，4个字节） bigint 8个字节 smallint（2个字节）tinyint（1个字节 -128--127）
    实数：
        decimal（实型，10进制小数，精度为17位）（总位数（包含小数点在内），小数位数  7，2）
        float（单精度，占4个字节，7位有效）    12.34e-3
        double（双精度，占8个字节，15位有效）  12.34e-3 
        real（实型）
        numerice(数值型)
文本（由键盘上能输入的字符组成，必须要设置宽度，除text外）
    char（有限长度，定长）
    varchar（可变长度）
    text（大文本，一般用于表示大批量文本内容，比如个人简历、备注等）
时序类型（系统默认宽度）
    datetime（日期时间） '2019-6-17 05:40:10 pm'
    date（日期）
    time（时间）   
```

### 20、约束

```mysql
NOT NULL（不能为空）/ NULL
    NOT NULL指示某列不能存储 NULL 值，主键的值不能为空（切记）
UNIQUE（唯一，值不能重复，也可以叫做候选关键字）
    保证某列的每行必须有唯一的值，最多可以有一个值是null。
PRIMARY KEY（PK,主键:值不能重复,且值不能有null的出现。）
    NOT NULL 和 UNIQUE 的结合，确保某列（或两个列多个列的结合）有唯一标识
DEFAULT（设置默认值）
    规定没有给列赋值时的默认值
CHECK（检查约束）
    保证列中的值符合指定的条件
FOREIGN KEY（FK,外键约束）（在一张表中它是主键，在当前这张表不是主键，在当前这张表中把它叫外键；它的作用是用来连接其它表）
    保证一个表中的数据匹配另一个表中的值的参照完整性
```

### 21、创建数据表

```mysql
create table 表名(列名1 数据类型 [（总宽度[,小数位数]）] [约束],列名2 数据类型 [（总宽度[,小数位数]）] [约束],...)
```

```mysql
use stumanager

create table course(id int auto_increment primary key,cno char(10),cname varchar(20) not null,credit int not null)

备注：auto_increment（自动编号，它的类型必须是数值型，创建好结构后输入数据时不需要输入内容）


create table stu(sno char(10) primary key,sname varchar(10) not null,sex char(2) default '女',birthday date null,age int check(age>0 and age<80),department varchar(20),tel char(11) unique)


 auto_increment:自动编号，如果某个字段要设置成自动编号，它首先必须是int型！
```

说明：

​	图形界面操作主要用于初始数据输入；用代码实现主要用在后台开发中。

### 22、数据表结构修改

如果表结构已建好，但又要去修改其中的内容，这时不能再用create table，只能用alter table来实现。

```
查看表结构：
	desc 表名
```

修改表结构语法：

```mysql
alter table [table_name] [add|change|drop|modify] [column] [type];
```

举个栗子：

```mysql
// 添加一列
alter table course add publish varchar(20) default '清华大学出版社'

alter table course modify cno primary key(cno)
// 添加多列
alter table course add publish1 varchar(20) default '清华大学出版社',add publish2 varchar(20) not null
```



```mysql
// 修改列结构(被修改的列名必须是已经存在的)，modify不能修改列名 =>只用来修改列的其它属性。
alter table course modify publish1 char(10) default '秦思出版社'
```

```mysql
// change用来修改列名和该列的其它属性   => 主要用来修改列名。
alter table course change publish1  pub1 char(15) default '?????'
```

```mysql
// 删除列,drop后只带列名即可
alter table course drop publish,drop pub1,drop publish2
```

```mysql
// 修改表名
rename table course to cs
```

### 23、外键（foreign key:fk）

```mysql
定义：在一个表A中它不是主键，但在另一个表B中它是主键，在表A中它叫外键。
作用：外键是用来连接两张表的。

注意：一张表有且只能有一个主键，但是主键可能是由多个列组成！！！外键可以有多个！
```

```mysql
-- 学生表
create table student
(
sno int primary key,
sname varchar(50) not null,
ssex varchar(50) not null,
sbirthday date,
class varchar(10)
)
-- 教师表
create table teacher
( 
tno varchar(50) primary key,
tname varchar(50) not null,
tsex varchar(50) not null,
tbirthday date,
prof varchar(50),
depart Varchar(10) not null
)
-- 课程表
create table course
( 
cno char(5) primary key,
cname Varchar(10)not null,
tno Varchar(50) not null,
foreign key(tno) references teacher(tno)
)
-- 成绩表
create table score
(
sno int not null,
cno Char(5) not null,
score decimal(5,1),
primary key(sno,cno),
foreign key(sno) references student(sno),
foreign key(cno) references course(cno)
)
注意：创建表是一定先要创建主键所在的表，再创建外键所的表！！！先创建1方的表，再创建n方的表。
```

### 24、设置组合关键字

```mysql
create table score
(
sno int not null,
cno Char(5) not null,
score decimal(5,1),
primary key(sno,cno),
foreign key(sno) references student(sno),
foreign key(cno) references course(cno)
)
```

### 25、添加数据

1）命令格式

```mysql
增加一个数据
    insert into [table_name] values([value1, ...])
    
增加多个数据
    insert into [table_name] value([value1, ...]), ([value2, ...]), ...
    insert into [table_name]([column1, ...]) value([value1, ...]), ([value2, ...]), ...
    
注意：
    1）value和values都可以用，但是，如果插入一条最好用values，而插入多条最好用value，这样用执行的效率较高。
    2）先添加主键所在表（主表）的数据，再添加外键所在表（子表）的数据。
```

  2）添加一条数据

```mysql
insert into student values(11100,'张三','男','1990-9-9','18级计科一班')
insert into student(sno,sname,ssex) values(11101,'王老五','男')
```

3）添加多条数据

```mysql
 insert into student value(11102,'aa','男','1990-9-9','18级计科一班'),(11103,'bb','男','1990-9-9','18级计科一班'),(11113,'cc','男','1990-9-9','18级计科一班')
```

### 26、复制表

```mysql
方法1：CREATE TABLE bk(SELECT * FROM USER); （推荐用法）
create table stu2(select * from student)  /*复制整个表*/
create table stu3(select * from student where false)  /*只复制表结构*/
create table stu4(select sno,sname,class from student)  /*复制部分列及列中的数据*/

方法2：INSERT INTO bk SELECT * FROM  user
I）create table student
    (
    sno int primary key,
    sname varchar(50) not null,
    ssex varchar(50) not null,
    sbirthday date,
    class varchar(10)
    )
II）insert into stu1 select * from student;
```

### 27、删除数据

1）delete（指定表中的数据全部或部分删除）

命令格式：

```mysql
delete from [table_name] where [condition];
```

```mysql
delete from stu1 where ssex = '男'
delete from stu2 where sname like '王%' and year(sbirthday)>197
delete from stu2
```

2）truncate（删除指定表中所有数据，不能带条件，删除后不能恢复，删除后结构仍然在，数据没有了）

```mysql
truncate table stu1
```

### 28、修改表中数据

1）语法

```mysql
update [table_name] set [column1 = value1, ...] where [condition];
```

2）示例

```mysql
-- 将stu1表中曾华改成曾小华，性别为女性。
update stu1 set sname = '曾小华',ssex = '女' where sname='曾华'
```

```mysql
-- 计算平时成绩（总成绩*60%）
alter table score_copy1 add finscore decimal(6,2)
update score_copy1 set finscore = score * .6
```

### 29、数据查询

基本语法格式：

```mysql
select [distinct] *|列名表｜表达式 [<as> 别名]                 -- 选择列
from 表名列表 [[as] 别名]										-- 数据来源（表名）
where <条件>												   -- 基本条件
group by [列名列表]											  -- 分组
having <带集合函数的条件>										-- 分组条件
order by [列名列表][asc|desc]								  -- 排序
limit 起始下标[,<条数>]										 -- 分页
```

1）基本查询

```mysql
select * from <table_name>; -- *表示所有列    查询所有列所有数据
select [column1], [column2]... from [table_name];  -- 查询指定列所有数据
select [column1] as [alias1], [column2] as [alias2]... from [table_name]; -- 查询指定列所有数据，并为列取别名，as可以省略不写
select [exp1] as [alias1], [exp2] as [alias2]... from [table_name];
```

举个栗子：

```mysql
select * from student
select sname,sbirthday from student
-- 输出所有学生的年龄
select sname 姓名,year(now())-year(sbirthday) as 年龄 from student


-- 把年龄加入到stu表中
create table stu(select * from student)
desc stu
alter table stu add age int
update stu set age = year(now())-year(sbirthday)
```

2）去重（去掉重复的行）

```mysql
select distinct [column1], [column2]... from [table_name];
```

举个栗子：

```mysql
-- 哪些学生选修课程了？
select distinct sno from score
```

3）条件查询

```mysql
select * from [table_name] where [condition];

	condition（条件）:
        关系运算符
            =（等于）、!=或<>（不等于）
            >（大于）、<（小于）
            >=（大于等于）、<=（小于等于） 优先级：谁先出现就先算谁
        逻辑运算符
            not（非）、and（与）、or（或）  优先级：not>and>or
        区间查询
            between ... and ... 相当于and运算
                在某个范围内
            in (...)  相当于or运算
                多个可能值
        模糊查询
            like ...（只能操作字符型数据）
                %匹配任意0个或多个字符
                _匹配任意1个字符
            rlike ...
                匹配正则表达式
        判空
            is null/is not null     千万不能写  =null
		集合运算：
			some
			any
			all        
```

举个栗子：

```mysql
select * from score where not score>=80;
select * from score where score<80;
select * from score where score=75;
select * from score where score!=75;
select * from score where score<>75;
```

```mysql
select sname from student where ssex='男' and class='95033'
```

```mysql
select * from score where score between 80 and 90;
-- 等价于
select * from score where score >= 80 and  score <= 90
```

```mysql
select * from student where sname in ('王丽','李军');
select * from student where sname = '王丽' or sname = '李军'
```

```mysql
select * from student where sname like '%小%';
select * from student where sname like '%小';
select * from student where sname like '_小_';
select * from student where sname like '_小';

注意：like只能对字符型（char,varchar,text,date,time,....）的数据进行查询，不要用它去查询日期型数据。

select * from student where year(sbirthday)>1990;
```

```mysql
select * from student where class is null;
```

4）聚合

```mysql
select aggr_func([column]) from [table_name] where [condition];
    
聚合（集合）函数有：
    count:汇总（用来统计行数）,可以操作所有类型的字段或用*表示（列/数据项）
    max:最大值，只能操作字符型、数值或日期、时间型数据
    min:最小值，只能操作字符型、数值或日期、时间型数据
    sum:求和，只能操作数值数据
    avg:求平均值，只能操作数值型数据
```

举个栗子：

```mysql
select count(sname)  from student;
select count('sdfdfd') 人数 from student;

select count(*) 人数 from student where ssex='男';

select max(score) 最高分 from score
select min(score) 最低分 from score


select sno,sum(score) 总分 from score group by sno
select sno,avg(score) 平均分 from score group by sno 
select sno,avg(score) 平均分 from score group by sno order by avg(score) desc
```

```mysql
select count(*) 人数 from student;
select count(sno) 人数 from student;
select count(sno) from student

select avg(score) 平均分 from score
select max(score) 最高分 from score
```

5）分组

```mysql
select [column] as [alias], count(*) 
from [table_name] 
where [condition] 
group by [column];
```

举个栗子：

```mysql
-- 统计每个班的人数
select class,count(*) as 每班人数 from student group by class;
```

```mysql
- 输出每个学生的平均分
select sno,avg(score) 平均分 from score group by sno;

注：分组后一般用集合函数实现相关操作。
```

6）分组条件（必须先分组，后使用条件，条件一般用聚合函数实现，也即是说：凡含有聚合函数的条件必须写在having后。）

```mysql
select * from [table_name] where [condition] group by [column] having [condition];
```

举个栗子：

```mysql
-- 查询选修两门课以上的学生。
select sno,count(*) 选修课程数 
from score
group by sno
having count(*)>=2
```

```mysql
-- 查询选修2门及以上课程的学生。
select * from score group by sno having count(*)>=2;
```

7）排序

```mysql
select * from [table_name] order by [column1] [asc|desc], [column2] ]asc|desc],...

Tip: 默认为升序排序。先按第一关键字排序，第一关键相同的再排序第二关键字。。。。。。
```

   举个栗子：

```mysql
select * from student order by sbirthday;
select * from student order by sbirthday asc;
select * from student order by sbirthday desc;

select * from student order by sbirthday desc,sno asc;
```

```mysql
-- 按成绩降序排序，成绩相同再按学号进行升序排序。
select * from score order by score desc,sno
```

8）分页

```mysql
select * from [table_name] limit [start], [count];
```

```mysql
-- 分页实现：
select * from score limit (页码-1)*每页显示的条数,每页显示的条数;
```

举个栗子：

```mysql
-- 查询考试成绩前三的学生。
select sno,score from score order by score desc limit 3;
```

### 30、子查询（嵌套查询：select语句的嵌套）

​	子查询最多可以嵌套128层，一般建议不要超过三层。

##### 30.1 子查询

​	1）标量查询

​	子查询返回一列一行的查询结果。

```mysql
-- 查询操作系统的最高分。
select max(score) 操作系统最高分 from score where cno = (
    select cno from course where cname = '操作系统')
```

​	2）列级子查询

​	子查询返回一列多行的查询结果。

```mysql
-- 查询选修两门及以上课程的学生的姓名。

select sname from student where sno in (
    select sno from score group by sno having count(*)>=2)
```

3）多列一行

```mysql
select * from (select sno,sname from student where sno='107') temp
```

4）多列多行

```mysql
select sname from (select sno,sname from student) temp where sno='107'
```

#####  30.2 any，in，some，all区别

注意：

​		1）any,some和all只能用在子查询中，in可以用在子查询中，也可以用在单表查询中。

​		2） any,some和all通常与=、>、>=、<、<=、<>结合起来使用 

​		3）any和some功能一样，都是表示大于或小于或...其中任意一个值即可。（如果是 >any:表示大于最小的那个）

all表示大于或小于或...所有的（如果是 >all:表示大于最大的那个）。

```mysql
-- 查询成绩高于操作系统成绩的学生。

select * from score where cno =(
	select cno from course where cname='操作系统');		
		
select * from score where score >any(
	select score from score where cno =(
		select cno from course where cname='操作系统'));		
		
select * from score where score >some(
	select score from score where cno =(
		select cno from course where cname='操作系统'));

select * from score where score >all(
	select score from score where cno =(
		select cno from course where cname='操作系统'))
```

### 31、多表查询

​	1）简单查询（等值连接，交集运算）

```mysql
select sname,cname,score 
from student,course,score
where student.sno = score.sno and course.cno = score.cno and sname = '王丽' and cname = '数字电路'

select a.sno,sname,cname,score 
from student a,course as b,score c
where a.sno = c.sno and b.cno = c.cno and a.sname = '王丽' and cname = '数字电路'

Tip:
    多表查询时，如果列名在多张表中出现，必须界定是哪张表的列。
```

```mysql
-- 基本关系运算：选择、投影和连接
-- 数学关系运算：并、差、交（等值连接或inner join实现）和笛卡尔积

-- 等值连接（交集运算）
-- 每位学生的每门的考试成绩。

select sname,cname,score 
from student,course,score
where student.sno=score.sno and course.cno=score.cno-- 凡是涉及到多张表的查询时，必须要对表进行两两连接（用外键进行连接）

select sname,cname,score 
from student,course,score
where student.sno=score.sno and course.cno=score.cno and sname='曾华'

select sname,cname,score 
from student as a,course b,score c
where a.sno=c.sno and b.cno=c.cno and sname='曾华'

select a.sno,sname,cname,score 
from student as a,course b,score c
where a.sno=c.sno and b.cno=c.cno and sname='曾华';

select c.sno,a.sname,b.cname,c.score 
from student as a,course b,score c
where a.sno=c.sno and b.cno=c.cno and sname='曾华'
```

​	内部连接（[inner] join ... on ...）

```mysql
-- 每位学生的每门的考试成绩。
select sname,cname,score 
from student a join score b on a.sno=b.sno  -- 逻辑连接
							 join course c on b.cno=c.cno

select sname,cname,score 
from student a join score b on a.sno=b.sno  -- 逻辑连接
							 join course c on b.cno=c.cno
where sname='曾华'	


select sname,cname,score 
from student a inner join score b on a.sno=b.sno  -- 逻辑连接
							 inner join course c on b.cno=c.cno
where sname='曾华'  -- inner join：内部连接
```

2）笛卡尔积（两张表相乘）

​	如果有两张表，笛卡尔积后，两张表所有列相加，行相乘。

​	语法：

```mysql
select * from 表1 join 表2 [join <表3> ....]
```

​	举个栗子：

```mysql
select * from student join course
```

​	3）内连接查询 inner join（交集运算）

​	语法：**select \* from a_table a inner join b_table b on a.a_id = b.b_id;**

​	**说明**：组合两个表中的记录，返回关联字段相符的记录，也就是返回两个表的交集（阴影）部分。

![img](https://img-blog.csdn.net/20181005173658980?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pqdDk4MDQ1MjQ4Mw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

​	举个栗子：

```mysql
select student.sno,sname,cname,score 
from student join score on student.sno = score.sno join course on course.cno = score.cno
where sname = '王丽' and cname = '数字电路'
```

4）外部连接（差集运算）

​	I）左外连接 left outer join

​	语句：SELECT * FROM a_table a left [outer] join b_table b ON a.a_id = b.b_id;

​	说明： left join 是left outer join的简写，它的全称是左外连接，是外连接中的一种。

​	左(外)连接，左表(a_table)的记录将会全部表示出来，而右表(b_table)只会显示符合搜索条件的记录。右表记录不足的地方均为NULL。

![img](https://img-blog.csdn.net/20181005211357263?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pqdDk4MDQ1MjQ4Mw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

​	举个栗子：

```mysql
select * from student left join score on student.sno = score.sno
```

II）右外连接（right join on / right outer join on）

​	语句：SELECT * FROM a_table a right outer join b_table b on a.a_id = b.b_id;

​	说明：right join是right outer join的简写，它的全称是右外连接，是外连接中的一种。

​	与左(外)连接相反，右(外)连接，左表(a_table)只会显示符合搜索条件的记录，而右表(b_table)的记录将会全部表示出来。左表记录不足的地方均为NULL。

![img](https://img-blog.csdn.net/20181005213457811?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pqdDk4MDQ1MjQ4Mw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

​	举个栗子：

```mysql
select * from student right join course on student.sno = course.cno
```

III）全连接（MySQL没有全连接，而SQL Server有）（不用掌握）

mysql默认不支持full join 。 什么是full join呢就是left join+right join 可以使用union联表解决这个问题。

举个栗子：

```mysql
select b.title,b.content,a.class_name,a.id as classid from news_class as a left join news as b on a.id=b.id
union all  
select b.title,b.content,a.class_name,a.id as classid from news_class as a right join news as b on a.id=b.id;
```

5）联合查询（并表查询）（union/union all）

​	联合查询执行的是并集运算。

```mysql
不去重
    select * from [table_name1] union all select * from [table_name2]
去重
    select * from [table_name1] union select * from [table_name2]
```

```mysql
union语句注意事项：
    1.通过union连接的SQL它们分别单独取出的列数必须相同；
    2.不要求合并的表列名称相同时，以第一个sql 表列名为准；
    3.使用union 时，完全相等的行，将会被合并，由于合并比较耗时，一般不直接使用 union 进行合并，而是通常采用union all 进行合并；
    4.被union 连接的sql 子句，单个子句中不用写order by ，因为不会有排序的效果。但可以对最终的结果集进行排序；
    (select id,name from A order by id) union all (select id,name from B order by id); //没有排序效果
    (select id,name from A ) union all (select id,name from B ) order by id; //有排序效果
```

```mysql
-- 查询王丽和曾华计算机导论的成绩。

select sname,cname,score
from student join score on student.sno = score.sno join course on course.cno = score.cno
where sname = '王丽' and cname = '计算机导论'
union all
select sname,cname,score
from student join score on student.sno = score.sno join course on course.cno = score.cno
where sname = '曾华' and cname = '计算机导论'
```

```mysql
select sno from student
union all
select sno from score
```

```mysql
select sno from student
union all
select sno from score
order by sno
```

```mysql
-- 查询选修两门及以上课程的学生的姓名。

select sname from student where sno in (
    select sno from score group by sno having count(*)>=2)
```

32、视图

视图就是由物理表（基表）派生出来的表（虚拟表）。

select查询的结果是一次性的，如果下次要这个查询结果，这个select语句要再次执行一次。

如果要想把查询的结果保存起来，这就是视图的职能。

语法格式：	

```mysql
create view 视图名 as select语句
```

```mysql
-- 创建视图
create view v_student_score as 
	select sname,cname,score from student a,course b,score c where a.sno=c.sno and b.cno=c.cno
	
-- 利用视图进行查询操作	
select * from v_student_score	
```

