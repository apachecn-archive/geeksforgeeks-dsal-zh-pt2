# 在给定的双音序列中找到双音点

> 原文:[https://www . geesforgeks . org/find-bitonic-point-给定-bitonic-sequence/](https://www.geeksforgeeks.org/find-bitonic-point-given-bitonic-sequence/)

给你一个双音素序列，任务是在其中找到**双音素点**。双调和数列是一个先严格递增，后严格递减的数列。
双调和点是双调和序列中的一个点，在此点之前元素严格增加，在此点之后元素严格减少。如果数组只是在减少或增加，那么双离子点是不存在的。
**示例:**

```
Input : arr[] = {6, 7, 8, 11, 9, 5, 2, 1}
Output: 11
All elements before 11 are smaller and all
elements after 11 are greater.

Input : arr[] = {-3, -2, 4, 6, 10, 8, 7, 1}
Output: 10
```

一个**简单的解决这个问题的方法**就是使用线性搜索。如果第 i-1 个和第 i+1 个元素都小于第 I 个元素，则元素 **arr[i]** 是双浊点。这种方法的时间复杂度为 0(n)。
针对这个问题的一个**高效解决方案**就是用**改装** [**二分搜索法**](https://www.geeksforgeeks.org/tag/binary-search/) 。

*   如果 **arr[mid-1] < arr[mid]** 和**arr[mid]>arr[mid+1]【T3]，那么我们就完成了比特点。**
*   如果 **arr[mid] < arr[mid+1]** 则在右子阵列中搜索，否则在左子阵列中搜索。

## C++

```
// C++ program to find bitonic point in a bitonic array.
#include<bits/stdc++.h>
using namespace std;

// Function to find bitonic point using binary search
int binarySearch(int arr[], int left, int right)
{
    if (left <= right)
    {
        int mid = (left+right)/2;

        // base condition to check if arr[mid] is
        // bitonic point or not
        if (arr[mid-1]<arr[mid] && arr[mid]>arr[mid+1])
            return mid;

        // We assume that sequence is bitonic. We go to
        // right subarray if middle point is part of
        // increasing subsequence. Else we go to left
        // subarray.
        if (arr[mid] < arr[mid+1])
            return binarySearch(arr, mid+1,right);
        else
            return binarySearch(arr, left, mid-1);
    }

    return -1;
}

// Driver program to run the case
int main()
{
    int arr[] = {6, 7, 8, 11, 9, 5, 2, 1};
    int n = sizeof(arr)/sizeof(arr[0]);
    int index = binarySearch(arr, 1, n-2);
    if (index != -1)
       cout << arr[index];
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find bitonic
// point in a bitonic array.

import java.io.*;

class GFG 
{
    // Function to find bitonic point 
    // using binary search
    static int binarySearch(int arr[], int left,
                                       int right)
    {
        if (left <= right)
        {
            int mid = (left + right) / 2;

            // base condition to check if arr[mid] 
            // is bitonic point or not
            if (arr[mid - 1] < arr[mid] && 
                   arr[mid] > arr[mid + 1])
                   return mid;

            // We assume that sequence is bitonic. We go to
            // right subarray if middle point is part of
            // increasing subsequence. Else we go to left
            // subarray.
            if (arr[mid] < arr[mid + 1])
                return binarySearch(arr, mid + 1, right);
            else
                return binarySearch(arr, left, mid - 1);
        }

        return -1;
    }

    // Driver program 
    public static void main (String[] args) 
    {
        int arr[] = {6, 7, 8, 11, 9, 5, 2, 1};
        int n = arr.length;
        int index = binarySearch(arr, 1, n - 2);
        if (index != -1)
        System.out.println ( arr[index]);

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 program to find bitonic 
# point in a bitonic array.

# Function to find bitonic point 
# using binary search
def binarySearch(arr, left, right):

    if (left <= right):

        mid = (left + right) // 2;

        # base condition to check if 
        # arr[mid] is bitonic point 
        # or not
        if (arr[mid - 1] < arr[mid] and arr[mid] > arr[mid + 1]):
            return mid;

        # We assume that sequence 
        # is bitonic. We go to right 
        # subarray if middle point 
        # is part of increasing 
        # subsequence. Else we go 
        # to left subarray.
        if (arr[mid] < arr[mid + 1]):
            return binarySearch(arr, mid + 1,right);
        else:
            return binarySearch(arr, left, mid - 1);

    return -1;

# Driver Code
arr = [6, 7, 8, 11, 9, 5, 2, 1];
n = len(arr);
index = binarySearch(arr, 1, n-2);
if (index != -1):
        print(arr[index]);

# This code is contributed by mits
```

## C#

```
// C# program to find bitonic
// point in a bitonic array.
using System;

class GFG 
{
    // Function to find bitonic point 
    // using binary search
    static int binarySearch(int []arr, int left,
                                      int right)
    {
        if (left <= right)
        {
            int mid = (left + right) / 2;

            // base condition to check if arr[mid] 
            // is bitonic point or not
            if (arr[mid - 1] < arr[mid] && 
                arr[mid] > arr[mid + 1])
                return mid;

            // We assume that sequence is bitonic. We go
            // to right subarray if middle point is part of
            // increasing subsequence. Else we go to left subarray.
            if (arr[mid] < arr[mid + 1])
                return binarySearch(arr, mid + 1, right);
            else
                return binarySearch(arr, left, mid - 1);
        }

        return -1;
    }

    // Driver program 
    public static void Main () 
    {
        int []arr = {6, 7, 8, 11, 9, 5, 2, 1};
        int n = arr.Length;
        int index = binarySearch(arr, 1, n - 2);
        if (index != -1)
        Console.Write ( arr[index]);
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find bitonic 
// point in a bitonic array.

// Function to find bitonic point 
// using binary search
function binarySearch($arr, $left, $right)
{
    if ($left <= $right)
    {
        $mid = ($left + $right) / 2;

        // base condition to check if 
        // arr[mid] is bitonic point 
        // or not
        if ($arr[$mid - 1] < $arr[$mid] && 
            $arr[$mid] > $arr[$mid + 1])
            return $mid;

        // We assume that sequence 
        // is bitonic. We go to right 
        // subarray if middle point 
        // is part of increasing 
        // subsequence. Else we go 
        // to left subarray.
        if ($arr[$mid] < $arr[$mid + 1])
            return binarySearch($arr, $mid + 1,$right);
        else
            return binarySearch($arr, $left, $mid - 1);
    }

    return -1;
}

    // Driver Code
    $arr = array(6, 7, 8, 11, 9, 5, 2, 1);
    $n = sizeof($arr);
    $index = binarySearch($arr, 1, $n-2);
    if ($index != -1)
        echo $arr[$index];

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// Javascript program to find bitonic
// point in a bitonic array.

// Function to find bitonic point
// using binary search
function binarySearch(arr , left,right)
{
    if (left <= right)
    {
        var mid = parseInt((left + right) / 2);

        // base condition to check if arr[mid] 
        // is bitonic point or not
        if (arr[mid - 1] < arr[mid] && 
               arr[mid] > arr[mid + 1])
               return mid;

        // We assume that sequence is bitonic. We go to
        // right subarray if middle point is part of
        // increasing subsequence. Else we go to left
        // subarray.
        if (arr[mid] < arr[mid + 1])
            return binarySearch(arr, mid + 1, right);
        else
            return binarySearch(arr, left, mid - 1);
    }

    return -1;
}

// Driver program 
var arr = [6, 7, 8, 11, 9, 5, 2, 1];
var n = arr.length;
var index = binarySearch(arr, 1, n - 2);
if (index != -1)
document.write( arr[index]);

// This code is contributed by Amit Katiyar 

</script>
```

**输出:**

```
11
```

**时间复杂度:** O(Log n)
本文由 [**Shashank Mishra(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。