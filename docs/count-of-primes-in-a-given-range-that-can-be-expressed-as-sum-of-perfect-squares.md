# 给定范围内的素数计数，可以表示为完美平方之和

> 原文:[https://www . geesforgeks . org/给定范围内可以表示为完美平方和的素数数量/](https://www.geeksforgeeks.org/count-of-primes-in-a-given-range-that-can-be-expressed-as-sum-of-perfect-squares/)

给定两个整数 **L** 和 **R** ，任务是在**【L，R】**范围内找到质数的个数，这个范围可以用两个数的两个平方之和来表示。
**举例:**

> **输入:** L = 1，R = 5
> **输出:** 1
> **说明:**
> 在给定范围内唯一能表示为两个完美平方之和的素数是 5(2<sup>2</sup>+1<sup>2</sup>)
> **输入:** L = 7， R = 42
> **输出:** 5
> **说明:**
> 给定范围内可以表示为两个完美平方之和的素数为:
> 13 = 2<sup>2</sup>+3<sup>2</sup>
> 17 = 1<sup>2</sup>+4<sup>2</sup>T33】29 = 5<sup>2</sup>+2

**方法:**
给定的问题可以用[费马小定理](https://www.geeksforgeeks.org/primality-test-set-2-fermet-method/)来求解，该定理指出如果 **p** 满足以下等式，素数 **p** 可以表示为两个平方之和

> (p–1)% 4 = = 0

按照以下步骤解决问题:

*   遍历**【L，R】**范围。
*   对于每个数字，[检查是否不是](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)的质数。
*   如果发现是这样，检查素数的形式是否为 **4K + 1** 。如果是 sp，增加**计数**。
*   遍历完整范围后，打印**计数**。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a prime number
// satisfies the condition to be
// expressed as sum of two perfect squares
bool sumSquare(int p)
{
    return (p - 1) % 4 == 0;
}

// Function to check if a
// number is prime or not
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to return the count of primes
// in the range which can be expressed as
// the sum of two squares
int countOfPrimes(int L, int R)
{
    int count = 0;
    for (int i = L; i <= R; i++) {

        // If i is a prime
        if (isPrime(i)) {

            // If i can be expressed
            // as the sum of two squares
            if (sumSquare(i))
                count++;
        }
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{
    int L = 5, R = 41;
    cout << countOfPrimes(L, R);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if a prime number
// satisfies the condition to be
// expressed as sum of two perfect
// squares
static boolean sumSquare(int p)
{
    return (p - 1) % 4 == 0;
}

// Function to check if a
// number is prime or not
static boolean isPrime(int n)
{

    // Corner cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to return the count of primes
// in the range which can be expressed as
// the sum of two squares
static int countOfPrimes(int L, int R)
{
    int count = 0;
    for(int i = L; i <= R; i++)
    {

        // If i is a prime
        if (isPrime(i))
        {

            // If i can be expressed
            // as the sum of two squares
            if (sumSquare(i))
                count++;
        }
    }

    // Return the count
    return count;
}

// Driver code
public static void main(String[] args)
{
    int L = 5, R = 41;

    System.out.println(countOfPrimes(L, R));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to check if a prime number
# satisfies the condition to be
# expressed as sum of two perfect
# squares
def sumsquare(p):

  return (p - 1) % 4 == 0

# Function to check if a
# number is prime or not
def isprime(n):

  # Corner cases
  if n <= 1:
    return False
  if n <= 3:
    return True
  if (n % 2 == 0) or (n % 3 == 0):
    return False

  i = 5
  while (i * i <= n):
    if ((n % i == 0) or
        (n % (i + 2) == 0)):
      return False
    i += 6

  return True

# Function to return the count of primes
# in the range which can be expressed as
# the sum of two squares
def countOfPrimes(L, R):

  count = 0
  for i in range(L, R + 1):

    # If i is a prime
    if (isprime(i)):

      # If i can be expressed
      # as the sum of two squares
      if sumsquare(i):
        count += 1

  # Return the count
  return count

# Driver code
if __name__=='__main__':

  L = 5
  R = 41
  print(countOfPrimes(L, R))

# This code is contributed by virusbuddah_
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if a prime number
// satisfies the condition to be
// expressed as sum of two perfect
// squares
static bool sumSquare(int p)
{
    return (p - 1) % 4 == 0;
}

// Function to check if a
// number is prime or not
static bool isPrime(int n)
{

    // Corner cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to return the count of primes
// in the range which can be expressed as
// the sum of two squares
static int countOfPrimes(int L, int R)
{
    int count = 0;
    for(int i = L; i <= R; i++)
    {

        // If i is a prime
        if (isPrime(i))
        {

            // If i can be expressed
            // as the sum of two squares
            if (sumSquare(i))
                count++;
        }
    }

    // Return the count
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int L = 5, R = 41;

    Console.WriteLine(countOfPrimes(L, R));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    // Function to check if a prime number
    // satisfies the condition to be
    // expressed as sum of two perfect
    // squares
    function sumSquare(p) {
        return (p - 1) % 4 == 0;
    }

    // Function to check if a
    // number is prime or not
    function isPrime(n) {

        // Corner cases
        if (n <= 1)
            return false;

        if (n <= 3)
            return true;

        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Function to return the count of primes
    // in the range which can be expressed as
    // the sum of two squares
    function countOfPrimes(L , R) {
        var count = 0;
        for (var i = L; i <= R; i++) {

            // If i is a prime
            if (isPrime(i)) {

                // If i can be expressed
                // as the sum of two squares
                if (sumSquare(i))
                    count++;
            }
        }

        // Return the count
        return count;
    }

    // Driver code
        var L = 5, R = 41;
        document.write(countOfPrimes(L, R));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>3/2</sup>)*
***辅助空间:** O(1)*