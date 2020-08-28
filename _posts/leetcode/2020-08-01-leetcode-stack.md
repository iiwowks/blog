---
layout:     post
title:      "Stack"
date:       2020-08-28
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---

### [496. 下一个更大元素 I](https://leetcode-cn.com/problems/next-greater-element-i/)

```
给定两个数组，nums1 是 nums2 的子集，
找到 nums1 中每一个元素在 nums2 中对应的位置右边第一个比其值大的元素，不存在输出-1
```

<mark>方法一：单调栈</mark>维护一个单调栈，栈中元素从底到顶单调递增，通过Stack、HashMap解决

* 先遍历大数组`nums2`，首先将第一个元素入栈；
* 继续遍历，当当前元素小于栈顶元素时，继续将它入栈；当当前元素大于栈顶元素时，栈顶元素出栈，此时应将该出栈的元素与当前元素形成`key-value`键值对，存入`HashMap`中；
* 当遍历完`nums2`后，得到`nums2`中元素所对应的下一个更大元素的hash表；
* 遍历`nums1`的元素在`hashMap`中去查找‘下一个更大元素’，当找不到时则为-1。

![image-496](/media/post/leetcode/leetcode-496.png)

```java
public class Solution {
    public int[] nextGreaterElement(int[] findNums, int[] nums) {
        Stack <Integer> stack = new Stack <> ();
        HashMap <Integer, Integer> map = new HashMap <> ();
        int[] res = new int[findNums.length];
        for (int i = 0; i < nums.length; i++) {
            while (!stack.empty() && nums[i] > stack.peek())
                map.put(stack.pop(), nums[i]);
            stack.push(nums[i]);
        }
        while (!stack.empty())
            map.put(stack.pop(), -1);
        for (int i = 0; i < findNums.length; i++) {
            res[i] = map.get(findNums[i]);
        }
        return res;
    }
}
```


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
        if (s1.isEmpty()) { // 若栈1为空，此时front = x;
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
            front = s1.peek(); // 更新front
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
