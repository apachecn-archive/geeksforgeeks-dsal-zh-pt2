# 在数组中找到一个局部极小值

> 原文:[https://www.geeksforgeeks.org/find-local-minima-array/](https://www.geeksforgeeks.org/find-local-minima-array/)

给定数组 arr[0..**的 n-1】个不同的**整数，任务是在其中找到一个局部极小值。我们说，如果一个元素 arr[x]小于它的两个邻居，那么它就是一个局部最小值。

*   对于角元素，我们只需要考虑一个邻居进行比较。
*   一个数组中可以有多个局部极小值，我们需要找到其中一个。

示例:

```
Input: arr[] = {9, 6, 3, 14, 5, 7, 4};
Output: Index of local minima is 2
The output prints index of 3 because it is 
smaller than both of its neighbors. 
Note that indexes of elements 5 and 4 are 
also valid outputs.

Input: arr[] = {23, 8, 15, 2, 3};
Output: Index of local minima is 1

Input: arr[] = {1, 2, 3};
Output: Index of local minima is 0

Input: arr[] = {3, 2, 1};
Output: Index of local minima is 2
```

一个**简单的解决方案**是对数组做一个线性扫描，只要我们找到一个局部最小值，我们就返回它。这种方法最差的时间复杂度是 O(n)。
一个**高效解决方案**基于[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。我们将中间元素与其邻居进行比较。如果中间元素不大于它的任何邻居，那么我们返回它。如果中间元素大于它的左邻，那么在左半部分总是有一个局部极小值(为什么？举几个例子)。如果中间元素大于它的右邻居，那么在右半部分总是有一个局部最小值(由于与左半部分相同的原因)。
以下是上述思路的实现:

## C++

```
// A C++ program to find a local minima in an array
#include <stdio.h>

// A binary search based function that returns
// index of a local minima.
int localMinUtil(int arr[], int low, int high, int n)
{
    // Find index of middle element
    int mid = low + (high - low)/2;  /* (low + high)/2 */

    // Compare middle element with its neighbours
    // (if neighbours exist)
    if ((mid == 0 || arr[mid-1] > arr[mid]) &&
            (mid == n-1 || arr[mid+1] > arr[mid]))
        return mid;

    // If middle element is not minima and its left
    // neighbour is smaller than it, then left half
    // must have a local minima.
    else if (mid > 0 && arr[mid-1] < arr[mid])
        return localMinUtil(arr, low, (mid -1), n);

    // If middle element is not minima and its right
    // neighbour is smaller than it, then right half
    // must have a local minima.
    return localMinUtil(arr, (mid + 1), high, n);
}

// A wrapper over recursive function localMinUtil()
int localMin(int arr[], int n)
{
    return localMinUtil(arr, 0, n-1, n);
}

/* Driver program to check above functions */
int main()
{
    int arr[] = {4, 3, 1, 14, 16, 40};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("Index of a local minima is %d",
                           localMin(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find a local minima in an array
import java.io.*;

class GFG
{

    // A binary search based function that returns
    // index of a local minima.
    public static int localMinUtil(int[] arr, int low,
                                   int high, int n)
    {

        // Find index of middle element
        int mid = low + (high - low) / 2;

         // Compare middle element with its neighbours
        // (if neighbours exist)
        if(mid == 0 || arr[mid - 1] > arr[mid] && mid == n - 1 ||
           arr[mid] < arr[mid + 1])
                return mid;

        // If middle element is not minima and its left
        // neighbour is smaller than it, then left half
        // must have a local minima.
        else if(mid > 0 && arr[mid - 1] < arr[mid])
                return localMinUtil(arr, low, mid - 1, n);

        // If middle element is not minima and its right
        // neighbour is smaller than it, then right half
        // must have a local minima.
        return localMinUtil(arr, mid + 1, high, n);
    }

    // A wrapper over recursive function localMinUtil()
    public static int localMin(int[] arr, int n)
    {
        return localMinUtil(arr, 0, n - 1, n);
    }

    public static void main (String[] args)
    {

        int arr[] = {4, 3, 1, 14, 16, 40};
        int n = arr.length;
        System.out.println("Index of a local minima is " + localMin(arr, n));

    }
}

//This code is contributed by Dheerendra Singh
```

## 蟒蛇 3

```
# Python3 program to find a
# local minima in an array

# A binary search based function that
# returns index of a local minima.
def localMinUtil(arr, low, high, n):

    # Find index of middle element
    mid = low + (high - low) // 2 

    # Compare middle element with its
    # neighbours (if neighbours exist)
    if(mid == 0 or arr[mid - 1] > arr[mid] and
       mid == n - 1 or arr[mid] < arr[mid + 1]):
        return mid

    # If middle element is not minima and its left
    # neighbour is smaller than it, then left half
    # must have a local minima.
    elif(mid > 0 and arr[mid - 1] < arr[mid]):
        return localMinUtil(arr, low, mid - 1, n)

    # If middle element is not minima and its right
    # neighbour is smaller than it, then right half
    # must have a local minima.
    return localMinUtil(arr, mid + 1, high, n)

# A wrapper over recursive function localMinUtil()
def localMin(arr, n):

    return localMinUtil(arr, 0, n - 1, n)

# Driver code
arr = [4, 3, 1, 14, 16, 40]
n = len(arr)
print("Index of a local minima is " ,
                    localMin(arr, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// A C# program to find a
// local minima in an array
using System;

class GFG
{

    // A binary search based function that returns
    // index of a local minima.
    public static int localMinUtil(int[] arr, int low,
                                   int high, int n)
    {

        // Find index of middle element
        int mid = low + (high - low) / 2;

        // Compare middle element with its neighbours
        // (if neighbours exist)
        if(mid == 0 || arr[mid - 1] > arr[mid] &&
           mid == n - 1 || arr[mid] < arr[mid + 1])
                return mid;

        // If middle element is not minima and its left
        // neighbour is smaller than it, then left half
        // must have a local minima.
        else if(mid > 0 && arr[mid - 1] < arr[mid])
                return localMinUtil(arr, low, mid - 1, n);

        // If middle element is not minima and its right
        // neighbour is smaller than it, then right half
        // must have a local minima.
        return localMinUtil(arr, mid + 1, high, n);
    }

    // A wrapper over recursive function localMinUtil()
    public static int localMin(int[] arr, int n)
    {
        return localMinUtil(arr, 0, n - 1, n);
    }

    // Driver Code
    public static void Main ()
    {

        int []arr = {4, 3, 1, 14, 16, 40};
        int n = arr.Length;
        Console.WriteLine("Index of a local minima is " +
                            localMin(arr, n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find a
// local minima in an array

// A binary search based
// function that returns
// index of a local minima.
function localMinUtil($arr, $low, $high, $n)
{

    // Find index of middle element
    /* (low + high)/2 */
    $mid = $low + ($high - $low) / 2;

    // Compare middle element
    // with its neighbours
    // (if neighbours exist)
    if (($mid == 0 or $arr[$mid - 1] > $arr[$mid]) and
        ($mid == $n - 1 or $arr[$mid + 1] > $arr[$mid]))
        return $mid;

    // If middle element is not
    // minima and its left
    // neighbour is smaller than
    // it, then left half
    // must have a local minima.
    else if ($mid > 0 and $arr[$mid - 1] < $arr[$mid])
        return localMinUtil($arr, $low, ($mid - 1), $n);

    // If middle element is not
    // minima and its right
    // neighbour is smaller than
    // it, then right half
    // must have a local minima.
    return localMinUtil(arr, (mid + 1), high, n);
}

// A wrapper over recursive
// function localMinUtil()
function localMin( $arr, $n)
{
    return floor(localMinUtil($arr, 0, $n - 1, $n));
}

    // Driver Code
    $arr = array(4, 3, 1, 14, 16, 40);
    $n = count($arr);
    echo "Index of a local minima is ",
                    localMin($arr, $n);

// This code is contributed by anuj_67.
?>
```

输出:

```
Index of a local minima is 2
```

时间复杂度:O(Log n)
**相关问题:**
[**找个峰元素**](https://www.geeksforgeeks.org/find-a-peak-in-a-given-array/)
本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。