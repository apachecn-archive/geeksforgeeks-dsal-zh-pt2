# 最大化相同大小子序列的相同索引元素的乘积

> 原文:[https://www . geeksforgeeks . org/最大化相同大小的索引元素子序列的乘积/](https://www.geeksforgeeks.org/maximize-product-of-same-indexed-elements-of-same-size-subsequences/)

给定两个整数数组 **a[]** 和 **b[]** ，任务是从两个给定数组中找到两个等长子序列的相同索引元素的最大可能乘积。

**示例:**

> **输入:** a[] = {-3，1，-12，7}，b[] = {3，2，-6，7}
> **输出:** 124
> **解释:**a[]的子序列[1，-12，7]和 b[]的子序列[3，-6，7]给出最大定标积，(1*3 + (-12)*(-6) + 7*7) = 124。
> 
> **输入:** a[] = {-2，6，-2，-5}，b[] = {-3，4，-2，8}
> **输出:** 54
> **解释:**来自 a[]的子序列[-2，6]和来自 b[]的子序列[-3，8]给出最大定标积，(-2)*(-3) + 6*8) = 54。

**方法:**问题类似于[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的[最长公共子序列](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)问题。基于[递归](https://www.geeksforgeeks.org/recursion/)和[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)的自顶向下方法解释如下:

*   让我们定义一个函数 F(X，Y)，它返回数组 a[0-X]和 b[0-Y]之间的最大标量积。
*   以下是递归定义:

> F(X，Y) =最大值(a[X]* b[Y]+F(X–1，Y–1)；使用两个数组中的最后一个元素，并进一步检查
> a[X]* b[Y]；只使用最后一个元素作为最大乘积
> F(X–1，Y)；忽略第一个数组的最后一个元素
> F(X，Y–1))；忽略第二个元素的最后一个元素

*   使用二维数组进行记忆，避免重新计算相同的子问题。

下面是上述方法的实现:

## C++

```
// C++ implementation to maximize
// product of same-indexed elements
// of same size subsequences

#include <bits/stdc++.h>
using namespace std;

#define INF 10000000

// Utility function to find the maximum
int maximum(int A, int B, int C, int D)
{
    return max(max(A, B), max(C, D));
}

// Utility function to find
// the maximum scalar product
// from the equal length sub-sequences
// taken from the two given array
int maxProductUtil(
    int X, int Y,
    int* A, int* B,
    vector<vector<int> >& dp)
{
    // Return a very small number
    // if index is invalid
    if (X < 0 or Y < 0)
        return -INF;

    // If the sub-problem is already
    // evaluated, then return it
    if (dp[X][Y] != -1)
        return dp[X][Y];

    // Take the maximum of all
    // the recursive cases
    dp[X][Y]
        = maximum(
            A[X] * B[Y]
                + maxProductUtil(
                      X - 1, Y - 1, A, B, dp),
            A[X] * B[Y],
            maxProductUtil(
                X - 1, Y, A, B, dp),
            maxProductUtil(
                X, Y - 1, A, B, dp));

    return dp[X][Y];
}

// Function to find maximum scalar
// product from same size sub-sequences
// taken from the two given array
int maxProduct(int A[], int N,
               int B[], int M)
{
    // Initialize a 2-D array
    // for memoization
    vector<vector<int> >
    dp(N, vector<int>(M, -1));

    return maxProductUtil(
        N - 1, M - 1,
        A, B, dp);
}

// Driver Code
int main()
{
    int a[] = { -2, 6, -2, -5 };
    int b[] = { -3, 4, -2, 8 };

    int n = sizeof(a) / sizeof(a[0]);
    int m = sizeof(b) / sizeof(b[0]);

    cout << maxProduct(a, n, b, m);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to maximize
// product of same-indexed elements
// of same size subsequences
class GFG{

static final int INF = 10000000;

// Utility function to find the maximum
static int maximum(int A, int B,
                   int C, int D)
{
    return Math.max(Math.max(A, B),
                    Math.max(C, D));
}

// Utility function to find the
// maximum scalar product from
// the equal length sub-sequences
// taken from the two given array
static int maxProductUtil(int X, int Y,
                          int []A, int[] B,
                          int [][]dp)
{

    // Return a very small number
    // if index is invalid
    if (X < 0 || Y < 0)
        return -INF;

    // If the sub-problem is already
    // evaluated, then return it
    if (dp[X][Y] != -1)
        return dp[X][Y];

    // Take the maximum of all
    // the recursive cases
    dp[X][Y] = maximum(A[X] * B[Y] +
                       maxProductUtil(X - 1, Y - 1,
                                      A, B, dp),
                       A[X] * B[Y],
                       maxProductUtil(X - 1, Y,
                                      A, B, dp),
                       maxProductUtil(X, Y - 1,
                                      A, B, dp));

    return dp[X][Y];
}

// Function to find maximum scalar
// product from same size sub-sequences
// taken from the two given array
static int maxProduct(int A[], int N,
                      int B[], int M)
{

    // Initialize a 2-D array
    // for memoization
    int [][]dp = new int[N][M];
    for(int i = 0; i < N; i++)
    {
       for(int j = 0; j < M; j++)
       {
          dp[i][j] = -1;
       }
    }

    return maxProductUtil(N - 1, M - 1,
                          A, B, dp);
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { -2, 6, -2, -5 };
    int b[] = { -3, 4, -2, 8 };

    int n = a.length;
    int m = b.length;

    System.out.print(maxProduct(a, n, b, m));
}
}

// This code is contributed by Amal Kumar Choubey
```

## 蟒蛇 3

```
# Python3 implementation to maximize
# product of same-indexed elements
# of same size subsequences
INF = 10000000

# Utility function to find the maximum
def maximum(A, B, C, D):

    return max(max(A, B), max(C, D))

# Utility function to find
# the maximum scalar product
# from the equal length sub-sequences
# taken from the two given array
def maxProductUtil(X, Y, A, B, dp):

    # Return a very small number
    # if index is invalid
    if (X < 0 or Y < 0):
        return -INF

    # If the sub-problem is already
    # evaluated, then return it
    if (dp[X][Y] != -1):
        return dp[X][Y]

    # Take the maximum of all
    # the recursive cases
    dp[X][Y]= maximum(A[X] * B[Y] +
                      maxProductUtil(X - 1, Y - 1,
                                     A, B, dp),
                      A[X] * B[Y],
                      maxProductUtil(X - 1, Y, A,
                                     B, dp),
                      maxProductUtil(X, Y - 1, A,
                                     B, dp))

    return dp[X][Y]

# Function to find maximum scalar
# product from same size sub-sequences
# taken from the two given array
def maxProduct(A, N, B, M):

    # Initialize a 2-D array
    # for memoization
    dp = [[-1 for i in range(m)]
              for i in range(n)]

    return maxProductUtil(N - 1, M - 1,
                          A, B, dp)

# Driver Code
a = [ -2, 6, -2, -5 ]
b = [ -3, 4, -2, 8 ]
n = len(a)
m = len(b)

print(maxProduct(a, n, b, m))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation to maximize
// product of same-indexed elements
// of same size subsequences
using System;

class GFG{

static readonly int INF = 10000000;

// Utility function to find the maximum
static int maximum(int A, int B,
                   int C, int D)
{
    return Math.Max(Math.Max(A, B),
                    Math.Max(C, D));
}

// Utility function to find the
// maximum scalar product from
// the equal length sub-sequences
// taken from the two given array
static int maxProductUtil(int X, int Y,
                          int []A, int[] B,
                          int [,]dp)
{

    // Return a very small number
    // if index is invalid
    if (X < 0 || Y < 0)
        return -INF;

    // If the sub-problem is already
    // evaluated, then return it
    if (dp[X, Y] != -1)
        return dp[X, Y];

    // Take the maximum of all
    // the recursive cases
    dp[X, Y] = maximum(A[X] * B[Y] +
                       maxProductUtil(X - 1, Y - 1,
                                        A, B, dp),
                       A[X] * B[Y],
                       maxProductUtil(X - 1, Y,
                                      A, B, dp),
                       maxProductUtil(X, Y - 1,
                                      A, B, dp));

    return dp[X, Y];
}

// Function to find maximum scalar
// product from same size sub-sequences
// taken from the two given array
static int maxProduct(int []A, int N,
                      int []B, int M)
{

    // Initialize a 2-D array
    // for memoization
    int [,]dp = new int[N, M];
    for(int i = 0; i < N; i++)
    {
       for(int j = 0; j < M; j++)
       {
          dp[i, j] = -1;
       }
    }

    return maxProductUtil(N - 1, M - 1,
                          A, B, dp);
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { -2, 6, -2, -5 };
    int []b = { -3, 4, -2, 8 };

    int n = a.Length;
    int m = b.Length;

    Console.Write(maxProduct(a, n, b, m));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// Javascript implementation to maximize
// product of same-indexed elements
// of same size subsequences

let INF = 10000000;

// Utility function to find the maximum
function maximum(A, B, C, D)
{
    return Math.max(Math.max(A, B),
                    Math.max(C, D));
}

// Utility function to find the
// maximum scalar product from
// the equal length sub-sequences
// taken from the two given array
function maxProductUtil(X, Y, A, B, dp)
{

    // Return a very small number
    // if index is invalid
    if (X < 0 || Y < 0)
        return -INF;

    // If the sub-problem is already
    // evaluated, then return it
    if (dp[X][Y] != -1)
        return dp[X][Y];

    // Take the maximum of all
    // the recursive cases
    dp[X][Y] = maximum(A[X] * B[Y] +
                       maxProductUtil(X - 1, Y - 1,
                                      A, B, dp),
                       A[X] * B[Y],
                       maxProductUtil(X - 1, Y,
                                      A, B, dp),
                       maxProductUtil(X, Y - 1,
                                      A, B, dp));

    return dp[X][Y];
}

// Function to find maximum scalar
// product from same size sub-sequences
// taken from the two given array
function maxProduct(A, N, B, M)
{

    // Initialize a 2-D array
    // for memoization
    let dp =new Array(N);
    for (var i = 0; i < dp.length; i++) {
    dp[i] = new Array(2);
    }
    for(let i = 0; i < N; i++)
    {
       for(let j = 0; j < M; j++)
       {
          dp[i][j] = -1;
       }
    }

    return maxProductUtil(N - 1, M - 1,
                          A, B, dp);
}

  // Driver Code

    let a = [ -2, 6, -2, -5 ];
    let b = [ -3, 4, -2, 8 ];

    let n = a.length;
    let m = b.length;

    document.write(maxProduct(a, n, b, m));

</script>
```

**Output:** 

```
54
```