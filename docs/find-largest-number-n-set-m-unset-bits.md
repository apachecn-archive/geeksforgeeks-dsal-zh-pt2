# 找到 n 个设置位和 m 个未设置位的最大数字

> 原文:[https://www . geesforgeks . org/find-最大数字-n-set-m-unset-bits/](https://www.geeksforgeeks.org/find-largest-number-n-set-m-unset-bits/)

给定两个非负数 **n** 和 **m** 。问题是找到在其二进制表示中具有 **n** 个设置位和 **m** 个未设置位的最大数。
**注:**二进制表示中前导 1(或最左边 1)前的 0 位计数
**约束:** 1 < = n，0 < = m，(m+n) < = 31
**示例:**

```
Input : n = 2, m = 2
Output : 12
(12)<sub>10</sub> = (1100)2
We can see that in the binary representation of 12 
there are 2 set and 2 unsets bits and it is the largest number. 

Input : n = 4, m = 1
Output : 30
```

以下是步骤:

1.  计算**数**=(1<<(n+m))–1。这将产生具有 **(n + m)** 比特数的数字**数**，并且所有比特都被设置。
2.  现在，切换**数**的最后 **m** 位，然后返回切换后的数字。参考[这篇](https://www.geeksforgeeks.org/toggle-last-m-bits/)帖子。

## C++

```
// C++ implementation to find the largest number
// with n set and m unset bits
#include <bits/stdc++.h>

using namespace std;

// function to toggle the last m bits
unsigned int toggleLastMBits(unsigned int n,
                            unsigned int m)
{
    // if no bits are required to be toggled
    if (m == 0)
        return n;

    // calculating a number 'num' having 'm' bits
    // and all are set
    unsigned int num = (1 << m) - 1;

    // toggle the last m bits and return the number
    return (n ^ num);
}

// function to find the largest number
// with n set and m unset bits
unsigned int largeNumWithNSetAndMUnsetBits(unsigned int n,
                                        unsigned int m)
{
    // calculating a number 'num' having '(n+m)' bits
    // and all are set
    unsigned int num = (1 << (n + m)) - 1;

    // required largest number
    return toggleLastMBits(num, m);
}

// Driver program to test above
int main()
{
    unsigned int n = 2, m = 2;
    cout << largeNumWithNSetAndMUnsetBits(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the largest number
// with n set and m unset bits
import java.io.*;

class GFG
{
    // Function to toggle the last m bits
    static int toggleLastMBits(int n, int m)
    {
        // if no bits are required to be toggled
        if (m == 0)
            return n;

        // calculating a number 'num' having 'm' bits
        // and all are set
        int num = (1 << m) - 1;

        // toggle the last m bits and return the number
        return (n ^ num);
    }

    // Function to find the largest number
    // with n set and m unset bits
    static int largeNumWithNSetAndMUnsetBits(int n, int m)
    {
        // calculating a number 'num' having '(n+m)' bits
        // and all are set
        int num = (1 << (n + m)) - 1;

        // required largest number
        return toggleLastMBits(num, m);
    }

    // driver program
    public static void main (String[] args)
    {
        int n = 2, m = 2;
        System.out.println(largeNumWithNSetAndMUnsetBits(n, m));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python implementation to
# find the largest number
# with n set and m unset bits

# function to toggle
# the last m bits
def toggleLastMBits(n,m):

    # if no bits are required
    # to be toggled
    if (m == 0):
        return n

    # calculating a number
    # 'num' having 'm' bits
    # and all are set
    num = (1 << m) - 1

    # toggle the last m bits
    # and return the number
    return (n ^ num)

# function to find
# the largest number
# with n set and m unset bits
def largeNumWithNSetAndMUnsetBits(n,m):

    # calculating a number
    # 'num' having '(n+m)' bits
    # and all are set
    num = (1 << (n + m)) - 1

    # required largest number
    return toggleLastMBits(num, m)

# Driver code

n = 2
m = 2

print(largeNumWithNSetAndMUnsetBits(n, m))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# implementation to find the largest number
// with n set and m unset bits
using System;

class GFG
{
    // Function to toggle the last m bits
    static int toggleLastMBits(int n, int m)
    {
        // if no bits are required to be toggled
        if (m == 0)
            return n;

        // calculating a number 'num' having 'm' bits
        // and all are set
        int num = (1 << m) - 1;

        // toggle the last m bits and return the number
        return (n ^ num);
    }

    // Function to find the largest number
    // with n set and m unset bits
    static int largeNumWithNSetAndMUnsetBits(int n, int m)
    {
        // calculating a number 'num' having '(n+m)' bits
        // and all are set
        int num = (1 << (n + m)) - 1;

        // required largest number
        return toggleLastMBits(num, m);
    }

    // Driver program
    public static void Main ()
    {
        int n = 2, m = 2;
        Console.Write(largeNumWithNSetAndMUnsetBits(n, m));
    }

}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// the largest number with n
// set and m unset bits

// function to toggle
// the last m bits
function toggleLastMBits($n, $m)
{
    // if no bits are required
    // to be toggled
    if ($m == 0)
        return $n;

    // calculating a number 'num'
    // having 'm' bits and all are set
    $num = (1 << $m) - 1;

    // toggle the last m bits
    // and return the number
    return ($n ^ $num);
}

// function to find the largest number
// with n set and m unset bits
function largeNumWithNSetAndMUnsetBits($n,
                                       $m)
{
    // calculating a number 'num'
    // having '(n+m)' bits and all are set
    $num = (1 << ($n + $m)) - 1;

    // required largest number
    return toggleLastMBits($num, $m);
}

// Driver Code
$n = 2; $m = 2;
echo largeNumWithNSetAndMUnsetBits($n, $m);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the largest number
// with n set and m unset bits

// function to toggle the last m bits
function toggleLastMBits(n, m)
{
    // if no bits are required to be toggled
    if (m == 0)
        return n;

    // calculating a number 'num' having 'm' bits
    // and all are set
    var num = (1 << m) - 1;

    // toggle the last m bits and return the number
    return (n ^ num);
}

// function to find the largest number
// with n set and m unset bits
function largeNumWithNSetAndMUnsetBits(n, m)
{
    // calculating a number 'num' having '(n+m)' bits
    // and all are set
    num = (1 << (n + m)) - 1;

    // required largest number
    return toggleLastMBits(num, m);
}

// Driver program to test above
var n = 2, m = 2;
document.write( largeNumWithNSetAndMUnsetBits(n, m));

</script>
```

**输出:**

```
12
```

对于 **n** 和 **m** 的较大值，可以使用**长 int** 和**长 int** 数据类型来生成所需的数字。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。