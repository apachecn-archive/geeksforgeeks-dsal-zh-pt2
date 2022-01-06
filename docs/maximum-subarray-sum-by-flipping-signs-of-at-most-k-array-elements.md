# 通过翻转最多 K 个阵列元素的符号得到的最大子阵列和

> 原文:[https://www . geesforgeks . org/max-subarray-sum-by-flip-至多 k 个数组元素的符号/](https://www.geeksforgeeks.org/maximum-subarray-sum-by-flipping-signs-of-at-most-k-array-elements/)

给定一个由 **N** 个整数和一个整数 **K** 组成的数组 **arr[]** 。任务是通过翻转最多 **K** 个数组元素的符号来找到最大的子数组和。

**示例:**

> **输入:** arr[] = {-6，2，-1，-1000，2}，k = 2
> **输出:** 1009
> 我们可以翻转-6 和-1000 的符号，得到最大子阵和为 1009
> 
> **输入:** arr[] = {-1，-2，-100，-10}，k = 1
> **输出:** 100
> 我们只能翻转-100 的符号得到 100
> 
> **输入:** {1，2，100，10}，k = 1
> **输出:** 113
> 我们不需要翻转任何元素

**方法:**使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。假设 dp[i][j]是来自索引 I 的最大子数组和，带有 j 个翻转。可以写一个递归函数来解决这个问题，我们可以记住它来避免多次函数调用。递归 DP 函数**(findsbarraysum(ind，flings))**将从初始翻转次数为 0 的每个索引中调用。

> ans = max(0，a[ind]+findsbarray sum(ind+ 1，翻转，n，a，k))
> ans = max(ans，-a[ind]+findsbarray sum(ind+1，翻转+1，n，a，k))
> 如果该值为负，我们将其替换为 0，与我们在 Kadane 的算法中所做的类似。

递归函数将有两种状态，一种是如果我们翻转第 I 个索引。第二个如果我们不翻转第 I 个索引。基本情况是如果 ind==n，当我们完成一个遍历直到最后一个索引。我们可以使用记忆来存储结果，这些结果可以在以后使用，以避免多次相同的函数调用。所有 dp[i][0]中的最大值将是我们的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define right 2
#define left 4
int dp[left][right];

// Function to find the maximum subarray sum with flips
// starting from index i
int findSubarraySum(int ind, int flips, int n, int a[],
                    int k)
{

    // If the number of flips have exceeded
    if (flips > k)
        return -1e9;

    // Complete traversal
    if (ind == n)
        return 0;

    // If the state has previously been visited
    if (dp[ind][flips] != -1)
        return dp[ind][flips];

    // Initially
    int ans = 0;

    // Use Kadane's algorithm and call two states
    ans = max(
        0,
        a[ind] + findSubarraySum(ind + 1, flips, n, a, k));
    ans = max(ans, -a[ind]
                       + findSubarraySum(ind + 1, flips + 1,
                                         n, a, k));

    // Memoize the answer and return it
    return dp[ind][flips] = ans;
}

// Utility function to call flips from index and
// return the answer
int findMaxSubarraySum(int a[], int n, int k)
{
    // Create DP array
    // int dp[n][k+1];
    memset(dp, -1, sizeof(dp));

    int ans = -1e9;

    // Iterate and call recursive function
    // from every index to get the maximum subarray sum
    for (int i = 0; i < n; i++)
        ans = max(ans, findSubarraySum(i, 0, n, a, k));

    // corner case
    if (ans == 0 && k == 0)
        return *max_element(a, a + n);

    return ans;
}

// Driver Code
int main()
{
    int a[] = { -1, -2, -100, -10 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 1;

    cout << findMaxSubarraySum(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;
class GFG {

    static int right = 2;
    static int left = 4;
    static int[][] dp = new int[left][right];

    // Function to find the maximum subarray sum with flips
    // starting from index i
    static int findSubarraySum(int ind, int flips, int n,
                               int[] a, int k)
    {

        // If the number of flips have exceeded
        if (flips > k)
            return (int)(-1e9);

        // Complete traversal
        if (ind == n)
            return 0;

        // If the state has previously been visited
        if (dp[ind][flips] != -1)
            return dp[ind][flips];

        // Initially
        int ans = 0;

        // Use Kadane's algorithm and call two states
        ans = Math.max(0, a[ind]
                              + findSubarraySum(
                                  ind + 1, flips, n, a, k));
        ans = Math.max(ans, -a[ind]
                                + findSubarraySum(ind + 1,
                                                  flips + 1,
                                                  n, a, k));

        // Memoize the answer and return it
        return dp[ind][flips] = ans;
    }

    // Utility function to call flips from index and
    // return the answer
    static int findMaxSubarraySum(int[] a, int n, int k)
    {
        // Create DP array
        // int dp[n,k+1];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < k + 1; j++)
                dp[i][j] = -1;

        int ans = (int)(-1e9);

        // Iterate and call recursive function
        // from every index to get the maximum subarray sum
        for (int i = 0; i < n; i++)
            ans = Math.max(ans,
                           findSubarraySum(i, 0, n, a, k));

        // corner case
        if (ans == 0 && k == 0)
            return Arrays.stream(a).max().getAsInt();

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = { -1, -2, -100, -10 };
        int n = a.length;
        int k = 1;

        System.out.println(findMaxSubarraySum(a, n, k));
    }
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

right = 3;
left = 6;

dp = np.ones((left, right))
dp = -1 * dp

# Function to find the maximum
# subarray sum with flips starting
# from index i
def findSubarraySum(ind, flips, n, a, k) :

    # If the number of flips
    # have exceeded
    if (flips > k) :
        return -1e9;

    # Complete traversal
    if (ind == n) :
        return 0;

    # If the state has previously
    # been visited
    if (dp[ind][flips] != -1) :
        return dp[ind][flips];

    # Initially
    ans = 0;

    # Use Kadane's algorithm and
    # call two states
    ans = max(0, a[ind] +
              findSubarraySum(ind + 1,
                              flips, n, a, k));
    ans = max(ans, -a[ind] +
              findSubarraySum(ind + 1, flips + 1,
                                       n, a, k));

    # Memoize the answer and return it
    dp[ind][flips] = ans;

    return dp[ind][flips] ;

# Utility function to call flips
# from index and return the answer
def findMaxSubarraySum(a, n, k) :

    ans = -1e9;

    # Iterate and call recursive
    # function from every index to
    # get the maximum subarray sum
    for i in range(n) :
        ans = max(ans, findSubarraySum(i, 0, n, a, k));

    # corner casae
    if ans == 0 and k == 0:
      return max(a);

    return ans;

# Driver Code
if __name__ == "__main__" :

    a = [-1, -2, -100, -10];
    n = len(a) ;
    k = 1;

    print(findMaxSubarraySum(a, n, k));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG {

    static int right = 2;
    static int left = 4;
    static int[, ] dp = new int[left + 1, right + 1];

    // Function to find the maximum subarray sum
    // with flips starting from index i
    static int findSubarraySum(int ind, int flips, int n,
                               int[] a, int k)
    {

        // If the number of flips have exceeded
        if (flips > k)
            return -(int)1e9;

        // Complete traversal
        if (ind == n)
            return 0;

        // If the state has previously been visited
        if (dp[ind, flips] != -1)
            return dp[ind, flips];

        // Initially
        int ans = 0;

        // Use Kadane's algorithm and call two states
        ans = Math.Max(0, a[ind]
                              + findSubarraySum(
                                  ind + 1, flips, n, a, k));
        ans = Math.Max(ans, -a[ind]
                                + findSubarraySum(ind + 1,
                                                  flips + 1,
                                                  n, a, k));

        // Memoize the answer and return it
        return dp[ind, flips] = ans;
    }

    // Utility function to call flips from
    // index and return the answer
    static int findMaxSubarraySum(int[] a, int n, int k)
    {
        // Create DP array
        // int dp[n][k+1];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < k + 1; j++)
                dp[i, j] = -1;

        int ans = -(int)1e9;

        // Iterate and call recursive function
        // from every index to get the maximum subarray sum
        for (int i = 0; i < n; i++)
            ans = Math.Max(ans,
                           findSubarraySum(i, 0, n, a, k));

        // corner case
        if (ans == 0 && k == 0)
            return a.Max();

        return ans;
    }

    // Driver Code
    static void Main()
    {
        int[] a = { -1, -2, -100, -10 };
        int n = a.Length;
        int k = 1;

        Console.WriteLine(findMaxSubarraySum(a, n, k));
    }
}

// This code is contributed by mits
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let right = 2;
    let left = 4;
    let dp = new Array(left);

    // Function to find the maximum subarray sum with flips
    // starting from index i
    function findSubarraySum(ind, flips, n, a, k)
    {

        // If the number of flips have exceeded
        if (flips > k)
            return (-1e9);

        // Complete traversal
        if (ind == n)
            return 0;

        // If the state has previously been visited
        if (dp[ind][flips] != -1)
            return dp[ind][flips];

        // Initially
        let ans = 0;

        // Use Kadane's algorithm and call two states
        ans = Math.max(0, a[ind]
                              + findSubarraySum(
                                  ind + 1, flips, n, a, k));
        ans = Math.max(ans, -a[ind]
                                + findSubarraySum(ind + 1,
                                                  flips + 1,
                                                  n, a, k));

        // Memoize the answer and return it
        return dp[ind][flips] = ans;
    }

    // Utility function to call flips from index and
    // return the answer
    function findMaxSubarraySum(a, n, k)
    {
        // Create DP array
        // int dp[n,k+1];
        for (let i = 0; i < n; i++)
        {
            dp[i] = new Array(k);
            for (let j = 0; j < k + 1; j++)
            {
                dp[i][j] = -1;
            }
        }

        let ans = (-1e9);

        // Iterate and call recursive function
        // from every index to get the maximum subarray sum
        for (let i = 0; i < n; i++)
            ans = Math.max(ans,
                           findSubarraySum(i, 0, n, a, k));

        // corner case
        if (ans == 0 && k == 0)
        {
            let max = Number.MIN_VALUE;
            for(let i = 0; i < a.length; i++)
            {
                max = Math.max(max, a[i]);
            }
            return max;
        }

        return ans;
    }

    let a = [ -1, -2, -100, -10 ];
    let n = a.length;
    let k = 1;

    document.write(findMaxSubarraySum(a, n, k));

</script>
```

**Output**

```
100
```

**时间复杂度:**O(N * K)
T3】辅助空间: O(N * K)