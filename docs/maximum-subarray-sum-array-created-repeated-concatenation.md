# 重复连接后创建的阵列中的最大子阵列和

> 原文:[https://www . geesforgeks . org/maximum-subarray-sum-array-created-repeated-concation/](https://www.geeksforgeeks.org/maximum-subarray-sum-array-created-repeated-concatenation/)

给定一个数组和一个数 k，求修改后的数组中连续数组的最大和，该数组是通过重复给定的数组 k 次而形成的。
示例:

```
Input  : arr[] = {-1, 10, 20}, k = 2
Output : 59
After concatenating array twice, we 
get {-1, 10, 20, -1, 10, 20} which has 
maximum subarray sum as 59.

Input  : arr[] = {-1, -2, -3}, k = 3
Output : -1
```

一个**简单的解决方案**是创建一个 n*k 大小的数组，然后运行[卡丹的算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。时间复杂度为 O(nk)，辅助空间为 O(n*k)
A **更好的解决方案**是在同一个数组上运行一个循环，并使用模块化算法在数组结束后从头向后移动。

## C++

```
// C++ program to print largest contiguous
// array sum when array is created after
// concatenating a small array k times.
#include<bits/stdc++.h>
using namespace std;

// Returns sum of maximum sum subarray created
// after concatenating a[0..n-1] k times.
int maxSubArraySumRepeated(int a[], int n, int k)
{
    int max_so_far = INT_MIN, max_ending_here = 0;

    for (int i = 0; i < n*k; i++)
    {
        // This is where it differs from Kadane's
        // algorithm. We use modular arithmetic to
        // find next element.
        max_ending_here = max_ending_here + a[i%n];

        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

/*Driver program to test maxSubArraySum*/
int main()
{
    int a[] = {10, 20, -30, -1};
    int n = sizeof(a)/sizeof(a[0]);
    int k = 3;
    cout << "Maximum contiguous sum is "
         << maxSubArraySumRepeated(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print largest contiguous
// array sum when array is created after
// concatenating a small array k times.
import java.io.*;

class GFG {

// Returns sum of maximum sum
// subarray created after
// concatenating a[0..n-1] k times.
static int maxSubArraySumRepeated(int a[],
                             int n, int k)
{
    int max_so_far = 0;
    int INT_MIN, max_ending_here=0;

    for (int i = 0; i < n*k; i++)
    {
        // This is where it differs from
        // Kadane's algorithm. We use modular
        //  arithmetic to find next element.
        max_ending_here = max_ending_here +
                                    a[i % n];

        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Driver program to test maxSubArraySum
public static void main (String[] args) {

    int a[] = {10, 20, -30, -1};
    int n = a.length;
    int k = 3;

    System.out.println("Maximum contiguous sum is "
                   + maxSubArraySumRepeated(a, n, k));
}

}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python program to print
# largest contiguous
# array sum when array
# is created after
# concatenating a small
# array k times.

# Returns sum of maximum
# sum subarray created
# after concatenating
# a[0..n-1] k times.
def maxSubArraySumRepeated(a, n, k):

    max_so_far = -2147483648
    max_ending_here = 0

    for i in range(n*k):

        # This is where it
        # differs from Kadane's
        # algorithm. We use
        #  modular arithmetic to
        # find next element.
        max_ending_here = max_ending_here + a[i%n]

        if (max_so_far < max_ending_here):
            max_so_far = max_ending_here

        if (max_ending_here < 0):
            max_ending_here = 0

    return max_so_far

# Driver program
# to test maxSubArraySum

a = [10, 20, -30, -1]
n = len(a)
k = 3

print("Maximum contiguous sum is ",
    maxSubArraySumRepeated(a, n, k))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to print largest contiguous
// array sum when array is created after
// concatenating a small array k times.
using System;

class GFG {

// Returns sum of maximum sum
// subarray created after
// concatenating a[0..n-1] k times.
static int maxSubArraySumRepeated(int []a,
                                  int n,
                                  int k)
{
    int max_so_far = 0;
    int max_ending_here=0;

    for (int i = 0; i < n * k; i++)
    {
        // This is where it differs from
        // Kadane's algorithm. We use modular
        // arithmetic to find next element.
        max_ending_here = max_ending_here +
                                  a[i % n];

        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Driver Code
public static void Main ()
{

    int []a = {10, 20, -30, -1};
    int n = a.Length;
    int k = 3;

    Console.Write("Maximum contiguous sum is "
                  + maxSubArraySumRepeated(a, n, k));
}
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print largest contiguous
// array sum when array is created after
// concatenating a small array k times.

// Returns sum of maximum
// sum subarray created
// after concatenating
// a[0..n-1] k times.
function maxSubArraySumRepeated($a, $n, $k)
{
    $INT_MIN=0;
    $max_so_far = $INT_MIN; $max_ending_here = 0;

    for ($i = 0; $i < $n*$k; $i++)
    {

        // This is where it differs
        // from Kadane's algorithm.
        // We use modular arithmetic
        // to find next element.
        $max_ending_here = $max_ending_here +
                                  $a[$i % $n];

        if ($max_so_far < $max_ending_here)
            $max_so_far = $max_ending_here;

        if ($max_ending_here < 0)
            $max_ending_here = 0;
    }
    return $max_so_far;
}

    // Driver Code
    $a = array(10, 20, -30, -1);
    $n = sizeof($a);
    $k = 3;
    echo "Maximum contiguous sum is "
          , maxSubArraySumRepeated($a, $n, $k);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to print largest contiguous
// array sum when array is created after
// concatenating a small array k times.

// Returns sum of maximum sum
// subarray created after
// concatenating a[0..n-1] k times.
function maxSubArraySumRepeated(a, n, k)
{
    let max_so_far = 0;
    let INT_MIN, max_ending_here=0;

    for (let i = 0; i < n*k; i++)
    {
        // This is where it differs from
        // Kadane's algorithm. We use modular
        //  arithmetic to find next element.
        max_ending_here = max_ending_here +
                                    a[i % n];

        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Driver code

    let a = [10, 20, -30, -1];
    let n = a.length;
    let k = 3;

    document.write("Maximum contiguous sum is "
                   + maxSubArraySumRepeated(a, n, k));

// This code is contributed by sanjoy_62.
</script>
```

输出:

```
Maximum contiguous sum is 30
```

**能否利用数组的重复性质得到更好的解？**