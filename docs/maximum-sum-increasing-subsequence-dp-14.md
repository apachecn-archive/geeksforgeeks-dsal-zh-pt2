# 最大和增加子序列| DP-14

> 原文:[https://www . geesforgeks . org/maximum-sum-递增-subsequence-dp-14/](https://www.geeksforgeeks.org/maximum-sum-increasing-subsequence-dp-14/)

给定 n 个正整数的数组。写一个程序，求给定数组的最大和子序列的和，使子序列中的整数按递增顺序排序。例如，如果输入是{1，101，2，3，100，4，5}，那么输出应该是 106 (1 + 2 + 3 + 100)，如果输入数组是{3，4，5，10}，那么输出应该是 22 (3 + 4 + 5 + 10)，如果输入数组是{10，5，4，3}，那么输出应该是 10

**解**
这个问题是标准[最长递增子序列(LIS)问题](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的变种。我们需要对 [LIS 问题](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的动态规划解决方案稍作改动。我们需要改变的是使用和作为标准，而不是增加子序列的长度。

以下是该问题的动态编程解决方案:

## C++

```
/* Dynamic Programming implementation
of Maximum Sum Increasing Subsequence
(MSIS) problem */
#include <bits/stdc++.h>
using namespace std;

/* maxSumIS() returns the maximum
sum of increasing subsequence
in arr[] of size n */
int maxSumIS(int arr[], int n)
{
    int i, j, max = 0;
    int msis[n];

    /* Initialize msis values
    for all indexes */
    for ( i = 0; i < n; i++ )
        msis[i] = arr[i];

    /* Compute maximum sum values
    in bottom up manner */
    for ( i = 1; i < n; i++ )
        for ( j = 0; j < i; j++ )
            if (arr[i] > arr[j] &&
                msis[i] < msis[j] + arr[i])
                msis[i] = msis[j] + arr[i];

    /* Pick maximum of
    all msis values */
    for ( i = 0; i < n; i++ )
        if ( max < msis[i] )
            max = msis[i];

    return max;
}

// Driver Code
int main()
{
    int arr[] = {1, 101, 2, 3, 100, 4, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Sum of maximum sum increasing "
            "subsequence is " << maxSumIS( arr, n ) << endl;
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
/* Dynamic Programming implementation
of Maximum Sum Increasing Subsequence
(MSIS) problem */
#include<stdio.h>

/* maxSumIS() returns the maximum
   sum of increasing subsequence
   in arr[] of size n */
int maxSumIS(int arr[], int n)
{
    int i, j, max = 0;
    int msis[n];

    /* Initialize msis values
       for all indexes */
    for ( i = 0; i < n; i++ )
        msis[i] = arr[i];

    /* Compute maximum sum values
       in bottom up manner */
    for ( i = 1; i < n; i++ )
        for ( j = 0; j < i; j++ )
            if (arr[i] > arr[j] &&
                msis[i] < msis[j] + arr[i])
                msis[i] = msis[j] + arr[i];

    /* Pick maximum of
       all msis values */
    for ( i = 0; i < n; i++ )
        if ( max < msis[i] )
            max = msis[i];

    return max;
}

// Driver Code
int main()
{
    int arr[] = {1, 101, 2, 3, 100, 4, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("Sum of maximum sum increasing "
            "subsequence is %d\n",
              maxSumIS( arr, n ) );
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Dynamic Programming Java
   implementation of Maximum Sum
   Increasing Subsequence (MSIS)
   problem */
class GFG
{
    /* maxSumIS() returns the
    maximum sum of increasing
    subsequence in arr[] of size n */
    static int maxSumIS(int arr[], int n)
    {
        int i, j, max = 0;
        int msis[] = new int[n];

        /* Initialize msis values
           for all indexes */
        for (i = 0; i < n; i++)
            msis[i] = arr[i];

        /* Compute maximum sum values
           in bottom up manner */
        for (i = 1; i < n; i++)
            for (j = 0; j < i; j++)
                if (arr[i] > arr[j] &&
                    msis[i] < msis[j] + arr[i])
                    msis[i] = msis[j] + arr[i];

        /* Pick maximum of all
           msis values */
        for (i = 0; i < n; i++)
            if (max < msis[i])
                max = msis[i];

        return max;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = new int[]{1, 101, 2, 3, 100, 4, 5};
        int n = arr.length;
        System.out.println("Sum of maximum sum "+
                            "increasing subsequence is "+
                              maxSumIS(arr, n));
    }
}

// This code is contributed
// by Rajat Mishra
```

## 计算机编程语言

```
# Dynamic Programming bsed Python
# implementation of Maximum Sum
# Increasing Subsequence (MSIS)
# problem

# maxSumIS() returns the maximum
# sum of increasing subsequence
# in arr[] of size n
def maxSumIS(arr, n):
    max = 0
    msis = [0 for x in range(n)]

    # Initialize msis values
    # for all indexes
    for i in range(n):
        msis[i] = arr[i]

    # Compute maximum sum
    # values in bottom up manner
    for i in range(1, n):
        for j in range(i):
            if (arr[i] > arr[j] and
                msis[i] < msis[j] + arr[i]):
                msis[i] = msis[j] + arr[i]

    # Pick maximum of
    # all msis values
    for i in range(n):
        if max < msis[i]:
            max = msis[i]

    return max

# Driver Code
arr = [1, 101, 2, 3, 100, 4, 5]
n = len(arr)
print("Sum of maximum sum increasing " +
                     "subsequence is " +
                  str(maxSumIS(arr, n)))

# This code is contributed
# by Bhavya Jain
```

## C#

```
// Dynamic Programming C# implementation
// of Maximum Sum Increasing Subsequence
// (MSIS) problem
using System;
class GFG {

    // maxSumIS() returns the
    // maximum sum of increasing
    // subsequence in arr[] of size n
    static int maxSumIS( int []arr, int n )
    {
        int i, j, max = 0;
        int []msis = new int[n];

        /* Initialize msis values
           for all indexes */
        for ( i = 0; i < n; i++ )
            msis[i] = arr[i];

        /* Compute maximum sum values
           in bottom up manner */
        for ( i = 1; i < n; i++ )
            for ( j = 0; j < i; j++ )
                if ( arr[i] > arr[j] &&
                    msis[i] < msis[j] + arr[i])
                    msis[i] = msis[j] + arr[i];

        /* Pick maximum of all
           msis values */
        for ( i = 0; i < n; i++ )
            if ( max < msis[i] )
                max = msis[i];

        return max;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = new int[]{1, 101, 2, 3, 100, 4, 5};
        int n = arr.Length;
        Console.WriteLine("Sum of maximum sum increasing "+
                                        " subsequence is "+
        maxSumIS(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Dynamic Programming implementation
// of Maximum Sum Increasing
// Subsequence (MSIS) problem

// maxSumIS() returns the maximum
// sum of increasing subsequence
// in arr[] of size n
function maxSumIS($arr, $n)
{
    $max = 0;
    $msis= array($n);

    // Initialize msis values
    // for all indexes
    for($i = 0; $i < $n; $i++ )
        $msis[$i] = $arr[$i];

    // Compute maximum sum values
    // in bottom up manner
    for($i = 1; $i < $n; $i++)
        for($j = 0; $j < $i; $j++)
            if ($arr[$i] > $arr[$j] &&
                $msis[$i] < $msis[$j] + $arr[$i])
                $msis[$i] = $msis[$j] + $arr[$i];

    // Pick maximum of all msis values
    for($i = 0;$i < $n; $i++ )
        if ($max < $msis[$i] )
            $max = $msis[$i];

    return $max;
}

    // Driver Code
    $arr = array(1, 101, 2, 3, 100, 4, 5);
    $n = count($arr);
    echo "Sum of maximum sum increasing subsequence is "
                                   .maxSumIS( $arr, $n );

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Dynamic Programming implementation
// of Maximum Sum Increasing Subsequence
// (MSIS) problem

// maxSumIS() returns the maximum
// sum of increasing subsequence
// in arr[] of size n
function maxSumIS(arr, n)
{
    let i, j, max = 0;
    let msis = new Array(n);

    // Initialize msis values
    // for all indexes
    for(i = 0; i < n; i++)
        msis[i] = arr[i];

    // Compute maximum sum values
    // in bottom up manner
    for(i = 1; i < n; i++)
        for(j = 0; j < i; j++)
            if (arr[i] > arr[j] &&
                msis[i] < msis[j] + arr[i])
                msis[i] = msis[j] + arr[i];

    // Pick maximum of
    // all msis values
    for(i = 0; i < n; i++)
        if (max < msis[i])
            max = msis[i];

    return max;
}

// Driver Code
let arr = [ 1, 101, 2, 3, 100, 4, 5 ];
let n = arr.length;
document.write("Sum of maximum sum increasing " +
               "subsequence is " + maxSumIS(arr, n));

// This code is contributed by rishavmahato348

</script>
```

**输出:**

```
Sum of maximum sum increasing subsequence is 106
```

时间复杂性:O(n^2)

空间复杂性

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。