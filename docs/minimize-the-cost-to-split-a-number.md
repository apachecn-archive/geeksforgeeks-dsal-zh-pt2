# 最小化拆分一个号码的成本

> 原文:[https://www . geeksforgeeks . org/最小化拆分号码的成本/](https://www.geeksforgeeks.org/minimize-the-cost-to-split-a-number/)

给定一个整数 **N ≥ 2** ，可以将该数拆分为 **k** 个整数之和即 **N = k1 + k2 + … + kn** 其中每个 kth 元素为 **≥ 2** 则拆分成本计算为**maxDiv(k1)+maxDiv(k2)+…+maxDiv(kn)**其中 **maxDiv(x)** 为 **x** 的最大除数
任务是以成本最小化的方式拆分号码，最终打印出最小化的成本。

**示例:**

> **输入:** N = 6
> **输出:** 2
> 6 可以表示为(3 + 3)，成本为 1 + 1 = 2。
> 
> **输入:**N = 5
> T3】输出: 1

**进场:**

*   当 **n 为质数时，**则成本为 **1** ，因为我们不需要拆分 **n** ，小于自身的 **n** 的最大除数为 **1** 。
*   如果 **n 为奇数****n–2 为质数，**则 **n** 可以拆分为 **(2 +质数)**，这将花费 **1 + 1 = 2** 。
*   如果 **n 为偶数，**则代价为 **2** 正如[哥德巴赫猜想](https://www.geeksforgeeks.org/program-for-goldbachs-conjecture-two-primes-with-given-sum/)一样，每一个大于 **2** 的偶数都可以表示为两个素数之和， **4 * 10 <sup>18</sup>** 证明了这一点。
*   如果不满足以上所有条件，那么 **n** 现在一定是奇数，如果从 **n** 中减去 **3** ，那么它将变成偶数，可以表示为 **(3 +偶数)= (3 +质数+质数)**，这将花费 **3** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// check if a number is prime or not
bool isPrime(int x)
{
    // run a loop upto square root of x
    for (int i = 2; i * i <= x; i++) {
        if (x % i == 0)
            return 0;
    }
    return 1;
}

// Function to return the minimized cost
int minimumCost(int n)
{
    // If n is prime
    if (isPrime(n))
        return 1;

    // If n is odd and can be
    // split into (prime + 2)
    // then cost will be 1 + 1 = 2
    if (n % 2 == 1 && isPrime(n - 2))
        return 2;

    // Every non-prime even number
    // can be expressed as the
    // sum of two primes
    if (n % 2 == 0)
        return 2;

    // n is odd so n can be split into (3 + even)
    // further even part can be
    // split into (prime + prime)
    // (3 + prime + prime) will cost 3
    return 3;
}

// Driver code
int main()
{
    int n = 6;
    cout << minimumCost(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// check if a number is prime or not
static boolean isPrime(int x)
{
    // run a loop upto square root of x
    for (int i = 2; i * i <= x; i++)
    {
        if (x % i == 0)
            return false;
    }
    return true;
}

// Function to return the minimized cost
static int minimumCost(int n)
{
    // If n is prime
    if (isPrime(n))
        return 1;

    // If n is odd and can be
    // split into (prime + 2)
    // then cost will be 1 + 1 = 2
    if (n % 2 == 1 && isPrime(n - 2))
        return 2;

    // Every non-prime even number
    // can be expressed as the
    // sum of two primes
    if (n % 2 == 0)
        return 2;

    // n is odd so n can be split into (3 + even)
    // further even part can be
    // split into (prime + prime)
    // (3 + prime + prime) will cost 3
    return 3;
}

// Driver code
public static void main(String args[])
{
    int n = 6;
    System.out.println(minimumCost(n));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# check if a number is prime or not
def isPrime(x) :

    # run a loop upto square root of x
    for i in range(2, int(sqrt(x)) + 1) :
        if (x % i == 0) :
            return 0;

    return 1;

# Function to return the minimized cost
def minimumCost(n) :

    # If n is prime
    if (isPrime(n)) :
        return 1;

    # If n is odd and can be
    # split into (prime + 2)
    # then cost will be 1 + 1 = 2
    if (n % 2 == 1 and isPrime(n - 2)) :
        return 2;

    # Every non-prime even number
    # can be expressed as the
    # sum of two primes
    if (n % 2 == 0) :
        return 2;

    # n is odd so n can be split into
    # (3 + even) further even part can be
    # split into (prime + prime)
    # (3 + prime + prime) will cost 3
    return 3;

# Driver code
if __name__ == "__main__" :

    n = 6;
    print(minimumCost(n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
public class GFG
{

// check if a number is prime or not
static bool isPrime(int x)
{
    // run a loop upto square root of x
    for (int i = 2; i * i <= x; i++)
    {
        if (x % i == 0)
            return false;
    }
    return true;
}

// Function to return the minimized cost
static int minimumCost(int n)
{
    // If n is prime
    if (isPrime(n))
        return 1;

    // If n is odd and can be
    // split into (prime + 2)
    // then cost will be 1 + 1 = 2
    if (n % 2 == 1 && isPrime(n - 2))
        return 2;

    // Every non-prime even number
    // can be expressed as the
    // sum of two primes
    if (n % 2 == 0)
        return 2;

    // n is odd so n can be split into (3 + even)
    // further even part can be
    // split into (prime + prime)
    // (3 + prime + prime) will cost 3
    return 3;
}

// Driver code
public static void Main(String []args)
{
    int n = 6;
    Console.WriteLine(minimumCost(n));
}
}

// This code is contributed by
// Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// check if a number is prime or not
function isPrime($x)
{
    // run a loop upto square root of x
    for ($i = 2; $i * $i <= $x; $i++)
    {
        if ($x % $i == 0)
            return 0;
    }
    return 1;
}

// Function to return the minimized cost
function minimumCost($n)
{
    // If n is prime
    if (isPrime($n))
        return 1;

    // If n is odd and can be
    // split into (prime + 2)
    // then cost will be 1 + 1 = 2
    if ($n % 2 == 1 && isPrime($n - 2))
        return 2;

    // Every non-prime even number
    // can be expressed as the
    // sum of two primes
    if ($n % 2 == 0)
        return 2;

    // n is odd so n can be split into (3 + even)
    // further even part can be
    // split into (prime + prime)
    // (3 + prime + prime) will cost 3
    return 3;
}

// Driver code
$n = 6;
echo(minimumCost($n));

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
// check if a number is prime or not
function isPrime(x)
{
    // run a loop upto square root of x
    for (let i = 2; i * i <= x; i++)
    {
        if (x % i == 0)
            return 0;
    }
    return 1;
}

// Function to return the minimized cost
function minimumCost(n)
{
    // If n is prime
    if (isPrime(n))
        return 1;

    // If n is odd and can be
    // split into (prime + 2)
    // then cost will be 1 + 1 = 2
    if (n % 2 == 1 && isPrime(n - 2))
        return 2;

    // Every non-prime even number
    // can be expressed as the
    // sum of two primes
    if (n % 2 == 0)
        return 2;

    // n is odd so n can be split into (3 + even)
    // further even part can be
    // split into (prime + prime)
    // (3 + prime + prime) will cost 3
    return 3;
}

// Driver code
let n = 6;
document.write(minimumCost(n));

// This code is contributed by _saurabh_jaiswal.

</script>
```

**Output:** 

```
2
```