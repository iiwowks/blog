---
layout:     post
title:      "Breath First Search"
date:       2020-08-20
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---

### [529. 扫雷游戏](https://leetcode-cn.com/problems/minesweeper/)


### [133. 克隆图](https://leetcode-cn.com/problems/clone-graph/hints/)

```
给你无向连通图中一个节点的引用，请你返回该图的深拷贝（克隆）
图中的每个节点都包含它的值 val（int） 和其邻居的列表（list[Node]）

class Node {
    public int val;
    public List<Node> neighbors;
}
```

<mark>解题思路：广度优先遍历</mark>

![image-133](/media/post/leetcode/leetcode-133.png#left)

使用一个哈希表 `visited` 存储所有已被访问和克隆的节点。哈希表中的 `key` 是原始图中的节点，`value` 是克隆图中的对应节点。
* 将题目给定的节点添加到队列。克隆该节点并存储到哈希表中。
* 每次从队列首部取出一个节点，遍历该节点的所有邻接点。如果某个邻接点已被访问，则该邻接点一定在 `visited` 中，那么从 `visited` 获得该邻接点，否则创建一个新的节点存储在 `visited` 中，并将邻接点添加到队列。将克隆的邻接点添加到克隆图对应节点的邻接表中。重复上述操作直到队列为空，则整个图遍历结束。
