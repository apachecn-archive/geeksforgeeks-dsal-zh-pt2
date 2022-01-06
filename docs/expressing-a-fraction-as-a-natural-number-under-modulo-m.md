# 在模‘m’下将分数表示为自然数

> 原文:[https://www . geesforgeks . org/expressing-a-fraction-as-自然数-模下 m/](https://www.geeksforgeeks.org/expressing-a-fraction-as-a-natural-number-under-modulo-m/)

给定两个整数 **A** 和 **B** ，其中 **A** 不能被 **B** 整除，任务是将 **A / B** 表示为自然数模 **m** ，其中 **m = 1000000007** 。
**注意:**当我们需要表达事件的概率、曲线和多边形的面积等时，这种表示非常有用。
**举例:**

> **输入:** A = 2，B = 6
> **输出:**3333333336
> **输入:** A = 4，B = 5
> **输出:** 600000005

**方法:**我们知道， **A / B** 可以写成 **A * (1 / B)** 即 **A * (B ^ -1)** 。
已知模(%)运算符满足关系:

```
(a * b) % m = ( (a % m) * (b % m) ) % m
```

所以，我们可以写:

```
(b ^ -1) % m = (b ^ m-2) % m (Fermat's little theorem)
```

因此结果将是:

```
( (A mod m) * ( power(B, m-2) % m) ) % m
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define m 1000000007

// Function to return the GCD of given numbers
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Recursive function to return (x ^ n) % m
ll modexp(ll x, ll n)
{
    if (n == 0) {
        return 1;
    }
    else if (n % 2 == 0) {
        return modexp((x * x) % m, n / 2);
    }
    else {
        return (x * modexp((x * x) % m, (n - 1) / 2) % m);
    }
}

// Function to return the fraction modulo mod
ll getFractionModulo(ll a, ll b)
{
    ll c = gcd(a, b);

    a = a / c;
    b = b / c;

    // (b ^ m-2) % m
    ll d = modexp(b, m - 2);

    // Final answer
    ll ans = ((a % m) * (d % m)) % m;

    return ans;
}

// Driver code
int main()
{
    ll a = 2, b = 6;

    cout << getFractionModulo(a, b) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;

class GFG {

static long m  = 1000000007;

// Function to return the GCD of given numbers
 static long gcd(long a, long b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Recursive function to return (x ^ n) % m
static long modexp(long x, long n)
{
    if (n == 0) {
        return 1;
    }
    else if (n % 2 == 0) {
        return modexp((x * x) % m, n / 2);
    }
    else {
        return (x * modexp((x * x) % m, (n - 1) / 2) % m);
    }
}

// Function to return the fraction modulo mod
 static long getFractionModulo(long a, long b)
{
    long c = gcd(a, b);

    a = a / c;
    b = b / c;

    // (b ^ m-2) % m
    long  d = modexp(b, m - 2);

    // Final answer
    long ans = ((a % m) * (d % m)) % m;

    return ans;
}

// Driver code

    public static void main (String[] args) {
        long a = 2, b = 6;

    System.out.println(getFractionModulo(a, b));
    }
}
// This code is contributed by inder_verma
```

## 蟒蛇 3

```
# Python3 implementation of the approach
m = 1000000007

# Function to return the GCD
# of given numbers
def gcd(a, b):

    if (a == 0):
        return b
    return gcd(b % a, a)

# Recursive function to return (x ^ n) % m
def modexp(x, n):

    if (n == 0) :
        return 1

    elif (n % 2 == 0) :
        return modexp((x * x) % m, n // 2)

    else :
        return (x * modexp((x * x) % m,
                           (n - 1) / 2) % m)

# Function to return the fraction modulo mod
def getFractionModulo(a, b):

    c = gcd(a, b)

    a = a // c
    b = b // c

    # (b ^ m-2) % m
    d = modexp(b, m - 2)

    # Final answer
    ans = ((a % m) * (d % m)) % m

    return ans

# Driver code
if __name__ == "__main__":

    a = 2
    b = 6

    print ( getFractionModulo(a, b))

# This code is contributed by ita_c
```

## C#

```
//C#  implementation of the approach

using System;

public class GFG{

static long m = 1000000007;

// Function to return the GCD of given numbers
static long gcd(long a, long b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Recursive function to return (x ^ n) % m
static long modexp(long x, long n)
{
    if (n == 0) {
        return 1;
    }
    else if (n % 2 == 0) {
        return modexp((x * x) % m, n / 2);
    }
    else {
        return (x * modexp((x * x) % m, (n - 1) / 2) % m);
    }
}

// Function to return the fraction modulo mod
static long getFractionModulo(long a, long b)
{
    long c = gcd(a, b);

    a = a / c;
    b = b / c;

    // (b ^ m-2) % m
    long d = modexp(b, m - 2);

    // Final answer
    long ans = ((a % m) * (d % m)) % m;

    return ans;
}

// Driver code

    static public void Main (){

        long a = 2, b = 6;
        Console.WriteLine(getFractionModulo(a, b));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the GCD of
// given numbers
function abc($a, $b)
{
    if ($a == 0)
        return $b;
    return abc($b % $a, $a);
}

// Recursive function to return (x ^ n) % m
function modexp($x, $n)
{
    $m = 1000000007;
    if ($n == 0)
    {
        return 1;
    }
    else if ($n % 2 == 0)
    {
        return modexp(($x * $x) % $m, $n / 2);
    }
    else
    {
        return ($x * modexp(($x * $x) % $m,
                        ($n - 1) / 2) % $m);
    }
}

// Function to return the fraction
// modulo mod
function getFractionModulo($a, $b)
{
    $m = 1000000007;
    $c = abc($a, $b);

    $a = $a / $c;
    $b = $b / $c;

    // (b ^ m-2) % m
    $d = modexp($b, $m - 2);

    // Final answer
    $ans = (($a % $m) * ($d % $m)) % $m;

    return $ans;
}

// Driver code
$a = 2;
$b = 6;

echo(getFractionModulo($a, $b)) ;

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
var m = 100000007;

    // Function to return the GCD of given numbers
    function gcd(a , b) {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Recursive function to return (x ^ n) % m
    function modexp(x , n) {
        if (n == 0) {
            return 1;
        } else if (n % 2 == 0) {
            return modexp((x * x) % m, n / 2);
        } else {
            return (x * modexp((x * x) % m, (n - 1) / 2) % m);
        }
    }

    // Function to return the fraction modulo mod
    function getFractionModulo(a , b) {
        var c = gcd(a, b);

        a = a / c;
        b = b / c;

        // (b ^ m-2) % m
        var d = modexp(b, m - 2);

        // Final answer
        var ans = ((a % m) * (d % m)) % m;

        return ans;
    }

    // Driver code

        var a = 2, b = 6;

        document.write(getFractionModulo(a, b));

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
333333336
```

**时间复杂度:** O(log(min(a，b) + logm)
T3】辅助空间: O(log(min(a，b)+logm)