---
layout:     post
title:      "Recursion"
date:       2020-08-22
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---

### [679. 24 点游戏](https://leetcode-cn.com/problems/24-game/)

```
你有 4 张写有 1 到 9 数字的牌。你需要判断是否能通过 *，/，+，-，(，) 的运算得到 24。
```

<mark>解题思路：</mark> 使用递归遍历所有不同的可能性，使用一个列表存储当前所有的数字，每次从列表中选出2个数字，再选择1种运算操作，用计算的结果代替选出的2个数字。重复这个步骤，直到列表中只剩一个数字。


### [93. 复原IP地址](https://leetcode-cn.com/problems/restore-ip-addresses/)

```
给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。
有效的 IP 地址正好由四个整数（每个整数位于 0 到 255 之间组成），整数之间用 '.' 分隔。
```

![image-93](/media/post/leetcode/leetcode-93.png)