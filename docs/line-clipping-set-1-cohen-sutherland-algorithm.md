# 线裁剪|集合 1(科恩-萨瑟兰算法)

> 原文:[https://www . geesforgeks . org/line-clipping-set-1-Cohen-Sutherland-algorithm/](https://www.geeksforgeeks.org/line-clipping-set-1-cohen-sutherland-algorithm/)

给定一组线和一个感兴趣的矩形区域，任务是移除感兴趣区域之外的线，并裁剪部分位于该区域内的线。

```
Input : Rectangular area of interest (Defined by
        below four values which are coordinates of
        bottom left and top right)
        x_min = 4, y_min = 4, x_max = 10, y_max = 8

        A set of lines (Defined by two corner coordinates)
        line 1 : x1 = 5, y1 = 5, x2 = 7, y2 = 7
        Line 2 : x1 = 7, y1 = 9, x2 = 11, y2 = 4
        Line 2 : x1 = 1, y1 = 5, x2 = 4, y2 = 1 

Output : Line 1 : Accepted from (5, 5) to (7, 7)
         Line 2 : Accepted from (7.8, 8) to (10, 5.25)
         Line 3 : Rejected
```

[科恩-萨瑟兰算法](https://en.wikipedia.org/wiki/Cohen%E2%80%93Sutherland_algorithm)将二维空间划分为 9 个区域，然后有效地确定给定矩形区域内的线和线的部分。

**算法可以概述如下:-**

```
Nine regions are created, eight "outside" regions and one 
"inside" region.

For a given line extreme point (x, y), we can quickly
find its region's four bit code. Four bit code can 
be computed by comparing x and y with four values 
(x_min, x_max, y_min and y_max).

If x is less than x_min then bit number 1 is set.
If x is greater than x_max then bit number 2 is set.
If y is less than y_min then bit number 3 is set.
If y is greater than y_max then bit number 4 is set
```

![Cohen-Sutherland algorithm outline](img/39e83b5eac866160b5b9483657708809.png)

对于任何给定的行，都有三种可能的情况。

1.  **完全在给定的矩形内:**线的两个端点的区域的按位或为 0(两个点都在矩形内)
2.  **完全在给定矩形之外:**两个端点共享至少一个外部区域，这意味着线不穿过可见区域。(端点的按位“与”！= 0).
3.  **部分在窗口内:**两个端点在不同的区域。在这种情况下，算法会找到矩形区域之外的两个点中的一个。外部点和矩形窗口的线的交点成为新的角点，算法重复

![cohen-sutherland-algo1](img/a21f5b6745136a1a3e8aa4bdacf84826.png)

**伪码:**

```
Step 1 : Assign a region code for two endpoints of given line.
Step 2 : If both endpoints have a region code 0000 
         then given line is completely inside.
Step 3 : Else, perform the logical AND operation for both region codes.
    Step 3.1 : If the result is not 0000, then given line is completely
               outside.
    Step 3.2 : Else line is partially inside.
        Step 3.2.1 : Choose an endpoint of the line 
                     that is outside the given rectangle.
        Step 3.2.2 : Find the intersection point of the 
                     rectangular boundary (based on region code).
        Step 3.2.3 : Replace endpoint with the intersection point 
                     and update the region code.
        Step 3.2.4 : Repeat step 2 until we find a clipped line either 
                     trivially accepted or trivially rejected.
        Step 4 : Repeat step 1 for other lines
```

下面是上述步骤的实现。

## C++

```
// C++ program to implement Cohen Sutherland algorithm
// for line clipping.
#include <iostream>
using namespace std;

// Defining region codes
const int INSIDE = 0; // 0000
const int LEFT = 1; // 0001
const int RIGHT = 2; // 0010
const int BOTTOM = 4; // 0100
const int TOP = 8; // 1000

// Defining x_max, y_max and x_min, y_min for
// clipping rectangle. Since diagonal points are
// enough to define a rectangle
const int x_max = 10;
const int y_max = 8;
const int x_min = 4;
const int y_min = 4;

// Function to compute region code for a point(x, y)
int computeCode(double x, double y)
{
    // initialized as being inside
    int code = INSIDE;

    if (x < x_min) // to the left of rectangle
        code |= LEFT;
    else if (x > x_max) // to the right of rectangle
        code |= RIGHT;
    if (y < y_min) // below the rectangle
        code |= BOTTOM;
    else if (y > y_max) // above the rectangle
        code |= TOP;

    return code;
}

// Implementing Cohen-Sutherland algorithm
// Clipping a line from P1 = (x2, y2) to P2 = (x2, y2)
void cohenSutherlandClip(double x1, double y1,
                         double x2, double y2)
{
    // Compute region codes for P1, P2
    int code1 = computeCode(x1, y1);
    int code2 = computeCode(x2, y2);

    // Initialize line as outside the rectangular window
    bool accept = false;

    while (true) {
        if ((code1 == 0) && (code2 == 0)) {
            // If both endpoints lie within rectangle
            accept = true;
            break;
        }
        else if (code1 & code2) {
            // If both endpoints are outside rectangle,
            // in same region
            break;
        }
        else {
            // Some segment of line lies within the
            // rectangle
            int code_out;
            double x, y;

            // At least one endpoint is outside the
            // rectangle, pick it.
            if (code1 != 0)
                code_out = code1;
            else
                code_out = code2;

            // Find intersection point;
            // using formulas y = y1 + slope * (x - x1),
            // x = x1 + (1 / slope) * (y - y1)
            if (code_out & TOP) {
                // point is above the clip rectangle
                x = x1 + (x2 - x1) * (y_max - y1) / (y2 - y1);
                y = y_max;
            }
            else if (code_out & BOTTOM) {
                // point is below the rectangle
                x = x1 + (x2 - x1) * (y_min - y1) / (y2 - y1);
                y = y_min;
            }
            else if (code_out & RIGHT) {
                // point is to the right of rectangle
                y = y1 + (y2 - y1) * (x_max - x1) / (x2 - x1);
                x = x_max;
            }
            else if (code_out & LEFT) {
                // point is to the left of rectangle
                y = y1 + (y2 - y1) * (x_min - x1) / (x2 - x1);
                x = x_min;
            }

            // Now intersection point x, y is found
            // We replace point outside rectangle
            // by intersection point
            if (code_out == code1) {
                x1 = x;
                y1 = y;
                code1 = computeCode(x1, y1);
            }
            else {
                x2 = x;
                y2 = y;
                code2 = computeCode(x2, y2);
            }
        }
    }
    if (accept) {
        cout << "Line accepted from " << x1 << ", "
             << y1 << " to " << x2 << ", " << y2 << endl;
        // Here the user can add code to display the rectangle
        // along with the accepted (portion of) lines
    }
    else
        cout << "Line rejected" << endl;
}

// Driver code
int main()
{
    // First Line segment
    // P11 = (5, 5), P12 = (7, 7)
    cohenSutherlandClip(5, 5, 7, 7);

    // Second Line segment
    // P21 = (7, 9), P22 = (11, 4)
    cohenSutherlandClip(7, 9, 11, 4);

    // Third Line segment
    // P31 = (1, 5), P32 = (4, 1)
    cohenSutherlandClip(1, 5, 4, 1);

    return 0;
}
```

## 计算机编程语言

```
# Python program to implement Cohen Sutherland algorithm
# for line clipping.

# Defining region codes
INSIDE = 0  # 0000
LEFT = 1    # 0001
RIGHT = 2   # 0010
BOTTOM = 4  # 0100
TOP = 8     # 1000

# Defining x_max, y_max and x_min, y_min for rectangle
# Since diagonal points are enough to define a rectangle
x_max = 10.0
y_max = 8.0
x_min = 4.0
y_min = 4.0

# Function to compute region code for a point(x, y)
def computeCode(x, y):
    code = INSIDE
    if x < x_min:      # to the left of rectangle
        code |= LEFT
    elif x > x_max:    # to the right of rectangle
        code |= RIGHT
    if y < y_min:      # below the rectangle
        code |= BOTTOM
    elif y > y_max:    # above the rectangle
        code |= TOP

    return code

# Implementing Cohen-Sutherland algorithm
# Clipping a line from P1 = (x1, y1) to P2 = (x2, y2)
def cohenSutherlandClip(x1, y1, x2, y2):

    # Compute region codes for P1, P2
    code1 = computeCode(x1, y1)
    code2 = computeCode(x2, y2)
    accept = False

    while True:

        # If both endpoints lie within rectangle
        if code1 == 0 and code2 == 0:
            accept = True
            break

        # If both endpoints are outside rectangle
        elif (code1 & code2) != 0:
            break

        # Some segment lies within the rectangle
        else:

            # Line Needs clipping
            # At least one of the points is outside, 
            # select it
            x = 1.0
            y = 1.0
            if code1 != 0:
                code_out = code1
            else:
                code_out = code2

            # Find intersection point
            # using formulas y = y1 + slope * (x - x1), 
            # x = x1 + (1 / slope) * (y - y1)
            if code_out & TOP:

                # point is above the clip rectangle
                x = x1 + (x2 - x1) * \
                                (y_max - y1) / (y2 - y1)
                y = y_max

            elif code_out & BOTTOM:

                # point is below the clip rectangle
                x = x1 + (x2 - x1) * \
                                (y_min - y1) / (y2 - y1)
                y = y_min

            elif code_out & RIGHT:

                # point is to the right of the clip rectangle
                y = y1 + (y2 - y1) * \
                                (x_max - x1) / (x2 - x1)
                x = x_max

            elif code_out & LEFT:

                # point is to the left of the clip rectangle
                y = y1 + (y2 - y1) * \
                                (x_min - x1) / (x2 - x1)
                x = x_min

            # Now intersection point x, y is found
            # We replace point outside clipping rectangle
            # by intersection point
            if code_out == code1:
                x1 = x
                y1 = y
                code1 = computeCode(x1, y1)

            else:
                x2 = x
                y2 = y
                code2 = computeCode(x2, y2)

    if accept:
        print ("Line accepted from %.2f, %.2f to %.2f, %.2f" % (x1, y1, x2, y2))

        # Here the user can add code to display the rectangle
        # along with the accepted (portion of) lines

    else:
        print("Line rejected")

# Driver Script
# First Line segment
# P11 = (5, 5), P12 = (7, 7)
cohenSutherlandClip(5, 5, 7, 7)

# Second Line segment
# P21 = (7, 9), P22 = (11, 4)
cohenSutherlandClip(7, 9, 11, 4)

# Third Line segment
# P31 = (1, 5), P32 = (4, 1)
cohenSutherlandClip(1, 5, 4, 1)
```

**输出:**

```
Line accepted from 5.00, 5.00 to 7.00, 7.00
Line accepted from 7.80, 8.00 to 10.00, 5.25
Line rejected
```

**下面是使用 graphics.h 的 C++代码**

## C++

```
// C++ program to implement Cohen Sutherland algorithm
// for line clipping.
// including libraries
#include <bits/stdc++.h>
#include <graphics.h>
using namespace std;

// Global Variables
int xmin, xmax, ymin, ymax;

// Lines where co-ordinates are (x1, y1) and (x2, y2)
struct lines {
    int x1, y1, x2, y2;
};

// This will return the sign required.
int sign(int x)
{
    if (x > 0)
        return 1;
    else
        return 0;
}

// CohenSutherLand LineClipping Algorithm As Described in theory.
// This will clip the lines as per window boundaries.
void clip(struct lines mylines)
{
    // arrays will store bits
    // Here bits implies initial Point whereas bite implies end points
    int bits[4], bite[4], i, var;
    // setting color of graphics to be RED
    setcolor(RED);

    // Finding Bits
    bits[0] = sign(xmin - mylines.x1);
    bite[0] = sign(xmin - mylines.x2);
    bits[1] = sign(mylines.x1 - xmax);
    bite[1] = sign(mylines.x2 - xmax);
    bits[2] = sign(ymin - mylines.y1);
    bite[2] = sign(ymin - mylines.y2);
    bits[3] = sign(mylines.y1 - ymax);
    bite[3] = sign(mylines.y2 - ymax);

    // initial will used for initial coordinates and end for final
    string initial = "", end = "", temp = "";

    // convert bits to string
    for (i = 0; i < 4; i++) {
        if (bits[i] == 0)
            initial += '0';
        else
            initial += '1';
    }
    for (i = 0; i < 4; i++) {
        if (bite[i] == 0)
            end += '0';
        else
            end += '1';
    }

    // finding slope of line y=mx+c as (y-y1)=m(x-x1)+c
    // where m is slope m=dy/dx;

    float m = (mylines.y2 - mylines.y1) / (float)(mylines.x2 - mylines.x1);
    float c = mylines.y1 - m * mylines.x1;

    // if both points are inside the Accept the line and draw
    if (initial == end && end == "0000") {
        // inbuild function to draw the line from(x1, y1) to (x2, y2)
        line(mylines.x1, mylines.y1, mylines.x2, mylines.y2);
        return;
    }

    // this will contain cases where line maybe totally outside for partially inside
    else {
        // taking bitwise end of every value
        for (i = 0; i < 4; i++) {

            int val = (bits[i] & bite[i]);
            if (val == 0)
                temp += '0';
            else
                temp += '1';
        }
        // as per algo if AND is not 0000 means line is completely outside hene draw nothing and return
        if (temp != "0000")
            return;

        // Here contain cases of partial inside or outside
        // So check for every boundary one by one
        for (i = 0; i < 4; i++) {
            // if boths bit are same hence we cannot find any intersection with boundary so continue
            if (bits[i] == bite[i])
                continue;
            // Otherwise there exist a intersection

            // Case when initial point is in left xmin
            if (i == 0 && bits[i] == 1) {
                var = round(m * xmin + c);
                mylines.y1 = var;
                mylines.x1 = xmin;
            }
            // Case when final point is in left xmin
            if (i == 0 && bite[i] == 1) {
                var = round(m * xmin + c);
                mylines.y2 = var;
                mylines.x2 = xmin;
            }
            // Case when initial point is in right of xmax
            if (i == 1 && bits[i] == 1) {
                var = round(m * xmax + c);
                mylines.y1 = var;
                mylines.x1 = xmax;
            }
            // Case when final point is in right of xmax
            if (i == 1 && bite[i] == 1) {
                var = round(m * xmax + c);
                mylines.y2 = var;
                mylines.x2 = xmax;
            }
            // Case when initial point is in top of ymin
            if (i == 2 && bits[i] == 1) {
                var = round((float)(ymin - c) / m);
                mylines.y1 = ymin;
                mylines.x1 = var;
            }
            // Case when final point is in top of ymin
            if (i == 2 && bite[i] == 1) {
                var = round((float)(ymin - c) / m);
                mylines.y2 = ymin;
                mylines.x2 = var;
            }
            // Case when initial point is in bottom of ymax
            if (i == 3 && bits[i] == 1) {
                var = round((float)(ymax - c) / m);
                mylines.y1 = ymax;
                mylines.x1 = var;
            }
            // Case when final point is in bottom of ymax
            if (i == 3 && bite[i] == 1) {
                var = round((float)(ymax - c) / m);
                mylines.y2 = ymax;
                mylines.x2 = var;
            }
            // Updating Bits at every point
            bits[0] = sign(xmin - mylines.x1);
            bite[0] = sign(xmin - mylines.x2);
            bits[1] = sign(mylines.x1 - xmax);
            bite[1] = sign(mylines.x2 - xmax);
            bits[2] = sign(ymin - mylines.y1);
            bite[2] = sign(ymin - mylines.y2);
            bits[3] = sign(mylines.y1 - ymax);
            bite[3] = sign(mylines.y2 - ymax);
        } // end of for loop
        // Initialize initial and end to NULL
        initial = "", end = "";
        // Updating strings again by bit
        for (i = 0; i < 4; i++) {
            if (bits[i] == 0)
                initial += '0';
            else
                initial += '1';
        }
        for (i = 0; i < 4; i++) {
            if (bite[i] == 0)
                end += '0';
            else
                end += '1';
        }
        // If now both points lie inside or on boundary then simply draw the updated line
        if (initial == end && end == "0000") {
            line(mylines.x1, mylines.y1, mylines.x2, mylines.y2);
            return;
        }
        // else line was completely outside hence rejected
        else
            return;
    }
}

// Driver Function
int main()
{
    int gd = DETECT, gm;

    // Setting values of Clipping window
    xmin = 40;
    xmax = 100;
    ymin = 40;
    ymax = 80;

    // initialize the graph
    initgraph(&gd, &gm, NULL);

    // Drawing Window using Lines
    line(xmin, ymin, xmax, ymin);
    line(xmax, ymin, xmax, ymax);
    line(xmax, ymax, xmin, ymax);
    line(xmin, ymax, xmin, ymin);

    // Assume 4 lines to be clipped
    struct lines mylines[4];

    // Setting the coordinated of  4 lines
    mylines[0].x1 = 30;
    mylines[0].y1 = 65;
    mylines[0].x2 = 55;
    mylines[0].y2 = 30;

    mylines[1].x1 = 60;
    mylines[1].y1 = 20;
    mylines[1].x2 = 100;
    mylines[1].y2 = 90;

    mylines[2].x1 = 60;
    mylines[2].y1 = 100;
    mylines[2].x2 = 80;
    mylines[2].y2 = 70;

    mylines[3].x1 = 85;
    mylines[3].y1 = 50;
    mylines[3].x2 = 120;
    mylines[3].y2 = 75;

    // Drawing Initial Lines without clipping
    for (int i = 0; i < 4; i++) {
        line(mylines[i].x1, mylines[i].y1,
             mylines[i].x2, mylines[i].y2);
        delay(1000);
    }

    // Drawing clipped Line
    for (int i = 0; i < 4; i++) {
        // Calling clip() which in term clip the line as per window and draw it
        clip(mylines[i]);
        delay(1000);
    }
    delay(4000);
    getch();
    // For Closing the graph.
    closegraph();
    return 0;
}
```

科恩-萨瑟兰算法只能用于矩形剪辑窗口。对于其他凸多边形裁剪窗口，使用赛勒斯-贝克算法。我们将在下一集讨论赛勒斯-贝克算法。

**相关帖子:**
[多边形裁剪|萨瑟兰–霍奇曼算法](https://www.geeksforgeeks.org/polygon-clipping-sutherland-hodgman-algorithm-please-change-bmp-images-jpeg-png/)
[计算机图形学中的点裁剪算法](https://www.geeksforgeeks.org/point-clipping-algorithm-computer-graphics/)
**参考:**
[https://en.wikipedia.org/wiki/Cohen–Sutherland_algorithm](https://en.wikipedia.org/wiki/Cohen%E2%80%93Sutherland_algorithm)
本文由**萨凯特·莫迪**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。