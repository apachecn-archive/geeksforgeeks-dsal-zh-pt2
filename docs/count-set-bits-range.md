# 在一定范围内计数设定位

> 原文:[https://www.geeksforgeeks.org/count-set-bits-range/](https://www.geeksforgeeks.org/count-set-bits-range/)

给定一个非负数 **n** 和两个值 **l** 和 **r** 。问题是在 **n** 的二进制表示中对 **l** 到 **r** 范围内的置位位数进行计数，即从最右边的 **lth** 位计数到最右边的 **rth** 位。
**约束:** 1 < = l < = r < =二进制表示的位数 **n** 。
示例:

```
Input : n = 42, l = 2, r = 5
Output : 2
(42)<sub>10</sub> = (101010)2
There are '2' set bits in the range 2 to 5.

Input : n = 79, l = 1, r = 4
Output : 4
```

**进场:**以下为步骤:

1.  计算**num**=((1<<r)–1)^((1<<(l-1))–1)。这将产生一个数字**号**，其具有 **r** 数量的比特，并且范围 **l** 到 **r** 中的比特是唯一设置的比特。
2.  计数 **(n &数)**中的设定位数。参考[这篇](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)帖子。

## C++

```
// C++ implementation to count set bits in the
// given range
#include <bits/stdc++.h>

using namespace std;

// Function to get no of set bits in the
// binary representation of 'n'
unsigned int countSetBits(int n)
{
    unsigned int count = 0;
    while (n) {
        n &= (n - 1);
        count++;
    }
    return count;
}

// function to count set bits in the given range
unsigned int countSetBitsInGivenRange(unsigned int n,
                       unsigned int l, unsigned int r)
{
    // calculating a number 'num' having 'r' number
    // of bits and bits in the range l to r are the
    // only set bits
    int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

    // returns number of set bits in the range
    // 'l' to 'r' in 'n'
    return countSetBits(n & num);
}

// Driver program to test above
int main()
{
    unsigned int n = 42;
    unsigned int l = 2, r = 5;
    cout << countSetBitsInGivenRange(n, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count set bits in the
// given range
class GFG {

    // Function to get no of set bits in the
    // binary representation of 'n'
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0) {
            n &= (n - 1);
            count++;
        }

        return count;
    }

    // function to count set bits in the given range
    static int countSetBitsInGivenRange(int n, int l, int r)
    {

        // calculating a number 'num' having 'r' number
        // of bits and bits in the range l to r are the
        // only set bits
        int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

        // returns number of set bits in the range
        // 'l' to 'r' in 'n'
        return countSetBits(n & num);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 42;
        int l = 2, r = 5;

        System.out.print(countSetBitsInGivenRange(n, l, r));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 implementation to count
# set bits in the given range

# Function to get no of set bits in the
# binary representation of 'n'
def countSetBits(n):
    count = 0
    while (n):
        n &= (n - 1)
        count = count + 1

    return count

# function to count set bits in
# the given range
def countSetBitsInGivenRange(n, l,  r):

    # calculating a number 'num' having
    # 'r' number of bits and bits in the
    # range l to r are the  only set bits
    num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1)

    # returns number of set bits in the range
    # 'l' to 'r' in 'n'
    return countSetBits(n & num)

# Driver program to test above
n = 42
l = 2
r = 5
ans = countSetBitsInGivenRange(n, l, r)
print (ans)

# This code is contributed by Saloni Gupta.
```

## C#

```
// C# implementation to count set bits in the
// given range
using System;

class GFG {

    // Function to get no of set bits in the
    // binary representation of 'n'
    static int countSetBits(int n)
    {
        int count = 0;

        while (n>0) {
            n &= (n - 1);
            count++;
        }

        return count;
    }

    // function to count set bits in the given range
    static int countSetBitsInGivenRange(int n,
                                       int l, int r)
    {

        // calculating a number 'num' having 'r' number
        // of bits and bits in the range l to r are the
        // only set bits
        int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

        // returns number of set bits in the range
        // 'l' to 'r' in 'n'
        return countSetBits(n & num);
    }

    //Driver code
    public static void Main()
    {
        int n = 42;
        int l = 2, r = 5;

        Console.WriteLine(countSetBitsInGivenRange(n, l, r));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count
// set bits in the given range

// Function to get no of set bits in
// the binary representation of 'n'
function countSetBits($n)
{
    $count = 0;
    while ($n)
    {
        $n &= ($n - 1);
        $count++;
    }
    return $count;
}

// function to count set
// bits in the given range
function countSetBitsInGivenRange($n, $l, $r)
{

    // calculating a number 'num'
    // having 'r' number of bits
    // and bits in the range l to
    // r are the only set bits
    $num = ((1 << $r) - 1) ^
           ((1 << ($l - 1)) - 1);

    // returns number of
    // set bits in the range
    // 'l' to 'r' in 'n'
    return countSetBits($n & $num);
}

    // Driver Code
    $n = 42;
    $l = 2;
    $r = 5;
    echo countSetBitsInGivenRange($n, $l, $r);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to
// count set bits in the
// given range

 // Function to get no of set bits in the
    // binary representation of 'n'
    function countSetBits(n)
    {
        let count = 0;
        while (n > 0) {
            n &= (n - 1);
            count++;
        }

        return count;
    }

    // function to count set
    // bits in the given range
    function countSetBitsInGivenRange(n, l, r)
    {

        // calculating a number 'num'
        // having 'r' number
        // of bits and bits in the
        // range l to r are the
        // only set bits
        let num = ((1 << r) - 1) ^
                   ((1 << (l - 1)) - 1);

        // returns number of set
        // bits in the range
        // 'l' to 'r' in 'n'
        return countSetBits(n & num);
    }

// driver program

        let n = 42;
        let l = 2, r = 5;

     document.write(countSetBitsInGivenRange(n, l, r));

</script>
```

**输出:**

```
2
```

本文由 [**阿育什·乔哈里**](https://auth.geeksforgeeks.org/profile.php?user=ayushjauhari14) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。