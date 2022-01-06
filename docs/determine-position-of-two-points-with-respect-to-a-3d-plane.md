# 确定两点相对于三维平面的位置

> 原文:[https://www . geeksforgeeks . org/确定两点相对于三维平面的位置/](https://www.geeksforgeeks.org/determine-position-of-two-points-with-respect-to-a-3d-plane/)

给定四个整数 **a** 、 **b** 、 **c** 和 **d** ，表示平面 **ax + by + cz + d = 0** 的[方程的系数，以及两个整数坐标 **(x1，y1，z1)** 和 **(x2，y2，z2)** ，任务是找出两个点是在同一侧，还是在不同侧](https://www.geeksforgeeks.org/program-to-find-equation-of-a-plane-passing-through-3-points/)

**示例:**

> **输入:** a = 1，b = 2，c = 3，d = 4，x1 = -2，y1 = -2，z1 = 1，x2 = -4，y2 = 11，z2 = -1
> **输出:**同侧
> **解释:**关于将 ax+上的(x1，y1，z1)和(x2，y2，z2)用+cz+d=0 分别给出 1 和 19，二者具有相同的符号，因此两个点位于同一侧
> 
> **输入:** a = 4，b = 2，c = 1，d = 3，x1 = -2，y1 = -2，z1 = 1，x2 = -4，y2 = 11，z2 = -1
> **输出:**不同侧

**方法:**这个想法是基于这样一个事实:如果应用于方程的两个点具有相同的宇称(符号)，那么它们将位于平面的同一侧，如果它们具有[不同的宇称](https://www.geeksforgeeks.org/detect-if-two-integers-have-opposite-signs/)，那么它们将位于平面的不同侧。按照以下步骤解决问题:

*   将给定点的坐标放在平面方程中，并将值存储在变量 **P1** 和 **P2** 中。
*   检查获得值的符号:
    *   如果 **P1** 和 **P2** 具有相同的宇称，那么它们在飞机的同一侧。
    *   如果 **P1** 和 **P2** 的宇称不同，那么它们位于飞机的相对两侧。
    *   如果 **P1** 和 **P2** 都为零，那么他们就躺在飞机上。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to check position of two
// points with respect to a plane in 3D
void check_position(int a, int b, int c, int d,
                    int x1, int y1, int z1,
                    int x2, int y2, int z2)
{
    // Put coordinates in plane equation
    int value_1 = a * x1 + b * y1 + c * z1 + d;
    int value_2 = a * x2 + b * y2 + c * z2 + d;

    // If both values have same sign
    if ((value_1 > 0 && value_2 > 0)
        || (value_1 < 0 && value_2 < 0))
        cout << "On same side";

    // If both values have different sign
    if ((value_1 > 0 && value_2 < 0)
        || (value_1 < 0 && value_2 > 0))
        cout << "On different sides";

    // If both values are zero
    if (value_1 == 0 && value_2 == 0)
        cout << "Both on the plane";

    // If either of the two values is zero
    if (value_1 == 0 && value_2 != 0)
        cout << "Point 1 on the plane";
    if (value_1 != 0 && value_2 == 0)
        cout << "Point 2 on the plane";
}

// Driver Code
int main()
{

    // Given Input
    int a = 1, b = 2, c = 3, d = 4;

    // Coordinates of points
    int x1 = -2, y1 = -2, z1 = 1;
    int x2 = -4, y2 = 11, z2 = -1;

    // Function Call
    check_position(a, b, c, d,
                   x1, y1, z1,
                   x2, y2, z2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to check position of two
    // points with respect to a plane in 3D
    static void check_position(int a, int b, int c, int d,
                               int x1, int y1, int z1,
                               int x2, int y2, int z2)
    {
        // Put coordinates in plane equation
        int value_1 = a * x1 + b * y1 + c * z1 + d;
        int value_2 = a * x2 + b * y2 + c * z2 + d;

        // If both values have same sign
        if ((value_1 > 0 && value_2 > 0)
            || (value_1 < 0 && value_2 < 0))
            System.out.print("On same side");

        // If both values have different sign
        if ((value_1 > 0 && value_2 < 0)
            || (value_1 < 0 && value_2 > 0))
            System.out.print("On different sides");

        // If both values are zero
        if (value_1 == 0 && value_2 == 0)
            System.out.print("Both on the plane");

        // If either of the two values is zero
        if (value_1 == 0 && value_2 != 0)
            System.out.print("Point 1 on the plane");
        if (value_1 != 0 && value_2 == 0)
            System.out.print("Point 2 on the plane");
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given Input
        int a = 1, b = 2, c = 3, d = 4;

        // Coordinates of points
        int x1 = -2, y1 = -2, z1 = 1;
        int x2 = -4, y2 = 11, z2 = -1;

        // Function Call
        check_position(a, b, c, d, x1, y1, z1, x2, y2, z2);
    }
}

// This code is contributed by sk944795.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check position of two
# points with respect to a plane in 3D
def check_position(a, b, c, d, x1, y1,
                       z1, x2, y2, z2):

    # Put coordinates in plane equation
    value_1 = a * x1 + b * y1 + c * z1 + d
    value_2 = a * x2 + b * y2 + c * z2 + d

    # If both values have same sign
    if ((value_1 > 0 and value_2 > 0) or
        (value_1 < 0 and value_2 < 0)):
        print("On same side")

    # If both values have different sign
    if ((value_1 > 0 and value_2 < 0) or
        (value_1 < 0 and value_2 > 0)):
        print("On different sides")

    # If both values are zero
    if (value_1 == 0 and value_2 == 0):
        print("Both on the plane")

    # If either of the two values is zero
    if (value_1 == 0 and value_2 != 0):
        print("Point 1 on the plane")
    if (value_1 != 0 and value_2 == 0):
        print("Point 2 on the plane")

# Driver Code
if __name__ == '__main__':

    # Given Input
    a, b, c, d = 1, 2, 3, 4

    # Coordinates of points
    x1, y1, z1 = -2, -2, 1
    x2, y2, z2 = -4, 11, -1

    # Function Call
    check_position(a, b, c, d, x1,
                   y1, z1, x2, y2, z2)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Function to check position of two
    // points with respect to a plane in 3D
    static void check_position(int a, int b, int c, int d,
                               int x1, int y1, int z1,
                               int x2, int y2, int z2)
    {
        // Put coordinates in plane equation
        int value_1 = a * x1 + b * y1 + c * z1 + d;
        int value_2 = a * x2 + b * y2 + c * z2 + d;

        // If both values have same sign
        if ((value_1 > 0 && value_2 > 0)
            || (value_1 < 0 && value_2 < 0))
            Console.Write("On same side");

        // If both values have different sign
        if ((value_1 > 0 && value_2 < 0)
            || (value_1 < 0 && value_2 > 0))
            Console.Write("On different sides");

        // If both values are zero
        if (value_1 == 0 && value_2 == 0)
            Console.Write("Both on the plane");

        // If either of the two values is zero
        if (value_1 == 0 && value_2 != 0)
           Console.Write("Point 1 on the plane");
        if (value_1 != 0 && value_2 == 0)
            Console.Write("Point 2 on the plane");
    }

// Driver code
static void Main()
{
    // Given Input
        int a = 1, b = 2, c = 3, d = 4;

        // Coordinates of points
        int x1 = -2, y1 = -2, z1 = 1;
        int x2 = -4, y2 = 11, z2 = -1;

        // Function Call
        check_position(a, b, c, d, x1, y1, z1, x2, y2, z2);

}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check position of two
// points with respect to a plane in 3D
function check_position(a , b , c , d,
                           x1 , y1 , z1,
                           x2 , y2 , z2)
{
    // Put coordinates in plane equation
    var value_1 = a * x1 + b * y1 + c * z1 + d;
    var value_2 = a * x2 + b * y2 + c * z2 + d;

    // If both values have same sign
    if ((value_1 > 0 && value_2 > 0)
        || (value_1 < 0 && value_2 < 0))
        document.write("On same side");

    // If both values have different sign
    if ((value_1 > 0 && value_2 < 0)
        || (value_1 < 0 && value_2 > 0))
        document.write("On different sides");

    // If both values are zero
    if (value_1 == 0 && value_2 == 0)
        document.write("Both on the plane");

    // If either of the two values is zero
    if (value_1 == 0 && value_2 != 0)
        document.write("Point 1 on the plane");
    if (value_1 != 0 && value_2 == 0)
        document.write("Point 2 on the plane");
}

// Driver code

// Given Input
var a = 1, b = 2, c = 3, d = 4;

// Coordinates of points
var x1 = -2, y1 = -2, z1 = 1;
var x2 = -4, y2 = 11, z2 = -1;

// Function Call
check_position(a, b, c, d, x1, y1, z1, x2, y2, z2);

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
On same side
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)