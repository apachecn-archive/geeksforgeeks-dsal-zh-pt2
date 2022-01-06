# 使用 STL 对字符串进行字典排序

> 原文:[https://www . geesforgeks . org/词典-rank-string-using-stl/](https://www.geeksforgeeks.org/lexicographic-rank-string-using-stl/)

给你一个字符串，找出它在所有排列中的排列顺序。

**例:**

```
Input : str[] = "acb"
Output : Rank = 2

Input : str[] = "string"
Output : Rank = 598

Input : str[] = "cba"
Output : Rank = 6

```

我们已经讨论了寻找[字符串字典排序](https://www.geeksforgeeks.org/lexicographic-rank-of-a-string/)的解决方案

在这篇文章中，我们使用 STL 函数“next _ 置换()”来生成给定字符串的所有可能的置换，并且，由于它以字典顺序给我们置换，我们将放置一个迭代器来找到每个字符串的秩。当我们的置换字符串变得与原始输入字符串相同时进行迭代，我们脱离循环，最后一次迭代的迭代器值就是我们需要的结果。

```
// C++ program to print rank of 
// string using next_permute()
#include <bits/stdc++.h>
using namespace std;

// Function to print rank of string
// using next_permute()
int findRank(string str)
{
    // store original string
    string orgStr = str;

    // Sort the string in lexicographically
    // ascending order
    sort(str.begin(), str.end());

    // Keep iterating until
    // we reach equality condition
    long int i = 1;
    do {
        // check for nth iteration
        if (str == orgStr)
            break;

        i++;
    } while (next_permutation(str.begin(), str.end()));

    // return iterator value
    return i;
}

// Driver code
int main()
{
    string str = "GEEKS";
    cout << findRank(str);
    return 0;
}
```

输出:

```
25

```

本文由**[Shivam Pradhan(anuj _ charm)](https://www.linkedin.com/in/imanuj/)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。