# 最大化从左上角单元格到给定矩阵所有其他单元格的路径和

> 原文:[https://www . geesforgeks . org/maximize-path-sum-从左上角单元格到给定矩阵的所有其他单元格/](https://www.geeksforgeeks.org/maximize-path-sum-from-top-left-cell-to-all-other-cells-of-a-given-matrix/)

给定维度为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)、 **mat[][]** ，任务是找到从左上角单元格 **(0，0)** 到给定矩阵所有其他单元格的最大路径和。任何单元格 **(i，j)** 唯一可能的移动是 **(i + 1，j)** 和 **(i，j + 1)** 。

**示例:**

> **输入:** mat[][] = {{3，2，1}，{6，5，4}，{7，8，9}}
> **输出:**
> 3 5 6
> 9 14 18
> 16 24 33
> **说明:**
> 从(0，0)到(0，1)的路径，最大和为(0，0) → (0，1)
> 从(0，0)到(1)的路径 0)最大和为(0，0) → (1，0)
> 从(0，0)到(1，1)最大和为(0，0) → (1，0) → (1，1)
> 从(0，0)到(1，2)最大和为(0，0) → (1，0) → (1，2)
> 从(0，0)到(2，0)最大和为(0，0) → (2，0)】 0) → (1，0) → (2，0) → (2，1)
> 从(0，0)到(2，2)的路径最大和为(0，0) → (1，0) → (2，0) → (2，1) → (2，2)
> 
> **输入:** mat[][] = {{10，20，30}，{40，50，40}，{70，80，80}}
> **输出:**
> 10 30 60
> 50 100 140
> 120 200 280

**方法:**使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。下面是解决问题的递归关系。

> **递归关系:**
> 路径总和(I，j) = mat[i][j] + max(路径总和(I–1，j)，路径总和(I，j–1))
> 其中 i > 0 和 j > 0
> 
> **基本情况:**
> **如果 i = 0 且 j = 0:** 返回 mat[0][0]
> **如果 i = 0:** 返回 mat[i][j] +路径总和(I，j–1)
> **如果 j = 0:** 返回 mat[i][j] +路径总和(I–1，j)

按照以下步骤解决问题:

1.  初始化矩阵 **dp[][]** ， **dp[i][j]** 存储从 **(0，0)** 到 **(i，j)** 的最大路径和。
2.  利用上述递推关系计算 **dp[i][j]** 的值。
3.  最后打印 **dp[][]** 矩阵的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
#define SZ 100

// Function to get the maximum path
// sum from top-left cell to all
// other cells of the given matrix
void pathSum(const int mat[SZ][SZ],
             int N, int M)
{

    // Store the maximum path sum
    int dp[N][M];

    // Initialize the value
    // of dp[i][j] to 0.
    memset(dp, 0, sizeof(dp));

    // Base case
    dp[0][0] = mat[0][0];
    for (int i = 1; i < N; i++) {
        dp[i][0] = mat[i][0]
                   + dp[i - 1][0];
    }

    for (int j = 1; j < M; j++) {
        dp[0][j] = mat[0][j]
                   + dp[0][j - 1];
    }

    // Compute the value of dp[i][j]
    // using the recurrence relation
    for (int i = 1; i < N; i++) {
        for (int j = 1; j < M; j++) {
            dp[i][j] = mat[i][j]
                       + max(dp[i - 1][j],
                             dp[i][j - 1]);
        }
    }

    // Print maximum path sum from
    // the top-left cell
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            cout << dp[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    int mat[SZ][SZ]
        = { { 3, 2, 1 },
            { 6, 5, 4 },
            { 7, 8, 9 } };
    int N = 3;
    int M = 3;

    pathSum(mat, N, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

static final int SZ = 100;

// Function to get the maximum path
// sum from top-left cell to all
// other cells of the given matrix
static void pathSum(int [][]mat,
                    int N, int M)
{
  // Store the maximum path sum
  int [][]dp = new int[N][M];

  // Base case
  dp[0][0] = mat[0][0];

  for (int i = 1; i < N; i++)
  {
    dp[i][0] = mat[i][0] +
               dp[i - 1][0];
  }

  for (int j = 1; j < M; j++)
  {
    dp[0][j] = mat[0][j] +
               dp[0][j - 1];
  }

  // Compute the value of dp[i][j]
  // using the recurrence relation
  for (int i = 1; i < N; i++)
  {
    for (int j = 1; j < M; j++)
    {
      dp[i][j] = mat[i][j] +
                 Math.max(dp[i - 1][j],
                          dp[i][j - 1]);
    }
  }

  // Print maximum path sum from
  // the top-left cell
  for (int i = 0; i < N; i++)
  {
    for (int j = 0; j < M; j++)
    {
      System.out.print(dp[i][j] + " ");
    }
    System.out.println();
  }
}

// Driver Code
public static void main(String[] args)
{
  int mat[][] = {{3, 2, 1},
                 {6, 5, 4},
                 {7, 8, 9}};
  int N = 3;
  int M = 3;
  pathSum(mat, N, M);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to get the maximum path
# sum from top-left cell to all
# other cells of the given matrix
def pathSum(mat, N, M):

    # Store the maximum path sum
    # Initialize the value
    # of dp[i][j] to 0.
    dp = [[0 for x in range(M)]
             for y in range(N)]

    # Base case
    dp[0][0] = mat[0][0]
    for i in range(1, N):
        dp[i][0] = (mat[i][0] +
                    dp[i - 1][0])

    for j in range(1, M):
        dp[0][j] = (mat[0][j] +
                    dp[0][j - 1])

    # Compute the value of dp[i][j]
    # using the recurrence relation
    for i in range(1, N):
        for j in range(1, M):
            dp[i][j] = (mat[i][j] +
                        max(dp[i - 1][j],
                            dp[i][j - 1]))

    # Print maximum path sum
    # from the top-left cell
    for i in range(N):
        for j in range(M):
            print(dp[i][j],
                  end = " ")
        print()

# Driver code
if __name__ == '__main__':

    mat = [[3, 2, 1],
           [6, 5, 4],
           [7, 8, 9]]
    N = 3
    M = 3
    pathSum(mat, N, M)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

static readonly int SZ = 100;

// Function to get the maximum path
// sum from top-left cell to all
// other cells of the given matrix
static void pathSum(int [,]mat,
                    int N, int M)
{
  // Store the maximum path
  // sum
  int [,]dp = new int[N, M];

  // Base case
  dp[0, 0] = mat[0, 0];

  for (int i = 1; i < N; i++)
  {
    dp[i, 0] = mat[i, 0] +
               dp[i - 1, 0];
  }

  for (int j = 1; j < M; j++)
  {
    dp[0, j] = mat[0, j] +
               dp[0, j - 1];
  }

  // Compute the value of dp[i,j]
  // using the recurrence relation
  for (int i = 1; i < N; i++)
  {
    for (int j = 1; j < M; j++)
    {
      dp[i, j] = mat[i,j] +
                Math.Max(dp[i - 1, j],
                          dp[i, j - 1]);
    }
  }

  // Print maximum path sum from
  // the top-left cell
  for (int i = 0; i < N; i++)
  {
    for (int j = 0; j < M; j++)
    {
      Console.Write(dp[i, j] + " ");
    }
    Console.WriteLine();
  }
}

// Driver Code
public static void Main(String[] args)
{
  int [,]mat = {{3, 2, 1},
                {6, 5, 4},
                {7, 8, 9}};
  int N = 3;
  int M = 3;
  pathSum(mat, N, M);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

let SZ = 100;

// Function to get the maximum path
// sum from top-left cell to all
// other cells of the given matrix
function pathSum(mat, N, M)
{
  // Store the maximum path sum
  let dp = new Array(N);
  // Loop to create 2D array using 1D array
    for (var i = 0; i < dp.length; i++) {
        dp[i] = new Array(2);
    }

  // Base case
  dp[0][0] = mat[0][0];

  for (let i = 1; i < N; i++)
  {
    dp[i][0] = mat[i][0] +
               dp[i - 1][0];
  }

  for (let j = 1; j < M; j++)
  {
    dp[0][j] = mat[0][j] +
               dp[0][j - 1];
  }

  // Compute the value of dp[i][j]
  // using the recurrence relation
  for (let i = 1; i < N; i++)
  {
    for (let j = 1; j < M; j++)
    {
      dp[i][j] = mat[i][j] +
                 Math.max(dp[i - 1][j],
                          dp[i][j - 1]);
    }
  }

  // Print maximum path sum from
  // the top-left cell
  for (let i = 0; i < N; i++)
  {
    for (let j = 0; j < M; j++)
    {
      document.write(dp[i][j] + " ");
    }
    document.write("<br/>");
  }
}

// Driver Code

    let mat = [[3, 2, 1],
                 [6, 5, 4],
                 [7, 8, 9]];
  let N = 3;
  let M = 3;
  pathSum(mat, N, M);

</script>
```

**Output:** 

```
3 5 6 
9 14 18 
16 24 33
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*