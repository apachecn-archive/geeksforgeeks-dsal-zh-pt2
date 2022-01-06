# 用数组元素的平方替换数组元素的最大子数组和

> 原文:[https://www . geeksforgeeks . org/maximum-subarray-sum-通过按平方替换数组元素来计算可能值/](https://www.geeksforgeeks.org/maximum-subarray-sum-possible-by-replacing-an-array-element-by-its-square/)

给定一个由 **N** 个整数组成的数组**a【】**，任务是通过用其平方替换单个数组元素来找到最大子数组和。

**示例:**

> **输入:** a[] = {1，-5，8，12，-8}
> **输出:** 152
> **解释:**
> 用 144 代替 12，子阵列{8，144}生成阵列中最大可能的子阵列和。
> **输入:** a[] = {-1，-2，-3}
> **输出:** 9
> **解释:**

**天真方法:**解决问题最简单的方法是用每个元素的平方替换每个元素，并使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)为每个元素找到最大子阵和。最后，打印得到的最大可能子阵列和。
**时间复杂度:** O(N <sup>2</sup> )
**辅助空间:** O(1)

**高效方法:**上述方法可以使用 [**动态规划进行优化。**](https://www.geeksforgeeks.org/dynamic-programming/) 按照以下步骤解决问题:

*   初始化记忆表 dp[][]，其中:
*   **dp[i][0]:** 存储可以获得的最大子阵和，包括第 i <sup>个</sup>元素和第**个**个不平方任何数组元素。
*   **dp[i][1]:** 存储最大子阵列和，该最大子阵列和可以包括第 i <sup>个</sup>元素和平方一个阵列元素
*   因此，循环关系是:

> **DP[I][0]= max(DP[I-1][0]+a[I]，a[i])** ，即要么延长以**I–1**<sup>th</sup>索引结束的前一个子阵列，要么从 i <sup>th</sup> 索引开始新的子阵列。
> **DP[I][1]= max(a[I]<sup>2</sup>、dp[i-1][0] + a[i] <sup>2</sup> 、dp[i-1][1] + a[i])** ，即要么从 **i <sup>th</sup> 索引**开始新的子阵列，要么通过添加一个[i] <sup>2</sup> 到**DP<sup>来扩展之前的子阵列</sup>**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h> 
using namespace std; 

// Function to find the maximum subarray
// sum possible
int getMaxSum(int a[], int n)
{
    int dp[n][2];

    // Stores sum without squaring
    dp[0][0] = a[0];

    // Stores sum squaring
    dp[0][1] = a[0] * a[0];

    // Stores the maximum subarray sum
    int max_sum = max(dp[0][0], dp[0][1]);
    for(int i = 1; i < n; i++)
    {

        // Either extend the subarray
        // or start a new subarray
        dp[i][0] = max(a[i],
                      dp[i - 1][0] + a[i]);

        // Either extend previous squared
        // subarray or start a new subarray
        // by squaring the current element
        dp[i][1] = max(dp[i - 1][1] + a[i],
                               a[i] * a[i]);

        dp[i][1] = max(dp[i][1],
                       dp[i - 1][0] +
                       a[i] * a[i]);

        // Update maximum subarray sum
        max_sum = max(max_sum, dp[i][1]);
        max_sum = max(max_sum, dp[i][0]);
    }

    // Return answer
    return max_sum;
}

// Driver Code
int32_t main()
{
    int n = 5;
    int a[] = { 1, -5, 8, 12, -8 };

    // Function call
    cout << getMaxSum(a, n) << endl;

    return 0;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;

class GFG {

    // Function to find the maximum subarray
    // sum possible
    public static int getMaxSum(int a[], int n)
    {
        int dp[][] = new int[n][2];

        // Stores sum without squaring
        dp[0][0] = a[0];

        // Stores sum squaring
        dp[0][1] = a[0] * a[0];

        // Stores the maximum subarray sum
        int max_sum = Math.max(dp[0][0], dp[0][1]);
        for (int i = 1; i < n; i++) {

            // Either extend the subarray
            // or start a new subarray
            dp[i][0] = Math.max(a[i],
                                dp[i - 1][0] + a[i]);

            // Either extend previous squared
            // subarray or start a new subarray
            // by squaring the current element
            dp[i][1] = Math.max(dp[i - 1][1] + a[i],
                                a[i] * a[i]);

            dp[i][1]
                = Math.max(dp[i][1],
                        dp[i - 1][0] + a[i] * a[i]);

            // Update maximum subarray sum
            max_sum = Math.max(max_sum, dp[i][1]);
            max_sum = Math.max(max_sum, dp[i][0]);
        }

        // Return answer
        return max_sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        int a[] = { 1, -5, 8, 12, -8 };

        // Function call
        System.out.println(getMaxSum(a, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum subarray
# sum possible
def getMaxSum(a, n):

    dp = [[0 for x in range(2)]
            for y in range(n)]

    # Stores sum without squaring
    dp[0][0] = a[0]

    # Stores sum squaring
    dp[0][1] = a[0] * a[0]

    # Stores the maximum subarray sum
    max_sum = max(dp[0][0], dp[0][1])

    for i in range(1, n):

        # Either extend the subarray
        # or start a new subarray
        dp[i][0] = max(a[i],
                    dp[i - 1][0] + a[i])

        # Either extend previous squared
        # subarray or start a new subarray
        # by squaring the current element
        dp[i][1] = max(dp[i - 1][1] + a[i],
                        a[i] * a[i])

        dp[i][1] = max(dp[i][1],
                    dp[i - 1][0] +
                        a[i] * a[i])

        # Update maximum subarray sum
        max_sum = max(max_sum, dp[i][1])
        max_sum = max(max_sum, dp[i][0])

    # Return answer
    return max_sum

# Driver Code
n = 5
a = [ 1, -5, 8, 12, -8 ]

# Function call
print(getMaxSum(a, n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the maximum subarray
// sum possible
public static int getMaxSum(int []a, int n)
{
    int [,]dp = new int[n, 2];

    // Stores sum without squaring
    dp[0, 0] = a[0];

    // Stores sum squaring
    dp[0, 1] = a[0] * a[0];

    // Stores the maximum subarray sum
    int max_sum = Math.Max(dp[0, 0], dp[0, 1]);
    for(int i = 1; i < n; i++)
    {

        // Either extend the subarray
        // or start a new subarray
        dp[i, 0] = Math.Max(a[i],
                        dp[i - 1, 0] + a[i]);

        // Either extend previous squared
        // subarray or start a new subarray
        // by squaring the current element
        dp[i, 1] = Math.Max(dp[i - 1, 1] + a[i],
                            a[i] * a[i]);

        dp[i, 1] = Math.Max(dp[i, 1],
                            dp[i - 1, 0] +
                            a[i] * a[i]);

        // Update maximum subarray sum
        max_sum = Math.Max(max_sum, dp[i, 1]);
        max_sum = Math.Max(max_sum, dp[i, 0]);
    }

    // Return answer
    return max_sum;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;
    int []a = { 1, -5, 8, 12, -8 };

    // Function call
    Console.WriteLine(getMaxSum(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

  // Function to find the maximum subarray
    // sum possible
    function getMaxSum(a, n)
    {
        let dp = new Array(n);
        // Loop to create 2D array using 1D array
        for (var i = 0; i < dp.length; i++) {
            dp[i] = new Array(2);
        }

        // Stores sum without squaring
        dp[0][0] = a[0];

        // Stores sum squaring
        dp[0][1] = a[0] * a[0];

        // Stores the maximum subarray sum
        let max_sum = Math.max(dp[0][0], dp[0][1]);
        for (let i = 1; i < n; i++) {

            // Either extend the subarray
            // or start a new subarray
            dp[i][0] = Math.max(a[i],
                                dp[i - 1][0] + a[i]);

            // Either extend previous squared
            // subarray or start a new subarray
            // by squaring the current element
            dp[i][1] = Math.max(dp[i - 1][1] + a[i],
                                a[i] * a[i]);

            dp[i][1]
                = Math.max(dp[i][1],
                        dp[i - 1][0] + a[i] * a[i]);

            // Update maximum subarray sum
            max_sum = Math.max(max_sum, dp[i][1]);
            max_sum = Math.max(max_sum, dp[i][0]);
        }

        // Return answer
        return max_sum;
    }

// Driver Code

        let n = 5;
        let a = [ 1, -5, 8, 12, -8 ];

        // Function call
        document.write(getMaxSum(a, n));

</script>
```

**Output:** 

```
152
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*