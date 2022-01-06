# 计算与 n 异或产生更大值的较小数字

> 原文:[https://www . geeksforgeeks . org/count-small-numbers-what-xor-n-产生-more-value/](https://www.geeksforgeeks.org/count-smaller-numbers-whose-xor-n-produces-greater-value/)

给定一个正整数 n，对 x 进行计数，使得 0 < x <n and="" x="">n，其中^是按位异或运算。
示例:</n> 

```
Input  : n = 12
Output : 3
Numbers are 1, 2 and 3
1^12 > 12,  2^12 > 12 and 3^12 > 12

Input  : n = 11
Output : 4
Numbers are 4, 5, 6 and 7
```

如果 x 在 n 为 0 的位置有一个置位位，则数字 x 可以产生一个更大的异或值。所以我们遍历 n 个比特，一个接一个地考虑所有的 0 比特。对于位置 k 处的每个设置位(考虑最右边的位 k = 0，第二个最右边的位 k = 1，..)，我们给结果加 2 ^ 2<sup>k</sup>。对于第 k 个位置的一个位，有 2 个 <sup>k</sup> 号，设置位 1。
下面是上述想法的实现。

## C++

```
// C++ program to count numbers whose XOR with n
// produces a value more than n.
#include<bits/stdc++.h>
using namespace std;

int countNumbers(int n)
{
    /* If there is a number like m = 11110000,
    then it is bigger then 1110xxxx. x can either
    0 or 1\. So we have pow(2, k) greater numbers
    where k is  position of rightmost 1 in m. Now
    by using XOR bit at each  position can be changed.
    To change bit at any position, it needs to XOR
    it with 1\. */
    int k = 0; // Position of current bit in n

    /* Traverse bits from LSB (least significant bit)
       to MSB */
    int count = 0;  // Initialize result
    while (n > 0)
    {
        // If current bit is 0, then there are
        // 2^k numbers with current bit 1 and
        // whose XOR with n produces greater value
        if ((n&1) == 0)
            count += pow(2, k);

        // Increase position for next bit
        k += 1;

        // Reduce n to find next bit
        n >>= 1;
    }

    return count;
}

// Driver code
int main()
{
    int n = 11;
    cout << countNumbers(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers
// whose XOR with n produces a
// value more than n.
import java.lang.*;
class GFG {

    static int countNumbers(int n)
    {

        // If there is a number like
        // m = 11110000, then it is
        // bigger than 1110xxxx. x
        // can either be 0 or 1\. So
        // where k is the position of
        // rightmost 1 in m. Now by
        // using the XOR bit at each
        // position can be changed.
        // To change the bit at any
        // position, it needs to
        // XOR it with 1.
        int k = 0;
        // Position of current bit in n

        // Traverse bits from LSB (least
        // significant bit) to MSB

        int count = 0;
        // Initialize result
        while (n > 0) {
            // If the current bit is 0, then
            // there are 2^k numbers with
            // current bit 1 and whose XOR
            // with n produces greater value
            if ((n & 1) == 0)
                count += (int)(Math.pow(2, k));

            // Increase position for next bit
            k += 1;

            // Reduce n to find next bit
            n >>= 1;
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 11;
        System.out.println(countNumbers(n));
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python program to count numbers whose
# XOR with n produces a value more than n.

def countNumbers(n):

    ''' If there is a number like m = 11110000,
    then it is bigger then 1110xxxx. x can either
    0 or 1\. So we have pow(2, k) greater numbers
    where k is position of rightmost 1 in m. Now
    by using XOR bit at each position can be changed.
    To change bit at any position, it needs to XOR
    it with 1\. '''

    # Position of current bit in n
    k = 0

    # Traverse bits from
    # LSB to MSB
    count = 0 # Initialize result
    while (n > 0):

        # If current bit is 0, then there are
        # 2^k numbers with current bit 1 and
        # whose XOR with n produces greater value
        if ((n & 1) == 0):
            count += pow(2, k)

        # Increase position for next bit
        k += 1

        # Reduce n to find next bit
        n >>= 1

    return count

# Driver code
n = 11
print(countNumbers(n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to count numbers
// whose XOR with n produces a
// value more than n.
using System;

class GFG {

    static int countNumbers(int n)
    {

        // If there is a number like
        // m = 11110000, then it is
        // bigger than 1110xxxx. x
        // can either be 0 or 1\. So
        // where k is the position of
        // rightmost 1 in m. Now by
        // using the XOR bit at each
        // position can be changed.
        // To change the bit at any
        // position, it needs to
        // XOR it with 1.
        int k = 0;
        // Position of current bit in n

        // Traverse bits from LSB (least
        // significant bit) to MSB

        int count = 0;
        // Initialize result
        while (n > 0) {
            // If the current bit is 0, then
            // there are 2^k numbers with
            // current bit 1 and whose XOR
            // with n produces greater value
            if ((n & 1) == 0)
                count += (int)(Math.Pow(2, k));

            // Increase position for next bit
            k += 1;

            // Reduce n to find next bit
            n >>= 1;
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        int n = 11;
        Console.WriteLine(countNumbers(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// numbers whose XOR with n
// produces a value more than n.

function countNumbers($n)
{

    /* If there is a number
       like m = 11110000,
       then it is bigger
       then 1110xxxx. x
       can either 0 or 1.
       So we have pow(2, k)
       greater numbers where
       k is position of
       rightmost 1 in m.
       Now by using XOR bit
       at each position can
       be changed. To change
       bit at any position,
       it needs to XOR it
       with 1\. */

    // Position of current bit in n
    $k = 0;

    /* Traverse bits from LSB
       (least significant bit)
       to MSB */

    // Initialize result  
    $count = 0;
    while ($n > 0)
    {

        // If current bit is 0,
        // then there are 2^k
        // numbers with current
        // bit 1 and whose XOR
        // with n produces greater
        // value
        if (($n & 1) == 0)
            $count += pow(2, $k);

        // Increase position
        // for next bit
        $k += 1;

        // Reduce n to
        // find next bit
        $n >>= 1;
    }

    return $count;
}

    // Driver code
    $n = 11;
    echo countNumbers($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program  to count numbers whose XOR with n
// produces a value more than n.

    function countNumbers(n)
    {

        // If there is a number like
        // m = 11110000, then it is
        // bigger than 1110xxxx. x
        // can either be 0 or 1\. So
        // where k is the position of
        // rightmost 1 in m. Now by
        // using the XOR bit at each
        // position can be changed.
        // To change the bit at any
        // position, it needs to
        // XOR it with 1.
        let k = 0;
        // Position of current bit in n

        // Traverse bits from LSB (least
        // significant bit) to MSB

        let count = 0;
        // Initialize result
        while (n > 0) {
            // If the current bit is 0, then
            // there are 2^k numbers with
            // current bit 1 and whose XOR
            // with n produces greater value
            if ((n & 1) == 0)
                count += (Math.pow(2, k));

            // Increase position for next bit
            k += 1;

            // Reduce n to find next bit
            n >>= 1;
        }

        return count;
    }

// Driver Code

    let n = 11;
    document.write(countNumbers(n));

</script>
```

**输出:**

```
4
```

时间复杂度:O(Log n)
本文由 **Smarak Chopdar** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。