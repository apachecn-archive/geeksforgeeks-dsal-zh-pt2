# 微软面试体验集 127 |(IDC 校内)

> 原文:[https://www . geesforgeks . org/Microsoft-面试-体验-设置-127-校园-idc/](https://www.geeksforgeeks.org/microsoft-interview-experience-set-127-campus-idc/)

**第 1 轮–在线评估**
**平台–**cocubes.com
**时长–**75 分钟
**格式–**3 道编码题
**最高分–**10 分
本次考试共出现约 120 名学生。问题是随机的，所有学生都有不同的问题集，有一些重叠的问题。

**1。完成以下功能-**

```
 int findMax(TreeNode arr[], int size_of_array){
    // code goes here
}

```

其中，树节点是一种结构，定义为:

```
struct TreeNode{
   int feet;
   int inches;
}; 

```

该函数应该返回树节点的最大值。这应该通过计算每个元素(12 *英尺+英寸)来完成。它由两个标记组成。

**2。完成以下功能-**

```
Node * findIntersection( Node* head1, Node*head2){
   // code goes here
}

```

其中“节点”是链接列表节点的结构，定义为:

```
struct Node{
  int data;
  struct Node *next;
}; 

```

代码应该递归地找到两个链表(已经排序)之间的交集，条件是不使用额外的空间。这个问题得了 3 分。
例:

```
Input-
1->2->14->15->26
2->10->14->16->18->26->32
Output-
2->14->26

```

**3。完成以下功能-**

```
Node * alternateReverse( Node* head1, Node*head2){
   // code goes here
}

```

其中“节点”是链接列表节点的结构，定义为:

```
struct Node{
  int data;
  struct Node *next;
}; 

```

alternateReverse()必须从链表中删除偶数个节点，并以相反的顺序将它们追加到末尾。不允许有额外的空间。是 5 马克。
例:

```
Input-1->2->3->4->5->6
Output-1->3->5->6->4->2

Input-1->2->3->4->5->6->7->8->9
Output-1->3->5->7->9->8->6->4->2

```

**第 2 轮–团体飞行**
约 40 名学生入围这一轮。这是一个基于纸笔的测试。候选人大致分为 4-5 人一组，每组由一名导师负责。给了我们一个问题，我们被要求用任何高级语言编写一个函数解决方案(不允许使用像 Ruby、PHP、Python 这样的脚本语言)。我们被分配了最多 45 分钟。

**问题-** 给定两个长度相同的字符数组(不是字符串)，并将它们的长度作为函数的参数。我们必须找出第一根弦是否是另一根弦的旋转。我们不应该使用任何额外的空间。时间复杂度可能是二次的。

导师不停地向大家走来。他先问我在想什么。我用一个例子告诉他方法，然后写下我的代码。导师们给予了帮助和激励。他们只要求代码。

**第三轮-技术面试**
约有 25 名学生入选本轮。
面试官自我介绍了一下，然后让我给她讲讲我自己。然后她让我从一串字符串中找出最长的公共前缀。我们讨论了一种方法，然后我不得不把它编码下来。她还问我时间复杂度，然后让我优化它。我给出了另一种方法，然后她让我对它进行编码并给出时间复杂度。我们用新的方法进一步优化了解决方案，我也对其进行了编码。面试官很满意。
[https://www . geesforgeks . org/long-common-prefix-set-1-word-by-word-matching/](https://www.geeksforgeeks.org/longest-common-prefix-set-1-word-by-word-matching/)
她最后问我有没有问题要问她？我问了她一个问题。面试持续了大约 1 小时 10 分钟。

**第 4 轮——技术面试**
面试官介绍了他，然后我就介绍了。他给了我两个问题-

*   检查给定的二叉树是否是 BST。讨论了不同的方法。对其中一个进行了编码。
    [https://www . geeksforgeeks . org/a-program-to-check-if-a-binary-tree-is-BST-or-not/](https://www.geeksforgeeks.org/a-program-to-check-if-a-binary-tree-is-bst-or-not/)
*   使用使用堆栈实现。我们讨论了方法，优化了操作，然后对它们进行了编码。[https://www.geeksforgeeks.org/queue-using-stacks/](https://www.geeksforgeeks.org/queue-using-stacks/)

他问我有没有问题要问他？我也问过他一个。采访持续了大约 45 分钟。

**第 5 轮–HR 面试**
面试官在微软有 20 多年的工作经验。他做了自我介绍，问我有没有问题要问他。然后我们讨论了大约 20 分钟我简历中的成就和责任职位。

*   然后他让我实施 Akinator 游戏。我们讨论了如何开始，会有什么问题，数据库会是什么样的，如何选择下一个问题，为什么选择它，等等。讨论持续了大约 30 分钟。他最初提到这个问题没有正确或错误的答案，他只是想看看我的思维过程是如何运作的。我们都在大声讨论和思考。[秋官](https://en.wikipedia.org/wiki/Akinator)
*   然后他问了我一个谜题。如果我有 10 个球，1 个球的重量稍轻，我有一个重量平衡，找到“坏球”所需的最小比较次数是多少？我们讨论了 10 个球和 9 个球的解决方案。我当时应该概括解决方案。

面试持续了大约 1 小时。第二天他们公布了结果，选出了 5 名学生。

如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。