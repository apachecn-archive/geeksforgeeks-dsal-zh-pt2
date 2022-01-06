# 一张纸上可以切割的最大给定尺寸的矩形

> 原文:[https://www . geeksforgeeks . org/最大给定大小的矩形-可以从一张纸上切出的矩形/](https://www.geeksforgeeks.org/maximum-given-sized-rectangles-that-can-be-cut-out-of-a-sheet-of-paper/)

给定一张纸的长度 **L** 和宽度 **B** ，任务是找出给定长度 **l** 和宽度 **b** 的矩形中可以从这张纸上切割的最大数量。
**举例:**

> **输入:** L = 5，B = 2，l = 14，b = 3
> **输出:** 0
> 板材小于所需矩形。因此，给定尺寸的矩形不能从薄板上切下。
> **输入:** L = 10，B = 7，l = 4，b = 3
> **输出:** 4

**进场:**

*   尝试水平切割矩形，即矩形的长度与纸张的长度对齐，矩形的宽度与纸张的宽度对齐，并将可能的矩形数量存储在**水平**中。
*   对垂直对齐重复同样的操作，即当矩形的长度与纸张的宽度对齐，并且矩形的宽度与纸张的长度对齐时，将结果存储在**垂直**中。打印 **max(水平，垂直)**作为结果。

以下是上述方法的实现:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the maximum rectangles possible
int maxRectangles(int L, int B, int l, int b)
{
    int horizontal = 0, vertical = 0;

    // Cut rectangles horizontally if possible
    if (l <= L && b <= B)
    {

        // One rectangle is a single cell
        int columns = B / b;
        int rows = L / l;

        // Total rectangles = total cells
        horizontal = rows * columns;
    }

    // Cut rectangles vertically if possible
    if (l <= B && b <= L)
    {
        int columns = L / b;
        int rows = B / l;

        vertical = rows * columns;
    }

    // Return the maximum possible rectangles
    return max(horizontal, vertical);
}

// Driver code
int main()
{
    int L = 10, B = 7, l = 4, b = 3;
    cout << (maxRectangles(L, B, l, b)) << endl;
}

// This code is contributed by
// Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the maximum rectangles possible
    static int maxRectangles(int L, int B, int l, int b)
    {
        int horizontal = 0, vertical = 0;

        // Cut rectangles horizontally if possible
        if (l <= L && b <= B) {

            // One rectangle is a single cell
            int columns = B / b;
            int rows = L / l;

            // Total rectangles = total cells
            horizontal = rows * columns;
        }

        // Cut rectangles vertically if possible
        if (l <= B && b <= L) {
            int columns = L / b;
            int rows = B / l;

            vertical = rows * columns;
        }

        // Return the maximum possible rectangles
        return Math.max(horizontal, vertical);
    }

    // Driver code
    public static void main(String[] args)
    {
        int L = 10, B = 7, l = 4, b = 3;
        System.out.print(maxRectangles(L, B, l, b));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum
# rectangles possible
def maxRectangles(L, B, l, b):

    horizontal, vertical = 0, 0

    # Cut rectangles horizontally if possible
    if l <= L and b <= B:

        # One rectangle is a single cell
        columns = B // b
        rows = L // l

        # Total rectangles = total cells
        horizontal = rows * columns

    # Cut rectangles vertically if possible
    if l <= B and b <= L:

        columns = L // b
        rows = B // l

        vertical = rows * columns

    # Return the maximum possible rectangles
    return max(horizontal, vertical)

# Driver code
if __name__ == "__main__":

    L, B, l, b = 10, 7, 4, 3
    print(maxRectangles(L, B, l, b))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the
    // maximum rectangles possible
    static int maxRectangles(int L, int B,
                                int l, int b)
    {
        int horizontal = 0, vertical = 0;

        // Cut rectangles horizontally if possible
        if (l <= L && b <= B)
        {

            // One rectangle is a single cell
            int columns = B / b;
            int rows = L / l;

            // Total rectangles = total cells
            horizontal = rows * columns;
        }

        // Cut rectangles vertically if possible
        if (l <= B && b <= L)
        {
            int columns = L / b;
            int rows = B / l;
            vertical = rows * columns;
        }

        // Return the maximum possible rectangles
        return Math.Max(horizontal, vertical);
    }

    // Driver code
    public static void Main()
    {
        int L = 10, B = 7, l = 4, b = 3;
        Console.WriteLine(maxRectangles(L, B, l, b));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum
// rectangles possible
function maxRectangles($L, $B, $l, $b)
{
    $horizontal = 0;
    $vertical = 0;

    // Cut rectangles horizontally if possible
    if ($l <= $L && $b <= $B)
    {

        // One rectangle is a single cell
        $columns = (int)($B / $b);
        $rows = (int)($L / $l);

        // Total rectangles = total cells
        $horizontal = $rows * $columns;
    }

    // Cut rectangles vertically if possible
    if ($l <= $B && $b <= $L)
    {
        $columns = (int)($L / $b);
        $rows = (int)($B / $l);

        $vertical = $rows * $columns;
    }

    // Return the maximum possible rectangles
    return max($horizontal, $vertical);
}

// Driver code
$L = 10;
$B = 7;
$l = 4;
$b = 3;
print(maxRectangles($L, $B, $l, $b));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum
// rectangles possible
function maxRectangles(L, B, l, b)
{
    var horizontal = 0, vertical = 0;

    // Cut rectangles horizontally
    // if possible
    if (l <= L && b <= B)
    {

        // One rectangle is a single cell
        var columns = parseInt(B / b);
        var rows = parseInt(L / l);

        // Total rectangles = total cells
        horizontal = rows * columns;
    }

    // Cut rectangles vertically if possible
    if (l <= B && b <= L)
    {
        var columns = parseInt(L / b);
        var rows = parseInt(B / l);

        vertical = rows * columns;
    }

    // Return the maximum possible rectangles
    return Math.max(horizontal, vertical);
}

// Driver Code
var L = 10, B = 7, l = 4, b = 3;

document.write(maxRectangles(L, B, l, b));

// This code is contributed by kirti

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)