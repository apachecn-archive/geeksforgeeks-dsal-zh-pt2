# 执行给定运算后数组所有元素的最大和

> 原文:[https://www . geeksforgeeks . org/执行给定操作后数组所有元素的最大和/](https://www.geeksforgeeks.org/maximum-sum-of-all-elements-of-array-after-performing-given-operations/)

给定一个整数数组。任务是在每次执行给定的两个操作后，找到数组中所有元素的最大和。
操作为:

> 1.从数组的开头选择一些(可能没有)连续的元素，然后乘以-1。
> 2。从数组末尾选择一些(可能没有)连续元素，然后乘以-1。

**例:**

```
Input : arr[] = {-1, 10, -5, 10, -2}
Output : 18
After 1st operation : 1 10 -5 10 -2
After 2nd operation : 1 10 -5 10 2

Input : arr[] = {-9, -8, -7}
Output : 24
After 1st operation : 9 8 -7
After 2nd operation : 9 8 7
```

**方法:**这个问题可以用线性时间解决，使用如下思路:

*   设 A1 元素的和..An 等于 s，那么当反转符号时，我们得到-A1，-A2..-An，然后总和变为-S，即当反转整个线段的符号时，线段上元素的总和将改变其符号。
*   考虑如下初始问题:选择一个连续的子序列，并反转它剩余的所有数字。
*   使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)求最大子阵和。
*   保持子阵列不变，其余的用-1 相乘。
*   将整个阵列的总和视为 S，相邻子阵列的最大总和视为 S1，总和将等于-(S-S1)+S1 = 2 * S1–S。这是所需的总和。

以下是上述方法的实现:

## C++

```
// CPP program to find the maximum
// sum after given operations

#include <bits/stdc++.h>
using namespace std;

// Function to calculate Maximum Subarray Sum
// or Kadane's Algorithm
int maxSubArraySum(int a[], int size)
{
    int max_so_far = INT_MIN, max_ending_here = 0;

    for (int i = 0; i < size; i++) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to find the maximum
// sum after given operations
int maxSum(int a[], int n)
{
    // To store sum of all elements
    int S = 0;

    // Maximum sum of a subarray
    int S1 = maxSubArraySum(a, n);

    // Calculate the sum of all elements
    for (int i = 0; i < n; i++)
        S += a[i];

    return (2 * S1 - S);
}

// Driver Code
int main()
{
    int a[] = { -35, 32, -24, 0, 27, -10, 0, -19 };

    // size of an array
    int n = sizeof(a) / sizeof(a[0]);

    cout << maxSum(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// sum after given operations

import java.io.*;

class GFG {

// Function to calculate Maximum Subarray Sum
// or Kadane's Algorithm
static int maxSubArraySum(int a[], int size)
{
    int max_so_far = Integer.MIN_VALUE, max_ending_here = 0;

    for (int i = 0; i < size; i++) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to find the maximum
// sum after given operations
static int maxSum(int a[], int n)
{
    // To store sum of all elements
    int S = 0;

    // Maximum sum of a subarray
    int S1 = maxSubArraySum(a, n);

    // Calculate the sum of all elements
    for (int i = 0; i < n; i++)
        S += a[i];

    return (2 * S1 - S);
}

// Driver Code

    public static void main (String[] args) {
    int a[] = { -35, 32, -24, 0, 27, -10, 0, -19 };

    // size of an array
    int n = a.length;

    System.out.println( maxSum(a, n));
    }
}
// This code is contributed by inder_verma
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# sum after given operations
import sys

# Function to calculate Maximum
# Subarray Sum or Kadane's Algorithm
def maxSubArraySum(a, size) :

    max_so_far = -(sys.maxsize - 1)
    max_ending_here = 0

    for i in range(size) :

        max_ending_here = max_ending_here + a[i]

        if (max_so_far < max_ending_here) :
                max_so_far = max_ending_here

        if (max_ending_here < 0) :
                max_ending_here = 0

    return max_so_far

# Function to find the maximum
# sum after given operations
def maxSum(a, n) :

    # To store sum of all elements
    S = 0;

    # Maximum sum of a subarray
    S1 = maxSubArraySum(a, n)

    # Calculate the sum of all elements
    for i in range(n) :
        S += a[i]

    return (2 * S1 - S)

# Driver Code
if __name__ == "__main__" :

    a = [ -35, 32, -24, 0,
           27, -10, 0, -19 ]

    # size of an array
    n = len(a)

    print(maxSum(a, n))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find the maximum
// sum after given operations

using System;

class GFG {

// Function to calculate Maximum Subarray Sum
// or Kadane's Algorithm
static int maxSubArraySum(int []a, int size)
{
    int max_so_far = int.MinValue, max_ending_here = 0;

    for (int i = 0; i < size; i++) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to find the maximum
// sum after given operations
static int maxSum(int []a, int n)
{
    // To store sum of all elements
    int S = 0;

    // Maximum sum of a subarray
    int S1 = maxSubArraySum(a, n);

    // Calculate the sum of all elements
    for (int i = 0; i < n; i++)
        S += a[i];

    return (2 * S1 - S);
}

// Driver Code

    public static void Main () {
    int []a = { -35, 32, -24, 0, 27, -10, 0, -19 };

    // size of an array
    int n = a.Length;

    Console.WriteLine( maxSum(a, n));
    }
}
// This code is contributed by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum
// sum after given operations

// Function to calculate Maximum Subarray
// Sum or Kadane's Algorithm
function  maxSubArraySum($a, $size)
{
    $max_so_far = PHP_INT_MIN;
    $max_ending_here = 0;

    for ($i = 0; $i < $size; $i++)
    {
        $max_ending_here = $max_ending_here + $a[$i];
        if ($max_so_far < $max_ending_here)
            $max_so_far = $max_ending_here;

        if ($max_ending_here < 0)
            $max_ending_here = 0;
    }
    return $max_so_far;
}

// Function to find the maximum
// sum after given operations
function maxSum($a, $n)
{
    // To store sum of all elements
    $S = 0;

    // Maximum sum of a subarray
    $S1 = maxSubArraySum($a, $n);

    // Calculate the sum of all elements
    for ($i = 0; $i < $n; $i++)
        $S += $a[$i];

    return (2 * $S1 - $S);
}

// Driver Code
$a = array(-35, 32, -24, 0,
            27, -10, 0, -19);

// size of an array
$n = sizeof($a);

echo( maxSum($a, $n));

// This code is contributed
// by Mukul Singh
```

## java 描述语言

```
<script>
// javascript program to find the maximum
// sum after given operations   

// Function to calculate Maximum Subarray Sum
    // or Kadane's Algorithm
    function maxSubArraySum(a , size)
    {
        var max_so_far = Number.MIN_VALUE, max_ending_here = 0;

        for (i = 0; i < size; i++)
        {
            max_ending_here = max_ending_here + a[i];
            if (max_so_far < max_ending_here)
                max_so_far = max_ending_here;

            if (max_ending_here < 0)
                max_ending_here = 0;
        }
        return max_so_far;
    }

    // Function to find the maximum
    // sum after given operations
    function maxSum(a, n)
    {

        // To store sum of all elements
        var S = 0;

        // Maximum sum of a subarray
        var S1 = maxSubArraySum(a, n);

        // Calculate the sum of all elements
        for (i = 0; i < n; i++)
            S += a[i];

        return (2 * S1 - S);
    }

    // Driver Code
        var a = [ -35, 32, -24, 0, 27, -10, 0, -19 ];

        // size of an array
        var n = a.length;

        document.write(maxSum(a, n));

// This code is contributed by todaysgaurav.
</script>
```

**Output:** 

```
99
```