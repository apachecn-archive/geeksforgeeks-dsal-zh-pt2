# 将数字减少到 2 所需的最小给定操作数

> 原文:[https://www . geesforgeks . org/最小给定操作数-需要将一个数减少为 2/](https://www.geeksforgeeks.org/minimum-number-of-given-operations-required-to-reduce-a-number-to-2/)

给定正整数 **N** ，任务是通过执行以下操作的最小次数将 **N** 减少到 **2** :

*   **操作 1:** 将 **N** 除以 **5** ，如果 **N** 正好被 **5** 整除。
*   **操作 2:** 从 **N** 中减去 **3** 。

*如果不可能，打印 **-1** 。*

**示例:**

> **输入:** N = 28
> **输出:** 3
> **说明:运算 1:**28 减 3。因此， **N** 变为 28–3 = 25。
> **运算 2:**25 除 5。因此 **N** 变成 25 / 5 = 5。
> **运算 3:**5 减 3。因此 **N** 变成 5–3 = 2。
> 因此，所需的最小操作数是 3。
> 
> **输入:** n=10
> **输出:** 1
> **说明:**运算 1:10 除以 5，所以 n 变成 10/5=2。
> 因此，所需的最小操作数为 1。

**天真方法:**想法是[递归](https://www.geeksforgeeks.org/recursion/)计算所需的最小步数。

*   如果该数不能被 5 整除，则从 n 中减去 3，并对修改后的 n 值进行循环，结果加 1。
*   否则进行两次递归调用，一次是从 n 中减去 3，另一次是将 n 除以 5，返回运算次数最少的一次，结果加 1。

***时间复杂度:**O(2<sup>n</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。按照以下步骤解决这个问题。

*   创建一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如 **dp[n+1]** 来存储最小操作，并用 [INT_MAX](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 初始化所有条目，其中 **dp[i]** 存储从 **i** 到达 2 所需的最小步数。
*   通过将**DP【2】**初始化为 **0** 来处理基本情况。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【2，n】**中迭代
    *   如果 **i*5 ≤ n** 的值，则更新 **dp[i*5]** 为最小 **dp[i*5]** 和 **dp[i]+1** 。
    *   如果 **i+3 ≤ n** 的值，则更新 **dp[i+3]** 至 **dp[i+3]** 和 **dp[i]+1** 的最小值。
*   打印**DP【n】**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of operations required to reduce n to 2
int findMinOperations(int n)
{
    // Initialize a dp array
    int i, dp[n + 1];

    for (i = 0; i < n + 1; i++) {
        dp[i] = 999999;
    }

    // Handle the base case
    dp[2] = 0;

    // Iterate in the range [2, n]
    for (i = 2; i < n + 1; i++) {

        // Check if i * 5 <= n
        if (i * 5 <= n) {

            dp[i * 5] = min(
dp[i * 5], dp[i] + 1);
        }

        // Check if i + 3 <= n
        if (i + 3 <= n) {

            dp[i + 3] = min(
dp[i + 3], dp[i] + 1);
        }
    }

    // Return the result
    return dp[n];
}

// Driver code
int main()
{
    // Given Input
    int n = 28;

    // Function Call
    int m = findMinOperations(n);

    // Print the result
    if (m != 9999)
        cout << m;
    else
        cout << -1;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to find the minimum number
    // of operations required to reduce n to 2
    static int findMinOperations(int n)
    {
        // Initialize a dp array
        int i = 0;
        int dp[] = new int[n + 1];

        for (i = 0; i < n + 1; i++) {
            dp[i] = 999999;
        }

        // Handle the base case
        dp[2] = 0;

        // Iterate in the range [2, n]
        for (i = 2; i < n + 1; i++) {

            // Check if i * 5 <= n
            if (i * 5 <= n) {

                dp[i * 5] = Math.min(dp[i * 5], dp[i] + 1);
            }

            // Check if i + 3 <= n
            if (i + 3 <= n) {

                dp[i + 3] = Math.min(dp[i + 3], dp[i] + 1);
            }
        }

        // Return the result
        return dp[n];
    }

    // Driver code
    public static void main(String[] args)
    {

      // Given Input
        int n = 28;

        // Function Call
        int m = findMinOperations(n);

        // Print the result
        if (m != 9999)
            System.out.println(m);
        else
            System.out.println(-1);
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of operations required to reduce n to 2
def findMinOperations(n):

    # Initialize a dp array
    dp = [0 for i in range(n + 1)]

    for i in range(n + 1):
        dp[i] = 999999

    # Handle the base case
    dp[2] = 0

    # Iterate in the range [2, n]
    for i in range(2, n + 1):

        # Check if i * 5 <= n
        if (i * 5 <= n):
            dp[i * 5] = min(dp[i * 5],
                            dp[i] + 1)

        # Check if i + 3 <= n
        if (i + 3 <= n):
            dp[i + 3] = min(dp[i + 3],
                           dp[i] + 1)

    # Return the result
    return dp[n]

# Driver code
if __name__ == '__main__':

    # Given Input
    n = 28

    # Function Call
    m = findMinOperations(n)

    # Print the result
    if (m != 9999):
        print (m)
    else:
        print (-1)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum number
// of operations required to reduce n to 2
static int findMinOperations(int n)
{

    // Initialize a dp array
    int i;
    int []dp = new int[n + 1];

    for(i = 0; i < n + 1; i++)
    {
        dp[i] = 999999;
    }

    // Handle the base case
    dp[2] = 0;

    // Iterate in the range [2, n]
    for(i = 2; i < n + 1; i++)
    {

        // Check if i * 5 <= n
        if (i * 5 <= n)
        {

            dp[i * 5] = Math.Min(dp[i * 5],
                                dp[i] + 1);
        }

        // Check if i + 3 <= n
        if (i + 3 <= n)
        {

            dp[i + 3] = Math.Min(dp[i + 3],
                                dp[i] + 1);
        }
    }

    // Return the result
    return dp[n];
}

// Driver code
public static void Main()
{

    // Given Input
    int n = 28;

    // Function Call
    int m = findMinOperations(n);

    // Print the result
    if (m != 9999)
        Console.Write(m);
    else
        Console.Write(-1);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum number
    // of operations required to reduce n to 2
function findMinOperations(n)
{
    // Initialize a dp array
        let i = 0;
        let dp = new Array(n + 1);

        for (i = 0; i < n + 1; i++) {
            dp[i] = 999999;
        }

        // Handle the base case
        dp[2] = 0;

        // Iterate in the range [2, n]
        for (i = 2; i < n + 1; i++) {

            // Check if i * 5 <= n
            if (i * 5 <= n) {

                dp[i * 5] = Math.min(dp[i * 5], dp[i] + 1);
            }

            // Check if i + 3 <= n
            if (i + 3 <= n) {

                dp[i + 3] = Math.min(dp[i + 3], dp[i] + 1);
            }
        }

        // Return the result
        return dp[n];
}

// Driver code
// Given Input
let n = 28;

// Function Call
let m = findMinOperations(n);

// Print the result
if (m != 9999)
    document.write(m);
else
    document.write(-1);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(n)*
T5**辅助空间:** O(n)