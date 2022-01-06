# 合并列表所有元素的最小成本

> 原文:[https://www . geesforgeks . org/最小成本合并所有列表元素/](https://www.geeksforgeeks.org/minimum-cost-to-merge-all-elements-of-list/)

给定一个 **N** 整数的列表，任务是将列表中的所有元素合并成一个具有最小可能成本的元素。合并规则如下:
选择列表中任意两个相邻元素，取值为 **X** 和 **Y** ，合并为单个元素，取值为 **(X + Y)** ，支付 **(X + Y)** 的总费用。
**举例:**

> **输入:** arr[] = {1，3，7}
> **输出:** 15
> 所有可能的合并方式:
> a) {1，3，7}(成本= 0) - > {4，7}(成本= 0+4 = 4) - > 11(成本= 4+11 = 15)
> b) {1，3，7}(成本= 0) - > {1，10}(成本= 0+10 = 0)

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。让我们首先定义 DP 的状态。 **DP[l][r]** 将是将子阵列 **arr[l…r]** 合并为一个的最小成本。
现在我们来看看递归关系:

> DP[l][r] = min(S(l，l) + S(l + 1，r) + DP[l][l] + DP[l + 1][r]，S(l，l + 1) + S(l + 2，r) + DP[l][l + 1] + DP[l + 2][r]，…，S(l，r–1)+S(r，r)+DP[l][r–1]+DP[r][r])= S(l，r) + min(DP[l][l]

该方法的时间复杂度为 **O(N <sup>3</sup> )** ，因为总共有 **N * N** 个状态，每个状态一般需要 **O(N)** 个时间来求解。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define N 401

// To store the states of DP
int dp[N][N];
bool v[N][N];

// Function to return the minimum merge cost
int minMergeCost(int i, int j, int* arr)
{

    // Base case
    if (i == j)
        return 0;

    // If the state has been solved before
    if (v[i][j])
        return dp[i][j];

    // Marking the state as solved
    v[i][j] = 1;
    int& x = dp[i][j];

    // Reference to dp[i][j]
    x = INT_MAX;

    // To store the sum of all the
    // elements in the subarray arr[i...j]
    int tot = 0;
    for (int k = i; k <= j; k++)
        tot += arr[k];

    // Loop to iterate the recurrence
    for (int k = i + 1; k <= j; k++) {
        x = min(x, tot + minMergeCost(i, k - 1, arr)
                       + minMergeCost(k, j, arr));
    }

    // Returning the solved value
    return x;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 7 };
    int n = sizeof(arr) / sizeof(int);

    cout << minMergeCost(0, n - 1, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static final int N = 401;

// To store the states of DP
static int [][]dp = new int[N][N];
static boolean [][]v = new boolean[N][N];

// Function to return the minimum merge cost
static int minMergeCost(int i, int j, int[] arr)
{

    // Base case
    if (i == j)
        return 0;

    // If the state has been solved before
    if (v[i][j])
        return dp[i][j];

    // Marking the state as solved
    v[i][j] = true;
    int x = dp[i][j];

    // Reference to dp[i][j]
    x = Integer.MAX_VALUE;

    // To store the sum of all the
    // elements in the subarray arr[i...j]
    int tot = 0;
    for (int k = i; k <= j; k++)
        tot += arr[k];

    // Loop to iterate the recurrence
    for (int k = i + 1; k <= j; k++)
    {
        x = Math.min(x, tot + minMergeCost(i, k - 1, arr)
                    + minMergeCost(k, j, arr));
    }

    // Returning the solved value
    return x;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 7 };
    int n = arr.length;

    System.out.print(minMergeCost(0, n - 1, arr));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

N = 401;

# To store the states of DP
dp = [[0 for i in range(N)] for j in range(N)];
v = [[False for i in range(N)] for j in range(N)];

# Function to return the minimum merge cost
def minMergeCost(i, j, arr):

    # Base case
    if (i == j):
        return 0;

    # If the state has been solved before
    if (v[i][j]):
        return dp[i][j];

    # Marking the state as solved
    v[i][j] = True;
    x = dp[i][j];

    # Reference to dp[i][j]
    x = sys.maxsize;

    # To store the sum of all the
    # elements in the subarray arr[i...j]
    tot = 0;
    for k in range(i, j + 1):
        tot += arr[k];

    # Loop to iterate the recurrence
    for k in range(i + 1, j + 1):
        x = min(x, tot + minMergeCost(i, k - 1, arr) + \
                minMergeCost(k, j, arr));

    # Returning the solved value
    return x;

# Driver code
if __name__ == '__main__':
    arr = [ 1, 3, 7 ];
    n = len(arr);

    print(minMergeCost(0, n - 1, arr));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static readonly int N = 401;

// To store the states of DP
static int [,]dp = new int[N, N];
static bool [,]v = new bool[N, N];

// Function to return the minimum merge cost
static int minMergeCost(int i, int j, int[] arr)
{

    // Base case
    if (i == j)
        return 0;

    // If the state has been solved before
    if (v[i, j])
        return dp[i, j];

    // Marking the state as solved
    v[i, j] = true;
    int x = dp[i, j];

    // Reference to dp[i,j]
    x = int.MaxValue;

    // To store the sum of all the
    // elements in the subarray arr[i...j]
    int tot = 0;
    for (int k = i; k <= j; k++)
        tot += arr[k];

    // Loop to iterate the recurrence
    for (int k = i + 1; k <= j; k++)
    {
        x = Math.Min(x, tot + minMergeCost(i, k - 1, arr)
                    + minMergeCost(k, j, arr));
    }

    // Returning the solved value
    return x;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 3, 7 };
    int n = arr.Length;

    Console.Write(minMergeCost(0, n - 1, arr));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var N = 401

// To store the states of DP
var dp = Array.from(Array(N), ()=> Array(N));
var v = Array.from(Array(N), ()=> Array(N));

// Function to return the minimum merge cost
function minMergeCost(i, j, arr)
{

    // Base case
    if (i == j)
        return 0;

    // If the state has been solved before
    if (v[i][j])
        return dp[i][j];

    // Marking the state as solved
    v[i][j] = 1;
    var x = dp[i][j];

    // Reference to dp[i][j]
    x = 1000000000;

    // To store the sum of all the
    // elements in the subarray arr[i...j]
    var tot = 0;
    for (var k = i; k <= j; k++)
        tot += arr[k];

    // Loop to iterate the recurrence
    for (var k = i + 1; k <= j; k++) {
        x = Math.min(x, tot + minMergeCost(i, k - 1, arr)
                       + minMergeCost(k, j, arr));
    }

    // Returning the solved value
    return x;
}

// Driver code
var arr = [1, 3, 7];
var n = arr.length;
document.write( minMergeCost(0, n - 1, arr));

</script>
```

**Output:** 

```
15
```