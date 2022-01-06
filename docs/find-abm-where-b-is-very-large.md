# 查找(a^b)%m 其中‘b’很大

> 原文:[https://www . geesforgeks . org/find-abm-where-b-is-非常大/](https://www.geeksforgeeks.org/find-abm-where-b-is-very-large/)

给定三个数字 a、b 和 m，其中 1 <=a, m<=10^6\. Given very large ‘b’ containing up to 10^6 digits and m is a prime number, the task is to find (a^b)%m.
**例如:**

> **输入:** a = 2，b = 3，m = 17
> **输出:** 8
> 2 ^ 3 % 17 = 8
> **输入:** a = 3，b = 1000000000000000000000，m = 100000000007
> **输出:** 835987331

**进场:**根据[费马小定理](https://www.geeksforgeeks.org/fermats-little-theorem/)，

```
a^(p-1) mod p = 1, When p is prime.
```

由此，作为问题，m 是质数，表示 A^B 模 m 如下:

```
A^B mod M = ( A^(M-1) * A^(M-1) *.......* A^(M-1) * A^(x) ) mod M
```

其中 x 是 B mod M-1，A ^ (M-1)继续 B/(M-1)次
现在，根据费马小定理，

```
A ^ (M-1) mod M = 1.
```

因此，

```
A^B mod M = ( 1 * 1 * ....... * 1 * A^(x) ) mod M
```

因此 mod B 用 M-1 把这个数减少到一个更小的数，然后用[幂()](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)的方法来计算(a^b)%m.
下面是上述方法的实现:

## C++

```
// C++ program to find
// (a^b)%m for b very large.
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to find power
ll power(ll x, ll y, ll p)
{
    ll res = 1; // Initialize result

    // Update x if it is more than or
    // equal to p
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x
        // with the result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}
// Driver Code
int main()
{
    ll a = 3;

    // String input as b is very large
    string b = "100000000000000000000000000";

    ll remainderB = 0;
    ll MOD = 1000000007;

    // Reduce the number B to a small number
    // using Fermat Little
    for (int i = 0; i < b.length(); i++)
        remainderB = (remainderB * 10 +
                       b[i] - '0') % (MOD - 1);

    cout << power(a, remainderB, MOD) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// (a^b)%m for b very large.
import java.io.*;

class GFG
{

// Function to find power
static long power(long x,
                  long y, long p)
{
    long res = 1; // Initialize result

    // Update x if it is more
    // than or equal to p
    x = x % p;

    while (y > 0)
    {
        // If y is odd, multiply
        // x with the result
        if ((y & 1) > 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Driver Code
public static void main (String[] args)
{
long a = 3;

// String input as
// b is very large
String b = "100000000000000000000000000";

long remainderB = 0;
long MOD = 1000000007;

// Reduce the number B to a small
// number using Fermat Little
for (int i = 0; i < b.length(); i++)
    remainderB = (remainderB * 10 +
                  b.charAt(i) - '0') %
                 (MOD - 1);

System.out.println(power(a, remainderB, MOD));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to find
# (a^b)%m for b very large.

# Function to find power
def power(x, y, p):
    res = 1 # Initialize result

    # Update x if it is
    # more than or equal to p
    x = x % p

    while (y > 0):

        # If y is odd, multiply
        # x with the result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# Driver Code
a = 3

# String input as b
# is very large
b = "100000000000000000000000000"

remainderB = 0
MOD = 1000000007

# Reduce the number B
# to a small number
# using Fermat Little
for i in range(len(b)):
    remainderB = ((remainderB * 10 +
                   ord(b[i]) - 48) %
                   (MOD - 1))

print(power(a, remainderB, MOD))

# This code is contributed by mits
```

## C#

```
// C# program to find
// (a^b)%m for b very large.
using System;

class GFG
{

// Function to find power
static long power(long x,
                  long y, long p)
{
    // Initialize result
    long res = 1;

    // Update x if it is more
    // than or equal to p
    x = x % p;

    while (y > 0)
    {
        // If y is odd, multiply
        // x with the result
        if ((y & 1) > 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Driver Code
public static void Main ()
{
    long a = 3;

    // String input as
    // b is very large
    string b = "100000000000000000000000000";

    long remainderB = 0;
    long MOD = 1000000007;

    // Reduce the number B to
    // a small number using
    // Fermat Little
    for (int i = 0; i < b.Length; i++)
        remainderB = (remainderB * 10 +
                          b[i] - '0') %
                             (MOD - 1);

    Console.WriteLine(power(a, remainderB, MOD));
}
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// (a^b)%m for b very large.

// Function to find power
function power($x, $y, $p)
{
    $res = 1; // Initialize result

    // Update x if it is
    // more than or equal to p
    $x = $x % $p;

    while ($y > 0)
    {
        // If y is odd, multiply
        // x with the result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Driver Code
$a = 3;

// String input as b
// is very large
$b = "100000000000000000000000000";

$remainderB = 0;
$MOD = 1000000007;

// Reduce the number B
// to a small number
// using Fermat Little
for ($i = 0; $i < strlen($b); $i++)
    $remainderB = ($remainderB * 10 +
                   $b[$i] - '0') %
                  ($MOD - 1);

echo power($a, $remainderB, $MOD);

// This code is contributed by mits
?>
```

**Output:** 

```
835987331
```