# 给定矩阵中 A[i][j] = 0 的指数(I，j)的最大差值

> 原文:[https://www . geeksforgeeks . org/最大指数差-I-j-这样-AIJ-0-给定矩阵/](https://www.geeksforgeeks.org/maximum-difference-of-indices-i-j-such-that-aij-0-in-the-given-matrix/)

给定 n*n 阶的矩阵，任务是找到|i-j|的最大值，使得 Aij = 0。给定矩阵必须至少包含一个 0。
**例:**

```
Input: matrix[][] = 
{{2, 3, 0},
{0, 2, 0},
{0, 1, 1}}
Output: 2
mat(0, 2) has a value 0 and difference of index is maximum i.e. 2.

Input: matrix[][] = 
{{2, 3, 4},
{0, 2, 0},
{6, 1, 1}}
Output: 1
```

**方法:**为了找到|i-j|的最大值，使得 Aij = 0，遍历整个矩阵，对于零的每次出现，计算(i-j)的 mod，并将其存储在辅助矩阵中对应于相同位置的位置。最后，从辅助矩阵中找出最大值。
除了使用辅助矩阵外，|i-j|的最大值可以存储在变量中，并且可以在计算时更新。这将节省额外的空间使用。
以下是上述办法的实施:

## C++

```
// CPP for maximum |i-j| such that Aij = 0
#include <bits/stdc++.h>
#define n 4
using namespace std;

// function to return maximum |i-j| such that Aij = 0
int calculateDiff(int matrix[][n])
{

    int result = 0;

    // traverse the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == 0)
                result = max(result, abs(i - j));
        }
    }

    // return result
    return result;
}

// driver program
int main()
{
    int matrix[n][n] = { { 2, 3, 0, 1 },
                         { 0, 2, 0, 1 },
                         { 0, 1, 1, 3 },
                         { 1, 2, 3, 3 } };

    cout << calculateDiff(matrix);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for maximum |i-j| such that Aij = 0
import java.math.*;
class GFG {

static int n = 4;

// function to return maximum |i-j| such that Aij = 0
static int calculateDiff(int matrix[][])
{

    int result = 0;

    // traverse the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == 0)
                result = Math.max(result, Math.abs(i - j));
        }
    }

    // return result
    return result;
}

// driver program
public static void main(String args[])
{
    int matrix[][] = new int[][] {{ 2, 3, 0, 1 },
                        { 0, 2, 0, 1 },
                        { 0, 1, 1, 3 },
                        { 1, 2, 3, 3 } };

    System.out.println(calculateDiff(matrix));
}

}
```

## 蟒蛇 3

```
# Python3 program for maximum
# |i-j| such that Aij = 0

# function to return maximum
# |i-j| such that Aij = 0
def calculateDiff(matrix, n):

    result = 0

    # traverse the matrix
    for i in range(0, n):
        for j in range(0, n):
            if(matrix[i][j] == 0):
                result = max(result, abs(i - j))

    return result

# Driver code
if __name__=='__main__':
    matrix = [[2, 3, 0, 1],
              [0, 2, 0, 1],
              [0, 1, 1, 3],
              [1, 2, 3, 3]]
    n = len(matrix)
    print(calculateDiff(matrix, n))

# This code is contributed by
# Kirti_Mangal
```

## C#

```
// C# for maximum |i-j| such that Aij = 0
using System;

class GFG
{
static int n = 4;

// function to return maximum |i-j|
// such that Aij = 0
static int calculateDiff(int [,]matrix)
{
    int result = 0;

    // traverse the matrix
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if (matrix[i, j] == 0)
                result = Math.Max(result,
                         Math.Abs(i - j));
        }
    }

    // return result
    return result;
}

// Driver code
static void Main()
{
    int [,]matrix = new int[,]
    {
        { 2, 3, 0, 1 },
        { 0, 2, 0, 1 },
        { 0, 1, 1, 3 },
        { 1, 2, 3, 3 }
    };

    Console.WriteLine(calculateDiff(matrix));;
}
}

// This code is contributed by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP for maximum |i-j| such that Aij = 0

// function to return maximum |i-j|
// such that Aij = 0
function calculateDiff($matrix)
{
    $n = 4;
    $result = 0;

    // traverse the matrix
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            if ($matrix[$i][$j] == 0)
                $result = max($result,
                          abs($i - $j));
        }
    }

    // return result
    return $result;
}

// Driver Code
$matrix = array(array( 2, 3, 0, 1 ),
                array( 0, 2, 0, 1 ),
                array( 0, 1, 1, 3 ),
                array( 1, 2, 3, 3 ));

echo calculateDiff($matrix);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript for maximum |i-j| such that Aij = 0
var n = 4

// function to return maximum |i-j| such that Aij = 0
function calculateDiff(matrix)
{

    var result = 0;

    // traverse the matrix
    for (var i = 0; i < n; i++) {
        for (var j = 0; j < n; j++) {
            if (matrix[i][j] == 0)
                result = Math.max(result, Math.abs(i - j));
        }
    }

    // return result
    return result;
}

// driver program
var matrix = [ [ 2, 3, 0, 1 ],
                     [ 0, 2, 0, 1 ],
                     [ 0, 1, 1, 3 ],
                     [ 1, 2, 3, 3 ] ];
document.write( calculateDiff(matrix));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(n^2)