# 相邻数字绝对差不超过 K 的 N 位数计数

> 原文:[https://www . geeksforgeeks . org/相邻数字绝对差不超过-k 的数字计数/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-with-absolute-difference-of-adjacent-digits-not-exceeding-k/)

给定两个整数 **N** 和 **K** ，任务是找出 **N 位数字**的个数，使得数字中相邻数字的绝对差值不大于 **K** 。

**示例:**

> **输入:** N = 2，K = 1
> **输出:** 26
> **说明:**数字为 10、11、12、21、22、23、32、33、34、43、44、45、54、55、56、65、66、67、76、77、78、87、88、89、98、99
> 
> **输入:** N = 3，K = 2
> T3】输出: 188

**天真方法**
最简单的方法是迭代所有 **N** 数字，如果相邻数字的绝对差值小于或等于 k，则检查每个数字。
***时间复杂度:** O(10 <sup>N</sup> * N)*

**高效方法:**
为了优化上述方法，我们需要使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)方法以及[范围更新](https://www.geeksforgeeks.org/difference-array-range-update-query-o1/)

*   初始化一个 DP[][]数组，其中 **dp[i][j]** 存储的数字计数为 **i** 位，以 **j** 结尾。
*   将数组从 **2** 迭代到 **N** 并检查最后一位数字是否为 j，则该位置允许的数字在范围**(最大值(0，j-k)，最小值(9，j+k))** 内。对此范围执行范围更新。
*   现在用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)得到实际答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return count
// of N-digit numbers with
// absolute difference of
// adjacent digits not
// exceeding K
long long getCount(int n, int k)
{
    // For 1-digit numbers,
    // the count is 10
    if (n == 1)
        return 10;

    long long dp[n + 1][11];

    // dp[i][j] stores the number
    // of such i-digit numbers
    // ending in j
    for (int i = 0; i <= n; i++) {
        for (int j = 0; j < 11; j++)
            dp[i][j] = 0;
    }
    // Initialize count for
    // 1-digit numbers
    for (int i = 1; i <= 9; i++)
        dp[1][i] = 1;

    // Compute values for count of
    // digits greater than 1
    for (int i = 2; i <= n; i++) {
        for (int j = 0; j <= 9; j++) {

            // Find the range of allowed
            // numbers if last digit is j
            int l = max(0, j - k);
            int r = min(9, j + k);

            // Perform Range update
            dp[i][l] += dp[i - 1][j];
            dp[i][r + 1] -= dp[i - 1][j];
        }

        // Prefix sum to find actual
        // values of i-digit numbers
        // ending in j
        for (int j = 1; j <= 9; j++)
            dp[i][j] += dp[i][j - 1];
    }

    // Stores the final answer
    long long count = 0;
    for (int i = 0; i <= 9; i++)
        count += dp[n][i];

    return count;
}

// Driver Code
int main()
{
    int N = 2, K = 1;
    cout << getCount(N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG {

    // Function to return count of such numbers
    public static long getCount(int n, int k)
    {
        // For 1-digit numbers, the count
        // is 10 irrespective of K
        if (n == 1)
            return 10;

        // dp[i][j] stores the number
        // of such i-digit numbers
        // ending in j
        long dp[][]
            = new long[n + 1][11];

        // Initialize count for
        // 1-digit numbers
        for (int i = 1; i <= 9; i++)
            dp[1][i] = 1;

        // Compute values for count of
        // digits greater than 1
        for (int i = 2; i <= n; i++) {
            for (int j = 0; j <= 9; j++) {

                // Find the range of allowed
                // numbers if last digit is j
                int l = Math.max(0, j - k);
                int r = Math.min(9, j + k);

                // Perform Range update
                dp[i][l] += dp[i - 1][j];
                dp[i][r + 1] -= dp[i - 1][j];
            }

            // Prefix sum to find actual values
            // of i-digit numbers ending in j
            for (int j = 1; j <= 9; j++)
                dp[i][j] += dp[i][j - 1];
        }

        // Stores the final answer
        long count = 0;
        for (int i = 0; i <= 9; i++)
            count += dp[n][i];
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 2, k = 1;
        System.out.println(getCount(n, k));
    }
}
```

## 蟒蛇 3

```
# Python 3 Program to implement
# the above approach

# Function to return count
# of N-digit numbers with
# absolute difference of
# adjacent digits not
# exceeding K
def getCount(n, k):

    # For 1-digit numbers, the
    # count is 10
    if n == 1:
        return 10

    # dp[i][j] stores the count of
    # i-digit numbers ending with j       
    dp = [[0 for x in range(11)]
            for y in range(n + 1)];    

    # Initialize count for
    # 1-digit numbers
    for i in range(1, 10):
        dp[1][i]= 1

    # Compute values for count
    # of digits greater than 1
    for i in range(2, n + 1):
        for j in range(0, 10):

            # Find the range of allowed
            # numbers if last digit is j
            l = max(0, j - k)
            r = min(9, j + k)

            # Perform Range update
            dp[i][l] = dp[i][l] + dp[i-1][j]
            dp[i][r + 1] = dp[i][r + 1] - dp[i-1][j]

        # Prefix sum to find count of
        # of i-digit numbers ending with j
        for j in range(1, 10):
            dp[i][j] = dp[i][j] + dp[i][j-1]

    # Stores the final answer
    count = 0

    for i in range(0, 10):
        count = count + dp[n][i]
    return count

# Driver Code
n, k = 2, 1
print(getCount(n, k))
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG {

    // Function to return the
    // count of N-digit numbers
    // with absolute difference of
    // adjacent digits not exceeding K
    static long getCount(int n, int k)
    {
        // For 1-digit numbers, the
        // count is 10
        if (n == 1)
            return 10;

        // dp[i][j] stores the count of
        // i-digit numbers ending with j
        long[, ] dp = new long[n + 1, 11];

        // Initialize count for
        // 1-digit numbers
        for (int i = 1; i <= 9; i++)
            dp[1, i] = 1;

        // Compute values for count of
        // digits greater than 1
        for (int i = 2; i <= n; i++) {
            for (int j = 0; j <= 9; j++) {

                // Find the range of allowed
                // numbers with last digit j
                int l = Math.Max(0, j - k);
                int r = Math.Min(9, j + k);

                // Perform Range update
                dp[i, l] += dp[i - 1, j];
                dp[i, r + 1] -= dp[i - 1, j];
            }

            // Prefix sum to count i-digit
            // numbers ending in j
            for (int j = 1; j <= 9; j++)
                dp[i, j] += dp[i, j - 1];
        }

        // Stores the final answer
        long count = 0;
        for (int i = 0; i <= 9; i++)
            count += dp[n, i];
        return count;
    }

    // Driver Code
    public static void Main()
    {
        int n = 2, k = 1;
        Console.WriteLine(getCount(n, k));
    }
}
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Function to return count
// of N-digit numbers with
// absolute difference of
// adjacent digits not
// exceeding K
function getCount(n, k)
{

    // For 1-digit numbers, the count
    // is 10 irrespective of K
    if (n == 1)
        return 10;

    // dp[i][j] stores the number
    // of such i-digit numbers
    // ending in j
    var dp = new Array(n + 1);
    for(var i = 0; i < dp.length; i++)
        dp[i] = Array(11).fill(0);

    // Initialize count for
    // 1-digit numbers
    for(i = 1; i <= 9; i++)
        dp[1][i] = 1;

    // Compute values for count of
    // digits greater than 1
    for(i = 2; i <= n; i++)
    {
        for(j = 0; j <= 9; j++)
        {

            // Find the range of allowed
            // numbers if last digit is j
            var l = Math.max(0, j - k);
            var r = Math.min(9, j + k);

            // Perform Range update
            dp[i][l] += dp[i - 1][j];
            dp[i][r + 1] -= dp[i - 1][j];
        }

        // Prefix sum to find actual values
        // of i-digit numbers ending in j
        for(j = 1; j <= 9; j++)
            dp[i][j] += dp[i][j - 1];
    }

    // Stores the final answer
    var count = 0;
    for(i = 0; i <= 9; i++)
        count += dp[n][i];

    return count;
}

// Driver Code
var n = 2, k = 1;

document.write(getCount(n, k));

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
26
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*