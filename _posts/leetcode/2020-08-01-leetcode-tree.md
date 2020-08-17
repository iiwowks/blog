---
layout:     post
title:      "Tree"
date:       2020-08-17
category:   Leetcode
author:     iiwowks
published:  true
syntaxhighlight: true
---

### [110. 平衡二叉树](https://leetcode-cn.com/problems/balanced-binary-tree/)

```
给定一个二叉树，判断它是否是高度平衡的二叉树。
本题中，一棵高度平衡二叉树定义为：
一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。
示例 1:
给定二叉树 [3,9,20,null,null,15,7]  => true
    3
   / \
  9  20
    /  \
   15   7
```

<mark>解题思路</mark>:
函数

`javascript`

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return height(root) >= 0;
    }

    private int height(TreeNode root) {
        if(root == null)
            return 0;
        int lh = height(root.left), rh = height(root.right);
        if(lh >= 0 && rh >= 0 && Math.abs(lh - rh) <= 1) {
            return Math.max(lh, rh) + 1;
        } else {
            return - 1;
        }
    }
}
```
