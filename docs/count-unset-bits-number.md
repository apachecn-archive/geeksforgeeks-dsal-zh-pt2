# 计数一个数字的未设置位

> 原文:[https://www.geeksforgeeks.org/count-unset-bits-number/](https://www.geeksforgeeks.org/count-unset-bits-number/)

给定一个数字 n，计算 MSB(最高有效位)后的未设置位。
**例:**

```
Input : 17
Output : 3
Binary of 17 is 10001
so unset bit is 3

Input : 7
Output : 0
```

一个**简单的解决方案**是遍历所有的位并计算未设置的位。

## C++

```
// C++ program to count unset bits in an integer
#include <iostream>
using namespace std;

int countunsetbits(int n)
{
    int count = 0;

    // x holds one set digit at a time
    // starting from LSB to MSB of n.
    for (int x = 1; x <= n; x = x<<1)
        if ((x & n) == 0)
            count++;    

    return count;
}

// Driver code
int main()
{
    int n = 17;
    cout << countunsetbits(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to Count unset bits in a number
class GFG {

    public static int countunsetbits(int n)
    {
        int count = 0;

        // x holds one set digit at a time
        // starting from LSB to MSB of n.
        for (int x = 1; x <= n; x = x<<1)
            if ((x & n) == 0)
                count++;    

        return count;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n = 17;
        System.out.println(countunsetbits(n));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python 3 program to count unset
# bits in an integer

def countunsetbits(n):
    count = 0

    # x holds one set digit at a time
    # starting from LSB to MSB of n.
    x = 1
    while(x < n + 1):
        if ((x & n) == 0):
            count += 1
        x = x << 1

    return count

# Driver code
if __name__ == '__main__':
    n = 17
    print(countunsetbits(n))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# Code to Count unset
// bits in a number
using System;

class GFG {

    // Function to count unset bits
    public static int countunsetbits(int n)
    {
        int count = 0;

        // x holds one set digit at a time
        // starting from LSB to MSB of n.
        for (int x = 1; x <= n; x = x << 1)
            if ((x & n) == 0)
                count++;    

        return count;
    }

    // Driver Code
    public static void Main()
    {
        int n = 17;
        Console.Write(countunsetbits(n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHp program to count
// unset bits in an integer
function countunsetbits($n)
{
    $count = 0;

    // x holds one set digit
    // at a time starting
    // from LSB to MSB of n.
    for ($x = 1; $x <= $n;
         $x = $x << 1)
        if (($x & $n) == 0)
            $count++;    

    return $count;
}

// Driver code
$n = 17;
echo countunsetbits($n);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to count unset bits in an integer

function countunsetbits(n)
{
    var count = 0;

    // x holds one set digit at a time
    // starting from LSB to MSB of n.
    for (var x = 1; x <= n; x = x<<1)
        if ((x & n) == 0)
            count++;    

    return count;
}

// Driver code
var n = 17;
document.write(countunsetbits(n));

</script>
```

**输出:**

```
3
```

以上解的复杂度为 **log(n)** 。
**高效解决方案:**
想法是在 O(1)时间内切换位。然后应用在[计数设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)文章中讨论的任何方法。
在 GCC 中，我们可以使用 __builtin_popcount()直接对集合位进行计数。首先[切换位](https://www.geeksforgeeks.org/toggle-bits-significant-bit/)，然后应用上述函数 __builtin_popcount()。

## C++

```
// An optimized C++ program to count unset bits
// in an integer.
#include <iostream>
using namespace std;

int countUnsetBits(int n)
{
    int x = n;

    // Make all bits set MSB 
    // (including MSB)

    // This makes sure two bits
    // (From MSB and including MSB)
    // are set
    n |= n >> 1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set
    n |= n >> 2;

    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // Count set bits in toggled number
    return  __builtin_popcount(x ^ n);
}

// Driver code
int main()
{
    int n = 17;
    cout << countUnsetBits(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An optimized Java program to count unset bits
// in an integer.
class GFG
{

static int countUnsetBits(int n)
{
    int x = n;

    // Make all bits set MSB
    // (including MSB)

    // This makes sure two bits
    // (From MSB and including MSB)
    // are set
    n |= n >> 1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set
    n |= n >> 2;

    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // Count set bits in toggled number
    return Integer.bitCount(x^ n);
}

// Driver code
public static void main(String[] args)
{
    int n = 17;
    System.out.println(countUnsetBits(n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# An optimized Python program to count
# unset bits in an integer.
import math

def countUnsetBits(n):
    x = n

    # Make all bits set MSB(including MSB)

    # This makes sure two bits(From MSB
    # and including MSB) are set
    n |= n >> 1

    # This makes sure 4 bits(From MSB and
    # including MSB) are set
    n |= n >> 2

    n |= n >> 4
    n |= n >> 8
    n |= n >> 16

    t = math.log(x ^ n, 2)

    # Count set bits in toggled number
    return math.floor(t)

# Driver code
n = 17
print(countUnsetBits(n))

# This code is contributed 29AjayKumar
```

## C#

```
// An optimized C# program to count unset bits
// in an integer.
using System;

class GFG
{

static int countUnsetBits(int n)
{
    int x = n;

    // Make all bits set MSB
    // (including MSB)

    // This makes sure two bits
    // (From MSB and including MSB)
    // are set
    n |= n >> 1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set
    n |= n >> 2;

    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // Count set bits in toggled number
    return BitCount(x^ n);
}

static int BitCount(long x)
{

    // To store the count
    // of set bits
    int setBits = 0;
    while (x != 0) {
        x = x & (x - 1);
        setBits++;
    }

    return setBits;
}

// Driver code
public static void Main(String[] args)
{
    int n = 17;
    Console.WriteLine(countUnsetBits(n));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An optimized PHP program
// to count unset bits in
// an integer.

function countUnsetBits($n)
{
    $x = $n;

    // Make all bits set 
    // MSB(including MSB)

    // This makes sure two
    // bits(From MSB and
    // including MSB) are set
    $n |= $n >> 1;

    // This makes sure 4
    // bits(From MSB and
    // including MSB) are set
    $n |= $n >> 2;

    $n |= $n >> 4;
    $n |= $n >> 8;
    $n |= $n >> 16;

    $t = log($x ^ $n,2);

    // Count set bits
    // in toggled number
    return floor($t);
}

// Driver code
$n = 17;
echo countUnsetBits($n);

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to count unset bits
// in an integer.

function countUnsetBits(n)
{
    let x = n;

    // Make all bits set MSB
    // (including MSB)

    // This makes sure two bits
    // (From MSB and including MSB)
    // are set
    n |= n >> 1;

    // This makes sure 4 bits
    // (From MSB and including MSB)
    // are set
    n |= n >> 2;

    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // Count set bits in toggled number
    return BitCount(x^ n);
}

function BitCount(x)
{

    // To store the count
    // of set bits
    let setBits = 0;
    while (x != 0) {
        x = x & (x - 1);
        setBits++;
    }

    return setBits;
}

// Driver Code

    let n = 17;
    document.write(countUnsetBits(n));

// This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
3
```

本文由**德万舒·阿加瓦尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。