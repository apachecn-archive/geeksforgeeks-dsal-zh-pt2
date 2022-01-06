# 将在矩阵上放置尺寸为 2 * 1 的瓷砖的成本降至最低

> 原文:[https://www . geeksforgeeks . org/最小化放置尺寸为 2-1 的瓷砖的成本/矩阵/](https://www.geeksforgeeks.org/minimize-cost-of-placing-tiles-of-dimensions-2-1-over-a-matrix/)

给定维度为 **2*N** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**M【】【】**，任务是找到用维度为 **2 * 1** 的图块填充矩阵的最小成本，使得填充图块的成本等于放置图块的单元格中的矩阵元素的**总和**，折扣等于这些单元格中的矩阵元素之间的**绝对差值**。

**示例:**

> **输入:** M[][] = {{1，4，3，5}，{2，5，4，3}}，N = 4
> **输出:** 18
> **解释:**
> 可能的解决方案之一是，
> 将第一个平铺块水平放置在(1，1)和(1，2)处。成本= (1+4) = 5。折扣=(4–1)= 3。
> 将第二个瓷砖水平放置在(1，3)和(1，4)处。成本= (3+5) = 8。折扣=(5–3)= 2。
> 将第三块瓷砖水平放置在(2，1)和(2，2)处。成本= (2 + 5) = 7。折扣(5-2)= 3。
> 将第四块瓷砖水平放置在(2，3)和(2，4)处。成本= (4 + 3) = 7。折扣=(4–3)= 1。
> 因此，总成本= (5 + 8 + 7 + 7) = 27。总折扣= (3 + 2 + 3 + 1) = 9。因此，实际成本=(27–9)= 18，这是放置所有瓷砖的最小成本。
> 
> **输入:** M[][] = {{7，5，1，3}，{8，6，0，2}}，N = 4
> **输出:** 20

**方法:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)方法解决问题，因为问题类似于[平铺问题](https://www.geeksforgeeks.org/tiling-problem/)。给定的问题可以基于以下观察来解决:

*   将图块放置在矩阵中的总成本等于矩阵中元素的[总和。](https://www.geeksforgeeks.org/find-the-sum-of-elements-of-the-matrix-generated-by-the-given-rules/)因此，通过最大化折扣，实际成本将最小化。
*   在这里， **dp[i]** 存储在矩阵中放置 **2×1** 瓷砖直到 **i <sup>第</sup>列**后的最小成本。
*   从一种状态到另一种状态的转换将通过将当前图块垂直放置在第 **i** 列或水平放置在第 **i** 和**(I–1)**列的两行中来实现。

> **dp[i]=最大值(DP[I-1]+ABS(m[0]–1]、DP[I-2]+ABS(m[0][I-1]–m[0]、I)+ABS(m[1]–1]–m[1])**

按照以下步骤解决问题:

*   初始化一个变量，比如**原始成本，**在没有折扣的情况下将总成本存储在瓷砖中。
*   初始化一个 [数组](https://www.geeksforgeeks.org/introduction-to-arrays/) ，说 **dp[]，**用于存储最大折扣费用在放置瓷砖直到 **i <sup>th</sup>** 列。
*   找到[网格中所有元素的总和](https://www.geeksforgeeks.org/maximum-sum-2-x-n-grid-no-two-elements-adjacent/)并存储在**原始成本**中。
*   遍历各列并更新**DP[I]= max(DP[I–1]+ABS(M[0][I]–M[1][I])，DP[I–2]+ABS(M[0][I–1]–M[0][I])+ABS(M[1][I–1]–M[1][I])**。
*   完成上述步骤后，打印**(原始成本–DP[N–1])**的值作为结果。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
// in placing N tiles in a grid M[][]
void tile_placing(vector<vector<int> > grid, int N)
{
    // Stores the minimum profit
    // after placing i tiles
    int dp[N + 5] = { 0 };
    int orig_cost = 0;

    // Traverse the grid[][]
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < N; j++) {

            // Update the orig_cost
            orig_cost += grid[i][j];
        }
    }

    dp[0] = 0;
    dp[1] = abs(grid[0][0] - grid[1][0]);

    // Traverse over the range [2, N]
    for (int i = 2; i <= N; i++) {

        // Place tiles horizentally
        // or vertically
        dp[i] = max(
            dp[i - 1]
                + abs(grid[0][i - 1] - grid[1][i - 1]),
            dp[i - 2] + abs(grid[0][i - 2] - grid[0][i - 1])
                + abs(grid[1][i - 2] - grid[1][i - 1]));
    }

    // Print the answer
    cout << orig_cost - dp[N];
}

// Driver Code
int32_t main()
{
    vector<vector<int> > M
        = { { 7, 5, 1, 3 }, { 8, 6, 0, 2 } };
    int N = M[0].size();

    tile_placing(M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

  // Function to find the minimum cost
  // in placing N tiles in a grid M[][]
  static void tile_placing(int[][] grid, int N)
  {
    // Stores the minimum profit
    // after placing i tiles
    int dp[] = new int[N + 5];
    Arrays.fill(dp, 0);
    int orig_cost = 0;

    // Traverse the grid[][]
    for (int i = 0; i < 2; i++) {
      for (int j = 0; j < N; j++) {

        // Update the orig_cost
        orig_cost += grid[i][j];
      }
    }

    dp[0] = 0;
    dp[1] = Math.abs(grid[0][0] - grid[1][0]);

    // Traverse over the range [2, N]
    for (int i = 2; i <= N; i++) {

      // Place tiles horizentally
      // or vertically
      dp[i] = Math.max(
        dp[i - 1]
        + Math.abs(grid[0][i - 1] - grid[1][i - 1]),
        dp[i - 2] + Math.abs(grid[0][i - 2] - grid[0][i - 1])
        + Math.abs(grid[1][i - 2] - grid[1][i - 1]));
    }

    // Print the answer
    System.out.println(orig_cost - dp[N]);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[][] M
      = { { 7, 5, 1, 3 }, { 8, 6, 0, 2 } };
    int N = M[0].length;

    tile_placing(M, N);
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum cost
# in placing N tiles in a grid M[][]
def tile_placing(grid, N) :

    # Stores the minimum profit
    # after placing i tiles
    dp = [0]*(N + 5);
    orig_cost = 0;

    # Traverse the grid[][]
    for i in range(2) :
        for j in range(N) :

            # Update the orig_cost
            orig_cost += grid[i][j];
    dp[0] = 0;
    dp[1] = abs(grid[0][0] - grid[1][0]);

    # Traverse over the range [2, N]
    for i in range(2, N + 1) :

        # Place tiles horizentally
        # or vertically
        dp[i] = max(
            dp[i - 1]
                + abs(grid[0][i - 1] - grid[1][i - 1]),
            dp[i - 2] + abs(grid[0][i - 2] - grid[0][i - 1])
                + abs(grid[1][i - 2] - grid[1][i - 1]));

    # Print the answer
    print(orig_cost - dp[N],end = "");

# Driver Code
if __name__ == "__main__" :

    M = [ [ 7, 5, 1, 3 ], [ 8, 6, 0, 2 ] ];
    N = len(M[0]);

    tile_placing(M, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find the minimum cost
  // in placing N tiles in a grid M[][]
  static void tile_placing(int[,] grid, int N)
  {

    // Stores the minimum profit
    // after placing i tiles
    int[] dp = new int[N + 5];
    for (int i = 0; i < N + 5; i++) {
        dp[i] = 0;
    }

    int orig_cost = 0;

    // Traverse the grid[][]
    for (int i = 0; i < 2; i++) {
      for (int j = 0; j < N; j++) {

        // Update the orig_cost
        orig_cost += grid[i, j];
      }
    }

    dp[0] = 0;
    dp[1] = Math.Abs(grid[0, 0] - grid[1, 0]);

    // Traverse over the range [2, N]
    for (int i = 2; i <= N; i++) {

      // Place tiles horizentally
      // or vertically
      dp[i] = Math.Max(
        dp[i - 1]
        + Math.Abs(grid[0, i - 1] - grid[1, i - 1]),
        dp[i - 2] + Math.Abs(grid[0, i - 2] - grid[0, i - 1])
        + Math.Abs(grid[1, i - 2] - grid[1, i - 1]));
    }

    // Print the answer
    Console.Write(orig_cost - dp[N]);
  }

// Driver Code
public static void Main()
{
    int[,] M
      = { { 7, 5, 1, 3 }, { 8, 6, 0, 2 } };
    int N = 4;

    tile_placing(M, N);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to find the minimum cost
    // in placing N tiles in a grid M[][]
    function tile_placing(grid, N)
    {
      // Stores the minimum profit
      // after placing i tiles
      let dp = new Array(N + 5);
      dp.fill(0);
      let orig_cost = 0;

      // Traverse the grid[][]
      for (let i = 0; i < 2; i++) {
        for (let j = 0; j < N; j++) {

          // Update the orig_cost
          orig_cost += grid[i][j];
        }
      }

      dp[0] = 0;
      dp[1] = Math.abs(grid[0][0] - grid[1][0]);

      // Traverse over the range [2, N]
      for (let i = 2; i <= N; i++) {

        // Place tiles horizentally
        // or vertically
        dp[i] = Math.max(
          dp[i - 1]
          + Math.abs(grid[0][i - 1] - grid[1][i - 1]),
          dp[i - 2] + Math.abs(grid[0][i - 2] - grid[0][i - 1])
          + Math.abs(grid[1][i - 2] - grid[1][i - 1]));
      }

      // Print the answer
      document.write((orig_cost - dp[N]) + "</br>");
    }

    let M = [ [ 7, 5, 1, 3 ], [ 8, 6, 0, 2 ] ];
    let N = M[0].length;

    tile_placing(M, N);

</script>
```

**Output:** 

```
20
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)