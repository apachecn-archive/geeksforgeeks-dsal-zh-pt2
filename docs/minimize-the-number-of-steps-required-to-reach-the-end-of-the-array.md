# 尽量减少到达阵列末端所需的步数

> 原文:[https://www . geesforgeks . org/最大限度地减少到达阵列末端所需的步骤数/](https://www.geeksforgeeks.org/minimize-the-number-of-steps-required-to-reach-the-end-of-the-array/)

给定一个由正整数组成的长度为 N 的整数数组 arr[]，任务是最小化达到索引“N-1”所需的步骤数。在给定的步骤中，如果我们在索引“I”处，我们可以转到索引“i-arr[i]”或“i+arr[i]”，因为我们以前没有访问过这些索引。此外，我们不能超出数组的界限。如果没有可能，打印-1。
**例:**

```
Input : arr[] = {1, 1, 1}
Output : 2
The path will be 0 -> 1 -> 2.
Step 1 - 0 to 1
Step 2 - 1 to 2

Input : {2, 1}
Output : -1
```

这个问题可以用动态规划方法解决。
让我们讨论一个在开始时看起来似乎是正确的方法。让我们假设我们处在第一个 T4 指数。我们能直接说 **dp[i] = 1 + min( dp[i-arr[i]]，dp[i+arr[i]] )** 吗？不，我们不能。我们到达索引“I”的路径也很重要，因为我们以前使用的索引将不再可用。
因此，我们唯一剩下的方法是尝试所有可能的组合，这些组合可能非常大。在本文中，我们将使用位屏蔽方法将复杂度降低到指数级。我们的掩码将是具有以下特征的整数值。

```
1) If, a index 'i' is visited, ith bit 
   will be set 1 in the mask. 
2) Else that bit will be set 0.
```

所需的重复关系将是。

```
dp[i][mask] = 1 + min(dp[i+arr[i]][mask|(1<<i)], 
                      dp[i-arr[i]][mask|(1<<i)])
```

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
#define maxLen 10
#define maskLen 130
using namespace std;

// variable to store states of dp
int dp[maxLen][maskLen];

// variable to check if a given state
// has been solved
bool v[maxLen][maskLen];

// Function to find the minimum number of steps
// required to reach the end of the array
int minSteps(int arr[], int i, int mask, int n)
{
    // base case
    if (i == n - 1)
        return 0;

    if (i > n - 1 || i < 0)
        return 9999999;
    if ((mask >> i) & 1)
        return 9999999;

    // to check if a state has
    // been solved
    if (v[i][mask])
        return dp[i][mask];
    v[i][mask] = 1;

    // required recurrence relation
    dp[i][mask] = 1 + min(minSteps(arr, i - arr[i], (mask | (1 << i)), n),
                          minSteps(arr, i + arr[i], (mask | (1 << i)), n));

    // returning the value
    return dp[i][mask];
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2, 2, 1, 1 };

    int n = sizeof(arr) / sizeof(int);

    int ans = minSteps(arr, 0, 0, n);
    if (ans >= 9999999)
        cout << -1;
    else
        cout << ans;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{

    static int maxLen = 10;
    static int maskLen = 130;

    // variable to store states of dp
    static int[][] dp = new int[maxLen][maskLen];

    // variable to check if a given state
    // has been solved
    static boolean[][] v = new boolean[maxLen][maskLen];

    // Function to find the minimum number of steps
    // required to reach the end of the array
    static int minSteps(int arr[], int i, int mask, int n)
    {
        // base case
        if (i == n - 1)
        {
            return 0;
        }

        if (i > n - 1 || i < 0)
        {
            return 9999999;
        }
        if ((mask >> i) % 2 == 1)
        {
            return 9999999;
        }

        // to check if a state has
        // been solved
        if (v[i][mask])
        {
            return dp[i][mask];
        }
        v[i][mask] = true;

        // required recurrence relation
        dp[i][mask] = 1 + Math.min(minSteps(arr, i - arr[i], (mask | (1 << i)), n),
                                minSteps(arr, i + arr[i], (mask | (1 << i)), n));

        // returning the value
        return dp[i][mask];
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 2, 2, 1, 1};

        int n = arr.length;

        int ans = minSteps(arr, 0, 0, n);
        if (ans >= 9999999)
        {
            System.out.println(-1);
        }
        else
        {
            System.out.println(ans);
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 计算机编程语言

```
# Python3 implementation of the above approach
maxLen = 10
maskLen = 130

# variable to store states of dp
dp = [[ 0 for i in range(maskLen)] for i in range(maxLen)]

# variable to check if a given state
# has been solved
v = [[False for i in range(maskLen)] for i in range(maxLen)]

# Function to find the minimum number of steps
# required to reach the end of the array
def minSteps(arr, i, mask, n):

    # base case
    if (i == n - 1):
        return 0

    if (i > n - 1 or i < 0):
        return 9999999

    if ((mask >> i) & 1):
        return 9999999

    # to check if a state has
    # been solved
    if (v[i][mask] == True):
        return dp[i][mask]
    v[i][mask] = True

    # required recurrence relation
    dp[i][mask] = 1 + min(minSteps(arr, i - arr[i], (mask | (1 << i)), n),
                        minSteps(arr, i + arr[i], (mask | (1 << i)), n))

    # returning the value
    return dp[i][mask]

# Driver code

arr=[1, 2, 2, 2, 1, 1]

n = len(arr)

ans = minSteps(arr, 0, 0, n)

if (ans >= 9999999):
    print(-1)
else:
    print(ans)

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    static int maxLen = 10;
    static int maskLen = 130;

    // variable to store states of dp
    static int[,] dp = new int[maxLen, maskLen];

    // variable to check if a given state
    // has been solved
    static bool[,] v = new bool[maxLen, maskLen];

    // Function to find the minimum number of steps
    // required to reach the end of the array
    static int minSteps(int []arr, int i, int mask, int n)
    {
        // base case
        if (i == n - 1)
        {
            return 0;
        }

        if (i > n - 1 || i < 0)
        {
            return 9999999;
        }
        if ((mask >> i) % 2 == 1)
        {
            return 9999999;
        }

        // to check if a state has
        // been solved
        if (v[i, mask])
        {
            return dp[i, mask];
        }
        v[i, mask] = true;

        // required recurrence relation
        dp[i,mask] = 1 + Math.Min(minSteps(arr, i - arr[i], (mask | (1 << i)), n),
                                minSteps(arr, i + arr[i], (mask | (1 << i)), n));

        // returning the value
        return dp[i,mask];
    }

    // Driver code
    static public void Main ()
    {
        int []arr = {1, 2, 2, 2, 1, 1};

        int n = arr.Length;

        int ans = minSteps(arr, 0, 0, n);
        if (ans >= 9999999)
        {
            Console.WriteLine(-1);
        }
        else
        {
            Console.WriteLine(ans);
        }
    }
}

/* This code contributed by ajit. */
```

## java 描述语言

```
<script>

    // Javascript implementation of
    // the above approach

    let maxLen = 10;
    let maskLen = 130;

    // variable to store states of dp
    let dp = new Array(maxLen);
    for(let i = 0; i < maxLen; i++)
    {
        dp[i] = new Array(maskLen);
    }

    // variable to check if a given state
    // has been solved
    let v = new Array(maxLen);
    for(let i = 0; i < maxLen; i++)
    {
        v[i] = new Array(maskLen);
    }

    // Function to find the minimum number of steps
    // required to reach the end of the array
    function minSteps(arr, i, mask, n)
    {
        // base case
        if (i == n - 1)
        {
            return 0;
        }

        if (i > n - 1 || i < 0)
        {
            return 9999999;
        }
        if ((mask >> i) % 2 == 1)
        {
            return 9999999;
        }

        // to check if a state has
        // been solved
        if (v[i][mask])
        {
            return dp[i][mask];
        }
        v[i][mask] = true;

        // required recurrence relation
        dp[i][mask] = 1 + Math.min(minSteps(arr, i - arr[i],
        (mask | (1 << i)), n), minSteps(arr, i + arr[i],
        (mask | (1 << i)), n));

        // returning the value
        return dp[i][mask];
    }

    let arr = [1, 2, 2, 2, 1, 1];

    let n = arr.length;

    let ans = minSteps(arr, 0, 0, n);
    if (ans >= 9999999)
    {
      document.write(-1);
    }
    else
    {
      document.write(ans);
    }

</script>
```

**Output:** 

```
3
```

**时间复杂度** : O(N*(2 <sup>N</sup> )

**辅助空间:** O(maxLen + maskLen)