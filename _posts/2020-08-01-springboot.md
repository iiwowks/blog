---
layout: post
title: "spring boot learn"
date: 2020-08-01
category: Backend
author: zhengjunan
published: true
photoswipe: true
syntaxhighlight: true
---

# Spring Boot

**优点：**

1. 让所有 Spring 开发者更快入门
2. 开箱即用，提供各种默认的配置来简化项目配置
3. 内嵌式容器简化 web 项目
4. 没有冗余代码生成和 xml 配置的要求

**微服务架构**：把每个功能模块独立出来，功能模块动态组合。好处： 节省了调用资源，每个功能元素的服务是一个可替换的、可独立升级的软件代码。高内聚、低耦合。

- 构建一个功能独立的微服务应用单元，可以使用`springBoot`，可以帮我们快速创建一个应用
- 大型分布式网络服务的调用，这部分由`spring cloud`来完成，实现分布式
- 在分布式中间，进行流式数据计算、批处理，有`spring cloud data flow`

## hello world spring boot

**pom.xml：**

- 项目的元数据信息：创建的时候输入`project metadata`的部分，也就是 maven 项目的基本元素，包括： `groupId, artifactId, version, name, description`等
- **parent**: 继承`spring-boot-starter-parent`的依赖管理，控制版本与打包等内容
- **dependencies**: 项目具体依赖，包含了`spring-boot-starter-web`用于实现 HTTP 接口；`spring-boot-starter-test`用于编写单元测试的依赖包。（使用 springmvc 创建 web 应用程序的，使用 tomcat 作为默认嵌入式容器）
- **build**：构建配置部分。默认使用了`spring-boot-maven-plugin`, 配合`spring-boot-starter-parent`就可以把`spring boot`应用打包成 jar 来直接运行
- `spring-boot-dependencies`：核心依赖在父工程中
- 在写或者引入 springboot 依赖的时候，不需要指定版本，就是因为有这些版本仓库

**启动器：**

1. springboot 会将所有的功能场景，变成一个个启动器
2. 我们要使用什么功能，只需要找到对应的启动器就行

主程序：

```java
// 程序的主入口， @SpringBootApplication: 标注这是一个springboot 应用
@SpringBootApplication
public class DemoApplication {

   public static void main(String[] args) {
       // 将springboot应用启动
       SpringApplication.run(DemoApplication.class, args);
   }
}
```

**结论：**

1. SpringBoot 在启动的时候从类路径下的`META-INF/spring.factories`中获取`EnableAutoConfiguration`指定的值
2. 将这些值作为自动配置类导入容器 ， 自动配置类就生效 ， 帮我们进行自动配置工作；
3. 整个 J2EE 的整体解决方案和自动配置都在`springboot-autoconfigure`的 jar 包中；
4. 它会给容器中导入非常多的自动配置类 （`xxxAutoConfiguration`）, 就是给容器中导入这个场景需要的所有组件 ， 并配置好这些组件 ；
5. 有了自动配置类 ， 免去了我们手动编写配置注入功能组件等的工作；

### SpringApplication

**这个类主要做了以下四件事情：**

1、推断应用的类型是普通的项目还是 Web 项目

2、查找并加载所有可用初始化器 ， 设置到 initializers 属性中

3、找出所有的应用程序监听器，设置到 listeners 属性中

4、推断并设置 main 方法的定义类，找到运行的主类

### run() 方法

![springbootApplication](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7L1vFQMnaRIJSmeZ58T2eZicjafiawQLp9u8wc4ic1Mjy6OyfibzfjVofeL5pnS1NSFKVjlIg6neI9ySg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## SpringBoot 配置

### Yaml 语法

yaml 可以直接给实体类赋值

配置文件：修改 Spring boot 自动配置的默认值

- `application.properties`

  - 语法格式： key=value

- `application.yaml`
  - 语法格式： key: value

@Value 这个使用起来并不友好！我们需要为每个属性单独注解赋值，比较麻烦；我们来看个功能对比图

![Image](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7KtjyIb9NEaYlz0tCWSiboOYjMibiaov73iaTsiaWEPoArDcAB1Ooibx9uR5JxtacIuicHblEtUI9SrySX2A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

1、`@ConfigurationProperties`只需要写一次即可 ， `@Value`则需要每个字段都添加

2、**松散绑定**：比如我的 yml 中写的`last-name`，这个和`lastName`是一样的， - 后面跟着的字母默认是大写的。

3、**JSR303 数据校验** ， 这个就是我们可以在字段是**增加一层过滤器验证** ， 可以保证数据的合法性

4、**复杂类型封装**，yml 中可以封装对象 ， 使用 value 就不支持

### JSR303 校验

JSR-303 是 JAVA EE 6 中的一项子规范，叫做 Bean Validation，Hibernate Validator 是 Bean Validation 的参考实现 . Hibernate Validator 提供了 JSR 303 规范中所有内置 constraint 的实现，除此之外还有一些附加的 constraint。

**Bean Validation 中内置的 constraint**

![img](https:////upload-images.jianshu.io/upload_images/3145530-8ae74d19e6c65b4c?imageMogr2/auto-orient/strip|imageView2/2/w/654/format/webp)

​ **Hibernate Validator 附加的 constraint**

![img](https:////upload-images.jianshu.io/upload_images/3145530-10035c6af8e90a7c?imageMogr2/auto-orient/strip|imageView2/2/w/432/format/webp)

**自动装配原理：**

1、SpringBoot 启动会加载大量的自动配置类

2、我们看我们需要的功能有没有在 SpringBoot 默认写好的自动配置类当中；

3、我们再来看这个自动配置类中到底配置了哪些组件；（只要我们要用的组件存在在其中，我们就不需要再手动配置了）

4、给容器中自动配置类添加组件的时候，会从 properties 类中获取某些属性。我们只需要在配置文件中指定这些属性的值即可；

**xxxxAutoConfigurartion：自动配置类；**给容器中添加组件

**xxxxProperties:封装配置文件中相关属性；**

## Springboot Web 开发

要解决的问题：

1. 导入静态资源
2. 首页
3. jsp,模版引擎`Thymeleaf`
4. 装配扩展`SpringMVC`
5. 增删改查
6. 拦截器
7. 国际化

### 导入静态资源

在 springboot 中，我们可以使用以下方式处理静态资源：

- `webjars` --> `localhost:8080/webjars/`：可以通过 meaven 的方式导入 jar 包，导入 web 资源
- `public, static, /**, resources` --> `localhost:8080/`
- **优先级：resources > static > public** 优先访问这些文件夹的资源

### 模版引擎

- `freemarker`
- `thymeleaf`
  模版引擎的作用就是写一个页面的模版，对于一些动态的值，直接写表达式，组装数据。将模版和数据交给模版引擎，模版引擎解析表达式，填充到指定的位置，生成我想要的内容。可以理解和 jsp 一样。

## 配置国际化解析

在 Spring 中有一个国际化的 Locale （区域信息对象）；里面有一个叫做`LocaleResolver `（获取区域信息对象）的解析器！
那假如我们现在想点击链接让我们的国际化资源生效，就需要让我们自己的 Locale 生效！

我们去自己写一个自己的`LocaleResolver`，可以在链接上携带区域信息！

修改一下前端页面的跳转连接：

```html
<!-- 这里传入参数不需要使用 ？使用 （key=value）-->
<a class="btn btn-sm" th:href="@{/index.html(l='zh_CN')}">中文</a>
<a class="btn btn-sm" th:href="@{/index.html(l='en_US')}">English</a>
```

我们去写一个处理的组件类！

```java
//可以在链接上携带区域信息
public class MyLocaleResolver implements LocaleResolver {
 //解析请求
 @Override
 public Locale resolveLocale(HttpServletRequest request) {

     String language = request.getParameter("l");
     Locale locale = Locale.getDefault(); // 如果没有获取到就使用系统默认的
     //如果请求链接不为空
     if (!StringUtils.isEmpty(language)){
         //分割请求参数
         String[] split = language.split("_");
         //国家，地区
         locale = new Locale(split[0],split[1]);
     }
     return locale;
 }
 @Override
 public void setLocale(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Locale locale) {

 }
}
```

为了让我们的区域化信息能够生效，我们需要再配置一下这个组件！在我们自己的`MvcConofig`下添加`bean`；

```java
@Bean
public LocaleResolver localeResolver(){
    return new MyLocaleResolver();
}
```

**小结：**

1. 首页配置：
   - 注意点，所有页面的静态资源都需要使用 thymeleaf 接管
   - url:@{}
2. 页面国际化
   - 我们需要配置**i18n**文件
   - 我们如果需要在项目中进行按钮自动切换，我们需要定义一个组件`LocalResolver`
   - 记得将自己写的组件配置到 spring 容器`@Bean`
   - `#{}`

### Thymeleaf 语法

Thymeleaf 官网：[https://www.thymeleaf.org/](https://www.thymeleaf.org/) ， 简单看一下官网！我们去下载 Thymeleaf 的官方文档！在线文档：[https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html](https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html)

**1、我们可以使用任意的 th:attr 来替换 Html 中原生属性的值！**

**2、我们能写哪些表达式呢？**

```shell
Simple expressions:（表达式语法）
Variable Expressions: ${...}：获取变量值；OGNL；
    1）、获取对象的属性、调用方法
    2）、使用内置的基本对象：#18
         #ctx : the context object.
         #vars: the context variables.
         #locale : the context locale.
         #request : (only in Web Contexts) the HttpServletRequest object.
         #response : (only in Web Contexts) the HttpServletResponse object.
         #session : (only in Web Contexts) the HttpSession object.
         #servletContext : (only in Web Contexts) the ServletContext object.

    3）、内置的一些工具对象：
　　　　　　#execInfo : information about the template being processed.
　　　　　　#uris : methods for escaping parts of URLs/URIs
　　　　　　#conversions : methods for executing the configured conversion service (if any).
　　　　　　#dates : methods for java.util.Date objects: formatting, component extraction, etc.
　　　　　　#calendars : analogous to #dates , but for java.util.Calendar objects.
　　　　　　#numbers : methods for formatting numeric objects.
　　　　　　#strings : methods for String objects: contains, startsWith, prepending/appending, etc.
　　　　　　#objects : methods for objects in general.
　　　　　　#bools : methods for boolean evaluation.
　　　　　　#arrays : methods for arrays.
　　　　　　#lists : methods for lists.
　　　　　　#sets : methods for sets.
　　　　　　#maps : methods for maps.
　　　　　　#aggregates : methods for creating aggregates on arrays or collections.
==================================================================================

  Selection Variable Expressions: *{...}：选择表达式：和${}在功能上是一样；
  Message Expressions: #{...}：获取国际化内容
  Link URL Expressions: @{...}：定义URL；
  Fragment Expressions: ~{...}：片段引用表达式

Literals（字面量）
      Text literals: 'one text' , 'Another one!' ,…
      Number literals: 0 , 34 , 3.0 , 12.3 ,…
      Boolean literals: true , false
      Null literal: null
      Literal tokens: one , sometext , main ,…

Text operations:（文本操作）
    String concatenation: +
    Literal substitutions: |The name is ${name}|

Arithmetic operations:（数学运算）
    Binary operators: + , - , * , / , %
    Minus sign (unary operator): -

Boolean operations:（布尔运算）
    Binary operators: and , or
    Boolean negation (unary operator): ! , not

Comparisons and equality:（比较运算）
    Comparators: > , < , >= , <= ( gt , lt , ge , le )
    Equality operators: == , != ( eq , ne )

Conditional operators:条件运算（三元运算符）
    If-then: (if) ? (then)
    If-then-else: (if) ? (then) : (else)
    Default: (value) ?: (defaultvalue)

Special tokens:
    No-Operation: _
```

# SpringData 简介

- 对于数据访问层，无论是 SQL(关系型数据库) 还是 NOSQL(非关系型数据库)，Spring Boot 底层都是采用 Spring Data 的方式进行统一处理。

- Spring Boot 底层都是采用 Spring Data 的方式进行统一处理各种数据库，Spring Data 也是 Spring 中与 Spring Boot、Spring Cloud 等齐名的知名项目。

- Sping Data 官网：[https://spring.io/projects/spring-data](https://spring.io/projects/spring-data)

- 数据库相关的启动器 ：可以参考官方文档：[https://docs.spring.io/spring-boot/docs/2.2.5.RELEASE/reference/htmlsingle/#using-boot-starter](https://docs.spring.io/spring-boot/docs/2.2.5.RELEASE/reference/htmlsingle/#using-boot-starter)

# 整合 JDBC

## 创建测试项目测试数据源

1. 我去新建一个项目测试：springboot-data-jdbc ; 引入相应的模块！基础模块

2. 项目建好之后，发现自动帮我们导入了如下的启动器：

   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-jdbc</artifactId>
   </dependency>
   <dependency>
       <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
       <scope>runtime</scope>
   </dependency>
   ```

3. 编写 yaml 配置文件连接数据库；

   ```yaml
   spring:
     datasource:
       username: root
       password: admin
       #?serverTimezone=UTC解决时区的报错
       url: jdbc:mysql://localhost:3306/mybatis?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
       driver-class-name: com.mysql.cj.jdbc.Driver
   ```

4. 配置完这一些东西后，我们就可以直接去使用了，因为 SpringBoot 已经默认帮我们进行了自动配置；去测试类测试一下

   ```java
   @SpringBootTest
   class SpringbootDataJdbcApplicationTests {

       //DI注入数据源
       @Autowired
       DataSource dataSource;

       @Test
       public void contextLoads() throws SQLException {
           //看一下默认数据源
           System.out.println(dataSource.getClass());
           //获得连接
           Connection connection = dataSource.getConnection();
           System.out.println(connection);
           //关闭连接
           connection.close();
       }
   }
   ```

结果：我们可以看到他默认给我们配置的数据源为 : class com.zaxxer.hikari.HikariDataSource ， 我们并没有手动配置

我们来全局搜索一下，找到数据源的所有自动配置都在 ：DataSourceAutoConfiguration 文件：

```java
@Import(
    {Hikari.class, Tomcat.class, Dbcp2.class, Generic.class, DataSourceJmxConfiguration.class}
)
protected static class PooledDataSourceConfiguration {
    protected PooledDataSourceConfiguration() {
    }
}
```

这里导入的类都在 DataSourceConfiguration 配置类下，可以看出 Spring Boot 2.2.5 默认使用 HikariDataSource 数据源，而以前版本，如 Spring Boot 1.5 默认使用 org.apache.tomcat.jdbc.pool.DataSource 作为数据源；

**<font color=red>HikariDataSource 号称 Java WEB 当前速度最快的数据源，相比于传统的 C3P0 、DBCP、Tomcat jdbc 等连接池更加优秀；</font>**

**可以使用 spring.datasource.type 指定自定义的数据源类型，值为 要使用的连接池实现的完全限定名。**

关于数据源我们并不做介绍，有了数据库连接，显然就可以 CRUD 操作数据库了。但是我们需要先了解一个对象 JdbcTemplate

## JDBCTemplate

1. 有了数据源(com.zaxxer.hikari.HikariDataSource)，然后可以拿到数据库连接(java.sql.Connection)，有了连接，就可以使用原生的 JDBC 语句来操作数据库；

2. 即使不使用第三方第数据库操作框架，如 MyBatis 等，Spring 本身也对原生的 JDBC 做了轻量级的封装，即 JdbcTemplate。

3. 数据库操作的所有 CRUD 方法都在 JdbcTemplate 中。

4. Spring Boot 不仅提供了默认的数据源，同时默认已经配置好了 JdbcTemplate 放在了容器中，程序员只需自己注入即可使用

5. JdbcTemplate 的自动配置是依赖 org.springframework.boot.autoconfigure.jdbc 包下的 JdbcTemplateConfiguration 类

**JdbcTemplate 主要提供以下几类方法：**

- execute 方法：可以用于执行任何 SQL 语句，一般用于执行 DDL 语句；
- update 方法及 batchUpdate 方法：update 方法用于执行新增、修改、删除等语句；batchUpdate 方法用于执行批处理相关语句；
- query 方法及 queryForXXX 方法：用于执行查询相关语句；
- call 方法：用于执行存储过程、函数相关语句。

## 测试

编写一个 Controller，注入 jdbcTemplate，编写测试方法进行访问测试；

```java
package nuc.ss.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;
import java.util.Map;

@RestController
public class JDBCController {

    @Autowired
    JdbcTemplate jdbcTemplate;

    // 查询数据库的所有信息
    // 没有实体类，获取数据库的东西，怎么获取？ Map
    @GetMapping("/userList")
    public List<Map<String,Object>> userList() {
        String sql = "select * from user";
        List<Map<String, Object>> maps = jdbcTemplate.queryForList(sql);
        return maps;
    }

    @GetMapping("/addUser")
    public String addUser() {
        String sql = "insert into mybatis.user(id, name, pwd) values(7,'小明','123456')";
        jdbcTemplate.update(sql);
        return "update-ok";
    }

    @GetMapping("/updateUser/{id}")
    public String updateUser(@PathVariable("id") int id) {
        String sql = "update mybatis.user set name  = ?,pwd = ? where id = " + id;
        //封装
        Object[] objects = new Object[2];

        objects[0] = "小明2";
        objects[1] = "aaaaaaa";

        jdbcTemplate.update(sql,objects);
        return "update-ok";
    }

    @GetMapping("/deleteUser/{id}")
    public String deleteUser(@PathVariable("id") int id) {
        String sql = "delete from mybatis.user where id = ?";
        jdbcTemplate.update(sql,id);
        return "update-ok";
    }
}

```

测试请求，结果正常；

到此，CURD 的基本操作，使用 JDBC 就搞定了。

## 集成 Druid

## Druid 简介

- Java 程序很大一部分要操作数据库，为了提高性能操作数据库的时候，又不得不使用数据库连接池。

- Druid 是阿里巴巴开源平台上一个数据库连接池实现，结合了 C3P0、DBCP 等 DB 池的优点，同时加入了日志监控。

- Druid 可以很好的监控 DB 池连接和 SQL 的执行情况，天生就是针对监控而生的 DB 连接池。

- Druid 已经在阿里巴巴部署了超过 600 个应用，经过一年多生产环境大规模部署的严苛考验。

- Spring Boot 2.0 以上默认使用 Hikari 数据源，可以说 Hikari 与 Driud 都是当前 Java Web 上最优秀的数据源，我们来重点介绍 Spring Boot 如何集成 Druid 数据源，如何实现数据库监控。

- Github 地址：https://github.com/alibaba/druid/

**com.alibaba.druid.pool.DruidDataSource 基本配置参数如下：**

|           **配置**            |       **缺省值**       | **说明**                                                                                                                                                                                                                              |
| :---------------------------: | :--------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|             name              |                        | 配置这个属性的意义在于，如果存在多个数据源，监控的时候可以通过名字来区分开来。 如果没有配置，将会生成一个名字，格式是：“DataSource-” + System.identityHashCode(this)                                                                  |
|            jdbcUrl            |                        | 连接数据库的 url，不同数据库不一样。例如： mysql : jdbc:mysql://10.20.153.104:3306/druid2 oracle : jdbc:oracle:thin:@10.20.149.85:1521:ocnauto                                                                                        |
|           username            |                        | 连接数据库的用户名                                                                                                                                                                                                                    |
|           password            |                        | 连接数据库的密码。如果你不希望密码直接写在配置文件中，可以使用 ConfigFilter。详细看这里：[https://github.com/alibaba/druid/wiki/%E4%BD%BF%E7%94%A8ConfigFilter](https://github.com/alibaba/druid/wiki/%E4%BD%BF%E7%94%A8ConfigFilter) |
|        driverClassName        |   根据 url 自动识别    | 这一项可配可不配，如果不配置 druid 会根据 url 自动识别 dbType，然后选择相应的 driverClassName(建议配置下)                                                                                                                             |
|          initialSize          |           0            | 初始化时建立物理连接的个数。初始化发生在显示调用 init 方法，或者第一次 getConnection 时                                                                                                                                               |
|           maxActive           |           8            | 最大连接池数量                                                                                                                                                                                                                        |
|            maxIdle            |           8            | 已经不再使用，配置了也没效果                                                                                                                                                                                                          |
|            minIdle            |                        | 最小连接池数量                                                                                                                                                                                                                        |
|            maxWait            |                        | 获取连接时最大等待时间，单位毫秒。配置了 maxWait 之后，缺省启用公平锁，并发效率会有所下降，如果需要可以通过配置 useUnfairLock 属性为 true 使用非公平锁。                                                                              |
|    poolPreparedStatements     |         false          | 是否缓存 preparedStatement，也就是 PSCache。PSCache 对支持游标的数据库性能提升巨大，比如说 oracle。在 mysql 下建议关闭。                                                                                                              |
|   maxOpenPreparedStatements   |           -1           | 要启用 PSCache，必须配置大于 0，当大于 0 时，poolPreparedStatements 自动触发修改为 true。在 Druid 中，不会存在 Oracle 下 PSCache 占用内存过多的问题，可以把这个数值配置大一些，比如说 100                                             |
|        validationQuery        |                        | 用来检测连接是否有效的 sql，要求是一个查询语句。如果 validationQuery 为 null，testOnBorrow、testOnReturn、testWhileIdle 都不会其作用。                                                                                                |
|    validationQueryTimeout     |                        | 单位:秒，检测连接是否有效的超时时间。底层调用 jdbc<br/>Statement 对象的 void setQueryTimeout(int seconds)方法                                                                                                                         |
|         testOnBorrow          |          true          | 申请连接时执行 validationQuery 检测连接是否有效，做了这个配置会降低性能                                                                                                                                                               |
|         testOnReturn          |         false          | 归还连接时执行 validationQuery 检测连接是否有效，做了这个配置会降低性能                                                                                                                                                               |
|         testWhileIdle         |         false          | 建议配置为 true，不影响性能，并且保证安全性。申请连接的时候检测，如果空闲时间大于 timeBetweenEvictionRunsMillis，执行 validationQuery 检测连接是否有效                                                                                |
| timeBetweenEvictionRunsMillis | 1 分钟<br/>( 1.0.14 )  | 有两个含义： 1) Destroy 线程会检测连接的间隔时间 2) testWhileIdle 的判断依据，详细看 testWhileIdle 属性的说明                                                                                                                         |
|    numTestsPerEvictionRun     |                        | 不再使用，一个 DruidDataSource 只支持一个 EvictionRun                                                                                                                                                                                 |
|  minEvictableIdleTimeMillis   | 30 分钟<br/>( 1.0.14 ) | 连接保持空闲而不被驱逐的最长时间                                                                                                                                                                                                      |
|      connectionInitSqls       |                        | 物理连接初始化的时候执行的 sql                                                                                                                                                                                                        |
|        exceptionSorter        |  根据 dbType 自动识别  | 当数据库抛出一些不可恢复的异常时，抛弃连接                                                                                                                                                                                            |
|            filters            |                        | 属性类型是字符串，通过别名的方式配置扩展插件，常用的插件有： 监控统计用的 filter:stat 日志用的 filter:log4j 防御 sql 注入的 filter:wall                                                                                               |
|         proxyFilters          |                        | 类型是 List<com.alibaba.druid.filter.Filter>，如果同时配置了 filters 和 proxyFilters，是组合关系，并非替换关系                                                                                                                        |

## 配置数据源

1. 添加上 Druid 数据源依赖，这个依赖可以从 Maven 仓库官网[<font color=red>Maven Respository</font>](https://mvnrepository.com/artifact/com.alibaba/druid)中获取

   ```xml
   <dependency>
       <groupId>com.alibaba</groupId>
       <artifactId>druid</artifactId>
       <version>1.1.23</version>
   </dependency>
   ```

   ![image-20200727215315060](https://gitee.com/lzh_gitee/springboot_image/raw/master/img/image-20200727215315060.png)

2. 切换数据源；之前已经说过 Spring Boot 2.0 以上默认使用 `com.zaxxer.hikari.HikariDataSource `数据源，但可以通过 `spring.datasource.type` 指定数据源。

   ```yam
   spring:
     datasource:
       username: root
       password: 123456
       url: jdbc:mysql://localhost:3306/springboot?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
       driver-class-name: com.mysql.cj.jdbc.Driver
       type: com.alibaba.druid.pool.DruidDataSource # 自定义数据源
   ```

3. 数据源切换之后，在测试类中注入 DataSource，然后获取到它，输出一看便知是否成功切换；

   ![image-20200727222109497](https://gitee.com/lzh_gitee/springboot_image/raw/master/img/image-20200727222109497.png)

4. 切换成功！既然切换成功，就可以设置数据源连接初始化大小、最大连接数、等待时间、最小连接数 等设置项；可以查看源码

   ```yaml
   spring:
     datasource:
       username: root
       password: 123456
       #?serverTimezone=UTC解决时区的报错
       url: jdbc:mysql://localhost:3306/springboot?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
       driver-class-name: com.mysql.cj.jdbc.Driver
       type: com.alibaba.druid.pool.DruidDataSource

       #Spring Boot 默认是不注入这些属性值的，需要自己绑定
       #druid 数据源专有配置
       initialSize: 5
       minIdle: 5
       maxActive: 20
       maxWait: 60000
       timeBetweenEvictionRunsMillis: 60000
       minEvictableIdleTimeMillis: 300000
       validationQuery: SELECT 1 FROM DUAL
       testWhileIdle: true
       testOnBorrow: false
       testOnReturn: false
       poolPreparedStatements: true

       #配置监控统计拦截的filters，stat:监控统计、log4j：日志记录、wall：防御sql注入
       #如果允许时报错  java.lang.ClassNotFoundException: org.apache.log4j.Priority
       #则导入 log4j 依赖即可，Maven 地址：https://mvnrepository.com/artifact/log4j/log4j
       filters: stat,wall,log4j
       maxPoolPreparedStatementPerConnectionSize: 20
       useGlobalDataSourceStat: true
       connectionProperties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=500
   ```

5. 导入 Log4j 的依赖

   ```xml
   <!-- https://mvnrepository.com/artifact/log4j/log4j -->
   <dependency>
       <groupId>log4j</groupId>
       <artifactId>log4j</artifactId>
       <version>1.2.17</version>
   </dependency>
   ```

6. 现在需要程序员自己为 DruidDataSource 绑定全局配置文件中的参数，再添加到容器中，而不再使用 Spring Boot 的自动生成了；我们需要 自己添加 DruidDataSource 组件到容器中，并绑定属性；

   ```java
   package nuc.ss.config;

   import com.alibaba.druid.pool.DruidDataSource;
   import org.springframework.boot.context.properties.ConfigurationProperties;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;

   import javax.sql.DataSource;

   @Configuration
   public class DruidConfig {

       /*
          将自定义的 Druid数据源添加到容器中，不再让 Spring Boot 自动创建
          绑定全局配置文件中的 druid 数据源属性到 com.alibaba.druid.pool.DruidDataSource从而让它们生效
          @ConfigurationProperties(prefix = "spring.datasource")：作用就是将 全局配置文件中
          前缀为 spring.datasource的属性值注入到 com.alibaba.druid.pool.DruidDataSource 的同名参数中
        */
       @ConfigurationProperties(prefix = "spring.datasource")
       @Bean
       public DataSource druidDataSource() {
           return new DruidDataSource();
       }

   }
   ```

7. 去测试类中测试一下；看是否成功！

   ```java
   @SpringBootTest
   class SpringbootDataJdbcApplicationTests {

       //DI注入数据源
       @Autowired
       DataSource dataSource;

       @Test
       public void contextLoads() throws SQLException {
           //看一下默认数据源
           System.out.println(dataSource.getClass());
           //获得连接
           Connection connection =   dataSource.getConnection();
           System.out.println(connection);

           DruidDataSource druidDataSource = (DruidDataSource) dataSource;
           System.out.println("druidDataSource 数据源最大连接数：" + druidDataSource.getMaxActive());
           System.out.println("druidDataSource 数据源初始化连接数：" + druidDataSource.getInitialSize());

           //关闭连接
           connection.close();
       }
   }
   ```

8. 输出结果 ：可见配置参数已经生效！

   ![image-20200727233746228](https://gitee.com/lzh_gitee/springboot_image/raw/master/img/image-20200727233746228.png)

## 配置 Druid 数据源监控

Druid 数据源具有监控的功能，并提供了一个 web 界面方便用户查看，类似安装 路由器 时，人家也提供了一个默认的 web 页面。

所以第一步需要设置 Druid 的后台管理页面，比如 登录账号、密码 等；配置后台管理；

```java
//配置 Druid 监控管理后台的Servlet；
//内置 Servlet 容器时没有web.xml文件，所以使用 Spring Boot 的注册 Servlet 方式
@Bean
public ServletRegistrationBean statViewServlet() {
    ServletRegistrationBean bean = new ServletRegistrationBean(new StatViewServlet(), "/druid/*");

    // 这些参数可以在 com.alibaba.druid.support.http.StatViewServlet
    // 的父类 com.alibaba.druid.support.http.ResourceServlet 中找到
    Map<String, String> initParams = new HashMap<>();
    initParams.put("loginUsername", "root"); //后台管理界面的登录账号
    initParams.put("loginPassword", "admin"); //后台管理界面的登录密码

    //后台允许谁可以访问
    //initParams.put("allow", "localhost")：表示只有本机可以访问
    //initParams.put("allow", "")：为空或者为null时，表示允许所有访问
    initParams.put("allow", "");
    //deny：Druid 后台拒绝谁访问
    //initParams.put("kuangshen", "192.168.1.20");表示禁止此ip访问

    //设置初始化参数
    bean.setInitParameters(initParams);
    return bean;
}
```

配置完毕后，我们可以选择访问 ：[http://localhost:8080/druid/login.html](http://localhost:8080/druid/login.html)

![image-20200727233409312](https://gitee.com/lzh_gitee/springboot_image/raw/master/img/image-20200727233409312.png)

进入之后

![image-20200727233436583](https://gitee.com/lzh_gitee/springboot_image/raw/master/img/image-20200727233436583.png)

**配置 Druid web 监控 filter 过滤器**

```java
//配置 Druid 监控 之  web 监控的 filter
//WebStatFilter：用于配置Web和Druid数据源之间的管理关联监控统计
@Bean
public FilterRegistrationBean webStatFilter() {
    FilterRegistrationBean bean = new FilterRegistrationBean();
    bean.setFilter(new WebStatFilter());

    //exclusions：设置哪些请求进行过滤排除掉，从而不进行统计
    Map<String, String> initParams = new HashMap<>();
    initParams.put("exclusions", "*.js,*.css,/druid/*,/jdbc/*");
    bean.setInitParameters(initParams);

    //"/*" 表示过滤所有请求
    bean.setUrlPatterns(Arrays.asList("/*"));
    return bean;
}
```
