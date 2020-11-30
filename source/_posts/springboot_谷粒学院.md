---
title: SpringBoot
date:
updated:
type: "tags"
comments:
categories: Java
description: SpringBoot
keywords: SpringBoot
top_img: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=848518668,3095786482&fm=26&gp=0.jpg
cover: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=848518668,3095786482&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.项目技术总结

```
项目采用前后端分离开发

//后端技术 
	springboot 
	springcloud
    MybatisPlus
    sping security 
    redis
    maven
    easyExcel
    jwt
    Oauth2
//前端技术
	vue + element UI + axios + node js
//其他技术
	阿里云oss
	阿里云视频点播服务
	阿里月短信服务
	微信支付和登录
	docker
	git
	jenkins
```



# 3.主键生成策略

```
1.自动增长
	Auto_increment  有序
2.UUID
	每次生成随机的值  无序性
3.Redis生成ID
	原子操作 五台redis初始值为12345，步长为5 生成后就是1-25
4.mybatis-plus twitter 开源雪花算法
	默认策略
	//修改主键生成策略
	@TableId(type = IdType.AUTO)
    private Long id;
```

# 4.开始实践项目

```java
//项目结构
	//创建父工程  Pom类型 管理依赖版本和公共依赖  spingboot工程
	//子模块一	maven工程
		//子子模块1	maven工程
		//子子模块2
	//子模块二

```

## 4.1修改POM

```xml
//POM 文件 
		//springboot版本  <version>2.2.1.RELEASE</version>
		//表示当前类型为pom
		//<artifactId>guli_parent</artifactId>
    	//<packaging>pom</packaging>

//删除掉父工程的 dependencies


//管理版本
 <properties>
        <java.version>1.8</java.version>
        <guli.version>0.0.1-SNAPSHOT</guli.version>
        <mybatis-plus.version>3.3.2</mybatis-plus.version>
        <velocity.version>2.0</velocity.version>
        <swagger.version>2.9.2</swagger.version>
        <aliyun.oss.version>3.10.0</aliyun.oss.version>
        <jodatime.version>2.10.6</jodatime.version>
        <poi.version>4.1.2</poi.version>
        <commons-fileupload.version>1.4</commons-fileupload.version>
        <commons-io.version>2.7</commons-io.version>
        <httpclient.version>4.5.12</httpclient.version>
        <jwt.version>0.9.1</jwt.version>
        <aliyun-java-sdk-core.version>4.5.2</aliyun-java-sdk-core.version>
        <aliyun-sdk-oss.version>3.1.0</aliyun-sdk-oss.version>
        <aliyun-java-sdk-vod.version>2.15.9</aliyun-java-sdk-vod.version>
        <aliyun-java-vod-upload.version>1.4.12</aliyun-java-vod-upload.version>
        <aliyun-sdk-vod-upload.version>1.4.12</aliyun-sdk-vod-upload.version>
        <fastjson.version>1.2.71</fastjson.version>
        <gson.version>2.8.2</gson.version>
        <json.version>20170516</json.version>
        <commons-dbutils.version>1.7</commons-dbutils.version>
        <canal.client.version>1.1.4</canal.client.version>
        <docker.image.prefix>zx</docker.image.prefix>
        <cloud-alibaba.version>0.2.2.RELEASE</cloud-alibaba.version>
        <swagger-version>2.0.3</swagger-version>
        <project-version>0.0.1-SNAPSHOT</project-version>
        <hutool-version>5.3.7</hutool-version>
        <nacos.version>0.9.0.RELEASE</nacos.version>
    </properties>
 
//锁定版本
         <dependencyManagement>
        <dependencies>
            <!--Spring Cloud-->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>Hoxton.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>

            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>${cloud-alibaba.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <!--mybatis-plus 持久层-->
            <dependency>
                <groupId>com.baomidou</groupId>
                <artifactId>mybatis-plus-boot-starter</artifactId>
                <version>${mybatis-plus.version}</version>
            </dependency>

            <!-- velocity 模板引擎, Mybatis Plus 代码生成器需要 -->
            <dependency>
                <groupId>org.apache.velocity</groupId>
                <artifactId>velocity-engine-core</artifactId>
                <version>${velocity.version}</version>
            </dependency>

            <!--swagger-->
            <dependency>
                <groupId>io.springfox</groupId>
                <artifactId>springfox-swagger2</artifactId>
                <version>${swagger.version}</version>
            </dependency>
            <!--swagger ui-->
            <dependency>
                <groupId>io.springfox</groupId>
                <artifactId>springfox-swagger-ui</artifactId>
                <version>${swagger.version}</version>
            </dependency>

            <!--aliyunOSS-->
            <dependency>
                <groupId>com.aliyun.oss</groupId>
                <artifactId>aliyun-sdk-oss</artifactId>
                <version>${aliyun.oss.version}</version>
            </dependency>

            <!--日期时间工具-->
            <dependency>
                <groupId>joda-time</groupId>
                <artifactId>joda-time</artifactId>
                <version>${jodatime.version}</version>
            </dependency>

            <!--xls-->
            <dependency>
                <groupId>org.apache.poi</groupId>
                <artifactId>poi</artifactId>
                <version>${poi.version}</version>
            </dependency>
            <!--xlsx-->
            <dependency>
                <groupId>org.apache.poi</groupId>
                <artifactId>poi-ooxml</artifactId>
                <version>${poi.version}</version>
            </dependency>

            <!--文件上传-->
            <dependency>
                <groupId>commons-fileupload</groupId>
                <artifactId>commons-fileupload</artifactId>
                <version>${commons-fileupload.version}</version>
            </dependency>

            <!--commons-io-->
            <dependency>
                <groupId>commons-io</groupId>
                <artifactId>commons-io</artifactId>
                <version>${commons-io.version}</version>
            </dependency>

            <!--httpclient-->
            <dependency>
                <groupId>org.apache.httpcomponents</groupId>
                <artifactId>httpclient</artifactId>
                <version>${httpclient.version}</version>
            </dependency>

            <dependency>
                <groupId>com.google.code.gson</groupId>
                <artifactId>gson</artifactId>
                <version>${gson.version}</version>
            </dependency>

            <!-- JWT -->
            <dependency>
                <groupId>io.jsonwebtoken</groupId>
                <artifactId>jjwt</artifactId>
                <version>${jwt.version}</version>
            </dependency>

            <!--aliyun-->
            <dependency>
                <groupId>com.aliyun</groupId>
                <artifactId>aliyun-java-sdk-core</artifactId>
                <version>${aliyun-java-sdk-core.version}</version>
            </dependency>
            <dependency>
                <groupId>com.aliyun.oss</groupId>
                <artifactId>aliyun-sdk-oss</artifactId>
                <version>${aliyun-sdk-oss.version}</version>
            </dependency>
            <dependency>
                <groupId>com.aliyun</groupId>
                <artifactId>aliyun-java-sdk-vod</artifactId>
                <version>${aliyun-java-sdk-vod.version}</version>
            </dependency>
            <dependency>
                <groupId>com.aliyun</groupId>
                <artifactId>aliyun-java-vod-upload</artifactId>
                <version>${aliyun-java-vod-upload.version}</version>
            </dependency>
            <dependency>
                <groupId>com.aliyun</groupId>
                <artifactId>aliyun-sdk-vod-upload</artifactId>
                <version>${aliyun-sdk-vod-upload.version}</version>
            </dependency>
            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>fastjson</artifactId>
                <version>${fastjson.version}</version>
            </dependency>
            <dependency>
                <groupId>org.json</groupId>
                <artifactId>json</artifactId>
                <version>${json.version}</version>
            </dependency>

            <dependency>
                <groupId>commons-dbutils</groupId>
                <artifactId>commons-dbutils</artifactId>
                <version>${commons-dbutils.version}</version>
            </dependency>

            <dependency>
                <groupId>com.alibaba.otter</groupId>
                <artifactId>canal.client</artifactId>
                <version>${canal.client.version}</version>
            </dependency>
        </dependencies>
    </dependencyManagement>

```

## 4.2调整创建子模块

```xml
//删除掉 src
//新建子模块
	子模块模式设置成POM	
	<packaging>pom</packaging>
	//删除src
    <dependencies>

        <dependency>
            <groupId>com.example</groupId>
            <artifactId>service</artifactId>
            <version>0.0.1-SNAPSHOT</version>
        </dependency>

        <!--<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-ribbon</artifactId>
        </dependency>-->

        <!--hystrix依赖，主要是用  @HystrixCommand -->
        <!--<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
        </dependency>-->

        <!--服务注册-->
        <!-- <dependency>
             <groupId>org.springframework.cloud</groupId>
             <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
         </dependency>-->
        <!--服务调用-->
        <!-- <dependency>
             <groupId>org.springframework.cloud</groupId>
             <artifactId>spring-cloud-starter-openfeign</artifactId>
         </dependency>-->

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!--mybatis-plus-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
        </dependency>

        <!--mysql-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>

        <!-- velocity 模板引擎, Mybatis Plus 代码生成器需要 -->
        <dependency>
            <groupId>org.apache.velocity</groupId>
            <artifactId>velocity-engine-core</artifactId>
        </dependency>

        <!--swagger-->
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger2</artifactId>
        </dependency>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger-ui</artifactId>
        </dependency>

        <!--lombok用来简化实体类：需要安装lombok插件-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>

        <!--xls-->
        <dependency>
            <groupId>org.apache.poi</groupId>
            <artifactId>poi</artifactId>
        </dependency>

        <dependency>
            <groupId>org.apache.poi</groupId>
            <artifactId>poi-ooxml</artifactId>
        </dependency>

        <dependency>
            <groupId>commons-fileupload</groupId>
            <artifactId>commons-fileupload</artifactId>
        </dependency>

        <!--httpclient-->
        <dependency>
            <groupId>org.apache.httpcomponents</groupId>
            <artifactId>httpclient</artifactId>
        </dependency>
        <!--commons-io-->
        <dependency>
            <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
        </dependency>
        <!--gson-->
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
        </dependency>

        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>


```

```properties
//application.properties
# 服务端口
server.port=8001
# 服务名
spring.application.name=service-edu

# 环境设置 dev test prod
spring.profiles.active=dev

# mysql数据库丽链接
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/guli?serverTimezone=GMT%2B8&characterEncoding=UTF8
spring.datasource.username=root
spring.datasource.password=root

#json解析时间
spring.jackson.date-format=yyyy-MM-dd HH:mm:ss
spring.jackson.time-zone=GMT+8

#mybatis日志
mybatis-plus.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
```

## 4.3 mp代码生成

```java
//gengrator.java
package com.guli.demo;

import com.baomidou.mybatisplus.annotation.DbType;
import com.baomidou.mybatisplus.annotation.IdType;
import com.baomidou.mybatisplus.generator.AutoGenerator;
import com.baomidou.mybatisplus.generator.config.DataSourceConfig;
import com.baomidou.mybatisplus.generator.config.GlobalConfig;
import com.baomidou.mybatisplus.generator.config.PackageConfig;
import com.baomidou.mybatisplus.generator.config.StrategyConfig;
import com.baomidou.mybatisplus.generator.config.rules.DateType;
import com.baomidou.mybatisplus.generator.config.rules.NamingStrategy;
import org.junit.Test;

/**
 * @author
 * @since 2018/12/13
 */
public class CodeGenerator {

    @Test
    public void run() {

        // 1、创建代码生成器
        AutoGenerator mpg = new AutoGenerator();

        // 2、全局配置
        GlobalConfig gc = new GlobalConfig();
        //获取路径
        String projectPath = System.getProperty("user.dir");
        gc.setOutputDir("E:\\java_pro\\service\\service_edu" + "/src/main/java");

        gc.setAuthor("mikasa");
        gc.setOpen(false); //生成后是否打开资源管理器
        gc.setFileOverride(false); //重新生成时文件是否覆盖

        //UserServie
        gc.setServiceName("%sService");	//去掉Service接口的首字母I

        gc.setIdType(IdType.ID_WORKER_STR); //主键策略
        gc.setDateType(DateType.ONLY_DATE);//定义生成的实体类中日期类型
        gc.setSwagger2(true);//开启Swagger2模式

        mpg.setGlobalConfig(gc);

        // 3、数据源配置
        DataSourceConfig dsc = new DataSourceConfig();
        dsc.setUrl("jdbc:mysql://localhost:3306/guli?serverTimezone=GMT%2B8");
        dsc.setDriverName("com.mysql.cj.jdbc.Driver");
        dsc.setUsername("root");
        dsc.setPassword("123456");
        dsc.setDbType(DbType.MYSQL);
        mpg.setDataSource(dsc);

        // 4、包配置
        PackageConfig pc = new PackageConfig();
        pc.setModuleName("eduservice"); //模块名
        //包  com.atguigu.eduservice
        pc.setParent("com.example");
        //包  com.atguigu.eduservice.controller
        pc.setController("controller");
        pc.setEntity("entity");
        pc.setService("service");
        pc.setMapper("mapper");
        mpg.setPackageInfo(pc);

        // 5、策略配置
        StrategyConfig strategy = new StrategyConfig();

        //表名称
        strategy.setInclude("edu_teacher");

        strategy.setNaming(NamingStrategy.underline_to_camel);//数据库表映射到实体的命名策略
        strategy.setTablePrefix(pc.getModuleName() + "_"); //生成实体时去掉表前缀

        strategy.setColumnNaming(NamingStrategy.underline_to_camel);//数据库表字段映射到实体的命名策略
        strategy.setEntityLombokModel(true); // lombok 模型 @Accessors(chain = true) setter链式操作

        strategy.setRestControllerStyle(true); //restful api风格控制器
        strategy.setControllerMappingHyphenStyle(true); //url中驼峰转连字符

        mpg.setStrategy(strategy);


        // 6、执行
        mpg.execute();
    }
}

```

```xml
//引入相关依赖
<dependency>
	<groupId>com.baomidou</groupId>
	<artifactId>mybatis-plus-boot-starter</artifactId>
</dependency>

<dependency>
	<groupId>com.baomidou</groupId>
	<artifactId>mybatis-plus-generator</artifactId>
	<version>3.3.2</version>
</dependency>
```

## 4.4创建启动类配置类

```java
@SpringBootApplication
public class EduApplication {
    public static void main(String[] args) {
        SpringApplication.run(EduApplication.class,args);
    }
}

//创建子模块配置类
```

## 4.5修改时区显示

```properties
#json解析时间
spring.jackson.date-format=yyyy-MM-dd HH:mm:ss
spring.jackson.time-zone=GMT+8
```

## 4.6逻辑删除

```java
	@DeleteMapping("{id}")
    public Boolean removeTeacher(@PathVariable String id){
        boolean flag = eduTeacherService.removeById(id);
        return flag;
    }
```

## 4.7配置Swagger测试

```java
//创建公共模块
//common模块
    


@Configuration
@EnableSwagger2
public class SwaggerConfig {
    @Bean
    public Docket webApiConfig() {
        return new Docket(DocumentationType.SWAGGER_2)
                .groupName("webApi")//名称
                .apiInfo(webApiInfo())//接口信息
                .select()
                .paths(Predicates.not(PathSelectors.regex("/admin/.*")))//包含匹配
                .paths(Predicates.not(PathSelectors.regex("/error.*")))//
                .build();
    }
    private ApiInfo webApiInfo() {
        return new ApiInfoBuilder()
                // 标题
                .title("古粒-课程中心Api文档")
                // 描述
                .description("描述了课程中心微服务定义接口")
                // 文档版本
                .version("1.0.0")
                .build();
    }
}
```

xml配置

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <scope>provided </scope>
        </dependency>

        <!--mybatis-plus-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <scope>provided </scope>
        </dependency>

        <!--lombok用来简化实体类：需要安装lombok插件-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <scope>provided </scope>
        </dependency>

        <!--swagger-->

        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger2</artifactId>
            <scope>provided </scope>
        </dependency>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger-ui</artifactId>
            <scope>provided </scope>
        </dependency>

        <!-- redis -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>

        <!-- spring2.X集成redis所需common-pool2
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
            <version>2.6.0</version>
        </dependency>-->
    </dependencies>
```

在Service使用

```xml
 <!--        引入common依赖-->
        <dependency>
            <groupId>com.example</groupId>
            <artifactId>service_base</artifactId>
            <version>0.0.1-SNAPSHOT</version>
        </dependency>


```

//启动类设置扫描规则

```java
@SpringBootApplication
@ComponentScan(basePackages = {"com.guli"})//扫描common配置类
public class EduApplication {
    public static void main(String[] args) {
        SpringApplication.run(EduApplication.class,args);
    }
}

http://localhost:8001/swagger-ui.html  访问

注意包名配置一样
```



## 4.8多条件分页查询

```java
//entity新建传入参数 得实体类
@Data
public class TeacherQuery {

    @ApiModelProperty(value = "教师查询，模糊查询")
    private String name;

    @ApiModelProperty(value = "头衔 1高级讲师 2首席讲师")
    private Integer level;

    @ApiModelProperty(value = "查询开始时间",example = "2019-01-01 10:10:10")
    private String begin;

    @ApiModelProperty(value = "查询结束时间",example = "2019-01-01 10:10:10")
    private String end;
}

//controller
 /**
     * 多条件组合分页查询
     */
    @GetMapping("pageTeacherCondition/{currentPage}/{pageSize}")
    public R pageTeacherCondition(@PathVariable long currentPage,@PathVariable long pageSize,TeacherQuery teacherQuery){
        Page<EduTeacher> page = new Page<>(currentPage,pageSize);
        QueryWrapper<EduTeacher> wrapper = new QueryWrapper<>();
        //动态sql
        String name = teacherQuery.getName();
        Integer level = teacherQuery.getLevel();
        String begin = teacherQuery.getBegin();
        String end = teacherQuery.getEnd();
        if(!StringUtils.isEmpty(name)){
            wrapper.like("name",name);
        }
        if(!StringUtils.isEmpty(level)){
            wrapper.eq("level",level);
        }
        if(!StringUtils.isEmpty(begin)){
            wrapper.ge("gmt_create",begin);
        }
        if(!StringUtils.isEmpty(end)){
            wrapper.le("gmt_create",end);
        }

        eduTeacherService.page(page,wrapper);
        long total = page.getTotal();
        List<EduTeacher> records = page.getRecords();
        return R.ok().data("total",total).data("records",records);
    }

```

# 5.统一返回数据格式

```
格式
	{
        "success":布尔，
        “code”：数字,
        "message":字符串,
        "data":Hashmap
	}
```

```java
创建子模块 common-utils

创建interface,定义数据返回码
public interface ResultCode {
    public static Integer SUCCESS = 200;
    public static Integer ERROR = 200;
}

//创建返回类
/**
 * 统一返回结果
 */
@Data
public class R {

    @ApiModelProperty(value = "是否成功")
    private Boolean success;

    @ApiModelProperty(value = "返回码")
    private Integer code;

    @ApiModelProperty(value = "返回消息")
    private String message;

    @ApiModelProperty(value = "返回数据")
    private Map<String,Object> data = new HashMap<String,Object>();

    //把构造方法私有
    private R(){}

    //静态方法
    public static R ok(){
        R r = new R();
        r.setSuccess(true);
        r.setCode(ResultCode.SUCCESS);
        r.setMessage("成功");
        return r;
    }

    public static R error(){
        R r = new R();
        r.setSuccess(false);
        r.setCode(ResultCode.ERROR);
        r.setMessage("失败");
        return r;
    }

    public R success(Boolean success){
        this.setSuccess(success);
        return this;
    }

    public R message(String message){
        this.setMessage(message);
        return this;
    }

    public R code(Integer code){
        this.setCode(code);
        return this;
    }

    public R data(Map<String,Object> map){
        this.setData(map);
        return this;
    }

    public R data(String key,Object value){
        this.data.put(key, value);
        return this;
    }
}
```

```xml
//使用
 <dependency>
 	<groupId>com.example</groupId>
 	<artifactId>common_utils</artifactId>
 	<version>0.0.1-SNAPSHOT</version>
 </dependency>
```

调用

```java
public R findAllData(){
        List<EduTeacher> list = eduTeacherService.list(null);
        return R.ok().data("items",list).code(200).message("成功");
 }
```

# 6.异常处理

```json
{
  "timestamp": "2020-10-26 09:53:00",
  "status": 500,
  "error": "Internal Server Error",
  "message": "/ by zero",
  "path": "/eduservice/teacher/findAll"
}
```

## 6.1全局异常处理类

```java
@ControllerAdvice//异常抛到controller
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)//捕捉异常
    @ResponseBody//返回数据
    public R error(Exception e){
        e.printStackTrace();
        return R.error().message("执行了全局异常处理");
    }
}
```

## 6.2特定异常处理

```java
/**
     * 特定异常处理
     * @param e
     * @return
     */
    @ExceptionHandler(ArithmeticException.class)//捕捉异常
    @ResponseBody//返回数据
    public R error(ArithmeticException e){
        e.printStackTrace();
        return R.error().message("执行了ArithmeticException异常");
    }

	{
      "success": false,
      "code": 500,
      "message": "执行了ArithmeticException异常",
      "data": {}
    }
```

## 6.3自定义异常处理

```java
@Data
@AllArgsConstructor//生成有参构造方法
@NoArgsConstructor//无参数构造方法
public class GuliExecption extends RuntimeException {

    private Integer code;

    private String msg;

}

//全局异常处理
	/**
     * 自定义异常类
     */
    @ExceptionHandler(GuliExecption.class)//捕捉异常
    @ResponseBody//返回数据
    public R error(GuliExecption e){
        e.printStackTrace();
        return R.error().code(e.getCode()).message(e.getMsg());
    }


```

调用

```java
try{
	int a = 30/0;
}catch (Exception e){
	//执行自定义异常
	throw new GuliExecption(505,"执行了自定义异常");
}
```

# 7.日志处理(logback)

```java
//配置日志级别
//日志记录器分为一下级别
//OFF,FATAL,ERROR,WARN,INFO,DEBUG,ALL

#日志级别
logging.level.root=WARN
```

## 7.1配置

```yml
清除以前的日志配置
#mybatis日志
#mybatis-plus.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl

#日志级别
#logging.level.root=WARN


彩色日志插件
	grep-console
resources创建logback-spring.xml

```

logback-spring.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration  scan="true" scanPeriod="10 seconds">
    <!-- 日志级别从低到高分为TRACE < DEBUG < INFO < WARN < ERROR < FATAL，如果设置为WARN，则低于WARN的信息都不会输出 -->
    <!-- scan:当此属性设置为true时，配置文件如果发生改变，将会被重新加载，默认值为true -->
    <!-- scanPeriod:设置监测配置文件是否有修改的时间间隔，如果没有给出时间单位，默认单位是毫秒。当scan为true时，此属性生效。默认的时间间隔为1分钟。 -->
    <!-- debug:当此属性设置为true时，将打印出logback内部日志信息，实时查看logback运行状态。默认值为false。 -->

    <contextName>logback</contextName>
    <!-- name的值是变量的名称，value的值时变量定义的值。通过定义的值会被插入到logger上下文中。定义变量后，可以使“${}”来使用变量。 -->
    <property name="log.path" value="E:/logs/edu" />

    <!-- 彩色日志 -->
    <!-- 配置格式变量：CONSOLE_LOG_PATTERN 彩色日志格式 -->
    <!-- magenta:洋红 -->
    <!-- boldMagenta:粗红-->
    <!-- cyan:青色 -->
    <!-- white:白色 -->
    <!-- magenta:洋红 -->
    <property name="CONSOLE_LOG_PATTERN"
              value="%yellow(%date{yyyy-MM-dd HH:mm:ss}) |%highlight(%-5level) |%blue(%thread) |%blue(%file:%line) |%green(%logger) |%cyan(%msg%n)"/>


    <!--输出到控制台-->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <!--此日志appender是为开发使用，只配置最底级别，控制台输出的日志级别是大于或等于此级别的日志信息-->
        <!-- 例如：如果此处配置了INFO级别，则后面其他位置即使配置了DEBUG级别的日志，也不会被输出 -->
        <filter class="ch.qos.logback.classic.filter.ThresholdFilter">
            <level>INFO</level>
        </filter>
        <encoder>
            <Pattern>${CONSOLE_LOG_PATTERN}</Pattern>
            <!-- 设置字符集 -->
            <charset>UTF-8</charset>
        </encoder>
    </appender>


    <!--输出到文件-->

    <!-- 时间滚动输出 level为 INFO 日志 -->
    <appender name="INFO_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 正在记录的日志文件的路径及文件名 -->
        <file>${log.path}/log_info.log</file>
        <!--日志文件输出格式-->
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%n</pattern>
            <charset>UTF-8</charset>
        </encoder>
        <!-- 日志记录器的滚动策略，按日期，按大小记录 -->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!-- 每天日志归档路径以及格式 -->
            <fileNamePattern>${log.path}/info/log-info-%d{yyyy-MM-dd}.%i.log</fileNamePattern>
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <maxFileSize>100MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
            <!--日志文件保留天数-->
            <maxHistory>15</maxHistory>
        </rollingPolicy>
        <!-- 此日志文件只记录info级别的 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>INFO</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>

    <!-- 时间滚动输出 level为 WARN 日志 -->
    <appender name="WARN_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 正在记录的日志文件的路径及文件名 -->
        <file>${log.path}/log_warn.log</file>
        <!--日志文件输出格式-->
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%n</pattern>
            <charset>UTF-8</charset> <!-- 此处设置字符集 -->
        </encoder>
        <!-- 日志记录器的滚动策略，按日期，按大小记录 -->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>${log.path}/warn/log-warn-%d{yyyy-MM-dd}.%i.log</fileNamePattern>
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <maxFileSize>100MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
            <!--日志文件保留天数-->
            <maxHistory>15</maxHistory>
        </rollingPolicy>
        <!-- 此日志文件只记录warn级别的 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>warn</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>


    <!-- 时间滚动输出 level为 ERROR 日志 -->
    <appender name="ERROR_FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 正在记录的日志文件的路径及文件名 -->
        <file>${log.path}/log_error.log</file>
        <!--日志文件输出格式-->
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%n</pattern>
            <charset>UTF-8</charset> <!-- 此处设置字符集 -->
        </encoder>
        <!-- 日志记录器的滚动策略，按日期，按大小记录 -->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>${log.path}/error/log-error-%d{yyyy-MM-dd}.%i.log</fileNamePattern>
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <maxFileSize>100MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
            <!--日志文件保留天数-->
            <maxHistory>15</maxHistory>
        </rollingPolicy>
        <!-- 此日志文件只记录ERROR级别的 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>ERROR</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>

    <!--
        <logger>用来设置某一个包或者具体的某一个类的日志打印级别、以及指定<appender>。
        <logger>仅有一个name属性，
        一个可选的level和一个可选的addtivity属性。
        name:用来指定受此logger约束的某一个包或者具体的某一个类。
        level:用来设置打印级别，大小写无关：TRACE, DEBUG, INFO, WARN, ERROR, ALL 和 OFF，
              如果未设置此属性，那么当前logger将会继承上级的级别。
    -->
    <!--
        使用mybatis的时候，sql语句是debug下才会打印，而这里我们只配置了info，所以想要查看sql语句的话，有以下两种操作：
        第一种把<root level="INFO">改成<root level="DEBUG">这样就会打印sql，不过这样日志那边会出现很多其他消息
        第二种就是单独给mapper下目录配置DEBUG模式，代码如下，这样配置sql语句会打印，其他还是正常DEBUG级别：
     -->
    <!--开发环境:打印控制台-->
    <springProfile name="dev">
        <!--可以输出项目中的debug日志，包括mybatis的sql日志-->
        <logger name="com.oyyo" level="INFO" />

        <!--
            root节点是必选节点，用来指定最基础的日志输出级别，只有一个level属性
            level:用来设置打印级别，大小写无关：TRACE, DEBUG, INFO, WARN, ERROR, ALL 和 OFF，默认是DEBUG
            可以包含零个或多个appender元素。
        -->
        <root level="INFO">
            <appender-ref ref="CONSOLE" />
            <appender-ref ref="INFO_FILE" />
            <appender-ref ref="WARN_FILE" />
            <appender-ref ref="ERROR_FILE" />
        </root>
    </springProfile>


    <!--生产环境:输出到文件-->
    <springProfile name="pro">

        <root level="INFO">
            <appender-ref ref="CONSOLE" />
            <appender-ref ref="DEBUG_FILE" />
            <appender-ref ref="INFO_FILE" />
            <appender-ref ref="ERROR_FILE" />
            <appender-ref ref="WARN_FILE" />
        </root>
    </springProfile>

</configuration>
```

7.2错误日志

```java
@Slf4j//日志
public class GlobalExceptionHandler {

log.error(e.getMessage());
```

# 8.阿里云oSS存储

```
//创建bucket
//公共读
//创建阿里云oss证书
//获取到id和密钥
//文档
https://help.aliyun.com/product/31815.html?spm=5176.11065253.5694434980.7.33fd3b1b3TYfbg
```

## 8.1引入依赖

```xml
<dependencies>
<!--    oss依赖    -->
        <dependency>
            <groupId>com.aliyun.oss</groupId>
            <artifactId>aliyun-sdk-oss</artifactId>
        </dependency>
<!--    日期工具栏目依赖    -->
        <dependency>
            <groupId>joda-time</groupId>
            <artifactId>joda-time</artifactId>
        </dependency>
    </dependencies>
```

## 8.2引入配置文件

```properties
#端口
server.port=8002

#服务名
spring.application.name=service-oss

#环境设置
spring.profiles.active=dev

#阿里云OS
#不同的服务地址不同
#地域节点
aliyun.oss.file.endpoint=oss-cn-chengdu.aliyuncs.com
aliyun.oss.file.keyid=LTAI4GDP1QpdyiQ2eEeephUU
aliyun.oss.file.keysecret=ySUVBLTOZJfVwa8zRUVAEL7UE63C35
#名称
aliyun.oss.file.bucketname=edu-101098
```

## 8.3创建启动类报错

```java
1.添加上数据库配置即可
2.@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)
```

## 8.5配置类去读取

```java
@Component
public class ConstandPropertiesUtils implements InitializingBean {
    //读取配置文件

    @Value("${aliyun.oss.file.endpoint}")
    private String endpoint;

    @Value("${aliyun.oss.file.keyid}")
    private String keyId;

    @Value("${aliyun.oss.file.keysecret}")
    private String keySecrect;

    @Value("${aliyun.oss.file.bucketname}")
    private String bucketname;


    //定义公开静态常量
    public static String END_POINT;
    public static String KEY_ID;
    public static String KEY_SECRECT;
    public static String BUCKET_NAME;

    /**
     * 赋值完毕会执行
     * @throws Exception
     */
    @Override
    public void afterPropertiesSet() throws Exception {
        END_POINT = endpoint;
        KEY_ID = keyId;
        KEY_SECRECT = keySecrect;
        BUCKET_NAME = bucketname;
    }
}
```

## 8.6服务实现类

```java
@Service
public class OssServiceImpl implements OssService {

    /**
     * 上传头像到service
     */
    @Override
    public String uploadFileAvatar(MultipartFile file) {
        // Endpoint以杭州为例，其它Region请按实际情况填写。
        String endpoint = ConstandPropertiesUtils.END_POINT;
        // 云账号AccessKey有所有API访问权限，建议遵循阿里云安全最佳实践，创建并使用RAM子账号进行API访问或日常运维，请登录 https://ram.console.aliyun.com 创建。
        String accessKeyId = ConstandPropertiesUtils.KEY_ID;
        String accessKeySecret = ConstandPropertiesUtils.KEY_SECRECT;
        String bucketname = ConstandPropertiesUtils.BUCKET_NAME;
        try{
            // 创建OSSClient实例。
            OSS ossClient = new OSSClientBuilder().build(endpoint, accessKeyId, accessKeySecret);
            // 上传文件流。
            // InputStream inputStream = new FileInputStream("<yourlocalFile>");
            InputStream inputStream = file.getInputStream();

            //获取文件名称
            String Filename = file.getOriginalFilename();

            /**
             * 参数1  buckname
             * 参数2  上传到oss文件路径
             */
            ossClient.putObject(bucketname, "/avatar/"+Filename, inputStream);
            // 关闭OSSClient。
            ossClient.shutdown();

        }catch (Exception e){

        }
        return null;
    }


}
```

```java
@CrossOrigin  //解决跨域
```

## 8.7解决覆盖

```java
//让文件唯一
String uuid = java.util.UUID.randomUUID().toString().replaceAll("-","");
Filename = uuid + Filename;

//按照日期进行分类
```

# 9. EasyExcel

```java
<dependencies>
        <!-- https://mvnrepository.com/artifact/com.alibaba/easyexcel -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>easyexcel</artifactId>
            <version>2.1.1</version>
        </dependency>
    </dependencies>
```

## 9.1写入

```java
//开始i操作
//创建实体类  和  excel一一对应
@Data
public class Test {
	//设置表头名称
    @ExcelProperty("学生编号")
    private Integer sno;

    @ExcelProperty("学生姓名")
    private String sname;
}

//调用
public static void main(String[] args) {
        //实现写Excel的操作
        //1.设置写入excel的文件夹地址和名称
        String filename = "E:\\write.xlsx";

        //2.实现写excel的方法  第二个参数实体类 sheet 和 数据
        EasyExcel.write(filename,Test.class).sheet("学生列表").doWrite(getData());
    }
    //返回list
    private static List<Test> getData(){
        List<Test> list = new ArrayList<>();

        for (int i = 0; i < 10 ; i++) {
            Test test = new Test();
            test.setSno(i);
            test.setSname("lucy"+i);
            list.add(test);
        }
        return list;
    }
```

## 9.2读取

```java
//实体类

@Data
public class Test {
    @ExcelProperty(value = "学生编号",index = 0)
    private Integer sno;

    @ExcelProperty(value = "学生姓名",index = 1)
    private String sname;
}
```

监听器

```java
public class ExcelListener extends AnalysisEventListener<Test> {

    /**
     * 一行一行读取
     * @param test
     * @param analysisContext
     */
    @Override
    public void invoke(Test test, AnalysisContext analysisContext) {
        System.out.println("************："+test);
    }

    /**
     * 读取表头
     */
    @Override
    public void invokeHead(Map<Integer, CellData> headMap, AnalysisContext context) {
        System.out.println("表头！！！！！"+headMap);
    }

    /**
     * 读取完成之后
     * @param analysisContext
     */
    @Override
    public void doAfterAllAnalysed(AnalysisContext analysisContext) {

    }
}
```

调用

```java
String filename = "E:\\write.xlsx";
EasyExcel.read(filename,Test.class,new ExcelListener()).sheet().doRead();
```

## 9.3实战

```java
serviceimpl

@Override
    public void saveSubject(MultipartFile file,EduSubjectService eduSubjectService) {
        try{
            InputStream in = file.getInputStream();

            //调用方法进行读取
            EasyExcel.read(in, SubjectData.class,new SubjectExcelListener(eduSubjectService)).sheet().doRead();

        }catch (Exception e){

        }
    }
    

//实体类
@Data
public class SubjectData {
    @ExcelProperty(index = 0)
    private String oneSubjectName;

    @ExcelProperty(index = 1)
    private String twoSubjectName;
}




//监听器

public class SubjectExcelListener extends AnalysisEventListener<SubjectData> {

    //因为不能交给spring进行管理,需要自己new,
    public EduSubjectService subjectService;
    //通过有参构造传入  subjectService
    /**
     * 读取excel
     * @param subjectData
     * @param analysisContext
     */
    @Override
    public void invoke(SubjectData subjectData, AnalysisContext analysisContext) {
        if(subjectData == null){
            throw new GuliExecption(20001,"文件数据为空");
        }

        //一行一行读取,每次读取两个值,分别判断一二级分类
        EduSubject eduOneSubject = this.existOneSubject(subjectService, subjectData.getOneSubjectName());
        if(eduOneSubject == null){
            eduOneSubject = new EduSubject();
            eduOneSubject.setParentId("0");
            eduOneSubject.setTitle(subjectData.getOneSubjectName());//一级类添加
            subjectService.save(eduOneSubject);
        }
        //添加二级
        String pid = eduOneSubject.getId();
        EduSubject edutwoSubject = this.existTwoSubject(subjectService, subjectData.getTwoSubjectName(), pid);
        if(edutwoSubject == null){
            edutwoSubject = new EduSubject();
            edutwoSubject.setParentId(pid);
            edutwoSubject.setTitle(subjectData.getTwoSubjectName());//二级类添加
            subjectService.save(edutwoSubject);
        }

    }

    /**
     * 判断一级分类
     *
     */
    private EduSubject existOneSubject(EduSubjectService eduSubjectService,String name){
        QueryWrapper<EduSubject> wrapper = new QueryWrapper<>();
        wrapper.eq("title",name);
        wrapper.eq("parent_id","0");
        EduSubject oneSubject = subjectService.getOne(wrapper);
        return oneSubject;
    }

    /**
     * 判断二级分类
     *
     */
    private EduSubject existTwoSubject(EduSubjectService eduSubjectService,String name,String pid){
        QueryWrapper<EduSubject> wrapper = new QueryWrapper<>();
        wrapper.eq("title",name);
        wrapper.eq("parent_id",pid);
        EduSubject twoSubject = subjectService.getOne(wrapper);
        return twoSubject;
    }

    @Override
    public void doAfterAllAnalysed(AnalysisContext analysisContext) {

    }


    /**
     * 有参
     * @param subjectService
     */
    public SubjectExcelListener(EduSubjectService subjectService) {
        this.subjectService = subjectService;
    }

    /**
     *
     *无参
     */
    public SubjectExcelListener(){}
}
```

# 10.树形结构返回

## 10.1创建实体类

```java
//创建一级分类
public class oneSubject {
    private String id;

    private String title;
}
//创建二级分类实体
@Data
public class twoSubject {
    private String id;

    private String title;
}
```

## 10.2建立联系

```java
//一个一级分类有多个二级分类
@Data
public class oneSubject {

    private String id;

    private String title;

    //一个一级分类有多个二级分类
    private List<twoSubject> children = new ArrayList<>();
}
```

## 10.3逻辑

```java
 /**
     * 返回树形结构
     * @return
     */
    @Override
    public List<oneSubject> getAllOneTwoSubject() {
        //查询所有的一二级分类
        QueryWrapper<EduSubject> wrapperOne = new QueryWrapper<>();
        wrapperOne.eq("parent_id","0");
        List<EduSubject> oneSubjectsList = baseMapper.selectList(wrapperOne);

        //查询所有的一二级分类
        QueryWrapper<EduSubject> wrapperTwo = new QueryWrapper<>();
        wrapperOne.ne("parent_id","0");
        List<EduSubject> TwoSubjectsList = baseMapper.selectList(wrapperTwo);

        List<oneSubject> finalSubjectsList = new ArrayList<>();

        for (int i = 0; i < oneSubjectsList.size(); i++) {
            EduSubject eduSubject = oneSubjectsList.get(i);
            oneSubject one = new oneSubject();

            //复制属性
            BeanUtils.copyProperties(eduSubject,one);
            finalSubjectsList.add(one);

            //二级
            List<twoSubject> twoFinalSubjectList = new ArrayList<>();
            for (int j = 0; j < TwoSubjectsList.size() ; j++) {
                EduSubject tsubject  = TwoSubjectsList.get(j);
                //判断parent_id 是否一样
                if(tsubject.getParentId().equals(eduSubject.getId())){
                    twoSubject twosubjcet = new twoSubject();
                    //放入
                    BeanUtils.copyProperties(tsubject,twosubjcet);
                    twoFinalSubjectList.add(twosubjcet);
                }
            }
            //把二级放入一级
            one.setChildren(twoFinalSubjectList);
        }

        return null;
    }
```

# 11.多表操作、

## 11.1插入数据

```java
1.定义value object  请求体实体类
@Data
public class CourseInfoVo {
    private String id;
    private String teacherId;
    private String subjectId;
    private String title;
    private BigDecimal price;
    private Integer lessonNum;
    private String cover;
    private String descrption;
}

@Service
public class EduCourseServiceImpl extends ServiceImpl<EduCourseMapper, EduCourse> implements EduCourseService {

    @Autowired
    EduCourseDescriptionService eduCourseDescriptionService;
    /**
     * 添加课程
     * @param courseInfoVo
     */
   @Override
    public void saveCourseInfo(CourseInfoVo courseInfoVo) {

        EduCourse eduCourse = new EduCourse();
        BeanUtils.copyProperties(courseInfoVo,eduCourse);
        //courseInfoVo转化属性到eduCourse
        //向添加第一张表
        int insert = baseMapper.insert(eduCourse);
        if(insert <= 0){
            throw new GuliExecption(20001,"添加课程信息失败");
        }
        String cid = eduCourse.getId();
        //向第二张表添加
        EduCourseDescription eduCourseDescription = new EduCourseDescription();
        eduCourseDescription.setDescription(courseInfoVo.getDescrption());
        eduCourseDescription.setId(cid);
        eduCourseDescriptionService.save(eduCourseDescription);
    }
}
```

## 11.2多表操作

```xml
 <!--sql:根据课程查询课程确认信息-->
        <select id="getPublishCourseInfo" resultType="com.example.eduservice.entity.vo.CoursePublishVo;">
            SELECT ec.id,ec.title,ec.price,ec.lesson_num AS lessonNum,ec.cover,
                et.name AS teacherName,
                es1.title AS subjectLevelOne,
                es2.title AS subjectLevelTwo,
            FROM
                edu_course ec
                LEFT JOIN edu_course_description ecd ON ec.id=ecd.id
                LEFT JOIN edu_teacher et ON ec.teacher_id=et.id
                LEFT JOIN edu_subject es1 ON ec.subject_parent_id=es1.id
                LEFT JOIN edu_subject es2 ON ec.subject_id=es2.id
            WHERE
                ec.id = #{id}
        </select>
```

serviceimpl操作

```java
 @Override
    public CoursePublishVo publishCourseInfo(String id) {
        CoursePublishVo publishCourseInfo = baseMapper.getPublishCourseInfo(id);
        return publishCourseInfo;
    }
```

返回的实体类

```java
//getPublishCourseInfo
@Data
public class CoursePublishVo {
    private String id;
    private String title;
    private String cover;
    private Integer lessonNum;
    private String subjectLevelOne;
    private String subjectLevelTwo;
    private String teacherName;
    private String price;
}
```

## 11.3处理绑定错误

```java
//不会编译xml文件
org.apache.ibatis.binding.BindingException:
Invalid bound statement (not found): com.example.eduservice.mapper.EduCourseMapper.getPublishCourseInfo


//解决方法
1.复制xml到target目录
2.把xml放进resource中
3.通过配置  //properties  /   pom.xml配置
```

xml配置

```xml
 <!-- 项目打包时会将java目录中的*.xml文件也进行打包 -->
    <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
```

properties配置

```
mybatis-plus.mapper-locations=classpath:com/example/eduservice/mapper/xml/*.xml
```

4.第四种方法  resource

```properties
mybatis-plus.mapper-locations=classpath:/xml/*.xml
```

# 12.阿里云视频点播

## 12.1引入依赖

```xml
//引入依赖

 <dependencies>
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-core</artifactId>
        </dependency>

        <dependency>
            <groupId>com.aliyun.oss</groupId>
            <artifactId>aliyun-sdk-oss</artifactId>
        </dependency>

        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-vod</artifactId>
        </dependency>

        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-sdk-vod-upload</artifactId>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
        </dependency>

        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
        </dependency>

        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
        </dependency>

        <dependency>
            <groupId>joda-time</groupId>
            <artifactId>joda-time</artifactId>
        </dependency>
    </dependencies>
```

## 12.2解决依赖

```shell
//解决
https://www.jianshu.com/p/98b1a8abf77b

```

## 13.3不加密播放

初始化

```java
public class InitObject {
    public static DefaultAcsClient initVodClient(String accessKeyId, String accessKeySecret) throws ClientException {
        String regionId = "cn-shanghai";  // 点播服务接入区域
        DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
        DefaultAcsClient client = new DefaultAcsClient(profile);
        return client;
    }
}
```

根据id获取地址

```java
   //根据视频id获取视频播放地址
        //初始化
        DefaultAcsClient client =  InitObject.initVodClient("LTAI4GDP1QpdyiQ2eEeephUU","ySUVBLTOZJfVwa8zRUVAEL7UE63C35");
        //创建request reponse
        GetPlayInfoRequest request = new GetPlayInfoRequest();
        GetPlayInfoResponse response = new GetPlayInfoResponse();
        //向request中设置视频id
        request.setVideoId("iddsadsadsadasda");
        //调用初始化对象里面的方法 传递request,获取数据
        response = client.getAcsResponse(request);

        //播放列表
        List<GetPlayInfoResponse.PlayInfo> playInfoList = response.getPlayInfoList();
        for (GetPlayInfoResponse.PlayInfo  playInfo : playInfoList){
            //播放地址
            System.out.println("PlayInfoList =" + playInfo.getPlayURL());
        }
        //BaSE信息
        System.out.println("VideoBase.TiTle :" + response.getVideoBase().getTitle());
```

## 13.4加密播放

//根据视频id获取凭证

```java
 //根据视频id获取播放凭证
        //初始化对象
        DefaultAcsClient client =  InitObject.initVodClient("LTAI4GDP1QpdyiQ2eEeephUU","ySUVBLTOZJfVwa8zRUVAEL7UE63C35");
        //获取视频凭证response和request
        GetVideoPlayAuthRequest request = new GetVideoPlayAuthRequest();
        GetVideoPlayAuthResponse response = new GetVideoPlayAuthResponse();

        //设置id
        request.setVideoId("6d7b130bf04d4d48a8e7ce98e16a07d8");
        //得到视频凭证
        response = client.getAcsResponse(request);
        System.out.println("response:"+response.getPlayAuth());
```

## 13.5整合

配置

```properties
#端口
server.port=8003

#服务名
spring.application.name=service-vod

#环境设置
spring.profiles.active=dev
#阿里云OS
#不同的服务地址不同
#地域节点
#aliyun.oss.file.endpoint=oss-cn-chengdu.aliyuncs.com
aliyun.oss.file.keyid=LTAI4GDP1QpdyiQ2eEeephUU
aliyun.oss.file.keysecret=ySUVBLTOZJfVwa8zRUVAEL7UE63C35


#最大上传单个文件大小  默认1M
spring.servlet.multipart.max-file-size=1024MB
#设置总文件大小
spring.servlet.multipart.max-request-size=1024MB
```

创建启动类

```java
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)
@ComponentScan(basePackages = {"com.example"})
public class VodApplication {
    public static void main(String[] args) {
        SpringApplication.run(VodApplication.class,args);
    }
}
```

serviceImpl

```java
@Service
public class VodServiceImpl implements VodService {
    @Override
    public String uploadAlyiVideo(MultipartFile file) {
        try {
            //原始文件名称
            String fileName = file.getOriginalFilename();
            //截取文件名称
            String title = fileName.substring(0,fileName.lastIndexOf("."));

            InputStream inputStream = file.getInputStream();

            System.out.println(ConstantVodUtils.ACCESS_KEY_ID);
            UploadStreamRequest request = new UploadStreamRequest(ConstantVodUtils.ACCESS_KEY_ID, ConstantVodUtils.ACCESS_KEY_SECRET, title, fileName,inputStream);
            UploadVideoImpl uploader = new UploadVideoImpl();
            UploadStreamResponse response = uploader.uploadStream(request);
            String videoId = null;
            if (response.isSuccess()) {
                videoId = response.getVideoId();
            } else {
                System.out.print("ErrorCode=" + response.getCode() + "\n");
                System.out.print("ErrorMessage=" + response.getMessage() + "\n");
                videoId = response.getVideoId();
            }
            return videoId;
        } catch (IOException e) {
            e.printStackTrace();
            return null;
        }
    }
}
```

配置nginx上传大小

```nginx
client _max_body_size 1024m;
  location / {
            root   html;
            index  index.html index.htm;
    }
    location  ~  /eduservice/ {
        proxy_pass http://localhost:8001;
    }
    location  ~  /eduoss/{
        proxy_pass http://localhost:8002;
    }
    location  ~  /eduvod/{
        proxy_pass http://localhost:8003;
    }
```

## 13.6删除

```java
  @DeleteMapping("removeAlyiVideo/{id}")
    public R removeAlyiVideo(@PathVariable String id){
        try {
            //初始化
            DefaultAcsClient client = InitObject.initVodClient(ConstantVodUtils.ACCESS_KEY_ID, ConstantVodUtils.ACCESS_KEY_SECRET);
            //创建删除对象
            DeleteVideoRequest request = new DeleteVideoRequest();
            //设置id
            request.setVideoIds(id);
            //调用初始化方法
            client.getAcsResponse(request);
            return R.ok();
        }catch (Exception e){
            e.printStackTrace();
            throw new GuliExecption(20001,"删除失败");
        }
    }
```

# 13.Spring Cloud

## 13.1介绍

```
1.微服务是架构风格
2.有多个服务，多个服务独立运行，每个服务占用独立进程
	

//优势
1.单体架构所有模块都耦合在一起，代码量大，维护困难
2.单体架构所有模块都是用一个数据库，存储方法单一
3.单体架构所有模块开发使用的技术一样


微服务开发框架
sping Cloud
Dubbo
Dropwizard
consul etcd&etc
```

## 13.2 Spring cloud相关基础服务组件

```
服务发现   Netflix Eureka (Nacos)
服务调用   Netflix Feign
熔断器    	Netflix Hystrsix
服务网关   Spring Cloud GateWay
分布式配置  SpingCloud Config (Nacos)
消息总线   SpingCloud Bus (Nacos)
```

## 13.3服务注册

```
实现 edu 和 vod 模块的调用
//注册中心
下载  nacos双击运行   注意 windows 和 linux不同
```

服务注册依赖

```xml
<!--服务注册-->
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```

edu配置

```java
#nacos服务地址
spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848

//启动类注解
@SpringBootApplication
@EnableDiscoveryClient
@ComponentScan(basePackages = {"com.example"})//扫描common配置类
public class EduApplication {
    public static void main(String[] args) {
        SpringApplication.run(EduApplication.class,args);
    }
}
```

## 13.4服务调用

```xml
<!--服务调用-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

```java
调用端 加注解
@SpringBootApplication
@EnableDiscoveryClient//服务注册
@EnableFeignClients//服务调用
@ComponentScan(basePackages = {"com.example"})//扫描common配置类
public class EduApplication {
    public static void main(String[] args) {
        SpringApplication.run(EduApplication.class,args);
    }
}
```

调用代码

新加interface

```java
@FeignClient("service-vod")//调用服务名
@Component
public interface VodClient {

    //定义调用方法的路径
    @DeleteMapping("/eduvod/video/removeAlyiVideo/{id}")
    public R removeAlyiVideo(@PathVariable("id") String id);
}
```

业务调用

```java
/**
     * 删除小节
     * TODo 删除完善
     * 服务调用
     */
    @DeleteMapping("{id}")
    public R deleteVideo(@PathVariable String id){
        //根据小节id查询视频id
        EduVideo eduvideo = eduVideoService.getById(id);
        String videoSourceId = eduvideo.getVideoSourceId();
        //根据视频id
        if(!StringUtils.isEmpty(videoSourceId)){
            vodClient.removeAlyiVideo(videoSourceId);
        }
        eduVideoService.removeById(id);
        return R.ok();
    }
```

## 13.5List转化为字符串拼接

```java
StringUtils.join(videoIdList.toArray(),",");
```

## 13.6接口调用流程

```
Hystrix基本概念

Feign -> Hystrix -> Ribbon -> Http Client

	1.接口化调用  
	
	2.找到服务 服务发现 调用  Feign
	
	3.服务是否能调用  调用不了 熔断    Hystrix
	
	4.Ribbon  负载均衡  
	
	5.Http Client 执行调用
	
	
	
是一个供分布式系统 提供延迟和容错功能 保证复杂的分布式系统 在面临不可避免的失败时，有其弹性  


```

依赖

```xml
<!--hystrix依赖，主要是用  @HystrixCommand -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
</dependency>
```

配置  (在调用配置中)

```properties
#开启熔断机制
feign.hystrix.enabled=true
#设置 hystrix 超时时间 默认 1000ms
hystrix.command.default.execution.isolation.thread.timeoutInMilliseconds=6000
```

创建调用出错实现类 出错了会调用实现类

```java

@Component
public class VodFileDegradeFeignClient implements VodClient {
    @Override
    public R removeAlyiVideo(String id) {
        return R.error().message("删除失败");
    }

    @Override
    public R deleteBatch(List<String> videoIdList) {
        return R.error().message("删除失败");
    }
}


在接口上加
@FeignClient(name = "service-vod",fallback = VodFileDegradeFeignClient.class)//调用服务名
@Component
public interface VodClient {
```

测试

```java
 //熔断器判断
 R res =  vodClient.removeAlyiVideo(videoSourceId);
 if(res.getCode() == 20001){
 	throw  new GuliExecption(20001,"删除视频失败 熔断器....");
 }
```

## 13.7联合调用(生成订单号)

实现订单  创建

//在base_utils创建公共返回类

```java
@Data
public class CourseWebVoOrder {

    private String id;

    private String title;

    private BigDecimal price;

    private Integer lessonNum;

    private String cover;

    private Long buyCount;

    private Long viewCount;

    private String description;

    private String teacherId;

    private String teacherName;

    private String intro;

    private String avatar;

    private String subjectLevelOneId;

    private String subjectLevelOne;

    private String subjectLevelTwoId;

    private String subjectLevelTwo;

}
```

//在educenter服务写接口

```java
/**
     * 根据用户id获取用户信息
     */
    @PostMapping("getUserInfoOrder/{id}")
    public UcenterMemberOrder getUserInfoOrder(@PathVariable String id){
        UcenterMember member = memberService.getById(id);
        UcenterMemberOrder memberOrder = new UcenterMemberOrder();
        BeanUtils.copyProperties(member,memberOrder);

        return memberOrder;
    }
```

//在eduservice写接口

```java
/**
     * 根据课程id查询课程详情
     */
    @PostMapping("getCourseInfo/{id}")
    public CourseWebVoOrder getCourseInfo(@PathVariable String id){
        CourseWebVo baseCourseInfo = courseService.getBaseCourseInfo(id);
        CourseWebVoOrder courseWebVoOrder = new CourseWebVoOrder();
        BeanUtils.copyProperties(baseCourseInfo,courseWebVoOrder);

        return courseWebVoOrder;
    }
```

//在edu_order注册接口

```java
@Component
@FeignClient("service-ucenter")
public interface UcenterClient {

    @PostMapping("educenter/member/getUserInfoOrder/{id}")
    public UcenterMemberOrder getUserInfoOrder(@PathVariable("id") String id);
}


@Component
@FeignClient("service-edu")
public interface EduClient {
    @PostMapping("/eduservice/coursefront/getUserInfoOrder/{id}")
    public CourseWebVoOrder getCourseInfo(@PathVariable("id") String id);
}
```

//生成订单号工具类

```java
public class OrderNoUtil {

    /**
     * 获取订单号
     * @return
     */
    public static String getOrderNo() {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyyMMddHHmmss");
        String newDate = sdf.format(new Date());
        String result = "";
        Random random = new Random();
        for (int i = 0; i < 3; i++) {
            result += random.nextInt(10);
        }
        return newDate + result;
    }

}
```

//调用

```java
	@Autowired
    EduClient eduClient;
    
    @Autowired
    UcenterClient ucenterClient;

 public String createOrder(String courseId, String memberIdByJwtToken) {
        //通过用户id调用获取用户信息
        UcenterMemberOrder userInfoOrder = ucenterClient.getUserInfoOrder(memberIdByJwtToken);

        //通过课程id远程调用获取课程信息
        CourseWebVoOrder courseInfo = eduClient.getCourseInfo(courseId);

        //添加到数据库
        TOrder order = new TOrder();
        order.setOrderNo(OrderNoUtil.getOrderNo());//订单号
        order.setCourseId(courseId);
        order.setCourseTitle(courseInfo.getTitle());
        order.setCourseCover(courseInfo.getCover());
        order.setTeacherName("test");
        order.setTotalFee(courseInfo.getPrice());
        order.setMemberId(memberIdByJwtToken);
        order.setMobile(userInfoOrder.getMobile());
        order.setNickname(userInfoOrder.getNickname());
        order.setStatus(0);//支付状态 未支付
        order.setPayType(1);//支付类型 微信
        baseMapper.insert(order);

        return order.getOrderNo();
    }
```

## 13.8 网关

```
网关的出现的原因是  微服务的出现  不同的微服务一般有不同的网络地址
而且 外部客户端需要调用多个服务的接口才能完成一个业务需求
(1) 客户端会多次请求不同的微服务  增加了客户端的复杂性
(2) 存在跨域请求 在一定场景下相对复杂
(3) 认证复杂  每一个服务都需要独立认证
(4) 难以重构
(5) 某些服务可能使用了防火墙  /对浏览器不友好的协议 直接访问具有一定的困难

功能类似 nginx 
可以做到
	请求转发
	负载均衡
	权限控制
	同意解决跨域
	限流保护
	等等
	
客户端调用  
	先到网关 集成nacos  

重要概念
  路由 不同的服务 不同的路由
  断言	匹配规则  
  过滤器	
```

### 13.8.1引入依赖

```xml
    <dependencies>
        <dependency>
            <groupId>com.example</groupId>
            <artifactId>common_utils</artifactId>
            <version>0.0.1-SNAPSHOT</version>
        </dependency>

        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
        </dependency>

        <!--gson-->
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
        </dependency>

        <!--服务调用-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
    </dependencies>

```

### 13.8.2启动类

```java
@SpringBootApplication
@EnableDiscoveryClient
public class ApiGatewayApplication {
    public static void main(String[] args) {
        SpringApplication.run(ApiGatewayApplication.class,args);
    }
}
```

### 13.8.3配置文件

```properties
# 服务端口
server.port=8222
# 服务名
spring.application.name=service-gateway
# nacos服务地址
spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848

#使用服务发现路由
spring.cloud.gateway.discovery.locator.enabled=true

#设置路由id
spring.cloud.gateway.routes[0].id=service-acl
#设置路由的uri   lb://nacos注册服务名称
spring.cloud.gateway.routes[0].uri=lb://service-acl
#设置路由断言,代理servicerId为auth-service的/auth/路径
spring.cloud.gateway.routes[0].predicates= Path=/*/acl/**

#配置service-edu服务
spring.cloud.gateway.routes[1].id=service-edu
spring.cloud.gateway.routes[1].uri=lb://service-edu
spring.cloud.gateway.routes[1].predicates= Path=/eduservice/**

#配置service-edu服务
spring.cloud.gateway.routes[2].id=service-msm
spring.cloud.gateway.routes[2].uri=lb://service-msm
spring.cloud.gateway.routes[2].predicates= Path=/edumsm/**


```

## 13.8.4跨域处理

```java
@Configuration
public class CorsConfig {
    @Bean
    public CorsWebFilter corsFilter() {
        CorsConfiguration config = new CorsConfiguration();
        config.addAllowedMethod("*");
        config.addAllowedOrigin("*");
        config.addAllowedHeader("*");

        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource(new PathPatternParser());
        source.registerCorsConfiguration("/**", config);

        return new CorsWebFilter(source);
    }
}
```

## 13.8.5全局配置过滤

```java
package com.example.gateway.filter;

import com.google.gson.JsonObject;
import org.springframework.cloud.gateway.filter.GatewayFilterChain;
import org.springframework.cloud.gateway.filter.GlobalFilter;
import org.springframework.core.Ordered;
import org.springframework.core.io.buffer.DataBuffer;
import org.springframework.http.server.reactive.ServerHttpRequest;
import org.springframework.http.server.reactive.ServerHttpResponse;
import org.springframework.stereotype.Component;
import org.springframework.util.AntPathMatcher;
import org.springframework.web.server.ServerWebExchange;
import reactor.core.publisher.Mono;

import java.nio.charset.StandardCharsets;
import java.util.List;

/**
 * <p>
 * 全局Filter，统一处理会员登录与外部不允许访问的服务
 * </p>
 *
 * @author qy
 * @since 2019-11-21
 */
@Component
public class AuthGlobalFilter implements GlobalFilter, Ordered {

    private AntPathMatcher antPathMatcher = new AntPathMatcher();

    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        ServerHttpRequest request = exchange.getRequest();
        String path = request.getURI().getPath();
        //谷粒学院api接口，校验用户必须登录
        if(antPathMatcher.match("/api/**/auth/**", path)) {
            List<String> tokenList = request.getHeaders().get("token");
            if(null == tokenList) {
                ServerHttpResponse response = exchange.getResponse();
                return out(response);
            } else {
//                Boolean isCheck = JwtUtils.checkToken(tokenList.get(0));
//                if(!isCheck) {
                    ServerHttpResponse response = exchange.getResponse();
                    return out(response);
//                }
            }
        }
        //内部服务接口，不允许外部访问
        if(antPathMatcher.match("/**/inner/**", path)) {
            ServerHttpResponse response = exchange.getResponse();
            return out(response);
        }
        return chain.filter(exchange);
    }

    @Override
    public int getOrder() {
        return 0;
    }

    private Mono<Void> out(ServerHttpResponse response) {
        JsonObject message = new JsonObject();
        message.addProperty("success", false);
        message.addProperty("code", 28004);
        message.addProperty("data", "鉴权失败");
        byte[] bits = message.toString().getBytes(StandardCharsets.UTF_8);
        DataBuffer buffer = response.bufferFactory().wrap(bits);
        //response.setStatusCode(HttpStatus.UNAUTHORIZED);
        //指定编码，否则在浏览器中会中文乱码
        response.getHeaders().add("Content-Type", "application/json;charset=UTF-8");
        return response.writeWith(Mono.just(buffer));
    }
}

```

## 13.8.6配置中心

在要加载的配置服务上面写上引入依赖

```xml
<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
        </dependency>
```

建立文件  bootstrap.properties

```properties
#nacos服务地址
spring.cloud.nacos.config.server-addr=127.0.0.1:8848
spring.application.name=service-edu
# 环境设置 dev test prod
spring.profiles.active=dev
```

在nacos控制台配置文件

```properties
# 服务端口
server.port=8001
# 服务名
spring.application.name=service-edu

# 环境设置 dev test prod
spring.profiles.active=dev

# mysql数据库丽链接
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/guli?serverTimezone=GMT%2B8&characterEncoding=UTF8
spring.datasource.username=root
spring.datasource.password=123456

#json解析时间
spring.jackson.date-format=yyyy-MM-dd HH:mm:ss
spring.jackson.time-zone=GMT+8

#mybatis日志
#mybatis-plus.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
mybatis-plus.mapper-locations=classpath:/xml/*.xml

#日志级别
#logging.level.root=WARN

#nacos服务地址
spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848

#开启熔断机制
feign.hystrix.enabled=true
#设置 hystrix 超时时间 默认 1000ms
hystrix.command.default.execution.isolation.thread.timeoutInMilliseconds=6000



```



# 13redis

```
强制停止 nginx
taskkill /f /t /im nginx.exe

比较人们的NoSQL系统 

redis的特点
1.Redis的读取速度 110000次/s  写的速度是 81000次/s
2.原子  redis的所有操作都是原子性的  
3.支持多种数据结构  String list hash set zset
4.持久化：集群部署
5.支持过期时间  支持事务 消息订阅


一般来讲 把经常进行查询 不经常修改的数据  不是特别重要的数据

```

## 13.1整合

xml

```xml
<!-- redis -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>

<!--         spring2.X集成redis所需common-pool2-->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
            <version>2.6.0</version>
        </dependency>
```

## 13.2配置

RedisConfig

```java
import com.fasterxml.jackson.annotation.JsonAutoDetect;
import com.fasterxml.jackson.annotation.JsonTypeInfo;
import com.fasterxml.jackson.annotation.PropertyAccessor;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.jsontype.impl.LaissezFaireSubTypeValidator;
import org.springframework.cache.CacheManager;
import org.springframework.cache.annotation.EnableCaching;
import org.springframework.cache.jcache.config.JCacheConfigurerSupport;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.cache.RedisCacheConfiguration;
import org.springframework.data.redis.cache.RedisCacheManager;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.serializer.Jackson2JsonRedisSerializer;
import org.springframework.data.redis.serializer.RedisSerializationContext;
import org.springframework.data.redis.serializer.RedisSerializer;
import org.springframework.data.redis.serializer.StringRedisSerializer;

import java.time.Duration;

@Configuration//配置类
@EnableCaching//开启缓存
public class RedisConfig extends JCacheConfigurerSupport {
    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory factory) {
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        RedisSerializer<String> redisSerializer = new StringRedisSerializer();
        Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);
        ObjectMapper om = new ObjectMapper();
        om.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
        om.activateDefaultTyping(LaissezFaireSubTypeValidator.instance ,
                ObjectMapper.DefaultTyping.NON_FINAL, JsonTypeInfo.As.PROPERTY);
        jackson2JsonRedisSerializer.setObjectMapper(om);
        template.setConnectionFactory(factory);
        //key序列化方式
        template.setKeySerializer(redisSerializer);
        //value序列化
        template.setValueSerializer(jackson2JsonRedisSerializer);
        //value hashmap序列化
        template.setHashValueSerializer(jackson2JsonRedisSerializer);
        return template;
    }

    @Bean
    public CacheManager cacheManager(RedisConnectionFactory factory) {
        RedisSerializer<String> redisSerializer = new StringRedisSerializer();
        Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);
        //解决查询缓存转换异常的问题
        ObjectMapper om = new ObjectMapper();
        om.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
        om.activateDefaultTyping(LaissezFaireSubTypeValidator.instance ,
                ObjectMapper.DefaultTyping.NON_FINAL, JsonTypeInfo.As.PROPERTY);
        jackson2JsonRedisSerializer.setObjectMapper(om);
        // 配置序列化（解决乱码的问题）,过期时间600秒
        RedisCacheConfiguration config = RedisCacheConfiguration.defaultCacheConfig()
                //数据过期时间  600s
                .entryTtl(Duration.ofSeconds(600))
                .serializeKeysWith(RedisSerializationContext.SerializationPair.fromSerializer(redisSerializer))
                .serializeValuesWith(RedisSerializationContext.SerializationPair.fromSerializer(jackson2JsonRedisSerializer))
                .disableCachingNullValues();
        RedisCacheManager cacheManager = RedisCacheManager.builder(factory)
                .cacheDefaults(config)
                .build();
        return cacheManager;
    }
}

```

## 13.3注解

```
@Cacheable  
	对请求结果进行缓存  缓存存在直接读取缓存 缓存不存在  直接执行方法
@CachePut
	每次都会执行  并且将结果存入缓存  一般用在新增方法上
@CacheEvict
	会清空缓存  一般用在更新或者删除方法上
```

## 13.4安装redis

```
//解压
tar xzvf redis-5.0.10.tar.gz 

cd redis-4.0.8
make
cd src
make install PREFIX=/usr/local/redis

移动配置文件到安装目录下
cd ..
mkdir /usr/local/redis/etc
mv redis.conf /usr/local/redis/etc


5.配置redis为后台启动
	　　vi /usr/local/redis/etc/redis.conf //将daemonize no 改成daemonize yes
6.redis加入到开机启动
	　vi /etc/rc.local //在里面添加内容：/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf (意思就是开机调用这段开启redis的命令)
	　
7.开启redis 
	在目录/usr/local/redis 输入下面命令启动redis
		./bin/redis-server& ./redis.conf
8.将redis-cli,redis-server拷贝到bin下，让redis-cli指令可以在任意目录下直接使用
	cp /usr/local/redis/bin/redis-server /usr/local/bin/
　　cp /usr/local/redis/bin/redis-cli /usr/local/bin/
9.设置redis密码
　a.运行命令：redis-cli
　　b.查看现有的redis密码(可选操作，可以没有)

　　　　运行命令：config get requirepass 如果没有设置过密码的话运行结果会如下图所示

　　c.设置redis密码

　　　　运行命令：config set requirepass ****(****为你要设置的密码)，设置成功的话会返回‘OK’字样

　　d.测试连接

　　　　重启redis服务

　　　　//（redis-cli -h 127.0.0.1 -p 6379 -a ****（****为你设置的密码））

　　　　输入 redis-cli 进入命令模式，使用 auth '*****' （****为你设置的密码）登陆　　
    
   10.,重启即可
        redis-cli shutdown
        redis-server
        　pkill redis  //停止redis
        　
      ps -ef | grep redis
      kill -9 pid
    11.
    	此时 虽然防火墙开放了6379端口，但是外网还是无法访问的，因为redis监听的是127.0.0.1：6379，并不监听外网的请求。
　　　　　　（一）把文件夹目录里的redis.conf配置文件里的bind 127.0.0.1前面加#注释掉
　　　　　　（二）命令：redis-cli连接到redis后，通过 config get  daemonize和config get  protected-mode 是不是都为no，如果不是，就用config set 配置名 属性 改为no。
```

## 13.5配置

```properties
#redis配置

spring.redis.host=47.101.212.62
spring.redis.port=6379
spring.redis.database=0
spring.redis.timeout=1800000
```

```
get banner::selectIndexList
//获取缓存
```

## 13.6调用

```
@Cacheable(value = "banner",key = "'selectIndexList'")
@Override
    public List<CrmBanner> selectAllBanner() {
        QueryWrapper<CrmBanner> wrapper = new QueryWrapper<>();
        wrapper.orderByDesc("id");
        wrapper.last("limit 2");
        List<CrmBanner> list = baseMapper.selectList(wrapper);
        return list;
    }
```

# 14.登录鉴权

## 14.1传统

```
单一服务器
	使用session实现 登录成功之后把用户数据存到 session里面 
	判断是否登录  从session里面获取

SSo  集群部署
	分布式
	单点登录 
		三种方式
			session广播机制 session复制
			cookie + redis 数据放到两个地方  redis 和 cookie
				redis key(唯一值)  value  用户数据
				cookie  存储key
				请求时候带上cookie 在redis里面查询 查询到就登陆成功
			token
```

## 14.2JWT

```
JWT字符串包含三部分信息 
	1.jwt头部信息
	2.有效载荷 包含主体信息 就是用户信息
	3.签名哈希 防伪标志 
	默认 SHA256
```

## 14.3引入

xml

```xml
		<dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt</artifactId>
        </dependency>
```

工具类

```java
package com.example.commonutils;

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jws;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import org.springframework.http.server.reactive.ServerHttpRequest;
import org.springframework.util.StringUtils;

import javax.servlet.http.HttpServletRequest;
import java.util.Date;

/**
 * @author helen
 * @since 2019/10/16
 */
public class JwtUtils {

    //过期时间
    public static final long EXPIRE = 1000 * 60 * 60 * 24;
    //密钥
    public static final String APP_SECRET = "ukc8BDbRigUDaY6pZFfWus2jZWLPHO";

    //生成token
    public static String getJwtToken(String id, String nickname){

        String JwtToken = Jwts.builder()
                .setHeaderParam("typ", "JWT")
                .setHeaderParam("alg", "HS256")
            	//分类 设置过期时间
                .setSubject("guli-user")
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + EXPIRE))
            
            	//主体用户信息
                .claim("id", id)
                .claim("nickname", nickname)
            
            	//签名哈希
                .signWith(SignatureAlgorithm.HS256, APP_SECRET)
                .compact();

        return JwtToken;
    }

    /**
     * 判断token是否存在与有效
     * @param jwtToken
     * @return
     */
    public static boolean checkToken(String jwtToken) {
        if(StringUtils.isEmpty(jwtToken)) return false;
        try {
            Jwts.parser().setSigningKey(APP_SECRET).parseClaimsJws(jwtToken);
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
        return true;
    }

    /**
     * 判断token是否存在与有效
     * @param request
     * @return
     */
    public static boolean checkToken(HttpServletRequest request) {
        try {
            String jwtToken = request.getHeader("token");
            if(StringUtils.isEmpty(jwtToken)) return false;
            Jwts.parser().setSigningKey(APP_SECRET).parseClaimsJws(jwtToken);
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
        return true;
    }

    /**
     * 根据token获取会员id
     * @param request
     * @return
     * 获取用户信息
     */
    public static String getMemberIdByJwtToken(HttpServletRequest request) {
        String jwtToken = request.getHeader("token");
        if(StringUtils.isEmpty(jwtToken)) return "";
        Jws<Claims> claimsJws = Jwts.parser().setSigningKey(APP_SECRET).parseClaimsJws(jwtToken);
        Claims claims = claimsJws.getBody();
        return (String)claims.get("id");
    }
}

```

# 15.短信

```java
//开启短信 
https://www.aliyun.com/product/sms?spm=5176.10695662.1128094.1.2a6b4beeu1EZbT

申请 模板管理 签名管理：
```

## 15.1依赖引入

xml

```xml
 <!-- 短信服务   -->
    <dependencies>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
        </dependency>

        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-core</artifactId>
        </dependency>
    </dependencies>
```

随机数工具类

```java
package com.example.msmservice.utils;

import java.text.DecimalFormat;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Random;

/**
 * 获取随机数
 * 
 * @author qianyi
 *
 */
public class RandomUtil {

	private static final Random random = new Random();

	private static final DecimalFormat fourdf = new DecimalFormat("0000");

	private static final DecimalFormat sixdf = new DecimalFormat("000000");

	public static String getFourBitRandom() {
		return fourdf.format(random.nextInt(10000));
	}

	public static String getSixBitRandom() {
		return sixdf.format(random.nextInt(1000000));
	}

	/**
	 * 给定数组，抽取n个数据
	 * @param list
	 * @param n
	 * @return
	 */
	public static ArrayList getRandom(List list, int n) {

		Random random = new Random();

		HashMap<Object, Object> hashMap = new HashMap<Object, Object>();

		// 生成随机数字并存入HashMap
		for (int i = 0; i < list.size(); i++) {

			int number = random.nextInt(100) + 1;

			hashMap.put(number, i);
		}

		// 从HashMap导入数组
		Object[] robjs = hashMap.values().toArray();

		ArrayList r = new ArrayList();

		// 遍历数组并打印数据
		for (int i = 0; i < n; i++) {
			r.add(list.get((int) robjs[i]));
			System.out.print(list.get((int) robjs[i]) + "\t");
		}
		System.out.print("\n");
		return r;
	}
}

```

## 15.2发送

controller

```java
 @GetMapping("send/{phone}")
    public R sendMsm(@PathVariable String phone){

        //生成验证码随机数
        String code = RandomUtil.getFourBitRandom();
        Map<String,Object> param = new HashMap<>();
        param.put("code",code);

        boolean isSend = msmService.send(param,phone);
        if(isSend){
            return R.ok();
        }else{
            return R.error().message("短信发送失败");
        }
    }
```

发送

```java
@Service
public class MsmServiceImpl implements MsmService {
    @Override
    public boolean send(Map<String, Object> param, String phone) {
        //判断手机号是否为空
        if(StringUtils.isEmpty(phone)) return false;

        DefaultProfile profile = DefaultProfile.getProfile("default","LTAI4GDP1QpdyiQ2eEeephUU","ySUVBLTOZJfVwa8zRUVAEL7UE63C35");

        IAcsClient cilent = new DefaultAcsClient(profile);

        //设置相关固定参数
        CommonRequest request = new CommonRequest();
        request.setSysMethod(MethodType.POST);
        request.setDomain("dysmsapi.aliyuncs.com");
        request.setVersion("2017-05-25");
        request.setAction("SendSms");


        //设置参数
        request.putQueryParameter("PhoneNumbers",phone);//手机号
        request.putQueryParameter("SignName","古粒在线教育网站");//签名
        request.putQueryParameter("TemplateCode","SMS_205392318");//模板
        request.putQueryParameter("TemplateParam", JSONObject.toJSONString(param));//code json

        //最终发送
        try {
            CommonResponse response = cilent.getCommonResponse(request);
            boolean success = response.getHttpResponse().isSuccess();
            return success;
        } catch (ClientException e) {
            e.printStackTrace();
            return false;
        }
    }
}
```

## 15.3解决时间有效时间

```java
@Autowired
private RedisTemplate<String,String> redisTemplate;


 /**
  * 先从redis里面取,没有自动生成，有的话获取
  */
String code = redisTemplate.opsForValue().get(phone);
if(!StringUtils.isEmpty(code)){
    return R.ok();
}
//生成验证码随机数
        code = RandomUtil.getFourBitRandom();
        Map<String,Object> param = new HashMap<>();
        param.put("code",code);

        boolean isSend = msmService.send(param,phone);
        if(isSend){
            //发送成功,把发送成功的验证码放到redis
            //设置有效时间
            redisTemplate.opsForValue().set(phone,code,5, TimeUnit.MINUTES);//五分钟
            return R.ok();
        }else{
            return R.error().message("短信发送失败");
        }
```

# 16.微信登录

```
//创建服务  逆向生成代码
```

普通登录

## 16.1.token生成  密码不加密

```java
 public String login(UcenterMember member) {
        String mobile = member.getMobile();
        String password = member.getPassword();

        //手机号非空判断
        if(StringUtils.isEmpty(mobile) || StringUtils.isEmpty(password)){
            throw new GuliExecption(20001,"手机号密码不能为空");
        }

        //判断手机号是否正确
        QueryWrapper<UcenterMember> wrapper = new QueryWrapper<>();
        wrapper.eq("mobile",mobile);
        UcenterMember mobileMember = baseMapper.selectOne(wrapper);
        //判断是否为空
        if(mobileMember == null){
            throw new GuliExecption(20001,"手机号不存在");
        }

        //判断密码
        if(!password.equals(mobileMember.getPassword())){
            throw new GuliExecption(20001,"密码错误");
        }

        //判断被禁用
        if(mobileMember.getIsDisabled()){
            throw new   GuliExecption(20003,"用户被禁用");
        }
        //生成token
        String token = JwtUtils.getJwtToken(mobileMember.getId(),mobileMember.getNickname());
        return token;
    }
```

## 16.2.加密

MD5工具类

```java
package com.example.commonutils;

import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;


public final class MD5 {

    public static String encrypt(String strSrc) {
        try {
            char hexChars[] = { '0', '1', '2', '3', '4', '5', '6', '7', '8',
                    '9', 'a', 'b', 'c', 'd', 'e', 'f' };
            byte[] bytes = strSrc.getBytes();
            MessageDigest md = MessageDigest.getInstance("MD5");
            md.update(bytes);
            bytes = md.digest();
            int j = bytes.length;
            char[] chars = new char[j * 2];
            int k = 0;
            for (int i = 0; i < bytes.length; i++) {
                byte b = bytes[i];
                chars[k++] = hexChars[b >>> 4 & 0xf];
                chars[k++] = hexChars[b & 0xf];
            }
            return new String(chars);
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
            throw new RuntimeException("MD5加密出错！！+" + e);
        }
    }

    public static void main(String[] args) {
        System.out.println(MD5.encrypt("111111"));
    }

}

```

//调用

```java
//判断密码  加密
if(!MD5.encrypt(password).equals(mobileMember.getPassword())){
	throw new GuliExecption(20001,"密码错误");
}
```

## 16.3注册

创建实体Vo类

```java
@Data
public class RegisterVo {

    @ApiModelProperty(value = "昵称")
    private String nickname;

    @ApiModelProperty(value = "手机号")
    private String mobile;

    @ApiModelProperty(value = "密码")
    private String password;

    @ApiModelProperty(value = "验证码")
    private String code;

}
```

service

```java
public void register(RegisterVo registerVo) {
        //获取注册的数据
        String code = registerVo.getCode();
        String mobile = registerVo.getMobile();
        String nickname = registerVo.getNickname();
        String password = registerVo.getPassword();

        //非空判断
        if(StringUtils.isEmpty(mobile) || StringUtils.isEmpty(nickname)
                || StringUtils.isEmpty(code) || StringUtils.isEmpty(password)){
            throw new GuliExecption(20001,"用户名密码验证码昵称不能为空");
        }

        //判断验证码是否正确
        //和redis里面的验证码是否一样
        String redisCode = redisTemplate.opsForValue().get(mobile);
        if(!code.equals(redisCode)){
           throw new GuliExecption(20001,"验证码错误");
        }

        //判断手机号是否重复
        QueryWrapper<UcenterMember> wrapper = new QueryWrapper<>();
        wrapper.eq("mobile",mobile);
        Integer count = baseMapper.selectCount(wrapper);
        if(count > 0){
            throw new GuliExecption(20001,"手机号已经注册");
        }
        UcenterMember member = new UcenterMember();
        member.setMobile(mobile);
        member.setNickname(nickname);
        member.setPassword(MD5.encrypt(password));
        member.setIsDisabled(false);
        baseMapper.insert(member);
    }
```

## 16.4根据token获取用户信息

```java
	/**
     * 根据token获取用户信息
     */
    @GetMapping("getMemberInfo")
    public R getMemberInfo(HttpServletRequest request){
        String memberId = JwtUtils.getMemberIdByJwtToken(request);
        //查询数据库  根据用户id
        UcenterMember member = memberService.getById(memberId);
        return R.ok().data("userinfo",member);
    }
```

## 16.5扫码登录

微信扫码登录

配置文件

```properties
wx.open.app_id=wxed9954c01bb89b47
wx.open.appsecret=a7482517235173ddb4083788de60b90e
wx.open.redirecturl=http://guli.shop/api/ucenter/wx/callback
```

controller

```java
 /**
     * 生成微信二维码
     */
    @GetMapping("login")
    public String getWxCode(){
        //固定地址
        String baseUrl = "https://open.weixin.qq.com/connect/qrconnect" +
                "?appid=%s" +
                "&redirect_uri=%s" +
                "&response_type=code" +
                "&scope=snsapi_login" +
                "&state=%s" +
                "#wechat_redirect";
        //对重定向地址编码
        String redirectUrl = ConstantWxUtils.WX_OPEN_REDIRECT_URL;
        System.out.println(redirectUrl);

        try {
            redirectUrl = URLEncoder.encode(redirectUrl,"UTF-8");
        } catch (UnsupportedEncodingException e) {
            e.printStackTrace();
            throw new GuliExecption(20001,"转码异常");
        }
        String url = String.format(
                baseUrl,
                ConstantWxUtils.WX_OPEN_APP_ID,
                redirectUrl,
                "atguigu"
        );
        //请求微信地址
        return "redirect:" + url;
    }
```

回调 扫码成功

```java
/**
     * 获取扫描人信息,添加数据
     */
    @GetMapping("callback")
    public String callback(String code,String state){
        return "redirect:http://localhost:3000";
    }
```

## 16.6请求

Httpclient依赖

```xml
<!-- httpClient依赖    -->
    <dependencies>
        <dependency>
            <groupId>org.apache.httpcomponents</groupId>
            <artifactId>httpclient</artifactId>
        </dependency>
        <dependency>
            <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
        </dependency>
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
        </dependency>
    </dependencies>
```

HttoClient工具类

```java
package com.example.educenter.utils;

import org.apache.commons.io.IOUtils;
import org.apache.commons.lang.StringUtils;
import org.apache.http.Consts;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.NameValuePair;
import org.apache.http.client.HttpClient;
import org.apache.http.client.config.RequestConfig;
import org.apache.http.client.config.RequestConfig.Builder;
import org.apache.http.client.entity.UrlEncodedFormEntity;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.conn.ConnectTimeoutException;
import org.apache.http.conn.ssl.SSLConnectionSocketFactory;
import org.apache.http.conn.ssl.SSLContextBuilder;
import org.apache.http.conn.ssl.TrustStrategy;
import org.apache.http.conn.ssl.X509HostnameVerifier;
import org.apache.http.entity.ContentType;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.impl.conn.PoolingHttpClientConnectionManager;
import org.apache.http.message.BasicNameValuePair;

import javax.net.ssl.SSLContext;
import javax.net.ssl.SSLException;
import javax.net.ssl.SSLSession;
import javax.net.ssl.SSLSocket;
import java.io.IOException;
import java.net.SocketTimeoutException;
import java.security.GeneralSecurityException;
import java.security.cert.CertificateException;
import java.security.cert.X509Certificate;
import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Set;

/**
 *  依赖的jar包有：commons-lang-2.6.jar、httpclient-4.3.2.jar、httpcore-4.3.1.jar、commons-io-2.4.jar
 * @author zhaoyb
 *
 */
public class HttpClientUtils {

	public static final int connTimeout=10000;
	public static final int readTimeout=10000;
	public static final String charset="UTF-8";
	private static HttpClient client = null;

	static {
		PoolingHttpClientConnectionManager cm = new PoolingHttpClientConnectionManager();
		cm.setMaxTotal(128);
		cm.setDefaultMaxPerRoute(128);
		client = HttpClients.custom().setConnectionManager(cm).build();
	}

	public static String postParameters(String url, String parameterStr) throws ConnectTimeoutException, SocketTimeoutException, Exception{
		return post(url,parameterStr,"application/x-www-form-urlencoded",charset,connTimeout,readTimeout);
	}

	public static String postParameters(String url, String parameterStr,String charset, Integer connTimeout, Integer readTimeout) throws ConnectTimeoutException, SocketTimeoutException, Exception{
		return post(url,parameterStr,"application/x-www-form-urlencoded",charset,connTimeout,readTimeout);
	}

	public static String postParameters(String url, Map<String, String> params) throws ConnectTimeoutException,
			SocketTimeoutException, Exception {
		return postForm(url, params, null, connTimeout, readTimeout);
	}

	public static String postParameters(String url, Map<String, String> params, Integer connTimeout,Integer readTimeout) throws ConnectTimeoutException,
			SocketTimeoutException, Exception {
		return postForm(url, params, null, connTimeout, readTimeout);
	}

	public static String get(String url) throws Exception {
		return get(url, charset, null, null);
	}

	public static String get(String url, String charset) throws Exception {
		return get(url, charset, connTimeout, readTimeout);
	}

	/**
	 * 发送一个 Post 请求, 使用指定的字符集编码.
	 *
	 * @param url
	 * @param body RequestBody
	 * @param mimeType 例如 application/xml "application/x-www-form-urlencoded" a=1&b=2&c=3
	 * @param charset 编码
	 * @param connTimeout 建立链接超时时间,毫秒.
	 * @param readTimeout 响应超时时间,毫秒.
	 * @return ResponseBody, 使用指定的字符集编码.
	 * @throws ConnectTimeoutException 建立链接超时异常
	 * @throws SocketTimeoutException  响应超时
	 * @throws Exception
	 */
	public static String post(String url, String body, String mimeType,String charset, Integer connTimeout, Integer readTimeout)
			throws ConnectTimeoutException, SocketTimeoutException, Exception {
		HttpClient client = null;
		HttpPost post = new HttpPost(url);
		String result = "";
		try {
			if (StringUtils.isNotBlank(body)) {
				HttpEntity entity = new StringEntity(body, ContentType.create(mimeType, charset));
				post.setEntity(entity);
			}
			// 设置参数
			Builder customReqConf = RequestConfig.custom();
			if (connTimeout != null) {
				customReqConf.setConnectTimeout(connTimeout);
			}
			if (readTimeout != null) {
				customReqConf.setSocketTimeout(readTimeout);
			}
			post.setConfig(customReqConf.build());

			HttpResponse res;
			if (url.startsWith("https")) {
				// 执行 Https 请求.
				client = createSSLInsecureClient();
				res = client.execute(post);
			} else {
				// 执行 Http 请求.
				client = HttpClientUtils.client;
				res = client.execute(post);
			}
			result = IOUtils.toString(res.getEntity().getContent(), charset);
		} finally {
			post.releaseConnection();
			if (url.startsWith("https") && client != null&& client instanceof CloseableHttpClient) {
				((CloseableHttpClient) client).close();
			}
		}
		return result;
	}


	/**
	 * 提交form表单
	 *
	 * @param url
	 * @param params
	 * @param connTimeout
	 * @param readTimeout
	 * @return
	 * @throws ConnectTimeoutException
	 * @throws SocketTimeoutException
	 * @throws Exception
	 */
	public static String postForm(String url, Map<String, String> params, Map<String, String> headers, Integer connTimeout,Integer readTimeout) throws ConnectTimeoutException,
			SocketTimeoutException, Exception {

		HttpClient client = null;
		HttpPost post = new HttpPost(url);
		try {
			if (params != null && !params.isEmpty()) {
				List<NameValuePair> formParams = new ArrayList<NameValuePair>();
				Set<Entry<String, String>> entrySet = params.entrySet();
				for (Entry<String, String> entry : entrySet) {
					formParams.add(new BasicNameValuePair(entry.getKey(), entry.getValue()));
				}
				UrlEncodedFormEntity entity = new UrlEncodedFormEntity(formParams, Consts.UTF_8);
				post.setEntity(entity);
			}

			if (headers != null && !headers.isEmpty()) {
				for (Entry<String, String> entry : headers.entrySet()) {
					post.addHeader(entry.getKey(), entry.getValue());
				}
			}
			// 设置参数
			Builder customReqConf = RequestConfig.custom();
			if (connTimeout != null) {
				customReqConf.setConnectTimeout(connTimeout);
			}
			if (readTimeout != null) {
				customReqConf.setSocketTimeout(readTimeout);
			}
			post.setConfig(customReqConf.build());
			HttpResponse res = null;
			if (url.startsWith("https")) {
				// 执行 Https 请求.
				client = createSSLInsecureClient();
				res = client.execute(post);
			} else {
				// 执行 Http 请求.
				client = HttpClientUtils.client;
				res = client.execute(post);
			}
			return IOUtils.toString(res.getEntity().getContent(), "UTF-8");
		} finally {
			post.releaseConnection();
			if (url.startsWith("https") && client != null
					&& client instanceof CloseableHttpClient) {
				((CloseableHttpClient) client).close();
			}
		}
	}




	/**
	 * 发送一个 GET 请求
	 *
	 * @param url
	 * @param charset
	 * @param connTimeout  建立链接超时时间,毫秒.
	 * @param readTimeout  响应超时时间,毫秒.
	 * @return
	 * @throws ConnectTimeoutException   建立链接超时
	 * @throws SocketTimeoutException   响应超时
	 * @throws Exception
	 */
	public static String get(String url, String charset, Integer connTimeout,Integer readTimeout)
			throws ConnectTimeoutException,SocketTimeoutException, Exception {

		HttpClient client = null;
		HttpGet get = new HttpGet(url);
		String result = "";
		try {
			// 设置参数
			Builder customReqConf = RequestConfig.custom();
			if (connTimeout != null) {
				customReqConf.setConnectTimeout(connTimeout);
			}
			if (readTimeout != null) {
				customReqConf.setSocketTimeout(readTimeout);
			}
			get.setConfig(customReqConf.build());

			HttpResponse res = null;

			if (url.startsWith("https")) {
				// 执行 Https 请求.
				client = createSSLInsecureClient();
				res = client.execute(get);
			} else {
				// 执行 Http 请求.
				client = HttpClientUtils.client;
				res = client.execute(get);
			}

			result = IOUtils.toString(res.getEntity().getContent(), charset);
		} finally {
			get.releaseConnection();
			if (url.startsWith("https") && client != null && client instanceof CloseableHttpClient) {
				((CloseableHttpClient) client).close();
			}
		}
		return result;
	}


	/**
	 * 从 response 里获取 charset
	 *
	 * @param ressponse
	 * @return
	 */
	@SuppressWarnings("unused")
	private static String getCharsetFromResponse(HttpResponse ressponse) {
		// Content-Type:text/html; charset=GBK
		if (ressponse.getEntity() != null  && ressponse.getEntity().getContentType() != null && ressponse.getEntity().getContentType().getValue() != null) {
			String contentType = ressponse.getEntity().getContentType().getValue();
			if (contentType.contains("charset=")) {
				return contentType.substring(contentType.indexOf("charset=") + 8);
			}
		}
		return null;
	}



	/**
	 * 创建 SSL连接
	 * @return
	 * @throws GeneralSecurityException
	 */
	private static CloseableHttpClient createSSLInsecureClient() throws GeneralSecurityException {
		try {
			SSLContext sslContext = new SSLContextBuilder().loadTrustMaterial(null, new TrustStrategy() {
				public boolean isTrusted(X509Certificate[] chain,String authType) throws CertificateException {
					return true;
				}
			}).build();

			SSLConnectionSocketFactory sslsf = new SSLConnectionSocketFactory(sslContext, new X509HostnameVerifier() {

				@Override
				public boolean verify(String arg0, SSLSession arg1) {
					return true;
				}

				@Override
				public void verify(String host, SSLSocket ssl)
						throws IOException {
				}

				@Override
				public void verify(String host, X509Certificate cert)
						throws SSLException {
				}

				@Override
				public void verify(String host, String[] cns,
								   String[] subjectAlts) throws SSLException {
				}

			});

			return HttpClients.custom().setSSLSocketFactory(sslsf).build();

		} catch (GeneralSecurityException e) {
			throw e;
		}
	}

	public static void main(String[] args) {
		try {
			String str= post("https://localhost:443/ssl/test.shtml","name=12&page=34","application/x-www-form-urlencoded", "UTF-8", 10000, 10000);
			//String str= get("https://localhost:443/ssl/test.shtml?name=12&page=34","GBK");
            /*Map<String,String> map = new HashMap<String,String>();
            map.put("name", "111");
            map.put("page", "222");
            String str= postForm("https://localhost:443/ssl/test.shtml",map,null, 10000, 10000);*/
			System.out.println(str);
		} catch (ConnectTimeoutException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SocketTimeoutException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

}
```

## 16.7完善扫码登陆

根据微信信息使用jwt 生成token字符串，把token字符串通过路径返回页面

因为cookie不能实现跨域

```java
	/**
     * 获取扫描人信息,添加数据
     */
    @GetMapping("callback")
    public String callback(String code,String state){


        try {
            //获取code,类似于验证码
            //拿到code去请求微信固定的地址，得到的两个值去请求 access_token和 openid
            String baseUrl = "https://api.weixin.qq.com/sns/oauth2/access_token" +
                    "?appid=%s" +
                    "&secret=%s" +
                    "&code=%s" +
                    "&grant_type=authorization_code";
            String url = String.format(
                    baseUrl,
                    ConstantWxUtils.WX_OPEN_APP_ID,
                    ConstantWxUtils.WX_OPEN_APP_SECRET,
                    code
            );
            //请求这个地址 使用httpClient
            String accessTokenInfo = HttpClientUtils.get(url);

            //字符串转 json
            Gson gson = new Gson();
            HashMap map = gson.fromJson(accessTokenInfo, HashMap.class);
            String access_token =(String) map.get("access_token");
            String openid = (String) map.get("openid");


            UcenterMember member = memberService.getOpenIdMember(openid);
            System.out.println("查询的数据为："+member);
            if(member == null){//表里没有 就添加
                //拿着信息再去请求固定地址用户信息
                String BaseUserInfoUrl = "https://api.weixin.qq.com/sns/userinfo" +
                        "?access_token=%s" +
                        "&openid=%s";
                String UserInfoUrl =  String.format(
                        BaseUserInfoUrl,
                        access_token,
                        openid
                    );
                //请求这个地址 使用httpClient
                String userInfo = HttpClientUtils.get(UserInfoUrl);
                //获取到用户信息
                HashMap userInfoMap = gson.fromJson(userInfo, HashMap.class);
                String nickname = (String) userInfoMap.get("nickname");
                String headimgurl = (String) userInfoMap.get("headimgurl");

                //添加到数据库
                //判断数据库是否存在相同的微信信息
                //根据openid判断
                member = new UcenterMember();
                member.setOpenid(openid);
                member.setNickname(nickname);
                member.setAvatar(headimgurl);
                //保存
                memberService.save(member);
            }

            //把memeber信息生成token
            String token = JwtUtils.getJwtToken(member.getId(), member.getNickname());
            //拼接到后面
            return "redirect:http://localhost:3000?token="+token;

        } catch (Exception e) {
            e.printStackTrace();
            throw new GuliExecption(20001,"登陆失败");
        }

    }
```

getOpenIdMember   服务层代码

```java
@Override
    public UcenterMember getOpenIdMember(String openid) {
        QueryWrapper<UcenterMember> wrapper = new QueryWrapper();
        wrapper.eq("openid",openid);
        UcenterMember member = baseMapper.selectOne(wrapper);
        return member;
    }
```

# 17.微信支付

申请微信支付账号

```xml
 <!--  微信支付依赖  -->
    <dependencies>
        <dependency>
            <groupId>com.github.wxpay</groupId>
            <artifactId>wxpay-sdk</artifactId>
            <version>0.0.3</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
        </dependency>
    </dependencies>
```

业务层代码

## 17.1生成二维码

```java
/**
     * 生成二维码
     * @param orderNo
     * @return
     */
    @Override
    public Map<String, Object> createNative(String orderNo) {
        try {
            //1 根据订单号查询订单信息
            QueryWrapper<TOrder> wrapper = new QueryWrapper<>();
            wrapper.eq("order_no",orderNo);
            TOrder order = tOrderService.getOne(wrapper);

            //2 使用map设置生成二维码需要参数
            Map m = new HashMap();
            m.put("appid","wx74862e0dfcf69954");
            m.put("mch_id", "1558950191");
            m.put("nonce_str", WXPayUtil.generateNonceStr());
            m.put("body", order.getCourseTitle()); //课程标题
            m.put("out_trade_no", orderNo); //订单号
            m.put("total_fee", order.getTotalFee().multiply(new BigDecimal("100")).longValue()+"");
            m.put("spbill_create_ip", "127.0.0.1");
            m.put("notify_url", "http://guli.shop/api/order/weixinPay/weixinNotify\n");
            m.put("trade_type", "NATIVE");

            //3 发送httpclient请求，传递参数xml格式，微信支付提供的固定的地址
            HttpClient client = new HttpClient("https://api.mch.weixin.qq.com/pay/unifiedorder");
            //设置xml格式的参数
            client.setXmlParam(WXPayUtil.generateSignedXml(m,"T6m9iK73b0kn9g5v426MKfHQH7X8rKwb"));
            client.setHttps(true);
            //执行post请求发送
            client.post();

            //4 得到发送请求返回结果
            //返回内容，是使用xml格式返回
            String xml = client.getContent();

            //把xml格式转换map集合，把map集合返回
            Map<String,String> resultMap = WXPayUtil.xmlToMap(xml);

            //最终返回数据 的封装
            Map map = new HashMap();
            map.put("out_trade_no", orderNo);
            map.put("course_id", order.getCourseId());
            map.put("total_fee", order.getTotalFee());
            map.put("result_code", resultMap.get("result_code"));  //返回二维码操作状态码
            map.put("code_url", resultMap.get("code_url"));        //二维码地址

            return map;
        }catch(Exception e) {
            throw new GuliExecption(20001,"生成二维码失败");
        }
    }
```

## 17.2查询状态

```java
 /**
     * 查询支付状态
     * @param orderNo
     * @return
     */
    @Override
    public Map<String, String> queryPayStatus(String orderNo) {
        try {
            //1、封装参数
            Map m = new HashMap<>();
            m.put("appid", "wx74862e0dfcf69954");
            m.put("mch_id", "1558950191");
            m.put("out_trade_no", orderNo);
            m.put("nonce_str", WXPayUtil.generateNonceStr());

            //2 发送httpclient
            HttpClient client = new HttpClient("https://api.mch.weixin.qq.com/pay/orderquery");
            client.setXmlParam(WXPayUtil.generateSignedXml(m,"T6m9iK73b0kn9g5v426MKfHQH7X8rKwb"));
            client.setHttps(true);
            client.post();

            //3 得到请求返回内容
            String xml = client.getContent();
            Map<String, String> resultMap = WXPayUtil.xmlToMap(xml);
            //6、转成Map再返回
            return resultMap;
        }catch(Exception e) {
            return null;
        }
    }

```

## 17.3添加支付记录设置订单状态

```java
 /**
     * 更新字段
     * @param map
     */
    @Override
    public void updateOrderStatus(Map<String, String> map) {

        //从map获取订单号
        String orderNo = map.get("out_trade_no");
        //根据订单号查询订单信息
        QueryWrapper<TOrder> wrapper = new QueryWrapper<>();
        wrapper.eq("order_no",orderNo);
        TOrder order = tOrderService.getOne(wrapper);

        //更新订单表订单状态
        if(order.getStatus().intValue() == 1) { return; }
        order.setStatus(1);//1代表已经支付
        tOrderService.updateById(order);

        //向支付表添加支付记录
        TPayLog payLog = new TPayLog();
        payLog.setOrderNo(orderNo);  //订单号
        payLog.setPayTime(new Date()); //订单完成时间
        payLog.setPayType(1);//支付类型 1微信
        payLog.setTotalFee(order.getTotalFee());//总金额(分)

        payLog.setTradeState(map.get("trade_state"));//支付状态
        payLog.setTransactionId(map.get("transaction_id")); //流水号
        payLog.setAttr(JSONObject.toJSONString(map));

        baseMapper.insert(payLog);

    }
```

controller整合

```java
/**
     * 查询订单支付状态
     */
    @GetMapping("queryPayStatus/{orderNo}")
    public R queryPayStatus(@PathVariable String orderNo){
        Map<String,String> map = payLogService.queryPayStatus(orderNo);
        System.out.println(map);
        if(map == null){
            return R.error().message("支付出错");
        }
        if(map.get("trade_state").equals("SUCCESS")){
            //添加支付记录到支付表
            payLogService.updateOrderStatus(map);
            return R.ok().message("支付成功");
        }
        return R.ok().code(20005).message("支付中");
    }
```

# 18.canal 数据同步工具

## 18.1介绍

https://blog.csdn.net/yehongzhi1994/article/details/107880162

```
在以前的统计分析中,我们采用服务调用的方式获取统计数据,这样耦合度高效率低
通过实时同步 数据库表的方式  cannal就是一个数据库同步工具
远程库里面的内容同步到   本地库里面的内容

java开发的工具

//目前只支持  MYSQL
```

## 18.2 canal环境搭建

```mysql
canal的原理是mysql binlog技术
所有一定要开启 mysql的 binlog功能

步骤
	1.开启linux mysql                service mysql start
	2.检查 binlog功能是否开启   show variables like 'log_bin'
	3.未开启  修改mysql的配置文件    追加内容
		log-bin-mysql-bin     #binlog文件名
		binlog_format=ROW      #选择ROW模式
		server  id-1           #mysql示例id   不能和canal的slaveId 重复
	4.重启mysql    service mysql restart
	5.mysql里面  添加  以下用户权限和相关用户
		CREATE USER 'canal'@'%' IDENTIFIED BY 'canal';
		GRANT SHOW VIEW,SELECT,REPLICATION SLAVE,REPLICATION ON *.* TO 'canal'@'%';
		FLUSH PRIVILEGES;
```

## 18.3 canal安装

```
https://github.com/alibaba/canal/releases

canal压缩文件上传到
	解压
```

接着打开配置文件conf/example/instance.properties，配置信息如下：

```properties
## mysql serverId , v1.0.26+ will autoGen
## v1.0.26版本后会自动生成slaveId，所以可以不用配置
# canal.instance.mysql.slaveId=0

# 数据库地址
canal.instance.master.address=127.0.0.1:3306
# binlog日志名称
canal.instance.master.journal.name=mysql-bin.000001
# mysql主库链接时起始的binlog偏移量
canal.instance.master.position=154
# mysql主库链接时起始的binlog的时间戳
canal.instance.master.timestamp=
canal.instance.master.gtid=

# username/password
# 在MySQL服务器授权的账号密码
canal.instance.dbUsername=canal
canal.instance.dbPassword=Canal@123456
# 字符集
canal.instance.connectionCharset = UTF-8
# enable druid Decrypt database password
canal.instance.enableDruid=false

# table regex .*\\..*表示监听所有表 也可以写具体的表名，用，隔开
canal.instance.filter.regex=.*\\..*
# mysql 数据解析表的黑名单，多个表用，隔开
canal.instance.filter.black.regex=
```

## 18.4创建模块

```java
启动类
@SpringBootApplication
public class CanalApplication implements CommandLineRunner {
    @Resource
    private CanalClient canalClient;

    public static void main(String[] args) {
        SpringApplication.run(CanalApplication.class, args);
    }

    @Override
    public void run(String... strings) throws Exception {
        //项目启动，执行canal客户端监听
        canalClient.run();
    }
}
```

## 18.4客户代码

```java
package com.example.canal.client;

import com.alibaba.otter.canal.client.CanalConnector;
import com.alibaba.otter.canal.client.CanalConnectors;
import com.alibaba.otter.canal.protocol.CanalEntry.*;
import com.alibaba.otter.canal.protocol.Message;
import com.google.protobuf.InvalidProtocolBufferException;
import org.apache.commons.dbutils.DbUtils;
import org.apache.commons.dbutils.QueryRunner;
import org.springframework.stereotype.Component;

import javax.annotation.Resource;
import javax.sql.DataSource;
import java.net.InetSocketAddress;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.Iterator;
import java.util.List;
import java.util.Queue;
import java.util.concurrent.ConcurrentLinkedQueue;

@Component
public class CanalClient {

    //sql队列
    private Queue<String> SQL_QUEUE = new ConcurrentLinkedQueue<>();

    @Resource
    private DataSource dataSource;

    /**
     * canal入库方法
     */
    public void run() {

        CanalConnector connector = CanalConnectors.newSingleConnector(new InetSocketAddress("192.168.44.132",
                11111), "example", "", "");
        int batchSize = 1000;
        try {
            connector.connect();
            connector.subscribe(".*\\..*");
            connector.rollback();
            try {
                while (true) {
                    //尝试从master那边拉去数据batchSize条记录，有多少取多少
                    Message message = connector.getWithoutAck(batchSize);
                    long batchId = message.getId();
                    int size = message.getEntries().size();
                    if (batchId == -1 || size == 0) {
                        Thread.sleep(1000);
                    } else {
                        dataHandle(message.getEntries());
                    }
                    connector.ack(batchId);

                    //当队列里面堆积的sql大于一定数值的时候就模拟执行
                    if (SQL_QUEUE.size() >= 1) {
                        executeQueueSql();
                    }
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            } catch (InvalidProtocolBufferException e) {
                e.printStackTrace();
            }
        } finally {
            connector.disconnect();
        }
    }

    /**
     * 模拟执行队列里面的sql语句
     */
    public void executeQueueSql() {
        int size = SQL_QUEUE.size();
        for (int i = 0; i < size; i++) {
            String sql = SQL_QUEUE.poll();
            System.out.println("[sql]----> " + sql);

            this.execute(sql.toString());
        }
    }

    /**
     * 数据处理
     *
     * @param entrys
     */
    private void dataHandle(List<Entry> entrys) throws InvalidProtocolBufferException {
        for (Entry entry : entrys) {
            if (EntryType.ROWDATA == entry.getEntryType()) {
                RowChange rowChange = RowChange.parseFrom(entry.getStoreValue());
                EventType eventType = rowChange.getEventType();
                if (eventType == EventType.DELETE) {
                    saveDeleteSql(entry);
                } else if (eventType == EventType.UPDATE) {
                    saveUpdateSql(entry);
                } else if (eventType == EventType.INSERT) {
                    saveInsertSql(entry);
                }
            }
        }
    }

    /**
     * 保存更新语句
     *
     * @param entry
     */
    private void saveUpdateSql(Entry entry) {
        try {
            RowChange rowChange = RowChange.parseFrom(entry.getStoreValue());
            List<RowData> rowDatasList = rowChange.getRowDatasList();
            for (RowData rowData : rowDatasList) {
                List<Column> newColumnList = rowData.getAfterColumnsList();
                StringBuffer sql = new StringBuffer("update " + entry.getHeader().getTableName() + " set ");
                for (int i = 0; i < newColumnList.size(); i++) {
                    sql.append(" " + newColumnList.get(i).getName()
                            + " = '" + newColumnList.get(i).getValue() + "'");
                    if (i != newColumnList.size() - 1) {
                        sql.append(",");
                    }
                }
                sql.append(" where ");
                List<Column> oldColumnList = rowData.getBeforeColumnsList();
                for (Column column : oldColumnList) {
                    if (column.getIsKey()) {
                        //暂时只支持单一主键
                        sql.append(column.getName() + "=" + column.getValue());
                        break;
                    }
                }
                SQL_QUEUE.add(sql.toString());
            }
        } catch (InvalidProtocolBufferException e) {
            e.printStackTrace();
        }
    }

    /**
     * 保存删除语句
     *
     * @param entry
     */
    private void saveDeleteSql(Entry entry) {
        try {
            RowChange rowChange = RowChange.parseFrom(entry.getStoreValue());
            List<RowData> rowDatasList = rowChange.getRowDatasList();
            for (RowData rowData : rowDatasList) {
                List<Column> columnList = rowData.getBeforeColumnsList();
                StringBuffer sql = new StringBuffer("delete from " + entry.getHeader().getTableName() + " where ");
                for (Column column : columnList) {
                    if (column.getIsKey()) {
                        //暂时只支持单一主键
                        sql.append(column.getName() + "=" + column.getValue());
                        break;
                    }
                }
                SQL_QUEUE.add(sql.toString());
            }
        } catch (InvalidProtocolBufferException e) {
            e.printStackTrace();
        }
    }

    /**
     * 保存插入语句
     *
     * @param entry
     */
    private void saveInsertSql(Entry entry) {
        try {
            RowChange rowChange = RowChange.parseFrom(entry.getStoreValue());
            List<RowData> rowDatasList = rowChange.getRowDatasList();
            for (RowData rowData : rowDatasList) {
                List<Column> columnList = rowData.getAfterColumnsList();
                StringBuffer sql = new StringBuffer("insert into " + entry.getHeader().getTableName() + " (");
                for (int i = 0; i < columnList.size(); i++) {
                    sql.append(columnList.get(i).getName());
                    if (i != columnList.size() - 1) {
                        sql.append(",");
                    }
                }
                sql.append(") VALUES (");
                for (int i = 0; i < columnList.size(); i++) {
                    sql.append("'" + columnList.get(i).getValue() + "'");
                    if (i != columnList.size() - 1) {
                        sql.append(",");
                    }
                }
                sql.append(")");
                SQL_QUEUE.add(sql.toString());
            }
        } catch (InvalidProtocolBufferException e) {
            e.printStackTrace();
        }
    }

    /**
     * 入库
     * @param sql
     */
    public void execute(String sql) {
        Connection con = null;
        try {
            if(null == sql) return;
            con = dataSource.getConnection();
            QueryRunner qr = new QueryRunner();
            int row = qr.execute(con, sql);
            System.out.println("update: "+ row);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            DbUtils.closeQuietly(con);
        }
    }
}

```

# 19.权限管理

## 19.1表结构

```mysql
# Host: localhost  (Version 5.7.19)
# Date: 2019-11-18 15:49:15
# Generator: MySQL-Front 6.1  (Build 1.26)


#
# Structure for table "acl_permission"
#

CREATE TABLE `acl_permission` (
  `id` char(19) NOT NULL DEFAULT '' COMMENT '编号',
  `pid` char(19) NOT NULL DEFAULT '' COMMENT '所属上级',
  `name` varchar(20) NOT NULL DEFAULT '' COMMENT '名称',
  `type` tinyint(3) NOT NULL DEFAULT '0' COMMENT '类型(1:菜单,2:按钮)',
  `permission_value` varchar(50) DEFAULT NULL COMMENT '权限值',
  `path` varchar(100) DEFAULT NULL COMMENT '访问路径',
  `component` varchar(100) DEFAULT NULL COMMENT '组件路径',
  `icon` varchar(50) DEFAULT NULL COMMENT '图标',
  `status` tinyint(4) DEFAULT NULL COMMENT '状态(0:禁止,1:正常)',
  `is_deleted` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '逻辑删除 1（true）已删除， 0（false）未删除',
  `gmt_create` datetime DEFAULT NULL COMMENT '创建时间',
  `gmt_modified` datetime DEFAULT NULL COMMENT '更新时间',
  PRIMARY KEY (`id`),
  KEY `idx_pid` (`pid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='权限';

#
# Data for table "acl_permission"
#


#
# Structure for table "acl_role"
#

CREATE TABLE `acl_role` (
  `id` char(19) NOT NULL DEFAULT '' COMMENT '角色id',
  `role_name` varchar(20) NOT NULL DEFAULT '' COMMENT '角色名称',
  `role_code` varchar(20) DEFAULT NULL COMMENT '角色编码',
  `remark` varchar(255) DEFAULT NULL COMMENT '备注',
  `is_deleted` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '逻辑删除 1（true）已删除， 0（false）未删除',
  `gmt_create` datetime NOT NULL COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL COMMENT '更新时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

#
# Data for table "acl_role"
#

INSERT INTO `acl_role` VALUES ('1','普通管理员',NULL,NULL,0,'2019-11-11 13:09:32','2019-11-18 10:27:18'),('1193757683205607426','课程管理员',NULL,NULL,0,'2019-11-11 13:09:45','2019-11-18 10:25:44'),('1196300996034977794','test',NULL,NULL,0,'2019-11-18 13:35:58','2019-11-18 13:35:58');

#
# Structure for table "acl_role_permission"
#

CREATE TABLE `acl_role_permission` (
  `id` char(19) NOT NULL DEFAULT '',
  `role_id` char(19) NOT NULL DEFAULT '',
  `permission_id` char(19) NOT NULL DEFAULT '',
  `is_deleted` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '逻辑删除 1（true）已删除， 0（false）未删除',
  `gmt_create` datetime NOT NULL COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL COMMENT '更新时间',
  PRIMARY KEY (`id`),
  KEY `idx_role_id` (`role_id`),
  KEY `idx_permission_id` (`permission_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='角色权限';



#
# Structure for table "acl_user"
#

CREATE TABLE `acl_user` (
  `id` char(19) NOT NULL COMMENT '会员id',
  `username` varchar(20) NOT NULL DEFAULT '' COMMENT '微信openid',
  `password` varchar(32) NOT NULL DEFAULT '' COMMENT '密码',
  `nick_name` varchar(50) DEFAULT NULL COMMENT '昵称',
  `salt` varchar(255) DEFAULT NULL COMMENT '用户头像',
  `token` varchar(100) DEFAULT NULL COMMENT '用户签名',
  `is_deleted` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '逻辑删除 1（true）已删除， 0（false）未删除',
  `gmt_create` datetime NOT NULL COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL COMMENT '更新时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_username` (`username`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='用户表';

#
# Data for table "acl_user"
#

INSERT INTO `acl_user` VALUES ('1','admin','96e79218965eb72c92a549dd5a330112','admin','',NULL,0,'2019-11-01 10:39:47','2019-11-01 10:39:47'),('2','test','96e79218965eb72c92a549dd5a330112','test',NULL,NULL,0,'2019-11-01 16:36:07','2019-11-01 16:40:08');

#
# Structure for table "acl_user_role"
#

CREATE TABLE `acl_user_role` (
  `id` char(19) NOT NULL DEFAULT '' COMMENT '主键id',
  `role_id` char(19) NOT NULL DEFAULT '0' COMMENT '角色id',
  `user_id` char(19) NOT NULL DEFAULT '0' COMMENT '用户id',
  `is_deleted` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '逻辑删除 1（true）已删除， 0（false）未删除',
  `gmt_create` datetime NOT NULL COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL COMMENT '更新时间',
  PRIMARY KEY (`id`),
  KEY `idx_role_id` (`role_id`),
  KEY `idx_user_id` (`user_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

#
# Data for table "acl_user_role"
#

INSERT INTO `acl_user_role` VALUES ('1','1','2',0,'2019-11-11 13:09:53','2019-11-11 13:09:53');
```

## 19.2依赖引入

```xml
    <dependencies>
<!--        <dependency>-->
<!--            <groupId>com.example</groupId>-->
<!--            <artifactId>spring_security</artifactId>-->
<!--            <version>0.0.1-SNAPSHOT</version>-->
<!--        </dependency>-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
        </dependency>
    </dependencies>

```

## 19.3递归查询获取菜单

```java
    //========================递归查询所有菜单================================================
    //获取全部菜单
    @Override
    public List<Permission> queryAllMenuGuli() {
        //1 查询菜单表所有数据
        QueryWrapper<Permission> wrapper = new QueryWrapper<>();
        wrapper.orderByDesc("id");
        List<Permission> permissionList = baseMapper.selectList(wrapper);
        //2 把查询所有菜单list集合按照要求进行封装
        List<Permission> resultList = bulidPermission(permissionList);
        return resultList;
    }

    //把返回所有菜单list集合进行封装的方法
    public static List<Permission> bulidPermission(List<Permission> permissionList) {

        //创建list集合，用于数据最终封装
        List<Permission> finalNode = new ArrayList<>();
        //把所有菜单list集合遍历，得到顶层菜单 pid=0菜单，设置level是1
        for(Permission permissionNode : permissionList) {
            //得到顶层菜单 pid=0菜单
            if("0".equals(permissionNode.getPid())) {
                //设置顶层菜单的level是1
                permissionNode.setLevel(1);
                //根据顶层菜单，向里面进行查询子菜单，封装到finalNode里面
                finalNode.add(selectChildren(permissionNode,permissionList));
            }
        }
        return finalNode;
    }

    private static Permission selectChildren(Permission permissionNode, List<Permission> permissionList) {
        //1 因为向一层菜单里面放二层菜单，二层里面还要放三层，把对象初始化
        permissionNode.setChildren(new ArrayList<Permission>());

        //2 遍历所有菜单list集合，进行判断比较，比较id和pid值是否相同
        for(Permission it : permissionList) {
            //判断 id和pid值是否相同
            if(permissionNode.getId().equals(it.getPid())) {
                //把父菜单的level值+1
                int level = permissionNode.getLevel()+1;
                it.setLevel(level);
                //如果children为空，进行初始化操作
                if(permissionNode.getChildren() == null) {
                    permissionNode.setChildren(new ArrayList<Permission>());
                }
                //把查询出来的子菜单放到父菜单里面
                permissionNode.getChildren().add(selectChildren(it,permissionList));
            }
        }
        return permissionNode;
    }
```

注意swagger

```java
//                .paths(Predicates.not(PathSelectors.regex("/admin/.*")))//包含匹配
```

## 19.4介绍

```
包含两部分  
	用户认证 、  登陆用户名密码认证成功
	用户授权	普通用户 管理员权限
	
	本质上是过滤器
	
	
	执行流程
		
		登陆用户名密码
		查询权限列表，在redis里面储存key  value  权限信息
		返回token   拿到token 下次请求携带 
		从token获取的用户id 
		拿着用户名从redis获取权限列表
		security给涌胡赋予权限
```

## 19.5依赖引入

```xml
    <dependencies>
        <dependency>
            <groupId>com.example</groupId>
            <artifactId>common_utils</artifactId>
            <version>0.0.1-SNAPSHOT</version>
        </dependency>
        <!-- Spring Security依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>

        <dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt</artifactId>
        </dependency>
    </dependencies>

```

## 19.6核心代码

### 19.6.1核心配置类  

包含核心配置,密码处理,那些请求不拦截。

```java

/**
 * <p>
 * Security配置类
 * </p>
 *
 * @author qy
 * @since 2019-11-18
 */
@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class TokenWebSecurityConfig extends WebSecurityConfigurerAdapter {

    private UserDetailsService userDetailsService;
    private TokenManager tokenManager;
    private DefaultPasswordEncoder defaultPasswordEncoder;
    private RedisTemplate redisTemplate;

    @Autowired
    public TokenWebSecurityConfig(UserDetailsService userDetailsService, DefaultPasswordEncoder defaultPasswordEncoder,
                                  TokenManager tokenManager, RedisTemplate redisTemplate) {
        this.userDetailsService = userDetailsService;
        this.defaultPasswordEncoder = defaultPasswordEncoder;
        this.tokenManager = tokenManager;
        this.redisTemplate = redisTemplate;
    }

    /**
     * 配置设置
     * @param http
     * @throws Exception
     */
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.exceptionHandling()
                .authenticationEntryPoint(new UnauthorizedEntryPoint())
                .and().csrf().disable()
                .authorizeRequests()
                .anyRequest().authenticated()
                .and().logout().logoutUrl("/admin/acl/index/logout")
                .addLogoutHandler(new TokenLogoutHandler(tokenManager,redisTemplate)).and()
                .addFilter(new TokenLoginFilter(authenticationManager(), tokenManager, redisTemplate))
                .addFilter(new TokenAuthenticationFilter(authenticationManager(), tokenManager, redisTemplate)).httpBasic();
    }

    /**
     * 密码处理
     * @param auth
     * @throws Exception
     */
    @Override
    public void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userDetailsService).passwordEncoder(defaultPasswordEncoder);
    }

    /**
     * 配置哪些请求不拦截
     * @param web
     * @throws Exception
     */
    @Override
    public void configure(WebSecurity web) throws Exception {
        web.ignoring().antMatchers("/api/**",
                "/swagger-resources/**", "/webjars/**", "/v2/**", "/swagger-ui.html/**"
               );
    }
}
```

### 19.6.2当前用户实体类

```java
@Data
@Slf4j
public class SecurityUser implements UserDetails {

    //当前登录用户
    private transient User currentUserInfo;

    //当前权限
    private List<String> permissionValueList;

    public SecurityUser() {
    }

    public SecurityUser(User user) {
        if (user != null) {
            this.currentUserInfo = user;
        }
    }

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        Collection<GrantedAuthority> authorities = new ArrayList<>();
        for(String permissionValue : permissionValueList) {
            if(StringUtils.isEmpty(permissionValue)) continue;
            SimpleGrantedAuthority authority = new SimpleGrantedAuthority(permissionValue);
            authorities.add(authority);
        }

        return authorities;
    }

    @Override
    public String getPassword() {
        return currentUserInfo.getPassword();
    }

    @Override
    public String getUsername() {
        return currentUserInfo.getUsername();
    }

    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @Override
    public boolean isEnabled() {
        return true;
    }
}

```

```java

@Data
@ApiModel(description = "用户实体类")
public class User implements Serializable {

	private static final long serialVersionUID = 1L;

	@ApiModelProperty(value = "微信openid")
	private String username;

	@ApiModelProperty(value = "密码")
	private String password;

	@ApiModelProperty(value = "昵称")
	private String nickName;

	@ApiModelProperty(value = "用户头像")
	private String salt;

	@ApiModelProperty(value = "用户签名")
	private String token;

}

```

### 19.6.3登录过滤器

```java

public class TokenLoginFilter extends UsernamePasswordAuthenticationFilter {

    private AuthenticationManager authenticationManager;
    private TokenManager tokenManager;
    private RedisTemplate redisTemplate;

    public TokenLoginFilter(AuthenticationManager authenticationManager, TokenManager tokenManager, RedisTemplate redisTemplate) {
        this.authenticationManager = authenticationManager;
        this.tokenManager = tokenManager;
        this.redisTemplate = redisTemplate;
        this.setPostOnly(false);
        this.setRequiresAuthenticationRequestMatcher(new AntPathRequestMatcher("/admin/acl/login","POST"));
    }

    @Override
    public Authentication attemptAuthentication(HttpServletRequest req, HttpServletResponse res)
            throws AuthenticationException {
        try {
            User user = new ObjectMapper().readValue(req.getInputStream(), User.class);

            return authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(user.getUsername(), user.getPassword(), new ArrayList<>()));
        } catch (IOException e) {
            throw new RuntimeException(e);
        }

    }

    /**
     * 登录成功
     * @param req
     * @param res
     * @param chain
     * @param auth
     * @throws IOException
     * @throws ServletException
     */
    @Override
    protected void successfulAuthentication(HttpServletRequest req, HttpServletResponse res, FilterChain chain,
                                            Authentication auth) throws IOException, ServletException {
        SecurityUser user = (SecurityUser) auth.getPrincipal();
        String token = tokenManager.createToken(user.getCurrentUserInfo().getUsername());
        redisTemplate.opsForValue().set(user.getCurrentUserInfo().getUsername(), user.getPermissionValueList());

        ResponseUtil.out(res, R.ok().data("token", token));
    }

    /**
     * 登录失败
     * @param request
     * @param response
     * @param e
     * @throws IOException
     * @throws ServletException
     */
    @Override
    protected void unsuccessfulAuthentication(HttpServletRequest request, HttpServletResponse response,
                                              AuthenticationException e) throws IOException, ServletException {
        ResponseUtil.out(response, R.error());
    }
}

```

### 19.6.4授权过滤器

```java
public class TokenAuthenticationFilter extends BasicAuthenticationFilter {
    private TokenManager tokenManager;
    private RedisTemplate redisTemplate;

    public TokenAuthenticationFilter(AuthenticationManager authManager, TokenManager tokenManager,RedisTemplate redisTemplate) {
        super(authManager);
        this.tokenManager = tokenManager;
        this.redisTemplate = redisTemplate;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest req, HttpServletResponse res, FilterChain chain)
            throws IOException, ServletException {
        logger.info("================="+req.getRequestURI());
        if(req.getRequestURI().indexOf("admin") == -1) {
            chain.doFilter(req, res);
            return;
        }

        UsernamePasswordAuthenticationToken authentication = null;
        try {
            authentication = getAuthentication(req);
        } catch (Exception e) {
            ResponseUtil.out(res, R.error());
        }

        if (authentication != null) {
            SecurityContextHolder.getContext().setAuthentication(authentication);
        } else {
            ResponseUtil.out(res, R.error());
        }
        chain.doFilter(req, res);
    }

    private UsernamePasswordAuthenticationToken getAuthentication(HttpServletRequest request) {
        // token置于header里
        String token = request.getHeader("token");
        if (token != null && !"".equals(token.trim())) {
            String userName = tokenManager.getUserFromToken(token);

            List<String> permissionValueList = (List<String>) redisTemplate.opsForValue().get(userName);
            Collection<GrantedAuthority> authorities = new ArrayList<>();
            for(String permissionValue : permissionValueList) {
                if(StringUtils.isEmpty(permissionValue)) continue;
                SimpleGrantedAuthority authority = new SimpleGrantedAuthority(permissionValue);
                authorities.add(authority);
            }

            if (!StringUtils.isEmpty(userName)) {
                return new UsernamePasswordAuthenticationToken(userName, token, authorities);
            }
            return null;
        }
        return null;
    }
}
```

### 19.6.5工具类

密码处理

```java
@Component
public class DefaultPasswordEncoder implements PasswordEncoder {

    public DefaultPasswordEncoder() {
        this(-1);
    }

    /**
     * @param strength
     *            the log rounds to use, between 4 and 31
     */
    public DefaultPasswordEncoder(int strength) {

    }

    public String encode(CharSequence rawPassword) {
        return MD5.encrypt(rawPassword.toString());
    }

    public boolean matches(CharSequence rawPassword, String encodedPassword) {
        return encodedPassword.equals(MD5.encrypt(rawPassword.toString()));
    }
}
```

退出

```java
public class TokenLogoutHandler implements LogoutHandler {

    private TokenManager tokenManager;
    private RedisTemplate redisTemplate;

    public TokenLogoutHandler(TokenManager tokenManager, RedisTemplate redisTemplate) {
        this.tokenManager = tokenManager;
        this.redisTemplate = redisTemplate;
    }

    @Override
    public void logout(HttpServletRequest request, HttpServletResponse response, Authentication authentication) {
        String token = request.getHeader("token");
        if (token != null) {
            tokenManager.removeToken(token);

            //清空当前用户缓存中的权限数据
            String userName = tokenManager.getUserFromToken(token);
            redisTemplate.delete(userName);
        }
        ResponseUtil.out(response, R.ok());
    }

}
```

token工具类

```java
@Component
public class TokenManager {

    private long tokenExpiration = 24*60*60*1000;
    private String tokenSignKey = "123456";

    public String createToken(String username) {
        String token = Jwts.builder().setSubject(username)
                .setExpiration(new Date(System.currentTimeMillis() + tokenExpiration))
                .signWith(SignatureAlgorithm.HS512, tokenSignKey).compressWith(CompressionCodecs.GZIP).compact();
        return token;
    }

    public String getUserFromToken(String token) {
        String user = Jwts.parser().setSigningKey(tokenSignKey).parseClaimsJws(token).getBody().getSubject();
        return user;
    }

    public void removeToken(String token) {
        //jwttoken无需删除，客户端扔掉即可。
    }

}

```

没有权限统一处理

```java
public class UnauthorizedEntryPoint implements AuthenticationEntryPoint {

    @Override
    public void commence(HttpServletRequest request, HttpServletResponse response,
                         AuthenticationException authException) throws IOException, ServletException {

        ResponseUtil.out(response, R.error());
    }
}

```

### 19.6.6创建查询登录和用户权限的类

```java
package com.example.aclservice.service.impl;

import com.example.aclservice.entity.User;
import com.example.aclservice.service.PermissionService;
import com.example.aclservice.service.UserService;
import com.example.serurity.entity.SecurityUser;
import org.springframework.beans.BeanUtils;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Service;

import java.util.List;


/**
 * <p>
 * 自定义userDetailsService - 认证用户详情
 * </p>
 *
 * @author qy
 * @since 2019-11-08
 */
@Service("userDetailsService")
public class UserDetailsServiceImpl implements UserDetailsService {

    @Autowired
    private UserService userService;

    @Autowired
    private PermissionService permissionService;

    /***
     * 根据账号获取用户信息
     * @param username:
     * @return: org.springframework.security.core.userdetails.UserDetails
     */
    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        // 从数据库中取出用户信息
        User user = userService.selectByUsername(username);

        // 判断用户是否存在
        if (null == user){
            //throw new UsernameNotFoundException("用户名不存在！");
        }
        // 返回UserDetails实现类
        com.example.serurity.entity.User curUser = new com.example.serurity.entity.User();
        BeanUtils.copyProperties(user,curUser);

        List<String> authorities = permissionService.selectPermissionValueByUserId(user.getId());
        SecurityUser securityUser = new SecurityUser(curUser);
        securityUser.setPermissionValueList(authorities);
        return securityUser;
    }

}

```

