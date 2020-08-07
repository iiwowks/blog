---
layout:     post
title:      "Data Structures"
date:       2020-08-02
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---


## 跳表（Skip List）

### 给链表加速

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