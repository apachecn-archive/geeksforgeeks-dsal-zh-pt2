# 最长的子序列，其和可被给定的数整除

> 原文:[https://www . geesforgeks . org/最长子序列-其和可被给定数字除尽/](https://www.geeksforgeeks.org/longest-subsequence-whose-sum-is-divisible-by-a-given-number/)

给定一个数组 **arr[]** 和一个整数 **M** ，任务是找到最长子序列的长度，其和可被 **M** 整除。如果没有这样的子序列，则打印 **0** 。
**举例:**

> **输入:** arr[] = {3，2，2，1}，M = 3
> **输出:** 3
> 最长的子序列，其和为
> 可被 3 整除，为{3，2，1}
> **输入:** arr[] = {2，2}，M = 3
> **输出:** 0

**方法:**解决这个问题的一个简单方法是生成所有可能的子序列，然后找到其中最大的可以被 **M** 整除的子序列。然而，对于较小值的 **M** ，可以使用基于[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)的方法。
我们先来看看递归关系。

> DP[I][curl _ mod]=最大值(DP[I+1][curl _ mod]，DP[I+1][(curl _ mod+arr[I])% m]+1)

现在让我们了解一下 DP 的状态。这里， **dp[i][curr_mod]** 存储子阵列 **arr[i…N-1]** 的最长子序列，使得该子序列和 **curr_mod** 的和可被 **M** 整除。每一步都可以选择索引 **i** 更新 **curr_mod** 或者忽略。
此外，请注意，只需要存储 **SUM % m** 而不是整个 SUM，因为该信息足以完成 DP 的状态。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define maxN 20
#define maxM 64

// To store the states of DP
int dp[maxN][maxM];
bool v[maxN][maxM];

// Function to return the length
// of the longest subsequence
// whose sum is divisible by m
int findLen(int* arr, int i, int curr,
            int n, int m)
{
    // Base case
    if (i == n) {
        if (!curr)
            return 0;
        else
            return -1;
    }

    // If the state has been solved before
    // return the value of the state
    if (v[i][curr])
        return dp[i][curr];

    // Setting the state as solved
    v[i][curr] = 1;

    // Recurrence relation
    int l = findLen(arr, i + 1, curr, n, m);
    int r = findLen(arr, i + 1,
                    (curr + arr[i]) % m, n, m);
    dp[i][curr] = l;
    if (r != -1)
        dp[i][curr] = max(dp[i][curr], r + 1);
    return dp[i][curr];
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 2, 1 };
    int n = sizeof(arr) / sizeof(int);
    int m = 3;

    cout << findLen(arr, 0, 0, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int maxN = 20;
static int maxM = 64;

// To store the states of DP
static int [][]dp = new int[maxN][maxM];
static boolean [][]v = new boolean[maxN][maxM];

// Function to return the length
// of the longest subsequence
// whose sum is divisible by m
static int findLen(int[] arr, int i,
                   int curr, int n, int m)
{
    // Base case
    if (i == n)
    {
        if (curr == 0)
            return 0;
        else
            return -1;
    }

    // If the state has been solved before
    // return the value of the state
    if (v[i][curr])
        return dp[i][curr];

    // Setting the state as solved
    v[i][curr] = true;

    // Recurrence relation
    int l = findLen(arr, i + 1, curr, n, m);
    int r = findLen(arr, i + 1,
                   (curr + arr[i]) % m, n, m);
    dp[i][curr] = l;
    if (r != -1)
        dp[i][curr] = Math.max(dp[i][curr], r + 1);
    return dp[i][curr];
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 3, 2, 2, 1 };
    int n = arr.length;
    int m = 3;

    System.out.println(findLen(arr, 0, 0, n, m));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

maxN = 20
maxM = 64

# To store the states of DP
dp = np.zeros((maxN, maxM));
v = np.zeros((maxN, maxM));

# Function to return the length
# of the longest subsequence
# whose sum is divisible by m
def findLen(arr, i, curr, n, m) :

    # Base case
    if (i == n) :
        if (not curr) :
            return 0;
        else :
            return -1;

    # If the state has been solved before
    # return the value of the state
    if (v[i][curr]) :
        return dp[i][curr];

    # Setting the state as solved
    v[i][curr] = 1;

    # Recurrence relation
    l = findLen(arr, i + 1, curr, n, m);
    r = findLen(arr, i + 1,
               (curr + arr[i]) % m, n, m);

    dp[i][curr] = l;
    if (r != -1) :
        dp[i][curr] = max(dp[i][curr], r + 1);

    return dp[i][curr];

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 2, 2, 1 ];
    n = len(arr);
    m = 3;

    print(findLen(arr, 0, 0, n, m));

# This code is contributed by AnkitRai
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int maxN = 20;
static int maxM = 64;

// To store the states of DP
static int [,]dp = new int[maxN, maxM];
static Boolean [,]v = new Boolean[maxN, maxM];

// Function to return the length
// of the longest subsequence
// whose sum is divisible by m
static int findLen(int[] arr, int i,
                   int curr, int n, int m)
{
    // Base case
    if (i == n)
    {
        if (curr == 0)
            return 0;
        else
            return -1;
    }

    // If the state has been solved before
    // return the value of the state
    if (v[i, curr])
        return dp[i, curr];

    // Setting the state as solved
    v[i, curr] = true;

    // Recurrence relation
    int l = findLen(arr, i + 1, curr, n, m);
    int r = findLen(arr, i + 1,
                   (curr + arr[i]) % m, n, m);
    dp[i, curr] = l;
    if (r != -1)
        dp[i, curr] = Math.Max(dp[i, curr], r + 1);
    return dp[i, curr];
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 3, 2, 2, 1 };
    int n = arr.Length;
    int m = 3;

    Console.WriteLine(findLen(arr, 0, 0, n, m));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var maxN = 20
var maxM = 64

// To store the states of DP
var dp = Array.from(Array(maxN), ()=> Array(maxM).fill(0));
var v = Array.from(Array(maxN), ()=> Array(maxM).fill(false));

// Function to return the length
// of the longest subsequence
// whose sum is divisible by m
function findLen(arr, i, curr, n, m)
{
    // Base case
    if (i == n) {
        if (!curr)
            return 0;
        else
            return -1;
    }

    // If the state has been solved before
    // return the value of the state
    if (v[i][curr])
        return dp[i][curr];

    // Setting the state as solved
    v[i][curr] = 1;

    // Recurrence relation
    var l = findLen(arr, i + 1, curr, n, m);
    var r = findLen(arr, i + 1, (curr + arr[i]) % m, n, m);
    dp[i][curr] = l;
    if (r != -1)
        dp[i][curr] = Math.max(dp[i][curr], r + 1);
    return dp[i][curr];
}

// Driver code
var arr = [3, 2, 2, 1];
var n = arr.length;
var m = 3;
document.write( findLen(arr, 0, 0, n, m));

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N * M)
T3】辅助空间 : O(N * M)。