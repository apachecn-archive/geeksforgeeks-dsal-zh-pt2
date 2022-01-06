# 容纳两个相同矩形的正方形的最小面积

> 原文:[https://www . geesforgeks . org/最小面积正方形-保持两个相同的矩形/](https://www.geeksforgeeks.org/minimum-area-of-square-holding-two-identical-rectangles/)

给定两个相同矩形的长度 **L** 和宽度 **B** ，任务是找到一个正方形的最小面积，在这个正方形中可以嵌入两个尺寸相同的矩形 **L × B** 。
**举例:**

> **输入:** L = 7，B = 4
> **输出:** 64
> **说明:**两个边长为 7×4 的矩形可以拟合成边长为 8 的正方形。通过将两个边为 4 的矩形放在一起，接触长度为 7。
> **输入:** L = 1，B = 3
> **输出:** 9
> **说明:**两个边长为 1×3 的矩形可以拟合成边长为 3 的正方形。通过将两个边为 1 的矩形放在一起，并且在两个矩形之间留有 1 的间隙。

**进场:**

*   如果矩形的一边小于或等于另一边长度的一半，那么正方形的一边就是矩形的长边。
*   如果较小边的两倍长度大于较大边的两倍长度，那么正方形的边就是矩形较小边的两倍长度。

以下是上述方法的实现:

## C++

```
// C++ program for the above problem
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// area of the square
int areaSquare(int L, int B)
{
    // Larger side of rectangle
    int large = max(L, B);

    // Smaller side of the rectangle
    int small = min(L, B);

    if (large >= 2 * small)
        return large * large;
    else
        return (2 * small) * (2 * small);
}

// Driver code
int main()
{
    int L = 7;
    int B = 4;
    cout << areaSquare(L, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG{

// Function to find the
// area of the square
static int areaSquare(int L, int B)
{

    // Larger side of rectangle
    int large = Math.max(L, B);

    // Smaller side of the rectangle
    int small = Math.min(L, B);

    if (large >= 2 * small)
    {
        return large * large;
    }
    else
    {
        return (2 * small) * (2 * small);
    }
}

// Driver code
public static void main(String[] args)
{
    int L = 7;
    int B = 4;

    System.out.println(areaSquare(L, B));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above problem

# Function to find the
# area of the square
def areaSquare(L, B):

    # Larger side of rectangle
    large = max(L, B)

    # Smaller side of the rectangle
    small = min(L, B)

    if(large >= 2 * small):
        return large * large
    else:
        return (2 * small) * (2 * small)

# Driver code
if __name__ == '__main__':

    L = 7
    B = 4

    print(areaSquare(L, B))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above problem
using System;

class GFG{

// Function to find the
// area of the square
public static int areaSquare(int L, int B)
{

    // Larger side of rectangle
    int large = Math.Max(L, B);

    // Smaller side of the rectangle
    int small = Math.Min(L, B);

    if (large >= 2 * small)
    {
        return large * large;
    }
    else
    {
        return (2 * small) * (2 * small);
    }
}

// Driver code
public static void Main()
{
    int L = 7;
    int B = 4;

    Console.Write(areaSquare(L, B));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the
// area of the square
function areaSquare(L, B)
{

    // Larger side of rectangle
    let large = Math.max(L, B);

    // Smaller side of the rectangle
    let small = Math.min(L, B);

    if (large >= 2 * small)
    {
        return large * large;
    }
    else
    {
        return (2 * small) * (2 * small);
    }
}

  // Driver Code

    let L = 7;
    let B = 4;

    document.write(areaSquare(L, B));

</script>
```

**Output:** 

```
64
```

***时间复杂度:** O(1)*
***辅助空间复杂度:** O(1)*