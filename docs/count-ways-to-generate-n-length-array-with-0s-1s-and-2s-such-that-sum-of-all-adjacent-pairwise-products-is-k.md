# 计算生成 0、1 和 2s 的 N 长度数组的方式，使得所有相邻的成对乘积之和为 K

> 原文:[https://www . geesforgeks . org/count-way-to-generate-n-length-array-with-0s-1s-2s-so-所有相邻成对乘积之和-is-k/](https://www.geeksforgeeks.org/count-ways-to-generate-n-length-array-with-0s-1s-and-2s-such-that-sum-of-all-adjacent-pairwise-products-is-k/)

给定两个整数 **N** 和 **K** ，任务是找出任意次使用数值 **0** 、 **1** 和 **2** 可以生成的 **N** 长度数组的个数，使得数组的所有[个相邻成对乘积](https://www.geeksforgeeks.org/product-of-all-pairwise-consecutive-elements-in-an-array/)之和为 **K** 。

**示例:**

> **输入:** N = 4，K = 3
> **输出:** 5
> **解释:**所有可能的安排是:
> 
> 1.  arr[] = {2，1，1，0}，相邻成对乘积和= 2 * 1 + 1 * 1 + 1 * 0 = 3。
> 2.  arr[] = {0，2，1，1}，相邻成对乘积和= 0 * 2 + 2 * 1 + 1 * 1 = 3。
> 3.  arr[] = {1，1，2，0}，相邻成对乘积和= 1 * 1 + 1 * 2 + 2 * 0 = 3。
> 4.  arr[] = {0，1，1，2}，相邻成对乘积和为 0 * 1 + 1 * 1 + 1 * 2 = 3。
> 5.  arr[] = {1，1，1，1}，相邻成对乘积和= 1*1 + 1*1 + 1*1 = 3。
> 
> **输入:** N = 10，K = 9
> T3】输出: 3445

**天真方法:**最简单的方法是[生成数组](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/)的所有可能排列，其值可以是 **0** 、 **1** 或 **2** ，并计算那些其[相邻成对乘积](https://www.geeksforgeeks.org/product-of-all-pairwise-consecutive-elements-in-an-array/)之和为 **K** 的数组。打印此类安排的计数。

***时间复杂度:**O(N * 3<sup>N</sup>)*
***辅助空间:** O(N)*

**高效途径:**优化上述途径，最优思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)T4。重叠子问题可以存储在 **dp[][][]表**中，其中**DP[I][剩余][上一个】**存储从位置**“I”**到位置**(N–1)**的答案，其中**“剩余”**作为要添加的**剩余值**和**“上一个”**作为放置在任何职位“I”都可能有三种情况:

*   将**‘0’**分配到**‘I’位置。**
*   将**‘1’**分配到**‘I’位置。**
*   将**‘2’**分配到**‘I’位置。**

按照以下步骤解决问题:

*   初始化 **dp[][][]** 存储当前位置、待添加的剩余值以及前一位置的元素。
*   过渡状态如下:

> DP[I][剩余 _sum][previous_element] = dp(将 0 分配给位置“I”)+DP(将 1 分配给“I”)+DP(将 2 分配给“I”)

*   递归求解上述递归关系，并将每个状态的结果存储在 [dp 表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)中。对于重叠，子问题使用存储在 **dp 表**中的结果。
*   上述递归调用结束后，打印数组中有相邻成对乘积的数组总数为 **K** 的函数返回。

下面是上述方法的一个实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find total number of
// possible arrangements of array
int waysForPairwiseSumToBeK(
    int i, int rem, int previous,
    int N, int dp[][15][3])
{
    // Base Case
    if (i == N) {
        if (rem == 0)
            return 1;
        else
            return 0;
    }

    // If rem exceeds 'k' return 0
    if (rem < 0)
        return 0;

    // Return the already calculated
    // states
    if (dp[i][rem][previous] != -1)
        return dp[i][rem][previous];

    int ways = 0;

    // Place a '0' at current position
    ways += waysForPairwiseSumToBeK(
        i + 1, rem, 0, N, dp);

    // Place a '1' at current position
    // Add it to previous value
    ways += waysForPairwiseSumToBeK(
        i + 1, rem - (previous), 1, N, dp);

    // Place a '2' at current position.
    // Add it to previous value.
    ways += waysForPairwiseSumToBeK(
        i + 1, rem - (2 * previous), 2, N, dp);

    // Store the current state result
    // return the same result
    return dp[i][rem][previous] = ways;
}

// Function to find number of possible
// arrangements of array with 0, 1, and
// 2 having pairwise product sum K
void countOfArrays(int i, int rem,
                   int previous, int N)
{
    // Store the overlapping states
    int dp[15][15][3];

    // Initialize dp table with -1
    memset(dp, -1, sizeof dp);

    // Stores total number of ways
    int totWays
        = waysForPairwiseSumToBeK(
            i, rem, previous, N, dp);

    // Print number of ways
    cout << totWays << ' ';
}

// Driver Code
int main()
{
    // Given N and K
    int N = 4, K = 3;

    // Function Call
    countOfArrays(0, K, 0, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class solution{

// Function to find total number of
// possible arrangements of array
static int waysForPairwiseSumToBeK(int i, int rem,
                                   int previous,
                                   int N, int [][][]dp)
{
  // Base Case
  if (i == N)
  {
    if (rem == 0)
      return 1;
    else
      return 0;
  }

  // If rem exceeds
  // 'k' return 0
  if (rem < 0)
    return 0;

  // Return the already
  // calculated states
  if (dp[i][rem][previous] != -1)
    return dp[i][rem][previous];

  int ways = 0;

  // Place a '0' at current position
  ways += waysForPairwiseSumToBeK(i + 1, rem,
                                  0, N, dp);

  // Place a '1' at current position
  // Add it to previous value
  ways += waysForPairwiseSumToBeK(i + 1, rem -
                                  (previous),
                                  1, N, dp);

  // Place a '2' at current position.
  // Add it to previous value.
  ways += waysForPairwiseSumToBeK(i + 1, rem -
                                  (2 * previous),
                                  2, N, dp);

  // Store the current state result
  // return the same result
  dp[i][rem][previous] = ways;
  return ways;
}

// Function to find number of possible
// arrangements of array with 0, 1, and
// 2 having pairwise product sum K
static void countOfArrays(int i, int rem,
                          int previous, int N)
{
  // Store the overlapping states
  int [][][]dp = new int[15][15][3];

  // Initialize dp table with -1
  for(int p = 0; p < 15; p++)
  {
    for(int q = 0; q < 15; q++)
    {     
      for(int r = 0; r < 3; r++)
        dp[p][q][r] = -1;
    }
  }

  // Stores total number of ways
  int totWays = waysForPairwiseSumToBeK(i, rem,
                                        previous,
                                        N, dp);
  // Print number of ways
  System.out.print(totWays);
}

// Driver Code
public static void main(String args[])
{
  // Given N and K
  int N = 4, K = 3;

  // Function Call
  countOfArrays(0, K, 0, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Pyhton3 program for the above approach

# Function to find total number of
# possible arrangements of array
def waysForPairwiseSumToBeK(i, rem, previous, N, dp):

    # Base Case
    if (i == N):
        if (rem == 0):
            return 1
        else:
            return 0

    # If rem exceeds 'k' return 0
    if (rem < 0):
        return 0

    # Return the already calculated
    # states
    if (dp[i][rem][previous] != -1):
        return dp[i][rem][previous]

    ways = 0

    # Place a '0' at current position
    ways += waysForPairwiseSumToBeK(i + 1, rem,
                                    0, N, dp)

    # Place a '1' at current position
    # Add it to previous value
    ways += waysForPairwiseSumToBeK(i + 1,
                                  rem - (previous),
                                  1, N, dp)

    # Place a '2' at current position.
    # Add it to previous value.
    ways += waysForPairwiseSumToBeK(i + 1,
                             rem - (2 * previous),
                             2, N, dp)

    # Store the current state result
    # return the same result
    dp[i][rem][previous] = ways

    return ways

# Function to find number of possible
# arrangements of array with 0, 1, and
# 2 having pairwise product sum K
def countOfArrays(i, rem, previous, N):

    # Store the overlapping states
    dp = [[[-1 for i in range(3)]
               for j in range(15)]
               for k in range(15)]

    # Stores total number of ways
    totWays = waysForPairwiseSumToBeK(i, rem,
                                      previous,
                                      N, dp)

    # Print number of ways
    print(totWays, end = " ")

# Driver Code
if __name__ == '__main__':

    # Given N and K
    N = 4
    K = 3

    # Function Call
    countOfArrays(0, K, 0, N)

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function to find total number of
// possible arrangements of array
static int waysForPairwiseSumToBeK(int i, int rem,
                                   int previous,
                                   int N, int [,,]dp)
{

  // Base Case
  if (i == N)
  {
    if (rem == 0)
      return 1;
    else
      return 0;
  }

  // If rem exceeds
  // 'k' return 0
  if (rem < 0)
    return 0;

  // Return the already
  // calculated states
  if (dp[i, rem, previous] != -1)
    return dp[i, rem, previous];

  int ways = 0;

  // Place a '0' at current position
  ways += waysForPairwiseSumToBeK(i + 1, rem,
                                  0, N, dp);

  // Place a '1' at current position
  // Add it to previous value
  ways += waysForPairwiseSumToBeK(i + 1, rem -
                                  (previous),
                                  1, N, dp);

  // Place a '2' at current position.
  // Add it to previous value.
  ways += waysForPairwiseSumToBeK(i + 1, rem -
                                  (2 * previous),
                                   2, N, dp);

  // Store the current state result
  // return the same result
  dp[i, rem, previous] = ways;

  return ways;
}

// Function to find number of possible
// arrangements of array with 0, 1, and
// 2 having pairwise product sum K
static void countOfArrays(int i, int rem,
                          int previous, int N)
{

  // Store the overlapping states
  int [,,]dp = new int[ 15, 15, 3 ];

  // Initialize dp table with -1
  for(int p = 0; p < 15; p++)
  {
    for(int q = 0; q < 15; q++)
    {     
      for(int r = 0; r < 3; r++)
        dp[p, q, r] = -1;
    }
  }

  // Stores total number of ways
  int totWays = waysForPairwiseSumToBeK(i, rem,
                                        previous,
                                        N, dp);

  // Print number of ways
  Console.Write(totWays);
}

// Driver Code
public static void Main(String []args)
{

  // Given N and K
  int N = 4, K = 3;

  // Function Call
  countOfArrays(0, K, 0, N);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the
// above approach

// Function to find total number of
// possible arrangements of array
function waysForPairwiseSumToBeK(i,rem,previous,N,dp)
{
    // Base Case
  if (i == N)
  {
    if (rem == 0)
      return 1;
    else
      return 0;
  }

  // If rem exceeds
  // 'k' return 0
  if (rem < 0)
    return 0;

  // Return the already
  // calculated states
  if (dp[i][rem][previous] != -1)
    return dp[i][rem][previous];

  let ways = 0;

  // Place a '0' at current position
  ways += waysForPairwiseSumToBeK(i + 1, rem,
                                  0, N, dp);

  // Place a '1' at current position
  // Add it to previous value
  ways += waysForPairwiseSumToBeK(i + 1, rem -
                                  (previous),
                                  1, N, dp);

  // Place a '2' at current position.
  // Add it to previous value.
  ways += waysForPairwiseSumToBeK(i + 1, rem -
                                  (2 * previous),
                                  2, N, dp);

  // Store the current state result
  // return the same result
  dp[i][rem][previous] = ways;
  return ways;
}

// Function to find number of possible
// arrangements of array with 0, 1, and
// 2 having pairwise product sum K
function countOfArrays(i,rem,previous,N)
{
    // Store the overlapping states
  let dp = new Array(15);
  for(let i = 0; i < 15; i++)
  {
      dp[i] = new Array(15);
    for(let j = 0; j < 15; j++)
    {
        dp[i][j] = new Array(3);
        for(let k = 0; k < 3; k++)
            dp[i][j][k] = -1;
    }
  }

  // Stores total number of ways
  let totWays = waysForPairwiseSumToBeK(i, rem,
                                        previous,
                                        N, dp);
  // Print number of ways
  document.write(totWays);
}

// Driver Code
// Given N and K
let N = 4, K = 3;

// Function Call
countOfArrays(0, K, 0, N);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N * K)*
T5**辅助空间:** O(N*K)