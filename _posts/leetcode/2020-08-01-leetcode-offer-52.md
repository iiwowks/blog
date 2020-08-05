---
layout:    post
title:     "剑指 Offer 52. 两个链表的第一个公共节点"
date:       2020-08-05
category:  Leetcode
author:    iiwowks
published: true
photoswipe: true
syntaxhighlight: false
---

### [剑指 Offer 52. 两个链表的第一个公共节点](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/)

<mark>链表</mark> <mark>双指针</mark>

![image](/media/post/leetcode-offer-52.png)

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    // 第一个公共结点
        ListNode h1 = headA, h2 = headB;
        while (h1 != h2){
            h1 = h1 == null ? headB : h1.next;
            h2 = h2 == null ? headA : h2.next;
        }
    return h1;
    }
}
```