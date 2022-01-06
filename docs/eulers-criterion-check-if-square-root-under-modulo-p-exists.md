# 欧拉准则(检查模 p 下的平方根是否存在)

> 原文:[https://www . geeksforgeeks . org/Euler s-criteria-check-if-平方根-下模-p-exists/](https://www.geeksforgeeks.org/eulers-criterion-check-if-square-root-under-modulo-p-exists/)

给定一个数 n 和一个素数 p，求模 p 下 n 的平方根是否存在。一个数 x 是模 p 下 n 的平方根，如果(x*x)%p = n%p。

**示例:**

```
Input:   n = 2, p = 5
Output:  false
There doesn't exist a number x such that 
(x*x)%5 is 2

Input:   n = 2, p = 7
Output:  true
There exists a number x such that (x*x)%7 is
2\.  The number is 3.
```

一种**天真的方法**是尝试每个数字 x，其中 x 从 2 到 p-1 不等。对于每个 x，检查(x * x) % p 是否等于 n % p。

## C++

```
// A Simple C++ program to check if square root of a number
// under modulo p exists or not
#include<iostream>
using namespace std;

// Returns true if square root of n under modulo p exists
bool squareRootExists(int n, int p)
{
    n = n%p;

    // One by one check all numbers from 2 to p-1
    for (int x=2; x<p; x++)
        if ((x*x)%p == n)
            return true;
    return false;
}

// Driver program to test
int main()
{
   int p = 7;
   int n = 2;
   squareRootExists(n, p)? cout << "Yes": cout << "No";
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple Java program to check if square
// root of a number under modulo p exists or not
class GFG
{

    // Returns true if square root of n under
    // modulo p exists
    static boolean squareRootExists(int n, int p)
    {
        n = n % p;

        // One by one check all numbers from 2
        // to p-1
        for (int x = 2; x < p; x++)
            if ((x * x) % p == n)
                return true;

        return false;
    }

    // Driver program to test
    public static void main (String[] args)
    {

        int p = 7;
        int n = 2;

        if(squareRootExists(n, p))
            System.out.print("Yes");
        else
            System.out.print("No"); 
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# A Simple Python 3 program to
# check if square root of a number
# under modulo p exists or not

# Returns true if square root of
# n under modulo p exists
def squareRootExists(n, p):
    n = n % p

    # One by one check all numbers
    # from 2 to p-1
    for x in range(2, p, 1):
        if ((x * x) % p == n):
            return True
    return False

# Driver Code
if __name__ == '__main__':
    p = 7
    n = 2
    if(squareRootExists(n, p) == True):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// A Simple C# program to check
// if square root of a number
// under modulo p exists or not
using System;

class GFG
{

    // Returns true if square root of 
    // n under modulo p exists
    static bool squareRootExists(int n,
                                 int p)
    {
        n = n % p;

        // One by one check all numbers
        // from 2 to p-1
        for (int x = 2; x < p; x++)
            if ((x * x) % p == n)
                return true;

        return false;
    }

    // Driver code
    public static void Main ()
    {

        int p = 7;
        int n = 2;

        if(squareRootExists(n, p))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Simple PHP program to check
// if square root of a number
// under modulo p exists or not

// Returns true if square root
// of n under modulo p exists
function squareRootExists($n, $p)
{
    $n = $n % $p;

    // One by one check all
    // numbers from 2 to p-1
    for ($x = 2; $x < $p; $x++)
        if (($x * $x) % $p == $n)
            return true;
    return false;
}

// Driver Code
$p = 7;
$n = 2;
if(squareRootExists($n, $p) == true)
    echo "Yes";
else
    echo "No";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// A Simple Javascript program to check
// if square root of a number
// under modulo p exists or not

// Returns true if square root
// of n under modulo p exists
function squareRootExists(n, p)
{
    n = n % p;

    // One by one check all
    // numbers from 2 to p-1
    for(let x = 2; x < p; x++)
        if ((x * x) % p == n)
            return true;

    return false;
}

// Driver Code
let p = 7;
let n = 2;

if (squareRootExists(n, p) === true)
    document.write("Yes");
else
    document.write("No");

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
Yes
```

该方法的时间复杂度为 0(p)。

这个问题有一个基于欧拉准则的直接解。
**欧拉准则**指出

```
Square root of n under modulo p exists if and only if
n<sup>(p-1)/2 % p = 1</sup>

Here square root of n exists means is, there exist
an integer x such that (x * x) % p = 1
```

以下是基于上述标准的实现。幂函数参见[模幂运算](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)。

## C++

```
// C++ program to check if square root of a number
// under modulo p exists or not
#include<iostream>
using namespace std;

// Utility function to do modular exponentiation.
// It returns (x^y) % p.
int power(int x, int y, int p)
{
    int res = 1;     // Initialize result
    x = x % p; // Update x if it is more than or
               // equal to p

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res*x) % p;

        // y must be even now
        y = y>>1; // y = y/2
        x = (x*x) % p;
    }
    return res;
}

// Returns true if there exists an integer x such
// that (x*x)%p = n%p
bool squareRootExists(int n, int p)
{
    // Check for Euler's criterion that is
    // [n ^ ((p-1)/2)] % p is 1 or not.
    if (power(n, (p-1)/2, p) == 1)
       return true;

    return false;
}

// Driver program to test
int main()
{
   int p = 7;
   int n = 2;
   squareRootExists(n, p)? cout << "Yes": cout << "No";
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// square root of a number
// under modulo p exists or not
import java.io.*;

class GFG
{

// Utility function to do
// modular exponentiation.
// It returns (x^y) % p.
static int power(int x, int y, int p)
{
    int res = 1;     // Initialize result
    x = x % p; // Update x if it is more
               // than or equal to p

    while (y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ((y & 1) == 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Returns true if there
// exists an integer x such
// that (x*x)%p = n%p
static boolean squareRootExists(int n,
                                int p)
{
    // Check for Euler's criterion
    // that is [n ^ ((p-1)/2)] % p
    // is 1 or not.
    if (power(n, (p - 1) / 2, p) == 1)
    return true;

    return false;
}

// Driver Code
public static void main (String[] args)
{
    int p = 7;
    int n = 2;
    if(squareRootExists(n, p))
        System.out.println ("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 program to check if square root
# of a number under modulo p exists or not

# Utility function to do modular
# exponentiation. It returns (x^y) % p.
def power(x, y, p):
    res = 1 # Initialize result
    x = x % p

    # Update x if it is more than
    # or equal to p
    while (y > 0):

        # If y is odd, multiply
        # x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p
    return res

# Returns true if there exists an integer
# x such that (x*x)%p = n%p
def squareRootExists(n, p):

    # Check for Euler's criterion that is
    # [n ^ ((p-1)/2)] % p is 1 or not.
    if (power(n, (int)((p - 1) / 2), p) == 1):
        return True
    return False

# Driver Code
p = 7
n = 2
if(squareRootExists(n, p) == True):
    print("Yes")
else:
    print("No")

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to check if
// square root of a number
// under modulo p exists or not
using System;

class GFG
{

// Utility function to do
// modular exponentiation.
// It returns (x^y) % p.
static int power(int x,
                 int y, int p)
{
    int res = 1;// Initialize result
    x = x % p;  // Update x if it is more
                // than or equal to p

    while (y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ((y & 1) == 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Returns true if there
// exists an integer x such
// that (x*x)%p = n%p
static bool squareRootExists(int n,
                             int p)
{
    // Check for Euler's criterion
    // that is [n ^ ((p-1)/2)] % p
    // is 1 or not.
    if (power(n, (p - 1) / 2, p) == 1)
    return true;

    return false;
}

// Driver Code
static public void Main ()
{
    int p = 7;
    int n = 2;
    if(squareRootExists(n, p))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// if square root of a
// number under modulo
// p exists or not

// Utility function to
// do modular exponentiation
// It returns (x^y) % p.
function power($x, $y, $p)
{
    $res = 1; // Initialize result
    $x = $x % $p; // Update x if it 
                  // is more than
                  // or equal to p

    while ($y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res *
                    $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Returns true if there
// exists an integer x such
// that (x*x)%p = n%p
function squareRootExists($n, $p)
{
    // Check for Euler's criterion
    // that is [n ^ ((p-1)/2)] % p
    // is 1 or not.
    if (power($n, (int)(($p - 1) / 2),
                         $p) == 1)
    return true;

    return false;
}

// Driver Code
$p = 7;
$n = 2;

if(squareRootExists($n, $p) == true)
    echo "Yes";
else
    echo "No";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to check if
    // square root of a number
    // under modulo p exists or not

    // Utility function to do
    // modular exponentiation.
    // It returns (x^y) % p.
    function power(x, y, p)
    {
        let res = 1;// Initialize result
        x = x % p;  // Update x if it is more
                    // than or equal to p

        while (y > 0)
        {
            // If y is odd, multiply
            // x with result
            if ((y & 1) == 0)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Returns true if there
    // exists an integer x such
    // that (x*x)%p = n%p
    function squareRootExists(n, p)
    {
        // Check for Euler's criterion
        // that is [n ^ ((p-1)/2)] % p
        // is 1 or not.
        if (power(n, (p - 1) / 2, p) == 1)
            return true;

        return false;
    }

    let p = 7;
    let n = 2;
    if(squareRootExists(n, p))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**输出:**

```
Yes
```

**这是如何工作的？**

```
If p is a prime, then it must be an odd number and (p-1) 
must be an even, i.e., (p-1)/2 must be an integer.

Suppose a square root of n under modulo p exists, then
there must exist an integer x such that,
      x2 % p = n % p 
or, 
     x2 ? n mod p

Raising both sides to power (p-1)/2,
      (x2)(p-1)/2 ? n(p-1)/2 mod p           
      xp-1 ? n(p-1)/2 mod p

Since p is a prime, from Fermet's theorem, we can say that 
   xp-1 ? 1 mod p

Therefore,
  n(p-1)/2 ? 1 mod p  
```

这种基于欧拉准则的方法时间复杂度为 O(Log p)
你可能会喜欢看下面:
[求模 p |集合 1 下的平方根(当 p 是 4*i + 3 的形式时)](https://www.geeksforgeeks.org/find-square-root-under-modulo-p-set-1-when-p-is-in-form-of-4i-3/)
本文由 **Shivam Gupta** 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息