# 找到任何具有给定 GCD 和 LCM 的配对

> 原文:[https://www . geesforgeks . org/find-any-pair-with-given-gcd-and-LCM/](https://www.geeksforgeeks.org/find-any-pair-with-given-gcd-and-lcm/)

给定 gcd G 和 lcm L。任务是打印任何具有 gcd G 和 lcm L 的配对。
**示例:**

```
Input: G = 3, L = 12 
Output: 3, 12

Input: G = 1, L = 10 
Output: 1, 10
```

一个**正常解**将对 g*l 的所有因子对进行迭代，并检查是否有任何一对将 gcd g 和 lcm 作为 l，如果有，则该对将是答案。
以下是上述办法的实施情况。

## C++

```
// C++ program to print any pair
// with a given gcd G and lcm L
#include <bits/stdc++.h>
using namespace std;

// Function to print the pairs
void printPair(int g, int l)
{
    int n = g * l;

    // iterate over all factor pairs
    for (int i = 1; i * i <= n; i++) {

        // check if a factor
        if (n % i == 0) {
            int first = i;
            int second = n / i;

            // find gcd
            int gcd = __gcd(first, second);

            // check if gcd is same as given g
            // and lcm is same as lcm l
            if (gcd == g && l % first == 0 && l % second == 0) {
                cout << first << " " << second;
                return;
            }
        }
    }
}

// Driver Code
int main()
{
    int g = 3, l = 12;
    printPair(g, l);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print any pair
// with a given gcd G and lcm L

import java.math.BigInteger;

class GFG {

// Function to print the pairs
    static void printPair(int g, int l) {
        int n = g * l;

        // iterate over all factor pairs
        for (int i = 1; i * i <= n; i++) {

            // check if a factor
            if (n % i == 0) {
                int first = i;
                int second = n / i;

                // find gcd
                int gcd = __gcd(first, second);

                // check if gcd is same as given g
                // and lcm is same as lcm l
                if (gcd == g && l % first == 0 && l % second == 0) {
                    System.out.println(first + " " + second);
                    return;
                }
            }
        }
    }
//Function return GCD of two give number

    private static int __gcd(int a, int b) {
        // there's a better way to do this. I forget.
        BigInteger b1 = new BigInteger("" + a);
        BigInteger b2 = new BigInteger("" + b);
        BigInteger gcd = b1.gcd(b2);
        return gcd.intValue();
    }
// Driver function

    public static void main(String[] args) {
        int g = 3, l = 12;
        printPair(g, l);

    }
}
// This code is contributed by RAJPUT-JI
```

## 蟒蛇 3

```
# Python program to print any pair
# with a given gcd G and lcm L

# Function to print the pairs
def printPair(g, l):
    n = g * l;

    # iterate over all factor pairs
    for i in range(1,n+1):

        # check if a factor
        if (n % i == 0):
            first = i;
            second = n // i;

            # find gcd
            gcd = __gcd(first, second);

            # check if gcd is same as given g
            # and lcm is same as lcm l
            if (gcd == g and l % first == 0 and
                              l % second == 0):
                print(first , " " , second);
                return;

# Function return GCD of two give number
def __gcd(a, b):
    if(b==0):
        return a;
    else:
        return __gcd(b, a % b);

# Driver Code
g = 3;
l = 12;
printPair(g, l);

# This code is contributed by Princi Singh
```

## C#

```
// C# program to print any pair
// with a given gcd G and lcm L
using System;
public class GFG {

// Function to print the pairs
    static void printPair(int g, int l) {
        int n = g * l;

        // iterate over all factor pairs
        for (int i = 1; i * i <= n; i++) {

            // check if a factor
            if (n % i == 0) {
                int first = i;
                int second = n / i;

                // find gcd
                int gcd = __gcd(first, second);

                // check if gcd is same as given g
                // and lcm is same as lcm l
                if (gcd == g && l % first == 0 && l % second == 0) {
                    Console.WriteLine(first + " " + second);
                    return;
                }
            }
        }
    }
//Function return GCD of two give number

    private static int __gcd(int a, int b) {
        return b == 0 ? a : __gcd(b, a % b);
    }
// Driver function

    public static void Main() {
        int g = 3, l = 12;
        printPair(g, l);

    }
}

// This code is contributed by RAJPUT-JI
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print any pair
// with a given gcd G and lcm L

// Function to print the pairs
function printPair($g, $l)
{
    $n = $g * $l;

    // iterate over all factor pairs
    for ($i = 1; $i * $i <= $n; $i++)
    {

        // check if a factor
        if ($n % $i == 0)
        {
            $first = $i;
            $second = (int)$n / $i;

            // find gcd
            $gcd = __gcd($first, $second);

            // check if gcd is same as given g
            // and lcm is same as lcm l
            if ($gcd == $g && $l % $first == 0 &&
                              $l % $second == 0)
            {
                echo $first , " " , $second;
                return;
            }
        }
    }
}

// Function return GCD of two give number
function __gcd($a, $b)
{
    return $b == 0 ? $a : __gcd($b, $a % $b);
}

// Driver Code
$g = 3;
$l = 12;
printPair($g, $l);

// This code is contributed by ajit
```

## java 描述语言

```
<script>
// javascript program to print any pair
// with a given gcd G and lcm L

    // Function to print the pairs
    function printPair(g , l) {
        var n = g * l;

        // iterate over all factor pairs
        for (i = 1; i * i <= n; i++) {

            // check if a factor
            if (n % i == 0) {
                var first = i;
                var second = n / i;

                // find gcd
                var gcd = __gcd(first, second);

                // check if gcd is same as given g
                // and lcm is same as lcm l
                if (gcd == g && l % first == 0 && l % second == 0) {
                    document.write(first + " " + second);
                    return;
                }
            }
        }
    }

// Function return GCD of two give number
    function __gcd(a, b)
{
    return b == 0 ? a : __gcd(b, a % b);
}
    // Driver function
        var g = 3, l = 12;
        printPair(g, l);

// This code is contributed by aashish1995
</script>
```

**输出:**

```
3 12
```

**时间复杂度:** O(sqrt(g*l))
一个**有效的解决方案**将是观察 lcm 总是被 gcd 整除，因此答案可以在 O(1)中得到。其中一个数字是 gcd G 本身，另一个是 lcm L.
下面是上述方法的实现。

## C++

```
// C++ program to print any pair
// with a given gcd G and lcm L
#include <iostream>
using namespace std;

// Function to print the pairs
void printPair(int g, int l)
{
    cout << g << " " << l;
}

// Driver Code
int main()
{
    int g = 3, l = 12;
    printPair(g, l);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print any pair
// with a given gcd G and lcm L

import java.io.*;

class GFG {

// Function to print the pairs
 static void printPair(int g, int l)
{
    System.out.print( g + " " + l);
}

// Driver Code
    public static void main (String[] args) {
    int g = 3, l = 12;
    printPair(g, l);
    }
}
// This code is contributed by inder_verma.
```

## 蟒蛇 3

```
# Python 3 program to print any pair
# with a given gcd G and lcm L

# Function to print the pairs
def printPair(g, l):
    print(g, l)

# Driver Code
g = 3; l = 12;
printPair(g, l);

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# program to print any pair
// with a given gcd G and lcm L
using System;

class GFG
{

// Function to print the pairs
static void printPair(int g, int l)
{
    Console.Write( g + " " + l);
}

// Driver Code
public static void Main ()
{
    int g = 3, l = 12;
    printPair(g, l);
}
}

// This code is contributed
// by Subhadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print any pair
// with a given gcd G and lcm L

// Function to print the pairs
function printPair($g, $l)
{
    echo $g ;
    echo (" ");
    echo $l;
}

// Driver Code
$g = 3;
$l = 12;
printPair($g, $l);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// javascript program to print any pair
// with a given gcd G and lcm L
// Function to print the pairs
    function printPair(g, l)
    {
        document.write(g + " " + l);
    }

    // Driver Code
        var g = 3, l = 12;
        printPair(g, l);

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
3 12
```

**时间复杂度:** O(1)