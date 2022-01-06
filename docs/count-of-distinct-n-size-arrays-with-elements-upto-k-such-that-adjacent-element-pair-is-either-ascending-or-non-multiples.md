# 元素数量最多为 K 的不同的 N 尺寸阵列的计数，使得相邻的元素对要么是升序要么是非倍数

> 原文:[https://www . geesforgeks . org/count-of-distinct-n-size-array-of-elements-up-k-so-neighbor-element-pair-or-non-multiples/](https://www.geeksforgeeks.org/count-of-distinct-n-size-arrays-with-elements-upto-k-such-that-adjacent-element-pair-is-either-ascending-or-non-multiples/)

给定两个整数 **N** 和 **K** ，找出不同的方法来创建一个 **N** 元素的数组，其中每个元素都在**【1，K】**的范围内，并且每对相邻的元素(P，Q)要么是 **P < = Q** 要么是 **P % Q > 0** 。

**示例:**

> **输入:** N = 2，K = 3
> **输出:** 7
> **解释:**满足给定条件的数组为{1，1}、{1，2}、{1，3}、{2，2}、{2，3}、{3，3}、{3，2}。
> 
> **输入:** N = 9，K = 1
> **输出:** 1
> **解释:**:唯一满足给定条件的数组是{1，1，1，1，1，1，1，1，1}。

**方法:**给定的问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)基于以下观察来解决:

*   考虑一个 2D 数组，比如说 **dp[][]** ，其中 **dp[x][y]** 表示长度为 **x** 的数组的计数，其中 **y** 是它们的最后一个元素。
*   现在，创建长度为 **x** 的数组的方法的数量是创建长度为**(y–1)**的数组的方法的总和，其中 **y** 是它们的最后一个元素，并且所有数组元素都在范围**【1，K】**内，并且可以表示为关系![dp[x][y] = \sum_{j=1}^{j = k} dp[x-1][j]                  ](img/6014c4631a5f63c6039c9f0ad3c27767.png "Rendered by QuickLaTeX.com")。
*   只有 **P < = Q** 或 **P % Q > 0** 的情况才被考虑，其中(P，Q)是相邻元素对。不满足这两个条件的数组可以使用关系![dp[x][y] = \sum_{j=1}^{j = k} dp[x-1][j]                  ](img/6014c4631a5f63c6039c9f0ad3c27767.png "Rendered by QuickLaTeX.com")从每个状态中减去，其中 **y % j = 0** 。

根据以上观察，计算 [dp[][]表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)并打印 **dp[N][K]** 的值作为形成的数组的结果计数。按照以下步骤解决给定的问题:

*   使用厄拉多塞的[筛中的方法，将所有整数](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)在范围**【1，K】**内的所有除数存储在一个数组中，比如说**除数[][]** 。
*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如说维度 **(N + 1)*(K + 1)** 的 **dp[][]** ，使得 **dp[x][y]** 代表长度为 **x** 的数组的计数，其中 **y** 是它们的最后一个元素。
*   将 **dp[1][j]** 初始化为 **1** 作为创建大小为 **1** 的数组的方法数，将任意元素 **j** 作为它们的最后一个元素是 **1** 。
*   [使用变量 **x** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【2，N】**，并执行以下步骤:
    *   对于范围**【1，K】**内 **j** 的每个可能值，将**DP【x】【y】**的值增加**DP【x–1】【j】**。
    *   [使用 **y** 的值迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，K】**，对于每个除数，**表示 **y** 的 D** 将 **dp[x][y]** 的值减少**DP[x–1][D]**，因为这不能满足 **P < = Q** 或**P % Q>0**的情况****
*   完成上述步骤后，打印![ \sum_{j=1}^{j = k} dp[N][j]                  ](img/21209efbd0612e1033d65bfb506343c9.png "Rendered by QuickLaTeX.com")的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of distinct
// arrays of size n having elements in
// range [1, k] and all adjacent elements
// (P, Q) follows (P <= Q) or (P % Q > 0)
int countArrays(int n, int k)
{
    // Stores the divisors of all
    // integers in the range [1, k]
    vector<vector<int> > divisors(k + 1);

    // Calculate the divisors of all
    // integers using the Sieve
    for (int i = 1; i <= k; i++) {
        for (int j = 2 * i; j <= k; j += i) {
            divisors[j].push_back(i);
        }
    }

    // Stores the dp states such that
    // dp[i][j] with i elements having
    // j as the last element of array
    vector<vector<int> > dp(
        n + 1, vector<int>(k + 1));

    // Initialize the dp array
    for (int j = 1; j <= k; j++) {
        dp[1][j] = 1;
    }

    // Calculate the dp states using the
    // derived relation
    for (int x = 2; x <= n; x++) {

        // Calculate the sum for len-1
        int sum = 0;
        for (int j = 1; j <= k; j++) {
            sum += dp[x - 1][j];
        }

        // Subtract dp[len-1][j] for each
        // factor of j from [1, K]
        for (int y = 1; y <= k; y++) {
            dp[x][y] = sum;
            for (int d : divisors[y]) {
                dp[x][y] = (dp[x][y] - dp[x - 1][d]);
            }
        }
    }

    // Calculate the final result
    int sum = 0;
    for (int j = 1; j <= k; j++) {
        sum += dp[n][j];
    }

    // Return the resultant sum
    return sum;
}

// Driver Code
int main()
{
    int N = 2, K = 3;
    cout << countArrays(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach

import java.util.*;

class GFG{

// Function to find the count of distinct
// arrays of size n having elements in
// range [1, k] and all adjacent elements
// (P, Q) follows (P <= Q) or (P % Q > 0)
static int countArrays(int n, int k)
{
    // Stores the divisors of all
    // integers in the range [1, k]
    Vector<Integer> []divisors = new Vector[k + 1];
    for (int i = 0; i < divisors.length; i++)
        divisors[i] = new Vector<Integer>();

    // Calculate the divisors of all
    // integers using the Sieve
    for (int i = 1; i <= k; i++) {
        for (int j = 2 * i; j <= k; j += i) {
            divisors[j].add(i);
        }
    }

    // Stores the dp states such that
    // dp[i][j] with i elements having
    // j as the last element of array
    int [][] dp = new int[n + 1][k + 1];

    // Initialize the dp array
    for (int j = 1; j <= k; j++) {
        dp[1][j] = 1;
    }

    // Calculate the dp states using the
    // derived relation
    for (int x = 2; x <= n; x++) {

        // Calculate the sum for len-1
        int sum = 0;
        for (int j = 1; j <= k; j++) {
            sum += dp[x - 1][j];
        }

        // Subtract dp[len-1][j] for each
        // factor of j from [1, K]
        for (int y = 1; y <= k; y++) {
            dp[x][y] = sum;
            for (int d : divisors[y]) {
                dp[x][y] = (dp[x][y] - dp[x - 1][d]);
            }
        }
    }

    // Calculate the final result
    int sum = 0;
    for (int j = 1; j <= k; j++) {
        sum += dp[n][j];
    }

    // Return the resultant sum
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int N = 2, K = 3;
    System.out.print(countArrays(N, K));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function to find the count of distinct
# arrays of size n having elements in
# range [1, k] and all adjacent elements
# (P, Q) follows (P <= Q) or (P % Q > 0)
def countArrays(n, k):

    # Stores the divisors of all
    # integers in the range [1, k]
    divisors = [[] for i in range(k + 1)]

    # Calculate the divisors of all
    # integers using the Sieve
    for i in range(1, k + 1, 1):
        for j in range(2 * i, k + 1, i):
            divisors[j].append(i)

    # Stores the dp states such that
    # dp[i][j] with i elements having
    # j as the last element of array
    dp = [[0 for i in range(k+1)] for j in range(n + 1)]

    # Initialize the dp array
    for j in range(1, k + 1, 1):
        dp[1][j] = 1

    # Calculate the dp states using the
    # derived relation
    for x in range(2, n + 1, 1):
        # Calculate the sum for len-1
        sum = 0
        for j in range(1, k + 1, 1):
            sum += dp[x - 1][j]

        # Subtract dp[len-1][j] for each
        # factor of j from [1, K]
        for y in range(1, k + 1, 1):
            dp[x][y] = sum
            for d in divisors[y]:
                dp[x][y] = (dp[x][y] - dp[x - 1][d])

    # Calculate the final result
    sum = 0
    for j in range(1, k + 1, 1):
        sum += dp[n][j]

    # Return the resultant sum
    return sum

# Driver Code
if __name__ == '__main__':
    N = 2
    K = 3
    print(countArrays(N, K))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the approach
using System;
using System.Collections.Generic;

class GFG {

// Function to find the count of distinct
// arrays of size n having elements in
// range [1, k] and all adjacent elements
// (P, Q) follows (P <= Q) or (P % Q > 0)
static int countArrays(int n, int k)
{
    // Stores the divisors of all
    // integers in the range [1, k]
    List<int> []divisors = new List<int>[k + 1];

    for (int i = 0; i < divisors.Length; i++)
        divisors[i] = new List<int>();

    // Calculate the divisors of all
    // integers using the Sieve
    for (int i = 1; i <= k; i++) {
        for (int j = 2 * i; j <= k; j += i) {
            divisors[j].Add(i);
        }
    }

    // Stores the dp states such that
    // dp[i][j] with i elements having
    // j as the last element of array
    int [,] dp = new int[n + 1, k + 1];

    // Initialize the dp array
    for (int j = 1; j <= k; j++) {
        dp[1, j] = 1;
    }

    int sum;

    // Calculate the dp states using the
    // derived relation
    for (int x = 2; x <= n; x++) {

        // Calculate the sum for len-1
        sum = 0;
        for (int j = 1; j <= k; j++) {
            sum += dp[x - 1, j];
        }

        // Subtract dp[len-1][j] for each
        // factor of j from [1, K]
        for (int y = 1; y <= k; y++) {
            dp[x, y] = sum;
            foreach (int d in divisors[y]) {
                dp[x, y] = (dp[x, y] - dp[x - 1, d]);
            }
        }
    }

    // Calculate the final result
    sum = 0;
    for (int j = 1; j <= k; j++) {
        sum += dp[n, j];
    }

    // Return the resultant sum
    return sum;
}

    // Driver Code
    public static void Main()
    {
        int N = 2, K = 3;
        Console.Write(countArrays(N, K));
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the count of distinct
        // arrays of size n having elements in
        // range [1, k] and all adjacent elements
        // (P, Q) follows (P <= Q) or (P % Q > 0)
        function countArrays(n, k)
        {

            // Stores the divisors of all
            // integers in the range [1, k]
            let divisors = new Array(k + 1).fill(new Array());

            // Calculate the divisors of all
            // integers using the Sieve
            for (let i = 1; i <= k; i++) {
                for (let j = 2 * i; j <= k; j += i) {
                    divisors[j].push(i);
                }
            }

            // Stores the dp states such that
            // dp[i][j] with i elements having
            // j as the last element of array
            let dp = new Array(n + 1).fill(new Array(k + 1));

            // Initialize the dp array
            for (let j = 1; j <= k; j++) {
                dp[1][j] = 1;
            }

            // Calculate the dp states using the
            // derived relation
            for (let x = 2; x <= n; x++) {

                // Calculate the sum for len-1
                let sum = 0;
                for (let j = 1; j <= k; j++) {
                    sum += dp[x - 1][j];
                }

                // Subtract dp[len-1][j] for each
                // factor of j from [1, K]
                for (let y = 1; y <= k; y++) {
                    dp[x][y] = sum;
                    for (let d of divisors[y]) {
                        dp[x][y] = (dp[x][y] - dp[x - 1][d]);
                    }
                }
            }

            // Calculate the final result
            let sum = 0;
            for (let j = 1; j <= k; j++) {
                sum += dp[n][j];
            }
            sum++;

            // Return the resultant sum
            return sum;
        }

        // Driver Code
        let N = 2, K = 3;
        document.write(countArrays(N, K));

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
7
```

***时间复杂度:**O(N * K * log K)*
T5**辅助空间:** O(K*log K)