# 微软面试体验|第 125 集(IDC 校内)

> 原文:[https://www . geesforgeks . org/Microsoft-面试-体验-设置-125-校园-idc/](https://www.geeksforgeeks.org/microsoft-interview-experience-set-125-campus-idc/)

**微软 IDC 面试体验**

**线上回合**

平台:CoCubes
格式:3 道编码题
时间:75 分钟

他们有一个问题池，随机给每个学生三个问题(2 + 3 + 5 分)。

1.  [Given an integer N and an integer M, output a number closest to N which is divisible by M](https://www.geeksforgeeks.org/find-number-closest-n-divisible-m/).

    ```
    Input: N = 15, M = 7
    Output: 14

    Input : N = 17, M = 3 
    Output : 18

    ```

    O1 中的预期解决方案

2.  Given a string of O’s and 1’s, output the maximum length of a sub-string of all 1’s.

    ```
    Input: 1011010111101
    Output: 4

    Input : 0110111110111101
    Output : 5

    ```

    [极客论坛链接](https://www.geeksforgeeks.org/maximum-consecutive-ones-or-zeros-in-a-binary-array/)
    O(n)中的预期解决方案。

3.  [Length of Longest Arithmetic Progression](https://www.geeksforgeeks.org/length-of-the-longest-arithmatic-progression-in-a-sorted-array/)

    O(n^3 的预期解决方案)

**团体复飞:**

*   *Question 1:*

    [在字符网格中找到一个单词](https://www.geeksforgeeks.org/find-all-occurrences-of-the-word-in-a-matrix/)
    这个问题是对上面问题的修改。我们可以在所有 8 个方向上移动，之字形遍历也是可能的。我们必须返回找到的遍历的坐标(I，j)列表。如果可能有多个遍历，返回任意一个。

    ```
    Input: 
    Grid:  a b c d 
           b d e e
           f g r k
           s g s s

    String: geeks

    Output: (2,1), (1,2), (1,3), (2,3), (3,2)

    ```

    我用 DFS 解决了。

    *   *Question 2:*

    [想象一个欧氏平面，在那个平面上有 N 个点(x，y)。给你一个这样的点的列表。然后，您将会收到关于平面中是否存在特定点的查询。](https://www.geeksforgeeks.org/how-to-check-if-a-given-point-lies-inside-a-polygon/)相应输出真或假。

    0 < N < 10^6
    -10^6 < = x，y < = 10^6

    ```
    Input: 
    Points: (2,1), (1,2), (1,3), (2,3), (3,3)

    Query1: (2,3)
    Output1: TRUE

    Query2: (2,2)
    Output2: FALSE

    ```

    他们希望我们优化查询。我使用无序映射在 O(1)中存储点和输出查询。

    个人面试
    50%的候选人在小组复飞后选出，即 20 名学生。

    **第一轮:**

    *   You have the following operators available with you: + – * / ( )
    Insert few of these operators to make the given line as a valid mathematical expression
    1 2 3 4 5 6 7 8 9 = 100.

    注意:如果我们不在 1 和 2 之间插入任何东西，它就会变成 12。1 到 9 的顺序必须保持不变。

    ```
    Solution: (1 + 2 + 3 + 4) * (-5 + 6) * (-7 + 8 + 9) = 100

    I gave the above solution within 2-3 min. He immediately told me to give one more solution.
    I again took 2-3 mins to come up with one more solution.

    Alternate Solution: 123 - (4 + 5 + 6 + 7) - (-8 + 9) = 100
    ```

    *   我问了他几个澄清问题，他很好地回答了。面试官很专业，乐于助人。

    *   多少部电梯？
        Ans: N 部电梯。n 不止一个。
    *   几层楼？
        Ans: M 层。
    *   我们是每个电梯都有一个按钮，还是每个楼层的所有电梯都只有一个按钮？
        Ans:只有一个按钮控制所有电梯。
    *   Do we need to consider things like max number allowed in the lift, etc?
        Ans: No

        。

        在设计系统的过程中，我几乎没有问其他问题。

        他想让我回答的事情:

    *   我们应该用什么样的算法来控制电梯的运动？
    *   Data Structures to be used

        。

    *   Optimization of the algorithm. A workable algorithm is not enough. It had to be optimised for efficient usage, time and power saving.

        后续问题:

    *   我将如何处理并发请求？
    *   不用的时候，电梯会停在几楼？为什么呢？
    *   一天中的所有时间都一样吗？为什么呢？
    *   白天和晚上我会用同样的算法吗？
    *   我计划如何节省电梯运行功率？
    *   如果其中一台电梯出现故障，我的算法会起作用吗？
    *   如果一个按钮在任何楼层被按了两次，我的数据结构能处理吗？
    *   I have been given one-year data on elevator usage. How would I use this data to optimize my algorithm to increase efficiency?

        你会用任何 ML/AI 的东西来优化这个问题吗？怎么做？

        还有很多问题我记不清了。我必须为每一个设计决定给出一个理由。然后他让我为它编写面向对象的代码。

        解决方案:我有一个中央管理器类来管理所有的电梯，每个电梯都作为一个线程工作。所有数据都存储在中央管理器中。我将收到的请求存储在平衡二叉查找树中。我给每个请求分配了优先级，如果它来自电梯内或电梯外，等等。

    他非常专业，经验丰富。他对我的回答印象深刻。当我写代码的时候，他在他的笔记本电脑上填写了我的反馈。在我写完代码之前，他说我完成了。不需要写代码。

    这轮过后，我被直接送到了招聘经理那里。对少数人进行了一两次技术面试。

    **第二轮(招聘经理):**

    问题:这是一个很长的问题陈述，解决方案归结为[拓扑](https://www.geeksforgeeks.org/topological-sorting/)。我给他解决方案，他让我写代码。

    他对代码深信不疑。然而，他告诉我关于我的代码的一件非常小的事情，它本可以写得更优雅。我同意他的观点。

    然后我们讨论了我的项目。他让我告诉他我在班加罗尔三星研究院实习期间做的项目。他还询问了我的个人项目，并跟进了相关问题。然后他问我有没有问题要问他。我说没有。

    我很惊讶我只给了 2 个回合，所以我问他在这之后还会不会有更多的回合。他说我做得很好。放松点。

    候选人的个人面试次数从 2 次到 4 次不等。

    结果:选中。在我准备期间，GeeksForGeeks 是一个很大的帮助。感谢其他同学分享面试经验。🙂

    如果你喜欢极客博客并想投稿，你也可以用 contribute.geeksforgeeks.org 写一篇文章，或者把你的文章发邮件到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    ## 相关实践问题

    [Closest Number](https://practice.geeksforgeeks.org/problems/closest-number/0)[All Practice Problems for Microsoft](https://practice.geeksforgeeks.org/company/Microsoft/) !