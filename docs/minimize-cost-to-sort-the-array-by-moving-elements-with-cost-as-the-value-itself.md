# 通过移动以成本为自身值的元素来最小化成本以对数组进行排序

> 原文:[https://www . geeksforgeeks . org/最小化按移动元素排序数组的成本，将成本作为其本身的价值/](https://www.geeksforgeeks.org/minimize-cost-to-sort-the-array-by-moving-elements-with-cost-as-the-value-itself/)

给定一个正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】****N**，任务是通过将一个数组元素移动到任意位置来找到对给定数组排序的最小成本，这样移动该元素的成本就是该元素的值。

**示例:**

> **输入:** arr[] = {7，1，2，3}
> **输出:** 6
> **解释:**
> 以下是以最小成本排序数组的可能移动集:
> 
> *   将 1 移到前面，arr[] = {1，7，2，3}。成本= 1
> *   将 2 移到第二位，arr[] = {1，2，7，3}。成本= 2
> *   将 3 移到第三位，arr[] = {1，2，3，7}，成本= 3
> 
> 因此，总成本为(1 + 2 + 3) = 6。
> 
> **输入:** arr[] = {7，1，2，5 }
> T3】输出: 7

**方法:**给定的问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。其思想是固定形成具有最大和的[最长非递减子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的数组元素，并对所有剩余的数组元素执行给定的移动。按照以下步骤解决问题:

*   [找到最大和最长的非递减子序列](https://www.geeksforgeeks.org/maximum-sum-increasing-subsequence-dp-14/)并存储在一个变量中，比如 **S** 。
*   完成上述步骤后，打印 **(** [**数组元素之和**](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**–S)**的值，作为排序给定数组的最终可能最小成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// non-decreasing subsequence
int maxSumIS(int arr[], int n)
{
    int i, j, max = 0;

    // Stores the maximum sum of
    // subsequence ending at index i
    int dp[n];

    // Initialize dp[] values for all
    // indexes
    for (i = 0; i < n; i++)
        dp[i] = arr[i];

    // Compute maximum sum values
    // in bottom up manner
    for (i = 1; i < n; i++)
        for (j = 0; j < i; j++)
            if (arr[i] >= arr[j]
                && dp[i] < dp[j] + arr[i])
                dp[i] = dp[j] + arr[i];

    // Pick maximum of all msis values
    for (i = 0; i < n; i++) {
        if (max < dp[i]) {
            max = dp[i];
        }
    }

    // Return the maximum sum as max
    return max;
}

// Function to find the minimum cost to
// sort given array in increasing order
int minCostSort(int arr[], int N)
{
    // Find the sum of array
    int sm = 0;
    for (int i = 0; i < N; i++) {
        sm += arr[i];
    }

    // Find the maximum sum non-decreasing
    // subsequence
    int res = maxSumIS(arr, N);

    // Return the minimum cost
    return sm - res;
}

// Driver Code
int main()
{
    int arr[] = { 7, 1, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << minCostSort(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

    // Function to find the maximum sum of
    // non-decreasing subsequence
    static int maxSumIS(int[] arr, int n)
    {
        int i, j, max = 0;

        // Stores the maximum sum of
        // subsequence ending at index i
        int[] dp = new int[n];

        // Initialize dp[] values for all
        // indexes
        for (i = 0; i < n; i++)
            dp[i] = arr[i];

        // Compute maximum sum values
        // in bottom up manner
        for (i = 1; i < n; i++)
            for (j = 0; j < i; j++)
                if (arr[i] >= arr[j]
                    && dp[i] < dp[j] + arr[i])
                    dp[i] = dp[j] + arr[i];

        // Pick maximum of all msis values
        for (i = 0; i < n; i++) {
            if (max < dp[i]) {
                max = dp[i];
            }
        }

        // Return the maximum sum as max
        return max;
    }

    // Function to find the minimum cost to
    // sort given array in increasing order
    static int minCostSort(int[] arr, int N)
    {
        // Find the sum of array
        int sm = 0;
        for (int i = 0; i < N; i++) {
            sm += arr[i];
        }

        // Find the maximum sum non-decreasing
        // subsequence
        int res = maxSumIS(arr, N);

        // Return the minimum cost
        return sm - res;
    }

    // Driver Code
    public static void main(String []args)
    {
        int[] arr = { 7, 1, 2, 3 };
        int N = arr.length;
        System.out.print(minCostSort(arr, N));
    }
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the maximum sum of
# non-decreasing subsequence
def maxSumIS(arr, n):

    max = 0

    # Stores the maximum sum of
    # subsequence ending at index i
    dp = [0 for _ in range(n)]

    # Initialize dp[] values for all
    # indexes
    for i in range(0, n):
        dp[i] = arr[i]

    # Compute maximum sum values
    # in bottom up manner
    for i in range(1, n):
        for j in range(0, i):
            if (arr[i] >= arr[j] and dp[i] < dp[j] + arr[i]):
                dp[i] = dp[j] + arr[i]

    # Pick maximum of all msis values
    for i in range(0, n):
        if (max < dp[i]):
            max = dp[i]

    # Return the maximum sum as max
    return max

# Function to find the minimum cost to
# sort given array in increasing order
def minCostSort(arr, N):

    # Find the sum of array
    sm = 0
    for i in range(0, N):
        sm += arr[i]

    # Find the maximum sum non-decreasing
    # subsequence
    res = maxSumIS(arr, N)

    # Return the minimum cost
    return sm - res

# Driver Code
if __name__ == "__main__":

    arr = [7, 1, 2, 3]
    N = len(arr)
    print(minCostSort(arr, N))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the maximum sum of
    // non-decreasing subsequence
    static int maxSumIS(int[] arr, int n)
    {
        int i, j, max = 0;

        // Stores the maximum sum of
        // subsequence ending at index i
        int[] dp = new int[n];

        // Initialize dp[] values for all
        // indexes
        for (i = 0; i < n; i++)
            dp[i] = arr[i];

        // Compute maximum sum values
        // in bottom up manner
        for (i = 1; i < n; i++)
            for (j = 0; j < i; j++)
                if (arr[i] >= arr[j]
                    && dp[i] < dp[j] + arr[i])
                    dp[i] = dp[j] + arr[i];

        // Pick maximum of all msis values
        for (i = 0; i < n; i++) {
            if (max < dp[i]) {
                max = dp[i];
            }
        }

        // Return the maximum sum as max
        return max;
    }

    // Function to find the minimum cost to
    // sort given array in increasing order
    static int minCostSort(int[] arr, int N)
    {
        // Find the sum of array
        int sm = 0;
        for (int i = 0; i < N; i++) {
            sm += arr[i];
        }

        // Find the maximum sum non-decreasing
        // subsequence
        int res = maxSumIS(arr, N);

        // Return the minimum cost
        return sm - res;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 7, 1, 2, 3 };
        int N = arr.Length;
        Console.WriteLine(minCostSort(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the maximum sum of
       // non-decreasing subsequence
       function maxSumIS(arr, n) {
           let i, j, max = 0;

           // Stores the maximum sum of
           // subsequence ending at index i
           let dp = new Array(n);

           // Initialize dp[] values for all
           // indexes
           for (i = 0; i < n; i++)
               dp[i] = arr[i];

           // Compute maximum sum values
           // in bottom up manner
           for (i = 1; i < n; i++)
               for (j = 0; j < i; j++)
                   if (arr[i] >= arr[j]
                       && dp[i] < dp[j] + arr[i])
                       dp[i] = dp[j] + arr[i];

           // Pick maximum of all msis values
           for (i = 0; i < n; i++) {
               if (max < dp[i]) {
                   max = dp[i];
               }
           }

           // Return the maximum sum as max
           return max;
       }

       // Function to find the minimum cost to
       // sort given array in increasing order
       function minCostSort(arr, N) {
           // Find the sum of array
           let sm = 0;
           for (let i = 0; i < N; i++) {
               sm += arr[i];
           }

           // Find the maximum sum non-decreasing
           // subsequence
           let res = maxSumIS(arr, N);

           // Return the minimum cost
           return sm - res;
       }

       // Driver Code
       let arr = [7, 1, 2, 3];
       let N = arr.length;
       document.write(minCostSort(arr, N));

    // This code is contributed by Potta Lokesh

   </script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*