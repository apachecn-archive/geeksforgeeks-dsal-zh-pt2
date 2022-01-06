# 亏数

> 原文:[https://www.geeksforgeeks.org/deficient-number/](https://www.geeksforgeeks.org/deficient-number/)

如果由*除数和(n)* 表示的数的所有除数之和小于数 n 的两倍，则称数 n 为亏数，这两个值之差称为**亏数**。
从数学上讲，如果低于条件成立，则称该数为亏数:

```
divisorsSum(n) < 2 * n
deficiency = (2 * n) - divisorsSum(n)
```

前几个亏数是:
1，2，3，4，5，7，8，9，10，11，13，14，15，16，17，19 …..
给定一个数 n，我们的任务是找出这个数是否是亏数。
**例:**

```
Input: 21
Output: YES
Divisors are 1, 3, 7 and 21\. Sum of divisors is 32.
This sum is less than 2*21 or 42.

Input: 12
Output: NO

Input: 17
Output: YES
```

一个**简单的解决方法**就是把所有的数字从 1 迭代到 n，检查这个数字是否除以 n，然后计算总和。检查这个总和是否小于 2 * n。
这种方法的时间复杂度:O ( n )
**优化解:**
如果我们仔细观察，n 的除数是成对出现的。例如，如果 n = 100，那么所有的除数对都是:(1，100)，(2，50)，(4，25)，(5，20)，(10，10)
利用这个事实，我们可以加快我们的程序。
在检查除数时，我们必须小心是否有两个相等的除数，如(10，10)的情况。在这种情况下，我们将只取其中的一个来计算总和。
优化方法的实施

## C++

```
// C++ program to implement an Optimized Solution
// to check Deficient Number
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of divisors
int divisorsSum(int n)
{
    int sum = 0; // Initialize sum of prime factors

    // Note that this loop runs till square root of n
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {
            // If divisors are equal, take only one
            // of them
            if (n / i == i) {
                sum = sum + i;
            }
            else // Otherwise take both
            {
                sum = sum + i;
                sum = sum + (n / i);
            }
        }
    }
    return sum;
}

// Function to check Deficient Number
bool isDeficient(int n)
{
    // Check if sum(n) < 2 * n
    return (divisorsSum(n) < (2 * n));
}

/* Driver program to test above function */
int main()
{
    isDeficient(12) ? cout << "YES\n" : cout << "NO\n";
    isDeficient(15) ? cout << "YES\n" : cout << "NO\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check Deficient Number

import java.io.*;

class GFG {
    // Function to calculate sum of divisors
    static int divisorsSum(int n)
    {
        int sum = 0; // Initialize sum of prime factors

        // Note that this loop runs till square root of n
        for (int i = 1; i <= (Math.sqrt(n)); i++) {
            if (n % i == 0) {
                // If divisors are equal, take only one
                // of them
                if (n / i == i) {
                    sum = sum + i;
                }
                else // Otherwise take both
                {
                    sum = sum + i;
                    sum = sum + (n / i);
                }
            }
        }

        return sum;
    }

    // Function to check Deficient Number
    static boolean isDeficient(int n)
    {
        // Check if sum(n) < 2 * n
        return (divisorsSum(n) < (2 * n));
    }

    /* Driver program to test above function */
    public static void main(String args[])
    {
        if (isDeficient(12))
            System.out.println("YES");
        else
            System.out.println("NO");

        if (isDeficient(15))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code is contributed by Nikita Tiwari
```

## 计算机编程语言

```
# Python program to implement an Optimized
# Solution to check Deficient Number
import math

# Function to calculate sum of divisors
def divisorsSum(n) :
    sum = 0  # Initialize sum of prime factors

    # Note that this loop runs till square
    # root of n
    i = 1
    while i<= math.sqrt(n) :
        if (n % i == 0) :

            # If divisors are equal, take only one
            # of them
            if (n / i == i) :
                sum = sum + i
            else : # Otherwise take both
                sum = sum + i;
                sum = sum + (n / i)
        i = i + 1
    return sum

# Function to check Deficient Number
def isDeficient(n) :

    # Check if sum(n) < 2 * n
    return (divisorsSum(n) < (2 * n))

# Driver program to test above function
if ( isDeficient(12) ):
    print "YES"
else :
    print "NO"
if ( isDeficient(15) ) :
    print "YES"
else :
    print "NO"

# This Code is contributed by Nikita Tiwari
```

## C#

```
// C# program to implement an Optimized Solution
// to check Deficient Number
using System;

class GFG {

    // Function to calculate sum of
    // divisors
    static int divisorsSum(int n)
    {
        // Initialize sum of prime factors
        int sum = 0;

        // Note that this loop runs till
        // square root of n
        for (int i = 1; i <= (Math.Sqrt(n)); i++) {
            if (n % i == 0) {

                // If divisors are equal,
                // take only one of them
                if (n / i == i) {
                    sum = sum + i;
                }
                else // Otherwise take both
                {
                    sum = sum + i;
                    sum = sum + (n / i);
                }
            }
        }

        return sum;
    }

    // Function to check Deficient Number
    static bool isDeficient(int n)
    {

        // Check if sum(n) < 2 * n
        return (divisorsSum(n) < (2 * n));
    }

    /* Driver program to test above function */
    public static void Main()
    {
        string var = isDeficient(12) ? "YES" : "NO";
        Console.WriteLine(var);

        string var1 = isDeficient(15) ? "YES" : "NO";
        Console.WriteLine(var1);
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// an Optimized Solution
// to check Deficient Number

// Function to calculate
// sum of divisors
function divisorsSum($n)
{
    // Initialize sum of
    // prime factors
    $sum = 0;

    // Note that this loop runs
    // till square root of n
    for ($i = 1; $i <= sqrt($n); $i++)
    {
        if ($n % $i==0)
        {
            // If divisors are equal,
            // take only one of them
            if ($n / $i == $i)
            {
                $sum = $sum + $i;
            }
            // Otherwise take both
            else
            {
                $sum = $sum + $i;
                $sum = $sum + ($n / $i);
            }
        }
    }
    return $sum;
}

// Function to check
// Deficient Number
function isDeficient($n)
{
    // Check if sum(n) < 2 * n
    return (divisorsSum($n) < (2 * $n));
}

// Driver Code
$ds = isDeficient(12) ?
              "YES\n" :
                "NO\n";
    echo($ds);
$ds = isDeficient(15) ?
              "YES\n" :
                "NO\n";
    echo($ds);

// This code is contributed by ajit;.
?>
```

## java 描述语言

```
<script>

// Javascript program to check Deficient Number

    // Function to calculate sum of divisors
    function divisorsSum(n)
    {
        let sum = 0; // Initialize sum of prime factors

        // Note that this loop runs till square root of n
        for (let i = 1; i <= (Math.sqrt(n)); i++)
        {
            if (n % i == 0)
            {

                // If divisors are equal, take only one
                // of them
                if (n / i == i) {
                    sum = sum + i;
                }
                else // Otherwise take both
                {
                    sum = sum + i;
                    sum = sum + (n / i);
                }
            }
        }

        return sum;
    }

    // Function to check Deficient Number
    function isDeficient(n)
    {

        // Check if sum(n) < 2 * n
        return (divisorsSum(n) < (2 * n));
    }

// Driver code to test above methods

        if (isDeficient(12))
            document.write("YES" + "<br/>");
        else
            document.write("NO" + "<br/>");

        if (isDeficient(15))
            document.write("YES" + "<br/>");
        else
           document.write("NO" + "<br/>");

 // This code is contributed by avijitmondal1998.
</script>
```

**输出:**

```
NO
YES
```

**时间复杂度:** O( sqrt( n ))
**辅助空间:** O( 1 )
**参考文献:**
[https://en.wikipedia.org/wiki/Deficient_number](https://en.wikipedia.org/wiki/Deficient_number)
本文由 [**Harsh Agarwal**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。