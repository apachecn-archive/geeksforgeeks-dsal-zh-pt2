# 重复 N 除以除数后的最大和

> 原文:[https://www . geeksforgeeks . org/n 除以除数后的最大和/](https://www.geeksforgeeks.org/maximum-sum-after-repeatedly-dividing-n-by-a-divisor/)

给定一个整数 **N** 。任务是找到应用以下操作后获得的中间值(包括 **N** 和 **1** )的最大可能和:

> 将 **N** 除以任意除数(> 1)，直到它变成 1。

**例:**

```
Input: N = 10
Output: 16
Initially, N=10
1st Division -> N = 10/2 = 5 
2nd Division -> N= 5/5 = 1

Input: N = 8
Output: 15
Initially, N=8
1st Division -> N = 8/2 = 4 
2nd Division -> N= 4/2 = 2
3rd Division -> N= 2/2 = 1
```

**方法:**由于任务是每一步后的价值总和最大化，所以尽量将个体价值最大化。所以，尽量减少 **N** 的数值。为了实现这一点，我们将**除以其最小除数。
以下是上述方法的实现:** 

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest divisor
int smallestDivisor(int n)
{
    int mx = sqrt(n);
    for (int i = 2; i <= mx; i++)
        if (n % i == 0)
            return i;
    return n;
}

// Function to find the maximum sum
int maxSum(int n)
{
    long long res = n;
    while (n > 1) {
        int divi = smallestDivisor(n);
        n /= divi;
        res += n;
    }
    return res;
}

// Driver Code
int main()
{
    int n = 34;
    cout << maxSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG
{

// Function to find the smallest divisor
static double smallestDivisor(int n)
{
    double mx = Math.sqrt(n);
    for (int i = 2; i <= mx; i++)
        if (n % i == 0)
            return i;
    return n;
}

// Function to find the maximum sum
static double maxSum(int n)
{
    long res = n;
    while (n > 1)
    {
        double divi = smallestDivisor(n);
        n /= divi;
        res += n;
    }
    return res;
}

    // Driver Code
    public static void main (String[] args)
    {
        int n = 34;
        System.out.println (maxSum(n));
    }
}

// This code is contributed by jit_t.
```

## 蟒蛇 3

```
from math import sqrt
# Python 3 implementation of the above approach

# Function to find the smallest divisor
def smallestDivisor(n):
    mx = int(sqrt(n))
    for i in range(2, mx + 1, 1):
        if (n % i == 0):
            return i
    return n

# Function to find the maximum sum
def maxSum(n):
    res = n
    while (n > 1):
        divi = smallestDivisor(n)
        n = int(n/divi)
        res += n

    return res

# Driver Code
if __name__ == '__main__':
    n = 34
    print(maxSum(n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to find the smallest divisor
    static double smallestDivisor(int n)
    {
        double mx = Math.Sqrt(n);
        for (int i = 2; i <= mx; i++)
            if (n % i == 0)
                return i;
        return n;
    }

    // Function to find the maximum sum
    static double maxSum(int n)
    {
        long res = n;
        while (n > 1)
        {
            double divi = smallestDivisor(n);
            n /= (int)divi;
            res += n;
        }
        return res;
    }

    // Driver Code
    public static void Main()
    {
        int n = 34;
        Console.WriteLine(maxSum(n));
    }
}

// This code is contributed by Ryuga.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the above approach
// Function to find the smallest divisor
function smallestDivisor($n)
{
    $mx = sqrt($n);
    for ($i = 2; $i <= $mx; $i++)
        if ($n % $i == 0)
            return $i;
    return $n;
}

// Function to find the maximum sum
function maxSum($n)
{
    $res = $n;
    while ($n > 1)
    {
        $divi = smallestDivisor($n);
        $n /= $divi;
        $res += $n;
    }
    return $res;
}

    // Driver Code
    $n = 34;
    echo maxSum($n);

#This code is contributed by akt_mit.
?>
```

## java 描述语言

```
<script>
// javascript implementation of the above approach

    // Function to find the smallest divisor
    function smallestDivisor(n) {
        var mx = Math.sqrt(n);
        for (i = 2; i <= mx; i++)
            if (n % i == 0)
                return i;
        return n;
    }

    // Function to find the maximum sum
    function maxSum(n) {
        var res = n;
        while (n > 1) {
            var divi = smallestDivisor(n);
            n /= divi;
            res += n;
        }
        return res;
    }

    // Driver Code
        var n = 34;
        document.write(maxSum(n));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
52
```

**时间复杂度:** O(sqrt(n)*log(n))