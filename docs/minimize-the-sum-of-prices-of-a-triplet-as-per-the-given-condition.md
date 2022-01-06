# 给定数组中三元组价格的最小可能总和

> 原文:[https://www . geeksforgeeks . org/按给定条件最小化三重价格总和/](https://www.geeksforgeeks.org/minimize-the-sum-of-prices-of-a-triplet-as-per-the-given-condition/)

给定一个由 **N** 个整数组成的**数组 num【】**，其中每个元素与另一个数组**price【】**给出的价格相关联，任务是通过取一个三元组来最小化价格的总和，使得**num[I]<num[j]<num[k]**。如果没有这样的三元组，那么打印-1。

**例:**

> **输入:** num[]={2，4，6，7，8}，price[]={10，20，100，20，40}
> **输出:** 50
> **说明:**
> 选择三联体{2，4，7}是因为(2 < 4 < 7)，价格是 10 + 20 + 20 = 50 这是最小可能的。
> **输入:** num[]={100，101，100}，price[]={2，4，5}
> **输出:** -1
> **解释:**
> 不存在可能的三元组。

**天真方法:**
最简单的方法是生成所有可能的三元组 **(i，j，k)** 这样 **i < j < k** 和**num【I】<num【j】<num【k】**然后求**价格【I】价格【j】**和**价格【k】**的和。打印所有这种三胞胎的最小总和。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效途径:**思路是使用辅助数组 **dp[]** 存储所有这类三胞胎的价格的最小和，打印其中存储的所有价格的最小值。以下是步骤:

1.  将 **dp[]** 数组初始化为 **INT_MAX** 。
2.  将当前最小和(比如**当前 _ 和**)初始化为 **INT_MAX** 。
3.  [生成所有可能的配对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **(i，j)** ，使得 **j > i** 。如果 **nums[j] > num[i]** 则更新 **dp[j] = min(dp[j]，price[i] + price[j])** ，因为这是可能的配对之一。
4.  在以上步骤的每对 **(i，j)** 中，将三胞胎的最小和更新为 **min(current_sum，dp[i] + price[j])** 。这一步将确保形成可能的三元组 **(i，j，k)** ，因为 dp[i]将在指数 **i 和 j** 处存储价格的总和，j 是 **k** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<iostream>
#include<bits/stdc++.h>
using namespace std;

// Function to minimize the sum of
// price by taking a triplet
long minSum(int n, int num[], int price[])
{

    // Initialize a dp[] array
    long dp[n];

    for(int i = 0; i < n; i++)
        dp[i] = INT_MAX;

    // Stores the final result
    long ans = INT_MAX;

    // Iterate for all values till N
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Check if num[j] > num[i]
            if (num[j] > num[i])
            {

                // Update dp[j] if it is
                // greater than stored value
                dp[j] = (long)min((long)dp[j],
                                  (long)price[i] +
                                  (long)price[j]);

                // Update the minimum
                // sum as ans
                ans = min(ans, (long)dp[i] +
                               (long)price[j]);
            }
        }
    }

    // If there is no minimum sum exist
    // then print -1 else print the ans
    return ans != INT_MAX ? ans : -1;
}

// Driver Code
int main()
{
    int num[] = { 2, 4, 6, 7, 8 };
    int price[] = { 10, 20, 100, 20, 40 };

    int n = sizeof(price) / sizeof(price[0]);

    cout << (minSum(n, num, price));
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
import java.io.*;

public class Main {

    // Function to minimize the sum of
    // price by taking a triplet
    public static long minSum(int n, int num[],
                              int price[])
    {

        // Initialize a dp[] array
        long dp[] = new long[n];

        Arrays.fill(dp, Integer.MAX_VALUE);

        // Stores the final result
        long ans = Integer.MAX_VALUE;

        // Iterate for all values till N
        for (int i = 0; i < n; i++) {

            for (int j = i + 1; j < n; j++) {

                // Check if num[j] > num[i]
                if (num[j] > num[i]) {

                    // Update dp[j] if it is
                    // greater than stored value
                    dp[j] = (long)Math.min(
                        (long)dp[j],
                        (long)price[i]
                            + (long)price[j]);

                    // Update the minimum
                    // sum as ans
                    ans = Math.min(
                        ans, (long)dp[i]
                                 + (long)price[j]);

                }
            }
        }

        // If there is no minimum sum exist
        // then print -1 else print the ans
        return ans != Integer.MAX_VALUE ? ans : -1;
    }

    // Driver Code
    public static void
        main(String[] args)
    {

        int num[] = { 2, 4, 6, 7, 8 };
        int price[] = { 10, 20, 100, 20, 40 };

        int n = price.length;

        System.out.println(minSum(n, num, price));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys;

# Function to minimize the sum of
# price by taking a triplet
def minSum(n, num, price):

    # Initialize a dp[] list
    dp = [0 for i in range(n)]
    for i in range(n):
        dp[i] = sys.maxsize

    # Stores the final result
    ans = sys.maxsize

    # Iterate for all values till N
    for i in range(n):
        for j in range(i + 1, n):

            # Check if num[j] > num[i]
            if (num[j] > num[i]):

                # Update dp[j] if it is
                # greater than stored value
                dp[j] = min(dp[j], price[i] +
                                   price[j])

                # Update the minimum
                # sum as ans
                ans = min(ans, dp[i] + price[j])

    # If there is no minimum sum exist
    # then print -1 else print the ans
    if ans is not sys.maxsize:
        return ans
    else:
        return -1

# Driver code
if __name__=='__main__':

    num = [ 2, 4, 6, 7, 8 ]
    price = [ 10, 20, 100, 20, 40 ]

    n = len(price)

    print(minSum(n, num, price))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to minimize the sum of
// price by taking a triplet
public static long minSum(int n, int []num,
                          int []price)
{

    // Initialize a []dp array
    long []dp = new long[n];
    for(int i = 0; i < n; i++)
        dp[i] = int.MaxValue;

    // Stores the readonly result
    long ans = int.MaxValue;

    // Iterate for all values till N
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Check if num[j] > num[i]
            if (num[j] > num[i])
            {

                // Update dp[j] if it is
                // greater than stored value
                dp[j] = (long)Math.Min((long)dp[j],
                                       (long)price[i] +
                                       (long)price[j]);

                // Update the minimum
                // sum as ans
                ans = Math.Min(ans, (long)dp[i] +
                                    (long)price[j]);
            }
        }
    }

    // If there is no minimum sum exist
    // then print -1 else print the ans
    return ans != int.MaxValue ? ans : -1;
}

// Driver Code
public static void Main(String[] args)
{
    int []num = { 2, 4, 6, 7, 8 };
    int []price = { 10, 20, 100, 20, 40 };

    int n = price.Length;

    Console.WriteLine(minSum(n, num, price));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

    // Function to minimize the sum of
    // price by taking a triplet
    function minSum(n, num, price)
    {

        // Initialize a dp[] array
        let dp = Array.from({length: n}, (_, i) => Number.MAX_VALUE);

        // Stores the final result
        let ans = Number.MAX_VALUE;

        // Iterate for all values till N
        for (let i = 0; i < n; i++) {

            for (let j = i + 1; j < n; j++) {

                // Check if num[j] > num[i]
                if (num[j] > num[i]) {

                    // Update dp[j] if it is
                    // greater than stored value
                    dp[j] = Math.min(
                        dp[j],
                        price[i]
                            + price[j]);

                    // Update the minimum
                    // sum as ans
                    ans = Math.min(
                        ans, dp[i]
                                 + price[j]);

                }
            }
        }

        // If there is no minimum sum exist
        // then print -1 else print the ans
        return ans != Number.MAX_VALUE ? ans : -1;
    }

// Driver Code   

        let num = [ 2, 4, 6, 7, 8 ];
        let price = [ 10, 20, 100, 20, 40 ];

        let n = price.length;

        document.write(minSum(n, num, price));

</script>
```

**Output:** 

```
50
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*