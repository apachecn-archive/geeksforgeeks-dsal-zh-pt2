# 不使用“/”运算符的除法

> 原文:[https://www . geesforgeks . org/division-不使用运算符/](https://www.geeksforgeeks.org/division-without-using-operator/)

给定两个数字，在不使用“/”运算符的情况下将一个数字除以另一个数字。
**例:**

```
Input : num1 = 13, num2 = 2
Output : 6

Input : num1 = 14, num2 = -2
Output : -7

Input : num1 = -11, num2 = 3
Output : -3

Input : num1 = 10, num2 = 10
Output : 1

Input : num1 = -6, num2 = -2
Output : 3

Input : num1 = 0, num2 = 5
Output : 0
```

为了在不使用“/”运算符的情况下执行除法运算，我们采用了一种方法，即计算 num1 减去 num2 的成功次数或完整次数。其中 num1 是要除的数，num2 是我们要除 num1 的数。

## C++

```
// CPP program to divide a number by other
// without using / operator
#include <bits/stdc++.h>
using namespace std;

// Function to find division without using
// '/' operator
int division(int num1, int num2)
{
   if (num1 == 0)
       return 0;
   if (num2 == 0)
     return INT_MAX;

   bool negResult = false;

   // Handling negative numbers
   if (num1 < 0)
   {
       num1 = -num1 ;
       if (num2 < 0)
           num2 = - num2 ;
       else
           negResult = true;
   }
   else if (num2 < 0)
   {
       num2 = - num2 ;
       negResult = true;
   }

   // if num1 is greater than equal to num2
   // subtract num2 from num1 and increase
   // quotient by one.
   int quotient = 0;
   while (num1 >= num2)
   {
       num1 = num1 - num2 ;
       quotient++ ;
   }

   // checking if neg equals to 1 then making
   // quotient negative
   if (negResult)
        quotient = - quotient ;
   return quotient ;
}

// Driver program
int main()
{
    int num1 = 13, num2 = 2 ;
    cout << division(num1, num2); ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to divide a number by other
// without using / operator
import java.io.*;

class GFG
{
    // Function to find division without using
    // '/' operator
    static int division(int num1, int num2)
    {
        if (num1 == 0)
            return 0;
        if (num2 == 0)
            return Integer.MAX_VALUE;

        boolean negResult = false;

        // Handling negative numbers
        if (num1 < 0)
        {
            num1 = -num1 ;
            if (num2 < 0)
                num2 = - num2 ;
            else
                negResult = true;
        }
        else if (num2 < 0)
        {
            num2 = - num2 ;
            negResult = true;
        }

        // if num1 is greater than equal to num2
        // subtract num2 from num1 and increase
        // quotient by one.
        int quotient = 0;
        while (num1 >= num2)
        {
            num1 = num1 - num2 ;
            quotient++ ;
        }

        // checking if neg equals to 1 then making
        // quotient negative
        if (negResult)
                quotient = - quotient ;
        return quotient ;
    }

    // Driver program
    public static void main (String[] args)
    {
        int num1 = 13, num2 = 2 ;
        System.out.println( division(num1, num2));

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to divide a number
# by other without using / operator

# Function to find division without 
# using '/' operator
def division(num1, num2):

    if (num1 == 0): return 0
    if (num2 == 0): return INT_MAX

    negResult = 0

    # Handling negative numbers
    if (num1 < 0):
        num1 = - num1

        if (num2 < 0):
            num2 = - num2
        else:
            negResult = true

    elif (num2 < 0):
        num2 = - num2
        negResult = true

    # if num1 is greater than equal to num2
    # subtract num2 from num1 and increase
    # quotient by one.
    quotient = 0

    while (num1 >= num2):
        num1 = num1 - num2
        quotient += 1

    # checking if neg equals to 1 then
    # making quotient negative
    if (negResult):
            quotient = - quotient
    return quotient

# Driver program
num1 = 13; num2 = 2
print(division(num1, num2))

# This code is contributed by Ajit.
```

## C#

```
// C# program to divide a number by other
// without using / operator
using System;

class GFG
{
    // Function to find division without
    // using '/' operator
    static int division(int num1, int num2)
    {
        if (num1 == 0)
            return 0;
        if (num2 == 0)
            return int.MaxValue;

        bool negResult = false;

        // Handling negative numbers
        if (num1 < 0)
        {
            num1 = -num1 ;
            if (num2 < 0)
                num2 = - num2 ;
            else
                negResult = true;
        }
        else if (num2 < 0)
        {
            num2 = - num2 ;
            negResult = true;
        }

        // if num1 is greater than equal to num2
        // subtract num2 from num1 and increase
        // quotient by one.
        int quotient = 0;
        while (num1 >= num2)
        {
            num1 = num1 - num2 ;
            quotient++ ;
        }

        // checking if neg equals to 1 then making
        // quotient negative
        if (negResult)
                quotient = - quotient ;
        return quotient ;
    }

    // Driver Code
    public static void Main ()
    {
        int num1 = 13, num2 = 2 ;
        Console.Write( division(num1, num2));

    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// CPP program to divide a number by other
// without using / operator

// Function to find division without using
// '/' operator

function division($num1, $num2)
{
    if ($num1 == 0)
        return 0;

    if ($num2 == 0)
        return INT_MAX;

    $negResult = false;

    // Handling negative numbers
    if ($num1 < 0)
    {
        $num1 = -$num1 ;

        if ($num2 < 0)
            $num2 = - $num2 ;
        else
            $negResult = true;
    }
    else if ($num2 < 0)
    {
        $num2 = - $num2 ;
        $negResult = true;
    }

    // if num1 is greater than equal to num2
    // subtract num2 from num1 and increase
    // quotient by one.
    $quotient = 0;
    while ($num1 >= $num2)
    {
        $num1 = $num1 - $num2 ;
        $quotient++ ;
    }

    // checking if neg equals to 1 then making
    // quotient negative
    if ($negResult)
            $quotient = - $quotient ;
    return $quotient ;
}

// Driver program
$num1 = 13; $num2 = 2 ;
echo division($num1, $num2) ;

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to divide a number by other
// without using / operator

    // Function to find division without using
    // '/' operator
    function division( num1, num2)
    {
        if (num1 == 0)
            return 0;
        if (num2 == 0)
            return Number.MAX_VALUE;;
        let negResult = false;

        // Handling negative numbers
        if (num1 < 0)
        {
            num1 = -num1;
            if (num2 < 0)
                num2 = -num2;
            else
                negResult = true;
        }
        else if (num2 < 0)
        {
            num2 = -num2;
            negResult = true;
        }

        // if num1 is greater than equal to num2
        // subtract num2 from num1 and increase
        // quotient by one.
        let quotient = 0;
        while (num1 >= num2)
        {
            num1 = num1 - num2;
            quotient++;
        }

        // checking if neg equals to 1 then making
        // quotient negative
        if (negResult)
            quotient = -quotient;
        return quotient;
    }

    // Driver program    
    let num1 = 13, num2 = 2;
    document.write(division(num1, num2));

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
6
```