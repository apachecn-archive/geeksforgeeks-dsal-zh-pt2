# 动态编程 vs 分而治之

> 原文:[https://www . geesforgeks . org/dynamic-programming-vs-分治法/](https://www.geeksforgeeks.org/dynamic-programming-vs-divide-and-conquer/)

**TL；DR**

在本文中，我试图通过两个例子来解释动态编程和分治法之间的区别/相似之处:[二分搜索法](https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/search/binary-search)和[最小编辑距离](https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/string/levenshtein-distance) (Levenshtein 距离)。
问题
当我[开始学习算法](https://github.com/trekhleb/javascript-algorithms)时，我很难理解动态规划(DP)的主要思想，以及它与各个击破(DC)的方法有何不同。当要比较这两种范式时，通常斐波那契函数作为一个伟大的[例子](https://stackoverflow.com/questions/13538459/difference-between-divide-and-conquer-algo-and-dynamic-programming)来拯救。但是，当我们试图使用动态规划和 DC 方法来解释同一问题时，我觉得我们可能会丢失有助于更快发现差异的有价值的细节。这些细节告诉我们，每种技术最适合不同类型的问题。
我还在理解 DP 和 DC 的区别的过程中，不能说到目前为止已经完全掌握了概念。但是我希望这篇文章能给你一些额外的启发，帮助你学习动态编程和分治等有价值的算法范式。
动态编程和分而治之的相似之处
就我目前所见，我可以说动态编程是分而治之范式的延伸。
我不会把它们当作完全不同的东西。因为它们都是通过递归地将一个问题分解成两个或多个相同或相关类型的子问题来工作的，直到这些子问题变得足够简单，可以直接解决。子问题的解决方案然后被组合以给出原始问题的解决方案。
那么为什么我们仍然有不同的范式名称，为什么我称动态编程为扩展。这是因为只有当问题有一定的限制或先决条件时，动态编程方法才能应用于问题。之后，动态规划用内存化或列表技术扩展了分治法。
让我们一步一步来……
动态编程的先决条件/限制
正如我们刚刚发现的，为了使动态编程适用，分治问题必须具备两个关键属性:

一旦这两个条件得到满足，我们可以说这个分治问题可以用动态规划方法来解决。
分治的动态编程扩展
动态编程方法通过两种技术(记忆和列表)扩展了分治方法，这两种技术都有存储和重用子问题解决方案的目的，这可能会大大提高性能。例如，斐波那契函数的朴素递归实现具有 O(2^n 的时间复杂度),其中 DP 解仅用 O(n)个时间做同样的事情。
记忆化(自上而下的缓存填充)是指缓存和重用先前计算结果的技术。因此，记忆光纤函数看起来像这样:

```
memFib(n) {
    if (mem[n] is undefined)
        if (n < 2) result = n
        else result = memFib(n-2) + memFib(n-1)
        mem[n] = result
    return mem[n]
}
```

制表(自下而上的高速缓存填充)类似，但侧重于填充高速缓存的条目。计算缓存中的值最容易迭代完成。fib 的列表版本如下所示:

```
tabFib(n) {
    mem[0] = 0
    mem[1] = 1
    for i = 2...n
        mem[i] = mem[i-2] + mem[i-1]
    return mem[n]
}
```

您可以在这里阅读更多关于记忆和列表比较[的内容。
这里你应该掌握的主要思想是，因为我们的分治问题有重叠的子问题，所以子问题解决方案的缓存成为可能，因此记忆/列表逐步上升到场景中。
那么 DP 和 DC 到底有什么区别呢
既然我们现在已经熟悉了 DP 的先决条件及其方法，我们就准备好将上面提到的所有内容放在一张图片中。](https://programming.guide/dynamic-programming-vs-memoization-vs-tabulation.html)

动态编程和分而治之范式依赖

让我们尝试使用动态规划和 DC 方法来解决一些问题，以使这个例子更加清晰。
分治示例:二分搜索法
[二分搜索法](https://en.wikipedia.org/wiki/Binary_search_algorithm)算法，也称为半区间搜索，是一种在排序数组中查找目标值位置的搜索算法。二分搜索法将目标值与数组的中间元素进行比较；如果它们不相等，则目标不能位于的那一半被消除，并且搜索在剩余的一半上继续，直到找到目标值。如果搜索结束，剩余的一半为空，则目标不在数组中。
示例
这里是二分搜索法算法的可视化，其中 4 是目标值。

二进制搜索算法逻辑

让我们以决策树的形式画出同样的逻辑。

决策树二进制搜索算法

你可能在这里清楚地看到解决问题的分治原则。我们迭代地将原始数组分解为子数组，并试图在其中找到所需的元素。
可以应用动态规划吗？不，是因为没有重叠的子问题。每次我们把阵列分成完全独立的部分。根据分治的前提/限制，子问题必须以某种方式重叠。
通常每次你画一棵决策树，它实际上是一棵树(而不是决策图)，这意味着你没有重叠的子问题，这不是动态规划问题。
代码
[在这里](https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/search/binary-search)你可以找到完整的二分搜索法函数源代码，有测试用例和解释。

```
function binarySearch(sortedArray, seekElement) {
  let startIndex = 0;
  let endIndex = sortedArray.length - 1;
  while (startIndex <= endIndex) {
    const middleIndex = startIndex + Math.floor((endIndex - startIndex) / 2);
    // If we've found the element just return its position.
    if (sortedArray[middleIndex] === seekElement)) {
      return middleIndex;
    }
    // Decide which half to choose: left or right one.
    if (sortedArray[middleIndex] < seekElement)) {
      // Go to the right half of the array.
      startIndex = middleIndex + 1;
    } else {
      // Go to the left half of the array.
      endIndex = middleIndex - 1;
    }
  }
  return -1;
}
```

动态编程示例:最小编辑距离
通常，在动态编程示例中，默认采用[斐波那契](https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/math/fibonacci)数算法。但是让我们用一个稍微复杂一点的算法来进行一些变化，这应该有助于我们理解这个概念。
[最小编辑距离](https://en.wikipedia.org/wiki/Levenshtein_distance)(或莱文斯坦距离)是用于测量两个序列之间差异的字符串度量。非正式地说，两个单词之间的 Levenshtein 距离是将一个单词变成另一个单词所需的最小单字符编辑(插入、删除或替换)次数。
示例
例如“小猫”和“坐着”之间的 Levenshtein 距离为 3，因为以下三个编辑将一个更改为另一个，少于三个编辑是没有办法做到的:

应用程序
这有广泛的应用，例如，拼写检查器、用于光学字符识别的校正系统、模糊字符串搜索以及基于翻译记忆辅助自然语言翻译的软件。
数学定义
数学上，两个字符串 a，b(长度分别为|a|和|b|的)之间的 Levenshtein 距离由函数 lev(|a|，|b|)给出，其中

请注意，最小值中的第一个元素对应于删除(从 a 到 b)，第二个对应于插入，第三个对应于匹配或不匹配，具体取决于各个符号是否相同。
解释
好的，让我们试着弄清楚那个公式在说什么。让我们举一个简单的例子，找出字符串 ME 和 MY 之间的最小编辑距离。直觉上你已经知道这里的最小编辑距离是 1 操作，这个操作就是“用 Y 替换 E”。但是让我们试着用算法的形式来形式化它，以便能够做更复杂的例子，比如将星期六转换成星期天。
要将公式应用于 ME > MY 变换，我们需要事先知道 ME > M、M > MY 和 M > M 变换的最小编辑距离。然后我们需要选择最小的一个，加上+1 运算来转换最后一个字母 E？Y.
所以我们已经可以在这里看到解决方案的递归性质:ME 的最小编辑距离>基于三个先前可能的变换来计算 MY 变换。因此我们可以说这是分治算法。
为了进一步解释这一点，让我们绘制以下矩阵。

查找我和我的字符串之间的最小编辑距离的简单示例

单元格(0，1)包含红色数字 1。这意味着我们需要 1 个操作来将 M 转换为空字符串:删除 M。这就是为什么这个数字是红色的。
单元格(0，2)包含红色数字 2。这意味着我们需要 2 个操作来将 ME 转换为空字符串:删除 E，删除 m
单元格(1，0)包含绿色数字 1。这意味着我们需要 1 个操作来将空字符串转换为 M:插入 M。这就是为什么这个数字是绿色的。
单元格(2，0)包含绿色数字 2。这意味着我们需要 2 个操作来将空字符串转换为 MY: insert Y，insert M.
单元格(1，1)包含数字 0。这意味着将 M 转换为 M 不需要花费任何成本。
单元格(1，2)包含红色数字 1。意思是我们需要 1 次运算把 ME 转换成 M: delete E.
等等……
这个对于我们这样的小矩阵来说看起来很容易(只有 3×3)。但是我们如何为更大的矩阵计算所有这些数字(比如说 9×7 ^ 1，用于周六>周日变换)？
好消息是，根据公式你只需要三个相邻的单元格(i-1，j)，(i-1，j-1)和(I，j-1)来计算当前单元格(I，j)的个数。我们所需要做的就是找到这三个单元格的最小值，然后加上+1，以防 i-s 行和 j-s 列的字母不同
所以你可能会再次清楚地看到问题的递归性质。

最小编辑距离问题的递归性质

好的，我们刚刚发现我们正在处理分治的问题。但是我们能应用动态规划方法吗？这个问题满足我们的重叠子问题和最优子结构限制吗？是的。让我们从决策图来看。

子问题重叠的最小编辑距离决策图

首先这不是决策树。这是一个决策图。您可能会在图片上看到一些用红色标记的重叠子问题。此外，也没有办法减少运算次数，使其少于公式中三个相邻单元格的最小值。
您可能还会注意到，矩阵中的每个单元号都是基于以前的单元号计算的。因此，这里应用了制表技术(以自下而上的方向填充缓存)。您将在下面的代码示例中看到它。
进一步应用这个原则，我们可能会解决更复杂的情况，比如周六>周日变换。

将周六转换为周日的最小编辑距离

代码
[在这里](https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/string/levenshtein-distance)你可以找到完整的最小编辑距离函数的源代码，带有测试用例和解释。

```
function levenshteinDistance(a, b) {
  const distanceMatrix = Array(b.length + 1)
    .fill(null)
    .map(
      () => Array(a.length + 1).fill(null)
    );

  for (let i = 0; i <= a.length; i += 1) {
    distanceMatrix[0][i] = i;
  }

  for (let j = 0; j <= b.length; j += 1) {
    distanceMatrix[j][0] = j;
  }

  for (let j = 1; j <= b.length; j += 1) {
    for (let i = 1; i <= a.length; i += 1) {
      const indicator = a[i - 1] === b[j - 1] ? 0 : 1;

      distanceMatrix[j][i] = Math.min(
        distanceMatrix[j][i - 1] + 1, // deletion
        distanceMatrix[j - 1][i] + 1, // insertion
        distanceMatrix[j - 1][i - 1] + indicator, // substitution
      );
    }
  }

  return distanceMatrix[b.length][a.length];
}
```

结论
本文比较了动态规划和分治两种算法。我们发现动态规划是基于分治原则的，只有当问题有重叠子问题和最优子结构时(如在 Levenshtein 距离的情况下)，才可以应用动态规划。然后，动态编程使用记忆或制表技术来存储重叠子问题的解决方案，供以后使用。
希望这篇文章没有给大家带来更多的困惑，而是对这两个重要的算法概念有所启发！🙂
你可以在 [JavaScript 算法和数据结构](https://github.com/trekhleb/javascript-algorithms)库中找到更多关于分治和动态编程问题的例子，包括解释、注释和测试用例。
快乐编码！