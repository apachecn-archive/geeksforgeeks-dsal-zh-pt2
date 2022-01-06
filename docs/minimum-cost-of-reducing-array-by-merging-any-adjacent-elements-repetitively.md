# 通过重复合并任何相邻元素来减少数组的最小成本

> 原文:[https://www . geeksforgeeks . org/通过重复合并任何相邻元素来减少数组的最小成本/](https://www.geeksforgeeks.org/minimum-cost-of-reducing-array-by-merging-any-adjacent-elements-repetitively/)

给定一个由 **N** 个数字组成的数组 **arr[]** 。我们可以将两个相邻的数字合并成一个，合并这两个数字的成本等于这两个值的总和。任务是找到合并所有数字的最小总成本。
**例:**

> **输入:** arr[] = { 6，4，4，6 }
> **输出:** 40
> **说明:**
> 以下是合并号码的最优方式，得到号码合并的总最小成本:
> 1。合并(6，4)，然后数组变成，arr[] = {10，4，6}，成本= 10
> 2。合并(4，6)，然后数组变成，arr[] = {10，10}，成本= 10
> 3。合并(10，10)，然后数组变成，arr[] = {20}，成本= 20
> 因此总成本为 10 + 10 + 20 = 40。
> **输入:** arr[] = { 3，2，4，1 }
> **输出:** 20
> **说明:**
> 以下是合并数字的最优方式，得到数字合并的总最小成本:
> 1。合并(3，2)，然后数组变成，arr[] = {5，4，1}，成本= 5
> 2。合并(4，1)，然后数组变成，arr[] = {5，5}，成本= 5
> 3。合并(5，5)，然后数组变成，arr[] = {10}，成本= 10
> 因此总成本为 5 + 5 + 10 = 20。

**方法:**使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。以下是步骤:

1.  想法是将 **2 个连续的数字**合并到每个可能的索引 **i** 中，然后递归求解索引 **i** 的左右部分。
2.  将以上步骤中两个数合并的结果相加，并存储其中的最小值。
3.  由于有许多子问题在重复，因此我们使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)将值存储在 **NxN** 矩阵中。
4.  上述问题陈述的递推关系如下:

> dp[i][j] = min(dp[i][j]，(总和[i][j] + dp[i][k] + dp[k + 1][j])，每一(I≤k lt；j)

5.现在 **dp[1][N]** 将给出合并所有数字的最小总成本。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the total minimum
// cost of merging two consecutive numbers
int mergeTwoNumbers(vector<int>& numbers)
{
    int len, i, j, k;

    // Find the size of numbers[]
    int n = numbers.size();

    // If array is empty, return 0
    if (numbers.size() == 0) {
        return 0;
    }

    // To store the prefix Sum of
    // numbers array numbers[]
    vector<int> prefixSum(n + 1, 0);

    // Traverse numbers[] to find the
    // prefix sum
    for (int i = 1; i <= n; i++) {
        prefixSum[i] = prefixSum[i - 1]
                       + numbers[i - 1];
    }

    // dp table to memoised the value
    vector<vector<int> > dp(
        n + 1,
        vector<int>(n + 1));

    // For single numbers cost is zero
    for (int i = 1; i <= n; i++) {
        dp[i][i] = 0;
    }

    // Iterate for length >= 1
    for (len = 2; len <= n; len++) {

        for (i = 1; i <= n - len + 1; i++) {
            j = i + len - 1;

            // Find sum in range [i..j]
            int sum = prefixSum[j]
                      - prefixSum[i - 1];

            // Initialise dp[i][j] to INT_MAX
            dp[i][j] = INT_MAX;

            // Iterate for all possible
            // K to find the minimum cost
            for (k = i; k < j; k++) {

                // Update the minimum sum
                dp[i][j]
                    = min(dp[i][j],
                          dp[i][k]
                              + dp[k + 1][j]
                              + sum);
            }
        }
    }

    // Return the final minimum cost
    return dp[1][n];
}

// Driver Code
int main()
{
    // Given set of numbers
    vector<int> arr1 = { 6, 4, 4, 6 };

    // Function Call
    cout << mergeTwoNumbers(arr1)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the total minimum
// cost of merging two consecutive numbers
static int mergeTwoNumbers(int []numbers)
{
    int len, i, j, k;

    // Find the size of numbers[]
    int n = numbers.length;

    // If array is empty, return 0
    if (numbers.length == 0)
    {
        return 0;
    }

    // To store the prefix Sum of
    // numbers array numbers[]
    int []prefixSum = new int[n + 1];

    // Traverse numbers[] to find the
    // prefix sum
    for (i = 1; i <= n; i++)
    {
        prefixSum[i] = prefixSum[i - 1] +
                         numbers[i - 1];
    }

    // dp table to memoised the value
    int [][]dp = new int[n + 1][n + 1];

    // Iterate for length >= 1
    for (len = 2; len <= n; len++)
    {

        for (i = 1; i <= n - len + 1; i++)
        {
            j = i + len - 1;

            // Find sum in range [i..j]
            int sum = prefixSum[j] -
                      prefixSum[i - 1];

            // Initialise dp[i][j] to Integer.MAX_VALUE
            dp[i][j] = Integer.MAX_VALUE;

            // Iterate for all possible
            // K to find the minimum cost
            for (k = i; k < j; k++)
            {

                // Update the minimum sum
                dp[i][j] = Math.min(dp[i][j],
                                    dp[i][k] +
                                    dp[k + 1][j] +
                                    sum);
            }
        }
    }

    // Return the final minimum cost
    return dp[1][n];
}

// Driver Code
public static void main(String[] args)
{
    // Given set of numbers
    int []arr1 = { 6, 4, 4, 6 };

    // Function Call
    System.out.print(mergeTwoNumbers(arr1) + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the total minimum
# cost of merging two consecutive numbers
def mergeTwoNumbers(numbers):

    # Find the size of numbers[]
    n = len(numbers)

    # If array is empty, return 0
    if (len(numbers) == 0):
        return 0

    # To store the prefix Sum of
    # numbers array numbers[]
    prefixSum = [0] * (n + 1)

    # Traverse numbers[] to find the
    # prefix sum
    for i in range(1, n + 1):
        prefixSum[i] = (prefixSum[i - 1] +
                          numbers[i - 1])

    # dp table to memoised the value
    dp = [[0 for i in range(n + 1)]
             for j in range(n + 1)]

    # For single numbers cost is zero
    for i in range(1, n + 1):
        dp[i][i] = 0

    # Iterate for length >= 1
    for p in range(2, n + 1):
        for i in range(1, n - p + 2):
            j = i + p - 1

            # Find sum in range [i..j]
            sum = prefixSum[j] - prefixSum[i - 1]

            # Initialise dp[i][j] to _MAX
            dp[i][j] = sys.maxsize

            # Iterate for all possible
            # K to find the minimum cost
            for k in range(i, j):

                # Update the minimum sum
                dp[i][j] = min(dp[i][j],
                              (dp[i][k] +
                               dp[k + 1][j] + sum))

    # Return the final minimum cost
    return dp[1][n]

# Driver Code

# Given set of numbers
arr1 = [ 6, 4, 4, 6 ]

# Function call
print(mergeTwoNumbers(arr1))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the total minimum
// cost of merging two consecutive numbers
static int mergeTwoNumbers(int []numbers)
{
    int len, i, j, k;

    // Find the size of numbers[]
    int n = numbers.Length;

    // If array is empty, return 0
    if (numbers.Length == 0)
    {
        return 0;
    }

    // To store the prefix Sum of
    // numbers array numbers[]
    int []prefixSum = new int[n + 1];

    // Traverse numbers[] to find the
    // prefix sum
    for (i = 1; i <= n; i++)
    {
        prefixSum[i] = prefixSum[i - 1] +
                         numbers[i - 1];
    }

    // dp table to memoised the value
    int [,]dp = new int[n + 1, n + 1];

    // Iterate for length >= 1
    for (len = 2; len <= n; len++)
    {

        for (i = 1; i <= n - len + 1; i++)
        {
            j = i + len - 1;

            // Find sum in range [i..j]
            int sum = prefixSum[j] -
                      prefixSum[i - 1];

            // Initialise dp[i,j] to int.MaxValue
            dp[i,j] = int.MaxValue;

            // Iterate for all possible
            // K to find the minimum cost
            for (k = i; k < j; k++)
            {

                // Update the minimum sum
                dp[i, j] = Math.Min(dp[i, j],
                                    dp[i, k] +
                                    dp[k + 1, j] +
                                    sum);
            }
        }
    }

    // Return the readonly minimum cost
    return dp[1, n];
}

// Driver Code
public static void Main(String[] args)
{
    // Given set of numbers
    int []arr1 = { 6, 4, 4, 6 };

    // Function Call
    Console.Write(mergeTwoNumbers(arr1) + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the total minimum
// cost of merging two consecutive numbers
function mergeTwoNumbers(numbers)
{
    var len, i, j, k;

    // Find the size of numbers[]
    var n = numbers.length;

    // If array is empty, return 0
    if (numbers.length == 0) {
        return 0;
    }

    // To store the prefix Sum of
    // numbers array numbers[]
    var prefixSum = Array(n+1).fill(0);

    // Traverse numbers[] to find the
    // prefix sum
    for (var i = 1; i <= n; i++) {
        prefixSum[i] = prefixSum[i - 1]
                       + numbers[i - 1];
    }

    // dp table to memoised the value
    var dp = Array.from(Array(n+1), ()=>Array(n+1));

    // For single numbers cost is zero
    for (var i = 1; i <= n; i++) {
        dp[i][i] = 0;
    }

    // Iterate for length >= 1
    for (len = 2; len <= n; len++) {

        for (i = 1; i <= n - len + 1; i++) {
            j = i + len - 1;

            // Find sum in range [i..j]
            var sum = prefixSum[j]
                      - prefixSum[i - 1];

            // Initialise dp[i][j] to INT_MAX
            dp[i][j] = 1000000000;

            // Iterate for all possible
            // K to find the minimum cost
            for (k = i; k < j; k++) {

                // Update the minimum sum
                dp[i][j]
                    = Math.min(dp[i][j],
                          dp[i][k]
                              + dp[k + 1][j]
                              + sum);
            }
        }
    }

    // Return the final minimum cost
    return dp[1][n];
}

// Driver Code

// Given set of numbers
var arr1 = [6, 4, 4, 6];

// Function Call
document.write( mergeTwoNumbers(arr1))

</script>
```

**Output:** 

```
40
```

**时间复杂度:***O(N<sup>3</sup>)*
T7】辅助空间复杂度:*O(N<sup>2</sup>)*