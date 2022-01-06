# 从给定边及其相邻角开始的三角形剩余两条边的长度

> 原文:[https://www . geeksforgeeks . org/给定边及其邻角三角形的剩余两边长度/](https://www.geeksforgeeks.org/length-of-remaining-two-sides-of-a-triangle-from-a-given-side-and-its-adjacent-angles/)

给定三角形的一条边 **a** 及其相邻角 **B** 和 **C** 的长度，任务是找到三角形的剩余两条边。

> **输入:** a = 5，B = 62.2，C = 33.5
> **输出:** 4.44，2.77
> **解释**
> 三角形剩下的两条边是 b = 4.44488228556699 和 C = 2.773397979419038
> **输入:** a = 12，B = 60

**进场:**

1.  剩余角度可以通过三角形中的角度和定理来计算:
2.  三角形的另外两条边可以用正弦公式计算:

以下是上述方法的实现:

## C++

```
// C++ program for above approach
#include<bits/stdc++.h>
using namespace std;

// Function for computing other
// 2 side of the trianlgle
void findSide(float a, float B, float C)
{

    // Computing angle C
    float A = 180 - C - B;

    // Converting A in to radian
    float radA = M_PI * (A / 180);

    // Converting B in to radian
    float radB = M_PI * (B / 180);

    // Converting C in to radian
    float radC = M_PI * (C / 180);

    // Computing length of side b
    float b = a / sin(radA) * sin(radB);

    // Computing length of side c
    float c = a / sin(radA) * sin(radC);

    cout << fixed << setprecision(15) << b << " ";
    cout << fixed << setprecision(15) << c;
}

// Driver code
int main()
{
    int a = 12, B = 60, C = 30;

    // Calling function
    findSide(a, B, C);
}

// This code is contributed by ishayadav181
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG{

// Function for computing other
// 2 side of the trianlgle
static void findSide(double a, double B,
                     double C)
{

    // Computing angle C
    double A = 180 - C - B;

    // Converting A in to radian
    double radA = (Math.PI * (A / 180));

    // Converting B in to radian
    double radB = (Math.PI * (B / 180));

    // Converting C in to radian
    double radC = (Math.PI * (C / 180));

    // Computing length of side b
    double b = (a / Math.sin(radA) *
                    Math.sin(radB));

    // Computing length of side c
    double c = (a / Math.sin(radA) *
                    Math.sin(radC));

    System.out.printf("%.15f", b);
    System.out.printf(" %.15f", c);
}

// Driver code
public static void main(String[] args)
{
    int a = 12, B = 60, C = 30;

    // Calling function
    findSide(a, B, C);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for above approach
import math

# Function for computing other
# 2 side of the trianlgle
def findSide(a, B, C):

    # computing angle C
    A = 180-C-B

    # converting A in to radian
    radA = math.pi *(A / 180)

    # converting B in to radian
    radB = math.pi *(B / 180)

    # converting C in to radian
    radC = math.pi *(C / 180)

    # computing length of side b
    b = a / math.sin(radA)*math.sin(radB)

    # computing length of side c
    c = a / math.sin(radA)*math.sin(radC)

    return b, c

# driver program
a = 12
B = 60
C = 30

# calling function
b, c = findSide(a, B, C)
print(b, c)
```

## C#

```
// C# program for above approach
using System;
class GFG{

// Function for computing other
// 2 side of the trianlgle
static void findSide(float a,
                     double B, double C)
{   
  // Computing angle C
  double A = 180 - C - B;

  // Converting A in to radian
  double radA = (Math.PI * (A / 180));

  // Converting B in to radian
  double radB = (Math.PI * (B / 180));

  // Converting C in to radian
  double radC = (Math.PI * (C / 180));

  // Computing length of side b
  double b = (a / Math.Sin(radA) *
              Math.Sin(radB));

  // Computing length of side c
  double c = (a / Math.Sin(radA) *
              Math.Sin(radC));

  Console.Write("{0:F15}", b);
  Console.Write("{0:F15}", c);
}

  // Driver code
  public static void Main(String[] args)
  {
    int a = 12, B = 60, C = 30;

    // Calling function
    findSide(a, B, C);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function for computing other
// 2 side of the trianlgle
function findSide(a, B, C)
{

    // Computing angle C
    var A = 180 - C - B;

    // Converting A in to radian
    var radA = Math.PI * (A / 180);

    // Converting B in to radian
    var radB = Math.PI * (B / 180);

    // Converting C in to radian
    var radC = Math.PI * (C / 180);

    // Computing length of side b
    var b = a / Math.sin(radA) * Math.sin(radB);

    // Computing length of side c
    var c = a / Math.sin(radA) * Math.sin(radC);

    document.write( b + " ");
    document.write( c);
}

// Driver code
var a = 12, B = 60, C = 30;

// Calling function
findSide(a, B, C);

</script>
```

**Output:** 

```
10.392304845413264 5.999999999999999
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*