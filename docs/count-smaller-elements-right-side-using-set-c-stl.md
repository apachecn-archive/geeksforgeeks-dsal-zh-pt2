# 使用 C++ STL 中的 Set 计算右侧较小的元素

> 原文:[https://www . geesforgeks . org/count-small-elements-right-side-use-set-c-STL/](https://www.geeksforgeeks.org/count-smaller-elements-right-side-using-set-c-stl/)

编写一个函数来计算数组中每个元素右边较小元素的数量。给定一个不同整数的未排序数组 arr[]，构造另一个 count small[]，使得 count small[I]包含数组中每个元素 arr[i]右侧较小元素的计数。
示例:

```
Input : arr[] =  {12, 1, 2, 3, 0, 11, 4}
Output :countSmaller[]  =  {6, 1, 1, 1, 0, 1, 0} 

Input :arr[]={5, 4, 3, 2, 1}
Output :countSmaller[]={4, 3, 2, 1, 0}
```

本文讨论了[的一个简单实现。
在](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side/) [C++ STL](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) 中创建一个空的[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)(注意 C++ STL 中的集合是通过自平衡二叉查找树实现的)。

1.  从 i=len-1 到 0 遍历数组元素，并插入集合中的每个元素。
2.  用下界函数求第一个低于 A[i]的元素。
3.  使用距离函数找出上面找到的元素和集合开头之间的距离。
4.  将距离存储在另一个数组中让我们假设 CountSmaller。
5.  打印那个数组。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find count of smaller
// elements on right side using set in C++
// STL.
#include <bits/stdc++.h>
using namespace std;
void countSmallerRight(int A[], int len)
{
    set<int> s;
    int countSmaller[len];
    for (int i = len - 1; i >= 0; i--) {
        s.insert(A[i]);
        auto it = s.lower_bound(A[i]);
        countSmaller[i] = distance(s.begin(), it);
    }

    for (int i = 0; i < len; i++)
        cout << countSmaller[i] << " ";
}

// Driver code
int main()
{
    int A[] = {12, 1, 2, 3, 0, 11, 4};
    int len = sizeof(A) / sizeof(int);
    countSmallerRight(A, len);
    return 0;
}
```

**Output**

```
6 1 1 1 0 1 0 
```