# 找出一个点是否位于圆内

> 原文:[https://www . geesforgeks . org/find-if-a-point-lies-in-or-on-circle/](https://www.geeksforgeeks.org/find-if-a-point-lies-inside-or-on-circle/)

给定一个圆(圆心和半径的坐标)和一个点(坐标)，找出该点是在圆内还是在圆上。

**示例:**

```
Input: x = 4, y = 4 // Given Point
       circle_x = 1, circle_y = 1, rad = 6; // Circle
Output: Inside 

Input: x = 3, y = 3 // Given Point
       circle_x = 0, circle_y = 1, rad = 2; // Circle
Output: Outside
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**

这个想法是计算点到中心的距离。如果距离小于或等于半径。重点在里面，在外面。

以下是上述想法的实现。

## C++

```
// C++ program to check if a point
// lies inside a circle or not
#include <bits/stdc++.h>
using namespace std;

bool isInside(int circle_x, int circle_y,
                   int rad, int x, int y)
{
    // Compare radius of circle with distance
    // of its center from given point
    if ((x - circle_x) * (x - circle_x) +
        (y - circle_y) * (y - circle_y) <= rad * rad)
        return true;
    else
        return false;
}

// Driver function
int main()
{
    int x = 1, y = 1;
    int circle_x = 0, circle_y = 1, rad = 2;
    isInside(circle_x, circle_y, rad, x, y) ?
    cout << "Inside" : cout << "Outside";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a point lies
// inside a circle or not

class GFG {

    static boolean isInside(int circle_x, int circle_y,
                                 int rad, int x, int y)
    {
        // Compare radius of circle with
        // distance of its center from
        // given point
        if ((x - circle_x) * (x - circle_x) +
            (y - circle_y) * (y - circle_y) <= rad * rad)
            return true;
        else
            return false;
    }

    // Driver Program to test above function
    public static void main(String arg[])
    {
        int x = 1, y = 1;
        int circle_x = 0, circle_y = 1, rad = 2;

        if (isInside(circle_x, circle_y, rad, x, y))
            System.out.print("Inside");
        else
            System.out.print("Outside");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to check if
# a point lies inside a circle
# or not

def isInside(circle_x, circle_y, rad, x, y):

    # Compare radius of circle
    # with distance of its center
    # from given point
    if ((x - circle_x) * (x - circle_x) +
        (y - circle_y) * (y - circle_y) <= rad * rad):
        return True;
    else:
        return False;

# Driver Code
x = 1;
y = 1;
circle_x = 0;
circle_y = 1;
rad = 2;
if(isInside(circle_x, circle_y, rad, x, y)):
    print("Inside");
else:
    print("Outside");

# This code is contributed
# by mits.
```

## C#

```
// C# program to check if a point lies
// inside a circle or not
using System;

class GFG {

    static bool isInside(int circle_x, int circle_y,
                              int rad, int x, int y)
    {
        // Compare radius of circle with
        // distance of its center from
        // given point
        if ((x - circle_x) * (x - circle_x) +
            (y - circle_y) * (y - circle_y)    <= rad * rad)
            return true;
        else
            return false;
    }

    // Driver Program to test above function
    public static void Main()
    {
        int x = 1, y = 1;
        int circle_x = 0, circle_y = 1, rad = 2;

        if (isInside(circle_x, circle_y, rad, x, y))
            Console.Write("Inside");
        else
            Console.Write("Outside");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a point
// lies inside a circle or not

function isInside($circle_x, $circle_y,
                          $rad, $x, $y)
{
    // Compare radius of circle
    // with distance of its center
    // from given point
    if (($x - $circle_x) * ($x - $circle_x) +
        ($y - $circle_y) * ($y - $circle_y) <=
                               $rad * $rad)
        return true;
    else
        return false;
}

// Driver Code
$x = 1; $y = 1;
$circle_x = 0; $circle_y = 1; $rad = 2;
if(isInside($circle_x, $circle_y,
            $rad, $x, $y))
echo "Inside";
else
echo "Outside";

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a point
// lies inside a circle or not
function isInside(circle_x, circle_y, rad, x, y)
{

    // Compare radius of circle with
    // distance of its center from
    // given point

    if ((x - circle_x) * (x - circle_x) +
        (y - circle_y) * (y - circle_y) <= rad * rad)
        return true;
    else
        return false;
}

// Driver code
var x = 1;
var y = 1;
var circle_x = 0;
var circle_y = 1;
var rad = 2;

if (isInside(circle_x, circle_y, rad, x, y))
{
    document.write("Inside");
}
else
{
    document.write("Outside");
}

// This code is contributed by bunnyram19

</script>
```

**输出:**

```
Inside
```

感谢 Utkarsh Trivedi 对上述解决方案的建议
如发现任何不正确的地方，或者您想分享更多关于上述讨论主题的信息，请写评论。