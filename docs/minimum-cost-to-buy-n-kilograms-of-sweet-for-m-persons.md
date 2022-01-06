# M 人购买 N 公斤糖果的最低成本

> 原文:[https://www . geesforgeks . org/m 人购买 n 公斤糖的最低成本/](https://www.geeksforgeeks.org/minimum-cost-to-buy-n-kilograms-of-sweet-for-m-persons/)

给定 n 种尺寸的数组，它包含了糖果的成本，这样，甜食[i]就是糖果的成本。任务是找到为 m 人购买 n 公斤糖果的最低成本。
由于糖果是袋装的，你最多只能给你的‘m’亲戚买一包糖果。你最多只能买一包糖果。此外，cost[i] = 0 表示数据包大小为 I 的 sweet 不可用。此外，还有无限数量的 I 大小的糖果包。

**示例**:

> **输入** : m = 3，n = 6，arr[] = {2，1，3，0，4，10}
> **输出** : 3
> 我们最多可以选择 3 包。我们选择 3 包 2 号的，每包 1 英镑。因此，输出为 3。
> 
> **输入** : m = 2，n = 7，arr[] = {1，3，0，5，0，0，0}
> **输出** : 0
> 我们最多可以选择 2 包。7 可以由 1 2 和 4 个索引组成，但是由于您最多需要 2 包才能获得 7 个糖果包的甜蜜答案，这是不可能的。因此，答案是 0，因为它由 3 个数据包组成，而不是 2 个。

**进场:**

1.  创建一个矩阵 sweet[m+1][n+1][n+1]，其中 m 是亲戚的数量，n 是要购买的糖果的总公斤数，以及糖果的包装数。
2.  用 0 初始化 sweet[i][0][j]元素，用-1 初始化 sweet[i][j][0]。
3.  现在根据以下规则填写矩阵–
    *   购买“k”包并将其分配给 dp 阵列。如果 i>0 并且 j > =当前包装的数量并且 k 糖果的价格大于 0。将 dp 定义为 d**p[I-1][j-k][k]+sweet[k]**
    *   如果 dp 未定义，从以前的 k-1 包中选择->**DP[I][j][k]= DP[I][j][k-1]**
4.  如果 dp[m][n][n]为-1，则答案为 0。否则，打印 dp[m][n][n]

下面是上述方法的实现:

## C++

```
// C++ program to minimum cost to buy
// N kilograms of sweet for M persons
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost of sweets
int find(int m, int n, int adj[])
{
    // Defining the sweet array
    int sweet[n + 1];

    // DP array to store the values
    int dp[n + 1][n + 1][n + 1];

    sweet[0] = 0;

    // Since index starts from 1 we
    // reassign the array into sweet
    for (int i = 1; i <= m; ++i)
        sweet[i] = adj[i - 1];

    // Assigning base cases for dp array
    for (int i = 0; i <= m; ++i) {
        for (int k = 0; k <= n; ++k)

            // At 0 it is free
            dp[i][0][k] = 0;

        // Package not available for desirable amount of sweets
        for (int k = 1; k <= n; ++k)
            dp[i][k][0] = -1;
    }

    for (int i = 0; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            for (int k = 1; k <= n; ++k) {

                dp[i][j][k] = -1;

                // Buying the 'k' kg package and
                // assigning it to dp array
                if (i > 0 && j >= k && sweet[k] > 0
                    && dp[i - 1][j - k][k] != -1)

                    dp[i][j][k] = dp[i - 1][j - k][k] + sweet[k];

                // If no solution, select from previous k-1 packages
                if (dp[i][j][k] == -1 || (dp[i][j][k - 1] != -1
                                          && dp[i][j][k] > dp[i][j][k - 1]))

                    dp[i][j][k] = dp[i][j][k - 1];
            }
        }
    }

    // If solution does not exist
    if (dp[m][n][n] == -1)
        return 0;

    // Print the solution
    else
        return dp[m][n][n];
}

// Driver Function
int main()
{
    int m = 3;
    int adj[] = { 2, 1, 3, 0, 4, 10 };
    int n = sizeof(adj) / sizeof(adj[0]);

    // Calling the desired function
    cout << find(m, n, adj);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to minimum cost to buy
// N kilograms of sweet for M persons
public class GFG {

    // Function to find the minimum cost of sweets
    static int find(int m, int n, int adj[])
    {
        // Defining the sweet array
        int sweet[] = new int [n + 1] ;

        // DP array to store the values
        int dp[][][] = new int [n + 1][n + 1][n + 1] ;

        sweet[0] = 0;

        // Since index starts from 1 we
        // reassign the array into sweet
        for (int i = 1; i <= m; ++i)
            sweet[i] = adj[i - 1];

        // Assigning base cases for dp array
        for (int i = 0; i <= m; ++i) {
            for (int k = 0; k <= n; ++k)

                // At 0 it is free
                dp[i][0][k] = 0;

            // Package not available for desirable amount of sweets
            for (int k = 1; k <= n; ++k)
                dp[i][k][0] = -1;
        }

        for (int i = 0; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                for (int k = 1; k <= n; ++k) {

                    dp[i][j][k] = -1;

                    // Buying the 'k' kg package and
                    // assigning it to dp array
                    if (i > 0 && j >= k && sweet[k] > 0
                        && dp[i - 1][j - k][k] != -1)

                        dp[i][j][k] = dp[i - 1][j - k][k] + sweet[k];

                    // If no solution, select from previous k-1 packages
                    if (dp[i][j][k] == -1 || (dp[i][j][k - 1] != -1
                                              && dp[i][j][k] > dp[i][j][k - 1]))

                        dp[i][j][k] = dp[i][j][k - 1];
                }
            }
        }

        // If solution does not exist
        if (dp[m][n][n] == -1)
            return 0;

        // Print the solution
        else
            return dp[m][n][n];
    }

    // Driver code
    public static void main(String args[])
    {
        int m = 3;
        int adj[] = { 2, 1, 3, 0, 4, 10 };
        int n = adj.length ;
        System.out.println( find(m, n, adj));
    }
    // This Code is contributed by ANKITRAI1
}

```

## 计算机编程语言

```
# Python3 program to minimum cost to buy
# N kilograms of sweet for M persons

# Function to find the minimum cost of sweets
def find(m, n, adj):

    # Defining the sweet array
    sweet = [0] * (n + 1)

    # DP array to store the values
    dp = [[[ 0 for i in range(n + 1)] for i in range(n + 1)] for i in range(n + 1)]

    sweet[0] = 0

    # Since index starts from 1 we
    # reassign the array into sweet
    for i in range(1, m + 1):
        sweet[i] = adj[i - 1]

    # Assigning base cases for dp array
    for i in range(m + 1):
        for k in range(n + 1):

            # At 0 it is free
            dp[i][0][k] = 0

        # Package not available for desirable amount of sweets
        for k in range(1, n + 1):
            dp[i][k][0] = -1

    for i in range(m + 1):
        for j in range(1, n + 1):
            for k in range(1, n + 1):

                dp[i][j][k] = -1

                # Buying the 'k' kg package and
                # assigning it to dp array
                if (i > 0 and j >= k and sweet[k] > 0 and dp[i - 1][j - k][k] != -1):

                    dp[i][j][k] = dp[i - 1][j - k][k] + sweet[k]

                # If no solution, select from previous k-1 packages
                if (dp[i][j][k] == -1 or (dp[i][j][k - 1] != -1 and dp[i][j][k] > dp[i][j][k - 1])):

                    dp[i][j][k] = dp[i][j][k - 1]

    # If solution does not exist
    if (dp[m][n][n] == -1):
        return 0

    # Print the solution
    else:
        return dp[m][n][n]

# Driver Function

m = 3
adj = [2, 1, 3, 0, 4, 10]
n = len(adj)

# Calling the desired function
print(find(m, n, adj))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to minimum cost to buy
// N kilograms of sweet for M persons
using System;

class GFG
{

// Function to find the minimum
// cost of sweets
static int find(int m, int n,
                int[] adj)
{
    // Defining the sweet array
    int[] sweet = new int [n + 1] ;

    // DP array to store the values
    int[,,] dp = new int [n + 1, n + 1,
                                 n + 1];

    sweet[0] = 0;

    // Since index starts from 1 we
    // reassign the array into sweet
    for (int i = 1; i <= m; ++i)
        sweet[i] = adj[i - 1];

    // Assigning base cases
    // for dp array
    for (int i = 0; i <= m; ++i)
    {
        for (int k = 0; k <= n; ++k)

            // At 0 it is free
            dp[i, 0, k] = 0;

        // Package not available for
        // desirable amount of sweets
        for (int k = 1; k <= n; ++k)
            dp[i, k, 0] = -1;
    }

    for (int i = 0; i <= m; ++i)
    {
        for (int j = 1; j <= n; ++j)
        {
            for (int k = 1; k <= n; ++k)
            {

                dp[i, j, k] = -1;

                // Buying the 'k' kg package and
                // assigning it to dp array
                if (i > 0 && j >= k && sweet[k] > 0 &&
                    dp[i - 1, j - k, k] != -1)

                    dp[i, j, k] = dp[i - 1, j - k, k] +
                                             sweet[k];

                // If no solution, select from
                // previous k-1 packages
                if (dp[i, j, k] == -1 ||
                   (dp[i, j, k - 1] != -1 &&
                    dp[i, j, k] > dp[i, j, k - 1]))

                    dp[i, j, k] = dp[i, j, k - 1];
            }
        }
    }

    // If solution does not exist
    if (dp[m, n, n] == -1)
        return 0;

    // Print the solution
    else
        return dp[m, n, n];
}

// Driver code
public static void Main()
{
    int m = 3;
    int[] adj = { 2, 1, 3, 0, 4, 10 };
    int n = adj.Length ;
    Console.Write(find(m, n, adj));
}
}

// This code is contributed
// by ChitraNayal
// C# program to minimum cost to buy
// N kilograms of sweet for M persons
using System;

class GFG
{

// Function to find the minimum
// cost of sweets
static int find(int m, int n,
                int[] adj)
{
    // Defining the sweet array
    int[] sweet = new int [n + 1] ;

    // DP array to store the values
    int[,,] dp = new int [n + 1, n + 1,
                                 n + 1];

    sweet[0] = 0;

    // Since index starts from 1 we
    // reassign the array into sweet
    for (int i = 1; i <= m; ++i)
        sweet[i] = adj[i - 1];

    // Assigning base cases
    // for dp array
    for (int i = 0; i <= m; ++i)
    {
        for (int k = 0; k <= n; ++k)

            // At 0 it is free
            dp[i, 0, k] = 0;

        // Package not available for
        // desirable amount of sweets
        for (int k = 1; k <= n; ++k)
            dp[i, k, 0] = -1;
    }

    for (int i = 0; i <= m; ++i)
    {
        for (int j = 1; j <= n; ++j)
        {
            for (int k = 1; k <= n; ++k)
            {

                dp[i, j, k] = -1;

                // Buying the 'k' kg package and
                // assigning it to dp array
                if (i > 0 && j >= k && sweet[k] > 0 &&
                    dp[i - 1, j - k, k] != -1)

                    dp[i, j, k] = dp[i - 1, j - k, k] +
                                             sweet[k];

                // If no solution, select from
                // previous k-1 packages
                if (dp[i, j, k] == -1 ||
                   (dp[i, j, k - 1] != -1 &&
                    dp[i, j, k] > dp[i, j, k - 1]))

                    dp[i, j, k] = dp[i, j, k - 1];
            }
        }
    }

    // If solution does not exist
    if (dp[m, n, n] == -1)
        return 0;

    // Print the solution
    else
        return dp[m, n, n];
}

// Driver code
public static void Main()
{
    int m = 3;
    int[] adj = { 2, 1, 3, 0, 4, 10 };
    int n = adj.Length ;
    Console.Write(find(m, n, adj));
}
}

// This code is contributed
// by ChitraNayal
```

## java 描述语言

```
<script>
// Javascript program to minimum cost to buy
// N kilograms of sweet for M persons

    // Function to find the minimum cost of sweets
    function find(m,n,adj)
    {
        // Defining the sweet array
        let sweet = new Array(n + 1) ;

        // DP array to store the values
        let dp = new Array(n + 1) ;
        for (let i = 0; i <n+1; ++i) {
            dp[i]=new Array(n+1);
            for (let j = 0; j <= n; ++j) {
                dp[i][j]=new Array(n+1);
                    for (let k = 0; k <= n; ++k) {

                        dp[i][j][k] = -1;
                      }
            }
        }
        sweet[0] = 0;

        // Since index starts from 1 we
        // reassign the array into sweet
        for (let i = 1; i <= m; ++i)
            sweet[i] = adj[i - 1];

        // Assigning base cases for dp array
        for (let i = 0; i <= m; ++i) {
            for (let k = 0; k <= n; ++k)

                // At 0 it is free
                dp[i][0][k] = 0;

            // Package not available for desirable amount of sweets
            for (let k = 1; k <= n; ++k)
                dp[i][k][0] = -1;
        }

        for (let i = 0; i <= m; ++i) {

            for (let j = 1; j <= n; ++j) {
                for (let k = 1; k <= n; ++k) {

                    dp[i][j][k] = -1;

                    // Buying the 'k' kg package and
                    // assigning it to dp array
                    if (i > 0 && j >= k && sweet[k] > 0
                        && dp[i - 1][j - k][k] != -1)

                        dp[i][j][k] = dp[i - 1][j - k][k] + sweet[k];

                    // If no solution, select from previous k-1 packages
                    if (dp[i][j][k] == -1 || (dp[i][j][k - 1] != -1
                                              && dp[i][j][k] > dp[i][j][k - 1]))

                        dp[i][j][k] = dp[i][j][k - 1];
                }
            }
        }

        // If solution does not exist
        if (dp[m][n][n] == -1)
            return 0;

        // Print the solution
        else
            return dp[m][n][n];
    }

    // Driver code
    let m = 3;
    let adj=[2, 1, 3, 0, 4, 10];
    let n = adj.length ;
    document.write( find(m, n, adj));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
3
```

上述算法的**时间复杂度**为 O(m*n*n)。