# 给定运算产生的素因子和序列的最大长度

> 原文:[https://www . geeksforgeeks . org/给定运算生成的素数因子和序列的最大长度/](https://www.geeksforgeeks.org/maximum-length-of-sequence-of-sums-of-prime-factors-generated-by-the-given-operations/)

给定两个整数 **N** 和 **M** ，任务是执行以下操作:

*   对于范围**【N，M】**中的每个值，计算其质因数之和，然后是该和的质因数之和，以此类推。
*   为每个数组元素生成上述序列，并计算序列的长度

> **插图**
> N = 8
> 质因数= {2，2，2}。总和= 2 + 2 + 2 = 6。
> 6 的质因数= {2，3}。总和= 2 + 3 = 5。
> 现在 5 不能再减了。
> 所以顺序是 **{8，6，5}** 。序列长度为 **3** 。

*   找出生成的子序列的最大长度。

**示例:**

> ***输入:** N = 5，M = 10*
> ***输出:** 3*
> ***解释:***
> *对于 N = 5，序列为{5}，所以长度为 1*
> *对于 N = 6，序列为{6，5}，所以长度为 2*
> *对于 N = 7，序列为{7}， 5}，所以长度为 3*
> *对于 N = 9，序列为{9，6，5}，所以长度为 3*
> *对于 N = 10，序列为{10，7}，所以长度为 2*
> *所以，这个范围内序列的最大长度为 3。*
> 
> ***输入:** N = 2，M = 14*
> T5**输出:** 4

**天真法:**解决问题最简单的方法是在范围**【N，M】**上迭代，对于每个整数，找到它的素因子并对它们求和，对于得到的和也重复这个过程 [**【递归地】**](https://www.geeksforgeeks.org/recursion/) 直到得到本身是素的和。

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。按照以下步骤解决问题:

*   使用厄拉多塞方法的[筛预计算素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   预计算每个整数的最小素因子，找出素因子，使用[使用筛](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)进行素因子分解。
*   现在，对于**【N，M】**范围内的每个整数，计算质因数之和，对得到的和递归重复。将序列的长度存储在 **dp[]** 数组中，以避免重新计算。如果得到的和是素数，存储进一步的计算。
*   更新获得的最大长度，对**【N，M】**范围内的每个数字重复上述步骤，除了 **4** ，这将导致*无限循环*。
*   打印获得的最大长度。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Smallest prime factor array
int spf[100005];

// Stores if a number is prime or not
bool prime[100005];

int dp[100005];

// Function to compute all primes
// using Sieve of Eratosthenes
void sieve()
{
    prime[0] = prime[1] = false;

    for (int i = 2; i < 100005; i++)
        prime[i] = true;

    for (int i = 2; i * i < 100005; i++) {
        if (prime[i]) {
            for (int j = i * i; j < 100005; j += i) {
                prime[j] = false;
            }
        }
    }
}

// Function for finding smallest
// prime factors for every integer
void smallestPrimeFactors()
{
    for (int i = 0; i < 100005; i++)
        spf[i] = -1;
    for (int i = 2; i * i < 100005; i++) {
        for (int j = i; j < 100005; j += i) {
            if (spf[j] == -1) {
                spf[j] = i;
            }
        }
    }
}

// Function to find the sum of
// prime factors of number
int sumOfPrimeFactors(int n)
{

    int ans = 0;
    while (n > 1) {

        // Add smallest prime
        // factor to the sum
        ans += spf[n];

        // Reduce N
        n /= spf[n];
    }

    // Return the answer
    return ans;
}

// Function to return the length of
// sequence of for the given number
int findLength(int n)
{

    // If the number is prime
    if (prime[n]) {
        return 1;
    }

    // If a previously computed
    // subproblem occurred
    if (dp[n]) {
        return dp[n];
    }

    // Calculate the sum of
    // prime factors
    int sum = sumOfPrimeFactors(n);

    return dp[n] = 1 + findLength(sum);
}

// Function to return the maximum length
// of sequence for the given range
int maxLength(int n, int m)
{

    // Pre-calculate primes
    sieve();

    // Precalculate smallest
    // prime factors
    smallestPrimeFactors();

    int ans = INT_MIN;

    // Iterate over the range
    for (int i = n; i <= m; i++) {
        if (i == 4) {
            continue;
        }

        // Update maximum length
        ans = max(ans, findLength(i));
    }

    return ans;
}

// Driver Code
int main()
{
    int n = 2, m = 14;

    cout << maxLength(n, m);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Smallest prime factor array
static int spf[] = new int[100005];

// Stores if a number is prime or not
static boolean prime[] = new boolean[100005];

static int dp[] = new int[100005];

// Function to compute all primes
// using Sieve of Eratosthenes
static void sieve()
{
    prime[0] = prime[1] = false;

    for (int i = 2; i < 100005; i++)
        prime[i] = true;

    for (int i = 2; i * i < 100005; i++)
    {
        if (prime[i])
        {
            for (int j = i * i; j < 100005; j += i)
            {
                prime[j] = false;
            }
        }
    }
}

// Function for finding smallest
// prime factors for every integer
static void smallestPrimeFactors()
{
    for (int i = 0; i < 100005; i++)
        spf[i] = -1;
    for (int i = 2; i * i < 100005; i++)
    {
        for (int j = i; j < 100005; j += i)
        {
            if (spf[j] == -1)
            {
                spf[j] = i;
            }
        }
    }
}

// Function to find the sum of
// prime factors of number
static int sumOfPrimeFactors(int n)
{

    int ans = 0;
    while (n > 1)
    {

        // Add smallest prime
        // factor to the sum
        ans += spf[n];

        // Reduce N
        n /= spf[n];
    }

    // Return the answer
    return ans;
}

// Function to return the length of
// sequence of for the given number
static int findLength(int n)
{

    // If the number is prime
    if (prime[n])
    {
        return 1;
    }

    // If a previously computed
    // subproblem occurred
    if (dp[n] != 0)
    {
        return dp[n];
    }

    // Calculate the sum of
    // prime factors
    int sum = sumOfPrimeFactors(n);

    return dp[n] = 1 + findLength(sum);
}

// Function to return the maximum length
// of sequence for the given range
static int maxLength(int n, int m)
{

    // Pre-calculate primes
    sieve();

    // Precalculate smallest
    // prime factors
    smallestPrimeFactors();

    int ans = Integer.MIN_VALUE;

    // Iterate over the range
    for (int i = n; i <= m; i++)
    {
        if (i == 4)
        {
            continue;
        }

        // Update maximum length
        ans = Math.max(ans, findLength(i));
    }

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int n = 2, m = 14;

    System.out.print(maxLength(n, m));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Smallest prime factor array
spf = [0] * 100005

# Stores if a number is prime or not
prime = [False] * 100005

dp = [0] * 100005

# Function to compute all primes
# using Sieve of Eratosthenes
def sieve():

    for i in range(2, 100005):
        prime[i] = True

    i = 2
    while i * i < 100005:
        if(prime[i]):
            for j in range(i * i, 100005, i):
                prime[j] = False

        i += 1

# Function for finding smallest
# prime factors for every integer
def smallestPrimeFactors():

    for i in range(10005):
        spf[i] = -1

    i = 2
    while i * i < 100005:
        for j in range(i, 100005, i):
            if(spf[j] == -1):
                spf[j] = i

        i += 1

# Function to find the sum of
# prime factors of number
def sumOfPrimeFactors(n):

    ans = 0
    while(n > 1):

        # Add smallest prime
        # factor to the sum
        ans += spf[n]

        # Reduce N
        n //= spf[n]

    # Return the answer
    return ans

# Function to return the length of
# sequence of for the given number
def findLength(n):

    # If the number is prime
    if(prime[n]):
        return 1

    # If a previously computed
    # subproblem occurred
    if(dp[n]):
        return dp[n]

    # Calculate the sum of
    # prime factors
    sum = sumOfPrimeFactors(n)

    dp[n] = 1 + findLength(sum)

    return dp[n]

# Function to return the maximum length
# of sequence for the given range
def maxLength(n, m):

    # Pre-calculate primes
    sieve()

    # Precalculate smallest
    # prime factors
    smallestPrimeFactors()

    ans = -sys.maxsize - 1

    # Iterate over the range
    for i in range(n, m + 1):
        if(i == 4):
            continue

        # Update maximum length
        ans = max(ans, findLength(i))

    return ans

# Driver Code
n = 2
m = 14

# Function call
print(maxLength(n, m))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Smallest prime factor array
static int []spf = new int[100005];

// Stores if a number is prime or not
static bool []prime = new bool[100005];

static int []dp = new int[100005];

// Function to compute all primes
// using Sieve of Eratosthenes
static void sieve()
{
    prime[0] = prime[1] = false;

    for(int i = 2; i < 100005; i++)
        prime[i] = true;

    for(int i = 2; i * i < 100005; i++)
    {
        if (prime[i])
        {
            for(int j = i * i; j < 100005; j += i)
            {
                prime[j] = false;
            }
        }
    }
}

// Function for finding smallest
// prime factors for every integer
static void smallestPrimeFactors()
{
    for(int i = 0; i < 100005; i++)
        spf[i] = -1;

    for(int i = 2; i * i < 100005; i++)
    {
        for(int j = i; j < 100005; j += i)
        {
            if (spf[j] == -1)
            {
                spf[j] = i;
            }
        }
    }
}

// Function to find the sum of
// prime factors of number
static int sumOfPrimeFactors(int n)
{
    int ans = 0;
    while (n > 1)
    {

        // Add smallest prime
        // factor to the sum
        ans += spf[n];

        // Reduce N
        n /= spf[n];
    }

    // Return the answer
    return ans;
}

// Function to return the length of
// sequence of for the given number
static int findLength(int n)
{

    // If the number is prime
    if (prime[n])
    {
        return 1;
    }

    // If a previously computed
    // subproblem occurred
    if (dp[n] != 0)
    {
        return dp[n];
    }

    // Calculate the sum of
    // prime factors
    int sum = sumOfPrimeFactors(n);

    return dp[n] = 1 + findLength(sum);
}

// Function to return the maximum length
// of sequence for the given range
static int maxLength(int n, int m)
{

    // Pre-calculate primes
    sieve();

    // Precalculate smallest
    // prime factors
    smallestPrimeFactors();

    int ans = int.MinValue;

    // Iterate over the range
    for(int i = n; i <= m; i++)
    {
        if (i == 4)
        {
            continue;
        }

        // Update maximum length
        ans = Math.Max(ans, findLength(i));
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 2, m = 14;

    Console.Write(maxLength(n, m));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

// Smallest prime factor array
let spf = Array.from({length: 100005}, (_, i) => 0);

// Stores if a number is prime or not
let prime = Array.from({length: 100005}, (_, i) => 0);

let dp = Array.from({length: 100005}, (_, i) => 0);

// Function to compute all primes
// using Sieve of Eratosthenes
function sieve()
{
    prime[0] = prime[1] = false;

    for (let i = 2; i < 100005; i++)
        prime[i] = true;

    for (let i = 2; i * i < 100005; i++)
    {
        if (prime[i])
        {
            for (let j = i * i; j < 100005; j += i)
            {
                prime[j] = false;
            }
        }
    }
}

// Function for finding smallest
// prime factors for every integer
function smallestPrimeFactors()
{
    for (let i = 0; i < 100005; i++)
        spf[i] = -1;
    for (let i = 2; i * i < 100005; i++)
    {
        for (let j = i; j < 100005; j += i)
        {
            if (spf[j] == -1)
            {
                spf[j] = i;
            }
        }
    }
}

// Function to find the sum of
// prime factors of number
function sumOfPrimeFactors(n)
{

    let ans = 0;
    while (n > 1)
    {

        // Add smallest prime
        // factor to the sum
        ans += spf[n];

        // Reduce N
        n /= spf[n];
    }

    // Return the answer
    return ans;
}

// Function to return the length of
// sequence of for the given number
function findLength(n)
{

    // If the number is prime
    if (prime[n])
    {
        return 1;
    }

    // If a previously computed
    // subproblem occurred
    if (dp[n] != 0)
    {
        return dp[n];
    }

    // Calculate the sum of
    // prime factors
    let sum = sumOfPrimeFactors(n);

    return dp[n] = 1 + findLength(sum);
}

// Function to return the maximum length
// of sequence for the given range
function maxLength(n, m)
{

    // Pre-calculate primes
    sieve();

    // Precalculate smallest
    // prime factors
    smallestPrimeFactors();

    let ans = Number.MIN_VALUE;

    // Iterate over the range
    for (let i = n; i <= m; i++)
    {
        if (i == 4)
        {
            continue;
        }

        // Update maximum length
        ans = Math.max(ans, findLength(i));
    }

    return ans;
}

// Driver Code

    let n = 2, m = 14;

    document.write(maxLength(n, m));

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O((NlogN)
T3】辅助空间: O(N)