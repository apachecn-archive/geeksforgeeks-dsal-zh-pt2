# 为获得轴一侧的剩余点，需要移除的最小点数

> 原文:[https://www . geesforgeks . org/最小点数-移除-获取-剩余点数-单侧轴/](https://www.geeksforgeeks.org/minimum-number-points-removed-get-remaining-points-one-side-axis/)

我们在笛卡尔平面上被赋予 **n** 个点。我们的任务是找到应该移除的最小点数，以便获得任何轴一侧的剩余点。

**示例:**

```
Input : 4
        1 1
        2 2
       -1 -1
       -2 2
Output : 1
Explanation :
If we remove (-1, -1) then all the remaining 
points are above x-axis. Thus the answer is 1.

Input : 3
        1 10
        2 3
        4 11
Output : 0
Explanation :
All points are already above X-axis. Hence the
answer is 0\.  
```

**方法:**
这个问题是几何上构造性蛮力算法的一个简单例子。可以简单地通过找到 X 轴和 Y 轴所有边上的点数来解决这个问题。这将是最起码的答案。

## C++

```
// CPP program to find minimum points to be moved
// so that all points are on same side.
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

// Structure to store the coordinates of a point.
struct Point
{
    int x, y;
};

// Function to find the minimum number of points
int findmin(Point p[], int n)
{
    int a = 0, b = 0, c = 0, d = 0;
    for (int i = 0; i < n; i++)
    {
        // Number of points on the left of Y-axis.
        if (p[i].x <= 0)        
            a++;

        // Number of points on the right of Y-axis.
        else if (p[i].x >= 0)
            b++;

        // Number of points above X-axis.
        if (p[i].y >= 0)
            c++;

        // Number of points below X-axis.
        else if (p[i].y <= 0)
            d++;
    }

    return min({a, b, c, d});
}

// Driver Function
int main()
{
    Point p[] = { {1, 1}, {2, 2}, {-1, -1}, {-2, 2} };
    int n = sizeof(p)/sizeof(p[0]);
    cout << findmin(p, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum points to be moved
// so that all points are on same side.
import java.util.*;

class GFG
{

// Structure to store the coordinates of a point.
static class Point
{
    int x, y;

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
};

// Function to find the minimum number of points
static int findmin(Point p[], int n)
{
    int a = 0, b = 0, c = 0, d = 0;
    for (int i = 0; i < n; i++)
    {
        // Number of points on the left of Y-axis.
        if (p[i].x <= 0)    
            a++;

        // Number of points on the right of Y-axis.
        else if (p[i].x >= 0)
            b++;

        // Number of points above X-axis.
        if (p[i].y >= 0)
            c++;

        // Number of points below X-axis.
        else if (p[i].y <= 0)
            d++;
    }
    return Math.min(Math.min(a, b),
                    Math.min(c, d));
}

// Driver Code
public static void main(String[] args)
{
    Point p[] = {new Point(1, 1), new Point(2, 2),
                 new Point(-1, -1), new Point(-2, 2)};
    int n = p.length;
    System.out.println(findmin(p, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find minimum points to be
# moved so that all points are on same side.

# Function to find the minimum number
# of points
def findmin(p, n):

    a, b, c, d = 0, 0, 0, 0
    for i in range(n):

        # Number of points on the left
        # of Y-axis.
        if (p[i][0] <= 0):    
            a += 1

        # Number of points on the right
        # of Y-axis.
        elif (p[i][0] >= 0):
            b += 1

        # Number of points above X-axis.
        if (p[i][1] >= 0):
            c += 1

        # Number of points below X-axis.
        elif (p[i][1] <= 0):
            d += 1

    return min([a, b, c, d])

# Driver Code
p = [ [1, 1], [2, 2], [-1, -1], [-2, 2] ]
n = len(p)
print(findmin(p, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find minimum points to be moved
// so that all points are on same side.
using System;

class GFG
{

// Structure to store the coordinates of a point.
public class Point
{
    public int x, y;

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
};

// Function to find the minimum number of points
static int findmin(Point []p, int n)
{
    int a = 0, b = 0, c = 0, d = 0;
    for (int i = 0; i < n; i++)
    {
        // Number of points on the left of Y-axis.
        if (p[i].x <= 0)    
            a++;

        // Number of points on the right of Y-axis.
        else if (p[i].x >= 0)
            b++;

        // Number of points above X-axis.
        if (p[i].y >= 0)
            c++;

        // Number of points below X-axis.
        else if (p[i].y <= 0)
            d++;
    }
    return Math.Min(Math.Min(a, b),
                    Math.Min(c, d));
}

// Driver Code
public static void Main(String[] args)
{
    Point []p = {new Point(1, 1),
                 new Point(2, 2),
                 new Point(-1, -1),
                 new Point(-2, 2)};
    int n = p.Length;
    Console.WriteLine(findmin(p, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find minimum points to be moved
// so that all points are on same side.

    // Function to find the minimum number of points
    function findmin(p,n)
    {
        let a = 0, b = 0, c = 0, d = 0;
    for (let i = 0; i < n; i++)
    {
        // Number of points on the left of Y-axis.
        if (p[i][0] <= 0)    
            a++;

        // Number of points on the right of Y-axis.
        else if (p[i][0] >= 0)
            b++;

        // Number of points above X-axis.
        if (p[i][1] >= 0)
            c++;

        // Number of points below X-axis.
        else if (p[i][1] <= 0)
            d++;
    }
    return Math.min(Math.min(a, b),
                    Math.min(c, d));
    }

    // Driver Code
    let p = [ [1, 1], [2, 2], [-1, -1], [-2, 2] ]
    let n = p.length;
    document.write(findmin(p, n));

// This code is contributed by unknown2108

</script>
```

**输出:**

```
1
```