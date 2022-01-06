# 到达矩阵中最后一栋建筑的最小跳跃次数

> 原文:[https://www . geesforgeks . org/最小跳跃到达矩阵中的最后一个建筑/](https://www.geeksforgeeks.org/minimum-jumps-to-reach-last-building-in-a-matrix/)

给定一个包含整数值的矩阵，其中矩阵的每个单元格代表建筑物的高度。找到从第一个建筑(0，0)到最后一个建筑(n-1，m-1)所需的最小跳跃。从一个单元格跳到下一个单元格是两个建筑高度的绝对差。

**示例:**

```
Input :  int height[][] = {{ 5, 4, 2 },
                           { 9, 2, 1 },
                           { 2, 5, 9 },
                           { 1, 3, 11}}; 
Output : 12
The minimum jump path is 5 -> 2 -> 5
-> 11\. Total jumps is 3 + 3 + 6 = 12.
```

**天真的递归解法:**
用递归很容易解决上面的问题。到达(m，n)的路径必须通过 3 个单元之一:(m-1，n-1)或(m-1，n)或(m，n-1)。所以最小跳跃达到(m，n)可以写成“3 个单元的最小跳跃加上当前跳跃。
以下是实施办法。

## C++

```
// Recursive CPP program to find minimum jumps
// to reach last building from first.
#include <bits/stdc++.h>
using namespace std;

# define R 4
# define C 3

bool isSafe(int x, int y)
{
    return (x < R && y < C);
}

/* Returns minimum jump path from (0, 0) to
  (m, n) in height[R][C]*/
int minJump(int height[R][C], int x, int y)
{
    // base case
    if (x == R - 1 && y == C - 1)
        return 0;

    // Find minimum jumps if we go through diagonal
    int diag = INT_MAX;
    if (isSafe(x + 1, y + 1))
        diag = minJump(height, x + 1, y + 1) +
           abs(height[x][y] - height[x + 1][y + 1]);

    // Find minimum jumps if we go through down
    int down = INT_MAX;
    if (isSafe(x + 1, y))
        down = minJump(height, x + 1, y) +
             abs(height[x][y] - height[x + 1][y]);

    // Find minimum jumps if we go through right
    int right = INT_MAX;
    if (isSafe(x, y + 1))
        right = minJump(height, x, y + 1) +
              abs(height[x][y] - height[x][y + 1]);

    // return minimum jumps
    return min({down, right, diag});
}

/* Driver program to test above functions */
int main()
{
    int height[][C] = { { 5, 4, 2 },
                       { 9, 2, 1 },
                       { 2, 5, 9 },
                       { 1, 3, 11 } };

    cout << minJump(height, 0, 0);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program
// to find minimum jumps
// to reach last building
// from first.
class GFG {

    static boolean isSafe(int x, int y)
    {
        return (x < 4 && y < 3);
    }

    // Returns minimum jump
    // path from (0, 0) to
    // (m, n) in height[R][C]
    static int minJump(int height[][], int x,
                                       int y)
    {
        // base case
        if (x == 4 - 1 && y == 3 - 1)
            return 0;

        // Find minimum jumps
        // if we go through
        // diagonal
        int diag = Integer.MAX_VALUE;

        if (isSafe(x + 1, y + 1))
            diag = minJump(height, x + 1, y + 1) +
                   Math.abs(height[x][y] - height[x + 1][y + 1]);

        // Find minimum jumps
        // if we go through
        // down
        int down = Integer.MAX_VALUE;

        if (isSafe(x + 1, y))
            down = minJump(height, x + 1, y) +
                   Math.abs(height[x][y] - height[x + 1][y]);

        // Find minimum jumps
        // if we go through right
        int right = Integer.MAX_VALUE;

        if (isSafe(x, y + 1))
            right = minJump(height, x, y + 1) +
                    Math.abs(height[x][y] - height[x][y + 1]);

        // return minimum jumps
        return Math.min(down, Math.min(right, diag));
    }

    // Driver program
    public static void main(String[] args)
    {
        int height[][] = { { 5, 4, 2 },
                           { 9, 2, 1 },
                           { 2, 5, 9 },
                           { 1, 3, 11} };

        System.out.println(minJump(height, 0, 0));
    }
}

// This article is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Recursive Python3 program to find minimum jumps
# to reach last building from first.
R = 4
C = 3

def isSafe(x, y):
    return (x < R and y < C)

# Returns minimum jump path from
# (0, 0) to (m, n) in height[R][C]
def minJump(height, x, y):

    # base case
    if (x == R - 1 and y == C - 1):
        return 0

    # Find minimum jumps if we go
    # through diagonal
    diag = 10**9
    if (isSafe(x + 1, y + 1)):
        diag = (minJump(height, x + 1, y + 1) +
                    abs(height[x][y] -
                        height[x + 1][y + 1]))

    # Find minimum jumps if we go through down
    down = 10**9
    if (isSafe(x + 1, y)):
        down = (minJump(height, x + 1, y) +
                    abs(height[x][y] -
                        height[x + 1][y]))

    # Find minimum jumps if we go through right
    right = 10**9
    if (isSafe(x, y + 1)):
        right = (minJump(height, x, y + 1) +
                     abs(height[x][y] -
                         height[x][y + 1]))

    # return minimum jumps
    return min([down, right, diag])

# Driver Code
height = [ [ 5, 4, 2 ],
           [ 9, 2, 1 ],
           [ 2, 5, 9 ],
           [ 1, 3, 11 ] ]

print(minJump(height, 0, 0))

# This code is contributed by mohit kumar
```

## C#

```
// Recursive C# program
// to find minimum jumps
// to reach last building
// from first.
using System;

class GFG {

    static bool isSafe(int x, int y)
    {
        return (x < 4 && y < 3);
    }

    // Returns minimum jump
    // path from (0, 0) to
    // (m, n) in height[R][C]
    static int minJump(int [,]height,
                       int x, int y)
    {

        // base case
        if (x == 4 - 1 && y == 3 - 1)
            return 0;

        // Find minimum jumps
        // if we go through
        // diagonal
        int diag = int.MaxValue;

        if (isSafe(x + 1, y + 1))
            diag = minJump(height, x + 1, y + 1) +
                   Math.Abs(height[x,y] -
                   height[x + 1,y + 1]);

        // Find minimum jumps
        // if we go through
        // down
        int down = int.MaxValue;

        if (isSafe(x + 1, y))
            down = minJump(height, x + 1, y) +
                   Math.Abs(height[x,y] -
                   height[x + 1,y]);

        // Find minimum jumps
        // if we go through right
        int right = int.MaxValue;

        if (isSafe(x, y + 1))
            right = minJump(height, x, y + 1) +
                    Math.Abs(height[x,y] -
                    height[x,y + 1]);

        // return minimum jumps
        return Math.Min(down, Math.Min(right, diag));
    }

    // Driver code
    public static void Main()
    {
        int [,]height = {{5, 4, 2},
                        {9, 2, 1},
                        {2, 5, 9},
                        {1, 3, 11}};

        Console.Write(minJump(height, 0, 0));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// Recursive PHP program to
// find minimum jumps to
// reach last building from first.
$R = 4;
$C = 3;

function isSafe($x, $y)
{
    global $R, $C;
    return ($x < $R and $y < $C);
}

// Returns minimum jump
// path from (0, 0) to
// (m, n) in height[R][C]
function minJump($height, $x, $y)
{
    global $R, $C;

    // base case
    if ($x == $R - 1 and $y == $C - 1)
        return 0;

    // Find minimum jumps if
    // we go through diagonal
    $diag = PHP_INT_MAX;
    if (isSafe($x + 1, $y + 1))
        $diag = minJump($height, $x + 1, $y + 1) +
                             abs($height[$x][$y] -
                         $height[$x + 1][$y + 1]);

    // Find minimum jumps
    // if we go through down
    $down = PHP_INT_MAX;
    if (isSafe($x + 1, $y))
        $down = minJump($height, $x + 1, $y) +
                         abs($height[$x][$y] -
                         $height[$x + 1][$y]);

    // Find minimum jumps if
    // we go through right
    $right = PHP_INT_MAX;
    if (isSafe($x, $y + 1))
        $right = minJump($height, $x, $y + 1) +
                          abs($height[$x][$y] -
                          $height[$x][$y + 1]);

    // return minimum jumps
    return min($down, min($right, $diag));
}

// Driver Code
$height = array(array( 5, 4, 2 ),
                array( 9, 2, 1 ),
                array( 2, 5, 9 ),
                array( 1, 3, 11 ));

echo minJump($height, 0, 0);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Recursive Javascript program to find minimum jumps
// to reach last building from first.
R = 4
C = 3

function isSafe(x, y)
{
    return (x < R && y < C);
}

/* Returns minimum jump path from (0, 0) to
  (m, n) in height[R][C]*/
function minJump(height, x, y)
{
    // base case
    if (x == R - 1 && y == C - 1)
        return 0;

    // Find minimum jumps if we go through diagonal
    var diag = 1000000000;
    if (isSafe(x + 1, y + 1))
        diag = minJump(height, x + 1, y + 1) +
           Math.abs(height[x][y] - height[x + 1][y + 1]);

    // Find minimum jumps if we go through down
    var down = 1000000000;
    if (isSafe(x + 1, y))
        down = minJump(height, x + 1, y) +
             Math.abs(height[x][y] - height[x + 1][y]);

    // Find minimum jumps if we go through right
    var right = 1000000000;
    if (isSafe(x, y + 1))
        right = minJump(height, x, y + 1) +
              Math.abs(height[x][y] - height[x][y + 1]);

    // return minimum jumps
    return Math.min(down, Math.min(right, diag));
}

/* Driver program to test above functions */
var height = [ [ 5, 4, 2 ],
                   [ 9, 2, 1 ],
                   [ 2, 5, 9 ],
                   [ 1, 3, 11 ] ];
document.write( minJump(height, 0, 0));

// This code is contributed by rutvik_56.
</script>
```

**输出:**

```
12
```

这个解的**时间复杂度**是**指数**。

**辅助空间:** O(1)
**动态规划解:**
如果画出上述递归解的递归树，可以观察到[重叠子问题](https://www.geeksforgeeks.org/dynamic-programming-set-1/)。由于问题有重叠的子问题，我们可以使用动态规划来有效地解决它。下面是基于动态规划的解决方案。

## C++

```
// Recursive CPP program to find minimum jumps
// to reach last building from first.
#include <bits/stdc++.h>
using namespace std;

# define R 4
# define C 3

bool isSafe(int x, int y)
{
    return (x < R && y < C);
}

/* Returns minimum jump path from (0, 0) to
  (m, n) in height[R][C]*/
int minJump(int height[R][C], int x, int y)
{
    // base case
    if (x == R - 1 && y == C - 1)
        return 0;

    // Find minimum jumps if we go through diagonal
    int diag = INT_MAX;
    if (isSafe(x + 1, y + 1))
        diag = minJump(height, x + 1, y + 1) +
           abs(height[x][y] - height[x + 1][y + 1]);

    // Find minimum jumps if we go through down
    int down = INT_MAX;
    if (isSafe(x + 1, y))
        down = minJump(height, x + 1, y) +
             abs(height[x][y] - height[x + 1][y]);

    // Find minimum jumps if we go through right
    int right = INT_MAX;
    if (isSafe(x, y + 1))
        right = minJump(height, x, y + 1) +
              abs(height[x][y] - height[x][y + 1]);

    // return minimum jumps
    return min({down, right, diag});
}

/* Driver program to test above functions */
int main()
{
    int height[][C] = { { 5, 4, 2 },
                       { 9, 2, 1 },
                       { 2, 5, 9 },
                       { 1, 3, 11 } };

    cout << minJump(height, 0, 0);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program
// to find minimum jumps
// to reach last building
// from first.
class GFG {

    static boolean isSafe(int x, int y)
    {
        return (x < 4 && y < 3);
    }

    // Returns minimum jump
    // path from (0, 0) to
    // (m, n) in height[R][C]
    static int minJump(int height[][], int x,
                                       int y)
    {
        // base case
        if (x == 4 - 1 && y == 3 - 1)
            return 0;

        // Find minimum jumps
        // if we go through
        // diagonal
        int diag = Integer.MAX_VALUE;

        if (isSafe(x + 1, y + 1))
            diag = minJump(height, x + 1, y + 1) +
                   Math.abs(height[x][y] - height[x + 1][y + 1]);

        // Find minimum jumps
        // if we go through
        // down
        int down = Integer.MAX_VALUE;

        if (isSafe(x + 1, y))
            down = minJump(height, x + 1, y) +
                   Math.abs(height[x][y] - height[x + 1][y]);

        // Find minimum jumps
        // if we go through right
        int right = Integer.MAX_VALUE;

        if (isSafe(x, y + 1))
            right = minJump(height, x, y + 1) +
                    Math.abs(height[x][y] - height[x][y + 1]);

        // return minimum jumps
        return Math.min(down, Math.min(right, diag));
    }

    // Driver program
    public static void main(String[] args)
    {
        int height[][] = { { 5, 4, 2 },
                           { 9, 2, 1 },
                           { 2, 5, 9 },
                           { 1, 3, 11} };

        System.out.println(minJump(height, 0, 0));
    }
}

// This article is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Recursive Python3 program to find minimum jumps
# to reach last building from first.
R = 4
C = 3

def isSafe(x, y):
    return (x < R and y < C)

# Returns minimum jump path from
# (0, 0) to (m, n) in height[R][C]
def minJump(height, x, y):

    # base case
    if (x == R - 1 and y == C - 1):
        return 0

    # Find minimum jumps if we go
    # through diagonal
    diag = 10**9
    if (isSafe(x + 1, y + 1)):
        diag = (minJump(height, x + 1, y + 1) +
                    abs(height[x][y] -
                        height[x + 1][y + 1]))

    # Find minimum jumps if we go through down
    down = 10**9
    if (isSafe(x + 1, y)):
        down = (minJump(height, x + 1, y) +
                    abs(height[x][y] -
                        height[x + 1][y]))

    # Find minimum jumps if we go through right
    right = 10**9
    if (isSafe(x, y + 1)):
        right = (minJump(height, x, y + 1) +
                     abs(height[x][y] -
                         height[x][y + 1]))

    # return minimum jumps
    return min([down, right, diag])

# Driver Code
height = [ [ 5, 4, 2 ],
           [ 9, 2, 1 ],
           [ 2, 5, 9 ],
           [ 1, 3, 11 ] ]

print(minJump(height, 0, 0))

# This code is contributed by mohit kumar
```

## C#

```
// Recursive C# program
// to find minimum jumps
// to reach last building
// from first.
using System;

class GFG {

    static bool isSafe(int x, int y)
    {
        return (x < 4 && y < 3);
    }

    // Returns minimum jump
    // path from (0, 0) to
    // (m, n) in height[R][C]
    static int minJump(int [,]height,
                       int x, int y)
    {

        // base case
        if (x == 4 - 1 && y == 3 - 1)
            return 0;

        // Find minimum jumps
        // if we go through
        // diagonal
        int diag = int.MaxValue;

        if (isSafe(x + 1, y + 1))
            diag = minJump(height, x + 1, y + 1) +
                   Math.Abs(height[x,y] -
                   height[x + 1,y + 1]);

        // Find minimum jumps
        // if we go through
        // down
        int down = int.MaxValue;

        if (isSafe(x + 1, y))
            down = minJump(height, x + 1, y) +
                   Math.Abs(height[x,y] -
                   height[x + 1,y]);

        // Find minimum jumps
        // if we go through right
        int right = int.MaxValue;

        if (isSafe(x, y + 1))
            right = minJump(height, x, y + 1) +
                    Math.Abs(height[x,y] -
                    height[x,y + 1]);

        // return minimum jumps
        return Math.Min(down, Math.Min(right, diag));
    }

    // Driver code
    public static void Main()
    {
        int [,]height = {{5, 4, 2},
                        {9, 2, 1},
                        {2, 5, 9},
                        {1, 3, 11}};

        Console.Write(minJump(height, 0, 0));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// Recursive PHP program to
// find minimum jumps to
// reach last building from first.
$R = 4;
$C = 3;

function isSafe($x, $y)
{
    global $R, $C;
    return ($x < $R and $y < $C);
}

// Returns minimum jump
// path from (0, 0) to
// (m, n) in height[R][C]
function minJump($height, $x, $y)
{
    global $R, $C;

    // base case
    if ($x == $R - 1 and $y == $C - 1)
        return 0;

    // Find minimum jumps if
    // we go through diagonal
    $diag = PHP_INT_MAX;
    if (isSafe($x + 1, $y + 1))
        $diag = minJump($height, $x + 1, $y + 1) +
                             abs($height[$x][$y] -
                         $height[$x + 1][$y + 1]);

    // Find minimum jumps
    // if we go through down
    $down = PHP_INT_MAX;
    if (isSafe($x + 1, $y))
        $down = minJump($height, $x + 1, $y) +
                         abs($height[$x][$y] -
                         $height[$x + 1][$y]);

    // Find minimum jumps if
    // we go through right
    $right = PHP_INT_MAX;
    if (isSafe($x, $y + 1))
        $right = minJump($height, $x, $y + 1) +
                          abs($height[$x][$y] -
                          $height[$x][$y + 1]);

    // return minimum jumps
    return min($down, min($right, $diag));
}

// Driver Code
$height = array(array( 5, 4, 2 ),
                array( 9, 2, 1 ),
                array( 2, 5, 9 ),
                array( 1, 3, 11 ));

echo minJump($height, 0, 0);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Recursive Javascript program to find minimum jumps
// to reach last building from first.
R = 4
C = 3

function isSafe(x, y)
{
    return (x < R && y < C);
}

/* Returns minimum jump path from (0, 0) to
  (m, n) in height[R][C]*/
function minJump(height, x, y)
{
    // base case
    if (x == R - 1 && y == C - 1)
        return 0;

    // Find minimum jumps if we go through diagonal
    var diag = 1000000000;
    if (isSafe(x + 1, y + 1))
        diag = minJump(height, x + 1, y + 1) +
           Math.abs(height[x][y] - height[x + 1][y + 1]);

    // Find minimum jumps if we go through down
    var down = 1000000000;
    if (isSafe(x + 1, y))
        down = minJump(height, x + 1, y) +
             Math.abs(height[x][y] - height[x + 1][y]);

    // Find minimum jumps if we go through right
    var right = 1000000000;
    if (isSafe(x, y + 1))
        right = minJump(height, x, y + 1) +
              Math.abs(height[x][y] - height[x][y + 1]);

    // return minimum jumps
    return Math.min(down, Math.min(right, diag));
}

/* Driver program to test above functions */
var height = [ [ 5, 4, 2 ],
                   [ 9, 2, 1 ],
                   [ 2, 5, 9 ],
                   [ 1, 3, 11 ] ];
document.write( minJump(height, 0, 0));

// This code is contributed by rutvik_56.
</script>
```

**输出:**

```
12
```

**时间复杂度:** (R*C)

**辅助空间:** O(1)