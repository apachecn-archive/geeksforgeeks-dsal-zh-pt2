# 通过给定单元之一的矩阵从左上角到右下角的最大路径和

> 原文:[https://www . geeksforgeeks . org/矩阵从左上方到右下方通过给定单元之一的最大路径总和/](https://www.geeksforgeeks.org/maximum-path-sum-from-top-left-to-bottom-right-of-a-matrix-passing-through-one-of-the-given-cells/)

给定尺寸为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】**和尺寸为 **Q** 的单元格**坐标【】【】【】**的一组坐标，任务是找到从左上角单元格 **(1，1)** 到右下角单元格 **(N，M)** 的路径的最大和，使得该路径应该包含来自数组**坐标的至少一个坐标从矩阵的任何单元 **(i，j)** 允许的唯一移动是 **(i + 1，j)** 或 **(i，j + 1)** 。**

**示例:**

> **输入:** mat[][ = {{1，2，3}，{4，5，6}，{7，8，9}}，坐标[][] = {{1，2}，{2，2}}
> **输出:** 27
> **解释:**
> 具有最大值的路径由:
> (1，1)—>(2，1)—>(2，2)—>(3，2)—**给出
> 以上路径经过坐标(2，2)。因此，路径的和由(1 + 4 + 5 + 8 + 9) = 27 给出，这是最大路径。**
> 
> **输入:** mat[][] = {{1，3}，{6，7}，{8，9}}，坐标[][2] = {{1，1}}
> **输出:** 24

**天真方法:**解决给定问题最简单的方法是[生成从矩阵的左上角到右下角单元格的所有可能路径](https://www.geeksforgeeks.org/print-all-possible-paths-from-top-left-to-bottom-right-of-a-mxn-matrix/)并打印该路径的单元格的最大和，该路径中至少有一个坐标位于数组**坐标【】【】【】**中。

***时间复杂度:** O((N + M)！)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。考虑两个矩阵**开始[][]** 和**结束[][]** ，使得**开始[i][j]** 表示从单元 **(1，1)** 到单元 **(i，j)** 和**结束[i][j]** 表示从单元 **(i，j)** 到单元 **(N，M)**的最大路径和因此，对于任何坐标 **(X，Y)**，最大路径和可以计算为:

> 开始[X][Y] +结束[x][y]-mat[x][y]

按照以下步骤解决问题:

*   初始化两个矩阵，比如尺寸为 **N*M** 的 **start[][]** 和 **end[][]** ，使得 **start[i][j]** 表示从单元格 **(1，1)** 到单元格 **(i，j)** 的最大路径和 **end[i][j]** 表示从单元格 **(i，j)** 到单元格**的最大路径和**
*   初始化一个变量，比如说**和**作为 [INT_MIN](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) ，存储结果的最大和。
*   使用本文[中讨论的自下而上方法](https://www.geeksforgeeks.org/maximum-sum-path-in-a-matrix-from-top-left-to-bottom-right/)计算从单元 **(1，1)** 到每个单元 **(i，j)** 的最大路径和，并将其存储在矩阵 **start[][]** 中。
*   使用本文[中讨论的自上而下方法](https://www.geeksforgeeks.org/maximum-sum-path-in-a-matrix-from-top-left-to-bottom-right/)计算从单元 **(N，M)** 到每个单元 **(i，j)** 的最大路径和，并将其存储在矩阵 **end[][]** 中。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **坐标[][]** ，对于每个坐标 **(X，Y)** 更新 **ans** 的值为 **ans** 和**的最大值(开始[X][Y] +结束[X][Y]–mat[X][Y])**。
*   完成上述步骤后，打印**和**的值作为结果的最大和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Stores the maximum path sum from the
// cell (1, 1) to (N, M)
int start[3][3];

// Stores the maximum path sum from the
// cell (j, j) to (N, M)
int ending[3][3];

// Function to find the maximum path
// sum from the cell (1, 1) to (N, M)
void calculateStart(int n, int m)
{
    // Traverse the first row
    for (int i = 1; i < m; ++i) {
        start[0][i] += start[0][i - 1];
    }

    // Traverse the first column
    for (int i = 1; i < n; ++i) {
        start[i][0] += start[i - 1][0];
    }

    // Traverse the matrix
    for (int i = 1; i < n; ++i) {

        for (int j = 1; j < m; ++j) {

            // Update the value of
            // start[i][j]
            start[i][j] += max(start[i - 1][j],
                               start[i][j - 1]);
        }
    }
}

// Function to find the maximum path
// sum from the cell (j, j) to (N, M)
void calculateEnd(int n, int m)
{
    // Traverse the last row
    for (int i = n - 2; i >= 0; --i) {
        ending[i][m - 1] += ending[i + 1][m - 1];
    }

    // Traverse the last column
    for (int i = m - 2; i >= 0; --i) {
        ending[n - 1][i] += ending[n - 1][i + 1];
    }

    // Traverse the matrix
    for (int i = n - 2; i >= 0; --i) {

        for (int j = m - 2; j >= 0; --j) {

            // Update the value of
            // ending[i][j]
            ending[i][j] += max(ending[i + 1][j],
                                ending[i][j + 1]);
        }
    }
}

// Function to find the maximum path sum
// from the top-left to the bottom right
// cell such that path contains one of
// the cells in the array coordinates[][]
void maximumPathSum(int mat[][3], int n,
                    int m, int q,
                    int coordinates[][2])
{
    // Initialize the start and the
    // end matrices
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            start[i][j] = mat[i][j];
            ending[i][j] = mat[i][j];
        }
    }

    // Calculate the start matrix
    calculateStart(n, m);

    // Calculate the end matrix
    calculateEnd(n, m);

    // Stores the maximum path sum
    int ans = 0;

    // Traverse the coordinates
    for (int i = 0; i < q; ++i) {

        int X = coordinates[i][0] - 1;
        int Y = coordinates[i][1] - 1;

        // Update the value of ans
        ans = max(ans, start[X][Y]
                           + ending[X][Y]
                           - mat[X][Y]);
    }

    // Print the resultant maximum
    // sum path value
    cout << ans;
}

// Drive Code
int main()
{

    int mat[][3] = { { 1, 2, 3 },
                     { 4, 5, 6 },
                     { 7, 8, 9 } };
    int N = 3;
    int M = 3;
    int Q = 2;
    int coordinates[][2] = { { 1, 2 },
                             { 2, 2 } };

    maximumPathSum(mat, N, M, Q,
                   coordinates);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Stores the maximum path sum from the
// cell (1, 1) to (N, M)
static int start[][] = new int[3][3];

// Stores the maximum path sum from the
// cell (j, j) to (N, M)
static int ending[][] = new int[3][3];

// Function to find the maximum path
// sum from the cell (1, 1) to (N, M)
static void calculateStart(int n, int m)
{

    // Traverse the first row
    for(int i = 1; i < m; ++i)
    {
        start[0][i] += start[0][i - 1];
    }

    // Traverse the first column
    for(int i = 1; i < n; ++i)
    {
        start[i][0] += start[i - 1][0];
    }

    // Traverse the matrix
    for(int i = 1; i < n; ++i)
    {
        for(int j = 1; j < m; ++j)
        {

            // Update the value of
            // start[i][j]
            start[i][j] += Math.max(start[i - 1][j],
                                 start[i][j - 1]);
        }
    }
}

// Function to find the maximum path
// sum from the cell (j, j) to (N, M)
static void calculateEnd(int n, int m)
{

    // Traverse the last row
    for(int i = n - 2; i >= 0; --i)
    {
        ending[i][m - 1] += ending[i + 1][m - 1];
    }

    // Traverse the last column
    for(int i = m - 2; i >= 0; --i)
    {
        ending[n - 1][i] += ending[n - 1][i + 1];
    }

    // Traverse the matrix
    for(int i = n - 2; i >= 0; --i)
    {
        for(int j = m - 2; j >= 0; --j)
        {

            // Update the value of
            // ending[i][j]
            ending[i][j] += Math.max(ending[i + 1][j],
                                  ending[i][j + 1]);
        }
    }
}

// Function to find the maximum path sum
// from the top-left to the bottom right
// cell such that path contains one of
// the cells in the array coordinates[][]
static void maximumPathSum(int mat[][], int n,
                           int m, int q,
                           int coordinates[][])
{

    // Initialize the start and the
    // end matrices
    for(int i = 0; i < n; ++i)
    {
        for(int j = 0; j < m; ++j)
        {
            start[i][j] = mat[i][j];
            ending[i][j] = mat[i][j];
        }
    }

    // Calculate the start matrix
    calculateStart(n, m);

    // Calculate the end matrix
    calculateEnd(n, m);

    // Stores the maximum path sum
    int ans = 0;

    // Traverse the coordinates
    for(int i = 0; i < q; ++i)
    {
        int X = coordinates[i][0] - 1;
        int Y = coordinates[i][1] - 1;

        // Update the value of ans
        ans = Math.max(ans, start[X][Y] +
                           ending[X][Y] -
                           mat[X][Y]);
    }

    // Print the resultant maximum
    // sum path value
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    int mat[][] = { { 1, 2, 3 },
                    { 4, 5, 6 },
                    { 7, 8, 9 } };
    int N = 3;
    int M = 3;
    int Q = 2;
    int coordinates[][] = { { 1, 2 },
                            { 2, 2 } };

    maximumPathSum(mat, N, M, Q,
                   coordinates);
}   
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the maximum path sum from the
# cell (1, 1) to (N, M)
start = [[0 for i in range(3)]
            for j in range(3)]

# Stores the maximum path sum from the
# cell (j, j) to (N, M)
ending = [[0 for i in range(3)]
             for j in range(3)]

# Function to find the maximum path
# sum from the cell (1, 1) to (N, M)
def calculateStart(n, m):

    # Traverse the first row
    for i in range(1, m, 1):
        start[0][i] += start[0][i - 1]

    # Traverse the first column
    for i in range(1, n, 1):
        start[i][0] += start[i - 1][0]

    # Traverse the matrix
    for i in range(1, n, 1):
        for j in range(1, m, 1):

            # Update the value of
            # start[i][j]
            start[i][j] += max(start[i - 1][j],
                               start[i][j - 1])

# Function to find the maximum path
# sum from the cell (j, j) to (N, M)
def calculateEnd(n, m):

    # Traverse the last row
    i = n - 2

    while(i >= 0):
        ending[i][m - 1] += ending[i + 1][m - 1]
        i -= 1

    # Traverse the last column
    i = m - 2

    while(i >= 0):
        ending[n - 1][i] += ending[n - 1][i + 1]
        i -= 1

    # Traverse the matrix
    i = n - 2

    while(i >= 0):
        j = m - 2
        while(j >= 0):

            # Update the value of
            # ending[i][j]
            ending[i][j] += max(ending[i + 1][j],
                                ending[i][j + 1])
            j -= 1

        i -= 1

# Function to find the maximum path sum
# from the top-left to the bottom right
# cell such that path contains one of
# the cells in the array coordinates[][]
def maximumPathSum(mat, n, m, q, coordinates):

    # Initialize the start and the
    # end matrices
    for i in range(n):
        for j in range(m):
            start[i][j] = mat[i][j]
            ending[i][j] = mat[i][j]

    # Calculate the start matrix
    calculateStart(n, m)

    # Calculate the end matrix
    calculateEnd(n, m)

    # Stores the maximum path sum
    ans = 0

    # Traverse the coordinates
    for i in range(q):
        X = coordinates[i][0] - 1
        Y = coordinates[i][1] - 1

        # Update the value of ans
        ans = max(ans, start[X][Y] +
                      ending[X][Y] -
                         mat[X][Y])

    # Print the resultant maximum
    # sum path value
    print(ans)

# Driver Code
if __name__ == '__main__':

    mat = [ [ 1, 2, 3 ],
            [ 4, 5, 6 ],
            [ 7, 8, 9 ] ]
    N = 3
    M = 3
    Q = 2

    coordinates = [ [ 1, 2 ], [ 2, 2 ] ]

    maximumPathSum(mat, N, M, Q,coordinates)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Stores the maximum path sum from the
// cell (1, 1) to (N, M)
static int[,] start = new int[3, 3];

// Stores the maximum path sum from the
// cell (j, j) to (N, M)
static int[,] ending = new int[3, 3];

// Function to find the maximum path
// sum from the cell (1, 1) to (N, M)
static void calculateStart(int n, int m)
{

    // Traverse the first row
    for(int i = 1; i < m; ++i)
    {
        start[0, i] += start[0, i - 1];
    }

    // Traverse the first column
    for(int i = 1; i < n; ++i)
    {
        start[i, 0] += start[i - 1, 0];
    }

    // Traverse the matrix
    for(int i = 1; i < n; ++i)
    {
        for(int j = 1; j < m; ++j)
        {

            // Update the value of
            // start[i][j]
            start[i, j] += Math.Max(start[i - 1, j],
                                 start[i, j - 1]);
        }
    }
}

// Function to find the maximum path
// sum from the cell (j, j) to (N, M)
static void calculateEnd(int n, int m)
{

    // Traverse the last row
    for(int i = n - 2; i >= 0; --i)
    {
        ending[i, m - 1] += ending[i + 1, m - 1];
    }

    // Traverse the last column
    for(int i = m - 2; i >= 0; --i)
    {
        ending[n - 1, i] += ending[n - 1, i + 1];
    }

    // Traverse the matrix
    for(int i = n - 2; i >= 0; --i)
    {
        for(int j = m - 2; j >= 0; --j)
        {

            // Update the value of
            // ending[i][j]
            ending[i, j] += Math.Max(ending[i + 1, j],
                                  ending[i, j + 1]);
        }
    }
}

// Function to find the maximum path sum
// from the top-left to the bottom right
// cell such that path contains one of
// the cells in the array coordinates[][]
static void maximumPathSum(int[,] mat, int n,
                           int m, int q,
                           int[,] coordinates)
{

    // Initialize the start and the
    // end matrices
    for(int i = 0; i < n; ++i)
    {
        for(int j = 0; j < m; ++j)
        {
            start[i, j] = mat[i, j];
            ending[i, j] = mat[i, j];
        }
    }

    // Calculate the start matrix
    calculateStart(n, m);

    // Calculate the end matrix
    calculateEnd(n, m);

    // Stores the maximum path sum
    int ans = 0;

    // Traverse the coordinates
    for(int i = 0; i < q; ++i)
    {
        int X = coordinates[i, 0] - 1;
        int Y = coordinates[i, 1] - 1;

        // Update the value of ans
        ans = Math.Max(ans, start[X, Y] +
                           ending[X, Y] -
                           mat[X, Y]);
    }

    // Print the resultant maximum
    // sum path value
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    int[,] mat = { { 1, 2, 3 },
                    { 4, 5, 6 },
                    { 7, 8, 9 } };
    int N = 3;
    int M = 3;
    int Q = 2;
    int[,] coordinates = { { 1, 2 },
                            { 2, 2 } };

    maximumPathSum(mat, N, M, Q,
                   coordinates);
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Stores the maximum path sum from the
// cell (1, 1) to (N, M)
var start = Array.from(Array(3), ()=>Array(3));

// Stores the maximum path sum from the
// cell (j, j) to (N, M)
var ending = Array.from(Array(3), ()=>Array(3));

// Function to find the maximum path
// sum from the cell (1, 1) to (N, M)
function calculateStart(n, m)
{
    // Traverse the first row
    for (var i = 1; i < m; ++i) {
        start[0][i] += start[0][i - 1];
    }

    // Traverse the first column
    for (var i = 1; i < n; ++i) {
        start[i][0] += start[i - 1][0];
    }

    // Traverse the matrix
    for (var i = 1; i < n; ++i) {

        for (var j = 1; j < m; ++j) {

            // Update the value of
            // start[i][j]
            start[i][j] += Math.max(start[i - 1][j],
                               start[i][j - 1]);
        }
    }
}

// Function to find the maximum path
// sum from the cell (j, j) to (N, M)
function calculateEnd(n, m)
{
    // Traverse the last row
    for (var i = n - 2; i >= 0; --i) {
        ending[i][m - 1] += ending[i + 1][m - 1];
    }

    // Traverse the last column
    for (var i = m - 2; i >= 0; --i) {
        ending[n - 1][i] += ending[n - 1][i + 1];
    }

    // Traverse the matrix
    for (var i = n - 2; i >= 0; --i) {

        for (var j = m - 2; j >= 0; --j) {

            // Update the value of
            // ending[i][j]
            ending[i][j] += Math.max(ending[i + 1][j],
                                ending[i][j + 1]);
        }
    }
}

// Function to find the maximum path sum
// from the top-left to the bottom right
// cell such that path contains one of
// the cells in the array coordinates[][]
function maximumPathSum(mat, n, m, q, coordinates)
{
    // Initialize the start and the
    // end matrices
    for (var i = 0; i < n; ++i) {
        for (var j = 0; j < m; ++j) {
            start[i][j] = mat[i][j];
            ending[i][j] = mat[i][j];
        }
    }

    // Calculate the start matrix
    calculateStart(n, m);

    // Calculate the end matrix
    calculateEnd(n, m);

    // Stores the maximum path sum
    var ans = 0;

    // Traverse the coordinates
    for (var i = 0; i < q; ++i) {

        var X = coordinates[i][0] - 1;
        var Y = coordinates[i][1] - 1;

        // Update the value of ans
        ans = Math.max(ans, start[X][Y]
                           + ending[X][Y]
                           - mat[X][Y]);
    }

    // Print the resultant maximum
    // sum path value
    document.write( ans);
}

// Drive Code
var mat = [ [ 1, 2, 3 ],
                 [ 4, 5, 6 ],
                 [ 7, 8, 9 ] ];
var N = 3;
var M = 3;
var Q = 2;
var coordinates = [ [ 1, 2 ],
                         [ 2, 2 ] ];
maximumPathSum(mat, N, M, Q,
               coordinates);

</script>
```

**Output:** 

```
27
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*