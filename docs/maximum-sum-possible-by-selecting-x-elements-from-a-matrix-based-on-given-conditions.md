# 基于给定条件从矩阵中选择 X 个元素的最大可能和

> 原文:[https://www . geeksforgeeks . org/基于给定条件从矩阵中选择 x 个元素的最大可能总和/](https://www.geeksforgeeks.org/maximum-sum-possible-by-selecting-x-elements-from-a-matrix-based-on-given-conditions/)

给定维度为 **N × M** 的矩阵 **G[][]** ，由正整数组成，任务是从具有最大和的矩阵中选择 **X** 元素，条件是 **G[i][j]** 只能从矩阵中选择，除非所有元素 **G[i][k]** 都被选择，其中 **0 ≤ k < j** 即， 当前**I**行中的 **j <sup>第</sup>** 个元素可以被选择，其当前 **i <sup>第</sup>** 行的所有前面的元素已经被选择。

**示例:**

> **输入:** N = 4，M = 4，X = 6，G[][] = {{3，2，6，1}，{1，9，2，4}，{4，1，3，9}，{3，8，2， 1}}
> **输出:** 28
> **说明:**
> 从第一行选择第一个元素= 3
> 从第二行选择前两个元素= 1 + 9 = 10
> 从第三行选择第一个元素= 4
> 从第四行选择前两个元素= 3 + 8 = 11
> 因此，所选元素为{G[0][0]、G[1][0]、G[1][1]、G[2][2]
> 
> **输入:** N = 2，M = 4，X = 4，G[][] = {{10，10，100，30}，{80，50，10，50}}
> **输出:** 200

**天真法:**解决这个问题最简单的方法就是计算所有可能的 **M** 选择的和，找到其中的**最大和**。

***时间复杂度:** O(N <sup>M</sup> )*
**辅助空间:** O(1)

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。相当多的州是:

1.  选择的行数: **i** 。
2.  选择的元素数量: **j** 。

初始化一个矩阵 **dp[][]** ，使得 **dp[i][j]** 存储通过从第一个 **i** 行中选择 **j** 元素可以获得的最大可能和。

dp[][]的过渡如下:

> DP[I][j]=max<sub>x =(0，min(j，m))</sub>(DP[I–1][j–x]+pref sum[I][x])
> 其中 **prefsum[i][x]** 是矩阵第 **i <sup>第</sup>** 行中第一个 **x** 元素的和。

下面是上述方法的实现:

## C++14

```
// C++14 program to implement 
// the above approach 
#include <bits/stdc++.h>
using namespace std;

int n, m, X;

// Function to calculate the maximum
// possible sum by selecting X elements
// from the Matrix
int maxSum(vector<vector<int>> grid)
{

    // Generate prefix sum of the matrix
    vector<vector<int>> prefsum(n, vector<int>(m));

    for(int i = 0; i < n; i++)
    {
        for(int x = 0; x < m; x++)
        {
            if (x == 0)
                prefsum[i][x] = grid[i][x];
            else
                prefsum[i][x] = prefsum[i][x - 1] +
                                   grid[i][x];
        }
    }

    vector<vector<int>> dp(n, vector<int>(X + 1, INT_MIN));

    // Maximum possible sum by selecting
    // 0 elements from the first i rows
    for(int i = 0; i < n; i++)
           dp[i][0] = 0;

    // If a single row is present
    for(int i = 1; i <= min(m, X); ++i)
    {
        dp[0][i] = dp[0][i - 1] +
                 grid[0][i - 1];
    }

    for(int i = 1; i < n; ++i)
    {
        for(int j = 1; j <= X; ++j)
        {

            // If elements from the
            // current row is not selected
            dp[i][j] = dp[i - 1][j];

            // Iterate over all possible
            // selections from current row
            for(int x = 1; x <= min(j, m); x++)
            {
                dp[i][j] = max(dp[i][j],
                               dp[i - 1][j - x] +
                              prefsum[i][x - 1]);
            }
        }
    }

    // Return maximum possible sum
    return dp[n - 1][X];
}

// Driver code
int main()
{
    n = 4;
    m = 4;
    X = 6;

    vector<vector<int>> grid = { { 3, 2, 6, 1 },
                                 { 1, 9, 2, 4 },
                                 { 4, 1, 3, 9 },
                                 { 3, 8, 2, 1 } };

    int ans = maxSum(grid);

    cout << (ans);
    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.io.*;

class GFG {

    static int n, m, X;

    // Function to calculate the maximum
    // possible sum by selecting X elements
    // from the Matrix
    public static int maxSum(int[][] grid)
    {

        // Generate prefix sum of the matrix
        int prefsum[][] = new int[n][m];
        for (int i = 0; i < n; i++) {
            for (int x = 0; x < m; x++) {
                if (x == 0)
                    prefsum[i][x] = grid[i][x];
                else
                    prefsum[i][x]
                        = prefsum[i][x - 1] + grid[i][x];
            }
        }

        int dp[][] = new int[n][X + 1];

        // Initialize dp[][]
        for (int dpp[] : dp)
            Arrays.fill(dpp, Integer.MIN_VALUE);

        // Maximum possible sum by selecting
        // 0 elements from the first i rows
        for (int i = 0; i < n; i++)
            dp[i][0] = 0;

        // If a single row is present
        for (int i = 1; i <= Math.min(m, X); ++i) {
            dp[0][i] = dp[0][i - 1] + grid[0][i - 1];
        }

        for (int i = 1; i < n; ++i) {
            for (int j = 1; j <= X; ++j) {

                // If elements from the
                // current row is not selected
                dp[i][j] = dp[i - 1][j];

                // Iterate over all possible
                // selections from current row
                for (int x = 1; x <= Math.min(j, m);
                     x++) {
                    dp[i][j]
                        = Math.max(dp[i][j],
                                   dp[i - 1][j - x]
                                       + prefsum[i][x - 1]);
                }
            }
        }

        // Return maximum possible sum
        return dp[n - 1][X];
    }

    // Driver Code
    public static void main(String[] args)
    {
        n = 4;
        m = 4;
        X = 6;

        int grid[][] = { { 3, 2, 6, 1 },
                         { 1, 9, 2, 4 },
                         { 4, 1, 3, 9 },
                         { 3, 8, 2, 1 } };

        int ans = maxSum(grid);

        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to calculate the maximum
# possible sum by selecting X elements
# from the Matrix
def maxSum(grid):

    # Generate prefix sum of the matrix
    prefsum = [[0 for x in range(m)]
                  for y in range(m)]

    for i in range(n):
        for x in range(m):
            if (x == 0):
                prefsum[i][x] = grid[i][x]
            else:
                prefsum[i][x] = (prefsum[i][x - 1] +
                                    grid[i][x])

    dp = [[-sys.maxsize - 1 for x in range(X + 1)]
                            for y in range(n)]

    # Maximum possible sum by selecting
    # 0 elements from the first i rows
    for i in range(n):
        dp[i][0] = 0

    # If a single row is present
    for i in range(1, min(m, X)):
        dp[0][i] = (dp[0][i - 1] +
                  grid[0][i - 1])

    for i in range(1, n):
        for j in range(1, X + 1):

            # If elements from the
            # current row is not selected
            dp[i][j] = dp[i - 1][j]

            # Iterate over all possible
            # selections from current row
            for x in range(1, min(j, m) + 1):
                    dp[i][j] = max(dp[i][j],
                                   dp[i - 1][j - x] +
                              prefsum[i][x - 1])

    # Return maximum possible sum
    return dp[n - 1][X]

# Driver Code
if __name__ == "__main__":

    n = 4
    m = 4
    X = 6

    grid = [ [ 3, 2, 6, 1 ],
             [ 1, 9, 2, 4 ],
             [ 4, 1, 3, 9 ],
             [ 3, 8, 2, 1 ] ]
    ans = maxSum(grid)

    print(ans)

# This code is contributed by chitranayal   
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

static int n, m, X;

// Function to calculate the maximum
// possible sum by selecting X elements
// from the Matrix
public static int maxSum(int[,] grid)
{

    // Generate prefix sum of the matrix
    int [,]prefsum = new int[n, m];

    for(int i = 0; i < n; i++)
    {
        for(int x = 0; x < m; x++)
        {
            if (x == 0)
                prefsum[i, x] = grid[i, x];
            else
                prefsum[i, x] = prefsum[i, x - 1] +
                                   grid[i, x];
        }
    }

    int [,]dp = new int[n, X + 1];

    // Initialize [,]dp
    for(int i = 1; i < n; i++)
        for(int j = 1; j <= X; ++j)
            dp[i, j] = int.MinValue;

    // Maximum possible sum by selecting
    // 0 elements from the first i rows
    for(int i = 0; i < n; i++)
        dp[i, 0] = 0;

    // If a single row is present
    for(int i = 1; i <= Math.Min(m, X); ++i)
    {
        dp[0, i] = dp[0, i - 1] + grid[0, i - 1];
    }

    for(int i = 1; i < n; ++i)
    {
        for(int j = 1; j <= X; ++j)
        {

            // If elements from the
            // current row is not selected
            dp[i, j] = dp[i - 1, j];

            // Iterate over all possible
            // selections from current row
            for(int x = 1; x <= Math.Min(j, m); x++)
            {
                dp[i, j] = Math.Max(dp[i, j],
                                    dp[i - 1, j - x] +
                               prefsum[i, x - 1]);
            }
        }
    }

    // Return maximum possible sum
    return dp[n - 1, X];
}

// Driver Code
public static void Main(String[] args)
{
    n = 4;
    m = 4;
    X = 6;

    int [,]grid = { { 3, 2, 6, 1 },
                    { 1, 9, 2, 4 },
                    { 4, 1, 3, 9 },
                    { 3, 8, 2, 1 } };

    int ans = maxSum(grid);

    Console.WriteLine(ans);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

let n, m, X;

    // Function to calculate the maximum
    // possible sum by selecting X elements
    // from the Matrix
    function maxSum(grid)
    {

        // Generate prefix sum of the matrix
        let prefsum = new Array(n);
        // Loop to create 2D array using 1D array
        for (var i = 0; i < prefsum.length; i++) {
            prefsum[i] = new Array(2);
        }

        for (let i = 0; i < n; i++) {
            for (let x = 0; x < m; x++) {
                if (x == 0)
                    prefsum[i][x] = grid[i][x];
                else
                    prefsum[i][x]
                        = prefsum[i][x - 1] + grid[i][x];
            }
        }

        let dp = new Array(n);
         // Loop to create 2D array using 1D array
        for (var i = 0; i < dp.length; i++) {
            dp[i] = new Array(2);
        }
        for (var i = 0; i < n; i++) {
            for (var j = 0; j < X+1; j++) {
            dp[i][j] = 0;
        }
        }

        // Maximum possible sum by selecting
        // 0 elements from the first i rows
        for (let i = 0; i < n; i++)
            dp[i][0] = 0;

        // If a single row is present
        for (let i = 1; i <= Math.min(m, X); ++i) {
            dp[0][i] = dp[0][i - 1] + grid[0][i - 1];
        }

        for (let i = 1; i < n; ++i) {
            for (let j = 1; j <= X; ++j) {

                // If elements from the
                // current row is not selected
                dp[i][j] = dp[i - 1][j];

                // Iterate over all possible
                // selections from current row
                for (let x = 1; x <= Math.min(j, m);
                     x++) {
                    dp[i][j]
                        = Math.max(dp[i][j],
                                   dp[i - 1][j - x]
                                       + prefsum[i][x - 1]);
                }
            }
        }

        // Return maximum possible sum
        return dp[n - 1][X];
    }

// Driver Code

           n = 4;
        m = 4;
        X = 6;

        let grid = [[ 3, 2, 6, 1 ],
                    [ 1, 9, 2, 4 ],
                    [ 4, 1, 3, 9 ],
                    [ 3, 8, 2, 1 ]];

        let ans = maxSum(grid);

        document.write(ans);

</script>
```

**Output:** 

```
28
```

***时间复杂度:**O(N * M * X)*
T5】辅助空间: O(N*M)