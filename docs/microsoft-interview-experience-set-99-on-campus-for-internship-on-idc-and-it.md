# 微软面试体验|设置 100(在校内进行 IDC 和 IT 实习)

> 原文:[https://www . geesforgeks . org/Microsoft-面试-体验-设置-99-校园实习-IDC-on-and-it/](https://www.geeksforgeeks.org/microsoft-interview-experience-set-99-on-campus-for-internship-on-idc-and-it/)

微软参观了我们的校园，在国际数据中心和信息技术档案实习选择。国际数据中心简介的选择过程有三轮

**第一轮:编码轮**
分 3 套提问。其中解决 2 个及以上的人入围。解决 3 个问题的人入围个人面试，解决 2 个问题的人入围团体复飞。

**问题为:**

1.  你将被给予一定高度的建筑，这些建筑彼此相邻。太阳开始从左侧落下。如果有一定高度的建筑物，它右边所有高度较小的建筑物都看不到太阳。你需要找到接收阳光的这类建筑的总数。
    求以第一栋楼为起始楼的递增子序列(不严格)。
    T2 解决方案:[极客论坛链接](https://www.geeksforgeeks.org/number-buildings-facing-sun/)
2.  You will be given two arrays of equal size and you need to maximize the first array with the second array elements ( swap the first array elements with second array elements . Once swapped , you cannot use the element anymore )

    ```
    For ex: A: 3 4 6 8 9 and A : 5 7 3 6 8

    B : 6 7 8 8 9 B : 3 4 6 9 10

    Op: 9 8 8 8 9 Op : 10 9 6 6 8

    ```

    **解决方案**:[geeks forges Link](https://www.geeksforgeeks.org/maximize-elements-using-another-array/)
    对第二个数组进行排序，如果 a[i] < b[i]，则开始交换。否则等待下一个小于 b[i]的 a 元素并交换(简单合并过程)

3.  你会得到两棵树 t1 和 t2。你需要检查[T2 是否是 t1](https://www.geeksforgeeks.org/check-if-a-binary-tree-is-subtree-of-another-binary-tree/) 的子树。如果是子树，需要返回 t2 的大小(其中的节点数)。
    如果 t1 或 T2 为空，返回-1。
    如果 t2 不是 t1 的子树，那么也返回-1

Most Efficient Solution was :
Any Tree has  2 unique traversals . ( Either it be (preorder,inoder) ,( in,post) ,(post,pre) ) . So , Traverse them and store any two traversals for both the trees  Check first traversal of both trees ([String Matching using KMP](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/) O(N+M) ) and similarly for the second traversal.If they both come out to be true ( I mean pattern exists in text ). Then you are done . Else return -1
This Complexity is O(N+M) and space O(N+M) . If you want to do without space , Try for the recursive approach which in worst case takes O(N*M) complexity

显然，我入围了个人面试，所以我没有参加团体复飞。

**Personal Interview  rounds ****1st round(Technical ) :   **Interviewer was bit cool and asked me questions directly

1.  [求未排序数组的中位数](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)。我告诉他按照 N(偶数或奇数)的奇偶性来排序和查找。NLogN 解决方案。他让我优化一下。然后我告诉他最坏情况下 O(N)方法的未排序数组的中值…(你可以在 gfg 中找到)。他问我是否可以使用快速选择..我告诉了他这样做的方法，并建议他最坏的情况可能会发生在 O(N^2。他告诉我没关系，让我写代码。我的代码有点乏味，但我最终能够得到正确的代码。
2.  然后他问我关于[散列](https://www.geeksforgeeks.org/hashing-set-1-introduction/)(链接和开放寻址-插入、删除等)和 [c++映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)及其复杂性

**2nd Round(Technical) **Interviewer was very cool and asked me questions regarding my project and I explained him briefly .Then he asked me coding questions .

1.  您将得到一个未排序的数组，其中任何元素都可以重复任意次。元素范围是>大小。n 太高了(10^7)。所以，我给了他 O(N)时间和 O(N)空间哈希解决方案，使用无序 _ 映射解决方案。他很满意。
2.  接下来的问题是[验证一个日期，使其采用预期的格式](https://www.geeksforgeeks.org/java-date-format-validation-using-regex/)，并且应该比当前日期少 20 年。如果异常无效，需要抛出异常。首先，我遇到了所有可能的异常，然后我编写了一个接受方法。他让我写代码。这次我写了一个干净的代码，涵盖了所有可能的异常。他很满意。并告诉我，这些技术回合的座右铭是检查我们是否能写出正确的代码，能否掌握基本知识，并分析我们在其中的优势。

**第三轮(HR 轮)**

经理非常非常冷静，问了我一些问题，比如。你为什么想加入微软？为什么我们要雇佣你和我相关的东西，他让我来解决这个问题。[求多数元素](https://www.geeksforgeeks.org/majority-element/)(在一个数组中重复(N/2)次以上的元素。如果不存在，返回-1。我告诉他使用摩尔投票算法在 O(N)时间和 O(1)空间内解决问题的方法。经过这几轮之后，我获得了国际数据公司实习的机会。

虽然我也被选入了高尔夫面试，但我不得不接受这个邀请，我没有参加高尔夫个人面试。

**感谢 GeeksforGeeks 在****[practice.geeksforgeeks.org](https://practice.geeksforgeeks.org/)的帮助下，帮我修改了所有的概念并进行练习。**我在实习生之前的最后 15 天完全花在了解决问题和在 GeeksforGeeks 中修改问题上。

非常感谢团队！！
如果你喜欢 GeeksforGeeks 并想投稿，你也可以写一篇文章，把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论

[All Practice Problems for Microsoft](https://practice.geeksforgeeks.org/company/Microsoft/) !