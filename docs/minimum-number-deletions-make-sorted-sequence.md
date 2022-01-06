# 组成排序序列的最小删除次数

> 原文:[https://www . geesforgeks . org/最小数量-删除-制作-排序-序列/](https://www.geeksforgeeks.org/minimum-number-deletions-make-sorted-sequence/)

给定 n 个整数的数组。任务是从数组中移除或删除最小数量的元素，以便当剩余的元素以相同的顺序排列时，形成一个**递增的排序序列**。
**例:**

```
Input : {5, 6, 1, 7, 4}
Output : 2
Removing 1 and 4
leaves the remaining sequence order as
5 6 7 which is a sorted sequence.

Input : {30, 40, 2, 5, 1, 7, 45, 50, 8}
Output : 4
```

一个**简单的解决方案**是逐个移除[所有子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，并检查剩余的元素集是否按排序顺序排列。这个解的时间复杂度是指数的。
一种**有效方法**使用[的概念来寻找给定序列的最长递增子序列](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/)的长度。
**算法:**

```
-->arr be the given array.
-->n number of elements in arr.
-->len be the length of longest
   increasing subsequence in arr.
-->// minimum number of deletions
   min = n - len
```

## C++

```
// C++ implementation to find
// minimum number of deletions
// to make a sorted sequence
#include <bits/stdc++.h>
using namespace std;

/* lis() returns the length
   of the longest increasing
   subsequence in arr[] of size n */
int lis( int arr[], int n )
{
    int result = 0;
    int lis[n];

    /* Initialize LIS values
    for all indexes */
    for (int i = 0; i < n; i++ )
        lis[i] = 1;

    /* Compute optimized LIS
       values in bottom up manner */
    for (int i = 1; i < n; i++ )
        for (int j = 0; j < i; j++ )
            if ( arr[i] > arr[j] &&
                 lis[i] < lis[j] + 1)
            lis[i] = lis[j] + 1;

    /* Pick resultimum
    of all LIS values */
    for (int i = 0; i < n; i++ )
        if (result < lis[i])
            result = lis[i];

    return result;
}

// function to calculate minimum
// number of deletions
int minimumNumberOfDeletions(int arr[],
                             int n)
{
    // Find longest increasing
    // subsequence
    int len = lis(arr, n);

    // After removing elements
    // other than the lis, we
    // get sorted sequence.
    return (n - len);
}

// Driver Code
int main()
{
    int arr[] = {30, 40, 2, 5, 1,
                   7, 45, 50, 8};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Minimum number of deletions = "
         << minimumNumberOfDeletions(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// minimum number of deletions
// to make a sorted sequence

class GFG
{
    /* lis() returns the length
    of the longest increasing
    subsequence in arr[] of size n */
    static int lis( int arr[], int n )
    {
        int result = 0;
        int[] lis = new int[n];

        /* Initialize LIS values
        for all indexes */
        for (int i = 0; i < n; i++ )
            lis[i] = 1;

        /* Compute optimized LIS
           values in bottom up manner */
        for (int i = 1; i < n; i++ )
            for (int j = 0; j < i; j++ )
                if ( arr[i] > arr[j] &&
                    lis[i] < lis[j] + 1)
                    lis[i] = lis[j] + 1;

        /* Pick resultimum of
        all LIS values */
        for (int i = 0; i < n; i++ )
            if (result < lis[i])
                result = lis[i];

        return result;
    }

    // function to calculate minimum
    // number of deletions
    static int minimumNumberOfDeletions(int arr[],
                                        int n)
    {
        // Find longest
        // increasing subsequence
        int len = lis(arr, n);

        // After removing elements
        // other than the lis, we get
        // sorted sequence.
        return (n - len);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = {30, 40, 2, 5, 1,
                       7, 45, 50, 8};
        int n = arr.length;
        System.out.println("Minimum number of" +
                               " deletions = " +
              minimumNumberOfDeletions(arr, n));
    }
}

/* This code is contributed by Harsh Agarwal */
```

## 蟒蛇 3

```
# Python3 implementation to find
# minimum number of deletions to
# make a sorted sequence

# lis() returns the length
# of the longest increasing
# subsequence in arr[] of size n
def lis(arr, n):

    result = 0
    lis = [0 for i in range(n)]

    # Initialize LIS values
    # for all indexes
    for i in range(n):
        lis[i] = 1

    # Compute optimized LIS values
    # in bottom up manner
    for i in range(1, n):
        for j in range(i):
            if ( arr[i] > arr[j] and
                lis[i] < lis[j] + 1):
                lis[i] = lis[j] + 1

    # Pick resultimum
    # of all LIS values
    for i in range(n):
        if (result < lis[i]):
            result = lis[i]

    return result

# Function to calculate minimum
# number of deletions
def minimumNumberOfDeletions(arr, n):

    # Find longest increasing
    # subsequence
    len = lis(arr, n)

    # After removing elements
    # other than the lis, we
    # get sorted sequence.
    return (n - len)

# Driver Code
arr = [30, 40, 2, 5, 1,
          7, 45, 50, 8]
n = len(arr)
print("Minimum number of deletions = ",
      minimumNumberOfDeletions(arr, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# implementation to find
// minimum number of deletions
// to make a sorted sequence
using System;

class GfG
{

    /* lis() returns the length of
    the longest increasing subsequence
    in arr[] of size n */
    static int lis( int []arr, int n )
    {
        int result = 0;
        int[] lis = new int[n];

        /* Initialize LIS values for
        all indexes */
        for (int i = 0; i < n; i++ )
            lis[i] = 1;

        /* Compute optimized LIS values
        in bottom up manner */
        for (int i = 1; i < n; i++ )
            for (int j = 0; j < i; j++ )
                if ( arr[i] > arr[j] &&
                     lis[i] < lis[j] + 1)
                  lis[i] = lis[j] + 1;

        /* Pick resultimum of all LIS
        values */
        for (int i = 0; i < n; i++ )
            if (result < lis[i])
                result = lis[i];

        return result;
    }

    // function to calculate minimum
    // number of deletions
    static int minimumNumberOfDeletions(
                        int []arr, int n)
    {

        // Find longest increasing
        // subsequence
        int len = lis(arr, n);

        // After removing elements other
        // than the lis, we get sorted
        // sequence.
        return (n - len);
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int []arr = {30, 40, 2, 5, 1,
                       7, 45, 50, 8};
        int n = arr.Length;
        Console.Write("Minimum number of" +
                          " deletions = " +
         minimumNumberOfDeletions(arr, n));
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// minimum number of deletions
// to make a sorted sequence

/* lis() returns the length of
   the longest increasing subsequence
   in arr[] of size n */
function lis( $arr, $n )
{
    $result = 0;
    $lis[$n] = 0;

    /* Initialize LIS values
       for all indexes */
    for ($i = 0; $i < $n; $i++ )
        $lis[$i] = 1;

    /* Compute optimized LIS
       values in bottom up manner */
    for ($i = 1; $i < $n; $i++ )
        for ($j = 0; $j < $i; $j++ )
            if ( $arr[$i] > $arr[$j] &&
                $lis[$i] < $lis[$j] + 1)
                $lis[$i] = $lis[$j] + 1;

    /* Pick resultimum of
    all LIS values */
    for ($i = 0; $i < $n; $i++ )
        if ($result < $lis[$i])
            $result = $lis[$i];

    return $result;
}

// function to calculate minimum
// number of deletions
function minimumNumberOfDeletions($arr, $n)
{
    // Find longest increasing
    // subsequence
    $len = lis($arr, $n);

    // After removing elements
    // other than the lis, we
    // get sorted sequence.
    return ($n - $len);
}

// Driver Code
$arr = array(30, 40, 2, 5, 1,
               7, 45, 50, 8);
$n = sizeof($arr) / sizeof($arr[0]);
echo "Minimum number of deletions = " ,
    minimumNumberOfDeletions($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// javascript implementation to find
// minimum number of deletions
// to make a sorted sequence
/* lis() returns the length
of the longest increasing
subsequence in arr[] of size n */
function lis(arr,n)
{
    let result = 0;
    let lis= new Array(n);

    /* Initialize LIS values
    for all indexes */
    for (let i = 0; i < n; i++ )
        lis[i] = 1;

    /* Compute optimized LIS
    values in bottom up manner */
    for (let i = 1; i < n; i++ )
        for (let j = 0; j < i; j++ )
            if ( arr[i] > arr[j] &&
                lis[i] < lis[j] + 1)
            lis[i] = lis[j] + 1;

    /* Pick resultimum
    of all LIS values */
    for (let i = 0; i < n; i++ )
        if (result < lis[i])
            result = lis[i];

    return result;
}

// function to calculate minimum
// number of deletions
function minimumNumberOfDeletions(arr,n)
{

    // Find longest increasing
    // subsequence
    let len = lis(arr,n);

    // After removing elements
    // other than the lis, we
    // get sorted sequence.
    return (n - len);
}

    let arr = [30, 40, 2, 5, 1,7, 45, 50, 8];
    let n = arr.length;
    document.write("Minimum number of deletions = "
    + minimumNumberOfDeletions(arr,n));

// This code is contributed by vaibhavrabadiya117.
</script>
```

**输出:**

```
Minimum number of deletions = 4 
```

**时间复杂度:** O(n <sup>2</sup> )
时间复杂度可以通过寻找[最长递增子序列大小(N Log N)](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)
降低到 O(nlogn)本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。