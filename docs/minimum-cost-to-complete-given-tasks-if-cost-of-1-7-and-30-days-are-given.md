# 如果给定 1、7 和 30 天的成本，完成给定任务的最小成本

> 原文:[https://www . geesforgeks . org/完成给定任务的最低成本-如果给定了 1-7 天和 30 天的成本/](https://www.geeksforgeeks.org/minimum-cost-to-complete-given-tasks-if-cost-of-1-7-and-30-days-are-given/)

给定排序的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**由 **N** 正整数组成，使得**arr【I】**代表工人将要工作的天数，以及大小为 **3** 的数组**成本【】**代表支付给工人的工资，分别为 **1 天**、 **7 天**和 **30 天**，任务是找到所需的最小成本

**示例:**

> **输入:**arr[]=【2，4，6，7，8，10，17】，成本[]=【3，8，20】
> **输出:** 14
> **说明:**
> 以下是以最小成本雇佣工人的可能方式之一:
> 
> 1.  在第 2 天，打电话给工人 1 天，费用为[0] = 3。
> 2.  在第 4 天，打电话给工人 7 天，费用[1] = 8，包括第 4、5、…、10 天。
> 3.  在第 17 天，呼叫工人 1 天，费用[0] = 3，包括第 17 天。
> 
> 因此，总成本为 3 + 8 + 3 = 14，这在所有可能的雇佣工人组合中是最小的。
> 
> **输入:**arr[]=【1，2，3，4，6，7，8，9，11，15，20，29】，成本=【3，8，10】
> **输出:** 10

**方法:**上述问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决，因为它有[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)和[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。按照以下步骤解决问题:

*   初始化一个数组，比如说 **dp[]** ，其中 **dp[i]** 存储在**【I，arr[N–1]】**这几天需要一个工人的最低成本。
*   将**DP[arr[N–1]]的值初始化为**{成本[0]、成本[1]、成本[2]}** 的最小值。**
*   初始化一个变量，比如说指向数组当前元素的**ptr****arr[]**。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【arr[N–1]–1，0】**，并执行以下步骤:
    1.  如果 **ptr >的值= 0** 和**arr【ptr】= = I**那么，
        *   初始化一个变量，说 **val1** 并将该值修改为 **dp[i + 1] +成本[0]** 。
        *   初始化一个变量，说 **val2** 并将该值修改为 **dp[i + 7] +成本[1]** 。
        *   初始化一个变量，比如 **val3** ，并将该值修改为 **dp[i + 30] +成本[2]** 。
        *   现在，将 **dp[i]** 的值更新为 **{val1，val2，val3}** 的最小值。
        *   将 **ptr** 的值减少 **1** 。
    2.  否则，将 **dp[i]** 的值更新为 **dp[i + 1]** 。
*   完成上述步骤后，打印**DP【1】**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
// to hire the workers for the given
// days in the array days[]
int MinCost(int days[], int cost[], int N)
{
    int size = days[N - 1] + 1;

    // Initialize the array dp
    int dp[size];

    // Minimum Cost for Nth day
    dp[size - 1] = min(cost[0],
                       min(cost[1],
                           cost[2]));

    // Pointer of the array arr[]
    int ptr = N - 2;

    // Traverse from right to left
    for (int i = size - 2; i > 0; i--) {

        if (ptr >= 0 && days[ptr] == i) {

            // If worker is hired for 1 day
            int val1 = dp[i + 1] + cost[0];

            // If worker is hired for 7 days
            int val2 = cost[1]
                       + ((i + 7 >= size)
                              ? 0
                              : dp[i + 7]);

            // If worker is hired for 30 days
            int val3
                = cost[2]
                  + ((i + 30 >= size)
                         ? 0
                         : dp[i + 30]);

            // Update the value of dp[i] as
            // minimum of 3 options
            dp[i] = min(val1, min(val2, val3));
            ptr--;
        }

        // If the day is not at the
        // array arr[]
        else {
            dp[i] = dp[i + 1];
        }
    }

    // Return the answer
    return dp[1];
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 6, 7, 8, 10, 17 };
    int cost[] = { 3, 8, 20 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << MinCost(arr, cost, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

// Function to find the minimum cost
// to hire the workers for the given
// days in the array days[]
static int MinCost(int days[], int cost[], int N)
{
    int size = days[N - 1] + 1;

    // Initialize the array dp
    int []dp = new int[size];

    // Minimum Cost for Nth day
    dp[size - 1] = Math.min(cost[0], Math.min(cost[1], cost[2]));

    // Pointer of the array arr[]
    int ptr = N - 2;

    // Traverse from right to left
    for (int i = size - 2; i > 0; i--) {

        if (ptr >= 0 && days[ptr] == i) {

            // If worker is hired for 1 day
            int val1 = dp[i + 1] + cost[0];

            // If worker is hired for 7 days
            int val2 = cost[1]  + ((i + 7 >= size)
                              ? 0
                              : dp[i + 7]);

            // If worker is hired for 30 days
            int val3
                = cost[2]
                  + ((i + 30 >= size)
                         ? 0
                         : dp[i + 30]);

            // Update the value of dp[i] as
            // minimum of 3 options
            dp[i] = Math.min(val1, Math.min(val2, val3));
            ptr--;
        }

        // If the day is not at the
        // array arr[]
        else {
            dp[i] = dp[i + 1];
        }
    }

    // Return the answer
    return dp[1];
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 2, 4, 6, 7, 8, 10, 17 };
    int cost[] = { 3, 8, 20 };
    int N = arr.length;
    System.out.println(MinCost(arr, cost, N));
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to find the minimum cost
# to hire the workers for the given
# days in the array days[]
def MinCost(days, cost, N):

    size = days[N - 1] + 1

    # Initialize the array dp
    dp = [0 for i in range(size)]

    # Minimum Cost for Nth day
    dp[size - 1] = min(cost[0], min(cost[1], cost[2]))

    # Pointer of the array arr[]
    ptr = N - 2

    # Traverse from right to left
    for i in range(size - 2, 0, -1):

        if (ptr >= 0 and days[ptr] == i):

            # If worker is hired for 1 day
            val1 = dp[i + 1] + cost[0]

            # If worker is hired for 7 days
            val2 = cost[1] + ( 0 if (i + 7 >= size) else dp[i + 7])

            # If worker is hired for 30 days
            val3 = cost[2] + ( 0 if (i + 30 >= size) else dp[i + 30])

            # Update the value of dp[i] as
            # minimum of 3 options
            dp[i] = min(val1, min(val2, val3))
            ptr -= 1;

        # If the day is not at the
        # array arr[]
        else:
            dp[i] = dp[i + 1]

    # Return the answer
    return dp[1]

# Driver Code
arr = [2, 4, 6, 7, 8, 10, 17]
cost = [3, 8, 20]
N = len(arr)
print(MinCost(arr, cost, N))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum cost
// to hire the workers for the given
// days in the array days[]
static int MinCost(int[] days, int[] cost, int N)
{
    int size = days[N - 1] + 1;

    // Initialize the array dp
    int[] dp = new int[size];

    // Minimum Cost for Nth day
    dp[size - 1] = Math.Min(
        cost[0], Math.Min(cost[1], cost[2]));

    // Pointer of the array arr[]
    int ptr = N - 2;

    // Traverse from right to left
    for(int i = size - 2; i > 0; i--)
    {
        if (ptr >= 0 && days[ptr] == i)
        {

            // If worker is hired for 1 day
            int val1 = dp[i + 1] + cost[0];

            // If worker is hired for 7 days
            int val2 = cost[1] + ((i + 7 >= size) ?
                            0 : dp[i + 7]);

            // If worker is hired for 30 days
            int val3 = cost[2] + ((i + 30 >= size) ?
                            0 : dp[i + 30]);

            // Update the value of dp[i] as
            // minimum of 3 options
            dp[i] = Math.Min(val1, Math.Min(val2, val3));
            ptr--;
        }

        // If the day is not at the
        // array arr[]
        else
        {
            dp[i] = dp[i + 1];
        }
    }

    // Return the answer
    return dp[1];
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 4, 6, 7, 8, 10, 17 };
    int[] cost = { 3, 8, 20 };
    int N = arr.Length;

    Console.WriteLine(MinCost(arr, cost, N));
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>
        // JavaScript Program for the above approach

        // Function to find the minimum cost
        // to hire the workers for the given
        // days in the array days[]
        function MinCost(days, cost, N)
        {
            let size = days[N - 1] + 1;

            // Initialize the array dp
            let dp = new Array(size);

            // Minimum Cost for Nth day
            dp[size - 1] = Math.min(cost[0],
                Math.min(cost[1],
                    cost[2]));

            // Pointer of the array arr[]
            let ptr = N - 2;

            // Traverse from right to left
            for (let i = size - 2; i > 0; i--) {

                if (ptr >= 0 && days[ptr] == i) {

                    // If worker is hired for 1 day
                    let val1 = dp[i + 1] + cost[0];

                    // If worker is hired for 7 days
                    let val2 = cost[1]
                        + ((i + 7 >= size)
                            ? 0
                            : dp[i + 7]);

                    // If worker is hired for 30 days
                    let val3
                        = cost[2]
                        + ((i + 30 >= size)
                            ? 0
                            : dp[i + 30]);

                    // Update the value of dp[i] as
                    // minimum of 3 options
                    dp[i] = Math.min(val1, Math.min(val2, val3));
                    ptr--;
                }

                // If the day is not at the
                // array arr[]
                else {
                    dp[i] = dp[i + 1];
                }
            }

            // Return the answer
            return dp[1];
        }

        // Driver Code
        let arr = [2, 4, 6, 7, 8, 10, 17];
        let cost = [3, 8, 20];
        let N = arr.length;
        document.write(MinCost(arr, cost, N));

    // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
14
```

***时间复杂度:** O(M)，其中 M 为* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(M)*