# 基本欧几里德算法的 C 程序

> 原文:[https://www . geesforgeks . org/c-program-for-basic-and-extended-euclidean-algorithms/](https://www.geeksforgeeks.org/c-program-for-basic-and-extended-euclidean-algorithms/)

两个数的 GCD 是除两个数的最大数。找到 GCD 的一个简单方法是分解两个数字并乘以公共因子。

## C

```
// C program to demonstrate Basic Euclidean Algorithm
#include <stdio.h>

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Driver program to test above function
int main()
{
    int a = 10, b = 15;
    printf("GCD(%d, %d) = %d\n", a, b, gcd(a, b));
    a = 35, b = 10;
    printf("GCD(%d, %d) = %d\n", a, b, gcd(a, b));
    a = 31, b = 2;
    printf("GCD(%d, %d) = %d\n", a, b, gcd(a, b));
    return 0;
}
```

**Output:** 

```
GCD(10, 15) = 5
GCD(35, 10) = 5
GCD(31, 2) = 1
```

**时间复杂度:** O(对数最小值(a，b))

**辅助空间:** O(1)
更多详情请参考[基础与扩展欧氏算法](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)完整文章！