# 计数乘积为 X 的正整数序列

> 原文:[https://www . geeksforgeeks . org/count-正整数序列-having-product-x/](https://www.geeksforgeeks.org/count-sequences-of-positive-integers-having-product-x/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出乘积正好为 **X** 的可能正整数序列的总数(大于 1)。 **X** 的值计算为项的乘积，其中 i <sup>第</sup>项通过将 i <sup>第</sup>T14】素数提升到**arr【I】**的幂来生成。

> x = 2 ^ arr[1]* 3 ^ arr[2]* 5 ^ arr[3]* 7 ^ arr[4]* 11 ^ arr[5]*…直到第 n 个任期

**注意:**由于这样的序列总数的个数可以很大，打印答案[模 10 <sup>9</sup> + 7](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

**示例:**

> **输入:** arr[] = {1，1}
> **输出:** 3
> **解释:**
> 这里，X = 2^1 * 3^1 = 6
> 可能的正序列，其乘积为 X: {2，3}、{3，2}、{6}
> 
> **输入:** arr[] = {2}
> **输出:** 2
> **解释:**
> 这里，X = 2^2 = 4。
> 产品为 X 的可能阳性序列:{2，2}和{4}。

**天真方法:**思路是先计算 **X** 的值，然后使用[递归](https://www.geeksforgeeks.org/recursion/)生成所有可能的序列，其乘积为 **X** 。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效途径:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和[组合学](https://www.geeksforgeeks.org/combinatorics-gq/)途径解决。以下是步骤:

*   首先，找出在所有可能的序列中可以出现的正元素的最大数量，这将是给定数组**arr【】**的总和。
*   然后使用动态编程来填充可能序列中的槽，从 1 到序列长度的索引 I 开始。
    *   对于值为 **P[j]** 的每个第 j 个素数，将所有 **P[j]** 素数划分到每个 I 槽中。
    *   使用**组合学方法**将**P【j】**元素分成 I 槽。将值存储在数组**中的方式【】**如下更新方式[i]:

> ![ways[i] \space *= \dbinom {P[j] + i - 1}{i - 1}                 ](img/8a6c0c175a55062183e5ead3796d691b.png "Rendered by QuickLaTeX.com")
> 
> 将 N 个相同元素划分为 K 个槽的方法数量=(N+K–1)C(K–1)
> 这种方法在组合学中也称为**星条法**。

*   对于每一个 j 个质数，将这些值相乘。
*   然而，**路[]** 也将包含一个或多个空时隙的序列，因此减去所有填充时隙数小于 1 的时隙的确切贡献
*   对于从 j = **1 到 I–1**的每个槽，从 *i* 中选择 **j** 槽并减去其贡献。

> ![ways[i] \space -= \dbinom{i}{j} * ways[j] ](img/7669148f0a69a0e1d5337b53921c8637.png "Rendered by QuickLaTeX.com")

*   最后，将数组**的所有值以[]** 的方式相加，得到总结果。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int bin[3000][3000];

// Function to print the total number
// of possible sequences with
// product X
void countWays(const vector<int>& arr)
{
    int mod = 1e9 + 7;
    bin[0][0] = 1;

    // Precomputation of
    // binomial coefficients
    for (int i = 1; i < 3000; i++) {
        bin[i][0] = 1;
        for (int j = 1; j <= i; j++) {
            bin[i][j] = (bin[i - 1][j]
                         + bin[i - 1][j - 1])
                        % mod;
        }
    }

    // Max length of a subsequence
    int n = 0;
    for (auto x : arr)
        n += x;

    // Ways dp array
    vector<int> ways(n + 1);

    for (int i = 1; i <= n; i++) {
        ways[i] = 1;

        // Fill i slots using all
        // the primes
        for (int j = 0;
             j < (int)arr.size(); j++) {
            ways[i] = (ways[i]
                       * bin[arr[j] + i - 1]
                            [i - 1])
                      % mod;
        }

        // Subtract ways for all
        // slots that exactly
        // fill less than i slots
        for (int j = 1; j < i; j++) {
            ways[i] = ((ways[i]
                        - bin[i][j] * ways[j])
                           % mod
                       + mod)
                      % mod;
        }
    }

    // Total possible sequences
    int ans = 0;
    for (auto x : ways)
        ans = (ans + x) % mod;

    // Print the resultant count
    cout << ans << endl;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 1 };

    // Function call
    countWays(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int [][]bin = new int[3000][3000];

// Function to print the total number
// of possible sequences with
// product X
static void countWays(int[] arr)
{
    int mod = (int)1e9 + 7;
    bin[0][0] = 1;

    // Precomputation of
    // binomial coefficients
    for(int i = 1; i < 3000; i++)
    {
        bin[i][0] = 1;
        for(int j = 1; j <= i; j++)
        {
            bin[i][j] = (bin[i - 1][j] +
                         bin[i - 1][j - 1]) % mod;
        }
    }

    // Max length of a subsequence
    int n = 0;
    for(int x : arr)
        n += x;

    // Ways dp array
    int[] ways = new int[n + 1];

    for(int i = 1; i <= n; i++)
    {
        ways[i] = 1;

        // Fill i slots using all
        // the primes
        for(int j = 0; j < arr.length; j++)
        {
            ways[i] = (ways[i] *
                    bin[arr[j] + i - 1][i - 1]) % mod;
        }

        // Subtract ways for all
        // slots that exactly
        // fill less than i slots
        for(int j = 1; j < i; j++)
        {
            ways[i] = ((ways[i] - bin[i][j] *
                        ways[j]) % mod + mod) % mod;
        }
    }

    // Total possible sequences
    int ans = 0;
    for(int x : ways)
        ans = (ans + x) % mod;

    // Print the resultant count
    System.out.print(ans + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 1 };

    // Function call
    countWays(arr);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
bin = [[0 for i in range(3000)]
          for i in range(3000)]

# Function to print the total number
# of possible sequences with
# product X
def countWays(arr):

    mod = 10**9 + 7
    bin[0][0] = 1

    # Precomputation of
    # binomial coefficients
    for i in range(1, 3000):
        bin[i][0] = 1

        for j in range(1, i + 1):
            bin[i][j] = (bin[i - 1][j] +
                         bin[i - 1][j - 1]) % mod

    # Max length of a subsequence
    n = 0

    for x in arr:
        n += x

    # Ways dp array
    ways = [0] * (n + 1)

    for i in range(1, n + 1):
        ways[i] = 1

        # Fill i slots using all
        # the primes
        for j in range(len(arr)):
            ways[i] = (ways[i] *
                    bin[arr[j] + i - 1][i - 1]) % mod

        # Subtract ways for all
        # slots that exactly
        # fill less than i slots
        for j in range(1, i):
            ways[i] = ((ways[i] - bin[i][j] *
                        ways[j]) % mod + mod) % mod

    # Total possible sequences
    ans = 0

    for x in ways:
        ans = (ans + x) % mod

    # Print the resultant count
    print(ans)

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 1 ]

    # Function call
    countWays(arr)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int [,]bin = new int[3000, 3000];

// Function to print the total number
// of possible sequences with
// product X
static void countWays(int[] arr)
{
    int mod = (int)1e9 + 7;
    bin[0, 0] = 1;

    // Precomputation of
    // binomial coefficients
    for(int i = 1; i < 3000; i++)
    {
        bin[i, 0] = 1;
        for(int j = 1; j <= i; j++)
        {
            bin[i, j] = (bin[i - 1, j] +
                         bin[i - 1, j - 1]) % mod;
        }
    }

    // Max length of a subsequence
    int n = 0;
    foreach(int x in arr)
        n += x;

    // Ways dp array
    int[] ways = new int[n + 1];

    for(int i = 1; i <= n; i++)
    {
        ways[i] = 1;

        // Fill i slots using all
        // the primes
        for(int j = 0; j < arr.Length; j++)
        {
            ways[i] = (ways[i] *
                    bin[arr[j] + i - 1, i - 1]) % mod;
        }

        // Subtract ways for all
        // slots that exactly
        // fill less than i slots
        for(int j = 1; j < i; j++)
        {
            ways[i] = ((ways[i] - bin[i, j] *
                        ways[j]) % mod + mod) % mod;
        }
    }

    // Total possible sequences
    int ans = 0;
    foreach(int x in ways)
        ans = (ans + x) % mod;

    // Print the resultant count
    Console.Write(ans + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 1, 1 };

    // Function call
    countWays(arr);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

var bin = Array.from(Array(3000), ()=> Array(3000).fill(0));

// Function to print the total number
// of possible sequences with
// product X
function countWays(arr)
{
    var mod = 1000000007;
    bin[0][0] = 1;

    // Precomputation of
    // binomial coefficients
    for (var i = 1; i < 3000; i++) {
        bin[i][0] = 1;
        for (var j = 1; j <= i; j++) {
            bin[i][j] = (bin[i - 1][j]
                         + bin[i - 1][j - 1])
                        % mod;
        }
    }

    // Max length of a subsequence
    var n = 0;
    for (var x =0; x<arr.length; x++)
        n += arr[x];

    // Ways dp array
    var ways = Array(n + 1).fill(0);

    for (var i = 1; i <= n; i++) {
        ways[i] = 1;

        // Fill i slots using all
        // the primes
        for (var j = 0;
             j <arr.length; j++) {
            ways[i] = (ways[i]
                       * bin[arr[j] + i - 1]
                            [i - 1])
                      % mod;
        }

        // Subtract ways for all
        // slots that exactly
        // fill less than i slots
        for (var j = 1; j < i; j++) {
            ways[i] = ((ways[i]
                        - bin[i][j] * ways[j])
                           % mod
                       + mod)
                      % mod;
        }
    }

    // Total possible sequences
    var ans = 0;
    for (var i = 1; i <= n; i++)
        ans = (ans + ways[i]) % mod;

    // Print the resultant count
    document.write( ans );
}

// Driver Code
var arr = [ 1, 1 ];
// Function call
countWays(arr);

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*