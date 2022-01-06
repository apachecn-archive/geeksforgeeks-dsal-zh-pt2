# 两个子阵列异或值的最小绝对差

> 原文:[https://www . geeksforgeeks . org/最小值-绝对差-异或-值-两个子数组/](https://www.geeksforgeeks.org/minimum-absolute-difference-xor-values-two-subarrays/)

给定一个包含 **n 个**数字的数组。问题是将阵列分成两个子阵列，使得两个子阵列的 xor 值的绝对差最小。
**注:**阵中至少包含 2 个数字。

示例:

```
Input : arr[] = {12, 6, 20, 14, 38, 6}
Output : 16
The two subarrays are:
{12, 6, 20} = 12 ^ 6 ^ 20 = 30
{14, 38, 6} = 14 ^ 38 ^ 6 = 46
Absolute difference = abs(30-46) 
                    = 16

Input : arr[] = {10, 16, 9, 34, 7, 46, 23}
Output : 1
```

**简单方法:**使用两个 for 循环找到两个子阵列的 xor 值 **sub_arr1[1..i]** 和 **sub_arr2[i+1..n]** 对于每一个 **i** = 1 到 n-1。找到它们的绝对差，并相应地更新最小绝对差。
时间复杂度:O(n <sup>2</sup> )

**有效方法:**它基于 **^(xor)** 算子的以下属性:

1.  a ^ 0 = a。
2.  a ^ a = 0。

**算法:**

```
minDiffBtwXorValues(arr, n)
    Declare tot_xor = 0
    for i = 0 to n-1
        tot_xor ^= arr[i]

    Declare part_xor = 0
    Declare min = Maximum Integer

    for i = 0 to n-2    
        tot_xor ^= arr[i]
    part_xor ^= arr[i]
    if abs(tot_xor - part_xor) < min
        min = abs(tot_xor - part_xor)

    return min
```

## C++

```
// C++ implementation to find the minimum
// absolute difference of the xor values
// of the two subarrays
#include <bits/stdc++.h>
using namespace std;

// function to find the minimum absolute
// difference of the xor values of the
// two subarrays
int minDiffBtwXorValues(int arr[], int n)
{
    // to store the xor value of the
    // entire array
    int tot_xor = 0;
    for (int i = 0; i < n; i++)
        tot_xor ^= arr[i];

    // 'part_xor' to store the xor value
    // of some subarray
    int part_xor = 0, min = INT_MAX;

    for (int i = 0; i < n - 1; i++) {

        // removing the xor value of the
        // subarray [0..i] form 'tot_xor',
        // i.e, it will contain the xor
        // value of the subarray [i+1..n-1]
        tot_xor ^= arr[i];

        // calculating the xor value of the
        // subarray [0..i]
        part_xor ^= arr[i];

        // if absolute difference is minimum,
        // then update 'min'
        if (abs(tot_xor - part_xor) < min)
            min = abs(tot_xor - part_xor);
    }

    // required minimum absolute difference
    return min;
}

// Driver program to test above
int main()
{
    int arr[] = { 12, 6, 20, 14, 38, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Minimum Absolute Difference = "
         << minDiffBtwXorValues(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// find the minimum
// absolute difference
// of the xor values
// of the two subarrays

import java.util.*;
import java.lang.*;

public class GfG{

    // function to find
    // the minimum absolute
    // difference of the
    // xor values of the
    // two subarrays
    public static int minDiffBtwXorValues(int arr[],
    int n)
    {
        // to store the xor value of the
        // entire array
        int tot_xor = 0;
        for (int i = 0; i < n; i++)
            tot_xor ^= arr[i];

        // 'part_xor' to store the xor value
        // of some subarray
        int part_xor = 0, min = Integer.MAX_VALUE;

        for (int i = 0; i < n - 1; i++) {

            // removing the xor value of the
            // subarray [0..i] form 'tot_xor',
            // i.e, it will contain the xor
            // value of the subarray [i+1..n-1]
            tot_xor ^= arr[i];

            // calculating the xor value of the
            // subarray [0..i]
            part_xor ^= arr[i];

            // if absolute difference is minimum,
            // then update 'min'
            if (Math.abs(tot_xor - part_xor) < min)
                min = Math.abs(tot_xor - part_xor);
        }

        // required minimum absolute difference
        return min;
    }

    // Driver function
    public static void main(String argc[]){

        int arr[] = { 12, 6, 20, 14, 38, 6 };
        int n = 6;
        System.out.println("Minimum Absolute Difference = " +
        minDiffBtwXorValues(arr, n));
    }

}

// This code is contributed by Sagar Shukla
```

## 计算机编程语言

```
# Python implementation to find the minimum
# absolute difference of the xor values
# of the two subarrays

import sys

# function to find the minimum absolute
# difference of the xor values of the
# two subarrays
def minDiffBtwXorValues(arr, n):

    # to store the xor value of the
    # entire array
    tot_xor = 0

    for i in range(n):
        tot_xor ^= arr[i]

    # 'part_xor' to store the xor value
    # of some subarray
    part_xor = 0
    min = sys.maxint

    for i in range(n - 1):

        # removing the xor value of the
        # subarray [0..i] form 'tot_xor',
        # i.e, it will contain the xor
        # value of the subarray [i+1..n-1]
        tot_xor ^= arr[i]

        # calculating the xor value of the
        # subarray [0..i]
        part_xor ^= arr[i]

        # if absolute difference is minimum,
        # then update 'min'
        if (abs(tot_xor - part_xor) < min):
            min = abs(tot_xor - part_xor)

    # required minimum absolute difference
    return min

# Driver program to test above
arr = [ 12, 6, 20, 14, 38, 6 ]
n = len(arr)
print "Minimum Absolute Difference =", minDiffBtwXorValues(arr, n)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# implementation to
// find the minimum
// absolute difference
// of the xor values
// of the two subarrays
using System;

class GFG {

    // function to find
    // the minimum absolute
    // difference of the
    // xor values of the
    // two subarrays
    public static int minDiffBtwXorValues(int[] arr,
                                              int n)
    {
        // to store the xor value of the
        // entire array
        int tot_xor = 0;
        for (int i = 0; i < n; i++)
            tot_xor ^= arr[i];

        // 'part_xor' to store the xor value
        // of some subarray
        int part_xor = 0, min = int.MaxValue;

        for (int i = 0; i < n - 1; i++) {

            // removing the xor value of the
            // subarray [0..i] form 'tot_xor',
            // i.e, it will contain the xor
            // value of the subarray [i+1..n-1]
            tot_xor ^= arr[i];

            // calculating the xor value of the
            // subarray [0..i]
            part_xor ^= arr[i];

            // if absolute difference is minimum,
            // then update 'min'
            if (Math.Abs(tot_xor - part_xor) < min)
                min = Math.Abs(tot_xor - part_xor);
        }

        // required minimum absolute difference
        return min;
    }

    // Driver function
    public static void Main()
    {

        int[] arr = { 12, 6, 20, 14, 38, 6 };
        int n = 6;
        Console.WriteLine("Minimum Absolute Difference = " +
                               minDiffBtwXorValues(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the minimum
// absolute difference of the xor values
// of the two subarrays

// function to find the minimum absolute
// difference of the xor values of the
// two subarrays
function minDiffBtwXorValues($arr, $n)
{

    // to store the xor value
    // of the entire array
    $tot_xor = 0;

    for ($i = 0; $i < $n; $i++)
        $tot_xor ^= $arr[$i];

    // 'part_xor' to store the
    // xor value of some subarray
    $part_xor = 0; $min = PHP_INT_MAX;

    for ( $i = 0; $i < $n - 1; $i++)
    {

        // removing the xor value of the
        // subarray [0..i] form 'tot_xor',
        // i.e, it will contain the xor
        // value of the subarray [i+1..n-1]
        $tot_xor ^= $arr[$i];

        // calculating the xor value
        // of the subarray [0..i]
        $part_xor ^= $arr[$i];

        // if absolute difference is
        // minimum, then update 'min'
        if (abs($tot_xor - $part_xor) < $min)
            $min = abs($tot_xor - $part_xor);
    }

    // required minimum
    // absolute difference
    return $min;
}

    // Driver Code
    $arr = array(12, 6, 20, 14, 38, 6);
    $n = count($arr);
    echo "Minimum Absolute Difference = "
        , minDiffBtwXorValues($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum absolute difference of the xor
// values of the two subarrays

// Function to find the minimum absolute
// difference of the xor values of the
// two subarrays
function minDiffBtwXorValues(arr, n)
{

    // To store the xor value of the
    // entire array
    let tot_xor = 0;
    for(let i = 0; i < n; i++)
        tot_xor ^= arr[i];

    // 'part_xor' to store the xor value
    // of some subarray
    let part_xor = 0, min = Number.MAX_VALUE;

    for(let i = 0; i < n - 1; i++)
    {

        // Removing the xor value of the
        // subarray [0..i] form 'tot_xor',
        // i.e, it will contain the xor
        // value of the subarray [i+1..n-1]
        tot_xor ^= arr[i];

        // Calculating the xor value of the
        // subarray [0..i]
        part_xor ^= arr[i];

        // If absolute difference is minimum,
        // then update 'min'
        if (Math.abs(tot_xor - part_xor) < min)
            min = Math.abs(tot_xor - part_xor);
    }

    // Required minimum absolute difference
    return min;
}

// Driver code
let arr = [ 12, 6, 20, 14, 38, 6 ];
let n = arr.length;

document.write("Minimum Absolute Difference = " +
               minDiffBtwXorValues(arr, n));

// This code is contributed by subham348

</script>
```

输出:

```
Minimum Absolute Difference = 16
```

时间复杂度:0(n)

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。