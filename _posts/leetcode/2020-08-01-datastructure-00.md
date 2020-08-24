---
layout:     post
title:      "Data Structures"
date:       2020-08-24
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: true
---


## BST二叉搜索树

```java
class BSTree {
    TreeNode root = null;

    // 查找二叉搜索树
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null || val == root.val) {
            return root;
        }
        return val < root.val ? searchBST(root.left, val) : searchBST(root.right, val);
    }
    // 插入二叉搜索树
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        if (val > root.val) {
            root.right = insertIntoBST(root.right, val); // 插入右节点
        }
        else if (val == root.val) {
            return root; // 值相同时，跳过这次插入
        }
        else {
            root.left = insertIntoBST(root.left, val); // 插入左节点
        }
        return root;
    }

    // 一步右，然后到最左下端
    public int successor(TreeNode root) {
        root = root.right;
        while (root.left != null) {
            root = root.left;
        }
        return root.val;
    }
    // 一步左，然后到最右下端
    public int predecessor(TreeNode root) {
        root = root.left;
        while (root.right != null) {
            root = root.right;
        }
        return root.val;
    }

    // 删除搜索二叉树节点
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) {
            return null;
        }
        // 从右子树中删除
        if (key > root.val) {
            root.right = deleteNode(root.right, key);
        }
        // 从左子树中删除
        else if (key < root.val) {
            root.left = deleteNode(root.left, key);
        }
        // key == root.val的时候
        else {
            // 叶节点
            if (root.left == null && root.right == null){
                root = null;
            }
            // 非叶节点，并有右孩子
            else if (root.right != null) {
                root.val = successor(root); // 右子树中最左下端节点值，作为
                root.right = deleteNode(root.right, root.val); // 从右子树中删除
            }
            else {
                root.val = predecessor(root);
                root.left = deleteNode(root.left, root.val);
            }
        }
        return root;
    }
}
```

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

## 深、广度优先搜索常用代码片段

```java
// 用于上下左右遍历的增量dx, dy
int[] dx = {1, -1, 0, 0};
int[] dy = {0, 0, 1, -1};
```

## 跳表（Skip List）

给链表加速

* 升维
* 用时间换空间

<figure>
    <img src="/media/post/algorithm-lianbiao-yijisuoyin.png">
    <figcaption> 一级索引 </figcaption>
</figure>

<figure>
    <img src="/media/post/algorithm-lianbiao-duojisuoying.png">
    <figcaption> 多级索引 </figcaption>
</figure>

* 时间复杂度：n/2 n/4 n/8 第k级索引结点的个数n/2<sup>k</sup>
* 索引有h级，最高级的索引有2个结点。n/2<sup>k</sup> = 2, 得到 <mark>h = log<sub>2</sub>(n) - 1 </mark>,所以时间复杂度为log<sub>2</sub>(n)

<figure>
    <img src="/media/post/algorithm-tiaobiao.png">
    <figcaption> 跳表实际中的应用 </figcaption>
</figure>

对跳表的更改，需要更新索引，时间复杂度为log<sub>2</sub>(n)

### 参考链接

- [Java 源码分析（ArrayList）](http://developer.classpath.org/doc/java/util/ArrayList-source.html)
- [Linked List 的标准实现代码](http://www.geeksforgeeks.org/implementing-a-linked-list-in-java-using-class/)
- [Linked List 示例代码](http://www.cs.cmu.edu/~adamchik/15-121/lectures/Linked Lists/code/LinkedList.java)
- [Java 源码分析（LinkedList）](http://developer.classpath.org/doc/java/util/LinkedList-source.html)
- LRU Cache - Linked list：[ LRU 缓存机制](http://leetcode-cn.com/problems/lru-cache)
- Redis - `Skip List`：[跳跃表](http://redisbook.readthedocs.io/en/latest/internal-datastruct/skiplist.html)、[为啥 Redis使用跳表（Skip List）而不是使用Red-Black？](http://www.zhihu.com/question/20202931)
