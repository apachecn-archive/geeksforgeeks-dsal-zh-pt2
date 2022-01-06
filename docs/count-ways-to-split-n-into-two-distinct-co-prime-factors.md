# 计数分割 N 的方式！分为两个不同的共同质因数

> 原文:[https://www . geesforgeks . org/count-way-to-split-n-in-two-distinct-co-prime-factors/](https://www.geeksforgeeks.org/count-ways-to-split-n-into-two-distinct-co-prime-factors/)

给定一个整数 **N** ，任务是找到[T3【N】的路数！](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/) 可以分为两个不同的因素 **A** 和 **B** ，这样 **A** 和 **B** 就是[共质数](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)。既然答案可以很大，那就打印出来[模 10 <sup>9</sup> + 7](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

**示例:**

> **输入:** N = 5
> **输出:** 4
> **说明:**对为(1，120)、(3，40)、(5，24)、(8，15)。
> 
> **输入:** N = 7
> **输出:** 8
> **说明:**对为(1，5040)，(5，1008)，(7，720)，(9，560)，(16，315)，(35，144)，(45，112)，(63，80)。

**天真法:**最简单的方法就是[计算 **N 的阶乘！**](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/) 并生成其所有因子，检查任意一对因子 **(i，j)** 是否有 [**GCD**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) **(i，j) == 1** 。

***时间复杂度:** O(√N！)*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，思路是[找到 N](https://www.geeksforgeeks.org/number-of-distinct-prime-factors-of-first-n-natural-numbers/) 的不同素因子，然后通过计数的方式将其拆分为两个不同的[共素因子](https://www.geeksforgeeks.org/generate-k-co-prime-pairs-of-factors-of-a-given-number/)T6】A&T8】B。按照以下步骤解决问题:

*   每个正整数都可以表示为素数幂的乘积([素数因式分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/))。因此 **N** 的每一个可能值都可以表示为**N = 2<sup>p</sup>×3<sup>q</sup>×5<sup>r</sup>…..(p ≥ 0，q ≥ 0，r ≥ 0)** 。
*   现在，任务是将 **N** 分成两个不同的共素因子。这可以通过每次将**N**T5 的[素因子分解中的每个项分配到两个可能的组合中来实现。](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)

插图:

> 让 **N = 18900** 。
> 以素因子的形式表示 N，**18900 = 2<sup>2</sup>* 3<sup>3</sup>* 5<sup>2</sup>* 7<sup>1</sup>**
> 
> **2<sup>2</sup>3<sup>3</sup>5<sup>2</sup>T7】和**7<sup>1</sup>T11】中的每一个都可以分配给这两个因素中的任何一个。使用[组合学](https://www.geeksforgeeks.org/mathematics-combinatorics-basics/)中的积法则，总的可能途径是**2<sup>4</sup>**=**16**。由于这两个因素没有顺序，总的可能方式是 **2 <sup>3</sup> = 8** 。因此 **N** 的路数为**2<sup>X–1</sup>**，其中 **X** 为 **N** 的素因子数。****

按照以下步骤解决问题:

1.  **N 的素分解！**包含所有小于或等于 **N** 的素数。
2.  如果 **x** 是小于等于 **N** 的素数，那么路数 **N！**(阶乘)可以拆分成两个不同的同素因子等于**2<sup>x–1</sup>**。
3.  使用埃拉托斯特尼的[筛预计算素数 **∀ n ≤ N** ,并将它们存储在数组中。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
4.  以 **10 <sup>9</sup> + 7** 为模计算结果，使用[模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)，即计算 **x <sup>y</sup> % p** 。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Maximum value of N
#define MAXN 1000000

// Stores at each indices if
// given number is prime or not
int is_prime[MAXN] = { 0 };

// Stores count_of_primes
int count_of_primes[MAXN] = { 0 };

// Function to generate primes
// using Sieve of Eratsothenes
void sieve()
{
    for (int i = 3; i < MAXN; i += 2) {

        // Assume all odds are primes
        is_prime[i] = 1;
    }

    for (int i = 3; i * i < MAXN; i += 2) {

        // If a prime is encountered
        if (is_prime[i])

            for (int j = i * i; j < MAXN;
                 j += i) {

                // Mark all its multiples
                // as non-prime
                is_prime[j] = 0;
            }
    }

    is_prime[2] = 1;

    // Count primes <= MAXN
    for (int i = 1; i < MAXN; i++)
        count_of_primes[i]
            = count_of_primes[i - 1]
              + is_prime[i];
}

// Function to calculate (x ^ y) % p
// in O(log y)
long long int power(long long int x,
                    long long int y,
                    long long int p)
{
    long long result = 1;
    while (y > 0) {
        if (y & 1 == 1)
            result = (result * x) % p;
        x = (x * x) % p;
        y >>= 1;
    }
    return result;
}

// Utility function to count the number of ways
// N! can be split into co-prime factors
void numberOfWays(int N)
{
    long long int count
        = count_of_primes[N] - 1;
    long long int mod = 1000000007;
    long long int answer
        = power(2, count, mod);

    if (N == 1)
        answer = 0;

    cout << answer;
}

// Driver Code
int main()
{
    // Calling sieve function
    sieve();

    // Given N
    int N = 7;

    // Function call
    numberOfWays(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;

class GFG {

    // Maximum value of N
    static final int MAXN = 1000000;

    // Stores at each indices if
    // given number is prime or not
    static int is_prime[];

    // Stores count_of_primes
    static int count_of_primes[];

    // Function to generate primes
    // using Sieve of Eratsothenes
    static void sieve()
    {
        is_prime = new int[MAXN];
        count_of_primes = new int[MAXN];
        Arrays.fill(is_prime, 0);
        Arrays.fill(count_of_primes, 0);

        for (int i = 3; i < MAXN; i += 2) {

            // Assume all odds are primes
            is_prime[i] = 1;
        }

        for (int i = 3; i * i < MAXN; i += 2) {

            // If a prime is encountered
            if (is_prime[i] == 1) {
                for (int j = i * i; j < MAXN;
                     j += i) {
                    // MArk all its multiples
                    // as non-prime
                    is_prime[j] = 0;
                }
            }
        }

        is_prime[2] = 1;

        // Count all primes upto MAXN
        for (int i = 1; i < MAXN; i++)
            count_of_primes[i]
                = count_of_primes[i - 1] + is_prime[i];
    }

    // Function to calculate (x ^ y) % p
    // in O(log y)
    static long power(long x, long y, long p)
    {
        long result = 1;
        while (y > 0) {
            if ((y & 1) == 1)
                result = (result * x) % p;
            x = (x * x) % p;
            y >>= 1;
        }
        return result;
    }

    // Utility function to count the number of
    // ways N! can be split into two co-prime factors
    static void numberOfWays(int N)
    {
        long count = count_of_primes[N] - 1;
        long mod = 1000000007;
        long answer = power(2, count, mod);
        if (N == 1)
            answer = 0;
        long ans = answer;
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Calling sieve function
        sieve();

        // Given N
        int N = 7;

        // Function call
        numberOfWays(N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Maximum value of N
MAXN = 1000000

# Stores at each indices if
# given number is prime or not
is_prime = [0] * MAXN

# Stores count_of_primes
count_of_primes = [0] * MAXN

# Function to generate primes
# using Sieve of Eratsothenes
def sieve():

    for i in range(3, MAXN, 2):

        # Assume all odds are primes
        is_prime[i] = 1

    for i in range(3, int(math.sqrt(MAXN)), 2):

        # If a prime is encountered
        if is_prime[i]:
            for j in range(i * i, MAXN, i):

                # Mark all its multiples
                # as non-prime
                is_prime[j] = 0

    is_prime[2] = 1

    # Count primes <= MAXN
    for i in range(1, MAXN):
        count_of_primes[i] = (count_of_primes[i - 1] +
                                     is_prime[i])

# Function to calculate (x ^ y) % p
# in O(log y)
def power(x, y, p):

    result = 1
    while (y > 0):
        if y & 1 == 1:
            result = (result * x) % p

        x = (x * x) % p
        y >>= 1

    return result

# Utility function to count the number of ways
# N! can be split into co-prime factors
def numberOfWays(N):

    count = count_of_primes[N] - 1
    mod = 1000000007
    answer = power(2, count, mod)

    if N == 1:
        answer = 0

    print(answer)

# Driver Code
if __name__ == "__main__":

    # Calling sieve function
    sieve()

    # Given N
    N = 7

    # Function call
    numberOfWays(N)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Maximum value of N
static int MAXN = 1000000;

// Stores at each indices if
// given number is prime or not
static int[] is_prime;

// Stores count_of_primes
static int[] count_of_primes;

// Function to generate primes
// using Sieve of Eratsothenes
static void sieve()
{
    is_prime = new int[MAXN];
    count_of_primes = new int[MAXN];
    Array.Fill(is_prime, 0);
    Array.Fill(count_of_primes, 0);

    for(int i = 3; i < MAXN; i += 2)
    {

        // Assume all odds are primes
        is_prime[i] = 1;
    }

    for(int i = 3; i * i < MAXN; i += 2)
    {

        // If a prime is encountered
        if (is_prime[i] == 1)
        {
            for(int j = i * i; j < MAXN; j += i)
            {

                // MArk all its multiples
                // as non-prime
                is_prime[j] = 0;
            }
        }
    }

    is_prime[2] = 1;

    // Count all primes upto MAXN
    for(int i = 1; i < MAXN; i++)
        count_of_primes[i] = count_of_primes[i - 1] +
                                    is_prime[i];
}

// Function to calculate (x ^ y) % p
// in O(log y)
static long power(long x, long y, long p)
{
    long result = 1;
    while (y > 0)
    {
        if ((y & 1) == 1)
            result = (result * x) % p;

        x = (x * x) % p;
        y >>= 1;
    }
    return result;
}

// Utility function to count the number of
// ways N! can be split into two co-prime factors
static void numberOfWays(int N)
{
    long count = count_of_primes[N] - 1;
    long mod = 1000000007;
    long answer = power(2, count, mod);

    if (N == 1)
        answer = 0;

    long ans = answer;
    Console.Write(ans);
}

// Driver Code
public static void Main()
{

    // Calling sieve function
    sieve();

    // Given N
    int N = 7;

    // Function call
    numberOfWays(N);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript Program for the above approach

// Maximum value of N
var MAXN = 1000000

// Stores at each indices if
// given number is prime or not
var is_prime = Array(MAXN).fill(0);

// Stores count_of_primes
var count_of_primes = Array(MAXN).fill(0);

// Function to generate primes
// using Sieve of Eratsothenes
function sieve()
{
    for (var i = 3; i < MAXN; i += 2) {

        // Assume all odds are primes
        is_prime[i] = 1;
    }

    for (var i = 3; i * i < MAXN; i += 2) {

        // If a prime is encountered
        if (is_prime[i])

            for (var j = i * i; j < MAXN;
                 j += i) {

                // Mark all its multiples
                // as non-prime
                is_prime[j] = 0;
            }
    }

    is_prime[2] = 1;

    // Count primes <= MAXN
    for (var i = 1; i < MAXN; i++)
        count_of_primes[i]
            = count_of_primes[i - 1]
              + is_prime[i];
}

// Function to calculate (x ^ y) % p
// in O(log y)
function power(x, y, p)
{
    var result = 1;
    while (y > 0) {
        if (y & 1 == 1)
            result = (result * x) % p;
        x = (x * x) % p;
        y >>= 1;
    }
    return result;
}

// Utility function to count the number of ways
// N! can be split into co-prime factors
function numberOfWays(N)
{
    var count
        = count_of_primes[N] - 1;
    var mod = 1000000007;
    var answer
        = power(2, count, mod);

    if (N == 1)
        answer = 0;

    document.write( answer);
}

// Driver Code
// Calling sieve function
sieve();
// Given N
var N = 7;
// Function call
numberOfWays(N);

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(log(log(N))+log(N))*
T5**辅助空间:** O(N)