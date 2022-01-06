# 求一个整数 X，它是除了一个数组中的一个元素之外的所有元素的除数

> 原文:[https://www . geeksforgeeks . org/find-a-integer-x-这是一个数组中一个元素的除数/](https://www.geeksforgeeks.org/find-an-integer-x-which-is-divisor-of-all-except-exactly-one-element-in-an-array/)

给定一个整数数组。找到一个整数 X，它是除了给定数组中的一个元素之外的所有元素的除数。
**注**:所有元素的 GCD 都不是 1。

**示例:**

```
Input : arr[] = {6, 18, 3, 12}
Output : 6
6 is the divisor of all except 3.

Input : arr[] = {40, 15, 30, 42}
Output : 3
3 is the divisor of all except 40\. 
```

**方法:**制作前缀数组 P，使得索引 I 包含从 1 到 I 的所有元素的 GCD。类似地，制作后缀数组 S，使得索引 I 包含从 I 到 n-1(最后一个索引)的所有元素的 GCD。如果 P[i-1]和 S[i+1]的 GCD 不是 I 处元素的除数，那么就是需要的答案。
以下是上述办法的实施情况:

## C++

```
// C++ program to find the  divisor  of all
// except for exactly one element in an array.

#include <bits/stdc++.h>
using namespace std;

// Function that returns the  divisor  of all
// except for exactly one element in an array.
int getDivisor(int a[], int n)
{
    // There's only one element in the array
    if (n == 1)
        return (a[0] + 1);

    int P[n], S[n];

    // Creating prefix array of GCD
    P[0] = a[0];
    for (int i = 1; i < n; i++)
         P[i] = __gcd(a[i], P[i - 1]);   

    // Creating suffix array of GCD
    S[n-1] = a[n-1];
    for (int i = n - 2; i >= 0; i--)
         S[i] = __gcd(S[i + 1], a[i]);   

    // Iterate through the array
    for (int i = 0; i <= n; i++) {

        // Variable to store the divisor
        int cur;

        // Getting the divisor
        if (i == 0)
            cur = S[i + 1];
        else if (i == n - 1)
            cur = P[i - 1];
        else
            cur = __gcd(P[i - 1], S[i + 1]);

        // Check if it is not a divisor of a[i]
        if (a[i] % cur != 0)
            return cur;
    }

    return 0;
}

// Driver code
int main()
{
    int a[] = { 12, 6, 18, 12, 16 };

    int n = sizeof(a) / sizeof(a[0]);

    cout << getDivisor(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find the divisor of all
// except for exactly one element in an array.
import java.io.*;

class GFG {

// Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0 
        if (a == 0)
          return b;
        if (b == 0)
          return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }
// Function that returns the divisor of all
// except for exactly one element in an array.
static int getDivisor(int a[], int n)
{
    // There's only one element in the array
    if (n == 1)
        return (a[0] + 1);

    int P[] = new int[n];
    int    S[] = new int[n];

    // Creating prefix array of GCD
    P[0] = a[0];
    for (int i = 1; i < n; i++)
        P[i] = __gcd(a[i], P[i - 1]);

    // Creating suffix array of GCD
    S[n-1] = a[n-1];
    for (int i = n - 2; i >= 0; i--)
        S[i] = __gcd(S[i + 1], a[i]);

    // Iterate through the array
    for (int i = 0; i < n; i++) {

        // Variable to store the divisor
        int cur;

        // Getting the divisor
        if (i == 0)
            cur = S[i + 1];
        else if (i == n - 1)
            cur = P[i - 1];
        else
            cur = __gcd(P[i - 1], S[i + 1]);

        // Check if it is not a divisor of a[i]
        if (a[i] % cur != 0)
            return cur;
    }

    return 0;
}

// Driver code

    public static void main (String[] args) {
            int a[] = { 12, 6, 18, 12, 16 };

    int n = a.length;

    System.out.println(getDivisor(a, n));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to find the divisor of all
# except for exactly one element in an array.
from math import gcd

# Function to find the divisor of all
# except for exactly one element in an array.
def getDivisor(a, n):

    # There's only one element in the array
    if (n == 1):
        return (a[0] + 1)

    P = [0] * n
    S = [0] * n

    # Creating prefix array of GCD
    P[0] = a[0]
    for i in range(1, n):
        P[i] = gcd(a[i], P[i - 1])

    # Creating suffix array of GCD
    S[n - 1] = a[n - 1]
    for i in range(n - 2, -1, -1):
        S[i] = gcd(S[i + 1], a[i])

    # Iterate through the array
    for i in range(0, n + 1):

        # Variable to store the divisor
        cur = 0

        # Getting the divisor
        if (i == 0):
            cur = S[i + 1]
        elif (i == n - 1):
            cur = P[i - 1]
        else:
            cur = gcd(P[i - 1], S[i + 1])

        # Check if it is not a divisor of a[i]
        if (a[i] % cur != 0):
            return cur

    return 0;

# Driver Code
if __name__=='__main__':
    a = [12, 6, 18, 12, 16]
    n = len(a)

    print(getDivisor(a, n))

# This code is contributed by Rupesh Rao
```

## C#

```
// C# program to find the divisor of all
// except for exactly one element in an array.
using System;

class GFG
{

// Recursive function to return gcd of a and b
static int __gcd(int a, int b)
{
    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);
    return __gcd(a, b - a);
}

// Function that returns the divisor of all
// except for exactly one element in an array.
static int getDivisor(int[] a, int n)
{

    // There's only one element in the array
    if (n == 1)
        return (a[0] + 1);

    int[] P = new int[n];
    int[] S = new int[n];

    // Creating prefix array of GCD
    P[0] = a[0];
    for (int i = 1; i < n; i++)
        P[i] = __gcd(a[i], P[i - 1]);

    // Creating suffix array of GCD
    S[n - 1] = a[n - 1];
    for (int i = n - 2; i >= 0; i--)
        S[i] = __gcd(S[i + 1], a[i]);

    // Iterate through the array
    for (int i = 0; i <= n; i++)
    {

        // Variable to store the divisor
        int cur;

        // Getting the divisor
        if (i == 0)
            cur = S[i + 1];
        else if (i == n - 1)
            cur = P[i - 1];
        else
            cur = __gcd(P[i - 1], S[i + 1]);

        // Check if it is not a divisor of a[i]
        if (a[i] % cur != 0)
            return cur;
    }

    return 0;
}

// Driver code
public static void Main ()
{
    int[] a = { 12, 6, 18, 12, 16 };

    int n = a.Length;

    Console.WriteLine(getDivisor(a, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the divisor of all
// except for exactly one element in an array.

// Recursive function to return
// gcd of a and b
function __gcd($a, $b)
{
    // Everything divides 0
    if ($a == 0)
        return b;
    if ($b == 0)
        return $a;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return __gcd($a - $b, $b);

    return __gcd($a, $b - $a);
}

// Function that returns the divisor of all
// except for exactly one element in an array.
function getDivisor($a, $n)
{
    // There's only one element in the array
    if ($n == 1)
        return ($a[0] + 1);

    $P = array() ;
    $S = array() ;

    // Creating prefix array of GCD
    $P[0] = $a[0];

    for ($i = 1; $i < $n; $i++)
        $P[$i] = __gcd($a[$i], $P[$i - 1]);

    // Creating suffix array of GCD
    $S[$n - 1] = $a[$n - 1];
    for ($i = $n - 2; $i >= 0; $i--)
        $S[$i] = __gcd($S[$i + 1], $a[$i]);

    // Iterate through the array
    for ($i = 0; $i <= $n; $i++)
    {

        // Getting the divisor
        if ($i == 0)
            $cur = $S[$i + 1];
        else if ($i == $n - 1)
            $cur = $P[$i - 1];
        else
            $cur = __gcd($P[$i - 1], $S[$i + 1]);

        // Check if it is not a divisor of a[i]
        if ($a[$i] % $cur != 0)
            return $cur;
    }

    return 0;
}

// Driver code
$a = array( 12, 6, 18, 12, 16 );

$n = sizeof($a);

echo getDivisor($a, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// divisor of all except for exactly
// one element in an array.

// Recursive function to return gcd of a and b
function __gcd(a, b)
{

    // Everything divides 0 
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a-b, b);
    return __gcd(a, b-a);
}

// Function that returns the divisor of all
// except for exactly one element in an array.
function getDivisor(a, n)
{
    // There's only one element in the array
    if (n == 1)
        return (a[0] + 1);

    var P = new Array(n);
    var S = new Array(n);

    // Creating prefix array of GCD
    P[0] = a[0];
    for(var i = 1; i < n; i++)
        P[i] = __gcd(a[i], P[i - 1]);

    // Creating suffix array of GCD
    S[n-1] = a[n-1];
    for (var i = n - 2; i >= 0; i--)
        S[i] = __gcd(S[i + 1], a[i]);

    // Iterate through the array
    for (var i = 0; i < n; i++) {

        // Variable to store the divisor
        var cur;

        // Getting the divisor
        if (i == 0)
            cur = S[i + 1];
        else if (i == n - 1)
            cur = P[i - 1];
        else
            cur = __gcd(P[i - 1], S[i + 1]);

        // Check if it is not a divisor of a[i]
        if (a[i] % cur != 0)
            return cur;
    }

    return 0;
}

// Driver Code
var a = [ 12, 6, 18, 12, 16 ];
var n = a.length;

document.write(getDivisor(a, n));

// This code is contributed by kirti

</script>
```

**Output:** 

```
6
```