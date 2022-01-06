# MakeMyTrip 面试体验|第七集(校内)

> 原文:[https://www . geesforgeks . org/make my trip-面试-体验-设置-7-在校园内/](https://www.geeksforgeeks.org/makemytrip-interview-experience-set-7-on-campus/)

最近，makemytrip 参观了我们的校园，我在招聘活动中被选中。放置驱动包括 4 轮。

**第 1 轮:MCQ 和编码轮**

这是一个 60 分钟的在线测试，包括 20 道能力倾向问题和 3 道编码问题。用于测试的平台很复杂，有点难以理解。

**问题 1:** [使用 logn 方法](https://practice.geeksforgeeks.org/problems/abset-2/0)计算^ b mod c 的功率。需要注意的是，您不需要返回或打印您的答案，但是您必须将其存储在他们预定义的全局变量中。你可以很容易地在 geeksforgeeks 网站上找到解决方案。

**问题 2:** [给定一个句子，你应该计算大写字母、小写字母和数字的个数。](https://practice.geeksforgeeks.org/problems/count-type-of-characters/0)这个问题看起来很简单，但重点是你需要将答案以 c1:c2:c3 的形式存储在 char*输出变量中，其中 c1 代表大写字母计数，c2 代表小写字母计数，c3 代表数字计数。
(提示使用 sprintf 将您的答案以格式化的方式存储在变量
sprintf 中(输出，“%d:%d:%d”，c1，c2，C3)；
)

**问题 3:** [活动调度问题](https://practice.geeksforgeeks.org/problems/n-meetings-in-one-room/0)
给你 2 个数组，代表活动的开始和结束时间。确定你能完成的非冲突活动的最大数量。
(提示:做一个开始和结束时间的结构，按照结束间隔排序)

我完全解决了 2 个，部分解决了 1 个
提示:因为他们只有一个样本测试用例，所以即使你不能解决编码问题，只要把硬编码的答案存储在那个变量中。我最后做了那件事

在 110 名学生中，有 30 名学生被选中参加个人面试。

**第 2 轮:个人面试**
由于我是名单中最后一个从上午 10:30 开始等待的候选人，所以晚上 10:30 轮到我了。面试官非常冷静友好。他首先问我关于你自己和我做过的项目。在对我的项目进行了半个小时的冗长讨论并制作了我在项目中使用的数据库模式后，他开始在 ds 上提问。

**问题 1:** [对 0，1，2 组成的链表进行排序](https://practice.geeksforgeeks.org/problems/given-a-linked-list-of-0s-1s-and-2s-sort-it/1)
(提示:我用 c++中 stl 的 hashmap 来存储 0，1，2 的计数)

**问题 2:** [给定一只股票你需要找到你能赚到的最大利润](https://practice.geeksforgeeks.org/problems/stock-buy-and-sell/0)。你可以尽可能多次买卖。)

**问题 3:** 用 java 设计一个树集。
(提示:我告诉他使用 BST，但他告诉我要想出更优化的方法，所以我告诉了 AVL，并编写了用于在 AVL 树中插入的函数)
**问题 4:** 方法重载和方法重写之间的区别。java 中什么是静态块？
**问题 5:** 钻取部署描述符、struts、mysql 的问题。

**第 3 轮:个人面试**
面试官看起来很疲惫。他问我既然你是最后一个人那么所有的问题你都会问。告诉我你问了什么问题。我告诉他字符串中有明显的回文子串，LIS、LCS 等同学告诉我你在问。他想了一会儿，让我写标准的 bfs 代码来遍历图。

**问题 2:** 给了你一个字符矩阵和一本字典。你需要找到你能从中获得的有效单词并打印出来。
(提示:我用 dfs 找到了有效序列，并假设所有单词都存储在一个 hashmap 中)
之后，何要求在给定时间内解决 6 个谜题。
谜题 1 : 1.5 只母鸡在 1.5 天内下 1.5 个鸡蛋。6 天需要多少只母鸡吃 4 打鸡蛋。
拼图 2: 2 根绳子，花 1 小时烧好。计算 45 分钟
拼图 3:10 罐，每个罐中有 10 克大理石。一个罐子只装 9 克弹珠。一圈找到有缺陷的罐子。
困惑 4:150 人按排序排队。一个盲人来到
想要在队列中处于正确的位置。所以他问任何人他是否能站在他面前。他会回答是或不是。2Yes 之后你要找对地方。
给出找对地方的策略。
(提示:这个谜题可以简化为落蛋谜题)
谜题 5:25 有比赛的马找到前 3
谜题 6:一个人在骑一辆车，他看到一个里程碑 A，1 小时后他看到一个里程碑 B，这个里程碑 B 的数字与 A 相反，一个小时后他找到一个里程碑 C，这个里程碑 C 包含了 A 和 B 的所有数字，假设 A < B < C 找到了汽车的速度。

(我朋友问的其他问题
1。字符串中的独特回文
2。事务最小化问题
3。LCS 和 LIS (dp 方法)
4。树的直径
5。模式匹配算法(KMP))

**HR 轮:**
他问我家庭背景，我做什么，爱好。我所知道的让我旅行。我更喜欢哪个位置，对套餐是否满意，工作环境等
持续了半个小时。

提示:(有表现力，大声思考，自信。他们需要知道你的方法，而不是解决方案)

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for MakeMyTrip](https://practice.geeksforgeeks.org/company/MakeMyTrip/) !

## 相关实践问题

[N meetings in one room](https://practice.geeksforgeeks.org/problems/n-meetings-in-one-room/0)[Stock buy and sell](https://practice.geeksforgeeks.org/problems/stock-buy-and-sell/0)[Word Boggle](https://practice.geeksforgeeks.org/problems/word-boggle/0)[Distinct palindromic substrings](https://practice.geeksforgeeks.org/problems/distinct-palindromic-substrings/0)[Diameter of Binary Tree](https://practice.geeksforgeeks.org/problems/diameter-of-binary-tree/1)[Longest Prefix Suffix](https://practice.geeksforgeeks.org/problems/longest-prefix-suffix/0)[Power of Numbers](https://practice.geeksforgeeks.org/problems/power-of-numbers/0)[Given a linked list of 0s, 1s and 2s, sort it.](https://practice.geeksforgeeks.org/problems/given-a-linked-list-of-0s-1s-and-2s-sort-it/1)[Longest Common Subsequence](https://practice.geeksforgeeks.org/problems/longest-common-subsequence/0)