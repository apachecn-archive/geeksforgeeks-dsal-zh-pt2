# 在每个位置具有非负前缀和的最长子序列

> 原文:[https://www . geeksforgeeks . org/每个位置有非负前缀的最长子序列/](https://www.geeksforgeeks.org/longest-subsequence-with-non-negative-prefix-sum-at-each-position/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到[个最长的子序列](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)，使得子序列每个位置的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)为非负。

**示例:**

> **输入:** arr[] = {4，-4，1，-3，1，-3}
> **输出:** 5
> **解释:**
> 考虑子序列为{4，1，-3，1，-3}。现在，所选子序列的前缀和为{4，5，2，3，0}。因为，前缀和在每个可能的索引处都是非负的。因此，这个子序列的最大长度为 5。
> 
> **输入:** arr[] = {1，3，5，7}
> **输出:** 4

**天真方法:**解决这个问题最简单的方法是[生成给定数组的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，并打印该子序列的长度，该子序列在每个位置都有一个非负的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，并且长度最大。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(2 <sup>N</sup> )*

**高效方法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为它具有[重叠子问题属性](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构属性](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。像其他[动态规划](https://www.geeksforgeeks.org/dynamic-programming/) (DP)问题一样，通过构造一个存储子问题结果的临时数组，可以避免相同子问题的重新计算。按照以下步骤解决问题:

*   初始化一个矩阵，说 **dp[][]** ，其中 **dp[i][j]** 存储最大可能和，如果有 **j** 有效元素，直到位置 **i** 和**T9】用 **-1** 初始化 **dp[][]** 数组。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，并将**DP【I】【0】**更新为 **0** 。
*   如果 **arr[0]** 的值至少为 **0** ，则更新 **dp[0][1]** 为 **arr[0]** 。否则，更新为 **-1** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N–1】**:
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，I+1】**:
        *   如果当前元素被**排除**，即如果**DP[I–1][j]**不等于 **-1** ，则更新 **dp[i][j]** 为 **dp[i][j]** 和**DP[I–1][j]**的最大值。
        *   如果包含当前元素**，即如果**DP[I–1][j–1]**和**DP[I–1][j–1]+arr[I]**大于或等于 **0** ，则更新 **dp[i][j]** 的值，作为 **dp[i][j]** 和**DP[I–1][j–1]+arr**的最大值**
*   **初始化一个变量 say， **ans** 为 **0** ，在每个位置存储非负[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的[最长子序列](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)。**
*   **[使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**内迭代，如果**DP【N–1】【j】**大于等于 **0** ，则将 **ans** 的值更新为 **j** 。**
*   **完成上述步骤后，打印**和**的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// longest subsequence with non negative
// prefix sum at each position
void longestSubsequence(int* arr, int N)
{
    // Stores the maximum sum possible
    // if we include j elements till
    // the position i
    int dp[N][N + 1];

    // Initialize dp array with -1
    memset(dp, -1, sizeof dp);

    // Maximum subsequence sum by
    // including no elements till
    // position 'i'
    for (int i = 0; i < N; ++i) {
        dp[i][0] = 0;
    }

    // Maximum subsequence sum by
    // including first element at
    // first position
    dp[0][1] = (arr[0] >= 0 ? arr[0] : -1);

    // Iterate over all the remaining
    // positions
    for (int i = 1; i < N; ++i) {

        for (int j = 1;
             j <= (i + 1); ++j) {

            // If the current element
            // is excluded
            if (dp[i - 1][j] != -1) {
                dp[i][j] = max(
                    dp[i][j], dp[i - 1][j]);
            }

            // If current element is
            // included and if total
            // sum is positive or not
            if (dp[i - 1][j - 1] >= 0
                && dp[i - 1][j - 1]
                           + arr[i]
                       >= 0) {

                dp[i][j] = max(
                    dp[i][j],
                    dp[i - 1][j - 1]
                        + arr[i]);
            }
        }
    }

    int ans = 0;

    // Select the maximum j by which
    // a non negative prefix sum
    // subsequence can be obtained
    for (int j = 0; j <= N; ++j) {
        if (dp[N - 1][j] >= 0) {
            ans = j;
        }
    }

    // Print the answer
    cout << ans << endl;
}

// Driver Code
int main()
{
    int arr[] = { 4, -4, 1, -3, 1, -3 };
    int N = sizeof arr / sizeof arr[0];
    longestSubsequence(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the length of the
// longest subsequence with non negative
// prefix sum at each position
static void longestSubsequence(int[] arr, int N)
{

    // Stores the maximum sum possible
    // if we include j elements till
    // the position i
    int dp[][] = new int[N][N + 1];

    // Initialize dp array with -1
    for(int i = 0; i < N; ++i)
    {
        for(int j = 0; j < N + 1; ++j)
        {
            dp[i][j] = -1;
        }
    }

    // Maximum subsequence sum by
    // including no elements till
    // position 'i'
    for(int i = 0; i < N; ++i)
    {
        dp[i][0] = 0;
    }

    // Maximum subsequence sum by
    // including first element at
    // first position
    dp[0][1] = (arr[0] >= 0 ? arr[0] : -1);

    // Iterate over all the remaining
    // positions
    for(int i = 1; i < N; ++i)
    {
        for(int j = 1; j <= (i + 1); ++j)
        {

            // If the current element
            // is excluded
            if (dp[i - 1][j] != -1)
            {
                dp[i][j] = Math.max(
                    dp[i][j], dp[i - 1][j]);
            }

            // If current element is
            // included and if total
            // sum is positive or not
            if (dp[i - 1][j - 1] >= 0 &&
                dp[i - 1][j - 1] + arr[i] >= 0)
            {
                dp[i][j] = Math.max(dp[i][j],
                                    dp[i - 1][j - 1] +
                                   arr[i]);
            }
        }
    }

    int ans = 0;

    // Select the maximum j by which
    // a non negative prefix sum
    // subsequence can be obtained
    for(int j = 0; j <= N; ++j)
    {
        if (dp[N - 1][j] >= 0)
        {
            ans = j;
        }
    }

    // Print the answer
    System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, -4, 1, -3, 1, -3 };
    int N = arr.length;

    longestSubsequence(arr, N);
}
}

// This code is contributed by avijitmondal1998
```

## **蟒蛇 3**

```
# Python3 Program for the above approach

# Function to find the length of the
# longest subsequence with non negative
# prefix sum at each position
def longestSubsequence(arr, N):

    # Stores the maximum sum possible
    # if we include j elements till
    # the position i

    # Initialize dp array with -1
    dp = [[-1 for i in range(N + 1)] for i in range(N)]

    # Maximum subsequence sum by
    # including no elements till
    # position 'i'
    for i in range(N):
        dp[i][0] = 0

    # Maximum subsequence sum by
    # including first element at
    # first position
    dp[0][1] = arr[0] if arr[0] >= 0 else -1

    # Iterate over all the remaining
    # positions
    for i in range(1, N):

        for j in range(1, i + 2):

            # If the current element
            # is excluded
            if (dp[i - 1][j] != -1):
                dp[i][j] = max(dp[i][j], dp[i - 1][j])

            # If current element is
            # included and if total
            # sum is positive or not
            if (dp[i - 1][j - 1] >= 0 and dp[i - 1][j - 1] + arr[i] >= 0):

                dp[i][j] = max(dp[i][j], dp[i - 1][j - 1] + arr[i])

    ans = 0

    # Select the maximum j by which
    # a non negative prefix sum
    # subsequence can be obtained
    for j in range(N + 1):
        if (dp[N - 1][j] >= 0):
            ans = j

    # Print the answer
    print(ans)

# Driver Code

arr = [4, -4, 1, -3, 1, -3]
N = len(arr)
longestSubsequence(arr, N)

# This code is contributed by _saurabhy_jaiswal
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to find the length of the
// longest subsequence with non negative
// prefix sum at each position
static void longestSubsequence(int[] arr, int N)
{

    // Stores the maximum sum possible
    // if we include j elements till
    // the position i
    int[,] dp = new int[N, N + 1];

    // Initialize dp array with -1
    for(int i = 0; i < N; ++i)
    {
        for(int j = 0; j < N + 1; ++j)
        {
            dp[i, j] = -1;
        }
    }

    // Maximum subsequence sum by
    // including no elements till
    // position 'i'
    for(int i = 0; i < N; ++i)
    {
        dp[i, 0] = 0;
    }

    // Maximum subsequence sum by
    // including first element at
    // first position
    dp[0, 1] = (arr[0] >= 0 ? arr[0] : -1);

    // Iterate over all the remaining
    // positions
    for(int i = 1; i < N; ++i)
    {
        for(int j = 1; j <= (i + 1); ++j)
        {

            // If the current element
            // is excluded
            if (dp[i - 1, j] != -1)
            {
                dp[i, j] = Math.Max(dp[i, j],
                                    dp[i - 1, j]);
            }

            // If current element is
            // included and if total
            // sum is positive or not
            if (dp[i - 1, j - 1] >= 0 &&
                dp[i - 1, j - 1] + arr[i] >= 0)
            {
                dp[i, j] = Math.Max(dp[i, j],
                                    dp[i - 1, j - 1] +
                                    arr[i]);
            }
        }
    }

    int ans = 0;

    // Select the maximum j by which
    // a non negative prefix sum
    // subsequence can be obtained
    for(int j = 0; j <= N; ++j)
    {
        if (dp[N - 1, j] >= 0)
        {
            ans = j;
        }
    }

    // Print the answer
    Console.Write(ans);
}

// Driver code
public static void Main()
{
    int[] arr = { 4, -4, 1, -3, 1, -3 };
    int N = arr.Length;

    longestSubsequence(arr, N);
}
}

// This code is contributed by ukasp
```

## **java 描述语言**

```
<script>
       // JavaScript Program for the above approach

       // Function to find the length of the
       // longest subsequence with non negative
       // prefix sum at each position
       function longestSubsequence(arr, N)
       {

           // Stores the maximum sum possible
           // if we include j elements till
           // the position i

           // Initialize dp array with -1
           let dp = Array(N).fill().map(() => Array(N + 1).fill(-1));

           // Maximum subsequence sum by
           // including no elements till
           // position 'i'
           for (let i = 0; i < N; ++i) {
               dp[i][0] = 0;
           }

           // Maximum subsequence sum by
           // including first element at
           // first position
           dp[0][1] = (arr[0] >= 0 ? arr[0] : -1);

           // Iterate over all the remaining
           // positions
           for (let i = 1; i < N; ++i) {

               for (let j = 1;
                   j <= (i + 1); ++j) {

                   // If the current element
                   // is excluded
                   if (dp[i - 1][j] != -1) {
                       dp[i][j] = Math.max(
                           dp[i][j], dp[i - 1][j]);
                   }

                   // If current element is
                   // included and if total
                   // sum is positive or not
                   if (dp[i - 1][j - 1] >= 0
                       && dp[i - 1][j - 1]
                       + arr[i]
                       >= 0) {

                       dp[i][j] = Math.max(
                           dp[i][j],
                           dp[i - 1][j - 1]
                           + arr[i]);
                   }
               }
           }

           let ans = 0;

           // Select the maximum j by which
           // a non negative prefix sum
           // subsequence can be obtained
           for (let j = 0; j <= N; ++j) {
               if (dp[N - 1][j] >= 0) {
                   ans = j;
               }
           }

           // Print the answer
           document.write(ans);
       }

       // Driver Code

       let arr = [4, -4, 1, -3, 1, -3];
       let N = arr.length;
       longestSubsequence(arr, N);

   // This code is contributed by Potta Lokesh

   </script>
```

****Output:** 

```
5
```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )***