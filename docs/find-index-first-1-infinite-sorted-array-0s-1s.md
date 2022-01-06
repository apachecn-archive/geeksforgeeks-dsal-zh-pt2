# 在 0 和 1 的无限排序数组中找到第一个 1 的索引

> 原文:[https://www . geesforgeks . org/find-index-first-1-无限排序-array-0s-1s/](https://www.geeksforgeeks.org/find-index-first-1-infinite-sorted-array-0s-1s/)

给定一个由 0 和 1 组成的无限排序数组。问题是找到该数组中第一个“1”的索引。由于数组是无限的，因此可以保证数组中会出现数字“1”。
**例:**

```
Input : arr[] = {0, 0, 1, 1, 1, 1} 
Output : 2

Input : arr[] = {1, 1, 1, 1,, 1, 1}
Output : 0
```

**处理方法:**这个问题与[在无穷多个排序数组](https://www.geeksforgeeks.org/find-position-element-sorted-array-infinite-numbers/)中寻找元素位置的问题密切相关。由于数组是无限的，因此我们不知道上下限，我们必须找到第一个“1”的出现。下面是一个求上下界的算法。
**算法:**

```
posOfFirstOne(arr)
    Declare l = 0, h = 1
    while arr[h] == 0
        l = h
    h = 2*h;
    return indexOfFirstOne(arr, l, h)
}
```

这里 **h** 和 **l** 是要求的上下限。**indexofferstone(arr，l，h)** 用于寻找这两个界限之间第一个‘1’的出现指数。参考[这个](https://www.geeksforgeeks.org/find-index-first-1-sorted-array-0s-1s/)岗位。

## C++

```
// C++ implementation to find the index of first 1
// in an infinite sorted array of 0's and 1's
#include <bits/stdc++.h>
using namespace std;

// function to find the index of first '1'
// binary search technique is applied
int indexOfFirstOne(int arr[], int low, int high)
{
    int mid;
    while (low <= high) {
        mid = (low + high) / 2;

        // if true, then 'mid' is the index of first '1'
        if (arr[mid] == 1 &&
            (mid == 0 || arr[mid - 1] == 0))
            break;

        // first '1' lies to the left of 'mid'
        else if (arr[mid] == 1)
            high = mid - 1;

        // first '1' lies to the right of 'mid'
        else
            low = mid + 1;
    }

    // required index
    return mid;
}

// function to find the index of first 1 in
// an infinite sorted array of 0's and 1's
int posOfFirstOne(int arr[])
{
    // find the upper and lower bounds between
    // which the first '1' would be present
    int l = 0, h = 1;

    // as the array is being considered infinite
    // therefore 'h' index will always exist in
    // the array
    while (arr[h] == 0) {

        // lower bound
        l = h;

        // upper bound
        h = 2 * h;
    }

    // required index of first '1'
    return indexOfFirstOne(arr, l, h);
}

// Driver program to test above
int main()
{
    int arr[] = { 0, 0, 1, 1, 1, 1 };
    cout << "Index = "
         << posOfFirstOne(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code For Find the index of first 1
// in an infinite sorted array of 0s and 1s
import java.util.*;

class GFG {

    // function to find the index of first '1'
    // binary search technique is applied
    public static int indexOfFirstOne(int arr[],
                                   int low, int high)
    {
        int mid=0;
        while (low <= high) {
            mid = (low + high) / 2;

            // if true, then 'mid' is the index of
            // first '1'
            if (arr[mid] == 1 &&
                (mid == 0 || arr[mid - 1] == 0))
                break;

            // first '1' lies to the left of 'mid'
            else if (arr[mid] == 1)
                high = mid - 1;

            // first '1' lies to the right of 'mid'
            else
                low = mid + 1;
        }

        // required index
        return mid;
    }

    // function to find the index of first 1 in
    // an infinite sorted array of 0's and 1's
    public static int posOfFirstOne(int arr[])
    {
        // find the upper and lower bounds
        // between which the first '1' would
        // be present
        int l = 0, h = 1;

        // as the array is being considered
        // infinite therefore 'h' index will
        // always exist in the array
        while (arr[h] == 0) {

            // lower bound
            l = h;

            // upper bound
            h = 2 * h;
        }

        // required index of first '1'
        return indexOfFirstOne(arr, l, h);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {

        int arr[] = { 0, 0, 1, 1, 1, 1 };
        System.out.println("Index = " +
                          posOfFirstOne(arr));

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python 3 implementation to find the
# index of first 1 in an infinite
# sorted array of 0's and 1's

# function to find the index of first
# '1' binary search technique is applied
def indexOfFirstOne(arr, low, high) :

    while (low <= high) :
        mid = (low + high) // 2

        # if true, then 'mid' is the index
        # of first '1'
        if (arr[mid] == 1 and (mid == 0 or
                       arr[mid - 1] == 0)) :
            break

        # first '1' lies to the left of 'mid'
        elif (arr[mid] == 1) :
            high = mid - 1

        # first '1' lies to the right of 'mid'
        else :
            low = mid + 1

    # required index
    return mid

# function to find the index of first
# 1 in an infinite sorted array of 0's
# and 1's
def posOfFirstOne(arr) :

    # find the upper and lower bounds between
    # which the first '1' would be present
    l = 0
    h = 1

    # as the array is being considered infinite
    # therefore 'h' index will always exist in
    # the array
    while (arr[h] == 0) :

        # lower bound
        l = h

        # upper bound
        h = 2 * h

    # required index of first '1'
    return indexOfFirstOne(arr, l, h)

# Driver program
arr = [ 0, 0, 1, 1, 1, 1 ]
print( "Index = ", posOfFirstOne(arr))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Code For Find the index of first 1
// in an infinite sorted array of 0's and 1's
using System;

class GFG {

    // function to find the index of first '1'
    // binary search technique is applied
    public static int indexOfFirstOne(int[] arr,
                              int low, int high)
    {
        int mid = 0;
        while (low <= high) {
            mid = (low + high) / 2;

            // if true, then 'mid' is the index of
            // first '1'
            if (arr[mid] == 1 && (mid == 0 || arr[mid - 1] == 0))
                break;

            // first '1' lies to the left of 'mid'
            else if (arr[mid] == 1)
                high = mid - 1;

            // first '1' lies to the right of 'mid'
            else
                low = mid + 1;
        }

        // required index
        return mid;
    }

    // function to find the index of first 1 in
    // an infinite sorted array of 0's and 1's
    public static int posOfFirstOne(int[] arr)
    {
        // find the upper and lower bounds
        // between which the first '1' would
        // be present
        int l = 0, h = 1;

        // as the array is being considered
        // infinite therefore 'h' index will
        // always exist in the array
        while (arr[h] == 0) {

            // lower bound
            l = h;

            // upper bound
            h = 2 * h;
        }

        // required index of first '1'
        return indexOfFirstOne(arr, l, h);
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int[] arr = { 0, 0, 1, 1, 1, 1 };
        Console.Write("Index = " + posOfFirstOne(arr));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// the index of first 1 in an
// infinite sorted array of
// 0's and 1's

// function to find the index
// of first '1' binary search
// technique is applied
function indexOfFirstOne($arr, $low, $high)
{
    $mid;
    while ($low <= $high)
    {
        $mid = ($low + $high) / 2;

        // if true, then 'mid' is
        // the index of first '1'
        if ($arr[$mid] == 1 and
            ($mid == 0 or $arr[$mid - 1] == 0))
            break;

        // first '1' lies to
        // the left of 'mid'
        else if ($arr[$mid] == 1)
            $high = $mid - 1;

        // first '1' lies to
        // the right of 'mid'
        else
            $low = $mid + 1;
    }

    // required index
    return ceil($mid);
}

// function to find the index of
// first 1 in an infinite sorted
// array of 0's and 1's
function posOfFirstOne($arr)
{
    // find the upper and lower
    // bounds between which the
    // first '1' would be present
    $l = 0; $h = 1;

    // as the array is being considered
    // infinite therefore 'h' index will
    // always exist in the array
    while ($arr[$h] == 0)
    {

        // lower bound
        $l = $h;

        // upper bound
        $h = 2 * $h;
    }

    // required index
    // of first '1'
    return indexOfFirstOne($arr,
                           $l, $h);
}

// Driver Code
$arr = array(0, 0, 1, 1, 1, 1);
echo "Index = " ,
      posOfFirstOne($arr);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the index of first 1
// in an infinite sorted array of 0's and 1's

// function to find the index of first '1'
// binary search technique is applied
function indexOfFirstOne(arr, low, high)
{
    var mid;
    while (low <= high) {
        mid = parseInt((low + high) / 2);

        // if true, then 'mid' is the index of first '1'
        if (arr[mid] == 1 &&
            (mid == 0 || arr[mid - 1] == 0))
            break;

        // first '1' lies to the left of 'mid'
        else if (arr[mid] == 1)
            high = mid - 1;

        // first '1' lies to the right of 'mid'
        else
            low = mid + 1;
    }

    // required index
    return mid;
}

// function to find the index of first 1 in
// an infinite sorted array of 0's and 1's
function posOfFirstOne(arr)
{
    // find the upper and lower bounds between
    // which the first '1' would be present
    var l = 0, h = 1;

    // as the array is being considered infinite
    // therefore 'h' index will always exist in
    // the array
    while (arr[h] == 0) {

        // lower bound
        l = h;

        // upper bound
        h = 2 * h;
    }

    // required index of first '1'
    return indexOfFirstOne(arr, l, h);
}

// Driver program to test above
var arr = [0, 0, 1, 1, 1, 1];
document.write( "Index = "
        + posOfFirstOne(arr));

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
Index = 2
```

设 p 为待搜索元素的位置。查找高索引“h”的步骤数为 0(对数 p)。“h”的值必须小于 2 * p。h/2 和 h 之间的元素数量必须是 O(p)。因此，二分搜索法步的时间复杂度也是 O(Log p)，整体时间复杂度是 2*O(Log p)，也就是 O(Log p)。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。