# 最小化两个 K 长度子集之和的差值

> 原文:[https://www . geesforgeks . org/minimum-两个 k 长度之和子集之间的差异/](https://www.geeksforgeeks.org/minimize-difference-between-sum-of-two-k-length-subsets/)

给定一个由 **N** 个正整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是找出大小为 **K** 的两个[子集中元素](https://www.geeksforgeeks.org/print-subsets-given-size-set/)的[和之间的最小差，这样每个数组元素最多可以出现在**的 1 个**子集中。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {12，3，5，6，7，17}，K = 2
> **输出:** 1
> **解释:**考虑两个子集{5，6}和{3，7}，它们的和=(5+6)–(3+7)=(11–10)= 1 之间的差，这是最小可能的。
> 
> **输入:** arr[] = {10，10，10，10，2}，K = 3
> **输出:** 8
> **解释:**考虑两个子集{10，10，10}和{10，10，2}，它们之和的差=(10+10+10)–(10+10+2)=(30–22)= 8。

**天真方法:**解决给定问题的最简单方法是[生成所有可能的大小为**K**T5 的子集，并选择每对大小为**K**的子集，使得每个数组元素最多可以出现在**1**子集中。找到所有可能的子集对后，打印每对子集的元素总和之间的最小差异。](https://www.geeksforgeeks.org/print-subsets-given-size-set/)

***时间复杂度:**O(3<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。为了实现这种方法，想法是使用[3D-数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)，比如 **dp[][][]** ，来存储每个[递归调用](https://www.geeksforgeeks.org/recursion/)的状态。
按照以下步骤解决问题:

*   初始化一个辅助数组，比如说 **dp[][][]** ，其中 **dp[i][S1][S2]** 存储两个子集的和，直到每个 **i <sup>第</sup>个索引**。
*   声明一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如说 **minimumDifference(arr，N，K1，K2，S1，S2)** ，它接受一个数组，数组的当前大小，存储在子集 **(K1 和 K2)** 中的元素数量，以及每个子集中元素的总和作为参数。
    *   **基本情况:**如果数组中的[元素个数为 **N** ， **K1** 和 **K2** 的值为 **0** ，则返回 **S1** 和 **S2** 的绝对差值。](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/)
    *   如果已经计算出当前状态的结果，则返回结果。
    *   将第一个子集中的第**N**元素和下一个迭代的递归调用返回的值存储为**最小差(arr，N–1，K1–1，K2，S1+arr[N–1]，S2)** 。
    *   将第一个子集中的第**N**元素和下一次迭代的递归调用返回的值存储为**最小差(arr，N–1，K1，K2–1，S1，S2+arr[N–1])**。
    *   将不包括子集中第**N**元素和递归调用下一次迭代的返回的值存储为**最小差(arr，N–1，K1，K2，S1，S2)** 。
    *   将上述三个递归调用返回的所有值的最小值[存储在当前状态，即 **dp[N][S1][S2]** ，并返回其值。](https://www.geeksforgeeks.org/stdmin_element-in-cpp/)
*   完成以上步骤后，打印 **minimumDifference(arr，N，K，K，0，0)** 函数返回的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the values at recursive states
int dp[100][100][100];

// Function to find the minimum difference
// between sum of two K-length subsets
int minSumDifference(int* arr, int n,
                     int k1, int k2,
                     int sum1, int sum2)
{
    // Base Case
    if (n < 0) {

        // If k1 and k2 are 0, then
        // return the absolute difference
        // between sum1 and sum2
        if (k1 == 0 && k2 == 0) {
            return abs(sum1 - sum2);
        }

        // Otherwise, return INT_MAX
        else {
            return INT_MAX;
        }
    }

    // If the result is already
    // computed, return the result
    if (dp[n][sum1][sum2] != -1) {
        return dp[n][sum1][sum2];
    }

    // Store the 3 options
    int op1 = INT_MAX;
    int op2 = INT_MAX;
    int op3 = INT_MAX;

    // Including the element in first subset
    if (k1 > 0) {
        op1 = minSumDifference(arr, n - 1,
                               k1 - 1, k2,
                               sum1 + arr[n],
                               sum2);
    }

    // Including the element in second subset
    if (k2 > 0) {
        op2 = minSumDifference(arr, n - 1,
                               k1, k2 - 1, sum1,
                               sum2 + arr[n]);
    }

    // Not including the current element
    // in both the subsets
    op3 = minSumDifference(arr, n - 1,
                           k1, k2,
                           sum1, sum2);

    // Store minimum of 3 values obtained
    dp[n][sum1][sum2] = min(op1,
                            min(op2,
                                op3));

    // Return the value for
    // the current states
    return dp[n][sum1][sum2];
}

// Driver Code
int main()
{
    int arr[] = { 12, 3, 5, 6, 7, 17 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    memset(dp, -1, sizeof(dp));

    cout << minSumDifference(arr, N - 1,
                             K, K, 0, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Stores the values at recursive states
static int[][][] dp = new int[100][100][100];

// Function to find the minimum difference
// between sum of two K-length subsets
static int minSumDifference(int[] arr, int n,
                            int k1, int k2,
                            int sum1, int sum2)
{

    // Base Case
    if (n < 0)
    {

        // If k1 and k2 are 0, then
        // return the absolute difference
        // between sum1 and sum2
        if (k1 == 0 && k2 == 0)
        {
            return Math.abs(sum1 - sum2);
        }

        // Otherwise, return INT_MAX
        else
        {
            return Integer.MAX_VALUE;
        }
    }

    // If the result is already
    // computed, return the result
    if (dp[n][sum1][sum2] != -1)
    {
        return dp[n][sum1][sum2];
    }

    // Store the 3 options
    int op1 = Integer.MAX_VALUE;
    int op2 = Integer.MAX_VALUE;
    int op3 = Integer.MAX_VALUE;

    // Including the element in first subset
    if (k1 > 0)
    {
        op1 = minSumDifference(arr, n - 1,
                               k1 - 1, k2,
                               sum1 + arr[n],
                               sum2);
    }

    // Including the element in second subset
    if (k2 > 0)
    {
        op2 = minSumDifference(arr, n - 1,
                               k1, k2 - 1, sum1,
                               sum2 + arr[n]);
    }

    // Not including the current element
    // in both the subsets
    op3 = minSumDifference(arr, n - 1,
                           k1, k2,
                           sum1, sum2);

    // Store minimum of 3 values obtained
    dp[n][sum1][sum2] = Math.min(op1,
                        Math.min(op2, op3));

    // Return the value for
    // the current states
    return dp[n][sum1][sum2];
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 12, 3, 5, 6, 7, 17 };
    int K = 2;
    int N = arr.length;

    for(int[][] row:dp)
    {
        for(int[] innerrow : row)
        {
            Arrays.fill(innerrow,-1);
        }
    }

    System.out.println(minSumDifference(arr, N - 1, K,
                                        K, 0, 0));
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Stores the values at recursive states
dp = [[[ -1 for i in range(100)]
            for i in range(100)]
            for i in range(100)]

# Function to find the minimum difference
# between sum of two K-length subsets
def minSumDifference(arr, n, k1, k2, sum1, sum2):

    global dp

    # Base Case
    if (n < 0):

        # If k1 and k2 are 0, then
        # return the absolute difference
        # between sum1 and sum2
        if (k1 == 0 and k2 == 0):
            return abs(sum1 - sum2)

        # Otherwise, return INT_MAX
        else:
            return sys.maxsize + 1

    # If the result is already
    # computed, return the result
    if (dp[n][sum1][sum2] != -1):
        return dp[n][sum1][sum2]

    # Store the 3 options
    op1 = sys.maxsize + 1
    op2 = sys.maxsize + 1
    op3 = sys.maxsize + 1

    # Including the element in first subset
    if (k1 > 0):
        op1 = minSumDifference(arr, n - 1, k1 - 1,
                             k2, sum1 + arr[n], sum2)

    # Including the element in second subset
    if (k2 > 0):
        op2 = minSumDifference(arr, n - 1, k1, k2 - 1,
                           sum1, sum2 + arr[n])

    # Not including the current element
    # in both the subsets
    op3 = minSumDifference(arr, n - 1, k1,
                           k2, sum1, sum2)

    # Store minimum of 3 values obtained
    dp[n][sum1][sum2] = min(op1, min(op2, op3))

    # Return the value for
    # the current states
    return dp[n][sum1][sum2]

# Driver Code
if __name__ == '__main__':

    arr = [12, 3, 5, 6, 7, 17]
    K = 2
    N = len(arr)

    #memset(dp, -1, sizeof(dp))

    print (minSumDifference(arr, N - 1, K, K, 0, 0))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Stores the values at recursive states
static int[,,] dp = new int[100, 100, 100];

// Function to find the minimum difference
// between sum of two K-length subsets
static int minSumDifference(int[] arr, int n,
                            int k1, int k2,
                            int sum1, int sum2)
{

    // Base Case
    if (n < 0)
    {

        // If k1 and k2 are 0, then
        // return the absolute difference
        // between sum1 and sum2
        if (k1 == 0 && k2 == 0)
        {
            return Math.Abs(sum1 - sum2);
        }

        // Otherwise, return INT_MAX
        else
        {
            return Int32.MaxValue;
        }
    }

    // If the result is already
    // computed, return the result
    if (dp[n, sum1, sum2] != -1)
    {
        return dp[n, sum1, sum2];
    }

    // Store the 3 options
    int op1 = Int32.MaxValue;
    int op2 = Int32.MaxValue;
    int op3 = Int32.MaxValue;

    // Including the element in first subset
    if (k1 > 0)
    {
        op1 = minSumDifference(arr, n - 1,
                               k1 - 1, k2,
                               sum1 + arr[n],
                               sum2);
    }

    // Including the element in second subset
    if (k2 > 0)
    {
        op2 = minSumDifference(arr, n - 1,
                               k1, k2 - 1, sum1,
                               sum2 + arr[n]);
    }

    // Not including the current element
    // in both the subsets
    op3 = minSumDifference(arr, n - 1,
                           k1, k2,
                           sum1, sum2);

    // Store minimum of 3 values obtained
    dp[n, sum1, sum2] = Math.Min(op1,
                        Math.Min(op2, op3));

    // Return the value for
    // the current states
    return dp[n, sum1, sum2];
}

// Driver Code
static public void Main()
{
    int[] arr = { 12, 3, 5, 6, 7, 17 };
    int K = 2;
    int N = arr.Length;

    for(int i = 0; i < 100; i++)
    {
        for(int j = 0; j < 100; j++)
        {
            for(int k = 0; k < 100; k++)
            {
                dp[i, j, k] = -1;
            }
        }
    }

    Console.WriteLine(minSumDifference(arr, N - 1, K,
                                        K, 0, 0));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Stores the values at recursive states
let dp = new Array(100);
for(let i = 0; i < 100; i++)
{
    dp[i] = new Array(100);
    for(let j = 0; j < 100; j++)
    {
        dp[i][j] = new Array(100);
        for(let k = 0; k < 100; k++)
            dp[i][j][k] = -1;
    }
}

// Function to find the minimum difference
// between sum of two K-length subsets
function minSumDifference(arr, n, k1, k2, sum1, sum2)
{
     // Base Case
    if (n < 0)
    {

        // If k1 and k2 are 0, then
        // return the absolute difference
        // between sum1 and sum2
        if (k1 == 0 && k2 == 0)
        {
            return Math.abs(sum1 - sum2);
        }

        // Otherwise, return INT_MAX
        else
        {
            return Number.MAX_VALUE;
        }
    }

    // If the result is already
    // computed, return the result
    if (dp[n][sum1][sum2] != -1)
    {
        return dp[n][sum1][sum2];
    }

    // Store the 3 options
    let op1 = Number.MAX_VALUE;
    let op2 = Number.MAX_VALUE;
    let op3 = Number.MAX_VALUE;

    // Including the element in first subset
    if (k1 > 0)
    {
        op1 = minSumDifference(arr, n - 1,
                               k1 - 1, k2,
                               sum1 + arr[n],
                               sum2);
    }

    // Including the element in second subset
    if (k2 > 0)
    {
        op2 = minSumDifference(arr, n - 1,
                               k1, k2 - 1, sum1,
                               sum2 + arr[n]);
    }

    // Not including the current element
    // in both the subsets
    op3 = minSumDifference(arr, n - 1,
                           k1, k2,
                           sum1, sum2);

    // Store minimum of 3 values obtained
    dp[n][sum1][sum2] = Math.min(op1,
                        Math.min(op2, op3));

    // Return the value for
    // the current states
    return dp[n][sum1][sum2];
}

// Driver Code
let arr = [12, 3, 5, 6, 7, 17 ];
let  K = 2;
let N = arr.length;
document.write(minSumDifference(arr, N - 1, K,
                                        K, 0, 0));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N*S <sup>2</sup> ，其中 **S** 是给定数组*
***元素的*** [*之和辅助空间: O(N*S <sup>2</sup> )*](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)