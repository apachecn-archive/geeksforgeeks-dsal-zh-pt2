# 不使用乘法、除法和 mod 运算符将两个整数相除| Set2

> 原文:[https://www . geesforgeks . org/divide-two-integer-not-use-乘除-mod-operator-set2/](https://www.geeksforgeeks.org/divide-two-integers-without-using-multiplication-division-and-mod-operator-set2/)

给定两个整数，比如 a 和 b，在不使用乘法、除法和 mod 运算符的情况下，求出 a 除以 b 后的商。
**例:**

```
Input: a = 10, b = 3
Output: 3

Input: a = 43, b = -8
Output: -5
```

这个问题已经在这里[讨论过了。](https://www.geeksforgeeks.org/divide-two-integers-without-using-multiplication-division-mod-operator/)在这篇文章中，讨论了一种不同的方法。
**进场:**

1.  让 a/b = c。
2.  取两边的原木
3.  对数(a)–对数(b) =对数(c)
4.  现在 RHS 日志在 LHS 可以写成 exp 了
5.  最终公式为:**exp(log(a)–log(b))= c**

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Returns the quotient of dividend/divisor.
void Divide(int a, int b)
{
    long long dividend = (long long)a;
    long long divisor = (long long)b;

    // Calculate sign of divisor i.e.,
    // sign will be negative only if
    // either one of them is negative
    // otherwise it will be positive

    long long sign = (dividend < 0) ^ (divisor < 0) ? -1 : 1;

    // Remove signs of dividend and divisor
    dividend = abs(dividend);
    divisor = abs(divisor);

    // Zero division Exception.
    if (divisor == 0) {
        cout << "Cannot Divide by 0" << endl;
        return;
    }

    if (dividend == 0) {
        cout << a << " / " << b << " is equal to : "
             << 0 << endl;
        return;
    }

    if (divisor == 1) {
        cout << a << " / " << b << " is equal to : "
             << sign * dividend << endl;
        return;
    }

    // Using Formula derived above.
    cout << a << " / " << b << " is equal to : "
         << sign * exp(log(dividend) - log(divisor))
         << endl;
}

// Drivers code
int main()
{
    int a = 10, b = 5;

    Divide(a, b);

    a = 49, b = -7;
    Divide(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// above approach
import java.io.*;

class GFG
{
static void Divide(int a, int b)
{
    long dividend = (long)a;
    long divisor = (long)b;

    // Calculate sign of divisor i.e.,
    // sign will be negative only if
    // either one of them is negative
    // otherwise it will be positive

    long sign = (dividend < 0) ^
                (divisor < 0) ? -1 : 1;

    // Remove signs of
    // dividend and divisor
    dividend = Math.abs(dividend);
    divisor = Math.abs(divisor);

    // Zero division Exception.
    if (divisor == 0)
    {
        System.out.println("Cannot Divide by 0");
        return;
    }

    if (dividend == 0)
    {
        System.out.println(a + " / " + b +
                            " is equal to : " + 0);
        return;
    }

    if (divisor == 1)
    {
        System.out.println(a + " / " + b +
                           " is equal to : " +
                             sign * dividend);
        return;
    }

    // Using Formula
    // derived above.
    System.out.println(a + " / " + b + " is equal to : " +
                                         Math.floor(sign *
                            (Math.exp(Math.log(dividend) -
                             Math.log(divisor)))));
}

// Driver code
public static void main (String[] args)
{
int a = 10, b = 5;

Divide(a, b);

a = 49; b = -7;
Divide(a, b);
}
}

// This code is contributed
// by shiv_bhakt.
```

## 蟒蛇 3

```
# Python3 program
# for above approach
import math
def Divide(a, b):
    dividend = a;
    divisor = b;

    # Calculate sign of divisor
    # i.e., sign will be negative
    # only if either one of them
    # is negative otherwise it
    # will be positive

    sign = -1 if ((dividend < 0) ^
                  (divisor < 0)) else 1;

    # Remove signs of
    # dividend and divisor
    dividend = abs(dividend);
    divisor = abs(divisor);

    # Zero division Exception.
    if (divisor == 0):
        print("Cannot Divide by 0");

    if (dividend == 0):
        print(a, "/", b, "is equal to :", 0);

    if (divisor == 1):
        print(a, "/", b, "is equal to :",
                      (sign * dividend));

    # Using Formula
    # derived above.
    print(a, "/", b, "is equal to :",
          math.floor(sign * math.exp(math.log(dividend) -
                                     math.log(divisor))));

# Driver code
a = 10;
b = 5;

Divide(a, b);

a = 49;
b = -7;
Divide(a, b);

# This code is contributed
# by mits
```

## C#

```
// C# program for
// above approach
using System;

class GFG
{
static void Divide(int a, int b)
{
    long dividend = (long)a;
    long divisor = (long)b;

    // Calculate sign of divisor
    // i.e., sign will be negative
    // only if either one of them
    // is negative otherwise it
    // will be positive

    long sign = (dividend < 0) ^
                (divisor < 0) ? -1 : 1;

    // Remove signs of
    // dividend and divisor
    dividend = Math.Abs(dividend);
    divisor = Math.Abs(divisor);

    // Zero division Exception.
    if (divisor == 0)
    {
        Console.WriteLine("Cannot Divide by 0");
        return;
    }

    if (dividend == 0)
    {
        Console.WriteLine(a + " / " + b +
                          " is equal to : " + 0);
        return;
    }

    if (divisor == 1)
    {
        Console.WriteLine(a + " / " + b +
                          " is equal to : " +
                            sign * dividend);
        return;
    }

    // Using Formula
    // derived above.
    Console.WriteLine(a + " / " + b + " is equal to : " +
                                        Math.Floor(sign *
                           (Math.Exp(Math.Log(dividend) -
                                   Math.Log(divisor)))));
}

// Driver code
public static void Main ()
{
    int a = 10, b = 5;

    Divide(a, b);

    a = 49; b = -7;
    Divide(a, b);
}
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for above approach

function Divide($a, $b)
{
    $dividend = $a;
    $divisor = $b;

    // Calculate sign of divisor
    // i.e., sign will be negative
    // only if either one of them
    // is negative otherwise it
    // will be positive

    $sign = ($dividend < 0) ^
            ($divisor < 0) ? -1 : 1;

    // Remove signs of
    // dividend and divisor
    $dividend = abs($dividend);
    $divisor = abs($divisor);

    // Zero division Exception.
    if ($divisor == 0)
    {
        echo "Cannot Divide by 0";
        echo"";
    }

    if ($dividend == 0)
    {
        echo $a , " / " , $b ,
             " is equal to : " , 0 ;
            echo "";
    }

    if ($divisor == 1)
    {
        echo $a , " / " , $b ,
             " is equal to : ",
             $sign * $dividend. "\n";
        echo "";
    }

    // Using Formula
    // derived above.
    echo $a , " / " , $b ,
         " is equal to : " ,
         $sign * exp(log($dividend) -
                      log($divisor)). "\n";
        echo "";
}

// Driver code
$a = 10;
$b = 5;

Divide($a, $b);

$a = 49;
$b = -7;
Divide($a, $b);

// This code is contributed
// by shiv_bhakt.
?>
```

## java 描述语言

```
<script>

// Javascript program for
// above approach

function Divide(a, b)
{
    var dividend = a;
    var divisor = b;

    // Calculate sign of divisor i.e.,
    // sign will be negative only if
    // either one of them is negative
    // otherwise it will be positive
    var sign = (dividend < 0) ^
                (divisor < 0) ? -1 : 1;

    // Remove signs of
    // dividend and divisor
    dividend = Math.abs(dividend);
    divisor = Math.abs(divisor);

    // Zero division Exception.
    if (divisor == 0)
    {
        document.write("Cannot Divide by 0");
        return;
    }

    if (dividend == 0)
    {
        document.write(a + " / " + b +
               " is equal to : " + 0 + "<br>");
        return;
    }

    if (divisor == 1)
    {
        System.out.println(a + " / " + b +
                           " is equal to : " +
                             sign * dividend + "<br>");
        return;
    }

    // Using Formula
    // derived above.
    document.write(a + " / " + b + " is equal to : " +
                           Math.floor(sign *
                          (Math.exp(Math.log(dividend) -
                          Math.log(divisor)))) + "<br>");
}

// Driver Code
var a = 10, b = 5;

Divide(a, b);

a = 49; b = -7;
Divide(a, b);

// This code is contributed by Kirti

</script>
```

**Output:** 

```
10 / 5 is equal to : 2
49 / -7 is equal to : -7
```