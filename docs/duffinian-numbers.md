# 杜非尼数字

> 原文:[https://www.geeksforgeeks.org/duffinian-numbers/](https://www.geeksforgeeks.org/duffinian-numbers/)

给定一个数字 **N** ，任务是检查 **N** 是否是**杜芬尼号**。如果 **N** 是一个杜非尼数字，那么打印**“是”**否则打印**“否”**。

> **杜非尼数**是一个复合数 **N** ，因此它是 N 的除数之和的相对素数

**示例:**

> **输入:** N = 35
> **输出:**是
> **说明:**
> 35 的除数之和= 1 + 5 + 7 + 35 = 48，
> 和 48 相对于 35 是素数。
> **输入:** N = 28
> **输出:** No
> **说明:**
> 28 的除数之和= 1 + 2 + 4 + 7 + 14 + 28 = 56，
> 和 56 相对于 28 不是素数。

**逼近:**思路是求数 **N** 的因子之和。如果 **N** 的 gcd 和 **N** 的因子之和相对素数，那么给定的数 **N** 是**杜非尼数**，否则 **N** 不是**杜非尼数**。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum of all
// divisors of a given number
int divSum(int n)
{
    // Sum of divisors
    int result = 0;

    // Find all divisors of num
    for (int i = 2; i <= sqrt(n); i++) {

        // if 'i' is divisor of 'n'
        if (n % i == 0) {

            // If both divisors are same
            // then add it once
            if (i == (n / i))
                result += i;
            else
                result += (i + n / i);
        }
    }

    // Add 1 and n to result as above
    // loop considers proper divisors
    // greater than 1.
    return (result + n + 1);
}

// Function to check if n is an
// Duffinian number
bool isDuffinian(int n)
{

    // Calculate the sum of divisors
    int sumDivisors = divSum(n);

    // If number is prime return false
    if (sumDivisors == n + 1)
        return false;

    // Find the gcd of n and sum of
    // divisors of n
    int hcf = __gcd(n, sumDivisors);

    // Returns true if N and sumDivisors
    // are relatively prime
    return hcf == 1;
}

// Driver Code
int main()
{
    // Given Number
    int n = 36;

    // Function Call
    if (isDuffinian(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Recursive function to return
// gcd of a and b
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to calculate the sum of
// all divisors of a given number
static int divSum(int n)
{

    // Sum of divisors
    int result = 0;

    // Find all divisors of num
    for(int i = 2; i <= Math.sqrt(n); i++)
    {

       // if 'i' is divisor of 'n'
       if (n % i == 0)
       {

           // If both divisors are same
           // then add it once
           if (i == (n / i))
               result += i;
           else
               result += (i + n / i);
       }
    }

    // Add 1 and n to result as above
    // loop considers proper divisors
    // greater than 1.
    return (result + n + 1);
}

// Function to check if n is an
// Duffinian number
static boolean isDuffinian(int n)
{

    // Calculate the sum of divisors
    int sumDivisors = divSum(n);

    // If number is prime return false
    if (sumDivisors == n + 1)
        return false;

    // Find the gcd of n and sum of
    // divisors of n
    int hcf = gcd(n, sumDivisors);

    // Returns true if N and sumDivisors
    // are relatively prime
    return hcf == 1;
}

// Driver code
public static void main(String[] args)
{

    // Given Number
    int n = 36;

    // Function Call
    if (isDuffinian(n))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to calculate the sum of all
# divisors of a given number
def divSum(n):

    # Sum of divisors
    result = 0

    # Find all divisors of num
    for i in range(2, int(math.sqrt(n)) + 1):

        # If 'i' is divisor of 'n'
        if (n % i == 0):

            # If both divisors are same
            # then add it once
            if (i == (n // i)):
                result += i
            else:
                result += (i + n / i)

    # Add 1 and n to result as above
    # loop considers proper divisors
    # greater than 1.
    return (result + n + 1)

# Function to check if n is an
# Duffinian number
def isDuffinian(n):

    # Calculate the sum of divisors
    sumDivisors = int(divSum(n))

    # If number is prime return false
    if (sumDivisors == n + 1):
        return False

    # Find the gcd of n and sum of
    # divisors of n
    hcf = math.gcd(n, sumDivisors)

    # Returns true if N and sumDivisors
    # are relatively prime
    return hcf == 1

# Driver Code

# Given number
n = 36

# Function call
if (isDuffinian(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Recursive function to return
// gcd of a and b
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to calculate the sum of
// all divisors of a given number
static int divSum(int n)
{

    // Sum of divisors
    int result = 0;

    // Find all divisors of num
    for(int i = 2; i <= Math.Sqrt(n); i++)
    {

       // If 'i' is divisor of 'n'
       if (n % i == 0)
       {

           // If both divisors are same
           // then add it once
           if (i == (n / i))
               result += i;
           else
               result += (i + n / i);
       }
    }

    // Add 1 and n to result as above
    // loop considers proper divisors
    // greater than 1.
    return (result + n + 1);
}

// Function to check if n is an
// Duffinian number
static bool isDuffinian(int n)
{

    // Calculate the sum of divisors
    int sumDivisors = divSum(n);

    // If number is prime return false
    if (sumDivisors == n + 1)
        return false;

    // Find the gcd of n and sum of
    // divisors of n
    int hcf = gcd(n, sumDivisors);

    // Returns true if N and sumDivisors
    // are relatively prime
    return hcf == 1;
}

// Driver code
public static void Main(string[] args)
{

    // Given number
    int n = 36;

    // Function call
    if (isDuffinian(n))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Recursive function to return
    // gcd of a and b
    function gcd( a , b) {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to calculate the sum of
    // all divisors of a given number
    function divSum( n) {

        // Sum of divisors
        let result = 0;

        // Find all divisors of num
        for (let i = 2; i <= Math.sqrt(n); i++) {

            // if 'i' is divisor of 'n'
            if (n % i == 0) {

                // If both divisors are same
                // then add it once
                if (i == (n / i))
                    result += i;
                else
                    result += (i + n / i);
            }
        }

        // Add 1 and n to result as above
        // loop considers proper divisors
        // greater than 1.
        return (result + n + 1);
    }

    // Function to check if n is an
    // Duffinian number
    function isDuffinian( n) {

        // Calculate the sum of divisors
        let sumDivisors = divSum(n);

        // If number is prime return false
        if (sumDivisors == n + 1)
            return false;

        // Find the gcd of n and sum of
        // divisors of n
        let hcf = gcd(n, sumDivisors);

        // Returns true if N and sumDivisors
        // are relatively prime
        return hcf == 1;
    }

    // Driver code

        // Given Number
        let n = 36;

        // Function Call
        if (isDuffinian(n)) {
            document.write("Yes");
        } else {
            document.write("No");
        }

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(1)*