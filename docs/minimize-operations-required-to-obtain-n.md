# 尽量减少获得 N

所需的操作

> 原文:[https://www . geesforgeks . org/minimum-operations-required-to-get-n/](https://www.geeksforgeeks.org/minimize-operations-required-to-obtain-n/)

给定一个整数 **N** ，任务是获得 **N** ，从 **1** 开始使用最少的操作次数。可以在一个步骤中执行的操作如下:

*   把这个数乘以 2。
*   将数字乘以 3。
*   在数字上加 1。

**说明:**

> **输入:** N = 5
> **输出:** 3
> **说明:**
> 起始值:x = 1
> 
> *   x 乘以 2 : x = 2
> *   x 乘以 2 : x = 4
> *   将 1 加到 x : x = 5
> 
> 因此，所需的最小操作数= 3
> 
> **输入:** N = 15
> **输出:** 4
> **解释:**
> 获得 x = 5 所需的 3 次运算。
> x 乘以 3 : x = 15。
> 因此，所需的最小操作次数= 4

**方法:**
思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的概念。请遵循以下步骤:

*   如果已知获得小于 **N** 的任意数的最小运算，则可以计算获得 **N** 的最小运算。
*   创建以下查找表:

> **dp[i]** =从 1 获取 I 的最小操作数

*   因此，对于任意数字 **x** ，获得 **x** 所需的最小运算可以计算为:

> **dp[x] = min(dp[x-1]、dp[x/2]、dp[x/3])**

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of operations
int minOperations(int n)
{
    // Storing the minimum operations
    // to obtain all numbers up to N
    int dp[n + 1];

    // Initilal state
    dp[1] = 0;

    // Iterate for the remaining numbers
    for (int i = 2; i <= n; i++) {

        dp[i] = INT_MAX;

        // If the number can be obtained
        // by multiplication by 2
        if (i % 2 == 0) {
            int x = dp[i / 2];
            if (x + 1 < dp[i]) {
                dp[i] = x + 1;
            }
        }
        // If the number can be obtained
        // by multiplication by 3
        if (i % 3 == 0) {
            int x = dp[i / 3];
            if (x + 1 < dp[i]) {
                dp[i] = x + 1;
            }
        }

        // Obtaining the number by adding 1
        int x = dp[i - 1];
        if (x + 1 < dp[i]) {
            dp[i] = x + 1;
        }
    }

    // Return the minm operations
    // to obtain n
    return dp[n];
}

// Driver Code
int main()
{
    int n = 15;
    cout << minOperations(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG{

// Function to find the minimum number
// of operations
static int minOperations(int n)
{

    // Storing the minimum operations
    // to obtain all numbers up to N
    int dp[] = new int[n + 1];

    // Initilal state
    dp[1] = 0;

    // Iterate for the remaining numbers
    for(int i = 2; i <= n; i++)
    {
        dp[i] = Integer.MAX_VALUE;

        // If the number can be obtained
        // by multiplication by 2
        if (i % 2 == 0)
        {
            int x = dp[i / 2];
            if (x + 1 < dp[i])
            {
                dp[i] = x + 1;
            }
        }

        // If the number can be obtained
        // by multiplication by 3
        if (i % 3 == 0)
        {
            int x = dp[i / 3];
            if (x + 1 < dp[i])
            {
                dp[i] = x + 1;
            }
        }

        // Obtaining the number by adding 1
        int x = dp[i - 1];
        if (x + 1 < dp[i])
        {
            dp[i] = x + 1;
        }
    }

    // Return the minm operations
    // to obtain n
    return dp[n];
}

// Driver Code
public static void main (String []args)
{
    int n = 15;

    System.out.print( minOperations(n));
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
import sys

# Function to find the minimum number
# of operations
def minOperations(n):

    # Storing the minimum operations
    # to obtain all numbers up to N
    dp = [sys.maxsize] * (n + 1)

    # Initial state
    dp[1] = 0

    # Iterate for the remaining numbers
    for i in range(2, n + 1):

        # If the number can be obtained
        # by multiplication by 2
        if i % 2 == 0:
            x = dp[i // 2]
            if x + 1 < dp[i]:
                dp[i] = x + 1

        # If the number can be obtained
        # by multiplication by 3
        if i % 3 == 0:
            x = dp[i // 3]
            if x + 1 < dp[i]:
                dp[i] = x + 1

        # Obtaining the number by adding 1
        x = dp[i - 1]
        if x + 1 < dp[i]:
            dp[i] = x + 1

    # Return the minimum operations
    # to obtain n
    return dp[n]

# Driver code
n = 15

print(minOperations(n))

# This code is contributed by Stuti Pathak
```

## C#

```
using System;
class GFG{

// Function to find the minimum number
// of operations
static int minOperations(int n)
{

    // Storing the minimum operations
    // to obtain all numbers up to N
    int []dp = new int[n + 1];

    int x;
    // Initilal state
    dp[1] = 0;

    // Iterate for the remaining numbers
    for(int i = 2; i <= n; i++)
    {
        dp[i] = int.MaxValue;

        // If the number can be obtained
        // by multiplication by 2
        if (i % 2 == 0)
        {
            x = dp[i / 2];
            if (x + 1 < dp[i])
            {
                dp[i] = x + 1;
            }
        }

        // If the number can be obtained
        // by multiplication by 3
        if (i % 3 == 0)
        {
            x = dp[i / 3];
            if (x + 1 < dp[i])
            {
                dp[i] = x + 1;
            }
        }

        // Obtaining the number by adding 1
        x = dp[i - 1];
        if (x + 1 < dp[i])
        {
            dp[i] = x + 1;
        }
    }

    // Return the minm operations
    // to obtain n
    return dp[n];
}

// Driver Code
public static void Main (string []args)
{
    int n = 15;

    Console.Write(minOperations(n));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

// Function to find the minimum number
// of operations
function minOperations(n)
{

    // Storing the minimum operations
    // to obtain all numbers up to N
    let dp = new Array(n + 1);

    // Initilal state
    dp[1] = 0;

    // Iterate for the remaining numbers
    for(let i = 2; i <= n; i++)
    {
        dp[i] = Number.MAX_VALUE;

        // If the number can be obtained
        // by multiplication by 2
        if (i % 2 == 0)
        {
            let x = dp[parseInt(i / 2, 10)];

            if (x + 1 < dp[i])
            {
                dp[i] = x + 1;
            }
        }

        // If the number can be obtained
        // by multiplication by 3
        if (i % 3 == 0)
        {
            let x = dp[parseInt(i / 3, 10)];
            if (x + 1 < dp[i])
            {
                dp[i] = x + 1;
            }
        }

        // Obtaining the number by adding 1
        let x = dp[i - 1];

        if (x + 1 < dp[i])
        {
            dp[i] = x + 1;
        }
    }

    // Return the minm operations
    // to obtain n
    return dp[n];
}

// Driver code
let n = 15;

document.write(minOperations(n));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*