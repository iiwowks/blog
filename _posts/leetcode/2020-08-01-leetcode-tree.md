---
layout:     post
title:      "Tree"
date:       2020-08-18
category:   Leetcode
author:     iiwowks
published:  true
syntaxhighlight: false
photoswipe: true
latex:      true
---

### [617. 合并二叉树](https://leetcode-cn.com/problems/merge-two-binary-trees/)

```
给定两个二叉树，想象当你将它们中的一个覆盖到另一个上时，两个二叉树的一些节点便会重叠。
你需要将他们合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则不为 NULL 的节点将直接作为新二叉树的节点。
输入:
	Tree 1                     Tree 2
          1                         2
         / \                       / \
        3   2                     1   3
       /                           \   \
      5                             4   7
输出:
合并后的树:
	     3
	    / \
	   4   5
	  / \   \
	 5   4   7
```

<mark>解题思路：</mark>

* 方法一：递归，对两棵树同时进行前序遍历，将对应的节点进行合并。
  * 如果两棵树当前节点都不为空：值相加，左右孩子递归
  * 如果有一棵树为空：返回另一棵树
  * 如果两棵树都为空：返回任意一棵树
* 方法二：迭代，将两棵树的根节点入栈，栈中每个元素存放两个根节点，处理栈顶元素。
  * 值相加
  * 如果两个节点都有左孩子，那么就将左孩子入栈；
  * 如果只有一个节点有左孩子，那么将其作为第一个节点的左孩子；
  * 如果都没有左孩子，那么不用做任何事情。
  * 对于右孩子同理。

### [108. 将有序数组转换为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

```
将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。
```

<mark style="background-color: red">二叉搜索树的中序遍历是升序序列，给定二叉搜索树的中序遍历，不可以唯一确定二叉搜索树。</mark>  
<mark>解题思路：</mark>选择中间数字作为二叉搜索树的根节点，这样分给左右子树的数字个数相同或只差1，可以使树保持平衡。可以通过递归的方式创建平衡二叉搜索树。

* 每一棵子树中的数字在数组中一定是连续的，可以通过数组下标范围确定子树包含的数字，下标范围$[left, right]$
* 对于中序遍历序列，下标范围：$left = 0$ 到 $right = nums.length - 1$，当 $left > right$时，平衡二叉搜索树为空。


```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return helper(nums, 0, nums.length - 1);
    }
    public TreeNode helper(int[] nums, int left, int right) {
        if (left > right) {
            return null;
        }
        int mid = left + (right - left) / 2; // 总是选择中间位置左边的数字作为根节点
        TreeNode root = new TreeNode(nums[mid]);
        root.left = helper(nums, left, mid - 1);
        root.right = helper(nums, mid + 1, right);
        return root;
    }
}
```

### [109. 有序链表转换二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/)

```
将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。
```
<mark>解题思路：</mark>

* 设定左闭右开的关系：可以直接用$(left, right)$和$(mid.next, right)$来表示左右子树对应的列表。
* 初始列表可以用$(head, null)$表示
* 寻找链表中的中位数：可以使用“快慢指针法”
* 用中位数作为当前根节点的元素，并递归构造左右子树

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

<mark>解题思路：</mark>

方法一：自顶向下的递归, 定义函数`height`用来计算二叉树中的任意一个节点p的高度：

$$
    height(p) =
    \begin{cases}
    0, & \text{p是空节点}\\
    max(height(p.left), height(p.right)) + 1, & \text{p是非空节点}
    \end{cases}
$$

```java
// 伪代码：
if (abs(height(root.left) - height(root.right)) <= 1 && root.left 也是平衡二叉树 && root.right 也是平衡二叉树){
    return true;
} else {
    return false;
}
```

<script src="https://gist.github.com/iiwowks/5f64e218fe2e72bb46cef5066e26660b.js"></script>