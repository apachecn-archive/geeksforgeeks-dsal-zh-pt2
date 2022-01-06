# 偶数完全数

> 原文:[https://www.geeksforgeeks.org/even-perfect-number/](https://www.geeksforgeeks.org/even-perfect-number/)

给定一个偶数 **N** ，任务是在没有找到其**因子**的情况下，检查其是否为 [**完全数**](https://www.geeksforgeeks.org/perfect-number/) 。

> *在数论中，**偶完全数**是一个正整数，它是偶数或者等于它的正整数除数之和，不包括数本身。*
> 
> 一个**偶完全数**可以表示为 **P * (P + 1) / 2** ，其中 P 为 [**梅森素数**](https://www.geeksforgeeks.org/mersenne-prime/) 。
> 
> A [**梅森素数**](https://www.geeksforgeeks.org/mersenne-prime/) 是形式**2<sup>q</sup>–1**的素数，其中 q 也是素数。
> 例如:如果 N = 6，
> 如果我们选择 q 为 2(素数)，那么梅森素数(P)为 2<sup>2</sup>–1 = 3。
> 因此，由公式形成的偶完全数为 3 * (3 + 1) / 2 = 6。

**示例:**

> **输入:** N = 6
> **输出:**是
> **说明:**
> 整数 6 可以写成 6 = 1 + 2 + 3。因此，它的完全数。
> 
> **输入:** N =156
> **输出:**否
> **说明:**
> 整数 156 不能写成其除数之和。因此，它不是一个完美的数字。

**进场:**

1.  求给定数的[平方根，得到一个接近**2<sup>q</sup>–1**的数。](https://www.geeksforgeeks.org/square-root-of-an-integer/)
2.  从数字的平方根找到 q-1，然后检查**2<sup>q-1</sup>*(2<sup>q</sup>-1)**是否给出输入的数字。如果不是，那么它不是一个完全数，否则继续。
3.  [检查 q 是否为质数](https://www.geeksforgeeks.org/check-if-a-number-is-prime-semi-prime-or-composite-for-very-large-numbers/)。如果不是质数，则 **2 <sup>q</sup> -1** 不能质数，随后检查 2 <sup>q</sup> -1 是否质数。
4.  如果以上所有条件都成立，那么它就是一个偶数完全数，否则就不是。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

bool isPrime(long n);

// Function to check for perfect number
void check(long num)
{

    // Find a number close to 2^q-1
    long root = (long)sqrt(num);

    // Calculate q-1
    long poww = (long)(log(root) / log(2));

    // Condition of perfect number
    if (num == (long)(pow(2, poww) *
                    (pow(2, poww + 1) - 1)))
    {

        // Check whether q is prime or not
        if (isPrime(poww + 1))
        {

            // Check whether 2^q - 1 is a
            // prime number or not
            if (isPrime((long)pow(2,
                poww + 1) - 1))
                cout << "Yes" << endl;
            else
                cout << "No" << endl;
        }
        else
            cout << "No" << endl;
    }
    else
        cout << "No" << endl;
}

// Function to check for prime number
bool isPrime(long n)
{
    if (n <= 1)
        return false;

    // Check whether it is equal to 2 or 3
    else if (n == 2 || n == 3)
        return true;

    else
    {

        // Check if it can be divided by 2
        // and 3 then it is not prime number
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        // Check whether the given number be
        // divide by other prime numbers
        for(long i = 5; i <= sqrt(n); i += 6)
        {
            if (n % i == 0 || n % (i + 2) == 0)
                return false;
        }
        return true;
    }
}

// Driver Code
int main()
{
    long num = 6;

    check(num);

    return 0;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to check for perfect number
    private static void check(long num)
    {
        // Find a number close to 2^q-1
        long root = (long)Math.sqrt(num);

        // Calculate q-1
        long pow
            = (long)(Math.log(root)
                    / Math.log(2));

        // Condition of perfect number
        if (num
            == (long)(Math.pow(2, pow)
                    * (Math.pow(2, pow + 1) - 1))) {

            // Check whether q is prime or not
            if (isPrime(pow + 1)) {

                // Check whether 2^q - 1 is a
                // prime number or not
                if (isPrime(
                        (long)Math.pow(
                            2, pow + 1)
                        - 1))
                    System.out.println("Yes");

                else
                    System.out.println("No");
            }
            else
                System.out.println("No");
        }
        else
            System.out.println("No");
    }

    // Function to check for prime number
    public static boolean isPrime(long n)
    {
        if (n <= 1)
            return false;

        // Check whether it is equal to 2 or 3
        else if (n == 2 || n == 3)
            return true;

        else {
            // Check if it can be divided by 2
            // and 3 then it is not prime number
            if (n % 2 == 0 || n % 3 == 0)
                return false;

            // Check whether the given number be
            // divide by other prime numbers
            for (long i = 5;
                i <= Math.sqrt(n);
                i += 6) {
                if (n % i == 0
                    || n % (i + 2) == 0)
                    return false;
            }
            return true;
        }
    }

    // Driver code
    public static void main(String args[])
    {
        long num = 6;
        check(num);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check for perfect number
def check(num):

    # Find a number close to 2^q-1
    root = (int)(math.sqrt(num))

    # Calculate q-1
    poww = (int)(math.log(root) /
                 math.log(2))

    # Condition of perfect number
    if (num == (int)(pow(2, poww) *
                    (pow(2, poww + 1) - 1))):

        # Check whether q is prime or not
        if (isPrime(poww + 1)):

            # Check whether 2^q - 1 is a
            # prime number or not
            if (isPrime((int)(pow(2,
                poww + 1)) - 1)):
                print("Yes")
            else:
                print("No")

        else:
            print("No")
    else:
        print("No")

# Function to check for prime number
def isPrime(n):

    if (n <= 1):
        return bool(False)

    # Check whether it is equal to 2 or 3
    elif (n == 2 or n == 3):
        return bool(True)

    else:

        # Check if it can be divided by 2
        # and 3 then it is not prime number
        if (n % 2 == 0 or n % 3 == 0):
            return bool(False)

        # Check whether the given number be
        # divide by other prime numbers
        for i in range(5, sqrt(n + 1) + 1, 6):
            if (n % i == 0 or n % (i + 2) == 0):
                return bool(False)

        return bool(True)

# Driver Code        
num = 6

check(num)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check for perfect number
private static void check(long num)
{

    // Find a number close to 2^q-1
    long root = (long)Math.Sqrt(num);

    // Calculate q-1
    long pow = (long)(Math.Log(root) /
                    Math.Log(2));

    // Condition of perfect number
    if (num == (long)(Math.Pow(2, pow) *
                    (Math.Pow(2, pow + 1) - 1)))
    {

        // Check whether q is prime or not
        if (isPrime(pow + 1))
        {

            // Check whether 2^q - 1 is a
            // prime number or not
            if (isPrime((long)Math.Pow(2, pow + 1) - 1))
                Console.WriteLine("Yes");

            else
                Console.WriteLine("No");
        }
        else
            Console.WriteLine("No");
    }
    else
        Console.WriteLine("No");
}

// Function to check for prime number
public static bool isPrime(long n)
{
    if (n <= 1)
        return false;

    // Check whether it is equal to 2 or 3
    else if (n == 2 || n == 3)
        return true;

    else
    {

        // Check if it can be divided by 2
        // and 3 then it is not prime number
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        // Check whether the given number be
        // divide by other prime numbers
        for(long i = 5;
                i <= Math.Sqrt(n);
                i += 6)
        {
            if (n % i == 0 || n % (i + 2) == 0)
                return false;
        }
        return true;
    }
}

// Driver code
public static void Main(String []args)
{
    long num = 6;
    check(num);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

    // Function to check for perfect number
    function check(num)
    {
        // Find a number close to 2^q-1
        let root = Math.floor(Math.sqrt(num));

        // Calculate q-1
        let pow
            = Math.floor(Math.log(root)
                    / Math.log(2));

        // Condition of perfect number
        if (num
            == Math.floor(Math.pow(2, pow)
                    * (Math.pow(2, pow + 1) - 1))) {

            // Check whether q is prime or not
            if (isPrime(pow + 1)) {

                // Check whether 2^q - 1 is a
                // prime number or not
                if (isPrime(
                        Math.floor(Math.pow(
                            2, pow + 1) )
                        - 1))
                    document.write("Yes");

                else
                    document.write("No");
            }
            else
                document.write("No");
        }
        else
            document.write("No");
    }

    // Function to check for prime number
    function isPrime(n)
    {
        if (n <= 1)
            return false;

        // Check whether it is equal to 2 or 3
        else if (n == 2 || n == 3)
            return true;

        else {
            // Check if it can be divided by 2
            // and 3 then it is not prime number
            if (n % 2 == 0 || n % 3 == 0)
                return false;

            // Check whether the given number be
            // divide by other prime numbers
            for (let i = 5;
                i <= Math.floor(Math.sqrt(n));
                i += 6) {
                if (n % i == 0
                    || n % (i + 2) == 0)
                    return false;
            }
            return true;
        }
    }

// Driver Code   

    let num = 6;
    check(num);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>1/4</sup>)*
***辅助空间:** O(1)*