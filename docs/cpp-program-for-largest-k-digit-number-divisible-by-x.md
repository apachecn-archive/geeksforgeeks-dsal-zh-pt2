# 可被 X 整除的最大 K 位数的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-program-for-maximum-k 位数-可被 x 整除/](https://www.geeksforgeeks.org/cpp-program-for-largest-k-digit-number-divisible-by-x/)

给出了整数 X 和 K。任务是找到能被 x 整除的最高 K 位数。

示例:

```
Input : X = 30, K = 3
Output : 990
990 is the largest three digit 
number divisible by 30.

Input : X = 7, K = 2
Output : 98

```

一个**有效的解决方案**是使用下面的公式。

```
ans = MAX - (MAX % X)
where MAX is the largest K digit 
number which is  999...K-times
```

这个公式适用于简单的学校方法划分。我们去掉余数得到最大的可除数。

```
// CPP code to find highest K-digit number divisible by X
#include <bits/stdc++.h>
using namespace std;

// Function to compute the result
int answer(int X, int K)
{
    // Computing MAX
    int MAX = pow(10, K) - 1;

    // returning ans
    return (MAX - (MAX % X));
}

// Driver
int main()
{
    // Number whose divisible is to be found
    int X = 30;

    // Max K-digit divisible is to be found
    int K = 3;

    cout << answer(X, K);
}
```

**Output:**

```
990

```

更多详情请参考[整篇文章最大 K 位数可被 X 整除](https://www.geeksforgeeks.org/largest-k-digit-number-divisible-x/)！