# 一个数与其最近素数的最小绝对差

> 原文:[https://www . geesforgeks . org/最小绝对差数及其最接近素数/](https://www.geeksforgeeks.org/minimum-absolute-difference-of-a-number-and-its-closest-prime/)

给定一个正整数 **N** ，任务是求 **N** 与最接近 N 的素数**的绝对差。
**注:**最接近 **N** 的素数可以小于、等于或大于 **N** 。
**举例:**** 

> **输入:**N = 25
> T3】输出: 2
> 对于 N = 25
> 最接近的大于 25 的素数为 29。所以差是 4。
> 小于 25 的最近素数为 23。所以差是 2。
> 这两个的最小值是 2。
> **输入:** N = 2
> **输出:** 0
> 由于 2 本身是素数，最接近的素数是 2。所以差是 0。

**进场:**

*   如果 **N** 为**质数**，则打印 **0** 。
*   否则，找到第一个质数 **> N** ，并注意其与 **N** 的区别。
*   然后，找出第一个质数 **< N** ，并注意其与 **N** 的区别。
*   并打印得到的这两个差值的**最小值**。

以下是上述方法的实现:

## C++

```
// C++ program to find the minimum absolute
// difference between a number and its closest prime

#include <bits/stdc++.h>

using namespace std;

    // Function to check if a number is prime or not
    bool isPrime(int N)
    {
        for (int i = 2; i <= sqrt(N); i++) {
            if (N % i == 0)
                return false;
        }
        return true;
    }

    // Function to find the minimum absolute difference
    // between a number and its closest prime
    int getDifference(int N)
    {
        if (N == 0)
            return 2;
        else if (N == 1)
            return 1;
        else if (isPrime(N))
            return 0;

        // Variables to store first prime
        // above and below N
        int aboveN = -1, belowN = -1;
        int n1;

        // Finding first prime number greater than N
        n1 = N + 1;
        while (true) {
            if (isPrime(n1)) {
                aboveN = n1;
                break;
            }
            else
                n1++;
        }

        // Finding first prime number less than N
        n1 = N - 1;
        while (true) {
            if (isPrime(n1)) {
                belowN = n1;
                break;
            }
            else
                n1--;
        }

        // Variables to store the differences
        int diff1 = aboveN - N;
        int diff2 = N - belowN;

        return min(diff1, diff2);
    }

// Driver code
int main()
{
    int N = 25;
   cout << getDifference(N) << endl;
   return 0;
  // This code is contributed by Ryuga
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum absolute
// difference between a number and its closest prime
class GFG {

    // Function to check if a number is prime or not
    static boolean isPrime(int N)
    {
        for (int i = 2; i <= Math.sqrt(N); i++) {
            if (N % i == 0)
                return false;
        }
        return true;
    }

    // Function to find the minimum absolute difference
    // between a number and its closest prime
    static int getDifference(int N)
    {
        if (N == 0)
            return 2;
        else if (N == 1)
            return 1;
        else if (isPrime(N))
            return 0;

        // Variables to store first prime
        // above and below N
        int aboveN = -1, belowN = -1;
        int n1;

        // Finding first prime number greater than N
        n1 = N + 1;
        while (true) {
            if (isPrime(n1)) {
                aboveN = n1;
                break;
            }
            else
                n1++;
        }

        // Finding first prime number less than N
        n1 = N - 1;
        while (true) {
            if (isPrime(n1)) {
                belowN = n1;
                break;
            }
            else
                n1--;
        }

        // Variables to store the differences
        int diff1 = aboveN - N;
        int diff2 = N - belowN;

        return Math.min(diff1, diff2);
    }

    // Driver code
    public static void main(String args[])
    {
        int N = 25;
        System.out.println(getDifference(N));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find the minimum
# absolute difference between a number
# and its closest prime
from math import sqrt

# Function to check if a number is
# prime or not
def isPrime(N):
    k = int(sqrt(N)) + 1
    for i in range(2, k, 1):
        if (N % i == 0):
            return False

    return True

# Function to find the minimum absolute
# difference between a number and its
# closest prime
def getDifference(N):
    if (N == 0):
        return 2
    elif (N == 1):
        return 1
    elif (isPrime(N)):
        return 0

    # Variables to store first prime
    # above and below N
    aboveN = -1
    belowN = -1

    # Finding first prime number
    # greater than N
    n1 = N + 1
    while (True):
        if (isPrime(n1)):
            aboveN = n1
            break

        else:
            n1 += 1

    # Finding first prime number
    # less than N
    n1 = N - 1
    while (True):
        if (isPrime(n1)):
            belowN = n1
            break

        else:
            n1 -= 1

    # Variables to store the differences
    diff1 = aboveN - N
    diff2 = N - belowN

    return min(diff1, diff2)

# Driver code
if __name__ == '__main__':
    N = 25
    print(getDifference(N))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the minimum absolute
// difference between a number and its closest prime
using System;
class GFG {

    // Function to check if a number is prime or not
    static bool isPrime(int N)
    {
        for (int i = 2; i <= Math.Sqrt(N); i++) {
            if (N % i == 0)
                return false;
        }
        return true;
    }

    // Function to find the minimum absolute difference
    // between a number and its closest prime
    static int getDifference(int N)
    {
        if (N == 0)
            return 2;
        else if (N == 1)
            return 1;
        else if (isPrime(N))
            return 0;

        // Variables to store first prime
        // above and below N
        int aboveN = -1, belowN = -1;
        int n1;

        // Finding first prime number greater than N
        n1 = N + 1;
        while (true) {
            if (isPrime(n1)) {
                aboveN = n1;
                break;
            }
            else
                n1++;
        }

        // Finding first prime number less than N
        n1 = N - 1;
        while (true) {
            if (isPrime(n1)) {
                belowN = n1;
                break;
            }
            else
                n1--;
        }

        // Variables to store the differences
        int diff1 = aboveN - N;
        int diff2 = N - belowN;

        return Math.Min(diff1, diff2);
    }

    // Driver code
    public static void Main()
    {
        int N = 25;
        Console.WriteLine(getDifference(N));
    }
}
// This code is contributed by  anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum absolute
// difference between a number and its
// closest prime

// Function to check if a number
// is prime or not
function isPrime($N)
{
    for ($i = 2; $i <= sqrt($N); $i++)
    {
        if ($N % $i == 0)
            return false;
    }
    return true;
}

// Function to find the minimum absolute difference
// between a number and its closest prime
function getDifference($N)
{
    if ($N == 0)
        return 2;
    else if ($N == 1)
        return 1;
    else if (isPrime($N))
        return 0;

    // Variables to store first prime
    // above and below N
    $aboveN = -1; $belowN = -1;

    // Finding first prime number greater than N
    $n1 = $N + 1;
    while (true)
    {
        if (isPrime($n1))
        {
            $aboveN = $n1;
            break;
        }
        else
            $n1++;
    }

    // Finding first prime number less than N
    $n1 = $N - 1;
    while (true)
    {
        if (isPrime($n1))
        {
            $belowN = $n1;
            break;
        }
        else
            $n1--;
    }

    // Variables to store the differences
    $diff1 = $aboveN - $N;
    $diff2 = $N - $belowN;

    return min($diff1, $diff2);
}

// Driver code
$N = 25;
echo getDifference($N) . "\n";

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
// Javascript program to find the minimum absolute
// difference between a number and its
// closest prime

// Function to check if a number
// is prime or not
function isPrime(N)
{
    for (let i = 2; i <= Math.sqrt(N); i++)
    {
        if (N % i == 0)
            return false;
    }
    return true;
}

// Function to find the minimum absolute difference
// between a number and its closest prime
function getDifference(N)
{
    if (N == 0)
        return 2;
    else if (N == 1)
        return 1;
    else if (isPrime(N))
        return 0;

    // Variables to store first prime
    // above and below N
    let aboveN = -1;
    let belowN = -1;

    // Finding first prime number greater than N
    let n1 = N + 1;
    while (true)
    {
        if (isPrime(n1))
        {
            aboveN = n1;
            break;
        }
        else
            n1++;
    }

    // Finding first prime number less than N
    n1 = N - 1;
    while (true)
    {
        if (isPrime(n1))
        {
            belowN = n1;
            break;
        }
        else
            n1--;
    }

    // Variables to store the differences
    let diff1 = aboveN - N;
    let diff2 = N - belowN;

    return Math.min(diff1, diff2);
}

// Driver code
let N = 25;
document.write(getDifference(N) + "<br>");

// This code is contributed
// by gfgking
```

**Output:** 

```
2
```