# 给定大小为 LxW 的矩形可外切的最大面积

> 原文:[https://www . geeksforgeeks . org/给定大小的最大外接矩形面积-lxw/](https://www.geeksforgeeks.org/maximum-area-of-a-rectangle-that-can-be-circumscribed-about-a-given-rectangle-of-size-lxw/)

给定一个矩形尺寸 **L** 和 **W** 。任务是找到一个矩形的最大面积，这个矩形可以用尺寸 **L** 和 **W** 围绕一个给定的矩形进行外切。

**示例:**

> **输入:** L = 10，W = 10
> T3】输出: 200
> 
> **输入:** L = 18，W = 12
> T3】输出: 450

**方法:**让下面是给定的矩形 **EFGH** 的尺寸 **L** 和 **W** 。我们必须找到矩形 **ABCD** 的面积，它是外接矩形 **EFGH** 。

![](img/98962504f2c5c5fe8ea39efc50bca7ab.png)

上图:
如果![\angle ABC = X ](img/61211ef2a33e41f302f151710b89defb.png "Rendered by QuickLaTeX.com")那么![\angle CGF = 90 - X ](img/0153a3324fd3fedfaa6aacc28a881ba5.png "Rendered by QuickLaTeX.com")作为 GCF 就是直角三角形。
因此，
![\angle HGD = 180 - \angle FGH - \angle CGF ](img/8c289274169e253a4967b0024600f4af.png "Rendered by QuickLaTeX.com")
=>![\angle HGD = 180 - 90 - (90 - X) ](img/e8841ec078f6c852403658e16c671f1a.png "Rendered by QuickLaTeX.com")
=>![\angle HGD = X ](img/b0c13d24fd5882e62b7654ce412b907a.png "Rendered by QuickLaTeX.com")
同样，
![\angle EHA = X ](img/b52ff6691770dff97f1bf527250fffd8.png "Rendered by QuickLaTeX.com")
![\angle FEB = X ](img/d99e73932c492fe9c28ab56b848e208e.png "Rendered by QuickLaTeX.com")
现在，矩形 ABCD 的面积由:
给出

> 面积= AB * AD
> 面积= (AE + EB)*(AH + HD) …..(1)

> 根据投影规则:
> AE = L * sin(X)
> EB = W * cos(X)
> AH = L * cos(X)
> HD = W * sin(X)

将上述投影的值代入等式(1)，我们得到:

> ![Area = (AE + EB)*(AH + HD) ](img/40204017111b1759538bf546fc3a937c.png "Rendered by QuickLaTeX.com")
> ![Area = (L*sin(X)+ W*cox(X))*(L*cos(X) + W*sin(X)) ](img/d45784897f4e53ebcf0eda99b0ed50dc.png "Rendered by QuickLaTeX.com")
> ![Area = ((L^{2} + W^{2})*sin(X)*cos(X) + L*W) ](img/9c64a3c9a2680de3078df850f872656b.png "Rendered by QuickLaTeX.com")
> ![Area = (\frac{(L^{2} + W^{2})*sin(2X)}{2} + L*W) ](img/c2e1374a1cdcd35cc8eb0b38ed648eb8.png "Rendered by QuickLaTeX.com")
> 现在要最大化面积，罪恶值(2X)必须最大化即 1。
> 因此在将罪恶(2X)替换为 1 之后，我们有
> ![Area = (\frac{(L^{2} + W^{2})}{2} + L*W) ](img/dcf60fe868da12ef88ec66bda0defb62.png "Rendered by QuickLaTeX.com")
> ![Area = (\frac{(L+W)^{2}}{2}) ](img/d71d9874ceeeeeb833d9fe03f3735abf.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find area of rectangle
// inscribed another rectangle of
// length L and width W
double AreaofRectangle(int L, int W)
{

    // Area of rectangle
    double area = (W + L) * (W + L) / 2;

    // Return the area
    return area;
}

// Driver Code
int main()
{

    // Given dimensions
    int L = 18;
    int W = 12;

    // Function call
    cout << AreaofRectangle(L, W);
    return 0;
}

// This code is contributed by Princi Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find area of rectangle
// inscribed another rectangle of
// length L and width W
static double AreaofRectangle(int L, int W)
{

    // Area of rectangle
    double area = (W + L) * (W + L) / 2;

    // Return the area
    return area;
}

// Driver Code
public static void main(String args[])
{

    // Given dimensions
    int L = 18;
    int W = 12;

    // Function call
    System.out.println(AreaofRectangle(L, W));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find area of rectangle
# inscribed another rectangle of
# length L and width W
def AreaofRectangle(L, W):

  # Area of rectangle
  area =(W + L)*(W + L)/2

# Return the area
  return area

# Driver Code
if __name__ == "__main__":

  # Given Dimensions
  L = 18
  W = 12

  # Function Call
  print(AreaofRectangle(L, W))
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find area of rectangle
// inscribed another rectangle of
// length L and width W
static double AreaofRectangle(int L, int W)
{

    // Area of rectangle
    double area = (W + L) * (W + L) / 2;

    // Return the area
    return area;
}

// Driver Code
public static void Main(String []args)
{

    // Given dimensions
    int L = 18;
    int W = 12;

    // Function call
    Console.Write(AreaofRectangle(L, W));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach

      // Function to find area of rectangle
      // inscribed another rectangle of
      // length L and width W
      function AreaofRectangle(L, W) {
        // Area of rectangle
        var area = parseFloat(((W + L) * (W + L)) / 2).toFixed(1);

        // Return the area
        return area;
      }

      // Driver Code
      // Given dimensions
      var L = 18;
      var W = 12;

      // Function call
      document.write(AreaofRectangle(L, W));
    </script>
```

**Output:** 

```
450.0
```

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*