# 经济数字

> 原文:[https://www.geeksforgeeks.org/economical-numbers/](https://www.geeksforgeeks.org/economical-numbers/)

**经济数**是一个数 **N** 如果 **N** 的素数因式分解中的位数(包括幂)小于 **N** 中的位数。
前几个经济数字是:

> 125、128、243、256、343、512、625、729……

### 找出小于 N 的经济数字

给定一个数字 **N** ，任务是打印所有**经济数字**到 **N** 。
**举例:**

> **输入:** N = 200
> **输出:** 125 128
> **输入:** N = 700
> **输出:** 125 128 243 256 343 512 625

**进场:**

1.  用圣代拉姆的筛子数 10^6 之前的所有素数。
2.  查找 n 中的位数
3.  找出 N 的所有质因数，并对每个质因数 p 做以下操作
    *   查找 p 中的位数
    *   计算除以 n 的最高幂
    *   求以上两项之和。
4.  如果质因数中的数字小于原始数字中的数字，则返回 true。否则返回 false。

以下是实施办法:

## C++

```
// C++ implementation to find
// Economical Numbers till n

#include <bits/stdc++.h>
using namespace std;
const int MAX = 10000;

// Array to store all prime less
// than and equal to MAX.
vector<int> primes;

// Utility function for sieve of sundaram
void sieveSundaram()
{
    // In general Sieve of Sundaram,
    // produces primes smaller
    // than (2*x + 2) for a number
    // given number x. Since
    // we want primes smaller than MAX,
    // we reduce MAX to half
    bool marked[MAX / 2 + 1] = { 0 };

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (int i = 1; i <= (sqrt(MAX) - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1;
             j <= MAX / 2; j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push_back(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.push_back(2 * i + 1);
}

// Function to check if a number is
// a Economical number
bool isEconomical(int n)
{
    if (n == 1)
        return false;

    // Count digits in original number
    int original_no = n;
    int sumDigits = 0;
    while (original_no > 0) {
        sumDigits++;
        original_no = original_no / 10;
    }

    // Count all digits in prime factors of n
    // pDigit is going to hold this value.
    int pDigit = 0, count_exp = 0, p;
    for (int i = 0; primes[i] <= n / 2; i++) {
        // Count powers of p in n
        while (n % primes[i] == 0) {
            // If primes[i] is a prime factor,
            p = primes[i];
            n = n / p;

            // Count the power of prime factors
            count_exp++;
        }

        // Add its digits to pDigit.
        while (p > 0) {
            pDigit++;
            p = p / 10;
        }

        // Add digits of power of
        // prime factors to pDigit.
        while (count_exp > 1) {
            pDigit++;
            count_exp = count_exp / 10;
        }
    }

    // If n!=1 then one prime
    // factor still to be
    // summed up;
    if (n != 1) {
        while (n > 0) {
            pDigit++;
            n = n / 10;
        }
    }

    // If digits in prime factors is less than
    // digits in original number  then
    // return true. Else return false.
    return (pDigit < sumDigits);
}

// Driver code
int main()
{
    // Finding all prime numbers
    // before limit. These
    // numbers are used to
    // find prime factors.
    sieveSundaram();

    for (int i = 1; i < 200; i++)
        if (isEconomical(i))
            cout << i << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// Economical Numbers till n
import java.util.*;
class GFG{

static int MAX = 10000;

// Array to store all prime less
// than and equal to MAX.
static Vector<Integer> primes = new Vector<Integer>();

// Utility function for sieve of sundaram
static void sieveSundaram()
{
    // In general Sieve of Sundaram,
    // produces primes smaller
    // than (2*x + 2) for a number
    // given number x. Since
    // we want primes smaller than MAX,
    // we reduce MAX to half
    boolean []marked = new boolean[MAX / 2 + 1];

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (int i = 1; i <= (Math.sqrt(MAX) - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1;
             j <= MAX / 2; j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.add(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.add(2 * i + 1);
}

// Function to check if a number is
// a Economical number
static boolean isEconomical(int n)
{
    if (n == 1)
        return false;

    // Count digits in original number
    int original_no = n;
    int sumDigits = 0;
    while (original_no > 0) {
        sumDigits++;
        original_no = original_no / 10;
    }

    // Count all digits in prime factors of n
    // pDigit is going to hold this value.
    int pDigit = 0, count_exp = 0, p = 0;
    for (int i = 0; primes.get(i) <= n / 2; i++) {
        // Count powers of p in n
        while (n % primes.get(i) == 0)
        {
            // If primes[i] is a prime factor,
            p = primes.get(i);
            n = n / p;

            // Count the power of prime factors
            count_exp++;
        }

        // Add its digits to pDigit.
        while (p > 0)
        {
            pDigit++;
            p = p / 10;
        }

        // Add digits of power of
        // prime factors to pDigit.
        while (count_exp > 1)
        {
            pDigit++;
            count_exp = count_exp / 10;
        }
    }

    // If n!=1 then one prime
    // factor still to be
    // summed up;
    if (n != 1)
    {
        while (n > 0)
        {
            pDigit++;
            n = n / 10;
        }
    }

    // If digits in prime factors is less than
    // digits in original number  then
    // return true. Else return false.
    return (pDigit < sumDigits);
}

// Driver code
public static void main(String[] args)
{
    // Finding all prime numbers
    // before limit. These
    // numbers are used to
    // find prime factors.
    sieveSundaram();

    for (int i = 1; i < 200; i++)
        if (isEconomical(i))
            System.out.print(i + " ");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find
# Economical Numbers till n
import math
MAX = 10000

# Array to store all prime less
# than and equal to MAX.
primes = []

# Utility function for sieve of sundaram
def sieveSundaram():

    # In general Sieve of Sundaram,
    # produces primes smaller
    # than (2*x + 2) for a number
    # given number x. Since
    # we want primes smaller than MAX,
    # we reduce MAX to half
    marked = [0] * (MAX // 2 + 1)

    # Main logic of Sundaram. Mark all numbers which
    # do not generate prime number by doing 2*i+1
    for i in range(1, (int(math.sqrt(MAX)) - 1) // 2 + 1):
        j = (i * (i + 1)) << 1
        while(j <= MAX // 2):
            marked[j] = True
            j = j + 2 * i + 1

    # Since 2 is a prime number
    primes.append(2)

    # Prother primes. Remaining primes are of the
    # form 2*i + 1 such that marked[i] is false.
    for i in range(1, MAX // 2 + 1):
        if (marked[i] == False):
            primes.append(2 * i + 1)

# Function to check if a number is
# a Economical number
def isEconomical(n):

    if (n == 1):
        return False

    # Count digits in original number
    original_no = n
    sumDigits = 0
    while (original_no > 0):
        sumDigits += 1
        original_no = original_no // 10

    # Count all digits in prime factors of n
    # pDigit is going to hold this value.
    pDigit = 0
    count_exp = 0
    i = 0
    p = 0
    while(primes[i] <= n // 2):

        # Count powers of p in n
        while (n % primes[i] == 0):

            # If primes[i] is a prime factor,
            p = primes[i]
            n = n // p

            # Count the power of prime factors
            count_exp += 1
        i += 1

        # Add its digits to pDigit.
        while (p > 0):
            pDigit += 1
            p = p // 10

        # Add digits of power of
        # prime factors to pDigit.
        while (count_exp > 1):
            pDigit += 1
            count_exp = count_exp // 10

    # If n!=1 then one prime
    # factor still to be
    # summed up
    if (n != 1):
        while (n > 0):
            pDigit += 1
            n = n // 10

    # If digits in prime factors is less than
    # digits in original number then
    # return true. Else return false.
    if (pDigit < sumDigits):
        return True
    return False

# Driver code

# Finding all prime numbers
# before limit. These
# numbers are used to
# find prime factors.
sieveSundaram()

for i in range(1, 200):
    if (isEconomical(i)):
        print(i, end = " ")

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to find
// Economical Numbers till n
using System;
using System.Collections.Generic;

class GFG{

static int MAX = 10000;

// Array to store all prime less
// than and equal to MAX.
static List<int> primes = new List<int>();

// Utility function for sieve of sundaram
static void sieveSundaram()
{

    // In general Sieve of Sundaram,
    // produces primes smaller
    // than (2*x + 2) for a number
    // given number x. Since
    // we want primes smaller than MAX,
    // we reduce MAX to half
    bool[] marked = new bool[MAX / 2 + 1];

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for(int i = 1; i <= (Math.Sqrt(MAX) - 1) / 2; i++)
        for(int j = (i * (i + 1)) << 1; j <= MAX / 2;
                j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.Add(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for(int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.Add(2 * i + 1);
}

// Function to check if a number is
// a Economical number
static bool isEconomical(int n)
{
    if (n == 1)
        return false;

    // Count digits in original number
    int original_no = n;
    int sumDigits = 0;

    while (original_no > 0)
    {
        sumDigits++;
        original_no = original_no / 10;
    }

    // Count all digits in prime factors of n
    // pDigit is going to hold this value.
    int pDigit = 0, count_exp = 0, p = 0;
    for(int i = 0; primes[i] <= n / 2; i++)
    {

        // Count powers of p in n
        while (n % primes[i] == 0)
        {

            // If primes[i] is a prime factor,
            p = primes[i];
            n = n / p;

            // Count the power of prime factors
            count_exp++;
        }

        // Add its digits to pDigit.
        while (p > 0)
        {
            pDigit++;
            p = p / 10;
        }

        // Add digits of power of
        // prime factors to pDigit.
        while (count_exp > 1)
        {
            pDigit++;
            count_exp = count_exp / 10;
        }
    }

    // If n!=1 then one prime
    // factor still to be
    // summed up;
    if (n != 1)
    {
        while (n > 0)
        {
            pDigit++;
            n = n / 10;
        }
    }

    // If digits in prime factors is less than
    // digits in original number then
    // return true. Else return false.
    return (pDigit < sumDigits);
}

// Driver code
public static void Main(String[] args)
{

    // Finding all prime numbers
    // before limit. These
    // numbers are used to
    // find prime factors.
    sieveSundaram();

    for(int i = 1; i < 200; i++)
        if (isEconomical(i))
            Console.Write(i + " ");
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
125 128
```

***时间复杂度:** O(n <sup>1/2</sup> )*

***辅助空间:** O(1)*

**参考**:[https://mathworld.wolfram.com/EconomicalNumber.html](https://mathworld.wolfram.com/EconomicalNumber.html)T4】