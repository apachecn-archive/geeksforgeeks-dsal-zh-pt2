# 费马小定理

> 原文:[https://www.geeksforgeeks.org/fermats-little-theorem/](https://www.geeksforgeeks.org/fermats-little-theorem/)

[费马小定理](https://en.wikipedia.org/wiki/Fermat%27s_little_theorem)指出，如果 p 是素数，那么对于任意整数 a，数字 a<sup>p</sup>–a 是 p 的整数倍

> 这里 p 是一个质数
> **a<sup>p</sup>a(mod p)。**

**特例:**如果 a 不能被 p 整除，费马小定理等价于 a <sup>p-1</sup> -1 是 p 的整数倍
的说法

> a<sup>p-1</sup>≡1(mod p)
> OR
> a<sup>p-1</sup>% p = 1
> 这里 a 不能被 p 整除。

**举个例子费马小定理是如何工作的**T2【例子:

```
 P = an integer Prime number   
 a = an integer which is not multiple of P  
 Let a = 2 and P = 17 

 According to Fermat's little theorem 
  2 17 - 1    ≡ 1 mod(17)
 we got  65536 % 17 ≡ 1   
 that mean (65536-1) is an multiple of 17 
```

**利用费马大定理**
如果我们知道 m 是素数，那么我们也可以利用费马大定理求逆。
a <sup>m-1</sup> ≡ 1 (mod m)
如果我们用 a <sup>-1</sup> 将两边相乘，我们得到
a<sup>-1</sup>≡a<sup>m-2</sup>(mod m)
以下是上面
的实现

## C++

```
// C++ program to find modular inverse of a
// under modulo m using Fermat's little theorem.
// This program works only if m is prime.
#include <bits/stdc++.h>
using namespace std;

// To compute x raised to power y under modulo m
int power(int x, unsigned int y, unsigned int m);

// Function to find modular inverse of a under modulo m
// Assumption: m is prime
void modInverse(int a, int m)
{
    if (__gcd(a, m) != 1)
        cout << "Inverse doesn't exist";

    else {

        // If a and m are relatively prime, then
        // modulo inverse is a^(m-2) mode m
        cout << "Modular multiplicative inverse is "
             << power(a, m - 2, m);
    }
}

// To compute x^y under modulo m
int power(int x, unsigned int y, unsigned int m)
{
    if (y == 0)
        return 1;
    int p = power(x, y / 2, m) % m;
    p = (p * p) % m;

    return (y % 2 == 0) ? p : (x * p) % m;
}

// Driver Program
int main()
{
    int a = 3, m = 11;
    modInverse(a, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find modular
// inverse of a under modulo m
// using Fermat's little theorem.
// This program works only if m is prime.

class GFG
{
    static int __gcd(int a, int b)
    {

        if(b == 0)
        {
            return a;
        }
        else
        {
            return __gcd(b, a % b);
        }
    }

    // To compute x^y under modulo m
    static int power(int x,int y,int m)
    {
        if (y == 0)
            return 1;
        int p = power(x, y / 2, m) % m;
        p = (p * p) % m;

        return (y % 2 == 0) ? p : (x * p) % m;
    }

    // Function to find modular
    // inverse of a under modulo m
    // Assumption: m is prime
    static void modInverse(int a, int m)
    {
        if (__gcd(a, m) != 1)
            System.out.print("Inverse doesn't exist");

        else {

            // If a and m are relatively prime, then
            // modulo inverse is a^(m-2) mode m
            System.out.print("Modular multiplicative inverse is "
                                            +power(a, m - 2, m));
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int a = 3, m = 11;
        modInverse(a, m);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# modular inverse of a
# under modulo m using
# Fermat's little theorem.
# This program works
# only if m is prime.

def __gcd(a,b):

    if(b == 0):
        return a
    else:
        return __gcd(b, a % b)

# To compute x^y under modulo m
def power(x,y,m):

    if (y == 0):
        return 1
    p = power(x, y // 2, m) % m
    p = (p * p) % m

    return p if(y % 2 == 0) else  (x * p) % m

# Function to find modular
# inverse of a under modulo m
# Assumption: m is prime
def modInverse(a,m):

    if (__gcd(a, m) != 1):
        print("Inverse doesn't exist")

    else:

        # If a and m are relatively prime, then
        # modulo inverse is a^(m-2) mode m
        print("Modular multiplicative inverse is ",
             power(a, m - 2, m))

# Driver code

a = 3
m = 11
modInverse(a, m)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find modular
// inverse of a under modulo m
// using Fermat's little theorem.
// This program works only if m is prime.
using System;

class GFG
{
    static int __gcd(int a, int b)
    {

        if(b == 0)
        {
            return a;
        }
        else
        {
            return __gcd(b, a % b);
        }
    }

    // To compute x^y under modulo m
    static int power(int x, int y, int m)
    {
        if (y == 0)
            return 1;
        int p = power(x, y / 2, m) % m;
        p = (p * p) % m;

        return (y % 2 == 0) ? p : (x * p) % m;
    }

    // Function to find modular
    // inverse of a under modulo m
    // Assumption: m is prime
    static void modInverse(int a, int m)
    {
        if (__gcd(a, m) != 1)
            Console.WriteLine("Modular multiplicative inverse is "
                                            +power(a, m - 2, m));

        else {

            // If a and m are relatively prime, then
            // modulo inverse is a^(m-2) mode m
            Console.WriteLine("Modular multiplicative inverse is "
                                            +power(a, m - 2, m));
        }
    }

    // Driver code
    public static void Main ()
    {
        int a = 3, m = 11;
        modInverse(a, m);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find modular inverse of a
// under modulo m using Fermat's little theorem.
// This program works only if m is prime.

// To compute x raised to
// power y under modulo m
// Recursive function to
// return gcd of a and b
function __gcd($a, $b)
{

    // Everything divides 0
    if ($a == 0 || $b == 0)
    return 0;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return __gcd($a-$b, $b);
    return __gcd($a, $b-$a);
}

// Function to find modular
// inverse of a under modulo m
// Assumption: m is prime
function modInverse($a, $m)
{
    if (__gcd($a, $m) != 1)
        echo "Inverse doesn't exist";

    else
    {

        // If a and m are relatively
        // prime, then modulo inverse
        // is a^(m-2) mode m
        echo "Modular multiplicative inverse is ",
                             power($a,$m - 2, $m);
    }
}

// To compute x^y under modulo m
function power($x, $y, $m)
{
    if ($y == 0)
        return 1;
    $p = power($x,$y / 2, $m) % $m;
    $p = ($p * $p) % $m;

    return ($y % 2 == 0) ? $p : ($x * $p) % $m;
}

    // Driver Code
    $a = 3; $m = 11;
    modInverse($a, $m);

// This code is contributed by anuj__67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find modular inverse of a
// under modulo m using Fermat's little theorem.
// This program works only if m is prime.

function __gcd(a, b)
{
    if(b == 0)
    {
        return a;
    }
    else
    {
        return __gcd(b, a % b);
    }
}
// Function to find modular inverse of a under modulo m
// Assumption: m is prime
function modInverse(a, m)
{
    if (__gcd(a, m) != 1)
        document.write( "Inverse doesn't exist");

    else {

        // If a and m are relatively prime, then
        // modulo inverse is a^(m-2) mode m
        document.write( "Modular multiplicative inverse is "
             + power(a, m - 2, m));
    }
}

// To compute x^y under modulo m
function power(x, y, m)
{
    if (y == 0)
        return 1;
    var p = power(x, parseInt(y / 2), m) % m;
    p = (p * p) % m;

    return (y % 2 == 0) ? p : (x * p) % m;
}

// Driver Program
var a = 3, m = 11;
modInverse(a, m);

// This code is contributed by rutvik_56.
</script>
```

输出:

```
Modular multiplicative inverse is 4
```

**一些基于费马小定理的文章**

*   [计算 nCr % p |集合 3(使用费马小定理)](https://www.geeksforgeeks.org/compute-ncr-p-set-3-using-fermat-little-theorem/)
*   [模乘逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)
*   [素性检验|集合 2(费马方法)](https://www.geeksforgeeks.org/primality-test-set-2-fermet-method/)
*   [模块 10^9+7 (1000000007)](https://www.geeksforgeeks.org/modulo-1097-1000000007/)