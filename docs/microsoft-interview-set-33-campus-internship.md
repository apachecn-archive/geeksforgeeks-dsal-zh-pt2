# 微软面试|第 33 集(校内实习)

> 原文:[https://www . geesforgeks . org/Microsoft-面试-设置-33-校园-实习/](https://www.geeksforgeeks.org/microsoft-interview-set-33-campus-internship/)

最近，微软国际数据中心访问了我们的校园进行实习。我一共打了 6 轮。

**客观轮:-**
客观轮是在 Cocubes.com 拍的，有 15 道题(我的题集中重复了 1 道题)。有一个关于“阵列中的矩形碰撞”的问题，我不知道。

**编码轮次:-**
有两个编码问题:-
1)在排序的数组中找到一个元素，该元素在 O(logn)时间内只在一个位置循环旋转。

2)找到二叉查找树中节点的有序后继节点。
(父指针出现在 BST 中)。(参考[方法 1](https://www.geeksforgeeks.org/inorder-successor-in-binary-search-tree/)

**小组面试回合:-**
前 10 分钟，他问我们期待科技领域的下一件大事是什么。然后他给出了两个问题:-
1)给定一个字符串，你要检查它是不是一个有效的数字。(数字可以是有符号的，浮点/整数)。如果是数字，返回真，否则返回假。
约束条件是:-
i)不允许决策语句(不允许 if-else，不允许切换情况)。
ii)不允许三元条件运算符(？:不允许)。
iii)不允许循环语句(不允许 for/while/do-while)。

(我的解决方案是递归实现，使用关系运算符和两个全局变量返回一个只有一个 return 语句的 bool，一个用于检查它是否是第一个出现的“.”另一个用于检查符号“+”/“-”是否出现在第一个位置)。

2)必应想通过给用户奖励积分来提升用户体验。设计一种算法，为不同的用户分配奖励积分。

**个人面试第一轮:-**
1)给你一个只包含“(”和“)”的字符串，检查字符串是否格式正确，即检查括号是否匹配良好。
(或者计数为“(”或者使用堆栈推送“(”并在遇到“)”时弹出)。

2)有一个原型如下的机器人类:-

```
class Bot {
// private data members
public :
 bool moveleft(); // The bot moves one block left and returns true.
 bool moveright(); // The bot moves one block right and returns true.
 bool movebottom(); // The bot moves one block down and returns true.
 bool movetop(); // The bot moves one block up and returns true.
 bool hasGold(); // returns true if the current position of bot has gold.
};
```

给你一个机器人和一个迷宫的尺寸，这个迷宫有墙壁和一些有金子的方块，检查这个机器人是否能到达一个有金子的方块。

(使用递归实现使用 dfs 图遍历，如果当前位置有黄金，则返回 true，如果不能再移动，则返回 false)。

**个人访谈第二轮:-**
1)给你两个二叉树的根，检查树是否同构。(最初他把问题框定为一棵树(不是二叉树)，给了我两个随机节点，而不是根)。

(参考 https://www.geeksforgeeks.org/tree-isomorphism-problem/)

2)给你一个 n×m 维的数组。你从第(0，0)个位置开始。您可以从(I，j)移动到第(i + 1，j)、(I，j + 1)、(i + 1，j + 1)个位置中的任何一个。找出从第(0，0)个位置到第(I，j)个位置的路径总数。

(对于所有 I 和 j，dp[i][0] = dp[0][j] = 1，DP[I][j]= DP[I–1][j–1]+DP[I][j–1]+DP[I–1][j])。

**个人访谈第三轮:-**
1)给定一个字典，将字谜组合在一起。
(对字典中的每个字符串进行排序，因为排序后字谜将具有相同的表示，所以使用哈希映射来存储字谜组)。
2)他问了与我的项目有关的问题。

谢谢你，geeksforgeeks.org。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[All Practice Problems for Microsoft](https://practice.geeksforgeeks.org/company/Microsoft/) !