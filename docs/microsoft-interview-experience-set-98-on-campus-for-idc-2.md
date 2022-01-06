# 微软面试体验|第 99 集(IDC 和 IT 校园)

> 原文:[https://www . geesforgeks . org/Microsoft-interview-experience-set-98-校园-for-idc-2/](https://www.geeksforgeeks.org/microsoft-interview-experience-set-98-on-campus-for-idc-2/)

最近，微软访问了我们的校园，为他们的国际数据中心和信息技术部门招聘实习生。
**第一轮**

*   **Q1:** 给定一个整数链表，[编写一个函数就地修改链表，使得修改后的链表中所有奇数出现在所有偶数之前。](https://www.geeksforgeeks.org/segregate-even-and-odd-elements-in-a-linked-list/)偶数和奇数的相对顺序应该保持不变。
    例如:

    ```
    Input: 1->8->2->10->5->4->7->6->NULL
    Output: 1->5->7->8->2->10->4->6->NULL

    ```

    *   **Q2:** [给定一个浮点数，不用内置 sqrt()函数计算其平方根。](https://www.geeksforgeeks.org/square-root-of-a-perfect-square/)*   **Q3:** Given a pattern string and a test string, implement RegEx substring matching. If the pattern is preceded by a ^, it will match with the starting position. Similarly, if it is preceded by a $, it will match the ending position. If no such markers are present, it will check whether pattern is a substring of test.
    For Example:

    ```
    ^coal
    coaltar
    Result: True
    $tar
    coaltar
    Result: True
    abcd
    efgh
    Result: False

    ```

    大约 50 人有资格参加下一轮。从跨越三个问题的总共 40 个测试用例中，成功通过 20 个测试用例确保了资格。所有这三个问题都有棘手的、隐藏的边缘情况，很少有考生能在一个问题中通过所有的测试情况。

    **第 2 轮**–纸笔轮:给出了两个编码问题，其解决方案将在纸笔上提交。这一轮总共分配了 45 分钟:

    1.  **Q1:** 顺时针旋转正方形图像 90 度
        **类似问题** : [GeeksforGeeks Link。](https://www.geeksforgeeks.org/inplace-rotate-square-matrix-by-90-degrees/)
    2.  **Q2:** [Given an array of integers and a target sum, write a function to check whether there exists a pair of integers whose sum equals the target](https://www.geeksforgeeks.org/given-an-array-a-and-a-number-x-check-for-pair-in-a-with-sum-as-x/). Use extra space to reduce the time complexity as much as possible.

        这一轮共有 17 名学生合格。

    **第 3 轮-个人面试 1:** 这是技术轮。对兴趣和项目进行了简短的讨论，然后是两个编码问题:

    1.  **Q1:** [编写一个函数来颠倒一个字符串中单词的顺序](https://www.geeksforgeeks.org/reverse-words-in-a-given-string/)
        我最初的解决方案有一个小 bug，后来我修复了这个 bug。
    2.  **Q2:** [给定一个链表和一个整数 n，编写一个函数从链表中移除每 n 个节点。](https://www.geeksforgeeks.org/remove-every-k-th-node-linked-list/)

        ```
        For Example, 1->2->3->4->5->6->NULL n=3;
        Result: 1->2->4->5->NULL
        ```

    **第 4 轮**–**个人访谈 2:** 这是第二轮技术赛。简短的课程讨论之后是三个编码问题。

    1.  **Q1:** [给定一棵二叉树和一个目标和，返回所有有目标和的根到叶路径。](https://www.geeksforgeeks.org/root-to-leaf-path-sum-equal-to-a-given-number/)解决了这个问题后，面试官问了一些可以用来测试代码工作是否完美的案例。一旦他满意了，他就修改了问题，现在想检查是否有节点到叶子的路径有目标和。我简要地讨论了我的方法，它已经足够好了。
    2.  **Q2:** [给定一个长度为 n 的字符串，生成该字符串所有可能的子字符串。](https://www.geeksforgeeks.org/program-print-substrings-given-string/)我最初误解了这个问题，以为字符串所有 2n 种可能的组合。看到这个问题的解决方案，面试官说我把解决方案搞得太复杂了，又把问题解释了一遍。他似乎对我给出的最终解决方案很满意。
    3.  **Q3:** 假设您必须构建一个 API，允许客户从所有可用的 API 中预订酒店。您将如何处理这个问题，以及您将为每个功能使用什么数据结构。这是一个面向对象的问题，他正在寻找一种能够让客户查看酒店详细信息并预订一家酒店的类设计。

    **第 5 轮-个人面试 3:**

    *   他问我读过哪些书，在大学里完成的最艰巨的作业是什么，在这个过程中我面临的问题是什么。*   在这之后，他问我在数组中搜索元素的最佳方式是什么。这是一个相当模糊的问题，我回答说，对于较小的阵列，线性搜索足够有效，但是对于较大的阵列，二分搜索法搜索更有效。*   Then I was asked to implement a library system which could allow anyone to issue or return a book and find the corresponding dues left. He kept adding certain functionalities as time went on which were to be implemented by modifying the classes as per the needs.

    最终，共有 5 名候选人入选微软国际数据中心，3 名候选人入选微软信息技术。

    总而言之，这对我来说是一次难忘的经历。整个过程从头到尾都非常专业，面试官也很友好和支持。他们更感兴趣的是看一个候选人如何实际应用他/她知道的概念，而不是看他/她知道多少不同的概念。
    我对其他候选人的建议是在这个过程中保持冷静，时刻保持自信。坚持你的基础知识，学会从头开始开发解决方案，而不是记住几个困难的算法。提供正确的方法和思路显然比实际给出完美的解决方案更重要。

    如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息

    [All Practice Problems for Microsoft](https://practice.geeksforgeeks.org/company/Microsoft/) !

    ## 相关实践问题

    [Reverse each word in a given string](https://practice.geeksforgeeks.org/problems/reverse-each-word-in-a-given-string/0)