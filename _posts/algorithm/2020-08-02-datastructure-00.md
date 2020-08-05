---
layout:     post
title:      "常见数据结构定义"
date:       2020-08-02
category:   Algorithm
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---

## 二叉树节点定义

```java
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode() {}
    TreeNode(int val) {
        this.val = val;
    }
    TreeNode(int val, TreeNode left, TreeNode right){
        this.val  = val;
        this.left  = left;
        this.right  = right;
    }
}
```