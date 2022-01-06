# 开悟数字

> 原文:[https://www.geeksforgeeks.org/enlightened-numbers/](https://www.geeksforgeeks.org/enlightened-numbers/)

**开悟数**是一个复合数 **N** 如果它以其独特的质因数
的连接开始的话一些开悟数是:

> 250、256、2048、2176、2304、2500、2560……

### 检查 N 是否为开悟数

给定一个数字 **N** ，任务是检查 **N** 是否为**开悟数**。如果 **N** 是开悟数，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 2500
> **输出:** Yes
> **解释:**
> 25 的因式分解= 2^2 * 5^4
> **n**也以‘25’开头。
> **输入:** N = 25
> **输出:**否

**方法:**想法是检查 N 是否是复合的，如果不是复合的则返回 false，否则将数字 **N** 的所有不同质因数连接成一个字符串。另外，将数字**转换为字符串。现在我们只需要检查不同质因数的连接是否是数字 **N** 的前缀，如果是则打印**“是”**否则打印**“否”**。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the
// above approach
#include<iostream>
#include<math.h>
using namespace std;

// Function to check if N is a
// Composite Number
bool isComposite(int n)
{

    // Corner cases
    if (n <= 3)
        return false;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to return concatenation of
// distinct prime factors of a given number n
int concatenatePrimeFactors(int n)
{
    char concatenate;

    // Handle prime factor 2 explicitly
    // so that can optimally handle
    // other prime factors.
    if (n % 2 == 0)
    {
        concatenate += char(2);
        while (n % 2 == 0)
            n = n / 2;
    }

    // n must be odd at this point.
    // So we can skip one element
    // (Note i = i + 2)
    for(int i = 3; i <= sqrt(n); i = i + 2)
    {
        // While i divides n, print
        // i and divide n
        if (n % i == 0)
        {
            concatenate += i;
            while (n % i == 0)
                n = n / i;
        }
    }

    // This condition is to handle the
    // case when n is a prime number
    // greater than 2
    if (n > 2)
        concatenate += n;

    return concatenate;
}

// Function to check if a number is
// is an enlightened number
bool isEnlightened(int N)
{

    // Number should not be prime
    if (!isComposite(N))
        return false;

    // Converting N to string
    char num = char(N);

    // Function call
    char prefixConc = concatenatePrimeFactors(N);

    return int(prefixConc);
}

// Driver code
int main()
{
    int n = 250;

    if (isEnlightened(n))
        cout << "Yes";
    else
        cout << "No";
}

// This code is contributed by adityakumar27200
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach

import java.util.*;

class GFG {

    // Function to check if N is a
    // Composite Number
    static boolean isComposite(int n)
    {
        // Corner cases
        if (n <= 3)
            return false;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return true;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return true;

        return false;
    }

    // Function to return concatenation of
    // distinct prime factors of a given number n
    static String concatenatePrimeFactors(int n)
    {
        String concatenate = "";

        // Handle prime factor 2 explicitly
        // so that can optimally handle
        // other prime factors.
        if (n % 2 == 0) {
            concatenate += "2";
            while (n % 2 == 0)
                n = n / 2;
        }

        // n must be odd at this point.
        // So we can skip one element
        // (Note i = i + 2)
        for (int i = 3; i <= Math.sqrt(n); i = i + 2) {
            // While i divides n, print
            // i and divide n
            if (n % i == 0) {
                concatenate += i;
                while (n % i == 0)
                    n = n / i;
            }
        }

        // This condition is to handle the
        // case when n is a prime number
        // greater than 2
        if (n > 2)
            concatenate += n;

        return concatenate;
    }

    // Function to check if a number is
    // is an enlightened number
    static boolean isEnlightened(int N)
    {
        // number should not be prime
        if (!isComposite(N))
            return false;

        // converting N to string
        String num = String.valueOf(N);
        // function call
        String prefixConc
            = concatenatePrimeFactors(N);

        return num.startsWith(prefixConc);
    }

    // Driver code
    public static void main(String args[])
    {

        int n = 250;
        if (isEnlightened(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
import math

# Function to check if N is a
# Composite Number
def isComposite(n):

    # Corner cases
    if n <= 3:
        return False

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return True

    i = 5
    while(i * i <= n):
        if(n % i == 0 or n % (i + 2) == 0):
            return True
        i = i + 6

    return False

# Function to return concatenation of
# distinct prime factors of a given number n    
def concatenatePrimeFactors(n):

    concatenate = ""

    # Handle prime factor 2 explicitly
    # so that can optimally handle
    # other prime factors.
    if(n % 2 == 0):
        concatenate += "2"

        while(n % 2 == 0):
            n = int(n / 2)

    # n must be odd at this point.
    # So we can skip one element
    # (Note i = i + 2)
    i = 3
    while(i <= int(math.sqrt(n))):

        # While i divides n, print
        # i and divide n
        if(n % i == 0):
            concatenate += str(i)

            while(n % i == 0):
                n = int(n / i)

        i = i + 2

    # This condition is to handle the
    # case when n is a prime number
    # greater than 2    
    if(n > 2):
        concatenate += str(n)

    return concatenate

# Function to check if a number is
# is an enlightened number
def isEnlightened(N):

    # Number should not be prime
    if(not isComposite(N)):
        return False

    # Converting N to string    
    num = str(N)

    # Function call
    prefixConc = concatenatePrimeFactors(N)

    return int(prefixConc)

# Driver code   
if __name__=="__main__":

    n = 250

    if(isEnlightened(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by adityakumar27200
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG{

// Function to check if N is a
// Composite Number
static bool isComposite(int n)
{

    // Corner cases
    if (n <= 3)
        return false;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    for(int i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return true;

    return false;
}

// Function to return concatenation of
// distinct prime factors of a given number n
static String concatenatePrimeFactors(int n)
{
    String concatenate = "";

    // Handle prime factor 2 explicitly
    // so that can optimally handle
    // other prime factors.
    if (n % 2 == 0)
    {
        concatenate += "2";
        while (n % 2 == 0)
            n = n / 2;
    }

    // n must be odd at this point.
    // So we can skip one element
    // (Note i = i + 2)
    for(int i = 3; i <= Math.Sqrt(n);
            i = i + 2)
    {

       // While i divides n, print
       // i and divide n
       if (n % i == 0)
       {
           concatenate += i;
           while (n % i == 0)
               n = n / i;
       }
    }

    // This condition is to handle the
    // case when n is a prime number
    // greater than 2
    if (n > 2)
        concatenate += n;

    return concatenate;
}

// Function to check if a number is
// is an enlightened number
static bool isEnlightened(int N)
{

    // Number should not be prime
    if (!isComposite(N))
        return false;

    // Converting N to string
    String num = String.Join("", N);

    // Function call
    String prefixConc = concatenatePrimeFactors(N);

    return num.StartsWith(prefixConc);
}

// Driver code
public static void Main(String []args)
{
    int n = 250;

    if (isEnlightened(n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above approach

// Function to check if N is a
// Composite Number
function isComposite(n)
{

    // Corner cases
    if (n <= 3)
        return false;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    for(var i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to return concatenation of
// distinct prime factors of a given number n
function concatenatePrimeFactors(n)
{
    var concatenate;

    // Handle prime factor 2 explicitly
    // so that can optimally handle
    // other prime factors.
    if (n % 2 == 0)
    {
        concatenate += "2";
        while (n % 2 == 0)
            n = parseInt(n / 2);
    }

    // n must be odd at this point.
    // So we can skip one element
    // (Note i = i + 2)
    for(var i = 3; i <= Math.sqrt(n); i = i + 2)
    {
        // While i divides n, print
        // i and divide n
        if (n % i == 0)
        {
            concatenate += i;
            while (n % i == 0)
                n = parseInt(n / i);
        }
    }

    // This condition is to handle the
    // case when n is a prime number
    // greater than 2
    if (n > 2)
        concatenate += n;

    return concatenate;
}

// Function to check if a number is
// is an enlightened number
function isEnlightened(N)
{

    // Number should not be prime
    if (!isComposite(N))
        return false;

    // Converting N to string
    var num = (N.toString());

    // Function call
    var prefixConc = concatenatePrimeFactors(N);

    return (prefixConc);
}

// Driver code
var n = 250;

if (isEnlightened(n))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**T2【O(n)T4】