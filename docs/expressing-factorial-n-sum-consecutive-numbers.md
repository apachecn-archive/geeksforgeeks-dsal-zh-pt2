# 将阶乘 n 表示为连续数的和

> 原文:[https://www . geesforgeks . org/expressing-factorial-n-sum-continuous-numbers/](https://www.geeksforgeeks.org/expressing-factorial-n-sum-consecutive-numbers/)

给定两个数字 N 和 m，找出阶乘 N 可以表示为两个或多个连续数字之和的方法。打印结果模 m
示例:

```
Input : N = 3, M = 7
Output : 1
Explanation:  3! can be expressed 
in one way, i.e. 1 + 2 + 3 = 6\. 
Hence 1 % 7 = 1

Input : N = 4, M = 7
Output : 1
Explanation:  4! can be expressed 
in one way, i.e. 7 + 8 + 9 = 24
Hence 1 % 7 = 1
```

一个**简单的解决方案**是首先[计算阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)，然后用[计数方式将阶乘表示为连续数之和的方法数](https://www.geeksforgeeks.org/count-ways-express-number-sum-consecutive-numbers/)表示一个数。此解决方案会导致溢出。
下面是一个**更好的解决方案**避免溢出。
我们考虑将 r 个连续数的和表示为:
(a+1)+(a+2)+(a+3)+……+(a+r)，简化为(r * (r + 2*a + 1)) / 2
因此，(a+1)+(a+2)+(a+3)+……+(a+r)=(r *(r+2 * a+1))/2。由于以上表达式等于阶乘 N，我们将其写成
2 * N！= r * (r + 2*a + 1)
我们不统计所有对(r，a)，而是统计所有对(r，r + 2*a + 1)。现在，我们只是在计算 XY = 2 * N 的所有有序对(X，Y)！其中 X < Y 和 X、Y 具有不同的奇偶性，这意味着如果(r)是偶数，(r + 2*a + 1)是奇数或者如果(r)是奇数那么(r + 2*a + 1)是偶数。这相当于求 2 * N 的奇数除数！这将与 N 的奇数除数相同！。
用于计算 N 中除数！，我们计算因式分解中素数的幂，除数的总数变成(p<sub>1</sub>+1)*(p<sub>2</sub>+1)*……*(p<sub>n</sub>+1)。计算 N 中一个素数的最大幂！，我们将使用[勒让德公式](https://www.geeksforgeeks.org/given-p-and-n-find-the-largest-x-such-that-px-divides-n-2/)。
![\nu _{p}(n!)=\sum _{{i=1}}^{{\infty }}\left\lfloor {\frac {n}{p^{i}}}\right\rfloor,  ](img/ec8a0873ca215e0a543f75b079f33518.png "Rendered by QuickLaTeX.com")
以下是上述方法的实施。

## C++

```
// CPP program to count number of
// ways we can express a factorial
// as sum of consecutive numbers
#include <bits/stdc++.h>
using namespace std;

#define MAX 50002

vector<int> primes;

// sieve of Eratosthenes to compute
// the prime numbers
void sieve()
{
    bool isPrime[MAX];
    memset(isPrime, true, sizeof(isPrime));

    for (int p = 2; p * p < MAX; p++) {
        if (isPrime[p] == true) {
            for (int i = p * 2; i < MAX; i += p)
                isPrime[i] = false;
        }
    }

    // Store all prime numbers
    for (int p = 2; p < MAX; p++)
        if (isPrime[p])
            primes.push_back(p);
}

// function to calculate the largest
// power of a prime in a number
long long int power(long long int x,
                    long long int y)
{
    long long int count = 0;
    long long int z = y;
    while (x >= z) {
        count += (x / z);
        z *= y;
    }
    return count;
}

// Modular multiplication to avoid
// the overflow of multiplication
// Please see below for details
// https://www.geeksforgeeks.org/how-to-avoid-overflow-in-modular-multiplication/
long long int modMult(long long int a,
                      long long int b,
                      long long int mod)
{
    long long int res = 0;
    a = a % mod;
    while (b > 0) {
        if (b % 2 == 1)
            res = (res + a) % mod;
        a = (a * 2) % mod;
        b /= 2;
    }
    return res % mod;
}

// Returns count of ways to express n!
// as sum of consecutives.
long long int countWays(long long int n,
                        long long int m)
{
    long long int ans = 1;

    // We skip 2 (First prime) as we need to
    // consider only odd primes
    for (int i = 1; i < primes.size(); i++) {

        // compute the largest power of prime
        long long int powers = power(n, primes[i]);

        // if the power of current prime number
        // is zero in N!, power of primes greater
        // than current prime number will also
        // be zero, so break out from the loop
        if (powers == 0)
            break;

        // multiply the result at every step
        ans = modMult(ans, powers + 1, m) % m;
    }

    // subtract 1 to exclude the case of 1
    // being an odd divisor
    if (((ans - 1) % m) < 0)
        return (ans - 1 + m) % m;
    else
        return (ans - 1) % m;
}

// Driver Code
int main()
{
    sieve();
    long long int n = 4, m = 7;
    cout << countWays(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of
// ways we can express a factorial
// as sum of consecutive numbers
import java.util.*;

class GFG {

    static int MAX = 50002;
    static ArrayList<Integer> primes
                 = new ArrayList<Integer>();

    // sieve of Eratosthenes to compute
    // the prime numbers
    public static void sieve()
    {

        boolean isPrime[] = new boolean[MAX];

        for(int i = 0; i < MAX; i++)
            isPrime[i] = true;

        for (int p = 2; p * p < MAX; p++) {
            if (isPrime[p] == true) {
                for (int i = p * 2; i < MAX; i += p)
                    isPrime[i] = false;
            }
        }

        // Store all prime numbers
        for (int p = 2; p < MAX; p++)
            if (isPrime[p] == true)
                primes.add(p);
    }

    // function to calculate the largest
    // power of a prime in a number
    public static int power(int x, int y)
    {
        int count = 0;
        int z = y;
        while (x >= z) {
            count += (x / z);
            z *= y;
        }

        return count;
    }

    // Modular multiplication to avoid
    // the overflow of multiplication
    // Please see below for details
    // https://www.geeksforgeeks.org/how-to-avoid-overflow-in-modular-multiplication/
    public static int modMult(int a, int b, int mod)
    {
        int res = 0;
        a = a % mod;
        while (b > 0) {
            if (b % 2 == 1)
                res = (res + a) % mod;
            a = (a * 2) % mod;
            b /= 2;
        }

        return res % mod;
    }

    // Returns count of ways to express n!
    // as sum of consecutives.
    public static int countWays(int n, int m)
    {
        int ans = 1;

        // We skip 2 (First prime) as we need to
        // consider only odd primes
        for (int i = 1; i < primes.size(); i++) {

            // compute the largest power of prime
            int powers = power(n, primes.get(i));

            // if the power of current prime number
            // is zero in N!, power of primes greater
            // than current prime number will also
            // be zero, so break out from the loop
            if (powers == 0)
                break;

            // multiply the result at every step
            ans = modMult(ans, powers + 1, m) % m;
        }

        // subtract 1 to exclude the case of 1
        // being an odd divisor
        if (((ans - 1) % m) < 0)
            return (ans - 1 + m) % m;
        else
            return (ans - 1) % m;
    }

    //Driver function
    public static void main (String[] args) {

        sieve();

        int n = 4, m = 7;

        System.out.println(countWays(n,m));
    }
}

// This code is contributed by akash1295.
```

## 蟒蛇 3

```
# Python 3 program to count number of
# ways we can express a factorial
# as sum of consecutive numbers
MAX = 50002;

primes = []

# sieve of Eratosthenes to compute
# the prime numbers
def sieve():
    isPrime = [True]*(MAX)

    p = 2
    while p * p < MAX :
        if (isPrime[p] == True):
            for i in range( p * 2,MAX, p):
                isPrime[i] = False
        p+=1

    # Store all prime numbers
    for p in range( 2,MAX):
        if (isPrime[p]):
            primes.append(p)

# function to calculate the largest
# power of a prime in a number
def power( x, y):

    count = 0
    z = y
    while (x >= z):
        count += (x // z)
        z *= y

    return count

# Modular multiplication to avoid
# the overflow of multiplication
# Please see below for details
# https://www.geeksforgeeks.org/how-to-avoid-overflow-in-modular-multiplication/
def modMult(a, b,mod):
    res = 0
    a = a % mod
    while (b > 0):
        if (b % 2 == 1):
            res = (res + a) % mod
        a = (a * 2) % mod
        b //= 2

    return res % mod

# Returns count of ways to express n!
# as sum of consecutives.
def countWays(n,m):
    ans = 1

    # We skip 2 (First prime) as we need to
    # consider only odd primes
    for i in range(1,len(primes)):

        # compute the largest power of prime
        powers = power(n, primes[i])

        # if the power of current prime number
        # is zero in N!, power of primes greater
        # than current prime number will also
        # be zero, so break out from the loop
        if (powers == 0):
            break

        # multiply the result at every step
        ans = modMult(ans, powers + 1, m) % m

    # subtract 1 to exclude the case of 1
    # being an odd divisor
    if (((ans - 1) % m) < 0):
        return (ans - 1 + m) % m
    else:
        return (ans - 1) % m

# Driver Code
if __name__ == "__main__":
    sieve()
    n = 4
    m = 7
    print(countWays(n, m))

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to count number of
// ways we can express a factorial
// as sum of consecutive numbers
using System ;
using System.Collections;

class GFG {

    static int MAX = 50002;
    static ArrayList primes = new ArrayList ();

    // sieve of Eratosthenes to compute
    // the prime numbers
    public static void sieve()
    {

        bool []isPrime = new bool[MAX];

        for(int i = 0; i < MAX; i++)
            isPrime[i] = true;

        for (int p = 2; p * p < MAX; p++) {
            if (isPrime[p] == true) {
                for (int i = p * 2; i < MAX; i += p)
                    isPrime[i] = false;
            }
        }

        // Store all prime numbers
        for (int p = 2; p < MAX; p++)
            if (isPrime[p] == true)
                primes.Add(p);
    }

    // function to calculate the largest
    // power of a prime in a number
    public static int power_prime(int x, int y)
    {
        int count = 0;
        int z = y;
        while (x >= z) {
            count += (x / z);
            z *= y;
        }

        return count;
    }

    // Modular multiplication to avoid
    // the overflow of multiplication
    // Please see below for details
    // https://www.geeksforgeeks.org/how-to-avoid-overflow-in-modular-multiplication/
    public static int modMult(int a, int b, int mod)
    {
        int res = 0;
        a = a % mod;
        while (b > 0) {
            if (b % 2 == 1)
                res = (res + a) % mod;
            a = (a * 2) % mod;
            b /= 2;
        }

        return res % mod;
    }

    // Returns count of ways to express n!
    // as sum of consecutives.
    public static int countWays(int n, int m)
    {
        int ans = 1;

        // We skip 2 (First prime) as we need to
        // consider only odd primes
        for (int i = 1; i < primes.Count; i++) {

            // compute the largest power of prime
            int powers = power_prime(n, Convert.ToInt32(primes[i]));

            // if the power of current prime number
            // is zero in N!, power of primes greater
            // than current prime number will also
            // be zero, so break out from the loop
            if (powers == 0)
                break;

            // multiply the result at every step
            ans = modMult(ans, powers + 1, m) % m;
        }

        // subtract 1 to exclude the case of 1
        // being an odd divisor
        if (((ans - 1) % m) < 0)
            return (ans - 1 + m) % m;
        else
            return (ans - 1) % m;
    }

    //Driver function
    public static void Main () {

        sieve();

        int n = 4, m = 7;

        Console.WriteLine(countWays(n,m));
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>
// Javascript program to count number of
// ways we can express a factorial
// as sum of consecutive numbers   
    let MAX = 50002;
    let primes = [];

    // sieve of Eratosthenes to compute
    // the prime numbers
    function sieve()
    {
        let isPrime = new Array(MAX);
        for(let i = 0; i < MAX; i++)
            isPrime[i] = true;
        for (let p = 2; p * p < MAX; p++)
        {
            if (isPrime[p] == true)
            {
                for (let i = p * 2; i < MAX; i += p)
                    isPrime[i] = false;
            }
        }

        // Store all prime numbers
        for (let p = 2; p < MAX; p++)
            if (isPrime[p] == true)
                primes.push(p);
    }

    // function to calculate the largest
    // power of a prime in a number
    function power(x,y)
    {
        let count = 0;
        let z = y;
        while (x >= z) {
            count += Math.floor(x / z);
            z *= y;
        }

        return count;
    }

    // Modular multiplication to avoid
    // the overflow of multiplication
    // Please see below for details
    // https://www.geeksforgeeks.org/how-to-avoid-overflow-in-modular-multiplication/
    function  modMult(a,b,mod)
    {
        let res = 0;
        a = a % mod;
        while (b > 0) {
            if (b % 2 == 1)
                res = (res + a) % mod;
            a = (a * 2) % mod;
            b = Math.floor(b/2);
        }

        return res % mod;
    }

    // Returns count of ways to express n!
    // as sum of consecutives.
    function countWays(n,m)
    {
        let ans = 1;

        // We skip 2 (First prime) as we need to
        // consider only odd primes
        for (let i = 1; i < primes.length; i++) {

            // compute the largest power of prime
            let powers = power(n, primes[i]);

            // if the power of current prime number
            // is zero in N!, power of primes greater
            // than current prime number will also
            // be zero, so break out from the loop
            if (powers == 0)
                break;

            // multiply the result at every step
            ans = modMult(ans, powers + 1, m) % m;
        }

        // subtract 1 to exclude the case of 1
        // being an odd divisor
        if (((ans - 1) % m) < 0)
            return (ans - 1 + m) % m;
        else
            return (ans - 1) % m;
    }

    //Driver function
    sieve();         
    let n = 4, m = 7;
    document.write(countWays(n,m));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
1
```