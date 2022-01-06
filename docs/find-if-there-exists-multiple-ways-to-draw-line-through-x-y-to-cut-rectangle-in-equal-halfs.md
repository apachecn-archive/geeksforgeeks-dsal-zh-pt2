# 查找是否存在多种画线方式通过(x，y)将矩形等分

> 原文:[https://www . geeksforgeeks . org/find-if-exists-multiple-way-draw-line-through-x-y-to-cut-rectant-in-equal-halfs/](https://www.geeksforgeeks.org/find-if-there-exists-multiple-ways-to-draw-line-through-x-y-to-cut-rectangle-in-equal-halfs/)

给定四个整数 **W** 、 **H** 、 **x** 和 **y** 。任务是查找是否存在多种画线方式通过 **(x，y)** 将矩形切割成两等份。如果有多种方式打印**是**否则打印**否**。矩形的坐标为 **(0，0)** 、 **(W，0)** 、 **(W，H)** 、 **(0，H)** 。
**注:**点 **(x，y)** 始终位于矩形内部或上方。
**举例:**

> **输入:** W = 2，H = 2，x = 1，y = 1
> **输出:**是
> 线段连接点(0，0)和(2，2)
> 或(0，2)和(2，0)等。都是有效的方法。
> **输入:** W = 1，H = 3，x = 1，y = 2
> **输出:**否

**逼近:**当直线垂直、水平或对角穿过矩形中心时，矩形可以分成两个相等的部分。所以，只有当点 **(x，y)** 是矩形的中心即 **(W / 2，H / 2)** 时，答案才会是**是**，否则答案是**否**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if multiple
// lines are possible passing through
// (x, y) that divide the given
// rectangle into two equal parts
int isPossible(int w, int h, int x, int y)
{

    // If the point (x, y) is the
    // centre of the rectangle
    if (x * 2 == w && y * 2 == h)
        return true;

    return false;
}

// Driver code
int main()
{
    int w = 1, h = 2, x = 1, y = 2;

    if (isPossible(w, h, x, y))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that returns true if multiple
// lines are possible passing through
// (x, y) that divide the given
// rectangle into two equal parts
static boolean isPossible(int w, int h, int x, int y)
{

    // If the point (x, y) is the
    // centre of the rectangle
    if (x * 2 == w && y * 2 == h)
        return true;

    return false;
}

// Driver code
public static void main(String[] args)
{
    int w = 1, h = 2, x = 1, y = 2;

    if (isPossible(w, h, x, y))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if multiple
# lines are possible passing through
# (x, y) that divide the given
# rectangle into two equal parts
def isPossible(w, h, x, y):

    # If the point (x, y) is the
    # centre of the rectangle
    if (x * 2 == w and y * 2 == h):
        return True

    return False

# Driver code
if __name__ == '__main__':
    w = 1
    h = 2
    x = 1
    y = 2

    if (isPossible(w, h, x, y)):
        print("Yes")
    else:
        print("No")

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if multiple
// lines are possible passing through
// (x, y) that divide the given
// rectangle into two equal parts
static bool isPossible(int w, int h,
                       int x, int y)
{

    // If the point (x, y) is the
    // centre of the rectangle
    if (x * 2 == w && y * 2 == h)
        return true;

    return false;
}

// Driver code
static public void Main ()
{
    int w = 1, h = 2, x = 1, y = 2;

    if (isPossible(w, h, x, y))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if multiple
// lines are possible passing through
// (x, y) that divide the given
// rectangle into two equal parts
function isPossible(w, h, x, y)
{

    // If the point (x, y) is the
    // centre of the rectangle
    if (x * 2 == w && y * 2 == h)
        return true;

    return false;
}

// Driver code
    let w = 1, h = 2, x = 1, y = 2;

    if (isPossible(w, h, x, y))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
No
```