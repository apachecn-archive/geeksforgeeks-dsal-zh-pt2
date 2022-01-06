# 计算网格中给定方向上可能的移动

> 原文:[https://www . geeksforgeeks . org/count-网格中给定方向的可能移动数/](https://www.geeksforgeeks.org/count-possible-moves-in-the-given-direction-in-a-grid/)

给定网格 **N x M** 大小和初始位置 **(X，Y)** 以及一系列 **K** 移动。
每一步包含 2 个整数 **Dx** 和 **Dy** 。
单次移动包括以下操作，也可以尽可能多次执行:

> **X = X+Dx****Y = Y+Dy**。

任务是计算执行的移动次数。
**注意**在每个时间点，当前位置必须在网格内。
**示例:**

> **输入:** N = 4，M = 5，X = 1，Y = 1，k[] = {{1，1}，{1，1}，{0，-2}}
> **输出:**4
> **(X，Y)** 的值如下:
> 移步 1: (1，1) - > (2，2) - > (3，3) - > (4，4)即 3 步【T9 5)哪一个超出了网格的界限
> 移动 3 中的步骤:(4，4)-(T22)【4，2】即单次移动和(4，0)将超出界限，因此不可能再移动。
> 总移动量= 3 + 1 = 4
> **输入:** N = 10，M = 10，X = 3，Y = 3，k[] = {{1，1}，{-1，-1}}
> **输出:** 16

**逼近:**可以观察到我们可以独立处理 **X** 和 **Y** ，合并为当前移动步数=最少(步数用 **X** ，步数用 **Y** )。用 **X** 求步数，我们可以用 **Dx** 的符号知道我们正在接近哪个终点，并求出到那个终点的距离，速度为 **Dx** ，我们可以求出它要走的步数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#define int long long
using namespace std;

// Function to return the count of
// possible steps in a single direction
int steps(int cur, int x, int n)
{

    // It can cover infinite steps
    if (x == 0)
        return INT_MAX;

    // We are approaching towards X = N
    if (x > 0)
        return abs((n - cur) / x);

    // We are approaching towards X = 1
    else
        return abs((cur - 1) / x);
}

// Function to return the count of steps
int countSteps(int curx, int cury, int n, int m,
               vector<pair<int, int> > moves)
{
    int count = 0;
    int k = moves.size();
    for (int i = 0; i < k; i++) {
        int x = moves[i].first;
        int y = moves[i].second;

        // Take the minimum of both moves independently
        int stepct
            = min(steps(curx, x, n), steps(cury, y, m));

        // Update count and current positions
        count += stepct;
        curx += stepct * x;
        cury += stepct * y;
    }
    return count;
}

// Driver code
main()
{
    int n = 4, m = 5, x = 1, y = 1;
    vector<pair<int, int> > moves = { { 1, 1 },
                                      { 1, 1 },
                                      { 0, -2 } };
    int k = moves.size();
    cout << countSteps(x, y, n, m, moves);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the count of
    // possible steps in a single direction
    static int steps(int cur, int x, int n)
    {

        // It can cover infinite steps
        if (x == 0)
            return Integer.MAX_VALUE;

        // We are approaching towards X = N
        if (x > 0)
            return Math.abs((n - cur) / x);

        // We are approaching towards X = 1
        else
            return Math.abs((cur - 1) / x);
    }

    // Function to return the count of steps
    static int countSteps(int curx, int cury,
                             int n, int m,
                             int[][] moves)
    {
        int count = 0;
        int k = moves.length;
        for (int i = 0; i < k; i++)
        {
            int x = moves[i][0];
            int y = moves[i][1];

            // Take the minimum of 
            // both moves independently
            int stepct = Math.min(steps(curx, x, n),
                                  steps(cury, y, m));

            // Update count and current positions
            count += stepct;
            curx += stepct * x;
            cury += stepct * y;
        }
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4, m = 5, x = 1, y = 1;
        int[][] moves = { { 1, 1 }, { 1, 1 },
                          { 0, -2 } };

        System.out.print(countSteps(x, y, n, m, moves));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# possible steps in a single direction
def steps(cur, x, n):

    # It can cover infinite steps
    if x == 0:
        return float('inf')

    # We are approaching towards X = N
    elif x > 0:
        return abs((n - cur) // x)

    # We are approaching towards X = 1
    else:
        return abs(int((cur - 1) / x))

# Function to return the count of steps
def countSteps(curx, cury, n, m, moves):

    count = 0
    k = len(moves)
    for i in range(0, k):
        x = moves[i][0]
        y = moves[i][1]

        # Take the minimum of both moves
        # independently
        stepct = min(steps(curx, x, n),
                     steps(cury, y, m))

        # Update count and current positions
        count += stepct
        curx += stepct * x
        cury += stepct * y

    return count

# Driver code
if __name__ == "__main__":

    n, m, x, y = 4, 5, 1, 1
    moves = [[1, 1], [1, 1], [0, -2]]

    print(countSteps(x, y, n, m, moves))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the count of
    // possible steps in a single direction
    static int steps(int cur, int x, int n)
    {

        // It can cover infinite steps
        if (x == 0)
            return int.MaxValue;

        // We are approaching towards X = N
        if (x > 0)
            return Math.Abs((n - cur) / x);

        // We are approaching towards X = 1
        else
            return Math.Abs((cur - 1) / x);
    }

    // Function to return the count of steps
    static int countSteps(int curx, int cury,
                          int n, int m,
                          int[,] moves)
    {
        int count = 0;
        int k = moves.GetLength(0);
        for (int i = 0; i < k; i++)
        {
            int x = moves[i, 0];
            int y = moves[i, 1];

            // Take the minimum of
            // both moves independently
            int stepct = Math.Min(steps(curx, x, n),
                                  steps(cury, y, m));

            // Update count and current positions
            count += stepct;
            curx += stepct * x;
            cury += stepct * y;
        }
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 4, m = 5, x = 1, y = 1;
        int[,] moves = { { 1, 1 }, { 1, 1 },
                         { 0, -2 } };

        Console.Write(countSteps(x, y, n, m, moves));
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the above approach

// Function to return the count of
// possible steps in a single direction
function steps($cur, $x, $n)
{

    // It can cover infinite steps
    if ($x == 0)
        return PHP_INT_MAX;

    // We are approaching towards X = N
    if ($x > 0)
        return floor(abs(($n - $cur) / $x));

    // We are approaching towards X = 1
    else
        return floor(abs(($cur - 1) / $x));
}

// Function to return the count of steps
function countSteps($curx, $cury, $n, $m, $moves)
{
    $count = 0;
    $k = sizeof($moves);
    for ($i = 0; $i < $k; $i++)
    {
        $x = $moves[$i][0];
        $y = $moves[$i][1];

        // Take the minimum of both moves independently
        $stepct = min(steps($curx, $x, $n), steps($cury, $y, $m));

        // Update count and current positions
        $count += $stepct;
        $curx += $stepct * $x;
        $cury += $stepct * $y;
    }
    return $count;
}

    // Driver code
    $n = 4 ;
    $m = 5 ;
    $x = 1 ;
    $y = 1 ;
    $moves = array( array( 1, 1 ),
                        array( 1, 1 ),
                        array( 0, -2 ) );
    $k = sizeof($moves);

    echo countSteps($x, $y, $n, $m, $moves);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

    // Function to return the count of
    // possible steps in a single direction
    function steps(cur, x, n)
    {

        // It can cover infinite steps
        if (x == 0)
            return Number.MAX_VALUE;

        // We are approaching towards X = N
        if (x > 0)
            return Math.abs((n - cur) / x);

        // We are approaching towards X = 1
        else
            return Math.abs((cur - 1) / x);
    }

    // Function to return the count of steps
    function countSteps(curx, cury, n, m, moves)
    {
        let count = 0;
        let k = moves.length;
        for (let i = 0; i < k; i++)
        {
            let x = moves[i][0];
            let y = moves[i][1];

            // Take the minimum of 
            // both moves independently
            let stepct = Math.min(steps(curx, x, n),
                                  steps(cury, y, m));

            // Update count and current positions
            count += stepct;
            curx += stepct * x;
            cury += stepct * y;
        }
        return Math.floor(count);
    }

// driver program

        let n = 4, m = 5, x = 1, y = 1;
        let moves = [[ 1, 1 ], [ 1, 1 ],
                          [ 0, -2 ]];

        document.write(countSteps(x, y, n, m, moves));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N)