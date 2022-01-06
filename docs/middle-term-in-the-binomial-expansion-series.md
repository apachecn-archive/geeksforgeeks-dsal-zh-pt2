# 二项式展开式系列的中间项

> 原文:[https://www . geesforgeks . org/二项式展开式中期系列/](https://www.geeksforgeeks.org/middle-term-in-the-binomial-expansion-series/)

给定三个整数 A、X 和 n，任务是找到二项式展开式级数的中间项。
示例:

```
Input : A = 1, X = 1, n = 6
Output : MiddleTerm = 20

Input : A = 2, X = 4, n = 7
Output : MiddleTerm1 = 35840, MiddleTerm2 = 71680
```

**接近**T2】

> **(A + X) <sup>n</sup>=<sup>n</sup>C<sub>0</sub>A<sup>n</sup>X<sup>0</sup>+<sup>n</sup>C<sub>1</sub>A<sup>n-1</sup>X<sup>1</sup>+<sup>n</sup>C<sub>2</sub>A<sup>n-2</sup>X<sup>2</sup>+ X <sup>n</sup>**
> 二项式展开式中的总项数为(A + X) <sup>n</sup> 为(n + 1)。
> 二项式展开式中的通称由下式给出:
> T49】T<sub>r+1</sub>=<sup>n</sup>C<sub>r</sub>A<sup>n-r</sup>X<sup>r</sup>T60
> T62】如果 n 为偶数:T64】设 m 为二项式展开式级数的中间项，则
> n = 2m【T62 这个中间项是(m + 1) <sup>第</sup>项。
> 因此，中项
> **T<sub>m+1</sub>=<sup>n</sup>C<sub>m</sub>A<sup>n-m</sup>X<sup>m</sup>**
> **如果 n 是奇数:**
> 设 m 为二项式展开式级数的中项，那么
> 设 n = 2m+1
> 这些中间项将是(m + 1) <sup>第</sup>和(m + 2) <sup>第</sup>项。
> 因此，中间术语为:
> **T<sub>m+1</sub>=<sup>n</sup>C<sub>(n-1)/2</sub>A<sup>(n+1)/2</sup>X<sup>(n-1)/2</sup>**T
> T<sub>m+2</sub>=<sup>n</sup>

## C++

```
// C++ program to find the middle term
// in binomial expansion series.
#include <bits/stdc++.h>
using namespace std;

// function to calculate
// factorial of a number
int factorial(int n)
{ 
    int fact = 1;
    for (int i = 1; i <= n; i++)
        fact *= i;

    return fact;
}

// Function to find middle term in
// binomial expansion series.
void findMiddleTerm(int A, int X, int n)
{
    int i, j, aPow, xPow;
    float middleTerm1, middleTerm2;

    if (n % 2 == 0)
    {
        // If n is even

        // calculating the middle term
        i = n / 2;

        // calculating the value of A to
        // the power k and X to the power k
        aPow = (int)pow(A, n - i);
        xPow = (int)pow(X, i);

        middleTerm1 = ((float)factorial(n) /
          (factorial(n - i) * factorial(i)))
                              * aPow * xPow;

        cout << "MiddleTerm = "
             << middleTerm1 << endl;
    }
    else {

        // If n is odd

        // calculating the middle term
        i = (n - 1) / 2;
        j = (n + 1) / 2;

        // calculating the value of A to the
        // power k and X to the power k
        aPow = (int)pow(A, n - i);
        xPow = (int)pow(X, i);

        middleTerm1 = ((float)factorial(n) /
           (factorial(n - i) * factorial(i)))
                               * aPow * xPow;

        // calculating the value of A to the
        // power k and X to the power k
        aPow = (int)pow(A, n - j);
        xPow = (int)pow(X, j);

        middleTerm2 = ((float)factorial(n) /
           (factorial(n - j) * factorial(j)))
                               * aPow * xPow;

        cout << "MiddleTerm1 = "
                      << middleTerm1 << endl;

        cout << "MiddleTerm2 = "
                      << middleTerm2 << endl;
    }
}

// Driver code
int main()
{
    int n = 5, A = 2, X = 3;

    // function call
    findMiddleTerm(A, X, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the middle term
// in binomial expansion series.
import java.math.*;

class GFG {

    // function to calculate factorial
    // of a number
    static int factorial(int n)
    {
        int fact = 1, i;
        if (n == 0)
            return 1;
        for (i = 1; i <= n; i++)
            fact *= i;

        return fact;
    }

    // Function to find middle term in
    // binomial expansion series.
    static void findmiddle(int A, int X, int n)
    {
        int i, j, aPow, xPow;
        float middleTerm1, middleTerm2;

        if (n % 2 == 0)
        {
            // If n is even

            // calculating the middle term
            i = n / 2;

            // calculating the value of A to
            // the power k and X to the power k
            aPow = (int)Math.pow(A, n - i);
            xPow = (int)Math.pow(X, i);

            middleTerm1 = ((float)factorial(n) /
              (factorial(n - i) * factorial(i)))
                                  * aPow * xPow;
            System.out.println("MiddleTerm = "
                                 + middleTerm1);
        }
        else {

            // If n is odd

            // calculating the middle term
            i = (n - 1) / 2;
            j = (n + 1) / 2;

            // calculating the value of A to the
            // power k and X to the power k
            aPow = (int)Math.pow(A, n - i);
            xPow = (int)Math.pow(X, i);

            middleTerm1 = ((float)factorial(n) /
               (factorial(n - i) * factorial(i)))
                                   * aPow * xPow;

            // calculating the value of A to the
            // power k and X to the power k
            aPow = (int)Math.pow(A, n - j);
            xPow = (int)Math.pow(X, j);

            middleTerm2 = ((float)factorial(n) /
               (factorial(n - j) * factorial(j)))
                                   * aPow * xPow;

            System.out.println("MiddleTerm1 = "
                                  + middleTerm1);

            System.out.println("MiddleTerm2 = "
                                  + middleTerm2);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 6, A = 2, X = 4;

        // calling the function
        findmiddle(A, X, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the middle term
# in binomial expansion series.
import math

# function to calculate
# factorial of a number
def factorial(n) :

    fact = 1
    for i in range(1, n+1) :
        fact = fact * i

    return fact;

# Function to find middle term in
# binomial expansion series.
def findMiddleTerm(A, X, n) :

    if (n % 2 == 0) :

        # If n is even

        # calculating the middle term
        i = int(n / 2)

        # calculating the value of A to
        # the power k and X to the power k
        aPow = int(math.pow(A, n - i))
        xPow = int(math.pow(X, i))

        middleTerm1 = ((math.factorial(n) /
                       (math.factorial(n - i)
                       * math.factorial(i)))
                       * aPow * xPow)

        print ("MiddleTerm = {}" .
                     format(middleTerm1))

    else :

        # If n is odd

        # calculating the middle term
        i = int((n - 1) / 2)
        j = int((n + 1) / 2)

        # calculating the value of A to the
        # power k and X to the power k
        aPow = int(math.pow(A, n - i))
        xPow = int(math.pow(X, i))

        middleTerm1 = ((math.factorial(n)
                    / (math.factorial(n - i)
                    * math.factorial(i)))
                        * aPow * xPow)

        # calculating the value of A to the
        # power k and X to the power k
        aPow = int(math.pow(A, n - j))
        xPow = int(math.pow(X, j))

        middleTerm2 = ((math.factorial(n)
                   / (math.factorial(n - j)
                   * math.factorial(j)))
                      * aPow * xPow)

        print ("MiddleTerm1 = {}" .
               format(int(middleTerm1)))

        print ("MiddleTerm2 = {}" .
               format(int(middleTerm2)))

# Driver code
n = 5
A = 2
X = 3

# function call
findMiddleTerm(A, X, n)

# This code is contributed by
# manishshaw1.
```

## C#

```
// C# program to find the middle term
// in binomial expansion series.
using System;

class GFG {

    // function to calculate factorial
    // of a number
    static int factorial(int n)
    {
        int fact = 1, i;
        if (n == 0)
            return 1;
        for (i = 1; i <= n; i++)
            fact *= i;

        return fact;
    }

    // Function to find middle term in
    // binomial expansion series.
    static void findmiddle(int A, int X, int n)
    {
        int i, j, aPow, xPow;
        float middleTerm1, middleTerm2;

        if (n % 2 == 0)
        {
            // If n is even

            // calculating the middle term
            i = n / 2;

            // calculating the value of A to
            // the power k and X to the power k
            aPow = (int)Math.Pow(A, n - i);
            xPow = (int)Math.Pow(X, i);

            middleTerm1 = ((float)factorial(n) /
            (factorial(n - i) * factorial(i)))
                                * aPow * xPow;
            Console.WriteLine("MiddleTerm = "
                                + middleTerm1);
        }
        else {

            // If n is odd

            // calculating the middle term
            i = (n - 1) / 2;
            j = (n + 1) / 2;

            // calculating the value of A to the
            // power k and X to the power k
            aPow = (int)Math.Pow(A, n - i);
            xPow = (int)Math.Pow(X, i);

            middleTerm1 = ((float)factorial(n) /
            (factorial(n - i) * factorial(i)))
                                * aPow * xPow;

            // calculating the value of A to the
            // power k and X to the power k
            aPow = (int)Math.Pow(A, n - j);
            xPow = (int)Math.Pow(X, j);

            middleTerm2 = ((float)factorial(n) /
            (factorial(n - j) * factorial(j)))
                                * aPow * xPow;

            Console.WriteLine("MiddleTerm1 = "
                                + middleTerm1);

            Console.WriteLine("MiddleTerm2 = "
                                + middleTerm2);
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 5, A = 2, X = 3;

        // calling the function
        findmiddle(A, X, n);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the middle term
// in binomial expansion series.

// function to calculate
// factorial of a number
function factorial(int $n)
{
    $fact = 1;
    for($i = 1; $i <= $n; $i++)
        $fact *= $i;

    return $fact;
}

// Function to find middle term in
// binomial expansion series.
function findMiddleTerm($A, $X, $n)
{
    $i; $j;
    $aPow; $xPow;
    $middleTerm1;
    $middleTerm2;

    if ($n % 2 == 0)
    {

        // If n is even
        // calculating the middle term
        $i = $n / 2;

        // calculating the value of A to
        // the power k and X to the power k
        $aPow = pow($A, $n - i);
        $xPow = pow($X, $i);

        $middleTerm1 = $factorial($n) /
        (factorial($n - $i) * factorial($i))
                            * $aPow * $xPow;

        echo "MiddleTerm = ","\n",
            $middleTerm1 ;
    }
    else
    {

        // If n is odd

        // calculating the middle term
        $i = ($n - 1) / 2;
        $j = ($n + 1) / 2;

        // calculating the value of A to the
        // power k and X to the power k
        $aPow = pow($A, $n - $i);
        $xPow = pow($X, $i);

        $middleTerm1 = ((float)factorial($n) /
        (factorial($n - $i) * factorial($i)))
                            * $aPow * $xPow;

        // calculating the value of A to the
        // power k and X to the power k
        $aPow = pow($A, $n - $j);
        $xPow = pow($X, $j);

        $middleTerm2 = factorial($n) /
        (factorial($n - $j) * factorial($j))
                            * $aPow * $xPow;

        echo "MiddleTerm1 = "
                    , $middleTerm1,"\n" ;

        echo "MiddleTerm2 = "
                    , $middleTerm2 ;
    }
}

    // Driver code
    $n = 5;
    $A = 2;
    $X = 3;

    // function call
    findMiddleTerm($A, $X, $n);

// This code is contributed by Vishal Tripathi.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the middle term
// in binomial expansion series.

// function to calculate
// factorial of a number
function factorial(n)
{
    let fact = 1;
    for (let i = 1; i <= n; i++)
        fact *= i;

    return fact;
}

// Function to find middle term in
// binomial expansion series.
function findMiddleTerm(A, X, n)
{
    let i, j, aPow, xPow;
    let middleTerm1, middleTerm2;

    if (n % 2 == 0)
    {
        // If n is even

        // calculating the middle term
        i = Math.floor(n / 2);

        // calculating the value of A to
        // the power k and X to the power k
        aPow = Math.floor(Math.pow(A, n - i));
        xPow = Math.floor(Math.pow(X, i));

        middleTerm1 = Math.floor(factorial(n) /
        (factorial(n - i) * factorial(i)))
                            * aPow * xPow;

        document.write("MiddleTerm = "
            + middleTerm1 + "<br>");
    }
    else {

        // If n is odd

        // calculating the middle term
        i = Math.floor((n - 1) / 2);
        j = Math.floor((n + 1) / 2);

        // calculating the value of A to the
        // power k and X to the power k
        aPow = Math.floor(Math.pow(A, n - i));
        xPow = Math.floor(Math.pow(X, i));

        middleTerm1 = Math.floor(factorial(n) /
        (factorial(n - i) * factorial(i)))
                            * aPow * xPow;

        // calculating the value of A to the
        // power k and X to the power k
        aPow = Math.floor(Math.pow(A, n - j));
        xPow = Math.floor(Math.pow(X, j));

        middleTerm2 = Math.floor(factorial(n) /
        (factorial(n - j) * factorial(j)))
                            * aPow * xPow;

        document.write("MiddleTerm1 = "
                    + middleTerm1 + "<br>");

        document.write("MiddleTerm2 = "
                    + middleTerm2 + "<br>");
    }
}

// Driver code

    let n = 5, A = 2, X = 3;

    // function call
    findMiddleTerm(A, X, n);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
MiddleTerm1 = 720
MiddleTerm2 = 1080
```