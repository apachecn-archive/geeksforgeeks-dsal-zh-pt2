# 微软面试体验|第 76 集(校内)

> 原文:[https://www . geesforgeks . org/Microsoft-面试-体验-设置-校园 76/](https://www.geeksforgeeks.org/microsoft-interview-experience-set-76-on-campus/)

最近微软来我们校园招聘，下面是我的面试经历。

**MCQ 回合-**
15 道 MCQ 题来自 C、C++、java (1 道题)、aptitute 等关于 cocubes.com 的题目。没有负面标记。很少有学生在这一轮被淘汰。

 **编码回合–**

**2 个编码问题–**

Q1。给你一个 M×N 大小的矩阵，矩阵中唯一可能的值是
0？代表空位置
1？代表一个新鲜的苹果
2？代表一个腐烂的苹果
一个腐烂的苹果在 1 个单位的时间内将所有的新鲜苹果转化为与其相邻的腐烂苹果。给定一个输入矩阵，你必须计算出所有新鲜苹果腐烂的时间。还要确定是否所有的新鲜苹果都能在有限的时间内腐烂。(10 分)

```
Input
2 1 0 2 1
1 0 1 2 1
1 0 0 2 1

After 1 time unit, the matrix will be transformed to
2 2 0 2 2
2 0 2 2 2
1 0 0 2 2

After 2 time units the matrix will look like
2 2 0 2 2
2 0 2 2 2
2 0 0 2 2
```

因此输出应该是 2 个时间单位。(相邻的定义只包括左、右、下、上单元格，不包括对角线单元格)
Q2。在二叉树中查找与给定节点相距 k 距离的所有节点–https://www . geeksforgeeks . org/print-nodes-distance-k-leaf-node/。(10 分)

有些学生是微软信息技术的简称，有些是微软国际数据中心的，有些是两者兼而有之的。

对部分学生进行了小组复飞，部分学生直接被选中进行面试。

 **团体复飞–**

对于微软 IDC–从输入字符串中删除所有重复项 https://www . geesforgeks . org/从输入字符串中删除所有重复项/
对于微软 IT–设计名称、角色和权限系统，其中每当用户输入其角色和名称时，将输出授予他的权限(读、写或执行)。

 **面试 1–**

1.说说你自己吧。
2。一个文件里有 100 万字。在文件中找出 10 个最常见的单词。[https://www . geeksforgeeks . org/从文件中找到最常用的单词/](https://www.geeksforgeeks.org/find-the-k-most-frequent-words-from-a-file/)

我用 trie 和 min heap 给出了解决方案。他让我编写程序，假设 trie 和 heap 的插入和删除是给定的。
然后他问我什么应该是测试用例。
以下是测试用例–
a)如果文件包含一个像“abc def”这样用引号括起来的单词。这里“abc def”应该被认为是一个单独的词，但是我的程序将“abc def”视为两个不同的词–(I)“ABC(ii)def”。
b)如果文件包含 tab (t)、r 等字符。那么我的程序就不能工作了。
3。基于虚拟记忆概念的几个问题？
4。写出任意 6 种排序算法的名称和平均运行时间复杂度。
5。什么时候应该使用合并排序？
6。有关于微软的问题吗？

 **访谈 2–**

1.找到第一个参观所有加油站的循环游-https://www . geeksforgeeks . org/find-a-tour-参观所有加油站/。
首先我给出了一个蛮力解。从每一个汽油泵开始，检查是否可以进行循环旅行。这个解决方案需要 O(n^2)时间复杂度然后他问我优化的解决方案。
我无法优化，但当他给出一些提示时，我给出了 O(n)解。之后他问了关于运行时间复杂性的问题，然后他让我编码。
2。关系表中的索引有什么用？
3。如果联接应用于两个表——表 1 和表 2。假设表 1 的行数比表 2 多，那么表 1 连接表 2 需要更多的时间来执行，或者表 2 连接表 1 需要更多的时间来执行？(假设两个表中都没有索引)

3.基于我的项目的一些问题。
4。你对哪种技术有热情？
5。有关于微软的问题吗？

 **采访 3–**

1.你喜欢链表吗？
我说好，然后他从链表问了两个问题。
2。用下一个随机指针克隆一个链表。
3。用下一个随机指针序列化和描述一个链表。
序列化和描述链表意味着将链表保存在一个文件中，然后使用该文件再次生成相同的链表。
首先我给了 O(n^2)运行时间解决方案，然后他要求优化。然后我用散列法给出了运行时间的解。
每当我陷入困境时，他都在给我暗示。

 **面试 4(HR)–**

1.微软为什么要聘用你？
2。今年夏天你做了什么？
3。基于我的项目的一些问题。
4。从给定的有序和预有序遍历构造二叉树。[https://www . geeksforgeeks . org/construct-tree-from-given-order-and-preorder-traverse/](https://www.geeksforgeeks.org/construct-tree-from-given-inorder-and-preorder-traversal/)
5。有关于微软的问题吗？

在采访中，他们给了我足够的时间思考解决方案，每当我陷入困境时，他们都会提供帮助。

我准备安置的主要来源是 GeeksForGeeks。几乎所有轮问的问题都在 GeeksForGeeks 里。我非常感谢 GeeksForGeeks 为安置准备工作提供了非常好的材料。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

## 相关实践问题

[Node at distance](https://practice.geeksforgeeks.org/problems/node-at-distance/1)[Construct Tree from Inorder & Preorder](https://practice.geeksforgeeks.org/problems/construct-tree-1/1)[Circular tour](https://practice.geeksforgeeks.org/problems/circular-tour/1)[Rotten Oranges](https://practice.geeksforgeeks.org/problems/rotten-oranges/0)[All Practice Problems for Microsoft](https://practice.geeksforgeeks.org/company/Microsoft/) !