# 最大化数组的位或

> 原文:[https://www . geeksforgeeks . org/按位最大化数组或/](https://www.geeksforgeeks.org/maximize-the-bitwise-or-of-an-array/)

给定一个 N 个整数的数组。必须通过执行一项任务来最大化数组所有元素的按位“或”。任务是将数组中的任意元素**乘以给定的整数 x，最多为** k 倍
**示例:**

> 输入:a = {1，1，1}，k = 1，x = 2
> 输出:3
> 解释:做数组的一个元素
> 的任何可能的选择都会得到相同的三个数字 1，1，2。
> 所以，结果是 1 | 1 | 2 = 3。
> 输入:a = {1，2，4，8}，k = 2，x = 3
> 输出:79

**方法:**预先计算前缀和后缀或数组。
在一次迭代中，将一个元素与 x^k 相乘，并对其进行逐位“或”运算，即对所有先前的元素和后缀进行逐位“或”，或对所有后续元素进行逐位“或”，并在所有迭代后返回最大值。

## C++

```
// C++ program to maximize the Bitwise
// OR Sum in given array
#include <bits/stdc++.h>
using namespace std;

// Function to maximize the bitwise
// OR sum
int maxOR(long long arr[], int n, int k, int x)
{
    long long preSum[n + 1], suffSum[n + 1];
    long long res, pow = 1;

    // Compute x^k
    for (int i = 0; i < k; i++)
        pow *= x;

    // Find prefix bitwise OR
    preSum[0] = 0;
    for (int i = 0; i < n; i++)
        preSum[i + 1] = preSum[i] | arr[i];

    // Find suffix bitwise OR
    suffSum[n] = 0;
    for (int i = n - 1; i >= 0; i--)
        suffSum[i] = suffSum[i + 1] | arr[i];

    // Find maximum OR  value
    res = 0;
    for (int i = 0; i < n; i++)
        res = max(res, preSum[i] | (arr[i] * pow) | suffSum[i + 1]);

    return res;
}

// Drivers code
int main()
{
    long long arr[] = { 1, 2, 4, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2, x = 3;

    cout << maxOR(arr, n, k, x) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximize the Bitwise
// OR Sum in given array
import java.io.*;

class GFG {

    // Function to maximize the bitwise OR sum
    public static long maxOR(long arr[], int n,
                                  int k, int x)
    {
        long preSum[] = new long[n + 1];
        long suffSum[] = new long[n + 1];
        long res = 0, pow = 1;

        // Compute x^k
        for (int i = 0; i < k; i++)
            pow *= x;

        // Find prefix bitwise OR
        preSum[0] = 0;
        for (int i = 0; i < n; i++)
            preSum[i + 1] = preSum[i] | arr[i];

        // Find suffix bitwise OR
        suffSum[n] = 0;
        for (int i = n - 1; i >= 0; i--)
            suffSum[i] = suffSum[i + 1] | arr[i];

        // Find maximum OR value
        res = 0;
        for (int i = 0; i < n; i++)
            res = Math.max(res, preSum[i] |
                (arr[i] * pow) | suffSum[i + 1]);

        return res;
    }

    // Drivers code
    public static void main(String args[])
    {
        long arr[] = { 1, 2, 4, 8 };
        int n = 4;
        int k = 2, x = 3;

        long ans = maxOR(arr, n, k, x);
        System.out.println(ans);
    }
}

// This code is contributed by Jaideep Pyne
```

## 蟒蛇 3

```
# Python3 program to maximize the Bitwise
# OR Sum in given array

# Function to maximize the bitwise
# OR sum
def maxOR(arr, n, k, x):

    preSum = [0] * (n + 1)
    suffSum = [0] * (n + 1)
    pow = 1

    # Compute x^k
    for i in range(0 ,k):
        pow *= x

    # Find prefix bitwise OR
    preSum[0] = 0
    for i in range(0, n):
        preSum[i + 1] = preSum[i] | arr[i]

    # Find suffix bitwise OR
    suffSum[n] = 0
    for i in range(n-1, -1, -1):
        suffSum[i] = suffSum[i + 1] | arr[i]

    # Find maximum OR value
    res = 0
    for i in range(0 ,n):
        res = max(res, preSum[i] |
           (arr[i] * pow) | suffSum[i + 1])

    return res

# Drivers code
arr = [1, 2, 4, 8 ]
n = len(arr)
k = 2
x = 3
print(maxOR(arr, n, k, x))

# This code is contributed by Smitha
```

## C#

```
// C# program to maximize the Bitwise
// OR Sum in given array
using System;

class GFG {

    // Function to maximize the bitwise OR sum
    public static long maxOR(long []arr, int n,
                                  int k, int x)
    {
        long []preSum = new long[n + 1];
        long []suffSum = new long[n + 1];
        long res = 0, pow = 1;

        // Compute x^k
        for (int i = 0; i < k; i++)
            pow *= x;

        // Find prefix bitwise OR
        preSum[0] = 0;
        for (int i = 0; i < n; i++)
            preSum[i + 1] = preSum[i] | arr[i];

        // Find suffix bitwise OR
        suffSum[n] = 0;
        for (int i = n - 1; i >= 0; i--)
            suffSum[i] = suffSum[i + 1] | arr[i];

        // Find maximum OR value
        res = 0;
        for (int i = 0; i < n; i++)
            res = Math.Max(res, preSum[i] |
                (arr[i] * pow) | suffSum[i + 1]);

        return res;
    }

    // Drivers code
    public static void Main()
    {
        long []arr = { 1, 2, 4, 8 };
        int n = 4;
        int k = 2, x = 3;

        long ans = maxOR(arr, n, k, x);
        Console.Write(ans);
    }
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to maximize the
// Bitwise OR Sum in given array

// Function to maximize
// the bitwise OR sum

function maxOR($arr, $n, $k, $x)
{
    $res; $pow = 1;

    // Compute x^k
    for ($i = 0; $i < $k; $i++)
        $pow *= $x;

    // Find prefix bitwise OR
    $preSum[0] = 0;
    for ($i = 0; $i < $n; $i++)
        $preSum[$i + 1] = $preSum[$i] |    
                              $arr[$i];

    // Find suffix bitwise OR
    $suffSum[$n] = 0;
    for ($i = $n - 1; $i >= 0; $i--)
        $suffSum[$i] = $suffSum[$i + 1] |
                                $arr[$i];

    // Find maximum OR value
    $res = 0;
    for ($i = 0; $i < $n; $i++)
        $res = max($res, $preSum[$i] |
                   ($arr[$i] * $pow) |
                    $suffSum[$i + 1]);

    return $res;
}

// Driver Code
$arr = array(1, 2, 4, 8);
$n = sizeof($arr);
$k = 2; $x = 3;

echo maxOR($arr, $n, $k, $x),"\n";

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
    // Javascript program to maximize the Bitwise OR Sum in given array

    // Function to maximize the bitwise OR sum
    function maxOR(arr, n, k, x)
    {
        let preSum = new Array(n + 1);
        let suffSum = new Array(n + 1);
        let res = 0, pow = 1;

        // Compute x^k
        for (let i = 0; i < k; i++)
            pow *= x;

        // Find prefix bitwise OR
        preSum[0] = 0;
        for (let i = 0; i < n; i++)
            preSum[i + 1] = preSum[i] | arr[i];

        // Find suffix bitwise OR
        suffSum[n] = 0;
        for (let i = n - 1; i >= 0; i--)
            suffSum[i] = suffSum[i + 1] | arr[i];

        // Find maximum OR value
        res = 0;
        for (let i = 0; i < n; i++)
            res = Math.max(res, preSum[i] | (arr[i] * pow) | suffSum[i + 1]);

        return res;
    }

    let arr = [ 1, 2, 4, 8 ];
    let n = 4;
    let k = 2, x = 3;

    let ans = maxOR(arr, n, k, x);
    document.write(ans);

// This code is contributed by suresh07.
</script>
```

**Output :** 

```
79
```