# 覆盖所有点的最小线

> 原文:[https://www.geeksforgeeks.org/minimum-lines-cover-points/](https://www.geeksforgeeks.org/minimum-lines-cover-points/)

给定二维空间中的 N 个点，我们需要打印穿过所有这 N 个点并且也穿过特定(xO，yO)点的最小行数。
示例:

```
If given points are (-1, 3), (4, 3), (2, 1), (-1, -2), 
(3, -3) and (xO, yO) point is (1, 0) i.e. every line
must go through this point. 
Then we have to draw at least two lines to cover all
these points going through (xO, yO) as shown in below
diagram.
```

我们可以通过用(xO，yO)考虑所有点的斜率来解决这个问题。如果两个不同的点与(xO，yO)具有相同的斜率，那么它们只能被相同的线覆盖，因此我们可以跟踪每个点的斜率，并且每当我们获得新的斜率时，我们将增加我们的线计数一。
在下面的代码中，斜率被存储为一对整数以解决精度问题，并且一个集合被用来跟踪发生的斜率。
为了更好的理解，请看下面的代码。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to get minimum lines to cover
// all the points
#include <bits/stdc++.h>
using namespace std;

//    Utility method to get gcd of a and b
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

//    method returns reduced form of dy/dx as a pair
pair<int, int> getReducedForm(int dy, int dx)
{
    int g = gcd(abs(dy), abs(dx));

    //    get sign of result
    bool sign = (dy < 0) ^ (dx < 0);

    if (sign)
        return make_pair(-abs(dy) / g, abs(dx) / g);
    else
        return make_pair(abs(dy) / g, abs(dx) / g);
}

/*    method returns minimum number of lines to
    cover all points where all lines goes
    through (xO, yO) */
int minLinesToCoverPoints(int points[][2], int N,
                                   int xO, int yO)
{
    //    set to store slope as a pair
    set< pair<int, int> > st;
    pair<int, int> temp;
    int minLines = 0;

    //    loop over all points once
    for (int i = 0; i < N; i++)
    {
        //    get x and y co-ordinate of current point
        int curX = points[i][0];
        int curY = points[i][1];

        temp = getReducedForm(curY - yO, curX - xO);

        // if this slope is not there in set,
        // increase ans by 1 and insert in set
        if (st.find(temp) == st.end())
        {
            st.insert(temp);
            minLines++;
        }
    }

    return minLines;
}

// Driver code to test above methods
int main()
{
    int xO, yO;
    xO = 1;
    yO = 0;

    int points[][2] =
    {
        {-1, 3},
        {4, 3},
        {2, 1},
        {-1, -2},
        {3, -3}
    };

    int N = sizeof(points) / sizeof(points[0]);
    cout << minLinesToCoverPoints(points, N, xO, yO);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
import java.io.*;
import java.util.*;
import java.util.Set;

// User defined Pair class
class Pair {
    int x;
    int y;

    // Constructor
    public Pair(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

class GFG {
    //  Utility method to get gcd of a and b
    public static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }
    // method returns reduced form of dy/dx as a pair
    public static Pair getReducedForm(int dy, int dx)
    {
        int g = gcd(Math.abs(dy), Math.abs(dx));

        //    get sign of result
        boolean sign = (dy < 0) ^ (dx < 0);
        Pair res = new Pair(0, 0);

        if (sign) {
            res.x = -Math.abs(dy) / g;
            res.y = Math.abs(dx) / g;
        }
        else {
            res.x = Math.abs(dy) / g;
            res.y = Math.abs(dx) / g;
        }
        return res;
    }

    /*  method returns minimum number of lines to
    cover all points where all lines goes
    through (xO, yO) */

    public static int minLinesToCoverPoints(int points[][],
                                            int N, int xO,
                                            int yO)
    {
        // set to store slope as a string
        Set<String> st = new HashSet<String>();

        Pair temp;
        int minLines = 0;

        //    loop over all points once
        for (int i = 0; i < N; i++) {
            //    get x and y co-ordinate of current point
            int curX = points[i][0];
            int curY = points[i][1];

            temp = getReducedForm(curY - yO, curX - xO);

            // convert pair into string to store in set
            String tempString = temp.x + "," + temp.y;

            // if this slope is not there in set,
            // increase ans by 1 and insert in set

            if (st.contains(tempString) == false) {
                st.add(tempString);
                minLines += 1;
            }
        }

        return minLines;
    }

    // Driver code
    public static void main(String[] args)
    {
        int xO, yO;
        xO = 1;
        yO = 0;

        int points[][] = { { -1, 3 },
                           { 4, 3 },
                           { 2, 1 },
                           { -1, -2 },
                           { 3, -3 } };

        int N = points.length;
        System.out.println(
            minLinesToCoverPoints(points, N, xO, yO));
    }
}

// This code is contributed by rj13to.
```

## 蟒蛇 3

```
# Python3 program to get minimum lines to cover
# all the points

# Utility method to get gcd of a and b
def gcd(a, b):
    if (b == 0):
        return a
    return gcd(b, a % b)

# method returns reduced form of dy/dx as a pair
def getReducedForm(dy, dx):
    g = gcd(abs(dy), abs(dx))

    # get sign of result
    sign = (dy < 0) ^ (dx < 0)

    if (sign):
        return (-abs(dy) // g, abs(dx) // g)
    else:
        return (abs(dy) // g, abs(dx) // g)

# /* method returns minimum number of lines to
#     cover all points where all lines goes
#     through (xO, yO) */
def minLinesToCoverPoints(points, N, xO, yO):

    # set to store slope as a pair
    st = dict()
    minLines = 0

    # loop over all points once
    for i in range(N):

        # get x and y co-ordinate of current point
        curX = points[i][0]
        curY = points[i][1]

        temp = getReducedForm(curY - yO, curX - xO)

        # if this slope is not there in set,
        # increase ans by 1 and insert in set
        if (temp not in st):
            st[temp] = 1
            minLines += 1

    return minLines

# Driver code
xO = 1
yO = 0

points =[[-1, 3],
         [4, 3],
         [2, 1],
         [-1, -2],
         [3, -3]]

N = len(points)
print(minLinesToCoverPoints(points, N, xO, yO))

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript program to get minimum lines to cover
// all the points

    //    Utility method to get gcd of a and b
    function gcd(a,b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // method returns reduced form of dy/dx as a pair
    function getReducedForm(dy,dx)
    {
        let g = gcd(Math.abs(dy), Math.abs(dx));

    // get sign of result
    let sign = (dy < 0) ^ (dx < 0);

    if (sign)
    {  
        return [Math.floor(-Math.abs(dy) / g), Math.floor(Math.abs(dx) / g)];

    }
    else
        return [Math.floor(Math.abs(dy) / g), Math.floor(Math.abs(dx) / g)];
    }

    /*    method returns minimum number of lines to
    cover all points where all lines goes
    through (xO, yO) */
    function minLinesToCoverPoints(points,N,x0,y0)
    {
        let st=new Set();
        let temp;
        let minLines = 0;

        // loop over all points once
    for (let i = 0; i < N; i++)
    {
        // get x and y co-ordinate of current point
        let curX = points[i][0];
        let curY = points[i][1];

        temp = getReducedForm(curY - yO, curX - xO);

        // if this slope is not there in set,
        // increase ans by 1 and insert in set
        if (!st.has(temp.join("")))
        {

            st.add(temp.join(""));
            minLines++;
        }
    }

    return minLines;
    }

    // Driver code to test above methods
    let xO, yO;
    xO = 1;
    yO = 0;

    let points =[[-1, 3],
         [4, 3],
         [2, 1],
         [-1, -2],
         [3, -3]];
    let N = points.length;
    document.write(minLinesToCoverPoints(points, N, xO, yO))

// This code is contributed by unknown2108
</script>
```

**输出:**

```
2
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。