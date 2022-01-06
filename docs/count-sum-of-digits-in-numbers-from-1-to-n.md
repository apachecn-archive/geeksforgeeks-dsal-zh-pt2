# 计算从 1 到 n 的所有数字的数字总和

> 原文:[https://www . geesforgeks . org/count-numbers-in-from-1-n/](https://www.geeksforgeeks.org/count-sum-of-digits-in-numbers-from-1-to-n/)

给定一个数字 n，求从 1 到 n 的所有数字的总和。
**例:**

```
Input: n = 5
Output: Sum of digits in numbers from 1 to 5 = 15

Input: n = 12
Output: Sum of digits in numbers from 1 to 12 = 51

Input: n = 328
Output: Sum of digits in numbers from 1 to 328 = 3241
```

**天真解:**
天真解是遍历从 1 到 n 的每个数字 x，通过遍历 x 的所有数字来计算 x 中的和，下面是这个想法的实现。

## C++

```
// A Simple C++ program to compute sum of digits in numbers from 1 to n
#include<bits/stdc++.h>
using namespace std;

int sumOfDigits(int );

// Returns sum of all digits in numbers from 1 to n
int sumOfDigitsFrom1ToN(int n)
{
    int result = 0; // initialize result

    // One by one compute sum of digits in every number from
    // 1 to n
    for (int x = 1; x <= n; x++)
        result += sumOfDigits(x);

    return result;
}

// A utility function to compute sum of digits in a
// given number x
int sumOfDigits(int x)
{
    int sum = 0;
    while (x != 0)
    {
        sum += x %10;
        x   = x /10;
    }
    return sum;
}

// Driver Program
int main()
{
    int n = 328;
    cout << "Sum of digits in numbers from 1 to " << n << " is "
         << sumOfDigitsFrom1ToN(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple JAVA program to compute sum of
// digits in numbers from 1 to n
import java.io.*;

class GFG {

    // Returns sum of all digits in numbers
    // from 1 to n
    static int sumOfDigitsFrom1ToN(int n)
    {
        int result = 0; // initialize result

        // One by one compute sum of digits
        // in every number from 1 to n
        for (int x = 1; x <= n; x++)
            result += sumOfDigits(x);

        return result;
    }

    // A utility function to compute sum
    // of digits in a given number x
    static int sumOfDigits(int x)
    {
        int sum = 0;
        while (x != 0)
        {
            sum += x % 10;
            x   = x / 10;
        }
        return sum;
    }

    // Driver Program
    public static void main(String args[])
    {
        int n = 328;
        System.out.println("Sum of digits in numbers"
                          +" from 1 to " + n + " is "
                          + sumOfDigitsFrom1ToN(n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# A Simple Python program to compute sum
# of digits in numbers from 1 to n

# Returns sum of all digits in numbers
# from 1 to n
def sumOfDigitsFrom1ToN(n) :

    result = 0   # initialize result

    # One by one compute sum of digits
    # in every number from 1 to n
    for x in range(1, n+1) :
        result = result + sumOfDigits(x)

    return result

# A utility function to compute sum of
# digits in a given number x
def sumOfDigits(x) :
    sum = 0
    while (x != 0) :
        sum = sum + x % 10
        x   = x // 10

    return sum

# Driver Program
n = 328
print("Sum of digits in numbers from 1 to", n, "is", sumOfDigitsFrom1ToN(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A Simple C# program to compute sum of
// digits in numbers from 1 to n

using System;

public class GFG {

    // Returns sum of all digits in numbers
    // from 1 to n
    static int sumOfDigitsFrom1ToN(int n)
    {

        // initialize result
        int result = 0;

        // One by one compute sum of digits
        // in every number from 1 to n
        for (int x = 1; x <= n; x++)
            result += sumOfDigits(x);

        return result;
    }

    // A utility function to compute sum
    // of digits in a given number x
    static int sumOfDigits(int x)
    {
        int sum = 0;

        while (x != 0)
        {
            sum += x % 10;
            x = x / 10;
        }

        return sum;
    }

    // Driver Program
    public static void Main()
    {
        int n = 328;

        Console.WriteLine("Sum of digits"
               + " in numbers from 1 to "
                             + n + " is "
                + sumOfDigitsFrom1ToN(n));
    }
}

// This code is contributed by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// A Simple php program to compute sum
//of digits in numbers from 1 to n

// Returns sum of all digits in
// numbers from 1 to n
function sumOfDigitsFrom1ToN($n)
{
    $result = 0; // initialize result

    // One by one compute sum of digits
    // in every number from 1 to n
    for ($x = 1; $x <= $n; $x++)
        $result += sumOfDigits($x);

    return $result;
}

// A utility function to compute sum
// of digits in a given number x
function sumOfDigits($x)
{
    $sum = 0;
    while ($x != 0)
    {
        $sum += $x %10;
        $x = $x /10;
    }
    return $sum;
}

// Driver Program

    $n = 328;
    echo "Sum of digits in numbers from"
               . " 1 to " . $n . " is "
               . sumOfDigitsFrom1ToN($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // A Simple Javascript program to compute sum of
    // digits in numbers from 1 to n

    // Returns sum of all digits in numbers
    // from 1 to n
    function sumOfDigitsFrom1ToN(n)
    {

        // initialize result
        let result = 0;

        // One by one compute sum of digits
        // in every number from 1 to n
        for (let x = 1; x <= n; x++)
            result += sumOfDigits(x);

        return result;
    }

    // A utility function to compute sum
    // of digits in a given number x
    function sumOfDigits(x)
    {
        let sum = 0;

        while (x != 0)
        {
            sum += x % 10;
            x = parseInt(x / 10, 10);
        }

        return sum;
    }

    let n = 328;

    document.write("Sum of digits"
                      + " in numbers from 1 to "
                      + n + " is "
                      + sumOfDigitsFrom1ToN(n));

    // This code is contributed by divyeshrabadiya07.                 
</script>
```

**输出:**

```
Sum of digits in numbers from 1 to 328 is 3241
```

**高效解决方案:**
以上是一个幼稚的解决方案。通过找到一种模式，我们可以更有效地做到这一点。
我们举几个例子。

```
sum(9) = 1 + 2 + 3 + 4 ........... + 9
       = 9*10/2 
       = 45

sum(99)  = 45 + (10 + 45) + (20 + 45) + ..... (90 + 45)
         = 45*10 + (10 + 20 + 30 ... 90)
         = 45*10 + 10(1 + 2 + ... 9)
         = 45*10 + 45*10
         = sum(9)*10 + 45*10 

sum(999) = sum(99)*10 + 45*100
```

一般来说，我们可以用下面的公式计算总和(10<sup>d</sup>–1)

```
   sum(10d - 1) = sum(10d-1 - 1) * 10 + 45*(10d-1) 
```

在下面的实现中，上面的公式是使用[动态编程](https://www.geeksforgeeks.org/tag/dynamic-programming/)实现的，因为有重叠的子问题。
上述公式是这个想法的一个核心步骤。下面是完整的算法

**算法:和(n)**

```
1) Find number of digits minus one in n. Let this value be 'd'.  
   For 328, d is 2.

2) Compute some of digits in numbers from 1 to 10d - 1\.  
   Let this sum be w. For 328, we compute sum of digits from 1 to 
   99 using above formula.

3) Find Most significant digit (msd) in n. For 328, msd is 3.

4) Overall sum is sum of following terms

    a) Sum of digits in 1 to "msd * 10d - 1".  For 328, sum of 
       digits in numbers from 1 to 299.
        For 328, we compute 3*sum(99) + (1 + 2)*100\.  Note that sum of
        sum(299) is sum(99) + sum of digits from 100 to 199 + sum of digits
        from 200 to 299\.  
        Sum of 100 to 199 is sum(99) + 1*100 and sum of 299 is sum(99) + 2*100.
        In general, this sum can be computed as w*msd + (msd*(msd-1)/2)*10d

    b) Sum of digits in msd * 10d to n.  For 328, sum of digits in 
       300 to 328.
        For 328, this sum is computed as 3*29 + recursive call "sum(28)"
        In general, this sum can be computed as  msd * (n % (msd*10d) + 1) 
        + sum(n % (10d))
```

下面是上述算法的实现。

## C++

```
// C++ program to compute sum of digits in numbers from 1 to n
#include<bits/stdc++.h>
using namespace std;

// Function to computer sum of digits in numbers from 1 to n
// Comments use example of 328 to explain the code
int sumOfDigitsFrom1ToN(int n)
{
    // base case: if n<10 return sum of
    // first n natural numbers
    if (n<10)
      return n*(n+1)/2;

    // d = number of digits minus one in n. For 328, d is 2
    int d = log10(n);

    // computing sum of digits from 1 to 10^d-1,
    // d=1 a[0]=0;
    // d=2 a[1]=sum of digit from 1 to 9 = 45
    // d=3 a[2]=sum of digit from 1 to 99 = a[1]*10 + 45*10^1 = 900
    // d=4 a[3]=sum of digit from 1 to 999 = a[2]*10 + 45*10^2 = 13500
    int *a = new int[d+1];
    a[0] = 0, a[1] = 45;
    for (int i=2; i<=d; i++)
        a[i] = a[i-1]*10 + 45*ceil(pow(10,i-1));

    // computing 10^d
    int p = ceil(pow(10, d));

    // Most significant digit (msd) of n,
    // For 328, msd is 3 which can be obtained using 328/100
    int msd = n/p;

    // EXPLANATION FOR FIRST and SECOND TERMS IN BELOW LINE OF CODE
    // First two terms compute sum of digits from 1 to 299
    // (sum of digits in range 1-99 stored in a[d]) +
    // (sum of digits in range 100-199, can be calculated as 1*100 + a[d]
    // (sum of digits in range 200-299, can be calculated as 2*100 + a[d]
    //  The above sum can be written as 3*a[d] + (1+2)*100

    // EXPLANATION FOR THIRD AND FOURTH TERMS IN BELOW LINE OF CODE
    // The last two terms compute sum of digits in number from 300 to 328
    // The third term adds 3*29 to sum as digit 3 occurs in all numbers
    //                from 300 to 328
    // The fourth term recursively calls for 28
    return msd*a[d] + (msd*(msd-1)/2)*p + 
           msd*(1+n%p) + sumOfDigitsFrom1ToN(n%p);
}

// Driver Program
int main()
{
    int n = 328;
    cout << "Sum of digits in numbers from 1 to " << n << " is "
         << sumOfDigitsFrom1ToN(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to compute sum of digits
// in numbers from 1 to n
import java.io.*;
import java.math.*;

class GFG{

    // Function to computer sum of digits in
    // numbers from 1 to n. Comments use
    // example of 328 to explain the code
    static int sumOfDigitsFrom1ToN(int n)
    {
        // base case: if n<10 return sum of
        // first n natural numbers
        if (n < 10)
          return (n * (n + 1) / 2);

        // d = number of digits minus one in
        // n. For 328, d is 2
        int d = (int)(Math.log10(n));

        // computing sum of digits from 1 to 10^d-1,
        // d=1 a[0]=0;
        // d=2 a[1]=sum of digit from 1 to 9 = 45
        // d=3 a[2]=sum of digit from 1 to 99 =
        // a[1]*10 + 45*10^1 = 900
        // d=4 a[3]=sum of digit from 1 to 999 =
        // a[2]*10 + 45*10^2 = 13500
        int a[] = new int[d+1];
        a[0] = 0; a[1] = 45;
        for (int i = 2; i <= d; i++)
            a[i] = a[i-1] * 10 + 45 *
                 (int)(Math.ceil(Math.pow(10, i-1)));

        // computing 10^d
        int p = (int)(Math.ceil(Math.pow(10, d)));

        // Most significant digit (msd) of n,
        // For 328, msd is 3 which can be obtained
        // using 328/100
        int msd = n / p;

        // EXPLANATION FOR FIRST and SECOND TERMS IN
        // BELOW LINE OF CODE
        // First two terms compute sum of digits from
        // 1 to 299
        // (sum of digits in range 1-99 stored in a[d]) +
        // (sum of digits in range 100-199, can be
        // calculated as 1*100 + a[d]
        // (sum of digits in range 200-299, can be
        // calculated as 2*100 + a[d]
        //  The above sum can be written as 3*a[d] +
        // (1+2)*100

        // EXPLANATION FOR THIRD AND FOURTH TERMS IN
        // BELOW LINE OF CODE
        // The last two terms compute sum of digits in
        // number from 300 to 328\. The third term adds
        // 3*29 to sum as digit 3 occurs in all numbers
        // from 300 to 328\. The fourth term recursively
        // calls for 28
        return (msd * a[d] + (msd * (msd - 1) / 2) * p + 
              msd * (1 + n % p) + sumOfDigitsFrom1ToN(n % p));
    }

    // Driver Program
    public static void main(String args[])
    {
        int n = 328;
        System.out.println("Sum of digits in numbers " +
                          "from 1 to " +n + " is " +
                          sumOfDigitsFrom1ToN(n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# PYTHON 3 program to compute sum of digits
# in numbers from 1 to n
import math

# Function to computer sum of digits in
# numbers from 1 to n. Comments use example
# of 328 to explain the code
def sumOfDigitsFrom1ToN( n) :

    # base case: if n<10 return sum of
    # first n natural numbers
    if (n<10) :
        return (n*(n+1)/2)

    # d = number of digits minus one in n.
    # For 328, d is 2
    d = (int)(math.log10(n))

    """computing sum of digits from 1 to 10^d-1,
    d=1 a[0]=0;
    d=2 a[1]=sum of digit from 1 to 9 = 45
    d=3 a[2]=sum of digit from 1 to 99 = a[1]*10
    + 45*10^1 = 900
    d=4 a[3]=sum of digit from 1 to 999 = a[2]*10
    + 45*10^2 = 13500"""
    a = [0] * (d + 1)
    a[0] = 0
    a[1] = 45
    for i in range(2, d+1) :
        a[i] = a[i-1] * 10 + 45 * (int)(math.ceil(math.pow(10,i-1)))

    # computing 10^d
    p = (int)(math.ceil(math.pow(10, d)))

    # Most significant digit (msd) of n,
    # For 328, msd is 3 which can be obtained
    # using 328/100
    msd = n//p

    """EXPLANATION FOR FIRST and SECOND TERMS IN
    BELOW LINE OF CODE
    First two terms compute sum of digits from 1 to 299
    (sum of digits in range 1-99 stored in a[d]) +
    (sum of digits in range 100-199, can be calculated
    as 1*100 + a[d]. (sum of digits in range 200-299,
    can be calculated as 2*100 + a[d]
    The above sum can be written as 3*a[d] + (1+2)*100

    EXPLANATION FOR THIRD AND FOURTH TERMS IN BELOW
    LINE OF CODE
    The last two terms compute sum of digits in number
    from 300 to 328\. The third term adds 3*29 to sum
    as digit 3 occurs in all numbers from 300 to 328.
    The fourth term recursively calls for 28"""
    return (int)(msd * a[d] + (msd*(msd-1) // 2) * p + 
           msd * (1 + n % p) + sumOfDigitsFrom1ToN(n % p))

# Driver Program
n = 328
print("Sum of digits in numbers from 1 to",
      n ,"is",sumOfDigitsFrom1ToN(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to compute sum of digits
// in numbers from 1 to n

using System;

public class GFG {

    // Function to computer sum of digits in
    // numbers from 1 to n. Comments use
    // example of 328 to explain the code
    static int sumOfDigitsFrom1ToN(int n)
    {

        // base case: if n<10 return sum of
        // first n natural numbers
        if (n < 10)
            return (n * (n + 1) / 2);

        // d = number of digits minus one in
        // n. For 328, d is 2
        int d = (int)(Math.Log(n) / Math.Log(10));

        // computing sum of digits from 1 to 10^d-1,
        // d=1 a[0]=0;
        // d=2 a[1]=sum of digit from 1 to 9 = 45
        // d=3 a[2]=sum of digit from 1 to 99 =
        // a[1]*10 + 45*10^1 = 900
        // d=4 a[3]=sum of digit from 1 to 999 =
        // a[2]*10 + 45*10^2 = 13500
        int[] a = new int[d+1];
        a[0] = 0; a[1] = 45;

        for (int i = 2; i <= d; i++)
            a[i] = a[i-1] * 10 + 45 *
                (int)(Math.Ceiling(Math.Pow(10, i-1)));

        // computing 10^d
        int p = (int)(Math.Ceiling(Math.Pow(10, d)));

        // Most significant digit (msd) of n,
        // For 328, msd is 3 which can be obtained
        // using 328/100
        int msd = n / p;

        // EXPLANATION FOR FIRST and SECOND TERMS IN
        // BELOW LINE OF CODE
        // First two terms compute sum of digits from
        // 1 to 299
        // (sum of digits in range 1-99 stored in a[d]) +
        // (sum of digits in range 100-199, can be
        // calculated as 1*100 + a[d]
        // (sum of digits in range 200-299, can be
        // calculated as 2*100 + a[d]
        // The above sum can be written as 3*a[d] +
        // (1+2)*100

        // EXPLANATION FOR THIRD AND FOURTH TERMS IN
        // BELOW LINE OF CODE
        // The last two terms compute sum of digits in
        // number from 300 to 328\. The third term adds
        // 3*29 to sum as digit 3 occurs in all numbers
        // from 300 to 328\. The fourth term recursively
        // calls for 28
        return (msd * a[d] + (msd * (msd - 1) / 2) * p +
            msd * (1 + n % p) + sumOfDigitsFrom1ToN(n % p));
    }

    // Driver Program
    public static void Main()
    {
        int n = 328;
        Console.WriteLine("Sum of digits in numbers " +
                             "from 1 to " +n + " is " +
                               sumOfDigitsFrom1ToN(n));
    }
}

// This code is contributed by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compute sum of digits
// in numbers from 1 to n

// Function to computer sum of digits in
// numbers from 1 to n. Comments use
// example of 328 to explain the code
function sumOfDigitsFrom1ToN($n)
{
    // base case: if n<10 return sum of
    // first n natural numbers
    if ($n < 10)
    return ($n * ($n + 1) / 2);

    // d = number of digits minus one in
    // n. For 328, d is 2
    $d = (int)(log10($n));

    // computing sum of digits from 1
    // to 10^d-1, d=1 a[0]=0;
    // d=2 a[1]=sum of digit from 1 to 9 = 45
    // d=3 a[2]=sum of digit from 1 to 99 =
    // a[1]*10 + 45*10^1 = 900
    // d=4 a[3]=sum of digit from 1 to 999 =
    // a[2]*10 + 45*10^2 = 13500
    $a[$d + 1] = array();
    $a[0] = 0;
    $a[1] = 45;
    for ($i = 2; $i <= $d; $i++)
        $a[$i] = $a[$i - 1] * 10 + 45 *
                 (int)(ceil(pow(10, $i - 1)));

    // computing 10^d
    $p = (int)(ceil(pow(10, $d)));

    // Most significant digit (msd) of n,
    // For 328, msd is 3 which can be obtained
    // using 328/100
    $msd = (int)($n / $p);

    // EXPLANATION FOR FIRST and SECOND
    // TERMS IN BELOW LINE OF CODE
    // First two terms compute sum of
    // digits from 1 to 299
    // (sum of digits in range 1-99 stored
    // in a[d]) + (sum of digits in range
    // 100-199, can be calculated as 1*100 + a[d]
    // (sum of digits in range 200-299,
    // can be calculated as 2*100 + a[d]
    // The above sum can be written as
    // 3*a[d] + (1+2)*100

    // EXPLANATION FOR THIRD AND FOURTH
    // TERMS IN BELOW LINE OF CODE
    // The last two terms compute sum of digits in
    // number from 300 to 328\. The third term adds
    // 3*29 to sum as digit 3 occurs in all numbers
    // from 300 to 328\. The fourth term recursively
    // calls for 28
    return ($msd * $a[$d] + ($msd * (int)($msd - 1) / 2) * $p +
            $msd * (1 + $n % $p) + sumOfDigitsFrom1ToN($n % $p));
}

// Driver Code
$n = 328;
echo ("Sum of digits in numbers " ),
      "from 1 to " , $n , " is ",
       sumOfDigitsFrom1ToN($n);

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>

    // Javascript program to compute sum of digits
    // in numbers from 1 to n

    // Function to computer sum of digits in
    // numbers from 1 to n. Comments use
    // example of 328 to explain the code
    function sumOfDigitsFrom1ToN(n)
    {

        // base case: if n<10 return sum of
        // first n natural numbers
        if (n < 10)
            return (n * (n + 1) / 2);

        // d = number of digits minus one in
        // n. For 328, d is 2
        let d = parseInt(Math.log(n) / Math.log(10), 10);

        // computing sum of digits from 1 to 10^d-1,
        // d=1 a[0]=0;
        // d=2 a[1]=sum of digit from 1 to 9 = 45
        // d=3 a[2]=sum of digit from 1 to 99 =
        // a[1]*10 + 45*10^1 = 900
        // d=4 a[3]=sum of digit from 1 to 999 =
        // a[2]*10 + 45*10^2 = 13500
        let a = new Array(d+1);
        a[0] = 0; a[1] = 45;

        for (let i = 2; i <= d; i++)
            a[i] = a[i-1] * 10 + 45 *
            parseInt(Math.ceil(Math.pow(10, i-1)), 10);

        // computing 10^d
        let p = parseInt(Math.ceil(Math.pow(10, d)), 10);

        // Most significant digit (msd) of n,
        // For 328, msd is 3 which can be obtained
        // using 328/100
        let msd = parseInt(n / p, 10);

        // EXPLANATION FOR FIRST and SECOND TERMS IN
        // BELOW LINE OF CODE
        // First two terms compute sum of digits from
        // 1 to 299
        // (sum of digits in range 1-99 stored in a[d]) +
        // (sum of digits in range 100-199, can be
        // calculated as 1*100 + a[d]
        // (sum of digits in range 200-299, can be
        // calculated as 2*100 + a[d]
        // The above sum can be written as 3*a[d] +
        // (1+2)*100

        // EXPLANATION FOR THIRD AND FOURTH TERMS IN
        // BELOW LINE OF CODE
        // The last two terms compute sum of digits in
        // number from 300 to 328\. The third term adds
        // 3*29 to sum as digit 3 occurs in all numbers
        // from 300 to 328\. The fourth term recursively
        // calls for 28
        return (msd * a[d] + (msd * (msd - 1) / 2) * p +
            msd * (1 + n % p) + sumOfDigitsFrom1ToN(n % p));
    }

    let n = 328;
    document.write("Sum of digits in numbers from 1 to " + n +
                     " is " + sumOfDigitsFrom1ToN(n));

</script>
```

**输出:**

```
Sum of digits in numbers from 1 to 328 is 3241
```

高效的算法还有一个优点，即使给我们多个输入，我们也只需要计算数组‘a[]’一次。

**改进:**
上述实现需要 O(d <sup>2</sup> )时间，因为每次递归调用都会再次计算 dp[]数组。第一次调用取 0(d)，第二次调用取 0(d-1)，第三次调用取 0(d-2)，依此类推。我们不需要在每次递归调用中重新计算 dp[]数组。下面是在运行时间内工作的修改后的实现。其中 **d** 是输入数字的位数。

## C++

```
// C++ program to compute sum of digits
// in numbers from 1 to n
#include<bits/stdc++.h>
using namespace std;

int sumOfDigitsFrom1ToNUtil(int n, int a[])
{
    if (n < 10)
        return (n * (n + 1) / 2);

    int d = (int)(log10(n));
    int p = (int)(ceil(pow(10, d)));
    int msd = n / p;

    return (msd * a[d] + (msd * (msd - 1) / 2) * p +
            msd * (1 + n % p) +
            sumOfDigitsFrom1ToNUtil(n % p, a));
}

// Function to computer sum of digits in
// numbers from 1 to n
int sumOfDigitsFrom1ToN(int n)
{
    int d = (int)(log10(n));
    int a[d + 1];
    a[0] = 0; a[1] = 45;

    for(int i = 2; i <= d; i++)
        a[i] = a[i - 1] * 10 + 45 *
               (int)(ceil(pow(10, i - 1)));

    return sumOfDigitsFrom1ToNUtil(n, a);
}

// Driver code
int main()
{
    int n = 328;

    cout << "Sum of digits in numbers from 1 to "
         << n << " is "<< sumOfDigitsFrom1ToN(n);
}

// This code is contributed by ajaykr00kj
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to compute sum of digits
// in numbers from 1 to n
import java.io.*;
import java.math.*;

class GFG{

    // Function to computer sum of digits in
    // numbers from 1 to n
    static int sumOfDigitsFrom1ToN(int n)
    {
        int d = (int)(Math.log10(n));
        int a[] = new int[d+1];
        a[0] = 0; a[1] = 45;
        for (int i = 2; i <= d; i++)
            a[i] = a[i-1] * 10 + 45 *
                (int)(Math.ceil(Math.pow(10, i-1)));

        return sumOfDigitsFrom1ToNUtil(n, a);
    }

    static int sumOfDigitsFrom1ToNUtil(int n, int a[])
    {
        if (n < 10)
            return (n * (n + 1) / 2);

        int d = (int)(Math.log10(n));
        int p = (int)(Math.ceil(Math.pow(10, d)));
        int msd = n / p;
        return (msd * a[d] + (msd * (msd - 1) / 2) * p +
            msd * (1 + n % p) + sumOfDigitsFrom1ToNUtil(n % p, a));
    }

    // Driver Program
    public static void main(String args[])
    {
        int n = 328;
        System.out.println("Sum of digits in numbers " +
                        "from 1 to " +n + " is " +
                        sumOfDigitsFrom1ToN(n));
    }
}

/*This code is contributed by Narendra Jha.*/
```

## 蟒蛇 3

```
# Python program to compute sum of digits
# in numbers from 1 to n
import math

# Function to computer sum of digits in
# numbers from 1 to n
def sumOfDigitsFrom1ToN(n):

    d = int(math.log(n, 10))
    a = [0]*(d + 1)
    a[0] = 0
    a[1] = 45
    for i in range(2, d + 1):
        a[i] = a[i - 1] * 10 + 45 * \
                int(math.ceil(pow(10, i - 1)))

    return sumOfDigitsFrom1ToNUtil(n, a)

def sumOfDigitsFrom1ToNUtil(n, a):
    if (n < 10):
        return (n * (n + 1)) // 2

    d = int(math.log(n,10))
    p = int(math.ceil(pow(10, d)))
    msd = n // p
    return (msd * a[d] + (msd * (msd - 1) // 2) * p +
    msd * (1 + n % p) + sumOfDigitsFrom1ToNUtil(n % p, a))

# Driver code
n = 328
print("Sum of digits in numbers from 1 to",n,"is",sumOfDigitsFrom1ToN(n))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to compute sum of digits
// in numbers from 1 to n
using System;

class GFG
{

    // Function to computer sum of digits in
    // numbers from 1 to n
    static int sumOfDigitsFrom1ToN(int n)
    {
        int d = (int)(Math.Log10(n));
        int []a = new int[d+1];
        a[0] = 0; a[1] = 45;
        for (int i = 2; i <= d; i++)
            a[i] = a[i-1] * 10 + 45 *
                (int)(Math.Ceiling(Math.Pow(10, i-1)));

        return sumOfDigitsFrom1ToNUtil(n, a);
    }

    static int sumOfDigitsFrom1ToNUtil(int n, int []a)
    {
        if (n < 10)
            return (n * (n + 1) / 2);

        int d = (int)(Math.Log10(n));
        int p = (int)(Math.Ceiling(Math.Pow(10, d)));
        int msd = n / p;
        return (msd * a[d] + (msd * (msd - 1) / 2) * p +
            msd * (1 + n % p) + sumOfDigitsFrom1ToNUtil(n % p, a));
    }

    // Driver code
    public static void Main(String []args)
    {
        int n = 328;
        Console.WriteLine("Sum of digits in numbers " +
                        "from 1 to " +n + " is " +
                        sumOfDigitsFrom1ToN(n));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to compute sum of digits
// in numbers from 1 to n

// Function to computer sum of digits in
// numbers from 1 to n
function sumOfDigitsFrom1ToNUtil( n,a)
{
    if (n < 10)
        return (n * (n + 1) / 2);

    var d = (parseInt)(Math.log10(n));
    var p = (Math.ceil(Math.pow(10, d)));
    var msd =(parseInt) (n / p);

    return (msd * a[d] + (msd * (msd - 1) / 2) * p +
            msd * (1 + n % p) +
            sumOfDigitsFrom1ToNUtil(n % p, a));
}

// Function to computer sum of digits in
// numbers from 1 to n
function sumOfDigitsFrom1ToN( n)
{
    var d =(parseInt)(Math.log10(n));
   var a=new Array(d + 1).fill(0);
    a[0] = 0; a[1] = 45;

    for(var i = 2; i <= d; i++)
        a[i] = a[i - 1] * 10 + 45 *
               (parseInt)(Math.ceil(Math.pow(10, i - 1)));

    return sumOfDigitsFrom1ToNUtil(n, a);
}

var n = 328;

    document.write( "Sum of digits in numbers from 1 to "
         + n + " is "+ sumOfDigitsFrom1ToN(n))

</script>
```

**输出:**

```
Sum of digits in numbers from 1 to 328 is 3241
```

本文由 **Shubham Gupta** 计算。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息