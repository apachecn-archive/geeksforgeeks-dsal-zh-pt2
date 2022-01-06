# 不使用算术运算符的十进制到二进制转换

> 原文:[https://www . geesforgeks . org/十进制-二进制-转换-不使用算术运算符/](https://www.geeksforgeeks.org/decimal-binary-conversion-without-using-arithmetic-operators/)

不使用算术运算符，求给定非负数 **n** 的二进制等价数。
**例:**

```
Input : n = 10
Output : 1010

Input : n = 38
Output : 100110
```

请注意，下面的+ in 算法/程序用于连接目的。
**算法:**

```
decToBin(n)
    if n == 0
        return "0"
    Declare bin = ""
    Declare ch
    while n > 0
        if (n & 1) == 0
            ch = '0'
        else
            ch = '1'
        bin = ch + bin
        n = n >> 1
    return bin
```

## C++

```
// C++ implementation of decimal to binary conversion
// without using arithmetic operators
#include <bits/stdc++.h>

using namespace std;

// function for decimal to binary conversion
// without using arithmetic operators
string decToBin(int n)
{
    if (n == 0)
        return "0";

    // to store the binary equivalent of decimal
    string bin = "";   
    while (n > 0)   
    {
        // to get the last binary digit of the number 'n'
        // and accumulate it at the beginning of 'bin'
        bin = ((n & 1) == 0 ? '0' : '1') + bin;

        // right shift 'n' by 1
        n >>= 1;
    }

    // required binary number
    return bin;
}

// Driver program to test above
int main()
{
    int n = 38;
    cout << decToBin(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of decimal
// to binary conversion without
// using arithmetic operators
import java.io.*;

class GFG {

    // function for decimal to
    // binary conversion without
    // using arithmetic operators
    static String decToBin(int n)
    {
        if (n == 0)
            return "0";

        // to store the binary
        // equivalent of decimal
        String bin = "";

        while (n > 0)
        {
            // to get the last binary digit
            // of the number 'n' and accumulate
            // it at the beginning of 'bin'
            bin = ((n & 1) == 0 ? '0' : '1') + bin;

            // right shift 'n' by 1
            n >>= 1;
        }

        // required binary number
        return bin;
    }

    // Driver program to test above
    public static void main (String[] args) {

    int n = 38;
    System.out.println(decToBin(n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 implementation of
# decimal to binary conversion
# without using arithmetic operators

# function for decimal to
# binary conversion without
# using arithmetic operators
def decToBin(n):
    if(n == 0):
        return "0";

    # to store the binary
    # equivalent of decimal
    bin = "";

    while (n > 0):

        # to get the last binary
        # digit of the number 'n'
        # and accumulate it at
        # the beginning of 'bin'
        if (n & 1 == 0):
            bin = '0' + bin;
        else:
            bin = '1' + bin;

        # right shift 'n' by 1
        n = n >> 1;

    # required binary number
    return bin;

# Driver Code
n = 38;
print(decToBin(n));

# This code is contributed
# by mits
```

## C#

```
// C# implementation of decimal
// to binary conversion without
// using arithmetic operators
using System;

class GFG {

    // function for decimal to
    // binary conversion without
    // using arithmetic operators
    static String decToBin(int n)
    {
        if (n == 0)
            return "0";

        // to store the binary
        // equivalent of decimal
        String bin = "";

        while (n > 0) {

            // to get the last binary digit
            // of the number 'n' and accumulate
            // it at the beginning of 'bin'
            bin = ((n & 1) == 0 ? '0' : '1') + bin;

            // right shift 'n' by 1
            n >>= 1;
        }

        // required binary number
        return bin;
    }

    // Driver program to test above
    public static void Main()
    {

        int n = 38;
        Console.WriteLine(decToBin(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of decimal
// to binary conversion without
// using arithmetic operators

// function for decimal to
// binary conversion without
// using arithmetic operators
function decToBin($n)
{
    if ($n == 0)
        return "0";

    // to store the binary
    // equivalent of decimal
    $bin = "";
    while ($n > 0)
    {
        // to get the last binary
        // digit of the number 'n'
        // and accumulate it at
        // the beginning of 'bin'
        $bin = (($n & 1) == 0 ?
                          '0' : '1') . $bin;

        // right shift 'n' by 1
        $n >>= 1;
    }

    // required binary number
    return $bin;
}

// Driver Code
$n = 38;
echo decToBin($n);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>
// javascript implementation of decimal
// to binary conversion without
// using arithmetic operators

// function for decimal to
// binary conversion without
// using arithmetic operators
function decToBin(n)
{
    if (n == 0)
        return "0";

    // to store the binary
    // equivalent of decimal
    var bin = "";

    while (n > 0)
    {
        // to get the last binary digit
        // of the number 'n' and accumulate
        // it at the beginning of 'bin'
        bin = ((n & 1) == 0 ? '0' : '1') + bin;

        // right shift 'n' by 1
        n >>= 1;
    }

    // required binary number
    return bin;
}

// Driver program to test above
var n = 38;
document.write(decToBin(n));

// This code is contributed by shikhasingrajput
</script>
```

**输出:**

```
100110
```

**时间复杂度:** O(num)，其中 **num** 是 **n** 二进制表示的位数。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。