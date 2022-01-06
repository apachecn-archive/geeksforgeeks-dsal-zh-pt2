# 计算将整数表示为指数的方式

> 原文:[https://www . geeksforgeeks . org/count-way-to-表示整数为指数/](https://www.geeksforgeeks.org/count-ways-to-represent-an-integer-as-an-exponent/)

给定一个整数 **N** ，任务是统计 **N** 可以表示为指数的方式数，即**x<sup>y</sup>T7】，其中 x 和 y 为正整数。**

**示例:**

> **输入:** N = 64
> **输出:** 4
> **说明:** 64 可以表示为 2 <sup>6</sup> ，4 <sup>3</sup> ，8 <sup>2</sup> 和 64 <sup>1</sup>
> 
> **输入:**N = 27
> T3】输出: 2

**方法:**解决给定问题的思路是求数**N**T5 的[素因子分解，然后求给定数 **N**](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/) 素因子的[指数的](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/) [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 素因子的[数。](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate GCD of a
// and b using Euclidean Algorithm
long long int gcd(long long int a,
                  long long int b)
{
    // Iterate until b is non-zero
    while (b > 0) {

        long long int rem = a % b;
        a = b;
        b = rem;
    }

    // Return the GCD
    return a;
}

// Function to count the number of
// ways N can be expressed as x^y
int countNumberOfWays(long long int n)
{
    // Base Case
    if (n == 1)
        return -1;

    // Stores the gcd of powers
    long long int g = 0;

    int power = 0;

    // Calculate the degree of 2 in N
    while (n % 2 == 0) {
        power++;
        n /= 2;
    }

    g = gcd(g, power);

    // Calculate the degree of prime numbers in N
    for (int i = 3; i <= sqrt(n); i += 2) {
        power = 0;

        // Calculate the degree of
        // prime 'i' in N
        while (n % i == 0) {

            power++;
            n /= i;
        }
        g = gcd(g, power);
    }

    // If N is a prime, g becomes 1.
    if (n > 2)
        g = gcd(g, 1);

    // Stores the number of ways
    // to represent N as x^y
    int ways = 1;

    // Find the number of Factors of g
    power = 0;

    while (g % 2 == 0) {
        g /= 2;
        power++;
    }

    // Update the count of ways
    ways *= (power + 1);

    // Iterate to find rest of the prime numbers
    for (int i = 3; i <= sqrt(g); i += 2) {
        power = 0;

        // Find the power of i
        while (g % i == 0) {
            power++;
            g /= i;
        }

        // Update the count of ways
        ways *= (power + 1);
    }

    // If g is prime
    if (g > 2)
        ways *= 2;

    // Return the total number of ways
    return ways;
}

// Driver Code
int main()
{
    int N = 64;
    cout << countNumberOfWays(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to calculate GCD of a
// and b using Euclidean Algorithm
static int gcd(int a,
                  int b)
{
    // Iterate until b is non-zero
    while (b > 0) {

        int rem = a % b;
        a = b;
        b = rem;
    }

    // Return the GCD
    return a;
}

// Function to count the number of
// ways N can be expressed as x^y
static int countNumberOfWays(int n)
{

    // Base Case
    if (n == 1)
        return -1;

    // Stores the gcd of powers
    int g = 0;

    int power = 0;

    // Calculate the degree of 2 in N
    while (n % 2 == 0) {
        power++;
        n /= 2;
    }

    g = gcd(g, power);

    // Calculate the degree of prime numbers in N
    for (int i = 3; i <= (int)Math.sqrt(n); i += 2) {
        power = 0;

        // Calculate the degree of
        // prime 'i' in N
        while (n % i == 0) {

            power++;
            n /= i;
        }
        g = gcd(g, power);
    }

    // If N is a prime, g becomes 1.
    if (n > 2)
        g = gcd(g, 1);

    // Stores the number of ways
    // to represent N as x^y
    int ways = 1;

    // Find the number of Factors of g
    power = 0;

    while (g % 2 == 0) {
        g /= 2;
        power++;
    }

    // Update the count of ways
    ways *= (power + 1);

    // Iterate to find rest of the prime numbers
    for (int i = 3; i <= (int)Math.sqrt(g); i += 2) {
        power = 0;

        // Find the power of i
        while (g % i == 0) {
            power++;
            g /= i;
        }

        // Update the count of ways
        ways *= (power + 1);
    }

    // If g is prime
    if (g > 2)
        ways *= 2;

    // Return the total number of ways
    return ways;
}

// Driver Code
public static void main(String[] args)
{
    int N = 64;
    System.out.print(countNumberOfWays(N));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to calculate GCD of a
# and b using Euclidean Algorithm
def gcd(a, b) :

    # Iterate until b is non-zero
    while (b > 0) :
        rem = a % b
        a = b
        b = rem

    # Return the GCD
    return a

# Function to count the number of
# ways N can be expressed as x^y
def countNumberOfWays(n) :

    # Base Case
    if (n == 1) :
        return -1

    # Stores the gcd of powers
    g = 0
    power = 0

    # Calculate the degree of 2 in N
    while (n % 2 == 0) :
        power += 1
        n //= 2
    g = gcd(g, power)

    # Calculate the degree of prime numbers in N
    for i in range(3, int(math. sqrt(g)) + 1, 2):
        power = 0

        # Calculate the degree of
        # prime 'i' in N
        while (n % i == 0) :
            power += 1
            n //= i      
        g = gcd(g, power)

    # If N is a prime, g becomes 1.
    if (n > 2) :
        g = gcd(g, 1)

    # Stores the number of ways
    # to represent N as x^y
    ways = 1

    # Find the number of Factors of g
    power = 0
    while (g % 2 == 0) :
        g //= 2
        power += 1

    # Update the count of ways
    ways *= (power + 1)

    # Iterate to find rest of the prime numbers
    for i in range(3, int(math. sqrt(g)) + 1, 2):
        power = 0

        # Find the power of i
        while (g % i == 0) :
            power += 1
            g /= i

        # Update the count of ways
        ways *= (power + 1)

    # If g is prime
    if (g > 2) :
        ways *= 2

    # Return the total number of ways
    return ways

# Driver Code
N = 64
print(countNumberOfWays(N))

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to calculate GCD of a
  // and b using Euclidean Algorithm
  static int gcd(int a,
                 int b)
  {

    // Iterate until b is non-zero
    while (b > 0)
    {
      int rem = a % b;
      a = b;
      b = rem;
    }

    // Return the GCD
    return a;
  }

  // Function to count the number of
  // ways N can be expressed as x^y
  static int countNumberOfWays(int n)
  {

    // Base Case
    if (n == 1)
      return -1;

    // Stores the gcd of powers
    int g = 0;
    int power = 0;

    // Calculate the degree of 2 in N
    while (n % 2 == 0)
    {
      power++;
      n /= 2;
    }
    g = gcd(g, power);

    // Calculate the degree of prime numbers in N
    for (int i = 3; i <= (int)Math.Sqrt(n); i += 2)
    {
      power = 0;

      // Calculate the degree of
      // prime 'i' in N
      while (n % i == 0)
      {
        power++;
        n /= i;
      }
      g = gcd(g, power);
    }

    // If N is a prime, g becomes 1.
    if (n > 2)
      g = gcd(g, 1);

    // Stores the number of ways
    // to represent N as x^y
    int ways = 1;

    // Find the number of Factors of g
    power = 0;
    while (g % 2 == 0)
    {
      g /= 2;
      power++;
    }

    // Update the count of ways
    ways *= (power + 1);

    // Iterate to find rest of the prime numbers
    for (int i = 3; i <= (int)Math.Sqrt(g); i += 2)
    {
      power = 0;

      // Find the power of i
      while (g % i == 0)
      {
        power++;
        g /= i;
      }

      // Update the count of ways
      ways *= (power + 1);
    }

    // If g is prime
    if (g > 2)
      ways *= 2;

    // Return the total number of ways
    return ways;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int N = 64;
    Console.Write(countNumberOfWays(N));
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

 // Javascript program for the above approach

// Function to calculate GCD of a
// and b using Euclidean Algorithm
function gcd(a, b)
{
    // Iterate until b is non-zero
    while (b > 0) {

        let rem = a % b;
        a = b;
        b = rem;
    }

    // Return the GCD
    return a;
}

// Function to count the number of
// ways N can be expressed as x^y
function countNumberOfWays(n)
{
    // Base Case
    if (n == 1)
        return -1;

    // Stores the gcd of powers
    let g = 0;

    let power = 0;

    // Calculate the degree of 2 in N
    while (n % 2 == 0) {
        power++;
        n /= 2;
    }

    g = gcd(g, power);

    // Calculate the degree of prime numbers in N
    for (let i = 3; i <= Math.sqrt(n); i += 2) {
        power = 0;

        // Calculate the degree of
        // prime 'i' in N
        while (n % i == 0) {

            power++;
            n /= i;
        }
        g = gcd(g, power);
    }

    // If N is a prime, g becomes 1.
    if (n > 2)
        g = gcd(g, 1);

    // Stores the number of ways
    // to represent N as x^y
    let ways = 1;

    // Find the number of Factors of g
    power = 0;

    while (g % 2 == 0) {
        g /= 2;
        power++;
    }

    // Update the count of ways
    ways *= (power + 1);

    // Iterate to find rest of the prime numbers
    for (let i = 3; i <= Math.sqrt(g); i += 2) {
        power = 0;

        // Find the power of i
        while (g % i == 0) {
            power++;
            g /= i;
        }

        // Update the count of ways
        ways *= (power + 1);
    }

    // If g is prime
    if (g > 2)
        ways *= 2;

    // Return the total number of ways
    return ways;
}

// Driver Code

let N = 64;
document.write(countNumberOfWays(N));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(√N)*
***辅助空间:** O(1)*