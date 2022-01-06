# 数据结构|杂项|问题 5

> 原文:[https://www . geesforgeks . org/data-structures-misc-question-4/](https://www.geeksforgeeks.org/data-structures-misc-question-4/)

需要一种数据结构来存储一组整数，以便可以在(log n)时间内完成以下每个操作，其中 n 是该组中的元素数量。

```
   o    Delection of the smallest element 
   o    Insertion of an element if it is not already present in the set

```

以下哪些数据结构可用于此目的？
**(A)** 可以用一堆但不能用平衡的二叉查找树
**(B)** 可以用平衡的二叉查找树但不能用一堆
**(C)** 平衡的二叉查找树和堆都可以用
**(D)** 既不能用平衡的二叉查找树也不能用堆

**回答:****(B)**

**说明:**因为它是一个 BST，所以我们可以很容易地找出 O(nlogn)中的最小元素。详见我们的帖子[找到二叉查找树](https://www.geeksforgeeks.org/find-the-minimum-element-in-a-binary-search-tree/)中的最小元素。

由于[堆](http://en.wikipedia.org/wiki/Binary_heap)是平衡二叉树(或几乎完全二叉树)，堆的插入复杂度为 O(logn)。在最小堆中获得最小值的复杂性也是 0(logn)，因为移除根节点会导致调用[堆](http://www.cs.virginia.edu/~luebke/cs332.fall00/lecture4/index.htm)(从数组中移除第一个元素后)来维护堆树属性。但是正如问题所说，堆不能用于上述目的——如果元素还不存在，就插入一个元素。对于堆，我们无法在 O(logn)中发现一个元素是否存在。感谢游戏提供了正确的解决方案。

[本题小考](https://www.geeksforgeeks.org/data-structure-gq/misc-3-gq/)