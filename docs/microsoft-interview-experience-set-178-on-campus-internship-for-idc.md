# 微软面试体验|第 178 集(IDC 校内实习)

> 原文:[https://www . geesforgeks . org/Microsoft-面试-体验-设置-178-校园-实习-for-idc/](https://www.geeksforgeeks.org/microsoft-interview-experience-set-178-on-campus-internship-for-idc/)

总共有 3 轮。第一轮是在线编码，第二轮是书面编码，最后一轮分为三部分，基本上是 3 次技术面试。

**第一轮:**

**科考网上考试包含 3 道编码题(仅功能完成)。给出的总时间是 75 分钟。**

1.  求字符串中所有字符的 ASCII 值之和的平均值。
    例:

```
Input : swati
Output :110.4

LOGIC:  (115+119+97+116+105)/5= 110.4 
```

[GeeksforGeeks Link](https://www.geeksforgeeks.org/average-of-ascii-values-of-characters-of-a-given-string/)

*   Evaluate the value of an infix string. The string will not have any spaces or brackets and priority of ‘*’ and ‘/’ is greater then the priority of ‘+’ & ‘-‘ .

    示例:

    ```
    Input : 5+10/2*6-3
    Output :32

    LOGIC: 5+5*6-3 = 5+30-3 = 35-3 = 32
    ```

    [GeeksforGeeks Link](https://www.geeksforgeeks.org/expression-evaluation/)

    *   Given a BST, a min value and a max value, delete the nodes of the BST having data smaller than min value and greater than max value.
    Example:

    ```
    Input :
                        10/ \              8           13/ / \         2           11        15最小值= 3 最大值= 13 输出:                   10/ \              8      13/                11
    ```

    [GeeksforGeeks Link](https://www.geeksforgeeks.org/remove-bst-keys-outside-the-given-range/)

    网上一轮很容易，因为他们在看学生的基本概念是否清楚。共有 109 名学生参加了在线考试，其中 31 人有资格参加下一轮考试。

    **第二轮:**

    **笔试 2 题，总时间 45 分钟。**

    1.  Given an array and a key you need to rotate the array elements ‘key’ times.
        Example:

        ```
        Input 1:  arr[]= [1, 2, 3, 4, 5, 6]

        key=2

        Output : [ 3, 4, 5, 6, 1, 2]

        Input 2 : arr[]= [1, 2, 3, 4, 5, 6]

        key=24
        Output : [1, 2, 3, 4, 5, 6] 
        ```

        [GeeksforGeeks Link](https://www.geeksforgeeks.org/array-rotation/)

    2.  给定一个字符串，你需要按照字典顺序打印它的所有子字符串
        。
        示例:

    ```
    Input :  ABC
    Output : A AB ABC AC ACB B BA BAC BC BCA C CA CB CAB CBA 
    ```

    [GeeksforGeeks Link](https://www.geeksforgeeks.org/generating-distinct-subsequences-of-a-given-string-in-lexicographic-order/)

写很多评论，让你的程序越来越易读。确保您的工作整洁，并尝试编写优化程度最高、占用空间最少的代码。但是如果优化后的代码没有打动你，那就写你能想到的逻辑。这一轮之后，14 名学生被选入第三轮。

**第三轮:**

**本轮共分 3 场技术面试。**

**技术面试 1:**

*   **主观题:**
    1.  如何实现虚拟析构函数？
    2.  遍历数组和链表哪个更好？
    3.  递归和函数循环有什么区别？
    4.  您认为在 MS Word 中可以添加或修改哪些功能？
    5.  堆栈的实际用途。
*   **编码问题:**
    1.  [给定一个十进制数，将其转换为等价的罗马数字](https://www.geeksforgeeks.org/converting-decimal-number-lying-between-1-to-3999-to-roman-numerals/)。
    2.  [给定数组中的前 n 个自然数，就说少了一个数。写代码找缺失的号码](https://www.geeksforgeeks.org/find-the-missing-number/)。
    3.  [给定数组中的前 n 个自然数，现在说少了两个数。写一个代码找到缺失的数字](https://www.geeksforgeeks.org/find-two-missing-numbers-set-1-an-interesting-linear-time-solution/)。

当我从 OOPs 得到我的第一个问题时，我告诉面试官我还没有研究 OOPs，并要求他从数据结构中提问。最后他问我有没有问题要问他，我就让他把我作为他们公司的候选人来回顾一下，哪些概念需要学习和改进。除了这些问题之外，我们还讨论了我的大学，以及他想给所有渴望在任何跨国公司(不一定只有微软)从事技术工作的学生什么建议。

**技术面试 2:**

*   **一般问题:**
    1.  微软为什么要聘用你？你和其他入围面试的候选人有什么不同？
    2.  他询问了我的暑期实习和我在简历中提到的项目。
    3.  询问堆栈、队列和链接列表的区别，以及哪个更好。
*   **编码问题:**
    1.  给定一个字符串列表，找出由列表中其他字符串组合而成的最大长度字符串。

        ```
        Input :[Information, Technology, Batchof2020, 
        InformationTechnology, Batchof2020InformationInternship]

        Output : InformationTechnology

        Note:"Batchof2020InformationInternship" is the longest string 
        but its has a sub string Internship which
         is not a string in the given list, hence its not the output.

        ```

**技术面试 3:**

这一轮面试，面试官把我的整个简历都彻底看了一遍，问我的爱好，其中辩论是最突出的一个。所以他和我就一个好演讲者的角色进行了一场伪辩论和讨论。

之后我们玩了一个猜字游戏，我不记得游戏的名字了。他基本上给我解释了游戏，告诉了我所有的规则。玩完游戏后，他告诉我写游戏的代码，这将是我今天的最后一个问题。我在 4-5 分钟内写好了代码。他似乎对代码很满意，并祝我好运！

这是选拔过程的结束，大约 10 分钟后，我被告知我被选中了😀

这是我的第一次面试经历，我被选中了！10 个小时的漫长过程结束了，给了我一生中最好的机会。

本文由 Swati Bararia 供稿。