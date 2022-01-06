# 将 2 的幂相加形成数字 X 的最小成本

> 原文:[https://www . geeksforgeeks . org/2 次方相加形成数字 x 的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-form-a-number-x-by-adding-up-powers-of-2/)

给定一个由 **N** 个整数和一个整数 **X** 组成的数组 **arr[]** 。数组中的元素**arr【I】**表示使用 **2 <sup>i</sup>** 的成本。任务是找到最小成本来选择加起来是 **X** 的数字。
**举例:**

> **输入:** arr[] = { 20，50，60，90 }，X = 7
> **输出:**120
> 2<sup>2</sup>+2<sup>1</sup>+2<sup>0</sup>= 4+2+1 = 7 成本= 60 + 50 + 20 = 130
> 但是我们可以用 2<sup>2</sup>+3 * 2<sup>0【T11
> **输入:** arr[] = { 10，5，50 }，X = 4
> **输出:** 10</sup>

**方法:**使用基本的[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。这里用到的事实是，每个数都可以用 2 的幂来构成。我们可以初步计算出形成 2 的幂所需的最小成本。复发情况如下:

> a[i] = min(a[i]，2 * a[I–1])

一旦数组被重新计算，我们可以简单地根据数字 **X** 中的设置位继续增加成本。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum cost
int MinimumCost(int a[], int n, int x)
{

    // Re-compute the array
    for (int i = 1; i < n; i++) {
        a[i] = min(a[i], 2 * a[i - 1]);
    }

    int ind = 0;

    int sum = 0;

    // Add answers for set bits
    while (x) {

        // If bit is set
        if (x & 1)
            sum += a[ind];

        // Increase the counter
        ind++;

        // Right shift the number
        x = x >> 1;
    }

    return sum;
}

// Driver code
int main()
{
    int a[] = { 20, 50, 60, 90 };
    int x = 7;
    int n = sizeof(a) / sizeof(a[0]);
    cout << MinimumCost(a, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the minimum cost
static int MinimumCost(int a[], int n, int x)
{

    // Re-compute the array
    for (int i = 1; i < n; i++)
    {
        a[i] = Math.min(a[i], 2 * a[i - 1]);
    }

    int ind = 0;

    int sum = 0;

    // Add answers for set bits
    while (x > 0)
    {

        // If bit is set
        if (x != 0 )
            sum += a[ind];

        // Increase the counter
        ind++;

        // Right shift the number
        x = x >> 1;
    }

    return sum;
}

// Driver code
public static void main (String[] args)
{

    int a[] = { 20, 50, 60, 90 };
    int x = 7;
    int n =a.length;
    System.out.println (MinimumCost(a, n, x));
}
}

// This Code is contributed by akt_mit
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimum cost
def MinimumCost(a, n, x):

    # Re-compute the array
    for i in range(1, n, 1):
        a[i] = min(a[i], 2 * a[i - 1])

    ind = 0

    sum = 0

    # Add answers for set bits
    while (x):

        # If bit is set
        if (x & 1):
            sum += a[ind]

        # Increase the counter
        ind += 1

        # Right shift the number
        x = x >> 1

    return sum

# Driver code
if __name__ == '__main__':
    a = [20, 50, 60, 90]
    x = 7
    n = len(a)
    print(MinimumCost(a, n, x))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum cost
public static int MinimumCost(int []a, int n, int x)
{

    // Re-compute the array
    for (int i = 1; i < n; i++)
    {
        a[i] = Math.Min(a[i], 2 * a[i - 1]);
    }

    int ind = 0;

    int sum = 0;

    // Add answers for set bits
    while (x > 0)
    {

        // If bit is set
        if (x != 0 )
            sum += a[ind];

        // Increase the counter
        ind++;

        // Right shift the number
        x = x >> 1;
    }

    return sum;
}

// Driver code
public static void Main ()
{

    int []a = { 20, 50, 60, 90 };
    int x = 7;
    int n =a.Length;
    Console.WriteLine(MinimumCost(a, n, x));
}
}

// This Code is contributed by SoM15242
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the approach
// Function to return the minimum cost

function MinimumCost($a, $n, $x)
{

    // Re-compute the array
    for ($i = 1; $i < $n; $i++)
    {
        $a[$i] = min($a[$i], 2 * $a[$i - 1]);
    }

    $ind = 0;

    $sum = 0;

    // Add answers for set bits
    while ($x)
    {

        // If bit is set
        if ($x & 1)
            $sum += $a[$ind];

        // Increase the counter
        $ind++;

        // Right shift the number
        $x = $x >> 1;
    }

    return $sum;
}

    // Driver code
    $a = array( 20, 50, 60, 90 );
    $x = 7;
    $n = sizeof($a) / sizeof($a[0]);
    echo MinimumCost($a, $n, $x);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

    // Function to return the minimum cost
    function MinimumCost(a , n , x) {

        // Re-compute the array
        for (i = 1; i < n; i++) {
            a[i] = Math.min(a[i], 2 * a[i - 1]);
        }

        var ind = 0;

        var sum = 0;

        // Add answers for set bits
        while (x > 0) {

            // If bit is set
            if (x != 0)
                sum += a[ind];

            // Increase the counter
            ind++;

            // Right shift the number
            x = x >> 1;
        }

        return sum;
    }

    // Driver code

        var a = [ 20, 50, 60, 90 ];
        var x = 7;
        var n = a.length;
        document.write(MinimumCost(a, n, x));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
120
```