# 寻找第 n 个斐波那契数的位数

> 原文:[https://www . geesforgeks . org/find-第 n 位数-fibonacci-number/](https://www.geeksforgeeks.org/finding-number-of-digits-in-nth-fibonacci-number/)

给定一个数字 n，求第 n 个斐波那契数的位数。前几个斐波那契数是 0，1，1，2，3，5，8，13，21，34，55，89，144，…
**例:**

```
Input : n = 6
Output : 1
6'th Fibonacci number is 8 and it has 
1 digit.

Input : n = 12
Output : 3
12'th Fibonacci number is 144 and it has 
3 digits.
```

一个**简单的解决方法**是找到[第 n 个斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，然后计算其中的位数。这种解决方案可能会导致大数值 n 的溢出问题
A **直接方法**是使用下面的比奈公式计算第 n 个斐波那契数的位数。

```
fib(n) = (Φn - Ψ-n) / √5
where
Φ = (1 + √5) / 2
Ψ = (1 - √5) / 2

The above formula can be simplified, 
fib(n) = round(Φn / √5) 
Here round function indicates nearest integer.

Count of digits in Fib(n) = Log10Fib(n)
                          = Log10(Φn / √5)
                          = n*Log10(Φ) - Log10√5
                          = n*Log10(Φ) - (Log105)/2
```

正如[这个](https://www.geeksforgeeks.org/g-fact-18-2/) G-Fact 中提到的，由于浮点运算的限制，这个公式似乎不起作用，不能产生正确的斐波那契数。然而，用这个公式来计算第 n 个斐波那契数的位数似乎是可行的。
以下是以上想法的实现:

## C++

```
/* C++ program to find number of digits in nth
   Fibonacci number */
#include<bits/stdc++.h>
using namespace std;

// This function returns the number of digits
// in nth Fibonacci number after ceiling it
// Formula used (n * log(phi) - (log 5) / 2)
long long numberOfDigits(long long n)
{
    if (n == 1)
        return 1;

    // using phi = 1.6180339887498948
    long double d = (n * log10(1.6180339887498948)) -
                    ((log10(5)) / 2);

    return ceil(d);
}

// Driver program to test the above function
int main()
{
    long long i;
    for (i = 1; i <= 10; i++)
    cout << "Number of Digits in F("
         << i <<") - "
         << numberOfDigits(i) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program  to find number of digits in nth
// Fibonacci number

class GFG
{
    // This function returns the number of digits
    // in nth Fibonacci number after ceiling it
    // Formula used (n * log(phi) - (log 5) / 2)
    static double numberOfDigits(double n)
    {
        if (n == 1)
            return 1;

        // using phi = 1.6180339887498948
        double d = (n * Math.log10(1.6180339887498948)) -
                   ((Math.log10(5)) / 2);

        return Math.ceil(d);
    }

    // Driver code
    public static void main (String[] args)
    {
        double i;
        for (i = 1; i <= 10; i++)
        System.out.println("Number of Digits in F("+i+") - "
                           +numberOfDigits(i));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# number of digits in nth
# Fibonacci number
import math

# storing value of
# golden ratio aka phi
phi = (1 + 5**.5) / 2

# function to find number
# of digits in F(n) This
# function returns the number
# of digitsin nth Fibonacci
# number after ceiling it
# Formula used (n * log(phi) -
# (log 5) / 2)
def numberOfDig (n) :
    if n == 1 :
        return 1
    return math.ceil((n * math.log10(phi) -
                      .5 * math.log10(5)))

// Driver Code
for i in range(1, 11) :
    print("Number of Digits in F(" +
                   str(i) + ") - " +
                str(numberOfDig(i)))

# This code is contributed by SujanDutta
```

## C#

```
// C# program to find number of
// digits in nth Fibonacci number
using System;

class GFG {

    // This function returns the number of digits
    // in nth Fibonacci number after ceiling it
    // Formula used (n * log(phi) - (log 5) / 2)
    static double numberOfDigits(double n)
    {
        if (n == 1)
            return 1;

        // using phi = 1.6180339887498948
        double d = (n * Math.Log10(1.6180339887498948)) -
                   ((Math.Log10(5)) / 2);

        return Math.Ceiling(d);
    }

    // Driver code
    public static void Main ()
    {
        double i;
        for (i = 1; i <= 10; i++)
        Console.WriteLine("Number of Digits in F("+ i +") - "
                           + numberOfDigits(i));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of
// digits in nth Fibonacci number

// This function returns the
// number of digits in nth
// Fibonacci number after
// ceiling it Formula used
// (n * log(phi) - (log 5) / 2)
function numberOfDigits($n)
{
    if ($n == 1)
        return 1;

    // using phi = 1.6180339887498948
    $d = ($n * log10(1.6180339887498948)) -
                          ((log10(5)) / 2);

    return ceil($d);
}

    // Driver Code
    $i;
    for ($i = 1; $i <= 10; $i++)
    echo "Number of Digits in F($i) - "
         , numberOfDigits($i), "\n";

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>// Javascript program to find number of
// digits in nth Fibonacci number

// This function returns the
// number of digits in nth
// Fibonacci number after
// ceiling it Formula used
// (n * log(phi) - (log 5) / 2)
function numberOfDigits(n)
{
    if (n == 1)
        return 1;

    // using phi = 1.6180339887498948
    let d = (n * Math.log10(1.6180339887498948)) -
                        ((Math.log10(5)) / 2);

    return Math.ceil(d);
}

    // Driver Code
    let i;
    for (let i = 1; i <= 10; i++)
    document.write(`Number of Digits in F(${i}) - ${numberOfDigits(i)} <br>`);

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
Number of Digits in F(1) - 1
Number of Digits in F(2) - 1
Number of Digits in F(3) - 1
Number of Digits in F(4) - 1
Number of Digits in F(5) - 1
Number of Digits in F(6) - 1
Number of Digits in F(7) - 2
Number of Digits in F(8) - 2
Number of Digits in F(9) - 2
Number of Digits in F(10) - 2
```

**参考文献:**
[http://www . mathematics . surrey . AC . uk/hosted-sites/R .克诺特/Fibonacci/fib formula . html # section 2](http://www.maths.surrey.ac.uk/hosted-sites/R.Knott/Fibonacci/fibFormula.html#section2)
[https://en.wikipedia.org/wiki/Fibonacci_number](https://en.wikipedia.org/wiki/Fibonacci_number)
本文由 **Ayush Khanduri** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。