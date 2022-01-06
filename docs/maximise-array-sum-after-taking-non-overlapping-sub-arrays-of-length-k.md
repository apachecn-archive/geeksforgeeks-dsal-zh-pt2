# 取长度为 K 的非重叠子阵列后最大化阵列和

> 原文:[https://www . geesforgeks . org/maximum-数组-取后求和-非重叠-长度为 k 的子数组/](https://www.geeksforgeeks.org/maximise-array-sum-after-taking-non-overlapping-sub-arrays-of-length-k/)

给定长度为 **N** 的整数数组**arr【】**和整数 **K** ，任务是选择一些不重叠的子数组，使得每个子数组的长度正好为 **K** ，没有两个子数组相邻，并且所选子数组的所有元素之和最大。
**举例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 2
> **输出:** 12
> 最大化和的子数组将是{{1，2}，{4，5}}。
> 这样，答案将是 12。
> **输入:** arr[] = {1，1，1，1，1}，K = 1
> **输出:** 3

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。让我们假设我们在一个指数 **i** 。假设 **dp[i]** 被定义为满足上述条件的子阵列 **arr[i…n-1]** 的所有可能子集的元素的最大和。
我们将有两种可能的选择，即选择子阵列 **arr[i…i+k-1]** 并求解 **dp[i + k + 1]** 或拒绝它并求解 **dp[i + 1]** 。
因此，递归关系为

> dp[i] = max（dp[i + 1]， scar[i] + scar[i + 1] + scar[i + 2] + + scar[i + k – 1] + dp[i + k + 1]）

由于 **K** 的值可以很大，我们将使用前缀和数组来寻找子数组**arr[I…I+K–1]**中 O(1)的所有元素的和。
总的来说，算法的时间复杂度将是 **O(N)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define maxLen 10
using namespace std;

// To store the states of dp
int dp[maxLen];

// To check if a given state
// has been solved
bool v[maxLen];

// To store the prefix-sum
int prefix_sum[maxLen];

// Function to fill the prefix_sum[] with
// the prefix sum of the given array
void findPrefixSum(int arr[], int n)
{
    prefix_sum[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefix_sum[i] = arr[i] + prefix_sum[i - 1];
}

// Function to find the maximum sum subsequence
// such that no two elements are adjacent
int maxSum(int arr[], int i, int n, int k)
{
    // Base case
    if (i + k > n)
        return 0;

    // To check if a state has
    // been solved
    if (v[i])
        return dp[i];
    v[i] = 1;

    int x;

    if (i == 0)
        x = prefix_sum[k - 1];
    else
        x = prefix_sum[i + k - 1] - prefix_sum[i - 1];

    // Required recurrence relation
    dp[i] = max(maxSum(arr, i + 1, n, k),
                x + maxSum(arr, i + k + 1, n, k));

    // Returning the value
    return dp[i];
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 7, 6 };
    int n = sizeof(arr) / sizeof(int);
    int k = 1;

    // Finding prefix-sum
    findPrefixSum(arr, n);

    // Finding the maximum possible sum
    cout << maxSum(arr, 0, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    static int maxLen = 10;

    // To store the states of dp
    static int[] dp = new int[maxLen];

    // To check if a given state
    // has been solved
    static boolean[] v = new boolean[maxLen];

    // To store the prefix-sum
    static int[] prefix_sum = new int[maxLen];

    // Function to fill the prefix_sum[] with
    // the prefix sum of the given array
    static void findPrefixSum(int arr[], int n)
    {
        prefix_sum[0] = arr[0];
        for (int i = 1; i < n; i++)
        {
            prefix_sum[i] = arr[i] + prefix_sum[i - 1];
        }
    }

    // Function to find the maximum sum subsequence
    // such that no two elements are adjacent
    static int maxSum(int arr[], int i, int n, int k)
    {
        // Base case
        if (i + k > n)
        {
            return 0;
        }

        // To check if a state has
        // been solved
        if (v[i])
        {
            return dp[i];
        }
        v[i] = true;

        int x;

        if (i == 0)
        {
            x = prefix_sum[k - 1];
        }
        else
        {
            x = prefix_sum[i + k - 1] - prefix_sum[i - 1];
        }

        // Required recurrence relation
        dp[i] = Math.max(maxSum(arr, i + 1, n, k),
                x + maxSum(arr, i + k + 1, n, k));

        // Returning the value
        return dp[i];
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 3, 7, 6};
        int n = arr.length;
        int k = 1;

        // Finding prefix-sum
        findPrefixSum(arr, n);

        // Finding the maximum possible sum
        System.out.println(maxSum(arr, 0, n, k));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

maxLen = 10

# To store the states of dp
dp = [0]*maxLen;

# To check if a given state
# has been solved
v = [0]*maxLen;

# To store the prefix-sum
prefix_sum = [0]*maxLen;

# Function to fill the prefix_sum[] with
# the prefix sum of the given array
def findPrefixSum(arr, n) :

    prefix_sum[0] = arr[0];
    for i in range(n) :
        prefix_sum[i] = arr[i] + prefix_sum[i - 1];

# Function to find the maximum sum subsequence
# such that no two elements are adjacent
def maxSum(arr, i, n, k) :

    # Base case
    if (i + k > n) :
        return 0;

    # To check if a state has
    # been solved
    if (v[i]) :
        return dp[i];

    v[i] = 1;

    if (i == 0) :
        x = prefix_sum[k - 1];
    else :
        x = prefix_sum[i + k - 1] - prefix_sum[i - 1];

    # Required recurrence relation
    dp[i] = max(maxSum(arr, i + 1, n, k),
                x + maxSum(arr, i + k + 1, n, k));

    # Returning the value
    return dp[i];

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 3, 7, 6 ];

    n = len(arr);
    k = 1;

    # Finding prefix-sum
    findPrefixSum(arr, n);

    # Finding the maximum possible sum
    print(maxSum(arr, 0, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int maxLen = 10;

    // To store the states of dp
    static int[] dp = new int[maxLen];

    // To check if a given state
    // has been solved
    static bool[] v = new bool[maxLen];

    // To store the prefix-sum
    static int[] prefix_sum = new int[maxLen];

    // Function to fill the prefix_sum[] with
    // the prefix sum of the given array
    static void findPrefixSum(int []arr, int n)
    {
        prefix_sum[0] = arr[0];
        for (int i = 1; i < n; i++)
        {
            prefix_sum[i] = arr[i] + prefix_sum[i - 1];
        }
    }

    // Function to find the maximum sum subsequence
    // such that no two elements are adjacent
    static int maxSum(int []arr, int i, int n, int k)
    {
        // Base case
        if (i + k > n)
        {
            return 0;
        }

        // To check if a state has
        // been solved
        if (v[i])
        {
            return dp[i];
        }
        v[i] = true;

        int x;

        if (i == 0)
        {
            x = prefix_sum[k - 1];
        }
        else
        {
            x = prefix_sum[i + k - 1] - prefix_sum[i - 1];
        }

        // Required recurrence relation
        dp[i] = Math.Max(maxSum(arr, i + 1, n, k),
                x + maxSum(arr, i + k + 1, n, k));

        // Returning the value
        return dp[i];
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {1, 3, 7, 6};
        int n = arr.Length;
        int k = 1;

        // Finding prefix-sum
        findPrefixSum(arr, n);

        // Finding the maximum possible sum
        Console.Write(maxSum(arr, 0, n, k));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var maxLen = 10

// To store the states of dp
var dp = Array(maxLen);

// To check if a given state
// has been solved
var v = Array(maxLen);

// To store the prefix-sum
var prefix_sum = Array(maxLen);;

// Function to fill the prefix_sum[] with
// the prefix sum of the given array
function findPrefixSum(arr, n)
{
    prefix_sum[0] = arr[0];
    for (var i = 1; i < n; i++)
        prefix_sum[i] = arr[i] + prefix_sum[i - 1];
}

// Function to find the maximum sum subsequence
// such that no two elements are adjacent
function maxSum(arr, i, n, k)
{
    // Base case
    if (i + k > n)
        return 0;

    // To check if a state has
    // been solved
    if (v[i])
        return dp[i];
    v[i] = 1;

    var x;

    if (i == 0)
        x = prefix_sum[k - 1];
    else
        x = prefix_sum[i + k - 1] - prefix_sum[i - 1];

    // Required recurrence relation
    dp[i] = Math.max(maxSum(arr, i + 1, n, k),
                x + maxSum(arr, i + k + 1, n, k));

    // Returning the value
    return dp[i];
}

// Driver code
var arr = [1, 3, 7, 6];
var n = arr.length;
var k = 1;
// Finding prefix-sum
findPrefixSum(arr, n);
// Finding the maximum possible sum
document.write( maxSum(arr, 0, n, k));

</script>
```

**Output:** 

```
9
```