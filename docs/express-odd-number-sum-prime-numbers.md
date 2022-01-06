# 将奇数表示为素数之和

> 原文:[https://www . geesforgeks . org/express-奇数-和-质数/](https://www.geeksforgeeks.org/express-odd-number-sum-prime-numbers/)

给定一个奇数，我们需要将其表示为至多三个素数的和。
**例:**

```
Input : 27
Output : 27 = 3 + 5 + 19

Input : 15
Output : 15 = 2 + 13
```

**方法:**这里，我们用[哥德巴赫猜想](https://www.geeksforgeeks.org/program-for-goldbachs-conjecture-two-primes-with-given-sum/)来解决这个问题。它说任何偶数都可以表示为两个素数之和。
我们这里有三种情况:
1)当 N 是质数时，打印该数。
2)当(N-2)为素数时，打印 2 和 N-2。
3)将 N 表示为 3 + (N-3)。显然，N-3 将是一个偶数(从一个奇数减去另一个奇数得到偶数)。所以，根据哥德巴赫猜想，可以表示为两个素数之和。所以，打印 3 和其他两个质数。

## C++

```
// CPP program to express N as sum of at-most
// three prime numbers.
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number is prime or not.
bool isPrime(int x)
{
    if (x == 0 || x == 1)
        return false;
    for (int i = 2; i * i <= x; ++i)
        if (x % i == 0)
            return false;   
    return true;
}

// Prints at most three prime numbers whose
// sum is n.
void findPrimes(int n)
{
    if (isPrime(n)) // CASE-I   
        cout << n << endl;

    else if (isPrime(n - 2)) // CASE-II   
        cout << 2 << " " << n - 2 << endl;

    else // CASE-III
    {
        cout << 3 << " ";
        n = n - 3;
        for (int i = 0; i < n; i++) {
            if (isPrime(i) && isPrime(n - i)) {
                cout << i << " " << (n - i);
                break;
            }
        }
    }
}

// Driver code
int main()
{
    int n = 27;
    findPrimes(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to express N as sum
// of at-most three prime numbers.
import java.util.*;

class GFG{

    // Function to check if a
    // number is prime or not.
    public static boolean isPrime(int x)
    {
        if (x == 0 || x == 1)
            return false;

        for (int i = 2; i * i <= x; ++i)
            if (x % i == 0)
                return false;
        return true;
    }

    // Prints at most three prime
    // numbers whose sum is n.
    public static void findPrimes(int n)
    {
        if (isPrime(n)) // CASE-I
            System.out.print( n );

        else if (isPrime(n - 2)) // CASE-II
            System.out.print( 2 + " " +
                              (n - 2) );

        else // CASE-III
        {
            System.out.print( 3 + " ");
            n = n - 3;

            for (int i = 0; i < n; i++) {
                if (isPrime(i) && isPrime(n - i)) {
                    System.out.print( i + " " +
                                         (n - i));
                    break;
                }
            }
        }
    }

    // driver code
    public static void main(String[] args)
    {
        int n = 27;
        findPrimes(n);
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 program to express N as
# sum of at-most three prime numbers

# Function to check if a number
# is prime or not.
def isPrime(x):
    if(x == 0 or x == 1) :
        return 0
    i = 2
    while i * i <= x :
        if (x % i == 0) :
            return 0
        i = i + 1
    return 1

# Prints at most three prime numbers
# whose sum is n.
def findPrimes(n) :
    if (isPrime(n)):

        # CASE-I
        print(n, end = " ")

    elif (isPrime(n - 2)) :

        # CASE-II
        print ("2", end = " ")
        print (n - 2, end = " " )

    else:
        #CASE-III
        print ( "3", end = " " )
        n = n - 3
        i = 0
        while i < n :
            if (isPrime(i) and isPrime(n - i)) :
                print(i, end = " ")
                print ((n - i), end = " ")
                break
            i = i + 1

# Driver Code
n = 27;
findPrimes(n);

# This code is contributed by rishabh_jain
```

## C#

```
// C# program to express N as sum
// of at-most three prime numbers.
using System;

class GFG
{

    // Function to check if a
    // number is prime or not.
    public static bool isPrime(int x)
    {
        if (x == 0 || x == 1)
            return false;

        for (int i = 2; i * i <= x; ++i)
            if (x % i == 0)
                return false;
        return true;
    }

    // Prints at most three prime
    // numbers whose sum is n.
    public static void findPrimes(int n)
    {
        if (isPrime(n)) // CASE-I
            Console.WriteLine( n );

        else if (isPrime(n - 2)) // CASE-II
            Console.Write( 2 + " " +
                            (n - 2) );

        else // CASE-III
        {
            Console.Write( 3 + " ");
            n = n - 3;

            for (int i = 0; i < n; i++) {
                if (isPrime(i) && isPrime(n - i))
                {
                    Console.WriteLine( i + " " +
                                        (n - i));
                    break;
                }
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 27;
        findPrimes(n);
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to express
// N as sum of at-most
// three prime numbers.

// Function to check if a
// number is prime or not.
function isPrime($x)
{
    if ($x == 0 || $x == 1)
        return false;
    for ($i = 2; $i * $i <= $x; ++$i)
        if ($x % $i == 0)
            return false;
    return true;
}

// Prints at most three prime
// numbers whose sum is n.
function findPrimes($n)
{
    // CASE-I
    if (isPrime($n))
        echo($n);

    // CASE-II
    else if (isPrime($n - 2)) 
        echo(2 . " " . ($n - 2));

    // CASE-III
    else
    {
        echo(3 . " ");
        $n = $n - 3;
        for ($i = 0; $i < $n; $i++)
        {
            if (isPrime($i) &&
                isPrime($n - $i))
            {
                echo($i . " " .
                    ($n - $i));
                break;
            }
        }
    }
}

// Driver code
$n = 27;
findPrimes($n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript program to express N as sum
// of at-most three prime numbers.

    // Function to check if a
    // number is prime or not.
    function isPrime(x)
    {
        if (x == 0 || x == 1)
            return false;

        for (let i = 2; i * i <= x; ++i)
            if (x % i == 0)
                return false;
        return true;
    }

    // Prlets at most three prime
    // numbers whose sum is n.
    function findPrimes(n)
    {
        if (isPrime(n)) // CASE-I
           document.write( n );

        else if (isPrime(n - 2)) // CASE-II
            document.write( 2 + " " +
                              (n - 2) );

        else // CASE-III
        {
            document.write( 3 + " ");
            n = n - 3;

            for (let i = 0; i < n; i++) {
                if (isPrime(i) && isPrime(n - i)) {
                    document.write( i + " " +
                                         (n - i));
                    break;
                }
            }
        }
    }

// Driver code
         let n = 27;
        findPrimes(n);

   // This code is contributed by susmitakundugoaldanga.
</script>
```

输出:

```
3 5 19
```