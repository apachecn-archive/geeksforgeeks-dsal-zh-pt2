# 用算术平均值和几何平均值求调和平均值

> 原文:[https://www . geesforgeks . org/find-harmonic-mean-use-算术平均-几何平均/](https://www.geeksforgeeks.org/find-harmonic-mean-using-arithmetic-mean-geometric-mean/)

给定两个数，首先计算这两个数的算术平均值和几何平均值。使用如此计算的算术平均值和几何平均值，找出两个数之间的调和平均值。

示例:

```
Input : a = 2
        b = 4
Output : 2.666

Input : a = 5
        b = 15
Output : 7.500
```

[算术平均值:](https://en.wikipedia.org/wiki/Arithmetic_mean)两个数字 a 和 b 之间的算术平均值‘AM’是这样一个数字:AM-a = b-AM。因此，如果给我们这两个数字，算术平均值 AM = 1/2(a+b)
[几何平均值:](https://en.wikipedia.org/wiki/Geometric_mean)两个数字 a 和 b 之间的几何平均值“GM”是这样一个数字，GM/a = b/GM。因此，如果我们给定这两个数字，两个数字 a 和 b 之间的几何平均 GM = sqrt(a*b)
[调和平均:](https://en.wikipedia.org/wiki/Harmonic_mean)调和平均“HM”是这样一个数字:1/HM–1/a = 1/b–1/HM。因此，如果给我们这两个数字，谐波平均值 HM = 2ab/a+b
现在，我们也知道![GM^2 = AM * HM  ](img/5069b43b945be37e4100910b59223dda.png "Rendered by QuickLaTeX.com")

## C++

```
// C++ implementation of compution of
// arithmetic mean, geometric mean
// and harmonic mean
#include <bits/stdc++.h>
using namespace std;

// Function to calculate arithmetic
// mean, geometric mean and harmonic mean
double compute(int a, int b)
{

    double AM, GM, HM;

    AM = (a + b) / 2;
    GM = sqrt(a * b);
    HM = (GM * GM) / AM;
    return HM;
}

// Driver function
int main()
{

    int a = 5, b = 15;
    double HM = compute(a, b);
    cout << "Harmonic Mean between " << a
          << " and " << b << " is " << HM ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of compution of
// arithmetic mean, geometric mean
// and harmonic mean
import java.io.*;

class GeeksforGeeks {

    // Function to calculate arithmetic
    // mean, geometric mean and harmonic mean
    static double compute(int a, int b)
    {

        double AM, GM, HM;

        AM = (a + b) / 2;
        GM = Math.sqrt(a * b);
        HM = (GM * GM) / AM;
        return HM;
    }

    // Driver function
    public static void main(String args[])
    {
        int a = 5, b = 15;
        double HM = compute(a, b);
        String str = "";
        str = str + HM;
        System.out.print("Harmonic Mean between " 
                         + a + " and " + b + " is " 
                         + str.substring(0, 5));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of compution
# of arithmetic mean, geometric mean
# and harmonic mean

import math

# Function to calculate arithmetic
# mean, geometric mean and harmonic mean
def compute( a, b) :
    AM = (a + b) / 2
    GM = math.sqrt(a * b)
    HM = (GM * GM) / AM
    return HM

# Driver function
a = 5
b = 15
HM = compute(a, b)
print("Harmonic Mean between " , a,
      " and ", b , " is " , HM )

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# implementation of compution of
// arithmetic mean, geometric mean
// and harmonic mean
using System;

class GeeksforGeeks {

    // Function to calculate arithmetic
    // mean, geometric mean and harmonic mean
    static double compute(int a, int b)
    {

        double AM, GM, HM;

        AM = (a + b) / 2;
        GM = Math.Sqrt(a * b);
        HM = (GM * GM) / AM;
        return HM;
    }

    // Driver function
    public static void Main()
    {
        int a = 5, b = 15;
        double HM = compute(a, b);
        Console.WriteLine("Harmonic Mean between "
                        + a + " and " + b + " is "
                        +HM);
    }
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of compution of
// arithmetic mean, geometric mean
// and harmonic mean

// Function to calculate arithmetic
// mean, geometric mean and harmonic mean
function compute( $a, $b)
{

    $AM;
    $GM;
    $HM;

    $AM = ($a + $b) / 2;
    $GM = sqrt($a * $b);
    $HM = ($GM * $GM) / $AM;
    return $HM;
}

// Driver Code
    $a = 5;
    $b = 15;
    $HM = compute($a, $b);
    echo"Harmonic Mean between " .$a.
        " and " .$b. " is " .$HM ;
    return 0;
// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of compution
// of arithmetic mean, geometric mean
// and harmonic mean

// Function to calculate arithmetic
// mean, geometric mean and harmonic mean
function compute(a, b)
{
    var AM = (a + b) / 2;
    var GM = Math.sqrt(a * b);
    var HM = (GM * GM) / AM;

    return HM;
}

// Driver Code
var a = 5;
var b = 15;
var HM = compute(a, b)

document.write("Harmonic Mean between " +
               a + " and " +  b  + " is " +
               HM.toFixed(3));

// This code is contributed by bunnyram19

</script>
```

**输出:**

```
Harmonic Mean between 5 and 15 is 7.500
```