---
layout:     post
title:      "bit-manipulation"
date:       2020-08-23
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---

### [201. 数字范围按位与](https://leetcode-cn.com/problems/bitwise-and-of-numbers-range/)

```
给定范围 [m, n]，其中 0 <= m <= n <= 2147483647，返回此范围内所有数字的按位与（包含 m, n 两端点）。
```

<!-- ![leetcode-201](/media/post/leetcode/leetcode-201.png) -->

![leetcode-201](https://i.loli.net/2020/08/23/JpLulWkw2BtrMI7.png#right)

一定存在连续的两个数 `x` 和 `x+1`，满足 `x` 的第 `i+1` 位为 0，后面全为 1，`x+1` 的第 `i+1` 位为 1，后面全为 0，对应上图中的例子即为 11 和 12。这样按位与的结果一定是0000

<mark>结论规律：</mark> 对所有的数字执行位与运算的结果是对应二进制字符串的公共前缀再用零补上后面的剩余位。`题目变成：给定两个整数，找它们对应的二进制字符串的公共前缀。`
<mark>解题思路：</mark> 此时通过**位移**找到公共前缀

```java
class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        int shift = 0;
        // 找到公共前缀
        while (m < n) {
            m >>= 1;
            n >>= 1;
            ++shift;
        }
        return m << shift;
    }
}
```