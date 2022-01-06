# 指数搜索

> 原文:[https://www.geeksforgeeks.org/exponential-search/](https://www.geeksforgeeks.org/exponential-search/)

这种搜索算法的名称可能会引起误解，因为它在 0(Log n)时间内工作。这个名字来自于它搜索元素的方式。

```
Given a sorted array, and an element x to be 
searched, find position of x in the array.

Input:  arr[] = {10, 20, 40, 45, 55}
        x = 45
Output: Element found at index 3

Input:  arr[] = {10, 15, 25, 45, 55}
        x = 15
Output: Element found at index 1
```

这个问题我们已经讨论过，[线性搜索](https://www.geeksforgeeks.org/linear-search/)，[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。
指数搜索包括两个步骤:

1.  查找元素所在的范围
2.  在上述发现的范围内做二分搜索法。

**如何找到元素可能存在的范围？**
这个想法是从 1 号子阵列开始，将其最后一个元素与 x 进行比较，然后尝试 2 号，然后是 4 号，以此类推，直到一个子阵列的最后一个元素不大于。
一旦我们找到一个指数 I(I 重复加倍后)，我们就知道元素一定存在于 i/2 和 I 之间(为什么是 i/2？因为我们在之前的迭代中找不到更大的值)
下面给出的是上面步骤的实现。

## C++

```
// C++ program to find an element x in a
// sorted array using Exponential search.
#include <bits/stdc++.h>
using namespace std;

int binarySearch(int arr[], int, int, int);

// Returns position of first occurrence of
// x in array
int exponentialSearch(int arr[], int n, int x)
{
    // If x is present at first location itself
    if (arr[0] == x)
        return 0;

    // Find range for binary search by
    // repeated doubling
    int i = 1;
    while (i < n && arr[i] <= x)
        i = i*2;

    //  Call binary search for the found range.
    return binarySearch(arr, i/2,
                            min(i, n-1), x);
}

// A recursive binary search function. It returns
// location of x in  given array arr[l..r] is
// present, otherwise -1
int binarySearch(int arr[], int l, int r, int x)
{
    if (r >= l)
    {
        int mid = l + (r - l)/2;

        // If the element is present at the middle
        // itself
        if (arr[mid] == x)
            return mid;

        // If element is smaller than mid, then it
        // can only be present n left subarray
        if (arr[mid] > x)
            return binarySearch(arr, l, mid-1, x);

        // Else the element can only be present
        // in right subarray
        return binarySearch(arr, mid+1, r, x);
    }

    // We reach here when element is not present
    // in array
    return -1;
}

// Driver code
int main(void)
{
   int arr[] = {2, 3, 4, 10, 40};
   int n = sizeof(arr)/ sizeof(arr[0]);
   int x = 10;
   int result = exponentialSearch(arr, n, x);
   (result == -1)? cout <<"Element is not present in array"
                 : cout <<"Element is present at index " << result;
   return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
// C++ program to find an element x in a
// sorted array using Exponential search.
#include <stdio.h>
#include <time.h>
#include <math.h>
#define min

int binarySearch(int arr[], int, int, int);

// Returns position of first occurrence of
// x in array
int exponentialSearch(int arr[], int n, int x)
{
    // If x is present at first location itself
    if (arr[0] == x)
        return 0;

    // Find range for binary search by
    // repeated doubling
    int i = 1;
    while (i < n && arr[i] <= x)
        i = i*2;

    //  Call binary search for the found range.
    return binarySearch(arr, i/2,
                            min(i, n-1), x);
}

// A recursive binary search function. It returns
// location of x in  given array arr[l..r] is
// present, otherwise -1
int binarySearch(int arr[], int l, int r, int x)
{
    if (r >= l)
    {
        int mid = l + (r - l)/2;

        // If the element is present at the middle
        // itself
        if (arr[mid] == x)
            return mid;

        // If element is smaller than mid, then it
        // can only be present n left subarray
        if (arr[mid] > x)
            return binarySearch(arr, l, mid-1, x);

        // Else the element can only be present
        // in right subarray
        return binarySearch(arr, mid+1, r, x);
    }

    // We reach here when element is not present
    // in array
    return -1;
}

// Driver code
int main(void)
{
   int arr[] = {2, 3, 4, 10, 40};
   int n = sizeof(arr)/ sizeof(arr[0]);
   int x = 10;
   int result = exponentialSearch(arr, n, x);
   (result == -1)? printf("Element is not
                            present in array")
                 : printf("Element is present
                                 at index %d",
                                       result);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to
// find an element x in a
// sorted array using
// Exponential search.
import java.util.Arrays;

class GFG
{
    // Returns position of
    // first occurrence of
    // x in array
    static int exponentialSearch(int arr[],
                                 int n, int x)
    {
        // If x is present at first location itself
        if (arr[0] == x)
            return 0;

        // Find range for binary search by
        // repeated doubling
        int i = 1;
        while (i < n && arr[i] <= x)
            i = i*2;

        // Call binary search for the found range.
        return Arrays.binarySearch(arr, i/2,
                              Math.min(i, n-1), x);
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = {2, 3, 4, 10, 40};
        int x = 10;
        int result = exponentialSearch(arr,
                                  arr.length, x);

        System.out.println((result < 0) ?
          "Element is not present in array" :
          "Element is present at index " +
                             result);
    }
}
```

## 计算机编程语言

```
# Python program to find an element x
# in a sorted array using Exponential Search

# A recursive binary search function returns
# location  of x in given array arr[l..r] is
# present, otherwise -1
def binarySearch( arr, l, r, x):
    if r >= l:
        mid = l + ( r-l ) / 2

        # If the element is present at
        # the middle itself
        if arr[mid] == x:
            return mid

        # If the element is smaller than mid,
        # then it can only be present in the
        # left subarray
        if arr[mid] > x:
            return binarySearch(arr, l,
                                mid - 1, x)

        # Else he element can only be
        # present in the right
        return binarySearch(arr, mid + 1, r, x)

    # We reach here if the element is not present
    return -1

# Returns the position of first
# occurrence of x in array
def exponentialSearch(arr, n, x):
    # IF x is present at first
    # location itself
    if arr[0] == x:
        return 0

    # Find range for binary search
    # j by repeated doubling
    i = 1
    while i < n and arr[i] <= x:
        i = i * 2

    # Call binary search for the found range
    return binarySearch( arr, i / 2,
                         min(i, n-1), x)

# Driver Code
arr = [2, 3, 4, 10, 40]
n = len(arr)
x = 10
result = exponentialSearch(arr, n, x)
if result == -1:
    print "Element not found in the array"
else:
    print "Element is present at index %d" %(result)

# This code is contributed by Harshit Agrawal
```

## C#

```
// C# program to find an element x in a
// sorted array using Exponential search.
using System;
class GFG {

// Returns position of first
// occurrence of x in array
static int exponentialSearch(int []arr,
                         int n, int x)
{

    // If x is present at
    // first location itself
    if (arr[0] == x)
        return 0;

    // Find range for binary search
    // by repeated doubling
    int i = 1;
    while (i < n && arr[i] <= x)
        i = i * 2;

    // Call binary search for
    // the found range.
    return binarySearch(arr, i/2,
                       Math.Min(i, n - 1), x);
}

// A recursive binary search
// function. It returns location
// of x in given array arr[l..r] is
// present, otherwise -1
static int binarySearch(int []arr, int l,
                        int r, int x)
{
    if (r >= l)
    {
        int mid = l + (r - l) / 2;

        // If the element is present
        // at the middle itself
        if (arr[mid] == x)
            return mid;

        // If element is smaller than
        // mid, then it can only be
        // present n left subarray
        if (arr[mid] > x)
            return binarySearch(arr, l, mid - 1, x);

        // Else the element can only
        // be present in right subarray
        return binarySearch(arr, mid + 1, r, x);
    }

    // We reach here when element
    // is not present in array
    return -1;
}

// Driver code
public static void Main()
{
    int []arr = {2, 3, 4, 10, 40};
    int n = arr.Length;
    int x = 10;
    int result = exponentialSearch(arr, n, x);
    if (result == -1)
            Console.Write("Element is not
                          present in array");
        else
            Console.Write("Element is
                           present at index "
                                   + result);
}
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find an element x in a
// sorted array using Exponential search.

// Returns position of first
// occurrence of x in array
function exponentialSearch($arr, $n, $x)
{

    // If x is present at
    // first location itself
    if ($arr[0] == $x)
        return 0;

    // Find range for binary search
    // by repeated doubling
    $i = 1;
    while ($i< $n and $arr[$i] <=$x)
        $i = $i * 2;

    // Call binary search
    // for the found range.
    return binarySearch($arr, $i / 2,
                        min($i, $n - 1), $x);
}

// A recursive binary search
// function. It returns location
// of x in given array arr[l..r] is
// present, otherwise -1
function binarySearch($arr, $l,
                      $r, $x)
{
    if ($r >= $l)
    {
        $mid = $l + ($r - $l)/2;

        // If the element is
        // present at the middle
        // itself
        if ($arr[$mid] == $x)
            return $mid;

        // If element is smaller
        // than mid, then it
        // can only be present
        // n left subarray
        if ($arr[$mid] > $x)
            return binarySearch($arr, $l,
                                $mid - 1, $x);

        // Else the element
        // can only be present
        // in right subarray
        return binarySearch($arr, $mid + 1,
                                    $r, $x);
    }

    // We reach here when
    // element is not present
    // in array
    return -1;
}

// Driver code
$arr = array(2, 3, 4, 10, 40);
$n = count($arr);
$x = 10;
$result = exponentialSearch($arr, $n, $x);
if($result == -1)
    echo "Element is not present in array";
else
    echo "Element is present at index ",
                                $result;

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>

// Javascript program to find an element x
// in a sorted array using Exponential Search

// A recursive binary search
// function. It returns location
// of x in given array arr[l..r] is
// present, otherwise -1
function binarySearch(arr, l, r, x)
{
    if (r >= l)
    {
        let mid = l + (r - l) / 2;

        // If the element is present
        // at the middle itself
        if (arr[mid] == x)
            return mid;

        // If element is smaller than
        // mid, then it can only be
        // present n left subarray
        if (arr[mid] > x)
            return binarySearch(arr, l, mid - 1, x);

        // Else the element can only
        // be present in right subarray
        return binarySearch(arr, mid + 1, r, x);
    }

    // We reach here when element
    // is not present in array
    return -1;
}

 // Returns position of first
// occurrence of x in array
function exponentialSearch(arr, n, x)
{

    // If x is present at
    // first location itself
    if (arr[0] == x)
        return 0;

    // Find range for binary search
    // by repeated doubling
    let i = 1;
    while (i < n && arr[i] <= x)
        i = i * 2;

    // Call binary search for
    // the found range.
    return binarySearch(arr, i/2,
                       Math.min(i, n - 1), x);
}

// Driver Code

    let arr = [2, 3, 4, 10, 40];
    let n = arr.length;
    let x = 10;
    let result = exponentialSearch(arr, n, x);
    if (result == -1)
         document.write("Element is not present in array");
    else
        document.write("Element is present at index " + result);

</script>
```

**Output**

```
Element is present at index 3
```

**时间复杂度:**O(Log n)
T3】辅助空间:二分搜索法的上述实现是递归的，需要 O(Log n)空间。利用迭代二分搜索法，我们只需要 O(1)空间。
**指数搜索的应用:**

1.  指数二分搜索法对于无界搜索特别有用，在无界搜索中数组的大小是无限的。请参考[无界二分搜索法](https://www.geeksforgeeks.org/find-the-point-where-a-function-becomes-negative/)的例子。
2.  对于有界数组，它比二分搜索法更有效，而且当要搜索的元素更接近第一个元素时也是如此。

**参考:**
https://en.wikipedia.org/wiki/Exponential_search
本文由**潘卡·夏尔马**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。