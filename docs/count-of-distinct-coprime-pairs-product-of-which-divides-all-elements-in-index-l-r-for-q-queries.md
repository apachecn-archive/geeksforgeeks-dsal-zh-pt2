# 不同互质对的计数，其乘积为 Q 查询的索引[L，R]中的所有元素除

> 原文:[https://www . geesforgeks . org/count-of-distinct-互素-pairs-product-of-division-in-index-l-r-for-q-query/](https://www.geeksforgeeks.org/count-of-distinct-coprime-pairs-product-of-which-divides-all-elements-in-index-l-r-for-q-queries/)

给定一个由 **N** 整数和 **Q** 查询组成的数组 **arr[]** ，形式为 **(l，r)** 。任务是为每个查询找到不同的互质整数对的数量，以便索引范围 **[l，r]** 中的所有整数都可以被互质整数的乘积整除。

***例:***

> ***输入:*** arr[] = {1，2，2，4，5}，查询[] = {{2，3}，{2，4}，{3，4}，{4，4}，{4，5}}
> ***输出:*** 3 3 3 5 1
> ***解释:*** 对于第一个查询[2，3]，子数组为{2，2}。
> 划分子阵列中所有整数的共矩阵对是{1，1}、{1，2}和{2，1}。
> 对于第二个查询[2，4]，子数组为{2，2，4}。
> 划分所有整数的共形对是{1，1}、{1，2}和{2，1}。
> 同样，继续进行进一步的查询。
> 
> **输入:** arr[] = {20，10，15}，查询[] = {{2，3}，{1，3}，{1，2}}
> **输出:** 3 3 9

**方法:**借助于[稀疏表](http://www.geeksforgeeks.org/sparse-table/)，可以最优地解决给定的问题。该方法基于这样的事实，即只有子阵列的 [GCD](http://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 的[主因子](http://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)可以划分其所有元素。因此，GCD 的主要因素有助于对的计数。可以使用稀疏表最佳地计算范围的 GCD。以下是要遵循的步骤:

*   创建一个[稀疏表](http://www.geeksforgeeks.org/sparse-table/)，在多个查询中以最佳时间找到范围**【L，R】**中的 GCD 元素。
*   遍历查询数组，并对每个查询执行以下操作:
    *   在当前查询的**【L，R】**范围内找到元素的 [GCD。](https://www.geeksforgeeks.org/gcds-of-a-given-index-ranges-in-an-array/)
    *   现在问题简化为寻找范围**【1，GCD】**中互质对的数量，它们的乘积为 **GCD** ，这可以使用这里[讨论的算法](https://www.geeksforgeeks.org/number-of-co-prime-pairs-from-1-to-n-with-product-equals-to-n/)来完成。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define MAXN 200001
int table[1001][1001];

// Function to build sparse table
void buildSparseTable(vector<int> arr, int n)
{
    // GCD of single element is
    // the element itself
    for (int i = 0; i < n; i++)
        table[i][0] = arr[i];

    // Build sparse table
    for (int j = 1; j <= log2(n); j++)
        for (int i = 0; i <= n - (1 << j);
             i++)
            table[i][j]
                = __gcd(table[i][j - 1],
                        table[i + (1 << (j - 1))][j - 1]);
}

// Fucntion to return the GCD of
// all elements in range [L, R]
int find_gcd(int L, int R)
{
    // Highest power of 2 that is not
    // more than count of elements
    int j = (int)log2(R - L + 1);

    // Return GCD in range
    return __gcd(table[L][j],
                 table[R - (1 << j) + 1][j]);
}

// Smallest prime factors array
int spf[MAXN];

// Function to build the smallest
// prime factor array using Sieve
void build_spf()
{
    spf[1] = 1;
    for (int i = 2; i < MAXN; i++)
        spf[i] = i;
    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (int i = 3; i * i < MAXN; i++) {
        if (spf[i] == i) {
            for (int j = i * i; j < MAXN;
                 j += i)
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to find the count of
// distinct prime factors of x
int getFactorization(int x)
{
    // Stores the required count
    int ctr = 0;

    while (x != 1) {
        ctr++;

        // Stores smallest prime
        // factor of x
        int p = spf[x];

        while (x % p == 0)
            x = x / p;
    }
    // Return count
    return ctr;
}
// Function to count of coprime pairs such
// that the product of the pair divides
// all integers of subarray in given range
void solveQueries(vector<int> a, int n,
                  vector<vector<int> > q)
{
    // Loop to iterate over queries
    for (int i = 0; i < q.size(); i++) {
        int l = q[i][0];
        int r = q[i][1];
        l--;
        r--;

        // Stores gcd in the range
        int gcd = find_gcd(l, r);

        // Stores the required count
        int ans = 0;

        // Count the pairs of co-primes
        // integers in given format
        for (int i = 1; i * i <= gcd; i++) {

            // If i is a factor of gcd
            if (gcd % i == 0) {
                ans = and + (1 << getFactorization(i));
                if (gcd / i != i)
                    ans += (1
                            << getFactorization(gcd / i));
            }
        }
        // Print answer
        cout << ans << " ";
    }
}

// Function to perform precomputation
void preProcess(vector<int> a, int n)
{
    build_spf();
    buildSparseTable(a, n);
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 2, 4, 5 };
    vector<vector<int> > queries = {
        { 2, 3 }, { 2, 4 }, { 3, 4 }, { 4, 4 }, { 4, 5 }
    };

    preProcess(arr, arr.size());
    solveQueries(arr, arr.size(), queries);

    return 0;
}
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
const MAXN = 200001;
let table = new Array(1001).fill(0).map(() =>
            new Array(1001).fill(0));

// Function to find gcd
const gcd = function(a, b)
{
    if (!b)
    {
        return a;
    }
    return gcd(b, a % b);
}

// Function to build sparse table
const buildSparseTable = (arr, n) => {

    // GCD of single element is
    // the element itself
    for(let i = 0; i < n; i++)
        table[i][0] = arr[i];

    // Build sparse table
    for(let j = 1; j <= parseInt(Math.log2(n)); j++)
        for(let i = 0; i <= n - (1 << j); i++)
            table[i][j]    = gcd(table[i][j - 1],
                              table[i + (1 << (j - 1))][j - 1]);
}

// Fucntion to return the GCD of
// all elements in range [L, R]
let find_gcd = (L, R) => {

    // Highest power of 2 that is not
    // more than count of elements
    let j = parseInt(Math.log2(R - L + 1));

    // Return GCD in range
    return gcd(table[L][j], table[R - (1 << j) + 1][j]);
}

// Smallest prime factors array
let spf = new Array(MAXN).fill(0);

// Function to build the smallest
// prime factor array using Sieve
const build_spf = () => {

    spf[1] = 1;
    for(let i = 2; i < MAXN; i++)
        spf[i] = i;
    for(let i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for(let i = 3; i * i < MAXN; i++)
    {
        if (spf[i] == i)
        {
            for(let j = i * i; j < MAXN; j += i)
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to find the count of
// distinct prime factors of x
let getFactorization = (x) => {

    // Stores the required count
    let ctr = 0;

    while (x != 1)
    {
        ctr++;

        // Stores smallest prime
        // factor of x
        let p = spf[x];

        while (x % p == 0)
            x = parseInt(x / p);
    }

    // Return count
    return ctr;
}

// Function to count of coprime pairs such
// that the product of the pair divides
// all letegers of subarray in given range
const solveQueries = (a, n, q) => {

    // Loop to iterate over queries
    for(let i = 0; i < q.length; i++)
    {
        let l = q[i][0];
        let r = q[i][1];
        l--;
        r--;

        // Stores gcd in the range
        let gcd = find_gcd(l, r);

        // Stores the required count
        let ans = 0;

        // Count the pairs of co-primes
        // letegers in given format
        for(let i = 1; i * i <= gcd; i++)
        {

            // If i is a factor of gcd
            if (gcd % i == 0)
            {
                ans = ans + (1 << getFactorization(i));
                if (parseInt(gcd / i) != i)
                    ans += (1 << getFactorization(
                            parseInt(gcd / i)));
            }
        }

        // Print answer
        document.write(`${ans} `);
    }
}

// Function to perform precomputation
const preProcess = (a, n) => {

    build_spf();
    buildSparseTable(a, n);
}

// Driver Code
let arr = [ 1, 2, 2, 4, 5 ];
let queries = [ [ 2, 3 ], [ 2, 4 ],
                [ 3, 4 ], [ 4, 4 ],
                [ 4, 5 ] ];

preProcess(arr, arr.length);
solveQueries(arr, arr.length, queries);

// This code is contributed by rakeshsahni

</script>
```

**Output**

```
3 3 3 5 1 
```

***时间复杂度:** O(Q * sqrt(M) * log M)，其中 M 是给定数组中的最大整数*
***辅助空间:** O(M*log M)*