# 购买至少 X 块巧克力的最低成本

> 原文:[https://www . geesforgeks . org/最低购买成本-至少 x-巧克力/](https://www.geeksforgeeks.org/minimum-cost-of-purchasing-at-least-x-chocolates/)

给定一个正整数 **X** 和一个由 **N** 对组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，其中每对 **(A，B)** 代表一盒，其中 **A** 代表巧克力的数量， **B** 代表当前盒的成本。任务是找到购买至少 **X** 个巧克力的最小成本。

**示例:**

> **输入:** arr[] = {{4，3}、{3，2}、{2，4}、{1，3}、{4，2}}，X = 7
> **输出:** 4
> **示例:**选择第 2 个和第 5 个框。巧克力的数量= 3 + 4 = 7。
> 总成本= 2 + 2 = 4，这是购买至少 7 块巧克力的最低成本。
> 
> **输入:** arr[] = {{10，2}，{5，3}}，X = 20
> **输出:** -1
> **示例:**不存在满足给定条件的盒子集。

**天真法:**最简单的方法是用[递归](https://www.geeksforgeeks.org/recursion/)，考虑盒子的所有子集，计算所有子集的巧克力成本和数量。从所有这样的子集中，选择成本最低的子集和至少 **X** 巧克力。
最优子结构:考虑项目的所有子集，每个盒子可以有两种情况。

*   案例 1:项目包含在最佳子集中。如果包含当前盒，则加上该盒的成本，用当前盒中巧克力的数量减去 **X** 。并重复剩余的 **X** 巧克力移动到下一个指数。
*   情况 2:项目不包含在最佳集合中。如果当前盒不包括在内，则只重复剩余的 **X** 巧克力移动到下一个索引。

因此，可以获得的最小成本是上述两种情况中的最小值。如果 **X ≤ 0** 处理好底壳，返回 **0** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum cost
// of buying least X chocolates
int findMinCost(pair<int, int> arr[],
                int X, int n, int i = 0)
{
    // Base Case
    if (X <= 0)
        return 0;

    if (i >= n)
        return INT_MAX;

    // Include the i-th box
    int inc = findMinCost(arr,
                          X - arr[i].first,
                          n, i + 1);

    if (inc != INT_MAX)
        inc += arr[i].second;

    // Exclude the i-th box
    int exc = findMinCost(arr, X, n, i + 1);

    // Return the minimum of
    // the above two cases
    return min(inc, exc);
}

// Driver Code
int main()
{
    // Given array and value of  X
    pair<int, int> arr[] = {
        { 4, 3 }, { 3, 2 },
        { 2, 4 }, { 1, 3 }, { 4, 2 }
    };

    int X = 7;

    // Store the size of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    int ans = findMinCost(arr, X, n);

    // Print the answer
    if (ans != INT_MAX)
        cout << ans;
    else
        cout << -1;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

// Function to calculate minimum cost
// of buying least X chocolates
static int findMinCost(int[][] arr, int X,
                       int n, int i)
{

    // Base Case
    if (X <= 0)
        return 0;

    if (i >= n)
        return Integer.MAX_VALUE;

    // Include the i-th box
    int inc = findMinCost(arr, X - arr[i][0],
                            n, i + 1);

    if (inc != Integer.MAX_VALUE)
        inc += arr[i][1];

    // Exclude the i-th box
    int exc = findMinCost(arr, X, n, i + 1);

    // Return the minimum of
    // the above two cases
    return Math.min(inc, exc);
}

// Driver Code
public static void main(String[] args)
{

    // Given array and value of  X
    int[][] arr = { { 4, 3 }, { 3, 2 },
                    { 2, 4 }, { 1, 3 },
                    { 4, 2 } };

    int X = 7;

    // Store the size of the array
    int n = arr.length;

    int ans = findMinCost(arr, X, n, 0);

    // Print the answer
    if (ans != Integer.MAX_VALUE)
        System.out.println(ans);
    else
        System.out.println(-1);
}
}

// This code is contributed by Hritik
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate minimum cost
# of buying least X chocolates
def findMinCost(arr,X, n, i = 0):

    # Base Case
    if (X <= 0):
        return 0

    if (i >= n):
        return 10**8

    # Include the i-th box
    inc = findMinCost(arr,X - arr[i][0], n, i + 1)

    if (inc != 10**8):
        inc += arr[i][1]

    # Exclude the i-th box
    exc = findMinCost(arr, X, n, i + 1)

    # Return the minimum of
    # the above two cases
    return min(inc, exc)

# Driver Code
if __name__ == '__main__':

    # Given array and value of  X
    arr = [[ 4, 3 ], [ 3, 2 ],[ 2, 4 ], [ 1, 3 ], [ 4, 2 ]]

    X = 7

    # Store the size of the array
    n = len(arr)
    ans = findMinCost(arr, X, n)

    # Print answer
    if (ans != 10**8):
        print(ans)
    else:
        print(-1)

        # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to calculate minimum cost
    // of buying least X chocolates
    static int findMinCost(int[, ] arr, int X, int n,
                           int i = 0)
    {

        // Base Case
        if (X <= 0)
            return 0;

        if (i >= n)
            return Int32.MaxValue;

        // Include the i-th box
        int inc = findMinCost(arr, X - arr[i, 0], n, i + 1);

        if (inc != Int32.MaxValue)
            inc += arr[i, 1];

        // Exclude the i-th box
        int exc = findMinCost(arr, X, n, i + 1);

        // Return the minimum of
        // the above two cases
        return Math.Min(inc, exc);
    }

    // Driver Code
    public static void Main()
    {

        // Given array and value of  X
        int[, ] arr = {
            { 4, 3 }, { 3, 2 }, { 2, 4 }, { 1, 3 }, { 4, 2 }
        };

        int X = 7;

        // Store the size of the array
        int n = arr.GetLength(0);

        int ans = findMinCost(arr, X, n);

        // Print the answer
        if (ans != Int32.MaxValue)
            Console.Write(ans);
        else
            Console.Write(-1);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

        // Javascript program for the above approach

        // Function to calculate minimum cost
        // of buying least X chocolates
        function findMinCost( arr, X, n,  i = 0)
        {
            // Base Case
            if (X <= 0)
                return 0;

            if (i >= n)
                return Number.MAX_SAFE_INTEGER;

            // Include the i-th box
            let inc = findMinCost(arr,
                X - arr[i][0],
                n, i + 1);

            if (inc != Number.MAX_SAFE_INTEGER)
                inc += arr[i][1];

            // Exclude the i-th box
            let exc = findMinCost(arr, X, n, i + 1);

            // Return the minimum of
            // the above two cases
            return Math.min(inc, exc);
        }

        // Driver Code
            // Given array and value of  X
            let arr = [
                [ 4, 3 ], [ 3, 2 ],
                [ 2, 4 ], [ 1, 3 ], [ 4, 2 ]
            ];

            let X = 7;

            // Store the size of the array
            let n = arr.length;

            let ans = findMinCost(arr, X, n);

            // Print the answer
            if (ans != Number.MAX_SAFE_INTEGER)
                document.write(ans)
            else
                document.write(-1)

        // This code is contributed by Hritik

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)，因为问题包含[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)属性。想法是用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)解决问题。创建一个 [**2D** 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、**DP【N】【X】**来存储递归调用的结果。如果已经计算了某个特定的状态，则以恒定的时间返回存储在表中的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to calculate minimum
// cost of buying at least X chocolates
int findMinCostUtil(pair<int, int> arr[],
                    int X, int n,
                    int** dp, int i = 0)
{
    // Base cases
    if (X <= 0)
        return 0;

    if (i >= n)
        return INT_MAX;

    // If the state is already computed,
    // return its result from the 2D array
    if (dp[i][X] != INT_MAX)
        return dp[i][X];

    // Include the i-th box
    int inc = findMinCostUtil(arr,
                              X - arr[i].first,
                              n, dp,
                              i + 1);

    if (inc != INT_MAX)
        inc += arr[i].second;

    // Exclude the i-th box
    int exc = findMinCostUtil(arr, X, n,
                              dp, i + 1);

    // Update the result of
    // the state in 2D array
    dp[i][X] = min(inc, exc);

    // Return the result
    return dp[i][X];
}

// Function to find the minimum
// cost to buy at least X chocolates
void findMinCost(pair<int, int> arr[], int X, int n)
{
    // Create a 2D array, dp[][]
    int** dp = new int*[n + 1];

    // Initialize entries with INT_MAX
    for (int i = 0; i <= n; i++) {

        dp[i] = new int[X + 1];

        for (int j = 0; j <= X; j++)

            // Update dp[i][j]
            dp[i][j] = INT_MAX;
    }

    // Stores the minimum cost required
    int ans = findMinCostUtil(arr, X, n, dp);

    // Print the answer
    if (ans != INT_MAX)
        cout << ans;
    else
        cout << -1;
}

// Driver Code
int main()
{
    // Given array and value of X
    pair<int, int> arr[] = {
        { 4, 3 }, { 3, 2 },
        { 2, 4 }, { 1, 3 }, { 4, 2 }
    };
    int X = 7;

    // Store the size of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    findMinCost(arr, X, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Recursive function to calculate minimum
// cost of buying at least X chocolates
static int findMinCostUtil(int[][] arr, int X, int n,
                           int[][] dp, int i)
{

    // Base cases
    if (X <= 0)
        return 0;

    if (i >= n)
        return Integer.MAX_VALUE;

    // If the state is already computed,
    // return its result from the 2D array
    if (dp[i][X] != Integer.MAX_VALUE)
        return dp[i][X];

    // Include the i-th box
    int inc = findMinCostUtil(arr, X - arr[i][0],
                              n, dp, i + 1);

    if (inc != Integer.MAX_VALUE)
        inc += arr[i][1];

    // Exclude the i-th box
    int exc = findMinCostUtil(arr, X, n,
                              dp, i + 1);

    // Update the result of
    // the state in 2D array
    dp[i][X] = Math.min(inc, exc);

    // Return the result
    return dp[i][X];
}

// Function to find the minimum
// cost to buy at least X chocolates
static void findMinCost(int[][] arr, int X, int n)
{

    // Create a 2D array, dp[][]
    int[][] dp = new int[n + 1][X + 1];

    // Initialize entries with INT_MAX
    for(int i = 0; i <= n; i++)
    {
        for(int j = 0; j <= X; j++)

            // Update dp[i][j]
            dp[i][j] = Integer.MAX_VALUE;
    }

    // Stores the minimum cost required
    int ans = findMinCostUtil(arr, X, n, dp, 0);

    // Print the answer
    if (ans != Integer.MAX_VALUE)
        System.out.println(ans);
    else
        System.out.println(-1);
}

// Driver code
public static void main(String[] args)
{

    // Given array and value of X
    int[][] arr = { { 4, 3 }, { 3, 2 },
                    { 2, 4 }, { 1, 3 },
                    { 4, 2 } };
    int X = 7;

    // Store the size of the array
    int n = 5;

    findMinCost(arr, X, n);
}
}

// This code is contributed by rameshtravel07
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Recursive function to calculate minimum
# cost of buying at least X chocolates
def findMinCostUtil(arr, X, n, dp, i):

    # Base cases
    if (X <= 0):
        return 0

    if (i >= n):
        return sys.maxsize

    # If the state is already computed,
    # return its result from the 2D array
    if (dp[i][X] != sys.maxsize):
        return dp[i][X]

    # Include the i-th box
    inc = findMinCostUtil(arr, X - arr[i][0], n, dp, i + 1)

    if (inc != sys.maxsize):
        inc += arr[i][1]

    # Exclude the i-th box
    exc = findMinCostUtil(arr, X, n, dp, i + 1)

    # Update the result of
    # the state in 2D array
    dp[i][X] = min(inc, exc)

    # Return the result
    return dp[i][X]

# Function to find the minimum
# cost to buy at least X chocolates
def findMinCost(arr, X, n):

    # Create a 2D array, dp[][]
    dp = [[sys.maxsize for i in range(X+1)] for j in range(n+1)]

    # Stores the minimum cost required
    ans = findMinCostUtil(arr, X, n, dp, 0)

    # Print the answer
    if (ans != sys.maxsize):
        print(ans)
    else:
        print(-1)

# Given array and value of X
arr = [ [ 4, 3 ], [ 3, 2 ], [ 2, 4 ], [ 1, 3 ], [ 4, 2 ] ]
X = 7

# Store the size of the array
n = 5

findMinCost(arr, X, n)

# This code is contributed by decode2207.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
    // Recursive function to calculate minimum
    // cost of buying at least X chocolates
    static int findMinCostUtil(int[,] arr, int X, int n, int[,] dp, int i)
    {
        // Base cases
        if (X <= 0)
            return 0;

        if (i >= n)
            return Int32.MaxValue;

        // If the state is already computed,
        // return its result from the 2D array
        if (dp[i,X] != Int32.MaxValue)
            return dp[i,X];

        // Include the i-th box
        int inc = findMinCostUtil(arr, X - arr[i,0], n, dp, i + 1);

        if (inc != Int32.MaxValue)
            inc += arr[i,1];

        // Exclude the i-th box
        int exc = findMinCostUtil(arr, X, n, dp, i + 1);

        // Update the result of
        // the state in 2D array
        dp[i,X] = Math.Min(inc, exc);

        // Return the result
        return dp[i,X];
    }

    // Function to find the minimum
    // cost to buy at least X chocolates
    static void findMinCost(int[,] arr, int X, int n)
    {
        // Create a 2D array, dp[][]
        int[,] dp = new int[n + 1, X + 1];

        // Initialize entries with INT_MAX
        for (int i = 0; i <= n; i++) {

            for (int j = 0; j <= X; j++)

                // Update dp[i][j]
                dp[i,j] = Int32.MaxValue;
        }

        // Stores the minimum cost required
        int ans = findMinCostUtil(arr, X, n, dp, 0);

        // Print the answer
        if (ans != Int32.MaxValue)
            Console.WriteLine(ans);
        else
            Console.WriteLine(-1);
    }

  static void Main ()
  {

    // Given array and value of X
    int[,] arr = {
        { 4, 3 }, { 3, 2 },
        { 2, 4 }, { 1, 3 }, { 4, 2 }
    };
    int X = 7;

    // Store the size of the array
    int n = 5;

    findMinCost(arr, X, n);
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Recursive function to calculate minimum
    // cost of buying at least X chocolates
    function findMinCostUtil(arr, X, n, dp, i)
    {

        // Base cases
        if (X <= 0)
            return 0;

        if (i >= n)
            return Number.MAX_VALUE;

        // If the state is already computed,
        // return its result from the 2D array
        if (dp[i][X] != Number.MAX_VALUE)
            return dp[i][X];

        // Include the i-th box
        let inc = findMinCostUtil(arr, X - arr[i][0], n, dp, i + 1);

        if (inc != Number.MAX_VALUE)
            inc += arr[i][1];

        // Exclude the i-th box
        let exc = findMinCostUtil(arr, X, n, dp, i + 1);

        // Update the result of
        // the state in 2D array
        dp[i][X] = Math.min(inc, exc);

        // Return the result
        return dp[i][X];
    }

    // Function to find the minimum
    // cost to buy at least X chocolates
    function findMinCost(arr, X, n)
    {

        // Create a 2D array, dp[][]
        let dp = new Array(n + 1);

        // Initialize entries with INT_MAX
        for(let i = 0; i <= n; i++)
        {
            dp[i] = new Array(X + 1);
            for(let j = 0; j <= X; j++)

                // Update dp[i][j]
                dp[i][j] = Number.MAX_VALUE;
        }

        // Stores the minimum cost required
        let ans = findMinCostUtil(arr, X, n, dp, 0);

        // Print the answer
        if (ans != Number.MAX_VALUE)
            document.write(ans);
        else
            document.write(-1);
    }

    // Given array and value of X
    let arr = [ [ 4, 3 ], [ 3, 2 ],
                    [ 2, 4 ], [ 1, 3 ],
                    [ 4, 2 ] ];
    let X = 7;

    // Store the size of the array
    let n = 5;

    findMinCost(arr, X, n);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * X)*
***辅助空间:** O(N * X)*