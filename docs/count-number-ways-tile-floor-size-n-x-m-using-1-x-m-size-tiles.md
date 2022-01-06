# 统计使用 1×m 尺寸瓷砖铺设 n×m 尺寸地板的方法数量

> 原文:[https://www . geesforgeks . org/count-number-way-tile-floor-size-n-x-m-using-1-x-m-size-tiles/](https://www.geeksforgeeks.org/count-number-ways-tile-floor-size-n-x-m-using-1-x-m-size-tiles/)

给定大小为 n x m 的地板和大小为 1 x m 的瓷砖，问题是计算使用 1 x m 瓷砖给给定地板贴瓷砖的方法的数量。瓷砖可以水平放置，也可以垂直放置。
n 和 m 都是正整数，2<= m
例:

```
Input : n = 2, m = 3
Output : 1
Only one combination to place 
two tiles of size 1 x 3 horizontally
on the floor of size 2 x 3\. 

Input :  n = 4, m = 4
Output : 2
1st combination:
All tiles are placed horizontally
2nd combination:
All tiles are placed vertically.
```

这个问题主要是对[平铺问题](https://www.geeksforgeeks.org/tiling-problem/)的一种更一般化的处理方法。
**方法:**对于给定的 n 和 m 值，可以从以下关系式中获得铺地板的方式数。

```
            |  1, 1 < = n < m
 count(n) = |  2, n = m
            | count(n-1) + count(n-m), m < n

```

## C++

```
// C++ implementation to count number of ways to
// tile a floor of size n x m using 1 x m tiles
#include <bits/stdc++.h>

using namespace std;

// function to count the total number of ways
int countWays(int n, int m)
{

    // table to store values
    // of subproblems
    int count[n + 1];
    count[0] = 0;

    // Fill the table upto value n
    for (int i = 1; i <= n; i++) {

        // recurrence relation
        if (i > m)
            count[i] = count[i - 1] + count[i - m];

        // base cases and for i = m = 1
        else if (i < m || i == 1)
            count[i] = 1;

        // i = = m
        else
            count[i] = 2;
    }

    // required number of ways
    return count[n];
}

// Driver program to test above
int main()
{
    int n = 7, m = 4;
    cout << "Number of ways = "
         << countWays(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count number
// of ways to tile a floor of size
// n x m using 1 x m tiles
import java.io.*;

class GFG {

    // function to count the total number of ways
    static int countWays(int n, int m)
    {
        // table to store values
        // of subproblems
        int count[] = new int[n + 1];
        count[0] = 0;

        // Fill the table upto value n
        int i;
        for (i = 1; i <= n; i++) {

            // recurrence relation
            if (i > m)
                count[i] = count[i - 1] + count[i - m];

            // base cases
            else if (i < m || i == 1)
                count[i] = 1;

            // i = = m
            else
                count[i] = 2;
        }

        // required number of ways
        return count[n];
    }

    // Driver program
    public static void main(String[] args)
    {
        int n = 7;
        int m = 4;
        System.out.println("Number of ways = "
                           + countWays(n, m));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python implementation to
# count number of ways to
# tile a floor of size n x m
# using 1 x m tiles

def countWays(n, m):

    # table to store values
    # of subproblems
    count =[]
    for i in range(n + 2):
        count.append(0)
    count[0] = 0

    # Fill the table upto value n
    for i in range(1, n + 1):

        # recurrence relation
        if (i > m):
            count[i] = count[i-1] + count[i-m]

        # base cases
        elif (i < m or i == 1):
            count[i] = 1

        # i = = m
        else:
            count[i] = 2

    # required number of ways
    return count[n]

# Driver code

n = 7
m = 4

print("Number of ways = ", countWays(n, m))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# implementation to count number
// of ways to tile a floor of size
// n x m using 1 x m tiles
using System;

class GFG {

    // function to count the total
    // number of ways
    static int countWays(int n, int m)
    {

        // table to store values
        // of subproblems
        int[] count = new int[n + 1];
        count[0] = 0;

        // Fill the table upto value n
        int i;
        for (i = 1; i <= n; i++) {

            // recurrence relation
            if (i > m)
                count[i] = count[i - 1]
                           + count[i - m];

            // base cases and i = m = 1
            else if (i < m || i == 1)
                count[i] = 1;

            // i = = m
            else
                count[i] = 2;
        }

        // required number of ways
        return count[n];
    }

    // Driver program
    public static void Main()
    {
        int n = 7;
        int m = 4;

        Console.Write("Number of ways = "
                      + countWays(n, m));
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count
// number of ways to tile a
// floor of size n x m using
// 1 x m tiles

// function to count the
// total number of ways
function countWays($n, $m)
{

    // table to store values
    // of subproblems
    $count[0] = 0;

    // Fill the table
    // upto value n
    for ($i = 1; $i <= $n; $i++)
    {

        // recurrence relation
        if ($i > $m)
            $count[$i] = $count[$i - 1] +
                         $count[$i - $m];

        // base cases
        else if ($i < $m or $i == 1)
            $count[$i] = 1;

        // i = = m
        else
            $count[$i] = 2;
    }

    // required number of ways
    return $count[$n];
}

    // Driver Code
    $n = 7;
    $m = 4;
    echo "Number of ways = ", countWays($n, $m);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to count number
    // of ways to tile a floor of size
    // n x m using 1 x m tiles

    // function to count the total
    // number of ways
    function countWays(n, m)
    {

        // table to store values
        // of subproblems
        let count = new Array(n + 1);
        count[0] = 0;

        // Fill the table upto value n
        let i;
        for (i = 1; i <= n; i++) {

            // recurrence relation
            if (i > m)
                count[i] = count[i - 1] + count[i - m];

            // base cases and i = m = 1
            else if (i < m || i == 1)
                count[i] = 1;

            // i = = m
            else
                count[i] = 2;
        }

        // required number of ways
        return count[n];
    }

    let n = 7;
    let m = 4;

    document.write("Number of ways = " + countWays(n, m));

// This code is contributed by rameshtravel07.
</script>
```

输出:

```
Number of ways = 5
```

时间复杂度:O(n)
辅助空间:O(n)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。