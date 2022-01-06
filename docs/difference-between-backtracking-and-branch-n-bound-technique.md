# 回溯和分支 N-界限技术的区别

> 原文:[https://www . geeksforgeeks . org/回溯与分支 n-bound-technology 的区别/](https://www.geeksforgeeks.org/difference-between-backtracking-and-branch-n-bound-technique/)

[算法](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)是为解决复杂问题而定义的有条不紊的步骤序列。

在本文中，我们将看到回溯和分支定界技术这两种算法之间的区别。

在讨论差异之前，让我们先了解一下这些算法。

**回溯:** [回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)是一种寻找某些计算问题(特别是约束满足问题)的所有解的通用算法，它对解增量地构建可能的候选，并且一旦确定候选不可能完成就放弃该候选，以最终成为有效解。这是一种递归解决问题的算法技术，通过尝试一次一个地逐步构建一个解决方案，移除那些在任何时间点都不能满足问题约束的解决方案(这里的时间指的是到达搜索树的任何级别所经过的时间)。

**分支和界限:** [分支和界限](https://www.geeksforgeeks.org/branch-and-bound-algorithm/#:~:text=Branch%20and%20bound%20is%20an, possible%20permutations%20in%20worst%20case.)是离散和组合优化问题以及数学优化的算法设计范例。分支定界算法由候选解的系统枚举组成。也就是说，候选解的集合被认为是形成一个根树，整个集合在根。该算法探索该树的分支，这些分支代表解集的子集。在枚举一个分支的候选解之前，根据最优解的估计上下限检查该分支，如果它不能产生比算法迄今为止找到的最佳解更好的解，则丢弃该分支。

下表解释了这两种算法之间的区别:

<figure class="table">

****参数****回溯****Branch and Bound**

方法回溯被用来寻找一个问题的所有可能的解决方案。当它意识到自己做了一个错误的选择时，它会通过备份来撤销最后的选择。它搜索状态空间树，直到找到问题的解决方案。分支定界用于解决优化问题。当它意识到它已经有了预解所导致的更好的最优解时，它就放弃了预解。它完全搜索状态空间树以获得最优解。横越回溯以 [DFS(深度优先搜索)](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)方式遍历状态空间树。分枝定界以任何方式遍历树， [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 或 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。功能回溯涉及可行性函数。分支定界包含一个定界函数。问题回溯用于解决决策问题。分支定界用于解决优化问题。搜索在回溯中，搜索状态空间树，直到获得解。在分支定界中，最优解可能出现在状态空间树的任何地方，因此需要完全搜索该树。效率回溯更有效。分支定界效率较低。应用程序有助于解决 [N 皇后问题](https://www.geeksforgeeks.org/n-queen-problem-backtracking-3/)，[子集](https://www.geeksforgeeks.org/subset-sum-backtracking-4/)之和。有助于解决[背包问题](https://www.geeksforgeeks.org/0-1-knapsack-using-branch-and-bound/)、[旅行推销员问题](https://www.geeksforgeeks.org/traveling-salesman-problem-using-branch-and-bound-2/)。** </figure>