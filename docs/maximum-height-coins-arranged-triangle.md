# 硬币排列成三角形时的最大高度

> 原文:[https://www . geesforgeks . org/最大高度-硬币-排列-三角形/](https://www.geeksforgeeks.org/maximum-height-coins-arranged-triangle/)

我们有 N 个硬币需要以三角形的形式排列，即第一排有 1 个硬币，第二排有 2 个硬币，以此类推，我们需要告诉我们使用这 N 个硬币可以达到的最大高度。
示例:

```
Input : N = 7
Output : 3
Maximum height will be 3, putting 1, 2 and
then 3 coins. It is not possible to use 1 
coin left.

Input : N = 12
Output : 4
Maximum height will be 4, putting 1, 2, 3 and 
4 coins, it is not possible to make height as 5, 
because that will require 15 coins.
```

这个问题可以通过找到三角形的高度和硬币数量之间的关系来解决。假设最大高度是 H，那么硬币的总和应该小于 N，

```
Sum of coins for height H <= N
            H*(H + 1)/2  <= N
        H*H + H – 2*N <= 0
Now by Quadratic formula 
(ignoring negative root)

Maximum H can be (-1 + √(1 + 8N)) / 2 

Now we just need to find the square root of (1 + 8N) for
which we can use Babylonian method of finding square root
```

以下代码基于上述概念
实现

## 卡片打印处理机（Card Print Processor 的缩写）

```
//  C++ program to find maximum height of arranged
// coin triangle
#include <bits/stdc++.h>
using namespace std;

/* Returns the square root of n. Note that the function */
float squareRoot(float n)
{
    /* We are using n itself as initial approximation
      This can definitely be improved */
    float x = n;
    float y = 1;

    float e = 0.000001; /* e decides the accuracy level*/
    while (x - y > e)
    {
        x = (x + y) / 2;
        y = n/x;
    }
    return x;
}

//  Method to find maximum height of arrangement of coins
int findMaximumHeight(int N)
{
    //  calculating portion inside the square root
    int n = 1 + 8*N;
    int maxH = (-1 + squareRoot(n)) / 2;
    return maxH;
}

//  Driver code to test above method
int main()
{
    int N = 12;
    cout << findMaximumHeight(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum height
// of arranged coin triangle
class GFG
{

    /* Returns the square root of n.
    Note that the function */
    static float squareRoot(float n)
    {

        /* We are using n itself as
        initial approximation.This
        can definitely be improved */
        float x = n;
        float y = 1;

        // e decides the accuracy level
        float e = 0.000001f;
        while (x - y > e)
        {
            x = (x + y) / 2;
            y = n / x;
        }

        return x;
    }

    // Method to find maximum height
    // of arrangement of coins
    static int findMaximumHeight(int N)
    {

        // calculating portion inside
        // the square root
        int n = 1 + 8*N;
        int maxH = (int)(-1 + squareRoot(n)) / 2;

        return maxH;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 12;

        System.out.print(findMaximumHeight(N));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find
# maximum height of arranged
# coin triangle

# Returns the square root of n.
# Note that the function
def squareRoot(n):

    # We are using n itself as
        # initial approximation
    # This can definitely be improved
    x = n
    y = 1

    e = 0.000001  # e decides the accuracy level
    while (x - y > e):
        x = (x + y) / 2
        y = n/x

    return x

# Method to find maximum height
# of arrangement of coins
def findMaximumHeight(N):

    # calculating portion inside the square root
    n = 1 + 8*N
    maxH = (-1 + squareRoot(n)) / 2
    return int(maxH)

# Driver code to test above method
N = 12
print(findMaximumHeight(N))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find maximum height
// of arranged coin triangle
using System;

class GFG
{
    /* Returns the square root of n.
    Note that the function */
    static float squareRoot(float n)
    {
        /* We are using n itself as
        initial approximation.This
        can definitely be improved */
        float x = n;
        float y = 1;

        // e decides the accuracy level
        float e = 0.000001f;
        while (x - y > e)
        {
            x = (x + y) / 2;
            y = n / x;
        }
        return x;
    }

    static int findMaximumHeight(int N)
    {

        // calculating portion inside
        // the square root
        int n = 1 + 8*N;
        int maxH = (int)(-1 + squareRoot(n)) / 2;

        return maxH;
    }

    /* program to test above function */
    public static void Main()
    {
        int N = 12;
        Console.Write(findMaximumHeight(N));
    }
}

// This code is contributed by _omg
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum height
// of arranged coin triangle

/* Returns the square root of n. Note
that the function */
function squareRoot( $n)
{
    /* We are using n itself as initial
    approximation This can definitely
    be improved */
    $x = $n;
    $y = 1;

    /* e decides the accuracy level*/
    $e = 0.000001;
    while ($x - $y > $e)
    {
        $x = ($x + $y) / 2;
        $y = $n/$x;
    }
    return $x;
}

// Method to find maximum height of
// arrangement of coins
function findMaximumHeight( $N)
{

    // calculating portion inside
    // the square root
    $n = 1 + 8 * $N;
    $maxH = (-1 + squareRoot($n)) / 2;
    return floor($maxH);
}

// Driver code to test above method
$N = 12;
echo findMaximumHeight($N) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find maximum height
// of arranged coin triangle

    /* Returns the square root of n.
    Note that the function */
    function squareRoot(n)
    {

        /* We are using n itself as
        initial approximation.This
        can definitely be improved */
        let x = n;
        let y = 1;

        // e decides the accuracy level
        let e = 0.000001;
        while (x - y > e)
        {
            x = (x + y) / 2;
            y = n / x;
        }

        return x;
    }

    // Method to find maximum height
    // of arrangement of coins
    function findMaximumHeight(N)
    {

        // calculating portion inside
        // the square root
        let n = 1 + 8*N;
        let maxH = (-1 + squareRoot(n)) / 2;

        return Math.round(maxH);
    }

// Driver Code
let N = 12;
document.write(findMaximumHeight(N));

 // This code is contributed by avijitmondal1998.
</script>
```

**输出:**

```
4
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。