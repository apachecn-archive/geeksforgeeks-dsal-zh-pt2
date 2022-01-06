# 由不同奇偶性的连续元素组成的最大和子序列

> 原文:[https://www . geesforgeks . org/最大和子序列-由不同奇偶校验的连续元素组成/](https://www.geeksforgeeks.org/maximum-sum-subsequence-made-up-of-consecutive-elements-of-different-parity/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到非空[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大和，使得每对连续项具有不同的[奇偶性](https://www.geeksforgeeks.org/program-to-find-parity/) ( *偶数*或*奇数*)。

**示例:**

> **输入:** arr[] = {1，2，6，8，-5，10}
> **输出:** 14
> **解释:**考虑满足给定条件的子序列{1，8，-5，10}，子序列的和=(1+8–5+10)= 14，这是最大可能和。
> 
> **输入:** arr[] = {1，-1，1，-1}
> **输出:** 1

**天真方法:**解决给定问题的最简单方法是[生成数组的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，并找到具有不同奇偶性的所有相邻元素的子序列的最大和。

***时间复杂度:**O(N *(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为它有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)可以将子问题存储在 **dp[][]** 表中，其中 **dp[i][prev]** 存储从**第一个位置**到数组末尾的最大可能和，此时选择的前一个数的奇偶性为**“prev”**。每个州有两种情况:

*   如果奇偶校验不同于前一个元素，则包括当前元素。
*   不包括当前元素。

保持布尔变量**被选择**以确保至少从子序列中的数组中选择一个数字，然后在每个[递归调用](https://www.geeksforgeeks.org/recursion/)中返回两种情况中的最大值。按照以下步骤解决问题:

*   通过执行以下步骤定义[递归](https://www.geeksforgeeks.org/recursive-functions/)函数 **maxSum(i，prev，is_selected)** :
    *   检查基本情况，如果 **i** 的值等于 **N** ，则返回 **0** ，或者如果 **i** 的值等于**N–1**，**被 _ 选中**为**假**，则返回**arr【I】**。
    *   如果已经计算出状态 **dp[i][prev]** 的结果，则返回该状态 **dp[i][prev]** 。
    *   如果当前元素的奇偶性与 **prev** 不同，则选择当前元素作为子集的一部分，并且[递归地](https://www.geeksforgeeks.org/recursion/)为索引 **(i + 1)** 处的元素调用 **maxSum** 函数。
    *   跳过当前子集的当前元素，[递归地](https://www.geeksforgeeks.org/recursion/)调用 **maxSum** 函数来索引 **(i + 1)** 。
    *   从当前递归调用中返回这两种情况的最大值。
*   完成以上步骤后，打印 **maxSum(0)** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

int dp[100][3];

// Function to find the maximum sum of
// subsequence with consecutive terms
// having different parity
int maxSum(int* arr, int i, int n,
           int prev, bool is_selected)
{
    // Base Case
    if (i == n) {
        return 0;
    }

    // Store the parity of number at
    // the ith position
    int cur = abs(arr[i]) % 2;

    // If the dp state has already been
    // calculated, return it
    if (dp[i][prev] != -1) {
        return dp[i][prev];
    }

    // If the array is traversed and
    // no element has been selected yet
    // then select the current element
    if (i == n - 1 && is_selected == 0)
        return dp[i][prev] = arr[i];

    // If the parity of the current and
    // previously selected element are
    // different, then select the
    // current element
    if (cur != prev) {
        dp[i][prev] = arr[i]
                      + maxSum(arr, i + 1,
                               n, cur, 1);
    }

    // Skip the current element and move
    // to the next element
    dp[i][prev]
        = max(dp[i][prev],
              maxSum(arr, i + 1, n,
                     prev, is_selected));

    // Return the result
    return dp[i][prev];
}

// Function to calculate the maximum sum
// subsequence with consecutive terms
// having different parity
void maxSumUtil(int arr[], int n)
{

    // Initialize the dp[] array with -1
    memset(dp, -1, sizeof(dp));

    // Initially the prev value is set to
    // say 2, as the first element can
    // anyways be selected
    cout << maxSum(arr, 0, n, 2, 0);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 6, 8, -5, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);
    maxSumUtil(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

// Function to find the maximum sum of
// subsequence with consecutive terms
// having different parity
static int maxSum(int[] arr, int i, int n, int prev,
                  boolean is_selected, int[][] dp)
{

    // Base Case
    if (i == n)
    {
        return 0;
    }

    // Store the parity of number at
    // the ith position
    int cur = Math.abs(arr[i]) % 2;

    // If the dp state has already been
    // calculated, return it
    if (dp[i][prev] != -1)
    {
        return dp[i][prev];
    }

    // If the array is traversed and
    // no element has been selected yet
    // then select the current element
    if (i == n - 1 && is_selected == false)
        return dp[i][prev] = arr[i];

    // If the parity of the current and
    // previously selected element are
    // different, then select the
    // current element
    if (cur != prev)
    {
        dp[i][prev] = arr[i] + maxSum(arr, i + 1, n,
                                      cur, true, dp);
    }

    // Skip the current element and move
    // to the next element
    dp[i][prev] = Math.max(dp[i][prev], maxSum(
        arr, i + 1, n, prev, is_selected, dp));

    // Return the result
    return dp[i][prev];
}

// Function to calculate the maximum sum
// subsequence with consecutive terms
// having different parity
static void maxSumUtil(int arr[], int n)
{
      int [][]dp = new int[100][3];

    // Initialize the dp[] array with -1
    for(int[] arr1 : dp)
        Arrays.fill(arr1, -1);

    // Initially the prev value is set to
    // say 2, as the first element can
    // anyways be selected
    System.out.print(maxSum(arr, 0, n, 2, false, dp));
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 6, 8, -5, 10 };
    int N = arr.length;

    maxSumUtil(arr, N);
}
}

// This code is contributed by shreyasshetty788
```

## 蟒蛇 3

```
# Python3 code for the above approach

# Function to calculate the maximum sum
# subsequence with consecutive terms
# having different parity
def maxSum(arr, i, n, prev, is_selected, dp):

    # Base Case
    if(i == n):
        return 0

    # Store the parity of number at
    # the ith position
    cur = abs(arr[i]) % 2

    # If the dp state has already been
    # calculated, return it
    if (dp[i][prev] != -1):
        return dp[i][prev]

    # If the array is traversed and
    # no element has been selected yet
    # then select the current element
    if (i == n - 1 and is_selected == 0):
        dp[i][prev] = arr[i]
        return dp[i][prev]

    # If the parity of the current and
    # previously selected element are
    # different, then select the
    # current element
    if (cur != prev):
        dp[i][prev] = arr[i] + maxSum(arr, i + 1,
                                      n, cur, 1, dp)

    # Skip the current element and move
    # to the next element
    dp[i][prev] = max(dp[i][prev], maxSum(
        arr, i + 1, n, prev, is_selected, dp))

    # Return the result
    return dp[i][prev]

# Function to calculate the maximum sum
# subsequence with consecutive terms
# having different parity
def maxSumUtil(arr, n):

    dp = [[-1 for i in range(3)]
              for j in range(100)]

    print(maxSum(arr, 0, n, 2, 0, dp))

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 6, 8, -5, 10 ]
    N = len(arr)

    maxSumUtil(arr, N)

# This code is contributed by shreyasshetty788
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum sum of
// subsequence with consecutive terms
// having different parity
static int maxSum(int []arr, int i, int n, int prev,
                  bool is_selected, int [,]dp)
{

    // Base Case
    if (i == n)
    {
        return 0;
    }

    // Store the parity of number at
    // the ith position
    int cur = Math.Abs(arr[i]) % 2;

    // If the dp state has already been
    // calculated, return it
    if (dp[i, prev] != -1)
    {
        return dp[i, prev];
    }

    // If the array is traversed and
    // no element has been selected yet
    // then select the current element
    if (i == n - 1 && is_selected == false)
        return dp[i, prev] = arr[i];

    // If the parity of the current and
    // previously selected element are
    // different, then select the
    // current element
    if (cur != prev)
    {
        dp[i, prev] = arr[i] + maxSum(arr, i + 1, n,
                                      cur, true, dp);
    }

    // Skip the current element and move
    // to the next element
    dp[i, prev] = Math.Max(dp[i, prev], maxSum(
        arr, i + 1, n, prev, is_selected, dp));

    // Return the result
    return dp[i, prev];
}

// Function to calculate the maximum sum
// subsequence with consecutive terms
// having different parity
static void maxSumUtil(int []arr, int n)
{
    int [,]dp = new int[100, 3];

    // Initialize the dp[] array with -1
    for(int i = 0; i < 100; ++i)
    {
        for(int j = 0; j < 3; ++j)
        {
            dp[i, j] = -1;
        }
    }

    // Initially the prev value is set to
    // say 2, as the first element can
    // anyways be selected
    Console.Write(maxSum(arr, 0, n, 2, false, dp));
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 2, 6, 8, -5, 10 };
    int N = arr.Length;

    maxSumUtil(arr, N);
}
}

// This code is contributed by shreyasshetty788
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

let dp = new Array(100).fill(0).map(() =>
new Array(3).fill(-1));

// Function to find the maximum sum of
// subsequence with consecutive terms
// having different parity
function maxSum(arr, i, n, prev, is_selected) {
    // Base Case
    if (i == n) {
        return 0;
    }

    // Store the parity of number at
    // the ith position
    let cur = Math.abs(arr[i]) % 2;

    // If the dp state has already been
    // calculated, return it
    if (dp[i][prev] != -1) {
        return dp[i][prev];
    }

    // If the array is traversed and
    // no element has been selected yet
    // then select the current element
    if (i == n - 1 && is_selected == 0)
        return dp[i][prev] = arr[i];

    // If the parity of the current and
    // previously selected element are
    // different, then select the
    // current element
    if (cur != prev) {
        dp[i][prev] = arr[i]
            + maxSum(arr, i + 1,
                n, cur, 1);
    }

    // Skip the current element and move
    // to the next element
    dp[i][prev]
        = Math.max(dp[i][prev],
            maxSum(arr, i + 1, n,
                prev, is_selected));

    // Return the result
    return dp[i][prev];
}

// Function to calculate the maximum sum
// subsequence with consecutive terms
// having different parity
function maxSumUtil(arr, n) {

    // Initially the prev value is set to
    // say 2, as the first element can
    // anyways be selected
    document.write(maxSum(arr, 0, n, 2, 0));
}

// Driver Code
let arr = [1, 2, 6, 8, -5, 10];
let N = arr.length
maxSumUtil(arr, N);

</script>
```

**Output:** 

```
14
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)