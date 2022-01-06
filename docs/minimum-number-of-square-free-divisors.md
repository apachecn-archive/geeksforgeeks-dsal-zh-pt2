# 最小平方自由约数

> 原文:[https://www . geesforgeks . org/最小平方自由因子数/](https://www.geeksforgeeks.org/minimum-number-of-square-free-divisors/)

给定一个整数 n，求最小平方自由约数。换句话说，N 的因式分解应该只包括那些平方自由的因子。平方自由数是不能被任何完美平方整除的数(当然，在这种情况下，1 不会被认为是完美平方)。

> **约束:**2≤N≤10<sup>6</sup>T4】

**例:**

> 输入:24
> 输出:3
> **说明:** 24 将表示为 24 = 6×2×2，这里每个因子
> (6 和 2)都是平方自由的。
> **注意:** 24 不能表示为(24 = 12×2)或(24 = 24)或(24 = 8×3)，因为在所有这些因式分解中，每个因式分解都至少有一个不是平方自由的数，即 12、24 和 8 可以被 4 整除(4 是完美平方)。因此最小平方自由因子数是 3。
> 输入:6
> 输出:1
> **说明:** 6 将表示为 6 = 6，因为 6 不能被任何完美的正方形整除。因此最小平方自由因子数是 1。

**先决条件:** [厄拉多塞的筛子](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
A **天真的方法**是考虑 N 个数的所有可能的因式分解，然后检查对于每个因式分解是否存在非平方自由(可被某个完美平方整除)的数。如果它存在，那么丢弃那个因式分解，否则在答案中考虑那个因式分解。考虑所有正确的因式分解后，求最小平方自由因子数。
**高效方法:**通过找到 N 的平方根(最多 10 个 <sup>3</sup> 考虑约束)的所有素因子，构建素筛(使用厄拉多塞的**筛)。现在，考虑所有小于或等于 N 的平方根的质因数，对于每个质因数，找到它在 N 中的最大幂(就像 24 中 2 的最大幂是 3)。现在，我们知道，如果一个质因数的 N 次方大于 1，它就不能与自身分组(例如 2 的 24 次方为 3，因此 2×2 = 4 或 2×2×2 = 8 不能出现在 24 的因式分解中，因为两者都不是平方自由的)，因为它可以被某个完美的平方整除。但是一个质因数和另一个质因数组合在一起(只有一次)永远不会被任何完美的正方形整除。这给了我们一种直觉，答案将是 n 数中所有质因数的最大幂的最大值，换句话说，** 

```
If prime factorization of N = f<sub>1<sup>p1 * f2p2 * ... * fnpn</sup></sub>
where f1, f2 ... fn are the prime factors and p1, p2 ... pn are their 
maximum respective powers in N. Then answer will be,
ans = max(p<sub>1, p2, ..., pn)</sub>
For e.g. 24 = 23 * 31
ans = max(3, 1) = 3
```

下面是解释上述算法
的图解

> 让 **N = 24** 。N 的因式分解可以用许多方法来表示，在这些方法中，我们必须找到最小除数，每个除数都是平方自由的。一些因式分解是:
> 24 = 24 (24 不是平方自由的)
> 24 = 2 * 12 (12 不是平方自由的)
> 24 = 3 * 8 (8 不是平方自由的)
> 24 = 4 * 6 (4 不是平方自由的)
> 24 = 6 * 2 * 2(每个除数都是平方自由的，除数= 3)
> 24 = 3 * 2 * 2 * 2(每个除数都是平方自由的，除数= 4)
> 因此，适当现在如果我们仔细观察，我们不能把一个质因数和它本身组合在一起，而是和另一个质因数组合在一起。就像在这种情况下，2 与 3 组合在一起，使 6(无平方)减少除数。因此，答案将是所有质因数的最大幂的最大值，因为我们至少需要那么多的计数来保持平方自由的条件，并且其他质因数(其幂不是最大的)可以与具有最大幂的质因数分组，以最小化除数的计数。

下面是上述方法的实现。在这里，我们将进行寻找素因子的预处理(使用 screen)，这样我们就可以同时回答许多查询。

## C++

```
// CPP Program to find the minimum
// number of square free divisors
#include <bits/stdc++.h>
using namespace std;

// Initializing MAX with SQRT(10 ^ 6)
#define MAX 1005

void SieveOfEratosthenes(vector<int>& primes)
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    bool prime[MAX];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p < MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i < MAX; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for (int p = 2; p < MAX; p++)
        if (prime[p])
            primes.push_back(p);
}

// This function returns the minimum number of
// Square Free divisors
int minimumSquareFreeDivisors(int N)
{
    vector<int> primes;

    // Precomputing Prime Factors
    SieveOfEratosthenes(primes);

    // holds max of max power of all prime factors
    int max_count = 0;
    for (int i = 0; i < primes.size() && primes[i] * primes[i] <= N; i++) {
        if (N % primes[i] == 0) {

            // holds the max power of current prime factor
            int tmp = 0;
            while (N % primes[i] == 0) {
                tmp++;
                N /= primes[i];
            }
            max_count = max(max_count, tmp);
        }
    }

    // If number itself is prime, it will be included
    // as answer and thus minimum required answer is 1
    if (max_count == 0)
        max_count = 1;

    return max_count;
}

// Driver Code to test above functions
int main()
{
    int N = 24;
    cout << "Minimum Number of Square Free Divisors is "
         << minimumSquareFreeDivisors(N) << endl;

    N = 6;
    cout << "Minimum Number of Square Free Divisors is "
         << minimumSquareFreeDivisors(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the minimum
// number of square free divisors

import java.util.Vector;

public class GFG {

// Initializing MAX with SQRT(10 ^ 6)
    static final int MAX = 1005;

    static void SieveOfEratosthenes(Vector<Integer> primes) {
        // Create a boolean array "prime[0..n]" and initialize
        // all entries it as true. A value in prime[i] will
        // finally be false if i is Not a prime, else true.
        boolean prime[] = new boolean[MAX];
        for (int i = 0; i < prime.length; i++) {
            prime[i] = true;
        }
        for (int p = 2; p * p < MAX; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i < MAX; i += p) {
                    prime[i] = false;
                }
            }
        }

        // Print all prime numbers
        for (int p = 2; p < MAX; p++) {
            if (prime[p]) {
                primes.add(primes.size(), p);
            }
        }
    }

// This function returns the minimum number of
// Square Free divisors
    static int minimumSquareFreeDivisors(int N) {
        Vector<Integer> primes = new Vector<>();

        // Precomputing Prime Factors
        SieveOfEratosthenes(primes);

        // holds max of max power of all prime factors
        int max_count = 0;
        for (int i = 0; i < primes.size() && primes.get(i) *
                         primes.get(i) <= N; i++) {
            if (N % primes.get(i) == 0) {

                // holds the max power of current prime factor
                int tmp = 0;
                while (N % primes.get(i) == 0) {
                    tmp++;
                    N /= primes.get(i);
                }
                max_count = Math.max(max_count, tmp);
            }
        }

        // If number itself is prime, it will be included
        // as answer and thus minimum required answer is 1
        if (max_count == 0) {
            max_count = 1;
        }

        return max_count;
    }

// Driver Code to test above functions
    public static void main(String[] args) {
        int N = 24;
        System.out.println("Minimum Number of Square Free Divisors is "
                + minimumSquareFreeDivisors(N));

        N = 6;
        System.out.println("Minimum Number of Square Free Divisors is "
                + minimumSquareFreeDivisors(N));
    }
}
```

## 蟒蛇 3

```
# Python 3 Program to find the minimum
# number of square free divisors
from math import sqrt

# Initializing MAX with SQRT(10 ^ 6)
MAX = 1005

def SieveOfEratosthenes(primes):

    # Create a boolean array "prime[0..n]" and
    # initialize all entries it as true. A value
    # in prime[i] will finally be false if i is
    # Not a prime, else true.
    prime = [True for i in range(MAX)]

    for p in range(2,int(sqrt(MAX)) + 1, 1):

        # If prime[p] is not changed, then
        # it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, MAX, p):
                prime[i] = False

    # Print all prime numbers
    for p in range(2, MAX, 1):
        if (prime[p]):
            primes.append(p)

    return primes

# This function returns the minimum number
# of Square Free divisors
def minimumSquareFreeDivisors(N):
    prime = []
    primes = []

    # Precomputing Prime Factors
    primes = SieveOfEratosthenes(prime)

    # holds max of max power of all
    # prime factors
    max_count = 0
    i = 0
    while(len(primes) and primes[i] *
                          primes[i] <= N):
        if (N % primes[i] == 0):

            # holds the max power of current
            # prime factor
            tmp = 0
            while (N % primes[i] == 0):
                tmp += 1
                N /= primes[i]

            max_count = max(max_count, tmp)

        i += 1

    # If number itself is prime, it will be included
    # as answer and thus minimum required answer is 1
    if (max_count == 0):
        max_count = 1

    return max_count

# Driver Code
if __name__ == '__main__':
    N = 24
    print("Minimum Number of Square Free Divisors is",
                         minimumSquareFreeDivisors(N))

    N = 6
    print("Minimum Number of Square Free Divisors is",
                         minimumSquareFreeDivisors(N))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# Program to find the minimum
// number of square free divisors

using System;
using System.Collections.Generic;

public class GFG {

// Initializing MAX with SQRT(10 ^ 6)
    static int MAX = 1005;

    static void SieveOfEratosthenes(List<int> primes) {
        // Create a boolean array "prime[0..n]" and initialize
        // all entries it as true. A value in prime[i] will
        // finally be false if i is Not a prime, else true.
        bool []prime = new bool[MAX];
        for (int i = 0; i < prime.Length; i++) {
            prime[i] = true;
        }
        for (int p = 2; p * p < MAX; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i < MAX; i += p) {
                    prime[i] = false;
                }
            }
        }

        // Print all prime numbers
        for (int p = 2; p < MAX; p++) {
            if (prime[p]) {
                primes.Add(p);
            }
        }
    }

// This function returns the minimum number of
// Square Free divisors
    static int minimumSquareFreeDivisors(int N) {
        List<int> primes = new List<int>();

        // Precomputing Prime Factors
        SieveOfEratosthenes(primes);

        // holds max of max power of all prime factors
        int max_count = 0;
        for (int i = 0; i < primes.Count && primes[i] *
                        primes[i] <= N; i++) {
            if (N % primes[i] == 0) {

                // holds the max power of current prime factor
                int tmp = 0;
                while (N % primes[i] == 0) {
                    tmp++;
                    N /= primes[i];
                }
                max_count = Math.Max(max_count, tmp);
            }
        }

        // If number itself is prime, it will be included
        // as answer and thus minimum required answer is 1
        if (max_count == 0) {
            max_count = 1;
        }

        return max_count;
    }

// Driver Code to test above functions
    public static void Main(){
        int N = 24;
        Console.WriteLine("Minimum Number of Square Free Divisors is "
                + minimumSquareFreeDivisors(N));

        N = 6;
        Console.WriteLine("Minimum Number of Square Free Divisors is "
                + minimumSquareFreeDivisors(N));
    }
    // This code is contributed by Ryuga
}
```

## java 描述语言

```
<script>
    // Javascript Program to find the minimum
    // number of square free divisors

    // Initializing MAX with SQRT(10 ^ 6)
    let MAX = 1005;

    function SieveOfEratosthenes(primes) {
        // Create a boolean array "prime[0..n]" and initialize
        // all entries it as true. A value in prime[i] will
        // finally be false if i is Not a prime, else true.
        let prime = new Array(MAX);
        for (let i = 0; i < prime.length; i++) {
            prime[i] = true;
        }
        for (let p = 2; p * p < MAX; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (let i = p * 2; i < MAX; i += p) {
                    prime[i] = false;
                }
            }
        }

        // Print all prime numbers
        for (let p = 2; p < MAX; p++) {
            if (prime[p]) {
                primes.push(p);
            }
        }
    }

    // This function returns the minimum number of
    // Square Free divisors
    function minimumSquareFreeDivisors(N) {
        let primes = [];

        // Precomputing Prime Factors
        SieveOfEratosthenes(primes);

        // holds max of max power of all prime factors
        let max_count = 0;
        for (let i = 0; i < primes.length && primes[i] *
                        primes[i] <= N; i++) {
            if (N % primes[i] == 0) {

                // holds the max power of current prime factor
                let tmp = 0;
                while (N % primes[i] == 0) {
                    tmp++;
                    N = parseInt(N / primes[i], 10);
                }
                max_count = Math.max(max_count, tmp);
            }
        }

        // If number itself is prime, it will be included
        // as answer and thus minimum required answer is 1
        if (max_count == 0) {
            max_count = 1;
        }

        return max_count;
    }

    let N = 24;
    document.write("Minimum Number of Square Free Divisors is "
                      + minimumSquareFreeDivisors(N) + "</br>");

    N = 6;
    document.write("Minimum Number of Square Free Divisors is "
                      + minimumSquareFreeDivisors(N));

    // This code is contributed by suresh07.
</script>
```

**输出:**

```
Minimum Number of Square Free Divisors is 3
Minimum Number of Square Free Divisors is 1
```