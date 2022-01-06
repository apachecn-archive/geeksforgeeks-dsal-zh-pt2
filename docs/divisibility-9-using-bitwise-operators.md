# 使用按位运算符

检查数字是否是 9 的倍数

> 原文:[https://www . geeksforgeeks . org/divisionity-9-使用按位运算符/](https://www.geeksforgeeks.org/divisibility-9-using-bitwise-operators/)

给定一个数字 n，写一个函数，如果 n 能被 9 整除，则返回 true，否则返回 false。检查 n 除以 9 的最简单方法是做 n%9。
另一种方法是对 n 的位数求和，如果位数之和是 9 的倍数，那么 n 就是 9 的倍数。
上述方法不是基于按位运算符的方法，需要使用%和/。
[按位运算符](https://www.geeksforgeeks.org/interesting-facts-bitwise-operators-c/)通常比模和除运算符更快。下面是一个基于按位运算符的方法，用于检查 9 的可除性。

## C++

```
// C++ program to check if a number
// is multiple of 9 using bitwise operators
#include <bits/stdc++.h>
using namespace std;

// Bitwise operator based function to check divisibility by 9
bool isDivBy9(int n)
{
    // Base cases
    if (n == 0 || n == 9)
        return true;
    if (n < 9)
        return false;

    // If n is greater than 9, then recur for [floor(n/9) - n%8]
    return isDivBy9((int)(n >> 3) - (int)(n & 7));
}

// Driver program to test above function
int main()
{
    // Let us print all multiples of 9 from 0 to 100
    // using above method
    for (int i = 0; i < 100; i++)
        if (isDivBy9(i))
            cout << i << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number
// is multiple of 9 using bitwise operators
import java.lang.*;

class GFG {

    // Bitwise operator based function
    // to check divisibility by 9
    static boolean isDivBy9(int n)
    {

        // Base cases
        if (n == 0 || n == 9)
            return true;
        if (n < 9)
            return false;

        // If n is greater than 9, then
        // recur for [floor(n/9) - n%8]
        return isDivBy9((int)(n >> 3) - (int)(n & 7));
    }

    // Driver code
    public static void main(String arg[])
    {

        // Let us print all multiples of 9 from
        // 0 to 100 using above method
        for (int i = 0; i < 100; i++)
            if (isDivBy9(i))
                System.out.print(i + " ");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Bitwise operator based
# function to check divisibility by 9

def isDivBy9(n):

    # Base cases
    if (n == 0 or n == 9):
        return True
    if (n < 9):
        return False

    # If n is greater than 9,
    # then recur for [floor(n / 9) - n % 8]
    return isDivBy9((int)(n>>3) - (int)(n&7))

# Driver code

# Let us print all multiples
# of 9 from 0 to 100
# using above method
for i in range(100):
    if (isDivBy9(i)):
        print(i, " ", end ="")

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to check if a number
// is multiple of 9 using bitwise operators
using System;

class GFG {

    // Bitwise operator based function
    // to check divisibility by 9
    static bool isDivBy9(int n)
    {
        // Base cases
        if (n == 0 || n == 9)
            return true;
        if (n < 9)
            return false;

        // If n is greater than 9, then
        // recur for [floor(n/9) - n%8]
        return isDivBy9((int)(n >> 3) - (int)(n & 7));
    }

    // Driver code
    public static void Main()
    {
        // Let us print all multiples of 9 from
        // 0 to 100 using above method
        for (int i = 0; i < 100; i++)
            if (isDivBy9(i))
                Console.Write(i + " ");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number
// is multiple of 9 using bitwise
// operators

// Bitwise operator based function
// to check divisibility by 9
function isDivBy9($n)
{

    // Base cases
    if ($n == 0 || $n == 9)
        return true;
    if ($n < 9)
        return false;

    // If n is greater than 9,
    // then recur for [floor(n/9) -
    // n%8]
    return isDivBy9(($n >> 3) -
                    ($n & 7));
}

    // Driver Code
    // Let us print all multiples
    // of 9 from 0 to 100
    // using above method
    for ($i = 0; $i < 100; $i++)
        if (isDivBy9($i))
            echo $i ," ";

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// javascript program to check if a number
// is multiple of 9 using bitwise operators

// Bitwise operator based function
// to check divisibility by 9
function isDivBy9(n)
{

    // Base cases
    if (n == 0 || n == 9)
        return true;
    if (n < 9)
        return false;

    // If n is greater than 9, then
    // recur for [floor(n/9) - n%8]
    return isDivBy9(parseInt(n >> 3) - parseInt(n & 7));
}

// Driver code

    // Let us print all multiples of 9 from
// 0 to 100 using above method
for (i = 0; i < 100; i++)
    if (isDivBy9(i))
        document.write(i + " ");

// This code is contributed by Princi Singh
</script>
```

输出:

```
0 9 18 27 36 45 54 63 72 81 90 99
```

**这是如何工作的？**
*n/9* 可以用下面的简单公式写成 *n/8* 。

```
n/9 = n/8 - n/72
```

因为我们需要使用按位运算符，所以我们使用*n>T22【3】T3 得到 *floor(n/8)* 的值，使用 *n & 7* 得到 *n%8* 的值。我们需要用*楼层(n/8)* 和 *n%8* 来写上面的表达式。
*n/8* 等于*“楼层(n/8)+(n % 8)/8”*。让我们用*楼层(n/8)* 和 *n%8* 来写上面的表达式*

```
n/9 = floor(n/8) + (n%8)/8 - [floor(n/8) + (n%8)/8]/9
n/9 = floor(n/8) - [floor(n/8) - 9(n%8)/8 + (n%8)/8]/9
n/9 = floor(n/8) - [floor(n/8) - n%8]/9
```

从上式可知，只有当表达式*floor(n/8)–【floor(n/8)–n % 8)/9*为整数时， *n* 才是 *9* 的倍数。只有子表达式*【楼层(n/8)–n % 8/9*为整数时，该表达式才能为整数。如果*【楼层(n/8)–n % 8】*是 *9* 的倍数，子表达式只能是整数。所以这个问题简化为一个更小的值，可以用按位运算符来写。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息