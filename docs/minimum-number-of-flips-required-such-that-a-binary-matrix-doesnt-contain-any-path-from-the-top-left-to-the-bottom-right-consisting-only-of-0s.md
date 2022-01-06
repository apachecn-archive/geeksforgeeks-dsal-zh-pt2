# 所需的最小翻转次数，使得二进制矩阵不包含从左上角到右下角的仅由 0 组成的任何路径

> 原文:[https://www . geesforgeks . org/最小翻转次数-要求这样-二进制矩阵不包含任何路径-从左上角到右下角-仅由 0 组成/](https://www.geeksforgeeks.org/minimum-number-of-flips-required-such-that-a-binary-matrix-doesnt-contain-any-path-from-the-top-left-to-the-bottom-right-consisting-only-of-0s/)

给定维度为 **N*M** 的[二进制矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/) **mat[][]** ，任务是从给定的二进制矩阵中找到所需的最小翻转次数，使得不存在从左上角单元格到右下角单元格的仅由 **0s** 组成的任何路径。

**示例:**

> **输入:** mat[][] = {{0，1，0，0}，{0，1，0，0}，{0，1，0，0}，{0，0，0，0}}
> **输出:** 1
> **解释:**
> **操作 1:** 翻转(1，0)处的单元格将给定矩阵修改为:
> 0 1 0 0
> 1 0 0 0
> 0 1 0 0 0 0 0 因此，所需的翻转总数为 1。
> 
> **输入:** mat[][] = {{0，0，0，0}，{0，0，0，0}}
> **输出:** 2

**方法:**给定的问题可以使用给定矩阵上的 [DFS 遍历来解决，并且基于节点最多只存在**2 个**翻转的观察，使得不存在从左上角单元格到右下角单元格的仅由 **0s** 组成的任何路径。其思想是执行从左上角单元格到右下角单元格的](https://www.geeksforgeeks.org/depth-first-traversal-dfs-on-a-2d-array/) [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，最多翻转一条路径，并打印成功的 DFS 调用次数作为结果。按照以下步骤解决问题:

*   初始化一个[函数](https://www.geeksforgeeks.org/functions-in-c/)，假设 **DFS(mat，I，j，N，M)** ，该函数将当前单元格、给定矩阵及其大小作为[参数](https://www.geeksforgeeks.org/parameter-passing-techniques-in-c-cpp/)，并执行以下步骤:
    *   如果当前单元格到达单元格**(N-1，M-1)**，则返回**真**。
    *   将 **(i，j)** 处的单元格值更新为 **1** 。
    *   [递归调用当前单元格所有四个方向的](https://www.geeksforgeeks.org/recursive-functions/)DFS 函数，即 **(i + 1，j)** 、 **(i，j + 1)** 、**(I–1，j)** 和 **(i，j–1)**如果存在的话。
*   如果来自单元格 **(0，0)** 的 DFS 调用返回**假**，则不存在从左上角到右下角的由 **0s** 组成的单元格的路径。因此打印 **0** 作为结果，[从功能](https://www.geeksforgeeks.org/return-statement-in-c-cpp-with-examples/)返回。
*   同样，如果来自单元格 **(0，0)** 的 DFS 调用返回**假**，那么从左上角到右下角的单元格只存在一条由 **0s** 组成的路径。因此打印 **1** 作为结果并从该功能返回。
*   否则，打印 **2** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// The four direction coordinates changes
// from the current cell
int direction[][2] = { { -1, 0 }, { 0, 1 },
                       { 0, -1 }, { 1, 0 } };

// Function that returns true if there
// exists any path from the top-left to
// the bottom-right cell of 0s
bool dfs(vector<vector<int> >& matrix,
         int i, int j, int N, int M)
{

    // If the bottom-right cell is
    // reached
    if (i == N - 1 and j == M - 1) {
        return true;
    }

    // Update the cell to 1
    matrix[i][j] = 1;

    // Traverse in all four directions
    for (int k = 0; k < 4; k++) {

        // Find the new coordinates
        int newX = i + direction[k][0];
        int newY = j + direction[k][1];

        // If the new cell is valid
        if (newX >= 0 and newX < N
            and newY >= 0 and newY < M
            and matrix[newX][newY] == 0) {

            // Recursively call DFS
            if (dfs(matrix, newX,
                    newY, N, M)) {

                // If path exists, then
                // return true
                return true;
            }
        }
    }

    // Return false, if there doesn't
    // exists any such path
    return false;
}

// Function to flip the minimum number
// of cells such that there doesn't
// exists any such path from (0, 0) to
// (N - 1, M - 1) cell consisting of 0s
int solve(vector<vector<int> >& matrix)
{

    int N = matrix.size();
    int M = matrix[0].size();

    // Case 1: If no such path exists
    // already
    if (!dfs(matrix, 0, 0, N, M)) {
        return 0;
    }

    // Case 2: If there exists only
    // one path
    if (!dfs(matrix, 0, 0, N, M)) {
        return 1;
    }

    // Case 3: If there exists two-path
    return 2;
}

// Driver Code
int main()
{
    vector<vector<int> > mat = {
        { 0, 1, 0, 0 },
        { 0, 1, 0, 0 },
        { 0, 0, 0, 0 }
    };
    cout << solve(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// The four direction coordinates changes
// from the current cell
static int[][] direction = { { -1, 0 }, { 0, 1 },
                             { 0, -1 }, { 1, 0 } };

// Function that returns true if there
// exists any path from the top-left to
// the bottom-right cell of 0s
static boolean dfs(int matrix[][], int i, int j,
                   int N, int M)
{

    // If the bottom-right cell is
    // reached
    if (i == N - 1 && j == M - 1)
    {
        return true;
    }

    // Update the cell to 1
    matrix[i][j] = 1;

    // Traverse in all four directions
    for(int k = 0; k < 4; k++)
    {

        // Find the new coordinates
        int newX = i + direction[k][0];
        int newY = j + direction[k][1];

        // If the new cell is valid
        if (newX >= 0 && newX < N && newY >= 0 &&
            newY < M && matrix[newX][newY] == 0)
        {

            // Recursively call DFS
            if (dfs(matrix, newX, newY, N, M))
            {

                // If path exists, then
                // return true
                return true;
            }
        }
    }

    // Return false, if there doesn't
    // exists any such path
    return false;
}

// Function to flip the minimum number
// of cells such that there doesn't
// exists any such path from (0, 0) to
// (N - 1, M - 1) cell consisting of 0s
static int solve(int[][] matrix)
{
    int N = matrix.length;
    int M = matrix[0].length;

    // Case 1: If no such path exists
    // already
    if (!dfs(matrix, 0, 0, N, M))
    {
        return 0;
    }

    // Case 2: If there exists only
    // one path
    if (!dfs(matrix, 0, 0, N, M))
    {
        return 1;
    }

    // Case 3: If there exists two-path
    return 2;
}

// Driver code
public static void main(String[] args)
{
    int[][] mat = { { 0, 1, 0, 0 },
                    { 0, 1, 0, 0 },
                    { 0, 0, 0, 0 } };

    System.out.println(solve(mat));
}
}

// This code is contributed by MuskanKalra1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# The four direction coordinates changes
# from the current cell
direction = [ [ -1, 0 ], [ 0, 1 ],
              [ 0, -1 ],[ 1, 0 ] ]

# Function that returns true if there
# exists any path from the top-left to
# the bottom-right cell of 0s
def dfs(i, j, N, M):

    global matrix

    # If the bottom-right cell is
    # reached
    if (i == N - 1 and j == M - 1):
        return True

    # Update the cell to 1
    matrix[i][j] = 1

    # Traverse in all four directions
    for k in range(4):

        # Find the new coordinates
        newX = i + direction[k][0]
        newY = j + direction[k][1]

        # If the new cell is valid
        if (newX >= 0 and newX < N and
            newY >= 0 and newY < M and
            matrix[newX][newY] == 0):

            # Recursively call DFS
            if (dfs(newX, newY, N, M)):

                # If path exists, then
                # return true
                return True

    # Return false, if there doesn't
    # exists any such path
    return False

# Function to flip the minimum number
# of cells such that there doesn't
# exists any such path from (0, 0) to
# (N - 1, M - 1) cell consisting of 0s
def solve():

    global matrix
    N = len(matrix)
    M = len(matrix[0])

    # Case 1: If no such path exists
    # already
    if (not dfs(0, 0, N, M)):
        return 0

    # Case 2: If there exists only
    # one path
    if (not dfs(0, 0, N, M)):
        return 1

    # Case 3: If there exists two-path
    return 2

# Driver Code
if __name__ == '__main__':

    matrix = [ [ 0, 1, 0, 0 ],
               [ 0, 1, 0, 0 ],
               [ 0, 0, 0, 0 ] ]

    print(solve())

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// The four direction coordinates changes
// from the current cell
static int[,] direction = { { -1, 0 }, { 0, 1 },
                            { 0, -1 }, { 1, 0 } };

// Function that returns true if there
// exists any path from the top-left to
// the bottom-right cell of 0s
static bool dfs(int [,]matrix, int i, int j,
                int N, int M)
{

    // If the bottom-right cell is
    // reached
    if (i == N - 1 && j == M - 1)
    {
        return true;
    }

    // Update the cell to 1
    matrix[i, j] = 1;

    // Traverse in all four directions
    for(int k = 0; k < 4; k++)
    {

        // Find the new coordinates
        int newX = i + direction[k, 0];
        int newY = j + direction[k, 1];

        // If the new cell is valid
        if (newX >= 0 && newX < N && newY >= 0 &&
            newY < M && matrix[newX, newY] == 0)
        {

            // Recursively call DFS
            if (dfs(matrix, newX, newY, N, M))
            {

                // If path exists, then
                // return true
                return true;
            }
        }
    }

    // Return false, if there doesn't
    // exists any such path
    return false;
}

// Function to flip the minimum number
// of cells such that there doesn't
// exists any such path from (0, 0) to
// (N - 1, M - 1) cell consisting of 0s
static int solve(int[,] matrix)
{
    int N = matrix.GetLength(0);
    int M = matrix.GetLength(1);

    // Case 1: If no such path exists
    // already
    if (!dfs(matrix, 0, 0, N, M))
    {
        return 0;
    }

    // Case 2: If there exists only
    // one path
    if (!dfs(matrix, 0, 0, N, M))
    {
        return 1;
    }

    // Case 3: If there exists two-path
    return 2;
}

// Driver code
public static void Main(String[] args)
{
    int[,] mat = { { 0, 1, 0, 0 },
                   { 0, 1, 0, 0 },
                   { 0, 0, 0, 0 } };

    Console.WriteLine(solve(mat));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// The four direction coordinates changes
// from the current cell
let direction = [ [ -1, 0 ], [ 0, 1 ],
                       [ 0, -1 ], [ 1, 0 ] ];

// Function that returns true if there
// exists any path from the top-left to
// the bottom-right cell of 0s
function dfs(matrix, i, j, N, M)
{

    // If the bottom-right cell is
    // reached
    if (i == N - 1 && j == M - 1) {
        return true;
    }

    // Update the cell to 1
    matrix[i][j] = 1;

    // Traverse in all four directions
    for (let k = 0; k < 4; k++) {

        // Find the new coordinates
        let newX = i + direction[k][0];
        let newY = j + direction[k][1];

        // If the new cell is valid
        if (newX >= 0 && newX < N
            && newY >= 0 && newY < M
            && matrix[newX][newY] == 0) {

            // Recursively call DFS
            if (dfs(matrix, newX,
                    newY, N, M)) {

                // If path exists, then
                // return true
                return true;
            }
        }
    }

    // Return false, if there doesn't
    // exists any such path
    return false;
}

// Function to flip the minimum number
// of cells such that there doesn't
// exists any such path from (0, 0) to
// (N - 1, M - 1) cell consisting of 0s
function solve(matrix)
{

    let N = matrix.length;
    let M = matrix[0].length;

    // Case 1: If no such path exists
    // already
    if (!dfs(matrix, 0, 0, N, M)) {
        return 0;
    }

    // Case 2: If there exists only
    // one path
    if (!dfs(matrix, 0, 0, N, M)) {
        return 1;
    }

    // Case 3: If there exists two-path
    return 2;
}

// Driver Code
    let mat = [
        [ 0, 1, 0, 0 ],
        [ 0, 1, 0, 0 ],
        [ 0, 0, 0, 0 ]
    ];
    document.write(solve(mat));

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(1)*