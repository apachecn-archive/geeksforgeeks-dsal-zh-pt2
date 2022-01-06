# 给出圆上三点时的圆方程

> 原文:[https://www . geeksforgeeks . org/给出圆上三点时的圆方程/](https://www.geeksforgeeks.org/equation-of-circle-when-three-points-on-the-circle-are-given/)

给定位于一个圆上的三个坐标， **(x1，y1)** 、 **(x2，y2)** 和 **(x3，y3)** 。任务是找到圆的方程，然后打印圆的中心和半径。
圆的方程式一般形式为 **x + y + 2gx + 2fy + c = 0** ，半径形式为**(x–h)+(y-k)= r**，其中 **(h，k)** 为圆心， **r** 为半径。
**举例:**

> **输入:** x1 = 1，y1 = 0，x2 = -1，y2 = 0，x3 = 0，y3 = 1
> **输出:**
> 中心= (0，0)
> 半径= 1
> 圆的方程式为 x <sup>2</sup> + y <sup>2</sup> = 1。
> **输入:** x1 = 1，y1 = -6，x2 = 2，y2 = 1，x3 = 5，y3 = 2
> **输出:**
> 圆心= (5，-3)
> 半径= 5
> 圆的方程为 x<sup>2</sup>+y<sup>2</sup>-10x+6y+9 = 0

**逼近:**我们知道所有的三点都位于圆上，所以它们将满足圆的方程，通过将它们放入一般方程中，我们得到三个具有三个变量的方程 **g** 、 **f** 和 **c** ，通过进一步求解，我们可以得到这些值。我们可以推导出公式，得到 g、f 和 c 的值为:

> **将坐标放入圆的方程中， 我们得到:**
> x1<sup>2</sup>+y1<sup>2</sup>+2g x1+2fy1+c = 0**–(1)**
> x2<sup>2</sup>+y2<sup>2</sup>+2g x2+2fy2+c = 0**–(2)**
> x3<sup>2</sup>+y3<sup>2</sup>+2g x3+2fy3 2g x1 =-x1<sup>2</sup>–y1<sup>2</sup>–2 fy1–c**–(4)**
> **从(1)我们得到**，c =-x1<sup>2</sup>–y1<sup>2</sup>–2g x1–2 fy1**–(5)**
> T42 从(3)我们得到， 2fy3 =-x3<sup>2</sup>–y3<sup>2</sup>–2g x3–c**–(6)**
> **从方程(1)中减去方程(2)我们得到**，
> 2g(x1–x2)=(x2<sup>2</sup>-x1<sup>2</sup>)+(y2<sup>2</sup>–y1<sup>2</sup>)+2f(y2–y1)**–(A)**
> **现在将等式(5)放入(6)中，我们得到**，
> 2 fy3 =-x3<sup>2</sup>–y3<sup>2</sup>–2g x3+x1<sup>2</sup>+y1<sup>2</sup>+2g x1+2 fy1**–(7)**
> **现在将等式(A)中的 2g 值放入(7)中，我们得到**，
> **2f**=((x1<sup>2</sup>–x3<sup>2</sup>)(x1–x2)+(y1<sup>2</sup>–y3<sup>2</sup>)(x1–x2)+(x2<sup>2</sup>–x1<sup>2</sup>)(x1–x3)+(y2<sup>2</sup>–y1 –(y2–y1)(x1–x3)
> **同样我们可以得到 2g:**
> **2g**=((x1<sup>2</sup>–x3<sup>2</sup>)(y1–x2)+(y1<sup>2</sup>–y3<sup>2</sup>)(y1–y2)+(x2<sup>2</sup>–x1 <sup>+(y2<sup>2</sup>–y1<sup>2</sup>)(y1–y3))/(x3-x1)(y1–y2)–(x2–x1)(y1–y3)
> 将 2g 和 2f 放入等式(5)中，我们得到 c 的值，并且知道我们有圆的等式为 x<sup>2</sup>+y<sup>2</sup>+2g x+2fy+c = 0</sup>

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the circle on
// which the given three points lie
void findCircle(int x1, int y1, int x2, int y2, int x3, int y3)
{
    int x12 = x1 - x2;
    int x13 = x1 - x3;

    int y12 = y1 - y2;
    int y13 = y1 - y3;

    int y31 = y3 - y1;
    int y21 = y2 - y1;

    int x31 = x3 - x1;
    int x21 = x2 - x1;

    // x1^2 - x3^2
    int sx13 = pow(x1, 2) - pow(x3, 2);

    // y1^2 - y3^2
    int sy13 = pow(y1, 2) - pow(y3, 2);

    int sx21 = pow(x2, 2) - pow(x1, 2);
    int sy21 = pow(y2, 2) - pow(y1, 2);

    int f = ((sx13) * (x12)
             + (sy13) * (x12)
             + (sx21) * (x13)
             + (sy21) * (x13))
            / (2 * ((y31) * (x12) - (y21) * (x13)));
    int g = ((sx13) * (y12)
             + (sy13) * (y12)
             + (sx21) * (y13)
             + (sy21) * (y13))
            / (2 * ((x31) * (y12) - (x21) * (y13)));

    int c = -pow(x1, 2) - pow(y1, 2) - 2 * g * x1 - 2 * f * y1;

    // eqn of circle be x^2 + y^2 + 2*g*x + 2*f*y + c = 0
    // where centre is (h = -g, k = -f) and radius r
    // as r^2 = h^2 + k^2 - c
    int h = -g;
    int k = -f;
    int sqr_of_r = h * h + k * k - c;

    // r is the radius
    float r = sqrt(sqr_of_r);

    cout << "Centre = (" << h << ", " << k << ")" << endl;
    cout << "Radius = " << r;
}

// Driver code
int main()
{
    int x1 = 1, y1 = 1;
    int x2 = 2, y2 = 4;
    int x3 = 5, y3 = 3;
    findCircle(x1, y1, x2, y2, x3, y3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.text.*;

class GFG
{

// Function to find the circle on
// which the given three points lie
static void findCircle(int x1, int y1,
                        int x2, int y2,
                        int x3, int y3)
{
    int x12 = x1 - x2;
    int x13 = x1 - x3;

    int y12 = y1 - y2;
    int y13 = y1 - y3;

    int y31 = y3 - y1;
    int y21 = y2 - y1;

    int x31 = x3 - x1;
    int x21 = x2 - x1;

    // x1^2 - x3^2
    int sx13 = (int)(Math.pow(x1, 2) -
                    Math.pow(x3, 2));

    // y1^2 - y3^2
    int sy13 = (int)(Math.pow(y1, 2) -
                    Math.pow(y3, 2));

    int sx21 = (int)(Math.pow(x2, 2) -
                    Math.pow(x1, 2));

    int sy21 = (int)(Math.pow(y2, 2) -
                    Math.pow(y1, 2));

    int f = ((sx13) * (x12)
            + (sy13) * (x12)
            + (sx21) * (x13)
            + (sy21) * (x13))
            / (2 * ((y31) * (x12) - (y21) * (x13)));
    int g = ((sx13) * (y12)
            + (sy13) * (y12)
            + (sx21) * (y13)
            + (sy21) * (y13))
            / (2 * ((x31) * (y12) - (x21) * (y13)));

    int c = -(int)Math.pow(x1, 2) - (int)Math.pow(y1, 2) -
                                2 * g * x1 - 2 * f * y1;

    // eqn of circle be x^2 + y^2 + 2*g*x + 2*f*y + c = 0
    // where centre is (h = -g, k = -f) and radius r
    // as r^2 = h^2 + k^2 - c
    int h = -g;
    int k = -f;
    int sqr_of_r = h * h + k * k - c;

    // r is the radius
    double r = Math.sqrt(sqr_of_r);
    DecimalFormat df = new DecimalFormat("#.#####");
    System.out.println("Centre = (" + h + "," + k + ")");
    System.out.println("Radius = " + df.format(r));
}

// Driver code
public static void main (String[] args)
{
    int x1 = 1, y1 = 1;
    int x2 = 2, y2 = 4;
    int x3 = 5, y3 = 3;
    findCircle(x1, y1, x2, y2, x3, y3);
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Function to find the circle on
# which the given three points lie
def findCircle(x1, y1, x2, y2, x3, y3) :
    x12 = x1 - x2;
    x13 = x1 - x3;

    y12 = y1 - y2;
    y13 = y1 - y3;

    y31 = y3 - y1;
    y21 = y2 - y1;

    x31 = x3 - x1;
    x21 = x2 - x1;

    # x1^2 - x3^2
    sx13 = pow(x1, 2) - pow(x3, 2);

    # y1^2 - y3^2
    sy13 = pow(y1, 2) - pow(y3, 2);

    sx21 = pow(x2, 2) - pow(x1, 2);
    sy21 = pow(y2, 2) - pow(y1, 2);

    f = (((sx13) * (x12) + (sy13) *
          (x12) + (sx21) * (x13) +
          (sy21) * (x13)) // (2 *
          ((y31) * (x12) - (y21) * (x13))));

    g = (((sx13) * (y12) + (sy13) * (y12) +
          (sx21) * (y13) + (sy21) * (y13)) //
          (2 * ((x31) * (y12) - (x21) * (y13))));

    c = (-pow(x1, 2) - pow(y1, 2) -
         2 * g * x1 - 2 * f * y1);

    # eqn of circle be x^2 + y^2 + 2*g*x + 2*f*y + c = 0
    # where centre is (h = -g, k = -f) and
    # radius r as r^2 = h^2 + k^2 - c
    h = -g;
    k = -f;
    sqr_of_r = h * h + k * k - c;

    # r is the radius
    r = round(sqrt(sqr_of_r), 5);

    print("Centre = (", h, ", ", k, ")");
    print("Radius = ", r);

# Driver code
if __name__ == "__main__" :

    x1 = 1 ; y1 = 1;
    x2 = 2 ; y2 = 4;
    x3 = 5 ; y3 = 3;
    findCircle(x1, y1, x2, y2, x3, y3);

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the circle on
// which the given three points lie
static void findCircle(int x1, int y1,
                        int x2, int y2,
                        int x3, int y3)
{
    int x12 = x1 - x2;
    int x13 = x1 - x3;

    int y12 = y1 - y2;
    int y13 = y1 - y3;

    int y31 = y3 - y1;
    int y21 = y2 - y1;

    int x31 = x3 - x1;
    int x21 = x2 - x1;

    // x1^2 - x3^2
    int sx13 = (int)(Math.Pow(x1, 2) -
                    Math.Pow(x3, 2));

    // y1^2 - y3^2
    int sy13 = (int)(Math.Pow(y1, 2) -
                    Math.Pow(y3, 2));

    int sx21 = (int)(Math.Pow(x2, 2) -
                    Math.Pow(x1, 2));

    int sy21 = (int)(Math.Pow(y2, 2) -
                    Math.Pow(y1, 2));

    int f = ((sx13) * (x12)
            + (sy13) * (x12)
            + (sx21) * (x13)
            + (sy21) * (x13))
            / (2 * ((y31) * (x12) - (y21) * (x13)));
    int g = ((sx13) * (y12)
            + (sy13) * (y12)
            + (sx21) * (y13)
            + (sy21) * (y13))
            / (2 * ((x31) * (y12) - (x21) * (y13)));

    int c = -(int)Math.Pow(x1, 2) - (int)Math.Pow(y1, 2) -
                                2 * g * x1 - 2 * f * y1;

    // eqn of circle be x^2 + y^2 + 2*g*x + 2*f*y + c = 0
    // where centre is (h = -g, k = -f) and radius r
    // as r^2 = h^2 + k^2 - c
    int h = -g;
    int k = -f;
    int sqr_of_r = h * h + k * k - c;

    // r is the radius
    double r = Math.Round(Math.Sqrt(sqr_of_r), 5);

    Console.WriteLine("Centre = (" + h + "," + k + ")");
    Console.WriteLine("Radius = " + r);
}

// Driver code
static void Main()
{
    int x1 = 1, y1 = 1;
    int x2 = 2, y2 = 4;
    int x3 = 5, y3 = 3;
    findCircle(x1, y1, x2, y2, x3, y3);
}
}

// This code is contributed by chandan_jnu
```

## java 描述语言

```
<script>

// Function to find the circle on
// which the given three points lie
function findCircle(x1,  y1,  x2,  y2, x3, y3)
{
    var x12 = (x1 - x2);
    var x13 = (x1 - x3);

    var y12 =( y1 - y2);
    var y13 = (y1 - y3);

    var y31 = (y3 - y1);
    var y21 = (y2 - y1);

    var x31 = (x3 - x1);
    var x21 = (x2 - x1);

    //x1^2 - x3^2
    var sx13 = Math.pow(x1, 2) - Math.pow(x3, 2);

    // y1^2 - y3^2
    var sy13 = Math.pow(y1, 2) - Math.pow(y3, 2);

    var sx21 = Math.pow(x2, 2) - Math.pow(x1, 2);
    var sy21 = Math.pow(y2, 2) - Math.pow(y1, 2);

    var f = ((sx13) * (x12)
            + (sy13) * (x12)
            + (sx21) * (x13)
            + (sy21) * (x13))
            / (2 * ((y31) * (x12) - (y21) * (x13)));
    var g = ((sx13) * (y12)
            + (sy13) * (y12)
            + (sx21) * (y13)
            + (sy21) * (y13))
            / (2 * ((x31) * (y12) - (x21) * (y13)));

    var c = -(Math.pow(x1, 2)) -
    Math.pow(y1, 2) - 2 * g * x1 - 2 * f * y1;

    // eqn of circle be
    // x^2 + y^2 + 2*g*x + 2*f*y + c = 0
    // where centre is (h = -g, k = -f) and radius r
    // as r^2 = h^2 + k^2 - c
    var h = -g;
    var k = -f;
    var sqr_of_r = h * h + k * k - c;

    // r is the radius
    var r = Math.sqrt(sqr_of_r);

    document.write("Centre = (" + h + ", "+ k +")" + "<br>");
    document.write( "Radius = " + r.toFixed(5));
}

var x1 = 1, y1 = 1;
    var x2 = 2, y2 = 4;
    var x3 = 5, y3 = 3;
    findCircle(x1, y1, x2, y2, x3, y3);

</script>
```

**Output:** 

```
Centre = (3, 2)
Radius = 2.23607
```