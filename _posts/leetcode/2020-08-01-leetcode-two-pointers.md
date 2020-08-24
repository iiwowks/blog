---
layout:     post
title:      "Two Pointers"
date:       2020-08-24
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: true
---


### [28. 实现 strStr()](https://leetcode-cn.com/problems/implement-strstr/)

```
实现 strStr() 函数。
给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。
如果不存在，则返回  -1。
```

<mark>方法一：子串逐一比较-线性时间复杂度</mark>

![image-28](/media/post/leetcode/leetcode-28.png)

```java
class Solution {
    public int strStr(String haystack, String needle) {
        int L = needle.length(), n = haystack.length();

        for (int start = 0; start < n - L + 1; ++start) {
            if (haystack.substring(start, start + L).equals(needle)) {
                return start;
            }
        }
        return -1;
    }
}
```

<mark>方法二：双指针-线性时间复杂度</mark>

发现一位不匹配时，开始回溯：
- **`pn`指针移动到`pn = pn - curr_len + 1`的位置**
- **`pl = 0`、`curr_len = 0`**


![image-28](/media/post/leetcode/leetcode-28-backtrack2.png)