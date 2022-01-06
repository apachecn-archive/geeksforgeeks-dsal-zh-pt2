# 斐波那契幂

> 原文:[https://www.geeksforgeeks.org/fibonacci-power/](https://www.geeksforgeeks.org/fibonacci-power/)

给定一个数字 n，你需要找到(Fib(n) ^ Fib(n) ) % 10^9 + 7，其中 Fib(n)是第 n 个斐波那契数。

**示例:**

> **输入** : n = 4
> **输出** : 27
> 第 4 个斐波那契数为 3
> 【fib(4)^ fib(4)】% 10^9+7 =(3 ^ 3)% 10^9+7 = 27
> 
> **输入** : n = 3
> **输出** : 4
> 第 3 个斐波那契数为 2
> 【fib(3)^ fib(3)】% 10^9+7 =(2 ^ 2)% 10^9+7 = 4

如果 n 很大，那么 **fib(n)** 将是巨大的，而 **fib(n)** ^ **fib(n)** 不仅难以计算，而且其存储也是不可能的。

**方法:**
( a ^ (p-1) ) % p = 1 其中 p 是素数(使用费马小定理)。
( a ^ a ) % m 可以写成((a % m ) ^ a ) % m
也可以写成 a = k *(m–1)+r(使用除法算法)
的任意数字‘a’，其中‘k’是商，‘r’是余数。我们可以说 r = a % (m-1)
所以，减少计算的步骤，让我们假设 a = fib(n)

```
  ( a ^ a ) % m 
= ( ( a % m ) ^ a ) % m 
= ( ( a % m ) ^ ( k * ( m - 1 ) + r ) ) % m 
= ( ( ( a % m ) ^ ( m-1 ) ) ^ k  * ( a % m ) ^ r ) % m
= ( (1 ^ k) * ( a % m ) ^ r ) % m
= ( ( a % m ) ^ r ) % m   
= ( ( a % m ) ^ (a % (m-1) ) % m 
```

a % m 和 a % (m-1)易于计算和存储。
我们可以使用[这篇](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/) GFG 文章来计算(x ^ y ) % m。
我们可以使用[这篇](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/) GFG 文章在 **log(n)** time 中找到 n <sup>th</sup> 斐波那契数。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
#define mod 1000000007
using namespace std;

// Iterative function to compute modular power
long long modularexpo(long long x, long long y, long long p)
{
    // Initialize result
    long long res = 1;
    // Update x if it is more than or
    // equal to p
    x = x % p;

    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Helper function that multiplies 2 matrices
// F and M of size 2*2, and puts the
// multiplication result back to F[][]
void multiply(long long F[2][2], long long M[2][2], long long m)
{
    long long x = ((F[0][0] * M[0][0]) % m +
                   (F[0][1] * M[1][0]) % m) % m;

    long long y = ((F[0][0] * M[0][1]) % m +
                   (F[0][1] * M[1][1]) % m) % m;

    long long z = ((F[1][0] * M[0][0]) % m +
                   (F[1][1] * M[1][0]) % m) % m;

    long long w = ((F[1][0] * M[0][1]) % m +
                   (F[1][1] * M[1][1]) % m) % m;

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Helper function that calculates F[][] raise to
// the power n and puts the  result in F[][]
// Note that this function is designed only for fib()
// and won't work as general power function
void power(long long F[2][2], long long n, long long m)
{
    if (n == 0 || n == 1)
        return;
    long long M[2][2] = { { 1, 1 }, { 1, 0 } };

    power(F, n / 2, m);
    multiply(F, F, m);

    if (n % 2 != 0)
        multiply(F, M, m);
}

// Function that returns nth Fibonacci number
long long fib(long long n, long long m)
{
    long long F[2][2] = { { 1, 1 }, { 1, 0 } };
    if (n == 0)
        return 0;
    power(F, n - 1, m);
    return F[0][0];
}

// Driver Code
int main()
{
    long long n = 4;
    long long base = fib(n, mod) % mod;
    long long expo = fib(n, mod - 1) % (mod - 1);
    long long result = modularexpo(base, expo, mod) % mod;
    cout << result << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{
static int mod = 1000000007;

// Iterative function to compute modular power
static long modularexpo(long x, long y, long p)
{
    // Initialize result
    long res = 1;

    // Update x if it is more than or
    // equal to p
    x = x % p;

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y % 2 == 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Helper function that multiplies 2 matrices
// F and M of size 2*2, and puts the
// multiplication result back to F[][]
static void multiply(long F[][],
                     long M[][], long m)
{
    long x = ((F[0][0] * M[0][0]) % m +
              (F[0][1] * M[1][0]) % m) % m;

    long y = ((F[0][0] * M[0][1]) % m +
              (F[0][1] * M[1][1]) % m) % m;

    long z = ((F[1][0] * M[0][0]) % m +
              (F[1][1] * M[1][0]) % m) % m;

    long w = ((F[1][0] * M[0][1]) % m +
              (F[1][1] * M[1][1]) % m) % m;

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Helper function that calculates F[][] raise to
// the power n and puts the result in F[][]
// Note that this function is designed only for fib()
// and won't work as general power function
static void power(long F[][], long n, long m)
{
    if (n == 0 || n == 1)
        return;
    long M[][] = { { 1, 1 }, { 1, 0 } };

    power(F, n / 2, m);
    multiply(F, F, m);

    if (n % 2 != 0)
        multiply(F, M, m);
}

// Function that returns nth Fibonacci number
static long fib(long n, long m)
{
    long F[][] = { { 1, 1 }, { 1, 0 } };
    if (n == 0)
        return 0;
    power(F, n - 1, m);
    return F[0][0];
}

// Driver Code
public static void main(String[] args)
{
    long n = 4;
    long base = fib(n, mod) % mod;
    long expo = fib(n, mod - 1) % (mod - 1);
    long result = modularexpo(base, expo, mod) % mod;
    System.out.println(result);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
mod = 1000000007;

# Iterative function to compute modular power
def modularexpo(x, y, p):

    # Initialize result
    res = 1;

    # Update x if it is more than or
    # equal to p
    x = x % p;

    while (y > 0):

        # If y is odd, multiply x with result
        if (y & 1):
            res = (res * x) % p;

        # y must be even now
        y = y >> 1;
        x = (x * x) % p;

    return res;

# Helper function that multiplies 2 matrices
# F and M of size 2*2, and puts the
# multiplication result back to F[][]
def multiply(F, M, m):

    x = ((F[0][0] * M[0][0]) % m +
         (F[0][1] * M[1][0]) % m) % m;

    y = ((F[0][0] * M[0][1]) % m +
         (F[0][1] * M[1][1]) % m) % m;

    z = ((F[1][0] * M[0][0]) % m +
         (F[1][1] * M[1][0]) % m) % m;

    w = ((F[1][0] * M[0][1]) % m +
         (F[1][1] * M[1][1]) % m) % m;

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;

# Helper function that calculates F[][] raise to
# the power n and puts the result in F[][]
# Note that this function is designed only for fib()
# and won't work as general power function
def power(F, n, m):

    if (n == 0 or n == 1):
        return;
    M = [[ 1, 1 ], [ 1, 0 ]];

    power(F, n // 2, m);
    multiply(F, F, m);

    if (n % 2 != 0):
        multiply(F, M, m);

# Function that returns nth Fibonacci number
def fib(n, m):

    F = [[ 1, 1 ], [ 1, 0 ]];
    if (n == 0):
        return 0;
    power(F, n - 1, m);
    return F[0][0];

# Driver Code
if __name__ == '__main__':
    n = 4;
    base = fib(n, mod) % mod;
    expo = fib(n, mod - 1) % (mod - 1);
    result = modularexpo(base, expo, mod) % mod;
    print(result);

# This code is contributed by 29AjayKumar
```

## C#

```
using System;

class GFG
{
static int mod = 1000000007;

// Iterative function to compute modular power
static long modularexpo(long x, long y, long p)
{
    // Initialize result
    long res = 1;

    // Update x if it is more than or
    // equal to p
    x = x % p;

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y % 2 == 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Helper function that multiplies 2 matrices
// F and M of size 2*2, and puts the
// multiplication result back to F[,]
static void multiply(long [,]F,
                     long [,]M, long m)
{
    long x = ((F[0, 0] * M[0, 0]) % m +
              (F[0, 1] * M[1, 0]) % m) % m;

    long y = ((F[0, 0] * M[0, 1]) % m +
              (F[0, 1] * M[1, 1]) % m) % m;

    long z = ((F[1, 0] * M[0, 0]) % m +
              (F[1, 1] * M[1, 0]) % m) % m;

    long w = ((F[1, 0] * M[0, 1]) % m +
              (F[1, 1] * M[1, 1]) % m) % m;

    F[0, 0] = x;
    F[0, 1] = y;
    F[1, 0] = z;
    F[1, 1] = w;
}

// Helper function that calculates F[,] raise to
// the power n and puts the result in F[,]
// Note that this function is designed only for fib()
// and won't work as general power function
static void power(long [,]F, long n, long m)
{
    if (n == 0 || n == 1)
        return;
    long [,]M = { { 1, 1 }, { 1, 0 } };

    power(F, n / 2, m);
    multiply(F, F, m);

    if (n % 2 != 0)
        multiply(F, M, m);
}

// Function that returns nth Fibonacci number
static long fib(long n, long m)
{
    long [,]F = { { 1, 1 }, { 1, 0 } };
    if (n == 0)
        return 0;
    power(F, n - 1, m);
    return F[0, 0];
}

// Driver Code
public static void Main(String[] args)
{
    long n = 4;
    long Base = fib(n, mod) % mod;
    long expo = fib(n, mod - 1) % (mod - 1);
    long result = modularexpo(Base, expo, mod) % mod;
    Console.WriteLine(result);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

let mod = 1000000007;

// Iterative function to compute modular power
function modularexpo(x, y, p)
{

    // Initialize result
    let res = 1;

    // Update x if it is more than or
    // equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if (y % 2 == 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Helper function that multiplies 2 matrices
// F and M of size 2*2, and puts the
// multiplication result back to F[][]
function multiply(F, M, m)
{
    let x = ((F[0][0] * M[0][0]) % m +
             (F[0][1] * M[1][0]) % m) % m;

    let y = ((F[0][0] * M[0][1]) % m +
             (F[0][1] * M[1][1]) % m) % m;

    let z = ((F[1][0] * M[0][0]) % m +
             (F[1][1] * M[1][0]) % m) % m;

    let w = ((F[1][0] * M[0][1]) % m +
             (F[1][1] * M[1][1]) % m) % m;

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Helper function that calculates F[][] raise to
// the power n and puts the result in F[][]
// Note that this function is designed only for fib()
// and won't work as general power function
function power(F, n, m)
{
    if (n == 0 || n == 1)
        return;

    let M = [ [ 1, 1 ], [ 1, 0 ] ];

    power(F, Math.floor(n / 2), m);
    multiply(F, F, m);

    if (n % 2 != 0)
        multiply(F, M, m);
}

// Function that returns nth Fibonacci number
function fib(n, m)
{
    let F = [ [ 1, 1 ], [ 1, 0 ] ];
    if (n == 0)
        return 0;

    power(F, n - 1, m);
    return F[0][0];
}

// Driver Code
let n = 4;
let base = fib(n, mod) % mod;
let expo = fib(n, mod - 1) % (mod - 1);
let result = modularexpo(base, expo, mod) % mod;

document.write(result);

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
27
```

**时间复杂度:** log(n)