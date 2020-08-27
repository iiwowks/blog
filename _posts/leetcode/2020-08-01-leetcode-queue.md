---
layout:     post
title:      "Queue"
date:       2020-08-27
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---

### [225. 用队列实现栈](https://leetcode-cn.com/problems/implement-stack-using-queues/)

```
使用队列实现栈的下列操作：

* push(x) -- 元素 x 入栈
* pop() -- 移除栈顶元素
* top() -- 获取栈顶元素
* empty() -- 返回栈是否为空
```

<mark>方法二：两个队列， 压入 - O(n)， 弹出 - O(1)</mark>

![image-225](/media/post/leetcode/leetcode-225.png)

```java
class MyStack {
    private Queue<Integer> q1;
    private Queue<Integer> q2;
    private int top;

    /** Initialize your data structure here. */
    public MyStack() {
        q1 = new LinkedList<>();
        q2 = new LinkedList<>();
    }

    /** Push element x onto stack. */
    public void push(int x) {
        q2.add(x);
        top = x;
        while (!q1.isEmpty()) {
            q2.add(q1.remove());
        }
        Queue<Integer> temp = q1;
        q1 = q2;
        q2 = temp;
    }

    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        q1.remove();
        int res = top;
        if (!q1.isEmpty()) {
            top = q1.peek();
        }
        return res;
    }

    /** Get the top element. */
    public int top() {
        return top;
    }

    /** Returns whether the stack is empty. */
    public boolean empty() {
        return q1.isEmpty();
    }
}
```

<mark>方法三：一个队列， 压入 - O(n)， 弹出 - O(1)</mark>

![image-225_2](/media/post/leetcode/leetcode-225_2.png)

```java
class MyStack {
    private Queue<Integer> q1;

    /** Initialize your data structure here. */
    public MyStack() {
        q1 = new LinkedList<>();
    }

    /** Push element x onto stack. */
    public void push(int x) {
        q1.add(x);
        int sz = q1.size();
        while (sz > 1) {
            q1.add(q1.remove());
            sz--;
        }
    }

    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        return q1.remove();
    }

    /** Get the top element. */
    public int top() {
        return q1.peek();
    }

    /** Returns whether the stack is empty. */
    public boolean empty() {
        return q1.isEmpty();
    }
}
```