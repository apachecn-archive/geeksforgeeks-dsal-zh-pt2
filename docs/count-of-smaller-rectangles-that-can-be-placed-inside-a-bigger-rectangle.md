# 可以放在大矩形内的小矩形的数量

> 原文:[https://www . geeksforgeeks . org/可放置在较大矩形内的较小矩形数量/](https://www.geeksforgeeks.org/count-of-smaller-rectangles-that-can-be-placed-inside-a-bigger-rectangle/)

给定四个整数 **L、B、l** 和 **b** ，其中 **L** 和 **B** 表示较大矩形的尺寸， **l** 和 **b** 表示较小矩形的尺寸，任务是计算可在较大矩形内绘制的较小矩形的数量。
***注意:**较小的矩形可以部分重叠。*

**示例:**

> **输入:** L = 5，B = 3，l = 4，b = 1
> **输出:** 6
> **说明:**
> 有 6 个尺寸为 4 × 1 的矩形，可以画在尺寸为 5 × 3 的更大的矩形内。
> 
> **输入:** L = 3，B = 2，l = 2，b = 1
> **输出:** 3
> **说明:**
> 有 3 个尺寸为 3 × 2 的矩形可以画在尺寸为 2 × 1 的更大的矩形里面。

**天真法:**思路是迭代大矩形的长度 **L** 和宽度 **B** 来计算尺寸 **l x b** 的小矩形的数量，这些小矩形可以在大矩形的范围内绘制。打印遍历后的总计数。
***时间复杂度:** O(L * B)*
***辅助空间:** O(1)*

**有效途径:**上述问题可以使用[排列组合](https://www.geeksforgeeks.org/permutation-and-combination/)解决。以下是步骤:

1.  使用长度 **L** 的较小矩形 **l** 的总可能长度值由**(L–L+1)**给出。
2.  使用长度 **B** 的较小矩形 **b** 的宽度的总可能值由**(B–b+ 1)**给出。
3.  因此，可以形成的可能矩形的总数由下式给出:

> (L–L+1)*(B–B+1)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count smaller rectangles
// within the larger rectangle
int No_of_rectangles(int L, int B,
                    int l, int b)
{
    // If the dimension of the smaller
    // rectangle is greater than the
    // bigger one
    if ((l > L) || (b > B)) {
        return -1;
    }

    else {

        // Return the number of smaller
        // rectangles possible
        return (L - l + 1) * (B - b + 1);
    }
}

// Driver Code
int main()
{
    // Dimension of bigger rectangle
    int L = 5, B = 3;

    // Dimension of smaller rectangle
    int l = 4, b = 1;

    // Function call
    cout << No_of_rectangles(L, B, l, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count smaller rectangles
// within the larger rectangle
static int No_of_rectangles(int L, int B,
                            int l, int b)
{

    // If the dimension of the smaller
    // rectangle is greater than the
    // bigger one
    if ((l > L) || (b > B))
    {
        return -1;
    }

    else
    {

        // Return the number of smaller
        // rectangles possible
        return (L - l + 1) * (B - b + 1);
    }
}

// Driver Code
public static void main(String[] args)
{

    // Dimension of bigger rectangle
    int L = 5, B = 3;

    // Dimension of smaller rectangle
    int l = 4, b = 1;

    // Function call
    System.out.println(No_of_rectangles(L, B, l, b));
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count smaller rectangles
# within the larger rectangle
def No_of_rectangles( L, B, l, b):

    # If the dimension of the smaller
    # rectangle is greater than the
    # bigger one
    if (l > L) or (b > B):
        return -1;

    else:

        # Return the number of smaller
        # rectangles possible
        return (L - l + 1) * (B - b + 1);

# Driver code
if __name__ == '__main__':

    # Dimension of bigger rectangle
    L = 5
    B = 3

    # Dimension of smaller rectangle
    l = 4
    b = 1

    # Function call
    print(No_of_rectangles(L, B, l, b))

# This code is contributed by jana_sayantan
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count smaller rectangles
// within the larger rectangle
static int No_of_rectangles(int L, int B,
                            int l, int b)
{

    // If the dimension of the smaller
    // rectangle is greater than the
    // bigger one
    if ((l > L) || (b > B))
    {
        return -1;
    }
    else
    {

        // Return the number of smaller
        // rectangles possible
        return (L - l + 1) * (B - b + 1);
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Dimension of bigger rectangle
    int L = 5, B = 3;

    // Dimension of smaller rectangle
    int l = 4, b = 1;

    // Function call
    Console.Write(No_of_rectangles(L, B, l, b));
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to count smaller rectangles
// within the larger rectangle
function No_of_rectangles(L, B,
                            l, b)
{

    // If the dimension of the smaller
    // rectangle is greater than the
    // bigger one
    if ((l > L) || (b > B))
    {
        return -1;
    }

    else
    {

        // Return the number of smaller
        // rectangles possible
        return (L - l + 1) * (B - b + 1);
    }
}

// Driver code

    // Dimension of bigger rectangle
    let L = 5, B = 3;

    // Dimension of smaller rectangle
    let l = 4, b = 1;

    // Function call
    document.write(No_of_rectangles(L, B, l, b));

    // This code is contributed by code_hunt.
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)