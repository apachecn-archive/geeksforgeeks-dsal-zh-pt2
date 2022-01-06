# 不包含给定序列的最长递增子序列的长度作为子阵列

> 原文:[https://www . geeksforgeeks . org/最长递增子序列长度不包含给定序列作为子阵列/](https://www.geeksforgeeks.org/length-of-the-longest-increasing-subsequence-which-does-not-contain-a-given-sequence-as-subarray/)

给定两个长度分别为 **N** 和 **M** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和 **arr1[]** ，任务是找到阵列[最长的递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/) **arr[]** ，使其不包含阵列 **arr1[]** 作为[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。

**示例:**

> **输入:** arr[] = {5，3，9，3，4，7}，arr1[] = {3，3，7}
> **输出:** 4
> **解释:**要求的最长递增子序列为{3，3，4，7}。
> 
> **输入:** arr[] = {1，2，3}，arr1[] = {1，2，3}
> **输出:** 2
> **说明:**所需最长递增子序列为{1，2}。

**朴素方法:**最简单的方法是[生成给定数组的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，并打印其中最长子序列的长度，不包含 arr1[]作为子数组。

***时间复杂度:** O(M * 2 <sup>N</sup> ，其中 N 和 M 是给定数组的长度。*
***辅助空间:** O(M + N)*

**高效方法:**思路是利用 [KMP 算法](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)和[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)生成的 [lps【】数组](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)找到[最长的不减子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)没有任何子数组等于**序列【】**。按照以下步骤解决问题:

1.  初始化一个数组 **dp[N][N][N]** ，其中 **dp[i][j][K]** 存储[非递减子序列的最大长度](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)直到索引 **i** ，其中 **j** 是数组 **arr[]** 中先前选择的元素的索引 **K** 表示当前找到的序列包含子数组**序列【0，K】**。
2.  另外，使用 [KMP 算法](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)生成一个数组来存储最长前缀后缀的长度。
3.  最大长度可以通过记忆以下 dp 转变找到:

> **dp(i，prev，k) = max(1 + dp(i + 1，I，k2)，dp(i + 1，prev，k))** 其中，
> 
> *   **i** 为当前指数。
> *   **prev** 是之前选择的元素。
> *   **k2** 是当前找到的序列中迄今为止包括的前缀子阵列的索引，该序列可以使用最长前缀后缀的 KMP 阵列来找到。
> 
> **基本情况:**
> 
> *   如果 k 等于给定序列的长度，则返回，因为当前找到的子序列包含 arr1[]。
> *   如果我到达 N，返回，因为没有更多的元素存在。
> *   如果已经计算出当前状态，则返回。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Initialize dp and KMP array
int dp[6][6][6];
int KMPArray[2];

// Length of the given sequence[]
int m;

// Function to find the max-length
// subsequence that does not have
// subarray sequence[]
int findSubsequence(int a[], int sequence[], int i,
                    int prev, int k, int al, int sl)
{
    // Stores the subsequence
    // explored so far
    if (k == m)
        return INT_MIN;

    // Base Case
    if (i == al)
        return 0;

    // Using memoization to
    // avoid re-computation
    if (prev != -1 && dp[i][prev][k] != -1) {
        return dp[i][prev][k];
    }

    int include = 0;

    if (prev == -1 || a[i] >= a[prev]) {
        int k2 = k;

        // Using KMP array to find
        // corresponding index in arr1[]
        while (k2 > 0
               && a[i] != sequence[k2])
            k2 = KMPArray[k2 - 1];

        // Incrementing k2 as we are
        // including this element in
        // the subsequence
        if (a[i] == sequence[k2])
            k2++;

        // Possible answer for
        // current state
        include = 1
                  + findSubsequence(
                        a, sequence,
                        i + 1, i, k2, al, sl);
    }

    // Maximum answer for
    // current state
    int ans = max(
        include, findSubsequence(
                     a, sequence,
                     i + 1, prev, k, al, sl));

    // Memoizing the answer for
    // the corresponding state
    if (prev != -1) {
        dp[i][prev][k] = ans;
    }

    // Return the answer for
    // current state
    return ans;
}

// Function that generate KMP Array
void fillKMPArray(int pattern[])
{

    // Previous longest prefix suffix
    int j = 0;

    int i = 1;

    // KMPArray[0] is a always 0
    KMPArray[0] = 0;

    // The loop calculates KMPArray[i]
    // for i = 1 to M - 1
    while (i < m) {

        // If current character is
        // same
        if (pattern[i] == pattern[j]) {
            j++;

            // Update the KMP array
            KMPArray[i] = j;
            i++;
        }

        // Otherwise
        else {

            // Update the KMP array
            if (j != 0)
                j = KMPArray[j - 1];
            else {
                KMPArray[i] = j;
                i++;
            }
        }
    }
}

// Function to print the maximum
// possible length
void printAnswer(int a[], int sequence[], int al, int sl)
{

    // Length of the given sequence
    m = sl;

    // Generate KMP array
    fillKMPArray(sequence);

    // Initialize the states to -1
    memset(dp, -1, sizeof(dp));

    // Get answer
    int ans = findSubsequence(a, sequence, 0, -1, 0, al, sl);

    // Print answer
    cout << ((ans < 0) ? 0 : ans) << endl;
}

// Driver code
int main()
{

    // Given array
    int arr[] = { 5, 3, 9, 3, 4, 7 };

    // Give arr1
    int arr1[] = { 3, 4 };

    // Function Call
    printAnswer(arr, arr1, 6, 2);
    return 0;
}

// This code is contributed by divyeshrabadiya07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Initialize dp and KMP array
    static int[][][] dp;
    static int[] KMPArray;

    // Length of the given sequence[]
    static int m;

    // Function to find the max-length
    // subsequence that does not have
    // subarray sequence[]
    private static int findSubsequence(
        int[] a, int[] sequence,
        int i, int prev, int k)
    {
        // Stores the subsequence
        // explored so far
        if (k == m)
            return Integer.MIN_VALUE;

        // Base Case
        if (i == a.length)
            return 0;

        // Using memoization to
        // avoid re-computation
        if (prev != -1
            && dp[i][prev][k] != -1) {
            return dp[i][prev][k];
        }

        int include = 0;

        if (prev == -1 || a[i] >= a[prev]) {
            int k2 = k;

            // Using KMP array to find
            // corresponding index in arr1[]
            while (k2 > 0
                   && a[i] != sequence[k2])
                k2 = KMPArray[k2 - 1];

            // Incrementing k2 as we are
            // including this element in
            // the subsequence
            if (a[i] == sequence[k2])
                k2++;

            // Possible answer for
            // current state
            include = 1
                      + findSubsequence(
                            a, sequence,
                            i + 1, i, k2);
        }

        // Maximum answer for
        // current state
        int ans = Math.max(
            include, findSubsequence(
                         a, sequence,
                         i + 1, prev, k));

        // Memoizing the answer for
        // the corresponding state
        if (prev != -1) {
            dp[i][prev][k] = ans;
        }

        // Return the answer for
        // current state
        return ans;
    }

    // Function that generate KMP Array
    private static void
    fillKMPArray(int[] pattern)
    {
        // Previous longest prefix suffix
        int j = 0;

        int i = 1;

        // KMPArray[0] is a always 0
        KMPArray[0] = 0;

        // The loop calculates KMPArray[i]
        // for i = 1 to M - 1
        while (i < m) {

            // If current character is
            // same
            if (pattern[i] == pattern[j]) {
                j++;

                // Update the KMP array
                KMPArray[i] = j;
                i++;
            }

            // Otherwise
            else {

                // Update the KMP array
                if (j != 0)
                    j = KMPArray[j - 1];
                else {
                    KMPArray[i] = j;
                    i++;
                }
            }
        }
    }

    // Function to print the maximum
    // possible length
    static void printAnswer(
        int a[], int sequence[])
    {

        // Length of the given sequence
        m = sequence.length;

        // Initialize kmp array
        KMPArray = new int[m];

        // Generate KMP array
        fillKMPArray(sequence);

        // Initialize dp
        dp = new int[a.length][a.length][a.length];

        // Initialize the states to -1
        for (int i = 0; i < a.length; i++)
            for (int j = 0; j < a.length; j++)
                Arrays.fill(dp[i][j], -1);

        // Get answer
        int ans = findSubsequence(
            a, sequence, 0, -1, 0);

        // Print answer
        System.out.println((ans < 0) ? 0 : ans);
    }

    // Driver code
    public static void
        main(String[] args) throws Exception
    {
        // Given array
        int[] arr = { 5, 3, 9, 3, 4, 7 };

        // Give arr1
        int[] arr1 = { 3, 4 };

        // Function Call
        printAnswer(arr, arr1);
    }
}
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Initialize dp and KMP array
static int[,,] dp;
static int[] KMPArray;

// Length of the given sequence[]
static int m;

// Function to find the max-length
// subsequence that does not have
// subarray sequence[]
private static int findSubsequence(int[] a,
                                   int[] sequence,
                                   int i, int prev,
                                   int k)
{

    // Stores the subsequence
    // explored so far
    if (k == m)
        return int.MinValue;

    // Base Case
    if (i == a.Length)
        return 0;

    // Using memoization to
    // avoid re-computation
    if (prev != -1 && dp[i, prev, k] != -1)
    {
        return dp[i, prev, k];
    }

    int include = 0;

    if (prev == -1 || a[i] >= a[prev])
    {
        int k2 = k;

        // Using KMP array to find
        // corresponding index in arr1[]
        while (k2 > 0 && a[i] != sequence[k2])
            k2 = KMPArray[k2 - 1];

        // Incrementing k2 as we are
        // including this element in
        // the subsequence
        if (a[i] == sequence[k2])
            k2++;

        // Possible answer for
        // current state
        include = 1 + findSubsequence(a, sequence,
                                      i + 1, i, k2);
    }

    // Maximum answer for
    // current state
    int ans = Math.Max(include,
                       findSubsequence(a, sequence,
                                       i + 1, prev, k));

    // Memoizing the answer for
    // the corresponding state
    if (prev != -1)
    {
        dp[i, prev, k] = ans;
    }

    // Return the answer for
    // current state
    return ans;
}

// Function that generate KMP Array
private static void fillKMPArray(int[] pattern)
{

    // Previous longest prefix suffix
    int j = 0;

    int i = 1;

    // KMPArray[0] is a always 0
    KMPArray[0] = 0;

    // The loop calculates KMPArray[i]
    // for i = 1 to M - 1
    while (i < m)
    {

        // If current character is
        // same
        if (pattern[i] == pattern[j])
        {
            j++;

            // Update the KMP array
            KMPArray[i] = j;
            i++;
        }

        // Otherwise
        else
        {

            // Update the KMP array
            if (j != 0)
                j = KMPArray[j - 1];
            else
            {
                KMPArray[i] = j;
                i++;
            }
        }
    }
}

// Function to print the maximum
// possible length
static void printAnswer(int[] a, int[] sequence)
{

    // Length of the given sequence
    m = sequence.Length;

    // Initialize kmp array
    KMPArray = new int[m];

    // Generate KMP array
    fillKMPArray(sequence);

    // Initialize dp
    dp = new int[a.Length, a.Length, a.Length];

    // Initialize the states to -1
    for(int i = 0; i < a.Length; i++)
        for(int j = 0; j < a.Length; j++)
            for(int k = 0; k < a.Length; k++)
                dp[i, j, k] = -1;

    // Get answer
    int ans = findSubsequence(a, sequence, 0, -1, 0);

    // Print answer
    Console.WriteLine((ans < 0) ? 0 : ans);
}

// Driver code
public static void Main()
{

    // Given array
    int[] arr = { 5, 3, 9, 3, 4, 7 };

    // Give arr1
    int[] arr1 = { 3, 4 };

    // Function Call
    printAnswer(arr, arr1);
}
}

// This code is contributed by akhilsaini
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>3</sup> )*