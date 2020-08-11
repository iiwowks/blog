---
layout:    post
title:     "Depth First Search"
date:       2020-08-11
category:  Leetcode
author:    iiwowks
published: true
photoswipe: true
syntaxhighlight: true
---

### [130. 被围绕的区域](https://leetcode-cn.com/problems/surrounded-regions/)

```
给定一个二维的矩阵，包含 'X' 和 'O'（字母 O）。
找到所有被 'X' 围绕的区域，并将这些区域里所有的 'O' 用 'X' 填充。

示例:
X X X X
X O O X
X X O X
X O X X
运行你的函数后，矩阵变为：
X X X X
X X X X
X X X X
X O X X
```

![image-130](/media/post/leetcode/leetcode-130.png#right)

注意到题目解释中提到：**任何边界上的O都不会被填充为X**。 我们可以想到，所有的不被包围的 `O` 都直接或间接与边界上的 `O` 相连。我们可以利用这个性质判断 `O` 是否在边界上，具体地说：

* 对于每一个边界上的 `O`，我们以它为起点，标记所有与它直接或间接相连的字母 `O`；
* 最后我们遍历这个矩阵，对于每一个字母：
  * 如果该字母被标记过，则该字母为没有被字母 `X` 包围的字母 `O`，我们将其还原为字母 `O`；
  * 如果该字母没有被标记过，则该字母为被字母 `X` 包围的字母 `O`，我们将其修改为字母 `X`。

