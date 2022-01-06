# 通过移除相等元素的连续子阵列来最大化清空阵列的成本

> 原文:[https://www . geeksforgeeks . org/通过移除相等元素的连续子数组来最大化空数组的成本/](https://www.geeksforgeeks.org/maximize-cost-to-empty-an-array-by-removing-contiguous-subarrays-of-equal-elements/)

给定一个由 **N** 个整数和一个整数 **M** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**，任务是找到通过执行以下任意次数的操作可以获得的最大成本。

> 在一个操作中，选择 **K** 个具有相同值的相邻元素(其中 K ≥ 1)并将其移除，该操作的成本为 **K * M** 。

**示例:**

> **输入:** arr[] = {1，3，2，2，2，3，4，3，1}，M = 3
> **输出:** 27
> **解释:**
> 第一步:去掉三个连续的 2 来修改 arr[] = {1，3，3，4，3，1}。成本= 3 * 3 = 9
> 步骤 2:删除 4 修改 arr[] = {1，3，3，3，1}。成本= 9 + 1 * 3 = 12
> 步骤 3:删除三个连续的 3 以修改 arr[] = {1，1}。成本= 12 + 3 * 3 = 21
> 步骤 4:移除两个连续的 1 以修改 arr[] = {}。成本= 21 + 2 * 3 = 27
> 
> **输入:** arr[] = {1，2，3，4，5，6，7}，M = 2
> **输出:** 14

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。以下是步骤:

1.  初始化三维数组 **dp[][][]** ，使得 **dp【左】【右】【计数】**，其中**左**和**右**表示索引**【左，右】**和**之间的操作计数**是 **arr【左】**的**左侧**的元素数量，其值与 **arr【左】**的值相同，计数不包括
2.  现在有以下两种可能的选择:
    *   结束序列，删除相同值的元素，包括*起始元素*(即 **arr【左】**)，然后从下一个元素继续。
    *   继续该序列，在索引**【左+ 1，右】**之间搜索与 **arr【左】**具有相同值的元素(比如索引 **i** ，这使我们能够继续该序列。
3.  从新序列进行递归调用，并继续上一序列的过程。
4.  完成上述所有步骤后，打印最大成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Initialize dp array
int dp[101][101][101];

// Function that removes elements
// from array to maximize the cost
int helper(int arr[], int left, int right,
           int count, int m)
{
    // Base case
    if (left > right)
        return 0;

    // Check if an answer is stored
    if (dp[left][right][count] != -1) {
        return dp[left][right][count];
    }

    // Deleting count + 1 i.e. including
    // the first element and starting a
    // new sequence
    int ans = (count + 1) * m
              + helper(arr, left + 1,
                       right, 0, m);

    for (int i = left + 1;
         i <= right; ++i) {

        if (arr[i] == arr[left]) {

            // Removing [left + 1, i - 1]
            // elements to continue with
            // previous sequence
            ans = max(
                ans,
                helper(arr, left + 1,
                       i - 1, 0, m)
                    + helper(arr, i, right,
                             count + 1, m));
        }
    }

    // Store the result
    dp[left][right][count] = ans;

    // Return answer
    return ans;
}

// Function to remove the elements
int maxPoints(int arr[], int n, int m)
{
    int len = n;
    memset(dp, -1, sizeof(dp));

    // Function Call
    return helper(arr, 0, len - 1, 0, m);
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 3, 2, 2, 2, 3, 4, 3, 1 };

    int M = 3;

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << maxPoints(arr, N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Initialize dp array
static int [][][]dp = new int[101][101][101];

// Function that removes elements
// from array to maximize the cost
static int helper(int arr[], int left, int right,
                  int count, int m)
{

    // Base case
    if (left > right)
        return 0;

    // Check if an answer is stored
    if (dp[left][right][count] != -1)
    {
        return dp[left][right][count];
    }

    // Deleting count + 1 i.e. including
    // the first element and starting a
    // new sequence
    int ans = (count + 1) * m +
             helper(arr, left + 1,
                    right, 0, m);

    for(int i = left + 1; i <= right; ++i)
    {
        if (arr[i] == arr[left])
        {

            // Removing [left + 1, i - 1]
            // elements to continue with
            // previous sequence
            ans = Math.max(ans,
                  helper(arr, left + 1,
                         i - 1, 0, m) +
                  helper(arr, i, right,
                         count + 1, m));
        }
    }

    // Store the result
    dp[left][right][count] = ans;

    // Return answer
    return ans;
}

// Function to remove the elements
static int maxPoints(int arr[], int n, int m)
{
    int len = n;
    for(int i = 0; i < 101; i++)
    {
        for(int j = 0; j < 101; j++)
        {
            for(int k = 0; k < 101; k++)
                dp[i][j][k] = -1;
        }
    }

    // Function call
    return helper(arr, 0, len - 1, 0, m);
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 1, 3, 2, 2, 2, 3, 4, 3, 1 };

    int M = 3;

    int N = arr.length;

    // Function call
    System.out.print(maxPoints(arr, N, M));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Initialize dp array
dp = [[[-1 for x in range(101)]
            for y in range(101)]
            for z in range(101)]

# Function that removes elements
# from array to maximize the cost
def helper(arr, left,
           right, count, m):

  # Base case
  if (left > right):
    return 0

  # Check if an answer is stored
  if (dp[left][right][count] != -1):
    return dp[left][right][count]

  # Deleting count + 1 i.e. including
  # the first element and starting a
  # new sequence
  ans = ((count + 1) * m +
          helper(arr, left + 1,
                 right, 0, m))

  for i in range (left + 1,
                  right + 1):

    if (arr[i] == arr[left]):

      # Removing [left + 1, i - 1]
      # elements to continue with
      # previous sequence
      ans = (max(ans, helper(arr, left + 1,
                             i - 1, 0, m) +
                         helper(arr, i, right,
                              count + 1, m)))

      # Store the result
      dp[left][right][count] = ans

      # Return answer
      return ans

# Function to remove the elements
def maxPoints(arr, n, m):
  length = n
  global dp

  # Function Call
  return helper(arr, 0,
                length - 1, 0, m)

# Driver Code
if __name__ == "__main__":

  # Given array
  arr = [1, 3, 2, 2,
         2, 3, 4, 3, 1]
  M = 3
  N = len(arr)

  # Function Call
  print(maxPoints(arr, N, M))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Initialize dp array
static int [,,]dp = new int[101, 101, 101];

// Function that removes elements
// from array to maximize the cost
static int helper(int []arr, int left, int right,
                  int count, int m)
{

    // Base case
    if (left > right)
        return 0;

    // Check if an answer is stored
    if (dp[left, right, count] != -1)
    {
        return dp[left, right, count];
    }

    // Deleting count + 1 i.e. including
    // the first element and starting a
    // new sequence
    int ans = (count + 1) * m +
              helper(arr, left + 1,
                    right, 0, m);

    for(int i = left + 1; i <= right; ++i)
    {
        if (arr[i] == arr[left])
        {

            // Removing [left + 1, i - 1]
            // elements to continue with
            // previous sequence
            ans = Math.Max(ans,
                  helper(arr, left + 1,
                         i - 1, 0, m) +
                  helper(arr, i, right,
                         count + 1, m));
        }
    }

    // Store the result
    dp[left, right, count] = ans;

    // Return answer
    return ans;
}

// Function to remove the elements
static int maxPoints(int []arr, int n, int m)
{
    int len = n;
    for(int i = 0; i < 101; i++)
    {
        for(int j = 0; j < 101; j++)
        {
            for(int k = 0; k < 101; k++)
                dp[i, j, k] = -1;
        }
    }

    // Function call
    return helper(arr, 0, len - 1, 0, m);
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 1, 3, 2, 2, 2, 3, 4, 3, 1 };

    int M = 3;

    int N = arr.Length;

    // Function call
    Console.Write(maxPoints(arr, N, M));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Initialize dp array
let dp = new Array(101);
for(let i = 0; i < 101; i++)
{
    dp[i] = new Array(101);
    for(let j = 0; j < 101; j++)
    {
        dp[i][j] = new Array(101);
        for(let k = 0; k < 101; k++)
        {
            dp[i][j][k] = -1;
        }
    }
}

// Function that removes elements
// from array to maximize the cost
function helper(arr, left, right, count, m)
{

    // Base case
    if (left > right)
        return 0;

    // Check if an answer is stored
    if (dp[left][right][count] != -1)
    {
        return dp[left][right][count];
    }

    // Deleting count + 1 i.e. including
    // the first element and starting a
    // new sequence
    let ans = (count + 1) * m +
              helper(arr, left + 1,
                     right, 0, m);

    for(let i = left + 1; i <= right; ++i)
    {
        if (arr[i] == arr[left])
        {

            // Removing [left + 1, i - 1]
            // elements to continue with
            // previous sequence
            ans = Math.max(ans,
                  helper(arr, left + 1,
                         i - 1, 0, m) +
                  helper(arr, i, right,
                         count + 1, m));
        }
    }

    // Store the result
    dp[left][right][count] = ans;

    // Return answer
    return ans;
}

// Function to remove the elements
function maxPoints(arr, n, m)
{
    let len = arr.length;

    // Function call
    return helper(arr, 0, len - 1, 0, m);
}

// Driver Code

// Given array
let arr = [ 1, 3, 2, 2, 2, 3, 4, 3, 1 ];
let M = 3;
let N = arr.length;

// Function call
document.write(maxPoints(arr, N, M));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
27
```

***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(N <sup>3</sup> )*