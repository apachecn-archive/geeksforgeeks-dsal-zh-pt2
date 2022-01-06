# 最小二乘法的 Prim 算法和 Kruskal 算法的区别

> 原文:[https://www . geeksforgeeks . org/prims-and-kruskals-algorithm-for-MST/](https://www.geeksforgeeks.org/difference-between-prims-and-kruskals-algorithm-for-mst/)

[**<u>克鲁斯卡尔算法求 MST</u>**T5】](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)

给定一个连通且无向的[图](https://www.geeksforgeeks.org/graph-and-its-representations/)，该图的生成树是一个将所有顶点连接在一起的树的子图。一个图可以有许多不同的生成树。加权、连通和无向图的[最小生成树(MST)](https://www.geeksforgeeks.org/applications-of-minimum-spanning-tree/) 或最小权重生成树是权重小于或等于所有其他生成树的权重的生成树。生成树的权重是赋予生成树每条边的权重之和。

**以下是使用克鲁斯卡尔算法**寻找 MST 的步骤

1.  按照权重的非递减顺序对所有边进行排序。
2.  选择最小的边。检查它是否与到目前为止形成的生成树形成一个循环。如果循环没有形成，包括这条边。否则，丢弃它。
3.  重复步骤#2，直到生成树中有(V-1)条边。

[**<u>普里姆的算法为</u>**](https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5/)

和 Kruskal 的算法一样，Prim 的算法也是一个 Greedy 算法。它从一个空的生成树开始。这个想法是保持两组顶点。第一个集合包含已经包含在 MST 中的顶点，另一个集合包含尚未包含的顶点。在每一步中，它都会考虑连接这两组边的所有边，并从这些边中挑选最小权重的边。拾取边后，它会将边的另一个端点移动到包含 MST 的集合中。

**以下是使用 Prim 算法**查找 MST 的步骤

1.  创建一个集合 mstSet 来跟踪已经包含在 MST 中的顶点。
2.  为输入图形中的所有顶点指定一个键值。将所有键值初始化为 INFINITE。为第一个顶点指定键值为 0，以便首先拾取它。
3.  虽然 mstSet 不包括所有顶点
    *   选择一个不在 mstSet 中的顶点 u，它有最小键值。
    *   包括 u 到 mstSet。
    *   更新 u 的所有相邻顶点的键值。要更新键值，请遍历所有相邻顶点。对于每个相邻的顶点 v，如果边 u-v 的权重小于 v 的前一个键值，则将键值更新为 u-v 的权重

Prim 算法和 Kruskal 算法都找到了最小生成树，并遵循贪婪的方法来解决问题，但它们之间的主要区别很少<u>。</u>

<figure class="table">

| 普里姆算法 | 克鲁斯卡尔算法 |
| --- | --- |
| 它开始从图中的任意顶点构建最小生成树。 | 它从图中承载最小权重的顶点开始构建最小生成树。 |
| 它会多次遍历一个节点来获得最小距离。 | 它只遍历一个节点一次。 |
| Prim 的算法时间复杂度为 O(V <sup>2</sup> ，V 为顶点数，使用斐波那契堆可以提高到 O(E log V)。 | Kruskal 算法的时间复杂度为 O(E log V)，V 为顶点数。 |
| Prim 的算法给出了连通分支，并且只在连通图上有效。 | Kruskal 的算法可以在任何时刻生成森林(断开的组件)，也可以在断开的组件上工作 |
| Prim 的算法在密集图中运行得更快。 | Kruskal 的算法在稀疏图中运行得更快。 |
| Prim 的算法使用列表数据结构。 | 克鲁斯卡尔的算法使用堆数据结构。 |

</figure>