---
layout:     post
title:      "Map"
date:       2020-08-27
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---

### [332. 重新安排行程](https://leetcode-cn.com/problems/reconstruct-itinerary/)

```
化简本题题意：给定一个 n 个点 m 条边的图，要求从指定的顶点出发
经过所有的边恰好一次（可以理解为给定起点的「一笔画」问题），使得路径的字典序最小。
```

![image-332-2](/media/post/leetcode/leetcode-332_2.png#right)

<mark>Hierholzer 算法</mark>用于在连通图中寻找**欧拉路径**，其流程如下：

* 从起点出发，进行深度优先搜索。
* 每次沿着某条边从某个顶点移动到另外一个顶点的时候，都需要删除这条边。
* 如果没有可移动的路径，则将所在节点加入到栈中，并返回。

```java
class Solution {
    Map<String, PriorityQueue<String>> map = new HashMap<String, PriorityQueue<String>>();
    List<String> itinerary = new LinkedList<String>();

    public List<String> findItinerary(List<List<String>> tickets) {
        for (List<String> ticket : tickets) {
            String src = ticket.get(0), dst = ticket.get(1);
            if (!map.containsKey(src)) {
                map.put(src, new PriorityQueue<String>()); // 入队
            }
            map.get(src).offer(dst); // 出队
        }
        dfs("JFK");
        Collections.reverse(itinerary); // 记住Collection.reverse()方法！
        return itinerary;
    }

    public void dfs(String curr) {
        while (map.containsKey(curr) && map.get(curr).size() > 0) {
            String tmp = map.get(curr).poll();
            dfs(tmp); // 递归调用
        }
        itinerary.add(curr); // 添加到结果集
    }
}
```

![image-332](/media/post/leetcode/leetcode-332.png)
