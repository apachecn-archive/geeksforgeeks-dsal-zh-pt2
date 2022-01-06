# 扩展背包问题

> 原文:[https://www.geeksforgeeks.org/extended-knapsack-problem/](https://www.geeksforgeeks.org/extended-knapsack-problem/)

给定 **N** 个项目，每个项目都有一个给定的权重**C<sub>I</sub>T5】和一个利润值**P<sub>I</sub>T9】，任务是通过选择最大 **K** 个项目相加得到最大权重 **W** 使利润最大化。****

**示例:**

> **输入:** N = 5，P[] = {2，7，1，5，3}，C[] = {2，5，2，3，4}，W = 8，K = 2。
> **输出:** 12
> **说明:**
> 这里，最大可能的利润是我们取 2 个项目时:项目 2 (P[1] = 7 和 C[1] = 5)和项目 4 (P[3] = 5 和 C[3] = 3)。
> 因此，最大利润= 7 + 5 = 12
> **输入:** N = 5，P[] = {2，7，1，5，3}，C[] = {2，5，2，3，4}，W = 1，K = 2
> **输出:** 0
> **说明:**所有权重均大于 1。因此，没有项目可以挑选。

**方法:**[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)方法优于一般递归方法。让我们首先验证 DP 的条件是否仍然满足。

1.  **重叠子问题:**尝试递归求解时，先增加 1 项，解集为(1)、(2)、……(n)。在第二次迭代中，我们有(1，2)等等，其中(1)和(2)被重新计算。因此会有重叠的解决方案。
2.  **最优子结构:**总体来说，每个项目只有两个选择，要么可以包含在解中，要么拒绝。对于 z 元素的特定子集，第(z+1) <sup>元素的解可以具有对应于 z 元素的解，或者如果不超过背包约束，则可以添加第(z+1) <sup>元素。无论哪种方式，都满足最佳子结构特性。</sup></sup>

让我们推导出循环。让我们考虑一个三维表格 **dp[N][W][K]** ，其中 **N** 是元素数量， **W** 是最大重量容量， **K** 是背包中允许的最大物品数量。让我们定义一个状态 **dp[i][j][k]** ，其中 **i** 表示我们正在考虑**I<sup>th</sup>T15】元素， **j** 表示当前填充的重量， **k** 表示到目前为止填充的项目数。
对于每个状态 **dp[i][j][k]** ，利润要么是前一状态的利润(当不包括当前状态时)，要么是当前项目添加到前一状态的利润(当选择当前项目时)。因此，循环关系是:**

> dp[i][j][k] =最大值(dp[i-1][j][k]，dp[i-1][j-W[i-1]][k-1] + P[i])

下面是上述方法的实现:

## C++

```
// C++ code for the extended
// Knapsack Approach
#include <bits/stdc++.h>
using namespace std;

// To store the dp values
vector<vector<vector<int> > > dp;

int maxProfit(int profit[], int weight[], int n, int max_W,
              int max_E)
{

    // for each element given
    for (int i = 1; i <= n; i++) {

        // For each possible
        // weight value
        for (int j = 1; j <= max_W; j++) {

            // For each case where
            // the total elements are
            // less than the constraint
            for (int k = 1; k <= max_E; k++) {

                // To ensure that we dont
                // go out of the array
                if (j >= weight[i - 1]) {

                    dp[i][j][k] = max(
                        dp[i - 1][j][k],
                        dp[i - 1][j - weight[i - 1]][k - 1]
                            + profit[i - 1]);
                }
                else {
                    dp[i][j][k] = dp[i - 1][j][k];
                }
            }
        }
    }

    return dp[n][max_W][max_E];
}

// Driver Code
int main()
{
    int n = 5;
    int profit[] = { 2, 7, 1, 5, 3 };
    int weight[] = { 2, 5, 2, 3, 4 };
    int max_weight = 8;
    int max_element = 2;

    dp = vector<vector<vector<int> > >(
        n + 1, vector<vector<int> >(
                   max_weight + 1,
                   vector<int>(max_element + 1, 0)));
    cout << maxProfit(profit, weight, n, max_weight,
                      max_element)
         << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the extended
// Knapsack Approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// To store the dp values
static int[][][] dp = new int[100][100][100];

static int maxProfit(int profit[],
                     int weight[],
                     int n, int max_W,
                     int max_E)
{

    // for each element given
    for(int i = 1; i <= n; i++)
    {

        // For each possible
        // weight value
        for(int j = 1; j <= max_W; j++)
        {

            // For each case where
            // the total elements are
            // less than the constraint
            for(int k = 1; k <= max_E; k++)
            {

                // To ensure that we dont
                // go out of the array
                if (j >= weight[i - 1])
                {
                    dp[i][j][k] = Math.max(dp[i - 1][j][k],
                                           dp[i - 1][j -
                                       weight[i - 1]][k - 1] +
                                       profit[i - 1]);
                }
                else
                {
                    dp[i][j][k] = dp[i - 1][j][k];
                }
            }
        }
    }

    return dp[n][max_W][max_E];
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    int profit[] = { 2, 7, 1, 5, 3 };
    int weight[] = { 2, 5, 2, 3, 4 };
    int max_weight = 8;
    int max_element = 2;

    System.out.println(maxProfit(profit,
                                 weight, n,
                                 max_weight,
                                 max_element));  
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// Javascript code for the extended
// Knapsack Approach

// To store the dp values
var dp = Array.from(Array(100), ()=>Array(100));
for(var i =0; i<100; i++)
        for(var j =0; j<100; j++)
            dp[i][j] = new Array(100).fill(0);

function maxProfit(profit,weight, n, max_W, max_E)
{

    // for each element given
    for (var i = 1; i <= n; i++)
    {

        // For each possible
        // weight value
        for (var j = 1; j <= max_W; j++)
        {

            // For each case where
            // the total elements are
            // less than the constraint
            for (var k = 1; k <= max_E; k++)
            {

                // To ensure that we dont
                // go out of the array
                if (j >= weight[i-1])
                {

                    dp[i][j][k]
                        = Math.max(dp[i - 1][j][k],
                                dp[i - 1][j -
                          weight[i-1]][k - 1]+
                                  profit[i-1]);
                }
                else
                {
                    dp[i][j][k]
                        = dp[i - 1][j][k];
                }
            }
        }
    }

    return dp[n][max_W][max_E];
}

// Driver Code
var n = 5;
var profit = [2, 7, 1, 5, 3 ];
var weight = [2, 5, 2, 3, 4 ];
var max_weight = 8;
var max_element = 2;
document.write( maxProfit(profit,
              weight, n,
              max_weight,
              max_element)
     + "<br>");

</script>
```

## 蟒蛇 3

```
# Python3 code for the extended
# Knapsack Approach

# To store the dp values
dp=[]

def maxProfit(profit, weight, n, max_W,
              max_E):

    # for each element given
    for i in range(1,n+1) :

        # For each possible
        # weight value
        for j in range(1,max_W+1) :

            # For each case where
            # the total elements are
            # less than the constra
            for k in range(1, max_E+1) :

                # To ensure that we dont
                # go out of the array
                if (j >= weight[i - 1]) :

                    dp[i][j][k] = max(
                        dp[i - 1][j][k],
                        dp[i - 1][j - weight[i - 1]][k - 1]
                            + profit[i - 1])

                else :
                    dp[i][j][k] = dp[i - 1][j][k]

    return dp[n][max_W][max_E]

# Driver Code
if __name__ == '__main__':
    n = 5
    profit = [2, 7, 1, 5, 3 ]
    weight = [ 2, 5, 2, 3, 4 ]
    max_weight = 8
    max_element = 2

    dp = [[[0 for j in range(max_element + 1)]for i in range(max_weight + 1)] for k in range(n+1)]
    print(maxProfit(profit, weight, n, max_weight,
                      max_element))
```

**Output:** 

```
12
```

**时间复杂度:***O(N * W * K)*
T5】辅助空间: *O(N * W * K)*