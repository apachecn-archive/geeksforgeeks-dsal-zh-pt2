# 按行和列排序的矩阵的任何子矩阵的最大和

> 原文:[https://www . geeksforgeeks . org/按行和列排序的矩阵的任意子矩阵的最大和/](https://www.geeksforgeeks.org/maximum-sum-of-any-submatrix-of-a-matrix-which-is-sorted-row-wise-and-column-wise/)

给定一个矩阵 **mat[][]** ，其元素按行和列进行排序。任务是从给定矩阵 **mat[][]** 中找到任意子矩阵的最大和。

**示例:**

> **输入:**mat[][]= {-6，-4，-1}，{-3，2，4}，{2，5，8}}
> **输出:** 19
> **解释:**
> 最大的子矩阵由下式给出:
> 2 4
> 5 8
> **输入:**mat[][]= {-4，-3}，{-2，-1} }
> **输出:【T0**

**天真方法:**想法是使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)在 2D 矩阵中找到[最大和矩形](https://www.geeksforgeeks.org/maximum-sum-rectangle-in-a-2d-matrix-dp-27/)。打印获得的最大总和。

***时间复杂度:**O(N)<sup>2</sup>* M<sup>2</sup>，其中 N 为行数，M 为列数*
***辅助空间:** O(N)*
**高效方法:**思想是从给定矩阵的底单元格中找出最大和，并使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)存储底单元格中任意子矩阵的最大和。以下是步骤:

1.  创建一个大小为 **NxM** 的 dp 表 **dp[][]** ，以存储从每个单元格 **(i，j)** 开始的子矩阵的最大和。
2.  从右下单元格 **(N，M)** 开始向上向左查找子矩阵的和，并不断将最大和更新为 **dp[][]** 。
3.  因为矩阵是按行和按列排序的，所以最大的子矩阵和可以从任何点开始，但肯定会在右下角的单元格(N，M)结束。
4.  下面是 dp 表的填写关系:

> DP[I][j]= DP[I+1][j]+DP[I][j+1]-DP[I+1][j+1]

1.  因此，在 dp 表中找到最大元素。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the maximum
// Sub-Matrix Sum
int maxSubMatSum(vector<vector<int> > mat)
{
    // Number of rows in the matrix
    int n = mat.size();

    // Number of columns in the matrix
    int m = mat[0].size();

    int i, j;

    // dp[][] matrix to store the
    // results of each iteration
    int dp[n][m];

    // Base Case - The largest
    // element in the matrix
    dp[n - 1][m - 1] = mat[n - 1][m - 1];

    // To stores the final result
    int res = dp[n - 1][m - 1];

    // Find the max sub matrix sum for
    // the last row
    for (i = m - 2; i >= 0; i--) {

        dp[n - 1][i] = mat[n - 1][i]
                       + dp[n - 1][i + 1];

        // Check whether the current
        // sub-array yields maximum sum
        res = max(res, dp[n - 1][i]);
    }

    // Calculate the max sub matrix
    // sum for the last column
    for (i = n - 2; i >= 0; i--) {

        dp[i][m - 1] = mat[i][m - 1]
                       + dp[i + 1][m - 1];

        // Check whether the current
        // sub-array yields maximum sum
        res = max(res, dp[i][m - 1]);
    }

    // Build the dp[][] matrix from
    // bottom to the top row
    for (i = n - 2; i >= 0; i--) {

        for (j = m - 2; j >= 0; j--) {

            // Update sum at each
            // cell in dp[][]
            dp[i][j]
                = mat[i][j] + dp[i][j + 1]
                  + dp[i + 1][j]
                  - dp[i + 1][j + 1];

            // Update the maximum sum
            res = max(res, dp[i][j]);
        }
    }

    // Return the maximum sum
    return res;
}

// Driver Code
int main()
{
    // Given matrix mat[][]
    vector<vector<int> > mat;
    mat = { { -6, -4, -1 },
            { -3, 2, 4 },
            { 2, 5, 8 } };

    // Function Call
    cout << maxSubMatSum(mat);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function that finds the maximum
// Sub-Matrix Sum
static int maxSubMatSum(int [][]mat)
{
    // Number of rows in the matrix
    int n = mat.length;

    // Number of columns in the matrix
    int m = mat[0].length;

    int i, j;

    // dp[][] matrix to store the
    // results of each iteration
    int [][]dp = new int[n][m];

    // Base Case - The largest
    // element in the matrix
    dp[n - 1][m - 1] = mat[n - 1][m - 1];

    // To stores the final result
    int res = dp[n - 1][m - 1];

    // Find the max sub matrix sum for
    // the last row
    for (i = m - 2; i >= 0; i--)
    {
        dp[n - 1][i] = mat[n - 1][i] +
                        dp[n - 1][i + 1];

        // Check whether the current
        // sub-array yields maximum sum
        res = Math.max(res, dp[n - 1][i]);
    }

    // Calculate the max sub matrix
    // sum for the last column
    for (i = n - 2; i >= 0; i--)
    {
        dp[i][m - 1] = mat[i][m - 1] +
                        dp[i + 1][m - 1];

        // Check whether the current
        // sub-array yields maximum sum
        res = Math.max(res, dp[i][m - 1]);
    }

    // Build the dp[][] matrix from
    // bottom to the top row
    for (i = n - 2; i >= 0; i--)
    {
        for (j = m - 2; j >= 0; j--)
        {

            // Update sum at each
            // cell in dp[][]
            dp[i][j] = mat[i][j] + dp[i][j + 1] +
                    dp[i + 1][j] - dp[i + 1][j + 1];

            // Update the maximum sum
            res = Math.max(res, dp[i][j]);
        }
    }

    // Return the maximum sum
    return res;
}

// Driver Code
public static void main(String[] args)
{
    // Given matrix mat[][]
    int [][]mat= {{ -6, -4, -1 },
                  { -3, 2, 4 },
                  { 2, 5, 8 } };

    // Function Call
    System.out.print(maxSubMatSum(mat));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the maximum
# Sub-Matrix Sum
def maxSubMatSum(mat):

    # Number of rows in the matrix
    n = len(mat)

    # Number of columns in the matrix
    m = len(mat[0])

    # dp[][] matrix to store the
    # results of each iteration
    dp = [[0] * m for _ in range(n)]

    # Base Case - The largest
    # element in the matrix
    dp[n - 1][m - 1] = mat[n - 1][m - 1]

    # To stores the final result
    res = dp[n - 1][m - 1]

    # Find the max sub matrix sum for
    # the last row
    for i in range(m - 2, -1, -1):
        dp[n - 1][i] = (mat[n - 1][i] +
                         dp[n - 1][i + 1])

        # Check whether the current
        # sub-array yields maximum sum
        res = max(res, dp[n - 1][i])

    # Calculate the max sub matrix
    # sum for the last column
    for i in range(n - 2, -1, -1):
        dp[i][m - 1] = (mat[i][m - 1] +
                     dp[i + 1][m - 1])

        # Check whether the current
        # sub-array yields maximum sum
        res = max(res, dp[i][m - 1])

    # Build the dp[][] matrix from
    # bottom to the top row
    for i in range(n - 2, -1, -1):
        for j in range(m - 2, -1, -1):

            # Update sum at each
            # cell in dp[][]
            dp[i][j] = (mat[i][j] +
                         dp[i][j + 1] +
                         dp[i + 1][j]-
                         dp[i + 1][j + 1])

            # Update the maximum sum
            res = max(res, dp[i][j])

    # Return the maximum sum
    return res

# Driver Code
if __name__ == '__main__':

    # Given matrix mat[][]
    mat = [ [ -6, -4, -1 ],
            [ -3, 2, 4 ],
            [ 2, 5, 8 ] ]

    # Function call
    print(maxSubMatSum(mat))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function that finds the maximum
// Sub-Matrix Sum
static int maxSubMatSum(int [,]mat)
{
    // Number of rows in the matrix
    int n = mat.GetLength(0);

    // Number of columns in the matrix
    int m = mat.GetLength(1);

    int i, j;

    // [,]dp matrix to store the
    // results of each iteration
    int [,]dp = new int[n, m];

    // Base Case - The largest
    // element in the matrix
    dp[n - 1, m - 1] = mat[n - 1, m - 1];

    // To stores the readonly result
    int res = dp[n - 1, m - 1];

    // Find the max sub matrix sum for
    // the last row
    for (i = m - 2; i >= 0; i--)
    {
        dp[n - 1, i] = mat[n - 1, i] +
                        dp[n - 1, i + 1];

        // Check whether the current
        // sub-array yields maximum sum
        res = Math.Max(res, dp[n - 1,i]);
    }

    // Calculate the max sub matrix
    // sum for the last column
    for (i = n - 2; i >= 0; i--)
    {
        dp[i, m - 1] = mat[i, m - 1] +
                        dp[i + 1, m - 1];

        // Check whether the current
        // sub-array yields maximum sum
        res = Math.Max(res, dp[i, m - 1]);
    }

    // Build the [,]dp matrix from
    // bottom to the top row
    for (i = n - 2; i >= 0; i--)
    {
        for (j = m - 2; j >= 0; j--)
        {

            // Update sum at each
            // cell in [,]dp
            dp[i, j] = mat[i, j] + dp[i, j + 1] +
                    dp[i + 1, j] - dp[i + 1, j + 1];

            // Update the maximum sum
            res = Math.Max(res, dp[i, j]);
        }
    }

    // Return the maximum sum
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    // Given matrix [,]mat
    int [,]mat= {{ -6, -4, -1 },
                 { -3, 2, 4 },
                 { 2, 5, 8 } };

    // Function Call
    Console.Write(maxSubMatSum(mat));
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program for the above approach   

// Function that finds the maximum
    // Sub-Matrix Sum
    function maxSubMatSum(mat)
    {
        // Number of rows in the matrix
        var n = mat.length;

        // Number of columns in the matrix
        var m = mat[0].length;

        var i, j;

        // dp matrix to store the
        // results of each iteration
        var dp = Array(n).fill().map(() =>
        Array(m).fill(0));

        // Base Case - The largest
        // element in the matrix
        dp[n - 1][m - 1] = mat[n - 1][m - 1];

        // To stores the final result
        var res = dp[n - 1][m - 1];

        // Find the max sub matrix sum for
        // the last row
        for (i = m - 2; i >= 0; i--) {
            dp[n - 1][i] = mat[n - 1][i] +
                            dp[n - 1][i + 1];

            // Check whether the current
            // sub-array yields maximum sum
            res = Math.max(res, dp[n - 1][i]);
        }

        // Calculate the max sub matrix
        // sum for the last column
        for (i = n - 2; i >= 0; i--) {
            dp[i][m - 1] = mat[i][m - 1] +
                            dp[i + 1][m - 1];

            // Check whether the current
            // sub-array yields maximum sum
            res = Math.max(res, dp[i][m - 1]);
        }

        // Build the dp matrix from
        // bottom to the top row
        for (i = n - 2; i >= 0; i--) {
            for (j = m - 2; j >= 0; j--) {

                // Update sum at each
                // cell in dp
                dp[i][j] = mat[i][j] + dp[i][j + 1] +
                dp[i + 1][j] - dp[i + 1][j + 1];

                // Update the maximum sum
                res = Math.max(res, dp[i][j]);
            }
        }

        // Return the maximum sum
        return res;
    }

    // Driver Code

        // Given matrix mat
        var mat = [ [ -6, -4, -1 ],
                    [ -3, 2, 4 ],
                    [ 2, 5, 8 ] ];

        // Function Call
        document.write(maxSubMatSum(mat));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
19
```

***时间复杂度:** O(N*M)，其中 N 为行数，M 为列数*
***辅助空间:** O(N*M)*