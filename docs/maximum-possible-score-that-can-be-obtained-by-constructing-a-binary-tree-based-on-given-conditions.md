# 基于给定条件构建二叉树可以获得的最大可能得分

> 原文:[https://www . geeksforgeeks . org/通过基于给定条件构建二叉树可以获得的最大可能分数/](https://www.geeksforgeeks.org/maximum-possible-score-that-can-be-obtained-by-constructing-a-binary-tree-based-on-given-conditions/)

给定一个由**(N–1)**个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，每个基于值**arr[I]**(***)1 的**索引*是具有度 **i** 的节点的得分。任务是确定 **N** 个节点中任意一个可以构建的树的最大得分。

**示例:**

> **输入:** arr[] = {1，3，0}
> **输出:** 8
> **解释:**
> 构造树的一种可能方式是:
> 1
> /\
> 2 3
> \
> 4
> 节点 1 有度 2。因此，它的得分是 3。
> 节点 2 为 1 级。因此，它的得分是 1。
> 节点 3 有 2 度。因此，它的得分是 3。
> 节点 4 为 1 级。因此，它的得分是 1。
> 所以总分= 3 + 1 + 3 + 1 = 8。
> 
> **输入:** arr[] = {0，1}
> **输出:** 1
> **解释:**
> 构造树的一种可能方式是:
> 1
> / \
> 2 3
> 节点 1 有度 2。因此，它的得分是 1。
> 节点 2 为 1 级。因此，其得分为 0。
> 节点 3 为 1 级。因此，其得分为 0。
> 因此，总分= 1 + 0 + 0 = 1。

**天真方法:**最简单的方法是生成构建具有 **N** 个节点的树的所有可能组合，并找到每个节点的总得分。然后，打印获得的所有分数的最大值。

***时间复杂度:** (N！)其中 N 是树中的节点数。*
***辅助空间:** O(N)*

**高效方法:**为了优化上述方法，想法是通过创建一个 **dp[][]** 表来使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)，其中 **dp[i][j]** 使用节点的度之和为 **j** 的 **i** 节点来表示最大得分。按照以下步骤解决问题:

*   初始化一个数组**DP[N+1][2 *(N–1)+1]**，其中 **N** 是节点数，**(2 *(N–1))**是度的最大和。
*   用 **0** 初始化 **dp[0][0]** 。
*   迭代两个嵌套循环，一个在范围**【1，N】**上，另一个从 **1** 直到可能的最大得分**2 *(N–1)**，对于范围**【1，N】**[中的每个得分 **s** ，遍历给定的得分数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr[]**，并将**DP【I】【s】**更新为:

> dp[i][s] = max(dp[i][s]，分数[j-1] dp[i-1][s-j])
> 其中 **dp[i][s]** 代表具有 **i** 节点的树的最大分数，度数之和为 **s** 。

*   对于具有 **N** 顶点和**(N–1)**边的树，所有度数的总和应为**2 *(N–1)**。因此，打印**DP[N][2 *(N–1)]**的值作为具有 **N** 节点的树的最大得分。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum score
// for one possible tree having N nodes
// N - 1 Edges
int maxScore(vector<int>& arr)
{
    int N = arr.size();

    // Number of nodes
    N++;

    // Initialize dp[][]
    vector<vector<int> >
        dp(N + 1, vector<int>(2 * N,
                              -100000));

    // Score with 0 vertices is 0
    dp[0][0] = 0;

    // Traverse the nodes from 1 to N
    for (int i = 1; i <= N; i++) {

        // Find maximum scores for
        // each sum
        for (int s = 1;
             s <= 2 * (N - 1); s++) {

            // Iterate over degree of
            // new node
            for (int j = 1; j <= N - 1
                            and j <= s;
                 j++) {

                // Update the current
                // state
                dp[i][s]
                    = max(dp[i][s],
                          arr[j - 1]
                              + dp[i - 1][s - j]);
            }
        }
    }

    // Return maximum score for N node
    // tree having 2(N - 1) sum of degree
    return dp[N][2 * (N - 1)];
}

// Driver Code
int main()
{
    // Given array of scores
    vector<int> arr = { 1, 3, 0 };

    // Function Call
    cout << maxScore(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum score
// for one possible tree having N nodes
// N - 1 Edges
static int maxScore(int[] arr)
{
    int N = arr.length;

    // Number of nodes
    N++;

    // Initialize dp[][]
    int [][] dp = new int[N + 1][2 * (N - 1) + 1];

    // Score with 0 vertices is 0
    dp[0][0] = 0;

    // Traverse the nodes from 1 to N
    for(int i = 1; i <= N; i++)
    {

        // Find maximum scores for
        // each sum
        for(int s = 1; s <= 2 * (N - 1); s++)
        {

            // Iterate over degree of
            // new node
            for(int j = 1; j <= N - 1 && j <= s; j++)
            {

                // Update the current
                // state
                dp[i][s] = Math.max(dp[i][s],
                                   arr[j - 1] +
                                    dp[i - 1][s - j]);
            }
        }
    }

    // Return maximum score for N node
    // tree having 2(N - 1) sum of degree
    return dp[N][2 * (N - 1)] - 1;
}

// Driver Code
public static void main(String[] args)
{

    // Given array of scores
    int [] arr = { 1, 3, 0 };

    // Function Call
    System.out.print(maxScore(arr));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum score
# for one possible tree having N nodes
# N - 1 Edges
def maxScore(arr):

    N = len(arr)

    # Number of nodes
    N += 1

    # Initialize dp[][]
    dp = [[-100000 for i in range(2 * N)]
                   for i in range(N + 1)]

    # Score with 0 vertices is 0
    dp[0][0] = 0

    # Traverse the nodes from 1 to N
    for i in range(1, N + 1):

        # Find maximum scores for
        # each sum
        for s in range(1, 2 * (N - 1) + 1):

            # Iterate over degree of
            # new node
            j = 1
            while j <= N - 1 and j <= s:

                # Update the current
                # state
                dp[i][s] = max(dp[i][s], arr[j - 1] +
                               dp[i - 1][s - j])
                j += 1

    # Return maximum score for N node
    # tree having 2(N - 1) sum of degree
    return dp[N][2 * (N - 1)]

# Driver Code
if __name__ == '__main__':

    # Given array of scores
    arr = [ 1, 3, 0 ]

    # Function Call
    print(maxScore(arr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find the
// maximum score for one
// possible tree having N
// nodes N - 1 Edges
static int maxScore(int[] arr)
{
  int N = arr.Length;

  // Number of nodes
  N++;

  // Initialize [,]dp
  int [,] dp = new int[N + 1,
                       2 * (N -
                       1) + 1];

  // Score with 0 vertices
  // is 0
  dp[0, 0] = 0;

  // Traverse the nodes from
  // 1 to N
  for(int i = 1; i <= N; i++)
  {
    // Find maximum scores for
    // each sum
    for(int s = 1;
            s <= 2 * (N - 1); s++)
    {
      // Iterate over degree of
      // new node
      for(int j = 1;
              j <= N - 1 && j <= s; j++)
      {
        // Update the current
        // state
        dp[i, s] = Math.Max(dp[i, s],
                            arr[j - 1] +
                            dp[i - 1,
                               s - j]);
      }
    }
  }

  // Return maximum score for
  // N node tree having 2(N - 1)
  // sum of degree
  return dp[N, 2 * (N -
            1)] - 1;
}

// Driver Code
public static void Main(String[] args)
{   
  // Given array of scores
  int [] arr = {1, 3, 0};

  // Function Call
  Console.Write(maxScore(arr));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum score
// for one possible tree having N nodes
// N - 1 Edges
function maxScore(arr)
{
    var N = arr.length;

    // Number of nodes
    N++;

    // Initialize dp[][]
    var dp = Array.from(Array(N+1), ()=> Array(2*N).fill(-10000000));

    // Score with 0 vertices is 0
    dp[0][0] = 0;

    // Traverse the nodes from 1 to N
    for (var i = 1; i <= N; i++) {

        // Find maximum scores for
        // each sum
        for (var s = 1;
             s <= 2 * (N - 1); s++) {

            // Iterate over degree of
            // new node
            for (var j = 1; j <= N - 1
                            && j <= s;
                 j++) {

                // Update the current
                // state
                dp[i][s]
                    = Math.max(dp[i][s],
                          arr[j - 1]
                              + dp[i - 1][s - j]);
            }
        }
    }

    // Return maximum score for N node
    // tree having 2(N - 1) sum of degree
    return dp[N][2 * (N - 1)];
}

// Driver Code

// Given array of scores
var arr = [1, 3, 0];

// Function Call
document.write( maxScore(arr));

</script>
```

**Output**

```
8
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*