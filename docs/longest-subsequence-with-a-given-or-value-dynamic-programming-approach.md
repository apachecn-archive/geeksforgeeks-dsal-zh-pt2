# 给定或值的最长子序列:动态规划方法

> 原文:[https://www . geeksforgeeks . org/带有给定或值的最长子序列动态编程方法/](https://www.geeksforgeeks.org/longest-subsequence-with-a-given-or-value-dynamic-programming-approach/)

给定一个数组 **arr[]** ，任务是找到给定 OR 值 **M** 的最长子序列。如果没有这样的子序列，则打印 **0** 。

**示例:**

> **输入:** arr[] = {3，7，2，3}，M = 3
> **输出:** 3
> {3，2，3}是所需的子序列
> 3 | 2 | 3 = 3
> **输入:** arr[] = {2，2}，M = 3
> **输出:** 0

**方法:**一个简单的解决方案是生成所有可能的子序列，然后用所需的 OR 值找到其中最大的一个。然而，对于较小值的 **M** ，可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)方法。
我们先来看看递归关系。

> DP[I][curr _ or]= max(DP[I+1][curr _ or]，dp[i + 1][curr_or | arr[i]] + 1)

现在让我们了解一下 DP 的状态。这里， **dp[i][curr_or]** 存储子阵列 **arr[i…N-1]** 的最长子序列，这样当与该子序列进行“或”运算时， **curr_or** 给出 **M** 。每一步，选择索引 **i** 并更新**curr _ 或**或拒绝索引 **i** 并继续。

下面是上述方法的实现:

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
    int r = findLen(arr, i + 1, curr | arr[i], n, m);
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

    int ans = findLen(arr, 0, 0, n, m);
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
class GFG
{

static int maxN = 20;
static int maxM = 64;

// To store the states of DP
static int [][]dp = new int[maxN][maxM];
static boolean [][]v = new boolean[maxN][maxM];

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
    int r = findLen(arr, i + 1, curr | arr[i], n, m);
    dp[i][curr] = l;
    if (r != -1)
        dp[i][curr] = Math.max(dp[i][curr], r + 1);
    return dp[i][curr];
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 3, 7, 2, 3 };
    int n = arr.length;
    int m = 3;

    int ans = findLen(arr, 0, 0, n, m);
    if (ans == -1)
        System.out.println(0);
    else
        System.out.println(ans);
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
    r = findLen(arr, i + 1, curr | arr[i], n, m);
    dp[i][curr] = l;
    if (r != -1) :
        dp[i][curr] = max(dp[i][curr], r + 1);
    return dp[i][curr];

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 7, 2, 3 ];
    n = len(arr);
    m = 3;

    ans = findLen(arr, 0, 0, n, m);
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

static int maxN = 20;
static int maxM = 64;

// To store the states of DP
static int [,]dp = new int[maxN,maxM];
static bool [,]v = new bool[maxN,maxM];

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
    if (v[i,curr])
        return dp[i,curr];

    // Setting the state as solved
    v[i,curr] = true;

    // Recurrence relation
    int l = findLen(arr, i + 1, curr, n, m);
    int r = findLen(arr, i + 1, curr | arr[i], n, m);
    dp[i,curr] = l;
    if (r != -1)
        dp[i,curr] = Math.Max(dp[i,curr], r + 1);
    return dp[i,curr];
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 3, 7, 2, 3 };
    int n = arr.Length;
    int m = 3;

    int ans = findLen(arr, 0, 0, n, m);
    if (ans == -1)
        Console.WriteLine(0);
    else
        Console.WriteLine(ans);
}
}

// This code is contributed by PrinciRaj1992
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
    var r = findLen(arr, i + 1, curr | arr[i], n, m);
    dp[i][curr] = l;
    if (r != -1)
        dp[i][curr] = Math.max(dp[i][curr], r + 1);
    return dp[i][curr];
}

// Driver code
var arr = [3, 7, 2, 3];
var n = arr.length;
var m = 3;
var ans = findLen(arr, 0, 0, n, m);
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

**时间复杂度:** O(N * maxArr)，其中 maxArr 是数组中的最大元素。