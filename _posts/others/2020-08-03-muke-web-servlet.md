---
layout:     post
title:      "servlet学习"
date:       2020-08-03
category:   Others
author:     iiwowks
published:  true
syntaxhighlight: true
---

### servlet访问方法

* `http://IP地址:端口/context-path/url-mapping`
* context-path称为“上下文路径”，默认为工程名
* 远程访问IP地址，本地访问`localhost(127.0.0.1)`

### servlet生命周期

1. 装载-`web.xml`
2. 创建-构造函数
3. 初始化-`init()`
4. 提供服务-`service()`
5. 销毁-`destroy()`

### 注解

* `@WebServlet("/映射名")`
模糊匹配，所有前缀是`/pattern/`的都会被该servlet拦截
* `@WebSerblet("/pattern/*")`

### Servlet缺点

* 静态html与动态java代码混合在一起，难以维护
* Servlet利用out.println()输出，效率低

### get请求

* `Response Headers`响应行和响应头
* `Response`是响应体

```java
@WebServlet("/request")
public class RequestServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.getWriter().println("this is get method");
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.getWriter().println("this is post method");
    }
}
```

### Post请求

* 相关参数在请求体中

### 使用请求头开发多端应用

```java
@WebServlet("/UserAgentServlet")
public class UserAgentServlet extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String useragent = request.getHeader("User-Agent");
        response.setContentType("text/html;charset=utf-8");
        response.getWriter().println(useragent);
        String output = "";
        //useragent.indexOf("iPad");
        if(useragent.indexOf("Windows NT") != -1){
            output = "<h1> 这是pc端</h1>";
        }
        else if(useragent.indexOf("iPhone") != -1 || useragent.indexOf("Android") != -1){
            output = "<h1> 这是移动端</h1>";
        }

        response.getWriter().println(output);
    }
}
```

* `User-Agent`: 可以表示Android，iPhone，Windows用户端类型

### http常见状态码

| 状态码   | 错误描述                               |
| :------- | :------------------------------------- |
| 200      | 服务器处理成功                         |
| 404      | 无法找到文件                           |
| 500      | 内部服务器错误                         |
| 403      | 服务器拒绝访问                         |
| 301、302 | 请求重定向                             |
| 400      | 无效的请求                             |
| 401      | 未经过授权                             |
| 503      | 服务器超负载或正停机维护，无法处理请求 |

### ContentType的作用

* `ContentType`决定浏览器采用何种方式对响应体进行处理

```java
@WebServlet("/ContentTypeServlet")
public class ContentTypeServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String output = "<h1><a href='http://www.baidu.com'><span>百度</span></h1>";
        // html
        response.setContentType("text/html;charset=utf-8");
        //纯文本 response.setContentType("text/plain;charset=utf-8");
        response.getWriter().println(output);
    }
}
```

| MIME类型                                 | 描述           |
| ---------------------------------------- | -------------- |
| text/plain                               | 纯文本         |
| text/html                                | HTML文档       |
| text/xml                                 | XML文档        |
| application/x-msdownload                 | 需要下载的资源 |
| image/jpeg<br />image/gif<br />image/... | 图片资源       |

### 请求转发响应与重定向

* 多个servlet之间跳转有两种方式：
* 请求转发是**服务器跳转**，只产生一次请求
  * 请求转发语句： `request.getRequestDispatcher().forward()`
* 响应重定向是**浏览器端跳转**，会产生两次请求
  * 响应重定向语句： `response.sendRedirect()`

### 设置请求自定义属性

```java
@WebServlet("/direct/check")
public class CheckLoginServlet extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("用户登陆成功");// 在控制台中输出
        // 设置请求属性
        request.setAttribute("username", "admin");
        //实现请求转发功能
        /*
        request.getRequestDispatcher("/direct/index").forward(request,response);
        */
        //响应重定向需要增加contextPath
        response.sendRedirect("/Demo2/direct/index");
    }
}
```

```java
@WebServlet("/direct/index")
public class indexServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String username = (String)request.getAttribute("username");
        response.getWriter().println("this is index page! current username is :" + username);
    }
}
```

* 设置请求属性： `request.setAttribute(属性名,属性值)`
* 获取请求属性： `Object attr = request.getAttribute(属性名)`

### Cookie

```java
Cookie cookie = new Cookie("user" , "admin"); //设置 cookie “name" = "user" , "value" = "admin"
cookie.setMaxAge(60 * 60 * 24 * 7); //设置最大时效，单位为秒
response.addCookie(cookie); //在响应中添加cookie
```

```java
//request.getCookies()用户获取所有的Cookie
Cookie[] cs = request.getCookies();
```

* cookie是浏览器保存在本地的文本文件
* 常用于保存登陆状态、用户资料等
* 具有时效性，内容会伴随请求发送给Tomcat
* `Cookie(name, value)`
* `response.addCookie(cookie)`
* `request.getCookies()`
* `setMaxAge()`
* `getName()`
* `getValue()`

### Session

* Session(用户会话)用于保存与“浏览器窗口”对应的数据
* Session的数据存储在Tomcat服务器的内存中，具有时效性
* Session通过浏览器Cookie的SessionID值提取用户数据
* `request.getSession()` - 获取Session对象
* `get|set|removeAttribute()` - 获取/设置/删除Session属性
* `setMaxInactiveInterval` - 设置Session超时时间

实现原理：

![image](https://i.loli.net/2020/04/11/oxVqgTdItZb6p2a.png)

### ServletContext

* ServletContext(Servlet上下文对象),是Web应用全局对象
* 一个Web应用只会创建一个ServletContext对象
* ServletContext**随着Web应用启动而自动创建**

### Java web三大作用域对象

* `HttpServletRequest` - 请求对象
* `HttpSession` - 用户会话对象
* `ServletContext` - web应用全局对象

### web应用中文乱码

* Tomcat默认使用ISO-8859-1字符集
* Servlet中请求和响应都需要设置UTF-8字符集
* 在请求中：
  * 在`doPost()`方法中用`request.setCharacterEncoding("UTF-8")`将请求体中的字符集转换为UTF-8格式
  * 在`doGet()`方法中，tomcat8.x中get请求发送中文就是utf-8格式，无需转换
* 在响应中：
  * 指定以什么方式显示文本`response.setContentType("text/html;charset = utf-8")`

### web.xml常用配置

* 修改web应用默认首页
* Servlet通配符映射及初始化参数
* 设置404、500等状态码默认页面

### jsp内置对象

![批注 2020-04-04 160747](https://i.loli.net/2020/04/17/xSbJHjuy8OtpY9o.png)

### tomcat常用配置

* 修改web应用端口号
* 修改ContextPath上下文路径
* 设置应用自动重载

### java web打包、发布

* 采用war包进行发布
* 发布路径：`{TOMCAT_HOME}/webapps`

### [参考servlet教程](https://www.w3cschool.cn/servlet/)