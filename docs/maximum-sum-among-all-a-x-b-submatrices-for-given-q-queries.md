# 给定 Q 个查询的所有(a×b)子矩阵的最大和

> 原文:[https://www . geeksforgeeks . org/a-x-b-给定 q-查询的最大总和/](https://www.geeksforgeeks.org/maximum-sum-among-all-a-x-b-submatrices-for-given-q-queries/)

给定一个大小为 **N x M** 的[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **mat[][]** 和一个大小为 **Q 的[数组**查询[]** ，包含 **(a，b)**](https://www.geeksforgeeks.org/array-data-structure/) [对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)。任务是找到[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**mat【】【】**的所有 **(a x b)** 子矩阵中的最大和。**

> **注意:**子矩阵的行和列必须是连续的。

**示例:**

> **输入:** N = 3，M = 4，Q = 1，查询[] = {(3，2)}
> mat[][] = {{1，2，3，9}，
> {4，5，6，2}，
> {8，3，2，6 } }
> 
> T7】输出: 28
> **解释** :
> 这里 a = 3 和 b = 2
> 第一个 3×2 子矩阵是
> 第二个 3×2 子矩阵为:
> 2 3
> 5 6
> 3 2
> 此处元素之和为 21。
> 第三个 3×2 子矩阵为:
> 3 9
> 6 2
> 2 6
> 此处元素之和为 28。
> 其中最大值为 28。
> 
> **输入** : N = 3，M = 4，Q = 3，查询[] = {(1，1)，(2，2)，(3，3)}
> mat[][] = {{1，2，3，9}，
> {4，5，6，2}，
> {8，3，2，6}}
> 
> **输出** : 9 20 38

**天真法:**解决这个问题最简单的方法就是对于每个查询，求每个子矩阵的和，打印最大的一个。

***时间复杂度:** O(Q*(N*M)^2)，其中 **Q** 为查询数， **N** 和 **M** 为矩阵 **mat【】【】的行数和列数。***
***辅助空间:** O(1)*

**高效途径:**这个问题可以通过在回答所有查询之前做一些[的预处理来解决。按照以下步骤解决此问题:](https://www.geeksforgeeks.org/submatrix-sum-queries/)

*   声明一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、 **dp** ，其中**DP【I】【j】**存储从 **(0，0)** 到 **(i，j)的元素之和。**
*   对输入 **mat[][]做一些预处理。**声明一个函数说，**预处理(mat，dp，n，m)**做以下步骤:
    *   [使用变量 **i** 和**T7】在范围**](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，m-1】**中迭代，将**DP【0】【I】**更新为**mat【0】【I】。**
    *   [使用变量 **i** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，n-1】**中迭代
        *   [使用变量 **j:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，m-1】**中迭代
            *   将 **dp[i][j]** 更新为 **dp[i-1][j] + mat[i][j]。**
    *   [使用变量 **i** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，n-1】**中迭代
        *   [使用变量 **j:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，m-1】**中迭代
            *   将 **dp[i][j]** 更新为 **dp[i][j] + dp[i][j-1]。**
*   声明一个[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **maxSum** 来存储每个查询的答案。
*   声明一个函数说， **sumQuery(dp，tli，tlj，rbi，rbj)**其中 **tli** 和 **tlj** 分别是查询子矩阵左上的行号和列号， **rbi** 和 **rbj** 是查询子矩阵右下的行号和列号，计算子矩阵在 **O(1)** 时间内的和。
    *   将变量 **res** 初始化为**DP【RBI】【rbj】**来存储子矩阵的和。
    *   如果**T1**I 大于 **0** ，则移除 **(0，0)** 和 **(tli-1，rbj)** 之间的元素。
    *   如果 **tlj** 大于 **0，**则移除(0，0)和(rbi，tlj-1)之间的元素。
    *   如果 **tli** 大于 **0** 并且 **tlj** 大于 **0，**则添加**DP【tli-1】【tlj-1】**作为 **(0，0)** 和 **(tli-1，tlj-1)** 之间的元素减去两次。
*   [使用变量 **qi** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，q-1】**中迭代
    *   [使用变量 **i:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，n-查询【qi】【0】】**中迭代
        *   [使用变量 **j** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，m-查询【qi】【1】】**中迭代
            *   将 **maxSum[qi]** 更新为 **maxSum[qi]** 和 **sumQuery(dp，I，j，i +查询[qi][0]–1，j +查询[qi][1]–1)的最大值。**
*   完成以上步骤后，打印[数组](https://www.geeksforgeeks.org/array-data-structure/) **maxSum** 作为每个查询的答案。

**参考:**T2】https://www.geeksforgeeks.org/submatrix-sum-queries/

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to preprcess input mat[N][M].
// This function mainly fills dp[N][M]
// such that dp[i][j] stores sum
// of elements from (0, 0) to (i, j)
void preProcess(vector<vector<int>> &mat,
                vector<vector<int>> &dp,
                              int n, int m)
{

    // Copy first row of mat[][] to dp[][]
    for(int i = 0; i < m; i++)
    {
        dp[0][i] = mat[0][i];
    }

    // Do column wise sum
    for(int i = 1; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {
            dp[i][j] = dp[i - 1][j] + mat[i][j];
        }
    }

    // Do row wise sum
    for(int i = 0; i < n; i++)
    {
        for(int j = 1; j < m; j++)
        {
            dp[i][j] += dp[i][j - 1];
        }
    }
}

// A O(1) time function to compute sum of submatrix
// between (tli, tlj) and (rbi, rbj) using dp[][]
// which is built by the preprocess function
int sumQuery(vector<vector<int>> dp, int tli,
             int tlj, int rbi, int rbj)
{

    // Result is now sum of elements
    // between (0, 0) and (rbi, rbj)
    int res = dp[rbi][rbj];

    // Remove elements between (0, 0)
    // and (tli-1, rbj)
    if (tli > 0)
        res = res - dp[tli - 1][rbj];

    // Remove elements between (0, 0)
    // and (rbi, tlj-1)
    if (tlj > 0)
        res = res - dp[rbi][tlj - 1];

    // Add dp[tli-1][tlj-1] as elements
    // between (0, 0) and (tli-1, tlj-1)
    // are subtracted twice
    if (tli > 0 && tlj > 0)
        res = res + dp[tli - 1][tlj - 1];

    return res;
}

// Function to find the maximum sum
// among all (a x b) sub-matrices of the matrix
vector<int> maxSubMatrixSumQueries(vector<vector<int>> mat,
                                   int n, int m,
                                   vector<vector<int>> queries,
                                   int q)
{
    vector<vector<int> > dp(n, vector<int>(m));

    // Function call
    preProcess(mat, dp, n, m);

    vector<int> maxSum((int)queries.size());

    // Run a loop for finding
    // answer for all queries
    for(int qi = 0; qi < q; qi++)
    {
        for(int i = 0; i < n - queries[qi][0] + 1; i++)
        {
            for(int j = 0; j < m - queries[qi][1] + 1; j++)
            {
                maxSum[qi] = max(maxSum[qi],
                                 sumQuery(dp, i, j,
                                          i + queries[qi][0] - 1,
                                          j + queries[qi][1] - 1));
            }
        }
    }
    return maxSum;
}

// Driver Code
int main()
{

    // Given input
    int n = 3, m = 4;
    vector<vector<int> > mat = { { 1, 2, 3, 9 },
                                 { 4, 5, 6, 2 },
                                 { 8, 3, 2, 6 } };

    int Q = 3;
    vector<vector<int> >Queries = { { 1, 1 },
                                    { 2, 2 },
                                    { 3, 3 } };

    // Function call
    vector<int> maxSum = maxSubMatrixSumQueries(
          mat, n, m, Queries, Q);

    // Print answer for all queries
    for(int i = 0; i < Q; i++)
    {
        cout << maxSum[i] << " ";
    }
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class Solution {

    // Function to preprcess input mat[N][M].
    // This function mainly fills dp[N][M]
    // such that dp[i][j] stores sum
    // of elements from (0, 0) to (i, j)
    static void preProcess(int mat[][], int dp[][],
                           int n, int m)
    {

        // Copy first row of mat[][] to dp[][]
        for (int i = 0; i < m; i++) {

            dp[0][i] = mat[0][i];
        }

        // Do column wise sum
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < m; j++) {

                dp[i][j] = dp[i - 1][j] + mat[i][j];
            }
        }

        // Do row wise sum
        for (int i = 0; i < n; i++) {
            for (int j = 1; j < m; j++) {

                dp[i][j] += dp[i][j - 1];
            }
        }
    }

    // A O(1) time function to compute sum of submatrix
    // between (tli, tlj) and (rbi, rbj) using dp[][]
    // which is built by the preprocess function
    static int sumQuery(int dp[][], int tli,
                        int tlj, int rbi,
                        int rbj)
    {

        // Result is now sum of elements
        // between (0, 0) and (rbi, rbj)
        int res = dp[rbi][rbj];

        // Remove elements between (0, 0)
        // and (tli-1, rbj)
        if (tli > 0)
            res = res - dp[tli - 1][rbj];

        // Remove elements between (0, 0)
        // and (rbi, tlj-1)
        if (tlj > 0)
            res = res - dp[rbi][tlj - 1];

        // Add dp[tli-1][tlj-1] as elements
        // between (0, 0) and (tli-1, tlj-1)
        // are subtracted twice
        if (tli > 0 && tlj > 0)
            res
                = res + dp[tli - 1][tlj - 1];

        return res;
    }

    // Function to find the maximum sum
    // among all (a x b) sub-matrices of the matrix
    static int[] maxSubMatrixSumQueries(
        int[][] mat,
        int n, int m,
        int[][] queries,
        int q)
    {

        int dp[][] = new int[n][m];

        // Function call
        preProcess(mat, dp, n, m);

        int maxSum[] = new int[queries.length];

        // Run a loop for finding
        // answer for all queries
        for (int qi = 0; qi < q; qi++) {

            for (int i = 0; i < n - queries[qi][0] + 1; i++) {
                for (int j = 0; j < m - queries[qi][1] + 1; j++) {
                    maxSum[qi]
                        = Math.max(maxSum[qi],
                                   sumQuery(dp, i, j,
                                            i + queries[qi][0] - 1,
                                            j + queries[qi][1] - 1));
                }
            }
        }

        return maxSum;
    }

    // Driver Code
    public static void main(String args[])
    {

        // Given input
        int n = 3, m = 4;
        int mat[][] = { { 1, 2, 3, 9 },
                        { 4, 5, 6, 2 },
                        { 8, 3, 2, 6 } };

        int Q = 3;
        int Queries[][] = { { 1, 1 },
                            { 2, 2 },
                            { 3, 3 } };

        // Function call
        int maxSum[]
            = maxSubMatrixSumQueries(
                mat, n, m, Queries, Q);

        // Print answer for all queries
        for (int i = 0; i < Q; i++) {
            System.out.print(maxSum[i] + " ");
        }
    }
}
```

## C#

```
using System;

public class GFG{

    // Function to preprcess input mat[N][M].
    // This function mainly fills dp[N][M]
    // such that dp[i][j] stores sum
    // of elements from (0, 0) to (i, j)
    static void preProcess(int[,] mat, int[,] dp,
                           int n, int m)
    {

        // Copy first row of mat[][] to dp[][]
        for (int i = 0; i < m; i++) {

            dp[0,i] = mat[0,i];
        }

        // Do column wise sum
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < m; j++) {

                dp[i,j] = dp[i - 1,j] + mat[i,j];
            }
        }

        // Do row wise sum
        for (int i = 0; i < n; i++) {
            for (int j = 1; j < m; j++) {

                dp[i,j] += dp[i,j - 1];
            }
        }
    }

    // A O(1) time function to compute sum of submatrix
    // between (tli, tlj) and (rbi, rbj) using dp[][]
    // which is built by the preprocess function
    static int sumQuery(int[,] dp, int tli,
                        int tlj, int rbi,
                        int rbj)
    {

        // Result is now sum of elements
        // between (0, 0) and (rbi, rbj)
        int res = dp[rbi,rbj];

        // Remove elements between (0, 0)
        // and (tli-1, rbj)
        if (tli > 0)
            res = res - dp[tli - 1,rbj];

        // Remove elements between (0, 0)
        // and (rbi, tlj-1)
        if (tlj > 0)
            res = res - dp[rbi,tlj - 1];

        // Add dp[tli-1][tlj-1] as elements
        // between (0, 0) and (tli-1, tlj-1)
        // are subtracted twice
        if (tli > 0 && tlj > 0)
            res
                = res + dp[tli - 1,tlj - 1];

        return res;
    }

    // Function to find the maximum sum
    // among all (a x b) sub-matrices of the matrix
    static int[] maxSubMatrixSumQueries(
        int[,] mat,
        int n, int m,
        int[,] queries,
        int q)
    {

        int[,] dp = new int[n,m];

        // Function call
        preProcess(mat, dp, n, m);

        int[] maxSum = new int[queries.GetLength(0)];

        // Run a loop for finding
        // answer for all queries
        for (int qi = 0; qi < q; qi++) {

            for (int i = 0; i < n - queries[qi,0] + 1; i++) {
                for (int j = 0; j < m - queries[qi,1] + 1; j++) {
                    maxSum[qi]
                        = Math.Max(maxSum[qi],
                                   sumQuery(dp, i, j,
                                            i + queries[qi,0] - 1,
                                            j + queries[qi,1] - 1));
                }
            }
        }

        return maxSum;
    }

    // Driver Code

    static public void Main (){

         // Given input
        int n = 3, m = 4;
        int[,] mat = { { 1, 2, 3, 9 },
                        { 4, 5, 6, 2 },
                        { 8, 3, 2, 6 } };

        int Q = 3;
        int[,] Queries = { { 1, 1 },
                            { 2, 2 },
                            { 3, 3 } };

        // Function call
        int[] maxSum
            = maxSubMatrixSumQueries(
                mat, n, m, Queries, Q);

        // Print answer for all queries
        for (int i = 0; i < Q; i++) {
            Console.Write(maxSum[i] + " ");
        }

    }
}

// This code is contributed by patel2127.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to preprcess input mat[N][M].
// This function mainly fills dp[N][M]
// such that dp[i][j] stores sum
// of elements from (0, 0) to (i, j)
function preProcess(mat, dp, n, m)
{

    // Copy first row of mat[][] to dp[][]
    for(let i = 0; i < m; i++)
    {
        dp[0][i] = mat[0][i];
    }

    // Do column wise sum
    for(let i = 1; i < n; i++)
    {
        for(let j = 0; j < m; j++)
        {
            dp[i][j] = dp[i - 1][j] + mat[i][j];
        }
    }

    // Do row wise sum
    for(let i = 0; i < n; i++)
    {
        for(let j = 1; j < m; j++)
        {
            dp[i][j] += dp[i][j - 1];
        }
    }
}

// A O(1) time function to compute sum of submatrix
// between (tli, tlj) and (rbi, rbj) using dp[][]
// which is built by the preprocess function
function sumQuery(dp, tli, tlj, rbi, rbj)
{

    // Result is now sum of elements
    // between (0, 0) and (rbi, rbj)
    let res = dp[rbi][rbj];

    // Remove elements between (0, 0)
    // and (tli-1, rbj)
    if (tli > 0)
        res = res - dp[tli - 1][rbj];

    // Remove elements between (0, 0)
    // and (rbi, tlj-1)
    if (tlj > 0)
        res = res - dp[rbi][tlj - 1];

    // Add dp[tli-1][tlj-1] as elements
    // between (0, 0) and (tli-1, tlj-1)
    // are subtracted twice
    if (tli > 0 && tlj > 0)
        res = res + dp[tli - 1][tlj - 1];

    return res;
}

// Function to find the maximum sum
// among all (a x b) sub-matrices of the matrix
function maxSubMatrixSumQueries(mat, n, m, queries, q)
{
    let dp = Array(n).fill().map(() => Array(m));

    // Function call
    preProcess(mat, dp, n, m);

    let maxSum = new Array(queries.length).fill(0);

    // Run a loop for finding
    // answer for all queries
    for(let qi = 0; qi < q; qi++)
    {
        for(let i = 0; i < n - queries[qi][0] + 1; i++)
        {
            for(let j = 0; j < m - queries[qi][1] + 1; j++)
            {
                maxSum[qi] = Math.max(maxSum[qi],
                    sumQuery(dp, i, j,
                             i + queries[qi][0] - 1,
                             j + queries[qi][1] - 1));
            }
        }
    }
    return maxSum;
}

// Driver code

// Given input
let n = 3, m = 4;
let mat = [ [ 1, 2, 3, 9 ],
            [ 4, 5, 6, 2 ],
            [ 8, 3, 2, 6 ] ];

let Q = 3;
let Queries = [ [ 1, 1 ],
                [ 2, 2 ],
                [ 3, 3 ] ];

// Function call
let maxSum = maxSubMatrixSumQueries(
    mat, n, m, Queries, Q);

// Print answer for all queries
for(let i = 0; i < Q; i++)
{
    document.write(maxSum[i] + " ");
}

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
9 20 38 
```

***时间复杂度:** O(Q*N*M)，其中 Q 为查询数，N 和 M 为矩阵的行数和列数 **mat[][]。***
***辅助空间:** O(N*M)*