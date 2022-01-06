# 最小封闭圆|集合 2–韦尔兹算法

> 原文:[https://www . geesforgeks . org/minimum-enclosing-circle-set-2-welzls-algorithm/](https://www.geeksforgeeks.org/minimum-enclosing-circle-set-2-welzls-algorithm/)

**前提:** [圆上三点给定时的圆方程](https://www.geeksforgeeks.org/equation-of-circle-when-three-points-on-the-circle-are-given/)、[最小包围圆](https://www.geeksforgeeks.org/minimum-enclosing-circle-set-1/?ref=rp)。
给定一个数组 **arr[][]** ，该数组包含二维平面中整数坐标的 **N 个**点。任务是找到最小封闭圆(MEC)的中心和半径。最小封闭圆是所有点都位于圆内或圆边界上的圆。
**举例:**

> **输入:** arr[][] = {{0，0}，{0，1}，{1，0}}
> **输出:**中心= {0.5，0.5}，半径= 0.7071
> **说明:**
> 在绘制上述半径为 0.707，中心为(0.5，0.5)的圆时，可以清楚地观察到，所有提到的点都位于圆内或圆上。
> 
> ![](img/b4ede2eab8f8bcfacc965fda22123225.png)
> 
> **输入:** arr[][] = {{5，-2}、{-3，-2}、{-2，5}、{1，6}、{0，2}}
> **输出:**中心= {1.0，1.0}，半径= 5.000

**方法:**在前一篇文章中，已经讨论了一种朴素方法和一种通过首先获得点集的凸满，然后执行朴素方法的优化方法。尽管优化后的解决方案对某些输入非常有效，但优化后的最坏情况时间复杂度仍然是 **O(N <sup>4</sup> )** 。本文讨论了一种优化方法。
思路是用 [Welzl 的递归算法](https://en.wikipedia.org/wiki/Smallest-circle_problem#Welzl's_algorithm)。使用该算法，可以在 **O(N)** 中找到 MEC。算法的工作取决于从上一篇文章中得出的观察结果和结论。该算法的思想是从给定的输入集中随机移除一个点，形成一个圆方程。一旦方程形成，检查被移除的点是否被方程包围。如果没有，那么这个点一定在 MEC 的边界上。因此，该点被视为边界点，并递归调用函数。该算法的具体工作如下:
该算法以一组最初为空的用于表示 MEC 边界上的点的点 **P** 和一组 **R** 作为输入。
算法的基本情况是当 **P** 变空或者集合 **R** 的大小等于 **3** :

*   如果 P 为空，则所有的点都已被处理。
*   如果 **|R| = 3** ，那么已经找到位于圆边界上的 3 个点，并且由于仅使用 3 个点就可以唯一确定一个圆，所以可以停止递归。

当算法到达上述基本情况时，返回 R 的平凡解，为:

*   如果 **|R| = 1** ，我们返回一个半径= 0，以 R[0]为中心的圆
*   如果 **|R| = 2** ，我们返回 R[0]和 R[2]的 MEC
*   如果 **|R| = 3** ，我们通过尝试 3 对(R[0]，R[1])，(R[0]，R[2])，(R[1]，R[2])来返回 MEC
    *   如果这些对都无效，我们返回由 R 中的 3 个点定义的圆

如果尚未达到基本情况，我们执行以下操作:

*   从 P 中选一个随机点 P，然后从 P 中去掉它
*   调用 P 和 R 上的算法得到圆 d
*   如果 p 用 d 括起来，那么我们返回 d
*   否则，p 必须位于 MEC 的边界上
    *   将 p 添加到 R
    *   返回 P 和 R 上的算法输出

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the minimum enclosing
// circle for N integer points in a 2-D plane
#include <algorithm>
#include <assert.h>
#include <iostream>
#include <math.h>
#include <vector>
using namespace std;

// Defining infinity
const double INF = 1e18;

// Structure to represent a 2D point
struct Point {
    double X, Y;
};

// Structure to represent a 2D circle
struct Circle {
    Point C;
    double R;
};

// Function to return the euclidean distance
// between two points
double dist(const Point& a, const Point& b)
{
    return sqrt(pow(a.X - b.X, 2)
                + pow(a.Y - b.Y, 2));
}

// Function to check whether a point lies inside
// or on the boundaries of the circle
bool is_inside(const Circle& c, const Point& p)
{
    return dist(c.C, p) <= c.R;
}

// The following two functions are used
// To find the equation of the circle when
// three points are given.

// Helper method to get a circle defined by 3 points
Point get_circle_center(double bx, double by,
                        double cx, double cy)
{
    double B = bx * bx + by * by;
    double C = cx * cx + cy * cy;
    double D = bx * cy - by * cx;
    return { (cy * B - by * C) / (2 * D),
             (bx * C - cx * B) / (2 * D) };
}

// Function to return a unique circle that
// intersects three points
Circle circle_from(const Point& A, const Point& B,
                   const Point& C)
{
    Point I = get_circle_center(B.X - A.X, B.Y - A.Y,
                                C.X - A.X, C.Y - A.Y);

    I.X += A.X;
    I.Y += A.Y;
    return { I, dist(I, A) };
}

// Function to return the smallest circle
// that intersects 2 points
Circle circle_from(const Point& A, const Point& B)
{
    // Set the center to be the midpoint of A and B
    Point C = { (A.X + B.X) / 2.0, (A.Y + B.Y) / 2.0 };

    // Set the radius to be half the distance AB
    return { C, dist(A, B) / 2.0 };
}

// Function to check whether a circle
// encloses the given points
bool is_valid_circle(const Circle& c,
                     const vector<Point>& P)
{

    // Iterating through all the points
    // to check  whether the points
    // lie inside the circle or not
    for (const Point& p : P)
        if (!is_inside(c, p))
            return false;
    return true;
}

// Function to return the minimum enclosing
// circle for N <= 3
Circle min_circle_trivial(vector<Point>& P)
{
    assert(P.size() <= 3);
    if (P.empty()) {
        return { { 0, 0 }, 0 };
    }
    else if (P.size() == 1) {
        return { P[0], 0 };
    }
    else if (P.size() == 2) {
        return circle_from(P[0], P[1]);
    }

    // To check if MEC can be determined
    // by 2 points only
    for (int i = 0; i < 3; i++) {
        for (int j = i + 1; j < 3; j++) {

            Circle c = circle_from(P[i], P[j]);
            if (is_valid_circle(c, P))
                return c;
        }
    }
    return circle_from(P[0], P[1], P[2]);
}

// Returns the MEC using Welzl's algorithm
// Takes a set of input points P and a set R
// points on the circle boundary.
// n represents the number of points in P
// that are not yet processed.
Circle welzl_helper(vector<Point>& P,
                    vector<Point> R, int n)
{
    // Base case when all points processed or |R| = 3
    if (n == 0 || R.size() == 3) {
        return min_circle_trivial(R);
    }

    // Pick a random point randomly
    int idx = rand() % n;
    Point p = P[idx];

    // Put the picked point at the end of P
    // since it's more efficient than
    // deleting from the middle of the vector
    swap(P[idx], P[n - 1]);

    // Get the MEC circle d from the
    // set of points P - {p}
    Circle d = welzl_helper(P, R, n - 1);

    // If d contains p, return d
    if (is_inside(d, p)) {
        return d;
    }

    // Otherwise, must be on the boundary of the MEC
    R.push_back(p);

    // Return the MEC for P - {p} and R U {p}
    return welzl_helper(P, R, n - 1);
}

Circle welzl(const vector<Point>& P)
{
    vector<Point> P_copy = P;
    random_shuffle(P_copy.begin(), P_copy.end());
    return welzl_helper(P_copy, {}, P_copy.size());
}

// Driver code
int main()
{
    Circle mec = welzl({ { 0, 0 },
                         { 0, 1 },
                         { 1, 0 } });
    cout << "Center = { " << mec.C.X << ", " << mec.C.Y
         << " } Radius = " << mec.R << endl;

    Circle mec2 = welzl({ { 5, -2 },
                          { -3, -2 },
                          { -2, 5 },
                          { 1, 6 },
                          { 0, 2 } });
    cout << "Center = { " << mec2.C.X << ", " << mec2.C.Y
         << " } Radius = " << mec2.R << endl;

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find the minimum enclosing
# circle for N integer points in a 2-D plane
from math import sqrt
from random import randint,shuffle

# Defining infinity
INF = 1e18

# Structure to represent a 2D point
class Point :
    def __init__(self,X=0,Y=0) -> None:
        self.X=X
        self.Y=Y

# Structure to represent a 2D circle
class Circle :
    def __init__(self,c=Point(),r=0) -> None:       
        self.C=c
        self.R=r

# Function to return the euclidean distance
# between two points
def dist(a, b):
    return sqrt(pow(a.X - b.X, 2)
                + pow(a.Y - b.Y, 2))

# Function to check whether a point lies inside
# or on the boundaries of the circle
def is_inside(c, p):
    return dist(c.C, p) <= c.R

# The following two functions are used
# To find the equation of the circle when
# three points are given.

# Helper method to get a circle defined by 3 points
def get_circle_center(bx, by,
                        cx, cy):
    B = bx * bx + by * by
    C = cx * cx + cy * cy
    D = bx * cy - by * cx
    return Point((cy * B - by * C) / (2 * D),
             (bx * C - cx * B) / (2 * D))

# Function to return the smallest circle
# that intersects 2 points
def circle_from1(A, B):
    # Set the center to be the midpoint of A and B
    C = Point((A.X + B.X) / 2.0, (A.Y + B.Y) / 2.0 )

    # Set the radius to be half the distance AB
    return Circle(C, dist(A, B) / 2.0 )

# Function to return a unique circle that
# intersects three points
def circle_from2(A, B, C):
    I = get_circle_center(B.X - A.X, B.Y - A.Y,
                                C.X - A.X, C.Y - A.Y)

    I.X += A.X
    I.Y += A.Y
    return Circle(I, dist(I, A))

# Function to check whether a circle
# encloses the given points
def is_valid_circle(c, P):

    # Iterating through all the points
    # to check  whether the points
    # lie inside the circle or not
    for p in P:
        if (not is_inside(c, p)):
            return False
    return True

# Function to return the minimum enclosing
# circle for N <= 3
def min_circle_trivial(P):
    assert(len(P) <= 3)
    if not P :
        return Circle()

    elif (len(P) == 1) :
        return Circle(P[0], 0)

    elif (len(P) == 2) :
        return circle_from1(P[0], P[1])

    # To check if MEC can be determined
    # by 2 points only
    for i in range(3):
        for j in range(i + 1,3):

            c = circle_from1(P[i], P[j])
            if (is_valid_circle(c, P)):
                return c

    return circle_from2(P[0], P[1], P[2])

# Returns the MEC using Welzl's algorithm
# Takes a set of input points P and a set R
# points on the circle boundary.
# n represents the number of points in P
# that are not yet processed.
def welzl_helper(P, R, n):
    # Base case when all points processed or |R| = 3
    if (n == 0 or len(R) == 3) :
        return min_circle_trivial(R)

    # Pick a random point randomly
    idx = randint(0,n-1)
    p = P[idx]

    # Put the picked point at the end of P
    # since it's more efficient than
    # deleting from the middle of the vector
    P[idx], P[n - 1]=P[n-1],P[idx]

    # Get the MEC circle d from the
    # set of points P - :p
    d = welzl_helper(P, R.copy(), n - 1)

    # If d contains p, return d
    if (is_inside(d, p)) :
        return d

    # Otherwise, must be on the boundary of the MEC
    R.append(p)

    # Return the MEC for P - :p and R U :p
    return welzl_helper(P, R.copy(), n - 1)

def welzl(P):
    P_copy = P.copy()
    shuffle(P_copy)
    return welzl_helper(P_copy, [], len(P_copy))

# Driver code
if __name__ == '__main__':
    mec = welzl([Point(0, 0) ,
                         Point(0, 1) ,
                         Point(1, 0)  ])
    print("Center = {",mec.C.X,",", mec.C.Y,"} Radius =",mec.R)

    mec2 = welzl([Point(5, -2) ,
                          Point(-3, -2) ,
                          Point(-2, 5) ,
                          Point(1, 6),
                          Point(0, 2)] )
    print("Center = {",mec2.C.X,",",mec2.C.Y,"} Radius =",mec2.R)
```

**Output:** 

```
Center = { 0.5, 0.5 } Radius = 0.707107
Center = { 1, 1 } Radius = 5
```

**时间复杂度:**该算法的期望时间和空间复杂度为 **O(N)** ，其中 N 为点数。这个空间是由于[递归](https://www.geeksforgeeks.org/recursion/)正在被使用。为了理解为什么时间复杂度是线性的，我们可以观察不同状态的数量，以知道递归函数可以发生多少次调用。每打一次电话， **P** 的尺寸减少**一**。此外，R 的大小可以保持不变，也可以增加一。由于 **|R|** 不能超过 **3** ，那么不同状态的数量为 **3N** 。因此，这使得时间复杂度为 **O(N)** 。