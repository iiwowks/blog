---
layout:     post
title:      "jQuery学习"
date:       2020-08-03
category:   Others
author:     iiwowks
published:  true
syntaxhighlight: true
---

### 选择器

jquery是一个轻量级js库，核心是**选择器**，用于获取页面元素

* 语法：
  * `jQuery(选择器表达式)`
  * `$(选择器表达式)`
* **基本选择器：**
  * `$("#id")`    - ID选择器，指定id元素的对象
  * `$("标签")`   - 元素选择器，选择指定标签名的选择器
  * `$(".class")` - 类选择器，选中拥有指定css类的元素
  * `$("S1,S2,SN")` - 组合选择器，对元素进行组合
* **层叠选择器：** 根据元素的位置关系来获取元素的选择器表达式
  * `$("ancestor descendant")`    - 后代选择器
  * `$("ancestor>descendant")`    - 子选择器
  * `$("prev~siblings")`          - 兄弟选择器：prev之后的同级元素
* **属性选择器**：根据元素的属性值来选择元素的选择器表达式
  * `$("selector[attribute=value]")` - 选中属性值等于具体值的的组件
  * `$("selector[attribute^=value]")` - 选中属性值以某值开头的组件
  * `$("selector[attribute$=value]")` - 选中属性值以某值结尾的组件
  * `$("selector[attribute*=value]")` - 选中属性包含某值的组件
* **位置选择器：** 根据位置获取指定的元素
  * `$("selector:first")` - 获取第一个元素
  * `$("selector:last")` - 获取最后一个元素
  * `$("selector:even")` - 获取偶数位置的元素(从0开始)
  * `$("selector:odd")` - 获取奇数位置的元素(从0开始)
  * `$("selector:eq(n)")` - 获取指定位置的元素(从0开始)
* **表单选择器：** 获取表单元素
  * `$("selector:input")` - 所有输入元素
  * `$("selector:text")` - 获取文本框
  * `$("selector:password")` - 获取密码框
  * `$("selector:submit")` - 获取提交按钮
  * `$("selector:reset")` - 获取重置按钮

### 操作元素属性

```html
<script type="text/javascript" src="js/jquery-3.4.1.js"></script>
<script type="text/javascript">
//获取属性值
var href_attr = $("a[href*='163']").attr("href");
alert(href_attr);
//更改属性值
$("a[href*='163']").attr("href", "http://www.github.com/iiwowks/");
//获取默认第一个a标签的href
var attr = $("a").attr("href");
alert(attr);
//移除属性
$("a").removeAttr("href");
</script>
```

* `attr(name|properties|key)` - 获取或设置元素属性
* `removeAttr(name)` - 移除元素属性

### 操作元素的css样式

```html
<style>
    .myclass {
        font-style: italic;
        color: darkblue;
    }
    /* 高亮css类 */
    .highlight {
        color: red;
        font-size: 30px;
        background: lightblue;
    }
</style>
<script type="text/javascript" src="../js/jquery-3.4.1.js"></script>
<script type="text/javascript">
    //获取css类 默认第一个a的color属性
    var color = $("a").css("color");
    alert(color);
    //设置css类属性 传入一个json对象
    $("a").css({"color": "red", "front-weight": "bold", "font-style": "italic"});
    $("a").css("color", "red");
    alert(color);
    //增加css类
    $("li").addClass("highlight myclass");
    //移除指定的所有css类
    $("p").removeClass("myclass");
</script>
```

* `css()` - 获取或设置匹配元素的样式属性
* `addClass()` - 为每个匹配的元素添加指定的类名
* `removeClass()` - 从所有匹配的元素中删除全部或者指定的类

### 设置元素内容

```html
<script type="text/javascript" src="../js/jquery-3.4.1.js"></script>
<script type="text/javascript">
    //获取、设置输入项表单内容
    $("input[name = 'uname']").val("administrator");
    //获取元素值
    var uname = $("input[name = 'uname']").val();
    alert(uname);
    //获取、设置元素纯文本 text() 会转义标签
    $("span.myclass").text("<b> github————— gayhub </b>");
    //html()不会做转义
    //$("span.myclass").html("<b> github————— gayhub </b>");
    var str = $("sapn.myclass").html();
    //屏蔽标签，直接输出文本
    var str = $("sapn.myclass").text();
    alert(str);
</script>
```

* `val()` - 获取或设置**输入项**的值
* `text()` - 获取或设置元素的**纯文本**
* `html()` - 获取或设置元素内部的**HTML**

### 事件处理

```html
<script type="text/javascript" src="../js/jquery-3.4.1.js"></script>
<script type="text/javascript">
    //点击事件
    $("p.myclass").on("click", function(){
       // $(this)是指当前事件产生的对象
        $(this).css("background-color", "yellow");
    });
    //
    $("span.myclass").click(function(){
        $(this).css("background-color", "lightgreen");
    });
    //键盘事件
    $("input[name = 'uname']").keypress(function(event){
        //可以在浏览器中查看具体的event内容
        console.log(event);
        if( event.keyCode == 32){
            $(this).css("color", "red");
        }
    });
</script>
```

* `on("click", function)` - 为选中的页面元素绑定单击事件
* `click(function)` - 是绑定事件的简写形式

**常用事件：**

![image0](https://i.loli.net/2020/04/11/FpzhtkPKAsTL8Yr.png)

### 页面就绪函数

* ☞在页面加载完成后执行的函数
* 语法1：`$(document).ready(function)`
* 语法2：`$(function)`