# 服务器负载的最小绝对差

> 原文:[https://www . geesforgeks . org/最小绝对服务器负载差/](https://www.geeksforgeeks.org/minimum-absolute-difference-of-server-loads/)

有一些流程需要执行。进程导致运行它的服务器的负载量，用一个整数表示。服务器上造成的总负载是在该服务器上运行的所有进程的负载总和。您可以使用两台服务器，上面可以运行上述进程。您的目标是在这两个服务器之间分配给定的进程，以使它们的负载的绝对差异最小化。
给定一个由 **A[]** 组成的 **N** 整数数组，该数组表示由连续进程引起的负载，任务是打印服务器负载的最小绝对差。
**示例:**

> **输入:** A[] = {1，2，3，4，5}
> **输出:** 1
> **解释:**
> 将负载为{1，2，4}的进程分布在第一台服务器上，负载为{3，5}的进程分布在第二台服务器上，这样它们的总负载将分别为 7 和 8。
> 它们的载荷之差将等于 1。
> 
> **输入:** A[] = {10，10，9，9，2 }
> T3】输出: 0

**天真方法:**解决问题最简单的方法是生成负载分布的所有可能性，并在两个服务器的所有可能负载组合中找到可能的最小差异。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效的方法:**这个问题可以被可视化为 [0/1 背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)问题的一个变种，其中给定了 2 个服务器，我们必须尽可能平均地分配负载。所以可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。以下是步骤:

*   计算**所需载荷**，等于**(所有载荷之和/ 2)** ，因为载荷需要尽可能平均分配。
*   创建一个记忆表 **DP[][]** ，以考虑范围**【1，所需 _ 负载】**内所有可能的服务器负载。
*   状态 **DP[i][j]** 存储**j–负载**的最大值，考虑到第 i <sup>个</sup>元素。因此，考虑到 **l <sub>i</sub>** (第 **i <sup>第</sup>行**中的载荷)，可将其填入所有具有**载荷值> l <sub>i</sub>** 的列中。
*   现在出现了两种可能性，要么在给定的列中填充 **l <sub>i</sub>** 要么不填充。
*   现在，取上述两种可能性的最大值，即

> DP[i][j] =最大值(DP[I–1][j]，DP[I–1][j–l 0]I+l<sub>I</sub>

*   最后， **DP[n][required_load]** 将包含服务器 1 上尽可能平衡的负载。

下面是上述方法的实现:

## C++14

```
// C++14 program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function which returns the minimum
// difference of loads
int minServerLoads(int n, vector<int>& servers)
{

    // Compute the overall server load
    int totalLoad = 0;
    for(int i : servers) totalLoad += i;

    int requiredLoad = totalLoad / 2;

    // Stores the results of subproblems
    vector<vector<int>> dp(n + 1,
    vector<int>(requiredLoad + 1, 0));

    // Fill the partition table
    // in bottom up manner
    for(int i = 1; i < n + 1; i++)
    {
        for(int j = 1; j < requiredLoad + 1; j++)
        {

            // If i-th server is included
            if (servers[i - 1] > j)
                dp[i][j] = dp[i - 1][j];

            // If i-th server is excluded
            else
                dp[i][j] = max(dp[i - 1][j],
                          servers[i - 1] +
                        dp[i - 1][j - servers[i - 1]]);
        }
    }

    // Server A load: total_sum-ans
    // Server B load: ans
    // Diff: abs(total_sum-2 * ans)
    return totalLoad - 2 * dp[n][requiredLoad];
}

// Driver Code
int main()
{
    int N = 5;

    vector<int> servers = { 1, 2, 3, 4, 5 };

    // Function call
    cout << (minServerLoads(N, servers));
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG {

    // Function which returns the minimum
    // difference of loads
    static int minServerLoads(int n, int[] servers)
    {
        // Compute the overall server load
        int totalLoad = 0;
        for (int i = 0; i < servers.length; i++)
            totalLoad += servers[i];
        int requiredLoad = totalLoad / 2;

        // Stores the results of subproblems
        int dp[][] = new int[n + 1][requiredLoad + 1];

        // Fill the partition table
        // in bottom up manner
        for (int i = 1; i < n + 1; i++)
        {
            for (int j = 1; j < requiredLoad + 1; j++)
            {
                // If i-th server is included
                if (servers[i - 1] > j)
                    dp[i][j] = dp[i - 1][j];

                // If i-th server is excluded
                else
                    dp[i][j] = Math.max(dp[i - 1][j],
                                        servers[i - 1] +
                                        dp[i - 1][j - servers[i - 1]]);
            }
        }

        // Server A load: total_sum-ans
        // Server B load: ans
        // Diff: abs(total_sum-2 * ans)
        return totalLoad - 2 * dp[n][requiredLoad];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 5;
        int servers[] = {1, 2, 3, 4, 5};

        // Function call
        System.out.print(minServerLoads(N, servers));
    }
}

// This code is contributed by Chitranayal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function which returns the minimum
# difference of loads
def minServerLoads(n, servers):

    # Compute the overall server load
    totalLoad = sum(servers)

    requiredLoad = totalLoad // 2

    # Stores the results of subproblems
    dp = [[0 for col in range(requiredLoad + 1)]
          for row in range(n + 1)]

    # Fill the partition table
    # in bottom up manner
    for i in range(1, n + 1):
        for j in range(1, requiredLoad + 1):

            # If i-th server is included
            if servers[i-1] > j:
                dp[i][j] = dp[i-1][j]

            # If i-th server is excluded
            else:
                dp[i][j] = max(dp[i-1][j],
                           servers[i-1] +
                           dp[i-1][j-servers[i-1]])

    # Server A load: total_sum-ans
    # Server B load: ans
    # Diff: abs(total_sum-2 * ans)
    return totalLoad - 2 * dp[n][requiredLoad]

# Driver Code

N = 5;

servers = [1, 2, 3, 4, 5]

# Function Call
print(minServerLoads(N, servers))
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function which returns the minimum
// difference of loads
static int minServerLoads(int n, int[] servers)
{

    // Compute the overall server load
    int totalLoad = 0;
    for(int i = 0; i < servers.Length; i++)
        totalLoad += servers[i];

    int requiredLoad = totalLoad / 2;

    // Stores the results of subproblems
    int [,]dp = new int[n + 1, requiredLoad + 1];

    // Fill the partition table
    // in bottom up manner
    for(int i = 1; i < n + 1; i++)
    {
        for(int j = 1; j < requiredLoad + 1; j++)
        {

            // If i-th server is included
            if (servers[i - 1] > j)
                dp[i, j] = dp[i - 1, j];

            // If i-th server is excluded
            else
                dp[i, j] = Math.Max(dp[i - 1, j],
                               servers[i - 1] +
                                    dp[i - 1, j -
                               servers[i - 1]]);
        }
    }

    // Server A load: total_sum-ans
    // Server B load: ans
    // Diff: abs(total_sum-2 * ans)
    return totalLoad - 2 * dp[n, requiredLoad];
}

// Driver Code
public static void Main(string[] args)
{
    int N = 5;
    int []servers = { 1, 2, 3, 4, 5 };

    // Function call
    Console.Write(minServerLoads(N, servers));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function which returns the minimum
// difference of loads
function minServerLoads(n, servers)
{

    // Compute the overall server load
    var totalLoad = 0;

    servers.forEach(i => {
        totalLoad+=i;
    });

    var requiredLoad = parseInt(totalLoad / 2);

    // Stores the results of subproblems
    var dp =
    Array.from(Array(n+1), ()=> Array(requiredLoad+1).fill(0));

    // Fill the partition table
    // in bottom up manner
    for(var i = 1; i < n + 1; i++)
    {
        for(var j = 1; j < requiredLoad + 1; j++)
        {

            // If i-th server is included
            if (servers[i - 1] > j)
                dp[i][j] = dp[i - 1][j];

            // If i-th server is excluded
            else
                dp[i][j] = Math.max(dp[i - 1][j],
                          servers[i - 1] +
                        dp[i - 1][j - servers[i - 1]]);
        }
    }

    // Server A load: total_sum-ans
    // Server B load: ans
    // Diff: abs(total_sum-2 * ans)
    return totalLoad - 2 * dp[n][requiredLoad];
}

// Driver Code
var N = 5;
var servers = [1, 2, 3, 4, 5];

// Function call
document.write(minServerLoads(N, servers));

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N*S)其中 N 为服务器数量，S 为**加载所有服务器的总和。*
***辅助空间:** O(N*S)*