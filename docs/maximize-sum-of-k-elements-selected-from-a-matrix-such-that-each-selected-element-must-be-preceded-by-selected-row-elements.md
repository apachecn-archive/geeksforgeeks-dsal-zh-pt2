# 最大化从矩阵中选择的 K 个元素的总和，使得每个选择的元素之前必须有选择的行元素

> 原文:[https://www . geesforgeks . org/max-sum-k-elements-从矩阵中选择-这样-每个选择的元素前面必须有选择的行元素/](https://www.geeksforgeeks.org/maximize-sum-of-k-elements-selected-from-a-matrix-such-that-each-selected-element-must-be-preceded-by-selected-row-elements/)

给定一个大小为 **N * M** 的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)**arr【】【】】**和一个整数 **K** ，任务是选择具有最大可能和的 **K** 元素，使得如果选择了元素**arr【I】【j】**，则来自**I**T14】第行的所有元素出现在**j**T18】第行之前

**示例:**

> **输入:** arr[][] = {{10，10，100，30}，{80，50，10，50}}，K = 5
> **输出:** 250
> **说明:**
> 从第一行选择前 3 个元素，求和= 10 + 10 + 100 = 120
> 从第二行选择前 2 个元素，求和= 80 + 50 = 130
> 因此
> 
> **输入:** arr[][] = {{30，10，110，13}，{810，152，12，5}，{124，24，54，124}}，K = 6
> **输出:** 1288
> **解释:**
> 从第二行选择前 2 个元素，求和= 810 + 152 = 962
> 从第三行选择所有 4 个元素，求和

**天真方法:**解决问题最简单的方法是[基于指定的约束从给定的矩阵中生成所有可能的子集**大小为 K** 的](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)，并从这些子集计算最大可能和。

***时间复杂度:** O((N*M)！/(K！)*(N * M–K)！)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。其思想是找到选择 **i** 元素直到 2D 数组**arr【】【】**的 **j <sup>第</sup>行的最大和。辅助数组 **dp[i][j + 1]** 存储选择 **i** 元素直到矩阵 **arr[][]** 的 **j <sup>第</sup>** 行的最大和。按照以下步骤解决问题:**

*   初始化大小为 **(K+1)*(N+1)** 的 **dp[][]** 表，并将 **dp[0][i]** 初始化为 **0** ，因为没有元素的和等于 **0** 。
*   将 **dp[i][0]** 初始化为 **0** ，因为没有要选择的元素。
*   使用两个嵌套循环迭代范围**【0，K】**，分别使用变量 **i** 和 **j** 迭代范围**【0，N】**:
    *   初始化一个变量，将 **sum** 设为 **0** ，以跟踪**arr【】【】**的 **j <sup>th</sup>** 行中元素的累计和。
    *   将 **maxSum** 初始化为 **dp[i][j]** ，如果不需要从 **arr[][]** 的 **j <sup>th</sup>** 行中选择任何项目。
    *   以 **k** 作为 **1** 迭代，直到 **k > M** 或 **k > i** :
        *   递增**和+=买入【j】【k–1】**。
        *   将现有 **maxSum** 和**(sum+DP[I–k][j])**的最大值存储在 **maxSum** 中。
    *   将 **dp[i][j + 1]** 存储为 **maxSum** 的值。
*   将数值 **dp[K][N]** 打印为 **K 元素**的最大和，直到矩阵**arr【】【】**的**(N–1)<sup>第</sup>行**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to return the maximum
// of two elements
int max(int a, int b)
{
    return a > b ? a : b;
}

// Function to find the maximum sum
// of selecting K elements from
// the given 2D array arr[][]
int maximumsum(int arr[][4], int K,
               int N, int M)
{
    int sum = 0, maxSum;
    int i, j, k;

    // dp table of size (K+1)*(N+1)
    int dp[K + 1][N + 1];

    // Initialize dp[0][i] = 0
    for (i = 0; i <= N; i++)
        dp[0][i] = 0;

    // Initialize dp[i][0] = 0
    for (i = 0; i <= K; i++)
        dp[i][0] = 0;

    // Selecting i elements
    for (i = 1; i <= K; i++) {

        // Select i elements till jth row
        for (j = 0; j < N; j++) {

            // dp[i][j+1] is the maximum
            // of selecting i elements till
            // jth row

            // sum = 0, to keep track of
            // cumulative elements sum
            sum = 0;
            maxSum = dp[i][j];

            // Traverse arr[j][k] until
            // number of elements until k>i
            for (k = 1; k <= M && k <= i; k++) {

                // Select arr[j][k - 1]th item
                sum += arr[j][k - 1];

                maxSum
                    = max(maxSum,
                          sum + dp[i - k][j]);
            }

            // Store the maxSum in dp[i][j+1]
            dp[i][j + 1] = maxSum;
        }
    }

    // Return the maximum sum
    return dp[K][N];
}

// Driver Code
int main()
{
    int arr[][4] = { { 10, 10, 100, 30 },
                     { 80, 50, 10, 50 } };

    int N = 2, M = 4;
    int K = 5;

    // Function Call
    cout << maximumsum(arr, K, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to return the maximum
// of two elements
static int max(int a, int b)
{
    return a > b ? a : b;
}

// Function to find the maximum sum
// of selecting K elements from
// the given 2D array arr[][]
static int maximumsum(int arr[][], int K,
                      int N, int M)
{
    int sum = 0, maxSum;
    int i, j, k;

    // dp table of size (K+1)*(N+1)
    int[][] dp = new int[K + 1][N + 1];

    // Initialize dp[0][i] = 0
    for(i = 0; i <= N; i++)
        dp[0][i] = 0;

    // Initialize dp[i][0] = 0
    for(i = 0; i <= K; i++)
        dp[i][0] = 0;

    // Selecting i elements
    for(i = 1; i <= K; i++)
    {

        // Select i elements till jth row
        for(j = 0; j < N; j++)
        {

            // dp[i][j+1] is the maximum
            // of selecting i elements till
            // jth row

            // sum = 0, to keep track of
            // cumulative elements sum
            sum = 0;
            maxSum = dp[i][j];

            // Traverse arr[j][k] until
            // number of elements until k>i
            for(k = 1; k <= M && k <= i; k++)
            {

                // Select arr[j][k - 1]th item
                sum += arr[j][k - 1];

                maxSum = Math.max(maxSum,
                                  sum + dp[i - k][j]);
            }

            // Store the maxSum in dp[i][j+1]
            dp[i][j + 1] = maxSum;
        }
    }

    // Return the maximum sum
    return dp[K][N];
}

// Driver Code
public static void main(String[] args)
{
    int arr[][] =  { { 10, 10, 100, 30 },
                     { 80, 50, 10, 50 } };

    int N = 2, M = 4;
    int K = 5;

    // Function Call
    System.out.print(maximumsum(arr, K, N, M));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python program for the above approach
import math;

# Function to return the maximum
# of two elements
def max(a, b):
    if(a > b):
        return a;
    else:
        return b;

# Function to find the maximum sum
# of selecting K elements from
# the given 2D array arr
def maximumsum(arr, K, N, M):
    sum = 0;
    maxSum = 0;

    # dp table of size (K+1)*(N+1)
    dp = [[0 for i in range(N + 1)] for j in range(K + 1)]

    # Initialize dp[0][i] = 0
    for i in range(0, N + 1):
        dp[0][i] = 0;

    # Initialize dp[i][0] = 0
    for i in range(0, K + 1):
        dp[i][0] = 0;

    # Selecting i elements
    for  i in range(1, K + 1):

        # Select i elements till jth row
        for  j in range(0, N):

            # dp[i][j+1] is the maximum
            # of selecting i elements till
            # jth row

            # sum = 0, to keep track of
            # cumulative elements sum
            sum = 0;
            maxSum = dp[i][j];

            # Traverse arr[j][k] until
            # number of elements until k>i
            for k in range(1, i + 1):
                if(k > M):
                    break;

                # Select arr[j][k - 1]th item
                sum += arr[j][k - 1];

                maxSum = max(maxSum, sum + dp[i - k][j]);

            # Store the maxSum in dp[i][j+1]
            dp[i][j + 1] = maxSum;

    # Return the maximum sum
    return dp[K][N];

# Driver Code
if __name__ == '__main__':
    arr = [[10, 10, 100, 30], [80, 50, 10, 50]];

    N = 2;
    M = 4;
    K = 5;

    # Function Call
    print(maximumsum(arr, K, N, M));

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return the maximum
// of two elements
static int max(int a, int b)
{
    return a > b ? a : b;
}

// Function to find the maximum sum
// of selecting K elements from
// the given 2D array [,]arr
static int maximumsum(int [,]arr, int K,
                      int N, int M)
{
    int sum = 0, maxSum;
    int i, j, k;

    // dp table of size (K+1)*(N+1)
    int[,] dp = new int[K + 1, N + 1];

    // Initialize dp[0,i] = 0
    for(i = 0; i <= N; i++)
        dp[0, i] = 0;

    // Initialize dp[i,0] = 0
    for(i = 0; i <= K; i++)
        dp[i, 0] = 0;

    // Selecting i elements
    for(i = 1; i <= K; i++)
    {

        // Select i elements till jth row
        for(j = 0; j < N; j++)
        {

            // dp[i,j+1] is the maximum
            // of selecting i elements till
            // jth row

            // sum = 0, to keep track of
            // cumulative elements sum
            sum = 0;
            maxSum = dp[i, j];

            // Traverse arr[j,k] until
            // number of elements until k>i
            for(k = 1; k <= M && k <= i; k++)
            {

                // Select arr[j,k - 1]th item
                sum += arr[j, k - 1];

                maxSum = Math.Max(maxSum,
                                  sum + dp[i - k, j]);
            }

            // Store the maxSum in dp[i,j+1]
            dp[i, j + 1] = maxSum;
        }
    }

    // Return the maximum sum
    return dp[K, N];
}

// Driver Code
public static void Main(String[] args)
{
    int [,]arr =  { { 10, 10, 100, 30 },
                    { 80, 50, 10, 50 } };

    int N = 2, M = 4;
    int K = 5;

    // Function Call
    Console.Write(maximumsum(arr, K, N, M));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to return the maximum
// of two elements
function max(a, b)
{
    return a > b ? a : b;
}

// Function to find the maximum sum
// of selecting K elements from
// the given 2D array arr[][]
function maximumsum(arr, K,
                      N, M)
{
    let sum = 0, maxSum;
    let i, j, k;

    // dp table of size (K+1)*(N+1)
    let dp = new Array(K + 1);

    // Loop to create 2D array using 1D array
    for ( i = 0; i < dp.length; i++) {
        dp[i] = new Array(2);
    }

    // Initialize dp[0][i] = 0
    for(i = 0; i <= N; i++)
        dp[0][i] = 0;

    // Initialize dp[i][0] = 0
    for(i = 0; i <= K; i++)
        dp[i][0] = 0;

    // Selecting i elements
    for(i = 1; i <= K; i++)
    {

        // Select i elements till jth row
        for(j = 0; j < N; j++)
        {

            // dp[i][j+1] is the maximum
            // of selecting i elements till
            // jth row

            // sum = 0, to keep track of
            // cumulative elements sum
            sum = 0;
            maxSum = dp[i][j];

            // Traverse arr[j][k] until
            // number of elements until k>i
            for(k = 1; k <= M && k <= i; k++)
            {

                // Select arr[j][k - 1]th item
                sum += arr[j][k - 1];

                maxSum = Math.max(maxSum,
                                  sum + dp[i - k][j]);
            }

            // Store the maxSum in dp[i][j+1]
            dp[i][j + 1] = maxSum;
        }
    }

    // Return the maximum sum
    return dp[K][N];
}

// Driver code
    let arr =  [[ 10, 10, 100, 30 ],
                     [ 80, 50, 10, 50 ]];

    let N = 2, M = 4;
    let K = 5;

    // Function Call
    document.write(maximumsum(arr, K, N, M));

 // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
250
```

***时间复杂度:**O(K * N * M)*
T5**辅助空间:** O(K*N)