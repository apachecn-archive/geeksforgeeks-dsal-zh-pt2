# N 与 2 的任意次方的最小绝对差

> 原文:[https://www . geesforgeks . org/n 和 2 的任意次方的最小绝对差/](https://www.geeksforgeeks.org/minimum-absolute-difference-between-n-and-any-power-of-2/)

给定一个正整数 **N** ，任务是求 **N** 与 **2** 任意次方的最小绝对差。

**示例:**

> **输入:** N = 3
> **输出:** 1
> 最接近 3 的 2 的较小幂为 2，ABS(3–2)= 1
> 最接近 3 的 2 的较大幂为 4，ABS(4–3)= 1
> 
> **输入:**N = 6
> T3】输出: 2

**进场:**

1.  找到小于或等于 N 的 2 的[最高幂，并将其存储在变量**低**中。](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/)
2.  找到大于或等于 N 的 2 的最小幂并将其存储在变量**高**中。
3.  现在，答案将是**max(N–低，高–N)**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the highest power
// of 2 less than or equal to n
int prevPowerof2(int n)
{
    int p = (int)log2(n);
    return (int)pow(2, p);
}

// Function to return the smallest power
// of 2 greater than or equal to n
int nextPowerOf2(int n)
{
    int p = 1;
    if (n && !(n & (n - 1)))
        return n;

    while (p < n)
        p <<= 1;

    return p;
}

// Function that returns the minimum
// absolute difference between n
// and any power of 2
int minDiff(int n)
{
    int low = prevPowerof2(n);
    int high = nextPowerOf2(n);

    return min(n - low, high - n);
}

// Driver code
int main()
{
    int n = 6;

    cout << minDiff(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the highest power
    // of 2 less than or equal to n
    static int prevPowerof2(int n)
    {
        int p = (int)(Math.log(n) / Math.log(2));

        return (int)Math.pow(2, p);
    }

    // Function to return the smallest power
    // of 2 greater than or equal to n
    static int nextPowerOf2(int n)
    {
        int p = 1;
        if ((n == 0) && !((n & (n - 1)) == 0))
            return n;

        while (p < n)
            p <<= 1;

        return p;
    }

    // Function that returns the minimum
    // absolute difference between n
    // and any power of 2
    static int minDiff(int n)
    {
        int low = prevPowerof2(n);
        int high = nextPowerOf2(n);

        return Math.min(n - low, high - n);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 6;

        System.out.println(minDiff(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import log

# Function to return the highest power
# of 2 less than or equal to n
def prevPowerof2(n):
    p = int(log(n))
    return pow(2, p)

# Function to return the smallest power
# of 2 greater than or equal to n
def nextPowerOf2(n):
    p = 1
    if (n and (n & (n - 1)) == 0):
        return n

    while (p < n):
        p <<= 1

    return p

# Function that returns the minimum
# absolute difference between n
# and any power of 2
def minDiff(n):
    low = prevPowerof2(n)
    high = nextPowerOf2(n)

    return min(n - low, high - n)

# Driver code
n = 6

print(minDiff(n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the highest power
    // of 2 less than or equal to n
    static int prevPowerof2(int n)
    {
        int p = (int)(Math.Log(n) / Math.Log(2));

        return (int)Math.Pow(2, p);
    }

    // Function to return the smallest power
    // of 2 greater than or equal to n
    static int nextPowerOf2(int n)
    {
        int p = 1;
        if ((n == 0) && !((n & (n - 1)) == 0))
            return n;

        while (p < n)
            p <<= 1;

        return p;
    }

    // Function that returns the minimum
    // absolute difference between n
    // and any power of 2
    static int minDiff(int n)
    {
        int low = prevPowerof2(n);
        int high = nextPowerOf2(n);

        return Math.Min(n - low, high - n);
    }

    // Driver code
    public static void Main (String []args)
    {
        int n = 6;

        Console.WriteLine(minDiff(n));
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the highest power
// of 2 less than or equal to n
function prevPowerof2(n)
{
    var p = parseInt(Math.log(n)/Math.log(2));
    return parseInt(Math.pow(2, p));
}

// Function to return the smallest power
// of 2 greater than or equal to n
function nextPowerOf2(n)
{
    var p = 1;
    if (n && !(n & (n - 1)))
        return n;

    while (p < n)
        p <<= 1;

    return p;
}

// Function that returns the minimum
// absolute difference between n
// and any power of 2
function minDiff(n)
{
    var low = prevPowerof2(n);
    var high = nextPowerOf2(n);

    return Math.min(n - low, high - n);
}

// Driver code
var n = 6;
document.write(minDiff(n));

// This code is contributed by noob2000.
</script>
```

**Output**

```
2
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*