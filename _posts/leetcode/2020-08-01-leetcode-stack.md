---
layout:     post
title:      "Stack"
date:       2020-08-27
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---

### [232. 用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

```
使用栈实现队列的下列操作：

* push(x) -- 将一个元素放入队列的尾部
* pop() -- 从队列首部移除元素
* peek() -- 返回队列首部的元素
* empty() -- 返回队列是否为空
```

<mark>方法一：使用两个栈 入队 - O(n)， 出队 - O(1)</mark>

![image-232](/media/post/leetcode/leetcode-232.png)

```java
class MyQueue {

    private Stack<Integer> s1;
    private Stack<Integer> s2;
    private int front;

    /** Initialize your data structure here. */
    public MyQueue() {
        s1 = new Stack<>();
        s2 = new Stack<>();
    }

    /** Push element x to the back of queue. */
    public void push(int x) {
        if (s1.empty()) { // 若栈1为空，此时front = x;
            front = x;
        }
        while (!s1.isEmpty()) { // 若栈1非空，将所有元素移动到栈2
            s2.push(s1.pop());
        }
        s2.push(x); // 将新元素入栈
        while (!s2.isEmpty()) { // 将栈2所有元素移动到栈1
            s1.push(s2.pop());
        }

    }

    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        int res = s1.pop();
        if (!s1.isEmpty()) {
            front = s1.peek();
        }
        return res;
    }

    /** Get the front element. */
    public int peek() {
        return front;
    }

    /** Returns whether the queue is empty. */
    public boolean empty() {
        return s1.isEmpty();
    }
}
```

### [84. 柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)

```
给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1。
求在该柱状图中，能够勾勒出来的矩形的最大面积。
```

![image-84](/media/post/leetcode/leetcode-84.png#left)

<mark>方法一：暴力</mark>依次遍历柱形的高度，对每一个高度向两边扩散，求出当前高度为矩形的最大宽度
