# 可被 C 整除的最大正整数，在【A，B】

范围内

> 原文:[https://www . geesforgeks . org/max-正整数可被 c 整除且在范围内-a-b/](https://www.geeksforgeeks.org/maximum-positive-integer-divisible-by-c-and-is-in-the-range-a-b/)

给定三个正整数 A、B 和 c。任务是找到最大整数 X > 0，这样:

1.  **X % C** = 0 且
2.  x 必须属于范围[A，B]

如果不存在这样的数字，即 X，打印 **-1** 。

**示例:**

```
Input: A = 2, B = 4, C = 2
Output: 4
B is itself divisible by C.

Input: A = 5, B = 10, C = 4
Output: 8 
B is not divisible by C. 
So maximum multiple of 4(C) smaller than 10(B) is 8 
```

**进场:**

*   如果 B 是 C 的倍数，那么 B 就是所需的数字。
*   否则得到 C 的最大倍数，只比 B 小，这是必需的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to return the required number
int getMaxNum(int a, int b, int c)
{

    // If b % c = 0 then b is the
    // required number
    if (b % c == 0)
        return b;

    // Else get the maximum multiple of
    // c smaller than b
    int x = ((b / c) * c);

    if (x >= a && x <= b)
        return x;
    else
        return -1;
}

// Driver code
int main()
{
    int a = 2, b = 10, c = 3;
    cout << getMaxNum(a, b, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG
{

// Function to return the required number
static int getMaxNum(int a, int b, int c)
{

    // If b % c = 0 then b is the
    // required number
    if (b % c == 0)
        return b;

    // Else get the maximum multiple of
    // c smaller than b
    int x = ((b / c) * c);

    if (x >= a && x <= b)
        return x;
    else
        return -1;
}

// Driver code
public static void main (String[] args)
{
    int a = 2, b = 10, c = 3;
    System.out.println(getMaxNum(a, b, c));
}
}

// This Code is contributed by ajit..
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the required number
def getMaxNum(a, b, c):

    # If b % c = 0 then b is the
    # required number
    if (b % c == 0):
        return b

    # Else get the maximum multiple
    # of c smaller than b
    x = ((b //c) * c)

    if (x >= a and x <= b):
        return x
    else:
        return -1

# Driver code
a, b, c = 2, 10, 3
print(getMaxNum(a, b, c))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;
class GFG
{

// Function to return the required number
static int getMaxNum(int a, int b, int c)
{

    // If b % c = 0 then b is the
    // required number
    if (b % c == 0)
        return b;

    // Else get the maximum multiple of
    // c smaller than b
    int x = ((b / c) * c);

    if (x >= a && x <= b)
        return x;
    else
        return -1;
}

// Driver code
public static void Main ()
{
    int a = 2, b = 10, c = 3;
    Console.WriteLine(getMaxNum(a, b, c));
}
}

// This Code is contributed by Code_Mech..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
// Function to return the required number
function getMaxNum($a, $b, $c)
{

    // If b % c = 0 then b is the
    // required number
    if ($b % $c == 0)
        return $b;

    // Else get the maximum multiple
    // of c smaller than b
    $x = ((int)($b / $c) * $c);

    if ($x >= $a && $x <= $b)
        return $x;
    else
        return -1;
}

// Driver code
$a = 2; $b = 10; $c = 3;
echo(getMaxNum($a, $b, $c));

// This Code is contributed
// by Mukul Singh
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the required number
function getMaxNum(a, b, c)
{

    // If b % c = 0 then b is the
    // required number
    if (b % c == 0)
        return b;

    // Else get the maximum multiple of
    // c smaller than b
    var x = (parseInt(b / c) * c);

    if (x >= a && x <= b)
        return x;
    else
        return -1;
}

// Driver code
var a = 2, b = 10, c = 3;
document.write( getMaxNum(a, b, c));

</script>
```

**Output:** 

```
9
```