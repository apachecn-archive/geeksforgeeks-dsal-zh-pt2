# 对范围内未设置的位进行计数

> 原文:[https://www.geeksforgeeks.org/count-unset-bits-range/](https://www.geeksforgeeks.org/count-unset-bits-range/)

给定一个非负数 **n** 和两个值 **l** 和 **r** 。问题是计算 **n** 二进制表示中 **l** 到 **r** 范围内的未置位位数，即从最右边的 **lth** 位到最右边的 **rth** 位计算未置位位数。
示例:

```
Input : n = 42, l = 2, r = 5
Output : 2
(42)<sub>10</sub> = (101010)2
There are '2' unset bits in the range 2 to 5.

Input : n = 80, l = 1, r = 4
Output : 4
```

**进场:**以下为步骤:

1.  计算**num**=((1<<r)–1)^((1<<(l-1))–1)。这将产生一个数字**号**，其具有 **r** 数量的比特，并且范围 **l** 到 **r** 中的比特是唯一设置的比特。
2.  计数**号(n &号)**中的设定位数。参考[这篇](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)帖子。让它成为**计数**。
3.  计算**和**=(r–l+1)–计数。
4.  返回〔t0〕年〔t1〕年。

## C++

```
// C++ implementation to count unset bits in the
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

// function to count unset bits
// in the given range
unsigned int countUnsetBitsInGivenRange(unsigned int n,
                        unsigned int l, unsigned int r)
{
    // calculating a number 'num' having 'r' number
    // of bits and bits in the range l to r are the
    // only set bits
    int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

    // returns number of unset bits in the range
    // 'l' to 'r' in 'n'
    return (r - l + 1) - countSetBits(n & num);
}

// Driver program to test above
int main()
{
    unsigned int n = 80;
    unsigned int l = 1, r = 4;
    cout << countUnsetBitsInGivenRange(n, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count unset bits in the
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

    // function to count unset bits
    // in the given range
    static int countUnsetBitsInGivenRange(int n,
                                    int l, int r)
    {

        // calculating a number 'num' having 'r'
        // number of bits and bits in the range
        // l to r are the only set bits
        int num = ((1 << r) - 1) ^ ((1 <<
                                   (l - 1)) - 1);

        // returns number of unset bits in the range
        // 'l' to 'r' in 'n'
        return (r - l + 1) - countSetBits(n & num);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 80;
        int l = 1, r = 4;

        System.out.print(
            countUnsetBitsInGivenRange(n, l, r));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 implementation to count
# unset bits in the given range

# Function to get no of set bits in
# the binary representation of 'n'
def countSetBits (n):
    count = 0
    while n:
        n &= (n - 1)
        count += 1
    return count

# function to count unset bits
# in the given range
def countUnsetBitsInGivenRange (n, l, r):

    # calculating a number 'num' having
    # 'r' number of bits and bits in the
    # range l to r are the only set bits
    num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1)

    # returns number of unset bits
    # in the range 'l' to 'r' in 'n'
    return (r - l + 1) - countSetBits(n & num)

# Driver code to test above
n = 80
l = 1
r = 4
print(countUnsetBitsInGivenRange(n, l, r))

# This code is contributed by "Sharad_Bhardwaj"
```

## C#

```
// C# implementation to count unset bits in the
// given range
using System;

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

    // function to count unset bits
    // in the given range
    static int countUnsetBitsInGivenRange(int n,
                                    int l,int r)
    {

        // calculating a number 'num' having 'r'
        // number of bits and bits in the range l
        // to r are the only set bits
        int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

        // returns number of unset bits in the range
        // 'l' to 'r' in 'n'
        return (r - l + 1) - countSetBits(n & num);
    }

    //Driver code
    public static void Main()
    {
        int n = 80;
        int l = 1, r = 4;

        Console.Write(countUnsetBitsInGivenRange(n, l, r));
    }
}

//This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php implementation to count
// unset bits in the given range

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

// function to count unset
// bits in the given range
function countUnsetBitsInGivenRange($n, $l, $r)
{

    // calculating a number 'num'
    // having 'r' number
    // of bits and bits in the
    // range l to r are the
    // only set bits
    $num = ((1 << $r) - 1) ^
            ((1 << ($l - 1)) - 1);

    // returns number of unset
    // bits in the range
    // 'l' to 'r' in 'n'
    return ($r - $l + 1) -
           countSetBits($n & $num);
}

    // Driver code
    $n = 80;
    $l = 1;
    $r = 4;
    echo countUnsetBitsInGivenRange($n, $l, $r);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation to count unset bits in the
// given range

// Function to get no of set bits in the
// binary representation of 'n'
function countSetBits(n)
{
    var count = 0;
    while (n) {
        n &= (n - 1);
        count++;
    }
    return count;
}

// function to count unset bits
// in the given range
function countUnsetBitsInGivenRange(n, l, r)
{
    // calculating a number 'num' having 'r' number
    // of bits and bits in the range l to r are the
    // only set bits
    var num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

    // returns number of unset bits in the range
    // 'l' to 'r' in 'n'
    return (r - l + 1) - countSetBits(n & num);
}

// Driver program to test above
var n = 80;
var l = 1, r = 4;
document.write( countUnsetBitsInGivenRange(n, l, r));

</script>
```

**输出:**

```
4
```