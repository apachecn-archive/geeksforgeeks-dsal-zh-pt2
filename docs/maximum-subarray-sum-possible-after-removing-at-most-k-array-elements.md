# 移除最多 K 个阵列元素后可能的最大子阵列和

> 原文:[https://www . geeksforgeeks . org/max-subarray-最多移除 k 个数组元素后的可能总和/](https://www.geeksforgeeks.org/maximum-subarray-sum-possible-after-removing-at-most-k-array-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是通过从数组中最多移除 **K** 元素来找到最大[子数组和](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。

**示例:**

> **输入:** arr[] = { -2，1，3，-2，4，-7，20 }，K = 1
> **输出:** 26
> **解释:**
> 从数组中移除 arr[5]会将 arr[]修改为{ -2，1，3，-2，4，20 }
> 最大和为{ 1，3，-2，4，20 }。
> 因此，所需输出为 26。
> 
> **输入:** arr[] = { -1，1，-1，-1，1}，K=2
> **输出:** 3
> **解释:**
> 从数组中移除 arr[2]和 arr[3]将 arr[]修改为{–1，1，1，1}
> 最大和为{ 1，1，1 }。
> 因此，要求输出为 3。

**方法:**使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。这个想法是使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)的概念。按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个数组元素，需要执行以下两个操作:
    *   从子阵列中移除当前阵列元素。
    *   在子阵列中包括当前阵列元素。
*   因此，解决这个问题的递推关系如下:

> mxsubum(I，j)= max(0，arr[I]+mxsubum(I–1，j))、mxsubum(I–1，j–1))
> 
> **i:** 存储数组元素的索引
> **j:** 可从子数组
> **中移除的元素的最大数量 mxSubSum(i，j):** 通过移除 K–j 数组元素，返回子数组{ arr[i]，arr[N–1]}中的最大子数组和。

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如 **dp[][]** ，来存储上述递归关系的重叠子问题。
*   使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)填充 **dp[][]** 数组。
*   从 dp[][]数组中找到[最大元素，说 **res** 。](https://www.geeksforgeeks.org/program-to-find-the-maximum-element-in-a-matrix/)
*   初始化一个变量，比如 **Max** ，来存储数组**arr【】**中的[最大元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   如果所有数组元素都是负的，那么更新 **res = max(res，Max)** 。
*   最后，打印 **res** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;
#define M 100

// Function to find the maximum subarray
// sum greater than or equal to 0 by
// removing K array elements
int mxSubSum(int i, int* arr,
             int j, int dp[][M])
{
    // Base case
    if (i == 0) {
        return dp[i][j] = max(0, arr[i]);
    }

    // If overlapping subproblems
    // already occurred
    if (dp[i][j] != -1) {
        return dp[i][j];
    }

    // Include current element in the subarray
    int X = max(0, arr[i]
                       + mxSubSum(i - 1, arr, j, dp));

    // If K elements already removed
    // from the subarray
    if (j == 0) {

        return dp[i][j] = X;
    }

    // Remove current element from the subarray
    int Y = mxSubSum(i - 1, arr, j - 1, dp);

    return dp[i][j] = max(X, Y);
}

// Utility function to find the maximum subarray
// sum by removing at most K array elements
int MaximumSubarraySum(int n, int* arr, int k)
{

    // Stores overlapping subproblems
    // of the recurrence relation
    int dp[M][M];

    // Initialize dp[][] to -1
    memset(dp, -1, sizeof(dp));

    mxSubSum(n - 1, arr, k, dp);

    // Stores maximum subarray sum by
    // removing at most K elements
    int res = 0;

    // Calculate maximum element
    // in dp[][]
    for (int i = 0; i < n; i++) {
        for (int j = 0; j <= k; j++) {

            // Update res
            res = max(res, dp[i][j]);
        }
    }

    // If all array elements are negative
    if (*max_element(arr, arr + n) < 0) {

        // Update res
        res = *max_element(arr, arr + n);
    }
    return res;
}

// Driver Code
int main()
{
    int arr[] = { -2, 1, 3, -2, 4, -7, 20 };
    int K = 1;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << MaximumSubarraySum(N, arr, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{
static final int M = 100;

// Function to find the maximum subarray
// sum greater than or equal to 0 by
// removing K array elements
static int mxSubSum(int i, int []arr,
             int j, int dp[][])
{
    // Base case
    if (i == 0) {
        return dp[i][j] = Math.max(0, arr[i]);
    }

    // If overlapping subproblems
    // already occurred
    if (dp[i][j] != -1) {
        return dp[i][j];
    }

    // Include current element in the subarray
    int X = Math.max(0, arr[i]
                       + mxSubSum(i - 1, arr, j, dp));

    // If K elements already removed
    // from the subarray
    if (j == 0)
    {
        return dp[i][j] = X;
    }

    // Remove current element from the subarray
    int Y = mxSubSum(i - 1, arr, j - 1, dp);

    return dp[i][j] = Math.max(X, Y);
}

// Utility function to find the maximum subarray
// sum by removing at most K array elements
static int MaximumSubarraySum(int n, int []arr, int k)
{

    // Stores overlapping subproblems
    // of the recurrence relation
    int [][]dp = new int[M][M];

    // Initialize dp[][] to -1
    for (int i = 0; i < M; i++)
        for (int j = 0; j < M; j++)
            dp[i][j] = -1;

    mxSubSum(n - 1, arr, k, dp);

    // Stores maximum subarray sum by
    // removing at most K elements
    int res = 0;

    // Calculate maximum element
    // in dp[][]
    for (int i = 0; i < n; i++) {
        for (int j = 0; j <= k; j++) {

            // Update res
            res = Math.max(res, dp[i][j]);
        }
    }

    // If all array elements are negative
    if (Arrays.stream(arr).max().getAsInt() < 0) {

        // Update res
        res = Arrays.stream(arr).max().getAsInt();
    }
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { -2, 1, 3, -2, 4, -7, 20 };
    int K = 1;
    int N = arr.length;
    System.out.print(MaximumSubarraySum(N, arr, K) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
M = 100

# Function to find the maximum subarray
# sum greater than or equal to 0 by
# removing K array elements
def mxSubSum(i, arr, j):
    global dp

    # Base case
    if (i == 0):
        dp[i][j] = max(0, arr[i])
        return dp[i][j]

    # If overlapping subproblems
    # already occurred
    if (dp[i][j] != -1):
        return dp[i][j]

    # Include current element in the subarray
    X = max(0, arr[i] + mxSubSum(i - 1, arr, j))

    # If K elements already removed
    # from the subarray
    if (j == 0):

        dp[i][j] = X
        return X

    # Remove current element from the subarray
    Y = mxSubSum(i - 1, arr, j - 1)

    dp[i][j] = max(X, Y)

    return dp[i][j]

# Utility function to find the maximum subarray
# sum by removing at most K array elements
# Utility function to find the maximum subarray
# sum by removing at most K array elements
def MaximumSubarraySum(n, arr, k):

    mxSubSum(n - 1, arr, k)

    # Stores maximum subarray sum by
    # removing at most K elements
    res = 0

    # Calculate maximum element
    # in dp[][]
    for i in range(n):
        for j in range(k + 1):

            # Update res
            res = max(res, dp[i][j])

    # If all array elements are negative
    if (max(arr) < 0):

        # Update res
        res = max(arr)
    return res

# Driver Code
if __name__ == '__main__':
    dp = [[-1 for i in range(100)] for i in range(100)]
    arr = [-2, 1, 3, -2, 4, -7, 20]
    K = 1
    N = len(arr)
    print(MaximumSubarraySum(N, arr, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;

class GFG{

static int M = 100;

// Function to find the maximum subarray
// sum greater than or equal to 0 by
// removing K array elements
static int mxSubSum(int i, int []arr,
                    int j, int [,]dp)
{

    // Base case
    if (i == 0)
    {
        return dp[i, j] = Math.Max(0, arr[i]);
    }

    // If overlapping subproblems
    // already occurred
    if (dp[i, j] != -1)
    {
        return dp[i, j];
    }

    // Include current element in the subarray
    int X = Math.Max(0, arr[i] +
                    mxSubSum(i - 1, arr, j, dp));

    // If K elements already removed
    // from the subarray
    if (j == 0)
    {
        return dp[i, j] = X;
    }

    // Remove current element from the subarray
    int Y = mxSubSum(i - 1, arr, j - 1, dp);

    return dp[i, j] = Math.Max(X, Y);
}

// Utility function to find the maximum subarray
// sum by removing at most K array elements
static int MaximumSubarraySum(int n, int []arr, int k)
{

    // Stores overlapping subproblems
    // of the recurrence relation
    int [,]dp = new int[M, M];

    // Initialize dp[,] to -1
    for(int i = 0; i < M; i++)
        for(int j = 0; j < M; j++)
            dp[i, j] = -1;

    mxSubSum(n - 1, arr, k, dp);

    // Stores maximum subarray sum by
    // removing at most K elements
    int res = 0;

    // Calculate maximum element
    // in dp[,]
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j <= k; j++)
        {

            // Update res
            res = Math.Max(res, dp[i, j]);
        }
    }

    Array.Sort(arr);

    // If all array elements are negative

    if (arr[n - 1] < 0)
    {

        // Update res
        res = arr[n - 1];
    }
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { -2, 1, 3, -2, 4, -7, 20 };
    int K = 1;
    int N = arr.Length;

    Console.WriteLine(MaximumSubarraySum(N, arr, K));
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach
var M = 100;

// Function to find the maximum subarray
// sum greater than or equal to 0 by
// removing K array elements
function mxSubSum(i, arr, j, dp)
{

    // Base case
    if (i == 0)
    {
        dp[i][j] = Math.max(0, arr[i]);
        return dp[i][j];
    }

    // If overlapping subproblems
    // already occurred
    if (dp[i][j] != -1)
    {
        return dp[i][j];
    }

    // Include current element in the subarray
    var X = Math.max(
        0, arr[i] + mxSubSum(i - 1, arr, j, dp));

    // If K elements already removed
    // from the subarray
    if (j == 0)
    {
        dp[i][j] = X;
        return dp[i][j]
    }

    // Remove current element from the subarray
    var Y = mxSubSum(i - 1, arr, j - 1, dp);

    dp[i][j] = Math.max(X, Y);
    return dp[i][j]
}

// Utility function to find the maximum subarray
// sum by removing at most K array elements
function MaximumSubarraySum(n, arr, k)
{

    // Stores overlapping subproblems
    // of the recurrence relation
    var dp = Array.from(Array(M), () => Array(M).fill(-1));

    mxSubSum(n - 1, arr, k, dp);

    // Stores maximum subarray sum by
    // removing at most K elements
    var res = 0;

    // Calculate maximum element
    // in dp[][]
    for(var i = 0; i < n; i++)
    {
        for(var j = 0; j <= k; j++)
        {

            // Update res
            res = Math.max(res, dp[i][j]);
        }
    }

    // If all array elements are negative
    if (arr.reduce((a, b) => Math.max(a, b)) < 0)
    {

        // Update res
        res = arr.reduce((a, b) => Math.max(a, b));
    }
    return res;
}

// Driver Code
var arr = [ -2, 1, 3, -2, 4, -7, 20 ];
var K = 1;
var N = arr.length;

document.write( MaximumSubarraySum(N, arr, K));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
26
```

***时间复杂度:**O(N * K)*
T5**辅助空间:** O(N * K)