# 某一范围内某一对的最大异或值

> 原文:[https://www . geeksforgeeks . org/max-xor-value-from-a-range/](https://www.geeksforgeeks.org/maximum-xor-value-of-a-pair-from-a-range/)

给定一个范围[L，R]，我们需要在这个范围内找到两个整数，使得它们的异或在两个整数的所有可能选择中是最大的。更正式地说，
给定[L，R]，求 max (A ^ B)，其中 L < = A，B
**例:**

```
Input  : L = 8
         R = 20
Output : 31
31 is XOR of 15 and 16\.  

Input  : L = 1
         R = 3
Output : 3
```

一个**简单的解决方法**就是生成所有的对，找到它们的异或值，最后返回最大的异或值。
一个**有效的解决方案**是考虑从 L 到 R 的二进制值的模式。我们可以看到从 L 到 R 的第一位要么从 0 变为 1，要么保持 1，即如果我们对最大值进行任意两个数字的异或，它们的第一位将是固定的，这将与 L 和 R 本身的异或的第一位相同。
在观察了获取第一位的技术之后，我们可以看到，如果我们对 L 和 R 进行异或运算，这个异或运算的最高有效位将告诉我们可以实现的最大值，即让 L 和 R 的异或运算是 1xx，其中 x 可以是 0 或 1，那么我们可以获得的最大异或值是 1111，因为从 L 到 R，我们有 xxx 的所有可能组合，并且总是可以从两个数字中选择这些位，使得它们的异或运算都变成 1。下面用一些例子来解释，

```
Examples 1:
L = 8    R = 20
L ^ R = (01000) ^ (10100) = (11100)
Now as L ^ R is of form (1xxxx) we
can get maximum XOR as (11111) by 
choosing A and B as 15 and 16 (01111 
and 10000)

Examples 2:
L = 16     R = 20
L ^ R = (10000) ^ (10100) = (00100)
Now as L ^ R is of form (1xx) we can 
get maximum xor as (111) by choosing  
A and B as 19 and 20 (10011 and 10100)
```

所以这个问题的解只取决于(L ^ R)的值。我们将首先计算 L^R 值，然后根据该值的最高有效位，将所有 1 相加，得到最终结果。

## C++

```
// C/C++ program to get maximum xor value
// of two numbers in a range
#include <bits/stdc++.h>
using namespace std;

// method to get maximum xor value in range [L, R]
int maxXORInRange(int L, int R)
{
    // get xor of limits
    int LXR = L ^ R;

    //  loop to get msb position of L^R
    int msbPos = 0;
    while (LXR)
    {
        msbPos++;
        LXR >>= 1;
    }

    // construct result by adding 1,
    // msbPos times
    int maxXOR = 0;
    int two = 1;
    while (msbPos--)
    {
        maxXOR += two;
        two <<= 1;
    }

    return maxXOR;
}

//  Driver code to test above methods
int main()
{
    int L = 8;
    int R = 20;
    cout << maxXORInRange(L, R) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get maximum xor value
// of two numbers in a range

class Xor
{
    // method to get maximum xor value in range [L, R]
    static int maxXORInRange(int L, int R)
    {
        // get xor of limits
        int LXR = L ^ R;

        //  loop to get msb position of L^R
        int msbPos = 0;
        while (LXR > 0)
        {
            msbPos++;
            LXR >>= 1;
        }

        // construct result by adding 1,
        // msbPos times
        int maxXOR = 0;
        int two = 1;
        while (msbPos-- >0)
        {
            maxXOR += two;
            two <<= 1;
        }

        return maxXOR;
    }

    // main function
    public static void main (String[] args)
    {
        int L = 8;
        int R = 20;
        System.out.println(maxXORInRange(L, R));
    }
}
```

## 蟒蛇 3

```
# Python3 program to get maximum xor
# value of two numbers in a range

# Method to get maximum xor
# value in range [L, R]
def maxXORInRange(L, R):

    # get xor of limits
    LXR = L ^ R

    # loop to get msb position of L^R
    msbPos = 0
    while(LXR):

        msbPos += 1
        LXR >>= 1

    # construct result by adding 1,
    # msbPos times
    maxXOR, two = 0, 1

    while (msbPos):

        maxXOR += two
        two <<= 1
        msbPos -= 1

    return maxXOR

# Driver code
L, R = 8, 20
print(maxXORInRange(L, R))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to get maximum xor
// value of two numbers in a range
using System;

class Xor
{

    // method to get maximum xor
    // value in range [L, R]
    static int maxXORInRange(int L, int R)
    {

        // get xor of limits
        int LXR = L ^ R;

        // loop to get msb position of L^R
        int msbPos = 0;
        while (LXR > 0)
        {
            msbPos++;
            LXR >>= 1;
        }

        // construct result by
        // adding 1, msbPos times
        int maxXOR = 0;
        int two = 1;
        while (msbPos-- >0)
        {
            maxXOR += two;
            two <<= 1;
        }

        return maxXOR;
    }

    // Driver code
    public static void Main()
    {
        int L = 8;
        int R = 20;
        Console.WriteLine(maxXORInRange(L, R));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get maximum
// xor value of two numbers
// in a range

// method to get maximum xor
// value in range [L, R]
function maxXORInRange($L, $R)
{
    // get xor of limits
    $LXR = $L ^ $R;

    // loop to get msb
    // position of L^R
    $msbPos = 0;
    while ($LXR)
    {
        $msbPos++;
        $LXR >>= 1;
    }

    // construct result by
    // adding 1, msbPos times
    $maxXOR = 0;
    $two = 1;
    while ($msbPos--)
    {
        $maxXOR += $two;
        $two <<= 1;
    }

    return $maxXOR;
}

// Driver Code
$L = 8;
$R = 20;
echo maxXORInRange($L, $R), "\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
    // Javascript program to get maximum xor
    // value of two numbers in a range

    // method to get maximum xor
    // value in range [L, R]
    function maxXORInRange(L, R)
    {

        // get xor of limits
        let LXR = L ^ R;

        // loop to get msb position of L^R
        let msbPos = 0;
        while (LXR > 0)
        {
            msbPos++;
            LXR >>= 1;
        }

        // construct result by
        // adding 1, msbPos times
        let maxXOR = 0;
        let two = 1;
        while (msbPos-- > 0)
        {
            maxXOR += two;
            two <<= 1;
        }

        return maxXOR;
    }

    let L = 8;
    let R = 20;
    document.write(maxXORInRange(L, R));

</script>
```

**输出:**

```
31
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。