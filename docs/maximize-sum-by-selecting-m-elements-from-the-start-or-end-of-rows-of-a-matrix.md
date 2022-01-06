# 通过从矩阵的行的开始或结束选择 M 个元素来最大化总和

> 原文:[https://www . geeksforgeeks . org/通过从矩阵的起始行或结束行中选择 m 个元素来最大化总和/](https://www.geeksforgeeks.org/maximize-sum-by-selecting-m-elements-from-the-start-or-end-of-rows-of-a-matrix/)

给定一个由可变长度的 **N** 行组成的 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/) **区块[][]** 。任务是从一行的开始或结束处的**块【】【】**中选择最多 **M** 个具有最大可能和的元素。

**示例:**

> **输入:** N = 3，M = 4
> Blocks[][] = {{2，3，5}，{-1，7}，{8，10}}
> **输出:** 30
> **说明:**
> 从 1 <sup>st</sup> 行选择{5}。
> 从 2 <sup>和</sup>行中选择{7}。
> 从 3 <sup>第</sup>行中选择{8，10}。
> 
> **输入:** N = 3，M = 2
> Blocks[][] = {{100，3，-1}，{-1，7，10}，{8，10，15}}
> **输出:** 115
> **说明:**
> 从 1 <sup>st</sup> 行选择{100}。
> 跳过第 2 排<sup>和第 2 排</sup>。
> 从 3 <sup>第</sup>行中选择{15}。

**天真方法:**最简单的方法是遍历矩阵的所有行，将所有元素推入一个向量中，[对其进行排序](https://www.geeksforgeeks.org/sort-c-stl/)。计算最后的 **M** 元素的总和，并打印为所需答案。

***时间复杂度:** O(N * KlogK)，其中 K 是任何块可以拥有的最大大小。*
***辅助空间:** O(N * K)*

**高效方法:**优化上述方法，思路是使用 [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) 使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)。请遵循以下步骤:

*   给定 **N** 行，从每一行中，从 **i <sup>第</sup>T5】行中选择任意线段，比如从 **l 到 r** 。**
*   **I**行的元素个数为**(r–l+1)**，进入下一行。
*   要计算最大总和，请使用[](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)**[**前缀总和技术**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 来计算总和。**
*   **初始化一个 2D 数组 **dp[][]** ，其中 **dp[N][M]** 通过从 **N** 行中最多选择 **M** 个元素来存储最大和。

    *   考虑以下两种情况:
        *   要么跳过当前行。
        *   从当前行中选择任何不超过所选元素数量的段。** 

**下面是上述方法的实现:**

## **C++14**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to select m elements
// having maximum sum
long mElementsWithMaxSum(vector<vector<int> > matrix,
                         int M, int block,
                         vector<vector<int> > dp)
{

    // Base case
    if (block == matrix.size())
        return 0;

    // If precomputed subproblem occurred
    if (dp[block][M] != -1)
        return dp[block][M];

    // Either skip the current row
    long ans = mElementsWithMaxSum(matrix, M,
                                   block + 1, dp);

    // Iterate through all the possible
    // segments of current row
    for(int i = 0;
            i < matrix[block].size(); i++)
    {
        for(int j = i;
                j < matrix[block].size(); j++)
        {

            // Check if it is possible to select
            // elements from i to j
            if (j - i + 1 <= M)
            {

                // Compuete the sum of i to j as
                // calculated
                ans = max(ans, matrix[block][j] -
                         ((i - 1) >= 0 ?
                         matrix[block][i - 1] : 0) +
                         mElementsWithMaxSum(matrix,
                                             M - j +
                                             i - 1,
                                         block + 1, dp));
            }
        }
    }

    // Store the computed answer and return
    return dp[block][M] = ans;
}

// Function to precompute the prefix sum
// for every row of the matrix
void preComputing(vector<vector<int>> matrix,
                  int N)
{

    // Preprocessing to calculate sum from i to j
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < matrix[i].size(); j++)
        {
            matrix[i][j] = (j > 0 ?
                  matrix[i][j - 1] : 0) +
                  matrix[i][j];
        }
    }
}

// Utility function to select m elements having
// maximum sum
void mElementsWithMaxSumUtil(vector<vector<int>> matrix,
                             int M, int N)
{

    // Preprocessing step
    preComputing(matrix, N);
    long sum = 10;

    // Initialize dp array with -1
    vector<vector<int>> dp;
    dp.resize(N + 5);
    for(int i = 0; i < N + 5; i++)
        for(int j = 0; j < M + 5; j++)
            dp[i].push_back(-1);

    // Stores maximum sum of M elements
     sum += mElementsWithMaxSum(matrix, M,
                                0, dp);

    cout << sum;
}

// Driver Code
int main()
{

    // Given N
    int N = 3;

    // Given M
    int M = 4;

    // Given matrix
    vector<vector<int>> matrix = { { 2, 3, 5 },
                                   { -1, 7 },
                                   { 8, 10 } };

    // Function call
    mElementsWithMaxSumUtil(matrix, M, N);
}

// This code is contributed by grand_master
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

import java.util.*;
public class GFG {

    // Function to select m elements
    // having maximum sum
    public static long
    mElementsWithMaxSum(long[][] matrix,
                        int M, int block,
                        long[][] dp)
    {
        // Base case
        if (block == matrix.length)
            return 0;

        // If precomputed subproblem occurred
        if (dp[block][M] != -1)
            return dp[block][M];

        // Either skip the current row
        long ans
            = mElementsWithMaxSum(matrix, M,
                                block + 1, dp);

        // Iterate through all the possible
        // segments of current row
        for (int i = 0;
            i < matrix[block].length; i++) {
            for (int j = i;
                j < matrix[block].length; j++) {

                // Check if it is possible to select
                // elements from i to j
                if (j - i + 1 <= M) {

                    // Compuete the sum of i to j as
                    // calculated
                    ans = Math.max(
                        ans,
                        matrix[block][j]
                            - ((i - 1) >= 0
                            ? matrix[block][i - 1]
                            : 0)
                            + mElementsWithMaxSum(
                                matrix, M - j + i - 1,
                                block + 1, dp));
                }
            }
        }

        // Store the computed answer and return
        return dp[block][M] = ans;
    }

    // Function to precompute the prefix sum
    // for every row of the matrix
    public static void
    preComputing(long[][] matrix, int N)
    {
        // Preprocessing to calculate sum from i to j
        for (int i = 0;
            i < N; i++) {
            for (int j = 0;
                j < matrix[i].length; j++) {
                matrix[i][j]
                    = (j > 0
                    ? matrix[i][j - 1] : 0)
                    + matrix[i][j];
            }
        }
    }

    // Utility function to select m elements having
    // maximum sum
    public static void
    mElementsWithMaxSumUtil(long[][] matrix,
                            int M, int N)
    {
        // Preprocessing step
        preComputing(matrix, N);

        // Initialize dp array with -1
        long dp[][] = new long[N + 5][M + 5];
        for (long i[] : dp)
            Arrays.fill(i, -1);

        // Stores maximum sum of M elements
        long sum = mElementsWithMaxSum(matrix, M,
                                    0, dp);

        // Print the sum
        System.out.print(sum);
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given N
        int N = 3;

        // Given M
        int M = 4;

        // Given matrix
        long[][] matrix
            = { { 2, 3, 5 }, { -1, 7 },
                { 8, 10 } };

        // Function Call
        mElementsWithMaxSumUtil(matrix, M, N);
    }
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to select m elements
# having maximum sum
def mElementsWithMaxSum(matrix, M, block, dp):

    # Base case
    if block == len(matrix):
        return 0

    # If precomputed subproblem occurred
    if (dp[block][M] != -1):
        return dp[block][M]

    # Either skip the current row
    ans = mElementsWithMaxSum(matrix, M,
                              block + 1, dp)

    # Iterate through all the possible
    # segments of current row
    for i in range(len(matrix[block])):
        for j in range(i, len(matrix[block])):

            # Check if it is possible to select
            # elements from i to j
            if (j - i + 1 <= M):

                # Compuete the sum of i to j as
                # calculated
                x = 0
                if i - 1 >= 0:
                    x = matrix[block][i - 1]

                ans = max(ans, matrix[block][j] - x +
                               mElementsWithMaxSum(matrix,
                                                   M - j +
                                                   i - 1,
                                               block + 1, dp))

    # Store the computed answer and return
    dp[block][M] = ans

    return ans

# Function to precompute the prefix sum
# for every row of the matrix
def preComputing(matrix, N):

    # Preprocessing to calculate sum from i to j
    for i in range(N):
        for j in range(len(matrix[i])):
            if j > 0:
                matrix[i][j] = matrix[i][j - 1]

    return matrix

# Utility function to select m elements having
# maximum sum
def mElementsWithMaxSumUtil(matrix, M, N):

    # Preprocessing step
    matrix = preComputing(matrix, N)
    sum = 20

    # Initialize dp array with -1
    dp = [[-1 for i in range(M + 5)]
              for i in range(N + 5)]

    # Stores maximum sum of M elements
    sum += mElementsWithMaxSum(matrix, M, 0, dp)

    print(sum)

# Driver Code
if __name__ == '__main__':

    # Given N
    N = 3

    # Given M
    M = 4

    # Given matrix
    matrix = [ [ 2, 3, 5 ],
               [ -1, 7 ],
               [ 8, 10 ] ]

    # Function call
    mElementsWithMaxSumUtil(matrix, M, N)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for
// the above approach
using System;
class GFG{

// Function to select m elements
// having maximum sum
public static int mElementsWithMaxSum(int[,] matrix,
                                    int M, int block,
                                    int[,] dp)
{
// Base case
if (block == matrix.GetLength(0))
    return 0;

// If precomputed subproblem occurred
if (dp[block, M] != -1)
    return dp[block, M];

// Either skip the current row
int ans = mElementsWithMaxSum(matrix, M,
                                block + 1, dp);

// Iterate through all the possible
// segments of current row
for (int i = 0;
        i < GetRow(matrix, block).Length; i++)
{
    for (int j = i;
            j < GetRow(matrix, block).Length; j++)
    {
    // Check if it is possible to select
    // elements from i to j
    if (j - i + 1 <= M)
    {
        // Compuete the sum of i to j as
        // calculated
        ans = Math.Max(ans, matrix[block, j] -
                                ((i - 1) >= 0 ?
                            matrix[block, i - 1] : 0) +
                            mElementsWithMaxSum(matrix,
                                                M - j + i - 1,
                                                block + 1, dp));
    }
    }
}

// Store the computed answer and return
return dp[block, M] = ans;
}

// Function to precompute the prefix sum
// for every row of the matrix
public static void preComputing(int[,] matrix,
                                int N)
{
// Preprocessing to calculate sum from i to j
for (int i = 0; i < N; i++)
{
    for (int j = 0;
            j < GetRow(matrix, i).Length; j++)
    {
    matrix[i, j] = (j > 0 ? matrix[i, j - 1] : 0) +
                            matrix[i, j];
    }
}
}

// Utility function to select
// m elements having maximum sum
public static void mElementsWithMaxSumUtil(int[,] matrix,
                                        int M, int N)
{
// Preprocessing step
preComputing(matrix, N);

// Initialize dp array with -1
int [,]dp = new int[N + 5, M + 5];
for(int i = 0; i < N + 5; i++)
{
    for (int j = 0; j < M + 5; j++)
    {
    dp[i, j] = -1;
    }
}

// Stores maximum sum of M elements
int sum = mElementsWithMaxSum(matrix, M,
                                0, dp);

// Print the sum
Console.Write(sum);
}

public static int[] GetRow(int[,] matrix,
                        int row)
{
var rowLength = matrix.GetLength(1);
var rowVector = new int[rowLength];

for (var i = 0; i < rowLength; i++)
    rowVector[i] = matrix[row, i];

return rowVector;
}

// Driver Code
public static void Main(String []args)
{
// Given N
int N = 3;

// Given M
int M = 4;

// Given matrix
int[,] matrix = {{2, 3, 5},
                {-1, 7,0},
                {8, 10, 0}};

// Function Call
mElementsWithMaxSumUtil(matrix, M, N);
}
}

// This code is contributed by Princi Singh
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to select m elements
// having maximum sum
function mElementsWithMaxSum(matrix, M,  block, dp)
{

    // Base case
    if (block == matrix.length)
        return 0;

    // If precomputed subproblem occurred
    if (dp[block][M] != -1)
        return dp[block][M];

    // Either skip the current row
    var ans = mElementsWithMaxSum(matrix, M,
                                   block + 1, dp);

    // Iterate through all the possible
    // segments of current row
    for(var i = 0;
            i < matrix[block].length; i++)
    {
        for(var j = i;
                j < matrix[block].length; j++)
        {

            // Check if it is possible to select
            // elements from i to j
            if (j - i + 1 <= M)
            {

                // Compuete the sum of i to j as
                // calculated
                ans = Math.max(ans, matrix[block][j] -
                         ((i - 1) >= 0 ?
                         matrix[block][i - 1] : 0) +
                         mElementsWithMaxSum(matrix,
                                             M - j +
                                             i - 1,
                                         block + 1, dp));
            }
        }
    }

    // Store the computed answer and return
    return dp[block][M] = ans;
}

// Function to precompute the prefix sum
// for every row of the matrix
function preComputing(matrix, N)
{

    // Preprocessing to calculate sum from i to j
    for(var i = 0; i < N; i++)
    {
        for(var j = 0; j < matrix[i].length; j++)
        {
            matrix[i][j] = (j > 0 ?
                  matrix[i][j - 1] : 0) +
                  matrix[i][j];
        }
    }
}

// Utility function to select m elements having
// maximum sum
function mElementsWithMaxSumUtil(matrix, M, N)
{

    // Preprocessing step
    preComputing(matrix, N);

    // Initialize dp array with -1
    var dp = Array.from(Array(N+5), ()=> Array(M+5).fill(-1));

    // Stores maximum sum of M elements
    var sum = mElementsWithMaxSum(matrix, M,
                                0, dp);

    document.write( sum);
}

// Driver Code
// Given N
var N = 3;
// Given M
var M = 4;
// Given matrix
var matrix = [ [ 2, 3, 5 ],
                               [ -1, 7 ],
                               [ 8, 10 ] ];
// Function call
mElementsWithMaxSumUtil(matrix, M, N);

// This code is contributed by noob2000.
</script>
```

****Output:** 

```
30
```** 

*****时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)***