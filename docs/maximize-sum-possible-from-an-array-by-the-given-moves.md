# 通过给定的移动最大化数组中可能的和

> 原文:[https://www . geeksforgeeks . org/按给定的移动从数组中最大化可能的总和/](https://www.geeksforgeeks.org/maximize-sum-possible-from-an-array-by-the-given-moves/)

给定三个整数 **N、M** 和 **K** 以及一个由 **N** 个整数组成的数组**a【】**，其中 **M** 和 **K** 分别表示数组中当前元素左侧的可能移动的总数和可能移动的数量(移位一个索引)，任务是通过利用所有可用移动遍历数组来最大化可能的总和。

**示例:**

> **输入:** N = 5，M = 4，K = 0，a[] = {1，5，4，3，2}
> **输出:** 15
> **解释:**
> 由于不可能向左移动，因此，唯一可能的路径是 a[0]->a[1]->a[2]->a[3]->a[4]。
> 因此，计算出的总和为 15。
> **输入:** N = 5，M = 4，K = 1，a[]= {1，5，4，3，2}
> **输出:** 19
> **说明:**
> 在路径 a[0]->a[1]->a[2]->a[1]->a[2]
> 中可以得到的最大和因此

**方法:**上述问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。按照以下步骤解决问题:

*   初始化一个 **dp[][]** 矩阵，使得 **dp[i][j]** 通过使用 **j** 左移来存储最大可能和，直到 **i <sup>th</sup> 索引**。
*   可以观察到，只有当 **i ≥ 1** 和 **k > 0** 时，才可能向左移动，而当**I<n–1 时，才可能向右移动。**
*   检查条件并更新上述两次移动的最大可能总和，并存储在 **dp[i][j]** 中。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
const int k = 1;
const int m = 4;

// Function to find the maximum sum possible
// by given moves from the array
int maxValue(int a[], int n, int pos,
             int moves, int left,
             int dp[][k + 1])
{
    // Checking for boundary
    if (moves == 0 || (pos > n - 1 || pos < 0))
        return 0;

    // If previously computed subproblem occurs
    if (dp[pos][left] != -1)
        return dp[pos][left];

    int value = 0;

    // If element can be moved left
    if (left > 0 && pos >= 1)

        // Calculate maximum possible sum
        // by moving left from current index
        value = max(value, a[pos] +
                    maxValue(a, n, pos - 1, moves - 1,
                             left - 1, dp));

    // If element can be moved right
    if (pos <= n - 1)

        // Calculate maximum possible sum
        // by moving right from current index
        // and update the maximum sum
        value = max(value, a[pos] +
                    maxValue(a, n, pos + 1,
                             moves - 1, left, dp));

    // Store the maximum sum
    return dp[pos][left] = value;
}

// Driver Code
int main()
{
    int n = 5;
    int a[] = { 1, 5, 4, 3, 2 };

    int dp[n + 1][k + 1];
    memset(dp, -1, sizeof(dp));
    cout << (a[0] + maxValue(a, n, 1, m, k, dp))
         << endl;
}

// This code is contributed by sapnasingh4991
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
import java.util.*;

public class GFG {

    // Function to find the maximum sum possible
    // by given moves from the array
    public static int maxValue(int a[], int n, int pos,
                               int moves, int left,
                               int dp[][])
    {
        // Checking for boundary
        if (moves == 0 || (pos > n - 1 || pos < 0))
            return 0;

        // If previously computed subproblem occurs
        if (dp[pos][left] != -1)
            return dp[pos][left];

        int value = 0;

        // If element can be moved left
        if (left > 0 && pos >= 1)

            // Calculate maximum possible sum
            // by moving left from current index
            value = Math.max(
                value, a[pos] + maxValue(a, n, pos - 1,
                                         moves - 1, left - 1, dp));

        // If element can be moved right
        if (pos <= n - 1)

            // Calculate maximum possible sum
            // by moving right from current index
            // and update the maximum sum
            value = Math.max(
                value, a[pos]
                           + maxValue(a, n, pos + 1,
                                      moves - 1, left, dp));

        // Store the maximum sum
        return dp[pos][left] = value;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 5;
        int a[] = { 1, 5, 4, 3, 2 };
        int k = 1;
        int m = 4;

        int dp[][] = new int[n + 1][k + 1];
        for (int i[] : dp)
            Arrays.fill(i, -1);

        System.out.println(
            (a[0] + maxValue(a, n, 1, m, k, dp)));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum sum possible
# by given moves from the array
def maxValue(a, n, pos, moves, left, dp):

    # Checking for boundary
    if(moves == 0 or (pos > n - 1 or pos < 0)):
        return 0

    # If previously computed subproblem occurs
    if(dp[pos][left] != -1):
        return dp[pos][left]

    value = 0

    # If element can be moved left
    if(left > 0 and pos >= 1):

        # Calculate maximum possible sum
        # by moving left from current index
        value = max(value, a[pos] +
                    maxValue(a, n, pos - 1,
                                 moves - 1,
                                  left - 1, dp))

    # If element can be moved right
    if(pos <= n - 1):

        # Calculate maximum possible sum
        # by moving right from current index
        # and update the maximum sum
        value = max(value, a[pos] +
                    maxValue(a, n, pos + 1,
                                 moves - 1,
                                 left, dp))

    # Store the maximum sum
    dp[pos][left] = value

    return dp[pos][left]

# Driver Code
n = 5
a = [ 1, 5, 4, 3, 2 ]
k = 1
m = 4

dp = [[-1 for x in range(k + 1)]
          for y in range(n + 1)]

# Function call
print(a[0] + maxValue(a, n, 1, m, k, dp))

# This code is contributed by Shivam Singh
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG
{

  // Function to find the maximum sum possible
  // by given moves from the array
  public static int maxValue(int []a, int n, int pos,
                             int moves, int left,
                             int [,]dp)
  {
    // Checking for boundary
    if (moves == 0 || (pos > n - 1 || pos < 0))
      return 0;

    // If previously computed subproblem occurs
    if (dp[pos, left] != -1)
      return dp[pos, left];

    int value = 0;

    // If element can be moved left
    if (left > 0 && pos >= 1)

      // Calculate maximum possible sum
      // by moving left from current index
      value = Math.Max(
      value, a[pos] + maxValue(a, n, pos - 1,
                               moves - 1,
                               left - 1, dp));

    // If element can be moved right
    if (pos <= n - 1)

      // Calculate maximum possible sum
      // by moving right from current index
      // and update the maximum sum
      value = Math.Max(
      value, a[pos] + maxValue(a, n, pos + 1,
                                 moves - 1,
                               left, dp));

    // Store the maximum sum
    return dp[pos, left] = value;
  }

  // Driver Code
  public static void Main(String []args)
  {
    int n = 5;
    int []a = { 1, 5, 4, 3, 2 };
    int k = 1;
    int m = 4;

    int [,]dp = new int[n + 1, k + 1];
    for(int i = 0; i <= n; i++)
      for(int j =0; j <= k; j++)
        dp[i, j] = -1;

    Console.WriteLine(
     (a[0] + maxValue(a, n, 1, m, k, dp)));
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// JavaScript program for the
// above approach

   // Function to find the maximum sum possible
    // by given moves from the array
    function maxValue(a, n, pos, moves, left,
                               dp)
    {
        // Checking for boundary
        if (moves == 0 || (pos > n - 1 || pos < 0))
            return 0;

        // If previously computed subproblem occurs
        if (dp[pos][left] != -1)
            return dp[pos][left];

        let value = 0;

        // If element can be moved left
        if (left > 0 && pos >= 1)

            // Calculate maximum possible sum
            // by moving left from current index
            value = Math.max(
                value, a[pos] + maxValue(a, n, pos - 1,
                                         moves - 1, left - 1, dp));

        // If element can be moved right
        if (pos <= n - 1)

            // Calculate maximum possible sum
            // by moving right from current index
            // and update the maximum sum
            value = Math.max(
                value, a[pos]
                           + maxValue(a, n, pos + 1,
                                      moves - 1, left, dp));

        // Store the maximum sum
        return dp[pos][left] = value;
    }

// Driver Code

         let n = 5;
        let a = [ 1, 5, 4, 3, 2 ];
        let k = 1;
        let m = 4;

        let dp = new Array(n + 1);
        // Loop to create 2D array using 1D array
        for (var i = 0; i < dp.length; i++) {
            dp[i] = new Array(2);
        }

        for (var i = 0; i < dp.length; i++) {
            for (var j = 0; j < dp.length; j++) {
            dp[i][j] = -1;
        }
        }

        document.write(
            (a[0] + maxValue(a, n, 1, m, k, dp)));

</script>
```

**Output:** 

```
19
```

***时间复杂度:** O(N * K)*
***辅助空间:** O(N * K)*