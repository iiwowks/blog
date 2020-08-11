---
layout:     post
title:      "Vue介绍"
date:       2020-08-11
category:   Vue
author:     iiwowks
published:  true
photoswipe: true
---

### `输入vue+tab键`: 模板快速生成

## 环境搭建

* 浏览器：`chrome`
* IDE: `Visual Studio Code`
* `Node.js 8.9+, npm`

```
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

一个实例中的data对象中的所有property加入到vue响应式系统中。



## 组件的组成-属性

![属性](/media/post/vue-shuxin.png)

## 组建的组成-事件

![事件](/media/post/vue-shijian.png)

## 插槽

![插槽](/media/post/vue-chacao.png)
