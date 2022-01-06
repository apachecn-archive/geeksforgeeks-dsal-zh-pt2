# 后验分析和先验分析的差异

> 原文:[https://www . geeksforgeeks . org/后验与先验分析之差/](https://www.geeksforgeeks.org/difference-between-posteriori-and-priori-analysis/)

先决条件–[算法分析](https://www.geeksforgeeks.org/fundamentals-of-algorithms/#AnalysisofAlgorithms)
算法是解决给定问题的有限状态的组合或序列。如果问题有一个以上的解决方案或算法，那么最好的一个是由基于两个因素的分析决定的。

1.  CPU 时间([时间复杂度](https://www.geeksforgeeks.org/understanding-time-complexity-simple-examples/)
2.  主内存空间([空间复杂度](https://www.geeksforgeeks.org/g-fact-86/)

算法的时间复杂度可以通过两种方法计算:

1.  后验分析
2.  先验分析

**使徒分析与先验分析的区别:**

<figure class="table">

| 后验分析 | 先验分析 |
| --- | --- |
| 后验分析是一种相对分析。 | 皮奥利分析是绝对分析。 |
| 这取决于编译器的语言和硬件的类型。 | 它独立于编译器的语言和硬件类型。 |
| 它会给出确切的答案。 | 它会给出大致的答案。 |
| 它不使用渐近符号来表示算法的时间复杂度。 | 它使用渐近符号来表示算法完成执行所需的时间。 |
| 使用后验分析的算法的时间复杂度因系统而异。 | 对于每个系统，使用先验分析的算法的时间复杂度是相同的。 |
| 如果程序花费的时间更少，那么功劳将归于编译器和硬件。 | 如果算法运行得更快，功劳归于程序员。 |

</figure>