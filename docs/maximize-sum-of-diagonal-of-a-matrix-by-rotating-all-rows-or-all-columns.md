# 通过旋转所有行或所有列最大化矩阵对角线的和

> 原文:[https://www . geesforgeks . org/通过旋转所有行或所有列来最大化矩阵的对角线总和/](https://www.geeksforgeeks.org/maximize-sum-of-diagonal-of-a-matrix-by-rotating-all-rows-or-all-columns/)

给定尺寸为 **N * N** 的正方形[矩阵](https://www.geeksforgeeks.org/matrix/)、 **mat[][]** ，任务是通过将矩阵的所有行或所有列旋转一个正整数，从给定矩阵中找到对角线元素的最大[和。](https://www.geeksforgeeks.org/efficiently-compute-sums-of-diagonals-of-a-matrix/)

**示例:**

> **输入:** mat[][] = { {1，1，2}，{ 2，1，2 }，{ 1，2，2 } }
> **输出:** 6
> **解释:**
> 将矩阵的所有列旋转 1 会将 mat[][]修改为{ {2，1，2 }，{ 1，2，2 }，{ 1，1，2 } }。
> 因此，矩阵对角元素之和= 2 + 2 + 2 = 6，这是最大可能。
> 
> **输入:** A[][] = { { -1，2 }，{ -1，3 } }
> T3】输出: 2

**方法:**思想是以所有可能的方式旋转矩阵的所有行和列，并计算得到的最大和。按照以下步骤解决问题:

*   初始化一个变量，比如说**最大对角线数**通过旋转矩阵的所有行或列来存储矩阵对角线元素的最大可能[和](https://www.geeksforgeeks.org/efficiently-compute-sums-of-diagonals-of-a-matrix/)。
*   将矩阵的所有行在**【0，N-1】**范围内旋转一个正整数，并更新**最大对角线数**的值。
*   将矩阵的所有列在**【0，N-1】**范围内旋转一个正整数，并更新**最大对角线数**的值。
*   最后，打印**maxdiansalsum**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;
#define N 3

// Function to find maximum sum of diagonal elements
// of matrix by rotating either rows or columns
int findMaximumDiagonalSumOMatrixf(int A[][N])
{

    // Stores maximum diagonal sum of elements
    // of matrix by rotating rows or columns
    int maxDiagonalSum = INT_MIN;

    // Rotate all the columns by an integer
    // in the range [0, N - 1]
    for (int i = 0; i < N; i++) {

        // Stores sum of diagonal elements
        // of the matrix
        int curr = 0;

        // Calculate sum of diagonal
        // elements of the matrix
        for (int j = 0; j < N; j++) {

            // Update curr
            curr += A[j][(i + j) % N];
        }

        // Update maxDiagonalSum
        maxDiagonalSum = max(maxDiagonalSum,
                                      curr);
    }

    // Rotate all the rows by an integer
    // in the range [0, N - 1]
    for (int i = 0; i < N; i++) {

        // Stores sum of diagonal elements
        // of the matrix
        int curr = 0;

        // Calculate sum of diagonal
        // elements of the matrix
        for (int j = 0; j < N; j++) {

            // Update curr
            curr += A[(i + j) % N][j];
        }

        // Update maxDiagonalSum
        maxDiagonalSum = max(maxDiagonalSum,
                                      curr);
    }

    return maxDiagonalSum;
}

// Driver code
int main()
{

    int mat[N][N] = { { 1, 1, 2 },
                    { 2, 1, 2 },
                    { 1, 2, 2 } };

    cout<< findMaximumDiagonalSumOMatrixf(mat);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static int N = 3;

// Function to find maximum sum of
// diagonal elements of matrix by
// rotating either rows or columns
static int findMaximumDiagonalSumOMatrixf(int A[][])
{

    // Stores maximum diagonal sum of elements
    // of matrix by rotating rows or columns
    int maxDiagonalSum = Integer.MIN_VALUE;

    // Rotate all the columns by an integer
    // in the range [0, N - 1]
    for(int i = 0; i < N; i++)
    {

        // Stores sum of diagonal elements
        // of the matrix
        int curr = 0;

        // Calculate sum of diagonal
        // elements of the matrix
        for(int j = 0; j < N; j++)
        {

            // Update curr
            curr += A[j][(i + j) % N];
        }

        // Update maxDiagonalSum
        maxDiagonalSum = Math.max(maxDiagonalSum,
                                  curr);
    }

    // Rotate all the rows by an integer
    // in the range [0, N - 1]
    for(int i = 0; i < N; i++)
    {

        // Stores sum of diagonal elements
        // of the matrix
        int curr = 0;

        // Calculate sum of diagonal
        // elements of the matrix
        for(int j = 0; j < N; j++)
        {

            // Update curr
            curr += A[(i + j) % N][j];
        }

        // Update maxDiagonalSum
        maxDiagonalSum = Math.max(maxDiagonalSum,
                                  curr);
    }
    return maxDiagonalSum;
}

// Driver Code
public static void main(String[] args)
{
    int[][] mat = { { 1, 1, 2 },
                    { 2, 1, 2 },
                    { 1, 2, 2 } };

    System.out.println(
        findMaximumDiagonalSumOMatrixf(mat));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

N = 3

# Function to find maximum sum of diagonal
# elements of matrix by rotating either
# rows or columns
def findMaximumDiagonalSumOMatrixf(A):

    # Stores maximum diagonal sum of elements
    # of matrix by rotating rows or columns
    maxDiagonalSum = -sys.maxsize - 1

    # Rotate all the columns by an integer
    # in the range [0, N - 1]
    for i in range(N):     

        # Stores sum of diagonal elements
        # of the matrix
        curr = 0

        # Calculate sum of diagonal
        # elements of the matrix
        for j in range(N):

            # Update curr
            curr += A[j][(i + j) % N]

        # Update maxDiagonalSum
        maxDiagonalSum = max(maxDiagonalSum,
                             curr)

    # Rotate all the rows by an integer
    # in the range [0, N - 1]
    for i in range(N):

        # Stores sum of diagonal elements
        # of the matrix
        curr = 0

        # Calculate sum of diagonal
        # elements of the matrix
        for j in range(N):         

            # Update curr
            curr += A[(i + j) % N][j]

        # Update maxDiagonalSum
        maxDiagonalSum = max(maxDiagonalSum,
                             curr)

    return maxDiagonalSum

# Driver code
if __name__ == "__main__":

    mat = [ [ 1, 1, 2 ],
            [ 2, 1, 2 ],
            [ 1, 2, 2 ] ]

    print(findMaximumDiagonalSumOMatrixf(mat))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

static int N = 3;

// Function to find maximum sum of
// diagonal elements of matrix by
// rotating either rows or columns
static int findMaximumDiagonalSumOMatrixf(int[,] A)
{

    // Stores maximum diagonal sum of elements
    // of matrix by rotating rows or columns
    int maxDiagonalSum = Int32.MinValue;

    // Rotate all the columns by an integer
    // in the range [0, N - 1]
    for(int i = 0; i < N; i++)
    {

        // Stores sum of diagonal elements
        // of the matrix
        int curr = 0;

        // Calculate sum of diagonal
        // elements of the matrix
        for(int j = 0; j < N; j++)
        {

            // Update curr
            curr += A[j, (i + j) % N];
        }

        // Update maxDiagonalSum
        maxDiagonalSum = Math.Max(maxDiagonalSum,
                                  curr);
    }

    // Rotate all the rows by an integer
    // in the range [0, N - 1]
    for(int i = 0; i < N; i++)
    {

        // Stores sum of diagonal elements
        // of the matrix
        int curr = 0;

        // Calculate sum of diagonal
        // elements of the matrix
        for(int j = 0; j < N; j++)
        {

            // Update curr
            curr += A[(i + j) % N, j];
        }

        // Update maxDiagonalSum
        maxDiagonalSum = Math.Max(maxDiagonalSum,
                                  curr);
    }
    return maxDiagonalSum;
}

// Driver Code
public static void Main()
{
    int[,] mat = { { 1, 1, 2 },
                   { 2, 1, 2 },
                   { 1, 2, 2 } };

    Console.Write(findMaximumDiagonalSumOMatrixf(mat));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach
let N = 3;

// Function to find maximum sum of
// diagonal elements of matrix by
// rotating either rows or columns
function findMaximumDiagonalSumOMatrixf(A)
{

    // Stores maximum diagonal sum of elements
    // of matrix by rotating rows or columns
    let maxDiagonalSum = Number.MIN_VALUE;

    // Rotate all the columns by an integer
    // in the range [0, N - 1]
    for(let i = 0; i < N; i++)
    {

        // Stores sum of diagonal elements
        // of the matrix
        let curr = 0;

        // Calculate sum of diagonal
        // elements of the matrix
        for(let j = 0; j < N; j++)
        {

            // Update curr
            curr += A[j][(i + j) % N];
        }

        // Update maxDiagonalSum
        maxDiagonalSum = Math.max(maxDiagonalSum,
                                  curr);
    }

    // Rotate all the rows by an integer
    // in the range [0, N - 1]
    for(let i = 0; i < N; i++)
    {

        // Stores sum of diagonal elements
        // of the matrix
        let curr = 0;

        // Calculate sum of diagonal
        // elements of the matrix
        for(let j = 0; j < N; j++)
        {

            // Update curr
            curr += A[(i + j) % N][j];
        }

        // Update maxDiagonalSum
        maxDiagonalSum = Math.max(maxDiagonalSum,
                                  curr);
    }
    return maxDiagonalSum;
}

    // Driver Code
    let mat = [[ 1, 1, 2 ],
                    [ 2, 1, 2 ],
                    [ 1, 2, 2 ]];

    document.write(
        findMaximumDiagonalSumOMatrixf(mat));

// This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*