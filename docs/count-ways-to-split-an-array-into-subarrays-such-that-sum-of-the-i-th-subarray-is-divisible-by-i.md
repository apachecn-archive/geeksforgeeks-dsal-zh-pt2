# 计算将一个阵列分割成子阵列的方法，使得第 I 个子阵列的总和可被 I 整除

> 原文:[https://www . geesforgeks . org/count-way-将数组拆分为子数组-这样第 I 个子数组的和就可以被 I 整除/](https://www.geeksforgeeks.org/count-ways-to-split-an-array-into-subarrays-such-that-sum-of-the-i-th-subarray-is-divisible-by-i/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出将数组拆分为非空[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的方法，使得 **i <sup>th</sup>** 子数组的和可以被 **i** 整除。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 3
> **解释:**
> 以下是将阵列拆分为非空子阵列的几种方法，如下所示:
> 
> 1.  将阵列分成{1}、{2}、{3}、{4}个子阵列，每个子阵列的总和可被 I 整除。
> 2.  将阵列分成{1，2，3}，{4}个子阵列，每个子阵列都可以被 I 整除。
> 3.  将阵列分成{1，2，3，4}个子阵列，每个子阵列都可以被 I 整除。
> 
> 因为只有 3 种可能的方法来分割给定的数组。因此，打印 3。
> 
> **输入:** arr[ ] = {1，1，1，1，1}
> **输出:** 3

**逼近:**给定的问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)求解，因为它有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构。](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)子问题可以使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)存储在 **dp[][]表**中，其中 **dp[i][j]** 将直到**的分区数与 **arr[]** 的**索引一起存储到 **j** 非空子数组中。这个想法可以使用[前缀 Sum](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) [数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**pre【】**来实现，该数组存储所有元素的[和](https://www.geeksforgeeks.org/sum-function-python/),直到每隔**I<sup>th</sup>T31】索引和 **dp[i][j]** 可以被计算为**DP[k][j–1]**对于 **k < i** 的所有值的和按照以下步骤解决给定的问题:**

*   初始化一个变量，比如**计数**，它存储给定阵列可能分裂为子阵列的次数。
*   [求数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的前缀和，存入另一个数组，比如**前缀[]** 。
*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如说 **dp[][]** ，存储所有重叠状态 **dp[i][j]** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，使用变量 **j** 嵌套迭代范围**【N，0】**，并执行以下步骤:
    1.  将 **dp[j + 1][pre[i + 1] % (j + 1)]** 的值增加 **dp[j][pre[i + 1] % j]** 的值，因为这表示直到索引 **i** 为可被 **(j + 1)** 整除的 **j** 连续子序列的分区数。
    2.  如果 **i** 的值为**(N–1)**，则通过 **dp[j][pre[i + 1] % j]** 更新**计数**的值。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count ways to split
// an array into subarrays such that
// sum of the i-th subarray is
// divisible by i
int countOfWays(int arr[], int N)
{

    // Stores the prefix sum of array
    int pre[N + 1] = { 0 };
    for (int i = 0; i < N; i++) {

        // Find the prefix sum
        pre[i + 1] = pre[i] + arr[i];
    }

    // Initialize dp[][] array
    int dp[N + 1][N + 1];
    memset(dp, 0, sizeof(dp));
    dp[1][0]++;

    // Stores the count of splitting
    int ans = 0;

    // Iterate over the range [0, N]
    for (int i = 0; i < N; i++) {
        for (int j = N; j >= 1; j--) {

            // Update the dp table
            dp[j + 1][pre[i + 1] % (j + 1)]
                += dp[j][pre[i + 1] % j];

            // If the last index is
            // reached, then add it
            // to the variable ans
            if (i == N - 1) {
                ans += dp[j][pre[i + 1] % j];
            }
        }
    }

    // Return the possible count of
    // splitting of array into subarrays
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << countOfWays(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class GFG {

// Function to count ways to split
// an array into subarrays such that
// sum of the i-th subarray is
// divisible by i
static int countOfWays(int arr[], int N)
{

    // Stores the prefix sum of array
    int pre[] = new int[N + 1];

    for (int i = 0; i < N; i++) {

        // Find the prefix sum
        pre[i + 1] = pre[i] + arr[i];
    }

    // Initialize dp[][] array
    int dp[][] = new int [N + 2][N + 2];

    dp[1][0]++;

    // Stores the count of splitting
    int ans = 0;

    // Iterate over the range [0, N]
    for (int i = 0; i < N; i++) {
        for (int j = N; j >= 1; j--) {

            // Update the dp table
            dp[j + 1][pre[i + 1] % (j + 1)]
                += dp[j][pre[i + 1] % j];

            // If the last index is
            // reached, then add it
            // to the variable ans
            if (i == N - 1) {
                ans += dp[j][pre[i + 1] % j];
            }
        }
    }

    // Return the possible count of
    // splitting of array into subarrays
    return ans;
}

    // Driver Code
    public static void main (String[] args) {

            int arr[] = { 1, 2, 3, 4 };
            int N = arr.length;

            System.out.println(countOfWays(arr, N));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

import numpy as np

# Function to count ways to split
# an array into subarrays such that
# sum of the i-th subarray is
# divisible by i
def countOfWays(arr, N) :

    # Stores the prefix sum of array
    pre = [ 0 ] * (N + 1);

    for i in range(N) :

        # Find the prefix sum
        pre[i + 1] = pre[i] + arr[i];

    # Initialize dp[][] array
    dp = np.zeros((N + 2,N + 2));
    dp[1][0] += 1;

    # Stores the count of splitting
    ans = 0;

    # Iterate over the range [0, N]
    for i in range(N) :
        for j in range(N, 0, -1) :

            # Update the dp table
            dp[j + 1][pre[i + 1] % (j + 1)] += dp[j][pre[i + 1] % j];

            # If the last index is
            # reached, then add it
            # to the variable ans
            if (i == N - 1) :
                ans += dp[j][pre[i + 1] % j];

    # Return the possible count of
    # splitting of array into subarrays
    return ans;

# Driver Code
if __name__ ==  "__main__" :

    arr = [ 1, 2, 3, 4 ];
    N = len(arr);

    print(countOfWays(arr, N));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to count ways to split
// an array into subarrays such that
// sum of the i-th subarray is
// divisible by i
static int countOfWays(int[] arr, int N)
{

    // Stores the prefix sum of array
    int[] pre = new int[N + 1];

    for (int i = 0; i < N; i++) {

        // Find the prefix sum
        pre[i + 1] = pre[i] + arr[i];
    }

    // Initialize dp[][] array
    int[,] dp = new int [N + 2, N + 2];

    dp[1, 0]++;

    // Stores the count of splitting
    int ans = 0;

    // Iterate over the range [0, N]
    for (int i = 0; i < N; i++) {
        for (int j = N; j >= 1; j--) {

            // Update the dp table
            dp[j + 1, pre[i + 1] % (j + 1)]
                += dp[j, pre[i + 1] % j];

            // If the last index is
            // reached, then add it
            // to the variable ans
            if (i == N - 1) {
                ans += dp[j, pre[i + 1] % j];
            }
        }
    }

    // Return the possible count of
    // splitting of array into subarrays
    return ans;
}

  // Driver Code
  public static void Main(String []args) {

    int[] arr = { 1, 2, 3, 4 };
    int N = arr.Length;

    Console.WriteLine(countOfWays(arr, N));
  }

}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count ways to split
// an array into subarrays such that
// sum of the i-th subarray is
// divisible by i
function countOfWays(arr, N)
{

  // Stores the prefix sum of array
  let pre = new Array(N + 1).fill(0);

  for (let i = 0; i < N; i++)
  {

    // Find the prefix sum
    pre[i + 1] = pre[i] + arr[i];
  }

  // Initialize dp[][] array
  let dp = new Array(N + 2).fill(0).map(() => new Array(N + 2).fill(0));

  dp[1][0]++;

  // Stores the count of splitting
  let ans = 0;

  // Iterate over the range [0, N]
  for (let i = 0; i < N; i++) {
    for (let j = N; j >= 1; j--) {
      // Update the dp table
      dp[j + 1][pre[i + 1] % (j + 1)] += dp[j][pre[i + 1] % j];

      // If the last index is
      // reached, then add it
      // to the variable ans
      if (i == N - 1) {
        ans += dp[j][pre[i + 1] % j];
      }
    }
  }

  // Return the possible count of
  // splitting of array into subarrays
  return ans;
}

// Driver Code

let arr = [1, 2, 3, 4];
let N = arr.length;

document.write(countOfWays(arr, N));

// This code is contributed by _Saurabh_Jaiswal

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*