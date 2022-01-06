# 两个以上(或数组)数 GCD 的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-program-for-gcd-of-two-or-array-numbers/](https://www.geeksforgeeks.org/cpp-program-for-gcd-of-more-than-two-or-array-numbers/)

三个或三个以上数的 GCD 等于所有数共有的质因数的乘积，但也可以通过重复取数对的 GCD 来计算。

```
gcd(a, b, c) = gcd(a, gcd(b, c)) 
             = gcd(gcd(a, b), c) 
             = gcd(gcd(a, c), b)

```

```
// C++ program to find GCD of two or
// more numbers
#include <bits/stdc++.h>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to find gcd of array of
// numbers
int findGCD(int arr[], int n)
{
    int result = arr[0];
    for (int i = 1; i < n; i++)
        result = gcd(arr[i], result);

    return result;
}

// Driven code
int main()
{
    int arr[] = { 2, 4, 6, 8, 16 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findGCD(arr, n) << endl;
    return 0;
}
```

**Output:**

```
2

```

更多详情请参考完整的两个以上(或数组)数字的 [GCD 文章！](https://www.geeksforgeeks.org/gcd-two-array-numbers/)