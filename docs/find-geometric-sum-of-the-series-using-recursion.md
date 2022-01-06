# 用递归求级数的几何和

> 原文:[https://www . geesforgeks . org/find-几何级数求和-使用递归/](https://www.geeksforgeeks.org/find-geometric-sum-of-the-series-using-recursion/)

给定一个**整数 N** ，我们需要用递归求下面级数的几何和。

> **1+1/3+1/9+1/27+……+1/(3^n)**T2】

**例:**

```
Input N = 5 
Output: 1.49794

Input: N = 7
Output: 1.49977
```

**方法:**
在上述问题中，我们被要求使用递归。我们将计算最后一项，并每次对剩余的 n-1 项调用递归。返回的最终总和就是结果。
以下是上述办法的实施:

## C++

```
// CPP implementation to Find the
// geometric sum of the series using recursion

#include <bits/stdc++.h>
using namespace std;

// function to find the sum of given series
double sum(int n)
{
    // base case
    if (n == 0)
        return 1;

    // calculate the sum each time
    double ans = 1 / (double)pow(3, n) + sum(n - 1);

    // return final answer
    return ans;
}

// Driver code
int main()
{

    // integer initialisation
    int n = 5;

    cout << sum(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation to Find the
// geometric sum of the series using recursion

import java.util.*;

class GFG {

    static double sum(int n)
    {
        // base case
        if (n == 0)
            return 1;

        // calculate the sum each time
        double ans = 1 / (double)Math.pow(3, n) + sum(n - 1);

        // return final answer
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        // integer initialisation
        int n = 5;

        // print result
        System.out.println(sum(n));
    }
}
```

## 蟒蛇 3

```
# CPP implementation to Find the
# geometric sum of the series using recursion

def sum(n):

    # base case
    if n == 0:
        return 1

    # calculate the sum each time
    # and return final answer
    return 1 / pow(3, n) + sum(n-1)

n = 5;

print(sum(n));
```

## C#

```
// C# implementation to Find the
// geometric sum of the series using recursion

using System;

class GFG {

    static double sum(int n)
    {
        // base case
        if (n == 0)
            return 1;

        // calculate the sum each time
        double ans = 1 / (double)Math.Pow(3, n) + sum(n - 1);

        // return final answer
        return ans;
    }

    // Driver code
    static public void Main()
    {
        int n = 5;

        Console.WriteLine(sum(n));
    }
}
```

## java 描述语言

```
<script>

// Javascript implementation to Find the
// geometric sum of the series using recursion

// function to find the sum of given series
function sum(n)
{
    // base case
    if (n == 0)
        return 1;

    // calculate the sum each time
    var ans = 1 / Math.pow(3, n) + sum(n - 1);

    // return final answer
    return ans;
}

// Driver code
// integer initialisation
var n = 5;
document.write( sum(n).toFixed(5));

</script>
```

**Output:** 

```
1.49794
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)