# 最小化选择和跳过数组元素以到达给定数组末尾的成本

> 原文:[https://www . geeksforgeeks . org/最小化选择和跳过数组元素以到达给定数组末尾的成本/](https://www.geeksforgeeks.org/minimize-cost-of-choosing-and-skipping-array-elements-to-reach-end-of-the-given-array/)

给定一个整数 **X** 和一个由 **N** 个整数组成的数组**成本【】**，任务是根据以下约束条件从第一个元素开始寻找到达给定数组末尾的最小成本:

*   参观点 **i** 的费用为**费用【I】**，其中 **1 ≤ i ≤ N** 。
*   成本跳过点 **i** 为 **min(成本[i]，X)** ，其中 **1 ≤ i ≤ N** 。
*   最多可连续跳过 **2** 点。
*   不能跳过第一个和最后一个位置。

**示例:**

> **输入:** N = 6，X = 4，成本[] = {6，3，9，2，1，3}
> **输出:** 19
> **解释:**
> 按照以下步骤操作:
> 第一步:选择 1 处的元素。总和= 6
> 第二步:在 2 处选择元素。Sum = 6 + 3 = 9
> 第三步:跳过 3 处的元素。总和= 6 + 3 + 4 = 13
> 第四步:选择 4 处的元素。总和= 6 + 3 + 4 + 2 = 15
> 第五步:选择 5 处的元素。总和= 6 + 3 + 4 + 2 + 1 = 16
> 第六步:选择 6 处的元素。总和= 6 + 3 + 4 + 2 + 1 + 3 = 19
> 因此，最小成本为 19。
> 
> **输入:** N = 7，X = 4，成本[] = {6，3，9，2，1，3，4}
> **输出:** 23
> **解释:**
> 按照以下步骤操作:
> 第一步:选择 1 处的元素。总和= 6
> 第二步:在 2 处选择元素。Sum = 6+3 = 9
> 第三步:跳过 3 处的元素。总和= 6+3+4 = 13
> 第四步:选择 4 处的元素。总和= 6 + 3 + 4 + 2 = 15
> 第五步:选择 5 处的元素。总和= 6+3+4+2+1 = 16
> 第六步:选择 6 处的元素。总和= 6+3+4+2+1+3 = 19
> 第七步:选择 6 处的元素。总和= 6 + 3 + 4 + 2 + 1 + 3 + 4 = 23
> 因此，最小成本为 23。

**天真方法:**最简单的方法是通过考虑或跳过某些位置来生成所有可能的解。每个元素有两个选项，即可以跳过或选择。因此最多只能有**2<sup>N</sup>T5】组合。检查每个组合中，跳过的位置不超过 **3** 。在这些组合中，选择成本最低的组合并打印成本最低的组合。**

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效途径:**优化上述途径，思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)观察，如果跳过任何位置 **i** ，成本增加**成本【I】**或 **X** 但是如果成本增加**成本【I】**那么最好选择那个位置，因为选择位置也会增加**成本【I】**。这意味着到达位置 **i** 的最小成本可以通过在到达位置**(I–1)**、 **X** +到达位置**(I–2)**和 **2X** +到达位置**(I–3)**的最小成本中取最小值来找到。

因此，dp 过渡如下:

> **dp[i] =成本[i] +分钟(dp[i-1]，分钟(2*X + dp[i-2]，2 * X+DP[I-3])**
> 其中，
> dp[i]存储从位置 0 到达位置 I 的最小答案。

按照以下步骤解决问题:

*   初始化一个数组 **dp[]** ，其中 **dp[i]** 将存储从位置 **0** 到达位置 **i** 的最小答案。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **成本【】**在范围**【0，N–1】**内，在每个位置 **i** ，更新**DP【I】**如下:

> cost[i] + min（dp[i-1]， min（2*X + dp[i-2]， 2*X + dp[i-3]））

*   完成上述步骤后，打印**dp【N–1】**，该 DP 存储从位置 **0** 到达位置**(N–1)**的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
// to reach the end of the array from
// the first element
void minimumCost(int* cost, int n, int x)
{
    // Store the results
    vector<int> dp(n + 2, 0);

    // Consider first index cost
    dp[0] = cost[0];

    // Find answer for each position i
    for (int i = 1; i < n; i++) {

        // First Element
        if (i == 1)
            dp[i] = cost[i] + dp[i - 1];

        // Second Element
        if (i == 2)
            dp[i] = cost[i]
                    + min(dp[i - 1],
                          x + dp[i - 2]);

        // For remaining element
        if (i >= 3)

            // Consider min cost for
            // skipping
            dp[i] = cost[i]
                    + min(dp[i - 1],
                          min(x + dp[i - 2],
                              2 * x + dp[i - 3]));
    }

    // Last index represents the
    // minimum total cost
    cout << dp[n - 1];
}

// Driver Code
int main()
{
    // Given X
    int X = 4;

    // Given array cost[]
    int cost[] = { 6, 3, 9, 2, 1, 3 };

    int N = sizeof(cost) / sizeof(cost[0]);

    // Function Call
    minimumCost(cost, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the minimum cost
// to reach the end of the array from
// the first element
static void minimumCost(int[] cost, int n, int x)
{

    // Store the results
    int[] dp = new int[n + 2];

    // Consider first index cost
    dp[0] = cost[0];

    // Find answer for each position i
    for(int i = 1; i < n; i++)
    {

        // First Element
        if (i == 1)
            dp[i] = cost[i] + dp[i - 1];

        // Second Element
        if (i == 2)
            dp[i] = cost[i] + Math.min(dp[i - 1],
                                   x + dp[i - 2]);

        // For remaining element
        if (i >= 3)

            // Consider min cost for
            // skipping
            dp[i] = cost[i] + Math.min(dp[i - 1],
                          Math.min(x + dp[i - 2],
                               2 * x + dp[i - 3]));
    }

    // Last index represents the
    // minimum total cost
    System.out.println(dp[n - 1]);
}

// Driver Code
public static void main(String[] args)
{

    // Given X
    int X = 4;

    // Given array cost[]
    int[] cost = { 6, 3, 9, 2, 1, 3 };

    int N = cost.length;

    // Function Call
    minimumCost(cost, N, X);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum cost
# to reach the end of the array from
# the first element
def minimumCost(cost, n, x):

    # Store the results
    dp = [0] * (n + 2)

    # Consider first index cost
    dp[0] = cost[0]

    # Find answer for each position i
    for i in range(1, n):

        # First Element
        if (i == 1):
            dp[i] = cost[i] + dp[i - 1]

        # Second Element
        if (i == 2):
            dp[i] = cost[i] + min(dp[i - 1],
                              x + dp[i - 2])

        # For remaining element
        if (i >= 3):

            # Consider min cost for
            # skipping
            dp[i] = (cost[i] +
                   min(dp[i - 1],
                   min(x + dp[i - 2],
                   2 * x + dp[i - 3])))

    # Last index represents the
    # minimum total cost
    print(dp[n - 1])

# Driver Code
if __name__ == '__main__':

    # Given X
    X = 4

    # Given array cost[]
    cost = [ 6, 3, 9, 2, 1, 3 ]

    N = len(cost)

    # Function Call
    minimumCost(cost, N, X)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum cost
// to reach the end of the array from
// the first element
static void minimumCost(int[] cost, int n, int x)
{

    // Store the results
    int[] dp = new int[n + 2];

    // Consider first index cost
    dp[0] = cost[0];

    // Find answer for each position i
    for(int i = 1; i < n; i++)
    {

        // First Element
        if (i == 1)
            dp[i] = cost[i] + dp[i - 1];

        // Second Element
        if (i == 2)
            dp[i] = cost[i] + Math.Min(dp[i - 1],
                                   x + dp[i - 2]);

        // For remaining element
        if (i >= 3)

            // Consider min cost for
            // skipping
            dp[i] = cost[i] + Math.Min(dp[i - 1],
                          Math.Min(x + dp[i - 2],
                               2 * x + dp[i - 3]));
    }

    // Last index represents the
    // minimum total cost
    Console.WriteLine(dp[n - 1]);
}

// Driver Code
public static void Main()
{

    // Given X
    int X = 4;

    // Given array cost[]
    int[] cost = { 6, 3, 9, 2, 1, 3 };

    int N = cost.Length;

    // Function Call
    minimumCost(cost, N, X);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum cost
// to reach the end of the array from
// the first element
function minimumCost(cost, n, x)
{

    // Store the results
    let dp = [];

    // Consider first index cost
    dp[0] = cost[0];

    // Find answer for each position i
    for(let i = 1; i < n; i++)
    {

        // First Element
        if (i == 1)
            dp[i] = cost[i] + dp[i - 1];

        // Second Element
        if (i == 2)
            dp[i] = cost[i] + Math.min(dp[i - 1],
                                   x + dp[i - 2]);

        // For remaining element
        if (i >= 3)

            // Consider min cost for
            // skipping
            dp[i] = cost[i] + Math.min(dp[i - 1],
                          Math.min(x + dp[i - 2],
                               2 * x + dp[i - 3]));
    }

    // Last index represents the
    // minimum total cost
    document.write(dp[n - 1]);
}

// Driver code

// Given X
let X = 4;

// Given array cost[]
let cost = [ 6, 3, 9, 2, 1, 3 ];

let N = cost.length;

// Function Call
minimumCost(cost, N, X);

// This code is contributed by splevel62

</script>
```

**Output:** 

```
19
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)