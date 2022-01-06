# 矩阵中最长的增加路径

> 原文:[https://www . geesforgeks . org/最长增加路径矩阵/](https://www.geeksforgeeks.org/longest-increasing-path-matrix/)

给定一个由 **N** 行和 **M** 列组成的矩阵。从 m[i][j]，我们可以移到 m[i+1][j]，如果 m[i+1][j] > m[i][j]，或者可以移到 m[i][j+1]如果 m[i][j+1] > m[i][j]。如果从(0，0)开始，任务是打印最长路径长度。
**例:**

```
Input : N = 4, M = 4
        m[][] = { { 1, 2, 3, 4 },
                  { 2, 2, 3, 4 },
                  { 3, 2, 3, 4 },
                  { 4, 5, 6, 7 } };
Output : 7
Longest path is 1 2 3 4 5 6 7.

Input : N = 2, M =2
        m[][] = { { 1, 2 },
                  { 3, 4 } };
Output :3
Longest path is either 1 2 4 or 
1 3 4.
```

这个想法是使用动态编程。维护 2D 矩阵 dp[][]，其中 dp[i][j]存储子矩阵从第 I 行和第 j 列开始的最长递增序列的长度值。
让 m[i+1][j]和 m[i][j+1]的最长递增子序列值分别已知为 v1 和 v2。那么 m[i][j]的值将是 max(v1，v2) + 1。
我们可以从 m[n-1][m-1]开始，作为最长递增子序列长度为 1 的基本情况，向上和向左移动更新单元格的值。那么单元格 m[0][0]的 LIP 值将是答案。
以下是本办法的实施情况:

## C++

```
// CPP program to find longest increasing
// path in a matrix.
#include <bits/stdc++.h>
#define MAX 10
using namespace std;

// Return the length of LIP in 2D matrix
int LIP(int dp[][MAX], int mat[][MAX], int n, int m, int x, int y)
{
    // If value not calculated yet.
    if (dp[x][y] < 0) {
        int result = 0;

        // If reach bottom left cell, return 1.
        if (x == n - 1 && y == m - 1)
            return dp[x][y] = 1;

        // If reach the corner of the matrix.
        if (x == n - 1 || y == m - 1)
            result = 1;

        // If value greater than below cell.
        if (mat[x][y] < mat[x + 1][y])
            result = 1 + LIP(dp, mat, n, m, x + 1, y);

        // If value greater than left cell.
        if (mat[x][y] < mat[x][y + 1])
            result = max(result, 1 + LIP(dp, mat, n, m, x, y + 1));

        dp[x][y] = result;
    }

    return dp[x][y];
}

// Wrapper function
int wrapper(int mat[][MAX], int n, int m)
{
    int dp[MAX][MAX];
    memset(dp, -1, sizeof dp);

    return LIP(dp, mat, n, m, 0, 0);
}

// Driven Program
int main()
{
    int mat[][MAX] = {
        { 1, 2, 3, 4 },
        { 2, 2, 3, 4 },
        { 3, 2, 3, 4 },
        { 4, 5, 6, 7 },
    };
    int n = 4, m = 4;
    cout << wrapper(mat, n, m) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest increasing
// path in a matrix.
import java.util.*;

class GFG {

    // Return the length of LIP in 2D matrix
    static int LIP(int dp[][], int mat[][], int n,
                   int m, int x, int y)
    {
        // If value not calculated yet.
        if (dp[x][y] < 0) {
            int result = 0;

            // If reach bottom left cell, return 1.
            if (x == n - 1 && y == m - 1)
                return dp[x][y] = 1;

            // If reach the corner of the matrix.
            if (x == n - 1 || y == m - 1)
                result = 1;

            // If value greater than below cell.
            if (x + 1 < n && mat[x][y] < mat[x + 1][y])
                result = 1 + LIP(dp, mat, n, m, x + 1, y);

            // If value greater than left cell.
            if (y + 1 < m && mat[x][y] < mat[x][y + 1])
                result = Math.max(result, 1 + LIP(dp, mat, n, m, x, y + 1));

            dp[x][y] = result;
        }

        return dp[x][y];
    }

    // Wrapper function
    static int wrapper(int mat[][], int n, int m)
    {
        int dp[][] = new int[10][10];
        for (int i = 0; i < 10; i++)
            Arrays.fill(dp[i], -1);

        return LIP(dp, mat, n, m, 0, 0);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int mat[][] = {
            { 1, 2, 3, 4 },
            { 2, 2, 3, 4 },
            { 3, 2, 3, 4 },
            { 4, 5, 6, 7 },
        };
        int n = 4, m = 4;
        System.out.println(wrapper(mat, n, m));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to find longest
# increasing path in a matrix.
MAX = 20

# Return the length of
# LIP in 2D matrix
def LIP(dp, mat, n, m, x, y):

    # If value not calculated yet.
    if (dp[x][y] < 0):
        result = 0

        # If reach bottom left cell,
        # return 1.
        if (x == n - 1 and y == m - 1):
            dp[x][y] = 1
            return dp[x][y]

        # If reach the corner
        # of the matrix.
        if (x == n - 1 or y == m - 1):
            result = 1

        # If value greater than below cell.
        if (x + 1 < n and mat[x][y] < mat[x + 1][y]):
            result = 1 + LIP(dp, mat, n,
                            m, x + 1, y)

        # If value greater than left cell.
        if (y + 1 < m and mat[x][y] < mat[x][y + 1]):
            result = max(result, 1 + LIP(dp, mat, n,
                                        m, x, y + 1))
        dp[x][y] = result
    return dp[x][y]

# Wrapper function
def wrapper(mat, n, m):
    dp = [[-1 for i in range(MAX)]
            for i in range(MAX)]
    return LIP(dp, mat, n, m, 0, 0)

# Driver Code
mat = [[1, 2, 3, 4 ],
    [2, 2, 3, 4 ],
    [3, 2, 3, 4 ],
    [4, 5, 6, 7 ]]
n = 4
m = 4
print(wrapper(mat, n, m))

# This code is contributed
# by Sahil Shelangia
```

## C#

```
// C# program to find longest increasing
// path in a matrix.
using System;

public class GFG {

    // Return the length of LIP in 2D matrix
    static int LIP(int[, ] dp, int[, ] mat, int n,
                   int m, int x, int y)
    {
        // If value not calculated yet.
        if (dp[x, y] < 0) {
            int result = 0;

            // If reach bottom left cell, return 1.
            if (x == n - 1 && y == m - 1)
                return dp[x, y] = 1;

            // If reach the corner of the matrix.
            if (x == n - 1 || y == m - 1)
                result = 1;

            // If value greater than below cell.
            if (x + 1 < n && mat[x, y] < mat[x + 1, y])
                result = 1 + LIP(dp, mat, n, m, x + 1, y);

            // If value greater than left cell.
            if (y + 1 < m && mat[x, y] < mat[x, y + 1])
                result = Math.Max(result, 1 + LIP(dp, mat, n, m, x, y + 1));

            dp[x, y] = result;
        }

        return dp[x, y];
    }

    // Wrapper function
    static int wrapper(int[, ] mat, int n, int m)
    {
        int[, ] dp = new int[10, 10];
        for (int i = 0; i < 10; i++) {
            for (int j = 0; j < 10; j++) {
                dp[i, j] = -1;
            }
        }

        return LIP(dp, mat, n, m, 0, 0);
    }

    /* Driver code */
    public static void Main()
    {
        int[, ] mat = {
            { 1, 2, 3, 4 },
            { 2, 2, 3, 4 },
            { 3, 2, 3, 4 },
            { 4, 5, 6, 7 },
        };
        int n = 4, m = 4;
        Console.WriteLine(wrapper(mat, n, m));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
    // Javascript program to find longest increasing path in a matrix.

    // Return the length of LIP in 2D matrix
    function LIP(dp, mat, n, m, x, y)
    {
        // If value not calculated yet.
        if (dp[x][y] < 0) {
            let result = 0;

            // If reach bottom left cell, return 1.
            if (x == n - 1 && y == m - 1)
                return dp[x][y] = 1;

            // If reach the corner of the matrix.
            if (x == n - 1 || y == m - 1)
                result = 1;

            // If value greater than below cell.
            if (x + 1 < n && mat[x][y] < mat[x + 1][y])
                result = 1 + LIP(dp, mat, n, m, x + 1, y);

            // If value greater than left cell.
            if (y + 1 < m && mat[x][y] < mat[x][y + 1])
                result = Math.max(result, 1 + LIP(dp, mat, n, m, x, y + 1));

            dp[x][y] = result;
        }

        return dp[x][y];
    }

    // Wrapper function
    function wrapper(mat, n, m)
    {
        let dp = new Array(10);
        for (let i = 0; i < 10; i++)
        {
            dp[i] = new Array(10);
            for (let j = 0; j < 10; j++)
            {
                dp[i][j] = -1;
            }
        }

        return LIP(dp, mat, n, m, 0, 0);
    }

    let mat = [
            [ 1, 2, 3, 4 ],
            [ 2, 2, 3, 4 ],
            [ 3, 2, 3, 4 ],
            [ 4, 5, 6, 7 ],
        ];
    let n = 4, m = 4;
    document.write(wrapper(mat, n, m));

</script>
```

**输出:**

```
7
```

**时间复杂度:** O(N*M)。
本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。