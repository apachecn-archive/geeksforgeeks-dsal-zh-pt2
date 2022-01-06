# 求解微分方程的欧拉方法

> 原文:[https://www . geesforgeks . org/欧拉-方法-求解-微分-方程/](https://www.geeksforgeeks.org/euler-method-solving-differential-equation/)

给定初始条件为 y(x0) = y0 的微分方程 dy/dx = f(x，y)。使用[欧拉法](https://en.wikipedia.org/wiki/Euler_method)求其近似解。
**欧拉方法:**
在数学和计算科学中，欧拉方法(也称为正向
欧拉方法)是求解具有给定初始值的常微分
方程的一阶数值程序。
考虑一个微分方程 dy/dx = f(x，y ),初始条件 y(x0)=y0
则该方程的逐次逼近式可由下式给出:

> **y(n+1) = y(n) + h * f(x(n)，y(n))**
> 其中 h =(x(n)–x(0))/n
> h 表示步长。选择较小的 h
> 值会导致更精确的结果
> 和更多的计算时间。

**例:**

```
    Consider below differential equation
            dy/dx = (x + y + xy)
    with initial condition y(0) = 1 
    and step size h = 0.025.
    Find y(0.1).

    Solution:
    f(x, y) = (x + y + xy)
    x0 = 0, y0 = 1, h = 0.025
    Now we can calculate y1 using Euler formula
    y1 = y0 + h * f(x0, y0)
    y1 = 1 + 0.025 *(0 + 1 + 0 * 1)
    y1 = 1.025
    y(0.025) = 1.025.
    Similarly we can calculate y(0.050), y(0.075), ....y(0.1).
    y(0.1) = 1.11167
```

## C++

```
/* CPP  Program to find approximation
   of a ordinary differential equation
   using euler method.*/
#include <iostream>
using namespace std;

// Consider a differential equation
// dy/dx=(x + y + xy)
float func(float x, float y)
{
    return (x + y + x * y);
}

// Function for Euler formula
void euler(float x0, float y, float h, float x)
{
    float temp = -0;

    // Iterating till the point at which we
    // need approximation
    while (x0 < x) {
        temp = y;
        y = y + h * func(x0, y);
        x0 = x0 + h;
    }

    // Printing approximation
    cout << "Approximate solution at x = "
         << x << "  is  " << y << endl;
}

// Driver program
int main()
{
    // Initial Values
    float x0 = 0;
    float y0 = 1;
    float h = 0.025;

    // Value of x at which we need approximation
    float x = 0.1;

    euler(x0, y0, h, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find approximation of an ordinary
// differential equation using euler method
import java.io.*;

class Euler {
    // Consider a differential equation
    // dy/dx=(x + y + xy)
    float func(float x, float y)
    {
        return (x + y + x * y);
    }

    // Function for Euler formula
    void euler(float x0, float y, float h, float x)
    {
        float temp = -0;

        // Iterating till the point at which we
        // need approximation
        while (x0 < x) {
            temp = y;
            y = y + h * func(x0, y);
            x0 = x0 + h;
        }

        // Printing approximation
        System.out.println("Approximate solution at x = "
                           + x + " is " + y);
    }

    // Driver program
    public static void main(String args[]) throws IOException
    {
        Euler obj = new Euler();
        // Initial Values
        float x0 = 0;
        float y0 = 1;
        float h = 0.025f;

        // Value of x at which we need approximation
        float x = 0.1f;

        obj.euler(x0, y0, h, x);
    }
}

// This code is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# Python Code to find approximation
# of a ordinary differential equation
# using euler method.

# Consider a differential equation
# dy / dx =(x + y + xy)
def func( x, y ):
    return (x + y + x * y)

# Function for euler formula
def euler( x0, y, h, x ):
    temp = -0

    # Iterating till the point at which we
    # need approximation
    while x0 < x:
        temp = y
        y = y + h * func(x0, y)
        x0 = x0 + h

    # Printing approximation
    print("Approximate solution at x = ", x, " is ", "%.6f"% y)

# Driver Code
# Initial Values
x0 = 0
y0 = 1
h = 0.025

# Value of x at which we need approximation
x = 0.1

euler(x0, y0, h, x)
```

## C#

```
// C# program to find approximation of an ordinary
// differential equation using euler method
using System;

class GFG {

    // Consider a differential equation
    // dy/dx=(x + y + xy)
    static float func(float x, float y)
    {
        return (x + y + x * y);
    }

    // Function for Euler formula
    static void euler(float x0, float y, float h, float x)
    {

        // Iterating till the point at which we
        // need approximation
        while (x0 < x) {
            y = y + h * func(x0, y);
            x0 = x0 + h;
        }

        // Printing approximation
        Console.WriteLine("Approximate solution at x = "
                          + x + " is " + y);
    }

    // Driver program
    public static void Main()
    {

        // Initial Values
        float x0 = 0;
        float y0 = 1;
        float h = 0.025f;

        // Value of x at which we need
        // approximation
        float x = 0.1f;

        euler(x0, y0, h, x);
    }
}

// This code is contributed by Vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find approximation
// of a ordinary differential equation
// using euler method

// Consider a differential equation
// dy/dx=(x + y + xy)

function func($x, $y)
{
    return ($x + $y + $x * $y);
}

// Function for Euler formula
function euler( $x0, $y, $h, $x)
{
    $temp = -0;

    // Iterating till the point
    // at which we need approximation
    while($x0 < $x)
    {
        $temp = $y;
        $y = $y + $h * func($x0, $y);
        $x0 = $x0 + $h;
    }

    // Printing approximation
    echo "Approximate solution at x = ",
        $x, " is ", $y, "\n";
}

// Driver Code

// Initial Values
$x0 = 0;
$y0 = 1;
$h = 0.025;

// Value of x at which
// we need approximation
$x = 0.1;

euler($x0, $y0, $h, $x);

// This code contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to find approximation of an ordinary
// differential equation using euler method

   // Consider a differential equation
    // dy/dx=(x + y + xy)
    function func(x, y)
    {
        return (x + y + x * y);
    }

    // Function for Euler formula
    function euler(x0, y, h, x)
    {
        let temp = -0;

        // Iterating till the point at which we
        // need approximation
        while (x0 < x) {
            temp = y;
            y = y + h * func(x0, y);
            x0 = x0 + h;
        }

        // Printing approximation
        document.write("Approximate solution at x = "
                           + x + " is " + y);
    }

// Driver Code

    // Initial Values
    let x0 = 0;
    let y0 = 1;
    let h = 0.025;

    // Value of x at which we need approximation
    let x = 0.1;

    euler(x0, y0, h, x);

// This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
Approximate solution at x = 0.1  is  1.11167
```