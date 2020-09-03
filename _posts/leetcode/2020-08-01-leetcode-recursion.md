---
layout:     post
title:      "Recursion"
date:       2020-09-03
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---

### [51. N 皇后](https://leetcode-cn.com/problems/n-queens/)

1. 设置*行状态、主对角线状态、副对角线状态布尔数组变量***记住拜访的皇后位置**
2. **主、副对角线**上面的元素特点：**横坐标 - 纵坐标** 的值固定
3. 发生冲突时：尝试摆放**同一行的下一个位置**，直至行尾，否则**退回上一行**
4. 深度优先遍历

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

### [491. 递增子序列](https://leetcode-cn.com/problems/increasing-subsequences/)

```
给定一个整型数组, 你的任务是找到所有该数组的递增子序列，递增子序列的长度至少是2。
```

<mark>方法二：递归枚举+ 减枝</mark>

<script src="https://gist.github.com/iiwowks/21fedbf5226880a18714eb54fec5e222.js"></script>