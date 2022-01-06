# 给定三个点的多边形的最小面积

> 原文:[https://www . geesforgeks . org/最小面积-多边形-三点-给定/](https://www.geeksforgeeks.org/minimum-area-polygon-three-points-given/)

给定正多边形的三个点(n > 3)，用给定的点找到正多边形的最小面积(所有边都相同)。
**例:**

```
Input : 0.00 0.00
        1.00 1.00
        0.00 1.00
Output : 1.00
By taking point (1.00, 0.00) square is 
formed of side 1.0 so area = 1.00 .
```

在我们继续之前，需要注意的一点是边数必须至少为 4(注意 n > 3 的条件)..
这里我们要求一个正多边形的最小可能面积，所以要计算最小可能面积，需要计算所需的 n 值，由于边长没有给定，所以我们先计算点形成的三角形的**外接圆半径。由公式
**R = abc / 4A**
给出，其中 A、b、c 是所形成三角形的边，A 是三角形的面积。这里，三角形的面积可以通过 **Heron 公式**来计算。
在计算出三角形的外接圆半径后，我们通过公式
**A = nX(sin(360/n)xr<sup>2</sup>/2)**
计算出多边形的面积，这里 r 表示 n 边正多边形(n 边正多边形)的外接圆半径。
但是， 首先我们要计算 n 的值，要计算 n 我们首先要通过**余弦公式**
**cosA =(b<sup>2</sup>+c<sup>2</sup>-a<sup>2</sup>)/2bc**
**cosB =(a<sup>2</sup>+c<sup>2</sup>-b<sup>2</sup>)计算出三角形的所有角度 2ac**
**cosC =(A<sup>2</sup>+B<sup>2</sup>-C<sup>2</sup>)/2ab**
然后，n 由
**给出 n = pi / GCD (A、B、C )**
其中 A、B、C 为三角形的夹角。 计算完 n 后，我们把这个值代入计算多边形面积的公式。
下面是给定方法的实现:** 

## C++

```
// CPP program to find minimum area of polygon of
// number of sides more than three with given three points.
#include <bits/stdc++.h>
using namespace std;

// assigning pi value to variable
const double pi = 3.14159265359;

// calculating gcd value of two double values .
double gcd(double x, double y)
{
    return fabs(y) < 1e-4 ? x : gcd(y, fmod(x, y));
}

// Calculating minimum area of polygon through this function .
double min_area_of_polygon(double Ax, double Ay, double Bx,
                            double By, double Cx, double Cy)
{
    double a, b, c, Radius, Angle_A, Angle_B, Angle_C,
                              semiperimeter, n, area;

    // calculating the length of the sides of the triangle
    // formed from given points a, b, c represents the
    // length of different sides of triangle .
    a = sqrt((Bx - Cx) * (Bx - Cx) + (By - Cy) * (By - Cy));
    b = sqrt((Ax - Cx) * (Ax - Cx) + (Ay - Cy) * (Ay - Cy));
    c = sqrt((Ax - Bx) * (Ax - Bx) + (Ay - By) * (Ay - By));

    // here we have calculated the semiperimeter of a triangle .
    semiperimeter = (a + b + c) / 2;

    // Now from the semiperimeter area of triangle is derived
    // through the heron's formula .
    double area_triangle = sqrt(semiperimeter * (semiperimeter - a)
                                * (semiperimeter - b)
                                * (semiperimeter - c));

    // thus circumradius of the triangle is derived from the
    // sides and area of the triangle calculated .
    Radius = (a * b * c) / (4 * area_triangle);

    // Now each angle of the triangle is derived from the sides
    // of the triangle .
    Angle_A = acos((b * b + c * c - a * a) / (2 * b * c));
    Angle_B = acos((a * a + c * c - b * b) / (2 * a * c));
    Angle_C = acos((b * b + a * a - c * c) / (2 * b * a));

    // Now n is calculated such that area is minimum for
    // the regular n-gon .
    n = pi / gcd(gcd(Angle_A, Angle_B), Angle_C);

    // calculating area of regular n-gon through the circumradius
    // of the triangle .
    area = (n * Radius * Radius * sin((2 * pi) / n)) / 2;

    return area;
}

int main()
{
    // three points are given as input .
    double Ax, Ay, Bx, By, Cx, Cy;
    Ax = 0.00;
    Ay = 0.00;
    Bx = 1.00;
    By = 1.00;
    Cx = 0.00;
    Cy = 1.00;

    printf("%.2f", min_area_of_polygon(Ax, Ay, Bx, By, Cx, Cy));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// area of polygon of number of
// sides more than three with
// given three points.
class GFG{

// Assigning pi value to variable
static double pi = 3.14159265359;

public static double fmod(double a,
                          double b)
{
  int result = (int) Math.floor(a / b);
  return a - result * b;
}

// calculating gcd value of
// two double values .
public static double gcd(double x,
                         double y)
{
  return Math.abs(y) < 1e-4 ? x :
         gcd(y, fmod(x, y));
}

// Calculating minimum area of polygon through this function .
public static double min_area_of_polygon(double Ax, double Ay,
                                         double Bx, double By,
                                         double Cx, double Cy)
{
  double a, b, c, Radius, Angle_A, Angle_B, Angle_C, 
         semiperimeter, n, area;

  // Calculating the length of the sides
  // of the triangle formed from given
  /// points a, b, c represents the 
  // length of different sides of triangle .
  a = Math.sqrt((Bx - Cx) * (Bx - Cx) +
                (By - Cy) * (By - Cy));
  b = Math.sqrt((Ax - Cx) * (Ax - Cx) +
                (Ay - Cy) * (Ay - Cy));
  c = Math.sqrt((Ax - Bx) * (Ax - Bx) +
                (Ay - By) * (Ay - By));

  // Here we have calculated the
  // semiperimeter of a triangle .
  semiperimeter = (a + b + c) / 2;

  // Now from the semiperimeter area
  // of triangle is derived
  // through the heron's formula .
  double area_triangle = Math.sqrt(semiperimeter *
                                  (semiperimeter - a) *
                                  (semiperimeter - b) *
                                  (semiperimeter - c));

  // Thus circumradius of the triangle
  // is derived from the sides and
  // area of the triangle calculated .
  Radius = (a * b * c) / (4 * area_triangle);

  // Now each angle of the triangle
  // is derived from the sides
  // of the triangle .
  Angle_A = Math.acos((b * b + c * c - a * a) /
                      (2 * b * c));
  Angle_B = Math.acos((a * a + c * c - b * b) /
                      (2 * a * c));
  Angle_C = Math.acos((b * b + a * a - c * c) /
                      (2 * b * a));

  // Now n is calculated such that
  // area is minimum for the regular n-gon .
  n = pi / gcd(gcd(Angle_A, Angle_B), Angle_C);

  // calculating area of regular n-gon
  // through the circumradius of the triangle .
  area = (n * Radius * Radius *
          Math.sin((2 * pi) / n)) / 2;

  return area;
}

// Driver code
public static void main(String[] args)
{
  // Three points are given as input .
  double Ax, Ay, Bx, By, Cx, Cy;
  Ax = 0.00;
  Ay = 0.00;
  Bx = 1.00;
  By = 1.00;
  Cx = 0.00;
  Cy = 1.00;
  System.out.println(String.format("%.2f",
                     min_area_of_polygon(Ax, Ay,
                                         Bx, By,
                                         Cx, Cy)));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find minimum area of
# polygon of number of sides more than three
# with given three points.

# from math lib import every function
from math import *

# assigning pi value to variable
pi = 3.14159265359

# calculating gcd value of two double values .
def gcd(x, y) :

    if abs(y) < 1e-4 :
        return x
    else :
        return gcd(y, fmod(x, y))

# Calculating minimum area of polygon
# through this function .
def min_area_of_polygon(Ax, Ay, Bx,
                        By, Cx, Cy) :

    # calculating the length of the sides of
    # the triangle formed from given points
    # a, b, c represents the length of different
    # sides of triangle
    a = sqrt((Bx - Cx) * (Bx - Cx) +
             (By - Cy) * (By - Cy))
    b = sqrt((Ax - Cx) * (Ax - Cx) +
             (Ay - Cy) * (Ay - Cy))
    c = sqrt((Ax - Bx) * (Ax - Bx) +
             (Ay - By) * (Ay - By))

    # here we have calculated the semiperimeter
    # of a triangle .
    semiperimeter = (a + b + c) / 2

    # Now from the semiperimeter area of triangle
    # is derived through the heron's formula
    area_triangle = sqrt(semiperimeter *
                        (semiperimeter - a) *
                        (semiperimeter - b) *
                        (semiperimeter - c))

    # thus circumradius of the triangle is derived
    # from the sides and area of the triangle calculated
    Radius = (a * b * c) / (4 * area_triangle)

    # Now each angle of the triangle is derived
    # from the sides of the triangle
    Angle_A = acos((b * b + c * c - a * a) / (2 * b * c))
    Angle_B = acos((a * a + c * c - b * b) / (2 * a * c))
    Angle_C = acos((b * b + a * a - c * c) / (2 * b * a))

    # Now n is calculated such that area is
    # minimum for the regular n-gon
    n = pi / gcd(gcd(Angle_A, Angle_B), Angle_C)

    # calculating area of regular n-gon through
    # the circumradius of the triangle
    area = (n * Radius * Radius *
            sin((2 * pi) / n)) / 2

    return area

# Driver Code
if __name__ == "__main__" :

    # three points are given as input .
    Ax = 0.00
    Ay = 0.00
    Bx = 1.00
    By = 1.00
    Cx = 0.00
    Cy = 1.00

    print(round(min_area_of_polygon(Ax, Ay, Bx,
                                    By, Cx, Cy), 1))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find minimum
// area of polygon of number of
// sides more than three with
// given three points. 
using System;
using System.Collections.Generic;

class GFG
{

    // Assigning pi value to variable
    static double pi = 3.14159265359;

    static double fmod(double a, double b)
    {
      int result = (int) Math.Floor(a / b);
      return a - result * b;
    }

    // calculating gcd value of
    // two double values .
    static double gcd(double x, double y)
    {
      return Math.Abs(y) < 1e-4 ? x : gcd(y, fmod(x, y));
    }

    // Calculating minimum area of polygon through this function .
    static double min_area_of_polygon(double Ax, double Ay,
                                             double Bx, double By,
                                             double Cx, double Cy)
    {
      double a, b, c, Radius, Angle_A, Angle_B, Angle_C, 
             semiperimeter, n, area;

      // Calculating the length of the sides
      // of the triangle formed from given
      /// points a, b, c represents the 
      // length of different sides of triangle .
      a = Math.Sqrt((Bx - Cx) * (Bx - Cx) +
                    (By - Cy) * (By - Cy));
      b = Math.Sqrt((Ax - Cx) * (Ax - Cx) +
                    (Ay - Cy) * (Ay - Cy));
      c = Math.Sqrt((Ax - Bx) * (Ax - Bx) +
                    (Ay - By) * (Ay - By));

      // Here we have calculated the
      // semiperimeter of a triangle .
      semiperimeter = (a + b + c) / 2;

      // Now from the semiperimeter area
      // of triangle is derived
      // through the heron's formula .
      double area_triangle = Math.Sqrt(semiperimeter *
                                      (semiperimeter - a) *
                                      (semiperimeter - b) *
                                      (semiperimeter - c));

      // Thus circumradius of the triangle
      // is derived from the sides and
      // area of the triangle calculated .
      Radius = (a * b * c) / (4 * area_triangle);

      // Now each angle of the triangle
      // is derived from the sides
      // of the triangle .
      Angle_A = Math.Acos((b * b + c * c - a * a) /
                          (2 * b * c));
      Angle_B = Math.Acos((a * a + c * c - b * b) /
                          (2 * a * c));
      Angle_C = Math.Acos((b * b + a * a - c * c) /
                          (2 * b * a));

      // Now n is calculated such that
      // area is minimum for the regular n-gon .
      n = pi / gcd(gcd(Angle_A, Angle_B), Angle_C);

      // calculating area of regular n-gon
      // through the circumradius of the triangle .
      area = (n * Radius * Radius *
              Math.Sin((2 * pi) / n)) / 2;

      return area;
    }  

  // Driver code
  static void Main()
  {
      // Three points are given as input .
      double Ax, Ay, Bx, By, Cx, Cy;
      Ax = 0.00;
      Ay = 0.00;
      Bx = 1.00;
      By = 1.00;
      Cx = 0.00;
      Cy = 1.00;
      Console.WriteLine(String.Format("{0:0.00}", min_area_of_polygon(Ax, Ay,
                                             Bx, By,
                                             Cx, Cy)));
  }
}

// This code is contributed by divyeshrabadiya07
```

**输出:**

```
1.00
```