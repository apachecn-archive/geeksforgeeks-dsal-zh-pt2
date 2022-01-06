# 计数唯一路径是元素乘积包含奇数除数的矩阵

> 原文:[https://www . geesforgeks . org/count-unique-path-is-a-matrix-其元素乘积包含奇数除数/](https://www.geeksforgeeks.org/count-unique-paths-is-a-matrix-whose-product-of-elements-contains-odd-number-of-divisors/)

给定维度为 **NxM** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **mat[][]** ，任务是计算从左上角单元格(即**mat【0】【0】**)到右下角单元格(即**mat【N–1】【M–1】**的唯一路径数，使得该路径中的元素乘积包含奇数个[因子](https://www.geeksforgeeks.org/total-number-divisors-given-number/)。任何单元格的可能移动 **(i，j)** 为 **(i，j + 1)** 或 **(i + 1，j)** 。

**示例:**

> **输入:** mat[][] = {{1，1}，{3，1}，{3，1}}
> **输出:** 2
> **解释:**满足条件的两条可能路径:
> 
> *   1->3->3->1，乘积= 9，9 的除数是 1，3，9，这是奇数。
> *   1->1->1->1，乘积= 1，1 的除数只有 1，这是奇数。
> 
> **输入:** mat[][] = {{4，1}，{4，4}}
> **输出:** 2
> **解释:**满足条件的两种可能路径:
> 
> *   4->4->4，乘积= 64，9 的除数是 1，2，4，8，16，32，64，这是奇数。
> *   4->1->4，乘积= 16，16 的除数是 1，2，4，8，16，这是奇数。

**天真方法:**最简单的方法是[为给定矩阵生成从左上角单元格到右下角单元格的所有可能路径](https://www.geeksforgeeks.org/count-possible-paths-top-left-bottom-right-nxm-matrix/)，并通过使用本文[中讨论的方法](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)找到所有除数来检查所有这些路径的所有元素的乘积是否有奇数个除数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int countPaths = 0;

// Store the product of all paths
vector<int> v;

// Function to calculate and store
// all the paths product in vector
void CountUniquePaths(int a[][105], int i,
                      int j, int m,
                      int n, int ans)
{
    // Base Case
    if (i >= m || j >= n)
        return;

    // If reaches the bottom right
    // corner and product is a
    // perfect square
    if (i == m - 1 && j == n - 1) {

        // Find square root
        long double sr = sqrt(ans * a[i][j]);

        // If square root is an integer
        if ((sr - floor(sr)) == 0)
            countPaths++;
    }

    // Move towards down in the matrix
    CountUniquePaths(a, i + 1, j, m,
                     n, ans * a[i][j]);

    // Move towards right in the matrix
    CountUniquePaths(a, i, j + 1, m,
                     n, ans * a[i][j]);
}

// Driver Code
int main()
{
    int M = 3, N = 2;

    // Given matrix mat[][]
    int mat[M][105] = { { 1, 1 },
                        { 3, 1 },
                        { 3, 1 } };

    // Function Call
    CountUniquePaths(mat, 0, 0, M, N, 1);

    // Print the result
    cout << countPaths;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG{

static int countPaths = 0;

// Function to calculate and store
// all the paths product in vector
static void CountUniquePaths(int[][] a, int i,
                             int j, int m,
                             int n, int ans)
{

    // Base Case
    if (i >= m || j >= n)
        return;

    // If reaches the bottom right
    // corner and product is a
    // perfect square
    if (i == m - 1 && j == n - 1)
    {

        // Find square root
        double sr = Math.sqrt(ans * a[i][j]);

        // If square root is an integer
        if ((sr - Math.floor(sr)) == 0)
            countPaths++;
    }

    // Move towards down in the matrix
     CountUniquePaths(a, i + 1, j, m,
                      n, ans * a[i][j]);

    // Move towards right in the matrix
     CountUniquePaths(a, i, j + 1, m,
                      n, ans * a[i][j]);
}

// Driver Code
public static void main (String[] args)
{
    int M = 3, N = 2;

    // Given matrix mat[][]
    int[][] mat = { { 1, 1 },
                    { 3, 1 },
                    { 3, 1 } };

    // Function call
    CountUniquePaths(mat, 0, 0, M, N, 1);

    System.out.println(countPaths); 
}
}

// This code is contributed by sallagondaavinashreddy7
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
import math 
countPaths = 0;

# Function to calculate
# and store all the paths
# product in vector
def CountUniquePaths(a, i, j,
                     m, n, ans):

    # Base Case
    if (i >= m or j >= n):
        return;

    # If reaches the bottom
    # right corner and product
    # is a perfect square
    global countPaths;

    if (i == m - 1 and
        j == n - 1):

        # Find square root
        sr = math.sqrt(ans * a[i][j]);

        # If square root is an integer
        if ((sr - math.floor(sr)) == 0):
            countPaths += 1;   

    # Move towards down
    # in the matrix
    CountUniquePaths(a, i + 1, j,
                     m, n, ans * a[i][j]);

    # Move towards right
    # in the matrix
    CountUniquePaths(a, i, j + 1,
                     m, n, ans * a[i][j]);

# Driver Code
if __name__ == '__main__':

    M = 3; N = 2;

    # Given matrix mat
    mat = [[1, 1],
           [3, 1],
           [3, 1]];

    # Function call
    CountUniquePaths(mat, 0,
                     0, M, N, 1);

    print(countPaths);

# This code is contributed by Princi Singh
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

static int countPaths = 0;

// Function to calculate and store
// all the paths product in vector
static void CountUniquePaths(int[,] a, int i,
                             int j, int m,
                             int n, int ans)
{   
  // Base Case
  if (i >= m || j >= n)
    return;

  // If reaches the bottom right
  // corner and product is a
  // perfect square
  if (i == m - 1 && j == n - 1)
  {

    // Find square root
    double sr = Math.Sqrt(ans *
                          a[i, j]);

    // If square root is an integer
    if ((sr - Math.Floor(sr)) == 0)
      countPaths++;
  }

  // Move towards down in the matrix
  CountUniquePaths(a, i + 1, j, m,
                   n, ans * a[i, j]);

  // Move towards right in the matrix
  CountUniquePaths(a, i, j + 1, m,
                   n, ans * a[i, j]);
}

// Driver Code
public static void Main (String[] args)
{
  int M = 3, N = 2;

  // Given matrix mat[][]
  int[,] mat = {{1, 1},
                {3, 1},
                {3, 1}};

  // Function call
  CountUniquePaths(mat, 0, 0,
                   M, N, 1);

  Console.Write(countPaths); 
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// Javascript program for the
// above approach
let countPaths = 0;

// Function to calculate and store
// all the paths product in vector
function CountUniquePaths(a, i, j, m, n, ans)
{

    // Base Case
    if (i >= m || j >= n)
        return;

    // If reaches the bottom right
    // corner and product is a
    // perfect square
    if (i == m - 1 && j == n - 1)
    {

        // Find square root
        let sr = Math.sqrt(ans * a[i][j]);

        // If square root is an integer
        if ((sr - Math.floor(sr)) == 0)
            countPaths++;
    }

    // Move towards down in the matrix
     CountUniquePaths(a, i + 1, j, m,
                      n, ans * a[i][j]);

    // Move towards right in the matrix
     CountUniquePaths(a, i, j + 1, m,
                      n, ans * a[i][j]);
}

// Driver Code
let M = 3, N = 2;

// Given matrix mat[][]
let mat = [ [ 1, 1 ],
            [ 3, 1 ],
            [ 3, 1 ] ];

// Function call
CountUniquePaths(mat, 0, 0, M, N, 1);

document.write(countPaths);

// This code is contributed by souravghosh0416

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O((2<sup>N</sup>)* sqrt(N))*
*T8】辅助空间: O(1)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。初始化一个辅助空间 **dp[][][]** ，该空间将存储给定矩阵的每一行的从左上角到每行末尾的所有路径的乘积。以下是步骤:

*   初始化一个 **3D** 辅助空间 **dp[][][]** ， **dp[i][j]** 将存储从单元格 **(0，0)** 到 **(i，j)** 的所有路径的乘积。
*   为了计算每个状态值，通过使用来自**DP(I–1，j)** 和 **dp(i，j–1)**的所有值来计算 dp[i][j]。
*   对于给定矩阵的第一行 **mat[][]** ，将第一行的前缀积存储在 **dp[i][0]** 。
*   对于给定矩阵的第一列 **mat[][]** ，将第一列的前缀乘积存储在 **dp[0][i]** 。
*   现在使用两个嵌套循环 **i** 和 **j** 迭代 **(1，1)** 到 **(N，M)** ，并执行以下操作:
    *   将向量顶部存储在索引**DP[I–1][j]**处，左侧存储在索引**DP[I][j–1]**处。
    *   将当前元素**mat【I】【j】**的乘积与存储在**top【】**和**left【】**中的元素存储在另一个辅助数组**curr【】**中。
    *   将当前 dp 状态更新为 **dp[i][j] = curr** 。
*   现在[遍历存储在**DP(N–1，M–1)**的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并计算所有数字，这是一个[完美的正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。
*   在上述步骤后打印最终计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the results
vector<vector<vector<int> > >
    dp(105, vector<vector<int> >(105));

// Count of unique product paths
int countPaths = 0;

// Function to check whether number
// is perfect square or not
bool isPerfectSquare(int n)
{
    long double sr = sqrt(n);

    // If square root is an integer
    return ((sr - floor(sr)) == 0);
}

// Function to calculate and store
// all the paths product in vector
void countUniquePaths(int a[][105],
                      int m, int n,
                      int ans)
{
    // Store the value a[0][0]
    dp[0][0].push_back(a[0][0]);

    // Initialize first row of dp
    for (int i = 1; i < m; i++) {

        // Find prefix product
        a[i][0] *= a[i - 1][0];
        dp[i][0].push_back(a[i][0]);
    }

    // Initialize first column of dp
    for (int i = 1; i < n; i++) {

        // Find the prefix product
        a[0][i] *= a[0][i - 1];
        dp[0][i].push_back(a[0][i]);
    }

    // Iterate over range (1, 1) to (N, M)
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {

            // Copy  dp[i-1][j] in top[]
            vector<int> top = dp[i - 1][j];

            // Copy dp[i][j-1] into left[]
            vector<int> left = dp[i][j - 1];

            // Compute the values of current
            // state and store it in curr[]
            vector<int> curr;

            // Find the product of a[i][j]
            // with elements at top[]
            for (int k = 0;
                 k < top.size(); k++) {
                curr.push_back(top[k] * a[i][j]);
            }

            // Find the product of a[i][j]
            // with elements at left[]
            for (int k = 0;
                 k < left.size(); k++) {
                curr.push_back(left[k] * a[i][j]);
            }

            // Update the current state
            dp[i][j] = curr;
        }
    }

    // Traverse dp[m - 1][n - 1]
    for (auto i : dp[m - 1][n - 1]) {

        // Check if perfect square
        if (isPerfectSquare(i)) {
            countPaths++;
        }
    }
}

// Driver Code
int main()
{
    int M = 3, N = 4;

    // Given matrix mat[][]
    int mat[M][105] = { { 1, 2, 3, 1 },
                        { 3, 1, 2, 4 },
                        { 2, 3, 1, 1 } };

    // Function Call
    countUniquePaths(mat, M, N, 1);

    // Print the final count
    cout << countPaths;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Stores the results
  static ArrayList<ArrayList<ArrayList<Integer>>> dp;

  // Count of unique product paths
  static int countPaths = 0;

  // Function to check whether number
  // is perfect square or not
  static boolean isPerfectSquare(int n)
  {
    double  sr = Math.sqrt(n);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
  }

  // Function to calculate and store
  // all the paths product in vector
  static void countUniquePaths(int a[][],
                               int m, int n,
                               int ans)
  {

    // Store the value a[0][0]
    dp.get(0).get(0).add(a[0][0]);

    // Initialize first row of dp
    for (int i = 1; i < m; i++)
    {

      // Find prefix product
      a[i][0] *= a[i - 1][0];
      dp.get(i).get(0).add(a[i][0]);
    }

    // Initialize first column of dp
    for (int i = 1; i < n; i++)
    {

      // Find the prefix product
      a[0][i] *= a[0][i - 1];
      dp.get(0).get(i).add(a[0][i]);
    }

    // Iterate over range (1, 1) to (N, M)
    for (int i = 1; i < m; i++)
    {
      for (int j = 1; j < n; j++)
      {

        // Copy  dp[i-1][j] in top[]
        ArrayList<Integer> top =
          dp.get(i - 1).get(j);

        // Copy dp[i][j-1] into left[]
        ArrayList<Integer> left =
          dp.get(i).get(j - 1);

        // Compute the values of current
        // state and store it in curr[]
        ArrayList<Integer> curr = new ArrayList<>();

        // Find the product of a[i][j]
        // with elements at top[]
        for (int k = 0;
             k < top.size(); k++)
        {
          curr.add(top.get(k) * a[i][j]);
        }

        // Find the product of a[i][j]
        // with elements at left[]
        for (int k = 0;
             k < left.size(); k++)
        {
          curr.add(left.get(k) * a[i][j]);
        }

        // Update the current state
        dp.get(i).set(j, curr);
      }
    }

    // Traverse dp[m - 1][n - 1]
    for (Integer i : dp.get(m - 1).get(n - 1))
    {

      // Check if perfect square
      if (isPerfectSquare(i))
      {
        countPaths++;
      }
    }
  }

  // Driver code
  public static void main (String[] args)
  {
    int M = 3, N = 4;

    // Given matrix mat[][]
    int mat[][] = { { 1, 2, 3, 1 },
                   { 3, 1, 2, 4 },
                   { 2, 3, 1, 1 } };

    dp = new ArrayList<>();

    for(int i = 0; i < 105; i++)
    {
      dp.add(new ArrayList<>());
      for(int j = 0; j < 105; j++)
        dp.get(i).add(new ArrayList<Integer>());
    }

    // Function Call
    countUniquePaths(mat, M, N, 1);

    // Print the final count
    System.out.println(countPaths);
  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt, floor

# Stores the results
dp = [[[] for j in range(105)]
          for k in range(105)]

# Count of unique product paths
countPaths = 0

# Function to check whether number
# is perfect square or not
def isPerfectSquare(n):

    sr = sqrt(n)

    # If square root is an integer
    return ((sr - floor(sr)) == 0)

# Function to calculate and store
# all the paths product in vector
def countUniquePaths(a, m, n, ans):

    global dp
    global countPaths

    # Store the value a[0][0]
    dp[0][0].append(a[0][0])

    # Initialize first row of dp
    for i in range(1, m):

        # Find prefix product
        a[i][0] *= a[i - 1][0]
        dp[i][0].append(a[i][0])

    # Initialize first column of dp
    for i in range(1, n):

        # Find the prefix product
        a[0][i] *= a[0][i - 1]
        dp[0][i].append(a[0][i])

    # Iterate over range (1, 1) to (N, M)
    for i in range(1, m):
        for j in range(1, n):

            # Copy  dp[i-1][j] in top[]
            top = dp[i - 1][j]

            # Copy dp[i][j-1] into left[]
            left = dp[i][j - 1]

            # Compute the values of current
            # state and store it in curr[]
            curr = []

            # Find the product of a[i][j]
            # with elements at top[]
            for k in range(len(top)):
                curr.append(top[k] * a[i][j])

            # Find the product of a[i][j]
            # with elements at left[]
            for k in range(len(left)):
                curr.append(left[k] * a[i][j])

            # Update the current state
            dp[i][j] = curr

    # Traverse dp[m - 1][n - 1]
    for i in dp[m - 1][n - 1]:

        # Check if perfect square
        if (isPerfectSquare(i)):
            countPaths += 1

# Driver Code
if __name__ == '__main__':

    M = 3
    N = 4

    # Given matrix mat[][]
    mat = [ [ 1, 2, 3, 1 ],
            [ 3, 1, 2, 4 ],
            [ 2, 3, 1, 1 ] ]

    # Function Call
    countUniquePaths(mat, M, N, 1)

    # Print the final count
    print(countPaths)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Stores the results
    static List<List<List<int>>> dp;

    // Count of unique product paths
    static int countPaths = 0;

    // Function to check whether number
    // is perfect square or not
    static bool isPerfectSquare(int n)
    {
        double sr = Math.Sqrt(n);

        // If square root is an integer
        return ((sr - Math.Floor(sr)) == 0);
    }

    // Function to calculate and store
    // all the paths product in vector
    static void countUniquePaths(int[,] a,
                                 int m, int n,
                                 int ans)
    {

        // Store the value a[0][0]
        dp[0][0].Add(a[0, 0]);

        // Initialize first row of dp
        for (int i = 1; i < m; i++)
        {

            // Find prefix product
            a[i, 0] *= a[i - 1, 0];
            dp[i][0].Add(a[i, 0]);
        }

        // Initialize first column of dp
        for (int i = 1; i < n; i++)
        {

            // Find the prefix product
            a[0, i] *= a[0, i - 1];
            dp[0][i].Add(a[0, i]);
        }

        // Iterate over range (1, 1) to (N, M)
        for (int i = 1; i < m; i++)
        {
            for (int j = 1; j < n; j++)
            {

                // Copy  dp[i-1][j] in top[]
                List<int> top = dp[i - 1][j];

                // Copy dp[i][j-1] into left[]
                List<int> left = dp[i][j - 1];

                // Compute the values of current
                // state and store it in curr[]
                List<int> curr = new List<int>();

                // Find the product of a[i][j]
                // with elements at top[]
                for (int k = 0;
                     k < top.Count; k++)
                {
                    curr.Add(top[k] * a[i, j]);
                }

                // Find the product of a[i][j]
                // with elements at left[]
                for (int k = 0;
                     k < left.Count; k++)
                {
                    curr.Add(left[k] * a[i, j]);
                }

                // Update the current state
                dp[i][j] = curr;
            }
        }

        // Traverse dp[m - 1][n - 1]
        foreach (int i in dp[m - 1][n - 1])
        {

            // Check if perfect square
            if (isPerfectSquare(i))
            {
                countPaths++;
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int M = 3, N = 4;

        // Given matrix mat[][]
        int[,] mat = { { 1, 2, 3, 1 },
                   { 3, 1, 2, 4 },
                   { 2, 3, 1, 1 } };

        dp = new List<List<List<int>>>();

        for (int i = 0; i < 105; i++)
        {
            dp.Add(new List<List<int>>());
            for (int j = 0; j < 105; j++)
                dp[i].Add(new List<int>());
        }

        // Function Call
        countUniquePaths(mat, M, N, 1);

        // Print the final count
        Console.Write(countPaths);
    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Stores the results
let dp = [];

// Count of unique product paths
let countPaths = 0;

// Function to check whether number
// is perfect square or not
function isPerfectSquare(n)
{
    let sr = Math.sqrt(n);

    // If square root is an integer
    return((sr - Math.floor(sr)) == 0);
}

// Function to calculate and store
// all the paths product in vector
function countUniquePaths(a, m, n, ans)
{

    // Store the value a[0][0]
    dp[0][0].push(a[0][0]);

    // Initialize first row of dp
    for(let i = 1; i < m; i++)
    {

        // Find prefix product
        a[i][0] *= a[i - 1][0];
        dp[i][0].push(a[i][0]);
    }

    // Initialize first column of dp
    for(let i = 1; i < n; i++)
    {

        // Find the prefix product
        a[0][i] *= a[0][i - 1];
        dp[0][i].push(a[0][i]);
    }

    // Iterate over range (1, 1) to (N, M)
    for(let i = 1; i < m; i++)
    {
        for(let j = 1; j < n; j++)
        {

            // Copy  dp[i-1][j] in top[]
            let top = dp[i - 1][j];

            // Copy dp[i][j-1] into left[]
            let left = dp[i][j - 1];

            // Compute the values of current
            // state and store it in curr[]
            let curr = [];

            // Find the product of a[i][j]
            // with elements at top[]
            for(let k = 0; k < top.length; k++)
            {
                curr.push(top[k] * a[i][j]);
            }

            // Find the product of a[i][j]
            // with elements at left[]
            for(let k = 0; k < left.length; k++)
            {
                curr.push(left[k] * a[i][j]);
            }

            // Update the current state
            dp[i][j] = curr;
        }
    }

    // Traverse dp[m - 1][n - 1]
    for(let i = 0; i < dp[m - 1][n - 1].length; i++)
    {

        // Check if perfect square
        if (isPerfectSquare(dp[m - 1][n - 1][i]))
        {
            countPaths++;
        }
    }
}

// Driver code
let M = 3, N = 4;
let mat = [ [ 1, 2, 3, 1 ],
            [ 3, 1, 2, 4 ],
            [ 2, 3, 1, 1 ] ];
for(let i = 0; i < 105; i++)
{
    dp.push([]);
    for(let j = 0; j < 105; j++)
        dp[i].push([]);
}

// Function Call
countUniquePaths(mat, M, N, 1);

// Print the final count
document.write(countPaths);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>3</sup> )*