# 给定两个数组所有索引前缀和的最大差值

> 原文:[https://www . geesforgeks . org/给定两个数组的所有索引的前缀和的最大差值/](https://www.geeksforgeeks.org/maximum-difference-of-prefix-sum-for-all-indices-of-given-two-arrays/)

给定两个整数**a【】**和**s【】**的数组,两个数组的大小均为 **N** 。任务是为给定数组的所有索引找到 [**前缀和**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 的最大差值。

**示例:**

> **输入:** N = 5，a[] = {20，20，35，20，35}，s[] = {21，31，34，41，14}
> **输出:** 32
> **解释:**前缀和后的数组是 a[] = {20，40，75，95，130}
> 和 b[] = {21，52，86，127，141}
> 
> **输入:** N = 1，a[] = {32}，s[] = {15}
> **输出:** A，17
> **说明:**最大差异(因为只有一个元素)是 32–15 = 17。

**方法:**这个问题可以通过计算两个数组中的前缀和，然后比较每个索引的差异来解决。按照以下步骤解决问题:

*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，n)** ，并计算两个数组的前缀和。
*   计算每个索引的前缀和之差。
*   返回最大差值。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the winner
int getWinner(int a[], int s[], int N)
{
    int maxDiff = abs(a[0] - s[0]);

    // Calculating prefix sum
    for (int i = 1; i < N; i++) {
        a[i] += a[i - 1];
        s[i] += s[i - 1];
        maxDiff = max(maxDiff, 
                      abs(a[i] - s[i]));
    }

    // Return the result
    return maxDiff;
}

// Driver Code
int main()
{
    int N = 5;

    int a[] = { 20, 20, 35, 20, 35 },
        s[] = { 21, 31, 34, 41, 14 };

    cout << getWinner(a, s, N);
    return 0;
}
```

**Output**

```
32
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)