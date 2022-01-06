# 一个范围内两个数的公倍数的计数

> 原文:[https://www . geesforgeks . org/范围内两个数字的公共倍数计数/](https://www.geeksforgeeks.org/count-of-common-multiples-of-two-numbers-in-a-range/)

给定从左到右的范围，每个 Xth 瓷砖都被涂成黑色，而每个 Yth 瓷砖在从左到右的范围内都被涂成白色。如果一个瓷砖被涂成白色和黑色，那么它被认为是被涂成灰色的。任务是找到从 L 到 R(包括两者)范围内的灰色瓷砖数量。
**例:**

```
Input: X = 2, Y = 3, L = 6, R = 18
Output: 3
The grey coloured tiles are numbered 6, 12, 18

Input: X = 1, Y = 4, L = 5, R = 10
Output: 1
The only grey coloured tile is 8.
```

**逼近:**由于 X 的每倍数都是黑色，Y 的每倍数都是白色。任何 X 和 Y 的倍数的瓷砖都是灰色的。可被 X 和 Y 整除的项是可被 X 和 Y 的 lcm 整除的项。
Lcm 可以用下面的公式求出:

```
lcm = (x*y) / gcd(x, y)
```

可以使用[欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)以对数时间计算 GCD。L 到 R 范围内 lcm 的倍数可以通过一个常见的技巧找到:

```
count(L, R) = count(R) - count(L-1)
```

可被 K 整除的小于 N 的项数为:

```
floor(N/K)
```

下面是查找灰瓦数量的实现:

## C++

```
// C++ implementation to find the number of
// grey tiles
#include <bits/stdc++.h>
using namespace std;

// Function to count the numbe ro fgrey tiles
int findTileCount(int x, int y, int l, int r)
{
    int lcm = (x * y) / __gcd(x, y);

    // Number multiple of lcm less than L
    int countl = (l - 1) / lcm;

    // Number of multiples of lcm less than R+1
    int countr = r / lcm;
    return countr - countl;
}

// Driver code
int main()
{
    int x = 2, y = 3, l = 6, r = 18;
    cout << findTileCount(x, y, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  implementation to find the
// number of grey tiles

import java.io.*;

class GFG {
    // Function to count the number
// of grey tiles
static int findTileCount(int x, int y,
                         int l, int r)
{
    int lcm = (x * y) / __gcd(x, y);

    // Number multiple of lcm less than L
    int countl = (l - 1) / lcm;

    // Number of multiples of
    // lcm less than R+1
    int countr = r / lcm;
    return countr - countl;
}

static int __gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0)
    return b;
    if (b == 0)
    return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);

    return __gcd(a, b - a);
}

// Driver code

    public static void main (String[] args) {

    int x = 2, y = 3, l = 6, r = 18;
        System.out.println(findTileCount(x, y, l, r));
}
}

// This code is contributed ajit
```

## 蟒蛇 3

```
# Python3 implementation to find the number of
# grey tiles

# from math lib import gcd method
from math import gcd

# Function to count the numbe of grey tiles
def findTileCount(x, y, l, r) :

    lcm = (x * y) // gcd(x, y)

    # Number multiple of lcm less than L
    count1 = (l - 1) // lcm

    # Number of multiples of lcm less than R+1
    countr = r // lcm

    return countr - count1

# Driver code
if __name__ == "__main__" :

    x, y, l, r = 2, 3, 6, 18
    print(findTileCount(x, y, l, r))

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# implementation to find the
// number of grey tiles
using System;

class GFG
{

// Function to count the number
// of grey tiles
static int findTileCount(int x, int y,
                         int l, int r)
{
    int lcm = (x * y) / __gcd(x, y);

    // Number multiple of lcm less than L
    int countl = (l - 1) / lcm;

    // Number of multiples of
    // lcm less than R+1
    int countr = r / lcm;
    return countr - countl;
}

static int __gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0)
    return b;
    if (b == 0)
    return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);

    return __gcd(a, b - a);
}

// Driver code
public static void Main()
{
    int x = 2, y = 3, l = 6, r = 18;
    Console.Write(findTileCount(x, y, l, r));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the
// number of grey tiles

// Function to count the number
// of grey tiles
function findTileCount($x, $y, $l, $r)
{
    $lcm = (int)(($x * $y) / __gcd($x, $y));

    // Number multiple of lcm less than L
    $countl = (int)(($l - 1) / $lcm);

    // Number of multiples of
    // lcm less than R+1
    $countr = (int)($r / $lcm);
    return $countr - $countl;
}

function __gcd($a, $b)
{

    // Everything divides 0
    if ($a == 0)
    return $b;
    if ($b == 0)
    return $a;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return __gcd($a - $b, $b);

    return __gcd($a, $b - $a);
}

// Driver code
$x = 2; $y = 3; $l = 6; $r = 18;
echo findTileCount($x, $y, $l, $r);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// number of grey tiles

// Function to count the number
// of grey tiles
function findTileCount(x,y,l,r)
{
    lcm = parseInt((x * y) / __gcd(x, y));

    // Number multiple of lcm less than L
    countl = parseInt((l - 1) / lcm);

    // Number of multiples of
    // lcm less than R+1
    countr = parseInt(r / lcm);
    return countr - countl;
}

function __gcd(a, b)
{

    // Everything divides 0
    if (a == 0)
    return b;
    if (b == 0)
    return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);

    return __gcd(a, b - a);
}

// Driver code
let x = 2;
let y = 3;
let l = 6;
let r = 18;
document.write(findTileCount(x, y, l, r));

// This code is contributed by bobby

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(log(x*y))