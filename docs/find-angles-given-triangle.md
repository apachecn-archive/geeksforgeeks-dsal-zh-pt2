# 找出给定三角形的所有角度

> 原文:[https://www.geeksforgeeks.org/find-angles-given-triangle/](https://www.geeksforgeeks.org/find-angles-given-triangle/)

给定三角形所有三个顶点在 2D 平面上的坐标，任务是找到所有三个角度。

**示例:**

```
Input : A = (0, 0), 
        B = (0, 1), 
        C = (1, 0)
Output : 90, 45, 45

```

为了解决这个问题，我们使用下面的余弦定律。
T3】

```
c^2 = a^2 + b^2 - 2(a)(b)(cos beta)

```

重新安排后

```
beta = acos( ( a^2 + b^2 - c^2 ) / (2ab) )

```

在三角学中，余弦定律(也称为余弦公式或余弦规则)将三角形边的长度与其中一个角的余弦联系起来。

```
First, calculate the length of all the sides. 
Then apply above formula to get all angles in 
radian. Then convert angles from radian into 
degrees.

```

下面是上述步骤的实现。

## C++

```
// Code to find all three angles
// of a triangle given coordinate
// of all three vertices
#include <iostream>
#include <utility> // for pair
#include <cmath> // for math functions
using namespace std;

#define PI 3.1415926535

// returns square of distance b/w two points
int lengthSquare(pair<int,int> X, pair<int,int> Y)
{
    int xDiff = X.first - Y.first;
    int yDiff = X.second - Y.second;
    return xDiff*xDiff + yDiff*yDiff;
}

void printAngle(pair<int,int> A, pair<int,int> B,
                pair<int,int> C)
{
    // Square of lengths be a2, b2, c2
    int a2 = lengthSquare(B,C);
    int b2 = lengthSquare(A,C);
    int c2 = lengthSquare(A,B);

    // length of sides be a, b, c
    float a = sqrt(a2);
    float b = sqrt(b2);
    float c = sqrt(c2);

    // From Cosine law
    float alpha = acos((b2 + c2 - a2)/(2*b*c));
    float betta = acos((a2 + c2 - b2)/(2*a*c));
    float gamma = acos((a2 + b2 - c2)/(2*a*b));

    // Converting to degree
    alpha = alpha * 180 / PI;
    betta = betta * 180 / PI;
    gamma = gamma * 180 / PI;

    // printing all the angles
    cout << "alpha : " << alpha << endl;
    cout << "betta : " << betta << endl;
    cout << "gamma : " << gamma << endl;
}

// Driver code
int main()
{
    pair<int,int> A = make_pair(0,0);
    pair<int,int> B = make_pair(0,1);
    pair<int,int> C = make_pair(1,0);

    printAngle(A,B,C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code to find all three angles
// of a triangle given coordinate
// of all three vertices

import java.awt.Point;
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;
import static java.lang.Math.acos;

class Test
{
    // returns square of distance b/w two points
    static int lengthSquare(Point p1, Point p2)
    {
        int xDiff = p1.x- p2.x;
        int yDiff = p1.y- p2.y;
        return xDiff*xDiff + yDiff*yDiff;
    }

    static void printAngle(Point A, Point B,
            Point C)
    {
    // Square of lengths be a2, b2, c2
    int a2 = lengthSquare(B,C);
    int b2 = lengthSquare(A,C);
    int c2 = lengthSquare(A,B);

    // length of sides be a, b, c
    float a = (float)sqrt(a2);
    float b = (float)sqrt(b2);
    float c = (float)sqrt(c2);

    // From Cosine law
    float alpha = (float) acos((b2 + c2 - a2)/(2*b*c));
    float betta = (float) acos((a2 + c2 - b2)/(2*a*c));
    float gamma = (float) acos((a2 + b2 - c2)/(2*a*b));

    // Converting to degree
    alpha = (float) (alpha * 180 / PI);
    betta = (float) (betta * 180 / PI);
    gamma = (float) (gamma * 180 / PI);

    // printing all the angles
    System.out.println("alpha : " + alpha);
    System.out.println("betta : " + betta);
    System.out.println("gamma : " + gamma);
    }

    // Driver method
    public static void main(String[] args) 
    {
        Point A = new Point(0,0);
        Point B = new Point(0,1);
        Point C = new Point(1,0);

        printAngle(A,B,C);
    }
}
```

## 蟒蛇 3

```
# Python3 code to find all three angles 
# of a triangle given coordinate 
# of all three vertices 
import math

# returns square of distance b/w two points 
def lengthSquare(X, Y): 
    xDiff = X[0] - Y[0] 
    yDiff = X[1] - Y[1] 
    return xDiff * xDiff + yDiff * yDiff

def printAngle(A, B, C): 

    # Square of lengths be a2, b2, c2 
    a2 = lengthSquare(B, C) 
    b2 = lengthSquare(A, C) 
    c2 = lengthSquare(A, B) 

    # length of sides be a, b, c 
    a = math.sqrt(a2); 
    b = math.sqrt(b2); 
    c = math.sqrt(c2); 

    # From Cosine law 
    alpha = math.acos((b2 + c2 - a2) /
                         (2 * b * c)); 
    betta = math.acos((a2 + c2 - b2) / 
                         (2 * a * c)); 
    gamma = math.acos((a2 + b2 - c2) / 
                         (2 * a * b)); 

    # Converting to degree 
    alpha = alpha * 180 / math.pi; 
    betta = betta * 180 / math.pi; 
    gamma = gamma * 180 / math.pi; 

    # printing all the angles 
    print("alpha : %f" %(alpha)) 
    print("betta : %f" %(betta))
    print("gamma : %f" %(gamma))

# Driver code
A = (0, 0)
B = (0, 1) 
C = (1, 0)

printAngle(A, B, C); 

# This code is contributed 
# by ApurvaRaj
```

## C#

```
// C# Code to find all three angles
// of a triangle given coordinate
// of all three vertices
using System;

class GFG
{
    class Point
    {
        public int x, y;
        public Point(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    // returns square of distance b/w two points
    static int lengthSquare(Point p1, Point p2)
    {
        int xDiff = p1.x - p2.x;
        int yDiff = p1.y - p2.y;
        return xDiff * xDiff + yDiff * yDiff;
    }

    static void printAngle(Point A, Point B, Point C)
    {
        // Square of lengths be a2, b2, c2
        int a2 = lengthSquare(B, C);
        int b2 = lengthSquare(A, C);
        int c2 = lengthSquare(A, B);

        // length of sides be a, b, c
        float a = (float)Math.Sqrt(a2);
        float b = (float)Math.Sqrt(b2);
        float c = (float)Math.Sqrt(c2);

        // From Cosine law
        float alpha = (float) Math.Acos((b2 + c2 - a2) / 
                                           (2 * b * c));
        float betta = (float) Math.Acos((a2 + c2 - b2) / 
                                           (2 * a * c));
        float gamma = (float) Math.Acos((a2 + b2 - c2) / 
                                           (2 * a * b));

        // Converting to degree
        alpha = (float) (alpha * 180 / Math.PI);
        betta = (float) (betta * 180 / Math.PI);
        gamma = (float) (gamma * 180 / Math.PI);

        // printing all the angles
        Console.WriteLine("alpha : " + alpha);
        Console.WriteLine("betta : " + betta);
        Console.WriteLine("gamma : " + gamma);
    }

    // Driver Code
    public static void Main(String[] args) 
    {
        Point A = new Point(0, 0);
        Point B = new Point(0, 1);
        Point C = new Point(1, 0);

        printAngle(A, B, C);
    }
}

// This code is contributed by Rajput-Ji
```

**Output:**

```
alpha : 90
betta : 45
gamma : 45

```

**参考**:
T3】https://en.wikipedia.org/wiki/Law_of_cosines

本文由 [**普拉蒂克·查哈尔**](https://github.com/pratik-chhajer) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。