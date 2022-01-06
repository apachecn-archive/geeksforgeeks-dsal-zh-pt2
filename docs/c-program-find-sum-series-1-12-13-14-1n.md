# 求数列 1 + 1/2 + 1/3 + 1/4 +和的程序..+ 1/n

> 原文:[https://www . geesforgeks . org/c-program-find-sum-series-1-12-13-14-1n/](https://www.geeksforgeeks.org/c-program-find-sum-series-1-12-13-14-1n/)

如果一个序列的逆遵循算术级数的规律，那么它被称为调和级数。一般来说，调和级数中的项可以表示为:1/a，1/(a + d)，1/(a + 2d)，1/(a + 3d) …。1/(a + nd)。
由于 AP 的第 n 项给出为(a+(n–1)d)。因此，调和级数的第 n 项是 AP 的第 n 项的倒数，即:1/(a+(n–1)d)
其中“a”是 AP 的第 1 项，“d”是共同的区别。
我们可以用 for 循环来求和。

## C++

```
// C++ program to find sum of series
#include <iostream>
using namespace std;

// Function to return sum of
// 1/1 + 1/2 + 1/3 + ..+ 1/n
class gfg
{

public : double sum(int n)
{
    double i, s = 0.0;
    for (i = 1; i <= n; i++)
    s = s + 1/i;
    return s;
}
};

// Driver code
int main()
{
    gfg g;
    int n = 5;
    cout << "Sum is " << g.sum(n);
    return 0;
}

// This code is contributed by SoM15242.
```

## C

```
// C program to find sum of series
#include <stdio.h>

// Function to return sum of 1/1 + 1/2 + 1/3 + ..+ 1/n
double sum(int n)
{
  double i, s = 0.0;
  for (i = 1; i <= n; i++)
      s = s + 1/i;
  return s;
}

int main()
{
    int n = 5;
    printf("Sum is %f", sum(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of series
import java.io.*;

class GFG {

    // Function to return sum of
    // 1/1 + 1/2 + 1/3 + ..+ 1/n
    static double sum(int n)
    {
      double i, s = 0.0;
      for (i = 1; i <= n; i++)
          s = s + 1/i;
      return s;
    }

    // Driven Program
    public static void main(String args[])
    {
        int n = 5;
        System.out.printf("Sum is %f", sum(n));

    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python program to find the sum of series

def sum(n):
    i = 1
    s = 0.0
    for i in range(1, n+1):
        s = s + 1/i;
    return s;

# Driver Code
n = 5
print("Sum is", round(sum(n), 6))

# This code is contributed by Chinmoy Lenka
```

## C#

```
// C# Program to find sum of series
using System;

class GFG {

    // Function to return sum of
    // 1/1 + 1/2 + 1/3 + ..+ 1/n
    static float sum(int n)
    {
        double i, s = 0.0;

        for (i = 1; i <= n; i++)
            s = s + 1/i;

        return (float)s;
    }

    // Driven Program
    public static void Main()
    {
        int n = 5;

        Console.WriteLine("Sum is "
                           + sum(n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of series

// Function to return sum of
// 1/1 + 1/2 + 1/3 + ..+ 1/n
function sum( $n)
{
    $i;
    $s = 0.0;
    for ($i = 1; $i <= $n; $i++)
        $s = $s + 1 / $i;
    return $s;
}

    // Driver Code
    $n = 5;
    echo("Sum is ");
    echo(sum($n));

//This code is contributed by vt_m
?>
```

## java 描述语言

```
<script>
// javascript Program to find sum of series

// Function to return sum of
// 1/1 + 1/2 + 1/3 + ..+ 1/n
function sum(n)
{
  var i, s = 0.0;
  for (i = 1; i <= n; i++)
      s = s + 1/i;
  return s;
}

// Driven Program
var n = 5;
document.write(sum(n).toFixed(5));

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
2.283333
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*