# 找到 gcd(a^n，c ),其中 a、n 和 c 可以从 1 到 10^9 变化

> 原文:[https://www . geesforgeks . org/find-gcdan-c-where-a-n-and-c-can-variable-from-1-109/](https://www.geeksforgeeks.org/find-gcdan-c-where-a-n-and-c-can-vary-from-1-to-109/)

问题指出，找到两个数字中的 gcd()，其中一个数字可以与(10^9)^(10^9)一样大，而后者不能存储在数据类型中，如 C++中的 long long int
**示例:**

```
Input : 1 1 1
Output : 1

Input : 10248585 1000000 12564
Output : 9
```

我们从[欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)知道，gcd(a，b) = gcd(a % b，b)。现在问题仍然是找到 a^n 模 c。这可以通过使用 O(logn)复杂度的[模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)来完成。

## C++

```
// CPP program to find GCD of a^n and b.
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

/* Iterative Function to calculate (x^y)%p in O(log y) */
ll modPower(ll x, ll y, ll p)
{
    ll res = 1;      // Initialize result

    x = x % p;  // Update x if it is more than or
                // equal to p

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res*x) % p;

        // y must be even now
        y = y>>1; // y = y/2
        x = (x*x) % p; 
    }
    return res;
}

// Finds GCD of a and b
ll gcd(ll a, ll b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Finds GCD of a^n and c
ll gcdPow(ll a, ll n, ll c)
{
    // check if c is a divisor of a
    if (a % c == 0)
        return c;

    // First compute (a^n) % c
    ll modexpo = modPower(a, n, c);

    // Now simply return GCD of modulo
    // power and c.
    return gcd(modexpo, c);
}

// Driver code
int main()
{
    ll a = 10248585, n = 1000000, c = 12564;
    cout << gcdPow(a, n, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// GCD of a^n and b.
class GFG
{
/* Iterative Function to calculate
(x^y)%p in O(log y) */
static long modPower(long x, long y,
                             long p)
{
    long res = 1; // Initialize result

    x = x % p; // Update x if it is more
               // than or equal to p

    while (y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ((y & 1) > 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Finds GCD of a and b
static long gcd(long a, long b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Finds GCD of a^n and c
static long gcdPow(long a,
                   long n, long c)
{
    // check if c is a divisor of a
    if (a % c == 0)
        return c;

    // First compute (a^n) % c
    long modexpo = modPower(a, n, c);

    // Now simply return GCD
    // of modulo power and c.
    return gcd(modexpo, c);
}

// Driver code
public static void main(String[] args)
{
    long a = 10248585,
         n = 1000000, c = 12564;
    System.out.println(gcdPow(a, n, c));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find
# GCD of a^n and b.

# Iterative Function to
# calculate (x^y)%p in O(log y)
def modPower(x, y, p):

    res = 1 # Initialize result

    x = x % p # Update x if it is more
              # than or equal to p

    while (y > 0):

        # If y is odd, multiply
        # x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# Finds GCD of a and b
def gcd(a, b):

    if (b == 0):
        return a
    return gcd(b, a % b)

# Finds GCD of a^n and c
def gcdPow(a, n, c):

    # check if c is a divisor of a
    if (a % c == 0):
        return c

    # First compute (a^n) % c
    modexpo = modPower(a, n, c)

    # Now simply return GCD of
    # modulo power and c.
    return gcd(modexpo, c)

# Driver code
if __name__ == "__main__":
    a = 10248585
    n = 1000000
    c = 12564
    print(gcdPow(a, n, c))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find
// GCD of a^n and b.
using System;

class GFG
{
/* Iterative Function to calculate
(x^y)%p in O(log y) */
static long modPower(long x, long y,
                             long p)
{
    long res = 1; // Initialize result

    x = x % p; // Update x if it is more
               // than or equal to p

    while (y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ((y & 1) > 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Finds GCD of a and b
static long gcd(long a, long b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Finds GCD of a^n and c
static long gcdPow(long a,
                   long n, long c)
{
    // check if c is a divisor of a
    if (a % c == 0)
        return c;

    // First compute (a^n) % c
    long modexpo = modPower(a, n, c);

    // Now simply return GCD
    // of modulo power and c.
    return gcd(modexpo, c);
}

// Driver code
public static void Main()
{
    long a = 10248585,
         n = 1000000, c = 12564;
    Console.Write(gcdPow(a, n, c));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find GCD
// of a^n and b.

/* Iterative Function to calculate
   (x^y)%p in O(log y) */
function modPower($x, $y, $p)
{
    $res = 1; // Initialize result

    $x = $x % $p; // Update x if it is more
                  // than or equal to p

    while ($y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Finds GCD of a and b
function gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return gcd($b, $a % $b);
}

// Finds GCD of a^n and c
function gcdPow($a, $n, $c)
{
    // check if c is a divisor of a
    if ($a % $c == 0)
        return $c;

    // First compute (a^n) % c
    $modexpo = modPower($a, $n, $c);

    // Now simply return GCD
    // of modulo power and c.
    return gcd($modexpo, $c);
}

// Driver code
$a = 10248585;
$n = 1000000;
$c = 12564;
echo gcdPow($a, $n, $c);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>
// Javascript program to find
// GCD of a^n and b.

    /* Iterative Function to calculate
(x^y)%p in O(log y) */
    function modPower(x,y,p)
    {
        let res = 1; // Initialize result

    x = x % p; // Update x if it is more
               // than or equal to p

    while (y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ((y & 1) > 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
    }

    // Finds GCD of a and b
    function gcd(a,b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Finds GCD of a^n and c
    function gcdPow(a,n,c)
    {
        // check if c is a divisor of a
    if (a % c == 0)
        return c;

    // First compute (a^n) % c
    let modexpo = modPower(a, n, c);

    // Now simply return GCD
    // of modulo power and c.
    return gcd(modexpo, c);
    }

    // Driver code
    let a = 10248585,
         n = 1000000, c = 12564;
    document.write(gcdPow(a, n, c));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
9
```