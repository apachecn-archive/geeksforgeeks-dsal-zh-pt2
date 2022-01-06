# 相邻数字绝对差不超过 K 的 N 位数计数|第 2 套

> 原文:[https://www . geeksforgeeks . org/n 位数计数相邻位数绝对差不超过-k-set-2/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-with-absolute-difference-of-adjacent-digits-not-exceeding-k-set-2/)

给定两个整数 **N** 和 **K** ，任务是找出 **N 位数字**的个数，使得数字中相邻数字的绝对差值不大于 **K** 。
**举例:**

> **输入** : N = 2，K = 1
> **输出** : 26
> **解释**:数字为 10、11、12、21、22、23、32、33、34、43、44、45、54、55、56、65、66、67、76、77、78、87、88、89、98、99
> **输入**

**朴素法和动态规划法:**最简单的解法和需要 O(N)个辅助空间的动态规划法，参考[相邻位数绝对差不超过 K 的 N 位数计数](https://www.geeksforgeeks.org/count-of-n-digit-numbers-with-absolute-difference-of-adjacent-digits-not-exceeding-k/)。
**节省空间的方法:**
按照以下步骤优化上述方法:

*   在上述方法中，2D 数组 **dp[][]** 被初始化，其中 **dp[i][j]** 存储具有 **i** 位并以 **j** 结尾的数字的计数。
*   可以观察到，任何长度 **i** 的答案仅取决于为**I–1**生成的计数。因此，代替 2D 数组，初始化所有可能数字大小的数组 dp[]，并且对于每一个以数字 **j** 结束的 **i** 到 **N** 、 **dp[j]** 存储这种长度数字的计数。
*   初始化另一个数组**下一个[]** 所有可能数字的大小。
*   由于以值 **j** 结尾的一位数计数始终为 **1** ，因此最初在所有索引处用 **1** 填充 **dp[]** 。
*   迭代范围**【2，N】**，对于范围 **i** 中的每一个值，检查最后一个数字是否为 **j** ，那么这个地方允许的数字在范围**(最大值(0，j-k)，最小值(9，j+k))** 内。执行范围更新:

> next[l]= next[l]+DP[j]
> next[r+1]= next[r+1]–DP[j]
> 其中 l 和 r 分别为 max(0，j–k)和 min(9，j + k)。

*   一旦对特定值 **i** 完成上述步骤，计算**next【】**的前缀和并用**next【】**的值更新**DP【】**。

以下是上述方法的实现:

## C

```
// C program to implement the above approach
#include <stdio.h>

// Function to find maximum between two numbers
int max(int num1, int num2)
{
    return (num1 > num2 ) ? num1 : num2;
}

// Function to find minimum between two numbers
int min(int num1, int num2)
{
    return (num1 > num2 ) ? num2 : num1;
}

// Function to return the count
// of such numbers
int getCount(int n, int k)
{

    // For 1-digit numbers, the count
    // is 10 irrespective of K
    if (n == 1)
        return 10;

    // dp[j] stores the number
    // of such i-digit numbers
    // ending with j
    int dp[11] = {0};

    // Stores the results of length i
    int next[11] = {0};

    // Initialize count for
    // 1-digit numbers
    for(int i = 1; i <= 9; i++)
        dp[i] = 1;

    // Compute values for count of
    // digits greater than 1
    for(int i = 2; i <= n; i++)
    {
        for(int j = 0; j <= 9; j++)
        {

            // Find the range of allowed
            // numbers if last digit is j
            int l = max(0, (j - k));
            int r = min(9, (j + k));

            // Perform Range update
            next[l] += dp[j];
            next[r + 1] -= dp[j];
        }

        // Prefix sum to find actual count
        // of i-digit numbers ending with j
        for(int j = 1; j <= 9; j++)
            next[j] += next[j - 1];

        // Update dp[]
        for(int j = 0; j < 10; j++)
        {
            dp[j] = next[j];
            next[j] = 0;
        }
    }

    // Stores the final answer
    int count = 0;
    for(int i = 0; i <= 9; i++)
        count += dp[i];

    // Return the final answer
    return count;
}

// Driver Code
int main()
{
    int n = 2, k = 1;
    printf("%d", getCount(n, k));
}

// This code is contributed by piyush3010.
```

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum between two numbers
int max(int num1, int num2)
{
    return (num1 > num2 ) ? num1 : num2;
}

// Function to find minimum between two numbers
int min(int num1, int num2)
{
    return (num1 > num2 ) ? num2 : num1;
}

// Function to return the count
// of such numbers
int getCount(int n, int k)
{

    // For 1-digit numbers, the count
    // is 10 irrespective of K
    if (n == 1)
        return 10;

    // dp[j] stores the number
    // of such i-digit numbers
    // ending with j
    int dp[11] = {0};

    // Stores the results of length i
    int next[11] = {0};

    // Initialize count for
    // 1-digit numbers
    for(int i = 1; i <= 9; i++)
        dp[i] = 1;

    // Compute values for count of
    // digits greater than 1
    for(int i = 2; i <= n; i++)
    {
        for(int j = 0; j <= 9; j++)
        {

            // Find the range of allowed
            // numbers if last digit is j
            int l = max(0, (j - k));
            int r = min(9, (j + k));

            // Perform Range update
            next[l] += dp[j];
            next[r + 1] -= dp[j];
        }

        // Prefix sum to find actual count
        // of i-digit numbers ending with j
        for(int j = 1; j <= 9; j++)
            next[j] += next[j - 1];

        // Update dp[]
        for(int j = 0; j < 10; j++)
        {
            dp[j] = next[j];
            next[j] = 0;
        }
    }

    // Stores the final answer
    int count = 0;
    for(int i = 0; i <= 9; i++)
        count += dp[i];

    // Return the final answer
    return count;
}

// Driver Code
int main()
{
    int n = 2, k = 1;
    cout <<  getCount(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG {

    // Function to return the count
    // of such numbers
    public static long getCount(
        int n, int k)
    {
        // For 1-digit numbers, the count
        // is 10 irrespective of K
        if (n == 1)
            return 10;

        // dp[j] stores the number
        // of such i-digit numbers
        // ending with j
        long dp[] = new long[11];

        // Stores the results of length i
        long next[] = new long[11];

        // Initialize count for
        // 1-digit numbers
        for (int i = 1; i <= 9; i++)
            dp[i] = 1;

        // Compute values for count of
        // digits greater than 1
        for (int i = 2; i <= n; i++) {
            for (int j = 0; j <= 9; j++) {

                // Find the range of allowed
                // numbers if last digit is j
                int l = Math.max(0, j - k);
                int r = Math.min(9, j + k);

                // Perform Range update
                next[l] += dp[j];
                next[r + 1] -= dp[j];
            }

            // Prefix sum to find actual count
            // of i-digit numbers ending with j
            for (int j = 1; j <= 9; j++)
                next[j] += next[j - 1];

            // Update dp[]
            for (int j = 0; j < 10; j++) {
                dp[j] = next[j];
                next[j] = 0;
            }
        }

        // Stores the final answer
        long count = 0;
        for (int i = 0; i <= 9; i++)
            count += dp[i];

        // Return the final answer
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
# Python3 program to implement
# the above approach

# Function to return the count
# of such numbers
def getCount(n, K):

    # For 1-digit numbers, the count
    # is 10 irrespective of K
    if(n == 1):
        return 10

    # dp[j] stores the number
    # of such i-digit numbers
    # ending with j
    dp = [0] * 11

    # Stores the results of length i
    next = [0] * 11

    # Initialize count for
    # 1-digit numbers
    for i in range(1, 9 + 1):
        dp[i] = 1

    # Compute values for count of
    # digits greater than 1
    for i in range(2, n + 1):
        for j in range(9 + 1):

            # Find the range of allowed
            # numbers if last digit is j
            l = max(0, j - k)
            r = min(9, j + k)

            # Perform Range update
            next[l] += dp[j]
            next[r + 1] -= dp[j]

        # Prefix sum to find actual count
        # of i-digit numbers ending with j
        for j in range(1, 9 + 1):
            next[j] += next[j - 1]

        # Update dp[]
        for j in range(10):
            dp[j] = next[j]
            next[j] = 0

    # Stores the final answer
    count = 0
    for i in range(9 + 1):
        count += dp[i]

    # Return the final answer
    return count

# Driver code
if __name__ == '__main__':

    n = 2
    k = 1

    print(getCount(n, k))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to return the count
// of such numbers
public static long getCount(int n, int k)
{

    // For 1-digit numbers, the count
    // is 10 irrespective of K
    if (n == 1)
        return 10;

    // dp[j] stores the number
    // of such i-digit numbers
    // ending with j
    long []dp = new long[11];

    // Stores the results of length i
    long []next = new long[11];

    // Initialize count for
    // 1-digit numbers
    for(int i = 1; i <= 9; i++)
        dp[i] = 1;

    // Compute values for count of
    // digits greater than 1
    for(int i = 2; i <= n; i++)
    {
        for(int j = 0; j <= 9; j++)
        {

            // Find the range of allowed
            // numbers if last digit is j
            int l = Math.Max(0, j - k);
            int r = Math.Min(9, j + k);

            // Perform Range update
            next[l] += dp[j];
            next[r + 1] -= dp[j];
        }

        // Prefix sum to find actual count
        // of i-digit numbers ending with j
        for(int j = 1; j <= 9; j++)
            next[j] += next[j - 1];

        // Update []dp
        for(int j = 0; j < 10; j++)
        {
            dp[j] = next[j];
            next[j] = 0;
        }
    }

    // Stores the readonly answer
    long count = 0;
    for(int i = 0; i <= 9; i++)
        count += dp[i];

    // Return the readonly answer
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 2, k = 1;
    Console.WriteLine(getCount(n, k));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program to implement the above approach

// Function to find maximum between two numbers
function max(num1, num2)
{
    return (num1 > num2 ) ? num1 : num2;
}

// Function to find minimum between two numbers
function min(num1, num2)
{
    return (num1 > num2 ) ? num2 : num1;
}

// Function to return the count
// of such numbers
function getCount(n, k)
{

    // For 1-digit numbers, the count
    // is 10 irrespective of K
    if (n == 1)
        return 10;

    // dp[j] stores the number
    // of such i-digit numbers
    // ending with j
    var dp = Array(11).fill(0);

    // Stores the results of length i
    var next = Array(11).fill(0);

    // Initialize count for
    // 1-digit numbers
    for(var i = 1; i <= 9; i++)
        dp[i] = 1;

    // Compute values for count of
    // digits greater than 1
    for(var i = 2; i <= n; i++)
    {
        for(var j = 0; j <= 9; j++)
        {

            // Find the range of allowed
            // numbers if last digit is j
            var l = Math.max(0, (j - k));
            var r = Math.min(9, (j + k));

            // Perform Range update
            next[l] += dp[j];
            next[r + 1] -= dp[j];
        }

        // Prefix sum to find actual count
        // of i-digit numbers ending with j
        for(var j = 1; j <= 9; j++)
            next[j] += next[j - 1];

        // Update dp[]
        for(var j = 0; j < 10; j++)
        {
            dp[j] = next[j];
            next[j] = 0;
        }
    }

    // Stores the final answer
    var count = 0;
    for(var i = 0; i <= 9; i++)
        count += dp[i];

    // Return the final answer
    return count;
}

// Driver Code
var n = 2, k = 1;
document.write( getCount(n, k));

// This code is contributed by chinmoy1997pal.
</script>   
```

**Output:** 

```
26
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*