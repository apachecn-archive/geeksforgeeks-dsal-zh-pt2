# 给定繁殖率

n 秒后计数 a、b & c

> 原文:[https://www . geesforgeks . org/给定再现速率 n 秒后的 a-b-c 计数/](https://www.geeksforgeeks.org/count-of-a-b-c-after-n-seconds-for-given-reproduction-rate/)

给定三个不同的字母**‘a’**、**‘b’**和**‘c’**，并遵循一定的规则，即每隔 **2 秒**后每**‘a’**变为 a**‘b’**，每隔 **5 秒**后每**‘b’**变为 1**‘c’**，每隔 **12 秒**
从一个**‘a’**开始，任务是给 **n 秒**后，找到 **a** 、 **b** 和 **c** 的最终计数。
**例:**

> **输入:** n = 2
> **输出:** a = 0，b = 1，c = 0
> 最初 a = 1，b = 0，c = 0
> 在 n = 1 时，什么都不会改变
> 在 n = 2 时，所有 a 都会变成 b，即 a = 0，b = 1，c = 0
> **输入:** n = 72
> **输出:** a = 64，b = 0

**进场:**可以观察到，a、b、c 的值每 60 秒(即 2、5、12 的 LCM)后会形成一个图案，如下:

*   n = 60 时-> a = 32 <sup>1</sup> ，b = 0，c = 0
*   n = 120 时-> a = 32 <sup>2</sup> ，b = 0，c = 0
*   在 n = 180 -> a = 32 <sup>3</sup> ，b = 0，c = 0 等等。

如果 **n** 是 **60** 的倍数，则计算上述观察的结果，否则计算离 **n** 最近的 **60** 的倍数的结果，说 **x** ，然后更新从 **x + 1** 到 **n** 的秒数的结果。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ull unsigned long long

// Function to print the count of
// a, b and c after n seconds
void findCount(int n)
{
    ull a = 1, b = 0, c = 0;

    // Number of multiples of 60 below n
    int x = n / 60;
    a = (ull)pow(32, x);

    // Multiple of 60 nearest to n
    x = 60 * x;

    for (int i = x + 1; i <= n; i++) {

        // Change all a to b
        if (i % 2 == 0) {
            b += a;
            a = 0;
        }

        // Change all b to c
        if (i % 5 == 0) {
            c += b;
            b = 0;
        }

        // Change each c to two a
        if (i % 12 == 0) {
            a += (2 * c);
            c = 0;
        }
    }

    // Print the updated values of a, b and c
    cout << "a = " << a << ", ";
    cout << "b = " << b << ", ";
    cout << "c = " << c;
}

// Driver code
int main()
{
    int n = 72;
    findCount(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to print the count of
// a, b and c after n seconds
static void findCount(int n)
{
    long a = 1, b = 0, c = 0;

    // Number of multiples of 60 below n
    int x = n / 60;
    a = (long)Math.pow(32, x);

    // Multiple of 60 nearest to n
    x = 60 * x;

    for (int i = x + 1; i <= n; i++)
    {

        // Change all a to b
        if (i % 2 == 0)
        {
            b += a;
            a = 0;
        }

        // Change all b to c
        if (i % 5 == 0)
        {
            c += b;
            b = 0;
        }

        // Change each c to two a
        if (i % 12 == 0)
        {
            a += (2 * c);
            c = 0;
        }
    }

    // Print the updated values of a, b and c
    System.out.println("a = " + a + ", b = " +
                           b + ", c = " + c);
}

// Driver code
public static void main (String[] args)
{
    int n = 72;
    findCount(n);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the count of
# a, b and c after n seconds
import math
def findCount(n):
    a, b, c = 1, 0, 0;

    # Number of multiples of 60 below n
    x = (int)(n / 60);
    a = int(math.pow(32, x));

    # Multiple of 60 nearest to n
    x = 60 * x;

    for i in range(x + 1, n + 1):

        # Change all a to b
        if (i % 2 == 0):
            b += a;
            a = 0;

        # Change all b to c
        if (i % 5 == 0):
            c += b;
            b = 0;

        # Change each c to two a
        if (i % 12 == 0):
            a += (2 * c);
            c = 0;

    # Print the updated values of a, b and c
    print("a =", a, end = ", ");
    print("b =", b, end = ", ");
    print("c =", c);

# Driver code
if __name__ == '__main__':
    n = 72;
    findCount(n);

# This code is contributed
# by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the count of
// a, b and c after n seconds
static void findCount(int n)
{
    long a = 1, b = 0, c = 0;

    // Number of multiples of 60 below n
    int x = n / 60;
    a = (long)Math.Pow(32, x);

    // Multiple of 60 nearest to n
    x = 60 * x;

    for (int i = x + 1; i <= n; i++)
    {

        // Change all a to b
        if (i % 2 == 0)
        {
            b += a;
            a = 0;
        }

        // Change all b to c
        if (i % 5 == 0)
        {
            c += b;
            b = 0;
        }

        // Change each c to two a
        if (i % 12 == 0)
        {
            a += (2 * c);
            c = 0;
        }
    }

    // Print the updated values of a, b and c
    Console.WriteLine("a = " + a + ", b = " + b + ", c = " + c);
}

// Driver code
static void Main()
{
    int n = 72;
    findCount(n);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the count of
// a, b and c after n seconds
function findCount($n)
{
    $a = 1; $b = 0; $c = 0;

    // Number of multiples of 60 below n
    $x = $n / 60;
    $a = pow(32, $x);

    // Multiple of 60 nearest to n
    $x = 60 * $x;

    for ($i = $x + 1; $i <= $n; $i++)
    {

        // Change all a to b
        if ($i % 2 == 0)
        {
            $b += $a;
            $a = 0;
        }

        // Change all b to c
        if ($i % 5 == 0)
        {
            $c += $b;
            $b = 0;
        }

        // Change each c to two a
        if ($i % 12 == 0)
        {
            $a += (2 * $c);
            $c = 0;
        }
    }

    // Print the updated values of a, b and c
    echo("a = " . $a . ", b = " .
                  $b . ", c = " . $c);
}

// Driver code
$n = 72;
findCount($n);

// This code is contributed
// by Code_Mech.
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach   
// Function to print the count of
    // a, b and c after n seconds

    function findCount(n) {
        var a = 1, b = 0, c = 0;

        // Number of multiples of 60 below n
        var x = parseInt(n / 60);
        a =  Math.pow(32, x);

        // Multiple of 60 nearest to n
        x = 60 * x;

        for (i = x + 1; i <= n; i++) {

            // Change all a to b
            if (i % 2 == 0) {
                b += a;
                a = 0;
            }

            // Change all b to c
            if (i % 5 == 0) {
                c += b;
                b = 0;
            }

            // Change each c to two a
            if (i % 12 == 0) {
                a += (2 * c);
                c = 0;
            }
        }

        // Print the updated values of a, b and c
        document.write("a = " + a + ", b = " + b + ", c = " + c);
    }

    // Driver code

        var n = 72;
        findCount(n);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
a = 64, b = 0, c = 0
```