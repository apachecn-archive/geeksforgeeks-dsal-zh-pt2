# 从左上角开始的所有子矩阵的按位异或的中值

> 原文:[https://www . geeksforgeeks . org/所有子矩阵的按位异或中值-从左上角开始/](https://www.geeksforgeeks.org/median-of-bitwise-xor-of-all-submatrices-starting-from-the-top-left-corner/)

给定一个大小为 **N * M** 的 [2D 矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**mat【】【】【】**，任务是从给定矩阵中找到所有可能子矩阵的[中值](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)，该矩阵在 **(0，0)** 处具有最左边的元素。

**示例:**

> **输入:** M[][] = { { 1，2 }，{ 2，3 } }
> **输出:** 2.5
> **解释:**
> 左上角为(0，0)最右下角为(0，0)的子矩阵按位异或为 mat[0][0] = 1。
> 左上角为(0，0)右下角为(0，1)的子矩阵按位异或为 mat[0][0] ^ mat[0][1] = 3。
> 左上角为(0，0)右下角为(1，0)的子矩阵按位异或为 mat[0][0] ^ mat[1][0] = 3。
> 左上角为(0，0)右下角为(1，1)的子矩阵按位异或为 mat[0][0]^ mat[1][0]^ mat[0][1]^ mat[1][1]= 2。
> 左上角为(2 + 3) / 2 = 2.5 的所有可能子矩阵按位异或的中值。
> 
> **输入:** M[][] = { { 1，5，2 }，{ 2，3，23 }，{ 7，43，13 } }
> T3】输出: 5

**方法:**问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)基于以下递归关系来解决

> DP[I][j]= DP[I-1][j-1]^ DP[I][j-1]^ DP[I-1][j]^ mat[I][j]
> 
> **mat[i][j]:** 存储左上角为(0，0)最右下角为(I，j)的子矩阵的按位异或。

按照以下步骤解决问题:

*   [初始化一个数组](https://www.geeksforgeeks.org/array-data-structure/)，比如**异或[]** ，存储所有可能的子矩阵的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，最左上角是 **(0，0)** 。
*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如 dp[][]，其中 dp[i][j]存储子矩阵的按位异或，子矩阵的左上角是 **(0，0)** ，最右下角是 **(i，j)** 。
*   使用[制表方法](https://www.geeksforgeeks.org/tabulation-vs-memoization/)填充 **dp[][]** 数组。
*   将 **dp[][]** 数组的所有元素存储到 **XOR[]** 中。
*   最后，[打印 XOR[]数组的中值](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to find the median of bitwise XOR
// of all the submatrix whose topmost leftmost
// corner is (0, 0)
double findMedXOR(int mat[][2], int N, int M)
{

    // dp[i][j]: Stores the bitwise XOR of
    // submatrix having top left corner
    // at (0, 0) and bottom right corner at (i, j)
    int dp[N][M];

    int med[N * M];

    dp[0][0] = mat[0][0];

    med[0] = dp[0][0];

    // Stores count of submatrix
    int len = 1;

    // Base Case
    for (int i = 1; i < N; i++) {

        dp[i][0]
            = dp[i - 1][0] ^ mat[i][0];
        med[len++] = dp[i][0];
    }

    // Base Case
    for (int i = 1; i < M; i++) {

        dp[0][i]
            = dp[0][i - 1] ^ mat[0][i];

        med[len++] = dp[0][i];
    }

    // Fill dp[][] using tabulation
    for (int i = 1; i < N; i++) {

        for (int j = 1; j < M; j++) {

            // Fill dp[i][j]
            dp[i][j] = dp[i - 1][j]
                       ^ dp[i][j - 1]
                       ^ dp[i - 1][j - 1]
                       ^ mat[i][j];

            med[len++] = dp[i][j];
        }
    }

    sort(med, med + len);

    if (len % 2 == 0) {

        return (med[(len / 2)]
                + med[(len / 2) - 1])
               / 2.0;
    }

    return med[len / 2];
}

// Driver Code
int main()
{

    int mat[][2] = { { 1, 2 }, { 2, 3 } };

    int N = sizeof(mat) / sizeof(mat[0]);
    int M = 2;
    cout << findMedXOR(mat, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to find the median of bitwise XOR
  // of all the submatrix whose topmost leftmost
  // corner is (0, 0)
  static double findMedXOR(int mat[][], int N, int M)
  {

    // dp[i][j]: Stores the bitwise XOR of
    // submatrix having top left corner
    // at (0, 0) and bottom right corner at (i, j)
    int dp[][] = new int[N][M];
    int med[] = new int[N * M];
    dp[0][0] = mat[0][0];
    med[0] = dp[0][0];

    // Stores count of submatrix
    int len = 1;

    // Base Case
    for (int i = 1; i < N; i++)
    {
      dp[i][0] = dp[i - 1][0] ^ mat[i][0];
      med[len++] = dp[i][0];
    }

    // Base Case
    for (int i = 1; i < M; i++)
    {

      dp[0][i] = dp[0][i - 1] ^ mat[0][i];
      med[len++] = dp[0][i];
    }

    // Fill dp[][] using tabulation
    for (int i = 1; i < N; i++)
    {
      for (int j = 1; j < M; j++)
      {

        // Fill dp[i][j]
        dp[i][j] = dp[i - 1][j]
          ^ dp[i][j - 1]
          ^ dp[i - 1][j - 1]
          ^ mat[i][j];

        med[len++] = dp[i][j];
      }
    }
    Arrays.sort(med);
    if (len % 2 == 0)
    {
      return (med[(len / 2)]
              + med[(len / 2) - 1])
        / 2.0;
    }
    return med[len / 2];
  }

  // Driver code
  public static void main(String[] args)
  {
    int mat[][] = { { 1, 2 }, { 2, 3 } };
    int N = mat.length;
    int M = 2;
    System.out.println(findMedXOR(mat, N, M));
  }
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find the median of bitwise XOR
# of all the submatrix whose topmost leftmost
# corner is (0, 0)
def findMedXOR(mat, N, M):

    # dp[i][j]: Stores the bitwise XOR of
    # submatrix having top left corner
    # at (0, 0) and bottom right corner at (i, j)
    dp = [[0 for i in range(M)] for j in range(N)];
    med = [0] * (N * M);
    dp[0][0] = mat[0][0];
    med[0] = dp[0][0];

    # Stores count of submatrix
    len = 1;

    # Base Case
    for i in range(1, N):
        dp[i][0] = dp[i - 1][0] ^ mat[i][0];
        med[len] = dp[i][0];
        len += 1;

    # Base Case
    for i in range(1, M):
        dp[0][i] = dp[0][i - 1] ^ mat[0][i];
        med[len] = dp[0][i];
        len += 1

    # Fill dp using tabulation
    for i in range(1, N):
        for j in range(1, M):

            # Fill dp[i][j]
            dp[i][j] = dp[i - 1][j] ^ dp[i][j - 1] ^ dp[i - 1][j - 1] ^ mat[i][j];
            med[len] = dp[i][j];
            len += 1

    med.sort();
    if (len % 2 == 0):
        return (med[(len // 2)] + med[(len // 2) - 1]) / 2.0;
    return med[len // 2];

# Driver code
if __name__ == '__main__':
    mat = [[1, 2], [2, 3]];
    N = len(mat[0]);
    M = 2;
    print(findMedXOR(mat, N, M));

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to find the median of bitwise XOR
  // of all the submatrix whose topmost leftmost
  // corner is (0, 0)
  static double findMedXOR(int [,]mat, int N, int M)
  {

    // dp[i,j]: Stores the bitwise XOR of
    // submatrix having top left corner
    // at (0, 0) and bottom right corner at (i, j)
    int [,]dp = new int[N, M];
    int []med = new int[N * M];
    dp[0, 0] = mat[0, 0];
    med[0] = dp[0, 0];

    // Stores count of submatrix
    int len = 1;

    // Base Case
    for (int i = 1; i < N; i++)
    {
      dp[i, 0] = dp[i - 1, 0] ^ mat[i, 0];
      med[len++] = dp[i, 0];
    }

    // Base Case
    for (int i = 1; i < M; i++)
    {

      dp[0, i] = dp[0, i - 1] ^ mat[0, i];
      med[len++] = dp[0, i];
    }

    // Fill [,]dp using tabulation
    for (int i = 1; i < N; i++)
    {
      for (int j = 1; j < M; j++)
      {

        // Fill dp[i,j]
        dp[i, j] = dp[i - 1, j]
          ^ dp[i, j - 1]
          ^ dp[i - 1, j - 1]
          ^ mat[i, j];

        med[len++] = dp[i, j];
      }
    }
    Array.Sort(med);
    if (len % 2 == 0)
    {
      return (med[(len / 2)]
              + med[(len / 2) - 1])
        / 2.0;
    }
    return med[len / 2];
  }

  // Driver code
  public static void Main(String[] args)
  {
    int [,]mat = { { 1, 2 }, { 2, 3 } };
    int N = mat.GetLength(0);
    int M = 2;
    Console.WriteLine(findMedXOR(mat, N, M));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the median of bitwise XOR
// of all the submatrix whose topmost leftmost
// corner is (0, 0)
function findMedXOR(mat, N, M)
{

    // dp[i][j]: Stores the bitwise XOR of
    // submatrix having top left corner
    // at (0, 0) and bottom right corner at (i, j)
    let dp = new Array(N);
    for (let i = 0; i < N; i++)
        dp[i] = new Array(M);

    let med = new Array(N * M);

    dp[0][0] = mat[0][0];

    med[0] = dp[0][0];

    // Stores count of submatrix
    let len = 1;

    // Base Case
    for (let i = 1; i < N; i++) {

        dp[i][0]
            = dp[i - 1][0] ^ mat[i][0];
        med[len++] = dp[i][0];
    }

    // Base Case
    for (let i = 1; i < M; i++) {

        dp[0][i]
            = dp[0][i - 1] ^ mat[0][i];

        med[len++] = dp[0][i];
    }

    // Fill dp[][] using tabulation
    for (let i = 1; i < N; i++) {

        for (let j = 1; j < M; j++) {

            // Fill dp[i][j]
            dp[i][j] = dp[i - 1][j]
                       ^ dp[i][j - 1]
                       ^ dp[i - 1][j - 1]
                       ^ mat[i][j];

            med[len++] = dp[i][j];
        }
    }

    med.sort();

    if (len % 2 == 0) {

        return (med[parseInt(len / 2)]
                + med[parseInt(len / 2) - 1])
               / 2.0;
    }

    return med[parseInt(len / 2)];
}

// Driver Code

    let mat = [ [ 1, 2 ], [ 2, 3 ] ];

    let N = mat.length;
    let M = 2;
    document.write(findMedXOR(mat, N, M));

</script>
```

**Output:** 

```
2.5
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*