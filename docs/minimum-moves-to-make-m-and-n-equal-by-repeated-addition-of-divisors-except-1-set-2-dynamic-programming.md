# 除了 1 |集合-2(动态规划)

之外，通过重复增加除数使 M 和 N 相等的最小移动

> 原文:[https://www . geeksforgeeks . org/最小移动使 m 和 n 等于除数的重复加法-除-1-集-2-动态编程/](https://www.geeksforgeeks.org/minimum-moves-to-make-m-and-n-equal-by-repeated-addition-of-divisors-except-1-set-2-dynamic-programming/)

给定两个整数 **N** 和 **M** ，任务是计算将 **N** 变为 **M** 的最小移动次数，其中一次移动允许将 **N** 当前值的除数加到除 1 以外的 **N** 本身。如果不能打印**-1”**。

**例**:

> **输入:** N = 4，M = 24
> **输出:** 5
> **说明:**N 的给定值可以通过以下步骤转换为 M:(4)+2->(6)+2->(8)+4->(12)+6->(18)+6->24。因此，移动的计数是 5，这是最小的可能。
> 
> **输入** : N = 4，M = 576
> 输出 : 14

**BFS 方法:**给定的问题已经在本文的[集 1 中讨论过了，它使用](https://www.geeksforgeeks.org/minimum-number-of-moves-to-make-m-and-n-equal-by-repeatedly-adding-any-divisor-of-number-to-itself-except-1-and-the-number/)[广度优先遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)来解决给定的问题。

**方法**:本文重点介绍一种基于[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)的不同方法。以下是要遵循的步骤:

*   创建一维[数组](https://www.geeksforgeeks.org/array-data-structure/) **dp[]** ，其中 **dp[i]** 存储从 **N** 到达 **i** 的最小操作数。最初， **dp[N+1… M] = {INT_MAX}** 和 **dp[N] = 0** 。
*   使用变量 **i** 遍历范围**【N，M】**，对于每个 **i** ，遍历[给定数字](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/) **i** 的所有因子。对于因子 **X** ，差压关系可以定义如下:

> dp[i + X] = min（ dp[i]， dp[i + X]）

*   存储在 **dp[M]** 的值是要求的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count of
// operations to convert N to M
int minOperationCnt(int N, int M)
{

    // Stores the DP state of the array
    int dp[M + 1];

    // Initialize each index with INT_MAX
    for (int i = N + 1; i <= M; i++) {
        dp[i] = INT_MAX;
    }

    // Initial condition
    dp[N] = 0;

    // Loop to iterate over range [N, M]
    for (int i = N; i <= M; i++) {

        // Check if this position
// can be reached or not
        if (dp[i] == INT_MAX) {
            continue;
        }

        // Loop to iterate through all divisors
        // of the current value i
        for (int j = 2; j * j <= i; j++) {

            // If j is a divisor of i
            if (i % j == 0) {
                if (i + j <= M) {

                    // Update the value of dp[i + j]
                    dp[i + j] = min(dp[i + j], dp[i] + 1);
                }

                // Check for value i / j;
                if (i + i / j <= M) {

                    // Update the value of dp[i + i/j]
                    dp[i + i / j]
                        = min(dp[i + i / j], dp[i] + 1);
                }
            }
        }
    }

    // Return Answer
    return (dp[M] == INT_MAX) ? -1 : dp[M];
}

// Driver Code
int main()
{
    int N = 4;
    int M = 576;

    cout << minOperationCnt(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
class GFG {

    // Function to find the minimum count of
    // operations to convert N to M
    public static int minOperationCnt(int N, int M) {

        // Stores the DP state of the array
        int[] dp = new int[M + 1];

        // Initialize each index with INT_MAX
        for (int i = N + 1; i <= M; i++) {
            dp[i] = Integer.MAX_VALUE;
        }

        // Initial condition
        dp[N] = 0;

        // Loop to iterate over range [N, M]
        for (int i = N; i <= M; i++) {

            // Check if this position
            // can be reached or not
            if (dp[i] == Integer.MAX_VALUE) {
                continue;
            }

            // Loop to iterate through all divisors
            // of the current value i
            for (int j = 2; j * j <= i; j++) {

                // If j is a divisor of i
                if (i % j == 0) {
                    if (i + j <= M) {

                        // Update the value of dp[i + j]
                        dp[i + j] = Math.min(dp[i + j], dp[i] + 1);
                    }

                    // Check for value i / j;
                    if (i + i / j <= M) {

                        // Update the value of dp[i + i/j]
                        dp[i + i / j] = Math.min(dp[i + i / j], dp[i] + 1);
                    }
                }
            }
        }

        // Return Answer
        return (dp[M] == Integer.MAX_VALUE) ? -1 : dp[M];
    }

    // Driver Code
    public static void main(String args[]) {
        int N = 4;
        int M = 576;

        System.out.println(minOperationCnt(N, M));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python implementation for the above approach
import math

INT_MAX = 2147483647

# Function to find the minimum count of
# operations to convert N to M
def minOperationCnt(N, M):

     # Stores the DP state of the array
    dp = [0 for _ in range(M + 1)]

    # Initialize each index with INT_MAX
    for i in range(N+1, M+1):
        dp[i] = INT_MAX

        # Initial condition
    dp[N] = 0

    # Loop to iterate over range [N, M]
    for i in range(N, M+1):

                # Check if this position
        # can be reached or not
        if (dp[i] == INT_MAX):
            continue

            # Loop to iterate through all divisors
            # of the current value i
        for j in range(2, int(math.sqrt(i))+1):

                        # If j is a divisor of i
            if (i % j == 0):
                if (i + j <= M):

                     # Update the value of dp[i + j]
                    dp[i + j] = min(dp[i + j], dp[i] + 1)

                    # Check for value i / j;
                if (i + i // j <= M):

                     # Update the value of dp[i + i/j]
                    dp[i + i // j] = min(dp[i + i // j], dp[i] + 1)

        # Return Answer
    if dp[M] == INT_MAX:
        return -1
    else:
        return dp[M]

# Driver Code
if __name__ == "__main__":

    N = 4
    M = 576

    print(minOperationCnt(N, M))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;
class GFG
{

  // Function to find the minimum count of
  // operations to convert N to M
  public static int minOperationCnt(int N, int M)
  {

    // Stores the DP state of the array
    int[] dp = new int[M + 1];

    // Initialize each index with INT_MAX
    for (int i = N + 1; i <= M; i++)
    {
      dp[i] = int.MaxValue;
    }

    // Initial condition
    dp[N] = 0;

    // Loop to iterate over range [N, M]
    for (int i = N; i <= M; i++)
    {

      // Check if this position
      // can be reached or not
      if (dp[i] == int.MaxValue)
      {
        continue;
      }

      // Loop to iterate through all divisors
      // of the current value i
      for (int j = 2; j * j <= i; j++)
      {

        // If j is a divisor of i
        if (i % j == 0)
        {
          if (i + j <= M)
          {

            // Update the value of dp[i + j]
            dp[i + j] = Math.Min(dp[i + j], dp[i] + 1);
          }

          // Check for value i / j;
          if (i + i / j <= M)
          {

            // Update the value of dp[i + i/j]
            dp[i + i / j] = Math.Min(dp[i + i / j], dp[i] + 1);
          }
        }
      }
    }

    // Return Answer
    return (dp[M] == int.MaxValue) ? -1 : dp[M];
  }

  // Driver Code
  public static void Main()
  {
    int N = 4;
    int M = 576;

    Console.Write(minOperationCnt(N, M));
  }
}

// This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to find the minimum count of
       // operations to convert N to M
       function minOperationCnt(N, M) {

           // Stores the DP state of the array
           let dp = new Array(M + 1)

           // Initialize each index with INT_MAX
           for (let i = N + 1; i <= M; i++) {
               dp[i] = Number.MAX_VALUE;
           }

           // Initial condition
           dp[N] = 0;

           // Loop to iterate over range [N, M]
           for (let i = N; i <= M; i++) {

               // Check if this position
               // can be reached or not
               if (dp[i] == Number.MAX_VALUE) {
                   continue;
               }

               // Loop to iterate through all divisors
               // of the current value i
               for (let j = 2; j * j <= i; j++) {

                   // If j is a divisor of i
                   if (i % j == 0) {
                       if (i + j <= M) {

                           // Update the value of dp[i + j]
                           dp[i + j] = Math.min(dp[i + j], dp[i] + 1);
                       }

                       // Check for value i / j;
                       if (i + i / j <= M) {

                           // Update the value of dp[i + i/j]
                           dp[i + i / j]
                               = Math.min(dp[i + i / j], dp[i] + 1);
                       }
                   }
               }
           }

           // Return Answer
           return (dp[M] == Number.MAX_VALUE) ? -1 : dp[M];
       }

       // Driver Code
       let N = 4;
       let M = 576;

       document.write(minOperationCnt(N, M));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
14
```

***时间复杂度:**O((M–N)*√(M–N))*
***辅助空间:** O(M)*