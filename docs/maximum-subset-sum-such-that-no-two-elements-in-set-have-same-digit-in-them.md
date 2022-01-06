# 最大子集和，使得集合中没有两个元素具有相同的数字

> 原文:[https://www . geeksforgeeks . org/最大子集和集合中没有两个元素的位数相同/](https://www.geeksforgeeks.org/maximum-subset-sum-such-that-no-two-elements-in-set-have-same-digit-in-them/)

给定一个由 N 个元素组成的数组。找出具有最大和的元素子集，使得子集中没有两个元素具有共同的数字。
**例:**

> **输入:**数组[] = {22，132，4，45，12，223}
> **输出:** 268
> 最大和子集将= {45，223}。
> 除 1 外，所有可能的数字都存在。
> 但要包括 1，则 2 或 2 和 3 都要删除
> ，这将导致较小的和值。
> **输入:**数组[] = {1，21，32，4，5 }
> **输出:** 42

*   这里我们可以使用动态编程和位屏蔽来解决这个问题。
*   考虑每个数字的 10 位表示，其中如果该数字中存在对应于该位的数字，则每个位为 1。
*   现在维护一个 dp[i]，它存储集合中所有数字可能达到的最大和，对应于 I 的二进制表示中的 1 位位置
*   递归关系的形式将是 **dp[i] = max(dp[i]，dp[i^mask] + a[j])** ，对于从 1 到 n 的所有那些 j，使得掩码(a[j]的 10 位表示)满足 i || mask = i(此后，只有我们能够确保 I 中所有可用的数字都得到满足)。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;
int dp[1024];

// Function to create mask for every number
int get_binary(int u)
{
    int ans = 0;
    while (u) {
        int rem = u % 10;
        ans |= (1 << rem);
        u /= 10;
    }

    return ans;
}

// Recursion for Filling DP array
int recur(int u, int array[], int n)
{
    // Base Condition
    if (u == 0)
        return 0;
    if (dp[u] != -1)
        return dp[u];

    int temp = 0;
    for (int i = 0; i < n; i++) {
        int mask = get_binary(array[i]);

        // Recurrence Relation
        if ((mask | u) == u) {
            dp[u] = max(max(0,
                    dp[u ^ mask]) + array[i], dp[u]);
        }
    }

    return dp[u];
}

// Function to find Maximum Subset Sum
int solve(int array[], int n)
{
    // Initialize DP array
    for (int i = 0; i < (1 << 10); i++) {
        dp[i] = -1;
    }

    int ans = 0;

    // Iterate over all possible masks of 10 bit number
    for (int i = 0; i < (1 << 10); i++) {
        ans = max(ans, recur(i, array, n));
    }

    return ans;
}

// Driver Code
int main()
{
    int array[] = { 22, 132, 4, 45, 12, 223 };
    int n = sizeof(array) / sizeof(array[0]);

    cout << solve(array, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG
{

static int []dp = new int [1024];

// Function to create mask for every number
static int get_binary(int u)
{
    int ans = 0;
    while (u > 0)

    {
        int rem = u % 10;
        ans |= (1 << rem);
        u /= 10;
    }

    return ans;
}

// Recursion for Filling DP array
static int recur(int u, int []array, int n)
{
    // Base Condition
    if (u == 0)
        return 0;
    if (dp[u] != -1)
        return dp[u];

    for (int i = 0; i < n; i++)
    {
        int mask = get_binary(array[i]);

        // Recurrence Relation
        if ((mask | u) == u)
        {
            dp[u] = Math.max(Math.max(0,
                    dp[u ^ mask]) + array[i], dp[u]);
        }
    }

    return dp[u];
}

// Function to find Maximum Subset Sum
static int solve(int []array, int n)
{
    // Initialize DP array
    for (int i = 0; i < (1 << 10); i++)
    {
        dp[i] = -1;
    }

    int ans = 0;

    // Iterate over all possible masks of 10 bit number
    for (int i = 0; i < (1 << 10); i++)
    {
        ans = Math.max(ans, recur(i, array, n));
    }

    return ans;
}

// Driver Code
static public void main (String[] args)
{
    int []array = { 22, 132, 4, 45, 12, 223 };
    int n = array.length;

    System.out.println(solve(array, n));
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of above approach

dp = [0]*1024;

# Function to create mask for every number
def get_binary(u) :

    ans = 0;
    while (u) :
        rem = u % 10;
        ans |= (1 << rem);
        u //= 10;
    return ans;

# Recursion for Filling DP array
def recur(u, array, n) :

    # Base Condition
    if (u == 0) :
        return 0;

    if (dp[u] != -1) :
        return dp[u];

    temp = 0;
    for i in range(n) :
        mask = get_binary(array[i]);

        # Recurrence Relation
        if ((mask | u) == u) :
            dp[u] = max(max(0, dp[u ^ mask]) + array[i], dp[u]);

    return dp[u];

# Function to find Maximum Subset Sum
def solve(array, n)  :
    i = 0

    # Initialize DP array
    while(i < (1 << 10)) :
        dp[i] = -1;
        i += 1

    ans = 0;

    i = 0
    # Iterate over all possible masks of 10 bit number
    while(i < (1 << 10)) :
        ans = max(ans, recur(i, array, n));

        i += 1

    return ans;

# Driver Code
if __name__ ==  "__main__" :

    array = [ 22, 132, 4, 45, 12, 223 ] ;
    n = len(array);

    print(solve(array, n));

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

static int []dp = new int [1024];

// Function to create mask for every number
static int get_binary(int u)
{
    int ans = 0;
    while (u > 0)

    {
        int rem = u % 10;
        ans |= (1 << rem);
        u /= 10;
    }

    return ans;
}

// Recursion for Filling DP array
static int recur(int u, int []array, int n)
{
    // Base Condition
    if (u == 0)
        return 0;
    if (dp[u] != -1)
        return dp[u];

    for (int i = 0; i < n; i++)
    {
        int mask = get_binary(array[i]);

        // Recurrence Relation
        if ((mask | u) == u)
        {
            dp[u] = Math.Max(Math.Max(0,
                    dp[u ^ mask]) + array[i], dp[u]);
        }
    }

    return dp[u];
}

// Function to find Maximum Subset Sum
static int solve(int []array, int n)
{
    // Initialize DP array
    for (int i = 0; i < (1 << 10); i++)
    {
        dp[i] = -1;
    }

    int ans = 0;

    // Iterate over all possible masks of 10 bit number
    for (int i = 0; i < (1 << 10); i++)
    {
        ans = Math.Max(ans, recur(i, array, n));
    }

    return ans;
}

// Driver Code
static public void Main ()
{
    int []array = { 22, 132, 4, 45, 12, 223 };
    int n = array.Length;

    Console.WriteLine (solve(array, n));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    let dp = new Array(1024);
    dp.fill(-1);

    // Function to create mask for every number
    function get_binary(u)
    {
        let ans = 0;
        while (u > 0)

        {
            let rem = u % 10;
            ans |= (1 << rem);
            u = parseInt(u / 10, 10);
        }

        return ans;
    }

    // Recursion for Filling DP array
    function recur(u, array, n)
    {
        // Base Condition
        if (u == 0)
            return 0;
        if (dp[u] != -1)
            return dp[u];

        for (let i = 0; i < n; i++)
        {
            let mask = get_binary(array[i]);

            // Recurrence Relation
            if ((mask | u) == u)
            {
                dp[u] = Math.max(Math.max(0,
                        dp[u ^ mask]) + array[i], dp[u]);
            }
        }

        return dp[u];
    }

    // Function to find Maximum Subset Sum
    function solve(array, n)
    {
        // Initialize DP array
        for (let i = 0; i < (1 << 10); i++)
        {
            dp[i] = -1;
        }

        let ans = 0;

        // Iterate over all possible masks of 10 bit number
        for (let i = 0; i < (1 << 10); i++)
        {
            ans = Math.max(ans, recur(i, array, n));
        }

        return ans;
    }

    let array = [ 22, 132, 4, 45, 12, 223 ];
    let n = array.length;

    document.write(solve(array, n));

</script>
```

**Output:** 

```
268
```

**时间复杂度:** O(N*(2^10)

**辅助空间:** O(1024)