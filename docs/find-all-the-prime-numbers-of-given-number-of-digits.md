# 求给定位数的所有素数

> 原文:[https://www . geesforgeks . org/find-all-the-prime-numbers-of-给定位数/](https://www.geeksforgeeks.org/find-all-the-prime-numbers-of-given-number-of-digits/)

给定一个整数 **D** ，任务是找出所有有 **D** 数字的素数。

> **示例:**
> **输入:** D = 1
> **输出:** 2 3 5 7
> **输入:** D = 2
> **输出:**11 13 17 19 23 29 31 37 41 43 47 53 61 67 71 73 79 83 89 97

**接近:**带有 **D** 数字的数字位于范围**【10<sup>(D–1)</sup>、10<sup>D</sup>–1】**内。所以，检查这个区间的所有数字，要检查数字是否是素数，使用厄拉多塞[筛](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)生成所有素数。
以下是上述方法的实施:

## C++

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

// Function to print all the prime
// numbers with d digits
void findPrimesD(int d)
{

    // Range to check integers
    int left = pow(10, d - 1);
    int right = pow(10, d) - 1;

    // For every integer in the range
    for (int i = left; i <= right; i++) {

        // If the current integer is prime
        if (isPrime[i]) {
            cout << i << " ";
        }
    }
}

// Driver code
int main()
{

    // Generate primes
    sieve();
    int d = 1;
    findPrimesD(d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int sz = 100000;
static boolean isPrime[] = new boolean[sz + 1];

// Function for Sieve of Eratosthenes
static void sieve()
{
    for(int i = 0; i <= sz; i++)
    isPrime[i] = true;

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

// Function to print all the prime
// numbers with d digits
static void findPrimesD(int d)
{

    // Range to check integers
    int left = (int)Math.pow(10, d - 1);
    int right = (int)Math.pow(10, d) - 1;

    // For every integer in the range
    for (int i = left; i <= right; i++)
    {

        // If the current integer is prime
        if (isPrime[i])
        {
            System.out.print(i + " ");
        }
    }
}

// Driver code
public static void main(String args[])
{

    // Generate primes
    sieve();
    int d = 1;
    findPrimesD(d);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import sqrt, pow
sz = 100005
isPrime = [True for i in range(sz + 1)]

# Function for Sieve of Eratosthenes
def sieve():
    isPrime[0] = isPrime[1] = False

    for i in range(2, int(sqrt(sz)) + 1, 1):
        if (isPrime[i]):
            for j in range(i * i, sz, i):
                isPrime[j] = False

# Function to print all the prime
# numbers with d digits
def findPrimesD(d):

    # Range to check integers
    left = int(pow(10, d - 1))
    right = int(pow(10, d) - 1)

    # For every integer in the range
    for i in range(left, right + 1, 1):

        # If the current integer is prime
        if (isPrime[i]):
            print(i, end = " ")

# Driver code
if __name__ == '__main__':

    # Generate primes
    sieve()
    d = 1
    findPrimesD(d)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int sz = 100000;
static bool []isPrime = new bool[sz + 1];

// Function for Sieve of Eratosthenes
static void sieve()
{
    for(int i = 0; i <= sz; i++)
    isPrime[i] = true;

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

// Function to print all the prime
// numbers with d digits
static void findPrimesD(int d)
{

    // Range to check integers
    int left = (int)Math.Pow(10, d - 1);
    int right = (int)Math.Pow(10, d) - 1;

    // For every integer in the range
    for (int i = left; i <= right; i++)
    {

        // If the current integer is prime
        if (isPrime[i])
        {
            Console.Write(i + " ");
        }
    }
}

// Driver code
static public void Main ()
{

    // Generate primes
    sieve();
    int d = 1;
    findPrimesD(d);

}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let sz = 100000;
    let isPrime = new Array(sz + 1);
    isPrime.fill(false);

    // Function for Sieve of Eratosthenes
    function sieve()
    {
        for(let i = 0; i <= sz; i++)
            isPrime[i] = true;

        isPrime[0] = isPrime[1] = false;

        for (let i = 2; i * i <= sz; i++)
        {
            if (isPrime[i])
            {
                for (let j = i * i; j < sz; j += i)
                {
                    isPrime[j] = false;
                }
            }
        }
    }

    // Function to print all the prime
    // numbers with d digits
    function findPrimesD(d)
    {

        // Range to check integers
        let left = Math.pow(10, d - 1);
        let right = Math.pow(10, d) - 1;

        // For every integer in the range
        for (let i = left; i <= right; i++)
        {

            // If the current integer is prime
            if (isPrime[i])
            {
                document.write(i + " ");
            }
        }
    }

    // Generate primes
    sieve();
    let d = 1;
    findPrimesD(d);

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
2 3 5 7
```