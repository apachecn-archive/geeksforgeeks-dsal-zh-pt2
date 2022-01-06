# 微软面试体验|第 102 集(IDC 校园版)

> 原文:[https://www . geesforgeks . org/Microsoft-面试-体验-set-102-校园-for-idc/](https://www.geeksforgeeks.org/microsoft-interview-experience-set-102-on-campus-for-idc/)

大约有 150 名学生参加了考试。

**第 1 轮(75 分钟):**

在线编码轮托管在黑客银行。问了三个编码问题。

1.  给定一个整数链表，编写一个函数就地修改链表，使得在修改后的链表中，所有奇数出现在所有偶数之前。偶数和奇数的相对顺序应该保持不变。–[https://www . geeksforgeeks . org/隔离链表中的奇偶元素/](https://www.geeksforgeeks.org/segregate-even-and-odd-elements-in-a-linked-list/)
2.  给定一个浮点数，在不使用内置 sqrt()函数的情况下计算其平方根。
3.  给定一个模式字符串和一个测试字符串，实现正则表达式子字符串匹配。如果图案前面有一个^，它将与起始位置相匹配。同样，如果它前面有一个$，它将匹配结束位置。如果不存在这样的标记，它将检查模式是否是测试的子串。

    ```
    Ex : ^coal
    coaltar
    Result : True
    tar$
    coaltar
    Result : True
    abcd
    efgh
    Result : False

    ```

25 名学生被选中参加下一轮。
**第 2 轮(纸张编码轮):**

1.  顺时针方向打印二叉树的边界遍历。(注意:检查给定树的左右遍历中的叶节点)。–[https://www . geeksforgeeks . org/二叉树的边界遍历/](https://www.geeksforgeeks.org/boundary-traversal-of-binary-tree/)
2.  顺时针旋转正方形图像 90 度。尽可能优化。类似问题:[https://www . geesforgeks . org/in place-rotate-square-matrix-by-90 度/](https://www.geeksforgeeks.org/inplace-rotate-square-matrix-by-90-degrees/)

8 名学生被选中参加下一轮。

**第 3 轮–**个人面试 1****

1.  讨论了论文编码轮问的第一个问题，即二叉树的边界遍历。
2.  如何[合并两个 BST](https://www.geeksforgeeks.org/merge-two-bsts-with-limited-extra-space/)。问我所有能实施的方法。然后让我在 O(logn)中做，其中 n 是节点总数。
3.  让我写代码来查找数组中出现次数大于 n/2 次的数字。然后让我证明写好的算法，基本上，他是在问我怎么能写出那段代码，为什么它能工作。
    再选 7 名学生进行下一轮。

**第 4 轮-个人面试 2**

1.  要求我在 BOOKMYSHOW.com 实施座位预订流程。如何处理两个人几乎同时试图接近同一个座位的情况？他告诉我写基于类的解决方案，询问应该用于解决预订程序所有案例的不同功能。
2.  什么是[单例类](https://www.geeksforgeeks.org/private-constructors-and-singleton-classes-in-java/)？
3.  如何[找到两条线段的交点](https://www.geeksforgeeks.org/given-a-set-of-line-segments-find-if-any-two-segments-intersect/)。给出了线段的两个端点。
4.  如何在 1 号到 n 号之间找到 2 号。他给了我一些提示，最后，他对我的方法很满意
5.  考虑到所有可能的解决方案，实现斐波那契数列。

又问了几个问题，但我不记得了。 **6** 学生被选中进行下一轮。

**第 5 轮-个人面试 3**

1.  为[编写函数，以便在不递归的情况下遍历二叉树。](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)那很简单！！
2.  问了我一个难题。给定一个 n*n 板，其中一个单元格是黑色的。此外，考虑到所有可能的旋转，给出了 L 形块(相当于给定矩阵的 3 个单元)。我必须用这些碎片填满整个网格。棋子不能放在黑格子上，两个棋子不能重叠，甚至不能部分重叠。我给出了一个答案，我试图将不可访问单元(黑色单元和已经放置在板上的块)的大小增加到给定板的大小，但是他问了我几个我的答案失败的例子。然后我对他说，我们可以使用回溯法对组合进行彻底的搜索，但这会花费太多时间。然后他给了我一个线索，那就是不要增加无法到达的细胞的大小，而要设法减少它。最后，我得出结论，它是基于分治的解决方案，将基本情况视为 2*2 板，带有 1 个黑单元。

**4** 学生被选中进行下一轮。

**第 6 轮-个人面试 4**

他让我实现 [LRU 缓存](https://www.geeksforgeeks.org/implement-lru-cache/)。我给了他所有可能的解决方案。他非常乐于助人。他发现了瑕疵，叫我优化。我给了他 3 个解决方案，最后一个是你可以在网上任何地方找到的。但在此之前，他让我用 hashmap 交换一个 DLL 的两个节点。我最初不知道什么是 Lru 缓存。哈哈的笑

**第 7 轮-个人面试 5**

1.  你的激情是什么？你这辈子想做什么？Hr 型问题。
2.  他用英语单词设计了一种新的语言，并将它们存储在一系列字符串中。然后他给了我两个字符串，让我设计 strcmpfunction。我告诉他最好的方法，但他试图迷惑我，他成功了。他给了我 5 分钟，让我想出另一个解决方案，并尝试新的解决方案。最后，我实现了我心中的第一个方法，他对此很满意。
3.  [如何序列化和反序列化 n 元树](https://www.geeksforgeeks.org/serialize-deserialize-n-ary-tree/)。我告诉了他序列化和反序列化二叉树的函数，但是没有给出给定问题的解决方案。

**3** 学生最终入选 MS-IDC。我是其中之一。:p
P.S:我对操作系统和数据库管理系统不太适应，所以我跟他们说得很清楚，但是他们试图间接问操作系统和数据库管理系统的所有基本问题，并告诉我用 C/C++实现它们。

**问朋友的问题:**

*   开发一个算法来解决元素个数为 n 的跨桥问题。
*   [两个链表的交集。](https://www.geeksforgeeks.org/union-and-intersection-of-two-linked-lists/)
*   如果链表中存在循环，则找到[，并且在其中找到循环的开始节点。](https://www.geeksforgeeks.org/write-a-c-function-to-detect-loop-in-a-linked-list/)
*   银行系统的类设计。
*   [使用递归和迭代的反向链表](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)等

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息

[All Practice Problems for Microsoft](https://practice.geeksforgeeks.org/company/Microsoft/) !