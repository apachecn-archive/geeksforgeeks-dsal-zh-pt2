# 找到一个正数 m，使得 gcd(N^M，N & M)最大

> 原文:[https://www . geesforgeks . org/find-a-正数-m-so-gcdnm-nm-is-maximum/](https://www.geeksforgeeks.org/find-a-positive-number-m-such-that-gcdnm-nm-is-maximum/)

给定一个数字 **N** ，任务是找到一个正数 m，使得 gcd(N^M，N & M)是最大可能值，M < N。任务是打印由此获得的最大 gcd。
**例:**

```
Input: N = 5 
Output: 7 
gcd(2^5, 2&5) = 7 

Input: N = 15 
Output: 5 
```

**方法:**有两种情况需要解决，以获得最大可能的 gcd。

*   如果数字中没有设置最小一位，那么 M 将是一个数字，它的位在 n 的每个位置翻转，然后得到最大 gcd。
*   如果所有的位都被置位，那么答案将是该数的最大因子，除了该数本身。

以下是上述方法的实现:

## C++

```
// C++ program to implement above approach

#include <bits/stdc++.h>
using namespace std;

// Recursive function to count
// the number of unset bits
int countBits(int n)
{
    // Base case
    if (n == 0)
        return 0;

    // unset bit count
    else
        return !(n & 1) + countBits(n >> 1);
}

// Function to return the max gcd
int maxGcd(int n)
{

    // If no unset bits
    if (countBits(n) == 0) {
        // Find the maximum factor
        for (int i = 2; i * i <= n; i++) {
            // Highest factor
            if (n % i == 0) {
                return n / i;
            }
        }
    }
    else {

        int val = 0;
        int power = 1;
        int dupn = n;

        // Find the flipped bit number
        while (n) {
            // If bit is not set
            if (!(n & 1)) {
                val += power;
            }

            // Next power of 2
            power = power * 2;

            // Right shift the number
            n = n >> 1;
        }

        // Return the answer
        return __gcd(val ^ dupn, val & dupn);
    }

    // If a prime number
    return 1;
}

// Driver Code
int main()
{
    // First example
    int n = 5;
    cout << maxGcd(n) << endl;

    // Second example
    n = 15;
    cout << maxGcd(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement above approach

class GFG
{

static int __gcd(int a,int b)
{
    if(b == 0)
    return a;
    return __gcd(b, a % b);
}

// Recursive function to count
// the number of unset bits
static int countBits(int n)
{
    // Base case
    if (n == 0)
        return 0;

    // unset bit count
    else
        return ((n & 1) == 0 ? 1 : 0) + countBits(n >> 1);
}

// Function to return the max gcd
static int maxGcd(int n)
{

    // If no unset bits
    if (countBits(n) == 0)
    {
        // Find the maximum factor
        for (int i = 2; i * i <= n; i++)
        {
            // Highest factor
            if (n % i == 0)
            {
                return n / i;
            }
        }
    }
    else
    {

        int val = 0;
        int power = 1;
        int dupn = n;

        // Find the flipped bit number
        while (n > 0)
        {
            // If bit is not set
            if ((n & 1) == 0)
            {
                val += power;
            }

            // Next power of 2
            power = power * 2;

            // Right shift the number
            n = n >> 1;
        }

        // Return the answer
        return __gcd(val ^ dupn, val & dupn);
    }

    // If a prime number
    return 1;
}

// Driver Code
public static void main(String[] args)
{
    // First example
    int n = 5;
    System.out.println(maxGcd(n));

    // Second example
    n = 15;
    System.out.println(maxGcd(n));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to implement
# above approach
from math import gcd, sqrt

# Recursive function to count
# the number of unset bits
def countBits(n):

    # Base case
    if (n == 0):
        return 0

    # unset bit count
    else:
        return (((n & 1) == 0) +
                  countBits(n >> 1))

# Function to return the max gcd
def maxGcd(n):

    # If no unset bits
    if (countBits(n) == 0):

        # Find the maximum factor
        for i in range(2, int(sqrt(n)) + 1):

            # Highest factor
            if (n % i == 0):
                return int(n / i)

    else:
        val = 0
        power = 1
        dupn = n

        # Find the flipped bit number
        while (n):

            # If bit is not set
            if ((n & 1) == 0):
                val += power

            # Next power of 2
            power = power * 2

            # Right shift the number
            n = n >> 1

        # Return the answer
        return gcd(val ^ dupn, val & dupn)

    # If a prime number
    return 1

# Driver Code
if __name__ == '__main__':

    # First example
    n = 5
    print(maxGcd(n))

    # Second example
    n = 15
    print(maxGcd(n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to implement above approach
using System;
class GFG
{

static int __gcd(int a,int b)
{
    if(b == 0)
    return a;
    return __gcd(b, a % b);
}
// Recursive function to count
// the number of unset bits
static int countBits(int n)
{
    // Base case
    if (n == 0)
        return 0;

    // unset bit count
    else
        return ((n & 1) == 0 ? 1 : 0) + countBits(n >> 1);
}

// Function to return the max gcd
static int maxGcd(int n)
{

    // If no unset bits
    if (countBits(n) == 0)
    {
        // Find the maximum factor
        for (int i = 2; i * i <= n; i++)
        {
            // Highest factor
            if (n % i == 0)
            {
                return n / i;
            }
        }
    }
    else
    {

        int val = 0;
        int power = 1;
        int dupn = n;

        // Find the flipped bit number
        while (n > 0)
        {
            // If bit is not set
            if ((n & 1) == 0)
            {
                val += power;
            }

            // Next power of 2
            power = power * 2;

            // Right shift the number
            n = n >> 1;
        }

        // Return the answer
        return __gcd(val ^ dupn, val & dupn);
    }

    // If a prime number
    return 1;
}

// Driver Code
static void Main()
{
    // First example
    int n = 5;
    Console.WriteLine(maxGcd(n));

    // Second example
    n = 15;
    Console.WriteLine(maxGcd(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement above approach

// Recursive function to count
// the number of unset bits
function countBits($n)
{
    // Base case
    if ($n == 0)
        return 0;

    // unset bit count
    else
        return !($n & 1) +
                 countBits($n >> 1);
}

// Recursive function to return
// gcd of a and b
function gcd($a, $b)
{

    // Everything divides 0
    if ($a == 0)
        return $b;
    if ($b == 0)
        return $a;

    // base case
    if($a == $b)
        return $a ;

    // a is greater
    if($a > $b)
        return gcd($a - $b , $b );

    return gcd($a , $b - $a );
}

// Function to return the max gcd
function maxGcd($n)
{

    // If no unset bits
    if (countBits($n) == 0)
    {

        // Find the maximum factor
        for ($i = 2; $i * $i <= $n; $i++)
        {

            // Highest factor
            if ($n % $i == 0)
            {
                return floor($n / $i);
            }
        }
    }
    else
    {
        $val = 0;
        $power = 1;
        $dupn = $n;

        // Find the flipped bit number
        while ($n)
        {

            // If bit is not set
            if (!($n & 1))
            {
                $val += $power;
            }

            // Next power of 2
            $power = $power * 2;

            // Right shift the number
            $n = $n >> 1;
        }

        // Return the answer
        return gcd($val ^ $dupn, $val & $dupn);
    }

    // If a prime number
    return 1;
}

// Driver Code

// First example
$n = 5;
echo maxGcd($n), "\n";

// Second example
$n = 15;
echo maxGcd($n), "\n";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// javascript program to implement above approach
    function __gcd(a , b) {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Recursive function to count
    // the number of unset bits
    function countBits(n) {
        // Base case
        if (n == 0)
            return 0;

        // unset bit count
        else
            return ((n & 1) == 0 ? 1 : 0) + countBits(n >> 1);
    }

    // Function to return the max gcd
    function maxGcd(n) {

        // If no unset bits
        if (countBits(n) == 0) {
            // Find the maximum factor
            for (i = 2; i * i <= n; i++) {
                // Highest factor
                if (n % i == 0) {
                    return n / i;
                }
            }
        } else {

            var val = 0;
            var power = 1;
            var dupn = n;

            // Find the flipped bit number
            while (n > 0) {
                // If bit is not set
                if ((n & 1) == 0) {
                    val += power;
                }

                // Next power of 2
                power = power * 2;

                // Right shift the number
                n = n >> 1;
            }

            // Return the answer
            return __gcd(val ^ dupn, val & dupn);
        }

        // If a prime number
        return 1;
    }

    // Driver Code

        // First example
        var n = 5;
        document.write(maxGcd(n)+"<br/>");

        // Second example
        n = 15;
        document.write(maxGcd(n));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
7
5
```