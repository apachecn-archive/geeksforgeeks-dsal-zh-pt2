# 最小化成本，通过给定的操作将数组缩减为单个元素

> 原文:[https://www . geeksforgeeks . org/通过给定的操作最小化将阵列缩减为单个元素的成本/](https://www.geeksforgeeks.org/minimize-cost-to-reduce-the-array-to-a-single-element-by-given-operations/)

给定一个由 **N** 整数和一个整数 **K** 组成的数组**a【】**，任务是通过选择任意一对连续的数组元素，找到将给定数组缩减为单个元素的最小代价，并用 **(a[i] + a[i+1])** 替换，代价为 **K * (a[i] + a[i+1])** 。

**示例:**

> **输入:** a[] = {1，2，3}，K = 2
> **输出:** 18
> **解释:**
> 将{1，2}重编 3 将数组修改为{3，3}。成本 2 * 3 = 6
> 将{3，3}重新乘以 6 会将数组修改为{6}。成本 2 * 6 = 12
> 因此，总成本为 18
> **输入:** a[] = {4，5，6，7}，K = 3
> **输出:** 132

**天真的方法:**
最简单的解决方案是将数组分成**两半**，对于每个索引，递归计算两半的成本，最后将它们各自的成本相加。
以下是上述方法的实施:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
#define inf 10000009

// Function to combine the sum of the two halves
int Combine(int a[], int i, int j)
{
    int sum = 0;

    // Calculate the sum from i to j
    for (int l = i; l <= j; l++)
        sum += a[l];

    return sum;
}

// Function to minimize the cost to
// reduce the array to a single element
int minCost(int a[], int i, int j, int k)
{
    if (i >= j)
    {

        // Base case
        // If n = 1 or n = 0
        return 0;
    }

    // Initialize cost to maximum value
    int best_cost = inf;

    // Iterate through all possible indices
    // and find the best index
    // to combine the subproblems
    for (int pos = i; pos < j; pos++)
    {

        // Compute left subproblem
        int left = minCost(a, i, pos, k);

        // Compute right subproblem
        int right = minCost(a, pos + 1, j, k);

        // Calculate the best cost
        best_cost = min(best_cost, left + right +
                                   k * Combine(a, i, j));
    }

    // Return the answer
    return best_cost;
}

// Driver code
int main()
{
    int n = 4;
    int a[] = { 4, 5, 6, 7 };
    int k = 3;

    cout << minCost(a, 0, n - 1, k) << endl;
    return 0;
}

// This code is contributed by PrinciRaj1992
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;

class GFG {

    static int inf = 10000009;

    // Function to minimize the cost to
    // reduce the array to a single element
    public static int minCost(int a[], int i,
                              int j, int k)
    {
        if (i >= j) {

            // Base case
            // If n = 1 or n = 0
            return 0;
        }

        // Initialize cost to maximum value
        int best_cost = inf;

        // Iterate through all possible indices
        // and find the best index
        // to combine the subproblems
        for (int pos = i; pos < j; pos++) {

            // Compute left subproblem
            int left = minCost(a, i, pos, k);

            // Compute right subproblem
            int right = minCost(a, pos + 1, j, k);

            // Calculate the best  cost
            best_cost = Math.min(
                best_cost,
                left + right + k * Combine(a, i, j));
        }

        // Return the answer
        return best_cost;
    }

    // Function to combine the sum of the two halves
    public static int Combine(int a[], int i, int j)
    {
        int sum = 0;

        // Calculate the sum from i to j
        for (int l = i; l <= j; l++)
            sum += a[l];

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4;
        int a[] = { 4, 5, 6, 7 };
        int k = 3;

        System.out.println(minCost(a, 0, n - 1, k));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach
inf = 10000009;

# Function to minimize the cost to
# reduce the array to a single element
def minCost(a, i, j, k):
    if (i >= j):

        # Base case
        # If n = 1 or n = 0
        return 0;

    # Initialize cost to maximum value
    best_cost = inf;

    # Iterate through all possible indices
    # and find the best index
    # to combine the subproblems
    for pos in range(i, j):

        # Compute left subproblem
        left = minCost(a, i, pos, k);

        # Compute right subproblem
        right = minCost(a, pos + 1, j, k);

        # Calculate the best cost
        best_cost = min(best_cost,
                        left + right +
                        k * Combine(a, i, j));

    # Return the answer
    return best_cost;

# Function to combine
# the sum of the two halves
def Combine(a, i, j):
    sum = 0;

    # Calculate the sum from i to j
    for l in range(i, j + 1):
        sum += a[l];

    return sum;

# Driver code
if __name__ == '__main__':
    n = 4;
    a = [4, 5, 6, 7];
    k = 3;

    print(minCost(a, 0, n - 1, k));

# This code is contributed by Amit Katiyar
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

  static int inf = 10000009;

  // Function to minimize the cost to
  // reduce the array to a single element
  public static int minCost(int []a, int i,
                            int j, int k)
  {
    if (i >= j)
    {

      // Base case
      // If n = 1 or n = 0
      return 0;
    }

    // Initialize cost to maximum value
    int best_cost = inf;

    // Iterate through all possible indices
    // and find the best index
    // to combine the subproblems
    for (int pos = i; pos < j; pos++)
    {

      // Compute left subproblem
      int left = minCost(a, i, pos, k);

      // Compute right subproblem
      int right = minCost(a, pos + 1, j, k);

      // Calculate the best  cost
      best_cost = Math.Min(best_cost,
                           left + right +
                           k * Combine(a, i, j));
    }

    // Return the answer
    return best_cost;
  }

  // Function to combine the sum of the two halves
  public static int Combine(int []a, int i, int j)
  {
    int sum = 0;

    // Calculate the sum from i to j
    for (int l = i; l <= j; l++)
      sum += a[l];

    return sum;
  }

  // Driver code
  public static void Main(String[] args)
  {
    int n = 4;
    int []a = { 4, 5, 6, 7 };
    int k = 3;

    Console.WriteLine(minCost(a, 0, n - 1, k));
  }
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach
var inf = 10000009;

// Function to combine the sum of the two halves
function Combine(a, i, j)
{
    var sum = 0;

    // Calculate the sum from i to j
    for (var l = i; l <= j; l++)
        sum += a[l];

    return sum;
}

// Function to minimize the cost to
// reduce the array to a single element
function minCost(a, i, j, k)
{
    if (i >= j)
    {

        // Base case
        // If n = 1 or n = 0
        return 0;
    }

    // Initialize cost to maximum value
    var best_cost = inf;

    // Iterate through all possible indices
    // and find the best index
    // to combine the subproblems
    for (var pos = i; pos < j; pos++)
    {

        // Compute left subproblem
        var left = minCost(a, i, pos, k);

        // Compute right subproblem
        var right = minCost(a, pos + 1, j, k);

        // Calculate the best cost
        best_cost = Math.min(best_cost, left + right +
                                   k * Combine(a, i, j));
    }

    // Return the answer
    return best_cost;
}

// Driver code

var n = 4;
var a = [4, 5, 6, 7];
var k = 3;
document.write( minCost(a, 0, n - 1, k));

</script>
```

**Output:** 

```
132
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的概念。按照以下步骤解决问题:

*   初始化矩阵 **dp[][]** ，使得 **dp[i][j]** 存储从索引 **i** 到 **j** 的总和。
*   使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术计算**和(I，j)** 。
*   计算两个子问题的总和，并用最小值更新成本。
*   存储在 dp[][]中并返回。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int inf = 10000000;

// Function to generate the cost using
// Prefix Sum Array technique
vector<int> preprocess(vector<int> a, int n)
{
    vector<int> p(n);
    p[0] = a[0];

    for(int i = 1; i < n; i++)
    {
        p[i] = p[i - 1] + a[i];
    }
    return p;
}

// Function to combine the sum of the
// two subproblems
int Combine(vector<int> p, int i, int j)
{
    if (i == 0)
        return p[j];
    else
        return p[j] - p[i - 1];
}

// Function to minimize the cost to
// add the array elements to a single element
int minCost(vector<int> a, int i, int j, int k,
            vector<int> prefix, vector<vector<int>> dp)
{
    if (i >= j)
        return 0;

    // Check if the value is
    // already stored in the array
    if (dp[i][j] != -1)
        return dp[i][j];

    int best_cost = inf;
    for(int pos = i; pos < j; pos++)
    {

        // Compute left subproblem
        int left = minCost(a, i, pos,
                           k, prefix, dp);

        // Compute left subproblem
        int right = minCost(a, pos + 1, j,
                            k, prefix, dp);

        // Calculate minimum cost
        best_cost = min(best_cost, left + right +
                       (k * Combine(prefix, i, j)));
    }

    // Store the answer to
    // avoid recalculation
    return dp[i][j] = best_cost;
}

// Driver code   
int main()
{
    int n = 4;

    vector<int> a = { 4, 5, 6, 7 };

    int k = 3;

    // Initialise dp array
    vector<vector<int>> dp;
    dp.resize(n + 1, vector<int>(n + 1));
    for(int i = 0; i < n + 1; i++)
    {
        for(int j = 0; j < n + 1; j++)
        {
            dp[i][j] = -1;
        }
    }

    // Preprocessing the array
    vector<int> prefix = preprocess(a, n);

    cout << minCost(a, 0, n - 1, k, prefix, dp)
         << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;
public class Main {

    static int inf = 10000000;

    // Function to minimize the cost to
    // add the array elements to a single element
    public static int minCost(int a[], int i, int j, int k,
                              int[] prefix, int[][] dp)
    {
        if (i >= j)
            return 0;

        // Check if the value is
        // already stored in the array
        if (dp[i][j] != -1)
            return dp[i][j];

        int best_cost = inf;
        for (int pos = i; pos < j; pos++) {

            // Compute left subproblem
            int left = minCost(a, i, pos, k, prefix, dp);

            // Compute left subproblem
            int right
                = minCost(a, pos + 1, j, k, prefix, dp);

            // Calculate minimum cost
            best_cost = Math.min(
                best_cost,
                left + right + (k * Combine(prefix, i, j)));
        }

        // Store the answer to
        // avoid recalculation
        return dp[i][j] = best_cost;
    }

    // Function to generate the cost using
    // Prefix Sum Array technique
    public static int[] preprocess(int[] a, int n)
    {
        int p[] = new int[n];
        p[0] = a[0];
        for (int i = 1; i < n; i++)
            p[i] = p[i - 1] + a[i];
        return p;
    }

    // Function to combine the sum of the two subproblems
    public static int Combine(int[] p, int i, int j)
    {
        if (i == 0)
            return p[j];
        else
            return p[j] - p[i - 1];
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 4;

        int a[] = { 4, 5, 6, 7 };

        int k = 3;

        // Initialise dp array
        int dp[][] = new int[n + 1][n + 1];
        for (int i[] : dp)
            Arrays.fill(i, -1);

        // Preprocessing the array
        int prefix[] = preprocess(a, n);

        System.out.println(
            minCost(a, 0, n - 1, k, prefix, dp));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
inf = 10000000

# Function to minimize the cost to
# add the array elements to a single element
def minCost(a, i, j, k, prefix, dp):

    if (i >= j):
        return 0

    # Check if the value is
    # already stored in the array
    if (dp[i][j] != -1):
        return dp[i][j]

    best_cost = inf
    for pos in range(i, j):

        # Compute left subproblem
        left = minCost(a, i, pos,
                       k, prefix, dp)

        # Compute left subproblem
        right = minCost(a, pos + 1, j,
                        k, prefix, dp)

        # Calculate minimum cost
        best_cost = min(best_cost,
                        left + right +
                          (k * Combine(prefix, i, j)))

    # Store the answer to
    # avoid recalculation
    dp[i][j] = best_cost

    return dp[i][j]

# Function to generate the cost using
# Prefix Sum Array technique
def preprocess(a, n):

    p = [0] * n
    p[0] = a[0]

    for i in range(1, n):
        p[i] = p[i - 1] + a[i]

    return p

# Function to combine the sum
# of the two subproblems
def Combine(p, i, j):

    if (i == 0):
        return p[j]
    else:
        return p[j] - p[i - 1]

# Driver Code
if __name__ == "__main__":

    n = 4
    a = [ 4, 5, 6, 7 ]
    k = 3

    # Initialise dp array
    dp = [[-1 for x in range (n + 1)]
              for y in range (n + 1)]

    # Preprocessing the array
    prefix = preprocess(a, n)

    print(minCost(a, 0, n - 1, k, prefix, dp))

# This code is contributed by chitranayal
```

## C#

```
// C# Program for the above approach
using System;
class GFG{

  static int inf = 10000000;

  // Function to minimize the cost to
  // add the array elements to a single element
  public static int minCost(int []a, int i, int j, int k,
                            int[] prefix, int[,] dp)
  {
    if (i >= j)
      return 0;

    // Check if the value is
    // already stored in the array
    if (dp[i, j] != -1)
      return dp[i, j];

    int best_cost = inf;
    for (int pos = i; pos < j; pos++)
    {

      // Compute left subproblem
      int left = minCost(a, i, pos, k, prefix, dp);

      // Compute left subproblem
      int right = minCost(a, pos + 1, j,
                          k, prefix, dp);

      // Calculate minimum cost
      best_cost = Math.Min(best_cost, left + right +
                          (k * Combine(prefix, i, j)));
    }

    // Store the answer to
    // avoid recalculation
    return dp[i, j] = best_cost;
  }

  // Function to generate the cost using
  // Prefix Sum Array technique
  public static int[] preprocess(int[] a, int n)
  {
    int []p = new int[n];
    p[0] = a[0];
    for (int i = 1; i < n; i++)
      p[i] = p[i - 1] + a[i];
    return p;
  }

  // Function to combine the sum of the two subproblems
  public static int Combine(int[] p, int i, int j)
  {
    if (i == 0)
      return p[j];
    else
      return p[j] - p[i - 1];
  }

  // Driver Code
  public static void Main(String []args)
  {
    int n = 4;

    int []a = { 4, 5, 6, 7 };

    int k = 3;

    // Initialise dp array
    int [,]dp = new int[n + 1, n + 1];
    for(int i = 0; i < n + 1; i++)
    {
      for (int j = 0; j < n + 1; j++)
      {
        dp[i, j] = -1;
      }
    }
    // Preprocessing the array
    int []prefix = preprocess(a, n);

    Console.WriteLine(minCost(a, 0, n - 1, k,
                              prefix, dp));
  }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

var inf = 10000000;

// Function to generate the cost using
// Prefix Sum Array technique
function preprocess(a, n)
{
    var p = Array(n);
    p[0] = a[0];

    for(var i = 1; i < n; i++)
    {
        p[i] = p[i - 1] + a[i];
    }
    return p;
}

// Function to combine the sum of the
// two subproblems
function Combine(p, i, j)
{
    if (i == 0)
        return p[j];
    else
        return p[j] - p[i - 1];
}

// Function to minimize the cost to
// add the array elements to a single element
function minCost(a, i, j, k, prefix, dp)
{
    if (i >= j)
        return 0;

    // Check if the value is
    // already stored in the array
    if (dp[i][j] != -1)
        return dp[i][j];

    var best_cost = inf;
    for(var pos = i; pos < j; pos++)
    {

        // Compute left subproblem
        var left = minCost(a, i, pos,
                           k, prefix, dp);

        // Compute left subproblem
        var right = minCost(a, pos + 1, j,
                            k, prefix, dp);

        // Calculate minimum cost
        best_cost = Math.min(best_cost, left + right +
                       (k * Combine(prefix, i, j)));
    }

    // Store the answer to
    // avoid recalculation
    return dp[i][j] = best_cost;
}

// Driver code   
var n = 4;
var a = [4, 5, 6, 7];
var k = 3;
// Initialise dp array
var dp = Array.from(Array(n+1), ()=>Array(n+1).fill(-1));

// Preprocessing the array
var prefix = preprocess(a, n);

document.write( minCost(a, 0, n - 1, k, prefix, dp))

</script>
```

**Output:** 

```
132
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*