# 通过将每个元素乘以其索引

得到的最大可能子序列和

> 原文:[https://www . geeksforgeeks . org/最大子序列-每个元素乘以其索引的总和/](https://www.geeksforgeeks.org/maximum-subsequence-sum-possible-by-multiplying-each-element-by-its-index/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过将结果子序列的每个元素乘以其索引(基于 *1 的索引*)来找到最大[子序列](https://www.geeksforgeeks.org/tag/subsequence/)的和。

**示例:**

> **输入:** arr[] = {-1，2，-10，4，-20}
> **输出:** 15
> **解释:**
> 对于子序列{-1，2，4}，执行给定运算后给定子序列的和= 1 *(1)+2 * 2+3 * 4 = 15，这是最大可能。
> 
> **输入:** arr[] = {1，0，-1，2}
> **输出:** 7
> **解释:**
> 对于子序列{1，0，2}，执行给定运算后给定子序列的和= 1*1 + 2*0 + 3*2 = 7，这是最大可能。

**天真方法:**想法是[使用](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)[递归](https://www.geeksforgeeks.org/recursion/)从数组中生成所有可能的子序列，并计算每个子序列所需的和并打印最大和。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**由于问题包含许多[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)，因此可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)优化上述方法。以下是步骤:

*   初始化一个辅助矩阵 **dp[][]** ，其中 **dp[i][j]** 存储长度子序列 **j** 直到索引 **i** 的最大值。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，有两种可能性:
    *   要么将当前元素包含到子序列和中，然后增加子序列中的元素数量。
    *   或者从子序列中排除当前元素并继续下一个元素。
*   因此，递归关系由以下等式给出:

> dp[i][j] =最大值(a[i] * j +最大值(j + 1，i + 1)，最大值(j，i + 1))

*   通过对每个索引使用上述递归关系，继续更新 **dp[][]** 表，并从整个数组中返回最大可能和。
*   在上述步骤后打印最大值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Initialize dp array
int dp[1005][1005];

// Function to find the maximum
// sum of the subsequence formed
int maximumSumUtil(int a[], int index,
                   int count, int n)
{
    // Base Case
    if (index > n || count > n + 1) {
        return 0;
    }

    // If already calculated
    // state occurs
    if (dp[index][count] != -1)
        return dp[index][count];

    // Include the current element
    int ans1 = maximumSumUtil(a, index + 1,
                              count + 1, n)
               + a[index] * count;

    // Exclude the current element
    int ans2 = maximumSumUtil(a, index + 1,
                              count, n);

    // Update the maximum ans
    return (dp[index][count]
            = max(ans1, ans2));
}

// Function to calculate maximum sum
// of the subsequence obtained
int maximumSum(int arr[], int N)
{
    // Initialise the dp array with -1
    memset(dp, -1, sizeof(dp));

    // Print the maximum sum possible
    cout << maximumSumUtil(arr, 0, 1,
                           N - 1);
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { -1, 2, -10, 4, -20 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maximumSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Initialize dp array
static int [][]dp = new int[1005][1005];

// Function to find the maximum
// sum of the subsequence formed
static int maximumSumUtil(int a[], int index,
                          int count, int n)
{
  // Base Case
  if (index > n || count > n + 1)
  {
    return 0;
  }

  // If already calculated
  // state occurs
  if (dp[index][count] != -1)
    return dp[index][count];

  // Include the current element
  int ans1 = maximumSumUtil(a, index + 1,
                            count + 1, n) +
                            a[index] * count;

  // Exclude the current element
  int ans2 = maximumSumUtil(a, index + 1,
                            count, n);

  // Update the maximum ans
  return (dp[index][count] =
          Math.max(ans1, ans2));
}

// Function to calculate maximum sum
// of the subsequence obtained
static void maximumSum(int arr[], int N)
{
  // Initialise the dp array with -1
  for(int i = 0; i < 1005; i++)
  {
    for (int j = 0; j < 1005; j++)
    {
      dp[i][j] = -1;
    }
  }

  // Print the maximum sum possible
  System.out.print(maximumSumUtil(arr, 0,
                                  1, N - 1));
}

// Driver Code
public static void main(String[] args)
{
  // Given array
  int arr[] = {-1, 2, -10, 4, -20};

  // Size of the array
  int N = arr.length;

  // Function Call
  maximumSum(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Initialize dp array
dp = [[-1 for x in range(1005)]
          for y in range(1005)]

# Function to find the maximum
# sum of the subsequence formed
def maximumSumUtil(a, index, count, n):

    # Base Case
    if (index > n or count > n + 1):
        return 0

    # If already calculated
    # state occurs
    if (dp[index][count] != -1):
        return dp[index][count]

    # Include the current element
    ans1 = (maximumSumUtil(a, index + 1,
                              count + 1, n) +
                           a[index] * count)

    # Exclude the current element
    ans2 = maximumSumUtil(a, index + 1,
                          count, n)

    # Update the maximum ans
    dp[index][count] = max(ans1, ans2)

    return dp[index][count]

# Function to calculate maximum sum
# of the subsequence obtained
def maximumSum(arr, N):

    # Print the maximum sum possible
    print(maximumSumUtil(arr, 0, 1,
                             N - 1))

# Driver Code

# Given array
arr = [ -1, 2, -10, 4, -20 ]

# Size of the array
N = len(arr)

# Function call
maximumSum(arr, N)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Initialize dp array
static int [,]dp = new int[1005, 1005];

// Function to find the maximum
// sum of the subsequence formed
static int maximumSumUtil(int []a, int index,
                          int count, int n)
{
  // Base Case
  if (index > n || count > n + 1)
  {
    return 0;
  }

  // If already calculated
  // state occurs
  if (dp[index, count] != -1)
    return dp[index, count];

  // Include the current element
  int ans1 = maximumSumUtil(a, index + 1,
                            count + 1, n) +
                            a[index] * count;

  // Exclude the current element
  int ans2 = maximumSumUtil(a, index + 1,
                            count, n);

  // Update the maximum ans
  return (dp[index, count] =
          Math.Max(ans1, ans2));
}

// Function to calculate maximum sum
// of the subsequence obtained
static void maximumSum(int []arr, int N)
{
  // Initialise the dp array with -1
  for(int i = 0; i < 1005; i++)
  {
    for (int j = 0; j < 1005; j++)
    {
      dp[i, j] = -1;
    }
  }

  // Print the maximum sum possible
  Console.Write(maximumSumUtil(arr, 0,
                               1, N - 1));
}

// Driver Code
public static void Main(String[] args)
{
  // Given array
  int []arr = {-1, 2, -10, 4, -20};

  // Size of the array
  int N = arr.Length;

  // Function Call
  maximumSum(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Let initialize dp array
let dp = new Array(1005);

// Loop to create 2D array using 1D array
for (var i = 0; i < dp.length; i++) {
    dp[i] = new Array(2);
}

// Function to find the maximum
// sum of the subsequence formed
function maximumSumUtil(a, index,
                          count, n)
{
  // Base Case
  if (index > n || count > n + 1)
  {
    return 0;
  }

  // If already calculated
  // state occurs
  if (dp[index][count] != -1)
    return dp[index][count];

  // Include the current element
  let ans1 = maximumSumUtil(a, index + 1,
                            count + 1, n) +
                            a[index] * count;

  // Exclude the current element
  let ans2 = maximumSumUtil(a, index + 1,
                            count, n);

  // Update the maximum ans
  return (dp[index][count] =
          Math.max(ans1, ans2));
}

// Function to calculate maximum sum
// of the subsequence obtained
function maximumSum(arr, N)
{
  // Initialise the dp array with -1
  for(let i = 0; i < 1005; i++)
  {
    for (let j = 0; j < 1005; j++)
    {
      dp[i][j] = -1;
    }
  }

  // Print the maximum sum possible
  document.write(maximumSumUtil(arr, 0,
                                  1, N - 1));
}

// Driver code

  // Given array
  let arr = [-1, 2, -10, 4, -20];

  // Size of the array
  let N = arr.length;

  // Function Call
  maximumSum(arr, N);

</script>
```

**Output:** 

```
15
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*