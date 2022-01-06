# 在允许重复的数组中找到一个固定点

> 原文:[https://www . geesforgeks . org/find-定点-数组-允许重复/](https://www.geeksforgeeks.org/find-fixed-point-array-duplicates-allowed/)

给定一个按升序排列的 n 个重复或不同整数的数组，编写一个函数返回数组中的一个固定点，如果数组中有任何固定点，则返回-1。数组中的不动点是一个索引 I，这样 arr[i]等于 I。注意数组中的整数可以是负数。
**例:**

```
Input : arr[] = {-10, -1, 3, 3, 10, 30, 30, 50, 100} 
Output: 3  
Note : arr[3] == 3 

Input: arr[] = {0, 2, 5, 8, 17}
Output: 0  

Input: arr[] = {-10, -5, 3, 4, 7, 9}
Output: -1  
No Fixed Point
```

我们已经讨论过[在给定的 n 个不同整数的数组中找到一个不动点](https://www.geeksforgeeks.org/find-a-fixed-point-in-a-given-array/)。

如果元素不明显，则先前讨论的算法失败。考虑以下阵列:

```
 // with duplicates value 
 Input : arr[] = {-10, -5, 2, 2, 2, 3, 4, 7, 9, 12, 13}; 
 Wrong Output : -1  // but arr[2] == 2 
```

当我们看到 A [mid] < mid, we cannot conclude which side the fixed index is on. It could be on the right side, as before. Or, it could be on the left side (as it, in fact, is). 
时，它可能在左侧的任何地方吗？不完全是。由于 A[ 5] = 3，我们知道 A[ 4]不可能是一个固定的指数。A[ 4]需要为 4 才能成为固定索引，但 A[ 4]必须小于或等于 A[ 5]。
事实上，当我们看到 A[ 5] = 3 时，我们将需要像以前一样递归搜索右侧。但是，要搜索左侧，我们可以跳过一堆元素，只递归搜索元素 A [ 0]到 A [ 3]。[ 3]是第一个可以是固定索引的元素。
一般的模式是，我们先比较中间指数和中间值，看是否相等。然后，如果它们不相等，我们递归搜索左右两侧，如下所示:
下面的代码实现了这个算法。

## C++

```
// C++ implementation to find fixed
// index using binary search
#include<bits/stdc++.h>

using namespace std;

// Main Function to find fixed
// index using binary search
int binarySearch(int arr[], int low,
                        int high)
{
    if (high < low)
        return -1;

    // low + (high - low) / 2
    int mid = (low + high) / 2;
    int midValue = arr[mid];

    if (mid == arr[mid])
        return mid;

    // Search left
    int leftindex = min(mid - 1, midValue);
    int left = binarySearch(arr, low, leftindex);

    if (left >= 0)
        return left;

    // Search right
    int rightindex = max(mid + 1, midValue);
    int right = binarySearch(arr, rightindex, high);

    return right;
}

// Driver code
int main()
{
    // input 1
    int arr[] = {-10, -5, 2, 2, 2, 
                 3, 4, 7, 9, 12, 13};

    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Fixed Point is "
         << binarySearch(arr, 0, n - 1);

    // input 2
    int arr1[] = {-10, -1, 3, 3, 10,
                    30, 30, 50, 100};

    int n1 = sizeof(arr) / sizeof(arr1[0]);

    cout << "\nFixed Point is "
         << binarySearch(arr1, 0, n1 - 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of find fixed
// index using binary search
class GFG
{
    // Main Function to find fixed
    // index using binary search
    static int binarySearch(int arr[], int low,
                                      int high)
    {
        if (high < low)
            return -1;

        // low + (high - low) / 2
        int mid = (low + high) / 2;
        int midValue = arr[mid];

        if (mid == arr[mid])
            return mid;

        // Search left
        int leftindex = Math.min(mid - 1, midValue);
        int left = binarySearch(arr, low, leftindex);

        if (left >= 0)
            return left;

        // Search right
        int rightindex = Math.max(mid + 1, midValue);
        int right = binarySearch(arr, rightindex, high);

        return right;
    }

    // Driver code
    public static void main(String[] args)
    {
        // input 1
        int arr[] = {-10, -5, 2, 2, 2,
                     3, 4, 7, 9, 12, 13};

        System.out.println("Fixed Point is " +
            binarySearch(arr, 0, arr.length - 1));

        // input 2
        int arr1[] = {-10, -1, 3, 3, 10,
                        30, 30, 50, 100};

        System.out.println("Fixed Point is " +
            binarySearch(arr1, 0, arr1.length - 1));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation to find fixed
# index using binary search

# Main Function to find fixed
# index using binary search
def binarySearch(arr, low, high):
    if (high < low):
        return -1

    # low + (high - low) / 2
    mid = int((low + high) / 2)
    midValue = arr[mid]

    if (mid == arr[mid]):
        return mid

    # Search left
    leftindex = min(mid - 1, midValue)
    left = binarySearch(arr, low, leftindex)

    if (left >= 0):
        return left

    # Search right
    rightindex = max(mid + 1, midValue)
    right = binarySearch(arr, rightindex, high)

    return right

# Driver code
if __name__ == '__main__':

    # input 1
    arr = [-10, -5, 2, 2, 2, 3,
               4, 7, 9, 12, 13]

    n = len(arr)
    print("Fixed Point is",
           binarySearch(arr, 0, n - 1))

    # input 2
    arr1 = [-10, -1, 3, 3, 10,
              30, 30, 50, 100]

    n1 = len(arr)

    print("Fixed Point is",
           binarySearch(arr1, 0, n1 - 1))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# implementation of find fixed
// index using binary search
using System;

class GFG
{
    // Main Function to find fixed
    // index using binary search
    static int binarySearch(int []arr, int low,
                                      int high)
    {
        if (high < low)
            return -1;

        // low + (high - low) / 2
        int mid = (low + high) / 2;
        int midValue = arr[mid];

        if (mid == arr[mid])
            return mid;

        // Search left
        int leftindex = Math.Min(mid - 1, midValue);
        int left = binarySearch(arr, low, leftindex);

        if (left >= 0)
            return left;

        // Search right
        int rightindex = Math.Max(mid + 1, midValue);
        int right = binarySearch(arr, rightindex, high);

        return right;
    }

    // Driver Code
    public static void Main()
    {
        // input 1
        int []arr = {-10, -5, 2, 2, 2, 
                     3, 4, 7, 9, 12, 13};

        Console.WriteLine("Fixed Point is " +
            binarySearch(arr, 0, arr.Length - 1));

        // input 2
        int []arr1 = {-10, -1, 3, 3, 10,
                       30, 30, 50, 100};

        Console.Write("Fixed Point is " +
            binarySearch(arr1, 0, arr1.Length - 1));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// find fixed index using
// binary search

// Main Function to find fixed
// index using binary search
function binarySearch($arr,
                      $low,
                      $high)
{
    if ($high < $low)
        return -1;

    // low + (high - low) / 2
    $mid = floor(($low + $high) / 2);
    $midValue = $arr[$mid];

    if ($mid == $arr[$mid])
        return $mid;

    // Search left
    $leftindex = min($mid - 1,
                     $midValue);
    $left = binarySearch($arr, $low,
                         $leftindex);

    if ($left >= 0)
        return $left;

    // Search right
    $rightindex = max($mid + 1,
                      $midValue);
    $right = binarySearch($arr,
                          $rightindex,
                          $high);

    return $right;
}

// Driver code

// input 1
$arr = array(-10, -5, 2, 2, 2, 3,
                4, 7, 9, 12, 13);

$n = sizeof($arr) / sizeof($arr[0]);
echo "Fixed Point is ",
      binarySearch($arr, 0, $n - 1);

// input 2
$arr1 = array(-10, -1, 3, 3, 10,
               30, 30, 50, 100);

$n1 = sizeof($arr) / sizeof($arr1[0]);

echo "\nFixed Point is ",
     binarySearch($arr1, 0, $n1 - 1);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find fixed
// index using binary search

// Main Function to find fixed
// index using binary search
function binarySearch(arr, low, high)
{
    if (high < low)
        return -1;

    // low + (high - low) / 2
    var mid = parseInt((low + high) / 2);
    var midValue = arr[mid];

    if (mid == arr[mid])
        return mid;

    // Search left
    var leftindex = Math.min(mid - 1, midValue);
    var left = binarySearch(arr, low, leftindex);

    if (left >= 0)
        return left;

    // Search right
    var rightindex = Math.max(mid + 1, midValue);
    var right = binarySearch(arr, rightindex, high);

    return right;
}

// Driver code

// input 1
var arr = [-10, -5, 2, 2, 2,
            3, 4, 7, 9, 12, 13];

var n = arr.length;
document.write("Fixed Point is "
    + binarySearch(arr, 0, n - 1));
// input 2
var arr1 = [-10, -1, 3, 3, 10,
                30, 30, 50, 100];

var n1 = arr1.length;

document.write("<br>Fixed Point is "
    + binarySearch(arr1, 0, n1 - 1));

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
Fixed Point is  2
Fixed Point is  3
```

**算法范式:**除&征服
T3】时间复杂度: O(Logn)

**辅助空间:** O(1)
本文由**Somesh Awasthi**先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。