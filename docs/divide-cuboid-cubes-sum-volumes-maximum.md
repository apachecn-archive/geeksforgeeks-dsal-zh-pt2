# 将长方体分成立方体，体积之和最大

> 原文:[https://www . geesforgeks . org/divide-长方体-立方体-总和-体积-最大值/](https://www.geeksforgeeks.org/divide-cuboid-cubes-sum-volumes-maximum/)

给定长方体的**长度**、**宽度**、**高度**。任务是将给定的立方体分成最小数量的立方体，使得所有立方体的大小相同，并且立方体的体积总和最大。
示例:

```
Input : l = 2, b = 4, h = 6
Output : 2 6
A cuboid of length 2, breadth 4 and 
height 6 can be divided into 6 cube 
of side equal to 2.
Volume of cubes = 6*(2*2*2) = 6*8 = 48.
Volume of cuboid = 2*4*6 = 48.

Input : 1 2 3
Output : 1 6
```

首先，我们不允许浪费长方体的体积，因为我们需要最大的体积总和。所以，每一面都应该在所有立方体中完全分开。因为立方体的三条边都相等，所以长方体的每条边都需要被同一个数整除，比如 x，它就是立方体的边。所以，我们必须最大化这个 x，它将划分给定的长度，宽度和高度。这个 x 只有在它是给定长度、宽度和高度的最大公约数时才是最大的。所以，立方体的长度将是长宽高的 GCD。
现在计算立方体的个数，我们知道长方体的总体积，就可以求出一个立方体的体积(因为边已经计算好了)。所以，立方体的总数等于(长方体的体积)/(立方体的体积)即(l * b * h)/(x * x * x)。
以下是本办法的实施情况:

## C++

```
// CPP program to find optimal way to break
// cuboid into cubes.
#include <bits/stdc++.h>
using namespace std;

// Print the maximum side and no of cube.
void maximizecube(int l, int b, int h)
{
    // GCD to find side.
    int side = __gcd(l, __gcd(b, h));

    // dividing to find number of cubes.
    int num = l / side;
    num = (num * b / side);
    num = (num * h / side);

    cout << side << " " << num << endl;
}

// Driver code
int main()
{
    int l = 2, b = 4, h = 6;

    maximizecube(l, b, h);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Divide cuboid into cubes
// such that sum of volumes is maximum
import java.util.*;

class GFG {

    static int gcd(int m, int n)
    {
        if(n == 0)
            return m;
        else if(n > m)
            return gcd(n,m);
        else
            return gcd(n, m % n);
    }

    // Print the maximum side and no
    //     of cube.
    static void maximizecube(int l, int b,
                                    int h)
    {
        // GCD to find side.
        int side = gcd(l, gcd(b, h));

        // dividing to find number of cubes.
        int num = l / side;
        num = (num * b / side);
        num = (num * h / side);

       System.out.println( side + " " + num);
    }

    /* Driver program  */
    public static void main(String[] args)
    {
         int l = 2, b = 4, h = 6;
         maximizecube(l, b, h);
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 code to find optimal way to break
# cuboid into cubes.
from fractions import gcd

# Print the maximum side and no of cube.
def maximizecube( l , b , h ):

    # GCD to find side.
    side = gcd(l, gcd(b, h))

    # dividing to find number of cubes.
    num = int(l / side)
    num = int(num * b / side)
    num = int(num * h / side)

    print(side, num)

# Driver code
l = 2
b = 4
h = 6

maximizecube(l, b, h)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# Code for Divide cuboid into cubes
// such that sum of volumes is maximum
using System;

class GFG {

    static int gcd(int m, int n)
    {
        if(n == 0)
            return m;
        else if(n > m)
            return gcd(n,m);
        else
            return gcd(n, m % n);
    }

    // Print the maximum side and no
    // of cube.
    static void maximizecube(int l, int b,
                                    int h)
    {
        // GCD to find side.
        int side = gcd(l, gcd(b, h));

        // dividing to find number of cubes.
        int num = l / side;
        num = (num * b / side);
        num = (num * h / side);

    Console.WriteLine( side + " " + num);
    }

    /* Driver program */
    public static void Main()
    {
        int l = 2, b = 4, h = 6;
        maximizecube(l, b, h);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find optimal way
// to break cuboid into cubes.

// Recursive function to
// return gcd of a and b
function __gcd($a, $b)
{

    // Everything divides 0
    if($a == 0 or $b == 0)
        return 0 ;

    // base case
    if($a == $b)
        return $a ;

    // a is greater
    if($a > $b)
        return __gcd($a - $b , $b ) ;

    return __gcd($a , $b - $a) ;
}

// Print the maximum side and no of cube.
function maximizecube($l, $b, $h)
{

    // GCD to find side.
    $side = __gcd($l, __gcd($b, $h));

    // dividing to find number of cubes.
    $num = $l / $side;
    $num = ($num * $b / $side);
    $num = ($num * $h / $side);

    echo $side , " " , $num ;
}

    // Driver code
    $l = 2;
    $b = 4;
    $h = 6;
    maximizecube($l, $b, $h);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program for Divide cuboid into cubes
// such that sum of volumes is maximum
    function gcd(m, n)
    {
        if(n == 0)
            return m;
        else if(n > m)
            return gcd(n,m);
        else
            return gcd(n, m % n);
    }

    // Print the maximum side and no
    //     of cube.
    function maximizecube(l, b, h)
    {

        // GCD to find side.
        let side = gcd(l, gcd(b, h));

        // dividing to find number of cubes.
        let num = l / side;
        num = (num * b / side);
        num = (num * h / side);

       document.write( side + " " + num);
    }

// Driver code      
        let l = 2, b = 4, h = 6;
         maximizecube(l, b, h);

         // This code is contributed by sanjoy_62.
</script>
```

输出:

```
2 6
```