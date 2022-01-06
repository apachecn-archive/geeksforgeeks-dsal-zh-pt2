# 通过从相邻的方块中选择不同颜色的钻石来最大化钻石

> 原文:[https://www . geeksforgeeks . org/通过从相邻的盒子中选择不同颜色的钻石来最大化钻石/](https://www.geeksforgeeks.org/maximize-the-diamonds-by-choosing-different-colour-diamonds-from-adjacent-boxes/)

给定两个整数 **N** 和 **M** ，其中 **N** 是一行中放置的盒子的数量， **M** 是分布在这些盒子中的钻石的颜色数量，使得每个盒子中至少包含 **1** 颗钻石。每个钻石都有一种颜色和一个由 **M * N** 矩阵表示的值，其中**mat【I】【j】**表示 **j <sup>th</sup>** 框中颜色为 **i** 的钻石数量。任务是从每个盒子中取出一种颜色的钻石，这样所选钻石的总价值最大，从相邻盒子中取出的钻石颜色不同。如果无法满足条件，则打印 **-1** 。

**示例:**

> **输入:** mat[][] = {
> {10，2，20，0}，
> {0，0，5，0}，
> {0，0，0，6}，
> {4，0，11，5}，
> {0，0，0，0，0}，
> {0，0，0，0，0}，
> {0，0，0，0}}
> **输出:** 23 【T12 但是由于从方框 2 中，我们必须选择 2 颗颜色 1 的钻石，因此从方框 1 中选择 4 颗颜色 4 的钻石。
> 同样，为了最大化钻石数量，从框 3 中选择 11 颗 Colour4 钻石，从框 4 中选择 6 颗 Colour3 钻石。
> 选择的钻石总数= 4 + 2 + 11 + 6 = 23，这是可能的最大数量。
> 
> **输入:** mat[][] = {
> {1，0，0}，
> {0，0，5}，
> {0，11，5}，
> {0，0，0}，
> {0，0，0}，
> {0，0，0}，
> {0，0，0}}
> **输出:** 16
> **说明:**我们选择

****进场:****

*   **[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以用来解决这个问题。**
*   **制作一个尺寸为 **M x N** 的二维数组，定义是通过选择**I<sup>th</sup>T5**j<sup>th</sup>T9】列的颜色可以得到的最大值。******
*   **递归关系为 **dp[i][j] = arr[i][j] +最大值(dp[1…M][i-1])** 。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the maximized value
int maxSum(vector<vector<int> > arr)
{

    // Number of rows and columns
    int m = (int)arr.size();
    int n = (int)arr[0].size() - 1;

    // Creating the Dp array
    int dp[m][n + 1];

    // memset(arr, 0, sizeof(arr));
    memset(dp, 0, sizeof(dp));

    // Populating the first column
    for (int i = 1; i < m; ++i)
        dp[i][1] = arr[i][1];

    for (int i = 1; i < n + 1; ++i) {

        // Iterating over all the rows
        for (int j = 1; j < m; ++j) {

            int mx = 0;

            // Getting the (i-1)th max value
            for (int k = 1; k < m; ++k) {
                if (k != j) {
                    if (dp[k][i - 1] > mx) {
                        mx = dp[k][i - 1];
                    }
                }
            }

            // Adding it to the current cell
            if (mx and arr[j][i]) {
                dp[j][i] = arr[j][i] + mx;
            }
        }
    }

    // Getting the max sum
    // from the last column
    int ans = -1;
    for (int i = 1; i <= m; ++i) {
        if (dp[i][n])
            ans = max(ans, dp[i][n]);
    }

    return ans;
}

// Driver code
int main()
{

    // Columns are indexed 1-based
    vector<vector<int> > arr = {
        { 0, 0, 0, 0, 0 },
        { 0, 10, 2, 20, 0 },
        { 0, 0, 0, 5, 0 },
        { 0, 0, 0, 0, 6 },
        { 0, 4, 0, 11, 5 },
        { 0, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0 },
        { 0, 0, 0, 0, 0 }
    };

    cout << maxSum(arr);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG{

// Function to return the maximized value
static int maxSum(int[][] arr)
{

    // Number of rows and columns
    int m = (int)arr.length;
    int n = (int)arr[0].length - 1;

    // Creating the Dp array
    int[][] dp = new int[m + 1][n + 2];

    // memset(arr, 0, sizeof(arr));
    for(int i = 0; i <= m; i++)
    {
        for(int j = 0; j <= n + 1; j++)
        {
            dp[i][j] = 0;
        }
    }

    // Populating the first column
    for(int i = 1; i < m; ++i)
        dp[i][1] = arr[i][1];

    for(int i = 1; i < n + 1; ++i)
    {

        // Iterating over all the rows
        for(int j = 1; j < m; ++j)
        {
            int mx = 0;

            // Getting the (i-1)th max value
            for(int k = 1; k < m; ++k)
            {
                if (k != j)
                {
                    if (dp[k][i - 1] > mx)
                    {
                        mx = dp[k][i - 1];
                    }
                }
            }

            // Adding it to the current cell
            if (mx != 0 && arr[j][i] != 0)
            {
                dp[j][i] = arr[j][i] + mx;
            }
        }
    }

    // Getting the max sum
    // from the last column
    int ans = -1;
    for(int i = 1; i <= m; ++i)
    {
        if ((dp[i][n]) != 0)
            ans = Math.max(ans, dp[i][n]);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Columns are indexed 1-based
    int[][] arr = { { 0, 0, 0, 0, 0 },
                    { 0, 10, 2, 20, 0 },
                    { 0, 0, 0, 5, 0 },
                    { 0, 0, 0, 0, 6 },
                    { 0, 4, 0, 11, 5 },
                    { 0, 0, 0, 0, 0 },
                    { 0, 0, 0, 0, 0 },
                    { 0, 0, 0, 0, 0 } };

    System.out.println(maxSum(arr));
}
}

// This code is contributed by sanjoy_62
```

## **蟒蛇 3**

```
# Python 3 implementation of the approach

# Function to return the maximized value
def maxSum(arr):

    # Number of rows and columns
    m = len(arr)
    n = len(arr[0]) - 1

    # Creating the Dp array
    dp = [[0 for i in range(n+1)] for j in range(m)]

    # Populating the first column
    for i in range(1,m,1):
        dp[i][1] = arr[i][1]

    for i in range(1,n + 1,1):

        # Iterating over all the rows
        for j in range(1,m,1):
            mx = 0

            # Getting the (i-1)th max value
            for k in range(1,m,1):
                if (k != j):
                    if (dp[k][i - 1] > mx):
                        mx = dp[k][i - 1]

            # Adding it to the current cell
            if (mx and arr[j][i]):
                dp[j][i] = arr[j][i] + mx

    # Getting the max sum
    # from the last column
    ans = -1
    for i in range(1,m,1):
        if (dp[i][n]):
            ans = max(ans, dp[i][n])

    return ans

# Driver code
if __name__ == '__main__':

    # Columns are indexed 1-based
    arr = [[0, 0, 0, 0, 0],
           [0, 10, 2, 20, 0],
           [0, 0, 0, 5, 0],
           [0, 0, 0, 0, 6],
           [0, 4, 0, 11, 5],
           [0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0],
           [0, 0, 0, 0, 0]]

    print(maxSum(arr))

    # This coe is contributed by bgangwar59.
```

## **C#**

```
// C# implementation of the approach
using System;
public class GFG
{

// Function to return the maximized value
static int maxSum(int[,] arr)
{

    // Number of rows and columns
    int m = (int)arr.GetLength(0);
    int n = (int)arr.GetLength(1) - 1;

    // Creating the Dp array
    int[,] dp = new int[m + 1,n + 2];

    // memset(arr, 0, sizeof(arr));
    for(int i = 0; i <= m; i++)
    {
        for(int j = 0; j <= n + 1; j++)
        {
            dp[i,j] = 0;
        }
    }

    // Populating the first column
    for(int i = 1; i < m; ++i)
        dp[i,1] = arr[i,1];

    for(int i = 1; i < n + 1; ++i)
    {

        // Iterating over all the rows
        for(int j = 1; j < m; ++j)
        {
            int mx = 0;

            // Getting the (i-1)th max value
            for(int k = 1; k < m; ++k)
            {
                if (k != j)
                {
                    if (dp[k,i - 1] > mx)
                    {
                        mx = dp[k,i - 1];
                    }
                }
            }

            // Adding it to the current cell
            if (mx != 0 && arr[j,i] != 0)
            {
                dp[j,i] = arr[j,i] + mx;
            }
        }
    }

    // Getting the max sum
    // from the last column
    int ans = -1;
    for(int i = 1; i <= m; ++i)
    {
        if ((dp[i,n]) != 0)
            ans = Math.Max(ans, dp[i,n]);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{

    // Columns are indexed 1-based
    int[,] arr = { { 0, 0, 0, 0, 0 },
                    { 0, 10, 2, 20, 0 },
                    { 0, 0, 0, 5, 0 },
                    { 0, 0, 0, 0, 6 },
                    { 0, 4, 0, 11, 5 },
                    { 0, 0, 0, 0, 0 },
                    { 0, 0, 0, 0, 0 },
                    { 0, 0, 0, 0, 0 } };

    Console.WriteLine(maxSum(arr));
}
}

// This code is contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>
// Javascript implementation of the approach

// Function to return the maximized value
function maxSum(arr)
{

  // Number of rows and columns
  let m = arr.length;
  let n = arr[0].length - 1;

  // Creating the Dp array
  let dp = new Array(m + 1).fill(0).map(() => new Array(n + 1).fill(0));

  // Populating the first column
  for (let i = 1; i < m; ++i) dp[i][1] = arr[i][1];

  for (let i = 1; i < n + 1; ++i) {
    // Iterating over all the rows
    for (let j = 1; j < m; ++j) {
      let mx = 0;

      // Getting the (i-1)th max value
      for (let k = 1; k < m; ++k) {
        if (k != j) {
          if (dp[k][i - 1] > mx) {
            mx = dp[k][i - 1];
          }
        }
      }

      // Adding it to the current cell
      if (mx && arr[j][i]) {
        dp[j][i] = arr[j][i] + mx;
      }
    }
  }

  // Getting the max sum
  // from the last column
  let ans = -1;
  for (let i = 1; i <= m; ++i) {
    if (dp[i][n]) {ans = Math.max(ans, dp[i][n])};
  }

  return ans;
}

// Driver code
// Columns are indexed 1-based
let arr = [
  [0, 0, 0, 0, 0],
  [0, 10, 2, 20, 0],
  [0, 0, 0, 5, 0],
  [0, 0, 0, 0, 6],
  [0, 4, 0, 11, 5],
  [0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0],
  [0, 0, 0, 0, 0],
];

document.write(maxSum(arr));

// This code is contributed by gfgking.
</script>
```

****Output:** 

```
23
```**