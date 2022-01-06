# 给定“与”值的最长子序列

> 原文:[https://www . geesforgeks . org/带有给定值的最长子序列/](https://www.geeksforgeeks.org/longest-subsequence-with-a-given-and-value/)

给定一个数组 **arr[]** 和一个整数 **M** ，任务是找到给定 and 值的最长子序列 **M** 。如果没有这样的子序列，则打印 **0** 。
**举例:**

> **输入:** arr[] = {3，7，2，3}，M = 3
> **输出:**3
> AND 值为 3 的最长子序列为{3，7，3}。
> **输入:** arr[] = {2，2}，M = 3
> **输出:** 0

**方法:**解决这个问题的一个简单方法是生成所有可能的子序列，然后用所需的“与”值找到其中最大的一个。
但是，对于较小的 **M** 值，可以使用基于[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)的方法。
我们先来看看递归关系。

> DP[I][curr _ and]= max(DP[I+1][curr _ and]，dp[i + 1][curr_and & arr[i]] + 1)

现在让我们了解一下 DP 的状态。这里， **dp[i][curr_and]** 存储子阵列 **arr[i…N-1]** 的最长子序列，使得该子序列的**curr _ AND**&AND 等于 **M** 。在每一步中，可以选择索引 **i** 更新**curr _ 和**，也可以拒绝。
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

// Function to return the required length
int findLen(int* arr, int i, int curr,
            int n, int m)
{
    // Base case
    if (i == n) {
        if (curr == m)
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
    int r = findLen(arr, i + 1, curr & arr[i],
                    n, m);
    dp[i][curr] = l;
    if (r != -1)
        dp[i][curr] = max(dp[i][curr], r + 1);
    return dp[i][curr];
}

// Driver code
int main()
{
    int arr[] = { 3, 7, 2, 3 };
    int n = sizeof(arr) / sizeof(int);
    int m = 3;

    int ans = findLen(arr, 0, ((1 << 8) - 1),
                      n, m);
    if (ans == -1)
        cout << 0;
    else
        cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int maxN = 300;
static int maxM = 300;

// To store the states of DP
static int dp[][] = new int[maxN][maxM];
static boolean v[][] = new boolean[maxN][maxM];

// Function to return the required length
static int findLen(int[] arr, int i,
                   int curr, int n, int m)
{
    // Base case
    if (i == n)
    {
        if (curr == m)
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
    int r = findLen(arr, i + 1, curr & arr[i], n, m);
    dp[i][curr] = l;
    if (r != -1)
        dp[i][curr] = Math.max(dp[i][curr], r + 1);
    return dp[i][curr];
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 3, 7, 2, 3 };
    int n = arr.length;
    int m = 3;

    int ans = findLen(arr, 0, ((1 << 8) - 1), n, m);
    if (ans == -1)
        System.out.print( 0);
    else
        System.out.print( ans);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

maxN = 20
maxM = 256

# To store the states of DP
dp = np.zeros((maxN, maxM));
v = np.zeros((maxN, maxM));

# Function to return the required length
def findLen(arr, i, curr, n, m) :

    # Base case
    if (i == n) :
        if (curr == m) :
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
    r = findLen(arr, i + 1, curr & arr[i], n, m);

    dp[i][curr] = l;

    if (r != -1) :
        dp[i][curr] = max(dp[i][curr], r + 1);

    return dp[i][curr];

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 7, 2, 3 ];
    n = len(arr);
    m = 3;

    ans = findLen(arr, 0, ((1 << 8) - 1), n, m);

    if (ans == -1) :
        print(0);
    else :
        print(ans);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int maxN = 300;
static int maxM = 300;

// To store the states of DP
static int[,] dp = new int[maxN, maxM];
static bool[,] v = new bool[maxN, maxM];

// Function to return the required length
static int findLen(int[] arr, int i,
                   int curr, int n, int m)
{
    // Base case
    if (i == n)
    {
        if (curr == m)
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
    int r = findLen(arr, i + 1, curr & arr[i], n, m);
    dp[i, curr] = l;
    if (r != -1)
        dp[i, curr] = Math.Max(dp[i, curr], r + 1);
    return dp[i, curr];
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 3, 7, 2, 3 };
    int n = arr.Length;
    int m = 3;

    int ans = findLen(arr, 0, ((1 << 8) - 1), n, m);
    if (ans == -1)
        Console.WriteLine(0);
    else
        Console.WriteLine(ans);
}
}

// This code is contributed by
// sanjeev2552
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var maxN = 20
var maxM = 64

// To store the states of DP
var dp = Array.from(Array(maxN), ()=> Array(maxM));
var v = Array.from(Array(maxN), ()=> Array(maxM));

// Function to return the required length
function findLen(arr, i, curr, n, m)
{
    // Base case
    if (i == n) {
        if (curr == m)
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
    var r = findLen(arr, i + 1, curr & arr[i],
                    n, m);
    dp[i][curr] = l;
    if (r != -1)
        dp[i][curr] = Math.max(dp[i][curr], r + 1);
    return dp[i][curr];
}

// Driver code
var arr = [3, 7, 2, 3];
var n = arr.length;
var m = 3;
var ans = findLen(arr, 0, ((1 << 8) - 1),
                  n, m);
if (ans == -1)
    document.write( 0);
else
    document.write( ans);

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N * maxVal)，其中 maxVal 是给定数组的最大元素。