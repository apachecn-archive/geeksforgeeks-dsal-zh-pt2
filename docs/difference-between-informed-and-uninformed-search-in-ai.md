# AI 中知情搜索和不知情搜索的区别

> 原文:[https://www . geeksforgeeks . org/知情与不知情的区别-ai 搜索/](https://www.geeksforgeeks.org/difference-between-informed-and-uninformed-search-in-ai/)

**先决条件:** [人工智能中的搜索算法](https://www.geeksforgeeks.org/search-algorithms-in-ai/)

**通知搜索:**通知搜索算法具有关于目标状态的信息，这有助于更有效的搜索。这个信息是通过一个估计一个状态离目标状态有多近的函数获得的。
**示例:** [贪婪搜索](https://www.geeksforgeeks.org/greedy-algorithms/)和图形搜索

**无信息搜索:**除了问题定义中提供的信息外，无信息搜索算法在目标节点上没有其他信息。从开始状态到达目标状态的计划仅在动作的顺序和长度上有所不同。
**示例:** [深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)和[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)

**知情搜索与不知情搜索:**

<figure class="table">

| 知情搜索 | 无信息搜索 |
| --- | --- |
| 它使用知识进行搜索。 | 它不使用知识进行搜索过程。 |
| 它能更快地找到解决方案。 | 与有根据的搜索相比，它找到解决方案的速度较慢。 |
| 它可能完整，也可能不完整。 | 它总是完整的。 |
| 成本低。 | 成本高。 |
| 它消耗更少的时间。 | 它消耗适度的时间。 |
| 它提供了解决方案的方向。 | 对于其中的解决方案，没有给出任何建议。 |
| 它在实现时不太冗长。 | 它在实现时更加冗长。 |
| 贪婪搜索，A*搜索，图形搜索 | 深度优先搜索，广度优先搜索 |

</figure>