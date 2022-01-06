# 矩阵中从左上角到右下角的最大和路径

> 原文:[https://www . geesforgeks . org/矩阵中最大和路径从左上方到右下方/](https://www.geeksforgeeks.org/maximum-sum-path-in-a-matrix-from-top-left-to-bottom-right/)

给定尺寸为 **N * M** 的矩阵 **mat[][]** ，任务是找到从给定矩阵的**左上角单元格** (0，0)到**右下角单元格**(N–1，M–1)的路径，使得路径中的元素总和最大。从矩阵的任何单元(I，j)允许的唯一移动是 **(i + 1，j)** 或 **(i，j + 1)** 。

**示例:**

> **输入:** mat[][] = {{3，7}，{9，8}}
> **输出:** 20
> **解释:**
> 最大和的路径为 3 = > 9 = > 8 为 20。
> 
> **输入:** mat[][] = {{1，2}，{3，5}}
> **输出:** 9
> **解释:**
> 最大和的路径为 1 = > 3 = > 5 为 9

**方法 1(自下而上):**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决这个问题。关键观察是细胞**网格【I】【j】**只能从**网格【I–1】【j】**或**网格【I】【j–1】**到达。因此，这个问题的递推关系由下式给出:

> sum(i，j)= max(sum(i–1，j)，sum(I，j–1))+grid[I][j]

1.  初始化尺寸 **N * M** 的辅助矩阵**和[][]** 。
2.  迭代矩阵元素，并使用上面形成的递归关系更新辅助矩阵 **sum[][]** 的每个单元。
3.  完成上述步骤后，值**sum【N】【M】**将包含从给定矩阵的**左上角**到**右下角**的路径的最大可能和。打印那个总数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// path in the grid
int MaximumPath(vector<vector<int> >& grid)
{
    // Dimensions of grid[][]
    int N = grid.size();
    int M = grid[0].size();

    // Stores maximum sum at each cell
    // sum[i][j] from cell sum[0][0]
    vector<vector<int> > sum;
    sum.resize(N + 1,
               vector<int>(M + 1));

    // Iterate to compute the maximum
    // sum path in the grid
    for (int i = 1; i <= N; i++) {

        for (int j = 1; j <= M; j++) {

            // Update the maximum path sum
            sum[i][j] = max(sum[i - 1][j],
                            sum[i][j - 1])
                        + grid[i - 1][j - 1];
        }
    }

    // Return the maximum sum
    return sum[N][M];
}

// Driver Code
int main()
{
    vector<vector<int> > grid
        = { { 1, 2 }, { 3, 5 } };

    cout << MaximumPath(grid);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
//the above approach
import java.util.*;
class GFG{

// Function to find the maximum sum
// path in the grid
static int MaximumPath(int [][]grid)
{
    // Dimensions of grid[][]
    int N = grid.length;
    int M = grid[0].length;

    // Stores maximum sum at each cell
    // sum[i][j] from cell sum[0][0]
    int [][]sum = new int[N + 1][M + 1];

    // Iterate to compute the maximum
    // sum path in the grid
    for (int i = 1; i <= N; i++)
    {
        for (int j = 1; j <= M; j++)
        {
            // Update the maximum path sum
            sum[i][j] = Math.max(sum[i - 1][j],
                                 sum[i][j - 1]) +
                                 grid[i - 1][j - 1];
        }
    }

    // Return the maximum sum
    return sum[N][M];
}

// Driver Code
public static void main(String[] args)
{
  int [][]grid = {{1, 2}, {3, 5}};
  System.out.print(MaximumPath(grid));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum sum
# path in the grid
def MaximumPath(grid):

    # Dimensions of grid[][]
    N = len(grid)
    M = len(grid[0])

    # Stores maximum sum at each cell
    # sum[i][j] from cell sum[0][0]
    sum = [[0 for i in range(M + 1)]
              for i in range(N + 1)]

    # Iterate to compute the maximum
    # sum path in the grid
    for i in range(1, N + 1):
        for j in range(1, M + 1):

            # Update the maximum path sum
            sum[i][j] = (max(sum[i - 1][j],
                             sum[i][j - 1]) +
                        grid[i - 1][j - 1])

    # Return the maximum sum
    return sum[N][M]

# Driver Code
if __name__ == '__main__':

    grid = [ [ 1, 2 ], [ 3, 5 ] ]

    print(MaximumPath(grid))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum sum
// path in the grid
static int MaximumPath(int [,]grid)
{

    // Dimensions of grid[,]
    int N = grid.GetLength(0);
    int M = grid.GetLength(1);

    // Stores maximum sum at each cell
    // sum[i,j] from cell sum[0,0]
    int [,]sum = new int[N + 1, M + 1];

    // Iterate to compute the maximum
    // sum path in the grid
    for(int i = 1; i <= N; i++)
    {
        for(int j = 1; j <= M; j++)
        {
            // Update the maximum path sum
            sum[i, j] = Math.Max(sum[i - 1, j],
                                 sum[i, j - 1]) +
                                grid[i - 1, j - 1];
        }
    }

    // Return the maximum sum
    return sum[N, M];
}

// Driver Code
public static void Main(String[] args)
{
    int [,]grid = { { 1, 2 }, { 3, 5 } };

    Console.Write(MaximumPath(grid));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript  program for
//the above approach

// Function to find the maximum sum
// path in the grid
function MaximumPath(grid)
{
    // Dimensions of grid[][]
    let N = grid.length;
    let M = grid[0].length;

    // Stores maximum sum at each cell
    // sum[i][j] from cell sum[0][0]
    let sum =  new Array(N + 1);
    // Loop to create 2D array using 1D array
    for (var i = 0; i < sum.length; i++) {
        sum[i] = new Array(2);
    }

    for (var i = 0; i < sum.length; i++) {
        for (var j = 0; j < sum.length; j++) {
        sum[i][j] = 0;
    }
    }

    // Iterate to compute the maximum
    // sum path in the grid
    for (let i = 1; i <= N; i++)
    {
        for (let j = 1; j <= M; j++)
        {
            // Update the maximum path sum
            sum[i][j] = Math.max(sum[i - 1][j],
                                 sum[i][j - 1]) +
                                 grid[i - 1][j - 1];
        }
    }

    // Return the maximum sum
    return sum[N][M];
}

// Driver Code

    let grid = [[1, 2], [3, 5]];
  document.write(MaximumPath(grid));

  // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*

**方法 2(自上而下):**我们将以自上而下的方式递归解决问题。我们基于到达单元**网格【I】【j】**的两种方式，将递归公式化如下:

1.  如果我们从单元格**网格【I】【j-1】**向右移动*一步，或者，*
2.  如果我们从单元格**网格【I-1】【j】**向下移动*一步*。

> **dp[i][j] = max(dp[i][j-1]、dp[i-1][j]) + grid[i][j]**

因此，我们需要选择给我们最大值的步骤(在上述两个步骤之间)。此外，我们需要添加我们进入的单元格中存在的值，即**网格[i][j]** 。由于这个问题具有重叠子问题的性质，我们可以将子问题的结果(memoize)存储在 2D 矩阵中(我们称之为 **dp** ，以避免相同子问题的重复计算。最初，我们将 **dp** 表中的所有单元格设置为值-1，每次我们找到子问题的答案时，我们都会将其结果覆盖在 **dp** 表中的相应单元格中。因此，在计算任何子问题之前，我们先检查一下——如果那个特定的子问题之前已经被解决或者没有被解决，如果它已经被解决(即，它的对应单元 **dp** 矩阵不是-1)，我们简单地返回那个值，否则我们解决它，并将结果存储在 **dp** 表中。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

vector<vector<int> > dp;

// Function to find the maximum sum path in the grid
int MaximumPathUtil(int i, int j, vector<vector<int> >& grid)
{
    // Base condition
      if (i == 0 || j == 0)
        return 0;

      // If current subproblem is already computed,
      // we simply return its result from the dp table
      if (dp[i][j] != -1)
        return dp[i][j];

      // Computing the current subproblem and
      // store the result in the dp table for future use
      return dp[i][j] = max(MaximumPathUtil(i, j-1, grid), MaximumPathUtil(i - 1, j, grid)) +
                        grid[i-1][j-1];
}

int MaximumPath(vector<vector<int> >& grid)
{
    // Dimensions of grid[][]
    int n = grid.size();
    int m = grid[0].size();

      // dp table to memoize the subproblem results
      dp.resize(n+1, vector<int> (m+1, -1));

      // dp[n][m] gives the max. path sum
      // from grid[0][0] to grid[n-1][m-1]
      return MaximumPathUtil(n, m, grid);
}

// Driver Code
int main()
{
    vector<vector<int> > grid = {{3, 7, 9, 2, 7},
                                 {9, 8, 3, 5, 5},
                                 {1, 7, 9, 8, 6},
                                 {3, 8, 6, 4, 9},
                                 {6, 3, 9, 7, 8}};

    cout << MaximumPath(grid);
    return 0;
}

// This code is contributed by tridib_samanta
```

**输出:**

> Sixty-seven

**时间复杂度:**O(n * m)
T3】空间复杂度: O(n*m)