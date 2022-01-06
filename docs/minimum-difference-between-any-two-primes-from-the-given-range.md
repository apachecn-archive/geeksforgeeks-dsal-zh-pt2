# 给定范围内任意两个素数之间的最小差

> 原文:[https://www . geeksforgeeks . org/给定范围内任意两个素数的最小差/](https://www.geeksforgeeks.org/minimum-difference-between-any-two-primes-from-the-given-range/)

给定两个整数 **L** 和 **R** ，任务是找出范围**【L，R】**内任意两个质数的最小差。

**示例:**

> **输入:** L = 21，R = 50
> **输出:** 2
> (29，31)和(41，43)是唯一给出最小差异的有效对
> 。
> 
> **输入:** L = 1，R = 11
> **输出:**1
> (2，3)之差最小。

**进场:**

*   使用厄拉多塞的[筛找出所有到 **R** 的质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   现在从 **L** 开始，找出范围内任意两个素数的差，更新到目前为止的最小差。
*   如果范围内的素数为 **< 2** ，则打印 **-1** 。
*   否则打印最小差异。

下面是上述方法的实现:

## C++14

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int sz = 1e5;
bool isPrime[sz + 1];

// Function for Sieve of Eratosthenes
void sieve()
{
    memset(isPrime, true, sizeof(isPrime));

    isPrime[0] = isPrime[1] = false;

    for (int i = 2; i * i <= sz; i++) {
        if (isPrime[i]) {
            for (int j = i * i; j < sz; j += i) {
                isPrime[j] = false;
            }
        }
    }
}

// Function to return the minimum difference
// between any two prime numbers
// from the given range [L, R]
int minDifference(int L, int R)
{

    // Find the first prime from the range
    int fst = 0;
    for (int i = L; i <= R; i++) {

        if (isPrime[i]) {
            fst = i;
            break;
        }
    }

    // Find the second prime from the range
    int snd = 0;
    for (int i = fst + 1; i <= R; i++) {

        if (isPrime[i]) {
            snd = i;
            break;
        }
    }

    // If the number of primes in
    // the given range is < 2
    if (snd == 0)
        return -1;

    // To store the minimum difference between
    // two consecutive primes from the range
    int diff = snd - fst;

    // Range left to check for primes
    int left = snd + 1;
    int right = R;

    // For every integer in the range
    for (int i = left; i <= right; i++) {

        // If the current integer is prime
        if (isPrime[i]) {

            // If the difference between i
            // and snd is minimum so far
            if (i - snd <= diff) {

                fst = snd;
                snd = i;
                diff = snd - fst;
            }
        }
    }

    return diff;
}

// Driver code
int main()
{
    // Generate primes
    sieve();

    int L = 21, R = 50;

    cout << minDifference(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int sz = (int) 1e5;
static boolean []isPrime = new boolean [sz + 1];

// Function for Sieve of Eratosthenes
static void sieve()
{
    Arrays.fill(isPrime, true);

    isPrime[0] = isPrime[1] = false;

    for (int i = 2; i * i <= sz; i++)
    {
        if (isPrime[i])
        {
            for (int j = i * i; j < sz; j += i)
            {
                isPrime[j] = false;
            }
        }
    }
}

// Function to return the minimum difference
// between any two prime numbers
// from the given range [L, R]
static int minDifference(int L, int R)
{

    // Find the first prime from the range
    int fst = 0;
    for (int i = L; i <= R; i++)
    {
        if (isPrime[i])
        {
            fst = i;
            break;
        }
    }

    // Find the second prime from the range
    int snd = 0;
    for (int i = fst + 1; i <= R; i++)
    {
        if (isPrime[i])
        {
            snd = i;
            break;
        }
    }

    // If the number of primes in
    // the given range is < 2
    if (snd == 0)
        return -1;

    // To store the minimum difference between
    // two consecutive primes from the range
    int diff = snd - fst;

    // Range left to check for primes
    int left = snd + 1;
    int right = R;

    // For every integer in the range
    for (int i = left; i <= right; i++)
    {

        // If the current integer is prime
        if (isPrime[i])
        {

            // If the difference between i
            // and snd is minimum so far
            if (i - snd <= diff)
            {
                fst = snd;
                snd = i;
                diff = snd - fst;
            }
        }
    }
    return diff;
}

// Driver code
public static void main(String []args)
{

    // Generate primes
    sieve();

    int L = 21, R = 50;
    System.out.println(minDifference(L, R));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

sz = int(1e5);
isPrime = [True] * (sz + 1);

# Function for Sieve of Eratosthenes
def sieve() :

    isPrime[0] = isPrime[1] = False;

    for i in range(2, int(sqrt(sz)) + 1) :
        if (isPrime[i]) :
            for j in range(i * i, sz, i) :
                isPrime[j] = False;

# Function to return the minimum difference
# between any two prime numbers
# from the given range [L, R]
def minDifference(L, R) :

    # Find the first prime from the range
    fst = 0;
    for i in range(L, R + 1) :

        if (isPrime[i]) :
            fst = i;
            break;

    # Find the second prime from the range
    snd = 0;
    for i in range(fst + 1, R + 1) :

        if (isPrime[i]) :
            snd = i;
            break;

    # If the number of primes in
    # the given range is < 2
    if (snd == 0) :
        return -1;

    # To store the minimum difference between
    # two consecutive primes from the range
    diff = snd - fst;

    # Range left to check for primes
    left = snd + 1;
    right = R;

    # For every integer in the range
    for i in range(left, right + 1) :

        # If the current integer is prime
        if (isPrime[i]) :

            # If the difference between i
            # and snd is minimum so far
            if (i - snd <= diff) :

                fst = snd;
                snd = i;
                diff = snd - fst;

    return diff;

# Driver code
if __name__ == "__main__" :

    # Generate primes
    sieve();

    L = 21; R = 50;

    print(minDifference(L, R));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int sz = (int) 1e5;
static Boolean []isPrime = new Boolean [sz + 1];

// Function for Sieve of Eratosthenes
static void sieve()
{
    for(int i = 2; i< sz + 1; i++)
        isPrime[i] = true;

    for (int i = 2; i * i <= sz; i++)
    {
        if (isPrime[i])
        {
            for (int j = i * i; j < sz; j += i)
            {
                isPrime[j] = false;
            }
        }
    }
}

// Function to return the minimum difference
// between any two prime numbers
// from the given range [L, R]
static int minDifference(int L, int R)
{

    // Find the first prime from the range
    int fst = 0;
    for (int i = L; i <= R; i++)
    {
        if (isPrime[i])
        {
            fst = i;
            break;
        }
    }

    // Find the second prime from the range
    int snd = 0;
    for (int i = fst + 1; i <= R; i++)
    {
        if (isPrime[i])
        {
            snd = i;
            break;
        }
    }

    // If the number of primes in
    // the given range is < 2
    if (snd == 0)
        return -1;

    // To store the minimum difference between
    // two consecutive primes from the range
    int diff = snd - fst;

    // Range left to check for primes
    int left = snd + 1;
    int right = R;

    // For every integer in the range
    for (int i = left; i <= right; i++)
    {

        // If the current integer is prime
        if (isPrime[i])
        {

            // If the difference between i
            // and snd is minimum so far
            if (i - snd <= diff)
            {
                fst = snd;
                snd = i;
                diff = snd - fst;
            }
        }
    }
    return diff;
}

// Driver code
public static void Main(String []args)
{

    // Generate primes
    sieve();

    int L = 21, R = 50;
    Console.WriteLine(minDifference(L, R));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
const sz = 1e5;
let isPrime = new Array(sz + 1);

// Function for Sieve of Eratosthenes
function sieve()
{
    isPrime.fill(true);
    isPrime[0] = isPrime[1] = false;

    for(let i = 2; i * i <= sz; i++)
    {
        if (isPrime[i])
        {
            for(let j = i * i; j < sz; j += i)
            {
                isPrime[j] = false;
            }
        }
    }
}

// Function to return the minimum difference
// between any two prime numbers
// from the given range [L, R]
function minDifference(L, R)
{

    // Find the first prime from the range
    let fst = 0;
    for(let i = L; i <= R; i++)
    {
        if (isPrime[i])
        {
            fst = i;
            break;
        }
    }

    // Find the second prime from the range
    let snd = 0;
    for(let i = fst + 1; i <= R; i++)
    {
        if (isPrime[i])
        {
            snd = i;
            break;
        }
    }

    // If the number of primes in
    // the given range is < 2
    if (snd == 0)
        return -1;

    // To store the minimum difference between
    // two consecutive primes from the range
    let diff = snd - fst;

    // Range left to check for primes
    let left = snd + 1;
    let right = R;

    // For every integer in the range
    for(let i = left; i <= right; i++)
    {

        // If the current integer is prime
        if (isPrime[i])
        {

            // If the difference between i
            // and snd is minimum so far
            if (i - snd <= diff)
            {
                fst = snd;
                snd = i;
                diff = snd - fst;
            }
        }
    }
    return diff;
}

// Driver code

// Generate primes
sieve();

let L = 21, R = 50;

document.write(minDifference(L, R));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
2
```