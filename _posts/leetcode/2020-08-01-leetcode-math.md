---
layout:     post
title:      "Math"
date:       2020-08-13
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---
### [43. 字符串相乘](https://leetcode-cn.com/problems/multiply-strings/)

```
给定两个以字符串形式表示的非负整数 num1 和 num2，返回 num1 和 num2 的乘积，它们的乘积也表示为字符串形式。

示例：
输入: num1 = "123", num2 = "456"
输出: "56088"
```

![image-43](/media/post/leetcode/leetcode-43.png#left)

<mark>思路</mark>：做加法，通过模拟"竖式乘法"的方法计算乘积<br>

1. 如果num1 和 num2 之一是0，直接返回0。
2. 如果都不是零，从右往左遍历乘数，将乘数的每一位与被乘数相乘得到对应的结果，再将每次得到的结果累加。
        num2 除了最低位以外，其他的每一位运算结果补零。

<script src="https://gist.github.com/iiwowks/1a2f5010644cb2cc37e277f15e50b97a.js"></script>