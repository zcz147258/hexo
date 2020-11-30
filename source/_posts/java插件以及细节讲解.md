---
title: Java插件
date:
updated:
type: "tags"
categories: Java
comments:
description: Java插件
keywords: Java插件
top_img: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2664815884,20638765&fm=26&gp=0.jpg
cover: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2664815884,20638765&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.pom.xml

## 1.1项目信息

```xml
<!--父项目的坐标。如果项目中没有规定某个元素的值，那么父项目中的对应值即为项目的默认值。 坐标包括group ID，artifact ID和 version。-->
    <parent>
        <!--被继承的父项目的构件标识符-->
        <artifactId/>
        <!--被继承的父项目的全球唯一标识符-->
        <groupId/>
        <!--被继承的父项目的版本-->
        <version/>
        <!-- 父项目的pom.xml文件的相对路径。相对路径允许你选择一个不同的路径。默认值是../pom.xml。Maven首先在构建当前项目的地方寻找父项 目的pom，其次在文件系统的这个位置（relativePath位置），然后在本地仓库，最后在远程仓库寻找父项目的pom。-->
        <relativePath/>
    </parent>
```

## 1.2POM打包

```xml
<!--声明项目描述符遵循哪一个POM模型版本。模型本身的版本很少改变，虽然如此，但它仍然是必不可少的，这是为了当Maven引入了新的特性或者其他模型变更的时候，确保稳定性。-->
    <modelVersion>4.0.0</modelVersion>
    <!--项目的全球唯一标识符，通常使用全限定的包名区分该项目和其他项目。并且构建时生成的路径也是由此生成， 如com.mycompany.app生成的相对路径为：/com/mycompany/app-->
    <groupId>asia.banseon</groupId>
    <!-- 构件的标识符，它和group ID一起唯一标识一个构件。换句话说，你不能有两个不同的项目拥有同样的artifact ID和groupID；在某个 特定的group ID下，artifact ID也必须是唯一的。构件是项目产生的或使用的一个东西，Maven为项目产生的构件包括：JARs，源 码，二进制发布和WARs等。-->
    <artifactId>banseon-maven2</artifactId>
    <!--项目产生的构件类型，例如jar、war、ear、pom。插件可以创建他们自己的构件类型，所以前面列的不是全部构件类型-->
    <packaging>jar</packaging>
    <!--项目当前版本，格式为:主版本.次版本.增量版本-限定版本号-->
    <version>1.0-SNAPSHOT</version>
    <!--项目的名称, Maven产生的文档用-->
    <name>banseon-maven</name>
    <!--项目主页的URL, Maven产生的文档用-->
    <url>http://www.baidu.com/banseon</url>
    <!-- 项目的详细描述, Maven 产生的文档用。  当这个元素能够用HTML格式描述时（例如，CDATA中的文本会被解析器忽略，就可以包含HTML标 签）， 不鼓励使用纯文本描述。如果你需要修改产生的web站点的索引页面，你应该修改你自己的索引页文件，而不是调整这里的文档。-->
    <description>A maven project to study maven.</description>
    <!--描述了这个项目构建环境中的前提条件。-->
    <prerequisites>
        <!--构建该项目或使用该插件所需要的Maven的最低版本-->
        <maven/>
```

## 1.3构建项目

```xml
<!--构建项目需要的信息-->
    <build>
        <!--该元素设置了项目源码目录，当构建项目的时候，构建系统会编译目录里的源码。该路径是相对于pom.xml的相对路径。-->
        <sourceDirectory/>
        <!--该元素设置了项目脚本源码目录，该目录和源码目录不同：绝大多数情况下，该目录下的内容 会被拷贝到输出目录(因为脚本是被解释的，而不是被编译的)。-->
        <scriptSourceDirectory/>
        <!--该元素设置了项目单元测试使用的源码目录，当测试项目的时候，构建系统会编译目录里的源码。该路径是相对于pom.xml的相对路径。-->
        <testSourceDirectory/>
        <!--被编译过的应用程序class文件存放的目录。-->
        <outputDirectory/>
        <!--被编译过的测试class文件存放的目录。-->
        <testOutputDirectory/>
        <!--使用来自该项目的一系列构建扩展-->
        <extensions>
            <!--描述使用到的构建扩展。-->
            <extension>
                <!--构建扩展的groupId-->
                <groupId/>
                <!--构建扩展的artifactId-->
                <artifactId/>
                <!--构建扩展的版本-->
                <version/>
            </extension>
        </extensions>
        <!--当项目没有规定目标（Maven2 叫做阶段）时的默认值-->
        <defaultGoal/>
        <!--这个元素描述了项目相关的所有资源路径列表，例如和项目相关的属性文件，这些资源被包含在最终的打包文件里。-->
        <resources>
            <!--这个元素描述了项目相关或测试相关的所有资源路径-->
            <resource>
                <!-- 描述了资源的目标路径。该路径相对target/classes目录（例如${project.build.outputDirectory}）。举个例 子，如果你想资源在特定的包里(org.apache.maven.messages)，你就必须该元素设置为org/apache/maven /messages。然而，如果你只是想把资源放到源码目录结构里，就不需要该配置。-->
                <targetPath/>
                <!--是否使用参数值代替参数名。参数值取自properties元素或者文件里配置的属性，文件在filters元素里列出。-->
                <filtering/>
                <!--描述存放资源的目录，该路径相对POM路径-->
                <directory/>
                <!--包含的模式列表，例如**/*.xml.-->
                <includes/>
                <!--排除的模式列表，例如**/*.xml-->
                <excludes/>
            </resource>
        </resources>
        <!--这个元素描述了单元测试相关的所有资源路径，例如和单元测试相关的属性文件。-->
        <testResources>
            <!--这个元素描述了测试相关的所有资源路径，参见build/resources/resource元素的说明-->
            <testResource>
                <targetPath/><filtering/><directory/><includes/><excludes/>
            </testResource>
        </testResources>
        <!--构建产生的所有文件存放的目录-->
        <directory/>
        <!--产生的构件的文件名，默认值是${artifactId}-${version}。-->
        <finalName/>
        <!--当filtering开关打开时，使用到的过滤器属性文件列表-->
        <filters/>
        <!--子项目可以引用的默认插件信息。该插件配置项直到被引用时才会被解析或绑定到生命周期。给定插件的任何本地配置都会覆盖这里的配置-->
        <pluginManagement>
            <!--使用的插件列表 。-->
            <plugins>
                <!--plugin元素包含描述插件所需要的信息。-->
                <plugin>
                    <!--插件在仓库里的group ID-->
                    <groupId/>
                    <!--插件在仓库里的artifact ID-->
                    <artifactId/>
                    <!--被使用的插件的版本（或版本范围）-->
                    <version/>
                    <!--是否从该插件下载Maven扩展（例如打包和类型处理器），由于性能原因，只有在真需要下载时，该元素才被设置成enabled。-->
                    <extensions/>
                    <!--在构建生命周期中执行一组目标的配置。每个目标可能有不同的配置。-->
                    <executions>
                        <!--execution元素包含了插件执行需要的信息-->
                        <execution>
                            <!--执行目标的标识符，用于标识构建过程中的目标，或者匹配继承过程中需要合并的执行目标-->
                            <id/>
                            <!--绑定了目标的构建生命周期阶段，如果省略，目标会被绑定到源数据里配置的默认阶段-->
                            <phase/>
                            <!--配置的执行目标-->
                            <goals/>
                            <!--配置是否被传播到子POM-->
                            <inherited/>
                            <!--作为DOM对象的配置-->
                            <configuration/>
                        </execution>
                    </executions>
                    <!--项目引入插件所需要的额外依赖-->
                    <dependencies>
                        <!--参见dependencies/dependency元素-->
                        <dependency>
                            ......
                        </dependency>
                    </dependencies>
                    <!--任何配置是否被传播到子项目-->
                    <inherited/>
                    <!--作为DOM对象的配置-->
                    <configuration/>
                </plugin>
            </plugins>
        </pluginManagement>
        <!--使用的插件列表-->
        <plugins>
            <!--参见build/pluginManagement/plugins/plugin元素-->
            <plugin>
                <groupId/><artifactId/><version/><extensions/>
                <executions>
                    <execution>
                        <id/><phase/><goals/><inherited/><configuration/>
                    </execution>
                </executions>
                <dependencies>
                    <!--参见dependencies/dependency元素-->
                    <dependency>
                        ......
                    </dependency>
                </dependencies>
                <goals/><inherited/><configuration/>
            </plugin>
        </plugins>
    </build>
```

## 1.4远程仓库

```xml
<!--发现依赖和扩展的远程仓库列表。-->
    <repositories>
        <!--包含需要连接到远程仓库的信息-->
        <repository>
            <!--如何处理远程仓库里发布版本的下载-->
            <releases>
                <!--true或者false表示该仓库是否为下载某种类型构件（发布版，快照版）开启。 -->
                <enabled/>
                <!--该元素指定更新发生的频率。Maven会比较本地POM和远程POM的时间戳。这里的选项是：always（一直），daily（默认，每日），interval：X（这里X是以分钟为单位的时间间隔），或者never（从不）。-->
                <updatePolicy/>
                <!--当Maven验证构件校验文件失败时该怎么做：ignore（忽略），fail（失败），或者warn（警告）。-->
                <checksumPolicy/>
            </releases>
            <!-- 如何处理远程仓库里快照版本的下载。有了releases和snapshots这两组配置，POM就可以在每个单独的仓库中，为每种类型的构件采取不同的 策略。例如，可能有人会决定只为开发目的开启对快照版本下载的支持。参见repositories/repository/releases元素 -->
            <snapshots>
                <enabled/><updatePolicy/><checksumPolicy/>
            </snapshots>
            <!--远程仓库唯一标识符。可以用来匹配在settings.xml文件里配置的远程仓库-->
            <id>banseon-repository-proxy</id>
            <!--远程仓库名称-->
            <name>banseon-repository-proxy</name>
            <!--远程仓库URL，按protocol://hostname/path形式-->
            <url>http://192.168.1.169:9999/repository/</url>
            <!-- 用于定位和排序构件的仓库布局类型-可以是default（默认）或者legacy（遗留）。Maven 2为其仓库提供了一个默认的布局；然 而，Maven 1.x有一种不同的布局。我们可以使用该元素指定布局是default（默认）还是legacy（遗留）。-->
            <layout>default</layout>
        </repository>
    </repositories>
    <!--发现插件的远程仓库列表，这些插件用于构建和报表-->
    <pluginRepositories>
        <!--包含需要连接到远程插件仓库的信息.参见repositories/repository元素-->
        <pluginRepository>
            ......
        </pluginRepository>
    </pluginRepositories>

```

## 1.5依赖

```xml
<!--该元素描述了项目相关的所有依赖。 这些依赖组成了项目构建过程中的一个个环节。它们自动从项目定义的仓库中下载。要获取更多信息，请看项目依赖机制。-->
    <dependencies>
        <dependency>
            <!--依赖的group ID-->
            <groupId>org.apache.maven</groupId>
            <!--依赖的artifact ID-->
            <artifactId>maven-artifact</artifactId>
            <!--依赖的版本号。 在Maven 2里, 也可以配置成版本号的范围。-->
            <version>3.8.1</version>
            <!-- 依赖类型，默认类型是jar。它通常表示依赖的文件的扩展名，但也有例外。一个类型可以被映射成另外一个扩展名或分类器。类型经常和使用的打包方式对应， 尽管这也有例外。一些类型的例子：jar，war，ejb-client和test-jar。如果设置extensions为 true，就可以在 plugin里定义新的类型。所以前面的类型的例子不完整。-->
            <type>jar</type>
            <!-- 依赖的分类器。分类器可以区分属于同一个POM，但不同构建方式的构件。分类器名被附加到文件名的版本号后面。例如，如果你想要构建两个单独的构件成 JAR，一个使用Java 1.4编译器，另一个使用Java 6编译器，你就可以使用分类器来生成两个单独的JAR构件。-->
            <classifier></classifier>
            <!--依赖范围。在项目发布过程中，帮助决定哪些构件被包括进来。欲知详情请参考依赖机制。
                - compile ：默认范围，用于编译
                - provided：类似于编译，但支持你期待jdk或者容器提供，类似于classpath
                - runtime: 在执行时需要使用
                - test:    用于test任务时使用
                - system: 需要外在提供相应的元素。通过systemPath来取得
                - systemPath: 仅用于范围为system。提供相应的路径
                - optional:   当项目自身被依赖时，标注依赖是否传递。用于连续依赖时使用-->
            <scope>test</scope>
            <!--仅供system范围使用。注意，不鼓励使用这个元素，并且在新的版本中该元素可能被覆盖掉。该元素为依赖规定了文件系统上的路径。需要绝对路径而不是相对路径。推荐使用属性匹配绝对路径，例如${java.home}。-->
            <systemPath></systemPath>
            <!--当计算传递依赖时， 从依赖构件列表里，列出被排除的依赖构件集。即告诉maven你只依赖指定的项目，不依赖项目的依赖。此元素主要用于解决版本冲突问题-->
            <exclusions>
                <exclusion>
                    <artifactId>spring-core</artifactId>
                    <groupId>org.springframework</groupId>
                </exclusion>
            </exclusions>
            <!--可选依赖，如果你在项目B中把C依赖声明为可选，你就需要在依赖于B的项目（例如项目A）中显式的引用对C的依赖。可选依赖阻断依赖的传递性。-->
            <optional>true</optional>
        </dependency>

```

```xml
 <!-- 继承自该项目的所有子项目的默认依赖信息。这部分的依赖信息不会被立即解析,而是当子项目声明一个依赖（必须描述group ID和 artifact ID信息），如果group ID和artifact ID以外的一些信息没有描述，则通过group ID和artifact ID 匹配到这里的依赖，并使用这里的依赖信息。-->
    <dependencyManagement>
        <dependencies>
            <!--参见dependencies/dependency元素-->
            <dependency>
                ......
            </dependency>
        </dependencies>
    </dependencyManagement>
```

## 1.6部署

```xml
<!--项目分发信息，在执行mvn deploy后表示要发布的位置。有了这些信息就可以把网站部署到远程服务器或者把构件部署到远程仓库。-->
    <distributionManagement>
        <!--部署项目产生的构件到远程仓库需要的信息-->
        <repository>
            <!--是分配给快照一个唯一的版本号（由时间戳和构建流水号）？还是每次都使用相同的版本号？参见repositories/repository元素-->
            <uniqueVersion/>
            <id>banseon-maven2</id>
            <name>banseon maven2</name>
            <url>file://${basedir}/target/deploy</url>
            <layout/>
        </repository>
        <!--构件的快照部署到哪里？如果没有配置该元素，默认部署到repository元素配置的仓库，参见distributionManagement/repository元素-->
        <snapshotRepository>
            <uniqueVersion/>
            <id>banseon-maven2</id>
            <name>Banseon-maven2 Snapshot Repository</name>
            <url>scp://svn.baidu.com/banseon:/usr/local/maven-snapshot</url>
            <layout/>
        </snapshotRepository>
        <!--部署项目的网站需要的信息-->
        <site>
            <!--部署位置的唯一标识符，用来匹配站点和settings.xml文件里的配置-->
            <id>banseon-site</id>
            <!--部署位置的名称-->
            <name>business api website</name>
            <!--部署位置的URL，按protocol://hostname/path形式-->
            <url>
                scp://svn.baidu.com/banseon:/var/www/localhost/banseon-web
            </url>
        </site>
        <!--项目下载页面的URL。如果没有该元素，用户应该参考主页。使用该元素的原因是：帮助定位那些不在仓库里的构件（由于license限制）。-->
        <downloadUrl/>
        <!--如果构件有了新的group ID和artifact ID（构件移到了新的位置），这里列出构件的重定位信息。-->
        <relocation>
            <!--构件新的group ID-->
            <groupId/>
            <!--构件新的artifact ID-->
            <artifactId/>
            <!--构件新的版本号-->
            <version/>
            <!--显示给用户的，关于移动的额外信息，例如原因。-->
            <message/>
        </relocation>
        <!-- 给出该构件在远程仓库的状态。不得在本地项目中设置该元素，因为这是工具自动更新的。有效的值有：none（默认），converted（仓库管理员从 Maven 1 POM转换过来），partner（直接从伙伴Maven 2仓库同步过来），deployed（从Maven 2实例部 署），verified（被核实时正确的和最终的）。-->
        <status/>
    </distributionManagement>
```

## 1.7依赖版本

```xml
    <properties>
        <java.version>8</java.version>
        <fastjson.version>1.2.9</fastjson.version>
        <caffeine.version>2.8.4</caffeine.version>
        <guava.version>29.0-jre</guava.version>
        <java.jwt.version>3.10.3</java.jwt.version>
        <knife4j.version>2.0.3</knife4j.version>
        <dozer.version>5.5.1</dozer.version>
        <kaptcha.version>0.0.9</kaptcha.version>
        <commons.io.version>2.7</commons.io.version>
        <jaxb-impl.version>2.3.1</jaxb-impl.version>
        <jaxb-core.version>2.3.0.1</jaxb-core.version>
        <javax.xml.bind.version>2.3.1</javax.xml.bind.version>
        <jsonwebtoken.jjwt.version>0.9.1</jsonwebtoken.jjwt.version>
        <org.apache.shiro.version>1.5.3</org.apache.shiro.version>
        <org.apache.commons.version>3.11</org.apache.commons.version>
        <hibernate-validator.version>6.1.5.Final</hibernate-validator.version>
        <org.apache.commons.lang3.version>3.9</org.apache.commons.lang3.version>
        <org.apache.httpcomponents.version>4.5.10</org.apache.httpcomponents.version>
        <mybatis-plus-boot-starter.version>3.3.2</mybatis-plus-boot-starter.version>
        <druid-spring-boot-starter.version>1.1.22</druid-spring-boot-starter.version>
    </properties>

```

# 2.Aop

```java
@Component
@Aspect
public class ZnqActivityAspect {

    @Autowired
    private PointsGlobalConfigService pointsGlobalConfigService;

	//定义切点
    @Pointcut("execution(* com.gbn.znq.view.controller..*.*(..))")
    
    //定义方法
    public void activityController(){}

    //在方法执行前执行
    @Before("activityController()")
    public void before(JoinPoint point) {

        Method method = ((MethodSignature) point.getSignature()).getMethod();
        GetMapping get = method.getAnnotation(GetMapping.class);
        boolean isGetMethod = (get == null);

        PointsGlobalConfigEntity globalConfig = pointsGlobalConfigService.getByCode(PointsConfigCodeEnum.ZNQ_ACTIVITY_TIME.getCode());
        if (ObjectUtils.isEmpty(globalConfig)) {
            throw new BusinessException("未配置周年庆活动起止时间");
        }

        if (StringUtils.isBlank(globalConfig.getValue())) {
            throw new BusinessException("未配置周年庆活动起止时间");
        }

        String[] configValues = globalConfig.getValue().split(",");
        LocalDateTime startTime = TimeUtils.parseTime(configValues[0]);
        LocalDateTime endTime = TimeUtils.parseTime(configValues[1]);

        // 验证活动是否在活动期间
        LocalDateTime now = LocalDateTime.now();
        if (isGetMethod && now.isBefore(startTime)) {
            throw new BusinessException("周年庆活动暂未开启,敬请期待");
        }

        if (isGetMethod && now.isAfter(endTime)) {
            throw new BusinessException("周年庆活动已结束");
        }
    }
}
```

# 3.日志

## 3.1Post请求

```java
package com.gbn.znq.component.httplog;

import com.alibaba.fastjson.JSON;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.core.MethodParameter;
import org.springframework.http.HttpInputMessage;
import org.springframework.http.converter.HttpMessageConverter;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.mvc.method.annotation.RequestBodyAdvice;

import java.io.IOException;
import java.lang.reflect.Method;
import java.lang.reflect.Type;

/**
 * @author alvins
 * @Description 请求日志
 * 注： 该拦截器只支持@RequestBody注解的方法
 * @date 2020/6/14 13:33
 * @since 1.0
 */
@ControllerAdvice
public class LogRequestBodyAdvice implements RequestBodyAdvice {

    public static final Logger LOGGER = LoggerFactory.getLogger(LogRequestBodyAdvice.class);

    @Override
    public boolean supports(MethodParameter methodParameter, Type type, Class<? extends HttpMessageConverter<?>> aClass) {
        return true;
    }

    @Override
    public HttpInputMessage beforeBodyRead(HttpInputMessage httpInputMessage, MethodParameter methodParameter, Type type, Class<? extends HttpMessageConverter<?>> aClass) throws IOException {
        return httpInputMessage;
    }

    @Override
    public Object afterBodyRead(Object body, HttpInputMessage httpInputMessage, MethodParameter methodParameter, Type type, Class<? extends HttpMessageConverter<?>> aClass) {

        Method method = methodParameter.getMethod();
        String classMappingUri = getClassMappingUri(method.getDeclaringClass());
        String methodMappingUri = getMethodMappingUri(method);
        if (!methodMappingUri.startsWith("/")) {
            methodMappingUri = "/" + methodMappingUri;
        }
        LOGGER.info("uri={} | requestBody={}", classMappingUri + methodMappingUri, JSON.toJSONString(body));
        return body;
    }

    @Override
    public Object handleEmptyBody(Object o, HttpInputMessage httpInputMessage, MethodParameter methodParameter, Type type, Class<? extends HttpMessageConverter<?>> aClass) {
        return o;
    }

    private String getMethodMappingUri(Method method) {

        RequestMapping requestMapping = method.getAnnotation(RequestMapping.class);
        return requestMapping == null ? "" : getMaxLength(requestMapping.value());
    }

    private String getClassMappingUri(Class<?> declaringClass) {
        RequestMapping classDeclaredAnnotation = declaringClass.getDeclaredAnnotation(RequestMapping.class);
        return classDeclaredAnnotation == null ? "" : getMaxLength(classDeclaredAnnotation.value());
    }

    private String getMaxLength(String[] strings) {
        String methodMappingUri = "";
        for (String string : strings) {
            if (string.length() > methodMappingUri.length()) {
                methodMappingUri = string;
            }
        }
        return methodMappingUri;
    }
}

```

## 3.2Get请求

```java
package com.gbn.znq.component.httplog;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.Pointcut;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;
import org.springframework.web.context.request.RequestContextHolder;
import org.springframework.web.context.request.ServletRequestAttributes;

import javax.servlet.http.HttpServletRequest;

/**
 * @author alvins
 * @Description 请求接口日志拦截器
 * @date 2020/6/14 13:41
 * @since 1.0
 */
@Aspect
@Component
public class LogRequestRecordAspect {

    public static final Logger LOGGER = LoggerFactory.getLogger(LogRequestRecordAspect.class);

    /**
     * 定义切点
     */
    @Pointcut("execution(* com.gbn.znq.view.controller..*.*(..))")
    public void webRequestLogs() {
    }

    /**
     * 请求日志打印
     * @param point
     */
    @Before("webRequestLogs()")
    public void doBefore(JoinPoint point) {
        // 接收到请求，记录请求内容
        ServletRequestAttributes attributes = (ServletRequestAttributes) RequestContextHolder.getRequestAttributes();
        assert attributes != null;
        HttpServletRequest request = attributes.getRequest();
        String beanName = point.getSignature().getDeclaringTypeName();
        String methodName = point.getSignature().getName();
        String uri = request.getRequestURI();
        Object[] paramsArray = point.getArgs();
        LOGGER.info("uri={} | beanName={} | methodName={} | params={}", uri, beanName, methodName, paramsArray);
    }
}

```

## 3.3响应日志

```java
package com.gbn.znq.component.httplog;

import com.alibaba.fastjson.JSON;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.core.MethodParameter;
import org.springframework.http.MediaType;
import org.springframework.http.server.ServerHttpRequest;
import org.springframework.http.server.ServerHttpResponse;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.servlet.mvc.method.annotation.ResponseBodyAdvice;

/**
 * @author alvins
 * @Description Request响应日志
 * @date 2020/6/14 13:44
 * @since 1.0
 */
@ControllerAdvice
public class LogResponseBodyAdvice implements ResponseBodyAdvice {

    public static final Logger LOGGER = LoggerFactory.getLogger(LogResponseBodyAdvice.class);

    @Override
    public boolean supports(MethodParameter methodParameter, Class aClass) {
        return true;
    }

    @Override
    public Object beforeBodyWrite(Object body, MethodParameter methodParameter, MediaType mediaType, Class aClass, ServerHttpRequest serverHttpRequest, ServerHttpResponse serverHttpResponse) {

        LOGGER.info("uri={} | responseBody={}", serverHttpRequest.getURI().getPath(), JSON.toJSONString(body));
        return body;
    }
}

```

## 3.4log4j配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE xml>  
<configuration>
	<!-- 定义常量 -->
	<properties>
        <!-- 日志文件存放路径 -->
        <property name="LOG_HOME">logs</property>
        <!-- 文件输出格式 -->
        <property name="ROLLINGFILE_PATTERN">[%p|%d{yyyy-MM-dd HH:mm:ss,SSS}] - [%t|%c{1}|%M|%L] - %m%n</property>
    </properties>
	
	<appenders>
		<!-- 输出控制台的配置 -->
		<Console name="CONSOLE" target="SYSTEM_OUT">
			<PatternLayout charset="UTF-8" pattern="${ROLLINGFILE_PATTERN}" />
		</Console>
		<!-- TRACE < DEBUG < INFO < WARN < ERROR < FATAL -->
		<RollingFile name="DEBUG" fileName="${LOG_HOME}/debug.log" filePattern="${LOG_HOME}/debug_%d{yyyy-MM-dd}.log">
			<PatternLayout charset="UTF-8" pattern="${ROLLINGFILE_PATTERN}"/>
			<Filters>  
				<!-- 屏蔽比level更高级别或者同等级别的日志 -->
				<ThresholdFilter level="info" onMatch="DENY" onMismatch="NEUTRAL"/>
				<!-- 输出比level更高级别或者同等级别的日志 -->  
			 	<ThresholdFilter level="debug" onMatch="ACCEPT" onMismatch="DENY" />
            </Filters> 
			<Policies>
				<!-- 按24小时(1天)生成一个文件 -->
       			<TimeBasedTriggeringPolicy modulate="true" interval="1"/>
       		</Policies>
       		<!-- 最多保存日志文件数 -->
       		<DefaultRolloverStrategy max="20"/>
		</RollingFile>
		
		<RollingFile name="INFO" fileName="${LOG_HOME}/info.log" filePattern="${LOG_HOME}/info_%d{yyyy-MM-dd}.log">
			<PatternLayout charset="UTF-8" pattern="${ROLLINGFILE_PATTERN}"/>
			<Filters>  
				<ThresholdFilter level="warn" onMatch="DENY" onMismatch="NEUTRAL"/>
			 	<ThresholdFilter level="info" onMatch="ACCEPT" onMismatch="DENY" />
            </Filters> 
			<Policies>
       			<TimeBasedTriggeringPolicy modulate="true" interval="1"/>
       		</Policies>
       		<DefaultRolloverStrategy max="20"/>
		</RollingFile>
		
		<RollingFile name="WARN" fileName="${LOG_HOME}/warn.log" filePattern="${LOG_HOME}/warn_%d{yyyy-MM-dd}.log">
			<PatternLayout charset="UTF-8" pattern="${ROLLINGFILE_PATTERN}"/>
			<Filters>  
				<ThresholdFilter level="error" onMatch="DENY" onMismatch="NEUTRAL"/>  
			 	<ThresholdFilter level="warn" onMatch="ACCEPT" onMismatch="DENY" />
            </Filters> 
			<Policies>
       			<TimeBasedTriggeringPolicy modulate="true" interval="1"/>
       		</Policies>
       		<DefaultRolloverStrategy max="20"/>
		</RollingFile>
		
		<RollingFile name="ERROR" fileName="${LOG_HOME}/error.log" filePattern="${LOG_HOME}/error_%d{yyyy-MM-dd}.log">
			<PatternLayout charset="UTF-8" pattern="${ROLLINGFILE_PATTERN}"/>
			<Filters>  
			 	<ThresholdFilter level="error" onMatch="ACCEPT" onMismatch="DENY" />
            </Filters> 
			<Policies>
       			<TimeBasedTriggeringPolicy modulate="true" interval="1"/>
       		</Policies>
       		<DefaultRolloverStrategy max="20"/>
		</RollingFile>
	</appenders>

	<!--定义logger，只有定义了logger并引入的appender，appender才会生效-->
	<loggers>
		<!-- 只打印info级别以上的 -->
		<Root level="INFO">
			<AppenderRef ref="CONSOLE"/>
			<AppenderRef ref="DEBUG"/>
			<AppenderRef ref="INFO"/>
			<AppenderRef ref="WARN"/>
			<AppenderRef ref="ERROR"/>
		</Root>
	</loggers>

</configuration>
```

# 4.spring-secrtity基础

```
本质上是一个过滤器链,
```



## 4.1初式

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
    </dependencies>
```

## 4.2解析

```
FilterSecurityInterceptor
			最底层的过滤器  方法级别过滤器
ExceptionTranslationFilter
			异常  判断认证授权中的异常
UsernamePasswordAuthenticationFilter
			登录密码用户名校验
			
			
加载过滤器的类
	DelegatingFilterProxy

//需要实现的的接口
	UserDetailsService
		查询数据库  用户名密码
		//执行过程
        
	PasswordEncoder
		加密密码
	
	1.创建类 继承 UsernamePasswordAuthenticationFilter 重写三个方法
	2.创建类实现UserDetailsService，编写数据查询过程返回User对象
	
	
```

## 4.3登录

```java
@Configuration
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private UserDetailsService userDetailsService;

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception{
        auth.userDetailsService(userDetailsService).passwordEncoder(password());
    }

    @Bean
    PasswordEncoder password(){
        return new BCryptPasswordEncoder();
    }
}
```

```java
@Service("userDetailsService")
public class MyUserDetailsService implements UserDetailsService {
    @Override
    public UserDetails loadUserByUsername(String s) throws UsernameNotFoundException {

        List<GrantedAuthority> auths = AuthorityUtils.commaSeparatedStringToAuthorityList("role");

        return new User("ddd",new BCryptPasswordEncoder().encode("123"),auths);
    }
}
```

## 4.4查询数据库登陆

```xml
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>

        <!--    plus    -->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.0.5</version>
        </dependency>
        <!--   mysql     -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
        <!--    lombok    -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
```

```java
@Service("userDetailsService")
public class MyUserDetailsService implements UserDetailsService {

    @Autowired
    private UserMapper userMapper;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {

        //查询数据库
        QueryWrapper<Users> wrapper = new QueryWrapper<Users>();
        wrapper.eq("username",username);
        Users users = userMapper.selectOne(wrapper);
        //判断
        if(users == null){
            throw new UsernameNotFoundException("用户名不存在");
        }

        List<GrantedAuthority> auths = AuthorityUtils.commaSeparatedStringToAuthorityList("role");

        return new User(users.getUsername(),new BCryptPasswordEncoder().encode(users.getPassword()),auths);
    }
}
```

## 4.5修改默认登录

```java
@Configuration
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private UserDetailsService userDetailsService;

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception{
        auth.userDetailsService(userDetailsService).passwordEncoder(password());
    }

    @Bean
    PasswordEncoder password(){
        return new BCryptPasswordEncoder();
    }


    @Override
    protected void configure(HttpSecurity http) throws Exception{
        //自定义登录页面
        http.formLogin()
                .loginPage("/login.html") //登录页面设置
                .loginProcessingUrl("/user/login") //登录访问路径
                .defaultSuccessUrl("/login/success").permitAll()//登陆成功跳转成功路径
                .and().authorizeRequests()
                    .antMatchers("/","/test/hello","user/login").permitAll()//设置那些路径无需认证
                .anyRequest().authenticated() //剩下的请求需要验证
                .and().csrf().disable(); //关闭csrf防护
    }
}
```

## 4.6授权

```java
hasAuthority   用户是否有指定的权限  拥有配置的所有权限
hasAnyAuthority  拥有其中一个权限   就可以访问


@Override
    protected void configure(HttpSecurity http) throws Exception{
        //自定义登录页面
        http.formLogin()
                .loginPage("/login.html") //登录页面设置
                .loginProcessingUrl("/user/login") //登录访问路径
                .defaultSuccessUrl("/login/success").permitAll()//登陆成功跳转成功路径
                .and().authorizeRequests()
                    .antMatchers("/","/test/hello","user/login").permitAll()//设置那些路径无需认证
                .antMatchers("/test/index").hasAuthority("admins,manager")//需要admins,manager权限才能访问
                .antMatchers("/test/index").hasAnyAuthority("admins,manager")//需要admins,manager权限其中一个才能访问
                .anyRequest().authenticated() //剩下的请求需要验证
                .and().csrf().disable(); //关闭csrf防护
    }
```

```java
hasAuthority("admins,manager")//需要admins,manager权限才能访问
hasAnyAuthority("admins,manager")//需要admins,manager权限其中一个才能访问

 .antMatchers("/test/index").hasRole("sale")//需要ROLE_sale角色才能访问
    .antMatchers("/test/index").hasAnyRole("sale,user")//需要ROLE_sale,ROLE_user角色之一才能访问
```

## 4.7自定义403

```java
//自定义403页面
        http.exceptionHandling().accessDeniedPage("/unauth.html");
```

## 4.8注解使用

```java
//使用注解要开启注解使用
@EnableGlobalMethodSecurity(securedEnabled = true)

@Secured({"ROLE_sale","ROLE_manager"})  角色验证  加前缀

@PreAuthorize("hasAnyAuthority('menu:system')")//在方法之前校验
    
@PostAuthorize(""hasAnyAuthority('menu:system')"")//在方法之后进行校验
    
@PreFilter(value = "filterObject.id%2 == 0")//参数过滤
    
@PosterFilter("filterObject.username == 'admin1'")

```

## 4.9用户退出

```java
//退出页面
   http.logout().logoutUrl("/logout").logoutSuccessUrl("/test/hello").permitAll();
```

## 4.10记住我功能

```java
1.cookie技术
2.安全框架机制实现自动登录

实现原理
	浏览器 认证成功后 把cookie和信息加密传存入 数据库
	再次访问 获取用户cookie信息  拿着cookie信息到数据库进行比对
	
具体步骤
	1.认证请求
	2.认证成功
	3.将token写入Cookie
	4.将token写入数据库
	5.服务再次请求 读取Cookie中的token 在数据库中查找token
	6.UserDetailsService
```

1.创建数据库

```java
CREATE TABLE `persistent_logins`(
`username` VARCHAR(64) NOT NULL,
`series` VARCHAR(64) NOT NULL,
`token` VARCHAR(64) NOT NULL,
`last_used` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
PRIMARY KEY(`series`)
) ENGINE=INNODB DEFAULT CHARSET=utf8mb4 COMMENT='记住登录';
```

2.配置类，注入数据源，配置操作数据库对象

```java
//注入数据源
@Autowired
private DataSource dataSource;

@Bean
public PersistentTokenRepository persistentTokenRepository(){
    JdbcTokenRepositoryImpl jdbcTokenRepository = new JdbcTokenRepositoryImpl();
    jdbcTokenRepository.setDataSource(dataSource);
    return jdbcTokenRepository;
}
```

3.配置类配置自动登录

```java
.antMatchers("/test/role").hasAnyRole("sale,user")//需要ROLE_sale,ROLE_user角色之一才能访问
.anyRequest().authenticated() //剩下的请求需要验证
.and().rememberMe().tokenRepository(persistentTokenRepository())//记住我
.tokenValiditySeconds(60)//设置有效时长
.userDetailsService(userDetailsService)//设置userDetails
.and().csrf().disable(); //关闭csrf防护
```

4.前端

```java
<input type="checkbox" name="remember-me">自动登录
```

自定义登录窗口

```java
 http.formLogin()
 	.loginPage("/userLogin").permisAll()
 	.usernameParameter("username")
 	.passwordParameter("passwrod")
 	.defaultSuccessUrl("/")
 	.failureUrl("/userLogin?error")
```

# 5.spring-security微服务

## 5.1密码处理工具类

```java
/**
 * 重写密码加密
 */
@Component
public class DefaultPasswordEncoder implements PasswordEncoder {


    /**
     * MD5加密
     * @param charSequence
     * @return
     */
    @Override
    public String encode(CharSequence charSequence) {
        return MD5.encrypt(charSequence.toString());
    }

    /**
     * 对密码进行比对
     * @param charSequence
     * @param encodePasswrod
     * @return
     */
    @Override
    public boolean matches(CharSequence charSequence, String encodePasswrod) {
        return encodePasswrod.equals(MD5.encrypt(charSequence.toString()));
    }
}
```

## 5.2token操作工具类

```java
@Component
public class TokenManager {

    /**
     * token有效时长
     */
    private long tokenExpiration = 24*60*60*1000;

    /**
     * 编码密钥
     */
    private String tokenSignKey = "123456";


    /**
     * 根据用户名生成token
     */
    public String createToken(String username){
        String token = Jwts.builder().setSubject(username)
                .setExpiration(new Date(System.currentTimeMillis() + tokenExpiration))
                .signWith(SignatureAlgorithm.HS512,tokenSignKey).compressWith(CompressionCodecs.GZIP).compact();

        return token;
    }


    /**
     * 根据token得到用户信息
     */
    public String getUserInfoFromToken(String token){
        String userinfo = Jwts.parser().setSigningKey(tokenSignKey).parseClaimsJws(token).getBody().getSubject();
        return userinfo;
    }

    /**
     * 删除token
     */
    public void removeToken(String token){}
}
```

## 5.3退出登录工具类

```java
/**
 * 退出登陆
 */
public class TokenLogoutHandler implements LogoutHandler {

    private TokenManager tokenManager;

    private RedisTemplate redisTemplate;

    /**
     * 有参构造
     */
    public TokenLogoutHandler(TokenManager tokenManager,RedisTemplate redisTemplate){
        this.tokenManager = tokenManager;
        this.redisTemplate = redisTemplate;
    }

    /**
     * 退出方法
     * @param request
     * @param response
     * @param authentication
     */
    @Override
    public void logout(HttpServletRequest request, HttpServletResponse response, Authentication authentication) {
        String token = request.getHeader("token");
        if(token != null){
            tokenManager.removeToken(token);

            String username = tokenManager.getUserInfoFromToken(token);
            redisTemplate.delete(username);
        }
        ResponseUtil.out(response, R.ok());
    }
}
```

## 5.4未授权统一处理类

```java
/**
 * 未授权处理类
 */
public class UnAuthEntryPoint implements AuthenticationEntryPoint {
    @Override
    public void commence(HttpServletRequest request, HttpServletResponse response, AuthenticationException e) throws IOException, ServletException {
        ResponseUtil.out(response, R.error().message("未授权").code(403));
    }
}
```

## 5.5Token认证过滤器

```java
public class TokenLoginFilter extends UsernamePasswordAuthenticationFilter {


    private RedisTemplate redisTemplate;
    private TokenManager tokenManager;
    private AuthenticationManager authenticationManager;

    /**
     * 有参构造
     * @param redisTemplate
     * @param tokenManager
     * @param authenticationManager
     */
    public TokenLoginFilter(RedisTemplate redisTemplate, TokenManager tokenManager, AuthenticationManager authenticationManager) {
        this.redisTemplate = redisTemplate;
        this.tokenManager = tokenManager;
        this.authenticationManager = authenticationManager;
        this.setPostOnly(false);//只能post
        this.setRequiresAuthenticationRequestMatcher(new AntPathRequestMatcher("admin/acl/login","POST"));//匹配登录路径
    }

    /**
     * 获取表单提交的用户名密码
     * @param request
     * @param response
     * @return
     * @throws AuthenticationException
     */
    @Override
    public Authentication attemptAuthentication(HttpServletRequest request, HttpServletResponse response) throws AuthenticationException {

        try {
            User user = new ObjectMapper().readValue(request.getInputStream(), User.class);
            return authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(user.getUsername(),user.getPassword(),
                    new ArrayList<>()));
        } catch (IOException e) {
            e.printStackTrace();
            throw new RuntimeException();
        }
    }


    /**
     * 认证成功的方法
     * @param request
     * @param response
     * @param chain
     * @param authResult
     * @throws IOException
     * @throws ServletException
     */
    @Override
    protected void successfulAuthentication(HttpServletRequest request, HttpServletResponse response, FilterChain chain, Authentication authResult) throws IOException, ServletException {

        //得到用户信息
        SecurityUser user = (SecurityUser) authResult.getPrincipal();

        //根据用户名生成token，存储到redis里面
        String token = tokenManager.createToken(user.getCurrentUserInfo().getUsername());
        redisTemplate.opsForValue().set(user.getCurrentUserInfo().getUsername(),user.getPermissionValueList());

        ResponseUtil.out(response, R.ok().data("token",token));
    }


    /**
     * 认证失败
     * @param request
     * @param response
     * @param failed
     * @throws IOException
     * @throws ServletException
     */
    @Override
    protected void unsuccessfulAuthentication(HttpServletRequest request, HttpServletResponse response, AuthenticationException failed) throws IOException, ServletException {
        ResponseUtil.out(response,R.error());
    }
}
```

## 5.6当前登录用户信息

```java
@Data
public class SecurityUser implements UserDetails {
    /**
     * 当前登录用户
     * @return
     */
    private transient User currentUserInfo;

    /**
     * 当前权限
     * @return
     */
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
        return false;
    }
}
```

## 5.7User实体类

```java
@Data
public class User implements Serializable {
    public static final long serialVersionUID = 1L;

    private String username;

    private String password;

    private String nickName;

    private String salt;//头像

    private String token;
}

```

## 5.8授权过滤器

```java
/**
 * 授权过滤器
 */
public class TokenAuthFilter extends BasicAuthenticationFilter {

    private TokenManager tokenManager;
    private RedisTemplate redisTemplate;

    public TokenAuthFilter(AuthenticationManager authenticationManager) {
        super(authenticationManager);

        this.tokenManager = tokenManager;
        this.redisTemplate = redisTemplate;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain chain) throws IOException, ServletException {
        //获取当前认证成功用户权限信息
        UsernamePasswordAuthenticationToken authRequest = getAuthentication(request);
        //判断是不是空
        if(authRequest != null){
            SecurityContextHolder.getContext().setAuthentication(authRequest);
        }
        //放行过滤器
        chain.doFilter(request,response);
    }

    /**
     * 根据当前认证用户获取权限信息
     * @param request
     * @return
     */
    private UsernamePasswordAuthenticationToken getAuthentication(HttpServletRequest request){
        //从header里面获取token
        String token = request.getHeader("token");
        if(token != null){
            String username = tokenManager.getUserInfoFromToken(token);
            List<String> permissionList = (List<String>) redisTemplate.opsForValue().get(username);
            Collection<GrantedAuthority> authorities = new ArrayList<>();
            for (String permissionValue:permissionList) {
                SimpleGrantedAuthority auth = new SimpleGrantedAuthority(permissionValue);
                authorities.add(auth);
            }
            return new UsernamePasswordAuthenticationToken(username,token,authorities);
        }
        return null;
    }
}
```

## 5.9核心配置类

```java
@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class TokenWebSecurityConfig extends WebSecurityConfigurerAdapter {

    private TokenManager tokenManager;
    private RedisTemplate redisTemplate;
    private DefaultPasswordEncoder defaultPasswordEncoder;
    private UserDetailsService userDetailsService;

    /**
     * 有参构造函数
     * @param tokenManager
     * @param redisTemplate
     * @param defaultPasswordEncoder
     * @param userDetailsService
     */
//    @Autowired
    public TokenWebSecurityConfig(UserDetailsService userDetailsService, DefaultPasswordEncoder defaultPasswordEncoder,
                                  TokenManager tokenManager, RedisTemplate redisTemplate) {
        this.userDetailsService = userDetailsService;
        this.defaultPasswordEncoder = defaultPasswordEncoder;
        this.tokenManager = tokenManager;
        this.redisTemplate = redisTemplate;
    }


    /**
     * 配置http设置
     * 设置过滤器以及配置登录入口出口
     * @param http
     * @throws Exception
     */
    @Override
    protected void configure(HttpSecurity http) throws Exception{

        http.exceptionHandling()
                .authenticationEntryPoint(new UnAuthEntryPoint())//没有权限去处理
                .and().csrf().disable()//csrf处理
                .authorizeRequests()//请求
                .anyRequest().authenticated()//权限
                .and().logout().logoutUrl("/admin/acl/index/logout")//设置退出的路径
                .addLogoutHandler(new TokenLogoutHandler(tokenManager,redisTemplate)).and()
                .addFilter(new TokenLoginFilter(redisTemplate,tokenManager,authenticationManager()))
                .addFilter(new TokenAuthFilter(authenticationManager(),tokenManager,redisTemplate))
                .httpBasic();
    }

    /**
     * 调用userDetailsService和密码处理
     */
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userDetailsService).passwordEncoder(defaultPasswordEncoder);
    }

    /**
     * 配置那些路径不需要授权
     */
    @Override
    public void configure(WebSecurity web) throws Exception {
        web.ignoring().antMatchers("/api/**");
    }
}
```



## 5.10UserDetails

```java
@Service("userDetailsService")
public class UserDetailsServiceImpl implements UserDetailsService {

    @Autowired
    private UserService userService;
    @Autowired
    private PermissionService permissionService;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userService.selectByUsername(username);
        if(user == null){
            throw new UsernameNotFoundException("用户不存在");
        }

        //security的对象
        com.security.demo.entity.User curUser = new  com.security.demo.entity.User();
        BeanUtils.copyProperties(user,curUser);

        List<String> permissionValueList = permissionService.selectPermissionValueByUserId(user.getId());

        SecurityUser securityUser = new SecurityUser();
        securityUser.setPermissionValueList(permissionValueList);
        return securityUser;
    }
}
```

## 5.11网关跨域

```java
@Configuration
public class CorsConfig {
    @Bean
    public CorsWebFilter corsWebFilter(){
        CorsConfiguration config = new CorsConfiguration();
        config.addAllowedMethod("*");
        config.addAllowedOrigin("*");
        config.addAllowedHeader("*");

        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource(new PathPatternParser());
        source.registerCorsConfiguration("/**",config);

        return new CorsWebFilter(source);

    }
}
```

## 5.12解决springsecurity跨域

跨域配置

```java
@Configuration
public class CorsConfig implements WebMvcConfigurer {
    private CorsConfiguration buildConfig() {
        CorsConfiguration corsConfiguration = new CorsConfiguration();
        corsConfiguration.addAllowedOrigin("*");
        corsConfiguration.addAllowedHeader("*");
        corsConfiguration.addAllowedMethod("*");
        corsConfiguration.addExposedHeader("Authorization");
        return corsConfiguration;
    }

    @Bean
    public CorsFilter corsFilter() {
        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**", buildConfig());
        return new CorsFilter(source);
    }

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("*")
                .allowCredentials(true)
                .allowedMethods("GET", "POST", "DELETE", "PUT","OPTIONS")
                .maxAge(3600);
    }
}
```

security设置

```java
/**
     * 配置设置
     * @param http
     * @throws Exception
     */
    //设置退出的地址和token，redis操作地址
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.exceptionHandling()
                .authenticationEntryPoint(new UnauthEntryPoint())//没有权限访问
                .and().csrf().disable()
                .cors().and()
                .authorizeRequests()
                .requestMatchers(CorsUtils::isPreFlightRequest).permitAll()
                //允许swagger-ui.html访问
                .antMatchers("/v2/api-docs", "/swagger-resources/configuration/ui",
                        "/swagger-resources", "/swagger-resources/configuration/security",
                        "/swagger-ui.html", "/webjars/**").permitAll()
                .anyRequest().authenticated()
                .and().logout().logoutUrl("/admin/acl/index/logout")//退出路径
                .addLogoutHandler(new TokenLogoutHandler(tokenManager,redisTemplate)).and()
                .addFilter(new TokenLoginFilter(authenticationManager(), tokenManager, redisTemplate))
                .addFilter(new TokenAuthFilter(authenticationManager(), tokenManager, redisTemplate)).httpBasic();
    }

    //调用userDetailsService和密码处理
    @Override
    public void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userDetailsService).passwordEncoder(defaultPasswordEncoder);
    }
    //不进行认证的路径，可以直接访问
    @Override
    public void configure(WebSecurity web) throws Exception {
        //swagger2所需要用到的静态资源，允许访问
        web.ignoring().antMatchers("/v2/api-docs",
                "/swagger-resources/configuration/ui",
                "/swagger-resources",
                "/webjars/**",
                "/swagger-resources/configuration/security",
                "/swagger-ui.html");

    }
```

# 6.整合log4j日志

```xml
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <exclusions>
                <exclusion>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-logging</artifactId>
                </exclusion>
            </exclusions>
        </dependency>

        <dependency> <!-- 引入log4j2依赖 -->
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-log4j2</artifactId>
        </dependency>
        
        <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>fastjson</artifactId>
                <version>${fastjson.version}</version>
         </dependency>
         <fastjson.version>1.2.28</fastjson.version>
```

配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE xml>  
<configuration>
	<!-- 定义常量 -->
	<properties>
        <!-- 日志文件存放路径 -->
        <property name="LOG_HOME">logs</property>
        <!-- 文件输出格式 -->
        <property name="ROLLINGFILE_PATTERN">[%p|%d{yyyy-MM-dd HH:mm:ss,SSS}] - [%t|%c{1}|%M|%L] - %m%n</property>
    </properties>
	
	<appenders>
		<!-- 输出控制台的配置 -->
		<Console name="CONSOLE" target="SYSTEM_OUT">
			<PatternLayout charset="UTF-8" pattern="${ROLLINGFILE_PATTERN}" />
		</Console>
		<!-- TRACE < DEBUG < INFO < WARN < ERROR < FATAL -->
		<RollingFile name="DEBUG" fileName="${LOG_HOME}/debug.log" filePattern="${LOG_HOME}/debug_%d{yyyy-MM-dd}.log">
			<PatternLayout charset="UTF-8" pattern="${ROLLINGFILE_PATTERN}"/>
			<Filters>  
				<!-- 屏蔽比level更高级别或者同等级别的日志 -->
				<ThresholdFilter level="info" onMatch="DENY" onMismatch="NEUTRAL"/>
				<!-- 输出比level更高级别或者同等级别的日志 -->  
			 	<ThresholdFilter level="debug" onMatch="ACCEPT" onMismatch="DENY" />
            </Filters> 
			<Policies>
				<!-- 按24小时(1天)生成一个文件 -->
       			<TimeBasedTriggeringPolicy modulate="true" interval="1"/>
       		</Policies>
       		<!-- 最多保存日志文件数 -->
       		<DefaultRolloverStrategy max="20"/>
		</RollingFile>
		
		<RollingFile name="INFO" fileName="${LOG_HOME}/info.log" filePattern="${LOG_HOME}/info_%d{yyyy-MM-dd}.log">
			<PatternLayout charset="UTF-8" pattern="${ROLLINGFILE_PATTERN}"/>
			<Filters>  
				<ThresholdFilter level="warn" onMatch="DENY" onMismatch="NEUTRAL"/>
			 	<ThresholdFilter level="info" onMatch="ACCEPT" onMismatch="DENY" />
            </Filters> 
			<Policies>
       			<TimeBasedTriggeringPolicy modulate="true" interval="1"/>
       		</Policies>
       		<DefaultRolloverStrategy max="20"/>
		</RollingFile>
		
		<RollingFile name="WARN" fileName="${LOG_HOME}/warn.log" filePattern="${LOG_HOME}/warn_%d{yyyy-MM-dd}.log">
			<PatternLayout charset="UTF-8" pattern="${ROLLINGFILE_PATTERN}"/>
			<Filters>  
				<ThresholdFilter level="error" onMatch="DENY" onMismatch="NEUTRAL"/>  
			 	<ThresholdFilter level="warn" onMatch="ACCEPT" onMismatch="DENY" />
            </Filters> 
			<Policies>
       			<TimeBasedTriggeringPolicy modulate="true" interval="1"/>
       		</Policies>
       		<DefaultRolloverStrategy max="20"/>
		</RollingFile>
		
		<RollingFile name="ERROR" fileName="${LOG_HOME}/error.log" filePattern="${LOG_HOME}/error_%d{yyyy-MM-dd}.log">
			<PatternLayout charset="UTF-8" pattern="${ROLLINGFILE_PATTERN}"/>
			<Filters>  
			 	<ThresholdFilter level="error" onMatch="ACCEPT" onMismatch="DENY" />
            </Filters> 
			<Policies>
       			<TimeBasedTriggeringPolicy modulate="true" interval="1"/>
       		</Policies>
       		<DefaultRolloverStrategy max="20"/>
		</RollingFile>
	</appenders>

	<!--定义logger，只有定义了logger并引入的appender，appender才会生效-->
	<loggers>
		<!-- 只打印info级别以上的 -->
		<Root level="INFO">
			<AppenderRef ref="CONSOLE"/>
			<AppenderRef ref="DEBUG"/>
			<AppenderRef ref="INFO"/>
			<AppenderRef ref="WARN"/>
			<AppenderRef ref="ERROR"/>
		</Root>
	</loggers>

</configuration>
```

AOP

POST请求

```java
@ControllerAdvice
public class LogRequestBodyAdvice implements RequestBodyAdvice {

    public static final Logger LOGGER = LoggerFactory.getLogger(LogRequestBodyAdvice.class);

    @Override
    public boolean supports(MethodParameter methodParameter, Type type, Class<? extends HttpMessageConverter<?>> aClass) {
        return true;
    }

    @Override
    public HttpInputMessage beforeBodyRead(HttpInputMessage httpInputMessage, MethodParameter methodParameter, Type type, Class<? extends HttpMessageConverter<?>> aClass) throws IOException {
        return httpInputMessage;
    }

    @Override
    public Object afterBodyRead(Object body, HttpInputMessage httpInputMessage, MethodParameter methodParameter, Type type, Class<? extends HttpMessageConverter<?>> aClass) {

        Method method = methodParameter.getMethod();
        String classMappingUri = getClassMappingUri(method.getDeclaringClass());
        String methodMappingUri = getMethodMappingUri(method);
        if (!methodMappingUri.startsWith("/")) {
            methodMappingUri = "/" + methodMappingUri;
        }
        LOGGER.info("uri={} | requestBody={}", classMappingUri + methodMappingUri, JSON.toJSONString(body));
        return body;
    }

    @Override
    public Object handleEmptyBody(Object o, HttpInputMessage httpInputMessage, MethodParameter methodParameter, Type type, Class<? extends HttpMessageConverter<?>> aClass) {
        return o;
    }

    private String getMethodMappingUri(Method method) {

        RequestMapping requestMapping = method.getAnnotation(RequestMapping.class);
        return requestMapping == null ? "" : getMaxLength(requestMapping.value());
    }

    private String getClassMappingUri(Class<?> declaringClass) {
        RequestMapping classDeclaredAnnotation = declaringClass.getDeclaredAnnotation(RequestMapping.class);
        return classDeclaredAnnotation == null ? "" : getMaxLength(classDeclaredAnnotation.value());
    }

    private String getMaxLength(String[] strings) {
        String methodMappingUri = "";
        for (String string : strings) {
            if (string.length() > methodMappingUri.length()) {
                methodMappingUri = string;
            }
        }
        return methodMappingUri;
    }
}
```

Get请求

```java
@Aspect
@Component
public class LogRequestRecordAspect {

    public static final Logger LOGGER = LoggerFactory.getLogger(LogRequestRecordAspect.class);

    /**
     * 定义切点
     */
    @Pointcut("execution(* com.atguigu.aclservice.controller..*.*(..))")
    public void webRequestLogs() {
    }

    /**
     * 请求日志打印
     * @param point
     */
    @Before("webRequestLogs()")
    public void doBefore(JoinPoint point) {
        // 接收到请求，记录请求内容
        ServletRequestAttributes attributes = (ServletRequestAttributes) RequestContextHolder.getRequestAttributes();
        assert attributes != null;
        HttpServletRequest request = attributes.getRequest();
        String beanName = point.getSignature().getDeclaringTypeName();
        String methodName = point.getSignature().getName();
        String uri = request.getRequestURI();
        Object[] paramsArray = point.getArgs();
        LOGGER.info("uri={} | beanName={} | methodName={} | params={}", uri, beanName, methodName, paramsArray);
    }
}
```

响应

```java
@ControllerAdvice
public class LogResponseBodyAdvice implements ResponseBodyAdvice {

    public static final Logger LOGGER = LoggerFactory.getLogger(LogResponseBodyAdvice.class);

    @Override
    public boolean supports(MethodParameter methodParameter, Class aClass) {
        return true;
    }

    @Override
    public Object beforeBodyWrite(Object body, MethodParameter methodParameter, MediaType mediaType, Class aClass, ServerHttpRequest serverHttpRequest, ServerHttpResponse serverHttpResponse) {

        LOGGER.info("uri={} | responseBody={}", serverHttpRequest.getURI().getPath(), JSON.toJSONString(body));
        return body;
    }
}
```

application.properties

```properties
logging.config=classpath:log4j2.xml
```

# 7.整合接口文档

## 7.1引入依赖

```xml
   <properties>
        <java.version>1.8</java.version>
        <mybatis-plus.version>3.0.5</mybatis-plus.version>
        <velocity.version>2.0</velocity.version>
        <swagger.version>2.7.0</swagger.version>
        <jwt.version>0.7.0</jwt.version>
        <fastjson.version>1.2.28</fastjson.version>
        <gson.version>2.8.2</gson.version>
        <json.version>20170516</json.version>
        <cloud-alibaba.version>0.2.2.RELEASE</cloud-alibaba.version>
        <knife4j.version>2.0.3</knife4j.version>
        <guava.version>29.0-jre</guava.version>
</properties>
       
<dependency>
    <groupId>com.github.xiaoymin</groupId>
    <artifactId>knife4j-spring-boot-starter</artifactId>
    <version>${knife4j.version}</version>
</dependency>
<dependency>
    <groupId>com.google.guava</groupId>
    <artifactId>guava</artifactId>
    <version>${guava.version}</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>${fastjson.version}</version>
</dependency>

```

## 7.2Swagger配置

```java
package com.atguigu.utils;

import com.github.xiaoymin.knife4j.spring.annotations.EnableKnife4j;
import com.google.common.collect.Lists;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;
import springfox.bean.validators.configuration.BeanValidatorPluginsConfiguration;
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.*;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spi.service.contexts.SecurityContext;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

import java.util.List;

@Configuration
@EnableSwagger2
@EnableKnife4j
@Import(BeanValidatorPluginsConfiguration.class)
public class SwaggerConfig {

    @Bean
    public Docket createRestApi() {

        return new Docket(DocumentationType.SWAGGER_2)
                .useDefaultResponseMessages(false)
                .apiInfo(apiInfo())
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.atguigu.aclservice"))
                .paths(PathSelectors.any())
                .build()
                .groupName("znq-service")
                .securityContexts(Lists.newArrayList(securityContext())).securitySchemes(Lists.newArrayList(apiKey()));
    }

    private ApiKey apiKey() {
        return new ApiKey("Bearer ", "token", "header");
    }

    /**
     * Swagger apiinfo
     * @return
     */
    private ApiInfo apiInfo() {

        return new ApiInfoBuilder()
                .title("周年庆活动接口文档")
                .description("api接口")
                .contact(new Contact("alvins", null, "qintian2xy@163.com"))
                .version("1.0")
                .build();
    }

    private SecurityContext securityContext() {
        return SecurityContext.builder()
                .securityReferences(defaultAuth())
                .forPaths(PathSelectors.regex("/.*"))
                .build();
    }

    private List<SecurityReference> defaultAuth() {

        AuthorizationScope scope = new AuthorizationScope("global", "accessEverything");
        AuthorizationScope[] scopes = new AuthorizationScope[1];
        scopes[0] = scope;
        return Lists.newArrayList(new SecurityReference("Bearer ", scopes));
    }
}

```

# 8.shiro

```
Subject：可以理解为与shiro打交道的对象，该对象封装了一些对方的信息，shiro可以通过subject拿到这些信息
SecurityManager：Shiro的总经理，通过指使Authorizer和Authenticator等对subject进行授权和身份验证等工作
Realm：管理着一些如用户、角色、权限等重要信息，Shiro中所需的这些重要信息都是从Realm这里获取的，Realm本质上就是一个重要信息的数据源
Authenticator：认证器，负责Subject的认证操作，认证过程就是根据Subject提供的信息通过Realm查询到相关信息，然后做对比，支持扩展
Authorizer：授权器，控制着Subject对服务资源的访问权限
SessionManager：用于管理Session，这个Session可以是web的也可以不是web的。
SessionDao：把Session的 CRUD和存储介质联系起来的工具，存储介质可以是数据库，也可以是缓存，比如把session放到redis里面
CacheManager：缓存控制器，Realm管理的数据（用户、角色、权限）可以放到缓存里由CacheManager管理，提高认证授权等的速度
Cryptography：加密组件，Shiro提供了很多加解密算法的组件
```

## 8.1建表

```mssql
DROP TABLE IF EXISTS `user`;
CREATE TABLE `user` (
  `id` int(32) NOT NULL,
  `name` varchar(60) DEFAULT NULL,
  `mob` varchar(60) DEFAULT NULL,
  `email` varchar(150) DEFAULT NULL,
  `valid` int(2) DEFAULT NULL,
  `pticket` varchar(200) DEFAULT NULL,
  `role_id` int(32) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

DROP TABLE IF EXISTS `user_role`;
CREATE TABLE `user_role` (
  `uid` int(32) NOT NULL,
  `role_id` int(32) NOT NULL,
  PRIMARY KEY (`uid`,`role_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

DROP TABLE IF EXISTS `role`;
CREATE TABLE `role` (
  `id` int(32) NOT NULL,
  `description` varchar(255) DEFAULT NULL,
  `role` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

DROP TABLE IF EXISTS `role_permission`;
CREATE TABLE `role_permission` (
  `permission_id` int(32) NOT NULL,
  `role_id` int(32) NOT NULL,
  PRIMARY KEY (`permission_id`,`role_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

DROP TABLE IF EXISTS `permission`;
CREATE TABLE `permission` (
  `id` int(32) NOT NULL,
  `name` varchar(255) DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

## 8.2核心配置

```
Subject  用户主体 (把操作交给给SecurityManager)
SecurityManager 安全管理器 （关联Realm）
Realm Shiro链接的桥梁
```

## 8.3ShiroConfig

```java
@Configuration
public class ShiroConfig {
    /**
     * 创建ShiroFilterFactoryBean
     */
    @Bean
    public ShiroFilterFactoryBean getShiroFilterFactoryBean(@Qualifier("securityManager") DefaultWebSecurityManager securityManager){
        ShiroFilterFactoryBean factoryBean = new ShiroFilterFactoryBean();
        //设置SecurityManager
        factoryBean.setSecurityManager(securityManager);

        Map<String, Filter> filterMap = new HashMap<>();
        filterMap.put("jwt", new JWTFilter());
        factoryBean.setFilters(filterMap);
        /*
         * anon：无需认证就可以访问
         * authc：必须认证了才能访问
         * user：必须用有了 记住我 功能才能用
         * perms：拥有对某个资源的权限才能访问
         * role：拥有某个角色权限才能访问
         */
        //对于没有登录的请求码拦截后返回JSON的状态信息码，
//        Map<String, Filter> filterMap = new LinkedHashMap<>();
//        factoryBean.setFilters(filterMap);


        Map<String, String> filterChainDefinitionMap = new LinkedHashMap<>();
        filterChainDefinitionMap.put("/doc.html", "anon");
        filterChainDefinitionMap.put("/configuration/ui", "anon");
        filterChainDefinitionMap.put("/swagger-resources", "anon");
        filterChainDefinitionMap.put("/swagger-ui.html", "anon");
        filterChainDefinitionMap.put("/v2/api-docs", "anon");
        filterChainDefinitionMap.put("/v2/api-docs-ext", "anon");
        filterChainDefinitionMap.put("/webjars/**", "anon");
        filterChainDefinitionMap.put("/redis/**", "anon");
        filterChainDefinitionMap.put("/test/user/login", "anon");


        filterChainDefinitionMap.put("/**", "jwt");

        factoryBean.setFilterChainDefinitionMap(filterChainDefinitionMap);
        //配置Shiro内置过滤器
        return factoryBean;
    }

    /**
     * 创建SecurityManager
     */
    @Bean(name = "securityManager")
    public DefaultWebSecurityManager defaultWebSecurityManager(@Qualifier("UserRealm") UserRealm realm){
        DefaultWebSecurityManager securityManager = new DefaultWebSecurityManager();
        //设置Realm
        securityManager.setRealm(realm);
        return securityManager;
    }
    /**
     * Realm
     */
    @Bean(name = "UserRealm")
    public UserRealm getRealm(){
        return new UserRealm();
    }


    @Bean("lifecycleBeanPostProcessor")
    public LifecycleBeanPostProcessor lifecycleBeanPostProcessor() {
        return new LifecycleBeanPostProcessor();
    }

    @Bean
    @DependsOn(value = "lifecycleBeanPostProcessor")
    public DefaultAdvisorAutoProxyCreator advisorAutoProxyCreator(){
        DefaultAdvisorAutoProxyCreator advisorAutoProxyCreator = new DefaultAdvisorAutoProxyCreator();
        advisorAutoProxyCreator.setProxyTargetClass(true);
        return advisorAutoProxyCreator;
    }

    @Bean
    public AuthorizationAttributeSourceAdvisor authorizationAttributeSourceAdvisor(SecurityManager securityManager) {
        AuthorizationAttributeSourceAdvisor advisor = new AuthorizationAttributeSourceAdvisor();
        advisor.setSecurityManager(securityManager);
        return advisor;
    }
}
```

## 8.4自定义Realm

```java
public class UserRealm extends AuthorizingRealm {

    @Autowired
    UserService userService;

    /**
     * 重写不报错
     * @param token
     * @return
     */
    @Override
    public boolean supports(AuthenticationToken token) {
        return token instanceof JwtToken;
    }

    /**
     *
     * 授权
     * @param principalCollection
     * @return
     */
    @Override
    protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
        System.out.println("********************执行授权");
        //获取用户的用户名
//        String username = (String) principalCollection.iterator().next();
        String username = JWTUtil.getUsername(principalCollection.getPrimaryPrincipal().toString());
        //查询角色列表
        Set<String> roleList = userService.getRoleListByName(username);
        //查询权限列表
        Set<String> permissionsList = userService.getPermissionListByName(username);

        SimpleAuthorizationInfo info = new SimpleAuthorizationInfo();
        info.setRoles(roleList);
        info.setStringPermissions(permissionsList);
        return info;
    }

    /**
     * 认证
     * @param authenticationToken
     * @return
     * @throws AuthenticationException
     */
    @Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken authenticationToken) throws AuthenticationException {
        System.out.println("********************执行认证");
        String token = (String) authenticationToken.getPrincipal();
        if (token == null) {
            throw new AuthenticationException("token 无效！");
        }
        return new SimpleAuthenticationInfo(token, token, getName());
    }
}
```

## 8.5重写JWT过滤

```java
public class JWTFilter extends BasicHttpAuthenticationFilter {

    /**
     * 判断用户是否想要登入。
     * 检测header里面是否包含Authorization字段即可
     */
    @Override
    protected boolean isLoginAttempt(ServletRequest request, ServletResponse response) {
        HttpServletRequest req = (HttpServletRequest) request;
        String authorization = req.getHeader("token");
        return authorization != null;
    }

    /**
     *
     */
    @Override
    protected boolean executeLogin(ServletRequest request, ServletResponse response) throws Exception {
        HttpServletRequest httpServletRequest = (HttpServletRequest) request;
        String authorization = httpServletRequest.getHeader("token");
        JwtToken token = new JwtToken(authorization);
        // 提交给realm进行登入，如果错误他会抛出异常并被捕获
        getSubject(request, response).login(token);
        // 如果没有抛出异常则代表登入成功，返回true
        return true;
    }

    /**
     * 这里我们详细说明下为什么最终返回的都是true，即允许访问
     * 例如我们提供一个地址 GET /article
     * 登入用户和游客看到的内容是不同的
     * 如果在这里返回了false，请求会被直接拦截，用户看不到任何东西
     * 所以我们在这里返回true，Controller中可以通过 subject.isAuthenticated() 来判断用户是否登入
     * 如果有些资源只有登入用户才能访问，我们只需要在方法上面加上 @RequiresAuthentication 注解即可
     * 但是这样做有一个缺点，就是不能够对GET,POST等请求进行分别过滤鉴权(因为我们重写了官方的方法)，但实际上对应用影响不大
     */
    @Override
    protected boolean isAccessAllowed(ServletRequest request, ServletResponse response, Object mappedValue) {
        if (isLoginAttempt(request, response)) {
            try {
                executeLogin(request, response);
            } catch (Exception e) {
                response401(request, response);
            }
        }
        return true;
    }

    /**
     * 对跨域提供支持
     */
    @Override
    protected boolean preHandle(ServletRequest request, ServletResponse response) throws Exception {
        HttpServletRequest httpServletRequest = (HttpServletRequest) request;
        HttpServletResponse httpServletResponse = (HttpServletResponse) response;
        httpServletResponse.setHeader("Access-control-Allow-Origin", httpServletRequest.getHeader("Origin"));
        httpServletResponse.setHeader("Access-Control-Allow-Methods", "GET,POST,OPTIONS,PUT,DELETE");
        httpServletResponse.setHeader("Access-Control-Allow-Headers", httpServletRequest.getHeader("Access-Control-Request-Headers"));
        // 跨域时会首先发送一个option请求，这里我们给option请求直接返回正常状态
        if (httpServletRequest.getMethod().equals(RequestMethod.OPTIONS.name())) {
            httpServletResponse.setStatus(HttpStatus.OK.value());
            return false;
        }
        return super.preHandle(request, response);
    }

    /**
     * 将非法请求跳转到 /401
     */
    private void response401(ServletRequest req, ServletResponse resp) {
        try {
            HttpServletResponse httpServletResponse = (HttpServletResponse) resp;
            httpServletResponse.sendRedirect("/401");
        } catch (IOException e) {
        }
    }
}
```

## 8.6JWT工具

```java
重写 JWtToken

public class JwtToken implements AuthenticationToken {

    // 密钥
    private String token;

    public JwtToken(String token) {
        this.token = token;
    }
    @Override
    public Object getPrincipal() {
        return token;
    }
    @Override
    public Object getCredentials() {
        return token;
    }
}
```

```java
JWt工具类
public class JWTUtil {

    //过期时间
    public static final long EXPIRE = 1000 * 60 * 60 * 24;
    //密钥
    public static final String APP_SECRET = "ukc8BDbRigUDaY6pZFfWus2jZWLPHO";

    //生成token
    public static String createToken(String username){

        String JwtToken = Jwts.builder()
                .setHeaderParam("typ", "JWT")
                .setHeaderParam("alg", "HS256")
                //分类 设置过期时间
                .setSubject("guli-user")
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + EXPIRE))

                //主体用户信息
//                .claim("id", id)
                .claim("username", username)

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
    public static boolean verify(String jwtToken) {
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
     * 根据token获取会员id /获取 username
     * @param request
     * @return
     * 获取用户信息
     */
    public static String getUsername(HttpServletRequest request) {
        String jwtToken = request.getHeader("token");
        if(StringUtils.isEmpty(jwtToken)) return "";
        Jws<Claims> claimsJws = Jwts.parser().setSigningKey(APP_SECRET).parseClaimsJws(jwtToken);
        Claims claims = claimsJws.getBody();
        return (String)claims.get("username");
    }

    /**
     * 根据token获取用户username
     * @param request
     * @return
     */
    public static String getUsername(String jwtToken) {
        if(StringUtils.isEmpty(jwtToken)) return "";
            Jws<Claims> claimsJws = Jwts.parser().setSigningKey(APP_SECRET).parseClaimsJws(jwtToken);
        Claims claims = claimsJws.getBody();
        return (String)claims.get("username");
    }
}
```

## 8.7权限注解

```java
    /**
     * 根据用户token查询权限列表
     */
    @RequiresPermissions("/test/user/update")
    @PostMapping("add")
    public R add(){
        return R.ok().message("增加");
    }

    @RequiresPermissions("/test/user/update")
    @PostMapping("update")
    public R update(){
        return R.ok().message("修改");
    }

    @RequiresPermissions("/test/user/delete")
    @PostMapping("delete")
    public R delete(){
        return R.ok().message("删除");
    }

    @RequiresPermissions("/test/user/query")
    @PostMapping("query")
    public R query(){
        return R.ok().message("查询");
    }
```

## 8.8登录

```java
 @PostMapping("login")
    public R login(String username, String password) {
        if (StringUtils.isEmpty(username) || StringUtils.isEmpty(password)) {
            return R.error().message("用户名密码不能为空");
        }
        try{
            QueryWrapper<User> wrapper = new QueryWrapper<>();
            wrapper.eq("name", username);
            User user = userService.getOne(wrapper);

            if (user == null) {
                return R.error().message("用户名不存在");
            }
            if (password.equals(user.getMob())) {
                return R.ok().message("登录成功").data("token", JWTUtil.createToken(username));
            }else{
                return R.error().message("密码错误");
            }
        }catch (Exception e){
        }
        return R.error();
    }
```

## 8.9异常捕捉

```java
 	@ExceptionHandler(AuthorizationException.class)
    @ResponseBody //为了返回数据
    public R error(AuthorizationException e) {
        log.error(e.getMessage());
        return R.error().code(401).message("没有权限");
    }
```

