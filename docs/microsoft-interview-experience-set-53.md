# 微软面试体验|第 53 集

> 原文:[https://www . geesforgeks . org/Microsoft-面试-体验-set-53/](https://www.geeksforgeeks.org/microsoft-interview-experience-set-53/)

**第 0 轮–**
英国标准时间第二大元素

对整数数组进行排序，使–T0–所有奇数都在左侧，并按升序排序。
–所有偶数按降序排序，从奇数结束的地方开始。
例如–
仪表板–2、3、4、5、8、10、12、11
仪表板–3、5、11、12、10、8、4、2

我使用快速排序分区逻辑来分离奇数和偶数，然后对这两部分运行快速排序。

**第 1 轮–**
假设内存大小为 1024 字节。系统上运行着多个进程。您的应用程序将获得此信息–
(线程标识、内存块、时间、读/写)–它实际上告诉线程 T 在时间 T 正在使用内存块 M，并且操作可以是读或写。

记忆冲突定义为–
–让 x 作为时间测量的标准单位。
–同一位置的多次读取操作不会导致冲突。
–在 x+5 到 x-5 到位置 M 之间的一次写操作，将是线程在时间 x 访问位置 M 的冲突原因。
–示例–如果线程 T1 在时间 x+1 访问内存位置 M，并且如果线程 T2 在时间 x+6 之前访问位置 M，那么给定一个写操作，那么 T1 和 T2 是冲突的候选。

给你一个访问内存位置的线程列表，你必须找到冲突。

示例–
(1，512，1，R)
(2，432，2，W)
(3，512，3，R)
(4，932，4，R)
(5，512，5，W)
(6，932，6，R)
(7，835，7，R)
(8，432，8，R)

o/P–
线程 1 & 3 与线程 5
冲突，所有其他操作都是安全的。

**第二轮–**
[https://www.geeksforgeeks.org/turn-an-image-by-90-degree/](https://www.geeksforgeeks.org/turn-an-image-by-90-degree/)

层级顺序遍历->
使用队列
使用递归

**第 3 轮–**
[http://stackoverflow . com/questions/746082/如何从字母矩阵中找到可能的单词列表-boggle-solver](http://stackoverflow.com/questions/746082/how-to-find-list-of-possible-words-from-a-letter-matrix-boggle-solver)
>我的解决方案是突变这个–[https://www . geeksforgeeks . org/mobile-数字键-problem/](https://www.geeksforgeeks.org/mobile-numeric-keypad-problem/)

**第 4 轮–**
3D 博格解算器和 3D 交叉词解算器。
设计数据结构存储并给出解决方案。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for Microsoft](https://practice.geeksforgeeks.org/company/Microsoft/) !