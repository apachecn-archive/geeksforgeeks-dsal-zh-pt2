# 通过从矩阵的不同部分选择元素来最大化总和

> 原文:[https://www . geeksforgeeks . org/通过从矩阵的不同部分中选择元素来最大化总和/](https://www.geeksforgeeks.org/maximize-sum-by-choosing-elements-from-different-section-of-a-matrix/)

给定一个由 **N** 行和 **M** 列组成的矩阵。给出 **M** 是 3 的倍数。列分为 3 段，第一段从 0 到 m/3-1，第二段从 m/3 到 2m/3-1，第三段从 2m/3 到 m。任务是从每行中选择一个元素，在相邻的行中，我们不能从同一段中选择。我们必须最大化所选元素的总和。
**举例:**

> **输入:** mat[][] = {
> {1，3，5，2，4，6}，
> {6，4，5，1，3，2}，
> {1，3，5，2，4，6}，
> {6，4，5，1，3，2}，
> {6，4，5，1，3，2}，
> {1，3，5，2，4，6}}
> **输出:【T10**

**方法:**通过存储子问题并重用它们，可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决方案来解决问题。创建一个 **dp[][]** 数组，其中 **dp[i][0]** 表示从 **0** 到 **i** 的行的元素之和，从 **1** 部分获取元素。同样，对于 **dp[i][1]** 和 **dp[i][2]** 。因此，打印**最大值(DP[n–1][0]、DP[n–1][1]、DP[n–1][2]**。
以下是上述办法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

const int n = 6, m = 6;

// Function to find the maximum value
void maxSum(long arr[n][m])
{
    // Dp table
    long dp[n + 1][3] = { 0 };

    // Fill the dp in bottom
    // up manner
    for (int i = 0; i < n; i++) {

        // Maximum of the three sections
        long m1 = 0, m2 = 0, m3 = 0;

        for (int j = 0; j < m; j++) {

            // Maximum of the first section
            if ((j / (m / 3)) == 0) {
                m1 = max(m1, arr[i][j]);
            }

            // Maximum of the second section
            else if ((j / (m / 3)) == 1) {
                m2 = max(m2, arr[i][j]);
            }

            // Maximum of the third section
            else if ((j / (m / 3)) == 2) {
                m3 = max(m3, arr[i][j]);
            }
        }

        // If we choose element from section 1,
        // we cannot have selection from same section
        // in adjacent rows
        dp[i + 1][0] = max(dp[i][1], dp[i][2]) + m1;
        dp[i + 1][1] = max(dp[i][0], dp[i][2]) + m2;
        dp[i + 1][2] = max(dp[i][1], dp[i][0]) + m3;
    }

    // Print the maximum sum
    cout << max(max(dp[n][0], dp[n][1]), dp[n][2]) << '\n';
}

// Driver code
int main()
{

    long arr[n][m] = { { 1, 3, 5, 2, 4, 6 },
                       { 6, 4, 5, 1, 3, 2 },
                       { 1, 3, 5, 2, 4, 6 },
                       { 6, 4, 5, 1, 3, 2 },
                       { 6, 4, 5, 1, 3, 2 },
                       { 1, 3, 5, 2, 4, 6 } };

    maxSum(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

static int n = 6, m = 6;

// Function to find the maximum value
static void maxSum(long arr[][])
{
    // Dp table
    long [][]dp= new long[n + 1][3];

    // Fill the dp in bottom
    // up manner
    for (int i = 0; i < n; i++)
    {

        // Maximum of the three sections
        long m1 = 0, m2 = 0, m3 = 0;

        for (int j = 0; j < m; j++)
        {

            // Maximum of the first section
            if ((j / (m / 3)) == 0)
            {
                m1 = Math.max(m1, arr[i][j]);
            }

            // Maximum of the second section
            else if ((j / (m / 3)) == 1)
            {
                m2 = Math.max(m2, arr[i][j]);
            }

            // Maximum of the third section
            else if ((j / (m / 3)) == 2)
            {
                m3 = Math.max(m3, arr[i][j]);
            }
        }

        // If we choose element from section 1,
        // we cannot have selection from same section
        // in adjacent rows
        dp[i + 1][0] = Math.max(dp[i][1], dp[i][2]) + m1;
        dp[i + 1][1] = Math.max(dp[i][0], dp[i][2]) + m2;
        dp[i + 1][2] = Math.max(dp[i][1], dp[i][0]) + m3;
    }

    // Print the maximum sum
    System.out.print(Math.max(Math.max(dp[n][0], dp[n][1]), dp[n][2]) + "\n");
}

// Driver code
public static void main(String[] args)
{

    long arr[][] = { { 1, 3, 5, 2, 4, 6 },
                    { 6, 4, 5, 1, 3, 2 },
                    { 1, 3, 5, 2, 4, 6 },
                    { 6, 4, 5, 1, 3, 2 },
                    { 6, 4, 5, 1, 3, 2 },
                    { 1, 3, 5, 2, 4, 6 } };

    maxSum(arr);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for the above approach
import numpy as np
n = 6; m = 6;

# Function to find the maximum value
def maxSum(arr) :

    # Dp table
    dp = np.zeros((n + 1, 3));

    # Fill the dp in bottom
    # up manner
    for i in range(n) :

        # Maximum of the three sections
        m1 = 0; m2 = 0; m3 = 0;

        for j in range(m) :

            # Maximum of the first section
            if ((j // (m // 3)) == 0) :
                m1 = max(m1, arr[i][j]);

            # Maximum of the second section
            elif ((j // (m // 3)) == 1) :
                m2 = max(m2, arr[i][j]);

            # Maximum of the third section
            elif ((j // (m // 3)) == 2) :
                m3 = max(m3, arr[i][j]);

        # If we choose element from section 1,
        # we cannot have selection from same section
        # in adjacent rows
        dp[i + 1][0] = max(dp[i][1], dp[i][2]) + m1;
        dp[i + 1][1] = max(dp[i][0], dp[i][2]) + m2;
        dp[i + 1][2] = max(dp[i][1], dp[i][0]) + m3;

    # Print the maximum sum
    print(max(max(dp[n][0], dp[n][1]), dp[n][2]));

# Driver code
if __name__ == "__main__" :

    arr = [[ 1, 3, 5, 2, 4, 6 ],
           [ 6, 4, 5, 1, 3, 2 ],
           [ 1, 3, 5, 2, 4, 6 ],
           [ 6, 4, 5, 1, 3, 2 ],
           [ 6, 4, 5, 1, 3, 2 ],
           [ 1, 3, 5, 2, 4, 6 ]];

    maxSum(arr);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;

class GFG
{
static int n = 6, m = 6;

// Function to find the maximum value
static void maxSum(long [,]arr)
{
    // Dp table
    long [,]dp = new long[n + 1, 3];

    // Fill the dp in bottom
    // up manner
    for (int i = 0; i < n; i++)
    {

        // Maximum of the three sections
        long m1 = 0, m2 = 0, m3 = 0;

        for (int j = 0; j < m; j++)
        {

            // Maximum of the first section
            if ((j / (m / 3)) == 0)
            {
                m1 = Math.Max(m1, arr[i, j]);
            }

            // Maximum of the second section
            else if ((j / (m / 3)) == 1)
            {
                m2 = Math.Max(m2, arr[i, j]);
            }

            // Maximum of the third section
            else if ((j / (m / 3)) == 2)
            {
                m3 = Math.Max(m3, arr[i, j]);
            }
        }

        // If we choose element from section 1,
        // we cannot have selection from same section
        // in adjacent rows
        dp[i + 1, 0] = Math.Max(dp[i, 1], dp[i, 2]) + m1;
        dp[i + 1, 1] = Math.Max(dp[i, 0], dp[i, 2]) + m2;
        dp[i + 1, 2] = Math.Max(dp[i, 1], dp[i, 0]) + m3;
    }

    // Print the maximum sum
    Console.Write(Math.Max(Math.Max(dp[n, 0],
                                    dp[n, 1]),
                                    dp[n, 2]) + "\n");
}

// Driver code
public static void Main(String[] args)
{
    long [,]arr = { { 1, 3, 5, 2, 4, 6 },
                    { 6, 4, 5, 1, 3, 2 },
                    { 1, 3, 5, 2, 4, 6 },
                    { 6, 4, 5, 1, 3, 2 },
                    { 6, 4, 5, 1, 3, 2 },
                    { 1, 3, 5, 2, 4, 6 } };

    maxSum(arr);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

const n = 6, m = 6;

// Function to find the maximum value
function maxSum(arr)
{
    // Dp table
    const dp = new Array(n+1).fill(0).map(() => new Array(3).fill(0));

    // Fill the dp in bottom
    // up manner
    for (var i = 0; i < n; i++) {

        // Maximum of the three sections
        var m1 = 0, m2 = 0, m3 = 0;

        for (var j = 0; j < m; j++) {

            // Maximum of the first section
            if (parseInt(j / (m / 3)) == 0) {
                m1 = Math.max(m1, arr[i][j]);
            }

            // Maximum of the second section
            else if (parseInt(j / (m / 3)) == 1) {
                m2 = Math.max(m2, arr[i][j]);
            }

            // Maximum of the third section
            else if (parseInt(j / (m / 3)) == 2) {
                m3 = Math.max(m3, arr[i][j]);
            }
        }

        // If we choose element from section 1,
        // we cannot have selection from same section
        // in adjacent rows
        dp[i + 1][0] = Math.max(dp[i][1], dp[i][2]) + m1;
        dp[i + 1][1] = Math.max(dp[i][0], dp[i][2]) + m2;
        dp[i + 1][2] = Math.max(dp[i][1], dp[i][0]) + m3;
    }

    // Print the maximum sum
    document.write( parseInt(Math.max(Math.max(dp[n][0], dp[n][1]), dp[n][2])) + "<br>");
}

arr = [ [ 1, 3, 5, 2, 4, 6 ],
        [ 6, 4, 5, 1, 3, 2 ],
        [ 1, 3, 5, 2, 4, 6 ],
        [ 6, 4, 5, 1, 3, 2 ],
        [ 6, 4, 5, 1, 3, 2 ],
        [ 1, 3, 5, 2, 4, 6 ] ];

maxSum(arr);

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
35
```

**时间复杂度:** O(N*M)