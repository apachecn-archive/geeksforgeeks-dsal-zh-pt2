# 计数长度为 K 的序列，每个项可被其前一项整除

> 原文:[https://www . geesforgeks . org/count-sequence-of-length-k-having-term-by-its-previous-term/](https://www.geeksforgeeks.org/count-sequences-of-length-k-having-each-term-divisible-by-its-preceding-term/)

给定两个整数 **N** 和 **K** ，任务是找到长度为 **K** 的序列数，该序列由范围**【1，N】**中的值组成，这样序列中的每一个 **(i + 1) <sup>第</sup>元素**都可以被它前面的 **i <sup>第</sup>元素**整除。

**示例:**

> **输入:** N = 3，K = 2
> **输出:** 5
> **解释:**
> 这 5 个序列是[1，1]，[2，2]，[3，3]，[1，2]，[1，3]
> 
> **输入:**N = 6k = 4
> T3】输出: 39

**方法:**
按照以下步骤解决问题:

1.  初始化一个矩阵 **fct[][]** ，将 **i** 的因子存储在行 **fct[i]** 中，我位于范围**【1，N】**内。
2.  初始化一个矩阵 **dp[][]** ，该矩阵在 **dp[i][j]** 存储以 **j** 结束的长度为 **i** 的序列数。
3.  如果**I<sup>th</sup>T3】指数有 **j** 、**(I–1)<sup>th</sup>**指数应该由**因子(j)** 组成。同样地，**(I–2)<sup>第</sup>** 个指数应该由一个**因子(因子(j)】**组成。**
4.  因此， **dp[i][j]** 应该由以因子 j 结束的(I–1)长度的所有可能序列组成。
5.  因此， **dp[i][j]** 等于所有可能的**DP[I–1][FCT[j][k]]**之和，其中**DP[I–1][FCT[j][k]]**表示长度为**I–1**的总序列数，以 **k <sup>为 j</sup>** 的第因子结束。
6.  最后，从 **1 < =j < =N** 中找出所有**DP【K】【j】**的和，并返回和。

下面是上述方法的实现:

## C++14

```
// C++ Program to implement the
// above approach

#include <bits/stdc++.h>
using namespace std;

#define ll long long

// Stores the factors of i-th
// element in v[i]
vector<ll int> vp[2009];

// Function to find all the
// factors of N
void finding_factors(ll int n)
{
    ll int i, a;

    // Iterate upto sqrt(N)
    for (i = 1; i * i <= n; i++) {

        if (n % i == 0) {

            if (i * i == n) {
                vp[n].push_back(i);
            }

            else {
                vp[n].push_back(i);
                vp[n].push_back(n / i);
            }
        }
    }
}

// Function to return the count of
// sequences of length K having
// all terms divisible by its
// preceding term
ll int countSeq(ll int N, ll int K)
{
    ll int i, j, k;

    ll int dp[109][109] = { 0 };

    for (i = 1; i <= N; i++) {

        // Calculate factors of i
        finding_factors(i);

        // Initialize dp[0][i] = 0: No
        // subsequence of length 0 ending
        // with i-th element exists
        dp[0][i] = 0;

        // Initialize dp[0][i] = 1: Only 1
        // subsequence of length 1 ending
        // with i-th element exists
        dp[1][i] = 1;
    }

    // Iterate [2, K] to obtain sequences
    // of each length
    for (i = 2; i <= K; i++) {

        for (j = 1; j <= N; j++) {

            // Calculate sum of
            // all dp[i-1][vp[j][k]]

            ll int sum = 0;

            for (k = 0; k < vp[j].size(); k++) {

                // vp[j][k] stores all factors
                // of j
                sum = (sum + dp[i - 1][vp[j][k]]);
            }

            // Store the sum in A[i][j]
            dp[i][j] = sum;
        }
    }

    ll int ans = 0;
    for (j = 1; j <= N; j++) {

        // Sum of all dp[K][j] obtain all
        // K length sequences ending with j
        ans = (ans + dp[K][j]);
    }
    return ans;
}

// Driver code
int main()
{

    ll int N, K;
    N = 3;
    K = 2;

    cout << countSeq(N, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.util.*;

class GFG{

// Stores the factors of i-th
// element in v[i]
@SuppressWarnings("unchecked")
static Vector<Integer> []vp = new Vector[2009];

// Function to find all the
// factors of N
static void finding_factors(int n)
{
    int i, a;

    // Iterate upto Math.sqrt(N)
    for(i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {
            if (i * i == n)
            {
                vp[n].add(i);
            }
            else
            {
                vp[n].add(i);
                vp[n].add(n / i);
            }
        }
    }
}

// Function to return the count of
// sequences of length K having
// aint terms divisible by its
// preceding term
static int countSeq(int N, int K)
{
    int i, j, k;

    int dp[][] = new int[109][109];

    for(i = 1; i <= N; i++)
    {

        // Calculate factors of i
        finding_factors(i);

        // Initialize dp[0][i] = 0: No
        // subsequence of length 0 ending
        // with i-th element exists
        dp[0][i] = 0;

        // Initialize dp[0][i] = 1: Only 1
        // subsequence of length 1 ending
        // with i-th element exists
        dp[1][i] = 1;
    }

    // Iterate [2, K] to obtain sequences
    // of each length
    for(i = 2; i <= K; i++)
    {
        for(j = 1; j <= N; j++)
        {

            // Calculate sum of
            // aint dp[i-1][vp[j][k]]
            int sum = 0;

            for(k = 0; k < vp[j].size(); k++)
            {

                // vp[j][k] stores aint factors
                // of j
                sum = (sum + dp[i - 1][vp[j].get(k)]);
            }

            // Store the sum in A[i][j]
            dp[i][j] = sum;
        }
    }

    int ans = 0;
    for(j = 1; j <= N; j++)
    {

        // Sum of aint dp[K][j] obtain all
        // K length sequences ending with j
        ans = (ans + dp[K][j]);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int N, K;
    N = 3;
    K = 2;

    for(int i = 0; i < vp.length; i++)
        vp[i] = new Vector<Integer>();

    System.out.print(countSeq(N, K) + "\n");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

# Stores the factors of i-th
# element in v[i]
vp = [[] for i in range(2009)]

# Function to find all the
# factors of N
def finding_factors(n):

    i = 1
    a = 0

    global vp

    # Iterate upto sqrt(N)
    while (i * i <= n):
        if (n % i == 0):
            if (i * i == n):
                vp[n].append(i)
            else:
                vp[n].append(i)
                vp[n].append(int(n / i))

        i += 1

# Function to return the count of
# sequences of length K having
# all terms divisible by its
# preceding term
def countSeq(N, K):

    i = 0
    j = 0
    k = 0

    dp = [[0 for i in range(109)]
             for j in range(109)]

    for i in range(1, N + 1):

        # Calculate factors of i
        finding_factors(i)

        # Initialize dp[0][i] = 0: No
        # subsequence of length 0 ending
        # with i-th element exists
        dp[0][i] = 0

        # Initialize dp[0][i] = 1: Only 1
        # subsequence of length 1 ending
        # with i-th element exists
        dp[1][i] = 1

    # Iterate [2, K] to obtain sequences
    # of each length
    for i in range(2, K + 1):
        for j in range(1, N + 1):

            # Calculate sum of
            # all dp[i-1][vp[j][k]]
            Sum = 0

            for k in range(len(vp[j])):

                # vp[j][k] stores all factors
                # of j
                Sum += dp[i - 1][vp[j][k]]

            # Store the sum in A[i][j]
            dp[i][j] = Sum

    ans = 0
    for j in range(1, N + 1):

        # Sum of all dp[K][j] obtain all
        # K length sequences ending with j
        ans += dp[K][j]

    return ans

# Driver code
N = 3
K = 2

print(countSeq(N, K))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to implement the
// above approach
using System;
using System.Collections.Generic;

class GFG{

// Stores the factors of i-th
// element in v[i]
static List<int> []vp = new List<int>[2009];

// Function to find all the
// factors of N
static void finding_factors(int n)
{
    int i ;

    // Iterate upto Math.Sqrt(N)
    for(i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {
            if (i * i == n)
            {
                vp[n].Add(i);
            }
            else
            {
                vp[n].Add(i);
                vp[n].Add(n / i);
            }
        }
    }
}

// Function to return the count of
// sequences of length K having
// aint terms divisible by its
// preceding term
static int countSeq(int N, int K)
{
    int i, j, k;

    int [,]dp = new int[109, 109];

    for(i = 1; i <= N; i++)
    {

        // Calculate factors of i
        finding_factors(i);

        // Initialize dp[0,i] = 0: No
        // subsequence of length 0 ending
        // with i-th element exists
        dp[0, i] = 0;

        // Initialize dp[0,i] = 1: Only 1
        // subsequence of length 1 ending
        // with i-th element exists
        dp[1, i] = 1;
    }

    // Iterate [2, K] to obtain sequences
    // of each length
    for(i = 2; i <= K; i++)
    {
        for(j = 1; j <= N; j++)
        {

            // Calculate sum of
            // aint dp[i-1,vp[j,k]]
            int sum = 0;

            for(k = 0; k < vp[j].Count; k++)
            {

                // vp[j,k] stores aint factors
                // of j
                sum = (sum + dp[i - 1, vp[j][k]]);
            }

            // Store the sum in A[i,j]
            dp[i,j] = sum;
        }
    }

    int ans = 0;
    for(j = 1; j <= N; j++)
    {

        // Sum of aint dp[K,j] obtain all
        // K length sequences ending with j
        ans = (ans + dp[K, j]);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int N, K;
    N = 3;
    K = 2;

    for(int i = 0; i < vp.Length; i++)
        vp[i] = new List<int>();

    Console.Write(countSeq(N, K) + "\n");
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript program to implement the
// above approach

// Stores the factors of i-th
// element in v[i]
let vp =  new Array(2009);

// Function to find all the
// factors of N
function finding_factors(n)
{
    let i, a;

    // Iterate upto Math.sqrt(N)
    for(i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {
            if (i * i == n)
            {
                vp[n].push(i);
            }
            else
            {
                vp[n].push(i);
                vp[n].push(n / i);
            }
        }
    }
}

// Function to return the count of
// sequences of length K having
// alet terms divisible by its
// preceding term
function countSeq(N, K)
{
    let i, j, k;

    let dp = new Array(109);
    // Loop to create 2D array using 1D array
    for (let i = 0; i < dp.length; i++) {
        dp[i] = new Array(2);
    }   

    for(i = 1; i <= N; i++)
    {

        // Calculate factors of i
        finding_factors(i);

        // Initialize dp[0][i] = 0: No
        // subsequence of length 0 ending
        // with i-th element exists
        dp[0][i] = 0;

        // Initialize dp[0][i] = 1: Only 1
        // subsequence of length 1 ending
        // with i-th element exists
        dp[1][i] = 1;
    }

    // Iterate [2, K] to obtain sequences
    // of each length
    for(i = 2; i <= K; i++)
    {
        for(j = 1; j <= N; j++)
        {

            // Calculate sum of
            // alet dp[i-1][vp[j][k]]
            let sum = 0;

            for(k = 0; k < vp[j].length; k++)
            {

                // vp[j][k] stores alet factors
                // of j
                sum = (sum + dp[i - 1][vp[j][k]]);
            }

            // Store the sum in A[i][j]
            dp[i][j] = sum;
        }
    }

    let ans = 0;
    for(j = 1; j <= N; j++)
    {

        // Sum of alet dp[K][j] obtain all
        // K length sequences ending with j
        ans = (ans + dp[K][j]);
    }
    return ans;
}
// Driver Code

    let N, K;
    N = 3;
    K = 2;

    for(let i = 0; i < vp.length; i++)
        vp[i] = [];

    document.write(countSeq(N, K) + "\n");

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(K * N<sup>3/2</sup>)*
***辅助空间:** O (N <sup>2</sup> )*