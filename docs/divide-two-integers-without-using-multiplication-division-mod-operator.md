# 不使用乘法、除法和 mod 运算符将两个整数相除

> 原文:[https://www . geeksforgeeks . org/不使用乘法-除法-mod-operator/](https://www.geeksforgeeks.org/divide-two-integers-without-using-multiplication-division-mod-operator/)

给 a 两个整数，比如 a 和 b，不使用乘法、除法和 mod 运算符，求 a 除以 b 后的商。

**示例:**

```
Input : a = 10, b = 3
Output : 3

Input : a = 43, b = -8
Output :  -5 
```

**逼近:**不断从被除数中减去除数，直到被除数变得小于除数。被除数变成余数，做减法的次数变成商。下面是上述方法的实现:

## C++

```
// C++ implementation to Divide two
// integers without using multiplication,
// division and mod operator
#include <bits/stdc++.h>
using namespace std;

// Function to divide a by b and
// return floor value it
int divide(int dividend, int divisor) {

  // Calculate sign of divisor i.e.,
  // sign will be negative only iff
  // either one of them is negative
  // otherwise it will be positive
  int sign = ((dividend < 0) ^ (divisor < 0)) ? -1 : 1;

  // Update both divisor and
  // dividend positive
  dividend = abs(dividend);
  divisor = abs(divisor);

  // Initialize the quotient
  int quotient = 0;
  while (dividend >= divisor) {
    dividend -= divisor;
    ++quotient;
  }

  // Return the value of quotient with the appropriate sign.
  return quotient * sign;
}

// Driver code
int main() {
  int a = 10, b = 3;
  cout << divide(a, b) << "\n";

  a = 43, b = -8;
  cout << divide(a, b);

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*Java implementation to Divide two
integers without using multiplication,
division and mod operator*/

import java.io.*;

class GFG
{

    // Function to divide a by b and
    // return floor value it
    static int divide(int dividend, int divisor)
    {

        // Calculate sign of divisor i.e.,
        // sign will be negative only iff
        // either one of them is negative
        // otherwise it will be positive
        int sign = ((dividend < 0) ^
                   (divisor < 0)) ? -1 : 1;

        // Update both divisor and
        // dividend positive
        dividend = Math.abs(dividend);
        divisor = Math.abs(divisor);

        // Initialize the quotient
        int quotient = 0;

        while (dividend >= divisor)
        {
            dividend -= divisor;
            ++quotient;
        }
        //if the sign value computed earlier is -1 then negate the value of quotient
        if(sign==-1) quotient=-quotient;

        return quotient;
    }   

    public static void main (String[] args)
    {
        int a = 10;
        int b = 3;

        System.out.println(divide(a, b));

        a = 43;
        b = -8;

        System.out.println(divide(a, b));
    }
}

// This code is contributed by upendra singh bartwal.
```

## 蟒蛇 3

```
# Python 3 implementation to Divide two
# integers without using multiplication,
# division and mod operator

# Function to divide a by b and
# return floor value it
def divide(dividend, divisor):

    # Calculate sign of divisor i.e.,
    # sign will be negative only iff
    # either one of them is negative
    # otherwise it will be positive
    sign = -1 if ((dividend < 0) ^  (divisor < 0)) else 1

    # Update both divisor and
    # dividend positive
    dividend = abs(dividend)
    divisor = abs(divisor)

    # Initialize the quotient
    quotient = 0
    while (dividend >= divisor):
        dividend -= divisor
        quotient += 1

     #if the sign value computed earlier is -1 then negate the value of quotient

    if sign ==-1:
      quotient=-quotient

    return quotient

# Driver code
a = 10
b = 3
print(divide(a, b))
a = 43
b = -8
print(divide(a, b))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# implementation to Divide two without
// using multiplication, division and mod
// operator
using System;

class GFG {

    // Function to divide a by b and
    // return floor value it
    static int divide(int dividend, int divisor)
    {

        // Calculate sign of divisor i.e.,
        // sign will be negative only iff
        // either one of them is negative
        // otherwise it will be positive
        int sign = ((dividend < 0) ^
                (divisor < 0)) ? -1 : 1;

        // Update both divisor and
        // dividend positive
        dividend = Math.Abs(dividend);
        divisor = Math.Abs(divisor);

        // Initialize the quotient
        int quotient = 0;

        while (dividend >= divisor)
        {
            dividend -= divisor;
            ++quotient;
        }

        //if the sign value computed earlier is -1 then negate the value of quotient
       if(sign==-1) quotient=-quotient;
        return quotient;
    }

    public static void Main ()
    {

        int a = 10;
        int b = 3;
        Console.WriteLine(divide(a, b));

        a = 43;
        b = -8;
        Console.WriteLine(divide(a, b));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to Divide two
// integers without using multiplication,
// division and mod operator

// Function to divide a by b and
// return floor value it
function divide($dividend, $divisor) {

    // Calculate sign of divisor i.e.,
    // sign will be negative only iff
    // either one of them is negative
    // otherwise it will be positive
    $sign = (($dividend < 0) ^
             ($divisor < 0)) ? -1 : 1;

    // Update both divisor and
    // dividend positive
    $dividend = abs($dividend);
    $divisor = abs($divisor);

    // Initialize the quotient
    $quotient = 0;
    while ($dividend >= $divisor)
    {
        $dividend -= $divisor;
        ++$quotient;
    }
    //if the sign value computed earlier is -1 then negate the value of quotient
    if($sign==-1) $quotient=-$quotient;
    return $quotient;
}

// Driver code
$a = 10;
$b = 3;
echo divide($a, $b)."\n";

$a = 43;
$b = -8;
echo divide($a, $b);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript implementation to Divide two
// integers without using multiplication,
// division and mod operator

// Function to divide a by b and
// return floor value it
function divide(dividend, divisor) {

// Calculate sign of divisor i.e.,
// sign will be negative only iff
// either one of them is negative
// otherwise it will be positive
let sign = ((dividend < 0) ^ (divisor < 0)) ? -1 : 1;

// Update both divisor and
// dividend positive
dividend = Math.abs(dividend);
divisor = Math.abs(divisor);

// Initialize the quotient
let quotient = 0;
while (dividend >= divisor) {
    dividend -= divisor;
    ++quotient;
}
//if the sign value computed earlier is -1 then negate the value of quotient
if(sign==-1) quotient=-quotient;
return quotient;
}

// Driver code
let a = 10, b = 3;
document.write(divide(a, b) + "<br>");

a = 43, b = -8;
document.write(divide(a, b));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output**

```
3
-5
```