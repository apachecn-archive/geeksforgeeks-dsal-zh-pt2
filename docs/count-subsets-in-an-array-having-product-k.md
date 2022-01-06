# 计数具有乘积 K 的数组中的子集

> 原文:[https://www . geesforgeks . org/count-数组中的子集-having-product-k/](https://www.geeksforgeeks.org/count-subsets-in-an-array-having-product-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是从给定数组中找出所有子集[的计数，其乘积等于 **K** 。](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)

**示例:**

> **输入:** arr[] = { 1，1，2，2，3 }，K = 4
> **输出:** 4
> **解释:**
> 积等于 K(= 4)的子集为:{ { arr[0]，arr[1]，arr[2]，arr[3] }，{ arr[0]，arr[2]，arr[3] }，{ arr[1]，arr[2]，arr[3] }。
> 因此，要求的输出为 4
> 
> **输入:** arr[] = { 1，1，2，2，3 }，K = 4
> T3】输出: 8

**方法:**问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)使用以下递归关系来解决:

> cntSub(idx，prod)= CNT sub(idx–1，prod * arr[I])+CNT sub(idx–1，prod)
> 
> **idx:** 存储数组元素的索引
> **prod:** 存储子集元素的乘积
> **cntSub(i，prod):** 存储乘积等于 **prod** 的子数组{ arr[i]，…，arr[N–1]}的子集计数。

按照以下步骤解决问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如 **dp[][]** ，来存储上述递归关系的重叠子问题。
*   利用上述递推关系，计算元素乘积等于 **K** 的子集数。
*   最后，打印**DP【N–1】【K】**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

#define M 1000

// Function to find the count of subsets
// whose product of elements is equal to K
int cntSub(int arr[], int idx,
           int prod, int K, int dp[][M])
{
    // Base Case
    if (idx < 0) {

        return (prod == K);
    }

    // If an already computed
    // subproblem occurred
    if (dp[idx][prod] != -1) {

        return dp[idx][prod];
    }

    // Count subsets including idx-th
    // element in the subset
    int X = cntSub(arr, idx - 1,
                   prod * arr[idx], K, dp);

    // Count subsets without including
    // idx-th element in the subset
    int Y = cntSub(arr, idx - 1,
                   prod, K, dp);

    return dp[idx][prod] = X + Y;
}

// Utility function to count subsets in
// an array whose product is equal to K
int UtilcntSub(int arr[], int N, int K)
{
    // dp[i][j]: Stores numberof subsets
    // with product j up to the i-th element
    int dp[N][M];

    // Initialize dp[][] to -1
    memset(dp, -1, sizeof(dp));

    cout << cntSub(arr, N - 1, 1, K, dp);
}

// Driver Code
int main()
{

    int arr[] = { 1, 1, 2, 2, 3, 4 };

    int K = 4;

    int N = sizeof(arr) / sizeof(arr[0]);

    UtilcntSub(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static int M = 1000;

// Function to find the count of subsets
// whose product of elements is equal to K
static int cntSub(int arr[], int idx,
                  int prod, int K, int dp[][])
{

    // Base Case
    if (idx < 0)
    {
        if (prod == K)
            return 1;
        else
            return 0;
    }

    // If an already computed
    // subproblem occurred
    if (dp[idx][prod] != -1)
    {
        return dp[idx][prod];
    }

    // Count subsets including idx-th
    // element in the subset
    int X = cntSub(arr, idx - 1,
                   prod * arr[idx], K, dp);

    // Count subsets without including
    // idx-th element in the subset
    int Y = cntSub(arr, idx - 1,
                   prod, K, dp);

    return dp[idx][prod] = X + Y;
}

// Utility function to count subsets in
// an array whose product is equal to K
static void UtilcntSub(int arr[], int N, int K)
{

    // dp[i][j]: Stores numberof subsets
    // with product j up to the i-th element
    int[][] dp = new int[N][M];

    // Initialize dp[][] to -1
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            dp[i][j] = -1;
        }
    }

    System.out.print(cntSub(arr, N - 1, 1, K, dp));
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 1, 1, 2, 2, 3, 4 };

    int K = 4;

    int N = arr.length;

    UtilcntSub(arr, N, K);
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python program to implement
# the above approach
M = 1000

# Function to find the count of subsets
# whose product of elements is equal to K
def cntSub(arr, idx, prod, K):
    global dp

    # Base Case
    if (idx < 0):
        return (prod == K)

    # If an already computed
    # subproblem occurred
    if (dp[idx][prod] != -1):
        return dp[idx][prod]

    # Count subsets including idx-th
    # element in the subset
    X = cntSub(arr, idx - 1, prod * arr[idx], K)

    # Count subsets without including
    # idx-th element in the subset
    Y = cntSub(arr, idx - 1, prod, K)
    dp[idx][prod] = X + Y
    return dp[idx][prod]

# Utility function to count subsets in
# an array whose product is equal to K
def UtilcntSub(arr, N, K):

    # dp[i][j]: Stores numberof subsets
    # with product j up to the i-th element
    print (cntSub(arr, N - 1, 1, K))

# Driver Code
if __name__ == '__main__':
    dp = [[-1 for i in range(1000)] for i in range(1000)]
    arr = [1, 1, 2, 2, 3, 4]
    K = 4
    N = len(arr)
    UtilcntSub(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;
class GFG
{

static int M = 1000;

// Function to find the count of subsets
// whose product of elements is equal to K
static int cntSub(int[] arr, int idx,
                  int prod, int K, int[,] dp)
{

    // Base Case
    if (idx < 0)
    {
        if (prod == K)
            return 1;
        else
            return 0;
    }

    // If an already computed
    // subproblem occurred
    if (dp[idx, prod] != -1)
    {
        return dp[idx, prod];
    }

    // Count subsets including idx-th
    // element in the subset
    int X = cntSub(arr, idx - 1,
                   prod * arr[idx], K, dp);

    // Count subsets without including
    // idx-th element in the subset
    int Y = cntSub(arr, idx - 1,
                   prod, K, dp);

    return dp[idx, prod] = X + Y;
}

// Utility function to count subsets in
// an array whose product is equal to K
static void UtilcntSub(int[] arr, int N, int K)
{

    // dp[i][j]: Stores numberof subsets
    // with product j up to the i-th element
    int[,] dp = new int[N, M];

    // Initialize dp[][] to -1
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            dp[i, j] = -1;
        }
    }

    Console.Write(cntSub(arr, N - 1, 1, K, dp));
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 1, 2, 2, 3, 4 };
    int K = 4; 
    int N = arr.Length; 
    UtilcntSub(arr, N, K);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

let M = 1000;

// Function to find the count of subsets
// whose product of elements is equal to K
function cntSub(arr, idx,
                  prod, K, dp)
{

    // Base Case
    if (idx < 0)
    {
        if (prod == K)
            return 1;
        else
            return 0;
    }

    // If an already computed
    // subproblem occurred
    if (dp[idx][prod] != -1)
    {
        return dp[idx][prod];
    }

    // Count subsets including idx-th
    // element in the subset
    let X = cntSub(arr, idx - 1,
                   prod * arr[idx], K, dp);

    // Count subsets without including
    // idx-th element in the subset
    let Y = cntSub(arr, idx - 1,
                   prod, K, dp);

    return dp[idx][prod] = X + Y;
}

// Utility function to count subsets in
// an array whose product is equal to K
function UtilcntSub(arr, N, K)
{

    // dp[i][j]: Stores numberof subsets
    // with product j up to the i-th element
    let dp = new Array(N);

    // Loop to create 2D array using 1D array
    for (var i = 0; i < dp.length; i++) {
        dp[i] = new Array(2);
    }

    // Initialize dp[][] to -1
    for(let i = 0; i < N; i++)
    {
        for(let j = 0; j < M; j++)
        {
            dp[i][j] = -1;
        }
    }

    document.write(cntSub(arr, N - 1, 1, K, dp));
}

// Driver code

        let arr = [ 1, 1, 2, 2, 3, 4 ];

    let K = 4;

    let N = arr.length;

    UtilcntSub(arr, N, K);

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N * K)*
T5**辅助空间:** O(N * K)