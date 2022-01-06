# 给定矩阵从左上方到右下方的路径的最大非负乘积

> 原文:[https://www . geeksforgeeks . org/从给定矩阵的左上方到右下方的最大非负路径积/](https://www.geeksforgeeks.org/maximum-non-negative-product-of-a-path-from-top-left-to-bottom-right-of-given-matrix/)

给定一个整数[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】**的维度 **N * M** ，任务是打印给定矩阵从左上角单元格 **(0，0)** 到右下角单元格**(N–1，M–1)**路径中矩阵元素的最大乘积。任何单元格 **(i，j)** 唯一可能的移动是 **(i + 1，j)** 或 **(i，j + 1)** 。如果最大乘积为负，则打印**-1”**。

**示例:**

> **输入:** mat[][] = [[1，-2，1]，[1，-2，1]，[3，-4，1]]
> **输出:** 8
> **说明:**从左上方到右下方乘积最大的路径是(0，0) → (1，0) - > (1，1) - > (2，1) - > (2，2)= 1 * 1 *(2)*(-4)*(1)= 8。
> 因此，最大正积为 8。
> 
> **输入:** mat[][] = [[-1，-2，-3]，[-2，-3，-3]，[-3，-3，-2]]
> **输出:** -1
> **说明:**从(0，0)到(2，2)的路径不可能得到非负积。因此，打印-1。

**天真法:**最简单的求解方法是[递归](https://www.geeksforgeeks.org/recursion/)从左上角单元格遍历，从每个单元格向右下移动，生成从左上角单元格到右下角单元格的所有可能路径。为生成的每个路径查找产品，并打印其中的最大值。
***时间复杂度:** O(2 <sup>max(N，M)</sup> )*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。按照以下步骤解决问题:

*   初始化矩阵**最大路径[][]** 和**最小路径[][]** ，分别存储路径的最大和最小乘积。
*   这个想法也是为了跟踪到目前为止获得的**最大负积**，因为如果遇到任何负积，那么**负积**乘以**最大负积**就可以生成**最大正积**。
*   为了达到指数 **(i，j)，**由于允许的可能移动是向右和向下的，所以**最大乘积**可以是最大乘积或最小乘积，直到**(I–1，j)第**指数或 **(i，j–1)<sup>第</sup>** 指数乘以指数 **(i，j)** 处的元素。
*   完成上述步骤后，如果**最大路径【M–1】【N–1】**的值为非负数，则打印为正产品路径。否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to find the maximum product
// from the top left and bottom right
// cell of the given matrix grid[][]
int maxProductPath(vector<vector<int>> grid){

    // Store dimension of grid
    int n = grid.size();
    int m = grid[0].size();

    // Stores maximum product path
    vector<vector<int>> maxPath(n, vector<int>(m, 0));

    // Stores minimum product path
    vector<vector<int>>  minPath(n, vector<int>(m, 0));

    // Traverse the grid and update
    // maxPath and minPath array
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {

            // Initialize to inf and -inf
            int mn = INT_MAX;
            int mx = INT_MIN;

            // Base Case
            if (i == 0 and j == 0)
            {
                mx = grid[i][j];
                mn = grid[i][j];
              }

            // Calculate for row:
            if (i > 0)
            {
                int tempmx = max((maxPath[i - 1][j] * grid[i][j]),
                             (minPath[i - 1][j] * grid[i][j]));

                // Update the maximum
                mx = max(mx, tempmx);
                int tempmn = min((maxPath[i - 1][j] * grid[i][j]),
                             (minPath[i - 1][j] * grid[i][j]));

                // Update the minimum
                mn = min(mn, tempmn);
              }

            // Calculate for column:
            if (j > 0)
            {
                int tempmx = max((maxPath[i][j - 1] * grid[i][j]),
                             (minPath[i][j - 1] * grid[i][j]));

                // Update the maximum
                mx = max(mx, tempmx);
                int tempmn = min((maxPath[i][j - 1] * grid[i][j]),
                             (minPath[i][j - 1] * grid[i][j]));

                // Update the minimum
                mn = min(mn, tempmn);
              }

            // Update maxPath and minPath
            maxPath[i][j] = mx;
            minPath[i][j] = mn;
          }
        }

    // If negative product
    if(maxPath[n - 1][m - 1] < 0)
        return -1;
    // Otherwise
    else
        return(maxPath[n - 1][m - 1]);
}

// Driver Code
int main(){

// Given matrix mat[][]
  vector<vector<int>> mat = {{1, -2, 1},
                            {1, -2, 1},
                            {3, -4, 1}};
  // Function Call
  cout<<(maxProductPath(mat));

}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

  // Function to find the maximum product
  // from the top left and bottom right
  // cell of the given matrix grid[][]
  static int maxProductPath(int[][] grid)
  {

    // Store dimension of grid
    int n = grid.length;
    int m = grid[0].length;

    // Stores maximum product path
    int[][] maxPath = new int[n][m];

    // Stores minimum product path
    int[][] minPath = new int[n][m];

    // Traverse the grid and update
    // maxPath and minPath array
    for(int i = 0; i < n; i++)
    {
      for (int j = 0; j < m; j++)
      {
        // Initialize to inf and -inf
        int mn = Integer.MAX_VALUE;
        int mx = Integer.MIN_VALUE;

        // Base Case
        if(i == 0 && j == 0)
        {
          mx = grid[i][j];
          mn = grid[i][j];
        }

        // Calculate for row:
        if(i > 0)
        {
          int tempmx =Math.max((maxPath[i - 1][j] *
                                grid[i][j]),(minPath[i - 1][j] *
                                             grid[i][j]));

          // Update the maximum
          mx = Math.max(mx, tempmx);
          int tempmn = Math.min((maxPath[i - 1][j] *
                                 grid[i][j]),(minPath[i - 1][j] *
                                              grid[i][j]));

          // Update the minimum
          mn=Math.min(mn, tempmn);            
        }

        // Calculate for column
        if(j > 0)
        {
          int tempmx = Math.max((maxPath[i][j - 1] *
                                 grid[i][j]),(minPath[i][j - 1] *
                                              grid[i][j]));

          // Update the maximum
          mx = Math.max(mx, tempmx);
          int tempmn = Math.min((maxPath[i][j - 1] *
                                 grid[i][j]),(minPath[i][j - 1] *
                                              grid[i][j]));

          // Update the minimum
          mn=Math.min(mn, tempmn);
        }

        // Update maxPath and minPath
        maxPath[i][j] = mx;
        minPath[i][j] = mn;
      }
    }

    // If negative product
    if(maxPath[n - 1][m - 1] < 0)
    {
      return -1;
    }

    // Otherwise
    else
    {
      return(maxPath[n - 1][m - 1]);
    }
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given matrix mat[][]
    int[][] mat = {{1, -2, 1}, {1, -2, 1}, {3, -4, 1}};

    // Function Call
    System.out.println(maxProductPath(mat));
  }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum product
# from the top left and bottom right
# cell of the given matrix grid[][]
def maxProductPath(grid):

    # Store dimension of grid
    n, m = len(grid), len(grid[0])

    # Stores maximum product path
    maxPath = [[0 for i in range(m)] for j in range(n)]

    # Stores minimum product path
    minPath = [[0 for i in range(m)] for j in range(n)]

    # Traverse the grid and update
    # maxPath and minPath array
    for i in range(n):
        for j in range(m):

            # Initialize to inf and -inf
            mn = float("inf")
            mx = float("-inf")

            # Base Case
            if (i == 0 and j == 0):
                mx = grid[i][j]
                mn = grid[i][j]

            # Calculate for row:
            if i > 0:
                tempmx = max((maxPath[i - 1][j] * grid[i][j]),
                             (minPath[i - 1][j] * grid[i][j]))

                # Update the maximum
                mx = max(mx, tempmx)
                tempmn = min((maxPath[i - 1][j] * grid[i][j]),
                             (minPath[i - 1][j] * grid[i][j]))

                # Update the minimum
                mn = min(mn, tempmn)

            # Calculate for column:
            if (j > 0):
                tempmx = max((maxPath[i][j - 1] * grid[i][j]),
                             (minPath[i][j - 1] * grid[i][j]))

                # Update the maximum
                mx = max(mx, tempmx)
                tempmn = min((maxPath[i][j - 1] * grid[i][j]),
                             (minPath[i][j - 1] * grid[i][j]))

                # Update the minimum
                mn = min(mn, tempmn)

            # Update maxPath and minPath
            maxPath[i][j] = mx
            minPath[i][j] = mn

    # If negative product
    if(maxPath[n - 1][m - 1] < 0):
        return -1

    # Otherwise
    else:
        return(maxPath[n - 1][m - 1])

# Driver Code

# Given matrix mat[][]
mat = [[1, -2, 1],
        [1, -2, 1],
        [3, -4, 1]]

# Function Call
print(maxProductPath(mat))
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find the maximum product
  // from the top left and bottom right
  // cell of the given matrix grid[][]
  static int maxProductPath(int[,] grid)
  {

    // Store dimension of grid
    int n = grid.GetLength(0);
    int m = grid.GetLength(1);

    // Stores maximum product path
    int[,] maxPath = new int[n, m];

    // Stores minimum product path
    int[,] minPath = new int[n, m];

    // Traverse the grid and update
    // maxPath and minPath array
    for(int i = 0; i < n; i++)
    {
      for (int j = 0; j < m; j++)
      {

        // Initialize to inf and -inf
        int mn = Int32.MaxValue;
        int mx = Int32.MinValue;

        // Base Case
        if(i == 0 && j == 0)
        {
          mx = grid[i, j];
          mn = grid[i, j];
        }

        // Calculate for row:
        if(i > 0)
        {
          int tempmx = Math.Max((maxPath[i - 1, j] *
                                 grid[i, j]),
                                (minPath[i - 1, j] *
                                 grid[i, j]));

          // Update the maximum
          mx = Math.Max(mx, tempmx);
          int tempmn = Math.Min((maxPath[i - 1, j] *
                                 grid[i, j]),
                                (minPath[i - 1, j] *
                                 grid[i, j]));

          // Update the minimum
          mn = Math.Min(mn, tempmn);
        }

        // Calculate for column
        if(j > 0)
        {
          int tempmx = Math.Max((maxPath[i, j - 1] *
                                 grid[i, j]),
                                (minPath[i, j - 1] *
                                 grid[i, j]));

          // Update the maximum
          mx = Math.Max(mx, tempmx);
          int tempmn = Math.Min((maxPath[i, j - 1] *
                                 grid[i, j]),
                                (minPath[i, j - 1] *
                                 grid[i,j]));

          // Update the minimum
          mn = Math.Min(mn, tempmn);

        }

        // Update maxPath and minPath
        maxPath[i,j] = mx;
        minPath[i,j] = mn;
      }
    }
    // If negative product
    if(maxPath[n - 1, m - 1] < 0)
    {
      return -1;
    }

    // Otherwise
    else
    {
      return(maxPath[n - 1, m - 1]);
    }
  }

  // Driver Code
  static public void Main ()
  {

    // Given matrix mat[][]
    int[,] mat={{1, -2, 1}, {1, -2, 1}, {3, -4, 1}};

    // Function Call
    Console.WriteLine(maxProductPath(mat));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum product
// from the top left and bottom right
// cell of the given matrix grid[][]
function maxProductPath(grid){

    // Store dimension of grid
    var n = grid.length;
    var m = grid[0].length;

    // Stores maximum product path
    var maxPath = Array.from(Array(n), ()=>Array(m).fill(0));

    // Stores minimum product path
    var minPath = Array.from(Array(n), ()=>Array(m).fill(0));

    // Traverse the grid and update
    // maxPath and minPath array
    for (var i = 0; i < n; i++)
    {
        for (var j = 0; j < m; j++)
        {

            // Initialize to inf and -inf
            var mn = 1000000000;
            var mx = -1000000000;

            // Base Case
            if (i == 0 && j == 0)
            {
                mx = grid[i][j];
                mn = grid[i][j];
              }

            // Calculate for row:
            if (i > 0)
            {
                var tempmx =
                Math.max((maxPath[i - 1][j] * grid[i][j]),
                         (minPath[i - 1][j] * grid[i][j]));

                // Update the maximum
                mx = Math.max(mx, tempmx);
                var tempmn =
                Math.min((maxPath[i - 1][j] * grid[i][j]),
                         (minPath[i - 1][j] * grid[i][j]));

                // Update the minimum
                mn = Math.min(mn, tempmn);
              }

            // Calculate for column:
            if (j > 0)
            {
                var tempmx =
                Math.max((maxPath[i][j - 1] * grid[i][j]),
                         (minPath[i][j - 1] * grid[i][j]));

                // Update the maximum
                mx = Math.max(mx, tempmx);
                var tempmn =
                Math.min((maxPath[i][j - 1] * grid[i][j]),
                         (minPath[i][j - 1] * grid[i][j]));

                // Update the minimum
                mn = Math.min(mn, tempmn);
              }

            // Update maxPath and minPath
            maxPath[i][j] = mx;
            minPath[i][j] = mn;
          }
        }

    // If negative product
    if(maxPath[n - 1][m - 1] < 0)
        return -1;
    // Otherwise
    else
        return(maxPath[n - 1][m - 1]);
}

// Driver Code

// Given matrix mat[][]
var mat = [[1, -2, 1],
           [1, -2, 1],
           [3, -4, 1]];

// Function Call
document.write(maxProductPath(mat));

</script>
```

**Output:** 

```
8
```

***时间复杂度:** O(M*N)*
***辅助空间:** O(M*N)*