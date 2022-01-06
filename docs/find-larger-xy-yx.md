# 找到 x^y 和 y^x 中较大的一个

> 原文:[https://www.geeksforgeeks.org/find-larger-xy-yx/](https://www.geeksforgeeks.org/find-larger-xy-yx/)

给定两个整数 x 和 y，找出 X^Y 和 Y^X 中较大的一个，或者确定它们是否相等。

**示例:**

```
Input : 2 3
Output : 3^2
We know 3^2 = 9 and 2^3 = 8.

Input : 2 4
Output : Equal
```

一个简单的解决方案是通过循环 y 次来计算 x^y，但是如果 x 和 y 的值太大，就会导致溢出。
为了解决溢出问题，我们可以通过取对数来简化方程。
log(x^y) = y* log(x)
现在，这个等式不会引起溢出，我们可以直接比较两个值。

## C++

```
// C++ program to print greater of x^y and
// y^x
#include <bits/stdc++.h>
using namespace std;

void printGreater(double x, double y)
{
    long double X = y * log(x);
    long double Y = x * log(y);
    if (abs(X - Y) < 1e-9) {
        cout << "Equal";
    }
    else if (X > Y) {
        cout << x << "^" << y;
    }
    else {
        cout << y << "^" << x;
    }
}

int main()
{
    double x = 5, y = 8;
    printGreater(x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// greater of x^y and y^x
import java.io.*;

class GFG
{
static void printGreater(int x,
                         int y)
{
    double X = y * Math.log(x);
    double Y = x * Math.log(y);
    if (Math.abs(X - Y) < 1e-9)
    {
        System.out.println("Equal");
    }
    else if (X > Y)
    {
        System.out.println(x + "^" + y);
    }
    else
    {
        System.out.println(y + "^" + x);
    }
}

// Driver Code
public static void main (String[] args)
{
    int x = 5, y = 8;
    printGreater(x, y);
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to print greater
# of x^y and y^x
import math

def printGreater(x, y):

    X = y * math.log(x);
    Y = x * math.log(y);
    if (abs(X - Y) < 1e-9):
        print("Equal");
    elif (X > Y):
        print(x, "^", y);
    else:
        print(y, "^", x);

# Driver Code
x = 5;
y = 8;
printGreater(x, y);

# This code is contributed by mits
```

## C#

```
// C# program to print
// greater of x^y and y^x
using System;

class GFG
{
static void printGreater(int x,
                          int y)
{
    double X = y * Math.Log(x);
    double Y = x * Math.Log(y);
    if (Math.Abs(X - Y) < 1e-9)
    {
        Console.WriteLine("Equal");
    }
    else if (X > Y)
    {
        Console.WriteLine(x +
                          "^" + y);
    }
    else
    {
        Console.WriteLine(y +
                          "^" + x);
    }
}

// Driver Code
public static void Main ()
{
    int x = 5, y = 8;
    printGreater(x, y);
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print greater
// of x^y and y^x
function printGreater($x, $y)
{
    $X = $y * log($x);
    $Y = $x * log($y);
    if (abs($X - $Y) < 1e-9)
    {
        echo "Equal";
    }
    else if ($X > $Y)
    {
        echo $x . "^" . $y;
    }
    else
    {
        echo $y . "^" . $x;
    }
}

// Driver Code
$x = 5;
$y = 8;
printGreater($x, $y);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to print greater of x^y and
// y^x

function printGreater(x, y)
{
    let X = y * Math.log(x);
    let Y = x * Math.log(y);
    if (Math.abs(X - Y) < 1e-9) {
        document.write("Equal");
    }
    else if (X > Y) {
        document.write(x + "^" + y);
    }
    else {
        document.write(y + "^" + x);
    }
}

// Driver Code

let x = 5, y = 8;
printGreater(x, y);

</script>
```

**Output:** 

```
5^8
```