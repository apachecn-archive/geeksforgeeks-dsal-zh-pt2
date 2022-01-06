# 填充矩形地板所需的最小方形瓷砖数量

> 原文:[https://www . geeksforgeeks . org/最小方块数-需要填充矩形地板/](https://www.geeksforgeeks.org/minimum-number-of-square-tiles-required-to-fill-the-rectangular-floor/)

给定一块(M X N)米的矩形地板，将铺上(s X s)的方形瓷砖。任务是找到铺设矩形地板所需的最小瓷砖数量。

**约束:**

1.  允许覆盖比地板大的表面，但是地板必须被覆盖。
2.  不允许打碎瓷砖。
3.  瓷砖的侧面应该与地板的侧面平行。

**示例:**

> **输入:** 2 1 2
> **输出:** 1
> 地板长度= 2
> 地板宽度= 1
> 瓷砖边长= 2
> 铺装所需瓷砖数量为 2。
> 
> **输入:**222 332 5
> T3】输出: 3015

**方法:**
给定每个瓦片的边必须平行于瓦片的边，允许我们分别分析 X 轴和 Y 轴，即需要多少段长度“s”来覆盖一段长度“s”和“N”——并取这两个量的乘积。

```
ceil(M/s) * ceil(N/s)
```

，其中 ceil(x)是大于或等于 x 的最小整数。仅使用整数，它通常写成

```
((M + s - 1) / s)*((N + s - 1) / s)
```

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of tiles
int solve(int M, int N, int s)
{
    // if breadth is divisible by side of square
    if (N % s == 0) {

        // tiles required is N/s
        N = N / s;
    }
    else {

        // one more tile required
        N = (N / s) + 1;
    }

    // if length is divisible by side of square
    if (M % s == 0) {

        // tiles required is M/s
        M = M / s;
    }
    else {
        // one more tile required
        M = (M / s) + 1;
    }

    return M * N;
}

// Driver Code
int main()
{
    // input length and breadth of
    // rectangle and side of square
    int N = 12, M = 13, s = 4;

    cout << solve(M, N, s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Function to find the
// number of tiles
static int solve(int M, int N, int s)
{
    // if breadth is divisible
    // by side of square
    if (N % s == 0)
    {

        // tiles required is N/s
        N = N / s;
    }
    else
    {

        // one more tile required
        N = (N / s) + 1;
    }

    // if length is divisible
    // by side of square
    if (M % s == 0)
    {

        // tiles required is M/s
        M = M / s;
    }
    else
    {

        // one more tile required
        M = (M / s) + 1;
    }

    return M * N;
}

// Driver Code
public static void main(String args[])
{
    // input length and breadth of
    // rectangle and side of square
    int N = 12, M = 13, s = 4;

    System.out.println(solve(M, N, s));
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach

# Function to find the number
# of tiles
def solve(M, N, s) :

    # if breadth is divisible
    # by side of square
    if (N % s == 0) :

        # tiles required is N/s
        N = N // s

    else :

        # one more tile required
        N = (N // s) + 1

    # if length is divisible by
    # side of square
    if (M % s == 0) :

        # tiles required is M/s
        M = M // s

    else :

        # one more tile required
        M = (M // s) + 1

    return M * N

# Driver Code
if __name__ == "__main__" :

    # input length and breadth of
    # rectangle and side of square
    N, M, s = 12, 13, 4

    print(solve(M, N, s))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to find the
// number of tiles
static int solve(int M, int N, int s)
{
    // if breadth is divisible
    // by side of square
    if (N % s == 0)
    {

        // tiles required is N/s
        N = N / s;
    }
    else
    {

        // one more tile required
        N = (N / s) + 1;
    }

    // if length is divisible
    // by side of square
    if (M % s == 0)
    {

        // tiles required is M/s
        M = M / s;
    }
    else
    {

        // one more tile required
        M = (M / s) + 1;
    }

    return M * N;
}

// Driver Code
static void Main()
{
    // input length and breadth of
    // rectangle and side of square
    int N = 12, M = 13, s = 4;

    Console.WriteLine(solve(M, N, s));
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the number of tiles
function solve($M, $N, $s)
{
    // if breadth is divisible
    // by side of square
    if ($N % $s == 0)
    {

        // tiles required is N/s
        $N = $N / $s;
    }
    else
    {

        // one more tile required
        $N = ($N / $s) + 1;
    }

    // if length is divisible
    // by side of square
    if ($M % $s == 0)
    {

        // tiles required is M/s
        $M = $M / $s;
    }
    else
    {

        // one more tile required
        $M = ($M / $s) + 1;
    }

    return (int)$M * $N;
}

// Driver Code

// input length and breadth of
// rectangle and side of square
$N = 12;
$M = 13;
$s = 4;

echo solve($M, $N, $s);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation
// of above approach

// Function to find the
// number of tiles
function solve(M, N, s)
{

    // If breadth is divisible
    // by side of square
    if (N % s == 0)
    {

        // Tiles required is N/s
        N = N / s;
    }
    else
    {

        // One more tile required
        N = (N / s) + 1;
    }

    // If length is divisible
    // by side of square
    if (M % s == 0)
    {

        // Tiles required is M/s
        M = M / s;
    }
    else
    {

        // One more tile required
        M = (M / s) + 1;
    }
    return parseInt(M * N);
}

// Driver Code

// Input length and breadth of
// rectangle and side of square
var N = 12, M = 13, s = 4;

document.write(solve(M, N, s));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
12
```

**使用** [**天花板功能**](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) **:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of tiles
int solve(double M, double N, double s)
{
    // no of tiles
    int ans = ((int)(ceil(M / s)) * (int)(ceil(N / s)));

    return ans;
}

// Driver Code
int main()
{
    // input length and breadth of
    // rectangle and side of square
    double N = 12, M = 13, s = 4;

    cout << solve(M, N, s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{
// Function to find the number of tiles
static int solve(double M,
                 double N, double s)
{
    // no of tiles
    int ans = ((int)(Math.ceil(M / s)) *
               (int)(Math.ceil(N / s)));

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    // input length and breadth of
    // rectangle and side of square
    double N = 12, M = 13, s = 4;

    System.out.println(solve(M, N, s));
}
}

// This Code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach
import math

# Function to find the
# number of tiles
def solve(M, N, s):

    # no of tiles
    ans = ((math.ceil(M / s)) *
           (math.ceil(N / s)));

    return ans

# Driver Code
if __name__ == "__main__":

    # input length and breadth of
    # rectangle and side of square
    N = 12
    M = 13
    s = 4

    print(solve(M, N, s))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;
class GFG
{
// Function to find the number of tiles
static int solve(double M,
                double N, double s)
{
    // no of tiles
    int ans = ((int)(Math.Ceiling(M / s)) *
            (int)(Math.Ceiling(N / s)));

    return ans;
}

// Driver Code
public static void Main()
{
    // input length and breadth of
    // rectangle and side of square
    double N = 12, M = 13, s = 4;

    Console.WriteLine(solve(M, N, s));
}
}

// This Code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of
// above approach

// Function to find the
// number of tiles
function solve($M, $N, $s)
{
    // no of tiles
    $ans = ((int)(ceil($M / $s)) *
            (int)(ceil($N / $s)));

    return $ans;
}

// Driver Code

// input length and breadth of
// rectangle and side of square
$N = 12;
$M = 13;
$s = 4;

echo solve($M, $N, $s);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to find the number of tiles
function solve(M, N, s)
{

    // No of tiles
    let ans = Math.floor(((Math.ceil(M / s)) *
                          (Math.ceil(N / s))));

    return ans;
}

// Driver Code

// Input length and breadth of
// rectangle and side of square
let N = 12, M = 13, s = 4;

document.write(solve(M, N, s));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
12
```