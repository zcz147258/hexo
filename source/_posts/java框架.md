---
title: Java框架
date:
updated:
type: "tags"
categories: Java
comments:
description: Java框架
keywords: Java框架
top_img: https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=564071848,1846939077&fm=26&gp=0.jpg
cover: https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=564071848,1846939077&fm=26&gp=0.jpg
mathjax: 
katex:
aside:
aplayer:
highlight_shrink:
---
# 一.maven

```java
项目管理工具
	使用maven来构建，会发现总体上工程文件会小很多
		jar包的坐标，放在 xml配置文件
	核心功能
	依赖管理，maven工程对jar包的管理
	一键构建 指的是项目从编译测试运行，打包，安装部署，整个过程都交给maven进行管理
```

## 1.1仓库的种类

```java
本地仓库
中央仓库
远程仓库（私服）
```

## 1.2配置文件

```java
核心代码部分
配置文件是  jar包之外的部分，不把他打包在 jar包里面
单元测试
测试配置文件
	
	标准目录结构
		src/main/java  核心代码部分
		src/main/resource 配置文件部分
		src/test/java 测试代码部分
        src/test/resource 测试配置文件
        src/main/webapp 页面资源 js css html
```

## 1.3maven常用指令

```java
mvn clean  删除掉target目录 
mvn compile  编译
mvn test   会把测试代码进行编译，会把main下面的主代码编译
mvn package  打包，把测试/main代码编译
mvn install  编译测试打包，把项目打包在本地仓库
mvn deploy  	发布
```

## 1.4创建java工程

```java
    
包是红色，选择  maven 重新导入
```



# 二.mybatis

```java
在 mybatis中把它的持久层的操作接口名称和映射文件 叫做  Mapper
```



## 2.1环境搭建流程

```java

	<dependencies>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.4.5</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.6</version>
        </dependency>
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.12</version>
        </dependency>

        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.10</version>
        </dependency>
    </dependencies>
    3.创建一个实体类对应数据字段，并在数据库中创建对应的数据表它内部封装了  jdbc，开发者只需要关注sql语句本身，不需要创建连接等繁琐的过程！

ORM（Object Relational Mapping）对象关系映射。简单地说，就是把数据库表和实体类及实体类的属性对应起来，让我们可以通过操作实体类来操作数据库表。

配置环境步骤
	1.创建工程
	2.引入mybatis所需jar包
        <dependencies>
            <dependency>
                <groupId>org.mybatis</groupId>
                <artifactId>mybatis</artifactId>
                <version>3.4.5</version>
            </dependency>
            <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
                <version>5.1.6</version>
            </dependency>
            <dependency>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
                <version>1.2.12</version>
            </dependency>

            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>4.10</version>
            </dependency>
        </dependencies>
    3.创建一个实体类对应数据字段，并在数据库中创建对应的数据表
    4.添加mysql配置文件，mybatis配置文件
    	<?xml version="1.0" encoding="UTF-8"?>
                <!--约束-->
                <!DOCTYPE configuration
                        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
                        "http://mybatis.org/dtd/mybatis-3-config.dtd">

                <!--配置环境-->
                <configuration>
                    <typeAliases>
                        <package name="com.it.domain"/>
                    </typeAliases>
                    <environments default="mysql">
                        <!--配置mysql的环境-->
                        <environment id="mysql">
                            <!--配置事务类型-->
                            <transactionManager type="JDBC" />
                            <!--配置数据源连接池-->
                            <dataSource type="POOLED">
                                <!--配置连接数据库的四个基本信息-->
                                <property name="driver" value="com.mysql.jdbc.Driver"/>
                                <property name="url" value="jdbc:mysql://localhost:3306/mybatis"/>
                                <property name="username" value="root"/>
                                <property name="password" value="root"/>
                            </dataSource>
                        </environment>
                    </environments>
                    <!--指定映射文件的位置，每个dao独立的配置文件-->
                    <!--指定带有注解的位置-->
                    <mappers>
                        <!--<mapper class="com.it.dao.IUserdao"/>-->
                        <package name="com.it.dao"/>
                    </mappers>
                </configuration>
                
        5.编写 sql 映射配置文件
        	<?xml version="1.0" encoding="UTF-8"?>
                <!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
                        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
                <mapper namespace="com.it.dao.IUserdao">
                    <!--配置查询所有-->
                    <select id="findAll">
                        SELECT * FROM USER
                    </select>
                </mapper>
              
              注意事项
              		1.mybatis的映射文件配置必须和dao接口的包结构相同
              		2.映射配置文件的mapper标签namespace必须是dao接口的全限定类名
              		3.映射配置文件的操作配置，id属性必须是dao接口的方法名 select
```

## 2.2注解

```java
把Iuserdao.xml删除，在dao接口的方法上 写 @select注解，并且sql语句，同时需要在
sqlmapconfig.xml  mapper配置的时候使用class属性指定接口的全类名
```

## 2.3开始执行

```java
		//读取配置文件
        //创建sqlSessionFactory工厂模式
        //生成sqlSession对象
        //使用sqlSession创建dao接口的代理对象
        //使用代理对象执行方法
        //释放资源
        InputStream in = Resources.getResourceAsStream("sqlmap.xml");
        SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
        SqlSessionFactory factory = builder.build(in);
        SqlSession session = factory.openSession();
        IUserdao userdao = session.getMapper(IUserdao.class);
        List<User> users = userdao.findAll();
        for (User user:users){
            System.out.println(user);
        }
        session.close();
        in.close();
        
        
        保存操作需要提交事务
        	 session.commit();
        	 新增用户后，还需要返回当前用户的id值
        	 <select key keyproperty ="id" 
        	 keyclunm ="id"
        	 order="AFTER" result type="INTERFE">  
        	 select last_insert_id()
        	 用keyproperty 代表要返回的值
        	 
        删除用户
        	parameterType="Integer"
       	查询根据id一个用户
       		parameterType="INt" resulttype="com.it.domain.User"
       	
        模糊查询的占位符分析
        	有两种方法
        		#{}  #%{}%
        	
        
        
        解决数据库添加汉字时候出现？？？
        	在mysql.xml  连接数据库配置文件后面加上
        	?useUnicode=true&amp;characterEncoding=UTF-8"
        	 
        
        代码分析
        	读取配置文件
        		1.使用类加载器，他只能读取类路径的配置文件
        		2.使用sessioncontext对象的getrealpath()
        	创建工厂mybatis使用了构建模式，
        		优势 解耦
        	创建Dao接口实现类使用了代理，
        		优势，不修改源码对已有方法进行增强
```

## 2.4 OGNL表达式

```java
对象图导航语言
	它通过对象中的取值方法来获取数据，在写法上 把get省略了
	因为在 parameterType中已经提供了属性所属的类，
	此时sql表达式不需要写对象名
	
	1.使用实体类的包装对象作为查询对象
	2.
```

## 2.5通过配置properties文件来实现

```java
也可以
<properties>
        <property name="driver" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useUnicode=true&amp;characterEncoding=UTF-8"/>
        <property name="username" value="root"/>
        <property name="password" value="root"/>
    </properties>
    
    下面改为${username}的方式来用
    
    
    
    还可以把属性内的数据库信息放到外部文件  properties内
    然后引入外部
    <properties resouce="jdbcconfig.properties">
    然后配置文件前面加上  jdbc.url
 	引入也加上
 	
 	urI: 统一资源标识符  http://localhost:8080/mybatis/demo1servlet
```

## 2.6typealiases，package标签

```java
typealiases标签 只能配置 domain的别名
package标签   用于指定要配置的包，自动注册别名


	MyBatis的返回参数类型分两种

对应的分类为：
1.1. resultMap :
			 结果集[对象等]
1.2. resultType :	 Integer,String ,Long ,class
```

## 2.7mybatis的连接池的使用

```
开发中都会使用连接池，因为它可以减少我们开发的时间
是一个用来存储连接的容器
	容器其实就是一个集合对象，该集合必须是线程安全的，不能两个线程拿到一个连接，
    该集合还必须实现队列的特性
```

### 2.7.1配置

```java
主配置文件
	datasource 取值
			POOLed    采用传统的java.sql.datasource规范的连接池，有实现
			UNPOOLed	采用了传统的获取链接，虽然也实现sql.datasource规范，但是没有池的思想
			JNDi	采用服务器提供的技术JNDI技术实现，来获取datasource实现，不同的服务器不一样，
					如果不是web或者maven的war工程是不能使用的，tomcat使用的就是dbcp连接池
```

### 2.7.2动态sql语句

```java
sqlif and sql where

if
choose (when, otherwise)
trim (where, set)
foreach


1.if
通常要做的事情是有条件地包含 where 子句的一部分，例如查询年龄，身高，筛选
	<select id="findActiveBlogLike"
         resultType="Blog">
      SELECT * FROM BLOG WHERE state = ‘ACTIVE’ 
      <if test="title != null">
        AND title like #{title}
      </if>
      <if test="author != null and author.name != null">
        AND author_name like #{author.name}
      </if>
    </select>
 
优化
where 元素知道只有在一个以上的if条件有值的情况下才去插入"WHERE"子句。而且，若最后的内容是"AND"或"OR"开头的，where 元素也知道如何将他们去除。
				<select id="findActiveBlogLike"
                     resultType="Blog">
                  SELECT * FROM BLOG 
                  <where> 
                    <if test="state != null">
                         state = #{state}
                    </if> 
                    <if test="title != null">
                        AND title like #{title}
                    </if>
                    <if test="author != null and author.name != null">
                        AND author_name like #{author.name}
                    </if>
                  </where>
                </select>
 
2.choose (when, otherwise)
有些时候，我们不想用到所有的条件语句，而只想从中择其一二。针对这种情况，MyBatis 提供了 choose 元素，它有点像 Java 中的 switch 语句。
        <select id="findActiveBlogLike"
             resultType="Blog">
          SELECT * FROM BLOG WHERE state = ‘ACTIVE’
          <choose>
            <when test="title != null">
              AND title like #{title}
            </when>
            <when test="author != null and author.name != null">
              AND author_name like #{author.name}
            </when>
            <otherwise>
              AND featured = 1
            </otherwise>
          </choose>
        </select>

3.trim (where, set)
如果 where 元素没有按正常套路出牌，我们还是可以通过自定义 trim 元素来定制我们想要的功能。比如，和 where 元素等价的自定义 trim 元素为：
						<trim prefix="WHERE" prefixOverrides="AND |OR ">
                          ... 
                        </trim>
                        
                   <update id="updateAuthorIfNecessary">
                      update Author
                        <set>
                          <if test="username != null">username=#{username},</if>
                          <if test="password != null">password=#{password},</if>
                          <if test="email != null">email=#{email},</if>
                          <if test="bio != null">bio=#{bio}</if>
                        </set>
                      where id=#{id}
                    </update>
                    
4.foreach
	动态 SQL 的另外一个常用的必要操作是需要对一个集合进行遍历，通常是在构建 IN 条件语句的时候。比如：
				<select id="selectPostIn" resultType="domain.blog.Post">
  SELECT *
  FROM POST P
  WHERE ID in
  <foreach item="item" index="index" collection="list"
      open="(" separator="," close=")">
        #{item}
  </foreach>
</select>
	foreach 遍历
	collection  代表要遍历的集合元素
	open开始的部分  
	close  结束的部分
	item 代表遍历集合的每个元素，生成的变量名
	sperator  分隔符
```

## 2.8多表查询

```java
1.创建一个新的类 ，继承account，tostring方法要super.toString

2.体现出主表和从表的关系
		1.从表实体应该包含主表实体的对象引用
			就是 private User user;
			生成get，set方法
		2.定义封装account和user的 resultmap
			<resultMap id="accountUserMap" type="account">
				<id property="id"  column="aid"></id>
				<result property="uid"  column="uid"></result>
				<result property="money"  column="money"></result>
				<!----!>
				<association property="user" column="uid">
                	<id property="id" column="id"><id>
                	<result property="username"  column="username"></result>
                	<result property="address"  column="address"></result>
                	<result property="sex"  column="sex"></result>
                	<result property="birthday"  column="birthday"></result>
                </association>
			</resultMap>
			
			
			
		也可以反过来操作
```

## 2.9延迟加载

```java
问题
	在查询用户时候，是么时候用，什么时候查询
	查询账户时候，账户所属的用户信息应该查出来
延迟加载
	查询用户，在真正使用数据时候才发起查询，也可以理解为懒加载，按需加载
立即加载
	不管用不用，只要一调用方法，马上发起来查询
	一对多，多对多 通常情况下都是延迟加载
				延迟加载全局开关在 主配置文件中
	多对一，一对一 通常都是立即加载

```

## 2.10缓存

```java
减少和数据库的交互次数，提高执行效率
	适用于缓存
		经常查询，并且不经常改变的
		数据的正确与否对最终的影响不大
	不适用于缓存
		经常改变的数据
		数据的正确与否对最终结果影响很大
		
	一级缓存
		值得是mybatis中sqlsession的缓存，查询的结果会存到SQL session中，结果是一个map
		再次查询同样的数据，mybatis回去sqlsession中查看是否有，直接拿出来用
		当sqlsession消失的时候，mybatis就消失了
		
		当修改的时候，就会清除一级缓存
		
	二级缓存
		值得是sqlsessionfactory对象的缓存，由同一个值得是sqlsessionfactory对象创建的sqlsession共享他的缓存
		opensession();
		二级缓存步骤
			让mybatis框架支持二级缓存   主配置文件  默认true
			让当前文件映射文件支持二级缓存 写一个cache标签
			让当前的操作支持二级缓存 查询用户的时候 加一个属性 操作usercache = "true";
			注意 二级缓存中存放的是数据 
```

## 2.11注解开发

```java
配置

		<!--配置别名-->
            <typeAliases>
                <package name="com.it.domain"/>
            </typeAliases>
		
		<mappers>
            <!--<mapper class="com.it.dao.IUserdao"/>-->
            <package name="com.it.dao"/>
        </mappers>
   		 
   		  @Select("select * from user");
    			List<User> findAll();
    			
    	 session.commit();删除操作需要提交
    	 注解来设置一对多
    	 @results()
    	 
    	 一对一
    	 		    @Select("select * from user")
                    @Results(id="userMap")
                    List<User> findAll();
                    //保存用户
                //    @Delete("delete from user where id=#{id} ")
                //    void deleteinfo(Integer userid);

                    @Select("select * from user where id =#{id} ")
                    @ResultMap(value = {"userMap"})
                    User findById(Integer id);
    	 	
    	 
    	 
    	 
    	 	    @Select("select * from account")
                @Results(id="accountMap",value = {
                        @Result(id = true,column = "id",property = "id"),
                        @Result(column = "money",property = "money"),
                        @Result(property = "user",column = "id",
                        one=@One(select = "com.it.dao.IUserdao.findById",
                                fetchType = FetchType.EAGER))
                })
                
       注意事项：         
               1. one=@One(select = "com.it.dao.IUserdao.findById",
                                fetchType = FetchType.EAGER) 是一对一的注解方式
                                一对多用many
               2.fenchtype用来配置  延迟加载还是懒加载
               3.一级缓存，mtbatis自动使用，不在主配置文件中配置，二级缓存也是默认开启的，在映射接口的上面写上@cacheNameSpace(blocking=true)	开启二级缓存
               4.@Results需要配合@Select一起使用
               5.已经定义的Result可以通过resultMap直接使用，两者通过id匹配
               6.子查询可以直接使用父查询的参数
               	
```

# 3.Spring

```java
1.spring框架的概述以及spring继续xml的ioc配置
2.spring中基于注解的ioc和ioc的案例
3.spring中的AOP和基于xml的Aop配置
4.spring中的jdbcTemplate和事务控制
下载地址：https://repo.spring.io/libs-release-local/

Spring是分层的javaSE/EE应用的轻量级的开源框架以AOP(面向切面编程)和IOC(控制反转)为核心
提供了展现层  SPringMVC 和Spring JDBC以及事务管理的技术

优势
	1.方便解耦，简化开发
	2.AOP编程的支持
	3.声明式的支持
	4.方便程序的测试
	5.方便集成各种优秀的框架
	6.降低javaEE api的使用难度
	
体系结构
	耦合：
		程序之间的依赖关系，
		方法之间的依赖
		类之间的依赖
	解耦：降低程序之间的依赖关系
	实际开发中：编译器不依赖，运行期依赖
		思路：
		1.使用反射来创建对象，而且避免new关键字
		2.通过读取配置文件来读取类名
		
		
		xml配置文件
			<?xml version="1.0" encoding="UTF-8"?>
            <beans xmlns="http://www.springframework.org/schema/beans"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                   xsi:schemaLocation="http://www.springframework.org/schema/beans
                            http://www.springframework.org/schema/beans/spring-beans.xsd">
                <!--把对象的创建交给spring来管理-->
                <bean id="accountService" class="com.it.service.imp1.AccountServiceImp"></bean>
                <bean id="accountDao" class="com.it.dao.impl.AccountDaoImpl"></bean>
            </beans>
            
            
          main函数调用
		 ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");
        /*根据id获取bean对象*/
        IAccountService as = (IAccountService)ac.getBean("accountService");
        IAccountDao adao = ac.getBean("accountDao",IAccountDao.class);
```

## 3.1 IOC

```java
控制反转
	把对象创建的权利交给框架或者工厂，并非面向对象编程的专业术语，它包括依赖注入和依赖查找
	作用
		降低他们之间的依赖关系
		
		
	表现层--->调业务层-->调持久层
	
	spring IOC核心容器
			ApplicationContext的三个常用是实现类
				ClassPathXmlApplicationContext 可以加载类路径下的配置文件
				FileSyetemXmlApplicationContext	可以加载磁盘任意路径下的配置文件
				AnnotationConfigApplicationContext 用于读取注解创建容器
				
	核心容器的两个接口
		ApplicationContext 采用立即加载的方式，只要读取完毕，马上创建配置对象
		Beanfactory		创建对象采取的策略是延迟加载的什么时候获取id，什么时候创建再使用
		
	bean细节三种创建对象
		1.默认构造函数
			<bean id="accountDao" class="com.it.dao.impl.AccountDaoImpl"></bean>
		2.使用普通工厂中的方法创建对象，并且存入spring容器
			factory-bean   factory-method="方法"
		3.使用静态方法创建对象并且存入spring容器
		<bean id="accountDao" class="com.it.dao.impl.AccountDaoImpl
		 factory-method="方法""></bean>
	
	作用范围
		scope属性用于指定作用范围
			singleton    单例   立马创建
			prototype	多例	使用对象时候创建   java辣鸡回收
			request		作用于web应用的请求范围
			session		作用域web应用的会话范围
			global-session		作于集群环境的会话范围，不是集群环境，就是session
								负载均衡，
		
```

## 3.2注入

```java
依赖关系的管理，交给spring来维护，就称为依赖注入
	有三类
		基本类型和String
		其他bean类型，在Spring容器中有的类
		复杂类型/集合
			<property name="shuxing">
				<array>
					<value>AAA<value>
					<value>AAdasdA<value>
					<value>AdasdaAA<value>
				<array>
			</property>
			<property name="shuxing">
				<map>
					<entry key=“”>
						<value>AAA<value>
					<entry>
					
				<map>
			</property>
	注入的方法有三种
		1.使用构造函数提供
			<constructor-arg
            type="java.lang.String"
            index=""  参数索引
            name=""		参数名字
            ref=""		引入外部的值，bean对象
            value=""   基本类型和string>
            </constructor-arg>
            优势 获取bean对象时候，注入式必须的操作
            弊端 改变了bean实例化的方式，用不到这些数据也必须提供
		2.使用set方法
			 <property name="" value="" ref=""></property>
			 name = 指定注入的所调用deset方法名称
			 常用
			 优势：创建对象没有明确的限制，直接可以使用默认构造函数
			 弊端：如果某个成员必须有值，则获取对象又可能set方法没有执行
		3.使用注解
			用于创建对象的注解
				@component 把当前对象存入spring容器中，不写默认id为当前类名，首字母小写
				aop jar包，注解扫描配置 ：context
				<context :component-scan base-package="com.it">
				@controller 表现层
				@service	业务层 
				@responsity	 持久层			
			用于注入数据的注解
				Autowired:自动按照类型注入，只要和容器中匹配，那就匹配
				类型匹配到变量匹配
				Qualifier  按照类型的基础上，在按照名称注入，再给类成员注入不能单独使用，和上面的组合，				
				Resoure  name用于指定bean的id，上面三个只能注入基本类型和String类型
				Value 用于注入基本类型和String类型的数据
						value用于指定数据的值，可以使用spring中的 el表达式  ${value}
			用于改变作用范围的
				Scope 指定bean的作用范围
			和生命周期相关 的
				preDestory  销毁方法
				postconstruct  用于指定初始化方法 
				
				
				Configration  指定当前类是一个配置类
			带有 @Configuration 的注解类表示这个类可以使用 Spring IoC 容器作为 bean 定义的来源
				
				Componentscan 用于通过注解指定spring在创建容器时候要扫描的包
				
				bean注解
				@Bean 注解告诉 Spring，一个带有 @Bean 的注解方法将返回一个对象，该对象应该被注册为在 Spring 应用程序上下文中的 bean。
				
				import注解

```

## 3.3AOP'

```java
面向切面编程
	将重复的代码提取出来，在需要执行的时候，利用动态代理技术，再不修改源码的基础上，对方法进行增强
	优势
		减少重复代码
		提高开发效率
		维护方便
	使用动态代理的技术，通过配置的方式
	
	连接点
		那些被拦截到的点，这些点指的是方法
	切入点
		指的是那些被增强的方法
	通知
		拦截到之后要干的事情
        	通知的类型 
        	前置通知 后置通知 异常通知 最终通知 环绕通知：整个
    引介
    target
    	代理的目标对象
    waving
    	增强应用到目标对象来创建新的对象的过程
    Proxy
    		一个类被aop织入增强后，就产生一个结果代理类
    aspect
    	切面 切入点和通知，引介的结合
    	
    	
    	开发阶段
    		编写核心业务代码：熟悉业务需求
    		公共代码抽取出来形成通知
    		配置文件中，声明切入点和通知间的关系
    	运行阶段
    		框架监控切入点方法的执行，使用代理机制，
```

### 3.3.1初步配置

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
	http://www.springframework.org/schema/beans/spring-beans.xsd
	http://www.springframework.org/schema/context
	http://www.springframework.org/schema/context/spring-context.xsd
	http://www.springframework.org/schema/aop
	http://www.springframework.org/schema/aop/spring-aop.xsd
	http://www.springframework.org/schema/tx
	http://www.springframework.org/schema/tx/spring-tx.xsd">
	
	最全约束



<!--aop配置
        1.把通知bean交给spring来管理
        2.配置aop
        3.配置切面
            id 给切面提供一个唯一标识
            ref 通知类bean的id
        4.aspect内部使用对应的标签配置通知类型
            现在是让logger方法在切入点之前执行，前置通知
            aop；before 前置通知
                    method属性用于执行logger内中的方法
                    pointcut 指定对那些方法进行增强
                        execution(表达式)
                            访问修饰符 返回值 包名 方法（参数列）
                            execution(public void com.it.service.impl.IAccountServiceimpl.saveAccount())
    -->
    <!--配置logger-->
    <bean id="logger" class="com.it.uitls.Logger"></bean>
    <!--配置aop-->
    <aop:config>
        <aop:aspect id="logAdvice" ref="logger">
            <aop:before method="printLog" pointcut="execution(public void com.it.service.impl.IAccountServiceimpl.saveAccount())"></aop:before>
        </aop:aspect>
    </aop:config>
```

### 3.3.2切入点表达式

```java
全通配符
	访问修饰父可以省略 返回值可以使用通配符 包名可以使用通配符，几个包几个※
	包名可以使用 ..表示当前包和子包 类名和方法名都可以使用统配
	参数列表可以直接写数据类型，通配符表示任意类型
	..表示任意类型，有无参数
	* *..*.*
	
	实际开发
		切到业务层是实现类下面的所有方法
		* com.it.service.impl.*.*(..)
		
	四种通知方法
		 <aop:before method="printLog" pointcut="execution(* com.it.service.impl.*.*(..)))"></aop:before>
            <aop:after method="afterLog" pointcut="execution(* com.it.service.impl.*.*(..)))"></aop:after>
            <aop:after-returning method="lastLog" pointcut="execution(* com.it.service.impl.*.*(..)))"></aop:after-returning>
            <aop:after-throwing method="excepLog" pointcut="execution(* com.it.service.impl.*.*(..)))"></aop:after-throwing>
            
            简化标签
            写在外面所有类可用
   <aop:pointcut id="pt" expression="execution(* com.it.service.impl.*.*(..)))"/>
               <aop:before method="printLog" pointcut-ref="pt"></aop:before>


	
```

### 3.3.3环绕通知

```java
   
   环绕通知
	当配置了环绕通知，切入点方法没有执行，通知方法执行了
	ProceedJoinPonit接口，接口方法 proceed(),可以明确调用切入点方法
	环绕通知可以控制什么时候执行
	
   public Object aroundPrint(ProceedingJoinPoint pjp){
        Object rtvalue = null;
        try {
            Object[] args = pjp.getArgs();
            System.out.println("前置通知执行....");
            System.out.println("环绕通知执行....");
            rtvalue = pjp.proceed(args);
            System.out.println("后置通知执行....");
            return rtvalue;
        } catch (Throwable throwable) {
            System.out.println("异常通知执行....");
            throwable.printStackTrace();
        }finally {
            System.out.println("最终通知执行....");
        }
        return rtvalue;
    }

```

### 3.3.4注解aop

```java
<!--配置spring容器要扫描的包-->
    <context:component-scan base-package="com.it"></context:component-scan>
    
        <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
        
     @Component("logger")
	@Aspect
	@Before("execution(* com.it.service.impl.*.*(..))")

	全局声明
		 @Pointcut("execution(* com.it.service.impl.*.*(..))")
    		private void pt1(){}
```

## 3.4JDBCtemp事务

```java
设置数据源
	DriverManageDateSource ds = new DriverManageDateSource();
	ds.setDriverClassName("com.mysql.jdbc.Driver");
	ds.setUrl("jdbc:mysql://localhost:3306/数据库名")
	ds.setUsername("root")
	ds.setPassword("root")
	
	创建jdbctemplate对象
	JdbcTEmplate jt = new JdbcTEmplate();
	jt.setDateSouce(ds);
	jt.execute("sql语句")
	
	原始的jdbc
	
	结合spring配置
	配置 在 bean.xml
	<bean id="jdbcTemplate" class="org.springframe.jdbc.core.Jdbctemplate">
		<property name="dataSource" ref="dataSource"><property>
	</bean>
	<bean id="datasource" class="rg.springframe.jdbc.datasource.DriverManagerDatesource">
		 <property name="driverClassName" value="com.mysql.jdbc.Driver"><property>
		 <property name="url" value=""><property>
		 <property name="username" value=""><property>
		 <property name="password" value=""><property>
	</bean>
	
	
	主执行函数
		Application ac = new ClasspathXmlApplicationContext("bean.xml")
		JdbcTemplate jt = ac.getbean("jdcetemplate",JdbcTemplate.class)
		jt.execute("sql")
```

## 3.5事务控制

```java
在aop
<aop:aspect>里面	
	前置	开启事务 
	后置	提交事务
    异常	回滚事务
    最终	释放连接
    
 上述 xml版本
 spring自己封装的事务控制
 txjar包
 xml中声明式事务控制
 	1.配置事务管理器
 	<bean id="tansction" class="org.framework.jdbc.datasource.DateSourceTranscationManager">
 	<property name="datasource" ref="datasource">
 	2.配置事务的通知
 	<tx:advice transaction-manager ="transactionmanager" id="txadvice">
 	3.配置通用切入点表达式aop
 		pt1
 	4.建立事务通知和切入点的关系
 		<aop:advise ref=“txadvice” point-cut="pt1">
 	5.配置事务的属性
 		在tx:advice内
 		<tx:attribute name="*"  除了查询
        isolation="事务隔离级别"
        no-rollvack-for="指定一个异常，产生异常事务回滚，产生其他异常不会滚" 默认值都回滚
        propagation="事务传播"
        read-only="事务是否只读"
        rollback-for="指定一个异常，产生异常事务不回滚，其他事务不会滚" 默认值回滚
        timeout="事务超时时间" 默认值永不超市>
        
        
     注解事务控制
     	
```

# 4.springmvc

```java
表现层  		业务层 			持久层 
springmvc		spring			mybatis

MVC模型	
	model 模型  		javabean
	view视图  		jsp
	controller 控制器  servlet
	
	请求驱动的轻量级web层框架，通过一套注解，成为一个简单的类成为请求的控制器，不需要实现接口，同时还支持restful编程风格
	核心控制器 servlet     			 	struts2 核心的  filter
	基于方法设计 							基于类设计
	JSTL效率高,简洁,jsr303 ajax方便		 OGNL表达式
```

## 4.1开始配置

```java
    //锁定版本
    1.配置pom.xml
    <spring.version>5.0.2.RELEASE</spring.version>
    
    <dependencies>
        <dependency>
          <groupId>junit</groupId>
          <artifactId>junit</artifactId>
          <version>4.11</version>
          <scope>test</scope>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-web</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>servlet-api</artifactId>
          <version>2.5</version>
          <scope>provided</scope>
        </dependency>
        <dependency>
          <groupId>javax.servlet.jsp</groupId>
          <artifactId>jsp-api</artifactId>
          <version>2.0</version>
          <scope>provided</scope>
        </dependency>
  </dependencies>
  
  
  	2.配置web.xml
  	<!--配置控制器-->
  <!--配置控制器-->
  <servlet>
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <!--初始化-->
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:SpringMVC.xml</param-value>
    </init-param>
    <!--启动服务器创建-->
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
  
  	3.配置springmvc.xml
  		<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd
    http://www.springframework.org/schema/mvc
    http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!--开启注解扫描-->
    <context:component-scan base-package="com.it"/>

    <!--视图解析器-->
    <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/pages/"></property>
        <property name="suffix" value=".jsp"></property>
    </bean>

    <!--开启mvc框架注解支持-->自动加载处理器映射器  处理器适配器
    <mvc:annotation-driven></mvc:annotation-driven>
</beans>
	
	4.写控制器

                //控制器
        @Controller
        public class HelloController {
            @RequestMapping(path = "/hello")
            public String sayHello(){
                System.out.println("HelloMVC");
                return "success";
            }
        }
  	5.跳转
  		<a href="hello">入门程序跳转</a>
  	6.配置tomacat服务器
  		记得把路径加到 deployment
```

## 4.2处理流程

```java
1.request
2.前端控制器  DispatcherServlet
3.处理器映射器  HaddlerMapping,返回一个执行链到前端控制器，返回执行方法
4.处理器适配器  HandlerAdapter 去执行 
5.执行  执行方法
6.返回一个Modelview到处理器适配器 到 前端控制器
7.视图解析器 返回view到前端控制器
8.前端控制器 找视图

```

## 4.3RequestMapping

```java
放在类上和方法上
	分模块处理  user/    类上面写代表一个模块
		下面 写  /submit    /login    方法上面写注解 requestmapping
		
	属性	path    和  value  都可以映射成功   value可以省略
		method={RequestMethod.POst}  枚举类  只能是 post请求
        params 指定请求参数限制条件 
        params={"username"}  必须有属性
        headers:用于指定限制请求头  headers = {"Accept"}  包含这个头
```

## 4.4请求参数的绑定

```java
public String sayHello(String username){
        System.out.println("HelloMVC");
        System.out.println(username);
        return "success";
    }
    
    接受请求参数
    封装bean
     public String sayHello(Account account){
        System.out.println("HelloMVC");
        System.out.println(account);
        return "success";
    }
    
    封装多层对象
    	<a href="hello?username=hehe&user.uname=ceshilei&user.uword=111">入门程序跳转</a>
    	private User user;
    	user类实现tostring方法 和setget方法
    	
    	
    	post请求中文乱码
    		过滤器拦截设置乱码
    		  <!--配置过滤器-->
              <filter>
                <filter-name>characterEncodingFilter</filter-name>
                <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
                <!--初始化拦截配置-->
                <init-param>
                  <param-name>encoding</param-name>
                  <param-value>UTF-8</param-value>
                </init-param>
              </filter>
              <filter-mapping>
                <filter-name>characterEncodingFilter</filter-name>
                <url-pattern>/*</url-pattern>
              </filter-mapping>
              
              
          集合对象处理
          前端
          	<form action="hello" method="post">
                姓名<input type="text" name="username"><br>
                密码<input type="text" name="password"><br>
                用户姓名<input type="text" name="list[0].uname"><br>
                用户密码<input type="text" name="list[0].uword"><br>
                用户2姓名<input type="text" name="map[0].uname"><br>
                用户2密码<input type="text" name="map[0].uword"><br>
                <input type="submit"><br>
            </form>
           后端
           	    private List<User> list;
   				 private Map<String,User> map;
   				 生成getset方法 tostring方法
   				 
   			打印
   				 	public String sayHello(Account account){
                        System.out.println("HelloMVC");
                        System.out.println(account);
                        return "success";
                    }
```

## 4.5自定义类型转化器

```java
mvc框架内部自动进行 数据转化 所以  String->>Interger

例如 日期  2002/11/11可以自动转化为日期
			2002-11-11 不能自动转化
1.定义一个类，实现converter接口，该接口有两个泛型 第一个泛型写你要转的类，第二个泛型写要转化到的类
	public class StringToDate implements Converter<String, Date> {
    @Override
    /*s指的是传进来的代码*/
    public Date convert(String s) {
        if(s == null){
            throw new RuntimeException("请你传入参数");
        }
        DateFormat df = new SimpleDateFormat("yyyy-MM-dd");
        try {
            return df.parse(s);
        } catch (Exception e) {
            throw new RuntimeException("数据类型转化出错");
        }
    }
}
2.配置自定义类型转化器
	<!--开启mvc框架注解支持-->
    <mvc:annotation-driven conversion-service="conversionService"></mvc:annotation-driven>

    <!--配置自定义转化器-->
    <bean id="conversionService" class="org.springframework.context.support.ConversionServiceFactoryBean">
        <property name="converters">
            <set>
                <bean class="com.it.utils.StringToDate"></bean>
            </set>
        </property>
    </bean>
```

## 4.6在控制器中拿到servlet Api

```java
直接在请求的方法里面加  HttpServletRequest req, HttpServletReSponse res
		HttpSession session = req.getsession();
		session.getServletContext(); 获取域对象
```

## 4.7常用注解

```java
RequestParam
		把请求中指定名称的参数给控制器中的形参赋值  用来指定名称对不上时候来赋值
		比如  请求 key为  name  接受为 username
		在请求控制器的参数 前面 写 @RequestParam(name="name") String username
RequsetBody
		用于获取请求体的内容，get请求方式不适用，get没有请求体，后面处理json有用
		在请求控制器的参数 前面 写 (@RequestBody String body)
PathVarible
		用于绑定url中的占位符  /delete/{id}  支持restful 风格
			restful风格好处
					请求地址一样，根据请求方式执行不同的函数  /user
					请求方式和地址一样  /user/10   /user/{id}
					很容易缓存
					
			@PathVarible String body
HiddenHttpMethodFilter
		过滤器  也是 restful风格的
RequestHeader
		用于获取请求消息的值 (@RequestHeader(value="Accept") String body)
CookieValue
		获取cookie的值(value="SessionId" String cookievalue)
ModelAttribute
		出现在方法上面，表示当前方法会在控制器的方法执行之前执行它
		出现在参数上面，获取指定的数据给参数赋值
		带返回值
			控制器执行方法会拿到你方法的返回值
		不带返回值
			参数传Map<String,User> map
			数据存到map集合当中，
			在控制器方法参数中加 @ModelAttribute("abc")
		应用场景
			提交表单有三个值，但是你只提交两个值，我们为剩下一个值赋值
SessionAttributes
		作用在类上面
		@SessionAttributes(value="msg")
		public class method{
            
		}
		多次执行控制器方法之间的参数共享
		public String aabb(Model model){
            model.setAttribute("msg","meimei");
            存到了  requset域对象
		}
		获取  model.get("msg")
		删除
		public String del(SessionStatus status){
            status.setComplete()
		}
```

## 4.8创建项目

```java
archetypeCatalog=internal  加上不然是一个空项目
```

## 4.9相应数据

```java
public String testString(Model model){
        User user = new User();
        user.setUsername("妹妹");
        user.setAge(18);
        user.setPassword("123");
        model.addAttribute("user",user);
        System.out.println("执行了");
        return "success";
    }
    
   //请求转发
        request.getRequestDispather("/WEB-INfo/pages/success.jsp请求路劲").forward(request.response)
   //没有返回值  默认值请求路径 url.jsp
   
返回值是MODelANDView对象
	对象调整具体的jsp视图
		 ModelAndView mv = new ModelAndView();
        //添加数据
        mv.addObject("user",user);
        //设置跳转的页面
        mv.setViewName("success");
    //请求转发，不使用视图解析器
    	return "forward:/WEB-INF/pages/success.jsp"
    	重定向//不适用视图解析器
    	return "redirect:/index.jsp"
```

## 4.10响应 JSON数据

```java
ResponseBody响应数据
	1.搭建异步
	2.静态资源不拦截
		 <!--告诉不拦截静态资源-->
    <mvc:default-servlet-handler/>
    3.发送请求
    	$.ajax({
                url: 'user/test',
                contentType: 'application/json;charset=UTF-8',
                data: '{"username":"张三","password":"123456","age":30}',
                dataType: 'json',
                type: 'post',
                success:(data)=>{
                    alert(data);
                }
            })
     3.导入jackson 坐标
                    <dependency>
                  <groupId>com.fasterxml.jackson.core</groupId>
                  <artifactId>jackson-core</artifactId>
                  <version>2.9.0</version>
                </dependency>
                <dependency>
                  <groupId>com.fasterxml.jackson.core</groupId>
                  <artifactId>jackson-annotations</artifactId>
                  <version>2.9.0</version>
                </dependency>
                <dependency>
                  <groupId>com.fasterxml.jackson.core</groupId>
                  <artifactId>jackson-databind</artifactId>
                  <version>2.9.0</version>
                </dependency>
     4.接受并且存入javabean
     		springmvc自动封装到集合里面
     		public void testString(@RequestBody User user){
             
                System.out.println("ajax执行了");
                System.out.println(user);
            }
     5.响应数据
              public @ResponseBody User testString(@RequestBody User user){
                //响应数据
                System.out.println("ajax执行了");
                user.setUsername("hahha");
                user.setAge(40);
                return user;
            }
```

## 4.11文件上传

```java
第三方组件  jar包
	1.导入jar包
		commons-fileupload
		commons-io
	2.<input type="file" name="upload"><br>
		注意名称必须和方法参数相同
	3.配置文件解析器
	4.具体流程
		 public String testString(HttpServletRequest request, MultipartFile upload) throws IOException {
        System.out.println("开始上传");
        /*配置上传路径*/
        String path = request.getSession().getServletContext().getRealPath("/upload/");
        //判断路径是否存在
        File file = new File(path);
        if (!file.exists()){
            file.mkdirs();
        }
        //说明上传文件项
        String filename = upload.getOriginalFilename();
        String uuid = UUID.randomUUID().toString().replace("-","");
        filename = uuid + "_" +filename;
        //完成
        upload.transferTo(new File(path,filename));
		return "success"
    }
    5.上传成功
    	D:\server\apache-tomcat-8.5.53\webapps\ROOT\upload
```

## 4.12跨服务器上传

```java
1.应用服务器  负责部署应用
2.数据库服务器 运行数据库
3.缓存和消息服务器 负责处理大并发访问的缓存和消息
4.文件服务器 负责存储用户上传文件的服务器

	流程	
			1.jar包  sun公司
					com.sun.jersey
					jersey-core
					1.18.1
					com.sun.jersy
					jersey-client
					1.18.1
			2.准备一个图片服务器
				端口设置 uploads文件夹
			3.
			System.out.println("开始上传");
        /*定义服务器上传路径*/
      	String path = "http://localhost:9090/uploads"
        //说明上传文件项
        String filename = upload.getOriginalFilename();
        String uuid = UUID.randomUUID().toString().replace("-","");
        filename = uuid + "_" +filename;
        //完成
       // 1.创建客户端对象
        Client cl = Client.create();
        //2.连接图片服务器
        WebReSourec webresource = cl.resource(path+filename );
        webresource.put(upload.getBytes())
        return "success";
    }
```

## 4.13异常处理

```java
MVC处理异常  
		浏览器--->前端控制器--->web --> service --> dao
		后面有异常 往上抛
		
		异常组件处理器 导入jar包
		2.编写自定义异常类
              public class EXP extends Exception {
                    //存储提示信息
                    private String message;

                    public EXP(String message) {
                        this.message = message;
                    }

                    @Override
                    public String getMessage() {
                        return message;
                    }

                    public void setMessage(String message) {
                        this.message = message;
                    }
                }
                    try {
                    int a =10 / 0;
                } catch (Exception e) {
                    //向上抛出自定义异常
                    e.printStackTrace();
                    throw new EXP("查询用户异常");
                }
		2.编写异常处理器
			public class excepresolve implements HandlerExceptionResolver {

    @Override
            public ModelAndView resolveException(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) {
               //获取异常对象
                EXP ee = null;
                if(ee instanceof EXP){
                    ee = (EXP)e;
                }else {
                    ee = new EXP("系统正在维护");
                }
                //ModelAndView对象
                ModelAndView mv = new ModelAndView();
                mv.addObject("errormsg",e.getMessage());
                mv.setViewName("error");
                return null;
            }
        }
		3.配置异常处理器
			<bean id="exp" class="com.it.exception.EXP">
    		</bean>
		
		
```

## 4.14拦截器

```java
类似于之前过滤器
		对处理器进行预处理和后处理
		1.编写拦截器类  实现HandlerIntercepter接口
			导入方法
				prehandle
		2.配置拦截器
		<mvc:interceptors>
			<mvc:interceptor>
				你要拦截的方法//
				<mvc:mapping path=“/”>
				//不要拦截的方法
				<mvc:exclude-mapping path="">
				//配置拦截器对象
				<bean class="">
```

# 5.SSM框架整合

```java
配置文件  加注解的方式
		坐标
			  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
    <!--springMvc-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>servlet-api</artifactId>
      <version>2.5</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.0</version>
      <scope>provided</scope>
    </dependency>
    <!--mybatis-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.4.5</version>
    </dependency>
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>1.3.0</version>
    </dependency>
    <dependency>
      <groupId>c3p0</groupId>
      <artifactId>c3p0</artifactId>
      <version>0.9.1.2</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.6</version>
    </dependency>
    <dependency>
      <groupId>log4j</groupId>
      <artifactId>log4j</artifactId>
      <version>1.2.12</version>
    </dependency>
    <!--spring-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>servlet-api</artifactId>
      <version>2.5</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.0</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>jstl</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
      <scope>provided</scope>
    </dependency>
  </dependencies>

```

## 5.1.搭建spring

```java
1.xml
	<?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:context="http://www.springframework.org/schema/context"
           xmlns:aop="http://www.springframework.org/schema/aop"
           xmlns:tx="http://www.springframework.org/schema/tx"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd">
        <!--开启注解扫描  只希望处理 dao和service-->
        <context:component-scan base-package="com.it">
            <!--配置那些注解不扫描-->
            <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
        </context:component-scan>


    </beans>
    
    
    
    测试
    	 public static void main(String[] args) {
            //加载spring得配置文件
            ApplicationContext ac = new
                    ClassPathXmlApplicationContext
                    ("classpath:applicationContext.xml");
            /*获取对象*/
            AccountService as = (AccountService) ac.getBean("accountService");
            //调用方法
            as.findAll();
        }
```

## 5.2springmvc整合

```java
web.xml
	<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

    <web-app>
      <display-name>Archetype Created Web Application</display-name>
      <!--前端控制器-->
      <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--加载springmvc.xml-->
        <init-param>
          <param-name>contextConfigLocation</param-name>
          <param-value>classpath:springmvc.xml</param-value>
        </init-param>
        <!--启动服务器创建参数-->
        <load-on-startup>1</load-on-startup>
      </servlet>
      <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
      </servlet-mapping>
      <!--解决中文乱码过滤器-->
      <filter>
        <filter-name>characterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
          <param-name>encoding</param-name>
          <param-value>UTF-8</param-value>
        </init-param>  
      </filter>
      <filter-mapping>
        <filter-name>characterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
      </filter-mapping>
    </web-app>


springmvc.xml
            <?xml version="1.0" encoding="UTF-8"?>
        <beans xmlns="http://www.springframework.org/schema/beans"
               xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
               xmlns:context="http://www.springframework.org/schema/context"
               xmlns:mvc="http://www.springframework.org/schema/mvc"
               xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd
            http://www.springframework.org/schema/mvc
            http://www.springframework.org/schema/mvc/spring-mvc.xsd">
            <!--开启注解扫描-->
            <context:component-scan base-package="com.it">
                <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
            </context:component-scan>
            <!--视图解析器-->
            <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
                <property name="prefix" value="/WEB-INF/pages/"></property>
                <property name="suffix" value=".jsp"></property>
            </bean>
            <!--不过滤静态资源-->
            <mvc:default-servlet-handler/>
            <!--开启springMvc注解支持-->
            <mvc:annotation-driven></mvc:annotation-driven>
        </beans>
```

## 5.3spring整合springmvc方法

```java
启动服务器  加载spring得配置文件  然后依赖注入

ServletContext对象 在服务器启动得时候创建 ，服务器关闭才销毁
		监听器 可以监听域对象得创建和销毁
				监听器去加载spring得配置文件
				创建web工厂，存储ServletContext对象
				
				
	在 webapp
		 <!--配置spring 得监听器-->
          <!--默认只加载web-inf目录下面得 spring.xml 配置文件-->
          <listener>
            <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
          </listener>
          <!--设置配置文件路径-->
          <context-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:applicationContext.xml</param-value>
          </context-param>
          
      在控制器
      		@Controller
                    @RequestMapping("/account")
                    public class AccountController {
                        @Autowired
                        private AccountService accountService;
                        @RequestMapping("testFindAll")
                        public String findAll(){
                            System.out.println("表现层查询所有账户信息");
                            accountService.findAll();
                            return "list";
                        }
                    }
```

## 5.4 spring整合mybatis框架

```java
代理对象
	<!--spring去整合mybatis框架-->
    <!--配置连接池c3p0-->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="com.mysql.jdbc.Driver"></property>
        <property name="jdbcUrl" value="jdbc:mysql:///ssm?useUnicode=true&amp;characterEncoding=UTF-8"></property>
        <property name="user" value="root"></property>
        <property name="password" value="root"></property>
    </bean>
    <!--配置sqlsessionfactory-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <!--配置接口所在的包-->
    <bean id="mapperScannerConfigurer" class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.it.dao"></property>
    </bean>


写道  spring.xml里面  不要 sqlmap.xml


保存  提交事务 
		<!--声明事务管理-->
            <!--配置事务管理器-->
            <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
                <property name="dataSource" ref="dataSource"></property>
            </bean>
            <!--配置事务通知-->
            <tx:advice id="txadvice" transaction-manager="transactionManager">
                <tx:attributes>
                    <tx:method name="find*" read-only="true"/>
                    <tx:method name="*" isolation="DEFAULT"></tx:method>
                </tx:attributes>
            </tx:advice>
            <!--配置aop增强-->
            <aop:config>
                <aop:advisor advice-ref="txadvice" pointcut="execution(* com.it.service.impl.*AccountServiceImpl.*(..))"></aop:advisor>
            </aop:config>
```

## 5.5 restful风格

```java
 <!--rest风格uri 将post请求转化-->
  <filter>
    <filter-name>HiddenHttpMethodFilter</filter-name>
    <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
  </filter>
  <filter-mapping>
    <filter-name>HiddenHttpMethodFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
```

## 5.6逆向工程

根据数据库生成bean以及对应的mapper

​		引入 

```java
<!-- https://mvnrepository.com/artifact/org.mybatis.generator/mybatis-generator-core -->
<dependency>
  <groupId>org.mybatis.generator</groupId>
  <artifactId>mybatis-generator-core</artifactId>
  <version>1.3.5</version>
</dependency>



逆向工程测试文件
	List<String> warnings = new ArrayList<String>();
        boolean overwrite = true;
        File configFile = new File("mbg.xml");
        ConfigurationParser cp = new ConfigurationParser(warnings);
        Configuration config = cp.parseConfiguration(configFile);
        DefaultShellCallback callback = new DefaultShellCallback(overwrite);
        MyBatisGenerator myBatisGenerator = new MyBatisGenerator(config, callback, warnings);
        myBatisGenerator.generate(null);
        
        
        
   pom.xml配置
   		<plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.2</version>
                <configuration>
                    <verbose>true</verbose>
                    <overwrite>true</overwrite>
                </configuration>
            </plugin>

```

# 6.springboot

```
微服务  一组小型服务，可以通过http方式沟通

把功能元素放到一个服务器中/

<version>4.13</version>
RUNWith爆红解决
```

## 6.1快速创建

### 6.1.导入包

```java
<!--导入springboot-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.9.RELEASE</version>
    </parent>
    //父项目 真正的管理spring boot里面所有的依赖
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
    //这个依赖 帮我们导入web模块正常需要运行需要的场景模块
    springboot将所有的功能场景都抽取出来 ，成为starter 只需要在项目中引入就可以将所有的依赖导入进来
```

### 6.2编写主方法

```java
@SpringBootApplication
public class helloworld {
    public static void main(String[] args) {
        /*让springboot启动起来*/
        SpringApplication.run(helloworld.class,args);
    }
}
```

### 6.3Controller

```java
@Controller
public class HelloController {
    @ResponseBody
    @RequestMapping("hello")
    public String hello(){
        return "Hello World!";
    }
}
```

### 6.4部署

```java
导入maven 插件
	<build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
    
    
    之后使用 java -jar spring名字   部署完成
```

## 6.2快速创建

```java
/*restful风格*/
//@ResponseBody
//@Controller
/*合体*/
@RestController
public class hello {
    //@ResponseBody
    @RequestMapping("/helloquick")
    public String hello1(){
        return "hello world quick!!是谁";
    }
}
```

## 6.3springboot配置

```java
application.properties
application.yml

		修改springboot修改的默认值  18693943425
YAML配置全程
```

### 6.3.1YAML语法

```java
key: value:   表示一对键值对

例如  区分大小写
	server:
		port: 8081
		path: /hello
	值得写法
    	值得写法  
    		字面量   直接来写  字符串默认不用加上单引号双引号 
    				“”不会转义特殊字符
    				‘’会转义特殊字符
    		对象,MAP  键值对
    			friends:
    				lastName: zhangsan
    				age: 20
    			写在一行
    				friends: { lastname:zhangsan,age:18 }
    		数组 LIst Set
            	用 - 表示数组中得元素
            	pets:
            		-cat
            		-dog
            		-pig
            		行内元素
            		pets:[cat,dog,dog]
    将配置文件中的映射
    	导入配置依赖
    	<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
            <optional>true</optional>
        </dependency>
        
        person:
            lastName: zhangsan
            age: 18
            boss: false
            birth: 2017/12/12
            maps: {k1: 11,k2: 12}
            lists:
              - lisi
              - zhaoliu
            dog:
              name: 小狗
              age: 2
              
            @Component
			@ConfigurationProperties(prefix = "person")
			//只有spring容器组件中的才能容器提供的功能
			runwith爆红  加 version  2.13
```

### 6.3.2在properties配置

```java
person.age=18
person.birth=2018/19/12
person.boss=false
person.dog.name=dog
person.last-name=你是
person.lists=a,b,c
person.dog.age=15
person.maps.k1=13
person.maps.k5=15
```

### 6.3.3value注解

```java
单个注入
	@value('${person.lastName}')
	@value('#{11*2}')
	支持SPEL表达式
	
	
	相比前者支持jsr303数据校验  后者不支持校验
	@Validated放在类上面
		@Email放在成员变量上面  启动校验
```

### 6.3.4@propertySource和@ImportResource

```java
@propertySource(value = {'classpath:文件路劲'})   加载指定配置文件
@ImportResource(location = {'classpath:beans.xml'})
	导入spring的配置文件，让配置文件里面的内容生效
	例如导入 spring配置文件中的 bean生效 用这个注解


@ConfigerationProperties()  默认全局配置文件中获取

spring推荐的方式
		1.推荐使用 配置类  
				@Configuration 指定当前类是一个配置类，替代配置文件
					@Bean  //将方法的返回值添加到容器中 默认的id就是方法名字
                    public helloService hello(){
                        return new helloService();
                    }
```

### 6.3.5配置文件占位符

```java
随机数 和  获取之前的值
		person.age=${random.int}
        person.birth=2018/19/12
        person.boss=false
        person.dog.name=${person.last-name}_dog
        person.last-name=张三萨达撒${random.uuid}
        
        默认值
        	 person.dog.name=${person.last-name：的撒大}_dog
```

### 6.3.6profile和配置文件加载位置

```java
是对spring不同环境提供不同配置的文档，可以通过激活环境等方式来切换环境
	文件名可以是  
	application-dev.properties    开发环境
	application-prod.properties		生产环境
	
	默认使用 application.properties的配置
		在里面激活其他文件
			spring.profiles.active=dev
            
            
    yml
   		里面用文档块分开
   				spring:
   					profiles:
   						active: dev
   				---
   				spring:
   					profiles: dev
   				---
   				spring:
   					profiles: app
   					
   		打包的时候可以在后面  --spring.profiles.active=dev
   		
   		
   配置文件加载位置
   	file:./config
   	file:./
   	classpath:/config/
   	classpath:/
   		优先级从高到底
   		
   		互补配置
   		
   		还可以使用spring.config.location=G:/application.properties
   		也是互补配置
   		命令行也可以  使用命令指定配置文件
   		
   		
   	外部配置加载顺序
   		1.命令行参数
   		2.jar包外部的application-{profile}.properties
   		3.jar包内部的application-{profile}.properties
   		4.jar包外部的application.properties
   		5.jar包内部的application.properties
   		
   		启用debug=true  打印自动配置类报告
```

## 6.4springboot日志

```java
日志门面  JCL SLF4j   jboss 
日志实现	log4j   JUL   log4j2   logback

选用  
	SLF4j门面
	logback实现
	
	springboot默认选用  SLF4j门面 选择SLF4j 和  logback，底层spring选用JCL
	
	以后开发调用日志抽象层的方法，不调用是实现类
	
	
	统一使用  日志记录   都使用 SLF4j门面logback实现
		springboot在底层也是使用适配器转化为  SLF4j
		springboot能自动适配所有日志，而且底层使用SLF4J + logback得方式记录日志，引入其他框架得时候，只需要把这个以来的日志排除掉
		
		
		 //记录器
        Logger logger = LoggerFactory.getLogger(getClass());
        //日志得级别由低到高，日志只会打印以下得级别
        logger.trace("这是trace日志");
        logger.debug("这是debug日志");
        logger.info("输入info日志");
        //默认是info日志
        logger.warn("这是warn日志");
        logger.error("这是error日志,捕获异常");
        
        logging.level.com.it = trace修改在application.properties
        
        
        指定目录
        	logging.level.com.it = trace
            #指定生成目录
            #logging.file.path=
            #当前项目下生成springboot.log日志
            #也可以指定完整得路径
            logging.file.name=C:/Users/Administrator/Desktop/spring.log
            
            也可以修改日志输出格式
            
        指定配置
        	给类路劲下面放上每个日志框架的自己得配置文件即可，springboot就不使用默认配置
        	logback.xml
```

## 6.5 Springboot-web开发

```java
1.选中模块
2.在配置文件中配置少量配置
3.编写业务

########################自动配置原理
		xxxAutoConfigruation  帮我们容器中自动配置组件
		xxxproperties    封装配置文件得内容
			
```

### 6.5.1对静态资源得映射规则

```java
1.所有  /webjars/**  都去resources/webjars  找资源  
		以jar包得方式引入资源
		访问得时候写webjars资源名称
		
		例如
			http://localhost:8080/webjars/jquery/3.4.1/jquery.js
			<!--引入jquery坐标-->
                <dependency>
                    <groupId>org.webjars</groupId>
                    <artifactId>jquery</artifactId>
                    <version>3.4.1</version>
                </dependency>
                
             !访问当前项目得任何资源
             	“classpath:/META-INF/resources/”
             	“classpath:/resources/”
             	“classpath:/static/”
             	"classpath:/public/"
             	/   当前项目根路径
             	maven重新导入访问
             	
             欢迎页面静态资源文件下得  html页面
             		放到  public
             		ctrl + f5   删除文件重新下载 刷新
```

### 6.5.2 引入thymeleaf模板引擎

```java
解决不能使用 jsp得问题
		<!--引入模板引擎-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
        
        语法
        	默认前后缀
        		"classpath:/templates/"
        		".html"
        		
        操作 
        	1.导入名称空间
        		<html lang="en" xmlns:th="http://www.thymeleaf.org">
        	2.语法
        		1.th:text=""  						将 div里面得值设置
        		2.th:id || th:class   th:任意属性  	  来替换原生属性
        		3.th:insert ||  th:replace   		插入公共片段
        		4.th:each   		遍历
        		5.th:if     		条件判断
        		6.th:object  		设置变量
        		7.th:attr    		属性修改支持增加
        		8.th:fragment  		声明片段
        		9.th:remove   		移除
        	3.表达式
        		${}   
        				用来获取变量值 调用方法  
        				${#local,parma,session} 内置基本对象
                        内置一些工具对象
        		#{}	  	获取国际化内容
        		*{}		选择表达式  和${}共功能一样 新增 去除的${user}对象直接获取属性 #{name}
        		@{}		定义url得 @{/name(orderID)=${user.id}}
        		~{}		片段引用表达式
        		
        		没有操作   _  
        		[[${item}]]  行内取出元素
```

### 6.5.2扩展springmvc

```java
编写一个  配置类
 拦截器过时WebMvcConfigurerAdapter，换
 		1.@Configuration
            public class WebMvcConfg implements WebMvcConfigurer {
              //省略
            }
        2.@Configuration
            public class WebMvcConfg extends WebMvcConfigurationSupport {
            //省略
            }
		@Cinfiguration
		
		    @Override
            public void addResourceHandlers(ResourceHandlerRegistry registry) {
                registry.addResourceHandler("/**").addResourceLocations("classpath:/templates/");
            }
            @Override
            public void addViewControllers(ViewControllerRegistry registry) {
                //super.addViewControllers(registry);
                /*将这个请求映射到success*/
                registry.addViewController("/it").setViewName("success");
            }
            
            @enablewebmvc 全部自动配置  全面接管
```

## 6.6项目

```java
1.首页展示 
		两种方法 @requestmapping({'/','index.html'})
				还有一种
					内部类在配置类中间写 加上@bean 将组件注册在容器里面
					路劲用模板引擎替换
2.国际化
		新建三种国家化配置文件
		spring.messages.basename=il8n/login 
		spring.messages.basename=i18n.login管理
		去页面获取值
		点击改变就自己去写一个区域信息解析器
		LOcaleResolver  接口 实现  重写两个方法
3.登陆和拦截器
		th:action="@{/user/login}“
		设置控制器
				 @PostMapping(value = "/user/login")
                //@RequestMapping(value = "/user/login",method = RequestMethod.POST)
                public String login(@RequestParam("username") String username,
                                    @RequestParam("password") String password,
                                    Map<String,Object> map){
                    if (!StringUtils.isEmpty(username) && "123456".equals(password)){
                        return "dashboard";
                    }else {
                        map.put("message","用户名密码错误");
                        return "index.html";
                    }
                }
                
                #禁用缓存
				spring.thymeleaf.cache=false
				
				登陆错误消息显示
		拦截器登陆检查
		public class interceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        Object user = request.getSession().getAttribute("loginUser");
        if(user == null){
            request.setAttribute("msg","没有权限请先登录");
            request.getRequestDispatcher("/index.html").forward(request,response);
            return false;
        }else {
            return true;
        }
    }
    注册拦截器
    	registry.addInterceptor(new LOginhandlerInterceptor()).addPathPatterns("/**").excludePathPatterns("index.html","/");  拦截所有请求  排除登陆请求
    			拦截任意请求
   4.RESTFUL  CRUD
   	路劲得格式  URI ：/资源名称/资源标识  HTTP请求方式区分CRUD操作
   		
```

## 6.7错误处理

```java
返回一个错误得默认页面
	
	如果是其他客户端，默认响应一个 json数据
	原理 可以参照ErrorMvcAutoConfiguration；错误处理得自动配置
		定制错误得页面
		定制错误得json数据
		
		给容器添加以下组件
			1.DefaultErrorAttributeS:帮我们在页面共享信息
			2.BasicErrorController 处理默认error请求,手机json，浏览器会是一个错误页面
			3.ErrorPAgeCustomizer  系统出现错误来到error请求进行处理 
			4.DefaultErrorViewResolver
			
			一旦出现4xx,5xx 3生效 定制错误得响应规则；
				有模板引擎得情况下，error/状态码
					获取时间戳，状态码，提示错误，异常消息，errors jsr303校验都在这里
				没有模板，去静态资源下面找
					
			异常处理器  
				@ControllerAdvice
				public class MyExceptionHandler{
					//浏览器和客户端返回的都是json
                    @ExceptionHandler(Exception.class)
                    public String handleException(Exception e){
                        转发到 error
                    }
				}
```

## 6.8. 配置嵌入式Servlet容器

```java
Springboot默认使用 嵌入式Servlet容器(Tomcat);
	问题：
		1.如何定制修改servlet的相关配置
			1.properties
            	server.port=8081
				server.context-path=/crud
				//通用信息设置
				server.xxx
				//tomcat的设置
				server.tomcat.uri-encoding=UTF-8
			2.定制EmbeddedServletContainerCustomizer
				定制嵌入式的servlet容器相关的
				被WebServerFactoryCustomizer替代了
		2.能不能切换其他的servlet容器
```

## 6.9注册Servlet的三大组件

```java
springboot中没有web.xml
	Servlet  ServletRegistrationBean
		写一个servlet
			1.public class Myservlet extends HttpServlet {
                @Override
                protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
                    super.doGet(req, resp);
                    resp.getWriter().write("hellodsadasdsada!");
                }
            }
            2.注册
	Filter   FilterRegistrationBean
		    @Override
            public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
                System.out.println("myFilter process....");
                filterChain.doFilter(servletRequest,servletResponse);
            }
	Listener	ServletListenerRegistrationBean
	
	
	
	
	在组件中注册：
@Configuration
public class MyservletConfig {
    //注册三大组件
    @Bean
    public ServletRegistrationBean myserver(){
        ServletRegistrationBean<Servlet> servletServletRegistrationBean
                = new ServletRegistrationBean<>(new Myservlet(),"/myservlet");
        return servletServletRegistrationBean;
    }
    //注册filter
    @Bean
    public FilterRegistrationBean myfilter(){
        FilterRegistrationBean<Filter> filterFilterRegistrationBean = new FilterRegistrationBean<>();
        filterFilterRegistrationBean.setFilter(new MyFilter());
        filterFilterRegistrationBean.setUrlPatterns(Arrays.asList("/hello","/myservlet"));
        return filterFilterRegistrationBean;
    }
    //注册Listener
    @Bean
    public ServletListenerRegistrationBean mylistener(){
        ServletListenerRegistrationBean<MyLsitener> myLsitenerServletRegistrationBean = new ServletListenerRegistrationBean<MyLsitener>(new MyLsitener());
        return myLsitenerServletRegistrationBean;
    }
}
默认拦截 / 可以修改
```

## 6.10切换其他嵌入式servlet容器

```java
Jetty （长连接应用适合聊天）
UnderTow  (不支持jsp)
tomcat(默认使用)

		
springboot支持切换
		首先排除tomcat容器
			exclusions
		引入其他的servlet容器
```

## 6.11外置的servlet容器

```java
嵌入式 servlet的
	优点
		简单，便捷  不用需要安装 tomcat
	缺点
		不能使用jsp，优化定制比较复杂
		
外置的servlet容器
		应用是  以 war包的方式打包
		选择 war包，创建项目得时候
```



# 8.Springboot与数据访问

```java
对于数据访问层，无论是 SQL还是 NOSQL 默认采用整合spring Data的方式进行统一处理，
测试相关 SQL相关，NoSQL再缓存，消息，检索等章节测试  
		JDBC  MYbatis  Jpa
		
		自定义数据源
		使用
```

## 8.1数据源类型执行sql原生jdbc

```java
DataSourceInitiaalizer:ApplicationListerner
	可以使用
		schema
			指定sql文件位置
```

## 8.2整合mybatis

```java
<dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.1.2</version>
        </dependency>
```

## 8.3SpringData

```java
简化数据访问操作
	1.统一数据访问的api

	2.统一的repository统一接口
	
	3.Jpa和SpringData   
```

### 8.3.1整合api

```java
1.编写一个实体类和数据表进行映射
	Entity   告诉这是一个实体类
	@Table(name = "tbl_user")  和数据表对应的类 指定和那个数据表对应
	@id   标注这是一个主键
	@Column() 这是和数据表对应的一个列  省略的话就是属性
2.编写Dao接口操作实体类对应的数据表
	继承 Reporsitory  泛型写 实体类型和主键的类型
3.基本的配置
	yml
	jpa:
	  hibernate:
	  	ddl-auto: update
	  show-sql: true	
```

# 9.SpringBoot 与 缓存

```java
JSR-107  五个核心接口 cacheingprovider cachaeManager cache  entry  expiry
Spring缓存抽象  简化缓存  ，可以使用 Jsr-107的注解
整合redis

```

## 9.1ConcurrentMapCacheManage

```java
1.搭建环境
	导入数据库文件
	创建javabean对象
	整合mybatis
		1.配置数据源
		2.注解版本的mybatis  扫描mapper  声明mapper类
		@MapperScan("com.cache.springcache.mapper")
		@SpringBootApplication
		
		@Component
		@Mapper
		
		体验缓存
			1.开启基于注解的缓存		@EnableCaching
			2.标注缓存注解即可
				@cacheable  根据方法的请求参数对结果进行缓存
					CahceManager 管理多个cache组件, 指定缓存管理器，
					对结果进行缓存，以后要是相同的数据，直接从缓存中获取
					cachenames/values 指定缓存名字，可以指定多个缓存
					key  缓存数据时候用的key:指定  默认是方法参数的值 1 2 3
							支持SPEL表达式   指定要放行的key具体的值
					condition  指定符合条件下的 才能被缓存
							condition = "#id>0"
					unless  和condition相反  unless = "#result == null"
					sync  指定异步
				@cahceEvict  清除缓存
					删除某个数据，清除缓存数据
					@CacheEvict(value = "emp" key = "#id")
					allEntries = true  缓存都删除不指定key
					beforeInvocation = false  缓存的清除是否在方法之前执行
						false 之后  默认数据
				@cacheput  保证方法被调用，希望结果被缓存
					更新缓存数据，例如修改了数据库的某个数据，同时更新数据
					1.先调用目标方法
					2.将目标方法缓存起来
				数据多了，进行多个配置
				@Caching (
					cacheable = {
                        @Cacheable()
					},
					put = {
                        @CachePut()
					}
				)
					注意只要加了 Cache就一定会执行这个方法
				@CacheConfig(value = "emp")
					加到类上面，这个类里面的方法都缓存为同一个名字

```

## 9.2redis

```java
实际开发中  使用缓存中间件  redis ,ehcache, memcached
整合redis 作为缓存
是一个开源的，内存中的数据结构存储系统，它可以作为数据库，缓存，消息中间件，支持多种数据结构

安装redis
		docker pull redis
		docker run -d --name myredis -p 6379:6379 redis --requirepass "mypassword"

整合redis缓存
	<!--引入redis-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>
配置文件
	spring.redis.host=47.101.212.62
	
	@Autowired
    StringRedisTemplate stringRedisTemplate;
    	操作字符串
    @Autowired
    RedisTemplate redisTemplate;
    	操作字符串
语法
	* redis常见五大类
    * String List Set Hash ZSet
    
     /*保存数据redis*/
        stringRedisTemplate.opsForValue().append("msg","hello");
     /*redis读取数据*/
        String msg = stringRedisTemplate.opsForValue().get("msg");
        System.out.println(msg);
  默认如果保存对象，使用jdk序列化对象，序列化后的数据保存在redis中
  切换系列化对象  配置类
  1.
  	@Configuration
public class redisConfig {
    @Bean
    public RedisTemplate<Object, Employee> empredisTemplate(RedisConnectionFactory 	redisConnectionFactory) throws UnknownHostException {
        RedisTemplate<Object, Employee> template = new RedisTemplate();
        template.setConnectionFactory(redisConnectionFactory);
        Jackson2JsonRedisSerializer<Employee> serializer = new  Jackson2JsonRedisSerializer<Employee>(Employee.class);
        template.setDefaultSerializer(serializer);
        return template;
    }
}
	2.
	/*自动注入
    * */
    @Autowired
    RedisTemplate<Object,Employee> employeeRedisTemplate;
    3.
     @Test
    public void Test3(){
        Employee employee = employeeMapper.getEmpById(1);
        employeeRedisTemplate.opsForValue().set("emp-01",employee);
        /*
        * 1.将redis以json的方法保存
        * 自己将对象转化为json
        * redisTemplate默认的序列化规则
        * */

    }
```

### 9.2.1测试缓存

```java
原理 缓存管理器
默认保存数据 特别是  kv都是对象时候  用序列化来保存的

保存为json'
	自定义cacheManager
```

# 10.消息队列

```java
中间件
	可以通过消息服务中间件来提升系统异步通信，扩展解耦能力
	
	两个概念
	消息代理  消息中间间服务器，服务器把消息传送到目的地
	
	目的地
	队列 点对点消息通信
		消息只有唯一的发送者和接受者，但是不一定只有一个接收者
	主题 发布，订阅 消息通信 
		发布者发送消息到主题，多个接收者订阅这个主题，那么消息就会同时收到
		

	JMS  java消息服务
		基于jvm消息代理的规范，ActiveMQ,HornetMQ是  JMS实现
	AMQP
		高级消息队列协议  兼容 JMS
		RabbitMQ
	
```

## 10.1RabbitMQ

```java
message
	消息，由消息头，消息体构成，消息体不透明，消息头包括路由键 routing-key,priority,delivery-mode等
publisher
	消息的生产者，也是一个向交换器发布消息的客户端应用程序
Exchange
	交换器，用来接受生产者发送的消息并且将这些消息	路由给服务器队列
	
	概念
		Queue	队列
		Binding  绑定
		Connect	 网络连接
		Channel  信道
		Consumer 消费者
		Virtual Host 虚拟主机
		broker  表示消息队列服务器主体
		
		Direct Exchange   匹配单播模式
		Fanout Exchange   广播模式速度最快
		Topic Exchange	  多个消息匹配一个队列
```

## 10.2安装使用

```java
docker pull rabbitmq:3-management
docker run -d -p 5672:5672 -p 15672:15672 --name myrabbit 5537c2a8f7c5

默认账号密码  guest   guest
//中国镜像
docker pull registry.docker-cn.com/library/ubuntu:16.04


Direct Exchange   匹配单播模式    点对点   key值对应
Fanout Exchange   广播模式速度最快   全部发出去  全部收到
Topic Exchange	  多个消息匹配一个队列  任意匹配一个就可以收到

配置
spring.rabbitmq.host=47.101.212.62
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
spring.rabbitmq.port=5672

测试
	 //rabbitTemplate.send(exchange,routekey,message);
	 //发送***********有问题
	  Map<String,Object> map = new HashMap<>();
        map.put("msg","第一个消息");
        map.put("data", Arrays.asList("helloword",123,true));
        rabbitTemplate.convertAndSend("exchange.dircet","atguigu.news",map)
     //接受
     	Object o = rabbitTemplate.receiveAndConvert("atguigu.news");
        System.out.println(o);
        
      //配置自动转化   json
      @Configuration
        public class MyRabbitmq {
            @Bean
            public MessageConverter messageConverter(){
                return new Jackson2JsonMessageConverter();
            }
        }
        
        
```

## 10.3监听

```java
@EnableRabbit  开启注解  在  springboot启动项目
//业务层
@Service
public class BookService {
    //如果收到消息  将会触发
    @RabbitListener(queues = "atguigu.news")
    public void receive(Book book){
        System.out.println(book);
    }
}
```

## 10.4程序中创建交换器和路由AmqpAdmin

```java
创建和删除队列  exchange  , bind等

 @Autowired
    AmqpAdmin amqpAdmin;

    @Test
    public void createExchange(){
        //amqpAdmin.declareExchange(new DirectExchange("amqpadmin.exchange"));
        //amqpAdmin.declareQueue(new Queue("adqpadmin.queue"));
        amqpAdmin.declareBinding(new Binding("adqpadmin.queue", Binding.DestinationType.QUEUE,"amqpadmin.exchange","amqp.haha",null));
    }
```

# 11.springboot检索

```java
javaElasticSearch检索  分布式搜索服务，提供restful服务，底层基于Lucene
docker pull registry.docker-cn.com/library/elasticsearch

配置阿里云docker镜像加速
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://rxamftpx.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker

访问  ：9200 端口在浏览器


存储员工数据
	PUT /megacorp/employee/1
        {
            "first_name" : "John",
            "last_name" :  "Smith",
            "age" :        25,
            "about" :      "I love to go rock climbing",
            "interests": [ "sports", "music" ]
        }
获取员工数据
	GEt /megacorp/employee/1
	
删除
	Delete /megacorp/employee/1
	
	
搜索所有员工

	GET /megacorp/employee/_search

尝试下搜索姓氏为 ``Smith`` 的雇员
	GET /megacorp/employee/_search?q=last_name:Smith

使用查询表达式搜索
	GET /megacorp/employee/_search
        {
            "query" : {
                "match" : {
                    "last_name" : "Smith"
                }
            }
        }
复杂的搜素
	GET /megacorp/employee/_search
        {
            "query" : {
                "bool": {
                    "must": {
                        "match" : {
                            "last_name" : "smith" 
                        }
                    },
                    "filter": {
                        "range" : {
                            "age" : { "gt" : 30 } 
                        }
                    }
                }
            }
        }
 全文搜素
 	GET /megacorp/employee/_search
        {
            "query" : {
                "match" : {
                    "about" : "rock climbing"
                }
            }
        }
  短语搜素 完整匹配
  	GET /megacorp/employee/_search
        {
            "query" : {
                "match_phrase" : {
                    "about" : "rock climbing"
                }
            }
        }
   高亮搜索
   	GET /megacorp/employee/_search
        {
            "query" : {
                "match_phrase" : {
                    "about" : "rock climbing"
                }
            },
            "highlight": {
                "fields" : {
                    "about" : {}
                }
            }
        }
```

## 11.1springboot整合

```java
springboot默认使用springdata来操作  ElasticSearch


@Autowired
    BookRepository bookRepository;

仓库
	public interface BookRepository extends ElasticsearchRepository<Book,Integer> {
	}

Bean  实体类

    @Test
    void contextLoads() {
        Book book = new Book();
        book.setId(1);
        book.setAuthor("吴承恩");
        book.setBookName("西游记");
        bookRepository.index(book);
    }
```

# 12.springboot 异步任务

快速体验

​	正常情况

```java
public void hello(){
    try {
        Thread.sleep(3000);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    System.out.println("处理数据中！！");
}

开启异步注解
	@Async 放在运行方法上面
        //开启异步注解
    @EnableAsync
    @SpringBootApplication
```

## 12.1定时任务

```java
@EnableScheduling
@SpringBootApplication  开启定时任务

// second,minutes,hour,day of month,month,day of week
    @Scheduled(cron = "0 * * * * MON-SAT")
    public void hello(){
        System.out.println("启动");
    }
    指定什么时候启动
    
    //没4秒执行一次
     @Scheduled(cron = "0/4 * * * * MON-SAT")
```

## 12.2邮件任务

```java
     <!--引入邮件任务-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-mail</artifactId>
        </dependency>
        
      关闭qq邮箱服务
      配置
      	spring.mail.username=1092283755@qq.com
		spring.mail.password=eqldanvdgggcfhhc
		spring.mail.host=smtp.qq.com
		spring.mail.properties.mail.smtp.ssl.enable=true
	 测试类
	 	@Autowired
    JavaMailSenderImpl mailSender;

    @Test
    void contextLoads() {
        SimpleMailMessage message = new SimpleMailMessage();
        //设置邮件信息
        message.setSubject("通知");
        message.setText("今晚7.30开会");
        message.setTo("ryhweo@163.com");
        message.setFrom("1092283755@qq.com");
        mailSender.send(message);
    }
    
    发送附件图片
    	MimeMessage mimeMessage = mailSender.createMimeMessage();
        //设置邮件信息
        MimeMessageHelper mimeMessageHelper = new MimeMessageHelper(mimeMessage, true);
        mimeMessageHelper.setText("今晚7.30开会");
        mimeMessageHelper.setTo("ryhweo@163.com");
        mimeMessageHelper.setFrom("1092283755@qq.com");
        mimeMessageHelper.setSubject("通知2");
        mimeMessageHelper.addAttachment("1.jpg",new File("C:\\Users\\Administrator\\Desktop\\太阳池.jpg"));
        mailSender.send(mimeMessage);
```

# 13.springboot和安全

```java
shiro
springsecurity
```

## 13.1认证和授权

```java
1.引入springsecurity模块
	<!--引入springsecurity-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>
2.编写一个配置类
    @EnableWebSecurity
    public class MysecurityConfig extends WebSecurityConfigurerAdapter {
    }
3.编写权限
	http.authorizeRequests().antMatchers("/").permitAll()
                .antMatchers("/level1/**").hasRole("Vip1")
                .antMatchers("/level2/**").hasRole("Vip2")
                .antMatchers("/level3/**").hasRole("Vip3");
4.登录页
	开启自动配置的登录功能
	//如果没有权限来到登陆页面
        http.formLogin();
5.分配授权
	//super.configure(auth);
         auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder()).withUser("zhangsan").password(new BCryptPasswordEncoder().encode("123")).roles("Vip1","Vip2")
                .and()
                .withUser("lisi").password(new BCryptPasswordEncoder().encode("123")).roles("Vip2","Vip3")
                .and()
                .withUser("wangwu").password(new BCryptPasswordEncoder().encode("123")).roles("Vip1","Vip3");


```

# 14.分布式dubbo+zookeeper

```java
zookeeper  注册中心
dubbo 	分布式服务框架


安装 zookeeper 
	docker pull zookeeper
	1.引入dubbo和zookeeper
		<!--引入dubbo-->
        <dependency>
            <groupId>com.alibaba.boot</groupId>
            <artifactId>dubbo-spring-boot-starter</artifactId>
            <version>0.1.0</version>
        </dependency>
        <!--引入zookeeper客户端工具-->
        <dependency>
            <groupId>com.github.sgroschupf</groupId>
            <artifactId>zkclient</artifactId>
            <version>0.1</version>
        </dependency>
     2.配置dubbo的扫描包和相关注册中心
     	dubbo.application.name=provider_ticket
		dubbo.registry.address=zookeeper://47.101.212.62:2181
		dubbo.scan.base-packages=com.it.Service
     3.使用@service 发布服务
     @Component
	@Service
	public class TicketServiceImpl implements TicketService{
```

# 15.springboot和springcloud

```java
Eureka  服务发现
Ribbon 客户端负载均衡
Hystrix 断路器
ZUUL 服务网关
springcloud 分布式配置
```

## 15.1配置

```java
配置 eureka
server:
  port: 8761
eureka:
  instance:
    hostname: eureka-server #实例的主机名字
  client:
    register-with-eureka: false #不把自己注册
    fetch-registry: false #不从eureka上获取服务注册信息
    service-url:
      defaultZone: http://localhost:8761/eureka/
      
      开启服务
      @EnableEurekaServer
   
  配置提供者
server:
  port: 8001
spring:
  application:
    name: provider-ticket
eureka:
  instance:
    prefer-ip-address: true #注册服务使用服务的ip
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
      
   配置消费者
server:
  port: 8200
spring:
  application:
    name: consumer
eureka:
  instance:
    prefer-ip-address: true #注册服务使用服务的ip
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
      
  开启发现服务功能
  @EnableDiscoveryClient
  controller  写   RestTemplate    getforobject("http://PROVIDER-TICKET/tivket",String.class)
```

## 17.java发请求和转化json

```java
转化json'
	 JSONObject json = JSONObject.parseObject(forObject);
	 <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.9</version>
        </dependency>
发请求
	 public ArrayList<Object> today(String cityname){
        //配置代理发送请求
        System.out.println(cityname);
        ArrayList<Object> obj = new ArrayList<>();
        obj.add(client(cityname));
        System.out.println(obj);
        return obj;
    }
    public Object client(String cityname){
        //url
        String uri = "http://v.juhe.cn/weather/index";
        //key
        String key = "26a341912ab49adbcf14685a286031a2";
        //map
        Map<String,String> map = new HashMap<>();
        //params
        map.put("cityname",cityname);
        map.put("key",key);
        RestTemplate client = new RestTemplate();
        String forObject = client.getForObject(uri+"?cityname={cityname}&key={key}",
                String.class,map);
        JSONObject json = JSONObject.parseObject(forObject);
        //响应头信息
        //  执行HTTP请求
        return json;
    }
```

# 18.https请求和转发

```xml
生成密钥
keytool -genkey -alias android.keystore -keyalg RSA -validity 20000 -keystore android.keystore 
密码 123456

keytool -genkey -alias tomcat -keyalg RSA -keystore tomcat.keystore
放到根目录下面
配置文件
server.ssl.key-store=tomcat.keystore
#密钥库密码
server.ssl.key-store-password=123456
server.ssl.keyStoreType=JKS
server.ssl.keyAlias:tomcat
 
#https加密端口号 443
server.port=443
#SSL证书路径 一定要加上classpath:
server.ssl.key-store=classpath:520oo.jks
#SSL证书密码
server.ssl.key-store-password=214215109110451
#证书类型
server.ssl.key-store-type=JKS
#证书别名
server.ssl.key-alias=alias


阿里巴巴官网下载证书
用命令转化
回车，会提示你输入三次密码，建议三次都是输入密码文本的密码，成功后会再文件夹下生成domains.jks文件
keytool -importkeystore -srckeystore 你的证书名称.pfx -destkeystore domains.jks -srcstoretype PKCS12 -deststoretype JKS

配置  pfx文件放到resources目录下
server.ssl.key-store=classpath:zcz.pfx
server.ssl.key-store-password=7QgFatf7
server.ssl.keyStoreType=PKCS12
```

# 19sprinngboot跨域

```java
1.
@Configuration
public class CorsConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("*")
                .allowedMethods("GET", "HEAD", "POST", "PUT", "DELETE", "OPTIONS")
                .allowCredentials(true)
                .maxAge(3600)
                .allowedHeaders("*");
    }
}
2.过滤器
@WebFilter(filterName = "CorsFilter ")
@Configuration
public class CorsFilter implements Filter {
    @Override
    public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain) throws IOException, ServletException {
        HttpServletResponse response = (HttpServletResponse) res;
        response.setHeader("Access-Control-Allow-Origin","*");
        response.setHeader("Access-Control-Allow-Credentials", "true");
        response.setHeader("Access-Control-Allow-Methods", "POST, GET, PATCH, DELETE, PUT");
        response.setHeader("Access-Control-Max-Age", "3600");
        response.setHeader("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
        chain.doFilter(req, res);
    }
}

3.注解
	@CrossOrigin(origins = "*",maxAge = 3600)
```

# 20.springboot返回时间类型

```java
@JsonFormat(pattern="yyyy-MM-dd HH:mm:ss", timezone="GMT+8")
    public Date time;
    
    
 全局配置
 	spring:
　　	jackson:
 		date-format: yyyy-MM-dd HH:mm:ss
 		time-zone: GMT+8
```

# 21.java实现qq轰炸

```java
import java.awt.AWTException;
import java.awt.Robot;
import java.awt.Toolkit;
import java.awt.datatransfer.Clipboard;
import java.awt.datatransfer.StringSelection;
import java.awt.datatransfer.Transferable;
import java.awt.event.KeyEvent;

public class Springdemo1Application {
    public static void main(String[] args) throws AWTException {
        SpringApplicationBuilder builder = new SpringApplicationBuilder(Springdemo1Application.class);
        //SpringApplication.run(SystemctlApplication.class, args);
        builder.headless(false)
                // .web(WebApplicationType.NONE)
                // .bannerMode(Banner.Mode.OFF)
                .run(args);
        String sentence = "从前有座山,山里有座庙,庙里有个老和尚和小和尚,和尚对小和尚说：";// 定义要发送的话
        Robot robot = new Robot();// 创建Robot对象
        robot.delay(3000);// 延迟三秒，主要是为了预留出打开窗口的时间，括号内的单位为毫秒
        Clipboard clip = Toolkit.getDefaultToolkit().getSystemClipboard();
        String[] authors = sentence.split("[,]");// 字符串根据,分割
        for (int j = 0; j < 50; j++) {//循环次数
            for (int i = 0; i < authors.length; i++) {
                String sentencet = authors[i];
                Transferable tText = new StringSelection(sentencet);
                clip.setContents(tText, null);
                // for (int j = 1; j <= 1; j++) {
                // 以下两行按下了ctrl+v，完成粘贴功能
                robot.keyPress(KeyEvent.VK_CONTROL);
                robot.keyPress(KeyEvent.VK_V);

                robot.keyRelease(KeyEvent.VK_CONTROL);// 释放ctrl按键，像ctrl，退格键，删除键这样的功能性按键，在按下后一定要释放，不然会出问题。crtl如果按住没有释放，在按其他字母按键是，敲出来的回事ctrl的快捷键。
                robot.delay(100);// 延迟一秒再发送，不然会一次性全发布出去，因为电脑的处理速度很快，每次粘贴发送的速度几乎是一瞬间，所以给人的感觉就是一次性发送了全部。这个时间可以自己改，想几秒发送一条都可以
                robot.keyPress(KeyEvent.VK_ENTER);// 回车
                // }
            }
        }
    }
}

```

# 22.实现jwt

```java
1.引入依赖
		<dependency>
              <groupId>com.auth0</groupId>
              <artifactId>java-jwt</artifactId>
              <version>3.4.0</version>
        </dependency>
2.token注解配置
	//用来跳过验证的 PassToken
	@Target({ElementType.METHOD, ElementType.TYPE})
	@Retention(RetentionPolicy.RUNTIME)
	public @interface PassToken {
    	boolean required() default true;
	}
	
	//用于登录后才能操作
	@Target({ElementType.METHOD, ElementType.TYPE})
    @Retention(RetentionPolicy.RUNTIME)
    public @interface UserLoginToken {
        boolean required() default true;
    }
3.新建一个拦截器配置 用于拦截前端请求 实现   WebMvcConfigurer 
    @Configuration
    public class WebConfig implements WebMvcConfigurer {
        @Autowired
        AuthenticationInterceptor authenticationInterceptor;
        @Override
        public void addInterceptors(InterceptorRegistry registry) {
            registry.addInterceptor(authenticationInterceptor)
                    .addPathPatterns("/**");
        }
    //    @Bean
    //    public AuthenticationInterceptor authenticationInterceptor() {
    //        return new AuthenticationInterceptor();
    //    }
    }
 4.新建一个 AuthenticationInterceptor  实现HandlerInterceptor接口  实现拦截还是放通的逻辑
 @Configuration
public class AuthenticationInterceptor implements HandlerInterceptor {
    @Autowired
    UserService userService;

    @Override
    public boolean preHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object object) throws Exception {
        String token = httpServletRequest.getHeader("token");// 从 http 请求头中取出 token
        // 如果不是映射到方法直接通过
        if (!(object instanceof HandlerMethod)) {
            return true;
        }
        HandlerMethod handlerMethod = (HandlerMethod) object;
        Method method = handlerMethod.getMethod();
        //检查是否有passtoken注释，有则跳过认证
        if (method.isAnnotationPresent(PassToken.class)) {
            PassToken passToken = method.getAnnotation(PassToken.class);
            if (passToken.required()) {
                return true;
            }
        }
        //检查有没有需要用户权限的注解
        if (method.isAnnotationPresent(UserLoginToken.class)) {
            UserLoginToken userLoginToken = method.getAnnotation(UserLoginToken.class);
            if (userLoginToken.required()) {
                // 执行认证
                if (token == null) {
                    throw new RuntimeException("无token，请重新登录");
                }
                // 获取 token 中的 user id
                String userId;
                try {
                    userId = JWT.decode(token).getAudience().get(0);
                } catch (JWTDecodeException j) {
                    throw new RuntimeException("401");
                }
                User user = userService.findUserById(userId);
                if (user == null) {
                    throw new RuntimeException("用户不存在，请重新登录");
                }
                // 验证 token
                JWTVerifier jwtVerifier = JWT.require(Algorithm.HMAC256(user.getPassword())).build();
                try {
                    jwtVerifier.verify(token);
                } catch (JWTVerificationException e) {
                    throw new RuntimeException("401");
                }
                return true;
            }
        }
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {

    }

    @Override
    public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) throws Exception {

    }

}
5.新建一个Server 用于下发Token
@Service
public class TokenService {

    public String getToken(User user) {
        Date start = new Date();
        long currentTime = System.currentTimeMillis() + 60* 60 * 1000;//一小时有效时间
        Date end = new Date(currentTime);
        String token = "";

        token = JWT.create().withAudience(user.getId()).withIssuedAt(start).withExpiresAt(end)
                .sign(Algorithm.HMAC256(user.getPassword()));
        return token;
    }
}
6.新建一个工具类 用户从token中取出用户Id
public class TokenUtil {
    public static String getTokenUserId() {
        System.out.println(1111);
        String token = getRequest().getHeader("token");// 从 http 请求头中取出 token
        String userId = JWT.decode(token).getAudience().get(0);
        return userId;
    }
     public static HttpServletRequest getRequest() {
         ServletRequestAttributes requestAttributes = (ServletRequestAttributes) RequestContextHolder
                 .getRequestAttributes();
         return requestAttributes == null ? null : requestAttributes.getRequest();
     }
}
7.新建一个简单的控制器用于验证，把token存到Session里面
	@Autowired
    UserService userService;
    @Autowired
    TokenService tokenService;
    @GetMapping("/login")
    public Map<String, Object> login(User user, HttpServletResponse response) throws JSONException {
        JSONObject jsonObject = new JSONObject();
        Map<String,Object> map = new HashMap<>();
        User userForBase = new User();
        userForBase.setId("1");
        userForBase.setPassword("123");
        userForBase.setUsername("mrc");

        if (!userForBase.getPassword().equals(user.getPassword())) {
            map.put("message", "登录失败,密码错误");
            return jsonObject;
        } else {
            String token = tokenService.getToken(userForBase);
            map.put("token", token);
            Cookie cookie = new Cookie("token", token);
            cookie.setPath("/");
            response.addCookie(cookie);

            return map;

        }
    }
    @UserLoginToken
    @GetMapping("/getMessage")
    public String getMessage() {

        // 取出token中带的用户id 进行操作
        TokenUtil.getTokenUserId();

        return "你已通过验证";
    }
```

# 23.实现文件的上传下载

```java
@RestController
public class UploadController {

    @PostMapping("/upload")
    public String fileUpload(@RequestParam("file") MultipartFile file){
        if(file.isEmpty()){
            return "false";
        }
        String fileName = file.getOriginalFilename();
        int size = (int) file.getSize();
        System.out.println(fileName + "-->" + size);
        String path = "D:/testupload" ;
        File dest = new File(path + "/" + fileName);
        if(!dest.getParentFile().exists()){ //判断文件父目录是否存在
            dest.getParentFile().mkdir();
        }
        /*判断文件后缀*/
        Integer last = fileName.lastIndexOf('.');
        String dotname = fileName.substring(last+1);
        System.out.println(dotname);
        //创建目录
        File checkexits = new File("D:/testupload/"+dotname+"/");
        System.out.println(checkexits.exists());
        if(checkexits.exists()){
            System.out.println("存在目录");
        }else {
            checkexits.mkdir();
        }
        File cunchu = new File("D:/testupload/"+dotname+"/"+fileName);
        try {
            file.transferTo(cunchu); //保存文件
            return "true";
        } catch (IllegalStateException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
            return "false";
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
            return "false";
        }
    }
}
    
```

```java
servlet:
  multipart:
    max-file-size: 500MB
    max-request-size: 500MB
```

```java
 @RequestMapping("/downloadFile")

 private String downloadFile(HttpServletResponse response){
         String downloadFilePath = "/root/fileSavePath/";//被下载的文件在服务器中的路径,
         String fileName = "demo.xml";//被下载文件的名称
         
         File file = new File(downloadFilePath);
         if (file.exists()) {
             response.setContentType("application/force-download");// 设置强制下载不打开            
             response.addHeader("Content-Disposition", "attachment;fileName=" + fileName);
             byte[] buffer = new byte[1024];
             FileInputStream fis = null;
             BufferedInputStream bis = null;
             try {
                 fis = new FileInputStream(file);
                 bis = new BufferedInputStream(fis);
                 OutputStream outputStream = response.getOutputStream();
                 int i = bis.read(buffer);
                 while (i != -1) {
                     outputStream.write(buffer, 0, i);
                     i = bis.read(buffer);
                 }
               
                 return "下载成功";
             } catch (Exception e) {
                 e.printStackTrace();
             } finally {
                 if (bis != null) {
                     try {
                         bis.close();
                     } catch (IOException e) {
                         e.printStackTrace();
                     }
                 }
                 if (fis != null) {
                     try {
                         fis.close();
                     } catch (IOException e) {
                         e.printStackTrace();
                     }
                 }
             }
         }
        return "下载失败";    
     }
```

```java
 <dependency>
                <groupId>commons-fileupload</groupId>
                <artifactId>commons-fileupload</artifactId>
                <version>1.3.3</version>
            </dependency>
```

# 24.正则表达式

```java
  //定义正则表达式
        String regEx = "^((html)|(mp4)|(exe)|(zip)|(jpg)|(png))$";
        //编译成为正则表达式
        Pattern pattern = Pattern.compile(regEx);
        // 忽略大小写的写法
        // Pattern pat = Pattern.compile(regEx, Pattern.CASE_INSENSITIVE);
        Matcher matcher = pattern.matcher(dotname);
        boolean rs = matcher.matches();
        System.out.println(rs);
```

# 25.shrio

```java
java的安全权限框架
认证 授权  加密 会话管理 web集成  缓存等

认证
subjects(主体)  访问系统的用户，可以是用户，程序，进行认证的都叫主体
principal(身份信息)  是主体进行身份认证的标识，标识具有唯一性，如用户名，密码，手机号，邮箱地址等。一个主体可以有多个身份，但是必须得有一个主身份
credential(凭证信息)  凭证信息 用户密码，指纹等等，只有主体自己知道

token  令牌  身份信息 和 凭证信息

授权
Who  主体 需要访问系统的资源
What  资源，资源类型
How  权限和许可  权限离开资源是没有意义的  粗颗粒 资源类型 和 细颗粒的资源实例


三大模块
    1. Subject：主体，一般指用户。
    2. SecurityManager：安全管理器，管理所有Subject，可以配合内部安全组件。(类似于SpringMVC中的DispatcherServlet)
    3. Realms：用于进行权限信息的验证，一般需要自己实现。
```

## 25.1RBAC

```java
基于角色的访问控制     缺点 系统的可扩展性比较差  需要修改代码

基于资源的访问控制     系统的可扩展性强
shiro.web.enabled=false
```

## 25.2粗粒度和细粒度

```
粗  用户具有用户管理的权限
细  用户只允许导出自己创建的订单明细
```

## 25.3开始搭建

```java
<dependency>
	<groupId>org.apache.shiro</groupId>
	<artifactId>shiro-spring-boot-web-starter</artifactId>
	<version>1.4.2</version>
</dependency>

1.安全管理器依赖于  realm
2.自定义realm   依赖于凭证匹配器
3.凭证匹配器   
		依赖于算法名称
		散列次数
1.导入 jar包
anon	无参，开放权限，可以理解为匿名用户或游客
authc	无参，需要认证
logout	无参，注销，执行后会直接跳转到shiroFilterFactoryBean.setLoginUrl(); 设置的 url
authcBasic	无参，表示 httpBasic 认证
user	无参，表示必须存在用户，当登入操作时不做检查
ssl	无参，表示安全的URL请求，协议为 https
perms[user]	参数可写多个，表示需要某个或某些权限才能通过，多个参数时写 perms["user, admin"]，当有多个参数时必须每个参数都通过才算通过
roles[admin]	参数可写多个，表示是某个或某些角色才能通过，多个参数时写 roles["admin，user"]，当有多个参数时必须每个参数都通过才算通过
rest[user]	根据请求的方法，相当于 perms[user:method]，其中 method 为 post，get，delete 等
port[8081]	当请求的URL端口不是8081时，跳转到schemal://serverName:8081?queryString 其中 schmal 是协议 http 或 https 等等，serverName 是你访问的 Host，8081 是 Port 端口，queryString 是你访问的 URL 里的 ? 后面的参数
```

## 25.4数据库创建

```java

@Data
public class User implements Serializable {
    private Integer id;
    private String username;
    private String password;
    private String perms;
}
```

## 25.5配置

```java
shiro.web.enabled=false
```

## 25.6 shrioConfig 过滤请求

```java
@Configuration
public class ShiroConfig {
    //创建拦截器
    /*
    * ShiroFilterFactoryBean 为Shiro过滤器工厂类
    * 配置一些过滤路径
    *
    * */
    @Bean
    public ShiroFilterFactoryBean getShiroFilterFactoryBean(@Qualifier("getSecurityManager") SecurityManager securityManager){
        ShiroFilterFactoryBean bean = new ShiroFilterFactoryBean();
        //必须设置安全管理器
        bean.setSecurityManager(securityManager);
        //配置资源受限列表
        //配置shiro默认登录界面地址，前后端分离中登录界面跳转由端控制，后台仅返回json数据
        bean.setLoginUrl("/unauth.action");


        //添加shiro的内置过滤器
        //注意过滤器配置顺序 不能颠倒
        /*
        * anon 无需认证就可以访问
        * authc   必须认证才能访问
        * user    必须拥有记住我的功能才能访问
        * perms   必须对某个资源拥有权限才能访问
        * role    必须拥有角色权限才能访问
        * */
        Map<String, String> map = new HashMap<>();
        bean.setFilterChainDefinitionMap(map);

        //授权 未授权跳转到未授权页面
        map.put("/del","perms[user:del]");
        map.put("/add","perms[user:add]");
        //自定义认证页面
        //无需认证
        map.put("/login","anon");
        // 需要认证的url
//        map.put("/add", "authc");
        //设置登录的请求
        bean.setLoginUrl("/login");
        //设置未授权
        bean.setUnauthorizedUrl("/noauth");
        return bean;
    }
    //创建安全管理器
    //SecurityManager 为shiro安全管理器，管理着所有的Subject
    @Bean
    public DefaultWebSecurityManager getSecurityManager(@Qualifier("getRealm") UserRealm userRealm){
        DefaultWebSecurityManager SecurityManager = new DefaultWebSecurityManager();
        //注入realm
        SecurityManager.setRealm(userRealm);
        return SecurityManager;
    }
    //创建自定义realm
    //引入自己实现的 ShiroRealm
    @Bean
    public UserRealm getRealm(){
        UserRealm realm = new UserRealm();
//        realm.setCredentialsMatcher(matcher());
        return realm;
    }
}
```

## 25.7配置Realm

```java
public class UserRealm extends AuthorizingRealm {
    @Autowired
    UserService userService;
    //授权
    @Override
    protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
        System.out.println("执行了授权");
        SimpleAuthorizationInfo info = new SimpleAuthorizationInfo();
        //执行授权
        //拿到当前登录用户对象
        Subject subject = SecurityUtils.getSubject();
        //获取user
        System.out.println(subject.getPrincipal());
        //强制转化为user
        User currentUser = (User) subject.getPrincipal();
        //设置当前用户的权限
        info.addStringPermission(currentUser.getPerms());
        return info;
    }
    //认证
    @Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
        System.out.println("执行了认证");
        /*
        * 获取用户名密码
        * */
        UsernamePasswordToken userToken = (UsernamePasswordToken) token;
        //链接真实数据库
        User user = userService.getUser(userToken.getUsername());
        if(user == null){//没有这个用户
            return null;//抛出异常
        }
        //密码加密   mD5 把密码加密   MD5 盐值加密  无法破解
        //密码认证shiro自己做
        return new SimpleAuthenticationInfo(user,user.getPassword(),"");
    }
}
```

## 25.8 QuickStart

```java
引入quickStart
package com.it.shiro.config;/*
 * Licensed to the Apache Software Foundation (ASF) under one
 * or more contributor license agreements.  See the NOTICE file
 * distributed with this work for additional information
 * regarding copyright ownership.  The ASF licenses this file
 * to you under the Apache License, Version 2.0 (the
 * "License"); you may not use this file except in compliance
 * with the License.  You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing,
 * software distributed under the License is distributed on an
 * "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
 * KIND, either express or implied.  See the License for the
 * specific language governing permissions and limitations
 * under the License.
 */

import org.apache.shiro.SecurityUtils;
import org.apache.shiro.authc.*;
import org.apache.shiro.config.IniSecurityManagerFactory;
import org.apache.shiro.mgt.SecurityManager;
import org.apache.shiro.session.Session;
import org.apache.shiro.subject.Subject;
import org.apache.shiro.util.Factory;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;


/**
 * Simple Quickstart application showing how to use Shiro's API.
 *
 * @since 0.9 RC2
 */
public class Quickstart {

    private static final transient Logger log = LoggerFactory.getLogger(Quickstart.class);


    public static void main(String[] args) {

        // The easiest way to create a Shiro SecurityManager with configured
        // realms, users, roles and permissions is to use the simple INI config.
        // We'll do that by using a factory that can ingest a .ini file and
        // return a SecurityManager instance:

        // Use the shiro.ini file at the root of the classpath
        // (file: and url: prefixes load from files and urls respectively):
        Factory<SecurityManager> factory = new IniSecurityManagerFactory("classpath:shiro.ini");
        SecurityManager securityManager = factory.getInstance();

        // for this simple example quickstart, make the SecurityManager
        // accessible as a JVM singleton.  Most applications wouldn't do this
        // and instead rely on their container configuration or web.xml for
        // webapps.  That is outside the scope of this simple quickstart, so
        // we'll just do the bare minimum so you can continue to get a feel
        // for things.
        SecurityUtils.setSecurityManager(securityManager);

        // Now that a simple Shiro environment is set up, let's see what you can do:

        // get the currently executing user:
        Subject currentUser = SecurityUtils.getSubject();

        // Do some stuff with a Session (no need for a web or EJB container!!!)
        Session session = currentUser.getSession();
        session.setAttribute("someKey", "aValue");
        String value = (String) session.getAttribute("someKey");
        if (value.equals("aValue")) {
            log.info("Retrieved the correct value! [" + value + "]");
        }

        // let's login the current user so we can check against roles and permissions:
        if (!currentUser.isAuthenticated()) {
            UsernamePasswordToken token = new UsernamePasswordToken("lonestarr", "vespa");
            token.setRememberMe(true);
            try {
                currentUser.login(token);
            } catch (UnknownAccountException uae) {
                log.info("There is no user with username of " + token.getPrincipal());
            } catch (IncorrectCredentialsException ice) {
                log.info("Password for account " + token.getPrincipal() + " was incorrect!");
            } catch (LockedAccountException lae) {
                log.info("The account for username " + token.getPrincipal() + " is locked.  " +
                        "Please contact your administrator to unlock it.");
            }
            // ... catch more exceptions here (maybe custom ones specific to your application?
            catch (AuthenticationException ae) {
                //unexpected condition?  error?
            }
        }

        //say who they are:
        //print their identifying principal (in this case, a username):
        log.info("User [" + currentUser.getPrincipal() + "] logged in successfully.");

        //test a role:
        if (currentUser.hasRole("schwartz")) {
            log.info("May the Schwartz be with you!");
        } else {
            log.info("Hello, mere mortal.");
        }

        //test a typed permission (not instance-level)
        if (currentUser.isPermitted("lightsaber:wield")) {
            log.info("You may use a lightsaber ring.  Use it wisely.");
        } else {
            log.info("Sorry, lightsaber rings are for schwartz masters only.");
        }

        //a (very powerful) Instance Level permission:
        if (currentUser.isPermitted("winnebago:drive:eagle5")) {
            log.info("You are permitted to 'drive' the winnebago with license plate (id) 'eagle5'.  " +
                    "Here are the keys - have fun!");
        } else {
            log.info("Sorry, you aren't allowed to drive the 'eagle5' winnebago!");
        }

        //all done - log out!
        currentUser.logout();

        System.exit(0);
    }
}

```

## 25.9配置controller

```java
package com.it.shiro.controller;

import org.apache.shiro.SecurityUtils;
import org.apache.shiro.authc.IncorrectCredentialsException;
import org.apache.shiro.authc.UnknownAccountException;
import org.apache.shiro.authc.UsernamePasswordToken;
import org.apache.shiro.subject.Subject;
import org.springframework.stereotype.Repository;
import org.springframework.web.bind.annotation.*;

@RestController
@CrossOrigin(origins = "*",maxAge = 3600)
public class LoginController {
    @GetMapping("/login")
    public String Login(String username,String password){
        //获取当前用户
        Subject subject = SecurityUtils.getSubject();
        //封装用户的登录数据
        UsernamePasswordToken token = new UsernamePasswordToken(username,password);
        try {
            subject.login(token);//执行登录方法，没有异常jiu ok
            return "登录成功";
        }catch (UnknownAccountException e){
            return "用户不存在";
        }catch (IncorrectCredentialsException e){
            return "密码错误";
        }
    }

    @GetMapping("/add")
    public String add(){
        return "增加";
    }

    @GetMapping("/del")
    public String del(){
        return "删除";
    }

    //未授权跳转
    @RequestMapping("/noauth")
    @ResponseBody
    public String Unauthorized(){
        return "未经授权无法范访问此页面";
    }
}
```



# 26.Swagger

## 26.1导入依赖

```java
1.导入依赖
	        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger2</artifactId>
            <version>2.7.0</version>
        </dependency>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger-ui</artifactId>
            <version>2.7.0</version>
        </dependency>
```

## 26.2 Swagger的配置类

```java
2.swagger的configuration
@Configuration
@EnableSwagger2
public class SwaggerConfig extends WebMvcConfigurationSupport {

    @Bean
    public Docket productApi() {
        return new Docket(DocumentationType.SWAGGER_2).select()
                // 扫描的包路径
                .apis(RequestHandlerSelectors.basePackage("com.it.shiro.controller"))
                // 定义要生成文档的Api的url路径规则
                .paths(PathSelectors.any())
                .build()
                // 设置swagger-ui.html页面上的一些元素信息。
                .apiInfo(metaData());
    }
    private ApiInfo metaData() {
        return new ApiInfoBuilder()
                // 标题
                .title("SpringBoot集成Swagger2")
                // 描述
                .description("这是一篇博客演示")
                // 文档版本
                .version("1.0.0")
                .license("Apache License Version 2.0")
                .licenseUrl("https://www.apache.org/licenses/LICENSE-2.0")
                .build();
    }

    @Override
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("swagger-ui.html")
                .addResourceLocations("classpath:/META-INF/resources/");

        registry.addResourceHandler("/webjars/**")
                .addResourceLocations("classpath:/META-INF/resources/webjars/");
    }
}
```

## 26.3在Api上进行申明

```java
@Api
	描述controller类
	tags = "" // 描述此controller类
@ApiOperation  描述一个方法或者一个API接口 
	value = "" // 描述方法
	notes = "" // 描述方法详细信息
@ApiParam，对API参数的描述。
		
@ApiImplicitParams
		功能:汇集多个参数
		注解位置: 方法
		@ApiImplicitParam组成的列表
		
		
 @ApiModelProperty(value="用户id",name="id",required=true)
 		用来描述实体类属性的
 		
 		
Bean实体类
	@Data
	@ApiModel
	public class User implements Serializable {
    @ApiModelProperty(value = "用户id")
    private Integer id;
    @ApiModelProperty(value = "用户名")
    private String username;
    @ApiModelProperty(value = "密码")
    private String password;
    @ApiModelProperty(value = "权限")
    private String perms;
}
```

## 26.4访问页面查看

```java
设定访问API doc的路由

springfox.documentation.swagger.v2.path: /api-docs

API doc的显示路由是：<http://localhost:8080/swagger-ui.html>
```





# 28.热部署

```java
1.导入jar包
	<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
2.配置文件
    #热部署生效
    spring.devtools.restart.enabled: true
    #设置重启的目录
    spring.devtools.restart.additional-paths: src/main/java
    #classpath目录下的WEB-INF文件夹内容修改不重启
    spring.devtools.restart.exclude: WEB-INF/**
    
 3.IDEA配置
当我们修改了Java类后，IDEA默认是不自动编译的，而spring-boot-devtools又是监测classpath下的文件发生变化才会重启应用，所以需要设置IDEA的自动编译：
（1）File-Settings-Compiler-Build Project automatically
（2）ctrl + shift + alt + /,选择Registry,勾上 Compiler autoMake allow when app running
```

# 29.配置druid

```java
<dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.0.18</version>
        </dependency>
        
        
  配置文件 
  spring:
  ##数据库连接信息
  datasource:
    url: jdbc:mysql://localhost:3306/shiro
    username: root
    password: lzxs@root123456
    driver-class-name: com.mysql.jdbc.Driver
    ###################以下为druid增加的配置###########################
    type: com.alibaba.druid.pool.DruidDataSource
    # 下面为连接池的补充设置，应用到上面所有数据源中
    # 初始化大小，最小，最大
    initialSize: 5
    minIdle: 5
    maxActive: 20
    # 配置获取连接等待超时的时间
    maxWait: 60000
    # 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒
    timeBetweenEvictionRunsMillis: 60000
    # 配置一个连接在池中最小生存的时间，单位是毫秒
    minEvictableIdleTimeMillis: 300000
    validationQuery: SELECT 1 FROM DUAL
    testWhileIdle: true
    testOnBorrow: false
    testOnReturn: false
    # 打开PSCache，并且指定每个连接上PSCache的大小
    poolPreparedStatements: true
    maxPoolPreparedStatementPerConnectionSize: 20
    # 配置监控统计拦截的filters，去掉后监控界面sql无法统计，'wall'用于防火墙
    filters: stat,wall,log4j
    # 通过connectProperties属性来打开mergeSql功能；慢SQL记录
    connectionProperties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=5000
    # 合并多个DruidDataSource的监控数据
    useGlobalDataSourceStat: true
    ###############以上为配置druid添加的配置########################################
    
    
   	public class DruidDataSource {
    @ConfigurationProperties(prefix = "spring.datasource")
    @Bean
    public DruidDataSource druidDataSource(){
        return new DruidDataSource();
    }

    /**
     * 配置监控服务器
     * @return 返回监控注册的servlet对象
     * @author SimpleWu
     */
    @Bean
    public ServletRegistrationBean statViewServlet() {
        ServletRegistrationBean servletRegistrationBean = new ServletRegistrationBean(new StatViewServlet(), "/druid/*");
        // 添加IP白名单
        servletRegistrationBean.addInitParameter("allow", "127.0.0.1");
        // 添加IP黑名单，当白名单和黑名单重复时，黑名单优先级更高
        servletRegistrationBean.addInitParameter("deny", "127.0.0.1");
        // 添加控制台管理用户
        servletRegistrationBean.addInitParameter("loginUsername", "SimpleWu");
        servletRegistrationBean.addInitParameter("loginPassword", "123456");
        // 是否能够重置数据
        servletRegistrationBean.addInitParameter("resetEnable", "false");
        return servletRegistrationBean;
    }
    /**
     * 配置服务过滤器
     *
     * @return 返回过滤器配置对象
     */
    @Bean
    public FilterRegistrationBean statFilter() {
        FilterRegistrationBean filterRegistrationBean = new FilterRegistrationBean(new WebStatFilter());
        // 添加过滤规则
        filterRegistrationBean.addUrlPatterns("/*");
        // 忽略过滤格式
        filterRegistrationBean.addInitParameter("exclusions", "*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*,");
        return filterRegistrationBean;
    }
}
```

# 30.Lombok

```java
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.10</version>
</dependency>

@Data最常用的注解之一。注解在类上，提供该类所有属性的getter/setter方法，还提供了equals、canEqual、hashCode、toString方法。

@Log4j
作用于类上，为该类提供一个属性名为log的log4j日志对象。

@AllArgsConstructor
作用于类上，为该类提供一个包含全部参的构造方法，注意此时默认构造方法不会提供。

@NoArgsConstructor
作用于类上，提供一个无参的构造方法。可以和@AllArgsConstructor同时使用，此时会生成两个构造方法：无参构造方法和全参构造方法。


@EqualsAndHashCode
作用于类上，生成equals、canEqual、hashCode方法

@NonNull
作用于属性上，提供关于此参数的非空检查，如果参数为空，则抛出空指针异常。

@Cleanup
作用于变量，保证该变量代表的资源会被自动关闭，默认调用资源的close()方法，如果该资源有其它关闭方法，可使用@Cleanup(“methodName”)来指定。

@SneakyThrows
作用于方法上，相当于把方法内的代码添加了一个try-catch处理，捕获异常catch中用Lombok.sneakyThrow(e)抛出异常。使用@SneakyThrows(BizException.class)指定抛出具体异常。


@Synchronized
作用于类方法或实例方法上，效果与synchronized相同。区别在于锁对象不同，对于类方法和实例方法，synchronized关键字的锁对象分别是类的class对象和this对象，而@Synchronized的锁对象分别是私有静态final对象lock和私有final对象lock。也可以指定锁对象。
```

# 31.SQL查询

```java
查询角色权限
SELECT a.username,ur.role_id,r.role_name,p.perms FROM user a
LEFT JOIN user_role ur on a.id = ur.user_id
LEFT JOIN role r on ur.user_id = r.role_id
LEFT JOIN role_perms rp on rp.role_id = ur.role_id 
LEFT JOIN permission p on p.perms_id = rp.perms_id
WHERE r.role_id = 2
```

# 32.MyBatis plus

```java
//entity  实体类
@Data
public class User {
    private Long id;
    private String name;
    private Integer age;
    private String email;
}
//mapper接口继承basemapper
@Repository
public interface UserMapper extends BaseMapper<User> {
}

//查看sql输出日志
#查看sql输出日志
mybatis-plus.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl

 	
    
//修改主键生成策略
	@TableId(type = IdType.AUTO)
    private Long id;
```

## 32.1基本操作

```java
/**
     * 查询
     */
    @Test
    public void findall() {
        List<User> users = userMapper.selectList(null);
        System.out.println(users);
    }
    
	//增加
	@Test
    public void add(){
        User user = new User();
        user.setAge(11);
        user.setEmail("1213@qq.com");
        user.setName("zhang");
//        id mp 自动生成
        userMapper.insert(user);
    }
	/**
     * 修改
     */
    @Test
    public  void update(){
        User user = new User();
        user.setId(2L);//L表示长类型
        user.setAge(120);
        userMapper.updateById(user);
    }
    
    //mp  主键生成策略
```

## 32.2自动填充

```java
1.在需要自动填充的实体类上面加上注解
    @TableField(fill = FieldFill.INSERT)
    private Date createTime;

    @TableField(fill = FieldFill.INSERT_UPDATE)
    private Date updateTime;
2.创建类实现接口
    @Component
    public class MyMetaObjectHandler implements MetaObjectHandler {
        //insert方法
        @Override
        public void insertFill(MetaObject metaObject) {
            this.setFieldValByName("createTime",new Date(),metaObject);
            this.setFieldValByName("updateTime",new Date(),metaObject);
        }
        //更新方法
        @Override
        public void updateFill(MetaObject metaObject) {
            this.setFieldValByName("updateTime",new Date(),metaObject);
        }
    }
```

## 32.3乐观锁

```java
主要解决丢失更新
如果不考虑事务隔离性 产生读的问题\
//脏读 不可重复读 幻读
丢失更新问题 
多人同时修改同一条记录，最后提交数据会把之前的覆盖掉

//解决方案 
1.悲观锁
	
2.乐观锁
	//实体类属性
	@TableField(fill = FieldFill.INSERT)
    @Version
    private Integer version;

	//配置类
	@Configuration
    @MapperScan("com.example.mpdemo1.mapper")
    public class Mpconfig {

        /**
         * 乐观锁插件
         * @return
         */
        @Bean
        public OptimisticLockerInterceptor optimisticLockerInterceptor() {
            return new OptimisticLockerInterceptor();
        }
    }

	//自动填充配置
	@Component
    public class MyMetaObjectHandler implements MetaObjectHandler {
        //insert方法
        @Override
        public void insertFill(MetaObject metaObject) {
            this.setFieldValByName("createTime",new Date(),metaObject);
            this.setFieldValByName("updateTime",new Date(),metaObject);
            this.setFieldValByName("version",1,metaObject);
        }
        //更新方法
        @Override
        public void updateFill(MetaObject metaObject) {
            this.setFieldValByName("updateTime",new Date(),metaObject);
        }
    }

	//单id查询
	@Test
    public  void testlegaunsuo(){
        User user1 = userMapper.selectById(1318836641189916674L);
        user1.setAge(150);
        userMapper.updateById(user1);
    }
```

## 32.4map查询

```java
 	@Test
    public  void TestSelectBatch(){
        HashMap<String, Object> map = new HashMap<>();
        map.put("name","dsa");
//        map.put("age",11);
        List<User> users = userMapper.selectByMap(map);
        System.out.println(users);
    }

	//用来查询AND 满足两个条件
```

## 32.5分页

```java
	//配置类
	/**
     * 分页插件
     * @return
     */
    @Bean
    public PaginationInterceptor paginationInterceptor(){
        return new PaginationInterceptor();
    }

 	@Test
    public void PageSelect(){
        Page<User> page = new Page<>(1, 3);
        userMapper.selectPage(page,null);
        System.out.println(page.getCurrent());//当前页
        System.out.println(page.getRecords());//数据集合List
        System.out.println(page.getSize());//显示记录数
        System.out.println(page.getTotal());//总记录数
        System.out.println(page.getPages());//总页数
        System.out.println(page.hasNext());//是否有下一页
        System.out.println(page.hasPrevious());//是否有上一页
    }
```

## 32.6删除

```java
逻辑删除和物理删除
//物理删除
	 /**
     * 物理删除
     */
    @Test
    public void delete1(){
        int i = userMapper.deleteById(1L);
        System.out.println(i);
    }
//逻辑删除
	//3.05版本
	/**
     * 逻辑删除
     */
    @TableLogic
    @TableField(fill = FieldFill.INSERT)
    private Integer deleted;

	/**\
     * 逻辑删除
     */
    @Bean
    public ISqlInjector sqlInjector() {
        return new LogicSqlInjector();
    }

	/**
     * 物理删除
     */
    @Test
    public void delete2(){
        int i = userMapper.deleteById(1319156625164599297L);
        System.out.println(i);
    }
```

## 32.7性能分析

```
@Bean
@Profile({"dev","test"})//设置dev test环境开启
    public PerformanceInterceptor performanceInterceptor() {
    PerformanceInterceptor performanceInterceptor = new PerformanceInterceptor();
    performanceInterceptor.setMaxTime(100);
    performanceInterceptor.setFormat(true);
    return performanceInterceptor;
}


// 环境 prod test prod
//spring.profiles.active=dev

	
```

## 32.8复杂查询

```java
//使用QueryWrapper构建复杂查询
	/**
     * 条件查询
     */
    @Test
    public void queryUnion(){
        //创建QueryWrapper
        QueryWrapper<User> wrapper = new QueryWrapper<>();
        //设置条件
        //ge,gt,le,lt  大于 小于 大于等于 小于等
        wrapper.ge("age", 30);
        List<User> users = userMapper.selectList(wrapper);
        System.out.println(users);

        //eq 等去  ne  不等于
        wrapper.eq("age", 110);
        List<User> users1 = userMapper.selectList(wrapper);
        System.out.println(users1);
        //between
        wrapper.between("age", 30,110);
        List<User> users2 = userMapper.selectList(wrapper);
        System.out.println(users2);
        //like 模糊查询
        wrapper.like("name", "a");
        List<User> users3 = userMapper.selectList(wrapper);
        System.out.println(users3);
        //orderBy 升序降序
        wrapper.orderByDesc("id");
        //last 拼接
        //拼接sql语句
        wrapper.last("limit 1");

        //查询指定列
        wrapper.select("id","name");
    }
```

