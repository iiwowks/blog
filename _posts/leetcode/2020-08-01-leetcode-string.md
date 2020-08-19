---
layout:     post
title:      "String"
date:       2020-08-19
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
latex:      true
---

### [647. 回文子串](https://leetcode-cn.com/problems/palindromic-substrings/)

```
给定一个字符串，你的任务是计算这个字符串中有多少个回文子串。
具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被视作不同的子串。
```

<mark>解题思路：</mark> 计算所有回文子串：可以枚举出所有的回文子串  
* 方法一：枚举所有子串，再判断是不是回文串
* 方法二：枚举所有回文中心，使用两个指针向两边拓展
  * 回文串长度是奇数
  * 回文串长度是偶数
* <mark>长度为$n$的字符串会生成 $2n - 1$组回文中心$[l_i, r_i]$, $l_i =\lfloor \frac{i}{2} \rfloor$, $r_i = l_i + (i\pmod 2)$</mark>
* 只要从 $0$ 到 $2n − 2$ 遍历 $i$，就可以得到所有可能的回文中心，这样就把奇数长度和偶数长度两种情况统一起来了


### [696. 计数二进制子串](https://leetcode-cn.com/problems/count-binary-substrings/)

![image-696](/media/post/leetcode/leetcode-696.png)