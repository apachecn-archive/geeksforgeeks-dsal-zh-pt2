# 计算机图形学中的 DDA 线生成算法

> 原文:[https://www . geesforgeks . org/DDA-line-generation-algorithm-computer-graphics/](https://www.geeksforgeeks.org/dda-line-generation-algorithm-computer-graphics/)

在任何二维平面中，如果我们连接两个点(x0，y0)和(x1，y1)，我们得到一条线段。但是在计算机图形的情况下，我们不能直接连接任何两个坐标点，为此，我们应该计算中间点的坐标，并在 C 中的 [putpixel(x，y，K)等函数的帮助下，为所需颜色的每个中间点放置一个像素，其中(x，y)是我们的坐标，K 表示某种颜色。
示例:](http://www.programmingsimplified.com/c/graphics.h/putpixel) 

```
Input: For line segment between (2, 2) and (6, 6) :
we need (3, 3) (4, 4) and (5, 5) as our intermediate
points.

Input: For line segment between (0, 2) and (0, 6) :
we need (0, 3) (0, 4) and (0, 5) as our intermediate
points.
```

使用图形功能时，我们的系统输出屏幕被视为一个坐标系，其中左上角的坐标为(0，0)，当我们向下移动时，y 坐标增加，当我们向右移动时，任何点(x，y)的 x 坐标增加。
现在，为了生成任何线段，我们需要中间点，为了计算它们，我们可以使用称为 [DDA(数字微分分析器)](https://en.wikipedia.org/wiki/Digital_differential_analyzer_%28graphics_algorithm%29)线生成算法的基本算法。

**DDA 算法:**
将直线的一点视为(X0，Y0)，将直线的第二点视为(X1，Y1)。

```
// calculate dx , dy
dx = X1 - X0;
dy = Y1 - Y0;

// Depending upon absolute value of dx & dy
// choose number of steps to put pixel as
// steps = abs(dx) > abs(dy) ? abs(dx) : abs(dy)
steps = abs(dx) > abs(dy) ? abs(dx) : abs(dy);

// calculate increment in x & y for each steps
Xinc = dx / (float) steps;
Yinc = dy / (float) steps;

// Put pixel for each step
X = X0;
Y = Y0;
for (int i = 0; i <= steps; i++)
{
    putpixel (round(X),round(Y),WHITE);
    X += Xinc;
    Y += Yinc;
}
```

## C

```
// C program for DDA line generation
#include<stdio.h>
#include<graphics.h>
#include<math.h>
//Function for finding absolute value
int abs (int n)
{
    return ( (n>0) ? n : ( n * (-1)));
}

//DDA Function for line generation
void DDA(int X0, int Y0, int X1, int Y1)
{
    // calculate dx & dy
    int dx = X1 - X0;
    int dy = Y1 - Y0;

    // calculate steps required for generating pixels
    int steps = abs(dx) > abs(dy) ? abs(dx) : abs(dy);

    // calculate increment in x & y for each steps
    float Xinc = dx / (float) steps;
    float Yinc = dy / (float) steps;

    // Put pixel for each step
    float X = X0;
    float Y = Y0;
    for (int i = 0; i <= steps; i++)
    {
        putpixel (round(X),round(Y),RED);  // put pixel at (X,Y)
        X += Xinc;           // increment in x at each step
        Y += Yinc;           // increment in y at each step
        delay(100);          // for visualization of line-
                             // generation step by step
    }
}

// Driver program
int main()
{
    int gd = DETECT, gm;

    // Initialize graphics function
    initgraph (&gd, &gm, "");  

    int X0 = 2, Y0 = 2, X1 = 14, Y1 = 16;
    DDA(2, 2, 14, 16);
    return 0;
}
```

输出:

**优势:**T2】

*   算法简单，易于实现。
*   它避免使用时间复杂度很高的多个操作。
*   它比直接使用线方程更快，因为它不使用任何浮点乘法，并且计算线上的点。

**劣势:**T2】

*   它处理舍入运算和浮点运算，因此时间复杂度很高。
*   由于它依赖于方向，因此端点精度较差。
*   由于浮点表示的精度有限，它会产生累积误差。

[Bresenham 的线生成算法](https://www.geeksforgeeks.org/bresenhams-line-generation-algorithm/)
本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。