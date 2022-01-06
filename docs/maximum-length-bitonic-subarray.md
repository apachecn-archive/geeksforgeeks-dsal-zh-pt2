# 最大长度双离子子阵列|集合 1 (O(n)时间和 O(n)空间)

> 原文:[https://www . geesforgeks . org/maximum-length-bitonic-subarray/](https://www.geeksforgeeks.org/maximum-length-bitonic-subarray/)

给定一个包含 n 个正整数的数组 A[0 … n-1]，如果有一个带有 I 的 k<= k <= j such that A[i] <= A[i + 1] … = A[k + 1] >=,则子数组 A[i … j]是双调和的..A[j–1]> = A[j]。编写一个函数，以数组为参数，返回最大长度的二次子数组的长度。
解的期望时间复杂度为 O(n)
*简单示例*
**1)** A[] = {12，4，78，90，45，23}，最大长度双子阵为{4，78，90，45，23}，长度为 5。
**2)** A[] = {20，4，1，2，3，4，2，10}，最大长度双子阵为{1，2，3，4，2}，长度为 5。
*极端示例*
**1)** A[] = {10}，单个元素为双音素，所以输出为 1。
**2)** A[] = {10，20，30，40}，完整的数组本身是双音素的，所以输出是 4。
**3)** A[] = {40，30，20，10}，完整的数组本身是双音素的，所以输出是 4。

**解**
让我们考虑一下数组{12，4，78，90，45，23}来理解解。
1)从左到右构建一个辅助数组 inc[]，使得 inc[i]包含以 arr[i]结束的非减子数组的长度。
对于 A[] = {12，4，78，90，45，23}，inc[]是{1，1，2，3，1，1}
2)从右向左构造另一个数组 dec[]，使得 dec[i]包含从 arr[i]开始的非递增子数组的长度。
对于 A[] = {12，4，78，90，45，23}，dec[]为{2，1，1，3，2，1}。
3)一旦有了 inc[]和 dec[]阵列，我们需要做的就是找到(Inc[I]+dec[I]–1 的最大值。
对于{12，4，78，90，45，23}，(Inc[I]+dec[I]–1)的最大值对于 i = 3 为 5。

## C++

```
// C++ program to find length of
// the longest bitonic subarray
#include <bits/stdc++.h>
using namespace std;

int bitonic(int arr[], int n)
{
    // Length of increasing subarray
    // ending at all indexes
    int inc[n];

    // Length of decreasing subarray
    // starting at all indexes
    int dec[n];
    int i, max;

    // length of increasing sequence
    // ending at first index is 1
    inc[0] = 1;

    // length of increasing sequence
    // starting at first index is 1
    dec[n-1] = 1;

    // Step 1) Construct increasing sequence array
    for (i = 1; i < n; i++)
    inc[i] = (arr[i] >= arr[i-1])? inc[i-1] + 1: 1;

    // Step 2) Construct decreasing sequence array
    for (i = n-2; i >= 0; i--)
    dec[i] = (arr[i] >= arr[i+1])? dec[i+1] + 1: 1;

    // Step 3) Find the length of
    // maximum length bitonic sequence
    max = inc[0] + dec[0] - 1;
    for (i = 1; i < n; i++)
        if (inc[i] + dec[i] - 1 > max)
            max = inc[i] + dec[i] - 1;

    return max;
}

/* Driver code */
int main()
{
    int arr[] = {12, 4, 78, 90, 45, 23};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "nLength of max length Bitonic Subarray is " << bitonic(arr, n);
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// C program to find length of the longest bitonic subarray
#include<stdio.h>
#include<stdlib.h>

int bitonic(int arr[], int n)
{
    int inc[n]; // Length of increasing subarray ending at all indexes
    int dec[n]; // Length of decreasing subarray starting at all indexes
    int i, max;

    // length of increasing sequence ending at first index is 1
    inc[0] = 1;

    // length of increasing sequence starting at first index is 1
    dec[n-1] = 1;

    // Step 1) Construct increasing sequence array
    for (i = 1; i < n; i++)
       inc[i] = (arr[i] >= arr[i-1])? inc[i-1] + 1: 1;

    // Step 2) Construct decreasing sequence array
    for (i = n-2; i >= 0; i--)
       dec[i] = (arr[i] >= arr[i+1])? dec[i+1] + 1: 1;

    // Step 3) Find the length of maximum length bitonic sequence
    max = inc[0] + dec[0] - 1;
    for (i = 1; i < n; i++)
        if (inc[i] + dec[i] - 1 > max)
            max = inc[i] + dec[i] - 1;

    return max;
}

/* Driver program to test above function */
int main()
{
    int arr[] = {12, 4, 78, 90, 45, 23};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("nLength of max length Bitonic Subarray is %d",
            bitonic(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of the longest bitonic subarray
import java.io.*;
import java.util.*;

class Bitonic
{
    static int bitonic(int arr[], int n)
    {
        int[] inc = new int[n]; // Length of increasing subarray ending
                                // at all indexes
        int[] dec = new int[n]; // Length of decreasing subarray starting
                                // at all indexes
        int max;

        // Length of increasing sequence ending at first index is 1
        inc[0] = 1;

        // Length of increasing sequence starting at first index is 1
        dec[n-1] = 1;

        // Step 1) Construct increasing sequence array
        for (int i = 1; i < n; i++)
           inc[i] = (arr[i] >= arr[i-1])? inc[i-1] + 1: 1;

        // Step 2) Construct decreasing sequence array
        for (int i = n-2; i >= 0; i--)
            dec[i] = (arr[i] >= arr[i+1])? dec[i+1] + 1: 1;

        // Step 3) Find the length of maximum length bitonic sequence
        max = inc[0] + dec[0] - 1;
        for (int i = 1; i < n; i++)
            if (inc[i] + dec[i] - 1 > max)
                max = inc[i] + dec[i] - 1;

        return max;
    }

    /*Driver function to check for above function*/
    public static void main (String[] args)
    {
        int arr[] = {12, 4, 78, 90, 45, 23};
        int n = arr.length;
        System.out.println("Length of max length Bitnoic Subarray is "
                            + bitonic(arr, n));
    }
}
/* This code is contributed by Devesh Agrawal */
```

## 计算机编程语言

```
# Python program to find length of the longest bitonic subarray

def bitonic(arr, n):

    # Length of increasing subarray ending at all indexes
    inc = [None] * n

    # Length of decreasing subarray starting at all indexes
    dec = [None] * n

    # length of increasing sequence ending at first index is 1
    inc[0] = 1

    # length of increasing sequence starting at first index is 1
    dec[n-1] = 1

    # Step 1) Construct increasing sequence array
    for i in range(n):
        if arr[i] >= arr[i-1]:
            inc[i] = inc[i-1] + 1
        else:
            inc[i] = 1

    # Step 2) Construct decreasing sequence array
    for i in range(n-2,-1,-1):
        if arr[i] >= arr[i-1]:
            dec[i] = inc[i-1] + 1
        else:
            dec[i] = 1

    # Step 3) Find the length of maximum length bitonic sequence
    max = inc[0] + dec[0] - 1
    for i in range(n):
        if inc[i] + dec[i] - 1 > max:
            max = inc[i] + dec[i] - 1

    return max

# Driver program to test above function

arr = [12, 4, 78, 90, 45, 23]
n = len(arr)
print("nLength of max length Bitonic Subarray is ",bitonic(arr, n))
```

## C#

```
// C# program to find length of the
// longest bitonic subarray
using System;

class GFG
{
    static int bitonic(int []arr, int n)
    {
        // Length of increasing subarray ending
        // at all indexes
        int[] inc = new int[n];

        // Length of decreasing subarray starting
        // at all indexes
        int[] dec = new int[n];

        int max;

        // Length of increasing sequence
        // ending at first index is 1
        inc[0] = 1;

        // Length of increasing sequence
        // starting at first index is 1
        dec[n - 1] = 1;

        // Step 1) Construct increasing sequence array
        for (int i = 1; i < n; i++)
        inc[i] = (arr[i] >= arr[i - 1]) ?
                 inc[i - 1] + 1: 1;

        // Step 2) Construct decreasing sequence array
        for (int i = n - 2; i >= 0; i--)
            dec[i] = (arr[i] >= arr[i + 1]) ?
                     dec[i + 1] + 1: 1;

        // Step 3) Find the length of maximum
        // length bitonic sequence
        max = inc[0] + dec[0] - 1;
        for (int i = 1; i < n; i++)
            if (inc[i] + dec[i] - 1 > max)
                max = inc[i] + dec[i] - 1;

        return max;
    }

    // Driver function
    public static void Main ()
    {
        int []arr = {12, 4, 78, 90, 45, 23};
        int n = arr.Length;
        Console.Write("Length of max length Bitonic Subarray is "
                      + bitonic(arr, n));
    }
}
// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length of
// the longest bitonic subarray

function bitonic($arr, $n)
{
    $i; $max;
    // length of increasing sequence
    // ending at first index is 1
    $inc[0] = 1;

    // length of increasing sequence
    // starting at first index is 1
    $dec[$n - 1] = 1;

    // Step 1) Construct increasing
    // sequence array
    for ($i = 1; $i < $n; $i++)
    $inc[$i] = ($arr[$i] >= $arr[$i - 1]) ?
                          $inc[$i - 1] + 1: 1;

    // Step 2) Construct decreasing
    // sequence array
    for ($i = $n - 2; $i >= 0; $i--)
    $dec[$i] = ($arr[$i] >= $arr[$i + 1]) ?
                          $dec[$i + 1] + 1: 1;

    // Step 3) Find the length of
    // maximum length bitonic sequence
    $max = $inc[0] + $dec[0] - 1;
    for ($i = 1; $i < $n; $i++)
        if ($inc[$i] + $dec[$i] - 1 > $max)
            $max = $inc[$i] + $dec[$i] - 1;

    return $max;
}

// Driver Code
$arr = array(12, 4, 78, 90, 45, 23);
$n = sizeof($arr);
echo "Length of max length Bitonic " .
     "Subarray is ", bitonic($arr, $n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

    // Javascript program to find length of the
    // longest bitonic subarray

    function bitonic(arr, n)
    {
        // Length of increasing subarray ending
        // at all indexes
        let inc = new Array(n);

        // Length of decreasing subarray starting
        // at all indexes
        let dec = new Array(n);

        let max;

        // Length of increasing sequence
        // ending at first index is 1
        inc[0] = 1;

        // Length of increasing sequence
        // starting at first index is 1
        dec[n - 1] = 1;

        // Step 1) Construct increasing sequence array
        for (let i = 1; i < n; i++)
            inc[i] = (arr[i] >= arr[i - 1]) ? inc[i - 1] + 1: 1;

        // Step 2) Construct decreasing sequence array
        for (let i = n - 2; i >= 0; i--)
            dec[i] = (arr[i] >= arr[i + 1]) ? dec[i + 1] + 1: 1;

        // Step 3) Find the length of maximum
        // length bitonic sequence
        max = inc[0] + dec[0] - 1;
        for (let i = 1; i < n; i++)
            if (inc[i] + dec[i] - 1 > max)
                max = inc[i] + dec[i] - 1;

        return max;
    }

    let arr = [12, 4, 78, 90, 45, 23];
    let n = arr.length;
    document.write("Length of max length Bitonic Subarray is " + bitonic(arr, n));

</script>
```

**Output**

```
nLength of max length Bitonic Subarray is 5
```

**输出:**

```
Length of max length Bitnoic Subarray is 5
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

[最大长度双离子子阵列|设置 2 (O(n)时间和 O(1)空间)](https://www.geeksforgeeks.org/maximum-length-bitonic-subarray-set-2-time-o1-space/)
作为练习，将上述实现扩展为也打印最长的双离子子阵列。上面的实现只返回这种子阵列的长度。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。