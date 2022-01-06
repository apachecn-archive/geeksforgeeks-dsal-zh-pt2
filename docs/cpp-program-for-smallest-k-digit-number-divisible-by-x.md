# 可被 X 整除的最小 K 位数的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-program-for-minist-k-digit-number-除尽-x/](https://www.geeksforgeeks.org/cpp-program-for-smallest-k-digit-number-divisible-by-x/)

给出了整数 X 和 K。任务是找到能被 x 整除的最小 K 位数。

示例:

```
Input : X = 83, K = 5
Output : 10043
10040 is the smallest 5 digit
number that is multiple of 83.

Input : X = 5, K = 2
Output : 10
```

一个有效的解决方案是:

```
Compute MIN : smallest K-digit number (1000...K-times)
If, MIN % X is 0, ans = MIN
else, ans = (MIN + X) - ((MIN + X) % X))
This is because there will be a number in 
range [MIN...MIN+X] divisible by X.

```

```
// CPP code to find smallest K-digit number
// divisible by X
#include <bits/stdc++.h>
using namespace std;

// Function to compute the result
int answer(int X, int K)
{
    // Computing MIN
    int MIN = pow(10, K - 1);

    // MIN is the result
    if (MIN % X == 0)
        return MIN;

    // returning ans
    return ((MIN + X) - ((MIN + X) % X));
}

// Driver
int main()
{
    // Number whose divisible is to be found
    int X = 83;

    // Max K-digit divisible is to be found
    int K = 5;

    cout << answer(X, K);
}
```

**Output:**

```
10043

```

详情请参考[最小可被 X 整除的 K 位数](https://www.geeksforgeeks.org/smallest-k-digit-number-divisible-x/)整篇文章！