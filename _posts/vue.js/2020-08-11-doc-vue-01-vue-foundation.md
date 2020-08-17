---
layout:     post
title:      "Vue基础"
date:       2020-08-14
category:   Vue
author:     iiwowks
published:  false
photoswipe: true
syntaxhighlight: false
---

## 介绍

### `输入vue+tab键`: 模板快速生成

### 环境搭建

* 浏览器：`chrome`
* IDE: `Visual Studio Code`
* `Node.js 8.9+, npm`

```bash
命令行工具cli安装：
npm install -g @vue/cli
# OR
yarn global add @vue/cli\

//创建一个项目：
vue create my-project
# OR
vue ui
// 本地运行
npm run serve
```

### 直接用`<script>`引入

```
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.11"></script>
```

### 组件化应用构造

组件系统是 Vue 的另一个重要概念，因为它是一种抽象，允许我们使用小型、独立和通常可复用的组件构建大型应用。仔细想想，几乎任意类型的应用界面都可以抽象为一个组件树：

![](https://cn.vuejs.org/images/components.png)

### 创建一个vue实例

```js
var vm = new Vue({
    // 选项
})
```

创建一个vue实例后，传入一个选项对象，利用选项创建想要的行为。  
一个vue应用通过一个`new Vue`创建**根Vue实例**, 以及可选的嵌套的、可复用的组件树组成。

```js
// todo应用组件树
根实例
└─ TodoList
   ├─ TodoItem
   │  ├─ DeleteTodoButton
   │  └─ EditTodoButton
   └─ TodoListFooter
      ├─ ClearTodosButton
      └─ TodoListStatistic
```

### 数据和方法

一个实例中的`data`对象中的所有property加入到vue响应式系统中。property变化时，视图会产生响应。

* `data`对象

```js
data: {
    newTodoText: '',
    visitCount: 0,
    todos: []
}
```

* `Object.freeze()`:会阻止修改现有的property

```js
var obj = {
  foo: 'bar'
}

Object.freeze(obj)

new Vue({
  el: '#app',
  data: obj
})
```

* 实例property和方法,使用前缀`$`可以与用户定义的property区分开

### 实例生命周期钩子

* `created`钩子: 用来在一个实例被创建之后执行代码
* `mounted`
* `updated`
* `destroyed`

```js
new Vue({
    data: {
        a: 1
    },
    created: function() {
        // this 指向vm实例
        console.log('a is: ' + this.a)   // => "a is: 1"
    }
})
```

![生命周期图示](https://cn.vuejs.org/images/lifecycle.png)

