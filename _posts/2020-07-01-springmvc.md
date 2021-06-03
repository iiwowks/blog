---
layout: post
title: "spring mvc learn"
date: 2020-07-01
category: Backend
author: zhengjunan
published: true
photoswipe: true
syntaxhighlight: true
---

# Spring MVC

什么是 mvc, 模型（Model）视图（View）控制器（Controller）

是将业务逻辑，数据，显示分离的方法来组织代码

mvc 主要作用是降低了视图与业务逻辑间的双向耦合

mvc 不是一种设计模式，mvc 是一种架构模式

Model：数据模型，提供要展示的数据，包含数据和行为。Value Object（数据 Dao）和服务层（行为 Service）。模型提供模型数据查询和模型数据的状态更新等功能，包括数据和业务。

View：视图，负责进行模型的展示，就是我们见到的用户界面

Cotroller：控制器，接受用户请求，委托给模型进行处理（状态改变），处理完毕后把返回的模型数据返回给视图，由视图负责展示

Model： 模型

1. 业务逻辑
2. 保存数据的状态

View：视图

1. 显示页面

Controller：控制器

1. 取得表单数据
2. 调用业务逻辑
3. 转向指定的页面

MVC 框架做的事情：

1. 将 URL 映射到 Java 类或 Java 类的方法上
2. 封装用户提交的数据
3. 处理请求-调用相关的业务处理-封装响应数据
4. 将响应的数据进行渲染

## SpringMVC 的优点：

1. 轻量级
2. 高效，基于请求响应的 MVC 框架
3. 与 Spring 兼容性好，无缝结合
4. 约定优于配置
5. 功能强大： RESTFul，数据验证，格式化，本地化，主题
6. 简约灵活

## MVC 一次请求的全过程

1. 用户发起请求
2. 中央控制器 dispatcherServlet
3. dispatcherServlet 调用处理器映射器 handlerMapping
4. handlerMapping 找到对应处理器，并返回对应的处理器对象 handler 给中央控制器
5. dispatcherServlet 将 handler 给 handlerAdapter 处理器适配器
6. handlerAdapter 调用 handler 处理器（controller）
7. controller 调用业务层
8. 业务层调用 dao 层
9. dao 层调用 jdbc 或 Mybatis 对数据库操作返回给业务层
10. controller 得到业务层返回的数据，返回 modelandview
11. dispatcherServlet 调用视图解析器 ViewResolve 解析 modelandview
12. ViewResolve 返回 view
13. dispatcherServlet 将 view 给 jsp 进行渲染呈现给用户

## 控制器 Controller：

1. 实现方式： 接口定义，或注解定义

2. 控制器负责解析用户的请求并将其转换为一个模型

3. 在 springmvc 中一个 controller 类可以包含多个方法

4. 在 springmvc 中对于 controller 的配置方式有很多种方式：

   1. 方式一：实现 Controller 接口

   ```java
   public interface Controller {
       @Nullable
       ModelAndView handleRequest(HttpServletRequest var1, HttpServletResponse var2) throws Exception;
   }
   ```

   2. 方式二： 使用注解@Controller

      1. @Controller 注解类型用于声明 Spring 类的实例是一个控制器
      2. Spring 可以使用扫描机制来找到应用程序中所有基于注解的控制器类，为了保证 Spring 能够找到自己的控制器，需要在配置文件中声明组件扫描

      ```xml
      <context:component-scan base-package="cn.zhengjunan.controller"/>
      ```

   3. `@Component @Service @Controller @Repository` 这四个注解等效, 组件、服务层、控制器层、dao 层

## RestFul 风格

RestFul 就是一种资源定位及资源操作的风格，不是标准也不是协议，只是一种风格。

功能：

1. 资源：所有事物都可以抽象成资源
2. 资源操作：使用 POST、DELETE、PUT、GET，使用不同的方法对资源进行操作
3. 分别对应 添加、删除、修改、查询

## ModelAndView

设置 ModelAndView 对象，根据 view 的名称，和视图解析器跳转到指定的页面

页面：视图解析器前缀 + viewName + 视图解析器后缀

```xml
	<!-- 视图解析器： 模版引擎： thymleaf -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="internalResourceViewResolver">
        <!-- 前缀 -->
        <property name="prefix" value="WEB-INF/jsp/"/>
        <!-- 后缀 -->
        <property name="suffix" value=".jsp"/>
    </bean>
```

## 重定向和转发

```java
rep.sendRedirect("/index.jsp");
//
req.getRequestDispatcher("/WEB-INF/jsp/test.jsp").forward(req, rep);
```

使用 Spring MVC 来实现转发和重定向，有视图解析器：

```java
	@RequestMapping("/rem/t1")
    public String test1() {
        //转发
        return "test";
    }

    @RequestMapping("/rem/t3")
    public String test3() {
        // 重定向
        return "redirect:/index.jsp";
    }
```

## 数据处理

处理提交数据：

1. 提交的域名名称和处理方法的参数名一致

   ```
   localhost:8080/hello?name=zhengjunan

   处理方法：
   @RequestMapping("/hello")
   public String hello(String name) {
   	System.out.println(name);
   	return "hello";
   }
   ```

2. 提交的域名名称和处理方法的参数名不一致

   ```
   localhost:8080/hello?name=zhengjunan

   @RequestMapping("/hello")
   public String hello(@RequestParam("username") String name) {
   	return "hello";
   }
   ```

3. 提交的是一个**对象**，参数会和对象内的字段进行匹配，前端传递的参数名必须和对象字段名一致，否则为 null

## 数据显示到前端

ModelAndView

ModelMap

Model

## Controlle 返回 JSON 数据

- Jackson

- **FastJson**

  - 主要的三个对象：
  - JSONObject：代表 json 对象
  - JSONArray：代表 json 对象数组
  - JSON

  ```java
  // java对象转JSON字符串
  JSON.toJSONString(user);
  // json字符串转java对象
  JSON.parseObject(str, User.class);
  // java对象转json对象
  JSONObject jsonObject = (JSONObject) JSON.toJSON(user2);
  // json对象转java对象
  User user = JSON.toJavaObject(jsonObject, User.class);
  ```
