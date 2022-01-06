# 基于比较的排序算法的下限

> 原文:[https://www . geesforgeks . org/基于比较的排序算法下限/](https://www.geeksforgeeks.org/lower-bound-on-comparison-based-sorting-algorithms/)

排序的问题可以看做如下。

**输入:**一系列 *n* 数字< *a* <sub>1</sub> ， *a* <sub>2</sub> 。。。， *a <sub>n</sub>* >。
**输出:** A 排列(重排)< *a* ' <sub>1</sub> ， *a* ' <sub>2</sub> ，。。。，*a*'*<sub>n</sub>*>的输入顺序使得*a*'<sub>1</sub><=*a*'<sub>2</sub>…..< = a' *<sub>n</sub>* 。

如果排序算法使用比较运算符来查找两个数字之间的顺序，则它是基于比较的。可以根据决策树抽象地看待比较排序。决策树是一种完整的二叉树，它表示元素之间的比较，这些比较由特定的排序算法在给定大小的输入上执行。排序算法的执行对应于追踪从决策树的根到叶子的路径。在每个内部节点，进行比较*a<sub>I</sub>T5<=*a<sub>j</sub>T9】。然后，左边的子树指示对*a<sub>I</sub>*<=*a<sub>j</sub>*的后续比较，右边的子树指示对*a<sub>I</sub>*>*a<sub>j</sub>*的后续比较。当我们来到一片叶子时，排序算法已经建立了排序。所以我们可以说决策树如下。**

**1)** 每个 *n* ！ *n* 元素上的排列必须作为决策树的一片叶子出现，排序算法才能正确排序。

**2)** 设 x 为排序算法中的最大比较次数。决策树的最大高度为 x。具有最大高度 x 的树最多有 2^x 树叶。

结合以上两个事实，我们得到以下关系。

```

      n!  <= 2^x

 Taking Log on both sides.
      log2(n!)  <= x

 Since log2(n!)  = Θ(nLogn),  we can say
      x = Ω(nLog2n)
```

因此，任何基于比较的排序算法都必须至少进行 nLog <sub>2</sub> n 次比较才能对输入数组进行排序，Heapsort 和 merge sort 是渐近最优的比较排序。

**参考文献:**
[算法导论，作者:托马斯·h·科曼、查尔斯·e·雷瑟森、罗纳德·L·李维斯特和克利福德·斯坦](http://mitpress.mit.edu/algorithms/)