# 求给定矩阵的 Frobenius 范数

> 原文:[https://www . geeksforgeeks . org/find-the-Frobenius-norm-of-a-given-matrix/](https://www.geeksforgeeks.org/finding-the-frobenius-norm-of-a-given-matrix/)

给定一个 **M * N** 矩阵，任务是找到矩阵的[弗罗贝纽斯范数](https://en.wikipedia.org/wiki/Matrix_norm#Frobenius_norm)。矩阵的 Frobenius 范数定义为矩阵元素平方和的平方根。
**例:**

> **输入:** mat[][] = {{1，2}，{3，4}}
> **输出:**5.47723
> sqrt(1<sup>2</sup>+2<sup>2</sup>+3<sup>2</sup>+4<sup>2</sup>)= sqrt(30)= 5.47723
> **输入:**mat[]= { { 1，T0 }

**逼近:**求矩阵元素的平方和，然后打印计算值的平方根。
以下是上述办法的实施情况:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int row = 2, col = 2;

// Function to return the Frobenius
// Norm of the given matrix
float frobeniusNorm(int mat[row][col])
{

    // To store the sum of squares of the
    // elements of the given matrix
    int sumSq = 0;
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col; j++) {
            sumSq += pow(mat[i][j], 2);
        }
    }

    // Return the square root of
    // the sum of squares
    float res = sqrt(sumSq);
    return res;
}

// Driver code
int main()
{
    int mat[row][col] = { { 1, 2 }, { 3, 4 } };

    cout << frobeniusNorm(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    final static int row = 2, col = 2;

    // Function to return the Frobenius
    // Norm of the given matrix
    static float frobeniusNorm(int mat[][])
    {

        // To store the sum of squares of the
        // elements of the given matrix
        int sumSq = 0;
        for (int i = 0; i < row; i++)
        {
            for (int j = 0; j < col; j++)
            {
                sumSq += (int)Math.pow(mat[i][j], 2);
            }
        }

        // Return the square root of
        // the sum of squares
        float res = (float)Math.sqrt(sumSq);
        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        int mat[][] = { { 1, 2 }, { 3, 4 } };

        System.out.println(frobeniusNorm(mat));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt
row = 2
col = 2

# Function to return the Frobenius
# Norm of the given matrix
def frobeniusNorm(mat):

    # To store the sum of squares of the
    # elements of the given matrix
    sumSq = 0
    for i in range(row):
        for j in range(col):
            sumSq += pow(mat[i][j], 2)

    # Return the square root of
    # the sum of squares
    res = sqrt(sumSq)
    return round(res, 5)

# Driver code

mat = [ [ 1, 2 ], [ 3, 4 ] ]

print(frobeniusNorm(mat))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int row = 2, col = 2;

    // Function to return the Frobenius
    // Norm of the given matrix
    static float frobeniusNorm(int [,]mat)
    {

        // To store the sum of squares of the
        // elements of the given matrix
        int sumSq = 0;
        for (int i = 0; i < row; i++)
        {
            for (int j = 0; j < col; j++)
            {
                sumSq += (int)Math.Pow(mat[i, j], 2);
            }
        }

        // Return the square root of
        // the sum of squares
        float res = (float)Math.Sqrt(sumSq);
        return res;
    }

    // Driver code
    public static void Main ()
    {
        int [,]mat = { { 1, 2 }, { 3, 4 } };

        Console.WriteLine(frobeniusNorm(mat));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    let row = 2, col = 2;

    // Function to return the Frobenius
    // Norm of the given matrix
    function frobeniusNorm(mat)
    {

        // To store the sum of squares of the
        // elements of the given matrix
        let sumSq = 0;
        for (let i = 0; i < row; i++)
        {
            for (let j = 0; j < col; j++)
            {
                sumSq += parseInt(Math.pow(mat[i][j], 2));
            }
        }

        // Return the square root of
        // the sum of squares
        let res = parseFloat(Math.sqrt(sumSq));
        return res;
    }

    // Driver code

        let mat = [[ 1, 2 ], [ 3, 4 ]];

        document.write(frobeniusNorm(mat).toFixed(5));

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
5.47723
```