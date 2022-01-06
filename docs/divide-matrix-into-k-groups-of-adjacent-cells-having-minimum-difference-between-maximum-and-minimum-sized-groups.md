# 将矩阵分成 K 组相邻单元，最大和最小尺寸组之间的差异最小

> 原文:[https://www . geeksforgeeks . org/将矩阵分成 k 个相邻单元组，最大和最小尺寸组之间的差异最小/](https://www.geeksforgeeks.org/divide-matrix-into-k-groups-of-adjacent-cells-having-minimum-difference-between-maximum-and-minimum-sized-groups/)

给定矩阵的 **N** 行和 **M** 列，任务是首先使用 **K** 整数填充矩阵单元格，这样:

*   每组单元格由一个整数表示。
*   包含最大和最小单元数的组之间的差异应该最小。
*   同一组的所有单元格应该是连续的，即对于任何组，两个相邻的单元格应该遵循规则**| x<sub>I+1</sub>–x<sub>I</sub>|+| y<sub>I+1</sub>–y<sub>I</sub>| = 1**。

**示例:**

> **输入:** N = 5，M = 5，K = 6
> **输出:**
> 1 1 1 1 1 1
> 3 2 2 2 2
> 3 3 4
> 5 5 5 4
> 5 6 6 6 6
> **说明:**
> 以上矩阵遵循以上所有条件，将矩阵划分为 K 个不同的组。
> 
> **输入:** N = 2，M = 3，K = 3
> **输出:**
> 1 1 2
> 3 3 2
> **说明:**
> 对于制作三组的矩阵每个都要有大小二的组。
> 因此，为了减少包含最大和最小单元数的组与所有矩阵单元之间的差异，使用 K 个不同的组使同一组的所有相邻元素遵循| x<sub>I+1</sub>–x<sub>I</sub>|+| y<sub>I+1</sub>–y<sub>I</sub>| = 1。

**进场:**以下是步骤:

*   创建大小为 **N * M** 的矩阵。
*   为了减少包含最大和最小单元数的组之间的差异，用至少 **(N*M)/ K** 单元填充所有部分。
*   剩余部分将包含 **(N * M)/ K + 1** 个单元。
*   为了遵循给定的规则，[遍历矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)，并相应地用不同的部分填充矩阵。
*   完成上述步骤后打印矩阵。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to fill the matrix with
// the given conditions
void fillMatrix(int** mat, int& row,
                int& col, int sizeOfpart,
                int noOfPart, int& start,
                int m, int& flag)
{

    // Count of parts with size sizeOfPart
    for (int i = 0; i < noOfPart; ++i) {

        int count = 0;

        while (count < sizeOfpart) {

            // Assigning the cell
            // with no of groups
            mat[row][col] = start;

            // Update row
            if (col == m - 1
                && flag == 1) {
                row++;
                col = m;
                flag = 0;
            }
            else if (col == 0
                     && flag == 0) {
                row++;
                col = -1;
                flag = 1;
            }

            // Update col
            if (flag == 1) {
                col++;
            }
            else {
                col--;
            }

            // Increment count
            count++;
        }

        // For new group increment start
        start++;
    }
}

// Function to return the reference of
// the matrix to be filled
int** findMatrix(int N, int M, int k)
{

    // Create matrix of size N*M
    int** mat = (int**)malloc(
        N * sizeof(int*));

    for (int i = 0; i < N; ++i) {
        mat[i] = (int*)malloc(
            M * sizeof(int));
    }

    // Starting index of the matrix
    int row = 0, col = 0;

    // Size of one group
    int size = (N * M) / k;
    int rem = (N * M) % k;

    // Element to assigned to matrix
    int start = 1, flag = 1;

    // Fill the matrix that have rem
    // no of parts with size size + 1
    fillMatrix(mat, row, col, size + 1,
               rem, start, M, flag);

    // Fill the remaining number of parts
    // with each part size is 'size'
    fillMatrix(mat, row, col, size,
               k - rem, start, M, flag);

    // Return the matrix
    return mat;
}

// Function to print the matrix
void printMatrix(int** mat, int N,
                 int M)
{
    // Traverse the rows
    for (int i = 0; i < N; ++i) {

        // Traverse the columns
        for (int j = 0; j < M; ++j) {
            cout << mat[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    // Given N, M, K
    int N = 5, M = 5, K = 6;

    // Function Call
    int** mat = findMatrix(N, M, K);

    // Function Call to print matrix
    printMatrix(mat, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int N, M;
static int [][]mat;
static int row, col, start, flag;

// Function to fill the matrix with
// the given conditions
static void fillMatrix(int sizeOfpart,
                       int noOfPart,
                       int m)
{

    // Count of parts with size sizeOfPart
    for(int i = 0; i < noOfPart; ++i)
    {
        int count = 0;

        while (count < sizeOfpart)
        {

            // Assigning the cell
            // with no of groups
            mat[row][col] = start;

            // Update row
            if (col == m - 1 && flag == 1)
            {
                row++;
                col = m;
                flag = 0;
            }
            else if (col == 0 && flag == 0)
            {
                row++;
                col = -1;
                flag = 1;
            }

            // Update col
            if (flag == 1)
            {
                col++;
            }
            else
            {
                col--;
            }

            // Increment count
            count++;
        }

        // For new group increment start
        start++;
    }
}

// Function to return the reference of
// the matrix to be filled
static void findMatrix(int k)
{

    // Create matrix of size N*M
    mat = new int[M][N];

    // Starting index of the matrix
    row = 0;
    col = 0;

    // Size of one group
    int size = (N * M) / k;
    int rem = (N * M) % k;

    // Element to assigned to matrix
    start = 1;
    flag = 1;

    // Fill the matrix that have rem
    // no of parts with size size + 1
    fillMatrix(size + 1, rem, M);

    // Fill the remaining number of parts
    // with each part size is 'size'
    fillMatrix(size, k - rem, M);
}

// Function to print the matrix
static void printMatrix()
{

    // Traverse the rows
    for(int i = 0; i < N; ++i)
    {

        // Traverse the columns
        for(int j = 0; j < M; ++j)
        {
            System.out.print(mat[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given N, M, K
    N = 5;
    M = 5;
    int K = 6;

    // Function Call
    findMatrix(K);

    // Function Call to print matrix
    printMatrix();
}
}

// This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

static int N, M;
static int [,]mat;
static int row, col,
           start, flag;

// Function to fill the
// matrix with the given
// conditions
static void fillMatrix(int sizeOfpart,
                       int noOfPart,
                       int m)
{   
  // Count of parts with size
  // sizeOfPart
  for(int i = 0;
          i < noOfPart; ++i)
  {
    int count = 0;

    while (count < sizeOfpart)
    {
      // Assigning the cell
      // with no of groups
      mat[row, col] = start;

      // Update row
      if (col == m - 1 &&
          flag == 1)
      {
        row++;
        col = m;
        flag = 0;
      }
      else if (col == 0 &&
               flag == 0)
      {
        row++;
        col = -1;
        flag = 1;
      }

      // Update col
      if (flag == 1)
      {
        col++;
      }
      else
      {
        col--;
      }

      // Increment count
      count++;
    }

    // For new group increment
    // start
    start++;
  }
}

// Function to return the
// reference of the matrix
// to be filled
static void findMatrix(int k)
{   
  // Create matrix of
  // size N*M
  mat = new int[M, N];

  // Starting index of the
  // matrix
  row = 0;
  col = 0;

  // Size of one group
  int size = (N * M) / k;
  int rem = (N * M) % k;

  // Element to assigned to
  // matrix
  start = 1;
  flag = 1;

  // Fill the matrix that have
  // rem no of parts with size
  // size + 1
  fillMatrix(size + 1,
             rem, M);

  // Fill the remaining number
  // of parts with each part
  // size is 'size'
  fillMatrix(size, k - rem, M);
}

// Function to print the
// matrix
static void printMatrix()
{   
  // Traverse the rows
  for(int i = 0; i < N; ++i)
  {
    // Traverse the columns
    for(int j = 0; j < M; ++j)
    {
      Console.Write(mat[i, j] +
                    " ");
    }
    Console.WriteLine();
  }
}

// Driver Code
public static void Main(String[] args)
{   
  // Given N, M, K
  N = 5;
  M = 5;
  int K = 6;

  // Function Call
  findMatrix(K);

  // Function Call to
  // print matrix
  printMatrix();
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
1 1 1 1 1 
3 2 2 2 2 
3 3 3 4 4 
5 5 5 4 4 
5 6 6 6 6

```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*