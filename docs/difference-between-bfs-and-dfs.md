# BFS 和 DFS 的区别

> 原文:[https://www . geesforgeks . org/bfs 和 dfs 之间的差异/](https://www.geeksforgeeks.org/difference-between-bfs-and-dfs/)

### **<u>广度优先搜索</u>**

[**BFS** 代表**广度优先搜索**](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 是一种基于顶点的技术，用于在图中寻找最短路径。它使用先入先出的[队列数据结构](https://www.geeksforgeeks.org/queue-data-structure/)。在 BFS，当一个顶点被访问和标记时，它被选中，然后它的相邻顶点被访问并存储在队列中。它比 DFS 慢。
**Ex-**

```
        A
       / \
      B   C
     /   / \
    D   E   F
```

**输出为:**

```
A, B, C, D, E, F
```

### **<u>深度优先搜索</u>**

[**DFS** 代表**深度优先搜索**](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 是一种基于边缘的技术。它使用[堆栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)，执行两个阶段，首先访问的顶点被推入堆栈，其次，如果没有顶点，则弹出访问的顶点。
**Ex-**

```
        A
       / \
      B   C
     /   / \
    D   E   F
```

**输出为:**

```
A, B, D, C, E, F
```

### **<u>BFS vs DFS</u>**

<figure class="table">

| S.NO | BFS | 深度优先搜索 |
| 1. | BFS 代表广度优先搜索。 | DFS 代表深度优先搜索。 |
| 2. | BFS(广度优先搜索)使用队列数据结构来寻找最短路径。 | 深度优先搜索使用堆栈数据结构。 |
| 3. | BFS 可以用来在未加权的图中寻找单源最短路径，因为在 BFS，我们到达的顶点与源顶点的边数最少。 | 在 DFS 中，我们可能会遍历更多的边来从一个源到达一个目的顶点。 |
| 3. | BFS 更适合搜索更接近给定源的顶点。 | 当有远离源头的解决方案时，DFS 更适合。 |
| 4. | BFS 首先考虑所有邻居，因此不适合在游戏或谜题中使用决策树。 | DFS 更适合游戏或解谜问题。我们做出决定，然后通过这个决定探索所有的途径。如果这个决定导致了胜利，我们就停下来。 |
| 5. | 使用邻接表时 BFS 的时间复杂度为 O(V + E)，使用邻接矩阵时 bfs 的时间复杂度为 O(V^2，其中 v 代表顶点，e 代表边。 | 当使用邻接表时，DFS 的时间复杂度也是 O(V + E)，当使用邻接矩阵时，DFS 的时间复杂度也是 O(V^2，其中 v 代表顶点，e 代表边。 |
| 6. | 在这里，兄弟姐妹先于孩子被拜访 | 在这里，孩子们比兄弟姐妹先到 |
|   |   |   |

另请参见[二叉树的 BFS vs DFS](https://www.geeksforgeeks.org/bfs-vs-dfs-binary-tree/)以了解二叉树遍历的区别。

</figure>