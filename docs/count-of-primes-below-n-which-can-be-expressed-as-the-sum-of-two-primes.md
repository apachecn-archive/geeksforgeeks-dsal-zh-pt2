# N 以下的素数计数，可以表示为两个素数之和

> 原文:[https://www . geesforgeks . org/质数-n 以下-哪些可以表示为两个质数之和/](https://www.geeksforgeeks.org/count-of-primes-below-n-which-can-be-expressed-as-the-sum-of-two-primes/)

给定一个整数 **N** ，任务是求 **N** 以下所有素数的个数，可以表示为两个素数之和。
**例:**

> **输入:** N = 6
> **输出:** 1
> 5 是唯一一个低于 6 的质数。
> 2 + 3 = 5。
> **输入:** N = 11
> **输出:** 2

**方法:**使用厄拉多塞的[筛创建一个数组 prime【】，其中 prime【I】将存储我是否是 prime。现在，对于范围[1，N–1]中的每个素数，使用这里讨论的方法](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)检查它是否可以表示为两个素数的和。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100005;
bool prime[MAX];

// Function for Sieve of Eratosthenes
void SieveOfEratosthenes()
{
    memset(prime, true, sizeof(prime));

    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the count of primes
// less than or equal to n which can be
// expressed as the sum of two primes
int countPrimes(int n)
{
    SieveOfEratosthenes();

    // To store the required count
    int cnt = 0;

    for (int i = 2; i < n; i++) {

        // If the integer is prime and it
        // can be expressed as the sum of
        // 2 and a prime number
        if (prime[i] && prime[i - 2])
            cnt++;
    }

    return cnt;
}

// Driver code
int main()
{
    int n = 11;

    cout << countPrimes(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int MAX = 100005;
static boolean []prime = new boolean[MAX];

// Function for Sieve of Eratosthenes
static void SieveOfEratosthenes()
{

    for (int i = 0; i < MAX; i++)
        prime[i] = true;

    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p < MAX; p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {
            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the count of primes
// less than or equal to n which can be
// expressed as the sum of two primes
static int countPrimes(int n)
{
    SieveOfEratosthenes();

    // To store the required count
    int cnt = 0;

    for (int i = 2; i < n; i++)
    {
        // If the integer is prime and it
        // can be expressed as the sum of
        // 2 and a prime number
        if (prime[i] && prime[i - 2])
            cnt++;
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int n = 11;

    System.out.print(countPrimes(n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 100005
prime = [True for i in range(MAX)]

# Function for Sieve of Eratosthenes
def SieveOfEratosthenes():

    # False here indicates
    # that it is not prime
    prime[0] = False
    prime[1] = False

    for p in range(MAX):

        if(p * p > MAX):
            break

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p,
            # set them to non-prime
            for i in range(2 * p, MAX, p):
                prime[i] = False

# Function to return the count of primes
# less than or equal to n which can be
# expressed as the sum of two primes
def countPrimes(n):
    SieveOfEratosthenes()

    # To store the required count
    cnt = 0

    for i in range(2, n):

        # If the integer is prime and it
        # can be expressed as the sum of
        # 2 and a prime number
        if (prime[i] and prime[i - 2]):
            cnt += 1

    return cnt

# Driver code
n = 11

print(countPrimes(n))

# This code is contributed by Mohit Kumar
```

## C#

```
    // C# implementation of the approach
using System;

class GFG
{
static int MAX = 100005;
static bool []prime = new bool[MAX];

// Function for Sieve of Eratosthenes
static void SieveOfEratosthenes()
{
    for (int i = 0; i < MAX; i++)
        prime[i] = true;

    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p < MAX; p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {
            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the count of primes
// less than or equal to n which can be
// expressed as the sum of two primes
static int countPrimes(int n)
{
    SieveOfEratosthenes();

    // To store the required count
    int cnt = 0;

    for (int i = 2; i < n; i++)
    {
        // If the integer is prime and it
        // can be expressed as the sum of
        // 2 and a prime number
        if (prime[i] && prime[i - 2])
            cnt++;
    }
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int n = 11;

    Console.Write(countPrimes(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
var MAX = 100005;
var prime = new Array(MAX).fill(false);

    // Function for Sieve of Eratosthenes
    function SieveOfEratosthenes()
    {
        for (i = 0; i < MAX; i++)
            prime[i] = true;

        // false here indicates
        // that it is not prime
        prime[0] = false;
        prime[1] = false;

        for (p = 2; p * p < MAX; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p])
            {

                // Update all multiples of p,
                // set them to non-prime
                for (i = p * 2; i < MAX; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to return the count of primes
    // less than or equal to n which can be
    // expressed as the sum of two primes
    function countPrimes(n)
    {
        SieveOfEratosthenes();

        // To store the required count
        var cnt = 0;
        for (i = 2; i < n; i++)
        {

            // If the integer is prime and it
            // can be expressed as the sum of
            // 2 and a prime number
            if (prime[i] && prime[i - 2])
                cnt++;
        }
        return cnt;
    }

    // Driver code
        var n = 11;
        document.write(countPrimes(n));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
2
```