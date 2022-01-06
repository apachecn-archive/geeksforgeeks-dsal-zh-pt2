# 范围[L，R]内与 N 相对素数的自然数的计数

> 原文:[https://www . geeksforgeeks . org/范围内自然数计数-l-r-哪些是-n 的相对素数/](https://www.geeksforgeeks.org/count-of-natural-numbers-in-range-l-r-which-are-relatively-prime-with-n/)

给定三个整数 **N、L 和 R** 。任务是计算范围[L，R](包括两者)内与 n 相对素数的自然数的个数。

**示例:**

> **输入:** N = 10，L = 1，R = 25
> **输出:** 10
> **说明:**
> 10 个自然数(在 1 到 25 的范围内)相对于 10 是素数。
> 它们是 1、3、7、9、11、13、17、19、21、23。
> 
> **输入:** N = 12，L = 7，R = 38
> **输出:** 11
> **说明:**
> 11 个自然数(在 1 到 38 的范围内)相对于 12 是素数。
> 分别是 7、11、13、17、19、23、25、29、31、35、37。

**进场:**

1.  首先，对数 n 进行因式分解，从而找出 n 的所有素因子
2.  在数组中存储 N 的质因数。
3.  我们可以确定不大于 R 且能被 n 的质因数整除的自然数的总数。
4.  假设值是 y，所以，不大于 R 的 y 个自然数至少有一个公约数为 n。
5.  所以，这些 y 数不能相对于 n 是质数。
6.  因此，相对于 N 为素数的不大于 R 的自然数的个数将是 R–y。
7.  现在，类似地，我们需要找出不大于 L-1 的 N 的相对素数的个数。
8.  然后，用 r 的答案减去 L-1 的结果。

下面是上述方法的实现:

## C++

```
// C++ code to count of natural
// numbers in range [L, R] which
// are relatively prime with N

#include <bits/stdc++.h>
using namespace std;
#define maxN (long long)1000000000000

// container of all the primes
// up to sqrt(n)
vector<int> prime;

// Function to calculate prime
// factors of n
void sieve(long long n)
{
    // run the sieve of Eratosthenes
    bool check[1000007] = { 0 };
    long long i, j;

    // 0(false) means prime,
    // 1(true) means not prime
    check[0] = 1, check[1] = 1,
    check[2] = 0;

    // no even number is
    // prime except for 2
    for (i = 4; i <= n; i += 2)
        check[i] = true;

    for (i = 3; i * i <= n; i += 2)
        if (!check[i]) {

            // all the multiples of each
            // each prime numbers are
            // non-prime
            for (j = i * i; j <= n; j += 2 * i)
                check[j] = true;
        }

    prime.push_back(2);

    // get all the primes
    // in prime vector
    for (int i = 3; i <= n; i += 2)
        if (!check[i])
            prime.push_back(i);

    return;
}

// Count the number of numbers
// up to m which are divisible
// by given prime numbers
long long count(long long a[],
                int n, long long m)
{
    long long parity[3] = { 0 };

    // Run from i= 000..0 to i= 111..1
    // or check all possible
    // subsets of the array
    for (int i = 1; i < (1 << n); i++) {
        long long mult = 1;
        for (int j = 0; j < n; j++)
            if (i & (1 << j))
                mult *= a[j];

        // take the multiplication
        // of all the set bits

        // if the number of set bits
        // is odd, then add to the
        // number of multiples
        parity[__builtin_popcount(i) & 1]
            += (m / mult);
    }

    return parity[1] - parity[0];
}

// Function calculates all number
// not greater than 'm' which are
// relatively prime with n.
long long countRelPrime(
    long long n,
    long long m)
{

    long long a[20];
    int i = 0, j = 0;
    long long pz = prime.size();
    while (n != 1 && i < pz) {

        // if square of the prime number
        // is greater than 'n', it can't
        // be a factor of 'n'
        if ((long long)prime[i]
                * (long long)prime[i]
            > n)
            break;

        // if prime is a factor of
        // n then increment count
        if (n % prime[i] == 0)
            a[j] = (long long)prime[i], j++;

        while (n % prime[i] == 0)
            n /= prime[i];
        i++;
    }

    if (n != 1)
        a[j] = n, j++;
    return m - count(a, j, m);
}

void countRelPrimeInRange(
    long long n, long long l,
    long long r)
{
    sieve(sqrt(maxN));
    long long result
        = countRelPrime(n, r)
          - countRelPrime(n, l - 1);
    cout << result << "\n";
}

// Driver code
int main()
{
    long long N = 7, L = 3, R = 9;
    countRelPrimeInRange(N, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count of natural
// numbers in range [L, R] which
// are relatively prime with N
import java.util.*;

class GFG{

static int maxN = 100000000;

// Container of all the primes
// up to sqrt(n)
static Vector<Integer> prime = new Vector<Integer>();

// Function to calculate prime
// factors of n
static void sieve(int n)
{

    // Run the sieve of Eratosthenes
    boolean[] check = new boolean[1000007];
    for(int i = 0; i < 1000007; i++)
        check[i] = false;

    int i, j;

    // 0(false) means prime,
    // 1(true) means not prime
    check[0] = false;
    check[1] = true;
    check[2] = false;

    // No even number is
    // prime except for 2
    for(i = 4; i <= n; i += 2)
        check[i] = true;

    for(i = 3; i * i <= n; i += 2)
        if (!check[i])
        {

            // All the multiples of each
            // each prime numbers are
            // non-prime
            for(j = i * i; j <= n; j += 2 * i)
                check[j] = true;
        }

    prime.add(2);

    // Get all the primes
    // in prime vector
    for(i = 3; i <= n; i += 2)
        if (!check[i])
            prime.add(i);

    return;
}

static int countSetBits(int n)
{
    int count = 0;
    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Count the number of numbers
// up to m which are divisible
// by given prime numbers
static int count(int a[],
                 int n, int m)
{
    int[] parity = new int[3];
    for(int i = 0; i < 3; i++)
        parity[i] = 0;

    // Run from i= 000..0 to i= 111..1
    // or check all possible
    // subsets of the array
    for(int i = 1; i < (1 << n); i++)
    {
        int mult = 1;
        for(int j = 0; j < n; j++)
            if ((i & (1 << j)) != 0)
                mult *= a[j];

        // Take the multiplication
        // of all the set bits

        // If the number of set bits
        // is odd, then add to the
        // number of multiples
        parity[countSetBits(i) & 1] += (m / mult);
    }
    return parity[1] - parity[0];
}

// Function calculates all number
// not greater than 'm' which are
// relatively prime with n.
static int countRelPrime(int n, int m)
{
    int[] a = new int[20];
    int i = 0, j = 0;
    int pz = prime.size();

    while(n != 1 && i < pz)
    {

        // If square of the prime number
        // is greater than 'n', it can't
        // be a factor of 'n'
        if ((int)prime.get(i) *
            (int)prime.get(i) > n)
            break;

        // If prime is a factor of
        // n then increment count
        if (n % prime.get(i) == 0)
        {
            a[j] = (int)prime.get(i);
            j++;
        }

        while (n % prime.get(i) == 0)
            n /= prime.get(i);

        i++;
    }

    if (n != 1)
    {
        a[j] = n;
        j++;
    }
    return m - count(a, j, m);
}

static void countRelPrimeInRange(int n, int l,
                                 int r)
{
    sieve((int)Math.sqrt(maxN));

    int result = countRelPrime(n, r) -
                 countRelPrime(n, l - 1);

    System.out.println(result);
}

// Driver code
public static void main(String[] args)
{
    int N = 7, L = 3, R = 9;

    countRelPrimeInRange(N, L, R);
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 code to count of natural
# numbers in range [L, R] which
# are relatively prime with N
from math import sqrt, floor

maxN = 1000000000000

# Container of all the primes
# up to sqrt(n)
prime = []

# Function to calculate prime
# factors of n
def sieve(n):

    # Run the sieve of Eratosthenes
    check = [0] * (1000007)
    i, j = 0, 0

    # 0(false) means prime,
    # 1(True) means not prime
    check[0] = 1
    check[1] = 1
    check[2] = 0

    # No even number is
    # prime except for 2
    for i in range(4, n + 1, 2):
        check[i] = True

    for i in range(3, n + 1, 2):
        if i * i > n:
            break
        if (not check[i]):

            # All the multiples of each
            # each prime numbers are
            # non-prime
            for j in range(2 * i, n + 1, 2 * i):
                check[j] = True

    prime.append(2)

    # Get all the primes
    # in prime vector
    for i in range(3, n + 1, 2):
        if (not check[i]):
            prime.append(i)

    return

# Count the number of numbers
# up to m which are divisible
# by given prime numbers
def count(a, n, m):

    parity = [0] * 3

    # Run from i = 000..0 to i = 111..1
    # or check all possible
    # subsets of the array
    for i in range(1, 1 << n):
        mult = 1
        for j in range(n):
            if (i & (1 << j)):
                mult *= a[j]

        # Take the multiplication
        # of all the set bits

        # If the number of set bits
        # is odd, then add to the
        # number of multiples
        parity[bin(i).count('1') & 1] += (m // mult)

    return parity[1] - parity[0]

# Function calculates all number
# not greater than 'm' which are
# relatively prime with n.
def countRelPrime(n, m):

    a = [0] * 20
    i = 0
    j = 0
    pz = len(prime)
    while (n != 1 and i < pz):

        # If square of the prime number
        # is greater than 'n', it can't
        # be a factor of 'n'
        if (prime[i] * prime[i] > n):
            break

        # If prime is a factor of
        # n then increment count
        if (n % prime[i] == 0):
            a[j] = prime[i]
            j += 1

        while (n % prime[i] == 0):
            n //= prime[i]
        i += 1

    if (n != 1):
        a[j] = n
        j += 1
    return m - count(a, j, m)

def countRelPrimeInRange(n, l, r):

    sieve(floor(sqrt(maxN)))
    result = (countRelPrime(n, r) -
              countRelPrime(n, l - 1))
    print(result)

# Driver code
if __name__ == '__main__':

    N = 7
    L = 3
    R = 9

    countRelPrimeInRange(N, L, R)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# code to count of natural
// numbers in range [L, R] which
// are relatively prime with N
using System;
using System.Collections.Generic;

class GFG{

static int maxN = 100000000;

// Container of all the primes
// up to sqrt(n)
static List<int> prime = new List<int>();

// Function to calculate prime
// factors of n
static void sieve(int n)
{

    // Run the sieve of Eratosthenes
    bool[] check = new bool[1000007];
    for(int I = 0; I < 1000007; I++)
        check[I] = false;

    int i, j;

    // 0(false) means prime,
    // 1(true) means not prime
    check[0] = false;
    check[1] = true;
    check[2] = false;

    // No even number is
    // prime except for 2
    for(i = 4; i <= n; i += 2)
        check[i] = true;

    for(i = 3; i * i <= n; i += 2)
        if (!check[i])
        {

            // All the multiples of each
            // each prime numbers are
            // non-prime
            for(j = i * i; j <= n; j += 2 * i)
                check[j] = true;
        }

    prime.Add(2);

    // Get all the primes
    // in prime vector
    for(i = 3; i <= n; i += 2)
        if (!check[i])
            prime.Add(i);

    return;
}

static int countSetBits(int n)
{
    int count = 0;

    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Count the number of numbers
// up to m which are divisible
// by given prime numbers
static int count(int[] a, int n, int m)
{
    int[] parity = new int[3];
    for(int i = 0; i < 3; i++)
        parity[i] = 0;

    // Run from i= 000..0 to i= 111..1
    // or check all possible
    // subsets of the array
    for(int i = 1; i < (1 << n); i++)
    {
        int mult = 1;
        for(int j = 0; j < n; j++)
            if ((i & (1 << j)) != 0)
                mult *= a[j];

        // Take the multiplication
        // of all the set bits

        // If the number of set bits
        // is odd, then add to the
        // number of multiples
        parity[countSetBits(i) & 1] += (m / mult);
    }
    return parity[1] - parity[0];
}

// Function calculates all number
// not greater than 'm' which are
// relatively prime with n.
static int countRelPrime(int n, int m)
{
    int[] a = new int[20];
    int i = 0, j = 0;
    int pz = prime.Count;

    while (n != 1 && i < pz)
    {

        // If square of the prime number
        // is greater than 'n', it can't
        // be a factor of 'n'
        if ((int)prime[i] * (int)prime[i] > n)
            break;

        // If prime is a factor of
        // n then increment count
        if (n % prime[i] == 0)
        {
            a[j] = (int)prime[i];
            j++;
        }

        while (n % prime[i] == 0)
            n /= prime[i];

        i++;
    }

    if (n != 1)
    {
        a[j] = n;
        j++;
    }
    return m - count(a, j, m);
}

static void countRelPrimeInRange(int n, int l,
                                 int r)
{
    sieve((int)Math.Sqrt(maxN));

    int result = countRelPrime(n, r) -
                 countRelPrime(n, l - 1);

    Console.WriteLine(result);
}

// Driver Code
static void Main()
{
    int N = 7, L = 3, R = 9;

    countRelPrimeInRange(N, L, R);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript code to count of natural
// numbers in range [L, R] which
// are relatively prime with N
let maxN = 100000000;

// Container of all the primes
// up to sqrt(n)
let prime = [];

// Function to calculate prime
// factors of n
function sieve(n)
{

    // Run the sieve of Eratosthenes
    let check = new Array(1000007);
    for(let i = 0; i < 1000007; i++)
        check[i] = false;

    let i, j;

    // 0(false) means prime,
    // 1(true) means not prime
    check[0] = false;
    check[1] = true;
    check[2] = false;

    // No even number is
    // prime except for 2
    for(i = 4; i <= n; i += 2)
        check[i] = true;

    for(i = 3; i * i <= n; i += 2)
        if (!check[i])
        {

            // All the multiples of each
            // each prime numbers are
            // non-prime
            for(j = i * i; j <= n; j += 2 * i)
                check[j] = true;
        }

    prime.push(2);

    // Get all the primes
    // in prime vector
    for(i = 3; i <= n; i += 2)
        if (!check[i])
            prime.push(i);

    return;
}

function countSetBits(n)
{
    let count = 0;
    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Count the number of numbers
// up to m which are divisible
// by given prime numbers
function count(a, n, m)
{
    let parity = new Array(3);
    for(let i = 0; i < 3; i++)
        parity[i] = 0;

    // Run from i= 000..0 to i= 111..1
    // or check all possible
    // subsets of the array
    for(let i = 1; i < (1 << n); i++)
    {
        let mult = 1;
        for(let j = 0; j < n; j++)
            if ((i & (1 << j)) != 0)
                mult *= a[j];

        // Take the multiplication
        // of all the set bits

        // If the number of set bits
        // is odd, then add to the
        // number of multiples
        parity[countSetBits(i) & 1] += (m / mult);
    }
    return parity[1] - parity[0];
}

// Function calculates all number
// not greater than 'm' which are
// relatively prime with n.
function countRelPrime(n, m)
{
    let a = new Array(20);
    let i = 0, j = 0;
    let pz = prime.length;

    while(n != 1 && i < pz)
    {

        // If square of the prime number
        // is greater than 'n', it can't
        // be a factor of 'n'
        if (prime[i] *
            prime[i] > n)
            break;

        // If prime is a factor of
        // n then increment count
        if (n % prime[i] == 0)
        {
            a[j] = prime[i];
            j++;
        }

        while (n % prime[i] == 0)
            n = Math.floor(n/prime[i]);

        i++;
    }

    if (n != 1)
    {
        a[j] = n;
        j++;
    }
    return m - count(a, j, m);
}

function countRelPrimeInRange(n, l, r)
{
    sieve(Math.floor(Math.sqrt(maxN)));

    let result = countRelPrime(n, r) -
                 countRelPrime(n, l - 1);

    document.write(result);
}

// Driver code
let N = 7, L = 3, R = 9;

countRelPrimeInRange(N, L, R);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
6
```