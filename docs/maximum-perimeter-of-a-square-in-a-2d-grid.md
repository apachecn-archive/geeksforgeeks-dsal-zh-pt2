# 2D 网格中正方形的最大周长

> 原文:[https://www . geesforgeks . org/2d 网格中正方形的最大周长/](https://www.geeksforgeeks.org/maximum-perimeter-of-a-square-in-a-2d-grid/)

给定一个整数矩阵 **mat[][]** ，大小为 **N * M** 。任务是找出矩阵中正方形的最大周长。正方形的周长被定义为位于正方形边上的所有值的总和。
**例:**

> **输入:** mat[][] = {
> {-3，-2，7}，
> {-4，6，0}，
> {-4，8，2}}
> **输出:** 16
> 最大周长平方为
> {6，0}
> {8，2}
> **输入:** mat[][] = {
> {1，1，0}，
> {1，1

**天真的方法:**一个简单的解决方案是在给定的矩阵**mat【】【】**内生成所有可能的正方形，然后找到它们的周长并从中取最大值。
**高效进场:**

*   要找到正方形的周长，边的长度应该是已知的。
*   这里，长度被描述为特定行和列上元素的总和。
*   将创建大小为 **N * M** 的两个矩阵，这两个矩阵将存储原始矩阵的行的前缀和以及列的前缀和，从而可以在恒定时间内计算边的长度。
*   将有两个嵌套的循环，一个从 **1** 到 **N** ，另一个从 **1** 到 **M** 找到方块的左上角(左上角)，一个循环是**min(N–I，M–j)**，它将告诉我们方块的大小，并确保索引不会超过矩阵的大小。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the prefix sum of the
// rows and the columns of the given matrix
void prefix_calculate(vector<vector<int> >& A,
                      vector<vector<int> >& row,
                      vector<vector<int> >& col)
{

    // Number of rows and cols
    int n = (int)A.size();
    int m = (int)A[0].size();

    // First column of the row prefix array
    for (int i = 0; i < n; ++i) {
        row[i][0] = A[i][0];
    }

    // Update the prefix sum for the rows
    for (int i = 0; i < n; ++i) {
        for (int j = 1; j < m; ++j) {
            row[i][j] = row[i][j - 1]
                        + A[i][j];
        }
    }

    // First row of the column prefix array
    for (int i = 0; i < m; ++i) {
        col[0][i] = A[0][i];
    }

    // Update the prefix sum for the columns
    for (int i = 0; i < m; ++i) {
        for (int j = 1; j < n; ++j) {
            col[j][i] = A[j][i]
                        + col[j - 1][i];
        }
    }
}

// Function to return the perimeter
// of the square having top-left corner
// at (i, j) and size k
int perimeter(int i, int j, int k,
              vector<vector<int> >& row,
              vector<vector<int> >& col,
              vector<vector<int> >& A)
{

    // i and j represent the top left
    // corner of the square and
    // k is the size
    int row_s, col_s;

    // Get the upper row sum
    if (j == 0)
        row_s = 0;
    else
        row_s = row[i][j - 1];

    // Get the left column sum
    if (i == 0)
        col_s = 0;
    else
        col_s = col[i - 1][j];

    int upper_row = row[i][j + k] - row_s;
    int left_col = col[i + k][j] - col_s;

    // At the distance of k in
    // both direction
    if (j == 0)
        row_s = 0;
    else
        row_s = row[i + k][j - 1];

    if (i == 0)
        col_s = 0;
    else
        col_s = col[i - 1][j + k];

    int lower_row = row[i + k][j + k] - row_s;
    int right_col = col[i + k][j + k] - col_s;

    // The perimeter will be
    // sum of all the values
    int sum = upper_row
              + lower_row
              + left_col
              + right_col;

    // Since all the corners are
    // included twice, they need to
    // be subtract from the sum
    sum -= (A[i][j]
            + A[i + k][j]
            + A[i][j + k]
            + A[i + k][j + k]);

    return sum;
}

// Function to return the maximum perimeter
// of a square in the given matrix
int maxPerimeter(vector<vector<int> >& A)
{

    // Number of rows and cols
    int n = (int)A.size();
    int m = (int)A[0].size();

    vector<vector<int> > row(n, vector<int>(m, 0));
    vector<vector<int> > col(n, vector<int>(m, 0));

    // Function call to calculate
    // the prefix sum of rows and cols
    prefix_calculate(A, row, col);

    // To store the maximum perimeter
    int maxPer = 0;

    // Nested loops to choose the top-left
    // corner of the square
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {

            // Loop for the size of the square
            for (int k = 0; k < min(n - i, m - j); ++k) {

                // Get the perimeter of the current square
                int perimtr = perimeter(i, j, k, row, col, A);

                // Update the maximum perimeter so far
                maxPer = max(maxPer, perimtr);
            }
        }
    }

    return maxPer;
}

// Driver code
int main()
{
    vector<vector<int> > A = {
        { 1, 1, 0 },
        { 1, 1, 1 },
        { 0, 1, 1 }
    };

    cout << maxPerimeter(A);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to calculate the prefix sum of the
// rows and the columns of the given matrix
static void prefix_calculate(int [][] A,
                    int [][] row,
                    int [][] col)
{

    // Number of rows and cols
    int n = (int)A.length;
    int m = (int)A[0].length;

    // First column of the row prefix array
    for (int i = 0; i < n; ++i)
    {
        row[i][0] = A[i][0];
    }

    // Update the prefix sum for the rows
    for (int i = 0; i < n; ++i)
    {
        for (int j = 1; j < m; ++j)
        {
            row[i][j] = row[i][j - 1]
                        + A[i][j];
        }
    }

    // First row of the column prefix array
    for (int i = 0; i < m; ++i)
    {
        col[0][i] = A[0][i];
    }

    // Update the prefix sum for the columns
    for (int i = 0; i < m; ++i)
    {
        for (int j = 1; j < n; ++j)
        {
            col[j][i] = A[j][i]
                        + col[j - 1][i];
        }
    }
}

// Function to return the perimeter
// of the square having top-left corner
// at (i, j) and size k
static int perimeter(int i, int j, int k,
                int [][] row, int [][] col,
                int [][] A)
{

    // i and j represent the top left
    // corner of the square and
    // k is the size
    int row_s, col_s;

    // Get the upper row sum
    if (j == 0)
        row_s = 0;
    else
        row_s = row[i][j - 1];

    // Get the left column sum
    if (i == 0)
        col_s = 0;
    else
        col_s = col[i - 1][j];

    int upper_row = row[i][j + k] - row_s;
    int left_col = col[i + k][j] - col_s;

    // At the distance of k in
    // both direction
    if (j == 0)
        row_s = 0;
    else
        row_s = row[i + k][j - 1];

    if (i == 0)
        col_s = 0;
    else
        col_s = col[i - 1][j + k];

    int lower_row = row[i + k][j + k] - row_s;
    int right_col = col[i + k][j + k] - col_s;

    // The perimeter will be
    // sum of all the values
    int sum = upper_row + lower_row +
                left_col + right_col;

    // Since all the corners are
    // included twice, they need to
    // be subtract from the sum
    sum -= (A[i][j] + A[i + k][j] +
             A[i][j + k] + A[i + k][j + k]);

    return sum;
}

// Function to return the maximum perimeter
// of a square in the given matrix
static int maxPerimeter(int [][] A)
{

    // Number of rows and cols
    int n = (int)A.length;
    int m = (int)A[0].length;

    int [][] row = new int[n][m];
    int [][] col = new int[n][m];

    // Function call to calculate
    // the prefix sum of rows and cols
    prefix_calculate(A, row, col);

    // To store the maximum perimeter
    int maxPer = 0;

    // Nested loops to choose the top-left
    // corner of the square
    for (int i = 0; i < n; ++i)
    {
        for (int j = 0; j < m; ++j)
        {

            // Loop for the size of the square
            for (int k = 0; k < Math.min(n - i, m - j); ++k)
            {

                // Get the perimeter of the current square
                int perimtr = perimeter(i, j, k,
                                        row, col, A);

                // Update the maximum perimeter so far
                maxPer = Math.max(maxPer, perimtr);
            }
        }
    }

    return maxPer;
}

// Driver code
public static void main(String[] args)
{
    int [][] A = {
        { 1, 1, 0 },
        { 1, 1, 1 },
        { 0, 1, 1 }
    };

    System.out.print(maxPerimeter(A));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to calculate the prefix sum of the
# rows and the columns of the given matrix
def prefix_calculate(A, row, col):

    # Number of rows and cols
    n = len(A)
    m = len(A[0])

    # First column of the row prefix array
    for i in range(n):
        row[i][0] = A[i][0]

    # Update the prefix sum for the rows
    for i in range(n):
        for j in range(1, m):
            row[i][j] = row[i][j - 1]+ A[i][j]

    # First row of the column prefix array
    for i in range(m):
        col[0][i] = A[0][i]

    # Update the prefix sum for the columns
    for i in range(m):
        for j in range(1, m):
            col[j][i] = A[j][i] + col[j - 1][i]

# Function to return the perimeter
# of the square having top-left corner
# at (i, j) and size k
def perimeter(i, j, k, row, col, A):

    # i and j represent the top left
    # corner of the square and
    # k is the size
    row_s, col_s = 0, 0

    # Get the upper row sum
    if (j == 0):
        row_s = 0
    else:
        row_s = row[i][j - 1]

    # Get the left column sum
    if (i == 0):
        col_s = 0
    else:
        col_s = col[i - 1][j]

    upper_row = row[i][j + k] - row_s
    left_col = col[i + k][j] - col_s

    # At the distance of k in
    # both direction
    if (j == 0):
        row_s = 0
    else:
        row_s = row[i + k][j - 1]

    if (i == 0):
        col_s = 0
    else:
        col_s = col[i - 1][j + k]

    lower_row = row[i + k][j + k] - row_s
    right_col = col[i + k][j + k] - col_s

    # The perimeter will be
    # sum of all the values
    sum = upper_row + lower_row + \
           left_col + right_col

    # Since all the corners are
    # included twice, they need to
    # be subtract from the sum
    sum -= (A[i][j] + A[i + k][j] + \
            A[i][j + k] + A[i + k][j + k])

    return sum

# Function to return the maximum perimeter
# of a square in the given matrix
def maxPerimeter(A):

    # Number of rows and cols
    n = len(A)
    m = len(A[0])

    row = [[0 for i in range(m)]
              for i in range(n)]
    col = [[0 for i in range(m)]
              for i in range(n)]

    # Function call to calculate
    # the prefix sum of rows and cols
    prefix_calculate(A, row, col)

    # To store the maximum perimeter
    maxPer = 0

    # Nested loops to choose the top-left
    # corner of the square
    for i in range(n):
        for j in range(m):

            # Loop for the size of the square
            for k in range(min(n - i, m - j)):

                # Get the perimeter of the current square
                perimtr = perimeter(i, j, k,
                                    row, col, A)

                # Update the maximum perimeter so far
                maxPer = max(maxPer, perimtr)

    return maxPer

# Driver code
A = [[ 1, 1, 0 ],
     [ 1, 1, 1 ],
     [ 0, 1, 1 ]]

print(maxPerimeter(A))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to calculate the prefix sum of the
// rows and the columns of the given matrix
static void prefix_calculate(int [,] A,
                    int [,] row,
                    int [,] col)
{

    // Number of rows and cols
    int n = (int)A.GetLength(0);
    int m = (int)A.GetLength(1);

    // First column of the row prefix array
    for (int i = 0; i < n; ++i)
    {
        row[i, 0] = A[i, 0];
    }

    // Update the prefix sum for the rows
    for (int i = 0; i < n; ++i)
    {
        for (int j = 1; j < m; ++j)
        {
            row[i, j] = row[i, j - 1]
                        + A[i, j];
        }
    }

    // First row of the column prefix array
    for (int i = 0; i < m; ++i)
    {
        col[0, i] = A[0, i];
    }

    // Update the prefix sum for the columns
    for (int i = 0; i < m; ++i)
    {
        for (int j = 1; j < n; ++j)
        {
            col[j, i] = A[j, i]
                        + col[j - 1, i];
        }
    }
}

// Function to return the perimeter
// of the square having top-left corner
// at (i, j) and size k
static int perimeter(int i, int j, int k,
                int [,] row, int [,] col,
                int [,] A)
{

    // i and j represent the top left
    // corner of the square and
    // k is the size
    int row_s, col_s;

    // Get the upper row sum
    if (j == 0)
        row_s = 0;
    else
        row_s = row[i, j - 1];

    // Get the left column sum
    if (i == 0)
        col_s = 0;
    else
        col_s = col[i - 1, j];

    int upper_row = row[i, j + k] - row_s;
    int left_col = col[i + k, j] - col_s;

    // At the distance of k in
    // both direction
    if (j == 0)
        row_s = 0;
    else
        row_s = row[i + k, j - 1];

    if (i == 0)
        col_s = 0;
    else
        col_s = col[i - 1, j + k];

    int lower_row = row[i + k, j + k] - row_s;
    int right_col = col[i + k, j + k] - col_s;

    // The perimeter will be
    // sum of all the values
    int sum = upper_row + lower_row +
                left_col + right_col;

    // Since all the corners are
    // included twice, they need to
    // be subtract from the sum
    sum -= (A[i, j] + A[i + k, j] +
            A[i, j + k] + A[i + k, j + k]);

    return sum;
}

// Function to return the maximum perimeter
// of a square in the given matrix
static int maxPerimeter(int [,] A)
{

    // Number of rows and cols
    int n = (int)A.GetLength(0);
    int m = (int)A.GetLength(1);

    int [,] row = new int[n, m];
    int [,] col = new int[n, m];

    // Function call to calculate
    // the prefix sum of rows and cols
    prefix_calculate(A, row, col);

    // To store the maximum perimeter
    int maxPer = 0;

    // Nested loops to choose the top-left
    // corner of the square
    for (int i = 0; i < n; ++i)
    {
        for (int j = 0; j < m; ++j)
        {

            // Loop for the size of the square
            for (int k = 0; k < Math.Min(n - i, m - j); ++k)
            {

                // Get the perimeter of the current square
                int perimtr = perimeter(i, j, k,
                                        row, col, A);

                // Update the maximum perimeter so far
                maxPer = Math.Max(maxPer, perimtr);
            }
        }
    }
    return maxPer;
}

// Driver code
public static void Main(String[] args)
{
    int [,] A = {{ 1, 1, 0 },
                { 1, 1, 1 },
                { 0, 1, 1 }};

    Console.Write(maxPerimeter(A));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to calculate the prefix sum of the
// rows and the columns of the given matrix
function prefix_calculate(A, row, col)
{

    // Number of rows and cols
    let n = A.length;
    let m = A[0].length;

    // First column of the row prefix array
    for (let i = 0; i < n; ++i)
    {
        row[i][0] = A[i][0];
    }

    // Update the prefix sum for the rows
    for (let i = 0; i < n; ++i)
    {
        for (let j = 1; j < m; ++j)
        {
            row[i][j] = row[i][j - 1]
                        + A[i][j];
        }
    }

    // First row of the column prefix array
    for (let i = 0; i < m; ++i)
    {
        col[0][i] = A[0][i];
    }

    // Update the prefix sum for the columns
    for (let i = 0; i < m; ++i)
    {
        for (let j = 1; j < n; ++j)
        {
            col[j][i] = A[j][i]
                        + col[j - 1][i];
        }
    }
}

// Function to return the perimeter
// of the square having top-left corner
// at (i, j) and size k
function perimeter(i,j,k,row,col,A)
{
    // i and j represent the top left
    // corner of the square and
    // k is the size
    let row_s, col_s;

    // Get the upper row sum
    if (j == 0)
        row_s = 0;
    else
        row_s = row[i][j - 1];

    // Get the left column sum
    if (i == 0)
        col_s = 0;
    else
        col_s = col[i - 1][j];

    let upper_row = row[i][j + k] - row_s;
    let left_col = col[i + k][j] - col_s;

    // At the distance of k in
    // both direction
    if (j == 0)
        row_s = 0;
    else
        row_s = row[i + k][j - 1];

    if (i == 0)
        col_s = 0;
    else
        col_s = col[i - 1][j + k];

    let lower_row = row[i + k][j + k] - row_s;
    let right_col = col[i + k][j + k] - col_s;

    // The perimeter will be
    // sum of all the values
    let sum = upper_row + lower_row +
                left_col + right_col;

    // Since all the corners are
    // included twice, they need to
    // be subtract from the sum
    sum -= (A[i][j] + A[i + k][j] +
             A[i][j + k] + A[i + k][j + k]);

    return sum;
}

// Function to return the maximum perimeter
// of a square in the given matrix
function maxPerimeter(A)
{
    // Number of rows and cols
    let n = A.length;
    let m = A[0].length;

    let row = new Array(n);
    let col = new Array(n);

    for(let i=0;i<n;i++)
    {
        row[i]=new Array(m);
        col[i]=new Array(m);
    }

    // Function call to calculate
    // the prefix sum of rows and cols
    prefix_calculate(A, row, col);

    // To store the maximum perimeter
    let maxPer = 0;

    // Nested loops to choose the top-left
    // corner of the square
    for (let i = 0; i < n; ++i)
    {
        for (let j = 0; j < m; ++j)
        {

            // Loop for the size of the square
            for (let k = 0; k < Math.min(n - i, m - j); ++k)
            {

                // Get the perimeter of the current square
                let perimtr = perimeter(i, j, k,
                                        row, col, A);

                // Update the maximum perimeter so far
                maxPer = Math.max(maxPer, perimtr);
            }
        }
    }

    return maxPer;
}

// Driver code
let A = [[1, 1, 0 ],[1, 1, 1],[0, 1, 1]];
document.write(maxPerimeter(A));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(N * M * min(N，M))