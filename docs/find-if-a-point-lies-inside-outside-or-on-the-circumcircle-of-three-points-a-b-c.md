# 找出一个点是在 A、B、C 三点的外接圆内、外还是在外接圆上

> 原文:[https://www . geesforgeks . org/find-if-a-point-lie-in-out-or-on-外接圆三点 a-b-c/](https://www.geeksforgeeks.org/find-if-a-point-lies-inside-outside-or-on-the-circumcircle-of-three-points-a-b-c/)

给定四个非共线点 **A、B、C 和 P** 。任务是找出点 **P** 是位于**内部、外部还是位于由点 **A、B 和 C** 形成的外接圆**上。
**示例**

> **输入:** A = {2，8}，B = {2，1}，C = {4，5}，P = {2，4 }；
> **输出:**点(2，4)在外接圆内。
> 
> **输入:** A = {2，8}，B = {2，1}，C = {4，5}，P = {3，0 }；
> **输出:**点(3，0)位于外接圆之外。

**进场:**

*   通过[这篇](https://www.geeksforgeeks.org/program-find-circumcenter-triangle-2/)文章中讨论的方法找到由点 **A、B 和 C** 形成的三角形的[圆心。](https://www.geeksforgeeks.org/program-find-circumcenter-triangle-2/)
*   在上述步骤中获得外心的点后，通过计算外心与 **A、B 或 C** 点之一的距离，使用以下公式计算外心的半径:

```
For Point A = (x, y) and Point B = (a, b)
The distance between points A and B is given by:- 
distance = sqrt((x - a)<sup>2 + (y - b)2</sup>)
```

*   既然我们知道圆的半径和圆心以及点 **P** 的坐标，那么就用[这篇](https://www.geeksforgeeks.org/find-if-a-point-lies-inside-or-on-circle/)文章中讨论的方法找到点 P 的位置。

下面是上述方法的实现:

## C++

```
// C++ program to find the points
// which lies inside, outside or
// on the circle
#include <bits/stdc++.h>
using namespace std;

// Structure Pointer to
// store x and y coordinates
struct point {
    double x, y;
};

// Function to find the line given
// two points
void lineFromPoints(point P, point Q,
                    double& a, double& b,
                    double& c)
{
    a = Q.y - P.y;
    b = P.x - Q.x;
    c = a * (P.x) + b * (P.y);
}

// Function which converts the
// input line to its perpendicular
// bisector. It also inputs the
// points whose mid-point lies o
// on the bisector
void perpenBisectorFromLine(point P, point Q,
                            double& a, double& b,
                            double& c)
{

    // Find the mid point
    point mid_point;

    // x coordinates
    mid_point.x = (P.x + Q.x) / 2;

    // y coordinates
    mid_point.y = (P.y + Q.y) / 2;

    // c = -bx + ay
    c = -b * (mid_point.x)
        + a * (mid_point.y);

    // Assign the coefficient of
    // a and b
    double temp = a;
    a = -b;
    b = temp;
}

// Returns the intersection point of
// two lines
double LineInterX(double a1, double b1,
                  double c1, double a2,
                  double b2, double c2)
{

    // Find determinant
    double determ = a1 * b2 - a2 * b1;

    double x = (b2 * c1 - b1 * c2);
    x /= determ;

    return x;
}

// Returns the intersection point of
// two lines
double LineInterY(double a1, double b1,
                  double c1, double a2,
                  double b2, double c2)
{

    // Find determinant
    double determ = a1 * b2 - a2 * b1;

    double y = (a1 * c2 - a2 * c1);
    y /= determ;

    return y;
}

// Function to find the point
// lies inside, outside or on
// the circle
void findPosition(point P, point Q,
                  point R, point D)
{

    // Store the coordinates
    // radius of circumcircle
    point r;

    // Line PQ is represented
    // as ax + by = c
    double a, b, c;
    lineFromPoints(P, Q, a, b, c);

    // Line QR is represented
    // as ex + fy = g
    double e, f, g;
    lineFromPoints(Q, R, e, f, g);

    // Converting lines PQ and QR
    // to perpendicular bisectors.
    // After this, L = ax + by = c
    // M = ex + fy = g
    perpenBisectorFromLine(P, Q, a, b, c);
    perpenBisectorFromLine(Q, R, e, f, g);

    // The point of intersection
    // of L and M gives r as the
    // circumcenter
    r.x = LineInterX(a, b, c, e, f, g);
    r.y = LineInterY(a, b, c, e, f, g);

    // Length of radius
    double q = (r.x - P.x) * (r.x - P.x)
               + (r.y - P.y) * (r.y - P.y);

    // Distance between radius
    // and the given point D
    double dis = (r.x - D.x) * (r.x - D.x)
                 + (r.y - D.y) * (r.y - D.y);

    // Condition for point lies
    // inside circumcircle
    if (dis < q) {
        cout << "Point (" << D.x << ", "
             << D.y << ") is inside "
             << "the circumcircle";
    }

    // Condition for point lies
    // on circumcircle
    else if (dis == q) {
        cout << "Point (" << D.x << ", "
             << D.y << ") lies on the "
             << "circumcircle";
    }

    // Condition for point lies
    // outside circumcircle
    else {
        cout << "Point (" << D.x << ", "
             << D.y << ") lies outside"
             << " the circumcircle";
    }
}

// Driver Code
int main()
{
    point A, B, C, D;

    // Given Points
    A = { 2, 8 };
    B = { 2, 1 };
    C = { 4, 5 };
    D = { 3, 0 };

    // Function call to find
    // the point lies inside,
    // outside or on the
    // circle
    findPosition(A, B, C, D);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the points
// which lies inside, outside or
// on the circle
class GFG{

// Structure Pointer to
// store x and y coordinates
static class point {
    double x, y;
    public point() {
    }
    public point(double x, double y) {
        this.x = x;
        this.y = y;
    }

};

// Function to find the line given
// two points
static void lineFromPoints(point P, point Q,
                    double a, double b,
                    double c)
{
    a = Q.y - P.y;
    b = P.x - Q.x;
    c = a * (P.x) + b * (P.y);
}

// Function which converts the
// input line to its perpendicular
// bisector. It also inputs the
// points whose mid-point lies o
// on the bisector
static void perpenBisectorFromLine(point P, point Q,
                            double a, double b,
                            double c)
{

    // Find the mid point
    point mid_point = new point();

    // x coordinates
    mid_point.x = (P.x + Q.x) / 2;

    // y coordinates
    mid_point.y = (P.y + Q.y) / 2;

    // c = -bx + ay
    c = -b * (mid_point.x)
        + a * (mid_point.y);

    // Assign the coefficient of
    // a and b
    double temp = a;
    a = -b;
    b = temp;
}

// Returns the intersection point of
// two lines
static double LineInterX(double a1, double b1,
                  double c1, double a2,
                  double b2, double c2)
{

    // Find determinant
    double determ = a1 * b2 - a2 * b1;

    double x = (b2 * c1 - b1 * c2);
    x /= determ;

    return x;
}

// Returns the intersection point of
// two lines
static double LineInterY(double a1, double b1,
                  double c1, double a2,
                  double b2, double c2)
{

    // Find determinant
    double determ = a1 * b2 - a2 * b1;

    double y = (a1 * c2 - a2 * c1);
    y /= determ;

    return y;
}

// Function to find the point
// lies inside, outside or on
// the circle
static void findPosition(point P, point Q,
                  point R, point D)
{

    // Store the coordinates
    // radius of circumcircle
    point r = new point();

    // Line PQ is represented
    // as ax + by = c
    double a = 0, b = 0, c = 0;
    lineFromPoints(P, Q, a, b, c);

    // Line QR is represented
    // as ex + fy = g
    double e = 0, f = 0, g = 0;
    lineFromPoints(Q, R, e, f, g);

    // Converting lines PQ and QR
    // to perpendicular bisectors.
    // After this, L = ax + by = c
    // M = ex + fy = g
    perpenBisectorFromLine(P, Q, a, b, c);
    perpenBisectorFromLine(Q, R, e, f, g);

    // The point of intersection
    // of L and M gives r as the
    // circumcenter
    r.x = LineInterX(a, b, c, e, f, g);
    r.y = LineInterY(a, b, c, e, f, g);

    // Length of radius
    double q = (r.x - P.x) * (r.x - P.x)
               + (r.y - P.y) * (r.y - P.y);

    // Distance between radius
    // and the given point D
    double dis = (r.x - D.x) * (r.x - D.x)
                 + (r.y - D.y) * (r.y - D.y);

    // Condition for point lies
    // inside circumcircle
    if (dis < q) {
        System.out.print("Point (" +  D.x+ ", "
             + D.y+ ") is inside "
            + "the circumcircle");
    }

    // Condition for point lies
    // on circumcircle
    else if (dis == q) {
        System.out.print("Point (" +  D.x+ ", "
             + D.y+ ") lies on the "
            + "circumcircle");
    }

    // Condition for point lies
    // outside circumcircle
    else {
        System.out.print("Point (" +  D.x+ ", "
             + D.y+ ") lies outside"
            + " the circumcircle");
    }
}

// Driver Code
public static void main(String[] args)
{
    point A, B, C, D;

    // Given Points
    A = new point(2, 8 );
    B = new point(2, 1 );
    C = new point(4, 5 );
    D = new point(3, 0 );

    // Function call to find
    // the point lies inside,
    // outside or on the
    // circle
    findPosition(A, B, C, D);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the points
# which lies inside, outside or
# on the circle

# Function to find the line given
# two points
def lineFromPoints(P, Q, a, b, c):

    a = Q[1] - P[1]
    b = P[0] - Q[0]
    c = a * (P[0]) + b * (P[1])

    return a, b, c

# Function which converts the
# input line to its perpendicular
# bisector. It also inputs the
# points whose mid-lies o
# on the bisector
def perpenBisectorFromLine(P, Q, a, b, c):

    # Find the mid point
    mid_point = [0, 0]

    # x coordinates
    mid_point[0] = (P[0] + Q[0]) / 2

    # y coordinates
    mid_point[1] = (P[1] + Q[1]) / 2

    # c = -bx + ay
    c = (-b * (mid_point[0]) +
          a * (mid_point[1]))

    # Assign the coefficient of
    # a and b
    temp = a
    a = -b
    b = temp

    return a, b, c

# Returns the intersection of
# two lines
def LineInterX(a1, b1, c1, a2, b2, c2):

    # Find determinant
    determ = a1 * b2 - a2 * b1

    x = (b2 * c1 - b1 * c2)
    x /= determ

    return x

# Returns the intersection of
# two lines
def LineInterY(a1, b1, c1, a2, b2, c2):

    # Find determinant
    determ = a1 * b2 - a2 * b1

    y = (a1 * c2 - a2 * c1)

    #print(y)
    y /= determ

    return y

# Function to find the point
# lies inside, outside or on
# the circle
def findPosition(P, Q, R, D):

    # Store the coordinates
    # radius of circumcircle
    r = [0, 0]

    # Line PQ is represented
    # as ax + by = c
    a, b, c = lineFromPoints(P, Q, 0, 0, 0)

    # Line QR is represented
    # as ex + fy = g
    e, f, g = lineFromPoints(Q, R, 0, 0, 0)

    # Converting lines PQ and QR
    # to perpendicular bisectors.
    # After this, L = ax + by = c
    # M = ex + fy = g
    a, b, c = perpenBisectorFromLine(P, Q,
                                     a, b, c)
    e, f, g = perpenBisectorFromLine(Q, R,
                                     e, f, g)

    # The of intersection
    # of L and M gives r as the
    # circumcenter
    r[0] = LineInterX(a, b, c, e, f, g)
    r[1] = LineInterY(a, b, c, e, f, g)

    # Length of radius
    q = ((r[0] - P[0]) *
         (r[0] - P[0]) +
         (r[1] - P[1]) *
         (r[1] - P[1]))

    # Distance between radius
    # and the given D
    dis = ((r[0] - D[0]) *
           (r[0] - D[0]) +
           (r[1] - D[1]) *
           (r[1] - D[1]))

    # Condition for lies
    # inside circumcircle
    if (dis < q):
        print("Point (", D[0], ",", D[1],
              ") is inside the circumcircle")

    # Condition for lies
    # on circumcircle
    elif (dis == q):
        print("Point (", D[0], ",", D[1],
              ") lies on the circumcircle")

    # Condition for lies
    # outside circumcircle
    else:
        print("Point (", D[0], ",", D[1],
              ") lies outside the circumcircle")

# Driver Code
if __name__ == '__main__':

    # A, B, C, D

    # Given Points
    A = [2, 8]
    B = [2, 1]
    C = [4, 5]
    D = [3, 0]

    # Function call to find
    # the lies inside,
    # outside or on the
    # circle
    findPosition(A, B, C, D)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the points
// which lies inside, outside or
// on the circle
using System;

class GFG{

// Structure Pointer to
// store x and y coordinates
class point {
    public double x, y;
    public point() {
    }
    public point(double x, double y) {
        this.x = x;
        this.y = y;
    }

};

// Function to find the line given
// two points
static void lineFromPoints(point P, point Q,
                    double a, double b,
                    double c)
{
    a = Q.y - P.y;
    b = P.x - Q.x;
    c = a * (P.x) + b * (P.y);
}

// Function which converts the
// input line to its perpendicular
// bisector. It also inputs the
// points whose mid-point lies o
// on the bisector
static void perpenBisectorFromLine(point P, point Q,
                            double a, double b,
                            double c)
{

    // Find the mid point
    point mid_point = new point();

    // x coordinates
    mid_point.x = (P.x + Q.x) / 2;

    // y coordinates
    mid_point.y = (P.y + Q.y) / 2;

    // c = -bx + ay
    c = -b * (mid_point.x)
        + a * (mid_point.y);

    // Assign the coefficient of
    // a and b
    double temp = a;
    a = -b;
    b = temp;
}

// Returns the intersection point of
// two lines
static double LineInterX(double a1, double b1,
                  double c1, double a2,
                  double b2, double c2)
{

    // Find determinant
    double determ = a1 * b2 - a2 * b1;

    double x = (b2 * c1 - b1 * c2);
    x /= determ;

    return x;
}

// Returns the intersection point of
// two lines
static double LineInterY(double a1, double b1,
                  double c1, double a2,
                  double b2, double c2)
{

    // Find determinant
    double determ = a1 * b2 - a2 * b1;

    double y = (a1 * c2 - a2 * c1);
    y /= determ;

    return y;
}

// Function to find the point
// lies inside, outside or on
// the circle
static void findPosition(point P, point Q,
                  point R, point D)
{

    // Store the coordinates
    // radius of circumcircle
    point r = new point();

    // Line PQ is represented
    // as ax + by = c
    double a = 0, b = 0, c = 0;
    lineFromPoints(P, Q, a, b, c);

    // Line QR is represented
    // as ex + fy = g
    double e = 0, f = 0, g = 0;
    lineFromPoints(Q, R, e, f, g);

    // Converting lines PQ and QR
    // to perpendicular bisectors.
    // After this, L = ax + by = c
    // M = ex + fy = g
    perpenBisectorFromLine(P, Q, a, b, c);
    perpenBisectorFromLine(Q, R, e, f, g);

    // The point of intersection
    // of L and M gives r as the
    // circumcenter
    r.x = LineInterX(a, b, c, e, f, g);
    r.y = LineInterY(a, b, c, e, f, g);

    // Length of radius
    double q = (r.x - P.x) * (r.x - P.x)
               + (r.y - P.y) * (r.y - P.y);

    // Distance between radius
    // and the given point D
    double dis = (r.x - D.x) * (r.x - D.x)
                 + (r.y - D.y) * (r.y - D.y);

    // Condition for point lies
    // inside circumcircle
    if (dis < q) {
        Console.Write("Point (" +  D.x+ ", "
             + D.y+ ") is inside "
            + "the circumcircle");
    }

    // Condition for point lies
    // on circumcircle
    else if (dis == q) {
        Console.Write("Point (" +  D.x+ ", "
             + D.y+ ") lies on the "
            + "circumcircle");
    }

    // Condition for point lies
    // outside circumcircle
    else {
        Console.Write("Point (" +  D.x+ ", "
             + D.y+ ") lies outside"
            + " the circumcircle");
    }
}

// Driver Code
public static void Main(String[] args)
{
    point A, B, C, D;

    // Given Points
    A = new point(2, 8 );
    B = new point(2, 1 );
    C = new point(4, 5 );
    D = new point(3, 0 );

    // Function call to find
    // the point lies inside,
    // outside or on the
    // circle
    findPosition(A, B, C, D);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find the points
// which lies inside, outside or
// on the circle

// Structure Pointer to
// store x and y coordinates
class point
{
    constructor(x,y)
    {
        this.x = x;
        this.y = y;
    }
}

// Function to find the line given
// two points
function lineFromPoints(P, Q, a, b, c)
{
    a = Q.y - P.y;
    b = P.x - Q.x;
    c = a * (P.x) + b * (P.y);
}

// Function which converts the
// input line to its perpendicular
// bisector. It also inputs the
// points whose mid-point lies o
// on the bisector
function perpenBisectorFromLine(P, Q, a, b, c)
{

    // Find the mid point
    let mid_point = new point();

    // x coordinates
    mid_point.x = (P.x + Q.x) / 2;

    // y coordinates
    mid_point.y = (P.y + Q.y) / 2;

    // c = -bx + ay
    c = -b * (mid_point.x)
        + a * (mid_point.y);

    // Assign the coefficient of
    // a and b
    let temp = a;
    a = -b;
    b = temp;
}

// Returns the intersection point of
// two lines
function LineInterX(a1, b1, c1, a2, b2, c2)
{

    // Find determinant
    let determ = a1 * b2 - a2 * b1;

    let x = (b2 * c1 - b1 * c2);
    x /= determ;

    return x;
}

// Returns the intersection point of
// two lines
function LineInterY(a1, b1, c1, a2, b2, c2)
{
    // Find determinant
    let determ = a1 * b2 - a2 * b1;

    let y = (a1 * c2 - a2 * c1);
    y /= determ;

    return y;
}

// Function to find the point
// lies inside, outside or on
// the circle
function findPosition(P, Q, R, D)
{

    // Store the coordinates
    // radius of circumcircle
    let r = new point();

    // Line PQ is represented
    // as ax + by = c
    let a = 0, b = 0, c = 0;
    lineFromPoints(P, Q, a, b, c);

    // Line QR is represented
    // as ex + fy = g
    let e = 0, f = 0, g = 0;
    lineFromPoints(Q, R, e, f, g);

    // Converting lines PQ and QR
    // to perpendicular bisectors.
    // After this, L = ax + by = c
    // M = ex + fy = g
    perpenBisectorFromLine(P, Q, a, b, c);
    perpenBisectorFromLine(Q, R, e, f, g);

    // The point of intersection
    // of L and M gives r as the
    // circumcenter
    r.x = LineInterX(a, b, c, e, f, g);
    r.y = LineInterY(a, b, c, e, f, g);

    // Length of radius
    let q = (r.x - P.x) * (r.x - P.x)
               + (r.y - P.y) * (r.y - P.y);

    // Distance between radius
    // and the given point D
    let dis = (r.x - D.x) * (r.x - D.x)
                 + (r.y - D.y) * (r.y - D.y);

    // Condition for point lies
    // inside circumcircle
    if (dis < q) {
        document.write("Point (" +  D.x+ ", "
             + D.y+ ") is inside "
            + "the circumcircle");
    }

    // Condition for point lies
    // on circumcircle
    else if (dis == q) {
        document.write("Point (" +  D.x+ ", "
             + D.y+ ") lies on the "
            + "circumcircle");
    }

    // Condition for point lies
    // outside circumcircle
    else {
        document.write("Point (" +  D.x+ ", "
             + D.y+ ") lies outside"
            + " the circumcircle");
    }
}

// Driver Code
let A, B, C, D;

// Given Points
A = new point(2, 8 );
B = new point(2, 1 );
C = new point(4, 5 );
D = new point(3, 0 );

// Function call to find
// the point lies inside,
// outside or on the
// circle
findPosition(A, B, C, D);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
Point (3, 0) lies outside the circumcircle
```