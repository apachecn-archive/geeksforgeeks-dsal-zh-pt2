# 平方、加 1 或乘以 2 将 2 转化为 N 的方式数

> 原文:[https://www . geeksforgeeks . org/将 2 转换为 n 乘平方加 1 或与 2 相乘的次数/](https://www.geeksforgeeks.org/count-of-ways-to-convert-2-into-n-by-squaring-adding-1-or-multiplying-with-2/)

给定一个正数 **N** ，任务是从 2 中找出到达 **N** 的方法数，其中每个操作可以执行以下操作之一:

*   在当前数字上加 1。
*   将当前数字乘以 2。
*   将当前数字平方。

**示例:**

> **输入:** N = 5
> **输出:** 3
> **说明:**整数5 可以通过以下方式达到:
> 
> *   2 (+1) => 3 (+1) => 4 (+1) => 5
> *   2 (*2) => 4 (+1) => 5
> *   2 (^2) => 4 (+1) => 5
> 
> 因此，从 2 到 5 的途径数是 3。
> 
> **输入:**N = 9
> T3】输出: 8

**方法:**使用[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)可以高效地解决给定的问题。想法是使用 DP [数组](https://www.geeksforgeeks.org/array-data-structure/)来计算从 2 到达 **N** 所需的路数。[从 2 到 **N** 迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **Dp** ，每次迭代后执行上述操作，计算到达 **N** 所需的路数，即 **Dp[i] = > Dp[i+1]** 、 **Dp[i] = > Dp[2 * i]** 、**Dp[I]=>Dp[I]因此，在上述所有三种状态中，增加达到 **Dp[i]** 的途径数。存储在 **Dp[N]** 的值是要求的答案。**

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// number of ways required
// to reach N from 2
int waysToReach(int N)
{

    // Initialize a DP array
    vector<int> Dp(N + 1, 0);

    // Initialize a DP[2] by 1
    Dp[2] = 1;

    // Iterate the array from 2 to N
    for (int i = 2; i <= N; i++) {

        // If i+1 is not out of bounds
        if (i + 1 <= N) {

            // Add the number of ways
            Dp[i + 1] += Dp[i];
        }

        // If i*2 is not out of bounds
        if (i * 2 <= N) {

            // Add the number of ways
            Dp[i * 2] += Dp[i];
        }

        // If i*i is not out of bounds
        if (i * i <= N) {

            // Add the number of ways
            Dp[i * i] += Dp[i];
        }
    }

    // Return the answer
    return Dp[N];
}

// Driver code
int main()
{
    int N = 5;
    cout << waysToReach(N);
    return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to calculate
    // number of ways required
    // to reach N from 2
    public static int waysToReach(int N)
    {

        // Initialize a DP array
        int[] Dp = new int[N + 1];

        // Initialize a DP[2] by 1
        Dp[2] = 1;

        // Iterate the array from 2 to N
        for (int i = 2; i <= N; i++) {

            // If i+1 is not out of bounds
            if (i + 1 <= N) {

                // Add the number of ways
                Dp[i + 1] += Dp[i];
            }

            // If i*2 is not out of bounds
            if (i * 2 <= N) {

                // Add the number of ways
                Dp[i * 2] += Dp[i];
            }

            // If i*i is not out of bounds
            if (i * i <= N) {

                // Add the number of ways
                Dp[i * i] += Dp[i];
            }
        }

        // Return the answer
        return Dp[N];
    }

    // Driver code
    public static void main(String[] args)
    {

        int N = 5;

        System.out.println(waysToReach(N));
    }
}
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to calculate
# number of ways required
# to reach N from 2
def waysToReach(N):

    # Initialize a DP array
    Dp = [0] * (N + 1)

    # Initialize a DP[2] by 1
    Dp[2] = 1

    # Iterate the array from 2 to N
    for i in range(2, N + 1):

        # If i+1 is not out of bounds
        if (i + 1 <= N):
            # Add the number of ways
            Dp[i + 1] += Dp[i]

        # If i*2 is not out of bounds
        if (i * 2 <= N):
            # Add the number of ways
            Dp[i * 2] += Dp[i]

        # If i*i is not out of bounds
        if (i * i <= N):
            # Add the number of ways
            Dp[i * i] += Dp[i]

    # Return the answer
    return Dp[N]

# Driver code
N = 5
print(waysToReach(N))

# This code is contributed by gfgking
```

## C#

```
// C# program for above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to calculate
// number of ways required
// to reach N from 2
static int waysToReach(int N)
{

    // Initialize a DP array
    int []Dp = new int[N+1];

    for(int i = 0; i < N+1; i++) {
        Dp[i] = 0;
    }

    // Initialize a DP[2] by 1
    Dp[2] = 1;

    // Iterate the array from 2 to N
    for (int i = 2; i <= N; i++) {

        // If i+1 is not out of bounds
        if (i + 1 <= N) {

            // Add the number of ways
            Dp[i + 1] += Dp[i];
        }

        // If i*2 is not out of bounds
        if (i * 2 <= N) {

            // Add the number of ways
            Dp[i * 2] += Dp[i];
        }

        // If i*i is not out of bounds
        if (i * i <= N) {

            // Add the number of ways
            Dp[i * i] += Dp[i];
        }
    }

    // Return the answer
    return Dp[N];
}

// Driver Code
public static void Main()
{
    int N = 5;

    Console.Write(waysToReach(N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to calculate
        // number of ways required
        // to reach N from 2
        function waysToReach(N) {

            // Initialize a DP array
            let Dp = new Array(N + 1).fill(0);

            // Initialize a DP[2] by 1
            Dp[2] = 1;

            // Iterate the array from 2 to N
            for (let i = 2; i <= N; i++) {

                // If i+1 is not out of bounds
                if (i + 1 <= N) {

                    // Add the number of ways
                    Dp[i + 1] += Dp[i];
                }

                // If i*2 is not out of bounds
                if (i * 2 <= N) {

                    // Add the number of ways
                    Dp[i * 2] += Dp[i];
                }

                // If i*i is not out of bounds
                if (i * i <= N) {

                    // Add the number of ways
                    Dp[i * i] += Dp[i];
                }
            }

            // Return the answer
            return Dp[N];
        }

        // Driver code
        let N = 5;
        document.write(waysToReach(N));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)