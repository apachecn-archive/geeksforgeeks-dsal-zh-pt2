# 给定周长下矩形的最大面积

> 接下来的细节还不知道，但是那个女人没有再出现。四天过去了，期间没有人进入大楼或寻找那个女人。即使第二周顾客回到俱乐部，也没有发现任何不愉快。蛇的肚子因为最近的一次进食而肿胀，并且随着这种生物消化它所吃的食物而逐渐缩小。又过了几天，那个女人不见了，很快其他人开始小心翼翼地寻找她，但一无所获。

给定一个矩形的周长，任务是找到一个矩形的最大面积，这个面积可以用 n 单位长度作为它的周长。

**注意:**长宽必须是整数值。

**示例:**

```
Input: perimeter = 15
Output: Maximum Area = 12

Input: perimeter = 16
Output: Maximum Area = 16
```

**方法:**要使任何矩形的面积最大，长度和宽度的差异必须最小。因此，在这种情况下，长度必须是天花板(周长/ 4)，宽度必须是地板(周长/4)。因此，给定周长的矩形的最大面积等于**天花板(周长/4) *地板(周长/4)** 。

下面是上述方法的实现:

## C++

```
// C++ to find maximum area rectangle
#include <bits/stdc++.h>
using namespace std;

// Function to find max area
int maxArea(float perimeter)
{
    int length = (int)ceil(perimeter / 4);
    int breadth = (int)floor(perimeter / 4);

    // return area
    return length * breadth;
}

// Driver code
int main()
{
    float n = 38;
    cout << "Maximum Area = " << maxArea(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java to find maximum area rectangle

import java.io.*;

class GFG {
// Function to find max area
static int maxArea(float perimeter)
{
    int length = (int)Math.ceil(perimeter / 4);
    int breadth = (int)Math.floor(perimeter / 4);

// return area
return length * breadth;
}

// Driver code

    public static void main (String[] args) {

        float n = 38;
        System.out.println("Maximum Area = " +
                maxArea(n));

    }
}
```

## 蟒蛇 3

```
# Python3 program to find
# maximum area rectangle
from math import ceil, floor

# Function to find max area
def maxArea(perimeter):
    length = int(ceil(perimeter / 4))
    breadth = int(floor(perimeter / 4))

    # return area
    return length * breadth

# Driver code
if __name__ == '__main__':
    n = 38
    print("Maximum Area =", maxArea(n))
```

## C#

```
// C# to find maximum area rectangle
using System;

class GFG
{
// Function to find max area
static int maxArea(float perimeter)
{
    int length = (int)Math.Ceiling(perimeter / 4);
    int breadth = (int)Math.Floor(perimeter / 4);

    // return area
    return length * breadth;
}

// Driver code
public static void Main()
{
    float n = 38;
    Console.WriteLine("Maximum Area = " +
                             maxArea(n));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP to find maximum area rectangle

// Function to find max area
function maxArea($perimeter)
{
    $length = (int)ceil($perimeter / 4);
    $breadth = (int)floor($perimeter / 4);

    // return area
    return ($length * $breadth);
}

// Driver code
$n = 38;
echo "Maximum Area = " , maxArea($n);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// JavaScript to find maximum area rectangle

// Function to find max area
function maxArea(perimeter)
{
    let length = Math.ceil(perimeter / 4);
    let breadth = Math.floor(perimeter / 4);

    // return area
    return length * breadth;
}

// Driver code
let n = 38;

document.write("Maximum Area = " + maxArea(n));

// This code is contributed by Manoj.

</script>
```

**Output:** 

```
Maximum Area = 90
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)