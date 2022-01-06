# 最小化清空给定数组的成本，其中移除元素的成本是其与时间瞬间的绝对差值

> 原文:[https://www . geeksforgeeks . org/最小化空给定数组的成本-其中移除元素的成本是其与时间的绝对差值-instant/](https://www.geeksforgeeks.org/minimize-cost-to-empty-given-array-where-cost-of-removing-an-element-is-its-absolute-difference-with-time-instant/)

给定由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到从数组中移除所有元素的最小成本，使得移除任何元素的成本是当前时间瞬间 **T** ( *初始 1* )和数组元素**arr【I】**之间的绝对差值，即**ABS(T–arr【I】)**，其中 **T**

**示例:**

> **输入:** arr[] = {3，6，4，2}
> **输出:** 0
> **解释:**
> T = 1:不移除
> T = 2:移除 arr[3]。成本= | 2–2 | = 0
> T = 3:移除 arr[0]。成本= | 3–3 | = 0
> T = 4:移除 arr[2]。成本= | 4–4 | = 0
> T = 5:无拆卸。
> T = 6:移除 arr[1]。成本= | 0 |+| 6–6 | = 0
> 因此，总成本= 0
> 
> **输入:** arr[] = {4，2，4，4，5，2}
> **输出:** 4

**天真的做法:**想法是用[递归](https://www.geeksforgeeks.org/recursion/)来解决问题。在每一瞬间，都有两种可能，要么移除任何元素，要么不移除。因此，为了最大限度地降低成本，[整理阵列](https://www.geeksforgeeks.org/sorting-algorithms/)。然后，从索引 **0** 和时间 **T = 1** 开始，利用以下递推关系解决问题:

> **minCost(index，time) = min(minCost(index + 1，T+1)+ABS(time–a[index])，minCost(index，T + 1))**
> 其中，基本情况:如果当前索引超过数组的当前大小。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效法:**对上述方法进行优化，思路是利用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)，因为上述递归关系存在[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[重叠子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。按照以下步骤解决问题:

*   初始化一个尺寸为 **N*2N** 的[二维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、**成本[][]** ，其中**成本[i][j]** 表示使用 **j** 时间从给定数组中删除直到 **i <sup>th</sup>** 索引的所有元素的最小成本。
*   此外，用 **0** 和变量**初始化**成本【0】【0】**，用 **0** 初始化**，其中 **prev** 将存储先前索引的所有先前成本值的最小值。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，然后，对于每个 **i** ，使用变量 **j** 迭代范围**【1，2N】**:
    *   如果**(prev+ABS(j–arr[I–1])**的值小于**成本[i][j]** ，则将**成本[i][j]** 更新为该值。
    *   如果**成本【I–1】【j】**小于 **prev** ，则将 **prev** 更新为该值。
*   完成上述步骤后，将最小成本打印为**成本【N】【j】**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define INF 10000

// Function to find the minimum cost
// to delete all array elements
void minCost(int arr[], int n)
{

    // Sort the input array
    sort(arr, arr + n);

    // Store the maximum time to delete
    // the array in the worst case
    int m = 2 * n;

    // Store the result in cost[][] table
    int cost[n + 1][m + 1];

    // Initialize the table cost[][]
    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= m; j++) {
            cost[i][j] = INF;
        }
    }

    // Base Case
    cost[0][0] = 0;

    // Store the minimum of all cost
    // values of the previous index
    int prev = 0;

    // Iterate from range [1, n]
    // using variable i
    for (int i = 1; i <= n; i++) {

        // Update prev
        prev = cost[i - 1][0];

        // Iterate from range [1, m]
        // using variable j
        for (int j = 1; j <= m; j++) {

            // Update cost[i][j]
            cost[i][j] = min(cost[i][j],
                             prev
                                 + abs(j - arr[i - 1]));

            // Update the prev
            prev = min(prev, cost[i - 1][j]);
        }
    }

    // Store the minimum cost to
    // delete all elements
    int minCost = INF;

    // Find the minimum of all values
    // of cost[n][j]
    for (int j = 1; j <= m; j++) {
        minCost = min(minCost, cost[n][j]);
    }

    // Print minimum cost
    cout << minCost;
}

// Driver Code
int main()
{
    int arr[] = { 4, 2, 4, 4, 5, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    minCost(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

class GFG{

static int INF = 10000;

// Function to find the minimum cost
// to delete all array elements
static void minCost(int arr[], int n)
{

    // Sort the input array
    Arrays.sort(arr);

    // Store the maximum time to delete
    // the array in the worst case
    int m = 2 * n;

    // Store the result in cost[][] table
    int cost[][] = new int[n + 1][m + 1];

    // Initialize the table cost[][]
    for(int i = 0; i <= n; i++)
    {
        for(int j = 0; j <= m; j++)
        {
            cost[i][j] = INF;
        }
    }

    // Base Case
    cost[0][0] = 0;

    // Store the minimum of all cost
    // values of the previous index
    int prev = 0;

    // Iterate from range [1, n]
    // using variable i
    for(int i = 1; i <= n; i++)
    {

        // Update prev
        prev = cost[i - 1][0];

        // Iterate from range [1, m]
        // using variable j
        for(int j = 1; j <= m; j++)
        {

            // Update cost[i][j]
            cost[i][j] = Math.min(cost[i][j],
                                  prev + Math.abs(
                                     j - arr[i - 1]));

            // Update the prev
            prev = Math.min(prev, cost[i - 1][j]);
        }
    }

    // Store the minimum cost to
    // delete all elements
    int minCost = INF;

    // Find the minimum of all values
    // of cost[n][j]
    for(int j = 1; j <= m; j++)
    {
        minCost = Math.min(minCost, cost[n][j]);
    }

    // Print minimum cost
    System.out.print(minCost);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 2, 4, 4, 5, 2 };
    int N = arr.length;

    // Function Call
    minCost(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

INF = 10000

# Function to find the minimum cost
# to delete all array elements
def minCost(arr, n):

    # Sort the input array
    arr = sorted(arr)

    # Store the maximum time to delete
    # the array in the worst case
    m = 2 * n

    # Store the result in cost[][] table
    cost = [[INF for i in range(m + 1)] for i in range(n + 1)]

    # Base Case
    cost[0][0] = 0

    # Store the minimum of all cost
    # values of the previous index
    prev = 0

    # Iterate from range [1, n]
    # using variable i
    for i in range(1, n + 1):

        # Update prev
        prev = cost[i - 1][0]

        # Iterate from range [1, m]
        # using variable j
        for j in range(1, m + 1):

            # Update cost[i][j]
            cost[i][j] = min(cost[i][j], prev + abs(j - arr[i - 1]))

            # Update the prev
            prev = min(prev, cost[i - 1][j])

    # Store the minimum cost to
    # delete all elements
    minCost = INF

    # Find the minimum of all values
    # of cost[n][j]
    for j in range(1, m + 1):
        minCost = min(minCost, cost[n][j])

    # Print minimum cost
    print(minCost)

# Driver Code
if __name__ == '__main__':
    arr=[4, 2, 4, 4, 5, 2]
    N = len(arr)

    # Function Call
    minCost(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int INF = 10000;

// Function to find the minimum cost
// to delete all array elements
static void minCost(int[] arr, int n)
{

    // Sort the input array
    Array.Sort(arr);

    // Store the maximum time to delete
    // the array in the worst case
    int m = 2 * n;

    // Store the result in cost[][] table
    int[,] cost = new int[n + 1, m + 1];

    // Initialize the table cost[][]
    for(int i = 0; i <= n; i++)
    {
        for(int j = 0; j <= m; j++)
        {
            cost[i, j] = INF;
        }
    }

    // Base Case
    cost[0, 0] = 0;

    // Store the minimum of all cost
    // values of the previous index
    int prev = 0;

    // Iterate from range [1, n]
    // using variable i
    for(int i = 1; i <= n; i++)
    {

        // Update prev
        prev = cost[i - 1, 0];

        // Iterate from range [1, m]
        // using variable j
        for(int j = 1; j <= m; j++)
        {

            // Update cost[i][j]
            cost[i, j] = Math.Min(cost[i, j],
                                  prev + Math.Abs(
                                     j - arr[i - 1]));

            // Update the prev
            prev = Math.Min(prev, cost[i - 1, j]);
        }
    }

    // Store the minimum cost to
    // delete all elements
    int minCost = INF;

    // Find the minimum of all values
    // of cost[n][j]
    for(int j = 1; j <= m; j++)
    {
        minCost = Math.Min(minCost, cost[n, j]);
    }

    // Print minimum cost
    Console.Write(minCost);
}

// Driver Code
public static void Main()
{
    int[] arr = { 4, 2, 4, 4, 5, 2 };
    int N = arr.Length;

    // Function Call
    minCost(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// JavaScript program for above approach

let INF = 10000;

// Function to find the minimum cost
// to delete all array elements
function minCost(arr, n)
{

    // Sort the input array
    arr.sort();

    // Store the maximum time to delete
    // the array in the worst case
    let m = 2 * n;

    // Store the result in cost[][] table
    let cost = new Array(n + 1);

    // Loop to create 2D array using 1D array
    for (var i = 0; i < cost.length; i++) {
        cost[i] = new Array(2);
    }

    // Initialize the table cost[][]
    for(let i = 0; i <= n; i++)
    {
        for(let j = 0; j <= m; j++)
        {
            cost[i][j] = INF;
        }
    }

    // Base Case
    cost[0][0] = 0;

    // Store the minimum of all cost
    // values of the previous index
    let prev = 0;

    // Iterate from range [1, n]
    // using variable i
    for(let i = 1; i <= n; i++)
    {

        // Update prev
        prev = cost[i - 1][0];

        // Iterate from range [1, m]
        // using variable j
        for(let j = 1; j <= m; j++)
        {

            // Update cost[i][j]
            cost[i][j] = Math.min(cost[i][j],
                                  prev + Math.abs(
                                     j - arr[i - 1]));

            // Update the prev
            prev = Math.min(prev, cost[i - 1][j]);
        }
    }

    // Store the minimum cost to
    // delete all elements
    let minCost = INF;

    // Find the minimum of all values
    // of cost[n][j]
    for(let j = 1; j <= m; j++)
    {
        minCost = Math.min(minCost, cost[n][j]);
    }

    // Print minimum cost
    document.write(minCost);
}

// Driver Code
     let arr = [ 4, 2, 4, 4, 5, 2 ];
    let N = arr.length;

    // Function Call
    minCost(arr, N);

// This code is contributed by avijitmondal1998.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*