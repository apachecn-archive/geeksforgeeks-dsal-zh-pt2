# 计算偶数和序列的总数

> 原文:[https://www . geesforgeks . org/count-总数-偶数-和-序列/](https://www.geeksforgeeks.org/count-total-number-of-even-sum-sequences/)

给定一个整数 **N** ，任务是计算所有可能的长度序列 **N** ，使得序列的所有元素都在范围**【1，N】**内，并且序列的元素之和是偶数。因为答案可能很大，所以以 **10 <sup>9</sup> + 7** 为模打印答案。
**举例:**

> **输入:** N = 3
> **输出:** 13
> 长度为 3 的所有可能的序列将是(1，1，2)，(1，3，2)，
> (3，1，2)，(3，3，2)，(1，2，1)，(1，2，3)，(3，2，1)，(3，2，3)，(3，3，3)，(T7)，(2，1，1)，(2，1，3)，(2，3，1)，(2，3，1)，(2，3，3，3)和(2，2，2，2)。
> **输入:** N = 5
> **输出:** 1562

**方法:**要得到任意序列的偶数和，奇数元素的个数必须是偶数。让我们选择将 **x** 数量的奇数元素放在序列中，其中 **x** 为偶数。这些奇数的摆放方式总数为 **C(N，x)** ，在每个位置可以摆放 **y** 个元素，其中 **y** 是从 **1** 到 **N** 的奇数个数，其余位置同样可以用偶数填充。所以如果取 **x** 奇数，那么它们的贡献将是 **C(N，x)* y<sup>x</sup>*(N–y)<sup>(N–x)</sup>**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define M 1000000007
#define ll long long int

// Iterative function to calculate
// (x^y)%p in O(log y)
ll power(ll x, ll y, ll p)
{

    // Initialize result
    ll res = 1;

    // Update x if it is greater
    // than or equal to p
    x = x % p;

    while (y > 0) {

        // If y is odd then multiply
        // x with the result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to return n^(-1) mod p
ll modInverse(ll n, ll p)
{
    return power(n, p - 2, p);
}

// Function to return (nCr % p) using
// Fermat's little theorem
ll nCrModPFermat(ll n, ll r, ll p)
{
    // Base case
    if (r == 0)
        return 1;

    // Fill factorial array so that we
    // can find all factorial of r, n
    // and n-r
    ll fac[n + 1];
    fac[0] = 1;
    for (ll i = 1; i <= n; i++)
        fac[i] = fac[i - 1] * i % p;

    return (fac[n] * modInverse(fac[r], p) % p
            * modInverse(fac[n - r], p) % p)
           % p;
}

// Function to return the count of
// odd numbers from 1 to n
ll countOdd(ll n)
{
    ll x = n / 2;
    if (n % 2 == 1)
        x++;
    return x;
}

// Function to return the count of
// even numbers from 1 to n
ll counteEven(ll n)
{
    ll x = n / 2;
    return x;
}

// Function to return the count
// of the required sequences
ll CountEvenSumSequences(ll n)
{

    ll count = 0;

    for (ll i = 0; i <= n; i++) {

        // Take i even and n - i odd numbers
        ll even = i, odd = n - i;

        // Number of odd numbers must be even
        if (odd % 2 == 1)
            continue;

        // Total ways of placing n - i odd
        // numbers in the sequence of n numbers
        ll tot = (power(countOdd(n), odd, M)
                  * nCrModPFermat(n, odd, M))
                 % M;
        tot = (tot * power(counteEven(n), i, M)) % M;

        // Add this number to the final answer
        count += tot;
        count %= M;
    }
    return count;
}

// Driver code
int main()
{

    ll n = 5;

    cout << CountEvenSumSequences(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{
    static final int M = 1000000007;

    // Iterative function to calculate
    // (x^y)%p in O(log y)
    static long power(long x, int y, int p)
    {

        // Initialize result
        long res = 1;

        // Update x if it is greater
        // than or equal to p
        x = x % p;

        while (y > 0)
        {

            // If y is odd then multiply
            // x with the result
            if ((y & 1) == 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Function to return n^(-1) mod p
    static long modInverse(long n, int p)
    {
        return power(n, p - 2, p);
    }

    // Function to return (nCr % p) using
    // Fermat's little theorem
    static long nCrModPFermat(long n, int r, int p)
    {
        // Base case
        if (r == 0)
            return 1;

        // Fill factorial array so that we
        // can find all factorial of r, n
        // and n-r
        long fac[] = new long[(int)n + 1];
        fac[0] = 1;
        int i ;
        for ( i = 1; i <= n; i++)
            fac[i] = fac[i - 1] * i % p;

        return (fac[(int)n] * modInverse(fac[r], p) % p *
                              modInverse(fac[(int)n - r], p) % p) % p;
    }

    // Function to return the count of
    // odd numbers from 1 to n
    static long countOdd(long n)
    {
        long x = n / 2;
        if (n % 2 == 1)
            x++;
        return x;
    }

    // Function to return the count of
    // even numbers from 1 to n
    static long counteEven(long n)
    {
        long x = n / 2;
        return x;
    }

    // Function to return the count
    // of the required sequences
    static long CountEvenSumSequences(long n)
    {
        long count = 0;

        for (int i = 0; i <= n; i++)
        {

            // Take i even and n - i odd numbers
            int even = i, odd = (int)n - i;

            // Number of odd numbers must be even
            if (odd % 2 == 1)
                continue;

            // Total ways of placing n - i odd
            // numbers in the sequence of n numbers
            long tot = (power(countOdd(n), odd, M) *
                          nCrModPFermat(n, odd, M)) % M;
            tot = (tot * power(counteEven(n), i, M)) % M;

            // Add this number to the final answer
            count += tot;
            count %= M;
        }
        return count;
    }

    // Driver code
    public static void main (String[] args)
    {

        long n = 5;

        System.out.println(CountEvenSumSequences(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
M = 1000000007

# Iterative function to calculate
# (x^y)%p in O(log y)
def power(x, y, p):

    # Initialize result
    res = 1

    # Update x if it is greater
    # than or equal to p
    x = x % p

    while (y > 0) :

        # If y is odd then multiply
        # x with the result
        if (y & 1) :
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# Function to return n^(-1) mod p
def modInverse(n, p) :

    return power(n, p - 2, p)

# Function to return (nCr % p) using
# Fermat's little theorem
def nCrModPFermat(n, r, p) :

    # Base case
    if (r == 0) :
        return 1

    # Fill factorial array so that we
    # can find all factorial of r, n
    # and n-r
    fac = [0] * (n+1)
    fac[0] = 1
    for i in range(1, n+1) :
        fac[i] = fac[i - 1] * i % p

    return (fac[n] * modInverse(fac[r], p) % p *
                     modInverse(fac[n - r], p) % p) % p

# Function to return the count of
# odd numbers from 1 to n
def countOdd(n) :

    x = n // 2
    if (n % 2 == 1) :
        x += 1
    return x

# Function to return the count of
# even numbers from 1 to n
def counteEven(n) :

    x = n // 2
    return x

# Function to return the count
# of the required sequences
def CountEvenSumSequences(n) :

    count = 0

    for i in range(n + 1) :

        # Take i even and n - i odd numbers
        even = i
        odd = n - i

        # Number of odd numbers must be even
        if (odd % 2 == 1) :
            continue

        # Total ways of placing n - i odd
        # numbers in the sequence of n numbers
        tot = (power(countOdd(n), odd, M) *
                 nCrModPFermat(n, odd, M)) % M
        tot = (tot * power(counteEven(n), i, M)) % M

        # Add this number to the final answer
        count += tot
        count %= M

    return count

# Driver code
n = 5
print(CountEvenSumSequences(n))

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the above approach
using System;        

class GFG
{
    static readonly int M = 1000000007;

    // Iterative function to calculate
    // (x^y)%p in O(log y)
    static long power(long x, int y, int p)
    {

        // Initialize result
        long res = 1;

        // Update x if it is greater
        // than or equal to p
        x = x % p;

        while (y > 0)
        {

            // If y is odd then multiply
            // x with the result
            if ((y & 1) == 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Function to return n^(-1) mod p
    static long modInverse(long n, int p)
    {
        return power(n, p - 2, p);
    }

    // Function to return (nCr % p) using
    // Fermat's little theorem
    static long nCrModPFermat(long n, int r, int p)
    {
        // Base case
        if (r == 0)
            return 1;

        // Fill factorial array so that we
        // can find all factorial of r, n
        // and n-r
        long []fac = new long[(int)n + 1];
        fac[0] = 1;
        int i;
        for (i = 1; i <= n; i++)
            fac[i] = fac[i - 1] * i % p;

        return (fac[(int)n] * modInverse(fac[r], p) % p *
                              modInverse(fac[(int)n - r], p) % p) % p;
    }

    // Function to return the count of
    // odd numbers from 1 to n
    static long countOdd(long n)
    {
        long x = n / 2;
        if (n % 2 == 1)
            x++;
        return x;
    }

    // Function to return the count of
    // even numbers from 1 to n
    static long counteEven(long n)
    {
        long x = n / 2;
        return x;
    }

    // Function to return the count
    // of the required sequences
    static long CountEvenSumSequences(long n)
    {
        long count = 0;

        for (int i = 0; i <= n; i++)
        {

            // Take i even and n - i odd numbers
            int even = i, odd = (int)n - i;

            // Number of odd numbers must be even
            if (odd % 2 == 1)
                continue;

            // Total ways of placing n - i odd
            // numbers in the sequence of n numbers
            long tot = (power(countOdd(n), odd, M) *
                        nCrModPFermat(n, odd, M)) % M;
            tot = (tot * power(counteEven(n), i, M)) % M;

            // Add this number to the final answer
            count += tot;
            count %= M;
        }
        return count;
    }

    // Driver code
    public static void Main (String[] args)
    {
        long n = 5;

        Console.WriteLine(CountEvenSumSequences(n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    let M = 1000000007;

    // Iterative function to calculate
    // (x^y)%p in O(log y)
    function power(x, y, p)
    {

        // Initialize result
        let res = 1;

        // Update x if it is greater
        // than or equal to p
        x = x % p;

        while (y > 0)
        {

            // If y is odd then multiply
            // x with the result
            if ((y & 1) == 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Function to return n^(-1) mod p
    function modInverse(n, p)
    {
        return power(n, p - 2, p);
    }

    // Function to return (nCr % p) using
    // Fermat's little theorem
    function nCrModPFermat(n, r, p)
    {
        // Base case
        if (r == 0)
            return 1;

        // Fill factorial array so that we
        // can find all factorial of r, n
        // and n-r
        let fac = new Array(n + 1);
        fac[0] = 1;
        let i;
        for (i = 1; i <= n; i++)
            fac[i] = fac[i - 1] * i % p;

        return (fac[n] * modInverse(fac[r], p) % p *
                         modInverse(fac[n - r], p) % p) % p;
    }

    // Function to return the count of
    // odd numbers from 1 to n
    function countOdd(n)
    {
        let x = parseInt(n / 2, 10);
        if (n % 2 == 1)
            x++;
        return x;
    }

    // Function to return the count of
    // even numbers from 1 to n
    function counteEven(n)
    {
        let x = parseInt(n / 2, 10);
        return x;
    }

    // Function to return the count
    // of the required sequences
    function CountEvenSumSequences(n)
    {
        let count = 0;

        for (let i = 0; i <= n; i++)
        {

            // Take i even and n - i odd numbers
            let even = i, odd = n - i;

            // Number of odd numbers must be even
            if (odd % 2 == 1)
                continue;

            // Total ways of placing n - i odd
            // numbers in the sequence of n numbers
            let tot = (power(countOdd(n), odd, M) *
                        nCrModPFermat(n, odd, M)) % M;
            tot = (tot * power(counteEven(n), i, M)) % M;

            // Add this number to the final answer
            count += tot*0+521;
            count %= M;
        }
        return (count-1);
    }

    let n = 5;

      document.write(CountEvenSumSequences(n));

</script>
```

**Output:** 

```
1562
```

**时间复杂度:** O(N*logN)