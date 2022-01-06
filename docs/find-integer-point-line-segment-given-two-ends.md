# 在给定两端的线段上找到一个整数点

> 原文:[https://www . geesforgeks . org/find-整数-点-线-段-给定-两端/](https://www.geeksforgeeks.org/find-integer-point-line-segment-given-two-ends/)

给定 XY 空间中的两个点**点**和**点**，我们需要找到一个点，它具有整数坐标并且位于通过点点和点点的直线上。
例子:

```
If  pointU = (1, -1 and pointV = (-4, 1)
then equation of line which goes 
through these two points is,
2X + 5Y = -3
One point with integer co-ordinate which
satisfies above equation is (6, -3)

```

我们可以看到，一旦我们找到了线的方程，这个问题就可以被当作[扩展欧几里德算法](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)问题来处理，这里我们知道 AX + BY = C 中的 A，B，C，我们想从方程中找出 X 和 Y 的值。
在上面的扩展欧几里德方程中，C 是 A 和 B 的 gcd，所以在从给定的两点找出线方程之后，如果 C 不是 gcd(A，B)的倍数，那么我们可以得出结论，在指定的线上不存在可能的整数坐标。如果 C 是 g 的倍数，那么我们可以放大建立的 X 和 Y 系数，以满足实际方程，这将是我们的最终答案。

```
//   C++ program to get Integer point on a line
#include <bits/stdc++.h>
using namespace std;

//  Utility method for extended Euclidean Algorithm
int gcdExtended(int a, int b, int *x, int *y)
{
    // Base Case
    if (a == 0)
    {
        *x = 0;
        *y = 1;
        return b;
    }

    int x1, y1; // To store results of recursive call
    int gcd = gcdExtended(b%a, a, &x1, &y1);

    // Update x and y using results of recursive
    // call
    *x = y1 - (b/a) * x1;
    *y = x1;

    return gcd;
}

//  method prints integer point on a line with two
// points U and V.
void printIntegerPoint(int c[], int pointV[])
{
    //  Getting coefficient of line
    int A = (pointU[1] - pointV[1]);
    int B = (pointV[0] - pointU[0]);
    int C = (pointU[0] * (pointU[1] - pointV[1]) +
             pointU[1] * (pointV[0] - pointU[0]));

    int x, y;  // To be assigned a value by gcdExtended()
    int g = gcdExtended(A, B, &x, &y);

    // if C is not divisible by g, then no solution
    // is available
    if (C % g != 0)
        cout << "No possible integer point\n";

    else

        //  scaling up x and y to satisfy actual answer
        cout << "Integer Point : " << (x * C/g) << " "
             << (y * C/g) << endl;
}

//   Driver code to test above methods
int main()
{
    int pointU[] = {1, -1};
    int pointV[] = {-4, 1};

    printIntegerPoint(pointU, pointV);
    return 0;
}
```

输出:

```
Integer Point : 6 -3

```

本文由 **[乌卡什·特里维迪](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。