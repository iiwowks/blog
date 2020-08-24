---
layout:     post
title:      "Hash Table"
date:       2020-08-24
category:   Leetcode
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---


### [706. 设计哈希映射](https://leetcode-cn.com/problems/design-hashmap/)

```
不使用任何内建的哈希表库设计一个哈希映射
具体地说，你的设计应该包含以下的功能
* put(key, value)：向哈希映射中插入(键,值)的数值对。如果键对应的值已经存在，更新这个值。
* get(key)：返回给定的键所对应的值，如果映射中不包含这个键，返回-1。
* remove(key)：如果映射中存在这个键，删除这个数值对。
```

* 设计哈希方法：将键值映射到某块存储空间
* 避免哈希冲突：不同键值映射到同一空间，哈希碰撞

<mark>方法一：取模 + 数组 </mark>

![image-706](/media/post/leetcode/leetcode-706_hashmap.png)

```java
/*
 * @lc app=leetcode.cn id=706 lang=java
 *
 * [706] 设计哈希映射: 
 * put(key, value)：向哈希映射中插入键值对
 * get(key)：返回给定键的值
 * remove(key): 删除键值对
 */

// @lc code=start
// Pair类
class Pair<U, V> {
    public U first;
    public V second;

    public Pair(U first, V second) {
        this.first = first;
        this.second = second;
    }
}
// 桶 类
class Bucket {
    private List<Pair<Integer, Integer>> bucket;

    public Bucket() {
        this.bucket = new LinkedList<Pair<Integer, Integer>>();
    }

    public Integer get(Integer key) {
        for (Pair<Integer, Integer> pair : this.bucket) {
            if (pair.first.equals(key)) {
                return pair.second;
            }
        }
        return -1;
    }

    public void update(Integer key, Integer value) {
        boolean found = false;
        for (Pair<Integer, Integer> pair : this.bucket) {
            if (pair.first.equals(key)) {
                pair.second = value;
                found = true;
            }
        }
        if (!found) {
            this.bucket.add(new Pair<Integer, Integer>(key, value));
        }
    }

    public void remove(Integer key) {
        for (Pair<Integer, Integer> pair : this.bucket) {
            if (pair.first.equals(key)) {
                this.bucket.remove(pair);
                break;
            }
        }
    }
}

class MyHashMap {

    private int key_space;
    private List<Bucket> hash_table;

    /** Initialize your data structure here. */
    public MyHashMap() {
        this.key_space = 2069;
        this.hash_table = new ArrayList<Bucket>();
        for (int i = 0; i < this.key_space; ++i) {
            this.hash_table.add(new Bucket());
        }
    }

    /** value will always be non-negative. */
    public void put(int key, int value) {
        int hash_key = key % this.key_space;
        this.hash_table.get(hash_key).update(key, value);
    }

    /** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
    public int get(int key) {
        int hash_key = key % this.key_space;
        return this.hash_table.get(hash_key).get(key);
    }

    /** Removes the mapping of the specified value key if this map contains a mapping for the key */
    public void remove(int key) {
        int hash_key = key % this.key_space;
        this.hash_table.get(hash_key).remove(key);
    }
}
```


### [705. 设计哈希集合](https://leetcode-cn.com/problems/design-hashset/)

```
不使用任何内建的哈希表库设计一个哈希集合
具体地说，你的设计应该包含以下的功能：
* add(value)：向哈希集合中插入一个值。
* contains(value) ：返回哈希集合中是否存在这个值。
* remove(value)：将给定值从哈希集合中删除。如果哈希集合中没有这个值，什么也不做。
```

```java
// * 哈希函数：分配一个地址存储值
// * 冲突处理：单独链表法，开放地址法，双散列法
// @lc code=start
// 方法一：单独链表法：hash = value mod base, 哈希函数使用模运算符。使用LinkedList
class MyHashSet {
    private Bucket[] bucketArray;
    private int keyRange;

    /** Initialize your data structure here. */
    public MyHashSet() {
        this.keyRange = 769;
        this.bucketArray = new Bucket[this.keyRange];
        for (int i = 0; i < this.keyRange; ++i) {
            this.bucketArray[i] = new Bucket();
        }
    }

    // 生成散列值
    protected int _hash(int key) {
        return (key % keyRange);
    }

    public void add(int key) {
        int bucketIndex = this._hash(key);
        this.bucketArray[bucketIndex].insert(key);
    }

    public void remove(int key) {
        int bucketIndex = this._hash(key);
        this.bucketArray[bucketIndex].delete(key);
    }

    /** Returns true if this set contains the specified element */
    public boolean contains(int key) {
        int bucketIndex = this._hash(key);
        return this.bucketArray[bucketIndex].exists(key);
    }
}

// 使用LinkedList实现HashSet中的桶
class Bucket {
    private LinkedList<Integer> container;
    public Bucket() {
        container = new LinkedList<Integer>();
    }

    public void insert(Integer key) {
        int index = this.container.indexOf(key);
        if (index == -1) {
            this.container.addFirst(key);
        }
    }

    public void delete(Integer key) {
        this.container.remove(key);
    }

    public boolean exists(Integer key) {
        int index = this.container.indexOf(key);
        return (index != -1);
    }
}
```

### [202. 快乐数](https://leetcode-cn.com/problems/happy-number/)

```
编写一个算法来判断一个数 n 是不是快乐数。
「快乐数」定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，
然后重复这个过程直到这个数变为1，也可能是无限循环 但始终变不到1。如果可以变为1，那么这个数就是快乐数。
```
