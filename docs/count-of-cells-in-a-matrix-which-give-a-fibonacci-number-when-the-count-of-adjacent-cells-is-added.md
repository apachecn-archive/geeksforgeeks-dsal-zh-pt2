# 当相邻单元格的计数相加时给出斐波那契数的矩阵中单元格的计数

> 原文:[https://www . geeksforgeeks . org/矩阵中的细胞计数-增加相邻细胞计数时给出斐波那契数/](https://www.geeksforgeeks.org/count-of-cells-in-a-matrix-which-give-a-fibonacci-number-when-the-count-of-adjacent-cells-is-added/)

给定一个 **M x N** 矩阵 **mat[][]** 。任务是计算矩阵中好细胞的数量。如果单元格值和相邻单元格的数量之和是斐波那契数，则单元格是好的。
**例:**

> **输入:** mat[][] = {
> {1，2}，
> {3，4}}
> **输出:** 2
> 只有细胞 mat[0][0]和 mat[1][0]是好的。
> 即(1 + 2) = 3 和(3 + 2) = 5 都是斐波那契数。
> **输入:** mat[][] = {
> {1，0，5，3}，
> {2，17，5，6}，
> {5，8，15，11 } }；
> **输出:** 7

**方法:**迭代整个矩阵，并为每个单元找到相邻单元的计数。可以有 3 种类型的细胞，一种具有 2 个相邻细胞，一种具有 3 个相邻细胞，其余的具有 4 个相邻细胞。将此计数与当前单元格的值相加，并检查结果是否为斐波那契数。如果是，则增加计数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define M 3
#define N 4

// Function that returns true if
// x is a perfect square
bool isPerfectSquare(long double x)
{
    // Find floating point value of
    // square root of x
    long double sr = sqrt(x);

    // If square root is an integer
    return ((sr - floor(sr)) == 0);
}

// Function that returns true
// if n is a Fibonacci number
bool isFibonacci(int n)
{
    return isPerfectSquare(5 * n * n + 4)
           || isPerfectSquare(5 * n * n - 4);
}

// Function to return the count of good cells
int goodCells(int mat[M][N])
{

    // To store the required count
    int count = 0;
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {

            int sum = mat[i][j];

            // Corner cells of the matrix
            // have only 2 adjacent cells
            if ((i == 0 && j == 0)
                || (i == M - 1 && j == 0)
                || (i == 0 && j == N - 1)
                || (i == M - 1 && j == N - 1)) {
                sum += 2;
            }

            // All the boundary elements
            // except the corner elements
            // have only 3 adjacent cells
            else if (i == 0 || j == 0
                     || i == M - 1 || j == N - 1) {
                sum += 3;
            }

            // Rest of the elements have 4 adjacent cells
            else {
                sum += 4;
            }

            // If the sum is a Fibonacci number
            if (isFibonacci(sum))
                count++;
        }
    }

    return count;
}

// Driver code
int main()
{
    int mat[M][N] = { { 1, 0, 5, 3 },
                      { 2, 17, 5, 6 },
                      { 5, 8, 15, 11 } };
    cout << goodCells(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

static int M = 3;
static int N = 4;

// Function that returns true if
// x is a perfect square
static boolean isPerfectSquare(long x)
{
    // Find floating point value of
    // square root of x
    double sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function that returns true
// if n is a Fibonacci number
static boolean isFibonacci(int n)
{
    return isPerfectSquare(5 * n * n + 4)
        || isPerfectSquare(5 * n * n - 4);
}

// Function to return the count of good cells
static int goodCells(int mat[][])
{

    // To store the required count
    int count = 0;
    for (int i = 0; i < M; i++)
    {
        for (int j = 0; j < N; j++)
        {

            int sum = mat[i][j];

            // Corner cells of the matrix
            // have only 2 adjacent cells
            if ((i == 0 && j == 0)
                || (i == M - 1 && j == 0)
                || (i == 0 && j == N - 1)
                || (i == M - 1 && j == N - 1))
            {
                sum += 2;
            }

            // All the boundary elements
            // except the corner elements
            // have only 3 adjacent cells
            else if (i == 0 || j == 0
                    || i == M - 1 || j == N - 1)
            {
                sum += 3;
            }

            // Rest of the elements have 4 adjacent cells
            else
            {
                sum += 4;
            }

            // If the sum is a Fibonacci number
            if (isFibonacci(sum))
                count++;
        }
    }

    return count;
}

    // Driver code
    public static void main (String[] args)
    {
        int mat[][] = { { 1, 0, 5, 3 },
                    { 2, 17, 5, 6 },
                    { 5, 8, 15, 11 } };
        System.out.println( goodCells(mat));
    }
}

// This code is contributed by anuj_67..
```

## 计算机编程语言

```
# Python implementation of the approach
from math import ceil,sqrt,floor
M = 3
N = 4

# Function that returns true if
# x is a perfect square
def isPerfectSquare(x):

    # Find floating povalue of
    # square root of x
    sr = (sqrt(x))

    # If square root is an integer
    return ((sr - floor(sr)) == 0)

# Function that returns true
# if n is a Fibonacci number
def isFibonacci(n):
    return isPerfectSquare(5 * n * n + 4) or isPerfectSquare(5 * n * n - 4)

# Function to return the count of good cells
def goodCells(mat):

    # To store the required count
    count = 0
    for i in range(M):
        for j in range(N):

            sum = mat[i][j]

            # Corner cells of the matrix
            # have only 2 adjacent cells
            if ((i == 0 and j == 0)
                or (i == M - 1 and j == 0)
                or (i == 0 and j == N - 1)
                or (i == M - 1 and j == N - 1)):
                sum += 2

            # All the boundary elements
            # except the corner elements
            # have only 3 adjacent cells
            elif (i == 0 or j == 0 or i == M - 1 or j == N - 1):
                sum += 3

            # Rest of the elements have 4 adjacent cells
            else:
                sum += 4

            # If the sum is a Fibonacci number
            if (isFibonacci(sum)):
                count += 1

    return count

# Driver code

mat = [ [ 1, 0, 5, 3 ],
    [ 2, 17, 5, 6 ],
    [ 5, 8, 15, 11 ] ]
print(goodCells(mat))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int M = 3;
static int N = 4;

// Function that returns true if
// x is a perfect square
static bool isPerfectSquare(long x)
{
    // Find floating point value of
    // square root of x
    double sr = Math.Sqrt(x);

    // If square root is an integer
    return ((sr - Math.Floor(sr)) == 0);
}

// Function that returns true
// if n is a Fibonacci number
static bool isFibonacci(int n)
{
    return isPerfectSquare(5 * n * n + 4)
        || isPerfectSquare(5 * n * n - 4);
}

// Function to return the count of good cells
static int goodCells(int [,]mat)
{

    // To store the required count
    int count = 0;
    for (int i = 0; i < M; i++)
    {
        for (int j = 0; j < N; j++)
        {

            int sum = mat[i,j];

            // Corner cells of the matrix
            // have only 2 adjacent cells
            if ((i == 0 && j == 0)
                || (i == M - 1 && j == 0)
                || (i == 0 && j == N - 1)
                || (i == M - 1 && j == N - 1))
            {
                sum += 2;
            }

            // All the boundary elements
            // except the corner elements
            // have only 3 adjacent cells
            else if (i == 0 || j == 0
                    || i == M - 1 || j == N - 1)
            {
                sum += 3;
            }

            // Rest of the elements have 4 adjacent cells
            else
            {
                sum += 4;
            }

            // If the sum is a Fibonacci number
            if (isFibonacci(sum))
                count++;
        }
    }

    return count;
}

// Driver code
public static void Main ()
{
    int [,]mat = { { 1, 0, 5, 3 },
                { 2, 17, 5, 6 },
                { 5, 8, 15, 11 } };
    Console.WriteLine( goodCells(mat));
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let M = 3;
    let N = 4;

    // Function that returns true if
    // x is a perfect square
    function isPerfectSquare(x)
    {
        // Find floating point value of
        // square root of x
        let sr = Math.sqrt(x);

        // If square root is an integer
        return ((sr - Math.floor(sr)) == 0);
    }

    // Function that returns true
    // if n is a Fibonacci number
    function isFibonacci(n)
    {
        return isPerfectSquare(5 * n * n + 4)
            || isPerfectSquare(5 * n * n - 4);
    }

    // Function to return the count of good cells
    function goodCells(mat)
    {

        // To store the required count
        let count = 0;
        for (let i = 0; i < M; i++)
        {
            for (let j = 0; j < N; j++)
            {

                let sum = mat[i][j];

                // Corner cells of the matrix
                // have only 2 adjacent cells
                if ((i == 0 && j == 0)
                    || (i == M - 1 && j == 0)
                    || (i == 0 && j == N - 1)
                    || (i == M - 1 && j == N - 1))
                {
                    sum += 2;
                }

                // All the boundary elements
                // except the corner elements
                // have only 3 adjacent cells
                else if (i == 0 || j == 0
                        || i == M - 1 || j == N - 1)
                {
                    sum += 3;
                }

                // Rest of the elements have 4 adjacent cells
                else
                {
                    sum += 4;
                }

                // If the sum is a Fibonacci number
                if (isFibonacci(sum))
                    count++;
            }
        }

        return count;
    }

    let mat = [ [ 1, 0, 5, 3 ],
                 [ 2, 17, 5, 6 ],
                 [ 5, 8, 15, 11 ] ];
    document.write( goodCells(mat));

</script>
```

**Output**

```
7
```

**时间复杂度:** O(N*M)

**辅助空间:** O(1)