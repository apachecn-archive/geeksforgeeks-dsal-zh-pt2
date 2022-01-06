# 使阵列的 GCD 等于 1 所需的最小删除量

> 原文:[https://www . geeksforgeeks . org/最小-删除-要求使阵列 gcd 等于 1/](https://www.geeksforgeeks.org/minimum-deletions-required-to-make-gcd-of-the-array-equal-to-1/)

给定一个由 **N** 个整数组成的数组**arr【】**，任务是找到使结果数组元素的 GCD 等于 **1** 所需的最小删除量。如果不可能，则打印 **-1** 。
**举例:**

> **输入:** arr[] = {2，4，6，3}
> **输出:** 0
> 很明显 GCD(2，4，6，3) = 1
> 所以，我们不需要删除任何元素。
> **输入:** arr[] = {8，14，16，26}
> **输出:** -1
> 无论删除多少元素，gcd 永远不会是 1。

**方法:**如果初始数组的 GCD 是 1，那么我们不需要删除任何元素，结果将是 0。如果 GCD 不是 1，那么不管我们删除什么元素，GCD 永远不会是 1。假设 **gcd** 是数组元素的 gcd，我们删除 **k** 元素。现在，剩下**N–k**元素，它们仍然以 **gcd** 为因子。所以，不可能得到数组元素的 GCD 等于 **1** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// deletions required
int MinDeletion(int a[], int n)
{

    // To store the GCD of the array
    int gcd = 0;
    for (int i = 0; i < n; i++)
        gcd = __gcd(gcd, a[i]);

    // GCD cannot be 1
    if (gcd > 1)
        return -1;

    // GCD of the elements is already 1
    else
        return 0;
}

// Driver code
int main()
{
    int a[] = { 3, 6, 12, 81, 9 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << MinDeletion(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

    // Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0)
        return b;
        if (b == 0)
        return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

    // Function to return the minimum
    // deletions required
    static int MinDeletion(int a[], int n)
    {

        // To store the GCD of the array
        int gcd = 0;
        for (int i = 0; i < n; i++)
            gcd = __gcd(gcd, a[i]);

        // GCD cannot be 1
        if (gcd > 1)
            return -1;

        // GCD of the elements is already 1
        else
            return 0;
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[] = { 3, 6, 12, 81, 9 };
        int n = a.length;

        System.out.print(MinDeletion(a, n));
    }
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd

# Function to return the minimum
# deletions required
def MinDeletion(a, n) :

    # To store the GCD of the array
    __gcd = 0;
    for i in range(n) :
        __gcd = gcd(__gcd, a[i]);

    # GCD cannot be 1
    if (__gcd > 1) :
        return -1;

    # GCD of the elements is already 1
    else :
        return 0;

# Driver code
if __name__ == "__main__" :

    a = [ 3, 6, 12, 81, 9 ];
    n = len(a)

    print(MinDeletion(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

    // Function to return the minimum
    // deletions required
    static int MinDeletion(int []a, int n)
    {

        // To store the GCD of the array
        int gcd = 0;
        for (int i = 0; i < n; i++)
            gcd = __gcd(gcd, a[i]);

        // GCD cannot be 1
        if (gcd > 1)
            return -1;

        // GCD of the elements is already 1
        else
            return 0;
    }

    // Driver code
    public static void Main ()
    {
        int []a = { 3, 6, 12, 81, 9 };
        int n = a.Length;

        Console.WriteLine(MinDeletion(a, n));
    }
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Recursive function to return gcd of a and b
    function __gcd(a , b) {
        // Everything divides 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

    // Function to return the minimum
    // deletions required
    function MinDeletion(a , n) {

        // To store the GCD of the array
        var gcd = 0;
        for (i = 0; i < n; i++)
            gcd = __gcd(gcd, a[i]);

        // GCD cannot be 1
        if (gcd > 1)
            return -1;

        // GCD of the elements is already 1
        else
            return 0;
    }

    // Driver code

        var a = [ 3, 6, 12, 81, 9 ];
        var n = a.length;

        document.write(MinDeletion(a, n));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
-1
```

**时间复杂度:** O(N)