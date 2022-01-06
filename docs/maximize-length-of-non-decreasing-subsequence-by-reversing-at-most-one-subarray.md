# 通过最多反转一个子阵列

来最大化非递减子序列的长度

> 原文:[https://www . geesforgeks . org/通过最多反转一个子阵列来最大化非递减子序列的长度/](https://www.geeksforgeeks.org/maximize-length-of-non-decreasing-subsequence-by-reversing-at-most-one-subarray/)

给定一个二进制[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到通过最多反转一次子阵列可以生成的非递减子序列的最大可能长度。

**示例:**

> **输入:** arr[] = {0，1，0，1}
> **输出:** 4
> **解释:**
> 将子阵列从索引[2，3]反转后，阵列修改为{0，0，1，1}。
> 因此，最长的非递减子序列是{0，0，1，1}。
> 
> **输入:** arr[] = {0，1，1，1，0，0，1，0}
> **输出:** 9
> **解释:**
> 将子阵列从索引[2，6]反转后，阵列修改为{0，0，0，1，1，1，1，1，1，0}。
> 因此，最长的非递减子序列是{0，0，0，1，1，1，1，1}。

**天真法:**解决问题最简单的方法是反转给定阵列中每个可能的子阵列，反转子阵列后从阵列中找到最长的[非递减子序列](https://www.geeksforgeeks.org/non-decreasing-subsequence-of-size-k-with-minimum-sum/)。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*
**高效途径:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决问题。按照以下步骤操作:

*   因为数组是二进制数组，所以我们的想法是在形式**{ 0…{ 0 }**， **{0…1…}** ， **{0】的子序列中找到最长的子序列..一..0…}, 0..一..0..1** 。
*   将动态编程表初始化为 **dp[][]** ，该表存储以下内容:

> dp[i][0]:存储最长子序列的长度(0..)从 a[0]到 I。
> dp[i][1]:存储最长子序列的长度(0..一..)从 a[0]到 I。
> dp[i][2]:存储最长子序列的长度(0..一..0..)从 a[0]到 I。
> dp[i][3]:存储最长子序列的长度(0..一..0..一..)从 a[0]到 I。

*   因此，答案是所有 4 种给定可能性中最长的子序列或最大值 **( dp[n-1][0]、d[n-1][1]、dp[n-1][2]、dp[n-1][3] )** 。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the maximum length
// non decreasing subarray by reversing
// at most one subarray
void main_fun(int arr[], int n)
{

    // dp[i][j] be the longest
    // subsequence of a[0...i]
    // with first j parts
    int dp[4][n];
    memset(dp, 0, sizeof(dp[0][0] * 4 * n));

    if (arr[0] == 0)
        dp[0][0] = 1;
    else
        dp[1][0] = 1;

    // Maximum length sub-sequence
    // of (0..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 0)
            dp[0][i] = dp[0][i - 1] + 1;
        else
            dp[0][i] = dp[0][i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 1)
            dp[1][i] = max(dp[1][i - 1] + 1,
                           dp[0][i - 1] + 1);
        else
            dp[1][i] = dp[1][i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..0..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 0)
        {
            dp[2][i] = max(dp[2][i - 1] + 1,
                           max(dp[1][i - 1] + 1,
                               dp[0][i - 1] + 1));
        }
        else
            dp[2][i] = dp[2][i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..0..1..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 1)
        {
            dp[3][i] = max(dp[3][i - 1] + 1,
                            max(dp[2][i - 1] + 1,
                                max(dp[1][i - 1] + 1,
                                    dp[0][i - 1] + 1)));
        }
        else
            dp[3][i] = dp[3][i - 1];
    }

    // Find the max length subsequence
    int ans = max(dp[2][n - 1], max(dp[1][n - 1],
              max(dp[0][n - 1], dp[3][n - 1])));

    // Print the answer
    cout << (ans);
}

// Driver Code
int main()
{
    int n = 4;
    int arr[] = {0, 1, 0, 1};

    main_fun(arr, n);
    return 0;
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the maximum length
// non decreasing subarray by reversing
// at most one subarray
static void main_fun(int arr[], int n)
{

    // dp[i][j] be the longest
    // subsequence of a[0...i]
    // with first j parts
    int[][] dp = new int[4][n];

    if (arr[0] == 0)
        dp[0][0] = 1;
    else
        dp[1][0] = 1;

    // Maximum length sub-sequence
    // of (0..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 0)
            dp[0][i] = dp[0][i - 1] + 1;
        else
            dp[0][i] = dp[0][i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 1)
            dp[1][i] = Math.max(dp[1][i - 1] + 1,
                                dp[0][i - 1] + 1);
        else
            dp[1][i] = dp[1][i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..0..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 0)
        {
            dp[2][i] = Math.max(dp[2][i - 1] + 1,
                       Math.max(dp[1][i - 1] + 1,
                                dp[0][i - 1] + 1));
        }
        else
            dp[2][i] = dp[2][i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..0..1..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 1)
        {
            dp[3][i] = Math.max(dp[3][i - 1] + 1,
                       Math.max(dp[2][i - 1] + 1,
                       Math.max(dp[1][i - 1] + 1,
                                dp[0][i - 1] + 1)));
        }
        else
            dp[3][i] = dp[3][i - 1];
    }

    // Find the max length subsequence
    int ans = Math.max(dp[2][n - 1],
              Math.max(dp[1][n - 1],
              Math.max(dp[0][n - 1],
                       dp[3][n - 1])));

    // Print the answer
    System.out.print(ans);
}

// Driver code
public static void main (String[] args)
{
    int n = 4;
    int arr[] = { 0, 1, 0, 1 };

    main_fun(arr, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to find the maximum length
# non decreasing subarray by reversing
# at most one subarray
def main(arr, n):

    # dp[i][j] be the longest
    # subsequence of a[0...i]
    # with first j parts
    dp = [[0 for x in range(n)] for y in range(4)]

    if arr[0] == 0:
        dp[0][0] = 1
    else:
        dp[1][0] = 1

    # Maximum length sub-sequence
    # of (0..)
    for i in range(1, n):
        if arr[i] == 0:
            dp[0][i] = dp[0][i-1] + 1
        else:
            dp[0][i] = dp[0][i-1]

    # Maximum length sub-sequence
    # of (0..1..)
    for i in range(1, n):
        if arr[i] == 1:
            dp[1][i] = max(dp[1][i-1] + 1, dp[0][i-1] + 1)
        else:
            dp[1][i] = dp[1][i-1]

    # Maximum length sub-sequence
    # of (0..1..0..)
    for i in range(1, n):
        if arr[i] == 0:
            dp[2][i] = max([dp[2][i-1] + 1,
                            dp[1][i-1] + 1,
                            dp[0][i-1] + 1])
        else:
            dp[2][i] = dp[2][i-1]

    # Maximum length sub-sequence
    # of (0..1..0..1..)
    for i in range(1, n):
        if arr[i] == 1:
            dp[3][i] = max([dp[3][i-1] + 1,
                            dp[2][i-1] + 1,
                            dp[1][i-1] + 1,
                            dp[0][i-1] + 1])
        else:
            dp[3][i] = dp[3][i-1]

    # Find the max length subsequence
    ans = max([dp[2][n-1], dp[1][n-1],
            dp[0][n-1], dp[3][n-1]])

    # Print the answer
    print(ans)

# Driver Code
if __name__ == "__main__":
    n = 4
    arr = [0, 1, 0, 1]
    main(arr, n)
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the maximum length
// non decreasing subarray by reversing
// at most one subarray
static void main_fun(int []arr, int n)
{

    // dp[i,j] be the longest
    // subsequence of a[0...i]
    // with first j parts
    int[,] dp = new int[4, n];

    if (arr[0] == 0)
        dp[0, 0] = 1;
    else
        dp[1, 0] = 1;

    // Maximum length sub-sequence
    // of (0..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 0)
            dp[0, i] = dp[0, i - 1] + 1;
        else
            dp[0, i] = dp[0, i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 1)
            dp[1, i] = Math.Max(dp[1, i - 1] + 1,
                                dp[0, i - 1] + 1);
        else
            dp[1, i] = dp[1, i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..0..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 0)
        {
            dp[2, i] = Math.Max(dp[2, i - 1] + 1,
                       Math.Max(dp[1, i - 1] + 1,
                                dp[0, i - 1] + 1));
        }
        else
            dp[2, i] = dp[2, i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..0..1..)
    for(int i = 1; i < n; i++)
    {
        if (arr[i] == 1)
        {
            dp[3, i] = Math.Max(dp[3, i - 1] + 1,
                       Math.Max(dp[2, i - 1] + 1,
                       Math.Max(dp[1, i - 1] + 1,
                                dp[0, i - 1] + 1)));
        }
        else
            dp[3, i] = dp[3, i - 1];
    }

    // Find the max length subsequence
    int ans = Math.Max(dp[2, n - 1],
              Math.Max(dp[1, n - 1],
              Math.Max(dp[0, n - 1],
                       dp[3, n - 1])));

    // Print the answer
    Console.Write(ans);
}

// Driver code
public static void Main(String[] args)
{
    int n = 4;
    int []arr = { 0, 1, 0, 1 };

    main_fun(arr, n);
}
}

// This code is contributed by Amit Katiyar 
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the maximum length
// non decreasing subarray by reversing
// at most one subarray
function main_fun(arr, n)
{

    // dp[i][j] be the longest
    // subsequence of a[0...i]
    // with first j parts
    var dp = Array.from(Array(4), ()=>Array(n).fill(0));

    if (arr[0] == 0)
        dp[0][0] = 1;
    else
        dp[1][0] = 1;

    // Maximum length sub-sequence
    // of (0..)
    for(var i = 1; i < n; i++)
    {
        if (arr[i] == 0)
            dp[0][i] = dp[0][i - 1] + 1;
        else
            dp[0][i] = dp[0][i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..)
    for(var i = 1; i < n; i++)
    {
        if (arr[i] == 1)
            dp[1][i] = Math.max(dp[1][i - 1] + 1,
                           dp[0][i - 1] + 1);
        else
            dp[1][i] = dp[1][i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..0..)
    for(var i = 1; i < n; i++)
    {
        if (arr[i] == 0)
        {
            dp[2][i] = Math.max(dp[2][i - 1] + 1,
                           Math.max(dp[1][i - 1] + 1,
                               dp[0][i - 1] + 1));
        }
        else
            dp[2][i] = dp[2][i - 1];
    }

    // Maximum length sub-sequence
    // of (0..1..0..1..)
    for(var i = 1; i < n; i++)
    {
        if (arr[i] == 1)
        {
            dp[3][i] = Math.max(dp[3][i - 1] + 1,
                            Math.max(dp[2][i - 1] + 1,
                                Math.max(dp[1][i - 1] + 1,
                                    dp[0][i - 1] + 1)));
        }
        else
            dp[3][i] = dp[3][i - 1];
    }

    // Find the max length subsequence
    var ans = Math.max(dp[2][n - 1], Math.max(dp[1][n - 1],
              Math.max(dp[0][n - 1], dp[3][n - 1])));

    // Print the answer
    document.write(ans);
}

// Driver Code
var n = 4;
var arr = [0, 1, 0, 1];

main_fun(arr, n);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*