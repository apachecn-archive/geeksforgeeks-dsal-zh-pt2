# 在正好有 N 个除数的数中可以存在的最大可能素数

> 原文:[https://www . geeksforgeeks . org/最大可能素数除数-在数中可以存在-具有-n 个除数/](https://www.geeksforgeeks.org/maximum-possible-prime-divisors-that-can-exist-in-numbers-having-exactly-n-divisors/)

给定一个整数 **N** ，它表示任意数的除数，任务是找出在有 N 个除数的数中可能的最大质因数。

**示例:**

> **输入:**N = 4
> T3】输出: 2
> 
> **输入:**N = 8
> T3】输出: 3

**方法:**思路是求数 N 的[素因子分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)，那么素因子的幂之和就是一个数与 N 个因子可以有的最大可能的素因子。

**例如:**

```
Let the number of divisors of number be 4,

Then the possible numbers can be 6, 10, 15,...
Divisors of 6 = 1, 2, 3, 6

Total number of prime-divisors = 2 (2, 3)

Prime Factorization of 4 = 22
Sum of powers of prime factors = 2
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum possible prime divisor
// of a number can have N divisors

#include <iostream>

using namespace std;

#define ll long long int

// Function to find the
// maximum possible prime divisors
// of a number can have with N divisors
void findMaxPrimeDivisor(int n){

    int max_possible_prime = 0;

    // Number of time number
    // divided by 2
    while (n % 2 == 0) {
        max_possible_prime++;
        n = n / 2;
    }

    // Divide by other prime numbers
    for (int i = 3; i * i <= n; i = i + 2) {
        while (n % i == 0) {
            max_possible_prime++;
            n = n / i;
        }
    }

    // If the last number of also
    // prime then also include it
    if (n > 2) {
        max_possible_prime++;
    }

    cout << max_possible_prime << "\n";
}

// Driver Code
int main()
{

    int n = 4;

    // Function Call
    findMaxPrimeDivisor(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum possible prime divisor
// of a number can have N divisors
import java.util.*;

class GFG{

// Function to find the
// maximum possible prime divisors
// of a number can have with N divisors
static void findMaxPrimeDivisor(int n)
{
    int max_possible_prime = 0;

    // Number of time number
    // divided by 2
    while (n % 2 == 0)
    {
        max_possible_prime++;
        n = n / 2;
    }

    // Divide by other prime numbers
    for(int i = 3; i * i <= n; i = i + 2)
    {
       while (n % i == 0)
       {
           max_possible_prime++;
           n = n / i;
       }
    }

    // If the last number of also
    // prime then also include it
    if (n > 2)
    {
        max_possible_prime++;
    }
    System.out.print(max_possible_prime + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int n = 4;

    // Function Call
    findMaxPrimeDivisor(n);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum possible prime divisor
# of a number can have N divisors

# Function to find the maximum
# possible prime divisors of a
# number can have with N divisors
def findMaxPrimeDivisor(n):

    max_possible_prime = 0

    # Number of time number
    # divided by 2
    while (n % 2 == 0):
        max_possible_prime += 1
        n = n // 2

    # Divide by other prime numbers
    i = 3
    while(i * i <= n):
        while (n % i == 0):

            max_possible_prime += 1
            n = n // i
        i = i + 2

    # If the last number of also
    # prime then also include it
    if (n > 2):
        max_possible_prime += 1

    print(max_possible_prime)

# Driver Code
n = 4

# Function Call
findMaxPrimeDivisor(n)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation to find the
// maximum possible prime divisor
// of a number can have N divisors
using System;

class GFG{

// Function to find the
// maximum possible prime divisors
// of a number can have with N divisors
static void findMaxPrimeDivisor(int n)
{
    int max_possible_prime = 0;

    // Number of time number
    // divided by 2
    while (n % 2 == 0)
    {
        max_possible_prime++;
        n = n / 2;
    }

    // Divide by other prime numbers
    for(int i = 3; i * i <= n; i = i + 2)
    {
       while (n % i == 0)
       {
           max_possible_prime++;
           n = n / i;
       }
    }

    // If the last number of also
    // prime then also include it
    if (n > 2)
    {
        max_possible_prime++;
    }
    Console.Write(max_possible_prime + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4;

    // Function Call
    findMaxPrimeDivisor(n);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// maximum possible prime divisor
// of a number can have N divisors

// Function to find the maximum
// possible prime divisors of a
// number can have with N divisors
function findMaxPrimeDivisor(n)
{
    let max_possible_prime = 0;

    // Number of time number
    // divided by 2
    while (n % 2 == 0)
    {
        max_possible_prime++;
        n = Math.floor(n / 2);
    }

    // Divide by other prime numbers
    for(let i = 3; i * i <= n; i = i + 2)
    {
        while (n % i == 0)
        {
            max_possible_prime++;
            n = Math.floor(n / i);
        }
    }

    // If the last number of also
    // prime then also include it
    if (n > 2)
    {
        max_possible_prime++;
    }
    document.write(max_possible_prime + "\n");
}

// Driver Code
let n = 4;

// Function Call
findMaxPrimeDivisor(n);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
2
```

时间复杂度:O(sqrt(N) * logN)

辅助空间:0(1)