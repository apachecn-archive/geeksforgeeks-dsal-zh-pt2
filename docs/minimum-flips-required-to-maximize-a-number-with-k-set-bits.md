# 用 k 个设置位最大化一个数所需的最小翻转次数

> 原文:[https://www . geeksforgeeks . org/最小翻转-需要最大化带有 k 位集的数字/](https://www.geeksforgeeks.org/minimum-flips-required-to-maximize-a-number-with-k-set-bits/)

给定两个数字 n 和 k，我们需要通过翻转给定数字的位来找到最大化给定数字所需的最小翻转次数，这样得到的数字正好有 k 个设置位。
注意:K 必须小于 n 中的位数
**示例:**

```
Input : n = 14, k = 2
Output : Min Flips = 1
Explanation : 
Binary representation of 14 = 1110
Largest 4-digit Binary number with
2 set bit = 1100
Conversion from 1110 to 1100 
requires 1 flipping

Input : n = 145, k = 4
Output : Min Flips = 3
Explanation : 
Binary representation of 145 = 10010001
Largest 8-digit Binary number with 
4 set bit = 11110000
Conversion from 10010001 to 11110000 
requires 3 flipping
```

对于给定的数字 n 和 k，用 k-set 位找到可能的最大数字，并且具有与 n 完全相同的位数，如下所示:

*   size = log2(n) + 1 给出 n 的位数。
*   max = pow(2，k)–1 给出 k 位的最大可能数。
*   max = max <
*   (n 异或最大值)中的置位位数是我们需要的翻转数。

上述方法说明:

```
let n = 145 (10010001), k = 4

size = log2(n) + 1 = log2(145) + 1 
                   = 7 + 1 = 8 

max = pow(2, k) -1 = pow(2, 4) - 1 
                   = 16 - 1 = 15 (1111) 

max = max << (size - k) = 15 << (8 - 4) 
                        = 240 (11110000)

number of set bit in  =  no. of set bit in 
(n XOR max )              (145 ^ 240 ) 
                      = 3
```

## C++

```
// CPP for finding min flip
// for maximizing given n
#include <bits/stdc++.h>
using namespace std;

// function for finding set bit
int setBit(int xorValue)
{
    int count = 0;
    while (xorValue) {
        if (xorValue % 2)
            count++;

        xorValue /= 2;
    }

    // return count of set bit
    return count;
}

// function for finding min flip
int minFlip(int n, int k)
{  
    // number of bits in n
    int size = log2(n) + 1;

    // Find the largest number of
    // same size with k set bits
    int max = pow(2, k) - 1;   
    max = max << (size - k);

    // Count bit differences to find
    // required flipping.
    int xorValue = (n ^ max);
    return (setBit(xorValue));
}

// driver program
int main()
{
    int n = 27, k = 3;
    cout << "Min Flips = " << minFlip(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to find Minimum flips required
// to maximize a number with k set bits
import java.util.*;

class GFG {

    // function for finding set bit
    static int setBit(int xorValue)
    {
        int count = 0;
        while (xorValue >= 1) {
            if (xorValue % 2 == 1)
                count++;

            xorValue /= 2;
        }

        // return count of set bit
        return count;
    }

    // function for finding min flip
    static int minFlip(int n, int k)
    {  
        // number of bits in n
        int size = (int)(Math.log(n) /
                         Math.log(2)) + 1;

        // Find the largest number of
        // same size with k set bits
        int max = (int)Math.pow(2, k) - 1;   
        max = max << (size - k);

        // Count bit differences to find
        // required flipping.
        int xorValue = (n ^ max);
        return (setBit(xorValue));
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
         int n = 27, k = 3;
         System.out.println("Min Flips = "+
                             minFlip(n, k));
    }
}

// This code is contributed by Arnav Kr. Mandal.   
```

## 蟒蛇 3

```
# Python3 for finding min flip
# for maximizing given n
import math

# function for finding set bit
def setBit(xorValue):

    count = 0
    while (xorValue):
        if (xorValue % 2):
            count += 1

        xorValue = int(xorValue / 2)

    # return count
    # of set bit
    return count

# function for
# finding min flip
def minFlip(n, k):

    # number of bits in n
    size = int(math.log(n) /
               math.log(2) + 1)

    # Find the largest number of
    # same size with k set bits
    max = pow(2, k) - 1
    max = max << (size - k)

    # Count bit differences to
    # find required flipping.
    xorValue = (n ^ max)
    return (setBit(xorValue))

# Driver Code
n = 27
k = 3
print("Min Flips = " ,
        minFlip(n, k))

# This code is contributed
# by Smitha
```

## C#

```
// C# Code to find Minimum flips required
// to maximize a number with k set bits
using System;

class GFG {

    // function for finding set bit
    static int setBit(int xorValue)
    {
        int count = 0;
        while (xorValue >= 1) {
            if (xorValue % 2 == 1)
                count++;

            xorValue /= 2;
        }

        // return count of set bit
        return count;
    }

    // function for finding min flip
    static int minFlip(int n, int k)
    {
        // number of bits in n
        int size = (int)(Math.Log(n) /
                         Math.Log(2)) + 1;

        // Find the largest number of
        // same size with k set bits
        int max = (int)Math.Pow(2, k) - 1;
        max = max << (size - k);

        // Count bit differences to find
        // required flipping.
        int xorValue = (n ^ max);
        return (setBit(xorValue));
    }

    // Driver Code
    public static void Main()
    {
        int n = 27, k = 3;
        Console.Write("Min Flips = "+ minFlip(n, k));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP for finding min flip
// for maximizing given n

// function for finding set bit
function setBit($xorValue)
{
    $count = 0;
    while ($xorValue)
    {
        if ($xorValue % 2)
            $count++;

        $xorValue /= 2;
    }

    // return count of set bit
    return $count;
}

// function for finding min flip
function minFlip($n, $k)
{
    // number of bits in n
    $size = log($n) + 1;

    // Find the largest number of
    // same size with k set bits
    $max = pow(2, $k) - 1;
    $max = $max << ($size - $k);

    // Count bit differences to find
    // required flipping.
    $xorValue = ($n ^ $max);
    return (setBit($xorValue));
}

// Driver Code
$n = 27; $k = 3;
echo "Min Flips = " , minFlip($n, $k);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// Javascript for finding min flip
// for maximizing given n

// function for finding set bit
function setBit( xorValue)
{
    var count = 0;
    while (xorValue) {
        if (xorValue % 2)
            count++;

        xorValue = parseInt(xorValue / 2);
    }

    // return count of set bit
    return count;
}

// function for finding min flip
function minFlip(n, k)
{  

    // number of bits in n
    var size = Math.log2(n) + 1;

    // Find the largest number of
    // same size with k set bits
    var max = Math.pow(2, k) - 1;   
    max = (max << (size - k));

    // Count bit differences to find
    // required flipping.
    var xorValue = (n ^ max);
    return (setBit(xorValue));
}

// driver program
var n = 27, k = 3;
document.write( "Min Flips = " + minFlip(n, k));

// This code is contributed by itsok.
</script>
```

**输出:**

```
Min Flips = 3
```

本文由[**Shivam Pradhan(anuj _ charm)**](http://www.facebook.com/ma5ter6it)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。