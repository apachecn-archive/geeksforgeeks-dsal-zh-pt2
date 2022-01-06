# 减少并征服

> 原文:[https://www.geeksforgeeks.org/decrease-and-conquer/](https://www.geeksforgeeks.org/decrease-and-conquer/)

由于[各个击破](https://www.geeksforgeeks.org/divide-and-conquer-introduction/)的方法已经讨论过了，其中包括以下步骤:
**将**问题分成若干个子问题，这些子问题是同一问题的较小实例。
**通过递归求解子问题来征服**。然而，如果子问题足够小，就直接解决子问题。
**将**子问题的解决方案合并为原问题的解决方案。

同样，减少-征服方法也是有效的，它还包括以下步骤:
**减少**或将问题实例减少到同一问题的更小实例并扩展解决方案。
**通过解决问题的较小实例来攻克问题。
**扩展较小实例的**解，得到原问题的解。
减少和征服技术的基本思想是基于利用问题的给定实例的解决方案与其较小实例的解决方案之间的关系。这种方法也被称为增量法或归纳法。**

**“分而治之”vs“减少而征服”:**

按照[维基百科](https://en.wikipedia.org/wiki/Divide_and_conquer_algorithm#Divide_and_conquer)的说法，有些作者认为“分治”这个名字只应该在每个问题可能产生两个或更多子问题的时候使用。名称减少和征服已被提议代替为单一子问题类。按照这个定义，[合并排序](https://www.geeksforgeeks.org/merge-sort/)和[快速排序](https://www.geeksforgeeks.org/quick-sort/)属于分治(因为有 2 个子问题)[二分搜索法](https://www.geeksforgeeks.org/binary-search/)属于减少征服(因为有 1 个子问题)。

**减少和征服的实现:**

这种方法既可以自顶向下实现，也可以自底向上实现。

**自上而下的方法:**它总是导致问题的递归实现。
**自下而上的方法:**它通常以迭代的方式实现，从问题的最小实例的解决方案开始。

**减少和征服的变化:**

减少和征服有三个主要的变化:

1.  减少一个常数
2.  减少一个常数
3.  可变尺寸减小

**减少一个常数**:在这个变体中，在算法的每次迭代中，实例的大小减少了相同的常数。通常，该常数等于 1，尽管偶尔会发生其他常数尺寸减小。以下是示例问题:

*   [插入输出](https://www.geeksforgeeks.org/insertion-sort/)
*   图形搜索算法:[DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)[BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)
*   [拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)
*   用于生成排列、子集

**减少一个常数因子**:这种技术建议在算法的每次迭代中用相同的常数因子减少一个问题实例。在大多数应用中，这个常数因子等于 2。减少两倍以外的因素尤其罕见。

减少一个常数因子算法是非常有效的，特别是当因子大于 2 时，如在假币问题。以下是示例问题:

*   [二分搜索法](https://www.geeksforgeeks.org/binary-search/)
*   假币问题
*   [俄罗斯农民倍增](https://www.geeksforgeeks.org/russian-peasant-multiply-two-numbers-using-bitwise-operators/)

**可变尺寸减小**:在这个变化中，尺寸减小模式随着算法的一次迭代而变化。
因为，在寻找两个数的 gcd 的问题中，虽然第二个参数的值在右手边总是比在左手边小，但它既没有减少一个常数，也没有减少一个常数因子。以下是示例问题:

*   [计算中位数和选择问题](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)。
*   [插值搜索](https://www.geeksforgeeks.org/interpolation-search/)
*   [欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)

可能有这样一种情况，即问题可以通过按常数减少和按因子减少的变化来解决，但是实现可以是递归的或迭代的。迭代实现可能需要更多的编码工作，但是它们避免了伴随递归的重载。

**参考:**
[阿纳尼·莱维丁](https://www.amazon.in/Introduction-Design-Analysis-Algorithms-Levitin/dp/0132316811)
[减少并征服](http://faculty.simpson.edu/lydia.sinapova/www/cmsc250/LN250_Levitin/L07-DecreaseConquer.htm#intro)