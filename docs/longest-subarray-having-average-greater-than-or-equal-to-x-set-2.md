# 平均值大于或等于 x 的最长子阵列| Set-2

> 原文:[https://www . geeksforgeeks . org/最长-子阵列-具有-平均值-大于或等于-x-set-2/](https://www.geeksforgeeks.org/longest-subarray-having-average-greater-than-or-equal-to-x-set-2/)

给定一个 N 个整数的数组。任务是找到最长的连续子阵列，使其元素的平均值大于或等于给定的数 x。
**示例:**

```
Input:  arr = {1, 1, 2, -1, -1, 1},  X = 1
Output: 3
Length of longest subarray
with average >= 1 is 3 i.e.
((1+1+2)/3)= 1.333

Input: arr[] = {2, -3, 3, 2, 1}, x = 2
Output: 3
Length of Longest subarray is 3 having 
average 2 which is equal to x.
```

时间复杂度为 *O(Nlogn)* 的方法已经在[这里](https://www.geeksforgeeks.org/longest-subarray-having-average-greater-than-or-equal-to-x/)讨论过了。在这篇文章中，将讨论一种具有时间复杂性的有效方法 *O(N)* 。
**进场:**

1.  从每个 arr[i]中减去 X，并将数组转换为前缀数组。让我们将新数组称为 prefixarr[]。
2.  现在问题变成了在 prefixarr[]中求 max(j-i)，使得 j > i 和 prefixarr[j] > prefixarr[i]，即类似于[给定一个数组 arr[]，求最大 j–I，使得 arr[j] > arr[i]](https://www.geeksforgeeks.org/given-an-array-arr-find-the-maximum-j-i-such-that-arrj-arri/)

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Utility Function to find the index
// with maximum difference
int maxIndexDiff(int arr[], int n)
{
    int maxDiff;
    int i, j;

    int LMin[n], RMax[n];

    // Construct LMin[] such that LMin[i]
    // stores the minimum value
    // from (arr[0], arr[1], ... arr[i])
    LMin[0] = arr[0];
    for (i = 1; i < n; ++i)
        LMin[i] = min(arr[i], LMin[i - 1]);

    // Construct RMax[] such that RMax[j]
    // stores the maximum value
    // from (arr[j], arr[j+1], ..arr[n-1])
    RMax[n - 1] = arr[n - 1];
    for (j = n - 2; j >= 0; --j)
        RMax[j] = max(arr[j], RMax[j + 1]);

    // Traverse both arrays from left to right
    // to find optimum j - i
    // This process is similar to merge()
    // of MergeSort
    i = 0, j = 0, maxDiff = -1;
    while (j < n && i < n) {
        if (LMin[i] < RMax[j]) {
            maxDiff = max(maxDiff, j - i);
            j = j + 1;
        }
        else
            i = i + 1;
    }

    return maxDiff + 1;
}

// utility Function which subtracts X from all
// the elements in the array
void modifyarr(int arr[], int n, int x)
{
    for (int i = 0; i < n; i++)
        arr[i] = arr[i] - x;
}

// Calculating the prefix sum array
// of the modified array
void calcprefix(int arr[], int n)
{
    int s = 0;
    for (int i = 0; i < n; i++) {
        s += arr[i];
        arr[i] = s;
    }
}

// Function to find the length of the longest
// subarray with average >= x
int longestsubarray(int arr[], int n, int x)
{
    modifyarr(arr, n, x);
    calcprefix(arr, n);

    return maxIndexDiff(arr, n);
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, -1, -1, 1 };
    int x = 1;
    int n = sizeof(arr) / sizeof(int);
    cout << longestsubarray(arr, n, x) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above approach
import java.io.*;
import java.lang.*;

class GFG
{

// Utility Function to find the
// index with maximum difference
static int maxIndexDiff(int arr[],
                        int n)
{
    int maxDiff;
    int i, j;

    int LMin[], RMax[];
    LMin = new int[n];
    RMax = new int[n];

    // Construct LMin[] such that
    // LMin[i] stores the minimum value
    // from (arr[0], arr[1], ... arr[i])
    LMin[0] = arr[0];
    for (i = 1; i < n; ++i)
        LMin[i] = Math.min(arr[i], LMin[i - 1]);

    // Construct RMax[] such that
    // RMax[j] stores the maximum value
    // from (arr[j], arr[j+1], ..arr[n-1])
    RMax[n - 1] = arr[n - 1];
    for (j = n - 2; j >= 0; --j)
        RMax[j] = Math.max(arr[j], RMax[j + 1]);

    // Traverse both arrays from left
    // to right to find optimum j - i
    // This process is similar to merge()
    // of MergeSort
    i = 0;
    j = 0;
    maxDiff = -1;
    while (j < n && i < n)
    {
        if (LMin[i] < RMax[j])
        {
            maxDiff = Math.max(maxDiff, j - i);
            j = j + 1;
        }
        else
            i = i + 1;
    }

    return (maxDiff + 1);
}

// utility Function which subtracts X
// from all the elements in the array
static void modifyarr(int arr[],
                      int n, int x)
{
    for (int i = 0; i < n; i++)
        arr[i] = arr[i] - x;
}

// Calculating the prefix sum
// array of the modified array
static void calcprefix(int arr[], int n)
{
    int s = 0;
    for (int i = 0; i < n; i++)
    {
        s += arr[i];
        arr[i] = s;
    }
}

// Function to find the length of the
// longest subarray with average >= x
static int longestsubarray(int arr[],
                           int n, int x)
{
    modifyarr(arr, n, x);
    calcprefix(arr, n);

    return maxIndexDiff(arr, n);
}

// Driver code
public static void main(String args[])
{
    int[] arr ={ 1, 1, 2, -1, -1, 1 };
    int x = 1;
    int n = arr.length;
    System.out.println(longestsubarray(arr, n, x));
}
}

// This code is contributed by Subhadeep
```

## 蟒蛇 3

```
# Python 3 implementation
# of above approach

# Utility Function to find the
# index with maximum difference
def maxIndexDiff(arr,n):
    LMin = [None] * n
    RMax = [None] * n

    # Construct LMin[] such that LMin[i]
    # stores the minimum value
    # from (arr[0], arr[1], ... arr[i])
    LMin[0] = arr[0]
    for i in range(1, n):
        LMin[i] = min(arr[i], LMin[i - 1])

    # Construct RMax[] such that RMax[j]
    # stores the maximum value
    # from (arr[j], arr[j+1], ..arr[n-1])
    RMax[n - 1] = arr[n - 1]
    for j in range(n - 2,-1,-1):
        RMax[j] = max(arr[j], RMax[j + 1])

    # Traverse both arrays from left
    # to right to find optimum j - i
    # This process is similar to merge()
    # of MergeSort
    i = 0
    j = 0
    maxDiff = -1
    while (j < n and i < n):
        if (LMin[i] < RMax[j]):
            maxDiff = max(maxDiff, j - i)
            j = j + 1

        else:
            i = i + 1

    return maxDiff + 1

# utility Function which subtracts X
# from all the elements in the array
def modifyarr(arr, n, x):
    for i in range(n):
        arr[i] = arr[i] - x

# Calculating the prefix sum
# array of the modified array
def calcprefix(arr, n):
    s = 0
    for i in range(n):
        s += arr[i]
        arr[i] = s

# Function to find the length of the
# longest subarray with average >= x
def longestsubarray(arr, n, x):
    modifyarr(arr, n, x)
    calcprefix(arr, n)

    return maxIndexDiff(arr, n)

# Driver code
if __name__ == "__main__":
    arr = [ 1, 1, 2, -1, -1, 1 ]
    x = 1
    n = len(arr)
    print(longestsubarray(arr, n, x))

# This code is contributed by ChitraNayal
```

## C#

```
// C# implementation of
// above approach
using System;

class GFG
{

// Utility Function to find the
// index with maximum difference
static int maxIndexDiff(int[] arr,
                        int n)
{
    int maxDiff;
    int i, j;

    int[] LMin = new int[n];
    int[] RMax = new int[n];

    // Construct LMin[] such that
    // LMin[i] stores the minimum value
    // from (arr[0], arr[1], ... arr[i])
    LMin[0] = arr[0];
    for (i = 1; i < n; ++i)
        LMin[i] = Math.Min(arr[i],
                      LMin[i - 1]);

    // Construct RMax[] such that
    // RMax[j] stores the maximum value
    // from (arr[j], arr[j+1], ..arr[n-1])
    RMax[n - 1] = arr[n - 1];
    for (j = n - 2; j >= 0; --j)
        RMax[j] = Math.Max(arr[j],
                           RMax[j + 1]);

    // Traverse both arrays from left
    // to right to find optimum j - i
    // This process is similar to merge()
    // of MergeSort
    i = 0;
    j = 0;
    maxDiff = -1;
    while (j < n && i < n)
    {
        if (LMin[i] < RMax[j])
        {
            maxDiff = Math.Max(maxDiff, j - i);
            j = j + 1;
        }
        else
            i = i + 1;
    }

    return (maxDiff + 1);
}

// utility Function which subtracts X
// from all the elements in the array
static void modifyarr(int[] arr,
                      int n, int x)
{
    for (int i = 0; i < n; i++)
        arr[i] = arr[i] - x;
}

// Calculating the prefix sum
// array of the modified array
static void calcprefix(int[] arr,
                       int n)
{
    int s = 0;
    for (int i = 0; i < n; i++)
    {
        s += arr[i];
        arr[i] = s;
    }
}

// Function to find the length of the
// longest subarray with average >= x
static int longestsubarray(int[] arr,
                           int n, int x)
{
    modifyarr(arr, n, x);
    calcprefix(arr, n);

    return maxIndexDiff(arr, n);
}

// Driver code
public static void Main()
{
    int[] arr ={ 1, 1, 2, -1, -1, 1 };
    int x = 1;
    int n = arr.Length;
    Console.Write(longestsubarray(arr, n, x));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Utility Function to find the
// index with maximum difference
function maxIndexDiff(&$arr, $n)
{
    $LMin[$n] = array();
    $RMax[$n] = array();

    // Construct LMin[] such that LMin[i]
    // stores the minimum value
    // from (arr[0], arr[1], ... arr[i])
    $LMin[0] = $arr[0];
    for ($i = 1; $i < $n; ++$i)
        $LMin[$i] = min($arr[$i],
                        $LMin[$i - 1]);

    // Construct RMax[] such that RMax[j]
    // stores the maximum value
    // from (arr[j], arr[j+1], ..arr[n-1])
    $RMax[$n - 1] = $arr[$n - 1];
    for ($j = $n - 2; $j >= 0; --$j)
        $RMax[$j] = max($arr[$j],
                        $RMax[$j + 1]);

    // Traverse both arrays from left
    // to right to find optimum j - i
    // This process is similar to merge()
    // of MergeSort
    $i = 0;
    $j = 0;
    $maxDiff = -1;
    while ($j < $n && $i < $n)
    {
        if ($LMin[$i] < $RMax[$j])
        {
            $maxDiff = max($maxDiff, $j - $i);
            $j = $j + 1;
        }
        else
            $i = $i + 1;
    }

    return $maxDiff + 1;
}

// utility Function which subtracts X
// from all the elements in the array
function modifyarr($arr, $n, $x)
{
    for ($i = 0; $i < $n; $i++)
        $arr[$i] = $arr[$i] - $x;
    return calcprefix($arr, $n);
}

// Calculating the prefix sum
// array of the modified array
function calcprefix(&$arr, $n)
{
    $s = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $s += $arr[$i];
        $arr[$i] = $s;
    }
    return maxIndexDiff($arr, $n);
}

// Function to find the length of the
// longest subarray with average >= x
function longestsubarray(&$arr, $n, $x)
{
    return modifyarr($arr, $n, $x);
}

// Driver code
$arr = array( 1, 1, 2, -1, -1, 1 );
$x = 1;
$n = sizeof($arr);
echo longestsubarray($arr, $n, $x) ;

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript implementation of
// above approach

// Utility Function to find the
// index with maximum difference   
function maxIndexDiff(arr,n)
{
    let maxDiff;
    let i, j;

    let LMin, RMax;
    LMin = new Array(n);
    RMax = new Array(n);

    // Construct LMin[] such that
    // LMin[i] stores the minimum value
    // from (arr[0], arr[1], ... arr[i])
    LMin[0] = arr[0];
    for (i = 1; i < n; ++i)
        LMin[i] = Math.min(arr[i], LMin[i - 1]);

    // Construct RMax[] such that
    // RMax[j] stores the maximum value
    // from (arr[j], arr[j+1], ..arr[n-1])
    RMax[n - 1] = arr[n - 1];
    for (j = n - 2; j >= 0; --j)
        RMax[j] = Math.max(arr[j], RMax[j + 1]);

    // Traverse both arrays from left
    // to right to find optimum j - i
    // This process is similar to merge()
    // of MergeSort
    i = 0;
    j = 0;
    maxDiff = -1;
    while (j < n && i < n)
    {
        if (LMin[i] < RMax[j])
        {
            maxDiff = Math.max(maxDiff, j - i);
            j = j + 1;
        }
        else
            i = i + 1;
    }

    return (maxDiff + 1);
}

// utility Function which subtracts X
// from all the elements in the array
function modifyarr(arr,n,x)
{
    for (let i = 0; i < n; i++)
        arr[i] = arr[i] - x;
}

// Calculating the prefix sum
// array of the modified array
function calcprefix(arr,n)
{
    let s = 0;
    for (let i = 0; i < n; i++)
    {
        s += arr[i];
        arr[i] = s;
    }
}

// Function to find the length of the
// longest subarray with average >= x
function longestsubarray(arr,n,x)
{
    modifyarr(arr, n, x);
    calcprefix(arr, n);

    return maxIndexDiff(arr, n);
}

// Driver code
let arr=[1, 1, 2, -1, -1, 1 ];
let x = 1;
let n = arr.length;
document.write(longestsubarray(arr, n, x));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)