# 直角三角形的正中心和外心之间的距离

> 原文:[https://www . geeksforgeeks . org/直角三角形的正中心和外心之间的距离/](https://www.geeksforgeeks.org/distance-between-orthocenter-and-circumcenter-of-a-right-angled-triangle/)

给定三对[整数 **A(x，y)** 、 **B(x，y)** 和 **C(x，y)** ，代表一个](https://www.geeksforgeeks.org/pair-in-cpp-stl/)[直角三角形](https://en.wikipedia.org/wiki/Right_triangle)的坐标，任务是找出[正心](https://en.wikipedia.org/wiki/Altitude_(triangle)#Orthocenter)和[外心](https://en.wikipedia.org/wiki/Circumscribed_circle)之间的距离。

**示例:**

> **输入:** A = {0，0}，B = {5，0}，C = {0，12}
> **输出:** 6.5
> **解释:**
> 三角形 ABC 在 A 点呈直角，因此，正交中心位于 A 点，即(0，0)。
> 圆心坐标为(2.5，6)。
> 因此，正中心与外心之间的距离为 6.5。
> 
> **输入:** A = {0，0}，B = {6，0}，C = {0，8}
> **输出:** 5
> **解释:**
> 三角形 ABC 在点 A 处呈直角，因此，正交中心位于(0，0)的点 A 上。
> 圆心坐标为(3，4)。
> 因此，正中心与外心之间的距离为 5。

**方法:**思路是根据以下观察找到给定三角形的**正心**和[T5】圆心的坐标:](https://www.geeksforgeeks.org/program-find-circumcenter-triangle-2/) 

> **正中心**是三个高度交汇的点。在直角三角形中，正中心是位于**直角顶点**的顶点。
> 圆心**是三角形的**垂直平分线**相交的点。在直角三角形中，圆心位于斜边**的**中心。**

按照以下步骤解决问题:

*   求直角三角形三条边中最长的边，即斜边。
*   找到斜边的中心，设置为**圆心**。
*   找到最长边对面的顶点，设置为**正心**。
*   计算它们之间的距离，并将其打印为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate Euclidean
// distance between the points p1 and p2
double distance(pair<double, double> p1,
                pair<double, double> p2)
{
    // Stores x coordinates of both points
    double x1 = p1.first, x2 = p2.first;

    // Stores y coordinates of both points
    double y1 = p1.second, y2 = p2.second;

    // Return the Euclid distance
    // using distance formula
    return sqrt(pow(x2 - x1, 2)
                + pow(y2 - y1, 2) * 1.0);
}

// Function to find orthocenter of
// the right angled triangle
pair<double, double>
find_orthocenter(pair<double, double> A,
                 pair<double, double> B,
                 pair<double, double> C)
{
    // Find the length of the three sides
    double AB = distance(A, B);
    double BC = distance(B, C);
    double CA = distance(C, A);

    // Orthocenter will be the vertex
    // opposite to the largest side
    if (AB > BC && AB > CA)
        return C;
    if (BC > AB && BC > CA)
        return A;
    return B;
}

// Function to find the circumcenter
// of right angle triangle
pair<double, double>
find_circumcenter(pair<double, double> A,
                  pair<double, double> B,
                  pair<double, double> C)
{
    // Circumcenter will be located
    // at center of hypotenuse
    double AB = distance(A, B);
    double BC = distance(B, C);
    double CA = distance(C, A);

    // Find the hypotenuse and then
    // find middle point of hypotenuse

    // If AB is the hypotenuse
    if (AB > BC && AB > CA)
        return { (A.first + B.first) / 2,
                 (A.second + B.second) / 2 };

    // If BC is the hypotenuse
    if (BC > AB && BC > CA)
        return { (B.first + C.first) / 2,
                 (B.second + C.second) / 2 };

    // If AC is the hypotenuse
    return { (C.first + A.first) / 2,
             (C.second + A.second) / 2 };
}

// Function to find distance between
// orthocenter and circumcenter
void findDistance(pair<double, double> A,
                  pair<double, double> B,
                  pair<double, double> C)
{

    // Find circumcenter
    pair<double, double> circumcenter
        = find_circumcenter(A, B, C);

    // Find orthocenter
    pair<double, double> orthocenter
        = find_orthocenter(A, B, C);

    // Find the distance between the
    // orthocenter and circumcenter
    double distance_between
        = distance(circumcenter,
                   orthocenter);

    // Print distance between orthocenter
    // and circumcenter
    cout << distance_between << endl;
}

// Driver Code
int main()
{
    pair<double, double> A, B, C;

    // Given coordinates A, B, and C
    A = { 0.0, 0.0 };
    B = { 6.0, 0.0 };
    C = { 0.0, 8.0 };

    // Function Call
    findDistance(A, B, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{
  static class pair
  {
    double first, second;
    public pair(double first, double second) 
    {
      this.first = first;
      this.second = second;
    }   
  }

  // Function to calculate Euclidean
  // distance between the points p1 and p2
  static double distance(pair p1,
                         pair p2)
  {

    // Stores x coordinates of both points
    double x1 = p1.first, x2 = p2.first;

    // Stores y coordinates of both points
    double y1 = p1.second, y2 = p2.second;

    // Return the Euclid distance
    // using distance formula
    return Math.sqrt(Math.pow(x2 - x1, 2)
                     + Math.pow(y2 - y1, 2) * 1.0);
  }

  // Function to find orthocenter of
  // the right angled triangle
  static pair
    find_orthocenter(pair A,
                     pair B,
                     pair C)
  {

    // Find the length of the three sides
    double AB = distance(A, B);
    double BC = distance(B, C);
    double CA = distance(C, A);

    // Orthocenter will be the vertex
    // opposite to the largest side
    if (AB > BC && AB > CA)
      return C;
    if (BC > AB && BC > CA)
      return A;
    return B;
  }

  // Function to find the circumcenter
  // of right angle triangle
  static pair
    find_circumcenter(pair A,
                      pair B,
                      pair C)
  {

    // Circumcenter will be located
    // at center of hypotenuse
    double AB = distance(A, B);
    double BC = distance(B, C);
    double CA = distance(C, A);

    // Find the hypotenuse and then
    // find middle point of hypotenuse

    // If AB is the hypotenuse
    if (AB > BC && AB > CA)
      return new pair((A.first + B.first) / 2,
                      (A.second + B.second) / 2 );

    // If BC is the hypotenuse
    if (BC > AB && BC > CA)
      return new pair((B.first + C.first) / 2,
                      (B.second + C.second) / 2 );

    // If AC is the hypotenuse
    return new pair( (C.first + A.first) / 2,
                    (C.second + A.second) / 2 );
  }

  // Function to find distance between
  // orthocenter and circumcenter
  static void findDistance(pair A,
                           pair B,
                           pair C)
  {

    // Find circumcenter
    pair circumcenter
      = find_circumcenter(A, B, C);

    // Find orthocenter
    pair orthocenter
      = find_orthocenter(A, B, C);

    // Find the distance between the
    // orthocenter and circumcenter
    double distance_between
      = distance(circumcenter,
                 orthocenter);

    // Print distance between orthocenter
    // and circumcenter
    System.out.print(distance_between +"\n");
  }

  // Driver Code
  public static void main(String[] args)
  {
    pair A, B, C;

    // Given coordinates A, B, and C
    A = new pair( 0.0, 0.0 );
    B = new pair(6.0, 0.0 );
    C = new pair(0.0, 8.0 );

    // Function Call
    findDistance(A, B, C);
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to calculate Euclidean
# distance between the points p1 and p2
def distance(p1, p2) :

    # Stores x coordinates of both points
    x1, x2 = p1[0], p2[0]

    # Stores y coordinates of both points
    y1, y2 = p1[1], p2[1]

    # Return the Euclid distance
    # using distance formula
    return int(math.sqrt(pow(x2 - x1, 2) + pow(y2 - y1, 2)))

# Function to find orthocenter of
# the right angled triangle
def find_orthocenter(A, B, C) :

    # Find the length of the three sides
    AB = distance(A, B)
    BC = distance(B, C)
    CA = distance(C, A)

    # Orthocenter will be the vertex
    # opposite to the largest side
    if (AB > BC and AB > CA) :
        return C
    if (BC > AB and BC > CA) :
        return A
    return B

# Function to find the circumcenter
# of right angle triangle
def find_circumcenter(A, B, C) :

    # Circumcenter will be located
    # at center of hypotenuse
    AB = distance(A, B)
    BC = distance(B, C)
    CA = distance(C, A)

    # Find the hypotenuse and then
    # find middle point of hypotenuse

    # If AB is the hypotenuse
    if (AB > BC and AB > CA) :
        return ((A[0] + B[0]) // 2, (A[1] + B[1]) // 2)

    # If BC is the hypotenuse
    if (BC > AB and BC > CA) :
        return ((B[0] + C[0]) // 2, (B[1] + C[1]) // 2)

    # If AC is the hypotenuse
    return ((C[0] + A[0]) // 2, (C[1] + A[1]) // 2)

# Function to find distance between
# orthocenter and circumcenter
def findDistance(A, B, C) :

    # Find circumcenter
    circumcenter = find_circumcenter(A, B, C)

    # Find orthocenter
    orthocenter = find_orthocenter(A, B, C)

    # Find the distance between the
    # orthocenter and circumcenter
    distance_between = distance(circumcenter, orthocenter)

    # Print distance between orthocenter
    # and circumcenter
    print(distance_between)

# Given coordinates A, B, and C
A = [ 0, 0 ]
B = [ 6, 0 ]
C = [ 0, 8 ]

# Function Call
findDistance(A, B, C)

# This code is contributed by divyesh072019.
```

## C#

```
// C# program for the above approach
using System;

class GFG{
  public class pair
  {
    public double first, second;
    public pair(double first, double second) 
    {
      this.first = first;
      this.second = second;
    }   
  }

  // Function to calculate Euclidean
  // distance between the points p1 and p2
  static double distance(pair p1,
                         pair p2)
  {

    // Stores x coordinates of both points
    double x1 = p1.first, x2 = p2.first;

    // Stores y coordinates of both points
    double y1 = p1.second, y2 = p2.second;

    // Return the Euclid distance
    // using distance formula
    return Math.Sqrt(Math.Pow(x2 - x1, 2)
                     + Math.Pow(y2 - y1, 2) * 1.0);
  }

  // Function to find orthocenter of
  // the right angled triangle
  static pair
    find_orthocenter(pair A,
                     pair B,
                     pair C)
  {

    // Find the length of the three sides
    double AB = distance(A, B);
    double BC = distance(B, C);
    double CA = distance(C, A);

    // Orthocenter will be the vertex
    // opposite to the largest side
    if (AB > BC && AB > CA)
      return C;
    if (BC > AB && BC > CA)
      return A;
    return B;
  }

  // Function to find the circumcenter
  // of right angle triangle
  static pair
    find_circumcenter(pair A,
                      pair B,
                      pair C)
  {

    // Circumcenter will be located
    // at center of hypotenuse
    double AB = distance(A, B);
    double BC = distance(B, C);
    double CA = distance(C, A);

    // Find the hypotenuse and then
    // find middle point of hypotenuse

    // If AB is the hypotenuse
    if (AB > BC && AB > CA)
      return new pair((A.first + B.first) / 2,
                      (A.second + B.second) / 2 );

    // If BC is the hypotenuse
    if (BC > AB && BC > CA)
      return new pair((B.first + C.first) / 2,
                      (B.second + C.second) / 2 );

    // If AC is the hypotenuse
    return new pair( (C.first + A.first) / 2,
                    (C.second + A.second) / 2 );
  }

  // Function to find distance between
  // orthocenter and circumcenter
  static void findDistance(pair A,
                           pair B,
                           pair C)
  {

    // Find circumcenter
    pair circumcenter
      = find_circumcenter(A, B, C);

    // Find orthocenter
    pair orthocenter
      = find_orthocenter(A, B, C);

    // Find the distance between the
    // orthocenter and circumcenter
    double distance_between
      = distance(circumcenter,
                 orthocenter);

    // Print distance between orthocenter
    // and circumcenter
    Console.Write(distance_between +"\n");
  }

  // Driver Code
  public static void Main(String[] args)
  {
    pair A, B, C;

    // Given coordinates A, B, and C
    A = new pair( 0.0, 0.0 );
    B = new pair(6.0, 0.0 );
    C = new pair(0.0, 8.0 );

    // Function Call
    findDistance(A, B, C);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to calculate Euclidean
// distance between the points p1 and p2
function distance( p1, p2)
{
    // Stores x coordinates of both points
    var x1 = p1[0], x2 = p2[0];

    // Stores y coordinates of both points
    var y1 = p1[1], y2 = p2[1];

    // Return the Euclid distance
    // using distance formula
    return Math.sqrt(Math.pow(x2 - x1, 2)
                + Math.pow(y2 - y1, 2) * 1.0);
}

// Function to find orthocenter of
// the right angled triangle
function find_orthocenter( A, B, C)
{
    // Find the length of the three sides
    var AB = distance(A, B);
    var BC = distance(B, C);
    var CA = distance(C, A);

    // Orthocenter will be the vertex
    // opposite to the largest side
    if (AB > BC && AB > CA)
        return C;
    if (BC > AB && BC > CA)
        return A;
    return B;
}

// Function to find the circumcenter
// of right angle triangle
function find_circumcenter( A, B, C)
{
    // Circumcenter will be located
    // at center of hypotenuse
    var AB = distance(A, B);
    var BC = distance(B, C);
    var CA = distance(C, A);

    // Find the hypotenuse and then
    // find middle point of hypotenuse

    // If AB is the hypotenuse
    if (AB > BC && AB > CA)
        return [ Math.floor((A[0] + B[0]) / 2),
                 Math.floor((A[1] + B[1]) / 2) ];

    // If BC is the hypotenuse
    if (BC > AB && BC > CA)
        return [ Math.floor((B[0] + C[0]) / 2),
                 Math.floor((B[1] + C[1]) / 2) ];

    // If AC is the hypotenuse
    return [ Math.floor((C[0] + A[0]) / 2),
             Math.floor((C[1] + A[1]) / 2) ];
}

// Function to find distance between
// orthocenter and circumcenter
function findDistance( A, B, C)
{

    // Find circumcenter
     circumcenter = find_circumcenter(A, B, C);

    // Find orthocenter
     orthocenter = find_orthocenter(A, B, C);

    // Find the distance between the
    // orthocenter and circumcenter
    var distance_between
        = distance(circumcenter,
                   orthocenter);

    // Print distance between orthocenter
    // and circumcenter
    document.write(distance_between+"<br>");
}

// Driver Code
var A, B, C;

// Given coordinates A, B, and C
A = [ 0, 0 ];
B = [ 6, 0 ];
C = [ 0, 8 ];

// Function Call
findDistance(A, B, C);

// This code is contributed by Shubham Singh
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)