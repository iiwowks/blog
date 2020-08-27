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

```java
// @lc code=start
// 思路：做加法，通过模拟"竖式乘法"的方法计算乘积
// 步骤：
//      1. 如果num1 和 num2 之一是0，直接返回0。
//      2. 如果都不是零，从右往左遍历乘数，将乘数的每一位与被乘数相乘得到对应的结果，再将每次得到的结果累加。
//         num2 除了最低位以外，其他的每一位运算结果补零。
class Solution {
    public String multiply(String num1, String num2) {
        if (num1.equals("0") || num2.equals("0")) {
            return "0";
        }
        String ans = "0";
        int m = num1.length(), n = num2.length();
        // num2从右往左各个位
        for (int i = n - 1; i >= 0; i--) {
            // curr 是单组相乘结果的 反转
            StringBuffer curr = new StringBuffer();
            // add 是进位
            int add = 0;
            // 最右位补零
            for (int j = n - 1; j > i; j--) {
                curr.append(0);
            }
            int y = num2.charAt(i) - '0';
            // num2的一位依次与num1各个位相乘
            for (int j = m - 1; j >= 0; j--) {
                int x = num1.charAt(j) - '0';
                int product = x * y +add;
                curr.append(product % 10); // 添余数
                add = product / 10; // 进位
            }
            // 如果最左边有进位，curr加入最后的进位
            if (add != 0) {
                curr.append(add % 10);
            }
            // 加入单组结果，curr.reverse().toString 反转变字符串
            ans = addStrings(ans, curr.reverse().toString());
        }
        return ans;
    }
    // 将两组字符串相加求和
    public String addStrings(String num1, String num2) {
        int i = num1.length() - 1, j = num2.length() - 1, add = 0;
        StringBuffer ans = new StringBuffer();
        while (i >= 0 || j >= 0 || add != 0) {
            int x = i >= 0 ? num1.charAt(i) - '0' : 0;
            int y = j >= 0 ? num2.charAt(j) - '0' : 0;
            int result = x + y + add;
            ans.append(result % 10);
            add = result / 10;
            i--;
            j--;
        }
        return ans.reverse().toString();
    }
}
// @lc code=end
```