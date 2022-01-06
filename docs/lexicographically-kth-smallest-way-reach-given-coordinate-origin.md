# 从原点到达给定坐标的字典上最小的方法

> 原文:[https://www . geesforgeks . org/词典学-kth-最小路-到达-给定-坐标-原点/](https://www.geeksforgeeks.org/lexicographically-kth-smallest-way-reach-given-coordinate-origin/)

给定 2D 平面上的坐标 **(x，y)** 。我们必须从原点即(0，0)的当前位置到达(x，y)。在每一步中，我们可以在平面上垂直或水平移动。当水平移动每一步时，我们写“H”，当垂直移动每一步时，我们写“V”。因此，可能有许多包含‘H’和‘V’的字符串，它们代表从(0，0)到(x，y)的路径。任务是在所有可能的字符串中找到字典上最小的 Kt 字符串。
**例:**

> 输入:x = 2，y = 2，k = 2
> 输出:HVVH
> **说明:**从(0，0)到(2，2)有 6 种方式。按字典顺序排序的字符串的可能列表:[“HHVV”、“hvhvhv”、“HVVH”、“VHHV”、“VHVH”、“VVHH”]。因此，从词典学角度来说，第二小的字符串是 hvhvhv。
> 输入:x = 2，y = 2，k = 3
> 输出:VHHV

**先决条件:** [从原点到达一个点的方法](https://www.geeksforgeeks.org/counts-paths-point-reach-origin/)
**方法:**想法是用递归来解决问题。从原点到达(x，y)的途径数为 <sup>x + y</sup> C <sub>x</sub> 。
现在观察，从(1，0)到达(x，y)的途径数将是(x+y–1，x–1)，因为我们已经在水平方向上迈出了一步，所以从 x 中减去 1。同样，从(0，1)到达(x，y)的途径数将是(x+y–1，y–1)，因为我们已经在垂直方向上迈出了一步， 所以从 y 中减去 1。因为“H”在字典上比“V”小，所以在所有字符串中，起始字符串将在开头包含“H”，即初始移动将是水平的。
所以，如果 K<=<sup>x+y–1</sup>C<sub>x–1</sub>，我们将把‘H’作为第一步，否则我们将把‘V’作为第一步，求解从(1，0)到(x，y)的进路数将是 K = K–<sup>x+y–1</sup>C<sub>x–1</sub>。
以下是本办法的实施情况:

## C++

```
// CPP Program to find Lexicographically Kth
// smallest way to reach given coordinate from origin
#include <bits/stdc++.h>
using namespace std;

// Return (a+b)!/a!b!
int factorial(int a, int b)
{
    int res = 1;

    // finding (a+b)!
    for (int i = 1; i <= (a + b); i++)
        res = res * i;

    // finding (a+b)!/a!
    for (int i = 1; i <= a; i++)
        res = res / i;

    // finding (a+b)!/b!
    for (int i = 1; i <= b; i++)
        res = res / i;

    return res;
}

// Return the Kth smallest way to reach given coordinate from origin
void Ksmallest(int x, int y, int k)
{
    // if at origin
    if (x == 0 && y == 0)
        return;

    // if on y-axis
    else if (x == 0) {
        // decrement y.
        y--;

        // Move vertical
        cout << "V";

        // recursive call to take next step.
        Ksmallest(x, y, k);
    }

    // If on x-axis
    else if (y == 0) {
        // decrement x.
        x--;

        // Move horizontal.
        cout << "H";

        // recursive call to take next step.
        Ksmallest(x, y, k);
    }
    else {
        // If x + y C x is greater than K
        if (factorial(x - 1, y) > k) {
            // Move Horizontal
            cout << "H";

            // recursive call to take next step.
            Ksmallest(x - 1, y, k);
        }
        else {
            // Move vertical
            cout << "V";

            // recursive call to take next step.
            Ksmallest(x, y - 1, k - factorial(x - 1, y));
        }
    }
}

// Driven Program
int main()
{
    int x = 2, y = 2, k = 2;

    Ksmallest(x, y, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find
// Lexicographically Kth
// smallest way to reach
// given coordinate from origin
import java.io.*;

class GFG
{

// Return (a+b)!/a!b!
static int factorial(int a,
                     int b)
{
    int res = 1;

    // finding (a+b)!
    for (int i = 1;
             i <= (a + b); i++)
        res = res * i;

    // finding (a+b)!/a!
    for (int i = 1; i <= a; i++)
        res = res / i;

    // finding (a+b)!/b!
    for (int i = 1; i <= b; i++)
        res = res / i;

    return res;
}

// Return the Kth smallest
// way to reach given
// coordinate from origin
static void Ksmallest(int x,
                      int y, int k)
{
    // if at origin
    if (x == 0 && y == 0)
        return;

    // if on y-axis
    else if (x == 0)
    {
        // decrement y.
        y--;

        // Move vertical
        System.out.print("V");

        // recursive call to
        // take next step.
        Ksmallest(x, y, k);
    }

    // If on x-axis
    else if (y == 0)
    {
        // decrement x.
        x--;

        // Move horizontal.
        System.out.print("H");

        // recursive call to
        // take next step.
        Ksmallest(x, y, k);
    }
    else
    {
        // If x + y C x is
        // greater than K
        if (factorial(x - 1, y) > k)
        {
            // Move Horizontal
            System.out.print( "H");

            // recursive call to
            // take next step.
            Ksmallest(x - 1, y, k);
        }
        else
        {
            // Move vertical
            System.out.print("V");

            // recursive call to
            // take next step.
            Ksmallest(x, y - 1, k -
            factorial(x - 1, y));
        }
    }
}

// Driver Code
public static void main (String[] args)
{
    int x = 2, y = 2, k = 2;

    Ksmallest(x, y, k);
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 Program to find Lexicographically Kth
# smallest way to reach given coordinate from origin

# Return (a+b)!/a!b!
def factorial(a, b):

    res = 1

    # finding (a+b)!
    for i in range(1, a + b + 1):
        res = res * i

    # finding (a+b)!/a!
    for i in range(1, a + 1):
        res = res // i

    # finding (a+b)!/b!
    for i in range(1, b + 1):
        res = res // i

    return res

# Return the Kth smallest way to reach
# given coordinate from origin
def Ksmallest(x, y, k):

    # if at origin
    if x == 0 and y == 0:
        return

    # if on y-axis
    elif x == 0:
        # decrement y.
        y -= 1

        # Move vertical
        print("V", end = "")

        # recursive call to take next step.
        Ksmallest(x, y, k)

    # If on x-axis
    elif y == 0:

        # decrement x.
        x -= 1

        # Move horizontal.
        print("H", end = "")

        # recursive call to take next step.
        Ksmallest(x, y, k)

    else:

        # If x + y C x is greater than K
        if factorial(x - 1, y) > k:

            # Move Horizontal
            print("H", end = "")

            # recursive call to take next step.
            Ksmallest(x - 1, y, k)

        else:

            # Move vertical
            print("V", end = "")

            # recursive call to take next step.
            Ksmallest(x, y - 1, k - factorial(x - 1, y))

# Driver Code
if __name__ == "__main__":

    x, y, k = 2, 2, 2
    Ksmallest(x, y, k)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# Program to find
// Lexicographically Kth
// smallest way to reach
// given coordinate from origin
using System;

class GFG
{

// Return (a+b)!/a!b!
static int factorial(int a,
                    int b)
{
    int res = 1;

    // finding (a+b)!
    for (int i = 1;
            i <= (a + b); i++)
        res = res * i;

    // finding (a+b)!/a!
    for (int i = 1; i <= a; i++)
        res = res / i;

    // finding (a+b)!/b!
    for (int i = 1; i <= b; i++)
        res = res / i;

    return res;
}

// Return the Kth smallest
// way to reach given
// coordinate from origin
static void Ksmallest(int x,
                    int y, int k)
{
    // if at origin
    if (x == 0 && y == 0)
        return;

    // if on y-axis
    else if (x == 0)
    {
        // decrement y.
        y--;

        // Move vertical
        Console.Write("V");

        // recursive call to
        // take next step.
        Ksmallest(x, y, k);
    }

    // If on x-axis
    else if (y == 0)
    {
        // decrement x.
        x--;

        // Move horizontal.
        Console.Write("H");

        // recursive call to
        // take next step.
        Ksmallest(x, y, k);
    }
    else
    {
        // If x + y C x is
        // greater than K
        if (factorial(x - 1, y) > k)
        {
            // Move Horizontal
            Console.Write( "H");

            // recursive call to
            // take next step.
            Ksmallest(x - 1, y, k);
        }
        else
        {
            // Move vertical
            Console.Write("V");

            // recursive call to
            // take next step.
            Ksmallest(x, y - 1, k -
            factorial(x - 1, y));
        }
    }
}

// Driver Code
public static void Main (String[] args)
{
    int x = 2, y = 2, k = 2;

    Ksmallest(x, y, k);
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find Lexicographically Kth
// smallest way to reach given coordinate from origin

// Return (a+b)!/a!b!
function factorial($a, $b)
{
    $res = 1;

    // finding (a+b)!
    for ($i = 1; $i <= ($a + $b); $i++)
        $res = $res * $i;

    // finding (a+b)!/a!
    for ($i = 1; $i <= $a; $i++)
        $res = $res / $i;

    // finding (a+b)!/b!
    for ($i = 1; $i <= $b; $i++)
        $res = $res / $i;

    return $res;
}

// Return the Kth smallest way to reach
// given coordinate from origin
function Ksmallest($x, $y, $k)
{
    // if at origin
    if ($x == 0 && $y == 0)
        return;

    // if on y-axis
    else if ($x == 0)
    {
        // decrement y.
        $y--;

        // Move vertical
        echo("V");

        // recursive call to
        // take next step.
        Ksmallest($x, $y, $k);
    }

    // If on x-axis
    else if ($y == 0)
    {
        // decrement x.
        $x--;

        // Move horizontal.
        echo("H");

        // recursive call to
        // take next step.
        Ksmallest($x, $y, $k);
    }
    else
    {
        // If x + y C x is
        // greater than K
        if (factorial($x - 1, $y) > $k)
        {
            // Move Horizontal
            echo("H");

            // recursive call to
            // take next step.
            Ksmallest($x - 1, $y, $k);
        }
        else
        {
            // Move vertical
            echo("V");

            // recursive call to
            // take next step.
            Ksmallest($x, $y - 1, $k -
            factorial($x - 1, $y));
        }
    }
}

// Driver Code
$x = 2; $y = 2;$k = 2;

Ksmallest($x, $y, $k);

// This code is contributed
// by Code_Mech.
?>
```

## java 描述语言

```
<script>

// Javascript Program to find Lexicographically Kth
// smallest way to reach given coordinate from origin

// Return (a+b)!/a!b!
function factorial(a, b)
{
    var res = 1;

    // finding (a+b)!
    for (var i = 1; i <= (a + b); i++)
        res = res * i;

    // finding (a+b)!/a!
    for (var i = 1; i <= a; i++)
        res = res / i;

    // finding (a+b)!/b!
    for (var i = 1; i <= b; i++)
        res = res / i;

    return res;
}

// Return the Kth smallest way to reach given coordinate from origin
function Ksmallest(x, y, k)
{
    // if at origin
    if (x == 0 && y == 0)
        return;

    // if on y-axis
    else if (x == 0) {
        // decrement y.
        y--;

        // Move vertical
        document.write( "V");

        // recursive call to take next step.
        Ksmallest(x, y, k);
    }

    // If on x-axis
    else if (y == 0) {
        // decrement x.
        x--;

        // Move horizontal.
        document.write( "H");

        // recursive call to take next step.
        Ksmallest(x, y, k);
    }
    else {
        // If x + y C x is greater than K
        if (factorial(x - 1, y) > k) {
            // Move Horizontal
            document.write( "H");

            // recursive call to take next step.
            Ksmallest(x - 1, y, k);
        }
        else {
            // Move vertical
            document.write( "V");

            // recursive call to take next step.
            Ksmallest(x, y - 1, k - factorial(x - 1, y));
        }
    }
}

// Driven Program
var x = 2, y = 2, k = 2;
Ksmallest(x, y, k);

// This code is contributed by rutvik_56.
</script>
```

**输出**T2】

```
HVVH
```