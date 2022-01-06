# 计数在给定点相交的直线

> 原文:[https://www . geesforgeks . org/count-直线-在给定点相交/](https://www.geeksforgeeks.org/count-straight-lines-intersecting-at-a-given-point/)

给定大小为 **N * 3** 的矩阵**行[][]** ，使得 i <sup>第</sup>行表示具有等式**行[i][0] * x +行[i][1]*y =行[i][2]** 的行，以及整数 **X** 和 **Y** ，表示点 **(X，Y)** 的坐标，任务是从给定矩阵中计算行数

**示例:**

> **输入:** N=5，X = 3，Y = 4，line[][]= { { 4，-1，8}，{2，-7，-2}，{1，1，7}，{1，-3，5}，{1，0，3}}
> **输出:** 3
> **解释:**
> 线 4 * X–Y = 8，1*x + 1* y = 7 和 1 * X–0 * Y = 3 在点(3，3
> 
> **输入:** N=4，X = -2，Y = 3，line[][]= { { 3，-2，-12}，{1，3，5}，{1，-1，-5}，{2，3，4}}
> 输出:2
> T6】解释:T8】line 3 * X–2 * Y =-12 和 1 * X–1 * Y =-5 在点(-2，3)相交。

**天真法:**解决问题最简单的方法是，对于每一条线，找到它与其他线的交点，检查它们是否在给定点 **(X，Y)** 相交。最后，打印在 **(X，Y)相交的行数。**
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过观察进行优化:

> 如果两条直线经过同一个点，那么它们肯定会在那个点相交。

按照以下步骤解决问题:

1.  所以，计算通过给定点的行数，让行数为 **cnt** 。
2.  计算完上述步骤后，打印交点总数:

> 在(X，Y)=**<sup>CNT</sup>C<sub>2</sub>**处相交的 ***cnt*** 线的交点计数

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure to store point
struct Point {

    int x, y;
};

// Structure to store line
struct Line {

    int a, b, c;
};

// Function to check if a line
// passes through a point or not
bool point_lies_on_line(Line l,
                        Point p)
{
    // Condition for the line
    // to pass through point p
    if (l.a * p.x + l.b * p.y
        == l.c) {

        return true;
    }
    return false;
}

// Function to find lines
// intersecting at a given point
int intersecting_at_point(
    vector<Line>& lines, Point p)
{
    int cnt = 0;
    for (int i = 0; i < lines.size(); i++) {

        // If the point lies on a line
        if (point_lies_on_line(lines[i], p)) {

            // Increment cnt
            cnt++;
        }
    }

    // Count of intersections
    int ans = (cnt * (cnt - 1)) / 2;

    // Return answer
    return ans;
}

// Driver Code
int main()
{
    // Number of lines
    int N = 5;

    // Point (x, y)
    Point p = { 3, 4 };

    // Array to store the lines
    vector<Line> lines;
    lines.push_back({ 4, -1, 8 });
    lines.push_back({ 1, 0, 3 });
    lines.push_back({ 1, 1, 7 });
    lines.push_back({ 2, -7, -2 });
    lines.push_back({ 1, -3, 5 });

    // Function call
    int ans = intersecting_at_point(lines, p);

    cout << ans << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Structure to store point
static class Point
{
    int x, y;

    public Point(int x, int y)
    {
        super();
        this.x = x;
        this.y = y;
    }
};

// Structure to store line
static class Line
{
    int a, b, c;

    public Line(int a, int b, int c)
    {
        super();
        this.a = a;
        this.b = b;
        this.c = c;
    }
};

// Function to check if a line
// passes through a point or not
static boolean point_lies_on_line(Line l,
                                  Point p)
{

    // Condition for the line
    // to pass through point p
    if (l.a * p.x + l.b * p.y == l.c)
    {
        return true;
    }
    return false;
}

// Function to find lines
// intersecting at a given point
static int intersecting_at_point(Vector<Line> lines,
                                 Point p)
{
    int cnt = 0;
    for(int i = 0; i < lines.size(); i++)
    {

        // If the point lies on a line
        if (point_lies_on_line(lines.get(i), p))
        {

            // Increment cnt
            cnt++;
        }
    }

    // Count of intersections
    int ans = (cnt * (cnt - 1)) / 2;

    // Return answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Number of lines
    int N = 5;

    // Point (x, y)
    Point p = new Point(3, 4);

    // Array to store the lines
    Vector<Line> lines = new Vector<Line>();
    lines.add(new Line(4, -1, 8));
    lines.add(new Line(1, 0, 3));
    lines.add(new Line(1, 1, 7));
    lines.add(new Line(2, -7, -2));
    lines.add(new Line(1, -3, 5));

    // Function call
    int ans = intersecting_at_point(lines, p);

    System.out.print(ans + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a line
# passes through a poor not
def point_lies_on_line(l, p):

    # Condition for the line
    # to pass through pop
    if (l[0] * p[0] + l[1] * p[1] == l[2]):
        return True

    return False

# Function to find lines
# intersecting at a given point
def intersecting_at_point(lines, p):

    cnt = 0
    for i in range(len(lines)):

        # If the polies on a line
        if (point_lies_on_line(lines[i], p)):

            # Increment cnt
            cnt += 1

    # Count of intersections
    ans = (cnt * (cnt - 1)) // 2

    # Return answer
    return ans

# Driver Code
if __name__ == '__main__':

    # Number of lines
    N = 5

    # Po(x, y)
    p = [ 3, 4 ]

    # Array to store the lines
    lines = []
    lines.append([ 4, -1, 8 ])
    lines.append([ 1, 0, 3 ])
    lines.append([ 1, 1, 7 ])
    lines.append([ 2, -7, -2 ])
    lines.append([ 1, -3, 5 ])

    # Function call
    ans = intersecting_at_point(lines, p)

    print(ans)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Structure to store point
class Point
{
  public int x, y;
  public Point(int x, int y)
  {
    this.x = x;
    this.y = y;
  }
};

// Structure to store line
class Line
{
  public int a, b, c;
  public Line(int a,
              int b, int c)
  {
    this.a = a;
    this.b = b;
    this.c = c;
  }
};

// Function to check if a line
// passes through a point or not
static bool point_lies_on_line(Line l,
                               Point p)
{  
  // Condition for the line
  // to pass through point p
  if (l.a * p.x + l.b * p.y == l.c)
  {
    return true;
  }
  return false;
}

// Function to find lines
// intersecting at a given point
static int intersecting_at_point(List<Line> lines,
                                 Point p)
{
  int cnt = 0;
  for(int i = 0; i < lines.Count; i++)
  {       
    // If the point lies on a line
    if (point_lies_on_line(lines[i], p))
    {           
      // Increment cnt
      cnt++;
    }
  }

  // Count of intersections
  int ans = (cnt * (cnt - 1)) / 2;

  // Return answer
  return ans;
}

// Driver Code
public static void Main(String[] args)
{   
  // Number of lines
  int N = 5;

  // Point (x, y)
  Point p = new Point(3, 4);

  // Array to store the lines
  List<Line> lines = new List<Line>();
  lines.Add(new Line(4, -1, 8));
  lines.Add(new Line(1, 0, 3));
  lines.Add(new Line(1, 1, 7));
  lines.Add(new Line(2, -7, -2));
  lines.Add(new Line(1, -3, 5));

  // Function call
  int ans = intersecting_at_point(lines, p);

  Console.Write(ans + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to check if a line
// passes through a point or not
function point_lies_on_line(l, p)
{
    // Condition for the line
    // to pass through point p
    if (l[0] * p[0] + l[1] * p[1]
        == l[2]) {

        return true;
    }
    return false;
}

// Function to find lines
// intersecting at a given point
function intersecting_at_point( lines, p)
{
    var cnt = 0;
    for (var i = 0; i < lines.length; i++) {

        // If the point lies on a line
        if (point_lies_on_line(lines[i], p)) {

            // Increment cnt
            cnt++;
        }
    }

    // Count of intersections
    var ans = (cnt * (cnt - 1)) / 2;

    // Return answer
    return ans;
}

// Driver Code

// Number of lines
var N = 5;

// Point (x, y)
var p = [3, 4];

// Array to store the lines
var lines = [];
lines.push([ 4, -1, 8 ]);
lines.push([ 1, 0, 3 ]);
lines.push([ 1, 1, 7 ]);
lines.push([ 2, -7, -2 ]);
lines.push([ 1, -3, 5 ]);

// Function call
var ans = intersecting_at_point(lines, p);
document.write( ans );

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)