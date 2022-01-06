# 均匀形状

> 原文:[https://www.geeksforgeeks.org/equable-shapes/](https://www.geeksforgeeks.org/equable-shapes/)

如果一个形状的面积等于它的周长，它就是均匀的。给定多边形的有序坐标，找出形状是否均匀。

**示例:**

```
Input : X[] = {0, 5, 0}
        Y[] = {0, 0, 12}
Output : Equable Shape

Input : X[] = {0, 4, 4, 0}
        Y[] = {0, 0, 4, 4}
Output : Equable Shape

Input: X[] = {0, 6, 6, 0}
       Y[] = {0, 0, 4, 4}
Output: Not Equable Shape
```

我们可以使用鞋带公式找到多边形的面积，该公式在给定 n 个有序顶点的多边形的面积中描述。我们也可以简单地通过增加相邻点之间的距离来找到它的周长。

## C++

```
// C++ program to find equable shape
#include <bits/stdc++.h>
using namespace std;

// To calculate area of polygon
double polygonArea(double X[], double Y[], int n)
{
    double area = 0.0;

    // Calculate value of area using shoelace
    // formula
    int j = n - 1;
    for (int i = 0; i < n; i++) {
        area += (X[j] + X[i]) * (Y[j] - Y[i]);
        j = i; // j is previous vertex to i
    }

    return abs(area / 2.0);
}

// To calculate perimeter of polygon
double polygonPerimeter(double X[], double Y[],
                                         int n)
{
    double perimeter = 0.0;

    // Calculate value of perimeter
    int j = n - 1;
    for (int i = 0; i < n; i++) {
        perimeter += sqrt((X[j] - X[i]) * (X[j] - X[i]) +
                          (Y[j] - Y[i]) * (Y[j] - Y[i]));
        j = i; // j is previous vertex to i
    }

    return perimeter;
}

// To find equable shape
void equableShape(double X[], double Y[], int n)
{
    // Find area and perimeter of polygon if
    // they are equal then it is equable shape
    if (polygonPerimeter(X, Y, n) == polygonArea(X, Y, n))
        cout << "Equable Shape";
    else
        cout << "Not Equable Shape";
}

// Driver program to test above function
int main()
{
    double X[] = { 0, 5, 0 };
    double Y[] = { 0, 0, 12 };

    int n = sizeof(X) / sizeof(X[0]);

    equableShape(X, Y, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find equable shape
class equable {

    // To calculate area of polygon
    static double polygonArea(double X[], double Y[], int n)
    {
        double area = 0.0;

        // Calculate value of area using shoelace formula
        int j = n - 1;
        for (int i = 0; i < n; i++) {
            area += (X[j] + X[i]) * (Y[j] - Y[i]);
            j = i; // j is previous vertex to i
        }

        return Math.abs(area / 2.0);
    }

    // To calculate perimeter of polygon
    static double polygonPerimeter(double X[], double Y[], int n)
    {
        double perimeter = 0.0;

        // Calculate value of perimeter
        int j = n - 1;
        for (int i = 0; i < n; i++) {
            perimeter += Math.sqrt((X[j] - X[i]) * (X[j] - X[i]) +
                                 (Y[j] - Y[i]) * (Y[j] - Y[i]));
            j = i; // j is previous vertex to i
        }

        return perimeter;
    }

    // To find equable shape
    static void equableShape(double X[], double Y[], int n)
    {
        // Find area and perimeter of polygon if
        // they are equal then it is equable shape
        if (polygonPerimeter(X, Y, n) == polygonArea(X, Y, n))
            System.out.println("Equable Shape");
        else
            System.out.println("Not Equable Shape");
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        double X[] = { 0, 5, 0 };
        double Y[] = { 0, 0, 12 };

        int n = X.length;

        equableShape(X, Y, n);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find equable shape
# To calculate area of polygon

import math
def polygonArea(X, Y, n):
    area = 0.0

    # Calculate value of area
    # using shoelace  formula
    j = n - 1
    for i in range(n):
        area += (X[j] + X[i]) * (Y[j] - Y[i])

        # j is previous vertex to i
        j = i 
    return abs(area / 2.0)

# To calculate perimeter of polygon
def polygonPerimeter(X, Y, n):
    perimeter = 0.0

    # Calculate value of perimeter
    j = n - 1
    for i in range(n):
        perimeter += math.sqrt((X[j] - X[i]) * (X[j] - X[i]) +
                          (Y[j] - Y[i]) * (Y[j] - Y[i]))

        # j is previous vertex to i
        j = i 

    return perimeter

# To find equable shape
def equableShape(X, Y, n):
    # Find area and perimeter of polygon if
    # they are equal then it is equable shape
    if (polygonPerimeter(X, Y, n) == polygonArea(X, Y, n)):
        print("Equable Shape")
    else:
        print("Not Equable Shape")

#  Driver program to test above function
X = [ 0, 5, 0 ]
Y = [ 0, 0, 12 ]
n = len(X)
equableShape(X, Y, n)

# This code is contributed by Azkia Anam.
```

## C#

```
// C# program to find equable shape
using System;

class equable {

    // To calculate area of polygon
    static double polygonArea(double []X,
                              double []Y,
                              int n)
    {
        double area = 0.0;

        // Calculate value of area using
        // Shoelace Formula
        int j = n - 1;
        for (int i = 0; i < n; i++)
        {
            area += (X[j] + X[i]) * (Y[j] - Y[i]);
            j = i; // j is previous vertex to i
        }

        return Math.Abs(area / 2.0);
    }

    // To calculate perimeter of polygon
    static double polygonPerimeter(double []X,
                                   double []Y,
                                   int n)
    {
        double perimeter = 0.0;

        // Calculate value of perimeter
        int j = n - 1;
        for (int i = 0; i < n; i++) {
            perimeter += Math.Sqrt((X[j] - X[i]) *
                                   (X[j] - X[i]) +
                                   (Y[j] - Y[i]) *
                                   (Y[j] - Y[i]));
            j = i; // j is previous vertex to i
        }

        return perimeter;
    }

    // To find equable shape
    static void equableShape(double []X,
                             double []Y,
                             int n)
    {
        // Find area and perimeter of
        // polygon if they are equal
        // then it is equable shape
        if (polygonPerimeter(X, Y, n) ==
            polygonArea(X, Y, n))
            Console.WriteLine("Equable Shape");
        else
            Console.WriteLine("Not Equable Shape");
    }

    // Driver Code
    public static void Main(String []args)
    {
        double []X = {0, 5, 0};
        double []Y = {0, 0, 12};

        int n = X.Length;

        // Calling Function
        equableShape(X, Y, n);
    }
}

// This Code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// equable shape

// To calculate area
// of polygon
function polygonArea($X, $Y, $n)
{
    $area = 0.0;

    // Calculate value of area
    // using shoelace formula
    $j = $n - 1;
    for ($i = 0; $i < $n; $i++)
    {
        $area += ($X[$j] + $X[$i]) *
                 ($Y[$j] - $Y[$i]);

        // j is previous vertex to i        
        $j = $i;
    }

    return abs($area / 2.0);
}

// To calculate perimeter of polygon
function polygonPerimeter($X, $Y, $n)

{
    $perimeter = 0.0;

    // Calculate value of perimeter
    $j = $n - 1;
    for ($i = 0; $i < $n; $i++)
    {
        $perimeter += sqrt(($X[$j] - $X[$i]) *
                           ($X[$j] - $X[$i]) +
                           ($Y[$j] - $Y[$i]) *
                           ($Y[$j] - $Y[$i]));

        // j is previous vertex to i
        $j = $i;
    }

    return $perimeter;
}

// To find equable shape
function equableShape($X, $Y, $n)
{
    // Find area and perimeter of
    // polygon if they are equal
    // then it is equable shape
    if (polygonPerimeter($X, $Y, $n) ==
        polygonArea($X, $Y, $n))
            echo "Equable Shape";
    else
            echo "Not Equable Shape";
}

// Driver Code
$X = array( 0, 5, 0 );
$Y = array( 0, 0, 12 );

$n = sizeof($X);

equableShape($X, $Y, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find equable shape

// To calculate area of polygon
function polygonArea(X, Y, n)
{
    let area = 0.0;

    // Calculate value of area using
    // Shoelace Formula
    let j = n - 1;
    for(let i = 0; i < n; i++)
    {
        area += (X[j] + X[i]) * (Y[j] - Y[i]);

        // j is previous vertex to i
        j = i;
    }

    return Math.abs(area / 2.0);
}

// To calculate perimeter of polygon
function polygonPerimeter(X, Y, n)
{
    let perimeter = 0.0;

    // Calculate value of perimeter
    let j = n - 1;
    for(let i = 0; i < n; i++)
    {
        perimeter += Math.sqrt((X[j] - X[i]) *
                               (X[j] - X[i]) +
                               (Y[j] - Y[i]) *
                               (Y[j] - Y[i]));

        // j is previous vertex to i                      
        j = i;
    }
    return perimeter;
}

// To find equable shape
function equableShape(X, Y, n)
{

    // Find area and perimeter of
    // polygon if they are equal
    // then it is equable shape
    if (polygonPerimeter(X, Y, n) ==
        polygonArea(X, Y, n))
        document.write("Equable Shape" + "</br>");
    else
        document.write("Not Equable Shape" + "</br>");
}

// Driver code
let X = [ 0, 5, 0 ];
let Y = [ 0, 0, 12 ];

let n = X.length;

// Calling Function
equableShape(X, Y, n);

// This code is contributed by suresh07 

</script>
```

**输出:**

```
Equable Shape
```

**参考:**T2[https://en.wikipedia.org/wiki/Equable_shape](https://en.wikipedia.org/wiki/Equable_shape)

本文由 [**核素**](https://facebook.com/nuclode) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。