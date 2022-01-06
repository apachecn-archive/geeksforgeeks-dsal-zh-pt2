# 最大子序列和，使得没有 K 个元素是连续的

> 原文:[https://www . geesforgeks . org/maximum-subsequer-sum-so-no-k-elements-continuous/](https://www.geeksforgeeks.org/maximum-subsequence-sum-such-that-no-k-elements-are-consecutive/)

给定一个由 N 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出由无 **K 个**连续数组元素组成的[子序列](https://www.geeksforgeeks.org/tag/subsequence/)的最大和。

**示例:**

> **输入:** arr[] = {10，5，8，16，21}，K = 4
> **输出:** 55
> **说明:**
> 最大和取 10，8，16，21。
> 
> **输入:** arr[] = {4，12，22，18，34，12，25}，K = 5
> **输出:** 111
> **说明:**
> 取 12，22，18，34，25
> 取最大和

**朴素方法:**最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)的所有子集，对于每个子集，检查它是否包含 **K** 个连续的数组元素。对于发现不包含 **K** 连续数组元素的子集，计算它们的和。求所有这些子序列和的最大值。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效途径:**以上解中有很多[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)，反复计算。为了避免重新计算相同的子问题，可以使用[记忆或制表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)。按照以下步骤解决问题:

1.  初始化一个数组 **dp[]** 来记住每个索引的和的最大值。
2.  现在， **dp[i]** 给出可选取的和的最大值，使得从**0**索引到 **i <sup>第</sup>** 索引，没有 **K** 元素是连续的。
3.  基本情况是当 **i < K** 时:
    *   因为数组元素都是正的，所以选择 **(K ) <sup>第</sup>个**索引之前的所有元素。
    *   所以 **dp[1] = arr [0]** 和 **dp[i] = dp[i -1] + arr[i-1]，(1 ≤ i < k)。**
4.  现在对于 **i ≥ K** :
    *   由于 **K** 连续元素不能被拾取，因此从 **i** 到**(I–K+1)**至少跳过一个元素，以确保没有 **K** 元素是连续的。
    *   由于任何元素都可能对结果有贡献，因此跳过从 **i** 到**(I–K+1)**的每个元素，并将跟踪最大和。
        *   要跳过第 **j <sup>个</sup>** 元素，添加最大和直到第**(j–1)<sup>个</sup>** 指数，该指数由第**DP【j–1】**给出，所有元素的和从第 **(j + 1) <sup>个</sup>** 指数到第 **i <sup>个</sup>** 指数，该指数可在第 ***O(1)** 中计算*
    *   因此，将当前 dp 状态更新为: **dp[i] = max (dp[i]，dp[j -1] +前缀[I]–前缀[j])，(I≤j ≤( I–K+1))**，其中前缀数组存储前缀和。
5.  完成上述步骤后，打印最大总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// of a subsequence consisting of
// no K consecutive array elements
int Max_Sum(int arr[], int K, int N)
{

    // Stores states of dp
    int dp[N + 1];

    // Initialise dp state
    memset(dp, 0, sizeof(dp));

    // Stores the prefix sum
    int prefix[N + 1];

    prefix[0] = 0;

    // Update the prefix sum
    for(int i = 1; i <= N; i++)
    {
        prefix[i] = prefix[i - 1] + arr[i-1];
    }

    // Base case for i < K
    dp[0] = 0;

    // For indices less than k
    // take all the elements
    for(int i = 1; i < K ; i++)
    {
        dp[i] = prefix[i];
    }

    // For i >= K  case
    for(int i = K ; i <= N; ++i)
    {

        // Skip each element from i to
        // (i - K + 1) to ensure that
        // no K elements are consecutive
        for(int j = i; j >= (i - K + 1); j--)
        {

            // j-th element is skipped

            // Update the current dp state
            dp[i] = max(dp[i], dp[j - 1] +
                    prefix[i] - prefix[j]);
        }
    }

    // dp[N] stores the maximum sum
    return dp[N];
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 4, 12, 22, 18, 34, 12, 25 };

    int N = sizeof(arr) / sizeof(int);
    int K = 5;

    // Function Call
    cout << Max_Sum(arr, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the maximum sum
// of a subsequence consisting of
// no K consecutive array elements
public static int Max_Sum(int[] arr, int K,
                          int N)
{

    // Stores states of dp
    int[] dp = new int[N + 1];

    // Initialise dp state
    Arrays.fill(dp, 0);

    // Stores the prefix sum
    int[] prefix = new int[N + 1];

    prefix[0] = 0;

    // Update the prefix sum
    for(int i = 1; i <= N; i++)
    {
        prefix[i] = prefix[i - 1] + arr[i-1];
    }

    // Base case for i < K
    dp[0] = 0;

    // For indices less than k
    // take all the elements
    for(int i = 1; i <= K - 1; i++)
    {
        dp[i] = prefix[i];
    }

    // For i >= K  case
    for(int i = K ; i <= N; ++i)
    {

        // Skip each element from i to
        // (i - K + 1) to ensure that
        // no K elements are consecutive
        for(int j = i; j >= (i - K + 1); j--)
        {

            // j-th element is skipped

            // Update the current dp state
            dp[i] = Math.max(dp[i], dp[j - 1] +
                         prefix[i] - prefix[j]);
        }
    }

    // dp[N] stores the maximum sum
    return dp[N];
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int[] arr = { 4, 12, 22, 18, 34, 12, 25 };

    int N = arr.length;
    int K = 5;

    // Function Call
    System.out.println(Max_Sum(arr, K, N));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum sum
# of a subsequence consisting of
# no K consecutive array elements
def Max_Sum(arr, K, N):

    # Stores states of dp
    dp = [0] * (N + 1)

    # Stores the prefix sum
    prefix = [None] * (N + 1)

    prefix[0] = 0

    # Update the prefix sum
    for i in range(1, N + 1):
        prefix[i] = prefix[i - 1] + arr[i - 1]

    # Base case for i < K
    dp[0] = 0

    # For indices less than k
    # take all the elements
    for i in range(1, K):
        dp[i] = prefix[i]

    # For i >= K case
    for i in range(K, N + 1):

        # Skip each element from i to
        # (i - K + 1) to ensure that
        # no K elements are consecutive
        for j in range(i, i - K, -1):

            # j-th element is skipped

            # Update the current dp state
            dp[i] = max(dp[i], dp[j - 1] +
                    prefix[i] - prefix[j])

    # dp[N] stores the maximum sum
    return dp[N]

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [ 4, 12, 22, 18, 34, 12, 25 ]

    N = len(arr)
    K = 5

    # Function call
    print(Max_Sum(arr, K, N))

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum sum
// of a subsequence consisting of
// no K consecutive array elements
static int Max_Sum(int[] arr, int K, int N)
{

    // Stores states of dp
    int[] dp = new int[N + 1];

    // Initialise dp state
    Array.Fill(dp, 0);

    // Stores the prefix sum
    int[] prefix = new int[N + 1];

    prefix[0] = 0;

    // Update the prefix sum
    for(int i = 1; i <= N; i++)
    {
        prefix[i] = prefix[i - 1] + arr[i - 1];
    }

    // Base case for i < K
    dp[0] = 0;

    // For indices less than k
    // take all the elements
    for(int i = 1; i <= K - 1; i++)
    {
        dp[i] = prefix[i];
    }

    // For i >= K case
    for(int i = K; i <= N; ++i)
    {

        // Skip each element from i to
        // (i - K + 1) to ensure that
        // no K elements are consecutive
        for(int j = i; j >= (i - K + 1); j--)
        {

            // j-th element is skipped

            // Update the current dp state
            dp[i] = Math.Max(dp[i], dp[j - 1] +
                         prefix[i] - prefix[j]);
        }
    }

    // dp[N] stores the maximum sum
    return dp[N];
}

// Driver Code
static public void Main()
{

    // Given array arr[]
    int[] arr = { 4, 12, 22, 18, 34, 12, 25 };

    int N = arr.Length;
    int K = 5;

    // Function Call
    Console.WriteLine(Max_Sum(arr, K, N));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum sum
// of a subsequence consisting of
// no K consecutive array elements
function Max_Sum(arr, K, N)
{

    // Stores states of dp
    var dp = Array(N+1).fill(0);

    // Stores the prefix sum
    var prefix = Array(N+1);

    prefix[0] = 0;

    // Update the prefix sum
    for(var i = 1; i <= N; i++)
    {
        prefix[i] = prefix[i - 1] + arr[i-1];
    }

    // Base case for i < K
    dp[0] = 0;

    // For indices less than k
    // take all the elements
    for(var i = 1; i < K ; i++)
    {
        dp[i] = prefix[i];
    }

    // For i >= K  case
    for(var i = K ; i <= N; ++i)
    {

        // Skip each element from i to
        // (i - K + 1) to ensure that
        // no K elements are consecutive
        for(var j = i; j >= (i - K + 1); j--)
        {

            // j-th element is skipped

            // Update the current dp state
            dp[i] = Math.max(dp[i], dp[j - 1] +
                    prefix[i] - prefix[j]);
        }
    }

    // dp[N] stores the maximum sum
    return dp[N];
}

// Driver Code

// Given array arr[]
var arr = [4, 12, 22, 18, 34, 12, 25];
var N = arr.length;
var K = 5;

// Function Call
document.write( Max_Sum(arr, K, N));

</script>
```

**Output:** 

```
111
```

***时间复杂度:** O(N*K)，其中 N 是数组中的元素个数，K 是输入，这样就没有 K 个元素是连续的。*
***辅助空间:** O(N)*