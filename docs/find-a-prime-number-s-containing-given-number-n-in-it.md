# 找出一个含有给定数 N 的素数 S

> 原文:[https://www . geesforgeks . org/find-a-质数-s-含给定数-n-in-it/](https://www.geeksforgeeks.org/find-a-prime-number-s-containing-given-number-n-in-it/)

给定一个整数 **N** ，找到一个质数 **S** ，这样 **N** 的所有数字都以连续的顺序出现。可能有多个答案。打印其中任何一个。

**示例:**

> **输入:** N = 42
> **输出:** 42013
> **解释:** <u>42</u> 013 是一个素数，42 在其中作为一个连续数出现。15 <u>42</u> 7 也是正确答案。
> 
> **输入:** N = 47
> **输出:** 47
> **说明:** 47 本身就是质数

**天真方法:**可以遵循以下步骤:

*   迭代所有从 **N** 开始的数字
*   用[到 _string()](https://www.geeksforgeeks.org/stdto_string-in-cpp/) 函数将每个数字转换成一个字符串
*   使用 [str.find()](https://www.geeksforgeeks.org/string-find-in-cpp/) 函数检查所需的子字符串
*   如果有任何一个数以 **N** 作为子串，并且它是质数，那么返回这个数

**时间复杂度:** O(S)，其中 S 是所需的素数

**有效方法:**可以遵循以下步骤:

*   可以利用的事实是**一个值高达 1e12 的数，在两个连续的素数之间，最多有 464 个非素数。**
*   将当前数字 **N** 乘以 1000。
*   之后，逐一遍历下一个数字，并检查每个数字。
*   如果数字是质数，则打印该数字。
*   很容易看出，第一个条件将始终跟随着数字，除了最后三个将是 n。

下面是上述方法的实现:

## C++

```
// C++ Implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number is prime
bool isPrime(long long N)
{
    if (N == 1)
        return false;
    for (long long i = 2; i <= sqrt(N); i++)

        // If N is divisible then its not a prime
        if (N % i == 0)
            return false;
    return true;
}
// Function to print a prime number
// which has N as a substring
long long prime_substring_Number(long long N)
{
    // Check for the base case
    if (N == 0) {
        return 103;

        // 103 is a prime
    }

    // multiply N by 10^3
    // Check for numbers from
    // N*1000 to N*1000 + 464
    N *= 1000;
    for (long long i = N; i < N + 465; i++) {
        if (isPrime(i)) {
            return i;
        }
    }
    return 0;
}

// Driver Code
int main()
{
    long N = 42;
    cout << prime_substring_Number(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
class GFG {
static boolean isPrime(long N)
{
    if (N == 1)
        return false;
    for (long i = 2; i <= Math.sqrt(N); i++)

        // If N is divisible then its not a prime
        if (N % i == 0)
            return false;
    return true;
}

// Function to print a prime number
// which has N as a substring
static long prime_substring_Number(long N)
{
    // Check for the base case
    if (N == 0) {
        return 103;

        // 103 is a prime
    }

    // multiply N by 10^3
    // Check for numbers from
    // N*1000 to N*1000 + 464
    N *= 1000;
    for (long i = N; i < N + 465; i++) {
        if (isPrime(i)) {
            return i;
        }
    }
    return 0;
}

// Driver Code
    public static void main(String[] args)
    {
        long N = 42;
        System.out.println(prime_substring_Number(N));
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# python Implementation for the above approach
# importing math library
from math import *

# Function to check if a number is prime
def isPrime(N) :
    if N > 1:

      # Iterate from 2 to n / 2
      for i in range(2, int(N/2)+1):

        # If num is divisible by any number between
        # 2 and n / 2, it is not prime
        if (N % i) == 0:
            return False
      else:
        return True 
    else:
        return False

# Function to print a prime number
# which has N as a substring
def prime_substring_Number(N) :

    # Check for the base case
    if (N == 0) :
        return 103

        # 103 is a prime

    # multiply N by 10^3
    # Check for numbers from
    # N*1000 to N*1000 + 464
    N =N * 1000
    for i in range(N,N + 465):
        if (isPrime(i)) :
            return i

    return 0

# Driver Code
N = 42
print(prime_substring_Number(N))

# This code is contributed by anudeep23042002.
```

## C#

```
// C# Implementation for the above approach
using System;
class GFG {

    // Function to check if a number is prime
    static bool isPrime(long N)
    {
        if (N == 1)
            return false;
        for (long i = 2; i <= Math.Sqrt(N); i++)

            // If N is divisible then its not a prime
            if (N % i == 0)
                return false;
        return true;
    }
    // Function to print a prime number
    // which has N as a substring
    static long prime_substring_Number(long N)
    {
        // Check for the base case
        if (N == 0) {
            return 103;

            // 103 is a prime
        }

        // multiply N by 10^3
        // Check for numbers from
        // N*1000 to N*1000 + 464
        N *= 1000;
        for (long i = N; i < N + 465; i++) {
            if (isPrime(i)) {
                return i;
            }
        }
        return 0;
    }

    // Driver Code
    public static void Main()
    {
        long N = 42;
        Console.WriteLine(prime_substring_Number(N));
    }
}

// This code is contributed y ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to check if a number is prime
        function isPrime(N) {
            if (N == 1)
                return false;
            for (let i = 2; i <= Math.sqrt(N); i++)

                // If N is divisible then its not a prime
                if (N % i == 0)
                    return false;
            return true;
        }

        // Function to print a prime number
        // which has N as a substring
        function prime_substring_Number(N)
        {

            // Check for the base case
            if (N == 0) {
                return 103;

                // 103 is a prime
            }

            // multiply N by 10^3
            // Check for numbers from
            // N*1000 to N*1000 + 464
            N *= 1000;
            for (let i = N; i < N + 465; i++) {
                if (isPrime(i)) {
                    return i;
                }
            }
            return 0;
        }

        // Driver Code
        let N = 42;
        document.write(prime_substring_Number(N));

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
42013
```

**时间复杂度:**O(sqrt(N * 1000)* 300)
T3】辅助空间: O(1)