# 相邻子序列之间的差值为 1 的最长子序列

> 原文:[https://www . geesforgeks . org/最长子序列相邻子序列之差为 1/](https://www.geeksforgeeks.org/longest-subsequence-such-that-difference-between-adjacents-is-one/)

给定一个 n 大小的数组，任务是找到最长的子序列，使得相邻子序列之间的差为 1。

示例:

```
Input :  arr[] = {10, 9, 4, 5, 4, 8, 6}
Output :  3
As longest subsequences with difference 1 are, "10, 9, 8", 
"4, 5, 4" and "4, 5, 6"

Input :  arr[] = {1, 2, 3, 2, 3, 7, 2, 1}
Output :  7
As longest consecutive sequence is "1, 2, 3, 2, 3, 2, 1"
```

这个问题是基于[最长增子序列问题](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/)的概念。

```
Let arr[0..n-1] be the input array and 
dp[i] be the length of the longest subsequence (with
differences one) ending at index i such that arr[i] 
is the last element of the subsequence.

Then, dp[i] can be recursively written as:
dp[i] = 1 + max(dp[j]) where 0 < j < i and 
       [arr[j] = arr[i] -1  or arr[j] = arr[i] + 1]
dp[i] = 1, if no such j exists.

To find the result for a given array, we need 
to return max(dp[i]) where 0 < i < n.
```

下面是一个基于动态编程的实现。它遵循上面讨论的递归结构。

## C++

```
// C++ program to find the longest subsequence such
// the difference between adjacent elements of the
// subsequence is one.
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of longest subsequence
int longestSubseqWithDiffOne(int arr[], int n)
{
    // Initialize the dp[] array with 1 as a
    // single element will be of 1 length
    int dp[n];
    for (int i = 0; i < n; i++)
        dp[i] = 1;

    // Start traversing the given array
    for (int i = 1; i < n; i++) {
        // Compare with all the previous elements
        for (int j = 0; j < i; j++) {
            // If the element is consecutive then
            // consider this subsequence and update
            // dp[i] if required.
            if ((arr[i] == arr[j] + 1) || (arr[i] == arr[j] - 1))

                dp[i] = max(dp[i], dp[j] + 1);
        }
    }

    // Longest length will be the maximum value
    // of dp array.
    int result = 1;
    for (int i = 0; i < n; i++)
        if (result < dp[i])
            result = dp[i];
    return result;
}

// Driver code
int main()
{
    // Longest subsequence with one difference is
    // {1, 2, 3, 4, 3, 2}
    int arr[] = { 1, 2, 3, 4, 5, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << longestSubseqWithDiffOne(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest subsequence
// such that the difference between adjacent
// elements of the subsequence is one.
import java.io.*;

class GFG {

    // Function to find the length of longest
    // subsequence
    static int longestSubseqWithDiffOne(int arr[],
                                        int n)
    {
        // Initialize the dp[] array with 1 as a
        // single element will be of 1 length
        int dp[] = new int[n];
        for (int i = 0; i < n; i++)
            dp[i] = 1;

        // Start traversing the given array
        for (int i = 1; i < n; i++) {
            // Compare with all the previous
            // elements
            for (int j = 0; j < i; j++) {
                // If the element is consecutive
                // then consider this subsequence
                // and update dp[i] if required.
                if ((arr[i] == arr[j] + 1) || (arr[i] == arr[j] - 1))

                    dp[i] = Math.max(dp[i], dp[j] + 1);
            }
        }

        // Longest length will be the maximum
        // value of dp array.
        int result = 1;
        for (int i = 0; i < n; i++)
            if (result < dp[i])
                result = dp[i];
        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Longest subsequence with one
        // difference is
        // {1, 2, 3, 4, 3, 2}
        int arr[] = { 1, 2, 3, 4, 5, 3, 2 };
        int n = arr.length;
        System.out.println(longestSubseqWithDiffOne(
            arr, n));
    }
}

// This code is contributed by Prerna Saini
```

## 计算机编程语言

```
# Function to find the length of longest subsequence
def longestSubseqWithDiffOne(arr, n):
    # Initialize the dp[] array with 1 as a
    # single element will be of 1 length
    dp = [1 for i in range(n)]

    # Start traversing the given array
    for i in range(n):
        # Compare with all the previous elements
        for j in range(i):
            # If the element is consecutive then
            # consider this subsequence and update
            # dp[i] if required.
            if ((arr[i] == arr[j]+1) or (arr[i] == arr[j]-1)):
                dp[i] = max(dp[i], dp[j]+1)

    # Longest length will be the maximum value
    # of dp array.
    result = 1  
    for i in range(n):
        if (result < dp[i]):
            result = dp[i]

    return result

# Driver code
arr = [1, 2, 3, 4, 5, 3, 2]
# Longest subsequence with one difference is
# {1, 2, 3, 4, 3, 2}
n = len(arr)
print longestSubseqWithDiffOne(arr, n)

# This code is contributed by Afzal Ansari
```

## C#

```
// C# program to find the longest subsequence
// such that the difference between adjacent
// elements of the subsequence is one.
using System;

class GFG {

    // Function to find the length of longest
    // subsequence
    static int longestSubseqWithDiffOne(int[] arr,
                                        int n)
    {

        // Initialize the dp[] array with 1 as a
        // single element will be of 1 length
        int[] dp = new int[n];

        for (int i = 0; i < n; i++)
            dp[i] = 1;

        // Start traversing the given array
        for (int i = 1; i < n; i++) {

            // Compare with all the previous
            // elements
            for (int j = 0; j < i; j++) {
                // If the element is consecutive
                // then consider this subsequence
                // and update dp[i] if required.
                if ((arr[i] == arr[j] + 1) || (arr[i] == arr[j] - 1))

                    dp[i] = Math.Max(dp[i], dp[j] + 1);
            }
        }

        // Longest length will be the maximum
        // value of dp array.
        int result = 1;
        for (int i = 0; i < n; i++)
            if (result < dp[i])
                result = dp[i];

        return result;
    }

    // Driver code
    public static void Main()
    {

        // Longest subsequence with one
        // difference is
        // {1, 2, 3, 4, 3, 2}
        int[] arr = { 1, 2, 3, 4, 5, 3, 2 };
        int n = arr.Length;

        Console.Write(
            longestSubseqWithDiffOne(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the longest
// subsequence such the difference
// between adjacent elements of the
// subsequence is one.

// Function to find the length of
// longest subsequence
function longestSubseqWithDiffOne($arr, $n)
{

    // Initialize the dp[]
    // array with 1 as a
    // single element will
    // be of 1 length
    $dp[$n] = 0;

    for($i = 0; $i< $n; $i++)
        $dp[$i] = 1;

    // Start traversing the
    // given array
    for($i = 1; $i < $n; $i++)
    {

        // Compare with all the
        // previous elements
        for($j = 0; $j < $i; $j++)
        {

            // If the element is
            // consecutive then
            // consider this
            // subsequence and
            // update dp[i] if
            // required.
            if (($arr[$i] == $arr[$j] + 1) ||
                ($arr[$i] == $arr[$j] - 1))

                $dp[$i] = max($dp[$i],
                         $dp[$j] + 1);
        }
    }

    // Longest length will be
    // the maximum value
    // of dp array.
    $result = 1;
    for($i = 0 ; $i < $n ; $i++)
        if ($result < $dp[$i])
            $result = $dp[$i];
    return $result;
}

    // Driver code
    // Longest subsequence with
    // one difference is
    // {1, 2, 3, 4, 3, 2}
    $arr = array(1, 2, 3, 4, 5, 3, 2);
    $n = sizeof($arr);
    echo longestSubseqWithDiffOne($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the
// longest subsequence such that the
// difference between adjacent elements
// of the subsequence is one.

// Function to find the length of longest
// subsequence
function longestSubseqWithDiffOne(arr, n)
{

    // Initialize the dp[] array with 1 as a
    // single element will be of 1 length
    let dp = [];
    for(let i = 0; i < n; i++)
        dp[i] = 1;

    // Start traversing the given array
    for(let i = 1; i < n; i++)
    {

        // Compare with all the previous
        // elements
        for(let j = 0; j < i; j++)
        {

            // If the element is consecutive
            // then consider this subsequence
            // and update dp[i] if required.
            if ((arr[i] == arr[j] + 1) ||
                (arr[i] == arr[j] - 1))

            dp[i] = Math.max(dp[i], dp[j] + 1);
        }
    }

    // Longest length will be the maximum
    // value of dp array.
    let result = 1;
    for(let i = 0; i < n; i++)
        if (result < dp[i])
            result = dp[i];

    return result;
}

// Driver Code

// Longest subsequence with one
// difference is
// {1, 2, 3, 4, 3, 2}
let arr = [1, 2, 3, 4, 5, 3, 2];
let n = arr.length;

document.write(longestSubseqWithDiffOne(arr, n));

// This code is contributed by souravghosh0416

</script>
```

**输出:**

```
6
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(n)

**高效方法**

## C++

```
#include<bits/stdc++.h>
using namespace std;
int longestSubsequence(int n, int arr[])
    {
        if(n==1)
            return 1;
        int dp[n];
        unordered_map<int,int> mapp;
        dp[0]=1;
        mapp[arr[0]]=0;
        for(int i=1;i<n;i++){
            if(abs(arr[i]-arr[i-1])==1)
                dp[i]=dp[i-1]+1;
            else{
                if(mapp.count(arr[i]+1) >0 || mapp.count(arr[i]-1)){
                    dp[i]=1+max(mapp[arr[i]+1],mapp[arr[i]-1]);
                }
                else
                    dp[i]=1;
            }
            mapp[arr[i]]=dp[i];
        }
        return (*max_element(dp,dp+n));
    }
int main()
{
    // Longest subsequence with one difference is
    // {1, 2, 3, 4, 3, 2}
    int arr[] = {1, 2, 3, 4, 5, 3, 2};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << longestSubsequence(n, arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.lang.Math;
import java.util.*;

class GFG {

    static int longestSubsequence(int n, int arr[])
    {
        if (n == 1)
            return 1;
        Integer dp[] = new Integer[n];
        HashMap<Integer, Integer> mapp = new HashMap<>();
        dp[0] = 1;
        mapp.put(arr[0], 0);
        for (int i = 1; i < n; i++) {
            if (Math.abs(arr[i] - arr[i - 1]) == 1)
                dp[i] = dp[i - 1] + 1;
            else {
                if (mapp.containsKey(arr[i] + 1)
                    || mapp.containsKey(arr[i] - 1)) {
                    dp[i] = 1
                            + Math.max(mapp.getOrDefault(
                                           arr[i] + 1, 0),
                                       mapp.getOrDefault(
                                           arr[i] - 1, 0));
                }
                else
                    dp[i] = 1;
            }
            mapp.put(arr[i], dp[i]);
        }
        return Collections.max(Arrays.asList(dp));
    }

    public static void main(String[] args)
    {
        // Longest subsequence with one
        // difference is
        // {1, 2, 3, 4, 3, 2}
        int arr[] = { 1, 2, 3, 4, 5, 3, 2 };
        int n = arr.length;
        System.out.println(longestSubsequence(n, arr));
    }
}

// This code is contributed by rajsanghavi9.
```

## 蟒蛇 3

```
def longestSubsequence(A, N):
    L = [1]*N
    hm = {}
    for i in range(1,N):
        if abs(A[i]-A[i-1]) == 1:
            L[i] = 1 + L[i-1]
        elif hm.get(A[i]+1,0) or hm.get(A[i]-1,0):
            L[i] = 1+max(hm.get(A[i]+1,0), hm.get(A[i]-1,0))
        hm[A[i]] = L[i]
    return max(L)
# Driver code
A =  [1, 2, 3, 4, 5, 3, 2]
N = len(A)
print(longestSubsequence(A, N))
```

**输出:**

```
6
```

本文由[**Sahil Chhabra(KILLER)**](https://www.facebook.com/sahil.chhabra.965)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。