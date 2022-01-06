# 矩阵中从上到下的最大和路径

> 原文:[https://www . geesforgeks . org/maximum-sum-path-matrix-top-bottom/](https://www.geeksforgeeks.org/maximum-sum-path-matrix-top-bottom/)

考虑一个 n*n 矩阵。假设矩阵中的每个单元格都有一个赋值。我们可以仅从第 I 行的每个单元格到第 i+1 行的对角更高的单元格[即，仅从单元格(I，j)到单元格(i+1，j-1)和单元格(i+1，j+1)]。根据上述条件找到从顶行到底行的路径，从而获得最大和。

**示例:**

```
Input : mat[][] = { {5, 6, 1, 7},
                {-2, 10, 8, -1},
                {3, -7, -9, 11},
                {12, -4, 2, 6} }
Output : 28

{5, 6, 1, 7},
{-2, 10, 8, -1},
{3, -7, -9, 11},
{12, -4, 2, 6} }

The highlighted numbers from top to bottom
gives the required maximum sum path.
(7 + 8 + 11 + 2) = 28
```

**算法:**思路是从第一行的每一个单元格开始寻找所有路径的最大和，最后返回第一行所有值的最大值。我们使用动态规划，因为许多子问题的结果是一次又一次需要的。

## C++

```
// C++ implementation to find the maximum sum
// path in a matrix
#include <bits/stdc++.h>
using namespace std;

#define SIZE 10

// function to find the maximum sum
// path in a matrix
int maxSum(int mat[SIZE][SIZE], int n)
{
    // if there is a single element only
    if (n == 1)
        return mat[0][0];

    // dp[][] matrix to store the results
    // of each iteration
    int dp[n][n];
    int maxSum = INT_MIN, max;

    // base case, copying elements of
    // last row
    for (int j = 0; j < n; j++)
        dp[n - 1][j] = mat[n - 1][j];

    // building up the dp[][] matrix from
    // bottom to the top row
    for (int i = n - 2; i >= 0; i--) {
        for (int j = 0; j < n; j++) {
            max = INT_MIN;

            // finding the maximum diagonal element in the
            // (i+1)th row if that cell exists
            if (((j - 1) >= 0) && (max < dp[i + 1][j - 1]))
                max = dp[i + 1][j - 1];
            if (((j + 1) < n) && (max < dp[i + 1][j + 1]))
                max = dp[i + 1][j + 1];

            // adding that 'max' element to the
            // mat[i][j] element
            dp[i][j] = mat[i][j] + max;
        }
    }

    // finding the maximum value from the
    // first row of dp[][]
    for (int j = 0; j < n; j++)
        if (maxSum < dp[0][j])
            maxSum = dp[0][j];

    // required maximum sum
    return maxSum;
}

// Driver program to test above
int main()
{
    int mat[SIZE][SIZE] = { { 5, 6, 1, 7 },
                            { -2, 10, 8, -1 },
                            { 3, -7, -9, 11 },
                            { 12, -4, 2, 6 } };
    int n = 4;

    cout << "Maximum Sum = "
         << maxSum(mat, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum sum path in a matrix
import java.io.*;

class MaxSumPath {
//int mat[][];

// function to find the maximum
// sum path in a matrix
static int maxSum(int[][] mat, int n)
{
    // if there is a single element only
    if (n == 1)
        return mat[0][0];

    // dp[][] matrix to store the results
    // of each iteration
    int dp[][] = new int[n][n];
    int maxSum = Integer.MIN_VALUE, max;

    // base case, copying elements of
    // last row
    for (int j = 0; j < n; j++)
        dp[n - 1][j] = mat[n - 1][j];

    // building up the dp[][] matrix
    // from bottom to the top row
    for (int i = n - 2; i >= 0; i--) {
        for (int j = 0; j < n; j++) {
            max = Integer.MIN_VALUE;

            // finding the maximum diagonal
            // element in the (i+1)th row
            // if that cell exists
            if (((j - 1) >= 0) &&
                 (max < dp[i + 1][j - 1]))
                 max = dp[i + 1][j - 1];
            if (((j + 1) < n) &&
                (max < dp[i + 1][j + 1]))
                max = dp[i + 1][j + 1];

            // adding that 'max' element
            // to the mat[i][j] element
            dp[i][j] = mat[i][j] + max;
        }
    }

    // finding the maximum value from
    // the first row of dp[][]
    for (int j = 0; j < n; j++)
        if (maxSum < dp[0][j])
            maxSum = dp[0][j];

    // required maximum sum
    return maxSum;
}

    // Driver code
    public static void main (String[] args) {

    int mat[][] = { { 5, 6, 1, 7 },
                    { -2, 10, 8, -1 },
                    { 3, -7, -9, 11 },
                    { 12, -4, 2, 6 } };
    int n = 4;

    System.out.println("Maximum Sum = "+
                        maxSum(mat , n));

    }
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 implementation to find
# the maximum sum path in a matrix

SIZE=10
INT_MIN=-10000000

# function to find the maximum sum
# path in a matrix
def maxSum(mat,n):

    #if there is a single elementif
    #there is a single element only only
    if n==1:
        return mat[0][0]

    # dp[][] matrix to store the results
    # of each iteration
    dp=[[0 for i in range(n)]for i in range(n)]
    maxSum=INT_MIN

    # base case, copying elements of
    # last row
    for j in range(n):
        dp[n - 1][j] = mat[n - 1][j]

    # building up the dp[][] matrix from
    # bottom to the top row
    for i in range(n-2,-1,-1):
        for j in range(n):
            maxi=INT_MIN

            # finding the maximum diagonal
            # element in the
            # (i+1)th row if that cell exists
            if ((((j - 1) >= 0) and
               (maxi < dp[i + 1][j - 1]))):
                   maxi = dp[i + 1][j - 1]
            if ((((j + 1) < n) and
               (maxi < dp[i + 1][j + 1]))):
                   maxi = dp[i + 1][j + 1]

            # adding that 'max' element to the
            # mat[i][j] element
            dp[i][j] = mat[i][j] + maxi

    # finding the maximum value from the
    # first row of dp[][]
    for j in range(n):
        if (maxSum < dp[0][j]):
            maxSum = dp[0][j]

    # required maximum sum
    return maxSum

# Driver program to test above
if __name__=='__main__':
    mat=[[5, 6, 1, 7],
        [-2, 10, 8, -1],
        [ 3, -7, -9, 11 ],
        [12, -4, 2, 6 ]]

    n=4
    print("Maximum Sum=",maxSum(mat,n))

#This code is contributed by sahilshelangia
```

## C#

```
// C# implementation to find the
// maximum sum path in a matrix
using System;

class MaxSumPath
{
    //int mat[][];

    // function to find the maximum
    // sum path in a matrix
    static int maxSum(int[,] mat, int n)
    {
        // if there is a single element only
        if (n == 1)
            return mat[0, 0];

        // dp[][] matrix to store the results
        // of each iteration
        int [,]dp = new int[n, n];
        int maxSum = int.MinValue, max;

        // base case, copying elements of
        // last row
        for (int j = 0; j < n; j++)
            dp[n - 1, j] = mat[n - 1, j];

        // building up the dp[][] matrix
        // from bottom to the top row
        for (int i = n - 2; i >= 0; i--)
        {
            for (int j = 0; j < n; j++)
            {
                max = int.MinValue;

                // finding the maximum diagonal
                // element in the (i+1)th row
                // if that cell exists
                if (((j - 1) >= 0) &&
                    (max < dp[i + 1, j - 1]))
                    max = dp[i + 1, j - 1];
                if (((j + 1) < n) &&
                    (max < dp[i + 1, j + 1]))
                    max = dp[i + 1, j + 1];

                // adding that 'max' element
                // to the mat[i][j] element
                dp[i, j] = mat[i, j] + max;
            }
        }

        // finding the maximum value from
        // the first row of dp[][]
        for (int j = 0; j < n; j++)
            if (maxSum < dp[0, j])
                maxSum = dp[0, j];

        // required maximum sum
        return maxSum;
    }

    // Driver code
    public static void Main () {

    int [,]mat = { { 5, 6, 1, 7 },
                    { -2, 10, 8, -1 },
                    { 3, -7, -9, 11 },
                    { 12, -4, 2, 6 } };
    int n = 4;

    Console.WriteLine("Maximum Sum = "+
                        maxSum(mat , n));

    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// the maximum sum path in a matrix

$SIZE = 10;

// function to find the maximum sum
// path in a matrix
function maxSum( $mat, $n)
{

    // if there is a single
    // element only
    if ($n == 1)
        return $mat[0][0];

    // dp[][] matrix to store the results
    // of each iteration
    $dp = array(array());
    $maxSum = PHP_INT_MIN;
    $max;

    // base case, copying elements of
    // last row
    for($j = 0; $j < $n; $j++)
        $dp[$n - 1][$j] = $mat[$n - 1][$j];

    // building up the dp[][] matrix from
    // bottom to the top row
    for ( $i = $n - 2; $i >= 0; $i--)
    {
        for ( $j = 0; $j < $n; $j++)
        {
            $max = PHP_INT_MIN;

            // finding the maximum
            // diagonal element in the
            // (i+1)th row if that cell
            // exists
            if ((($j - 1) >= 0) and
                ($max < $dp[$i + 1][$j - 1]))

                $max = $dp[$i + 1][$j - 1];

            if ((($j + 1) < $n) and ($max <
                      $dp[$i + 1][$j + 1]))

                $max = $dp[$i + 1][$j + 1];

            // adding that 'max' element to the
            // mat[i][j] element
            $dp[$i][$j] = $mat[$i][$j] + $max;
        }
    }

    // finding the maximum value from the
    // first row of dp[][]
    for ( $j = 0; $j < $n; $j++)
        if ($maxSum < $dp[0][$j])
            $maxSum = $dp[0][$j];

    // required maximum sum
    return $maxSum;
}

    // Driver Code
    $mat = array(array(5, 6, 1, 7),
                 array(-2, 10, 8, -1),
                 array(3, -7, -9, 11),
                 array(12, -4, 2, 6));
    $n = 4;
    echo "Maximum Sum = "
        , maxSum($mat, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// maximum sum path in a matrix

// Function to find the maximum
// sum path in a matrix
function maxSum(mat, n)
{

    // If there is a single element only
    if (n == 1)
        return mat[0][0];

    // dp[][] matrix to store the results
    // of each iteration
    let dp = new Array(n);

    // Loop to create 2D array using 1D array
    for(var i = 0; i < dp.length; i++)
    {
        dp[i] = new Array(2);
    }

    let maxSum = Number.MIN_VALUE, max;

    // Base case, copying elements of
    // last row
    for(let j = 0; j < n; j++)
        dp[n - 1][j] = mat[n - 1][j];

    // Building up the dp[][] matrix
    // from bottom to the top row
    for(let i = n - 2; i >= 0; i--)
    {
        for(let j = 0; j < n; j++)
        {
            max = Number.MIN_VALUE;

            // Finding the maximum diagonal
            // element in the (i+1)th row
            // if that cell exists
            if (((j - 1) >= 0) &&
               (max < dp[i + 1][j - 1]))
                 max = dp[i + 1][j - 1];
            if (((j + 1) < n) &&
               (max < dp[i + 1][j + 1]))
                max = dp[i + 1][j + 1];

            // Adding that 'max' element
            // to the mat[i][j] element
            dp[i][j] = mat[i][j] + max;
        }
    }

    // Finding the maximum value from
    // the first row of dp[][]
    for(let j = 0; j < n; j++)
        if (maxSum < dp[0][j])
            maxSum = dp[0][j];

    // Required maximum sum
    return maxSum;
}

// Driver Code
let mat = [ [ 5, 6, 1, 7 ],
            [ -2, 10, 8, -1 ],
            [ 3, -7, -9, 11 ],
            [ 12, -4, 2, 6 ] ];
let n = 4;

document.write("Maximum Sum = "+
               maxSum(mat , n));

// This code is contributed by sanjoy_62

</script>
```

**输出:**

```
Maximum Sum = 28
```

时间复杂度:O(n <sup>2</sup> )。
辅助空间:O(n <sup>2</sup> )。

**练习:**尽量在 O(n)的辅助空间求解。