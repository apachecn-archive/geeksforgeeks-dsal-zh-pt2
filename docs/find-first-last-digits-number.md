# 查找一个数字的第一个和最后一个数字

> 原文:[https://www . geesforgeks . org/find-first-last-digits-number/](https://www.geeksforgeeks.org/find-first-last-digits-number/)

给定一个数字并找出数字的第一个和最后一个数字。
**例:**

```
Input : 12345 
Output : First digit: 1
         last digit : 5

Input : 98562
Output : First digit: 9
         last digit : 2
```

为了找到数字的最后一位，我们使用**模运算符%** 。当模除以 10 时，返回其最后一位数字。
假设如果 n = 1234
那么最后一位数字= n % 10 = > 4
查找一个数字的第一位数字比最后一位数字稍微贵一点。为了找到一个数的第一个数字，我们把给定的数除以 10，直到数大于 10。最后我们剩下第一个数字。

**接近 1(带循环):**

## C++

```
// Program to find first and last
// digits of a number
#include <bits/stdc++.h>
using namespace std;

// Find the first digit
int firstDigit(int n)
{
    // Remove last digit from number
    // till only one digit is left
    while (n >= 10)
        n /= 10;

    // return the first digit
    return n;
}

// Find the last digit
int lastDigit(int n)
{
    // return the last digit
    return (n % 10);
}

// Driver program
int main()
{
    int n = 98562;
    cout << firstDigit(n) << " "
        << lastDigit(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find first and last
// digits of a number
import java.util.*;
import java.lang.*;

public class GfG{

    // Find the first digit
    public static int firstDigit(int n)
    {
        // Remove last digit from number
        // till only one digit is left
        while (n >= 10)
            n /= 10;

        // return the first digit
        return n;
    }

    // Find the last digit
    public static int lastDigit(int n)
    {
        // return the last digit
        return (n % 10);
    }

    // driver function
    public static void main(String argc[])
    {
        int n = 98562;
        System.out.println(firstDigit(n) + " "
        + lastDigit(n));
    }
}

// This code is contributed by Sagar Shukla
```

## 蟒蛇 3

```
# Python3 program to find first and
# last digits of a number

# Find the first digit
def firstDigit(n) :

    # Remove last digit from number
    # till only one digit is left
    while n >= 10:
        n = n / 10;

    # return the first digit
    return int(n)

# Find the last digit
def lastDigit(n) :

    # return the last digit
    return (n % 10)

# Driver Code
n = 98562;
print(firstDigit(n), end = " ")
print(lastDigit(n))

# This code is contributed by rishabh_jain
```

## C#

```
// C# Program to find first and last
// digits of a number
using System;

public class GfG{

    // Find the first digit
    public static int firstDigit(int n)
    {
        // Remove last digit from number
        // till only one digit is left
        while (n >= 10)
            n /= 10;

        // return the first digit
        return n;
    }

    // Find the last digit
    public static int lastDigit(int n)
    {
        // return the last digit
        return (n % 10);
    }

    // driver function
    public static void Main()
    {
        int n = 98562;
        Console.WriteLine(firstDigit(n) + " "
        + lastDigit(n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find first
// and last digits of a number

// Find the first digit
function firstDigit($n)
{
    // Remove last digit from number
    // till only one digit is left
    while ($n >= 10)
        $n /= 10;

    // return the first digit
    return (int)$n;
}

// Find the last digit
function lastDigit($n)
{
    // return the last digit
    return ((int)$n % 10);
}

// Driver Code
$n = 98562;
echo firstDigit($n) . " " .
     lastDigit($n) . "\n";

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>
// javascript Program to find first and last
// digits of a number

    // Find the first digit
    function firstDigit(n)
    {
        // Remove last digit from number
        // till only one digit is left
        while (n >= 10)
            n /= 10;

        // return the first digit
        return Math.floor(n);
    }

    // Find the last digit
    function lastDigit(n)
    {
        // return the last digit
        return Math.floor(n % 10);
    }

// Driver code

         let n = 98562;
        document.write(firstDigit(n) + " "
        + lastDigit(n));

 // This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
9 2
```

**接近 2(无回路)**

## C++

```
// Program to find first and last
// digits of a number
#include <bits/stdc++.h>
using namespace std;

// Find the first digit
int firstDigit(int n)
{
    // Find total number of digits - 1
    int digits = (int)log10(n);

    // Find first digit
    n = (int)(n / pow(10, digits));

    // Return first digit
    return n;
}

// Find the last digit
int lastDigit(int n)
{
    // return the last digit
    return (n % 10);
}

// Driver program
int main()
{
    int n = 98562;
    cout << firstDigit(n) << " "
         << lastDigit(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first and
// last  digits of a number
import java.math.*;

class GFG {

    // Find the first digit
    static int firstDigit(int n)
    {
        // Find total number of digits - 1
        int digits = (int)(Math.log10(n));

        // Find first digit
        n = (int)(n / (int)(Math.pow(10, digits)));

        // Return first digit
        return n;
    }

    // Find the last digit
    static int lastDigit(int n)
    {
        // return the last digit
        return (n % 10);
    }

    // Driver program
    public static void main(String args[])
    {
        int n = 98562;
        System.out.println(firstDigit(n) +
                           " " + lastDigit(n));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 program to find first 
# and last digits of a number
import math

# Find the first digit
def firstDigit(n) :

    # Find total number of digits - 1
    digits = (int)(math.log10(n))

    # Find first digit
    n = (int)(n / pow(10, digits))

    # Return first digit
    return n;

# Find the last digit
def lastDigit(n) :

    # return the last digit
    return (n % 10)

# Driver Code
n = 98562;
print(firstDigit(n), end = " ")
print(lastDigit(n))

# This code is contributed by rishabh_jain
```

## C#

```
// C# program to find first and
// last digits of a number
using System;

class GFG {

    // Find the first digit
    static int firstDigit(int n)
    {
        // Find total number of digits - 1
        int digits = (int)(Math.Log10(n));

        // Find first digit
        n = (int)(n / (int)(Math.Pow(10, digits)));

        // Return first digit
        return n;
    }

    // Find the last digit
    static int lastDigit(int n)
    {
        // return the last digit
        return (n % 10);
    }

    // Driver program
    public static void Main()
    {
        int n = 98562;
        Console.WriteLine(firstDigit(n) +
                        " " + lastDigit(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find first and last
// digits of a number

// Find the first digit
function firstDigit($n)
{
    // Find total number of digits - 1
    $digits = (int)log10($n);

    // Find first digit
    $n = (int)($n / pow(10, $digits));

    // Return first digit
    return $n;
}

// Find the last digit
function lastDigit($n)
{
    // return the last digit
    return ($n % 10);
}

// Driver Code
$n = 98562;
echo firstDigit($n) , " ",
     lastDigit($n), "\n";

// This code is contributed by ajit
?>
```

**输出:**

```
9 2
```

**重要提示:** log10()是 math.h 头文件中存在的一个数学函数。它将传递给 log10()函数的参数的 log base 10 值返回。