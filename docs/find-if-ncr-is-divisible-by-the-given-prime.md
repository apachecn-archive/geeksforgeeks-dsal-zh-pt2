# 找出 nCr 是否能被给定的素数整除

> 原文:[https://www . geeksforgeeks . org/find-if-NCR-被给定素数除尽/](https://www.geeksforgeeks.org/find-if-ncr-is-divisible-by-the-given-prime/)

给定三个整数 **N** 、 **R** 和 **P** ，其中 **P** 为素数，任务是找出**T9】NC<sub>R</sub>T13】是否能被 **P** 整除。
**举例:**** 

> **输入:** N = 6，R = 2，P = 7
> **输出:**No
> <sup>6</sup>C<sub>2</sub>= 15 不能被 7 整除。
> **输入:** N = 7，R = 2，P = 3
> **输出:**是
> <sup>7</sup> C <sub>2</sub> = 21，可被 3 整除。

**进场:**我们知道**T3】NC<sub>R</sub>= N！/ (R！*(N–R)！)**。现在使用[勒让德公式](https://www.geeksforgeeks.org/legendres-formula-highest-power-of-prime-number-that-divides-n/)，求 **P** 除以任意 **N 的最大幂！**、 **R！**和 **(N -R)！**分别表示 **x1** 、 **x2** 和 **x3** 。
为了使**<sup>N</sup>C<sub>R</sub>**能够被 **P** 整除，必须满足条件 **x1 > x2 + x3** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to return the highest
// power of p that divides n!
// implementing Legendre Formula
int getfactor(int n, int p)
{
    int pw = 0;

    while (n) {
        n /= p;
        pw += n;
    }

    // Return the highest power of p
    // which divides n!
    return pw;
}

// Function that returns true
// if nCr is divisible by p
bool isDivisible(int n, int r, int p)
{
    // Find the highest powers of p
    // that divide n!, r! and (n - r)!
    int x1 = getfactor(n, p);
    int x2 = getfactor(r, p);
    int x3 = getfactor(n - r, p);

    // If nCr is divisible by p
    if (x1 > x2 + x3)
        return true;

    return false;
}

// Driver code
int main()
{
    int n = 7, r = 2, p = 7;

    if (isDivisible(n, r, p))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of above approach
import java.io.*;

class GFG
{

// Function to return the highest
// power of p that divides n!
// implementing Legendre Formula
static int getfactor(int n, int p)
{
    int pw = 0;

    while (n != 0)
    {
        n /= p;
        pw += n;
    }

    // Return the highest power of p
    // which divides n!
    return pw;
}

// Function to return N digits
// number which is divisible by D
static int isDivisible(int n, int r, int p)
{
    // Find the highest powers of p
    // that divide n!, r! and (n - r)!
    int x1 = getfactor(n, p);
    int x2 = getfactor(r, p);
    int x3 = getfactor(n - r, p);

    // If nCr is divisible by p
    if (x1 > x2 + x3)
        return 1;

    return 0;
}

// Driver code
public static void main (String[] args)
{
    int n = 7, r = 2, p = 7;

    if (isDivisible(n, r, p) == 1)
        System.out.print("Yes");
    else
        System.out.print("No");

}
}

// This code is contributed by krikti..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the highest
# power of p that divides n!
# implementing Legendre Formula
def getfactor(n, p) :

    pw = 0;

    while (n) :
        n //= p;
        pw += n;

    # Return the highest power of p
    # which divides n!
    return pw;

# Function that returns true
# if nCr is divisible by p
def isDivisible(n, r, p) :

    # Find the highest powers of p
    # that divide n!, r! and (n - r)!
    x1 = getfactor(n, p);
    x2 = getfactor(r, p);
    x3 = getfactor(n - r, p);

    # If nCr is divisible by p
    if (x1 > x2 + x3) :
        return True;

    return False;

# Driver code
if __name__ == "__main__" :

    n = 7; r = 2; p = 7;

    if (isDivisible(n, r, p)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# Implementation of above approach
using System;

class GFG
{

// Function to return the highest
// power of p that divides n!
// implementing Legendre Formula
static int getfactor(int n, int p)
{
    int pw = 0;

    while (n != 0)
    {
        n /= p;
        pw += n;
    }

    // Return the highest power of p
    // which divides n!
    return pw;
}

// Function to return N digits
// number which is divisible by D
static int isDivisible(int n, int r, int p)
{
    // Find the highest powers of p
    // that divide n!, r! and (n - r)!
    int x1 = getfactor(n, p);
    int x2 = getfactor(r, p);
    int x3 = getfactor(n - r, p);

    // If nCr is divisible by p
    if (x1 > x2 + x3)
        return 1;

    return 0;
}

// Driver code
static public void Main ()
{
    int n = 7, r = 2, p = 7;

    if (isDivisible(n, r, p) == 1)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
    // Javascript Implementation of above approach

    // Function to return the highest
    // power of p that divides n!
    // implementing Legendre Formula
    function getfactor(n, p)
    {
        let pw = 0;

        while (n != 0)
        {
            n = parseInt(n / p, 10);
            pw += n;
        }

        // Return the highest power of p
        // which divides n!
        return pw;
    }

    // Function to return N digits
    // number which is divisible by D
    function isDivisible(n, r, p)
    {
        // Find the highest powers of p
        // that divide n!, r! and (n - r)!
        let x1 = getfactor(n, p);
        let x2 = getfactor(r, p);
        let x3 = getfactor(n - r, p);

        // If nCr is divisible by p
        if (x1 > x2 + x3)
            return 1;

        return 0;
    }

    let n = 7, r = 2, p = 7;

    if (isDivisible(n, r, p) == 1)
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```