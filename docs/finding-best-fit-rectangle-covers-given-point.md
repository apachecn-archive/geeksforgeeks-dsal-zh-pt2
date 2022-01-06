# 寻找覆盖给定点的最佳拟合矩形

> 原文:[https://www . geesforgeks . org/find-最佳拟合-矩形-封面-给定点/](https://www.geeksforgeeks.org/finding-best-fit-rectangle-covers-given-point/)

我们有一个 2D 平面和一个点(![X  ](img/7071aad526c32d3465fcf414c4d866ba.png "Rendered by QuickLaTeX.com")、![Y  ](img/f9cf20b910c48236b50f5002c3b8e9a9.png "Rendered by QuickLaTeX.com"))。我们必须找到一个矩形(![X_1  ](img/8a1a30fd7a31d1cfc734b9f2b36481ca.png "Rendered by QuickLaTeX.com")、![Y_1  ](img/4d0b11317b872702c8dffe5b5bf1b10e.png "Rendered by QuickLaTeX.com")、![X_2  ](img/d7064281f97a3ae8952b7cbe40ef47d6.png "Rendered by QuickLaTeX.com")、![Y_2  ](img/f92280609e836b659465c4b8356c2b36.png "Rendered by QuickLaTeX.com"))使其
包含给定点(![X  ](img/7071aad526c32d3465fcf414c4d866ba.png "Rendered by QuickLaTeX.com")、![Y  ](img/f9cf20b910c48236b50f5002c3b8e9a9.png "Rendered by QuickLaTeX.com"))。选择的矩形必须满足给定的条件![\frac{length}{breadth}=\frac{a}{b}  ](img/4eab1a1adc43cba560695eea5777081c.png "Rendered by QuickLaTeX.com")。如果
多个矩形是可能的，我们必须选择矩形中心和点之间欧几里德距离最小的一个(![X  ](img/7071aad526c32d3465fcf414c4d866ba.png "Rendered by QuickLaTeX.com")、![Y  ](img/f9cf20b910c48236b50f5002c3b8e9a9.png "Rendered by QuickLaTeX.com"))。

![](img/959dda90c99c993b569ddc2c3cc0d76a.png)

图片来源–[代号](http://codeforces.com/problemset/problem/303/B?locale=ru)
**示例:**

```
Input : 70 10 20 5 5 3
Output :12 0 27 9

Input :100 100 32 63 2 41
Output :30 18 34 100
```

问题背后的逻辑如下。首先我们通过将 a 和 b 除以![gcd(a, b)  ](img/ccd022f6348166667cc47dd81fdf34d7.png "Rendered by QuickLaTeX.com")将![\frac{a}{b}  ](img/c9fa1d854cf758b2d9c6972a425d01eb.png "Rendered by QuickLaTeX.com")简化为最低不可约形式。我们以两个独立的维度![X  ](img/7071aad526c32d3465fcf414c4d866ba.png "Rendered by QuickLaTeX.com")和![Y  ](img/f9cf20b910c48236b50f5002c3b8e9a9.png "Rendered by QuickLaTeX.com")独立思考这个问题。我们通过将 a 和 b 除以它们的 gcd 找到![min(n/a, m/b)  ](img/0716a53cf3b5aa47fa776e9dd8fc4b03.png "Rendered by QuickLaTeX.com")，从而找到我们在![(0, 0) to (n, m)  ](img/da96e01bfc4fe7481e7da1accfe0d1b9.png "Rendered by QuickLaTeX.com")范围内可以安全行驶的最大距离。由于我们必须找到中心距点(![X  ](img/7071aad526c32d3465fcf414c4d866ba.png "Rendered by QuickLaTeX.com")、![Y  ](img/f9cf20b910c48236b50f5002c3b8e9a9.png "Rendered by QuickLaTeX.com"))距离最小的矩形，因此我们从假设点(![X  ](img/7071aad526c32d3465fcf414c4d866ba.png "Rendered by QuickLaTeX.com")、![Y  ](img/f9cf20b910c48236b50f5002c3b8e9a9.png "Rendered by QuickLaTeX.com"))是我们的中心开始。然后我们通过对![X  ](img/7071aad526c32d3465fcf414c4d866ba.png "Rendered by QuickLaTeX.com")减去和加上一半的长度来找到![X_1  ](img/8a1a30fd7a31d1cfc734b9f2b36481ca.png "Rendered by QuickLaTeX.com")和![X_2  ](img/d7064281f97a3ae8952b7cbe40ef47d6.png "Rendered by QuickLaTeX.com")。如果![X_1  ](img/8a1a30fd7a31d1cfc734b9f2b36481ca.png "Rendered by QuickLaTeX.com")或![X_2  ](img/d7064281f97a3ae8952b7cbe40ef47d6.png "Rendered by QuickLaTeX.com")超出范围，我们相应地移动坐标，使其在范围![(0, 0) to (n, m)  ](img/da96e01bfc4fe7481e7da1accfe0d1b9.png "Rendered by QuickLaTeX.com")内。同样，我们继续计算![Y_1  ](img/4d0b11317b872702c8dffe5b5bf1b10e.png "Rendered by QuickLaTeX.com")和![Y_2  ](img/f92280609e836b659465c4b8356c2b36.png "Rendered by QuickLaTeX.com")。
根据上述逻辑，第一个例子的答案是![12, 0, 27, 9  ](img/5d3ab2f95d311227bb861e653504f976.png "Rendered by QuickLaTeX.com")。

## C++

```
#include <cmath>
#include <iostream>
using namespace std;

// Function to calculate
// GCD of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    else
        return gcd(b % a, a);
}

// Function to calculate the
// coordinates of the rectangle
void solve(int n, int m, int x, int y, int a, int b)
{

    int k, g;
    int x1, y1, x2, y2;
    g = gcd(a, b);

    // Reducing the ratio to
    // lowest irreducible form
    a /= g;
    b /= g;

    // Finding the maximum multiple
    // of length that can be chosen
    k = min(n / a, m / b);

    // Assuming the point (X, Y) as the
    // centre of the required rectangle
    // Finding the lower X coordinate by
    // subtracting half of total length from X
    x1 = x - (k * a - k * a / 2);

    // Finding the upper X coordinate
    // by adding half of total length to X
    x2 = x + k * a / 2;

    // Finding lower Y coordinate by
    // subtracting half of breadth from Y
    y1 = y - (k * b - k * b / 2);

    // Finding upper Y coordinate
    // by adding half of breadth to Y
    y2 = y + k * b / 2;

    // If lower X coordinate
    // goes below 0 then we shift
    // the lower coordinate to 0
    // and the upper coordinate
    // accordingly to bring lower
    // coordinate in range
    // and to keep center as
    // close as possible to X, Y
    if (x1 < 0) {
        x2 -= x1;
        x1 = 0;
    }

    // If upper X coordinate goes
    // beyond n, then we shift the
    // upper X coordinate ton
    // and we shift the lower coordinate
    // accordingly to bring the upper
    // coordinate in range
    if (x2 > n) {
        x1 -= x2 - n;
        x2 = n;
    }

    // If lower Y coordinate goes
    // below 0 then we shift the
    // lower coordinate to 0
    // and the upper coordinate
    // accordingly to bring lower
    // coordinate in range
    // and to keep center as
    // close as possible to X, Y
    if (y1 < 0) {
        y2 -= y1;
        y1 = 0;
    }

    // If upper Y coordinate goes
    // beyond n, then we shift the
    // upper X coordinate
    // to n and we shift the lower
    // coordinate accordingly to
    // bring the upper
    // coordinate in range
    if (y2 > m) {
        y1 -= y2 - m;
        y2 = m;
    }

    cout << x1 << " " << y1 << " " << x2
         << " " << y2 << endl;
}

// Driver function
int main()
{
    int n = 70, m = 10, x = 20, y = 5, a = 5, b = 3;
    solve(n, m, x, y, a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {

    // Function to calculate
    // GCD of a and b
    public static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        else
            return gcd(b % a, a);
    }

    // Function to calculate the
    // coordinates of the rectangle
    public static void solve(int n, int m,
                             int x, int y,
                             int a, int b)
    {

        int k, g;
        int x1, y1, x2, y2;
        g = gcd(a, b);

        // Reducing the ratio to
        // lowest irreducible form
        a /= g;
        b /= g;

        // Finding the maximum multiple
        // of length that can be chosen
        k = Math.min(n / a, m / b);

        // Assuming the point (X, Y) as the
        // centre of the required rectangle
        // Finding the lower X coordinate by
        // subtracting half of total length
        // from X
        x1 = x - (k * a - k * a / 2);

        // Finding the upper X coordinate
        // by adding half of total length
        // to X
        x2 = x + k * a / 2;

        // Finding lower Y coordinate by
        // subtracting half of breadth
        // from Y
        y1 = y - (k * b - k * b / 2);

        // Finding upper Y coordinate
        // by adding half of breadth
        // to Y
        y2 = y + k * b / 2;

        // If lower X coordinate
        // goes below 0 then we shift
        // the lower coordinate to 0
        // and the upper coordinate
        // accordingly to bring lower
        // coordinate in range
        // and to keep center as
        // close as possible to X, Y
        if (x1 < 0) {
            x2 -= x1;
            x1 = 0;
        }

        // If upper X coordinate goes
        // beyond n, then we shift the
        // upper X coordinate ton
        // and we shift the lower coordinate
        // accordingly to bring the upper
        // coordinate in range
        if (x2 > n) {
            x1 -= x2 - n;
            x2 = n;
        }

        // If lower Y coordinate goes
        // below 0 then we shift the
        // lower coordinate to 0
        // and the upper coordinate
        // accordingly to bring lower
        // coordinate in range
        // and to keep center as
        // close as possible to X, Y
        if (y1 < 0) {
            y2 -= y1;
            y1 = 0;
        }

        // If upper Y coordinate goes
        // beyond n, then we shift the
        // upper X coordinate
        // to n and we shift the lower
        // coordinate accordingly to
        // bring the upper
        // coordinate in range
        if (y2 > m) {
            y1 -= y2 - m;
            y2 = m;
        }

        System.out.println(x1 + " " + y1 + " " + x2
                           + " " + y2);
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 70, m = 10;
        int x = 20, y = 5;
        int a = 5, b = 3;
        solve(n, m, x, y, a, b);
    }
}

// This code is contributed by - vkz6198
```

## 蟒蛇 3

```
# Function to calculate
# GCD of a and b
def gcd(a, b):

    if (a == 0):
        return b
    else:
        return gcd(b % a, a)

# Function to calculate the
# coordinates of the rectangle
def solve(n, m, x, y, a, b):

    g = int(gcd(a, b))

    # Reducing the ratio to
    # lowest irreducible form
    a /= g
    b /= g

    # Finding the maximum multiple
    # of length that can be chosen
    k = int(min(n / a, m / b))

    # Assuming the point (X, Y) as the
    # centre of the required rectangle
    # Finding the lower X coordinate by
    # subtracting half of total length
    # from X
    x1 = int(x - (k * a - k * a / 2))

    # Finding the upper X coordinate
    # by adding half of total length
    # to X
    x2 = int(x + k * a / 2)

    # Finding lower Y coordinate by
    # subtracting half of breadth from Y
    y1 = int(y - (k * b - k * b / 2))

    # Finding upper Y coordinate
    # by adding half of breadth to Y
    y2 = int(y + k * b / 2)

    # If lower X coordinate
    # goes below 0 then we shift
    # the lower coordinate to 0
    # and the upper coordinate
    # accordingly to bring lower
    # coordinate in range
    # and to keep center as
    # close as possible to X, Y
    if (int(x1) < 0):
        x2 -= x1
        x1 = 0

    # If upper X coordinate goes
    # beyond n, then we shift the
    # upper X coordinate ton
    # and we shift the lower coordinate
    # accordingly to bring the upper
    # coordinate in range
    if (int(x2) > n):
        x1 -= x2 - n
        x2 = n

    # If lower Y coordinate goes
    # below 0 then we shift the
    # lower coordinate to 0
    # and the upper coordinate
    # accordingly to bring lower
    # coordinate in range
    # and to keep center as
    # close as possible to X, Y
    if (int(y1) < 0) :
        y2 -= y1
        y1 = 0

    # If upper Y coordinate goes
    # beyond n, then we shift the
    # upper X coordinate
    # to n and we shift the lower
    # coordinate accordingly to
    # bring the upper
    # coordinate in range
    if (int(y2) > m):
        y1 -= y2 - m
        y2 = m

    print(x1 , " " , y1 , " " , x2
        , " " , y2,sep="")

# Driver function
n = 70
m = 10
x = 20
y = 5
a = 5
b = 3
solve(n, m, x, y, a, b)

# This code is contributed by Smitha
```

## C#

```
using System;

class GFG {

    // Function to calculate
    // GCD of a and b
    public static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        else
            return gcd(b % a, a);
    }

    // Function to calculate the
    // coordinates of the rectangle
    public static void solve(int n, int m,
                            int x, int y,
                            int a, int b)
    {

        int k, g;
        int x1, y1, x2, y2;
        g = gcd(a, b);

        // Reducing the ratio to
        // lowest irreducible form
        a /= g;
        b /= g;

        // Finding the maximum multiple
        // of length that can be chosen
        k = Math.Min(n / a, m / b);

        // Assuming the point (X, Y) as the
        // centre of the required rectangle
        // Finding the lower X coordinate by
        // subtracting half of total length
        // from X
        x1 = x - (k * a - k * a / 2);

        // Finding the upper X coordinate
        // by adding half of total length
        // to X
        x2 = x + k * a / 2;

        // Finding lower Y coordinate by
        // subtracting half of breadth
        // from Y
        y1 = y - (k * b - k * b / 2);

        // Finding upper Y coordinate
        // by adding half of breadth
        // to Y
        y2 = y + k * b / 2;

        // If lower X coordinate
        // goes below 0 then we shift
        // the lower coordinate to 0
        // and the upper coordinate
        // accordingly to bring lower
        // coordinate in range
        // and to keep center as
        // close as possible to X, Y
        if (x1 < 0) {
            x2 -= x1;
            x1 = 0;
        }

        // If upper X coordinate goes
        // beyond n, then we shift the
        // upper X coordinate ton
        // and we shift the lower coordinate
        // accordingly to bring the upper
        // coordinate in range
        if (x2 > n) {
            x1 -= x2 - n;
            x2 = n;
        }

        // If lower Y coordinate goes
        // below 0 then we shift the
        // lower coordinate to 0
        // and the upper coordinate
        // accordingly to bring lower
        // coordinate in range
        // and to keep center as
        // close as possible to X, Y
        if (y1 < 0) {
            y2 -= y1;
            y1 = 0;
        }

        // If upper Y coordinate goes
        // beyond n, then we shift the
        // upper X coordinate
        // to n and we shift the lower
        // coordinate accordingly to
        // bring the upper
        // coordinate in range
        if (y2 > m) {
            y1 -= y2 - m;
            y2 = m;
        }

        Console.Write(x1 + " " + y1 +
                 " " + x2 + " " + y2);
    }

    // Driver Code
    public static void Main()
    {
        int n = 70, m = 10;
        int x = 20, y = 5;
        int a = 5, b = 3;
        solve(n, m, x, y, a, b);
    }
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to calculate
// GCD of a and b

function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    else
        return gcd($b % $a, $a);
}

// Function to calculate the
// coordinates of the rectangle
function solve($n, $m, $x, $y, $a, $b)
{

    $k; $g;
    $x1; $y1; $x2; $y2;
    $g = gcd($a, $b);

    // Reducing the ratio to
    // lowest irreducible form
    $a /= $g;
    $b /= $g;

    // Finding the maximum multiple
    // of length that can be chosen
    $k = min($n / $a, $m / $b);

    // Assuming the point (X, Y)
    // as the centre of the required
    // rectangle Finding the lower
    // X coordinate by subtracting
    // half of total length from X
    $x1 = $x - ($k * $a - $k * $a / 2);

    // Finding the upper X
    // coordinate by adding
    // half of total length to X
    $x2 = $x + $k * $a / 2;

    // Finding lower Y coordinate by
    // subtracting half of breadth from Y
    $y1 = $y - ($k * $b - $k * $b / 2);

    // Finding upper Y coordinate
    // by adding half of breadth to Y
    $y2 = $y + $k * $b / 2;

    // If lower X coordinate
    // goes below 0 then we shift
    // the lower coordinate to 0
    // and the upper coordinate
    // accordingly to bring lower
    // coordinate in range
    // and to keep center as
    // close as possible to X, Y
    if ($x1 < 0)
    {
        $x2 -= $x1;
        $x1 = 0;
    }

    // If upper X coordinate goes
    // beyond n, then we shift the
    // upper X coordinate ton
    // and we shift the lower coordinate
    // accordingly to bring the upper
    // coordinate in range
    if ($x2 > $n)
    {
        $x1 -= $x2 - $n;
        $x2 = $n;
    }

    // If lower Y coordinate goes
    // below 0 then we shift the
    // lower coordinate to 0
    // and the upper coordinate
    // accordingly to bring lower
    // coordinate in range
    // and to keep center as
    // close as possible to X, Y
    if ($y1 < 0)
    {
        $y2 -= $y1;
        $y1 = 0;
    }

    // If upper Y coordinate goes
    // beyond n, then we shift the
    // upper X coordinate
    // to n and we shift the lower
    // coordinate accordingly to
    // bring the upper
    // coordinate in range
    if ($y2 > $m)
    {
        $y1 -= $y2 - $m;
        $y2 = $m;
    }

    echo $x1, " ", $y1, " ",
         $x2, " ", $y2, "\n";
}

// Driver Code
$n = 70; $m = 10; $x = 20;
$y = 5; $a = 5; $b = 3;
solve($n, $m, $x, $y, $a, $b);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
    // Function to calculate
    // GCD of a and b
    function gcd(a, b)
    {
        if (a == 0)
            return b;
        else
            return gcd(b % a, a);
    }

    // Function to calculate the
    // coordinates of the rectangle
    function solve(n, m, x, y, a, b)
    {

        let k, g;
        let x1, y1, x2, y2;
        g = gcd(a, b);

        // Reducing the ratio to
        // lowest irreducible form
        a = a / g;
        b = b / g;

        // Finding the maximum multiple
        // of length that can be chosen
        k = Math.min(parseInt(n / a, 10), parseInt(m / b, 10));

        // Assuming the point (X, Y) as the
        // centre of the required rectangle
        // Finding the lower X coordinate by
        // subtracting half of total length
        // from X
        x1 = x - (k * a - k * parseInt(a / 2, 10));

        // Finding the upper X coordinate
        // by adding half of total length
        // to X
        x2 = x + k * parseInt(a / 2, 10);

        // Finding lower Y coordinate by
        // subtracting half of breadth
        // from Y
        y1 = y - (k * b - k * parseInt(b / 2, 10));

        // Finding upper Y coordinate
        // by adding half of breadth
        // to Y
        y2 = y + k * parseInt(b / 2, 10);

        // If lower X coordinate
        // goes below 0 then we shift
        // the lower coordinate to 0
        // and the upper coordinate
        // accordingly to bring lower
        // coordinate in range
        // and to keep center as
        // close as possible to X, Y
        if (x1 < 0) {
            x2 -= x1;
            x1 = 0;
        }

        // If upper X coordinate goes
        // beyond n, then we shift the
        // upper X coordinate ton
        // and we shift the lower coordinate
        // accordingly to bring the upper
        // coordinate in range
        if (x2 > n) {
            x1 -= x2 - n;
            x2 = n;
        }

        x1 += 1; x2 += 1;

        // If lower Y coordinate goes
        // below 0 then we shift the
        // lower coordinate to 0
        // and the upper coordinate
        // accordingly to bring lower
        // coordinate in range
        // and to keep center as
        // close as possible to X, Y
        if (y1 < 0) {
            y2 -= y1;
            y1 = 0;
        }

        // If upper Y coordinate goes
        // beyond n, then we shift the
        // upper X coordinate
        // to n and we shift the lower
        // coordinate accordingly to
        // bring the upper
        // coordinate in range
        if (y2 > m) {
            y1 -= y2 - m;
            y2 = m;
        }

        document.write(x1 + " " + y1 + " " + x2 + " " + y2);
    }

    let n = 70, m = 10;
    let x = 20, y = 5;
    let a = 5, b = 3;
    solve(n, m, x, y, a, b);

</script>
```

**输出:**

```
12 0 27 9
```