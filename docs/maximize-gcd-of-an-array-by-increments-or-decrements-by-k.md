# 通过增加或减少 K 来最大化数组的 GCD

> 原文:[https://www . geesforgeks . org/maximize-gcd-of-a-array-by-increments-k/](https://www.geeksforgeeks.org/maximize-gcd-of-an-array-by-increments-or-decrements-by-k/)

给定一个由 **N** 正整数**T7】和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过 **K** 增加或减少任意数组元素来最大化数组[GCD](https://www.geeksforgeeks.org/gcd-two-array-numbers/)**arr【】**。**

**示例:**

> **输入:** arr[] = {3，9，15，24}，K = 1
> **输出:** 4
> **解释:**
> 对数组 arr[]:
> 将 arr[0]递增 1。因此，arr[]修改为{4，9，15，24}。
> 将 arr[1]减 1。因此，arr[]修改为{4，8，15，24}。
> 将 arr[2]增加 1。因此，arr[]修改为{4，8，16，24}。
> 因此，修改后数组的 GCD 为 4。
> 
> **输入:** arr[] = {5，9，2}，K = 1
> T3】输出: 3

**天真方法:**解决这个问题最简单的方法是考虑每个数组元素**arr【I】**的所有三个选项，即增加**arr【I】**到 **K** ，减少**arr【I】**到 **K** 或者既不增加也不减少**arr【I】**。使用[递归](https://www.geeksforgeeks.org/recursion/)生成所有 3 种情况下形成的数组，并打印得到的所有数组的最大值 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。

***时间复杂度:**O(3<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。按照以下步骤解决给定的问题:

*   初始化一个辅助数组，比如说 **dp[][3]** ，其中 **dp[i][0]** 、 **dp[i][1]** 、 **dp[i][2]** 通过不改变 **i <sup>th</sup> 元素**，递增或递减 **i <sup>th</sup> 来表示最大可能 GCD 到**I**th 索引**
*   通过分别更新 **dp[0][0]** 、 **dp[0][1]** 和 **dp[0][2]** 将第一行 **dp[][3]** 填充为 **arr[0]** 、 **arr[0] + K** 和**arr[0]–K**。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N–1】**并执行以下步骤:
    *   对于 **dp[i][0]** ，一次查找 **A[i]** 的最大[GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)3 个前状态，即**DP[I–1][0]、DP[I–1][1]**和**DP[I–1][2]**，并将最大结果存储在 **dp[i][0]** 中。
    *   同样，通过分别取 **(arr[i] + K)** 和**(arr[I]–K)**，将结果存储在 **dp[i][1]** 和 **dp[i][2]** 中。
*   完成以上步骤后，打印行[最大值**DP【N–1】**作为结果。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum GCD
// by taking each operation
int findGCD(int x, int y, int z, int res)
{
    // Store the maximum GCD obtained
    // by either incrementing, decrementing
    // or not changing A[i]
    int ans = __gcd(x, res);
    ans = max(ans, __gcd(y, res));
    ans = max(ans, __gcd(z, res));

    // Return the maximum GCD
    return ans;
}

// Function to find the maximum GCD of
// the array arrA[] by either increasing
// or decreasing the array elements by K
int maximumGCD(int A[], int N, int K)
{
    // Initialize a dp table of size N*3
    int dp[N][3];
    memset(dp, 0, sizeof(dp));

    // Base Cases:
    // If only one element is present
    dp[0][0] = A[0];
    dp[0][1] = A[0] + K;
    dp[0][2] = A[0] - K;

    // Traverse the array A[] over indices [1, N - 1]
    for (int i = 1; i < N; i++) {

        // Store the previous state results
        int x = dp[i - 1][0];
        int y = dp[i - 1][1];
        int z = dp[i - 1][2];

        // Store maximum GCD result
        // for each current state
        dp[i][0] = findGCD(x, y, z, A[i]);
        dp[i][1] = findGCD(x, y, z, A[i] + K);
        dp[i][2] = findGCD(x, y, z, A[i] - K);
    }

    // Store the required result
    int mx = max(
        { 3, dp[N - 1][0], dp[N - 1][1],
          dp[N - 1][2] });

    // Return the result
    return mx;
}

// Driver Code
int main()
{
    int arr[] = { 3, 9, 15, 24 };
    int K = 1;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maximumGCD(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Recursive function to return gcd of a and b
  static int gcd(int a, int b)
  {
    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return gcd(a-b, b);
    return gcd(a, b-a);
  }

  // Function to return the maximum GCD
  // by taking each operation
  static int findGCD(int x, int y, int z, int res)
  {
    // Store the maximum GCD obtained
    // by either incrementing, decrementing
    // or not changing A[i]
    int ans = gcd(x, res);
    ans = Math.max(ans, gcd(y, res));
    ans = Math.max(ans, gcd(z, res));

    // Return the maximum GCD
    return ans;
  }

  // Function to find the maximum GCD of
  // the array arrA[] by either increasing
  // or decreasing the array elements by K
  static int maximumGCD(int A[], int N, int K)
  {
    // Initialize a dp table of size N*3
    int dp[][] = new int[N][3];
    for (int i = 0; i < N; i++) {
      for (int j = 1; j < 3; j++) {
        dp[i][j] = 0;
      }
    }

    // Base Cases:
    // If only one element is present
    dp[0][0] = A[0];
    dp[0][1] = A[0] + K;
    dp[0][2] = A[0] - K;

    // Traverse the array A[] over indices [1, N - 1]
    for (int i = 1; i < N; i++) {

      // Store the previous state results
      int x = dp[i - 1][0];
      int y = dp[i - 1][1];
      int z = dp[i - 1][2];

      // Store maximum GCD result
      // for each current state
      dp[i][0] = findGCD(x, y, z, A[i]);
      dp[i][1] = findGCD(x, y, z, A[i] + K);
      dp[i][2] = findGCD(x, y, z, A[i] - K);
    }

    // Store the required result
    int mx = Math.max(3, Math.max(dp[N - 1][0], Math.max(dp[N - 1][1],
                                                         dp[N - 1][2])));

    // Return the result
    return mx;
  }

  // Driver code
  public static void main(String[] args)
  {
    int arr[] = { 3, 9, 15, 24 };
    int K = 1;
    int N = arr.length;

    System.out.print( maximumGCD(arr, N, K));
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to return the maximum GCD
# by taking each operation
def findGCD(x, y, z, res):

    # Store the maximum GCD obtained
    # by either incrementing, decrementing
    # or not changing A[i]
    ans = math.gcd(x, res)
    ans = max(ans, math.gcd(y, res))
    ans = max(ans, math.gcd(z, res))

    # Return the maximum GCD
    return ans

# Function to find the maximum GCD of
# the array arrA[] by either increasing
# or decreasing the array elements by K
def maximumGCD(A, N, K):

    # Initialize a dp table of size N*3
    dp = [[0 for x in range(3)]
             for y in range(N)]

    # Base Cases:
    # If only one element is present
    dp[0][0] = A[0]
    dp[0][1] = A[0] + K
    dp[0][2] = A[0] - K

    # Traverse the array A[] over
    # indices [1, N - 1]
    for i in range(1, N):

        # Store the previous state results
        x = dp[i - 1][0]
        y = dp[i - 1][1]
        z = dp[i - 1][2]

        # Store maximum GCD result
        # for each current state
        dp[i][0] = findGCD(x, y, z, A[i])
        dp[i][1] = findGCD(x, y, z, A[i] + K)
        dp[i][2] = findGCD(x, y, z, A[i] - K)

    # Store the required result
    mx = max([3, dp[N - 1][0],
                 dp[N - 1][1],
                 dp[N - 1][2]])

    # Return the result
    return mx

# Driver Code
if __name__ == "__main__":

    arr = [ 3, 9, 15, 24 ]
    K = 1
    N = len(arr)

    print(maximumGCD(arr, N, K))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Recursive function to return gcd of a and b
  static int gcd(int a, int b)
  {

    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return gcd(a-b, b);
    return gcd(a, b-a);
  }

  // Function to return the maximum GCD
  // by taking each operation
  static int findGCD(int x, int y, int z, int res)
  {

    // Store the maximum GCD obtained
    // by either incrementing, decrementing
    // or not changing A[i]
    int ans = gcd(x, res);
    ans = Math.Max(ans, gcd(y, res));
    ans = Math.Max(ans, gcd(z, res));

    // Return the maximum GCD
    return ans;
  }

  // Function to find the maximum GCD of
  // the array arrA[] by either increasing
  // or decreasing the array elements by K
  static int maximumGCD(int[] A, int N, int K)
  {

    // Initialize a dp table of size N*3
    int[,] dp = new int[N, 3];
    for (int i = 0; i < N; i++) {
      for (int j = 1; j < 3; j++) {
        dp[i, j] = 0;
      }
    }

    // Base Cases:
    // If only one element is present
    dp[0, 0] = A[0];
    dp[0, 1] = A[0] + K;
    dp[0, 2] = A[0] - K;

    // Traverse the array A[] over indices [1, N - 1]
    for (int i = 1; i < N; i++) {

      // Store the previous state results
      int x = dp[i - 1, 0];
      int y = dp[i - 1, 1];
      int z = dp[i - 1, 2];

      // Store maximum GCD result
      // for each current state
      dp[i, 0] = findGCD(x, y, z, A[i]);
      dp[i, 1] = findGCD(x, y, z, A[i] + K);
      dp[i, 2] = findGCD(x, y, z, A[i] - K);
    }

    // Store the required result
    int mx = Math.Max(3, Math.Max(dp[N - 1, 0], Math.Max(dp[N - 1, 1],
                                                         dp[N - 1, 2])));

    // Return the result
    return mx;
  }

  // Driver code
  public static void Main()
  {
    int[] arr = { 3, 9, 15, 24 };
    int K = 1;
    int N = arr.Length;

    Console.Write( maximumGCD(arr, N, K));
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>
//Javascript program for the above approach

function gcd( a, b)
  {
    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return gcd(a-b, b);
    return gcd(a, b-a);
  }

function findGCD(x, y, z,  res)
{
    // Store the maximum GCD obtained
    // by either incrementing, decrementing
    // or not changing A[i]
    var ans = gcd(x, res);
    ans = Math.max(ans, gcd(y, res));
    ans = Math.max(ans, gcd(z, res));

    // Return the maximum GCD
    return ans;
}

// Function to find the maximum GCD of
// the array arrA[] by either increasing
// or decreasing the array elements by K
function maximumGCD( A, N, K)
{
    // Initialize a dp table of size N*3
var dp = new Array(N).fill(0).map(() => new Array(3).fill(0));
    // Base Cases:
    // If only one element is present
    dp[0][0] = A[0];
    dp[0][1] = A[0] + K;
    dp[0][2] = A[0] - K;

    // Traverse the array A[] over indices [1, N - 1]
    for (var i = 1; i < N; i++) {

        // Store the previous state results
        var x = dp[i - 1][0];
        var y = dp[i - 1][1];
        var z = dp[i - 1][2];

        // Store maximum GCD result
        // for each current state
        dp[i][0] = findGCD(x, y, z, A[i]);
        dp[i][1] = findGCD(x, y, z, A[i] + K);
        dp[i][2] = findGCD(x, y, z, A[i] - K);
    }

    // Store the required result
    var mx = Math.max(3, Math.max(dp[N - 1][0], Math.max(dp[N - 1][1],
                                                         dp[N - 1][2])));

    // Return the result
    return mx;
}

var arr = [ 3, 9, 15, 24 ];
    var K = 1;
    var N = arr.length;

document.write( maximumGCD(arr, N, K));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
4
```

**时间复杂度:** *O(N*log(M))，其中 **M** 是数组中* [*最小的元素*](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)*arr【】*
**辅助空间:** *O(N)*