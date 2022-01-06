# 数 N 的质因数！

> 原文:[https://www.geeksforgeeks.org/count-prime-factors-of-n/](https://www.geeksforgeeks.org/count-prime-factors-of-n/)

给定一个整数 **N** ，任务是统计 **N 的[质因数](https://www.geeksforgeeks.org/prime-factor/)的个数！**。

**示例:**

> **输入:** N = 5
> **输出:** 3
> **说明:**5 的阶乘= 120。120 的质因数是{2，3，5}。因此，计数为 3。
> 
> **输入:**N = 1
> T3】输出: 0

**天真方法:**按照步骤解决问题:

1.  初始化一个变量，比如说 **fac** ，来存储一个数的[阶乘。](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)
2.  初始化一个变量，说**计数**，到[计数 **N 的质因数**](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)！。
3.  迭代范围**【2，fac】**，如果数字不是素数，递增**计数**。
4.  打印**数**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// factorial of a number
int factorial(int f)
{
    // Base Case
    if (f == 0 || f == 1) {
        return 1;
    }
    else {

        // Recursive call
        return (f * factorial(f - 1));
    }
}

// Function to check if a
// number is prime or not
bool isPrime(int element)
{
    for (int i = 2;
         i <= sqrt(element); i++) {
        if (element % i == 0) {

            // Not prime
            return false;
        }
    }

    // Is prime
    return true;
}

// Function to count the number
// of prime factors of N!
int countPrimeFactors(int N)
{
    // Stores factorial of N
    int fac = factorial(N);

    // Stores the count of
    // prime factors
    int count = 0;

    // Iterate over the rage [2, fac]
    for (int i = 2; i <= fac; i++) {

        // If not prime
        if (fac % i == 0 && isPrime(i)) {

            // Increment count
            count++;
        }
    }

    // Print the count
    cout << count;
}

// Driver Code
int main()
{
    // Given value of N
    int N = 5;

    // Function call to count the
    // number of prime factors of N
    countPrimeFactors(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

  // Function to calculate
  // factorial of a number
  static int factorial(int f)
  {
    // Base Case
    if (f == 0 || f == 1) {
      return 1;
    }
    else {

      // Recursive call
      return (f * factorial(f - 1));
    }
  }

  // Function to check if a
  // number is prime or not
  static boolean isPrime(int element)
  {
    for (int i = 2;
         i <= (int)Math.sqrt(element); i++) {
      if (element % i == 0) {

        // Not prime
        return false;
      }
    }

    // Is prime
    return true;
  }

  // Function to count the number
  // of prime factors of N!
  static void countPrimeFactors(int N)
  {
    // Stores factorial of N
    int fac = factorial(N);

    // Stores the count of
    // prime factors
    int count = 0;

    // Iterate over the rage [2, fac]
    for (int i = 2; i <= fac; i++) {

      // If not prime
      if ((fac % i == 0 && isPrime(i))) {

        // Increment count
        count++;
      }
    }

    // Print the count
    System.out.println(count);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given value of N
    int N = 5;

    // Function call to count the
    // number of prime factors of N
    countPrimeFactors(N);
  }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach
from math import sqrt

# Function to calculate
# factorial of a number
def factorial(f):

    # Base Case
    if (f == 0 or f == 1):
        return 1
    else:

        # Recursive call
        return (f * factorial(f - 1))

# Function to check if a
# number is prime or not
def isPrime(element):

    for i in range(2,int(sqrt(element))+1):
        if (element % i == 0):

            # Not prime
            return False

    # Is prime
    return True

# Function to count the number
# of prime factors of N!
def countPrimeFactors(N):

    # Stores factorial of N
    fac = factorial(N)

    # Stores the count of
    # prime factors
    count = 0

    # Iterate over the rage [2, fac]
    for i in range(2, fac + 1):

        # If not prime
        if (fac % i == 0 and isPrime(i)):

            # Increment count
            count += 1

    # Print the count
    print(count)

# Driver Code
# Given value of N
N = 5

# Function call to count the
# number of prime factors of N
countPrimeFactors(N)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

  // Function to calculate
  // factorial of a number
  static int factorial(int f)
  {

    // Base Case
    if (f == 0 || f == 1) {
      return 1;
    }
    else {

      // Recursive call
      return (f * factorial(f - 1));
    }
  }

  // Function to check if a
  // number is prime or not
  static bool isPrime(int element)
  {
    for (int i = 2;
         i <= (int)Math.Sqrt(element); i++) {
      if (element % i == 0) {

        // Not prime
        return false;
      }
    }

    // Is prime
    return true;
  }

  // Function to count the number
  // of prime factors of N!
  static void countPrimeFactors(int N)
  {

    // Stores factorial of N
    int fac = factorial(N);

    // Stores the count of
    // prime factors
    int count = 0;

    // Iterate over the range [2, fac]
    for (int i = 2; i <= fac; i++) {

      // If not prime
      if ((fac % i == 0 && isPrime(i))) {

        // Increment count
        count++;
      }
    }

    // Print the count
    Console.Write(count);
  }

// Driver Code
public static void Main()
{

    // Given value of N
    int N = 5;

    // Function call to count the
    // number of prime factors of N
    countPrimeFactors(N);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to calculate
// factorial of a number
function factorial(f){

    // Base Case
    if (f == 0 || f == 1){
        return 1
    }
    else{
         // Recursive call
         return (f * factorial(f - 1))
        }
    }

// Function to check if a
// number is prime or not
function isPrime(element){

    for (let i = 2;  i < Math.floor(Math.sqrt(element)+1); i++){
        if (element % i == 0){
            // Not prime
            return false
        }
    }
    // Is prime
    return true
}

// Function to count the number
// of prime factors of N!
function countPrimeFactors(N){

    // Stores factorial of N
    let fac = factorial(N)

    // Stores the count of
    // prime factors
    let count = 0

    // Iterate over the range [2, fac]
    for(let i = 2;  i < fac + 1; i++){

        // If not prime
        if (fac % i == 0 && isPrime(i)){   
            // Increment count
            count += 1
        }
    }

    // Print the count
    document.write(count)
}

// Driver Code
// Given value of N
let N = 5

// Function call to count the
// number of prime factors of N
countPrimeFactors(N)
// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N！* sqrt(N))*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。按照以下步骤解决问题:

1.  初始化一个变量，说**计数**，存储 **N 的质因数的[计数！](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)**。
2.  初始化一个布尔数组，说**质数[]** 到[检查一个数是否是质数。](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)
3.  如果发现质数，则在每次迭代中执行厄拉多塞的[筛选并填充**计数**。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
4.  打印**的值，计**为答案。

下面是上述方法的实现:

## C++

```
// C++ approach for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the
// prime factors of N!
int countPrimeFactors(int N)
{
    // Stores the count of
    // prime factors
    int count = 0;

    // Stores whether a number
    // is prime or not
    bool prime[N + 1];

    // Mark all as true initially
    memset(prime, true, sizeof(prime));

    // Sieve of Eratosthenes
    for (int p = 2; p * p <= N; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all subsequent multiples
            for (int i = p * p; i <= N; i += p)
                prime[i] = false;
        }
    }

    // Traverse in the range [2, N]
    for (int p = 2; p <= N; p++) {

        // If prime
        if (prime[p]) {

            // Increment the count
            count++;
        }
    }

    // Print the count
    cout << count;
}

// Driver Code
int main()
{
    // Given  value of N
    int N = 5;

    // Function call to count
    // the prime factors of N!
    countPrimeFactors(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to count the
  // prime factors of N!
  static void countPrimeFactors(int N)
  {

    // Stores the count of
    // prime factors
    int count = 0;

    // Stores whether a number
    // is prime or not
    boolean[] prime = new boolean[N + 1];

    // Mark all as true initially
    Arrays.fill(prime, true);

    // Sieve of Eratosthenes
    for (int p = 2; p * p <= N; p++) {

      // If prime[p] is not changed,
      // then it is a prime
      if (prime[p] == true) {

        // Update all subsequent multiples
        for (int i = p * p; i <= N; i += p)
          prime[i] = false;
      }
    }

    // Traverse in the range [2, N]
    for (int p = 2; p <= N; p++) {

      // If prime
      if (prime[p] != false) {

        // Increment the count
        count++;
      }
    }

    // Print the count
    System.out.print(count);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given  value of N
    int N = 5;

    // Function call to count
    // the prime factors of N!
    countPrimeFactors(N);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python3 approach for the above approach

# Function to count the
# prime factors of N!
def countPrimeFactors(N):

    # Stores the count of
    # prime factors
    count = 0

    # Stores whether a number
    # is prime or not
    prime = [1] * (N + 1)

    # Sieve of Eratosthenes
    for p in range(2, N + 1):
        if p * p > N:
            break

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all subsequent multiples
            for i in range(p * p, N + 1, p):
                prime[i] = 0

    # Traverse in the range [2, N]
    for p in range(2, N + 1):

        # If prime
        if (prime[p]):

            # Increment the count
            count += 1

    # Print the count
    print (count)

# Driver Code
if __name__ == '__main__':

    # Given  value of N
    N = 5

    # Function call to count
    # the prime factors of N!
    countPrimeFactors(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to count the
  // prime factors of N!
  static void countPrimeFactors(int N)
  {

    // Stores the count of
    // prime factors
    int count = 0;

    // Stores whether a number
    // is prime or not
    bool[] prime = new bool[N + 1];

    // Mark all as true initially
    for (int i = 0; i < prime.Length; i++)
        prime[i] = true;

    // Sieve of Eratosthenes
    for (int p = 2; p * p <= N; p++) {

      // If prime[p] is not changed,
      // then it is a prime
      if (prime[p] == true) {

        // Update all subsequent multiples
        for (int i = p * p; i <= N; i += p)
          prime[i] = false;
      }
    }

    // Traverse in the range [2, N]
    for (int p = 2; p <= N; p++) {

      // If prime
      if (prime[p] != false) {

        // Increment the count
        count++;
      }
    }

    // Print the count
    Console.Write(count);
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given  value of N
    int N = 5;

    // Function call to count
    // the prime factors of N!
    countPrimeFactors(N);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

     // Function to count the
    // prime factors of N!
    function countPrimeFactors( N) {

        // Stores the count of
        // prime factors
        var count = 0;

        // Stores whether a number
        // is prime or not
        var prime = Array(N + 1).fill(true);

        // Sieve of Eratosthenes
        for (var p = 2; p * p <= N; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all subsequent multiples
                for (var i = p * p; i <= N; i += p)
                    prime[i] = false;
            }
        }

        // Traverse in the range [2, N]
        for (var p = 2; p <= N; p++) {

            // If prime
            if (prime[p] != false) {

                // Increment the count
                count++;
            }
        }

        // Print the count
        document.write(count);
    }

    // Driver Code

        // Given value of N
        var N = 5;

        // Function call to count
        // the prime factors of N!
        countPrimeFactors(N);

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N * log(logN))*
***辅助空间:** O(N)*