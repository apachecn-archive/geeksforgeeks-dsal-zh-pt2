# 总和大于等于零的最长子阵列

> 原文:[https://www . geesforgeks . org/sum 大于等于零的最长子数组/](https://www.geeksforgeeks.org/longest-subarray-with-sum-greater-than-equal-to-zero/)

给定一个 N 个整数的数组。任务是找到最大长度子阵列，使其所有元素之和大于或等于 0。

**示例**:

```
Input: arr[]= {-1, 4, -2, -5, 6, -8}
Output: 5
Explanation: {-1, 4, -2, -5, 6} forms the longest subarray with sum=2.

Input: arr[]={-5, -6}
Output: 0
Explanation: No such subarray is possible 
```

一种**天真的方法**是预先计算数组的前缀和。然后对每个开始和结束索引使用两个嵌套循环，如果直到结束索引的前缀总和减去开始索引之前的前缀总和大于或等于 0，则相应地更新答案。
T3】时间复杂度 : O(N <sup>2</sup>

一个**有效的方法**是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来解决以下问题。以下是解决上述问题的步骤:

*   首先，计算数组每个索引的后缀和，并将其存储在另一个数组中。
*   使用另一个数组*搜索空间*存储每个子数组的起点。
*   从第 0 个索引开始迭代，如果第 I 个索引之前的后缀大于搜索空间中最顶端的元素，则将该后缀和添加到搜索空间中。
*   使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来寻找搜索空间中的最低索引，使得后缀和直到该索引减去后缀和直到(I+1)’th 大于等于 0。如果存在任何这样的索引，则相应地更新答案。

这里的关键观察是，如果后缀和大于搜索空间中的所有其他后缀和，则向搜索空间添加后缀和，因为长度必须最大化。

下面是上述方法的实现。

## C++

```
// C++ Program to compute the
// longest subarray with
// sum greater than equal to 0.
#include <bits/stdc++.h>
using namespace std;

// Function for the searching the
// starting index of the subarray
int search(int* searchspace, int s, int e, int key)
{
    // -1 signifies that no
    // starting point of the subarray
    // is not found with sum greater
    // than equal to 0.
    int ans = -1;

    // Binary search
    while (s <= e) {
        int mid = (s + e) / 2;

        if (searchspace[mid] - key >= 0) {
            ans = mid;
            e = mid - 1;
        }
        else {
            s = mid + 1;
        }
    }

    return ans;
}

// Function to return the longest subarray
int longestSubarray(int a[], int n)
{
    // Array for the suffix sum
    // of the above the array.
    int SuffixSum[n + 1];
    SuffixSum[n] = 0;

    for (int i = n - 1; i >= 0; --i) {
        SuffixSum[i] = SuffixSum[i + 1] + a[i];
    }

    int ans = 0;

    // Search Space for potential starting
    // points of the subarray.
    // It will store the suffix sum
    // till i'th index in increasing order.
    int searchspace[n];

    // It will store the indexes
    // till which the suffix sum
    // is present in search space.
    int index[n];

    int j = 0;

    for (int i = 0; i < n; ++i) {

        // add the element to the search space if the j=0
        // or if the topmost element is lesser
        // than present suffix sum.
        if (j == 0 or SuffixSum[i] > searchspace[j - 1]) {
            searchspace[j] = SuffixSum[i];
            index[j] = i;
            j++;
        }

        int idx = search(searchspace, 0, j - 1, SuffixSum[i + 1]);

        // Only when idx is not -1 an subarray is
        // possible with ending index at i.
        if (idx != -1)
            ans = max(ans, i - index[idx] + 1);
    }

    return ans;
}

// Driver Code
int main()
{
    int a[] = { -1, 4, -2, -5, 6, -8 };

    int n = sizeof(a) / sizeof(a[0]);

    cout << longestSubarray(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  Program to compute the
// longest subarray with
// sum greater than equal to 0.

import java.io.*;

class GFG {

// Function for the searching the
// starting index of the subarray
static int search(int searchspace[], int s, int e, int key)
{
    // -1 signifies that no
    // starting point of the subarray
    // is not found with sum greater
    // than equal to 0.
    int ans = -1;

    // Binary search
    while (s <= e) {
        int mid = (s + e) / 2;

        if (searchspace[mid] - key >= 0) {
            ans = mid;
            e = mid - 1;
        }
        else {
            s = mid + 1;
        }
    }

    return ans;
}

// Function to return the longest subarray
static int longestSubarray(int []a, int n)
{
    // Array for the suffix sum
    // of the above the array.
    int SuffixSum[] = new int[n+1];
    SuffixSum[n] = 0;

    for (int i = n - 1; i >= 0; --i) {
        SuffixSum[i] = SuffixSum[i + 1] + a[i];
    }

    int ans = 0;

    // Search Space for potential starting
    // points of the subarray.
    // It will store the suffix sum
    // till i'th index in increasing order.
    int searchspace[] = new int[n];

    // It will store the indexes
    // till which the suffix sum
    // is present in search space.
    int index[] = new int[n];

    int j = 0;

    for (int i = 0; i < n; ++i) {

        // add the element to the search space if the j=0
        // or if the topmost element is lesser
        // than present suffix sum.
        if ((j == 0) || SuffixSum[i] > searchspace[j - 1]) {
            searchspace[j] = SuffixSum[i];
            index[j] = i;
            j++;
        }

        int idx = search(searchspace, 0, j - 1, SuffixSum[i + 1]);

        // Only when idx is not -1 an subarray is
        // possible with ending index at i.
        if (idx != -1)
            ans = Math.max(ans, i - index[idx] + 1);
    }

    return ans;
}

// Driver Code

    public static void main (String[] args) {
            int []a = { -1, 4, -2, -5, 6, -8 };

    int n = a.length;

    System.out.println(longestSubarray(a, n));
    }
}
// This code is contributed
// by  anuj_67..
```

## 蟒蛇 3

```
# Python3 program to compute the longest
# with sum greater than equal to 0
import math as mt

# function for the searching the
# starting index of the subarray
def search(searchspace, s, e, key):

    # -1 signifies that no starting point
    # of the subarray is not found with
    # sum greater than equal to 0.

    ans = -1

    # Binary search
    while s <= e:
        mid = (s + e) // 2

        if searchspace[mid] - key >= 0:
            ans = mid
            e = mid - 1
        else:
            s = mid + 1
    return ans

# function to return the longest subarray
def longestSubarray(a, n):
    # Array for the suffix sum of
    # the above the array
    SuffixSum = [0 for i in range(n + 1)]

    for i in range(n - 1, -1, -1):
        SuffixSum[i] = SuffixSum[i + 1] + a[i]

    ans = 0

    # Search Space for potential starting
    # points of the subarray.
    # It will store the suffix sum
    # till i'th index in increasing order
    searchspace = [0 for i in range(n)]

    # It will store the indexes
    # till which the suffix sum
    # is present in search space
    index = [0 for i in range(n)]

    j = 0

    for i in range(n):

        # add the element to the search space
        # if the j=0 or if the topmost element
        # is lesser than present suffix sum
        if j == 0 or (SuffixSum[i] >
                      searchspace[j - 1]):
            searchspace[j] = SuffixSum[i]
            index[j] = i
            j += 1

        idx = search(searchspace, 0, j - 1,
                     SuffixSum[i + 1])

        # Only when idx is not -1 an subarray is
        # possible with ending index at i.
        if idx != -1:
            ans = max(ans, i - index[idx] + 1)

    return ans

# Driver Code
a = [-1, 4, -2, -5, 6, -8]

n = len(a)
print(longestSubarray(a, n))

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C#  Program to compute the
// longest subarray with
// sum greater than equal to 0.

using System;

class GFG {

// Function for the searching the
// starting index of the subarray
static int search(int[] searchspace, int s, int e, int key)
{
    // -1 signifies that no
    // starting point of the subarray
    // is not found with sum greater
    // than equal to 0.
    int ans = -1;

    // Binary search
    while (s <= e) {
        int mid = (s + e) / 2;

        if (searchspace[mid] - key >= 0) {
            ans = mid;
            e = mid - 1;
        }
        else {
            s = mid + 1;
        }
    }

    return ans;
}

// Function to return the longest subarray
static int longestSubarray(int[] a, int n)
{
    // Array for the suffix sum
    // of the above the array.
    int[] SuffixSum = new int[n+1];
    SuffixSum[n] = 0;

    for (int i = n - 1; i >= 0; --i) {
        SuffixSum[i] = SuffixSum[i + 1] + a[i];
    }

    int ans = 0;

    // Search Space for potential starting
    // points of the subarray.
    // It will store the suffix sum
    // till i'th index in increasing order.
    int[] searchspace = new int[n];

    // It will store the indexes
    // till which the suffix sum
    // is present in search space.
    int[] index = new int[n];

    int j = 0;

    for (int i = 0; i < n; ++i) {

        // add the element to the search space if the j=0
        // or if the topmost element is lesser
        // than present suffix sum.
        if ((j == 0) || SuffixSum[i] > searchspace[j - 1]) {
            searchspace[j] = SuffixSum[i];
            index[j] = i;
            j++;
        }

        int idx = search(searchspace, 0, j - 1, SuffixSum[i + 1]);

        // Only when idx is not -1 an subarray is
        // possible with ending index at i.
        if (idx != -1)
            ans = Math.Max(ans, i - index[idx] + 1);
    }

    return ans;
}

// Driver Code

    public static void Main () {
            int[] a = { -1, 4, -2, -5, 6, -8 };

    int n = a.Length;

    Console.Write(longestSubarray(a, n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to compute the
// longest subarray with
// sum greater than equal to 0.

// Function for the searching the
// starting index of the subarray
function search($searchspace, $s,
                $e, $key)
{
    // -1 signifies that no starting
    // point of the subarray is not
    // found with sum greater than 
    // equal to 0.
    $ans = -1;

    // Binary search
    while ($s <= $e)
    {
        $mid = ($s + $e) / 2;

        if ($searchspace[$mid] - $key >= 0)
        {
            $ans = $mid;
            $e = $mid - 1;
        }
        else
        {
            $s = $mid + 1;
        }
    }

    return $ans;
}

// Function to return the
// longest subarray
function longestSubarray(&$a, $n)
{
    // Array for the suffix sum
    // of the above the array.
    $SuffixSum[$n] = 0;

    for ($i = $n - 1; $i >= 0; --$i)
    {
        $SuffixSum[$i] = $SuffixSum[$i + 1] +
                         $a[$i];
    }

    $ans = 0;

    // Search Space for potential
    // starting points of the subarray.
    // It will store the suffix sum
    // till i'th index in increasing order.

    // It will store the indexes
    // till which the suffix sum
    // is present in search space.
    $j = 0;

    for ($i = 0; $i < $n; ++$i)
    {

        // add the element to the search
        // space if the j=0 or if the
        // topmost element is lesser
        // than present suffix sum.
        if ($j == 0 or $SuffixSum[$i] >
                       $searchspace[$j - 1])
        {
            $searchspace[$j] = $SuffixSum[$i];
            $index[$j] = $i;
            $j++;
        }

        $idx = search($searchspace, 0, $j - 1,
                      $SuffixSum[$i + 1]);

        // Only when idx is not -1 an
        // subarray is possible with
        // ending index at i.
        if ($idx != -1)
            $ans = max($ans, $i -
                       $index[$idx] + 1);
    }

    return $ans;
}

// Driver Code
$a = array(-1, 4, -2, -5, 6, -8 );
$n = sizeof($a);
echo (longestSubarray($a, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript  Program to compute the
// longest subarray with
// sum greater than equal to 0.

// Function for the searching the
// starting index of the subarray
    function search(searchspace,s,e,key)
    {
        // -1 signifies that no
        // starting point of the subarray
        // is not found with sum greater
        // than equal to 0.
        let ans = -1;

        // Binary search
        while (s <= e) {
            let mid = Math.floor((s + e) / 2);

            if (searchspace[mid] - key >= 0) {
                ans = mid;
                e = mid - 1;
            }
            else {
                s = mid + 1;
            }
        }

        return ans;
    }

    // Function to return the longest subarray
    function longestSubarray(a,n)
    {
        // Array for the suffix sum
        // of the above the array.
        let SuffixSum = new Array(n+1);
        SuffixSum[n] = 0;

        for (let i = n - 1; i >= 0; --i) {
            SuffixSum[i] = SuffixSum[i + 1] + a[i];
        }

        let ans = 0;

        // Search Space for potential starting
        // points of the subarray.
        // It will store the suffix sum
        // till i'th index in increasing order.
        let searchspace = new Array(n);

        // It will store the indexes
        // till which the suffix sum
        // is present in search space.
        let index = new Array(n);

        let j = 0;

        for (let i = 0; i < n; ++i) {

        // add the element to the search space if the j=0
        // or if the topmost element is lesser
        // than present suffix sum.
            if ((j == 0) || SuffixSum[i] > searchspace[j - 1]) {
                searchspace[j] = SuffixSum[i];
                index[j] = i;
                j++;
            }

            let idx = search(searchspace, 0, j - 1, SuffixSum[i + 1]);

        // Only when idx is not -1 an subarray is
        // possible with ending index at i.
            if (idx != -1)
                ans = Math.max(ans, i - index[idx] + 1);
        }

        return ans;
    }

    // Driver Code
    let a=[-1, 4, -2, -5, 6, -8];
    let n = a.length;
    document.write(longestSubarray(a, n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
5
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(N)